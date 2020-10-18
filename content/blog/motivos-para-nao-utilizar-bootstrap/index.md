---
title: Motivos para não utilizar Bootstrap
date: "2020-10-17T23:46:37.121Z"
description: Confira alguns motivos para não utilizar Bootstrap.
---

Nesse post te introduzo ao Bootstrap, te explico como ele funciona, e os motivos de não usá-lo (principalmente se você está entrando agora na área).

*PS: O que você irá ler abaixo é apenas uma opinião minha, ok? Você pode utilizar o BS quando quiser.*

### Ah, os frameworks CSS...

Bom, se você caiu aqui de paraquedas e não sabe o que é o "Bootstrap" e muito menos "framework css", pega um café e vamos aprender. Afinal, aprender e ler são coisas agradáveis!


Se formos dar um Google em "o que são frameworks css" receberemos a seguinte resposta: 

> "Frameworks CSS são conjuntos de componentes que provêm uma estrutura básica de elementos reutilizáveis, tendo uma arquitetura consistente de funcionalidade genérica sob a qual a aplicação será construída."

...e certamente o Google não está errado. Deixando o Google de lado, a grosso modo, frameworks são ferramentas que agilizam o desenvolvimento de uma aplicação. Eles agilizam o desenvolvimento, pois como citado, "são conjutos de componentes que provêm uma estrutura básica de elementos reutilizáveis". 

Existem diversos frameworks, mas como o caso do Bootstrap, que é um framework de CSS, ele agrupa um conjunto de classes CSS com estilos. 
Dito isso, então fica bem mais rápido para desenvolver. Concorda?

Por exemplo, caso a gente queira utilizar um botão do Bootstrap, basta inserirmos o ```button``` com as classes no HTML. Assim: 

    <button type="button" class="btn btn-primary">Primary</button>

