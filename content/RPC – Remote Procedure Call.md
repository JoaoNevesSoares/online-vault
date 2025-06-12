# Introdução
No paradigma cliente-servidor, os usuários interagem com aplicativos clientes que solicitam tarefas aos servidores. A comunicação entre clientes e servidores ocorre por meio de um mecanismo de SEND/RECEIVE utilizando sockets. Os sockets fornecem uma interface de comunicação de mais baixo nível que permite o estabelecimento de conexões entre as máquinas cliente e servidor pela rede. O RPC, introduz uma abstração adicional nesse esquema, permitindo que os clientes se comuniquem com os servidores por meio de chamadas a procedimentos.
Em poucas palavras, O RPC permite que procedimentos sejam chamados remotamente. Quando um processo na máquina A chama um procedimento na máquina B, o processo chamador em A é suspenso e a execução do procedimento chamado ocorre em B, como podemos ver na figura abaixo. Os dados de entrada são passados por parâmetros para a chamada remota e retornados por resultados do procedimentos. Nesta técnica nenhuma troca de mensagens é visível ao programador.[tanenbaum,1994]
![[Screenshot 2023-05-11 at 11.03.37.png]]

Existem duas categorias de RPC:
1.  Na primeira categoria, o RPC é incorporado a uma linguagem de programação. Isso traz a vantagem de ter a IDL (Interface Description Language) integrada às construções da linguagem, facilitando aspectos como o tratamento de exceções. Exemplos disso são os sistemas Cedar, Argus e Arjuna.
2.  Na segunda categoria, é utilizada uma linguagem específica para definir a interface entre clientes e servidores. Essa abordagem tem a vantagem de não exigir o aprendizado de uma nova linguagem de programação, permitindo aproveitar o conhecimento já adquirido. Na prática, a linguagem comumente usada é C, que se estabeleceu como um padrão para desenvolver aplicativos desse tipo. Exemplos incluem o SunRPC, base do NFS (Network File System), o Sistema ANSA e o MIG, utilizado no sistema operacional Mach.
# Funcionamento Básico de uma RPC
Como já foi comentado, o mecanismo de RPC tem que ser transparente, ou seja, para o programador as chamadas têm que parecer locais. Dessa forma é necessário introduzir alguns elementos que vão esconder as complexidades inerentes ao problema. Para isso é utilizado dois componentes fundamentais para esse processo que atuam como "middleware": 
- Cliente Stub – também conhecido como "proxy" ou "stub do cliente", é responsável por fornecer uma interface local no cliente que se assemelha à chamada de um procedimento local. Quando o cliente faz uma chamada a um procedimento remoto, o cliente stub é invocado em vez do procedimento real. O cliente stub empacota os parâmetros da chamada em uma mensagem de requisição e a envia para o servidor remoto por meio da rede.
- Servidor Stub – também conhecido como "skeleton", é responsável por receber as mensagens de requisição do cliente stub. Ele desempacota os parâmetros contidos na mensagem de requisição e invoca o procedimento remoto correspondente. Após a execução do procedimento, o servidor stub empacota o resultado em uma mensagem de resposta e a envia de volta para o cliente através da rede.

Para resumir, uma chamada remota de procedimentos envolve os seguintes eventos:
1.  O procedimento do cliente faz a chamada ao stub do cliente de forma normal.
2.  O stub do cliente constrói uma mensagem e faz uma chamada ao sistema operacional local.
3.  O sistema operacional do cliente envia a mensagem para o sistema operacional remoto.
4.  O sistema operacional remoto entrega a mensagem ao stub do servidor.
5.  O stub do servidor desempacota os parâmetros e faz a chamada ao servidor.
6.  O servidor realiza o trabalho e retorna o resultado para o stub.
7.  O stub do servidor empacota o resultado em uma mensagem e faz uma chamada ao seu sistema operacional local.
8.  O sistema operacional do servidor envia a mensagem para o sistema operacional do cliente.
9.  O sistema operacional do cliente entrega a mensagem ao stub do cliente.
10.  O stub desempacota o resultado e o retorna para o cliente.

Essa sequência de eventos descreve o fluxo básico de uma chamada de procedimento remoto (RPC). O cliente chama o seu stub local, que constrói uma mensagem contendo os parâmetros da chamada e a envia para o sistema operacional do cliente. Em seguida, a mensagem é transmitida para o sistema operacional remoto, que a entrega ao stub do servidor. O stub do servidor desempacota os parâmetros, chama o servidor real para realizar o trabalho e recebe o resultado de volta. O stub do servidor empacota o resultado em uma mensagem e a envia de volta para o sistema operacional do servidor, que a transmite para o sistema operacional do cliente. Por fim, o stub do cliente desempacota o resultado e o retorna para o cliente original.

Essa sequência de eventos demonstra como os stubs do cliente e do servidor atuam como intermediários para facilitar a comunicação entre o cliente e o servidor no RPC, abstraindo a complexidade da comunicação de rede e permitindo que os procedimentos remotos sejam chamados e os resultados sejam transmitidos de forma transparente. 
Os eventos envolvidos durante uma chamada remota de procedimentos pode ser vista na figura abaixo para o procedimento `doit(a,b)`
![[Screenshot 2023-05-11 at 12.10.59.png]]

# RPC Semantics in the Presence of Faults

