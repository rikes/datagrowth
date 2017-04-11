---
layout: post
title: Arquitetura de Software
description: "Neste post discutiremos um pouco sobre a arquitetura de software"
modified: 2017-03-28
permalink: /projeto/arquitetura-de-software
published: true
tags: [Arquitetura, Engenharia de Software]
categories: [Projeto de Sistemas]
image:
    feature: software-architecture.jpg
    credit: Gaurav5582
    creditlink: https://www.codeproject.com/Articles/1064240/Introduction-to-Software-Architecture
---




Fala pessoal, hoje iremos discutir um pouco sobre a arquitetura de software e a importância do SOA em projetos de desenvolvimento de software, conceitos um pouco antigo, mas considerado moderno por estar presente nas atividades cotidianas de equipes de desenvolvimento de software. Na postagem de hoje irei me basear no Podcast realizado pela galera do GrokPodcast[^1].



[^1]: <http://www.grokpodcast.com/series/arquitetura-e-design-de-software/>

Então vamos colocar fogo na nesta lenha, com um dos assuntos mais discutidos quanto ao perfil do profissional. Arquiteto de software ajuda no desenvolvimento ou não? Como os cara do podcast mencionaram existe uma visão de que tais profissionais exercem cargos mais elevados na empresa, e que sempre estão atrás de uma mesa separada dando ordem a todo momento. Essa visão de um profissional de arquiteto de software pode até ter sido verdade em algum momento no passado, mas hoje para um profissional deste nível estar no mercado de trabalho se faz necessário a disposição em colocar a mão na massa junto com a equipe de desenvolvimento. Seu papel é organizar uma equipe de desenvolvimento, em um exemplo simples podemos considerar uma equipe desenvolvido um sistema X, neste sistema cada desenviolador será relacionado a uma _task_, cada desenvolvedor deve conhe  cer a sua task, mas como elas se relacionam e como isso ira gerar um sistema? E aí que entra o arquiteto de software, ele deve conhecer todas as _tasks_, e saber como elas se interagem e completam.
<!-- more --> <br>
E é justamente disso que emprega a arquitetura de software, a capacidade de dividir seu projeto de sistemas em diversas frentes. Podemos dizer que um estilo arquitetural é um conceito organizacional, referente a um sistema. Em geral um quando se aplica os conceitos sobre arquitetura de software definimos os "estilos" que serão seguidos ao longo do projeto, existe diversos estilos padronizados um dos mais famosos é o estilo em camadas, na qual o sistema é organizado de forma hierárquica, cada camada oferencedo um serviço as camadas superiores e servindo como cliente a camadas inferior a ela. O modelo OSI é o melhor exemplo para arquiteturas em camadas.

Ao final do podcast os convidados discutem um pouco sobre SOA(_Service-Oriented Architecture_), a definição de SOA é um pouco complexo já que é mais fácil dizer o que ela não é: 


 - SOA não é uma tecnologia;
 - SOA não é uma metodologia;
 - SOA pode ser considerada uma filosofia arquitetural;
 - SOA não é algo que se possa comprar ou instalar;
 - SOA não é um webservice;
 - SOA não cria nada, ela apenas sugere, propõe, define.

Segundo o Blog Iprocess[^2], sua definição está próxima de  "SOA é uma filosofia de TI que visa facilitar a integração entre sistemas, orientando a criação e a disponibilização de soluções modulares e fracamente acopladas baseadas no conceito de serviços".

[^2]: <http://blog.iprocess.com.br/2012/10/soa-arquitetura-orientada-a-servicos/>

## Referências