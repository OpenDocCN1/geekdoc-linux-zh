
# cp VERSUS ln

The following commands verify that ln does not make an additional copy of a file. Create a file, use ln to make an additional link to the file, change the contents of the file through one link, and verify the change through the other link:

```
$ cat file_a
This is file A.
$ ln file_a file_b
$ cat file_b
This is file A.
$ vim.tiny file_b
....
$ cat file_b
This is file B after the change.
$ cat file_a
This is file B after the change.
```

If you try the same experiment using cp instead of ln and change a copy of the file, the difference between the two utilities will become clearer. Once you change a copy of a file, the two files are different:

```
$ cat file_c
This is file C.
$ cp file_c file_d
$ cat file_d
This is file C.
$ vim.tiny file_d
....
$ cat file_d
This is file D after the change.
$ cat file_c
This is file C.
```

# ls and link counts

You can use ls with the -l option, followed by the names of the files you want to compare, to confirm that the status information is the same for two links to the same file and is different for files that are not linked. In the following example, the 2 in the links field (just to the left of max) shows there are two links to file_a and file_b (from the previous example):

```
$ ls -l file_a file_c file_d file_e
-rw-r--r-- 2 max pubs 33 2010-05-24 10:52 file_a
-rw-r--r-- 2 max pubs 33 2010-05-24 10:52 file_b
-rw-r--r-- 1 max pubs 16 2010-05-24 10:55 file_c
-rw-r--r-- 1 max pubs 33 2010-05-24 10:57 file_d
```

Although it is easy to guess which files are linked to one another in this example, ls does not explicitly tell you.

# ls and inodes

Use ls with the -i option to determine without a doubt which files are linked. The -i option lists the inode (page 1153) number for each file. An inode is the control structure for a file. If the two filenames have the same inode number, they share the same control structure and are links to the same file. Conversely, when two filenames have different inode numbers, they are different files. The following example shows that **file_a** and **file_b** have the same inode number and that **file_c** and **file_d** have different inode numbers:

```
$ ls -i file_a file_b file_c file_d
3534 file_a  3534 file_b  5800 file_c  7328 file_d
```

All links to a file are of equal value: The operating system cannot distinguish the order in which multiple links were created. When a file has two links, you can remove either one and still access the file through the remaining link. You can remove the link used to create the file, for example, and, as long as one link remains, still access the file through that link.

# SYMBOLIC LINKS

In addition to hard links, Linux supports *symbolic links*, also called *soft links* or *symlinks*. A hard link is a pointer to a file (the directory entry points to the inode), whereas a symbolic link is an *indirect* pointer to a file (the directory entry contains the pathname of the pointed-to file—a pointer to the hard link to the file).

Symbolic links were developed because of the limitations inherent in hard links. You cannot create a hard link to a directory, but you can create a symbolic link to a directory.

In many cases the Linux file hierarchy encompasses several filesystems. Because each filesystem keeps separate control information (that is, separate inode tables or filesystem structures) for the files it holds, it is not possible to create hard links between files in different filesystems. A symbolic link can point to any file, regardless of where it is located in the file structure, but a hard link to a file must be in the same filesystem as the other hard link(s) to the file. When you create links only among files in your home directory, you will not notice this limitation.

A major advantage of a symbolic link is that it can point to a nonexistent file. This ability is useful if you need a link to a file that is periodically removed and re-created. A hard link keeps pointing to a “removed” file, which the link keeps alive even after a new file is created. In contrast, a symbolic link always points to the newly created file and does not interfere when you delete the old file. For example, a symbolic link could point to a file that gets checked in and out under a source code control system, a **.o** file that is re-created by the C compiler each time you run **make**, or a log file that is repeatedly archived.

Although they are more general than hard links, symbolic links have some disadvantages. Whereas all hard links to a file have equal status, symbolic links do not have the same status as hard links. When a file has multiple hard links, it is analogous to a person having multiple full legal names, as many married women do. In contrast, symbolic links are analogous to nicknames. Anyone can have one or more nicknames, but these nicknames have a lesser status than legal names. The following sections describe some of the peculiarities of symbolic links.

## In: **CREATES SYMBOLIC LINKS**

