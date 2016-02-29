Twig Debug
==========

Purpose
-------

During Twig development, we need to enable Twig debugging to see what
are the template suggestions and which files to override.

Outline
-------

-  Enable local settings
-  Use development service yml file
-  Override Twig parameters

Resources
---------

-  `Debugging compiled Twig
   templates <https://www.drupal.org/node/1903374>`__

Guide
-----

1. Copy ``sites/example.settings.local.php`` to
   ``sites/default/settings.local.php``
2. Edit ``sites/default/settings.local.php`` line 92 to change
   ``DRUPAL_ROOT . '/sites/development.services.yml`` to
   ``__DIR__ . '/../development.services.yml``
3. Uncomment the files that include the ``settings.local.php`` in
   ``settings.php``
   ``php    if (file_exists(__DIR__ . '/settings.local.php')) {  include __DIR__ . '/settings.local.php';    }``
4. Edit ``sites/development.service.yml`` to override Twig parameters.
   Add the following lines with spaces to the end of the file.
   ``yml    parameters:  twig.config:    debug: true``

