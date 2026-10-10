# **Linking Files**

![](bbox=[0.26, 0.09, 0.81, 0.2])

# **Figure 4-1**  The structure of hard-linked files

hard-linked files can be seen in Figure 4-1. You can hard-link a file an unlimited number of times; however, the hard-linked files must reside on the same filesystem.

To create a hard link, you must use the **ln (link)** command and specify two arguments: the existing file to hard-link and the target file that will be created as a hard link to the existing file. Each argument can be the absolute or relative pathname to a file. Take, for example, the following contents of the root user's home directory:

```
[root@server1 ~]# ls -l
total 520
drwx------ 3 root root 4096 Apr 8 07:12 Desktop
-rw-r--r-x 1 root root 519964 Apr 7 09:59 file1
-rw-r--xr-x 1 root root 1244 Apr 27 18:17 file3
[root@server1 ~]# _
```

Suppose you want to make a hard link to file1 and call the new hard link file2, as shown in Figure 4-1. To accomplish this, you issue the command **ln file1 file2** at the command prompt; a file called file2 is created and hard-linked to file1. To view the hard-linked filenames after creation, you can use the ls -1 command:

```
[root@server1 ~]# ln file1 file2
[root@server1 ~]# ls -l
total 1032
drwx------ 3 root root 4096 Apr 8 07:12 Desktop
-rw-r--r-x 1 root root 519964 Apr 7 09:59 file1
-rw-r--xr-x 2 root root 519964 Apr 7 09:59 file2
-rw-r--xr-x 1 root root 1244 Apr 27 18:17 file3
[root@server1 ~]# _
```

Notice from the preceding long listing that file1 and file2 share the same inode and data section, as they have the same size, permissions, ownership, modification date, and so on. Also note that the link count (the number after the permission set) for file1 has increased from the number one to the number two in the preceding output. A link count of one indicates that only one inode is shared by the file. A file that is hard-linked to another file shares two inodes and, thus, has a link count of two. Similarly, a file that is hard-linked to three other files shares four inodes and, thus, has a link count of four.

Although hard links share the same inode and data section, deleting a hard-linked file does not delete all the other hard-linked files; it simply removes one filename reference. Removing a hard link can be achieved by removing one of the files, which then lowers the link count.

To view the inode number of hard-linked files to verify that they are identical, you can use the -i option to the ls command in addition to any other options. The inode number is placed on the left of the directory listing on each line, as shown in the following output: