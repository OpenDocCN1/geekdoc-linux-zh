
Linux does not tell you which group you're in. Usually the only way to find out which group is active is to save a file and then look at the permissions. If you try to change to another group that you don't belong to with `newgrp`, Linux will give you a friendly warning like this one:

```
newgrp programmers
newgrp: Sorry
```

## Changing Group Ownership

You've already seen how to change the ownership of a file. You might also want to change the group owner. To change the ownership of a group, you don't have to belong to the group, but you must own the file. Before you can begin, Linux first checks that the group exists.

The `chgrp` command is used to change the group the file belongs to. It works just like `chown`:

```
chgrp <group> <filename>
```

For example, to change the ownership of the file `book` to a group called `editors`. issue this command:

```
$ ls book*
-rwxr-xr-x   2 tparker  group    4512 May  9 09:20 book
$ chgrp editors book
$ ls book*
-rwxr-xr-x   2 tparker  editors  4512 May  9 09:20 book
```

You can use wildcards with both `chown` and `chgrp`, as the following example shows:

```
$ ls book*
-rwxr-xr-x   2 tparker  group    4512 May  9 09:20 book1
-rwxr-xr-x   2 tparker  group    4625 May  9 09:21 book2
-rwxr-xr-x   2 tparker  group    7834 May  9 09:22 book3
$ chown bills book*
$ ls book*
-rwxr-xr-x   2 bills  group     4512 May  9 09:20 book1
-rwxr-xr-x   2 bills  group     4625 May  9 09:21 book2
-rwxr-xr-x   2 bills  group     7834 May  9 09:22 book3
$ chgrp editors book*
$ ls book*
-rwxr-xr-x   2 bills  editors   4512 May  9 09:20 book1
-rwxr-xr-x   2 bills  editors   4625 May  9 09:21 book2
-rwxr-xr-x   2 bills  editors   7834 May  9 09:22 book3
```

Notice that the `chgrp` and `chown` commands don't affect anything else about the file, such as the date and time it was created or the permissions in the first field.

## File Permissions

Since the early days, UNIX has tried to set up a flexible, powerful, yet simple set of file access permissions that balances security with convenience. The approach UNIX (and hence Linux) takes is simple. It sets only three different types of access (called permissions) that you may have on a file or directory. These are read, write, and execute permissions.

Having read permission to a file enables you to look at the file's contents. In the case of a directory, read permission lets you list the directory's contents using `ls`.

Write permission enables you to modify (or delete) the file, even if you are not the owner. In the case of a directory, you must have write permission in order to create, move, or delete files in that directory.

Execute permission enables you to execute the file by typing its name. This has no effect if the contents of the file can't be understood by an application. For example, having execute permission on a file that has statistical data in it won't allow you to run it. On the other hand, if the file is a statistical analysis program, it needs execute permission for it to run. With directories, execute permission enables you to `cd` into them.

So, we have three types of permissions: read, write, and execute. UNIX separates all users on the system into three categories based on the ownership of the file or directory. There is one set of permissions (read, write, and execute) for the owner, another set (read, write, and execute) for anyone in the group that owns the file, and a third set (read, write, and execute) for everyone else on the system (called other or world). The three sets of permissions are written one after another in a consistent format. The permissions are always in order of read, write, and execute; first for owner, then for group, then for other.

That's nine bits of information to indicate the permissions of the file or directory. These bits always appear in a block of ten and are the first thing you see in a long directory listing. The first character is special and indicates whether the entry is a file or directory (there are a few other valid values, but we won't bother with them now). For a concrete example, let's look at the long directory listing for `myfile` again:

```
-rw-r--r--  1 fidio  users    163 Dec  7 14:31 myfile
```

The first character of the permissions is `-`, which indicates that it's an ordinary file. If this were a directory, the first character would be `d`. The next nine characters are broken into three groups of three, giving permissions for owner, group, and other. Each triplet gives read, write, and execute permissions, always in that order. Permission to read is signified by an `r` in the first position, permission to write is shown by a `w` in the second position, and permission to execute is shown by an `x` in the third position. If a particular permission is absent, its space is filled by `-`.

In the case of `myfile`, the owner has `rw-`, which means read and write permissions. This file cannot be executed by typing `myfile` at the Linux prompt since there is no execute permission. The group permissions are `r--`, which means that members of the group `users` can read the file but cannot change it or execute it. Likewise, the permissions for all others are `r--`, or read-only.

## UMASK Settings

When you create a file (such as with redirection), how does Linux know which file permissions to assign? The answer is that a variable called the UMASK (user file creation mask) contains the instructions for every file you create. The system administrator can set the UMASK setting for any user or for the entire set of users on the whole system. You can change your own UMASK setting, but not that of others (unless you are logged in as root).

The value of UMASK can be shown at any time by typing the command `umask` (lower-case to distinguish it from the environment variable UMASK) at the shell prompt:

```
$ umask
022
```

You may have four numbers instead of three, but the first one doesn't mean anything so simply ignore it. What do the numbers mean? They are a set of octal numbers which indicate the user, group, and other permissions. The valid set of numbers in the `umask` command are shown in Table 9.1.

**TABLE 9.1. OCTAL VALUES USED BY UMASK AND THEIR MEANINGS.**

| Octal number | Permissions granted |
| :--- | :--- |
| 0 | Read and write (and execute for directories) |
| 1 | Read and write |
| 2 | Read (and execute for directories) |
| 3 | Read |
| 4 | Write (and execute for directories) |
| 5 | Write |
| 6 | Execute for directories only |
| 7 | No permissions |

In the UMASK setting of 022 shown earlier, the simple translation, according to this table, is that the user has read and write permissions (and execute for directories), while group and other have read-only (and execute for directories). This corresponds to the following directory block:

```
rw-r--r--
```

The column regarding execute for directories shows that if you were to create a directory with this UMASK setting, the permissions would include execute (which allows `cd` to be used to change that directory). The permission block for a directory created with this set of umask values would be as follows:

```
rwxr-xr-x
```

Note that there is no way to automatically assign execute permission to a file using the file creation mask. This was done intentionally so that you, the system administrator, have to manually set the execute permission on a file.

To change your UMASK setting, specify the three new values you want to use. For example, the setting 077 removes all permissions for group and other:

```
$ umask
0022
$ who > file1
$ ls -1
total 2
-rw-r--r--   1 tparker group    37 May  9 11:18 file1
$ umask 077
$ who > file2
$ ls -1
total 4
-rw-r--r--   1 tparker group    37 May  9 11:18 file1
-rw-------   1 tparker group    37 May  9 11:18 file2
```

Notice that the permissions of `file2` have set no access for members of the group or for the other users on the system. Only the owner has access to this file. Your UMASK setting is in effect until you log out.

## Changing File Permissions

You will probably be happy with the default permissions on your files for a while. Eventually, though, you will want to change them, either to add execute permission to a program that you own (so you can run it) or to let others have better or more restrictive access. To change file permissions, UNIX uses the `chmod` (change mode of a file) command.
