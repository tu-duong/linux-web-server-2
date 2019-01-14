# Linux web server configuration

## i. The IP address and SSH port so your server can be accessed by the reviewer.
18.234.255.183 port 22

## ii. The complete URL to your hosted web application.
http://18.234.255.183

## iii. A summary of software you installed and configuration changes made.

  * Apache: apache2
  * Wsgi: libapache2-mod-wsgi-py3
  * Flask: python3-flask
  * SQLAlchemy: python3-sqlalchemy
  * SQLAlchemy support for Flask: python3-flask-sqlalchemy
  * Oath2: python3-oauth2client

These packages can be installed by using the command: sudo apt-get install <package name>
 
## iv. Step by step configuration

* update packakges by sudo apt-get update and sudo apt-get upgrade

* install required packages (see iii above)

* create users student and grader. secure access to .ssh and authorized_keys. Create and update ssh keypair. Give student and grader access as sudoer

* configure ufw firewall, default block all incoming and allow all outgoing, enable required ports (2200, 80, 123, 22 - 22 to be removed later). Update Port 2200 at /etc/ssh/sshd_config. Add Port 2200 in Lightsail. Test connection with new Port 2200. If success, delete Port 22 from ufw, sshd_config, and Lightsail console.

* create catalog_wsgi files.
    * $ sudo nano /var/www/catalog/catalog.wsgi
    * #!/usr/bin/python3
    * import sys
    * import logging
    * logging.basicConfig(stream=sys.stderr)
    * sys.path.insert(0, "/var/www/catalog/")

    * from project import app as application
    * application.secret_key = 'your_secret_key'

* create, configure, enable catalog.conf file
    * $ sudo nano /etc/apache2/sites-available/catalog.conf
    * Update server name, WSGIScriptAlias, Director (/var/www/catalog)
   
* Link catalog.conf file and restart apache2 server
    * sudo a2ensite catalog.conf
    * sudo service apache2 restart 

## v. A list of any third-party resources you made use of to complete this project.

  * http://terokarvinen.com/2017/write-python-3-web-apps-with-apache2-mod_wsgi-install-ubuntu-16-04-xenial-every-tiny-part-tested-separately

 * http://flask.pocoo.org/docs/1.0/deploying/mod_wsgi/

  * https://www.bogotobogo.com/python/Flask/Python_Flask_HelloWorld_App_with_Apache_WSGI_Ubuntu14.php

  * https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-18-04