e o resultado será esse: <br /> ![Alt Text](https://i.gyazo.com/243edbde0fa2bdb43c8065027c180200.png "Um botão HTML com Bootstrap :)")

E não funciona apenas com botões, podemos utilizar para tudo! 

Apesar de o Bootstrap possuir lindos elementos, muitas pessoas utilizam o mesmo apenas por causa do sistema de [grid](https://getbootstrap.com/docs/4.0/layout/grid/), isso porque o sistema de grid é todo responsivo (se adaptam à qualquer tamanho/largura de tela de qualquer dispositivo). 

Mas para que isso tudo funcione, precisamos adicionar o Bootstrap ao nosso projeto. Veja abaixo como.

### Adicionando Bootstrap

Como citei anteriormente, o Bootstrap é um framework de CSS, e para adicionarmos o mesmo em nossa aplicação, precisamos importar através de um arquivo .CSS. Importando o CSS, já podemos brincar com o Bootstrap.

Se a gente der uma olhada na [documentação do Bootstrap](https://getbootstrap.com/docs/4.5/getting-started/introduction/), ele nos diz que precisamos importar dois tipos de arquivos, sendo eles: 

- Arquivo .CSS (Estilizações)
- Arquivo .JS (JavaScript para interações)

*PS: É recomendado importar tanto CSS quanto JS, ok? Isso porque para adicionar as classes você precisa do CSS. É necessário importar o JS pois alguns elementos usam do JavaScript para funcionar (como um [carousel](https://getbootstrap.com/docs/4.5/components/carousel/), por exemplo).*


Para importar o CSS precisamos inserir a folha de estilo abaixo no nosso HTML. 

    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/css/bootstrap.min.css" integrity="sha384-TX8t27EcRE3e/ihU7zmQxVncDAy5uIKz4rEkgIXeMed4M0jlfIDPvg6uqKI2xXr2" crossorigin="anonymous">

Devemos inserir a mesma dentro do ``head``. E o arquivos JS, abaixo, uma linha antes do fechamento do ``body``.

    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ho+j7jyWK8fNQe+A12Hb8AhRq26LrZ/JpcUGGOn+Y7RsweNrtN/tE3MoK7ZeZDyx" crossorigin="anonymous"></script>

Então deve ficar assim:

    <!doctype html>
        <html lang="pt-br">
            <head>
                <!-- Meta tags -->
                <meta charset="utf-8">
                <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

                <!-- Bootstrap CSS -->
                <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/css/bootstrap.min.css" integrity="sha384-TX8t27EcRE3e/ihU7zmQxVncDAy5uIKz4rEkgIXeMed4M0jlfIDPvg6uqKI2xXr2" crossorigin="anonymous">

                <title>Olá, mundo!</title>
            </head>
            <body>
                <h1>Olá, mundo!</h1>


                <!-- Arquivos .JS -->
                <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
                <script src="https://cdn.jsdelivr.net/npm/bootstrap@4.5.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ho+j7jyWK8fNQe+A12Hb8AhRq26LrZ/JpcUGGOn+Y7RsweNrtN/tE3MoK7ZeZDyx" crossorigin="anonymous"></script>
            </body>
        </html>

### Vantagens e desvantagens 

Como você deve ter reparado, a principal vantagem de usarmos o Bootstrap em algum projeto é que "não precisamos mais escrever CSS e nem precisamos sequer preocuparmos com a responsividade". 

Mas como nem tudo são flores, temos as desvantagens de usá-lo. 
Apesar de usarmos as classes, os elementos que já vêm todos "customizados" e tudo prontinho, têm lá seus "defeitos"...

Ao longo desse post eu te introduzi ao Bootstrap, e ensinei que, para "instalar", você precisa importar alguns arquivos. 
Lembra que falei que o Bootstrap agrupa um conjunto de classes CSS? Se você parar para pensar, verá que isso é um problema. 

Visto que o Bootstrap possui mais de três mil linhas de códigos, importar um arquivo que possui essa quantidade enorme de linhas de código, é um grande problema. Podemos reforçar isso pois é praticamente impossível você usar todas as classes presentes no arquivo .CSS do Bootstrap, o que acaba sujando seu .CSS e pesando seu projeto (porque você precisa importar arquivos, concorda?).

E não acaba aqui. Como você viu, o Bootstrap precisa importar os arquivos .JS, o que pesa ainda mais. Entretanto, os arquivos .JS que o Bootstrap importa não são arquivos JavaScript puro (sem outro framework). O JavaScript do Bootstrap importa um framework JavaScript nomeado de "JQuery" (importa apenas na versão 4 do Bootstrap, na 5 ele deixa de usar), o que é um framework que caiu em desuso. Ou seja: quanto mais arquivos você importa = mais pesado ficará seu projeto final.

### (Talvez) o maior problema

Mesmo que importar arquivos para seu projeto seja um problema, (talvez) o maior problema não é esse. Muitos desenvolvedores descobrem do que se trata um framework e ficam loucos para aprender tal, pois quanto menos tempo gasto, melhor. Né?

Diante disso, muitos desenvolvedores que estão iniciando, começam a depender dos frameworks para desenvolverem suas aplicações, pois como o Bootstrap "entrega tudo pronto", fica mais fácil para escrever códigos. 

*Ah Caio, mas qual o problema disso?*

O problema é que, esses novos desenvolvedores, acabam por não aprender a base, que seria o HTML e CSS. E isso se torna um problema enorme, pois para utilizarmos algum tipo de framework, devemos ao menos conhecer a base para conseguirmos aproveitar do framework 100% (ou até mesmo parar de depender de um framework como o Bootstrap).

### Bootstrap ou CSS puro?

Isso vai de cada um. Muitos desenvolvedores utilizam Bootstrap para entregar um projeto que deve ser feito muito em cima da hora, por exemplo. Outros, assim como eu, preferem escrever CSS puro, pois não vão depender de um framework e de milhares de classes.

Dito isso, caso você seja um desenvolvedor iniciante, lhe recomendo a estudar a base de qualquer framework para que você possa prosseguir e aproveitar ao máximo de cada um deles. Tente nunca depender deles, ok? Você pode sofrer um pouco mais escrevendo na mão mas te garanto que você irá aprender mais :)

### Conclusão 

Esse foi um assunto que eu já estava discutindo com alguns colegas em alguns grupos e diariamente vejo a mesma pergunta, então resolvi criar esse post. Acredito que detalhei bastante, ficou bem grande, mas eu espero ter tirado todas suas dúvidas.

Todavia, vimos que, assim como os frameworks podem nos ajudar, eles também podem nos atrapalhar, então devemos pensar bem onde e quando usar eles, afinal ninguém quer um projeto com uns arquivos a mais, hum? 

*Referências: https://getbootstrap.com, https://www.ciawebsites.com.br/sites/o-que-e-bootstrap/, http://www.tutorialwebdesign.com.br/o-que-e-bootstrap/*
