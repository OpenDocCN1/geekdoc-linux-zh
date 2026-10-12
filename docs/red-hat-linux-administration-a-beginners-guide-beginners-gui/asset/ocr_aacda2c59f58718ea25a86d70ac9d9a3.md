Now you’re ready to create the last three partitions:

```
```
Command (m for help): n
First cylinder (289-665, default 289): 289
Last cylinder or +size or +sizeM or +sizeK (289-665, default 665): +100M
Command (m for help): n
First cylinder (493-665, default 493): 493
Last cylinder or +size or +sizeM or +sizeK (493-665, default 665): +45M
Command (m for help): n
First cylinder (585-665, default 585): 585
Last cylinder or +size or +sizeM or +sizeK (585-665, default 665): 665
Command (m for help):
```
```

Note that for the very last partition, you again specified the last cylinder instead of a megabyte value, so that you are sure that you have allocated the entire disk. One last p command shows you what your partitions now look like:

```
```
Command (m for help): p
Disk /dev/hdb: 16 heads, 63 sectors, 665 cylinders
Units = cylinders of 1008 * 512 bytes

Device Boot Start End Blocks Id System
/dev/hdb1 1 51 2567+ 83 Linux
/dev/hdb2 52 84 16632 82 Linux swap
/dev/hdb3 85 288 102816 83 Linux
/dev/hdb4 289 665 190008 5 Extended
/dev/hdb5 289 492 102784+ 83 Linux
/dev/hdb6 493 584 46336+ 83 Linux
/dev/hdb7 585 665 40792+ 83 Linux
Command (m for help):
```
```

Perfect. Commit the changes to disk and quit the fdisk utility by using the w (write table to disk and exit) command:

```
```
Command (m for help): w
The partition table has been altered!
Calling ioctl() to re-read partition table.
Syncing disks.
WARNING: If you have created or modified any DOS 6.x
partitions, please see the fdisk manual page for additional
information.
[root@tedford /root]#
```
```

If you needed to write an /etc/fstab file yourself for this configuration, it would look something like this: