# Access determination

When the ACL shown in the previous example is expanded to include entries for a specific user and group, setfacl automatically supplies an appropriate mask:

```
```text
$ ls -l /tmp/example
-rw-rw----+ 1 garth garth    0 Jun 14 15:57 /tmp/example
$ setfacl -m user::r,user:trent:rw,group::r,group:admin:rw /tmp/example
$ ls -l /tmp/example
-r--rw----+ 1 garth garth    0 Jun 14 15:57 /tmp/example
$ getfacl --omit-header /tmp/example
user::r--
user:trent:rw-
group::r--
group:admin:rw-
mask::rw-
other::---
```
```

As seen here, the Linux version of **setfacl** generates a mask that allows all the permissions granted in the ACL to take effect. If you want to set the mask by hand, include it in the ACL entry list given to **setfacl** or use the **-n** option to prevent **setfacl** from regenerating it. (The Solaris setfacl defaults to not recalculating the mask entry; use the **-r** flag to regenerate it.)

Note that after the **setfacl** command, **ls -l** shows a + sign at the end of the files mode to indicate that it now has a real ACL associated with it. The first **ls -l** shows no + because at that point the ACL is “minimal.” That is, it is entirely described by the 9-bit mode and so does not need to be stored separately.

If you use the traditional **chmod** command to manipulate the group permissions on an ACL-bearing file, be aware that your changes affect only the mask. To continue the previous example:

```
```text
$ chmod 770 /tmp/example
$ ls -l /tmp/example
-rwxrwx---+ 1 garth staff    0 Jun 14 15:57 /tmp/example
$ getfacl --omit-header /tmp/example
user::rwx
user:trent:rw-
group::r--
group:admin:rw-
mask::rwx
other::---
```
```

The **ls** output in this case is misleading. Despite the apparently generous group permissions, no one actually has permission to execute the file by reason of group membership. To grant such permission, you must edit the ACL itself.

# Access determination

When a process attempts to access a file, its effective UID is compared to the UID that owns the file. If they are the same, access is determined by the ACL’s user::