Dev Server Virtual Machines
###########################

Setup
=====

| Dev server has ``vmware`` software to run *Virtual Machines*. There
are currently two virtual machines:
| \* Win12SQL \* win7-Photoshop

All Virtual Machines are located at ``/home/Vm's/``. Each VM has two
``vmnet`` network interfaces to access both sub-networks.

Auto-start
==========

It was requested that both VM's be available after booting the server.
This was achieved using ``/etc/rc.local`` script.

A version of the *rc* script can be found on this wiki project files as
``rc.local`` on project root.

VMWare cmd
==========

To manage vmware VM's from command line, use ``vmrun`` command. `Online
help for the
command <https://www.vmware.com/support/ws55/doc/ws_learning_cli_vmrun.html>`__
