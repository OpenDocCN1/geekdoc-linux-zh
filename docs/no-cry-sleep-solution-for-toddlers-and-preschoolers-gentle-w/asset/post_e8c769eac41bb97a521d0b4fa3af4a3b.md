
Even the file systems on your hard disk partition must be explicitly mounted. When you install your Linux system and create the Linux partition on your hard drive, however, your system is automatically configured to mount your main file system whenever it starts. When your system shuts down, they are automatically unmounted. You have the option of unmounting any file system, removing it from the directory tree, and possibly replacing it with another, as is the case when you replace a CD-ROM.

Once a file system is actually mounted, an entry for it is made by the operating system in the /etc/mtab file. Here you will find listed all file systems currently mounted.

## File System Information

The file systems on each storage device are formatted to take up a specified amount of space. For example, you may have formatted your hard drive partition to take up 3GB. Files installed or created on that file system take up part of the space, while the remainder is available for new files and directories. To find out how much space you have free on a file system, you can use the df command or, on GNOME, you can use either the Procman System Monitor or the KDE DiskFree utility (More System Tools menu). For the Procman System Monitor (System Tools menu), click the System Monitor tab to display a bar graph of the free space on your file systems. KDE DiskFree displays a list of devices showing how much space is free on each partition, and the percentage used.

### df

The df command reports file system disk space usage. It lists all your file systems by their device names, how much disk space they take up, and the percentage of the disk space used, as well as where they are mounted. With the -h option, it displays information in a more readable format; such as measuring disk space in megabytes instead of memory blocks.

The df command is also a safe way to obtain a listing of all your partitions, instead of using fdisk (with fdisk you could erase partitions). df shows only mounted partitions, however, whereas fdisk shows all partitions.

```
$ df -h
Filesystem Size Used Avail Use% Mounted on
/dev/hda3 9.7G 2.8G 6.4G 31% /
/dev/hda2 99M 6.3M 88M 7% /boot
/dev/hda2 22G 36M 21G 1% /home
/dev/hdc 525M 525M 0 100% /mnt/cdrom
```

You can also use df to tell you to what file system a given directory belongs. Enter df with the directory name or df . for the current directory.

```
$ df
Filesystem 1024-blocks Used Available Capacity Mounted on
/dev/hda3 297635 169499 112764 60% /
```

### e2fsck and fsck

To check the consistency of the file system and repair it if it is damaged, you can use file system checking tools. fsck checks and repairs a Linux file system. e2fsck is designed to support ext2 and ext3 file systems, whereas the more generic fsck also works on any other file systems. The ext2 and ext3 file systems are the file systems normally used for Linux

hard disk partitions and floppy disks. Linux file systems beginning with Red Hat 7.3 are normally ext3, which you would use e2fsck to check. fsck and e2fsck take as their argument the device name of the hard disk partition that the file system uses.

```
fsck device-name
```

Before you check a file system, be sure that the file system is unmounted. e2fsck should not be used on a mounted file system. To use e2fsck, enter e2fsck and the device name that references the file system. The -p option automatically repairs a file system without first requesting approval from the user for each repair task. The following examples check the disk in the floppy drive and the primary hard drive:

```
# e2fsck /dev/fd0
# e2fsck /dev/hda1
```

With fsck, the -t option lets you specify the type of file system to check, and the -a option automatically repairs systems, whereas the -r option first asks for confirmation. The -A option checks all systems in the /etc/fstab file.

> Tip In earlier distribution versions, fsck and e2fsck were also used to recover file systems after disk crashes or reset-button reboots. With recent releases, journaling capabilities were introduced with file systems like ext3 and ReiserFS. Journaling provides for fast and effective recovery in case of disk crashes, so recovering with fsck or e2fsck is no longer necessary.

### Journaling

The ext3 and ReiserFS file systems introduced journaling capabilities to Linux systems. Journaling provides for fast and effective recovery in case of disk crashes, instead of using e2fsck or fsck. With journaling, a log is kept of all file system actions, which are placed in a journal file. In the event of a crash, Linux only needs to read the journal file and replay it to restore the system to its previous (stable) state. Files that were in the process of writing to the disk can be restored to their original state. Journaling also avoids lengthy fsck checks on reboots that occur when your system suddenly loses power or freezes and has to be restarted physically. Instead of using fsck to manually check each file and directory, your system just reads its journal files to restore the file system.

Keeping a journal entails more work for a file system than a nonjournal method. Though all journaling systems maintain a file system’s directory structure (what is known as the metadata), they offer various levels of file data recovery. Maintaining file data recovery information can be time-consuming, slowing down the file system’s response time. At the same time, journaling systems make more efficient use of the file system, providing a faster response time than the nonjournaled ext2 file system.
