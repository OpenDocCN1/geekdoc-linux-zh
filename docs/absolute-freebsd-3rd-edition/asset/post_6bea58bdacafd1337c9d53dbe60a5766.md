
### BSD Labels

three of those slices have no sectors assigned to them. While the MBR format supports a linked list of up to 20 extended partitions, FreeBSD doesn’t need them thanks to BSD labels.

One of the four primary slices is considered active. When the system powers on, the bootstrap code looks for the active slice and tries to boot it.

The MBR sector also contains bootstrap code. You don’t need to allocate space specifically for a boot loader. In FreeBSD, the bootstrap code finds and executes the kernel. FreeBSD includes two different boot loaders, *mbr* and *boot0*. The mbr loader is for a host with a single operating system. If you have multiple operating systems installed on your hardware, use the boot0 loader—or, better still, dedicate your host to FreeBSD and virtualize the other operating systems.

The main function of a slice is to contain a *bsdlabel*(8) partition.

BSD existed before either the MBR or the IBM PC. BSD used its own disk partition format, called a *disklabel*. Now that labeling disks is much more common, disklabels are also called *BSD labels* or *bsdlabels*. (If you want to start a spirited discussion, ask a room of FreeBSD developers which is more correct.) BSD systems had several partitions including at least / *(root)*, / *usr*, / *var*, / *tmp*, and swap space, plus separate partitions for whatever actual work the system did.

When BSD was ported to the i386 platform, they could have switched disks to using MBR partitions. With extended MBR partitions, one disk could have had up to 24 partitions. Disklabel partitions were embedded throughout the kernel, however, often in icky places that nobody dared touch. The porting group decided to treat an MBR slice as a BSD disk and to partition each slice with a BSD disklabel. Sysadmins needed to create MBR partitions and then nest disklabel partitions inside those MBR partitions.

This worked but also made the word *partition* ambiguous. Does *partition* mean an MBR partition or a disklabel partition? FreeBSD dusted off the word *slices* for MBR partitions. Each MBR slice will have its own disklabel, listing the BSD partitions contained within the slice. If you come from a Linux or Microsoft Windows background, the MBR partitions you're familiar with are called slices over here.

You can't label slices or disklabel partitions. These formats have no space for labels. Instead, label the ZFS or UFS filesystem on the partition.

It's possible to skip slicing a disk, instead installing a disklabel directly on the hard drive. Some hardware refused to boot from such disks, so they're called dangerously dedicated. With the advent of GPT, dangerously dedicated disks aren't really used any more.

### MBR Device Nodes

Every disk, slice, and partition has a device node. The slice device node is an extension of the underlying disk, and the partition device node is an extension of the device's node. Here are the device nodes on disk ada0 of an MBR-based system:

| | | |
|:---|:---|:---|
| /dev/ada0 | /dev/ada0s1a | /dev/ada0s1d |
| /dev/ada0s1 | /dev/ada0s1b | /dev/ada0s1e |

The first subdivision of the disk is the slice. Device nodes indicate a slice with the letter s and a number from 1 to 4. The first slice is s1, the second is s2, and so on. Unused MBR partitions don't get device nodes. Here, /dev/ada0s1 is slice 1 on the disk.

The second layer of subdivision is the disklabel partition inside the slice. Each partition has a unique device node name created by adding a letter to the slice's device node. Here, we have four disklabel partitions, /dev/ada0s1a through /dev/ada0s1e. Traditionally, the node ending in a (/dev/ada0s1a) is the root partition, while the node ending in b (/dev/ada0s1b) is swap space.

Note that the list of device nodes doesn't use the letter c. The c partition represents the entire slice. These days, you run disk partitioning tools on the slice entry rather than the disklabel for the slice.

Assign partitions d through h any way you like. A default disklabel can have up to seven usable partitions. With up to four slices on each drive, you can have up to 28 partitions on a drive. A disklabel can support up to 20 partitions, but you must indicate you want extra partitions when first creating the label.

### MBR and Disklabel Alignment

