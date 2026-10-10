multiplying all of them together. The disk used for the demonstration of **fdisk** back in Chapter 9 had the following information:

```
# fdisk /dev/ad1
*****  Working on device /dev/ad1  *****
parameters extracted from in-core disklabel are:
cylinders=1247 heads=255 sectors/track=63 (16065 blks/cyl)
Media sector size is 512
```

Multiplying these figures together (ignoring the blocks-per-cylinder figure) and remembering that a cylinder-head is equivalent to a track (to keep your units straight), produces the following:

1247 cylinders × 255 heads × 63 sectors/track × 512 bytes/sector = 10.2GB

But wait a minute... 255 heads? Does that make sense at all? No, first of all we’d expect the number of heads to at least be an even number. Even if we allowed for that, we’re talking about what appears to be at least 64 platters, which just isn’t physically possible in a half-inch-high hard disk. What we’ve got here is a virtual disk geometry, made possible by two successive hacks by the hard disk industry, which get around register-size limitations imposed by the original design of the disk interface in the BIOS. These two hacks are LBA and Extended INT13 modes.

# LBA and the 528MB Limit

In the days of floppy disks, nobody ever thought that anyone would ever use a disk as gargantuan as 528MB; this is why that number was allowed to remain as the size limitation imposed by the number of bits the original PC BIOS (combined with the ATA/IDE standard) allocated to each of the disk geometry dimensions, shown in Table 18.5.

TABLE 18.5 Dimensional Limits on Hard Disk Geometry

| Dimension | Bit Size | Maximum Value |
| :--- | :--- | :--- |
| Cylinders | 10 bits | 2^10 = 1,024 |
| Heads | 8 bits | 2^8 = 256 |
| Sectors/track | 6 bits | 2^6-1 = 63 |

Therefore, a disk was allowed to have up to 256 heads, but no more than 1,024 cylinders. Because the number of bytes per sector and the number of sectors per track are relatively fixed numbers (dependent on physical limitations such as rotation speed and read reliability), and because you can’t really put more than a few platters and heads into a drive you want people to be able to lift, this meant that the cylinder number rapidly emerged as the limiting factor in a disk’s ultimate size. Disk manufacturers eventually converged on the ATA standard of 16 physical heads in a disk, so this meant a size limit of 528MB. The manufacturers could produce disks larger than that size by adding more cylinders—which