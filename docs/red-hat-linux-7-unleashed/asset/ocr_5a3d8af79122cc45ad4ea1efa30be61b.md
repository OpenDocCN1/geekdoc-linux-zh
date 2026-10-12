When you are browsing the filesystem, it is not always easy to quickly see the difference between an empty device and a mount point on which no device has been mounted. A good way to make this simpler is to create a file called filesystem not. mounted in each directory that is to serve as a mount point. You will then immediately see whether or not there is a device mounted on the mount point.

Here is an example of the mount command being used:

```
```
# ls /mnt/floppy
filesystem not mounted
# mount -t vfat /dev/fd1 /mnt/floppy
mount: block device /dev/fd1 is write-protected, mounting read-only
# ls /mnt/floppy
grub-0.4.tar.gz
# umount /mnt/floppy
# ls /mnt/floppy
filesystem not mounted
```
```

In this example, I listed the files in my /mnt/floppy mount point. I saw that no diskette was mounted, so I mounted a diskette containing a vfat filesystem at the mount point. I got an informational message telling me that the diskette was write-protected; if the diskette had not been write-protected, there would have been no message. The directory /mnt/floppy already existed. I used ls to see what was on the disk and unmounted it again using the umount command. I then ran ls again, and the response I got was simply the name of a file that I leave in the directory /mnt/floppy on my hard disk to remind me that there currently is nothing mounted there. This hint enables me to distinguish a written diskette from an empty diskette that is mounted. You can also use the df command to see what filesystems are mounted. For example:

```
```
# mount -t vfat /dev/fd0 /mnt/floppy
# df /mnt/floppy
Filesystem           1k-blocks     Used Available Use% Mounted on
/dev/fd0                1423        0      1423   0% /mnt/floppy
# umount /mnt/floppy
# df /mnt/floppy
Filesystem           1k-blocks     Used Available Use% Mounted on
/dev/hda6              202006   1850753    72493  96% /
```
```

As you see from the example, when a device is mounted on a mount point, df will output statistics for that device; otherwise it will output statistics about the device upon which the directory resides.