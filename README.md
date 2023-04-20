# Porque aprender Linux e as principais distribuições
Histórico das distribuições do Linux: https://i.redd.it/aygzaivcbmd51.png

Distribuições em uso: https://distrowatch.com/

Atualmente, as distribuições "raiz" são:
* Debian (pai de Ubuntu, Kubuntu, Xubuntu, Linux Mint etc.);
* Slackware (pai de SUSE e OpenSUSE);
* Red Hat Enterprise (pai de Fedora, CentOS);
* Gentoo;
* Arch;
* Puppy (pai de Simplicity);
* Alpine;
* Void Linux;
* Evolve OS ou Solus;
* Android.

No curso usaremos o Ubuntu.

# VirtualBox
Download do VirtualBox: https://www.virtualbox.org/wiki/Downloads

Download do Ubuntu: https://ubuntu.com/download#download

# Criando uma máquina virtual
Configurações do hardware da nova VM: 

## Tela "Nome da máquina virtual e Sistema Operacional
* Marque a opção "Pular Instalação Desassistida" para instalar manualmente o OS na VM/máquina convidada;

## Hardware
* Memória Base RAM: 2048 MB (2 GB). Use no máximo 1/3 (um terço) da memória do host;
* Processadores: Use 2 processsadores no curso. Use até 1/3 dos núcleos disponíveis no host;

## Disco Rígido Virtual
* A opção padrão é 25GB. Vamos usar essa mesmo.

# Configurando redes na máquina virtual
Nas configurações da máquina convidada (VM) modifique o primeiro adaptador de rede:
1. Ligue a opção `Habilitar Placa de Rede`;
2. Escolha a opção `Placa em modo Bridge` (a opção anterior seria NAT);
3. O campo `Nome` indica a placa de rede que será usada. Geralmente a placa de rede deve iniciar com `Intel` ou `Realtek`. Dê preferência para as placas de rede físicas: não escolha placas de rede virtuais.

# Instalando o Linux
Passos para o Ubuntu:
1. Inicie a máquina convidada (VM);
2. Escolha o idioma (Português);
3. Escolha o layout de teclado para Portuguese Brazil;
4. Escolha como base de instalação o Ubuntu Server sem ser o minimizado. Não marque a opção de busca de drivers de terceiros;
5. Anote o número IP informado e associado à placa de rede do host (no caso, o número é 192.168.18.254/24);
6. Ignore a configuração do proxy;
7. Ignore a configuração dos mirrors;
8. Use o HD inteiro para a instalação do OS;
9. Leia o sumário e continue a instalação;
10. Defina o seu perfil:
    1. Nome: Thiago
    2. Nome do seu servidor (a-z,0-9,- ou _): thiago-pc
    3. Nome de usuário (a-z,0-9,- ou _): thiago
    4. Senha e confirmação de senha: thiago
11. Pule o "Upgrade to Ubuntu Pro";
12. Marque a opção "Install OpenSSH Server" apertando Enter, e depois confirme;
13. Pule as instalações das Featured Server Snaps (docker, postgre, powershell etc.);
14. Dê reboot na máquina convidada após o término da instalação.
