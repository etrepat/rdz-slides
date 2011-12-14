!SLIDE subsection
# Models
## Associacions

!SLIDE subsection
# Associacions

En Rails, una associacó és una *connexió ó relació* ente dos models `ActiveRecord.

Rails soporta sis tipus d'associacions:

`
belongs_to,
has_one,
has_many,
has_many :through,
has_one :through,
has_and_belongs_to_many,
`

!SLIDE subsection
# `belongs_to`

![belongs_to](/file/assets/images/belongs_to.png)

Defineix una associació un-a-un amb un altre model o de pertinença

    @@@ ruby
    class Order < ActiveRecord::Base
      belongs_to :customer
    end

!SLIDE subsection
# `has_one`

![has_one](/file/assets/images/has_one.png)

També Defineix una associació un-a-un amb un altre model però amb diferent
significat. Cada instancia del model que defineix aquesta associacó conté una
instancia de l'altre.

    @@@ ruby
    class Supplier < ActiveRecord::Base
      has_one :account
    end

!SLIDE subsection
# `has_many`

![has_many](/file/assets/images/has_many.png)

Defineix una associació 1-a-N. Normalment en l'altre costat trobarem una
associació `belongs_to`.

    @@@ ruby
    class Customer < ActiveRecord::Base
      has_many :orders
    end

!SLIDE subsection
# `has_many :through`

![has_many_through](/file/assets/images/has_many_through.png)

Defineix una relació M-a-N amb un altre model **a través** d'un tercer
model.

!SLIDE subsection
# `has_many :through`

Defineix una relació M-a-N amb un altre model **a través** d'un tercer

    @@@ ruby
    class Physician < ActiveRecord::Base
      has_many :appointments
      has_many :patients, :through => :appointments
    end

    class Appointment < ActiveRecord::Base
      belongs_to :physician
      belongs_to :patient
    end

    class Patient < ActiveRecord::Base
      has_many :appointments
      has_many :physicians, :through => :appointments
    end

!SLIDE subsection
# `has_many :through`

També s'utilitza per definir "atajos" a través d'associacions `has_many`
anidades.

    @@@ ruby
    class Document < ActiveRecord::Base
      has_many :sections
      has_many :paragraphs, :through => :sections
    end

    class Section < ActiveRecord::Base
      belongs_to :document
      has_many :paragraphs
    end

    class Paragraph < ActiveRecord::Base
      belongs_to :section
    end

!SLIDE subsection
# `has_one :through`

Defineix una relació 1-a-1 amb un altre model **a través** d'un tercer

![has_one_through](/file/assets/images/has_one_through.png)

!SLIDE subsection
# `has_one :through`

Defineix una relació 1-a-1 amb un altre model **a través** d'un tercer

    @@@ ruby
    class Supplier < ActiveRecord::Base
      has_one :account
      has_one :account_history, :through => :account
    end

    class Account < ActiveRecord::Base
      belongs_to :supplier
      has_one :account_history
    end

    class AccountHistory < ActiveRecord::Base
      belongs_to :account
    end

!SLIDE
### `has_and_belongs_to_many`

Defineix una relació M-a-N entre *2 models*

![has_and_belongs_to_many](/file/assets/images/has_and_belongs_to_many.png)

!SLIDE
### `has_and_belongs_to_many`

Defineix una relació M-a-N entre *2 models*

    @@@ ruby
    class Assembly < ActiveRecord::Base
      has_and_belongs_to_many :parts
    end

    class Part < ActiveRecord::Base
      has_and_belongs_to_many :assemblies
    end

!SLIDE
### `has_and_belongs_to_many`

Ens hem d'enrecordar de crear la taula de "JOIN"

    @@@ ruby
    class CreateAssemblyPartJoinTable < ActiveRecord::Migration
      def change
        create_table :assemblies_parts, :id => false do |t|
          t.integer :assembly_id
          t.integer :part_id
        end
      end
    end

S'hauria de crear sense clau primaria

!SLIDE subsection bullets incremental
# Triar entre BT i HO?

* Per decidir si apliquem una relació 1-1 amb has_one o belongs_to hem de pensar
**on va la clau forànea**.

* On col.loquem la FK: `belongs_to`

* Forma part del disseny de la BD i del cas d'ús concret

!SLIDE subsection
# Triar entre BT i HO?

    @@@ ruby
    class Supplier < ActiveRecord::Base
      has_one :account
    end

    class Account < ActiveRecord::Base
      belongs_to :supplier
    end

Té més *sentit* que un proveidor tingui in compte on compte associat i no
a l'inrevés.

**Tinença vs Pertinença**

!SLIDE subsection
# Triar entre BT i HO?

La migració anterior seria com la següent

    @@@ ruby
    class CreateSuppliers < ActiveRecord::Migration
      def change
        create_table :suppliers do |t|
          t.string  :name
          t.timestamps
        end

        create_table :accounts do |t|
          t.integer :supplier_id
          t.string  :account_number
          t.timestamps
        end
      end
    end

!SLIDE subsection bullets incremental
# Triar entre HM :through i HBTM?

* Utilitzar `has_many :through` si necessitem treballar amb el model intermig o
realitzar-li validacions, etc.
* En qualsevol altre cas podem utilitzar `has_and_belongs_to_many`

!SLIDE subsection
# Associacions polimòrfiques

Amb les associons polimòrfiques un model pot pertanyer a més d'un altre
model utilitzan una única associacó

    @@@ ruby
    class Picture < ActiveRecord::Base
      belongs_to :imageable, :polymorphic => true
    end

    class Employee < ActiveRecord::Base
      has_many :pictures, :as => :imageable
    end

    class Product < ActiveRecord::Base
      has_many :pictures, :as => :imageable
    end

!SLIDE subsection
# Associacions polimòrfiques

Especificar-la a la migració

    @@@ ruby
    class CreatePictures < ActiveRecord::Migration
      def change
        create_table :pictures do |t|
          t.string :name
          t.references :imageable, :polymorphic => true
          t.timestamps
        end
      end
    end

!SLIDE subsection
# Associacions polimòrfiques

Especificar-la a la migració (alternativa)

    @@@ ruby
    class CreatePictures < ActiveRecord::Migration
      def change
        create_table :pictures do |t|
          t.string  :name
          t.integer :imageable_id
          t.string  :imageable_type
          t.timestamps
        end
      end
    end

!SLIDE subsection
# Associacions polimòrfiques

![polymorphic](/file/assets/images/polymorphic.png)
