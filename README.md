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

# SSH no Windows
Security Shell (SSH) é um protocolo de rede utilizado para oferecer acesso remoto seguro a um computador ou servidor. Para isso, o SSH estabelece uma comunicação criptografada entre um cliente e um servidor, garantindo que dados sensíveis, tais como informações pessoais e senhas, sejam protegidas contra espionagem virtual.

Podemos usar o SSH em tarefas como acesso a arquivos armazenados em outros computadores, como: execução remota de programas e gerenciamento de servidores remotos. Logo, essa ferramenta é muito usada por administradores de sistemas, desenvolvedores e profissionais de segurança.

Dessa forma, para estabelecermos uma conexão remota segura entre dois computadores, usamos o comando SSH. A sintaxe básica do comando é:
```bash
ssh [options] [user@]hostname [command]
```

Algumas opções [options] comuns são: 
* -p port: usada para especificar o número da porta adotada para a conexão. Por default, o comando SSH utiliza a porta 22. 
* -i identity_file: indica o arquivo de chave privada a ser usado na autenticação.
* -l login_name: utilizada na especificação do nome de usuário a ser usado na conexão.

Se quisermos acessar um servidor remoto, por exemplo, o comando é bem simples:

```bash
ssh username@remote_server_ip_address
```

Basta inserirmos o usuário de acesso ao servidor no campo `username` e o endereço de IP do servidor no campo `remote_server_ip_address`. Ao confirmarmos o comando apertando enter, deveremos digitar a senha de acesso do usuário indicado para estabelecermos a conexão ao servidor. Estabelecida a sessão de acesso, poderemos buscar arquivos e executar comandos no servidor. Podemos encerrar a conexão a qualquer momento digitando o comando `exit`.

Apesar de ser um procedimento simples, podemos encontrar algumas dificuldades na execução do comando SSH em algumas versões do sistema operacional Windows. Infelizmente, em algumas versões o comando não está disponível, no entanto podemos contornar esse entrave seguindo alguns passos de acordo com a versão instalada em nosso computador.

Caso estejamos utilizando o Windows 10, podemos seguir os passos abaixo:

1. Vamos abrir as configurações do Windows;
2. Acessar a aba Aplicativos;
3. Procurar por Aplicativos e Recursos;
4. Clicar na opção Recursos Opcionais;
5. Identificar se o recurso OpenSSH está incluído na lista exibida. Caso não esteja, devemos clicar na opção Adicionar um Recurso;
6. Vamos procurar a opção “Cliente SSH” e instalar o recurso em nosso computador.

Após esses passos, o comando SSH estará prontamente disponível no terminal de comando do Windows. Caso não esteja, uma boa alternativa é usarmos a próxima estratégia (acesso SSH com programa PuTTY), indicada para versões anteriores do Windows.

Pode ser que estejamos utilizando uma versão anterior do Windows, neste caso vamos instalar um programa chamado PuTTY para conseguir usar o protocolo SSH em nosso computador. Listamos uma breve sequência de passos para facilitar a utilização do PuTTY para acesso remoto:

