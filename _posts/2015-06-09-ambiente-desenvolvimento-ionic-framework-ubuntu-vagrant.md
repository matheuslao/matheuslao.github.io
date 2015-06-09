---
layout: post
title: "Ambiente de Desenvolvimento Ionic Framework no Ubuntu 14.04 (com Vagrant)"
date: 2015-06-09 16:10:53
categories: Ionic Framework, Apache Cordova, Mobile, Vagrant
tags: html, css, js, mobile, ionic, cordova, vagrant, ubuntu

---

Pequeno tutorial de como criar uma máquina virtual usando **vagrant** para desenvolver
com **Ionic Framework**

### Vagrant

Vamos trabalhar com uma **box** simples e leve como uma instalação de um **ubuntu 32 bits**.

* Instalar [Virtual Box][virtual_box_download]
* Instalar [Vagrant][vagrant_download]

Baixar a box:

    $ vagrant box add ubuntu/trusty32

Criar um pasta teste que será sincronizada com a máquina virtual e adicionar o *VagrantFile*

    $ mkdir vagrant_ionic
    $ cd vagrant_ionic
    $ vagrant init ubuntu/trusty32

Ligar a máquina:

    $ vagrant up

Entrar na máquina:

    $ vagrant ssh

e vamos para a pasta sincronizada com nossa máquina (perceba que o VagrantFile está lá):

    $ cd /vagrant

### Repositórios ubuntu

Mantenha atualizado seus pacotes com

    $ sudo apt-get update

### Java

Instalar Java 7 com

    $ sudo apt-get install -y openjdk-7-jdk

Adicionar no bashrc:

    $ echo "export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-i386" >> /home/vagrant/.bashrc


### Outras instalações

Instalar também o Ant, NPM

    $ sudo apt-get install -y ant npm

Instalar NodeJS:

    $ sudo npm install -g n
    $ sudo n stable

###Android SDK

Na página de downloads do [SDK][android-sdk-linux] tem várias opções de downloads (somente SKD, Android Studio, etc). Baixemos somente o SDK.

No terminal de sua máquina virtual:

    $ curl -O http://URL_DO_SDK

Descompactamos o arquivo:

    $ tar -xzvf NOME_DO_ARQUIVO_BAIXADO

Adiciona permissão para o usuário *vagrant* da máquina executar conteúdo da pasta como *root*

    $ sudo chown -R vagrant android-sdk-linux/

Se quiser, apague o arquivo zipado baixado:

    $ rm NOME_DO_ARQUIVO_BAIXADO

Agora, adicionamos algumas variáveis de ambiente em seu usuário para o *Android SDK*

    $ echo "ANDROID_HOME=~/android-sdk-linux" >> /home/vagrant/.bashrc
    $ echo "PATH=\$PATH:~/android-sdk-linux/tools:~/android-sdk-linux/platform-tools" >> /home/vagrant/.bashrc

Por fim, atualizamos nosso Android SDK e demais bibliotecas. Até o dia em que escrevi
este post, a API mais atual era a **22** e o *build-tools* era o **22.0.1**:

    $ /home/vagrant/android-sdk-linux/tools/android update sdk -u --all --filter platform-tool,android-22,build-tools-22.0.1


### Apache Cordova e Ionic Framework

Para finalizar as instalações:

    $ sudo npm install -g cordova
    $ sudo npm install -g ionic


### Testando....

Um teste rápido será criarmos um projeto IONIC, adicionarmos uma plataforma e
fazer o *build* gerando o instalável no dispositivo.

    $ ionic start teste

    $ ionic platform add android

    $ ionic build


[virtual_box_download]: https://www.virtualbox.org/wiki/Downloads
[vagrant_download]: https://www.vagrantup.com/downloads.html
[android-sdk-linux]: https://developer.android.com/sdk/index.html#Other
