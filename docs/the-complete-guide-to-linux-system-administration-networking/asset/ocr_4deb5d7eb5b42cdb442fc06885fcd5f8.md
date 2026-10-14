The number in the second column from the left (in this case, 1) indicates the number of file records that refer to the same inode as this file record.

The zcat file name (also in Red Hat Linux) is an example of a hard link. The zcat file record refers to an inode to which two other file records also refer. The ls -l command again shows this:

```
$ ls -l /bin/zcat
-rwx-r-xr-x  3 root root  63555 Mar 25 13:28 /bin/zcat
```

In this sample screen output, the number 3 in the second column from the left indicates that the file record holding the file name zcat refers to an inode to which two other file records also refer (for a total of three).

Figure 4-6 illustrates the difference between a symbolic link and a hard link. In this figure, a programming language named Perl is stored in a file called perl5.6.1, where the 5.6.1 indicates a precise version number. Other file records also point to the same information (inode) using different file names. This allows users who might not know the precise version number to access the perl programming language file.

![](bbox=[0.15, 0.58, 0.88, 0.85])

Figure 4-6 Comparing hard and symbolic links

# File Types

Most of the files you have worked with so far have been standard data files, but you have also been introduced to other types of files, such as symbolic links. Because nearly everything in Linux is accessed using the file system, different types of files are used to perform different functions. Table 4-3 lists the seven types of files used by Linux. Several of these are used mainly by programs—you will not encounter them in your work at the command line and they are not discussed in more detail in this book.