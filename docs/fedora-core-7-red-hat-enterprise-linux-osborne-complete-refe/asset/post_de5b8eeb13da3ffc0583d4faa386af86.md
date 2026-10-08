
## groupadd and groupdel

With the **groupadd** command, you can create new groups. When you add a group to the system, the system places the group's name in the `/etc/group` file and gives it a group ID number. If shadow security is in place, changes are made to the `/etc/gshadow` file. The **groupadd** command only creates the group category. You need to add users to the group individually. In the following example, the **groupadd** command creates the `engines` group:

```bash
# groupadd engines
```

You can delete a group with the **groupdel** command. In the next example, the `engines` group is deleted:

```bash
# groupdel engines
```

## groupmod

You can change the name of a group or its ID using the **groupmod** command. Enter `groupmod -g` with the new ID number and the group name. To change the name of a group, you use the `-n` option. Enter `groupmod -n` with the new name of the group, followed by the current name. In the next example, the `engines` group has its name changed to `trains`:

```bash
# groupmod -n trains engines
```

## Controlling Access to Directories and Files: chmod

Each file and directory in Linux contains a set of permissions that determine who can access them and how. You set these permissions to limit access in one of three ways: You can restrict access to yourself alone, you can allow users in a pre-designated group to have access, or you can permit anyone on your system to have access. You can also control how a given file or directory is accessed.

> *NOTE* See Chapter 17 to learn how to use SELinux to set permissions on users and files.

### Permissions

A file or directory may have read, write, and execute permissions. When a file is created, it is automatically given read and write permissions for the owner, enabling you to display and modify the file. You may change these permissions to any combination you want. A file could also have read-only permission, preventing any modifications.

> *TIP* From GNOME you can change permissions easily by right-clicking and selecting Properties. On the Permissions panel you will see options for setting Owner, Group, and Other permissions. These correspond to the Owner, Group, and Other permissions described here (see Chapter 6).

### Permission Categories

Three different categories of users can have access to a file or directory: the owner, the group, and all others not belonging to that group. The owner is the user who created the file. Any file you create, you own. You can also permit a group to have access to a file. Often, users are collected into groups. For example, all the users for a given class or project could be formed into a group by the system administrator. A user can grant access to a file to the members of a designated group. Finally, you can also open up access to a file to all other users on the system. In this case, every user not part of the file's group could have access to that file. In this sense, every other user on the system makes up the *others* category. If you want to give the same access to all users on your system, you set the same permissions for both the group and the others. That way, you include both members of the group (group permission) and all those users who are not members (others permission).

### Read, Write, Execute Permissions

Each category has its own set of read, write, and execute permissions. The first set controls the user's own access to his or her files—the owner access. The second set controls the access of the group to a user's files. The third set controls the access of all other users to the user's files. The three sets of read, write, and execute permissions for the three categories—owner, group, and other—make a total of nine types of permissions.

The `ls` command with the `-l` option displays detailed information about the file, including the permissions. In the following example, the first set of characters on the left is a list of the permissions set for the `mydata` file:

```bash
$ ls -l mydata
-rw-r--r-- 1 chris weather 207 Feb 20 11:55 mydata
```

An empty permission is represented by a dash, -. The read permission is represented by **r**, write by **w**, and execute by **x**. Notice there are ten positions. The first character indicates the file type. In a general sense, a directory can be considered a type of file. If the first character is a dash, a file is being listed. If the first character is **d**, information about a directory is being displayed.

The next nine characters are arranged according to the different user categories. The first set of three characters is the owner's set of permissions for the file. The second set of three characters is the group's set of permissions for the file. The last set of three characters is the others' set of permissions for the file.

### Permissions on GNOME

On GNOME, you can set a directory or file permission using the Permissions panel in its Properties window (see Chapter 6). Right-click the file or directory entry in the file manager window and select Properties. Then select the Permissions panel. Here you will find Access pop-up menus for Owner, Group, and Other where you can set Read, Write, and Execute permissions. You can specify the group you want access provided to from the Group drop-down menu. This displays the groups a user belongs to. The root user can change the owner of the file, listing all possible users from the Owner pop-up menu. You can even change the SELinux security context for the file or directory.

### chmod

