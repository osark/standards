`Conditional Fields
Module <https://www.drupal.org/project/conditional_fields>`__ define
dependencies between fields based on their states and values.

Module define to entities for each condition: \* Dependent: The field
that depends on other field \* Dependees: The controlling field on which
other fields depend on its state.

Symptom
-------

*Dependent* field values not save on form submit.

Bug Resources:
--------------

-  https://www.drupal.org/node/2061405
-  https://www.drupal.org/node/1542706#comment-6773474

Fix:
----

In **Values input mode**, instead of using "*Insert value from
widget...*\ ", choose any option of group "*Set of values*\ ".
