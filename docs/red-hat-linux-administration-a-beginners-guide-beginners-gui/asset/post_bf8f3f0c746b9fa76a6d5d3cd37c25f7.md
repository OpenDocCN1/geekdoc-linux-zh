
where `program_name` identifies the program you're interested in. For example:

```
[michael@workbox michael]$ man 1s
```

While reading about UNIX and UNIX-related information sources (newsgroups and so forth), you may encounter references to commands followed by numbers in parentheses—for example, 1s(1). The number represents the section of the manual pages (see Table 6-1). Each section covers various subject areas, to accommodate the fact that some tools (such as printf) are commands in the C programming language as well as command-line commands.

To refer to a specific `man` section, simply specify the section number as the first parameter and then the command as the second parameter. For example, to get the C programmers' information on printf, you'd enter this:

```
[michael@workbox michael]$ man 3 printf
```

To get the command-line information, you'd enter this:

```
[michael@workbox michael]$ man 1 printf
```

By default, the lowest section number gets displayed first.

Unfortunately, this organization is sometimes difficult to use. You may find it helpful to use the graphical interface for this library of documentation, developed as part of the GNOME project; it's called gnome-help. If you have installed GNOME on a system, you can always start it from a terminal window yourself with this command:

```
[michael@workbox michael]$ gnome-help
```

| **Manual Section** | **Subject** |
| --- | --- |
| 1 | User tools |
| 2 | System calls |
| 3 | C library calls |
| 4 | Device driver information |
| 5 | Configuration files |
| 6 | Games |
| 7 | Packages |
| 8 | System tools |

**Table 6-1** Man Page Section Descriptions

![](img/ec2066d370d3af1a767664d36aa7ddfe_178_0.png)

A handy option to the **man** command is **-k** preceding the *command parameter*. With this option, **man** will search the summary information of all the man pages and list pages matching your specified command, along with their section number. For example:

```
[michael@workbox michael]$ man -k printf
```

# The texinfo System

Another common form of documentation is *texinfo*. Established as the GNU standard, texinfo is a documentation system similar to the hyperlinked World Wide Web format. Because documents can be hyperlinked together, texinfo is often easier to read, use, and search.

To read the texinfo documents on a specific tool or application, invoke **info** with the parameter specifying the tool’s name. For example, to read about **emacs**, type:

```
[michael@workbox michael]$ info emacs
```

In general, you will want to verify that a man page exists before using **info** (there is still a great deal more information available in **man** format than in texinfo). If you run **info** on a command that isn’t described in texinfo but does have a man page, the information from **man** is often displayed. On the other hand, some man pages will explicitly state that the texinfo pages are more authoritative and should be read instead.

While **info** is a much more powerful system, it’s also more complex as a result. A good starting place may be:

```
[michael@workbox michael]$ info info
```

Alternatively you may want to start **info**, and press CTRL-H to bring up the help menu, and then press H to start the built-in tutorial.

# 6.4

## Understanding File Listings, Ownerships, and Permissions

Managing files under Linux is different than managing files under Windows 2000/.NET, and radically different from managing files under Windows 95/98. This section discusses basic file management tools for Linux. We’ll start with specifics on some useful general-purpose commands and then step back and look at some background information.

# Listing Files: ls

The **ls** command is used to list all the files in a directory. Of more than 26 available options, the ones listed here are the most commonly used. The options can be used in any combination. See the **texinfo** page for a complete list.

| Option for ls | Description |
|---|---|
| -l | Long listing. In addition to the filename, shows the file size, date/time, permissions, ownership, and group information. |
| -a | All files. Shows all files in the directory, including hidden files. Names of hidden files begin with a period. |
| -1 | Single column listing. |
| -R | Recursively lists all files and subdirectories. |

To list all files in a directory with a long listing, type this command:

```
[michael@workbox michael]$ ls -1a
```

To list a directory’s nonhidden files that start with *A*, type this:

```
[michael@workbox michael]$ ls A\*
```

