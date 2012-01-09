!SLIDE
# Cookies

!SLIDE subsection bullets incremental
# Cookies

* Les nostres aplicacions poden enmagatzemar petites quantitats de dades
per al client (anomenades cookies) que serán persistides entre *requests* i
inclús sessions.

* Podem accedir a les cookies per mitjà del mètode `cookies`.

* Igual que amb els paràmetres o sessions, funciona com un `Hash`.

!SLIDE subsection
# Cookies

Establir/modificar i llegir una cookie

    @@@ ruby
    cookies[:idioma] = I18n.locale

    puts cookies[:idioma]
    => 'es'

Eliminar una cookie

    @@@ ruby
    # Eliminar una cookie
    cookies.delete(:idioma)

A diferencia que amb les sessions, on les eliminàvem assignant `nil`, per eliminar
el valor d'una cookie hem d'utilitzar `cookies.delete(:key)`.
