---
title: A Lei de Benford e a beleza dos números
layout: post
---

Conte o número de habitantes de cada cidade brasileira. Coloque isso numa tabela e me diga, quantas vezes cada número (de 1 a 9) se repete como primeiro dígito da contagem. Tá, nós temos 5570 municípios no Brasil, contar a frequência de cada primeiro dígito vai cansar então pode chutar vai, eu deixo. Me diz qual a probabilidade de encontrar o 1 como primeiro dígito? E qual a probabilidade de encontrar o 2 como primeiro dígito?

![se beber nao case gif das contas](https://media.giphy.com/media/BmmfETghGOPrW/giphy.gif)
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

$$P (d) =  \frac{1}{n^{2}} $$

## A Lei

### Cadê o Python?


### Exemplo

- http://gigamatematica.blogspot.com.br/2011/07/lei-de-benford.html
- https://www.r-bloggers.com/benfords-law-graphed-in-r/
- http://www.businessinsider.com/benfords-law-to-detect-financial-fraud-2014-12
- github com codigo
