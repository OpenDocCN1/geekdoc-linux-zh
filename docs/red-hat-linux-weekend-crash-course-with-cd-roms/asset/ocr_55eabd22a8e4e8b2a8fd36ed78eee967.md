The du command displays the disk space used by each directory and the last line shows the total disk space used by that directory. If you want to see only the total space used by a directory, type the -s option like this:

```
du -sh /home
16M      /home
```

# Exploring the /proc File System

You can find out a great deal about your Red Hat Linux system by consulting the contents of a special file system known as the /proc (also called the process file system) file system. It can help you monitor a wide variety of information about your system. In fact, you can even change kernel parameters through the /proc file system and thereby modify the system’s behavior.

The /proc file system is not a real directory on the disk, but a collection of data structures in memory (managed by the Linux kernel) that appears to the user as a set of directories and files.

You can access the /proc file system and navigate it just as you do any other directory, but you have to know the meaning of various files to interpret the information. Typically, you can use the cat or more command to view the contents of a file in /proc; the file’s contents provide information about some aspect of the system.

As with any directory, you may want to start by looking at a detailed directory listing of /proc. To do so, type ls -l /proc. In the output, the first set of directories (indicated by the letter d at the beginning of the line) represents the processes that are currently running on your system. Each directory that corresponds to a process has the process ID (a number) as its name.

![](bbox=[0.07, 0.71, 0.2, 0.78])

You should also notice a very large file in the listing named /proc/kcore; that file represents the entire physical memory of your system. There is no physical file occupying that much space on your hard disk, so do not try to remove the file to reclaim disk space.

The /proc/cpuinfo file in /proc lists the key characteristics of your system, such as processor type and floating-point processor information. You can view the