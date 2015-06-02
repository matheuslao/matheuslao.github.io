---
layout: post
title: "Formatando e apresentando números de telefones com Javascript e Ruby on Rails"
date: 2015-06-01 23:29:12
categories: Ruby on Rails, Javascript, JQuery, Rails
tags: javascript, jquery, ruby, rails, helpers

---

Me bati um pouco ao procurar uma forma simples e elegante de mostrar números de
telefones no formato brasileiro. Então, deixo aqui dica rápida em como apresentar
números de telefones brasileiros em projetos **Rails**

De imediato, encontrei um **helper** do Rails com a função [number-to-phone][1], mas
confesso que não encontrei uma forma de usá-lo e formatá-lo aos padrões brasileiros.

Assim, fui procurar outra solução.

Lembrando que para os exemplos abaixo, considerei
armazenar o número de telefone no banco como uma **String** que contem somente números,
ou seja, não persisto valores como parênteses e espaços em brancos.


### COM formulários

Trabalhando com formulários, a dica é bem simples: utilizar a função **mask()**
passando como parâmetros o formato desejado

Em seu arquivo **.js**:

```js
  $("#phone-number").mask("(99) 9999?9-9999");
```

Repare que a máscara já valida números com 8 ou 9 dígitos para um *input* identificado como *#phone-number*.

Aqui usamos somente **javascript**! :)


### SEM formulários

Agora, quando quis renderizar um telefone sem a presença de campos *inputs* e formulários, simplesmente não consegui aplicar a função javascript acima em *tags* HTML.

Assim, podemos utilizar outro código em **javascript** para refazer a visualização do valor do telefone, como por exemplo:

```js
$('.phone-number').text(function(i, text) {
  if (text.length == 10){
    return text.replace(/(\d{2})(\d{4})(\d{4})/, '($1) $2-$3');
  }
  else{
    return text.replace(/(\d{2})(\d{5})(\d{4})/, '($1) $2-$3');
  }
});
```

Repare que já verificamos se o campo com o valor de telefone possue 8 ou 9 dígitos e arrumamos no formato desejado.


### Usando Rails Helpers

E para finalizar e arrumar um pouco o código, pode-se criar uma função e adicioná-la nos **helpers**.

Como exemplo: Temos um *model* **Person** e o atributo *phone_number*.

Em *people_helper.rb*:

```ruby
  def phone_format number
    if !number.nil?
      raw "<span class='phone-number'>#{number}</span>"
    end
  end
```

E em nossas *views* referentes, basta chamar assim:

```ruby
<%= phone_format @person.phone_number %>  
```

[1]: http://api.rubyonrails.org/classes/ActionView/Helpers/NumberHelper.html#method-i-number_to_phone
