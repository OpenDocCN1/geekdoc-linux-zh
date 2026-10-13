Be sure to specify the persistent superblock option to have your RAID devices automatically detected when you boot.

+   4. Create your RAID device with `mkraid`.
+   5. Activate the RAID device with `raidstart`.
+   6. Create a file system on the RAID device (`mkfs`) and then mount it.

# Table 31-2: RAID Tools

| Tool | Description |
|------|-------------|
| `mkraid` | Creates (configures) RAID devices from a set of block devices, initializing them. |
| `raidstart` | Activates RAID devices. |
| `raid0start` | Activates older nonpersistent linear and RAID 0 RAID devices. |
| `raidstop` | Turns off a RAID device. |

# Creating Hard Disk Partitions: fd

To add new RAID devices or to create them in the first place, you need to manually create the hard disk partitions they will use, and then configure RAID devices to use those partitions. To create a hard disk partition for use in a RAID array, use `fdisk` or `parted` and specify `fd` as the file system type. You invoke `fdisk` or `parted` with the device name of the hard disk you want to create the partition on. Be sure to specify `fd` as the partition type. The following example invokes `fdisk` for the hard disk `/dev/hdb` (the second hard disk on the primary IDE connection):

`fdisk /dev/hdb`

Though technically partitions, these hard disk devices are referred to as disks in RAID configuration documentation and files.

# Configuring RAID: /etc/raidtab

Once you have your disks, you then need to configure them as RAID devices. RAID devices are configured in the `/etc/raidtab` file. This file will be used by the `mkraid` command to create the RAID device. In the `/etc/raidtab` file, you create a `raiddev` entry for each RAID device, and specify which disks they will use along with any RAID options. For a `raiddev` entry, you specify the name of the RAID device you are configuring, such as `/dev/md0` for the first RAID device.

`raiddev /dev/md0`

You then specify the level for the RAID device, such as 0, 1, or 5 using the keyword `raid-level` followed by the RAID level number. Then add any options you may need along with the list of disks making up the RAID array. A disk is defined with the `device` entry, and its position in the RAID array, with the `raid-disk` option. The configuration directives and options are listed in Table 31-3. A sample entry for the `/etc/raidtab` file is shown here:

```
raiddev /dev/md0
  raid-level          5
  nr-raid-disks       3
  nr-spare-disks      1
  persistent-superblock 1
  chunk-size          4
  parity-algorithm    left-symmetric
  device              /dev/hdb1
  raid-disk           0
  device              /dev/hdc1
```