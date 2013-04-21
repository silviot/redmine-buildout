================
Redmine buildout
================


About
=====
A `buildout <http://www.buildout.org/>`_ configuration to deploy
`redmine <http://www.redmine.org/>`_ project management.

To configure the database edit the top of the file buildout.cfg.
You'll need to create the database too.
The default is a postgresql database named redmine.
Edit buildout.cfg to change these settings.

So far you can configure the ``production-database`` name, the ``database-adapter`` and the ``http-server-port``.


Prerequisites
=============
You will need ruby and ruby-dev installed. Tested with ruby 1.8.
On Ubuntu (and probably all other debian-based distros)

``sudo apt-get install build-essential libopenssl-ruby ruby1.8-dev libmagickwand-dev libmagickcore-dev``

will install prerequisites

Installation
============
As with all buildouts, you'll need to issue a

``python bootstrap.py``

followed by a

``./bin/buildout``

this will download and install redmine in the local directory.

Install the database adapter of choice to the local gem repo::

    ./bin/gem1.8 install pg

After completion you can prepare the database structure::

    cd parts/redmine
    RAILS_ENV=production ../../bin/rake db:migrate

and start the unicorn server through supervisor::

    cd ../..
    ./bin/supervisord

Point your browser to http://127.0.0.1:3000/ to browse your new redmine site.

To stop the server use::

    ./bin/supervisorctl shutdown

and to restart it::

    ./bin/supervisorctl restart redmine

You will probably want some basic data set up in the database::

    cd parts/redmine
    RAILS_ENV=production ../../bin/rake redmine:load_default_data

Or, if you're upgrading::

    cd parts/redmine
    RAILS_ENV=production ../../bin/rake db:migrate RAILS_ENV=production
    RAILS_ENV=production ../../bin/rake redmine:plugins:migrate RAILS_ENV=production


The code will live in ``parts/redmine`` while the data
will be stored in ``var/`` and in the database.


Postgresql caveat
=================

If you Postgresql in a region with a sane date format (d/m/y)
you'll need to change the redmine db option DATESTYLE to US::
    ALTER DATABASE redmine SET DATESTYLE=US;

