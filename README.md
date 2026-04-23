# Gonx Forge OS

<img width="1024" height="543" alt="Captura de tela de 2026-04-13 15-17-02" src="https://github.com/user-attachments/assets/b4c00b30-63e9-4c9a-b308-7d22a941d742" />

---

[![Download v1.2 ISO](https://img.shields.io/badge/Download-Gonx_Forge_OS_v1.2_ISO-blue?style=for-the-badge&logo=linux)](https://github.com/asyncx-labs/gonx-forge-os/releases/download/v1.2iso/gonx-forge-os-v1.2.iso)

[![Download v1.0 PROXMOX](https://img.shields.io/badge/Download-Gonx_Forge_OS_v1.0_PROXMOX-blue?style=for-the-badge&logo=linux)](https://github.com/asyncx-labs/gonx-forge-os/releases/download/v1.0.0/gonx-forge-os-v1.qcow2)

[![Download v1.0 VIRTUALBOX](https://img.shields.io/badge/Download-Gonx_Forge_OS_v1.0_VIRTUALBOX-6222C0?style=for-the-badge&logo=virtualbox&logoColor=white)](https://github.com/asyncx-labs/gonx-forge-os/releases/download/v1.0.0vbox/gonx-forge-os-v1.ova)



> **A Linux distribution built from scratch.**

![License](https://img.shields.io/badge/license-GPLv3-blue.svg)
![Kernel](https://img.shields.io/badge/kernel-6.13.4-black.svg)
![Status](https://img.shields.io/badge/status-stable-green.svg)

Gonx Forge OS é um projeto para engenheiros de sistemas. Se você já dominou o Arch e o Gentoo, este é o seu próximo nível de domínio. Construído bit por bit, ele oferece o controle absoluto sobre a infraestrutura.

---

## Especificações Técnicas

| Componente | Detalhe |
| :--- | :--- |
| **Base Engine** | LFS 12.3 Build Base |
| **Kernel** | 6.13.4 |
| **Glibc** | 2.41 |
| **Architecture** | x86_64 |
| **Init System** | Systemd |
| **Default Shell** | Bash |

---

## Instalação via ISO 
Para instalar o Gonx Forge OS de forma personalizada em discos físicos ou virtuais utilizando a mídia de instalação oficial.

1. Preparação
Baixe a ISO na seção [Releases](https://github.com/asyncx-labs/gonx-forge-os/releases).

Verifique a integridade do arquivo:
```bash
sha256sum gonx-forge-os-v1.2.iso

# 85b4c6a99843d3c61fcd10cec734a4cb6fe2abe288a2de7765219821b571974e
```
Mídia Física: Grave em um pendrive utilizando Rufus.

Virtualização:
- 512MB RAM 
- 1 vCPU 
- SATA

2. Processo de Instalação
O sistema iniciará em Modo Live. Entre com as credenciais padrão:

User: root
Pass: root

No terminal, digite o comando:
```bash
gonx-install
```
3. Siga as instruções de instalação

4. Desligue a maquina, remova a mídia de instalação e mude a ordem de boot.

5. Basta acessar sua distro instalada com usuário root e a senha definida no processo de instalação.

## Instalação no Proxmox 

Para instalar a versão `.qcow2` otimizada para ambientes de virtualização.

1. Baixe o arquivo na seção [Releases](https://github.com/asyncx-labs/gonx-forge-os/releases).
2. Verifique a integridade do arquivo baixado com o comando
```bash
sha256sum gonx-forge-os-v1.qcow2

# 55c461b6ceab362d9fda8963421ce3a27ed139e2387fc77c369b871a467528c4
```
2. Importe para o storage do seu hypervisor.
3. Crie uma VM (2GB RAM / 1 vCPU).
4. Vincule o disco com o PID da vm criada pelo shell do proxmox:

```bash
qm importdisk 100 gonx-forge-v1.qcow2 local-lvm
```
- Substitua 100 pelo ID da sua VM e local-lvm pelo nome do seu storage.
- Vá em VM > Hardware.
- Clique duas vezes em Unused Disk 0 e adicione-o como SCSI.
- Vá em VM > Options > Boot Order e coloque o novo disco como primeira opção.

5. **Credenciais Padrão:**
   - **User:** `root`
   - **Pass:** `root`

### Acesso ssh:

```bash
# Verifique o ip atribuido no bash da máquina
-bash-5.2# ip a
```

### Acesse do seu terminal com User e Pass:

```bash
ssh root@IP_ATRIBUIDO 
```
---

## Instalação no VirualBox

Para instalar a versão `.ova` pré configurada.

1. Baixe o arquivo na seção [Releases](https://github.com/asyncx-labs/gonx-forge-os/releases).
2. Verifique a integridade do arquivo baixado com o comando
```bash
sha256sum gonx-forge-os-v1.ova

# 8b73f5044d8ba716a02c62389ab4824ae9cd648c28e3528d354dfbb2c4afef76
```

3. Abra o VirtualBox e vá em Arquivo > Importar Appliance (Import Appliance).

4. Selecione o arquivo .ova e siga as instruções de importação.

- O hardware já está otimizado (2GB RAM / 1 vCPU).

- O adaptador de rede está configurado como NAT com Port Forwarding.

- Acesso via SSH em modo localhost para desenvolvimento


No terminal da sua máquina


```bash
ssh root@127.0.0.1 -p 2222

```

User: root
Pass: root

---

## Escolha um projeto

O **Gonx Forge OS** é um ecossistema aberto, que te desafia nas implementações e construção de sistemas úteis.

| **Security & Infra** | **Development & Data** |
| :--- | :--- |
| **Cybersec & CTF Lab** | **Private AI Node** |
| **Cloud Infrastructure** | **Big Data Pipeline** |
| **Hardened Server** | **Dev Sandbox (C/Rust)** |
| **Zero-Trust Gateway** | **Bare Metal Gaming** |
| **Edge Computing / IoT** | **Desktop Environment** |
| **Digital Forensics Lab** | **Firmware Reversing** |

---

## Teste inicial.

O Gonx Forge OS esta equipado somente com funcionalidades básicas por design. Teste suas ferramentas de construção compilando seu primeiro binário:

```bash
# Baixar e extrair
cd /sources && wget http://www.roland-riegel.de/nload/nload-0.7.4.tar.gz --no-check-certificate
tar -xvf nload-0.7.4.tar.gz && cd nload-0.7.4

# Compilar e Instalar
./configure --prefix=/usr && make
make install

# Executar
nload

