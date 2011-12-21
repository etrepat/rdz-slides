!SLIDE
# Sessions

!SLIDE subsection bullets incremental
# Sessions

* Una aplicació web té una sessió per usuari que ens serveix per enmagatzemar
dades que podrán persistir entre crides.

* En Rails podem utilizar diferents mecanismes per enmagatzemar
les dades d'una sessió: `CookiStore, MemcacheStore, ActiveRecordStore, ...`.

* Podem configurar-ho a: `config/initializers/session_store.rb`.

!SLIDE subsection bullets incremental
# Sessions

* En un controlador podem accedir a les dades de sessió per mitjà del mètode
`session`.

* Al igual que el mètode `params`, podem entendre que `session` es comporta
igual que un `Hash`.

* Les sessions en Rails també son "Lazy Loaded". Si no es fant servir, no es
carreguen i, per tant, no cal desactivar-les.

!SLIDE subsection
# Sessions
### Accedir a valors en la sessió

    @@@ ruby
    class ApplicationController < ActionController::Base
      ...
      private

      def current_user
        @current_user ||= if session[:current_user_id]
          User.find(session[:current_user_id])
        end
      end
    end

!SLIDE subsection
# Sessions
### Enmagatzemar valors en la sessió

    @@@ ruby
    class UserSessionsController < ApplicationController
      ...
      def create
        if user = User.authenticate(params[:username],
          params[:password])
          session[:current_user_id] = user.id

          redirect_to root_url,
            :notice => "Benvingut, #{user.name}."
        end

        render :new, :alert => 'Usuari invalid'
      end
    end

!SLIDE subsection
# Sessions
### Eliminar valors de la sessió

    @@@ ruby
    class UserSessionsController < ApplicationController
      ...
      def destroy
        @current_user = session[:current_user_id] = nil
        redirect_to root_url
      end
    end
