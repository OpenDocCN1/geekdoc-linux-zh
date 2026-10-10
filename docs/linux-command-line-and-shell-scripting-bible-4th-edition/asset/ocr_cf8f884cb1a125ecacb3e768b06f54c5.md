numerical user ID or group ID, or the names. Here’s an example:

```
$ setfacl -m g:sales:rw test
$ ls -1
total 0
-rw-rw----+ 1 rich rich 0 Apr 19 17:33 test
$
```

This example adds read and write permissions for the sales group to the test file. Notice that there’s no output from the setfacl command. When you list the file, only the standard owner, group, and other permissions are shown, but note that there’s a plus sign (+) added to the permissions list. This indicates that the file has additional ACLs applied to it. To view the additional ACLs, use the getfacl command again:

```
$ getfacl test
# file: test
# owner: rich
# group: rich
user::rw-
group::r--
group:sales:rw-
mask::rw-
other::---
$
```

The getfacl output now shows that there are permissions assigned to two groups. The default file group (rich) is assigned read permissions, but now the sales group has read and write permissions to the file. To remove the permissions, use the -x option:

```
$ setfacl -x g:sales test
$ getfacl test
# file: test
# owner: rich
# group: rich
user::rw-
group::r--
mask::r--
other::---

$
```

Linux also allows you to set a default ACL on a directory that is