Git Shell Prompt
################

Do you have several branches and not sure which is you current branch?
Do you type ``git branch`` so many times just to keep track of your
working branch?

The solution to this is to have your terminal prompt display the current
branch. Windows *Git Bash* users have it why not us !Linux! users?!

Go to this `awesome GitHub project for *Git Aware
Prompt* <https://github.com/jimeh/git-aware-prompt#installation>`__ and
follow the installation instructions.

1. To use the new shell prompt find your bash initialization script
   ``~/.bash_profile`` or ``~/.bashrc`` or ``~/.profile``.

2. Check your ``PS1`` prompt variable

   .. code:: bash

       echo $PS1

3. Append the following line at the end of file.

   .. code:: bash

       export PS1="\[\e]0;\u@\h: \w\a\]${debian_chroot:+($debian_chroot)}\u@\h:\w \[$txtylw\]\$git_branch\[$txtred\]\$git_dirty\[$txtrst\]\$ "

4. To test the new prompt:

   .. code:: bash

       source ~/<bash init script name>

   Where is the name of the file you just edited.

If you find any problems you can comment the newly added line by putting
``#`` at the line start.

You can update the ``PS1`` value according your original ``PS1`` from
step **2**
