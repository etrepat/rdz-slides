!SLIDE
# Layouts
### La base HTML per a la web

!SLIDE subsection bullets incremental small
# Layouts
## Layout d'aplicació

* Es troba a `app/views/layouts/application.html.erb`.
* Conté l'HTML bàsic per a la nostra web.
* Enllaça les fulles d'estil
* Inclou els fitxers javascript.

!SLIDE subsection
# Layout d'aplicació

    @@@ html
    <!DOCTYPE html>
    <html>
    <head>
      <title>Titol</title>
      <%= stylesheet_link_tag    "application" %>
      <%= javascript_include_tag "application" %>
      <%= csrf_meta_tags %>
    </head>
    <body>

    <%= yield %>

    </body>
    </html>

!SLIDE subsection bullets incremental
# Layouts
## Utilitzant layouts

* En Rails podem en tot moment especificar el layout a utilitzar per mitjà
de la sentència `layout`.
* Els layouts sempre són compartits en la cadena jeràrquica i sempre
substitueixin els més generals.

!SLIDE subsection
# Especificar un layout

Per especificar un layout diferent en un controlador, podem:

    @@@ ruby
    class ProductsController < ApplicationController
      layout "inventory"
      #...
    end

En aquest càs, les vistes corresponents a `ProductsController` utilitzarant
el layout `app/views/layouts/inventory.html.erb`.

!SLIDE subsection
# Especificar un layout

Podem també utilizar un mètode per definir quin layout utilitzar:

    @@@ ruby
    class ApplicationController < ActionController::Base
      ...
      layout :layout_by_resource

      private

      def layout_by_resource
        if devise_controller?
          'sign'
        else
          'application'
        end
      end
      ...
    end

En aquest cas, si estem utilitzan `devise`, renderitzarem el layout `sign`.

!SLIDE subsection incremental
# `yield`

* En un layout, la sentència `yield` identifica on el contingut d'una vista
ha de ser introduït.

* Podem tenir més d'una sentencia `yield` per layout especificant-li un nom per
mitjà d'un símbol.
  * p.ex: `<%= yield :head %>`

!SLIDE subsection
# `yield`

Un sol bloc `yield`

    @@@ html
    <html>
      <head></head>
      <body>
        <%= yield %>
      </body>
    </html>

Varis

    @@@ html
    <html>
      <head><%= yield :head %></head>
      <body>
        <%= yield %>
      </body>
    </html>

!SLIDE subsection
# `content_for`

La sentencia `content_for` denota el contingut que correspon a un block `yield`
amb nom.

Ex:

    @@@ ruby
    <% content_for(:head) do %>
    ...
    <% end %>

!SLIDE subsection small
# `yield/content_for`
### Exemple

    @@@ html
    <!-- app/views/layouts/application.html.erb -->
    <!DOCTYPE html>
    <html>
      <head>
        <title>
          <%= content_for?(:title) ? yield(:title) : 'Untitled' %>
        </title>
        <%= stylesheet_link_tag 'application' %>
        <%= csrf_meta_tag %>
      </head>
      <body>
        <%= javascript_include_tag 'application' %>
        <%= yield(:foot) %>
      </body>
    </html>

!SLIDE subsection small
# `yield/content_for`
### Exemple

    @@@ html
    <!-- app/views/home/index.html.erb -->
    <% content_for(:title) { "Inici - Benvinguts!" } %>
    <% content_for(:foot) do %>
      <%= javascript_include_tag 'home' %>
    <% end %>

    <h1>Benvigut visitant!</h1>

    ...

!SLIDE subsection smaller
# `yield/content_for`

També ho podem fer servir per definir-nos mètodes d'ajuda si ens convé

    @@@ ruby
    # helper :layout
    module LayoutHelper
      def title(page_title, show_title = true)
        content_for(:title) { h(page_title.to_s) }
        @show_title = show_title
      end

      def show_title?
        @show_title
      end

      def set_updated_at(timestamp)
        content_for(:updated_at) { h(timestamp.strftime('%d/%m/%Y %H:%M')) }
      end

      def stylesheet(*args)
        content_for(:head) { stylesheet_link_tag(*args) }
      end

      def javascript(*args)
        content_for(:foot) { javascript_include_tag(*args) }
      end
    end
