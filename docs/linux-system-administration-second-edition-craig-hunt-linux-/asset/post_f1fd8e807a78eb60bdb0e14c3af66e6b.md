
## Listing 6.1: A Sample /etc/fstab File

| #device | mountpoint | fs | options | dump | fsck |
|---|---|---|---|---|---|
| /dev/hda2 | / | ext2 | defaults | 1 | 1 |
| /dev/hdb7 | /home | jfs | defaults | 0 | 2 |
| /dev/hda3 | /dos | msdos | umask=0 | 0 | 0 |
| server:/home | /server/home | nfs | ro | 0 | 0 |
| /dev/cdrom | /mnt/cdrom | iso9660 | noauto,user | 0 | 0 |
| /dev/fd0 | /mnt/floppy | auto | noauto,user | 0 | 0 |
| /dev/hdb8 | swap | swap | defaults | 0 | 0 |

The /etc/fstab file's columns contain the following information:

**device** This column lists the device filename associated with the disk or partition. One of the devices in Listing 6.1, *server:/home*, is an NFS share. For this device, *server* is the name of the server, and */home* is the directory it exports.

**mountpoint** This column indicates the mount point for the filesystem. The first entry is usually */*, the root filesystem. Linux normally reads the /etc/fstab file from the root filesystem, but once it gets this file, it remounts the root filesystem using the options specified in this file. A swap partition, which is used as an extension of RAM, uses a mount point of swap or none.

**fs** You must specify the filesystem type code for most filesystems. If you use any nonstandard filesystems, such as jfs for the /home partition in Listing 6.1, you must ensure that you've compiled your kernel with that support. It's also critically important that the root partition's filesystem be compiled *into the kernel* (rather than as a module), or else Linux won't be able to read its startup files. The /mnt/floppy mount point in Listing 6.1 specifies a filesystem type code of auto. Linux can auto-detect many filesystem types, and this configuration is particularly convenient for removable-media devices such as floppy drives.

> Don't confuse the /etc/fstab filesystem type code of auto (which tells Linux to auto-detect the filesystem type) with the auto mount option (which tells Linux to mount the filesystem at boot time).

**options** You can specify options from Table 6.1, as well as any other options you discover, for any filesystem. The noauto, user combination used for the floppy disk and CD-ROM drive in Listing 6.1 is particularly useful for removable-media devices, because it allows ordinary users to mount and unmount these devices. Be sure not to put spaces between mount options, just commas.

**dump** This column contains a 1 or 0, indicating that the dump utility should or should not back up the specified partition when it's run. This utility is filesystem-specific, and JFS still lacks a dump program, which is why it's set to 0 for the JFS /home partition in Listing 6.1.

**fsck** This column indicates the *file system check* order. When Linux boots, it checks filesystems with non-0 values in this column for corruption, in the order specified by this column's value. Normally, the root partition has a value of 1, while other Linux native filesystems have higher values. XFS and ext3fs partitions should have values of 0, because these filesystems handle this task automatically whenever they're mounted. Most non-native filesystems lack fsck utilities, and so should have 0 values, as well.

When you install Linux, it creates an initial /etc/fstab file based on the information you gave the installation programs about your partitions. You can modify this configuration to add partitions not understood by the installation routines (such as BeFS partitions, if you have BeOS installed); to fine-tune the configuration (such as adding extra parameters for FAT partitions); and to add variants, particularly for removable media. It’s a good idea to test mount options by issuing them directly with the mount command before adding them to /etc/fstab. (Of course, this doesn’t make much sense for some options, such as noauto and user.) Once you’ve modified /etc/fstab, you can test its configuration by typing **mount -a**. This causes Linux to reread /etc/fstab and mount any filesystems that are not mounted but that are listed without a noauto option in /etc/fstab.

You can also modify /etc/fstab using GUI configuration tools. In Webmin, for example, you can select the Disk and Network File systems item in the System area, as shown in Figure 6.4. This configuration page presents a summary of information on the computer’s filesystems. By clicking a mount point (in the Mounted As column), you can adjust the mount options, as shown in Figure 6.5. You can also mount and unmount a filesystem from this page.

![](img/10371fe30b7fdac23ef2ef30d5ffe738_157_0.png)

Figure 6.4: GUI system configuration tools let you edit /etc/fstab via a point-and-click interface.

## Using the `umount` Command

When you’re done using a filesystem, you can issue the umount command to unmount it. The basic syntax for this command is as follows:

```
umount [-a] [-f] [-t *fstype*] *mountpoint* | *device*
```

The meanings of the options are as follows:

- **-a** If this option is specified, umount tries to unmount all the partitions specified in /etc/fstab. This is an option you should *not* issue in normal operation, although you might in emergency recovery situations after restoring a system to health.
- **`-f`** When you specify `-f`, umount forces the unmount operation. This option can be useful if an ordinary umount command fails, which often occurs when an NFS server goes down.
- **`-t fstype`** If you use this parameter, umount unmounts filesystems of the specified type.
- **`mountpoint`** This is the mount point on which the device is mounted, such as /mnt/floppy or /home.
- **`device`** This is the device on which the filesystem resides, such as /dev/fd0 or /dev/hdb8.

Normally, you use umount without most options and specify only the mount point or the device, not both. For instance, you might type `umount /mnt/floppy` to unmount the floppy disk.

The umount command is most useful when applied to removable-media devices, because these devices are typically mounted and unmounted on a regular basis while Linux is running. Most installations leave hard disk partitions permanently mounted, so they need not be explicitly unmounted. Linux automatically unmounts these partitions when it shuts down, however, and you may need to temporarily unmount a normally mounted partition when performing certain types of system maintenance, such as moving the contents of a partition to a new hard disk.

![](img/10371fe30b7fdac23ef2ef30d5ffe738_158_0.png)

**Figure 6.5.** Webmin uses mount option descriptions that are more verbose than the actual options in /etc/fstab.

**Warning** Linux locks most removable devices, such as CD-ROM and Zip drives, so that you can't eject the disk while it's mounted. When you unmount the disk, the eject button will work again. Floppy disk drives on x86 computers, however, cannot be locked. It's therefore possible to eject a floppy disk while it's still mounted. Because Linux caches writes to its filesystems, this mistake can cause serious filesystem corruption. Be very careful to unmount a floppy disk before ejecting it.

## Using Removable Media

Linux's model of the disk world makes little distinction between hard disks and removable disks. You use the same mount and umount commands to access both types of devices, and you can create similar /etc/fstab entries for both types of media. Nonetheless, there are a few caveats and special features that apply to removable media only.

### Accessing Floppy Disks

The most important caveat concerning floppy disks is about accidentally ejecting them, as noted in the preceding Warning. Beyond this, you can access floppy disks as if they were very small hard disk partitions. The usual device file for accessing floppies is /dev/fd0. If your system has two floppy drives, the second is accessible as /dev/fd1. There are also a number of specialized device access files, such as /dev/fd0H1440, which provide forced access to a disk of a specific capacity, such as 1440KB for /dev/fd0H1440. (In normal operation, you can use /dev/fd0 to access disks of any capacity.)

If you're presented with an unformatted floppy disk, you must format it. In DOS or Windows, this procedure is handled with a single command, FORMAT. In Linux, by contrast, you perform two actions. First, you do a low-level format using the fdformat command, as in fdformat /dev/fd0. (It's here that the capacity-specific device files can be most useful, because they can force a format at a specified capacity.) Second, you create a filesystem on the disk, as described in "Creating a Filesystem" later in this chapter.

Most filesystems that you use on hard disks can be used on floppy disks, with a few exceptions. Most notably, some journalling filesystems require journal files larger than floppies can hold. You can use Linux's ext2fs on floppy disks, but ext2fs has enough overhead that it's not the best choice. The Minix filesystem is popular on floppy disks because it includes support for Linux permissions and ownership, and it consumes less overhead than ext2fs. FAT filesystems, too, are popular on floppies, even for transfer between Linux systems. The drawback to FAT is that you lose Linux ownership and permissions unless you also archive files into a tar or similar carrier file.

### Disk Access without a Filesystem

It's possible to access a floppy disk without using a filesystem *per se*. This is commonly done by writing a tar file directly to a floppy disk. Suppose you want to transfer a directory, somedir, between systems. You can do so by issuing the following tar command on the source system:

```
$ tar -cvf /dev/fd0 somedir
```

This command copies the contents of somedir to a tar file on the floppy disk. You can reverse the process on the target system by issuing this command:

```
$ tar -xvf /dev/fd0
```

Of course, you can also transfer tar files in a similar way by mounting a disk with a filesystem and then using an appropriate tar file on the disk (such as /mnt/floppy/somedir.tar) rather than the device file (/dev/fd0). Why use direct access, then? It's most useful when transferring files between versions of Unix that don't share an appropriate common filesystem. You can be sure that a tar file written without a filesystem can be read by any Unix-like OS, because tar is so widely available. Support for any given filesystem is not so universal, although FAT filesystem support is extremely
