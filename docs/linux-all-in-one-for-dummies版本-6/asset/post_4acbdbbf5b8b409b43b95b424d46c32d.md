
## TABLE 2-3 Typical Environment Variables in Linux

| Environment Variable | Contents |
|---|---|
| DISPLAY | The name of the display on which the X Window System displays output (typically set to :0.0) |
| HOME | Your home directory |
| HOSTNAME | The host name of your system |
| LOGNAME | Your login name |
| MAIL | The location of your mail directory |
| PATH | The list of directories in which the shell looks for programs |
| SHELL | Your shell (SHELL=/bin/bash for bash) |
| TERM | The type of terminal |

## Changing User and Group Ownership of Files

In Linux, each file or directory has two types of owners: a user and a group. In other words, a user and group own each file and directory. The user and group ownerships can control who can access a file or directory.

To view the owner of a file or directory, use the ls -l command to see the detailed listing of a directory. Here’s a typical file’s information:

```
-rw-rw-r-- 1 kdulaney kdulaney 40909 Aug 16 20:37
composer.txt
```

In this example, the first set of characters shows the file’s permission setting — who can read, write, or execute the file. The third and fourth fields (in this example, kdulaney kdulaney) indicate the user and group owner of the file. Each user has a private group that has the same name as the username. Thus, most files appear to show the username twice when you list user and group ownership.

As a system administrator, you may decide to change the group ownership of a file to a common group. Suppose that you want to change the group ownership of the composer.txt file to the class group. To do so, log in as root and then type the following command:

```
chgrp class composer.txt
```

This chgrp command changes the group ownership of composer.txt to class.

You can use the chown command to change the user owner. The command has the following format:

```
chown username filename
```

To change the user ownership of a file named sample.jpg to kdulaney, type

```
chown kdulaney sample.jpg
```

The chown command can change both the user and group owner at the same time. To change the user owner to kdulaney and the group owner to class, type

```
chown kdulaney.class composer.txt
```

In other words, you simply append the group name to the username with a period in between the two values.

## IN THIS CHAPTER

- Navigating the Linux file system
- Sharing Files through NFS
- Performing file backup and restoration
- Mounting the NTFS file system
- Accessing MS-DOS files

## Chapter 3

## Managing File Systems

A file system refers to the organization of files and directories. As a system administrator, you have to perform certain operations to manage file systems on various storage media. You have to know, for example, how to mount — add a file system on a storage medium by attaching it to the overall Linux file system. You also have to back up important data and restore files from a backup. Other file-system operations include sharing files with the Network File System (NFS) and accessing MS-DOS files. This chapter shows you how to perform all file-system management tasks.

## Exploring the Linux File System

Whether you are studying for the Linux-related certification exams or just trying to understand the working of Linux more, it is important to know that the files and directories in your PC store information in an organized manner, just like paper filing systems. When you store information on paper, you typically put several pages in a folder and then store the folder in a file cabinet. If you have many folders, you probably have some sort of filing system. You might label each

folder’s tab and then arrange them alphabetically in the file cabinet, for example. You might have several file cabinets, each with lots of drawers, which in turn contain folders full of pages.

Operating systems such as Linux organize information in your computer in a manner similar to your paper filing system. Linux uses a file system to organize all information in your computer. The storage media aren’t a metal file cabinet and paper, of course. Instead, Linux stores information on devices such as hard drives, USB drives, and DVD drives.

To draw an analogy between your computer’s file system and a paper filing system, think of a disk drive as being the file cabinet. The drawers in the file cabinet correspond to the directories in the file system. The folders in each drawer are also directories — because a directory in a computer file system can contain other directories. You can think of files as being the pages inside the folder — where the actual information is stored. Figure 3-1 illustrates the analogy between a file cabinet and the Linux file system.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_348_0.png)

FIGURE 3-1:
It's a bit of a stretch, but you can think of the Linux file system as being similar to a filing cabinet.

The Linux file system has a hierarchical structure. Directories can contain other directories, which in turn contain individual files.

Everything in your Linux system is organized in files and directories. To access and use documents and programs on your system, you have to be familiar with the file system.

## Understanding the file-system hierarchy

For basic administration and for exam study alike, know that the Linux file system is organized like a tree, with a root directory from which all other directories branch out. When you write a complete pathname, the root directory is represented by a single slash (/). Then there’s a hierarchy of files and directories. Parts of the file system can be on different physical drives or in different hard drive partitions.

Linux uses a standard directory hierarchy. Figure 3-2 shows some of the standard parts of the Linux file system. You can create new directories anywhere in this structure.

FIGURE 3-2:
The Linux file system uses a standard directory hierarchy similar to this one.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_349_0.png)

Write the name of any file or directory by concatenating the names of directories that identify where that file or directory is and by using the forward slash (/) as a separator. In Figure 3-2, the usr directory at the top level is written as /usr because the root directory (/) contains usr. On the other hand, the X11R6 directory is inside the usr directory, which is inside the root directory (/). Therefore, the X11R6 directory is uniquely identified by the name /usr/X11R6. This type of full name is a pathname because the name identifies the path you take from the root directory to reach a file. Thus, /usr/X11R6 is a pathname.

Each of the standard directories in the Linux file system has a specific purpose. Table 3-1, Table 3-2, and Table 3-3 summarize these directories.

## Standard Directories in Linux File System

| Directory | Used to Store |
|---|---|
| /bin | Executable files for user commands (for use by all users) |
| /boot | Files needed by the bootloader to load the Linux kernel |
| /dev | Device files |
| /etc | Host-specific system configuration files |
| /home | User home directories |
| /lib | Shared libraries and kernel modules |
| /media | Mount point for removable media |
| /mnt | Mount point for a temporarily mounted file system |
| /opt | Add-on application software packages |
| /root | Home directory for the root user |
| /sbin | Utilities for system administration |
| /srv | Data for services (such as web and FTP) offered by this system |
| /tmp | Temporary files |

## The /usr Directory Hierarchy

| Directory | Secondary Directory Hierarchy |
|---|---|
| /usr/bin | Most user commands |
| /usr/games | Many games install here though they are not technically required to do so other than for historic reasons |
| /usr/include | Directory for *include files* — files that are inserted into source code of applications by using various directives — used in developing Linux applications |
| /usr/lib | Libraries used by software packages and for programming |
| /usr/libexec | Libraries for applications |
| /usr/local | Any local software |
| /usr/sbin | Nonessential system administrator utilities |
| /usr/share | Shared data that doesn't depend on the system architecture (whether the system is an Intel PC or a Sun SPARC workstation) |
| /usr/src | Source code |
