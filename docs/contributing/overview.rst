.. _contributing:

============
Contributing
============

Development Environment
=======================
Docker is required follow these `install instructions`_.

OSX::

    # install home brew this will also install Xcode command line tool.  Follow all instructions given during install
    $ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)”

    # update brew
    $ brew update

    # install pyenv
    $ brew install pyenv

    # You may need to manually set PYENV_ROOT, open a new terminal and see if it
    # was set by the install proces:

    $ echo $PYENV_ROOT

    ## Setting Manually
    #
    # If your PYENV_ROOT isn't set, you can use either $HOME/.pyenv or the
    # homebrew pyenv directory, /usr/local/opt/pyenv.  Put
    #
    # export PYENV_ROOT=/usr/local/opt/pyenv
    #
    # -or-
    #
    # export PYENV_ROOT="$HOME"/.pyenv
    #
    # in your .bashrc or .bash_profile, or whatever your appropriate dotfile is.
    #
    # ---
    #
    ## Setting with oh-my-zsh
    #
    # You can just use the pyenv plugin.  Open your .zshrc and make sure that
    # this line:
    #   plugins=(git rvm osx pyenv)
    # contains pyenv.  Yours may have more or fewer plugins.
    #
    # If you just activated the pyenv plugin, you need to open a new shell to
    # make sure it loads.

    # install libyaml
    $ brew install libyaml

    # install a few plugins for pyenv
    $ mkdir -p $PYENV_ROOT/plugins
    $ git clone "git://github.com/yyuu/pyenv-pip-rehash.git" "${PYENV_ROOT}/plugins/pyenv-pip-rehash"
    $ git clone "git://github.com/yyuu/pyenv-virtualenv.git" "${PYENV_ROOT}/plugins/pyenv-virtualenv"
    $ git clone "git://github.com/yyuu/pyenv-which-ext.git"  "${PYENV_ROOT}/plugins/pyenv-which-ext"

    ##  Load pyenv-virtualenv when shells are created:
    #
    # To make sure that both of your pugins are loading, these lines should be
    # in one of your dotfiles.
    #
    #     eval "$(pyenv init -)"
    #     eval "$(pyenv virtualenv-init -)"

    # Now that it will load automatically, activate the plugin for this shell:
    $ eval "$(pyenv virtualenv-init -)"

    # install a specific version
    $ pyenv install 2.7.10

    # create a virtual env
    $ pyenv virtualenv 2.7.10 freight-forwarder

    # list all of your virtual environments
    $ pyenv virtualenvs

    # activate your environment
    $ pyenv activate freight-forwarder

    # clone repo
    $ git clone git@github.com:Adapp/freight_forwarder.git

    # install requirements
    $ pip install -r requirements.txt


Style Guidelines
================
Coming soon!

Release Steps
=============
* version++; The verson can be found freight_forwarder/const.py
* Update change log.
* Git tag the version
* $ python ./setup.py bdist_wheel
* Upload to pypi.

Build Documentation
===================

Docker::

    $ pip install freight-forwarder


The freight-forwarder.yml file will have to be updated with your specific docker host info::

    environments:
      alexb: &alexb
        address: "https://172.16.135.137:2376" # <- Change me
        ssl_cert_path: "/Users/alexb/.docker/machine/machines/ff02-dev" # <- Change me
        verify: false

      development:
        local:
          hosts:
            default:
              - *alexb


Then just run Freight to start the documentation containers::

    $ freight-forwarder quality-control --environment development --data-center local --service docs

After the containers start you can find the documentation at: your_container_ip:8080

Make::

    $ cd docs/
    $ pip install -r requirements.txt
    $ make html

The html can found here: ./docs/_build/

.. _install instructions: https://docs.docker.com/installation/
