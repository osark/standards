Git Bare Repos
##############

Git --bare is a special repository that doesn't contain any working
directory and you cannot directly checkout branches from it. Bare git
repos are most suitable for adding them as remotes to your local
repositories in order to share your changes with other users.

Remote Server
-------------

First initialize bare git

.. code:: bash

       git init --bare <REPO_NAME>.git

The ``<REPO_NAME>`` should be anything related to your project that
contains alphanumeric characters (in both capital and small cases),
underscores, dashes and dots (without and slashes, square and angular
bracket, parentheses or curly braces). Adding ``.git`` suffix is just
for convention, and recommended but not required.

This will create a new directory named ``<REPO_NAME>.git``.

    *Important* *Note*: All developers will access the repository
    through single user via ssh, so it's important to make sure that you
    can access the repository folder through ssh!

Local Users Access
------------------

Now we have an accessible remote repository, we need to add our local
ssh private key in order to automatically authenticate through ssh.

.. code:: bash

       cd ~/.ssh
       ls id_rsa.pub
       # If you don't find this file, use the following command
       # $ ssh_keygen
       # Just agree with all the defaults
       cat id_rsa.pub 

Copy the output from ``~/.ssh/id_rsa.pub``, and append it to the end of
file ``/home/<remote_user>/.ssh/authorized_keys`` in the remote server.
You can download the file through ``FTP`` and update it locally and
upload it again, or you can create it if not found.

To test that ssh authentication is working you can use the following
command

::

    ssh <remote_user>@<remote_server_ip>

If everything works correctly should be logged in to remote server
without being asked for any password.


Git Remote
----------

To find the remote URL , use the following schema:
ssh://@:/path/to/git/bare/repo.git

Each developer will have to add the information of the newly created
repo to their local repository.

.. code:: bash

       cd /path/to/local/git/project
       git remote add <remote_server_alias> <remote_git_url>

For the first/lead developer, you will have to populate the newly
created remote repository with the following command.

::

     git push -u <remote_server_alias> master

If you need to add all branches you can add --all flag as follow:

::

     git push --all -u <remote_server_alias>


Helpful Notes
-------------

-  Add the to your /etc/hosts file, in order to use a simple domain name
   instead of server ip. Now use the domain name instead of the ip in
   all commands.
-   can be any short name that containes alphanumeric and underscores
   character (It's not recommended to use any characters)
-  Default is ``origin``, but you can add as many remotes as you want.
-   is defined only per developer per project, so different developers
   can have different

**For More Information/Details** You can find plenty of resources on the
web.
