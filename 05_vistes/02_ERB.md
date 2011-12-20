!SLIDE
# ERB
### Embedded Ruby

!SLIDE subsection incremental
# ERB

* ERB es el llenguatge de "template" per defecte en Rails.
  * Podem utilitzar d'altres instal.lant les gemes corresponents com: Haml,
  Liquid, Slim, etc.

* ERB ens permet incloure codi Ruby dins d'HTML.
  * Similar a ASP, JSP, PHP

* Els blocs de codi Ruby es delimiten per `<% %>`.

!SLIDE subsection
# ERB
## Exemples

Imprimir una variable

    @@@ ruby
    # Escriu el titol de l'article (ja escapat)
    <%= @article.titol %>

    # igual però no segur
    <%= raw @article.text %>

!SLIDE subsection
# ERB
## Exemples

Llistar un conjunt d'articles

    @@@ ruby
    # app/views/articles/index.html.erb
    <% @articles.each do |article| %>
      ...
    <% end %>

!SLIDE
# Helpers
### Simplificar vistes i evitar duplicació

!SLIDE subsection
# URL Helpers

Generar enllaços amb el mètode d'ajuda (helper) `link_to`:

    @@@ ruby
    link_to 'Mostra', article
    # => "/articles/17" (GET)

    link_to 'Edita', edit_article_path(article)
    # => "/articles/17/edit" (GET)

    link_to 'Elimina', article, :method => :delete,
      :confirm => 'Segur?'
    # => "/articles/17" (DELETE)

!SLIDE subsection
# Exemple

`LlibresController`

    @@@ ruby
    class LlibresController < ApplicationController
      def index
        @llibres = Llibre.all
      end
    end

`config/routes.rb`

    @@@ ruby
    resources :llibres

!SLIDE subsection smaller
# Exemple

`app/views/llibres/index.html.erb`

    @@@ html
    <h1>Llistat de llibres</h1>

    <table>
      <tr>
        <th>Titol</th>
        <th>Sumari</th>
        <th></th>
        <th></th>
        <th></th>
      </tr>
      <% @llibres.each do |llibre| %>
      <tr>
        <td><%= llibre.title %></td>
        <td><%= llibre.content %></td>
        <td><%= link_to 'Mostra', llibre %></td>
        <td><%= link_to 'Edita', edit_llibre_path(book) %></td>
        <td><%= link_to 'Elimina', book, :confirm => 'Segur?', :method => :delete %></td>
      </tr>
      <% end %>
    </table>

    <br />

    <%= link_to 'Nou llibre', new_llibre_path %>

!SLIDE subsection
# Altres mètodes d'ajuda
## Formateig de nombres

    @@@ ruby
    number_to_currency
    number_to_human
    number_to_percentage
    number_wtih_precision

!SLIDE subsection
# Altres mètodes d'ajuda
## "Assets"

    @@@ ruby
    javascript_include_tag
    stylesheet_link_tag
    image_tag
    video_tag
    audio_tag

!SLIDE subsection bullets incremental
# Creant mètodes d'ajuda

* Rails ens permet crear els nostres mètodes d'ajuda propis.
* Es situen a `app/helpers`
* Són mòduls on podem escriure les funcions que volem tenir disponibles a les
vistes.

!SLIDE subsection bullets incremental
# Creant mètodes d'ajuda
## Com?

* Aprofitar l'arxiu existent per defecte `app/helpers/application_helper.rb`
* Podem escriure nous arxius `_helper.rb` i carregar-los mitjançant el
mètode `helper`.

!SLIDE subsection
# Creant mètodes d'ajuda
## Com?

Modificar `ApplicationHelper`

    @@@ ruby
    # app/helpers/application_helper
    module ApplicationHelper
      def formateja_data(d)
        d.strftime("%B %e, %Y")
      end
    end

!SLIDE subsection
# Creant mètodes d'ajuda
## Com?

Creant nous arxius `_helper`:

    @@@ ruby
    # app/helpers/formats_helper
    module FormatsHelper
      def formateja_data(d)
        d.strftime("%B %e, %Y")
      end
    end

Després l'hem d'incloure en el controlador on el volem fer servir amb el
mètode `helper`

!SLIDE subsection
# Creat mètodes d'ajuda
## Com?

Fer els nostres mòduls d'ajuda accessibles

    @@@ ruby
    # app/controllers/home_controller.rb
    class HomeController < ApplicationController
      # incloure el helper de formats de data
      helper :formats
    end

!SLIDE subsection
# Creat mètodes d'ajuda
## Com?

Fer els nostres mòduls d'ajuda accessibles

    @@@ ruby
    # app/controllers/application_controller.rb
    class ApplicationController < ActionController::Base
      # incloure tots els helpers definits
      helper :all
    end
