# MetodoExaustao

O método da exaustão foi desenvolvido nos tempos de Eudoxo e Arquimedes. Este post visa mostrar a ideia geral do método. Os gregos antigos tinham uma noção bastante forte de geometria, e por isso, é bastante lúdico entender o raciocínio.

Como calcular a área de um círculo, ou de alguma outra forma complicada? Uma resposta é aproximar por algo mais simples, como um triângulo ou um quadrado.

![](https://ideiasesquecidas.files.wordpress.com/2020/05/exaustao01.jpg)

O maior quadrado possível que cabe dentro de um círculo é o quadrado inscrito.

O menor quadrado possível em que o círculo cabe dentro é o quadrado circunscrito.

Assumindo que o raio é igual a 1, para facilitar, a área do círculo vai estar entre 2 e 3,31 (demonstração nos capítulos seguintes abaixo).

Mas o quadrado é muito diferente do círculo. Não dá para melhorar?

Que tal utilizar um pentágono?
![](https://ideiasesquecidas.files.wordpress.com/2020/05/exaustao02.jpg)

A aproximação melhorou um pouco, entre 2,38 e 3,25 (hoje sabemos que a área é pi*r^2, se o raio é 1, a área é pi = 3.1415…)

Podemos continuar crescendo o número de lados do polígono.

Digamos, 6 lados (hexágono):

![](https://ideiasesquecidas.files.wordpress.com/2020/05/exaustao03.jpg)

10 lados:
![](https://ideiasesquecidas.files.wordpress.com/2020/05/exaustao04.jpg)

15 lados:
![](https://ideiasesquecidas.files.wordpress.com/2020/05/exaustao05.jpg)

Quanto maior o número de lados, o polígono regular é mais parecido com o círculo.

Repetindo o procedimento, até a exaustão (daí o nome), podemos chegar ao valor de pi com a precisão desejada.

Os gregos utilizaram técnica semelhante para calcular área de diversas outras formas, e também o volume de esferas e outros sólidos.

O método acima tem pouca álgebra e muita geometria e é uma espécie de precursor do cálculo integral.

Mexa na versão web em https://asgunzi.github.io/MetodoExaustao/index.html

É possível utilizar o Excel para traçar os polígonos acima, embora seja um pouco mais avançado (utilizando VBA).

O desenho utiliza apenas retas e círculos, o que facilita bastante.
![](https://ideiasesquecidas.files.wordpress.com/2020/05/exaustao06.png)

Em essência, para adicionar uma linha, só é necessário saber as coordenadas iniciais (x1,y1) e finais (x2,y2).

ActiveSheet.Shapes.AddLine(x1, y1, x2, y2)

O número de lados N do polígono regular vai dividir o círculo em N, mostrado acima como bolinhas amarelas.

Se uma volta completa é igual a 360 graus (2*pi), o ângulo theta entre dois pontos é de 2*pi/N.

As coordenadas do ponto i são (r*cos(theta_i), r*sin(theta_i)), com theta_i = i*2*pi/N.

O código final envolve vários outros detalhes, porém, a essência está descrita acima.

For i = 1 To nlados

    theta = 2 * i * pi / nlados + theta0

    x1 = cx0 + raio * Math.Sin(theta)

    y1 = cy0 + raio * Math.Cos(theta)

theta = 2 * (i + 1) * pi / nlados + theta0

    x2 = cx0 + raio * Math.Sin(theta)

    y2 = cy0 + raio * Math.Cos(theta)

    plotaLinha "FrmRef", x1, y1, x2, y2, r, g, b

Next i

Para calcular a área, utilizar geometria novamente.

Se o lado do polígono é igual a x, e a altura do triângulo h, temos um triângulo retângulo h – x/2 – r.

Lembrando que o raio do círculo é conhecido.

![](https://ideiasesquecidas.files.wordpress.com/2020/05/exaustao07.png)

O ângulo é theta = 360 / N.

Fazendo as contas, a área do polígono inscrito é N/2 * sin(2*pi/N).

A área do polígono circunscrito é 2*N*tan(pi/(2*N)).

Há um erro lógico aqui no exercício. Utilizei o conhecimento moderno de trigonometria para calcular a área – e tal conhecimento utiliza explicitamente o pi, que era justamente o que Eudoxo e Arquimedes queriam descobrir. Porém, para efeito de ilustração, imagino que seja suficiente.

Versão web em https://asgunzi.github.io/MetodoExaustao/index.html

Para baixar o arquivo Excel e o código-fonte em Javascript:

https://github.com/asgunzi/MetodoExaustao

Vide também:

https://ideiasesquecidas.com/laboratorio-de-matematica/
