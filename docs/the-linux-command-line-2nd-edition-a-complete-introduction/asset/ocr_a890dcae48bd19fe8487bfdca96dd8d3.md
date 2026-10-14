```
```bash
[me@linuxbox ~]$ ls -l /etc > foo.txt
[me@linuxbox ~]$ ls -l foo.txt
-rw-r--r-- 1 me me 15738 2008-10-17 13:51 foo.txt
[me@linuxbox ~]$ bzip2 foo.txt
[me@linuxbox ~]$ ls -l foo.txt.bz2
-rw-r--r-- 1 me me 2792 2008-10-17 13:51 foo.txt.bz2
[me@linuxbox ~]$ bunzip2 foo.txt.bz2
```
```

As we can see, bzip2 can be used the same way as gzip. All the options (except for -r) that we discussed for gzip are also supported in bzip2. Note, however, that the compression level option (-number) has a somewhat different meaning to bzip2. bzip2 comes with bunzip2 and bzcat for decompressing files.

bzip2 also comes with the bzip2recover program, which will try to recover damaged .bz2 files.

> ### Don’t Be Compressive Compulsive
> 
> I occasionally see people attempting to compress a file, that has already been compressed with an effective compression algorithm, by doing something like this:
> 
> ```bash
> $ gzip picture.jpg
> ```
> 
> Don’t do it. You’re probably just wasting time and space! If you apply compression to a file that is already compressed, you will actually end up with a larger file. This is because all compression techniques involve some overhead that is added to the file to describe the compression. If you try to compress a file that already contains no redundant information, the compression will not result in any savings to offset the additional overhead.

# Archiving Files

A common file-management task often used in conjunction with compression is archiving. Archiving is the process of gathering up many files and bundling them together into a single large file. Archiving is often done as a part of system backups. It is also used when old data is moved from a system to some type of long-term storage.

# tar

In the Unix-like world of software, the tar program is the classic tool for archiving files. Its name, short for tape archive, reveals its roots as a tool for making backup tapes. While it is still used for that traditional task, it is equally adept on other storage devices as well.