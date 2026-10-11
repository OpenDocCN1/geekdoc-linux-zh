On GNU/Linux, `remove()` uses the `unlink()` system call to remove files, and the `rmdir()` system call (discussed later in the chapter) to remove directories. (On older GNU/Linux systems not using glibc, `remove()` is an alias for `unlink()`; this fails on directories. If you have such a system, you should probably upgrade it.)

# 5.1.6  Symbolic Links

We started the chapter with a discussion of partitions, file systems, and inodes. We also saw that directory entries associate names with inode numbers. Because directory entries contain no other information, hard links are restricted to files within the same *file system*. This has to be; there is no way to distinguish inode 2341 on one file system from inode 2341 on another file system. Here is what happens when we try:

```
$ mount                                   *Show file systems in use*  
/dev/hda2 on / type ext3 (rw)  
/dev/hda5 on /d type ext3 (rw)  
...  
$ ls -11 /tmp/message                   *Earlier example was on file system for /d*  
228708 -rw-r--r-- 2 arnold  devel  19 May  4 15:51 /tmp/message  
$ cat /tmp/message  
Hi, how ya doin' ?  
$ ls /bin/pwd                            *Current directory is on a different file system*  
/d/home/arnold  
$ ln /tmp/message .  
Attempt the link  
ln: creating hard link `./message' to `/tmp/message': Invalid cross-device link
```

Large systems often have many partitions, both on physically attached local disks and on remotely mounted network file systems. The hard-link restriction to the same file system is inconvenient, for example, if some files or directories must be moved to a new location, but old software uses a hard-coded filename for the old location.

To get around this restriction, 4.2 BSD introduced *symbolic links*. A symbolic link (also referred to as a *soft link*) is a special kind of file (just as a directory is a special kind of file). The contents of the file are the *pathname* of the file being “pointed to.” All modern Unix systems, including Linux, provide symbolic links; indeed they are now part of POSIX.

Symbolic links may refer to any file anywhere on the system. They may also refer to directories. This makes it easy to move directories from place to place, with a symbolic link left behind in the original location pointing to the new location.