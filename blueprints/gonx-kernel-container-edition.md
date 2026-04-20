## Instalação de Kernel customizado para conteiners, otimizado com zRAM e eliminação de serviços desnecessários

1. Faça o Download do kernel pelo link abaixo:

[![Download KERNEL GONX CE 7.0.0](https://img.shields.io/badge/Download-Forge_OS_v1.0_PROXMOX-blue?style=for-the-badge&logo=linux)](https://github.com/asyncx-labs/gonx-forge-os/releases/download/gonx-kernel-container-edition-7.0.0/gonx-kernel-7.0.0-ce.tar.xz)

2. Faça a extração

```bash
cd /sources

tar -xf gonx-kernel-7.0.0-ce.tar.xz

cd linux-7.0
```

(OPCIONAL)
Você pode checar a compatibilidade e os pacotes requiridos para containers (docker), com o comando abaixo, note que algumas funcionalidades estarão desativadas, fique à vontade para ativar as flags que achar necessário para seu projeto.

```bash
.check-config.sh .config
```

### 1. Validação de Sintaxe

```bash
make init/main.o
if [ $? -ne 0 ]; then
    echo "ERRO: Falha na sintaxe do main.c. Abortando."
    exit 1
fi
```

### 2. Preservação da Configuração

```bash
cp -v .config ../gonx_kernel_ce

make mrproper

cp -v ../gonx_kernel_ce .config

make oldconfig
```

### 3. Compilação 

```bash
make -j$(nproc) bzImage modules
if [ $? -ne 0 ]; then
    echo "ERRO: Falha na compilação do Kernel. Verifique os logs."
    exit 1
fi
```

### 4. Instalação de Módulos

```bash
make modules_install
```

### 5. Deploy

```bash
cp -v arch/x86/boot/bzImage /boot/vmlinuz-7.0.0-gonx-container-edition

cp -v System.map /boot/System.map-7.0.0-gonx-container-edition

cp -v .config /boot/config-7.0.0-gonx-container-edition

grub-mkconfig -o /boot/grub/grub.cfg
```

