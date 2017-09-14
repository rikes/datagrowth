---
layout: post
title: Configuração do ambiente de banco de dados
description: "Post para descrever a configuração dos softwares utilizados para a modelagem e contrução de meu banco de dados"
modified: 2017-09-09
permalink: /data/config-ambiente-sgbd
published: true
tags: [sgbd,tcc,banco,pentaho,java]
categories: [Big Data]
image:
    feature: Pentaho_new_logo_2013.png
    credit: WikiMedia 
    creditlink: https:\\www.wikimedia.org
---

## Aplicações para armazenagem e processamento de dados

Nos próximos passos irei abordar como configurei meu ambiente com **Pentaho kettle** para extrair dados das fontes utdilizadas, inserindo-os em uma base de dados MySQL e MongoDB.

<!-- more -->

### Instalando o JAVA 8

O Pentaho foi desenvolvido na plataforma Java, para a versão que iremos utilizar do Kettle precisamos ter a versão mais recente do Java 8 instalado, para isso vamos atualizar nossos repositórios e instalar a versão mais recente do Java.
Lembrando que o Ubuntu não tem mais o Oracle JDK em seus repositórios, por se tratar de um código proprietário, portanto, instalaremos a _OpenJDK_.
 
1. Atualiza os pacotes:<br> `sudo apt-get update`

2. Instale o Java OpenJDK: <br> `sudo apt-get install default-jdk`

3. Verifique a instalação:<br> `java -version` 

4. Verifique o caminho de sua instalação:<br> `update-alternatives --config java`

5. Configure o Java Home:<br> `sudo nano /etc/environment`

6. Adicione na última linha o local de instalação:<br> `JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/" `

7. Verifique se foi configurada com sucesso:<br>  `echo $JAVA_HOME`


### Pentaho Data Integration (Kettle)

Depois de instalar o Java 8 e os repositórios do Ubuntu, faremos o download do arquivo em seu [repositório](https://sourceforge.net/projects/pentaho/files/Data%20Integration/). O arquivo que obtemos é semelhante a este: _pdi-ce-7.0.0.0.25.zip_.

1. Cria uma pasta para mover os arquivos de instalação:<br> `sudo mkdir /opt/pentaho` 

2. Extraia o arquivo na pasta _opt/pentaho_:<br> `sudo unzip pdi-ce-7.0.0.0.25.zip -d /opt/pentaho`

3. Vá até a pasta extraída e dê permissão a todos os arquivos do tipo _.sh_:<br> `sudo chmod 755 *.sh`

4. Antes de executar atualize instale a biblioteca _libwebkitgtk_ e atualize seus repositórios:<br>
`sudo apt-get install libwebkitgtk-1.0-0 && sudo apt-get update`

4. Execute o PDI na pasta de instalação (/opt/pentaho/-data-integration) com o seguinte comando: <br> `./spoon.sh`

### Pentaho BI Server (CE)

O servidor de BI do Pentaho permite que você acesse seus dados de negócios na forma de painéis, relatórios ou cubos OLAP através de uma interface web adequada. Além disso, fornece uma interface para administrar seus processos de configuração e agendamento de BI.
A instalação é bem parecida com o PDI, precisamos efetuar o download(versão 7.1 no dia 09/09/2017) em seu [repositório](https://sourceforge.net/projects/pentaho/files/Business%20Intelligence%20Server/7.1/pentaho-server-ce-7.1.0.0-12.zip/download), para darmos continuidade a isntalação:

1. Extraia o arquivo na pasta _opt/pentaho_:<br> `sudo unzip pentaho-server-ce-7.1.0.0-12.zip -d /opt/pentaho`

2. Vá até a pasta extraída e dê permissão a todos os arquivos do tipo _.sh_:<br> `sudo chmod 755 *.sh`

3. Inicie a aplicação junto ao servidor Tomcat: <br>  `sudo ./start-pentaho.sh`

***

#### Problemas encontrados

Bom, tive vários problemas ao instalar esta aplicação, então segue algumas dicas:

- Caso você já tenha o Tomcat instalado, será necessário desinstala-lo completamente. Inclusive apagando seu usuário e o arquivo de serviço(_tomcat.service_). É possível aproveitar a instalação do seu tomcat ou até mesmo um Jboss, mas não é o que queríamos.
- Talvez seja necessário criar uma variável de ambiente em relação ao PENTAHO, fique atento ao iniciar a aplicação.
- Tive muitos problemas com erros de porta já utilizada, a primeira recomedação já resolveria isso, mas ele reclamava de uma outra porta, a **9092**, foi então necessário mudar essa porta e adicionar meu localhost a pasta **/etc/hosts**. Siga esses passos:
1. Edite a porta para **9093** em <br> `pentaho-solutions/system/GettingStartedDB.properties`
2. Edite o arquivo **/etc/hosts** adicionando <br> `127.0.0.1 nomeDaSuaMaquina`
3. Obs: Este é o erro: <br> `Invocation of init method failed; nested exception is org.h2.jdbc.JdbcSQLException: Exception opening port "H2 TCP Server (tcp://localhost:9092)"`


### MoongoDB

### PostgreSQL



