!SLIDE
![Ruby logo](/file/assets/images/ruby_logo.png)
# Clases

!SLIDE subsection
# Clases
## Definició

    @@@ ruby
    class Animal
      def viu?
      end
    end

!SLIDE subsection bullets
# Clases
## Variables

* `@variable` representa una variable d'instancia
* `@@variable` representa una variable de classe
* `self` representa la instancia actual (this)

!SLIDE subsection
# Clases
## Variables

    @@@ ruby
    class Persona
      @nom = "Estanis"

      def saluda
        "Hola #{@nom!}"
      end

      def renombra(nom)
        @nom = nom
      end
    end

!SLIDE subsection
# Clases
## Variables

Com s'utilitza?

    @@@ ruby
    p = Persona.new
    puts p.saluda   # => "Hola Estanis!"
    p.renombra("Jaume")
    puts p.saluda   # => "Hola Jaume!"

!SLIDE subsection
# Clases
## Constructor

S'utilitza el mètode especial `initialize` que es crida sempre que creem
una nova instancia d'una classe.

    @@@ ruby
    class Persona
      def initialize(nom)
        @nom = nom
      end
    end

    p = Persona.new("Estanis")

Els objectes s'instancien amb el mètode `new`

!SLIDE subsection
# Clases
### Accedint a les variables d'instancia

    @@@ ruby
    class Persona
      def initialize(nom)
        @nom = nom
      end

      def nom
        @nom
      end

      def nom=(nom)
        @nom = nom
      end
    end

!SLIDE subsection bullets
# Clases
### Accedint a les variables d'instancia

Per a no repetir sempre el mateix codi, ruby ens proporciona 3 mètodes
especials que defineixen el comportament anterior.

`attr_accessor`, `attr_reader` i `attr_writer`

!SLIDE subsection
# Clases
### Accedint a les variables d'instancia

    @@@ ruby
    class Persona
      def initialize(nom)
        @nom = nom
      end

      attr_accessor :nom
    end

!SLIDE subsection
# Clases
## Herència

Els mètodes i les variables poden ser *heredats* d'una altra classe per mitjà
de l'operador `<`. Ruby no soporta herència múltiple

    @@@ ruby
    class Persona
      attr_accessor :nom
    end

    class Empleat < Persona
      attr_accessor :carrec
    end

!SLIDE subsection
# Clases
## Control d'accés

Podem registrir l'accés a les nostres variables i metodes mitjançant les
paraules reservades: `private` i `protected`

* `private`: accessible només per a la classe que els defineix
* `protected`: accessible també per a les subclasses

!SLIDE subsection
# Clases
### Control d'accés

    @@@ ruby small
    class Persona
      attr_accessor :nom

      protected

      def saluda
        "Hola #{@nom}!"
      end

      private

      def renombra(nom)
        @nom = nom
      end
    end

!SLIDE subsection
# Clases
## Mètodes de clase (estàtics)

Es defineixen per prefixant-los amb la referència a la instància en curs

    @@@ ruby
    class Persona
      def self.crea(nom)
        Persona.new(nom)
      end
    end

!SLIDE subsection
# Clases
## Mètodes de clase (estàtics)

Sintàxi alternativa modificant la referencia a la instància actual. Ja no
cal prefixar-los.

    @@@ ruby
    class Persona
      class << self
        def crea(nom)
          Persona.new(nom)
        end
      end
    end

!SLIDE
![Ruby logo](/file/assets/images/ruby_logo.png)
# Mòduls

!SLIDE subsection bullets
# Mòduls

* Un mòdul es una col.lecció de mètodes, constants i variables (de classe)
* Es poden incloure "mix in" dins de classes
* Els mòduls no es poden instanciar

!SLIDE subsection
# Mòduls

Exemple

    @@@ ruby
    module Edat
      MITJANA_EDAT = 50

      def edat=(edat)
        @edat = edat
      end

      def edat
        @edat
      end

      def gran?
        edat > MITJANA_EDAT
      end
    end

!SLIDE subsection
# Mòduls

Incloiem el mòdul anterior en una classe
    @@@ ruby
    class Persona
      include Edat # <= !!
      attr_accessor :name
      ...
      def initialize(name)
        self.name = name
      end
    end

    p = Persona.new("Jordi")
    p.edat = 36
    p.gran? # => false
