
[[Exercicios]]
[[Exercicios 2]]
# Classificação de Flynn
# Classificação Estrutura
## Acoplamento
## UMA
## NUMA
## NORMA
# Granularidade
## Nível Instrução
## Nível Fluxo de execução
### SMT
### multiprocessador
## Nível Processo
### Clusters
### Constelações
### MPP
### GRID
# Inter Process Communication
## Pipes
## Troca de Mensagem
## Memória Compartilhada

# Multiprocessadores x MultiComputadores (aula5-pdf)
# Computação em Nuvem
## Modelo MapReduce
# TASK VS THREADS
# Modelo PARBEGIN/PAREND
# Modelo FORK/JOIN
# Mutex vs Monitor
# SpinLock
# Thread-aware
# OPenMP
## OpenMP vs Pthreads
## Variáveis de Ambiente
## Serviço de Biblioteca
## Corpo de Tarefas
## Modelo de memória
## Parametro as tarefas
## Worksharing
## Escalonando algoritmos recursivos
# Sistemas Distribuídos em Camadas
# Sistemas Distribuídos em Objetos
# Sistemas distribuídos sem Recursos
# Sistemas distribuídos Publish/Subscribe
# Wrappers e Brokers
# Modelos de Arquitetura Distribuídas
## Troca de Mensagens
## RPC – Chamada remota de procedimentos
## Objetos Distribuídos 
## Publish/Subscrive
## Espaço de Tuplas
# RPC
# RMI
# MPI
---
# Prova do Kevin
1. Mecanismos/Técnicas Sistemas distribuídos.
2. diretivas: `#pragma omp parallel` e `#pragma omp parallel for`
3. Api, recurso de escritas concorrentes em operação de redução. Descreva funcionamento básico.
4. laços: dependencia verdadeira, dependencia de saída, antidependencia.
5. Diretivas MPI
6. 
	1. Arquitetura UMA - NUMA Diferencie
		```
		UMA 
		- possuí uma memória acessível para todos os cores da máquina com tempos de acesso uniforme.
		NUMA
		- possuí vários módulos de memória acessível para todos os cores com tempos de acesso não uniforme, (depende da distância).
		``` 
	1. Multiprocessada x multicomputadores
		```
		Multiprocessador
			- espaço de endereçamento único e dados são compartilhados no mesmo substrato de comunicação.
		Multicomputador
			- espaço de endereçamento distribuído e dados são compartilhado por um substrato de rede.
		```
7. Modelos de Arquitetura Distribuída: Grau de acoplamento - Modelo de Sincronização suportado
8. Identificar o Modelo de Arquitetura de sistemas distribuídos.


# Outras questões

Modelo _Map Reduce_:
Aplica a operação map sob subconjuntos de dados modificando-os e em seguida aplicação a operação reduce que combina resultados parciais em um resultado único.