The *ln* utility (or the --**symbolic** (or -s) option creates a symbolic link. The following example creates a symbolic link **/tmp/s3** to the file **sum** in Max’s home directory. When you use an `ls -l` command to look at the symbolic link, `ls` displays the name of the link and the name of the file it points to. The first character of the listing is `l` (for link).

![](img/2344fc4a798f29dca9e8b5ed7288171a_280_0.png)

```
$ ln --symbolic /home/max/sum /tmp/s3
$ ls -l /home/max/sum /tmp/s3
-rw-rw-r--  1 max max 38 2010-06-12 09:51 /home/max/sum
lrwxrwxrwx  1 max max 14 2010-06-12 09:52 /tmp/s3 -> /home/max/sum
$ cat /tmp/s3
This is sum.
```

The sizes and times of the last modifications of the two files are different. Unlike a hard link, a symbolic link to a file does not have the same status information as the file itself.

You can also use `ln` to create a symbolic link to a directory. When you use the `--symbolic` option, it works as expected whether the file you are creating a link to is an ordinary file or a directory.

### Use absolute pathnames with symbolic links

> Symbolic links are literal and are not aware of directories. A link that points to a relative pathname, which includes simple filenames, assumes the relative pathname is relative to the directory that the link was created *in* (not the directory the link was created *from*). In the following example, the link points to the file named **sum** in the /tmp directory. Because no such file exists, `cat` gives an error message:
>
> $ pwd
> /home/max
> $ ln --symbolic sum /tmp/s4
> $ ls -l sum /tmp/s4
> lrwxrwxrwx 1 max max   3 2010-06-12 10:13 /tmp/s4 -> sum
> -rw-rw-r-- 1 max max  38 2010-06-12 09:51 sum
> $ cat /tmp/s4
> cat: /tmp/s4: No such file or directory

### **optional** cd AND SYMBOLIC LINKS

When you use a symbolic link as an argument to `cd` to change directories, the results can be confusing, particularly if you did not realize that you were using a symbolic link.

If you use `cd` to change to a directory that is represented by a symbolic link, the `pwd` shell builtin (page 261) lists the name of the symbolic link. The `pwd` utility (/bin/pwd) lists the name of the linked-to directory, not the link, regardless of how you got there.

```
$ ln -s /home/max/grades /tmp/grades.old
$ pwd
/home/max
$ cd /tmp/grades.old
$ pwd
/tmp/grades.old
$ /bin/pwd
/home/max/grades
```

When you change directories back to the parent, you end up in the directory holding the symbolic link:

```
$ cd ..
$ pwd
/tmp
$ /bin/pwd
/tmp
```

# rm: Removes a Link

When you create a file, there is one hard link to it. You can then delete the file or, using Linux terminology, remove the link with the rm utility. When you remove the last hard link to a file, you can no longer access the information stored there and the operating system releases the space the file occupied on the disk for use by other files. This space is released even if symbolic links to the file remain. When there is more than one hard link to a file, you can remove a hard link and still access the file from any remaining link. Unlike DOS and Windows, Linux does not provide an easy way to undelete a file once you have removed it. A skilled hacker, however, can sometimes piece the file together with time and effort.

When you remove all hard links to a file, you will not be able to access the file through a symbolic link. In the following example, cat reports that the file total does not exist because it is a symbolic link to a file that has been removed:

```
$ ls -l sum
-rw-r--r-- 1 max pubs 981 2010-05-24 11:05 sum
$ ln -s sum total
$ rm sum
$ cat total
cat: total: No such file or directory
$ ls -l total
lrwxrwxrwx 1 max pubs 6 2010-05-24 11:09 total -> sum
```

When you remove a file, be sure to remove all symbolic links to it. Remove a symbolic link in the same way you remove other files:

```
$ rm total
```

# CHAPTER SUMMARY

Linux has a hierarchical, or tree-like, file structure that makes it possible to organize files so you can find them quickly and easily. The file structure contains directory files and ordinary files. Directories contain other files, including other directories; ordinary files generally contain text, programs, or images. The ancestor of all files is the root directory and is represented by / (standing alone or at the left end of a pathname.
