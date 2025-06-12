-- João Antonio Soares
# What is G0, G1, G2 and G3 continuity
São continuidades _geométricas_. Uma curva diz possuir Gn continuidade se existir alguma maneira de parametrizar a curva de forma que possua continuidade Cn. Em geral uma curva é Cn contínua, se todas as suas derivadas até n, coincidirem entre as partes.
Desse modo a continuidade G0 pode ser representada por "toque" no mesmo ponto u\_j por duas curvas de modo que satisfaça: P\_{j-1}(u\_j) = P\_j(uj). A continuidade G1 é satisfeita se as duas derivadas de primeira ordem (_unit tangent_) são colineares. As continuidades G2 e G3 extende a mesma ideia, porém envolvendo as derivas de ordem mais alta. 
# How to connect two curves?
Uma das maneiras que podemos conectar duas curvas de bézier é garantindo que elas possuam continuidade G1 em um ponto P em comum. Isso é: a tangente no ponto final da primeira que coincide com P e  o ponto inicial da segunda curva que também coincide com P, devem possuir tangentes paralelas a curva e serem colineares.
# How to have linear velocity over a curve ?
Se eu bem entendi a pergunta. Em termos matemático, para saber a velocidade linear em um dado ponto de uma curva paramétrica, calcula-se as derivadas dx/dt e dy/dt e obtem-se a tangente ao ponto em questão. A partir disso é possível descobrir a velocidade que um objeto percorre sobre a curva em um instante de tempo _t_ utilizando o teorema de pitágoras em cima do cálculo das derivadas anteriores. Claro, existem diversas maneiras diferentes de calcular esse resultado, uma das maneiras que o livro apresenta é utilizando o ferramental do cálculo vetorial e equações diferênciais. Outro ponto intuitivo que acho estar relacionado é que quanto menos "brusca" é a diferença de velocidade entre dois pontos continuos em uma curva, maior é o grau de G_n de continuidade e por conseguinte mais suave é a transição entre as partes.

Referências: 
- Livro do tigre página 347
- Livro do cacto página 453
- Livro do 3d math primer página 701
# Find a way to know that a low resolution mesh can be used, because no one will see the difference to a high resolution one.
Para esse propósito é utilizado o princípio _level of detail (LOD)_,que é basicamente simplificar a quantidade de detalhes usados para renderizar os objetos pequenos ou distantes na cena. O LOD tradicional é feito, de modo que para cada objeto, é criado um conjunto de objetos com níveis de detalhes diferentes, e durante a execução da aplicação gráfica, é escolhido um dos Lod's do objeto de acordo com a distância ou outro critério semelhante. 
As operações matemáticas envolvidas na implementação de Lod's incluem: Simplificação geométrica dos _meshes_ do objeto, a partir de duas operações: Redução do número de: vértices, arestas, e triângulos; Simplificação da topologia: Reduzir o número de cavidades, buracos, e túneis nos modelos. Uma técnica que achei interessante para processar os Lod's é a _Variable-preicison transformation_ que reduz a precisão dos valores númericos das primitivas geométricas(vértices, pontos) dos modelos. A ideia aqui é que com precisão menor, aumenta a velocidade de computação da renderização dos modelos sem uma perda tão relevante de qualidade visual. Operações envolvendo _f64_ possui maior overhead de computação.
![[variable_precision.png]]

Essas operações descritas acima são frequentemente aplicada em jogos digitais através da técnica de filtro de texturas _Mip-Mapping_: que utiliza um piramide de qualidade da imagem, onde cada nível da piramide é um downsampling da média das imagens no nível superior. De acordo com a distância do objeto em relação a câmera na cena, é escolhido um nível apropriado da pirâmide para escolher a versão da textura a ser exibida na tela.

Refêrencias: 
- Varshney_GeneratingLOD - Slides LOD 2003
- Livro: Level of detail for 3d graphics - página 339

# What i ssubdivision surfaces ?
É uma técnica algorítmica que permite criar superfícies complexas a partir de formas mais simples, como um retângulo. Resumidamente, o algorítmo funciona em dois passos, o primeiro: chamado split, funciona adicionando pontos intermediários na linha da forma original, resultando em novos vértices e superfícies, O segundo passo é chamado de _average step_, onde cada ponto é redimensionado para a métade do caminho do ponto anterior, executando esses 2 passos recursivamente diversas vezes torna a forma mais fina (_smooth_). O legal dessa técnica é que permite animar toda as formas utilizando os pontos originais utilizados como pontos de controle. 
Refêrencia: 
- https://www.khanacademy.org/computing/pixar/modeling-character/modeling-subdivision/v/cm-start
- https://en.wikipedia.org/wiki/Subdivision_surface
