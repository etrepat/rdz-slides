!SLIDE subsection
# Models
## Càlculs

!SLIDE subsection bullets incremental
# Càlculs

* `ActiveRecord` ens proporciona algunes funcions senzilles per a realitzar
càlculs en les col.leccions que ens retorna.
* Les funcions principals de càlcul són: `count, average, minimum, maximum,
i sum`.
* Retornen un valor segons el tipus de dades de la columna en la que treballen
o `nil` si no hi ha resultats.

!SLIDE subsection
# Càlculs

Tots els mètodes de càlcul treballen directament en el model:

    @@@ ruby
    Client.count
    # SELECT count(*) AS count_all FROM clients

ó sobre una relació:

    @@@ ruby
    Client.where(:primer_cognom => "Trepat").count

!SLIDE subsection
# Càlculs
## Exemples

!SLIDE subsection
# `count`

Compta el nº de registres retornats.

    @@@ ruby
    Client.includes("comandes")
    .where(:primer_cognom => 'Trepat',
      :comandes => {:estat => 'pendent'}).count

!SLIDE subsection
# `average`

Executa una mitja aritmètica: suma(N) / N

    @@@ ruby
    Comandes.average("import_total")

!SLIDE subsection
# `minimum`

Retorna el registre amb el **mínim** valor del camp especificat.

    @@@ ruby
    Client.minimum("edat")

!SLIDE subsection
# `maximum`

Retorna el registre amb el **màxim** valor del camp especificat.

    @@@ ruby
    Client.maximum("edat")

!SLIDE subsection
# `sum`

Retorna la suma dels valors de la columna especificada.

    @@@ ruby
    Client.where(:primer_cognom => "Trepat")
    .sum("no_comandes")
