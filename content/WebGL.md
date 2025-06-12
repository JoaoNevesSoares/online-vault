
# Fundamentos

> WebGL is just a rasterization engine. It draw Points, lines and Triangles.

>[!tip] O que são Shaders
>São códigos (programas) que rodam na GPU e descrevem como os gráficos devem transformar os vértices, texturas e outras entradas em imagem no computador. São descritos em linguagem de alto nível chamada de GLSL _(OpenGL Shader Languge)_



WebGL roda em GPU, para isso é preciso providenciar código na forma de 2 funções: _vertex shader_ e _fragment shader_. 
- Papel do _vertex shader_:
Computar a posição dos vértices, e com base nas posições que essa função gera, o WebGL pode rasterizar vários tipos de primitivas, como pontos, linhas e triangulos.
- Papel do _Fragment Shader_:
Essa outra função serve para computar uma cor para cada pixel da primitiva que está sendo desenhado no momento.
---
Para cada coisa que desenhar, define um monte de estados e então executa o par de funções através da chamada dos métodos `gl.drawArrays` ou `gl.drawElements` os quais executam os seus shaders na GPU.

- Maneiras de passar dados para o shader
	1. _Atributos, Buffers, Vertex Arrays_
	**Buffers** são vetores de dados binários, geralmente contém coisas como posições, normal(alga), coordenadas de textura, cores dos vértices, etc.
	**Atributos** são utilizados para especificar como extrair dados do buffers e providenciar para o _vertex shader_.

---
# Função que cria um Retângulo
```js
function setRectangle(gl, x, y, width, height) {
  var x1 = x+;
  var x2 = x + width;
  var y1 = y;
  var y2 = y + height;
  gl.bufferData(gl.ARRAY_BUFFER, new Float32Array([
    x1, y1,
    x2, y1,
    x1, y2,
    x1, y2,
    x2, y1,
    x2, y2,
  ]), gl.STATIC_DRAW);
}
```

# Função que cria um Triângulo
```js
function setTriangle(gl, x, y,width, height) {

	var x1 = x;
  var x2 = x + width;
  var y1 = y;
  var y2 = y + height;
  gl.bufferData(gl.ARRAY_BUFFER, new Float32Array([
  	x1,y1,
    x2,y1,
    x1,y2,
  ]), gl.STATIC_DRAW);
}
```
