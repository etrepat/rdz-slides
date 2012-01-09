!SLIDE
![Rails logo](/file/assets/images/rails.png)
# Rails desde Zero

!SLIDE subsection
![Rails logo](/file/assets/images/rails.png)
# Rails desde Zero
##  Aplicació en 5 minuts

!SLIDE subsection
# Aplicació en 5 minuts

Tot seguit prepararem una petita aplicació per a gestionar llistes
de tasques.

!SLIDE subsection
# 1

Creem una nova aplicació Rails i ens situem en el seu directori

    @@@ sh
    $ rails new todos
    ...
    $ cd todos

!SLIDE subsection
# 2

Generem un "scaffold" (model, vista i controlador) per a generar ràpidament
el codi necessari per a una senzilla llista de tasques

    @@@ sh small
    $ rails g scaffold todo name:string due_on:date completed:boolean
    ...

!SLIDE subsection
# 3

Executem la migració de la base de dades

    @@@ sh
    $ bundle exec rake db:migrate

!SLIDE subsection
# 4

Llancem el servidor i ens dirigim a: [http://localhost:3000/todos](http://localhost:3000/todos)

    @@@ sh
    $ rails s

!SLIDE subsection
# i 5.
