
# LAB 25

## Special Directories and Files

### Lab Objective

Learn how to use temporary files and directories, symbolic links, and special permissions.

### Lab Purpose

In this lab, you will work with symbolic links, special file/directory permissions, and temporary files and directories.

### Lab Tool

`Ubuntu 18.04` (or another distro of your choice)

### Lab Topology

A single Linux machine, or virtual machine

### Lab Walkthrough

#### Task 1

Open the Terminal and run: `ls -ld /tmp`

Notice the permissions: `drwxrwxrwt`

The `t` at the end indicates what is called the sticky bit. This means that only users/groups who own a given file may modify it. This is important on world-writable directories, such as those holding temporary files, to prevent users from messing with other users’ files.

#### Task 2

Now run:

```
ln -sv $(mktemp) mytmp
ls -l mytmp
rm mytmp
```

What just happened? `mktemp` created a randomly-named temporary file. Then you created a symbolic link to that file called `mytmp`. The `ls` output shows this link. A symbolic link
