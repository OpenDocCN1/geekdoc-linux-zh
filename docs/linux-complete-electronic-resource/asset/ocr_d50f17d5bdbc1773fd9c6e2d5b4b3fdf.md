# ## Using Fdisk and Cfdisk

Your first installation step once the root-disk Linux is booted will be to create or edit the partition tables on your disks. Even if you used FDISK to set up partitions earlier, you’ll need to go back to the partition table and insert some Linux-specific information.

To create or edit Linux partitions, we’ll use the Linux version of the fdisk program or its screen-oriented sibling cfdisk.

Generally the installation program will look for a preexisting partition table and offer to run fdisk or cfdisk on it for you. Of the two, cfdisk is definitely easier to use, but current versions of it are also less tolerant of a nonexistent or garbled partition table.

Therefore you may find (especially if you’re installing on virgin hardware) that you need to start with fdisk to get to a state that cfdisk can deal with. Try running cfdisk; if it complains, run fdisk. (A good way to proceed if you’re building an all-Linux system and cfdisk complains is to use fdisk to delete all the existing partitions and then fire up cfdisk to edit the empty table.)

A few notes apply to both fdisk and cfdisk. Both take an argument that is the name of the drive on which you wish to create Linux partitions. Hard disk device names are

+   - `/dev/hda`  First IDE drive
+   - `/dev/hdb`  Second IDE drive
+   - `/dev/sda`  First SCSI drive
+   - `/dev/sdb`  Second SCSI drive

For example, to create Linux partitions on the first SCSI drive in your system, you will use or your installation program might generate from a menu choice) the command

```
```bash
cfdisk /dev/sda
```
```

If you use fdisk or cfdisk without an argument, it will assume `/dev/hda`.

To create Linux partitions on the second drive in your system, simply specify either `/dev/hdb` (for IDE drives) or `/dev/sdb` (for SCSI drives) when running fdisk.

Your Linux partitions don’t all have to be on the same drive. You might want to create your root filesystem partition on `/dev/hda` and your swap partition on `/dev/hdb`, for example. In order to do so just run fdisk or cfdisk once for each drive.