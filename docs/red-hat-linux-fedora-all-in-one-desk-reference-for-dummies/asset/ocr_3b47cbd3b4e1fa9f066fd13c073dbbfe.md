The umount command succeeds as long as no one is using the CD-ROM. If you get an error when trying to unmount the CD-ROM, check to see whether the current working directory is on the CD-ROM. If you're currently working in one of the CD-ROM's directories, that also qualifies as a use of the CD-ROM.

# Examining the /etc/fstab file

The mount command has the following general format:

```
mount device-name mount-point
```

However, you can mount the CD-ROM by typing one of the following commands:

```
mount /dev/cdrom
mount /mnt/cdrom
```

![](bbox=[0.18, 0.55, 0.27, 0.68])

You can mount by specifying only the CD-ROM device name or the mount-point name because of what's in a file named /etc/fstab. There is a line in the /etc/fstab file for the /mnt/cdrom mount point. That entry specifies the CD-ROM device name and the file-system type. That's why you can mount the CD-ROM with a shorter mount command.

The /etc/fstab file is a configuration file — a text file containing information that the mount and umount commands use. Each line in the /etc/fstab file provides information about a device and its mount point in the Red Hat Linux file system. Essentially, the /etc/fstab file associates various mount points within the file system with specific devices, which enables the mount command to work from the command line with only the mount point or the device as argument.

Here is a /etc/fstab file from a typical Red Hat Linux system:

```
LABEL=/              /           ext3    defaults        1 1
LABEL=/boot          /boot       ext3    defaults        1 2
none                 /dev/pts    devpts  gid=5,mode=620  0 0
none                 /proc       proc    defaults        0 0
none                 /dev/shm    tmpfs   defaults        0 0
/dev/hda6            swap        swap    defaults        0 0
/dev/cdrom           /mnt/cdrom  udf,iso9660 noauto,owner,kudzu,ro 0 0
/dev/fd0             /mnt/floppy auto    noauto,owner,kudzu 0 0
```

The first field on each line shows a device name, such as a hard-drive partition (or it identifies a partition by a LABEL keyword). The second field is the mount point, and the third field indicates the type of file system on the device. You can ignore the last three fields for now.