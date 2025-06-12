# O que é Obsidian

É um editor de texto em formato [[Markdown]] e um aplicativo para gestão de sua própia base de conhecimento offiline. A forma mais básica de uso é a de criar, editar, pré-visualizar os arquivos em formato [[Markdown]]. Entretanto o poder de expressão que podemos obter utilizando o Obsidian está na capacidade de criação e manutenção de densas bases de redes de conhecimento.

#  Filosofia do Obsidian
O projeto Obsidian acredita que o cerne do conhecimento pessoal deve estar em posse do indivíduo, para tanto, o Obsidian armazena as notas criadas no dispositivo de armazenamento **local** do computador do usuário, ao invés de servidores na nuvem. Essa decisão resulta em diversas vantagens para o usuário, como: a flexibilidade de escolher o lugar onde armazenar os arquivos, fazer backup em nuvem (dropbox, gdrive, icloud), utilizar ferramentas de **versionamento** como [[git]], utilizar criptografia em disco para proteger os arquivos entre outras tantas possibilidades.


# Links e conexões

Os links e as conexões são cruciais na construção do conhecimento que possuímos, é por meio das conexões cerebrais que conseguimos solucionar problemas complexos da matemática e da física, por exemplo. No Obsidian, links e conexões são valiosos para a construção de notas e da database de conhecimento, para isso oferece como solução, entre outras coisas, a capacidade de:
- Criar Links internos
- Visualizar as conexões entre as notas através do Graph View


# Command Palette

O command palette funciona de forma a permitir acessar vários comandos a partir de um único lugar utilizando apenas o teclado. Para abrir-lo utilize o shortcut _Cmd+P_
Para navegar entre os items presentes no command Palette, utilize as setas do teclado.

## Como fixar comandos no topo do Command Palette
Existe a facilidade do usuário escolher fixar algum comando que deseje no topo do do command palette, dessa forma é possivel acessa-lo sem precisar saber o nome do comando, Para fixar um comando basta:
1. Abrir as configurações
2. Na barra lateral clique em Paleta de Comandos
3. E escolha o comando a ser salvo


# Formate suas notas

## Cabeçalhos
No Obsidian você pode ter até 6 níveis de cabeçalhos para títulos.
```md
# Titulo 1
## Titulo 2
### Titulo 3
#### Titulo 4
##### Titulo 5
###### Titulo 6


```
# Titulo 1
## Titulo 2
### Titulo 3
#### Titulo 4
##### Titulo 5
###### Titulo 6

## Ênfase
``` 
*Texto em itálico*
_Outra forma de texto em itálico_

**Texto em negrito/Bold**
_**Texto em negrito e itálico**_
```
*Texto em itálico*
_Outra forma de texto em itálico_
**Texto em negrito/Bold**
_**Texto em negrito e itálico**_

