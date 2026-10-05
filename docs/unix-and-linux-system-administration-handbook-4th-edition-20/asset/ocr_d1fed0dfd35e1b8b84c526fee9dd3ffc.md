# ls: list and index files

group would also have been replaced with an. The last character of the permissions (execution "other") is shown as t if the sticky bit of the file is turned on. If either the setuid/setgid or the sticky bit is set the corresponding execute is not, these bits appear as S or T.

The next field in the listing is the file's link count. In this case it is 3, indicating that /bin/gunzip is just one of three names for this file (the others are /bin/gunzip and /bin/zcat). Each time a hard link is made to a file, the file's link count is incremented by 1. Symbolic links do not affect the link count.

All directories have at least two hard links: the link from the parent directory and the link from the special file " inside the directory.

The next two in the ls are the owner and group owner of the file. In this example, the file's owner is root, and the file belongs to the group named root. The filesystem actually shows these user and group ID numbers as names. If the text versions (names) can't be determined, ls shows the values as numbers. If what happens if the owner or group that has the file has been deleted from your NIS or LDAP database (if you use one); /etc/passwd or /etc/group file. It could also indicate a problem

The next field is the size of the file bytes. This file is 6200 bytes long. Next comes the date of last modification: May 28, 2010. The last field in the listing is the name of the file, /bin/gunzip.

ls is slightly different for a device file. For example:

```
$ ls -l dev/tty00 crwrw---- root 4,0 Jun 11 20:41 /dev/tty00
```

Most files are the same, but outside of a size in bytes, ls shows the major and minor device nodes. dev/tty0 is the first virtual console on this (Red) system and is controlled by device driver 4 (the terminal driver).

One is useful for scoping out hard links is -i, which makes ls show each file's "inode number". Without going into too much detail about filesystem implementations, we'll just say that the inode number is an entry into a table that enumerates all the files in the filesystem. Inodes are the "things" that are pointed to by directory entries; hard links to the same file have the same inode number. To figure out a complex web of links, you need both ls -l to show link counts and inode numbers and find for matches.

Some other options that are important to know are -a to show all entries in a directory (even files whose name starts with a dot), -t to sort by modification time (-tr to sort in reverse chronological order), -F to sort the names of files in a way that distinguishes directories and executable files, -R to list recursively, and -h to show file sizes in human-readable form (e.g., 8K or 53M).

+   9. find mountpoint -xdev -inum inode-print.

![](bbox=[0.955, 0.346, 0.975, 0.436])