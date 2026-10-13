![](bbox=[0.15, 0.16, 0.22, 0.27])

> Never ever run fsck on a mounted filesystem!!

To unmount the filesystem, use the umount command. If the filesystem is listed in /etc/fstab, the main table of filesystems and their mount points, you can specify either the mount point or the device name. Otherwise, just use the device name:

```
# umount /dev/hdb
umount: /disk2: device is busy
```

Oops! We need to move out of the /disk2 subsystem before we can unmount the disk:

```
# umount /dev/hdb
#
```

# 2. Let's try that fsck command again!

```
# fsck /dev/hdb
Parallelizing fsck version 1.23, (15-Aug-2001)
e2fsck 1.23, 15-Aug-2001 for EXT2 FS 0.5b, 95/08/09
/dev/hdb: clean, 11/64000 files, 8004/255528 blocks
```

When fsck reports "clean" as a result, it means that it didn't need to run a filesystem integrity check because one had been run sufficiently recently (by default, disks only force an fsck when there's a reason to do so, or every few months). The information about when the next scheduled fsck should occur is part of what's in the superblock.

Did you catch that this is a "parallelizing" version of fsck? That's a good thing. It means this program can check multiple filesystems simultaneously by running parallel check processes. This means that you can boot your system quite a bit faster, even after a bad shutdown sequence.

Also, it turns out that because of the different filesystems supported on many Unix systems, fsck is a front-end to versions of fsck designed for specific filesystem formats. In this case, because the system detected that /dev/hdb is an ext2 filesystem, it handed the request to check the disk off to e2fsck for processing.

Finally, notice that the last line reports the number of files and blocks used and available. Here there are 11 files out of 64,000 possible, and 8,094 blocks out of 255,528 possible used.

# 3. The -f flag forces fsck to step through a proper disk check regardless of when the next check is scheduled, and the -c flag causes the program to test and check for bad blocks. If you want a bit more of a clue regarding what the program is doing, use -v for verbose output (see Table 9.1 for a list of useful fsck flags).

![](bbox=[0.15, 0.88, 0.18, 0.92])