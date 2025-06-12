Tags: #draft

# Prefácio
## História
O desenvolvimento da primeira versão do Unix começou em 1969 nos bell-labs em um computador chamado de [[DEC PDP-7]]. Os idealizadores foram o famoso [[Ken Thompson]] com a ajuda de Rudd Canaday, Doug Mcilrouy e entre outros, o ilustre [[Dennis Ritchie]] que escreveu uma versão do compilador da [[C]] para o [[DEC PDP-7]]. O objetivo dos funcionários era desenvolver um pequeno '_time-sharing system_' de propósito geral que fosse atrativo para usuários entusiastas e que angariasse a credibilidade para adquirir um novo computador [[PDP-11/20]] para o laboratório.
Em 1973 Dennis Ritchie e Thompson reescreveram o sistema UNIX utilizando a linguagem C. Este feito quebrou um antigo paradigma que sistemas de software só podiam ser escritos em linguagem [[Assembly]].
## Qual a razão do sucesso do sistema Unix ?
Uma das razões do sucesso do sistema Unix é pelo motivo de ser escrito na linguagem C. Entre as vantagens de se escrever um sistema operacional utilizando de linguagens de mais alto nível em comparação as linguagens de montagem, podemos citar:
- Portabilidade

	A facilidade de portar o SO para um ampla gama de hardwares e arquiteturas, desde microprocessadores até os maiores mainframes.
- Manutenibilidade

	A capacidade de adaptar o sistema para algum requisito particular, adicionar novas funcionalidades, corrigir possíveis erros e falhas de segurança

## Filosofia
A ideia central do Unix advém da integração entre  as tarefas/programas, de modo que nenhuma tarefa isolada terá o mesmo poder de expressão que a combinação de múltiplos programas operando em conjunto. – _O que o torna, de fato, eficaz é a abordagem de programação_.

> A _essência_ do Unix está na ideia de que o potencial do sistema vem das relacões entre os programas, e não dos programas em si. De fato, a maioria dos programas do Unix realizam tarefas triviais(como o comando _cat_), porém, quando combinados oferecem um alto poder de expressão computacional, e uma ferramenta poderosa para resolver problemas utilizando computadores.


# Primeiro Capítulo: Unix para iniciantes
## O que é Unix?
É um _time-sharing operating system_ [[Kernel]] – Um programa que controla os recursos de hardware e realiza a alocação destes entre as tareafas dos usuários. entre os recursos ofercidos estão:
- Permitir que usuários executem seus programas/tarefas
- controlar a comunição entre o computador e os dispositivos periféricos.
- Disponibilizar um sistema para organizar e manipular arquivos não voláteis.

## Escrever no terminal
### Conceito: _full duplex_
Os caracteres que voce digita no teclado são enviados para o sistema, e então enviados de volta para o terminal para ser exibido na tela.
Normalmente esse processo é chamado de _echo_ – copiar os caracteres passados para o sistema direto para a tela do terminal assim que o usuário digitar no teclado. Em algumas situações o _echo_ pode ser disabilitado como ocorre quando o usuário digita uma senha.
### Conceito: _Control Character_
Normalmente, a maioria dos caracteres são ecoados normalmente para o terminal, sem nenhum siginificado adicional. mas alguns possuem significado extra para o sistema. 
- _Return Key_
	É uma das teclas que é interpretada pelo computador. Quando o usuário pressiona a tecla _Return_ o sistema processa a linha atual e move o cursor do terminal para o início de uma nova linha.
O _RETURN_ é um exemplo de caractere de controle, **Definição:** – um caractere invisivel que controla algum aspecto de entrada/saída do terminal.
Ao contrário de _RETURN_ que possui uma tecla única no teclado, a maioria dos caracteres de controle não possuem e são formados por uma combinação de teclas ordinárias e a tecla Control/_CTRL_. 
#### Exemplos de Control Character
- _CTRL_ + m 
	Mesmo efeito que a tecla _RETURN_
- _CTRL_ + g
	toca o sininho do teminal
- _CTRL_ + h
	Mesmo efeito que o backspace
- _CTRL_ + i
	Mesmo efeito que o tab

- _CTRL_ + c OU _CTRL_ + z
	Interrompe a execução de um programa do terminal. ctrl c não funciona no alacritty no mac.
