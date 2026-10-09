
the group that the file is associated with have read and write permissions for the file. The effective rights mask is set to read and write so that the effective permission for **pubs** is read and the effective permissions for **adm** are read and write. Neither group has execute permission.

```text
$ cd dir
$ touch new
$ ls -1 new
-rw-rw----+ 1 max pubs 0 02-13 00:39 new
$ getfacl --omit new
user::rw-
group::---
group:pubs:r-x #effective:r-
group:adm:rwx #effective:rw-
mask::rw-
other::---
```

If you change the file’s traditional permissions to read, write, and execute for the owner and the group, the effective rights mask changes to read, write, and execute, and the groups specified by the default rules gain execute access to the file.

```text
$ chmod 770 new
$ ls -1 new
-rwxrwx---+ 1 max pubs 0 02-13 00:39 new
$ getfacl --omit new
user::rwx
group::---
group:pubs:r-x
group:adm:rwx
mask::rwx
other::---
```

## LINKS

A *link* is a pointer to a file. Each time you create a file using vim, touch, cp, or some other means, you are putting a pointer in a directory. This pointer associates a filename with a place on the disk. When you specify a filename in a command, you are indirectly pointing to the place on the disk that holds the information you want.

Sharing files can be useful when two or more people are working on the same project and need to share some information. You can make it easy for other users to access one of your files by creating additional links to the file.

To share a file with another user, first give the user permission to read from and write to the file (page 193). You might also have to change the access permissions of the parent directory of the file to give the user read, write, or execute permission (page 197). When the permissions are appropriately set, the user can create a link to the file so each of you can access the file from your separate directory hierarchies.

A link can also be useful to a single user with a large directory hierarchy. You can create links to cross-classify files in your directory hierarchy, using different classifications for different tasks. For example, if you have the file layout depicted in Figure 6-2 on page 177, a file named **to_do** might appear in each subdirectory of the **correspond** directory—that is, in **personal**, **memos**, and **busines**. If you find it difficult to keep track of everything you need to do, you can create a separate directory named **to_do** in the **correspond** directory. You can then link each subdirectory’s to-do list into that directory. For example, you could link the file named **to_do** in the **memos** directory to a file named **memos** in the **to_do** directory. This set of links is shown in Figure 6-10. Although it might sound complicated, this technique keeps all your to-do lists conveniently in one place. The appropriate list is easily accessible in the task-related directory when you are busy composing letters, writing memos, or handling personal business.

![](img/243613168ac865b539f12460d966088e_260_0.png)

Figure 6-10 Using links to cross-classify files

### About the discussion of hard links

> tip Two kinds of links exist: hard links and symbolic (soft) links. Hard links are older and becoming outdated. The section on hard links is marked as optional; you can skip it, although it discusses inodes and gives you insight into the structure of the filesystem.

### optional

#### LE HARD LINKS

A hard link to a file appears as another file. If the file appears in the same directory as the linked-to file, the links must have different filenames because two files in the same directory cannot have the same name. You can create a hard link to a file only from within the filesystem that holds the file.

#### LPI ln: CREATES A HARD LINK

The **ln** (link) utility (without the **-s** or **--symbolic** option) creates a hard link to an existing file using the following syntax:

```
ln existing-file new-link
```

![](img/243613168ac865b539f12460d966088e_261_0.png)

Figure 6-11  Two links to the same file: /home/max/letter and /home/zach/draft

The next command shows Zach making the link shown in Figure 6-11 by creating a new link named /home/max/letter to an existing file named draft in Zach’s home directory:

```
$ pwd  
/home/zach  
$ ln draft /home/max/letter
```

The new link appears in the /home/max directory with the filename letter. In practice, Max might need to change directory permissions so Zach will be able to create the link. Even though /home/max/letter appears in Max’s directory, Zach is the owner of the file because he created it.

The ln utility creates an additional pointer to an existing file, but it does not make another copy of the file. Because there is only one file, the file status information—such as access permissions, owner, and the time the file was last modified—is the same for all links; only the filenames differ. When Zach modifies /home/zach/draft, for example, Max sees the changes in /home/max/letter.

#### cp VERSUS ln

The following commands verify that ln does not make an additional copy of a file. Create a file, use ln to make an additional link to the file, change the contents of the file through one link, and verify the change through the other link:

```
$ cat file_a  
This is file A.  
$ ln file_a file_b  
$ cat file_b  
This is file A.  
$ vim file_b  
…  
$ cat file_b  
This is file B after the change.  
$ cat file_a  
This is file B after the change.
```

