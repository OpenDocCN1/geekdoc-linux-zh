
scheme used by most hardware and operating systems is *GUID Partition Tables* (GPT). Each scheme has its own requirements for boot blocks, hardware architecture, and partitions. This book discusses the MBR and GPT schemes, but you should be aware that other schemes exist.

Each disk partition gets its own device node, created by adding something to the end of the underlying device node name. Here, I look at the device node for a default FreeBSD install using UFS on a virtual disk:

```
# ls /dev/vtbd0*
/dev/vtbd0	/dev/vtbd0p1	/dev/vtbd0p2	/dev/vtbd0p3
```

We have a device node for the disk itself and then three others ending in p1, p2, and p3. What are those subdivisions? The *p* indicates that they're GPT partitions. In a default install, p1 is the boot partition, p2 is the swap space, and p3 is the main filesystem.

Each partitioning scheme has its own device node extensions. We'll read about those later this chapter.

## The Filesystem Table: /etc/fstab

FreeBSD, like most Unix-like operating systems, uses the file system table */etc/fstab* to map on-disk partitions to filesystems and swap space. While ZFS doesn't use */etc/fstab*, every other FreeBSD filesystem can appear therein. Each partition in use appears on a separate line, along with mounting and management instructions.

```
/dev/gpt/rootfs	/		uifs	rw	2	1
/dev/gpt/swapfs	none		swap	sw	0	0
proc			/proc		procfs	rw	0	0
```

The first field gives the GEOM provider name. This might be a physical disk partition such as */dev/ada0p1* or perhaps a partition of a GEOM device node. The first two lines here offer device nodes under */dev/gpt*. They're GPT labels, which we'll see later this chapter. Our third entry lists the word *proc* rather than a device node: it's the procfs(5) virtual filesystem, which we'll examine in Chapter 13.

The second field gives the directory where the filesystem is available, called the *mount point*. Every partition you can read or write files on is attached to a mount point, such as /usr, /var, and so on. A few special partitions, such as swap space (line 2 here), have a mount point of none. You can't read or write usable files to the swap space because they're not attached to the directory tree and because the system would overwrite those files when it swapped.

Next, we have the filesystem type. The first line shows a type of ufs, or Unix File System. The second line is defined as swap space, while the third is type proofts. Other types include cd9660 (CD disks or images), nfs (Network File System mounts), and ext4fs (Linux filesystems). The filesystem table tells FreeBSD how to mount this partition. Chapter 13 discusses alternate filesystems.

The fourth field shows the mount(8) options used for this particular partition. Each filesystem has its own mount options, but here are a few that multiple filesystems use and that frequently appear in /etc/fstab:

- **ro** The filesystem is mounted read-only. Not even root can write to it.
- **rw** The filesystem is mounted read-write.
- **noauto** FreeBSD won't automatically mount the filesystem, neither at boot nor when using mount -a. This option is useful for removable media drives that might not have media in them at boot.