### Conceito: _Prompt_
O prompt é um caractere exibido a esquerda da linha do terminal antes do usuário digitar qualquer comando. Na verdade o prompt é printado por um programa chamado de _command interpreter_ ou _shell_.
- indica que o sistema está pronto para aceitar comandos
- O caractere que normalmente representa o prompt é o _$_
### Conceito: _Type-ahead_
O kernel lê e interpreta a entrada assim que o usuário a digitar, entretanto se o usuário digitar enquanto o terminal está imprimindo o reusltado de um outro programa os caracteres digitados serão exibidos entre os caracteres que estão sendo impressos, no entanto eles serão armazenados e executados se estiverem corretos.
>[!info] É possivel dar comandos para o terminal enquanto alguma coisa estiver sendo printada na tela
## Introdução básica ao sistema de Arquivos
No Unix, os blocos de informação são armazenados em arquivos.
### Caracteristicas de Arquivos:
- Nome
- Conteúdo
- Endereço
e outras informações como tamanho ocupado no armazenamento. (pode ser expresso tanto em blocos como em bytes).
### Nome de Arquivos
Em sistemas Unix mais antigos possuem regras para o nome de arquivos como por exemplo:
- Limite de 14 caractere
- Evitar símbolos, utilizar apenas letras, números, ponto(period) e _underscore_
- Distinguir letra maíusculas de minusculas, Ex: junk, JUNK, Junk não são o mesmo arquivo.

### Diretórios
Unix distingue arquivos de diferentes usuários e aplicações através do uso de diretórios. Usualmente cada usuário possuí um _home directory_. 
>[!info] Dois arquivos podem possuir nomes iguais se estiverem em diretórios diferentes.

Um diretório pode incluir outro diretório, isso é comumente chamado de níveis de diretórios.
A forma natural de visualizar a estrutura de diretórios do sistema é imaginar uma organização em forma de árvore, onde a raiz é o diretório _/_ 
![[tree_directory_struct.png]]
_**Exemplo de uma estrutura contendo 3 níveis de diretório.**_

