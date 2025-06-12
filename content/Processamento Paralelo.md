[[OpenMP]]
- Memória Transacional
permitir compartilhamento de memória em programação concorrente.


# Flyn's Classification (taxonomy)
> Classificação quanto aos fluxos

- SISD – _Single Instruction Multiple Data_
Arquiteturas monoprocessadores são típicamente arquietura Von Neumann.
- MIMD – _Multiple Instruction Multiple Data_
Arquiteturas Multiprocessadores – Os diferentes processadores(_cores_) manipulam diferentes conjuntos de dados.
- SIMD – _Single Instruction Multiple Data_
Arquiteturas Vetorial – típicamente de Asics e de Gpus
- MISD
Arquiteturas com Pipeline

# ACOPLAMENTO
> Classificação quanto a Estrutura.

## Fracamente Acoplado
- MultiComputadores
Espaço de endereçamento distribuído e diferentes instâncias do sistema operacional.

## Fortemente Acoplado
- Multiprocessadores
Uma única instância do sistema operacional gere todos os recursos da arquiteura e um espaço de endereçamento compartilhado por todos o substrato de comunicação.

# MIMD – Multiprocessador – Subclasses
## UMA 
- _Uniform Memory Alocation_
Tempo de latência de acesso a memória é fixo para todos os processadores.
## NUMA
- _Non Uniform Memory Alocation_
Espaço de endereçamento contiguo porém com tempo de acesso variável dependendo da proximidade do processador com o módulo de memória.
## COMA
- _Cache Only Memory Acess_

## UMA VS NUMA, QUAL A MELHOR ? QUAL AS VANTAGENS ?

# MIMD - Multicomputador - Subclasses

## NORMA
- _Non Remote Memory Acess_
- Arquitetura de Clusters
Não existe nenhum compartilhamento de memória ou espaço de endereçamento. Eles trocam informações através de uma rede por mensagens.


# GRANULARIDADE

> Indica a carga de trabalho que está descrevendo na unidade de paralelismo

_Menor_ a carga de processamento, _menor_ a granularidade. + paralelismo + overhead de gerir o paralelismo.

_Maior_ a carga de processamento, _maior_ a granularidade. - paralelismo - overhead de gerir o paralelismo.

## Ao nível de instrução
Granularidade fina (muito overhead para ser tratado em nível de aplicação) dessa forma é implementado soluções diretamente em Hardware.
- Pipeline
- Vetorial
- superescalar
- execução especulativa
## Ao nível de fluxo de execução

## Ao nível de processo
- Clusters
- Constelações

## Ao nível de Aplicação
- Computação em rede
- Cloud Computing

# Ferramentas de Programação

## Multiprocessadores
- Pthreads
- OpenMP
- C++
- TBB
- Java
- Rust
## Multicomputadores
RPC
RMI (Java)
MPI (troca de mensagens)

## Núvem
> [!itp] Importante
- Modelo **MapReduce**
> Permite Aplicar a operação **Map** sobre um conjunto de dados de uma grande base de dados, e sobre o resultado dessa operação realiza então uma operação de redução dessa informação, que na verdade uma operação que compõe resultados parciais em um resultado único final. O resultado final da operação de MapReduce é um conjunto de arquivos de saída que reproduzem uma informação retirada dessa grande base de dados.




[[Topicos Prova 1]]