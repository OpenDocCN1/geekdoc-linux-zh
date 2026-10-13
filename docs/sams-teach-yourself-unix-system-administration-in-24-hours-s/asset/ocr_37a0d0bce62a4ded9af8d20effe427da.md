naturally expands to cover a variety of additional topics, including umask, chmod, and more.

# Task 4.1: The Basics of File Permissions

To start at the beginning, all directories in Unix are treated as if they were files. Similar to files, directories also have a user owner and group owner, and similar to files, groups have a finite number of possible permissions. Both files and directories have their permissions split into three categories: user, group, and others.

+   1. To start, here's a long-format listing of a few files and directories:

```
$ ls -lAF
total 172
drwxr-x... 3 taylor coders 4096 Jan 7 21:35 ./
drwxr-x... 13 taylor coders 4096 Jan 7 21:35 ../
-rw-rw-... 1 taylor coders 263 Dec 5 05:12 snapshot.sh
-rw-rw-... 1 taylor coders 153600 Dec 5 05:12 sourcefiles.cpio
drwxrwxr... 2 taylor coders 4096 Dec 5 05:12 Src/
```

The permission string is of, course, the sequence of dashes, r, w, and x at the beginning of each file listed. The owner of each file (or directory) is listed, then the group. In this case, notice that all files are associated with account taylor and group coders.

The .. (parent) directory is an interesting example of permission strings because it offers read, write, and execute permission (rwx) to the owner of the directory (taylor), read and execute permission to other members of the group coders, and no access to anyone else on the system.

+   2. To change file permissions, use the chmod command. Although you can specify a target octal permission (for example, 0750), it's probably easiest to use mnemonic change notation instead. To fix the peculiar permissions of the current directory, for example:

```
chmod u+x .
```

says "user plus execute" (user = file owner, but the o notation is for others, confusingly).

+   3. To be able to experiment, two useful Unix commands should be highlighted: touch and mkdir.

touch updates the last-modified-time of a specific file or directory, but if the file doesn't exist, touch creates an empty file. mkdir, of course, makes directories.

A quick example. Note the default permissions for the new file and directory that are set up: