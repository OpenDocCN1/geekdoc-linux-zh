# ## LINKING FILES

If you want to make a hard link to file1 called file2, as in Figure 5-1, you can issue the command `ln file1 file2` at the command prompt; a file called file2 is created and hard-linked to file1. To view the hard-linked filenames after creation, you can use the `ls -l` command:

```
[root@server1 root]# ln file1 file2
[root@server1 root]# ls -l
total 1032
drw-------   3 root root  4096 Apr 8 07:12 Desktop
-rw-r--r-x   2 root root 519964 Apr 7 09:59 file1
-rw-r--r-x   2 root root 519964 Apr 7 09:59 file2
-rw-r--r-x   1 root root  1244 Apr 27 18:17 file3 [root@server1 root]# _
```

Notice from the preceding long listing that file1 and file2 share the same inode, as they have the same size, permissions, ownership, modification date, and so on. Also note that the link count (the number after the permission set) for file1 has increased from the number one to the number two in the preceding output. A link count of one indicates that only one inode is shared by the file. A file that is hard-linked to another file shares two inodes and, thus, has a link count of two. Similarly, a file that is hard-linked to three other files shares four inodes and, thus, has a link count of four.

Although hard links share the same inode, deleting a hard linked file does not delete all the other hard linked files. Removing a hard link can be achieved by removing one of the files, which then lowers the link count.

To view the inode number of hard-linked files to verify that they are identical, you can use the -i option to the ls command in addition to any other options. The inode number is placed on the left of the directory listing on each line, as shown in the following output:

```
[root@server1 root]# ls -li
total 1032
37595 drw-------   3 root root  4096 Apr 8 07:12 Desktop
 1204 -rw-r--r-x   2 root root 519964 Apr 7 09:59 file1
 1204 -rw-r--r-x   2 root root 519964 Apr 7 09:59 file2
17440 -rw-r--r-x   1 root root  1244 Apr 27 18:17 file3 [root@server1 root]# _
```

![](bbox=[0.15, 0.72, 0.22, 0.77])

# **NOTE**

Directory files are not normally hard-linked, as the result would consist of two directories that contain the same contents. However, the root user has the ability to hard-link directories in some cases, using the -f or -d option to the ln command. Only directories that have files regularly added and need to maintain identical file contents are typically hard-linked.