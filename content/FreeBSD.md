# WIFI
[WiFi/FAQ - FreeBSD Wiki](https://wiki.freebsd.org/WiFi/FAQ)
>[!info] Navegar entre os terminais virtuais
>``` option ⌥ + fn + F1-F8```

>[!info] Scroll Lock na VM
>Ctrl + 0
>Tutorial: [Keyboard without Scroll Lock (freebsd.org)](https://lists.freebsd.org/pipermail/freebsd-questions/2007-September/158918.html)
>
# Utilidades
[torrent server](https://forums.freebsd.org/threads/freebsd-install-rtorrent-and-rutorrent-on-lighttpd-full-guide.85230/)
[FUG-BR / Grupo Brasileiro de Usuarios de FreeBSD](https://www.fug.com.br/)
[Solved - bsdinstall scripting guide/tutorial | The FreeBSD Forums](https://forums.freebsd.org/threads/bsdinstall-scripting-guide-tutorial.79105/)
# Introdução
FreeBSD é um sistema operacional baseado nos padrões do 4.4BSD-Lite feito pelo Computer Systems Research Group (CSRG) na UCB

## Suporte à arquiteturas de computadores
- x86 intel/amd ambos 32 e 64 bits
- ARM e AArch64
- RISC-V, MIPS
- PowerPC
- Sun UltraSPARC

## Suporta recursos de sistemas Operacionais modernos
- Preemptive multitasking
- Memory protection
- Virtual memory
- Multi-user facilities
- SMP support
- All Open Source Development Tools such as different langauges and frameworks
- Desktop features
	- DE's X Window System, KDE, GNOME

## Vantagens do FreeBSD

- Liberal Open Source License
Liberdade de usar o sistema em projetos open source e de cunho comercial.
- Strong TCP/IP networking 
- OpenZFS support
- Extensive security features
Mandatory Acess Control framework, Capsicum capability, sandbox mechanisms.
- +30.000 prebuilt packages for all supported architectures
- Ports Collection
- Extensible Documentation
- Simple and consistent repository structure and build system
single repository for all components, both kernel and userspace.
- Staying true to [[Unix]] philosophy
- Binary compatibility with Linux Can run linux binaries without virtualization


# Habilitar Scroll Lock Freebsd nas teclas desejada
<div class="rich-link-card-container"><a class="rich-link-card" href="https://lists.freebsd.org/pipermail/freebsd-questions/2007-September/158918.html" target="_blank">
	<div class="rich-link-image-container">
		<div class="rich-link-image" style="background-image: url('https://lists.freebsd.org/favicon.ico')">
	</div>
	</div>
	<div class="rich-link-card-text">
		<h1 class="rich-link-card-title">Keyboard without Scroll Lock</h1>
		<p class="rich-link-card-description">
		
		</p>
		<p class="rich-link-href">
		https://lists.freebsd.org/pipermail/freebsd-questions/2007-September/158918.html
		</p>
	</div>
</a></div>

# Alterar o hostname no Freebsd
modificar no arquivo /etc/[[rc]].conf a variável freebsdinho
# Virtual Consoles and Terminals
útil quando estiver utilizando o FreeBSD sem uma interface gráfica. Os virtuais consoles serve para trabalhar em diversos programas ao mesmo tempo utilizando o terminal, ele resolve o problema de o usuário ficar esperando um programa terminar sua execução para assumir o controle do teclado. Ele funciona da mesma forma que abrir várias janelas do terminal ao mesmo tempo em um ambiente gráfico.
Para alterar de console utilize as teclas `alt + Fn` onde os consoles virtuais vão de `F1` até `F8`:
## O arquivo _/etc/ttys_
Este arquivo possuí várias informações a respeito do terminal do ssitema, como:
- nome
	Nome do dispositivo de terminal
- getty
é um programa que manipula os terminais virtuais, é chamado por init(8) para abrir e inicializar a linha [[tty]], ler o login do usuário e invocar login(1)
- type
	o tipo do terminal, o padrão para terminais virtuais é _xterm_.
- status on/off
se tiver on o programa getty vai rodar o init no dispositivo especifico. Geralmente vem acompanhado da palavra 'secure' que indica que root pode fazer login neste terminal.

O último dispositivo ttyv8 é reservado para acessar o ambiente gráfico (desktop environment) se este for instalado.

Mais informações: `ttys(5)`

### Desabilitar um dispositivo de terminal
Para desabilitar um dispositivo de terminal basta comentar o inicio da linha dispositivo com "#", tem que ter atenção para **NÃO** comentar o dispositivo ttyv0.

## Modificar console video mode
página: 81 – FreeBSD handbook

# User and Basic Account management
## tipos de conta
### System Accounts
É utilizado para rodar serviços como: DNS, mail, web servers. A razão de existir é por motivos de segurança.
### User Accounts
São o tipo de conta das pessoas que utilizam o sistema operacional. Cada conta possui as seguintes informações
- nome de usuário
- senha
- uid
- group id
- login class
- Home directory
- User shell
### Superuser Account  – ROOT
não possui limitações de permissões para manipular o sistema. É recomendado logar como usuário e sempre que houver a necessidade de permissões de _root_ trocar para esse usuário, realizar a tarefa e logar como usuário novamente.

## Como alterar de usuário
> Comando `$ su username`
> Exemplo: `$ su root` faz login como root do sistema.

## Manipulação de contas
>[!caution] Executar estes comandos como root!!
> Para trocar para _root_ [[#Como alterar de usuário]]
### Listar usuários e grupos
`$ cat /etc/passwd`
### Criar usuário
`$ adduser`
### Remover Usuário
` $ rmuser`
### Adicionar um usuário à um grupo
`$ pw groudmod [groupname] -m [username]
### Listar os grupos que um  usuário pertence
`$ id [username]`

# Permissões
No [[Unix]] existe 3 tipos básicos de permissões atribuídas a arquivos:
1. _r_ – read
2. _w_ – write
3. _x_ – execute 
```shell
$ ls -l
-rw-r--r-- 1 jao jao 962 4 22:50 .cshrc
```
o primeiro _-_ indica que é um arquivo normal. Os próximo 3 caracteres _rw-_ indica as permissões do usuário os próximos _r--_ indicam as permissões do grupo e os últimos 3 _r--_ indicam as permissões para o resto dos usuários do sistema. 
## Como o sistema controla as permissões aos dipositivos (devices) ???
FreeBSD trata a maioria dos dispositivos de hardware como arquivos uqe os programas podem escrever e ler dados. Para ver as permissões aos dispositivos basta utilizar o comando ls -l no diretório \/dev
`$ ls -l /dev`

## Modificar as permissões de arquivos
Comando: _$ chmod_
>Exemplo: Adicionar permissão de ler e escrever a todos os usuário / grupos – `$ chmod 666 lovefreebsd`

## FreeBSD File flags
página: 92 – freeBSD handbook

## _setuid_, _setgid_ and _sticky_ permissions
Existe outras 3 configurações especificas que todo administrador deve saber! São as permissões:
- _setuid_
- _setgid_
- _sticky_
Quando um _sticky_ bit é setado em um diretório, implica que apenas o dono dos arquivos podem remove-los. É útil para impedir a exclusão de arquivos em diretórios públicos como **/tmp** por outros usuários a não ser o dono. 
Para setar essa permissão utilize use o prefixo '1', exemplo:
`$ chmod 1777 /tmp`
Quando executar _ls -l_ o sticky bit estará representado por '_t_' no final da string de permissões.
### A diferença entre Real x Effective Uid
O Uid **real** é o id do usuário que iniciou o programa/[[processo]].
O Uid **efetivo** é id do usuário que roda o processo.
>[!tip] Exemplo: Comando _passwd_
>O comando `$ passwd` inicia com o uid do usuário que o executou (**real uid**), portanto para editar o arquivo de passwords precisa executar em modo superusuário, ou seja,**effective uid** é do root.

# Estrutura de diretórios

## Mount Point
> _directory where additional file systems can be grafted onto a parent file system_

## Diretórios importantes
| Diretórios | Descrição |
|------------| ----------|
| \/ | Root do sistema de arquivos |
| /bin/ | Executáveis tanto para single-users quanto para multi-users|
| /boot/ | Programas e arquivos de configurações usados durante o boot do sistema|
|/boot/defaults/|Configurações padrões usadas durante o boostrap do sistema operacional|
| /dev/ | Arquivos de dispositivos como ttys0 e entre outros, veja intro(4) para detalhes
| /etc/ | Configurações do sistema e scripts |
| /etc/defaults/ | Arquivos de configurações padrões do sistema, [[rc]](8) para mais detalhes|
| /proc/ |  Process file system. procfs(5), mount_procfs(8) para mais detalhes |
| /root/ | diretório home da conta root
| /sbin/ | Programas do sistema e utilidades de administrador fundamentais para single-user e multi-user |
| /tmp/ | arquivos temporários que não são mantidos depois que o sistema reinicia. A memory-based file system is often mounted at /tmp/. 
| /usr/ | A maioria das utilidades e aplicações |
| /usr/bin/ | utilidades comuns, ferramentas de desenvolvimento e programação e aplicações
| /usr/include/ | Standard C include files
| /usr/lib/ | Achieve libraries
| /usr/libexec/| System daemons e utilidades do sistema executadas por outros programas
| /usr/local/ | Executáveis locais e bibliotecas. Também é utilizado como destino para o FreeBSD ports framework.
| /usr/obj/ | Architecture-specific target tree produced by building the /usr/src tree.
| /usr/ports/| FreeBSD ports Collection (opcional!)
| /usr/sbin/| System daemons and system utilities executed by users
|/usr/share/| arquivos architecture independent
| /usr/src/ | BSD and/or local source files
| /var/| Multi-purpose log, temporary, transient, and spool files. A memory-based file system is sometimes mounted at 


#  Processos e Daemons
## Processos
FreeBSD é um sistema multi-tasking onde cada programa programa rodando em qualquer determinado instante de tempo é chamado de processo. Cada comando executado no shell inicia pelo menos um processo, além dos processos do sistema que rodam o FreeBSD.Os processos são identificados por um número chamado process ID (PID). Cada processo possui um dono e um grupo e as permissões associadas para determinar quais arquivos e dipositivos o processo pode acessar.
A maioria dos processos também possuem processos pais. A excessão é o processo chamado _init(8)_ que sempre é o primeiro processo a iniciar após o boot e sempre possui PID 1.
### Visualizar processos ativos
#### Comando: `$ ps`
Mostra apenas os processos ativos no terminal corrente e criados pelo usuário logado.
>"A number of different options are available to change the information that is displayed. One of the most useful sets is auxww, where a displays information about all the running processes of all users, u displays the username and memory usage of the process' owner, x displays information about daemon processes, and ww causes ps(1) to display the full command line for each process, rather than truncating it once it gets too long to fit on the screen"
#### Comando `$ top`
Mostra informações dos maiores (top) processos no sistema e contém mais informações que o comando `ps` como: _system load_, uso de memória entre outros.
>[!info] Se o módulo do sistema de arquivos _ZSF_ tiver sido carregado, uma linha indicando _ARC_ irá indicar a quantidade de dados foi lida da memória cache no lugar do disco.
### Matar processos
Uma das maneiras de comunicar com um processo é enviar um [[signal]]. 
Um usuário somente pode enviar um signal para um processo que o pertence (com excessão do usuário root). O sistema operacional também pode enviar signal para um processo. Como de exemplo: o signal (_SIGSEGV_) "Segmentation Violation".
O comando `$ alarm` também envia um signal _SIGALARM_ para programas que utilizar essa chamada de sistema.
#### Signal para matar processos 
- _SIGTERM_: É a maneira mais "gentil"de terminar um processo, sendo que o processo pode fechar alguns arquivos e tentar terminar algum tarefa antes de encerrar. Em alguns casos o processo até pode ignorar o _SIGTERM_ se estiver no meio de uma tarefa que não pode ser interrompida.
- _SIGKILL_: É a forma mais "bruta" de encerrar um processo. SIGKILL encerrará imediatamente um processo e não poderá ser ignorado.
#### Outros signals de propósito geral
- _SIGHUP_
- _SIGUSR1_
- _SIGUSR2_
#### Exemplo Matar um Daemon
1. Iniciamos daemon _inetd(8)_
`$ inetd8`
2. Descobrimos o PID do processo com o comando seguinte:
`$ pgrep -l inetd`
3. Como o _inetd(8)_ pertence ao root, precisamos troca-lo para este usuário.
`$ su root`
4. Matamos o processo com o comando _kill_
`$ kill pid`

>[!info] Qual a diferença de kill e /bin/kill ?
>Hint: Final da página 108!


## Daemons
São programas que não são destinados a rodar com entrada continua do terminal, ao invés disso, são desconectados do terminal na primeira oportunidade. Por exemplo, um servidor Web responde por requisições ao invés de entrada do usuário. Outra definição é de que _daemons_  são programas que rodam como _background process_ em vez de controle interativo com o usuário.
### Convenção de nomes de Daemons
normalmente são programas que terminam com "_d_" como:
- BIND – Berkeley Internet Name Domain
- HTTPD – Apache web Server
- LPD – line printer spooling
mas importante notar que é apenas uma convenção e nem todos os programas obedecem-a.

# SHELL
## Arquivo contendo os shells presentes no sistema
	/etc/shells
```shell
# List of acceptable shells for chpass(1).
# Ftpd will not allow users to connect who are not using
# one of these shells.

/bin/bash
/bin/csh
/bin/dash
/bin/ksh
/bin/sh
/bin/tcsh
/bin/zsh
```
## Environment Variables
São variáveis que armazenam valores de configurações que pode ser lida por vários programas que utilizam o shell. Abaixo uma tabela com algumas variáveis comuns.
| Variável | Descrição |
|----------|-----------|
|USER| Nome do usuário logado e ativo
|PATH| o path dos diretórios que o shell procura pelos executáveis binários, cada path é separado  por um _:_
|DISPLAY| Network name of Xorg display to connect to, if available 
|SHELL| Nome do Shell em uso.
|TERM| O nome do tipo de terminal utilizado
|TERMCAP| Database entry of the terminal escape codes to perform various terminal functions
|OSTYPE| TIpo do sistema sistema operacional (kernel)
|MACHTYPE| Arquitetura da CPU do sistema.
|EDITOR| O editor favorito do usuário
|PAGER| User preferred utility for viewing text one page at a time.
|MANPATH| diretórios que busca os arquivos de manual.
### Como alterar as variáveis ambiente do shell
Exemplo: Alterar a variável _EDITOR_:
Nos shell: _sh_, _bash_, _zsh_
`$ export EDITOR="usr/bin/nano"`
Nos shell: _tcsh_ e _csh_
`$ setenv EDITOR /usr/bin/nano`

### Como mostrar o conteúdo das variáveis ambiente do shell
echo $_nome_da_variável_
`$ echo $TERM`
`$echo $PATH`

## Alterar o shell padrão de um usuário
Comando: _chpass_ ou _chsh_
Exemplo: `$ chsh -s bash`
Exemplo: `$ chpass -s zsh`
## Redirecionamento
Todo sistema Unix possui file descriptors que incluem:
- _stdin_ – standard input
- _stdout_ – standard output
- _stderr_ – standard error

Esses 3 são considerados I/O file descriptors e algumas vezes também são chamados de streams.

![[The Unix Programming Environment#Redirecionamento de Entrada/Saída]]

![[The Unix Programming Environment#Pipes]]

# Devices and Device Nodes
"Device" é um termo utilizado atividades relacionadas ao hardware do sistema, incluíndo discos, impressoras, placas gráficas e teclados. Quando o FreeBSD boota a maioria das mensagens está relacionada a detecção destes dispositivos.
A maioria dos dispositivos podem ser acessadas apartir de arquivos especiais chamaos de _devices node_ que estão localizados no diretório /dev. 
## Acessar uma copia da mensagem de BOOT
	Está localizada no arquivo: /var/run/dmesg.boot




# Compress / Decompress with `$ gzip`
Arquivos com o formato .xz ou .gz podem ser descomprimidos utilizando o comando: `$ gzip -d filename`

# Instalação de aplicações no freeBSD
## Onde encontrar Softwares
<div class="rich-link-card-container"><a class="rich-link-card" href="https://www.freebsd.org/ports/" target="_blank">
	<div class="rich-link-image-container">
		<div class="rich-link-image" style="background-image: url('https://www.freebsd.org/images/logo-thepowertoserve.png')">
	</div>
	</div>
	<div class="rich-link-card-text">
		<h1 class="rich-link-card-title">About FreeBSD Ports</h1>
		<p class="rich-link-card-description">
		FreeBSD is an operating system used to power modern servers, desktops, and embedded platforms.
		</p>
		<p class="rich-link-href">
		https://www.freebsd.org/ports/
		</p>
	</div>
</a></div>
<div class="rich-link-card-container"><a class="rich-link-card" href="https://www.freshports.org/" target="_blank">
	<div class="rich-link-image-container">
		<div class="rich-link-image" style="background-image: url('https://www.freshports.org/images/android-icon-192x192.png')">
	</div>
	</div>
	<div class="rich-link-card-text">
		<h1 class="rich-link-card-title">FreshPorts -- The Place For Ports - Most recent commits</h1>
		<p class="rich-link-card-description">
		Most recent commits
		</p>
		<p class="rich-link-href">
		https://www.freshports.org/
		</p>
	</div>
</a></div>

## PKG – Binaries Packages Manager
### Beneficios:
- Um package comprimido é típicamente menor que um source code da aplicação comprimido.
- Packages não necessitam de tempo de compilação. Para aplicações complexas como Mozzila Firefox, KDE ou GNOME isso pode ser importante para sistemas lentos.
- Packages não necessitam de nenhum conhecimento do processo de compilação de software no FreeBSD.

### Buscar pelo pacote binário de uma aplicação pelo terminal
	$ pkg search nome_pacote
	Exemplo: pkg search java

![[pkg_search.png]]

### Getting Started
Informações para o usuário – `$ man pkg`; `$ man pkg-install`
Por padrão o _pkg_ usa os pacotes binários do FreeBSD package _mirrors_ (repositório). Para informações adicionais sobre opções de configuração para o _pkg_ buscar em: `$man pkg.conf`.

#### Atualizar o repositório dos pacotes
	$ pkg update -f
#### Instalar um pacote de um repositório remoto
	$ pkg install packagename
#### Remover pacotes instalados
	$ pkg delete packagename
#### Listar todos os pacotes instalados com pkg
	$ pkg info --all
#### Mostrar informações sobre um pacote especifico
	$ pkg info packagename
#### Atualizar pacotes instalados
	$ pkg upgrade
#### Remover left-behind dependencies packages
	$ pkg autoremove
#### Listar pacotes que foram instalados como não-dependencias
	$ pkg prime-list
#### Auditar pacotes
	$ package audit -F
#### Get origin port directory
	$ package prime-origins
#### Remove Stale packages
	$ pkg clean -a

## Ports Collection

### Livro sobre Ports Collection:
[FreeBSD Porter's Handbook | FreeBSD Documentation Portal](https://docs.freebsd.org/en/books/porters-handbook/book/)
### Beneficios
- Pacotes são normalmente compiladores com opções conservadoras por que eles tem que rodarem no máximo número de sistemas. Ao compilar com o ports qualquer um pode alterar as opções de compilação.
- Algumas aplicações possuem opções em tempo de compilação relativo a quais recursos são instalados.
- As condições de licensa de alguns softwares proíbem distribuições binárias. Estes softwares precisam serem distribuídos com o código fonte e precisa ser compilado pelo usuário final.
- Algumas pessoas não confiam em distribuições binárias ou preferem visualizar o source code para averiguar potenciais problemas.
- Source code is needed to apply custom patches.

### O que é Ports Collection
é um conjunto de makefiles, patches, e descriptions files. Cada conjunto destes arquivos é utilizado para compilar e instalar aplicações no FreeBSD, tais aplicações são chamadas de _ports_.
> Por padrão, Ports Collection é armazenada no sub-diretório: `/usr/ports`

>[!caution] Cuidado!
> É desaconselhável usar a Coleção de Ports em conjunto com os pacotes binários fornecido via pacote para instalar o software. O pkg, por padrão, rastreia os lançamentos de ramificação trimestrais da árvore de ports e não o HEAD. As dependências podem ser diferentes para uma porta em HEAD em comparação com sua contraparte em um lançamento de ramificação trimestral e isso pode resultar em conflitos entre as dependências instaladas pelo pkg e as dos Ports Coleção. Se a Coleção de Ports e o pacote devem ser usados ​​em conjunto, então certifique-se de que sua coleção de ports e o pacote estejam na mesma versão de ramificação dos ports árvore.
>

### Instalar Ports Collection

1. instalar o git por meio do comando `$ pkg install git`
2. Executar o comando `$ git clone https://git.FreeBSD.org/ports.git /usr/ports
3. atualize /usr/ports depois do git checkout inicial – `$ git -C /usr/ports pull`
4. switch /usr/ports para um quarterly branch diferente `$ git -C /usr/ports switch 2020Q4`

### Instalando Ports
Para usar o ports collection necessita de privilégios de super-usuário (root) e de conexão com a internet.
1. Entrar na pasta do port que deseja instalar Exemplo: `usr/ports/sysutils/snooze`
2. `$ make install`
3. Para obter o _source code_ do ports rodar o comando: `$ make extract` e o source code está na pasta /work dentro do diretório do port

### Removendo Ports
Há duas maneiras de remover programas instalados com ports:
1. Usando `$ pkg delete`
2. Usando `$ make deinstall` no diretório corrente do port

