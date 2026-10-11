
![](img/577d3bff979ee86b07f9836e0df274ce_59_0.png)

**FIGURE 3-6**: The Ubuntu Installation Type window.

- If you've already shrunk your existing Windows partition manually (as discussed in Chapter 2), the Ubuntu installer offers to install Ubuntu on the available empty partition and create a dual-boot environment.
- If you have a previous version of Ubuntu already installed, the Ubuntu installer offers to upgrade only the OS and leave your data intact if possible.
- If you have a second hard drive in your workstation the Ubuntu installer offers to use it for Ubuntu, leaving your existing hard drive alone, and create a dual-boot environment.
- If you have a single hard drive that already contains an existing Windows or Linux partition, the Ubuntu installer offers to erase the entire partition and just install Ubuntu.
- Allows you to manually partition your hard drive to create your own partitions.

Which option you select depends on just what type of setup you want to try. If you want to run an Ubuntu-only workstation, the option to erase the existing operating system is the quickest and easiest way to go.

Even if you select one of the options to keep the existing operating system, it's a very good idea to back up any important files contained in that operating system. Mistakes can (and often do) happen when working with hard drives.

If you select an option to keep an existing operating system on your hard drive, the Ubuntu installer allows you to select how much disk space to allocate for the new Ubuntu partition. You can drag the partition separator to redistribute disk space between the original operating system and the new Ubuntu partition. Hopefully you remember your disk space requirements determined earlier in Chapter 2 to use here!

If you select the manual partition process, Ubuntu turns control of the partition process over to you. It does provide a great partition utility, shown in Figure 3-7, for you to use to create, edit, or delete hard drive partitions.

![](img/577d3bff979ee86b07f9836e0df274ce_60_0.png)

**FIGURE 3-7:** The Ubuntu manual partition utility.

The manual partition utility displays the current hard drives, along with any existing partitions configured in them. Once you become an experienced Linux user you can manually remove, modify, or create individual partitions on any hard drives installed on the system to customize your Linux setup.

7. If you're performing a manual partition, select a filesystem for your Ubuntu partition.

Part of the manual partition process is to assign a filesystem to each partition. A filesystem is a method used for storing and accessing files on the partition. Unlike some other operating systems, Ubuntu supports several different filesystems. You can select any of the available filesystems for any of the partitions Ubuntu will use. Table 3-1 shows the filesystem types available for you when creating disk partitions in Ubuntu.

## TABLE 3-1 Ubuntu Partition Filesystem Types

| Partition Type | Description |
| :--- | :--- |
| ext4 | A popular Linux journaling filesystem that is the current extension over the original Linux ext2 file system |
| ext3 | A legacy Linux journaling filesystem that is an extension over the original Linux ext2 file system |
| ext2 | The original non-journaling Linux filesystem |
| btrfs | A newer, high-performance filesystem that supports large file sizes |
| JFS | The Journaled Filesystem, created by IBM and used in AIX Unix systems |
| XFS | A high-performance journaling filesystem created by Silicon Graphics for the IRIX operating system |
| FAT16 | Older Microsoft DOS filesystem |
| FAT32 | Newer Microsoft DOS filesystem compatible with Microsoft Windows |
| swap area | Virtual memory area |
| encrypted volume | Linux allows you to encrypt an entire partition — just don't forget the key |
| Do not use | Ignore the partition |

The most common partition type (and the default used by the Ubuntu guided methods) is the ext4 format. This filesystem format provides a journaling filesystem for Ubuntu. A journaling filesystem logs any file changes into a log file before attempting to commit them to the disk. If the system should crash before it can properly commit the data, the journal log file is used to complete the pending file commits, and return the disk to a normal state. Journaling filesystems greatly reduce file corruption in Linux.

8. If you're performing a manual partition, select the mount points for the partitions.

After selecting a filesystem for the partition, the next item that Ubuntu wants for the partition is where to mount the partition in the virtual filesystem (see Chapter 7). The Ubuntu virtual filesystem handles hard drives by plugging them into specific locations in the virtual filesystem. Table 3-2 lists the possible locations where you can mount a partition.

If you create just one partition for Ubuntu, you must mount it at the root mount point (/). If you have additional partitions available, you can mount them in other locations within the virtual filesystem.

## TABLE 3-2 Mount Point Locations

| Location | Description |
| :--- | :--- |
| `/` | The root of the Linux virtual filesystem |
| `/boot` | The location of the Linux kernel used for booting the system |
| `/home` | User directories for storing personal files and individual application setting files |
| `/tmp` | Temporary files used by applications and the Linux system |
| `/usr` | A common location for multi-user application files |
| `/var` | The variable directory, commonly used for log files and spool files |
| `/srv` | A common location for files used by services running on the system |
| `/opt` | Optional package installation directory for third-party applications |
| `/usr/local` | A common alternative location for optional multi-user package installations |

![](img/577d3bff979ee86b07f9836e0df274ce_62_0.png)

If you're using the manual partition method, don't forget to allocate a partition for the swap area, even if you already have lots of physical memory installed on your system. The Linux kernel uses the swap area as a temporary holding ground to move sleeping applications out of physical memory to make more room for running applications. The standard rule for this is to create as large of a swap area as you have physical memory. Thus, if you have 8GB of physical memory, create an 8GB partition and assign it as the swap area.

9. If you're erasing an existing partition, or creating a new one, select any advanced disk features to use, and then click OK.

Ubuntu provides the option for you to use the Logical Volume Manager (LVM) feature in Linux with your hard drive partitions. LVM provides a way for you to easily add more space to an existing directory at any time if needed, even if there's data already in the directory. You may also choose to encrypt the logical volume if you need to. The other option is to use the ZFS filesystem, which is a commercial filesystem recently released to the open source world.

10. Click Install Now to accept the proposed hard drive partition changes and continue with the installation.

Up until this point you can change your mind about the hard drive changes. However, after you click Install Now here you're committed to those changes and there's no going back!

11. Select your location, and then click Continue.

Because Ubuntu is in use worldwide, you'll need to manually select just where in the world you are located so Ubuntu can assign the correct time zone and locale settings.

12. Create a Login ID, and then click Continue.

Up next in the installation process is the Login ID window, shown in Figure 3-8.

![](img/577d3bff979ee86b07f9836e0df274ce_63_0.png)

The login ID you create in this process is somewhat important. Unlike other Linux distributions, the Ubuntu distribution doesn't use an administrator login account (usually called *root* in the Unix/Linux world). Instead, Ubuntu provides the ability for normal user accounts to belong to an administrators group. Members in the administrators group have the ability to become temporary administrators on the system (see Chapter 17).

![](img/577d3bff979ee86b07f9836e0df274ce_63_1.png)

Having an account with administrative privileges is important, as the administrator is the only account that's allowed to perform most system functions, such as changing system features, adding new devices, and installing new software. Without an administrative account, you won't be able to do much of anything new on the system.

Besides identifying yourself, you'll also need to assign a name to the computer itself. Ubuntu uses this name when advertising its presence on the network, as well as when referencing the system in log files. You should select a computer name that's unique on your network, is less than 63 characters long, and does not contain any special characters (although hyphens are allowed).

One final setting — you must determine whether you want the system to automatically log you into your desktop, or to prompt for your login password. I wouldn't recommend using this feature on laptops that you may accidentally leave behind somewhere. If you'll be the only one using the desktop PC (and
