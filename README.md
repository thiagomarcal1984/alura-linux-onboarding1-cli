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

# Acesso via SSH
No terminal do Linux, use o comando abaixo (note o espaço) para identificar o endereço IP da máquina convidada (VM):
```
ip addr
```
Procure na saída o texto `inet`: ele vai indicar o endereço IP.

Para acessar a máquina convidada via SSH, use o comando no prompt do Windows: `ssh usuario@servidor`:

```
C:\Users\Thiago>ssh thiago@192.168.18.254
```

O cliente SSH diz que a autenticidade do servidor acessado não pode ser estabelecida. Nesse caso temos 3 opções:
1. Continuar a conexão (yes);
2. Não continuar a conexão (no);
3. Informar a fingerprint para confirmar autenticidade ([fingerprint]).
```
The authenticity of host '192.168.18.254 (192.168.18.254)' can't be established.
ECDSA key fingerprint is SHA256:my7KuvY0YPb3Kl2twlQJsWAL3xZL8bafk2afg9gYI2g.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.18.254' (ECDSA) to the list of known hosts.
```
Depois que você continuar a conexão, informe a senha do usuário:
```
thiago@192.168.18.254's password:
Welcome to Ubuntu 22.04.2 LTS (GNU/Linux 5.15.0-70-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of qui 20 abr 2023 16:43:47 UTC

  System load:             0.046875
  Usage of /:              42.7% of 11.21GB
  Memory usage:            11%
  Swap usage:              0%
  Processes:               115
  Users logged in:         1
  IPv4 address for enp0s3: 192.168.18.254
  IPv6 address for enp0s3: 2804:2488:5084:2270:a00:27ff:fefe:8ba7


Manutenção de Segurança Expandida para Applications não está ativa.

40 as atualizações podem ser aplicadas imediatamente.
Para ver as actualizações adicionais corre o comando: apt list --upgradable

Ativar ESM Apps para poder receber possiveis futuras atualizações de segurança.
Consulte https://ubuntu.com/esm ou execute: sudo pro status


Last login: Thu Apr 20 16:37:42 2023
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

thiago@thiago-pc:~$
```

# Conhecendo o WSL
O WSL (Windows Subsystem for Linux) é uma alternativa ao VirtualBox, mas ela tem mais limitações do que VM do VirtualBox. É um jeito de usar Linux no Windows.

Consulte a documentação para instalar o WSL: https://learn.microsoft.com/pt-br/windows/wsl/install

Para instalar o WSL, execute o comando abaixo como administrador, confirme os passos e reinicie o host:

```
wsl --install
```

Depois de reiniciar, você pode acessar o WSL usando o comando:

```
wsl
```
O prompt vai ser exibido com o path atual no formato do Linux.

# Acessando o Linux remotamente

Para acessar um computador via SSH, use o comando no prompt do Windows: `ssh usuario@servidor`:

```
C:\Users\Thiago>ssh thiago@192.168.18.254
```
Depois de acessar a máquina convidada, atualize o gerenciador de pacotes apt:

```
sudo apt update
```
O `APT (Advanced Package Tool)` é a ferramenta de gerenciamento de pacotes do Debian.

O comando `sudo` significa `subsitute user do`, ou seja, executa algum comando como outro usuário (por padrão, o usuário root). Sem o sudo, a atualização do APT não é autorizada.

Exemplo de comando para instalar o servidor SSH no Ubuntu:

```
sudo apt install openssh-server
```
# Utilizando uma estância na nuvem
No curso, é mostrado um exemplo de acesso a uma máquina da AWS (^^à qual não temos acesso).

Mas o destaque é para o parâmetro `-i` do comando `ssh`: ele recebe o caminho para o arquivo de identificação do usuário (identity_file).
```
ssh -i "path/para/arquivo.pem" usario@servidor.com
```

# As limitações do WSL
O WSL não é utilizado em ambientes de produção, onde temos que rodar uma aplicação o tempo todo, já que o próprio Windows não é muito utilizado, e o WSL é uma ferramenta exclusiva do Windows. O Windows não é muito utilizado em servidores por alguns motivos, sendo os principais:

* A necessidade de uma licença paga por servidor, igual temos nos computadores pessoais, porém para o Windows Server;
* A instabilidade, principalmente nos sistemas que ficam ligados 24 horas por dia, onde vários pequenos serviços acabam acumulando erros e forçando uma reinicialização do servidor;
* As atualizações constantes que dependem de uma reinicialização do sistema para serem concluídas;
* Não ter o código aberto, impedindo que modificações legítimas sejam feitas para correção de erros, desativação de recursos ou melhorias de desempenho, atrapalhando e dificultando a execução de certas aplicações.

Com todas essas limitações, o WSL não é uma ferramenta muito comum para pessoas de DevOps, já que sua utilização em servidores não é recomendada e devemos sempre rodar e testar códigos com o ambiente mais próximo do real, porém ele acaba sendo muito popular entre pessoas que desenvolvem softwares, já que o WSL consegue rodar a maioria dos comandos padrão do Linux e é mais rápido e leve que uma máquina virtual, como as do VirtualBox.

Caso queira saber mais sobre o WSL, temos um artigo que passa por vários de seus aspectos: https://www.alura.com.br/artigos/wsl-executar-programas-comandos-linux-no-windows .