Slices have their own disk sector and filesystem block alignment issues. Traditionally, MBR partitions end on a cylinder boundary. Cylinder boundaries don't mean anything on modern hardware, but even newer drives provide them as a comforting lie for older or less capable hardware. If you create MBR partitions that don't end on a cylinder boundary, and you put that disk in a machine that requires respecting cylinder boundaries, the machine will have some sort of nervous breakdown. A disk you slice today could theoretically find its way into an older system. FreeBSD therefore arranges slices so that they end on cylinder boundaries. Cylinder boundaries not only can but probably do conflict with 4K disk sector sizes. If nothing else, the MBR itself takes up the first cylinder, or sixty-three 512-byte sectors!

Fortunately you rarely write to slice tables, and the performance of writing slice tables is rarely an issue. If you align your disklabel partitions within a slice to 1MB boundaries, you'll lose a few sectors between the slice partition table and the disklabel partition, but you'll have proper performance.

So: align disklabel partitions. Don't align slices.

### Creating Slices

Use *gpart*(8) to manage MBR slices. To create a slice, you need a partition type and a size. FreeBSD slices use type *freebsd*. If you don't specify a size, *gpart*(8) uses all available space. On an empty disk, this dedicates the whole disk to a single slice.

Here, I erase the existing partitioning, tell the disk to use the MBR scheme, and create a single FreeBSD slice:

```
# gpart destroy -F ada3
# gpart create -s mbr ada3
# gpart add -t freebsd ada3
ada3s1 added
```

Run *gpart show* and you’ll see that this disk now has a single slice. Add the *-p* flag to see the slice’s device node.

```
# gpart show -p ada3
=>        63      1953525105        ada3      MBR      (932G)
            63      1953525105        ada3s1    freebsd  (932G)
```

Our slice ada3s1 is now ready for disklabel partitions. To create multiple slices, specify a size with *-s*. A common configuration for small embedded systems is to put three slices on a disk. Two smaller slices contain different versions of the operating system, while the third contains any data. Here, I divide this 1TB disk into two 150GB slices and give the rest to a third slice:

```
# gpart add -s 150g -t freebsd ada3
ada3s1 added
# gpart add -s 150g -t freebsd ada3
ada3s2 added
# gpart add -t freebsd ada3
ada3s3 added
```

### Removing Slices

Use *gpart delete* to remove unwanted slices. Give the slice number with *-i*. Here, I remove the third, larger slice from our multislice disk created in the last section:

```
# gpart delete -i 3 ada3
ada3s3 deleted
```

### Activating Slices

The active slice is the one that the BIOS tries to boot. Set the active slice with the *-a active* flag. Use *-i* to give the number of the active slice.

```
# gpart set -a active -i 1 ada3
```

Change which slice gets booted by setting a different active slice.

The boot disk also needs a boot loader. While the MBR boot loader is different from the GPT or UEFI boot loaders, it uses the same *gpart*(8) *-b* flag. FreeBSD provides a copy of the MBR boot loader as /boot/mbr.

```
# gpart bootcode -b /boot/mbr ada3
```

Slice 1 on disk ada3 is now bootable. Now that you’ve sliced your disk, you can create BSD labels inside the slices.

### BSD Labels

Creating BSD label (or disklabel) partitions inside a slice is much like creating slices or GPT partitions. You must tell the storage device the scheme to be used, create and remove partitions until you’re satisfied with them, and install a boot loader.

#### Creating a BSD Label

Where GPT and MBR specifically provide space for partition tables, you must create a BSD label and write it to the beginning of the slice. As with any scheme, use *-s* and the name of the scheme. Install this scheme on the slice, not on the disk.

Suppose you want to create a BSD label on the slice ada3s1. Use the BSD scheme.

```
# gpart create -s bsd ada3s1
ada3s1 created
```

This is a default disklabel, with room for 8 disklabel partitions. You can increase the number of partitions, up to 20, by using the *-n* flag. Here, I create a whole bunch of partitions on ada3s3, the large partition.

```
# gpart create -n 20 -s bsd ada3s3
ada3s3 created
```
