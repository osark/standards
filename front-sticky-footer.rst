Sticky Footer
=============

Problem Statement
-----------------

How to pin footer to be fixed to bottom of browser window without
min-height for content cell

Sample CSS
----------

.. code:: css

    html {
      position: relative;
      min-height: 100%;
    }
    body {
      /* Margin bottom by footer height */
      margin-bottom: 60px;
    }
    .footer {
      position: absolute;
      bottom: 0;
      width: 100%;
      /* Set the fixed height of the footer here */
      height: 60px;
    }

Common Issues
-------------

-  Footer must be absolute from ``<html>``. Avode any parents to
   ``.footer`` with position relative.
-  If you don't need to put a fixed height to your footer, you need to
   change "margin-bottom" at the ``body`` in the different media queries
   in your css

Resources
---------

https://getbootstrap.com/examples/sticky-footer/
