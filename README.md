# gonx-forge-os

# 🛠️ Gonx Forge OS v1.0
> **A minimal, bit-by-bit Linux distribution built from scratch (LFS 12.x).**

![License](https://img.shields.io/badge/license-GPLv3-blue.svg)
![Kernel](https://img.shields.io/badge/kernel-6.13.4-black.svg)
![Status](https://img.shields.io/badge/status-stable-green.svg)

Gonx Forge OS é um "Canvas em Branco" para engenheiros de sistemas. Se você já dominou o Arch e o Gentoo, este é o seu próximo nível de domínio. Construído bit por bit, ele oferece o controle absoluto sobre a infraestrutura.

---

## ⚡ Especificações Técnicas

| Componente | Detalhe |
| :--- | :--- |
| **Base Engine** | Linux From Scratch 12.x |
| **Kernel** | 6.13.4 (Hardened Baseline) |
| **Glibc** | 2.41 |
| **Architecture** | x86_64 |
| **Init System** | Systemd (Minimal) |
| **Default Shell** | Bash (Custom ASCII MOTD) |

---

## 🚀 Como Iniciar (Proxmox / KVM)

O sistema é distribuído como uma imagem `.qcow2` otimizada para ambientes de virtualização.

1. Baixe o arquivo na seção [Releases](https://github.com/asyncx-labs/gonx-forge-os/releases).
2. Importe para o storage do seu hypervisor.
3. Crie uma VM (2GB RAM / 1 vCPU).
4. **Credenciais Padrão:**
   - **User:** `root`
   - **Pass:** `asyncx`

---

## 🛠️ Desafio de Compilação: nload

O Forge OS vem "nu" por design. Teste suas ferramentas de construção compilando seu primeiro binário:

```bash
# Baixar e extrair
wget [http://www.roland-riegel.de/nload/nload-0.7.4.tar.gz](http://www.roland-riegel.de/nload/nload-0.7.4.tar.gz) --no-check-certificate
tar -xvf nload-0.7.4.tar.gz && cd nload-0.7.4

# Compilar e Instalar
./configure --prefix=/usr && make
make install

# Executar
nload
