# 382

If he has been wasting space with noncompany work or materials, you might want to restrict him from saving anything to this directory:

```
nwbootspace -d /NetWare/bindy/cburns/volumes/users/hsimpson -b -1
```

A file system trustee on a NetWare bindery server is an object (usually a user object) that has been granted a set of access rights to a file or directory on a NetWare volume. As you view trustee assignments, remember that the effective rights a user has (that is, what the user can actually do with a file or directory) can be a combination of the trustee assignments that the user has to a file or directory, trustee assignments to parent directories, and group trustee assignments.

First, locate the bindery object that you want to be the trustee; for example, find the user you want to grant access to and then use the nwboots trust command to view an object’s rights to files and or directories on the server. You must include either the -o or -p option. If you use -o, nwboots trust displays the trustee rights the object has to any and all directories on the server specified in the bindery object path. If you use -p, you see all the objects that are trustees of the directory.

The rights for the user are displayed as a symbolic rights mask. Rights are enclosed inside square brackets, using standard NetWare rights syntax, containing zero or more of the following values:

+   - R Read from file.
+   - W Write to file.
+   - C Create directory or file.
+   - E Erase directory or file.
+   - M Modify directory or file.
+   - F File scan.
+   - A Access control.

If nwboots trust returns [RWF], the user has read, write, and file scan rights to that directory.

To show the rights for all directories that the bindery object hsimpson has on the authenticated server cburns, use the following:

```
nwboots trust -o /NetWare/bindy/cburns/objects/hsimpson
```

You can also show the rights of all bindery trustees for the directory or file SYS:/users/hsimpson on the server cburns:

```
nwboots trust -p /NetWare/bindy/cburns/volumes/SYS/users /hsimpson
```