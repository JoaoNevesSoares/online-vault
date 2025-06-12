
## 1. Descreva dois mecanismos/técnicas utilizados para reduzir o impacto no desempenho dos tempos de latência originados nos custos das comunicações realizadas durante a execução de aplicações sobre sistemas distribuidos.

Mecanismo de _Caching_ e comunicação _assíncronas_
Caching: Armazenar cópias de dados requisitados frequentemente em um local próximo ao usuário.

##  2.Apresente o resultado dos dois códigos escritos em OpenMP abaixo e caracterize suas diferenças. Considere que a execucão se dá utilizando quatro threads no núcleo de execução.

- (a) 
```c
#pragma omp parallel
for (i = 0; i < 4; i++)
	printf("i = %d\n", i);
```
i = 0 i = 1 i = 2 i = 3
i = 0 i = 1 i = 2 i = 3
i = 0 i = 1 i = 2 i = 3
i = 0 i = 1 i = 2 i = 3
Cada task executa o loop separadamente
(ordem pode variar)
- (b)
	```c
	#pragma omp parallel for
	for(i =0; i<4; i++)
		printf("i = %d\n",i);
	```
i = 0 
i = 1
i = 2
i = 3
cada task executa uma iteração do loop apenas 1 única vez

## 3. Muitas ferramentas de programação concorrente oferecem na sua API um recurso de escritas concorrentes em uma operação de redução. Descreva o funcionamento básico desta operação.
Aplicação de uma operação de redução ao resultado parcial calculado por cada tarefa em uma váriavel em redução.

## 4. Dependencias verdadeira, de saída e antidependência. Observe o laço ao lado e identifique estas dependencias.
```c
int vec[TAM], i;
for( i = 0; i < TAM-1; i++){
	aux[i] = vet[i];
	vet[i+1] = foo(aux[i]);
}
```
- A dependência _verdadeira_: um dado é lido numa iteração depois da qual foi escrito.
- A _anti_-dependência: quando um dado é lido numa iteração antes que ele seja escrito.
- Depêndencia de _Saída_: O dado é escrito e acessado na mesma iteração.

i =0 
aux[0] = vet[0]; vet[1] = aux[0]
i = 1
aux[1] = vet[1]; vet[2] = aux[1]
i = 2
aux[2] = vet[2]; vet[3] = aux[2]

`aux[0]` e `foo(aux[0])` – Dependencia de saída
`vet[1]` e `vet[i=0+1]` – Dependencia verdadeira
`vet[i]` – antidependencia

## 5. A primitiva MPI_Rsend é uma primitiva de envio de mensagem em MPI que somente pode ser postada quando a primitiva equivalente de recepção já tiver sido invocado no processo receptor. Ou seja, MPI_Rsend é uma operação não local, bloqueante e síncrona. É possível a existência de uma primitiva MPI_Irsend, não local, não bloqueante, mas ainda assim síncrona ? Explique.
Sim, é possível utilizar a função MPI_WAIT para aguardar até que o processo de comunicação tenha finalizado.

## 6. Em poucas palavras, diferencie:
### a) Arquiteturas UMA (uniform memory access) e NUMA (uniform memory access)
Uma: A memória é compartilhada em um substrato de comunicação para todos os cores com um tempo de acesso e de latência fixo.
NUMA: A memória é particionada em módulos e os tempos de acesso e de latência são diferentes para cada core de acordo com a proximidade física (passos para acessar o dado).
### b) Arquiteturas multiprocessadas e multicomputadores (ou clusters)
- Arquitetura multiprocessada: Forte acoplamento, um único espaço de endereçamento e único substrato de SO compartilhado por vários processadores. 
- Arquitetura multicomputadores: Fraco acoplamento, espaços de endereçamento distribuído e compartilhamento de dados através substrato de rede.

## 7. Preencha nos quadros "brancos", o número que identífica o modelo de implantação de sistema distribuído que se
- Grau de acoplamento entre os participantes da comunicação
	- Baixo:
	_publish/subscribe_
	_Espaço de Tuplas_
	- Alto:
	_Troca de mensagens_
	_Objetos distribuídos_
	_RMI: chamada remota de procedimentos_
- Modelos de sincronização suportados
	- Síncrono:
		_Troca de mensagens_
		_Objetos distribuídos_
		_RMI_
	- Assíncrono:
		_Publish/Subscribe_
		_Espaço de Tuplas_
		_Troca de mensagens_
## 8. indicando ao menos uma tecnologia utilizada nos seguintes modelos para implantação de sistemas distribuídos
A. Troca de Mensagens: _MPI_
B. Publish/Subscribe: _RSS_
C. Objetos Distribuídos: _RMI_
D. Espaço de Tuplas: _Linda_
E. chamada remota de Procedimentos: _RPC_


