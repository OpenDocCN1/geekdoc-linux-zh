# TABLE 6.10
ACL Specifications

| TYPE | SYNTAX |
|---|---|
| User | `u[user]:[username]:mode` |
| Group | `g[group]:[groupname]:mode` |
| Other | `o[other]:mode` |
| ACL mask | `m[ask]:mode` |

Consider the following example in which user eric is given read and write access to a file called report:

```
```text
Athena:/home/testuser # ls -l report
-rw-rw---- 1 testuser users 0 2005-01-12 10:25 report
Athena:/home/testuser # setfacl -m u:eric:rw- report
Athena:/home/testuser # ls -l report
-rw-rw----+ 1 testuser users 0 2005-01-12 10:25 report
Athena:/home/testuser # getfacl report
# file: report
# owner: testuser
# group: users
user::rw-
user:eric:rw-
group::rw-
mask::rw-
other::r--
```
```

# TIP

In the ls output after the setfacl command, notice the + after the permission bits. This symbol indicates the file has extended attributes associated with it.

The getfacl command displays ACLs and other file information. The first three lines show the file’s name (report), the file’s owner (testuser), and the group owner (users). The line user::rw- and the lines group::rw- and other::r-- simply reflect the traditional file mode permission bits. The user:eric:rw- line is the new, named user ACL (where a specifically named user is given an ACL assignment). Assume that Eric is not a member of the group users. This named ACL has just granted Eric read and write access to the file. Without the use of ACLs, either Eric would just have read access (as a result of the world permission bits), or you would have to add him to the group users to grant him read/write access.