You use the `chmod` command to change different permission configurations. `chmod` takes two lists as its arguments: permission changes and filenames. You can specify the list of permissions in two different ways. One way uses permission symbols and is referred to as the symbolic method. The other uses what is known as a "binary mask" and is referred to as either the absolute or the relative method. Table 28-5 lists options for the **chmod** command.

> **NOTE** When a program is owned by the *root*, setting the user ID permission will give the user the ability to execute the program with root permissions. This can be a serious security risk for any program that could effect changes—such as *rm*, which removes files.

**TABLE 28-5** File and Directory Permission Operations

| Command or Option | Execution |
| :---------------- | :-------- |
| **chmod** | Changes the permission of a file or directory. |
| **+** | Adds a permission. |
| **-** | Removes a permission. |
| **=** | Assigns entire set of permissions. |
| **r** | Sets read permission for a file or directory. A file can be displayed or printed. A directory can have the list of its files displayed. |
| **w** | Sets write permission for a file or directory. A file can be edited or erased. A directory can be removed. |
| **x** | Sets execute permission for a file or directory. If the file is a shell script, it can be executed as a program. A directory can be changed to and entered. |
| **u** | Sets permissions for the user who created and owns the file or directory. |
| **g** | Sets permissions for group access to a file or directory. |
| **o** | Sets permissions for access to a file or directory by all other users on the system. |
| **a** | Sets permissions for access by the owner, group, and all other users. |
| **s** | Set User ID and Group ID permission; program owned by owner and group. |
| **t** | Set sticky bit permission; program remains in memory. |
| *chgrp groupname filenames* | Changes the group for a file or files. |
| *chown user-name filenames* | Changes the owner of a file or files. |
| *ls -l filename* | Lists a filename with its permissions displayed. |
| *ls -ld directory* | Lists a directory name with its permissions displayed. |
| *ls -l* | Lists all files in a directory with its permissions displayed. |

## **Ownership**

Files and directories belong to both an owner and a group. A group usually consists of a collection of users, all belonging to the same group. In the following example, the **mydata** file is owned by the user **robert** and belongs to the group **weather**:

```text
-rw-r--r-- 1 robert weather 207 Feb 20 11:55 mydata
```

A group can also consist of one user, however, normally the user who creates the file. Each user on the system, including the root user, is assigned their own group, of which they are the only member, ensuring access only by that user. In the next example, the report file is owned by the **robert** user and belongs to that user’s single user group, **robert**:

```text
-rw-r--r-- 1 robert robert 305 Mar 17 12:01 report
```

The root user, the system administrator, owns most of the system files that also belong to the root group, of which only the root user is a member. Most administration files, like configuration files in the */etc* directory, are owned by the root user and belong to the root group. Only the root user has permission to modify them, whereas normal users can read and, in the case of programs, also execute them. In the next example, the root user owns the *fstab* file in the */etc* directory, which also belongs to the root user group:

```text
-rw-r--r-- 1 root root 621 Apr 22 11:03 fstab
```

Certain directories and files located in the system directories are owned by a service, rather than the root user, because the services need to change those files directly. This is particularly true for services that interact with remote users, such as Internet servers. Most of these files are located in the */var* directory. Here you will find files and directories managed by services like the Squid proxy server and the Domain Name Server (named). In this example, the Squid proxy server directory is owned by the **squid** user and belongs to the **squid** group:

```text
drwxr-x--- 2 squid squid 4096 Jan 24 16:29 squid
```

## **Changing a File's Owner or Group: chown and chgrp**

Although other users may be able to access a file, only the owner can change its permissions. If, however, you want to give some other user control over one of your file's permissions, you can change the owner of the file from yourself to the other user. The **chown** command transfers control over a file to another user. This command takes as its first argument the name of the other user. Following the username, you list the files you are transferring. In the next example, the user gives control of the **mydata** file to user **robert**:

```text
$ chown robert mydata
$ ls -l mydata
-rw-r--r-- 1 robert weather 207 Feb 20 11:55 mydata
```

You can also, if you wish, change the group for a file, using the **chgrp** command. **chgrp** takes as its first argument the name of the new group for a file or files. Following the new group name, you list the files you want changed to that group. In the next example, the
