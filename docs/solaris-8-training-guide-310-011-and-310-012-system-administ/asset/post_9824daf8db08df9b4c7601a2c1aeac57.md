
## Sticky Bit

The sticky bit is a permission bit that protects the files within a directory. If the directory has the sticky bit set, a file can be deleted only by the owner of the file, the owner of the directory, or root. This prevents a user from deleting other users’ files from public directories. A t or T in the access permissions column of a file listing indicates that the sticky bit has been set:

```
drwxrwxrwt  2 uucp  uucp  512 Feb 12 07:32 \
/var/spool/uucppublic
```

Use the chmod command to set the sticky bit. The symbols for setting the sticky bit by using the chmod command in symbolic mode are listed in Table 8.9.

### TABLE 8.9
### STICKY BIT MODES

| Symbol | Description |
| --- | --- |
| t | Sticky bit is on; execution bit for others is on. |
| T | Sticky bit is on; execution bit for others is off. |

## Access Control Lists (ACLs)

ACLs (pronounced acls) can provide greater control over file permissions when the traditional UNIX file protection in the Solaris operating system is not enough. The traditional UNIX file protection provides read, write, and execute permissions for the three user classes: owner, group, and other. An ACL provides better file security by allowing you to define file permissions for the owner, owner’s group, others, specific users and groups, and default permissions for each of these categories.

For example, assume you have a file you want everyone in a group to be able to read. To give everyone access, you would give “group” read permissions on that file. Now, assume you want only one person in the group to be able to write to that file. Standard UNIX doesn’t let you set that up; however, you can set up an ACL to give only one person in the group write permissions on the file. Think of ACL entries as an extension to regular UNIX permissions.

ACL entries are the way to define an ACL on a file, and they are set through the ACL commands. ACL entries consist of the following fields, separated by colons:

```
entry_type:uid:gid:perms
```

ACL entries are defined in Table 8.10.

### TABLE 8.10
### ACL ENTRIES

| ACL Field | Description |
|---|---|
| entry_type | The type of ACL entry on which to set file permissions. For example, entry_type can be user (the owner of a file) or mask (the ACL mask). |
| uid | The username or identification number. |
| gid | The group name or identification number. |
| perms | The permissions set on entry_type. Permissions are indicated by the symbolic characters rwx or an octal number, as used with the chmod command. |

The ACL mask entry indicates the maximum permissions allowed for users, other than the owner, and for groups. The mask is a quick way to change permissions on all users and groups. For example, the mask:r-- mask entry indicates that users and groups cannot have more than read permissions, even though they might have write/execute permissions.

## Setting ACL Entries

Set ACL entries on a file by using the setfacl command:

```
$ setfacl -s \
user::perms,group::perms,other::perms,mask:perms, \
acl_entry_list filename ...
```

The -s option replaces the entire ACL with the new ACL entries, if an ACL already exists on the file.

The following example sets the user permissions to read/write, group permissions to read-only, and other permissions to none on the txt1.doc file. In addition, the user bill is given read/write permissions on the file, and the ACL mask permissions are set to read/write, which means that no user or group can have execute permissions.

```
$ setfacl -s user::rw-,group::r--,other:---,mask: \
 rw-,user:bill:rw- txt1.doc
```

In addition to the ACL entries for files, you can set default ACL entries on a directory that apply to files created within the directory. For example, I'll use the setfacl command to set execute privileges on the /home/bholzgen directory for user bcalinks. Execute privileges on a directory allow a user to change to that directory and do a long listing with the ls -l command on that directory. Before I set the ACL on this directory, let's look at the default permission that currently exists on that directory:

```
drwxr-xr-x  2 bholzgen  staff  512 Jul 30 12:41 \
 bholzgen
```

> NOTE
When you set default ACL entries for specific users and groups on a directory for the first time, you must also set default ACL entries for the file owner, file group, others, and ACL mask.

Now, issue the command to set the ACL privileges:

```
setfacl -s user::rwx,g::r--,o:---,m:rwx,user:bcalinks:rwx \
 /export/home/bholzgen
```

Use the getfacl command to display the ACL entry for the /export/home/bholzgen directory as follows:

```
getfacl /export/home/bholzgen
```

The system responds with the following:

```
# file: /export/home/bholzgen
# owner: bholzgen
# group: staff
user::rwx
user:bcalinks:rwx                #effective:rwx
group:r--                        #effective:r--
mask:rwx
other:---
```

Now, the only persons allowed to change into the /export/home/bholzgen directory are bholzgen and bcalinks. No other members, except root, will be able to access this directory—not even members of the same group.

## Checking the New File Permissions

Check the new file permissions with the ls -l command. The plus sign (+) to the right of the mode field indicates that the file has an ACL:

```
$ ls -l
 total 210
```

```
-rw-r-----+	1 mike sysadmin 32100 Sep 11 13:11 txt1.doc
-rw-r--r--	1 mike sysadmin 1410 Sep 11 13:11 txt2.doc
-rw-r--r--	1 mike sysadmin 1700 Sep 11 13:11 labnotes
```

## Verifying ACL Entries

To verify which ACL entries were set on the file, use the getfacl command:

```
$ getfacl txt1.doc
```

The system responds with this:

```
# file: txt1.doc
# owner: mike
# group: sysadmin
user::rw-
user:bill:rw-	#effective:rw-
group::r--	#effective:r--
mask:rw-
other:---
```

## Copying a File's ACL to Another File

Copy a file's ACL to another file by redirecting the getfacl output as follows:

```
getfacl <filename1> | setfacl -f - <filename2>
```

In the following example, I copy the ACL from file1 to file2:

```
getfacl file1 | setfacl -f - file2
```

Issuing the getfacl command, I can verify that the change has been made:

```
getfacl file*
```

```
# file: file1
# owner: root
# group: other
user::rw-
user:bcalkins:rw-	#effective:rw-
group::r--	#effective:r--
mask:rw-
other:---

# file: file2
# owner: root
# group: other
user::rw-
user:bcalkins:rw-	#effective:rw-
group::r--	#effective:r--
mask:rw-
other:---
```

## Modifying ACL Entries on a File

Modify ACL entries on a file by using the setfacl command:

```
setfacl -m <acl_entry_list> <filename1> [filename2 ...]
```

The arguments for the setfacl command are described in Table 8.11.

### TABLE 8.11
### setfacl ARGUMENTS

| Argument | Description |
|---|---|
| -m | Modifies the existing ACL entry. |
| <acl_entry_list> | Specifies the list of one or more ACL entries to modify on the file or directory. You can also modify default ACL entries on a directory. (See Table 8.12 for the list of ACL entries.) |
| <filename> | Specifies the file or directory. |

The ACL entries that can be specified with the setfacl command are described in Table 8.12.

### TABLE 8.12
### ACL ENTRIES FOR FILES

| ACL Entry | Description |
|---|---|
| u[ser]:: <perms> | File owner permissions. |
| g[roup]:: <perms> | File group permissions. |
| o[ther]:<perms> | Permissions for users other than the file owner or members of the file group. |
| m[ask]:<perms> | The ACL mask. The mask entry indicates the maximum permissions allowed for users (other than the owner) and for groups. The mask is a quick way to change permissions on all the users and groups. For example, the mask:r-- mask entry indicates that users and groups cannot have more than read permissions, even though they might have write/execute permissions. |
| u[ser]:uid:<perms> | Permissions for a specific user. For uid, you can specify either a username or a numeric UID. |
| g[roup]:gid:<perms> | Permissions for a specific group. For gid, you can specify either a group name or a numeric GID. |
