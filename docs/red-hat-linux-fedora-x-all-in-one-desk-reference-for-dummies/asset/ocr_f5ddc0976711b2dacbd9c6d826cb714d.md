# Learning the Linux File System 441

drive. These physical devices are mounted at specific mount points on the Linux file system. For example, the DVD/CD-ROM drive, /dev/cdrom, is mounted on /mnt/cdrom in the file system. After mounting the CD-ROM the Fedora directory on a CD-ROM or DVD-ROM appears as /mnt/cdrom/Fedora in the Linux file system.

![](bbox=[0.233, 0.249, 0.813, 0.568])

**Figure 3-3:** You have to mount a device on the Linux file system before accessing it.

You can use the mount command to manually mount a device on the Linux file system at a specified directory. That directory is the mount point. For example, to mount the DVD/CD-ROM drive at /mnt/cdrom directory, you type the following command (after logging in root):

```
mount /dev/cdrom /mnt/cdrom
```

The mount command reports an error if the DVD/CD-ROM device is mounted already or if no CD or DVD media is in the drive. Otherwise, the mount operation succeeds, and you can access the DVD or CD's contents through /mnt/cdrom directory.

You can use any directory as the mount point. If you mount a device on a nonempty directory, however, you cannot access the files in that directory until you unmount the device by using the unmount command. Therefore, always use an empty directory as the mount point.

Fedora Core comes with the /mnt/cdrom directory for mounting DVDs and CDs and /mnt/floppy for mounting floppy drives.

![](bbox=[0.123, 0.868, 0.203, 0.936])