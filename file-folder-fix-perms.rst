Fix Files & Folders Permissions
###############################

Introduction
============

Default file permissions should be ``644`` and default folder
permissions should be ``755``. Sometimes while working on partitions
that doesn't recognize *Linux File Permissions* such as: *NTFS*, all
files and folders permissions turns to ``777`` which propose a *major*
security risk.

Find Bad Perms
==============

To find bad permissions in certain *folder path*: ``sites/all`` for
example, use the following command:

.. code:: bash

        find sites/all/ \( -type d -perm -o+w -exec ls -dl '{}' \; \) , \( -type f -perm -o+x -exec ls -l '{}' \; \) | less

This will list all files and folders with bad permissions. You can
finish the command by pressing ``q`` key.

Fix Bad Perms
=============

To fix all bad permissions of the previously found files and folders,
use the following command:

.. code:: bash

        find sites/all/ \( -type d -perm -o+w -exec chmod 755 '{}' \; \) , \( -type f -perm -o+x -exec chmod 644 '{}' \; \)

This command is silent, and you'll see no output until it finishes and
return the prompt back to you.

*PLEASE NOTE:* The command will operate on *all* files and folders found
by the first find command. Make sure that you review the list or be more
specific with the folder path.
