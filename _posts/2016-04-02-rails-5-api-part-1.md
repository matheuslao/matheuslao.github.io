---
layout: post
title: "Rails 5 API - App Exemplo - parte 1"
date: 2016-04-02 13:50:53
categories: rails, api, tutoriais
tags: rails, rails 5, api, restful, tutoriais, postman, curl

---

Olá!

Como o próprio título do post diz, pretendo fazer uma aplicação-exemplo para estudo de como desenvolver uma API utilizando Rails 5 (em *beta_3* no momento que escrevo este post) e consumir os dados em uma app desenvolvida com tecnologias _frontend_.

Até agora não sei que tecnologia/framework _javascript_ irei utilizar neste tutorial, ficando aberto à sugestões.

Nossa aplicação será um simples Gerenciador de Notas chamado **notes-api**


## Criando o projeto em modo API

A quinta versão de nosso amado framework incorporou uma famosa gem para desenvolvimento de APIs com Rails: [rails-api][rails_api].

Enquanto o Rails 5 não entra em sua versão estável, instale com:

    gem install rails --pre

E crie o projeto api com rails :

    rails new <nome_projeto> --api

sendo no nosso caso:

    rails new notes-api --api


##  Algumas diferenças do modo API

Se você já tem experiência com Rails, perceberá a diferença na estrutura do projeto em relação a uma aplicação rails "normal".

Caso contrário, basta saber que no modo api, o Rails apenas adiciona no projeto recursos necessários para o funcionamento de uma aplicação no backend, sem a necessidade da camada de apresentação como *assets* css, javascripts, jquery, configurações de sessões, cookies, etc.

Mas como curiosidade, visualize que o controlador principal de nossa aplicação herda diferente do convencional:

```ruby
class ApplicationController < ActionController::API
end
```

E verifique que o projeto foi configurado para funcionar somente no modo API no arquivo **config/application.rb**

```ruby
module NotesApi
  class Application < Rails::Application
    config.api_only = true
  end
end
```

## Scaffold para API

Como nossa aplicação é apenas para estudo, uma maneira rápida de criar uma estrutura completa de **CRUD** no Rails é utilizando o gerador conhecido como *scaffold*.

Não entrarei em detalhes explicando o motivo de utilizar um *scaffold* somente para estudo e não em ambiente de produção real, ok? Mas fica a dica para pesquisa.

No terminal, use o comando Rails conhecido e sem diferenças:

    rails g scaffold note title description:text

Perceba que ele não cria *views*, uma vez que estamos em modo API. Além disso, observe os métodos do *notes_controller* criados e veja que ele responde em formato *json*

```ruby
if @note.save
  render json: @note, status: :created, location: @note
else
  render json: @note.errors, status: :unprocessable_entity
end
```

Lembre-se de rodar a *migration* criada:

    rails db:migrate

E iniciar o server para verificar a aplicação funcionando:

    rails s

## Testando a API

Você pode testar as requisições para a API com a ferramenta que achar melhor.

Se domina ou curte fazer pelo terminal, utilize o [curl][curl-url]. A chamada mais básica, seria a requisição GET para nosso método *index* visualizando os cabeçalhos com:

    curl -i http://localhost:3000/notes

E uma requisição POST para criação de uma nova nota com um comando assim:

    curl -X POST -H "Cache-Control: no-cache" -H "Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW" -F "note[title]=titulo da nota" -F "note[description]=descrição da nota" "http://localhost:3000/notes"


Se deseja uma interface gráfica, recomendo o [postman][postman-url] que possue um *plugin* para o *Google Chrome* e um aplicativo para usuários Mac.


## Próximos Passos

Nos próximos posts da série, tentarei aplicar funcionalidades de serialização, autenticação, proteção/configuração para requisições e o que mais for interessante.

Até!







[rails_api]:(https://github.com/rails-api/rails-api)
[curl-url]:(https://curl.haxx.se)
[postman-url]:(https://www.getpostman.com)
