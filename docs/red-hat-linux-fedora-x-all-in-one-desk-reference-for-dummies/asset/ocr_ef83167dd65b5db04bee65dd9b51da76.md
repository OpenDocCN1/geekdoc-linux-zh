# 456 Using mtools

If you want a quick directory listing of a DOS floppy disk, however, mounting can become some quite tedious. First, you have to mount the floppy drive. Then you must use the ls command. Finally, you must use the umount command before ejecting the floppy out of the drive.

This situation is where the mtools package comes to the rescue. The mtools package implements most common DOS commands: the commands use the same names as DOS except that you add an m prefix to each command. Thus the command for getting a directory listing is mdir and mcopy copies files. The best part of mtools is the fact that you don't have to mount the floppy disk to use the mtools commands.

Because the mtools commands write to and read from the physical device (floppy disk), you must log in as root to perform these commands. If you want any user to access the mtools commands, you must alter the permission settings for the floppy drive devices. Use the following command to permit anyone to read from and write to the first floppy drive:

![](bbox=[0.14, 0.323, 0.215, 0.403])

```
chmod +rw /dev/fd0
```

# Trying mtools

To out mtools, follow these steps:

+   1. Place an MS-DOS floppy disk in your system's A drive.
2. Type mdir.

You see the floppy disk (in the standard DOS directory-listing format).

Typically, you use the mtools utilities to access the floppy disks. The default configuration file, /etc/mtools.conf, is set up to access the floppy drive as A Drive. You can also edit it to define C and D drives for your DOS hard-drive partitions, you can as well access the hard drive partitions by the Linux mount command to mount them. Because you can mount the hard-drive partitions automatically at startup, accessing them through Linux commands is normally just as easy.

# Understanding the /etc/mtools.conf file

The mtools package works with the default setup, but if you get any errors, check the /etc/mtools.conf file. That file contains the definitions of the drives (such as A, B, and C) that the mtools utilities see. Following are a few lines from a typical /etc/mtools.conf file: