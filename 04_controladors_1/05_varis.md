!SLIDE subsection bullets
# Paràmetres

* Els paràmetres ens arriben al controlador dins del hash `params`.
* En els missatges de de `log` de la comanda `rails server` podem
observar-los (depurar)

!SLIDE subsection bullets small
# Render / Redirect

* Cada acció **ha** de renderitzar una vista (o text) o redirigir
a alguna altra acció.

* Per defecte Rails anirà a buscar la vista amb el mateix nom que
l'acció en execució.

Exemple:

    @@@ ruby
    render :action => "edit"
    # renderitza la vista corresponen
    # a l'acció 'edit'

    redirect_to(articles_url)
    # redirigeix a /articles

!SLIDE subsection bullets incremental
# Formats de resposta

* Rails pot generar respostes en altres formats a part d'HTML.
* Els controladors pre-generats per `scaffold` inclouen respostes
en format XML.
* Altres exemples de formats inclouen Javascript i JSON.

!SLIDE subsection bullets
# El Flash

* Representa missatges que només viuen (o són vàlids) per una petició.
* Habitualment es defineixen en un redirect per indicar un canvi d'estat en
l'aplicació.

Exemple:

    @@@ ruby
    # ArticlesController.update
    redirect_to @article, :notice => 'Actualitzat OK.'
