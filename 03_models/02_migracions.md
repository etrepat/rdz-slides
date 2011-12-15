!SLIDE subsection
# Models
## Migracions

!SLIDE subsection
# Migracions

Anatomia d'una migració

    @@@ ruby
    class CreateProducts < ActiveRecord::Migration
      def change
        create_table :products do |t|
          t.string  :name
          t.text    :description

          t.timestamps
        end
      end
    end

!SLIDE subsection
# Migracions

Una migració és una subclasse de `ActiveRecord::Migration` que implementa
dos mètodes: `up` (crear modificacions) i `down` (desfer-les)

* `create_table, drop_table, change_table`
* `add_column, change_column, rename_column, remove_column`
* `add_index, remove_index`

!SLIDE subsection
# Migracions

Els tipus de dades que podem utilitzar per als camps d'una taula en una
migració són els que soporta `ActiveRecord`.

`:primary_key
:string
:text
:integer
:float
:decimal
:datetime
:timestamp
:time
:date
:binary
:boolean`

Es mapejen automàticament al tipus de dades corresponent segons el motor de BD. Per
exemple, en MySQL un `:string` correspon a `VARCHAR(255)`.

!SLIDE subsection
# Migracions
## Generar una migració

!SLIDE
## Habitualment, podem crear una migració de 2 maneres

!SLIDE subsection
# 1

Creant-la mitjançant un model o scaffold
    @@@ shell small
    rails generate model Product name:string description:text

el que ens crearà una migració com la següent:
    @@@ ruby
    class CreateProducts < ActiveRecord::Migration
      def change
        create_table :products do |t|
          t.string :name
          t.text :description

          t.timestamps
        end
      end
    end

!SLIDE subsection
# 2

Individualment
    @@@ shell small
    $ rails generate migration AddPartNumberToProducts

que ens crearà:
    @@@ ruby
    class AddPartNumberToProducts < ActiveRecord::Migration
      def change
      end
    end

!SLIDE subsection
# Migracions
## Creant una taula

    @@@ ruby
    create_table :products, :id => [true|false],
      :options => '' do |t|
      t.string  :name
      t.text    :description
      t.boolean :active, :null => false

      t.timestamps
    end

!SLIDE subsection
# Migracions
## Modificant taules

    @@@ ruby
    change_table :products do |t|
      t.remove :description, :name
      t.string :part_number
      t.index :part_number
      t.rename :upccode, :upc_code
    end

    remove_column :products, :description
    remove_column :products, :name
    add_column :products, :part_number, :string
    add_index :products, :part_number
    rename_column :products, :upccode, :upc_code

!SLIDE subsection
# Migracions
## Funcions d'ajuda (helpers)

    @@@ ruby
    create_table :products do |t|
      t.timestamps
    end

Crea columnes `created_at` i `updated_at` que es mantenen automàticament

!SLIDE subsection
# Migracions
## Funcions d'ajuda (helpers)

    @@@ ruby
    create_table :products do |t|
      t.references :category
      # també
      # t.belongs_to :category
    end

Crea el camp `category_id` associat del tipus adecuat

**NO** crea automàticament les restriccions `FOREIGN_KEY`

!SLIDE subsection
# Migracions
## SQL

Podem utilitzar SQL en les migracions per mitjà del mètode `execute`

    @@@ ruby small
    class ExampleMigration < ActiveRecord::Migration
      def change
        create_table :products do |t|
          t.references :category
        end

        # Afegim la clau foranea
        execute <<-SQL
          ALTER TABLE products
            ADD CONSTRAINT fk_products_categories
            FOREIGN KEY (category_id)
            REFERENCES categories(id)
        SQL
      end
    end

!SLIDE subsection
# Migracions
### Executant migracions

* `rake db:migrate [VERSION=N]`
* `rake db:rollback [STEP=3]`
* `rake db:migrate:up VERSION=N`
* `rake db:migrate:down VERSION=N`
