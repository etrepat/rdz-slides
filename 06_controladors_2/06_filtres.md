!SLIDE
# Filtres

!SLIDE subsection bullets incremental
# Filtres

* Els "filtres" són mètodes que s'executen abans, despres o "al voltant" d'una
acció d'un controlador.

* Els filtres s'hereden jeràrquicament, llavors si definim un filtre en
`ApplicationController`, serà executat en cada controlador de l'aplicació.

!SLIDE subsection
# Filtes
## Especificant filtres

    @@@ ruby
    # el mètode require_login es cridarà ABANS
    # que qualsevol acció d'un controlador
    before_filter :require_login

    # desprès d'executar l'acció "destroy" es cridarà
    # el mètode cleanup
    after_filter  :cleanup, :only => :destroy

    # s'encapsularà l'acció "show" dins de la funció
    # wrap_in_transaction
    around_filter :wrap_in_transaction, :only => :show

!SLIDE subsection
# `before_filter`

Els filtres de tipus `before_filter` s'executen **abans** que les accions del
controlador i poden modificar i/o aturar el cicle de request.

    @@@ ruby
    class ApplicationController < ActionController::Base
      before_filter :login_required

      private

      def login_required
        unless !!current_user
          redirect_to login_url
        end
      end
    end

!SLIDE subsection
# `after_filter`

Els filtres de tipus `after_filter` s'executen **després** que una acció d'un
controlador s'ha executat. Obviament, no poden modificar el cicle de request però
en canvi tenen accés a les dades de la resposta.

    @@@ ruby
    class BooksController < ActionController::Base
      after_filter :cleanup, :only => :destroy

      private

      def cleanup
        # ...
      end
    end

!SLIDE subsection small
# `around_filter`

Aquests filtres "encapsulen" les accions d'un controlador dins de la funció
especificada. S'ha d'utilitzar `yield` per indicar el moment on s'ha d'executar
l'acció corresponent.

    @@@ ruby
    class ChangesController < ActionController::Base
      around_filter :wrap_in_transaction, :only => :show

      private

      def wrap_in_transaction
        ActiveRecord::Base.transaction do
          begin
            yield # s'executa l'acció corresponent
          ensure
            raise ActiveRecord::Rollback
          end
        end
      end
    end
