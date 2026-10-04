The ACL mask entry indicates the maximum permissions allowed for users, other than the owner, and for groups. The mask is a quick way to change permissions on all users and groups. For example, the mask:r-- mask entry indicates users and groups cannot have more than read permissions, even though they might have write/execute permissions.

Set ACL entries on a file by using the setfacl command.

```
$ setfacl -s user::perms,group::perms,other:perms,mask:perms,acl_entry_list
filename ...
```

The -s option replaces the entire ACL with the new ACL entries, if an ACL already exists on the file.

The following example sets the user permissions to read/write, group permissions to read only, and other permissions to none on the txt1.doc file. In addition, the user Bill is given read/write permissions on the file, and the ACL mask permissions are set to read/write, which means no user or group can have execute permissions.

```
$ setfacl -s user::rw,group:r--,other:---,mask:rw, user:bill:rw- txt1.doc
```

Check the new file permissions with the ls -l command. The plus sign (+) to the right of the mode field indicates the file has an ACL:

```
$ ls -l
total 210
-rw-r--...+ 1 mike sysadmin 32100 Sep 11 13:11 txt1.doc
-rw-r--r-- 1 mike sysadmin 1410 Sep 11 13:11 txt2.doc
-rw-r--r-- 1 mike sysadmin 1700 Sep 11 13:11 labnotes
```

To verify which ACL entries were set on the file, use the getfacl command:

```
$ getfacl txt1.doc
```

The system responds with

```
# file: txt1.doc
# owner: mike
# group: sysadmin
user::rw-
user:bill:rw-      #effective:rw-
group::r--        #effective:r--
mask:rw-
other:---
```

In addition to the ACL entries for files, you can set default ACL entries on a directory that apply to files created within the directory.