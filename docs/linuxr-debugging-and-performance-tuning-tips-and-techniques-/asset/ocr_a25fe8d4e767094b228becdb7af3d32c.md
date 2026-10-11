really uses, shows that the file uses only 16 blocks. ${ }^{3}$ The missing blocks in the file are the holes. This is illustrated in Figure 4.2.

![](bbox=[0.1, 0.17, 0.9, 0.31])

# FIGURE 4.2
Holes in a file

> NOTE ch04-holes.c does direct binary I/O. This nicely illustrates the beauty of random access I/O: You can treat a disk file as if it were a very large array of binary data structures.
> 
> In practice, storing live data by using binary I/O is a design decision that you should consider carefully. For example, suppose you need to move the data to a system using different byte orders for integers? Or different floating-point formats? Or to a system with different alignment requirements? Ignoring such issues can become significantly costly.

# 4.6 Creating Files

As described earlier, `open()` apparently opens existing files only. This section describes how brand-new files are created. There are two choices: `creat()` and `open()` with additional flags. Initially, `creat()` was the only way to create a file, but `open()` was later enhanced with this functionality as well. Both mechanisms require specification of the initial file permissions.

# 4.6.1 Specifying Initial File Permissions

As a GNU/Linux user, you are familiar with file permissions as printed by `^\ls -l`: read, write, and execute for each of user (the file's owner), group, and other. The various

${ }^{3}$ At least three of these blocks contain the data that we wrote out; the others are for use by the operating system in keeping track of where the data reside.