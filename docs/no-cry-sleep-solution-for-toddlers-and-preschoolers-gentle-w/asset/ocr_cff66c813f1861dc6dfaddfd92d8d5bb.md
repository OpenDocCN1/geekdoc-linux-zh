When you shut down your system, any disk you have mounted is automatically unmounted. You do not have to unmount it explicitly.

# Mounting CD-ROMs

Remember, when you mount a CD-ROM or floppy disk, you cannot then simply remove it to put another one in the drive. You first have to unmount it, detaching the file system from the overall directory tree. In fact, the CD-ROM drive remains locked until you unmount it. Once you unmount a CD-ROM, you can then take it out and put in another one, which you must then mount before you can access it. When changing several CD-ROMs or floppy disks, you are continually mounting and unmounting them. For a CD-ROM, instead of using the umount command, you can use the eject command with the device name or mount point, which will unmount and then eject the CD-ROM from the drive.

You can also mount CD-ROM disks to your Linux system using the mount command. On many distributions, the directory /mnt/cdrom has been reserved for CD-ROM file systems. You can see an entry for this in the /etc/fstab file presented earlier in the chapter. With such an entry, to mount a CD-ROM, all you have to do is enter the command mount and the directory /mnt/cdrom. You needn't specify the device name. Once it is mounted, you can access the CD-ROM through the /mnt/cdrom directory.

```
# mount /mnt/cdrom
```

> Tip On GNOME, CD-ROMs are automatically mounted, though you can manually mount them by right-clicking the desktop background to display the desktop menu and then selecting CD-ROM in the Disk entry. To unmount, right-click the CD-ROM icon and select Eject from the pop-up menu.

```
# umount /mnt/cdrom
```

If you want to mount a CD-ROM to another directory, you have to include the device name in the mount command. The following example mounts the disc in your CD-ROM drive to the /mydir directory. The particular device name for the CD-ROM in this example is /dev/hdc.

```
# mount /dev/hdc /mydir
```

When you burn a CD, you may need to create a CD image file. You could access such an image file from your hard drive, mounting it as if it were another file system (even ripped images could be mounted in this way). For this, you use the loop option, specifying an open loop device such as /dev/loop0. If no loop device is indicated, mount will try to find a open one. The file system type is iso9660, a CD-ROM iso image file type.