![](bbox=[0.35, 0.13, 0.75, 0.42])

Figure 3-22 Selecting the operating system from a dual-boot system

**Use existing free space**—If there is sufficient free space on the Windows disk, you can install Linux there. This technique is the optimal choice, but there is rarely enough free space on an installed hard disk.

**Reclaim space from a Windows partition**—Windows partitions often occupy the entire disk, which explains why reclaiming space from a Windows partition is the technique most commonly used to free up space. Windows systems typically use NTFS, FAT32, and/or FAT16 filesystems. You can reclaim space from an existing Windows partition when you install Fedora/RHEL (page 77).

**Remove a Windows partition**—If you can delete a big enough Windows partition, you can install Linux in its place. To delete a Windows partition, you must have multiple partitions under Windows and be willing to lose the data in the partition you delete. In many cases, you can save this data by moving it from the partition you will delete to another Windows partition.

Once you are sure a partition contains no useful information, you can delete it when you install Fedora/RHEL. Alternatively, you can use gnome-disks from a live session to delete it (page 82). After deleting the partition, you can install Fedora/RHEL in the free space formerly occupied by the partition you deleted.

# **If you install Windows after you install Linux**

> When you install Windows as the second operating system it overwrites the existing boot loader. In this case you need to reload the boot loader. See “Reinstalling the MBR” on page 456 for instructions.

# **INSTALLING FEDORA/RHEL AS THE SECOND OPERATING SYSTEM**

After you have created enough free space on a Windows system, you can begin installing Fedora/RHEL in the free space you created. When you boot the updated system, you will be able to choose which operating system you want to run (Figure 3-22).