---
title: "Projetos Jekyll com Docker"
layout: post
date: '2018-01-14 08:00:00'
tags:
- tutorial
- jekyll
- ruby
- docker
- docker-compose
- site
- português
comments: true
---

Uma curiosidade crescente hoje em dia é o uso de [Docker]() em projetos. Depois que troquei de máquina por causa do trabalho decidi que ia tentar manter tudo que eu pudesse usando Docker e [Docker Compose](). Principalmente pois na empresa nova o uso de Docker é intenso e para usar bem uma ferramenta o primeiro passo é começar a usar.

Acredito que é possível encontrar imagens Docker no [DockerHub]() para quase tudo, inclusive para o [Jekyll](). Então se tiver interesse de aprender a rodar os projetos Jekyll com Docker, continue lendo ;)

## Docker e Docker compose, onde vivem, do que se alimentam?

Se você não conhece nenhuma dessas ferramentas ou se já ouviu falar, mas nunca usou com propriedade, a minha dica é: Não é trivial, mas da pra aprender. Então coloque a síndrome do impostor de lado e brique com elas. Não vou explicar muito a fundo o que são nem como funcionam, mas se quiser aprender com sobre elas recomendo [ler o livro open source do Gomex]().

Mas vamos lá, o básico do básico é o seguinte: Docker é uma ferramenta que surgiu baseado no conceito de [Linux Containers ou LXC]() e segue a premissa de utilizar o kernel da máquina host (geralmente o seu computador ou um servidor) para executar um processo. Isso torna os containers um sistema "fechado" e em muitos casos evita a famosa frase "Aaah mas funciona na minha máquina!".

O Docker Compose por sua vez, é uma camada em cima do Docker que permite você desenvolver uma arquitetura de containers de forma menos complicada. Eu particularmente sou fã do Docker Compose uma vez que para mim são mais claras as instruções que estou dando a montar meu container Docker e executar ações nesse container.

Aah e ponto muito importante: Docker e containers não são máquinas virtuais uma vez que sem um kernel para apoiar sua existência não é possível rodar o docker e máquinas virtuais são um sistema contido em si.

## Jekyll, Ruby e outras coisas

Para quem não sabe, Jekyll é um gerador de sites estáticos baseado em markdown. Eu já fiz, um tempinho atrás, um [tutorial de como colocar um site no ar usando Jekyll]() só que esse tutorial considerava que você estava rodando (e instalando) tudo na sua máquina. Se assim como eu, você não quiser instalar um trilhão de gemas ruby, e lidar com o versionamento tanto dessas gemas como do próprio ruby, uma alternativa é usar o Docker.

## Imagem Jekyll

Para começar, vamos fazer o pull da imagem docker em questão:

```console
$ docker pull blabla
```

Isso vai fazer o download da versão mais recente  da imagem jekyll, essa imagem contém o minimo necessario de gemas Ruby para rodar um projeto Jekyll, se preferir você pode também fazer o download de uma imagem minimalista, e instalar apenas os pacotes que você precisa, nesse caso use a `blabla` no lugar da `blabla` do comando acima.


