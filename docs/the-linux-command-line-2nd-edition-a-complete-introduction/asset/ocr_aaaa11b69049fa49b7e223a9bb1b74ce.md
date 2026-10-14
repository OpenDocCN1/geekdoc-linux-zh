Imagine that the file system is a maze shaped like an upside-down tree and we are able to

![](bbox=[0.3, 0.19, 0.62, 0.42])

Figure 1: File system tree as shown by a graphical file manager

stand in the middle of it. At any given time, we are inside a single directory and we can see the files contained in the directory and the pathway to the directory above us (called the parent directory) and any subdirectories below us. The directory we are standing in is called the current working directory. To display the current working directory, we use the pwd (print working directory) command.

```
[me@linuxbox ~]$ pwd
/home/me
```

When we first log in to our system (or start a terminal emulator session) our current working directory is set to our home directory. Each user account is given its own home directory and it is the only place a regular user is allowed to write files.

# Listing The Contents Of A Directory

To list the files and directories in the current working directory, we use the ls command.

```
[me@linuxbox ~]$ ls
Desktop  Documents  Music  Pictures  Public  Templates  Videos
```