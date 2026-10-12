# # Reading Documentation

Although you learn the basics of using Fedora in this book, you need time and practice to master and troubleshoot more complex aspects of the Linux operating system and your distribution. As with any operating system, you can expect to encounter some problems or perplexing questions as you continue to work with Linux. The first place to turn to help with these issues is the documentation included with your system; if you cannot find the information you need there, check Fedora's website.

> **NOTE**
> 
> Checking Fedora's website for security updates and bug fixes is a good idea. Browse to http://fedoraredhat.com/download/. Alternatively, you can always do a quick yum update to make sure your system has the most up-to-date software available.

Linux, like Unix, is a self-documenting system, with manual pages accessible through the man command. Linux offers many other helpful commands for accessing its documentation. You can use the apropos command—for example, with a keyword such as partition—to find commands related to partitioning, like this:

```
```
$ apropos partition
GNU Parted [parted]     (8) - a partition manipulation program
fdisk                   (8) - Partition table manipulator for Linux
jfs_mkfs                (8) - create a JFS formatted partition
jfs_mkfs [mkfs]         (8) - create a JFS formatted partition
lvmdiskscan             (8) - scan for all disks / multiple devices / partitions
➜ available
mpartition              (1) - partition an MSDOS hard disk
partprobe               (8) - inform the OS of partition table changes
pvcreate                (8) - initialize a disk or partition for use by LVM
sfdisk                  (8) - Partition table manipulator for Linux
```
```

To find a command and its documentation, you can use the whereis command. For example, if you are looking for the fdisk command, you can do this:

```
```
$ whereis fdisk
fdisk: /sbin/fdisk /usr/share/man/man8/fdisk.8.gz
```
```

# ## Using man Pages

To learn more about a command or program, use the man command, followed by the name of the command. Manual pages for Linux and X Window commands are within the /usr/share/man, /usr/local/share/man, and /usr/X11R6/man directories; so, for example, to read the rm command's man page, use the man command like this:

```
```
$ man rm
```
```