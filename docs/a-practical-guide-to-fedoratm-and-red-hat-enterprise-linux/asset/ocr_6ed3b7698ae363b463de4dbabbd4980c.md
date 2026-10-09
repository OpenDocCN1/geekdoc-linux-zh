always sets the effective rights mask to the least restrictive ACL permissions for the file, the mask has no effect unless you set it explicitly after you set up an ACL for the file. You can set the mask by specifying **mask** in place of *ugo* and by not specifying a *name* in a **setfacl** command.

The following example sets the effective rights mask to *read* for the report file:

```
```bash
$ setfacl -m mask::r-- report
```
```

The **mask** line in the following **getfacl** output shows the effective rights mask set to read (r—). The line that displays Sam’s file access permissions shows them still set to read and write. However, the comment at the right end of the line shows that his effective permission is read.

```
```bash
$ getfacl report
# file: report
# owner: max
# group: pubs
user::rw-
user:sam:rw-                        #effective:r--
group::r--
mask::r--
other::r--
```
```

As the next example shows, **setfacl** can modify ACL rules and can set more than one ACL rule at a time:

```
```bash
$ setfacl -m u:sam:r--,u:zach:rw- report
```
```

```
```bash
$ getfacl --omit-header report
user::rw-
user:sam:r--
user:zach:rw-
group::r--
mask::rw-
other::r--
```
```

The −x option removes ACL rules for a user or a group. It has no effect on permissions for the owner of the file or the group that the file is associated with. The next example shows **setfacl** removing the rule that gives Sam permission to access the file:

```
```bash
$ setfacl -x u:sam report
```
```

```
```bash
$ getfacl --omit-header report
user::rw-
user:zach:rw-
group::r--
mask::rw-
other::r--
```
```

You must not specify *permissions* when you use the −x option. Instead, specify only the *ugo* and *name*. The −b option, followed by a filename only, removes all ACL rules and the ACL itself from the file or directory you specify.

Both **setfacl** and **getfacl** have many options. Use the **−−help** option to display brief lists of options or refer to the *man* pages for details.