# FILE LISTINGS, OWNERSHIPS, AND PERMISSIONS

Managing files under Linux is different from managing files under Windows NT, and radically different from managing files under Windows 95/98. In this section, we discuss basic file management tools for Linux. We'll start with specifics on some useful general-purpose commands, and then step back and look at some background information.

# Listing Files: ls

The **ls** command is used to list all the files in a directory. Of more than 26 available options, the ones listed here are the most commonly used. The options can be used in any combination. See the *texinfo* page for a complete list.

| **Options for ls** | **Description** |
|:---|:---|
| -l | Long listing. In addition to the filename, shows the file size, date/time, permissions, ownership, and group information. |
| -a | All files. Shows all files in the directory, including hidden files. Names of hidden files begin with a period. |
| -1 | Single column listing. |
| -R | Recursively lists all files and subdirectories. |

To list all files in a directory with a long listing:

```
[root@ford /root]# ls -1a
```

To list a directory's nonhidden files that start with A:

```
[root@ford /root]# ls A*
```

# Types of Files and Directories

Under Linux (and UNIX in general), almost everything is abstracted to a file. Originally this was done to simplify the programmer's job. Instead of having to communicate directly with device drivers, special files (which look like ordinary files to the application) are used as a bridge. Several types of files accommodate all these file uses.

# Normal Files

Normal files are just that—normal. They contain data or executables, and the operating system makes no assumptions about their contents.

# Directories

Directory files are a special instance of normal files. Directory files list the location of other files, some of which may be other directories. In general, the contents of directory files are...