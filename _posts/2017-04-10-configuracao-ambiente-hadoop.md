---
layout: post
title: Configuração de ambiente para Hadoop
description: "Neste post explicarei de forma mais detalhada possível a instalação do Hadoop e a preparação de seu ambiente"
modified: 2017-04-09
permalink: /hadoop/configuracao-ambiente-hadoop
published: true
tags: [hadoop,Big Data, Instalação]
categories: [Big Data]
image:
    feature: hadoop.jpg
    credit: Intel Free Press
    creditlink: https://www.flickr.com/photos/intelfreepress/8552968000
---


Neste post explicarei de forma mais detalhada possível a instalação do Hadoop e a preparação de seu ambiente no ubuntu.

A instalação do Hadoop por conta própria em sua máquina linux, se faz algo custoso, mas necessário para entender desde o básico sobre ele. De modo alternativo você poderá utilizar-se de máquinas virtuais ou efetuar o download de um ambiente preparado oferecido pela Cloudera.
Tenha coragem e se aventure nos próximos passos a seguir ;) 
<!-- more -->
Pré-requisitos:
 - Ubuntu 16.04 LTS
 - Hadoop 2.7.3
 
# Hadoop

_Hadoop_ é um sistema computacional distribuído que oferece agilidade na análise de arquivos extensos. Possui robustez contra falhas nos nodos do cluster através de serviços que monitoram os nodos(mestre e escravo) e a aplicação que manuseia os arquivos. 
Antes de prosseguirmos, certifique-se que seu ambiente esteja atualizado executando o seguinte comando:

`sudo apt-get update && sudo apt-get upgrade`

## Modo Single-Node

