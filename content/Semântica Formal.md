

# AULA 2 – 9/02

## Tipos de Semântica Formal

1. Semântica Operacional
	- Se preocupa com todso os aspectos da execução de um programa.
	- define um interpretador para a linguagem
	-  Existem dois tipos:
		-  BIG-STEP (Semântica natural)
		- SMALL-STEP (Semântica estrutural)
2. Semântica axiomática: não se preocupa com todos os aspectos da execução.
	- Se preocupa em mostrar que propriedades a respeito dos programas são respeitadas
3. Semântica denotacional
	- Explica o significado dos programas em termos de objetos matemáticos
		- Objetos matemáticos: funções, conjuntos e composição de funções.

## Árvore Sintática Concreta
São árvores que contém não terminais, entretanto podemos construir uma versão optimizada da árvore Concreta que é chamada de árvore sintática abstrata, em que os nós contém apenas operações e as folhas são os terminais.

## Semântica Operacional BIG-STEP
Linguagem que será utilizada: L.Simples de Expressões Aritméticas
E = M | E+ E | E \* E
M pertence "N"
1 
3+4
3 + 4 \* 5 + 6 \* 19
---
- Semântica operacional define um interpretador
- Na semântica operacional definidos uma máquina abstrata onde as construções da linguagem são as instruções e a semântica explica como executar essas instruções.
- A semântica é uma função que recebe como entrada expressão e devolve na saída o resultado de computar essa expressão.
- Usamos o símbolo \\||/ (seta para baixo) para indicar a semântica big-step.
- A semântica operacional é dada por um conjunto de  regras (parecidas comas regras da lógica proposiocional):
p_1 p_1 p_3 ...
- Se todas as permissões são verdadeiras, podemos derivar as conclusão.
- na semântica BIG-STEP temos pelo menos uma regra para cada categoria sintática.