# File and Directory Types

Under Linux (and UNIX in general), almost everything is abstracted to a file. Originally this was done to simplify the programmer’s job. Instead of having to communicate directly with device drivers, special files (which look like ordinary files to the application) are used as a bridge. Several types of files accommodate all these file uses.

## Normal Files

Normal files are just that—normal. They contain data or executables, and the operating system makes no assumptions about their contents.

## Directories

*Directory files* are a special instance of normal files. Directory files list the location of other files, some of which may be other directories. (This is similar to folders in Windows.) In general, the contents of directory files won’t be of importance to your daily operations, unless you need to open and read the file yourself rather than using existing applications to navigate directories. (This would be similar to trying to read the DOS File Allocation Table directly rather than using command.com to navigate directories, or using the findfirst/findnext system calls.)

## Hard Links

Each file in the Linux file system gets its own $i$-node. An i-node keeps track of a file's attributes and its location on the disk. If you need to be able to refer to a single file using two separate filenames, you can create a *hard link*. The hard link will have the same i-node as the original file and will therefore look and behave just like the original. With every hard link that is created, a *reference count* is incremented. When a hard link is removed, the reference count is decremented. Until the reference count reaches zero, the file will remain on disk.

> A hard link *cannot exist* between two files on separate partitions. This is because the hard link refers to the original file by $i$-node, and a file's $i$-node may differ among file systems.

## Symbolic Links

Unlike a hard link, which points to a file by its i-node, a *symbolic link* points to another file by its name. This allows symbolic links (often abbreviated *symlinks*) to point to files located on other partitions, even other network drives.

## Block Devices

Since all device drivers are accessed through the file system, files of type *block device* are used to interface with devices such as disks. A block device file has three identifying traits:

- It has a major number.
- It has a minor number.
- When viewed using the `ls -l` command, it shows **b** as the first character of the permissions.

For example:

```
[michael@workbox michael]$ ls -l /dev/hda
brw-rw---- 1 root disk 3, 0 May 5 1998 /dev/hda
```

Note the **b** at the beginning of the file's permissions; the **3** is the major number, and the **0** is the minor number.

A block device file's major number identifies the represented device driver. When this file is accessed, the minor number is passed to the device driver as a parameter telling it which device it is accessing. For example, if there are two serial ports, they will share the same device driver and thus the same major number, but each serial port will have a unique minor number.

## Character Devices

Similar to block devices, character devices are special files that allow you to access devices through the file system. The obvious difference between block and character devices is that block devices communicate with the actual devices in large blocks, whereas character devices work one character at a time. (A hard disk is a block device; a modem is a character device.) Character device permissions start with a c, and the file has a major and a minor number. For example:

```
[michael@workbox michael]$ ls -l /dev/ttyS0
crw------- 1 root tty 4, 64 May 5 1998 /dev/ttyS0
```

## Named Pipes

Named pipes are a special type of file that allows for interprocess communication. Using the mknod command (discussed later in this module), you can create a named pipe file that one process can open for reading and another process can open for writing, thus allowing the two to communicate with one another. This works especially well when a program refuses to take input from a command-line pipe, but another program needs to feed the other one data and you don’t have the disk space for a temporary file.

For a named pipe file, the first character of its file permissions is a p. For example:

```
[michael@workbox michael]$ ls -l mypipe
prw-r--r-- 1 root root 0 Jun 16 10:47 mypipe
```

# Changing Ownership: chown

The chown command allows you to change the ownership of a file to someone else. Only the root user can do this. (Normal users may not give away file ownership or steal ownership from another user.) The format of the command is as follows:

```
[root@workbox /root]$ chown [-R] username filename
```

where username is the login of the user to whom you want to assign ownership, and filename is the name of the file in question. The filename may be a directory as well.

The -R option applies when the specified filename is a directory name. This option tells the command to recursively descend through the directory tree and apply the new ownership not only to the directory itself, but to all of the files and directories within it.
