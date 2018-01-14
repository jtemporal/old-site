---
title: "Comandos Docker"
layout: post
date: '2018-01-14 08:00:00'
tags:
- colinha
- docker
- português
- container
- containers
- conteiner
- conteiners
comments: true
---

Se você lida com Docker diariamente é necessário saber alguns comandos. Se você for feito eu que esquece essas coisas, aqui vai uma colinha pra ajudar ;)

## Sumário
<!--toc-->
1. [Listando](#listando)
1. [Removendo](#removendo)
1. [Matando](#matando)
1. [Alguns opções válidas de conhecer](#opcoes)
<!--end toc-->

---

<h2 id="listando">Listando</h2>

### Imagens na sua máquina
Lista todas as imagens da sua máquina inclusive as penduradas (dangling)

``` console
$ docker images -a
```

### Containers em execução

``` console
$ docker ps
```

### Todos containers

``` console
$ docker ps -a
```

---

<h2 id="removendo">Removendo</h2>

### Um container
Removendo um cotainer que foi parado

``` console
$ docker rm ID
```

### Uma imagem do sistema
Se a imagem nao estiver em uso, você pode removê-la usando o comando abaixo e a ID da imagem

``` console
$ docker rmi ID
```

### Todas imagens do sistema
Remove **TODAS** as imagens Docker da sua máquina. Use com cuidado!

``` console
$ docker system prune --all
```
![resultado da remoção](https://i.imgur.com/BCPzKXW.png)

---

<h2 id="matando">Matando</h2>

### Um ou mais containers
Basta passar uma lista de IDs para matar mais do que um container

``` console
$ docker kill ID
```

---

<h2 id="opcoes">Alguns opções válidas de conhecer</h2>

### -a
Maioria, se não todos, os comandos e subcomandos do Docker possuem uma opção `-a` que vem de `all` todos.

### --rm
Mesma coisa coisa acontece com a opção `--rm`. Quando usada ela indica que o container deverá ser removido após sua execução
