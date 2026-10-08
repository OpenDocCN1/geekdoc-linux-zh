# Chapter 20: Adding Hardware and Attaching Peripherals

# # Adding Internal Disks and CD/DVD Drives

Portable USB and FireWire drives are common today, as are USB flash/thumb drives (which look like small hard drives to your system). These portable, removable storage devices simplify backups, transporting large amounts of data and transferring large amounts of data from one system to another. For the most part, these removable devices are correctly identified by Ubuntu systems, which either mount new devices or prompt you for the action to take, as described in the portions of Chapter 18 on digital detection.

While portable, external devices are convenient, you may eventually want to add more storage to your system permanently, which means adding new drives to free connections that are available on your system. These interfaces are faster than external storage and also keep the number of cables running and from the exterior of your system to a minimum.

This section explains how to add internal drives to your systems. The most common types of hard drives found in desktop and laptop IDE/ATA (Enhanced Integrated Drive/Advanced Technology Attachment) and SATA (Serial Advanced Technology) drives. Because of the popularity of SATA drives, IDE/ATA are also known as PATA (Parallel Adaptive Technology Attachment) drives, which highlights the basic difference between these two types of drives (parallel versus serial) and also delivers a nicely paired acronym at the same time. SCSI (Small Computer System Interface) hard drives are another possibility, but are much less common in desktop systems. Most CD and DVD drives are IDE/ATA drives, using a standard referred to as ATAPI, although SCSI and SATA CD and DVD drives are also available.

To add any of these internally to your system, you will have to shut down the system and remove its side cover to give you access to the motherboard and to the partitions of the case where hard drives can be mounted, which are usually referred to as drive bays*

The next few sections explain how to add extra drives of these various types to your system, describe how to identify the device nodes associated with those drives when you reboot your system, and provide an overview of partitioning and creating filesystems on these devices.

# Tip

Before adding new internal disks to your system, you should modify the GRUB bootloader's configuration so it gives you a chance to choose boot options if something goes wrong. To do this, edit the /etc/default/grub and comment out the following lines (putting a # character at the beginning of each line):

```
GRUB_HIDDEN_TIMEOUT=0
GRUB_HIDDEN_TIMEOUT_QUIET=true
```

Commenting these lines causes GRUB to display a boot menu before showing its splash screen. If problems occur, you can edit the commands in menu to boot your system, and update your GRUB configuration to make your changes permanent.

After making these changes and saving the file, run the update-grub command configuration files on your system. Once you've added the new drives and verified that your system boots correctly, you can un-comment these entries and rerun update-grub to hide the boot menus—until the next time you need them, of course. ■