!SLIDE
# Rails desde Zero
![Rails logo](/file/assets/images/rails.png)

!SLIDE subsection bullets
# Instal.lació

1. Entorn
2. Git
3. RVM / Ruby / Gemsets
4. Bundler
5. Rails

!SLIDE subsection
# Instal.lació: Entorn (OSX)

* Instal.lar GCC via XCode ó [http://git.io/osxgcc](http://git.io/osxgcc)
* Instal.lar Homebrew: [http://mxcl.github.com/homebrew/](http://mxcl.github.com/homebrew/)

!SLIDE subsection
# Instal.lació: Entorn (Linux)

    @@@ shell
    # Eines
    $ sudo apt-get install build-essential

    # Llibreries
    $ sudo apt-get install bison openssl
    libreadline6 libreadline6-dev curl
    zlib1g zlib1g-dev libssl-dev
    libyaml-dev libxml2-dev libxslt-dev
    autoconf

!SLIDE subsection
# Instal.lació: Entorn (Linux)

    @@@ shell
    # SQLite3 ?
    $ sudo apt-get install libsqlite3-0
    libsqlite3-dev sqlite3

    # PostgreSQL ?
    $ sudo apt-get install postgresql
    postgresql-client postgresql-doc
    libpq-dev

    # Imagemagick ?
    $ sudo apt-get install imagemagick
    libmagickcore-dev libmagickwand-dev

!SLIDE subsection
# Instal.lació: Git

### Via gestor de paquets:

    @@@ shell
    # OSX
    $ brew install git

    # Linux
    $ sudo apt-get install git-core

### Via web: [http://git-scm.com/](http://git-scm.com/)

!SLIDE subsection
# Instal.lació: RVM / Ruby / Gemset

## RVM: Ruby Version Manager

### [http://beginrescueend.com/](http://beginrescueend.com/)

    @@@ shell
    $ rvm install 1.9.2
    $ rvm gem list
    $ rvm gemset create [nom]

!SLIDE subsection
# Instal.lació: Bundler

### [http://gembundler.com/](http://gembundler.com/)

    @@@ shell
    $ gem install bundler

!SLIDE subsection
# Instal.lació: Rails

![Rails logo](/file/assets/images/rails.png)

    @@@ shell
    $ gem install rails
