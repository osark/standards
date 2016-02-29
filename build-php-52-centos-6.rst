Build PHP 5.2 on CentOs 6
#########################

Notice
------

| This guide can easily destroy your CentOs system and definitely not
secure.You'll downgrade some packages and install insecure version of
PHP.
| **Use virtual box and only for testing purposes.**

Prerequisite
------------

-  CentOs 6.7
-  ``git``
-  *root* access
-  Good internet connection

General Steps
-------------

1. Download `phpenv <https://github.com/CHH/phpenv>`__ in your home
   directory using ``git clone https://github.com/CHH/phpenv.git``
2. Run ``sudo ~/phpenv/install.sh && mkdir ~/.phpenv/plugins``
3. Download `php-build <https://github.com/php-build/php-build>`__ using
   ``git clone https://github.com/php-build/php-build.git ~/.phpenv/plugins/php-build``
4. Downgrade libxml2 rpm package
   ``sudo yum downgrade libxml2-2.7.6-1.el6.rfx``
5. Download PHP 5.2 build dependencies
   ``bash    sudo yum -y install gcc make gcc-c++ cpp kernel-headers.x86_64 libxml2-devel openssl-devel \ bzip2-devel libjpeg-devel libpng-devel freetype-devel openldap-devel postgresql-devel \ aspell-devel net-snmp-devel libxslt-devel libc-client-devel libicu-devel gmp-devel curl-devel \ libmcrypt-devel unixODBC-devel pcre-devel sqlite-devel db4-devel enchant-devel libXpm-devel \ mysql-devel readline-devel libedit-devel recode-devel libtidy-devel``
6. Build PHP 5.2 using *phpenv* ``phpenv install 5.2.17``

