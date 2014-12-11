AUFS Apply

Description
===========

This small script will apply an AUFS change layer to a directory.

It supports:

- whiteout to remove files (``.wh.FILENAME`` files)
- normal files are copied
- opaque dirs are removed (``.wh..wh..opq`` files)

It tries to make the minimum filesystem change and to be performant.

Main objectives where:

- have the less dependency possible (only need ``bash``, no need of ``aufs`` itself)
- touch the less files possible.
- be quick.

If you don't need those objective, a simple cp -a from a mounted aufs
would do the same.

Why
===

Aufs layers are a not so inefficient wait to store binary patches to big complex code
tree. Besides, on some VM, space is an issue, and you can't afford storing GIT history
for instance, nor you want to install ``git`` or ``rsync`` and their dependency.

VM file system is not always available from external host (think at
docker) with external tools.

Usage
=====

For instance, let's say you had mounted::

     mount -t aufs -o br=changes:root -o udba=none none mntpoint

Then you apply some changes::

     cd mntpoint
     # ... changes on filesystem ...
     cd ..

Then, for some reason, you want to remove the need of aufs, but want
to apply the changes stored in folder ``changes``. Then you can use
``aufs_apply``::

     aufs_apply root changes
     cd root
     # ... marvel as your changes where applied to your directory.

This doesn't go further than this.

Maturity
========

Just as been tested with a large GIT repository changes. That's all.

No Warranty of any sort. Use at your own risk.
