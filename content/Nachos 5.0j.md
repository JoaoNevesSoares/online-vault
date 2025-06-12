# Introdução
Nachos é sistema operacional com propósito educacional desenvolvido em 1992 na UC Berkley, o objetivo é ser um OS simples e modular o suficiente para que alunos consigam implementar e modificar diversos componenetes do sistema operacional durante um semestre acadêmico. De acordo com os autores essa abordagem permite que os alunos pratiquem escrever e testar programas concorrentes. Eles aproveitam para fazer com que os estudantes avaliem e expliquem o desempenho de suas implementações em alguns testes simples.
Diferente do MINIX, ele roda em um processo normal do sistema operacional, sendo o hardware utilizado emulado em software. A vantagem está na simplicidade da implementação, por exemplo, no UNIX, só o código para acessar o dispositivo de disco são quase 5.000 linhas. Já no Nachos, o disco é simulado como um diretório no sistema operacional, e as operações de leitura e escrita são simuladas com as próprias chamadas da linguagem para I/O.
# Overview
- Nachos simula execução de instruções MIPS/R2 3000 _somente_ para instruções de programas do usuário. Isso permite que seja possível capturar _page faults_ e outras _exceptions_ no código dos alunos.
- As instruções do Kernel, executam em código nativo C++ e Java, por dois motivos: 
	1. Por ser mais simples, reaproveita chamadas de sistemas das linguagens C++/Java.
	2. Ser mais rápido. sem indereções.

Dessa forma o sistema operacional possuí dois modos de execução: – **Modo usuário**, – **Modo Kernel**.

# Máquina Virtual

## Arquivo de Configuração
A máquina virtual do Nachos pode ser configurada de maneira diferente para cada projeto usando um arquivo do tipo `.conf`
>[!info] .conf files 
> Esse arquivo é como se fosse à configuração da BIOS ou OpenFirmware. No *freebsd* temos que editar esse arquivo toda hora, seja para mudar o layout do teclado, configuração servidor DHCP, ou habilitar o sshd.

Esse arquivo possui uma lista de configurações do tipo `key = value`. Da para configurar o escalonador padrão, modificar a quantidade de memória, entre outros.
![[Screenshot 2023-05-17 at 14.14.03.png]]

>[!tip] Selecionar a máquina virtual
>Podemos colocar uma opção para selecionar uma configuração para alterar a máquina virtual. (Simular Mips ou Dummy machine). 


## Processo de Boot
O ponto de partida do Nachos é o método `machine.Machine.main()`, ele que realiza o "boot da máquina da máquina virtual" de acordo com os seguintes passos:
1. `processArgs()` – Processa os argumentos passados por linha de comando para o Nachos, uma lista de comandos pode ser encontrada no final desse documento, mas um que nos importa por agora é **-m "numero de páginas físicas da memória"** (tamanho da página é _1KB_).
2. `Config.load(configFilenName)` – Faz o parsing do arquivo _.conf_ e carrega para uma HashMap.
3. `createDevices()` – Cria os dispositivos da máquina de acordo com o especificado no arquivo de configuração. Os dispositivos podem ser:
	1. `Machine.processor` – processador que interp ISA
	2. `Machine.console` – console !?
	3. `Machine.StubFileSystem` – sistema de disco !?
	4. `Machine.networkLink` – Um placa de rede !?
4. `Lib.constructObject(autoGraderClassName)` – Cria um objeto da clase _Autograder_, esse objeto é basicamente o "faz-tudo" do Nachos. Ele serve para criar o kernel do SO e rodar _testes_ e _avaliar a implementação do sistema_. A minha melhor descrição seria que essa classe "roda" o SO.
5. `TCB.start(new Runnable())` – Cria o primeiro objeto TCB passando um objeto Java _Runnable_ que cria uma nova _thread Java_ executando o método `autoGrader.start()`. Vai ter uma thread do SO mapeada em uma thread do Java, executando o Autograder que cria o kernel do SO especificado no arquivo .conf e depois executa algo no método .run() que pode ser subscrito.

# Kernel
## `Machine.Kernel` => Um template de Kernel
> Classe abstrata que implementa uma interface que especifica a assinatura de 3 métodos que devem ser implementados por um Kernel do Nachos.
- `initialize(args [])` – Descreva a construção e inicialização do Kernel
- `selfTest()` – Testa se o kernel implementado funciona
- `run()` 
- `terminate()`
Entre as classes já preestabelecidas no Nachos que estendem a interface Kernel está:

### ThreadedKerned
> "_Allocate a new multi-threaded kernel_."

`initialize()`
1. Cria um Escalonador, baseado no .conf
2. Cria primeira Thread (`new KThread(null)`)
3. Um alarme
4. O sistema de arquivo se foi especificado no arquivo de configuração
5. Ativa as interrupções de sistema

`selfTest()` 
1. Testa se a implementação de Kthread está funcionando
2. Testa os mecânismos de sincronização

`run()`
1. Vazio, esse kernel não executa programa do usuário.
2. Esse metodo não faz nada nesse kernel

`terminate()`
_Halts the machine execution_

### A ideia que possamos criar nosso proprio kernel para o simulador que suporte memória virtual,  vários processos, etc.

