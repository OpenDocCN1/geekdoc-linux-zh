
For the most part, the alternate install CD requests the same information for the installation as the LiveCD, but it uses text-oriented menus instead of graphical GUI menus. You’ll be prompted to select the installation language, the time zone, the keyboard type (the alternate install CD can even autodetect most standard types of keyboards), and the default userID and host name information.

The alternate install CD provides something that’s not available in the LiveCD, and that feature appears in the disk partitioning section. Linux systems can use a feature called logical volume management (LVM), which allows you to create dynamic partitions on your system. You can add and remove disk space from LVM partitions at any time, providing a flexible way to allocate disk space on your system.

The following sections describe how to use LVM in both the guided and manual partition methods when using the alternate install CD.

## Guided Partitions

When you get to the Partition Disks section of the alternate install CD process, you’ll see a slightly different configuration from what the LiveCD presents. Figure 3-13 shows the main Partition Disks window that appears when performing an installation from the alternate install CD.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_97_0.png)

Figure 3-13: The Partition Disks window in the alternate CD installation.

Notice that there are two additional guided options available for you to use:

- Use the entire disk and set up LVM.
- Use the entire disk and set up encrypted LVM.

When you select one of these options, the Ubuntu installer will automatically create a logical volume on your hard drive for Ubuntu. Once the logical volume is created, you can use Linux utilities to modify it at any time (see Chapter 18, "Basic Administration").

Disk space management is a tricky business, and the Linux logical volume management (LVM) feature is a great tool designed to help solve some of the basic problems of disk management, but it has been known to cause other problems.

When designing the layout of a system, often it’s difficult to predict exactly how much disk space will be required for applications and user data. With standard filesystems such as ext3, if you need to add space you must back up the data, create a completely new partition, then restore the data on the new partition.

With LVM, instead of associating a location in the virtual filesystem to a partition, you assign it to a logical volume group. You can add any physical disk partition you wish to the logical volume group. If the logical volume group runs out of space, you can add a new hard drive, then dynamically add space to the existing logical volume group.

LVM maintains its own table so it knows which partitions are part of which logical volume group. It’s not uncommon for a logical volume group to become corrupt, even though the data on the hard drive partition are just fine. Data corruption can cause catastrophic problems on a Linux system, especially if it happens to the root partition.

Therefore, administrators for large Linux systems often use a combination of dedicated partitions and LVM partitions. They’ll use a dedicated partition for the root partition, then create LVM partitions for the /opt and /home portions of the virtual filesystem. This configuration allows you to add disk space as new applications are installed or when users start running out of space, while maintaining the integrity of the root filesystem.

## Manual Partitions

Besides the guided LVM partitions, you can manually create LVM partitions on your Ubuntu installation from the alternate install CD. If you select the Manual Partition option from the Partition Disks window, you’ll get the second-level Partition Disks window, shown in Figure 3-14.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_98_0.png)

Figure 3-14: The second-level Partition Disks window.

In this window you can manually select a partition to modify or delete, or you can add a new partition. The first entry shows the actual hard drive device detected. The indented entries under that show the free space on that hard drive, plus any existing partitions on that hard drive, and their information.

Select the free space area you want to work on, and hit the Enter key. The Partition Disks window for the next level appears, shown in Figure 3-15.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_99_0.png)

Figure 3-15: The individual partition configuration window.

When you select the Use As entry, a menu appears, allowing you to select which filesystem to install on the partition. Besides the standard filesystems available in the LiveCD install (see “Prepare the Disk Space” section earlier in this chapter), you’ll see three additional entries—the two LVM options (regular and encrypted) and an option to create a software RAID volume.

Once you’ve created the partition with the filesystem of your choice, you can save the settings and continue with the installation.

## Server Installation

If you’re interested in installing a Linux server, the Ubuntu server LiveCD is probably the easiest way to go. The Ubuntu server installs many popular server packages automatically for you, without any configuration required.

This section walks through the Ubuntu server installation process, showing how to configure your server.

### Main Installation

The Ubuntu server LiveCD installation is very similar to the workstation alternate CD installation process. The server installation uses a text-based approach because servers often don’t have (or need) fancy video cards.
