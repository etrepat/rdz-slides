!SLIDE subsection
# Models
## Consultes

!SLIDE subsection bullets incremental
# Consultes

* El mòdul ActiveRecord de Rails ens evitarà, en la majoria de casos, tenir
que utilizar sentències SQL per a extreure informació de la BD.

* Tots els mètodes de consulta de Rails >= 3 executen la sentència SQL corresponent
**només** quan s'accedeix a la col.lecció que retornen ("lazy loading").

!SLIDE subsection bullets incremental
# Consultes
## Mètodes

Els mètodes de consultas en rails són els següents:

`
where,
order,
select,
limit,
offset,
group,
having,
joins
`

Tots aquests mètodes retornen una instància d'`ActiveRecord::Relation`.

A més, tots aquests mètodes són encadenables.

!SLIDE subsection
# `where`

    @@@ ruby
    Client.where("comandes = ?", params[:comandes])

    Client.where("comandes = ? AND pendent = ?",
      params[:comandes], false)

    Client.where("created_at >= :start_date",
      {:start_date => data_inici})

Es reemplaçaran els interrogantss pels valors de les variables proporcionades.

En l'últim exemple es reemplacen per nom amb els valors del hash que identifica
la clau amb el nom coincident.

!SLIDE subsection
# `where`

En comptes de passar-hi un `String` podem passar un `Hash`

    @@@ ruby
    Client.where(:actiu => true)

    Client.where(:created_at =>
      (Time.now.midnight - 1.day)..Time.now.midnight)

    Client.where(:no_comandes => [1,3,5])

Només soporta condicions d'igualtat, rang i subconjunt

!SLIDE subsection
# `order`

Ordenar els resultats

    @@@ ruby
    Client.order("created_at")

    # podem especificar ASC o DESC
    Client.order("created_at ASC")
    Client.order("created_at DESC")

    # i més d'un camp
    Client.order("comandes_pendents ASC, created_at DESC")


!SLIDE subsection
# `select`

Limitar els camps que retorna una consulta que per defecte s'executa
amb `SELECT *`

    @@@ ruby
    Client.select("nom, empresa, actiu")

    # La sentencia SQL:
    # SELECT nom, empresa, actiu FROM clients

Si s'utilitza `select` el resultat es de només lectura (no es pot guardar
les modificacions ni esborrar).

S'ha d'anar en compte doncs només emplenarà els atributs del model
que seleccionem.

!SLIDE subsection
# `limit` / `offset`

Es pot utilitzar `limit` per especificar el nombre de registres que es retornen
i `offset` per saltar-ne una quantitat desde l'inici.

    @@@ ruby
    Client.limit(5)
    # SQL: SELECT * FROM clients LIMIT 5

    Client.limit(5).offset(30)
    # SQL: SELECT * FROM clients LIMIT 5 OFFSET 30

!SLIDE subsection
# `group`

Especificar una clausula `GROUP BY`

    @@@ ruby small
    Comanda.select("created_at as data_creacio, sum(import) as import_total").group("created_at")

    # SQL
    # SELECT created_at as data_creacio, sum(import) as import_total
    # FROM comandes
    # GROUP BY created_at

!SLIDE subsection
# `having`

Clausula `HAVING`

    @@@ ruby small
    Comanda.select("created_at as data_creacio, sum(import) as import_total").group("created_at")
    .having("sum(import) > ?", 100)

    # SQL:
    # SELECT created_at as data_creacio, sum(import) as import_total
    # FROM comandes
    # GROUP BY created_at
    # HAVING sum(import) > 100

!SLIDE subsection
# `joins`

`joins` ens permet especificar clausules `JOIN` en la consulta resultant.

    @@@ ruby small
    Client.joins('LEFT JOIN adreces on adreces.client_id = clients.id')

    # Produeix en SQL:
    # SELECT clients.*
    # FROM clients
    # LEFT JOIN adreces ON adreces.client_id = clients.id

També podem utilitzar un Array/Hash d'associacions ja definides

**Només** ens permet crear clausules `INNER JOIN`

    @@@ ruby small
    Categoria.joins(:articles)

    # SELECT categories.* FROM categories
    # INNER JOIN articles ON articles.categoria_id = categories.id

