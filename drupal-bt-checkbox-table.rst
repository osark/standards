Problem
=======

| Drupal Bootstrap theme display messed up table when table only have
check-boxes. For example, try view the permission table in Bootstrap
based theme.
| This issue can also reproduced with ``webform`` module. Create a new
*webform* content with at least one component of type *Grid*. Add at
least 3 options and 3 questions.

*Example of Bootstrap Table Issue*
|Drupal\_Bootstrap\_checkbox\_table\_issue|

Proposed Solution
=================

The problem occurs because Drupal adds class ``checkbox`` to the ``td``
and ``th`` tags. Default bootstrap css rules for ``.checkbox`` is

.. code:: CSS

    .radio, .checkbox {
        position: relative;
        display: block;
        min-height: 20px;
        margin-top: 10px;
        margin-bottom: 10px;
    }

The problem occurs because the two properties ``position`` and
``display``. To solve the probme you can use the following css rule:

.. code:: CSS

    td.checkbox, th.checkbox {
        position: static;
        display: table-cell;
        text-align: center;
    }

``text-align`` property is used because usually the *checkbox* label is
hidden.

*Final Result* |Drupal\_Bootstrap\_checkbox\_table\_fixed|

.. |Drupal\_Bootstrap\_checkbox\_table\_issue| image:: http://dev-server/open-source/opensourcewiki/uploads/e439dd5bc332e76d9801fda7fa10e601/Drupal_Bootstrap_checkbox_table_issue.png
.. |Drupal\_Bootstrap\_checkbox\_table\_fixed| image:: http://dev-server/open-source/opensourcewiki/uploads/3a3020500077e80c41d0828285f6bce9/Drupal_Bootstrap_checkbox_table_fixed.png
