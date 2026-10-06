# Displaying Space with df

You can display the space available in your file systems using the df command. You can see the amount of space available on all the mounted file systems on your Linux computer, type df:

| Filesystem | k-blocks | Used | Available | Use% | Mounted on |
| /dev/hda3 | 3065460 | 2958356 | 26130408 | 11% | / |
| /dev/hda2 | 46668 | 8340 | 35919 | 19% | / |
| /dev/fd0 | 1412 | 13 | 1327 | 1% | /mnt/floppy |

This example shows the space available on the hard disk partition on the (root) partition (/dev/hda1) and boot partition (/dev/hda2), floppy disk mounted at /mnt/floppy directory (/dev/fd0). Space is shown in 1K blocks. To produce a more human-readable output, use the -h option

| Filesystem | Size | Used | Avail | Use% | Mounted on |
| /dev/hda3 | 29G | 2.9G | 24G | 11% | / |
| /dev/hda2 | 46M | 8.2M | 25M | 19% | / |
| /dev/fd0 | 1.4M | 1K | 1.2M | | /mnt/floppy |

With the -h option, output appears in megabyte or gigabyte listing. Other options with df enable you to do the following:

+   * Print only file systems of a particular type (-t type)
* Exclude file systems of a particular type (-x type)
* Include file systems that have no space, such as /proc and /devpts (-a)
* List only available and used nodes (-i)
* Display space in certain block sizes (-block-size=#)

# Checking Disk Usage with du

To find how much space is being consumed by a particular directory (and its subdirectories), use the du command. du lists all directories below the current directory, along with the space consumed by each directory. At the end, du produces total disk space used within that directory structure.

The du command is a good way to check how much space is being used by particular user (du /home/user) or in a particular file partition (du /var). By default, disk space is displayed in 1K blocks. To produce a more human-readable output (in kilobytes, megabytes, and gigabytes), use the -h option as follows:

```
$ du -h /home/jake
114k /home/jake/stuff
234k /home/jake/httpd
137k /home/jake/ucp
701k /home/jake/uucp
1.0M /home/jake
```