================
Redmine buildout
================

About
=====

A `buildout <http://www.buildout.org/>`_ configuration to deploy `redmine <http://www.redmine.org/>`_ project management.

To configure the database edit the top of the file buildout.cfg.

As with all buildouts, you'll need to issue a

``python bootstrap.py``

followed by a 

``bin/buildout``

this will download and install redmine in the local directory.

The code will live in ``parts/redmine`` while the data will be stored in ``var/`` and in the database.