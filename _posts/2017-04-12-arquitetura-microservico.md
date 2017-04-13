---
layout: post
title: Arquitetura Microservice
description: "Afinal, o que é microserviços e qual a necessidade dela em sua empresa"
modified: 2017-04-12
permalink: /projeto/arquitetura-microservico
published: true
tags: [microservice,Projeto,Arquitetura]
categories: [Projeto de Sistemas]
image:
    feature: microservice.png
    credit: Peter B. Nichol 
    creditlink: https://leadersneedpancakes.com
---



Quando falamos em implantar uma solução de arquitetura em _microserviços_,estamos discutindo uma alternativa com diversas vantanges(e desvantagens) sobre o padrão adotado por muitas empresas sobre a arquitetura monolítica. Esse padrão funciona razoalvemente bem para aplicações de complexidade baixas e pequenas, pois o desenvolvimento, testes e build(implantação) é relativamente simples. No entanto, aplicações complexas, grandes com um alto consumo de tempo, processamento e memória, acaba tornando um obstáculo ao desenvolvimento e implantação, dificultando a manutenibilidade e adoção de novas tecnologias do mercado.

<!-- more -->

A arquiteura de _microserives_ tem muitas vantanges sobre a monolítica, a ideia é dividir uma determinada aplicação em pequenos seriviços selecionados e acionados por qualquer outro tipo de aplicação não importando a tecnologia da mesma, de modo que a união destas partes realize um trabalho maior. Assim, os microserviços permitem a integração entre vários serviços e a inserção de vários componentes no sistema.

Enquanto as aplicações monolíticas preferem um único banco de dados lógico, as empresas geralmente preferem um único banco de dados em uma variedade de aplicativos. Microservices preferem deixar cada serviço gerenciar seu próprio banco de dados, deixando instâncias diferentes da mesma tecnologia de banco de dados, ou totalmente diferentes sistemas de banco de dados.

A imagem abaixo demonstra uma aplicação monolítica onde usuários acessam uma aplicação qualquer e suas requisições são disparadas para um mesmo sistema em uma mesma base de dados. Já na arquitetura de microserviços nós temos um usuário acessando também uma aplicação, porém cada ação disparada pelo usuário pode fazer uma chamada para diferentes serviços que compartilham ou não um banco de dados.

<figure>
	<img src="/images/arquitetura-microservice.png" alt="">
	<figcaption >
        Diferenças entre Arquitetura Monolítica e Microserviços.
    </figcaption>
</figure>

 A arquitetura de microservices também tem algumas desvantagens significativas. Em particular, as aplicações são muito mais complexas e constituídas por mais elementos. Apesar de ter inicialmente a nomeclatura _micro_ não é recomendado criar divisões tão pequenas de seus serviços, pois a manutenção e o controle dos serviços será quase impossível.



## Referências


 <https://www.youtube.com/watch?v=ANPvIMUkYQ0>

 <http://blog.caelum.com.br/arquitetura-de-microservicos-ou-monolitica/>





