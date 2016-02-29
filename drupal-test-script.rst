Drupal Testing Scripts
######################

Sometimes you want to test a function that needs Drupal to be fully
strapped without waiting for certain user action.

We'll use Drush ability to run any script file after bootstrapping
Drupal.

.. code:: bash

    drush scr migs_donation_test.php --script-path=`pwd`/sites/all/modules/custom/migs_donation/tests

Be Careful
----------

-  Don't modify database
-  You can run any function from command line directly
-  For more information about Drush scr command: ``drush help scr``

