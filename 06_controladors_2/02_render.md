!SLIDE
# Renderitzant respostes

!SLIDE subsection bullets incremental
# Renderitzant respostes

Des del punt de vista d'un controlador, existeixen **3 maneres** de generar
una resposta HTTP en rails.

* Utilitzar el mètode `render` per a renderitzar una vista.
* Utilizar el mètode `redirect_to` per a enviar un codi de redirecció HTTP.
* Cridar el mètode `head` per generar una resposta consistent en només
les capçaleres.

!SLIDE subsection bullets incremental
# `render`
### Mitjançant la comanda `render` podem

* Renderitzar vistes inclús d'altres accions.
* Renderitzar arxius.
* Renderitzar text arbitrari o formats pròpis.

!SLIDE subsection
# Renderitzar: Vistes

    @@@ ruby
    render :edit
    render :action => :edit
    render 'edit'
    render 'edit.html.erb'
    render :action => 'edit'
    render :action => 'edit.html.erb'
    render 'books/edit'
    render 'books/edit.html.erb'

!SLIDE subsection
# Renderitzar: Arxius

    @@@ ruby
    render :file => "{Rails.root}/views/books/edit"
    render :file => "{Rails.root}/public/400.html"

!SLIDE subsection
# Renderitzar: Text o formats

    @@@ ruby
    render :text => "OK"
    render :json => @product
    render :xml => @product
    render :js => "alert('Hello Rails');"

    # també no res
    render :nothing => true

!SLIDE subsection
# `render`
## Opcions comuns
### `:content_type, :layout, :status`

!SLIDE subsection
# `render :content_type`

Podem necessitar modificar el `Content-Type` generat per defecte des del
nostre controlador (per defect text/html).

    @@@ ruby
    render :file => arxiu, :content_type => "application/pdf"

!SLIDE subsection
# `render :layout`

Sense aquesta opció, render utilitzar el "layout" que estigui definit
en el controlador en curs o el general (application).

Si volem forçar-lo puntualment:

    @@@ ruby
    render :layout => 'especial'

O no utilizar cap layout:

    @@@ ruby
    render :layout => false

!SLIDE subsection
# `render :status`

La opció `:status` ens permet modificar el codi d'estat de la resposta HTTP.

    @@@ ruby
    render :status => 500
    render :status => :forbidden

!SLIDE subsection bullets incremental
# `redirect_to`

* Com hem vist `render` diu a Rails quina vista (o arxiu) s'ha d'utilizar per
a construir una resposta.

* `redirect_to` diu al navegador que ha de "redirigir" a una URL diferenta.

!SLIDE subsection
# `redirect_to`

    @@@ ruby
    redirect_to photos_path

    redirect_to :back

Podem també especificar el codi HTTP que correspon a la redirecció.

    @@@ ruby
    redirect_to photos_path, :status => 301

!SLIDE subsection bullets incremental
# `head`

* El mètode `head` pot utilitzar-se per enviar respostes només amb capçaleres
HTTP (sense cos).
* Alternativa més adequada a `render :nothing`.
* Només accepta un paràmetre que s'interpreta com un hash de capçaleres HTTP
amb els seus valors.

!SLIDE subsection
# `head`

Exemple

    @@@ ruby
    head :bad_request
    # HTTP/1.1 400 Bad Request
    # Connection: close
    ...

    head :created, :location => photo_path(@photo)
    # HTTP/1.1 201 Created
    # Connection: close
    # ...
    # Location: /photos/1
    # ...
