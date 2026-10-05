# Disk devices for HP-UX

Linux doesn't have raw device files for disks or disk partitions, just use the block device wherever you might be accustomed to specifying a raw device.

parted -l lists the partition tables, model numbers, and manufacturers of every disk on the system.

# Disk devices for Solaris

> Solaris disk device names are of the form /dev/[r]disk/cWtXdYs, W is the controller number, X is the SCSI target number, Y is the SCSI local unit number (or LUN, almost always 0), and Z is the partition (slice) number. There are couple of subsets: ATA drives show up as cWdYs (with no t clause), and disks can have a series of DOS-style partitions, signed by pZ, and as the Solaris-type slices denoted by sZ.

These device files are actually just symbolic links into the /devices tree, where real device files live. More generally, Solaris makes an effort to give continuity to device names, even in the face of hardware changes. Once a disk has shown under a given name, it can generally be found at that name in the future unless you switch controllers or SCSI IDs.

By convention, slice 2 represents the complete, unpartitioned disk. Unlike Linux, Solaris gives you device files for every slice and partition, and whether not those slices and partitions actually exist. Solaris also overlapping partitions, but that's just crazy talk. Oracle may well ship Solaris system with a loaded gun.

Hot-plugging should work fine on Solaris. When you add a new disk, devfsadm detect it and create the appropriate device files for. If you need, you can run devfsadm.

# Disk devices for HP-UX

HP-UX has traditionally used disk device names patterned after those of Solaris, which record a lot of hardware-specific information in the device path. As of HP-UX 11i v3, those patterns however, have been deprecated in favor of "agile addresses" of the form /dev/disk/disk. The paths are stable and do not change with the details of the system's hardware configuration.

Before you use UNIX, you can obtain a listing of the system's SCSI devices from the PROM monitor. Unfortunately, the exact way in which this is varies among choices. After you boot, you can list disks by running ioscan.

```
sudo ioscan -Nfn -C disk
Class 1 H/W Driver S/W TypeDescription
=================================================================================
disk 3 64000/0xfa/00 esdisk CLAIMED DEVICE TEACVD-28-B
    /dev/disk/disk3 /dev/disk/disk3
disk 4 64000/0xfa/01 esdisk CLAIMED DEVICE HP 73.4GMAS3735NC
    /dev/disk/disk4 /dev/disk/disk4
    /dev/disk/disk4_p1 /dev/disk/disk4_p1
```