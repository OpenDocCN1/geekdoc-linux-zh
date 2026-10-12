Here's a typical output of that command:

```
152K   /var/log/cups
4.0K   /var/log/vbox
4.0K   /var/log/httppd
508K   /var/log/gdm
4.0K   /var/log/samba
8.0K   /var/log/mail
4.0K   /var/log/news/OLD
8.0K   /var/log/news
4.0K   /var/log/squid
2.2M   /var/log
```

The du command displays the disk space used by each directory and the last line shows the total disk space used by that directory. If you want to see only the total space used by a directory, use the -s option, like this:

```
du -sh /home
89M    /home
```

# ## Viewing System Information via the /proc File System

Your Fedora Core system has a special file system called the /proc file system. You can find out many things about your system from this file system. In fact, you can even change kernel parameters through the /proc file system (just by writing to a file in that file system), thereby modifying the system's behavior.

The /proc file system isn't a real directory on the disk but a collection of data structures in memory, managed by the Linux kernel, that appears to you as a set of directories and files. The purpose of /proc (also called the process file system) is to give you access to information about the Linux kernel as well as to help you find out about all processes currently running on your system.

You can access the /proc file system just as you access any other directory, but you have to know the meaning of various files to interpret the information. Typically, you can use the cat or more commands to view the contents of a file in /proc; the file's contents provide information about some aspect of the system.

As with any directory, start by looking at a detailed directory listing of /proc. To do so, log in as root and type ls -1 /proc in a terminal window. In the output, the first set of directories (indicated by the letter d at the beginning of the line) represents the processes currently running on your system. Each directory that corresponds to a process has the process ID (a number) as its name.