# Configuring a CD-ROM Drive

You treat CD-ROM drives similar to — not exactly like — disk drives. The special file for CD-ROMs in Linux is usually /dev/cdrom, /dev/hdc, /dev/hdd, or /dev/sr0, depending on factors such as the CD-ROM's type, how it is connected to the controller, and its device number.

![](bbox=[0.133, 0.252, 0.203, 0.335])

The most common type of CD-ROM is ATAPI, and Linux recognizes SCSI CD-ROMs are normally recognized as the kernel boots. If you installed the system from the SuSE Linux For Dummies CD-ROM, the CD-ROM will have been recognized by Linux and is probably called /dev/cdrom.

We mention that CD-ROMs are "not exactly like" other drives because CD-ROMs are read-only (which means you can't change their contents) and typically have only one file system to a disk. Therefore, you don't partition a CD-ROM, nor do you make a file system before mounting it. The manufacturer did these things. You simply have to mount where you want the CD-ROM and which it is attached to. We assume your CD-ROM drive is /dev/cdrom, which is really just a pointer to another special device file. This extra pointer (called a link) enables you to call the CD-ROM by the name /dev/cdrom, instead of having to call it /dev/sda or /dev/hdc on some systems (because it happens to be an IDE-based device).

Following is the command to mount a CD-ROM on your Linux system:

```
mount -r -t iso9660 /dev/cdrom /cdrom
```

Now you know about every type of disk storage that you'll see on a Linux system. You know how to identify the types of disk storage and partition them. You also know how to create file systems for them and how to mount and dismount file systems while the system is running. The Linux system dismounts file systems automatically when you shut the machine down — if you have put all of the necessary information into the /etc/fstab file — automatically mounts when you start the system up. So, as far as disk systems go, you should be all set.