## Comandos básicos
%%Serão adicionados mais adiante, por enquanto estarão marcados em vermelho no livro%%
### Manual
- Descreve a maioria dos comandos do sistema
- Possui uma versão em pdf neste [link](https://dspinellis.github.io/unix-v4man/v4man.pdf)
O manual também está imbutido em sistemas que utilizam como base o Unix através do comando: **man** _command-name_
>Exemplo: `$ man echo`
>![[man_echo.png]]
>Presionar _Q_ para _**sair**_ da página do manual.

## Editores de Texto
> É um programa para armazenar e manipular informação em formato de texto no computador.

Os editores de texto mais populares em sistemas Unix são o [[vi]] e o [[emacs]]. Entretanto existem diversos editores de texto por aí e não existem um que seja padrão para todas os sistemas Unix.
### ED Text Editor
o _Ed_ é um dos primeiros editores de texto feitos para Unix. Por ser muito simples, funciona em qualquer tipo de terminal, já que não possui comandos especiais de terminais mais complexos.
O Ed também foi a base para diversos programas essenciais e até mesmo outros editores de textos mais completos. Portanto é válido aprender um pouco sobre seu funcionamento.
## SHELL
É o programa que faz a comunicação entre os comandos que o usuário digita e o kernel do sistema. O fato do shell ser um programa e não uma parte do kernel oferece diversos beneficios. Entre os principais:
- Atalhos para nomes de arquivos: É possivel escolher diversos nomes de arquivos como argumento de um programa ao especificar uma padrão de busca, apartir disso o shell irá buscar os nomes que casam com o padrão estipulado.
- Redirecionamento de Entrada/Saída: É possível escolher que a saída de um programa seja escrita em um arquivo ao invés do terminal. O mesmo ocorre com as entradas, é possivel passar um arquivo contendo os argumentos de entrada ao invés de digita-los no terminal. Outro ponto é que a saída de um programa pode ser conectada à entrada de outro programa.
- Personalizar o ambiente/terminal: É possivel determinar configurações para o terminal, como rodar um comando sempre que abrir o terminal, definir atalhos, etc.

### Filename shorthands

É possível buscar por nomes de arquivos que sigam algum determinado padrão de caracteres. alguns exemplos de utilização podem ser vistos abaixo

#### Todos os nomes de arquivos que terminem com .java
- \*.java
Neste caso o shell interpreta o '\*' como "qualquer sequência de caracteres que termine com .java"

#### Todos os nomes de arquivos que comecem com "texto"
- texto*
O mesmo que o de cima,porém o shell vai retornar todos os arquivos em que o nome comece com a string 'texto' e que prossiga com qualquer caractere.
>[!info] O aspecto crucial é que os padrões de nomes é um serviço que pertence ao shell e não aos comandos com os quais é utilizado.
#### Todos os nomes de arquivos que possuem um grupo especifico de caractere.
- ch[12346789]
Irá buscar por todos os arquivos que possuem como nome iniciando com ch e seguindo por um numero entre 1-9 exceto o 5!
#### Todos os nomes de arquivos que possuem um único caractere especifico.
- `$ ls ?`
- texto?
Irá buscar correspondencias onde um caractere irá se encaixar. por exemplo, no ls ? irá listar todos os arquivos que possuem nome com apenas 1 caractere e em texto? irá imprimir todos os arquivos que possuirá além da string 'texto' mais um caractere, portanto se existir um arquivo com nome "texto10" este não irá corresponder!

>[!tip] Dicas
>1. Padrões de caracteres como \* pode ser utilizado com caminho de arquivos como _/usr/mary/*_ performa uma busca de todos os arquivos presentes no diretório _mary_
>2. Se você precisar utilizar os caracteres \*, ? com outro significado, basta utiliza-los entre aspas simples como `$ ls '?'`
>


### Redirecionamento de Entrada/Saída
> O terminal pode ser substituido por arquivo tanto para operações em entrada ou saída de dados.

#### Redirecionar saída de um programa para um arquivo
- Utilizar o símbolo "_>_" que significa "coloque a saída no seguinte **arquivo** ao invés de ser no terminal", Exemplo:
	1. `$ ls > filelist.txt`
	2. `$ tree > dirstruct.txt`

#### Anexar a saída de um programa no fim de um arquivo
- "_>>_" 
`$ cat f1 f2 >> temp.txt` – Concatena os arquivos f1 e f2 e adiciona ao final do arquivo temp.txt

#### Ler uma entrada apartir de um arquivo
É possível passar os argumentos para um programa através de um arquivo. O símbolo utilizado é o mesmo que o de redirecionamento de saída só com o sentido invertido.
Exemplo:
- `who > temp.txt` – Redireciona a saída de _who_ para _temp.txt_
- `sort < temp.txt` – utiliza com argumento para _sort_ o conteúdo que está em _temp.txt_

###  Pipes
Os _Pipes_ são uma forma de conectar a saída de um programa direto na entrada de outro programa via terminal sem a necessidade de um arquivo intermediário; Uma _pipeline_ é a conexão entre dois ou mais programas através de _pipes_.
>[!info]
>Programas em pipeline rodam ao mesmo tempo em _paralelo_. Isso significa que programas em um pipeline podem ser interativos, o kernel é responsável por fazer a sincronização e escalonar as tarefas em um _pipeline_.

### Processos
O shell do Unix possui mais funcionalidades para concorrencia além do uso de pipes.

#### Como rodar múltiplos programas em uma única linha do terminal

##### Sequencial
É possivel rodar mais de um programa na mesma linha do terminal separando os programas por um ';'.
###### Exemplo
``` 
$ date ; who
```
>#### O resultado de rodar a linha acima:
>```
>Fri Dec 23 15:39:45 -03 2022
joao             console      Dec 19 18:02
joao             ttys000      Dec 23 15:39
>```

###### Como funciona
> _Os programas executam sequencialmente, primeiro **date** depois **who** _

O shell reconhece o caractere ';' e quebra a linha original em cada linha contendo um único programa, portanto a saída de cada programa é impressa sequencialmente respeitando a ordem de execução.

##### Paralelo
Assim como é possivel rodar mais de um programa na mesma linha do terminal de forma sequencial, também é possivel ter múltiplos programas rodando em paralelo.
###### Exemplo
> ```
> $ tree > teste.out & date
> ```
> #### O resultado de rodar a linha acima:
>```
[1] 22000
Fri Dec 23 16:31:42 -03 2022
[1]  + exit 2     tree > teste.out

A saída "[1] 22000" é o id do processo.

###### Como funciona
> O shell interpreta a letra '&' de modo a executar os programas que precedem a ocorrência de '&' e liberar o terminal para continuar executando comandos, sem esperar o programa anterior acabar.

>[!info] É uma boa redirecionar a saída para um arquivo de modo à não interferir no fluxo de impressão do terminal.
>

#### Como esperar terminar todos os processos inicializados com '&'
>Comando: `$ wait`
>

>[!info] É possivel interromper _$ wait_ com a tecla DELETE

#### Utilidade prática do '&' 
- Deixar o [[FFMPEG]] rodando no background

### Comando _nohup_
Do jeito que o shell funciona, os comandos podem rodar no background quando utilizam o caractere '&' ou no foreground que é a forma padrão. Quando um programa no terminal estiver demorando muito tempo para ser executado e queremos desligar o terminal, podemos rodar nosso programa em background fora do terminal.
> ## Exemplo:
> ` $ nohup command &`

O programa _comand_ continuará rodando no background mesmo que você desligue o terminal.
> [!info] A saída de um programa executado após o nohup será armazenada no arquivo _nohup.out_

### Comando _nice_
O comando nice é uma boa opção para se utilizar em ambientes de execução compartilhada. O que esse comando faz é alterar a prioridade dos processos do usuário para uma prioridade mais baixa.
> ## Exemplo:
> `$ nice expensive-command &`
### Relação entre _nohup_ e _nice_
Quando você executa um comando com o nohup ele automaticamente invoca  _nice_ para diminuir a prioridade de execução do comando.
### Modificando o ambiente do shell
Vários shells permitem modificações em suas funcionalidades através de comandos passados para um arquivo de configuração.
#### Arquivo de configuração
O nome deste arquivo pode variar de shell para shell, por exemplo, no caso do [[zsh]] esse arquivo é `.zshrc`. Outro nome popular para esse arquivo é `.profile`
> [!info] Comandos passados para o arquivo de configuração do shell serão executados sempre antes de executar qualquer comando no terminal.
### Variáveis Shell
Algumas propiedades do ambiente de linha de comando pode ser alterado através da atribução de valores personalizado para variaveis do _SHELL_.
#### PS1  – String do prompt
#### HOME  – Diretório inicial
#### PATH  – Lugares onde o shell irá procurar os comandos
Quando o usuário digita um comando, como _neofetch_ o shell primeiro irá procurar o comando no diretório atual logo nos diretórios `/bin` e `/usr/bin`. Essa sequência de diretórios é chamado de _search path_ e está armazenado na variavel _PATH_. O conteúdo da variavel PATH se parace com algo do tipo: `/opt/homebrew/bin:/opt/homebrew/sbin:/usr/local/bin:/System/Cryptexes/App/usr/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Library/Apple/usr/bin`

>Para obter o conteúdo da váriavel **PATH** basta utilizar o comando echo `$ echo $PATH`

>[!tip] DICA
>Para adicionar um diretório ao _PATH_ do shell basta modificar a variável PATH e salva-lá no arquivo de configuração (.profile por exemplo) do shell.
> `PATH=$PATH:/Users/joao/Documents`

#### Export
Se você precisar utilizar as váriaveis do shell em outros programas é necessário exporta-lás, isso é feito com o comando `$ export`
>**Exemplo: `$ export PATH`**
>


## Referências do 1º capítulo

- **The Unix Time-sharing System** [Artigo](https://dsf.berkeley.edu/cs262/unix.pdf)
- **The Bell System Technical Journal(BSTJ) special issue on the UNIX system (July, 1978)** [Artigo](https://www.tuhs.org/Archive/Documentation/Papers/BSTJ/bstj57-6-1905.pdf)
- **The Unix Programmer Manual** [LIVRO](http://libgen.rs/book/index.php?md5=5445F067FB25C329ACE9B21AD64E2744)]

 






# Segundo Capítulo: O sistema de arquivos
%%Pág: 41-70%%
## Arquivos
Um arquivo é um conjunto de bytes sem uma estrutura ou conteúdo imposto pelo sistema operacional UNIX. O significado de um arquivo depende do programa que o interpreta.

>[!tip] Comando _od_
>od ou ASCII Dump, é um comando que exibe os caracteres de um arquivo, em diversos formatos.
>%%Alterar essa ordered list para exibicao em tabela%%
> 1. Exemplo: `$ od -c filename` – Exibe Formato ascii.
> 2. Exemplo: `$ od -o filename` - Exibe Formato Octal.
> 3. Exemplo: `$ od -N 12 -c filename` – Exibe um determinado tamanho (argumento -N 12)) de caracteres no formato ascii (-c option)


>[!INFO]
>Tudo que é necessário para acessar um arquivo em um sistema Unix é o nome do arquivo.

>[!tip] Comando mv
>É utilizado para mover ou renomear arquivos, o seu funcionamento se dá através de re-arranjar links. 
>Exemplo: `$ mv junk sameoldjunk` – renomeará o arquivo junk para "sameoldjunk". este comando troca apenas o nome do arquivo porém o [[#i-nodes]] mantém-se igual.

### Formato de Arquivos
É definido pelo programa que o interpreta. O kernel não impõe nenhum formato padrão para arquivos e tão pouco sabe qual o formato impregado nos arquivos do usuário. Por exemplo – um arquivo com sufixo '.c' pode conter instruções java ao invés de instruções em C como esperado.
>[!tip] Comando _file_
>Este comando tenta descobrir qual é o formato do arquivo passado como argumento para ele.
>Exemplo: `$ file /bin/ed ` retorna: `ELF 64-bit LSB pie executable...`

### Inicio de uma linha e fim de Arquivos
O sistema Unix utiliza _newlines_ (caractere especial) para indicar o inicio de uma nova linha em um arquivo. É representado em Ascii pelo caractere especial `\n` o qual é herdado da linguagem C.
Para fim de arquivos não é necessário nenhum caractere especial para representa-lo uma vez que é ambiguo que todos os arquivos terão um final de arquivo, o sistema interpreta o fim de arquivo quando não existe mais conteúdo para ler em um arquivo. O kernel mantém o tamanho dos arquivos, um programa encontra o _END-OF-FILE_ de um arquivo quandoeste já teve todos os seus bytes processados.

#### Como os programas acessam os dados de um arquivo?
O acesso aos bytes de um arquivo pelos programas é dado através de uma chamada de sistema (uma subrotina do Kernel) nomeada _read_. Toda vez que a subrotina _read_ é invocada, ela retorna uma parte do arquivo, por exemplo,essa parte pode ser uma nova linha. _read_ também informa quantos bytes são retornados. Portanto quando read retorna 0 bytes indica que o conteúdo do aruqivo chegou ao fim.
>[!tip] Um possivel Flashcard
>Como o sistema operacional e seus programas sabem que um arquivo chegou ao final?
># R:
>Através da chamada de sistema _read_ o qual informa a quantidade de bytes retornada após ler um arquivo, se _read_ retornar 0 bytes não há mais informação presente no arquivo e portanto o seu fim foi alcançado.

#### Records
Outros sistemas podem utilizar uma estrutura chamada records para indicar o número de caracteres que existem na linha sem precisar utilizar o _newline_.
>[!info] INFO
>_linefeed_ é o sinônimo para **newline**. Essa sequência também é chamada de CRLF.

## Diretórios e Filenames
Todo processo ativo possui um "_current directory_" e todos os aruqivos presentes neste diretório possuem implicitamente o nome começando com o nome do diretório. Isso ocorre para permitir nomes iguais para arquivos em diferentes diretórios. O "Current Directory" é um atributo do processo e não de um usuário ou de um programa.

>[!tip] Comando ls – list
>Lista todos os arquivos ou subdiretorios do diretorio atual ou de qualquer outro diretorio passado como argumento.
>

>[!tip] Comando du – disc usage
>Informa o quanto de espaço em disco é consumido para armazenar os arquivos dos diretórios inlcluíndo  todos os sub-diretorios pertencentes.
>Exemplos:
>1. `$ du -hc` – Mostra o espaço em disco consumido pelos arquivos com medidas em K,MB,GB a opção -c informa o espaço total consumido no final da saída.
>2. `$ du -hc | tail -n 1 > consumo_dir.txt` – Copia para o arquivo "consumo_dir.txt" o espaço total consumido pelo diretório.
>3. `$du -ahc | grep "filename"` – Busca pelo custo de armazenamento de um arquivo ou subdiretório especifico.

Apesar das propiedades fundamentais dos diretórios dentro do kernel, eles são postos como qualquer outro arquivo no sistema de arquivo.

### Root Directory
O diretório '_/_' é chamado de raiz do sistema. Todos os arquivos do sistema estão em algum nível de sub-diretório apartir do diretório raiz.

### Permissões
Todo os arquivos possuem um conjunto de permissões a respeito da manipulação pelo usuário. 

>[!tip] Comando _su_
> Altera o usuário para o modo administrador "root" do sistema.

>[!tip] Comando _chmod_
>Permite alterar a permissão de arquivos. As permissões passadas para o comando chmod pode ser de duas maneiras:
> 1. Números em formato Octal
> 	> A representação em octal funciona de maneira de adicionar valores para cada permissão por exemplo: para leitura é 2, para escrita é 4 e para leitura e escrita é 2+4=6. Isso deve ser feito cada grupo de permissão separado.
> 	- Exemplo: `$ chmod 666 junk`
> 2. Representação simbólico
> 	> A representação simbólica é dificil de explicar, mas a ideia é que para cada permissão que queira adicionar ou remover basta utilizar os sinais '+' e '-' na frente da permissão
> 	- Exemplo: `$ chmod -w junk` removerá a permissão de escrita do usuário atual.
> 
>[!tip] Comando _ls -l_
>É utilizado para listar os arquivos e informações de ownership e permissões.
>As permissões listadas de modo -rw-r--r-- que representa que o primeiro '-' em branco o arquivo não é um diretório senão seria um 'd', seguindo rw representa que o root(dono) do arquivo possui permissões de ler e escrever. O próximo r-- significa que o grupo possui permissão apenas para ler. o próximo r-- significa que os demais usuários possuem permissões apenas para ler.

>[!info]Atenção
>Modificar a permissão de um arquivo ou diretório não altera a **data** de modificação dele. A data de modificação reflete somente a alteração do conteúdos nos arquivos ou diretórios.
>As permissões e datas de modificação não são armazenadas no próprio arquivo mas em uma estrutura de sistema chamada index node.
>
#### Uid – user id
Quando um usuário faz login no sistema ele passa o nome de login e a senha, entretanto o Unix trata cada usuário com um número de identificação _uid_. 


#### Grupos
O sistema classifica os usuários em grupos, um grupo serve para automatizar a permissão dos usuários aos arquivos e ao sistema. 


>[!tip] Descobrir o uid e group-id do usuário
> `$ grep 'username' /etc/passwd`
> A saída é um string no formato: _login-id:password:uid:group-id:miscelanous:login-directory:shell_
> Exemplo: _jao:*:1002:1002:jao/home/jao:/bin/sh_
> 

### /etc/passwd
O arquivo _passwd_ que fica localizado no diretório /etc apartir da raiz do sistema contém informações de login de cada usuário do sistema.

### i-nodes
Arquivos possuem diversas informações atreladas como: 
- nome do arquivo
- conteúdo
- informações administrativas: permissões, datas, etc.
- informações do sistema: tamanho do arquivo, localização no disco
Internamente o sistema não trabalha com os nomes dos arquivos mas com _i-numbers_ para identificar arquivos.
>[!info] i-numbers
>São armazenados nos dois primeiros bytes do diretório antes do nome

## Hierarquia de diretórios
O diretório raiz do sistema é o diretório _/_ Alguns outros diretórios que podemos acessar apartir do root são:
- /bin – é o diretório que contém os programas básico para shell como o [[#ED Text Editor]]
- /boot 
- /dev – devices (dispositivos)
- /etc – contém vários arquivos administrativos do sistema, como o arquivo contendo informações de login dos usuários, informações do shell e alguns programas do sistema.
- /lib - (library) contém partes do compilador da linguagem C, como seu preprocessador. e _C subrotine library_ 
- /tmp – armazena arquivos temporários criados durante a execução de programas.
- /unix – é diretório que contém o programa para o próprio kernel do UNIX.
- /usr – é o diretório dos arquivos dos usuários. pode conter alguns dos mesmos diretórios em _/_ como usr/bin, usr/tmp mas que possui um impacto menos crítico ao sistema.

### Dispositivos
Uma das ideias mais legais do UNIX é a forma de como é manejado os periféricos – disco,fita,drivers,terminais, etc. Ao invés de haver rotinas de sistema para ler estes dispositivos, existe um arquivo chamado _/dev/mt0_ (podendo váriar de distribuição). Dentro do kernel referencias para este arquivo são convertidos em comandos de hardware para acessar os dispositivos periféricos e então escrever o conteúdo dos dispositivos é retornado.
#### Exemplo de arquivos presentes no diretório /dev 
![[dev_dir_content.png]]
A imagem acima mostra como ls exibe as informações de um i-node que especifica um dispositivo em contraste ao arquivo regular. Algumas coisas para notar é que a permissão inicial é sempre 'c' ou 'b'. 
Por razões históricas e facilidade de manutenção o sistema de arquivos (file system) é dividido em subsistemas menores. Os arquivos em um subsistema são acessiveis a partir de um diretório no sistema principal. O sistema raiz ocupa o diretório _/dev/rp00_ e os arquivos e subdiretórios de _/usr_ estão residem em _/dev/rp01_.
O _root system_ precisa estar presente o sistema executar, dessa foram os diretórios _/bin_ _/dev_ e _/etc_ são sempre mantidos no _root system_, pois quando o sistema ligar **APENAS** arquivos no root system são acessiveis, e alguns arquivos e programas em /bin são necessários. Durante o processo de bootstrap é verificado a _self-consistency_ dos sistemas e conectados ao sistema raiz. Essa conexão é chamada de _mounting_. após a montagem do _/dev/rp01_ como _/usr_, os arquivos no sistema de arquivos são acessados exatamente como se fossem para do sistema raiz.

> [!tip] Comando _df_
> Informa a quantidade de espaço livre nos nos sistemas de arquivos montados
> Exemplo: `$ df -h`
> ![[command_df_output.png]]
> - Na coluna mais da esquerda mostra os dispositivos do sistema de arquivo na pasta /dev
> - Nas colunas intermediárias mostra algumas estátisica do sistema de arquivos como espaço ocupado / livre.
> - Na coluna mais a direita mostra o diretório onde foi montado o dispositivo do sistema de arquivos.

> [!info] Redirecionar a saída do terminal para o própio dispositivo de terminal
>  1. Descobrir qual é o dipositivo de terminal através do comando `$ who am i`
>  2. Como resposta temos "/dev/ttys000" como o terminal do usuário 'joao'
>  3. redirecionar um "hello world" utilizando o arquivo de terminal com ">" `$ echo "Hello World" > /dev/ttys000`
>  

_/dev/tty_ é o arquivo do dispositivo do terminal de login, também é particularmente importante quando um programa precisa interagir com um usuário mesmo que o standard i/o esteja  conectado com arquivos ao invés do terminal. 

## /dev/null
Este dispositivo haje como se fosse um limbo para a saída de dados de programas. Dados escritos no /dev/null são discartados diretamente. Equanto que programas que lerem deste dispositivo receberão _end-of-file_ automaticamente uma vez que sempre retornará 0 bytes.
>[!tip] Uso típico
>_/dev/null_ pode ser útil quando queremos rodar diagnostico de algum programa sem se importar com a saída produzida. Um exemplo claro dessa situação é rodar o comando _time_ em conjunto com outro programa redirecionando a saída deste para este dispositivo.
>Exemplo: `$ time neofetch > /dev/null`


## Referências do 2º capítulo

- Unix implementation [artigo](https://ieeexplore.ieee.org/document/6770405) 
- "The evolution of the UNIX time-sharing system" (symposium on language design and programming methodology) [artigo](https://ieeexplore.ieee.org/document/6771908) 
- The MULTICS System: An Examination of its Structure [livro](https://www.goodreads.com/book/show/3967095-the-multics-system?from_search=true&from_srp=true&qid=lbsaMHdrtv&rank=1) 

# Terceiro Capítulo: USANDO O SHELL





