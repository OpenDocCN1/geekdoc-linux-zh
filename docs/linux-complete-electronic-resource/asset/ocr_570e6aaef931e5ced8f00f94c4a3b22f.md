# Installing Linux

In Linux, partitions are given a name based on the drive which they belong to. For example, the first partition on the drive `/dev/hda` is `/dev/hda1`, the second is `/dev/hda2`, and so on. If you have any logical partitions, they are numbered starting with `/dev/hda5`, `/dev/hda6`, and so on.

![](bbox=[0.07, 0.2, 0.18, 0.28])

> **WARNING**
> 
> With Linux `fdisk` or `cfdisk`, you should not create or delete partitions for operating systems other than Linux. That is, don't create or delete MS-DOS partitions with this version of `fdisk`; use MS-DOS's version of FDISK instead. If you try to create MS-DOS partitions with Linux `fdisk`, chances are MS-DOS will not recognize the partition and not boot correctly.

Here's an example of using `fdisk`. Assume you have a single MS-DOS partition using 61693 blocks on the drive, and the rest of the drive is free for Linux. (Under Linux, one block is 1024 bytes. Therefore, 61693 blocks is about 61 megabytes.) You'll create just two partitions in this tutorial example, swap and root. You should probably extend this to four Linux partitions in line with the recommendations above: one for swap, one for the root filesystem, one for system software, and a home directory area.

First, use the p command to display the current partition table. As you can see, `/dev/hda1` (the first partition on `/dev/hda`) is a DOS partition of 61693 blocks.

```
```
Command (m for help): p
  Disk /dev/hda: 16 heads, 38 sectors, 683 cylinders
  Units = cylinders of 608 * 512 bytes

  Device    Boot Begin  Start End   Blocks Id System
  /dev/hda1 *   1      203   61693 6  DOS 16-bit >32M

Command (m for help): 
```
```

Next, use the n command to create a new partition. The Linux root partition will be 80 megs in size.

```
```
Command (m for help): n
Command action
  e extended
  p primary partition (1-4)
  p
```
```

Here the system is asking if you want to create an extended or primary partition. In most cases you want to use primary partitions, unless you