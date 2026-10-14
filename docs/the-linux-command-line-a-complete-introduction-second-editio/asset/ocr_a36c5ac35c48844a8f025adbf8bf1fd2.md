standing in is called the *current working directory*. To display the current working directory, we use the pwd (print working directory) command.

```
[me@linuxbox ~]$ pwd
/home/me
```

When we first log in to our system (or start a terminal emulator session), our current working directory is set to our *home directory*. Each user account is given its own home directory, and it is the only place a regular user is allowed to write files.

# Listing the Contents of a Directory

To list the files and directories in the current working directory, we use the ls command.

```
[me@linuxbox ~]$ ls
Desktop Documents Music Pictures Public Templates Videos
```

Actually, we can use the ls command to list the contents of any directory, not just the current working directory, and there are many other fun things it can do as well. We’ll spend more time with ls in Chapter 3.

# Changing the Current Working Directory

To change our working directory (where we are standing in the tree-shaped maze), we use the cd command. To do this, type cd followed by the pathname of the desired working directory. A pathname is the route we take along the branches of the tree to get to the directory we want. We can specify pathnames in one of two different ways: as *absolute pathnames* or as *relative pathnames*. Let’s deal with absolute pathnames first.

# Absolute Pathnames