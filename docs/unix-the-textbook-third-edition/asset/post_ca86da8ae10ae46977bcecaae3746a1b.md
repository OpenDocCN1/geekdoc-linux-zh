
The directory entry for the file, releases the file's inode and all other kernel resources allocated to the file so they can be reused, and deallocates disk blocks allocated to the file so that they can be used to store other files and/or directories created in the future.

If the new link count is not 0, only the directory entry for the removed file is deleted; the file contents and other directory entries for the file (hard links) remain intact. The following session illustrates this point.

```
$ rm Chapter3
$ ls -il
13059 -rwx------ 1 sarwar faculty 398 Mar 11 14:20 Chapter1
17488 -rwx------ 1 sarwar faculty 5983 Apr 17 11:57 Chapter2
52473 -rwx------ 1 sarwar faculty 9352 Aug 20 23:09 Chapter3.hard
$
```

This session clearly shows that removing Chapter3 results in the removal of the directory entry for this file but that the file still exists on disk and is accessible via Chapter3.hard. This link has the inode number and file attributes that Chapter3 had, except that the link count, as expected, has been decremented from 2 to 1.

The following ln command can be used to create a hard link called memo6.hard in the present working directory to a file ~/memos/memo6. The ls -il command is used to view attributes of the file before the hard link to it is created.

```
$ ls -il ~/memos/memo6
83476 -rwx------ 1 sarwar faculty 1673 May 29 11:22 /home/sarwar/memos/memo6
$ ln ~/memos/memo6 memo6.hard
$
```

After executing the ln command, you can run the ls -il command to confirm that both files (~/memos/memo6 and memo6.hard) have the same inode number and attributes, as shown in the following session.

```
$ ls -il ~/memos/memo6
83476 -rwx------ 2 sarwar faculty 1673 May 29 11:22 /home/sarwar/memos/memo6
$ ls -il memo6.hard
83476 -rwx------ 2 sarwar faculty 1673 May 29 11:22 memo6.hard
$
```

The output shows two important things: first, the link count is up by 1; second, both files are represented by the same inode, 83476. Figure 8.3 shows the hard link pictorially.

### Contents of current directory

| Inode # | File |
|---|---|
| 1076 | . |
| 2083 | .. |
| 13059 | Chapter1 |
| 17488 | Chapter2 |
| 52473 | Chapter3 |
| 83476 | memo6.hard |

### Contents of ~/memos

| Inode # | File |
|---|---|
| 1076 | . |
| 2083 | .. |
| 83468 | memo01 |
| ... | ... |
| 83476 | memo6 |
| ... | ... |

![](img/02e070097d401d3bf7de4bf1c470b267_330_0.png)

FIGURE 8.3 Pictorial representation of the hard link between ~/memos/memo6 and memo6.hard in the current directory.

In the following session, the ln command creates hard links to all nondirectory files in the directory called ~/unixbook/examples/dir1. The hard links reside in the directory ~/unixbook/examples/dir2 and have the names of the original files in the dir1 directory. The second argument, dir2, must be an existing directory, and you must have execute and write permissions to it. Note that the link counts for all the files in dir1 and dir2 are 2. The -f option is used to force creation of a hard link in case any of the files f1, f2, or f3 already exist in the ~/unixbook/examples/dir2 directory.

```
$ cd unixbook/examples
$ more dir1/f1
Hello, World!
This is a test file.
$ ls -l dir1
-rw------ 1 sarwar faculty 35 Jun 22 22:21 f1
-rw------ 1 sarwar faculty 68 May 16 21:03 f2
-rw------ 1 sarwar faculty 94 Jul 11 11:39 f3
$ ln -f ~/unixbook/examples/dir1/* ~/unixbook/examples/dir2
$ ls -l dir1
-rw------ 2 sarwar faculty 35 Jun 22 22:21 f1
-rw------ 2 sarwar faculty 68 May 16 21:03 f2
-rw------ 2 sarwar faculty 94 Jul 11 11:39 f3
$ ls -l dir2
-rw------ 2 sarwar faculty 35 Jun 22 22:21 f1
-rw------ 2 sarwar faculty 68 May 16 21:03 f2
-rw------ 2 sarwar faculty 94 Jul 11 11:39 f3
$ more dir2/f1
Hello, World!
This is a test file.
$
```

You can run the following command to create a hard link in your home directory to the file /home/sarwar/unixbook/examples/demo1. The hard link appears as a file demo1 in your home directory. If demo1 already exists in your home directory, you can overwrite it with the -f option. If demo1 exists in the home directory and you don’t use the -f option, an error message is displayed on the screen informing you that the demo1 file exists. You must have the execute permission for the directories in the pathname /home/sarwar/unixbook/examples/demo1, and demo1 must be a file.

```
$ ln -f /home/sarwar/unixbook/examples/demo1 ~
$
```

The user sarwar can run the following command to create a hard link demo1 in a directory dir1 in bob's home directory that points to the file /home/sarwar/unixbook/examples/demo1. The name of the link in bob's directory is demo1, the same as the original file. Figure 8.4 shows the establishment of the link.

```
$ ln -f /home/sarwar/unixbook/examples/demo1 /home/bob/dir1
$
```

The user sarwar must have execute permission for bob's home directory and execute and write permissions for dir1 (the directory in which the link is created). The user bob must have proper access permissions for demo1 in sarwar's directory structure to access this file. Thus, if sarwar and bob are in the same user group and bob needs to edit demo1, sarwar must set the group access privileges for the file to read and write. Then, bob is able to edit demo1 by using, for example, the vim demo1 command from his home directory.

The following command accomplishes the same task. Remember that sarwar runs this command.

```
$ ln -f ~/unixbook/examples/demo1 /home/bob/dir1
$
```

You can run the following command to create hard links to all nondirectory files in your ~/unixbook/examples directory. The hard links reside in the unixbook/examples

![](img/02e070097d401d3bf7de4bf1c470b267_331_0.png)

FIGURE 8.4 A hard link between /home/sarwar/unixbook/examples and /home/bob/dir1.
