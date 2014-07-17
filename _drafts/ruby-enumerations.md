---

layout: post
title: "ENUM no Ruby on Rails"
categories: RubyOnRails
tags: ruby rails ror enum activerecord

---

Olá, este é o primeiro post do blog!

### O problema

Ao desenvolver aplicações, sistemas, podemos ter a situação (_na verdade sempre acontece!_) em que criamos no banco de dados tabelas para armazenar valores que representarão um estado ou um _status_ de uma determinada entidade. E, com frequência, estes valores geralmente são em número bastante reduzido e praticamente não são alterados com o tempo.

Quer um exemplo? O _status_ de um chamado/ticket em sistemas de atendimento, **geralmente** contem valores como: novo, aberto, em andamento, pendente, solucionado, cancelado. Já o _status_ de uma fatura em um sistema financeiro, pode conter valores como pendente, vencido, cancelado, pago, etc.

Reparou que criaríamos tabelas como *tipos_chamado* e *tipos_fatura* , daríamos uma carga inicial com valores já pré-definidos e possivelmente nunca mais alteraríamos estas tabelas com _inserts_, _updates_ ou _deletes_?

Outra coisa interessante: Outras pessoas poderiam questionar que valores como este deveriam estar na aplicação e não armazenadas em um banco de dados por fazerem parte da lógica da aplicação.

### Enums

Enumerações, ou enums, podem ser descritas como um tipo de dado para descrever conjunto de valores (elementos) que, geralmente se comportam como constantes.

Assim, se considerarmos que os _status_ de uma fatura para nossa aplicação de acordo com nossas regras de negócio se comportariam como constantes e seria relacionados fazendo parte de um conjunto de valores, seria interessante a utilização de **enums**

FALAR DA EXISTENCIA DAS LOOCKUPS TABLES

MOSTRAR EXEMPLO COM RAILS