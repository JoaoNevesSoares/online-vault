>[!warning] Este documento está em construção

# Aspectos gerais
De acordo com a seção de trabalhos relacionados nos artigos que observei, os autores costumam classificar os simuladores presentes na literatura em duas grandes classes de acordo com complexidade do simulador:
1. Simuladores completos, que são os que incluem a maioria dos componentes presentes em um sistema operacinal, como gerênciamento de processos, gerênciamento de memória, I/O, interrupções de sistema, etc.
Podemos citar como exemplo de simuladores que pertencem a essa classificação, SOsim, YASS, 
2. Ferramentas para simulação de componentes especificos do sistema operacional, em muitos casos, esses trabalhos prezam pela precisão na simulação do componente ou na eficiencia/desempenho apresentado.
Como exemplo: TBC-SO/WEB,VizzScheduler-A,Visualizing Dynamic
Memory Allocations, entre outros.

# Métricas para direcionar o desenvolvimento e a implementação do nosso simulador
Com base no artigo "Apoio ao Aprendizado em Arquitetura e Organização de Computadores: Um Estudo Comparativo entre Simuladores Computacionais" apresento algumas métricas que podem fundamentar os requisitos funcionais e não funcionais desejáveis no nosso simulador.

| Id  | Métrica                                        | Descrição                                                                                                                                                                                                                                                    |
| --- | ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | 
| 1   | Portabilidade/Disponibilidade                  | Disponibilização da implementação do simulador para diferentes sistemas operacionais, arquiteturas, e hardwares                                                                                                                                              |
| 2   | Parametrização                                 | Presença de mecanismos que permitam alterar a configuração das caracterisitcas dos componentes do simualdor, como prioridade dos procesos, CPU time, número de páginas ativas por processo,tempo de chegada,entre outros                                     |
| 3   | Suporte a código externo                       | Possibilidade do usuário extender as funcionalidades do simulador e modificar o código dos componentes, codificar o comportamento dos mecanismos do sistema operacinal                                                                                       |
| 4   | Modos/Perfis de simulação                      | Suporte a diferentes modos de simulação, como simulação passo a passo, contínua, comparação entre dois mecanismos ao mesmo tempo, animação da troca de contexto entre estados do processo                                                                    |
| 5   | Visualização do estado interno do SO           | Visualização da comunicação entre os componentes, visualização do conteúdo de memória, do disco, histórico de processos ativos, entre outros coisas                                                                                                          |
| 6   | Estátisticas de Simulação                      | Mecanismos para sumarização dos eventos gerados pelos componentes do SO, durante uma simulação, verificação do tempo de execução, throughtput de jobs concluídos, gargalos de desempenho, utilização de memória, numero de interrupções I/O (Acesso a disco) |
| 7   | Interface Gráfica                              | Presença de interface gráfica para intermediar a interação do usuário com os recursos presentes no simualdor                                                                                                                                                 |
| 8   | Personalização da interface                    | Suporte a mecanismos para ajustes da interface gráfica, como a personalização de cores, botões, tamabho da fonte, tema de background, etc                                                                                                                    |
| 9   | Materiais didáticos e documentação de apoio    | Disponibilidade de propostas de exemplos de uso pré-estabelecidos, manual da interface e controles, documentação de desenvolvimento, entre outras coisas                                                                                                     |
| 10  | Facilidade de Suporte, integração e manutenção | Utilizar tecnologias que facilitem a disponibilidade atualizações futuras ao sistema, facilidade de integração com novas plataformas de ensino, e recursos para novos desenvolvedores adotarem o desenvolvimento posterior                                   |

# Trabalhos de conclusão de curso e monografias na area
_Simulador de Gerência de Processos para Sistemas Operacionais_ – Guilherme Moreria Bomfim de Freitas, Universidade Federal de Uberlândia – **2023**
![[Screenshot 2023-04-04 at 23.34.07.png]]
![[Screenshot 2023-04-04 at 23.34.49.png]]
![[Screenshot 2023-04-04 at 23.35.43.png]]
![[Screenshot 2023-04-04 at 23.37.24.png]]

_TBC-SO/WEB: SOFTWARE EDUCATIVO PARA APRENDIZAGEM DE GERÊNCIA DE PROCESSOS E DE GERÊNCIA DE MEMÓRIA EM SISTEMAS OPERACIONAIS_ Fabrício Pereira Reis – **2009**
> [!tip] A interface foi desenvolvida utilizando JAVA

![[Screenshot 2023-04-04 at 23.40.00.png]]
![[Screenshot 2023-04-04 at 23.40.57.png]]
![[Screenshot 2023-04-04 at 23.41.36.png]]
![[Screenshot 2023-04-04 at 23.43.13.png]]

