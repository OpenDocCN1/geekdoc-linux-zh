# Chapter 2: Installing Fedora 71

The fdisk command is one that is available on many different operating systems (although it looks and behaves differently on each). In Linux, fdisk is a menu-based command. To use fdisk to list all partitions, type the following (as root user):

```
# fdisk -l
Disk /dev/sda: 40.0 GB, 40020664320 bytes
255 heads, 63 sectors/track, 4865 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
```

To see how each partition is being used on your current system, type the following:

```
# df -h
Filesystem Size Used Avail% Mounted on
/dev/sda 37G 5.4G 30G 16% /
/dev/sda1 99M 8.6M 81M /boot
none 61M 0% /dev/shm
```

From the output of df, you can see that the root of your Linux system (/) is on /dev/sda2 partition and that the /dev/sda partition is used for /boot.

> CAUTION: Before using fdisk to change your partitions, I strongly recommend running the df -h command to see how your partitions are currently being defined. This will help reduce the risk of changing or deleting the wrong partition.

To use fdisk to change your partitions, begin (as root user) by typing:

```
# fdisk device
```

where fdisk is replaced by the name of the device you want to work with. For example, here are some of choices:

+   - /dev/sda — For the first IDE or SCSI hard disk; sdb, sdc, and so on for other SCSI disks. (For Fedora 10, IDE hard no longer appear as hda, hdb, and so on.)
- /dev/md0 — For a RAID device.

After you have started fdisk, type m to see the options. Here is what you can do with fdisk:

+   - Delete a partition — Type d and you are asked to enter a partition number on the current hard disk. Type the partition number and press Enter. For example, /dev/sda2 would be partition number 2. (The deletion won't take effect until you write the change. Until then, it's not too late to back out.)