After using cd to make **promo** (a subdirectory of **literature**) his working directory, Alex can use a relative pathname to call **vim** to edit a file in his home directory.

```
$ cd promo
$ vim ../.names
```

You can use an absolute or relative pathname or a simple filename virtually any-where that a utility or program requires a filename or pathname. This usage holds true for ls, vim, mkdir, rm, and most other Linux utilities.

# Important Standard Directories and Files

Originally files on a Linux system were not located in standard places. The scatted files made it difficult to document and maintain a Linux system and just about impossible for someone to release a software package that would compile and run on all Linux systems. The first standard for the Linux filesystem, the FSSTND (Linux Filesystem Standard), was released on February 14, 1994. In early 1995 work was started on a broader standard covering many UNIX-like systems: FHS (Linux Filesystem Hierarchy Standard, www.pathname.com/fhs). More recently FHS has been incorporated in LSB (Linux Standard Base, www.linuxbase.org), a workgroup of FSG (Free Standards Group, www.freestandards.org). Figure 6-10 shows the locations of some important directories and files as specified by FHS. The significance of many of these directories will become clear as you continue reading.

The following list describes the directories shown in Figure 6-10, some of the directories specified by FHS, and some other directories. Fedora/RHEL, however, does not use all the directories specified by FHS. Be aware that you cannot always determine the function of a directory by its name. For example, although /opt stores add-on software, /etc/opt stores configuration files for the software in /opt. See also “Important Files and Directories” on page 468.

/ Root The root directory, present in all Linux filesystem structures, is the ancestor of all files in the filesystem.

/bin Essential command binaries Holds the files needed to bring the system up and run it when it first comes up in single-user mode (page 430).

/boot Static files of the boot loader Contains all of the files needed to boot the system.

![](bbox=[0.15, 0.68, 0.85, 0.92])