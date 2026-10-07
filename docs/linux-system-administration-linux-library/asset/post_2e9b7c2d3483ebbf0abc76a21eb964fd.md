
You can specify options from Table 10.1, as well as any other options you discover, for any filesystem. The noauto,user combination used for the floppy disk and CD-ROM drive in Listing 10.1 is particularly useful for removable-media devices, which it allows ordinary users to mount and unmount these devices. We be sure not to put spaces between mount options, just commas.

dump This column contains a 1 or 0, indicating that the dump utility should or not back up the specified partition when it runs.

fsck This column indicates the file system check order. When Linux boots, it checks filesystems with non-0 values in this column for corruption, in the order specified by this column's value. Normally, the root partition has a value of 1, while other Linux filesystems have higher values.

When you install Linux, it creates an initial /etc/fstab file based on the information you give the installation programs about your partitions. You can modify this configuration to add partitions not understood by the installation routines (such as BFS partitions, if you have OS installed); to fine-tune the configuration (such as adding extra parameters for FAT partitions); and to add variants, particularly for removable media. It's a good idea to test your mount options by issuing them with the mount command before adding them to /etc/fstab. (Of course, this doesn't make sense for some options, as noauto and user.) Once you've modified /etc/fstab, you can test its configuration by issuing the -a command which causes Linux to reread /etc/fstab and mount any filesystems that are not mounted but are listed without a noauto option in /etc/fstab.

You can also modify /etc/fstab using GUI configuration tools. Red Hat's Linuxconf, for example, enables this facility in its File Systems Access Local Drive area, as shown in Figure 10.2. You can add a new filesystem to the file by clicking Add, or edit an existing configuration by double-clicking the link on the right side of the window. In either case, you can set base features (such as the device filename, filesystem type, and mount point) and filesystem options (such as read-only, user mountable, and so on). These options were discussed in preceding sections.

## Using the mount Command

When you're using a filesystem, you can issue the umount command to unmount it. The basic syntax for command is:

```
umount [-a] [-f] [-t ftype] mountpoint | device
```

The meanings of the options are as follows:

- -a If this option is specified, umount tries to unmount all the partitions specified in /etc/fstab. This is an option that should not issue in normal operation, although you might need in emergency recovery systems after restoring a system to health.

# Figure 10.2 GUI system configuration tools let you edit /etc/fstab via a point-and-click interface.

![](img/4fb617eb648f87def380ef5d92052d01_348_0.png)

- -f When you specify -f, umount forces the mount operation. This option is useful if an ordinary umount command fails, which often occurs when an NFS server goes down.

- -t ftype If you use this parameter, umount unmounts filesystems of the specified type.

mountpoint is the mount point on which the device is mounted, such as /mnt/floppy or /home.

device is the device on which the filesystem resides, such as /dev/fd0 or /dev/hdb8.

Normally, you use umount without most options and specify only the mount point or the device, not both. For instance, you might type umount /mnt/floppy to unmount the floppy disk.

The umount command is most useful when applied to removable-media devices, because these devices are typically mounted and unmounted on a regular basis like Linux is running. Most installations leave hard disk partitions permanently mounted, so they need not be explicitly unmounted. Linux automatically unmounts these partitions when it shuts down, however; you may need to temporarily unmount a normally mounted partition when performing certain types of system maintenance, such as moving the contents of a partition to a new hard disk.

# PART 3

> WARNING Linux locks most removable devices, such as CD-ROM and Zip drives, so that you can't eject the disk while it's mounted. When you unmount the disk, the Eject button will work again. Floppy disk drives on x86 computers, however, cannot be locked. It's therefore possible to eject a floppy disk while it's still mounted. Because Linux caches writes to its filesystems, this mistake can cause serious filesystem corruption. Be very careful to mount a floppy disk before ejecting it.

## Removable Media

Linux's model of the disk world makes little distinction between hard disks and removable disks. You use the same mount and unmount commands to access both types of device, and you can use similar /etc/fstab entries for both types of media. Nonetheless, there are a few caveats and special features that apply to removable media devices only.

## Accessing Floppy Disks

The most important caveat concerning floppy disks is about ejecting them, as noted in the preceding Warning. Beyond this, you can access floppy disks as if they were very small hard disk partitions. The usual device file for accessing floppies is /dev/fd0. If your system has two floppy drives, the second is accessible as /dev/fd1. There are also a number of specialized device access files, such as /dev/fd0H1440, which provide forced access to a disk of 1440KB.

If you're presented with an unformatted disk, you must format it using two actions. First, you do a low-level format, as in /dev/fd0. Second, you create a tar file by issuing the following on source system:

```
$ tar -cvf/fd0 somidir
```

This command copies the contents of somidir to a floppy disk. You can reverse the process on the target system by issuing this command:

```
$ tar -xvf /dev/fd0
```

Of course, you can also transfer tar files in a similar way by mounting a disk with a filesystem (as /mnt/floppy/somidir.tar) rather than the device file. Why use direct access, it's most useful when transferring files between versions of Unix that don't share a common filesystem. You can be sure that a tar file written without a filesystem can be read by any Unix-like OS, because tar is so widely available. Support for any given filesystem is not so universal, although FAT support is extremely common on modern Unix.

One unusual shortcut for access to floppy disks is the Mtools package. It's a set of programs that allow access to FAT floppy disks (or, in principle, other removable media formatted with FAT) without explicitly mentioning them. Mtools includes a series of commands named after DOS disk-access commands. These include mkdir (to create a directory), mcopy (to copy a file), mdel (to delete a file), and mformat (to create a FAT file on a system). These commands use a DOS-style drive letter in place of Linux's device identifier. For instance, to copy a file to a floppy, you would type mcopy filename:: Mtools is a very useful method for copying a few files or from a FAT floppy, but if you want to give programs direct access to files on a floppy, you must mount it normally. Mtools comes with most Linux distributions. You can read more about it at http://mtools.linux/

A package similar to Mtools, called HFS Utilities, exists for accessing Macintosh floppies (http://www.mars.org/home/proj/hfs/). These utilities use an h prefix to the DOS-style commands, as in hdir and hformat. The package also includes a GUI front-end.

![](img/4fb617eb648f87def380ef5d92052d01_349_0.png)
