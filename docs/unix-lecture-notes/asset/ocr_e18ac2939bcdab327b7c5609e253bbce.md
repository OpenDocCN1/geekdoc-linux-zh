```
value = r?4:0 + w?2:0 + x?1:0
```

which results in the following table of values for each group of three bits.

rwx  rw-  r-x  r--  -wx  -w-  --x  ---
7    6    5    4    3    2    1    0

For example, the octal number for rwxr--r-- is 764 because the user digit is 7, the group is 6 and the others is 4.

In addition to the mode bits, a file's permission string is usually displayed with a single character file attribute that characterizes the file type. The character, which appears to the left of the mode bits, can be one of - (regular file), d (directory), b (buffered special file), c (character special file), l (symbolic link), p (pipe), or s (socket).

# 1.8.2.5 Viewing and Modifying File Attributes

To see the attributes of a file, use the -l option to the ls command: The "-l" means "long listing" and it prints the permission string, the number of links to the file, the user-name of the owner, the group name of the group, the number of bytes in the file, the last modification time, and the file link. For example, to look at the attributes of the file named .bashrc in the current working directory, I would type

```
$ ls -l ~/.bashrc
-rw-r--r-- 1 sweiss faculty 3304 Sep 22 13:05 .bashrc
```

This file is a regular file and can be read and modified by me, its owner (-rw-). It can be read by anyone in the faculty group (r--), and it can be read by anyone else (r--). ls has many other options, for displaying additional information. Read its man page for details. You can also use the stat command, which will provide additional information:

```
$ stat .bashrc
    File: '.bashrc'
    Size: 3304      Blocks: 8       IO Block: 4096  regular file
    Device: 1b4/24d Inode: 1318      Links: 1
    Access:(0644/-rw-r--r--):Uid:(1220/ sweiss)Gid:(400/ faculty)
    Access: 2010-12-20 13:20:04.582733000 -0500
    Modify: 2010-09-22 13:05:11.271251000 -0400
    Change: 2010-09-22 13:05:11.278893000 -0400
```

You can get the count of bytes, words, and lines with wc:

```
$ wc .bashrc
156 387 3304 .bashrc
```