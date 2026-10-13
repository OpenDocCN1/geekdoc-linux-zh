
## chmod

You use the `chmod` command to change different permission configurations. `chmod` takes two lists as its arguments: permission changes and filenames. You can specify the list of permissions in two different ways. One way uses permission symbols and is referred to as the symbolic method. The other uses what is known as a "binary mask" and is referred to as either the absolute or the relative method. Table 28-4 lists options for the `chmod` command.

> **Note** When a program is owned by the root, setting the user ID permission will give the user the ability to execute the program with root permissions. This can be a serious security risk for any program that could effect changes—such as `rm`, which removes files.

## Ownership

Files and directories belong to both an owner and a group. A group usually consists of a collection of users, all belonging to the same group. In the following example, the `mydata` file is owned by the user `robert` and belongs to the group `weather`.

```bash
-rw-r--r-- 1 robert weather 207 Feb 20 11:55 mydata
```

**Table 28-4: File and Directory Permission Operations**

| Command or Option | Execution |
| :--- | :--- |
| `chmod` | Changes the permission of a file or directory. |
| **Options** | |
| `+` | Adds a permission. |
| `-` | Removes a permission. |
| `=` | Assigns entire set of permissions. |
| `r` | Sets read permission for a file or directory. A file can be displayed or printed. A directory can have the list of its files displayed. |
| `w` | Sets write permission for a file or directory. A file can be edited or erased. A directory can be removed. |
| `x` | Sets execute permission for a file or directory. If the file is a shell script, it can be executed as a program. A directory can be changed to and entered. |
| `u` | Sets permissions for the user who created and owns the file or directory. |
| `g` | Sets permissions for group access to a file or directory. |
| `o` | Sets permissions for access to a file or directory by all other users on the system. |
| `a` | Sets permissions for access by the owner, group, and all other users. |
| `s` | Sets User ID and Group ID permission; program owned by owner and group. |
| `t` | Sets sticky bit permission; program remains in memory. |
| `chgrp groupname filenames` | Changes the group for a file or files. |
| `chown user-name filenames` | Changes the owner of a file or files. |
| `ls -l filename` | Lists a filename with its permissions displayed. |
| `ls -ld directory` | Lists a directory name with its permissions displayed. |
| `ls -l` | Lists all files in a directory with its permissions displayed. |

A group can also consist of one user, however, normally the user who creates the file. Each user on the system, including the root user, is assigned their own group, of which they are the only member, ensuring access only by that user. In the next example, the `report` file is owned by the `robert` user and belongs to that user's single user group, `robert`.

```bash
-rw-r--r-- 1 robert robert 305 Mar 17 12:01 report
```

The root user, the system administrator, owns most of the system files that also belong to the root group, of which only the root user is a member. Most administration files, like configuration files in the `/etc` directory, are owned by the root user and belong to the root group. Only the root user has permission to modify them, whereas normal users can read and, in the case of programs, also execute them. In the next example, root user owns the `fstab` file in `/etc` directory, which also belongs to the root user group.

```bash
-rw-r--r-- 1 root root 621 Apr 22 11:03 fstab
```

Certain directories and files located in the system directories are owned by a service, rather than the root user, because the services need to change those files directly. This is particularly true for services that interact with remote users, such as Internet servers. Most of these files are located in the `/var` directory. Here you will find files and directories managed by services like the Squid proxy server and the Domain Name Server (`named`). In this example, the Squid proxy server directory is owned by the `squid` user and belongs to the `squid` group.

```bash
drwxr-x--- 2 squid squid 4096 Jan 24 16:29 squid
```

## Changing a File's Owner or Group: chown and chgrp

Although other users may be able to access a file, only the owner can change its permissions. If, however, you want to give some other user control over one of your file's permissions, you can change the owner of the file from yourself to the other user. The `chown` command transfers control over a file to another user. This command takes as its first argument the name of the other user. Following the username, you list the files you are transferring. In the next example, the user gives control of the `mydata` file to user `robert`:

```bash
$ chown robert mydata
$ ls -l mydata
-rw-r--r-- 1 robert weather 207 Feb 20 11:55 mydata
```

You can also, if you wish, change the group for a file, using the `chgrp` command. `chgrp` takes as its first argument the name of the new group for a file or files. Following the new group name, you list the files you want changed to that group. In the next example, the user changes the group name for `today` and `weekend` to the `forecast` group. The `ls -l` command then reflects the group change.

```bash
$ chgrp forecast today weekend
$ ls -l
-rw-rw-r-- 1 chris forecast 568 Feb 14 10:30 today
-rw-rw-r-- 1 chris forecast 308 Feb 17 12:40 weekend
```

You can combine the `chgrp` operation in the `chown` command by attaching a group to the new owner with a colon.

```bash
$ chown george:forecast tomorrow
-rw-rw-r-- 1 george forecast 568 Feb 14 10:30 tomorrow
```

## Setting Permissions: Permission Symbols

The symbolic method of setting permissions uses the characters `r`, `w`, and `x` for read, write, and execute, respectively. Any of these permissions can be added or removed. The symbol to add a permission is the plus sign, `+`. The symbol to remove a permission is the minus sign, `-`. In the next example, the `chmod` command adds the execute permission and removes the write permission for the `mydata` file for all categories. The read permission is not changed.

```bash
$ chmod +x-w mydata
```

Permission symbols also specify each user category. The owner, group, and others categories are represented by the `u`, `g`, and `o` characters, respectively. Notice the owner category is represented by a `u`, and can be thought of as the user. The symbol for a category is placed before the plus and minus signs preceding the read, write, and execute permissions. If no category symbol is used, all categories are assumed, and the permissions specified are set for the user, group, and others. In the next example, the first `chmod` command sets the permissions for the group to read and write. The second `chmod` command sets permissions for other users to read. Notice no spaces are between the permission specifications and the category. The permissions list is simply one long phrase, with no spaces.

```bash
$ chmod g+rw mydata
$ chmod o+r mydata
```

A user may remove permissions as well as add them. In the next example, the read permission is set for other users, but the write and execute permissions are removed:

```bash
$ chmod o+r-wx mydata
```

Another permission character exists, `a`, which represents all the categories. The `a` character is the default. In the next example, the two commands are equivalent. The read permission is explicitly set with the `a` character denoting all types of users: other, group, and user.

```bash
$ chmod a+r mydata
$ chmod +r mydata
```

One of the most common permission operations is setting a file's executable permission. This is often done in the case of shell program files. The executable permission indicates a file contains executable instructions and can be directly run by the system. In the next example, the file `lsc` has its executable permission set and then executed:

```bash
$ chmod u+x lsc
$ lsc
main.c lib.c
$
```

## Absolute Permissions: Binary Masks

Instead of the permission symbols in Table 28-4, many users find it more convenient to use the absolute method. The absolute method changes all the permissions at once, instead of specifying one or the other. It uses a binary mask that references all the permissions in each category. The three categories, each with three permissions, conform to an octal binary format. Octal numbers have a base 8 structure. When translated into a binary number, each octal digit becomes three binary digits. A binary number is a set of 1 and 0 digits. Three octal digits in a number translate into three sets of three binary digits, which is nine altogether—and the exact number of permissions for a file.
