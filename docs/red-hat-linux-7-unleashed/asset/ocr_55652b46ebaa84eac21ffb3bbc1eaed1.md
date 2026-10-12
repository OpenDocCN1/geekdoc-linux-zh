# # Installing and Configuring LILO

You should know where your Linux partition is before LILO is installed. You should also know if and where other operating systems are installed. For example (using the Linux `df`, or disk file usage command), partitions may appear as

```
$ df
```

```
Filesystem  1k-blocks  Used Available Use% Mounted on
/dev/hda5  6079464  2168440 3602200  38% /
/dev/hda1   21929   2421    18376   12% /boot
```

This simple example, typical of a single hard disk system, shows that the Linux `/boot` partition is installed on `/dev/hda1`, with the rest of the Linux filesystem resident on `/dev/hda5` (there are other partitions present, such as swap and hibernation, but only those recognized are displayed). Here, LILO is installed in the Master Boot Record (MBR) of `/dev/hda`. Here is another example, using the output of the `fdisk` command's print partition table option:

```
```
Disk /dev/hda: 240 heads, 63 sectors, 1559 cylinders
Units = cylinders of 15120 * 512 bytes

Device Boot    Start   End  Blocks   Id System
/dev/hda1 *      1     218 1648048+ c  Win95 FAT32 (LBA)
/dev/hda2          219   1559 10137960 5 Extended
/dev/hda5          219   221 22648+ 83 Linux
/dev/hda6          222   499 210148+ 83 Linux
/dev/hda7          500   534 264568+ 82 Linux swap
/dev/hda8          535   881 2623288+ 83 Linux
/dev/hda9          882   1559 5125648+ 83 Linux
```
```

In this example, the Linux filesystem is installed across several partitions, such as `/dev/hda5`, `/dev/hda6`, `/dev/hda8`, and `/dev/hda9`. Although not obvious, these partitions correspond to `/boot`, root (`/`), and two additional volumes, with Windows installed on `/dev/hda1`. Again, LILO is installed in the MBR of `/dev/hda`, although it could also be installed in `/dev/hda9`.

If Linux is the only operating system on your computer or if you already have Windows installed, install LILO as the MBR of the boot drive. If you have OS/2 also, you will want to install LILO on the root partition of your hard drive and use OS/2's bootloader on the MBR to boot different operating systems.