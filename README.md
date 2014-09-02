mezzanine_test
==============

repo setup to work through mezzanine tutorials

will be using virtualenv to encase the project:

	mkvirtualenv mezzanine_test --python=/usr/bin/python2.7

using python 2.7 because the idea is to use Fabric for deployment eventually .. not in this repo most likely, but want to get used to everything without Python 3.

	$ sudo apt-get install libjpeg8 libjpeg8-dev
	$ sudo apt-get build-dep python-imaging

and from *within virtualenv*:

	$ sudo pip install mezzanine

(the following are optional and will require adding to the conf files of the project)

South for DB migrations:
	
	$ sudo pip install south

psycopg2 for PostgreSQL (which I will be using - might require libpq-dev or postgresql-devel):

	$ sudo pip install psycopg2

django-compressor for merging JS/CSS assets:

	$ pip install django-compressor

after successful installation, should have the same list of requirements as shown in requirements.txt

create the project:

	$ mezzanine-project test_project

at this point, I needed to edit test_project/local_settings.py in order to add the proper DB connections.  Use local_settings.py as it contains the local environment settings so you don't have to manually change the DB location or the Debug state when deploying.

need to create the DB itself in the postgres admin prompt, I named the db: mezz_test_db

    $ sudo -u postgres psql postgres
    =# createdb mezz_test_db

Then we need to create the database within the PostgreSQL server.

	CREATE DATABASE mezz_test_db
		WITH ENCODING='UTF8'
		OWNER=mezz
       		CONNECTION LIMIT=-1;

after this, we can create the tables, and then test it:

	cd test_project
	python manage.py createdb --noinput
	python manage.py runserver

uses the default admin UN/PW: admin/default

The next step could be to change the FABRIC settings in settings.py to setup deployment settings

