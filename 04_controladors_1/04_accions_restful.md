!SLIDE
# Accions per defecte
### "Convention Over Configuration"

!SLIDE subsection incremental
# Mètodes RESTful

!SLIDE subsection smaller incremental
# Mètodes RESTful

* index
* show
* new
* edit
* create
* update
* destroy

!SLIDE subsection smaller
# Mètodes RESTful

* index *(Llista tots els registres)*
* show *(Ensenya un registre)*
* new *(Nou registre)*
* edit *(Editar registre)*
* create *(Crear registre (guardar))*
* update *(Actualitzar registre (guardar))*
* destroy *(Eliminar un registre)*

!SLIDE subsection smaller
# Mètodes RESTful

* index *(Llista tots els registres)* --> <font color="green">GET</font>
* show *(Ensenya un registre)* --> <font color="green">GET</font>
* new *(Nou registre)* --> <font color="green">GET</font>
* edit *(Editar registre)* --> <font color="green">GET</font>
* create *(Crear registre (guardar))* --> <font color="yellow">POST</font>
* update *(Actualitzar registre (guardar))* --> <font color="green">PUT</font>
* destroy *(Eliminar un registre)* --> <font color="red">DELETE</font>

!SLIDE subsection
# Mètodes RESTful
## `index`

    @@@ ruby
    def index
      @articles = Articles.all

      respond_to do |format|
        format.html # index.html.erb
        format.xml { render :xml => @articles }
      end
    end

!SLIDE subsection
# Mètodes RESTful
## `show`

    @@@ ruby
    def show
      @article = Article.find(params[:id])

      respond_to do |format|
        format.html # show.html.erb
        format.xml { render :xml => @article }
      end
    end

!SLIDE subsection
# Mètodes RESTful
## `new`

    @@@ ruby
    def new
      @article = Article.new

      respond_to do |format|
        format.html # new.html.erb
        format.xml { render :xml => @article }
      end
    end

!SLIDE subsection
# Mètodes RESTful
## `edit`

    @@@ ruby
    def edit
      @article = Article.find(params[:id])
    end

!SLIDE subsection small
# Mètodes RESTful
## `create`

    @@@ ruby
    def create
      @article = Article.new(params[:article])

      respond_to do |format|
        if @article.save
          format.html { redirect_to @article, :notice => 'Ok' }
          format.xml {
            render :xml => @article, :status => :created,
              :location => @article
          }
        else
          format.html { render :action => "new" }
          format.xml {
            render :xml => @article.errors,
              :status => :unprocessable_entity
          }
        end
      end
    end

!SLIDE subsection small
# Mètodes RESTful
## `update`

    @@@ ruby
    def update
      @article = Article.find(params[:id])

      respond_to do |format|
        if @article.update_attributes(params[:article])
          format.html { redirect_to @article, :notice => 'Ok' }
          format.xml { head :ok }
        else
          format.html { render :action => "edit" }
          format.xml {
            render :xml => @article.errors,
              :status => :unprocessable_entity
          }
        end
      end
    end

!SLIDE subsection
# Mètodes RESTful
## `destroy`

    @@@ ruby
    def destroy
      @article = Article.find(params[:id])
      @article.destroy

      respond_to do |format|
        format.html { redirect_to(articles_url) }
        format.xml  { head :ok }
      end
    end
