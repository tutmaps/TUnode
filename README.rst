Tunode
========================

Install Geonode and create new template for editing on GitHub

Installation
------------

Install geonode with::

    $ sudo add-apt-repository ppa:geonode/stable

    $ sudo apt-get update

    $ sudo apt-get install geonode
    
    $ geonode createsuperuser

    $ sudo geonode-updateip 127.0.0.1

Create a new template based on the geonode example project.::
    
    $ django-admin.py startproject TUnode --template=https://github.com/GeoNode/geonode-project/archive/master.zip -epy,rst 
    $ sudo pip install -e TUnode

.. note:: You should NOT use the name geonode for your project as it will conflict with the default geonode package name.

Usage
-----

Edit /etc/geonode/local_settings.py content by setting the SITEURL and SITENAME.

Edit the file /etc/apache2/sites-available/geonode.conf and change the following directive from:

    WSGIScriptAlias / /var/www/geonode/wsgi/geonode.wsgi

to:

    WSGIScriptAlias / /path/to/TUnode/TUnode/wsgi.py

Add the "Directory" directive for your folder like the following example:

    <Directory "/home/vagrant/TUnode/TUnode/">

       Order allow,deny

       Options Indexes FollowSymLinks

       Allow from all

       Require all granted

       IndexOptions FancyIndexing
       
    </Directory>

Restart apache::

    $ sudo service apache2 restart

Edit the templates in my_geonode/templates, the css and images to match your needs.

In the my_geonode folder run::

    $ python manage.py collectstatic


