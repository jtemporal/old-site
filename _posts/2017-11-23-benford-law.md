---
title: A Lei de Benford e a beleza dos números
layout: post
---

Conte o número de habitantes de cada cidade brasileira. Coloque isso numa tabela e me diga, quantas vezes cada número (de 1 a 9) se repete como primeiro dígito da contagem. Tá, nós temos 5570 municípios no Brasil, contar a frequência de cada primeiro dígito vai cansar então pode chutar vai, eu deixo. Me diz qual a probabilidade de encontrar o 1 como primeiro dígito? E qual a probabilidade de encontrar o 2 como primeiro dígito?

![gif da cena de contas do filme se beber nao case](https://media.giphy.com/media/BmmfETghGOPrW/giphy.gif)
<center>
<a href="https://media.giphy.com/media/BmmfETghGOPrW/giphy.gif">
<i>Fonte</i>
</a>
</center>

E se eu te dissesse que, ao contrário do que imaginamos, a distribuição de "primeiros digitos" não é a mesma para os algarismos de 1 a 9  😱😱😱  Pelo menos não num conjunto "natural" ou de números aleatórios.

## Os primeiros dígitos num conjunto númerico
Okay, se o que a gente esperava não é verdade, então qual é a verdadeira distribuição?! Foi essa pergunta que Frank Benford ajudou a responder. 

### Frank Benford
[Benford](https://en.wikipedia.org/wiki/Frank_Benford) era um físico americano que pegou as observações iniciais de um astronomo [Simon Newcomb](https://en.wikipedia.org/wiki/Simon_Newcomb), generalizou e aplicou para vários datasets provando a existência de um padrão diferente daquele que a gente pensava ali no começo do post.

### A Lei
Também conhecida como a Lei dos Primeiros Dígitos, a Lei de Benford define que a probabilidade do primeiro dígito de um número segue uma função logaritímica que mostro abaixo:

$$P (d) =  \log_{10} \left(1 + \frac{1}{d} \right)$$

A probabilidadade do primeiro dígito de um número ser $$d$$ é dada pelo $$\log$$ na base $$10$$ de $$1 + \frac{1}{d}$$. Por exemplo se tomarmos $$ d = 1 $$ e $$ d = 9 $$ temos:

$$P (1) =  \log_{10} \left(1 + \frac{1}{1} \right) = \log_{10} \left(1+1\right) = \log_{10} 2 = 0.3010 $$

$$P (9) =  \log_{10} \left(1 + \frac{1}{9} \right) = \log_{10} \left(1+0.11\right) = \log_{10} 1.11 = 0.0453$$

Com isso sabemos que, a probabilidade de termos um $$1$$ como primeiro dígito é seis vezes maior de encontrarmos um $$9$$ como primeiro dígito. Louco né?

![gif da nazaré confusa](https://media.giphy.com/media/l44QkVjrTiBgettq8/giphy.gif)
<center>
<a href="https://media.giphy.com/media/l44QkVjrTiBgettq8/giphy.gif">
<i>Fonte</i>
</a>
</center>

### Isso é muita matemática pra mim, cadê o código?
Vamos lá! Hoje vou usar R para demonstrar com código como funciona a Lei de Benford. O objetivo dos passos a seguir é crirar um script que gere automáticamente o gráfico da análise de benford e um gráfico para a frequência de cada um dos primeiros dígitos.

#### Instalando
Comece instalando o R seguindo as instruções disponíveis [no site oficial do projeto](https://cran.r-project.org/).

Depois no seu diretório de trabalho crie um arquivo para instalar as dependencias, você pode chamar esse arquivo do que quiser, aqui vou chamar de `install_packages.R`:

~~~ r
options(repos = subset(getCRANmirrors(), Country == "Brazil")$URL)
install.packages("benford.analysis")
~~~

O `install_packages.R` se encarrega de instalar o pacote [`benford.analysis`](https://github.com/carloscinelli/benford.analysis) que traz pronto um conjunto de funções para analisar os dados contra a distribuição de Benford. Para rodar fazemos:

~~~ console
$ Rscript install_packages.R
~~~

#### Rodando o script
Depois criei um arquivo que chamei de `benfords_law.R` que vai conter os próximos blocos de código.

Começamos importando/carregando o nosso pacote escolhido e depois escolhendo um dataset de exemplo que vem com o pacote e contém o censo da População das Cidades dos Estados Unidos em  2009, veja:

~~~ r
require("benford.analysis")              # Carrega o pacote benford.analysis
data("census.2009")                      # Carrega o dataset 
~~~

A função principal desse pacote é a `benford()` é ela que faz todos os calculos em cima dos meus dados para validar os dados de acordo com a Lei de Benford. Ela irá receber um array numérico e podemos dizer quantos primeiros dígitos queremos análisar usando o argumento `number.of.digits`, o padrão para esse argumento é `2`, mas aqui vamos usar `1` por questões demonstrativas:

~~~ r
bfd <- benford(census.2009$pop.2009,     # Coluna com o censo por cidade em 2009
               number.of.digits = 1)     # Número de Primeiros Dígitos para analisar
~~~

E plotando o gráfico temos o seguinte resultado:

~~~ r
plot(bfd)
~~~

![gráficos original](https://raw.githubusercontent.com/jtemporal/talks/master/benfords-law/benford-population-us.png)
<center>
<i>Gráfico Original gerado pela função <code class="highlighter-rouge">benford()</code>.</i>
</center>

Agora, vamos reproduzir o primeiro gráfico separadamente. Esse primeiro gráfico traz alguns elementos interessantes:

- Cada barra indica a frequência observada para cada primeiro dígito dentro do dataset;
- A linha vermelha traça a frequência esperada caso aquele dataset esteja de acordo com a distribuição de Benford;

Para reproduzir esse gráfico começamos utilizando a função para plotar um gráfico de barras `barplot()`. Passamos para ela as frequências calculadas pela função `benford()` para cada primeiro dígito que se encontram em `bfd$bfd$data.dist.freq`. Os demais atributos setados são para deixar o gráfico de barras mais próximo do gráfico original.
~~~ r
barplot(bfd$bfd$data.dist.freq,          # Valores de frequencia para cada barra
        names.arg = bfd$bfd$digits,      # Legenda de cada barra no eixo x
        col = "#A1DCF0",                 # Coloração das barras
        main = "Digits Distribution",    # Título principal
        xlab = "Digits",                 # Legenda eixo x
        ylab = "Freq",                   # Legenda eixo y
        ylim = range(0:6000),            # Limite no eixo y
        xlim = range(0:10),              # Limite no eixo x
        width = .85)                     # Largura da barra
~~~

Como gráficos em R são feitos por camadas, podemos adicionar a linha vermelha usando uma outra função chamada `lines()`. Essa função acrescenta uma nova camada em cima do gráfico plotado anteriormente criando uma linha ao ligar os pontos. No gráfico original, a linha vermelha corresponde a frequência eperada quando aquele dataset conforma com a distribuição de Benford, vejamos:

~~~ r
lines(x = bfd$bfd$benford.dist.freq,     # Pontos para formar a linha
      col = "red",                       # Cor da linha
      lwd=2.5,                           # Espessura da linha
      type="c")                          # Tipo da linha: tracejado
~~~

![frequência de cada dígito num gráfico de barras](https://raw.githubusercontent.com/jtemporal/talks/master/benfords-law/digits-distribution-population-us.png)
<center>
<i>Gráfico de barras gerado utilizando <code class="highlighter-rouge">barplot()</code>.</i>
</center>

Nota com a linha vermelha quase sobrepõe o topo das barras de frequência?!

## Benford pra quê?





## Links
- http://gigamatematica.blogspot.com.br/2011/07/lei-de-benford.html
- https://www.r-bloggers.com/benfords-law-graphed-in-r/
- http://www.businessinsider.com/benfords-law-to-detect-financial-fraud-2014-12
- github com codigo

![bla](https://media.giphy.com/media/d6WWh3Em7kWHu/giphy.gif)
