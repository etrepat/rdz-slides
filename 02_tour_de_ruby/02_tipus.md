!SLIDE
![Ruby logo](/file/assets/images/ruby_logo.png)
# Tipus de dades

!SLIDE subsection bullets incremental
# Nombres (Numeric)

* En ruby els nombres es representen mitjançant la classe
base `Numeric`
* La majoria dels nombres que ens trobarem són subclasses de `Fixnum` o
`Float`
* També existeixen els tipus numérics: `BigDecimal, Complex, Rational`

!SLIDE subsection
# Nombres (Numeric)

Exemples
    @@@ ruby
    1 + 3 - 7
    => -3
    3 / 4
    => 0
    3 / 4.0
    => 0.75
    3 * 3
    => 9
    185 * 1.18
    => 218.3
    12**2
    => 144
    8 % 2
    => 0

!SLIDE subsection
# Nombres (Numeric)

El mòdul `Math` conté tot de funcions matemàtiques estándar

    @@@ ruby
    y = 144
    x = Math.sqrt(y)
    => 12
    Math.hypot(3, 4)
    => 5 # sqrt(x**2, y**2)

!SLIDE subsection smbullets incremental
# Cadenes (String)

* Objectes de la classe `String`
* Soporta nativament UTF-8 i cadenes multi-byte
* Poden estar representades per comilles simples o dobles
* Operadors de concatenació i accés: +, <<, []
* Es poden interpolar amb l'expressió #{}
* Alguns mètodes útils de la classe `String`: `size, each_char, each_line,
empty?, gsub, strip, upcase`

!SLIDE subsection
# Cadenes (String)

    @@@ ruby
    cadena = "Hola"
    cadena << " Ruby"
    cadena = cadena + "!"
    puts cadena

!SLIDE subsection
# Cadenes (String)

    @@@ ruby
    # Amb entrecomillat doble,
    # s'interpola l'expressió #{}
    puts "Ara son les: #{Time.now}"

    # Amb entrecomillat simple no
    puts 'Ara son les #{Time.now}'

!SLIDE subsection
# Cadenes (String)

Podem utilitzar seqüències d'escapament (a la C)

    @@@ ruby
    puts "\t Prova\n"

    puts 'Això és un \'EXEMPLE\''

!SLIDE subsection
# Cadenes (String)

Per accedir als caràcters podem utilitzar l'operador `[]`

    @@@ ruby small
    a = "Hola"
    puts "a[1] == #{a[1]}"

Utilitzar funcions de la classe `String`

    @@@ ruby small
    a = "partirem aquesta cadena per espais".split(' ').join(', ')
    puts a
    => "partirem, aquesta, cadena, per, espais"

    b = "ho vull en majuscules".upcase
    puts b
    => "HO VULL EN MAJUSCULES"

    c = ""
    puts c.empty?
    => true
    c = "no buida"
    puts c.empty?
    => false

!SLIDE subsection bullets incremental
# Symbol (símbols)

* Són cadenes inmutables
* Es prefixen per mitjà de dos punts: `:un_simbol`
* S'utilitzen molts cops com a claus d'un Hash o per representar noms
de mètodes o funcions
* Podem convertir cadenes i simbols entre si mitjançant: `to_s` i `to_sym`

!SLIDE subsection
# Symbol (símbols)

    @@@ ruby
    a, b = "hola", "hola"
    a == b
    => true
    a.object_id == b.object_id
    => false

    a, b = :hola, :hola
    a == b
    => true
    a.object_id == b.object_id
    => true

!SLIDE subsection bullets incremental
# Array

* Seqüències d'objectes dinàmiques (mida variable), sense tipus i
indexades (desde zero)

* Array i String comparteixen alguns operadors: `+, <<, []`

* La classe `Array` inclou el mòdul `Enumerable`, el que dona accés
a un conjunt de mètodes com: `each, select, map, inject, etc.`

!SLIDE subsection
# Array

Semàntica similar
    @@@ ruby
    a = ["Ruby", 3.141592]
    a << "Rails"
    puts a[1]
    => 3.141592
    puts a[1..2]
    puts a[1, 2]
    b = [3, 4, 5, "vint-i-dos"]
    puts a+b

!SLIDE subsection
# Array

Iterar els elements
    @@@ ruby
    c = ["pera", "poma", "pressec"]
    c.each do |fruita|
      puts "#{fruita.capitalize}, mmm..."
    end

Un "block" es pot entendre, de moment, com una funció (o métode) anónima

!SLIDE subsection
# Array

El modul `Enumerable` conté un **munt** de funcions útils
    @@@ ruby
    c = [3, 3, 2, 1]
    c.join(' | ')
    c.map { |x| x**2 }
    c.select { |x| x % 2 == 0 }
    c.reject { |x| x < 3 }
    c.inject { |sum, i| sum + i }
    c.include?(2)
    c.sort
    c.uniq
    c.uniq.select { |x| x < 3 }.sort

!SLIDE subsection bullets incremental
# Hash

* Un *hash* és un array associatiu de parells clau-valor
* Com a *clau* podem utilitzar, gairebé, qualsevol objecte. Habitualment
s'utilitzen symbols.
* La classe `Hash` també inclou els mètodes del mòdul `Enumerable`.

!SLIDE subsection
# Hash

Sintaxi
    @@@ ruby
    hash = {
      :leia => "Princesa",
      :han => "Rebel",
      :luke => "Jedi"
    }
    puts hash[:luke]
    => "Jedi"

!SLIDE subsection
# Hash

Treballar amb els elements d'un Hash
    @@@ruby
    hash = {}
    hash[:han]
    => nil
    hash[:han] = "Fugitiu"
    => "Fugitiu"
    hash.delete(:han)
    hash[:han]
    => nil

!SLIDE subsection
# Hash

Iterar un hash
    @@@ ruby
    hash.each do |clau, valor|
      puts "#{clau}: #{valor}"
    end

    # Accedir a les claus com un Array
    hash.keys
    => [:leia, :han, :luke]

Recordem que podem utilitzar els mètodes del mòdul `Enumerable` com `map`,
`select`, `reject`, ...

!SLIDE subsection bullets incremental
# Rangs (Range)

* Un rang és un objecte que representa tots els valors dins d'un rang:
`1..100`
* Utiltizant 3 punts no inclou l'últim valor `1...100`
* Alguns mètodes útils: `each, step, include?`
* Es poden crear rangs d'objectes propis sempre que implementin
els mètodes: `<=>` i `succ`

!SLIDE subsection
# Rangs (Range)

Sintaxi
    @@@ ruby
    a = 1..5
    b = 1...5
    a.to_a
    => [1,2,3,4,5]
    b.to_a
    => [1,2,3,4]

Podem iterar també els rangs
    @@@ ruby
    (1..100).each { |n| puts "#{n}" }
