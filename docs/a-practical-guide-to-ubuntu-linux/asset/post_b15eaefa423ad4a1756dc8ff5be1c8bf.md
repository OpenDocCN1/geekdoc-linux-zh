
[content]
# HARD LINKS

A hard link to a file appears as another file. If the file appears in the same directory as the linked-to file, the links must have different filenames because two files in the same directory cannot have the same name. You can create a hard link to a file only from the filesystem that holds the file.

In: Creates a Hard Link

The ln utility (without the -s or --symbolic option) creates a hard link to an existing file using the following syntax:

```
ln existing-file new-link
```

The next command shows Zach making the link shown in Figure 6-14 by creating a new link named /home/max/letter to an existing file named draft in Zach's home directory:

```
$ pwd
/home/zach
$ ln draft /home/max/letter
```

The new link appears in the /home/max/ directory with the filename letter. In practice, Max may need to change directory permissions so Zach will be able to create the link. Even though /home/max/letter appears in Max's directory, Zach is the owner of the file he created it.

The ln creates an additional pointer to an existing file but it does not make another copy of the file. Because there is only one file, the file status information—such as access permissions, owner, and the time the file was last modified—is the same for all links; only the filenames differ. When Zach modifies /home/zach/draft, for example, Max sees the changes in /home/max/letter.

![](img/45ff4cd21497435daa35084a84b95d07_278_0.png)

Figure 6-14 Two links to the same file: /home/max/letter and /home/zach/draft

# cp VERSUS ln

The following commands verify that ln does not make an additional copy of a file. Create a file, use ln to make an additional link to the file, change the contents of the file through one link, and verify the change through the other link:

```
$ cat file_a
This is file A.
$ ln file_a file_b
$ cat file_b
This is file A.
$ vim.tiny file_b
..
$ cat file_b
This is file B after the change.
$ cat file_a
This is file B after the change.
```

If you try the same experiment using cp instead of ln and change a copy of the file, the difference between the two utilities will be clearer. Once you change a copy of a file, the two files are different:

```
$ cat file_c
This is file C.
$ cp file_c file_d
$ cat file_d
This is file C.
$ vim.tiny file_d
..
$ cat file_d
This is file D after the change.
$ cat file_c
This is file C.
```

ls and link counts

You use ls with the -l option, followed by the names of the files you want to compare, find that the status information is the same for two links to the same file and is different for files that are not linked. In the example, the 2 in the links field (just to the left of max) shows there are two links to file_a and file_b (from the previous example):

```
$ ls -l file_a file_b file_c file_d
r-r--r---- 2 max pubs 33 2010-05-24 10:52 file_a
r-r--r---- 2 max pubs 33 2010-05-24 10:52 file_b
r-r--r---- 1 max pubs 16 2010-05-24 10:55 file_c
r-r--r---- 1 max pubs 33 2010-05-24 10:57 file_d
```

Although it is easy to guess which files are linked to another, ls -i does not explicitly tell you. Use ls with the -i option to determine without doubt which files are linked. The -i option lists the inode for each file. If two filenames have the same inode number, they share the same control structure and are links to the same file. Conversely, when two filenames have different inode numbers, they are different files. The following example shows that file_a and file_b have the same inode number and file_c and file_d have different inode numbers:

```
$ ls -i file_a file_b file_c file_d
3534 file_a 3534 file_b 5800 file_c 7328 file_d
```

All links to a file are of value: the operating system cannot distinguish the order in which links were created. When a file has two links, you can remove either and still access the file through the remaining link. You can remove the link used to create the file, for example, as long as one link remains, still access the file through that link.

# SYMBOLIC LINKS

In addition to hard links, Linux supports symbolic links, also called soft links or symlinks. A hard link is a pointer to a file (the directory entry points to the inode), whereas a symbolic link is an indirect pointer to a file (the directory entry contains the pathname of the file).

Symbolic links were developed because of the limitations in hard links. You cannot create a hard link to a directory, but you can create a symbolic link to a directory. In many cases the Linux file hierarchy encompasses several systems. Because each filesystem separates control information (that is, separate inode tables) for the files it holds, it is not possible to create hard links between systems. A symbolic link can point to any file, regardless of where it is located in the file structure. When you create links among files in your home directory, you will not notice this.

A major advantage of a symbolic link is that it can point to a nonexistent file. This ability is useful if you need to link to a file that is periodically removed and recreated. A hard link keeps to a “removed” file, which the links keep after a new file is created. In contrast, a symbolic link points to the newly created file and does not interfere when you delete the file. For example, a symbolic link could point to a source file that gets checked in or out, a .o file that is rebuilt each time you make, or a log file that is repeatedly appended.

Although they are more general than hard links, symbolic links have some disadvantages. Whereas all hard links to a file have equal status, symbolic links do not have the same status as hard links. When a file has multiple hard links, it is analogous to a person having full legal names. In contrast, symbolic links are analogous to nicknames. Anyone can have one or more nicknames, but these nicknames have a lesser status than legal names. The following sections describe some of the peculiarities of symbolic links.

In: CREATES SYMBOLIC LINKS

The utility with the --symbolic (or -s) option creates a symbolic link. The following example creates a symbolic link /tmp/s3 to the file in Max’s home directory. When you use an -l command to look at the symbolic link, ls displays the name of the link and the name of the file it points to. The first character of the listing is l (for link).

```
$ ln --symbolic /home/max/sum /tmp/s3
$ ls -l /home/max/sum /tmp/s3
-rw-rw-r-- 1 max 38 2010-06-12 09:51 /home/max/sum
lrwxr-xr-x 1 max 14 2010-06-12 09:52 / -> /home/max/sum
$ cat /tmp/s3
```

This is sum.

The sizes and times of the last modifications of the two files are different. Unlike a hard link, a symbolic link to a file does not have the same status information as the file itself. You can also use ln to create a symbolic link to a directory. When you use the --symbolic option, in facts works as expected whether the file you are creating a link to an ordinary file or a directory.

# Use absolute pathnames with symbolic links

- Symbolic links are literal and are not aware of directories. A link that points to a relative pathname, which includes simple filenames, assumes the pathname is relative to the directory that the link was created in (the directory it was created from). In the following example, the link points to the file named sum in the /tmp directory. Because no such file exists, cat gives an error message:

```
$ pwd
/home/max
$ ln --symbolic sum /tmp/s4
$ ls -l sum /tmp/s4
lrwxr-xr-x 1 max 38 2010-06-12 10:13 /tmp/s4 - sum
-rw-rw-r-- 1 max 38 2010-06-12 09:51 sum
$ cat /tmp/s4
```
cat:/tmp/s4: No file or directory

# cd AND SYMBOLIC LINKS

When you use a symbolic link as an argument to cd to change directories, the results can be confusing, particularly if you did not realize that you were using a symbolic link.

If you use cd to change to a directory that is represented by a symbolic link, the shell builtin (page 261) lists the name of the symbolic link. The pwd utility (/bin/pwd) lists the name of the linked-directory, not the link, regardless of how you got there.

```
$ ln -s /home/max/grades /tmp/grades.old
$ pwd
/home/max
$ cd ~/grades.old
$ pwd
/tmp/grades.old
$ /bin/pwd
/home/max/grades
```
