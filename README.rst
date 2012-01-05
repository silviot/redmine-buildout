================
Redmine buildout
================

About
=====

A `buildout <http://www.buildout.org/>`_ configuration to deploy `redmine <http://www.redmine.org/>`_ project management.

To configure the database edit the top of the file buildout.cfg.

So far you can configure the ``production-database`` name, the ``database-adapter`` and the ``http-server-port``.


As with all buildouts, you'll need to issue a

``python bootstrap.py``

followed by a 

``./bin/buildout``

this will download and install redmine in the local directory.

After completion you can start the server:

``./bin/supervisord``

and point your browser to http://127.0.0.1:3000/ to browse your new redmine site.

To stop the server use

``./bin/supervisorctl shutdown``

and to restart it

``./bin/supervisorctl restart redmine``


The code will live in ``parts/redmine`` while the data will be stored in ``var/`` and in the database.