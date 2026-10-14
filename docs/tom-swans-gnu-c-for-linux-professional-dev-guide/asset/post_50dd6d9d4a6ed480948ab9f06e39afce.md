
directories for the mount points. Do this in Linux by logging in as root and then entering commands at a console prompt such as the following:

```
$ cd /mnt
$ mkdir msdosC
$ mkdir msdosD
```

You now have two directories, /mnt/msdosC and /mnt/msdosD, that you can use to mount your MS-DOS partitions. You need to know the device names for each partition, which you can find using fdisk or the equivalent utility. (You must be the super user to run the Linux /sbin/fdisk utility.) For example, to mount my C: and D: drives, I can enter these commands:

```
$ mount -t msdos /dev/hda1 /mnt/msdosC
$ mount -t msdos /dev/hda5 /mnt/msdosD
```

> **Tip**  
> To become the super user, instead of logging off and back in, you can simply enter `su` at a console prompt and enter the root password. Type `exit` to give up your super powers and return to normal.

The -t option specifies the disk type (msdos here). The last two arguments give the device name and mount point directories. If the commands are successful, you should now have access to all files on C: and D:. (However, depending on the type of file allocation table, or FAT, in use on your MS-DOS or Microsoft Windows partitions, long filenames might be truncated to the old MS-DOS 8.3 format.)

Determining the proper device names might take some digging. On my system, /dev/hda1 is the first partition and references my C: drive. This should be the same for all users. The /dev/hda5 device is the first logical drive (my D: drive), which is actually stuffed inside an extended partition. That partition's device name is /dev/hda2, but we don't want to mount the partition; we want to mount the logical drive inside the partition (which might contain multiple logical drives). Because only four primary partitions are permitted, logical partitions begin with /dev/hda5, /dev/hda6, and so on.

Hard drive partitions are unmounted automatically when you shut down Linux. Because you can't physically remove hard disks from their chassis, it isn't necessary to unmount them. However, you may do so by issuing the following commands (again, you might have to be the super user):

```
$ umount /mnt/msdosC
$ umount /mnt/msdosD
```

## AUTOMATIC MS-DOS DRIVE MOUNTING

If you want to have Linux automatically mount your MS-DOS partitions at boot time, log in as root and edit the file /etc/fstab with the necessary mounting information. Unless specified as noauto, all devices in /etc/fstab are mounted if possible when Linux starts. The information in the file also makes using the mount command easier. After entering the correct data in /etc/fstab, you can simply specify the mount point to mount any device. The mount utility retrieves the drive's type and its device name from the information in /etc/fstab.

Listing 2.1 shows the /etc/fstab file on my system. Do not blindly copy this data to your file! Before creating an entry in your file, you should have tested the command thoroughly as suggested in the preceding section. After successfully mounting a disk in a drive, you can enter that device's information into /etc/fstab. Copy and preface any modified lines with # to turn them into comments for future reference. For safety, make a copy of the unmodified file and also note in your installation log any changes you make.

### LISTING 2.1 THE AUTHOR'S /ETC/FSTAB FILE

| /dev/hda4 | / | ext2 | defaults | 1 | 1 |
| --- | --- | --- | --- | --- | --- |
| /dev/hda3 | swap | swap | defaults | 0 | 0 |
| /dev/fd0 | /mnt/floppy | ext2 | noauto,user | 0 | 0 |
| /dev/cdrom | /mnt/cdrom | iso9660 | noauto,ro,user | 0 | 0 |
| /dev/hda1 | /mnt/msdosC | msdos | defaults | 0 | 0 |
| /dev/hda5 | /mnt/msdosD | msdos | defaults | 0 | 0 |
| /dev/hda4 | /mnt/zip | ext2 | noauto,user | 0 | 0 |
| none | /proc | proc | defaults | 0 | 0 |

> Listing 2.1, /etc/fstab, is for reference only. It is not included on this book's CD-ROM. Do not copy or use this file on your system. Use it only as a guide for configuring the actual file-system devices listed in your installation's /etc/fstab file.

In addition to adding entries for /mnt/msdosC and /mnt/msdosD, I also changed the entries for /dev/fd0 (floppy drive 0, otherwise known as A:) and /dev/cdrom to include the word user in the fourth column. This change allows me to mount these devices while logged in under my username instead of root. I also specified noauto for these entries to prevent them from being mounted automatically during booting because I normally don't keep disks in the drives. (See the sections on Iomega zip drives near the end of this chapter for the meaning of the next-to-last entry.) With my /etc/fstab file, to mount a Linux floppy disk, I can insert it and simply type the following:

```
$ mount /mnt/floppy
```

This causes the mount utility to read the device information for that mount point from /etc/fstab. I can similarly mount a CD-ROM by inserting it and then typing this:
