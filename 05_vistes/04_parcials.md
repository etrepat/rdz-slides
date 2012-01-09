!SLIDE
# Parcials
### Compartir codi entre pàgines

!SLIDE subsection bullets incremental
# Parcials

* Les parts que es *repeteixen* en una vista, habitualment es separen
en "parcials" (partials).

* Un "parcial" (partial) és un arxiu de vista (p, ex: .html.erb) que comença
per un guió baix. P.ex: `_form.html.erb`.

!SLIDE subsection
# Parcials
### Utilitzant parcials

Per a renderitzar un parcial com a part d'una vista s'utilitza el mètode
`render` desde la mateixa.

    @@@ html
    <%= render "menu" %>

Això renderitza l'arxiu `_menu.html.erb` del **mateix** directori que la
vista en execució. Per a utilitzar un parcial situat en un altra carpeta:

    @@@ html
    <%= render "shared/menu" %>

Aquest últim renderitzarà l'arxiu de `app/views/shared/_menu.html.erb`.

!SLIDE subsection
# Parcials
### Simplificar vistes

Els parcials s'utilitzen **principalment** per a simplificar vistes.

    @@@ html
    <%= render "shared/banner" %>

    <h1>Articles</h1>

    <p>Uns quants articles:</p>
    ...

    <%= render "shared/footer" %>

En aquest cas, `_banner.html.erb` i `_footer.html.erb` poden contenir contingut
que es pot "compartir" en diverses vistes.

!SLIDE subsection
# Parcials
### Layouts pròpis

Un parcial pot utilitzar el seu propi arxiu de layout. Per exemple:

    @@@ ruby
    <%= render :partial => "links", :layout => "link_bar" %>

Nota: L'arxiu de layout per un parcial també ha de començar per `_` i han
d'estar situats en la mateix carpeta que el parcial al que pertanyen (no a
la carpeta `app/views/layouts`).

S'ha d'especificar explícitament la clau `:partial` quan utilitzem altres
parametres com `:layout`.

!SLIDE subsection bullets
# Parcials
### Variables locals

* Podem passar variables als parcials per a fer-los més potents. Per exemple:

!SLIDE subsection smaller
# Parcials
### Variables locals

`new.html.erb`

    @@@ html
    <h1>Nou article</h1>
    <%= error_messages_for :article %>
    <%= render :partial => "form", :locals => { :article => @article } %>

`edit.html.erb`

    @@@ html
    <h1>Editar article</h1>
    <%= error_messages_for :article %>
    <%= render :partial => "form", :locals => { :article => @article } %>

`_form.html.erb`

    @@@ html
    <%= form_for(article) do |f| %>
      <p>
        <b>Nom de l'article</b><br />
        <%= f.text_field :nom %>
      </p>
      <p>
        <%= f.submit %>
      </p>
    <% end %>

!SLIDE subsection
# Parcials
### Variables locals

Cada parcial **ja** té definida automàticament una variable local amb el
mateix nom que el parcial (meny el guió baix). Podem assignar-li un valor
per mitjà de la opció `:object`:

    @@@ ruby
    <%= render :partial => "client", :object => @client %>

!SLIDE subsection
# Parcials
### Variables locals

Un mètode ràpid, alternatiu a l'anterior

    @@@ ruby
    <%= render @client %>

Suposant que la variable d'instància `@client` conté una instància del model
`Client`, es traduirà a:

    @@@ ruby
    <%= render :partial => "client", :object => @client %>

!SLIDE subsection
# Parcials
### Renderitzar col.leccions

Els parcials són molt útils per a renderitzar col.leccions. Per a fer-ho podem
utilizar la opció: `:collection`.

`index.html.erb`

    @@@ html
    <h1>Productes</h1>
    <%= render :partial => "product", :collection => @products %>

`_product.html.erb`

    @@@ html
    <p>Producte: <%= product.name %></p>

!SLIDE subsection
# Parcials
### Renderitzar col.leccions

En l'exemple anterior ens enstalviem de fer:

`index.html.erb`

    @@@ html
    <h1>Productes</h1>
    <% @products.each do |product| %>
      <%= render :partial => "product", :object => product %>
    <% end %>
