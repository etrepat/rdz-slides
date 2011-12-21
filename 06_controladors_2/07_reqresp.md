!SLIDE
# Request/Response

!SLIDE subsection bullets incremental
# Request/Response

### Rails ens proporciona 2 objectes `request` i `response` per a treballar tant amb la petició (request) com amb la resposta que hem de generar (response).

!SLIDE subsection
# `request`

L'objecte `request` conté tota la informació relativa a la petició que ens
arriba des del client.

Alguns mètodes de l'objecte `request` són:

    @@@ ruby
    request.host          # hostname
    request.get?          # és una peticio GET?
    request.post?         # és un POST?
    request.headers       # Hash amb les capçaleres
    request.query_string  # Paràmetres de la URL

La llista complerta de mètodes de l'objecte `request` la podem trobar a:
[http://api.rubyonrails.org/classes/ActionDispatch/Request.html](http://api.rubyonrails.org/classes/ActionDispatch/Request.html)

!SLIDE subsection
# `response`

L'objecte `response` ens permet modificar (per exemple, dins un `after_filter`) la
resposta que hem de generar al client.

Alguns mètodes de l'objecte `response` són:

    @@@ ruby
    response.body         # dades complertes
    response.status       # codi d'estat HTTP
    response.content_type # mime-type de la resposta
    response.charset      # codificació de caràcters
    response.headers      # Hash amb les capçaleres

Per exemple si volguèssim modificar alguna capçalera de la resposta HTTP:

    @@@ ruby
    response.headers["Content-Type"] = "application/pdf"
