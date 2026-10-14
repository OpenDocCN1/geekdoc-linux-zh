
To see the current amount of free space on your disk drives, enter df:

```
[me@linuxbox ~]$ df
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/sda2      15115452 5012392  9980716 34% /
/dev/sda5      59631908 20545424 30008432 47% /home
/dev/sda1       147764   17370   122765 13% /boot
tmpfs           256856      0   256856  0% /dev/shm
```

Likewise, to display the amount of free memory, enter the free command:

```
[me@linuxbox ~]$ free
             total       used       free     shared    buffers     cached
Mem:       513712     503976      9736          0       5312     122916
-/+ buffers/cache:   375748     137964
Swap:      1052248    104712     947536
```

## Ending a Terminal Session

We can end a terminal session by either closing the terminal emulator window or entering the exit command at the shell prompt:

```
[me@linuxbox ~]$ exit
```

## THE CONSOLE BEHIND THE CURTAIN

Even if we have no terminal emulator running, several terminal sessions continue to run behind the graphical desktop. Called virtual terminals or virtual consoles, these sessions can be accessed on most Linux distributions by pressing CTRL-ALT-F1 through CTRL-ALT-F6 on most systems. When a session is accessed, it presents a login prompt into which we can enter our username and password. To switch from one virtual console to another, press ALT and F1-F6. To return to the graphical desktop, press ALT-F7.

## 2

## NAVIGATION

The first thing we need to learn (besides just typing) is how to navigate the filesystem on our Linux system. In this chapter we will introduce the following commands:

- pwd—Print name of current working directory.
- cd—Change directory.
- ls—List directory contents.

### Understanding the Filesystem Tree

Like Windows, a Unix-like operating system such as Linux organizes its files in what is called a *hierarchical directory structure*. This means that they are organized in a tree-like pattern of directories (sometimes called folders in other systems), which may contain files and other directories. The first directory in the filesystem is called the *root directory*. The root directory contains files and subdirectories, which contain more files and subdirectories, and so on.

Note that unlike Windows, which has a separate filesystem tree for each storage device, Unix-like systems such as Linux always have a single filesystem tree, regardless of how many drives or storage devices are attached to the computer. Storage devices are attached (or more correctly, mounted) at various points on the tree according to the whims of the system administrator, the person (or persons) responsible for the maintenance of the system.

### The Current Working Directory

Most of us are probably familiar with a graphical file manager, which represents the filesystem tree, as in Figure 2-1. Notice that the tree is usually shown upended, that is, with the root at the top and the various branches descending below.

However, the command line has no pictures, so to navigate the filesystem tree, we need to think of it in a different way.

Imagine that the filesystem is a maze shaped like an upside-down tree and we are able to stand in the middle of it. At any given time, we are inside a single directory and we can see the files contained in the directory and the pathway to the directory above us (called the parent directory) and any sub-directories below us. The directory we are standing in is called the current working directory. To display the current working directory, we use the pwd (print working directory) command:

![](img/9923d0e9dcb7396145d88fba19cb5312_39_0.png)

```
[me@linuxbox ~]$ pwd
/home/me
```

When we first log in to our system (or start a terminal emulator session), our current working directory is set to our home directory. Each user account is given its own home directory, which is the only place the user is allowed to write files when operating as a regular user.

### Listing the Contents of a Directory

To list the files and directories in the current working directory, we use the ls command:

```
[me@linuxbox ~]$ ls
Desktop Documents Music Pictures Public Templates Videos
```

Actually, we can use the ls command to list the contents of any directory, not just the current working directory, and it can do many other fun things as well. We'll spend more time with ls in Chapter 3.
