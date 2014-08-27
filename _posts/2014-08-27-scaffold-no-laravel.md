---
layout: post
title: "Scaffold no Laravel"
date: 2014-08-27 17:29:12
categories: php laravel
tags: php laravel scaffold
---

Depois de muito tempo sem programar em PHP (hoje estou no mundo Ruby, Java),
resolvi testar um framework cujo site, documentação e comunidade me chamou a
atenção: [Laravel Framework][laravel]. E para mim que sou apaixonado pelo Rails,
de cara fiquei curioso em algo "parecido" no PHP.

Iniciando o estudo e utilização do [Laravel][laravel], realizei a instalação e
configuração do ambiente de desenvolvimento sem problemas através de sua
excelente documentação e ferramentas disponíveis como o [Laravel Homestead][homestead].

### Cadê meu Scaffold?

Vendo os conceitos de REST, _migrations_, e o modo de trabalho com _routes_,
criação de _models_, _controllers_ e _views_ presentes no [Laravel][laravel]
(como no Rails), a primeira coisa que quis fazer foi o conhecido [scaffold][scaffold]

Não achei na documentação oficial nada referente a esta funcionalidade, que julgo
interessantíssima para quem inicia o desenvolvimento em um framework novo.

Mas tudo bem. A comunidade é grande e alguém (ou muitos) deve ter sentido falta
e feito algo!

### Procurando...

Ao digitar no Google as simples palavras `laravel scaffold` os resultados são
bacanas. Muitos posts, implementações.

Como primeiro link no google, um projeto no [GitHub][github] do Jeffrey Way
bem documentado e que tinha tudo que procurava:

[Laravel Generators][laravel-generator]

Mas até o dia em que escrevi este post, não funcionou. Configuração de meu ambiente:

* Mac OS x 10.9.4
* Laravel Homestead - versão 0.1.7 (PHP 5.5., Nginx, MySql...)
* Laravel Framework 4.2.8

As vezes ocorriam alguns erros na execução do _migrate_ no banco e todas as tentativas
resultavam _views_ vazias, sem implementações.

### A Solução

Um outro desenvolvedor deu um _fork_ no projeto do Jeffrey e ainda adicionou nas
 _views_ do scaffold o conhecido quebra-galho [Twitter Bootstrap][twitter-boot]!

O projeto:

[Laravel Generators 4 with Bootstrap 3][laravel-generator-boot]

Como _fork_ do projeto original, o conteúdo e passa-a-passo para utilizacão
continua intuitivo e desta vez **FUNCIONOU**!


### A Dúvida do Iniciante

Minha grande dúvida consiste em: por quê o Laravel não apresenta um _scaffold_
básico? O Projeto destacado acima não poderia ser integrado ao core do framework?

[laravel]: http://www.laravel.com
[homestead]: http://laravel.com/docs/homestead
[github]: http://www.github.com
[twitter-boot]: http://getbootstrap.com
[laravel-generator]: https://github.com/JeffreyWay/Laravel-4-Generators
[laravel-generator-boot]: https://github.com/wdollar/Laravel-4-Generators-Bootstrap-3
[scaffold]: http://en.wikipedia.org/wiki/Scaffold_(programming)
