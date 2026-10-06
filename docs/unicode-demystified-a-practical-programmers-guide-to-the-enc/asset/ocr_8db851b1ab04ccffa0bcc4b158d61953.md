# Options

--changes -c For each file whose mode is changed, displays a message saying that its mode was changed and giving the value of the mode absolutely and symbolically.

--quiet or -f Prevents chmod from displaying error messages when it is unable to change the permissions of a file.

--recursive -R When you include a directory in file-list, descends the directory hierarchy, setting the specified modes on all the files it encounters.

--verbose -v Displays for each file message saying that its mode was changed—even if it was not changed—and giving the value of the mode absolutely and symbolically.

--reference=rfile Changes the access mode of the files in file-list to that of rfile.

# Notes

When you use symbolic arguments, you can omit the permission from the command line only when the operation is=. This omission takes away all permissions.

# Examples

The following examples show how to use the chmod utility to change permissions on a file named temp. The initial access mode of temp is shown by is:

```
$ ls -l temp
-rw-rw-rw- 1 alex pubs 57 Jul 12 16:47 temp

```

The following command line removes all permissions for the group and all other users so that only the owner has access to the file:

```
$ chmod go= temp
$ ls -l temp
-rw-rw-rw- 1 alex pubs 57 Jul 12 16:47 temp

```

When you do not follow an equal sign with permission, chmod removes all permissions for the specified user class. The ls utility verifies the change.

The next command changes the access mode for all users (owner, group, and all others) to read and write. Now anyone can read from or write to the file.

```
$ chmod a=rw temp
$ ls -l temp
-rw-rw-rw- 1 alex pubs 57 Jul 12 16:47 temp

```

Using an absolute argument, the a=rw becomes 666. The next command performs the same function as the previous chmod command:

```
$ chmod 666 temp

```