Note that you will need root permission, and in this example, the new drive is attached as a slave on IDE channel 0. Do not change partitioning on your root device; otherwise, you will wreck your system! The fdisk command is interactive, and you can press M to get help when using the utility. You can use parted in much the same way if you specify the -i, or interactive option on the command line, as follows:

```
# parted -i /dev/hdb
```

To get help when using parted interactively, press ? or type help followed by a command keyword. The parted command has other helpful features, such as the capability to copy a file system directly from one partition to another.

Finally, you can prepare partitions ahead of installation by booting your system using a live Linux distribution (such as the LNX Bootable Business Card, available at http://www.lnx-bbc.org/) and then using a native Linux utility such as fdisk to partition your drive. For details on using the fdisk partitioning utility and alternative software tools to partition your hard drive, see the section “Creating the Partition Table” in Chapter 35, “Managing the File System.”

> **NOTE**
> 
> It is possible to create a dual-boot configuration, which allows the choice of booting Fedora and another operating system, such as Windows XP. To configure your system for dual booting, you must first install Windows and then install Linux. Note that many Windows system-restore CD-ROMS wipe out all data on your hard drive, including Linux. During installation of Fedora, you install the GRUB Linux boot loader in the primary drive's Master Boot Record, or MBR. When properly configured, GRUB allows your system to reboot to Windows or Linux. Browse to http://www.gnu.org/software/grub/manual/ to read the GRUB manual online.

# ### Choosing a Partitioning Scheme

As with deployment and installation of Linux, partitioning your hard drive to accept Fedora requires some forethought, especially if the target computer is going to be used other than as a home PC on which to learn Linux. If Linux is to be the only resident operating system, you can have the installer automatically create and use a partition scheme according to the type of installation you select during the install. If you plan to have a dual-boot system in which you can boot Linux or another operating system, you have to manually partition your hard drive before and possibly during the install.

> **CAUTION**
> 
> Before you begin partitioning your drive, get your safety nets in order. First, back up all critical data! Any changes to your system's hard drive or operating system put your existing data at risk. To prevent the loss of time and resources that inevitably follow data loss, do full backups before you make any changes to your system. Create a bootdisk during the install (you will be asked before the install finishes) so that you will be able to at least boot Linux if something goes wrong.