If you try the same experiment using `cp` instead of `ln` and change a copy of the file, the difference between the two utilities will become clearer. After you change a copy of a file, the two files are different:

```
$ cat file_c
This is file C.
$ cp file_c file_d
$ cat file_d
This is file C.
$ vim file_d
...
$ cat file_d
This is file D after the change.
$ cat file_c
This is file C.
```

#### lpa ls and link counts

You can use `ls` with the -l option, followed by the names of the files you want to compare, to confirm that the status information is the same for two links to the same file and is different for files that are not linked. In the following example, the 2 in the links field (just to the left of `max`) shows there are two links to `file_a` and `file_b` (from the previous example):

```
$ ls -l file_a file_b file_c file_d
-rw-r--r--. 2 max pubs 33 05-24 10:52 file_a
-rw-r--r--. 2 max pubs 33 05-24 10:52 file_b
-rw-r--r--. 1 max pubs 16 05-24 10:55 file_c
-rw-r--r--. 1 max pubs 33 05-24 10:57 file_d
```

Although it is easy to guess which files are linked to one another in this example, `ls` does not explicitly tell you.

#### lpi ls and inodes

Use `ls` with the -i option to determine without a doubt which files are linked. The -i option lists the inode (page 1254) number for each file. An inode is the control structure for a file. If the two filenames have the same inode number, they share the same control structure and are links to the same file. Conversely, when two filenames have different inode numbers, they are different files. The following example shows that `file_a` and `file_b` have the same inode number and that `file_c` and `file_d` have different inode numbers:

```
$ ls -i file_a file_b file_c file_d
3534 file_a 3534 file_b 5800 file_c 7328 file_d
```

All links to a file are of equal value. The operating system cannot distinguish the order in which multiple links were created. When a file has two links, you can remove either one and still access the file through the remaining link. You can remove the link used to create the file, for example, and as long as one link remains, still access the file through that link.

### SYMBOLIC LINKS

In addition to hard links, Linux supports symbolic links, also called soft links or symlinks. A hard link is a pointer to a file (the directory entry points to the inode), whereas a symbolic link is an *indirect* pointer to a file (the directory entry contains the pathname of the pointed-to file—a pointer to the hard link to the file).

#### Advantages of symbolic links

Symbolic links were developed because of the limitations inherent in hard links. You cannot create a hard link to a directory, but you can create a symbolic link to a directory.

In many cases the Linux file hierarchy encompasses several filesystems. Because each filesystem keeps separate control information (i.e., separate inode tables or filesystem structures) for the files it holds, it is not possible to create hard links between files in different filesystems. A symbolic link can point to any file, regardless of where it is located in the file structure, but a hard link to a file must be in the same filesystem as the other hard link(s) to the file. When you create links only among files in your home directory, you will not notice this limitation.

A major advantage of a symbolic link is that it can point to a nonexistent file. This ability is useful if you need a link to a file that is periodically removed and re-created. A hard link keeps pointing to a “removed” file, which the link keeps alive even after a new file is created. In contrast, a symbolic link always points to the newly created file and does not interfere when you delete the old file. For example, a symbolic link could point to a file that gets checked in and out under a source code control system, a .o file that is re-created by the C compiler each time you run **make**, or a log file that is repeatedly archived.

Although they are more general than hard links, symbolic links have some disadvantages. Whereas all hard links to a file have equal status, symbolic links do not have the same status as hard links. When a file has multiple hard links, it is analogous to a person having multiple full legal names, as many married women do. In contrast, symbolic links are analogous to nicknames. Anyone can have one or more nicknames, but these nicknames have a lesser status than legal names. The following sections describe some of the peculiarities of symbolic links.

#### ln: Creates Symbolic Links

The **ln** utility with the **--symbolic** (or **-s**) option creates a symbolic link. The following example creates a symbolic link /tmp/s3 to the file **sum** in Max's home directory. When you use the **ls** command to look at the symbolic link, **ls** displays the name of the link and the name of the file it points to. The first character of the listing is **l** (for link).

```
$ ln --symbolic /home/max/sum /tmp/s3
$ ls -l /home/max/sum /tmp/s3
-rw-rw-r--. 1 max pubs 38 06-12 09:51 /home/max/sum
lrwxrwxrwx. 1 max pubs 14 06-12 09:52 /tmp/s3 -> /home/max/sum
$ cat /tmp/s3
This is sum.
```

The sizes and times of the last modifications of the two files are different. Unlike a hard link, a symbolic link to a file does not have the same status information as the file itself.
