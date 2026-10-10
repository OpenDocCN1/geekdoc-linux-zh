
## zcat

**Purpose:** Read the contents of a compressed file.

**Usage syntax:** `zcat [OPTIONS] [FILE]`

```bash
$ file ShoppingList.txt.gz
ShoppingList.txt.gz: gzip compressed data, was "ShoppingList.txt", from Unix, last modified: Mon Apr 12 19:33:38 2010
$ zcat ShoppingList.txt.gz
Milk
Eggs
Cheese
Tacos
```

Viewing the contents of a compressed text file with the zcat command

The `zcat` command allows you to read the contents of a compressed text file without having to manually uncompress it first. In the above example the `ShoppingList.txt.gz` file is a compressed `gzip` archive. Using the traditional `cat` command would produce unreadable output in this scenario. The `zcat` command, however, allows you to view the contents of the file without having to first uncompress it.

**Common usage examples:**

- `zcat [FILE]`: Read the contents of a compressed file

## diff

**Purpose:** Compare files.

**Usage syntax:** `diff [OPTIONS] [FILE]`

```bash
$ diff ShoppingList.txt ShoppingList.old
4c4
< Tacos
---
> Nachos
```

Default output of the diff command

The **diff** command allows you to compare two text files line by line and display the differences between them. The **diff** command provides two types of output:

1. Single column (default)
2. Two column side-by-side comparison (activated with the **-y** option)

In the above example the **diff** command displays the default single column output which only shows the differences between the two files. Indicators are used to mark the differing lines:

- `<`: Indicates the text in the first file
- `>`: Indicates the text in the second file

The **-y** option can be used to display two column side-by-side output. The next example demonstrates the output generated with this option.

```bash
$ diff -y ShoppingList.txt ShoppingList.old
Milk                          | Milk
Eggs                          | Eggs
Cheese                        | Cheese
Tacos                         | Nachos
```

Comparing two files with the diff command

**Common usage examples:**

| Command | Description |
| :--- | :--- |
| `diff [FILE1] [FILE2]` | Compare files and display differences |
| `diff -y [FILE1] [FILE2]` | Compare files side by side |
| `diff -i [FILE1] [FILE2]` | Ignore case when comparing files |

## dos2unix / unix2dos

**Purpose:** Convert file formats between Windows/MS-DOS and Unix/Linux systems.

**Usage syntax:** `dos2unix / unix2dos [OPTIONS] [FILE]`

