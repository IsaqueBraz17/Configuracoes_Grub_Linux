# 🐧 Guia Definitivo: Configuração e Customização do GRUB

Bem-vindo ao guia de configuração do **GRUB (GRand Unified Bootloader)**. Este repositório serve como um manual prático para quem deseja entender, modificar, customizar e consertar o gerenciador de boot mais utilizado no ecossistema Linux.

![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white)

---

## 📑 Índice
1. [Estrutura de Arquivos](#1-estrutura-de-arquivos)
2. [Configurações Essenciais](#2-configurações-essenciais)
3. [Aplicando Mudanças](#3-aplicando-mudanças)
4. [Customização Visual](#4-customização-visual)
5. [Parâmetros do Kernel](#5-parâmetros-do-kernel)
6. [Troubleshooting (Resolução de Problemas)](#6-troubleshooting)

---

## 1. 📂 Estrutura de Arquivos

Para mexer no GRUB com segurança, você precisa conhecer três caminhos principais:

- `/etc/default/grub`: **Onde você deve fazer suas alterações.** É o arquivo de configuração principal e seguro para edição manual.
- `/etc/grub.d/`: Diretório que contém os scripts que geram o menu do GRUB. Os scripts são executados em ordem numérica (ex: `10_linux`, `30_os-prober`).
- `/boot/grub/grub.cfg`: O arquivo final gerado. **NÃO EDITE ESTE ARQUIVO DIRETAMENTE.** Ele é reescrito toda vez que o GRUB é atualizado.

---

## 2. ⚙️ Configurações Essenciais

Abra o arquivo de configuração com seu editor de texto preferido (requer privilégios de root):
'''bash
sudo nano /etc/default/grub

## 3. 🔄 Aplicando Mudanças
Sempre que você alterar o arquivo /etc/default/grub :<br />
ou adicionar um tema, é obrigatório atualizar o GRUB para gerar um novo arquivo grub.cfg.

Para sistemas baseados em Debian/Ubuntu/Mint: sudo update-grub
Para sistemas baseados em Arch/Fedora/OpenSUSE: sudo grub-mkconfig -o /boot/grub/grub.cfg

## 4. 🎨 Customização Visual
Alterando a Resolução do Menu
Se o seu GRUB estiver gigante ou muito pequeno, ajuste a resolução:<br />
# Adicione/Edite esta linha no /etc/default/grub:<br />
GRUB_GFXMODE=1920x1080x32

Colocando uma Imagem de Fundo
Você pode definir uma imagem (PNG, JPG, TGA) como plano de fundo do seu GRUB:
# Adicione esta linha apontando para sua imagem
GRUB_BACKGROUND="/caminho/para/sua/imagem.png"

Instalando Temas de Terceiros
Baixe um tema (ex: do Gnome-Look).

Extraia a pasta do tema em /boot/grub/themes/.

Edite o /etc/default/grub e aponte para o arquivo theme.txt:
GRUB_THEME="/boot/grub/themes/NomeDoTema/theme.txt"

## 5. 🛠️ Parâmetros do Kernel
A linha GRUB_CMDLINE_LINUX_DEFAULT no arquivo de configuração passa instruções diretas para o Kernel do Linux durante o boot.

Exemplos comuns:

quiet splash: Esconde os textos de inicialização e mostra a logo da sua distro (padrão em várias distribuições).

nomodeset: Essencial para resolver problemas de tela preta com placas de vídeo NVIDIA/AMD antes de instalar os drivers proprietários.

acpi=off ou noapic: Útil se o computador estiver travando na inicialização por problemas de energia.
# Exemplo de configuração para silenciar o boot e usar nomodeset
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash nomodeset"

## 6. 🚑 Troubleshooting (Resumo do Rescue Mode)
Se o GRUB quebrar e você cair na tela grub rescue>, siga os passos para dar boot manualmente:

Liste as partições disponíveis::<br />
ls:<br />
ls (hd0,msdos1)/:<br />
set prefix=(hd0,msdos1)/boot/grub:<br />
set root=(hd0,msdos1):<br />
insmod normal:<br />
normal