## Atributos
```java
/** Globally accessible reference to the scheduler. */
public static Scheduler scheduler = null;

/** Globally accessible reference to the alarm. */
public static Alarm alarm = null;

/** Globally accessible reference to the file system. */
public static FileSystem fileSystem = null;
```

# TCB
> A TCB simulates the low-level details necessary to create, context-switch, and destroy Nachos threads. Each TCB controls an underlying JVM Thread object.

## Método `start(Runnable Target)`
Faz com que a Thread representada pelo objeto TCB comece a executar o trabalho especificado em `Target`
> Não realiza sincronização, porque assume que: É primeira chamada após criar o TCB, ou/e `start` está sendo chamada no contexto de outra TCB. Uma vez que só permite que 1 objeto TCB rode por java Thread por vez.

Executa o `Target` com o método `Runnable.run()` 
## Método `contextSwitch()`
> Troca o contexto entre o TCB attual e o TCB que invocar esse método, virando a ser o TCB atual, (se for possível)
```java
...

TCB previous = currentTCB;

previous.running = false;

this.interrupt();

previous.yield();
```

## Método `destroy`

## Atributos
```java
// atributos que pertencem a classe e não ao objeto
public static final int maxThreads = 250;
private static TCB currentTCB = null;
private static Vector<TCB> runningThreads = new Vector<TCB>();
// atributos que pertencem ao objeto em si.
private boolean isFirstTCB;
private Thread javaThread = null;
private boolean done = false;
private KThread nachosThread = null;
private boolean associated = false;
private Runnable target;
private Runnable tcbTarget;
```
---
>[!Note] Ideia
>Nossa interface do simulador pode rodar como uma thread java representada pelo TCB.

# Threads

> Todas as Threads do NachOS são derivadas da classe `threads.KThread`, (thread de sistema ou thread de usuário)
- Cada Kthread possui um objeto TCB que fornece suporte de baixo nível para trocas de contexto, criação e destruição de threads, e suspensão de threads.
- Cada objeto Kthread tem um campo `status` para monitorar o estado corrente da thread, pois alguns métodos vão falhar se forem chamados em um estado inválido da Thread.![[Screenshot 2023-05-18 at 02.32.25.png]]
- A primeira Kthread **é sempre** criada na rotina de inicialização do Kernel.
A primeira vez que o construtor do Kthread é chamado ele executa os seguintes passos:
1. Cria a fila de _prontos_ – `scheduler.newThreadQueue()`
2. Aloca o CPU para kthread que foi criada
3. Muda `currentThread` para apontar para thread criada
4. Seta objeto TCB da kthread criada para ser o `TCB.currentTCB()`
5. Altera o status de (new) para (Ready)
6. Cria uma thread `idle` e coloca para esperar infinitamente
Depois dessa sequência, a primeira thread criada é a _main_ thread, ela pode criar novas threads, pode se matar e também pode se bloquear.( a execução só termina quando todas as threads terminaram, não importa se a thread _main_ estiver morta ou não). Nessa mesma ideia, se não existir nenhuma thread pronta para executar, o SO vai trocar para thread `idle`.
>[!tip] Interessante
> Sempre quando o construtor de Kthread for chamado por uma thread executando, ele vai criar um objeto TCB com status `new` vai chamar o método `fork()` que vai colocar a thread Java associada com a thread criada para começar a executar, e vai chamar `Kthread.ready()` para colocar a thread atual na fila de prontos.


>[!info] Thread Impl
>Nachos implements threading using a Java thread for each TCB object. The Java threads are synchronized by the TCBs such that exactly one is running at any given time. This provides the illusion of context switches saving state for the current thread and loading the saved state of the new thread.

# Scheduler
> A classe `threads.Scheduler` define uma interface para implementar políticas de escalonamento. A política `default` é _RoundRobinScheduler_ que implementa uma fila **FIFO**

> A classe `threads.Queue` define uma interface para implementar uma fila de threads. a fila padrão usa algoritmo `fifo`.

Um escalonador é responsável por "escalonar" as threads para os recursos disponíveis no sistema. Um recurso pode ser a **CPU** mas também pode ser um buffer, ou um _semáforo_. Um ponto importante é que, a implementação do recurso, é o responsável por adicionar as threads na fila de threads. `waitForAccess()`. Em outras palavras: O recurso _é responsável por gerênciar o acesso a ele mesmo_. 
- Portanto, toda decisão do escalonador se reduz a selecionar a próxima thread da fila de threads.
- A implementação da fila de thread, é quem define qual será o próximo thread da fila.

>[!info] Nota de Implementação
>Apenas um "tipo" de escalonador pode ser utilizado por todos os recursos.
>Implementar um novo escalonador, implica em implementar a propria fila de threads, ou utilizar uma fila já existente.

# Gêrencia de memória
Pelo que eu entendi, a memória implica existir um processador, que na maioria das vezes, implica executar programas do usuário. Pelo que eu entendi as construções da memória estão relacionado com a ISA do mips implementado, por exemplo a resolução de endereços do programa do usuário para endereços "físicos". TLB, etc.
# Trabalhos futuros
- Melhorar a simulação de rede
- Implementar kernel do Nachos para sistemas distribuídos em redes.

# a 
## aa
### aaa
#### aaaa
##### aaaaa
###### aaaaaaaa
