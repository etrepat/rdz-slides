!SLIDE
# Formularis
### Obtenir dades dels usuaris

!SLIDE subsection bullets incremental
# Formularis
### En Rails tenim 2 maneres principals de generar formularis en una vista

* `form_for`
* `form_tag`

!SLIDE subsection bullets incremental
# `form_for`

* El bloc `form_for` s'utilitza per a crear un formulari *associat* a un
mòdel (entitat o recurs).

* Dins d'aquest bloc tenim accés a mètodes per construir els controls
del formulari.

* Per exemple, `f.text_field :title` indica a Rails que ha de generar
una caixa de text i "conectarla" a l'atribut `title` del model referenciat
pel formulari.

!SLIDE subsection
# `form_for`
### Exemple

    @@@ html
    <%= form_for @article do |f| %>
      <%= f.text_field :title %>
      <%= f.text_area :body, :size => "60x12" %>
      <%= f.submit "Create" %>
    <% end %>

!SLIDE subsection
# `form_for`
### Algunes opcions comuns

    @@@ ruby
    # Crear un nou article
    form_for(@article, :url => articles_path)
    form_for(@article)
    # utilizar atributs d'estil
    form_for(@article, :html => {:class => 'nice_form'})

    ## Editar un article
    form_for(@article, :url => article_path(@article),
      :html => { :method => "put" })
    form_for(@article)

!SLIDE subsection small
# `form_for`
### Utilitzant més d'un recurs (anidats)

    @@@ ruby
    <h3>Afegir un comentari</h3>
    <%= form_for([@article, @article.comentaris.build]) do |f| %>
      <div class="field">
        <p><%= f.label :text %></p>
        <p><%= f.text_area :text %></p>
      </div>
      div class="actions">
        <%= f.submit %>
      </div>
    <% end %>

!SLIDE subsection
# `form_for`
### Form Helpers

    @@@ ruby
    label
    text_field
    text_area
    check_box
    file_field
    password_field
    ...

Podem veure'n la llista complerta a:
[http://api.rubyonrails.org/classes/ActionView/Helpers/FormHelper.html](http://api.rubyonrails.org/classes/ActionView/Helpers/FormHelper.html)

!SLIDE subsection bullets incremental
# `form_tag`

* El bloc `form_tag` s'utilitza per a generar un formulari que no està
*associat* a un model.

* Els "helpers" o mètodes que s'utilitzen dins d'un bloc `form_tag`
acaben amb `_tag`. P.ex: `label_tag` i `text_field_tag`.

!SLIDE subsection
# `form_tag`
### Exemple

    @@@ html
    <%= form_tag("/search", :method => "get") do %>
      <%= label_tag(:q, "Search for:") %>
      <%= text_field_tag(:q) %>
      <%= submit_tag("Search") %>
    <% end %>

!SLIDE subsection
# `form_tag`
### Algunes opcions comuns

    @@@ ruby
    form_tag({:controller => "people", :action => "search"},
      :method => "get", :class => "nice_form")

!SLIDE subsection
# `form_tag`
### Exemple

    @@@ html
    <%= form_tag({:action => :upload},
        :multipart => true) do %>
      <%= file_field_tag 'picture' %>
    <% end %>

!SLIDE subsection
# `form_tag`
### Form Helpers

    @@@ ruby
    <%= label_tag(:pet_dog, "I own a dog") %>
    <%= text_field_tag(:name, "John") %>
    <%= text_area_tag(:message, "Hi, nice site", :size => "24x6") %>
    <%= hidden_field_tag(:parent_id, "5") %>
    <%= password_field_tag(:password) %>
    <%= check_box_tag(:pet_dog) %>
    <%= radio_button_tag(:age, "child") %>
    ...

Podem veure'n la llista complerta a:
[http://api.rubyonrails.org/classes/ActionView/Helpers/FormTagHelper.html](http://api.rubyonrails.org/classes/ActionView/Helpers/FormTagHelper.html)
