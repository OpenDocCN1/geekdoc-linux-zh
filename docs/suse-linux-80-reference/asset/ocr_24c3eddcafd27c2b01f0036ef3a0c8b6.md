![](bbox=[0.289, 0.098, 0.822, 0.359])

*Figure 2.4: Selecting the Mouse Type*

# Partitioning

The suggested partitioning appears with a confirmation option, allowing you to accept, change, or discard the suggestion. See *More Partitioning Tips* on page 16 regarding automatic entries in `/etc/fstab`. Clicking “Change” opens the “Partitioner”.

YaST2 shows all partitions present on the selected hard disk (Figure 2.6 on page 12). Any free storage space is shown and automatically selected. To assign more disk space to Linux, you can assign more partitions following the order from the last to the first partition. If you have three partitions, it is not possible to use the second one for Linux and the first and third for other operating systems.

If you choose “Discard”, a dialog appears containing the hard disk selection (Figure 2.7 on page 13). All the hard disks on your system are listed here. Decide where to install SuSE Linux. There is no risk associated with selecting the hard disk, as no changes are made at this time.

The menu “Advanced Settings, Manual Partitioning” shows the previous partitioning of your system, which can be manually modified or reused for your new system.

By clicking “Entire hard disk”, the entire hard disk and all its partitions are activated for Linux. If you already installed a Windows operating system with a FAT file system, you will be asked if you want to delete or shrink the Windows partition (refer to *Resizing a Windows Partition* on page 12). **Caution:** All partitions and data existing on this hard disk will be lost.