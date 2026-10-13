Remember, you are mounting a particular floppy disk, not the floppy drive. You cannot simply remove the floppy disk and put in another one. The mount command has attached those files to your main directory tree, and your system expects to find those files on a floppy disk in your floppy drive. If you take out the disk and put another one in, you get an error message when you try to access it.

To change disks, you must first unmount the floppy disk already in your disk drive. Then, after putting in the new disk, you must explicitly mount that new disk. To do this, use the umount command.

```
# umount /dev/fd0
```

For the umount or mount operations, you can specify either the directory it is mounted on or the /dev/fd0 device.

```
# umount /mnt/floppy
```

You can now remove the floppy disk, put in the new one, and then mount it:

```
# mount /mnt/floppy
```

When you shut down your system, any disk you have mounted is automatically unmounted. You do not have to unmount it explicitly.

# Mounting CD-ROMs

Remember, when you mount a CD-ROM or floppy disk, you cannot then simply remove it to put another one in the drive. You first have to unmount it, detaching the file system from the overall directory tree. In fact, the CD-ROM drive remains locked until you unmount it. Once you unmount a CD-ROM, you can then take it out and put in another one, which you then must mount before you can access it. When changing several CD-ROMs or floppy disks, you are continually mounting and unmounting them. For a CD-ROM, instead of using the umount command, you can use the eject command with the device name or mount point, which will unmount and then eject the CD-ROM from the drive.

You can also mount CD-ROM disks to your Linux system using the mount command. On many distributions, the directory /mnt/cdrom has been reserved for CD-ROM file systems. You can see an entry for this in the /etc/fstab file presented earlier in the chapter. With such an entry, to mount a CD-ROM, all you have to do is enter the command mount and the directory /mnt/cdrom. You needn't specify the device name. Once it is mounted, you can access the CD-ROM through the /mnt/cdrom directory.

```
# mount /mnt/cdrom
```