# 8.6.3 Soft/Symbolic Links

Soft/symbolic links take care of all the problems inherent in hard links and are therefore used more often than hard links. They are different from hard links both conceptually and in terms of how they are implemented. They do have a cost associated with them, which we discuss in Section 8.6.4, but they are extremely flexible and can be used to link files across machines and networks.

You can create soft links by using the ln command with the -s option. The following session illustrates the creation of a soft link.

```
$ ls -il
total 2
13059 -rw-r--r-- 1 sarwar faculty 398 Mar 11 14:20 Chapter1
17488 -rw-r--r-- 1 sarwar faculty 5983 Jan 17 11:57 Chapter2
52473 -rw-r--r-- 2 sarwar faculty 9352 May 28 23:09 Chapter3
52473 -rw-r--r-- 2 sarwar faculty 9352 May 28 23:09 Chapter3.hard
$ ln -s Chapter3 Chapter3.soft
$ ls -il
total 2
13059 -rw-r--r-- 1 sarwar faculty 398 Mar 11 14:20 Chapter1
17488 -rw-r--r-- 1 sarwar faculty 5983 Jan 17 11:57 Chapter2
52473 -rw-r--r-- 2 sarwar faculty 9352 May 28 23:09 Chapter3
52473 -rw-r--r-- 2 sarwar faculty 9352 May 28 23:09 Chapter3.hard
52479 lrwxr-xr-x 1 sarwar faculty 8 Aug 23 13:57 Chapter3.soft
-> Chapter3
$
```

The ln -s Chapter3 Chapter3.soft command is used to create a symbolic link to the file Chapter3 in the present working directory, and the symbolic link is given the name Chapter3.soft. The output of the ls -il command shows a number of important items that reveal how symbolic links are implemented and how they are identified in the output. First, the original file (Chapter3) and the link file (Chapter3.soft) have different inode numbers: 52473 for Chapter3 and 52479 for Chapter3.soft, which means that they are different files. Second, the original file (Chapter3) is of file type - (ordinary) and the link file (Chapter3.soft) is of type l (link). Third, the value link count has not changed for Chapter3 (and Chapter3.hard) and is 1 for Chapter3.soft, which further indicates that the two files are different. Fourth, the file sizes are different: 9352 bytes for the original file (Chapter3) and 8 bytes file the link file (Chapter3.soft). Last, the name of the link file followed by -> Chapter3, the pathname for the file that Chapter3.soft is a symbolic link to; the string after the -> sign is specified as the first argument in the ln -s command. The pathname of the existing file is the content of the link file, which also explains the size of the link file (8 characters in the word Chapter3). Figure 8.5 shows the logical file structure of the current directory, directory entries in the current directory, and a diagram that shows that Chapter3 and Chapter3.soft are truly separate files and that the link file contains the pathname of the file to which it is a link.