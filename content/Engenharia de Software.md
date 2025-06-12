[[E.S Etapa 1 - Sistema de Submissão Propostas TCC]]
[[Trabalho de Modelagem]]
[[Revisao Prova]]

# Princípios da Engenharia de Software
## KEEP IT SIMPLE, STUPID (KISS)
De acordo com o _Routledge Dictionary of Modern American Slang and Unconventional English_ esse termo foi originado na U.S navy na década 60. O engenheiro Kelly Johnson então funcionário da _Lockheed_ a época, foi conhecido por ser um dos primeiros a colocar em prática este princípio em conjunto de sua equipe de projetistas do jato _Lockheed U-2_. A ideia era, apesar de que os engenheiros possuíssem as ferramentas mais sofisticadas e complexas afim de projetar o jato, a construção do mesmo deveria ser simples o suficiente de forma que um mecânico mediano pudesse realizar consertos em campo de batalha com as ferramentas mais triviais. Ao traduzir esse princípio para a realidade do desenvolvimento de software, devemos sempre optar por manter as soluções o mais simples possível. Em geral, na matemática e na computação soluções mais enxutas são as mais elegantes.


# Revisão toda matéria prova 1

# Indice
1. [[#Introdução à Engenharia de Software]]
	1. [[#Conceito de Software]]
	2. [[#O que é Engenharia de Software]]
	3. [[#Quais são as principais atividades da engenharia de software]]
	4. [[#Tipos de Software]]
	5. [[#Problemas da E.S]]
	6. [[#Engenharia de Software na Prática]]
	7. [[#Princípios gerais]]
	8. [[#Lições ou Boas Práticas]]
2. [[#Ciclo de vida do Software]]
	1. [[#Ciclo de Vida]]
	2. [[#Produção de Software]]
	3. [[#Definição]]
	4. [[#Desenvolvimento]]
	5. [[#Manutenção]]
3. 



# Introdução à Engenharia de Software

## Conceito de Software
- É um produto que profissionais de software desenvolvem e ao qual dão suporte no longo pazo.
- Software é desenvolvido e não fabricado.

## O que é Engenharia de Software
- É uma profissão dedicada a _projetar_, _implementar_ e _modificar_ software, de forma que ele seja de alta qualidade, tenha um custo razoavel, seja manutenível e rápido de construir

## Quais são as principais atividades da engenharia de software
- analisar
- especificar
- projetar
- programar (implementar)
- validar
- manutenir
- gerenciar
## Tipos de Software
- Classificação:
	- Genéricos: (Prateleira): Funcionalidades que atendam _múltiplos usuários_
	- Customizados (Encomenda): Desenvolvido para uma demanda específica
- TIpos de Software:
	- Software _Básico_: (Compiladores, drivers, Componentes do SO)
	- Software _Tempo-Real_
	- Software _Comercial_
	- Software _Científico_
> Cada tipo de software exigem um processo. de desenvolvimento diferenciado!

## Problemas da E.S
- Aspectos críticos da Engenharia de Software
	- Requisitos
	- Prazos
	- Custos
Causas dos problemas:
- Não Dedicar tempo para coletar dados históricos sobre o desenvolvimento
- Comunicação pouco produtíva entre o cliente e desenvolvedor
- Falta de testes
- falta de maturidade dos profissionais e das técnicas utilizadas
- Não utiliza técnicas de engenharia no desenvolvimento
- Falta de investimento em Engenharia de Software

## Engenharia de Software na Prática
- Compreender o problema (Comunicação e análise)
- Planejar uma solução (Modelagem e projeto de software)
- Implementação (gerar código)
- Examinar o resultado (Testes e garantia de qualidade)

## Princípios gerais

Razão de existir
KISS
Mantenha a visão
Esteja aberto para o futuro
planeje com antecedência, visando a reutilização
pense

## Lições ou Boas Práticas
- **Decompoisção**: Construir o software apartir de partes menores
- **Abstração**: Compreender as estruturas grandes e complexas apartir da abstração de detalhes.
- **Generalização:** produzir soluções genéricas que possibilitem o reuso de componentes.
	- Princípio básico da O.O: Um objeto pode ser classificado em mais de uma classe
- **Flexibilização**: Permitir atualizações e modificações com facilidade.
- **Padronização**: A criação de padrões de programação, de projeot e análise ajudam a elaborar produtos com qualidade previsível
- **Formalidade**: Utilizar de especificações formais.
- **Desenvolimento iterativo**: Desenvolver o software em vários ciclos. Cada ciclo contribui para a finalização do produto.

## Refêrencias

# Ciclo de vida do Software

## Ciclo de Vida
- O software tem um ciclo de vida
	1. É concebido
	2. É desenvolvido
	3. Entra em operação
	4. É retirado de operação

## Produção de Software
Uma abordagem global exige: _definição_,_desenvolvimento_, _manutenção_.

## Definição
### Análise de requisitos

>[!info] Objetivos
>Identificar quais funções são requiridas pelo sistema e as restriçÕes sobre a operação do sistema e seu desenvolvimento.
>Identificação, descrição e validação dos requisitos.

- Especificação da _função_ e _desempennho_ do software
- Indicação da _interface_ com outros elementos do sistema
- Estabelece _restrições_ que o software vai enfrentar
#### Envolve
1. Descoberta
2. Refinamento
3. Modelagem
4. Especificação

### Definição do Projeto
Define:
- Arquitetura
- Interface
- Componentes
- Estruturas de Dados
- Algoritmos

#### Modelo projeto
- ***Orientados a Objetos (UML)**

## Desenvolvimento

- Implementação / Programação
- Teste de Software
	- Validação: _Estamos construindo o produto certo_
	- Verificação: _Estamos construindo certo o produto?_
- Instalação

## Manutenção
### Evolução do Sistema


# Processo de Software
> Um projeto representa a execução de um **processo**
> Processo é um conjunto de atividades, ações e tarefas realizadas para a criação de um produto.

- É documentado
- subdivisões terminadas por _marcos_.

## Atividades Essenciais no Ciclo de vida de Software
- Comunicação (levantamento de necessidades)
- Planejamento (cronograma)
- Modelagem (análise de projeto)
- Construção (programação, testes)
- Entrega (suporte)
## Modelo de Processo

- Modelos definem um _fluxo de processo_. A ordem que as [[#Atividades Essenciais]] devem ser realizadas.
### Tipos de Fluxos

#### Fluxo Linear (Sequencial)
>Uma atividade só pode ser realizada após a anterior ser concluída.
- Modelo que utiliza: Modelo Cascata
#### Fluxo Paralelo


#### Fluxo Evolucionário
Cada "volta" conduz a uma versão masi evoluída ou completa do software

#### Fluxo Iterativo
> Pode repetir etapas anteriores antes de passar para próxima etapa.

## Modelo Cascata

- Implementa **Fluxo Sequencial**
- Dirigido por Documentação
### Caracteristicas
- Fases Bem definidas
- Promove a estabilidade dos requisitos

### Atividades no Modelo Cascata Original
1. Análise de Requisitos
2. Modelagem
3. Implementação / Codificação
4. Testes
5. Operação


### Vantagem:
- _Abordagem Estruturada_: Ajuda a garantir que o processo de desenvolvimento siga uma ordem lógica e que cada fase seja concluída para prosseguir para a próxima fase.
- _Requisitos claros e Estáveis_: Funciona bem para requisitos estáveis, pois eles são documentados na fase inicial e usados em todo o restante do processo de desenvolvimento.
- _Documentação detalhada_: Exige que a cada etapa seja documentada de forma detalhada. pode ser benéfico para 
### Desvantagens:
- Não possui flexibilidade com requisitos: É muito trabalhoso voltar atrás para corrigir requisitos mal estabelecidos.
- Testes só ocorre somente ao final do processo.
- Dificuldade de acomodação de mudanças ( de requisitos, de critérios de qualidade,etc)
- Não é viável para projetos com riscos pois é difícil de identificar, avaliar e mitigar os riscos do projeto, uma vez que os problemas podem surgir em fases posteriores e resultar em custos adicionais e atrasos no cronograma. 

### Questões de Reflexão sobre o modelo Cascata

1. Quais são as vantagens e desvantagens do modelo de processo cascata em comparação com outras abordagens de desenvolvimento de software?

O modelo cascata possui algumas vantagens, tais como sua facilidade de implementação em _projetos com requisitos estáveis ou previsíveis e com equipes pequenas ou inexperientes_. Outra vantagem é a estruturação do projeto baseada em documentação, que auxilia no desenvolvimento das etapas finais. Porém, algumas desvantagens do modelo cascata incluem sua _falta de flexibilidade_ em relação a mudanças nos requisitos do projeto e _a necessidade de ter uma visão completa e precisa do projeto desde o início_, o que pode ser difícil em projetos grandes e complexos.

2. Em que tipo de projetos o modelo de processo cascata é mais adequado? Em que tipo de projetos o modelo de processo cascata pode ser menos adequado?

O modelo cascata é mais adequado para projetos pequenos e com requisitos estáveis. Em contrapartida, ele pode ser menos adequado para projetos grandes que necessitam de mudanças constantes nos requisitos técnicos e de qualidade, pois o modelo cascata não possui muita flexibilidade para lidar com mudanças durante o processo de desenvolvimento.

3. Como o modelo de processo cascata pode ser adaptado para lidar com requisitos em constante mudança ou para lidar com situações em que é necessário ajustar o processo de desenvolvimento à medida que o projeto avança?

Para lidar com requisitos em constante mudança, o modelo cascata pode ser adaptado _adicionando iterações_ em que, ao finalizar uma etapa, é possível voltar a ela futuramente para ajustar detalhes nos levantamentos de requisitos, sem necessitar que todo o trabalho seja feito novamente. Além disso, o modelo pode ser adaptado para lidar com situações em que _é necessário ajustar o processo de desenvolvimento à medida que o projeto avança_, _criando iterações adicionais para acomodar as mudanças_.

4.  Quais são as principais fases do modelo de processo cascata e quais são as atividades e entregáveis ​​associados a cada fase?

As principais fases do modelo de processo cascata são as seguintes:

	1.  Fase de Comunicação: nesta fase, a equipe de desenvolvimento se comunica com o cliente para entender os requisitos e especificações do projeto. O resultado desta fase é uma documentação que descreve os requisitos técnicos e de qualidade.
	2.  Fase de Modelagem: nesta fase, a equipe de desenvolvimento descreve os requisitos em alto nível de abstração e modela-os em uma linguagem que possa ser facilmente convertida em código na fase de implementação. O resultado desta fase é uma documentação que descreve a modelagem do software que será desenvolvido em conformidade com as especificações definidas na fase de comunicação.
	3.  Fase de Implementação: nesta fase, a equipe de desenvolvimento codifica a solução proposta com base nas especificações definidas na fase anterior. O resultado desta fase é um modelo funcional do projeto que pode ser testado na fase seguinte.
	4.  Fase de Testes: nesta fase, a equipe de desenvolvimento realiza testes para garantir que o software esteja funcionando corretamente e atendendo aos requisitos definidos na fase anterior. Os testes incluem testes de funcionalidade e qualidade, e o resultado desta fase é um software que funciona e uma documentação de utilização/configuração.
	5.  Fase de Operação: nesta fase, a equipe de desenvolvimento instala e configura o software no ambiente de trabalho do cliente e oferece suporte aos usuários finais do sistema.
1. Quais são as habilidades e competências necessárias para gerenciar um projeto usando o modelo de processo cascata com sucesso?
-   **Boa comunicação**: uma comunicação eficaz com o cliente e a equipe de desenvolvimento é fundamental para entender e definir os requisitos do projeto e garantir que o projeto esteja seguindo o cronograma e as expectativas.
-   **Habilidade de planejamento**: ter uma visão clara dos prazos e cronogramas para cada etapa do projeto. Conhecimentos em engenharia de software, modelagem e programação 
Possuir uma boa comunicação entre a equipe de desenvolvimento e o cliente. Possuir uma boa visão de prazos e cronograma para cada etapa do modelo de cascata, saber o que esperar da equipe de desenvolvimento a termino de etapa.


## Modelo prototipação

> Baseado na idéia de criar protótipos para entender melhor requisitos e reduzir os riscos. 
- A especificação pode ser desenvolvida _gradativamente_ a medida que os usuários conseguem compreender melhor suas necessidades.
### Duas Abordagens
- Throw-away (descatável)
> Útil para definir melhor os requisitos do sistema. 
> _Como?_ – Fazer experimentos para compreender melhor os requisitos.
	- Especificação do sistema é derivada do protótipo
	- Alguns componentes dos protótipos podem ser reusados na versão final de produção.
- CornerStone (Evolucionária)
É realizada uma implementação inicial (um protótipo) e a partir dele e com base nos comentários e sugestões dos usuários é desenvolvido as funcionalidades do sistema até que se o obtenha o sistema final.
- Emprega a ideia de ir refinando e melhorando o protótipo com base nas sugestões dos usuários.
### Desvantagem Prototipação Evolucionária
- Falta de Planejamento, é difícil de prever o tempo e o progresso uma vez que os requisitos são flexiveis.
- Necessita de uma boa ou ótima comunicação entre as partes que estão desenvolvendo o sistema com o gerente e com os clientes.
- Dificuldade de gerar documentação estruturada, pois mudanças costantes são difíceis de prever e ocorrem o tempo todo.
- Qualidade: Implementações rápidas e de curto prazo que Não visam a estabilidade ao longo prazo e a manutenção futura.

### Aplicação da Prototipação Evolucionária
- Sistemas _pequenos_ e com vida útil curta.
- Partes de sistemas interativos grandes (interface com usuário), mais fácil entender o uso do usuário e prototipar para que este possa testar.

## Modelo Espiral

**PALAVRA CHAVE**: _ANÁLISE DE RISCOS_ 

- Segue a abordagem de _passos sistemáticos_ do cascata, mas utiliza estrutura _iterativa (ciclos)_.
- Prototipação em qualquer etapa da evolucação do produto. (Reduzir Riscos)

### Vantagens:
- Reduz os Riscos
- Construção de protótipos para entender a especificação
- Mantém o enfoque sistemático do ciclo clássico (Documentação e segurança).

### Desvantagens:
- Boa capacidade de Análise de Riscos
- Dificuldadde para prever cronogramas e tempo de ciclos.
- Maior complexidade em relação com outros modelos, necessita de equipe experiente.

## Modelo em Estágios

Combinação do **Modelo Cascata** com a _iteração_ da **prototipação evolucionária**.

Etapas Sequenciais: _concepção, análise de requisitos, projeto arquitetural_.
Etapas Iterativas: _projeto detalhado, codificação, teste, entrega do incremento_.
> - A cada sequência linear é produzido uma versão do produto.
> - Evita problemas de mudança constante presente na prototipação evolucionária.

### Vantagens
- Entrega de forma contínua, aliviando cronograma
- Menor risco de fracasso
- Base para processos iterativos, (Métodos Ágeis)
- Fornecer partes úteis do sistema ao cliente antes de completar o projeto.

### Desvantagens
- Incrementos devem ser pequenos.
- Dificuldade para identificar facilidades comuns que vários incrementos exijam. (requisitos não são definidos até que o incremento seja concluído.)


# Engenharia de Requisitos

## Etapas
- Concepção
- Levantamento
- Elaboração
- Negociação
- Especificação
- Validação
- Gestão

## Requisitos:

### Requisitos Funcionais

- Funcionalidades que o software deve prover ou ser capaz de realizar

### Requisitos Não funcionais
- Propriedades do Produto
- Ser Multi-plataforma, abranger diversos dispositivos, performance, eficiência energética, confiabilidade escalabilidade

**Requisitos não funcionais**: podem ser mais críticos do que os requisitos funcionais. Se estes não forem atendidos **o sistema é inútil**.

#### Tipos:
Requisitos de produto: Referente a uma propriedadae do Produto
Requisitos Organizacionais: processo de desenovlvimento e os documentos devem estar em conformidade com padrão _XYZ_.
Requisitos Externos: Privacidade dos dados, éticos, interoperabilidade.

## Diagrama Casos de Uso
- Modela a interação entre o produto de software e os seus usuários (Representado por _atores_).
Para se escrever um caso de uso deve:
- Identificar e definir os _Atores_.
- Identificar funcionalidades no Software

# Diagramas de Atividade


