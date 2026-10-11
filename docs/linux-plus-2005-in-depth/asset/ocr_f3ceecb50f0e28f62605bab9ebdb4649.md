# **NOTE**

Each file and directory must have an inode. All files except for special device files also have data blocks associated with the inode. Special device files are discussed in Chapter 6, "Linux Filesystem Administration."

Directories are simply files that are used to organize other files; they too have an inode and data blocks, but their data blocks contain a list of filenames that are located within the directory.

Hard-linked files are direct copies of one another, as they share the same inode and inode number. All hard linked files have the same size, and when one file is modified, the other hard linked files are updated as well. This relationship between hard linked files can be seen in Figure 5-1. You can hard-link a file an unlimited number of times; however, the hard linked files must reside on the same filesystem. This is because inode numbers are unique only on the same filesystem and hard links are recognized by ignoring this rule.

![](bbox=[0.15, 0.47, 0.85, 0.74])

**FIGURE 5-1** *The structure of hard-linked files*

To create a hard link, you must use the **ln (link) command** and specify two arguments: the existing file to hard link and the target file that will be created as a hard link to the existing file. Each argument can be the absolute or relative pathname to a file. Take, for example, the following contents of the root user's home directory:

```
```bash
[root@server1 root]$ ls -l
total 520
drwx------ 3 root root 4096 Apr 8 07:12 Desktop
-rw-r--xr-x 1 root root 519964 Apr 7 09:59 file1
-rw-rxr-x 1 root root 1244 Apr 27 18:17 file3
```
```