---
layout: post
title: Modelos de Domínio
description: "Neste post discutiremos um pouco sobre o domínio Rico e Anêmico"
modified: 2017-04-09
permalink: /projeto/modelos-de-dominio
published: true
tags: [Anêmico,Domínio, Engenharia de Software]
categories: [Projeto de Sistemas]
image:
    feature: model-anemic-rich.jpg
    credit: Julie Lerman
    creditlink: https://www.slideshare.net/JulieLerman/entity-framework-ddd
---


O desenvolvimento em camadas não é nada revolucionário no desenvolvimento de software, equipes experientes sabem o valor de separar as regras de negócio de outras camadas, muitos de nós programadores aprendamos na faculdade os princípios de orientação a objeto, são diversas conceitos que evoluem e enriquecem a maneira de se escrever código, em comparação ao modelo procedural é uma grande evolução para o desenvolvimento de software em camadas. Mas será que estamos no caminho certo? É isso que pretendo discutir neste artigo.

Um dos princípios básicos que aprendemos em Orietação a Objetos(OO) se refere ao desenvolvimento de uma classe, que representa um "objeto" do mundo real. Uma objeto possuí características(atributos) e ações(métodos), uma classe que atenda esses requisitos é considerada OO. Mas pensando um pouco melhor quantas vezes você já criou uma classe apenas com alguns atributos e _getters_ e _setters_? Perdeu a conta né? Quando você não cria métodos em sua classe que representam ações você está fugindo de OO e mais, problemas que tinhamos na linguagem procedural estão de volta como: Repetição de código, Propagação de _bugs_, inconsitência, dificuldade de manutenção, entre outros...

<!-- more -->

Por tais motivos equipes de desenvolvimentos foram aprimorando suas técnicas e foi sendo desenvolvido diferentes tipos de **arquitteturas em camadas**. Arquiteturas que propõem a divisão em três ou cinco camadas se tornanram muito comuns e difundidas, veja o seguinte exemplo:

{% highlight java linenos %}
// camada de modelo
class NotaFiscal {
  private int numero;
  private double valor;
  private String razaoSocial;
  // getters e setters
}
 
// camada de regra de negocios
class NotaFiscalBLL {
  public void encerraNota(NotaFiscal nf) {
    nf.setEncerrada(true);
  }
}
 
// camada de acesso a dados
class NotaFiscalDAO {
  public void insere(NotaFiscal nf) {
    // insert into nota fiscal (...)
  }
}
{% endhighlight %}

Como podemos ver, temos o problema citado anteriormente. O fato de achar que está utilizando OO, mas não está, mesmo em uma linguagem tão tradicional para OO como Java. Perceba, no momento que separamos dados de um lado, e comportamento de outro, voltamos a programar de maneira procedural. Nesse tipo de arquitetura,é comum vermos imensas classes com as regras de negócios repetidas e espalhadas. A consequência disso? Um código dificílimo de ser mantido e evoluído. Tanto é que, hoje, esse tipo de arquitetura, é conhecida por **modelo anêmico**.

Esta semana escutei mais uma vez o galera do dotnetarchitects[^1], apesar da qualidade do áudio está um pouco ruim está semana os convidados eram de primeira. Em muitos momentos os convidados discutem os problemas do modelo anêmico e exaltam **modelos ricos**, que são aqueles que seguem à risca princípios que realmente deram certo, que concentram informações em um único ponto do sistema, tornando mais fáceis de testar e evoluir. 

[^1]: <http://podcast.dotnetarchitects.net/2010/03/podcast-11-modelo-anemico/>

Um dos modelos ricos mais consagrados até hoje é o DDD (_Domain-Driven Design_), que é um padrão de modelagem de software totalmente orientado a objetos, que tem como objetivo reforçar todos os princípios e boas práticas que estão de alguma forma relacionadas a OO. Bom,mas isso é história para outro post, não dá para falar de DDD com pouco texto.



## Referências

<http://blog.caelum.com.br/o-que-e-modelo-anemico-e-por-que-fugir-dele/>


