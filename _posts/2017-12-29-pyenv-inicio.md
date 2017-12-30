---
title: "Python e suas versões: pyenv"
layout: post
date: '2017-12-29 10:00:00'
tags:
- colinha
- python
- pyenv
- versoes
- português
comments: true
---


Uma das primeiras coisas que aprendemos sobre [Python](https://www.python.org/) é que existem mais de uma versão da mesma linguagem funcionando a todo vapor. Isso traz alguns problemas e a inevitável pergunta _"Qual versão eu devo usar?"_. A colinha de hoje mostra uma forma de instalar e manter o controle de vaárias versões do Python na sua máquina 😉.

Entre outras coisas, as duas melhores coisas que o [pyenv](https://github.com/pyenv/pyenv) faz na minha humilde opinião são:

1. instalar novas versões do Python;
1. escolher a versão global do Python.

![sombrancelhas gif](https://media.giphy.com/media/10lqVdCCc9812M/giphy.gif)

Pra começar você precisa instalar ele, aqui eu vou mostrar um dos métodos de instalação, mas [lá no _readme_ do projeto tem outras](https://github.com/pyenv/pyenv#installation) (e também detalhes espeficíficos de cada sistema operacional):

~~~ console
$ git clone https://github.com/pyenv/pyenv.git ~/.pyenv
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
$ exec "$SHELL"
~~~

Depois desse passo é bem facinho, as outras versões do Python estão a um _install_ de distância:

~~~ console
$ pyenv install 3.6.4
~~~

Se tiver em dúvida quais versões você pode instalar só usar a flag `-l` com o _install_ que ele vai listar todas:

~~~ console
$ pyenv install -l
~~~

Massa né? Agora é só sair instalando adoidado 😂

----
