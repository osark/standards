Git Workflow
#############

Overview
--------

| Workflow is a consistent standard ways of how we use any project git
repository and branches.
| This workflow is a simplified version of the first `Git branching
model <http://nvie.com/posts/a-successful-git-branching-model/>`__.

*How it works?* Every project have two different types of branches: \*
Infinite Lifetime Branches \* Supporting Branches

| *Infinite Lifetime Branches* are special branches that should always
exists in any project repository at any given time. Most of the time
they reflects actual deployed instances of the project on live sever.
| The two main branches are: \* master \* develop

| On ``origin/master`` with source code on ``HEAD`` always reflects
*production ready* state. You can always checkout the ``origin/master``
branch and deploy the code to the production with no fear of breaking
live site.
| This means that if any file was changed or deleted from production
site by accident, you can always revert it back by checking it out of
``origin/master/HEAD``.

| On ``origin/develop`` with source code on ``HEAD`` always reflects
*next release ready* state. All features that are ready for client
review and will be deployed on the next release exists on
``origin/develop/HEAD``.
| If the client wants to test and integration of all requested features
ready for the next production deployment, you can checkout
``origin/develop`` branch and deploy it on stage site (e.g.,
stage.example.com).

*Supporting Branches* have short lifetime and most of the time they are
created for certain purpose and can be safely deleted after merging into
other branches or discarded completely. There are three different types
of branches: \* Feature Branches \* Hotfix Branches \* Release Branches

| *Feature Branches* usually have a name in the format ``feature/...``,
they represent a distinctive feature request or client change request,
that is modular enough to safely revert it if requested.
| There can be any number of feature branches in the project repository
at any point of time.

*Hotfix Branches* usually have a name in the format ``hotfix/...``, they
represent bugs and issues found by client in the production site. Issues
found in development instance by team members including internal testing
team should be solved in their own *Feature Branches*.

*Release Branches* are very special type of branches that are needed in
only large projects, where there are many activities needed before
deploying any major release, like generating the documentation and
release preparation.
