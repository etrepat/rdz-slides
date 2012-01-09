!SLIDE subsection
# Models
## Validacions

!SLIDE subsection
# Validacions

Exemple

    @@@ ruby
    class Product < ActiveRecord::Base
      validates :status, :presence => true
    end

Si ho provem en una sessió de la consola

    @@@ sh
    > p = Product.new
    > p.save
    => false
    > p.valid?
    => false
    > p.errors
    => {:status => ["can't be blank"]}

!SLIDE subsection
# Validacions

    @@@ ruby
    validates :status, :presence => true
    validates :status, :length => {:minimum => 3}

    # ó també

    validates :status, :presence => true,
      :length => {:minimum => 3}

!SLIDE subsection
# Validacions
## Opcions de `validates`

    @@@ ruby
    :presence => true
    :uniqueness => true
    :numericality => true
    :length => { :minimum => 0, :maximum => 2000 }
    :format => { :with => /.*/ }
    :inclusion => { :in => [1,2,3] }
    :exclusion => { :in => [1,2,3] }
    :acceptance => true
    :confirmation => true

!SLIDE subsection smbullets
# Validacions
## Sintaxi alternativa

    @@@ ruby
    validates_presence_of :status
    validates_numericality_of :fingers
    validates_uniqueness_of :toothmarks
    validates_confirmation_of :password
    validates_acceptance_of :zombification
    validates_length_of :password, :minimum => 3
    validates_format_of :email, :with => /regex/i
    validates_inclusion_of :age, :in => 18..99
    validates_exclusion_of :age, :in => 0...18,
      :message => "Has de ser mes gran de 18"

!SLIDE subsection
# Validacions
## Quan s'executen?

En un model les validacions s'executen *sempre* que utilitzem qualsevol
dels següents mètodes:

`create,
create!,
save,
save!,
update,
update_attributes,
update_attributes!`

!SLIDE subsection
# Validacions
## Es poden saltar?

Els següents mètodes **no** executen les validacions definides en un model:

`decrement!,
decrement_counter,
increment!,
increment_counter,
toggle,
touch,
update_all,
update_attribute,
update_column,
update_counters,
`

El mètode `save` també accepta un paràmetre que especifica si s'han d'executar
les validacions o no

`save(:validate => false)`
