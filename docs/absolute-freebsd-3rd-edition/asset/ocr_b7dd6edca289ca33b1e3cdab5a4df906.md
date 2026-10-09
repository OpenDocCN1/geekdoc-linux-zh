```
zroot   capacity        0%
 zroot   health         ONLINE           -
 zroot   guid           7955546176707282768      default
 ---snip---
```

Some of this information gets pulled into commands like `zpool status` and `zpool list`. You can also query for individual properties across all pools by using the property name.

```
# zpool get readonly
NAME     PROPERTY   VALUE    SOURCE
zroot    readonly   off      -
jail     readonly   off      -
scratch  readonly   off      -
```

Unlike dataset properties, most pool properties are set when you create or import the pool.

# Virtual Devices

A virtual device (VDEV) is a group of storage devices. You might think of a VDEV as a RAID container: a big RAID-5 presents itself to the operating system as a huge device, even though the sysadmin knows it’s really a bunch of smaller disks. The virtual device is where ZFS’s magic happens. You can arrange pools for different levels of redundancy or abandon redundancy and maximize space.

ZFS’s automated error correction takes place at the VDEV level. Everything in ZFS, from znodes (index nodes) to data blocks, is checksummed to verify integrity. If your pool has sufficient redundancy, ZFS will notice that data is damaged and restore it from a good copy. If your pool lacks redundancy, ZFS will notify you that the data is damaged and you can restore from backup.

A zpool consists of one or more identical VDEVs. The pool stripes data across all the VDEVs, with no redundancy. The loss of a VDEV means the loss of the pool. If you have a pool with a whole bunch of disks, make sure to use redundant VDEVs.

# VDEV Types and Redundancy