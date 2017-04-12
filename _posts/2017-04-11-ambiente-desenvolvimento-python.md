---
layout: post
title: Ambiente de desenvolvimento com Python
description: "Neste post farei uma breve explicação de como preparar seu ambiente de desenvolvimento utilizando tecnologias Python"
modified: 2017-04-09
permalink: /hadoop/ambiente-desenvolvimento-python
published: true
tags: [Python,Big Data, Anaconda,Ambiente]
categories: [Big Data]
image:
    feature: pydatalogo.png
    credit: Continuum
    creditlink: https://docs.continuum.io/
---

Apesar do ecossistema Hadoop ser construído em cima do JVM, JAva não é a única opção para programadores. Ao se utilizar o framework _MapReduce_ podemos trabalhar com outras linguagens como C++, R  e Python. Tudo isso através de utilitários disponíveis para Hadoop, junto com a sua instalação temos o utilitário _Hadoop Streaming_, que vem empacotado em um arquivo JAR.


# Python

Precisamos baixar e instalar os pacotes Python disponibilizados nos repositórios linux ou baixar os fontes diretamente no [site](https://www.python.org/downloads/). 
Primeiro vamos atualizar os pacotes locais existentes.
<!-- more -->

`sudo apt-get update && sudo apt-get -y upgrade`

Ao adicionar a flag `-y` estamos informando que concordados de imediato com os termos de aceitação.
Por padrão o Ubuntu já vem com o Python instalado em sua versão 2.7, em versões mais novos do sistema operacional já é possível contar com a versão 3.x do python, então provavelmente não será necessário sua instalação. Você poderá usar os repositórios para efetuar a sua instalação ou efetuar o download dos arquivos necessários no link postado logo acima.

- Verificando versão:<br> `python3 -V`

- Caso não aparece a versão 3.x, instale-a:<br> `sudo apt-get install python3` 

- Python possuí seu próprio gerenciador de pacotes, sua instalação se faz necessário para utilização de novas bibliotecas e complementos do Python: <br> `sudo apt-get install -y python3-pip`

## Complementos do Python

O Python em si é uma excelente linguagem, não abordarei os motivos aqui, mas ela está bem difundida e pode estar presente em todos os ambientes possíveis. Considerada a preferida por profissionais que trabalham com manipulação de dados.
Nos próximos passos mostrarei diversos pacotes e até mesmo ambientes para se desenvolver códigos ricos e com facilidade utilizando Python.
Antes de mostrar cada um dos itens faça a instalação de um conjunto de pacotes considerados essenciais pela comunidade, alguns deles já deverão existir em sua máquina.

`sudo apt-get install build-essential libssl-dev libffi-dev python-dev`

### Numpy

Após instalarmos o gerenciador de pacotes do Python, poderemos buscar bibliotecas que ajudem no desenvolvimento de nossas aplicações. O **Numpy** é um dos pacotes mais básicos para o Python, voltado principalmente para matemáticos e cientista de dados.

`pip3 install numpy`

### Ambiente virtual

Python permite a você criar um ambiente virtual isolado de outros projetos em Python, garantindo assim, que cada um de seus projetos terão seu próprio conjunto de dependências que não conflitaram com outros projetos. Isso te assegura a usar pacotes de terceiros sem que haja problemas críticos em seu ambiente, permitindo um maior controle sobre os pacotes que você esteja trabalhando.
Será necessário instalar o pacote `venv`, em seguida usaremos o comando `pyvenv` que criará nosso ambiente virtual:

- Instalação: <br> `sudo apt-get install -y python3-venv`

- Criamos uma pasta para teste: <br> `mkdir amb cd amb`

- Criamos o ambiente: <br> `pyvenv my_amb`

- Podemos ver os arquivos criado e o tamanho da pasta: <br> `ls my_amb/ && du -csh`

- Para começar a utilizar este ambiente é necessário ativá-lo: <br> `source my_amb/bin/activate`


## Anaconda

Anaconda consiste em uma distribuição para Python, contém diversos pacotes pre-instalados, um gerenciador de pacote chamado _Conda_ e a IDE Spyder. Anaconda é uma excelente opção para cientistas de dados,  ela oferece uma plataforma completa _open-source_ de alto desempenho para Python, R e Scala. Além dos pacotes pré-instalados é possível instalar cerca de 720 pacotes utilizando seu gerenciador _Conda_. Anaconda é mantido e distribuído pela [Continuum](https://www.continuum.io) em todas as plataformas e atende tanto a versão 2.7 quanto a 3.X do Python.
Além de possuir cerca de 70 pacotes em sua instalação (inclusive a NumPy), Anaconda também possui um ambiente virtual próprio, tendo as mesmas vantagens do pacote `venv`, além de outras pois estamos trabalhando em um ambiente desenvolvido e mantido por apenas uma organização.

- Baixe o arquivo .SH de instalação do Conda no site da [Continuum](https://www.continuum.io/downloads)

- Verifique a integridade do arquivo, deve ser igual ao listado na [documentação] (https://docs.continuum.io/anaconda/hashes/lin-3-64). <br> `md5sum Anaconda3-4.3.1-Linux-x86_64.sh`

- Instale a partir do arquivo baixado: <br> `bash Anaconda3-4.3.1-Linux-x86_64.sh`

- Ative a instalação no arquivo _.bashrc_:<br> `source ~/.bashrc`

- Você pode ver todos os pacotes contidos no Anaconda com o comando: <br> `conda list`

Como dito anteriormente Anaconda oferece um ambiente de virtual para você desenvolver de modo seguro seus projetos. Iremos criar um ambiente virtual nos passos seguintes com a versão mais recente do Python 3, mas você pode definir qual versão do Python 3 deseja.

- Crie seu novo ambiente: <br> `conda create --name my_amb python=3`

- Ative o ambiente: <br> `source activate my_amb`

- Verifique a versão instalada: <br> `python --version`

- Os arquivos criados ficam na pasta de `envs` onde foi instalado o Anaconda, podemos verificar este local com o seguinte comando: <br> `conda info --envs`

- Navegando até está pasta podemos ver os arquivos criados e o tamanho da pasta: <br> `ls /home/henrique/anaconda3/envs/my_amb/ && du -csh`

- Para adicionar pacotes como o NumPy podemos utilizar o seguinte comando: <br> `conda install --name my_amb numpy`

- Caso queira remover algum ambiente criado você deverá sair deste ambiente para depois remove-lo: <br> `source deactivate` <br> `conda remove --name my_amb --all`

## Jupyter Notebook 

Jupyter Notebook já vem no pacote de instalação do Anaconda, o Jupyter oferece um ambiente riquíssimo para apresentação de textos, fomulários, fórmulas matemáticas, gráficos, códigos  ou qualquer outro tipo de mídia que um navegador pode interpretar. Ele é recomendável para usuários que desejam maximizar a exibição de seus resultados em um ambiente interativo e de certa forma divertida, considerado em uma tradução livre um Bloco de Anotações Jupyter.

- Execute o Jupyter Notebook: <br> `jupyter notebook`

- Execute sem abrir o mouse automaticamente: <br> `jupyter notebook --no-browser`

Como dito, Jupyter oferece um ambiente moderno para exibição de diversos arquivos. Códigos em **LaTex** e **Markdown** por exemplo são amplamente aceitáveis.

- Entramos no servidor que está rodando localmente.
- Criamos um novo arquivo do tipo notebook **New -> Python3**
- Mudamos a célula para Markdown  **Cell -> Cell Type -> Markdown**
- Inserimos o exemplo abaixo e pressionamos **CRTL+ENTER**

{% highlight Latex linenos %}
# Equação simples

Uma equação que eleva um número ao quadrado:
$$ y = x^2$$

where $x = 2$
{% endhighlight %}
- Podemos inserir novas linhas **Insert -> Insert Cell Below** ou no simbolo de `+`
- Executando um novo código:<br>
{% highlight Python linenos %}
x = 2
y = x*x
print (y)
{% endhighlight %}




