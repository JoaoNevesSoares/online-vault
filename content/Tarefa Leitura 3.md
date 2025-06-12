-- Autor: João Antonio Soares
# Tell the advantages and disadvantages of Vertex-Vertex mesh vs Face-Vertex mesh
_Vertex-to-Vertex mesh encoding_: Armazena em um buffer as informações das posições dos vértices e como eles se relacionam entre si, ao invés de armazenar o triangulo ou a faces. A vantagem desse método é que ele é muito eficiente em guardar informação de meshes, e por conseguinte possui maior throughput de dados resultando em renderização mais rápida. Adjulgo que a desvantagem seja na perca de informação relacionada na interpolação dos pontos entre os vértices dos triangulos e a releação de sentido (ou posição) das faces do triangulo.
_Vertex-to-Face mesh encoding_: Armazena tanto as informações dos vértices que formam os triangulos do objeto, quanto as faces dos triangulos. A disvantagem é que esse excesso de informação possui um custo para armazenar e para "transportar" (menor througput). A vantagem é que produz maior qualidade gráfica, uma vez que explicita melhor a topologia do objeto. (maior sharpeness).
Refêrencias:
Livro Real-Time Rendering Thomas Moller
Livro do tigre, página 262
Pesquisas no google

# Find a Wavefront OBJ file (.obj) and understand how both type of mesh encode are done on this file format
## Apenas vértices Ligado
![[suzanne_only_vertex.png]]
## Vértices e faces ligado
![[suzanne_vertex_and_surfaces.png]]
## Apenas pontos e arestas
![[suzanne_wireframe_points.png]]

Wavefron "suzanne" obtido do site: https://www.prinmath.com/csci5229/OBJ/index.html

# Filtros de Aliasing de Textura

Video de 4min falando sobre fxaa,msaa,ssaa
https://youtu.be/HX4eqeQwt2o
https://vr.arvilab.com/blog/anti-aliasing

## Explique a questão do pixel ser uma janela e não um ponto, falei disso na aula e tem uma figura disso.
O pixel é uma "janela" para um segmento do objeto e não um mapeamento de ponto 1 para 1 do objeto, porque em imagens digitais existe o processo de **discretização** do objeto do mundo real para um objeto digital, esses detalhes, eu me lembro de ter estudado no livro de Procesamento digital de imagens do Gonzalez e Woods. Outro fato é que um pixel captura mais informação do que apenas um "ponto", essas informações são coisas do tipo: cores, nível de brilho, textura,etc.
