Drupal 8: Installation Guide
============================

This guide will descripe steps and hacks for installing Drupal 8 using
Composer, Drush and standard MySQL cli client.

Prerequisite
------------

-  `PHP <http://php.net>`__ v5.3.2+
-  `Composer <https://getcomposer.org/>`__
-  Your ``PATH`` shell variable includes the path to Composer binaries
   at ``$HOME/.composer/vendor/bin``
-  `MySQL <http://mysql.com/>`__ 5.1+

Resources
---------

-  `Drush 8 installation using
   Composer <http://whaaat.com/installing-drush-8-using-composer>`__
-  `Composer
   timeout <http://stackoverflow.com/questions/18917768/why-composer-install-timeouts-after-300-seconds>`__
-  `MySQL
   Collation <http://dev.mysql.com/doc/refman/5.7/en/show-collation.html>`__

Goal
----

Install latest `Drupal <http://drupal.org>`__ 8 instance using Drush
installed through Composer. Drupal will use MySQL database.

Installation Steps
------------------

Each installation step comes with its own command lines examples and
notes for more help.

1. Install Drush
~~~~~~~~~~~~~~~~

To bootstrap Drupal 8, we need Drush 8, which isn't stable by the time
of writing this guide.

If you are installing Drush for the first time, use the following
command:

.. code:: bash

    export COMPOSER_PROCESS_TIMEOUT=600 # default 300
    sudo composer self-update # Make sure that composer is updated
    composer global update # Update all global packages to prevent conflict in dependency versions
    composer global require --prefer-dist drush/drush:dev-master

*NOTES*: \* The ``export`` command will prevent composer from running
into timeout error while install *psy/psysh* package. \* We are using
composer ``--prefere-dist`` flag to prevent composer from downloading
the source code of every required package. \* We are not using
``drush/drush:8.*`` package because drush 8 is not stable by the time of
writing this guide. \* Composer will not install any package without
stable version by default according to:
https://groups.google.com/d/topic/composer-dev/\_g3ASeIFlrc/discussion

If you already has drush installed, or you want to change the installed
version use the following command:

.. code:: bash

    composer global require drush/drush:7.*
    # OR
    composer gloabl require drush/drush:dev-master

To test drush version:

.. code:: bash

    drush --version
    # output should be something like:
    # Drush Version  :  8.0.0-rc3

*NOTES*: \* Drush 8 requires special xdebug configuration, if you don't
have *xdebug* php extension installed, ignore the following commands:

.. code:: bash

       sudo vi /etc/php5/cli/php.ini # Or find the used PHP configuration file by running: `drush status` command.
       # You are now in `vi` command mode, type the following sequence of characters to move in `vi`
       # Go
       # You are now in `vi` edit mode, just add the followin lines to the end of file
       [xdebug]
       xdebug.max_nesting_level=256
       # Hit [Esc] button and type
       # :x

2. Download Drupal
~~~~~~~~~~~~~~~~~~

We will use drush to download Drupal 8 instance. By default, drush will
download Drupal to a folder in the current directory with schema
``drupal-x-x-x``

.. code:: bash

    drush dl drupal-8 --select --all --drupal-project-rename

| *NOTES*: \* We use ``--drupal-project-rename`` to rename the project
folder name, which defaults to "*drupal*\ ". You can rename the folder
any name you like be providing the new name after the
``--drupal-project-rename`` switch.
|  For more help: ``drush help dl`` \* We use ``--select --all`` because
Drupal 8 doesn't have a stable version by the time of writing this
guide.

Now, if used the previous command as is, you have a new folder called
"*drupal*\ " in the current directory. Go ahead and check the downloaded
files.

3. Install Drupal
~~~~~~~~~~~~~~~~~

We will use MySQL database for Drupal installation. For this we will
connect to mysql server using mysql cli client with the root username
and password.

For demonstration will assume the following mysql steup: \* 'root'
passowrd: root \* mysql hostname: localhost \* mysql port: *DEFAULT* \*
Drupal mysql user: drupal *(User already exists in database)* \* Drupal
mysql pass: drupalpass

.. code:: bash

    mysql -u root -proot -e 'CREATE DATABASE drupal8 COLLATE = "utf8_general_ci"; GRANT ALL ON drupal8.* TO "drupal"@"localhost";'

*NOTES*: \* If you want to create the mysql user "drupal" add the
following code before the last semicolon:
``IDENTIFIED BY PASSWORD "drupalpass"``

Now go to the Drupal folder and use ``drush si`` command.

For demonstration will assume the following setup: \* Current Working
Directory: . \* Drupal files root: ./drupal \* Drupal Super Admin name:
sadmin \* Drupal Super Admin pass: sadminpass \* Drupal Super Admin
mail: sadmin@example.com

.. code:: bash

    cd drupal
    drush si minimal --account-name=sadmin --account-pass=sadminpass --account-mail=sadmin@example.com --db-url=mysql://drupal:drupalpass@localhost/drupal8

*NOTES*: \* You can add additional switches to the ``site-install``
command like ``--site-mail`` and ``--site-name``. For more help:
``drush help si``

4. Run Drupal
~~~~~~~~~~~~~

You have to options to run your Drupal site now: \* HTTP Server (Apache
Virtual Host/Nginx) \* Drush ``runserver``

There are plenty of resources online to help you setup HTTP Server. It
requires few configurations but this is usually how your site will run
in production environment. For development environmnet the second option
requires no steup because it uses PHP's buil-in http server.

.. code:: bash

    drush rs

*NOTES*: \* The output will indicate the exact URL to access your Drupal
site. *(Defaults to: http://127.0.0.1:8888)* \* The ``minimal`` profile
uses *Stark* theme, so you'll properly need to change to more visual
theme.
