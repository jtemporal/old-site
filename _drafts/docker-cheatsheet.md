---
title: "Colinha docker"
layout: post
date: '2018-01-14 08:00:00'
tags:
- docker
- português
comments: true
---

## Listando

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

## Removendo

### Uma imagem do sistema
Se a imagem nao estiver em uso, você pode removê-la usando o comando abaixo e a ID da imagem

``` console
$ docker rmi ID
```

### Todas imagens do sistema
Remove **TODAS** as imagens docker da sua máquina. Use com cuidado!

``` console
$ docker system prune --all
```
![resultado da remoção](https://i.imgur.com/BCPzKXW.png)

---

## Matando

## Um ou mais containers
Basta passar uma lista de IDs para matar mais do que um container

``` console
$ docker kill ID
```
