```
```text
% touch iecc.list
% ls -t
iecc.list        RUMORS.18Sept    News/             OWL/              src/
mailing.lists    LISTS             bin/              Mail/
Cancelled.mail   newlists          InfoWorld/        Archives/
```
```

You probably will not use `touch` for this purpose very often.

+   2. If you try to use the `touch` command on a file that doesn’t exist, the program creates the file:

[Click here to view code image](#)

```
```text
% ls
Archives/        LISTS             OWL/              iecc.list        src/
Cancelled.mail   Mail/             RUMORS.18Sept     mailing.lists
InfoWorld/       News/             bin/              newlists
% touch new.file
% ls
Archives/        LISTS             OWL/              iecc.list        newlists
Cancelled.mail   Mail/             RUMORS.18Sept     mailing.lists     src/
InfoWorld/       News/             bin/              new.file
% ls -l new.file
-rw-rw----  1 taylor          0 Oct 10 16:28 new.file
```
```

The new file has zero bytes, as can be seen in the `ls -l` output. Notice that by default the files are created with read and write permission for the user and anyone in the user’s group. You’ll learn in the next hour how to specify, by using the `umask` command, your own default permission for files.

You won’t need `touch` very often, but it’s valuable to know.

# Task 4.10: Checking Disk Space Usage with `du`

One advantage that Windows and Macintosh systems have over Unix is that they make it easy to find out how much disk space you’re using and how much remains available. On a Mac, viewing folders by size shows disk space used, and the bottom of any Finder window shows available space.

Like a close-mouthed police informant, Unix never volunteers any information, so you need to learn two new commands. The `du` (disk usage) command is used to find out how much disk space is used; the `df` (disk free) command is used to find out how much space is available.

+   1. The `du` command lists the size, in kilobytes, of all directories at or below the current point in the file system.

```
```text
% du
11       ./OWL
38       ./elm
20       ./Archives
14       ./InfoWorld/PIMS
28       ./InfoWorld
710      ./Mail
191      ./News
25       ./bin
35       ./src
1627     .
```
```