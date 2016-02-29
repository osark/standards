How to Dependency Injection in drupal ?
=======================================

we are going to explain how dependency injection with twig as example .

Resources
---------

-  `Late Static
   Binding <http://php.net/manual/en/language.oop5.late-static-bindings.php>`__
   .
-  `ClassResolver <https://api.drupal.org/api/drupal/core!lib!Drupal!Core!DependencyInjection!ClassResolver.php/class/ClassResolver/8>`__
   .
-  `getInstanceFromDefinition <https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21DependencyInjection%21ClassResolver.php/function/ClassResolver%3A%3AgetInstanceFromDefinition/8>`__
   .

Dependency Injection
~~~~~~~~~~~~~~~~~~~~

In Dependency Injection we have over three solutions to load and render
TWIG as example

1. By implement ``ContainerInjectionInterface`` interface in your controller
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

implement this interface you must add ``create`` method like this

.. code:: bash

        class CustomController implements ContainerInjectionInterface {

            protected $twig ;

            public function __construct(\Twig_Environment $twig)
            {
                $this->twig = $twig ;
            }

            public static function create(ContainerInterface $container)
            {
                return new static(
                    $container->get('twig')
                );
            }

        }

    ``public static function create(ContainerInterface $container)``

-  make sure your function is public and static because it called
   without instance of your controller

    ``return new static();``

-  this new concept called (late static binding LSP) start with php 5.3+
   you will find info
   `here <http://php.net/manual/en/language.oop5.late-static-bindings.php>`__

-  more info `self vs
   static <http://stackoverflow.com/questions/5197300/new-self-vs-new-static>`__

    ``$container->get('twig')``

-  this load twig container and send to constructor as parameter .

    ``protected $twig ;``

-  declare a variable , you can avoid this step and use magic function
   as you like .

    ``public function __construct(\Twig_Environment $twig)``

-  in constructor must receive twig as parameter and assign to protected
   twig variable .

*NOTES*:

-  The responsible class about call your create function is
   `ClassResolver <https://api.drupal.org/api/drupal/core!lib!Drupal!Core!DependencyInjection!ClassResolver.php/class/ClassResolver/8>`__
   and method is
   `getInstanceFromDefinition <https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21DependencyInjection%21ClassResolver.php/function/ClassResolver%3A%3AgetInstanceFromDefinition/8>`__

2. By implement ContainerAwareInterface interface in your controller
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  After implement this interface you must add (setContainer) method
   like this .

.. code:: bash

        class CustomController implements ContainerAwareInterface {

            protected $twig ;

            public function setContainer(ContainerInterface $container = null)
            {
                $this->twig = $container->get('twig') ;
            }

        }

``$this->twig = $container->get('twig') ;`` to assign twig container to
twig variable

*NOTES*:

-  make sure you are implement (ContainerAwareInterface)[#]
-  The responsible class about call your create function is
   `ClassResolver <https://api.drupal.org/api/drupal/core!lib!Drupal!Core!DependencyInjection!ClassResolver.php/class/ClassResolver/8>`__
   and method is
   `getInstanceFromDefinition <https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21DependencyInjection%21ClassResolver.php/function/ClassResolver%3A%3AgetInstanceFromDefinition/8>`__

3. By get container directly *( not recommended )*
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: bash

    $twig = \Drupal::getContainer()->get('twig') ;

Common Questions
----------------

\* Whats the difference between 3 ways ?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

No mainly difference between all ways but first one required you to receive twig variable in the constructor as parameter .
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

\* I Cannot see the twig error just one message for all cases ?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- You should make sure that your logging and errors is enable '' yoursite/admin/config/development/logging '' .
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

