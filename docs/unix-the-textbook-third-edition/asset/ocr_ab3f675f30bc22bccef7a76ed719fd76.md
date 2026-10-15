A nontrivial entry might look like the following example, where permissions are specifically granted to user mansoor:

```
0:user:mansoor:read_data/write_data:file_inherit:allow
```

# 23.9.3.1.2 ACL Entry Descriptions: Components of NFSv4 ACL Command Entry Descriptions

The following describes the syntactic components, both general and specific, of the setfacl command applied to files and directories. We also show the general form of the output from the getfacl command after the example is executed:

```
Command To Whom Permissions To What
Files setfacl -a 0 user:bob:rwx------:----:allow filename
  a   b c d e f      g   h   i
Directories setfacl -a 0 user:bob:r------:fd--:allow dirname
  a   b c d e f      g   h   i
```

+   key-
+   a-command
+   b-option
+   c-position option argument starting at 0, cannot be a number at the end!
+   d- ACL tag
+   e- ACL qualifier, in these cases user
+   f- 14 permissions, in short form, the hyphens(-) optional
+   g- 6 inheritance flags, for directories only, the hyphens(-) optional
+   h- ACL type, either allow or deny
+   i- command argument, a filename or directory name specification

Format of getfacl output for the preceding file’s command:

```
%getfacl filename
#file filename
#owner owner name
#group group name
position 0 user:bob:rwx------:-----:allow
filename
position1 owner@-----------------------------------------
position2 group@-----------------------------------------
position3 everyone@-------------------------------------
```

Use the following additional sample entry as a reference to the elements that comprise an ACL entry. These elements apply to both trivial and nontrivial ACLs.

```
user:mansoor:read_data/write_data:file_inherit:allow
```