
Linux doesn't have raw device files for disks or disk partitions, so just use the block device wherever you might be accustomed to specifying a raw device.

parted -l lists the sizes, partition tables, model numbers, and manufacturers of every disk on the system.

## Disk devices for Solaris

Solaris disk device names are of the form /dev/[r]dsk/cWtXdYsZ, where W is the controller number, X is the SCSI target number, Y is the SCSI logical unit number (or LUN, almost always 0), and Z is the partition (slice) number. There are a couple of subtleties: ATA drives show up as cWdYsZ (with no t clause), and disks can have a series of DOS-style partitions, signified by pZ, as well as the Solaris-style slices denoted by sZ.

These device files are actually just symbolic links into the /devices tree, where the real device files live. More generally, Solaris makes an effort to give continuity to device names, even in the face of hardware changes. Once a disk has shown up under a given name, it can generally be found at that name in the future unless you switch controllers or SCSI target IDs.

By convention, slice 2 represents the complete, unpartitioned disk. Unlike Linux, Solaris gives you device files for every possible slice and partition, whether or not those slices and partitions actually exist. Solaris also supports overlapping partitions, but that's just crazy talk. Oracle may as well ship every Solaris system with a loaded gun.

Hot-plugging should work fine on Solaris. When you add a new disk, devfsadmd should detect it and create the appropriate device files for you. If need be, you can run devfsadm by hand.

## Disk devices for HP-UX

HP-UX has traditionally used disk device names patterned after those of Solaris, which record a lot of hardware-specific information in the device path. As of HP-UX 11i v3, however, those pathnames have been deprecated in favor of "agile addresses" of the form /dev/disk/disk1. The latter paths are stable and do not change with the details of the system's hardware configuration.

Before you boot UNIX, you can obtain a listing of the system's SCSI devices from the PROM monitor. Unfortunately, the exact way in which this is done varies among machines. After you boot, you can list disks by running ioscan.

```
$ sudo ioscan -fnn -C disk
Class    I   H/W Path        Driver   S/W State   H/W Type Description
================================================================================
disk     3  64000/0xfa00/0x0  esdisk   CLAIMED    DEVICE    TEACDV-28E-B
          /dev/disk/disk3     /dev/rdisk/disk3
disk     4  64000/0xfa00/0x1  esdisk   CLAIMED    DEVICE    HP 73.4GMAS3735NC
          /dev/disk/disk4     /dev/rdisk/disk4
          /dev/disk/disk4_p1  /dev/rdisk/disk4_p1
/dev/disk/disk4_p2    /dev/rdisk/disk4_p2
/dev/disk/disk4_p3    /dev/rdisk/disk4_p3
disk 5 64000/0xf00/0x2 esdisk CLAIMED DEVICE HP 73.4GMAS3735NC
/dev/disk/disk5        /dev/rdisk/disk5
/dev/disk/disk5_p1     /dev/rdisk/disk5_p1
/dev/disk/disk5_p2     /dev/rdisk/disk5_p2
/dev/disk/disk5_p3     /dev/rdisk/disk5_p3
```

The old-style device names are still around in the /dsk and /rdsk directories, and you can continue to use them if you wish—at least for now. Run ioscan -m dsf to see the current mapping between old- and new-style device names.

```
hp-ux% ioscan -m dsf
Persistent DSF*          Legacy DSF(s)
=================================  ===================
/dev/rdisk/disk3        /dev/rdsk/c0t0d0
/dev/rdisk/disk4        /dev/rdsk/c2t1d0
/dev/rdisk/disk4_p1     /dev/rdsk/c2t1d0s1
/dev/rdisk/disk4_p2     /dev/rdsk/c2t1d0s2
/dev/rdisk/disk4_p3     /dev/rdsk/c2t1d0s3
/dev/rdisk/disk5        /dev/rdsk/c2t0d0
/dev/rdisk/disk5_p1     /dev/rdsk/c2t0d0s1
/dev/rdisk/disk5_p2     /dev/rdsk/c2t0d0s2
/dev/rdisk/disk5_p3     /dev/rdsk/c2t0d0s3
```

Note that partitions are now abbreviated p instead of s in the Solaris manner (for "slice"). Unlike Solaris, HP-UX uses names such as disk3 with no partition suffix to represent the entire disk. On Solaris systems, partition 2 represents the whole disk; on HP-UX, it's just another partition.

The system from which this example comes is Itanium-based and so has disk partitions. Other HP systems use logical volume management instead of partitioning.

## Disk devices for AIX

AIX's /dev/hdiskX and /dev/rhdiskX paths are refreshingly simple. Disk names are unfortunately subject to change when the hardware configuration changes. However, most AIX disks will be under logical volume management, so the hardware device names are not that important. The logical volume manager writes a unique ID to each disk as part of the process of inducting it into a volume group. This labeling allows the system to sort out the disks automatically, so changes in device names are less troublesome than they might be on other systems.

You can run lsdev -C -c disk to see a list of the disks the system is aware of.

## Formatting and bad block management

All hard disks come preformatted, and the factory formatting is at least as good as any formatting you can do in the field. It is best to avoid doing a low-level format if it's not required. Don't reformat new drives as a matter of course.
