
```
value = r?4:0 + w?2:0 + x?1:0
```

which results in the following table of values for each group of three bits.

rwx  rw-  r-x  r--  -wx  -w-  --x  ---
7    6    5    4    3    2    1    0

For example, the octal number for rwxr--r-- is 764 because the user digit is 7, the group is 6 and the others is 4.

In addition to the mode bits, a file's permission string is usually displayed with a single character file attribute that characterizes the file type. The character, which appears to the left of the mode bits, can be one of - (regular file), d (directory), b (buffered special file), c (character special file), l (symbolic link), p (pipe), or s (socket).

## 1.8.2.5 Viewing and Modifying File Attributes

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

There are 156 lines, 387 words, and 3304 bytes in the file. Other options provide different information.

Commands that alter the attributes of a file are:

| Command | Explanation |
|---|---|
| chmod <mode> <files> | change the file permissions |
| chown <owner> <files> | change the file ownership |
| chgrp <group> <files> | change the group ownership |
| touch <files> | update timestamps of files; create empty files (a file of size 0) |

## 1.8.2.6 Symbolic Links

A symbolic link, also called a soft link, is a file that stores a string containing the pathname of another file. The stored string has a length of SYMLINK_MAX bytes or fewer. This string is not part of the content of the file, but can be used by programs to access the file whose pathname it contains. Symbolic links are like shortcuts in the Windows operating system; they have no data in themselves, but instead point to files. They are useful for overcoming the limitations of hard links that they cannot link to directories and cannot cross file systems. For example, suppose that one frequently accesses a directory whose absolute path is

```
/data/research/biochem/proteins
```

He or she could create a link in his or her home directory for easier access to this directory, as follows:

```
$ ln -s /data/research/biochem/proteins ~/proteins
```

The ln command, with the -s option, creates symbolic links. The pathname /data/research/biochem/proteins would be stored in the file ~/proteins in such a way that the commands that use the filename proteins would replace it by the pathname stored there.

Symbolic links pose hazards for the operating system because of the possibility of circular references and infinite loops. More will be said about them in Chapter 3.

## 1.9 Under the Hood: How Logging In Works

When you log in to a UNIX system, what actually happens? What does it mean to be logged in?

There is no single answer to this question, as it depends upon (1) which version of UNIX is running and (2) whether the login is at the console, or within a terminal window, or across a network using a protocol such as SSH. Fortunately, the way that logging in works at the console or in a terminal window in the predominant UNIX systems – Linux, Mac OS, Solaris, and BSD variants – is pretty much the same, with minor variations, and the way that it works over a network, while very different from how it works at a console or terminal window, is similar across the major UNIX systems.

> 24 BSD stands for Berkeley Software Distribution. See the historical notes at the end of this chapter.