### Instalando Java
A instalação do Java se faz necessário já que o Hadoop usa a JVM como plataforma e execução de seus códigos.  Lembrando que o Ubuntu não tem mais o Oracle JDK em seus repositórios, por se tratar de um código proprietário, portanto, instalaremos a _OpenJDK_, uma versão recomendada no Wiki da [Apache](https://wiki.apache.org/hadoop/HadoopJavaVersions).

 
1. Atualiza os pacotes:<br> `sudo apt-get update`

2. Instale o Java OpenJDK: <br> `sudo apt-get install default-jdk`

3. Verifique a instalação:<br> `java -version` 

4. Verifique o caminho de sua instalação:<br> `update-alternatives --config java`

5. Configure o Java Home:<br> `sudo nano /etc/environment`

6. Adicione na última linha o local de instalação:<br> `JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/" `

7. Verifique se foi configurada com sucesso:<br>  `echo $JAVA_HOME`

### Adicionando usuário dedicado ao Hadoop
De forma a garantir a execução dos serviços Hadoop é recomendável criar um usuário e grupo próprios para manipulação sua manipulação. Com este usuário será possível fazer conexões via SSH com outros nós contidos em um cluster Hadoop, porém sem acesso aos privilégios de um administrador, evitando danos ao sistema local.
1. Crie um grupo de usuário:<br> `sudo addgroup hadoop`
2. Crie o usuário _hduser_ e adicione no grupo Hadoop:<br> `sudo adduser --ingroup hadoop hduser`
3. Adicione uma senha (recomendável)
4. Adicione _hduser_ para o grupo de super usuários:<br> `sudo adduser hduser sudo`

### Instalar e configurar SSH
Nesta etapa será feito a instalação do SSH, a chave gerada deverá ser copiada para o arquivo _authorized_keys_.

1. Instalação:<br> `sudo apt-get install ssh`
2. Logue como _hduser_:<br> `su hduser`
3. Gere os pares de chave de autenticação:<br> `ssh-keygen -t rsa -P ""`
4. Este comando adiciona a chave recém criada para a lista de chaves autorizadas:<br> 
`cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys`
5. Cheque se o ssh está funcionando, a versão é exibida na tela:<br> `ssh localhost`

## Desativando IPV6
Nas primeiras versões do Hadoop havia conflitos graves com o protocolo IPV6, não encontrei uma nota oficial informando que este conflito teria sido resolvido e por vias das dúvidas considero como melhor opção sua desativação. 

1. Instale o pacote _gksu_:<br> `sudo apt-get install gksu`
2. Edite o arquivo _/etc/sysctl.conf_: <br> `gksu gedit /etc/sysctl.conf`
3. Acrescente as linhas abaixo para desabilitá-lo: <br>
{% highlight vim linenos %}
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1
{% endhighlight %}
4. Reinicie o computador.
5. Verifique a instalação, 0 habilitado e 1 desabilitado:<br> `cat /proc/sys/net/ipv6/conf/all/disable_ipv6`


### Instalação do Hadoop
A versão estável no dia que escrevi este documento é a versão 2.7.3, caso queira alterar insira o link no navegador removendo as duas últimas barras.

***
Fugindo um pouco sobre a instalação, mas nem tanto, vamos falar um pouco sobre as definições de estruturas de diretório do Linux, que é essencial para seu funcionamento.

Raiz:<br> 
- _/etc_ é usado para armazenar arquivos de configuração;
- _/home_ é utilizado para armazenar arquivos específicos do usuário.
Aplicações:<br>
- _/bin_ e _/sbin_ é usado para armazenar programas vitais para o sistema operacional;
- _/usr/bin_ e _/usr/sbin_ é utilizado para programas não vitais do SO, porém utilizado por todo o sistema;
- _/usr/local_ é usado para armazenar programas instalados localmente;
- _/var_ é utilizado para armazenar dados dos programas.
Fontes:<br>
- _/opt_ é utilizado para armazenar programas não empacotados, ou seja, em sua maioria fontes; 
- _/srv_ é utilizado para armazenar os serviços de sua aplicação. E é aqui que é recomendável a instalação dos pacotes baixados do Hadoop.

Porém, como estamos criando um ambiente de teste, vamos em um primeiro momento criar e utilizar uma pasta em: _/usr/local/hadoop_. PAra mais detalhes e regras sobre o padrão e recomeçadões de diretórios visite a página do [Stack Exchange](http://unix.stackexchange.com/questions/tagged/directory).
***

A seguir os passos necessários para instalação do ambiente Hadoop.

1. Download:<br> `wget http://mirrors.sonic.net/mirrors/apache/hadoop/common/hadoop-2.7.3/hadoop-2.7.3.tar.gz`
2. Extração:<br> `tar xvzf hadoop-2.7.3.tar.gz`
3. Cria uma pasta hadoop:<br> `sudo mkdir /usr/local/hadoop `
4. Entre na pasta extraída **e** mova para uma pasta Hadoop:<br> `sudo mv * /usr/local/hadoop`
5. Dê permissões da pasta ao usuário _hduser_:<br> `sudo chown -R hduser:hadoop /usr/local/hadoop`

### Modificando as configurações de arquivos do Hadoop
Bom, eu uso o **nano**, mas você pode usar qualquer editor para salvar o arquivo. Precisamos do endereço do nosso java, no meu caso: **/usr/lib/jvm/java-8-openjdk-amd64**. Então digite por exemplo nano + o arquivo. 
**OBS: Pode haver incompatibilidade com o formato do arquivo xml, é necessário
retirar a '?' da tag inicial e fechar as tags.** 
Arquivos que serão modificados:

1. `~/.bashrc`
2. `/usr/local/hadoop/etc/hadoop/hadoop-env.sh`
3. `/usr/local/hadoop/etc/hadoop/hdfs-site.xml`
4. `/usr/local/hadoop/etc/hadoop/core-site.xml`
5. `/usr/local/hadoop/etc/hadoop/mapred-site.xml.template`

> Bashrc

Este comando adiciona os endereços e atalhos do hadoop. Adicione ao fim da linha:<br> 
`sudo nano ~/.bashrc`

{% highlight vim linenos %}
\#HADOOP VARIABLES START
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export HADOOP_INSTALL=/usr/local/hadoop
export PATH=$PATH:$HADOOP_INSTALL/bin
export PATH=$PATH:$HADOOP_INSTALL/sbin
export HADOOP_MAPRED_HOME=$HADOOP_INSTALL
export HADOOP_COMMON_HOME=$HADOOP_INSTALL
export HADOOP_HDFS_HOME=$HADOOP_INSTALL
export YARN_HOME=$HADOOP_INSTALL
export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_INSTALL/lib/native
export HADOOP_OPTS="-Djava.library.path=$HADOOP_INSTALL/lib"
\#HADOOP VARIABLES END
{% endhighlight %}

Recarregue o arquivo: ´source ~/.bashrc´

> hadoop-env.sh

`sudo nano /usr/local/hadoop/etc/hadoop/hadoop-env.sh`

export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64

> hdfs-site.xml

Precisamos configurar cada host no cluster. Vamos especificar os diretórios do nameNode e dataNode no host. Vamos criar as pastas com eles: <br>
`sudo mkdir -p /usr/local/hadoop_store/hdfs/namenode `<br>
`sudo mkdir -p /usr/local/hadoop_store/hdfs/datanode `<br>
`sudo chown -R hduser:hadoop /usr/local/hadoop_store`<br>

Agora editamos o arquivo hdfs-site.xml:<br>
`sudo nano /usr/local/hadoop/etc/hadoop/hdfs-site.xml`

{% highlight xml linenos %}
<configuration> 
 <property> 
  <name>dfs.replication</name> 
  <value>1</value> 
  <description>Default block replication. 
  The actual number of replications can be specified when the file is created. 
  The default is used if replication is not specified in create time. 
  </description> 
 </property> 
 <property> 
   <name>dfs.namenode.name.dir</name> 
   <value>file:/usr/local/hadoop_store/hdfs/namenode</value> 
 </property> 
 <property> 
   <name>dfs.datanode.data.dir</name> 
   <value>file:/usr/local/hadoop_store/hdfs/datanode</value> 
 </property> 
</configuration>
{% endhighlight %}

> core-site.xml

Crie um diretório tmp e dê permissões a ele: <br>
1. `sudo mkdir -p /app/hadoop/tmp `<br>
2. `sudo chown hduser:hadoop /app/hadoop/tmp `

Agora mude o arquivo core:<br>
`sudo nano /usr/local/hadoop/etc/hadoop/core-site.xml `

{% highlight xml linenos %}
<configuration> 
 <property> 
  <name>hadoop.tmp.dir</name> 
  <value>/app/hadoop/tmp</value> 
  <description>A base for other temporary directories.</description> 
 </property> 
 <property> 
  <name>fs.default.name</name> 
  <value>hdfs://localhost:54310</value> 
  <description>The name of the default file system.  A URI whose 
	  scheme and authority determine the FileSystem implementation.  The 
	  uri's scheme determines the config property (fs.SCHEME.impl) naming 
	  the FileSystem implementation class.  The uri's authority is used to 
	  determine the host, port, etc. for a filesystem.</description> 
 </property> 
</configuration>
{% endhighlight %}

> mapred-site.xml.template

Renomeie o arquivo indicado template:<br> 
1. `cp /usr/local/hadoop/etc/hadoop/mapred-site.xml.template /usr/local/hadoop/etc/hadoop/mapred-site.xml`
<br>
2. `sudo nano /usr/local/hadoop/etc/hadoop/mapred-site.xml `

{% highlight xml linenos %}
<configuration> 
 <property> 
  <name>mapred.job.tracker</name> 
  <value>localhost:54311</value> 
  <description>The host and port that the MapReduce job tracker runs  at.  
             If "local", then jobs are run in-process as a single map  and reduce task. 
  </description> 
 </property> 
</configuration>
{% endhighlight %}

### Formatar sistema de arquivos Hadoop (NameNode)
O último passo para podermos inicializar o Hadoop e a formatação do Namenode. Lembrando que o NameNode é responsável pelo HDFS:<br> 

`hadoop namenode –format`

Caso o comando não seja reconhecido, entre na pasta do hadoop e digite:<br>
`bin/hadoop namenode -format`

### Inicialize o Hadoop

Caso tenha configurando tudo certo até aqui, poderá inicializar e executar os _daemons_(software que executa em segundo plano e não exige entradas do usuário) do Hadoop. 
Com o usuário hadoop será possível executar os comandos através de variáveis de ambiente:<br>
```
$HADOOP_HOME/sbin/start-dfs.sh
$HADOOP_HOME/sbin/start-yarn.sh
```

Se a chave SSH for solicitada durante este processo basta digitar 'y' no terminal.
Caso os comandos acima não funcionem algo deu errado em suas variáveis de ambiente, tente executar os seguintes passos:

Navegue para:<br> `cd /usr/local/hadoop/sbin `

Inicie os processos, como o Yarn, HDFS, DataNodes e NameNodes na pasta bin execute o comando: **start-all.sh** 

Verifique se os serviços foram iniciados com o comando: _jps_. Deverá aparecer algo como:

**9026 NodeManager**<br>
**7348 NameNode**<br>
**9766 Jps**<br>
**8887 ResourceManager**<br>
**7507 DataNode**

Também é possível verificar pelo localhost, vá no seu navegador e entre no endereço: http://localhost:50070/ e http://localhost:8088/

## Modo Distribuído
O Hadoop trabalha em uma arquitetura do tipo "Mestre x Escravo", normalmente uma máquina do cluster é designada como _NameNode_ e a outra máquina como _JobTracker_, estes são os reais "nós mestres". O restante das máquinas do cluster, tanto os _DataNodes_ como os _TaskTracker_ são os "nós escravos".

### Configuração de Ip's
Em nosso exemplo teremos três máquinas, uma com master e dois slaves. Verifique os ip's de suas máquinas e mude conforme seu caso.

1. Edite o arquivo /etc/hosts/ no nó master;<br>
`127.0.0.1 master`
`192.168.2.11 slave-1`
`192.168.2.12 slave-2`

2. Verifique a configuração nas máquinas;
`sudo hostname -f`

3. Edite o arquivo /etc/hosts/ nas máquinas escravas;<br>
`192.168.2.10 master`
`127.0.0.1 slave-1`
`192.168.2.12 slave-2`

4. Verifique a configuração em casa slave;
`hostname -f`

5. Configure o ssh para que possa ser autorizado a troca de dados no cluster. Dando permissão para que elas possam se conectar.
Replique os comandos abaixo em casa máquina do cluster:<br>

* `ssh-keygen -t rsa`
* `ssh-copy-id -i ~/.ssh/id_rsa.pub [hduser]@master`
* `ssh-copy-id -i ~/.ssh/id_rsa.pub [hduser]@slave-1`
* `ssh-copy-id -i ~/.ssh/id_rsa.pub [hduser]@slave-2`

Cheque se a configuração foi executada com sucesso. Execute o comando abaixo e deverá logar nas máquinas sem a requisição de uma senha.

1. `ssh master`
2. `exit ( fazendo logout)`
3. `ssh slave-1`
4. `exit ( fazendo logout)`
5. `ssh slave-2`
6. `exit ( fazendo logout)`




***

Referências:
...
https://wiki.apache.org/hadoop
http://www.scratchtoskills.com/install-hadoop-2-7-2-on-ubuntu-15-10-single-node-cluster/
Livro: Analítica de dados com Hadoop