1. Vamos acessar o website oficial do [PuTTY] (https://www.putty.org) para fazermos o download do programa. Basta acessarmos a opção “Download PuTTY” e aguardar;
2. Concluído o download do programa, vamos fazer sua instalação utilizando as configurações padrão;
3. Após a instalação, vamos abrir o programa e procurar as caixas de texto “Host name” e “Port” para configurarmos o acesso remoto. No campo “Host name” devemos inserir o IP do dispositivo que iremos acessar remotamente (computador, servidor ou máquina virtual), já no campo “Port” usamos a porta default do protocolo SSH (porta 22);
4. Uma vez configurado as opções de acesso, vamos clicar na opção “Open” que exibirá em nossa tela uma solicitação do nome do usuário de acesso. Fornecemos então o nome de usuário de acesso ao servidor ou máquina virtual e, na sequência, nos será solicitada também a senha de acesso;
5. Depois da verificação de acesso (usuário e senha), poderemos acessar o servidor ou máquina virtual de modo remoto via protocolo SSH.

# Navegando no sistema PWD e LS
Significado dos elementos do shell bash:
```
usuario@servidor:~$
thiago@thiago-pc:~$
```
* `usuario`: Nome do usuário (ex.: thiago);
* `@`: A arroba separa o usuário do servidor onde ele está logado;
* `servidor`: Computador onde o usuário está logado (ex.: thiago-pc);
* `:`: Separa o username@servidor do caminho acessado pelo usuário;
* `~`: O til significa a pasta home do usuário. Pode ser substituído pelo diretório atual que o usuário acessa;
* `$`: O cifrão significa que o usuário `não tem privilégios de administrador`. Se substituído pela cerquilha (`#`), significa que o usuário `tem privilégios de administrador`. Experimente usar o comando `sudo su` para logar como o usuário root.

## Alguns comandos
* `pwd`: Exibe o caminho atual (Print Working Directory). Ele diz onde estamos no servidor;
* `ls`: Lista informações sobre arquivos ou diretórios (por padrão, lista informações do path atual). 
  * O comando `ls -l` lista com descrição longa (long) os arquivos;
  * O comando `ls -a` lista todos (all) os arquivos, inclusive os ocultos, diretório atual (.) e  diretório pai (..);
  * O comando `ls -A` lista quase todos (Almost all) os arquivos, inclusive os ocultos. O diretório atual (.) e  diretório pai (..) não aparecem no resultado;
  * O comando `ls -a` lista todos (all) os arquivos, inclusive os ocultos;
* `ll`: Comando do Ubuntu que é um alias para o comando `ls -la`: mostra todos os arquivos (inclusive ocultos), com descrição longa;
* `touch <nomeDoArquivo>`: Cria um arquivo em branco;
* `man <nome_do_comando>`: Exibe o manual do comando;

# Hierarquia no filesystem - FHS

FHS (Filesystem Hierarchy Standard - Padrão de Hierarquia de Sistema de Arquivos). O FHS se baseia no princípio de haver uma única raiz (/) para todos os diretórios/pastas do sistema de arquivos. É diferente do Windows, que usa unidades identificadas por letras.

> O comando `cd` sem parâmetros muda para o diretório home do usuário.

# Atalhos para navegação
* Use as `setas para cima ou para baixo` para ver os últimos comandos executados no bash;
* Use a tecla `tab` para autocompletar os paths no bash;
* O comando `cd -` (com o traço) muda para o último diretório acessado antes do diretório atual.

# Criando diretórios com o MKDIR
* `mkdir -p path/com/subdirs`: O parâmetro `-p` inclui os diretórios-pai/subpastas na medida do necessário.
* O comando `touch` permite criar vários arquivos ao mesmo tempo: `touch arq1 arq2 arq3`.

# Removendo diretórios e arquivos - RMDIR E RM
* `rmdir` remove diretórios ***não vazios***. Comando pouco usado.
* O comando `rm` remove arquivos e diretórios. É possível apagar mais de um arquivo/diretório por vez: `rm arq1 arq2`.
* O comando `rm -rf` apaga recursivamente e forçadamente arquivos e diretórios e o seu conteúdo.
  * O comando `rm -r` (com o parâmetro `-r` de recursivo) apaga um diretório e o seu conteúdo, se houver.
  * O comando `rm -f` (com o parâmetro `-f` de forçado) força a exclusão.

> O comando `mkdir` admite criar vários diretórios de uma vez: `mkdir dir1 dir2 dir3` cria 3 diretórios.
> Para criar diretórios com espaços, há duas formas:
> 1. Escape o espaço com uma contrabarra: 
>```
>thiago@thiago-pc:~/labs/arqs_dirs$ mkdir diretorio\ 1 diretorio\ 2
>thiago@thiago-pc:~/labs/arqs_dirs$ ls
>'diretorio 1'  'diretorio 2'
>```
> 2. Envolva os nomes de diretório com aspas (simples ou duplas): 
>```
>thiago@thiago-pc:~/labs/arqs_dirs$ mkdir 'diretorio 3' 'diretorio 4'
>thiago@thiago-pc:~/labs/arqs_dirs$ ls
>'diretorio 1'  'diretorio 2'  'diretorio 3'  'diretorio 4'
>
>thiago@thiago-pc:~/labs/arqs_dirs$ mkdir "diretorio 5" "diretorio 6"
>thiago@thiago-pc:~/labs/arqs_dirs$ ls
>'diretorio 1'  'diretorio 3'  'diretorio 5'
>'diretorio 2'  'diretorio 4'  'diretorio 6'
>```
