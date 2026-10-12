directory. For example, if you like to refer to the CD-ROM drive as /cd, first create the /cd directory with the mkdir /cd command and then use the following mount command:

```
mount /dev/cdrom /cd
```

Before you try this command, you have to “unmount” the CD-ROM with the following umount command:

```
umount /dev/cdrom
```

Only then you can mount the CD-ROM again on another directory in the Linux file system.

I have shown you the longer syntax for the mount command in which you explicitly specify the device name and the mount point, but Red Hat Linux contains a line in the /etc/fstab file that enables you to mount the CD-ROM through one of the following commands:

```
mount /mnt/cdrom
mount /dev/cdrom
```

It is customary to mount devices on directories in the /mnt directory. Red Hat Linux comes with two predefined directories: /mnt/cdrom for mounting the CD-ROM and /mnt/floppy for mounting the floppy.

In addition to mount and umount, you should know two more commands — df and du — that enable you to check the disk space usage. These commands are simple to use. The df command shows you a summary of disk space usage for all mounted devices, as shown in this example:

```
df
```

| Filesystem | 1k-blocks | Used | Available | Use% | Mounted on |
|---|---|---|---|---|---|
| /dev/hda2 | 2000236 | 1103852 | 794776 | 59% | / |
| /dev/hda1 | 2096160 | 1833600 | 262560 | 88% | /dosc |
| /dev/hdc | 656560 | 656560 | 0 | 100% | /mnt/cdrom |

The output is a table that shows the device, the total kilobytes of storage, how much is in use, how much is available, the percentage being used, and the mount point. For example, on my system, the /dev/hda2 device (a disk partition) is mounted on the Linux file system’s root directory (/). It has about 2GB of space of which 1.1GB (or 59 percent) are used and 794MB are available. Similarly, you can see from the last line that the CD-ROM has about 656MB of storage in use.