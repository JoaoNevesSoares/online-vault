Tarefa Leitura 4

# Ray Tracing Denoising
## Por que Existe Ruído em cenas geradas com Ray-Tracing ?
Em termos de Ray-Tracing a iluminação global é definida recursivamente pela quantidade de raios que se propagam direta e indiretamente em um determinado ponto de uma superfície da cena. É por isso que típicamente é necessário um número muito grande de amostras (raios) para se ter uma imagem perfeita. Dado essa complexidade e o custo computacional para esse cálculo recursivo dos raios, é impráticavel ter um alto número de amostras no ray-tracing em tempo real, sendo que o normal é ter entre 1 até 3 amostras por pixel, o que de fato é uma quantidade extremamente insuficiente para ter uma cena de qualidade.

## O que é Ray-tracing Denoising e como funciona ?
O denoising é uma técnica utilizada para processar as imagens geradas usando Ray-tracing a fim de criar uma imagem mais uniforme (suave) sem aumentar "na força bruta" a quantidade de raios por pixel. Em geral, no processamento de imagens, é utilizado o conceito de **predição** que é basicamente "_adivinhar_" qual é a informação (luminicencia ou/e cor) de um pixel com base no contexto temporal ( entre frames) e espacial (no mesmo frame) e métodos sofisticados de estatística.
![[Screenshot 2023-04-15 at 13.57.45.png]]
Os denoiser do ray tracing usam técnicas de inteligencia artificial e aprendizado de máquina que são os métodos mais eficientes para fazer a predição da imagem com ruído. Em geral esses métodos utilizam Redes neurais convolucionais para "aprender" como uma imagem sem ruído deve ser por meio de grandes datasets de imagens. As gpus modernas da Nvidia possui hardware especializado para treinar essas modelos de CNN's e aplicar em tempo real o denoising enquanto a imagem está sendo renderizada. Outro ponto, é que existe métodos podem gerar quadros totalmente novos com base em Inteligencia artificial, e intercalar (temporalmente) com os quadros que estão sendo renderizado pela gpu a fim de aumentar a quantidade de amostras para a predição do ruído.
### Arquitetura típica de uma rede neural utilizada para predição de ruído de imagens com Ray-tracing
![[Screenshot 2023-04-15 at 13.49.32.png]]

# Aliasing
É o problema gerado com a discretização na renderização de um objeto contínuo para ser visualizado por um meio discreto, como o nosso monitor, que possui um número finito de pixels. 
![[anti-aliasing_image_03.png]]
# Anti-Aliasing
## SSAA 
É um das técnicas mais computacionalmente intensas de Anti-alisiang, O princípio que essa técnica usa é renderizar o objeto em uma resoluação maior que a nativa, e ele faz isso para aumentar o número de amostras na discretização do objeto, em seguida utiliza o Box filter para cálcular o valor do pixel cenrtral na imagem final, como a média dos valores do n pixels mais próximos, e por fim faz o downsampling para poder exibir na resolução nativa.
![[anti-aliasing_image_11.png.jpeg]]
## MSAA
O MSAA é uma técnica que atinge bons resultados sem um custo computacional muito alto para as gpus modernas. O principio de operação é baseado na tentativa de detecção das bordas do objeto, e o só aumentar o número de amostras nessas regiões, de modo que o contorno dos objetos não seja renderizado como valor de um único pixel, mas como a média dos valore dos pixels mais próximos, ou seja é feita uma maior amostragem nos contornos do objeto a fim de reduzir o cerrilhamento. Vale lembrar que essa técnica ela não resolve por completo o problema aliasing, e do flickering temporal. Então a principal diferença do MSAA para o SSAA é que o MSAA não renderiza uma imagem uma resolução maior do que a resolução nativa, e portanto tem um custo computacional menor.
![[Screenshot 2023-04-16 at 17.00.13.png]]