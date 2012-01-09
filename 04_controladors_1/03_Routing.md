!SLIDE
# Routing
## Conectant URL's al codi
### (Introducció)

!SLIDE
# Routing

Quan una aplicació Rails rep una petició com la següent:

    @@@ sh
    GET /patients/17

Demana al "router" que ho enllaci amb una acció d'un controlador. Si la
primera que coincideix és:

    @@@ ruby
    match "/patients/:id" => "patients#show"

Aquesta petició es dirigeix a l'acció `show` del controlador `patients` amb
els paràmetres: `{:id => "17"}`

!SLIDE subsection
# Routing
### Rutes de recurs

Una ruta de *recurs* direcciona un nombre de peticions predefinit a
accions en un controlador

`config/routes.rb`

    @@@ ruby
    Sample::Application.routes.draw do
      resources :articles
      # Ens crea les rutes corresponents
      # a les accions:
      # index, create, new, edit,
      # update, destroy
    end

!SLIDE subsection
# Routing
## Comprobant rutes

### `rake routes`

    @@@ sh small
    $ rake routes
        articles GET    /articles(.:format)          {:action => "index", :controller => ...}
                 POST   /articles(.:format)          {:action => "create", :controller => ...}
     new_article GET    /articles/new(.:format)      {:action => "new", :controller => ...}
    edit_article GET    /articles/:id/edit(.:format) {:action => "edit", :controller => ...}
         article GET    /articles/:id(.:format)      {:action => "show", :controller => ...}
                 PUT    /articles/:id(.:format)      {:action => "update", :controller => ...}
                 DELETE /articles/:id(.:format)      {:action => "destroy", :controller => ...}

!SLIDE subsection
# Routing
### Recursos anidats

Útil si un recurs pertany a un altre, per exemple en models que estàn relacionats
1-N amb `has_many` i `belongs_to`.

Exemple:

    @@@ ruby
    # config/routes.rb
    resources :articles do
      resources :comentaris
    end

!SLIDE subsection
# Routing
### Restringint recursos

Podem registrir les accions associades a un recurs amb `only` i `except`.

Exemple:

    @@@ ruby
    # config/routes.rb
    resources :articles, :except => :show do
      resources :comentaris, :only => :create
    end

!SLIDE subsection
# Routing
### Mètodes d'ajuda

Al definir una ruta de recurs, automàticament tindrem accessibles desde
l'aplicació tot un seguit de mètodes d'ajuda per a referenciar-les i
utilitzar-les.

Són de la forma: `(nom_recurs)_path` i `(nom_recurs)_url`

!SLIDE subsection
# Routing
### Mètodes d'ajuda

Utilitzant l'exemple anterior:

    @@@ ruby
    # config/routes.rb
    Sample::Application.routes.draw do
      resources :articles
    end

!SLIDE subsection
# Routing
### Mètodes d'ajuda

Ens generaria els mètodes d'ajuda següents:

    @@@ ruby
    articles_path           articles_url
    new_article_path        new_article_url
    edit_article_path(id)   edit_article_url(id)
    article_path(id)        post_url(id)

La diferencia entre els mètodes `_path` i els `_url` és que l'últim
retorna el path prefixat amb el host/port.

!SLIDE subsection
# Routing
### Rutes pròpies

En Rails podem definir rutes pròpies en comptes d'utilitzar les generades
per un recurs ("Non-Resourceful routes").

Exemples:

    @@@ ruby
    match 'photos/:id' => 'photos#show'
    # /photos/12 => PhotosController.show
    match 'login' => 'user_sessions#new'
    # /login => UserSessionsController.new
    match 'logout' => 'user_sessions#destroy'
    # /logout => UserSessionsController.destroy

!SLIDE subsection
# Routing
### Rutes pròpies (amb nom)

També podem assignar noms o identificadors a les rutes per a referènciar-les
per mitjà de mètodes d'ajuda en l'aplicació.

    @@@ ruby
    match 'login' => 'user_sessions#new', :as => :signin

L'anterior ens crearà els mètodes d'ajuda: `signing_path` i `signin_url`. Per
exemple, cridar `signin_path` ens retornaria `"/login"`.

!SLIDE subsection bullets incremental
# Routing
### La ruta "arrel" (root route)

* La ruta "arrel" defineix l'arrel de l'aplicació o plana web.
* S'ha d'eliminar l'arxiu: `public/index.html`.
* S'estableix dins de `config/routes.rb` amb la sintaxi:
  `root :to => "articles#index"`.
