!SLIDE
![Rails logo](/file/assets/images/rails.png)
# Rails desde Zero

!SLIDE subsection
![Rails logo](/file/assets/images/rails.png)
# Rails desde Zero
##  Instal.lació

!SLIDE subsection
# Instal.lació

1. Git
2. Eines d'entorn
3. RVM, Gemsets i Ruby
4. Bundler
5. Rails

!SLIDE subsection
# Instal.lació
## 1. Git

!SLIDE
Git es pot instal.lar directament descarregant-lo de la web (binari o per compilar)

[http://git-scm.com/](http://git-scm.com/)

ó, mitjançant un gestor de paquets

OSX

    @@@ sh
    $ brew install git

Linux

    @@@ sh
    $ sudo apt-get install git-core

!SLIDE subsection
# Instal.lació
## 2. Eines d'entorn

!SLIDE subsection bullets incremental
# Instal.lacio
## 2. Eines d'entorn

* GCC i llibreries
* Motor de BD i/o bindings per a Ruby

!SLIDE subsection
# Instal.lacio
## 2. Eines d'entorn
### GCC i llibreries

!SLIDE

## OSX
Directament vía XCode (versió >= 4.1.x) ó només el compilador desde
[http://git.io/osxgcc](http://git.io/osxgcc)

## Linux

Compilador GCC + eines

    @@@ sh
    $ sudo apt-get install build-essential

Llibreries bàsiques

    @@@ sh
    $ sudo apt-get install bison openssl libreadline6
    libreadline6-dev curl zlib1g zlib1g-dev libssl-dev
    libyaml-dev libxml2-dev libxslt-dev autoconf

[https://gist.github.com/481301](https://gist.github.com/481301)

!SLIDE subsection
# Instal.lacio
## 2. Eines d'entorn
### Motor de BD i/o bindings per a Ruby

!SLIDE

## OSX

[Homebrew](http://mxcl.github.com/homebrew/)

*"Homebrew is the easiest and most flexible way to install the UNIX tools Apple
didn't include with OS X."*

[https://github.com/mxcl/homebrew/wiki/installation](https://github.com/mxcl/homebrew/wiki/installation)

Un cop instal.lat...

    @@@ sh
    $ brew install sqlite3

ó

    @@@ sh
    $ brew install postgresql

!SLIDE small

## Linux

Utilitzant el gestor de paquets de la nostra distribució (en aquest cas, debian)

SQLite 3

    @@@ sh
    $ sudo apt-get install libsqlite3-0 libsqlite3-dev sqlite3

PostgreSQL

    @@@ sh
    $ sudo apt-get install postgresql postgresql-client postgresql-doc
    libpq-dev

Imagemagick

    @@@ sh
    $ sudo apt-get install imagemagick libmagickcore-dev libmagickwand-dev

Etcétera

    @@@ sh
    $ sudo apt-get install blah blah blah ...

!SLIDE
# ![RVM Logo](/file/assets/images/rvm_logo.png)

!SLIDE subsection
# Instal.lacio
## 3. RVM, Gemsets i Ruby

!SLIDE
## RVM
### [http://beginrescueend.com/](http://beginrescueend.com/)

Instal.lem via

    @@@ sh small
    $ bash < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)

Per a que RVM es carregui automàticament a cada sessió de terminal

    @@@ sh small
    $ echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm" ' >> ~/.bash_profile

Comprobar que està instal.lat correctament

    @@@ sh small
    $ type rvm | head -1

!SLIDE
## Ruby
Un cop RVM está funcionant i passa a gestionar-nos les nostres instal.lacions dels
diferents intèrprets de ruby ja podem procedir a instal.lar-lo

Llistar els diferents intèrprets de Ruby coneguts

    @@@ sh small
    $ rvm list known
    ...

Instal.lar una versió de ruby

    @@@ sh small
    $ rvm install 1.9.3
    $ ruby -v
    ruby 1.9.3p0 (2011-10-30 revision 33570) [x86_64-darwin11.2.0]

Utilitzar un ruby (instalat previament)

    @@@ sh small
    $ rvm use 1.9.2
    Using /Users/user/.rvm/gems/ruby-1.9.2-p290
    $ ruby -v
    ruby 1.9.2p290 (2011-07-09 revision 32553) [x86_64-darwin11.0.0]
    $ rvm use 1.9.3 --default
    Using /Users/user/.rvm/gems/ruby-1.9.3-p0

!SLIDE
## Gemsets

RVM ens proporciona entorns de ruby compartimentalitzats i independents. El que vol
dir que l'intèrpret de ruby, les gemes i l'irb están tots separats i auto-continguts.
Del sistema i entre ells.

Crear un gemset

    @@@ sh small
    $ rvm gemset create rails31
    Gemset 'rails31' created.

Utilitzar-lo

    @@@ sh small
    $ rvm use 1.9.3@rails31
    Using /Users/user/.rvm/gems/ruby-1.9.3-p0 with gemset rails31
    $ gem install blah
    ...
    $ gem install bluh
    ...

!SLIDE subsection
# Instal.lacio
## 4. Bundler

!SLIDE
## Bundler

Bundler gestiona les *dependències d'una aplicació* durant tot el seu cicle
de vida i a través de totes les màquines d'una forma sistemàtica i repetible.

    @@@ sh
    $ gem install bundler --no-rdoc --no-ri

També podem instal.lar-lo en el gemset especial '@global' per a tenir-lo sempre
disponible.

    @@@ sh
    $ rvm use 1.9.3@global
    $ gem install bundler --no-rdoc --no-ri
    $ rvm use 1.9.3@[el gemset que teniem definit]

!SLIDE subsection
# Instal.lacio
## 5. Rails

!SLIDE subsection
## Rails

    @@@ sh
    $ gem install rails
    ...
