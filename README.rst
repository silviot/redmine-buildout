================
Redmine buildout
================


About
=====
A `buildout <http://www.buildout.org/>`_ configuration to deploy `redmine <http://www.redmine.org/>`_ project management.

To configure the database edit the top of the file buildout.cfg. You'll need to create the database too. The default is a postgresql database named redmine.

So far you can configure the ``production-database`` name, the ``database-adapter`` and the ``http-server-port``.


Prerequisites
=============
You will need ruby and ruby-dev installed. Tested with ruby 1.8.
On Ubuntu (and probably all other debian-based distros)

``sudo apt-get install build-essential libopenssl-ruby ruby1.8-dev``

will install prerequisites

Installation
============
As with all buildouts, you'll need to issue a

``python bootstrap.py``

followed by a 

``./bin/buildout``

this will download and install redmine in the local directory.

After completion you can prepare the database structure: cd to the code directory

``cd parts/redmine``

issue

``RAILS_ENV=production ../../bin/rake db:migrate``

and start the unicorn server through supervisor:

``./bin/supervisord``

Point your browser to http://127.0.0.1:3000/ to browse your new redmine site.

To stop the server use

``./bin/supervisorctl shutdown``

and to restart it

``./bin/supervisorctl restart redmine``

You will probably want some basic data set up in the database.

from the ``parts/redmine`` dir issue

``RAILS_ENV=production ../../bin/rake redmine:load_default_data``


The code will live in ``parts/redmine`` while the data will be stored in ``var/`` and in the database.