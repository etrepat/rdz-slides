!SLIDE subsection
# Models
## (Named) Scopes

!SLIDE subsection bullets incremental
# Scopes

* Rails ens permet definir consultes "comuns" o que tenim previst utilitzar
frequentment i referenciarles com una crida a un mètode d'un model o associació.

* Un "scope" pot utilitzar qualsevol dels mètodes de consulta vistos fins
ara i encadenar-los.

* Retornen un objecte `ActiveRecord::Relation` que ens permetrà cridar
a altres mètodes de consulta o altres "scopes"

!SLIDE subsection
# Scopes

Definim un "scope" senzill

    @@@ ruby
    class Article < ActiveRecord::Base
      belongs_to :categoria

      scope :publicat, where(:publicat => true)
    end

Llavors podem:

    @@@ shell
    > Article.publicat # => articles publicats
    > categoria = Categoria.first
    > categoria.articles.publicat # => articles publicats

!SLIDE subsection
# Scopes
## Treballar amb dates

Degut a com s'evaluen les dates necessitem utilitzar una funció `lambda`

    @@@ ruby small
    class Article < ActiveRecord::Base
      scope :ultima_setmana, lambda { where("created_at < ?", Time.zone.now) }
    end

Sense la funció `lambda`, `Time.zone.now` només es cridaria un cop (el primer) i
necessitem que s'evalui cada vegada.

!SLIDE subsection
# Scopes
## `default_scope`

Si desitjem que un "scope" s'apliqui a totes les consultes d'un model,
podem utilitzar el mètode `default_scope` desde el model.

    @@@ ruby
    class Client < ActiveRecord::Base
      default_scope where("data_baixa IS NULL")
    end

!SLIDE subsection
# Scopes
## Mètodes estàtics

Podem pensar en els "scopes" com a mètodes estàtics del model en el que
es declaren, per tant podem definir-los també de la següent manera:

    @@@ ruby
    class Article < ActiveRecord::Base
      class << self
        def ultima_setmana
          where("created_at < ?", Time.zone.now)
        end
      end
    end

    > Article.ultima_setmana
