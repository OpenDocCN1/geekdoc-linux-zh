Device drivers in Unix, however, are files. They're special files, but they show up as part of the file system along with your e-mail archive and login scripts.

That's what the /dev/sda5 is on the first line, for example. We can have a look at this file with ls to see what it is:

```
```
# ls -l /dev/sda5
brw-rw---- 1 root disk 8, 5 Aug 30 13:30 /dev/sda5
```
```

The leading b is something you probably haven't seen before. It denotes that this device is a block-special device.

> > If you ever have problems with a device, use ls -l to make sure it's configured properly. If the listing doesn't begin with a c (for a character special device) or a b (for a block-special device), something's gone wrong and you need to delete it and rebuild it with mknod.

Here's a nice thing to know: The device names in Unix have meaning. In fact, sd typically denotes a SCSI device, and the next letter is the major device number (in this case an a), and the last letter is the minor device number (5).

From this information, we can glean that there are three devices with the same major number but different minor numbers (sda1, sda3, and sda5), and two devices with a different major number and different minor numbers (sdb1 and sdb2).

In fact, the first three are partitions on the same hard disk, and the second two are partitions on a different disk.

# 3. How big is the disk?

Well, in some sense it doesn't really matter in the world of Unix, because Unix only cares about the partitions that are assigned to it. If the second disk is 75GB, but we only have a 50MB partition that's available to Unix, the vast majority of the disk is untouchable and therefore doesn't matter.

If you really want to figure it out, you could add up the size of each partition (the Available column), but let's dissect a single line of output first, so you can see what's what:

```
```
/dev/sda5 380791 108116 253015 30% /
```
```