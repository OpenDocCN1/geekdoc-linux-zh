Tip Hot swapping is the practice of replacing drives while the system is running. Its feasibility is limited. Never try to hot-swap an IDE drive; you could destroy the drive. SCSI drives might successfully swap, though most likely will not. IBM SCA drives can successfully swap. You can use the raidhotadd and raidhotremove commands to perform such a swap.

# RAID Example

Earlier in the chapter, Figure 31-1 showed a simple RAID configuration with three RAID devices using corresponding partitions on two hard disks for /boot, / (root), and /home partitions. The boot partition is configured as a RAID 1 device because systems can be booted only from a RAID 1 device, not RAID 5. The other partitions are RAID 5 devices, a more commonly used RAID access method.

You could set up such a system during installation, selecting and formatting your RAID devices and their partitions using Disk Druid. The steps described here assume you have your system installed already on a standard IDE drive and are setting up RAID devices on two other IDE disk drives. You can then copy your file from your standard drive to your RAID devices.

First you create the hard disk partitions using a partition tool like parted or fdisk. Then configure the three raid devices in the /etc/raidtab file.

```
raiddev /dev/md0
    raid-level        1
    nr-raid-disks     2
    nr-spare-disks    0
    persistent-superblock 1
    chunk-size        4
    device            /dev/hda1
    raid-disk         0
    device            /dev/hdc1
    raid-disk         1
```

```
raiddev /dev/md1
    raid-level        5
    nr-raid-disks     2
    persistent-superblock 1
    chunk-size        4
    parity-algorithm  left-symmetric
    device            /dev/hda2
    raid-disk         0
    device            /dev/hdc2
    raid-disk         1
```

```
raiddev /dev/md2
    raid-level        5
    nr-raid-disks     2
    persistent-superblock 1
    chunk-size        4
    parity-algorithm  left-symmetric
    device            /dev/hda3
    raid-disk         0
    device            /dev/hdc3
    raid-disk         1
```