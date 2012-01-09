!SLIDE
![Ruby logo](/file/assets/images/ruby_logo.png)
# Estructures de control

!SLIDE subsection bullets incremental
# Condicionals

* Clausules `if`: if, elsif, else, end
* Clasules `case`
* Les estructures condicionals retornen el valor de l'ultima expressió
evaluada
* Operador ternari: `?`

!SLIDE subsection
# Condicionals
## if

    @@@ ruby
    c = 10
    if c > 10
      puts "M'he passat!"
    elsif c == 10
      puts "He arribat!"
    else
      puts "Venint..."
    end

!SLIDE subsection
# Condicionals
## if

    @@@ ruby
    c = 100
    missatge = if c == 100
                 "Has encertat"
               else
                 "Has fallat"
               end

!SLIDE subsection
# Condicionals
## if

També es pot uitlitzar com a modificador de sentència

    @@@ ruby
    height = 1.62
    puts "Que alt que ets!" if height >= 1.85

També es pot utilitzar `unless` com a representació de `if !(expr)`

    @@@ ruby
    puts "Que alt que ets!" unless height < 1.85

!SLIDE subsection
# Condicionals
## case

    @@@ ruby
    x = 17
    case x
    when 0
    when 2..5
      puts "Ah!"
    when x.to_s.downcase == "Estanis"
      puts "Ondia!"
    else
      puts "No res"
    end

!SLIDE subsection bullets incremental
# Bucles

* Les col.leccions basades en el mòdul `Enumerable` normalment es recorrent
mitjançant el mètode `each`
* Es pot utilitzar també l'expressió: `for..in`
* Similars a altres llenguages: `while, until`

!SLIDE subsection
# Bucles
## Exemples

    @@@ ruby
    count = 0
    while count < 3
      puts count
      count += 1
    end

També com a modificador de sentència

    @@@ ruby
    count = 0
    puts count while (count < 3 && count += 1)

!SLIDE subsection
# Bucles
## Exemples

Es pot utilitzar `for..in` per iterar col.leccions. Podem utiltizar
les paraules clau `next` i `break` dins dels bucles per a saltar-nos elements
i "trencar-los"

    @@@ ruby
    for value in [0, 1, 2, 3, 4]
      next if value == 1
      break if value == 3
      puts value
    end

!SLIDE subsection
# Bucles
## Exemples

    @@@ ruby
    count = 0
    until count == 3
       puts count
       count += 1
    end

També com a modificador de sentència

    @@@ ruby
    count = 0
    puts(count += 1) until count == 3

!SLIDE subsection bullets incremental
# Excepcions

Les excepcions es "llancen" mitjançant la instrucció `raise`

    @@@ ruby
    raise StandardError, "WTF!"

i es capturen per mitjà del bloc `begin..rescue..ensure..end`

    @@@ ruby
    begin
      # codi que pot fallar
    rescue Exception => e
      # si fallo, m'executo
    ensure
      # m'executo sempre
    end

Podem definir les nostres propies excepcions creant subclasses de les
definides per Ruby

!SLIDE subsection
# Excepcions
## Exemple

    @@@ ruby small
    url       = "http://some.url"
    attempts  = 0
    begin
      contents = open(url).read
      puts contents
    rescue SocketError => e
      puts "No he pogut obrir #{url}, intents: #{attempts}: #{e}"
      attempts += 1
      retry unless attempts >= 3
    rescue Exception => e
      puts "Error desconegut: #{e.message} #{e.backtrace.join("\n")}"
      raise
    ensure
      puts "Sempre m'executo, passi el que passi"
    end
