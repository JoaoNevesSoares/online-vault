# Overview
>[!tip] Terminologia
> - **Maquina**: É a representação do hardware/computador em que o sistema operacional está rodando
> - **Memoria física**: É a memória principal do computador
> - **Palavra**: É a unidade fundamental de memória para acesso/armazenamento de dados no SO. Cada palavra de memória pode armazenar uma *String* representando uma sequência de caractere ou valor inteiro.
> - **Processo**: É basicamente um programa em execução
> - **Kernel**: É uma coleção de rotinas de sistema operacional que são executadas no modo de sistema é chamada de kernel do sistema operacional.
> - **Multiprogramming**: Vários processos residem na memória simultaneamente e o sistema operacional compartilha o tempo da máquina entre os processos por meio do agendamento. Os processos são ditos executar concorrentemente. Um sistema operacional que suporta a execução concorrente de processos é chamado de sistema operacional de multiprogramação.
# Conceitos primitivos
- Um processo rodando em modo usuário (modo não privilegiado) tem acesso limitado a recursos, como: instruções de máquina, registradores e conjunto limitado de endereços de memória, esse último chamado de **espaço de endereçamento virtual do processo**. Esse modelo de máquina restrito fornecido pelo SO é chamado de *modelo de máquina virtual*.

- Ao final do *bootstrap* (processo de inicialização), o sistema operacional cria manualmente o primeiro processo de usuário chamado de *INIT process* na memória. O processo INIT cria um processo de usuário especial chamado de **shell** carregando e executando um **programa shell** do disco. O programa shell lê repetidamente comandos de usuário da entrada e executa programas especificados pelo usuário.

- O eXpOS trata os dispositivos de *standard I/O* como se fossem **arquivos especiais**. Dessa forma os processos de usuário devem usar chamadas de sistemas de read/write em arquivo para executar operações de I/O.

- O disco geralmente é dividido em **blocos** e a máquina fornece instruções para transferir blocos do disco para memória virtual e vice-versa.

- O eXpOS pressupõe um dispositivo *timer* de hardware que pode interromper a máquina em **intervalos regulares pré-definidos**. O manipulador (*handler*) de interrupção do temporizador é o *scheduler* do kernel do eXpOS, que é responsável por compartilhar o tempo da máquina entre os processos.

- O eXpOS pressupõe que a máquina forneça hardware de *paging* para implementar o **mapeamento do espaço de endereçamento virtual de um processo na memória física da máquina**.


# Processo
- Uma vez que um processo é criado, ele pode gerar novos processos usando a chamada de sistema *fork*. Quando um processo gera um novo processo, o anterior é chamado de processo pai (*parent process*) e o novo de processo filho (*child process*). 

- Um processo pode decidir terminar a si mesmo usando a chamada de sistema exit.

- O **espaço de endereço virtual** é um espaço de *endereço contínuo* que começa no endereço 0 e vai até um limite máximo que depende da implementação. Internamente o SO mapeia o espaço de endereço virtual na memória principal usando mecanismos de *paginação / segmentação* 

- O eXpOS divide logicamente o espaço de endereçamento virtual de um processo em regiões de *library*, *code*, *stack* e *heap*.
- Quando um novo processo é criado com a chamada de _fork_, o processo filho herda _library, código, heap_ do processo pai. Isso significa que qualquer modificação nos endereços que residem nessas regiões da memória por um dos processos afeta ambos os processos.
- O pai e o filho prosseguem com a execução simultaneamente(_concurrently_) a partir da instrução imediatamente após a chamada de fork no código.

>[!tip] Compartilhamento de recursos entre processos
>Já foi observado que o processo filho compartilha o heap do processo pai. Portanto, a memória alocada no heap será uma memória compartilhada entre **ambos** os processos. 
>No entanto, se o processo pai ou o processo filho carregar outro programa em seu espaço de endereço virtual usando a chamada de sistema exec, então o heap compartilhado é **desvinculado** desse processo e o processo sobrevivente manterá o heap intacto. Os ponteiros de arquivo manipulados pelo processo pai também são compartilhados pelo processo filho. 
>Assim, o eXpOS não oferece suporte a primitivas explícitas para compartilhamento de memória, mas permite que processos relacionados compartilhem esses recursos implicitamente usando a semântica da chamada de sistema fork.

## Process System Call

## Idle Process
O processo ocioso é um processo de usuário criado pelo kernel durante o processo de inicialização. Ele executa um loop infinito. Seu objetivo é garantir que haja pelo menos um processo de usuário para o escalonador agendar. O sistema operacional escalonará o processo ocioso quando todos os outros processos de usuário estiverem em estado de espera. O processo ocioso nunca é trocado (swapped).