## Perda de Mensagens de Resposta
- Usa um _timeout_ para solucionar o problema, reenvia a mensagem.
- faz com que cada mensagem RPC contenha um número de seqüência para que o servidor diferencie mensagens novas de repetidas, usar um bit indicar essa situação
## Falha/Crash do Servidor 
Se depois de várias tentantivas fracassadas, o que poderá acontecer dependaera da semântica da chamada:
-  Semântica Maybe → Não é assegurada a tolerância a falhas. Em geral, os clientes não são capazes de determinar se a chamada foi efetivamente executada. Fácil de implementar, porém não é uma solução aceitável para a maioria dos casos.
-  Semântica At-least-once → Garante que a solicitação foi executada uma ou mais vezes. Se as operações do servidor são todas idempotentes, então não há problemas.
![[Screenshot 2023-05-11 at 13.14.07.png]]
-  Semântica At-most-once → Garante que a solicitação foi executada no máximo uma vez, mas pode também não ter sido executada. É a semântica mais utilizada nas implementações de RPCs.
![[Screenshot 2023-05-11 at 13.14.16.png]]
-  Semântica Exactly-once → A chamada é executada uma única vez. Seria o tipo ideal de semântica, mas é difícil consegui-lo, especialmente se existir ações externas que não podem ser desfeitas.
![[Screenshot 2023-05-11 at 13.18.09.png]]
# RPC Assíncrono
Uma variação em torno do RPC é o RPC assíncrono, que são um tipo de RPC que não exige que o cliente se bloqueie aguardando a resposta do servidor e, às vezes, não requer nem mesmo que uma resposta seja enviada. O benefício do RPC assíncrono é que ele vem justamente eliminar algumas “desvantagens” do RPC convencional, como, por exemplo, a necessidade do cliente bloquear-se esperando pela resposta do servidor, ao invés de ficar executando outras operações em paralelo, o que melhoraria a resposta do sistema. Outra vantagem é que o RPC assíncrono também possibilita que um cliente envie requisições em paralelo a diversos servidores. Uma utilidade aparente do uso de RPC assíncronos é em aplicações de gerência de janelas em interfaces gráficas. Este tipo de aplicação pode ser programado como um servidor e os programas que quiserem mostrar textos ou gráficos em uma janela devem enviar solicitações a ele. Aqui, fica clara a melhoria de desempenho proporcionada pelo RPC assíncrono, uma vez que a mensagem do cliente, muitas vezes, é um caracter ou um movimento do apontador do mouse e a resposta vem a ser a própria alteração na tela, não sendo necessário e até indesejável o bloqueio do cliente a cada tecla pressionada.
_A figura abaixo exemplifica a interação entre cliente-servidor utilizando RPC síncrono (1° figura) e o RPC assíncrono (2°)._
![[Screenshot 2023-05-11 at 12.46.20 1.png]]
---
![[Screenshot 2023-05-11 at 12.46.45.png]]


# Extra
> Discuta a implicação da aplicação das seguintes semânticas para RPC para implementar um servidor RPC assíncrono: at-least-once (onde deve ser garantido que a requisição será atendida ao menos uma vez) e at-most-once (onde deve ser garantido que nenhuma requisição será atendida mais de uma vez), no entendimento aos serviços solicitados pelo cliente. Considere a seguinte aplicação exemplo: o servidor é responsável por gerar Arquivos PDF de material recebido pelo cliente. Relate, em particular, quais são as consequências no atendimento às requisições e qual o comportamento esperado do usuário em cada caso.

A semântica "at-least-once" implica que o servidor RPC assíncrono garante que cada requisição será atendida ao menos uma vez. Isso significa que, mesmo que ocorram falhas temporárias durante a comunicação, o servidor fará todas as tentativas necessárias para processar a requisição e enviar a resposta ao cliente. Se a primeira tentativa de processamento falhar, o servidor tentará novamente até que a requisição seja processada com sucesso.

No contexto do exemplo dado, em que o servidor é responsável por gerar arquivos PDF a partir do material recebido pelo cliente, a aplicação da semântica "at-least-once" implica que o servidor fará todas as tentativas necessárias para processar cada requisição de geração de PDF. Mesmo que ocorram problemas temporários de rede, falhas de servidor ou outros obstáculos, o servidor continuará tentando processar a requisição até que seja bem-sucedido. O comportamento esperado do usuário nesse caso é que, mesmo que ocorram atrasos ou interrupções temporárias, o servidor eventualmente atenderá à solicitação de geração do arquivo PDF.

Por outro lado, a semântica "at-most-once" implica que o servidor RPC assíncrono garante que nenhuma requisição será atendida mais de uma vez. Isso significa que o servidor fará todas as tentativas necessárias para processar a requisição, mas garantirá que a resposta seja enviada ao cliente apenas uma vez. Se ocorrerem falhas durante o processamento da requisição, o servidor descartará a resposta anterior e iniciará novamente o processamento para evitar respostas duplicadas.

No exemplo do servidor de geração de arquivos PDF, a aplicação da semântica "at-most-once" significa que o servidor garantirá que nenhum arquivo PDF seja gerado mais de uma vez para a mesma solicitação do cliente. Se ocorrerem falhas temporárias ou interrupções de comunicação durante o processamento, o servidor descartará qualquer resposta anterior e reiniciará o processamento para evitar a geração duplicada do arquivo PDF. O comport
# Refêrencias
https://datatracker.ietf.org/doc/html/rfc5531
http://www.deinf.ufma.br/~mario/grad/redes2/rpc_cap.pdf
https://web.fe.up.pt/~pfs/aulas/sd2021/at/5rpc.pdf
https://www.ime.usp.br/~reverbel/SMW-07/Slides/alonso-ch2-RPC.pdf
- M. van Steen and A.S. Tanenbaum, Distributed Systems, 3rd ed., distributed-systems.net, 2017.
-   Coutinho, R. A. (1994). Arquitetura Cliente-Servidor: Princípios e Práticas. Rio de Janeiro: Campus.
- Coulouris, G., Dollimore, J., Kindberg, T., & Blair, G. (2011). Distributed Systems: Concepts and Design (5th ed.). Addison-Wesley.