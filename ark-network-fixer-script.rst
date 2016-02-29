Internal Network Fixer
######################

Challenge
=========

Automatically change all IPs of *ArkDev* internal servers in our local
``/etc/hosts`` file according to current machine local network *1/2*.

Network Fixer Script **ark\_network\_fixer.sh**
===============================================

This script checks the current local network, and make sure that you
have entries in you ``/etc/hosts`` that has IPs on the wrong
sub-network, and changes these entries automatically.

You can call this script manually. It has an interactive mode that show
the changed ``/etc/hosts`` file, and can take backup files of your
``/etc/hosts`` files before fixing it.

To run this script manually you have to be *root* or use ``sudo``
command.

-  Download this file from the wiki project files.
-  Change file permissions to executable
-  Change Owner to *root*
-  Place the file in your ``/usr/local/bin`` folder

.. code:: bash

    wget http://dev-server/open-source/opensourcewiki/raw/master/ark_network_fixer.sh
    chmod 755 ark_network_fixer.sh
    sudo chown root:root ark_network_fixer.sh
    sudo mv ark_network_fixer.sh /usr/local/bin

Network Change Dispatcher **99ark\_network\_fixer**
===================================================

This simple script is used by *NetworkManager* to detect any changes in
network interfaces and call the **ark\_network\_fixer.sh** script.

If you don't have *NetworkManager* on your system, you can consult your
distribution documentation or online help and find where you need to
call the **ark\_network\_fixer.sh** script.

This file depends on **ark\_network\_fixer.sh** and you must follow the
previous steps to download and configure **ark\_network\_fixer.sh** for
this file to work. But **ark\_network\_fixer.sh** doesn't need this file
to work.

-  Download this file from the wiki project files.
-  Change file permissions to only executable by owner.
-  Change Owner to *root*
-  Place the file in ``/etc/NetworkManager/dispatcher.d`` folder

.. code:: bash

    wget http://dev-server/open-source/opensourcewiki/raw/master/99ark_network_fixer
    chmod 700 99ark_network_fixer
    sudo chown root:root 99ark_network_fixer
    sudo mv 99ark_network_fixer /etc/NetworkManager/dispatcher.d

