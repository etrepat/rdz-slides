!SLIDE
![Rails logo](/file/assets/images/rails.png)
# Rails desde Zero
## Nocions de Ruby
![Ruby logo](/file/assets/images/ruby_logo.png)

!SLIDE subsection bullets incremental
# Ruby

* Generic, interpretat, GC
* Sintaxi neta
* Completament OO - *TOT* és un objecte (primitives, classes i nil)
* Permet programar en format procedural i funcional
* Tipus de dades dinàmics *("duck typing")*

!SLIDE subsection
# Ruby
## [http://ruby-doc.org/](http://ruby-doc.org/)

!SLIDE subsection
# Irb
## Irb és la interfície interactiva a Ruby

Executar en una finestra del terminal

    @@@ shell
      $ irb

S'utilitza, principalment, per a testejar petits trocets de
codi.

!SLIDE
![Ruby logo](/file/assets/images/ruby_logo.png)
# Introduccio a la sintaxi

!SLIDE subsection
# Identificadors

    @@@ ruby
    MyClass, MyModule
    PI = 3.141592
    un_metode
    variable_local = 12
    @variable_instancia
    @@variable_classe
    $variable_global

!SLIDE subsection
# Tipus de dades

En ruby *tot* és un objecte. Provem el següent en una sessió de Irb

    @@@ ruby
      123.class
      nil.class
      true.class
      "hola mundo!".class
      :symbol.class

!SLIDE subsection bullets incremental
# Certesa

* En ruby els **únics** valors que s'evaluen com a fals són: `false, nil`
* A diferència d'altres llenguatges ón el zero (0) ó una cadena buida ("")
s'evaluen com a fals

!SLIDE subsection bullets incremental
# nil

* L'absència d'un objecte en ruby es representa mitjançant la paraula
reservada `nil`
* `nil` és la única instancia de `NilClass < Object < BasicObject`
* `nil` s'evalua com a fals

!SLIDE subsection bullets incremental
# Constants

Les constants *sempre* comencen per una lletra majúscula

    @@@ shell
      Constant = 12   # Aixó és una constant
      constant = 12   # Aixó no, és una variable

!SLIDE subsection
# Operadors
## Assignació

Mitjançant el signe d'igualtat (=)

    @@@ ruby
    color = "vermell"
    un_altre_color = "blau"
    numero = 123

!SLIDE subsection
# Operadors
## Auto-assignació

    @@@ ruby
    x = 1       # => 1
    x += x      # => 2
    x -= x      # => 0
    x += 4      # => 4
    x *= x      # => 16
    x **= x     # => (16^16)
    x /= x      # => 1

No hi ha operadors d'increment o decrement (++) en Ruby

!SLIDE subsection
# Operadors

## Assignació múltiple

    @@@ ruby
    color1, color2, color3 = "vermell", "blau", "verd"
    colors, ciutat = ["vermell", "blau", "verd"], "Barcelona"

## Assignació condicional

    @@@ ruby
    config ||= "valor"

L'operador `||=` comproba si la variable és nula (o inexistent) i li
assigna el valor (objecte) especificat

!SLIDE subsection
# Operadors
## Comparació

    @@@ ruby
    ==      # => Equivalència
    !=      # => No igual
    <, <=   # => Més petit (o igual) que
    >, >=   # => Més gran (o igual) que
    <=>     # Combinat: 0 si iguals,
            # -1 si el segon > que el primer
            # 1 si el segon < que el primer

!SLIDE subsection
# Operadors
## And (&&), Or (||), Not(!)

    @@@ ruby
    x = false
    y = true

    x && y  # => false
    X || y  # => true
    !x      # => true
    !y      # => false
