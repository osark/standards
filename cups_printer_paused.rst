CUPS shared printer troubleshooting
###################################

Sometimes due to communication errors, the shared printer at
``192.168.1/2.11`` get *paused*.

This is simple issue that a simple *resume* command can bring the
printer back to work.

Here are simple steps to do that. [*All using SSH*\ ] :(

Using Browser
-------------

This is the hard option. First you need to do something called "Port
Forwarding".

*From Shell:*

.. code:: shell

          ssh -L 6310:localhost:631 root@git-server

*From Putty:* Search Google how to configure Putty to do that. Use the
local port: 6310 and remote port:631

Now keep the terminal running and go to browser and use the following
URL: ``http://localhost:6310``

This is the graphical interface for CUPS, the printer management server.
From top navigation menu choose "Administration" (*If asked for
credentials, use the root username and password.*)

Choose ``Manage Printers`` button, to access a list of available
printers. Choose ``shared_printer`` (*This should be the only available
printer*)

From ``Maintenance`` drop down, select ``Resume Printer``. If you can't
find this option, then there is another problem with the printer. You
can check that the printer is actually "On", connected to the server via
USB, with paper in the tray and no paper is jammed inside the printer.

--------------

Server Logs
-----------

If you already have a terminal and want to check if there are any
printer errors, use the following commands:

.. code:: shell

        tac /var/log/cups/error.log | less

This command will list the latest error logs from today. Hit ``q`` to
stop this command and exit back to terminal.

For listing older logs use the following commands:

.. code:: shell

        zcat /var/log/cups/error_log.* | tac | less

This will aggregate all error logs available order that today.

Using the past two commands will list logs in a reverse chronological
order - latest logs first.
