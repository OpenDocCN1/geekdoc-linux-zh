**“Installing Software,” for more details.**

All the filesystem commands allow you to create a default filesystem with just the simple command with no options, but you'll need to have super user privileges:

```
$ sudo mkfs.ext4 /dev/sdb1
[sudo] password for christine:
mke2fs 1.44.6 (5-Mar-2019)
Creating filesystem with 524032 4k blocks and 131072 inodes
[...]
Creating journal (8192 blocks): done
Writing superblocks and filesystem accounting information:
done
$
```

The new filesystem uses the ext4 filesystem type, which is a journaling filesystem in Linux. Notice that part of the creation process was to create the new journal.

**TIP**

Each filesystem utility command has lots of command-
line options that allow you to customize just how the
filesystem is created in the partition. To see all the
command-line options available, use the man command
(see Chapter 3) to display the manual pages for the
filesystem command you wish to use.

After you create the filesystem for a partition, the next step is to mount it on a virtual directory mount point so that you can store data there. You can mount the new filesystem anywhere in your virtual directory where you need the extra space.

```
$ mkdir /home/christine/part
$ sudo mount -t ext4 /dev/sdb1 /home/christine/part
[sudo] password for christine:
$
$ lsblk -f /dev/sdb
```