# Starting installation

If you own a modern motherboard/or BIOS, installation starts directly from the CD-ROM. If this is not the case, take a look at your BIOS settings; maybe booting from CD-ROM is deactivated.

If direct installation from CD-ROM does not work, you will need to create installation diskettes. Under DOS, or in a DOS window over Windows, you execute the following command (where X stands for the drive letter of your CD-ROM drive).

+   > X:\TOOLS\WRITE1\WRITE2 -f X:\BOOT\RESC1440.BIN -d A:

If you already have a Linux system installed, you can obviously create the two diskettes under Linux:

```
root# dd if=/cdrom/boot/resc1440.bin of=/dev/0 bs=1440k
```

# Basic installation

First Linux kernel and then the installation program are automatically started. Subsequently, you work your way through all relevant items of the main menu, with the installation program automatically proposing the (presumably) most reasonable next item, you need not stick to these suggestions.

# CONFIGURE KEYBOARD

Here you can select a keyboard table for support of a non-English keyboard (xx-latin1, where xx stands for the required language).

# PARTITION HARDDISK

In contrast to most other distribution, Debian makes use of cfdisk instead of fdisk for partitioning the hard disk. Handling of this program is significantly easier than fdisk. Do not forget to write down the device names of the new partition(s)!

![](bbox=[0.48, 0.616, 0.595, 0.63])

Disk Drive: /dev/hda
Hads: 128 Sectors per Track: 63 Cylinders: 787

| Name | Flags | Part Type | FS Type | Size (MB) |
|---|---|---|---|---||
| /dev/hda1 | Boot | Primary | DOS FAT16 | J | 303.19 |
| /dev/hda5 | | Logical | DOS FAT16 IDE-DATA | J | 1023.75 |
| /dev/hda6 | | Logical | Linux | | 452.82 |
| /dev/hda7 | | Logical | Linux | | 441.00 |
| | | Pri/Log | Free Space | | 878.07 |

```
[Bootable] [ Delete ] [ Help ] [Maximize] [ Print ]
[ Quit ] [ Type ] [ Units ] [ Write ]
```