```bash
$ cat ShoppingList.txt
Milk^M
Eggs^M
Cheese^M
Tacos

$ dos2unix ShoppingList.txt
$ cat ShoppingList.txt
Milk
Eggs
Cheese
Tacos
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_79_0.png)

Text files created in Windows and MS-DOS are formatted with line feed characters that are not compatible with Unix/Linux systems. The **dos2unix** command reformats the specified file so that it will display properly on Unix/Linux systems. In the above example, the line feed characters in the `ShoppingList.txt` file are converted so they will display properly on Unix-based systems.

Similar to the **dos2unix** command, **unix2dos** formats text files created on Unix/Linux systems so they can be displayed properly when transferred to Windows systems.

> **Tip**
> *Conversions are done directly to the specified file. Use the -b option to create a backup of the file before converting.*

**Common usage examples:**

- `dos2unix [FILE]`: Convert a Windows text file to a Unix-formatted file
- `dos2unix -b [FILE]`: Create a backup before converting
- `unix2dos [FILE]`: Convert a Unix text file to a Windows-formatted file
- `unix2dos -b [FILE]`: Create a backup before converting the file

## Section 5: Users, Groups, and Security

### Overview

This chapter covers the most common commands related to users, groups, and security. It will also discuss topics like account creation/deletion, file and directory permissions, and other user/security related commands.

**Commands covered in this section:**

| Command | Purpose |
| :--- | :--- |
| chmod | Change file and directory permissions. |
| chown | Change the owner of a file or directory. |
| chgrp | Change the group of files and directories. |
| umask | Display/set a user's default file creation mask. |
| su | Switch user accounts. |
| sudo | Run a single command as a different user. |
| id | Display information about a user's identity. |
| groups | Display which groups a user belongs to. |
| who | Display who is logged into the system. |
| whoami | Display the current user's identity |
| w | Display detailed information about users logged in to the system. |
| last, lastb | Display the last successful/failed user logins. |
| lastlog | Display the most recent user login information. |
| finger | Display information about a user account. |
| passwd | Change passwords. |
| useradd, userdel | Create/delete user accounts. |
| adduser, deluser | Create/delete user accounts on Linux systems. |
| groupadd, groupdel | Add/remove a group. |
| usermod, groupmod | Modify user and group account settings. |
| wall | Broadcast a message to all users on the system. |
| ulimit | Display/set system resource limits. |

### Glossary of terms used in this section

- **GID (Group IDentifier)**: A numerical value assigned to a group in the /etc/group file.
- **Group**: A grouping of user accounts used to simplify security and access control.
- **Mode**: Indicator of permissions for files and directories.
- **Octal Notation**: A numerical value used to apply permissions to files and directories.
- **Permissions**: Settings used to control access to a file or directory.
- **Profile**: Collection of settings assigned to a user.
- **Symbolic Notation**: A user friendly way to display or apply permissions to files and directories.
- **UID (User IDentifier)**: A numerical value assigned to a user account in the /etc/passwd file.
- **User Account**: An account assigned to each person with login access to the local system.

### Types of Accounts

There are several types of user accounts used on Unix, Linux, and BSD systems. The graphic below illustrates the user security model used on most systems.

![](img/8f33496304c637dbf51ff6ddc3c7ff29_82_0.png)

By default, normal users and the programs they execute are given the least amount of privileges on the system. System accounts have slightly elevated privileges and are used to run system services (like a web server or FTP server). The root account has unrestricted administrative access to the entire system.

### Groups

Groups are used to simplify the management of system security. Users can be a member of one or more groups. All users are part of at least one group by default; this group is known as the user’s primary group.

### File and Directory Permissions

File and directory permissions are managed using a set of nine “flags”. The following example describes permissions found on a typical file.

![](img/8f33496304c637dbf51ff6ddc3c7ff29_82_1.png)

Within these nine flags, three sets of permissions are specified:

- User (AKA owner) permissions
- Group permissions
- Other (i.e. everyone else)

There are four types of permissions that can be used to control access to a file or directory. The following table describes each permission.

| **Symbolic** | **Meaning** |
| :---: | :---: |
| **r** | Read |
| **w** | Write |
| **x** | Execute |
| **–** | No access |

Example of directory permissions

In most cases, the owner of a file will always have full read/write access to that file. Execute permission is a special flag used for programs, scripts, and directories to indicate they are executable.

The example below displays basic file permissions.

```bash
$ ls -l ShoppingList.txt
-rw-r--r--  1 nick users 254 2009-06-01 15:35 ShoppingList.txt
```

Output of the ls -l command displaying file permissions

| **User** | **Group** | **Other** |
| :---: | :---: | :---: |
| **Symbolic** | **rw-** | **r--** | **r--** |
| **Meaning** | Read & Write | Read only | Read only |

Example of file permissions

The next example demonstrates directory permissions. Directory permissions work the same as file permissions except they are used to control access to directories.

```bash
$ ls -ld finance/
drwxr-x--- 2 root finance 4096 2009-06-12 09:48 finance/
```

Output of the ls -ld command displaying directory permissions

| **User** | **Group** | **Other** |
| :---: | :---: | :---: |
| **Symbolic** | **rwx** | **r-x** | **---** |
| **Meaning** | Read, Write, & Execute | Read only & Execute | No Access |

Example of directory permissions

Each file and directory has its own set of permissions. Permissions are not inherited from the parent directory. Additionally, directories require execute permission in order to be accessible, as shown in the previous example.
