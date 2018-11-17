---
title: "Subindo imagens docker pro dockerhub"
layout: post
date: '2018-11-17 08:00:00'
tags:
- tutorial
- docker hub
- automação
- automatização
- docker
- português
- container
- containers
- conteiner
- conteiners
comments: true
---

Já achou mágico aquelas imagens pros containers docker que qualquer um pode usar e já pensou em fazer uma mas não sabe como? Vem que eu te ensino 😉

Pra começar você vai precisar de uma conta no [Docker Hub](https://hub.docker.com/) é lá que todas todas as imagens para containers Docker vivem. Depois de criar sua continha lá, podemos passar para linha de comando e começar a usar a CLI do Docker.

Vamos começar pelo login, embora você não precise fazer login para fazer o build das suas imagens, uma vez feito o login você pode esquecer que ele existe:

![login](https://raw.githubusercontent.com/jtemporal/autom-dockerhub-example/master/gifs/docker-login.gif)
<center>
<i>docker login</i>
</center>

Agora vamos fazer o build da nossa imagem:

![build da imagem docker](https://raw.githubusercontent.com/jtemporal/autom-dockerhub-example/master/gifs/docker-build-sum.gif)
<center>
<i>docker build -t sum .</i>
</center>

Aqui usamos o parâmetro `-t` para dar nome à nossa imagem. Depois de fazer o build podemos conferir a imagem na nossa lista de imagens disponíveis localmente: 

![listagem de imagens antes do tag](https://raw.githubusercontent.com/jtemporal/autom-dockerhub-example/master/gifs/docker-images-before-tag.gif)
<center>
<i>docker images | grep sum</i>
</center>

Agora que temos uma imagem  pronta, vamos dar uma tag para ela e conferir se ela foi taggeada corretamente:

![docker tag e listagem de imagens depois da tag](https://raw.githubusercontent.com/jtemporal/autom-dockerhub-example/master/gifs/docker-tag-sum.gif)
<center>
<i>docker tag sum $(echo DOCKER_USERNAME)/sum</i>
</center>

Basicamente é esse passo que nos permite divulgar nossas imagens. Então depois de dar uma tag para sua imagem. Chegou a hora de fazer o push (envio da imagem para o Docker Hub):

![push manual da imagem docker](https://raw.githubusercontent.com/jtemporal/autom-dockerhub-example/master/gifs/docker-push-sum.gif)
<center>
<i>docker push $(echo DOCKER_USERNAME)/sum</i>
</center>

e pronto. Agora a imagem foi enviada para o Docker Hub, tornando possível qualquer pessoa usar o `docker pull` para baixar a imagem.

## Algo extra

Ficar fazendo esses passos todos na mão pode ser cansativo se você precisar subir muitas imagens e além disso, tudo que fazemos a mão pode estar propenso a erros. Então o caminho natural seria automatizar essas tarefas.

Existem várias formas de fazer isso, mas vamos aqui usar um _script shell_ que chamei de `push.sh` para isso:

~~~bash
#!/bin/bash

if [ -z ${DOCKER_USERNAME} ]; then
    echo "Missing DOCKER_USERNAME variable!"
    exit 1
fi

error() {
    if [ $? != 0 ]; then
        echo "Error!"
        exit 122
    fi
}

build() {
    echo "=> Building ${1}"
    docker build -t ${1} .
    echo "=> Built ${1}"
}

tag() {
    echo "=> Tagging ${1}"
    docker tag ${1} $(echo $DOCKER_USERNAME)/${1}
    echo "=> Tagged ${1}"
}

push() {
    echo "=> Pushing ${1}"
    docker push $(echo $DOCKER_USERNAME)/${1}
    echo "=> Pushed ${1}"
}

build ${1}
error
tag ${1}
error
push ${1}
error
echo

exit 0
~~~

Nele reproduzi todos os passos que fizemos até aqui  e para usar basta fazer:

![gif do push automatizado](https://raw.githubusercontent.com/jtemporal/autom-dockerhub-example/master/gifs/docker-automated-push.gif)
<center>
<i>./push.sh sum</i>
</center>

Você pode ainda colocar esse script em uma ferramenta de entrega contínua e deixar a mágica acontecer.

---

## Links

Os códigos e passos demonstrados aqui [estão neste repositório do GitHub](https://github.com/jtemporal/autom-dockerhub-example) passa lá pra deixar uma ⭐️
