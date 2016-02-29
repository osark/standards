Zen Coding And Netbeans Templates
#################################

The objective is to write code quickly and efficiently.This tip focuses
on HTML code, because it can be tedious to write, however, the technique
can be applied to other languages using code editor plugins and
different utilities.

.. rubric:: `Zen Coding <https://code.google.com/p/zen-coding>`__

The main principle behind then coding is not to repeat yourself. It
provides a short syntax to write HTML code.

For netbeans, you can find the plugin under
``Tools > Plugins > Available Plugins > Zen Coding``. After installation
and restarting Netbeans, you can start testing in any HTML context files
like ``index.html`` or ``index.xhtml`` and test the following code

::

    html:5
    (header>ul>li>a.item-$*3)+.container>.col-md-6.col-xs-12>p*2

Hit ``Alt``\ +\ ``Ctr``\ +\ ``n`` shortcut to start converting the
sample to actual HTML code

.. code:: html

    <!DOCTYPE HTML>
    <html lang="en-US">
      <head>
        <meta charset="UTF-8">
        <title></title>
      </head>
      <body>

      </body>
    </html

And

.. code:: html

    <header>
        <ul>
            <li>
                <a href="" class="item-1"></a>
                <a href="" class="item-2"></a>
                <a href="" class="item-3"></a>
            </li>
        </ul>
    </header>
    <div class="container">
        <div class="col-md-6 col-xs-12">
            <p></p>
            <p></p>
        </div>
    </div>

For more details check `Zen Coding cheat sheet -
PDF <https://code.google.com/p/zen-coding/downloads/detail?name=ZenCodingCheatSheet.pdf>`__

These tools are here to help, but don't try to overload yourself with
their details. Just keep it simple and enjoy coding with speed.