## Imagens
### Imagens de um link na internet
```
![Kurt Vonnegut](https://i.pinimg.com/originals/6f/65/43/6f65430f954679aaa1e8978011dd9a1e.jpg)

Imagem Redimensionada!
![Kurt Vonnegut | 250](https://i.pinimg.com/originals/6f/65/43/6f65430f954679aaa1e8978011dd9a1e.jpg)

```
![Kurt Vonnegut | 250](https://i.pinimg.com/originals/6f/65/43/6f65430f954679aaa1e8978011dd9a1e.jpg)

### Imagem local 
```
![[vonnegut_img.jpeg]]


```
![[vonnegut_img.jpeg]]

## Links
### Links Externos
```

[Obsidian Help Format your notes](https://help.obsidian.md/How+to/Format+your+notes)


```
[Obsidian Help Format your notes](https://help.obsidian.md/How+to/Format+your+notes)

### Links para blocos de dentro da página
Para linkar à um bloco especifico dentro de uma página utiliza-se como referencia primeiro o nome da página seguido por um  \# e a seção a ser escolhida (deve ser formatado como um título)
```
[[Obsidian#Filosofia do Obsidian]]
```
### Inserir um bloco um bloco em uma refêrencia
Para inserir um bloco de um outro lugar da página ou de outra página utilizar a seguinte sintaxe, que é semelhante de ![[Obsidian#Links para blocos de dentro da página]] com a a adição do \! na frente
```
![[Obsidian#Command Palette]]
```

## URI LINKS 
### To be constructed
Mais informações nesse link: [DOCS - URI LINKS ](https://help.obsidian.md/Advanced+topics/Using+ob[DOCS - idian+URI)

## Como reconhecer espaços em url e arquivos ?
Há duas maneiras de reconhecer url de links com espaços em branco
- Usando um caractere de escape `%20` no lugar do espaço
- Ou utilizar os símbolos `< >` em volta da palavra com espaços em brancos
```
[my note](<my note>)
```

## Como Criar uma lista de tarefas?
```
- [ ] primeira tarefa
- [ ] segunda tarefa
- [ ] etc.
```
Note que para criar a lista de tarefas, precisa escrever os colchetes com um espaço no centro, e  o botão só será exibido depois de escrever o último '\[' e dar espaço.

## Tables
### To be constructed
Mais informações no link: [TABLES](https://help.obsidian.md/How+to/Format+your+notes#Tables)

## Highlight Text
Para marcação de texto, envolva a palavra ou frase entre dois '\=\=' por exemplo:
` Essa é uma ==marcação== de texto
Essa é uma ==marcação== de texto

## Notas de rodapé
É uma funcionalidade importante para referenciar alguma coisa dentro de alguma linha de texto, sem alterar o fluxo dos pensamentos.
Notas de rodapé são escritas em [[Markdown]] e são criadas no final da página (rodapé!)
Exemplo:
lorem ipsum dum laurem doit ^[teste nota de rodapé]

## Formatação matemática
### To be constructed
Mais informações no link: [MATH](https://help.obsidian.md/How+to/Format+your+notes#Math)

## Comentários
São linhas que estão visiveis no modo editor mais não aparecem enquanto estiver no modo leitor, para adicionar texto como comentário, utilizar \%\% texto comentário \%\%

## Callouts
### To be constructed
Mais informações no link: [Callouts](https://help.obsidian.md/How+to/Use+callouts)

## Diagramas
O Obsidian possui bastante opções para a criação e manipulação de diagramas, a ferramenta utilizada para renderizar diagramas é o [Mermaid](https://mermaid.js.org/#/)
### To be constructed
Mais informações no link: [Diagrams](https://help.obsidian.md/How+to/Format+your+notes#Diagram)

## Como adicionar cores no texto
A linguagem Markdown não suporta cores nativamente, portanto para adicionar cores no texto precisamos modificar o estilo [[html]] / [[css]] da página.
```
<font style="color:blue">TEXTO PARA COLORIR AQUI</font>
```

# Aliases: Apelidos para notas
Os apelidos é uma forma simples de se referir a uma mesma nota utilizando nomes diferentes, por exemplo, em uma nota queremos nos referir pelo nome completo da nota [[Markdown]] mas em outra queremos utilizar apenas a abreviação [[Markdown|Md]].
Para cada nota que queremos apelidar é necessário adicionar um bloco de códio [[YAML]] no inicio da página. por exemplo:
``` 
---
aliases: [Md, Markup]
---
```
Neste caso a página **Markdown** terá dois apelidos: Md e Markup. Para nos referir-mos ao apelido nos links, basta escrever-lo no lugar do nome da página, e selecionar na barra de opções a nota que se encaixa o apelido.

# Editar várias linhas ao mesmo tempo

## AKA: Trabalhar com multiplos cursores
Segure <font style="color:red">⌥ Options</font> nas linhas que desejar adicionar um cursor

# Configurações
Um vault manterá seus próprios [Plugins](https://help.obsidian.md/Plugins/Core+plugins) e [custom styling](https://help.obsidian.md/How+to/Add+custom+styles). Isso é útil, por exemplo, se você tiver um vault onde mantém anotações, mas um diferente no qual você faz escrita longa.

# Plugins

## Daily Stats
**To be constructed**