The fifth field is used to tell dump(8) what backup level is needed to back up this filesystem. Dump is largely obsolete these days; people perform file-level backup with tar(1) or use more advanced backup software, like Bacula (http://www.bacula.org/) or TarSnap (https://www.tarsnap.com/).

The last field tells the FreeBSD boot process when to check filesystem integrity. All the partitions with the same number get checked in parallel with fsck(8). The root filesystem gets marked with a 1, meaning it's checked first. Only the root filesystem should get a 1. Any other partitions should get a 2 or higher, meaning they get checked later. Swap, read-only media, and logical filesystems don't require integrity checking, so they get set to 0.

FreeBSD configures all filesystems found in /etc/fstab at boot. As the system runs, though, the sysadmin can mount other filesystems. And she can unmount ones listed there. That leads to our next question...

## What's Mounted Now?

If not all filesystems are mounted automatically at boot, and if the sysadmin can add and remove mounted filesystems, how can you determine what's mounted right now? Use mount(8) without any options to see all mounted filesystems.

```
# mount
/dev/gpt/rootfs on / (ufs, local, journaled soft-updates)
/devfs on /dev (devfs, local, multilabel)
```

This is a small UFS-based host. It has one disk partition and an instance of devfs(5) (see Chapter 13). The word local means that the partition is on a hard drive attached to this machine. The journaled soft-updates option is a UFS feature we'll discuss in Chapter 11. If you're using NFS or SMB to mount partitions, they'll appear here.

More complicated hosts give larger results:

```
# mount
base/ROOT/default on / (zfs, local, noatime, nfs4v4aclcs)
base/tmp on /tmp (zfs, local, noatime, nosuid, nfs4v4aclcs)
base/usr/home on /usr/home (zfs, local, noatime, nfs4v4aclcs)
base/usr/ports on /usr/ports (zfs, local, noatime, nosuid, nfs4v4aclcs)
procfs on /proc (procfs, local)
devfs on /dev (devfs, local, multilabel)
--snip--
```

This host uses many ZFS datasets, each with its own mount point. The mount(8) output shows selected ZFS options, such as noatime and nfs4v4aclcs.

At the end of this output, we have a procfs(5) entry and one for a devfs(5) mount. A working FreeBSD system needs devfs mounted at /dev or it won't work very well or for very long.

## Disk Labeling

At the lowest level, operating systems identify disks by their physical attachment to the system. Traditionally, the filesystem table says something like, “Use the disk attached at ATA port 3 as the /var/log filesystem.” This worked fine with less flexible hardware, but as hardware technology improved, such connections became much more flexible. If you assign drive roles based on the physical attachment, sometimes that attachment changes. I’ve had more than one mainboard explode at an inconvenient hour, forcing a desperate emergency replacement. Tracking which cable goes to which connector under such circumstances never goes well. In older versions of FreeBSD, you needed to “wire down” devices so that a specific disk always showed up as a specific device node. This is no longer needed.

Today, a sysadmin uses on-disk labels to refer to the disk by something other than the physical attachment. A label identifies an instance of a geom. Rather than telling FreeBSD that /var/www is on the disk attached to SATA port 2, you declare that /var/www is on the disk labeled website. While the former easily goes wrong, the latter is mostly immune to sleepy hardware techs. One disk can have several labels simultaneously, if they’re different types of label. FreeBSD automatically derives many labels from inherent disk characteristics; the sysadmin can define others.

Most label types have a dedicated device node directory. Each GPT partition has a globally unique identifier (GUID), and the autcreated labels for those partitions live in /dev/gptid. Disks get unique disk IDs based on their serial number, which gets entries in /dev/diskid. Manually created GPT labels appear in /dev/gpt.

Use these labels as you would any other device name. If you label the disk ada5 as stuff1, you can partition the disk stuff into stuff1p1 and stuff1p2, use those partitions in configuration files, and more.

Not all labels come from GEOM. ZFS uses its own internal labeling method for filesystems and pools. You can also add labels to UFS filesystems.

Don’t let swapped SATA cables ruin your weekend. Label everything.

## Viewing Labels

View labels with `glabel(8)`, a shortcut for `geom` `label`. Here are parts of a label from a small virtual machine. The labels on real hardware can quickly become very complex.

```
$ glabel list
   1 Geom name: ada0p1
 Providers:
   2 1. Name: gptid/b9c0c7c5-5b66-11e7-8aec-080027739ff6
  Media size: 524288 (512K)
  Sectorsize: 512
  --snip--
   3 Consumers:
    1. Name: ada0p1
      Mediasize: 524288 (512K)
      Sectorsize: 512
      Stripesize: 0
      Stripeoffset: 20480
      Mode: r0w0e0
```

This host has a single geom **①** on the disk partition `/dev/ada0p1`. It provides an appallingly long label based on the GPT partition ID **②**. We’ll see a bunch of information on the underlying disk, such as the number of sectors on the disk, the sector size, and other information you might see in `geom disk list` output. This information comes from the partition, however. The physical drive information is passed up from the underlying disk.

This drive has a single consumer **③**, the actual underlying partition. We’re at the very bottom of this simple GEOM stack, right up against the disk, so it’s consuming itself. If you add cryptographic layers or software RAID, you’ll see what other device this geom consumes.

## Sample Labels

Here are some examples of the kinds of labels you’ll see on most FreeBSD systems.
