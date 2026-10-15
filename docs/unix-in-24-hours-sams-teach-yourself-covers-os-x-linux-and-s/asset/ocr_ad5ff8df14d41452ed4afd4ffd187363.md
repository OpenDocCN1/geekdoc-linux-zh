# Hour 5. Ownership and Permissions

# Goals for This Hour

In this hour, you will learn

+   - About file permissions settings
+   - About directory permissions settings
+   - How to modify file and directory permissions with `chmod`
+   - About working with `chmod` numeric permissions strings
+   - How to establish default file and directory permissions with `umask`
+   - How to identify the owner and group for any file or directory

This hour focuses on teaching the basics of Unix file permissions. Topics include setting and modifying file permissions with `chmod`, analyzing file permissions as shown by the `ls -l` command, and setting up default file permissions with the `umask` command. Permission is only half the puzzle, however, and you’ll also learn about file ownership and group ownership, and how to change either for any file or directory.

The preceding hour contained the first tutorial dealing with the permissions of a file or directory using the -l option with `ls`. If you haven’t read that material recently, it would help to review it. In this hour, you’ll learn about another option to `ls` that tells Unix to show the group and owner of files or directories. Two more commands are introduced and discussed in detail: `chmod` for changing the permissions of a file and `umask` for defining default permissions.

# Working with File Permissions

As you have seen in examples throughout the book, Unix treats all directories as files; each has its own size (sometimes independent of its contents), its own permissions strings, and more. As a result, unless it’s an important difference, from here on when I talk about files, I’m referring to both files and directories. Logic will confirm whether commands can apply to both, or to files only, or to directories only. (For example, you can’t edit a directory, and you can’t store files inside other files.)

# Task 5.1: Understanding File Permissions Settings

In the past hour you learned a bit about how to interpret the information that `ls` offers on file permissions when it is used with the -l flag. Consider the following example:

Click here to view code image

```
% ls -l
total 403
drwx--  2 taylor        512 Sep 30 10:38 Archives/
drwx--  3 taylor        512 Oct  1 08:23 InfoWorld/
-rw---  1 taylor     106020 Oct 10 13:47 LISTS
```