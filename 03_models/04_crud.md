!SLIDE subsection
# Models
## CRUD

### <font color="green">**C**</font>reate
### <font color="blue">**R**</font>ead
### <font color="yellow">**U**</font>pdate
### <font color="red">**D**</font>elete

!SLIDE subsection
# <font color="green">C</font>reate

Mètodes per a instanciar i/o crear models
    @@@ ruby
    new(attributes)       # instancia un nou model
    create(attributes)    # instancia i crea
    create!(attributes)   # excepció si error

Exemple
    @@@ ruby
    p = Persona.new
    p.nom = "Estanis"
    p.save

!SLIDE subsection
# <font color="blue">R</font>ead

Mètodes per a llegir objectes (consultes a continuació)
    @@@ ruby
    find(id)      # també amb un array de ids
    exists?       # existeix?
    new_record?   # nou?

Exemple
    @@@ ruby
    Categories.find(1)
    Categories.find([2,3,4,5])

!SLIDE subsection
# <font color="yellow">U</font>pdate

Actualització *directa* d'atributs d'un o més models
    @@@ ruby
    update(ids, actualitzacions)  # poden ser arrays
    update_all(actualitzacions)

Exemple
    @@@ ruby
    # actualitza un únic registre
    Empleat.update(15, :salari => 3000,
      :categoria => 'Enginyer')

    # diversos registres alhora
    empleats = { 1 => {"Nom" => "Estanis"},
      2 => {"Nom" => "Jaume"} }
    Empleat.update(empleats.keys, empleats.values)

!SLIDE subsection
# <font color="red">D</font>elete

Com eliminem registres?

Sense instanciar els models corresponents i, per tant, sense executar validacions
ni "callbacks" ni cap lògica associada a les relacions que puguin existir.
    @@@ ruby
    delete(id)      # també amb array
    delete_all

Instanciant els models abans d'eliminar-los i executant tota la lògica
definida
    @@@ ruby
    destroy(id)     # també amb array
    destroy_all

`delete` és més eficient però s'ha d'anar amb compte
