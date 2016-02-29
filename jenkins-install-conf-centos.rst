Jenkins Installation & Configuration *CentOs*
#############################################

Practical guide for installing Jenkins as part of setting up *Continuous
Integration (CI)* server.

This guide can be applied to any Linux distribution, but tested only on
Centos 6.6.

Steps Outline
=============

-  `Create bare git repository on server <#git-bare-repo>`__
-  `Jenkins Installation <#jenkins-installation>`__
-  `Jenkins Security Configuration <#jenkins-security-configuration>`__
-  `Jenkins Git Configuration <#jenkins-git-configuration>`__

Git Bare Repo
=============

Create a new user called ``git`` that will be used to create the bare
git repo. Add ssh ``authorized_keys`` file to allow ssh authentication
without password. Prevent interactive ssh login to ``git`` user account
by changing login shell to the special ``git-shell``.

.. code:: bash

    adduser git
    su git - # Switch to git user
    cd
    mkdir .ssh && chmod 700 .ssh
    touch .ssh/authorized_keys && chmod 600 .ssh/authorized_keys
    exit # exit git shell and return to root user
    cat /root/.ssh/authorized_keys >> /home/git/.ssh/authorized_keys
    which git-shell >> vi /etc/shells
    chsh git -s `which git-shell`

Make sure that the server has Git installed, then follow the `guide to
create new bare git repository <git-bare>`__.

Post Git Init Checks
--------------------

After creating the new Git bare repository, remember to: \* You have
added all allowed users passwords in the ``.ssh/authorized_keys`` file
in ``git`` home directory.

Jenkins Installation
====================

Jenkins `official documentation for
installation <https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins>`__
covers the basic steps and gotchas that you might face while installing
Jenkins.

Post Installation Checks
------------------------

-  Make sure that Jenkins default port (8080) is open in the firewall
   configuration.
-  Jenkins will try to execute binaries from ``/tmp`` folder. Make sure
   that ``/tmp`` folder is not mounted with option ``noexec`` using
   ``mount`` command. Otherwise (change Jenkins temporary
   folder](#change-jenkins-temp-folder)

Change Jenkins Temp Folder
--------------------------

If you have problems starting Jenkins and the log say it can't execute
with exception like ``InvocationTargetException`` "Operation not
permitted", most probably you'll need to change the temporary folder
that Jenkins uses.

1. Open ``/etc/sysconfig/jenkins``.
2. Change the Java options line

-  *From*: JENKINS\_JAVA\_OPTIONS="-Djava.awt.headless=true"
-  *To*: JENKINS\_JAVA\_OPTIONS="-Djava.awt.headless=true
   -Djava.io.tmpdir=$JENKINS\_HOME/tmp"

3. Find the ``JENKINS_HOME`` directory value from the same file
   (Usually: ``/var/lib/jenkins``).
4. Create an empty ``tmp`` folder inside the ``JENKINS_HOME`` directory.
5. Make sure that the ``tmp`` folder is writable by the Jenkins user.
6. Start Jenkins: ``service jenkins start``

Jenkins Security Configuration
==============================

By default Jenkins allow anonymous users to do everything. To tighten
Jenkins security we will prevent anonymous user from doing anything.
Only authenticated user will be able to do everything.

For small and medium teams, we will use Jenkin's Own User database. The
`official
documentation <https://wiki.jenkins-ci.org/display/JENKINS/Standard+Security+Setup#StandardSecuritySetup-Jenkins%27OwnUserDatabase>`__
explains the steps clearly.

To disallow anonymous users from accessing any information on Jenkins,
we will use `Matrix-based
Security <https://wiki.jenkins-ci.org/display/JENKINS/Standard+Security+Setup#StandardSecuritySetup-MatrixbasedSecurity>`__

-  Go to Jenkins Dashboard, usually ``http://server_domain:8080``.
-  Select *Manage Jenkins* then *Configure Global Security*.
-  Click *Enable Security*.
-  Select *Jenkins' own user database*.
-  In *Authorization* section, select *Logged-in users can do anything*.
-  Make sure you click ``Save``
-  You'll be promoted to create your first user. Remember the username
   and password.

Jenkins Git Configuration
=========================

By default, Jenkins doesn't come with Git plugin. You'll need to find
and install the ``Git Plugin``, configure Jenkins ssh authorization to
access the *bare Git repo*.

-  Go To ``http://_server_:8080/pluginManager/available``
-  Search for ``git``
-  Select and Install ``GIT plugin``
-  Restart Jenkins
-  Go to ``JENKINS_HOME`` directory (defaults to ``/var/lib/jenkins``.
-  Change user to jenkins: ``su jenkins``
-  Generate ssh keys: ``ssh-keygen``
-  Make sure that the generated key is found at
   ``$JENKINS_HOME/.ssh/id_rsa``
-  The ``.ssh`` folder has permission ``700`` and the ``id_rsa`` file
   has permission ``600``
-  Append file ``$JENKINS_HOME/.ssh/id_rsa.pub`` to git user
   ``authorized_keys`` file

   .. code:: bash

       cat /var/lib/jenkins/.ssh/id_ras.pub >> /home/git/.ssh/authorized_keys

-  When creating a new workspace, make sure that the authorization is
   using ``jenkins`` private key file.

Jenkins Git Plugin and CentOS 6.6
---------------------------------

Jenkins Git Plugin requires git of version ``1.7.9`` minimum, ``1.8.x``
recommended. The default git version on CentOs 6.6 is ``1.7.1``.

As a workaround, you can use ``JGit`` a Java git implementation that is
bundles with ``Git Client`` a Jenkins plugin dependency for *Git
Plugin*.
