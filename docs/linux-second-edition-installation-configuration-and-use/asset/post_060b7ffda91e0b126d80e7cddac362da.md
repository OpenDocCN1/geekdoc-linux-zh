
# FILE SYSTEM ADMINISTRATION 153

If you now access data in /usr/local, the link points to /localpart, that is, to the new partition. These links are transparent, and you will not notice while working normally. Again, you must make an addition to fstab in the file system at the point /localpart at every system start-up:

```
# Addition to /etc/fstab
# Mount /dev/sdc3 as /localpart into the file system
/dev/sdc3        localpart       defaults       0 2
```

In principle, you can transfer any number of directories in this way. However, make sure that the access rights are kept the same. In newly created directories or links, you may have to use chown to change owners or chmod to change the access bits.

# Mounting DOS, Windows, and OS/2 partitions

Under Linux, you can also access DOS, Windows, and OS/2 partitions. For the DOS file system, obviously all restrictions apply (file names with a maximum of 8+3 characters, no links). For Windows, currently - that is, in kernel 2.2 - the file systems of Windows 9x (including FAT32) and Windows NT 4 are supported. NT file systems can however, are only read (but not modified). For OS/2 partitions too, access is limited to read-only.

Depending on who is allowed to access the DOS partition, you must use the gid, uid, and umask options in fstab (see above). If you need to access DOS partitions only from time to time, you can specify the noauto option in the fstab entry. This has the advantage that mount /mnt/dos can be executed easily without specifying any additional options. On the other hand, the DOS partition is not mounted automatically all the time, which is a small safety risk (as with any other partition).

The necessary additions to fstab look as follows (again, you must substitute the device names and directories used in your system):

```
# Addition to /etc/fstab
# Mount DOS partition /dev/hda5 as /mnt/dos into the file system
/dev/sda5        /mnt/dos       defaults       0 0
# If read-only (no writing) is required
/dev/sda6        /mnt/dos        ro             0 0
# Windows 9x partition
/dev/sda7        /mnt/win95      vfat           0 0
# Windows 9x partition, free rw access for all users
/dev/sda8        /mnt/win95-rw  vfat           umask=111     0 0
# Windows NT partition
/dev/sda9        /mnt/nt         ntfs           defaults       0 0
# OS/2 partition
/dev/hda10       /mnt/os2        hpfs           defaults       0 0
```

# Mounting a CD-ROM drive

There is not much difference between mounting hard partitions and mounting CD-ROM drives. The latter are normally mounted into the file system at the points /mnt/cdrom or /cdrom. Instead of /dev/hdb, you must specify the device name of your own CD-ROM drive.

```
# Addition to /etc/fstab
# Mount CD-ROM drive as /cdrom into the file system
/dev/cdrom      iso9660  ro,user,noautopt  0 0
```

The option means that no data can be modified on the CD-ROM drive (read only). user allows every user (not only root) to mount and unmount the CD-ROM drive with mount and umount (but only when required). noautopt ensures that the CD-ROM is not automatically mounted into the file system at start-up. /dev/hdb, you must specify /dev/hdc or /dev/hdd, if the CD-ROM drive is connected to the second controller.

The device names for the different types of CD-ROM are listed on page 102. When changing CDs, you must execute mount and unmount to make Linux aware of the modified file system (see page 103). You can only access your CD-ROM drive if you use a kernel that has a built-in support for your particular type of CD-ROM drive.

Since kernel 2.2 (precisely, since later 2.0.x) Linux recognizes Juliet CDs. CD-ROMs are for Windows 95/NT with long file names. Although these CD-ROMs comply with the ISO-9660 standard, they do not employ the ridge extension commonly used under Unix, the Juliet extension for representation of long file names introduced by Microsoft. If you are using an older kernel, you can still use CD-ROMs, but you will only see the short forms of the file names.

If you want to mount a Linux CD and immediately execute programs without it, you need to use the mount option exec. Normally, execution of programs from a CD-ROM is protected for security reasons.

```
root# mount -o exec /cdrom
```

# Mounting swap partitions

The creation of a swap partition is usually carried out within the framework of the installation of Linux. If this has not happened, you need a dedicated hard disk partition, which can be created using the fdisk command. T must be used to change the partition type from 83 (Linux) to 82 (Linux). After the partition has been formatted with mkswap it can be activated with swapon.

If the swap partition is to be used automatically at startup of Linux, the hard disk partition must be entered into fstab:

```
# Addition to /etc/fstab
# Mount swap partition
/dev/sdc6 none swap sw 0 0
```

# Mounting a swap file

The creation of a swap file is, strictly speaking, just an expedient. Accessing a swap file is considerably slower than accessing a swap partition. The only advantage of a swap file is that it can be created without repartitioning the hard disk.

Swap files are normally created in the /dev directory. The first step consists of using the dd command to create an empty file with a specified size. The data source is /dev/zero, a device out which any number of zero bytes can be read. The size is specified in blocks, with the block size set to 1024. Subsequently, the swap file is formatted with mswap and activated with swapon. The following example creates a small swap file of about 1 Megabyte.

```
root# dd bs=1024 if=/dev/zero of=/dev/swapfile count=1000
1000+ records in
1000+ records out
root# mswap /dev/swapfile 1000
Setting swapspace, size = 1019904 bytes
root# sync
root# swapon /dev/swapfile
```

The swap file can be entered in fstab:

```
# Addition to /etc/fstab
# Mount swap file
/dev/swapfile none swap sw 0 0
```

# Hard disk tuning

This section is explicitly addressed to Linux. It shows two ways in which — depending on the hardware — access speed can be increased. The first variation — use of called bus master mode — is of interest for all users. The second variation — distribution of data across partitions.

# Bus DMA mode

The bus DMA mode allows a particularly efficient data transfer between hard disk and main memory. Transfer is not byte by byte via the CPU, but via DMA (Direct Memory Access) channel. The advantages of bus DMA mode are obvious: the data rate is significantly higher; at the same time, CPU load for loading/saving large files is reduced.

For you to be able to use the DMA mode, both your motherboard and hard disk must support this mode. With regard to motherboard support, you are advised to read the corresponding manual and check the kernel messages displayed during booting:

```
root# dmesg
PIX4: IDE controller on PCI bus 00 dev 21
PIX4: 100% native mode; will probe irqs later
ide0: B-DMA at 0xc800-0xc807, BIOS settings: hdc:DMA, hdd:pio
ide1: B-DMA at 0xc808-0xc8ff, BIOS settings: hdc:DMA, hdd:pio
```

Whether your hard disk supports DMA transfer can easily be found out by the first IDE hard disk:

```
root# hdparm -i /dev/hda
...
DMA=yes, maxDMA=2(fast)
```

A prerequisite is the availability of the corresponding kernel module. (Kernels supplied with current distributions fulfill this requirement. In other distributions, you may need to recompile the kernel, setting the Intel 82371 PIIX DMA support option in the Floppy/IDE other block device option group to Y or M.)

> CAUTION Even if all three requirements are met, the DMA mode is often not activated automatically for safety reasons; depending on the chip set, the length of the hard disk (according to the specification, a maximum length of 45 cm is allowed), and so on. the DMA mode may lead to reliability problems. For this reason, DMA mode experiments should be carried out with extreme care: execute upon for all partitions that are not needed! Ideally, you should have a separate partition available for your DMA tests which does not contain any valuable or unsaved data.

Whether the DMA mode is already active can be determined with hdparm -d /dev/hda-
root# /dev/hda:
using_dma = 0 (off)
