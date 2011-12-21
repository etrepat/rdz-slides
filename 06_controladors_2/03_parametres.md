!SLIDE
# Paràmetres

!SLIDE subsection bullets incremental
# Paràmetres

* Per accedir als paràmetres d'una petició HTTP en els nostres
controladors, podem utilizar el mètode `params`.
* Els paràmetres poden venir identificats per les rutes, formularis o directament
pel query string.
* Podem entendre `params` com un `Hash`.

!SLIDE subsection
# Paràmetres

    @@@ ruby
    class ClientsController < ActionController::Base
      # GET /clients?status=activated
      def index
        if params[:status] == "activated"
          @clients = Client.activated
        else
          @clients = Client.unactivated
        end
      end

      # POST /clients
      def create
        @client = Client.new(params[:client])
        ...
      end
    end

!SLIDE subsection
# Paràmetres

Podem, a més, especificar paràmetres per defecte que seran utilitzats
per a generar URL's si definim el mètode `default_url_options` en un
controlador:

    @@@ ruby
    class ApplicationController < ActionController::Base
      def default_url_options(opts)
        {:locale => I18n.locale}
      end
    end

Ho podem definir a un controlador concret o a `ApplicationController` si
volem utilizar-ho globalment.
