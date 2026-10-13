![](bbox=[0.16, 0.2, 0.24, 0.3])

> Those purists among you will realize the error of this calculation: 380,791/1024 is not a simple division by 1,000. So everyone is happy, that reveals that this partition is exactly 371.8MB.

The last value is perhaps the most important because it indicates where the partition has been connected to the Unix file system. Partition sda5 is the root partition, as can be seen by the /.

4. Let's look at another line from the df output:

```
/dev/sda3 16033712 62616 15156608 1% /home
```

Notice here that the partition is considerably bigger! In fact, it's 16,033,712KB, or roughly 16GB (15.3GB for purists). Unsurprisingly, very little of this is used—less than 1%—and it's mounted to the system as the /home directory.

In fact, look at the mount points for all the partitions for just a moment:

```
# df
Filesystem 1k-blocks Used Available Use% Mounted on
/dev/sda5 380791 108116 253015 30% /
/dev/sda1 49558 7797 39202 17% /boot
/dev/sda3 16033712 62616 15156608 1% /home
none 256436 0 256436 0% /dev/shm
/dev/sdb1 17245524 1298460 15070936 8% /usr
/dev/sdb2 253871 8839 152375 37% /var
```

We have the topmost root partition (sda5); then we have additional small partitions for /boot, /usr, and /var. The two really big spaces are /home, where all the individual user files will live, and /usr, where I have all the Web sites on this server stored.

This is a very common configuration, where each area of Unix has its own sandbox to play in, as it were. This lets you, the sysadmin, manage file usage quite easily, ensuring that running out of space in one directory (say, /home) doesn't affect the overall system.

5. Solaris 8 has a df command that offers very different information, focused more on files and the file system than on disks and disk space used:

```
# df
/ (/dev/dsk/c0d0s0 :) 827600 blocks 276355 files
/boot (/dev/dsk/c0d0p0:boot:) 17584 blocks -1 files
/proc (/proc :) 0 blocks 1888 files
/dev/fd (fd :) 0 blocks 0 files
/etc/mnttab (mnttab :) 0 blocks 0 files
/var/run (swap :) 1177992 blocks 21263 files
/tmp (swap :) 1177992 blocks 21263 files
/export/home (/dev/dsk/c0d0s7 :) 4590890 blocks 387772 files
```