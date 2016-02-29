Drupal 8: Menu Links in Admin Config
====================================

| Drupal 8 ``admin/config`` is the place to manage all site
configuration.
| Adding custom links under existing sections is easy.
| Adding custom sections is not so easy for beginners.

Challenge
---------

Add new custom section in ``admin/config`` and add several links in this
new section.

Live Example
------------

This example is taken from Drupal 8 installed instance. Because we have
the source code of Drupal 8 in plain text, we can examine how Drupal
used its own system to include sections on links in the ``admin/config``
page. You can examin how *Media* section is implemented in the following
files: \* ``core/modules/system/system.router.yml`` \*
``core/modules/system/system.links.menu.yml`` You'll find other sections
in the same files. And even the implementation of ``admin/config`` route
iteself.

Assumptions
-----------

-  All configurations are part of a custom module *myModule* .
-  You have custom route, that you want to add under new section.
-  Route path: /admin/config/myModule/config
-  Section

   -  Title: myModule Configuration
   -  path: /admin/config/myModule

Abstract Guideline:
-------------------

1. Create at least 2 routes, one for the section and any other route to
   be added as links in this section.
2. Create at least 2 links, one for the section and any other menu link
   to be added to this section.

Solution
--------

Keep in mind the following information about your module. \* Module
Path: ``modules/custom/myModule`` \* Router File:
``modules/custom/myModule/myModule.router.yml`` \* Links File :
``modules/custom/myModule/myModule.links.menu.yml`` Here is the sample
code to for the routes.

Router Files
~~~~~~~~~~~~

.. code:: yml

    # file modules/custom/myModule/myModule.router.yml

    # ... add your other routes

    # Section Route in `admin/config` page
    myModule.admin_config:
      path: 'admin/config/myModule'
      defaults:
        _controller: '\Drupal\system\Controller\SystemController::systemAdminMenuBlockPage'
        _title: 'myModule'
      requirements:
        _premission: 'access administration pages'

    # Example of any existing routes
    myModule.settings:
      path: 'admin/myModule/settings'
      defaults:
        _form: '\Drupal\myModule\Form\myModuleSettingsForm'
        _title: 'myModule Settings'
      requirements:
        _permission: 'administer myModule configuration'
      options:
        _admin_route: TRUE

| **Notes**
| \* Route names are arbitary; they can be anything. \*
*myModule.settings* route can be any route with **any** configuration,
there are no mandatory properties. \* *myModule.admin*\ config\_ route
can have any title, use other properties as is. You can test other path
values but at least not \_controller property!

Links Menu Files
~~~~~~~~~~~~~~~~

.. code:: yml

    # file modules/custom/myModule/myModule.links.menu.yml

    # ... add your other menu links

    # Section Menu Link in `admin/config` page
    myModule.admin_config:
      title: 'myModule'
      parent: system.admin_config
      description: 'Administer myModule'
      route_name: myModule.admin_config

    # Example of any link you want to include under 'myModule' section
    myModule.settings:
      title: 'myModule Settings'
      parent: myModule.admin_config
      description: 'Manage myModule behavior through settings form'
      route_name: myModule.settings

**Notes** \* Menu links names use the same router name for consistancy.
Is it a must? \* You can include any other configuration link under the
new section if you use: ``parent: myModule.admin_config``

Cache Rebuild
~~~~~~~~~~~~~

Rebuild your cache for the new section and links to be visible.

Common Problems
---------------

The section might not appear after clearing the cache, check the
following points: \* Spelling of the all router names and menu link
names \* The section must have at least on link for it to appear in
``admin/config`` page \* In ``links.menu.yml`` file, use link names in
``parent``

To Do
-----

1. Test other properties that may affect the section menu link like
   ``weight`` and ``position``

