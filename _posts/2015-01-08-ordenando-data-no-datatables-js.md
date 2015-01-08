---
layout: post
title: "Ordenando datas no DataTables.js"
date: 2015-01-08 23:29:12
categories: javascript
tags: js datatables moment javascript
---

Atualmente o melhor, ou mais conhecido, ou mais usado plugin para prover funcionalidades
em tabelas é o famoso [DataTables.js][datatables].

Os recursos são muitos e sua utilização é bem simples. Paginação e pesquisa é uma
beleza e integrar em suas tabelas é bem fácil deixando-as mais robustas para o
usuário. Adicionando o recurso de escolha de ordenação pelas colunas finaliza uma
configuração básica, funcional e proveitosa para seu projeto.

### O problema

No entanto, a ordenação de datas não sai simplesmente com o [DataTables.js][datatables]
básico. Se você experimentar, verá que a ordenação por colunas com Datas (e suas variações)
não funciona.

Dar uma pesquisada no [Novo Pai dos Burros][google-search-result] por palavras como
_datatables date sorting_ será seu primeiro passo como bom desenvolvedor! Tem muita
coisa por lá, muitas soluções, algumas gambiarras que funcionam, outras que se perdem no tempo.

A solução que utilizava era um [plugin][datatables-sorting-deprecated] que está na
própria página do [DataTables.js][datatables] na seção _plugins/sorting_.
Mas o plugin em 2015 está [deprecated][deprecated]. O que fazer agora?


### O que funciona hoje

Em 18/12/2014 em um post no site do próprio site do [DataTables.js][datatables],
foi postado a nova maneira de ordenar colunas com datas. Bem simples e você pode
conferir [aqui][datatable-sorting-new].

Basicamente o novo plugin chamado [datetime-moment][datetime-moment.js] é uma implementação com base
no [Moment.js][moment], uma biblioteca bastante poderosa para se trabalhar
com datas com javascript.


### Como funciona? Como ordenar datas no Datatable.js?

Direto ao assunto então:

Primeiro, claro, adicionar as bibliotecas [datetime-moment][datetime-moment.js] e
[Moment.js][moment] ao seu projeto. (seguindo boas práticas como
  minificando, comprimindo... :P)

Depois,

```javascript
$(document).ready(function() {
  $.fn.dataTable.moment( 'DD/MM/YYYY' );
  //Existem infinitos formatos suportados! Confere no site

  $('#my-table').DataTable();
    //aqui vai a configuração normal do datatable em sua tabela
  } );
```

Pronto!


[datatables]: http://datatables.net
[datatables-sorting-deprecated]: https://datatables.net/plug-ins/sorting/date-dd-MMM-yyyy
[datatable-sorting-new]: https://datatables.net/blog/2014-12-18
[datetime-moment.js]: https://github.com/DataTables/Plugins/blob/master/sorting/datetime-moment.js
[deprecated]: http://en.wikipedia.org/wiki/Deprecation
[moment]: http://momentjs.com
[google-search-result]: https://www.google.com.br/search?client=safari&rls=en&q=datatables+date+sorting+format&ie=UTF-8&oe=UTF-8&gfe_rd=cr&ei=6_uuVODCJ4aX8QeNpYGACQ#rls=en&q=datatables+date+sorting
