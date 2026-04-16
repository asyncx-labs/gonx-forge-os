<img width="1024" height="543" alt="Captura de tela de 2026-04-13 15-17-02" src="https://github.com/user-attachments/assets/b4c00b30-63e9-4c9a-b308-7d22a941d742" />

# Gonx Forge OS v1.0
[![Download v1.0](https://img.shields.io/badge/Download-Forge_OS_v1.0-blue?style=for-the-badge&logo=linux)](https://github.com/asyncx-labs/gonx-forge-os/releases/download/v1.0.0/gonx-forge-os-v1.qcow2)

> **A minimal, bit-by-bit Linux distribution built from scratch (LFS 12.3).**

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

## Como Iniciar com Proxmox 

Para instalar a versão `.qcow2` otimizada para ambientes de virtualização.

1. Baixe o arquivo na seção [Releases](https://github.com/asyncx-labs/gonx-forge-os/releases).
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

## Compile nload e teste as ferramentas de compilação

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

