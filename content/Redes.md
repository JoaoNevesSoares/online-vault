>[!info] Horários 📅
>Segunda-feira: 10:00 - 11:50
>Sexta-feira: 13:30 - 15:10

>[!tip] Livro da disciplina
> [Computer Networking: A Top-Down Approach](http://library.lol/main/BC53750BE7CE383B9A7C3B70C2C5DECC)

>[!tip] Protocolos
>[Language Server Protocol](https://en.wikipedia.org/wiki/Language_Server_Protocol)
# Conteúdo
## Unidade 1: Introdução ás Redes de Computadores
_Hosts/End systems_
Nome dado ao hardware que acessa a rede, estes podem ser tanto, computadores tradicionais (desktops,workstations) ou Iot (cameras, carros, telefones, etc.).
_Communication Links_
É o recurso físico que faz a conexão entre os sistemas. podem ser feito de diferentes materiais (como cabo coaxial,fio de cobre, fibra óptica, ondas de rádio) e que resulta em diferentes taxas de transferência.
_Internet Service Providers (ISP)_
Provedores de conexão a internet, podem ser locais(regionais) ou inter regionais. Cada provedor roda o procolo IP em conformidade com as convenções de nomenclaturas e endereços. 

# Protocolo de Rede
>A _protocol_ defines the format and the order of messages exchanged between two or more communicating entitie, as well as the actions taken on the transmission and/or receipt of a message or other event.

## Client and Server model
- Cliente: _Um cliente é um programa rodando no sistema final que faz a request e recebe um serviço de um programa server rodando em outro sistema._
- Client-Server Internet Applications are, by definition: **distributed applicaitons**.
- 

# Camada de Aplicações

# Principios
> Antes de mergulhar no desenvolvimento de aplicações de rede, o desenvolvedor deve ter um plano arquitetural da aplicação.

## Client-Server Architecture
Neste tipo de arquitetura existe um servidor que está sempre conectado e um cliente que pode ou não estar conectado. Um exemplo clássico é o serviço de e-mail (gmail). Outra característica é que o server possui um endereço de IP **fixo** onde o cliente pode sempre realizar conexão para enviar requisições e pacotes.

## P2P architecture
Em vez de existir um programa cliente ou um programa servidor, a aplicação explora a comunicação direta entre os pares de hosts conectados intermitentemente, chamado de _peers_. 
- Uma das vantagens das aplicações P2P é a sua _AUTO-ESCALABILIDADE_. de forma simplória, isso sinifica que para aumentar o poder da rede, basta aumentar o número de usuários (peers), sem a necessidade de comprar data-centers.

## Process Comunicating
O conceito de processos em Redes é o mesmo de Sistemas Operacionais. Um processo é uma instância de um programa rodando em um determinado instante de tempo.
- Processos em dois end-system comunicam-se através de trocas de mensagens através de uma rede de computadores.
### Processos Cliente e Servidor
Uma aplicação de rede consiste de pares de processos que enviam mensagens para cada através de uma network.

#### Socket
É a interface entre a camada de aplicação e a camada de transporte, dentro de um host. Pode-se referir a um socket como uma _API entre a aplicação e a rede_. De certo modo, o desenvolvedor possui controle de tudo que está do lado da camada de aplicação do socket, porém possui pouco ou nenhum controle do lado da camada de transporte. As poucas decisões que um desenvolvedor pode tomar em relação a camada de transporte é:
1. A escolha de qual protocolo de transporte utilizar.
2. Definir alguns parametros como: _Maximum buffer_ e _Maximum segment sizes_. 

## Transport Services Provided by the Internet
A internet(mais específico o protocolo: TCP/IP) provê dois tipos de protoloco de transporte: **UDP** & **TCP**.
>[!info] Developement Info
>When an application developer crate a new network application, _one of the first decisions_ is wheter to use UDP or TCP. Each of these protocols offers a different set of services to the invoking applications.


 ### TCP CONNECTION
 Uma conexão TCP é dita existir entre dois sockets de dois processos. A conexão é _full duplex_, no sentido que dois processos podem enviar mensagens simultaneamente pela conexão.
 Caracteristicas:
 - Reliable data transfer service:
	 A comunicação dos processos pode confiar no TCP para entregar todos os dados enviados sem qualquer perca ou erro, e na mesma ordem. Em resumo, quando um processo passa uma mensagem pelo socket ele pode contar com o protocolo TCP para que a mensagem chegue ao destino com a mesma stream de bytes que passou pelo socket, sem perdas ou dados duplicados.

### UDP CONNECTION
provê serviço de transferencia de dados não confiável. Isso significa que processos podem enviar mensagens para o socket UDP, e o UDP não dará nenhuma garantia que a mensagem enviada chegará intacta ou se sequer chegará no processo. Além do mais, mensagens podem chegar fora de ordem para o processo que o recebe.
Caracteristica:
- UDP pode transferir dado entre camadas em qualquer velocidade ele puder enviar.


## Endereçamento de processos
> [!info] How does a process indicate which process it wants to communicate
> Para identificar um processo destino, 2 peças de informações é necessária:
> 1. Endereço de IP do processo que irá receber
> 2. Uma **número de porta** que indica qual serviço rodando no destino receberá a mensagem. (quando uma nova aplicação de rede é criada, é preciso destinar um número de porta para ela)

## Protocolo HTTP
- Usa TCP como protocolo na camada de transporte. (Ao invés de rodar em cima do UDP.)
- É dito ser _stateless_ protocol.(Protocolo que não possuí estados). É importante de notar que um server HTTP envia os arquivos solicitados sem armazenar nenhuma informação "stado" do cliente.

### HTTP message format
```http
GET /somedir/page.html HTTP/1.1
Host: www.someschool.edu
Connection: close
User-agent: Mozilla/4.0
Accept-language: fr
```

- A primeira linha é chamada de **Request line**
- As linhas subsequentes são chamadas de **Header lines**
- A informação provida pela linha _host_ do header é necessária para _Web proxy Caches_. 

## Non-Persistent and Persistent Connections
> O desenvolvedor da aplicação de rede precisa fazer uma importante decisão – Deverá cada par request/response ser enviado em uma conexão TCP _diferente_, ou será que todas os pares de request/reponse serem enviados _na mesma_ conexão TCP?

### Non-Persistent
- Todo par de request/response é enviado em uma conexão TCP _diferente_. Em suma neste tipo de conexão, sempre que um objeto é enviado pelo servidor a conexão é fechada logo em seguida.
Isso pode ser prejudicial em aplicações que fazem múltiplas requisições uma vez que há um custo associado em alocar os _buffers TCP_ e outras variáveis precisam ser mantidas em ambos lados da conexão, (server e cliente).

### Persistent Connections
Com conexão persistente o servidos deixa a conexão aberta com o TCP após enviar uma resposta. Requests subsequentes entre o mesmo servidor e cliente pode ser feito em cima da mesma conexão.