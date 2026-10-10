ls of tries to process all mounted filesystems. This warning message is raised because ls of has encountered a GNOME Virtual file system (GVFS). This is a special case of a filesystem in user space (FUSE). It acts as a bridge between GNOME, its APIs and the kernel. No one—not even root—can access one of these file systems, apart from the owner who mounted it (in this case, GNOME). You can ignore this warning.

# Where to Mount?

You can mount a filesystem anywhere you want. However, there are some good practices that should be followed to make system administration easier.

Traditionally, /mnt was the directory under which all external devices would be mounted and a number of pre-configured “anchor points” for common devices, like CD-ROM drives (/mnt/cdrom) and floppy disks (/mnt/floppy) existed under it.

This has been superseded by /media, which is now the default mount point for any user-removable media (e.g. external disks, USB flash drives, memory card readers, etc.) connected to the system.

On most modern Linux distributions and desktop environments, removable devices are automatically mounted under /media/USER/LABEL when connected to the system, where USER is the username and LABEL is the device label. For example, a USB flash drive with the label FlashDrive connected by the user john would be mounted under /media/john/FlashDrive/. The way this is handled is different depending on the desktop environment.

That being said, whenever you need to manually mount a filesystem, it is good practice to mount it under /mnt.

# Mounting Filesystems on Bootup

The file /etc/fstab contains descriptions about the filesystems that can be mounted. This is a text file, where each line describes a filesystem to be mounted, with six fields per line in the following order:

```
FILESYSTEM MOUNTPOINT TYPE OPTIONS DUMP PASS
```

Where:

**FILESYSTEM**

The device containing the filesystem to be mounted. Instead of the device, you can specify the UUID or label of the partition, something which we will discuss later on.