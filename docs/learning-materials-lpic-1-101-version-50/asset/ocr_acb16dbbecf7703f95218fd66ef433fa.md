+   3. Imagine you have a disk at /dev/sdb, and you want to create a 1 GB partition at the start of it. So, using parted, you create the partition with mkpart primary linux-swap 0 1024M. Then, you enable swap on this partition with swapon /dev/sdb1, but get the following error message:

```
swapon: /dev/sdb1: read swap header failed
```

What went wrong?

You created a partition of the correct type (linux-swap), but remember that mkpart does not create a filesystem. You forgot to set-up the partition as a swap space first with mkswap before using it.

+   4. During the course of this lesson, you were trying out some commands in parted but, by mistake, deleted the 3rd partition on your hard disk. You know that it came after a 250 MB EFI partition and a 4 GB swap partition, and was 10 GB in size. Which parted command can you use to recover it?

Don’t panic, you have all the information you need to recover the partition, just use rescue and do the math. You had 250 MB + 4.096 MB (4*1024) before it, so the start point should be around 4346 MB. Plus 10,240 MB (10*1024) in size, it should end at 14,586 MB. So, rescue 4346m 14586m should to the trick. You might need to give some “slack” to rescue, starting a little early and ending a little late, depending on the geometry of your disk.

+   5. Imagine you have a 4 GB unused partition on /dev/sda3. Using fdisk, what would be the sequence of operations to turn it into an active swap partition?

First, change the partition type to “Linux Swap” (82), write your changes to disk and quit. Then, use mkswap to set up the partition as a swap area. Then, use swapon to enable it.