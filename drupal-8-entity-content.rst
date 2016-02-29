Drupal 8: Content Entities
==========================

Content entities are used to store information in database that can be
translated and revisioned.

Getting Started
---------------

**NOTE**: Make sure you are working on local git repo, to revert back
any unwanted changes, or examining generated codes

1. Use *drupal console* to generate some boilerplate code to get things
   started. 

   .. code-block:: bash

      $ drupal generate:entity:content

  -  The *console* will ask several questions about the new content
     entity, like: the module this entity belongs to, Label and
     machine\_name.
  -  Use *console* help to find what arguments this command accepts.
  -  Revert back all changed files, and remove added one, and repeat the
     ``generate:entity:content`` command using ``--learning`` option.
  -  Examin generated files and changes and try to guess what they do.

2. Until *drupal v0.9.8* the generated code have some issues solve them:

  -  Forms: Find the generated form files and fix them; rename and move
     them according to their content
  -  Routes: Find the two routes that have the same path, change on of
     them. Make sure that changed path has no other dependency pathes.
  -  Links: Use :doc:`Drupal 8 Config Menu Links
     wiki <drupal-8-config-menu-links>` to create a new configuration
     links block at ``admin/config`` page, and the links to main entity
     routes there.

3.  Fields There are two ways to add fields to entities, use both of
    them to add different fields:

    1.  ``ContentEntityBase::baseFieldDefinitions()``
    2.  Using Field UI

4.  Field Validation Use `Entity Validation API in Drupal
    8 <https://www.drupal.org/node/2015613>`__ to add constraint to
    field item properties. Try adding the following validations:

    1.  *Email*
    2.  *Unique*
    3.  *Not Blank*!

5.  Interfaces 
    Use the intreface class to add setters and getters for this content type.

6.  Install your entity Schema If your module was already installed,
    clear the cache. If it wasn't installed yet, install it now to
    install the entity database schema. Examin the create database
    table.

7.  Entity Listing: 
    Try adding few entity instances using the *create
    route* to find the form and examin the listing, there is no entity
    view link in the listing table. Find the listing class and add
    columns to show one or two extra fields and make the name column
    links to entity view URL

Entity Challenges
-----------------

Working with content entity is not a smooth joureny, there are some
challenges that you need to be aware of. 

*  In Drupal 8 there is no module disable. You can either install or uninstall a modules. You can not uninstall a module with content entity, if the content entity table is not empty, or doesn't exist. Try it!
*  Content Entity database schema updates implemented at ``ContentEntityBase::baseFieldDefinitions()`` are applied on only two events (for now):

   * *Cache Rebuild* if the module was enabled and you created the entity class 
   * *Module Install* will apply the updates, which means: 
   * If there was a problem in the ``ContentEntityBase::baseFieldDefinitions()`` method that prevented the entity table from being created, you'll have to create it first by hand and then you can uninstall your module! Use simple command like ``$ echo 'CREATE TABLE entity_machine_name (id int);' | drush sqlc``
* Try to add any validation to fields created throught *Field UI* using only Drupal core, it is not that simple if not impossible for now!
* Uninstall and re-install your module, where are the attached entities?! Use configuration export to persist them.

