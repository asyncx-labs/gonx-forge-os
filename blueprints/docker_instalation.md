## Docker Instalation 

Este guia documenta o processo de implementação do Docker Engine no Gonx Forge OS, garantindo a compatibilidade de rede, segurança e isolamento de processos.

Nota: Se achar conveniente compile o gonx-kernel-container-edition para maior capacidade e velocidade nos containers

1. Iptables 1.8.10


```bash
cd /sources

wget https://www.netfilter.org/projects/iptables/files/iptables-1.8.10.tar.xz --nocheck-certificate

tar -xf iptables-1.8.10.tar.xz && cd iptables-1.8.10
```

2. Configuração para modo legacy 

```bash
./configure --prefix=/usr --disable-nftables

make -j$(nproc)

make install
```

3. Configuração de Rede (DNS)


```bash
cat > /etc/resolv.conf << "EOF"
nameserver 8.8.8.8
nameserver 1.1.1.1
EOF
```

4. Download dos Certificados Mozilla

```bash
mkdir -p /etc/ssl/certs

cd /etc/ssl/certs

wget https://curl.se/ca/cacert.pem --no-check-certificate

ln -s cacert.pem ca-certificates.crt
```

5. Deploy do Docker Engine Static Binary


Instalação 

```bash
cd /sources

wget https://download.docker.com/linux/static/stable/x86_64/docker-29.4.0.tgz --no-check-certificate

tar xzvf docker-29.4.0.tgz

cp docker/* /usr/bin/
```

6. DNS no Docker para garantir que os containers herdem a capacidade de resolução de nomes.

```bash
mkdir -p /etc/docker
cat > /etc/docker/daemon.json << "EOF"
{
  "dns": ["8.8.8.8", "1.1.1.1"]
}
EOF
```

7. Orquestração com Systemd

Criação do Service Unit

```bash
cat > /lib/systemd/system/docker.service << "EOF"
[Unit]
Description=Docker Application Container Engine
After=network-online.target

[Service]
Type=notify
ExecStart=/usr/bin/dockerd
ExecReload=/bin/kill -s HUP $MAINPID
LimitNOFILE=infinity
Delegate=yes
KillMode=process
Restart=on-failure

[Install]
WantedBy=multi-user.target
EOF
```