# Propostas de Simuladores em artigos cientificos não foram revisados ainda
SSOG – Um Simulador didático como ferramenta de apoio ao ensino da disciplina de Sistemas Operacionais – https://fai-mg.br/portal/download/revista_inicia_2008/pub_dw_artigo_simulador.pdf
Simulador de Rotinas do Sistema Operacional para Auxilio as Aulas teóricas– https://fai-mg.br/portal/download/revista_inicia_2008/pub_dw_artigo_simulador.pdf
> [!tip] Parece que possui animações 3d para visualizar o gerenciamento de memória
> ![[Screenshot 2023-04-04 at 23.58.01.png]]
> ---
> ![[Screenshot 2023-04-04 at 23.58.37.png]]

_38 citações, Y:2001_,RcOS.JAVA – A simulated Operating System with Animations
https://lekythos.library.ucy.ac.cy/bitstream/handle/10797/14820/C4_Jones_RCOSjava_A%20Simulated%20Operating%20System%20with%20Animations_CBLIS_2001.pdf?sequence=1&isAllowed=y
> [!danger] CPUSim: A Simulator supporting the education of CPU Scheduling Algorithms
> Artigo publicado em Coreano
> https://koreascience.kr/article/JAKO201215239621251.kr
> Fun-Fact: Cita o SOsim do MAIA


# Sistemas Operacionais com propósito educacional
## Minix
não preciso comentar...
## xV6
![[Screenshot 2023-04-05 at 00.17.38.png]]
_Baseado no Unix que rodava no PDP-11, mas atualizado para arquiteturas modernas._
![[Pdp-11-40.jpg]]
### Refêrencias: _Lions' _Commentary on UNIX' 6th Edition, John Lions_ 
https://cs3210.cc.gatech.edu/r/unix6.pdf
### Livro Base: _xV6:  a simple, Unix-like teaching operating system_
https://pdos.csail.mit.edu/6.828/2022/xv6/book-riscv-rev3.pdf
### Source Code
https://github.com/mit-pdos/xv6-public
## Pintos
![[3-Figure2-1-2.png]]
>sistema operacional instrucional para a arquitetura de conjunto de instruções x86. Ele suporta threads do kernel, carregamento e execução de programas do usuário, e um sistema de arquivos, mas implementa todos esses recursos de maneira muito simples. Foi criado na Universidade de Stanford por Ben Pfaff em 2004. Ele surgiu como um substituto para o Not Another Completely Heuristic Operating System (Nachos), um sistema similar originalmente desenvolvido na UC Berkeley por Thomas E. Anderson, e foi projetado ao longo das mesmas linhas. Como Nachos, o Pintos destina-se a apresentar aos alunos de graduação conceitos em design e implementação de sistemas operacionais, exigindo que eles implementem porções significativas de um sistema operacional real, incluindo gerenciamento de threads e memória e acesso ao sistema de arquivos. O Pintos também ensina aos alunos habilidades valiosas de depuração. Ao contrário do Nachos, o Pintos pode ser executado em hardware x86 real, embora geralmente seja executado em um emulador x86, como Bochs ou QEMU. O Nachos, por outro lado, é executado como um processo do usuário em um sistema operacional host e tem como alvo a arquitetura MIPS (o código do Nachos deve ser executado em um simulador MIPS). O Pintos e suas atribuições acompanhantes também são escritos na linguagem de programação C, em vez de C++ (usado para o Nachos original) ou Java (usado para o Nachos 5.0j).

### Livro de Refêrencia:
https://web.stanford.edu/class/cs140/projects/pintos/pintos.pdf

## Tropix
![[tropix.gif]]
> O **TROPIX** (pronuncia-se "Trópix") é um Sistema Operacional multiusuário e multitarefa, de filosofia UNIX ®, desenvolvido no Núcleo de Computação Eletrônica da Universidade Federal do Rio de Janeiro (NCE/UFRJ). 
> O TROPIX foi inicialmente concebido durantes os anos de 1982 a 1986 (na época com o nome PLURIX) para o computador PEGASUS. Este computador foi construído também no NCE, e era baseado nos processadores MOTOROLA 68010/20. O sistema foi transportado em 1987 para o computador ICARUS, também baseado nestes mesmos processadores. Em 1994 foi iniciado o transporte para a linha INTEL de processadores (386, 486, Pentium), e desde 1996 o TROPIX já está operacional em PCs, sendo utilizado em diversos computadores. O TROPIX tem diversas utilidades, tais como o estudo/aprendizado/utilização de um sistema operacional de filosofia UNIX, o desenvolvimento de programas ("software") e a implementação de servidores para a INTERNET (esta página que você está lendo está vindo do servidor WWW de um computador rodando TROPIX). Além disto, é ideal para a utilização em cursos de sistemas operacionais, pois contém primitivas para processos "leves" ("threads"), memória compartilhada, semáforos a nível de usuário, dentre outros. A distribuição do TROPIX é gratuita, segundo a licença pública do GNU.

### Refêrencia: http://www.tropix.nce.ufrj.br


Na literatura, tem-se notado diversos esforços direcionados ao ensino de componentes do sistema operacional como escalonamento de processos e gerenciamento de memória utilizando ferramentas de simulação. O uso de simulação facilita o compreendimento ao permitir a visualização do funcionamento de um sistema operacional de maneira sistemática.