!SLIDE
![Ruby logo](/file/assets/images/ruby_logo.png)
# Mètodes

!SLIDE subsection
# Mètodes
## Definició

    @@@ ruby
    def saluda(nom)
      puts "Hola #{nom}!"
    end

Els parèntesis són opcionals tant en la definició com en la crida, pero
poden ésser necessaris

    @@@ ruby
    saluda "Jordi"
    => "Hola Jordi!"
    saluda("Jordi").downcase
    => "hola jordi!"

!SLIDE subsection
# Mètodes
## Valors de retorn

Els mètodes en ruby sempre retornen el valor de l'última expressió evaluada
(igual que en les sentències condicionals)

    @@@ ruby
    def suma(x, y)
      x + y
    end

!SLIDE subsection
# Mètodes
## Valors de retorn

També podem fer retornar un mètode de forma explícita mitjançant la
instrucció `return`

    @@@ ruby
    def authenticate(username)
      return unless username == "jaume"
      puts "Benvingut, Jaume!"
    end

!SLIDE subsection
# Mètodes
## Paràmetres

Podem utilitzar qualsevol tipus d'objecte com a paremetre d'un mètode. Molt sovint
veurem que s'utilitzen objectes `Hash`.

!SLIDE subsection
# Mètodes

    @@@ ruby
    def distancia(x=0, y=0)
      Math.hypot(x, y)
    end

    def saluda(nom, opcions={})
      es_de_nit = opcions[:nit] || false
      if es_de_nit
        puts "Bona nit, #{nom}!"
      else
        puts "Bon dia, #{nom}!"
      end
    end

Com hem vist podem especificar valors per defecte en els parámetres
