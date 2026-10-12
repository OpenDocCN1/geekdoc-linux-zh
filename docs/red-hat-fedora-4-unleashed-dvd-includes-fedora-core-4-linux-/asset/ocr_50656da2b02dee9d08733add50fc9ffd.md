If a new hard drive is properly attached to your PC and you then boot Linux, you can see if the kernel recognizes the device by viewing the output of the `dmesg` command. You can then use `fdisk` with the device name to begin partitioning like so:

```
# fdisk /dev/hdb
```

Note that you will need root permission, and in this example, the new drive is attached as a slave on IDE channel 0. Do not change partitioning on your root device, or you'll fork your system! The `fdisk` command is interactive, and you can press `m` to get help when using the utility. You can use `parted` in much the same way if you specify the `i`, or interactive option on the command line like so:

```
# parted -i /dev/hdb
```

To get help when using `parted` interactively, press ? or type `help` followed a command keyword. The `parted` command has other helpful features, such as the ability to copy a file system directly from one partition to another.

Finally, you can prepare partitions ahead of installation by booting your system using a live Linux distribution (such as the LNX Bootable Business Card, available at http://www.lnx-bbc.org/) and then using a native Linux utility such as `fdisk` to partition your drive. For details on using the `fdisk` partitioning utility and alternative software tools to partition your hard drive, see the section “How to Access and Manipulate the Partition Table” in Chapter 37, “Managing the File System.”

> **TIP**
> You can use the first Fedora CD or the DVD to perform other tasks aside from installing Linux. The CD-ROM/DVD features a rescue mode and can also be used to partition and prepare a hard drive for Linux. See Chapter 3.

> **NOTE**
> It is possible to create a dual-boot configuration, which allows the choice of booting Fedora and another operating system, such as Windows XP. To configure your system for dual-booting, you must first install Windows and then install Linux. Note that many Windows system-restore CD-ROMs will wipe out all data on your hard drive, including Linux. During installation of Fedora, you install the GRUB Linux bootloader in the primary drive's Master Boot Record, or MBR. When properly configured, GRUB allows your system to reboot to Windows or Linux. See Chapter 16, “Backing Up, Restoring, and Recovery,” for information on using GRUB, or browse to http://www.gnu.org/software/grub/manual/ to read the GRUB manual.

> **CAUTION**
> Before you begin partitioning your drive, get your safety nets in order. First, back up all critical data! Any changes to your system's hard drive or operating system put your existing data at risk. To prevent the loss of time and resources that inevitably follow data loss, do full backups before