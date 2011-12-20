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

!SLIDE subsection incremental
# `yield`

* En un layout, la sentència `yield` identifica on el contingut d'una vista
ha de ser introduït.

* Podem tenir més d'una sentencia `yield` per layout especificant-li un nom per
mitjà d'un símbol.
  * p.ex: `<%= yield :head %>`

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
