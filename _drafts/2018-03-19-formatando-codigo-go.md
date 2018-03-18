---
title: "Formatando código Go usando o próprio Go pra isso"
layout: post
date: '2018-03-19 08:00:00'
tags:
- colinha
- go
- gophers
- golang
- formatação
- português
comments: true
---

Coisa linda de se ver é usar um formatador de código, principalmente quando você tem preguiça de ficar formatando coisas ou quando você está preocupada em aprender a sintaxe de uma nova linguagem e ainda não pegou o jeito com o estilo de código.

A colinha de hoje mostra como a linguagem de programação [Go](https://golang.org/) ajuda a formatar o código sem sofrimento.

Então vamos lá, vamos supor que você escreveu o seguinte código num arquivo chamado `helloworld.go`:

```go
package main
import "fmt"
func main(){
fmt.Println("Hello world!")
}
```

Até aí tudo bem, esse códgio compila e se você fizer `go run helloworld.go` ele ainda escreve na tela o seu `Hello World!` porém, se você tivesse que mandar esse código para um projeto aberto, provavelmente pessoas revisando seu código iriam pedir para você formatá-lo melhor.

Existe um monte de ferramentas própria da linguagem para ajudar a pessoa que desenvolve, sendo uma delas o `gofmt`. Ele pode mostrar na tela a formatação indicada para um código fonte ou até mesmo formatar para você o código que você escreve. Para usar o `gofmt` basta passar o nome do arquivo para ele:

```console
gofmt helloworld.go
```

Isso irá escrever na tela a versão formatada do seu código fonte. Existem algumas flags que você pode usar para mudar esse resultado. Por exemplo, a flag `-d` irá mostrar um diff do seu arquivo num formato idêntico ao `git diff`ótimo para envio de patches.

Mas a flag/opção mais interessante é a `-w` que converte a impressão na tela para escrita em arquivo. Nesse caso, se você utilizar essa flag assim:

```console
gofmt -w helloworld.go
```

Nada será printado na tela e o código formatado será escrito no seu arquivo fonte, então aquele código que eu mostrei no início, após a execucção com a flag `-w` fica assim:

```go
package main

import "fmt"

func main() {
        fmt.Println("Hello World!")
}
```

Massa né? Agora não tem mais desculpa pra não formatar os códigos bonitinhos os 😜

----
## Links

## Agradecimentos
Principalmente ao Cesar que pacientemente tem me ensinado Go.