!SLIDE subsection
# `joins`

  Considerem el següent exemple amb els models `Categoria`, `Article`,
  `Comentari`, `Usuari` i `Tag`

    @@@ ruby small
    class Categoria < ActiveRecord::Base
      has_many :articles
    end

    class Article < ActiveRecord::Base
      belongs_to :categoria
      has_many :comentaris
      has_many :tags
    end

    class Comentari < ActiveRecord::Base
      belongs_to :article
      has_one :usuari
    end

    class Usuari < ActiveRecord::Base
      belongs_to :comentari
    end

    class Tag < ActiveRecord::Base
      belongs_to :article
    end

!SLIDE subsection
# `joins`
### Join simple

    @@@ ruby
    Categoria.joins(:articles)

Produeix

    @@@ sql
    SELECT categories.* FROM categories
    INNER JOIN articles
      ON articles.categoria_id = categories.id

*Retorna'm les categories que tinguin articles*

Nota: Retornarà duplicats si hi ha més d'un article en la mateixa categoria, podem
evitar-ho: `Categoria.joins(:articles).select("distinct(categories.id)")`

!SLIDE subsection
# `joins`
### Join múltiple

    @@@ ruby
    Article.joins(:categoria, :comentaris)

Produeix

    @@@ sql
    SELECT articles.* FROM articles
    INNER JOIN categories
      ON articles.categoria_id = categories.id
    INNER JOIN comentaris
      ON comentaris.article_id = article.id

*Retorna'm els articles que estan categoritzats i tenen almenys 1 comentari*

!SLIDE subsection
# `joins`
### Join anidat (nivell 1)

    @@@ ruby
    Article.joins(:comentaris => :usuaris)

Produeix

    @@@ sql
    SELECT articles.* FROM articles
    INNER JOIN comentaris
      ON comentaris.article_id = articles.id
    INNER JOIN usuaris
      ON usuaris.comentari_id = comentaris.id

*Retorna'm els articles comentats per un usuari registrat*

!SLIDE subsection
# `joins`
### Join anidat (múltiples nivells)

    @@@ ruby
    Categoria.jons(:articles => [{:comentaris => :usuari}, :tags])

Produeix

    @@@ sql
    SELECT categories.* FROM categories
    INNER JOIN articles
      ON articles.categoria_id = categories.id
    INNER JOIN comentaris
      ON comentaris.article_id = articles.id
    INNER JOIN usuaris
      ON usuaris.comentari_id = comentaris.id
    INNER JOIN tags
      ON tags.article_id = articles.id

!SLIDE subsection
# `joins`

Podem especificar opcions en clausules `join` encadenant el mètode
`where`

    @@@ ruby
    ahir = Time.now.midnight - 1.day
    Client.joins(:comandes).where('orders.created_at >= ?',
      ahir)

!SLIDE subsection
# El problema de les N+1 consultes

!SLIDE subsection
# N+1 consultes

Considerem el seguent exemple que ens busca 10 clients i imprimeix
el seu codi postal

    @@@ ruby
    clients = Client.limit(10)

    clients.each do |client|
      puts client.dades_enviament.cp
    end

!SLIDE subsection bullets incremental
# N+1 consultes

* El codi anterior es correcte però inòptim.
* Executa 1 consulta (per trobar els 10 clients) i després 10 (per carregar
el model `dades_enviament` i extreure'n el codi postal)
* <font color="red">**11**</font> consultes!

!SLIDE subsection bullets incremental
# N+1 consultes
## Sol.lució

* Utilitzar el mètode `includes`
* `includes` permet a Rails conèixer quines associacions ha de carregar i
utilitzar el mínim nombre de consultes possible
* "Eager loading" ó pre-càrrega

!SLIDE subsection bullets incremental
# N+1 consultes

Reescrivint el exemple anterior

    @@@ ruby
    clients = Client.includes(:dades_enviament).limit(10)

    clients.each do |client|
      puts client.dades_enviament.cp
    end

* Executa 1 consulta (per trobar els 10 clients) i 1 altra consulta
per a trobar totes les adreces.

* <font color="green">**2**</font> consultes

!SLIDE subsection
# N+1 consultes

En rails

    @@@ ruby
    clients = Client.includes(:dades_enviament).limit(10)

    clients.each do |client|
      puts client.dades_enviament.cp
    end

En SQL

    @@@ sql
    SELECT * FROM clients LIMIT 10
    SELECT dades_enviament.*
    FROM dades_enviament
    WHERE (dades_enviament.client_id IN (1,2,3,4,5,6,7,8,9,10))
