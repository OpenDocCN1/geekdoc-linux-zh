
```text
# ls -l
-rwxrw-r--  1 dla      other       636 Jan 24 12:42 file1
# chmod g+s file1
# ls -l
-rwxrwsr--  1 dla      other       636 Jan 24 12:42 file1
#
```

Another special file permission is the sticky bit. Originally, it was used to indicate programs that should be left in memory after execution. When set for frequently used programs, the sticky bit saved time and CPU cycles by using the image left in memory instead of loading it from disk again.

When the sticky bit is set on a directory that allows write permission for everyone, only the user account that created files and subdirectories under the directory can remove those files and subdirectories. This restriction is especially useful for the /tmp directory, which is available from any user account.

The sticky bit permission has an absolute mode of 1000 and a symbolic mode of t when used with the chmod command. This permission is shown as t in the other account execution permission field in the output of an ls command, but it is considered a user account (owner) permission. The following example shows using the chmod command to remove the sticky bit permission and then add it to a directory:

```text
# ls -ld /tmp
drwxrwxrwt  7 sys      sys         410 Jan 28 03:30 /tmp
# chmod u-t /tmp
# ls -ld /tmp
drwxrwxrwx  7 sys      sys         410 Jan 28 03:30 /tmp
# chmod 1777 /tmp
# ls -ld /tmp
drwxrwxrwt  7 sys      sys         410 Jan 28 03:30 /tmp
#
```

## Extended File Permissions: Access Control Lists

Solaris 8 extends the standard Unix file permissions by adding an Access Control List (ACL) capability. ACLs enable you to add permissions for specific users and groups along with a default permission (mask).

In addition to supporting the standard read/write/execute permissions for the standard file user account (owner), ACLs can be used to set read/write/execute permissions for additional user accounts. Likewise, ACLs support read/write/execute permissions for the standard file group account and allow read/write/execute permissions for additional group accounts. In addition, ACLs support read/write/execute permissions for the standard others (everyone else).

ACLs also include a mask capability that controls the maximum allowed permissions given to user and group accounts other than the standard file user account and the standard file group account.

For example, suppose root owns a file and sets its ACL mask to read/execute. Later, root adds read/write/execute permission to the file ACL for the guest user account. Because of the mask, the write permission is overridden, and the effective permissions for the guest account are read/execute.

The ACL for a directory includes default entries that determine the permissions assigned to files and subdirectories created under the directory. Default permissions can be defined for the standard Unix user, group, and other along with a default mask and default permissions for specific users or groups.

Two commands are used to manage ACLs: The **setfacl** command sets ACLs, and the **getfacl** command displays ACLs.

![](img/b957f979417d9f16274c2eb52c8f2c9f_135_0.png)

> Using the **setfacl** command to add, modify, and delete ACLs on files and directories is a stated test objective.

### Setting ACLs by Using setfacl

You use the setfacl(1) command to set and modify ACLs. It supports three command-line arguments:

- **-d**—Deletes the specified ACL entries
- **-m**—Adds/changes the specified ACL entries
- **-s**—Replaces the whole ACL with the specified entries

ACL entries for the standard user and group permissions are specified by using the format **entry::permissions** (note the two colons); **entry** is the keyword **user** or **group** (or the single-letter abbreviation **u** or **g**), and **permissions** is the appropriate combination of **r**, **w**, **x**, and **-** needed to define the permission.

ACL entries for the standard other permission and the mask used for maximum permissions use a slightly different syntax. The format is **entry:permissions** (note the single colon); **entry** is the keyword **other** or **mask** (or the single-letter abbreviation **o** or **m**), and **permissions** is the appropriate combination of **r**, **w**, **x**, and **-** needed to define the permission.

The following line shows the **setfacl** command for setting the user permission to read/write and setting the group and other permissions to read-only:

```text
# setfacl -s u::rw-,g::r--,o::r-- file1
```

ACL entries for other users and groups are specified by using the format **entry:id:permissions**. *entry* is the keyword **user** or **group** (or the single-letter abbreviation **u** or **g**); *id* is a user name, UID, group name, or GID; and *permissions* is the appropriate combination of **r**, **w**, **x**, and **-** needed to define the permission.

The following line shows the **setfacl** command for adding read/write permission for the user account guest and read-only permission for the group account staff:

```text
# setfacl -m u:guest:rw-,g:staff:r-- file1
```

In addition to the previously described ACL entries, you can define additional entries for directories. These entries specify the default ACL entries for files and subdirectories created under the directory. To establish defaults, use the previously described formats and add **d:** at the beginning of the *entry* field. All the standard user, group, and other defaults, along with the default mask, must be defined initially at the same time.

For example, to define the default ACL entries for the directory shlog, you can use the following **setfacl** command:

```text
# setfacl -m d:u::rw-,d:g::r--,d:o::r--,d:m::r-- shlog
```

The **-d** command-line argument is used to delete ACL entries. The remainder of the mask and file command-line arguments are identical to those used with the **-s** and **-m** command-line arguments.

### Displaying ACLs by Using getfacl

To display the ACLs for a file or directory, use the **getfacl** command. The following example displays the ACLs for the shlog directory using the **getfacl** command:

```text
# getfacl shlog
# file: shlog
# owner: shlog
# group: staff
user::rwx
group::r-x              #effective:r-x
mask::r-x
other::r-x
default:user::rw-
default:group::rw-
default:mask:r--
default:other:r--
#
```

When you use the **ls** command, files that have ACLs are shown with a **+** in front of the file entry.

## Changing File Ownership

Two commands are used to control file ownership:

- **chown(1M)**—Changes file user account ownership
- **chgrp(1M)**—Changes file group account ownership

### Changing the File User Account

The **chown** command is used to change the file user account that is the owner of a file or directory. You specify the user account name or associated UID along with the name of one or more files that should be owned by the specified user account. The following example uses the **chown** command to change the ownership of several files to the guest user account, which has a UID of 1001. Each **chown** command is preceded and followed by the **ls** command, which lists the file ownership and permissions:

```text
# ls -l
total 18
-rw-rw-rw-  1 root   other       120 Feb 28 07:38 data
-rw-rw-rw-  1 root   other      6528 Feb 28 07:38 junk
-rw-r--r--  1 root   other       636 Feb 28 07:39 list
# chown guest junk
# ls -l
total 18
-rw-rw-rw-  1 root   other       120 Feb 28 07:38 data
-rw-rw-rw-  1 guest  other      6528 Feb 28 07:38 junk
-rw-r--r--  1 root   other       636 Feb 28 07:39 list
# chown 1001 data
# ls -l
total 18
-rw-rw-rw-  1 guest  other       120 Feb 28 07:38 data
-rw-rw-rw-  1 guest  other      6528 Feb 28 07:38 junk
-rw-r--r--  1 guest  other       636 Feb 28 07:39 list
#
```

The **chown** command supports a recursive command-line argument, **-R**. When you use it to change a directory’s owner, the ownership of any files or subdirectories under the directory also changes.

Even though a separate command exists to change file group account ownership, you can use the **chown** command to change group ownership at the
