1156

read

# Files

```
~/.hosts      User's trusted hosts and users.
/etc/host.equiv  System trusted hosts and users.
/tmp/rdist*       Temporary file for update lists.
```

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWrcmdc |

# See Also

csh(1), ed(1), sh(1), make(1S), stat(2), hosts.equiv(4), attributes(5),
ip6 (7P)

# Diagnostics

A complaint about mismatch of rdist version numbers can really stem from some problem with starting your shell, for example, you are in too many groups.

# Warnings

The superuser does not have the accustomed access privileges on NFS-mounted file systems. Using rdist to copy such a file system may fail or the copies may be owned by user nobody.

# Bugs

Source files must reside on or be mounted on the local host.
There is no easy way to have a special command executed once after all files in a directory have been updated.
Variable expansion works only for name lists; there should be a general macro facility.dist aborts on files that have a negative modification time (before Jan. 1, 1970).
There should be a "force" option to enable replacement of nonempty directories by regular files or symbolic links. A means of updating file modes and owners of otherwise identical files is also needed.

# read — Read a Line from Standard Input

# Synopsis

```
/usr/bin/read [-r] var...
sh
read name...
```