# Blueprint: Network Access & Security Stack (OpenSSH)

Este documento detalha o processo de compilação e integração da stack de acesso remoto no **Gonx Forge OS**. Diferente de distros convencionais, cada componente aqui é vinculado estaticamente às bibliotecas do sistema, garantindo integridade e performance.

## Visão Geral da Arquitetura
A implementação do serviço de SSH no Gonx segue uma cadeia de dependência linear necessária para suporte a criptografia, compressão e transferência de dados:
`ZLIB` > `OpenSSL` > `OpenSSH`.

---

## 1. ZLIB v1.3.1 

```bash
cd /sources
tar -xf zlib-1.3.1.tar.gz
cd zlib-1.3.1

./configure --prefix=/usr

make -j$(nproc)
make install

```
---
## 2. OpenSSL v3.4.1

```bash
cd /sources
tar -xf openssl-3.4.1.tar.gz
cd openssl-3.4.1

./config --prefix=/usr         \
         --openssldir=/etc/ssl \
         --libdir=lib          \
         shared                \
         zlib-dynamic

make -j$(nproc)
make install
```
---

## 3.OpenSSH v9.9p1

```bash
cd /sources
rm -rf openssh-9.9p1
tar -xf openssh-9.9p1.tar.gz
cd openssh-9.9p1

./configure --prefix=/usr                             \
            --sysconfdir=/etc/ssh                     \
            --with-md5-passwords                      \
            --with-privsep-path=/var/lib/sshd         \
            --with-default-path=/usr/bin:/bin:/usr/sbin:/sbin

make -j$(nproc)
make install
```
---

### Configurações iniciais

```bash
groupadd -g 50 sshd
useradd -c "sshd PrivSep" -d /var/lib/sshd -g sshd -s /bin/false -u 50 sshd

install -v -m700 -d /var/lib/sshd
chown -v root:sys /var/lib/sshd
```
---

### Subindo serviço no systemd

```bash
cat > /lib/systemd/system/sshd.service << "EOF"
[Unit]
Description=OpenSSH Daemon
After=network.target

[Service]
ExecStart=/usr/sbin/sshd -D
ExecReload=/bin/kill -HUP $MAINPID
KillMode=process
Restart=always

[Install]
WantedBy=multi-user.target
EOF
```
---

### Testando a sintaxe, habilitando e iniciando o Daemon

```bash
systemctl daemon-reload

systemctl enable sshd

systemctl start sshd

/usr/sbin/sshd -t

systemctl status sshd
```
---

Por padrão, o acesso via Root está configurado. Recomenda-se editar /etc/ssh/sshd_config e alterar PermitRootLogin para no após a configuração de um usuário comum com chaves SSH Ed25519.