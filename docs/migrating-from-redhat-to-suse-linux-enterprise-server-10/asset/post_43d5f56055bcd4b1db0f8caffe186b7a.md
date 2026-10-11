
Since trusted and preferred networks are user-specific, there must be some mechanism of getting and storing this information per user. This is achieved with a desktop-level per-user process, **nm-applet** or KNetworkManager in KDE. NetworkManager communicates over DBUS with these user-level processes.

Switching to NetworkManager is done by starting YaST and selecting **Network Devices > Network Cards**. In the Network Setup Method dialog, you select **User Controlled** with NetworkManager:

# Figure 3-9

![](img/63e88022bf135307e3eac051ad238b5b_163_0.png)

The following dialogs of this module are the same for both setup methods.

When selecting **User Controlled with NetworkManager**, YaST sets the variable **NETWORKMANAGER** in */etc/sysconfig/network/config* to “yes”.

Choosing the NetworkManager in YaST will also automatically start the Network Applet when a user logs in. Using the desktop applet, the user can easily change the network configuration:

![](img/63e88022bf135307e3eac051ad238b5b_164_0.png)

Note: As there was no wireless card built into the computer on which the above screenshot was taken, there is no option for switching networks in this screenshot.

**1 HARDCOPY PERMITTED-NO DISTRIBUTION ALLOWED**

*Copying all or part of this manual, or distributing such copies, is strictly prohibited. To report suspected copying, please call 1-800-PIRATES.*

## Summary

| Objective | Summary |
| :--- | :--- |
| 1. Manage the Network with YaST | The YaST module for configuring the network card and the network connection can be found at **Network Devices > Network Card**.<br>The following details are needed to integrate the network device into an existing network:<br>- Method of network setup<br>- Static IP address<br>- Network mask<br>- Host name<br>- Name server<br>- Routing (gateway) |

| Objective | Summary |
| :--- | :--- |
| 2. Configure the Network Manually | You can perform the following tasks with the ip tool:<br>- Display the IP address setup: `ip address show`<br>- Display device attributes: `ip link show`<br>- Display device statistics: `ip -s link show`<br>- Assign an IP address: `ip address add IP_address/netmaskbrd + dev device_name`<br>- Delete an IP address: `ip address del IP_addressdev device_name` |

On SLES 10, the configuration files for network devices are located in `/etc/sysconfig/network/`.

Configured devices can be enabled with `ifup device_name` and disabled with `ifdown device_name`.

| Objective | Summary |
| :--- | :--- |
| 3. Set Up Routing with the ip Tool | You can perform the following tasks with the ip tool:<br>- View the routing table: `ip route show`<br>- Add routes to the routing table: `ip route add network/netmask dev device_name`<br>- Delete routes from the routing table: `ip route del network/netmask dev device_name` |

The configuration for the routing table is located in the file */etc/sysconfig/network/routes*.

| Objective | Summary |
| :--- | :--- |
| 4. Configure Host Name and Name Resolution | The host name is configured in the file */etc/HOSTNAME*.<br><br>The name resolution is configured in the file */etc/resolv.conf*.<br><br>One line specifies the search domain; the others list up to three available name servers. |

| Objective | Summary |
| :--- | :--- |
| 5. Use the NetworkManager to Configure the Network | NetworkManager allows the user to change the network configuration without having to assume root privileges.<br><br>NetworkManager is mainly useful for use on laptops. |

## SECTION 4 Manage the Linux File System

In this section, you learn how to manage your SUSE Linux Enterprise Server 10 file system by implementing partitions, creating file systems, checking the file system for errors, and setting up LVM and software RAID.

The default installation proposal for partitioning and file systems on SLES 10 differs from RHEL. The default in SLES 10 does not include LVM, and the file system suggested is ReiserFS. Unlike RHEL, SLES 10 also supports XFS.

### Objectives

- Select a Linux File System
- Configure Linux File System Partitions
- Manage Linux File Systems
- Configure Logical Volume Manager (LVM) and Software RAID

### Objective 1 Select a Linux File System

One of the key roles performed by the Linux operating system is providing storage services through creating and managing a file system.

To successfully select a file system that meets your server requirements, you need to understand the following about file systems available for Linux:

- Linux File Systems
- Linux File System Internals
- File System Journaling
- Additional File System Documentation

It is very important to keep in mind that there might be no file system that best suits all kinds of applications. Each file system has its particular strengths and weaknesses, which must be taken into account.

Always bear in mind that even the most sophisticated file system cannot be a substitute for a reasonable backup strategy.

> For additional details on specific file systems (such as ext3 and ReiserFS), see Section 18.2 in the **SLES 10 Installation and Administration manual** (/usr/share/doc/manual/sles-admin_en/, package sles-admin_en).
> 
> Also see “Additional File System Documentation” on page 4-12 at the end of this objective.

#### Linux File Systems

The type of file system you select depends on several factors (including speed and journaling). While Linux supports several file systems, for a server the choice is usually between three of them.

- **ext2/ext3.** The ext2 file system is inode-based, designed for speed, is efficient, and does not fragment easily.
  Because of these features, ext2 continues to be used by many administrators, even though it does not provide a journaling feature.
  
  The ext2 file system has been available for many years, and is easily converted to an ext3 file system.
- **ext3.** ext3 is the version of the ext2 file system that supports journaling.
- **ReiserFS.** Originally designed by Hans Reiser, ReiserFS treats the entire disk partition as if it were a single database table, storing not only the file metadata, but the file itself.
  Directories, files, and file metadata are organized in an efficient data structure called a “balanced tree,” which offers significant speed improvements for many applications, especially those which use lots of small files.
- **XFS.** XFS is a high-performance journaling file system from SGI. It provides quick recovery after a crash, fast transactions, high scalability, and excellent bandwidth.
  
  XFS combines advanced journaling technology with full 64-bit addressing and scalable structures and algorithms.

For details on XFS, see http://oss.sgi.com/projects/xfs/.

**1 HARDCOPY PERMITTED-NO DISTRIBUTION ALLOWED**

### Linux File System Internals

File systems in Linux are characterized by the fact that data and administration information are kept separate. Each file is described by an *inode* (index node or information node).

Each of these inodes has a size of 128 bytes and contains all the information about this file except the filename. This includes details such as the owner, access permissions, the size, various time details (time of modification, last time of access, and time of modification of the inode), and the links to the data blocks of the file.

How data organization takes place differs from one file system format to the next. To understand the basics of file system data organization on Linux, you need to know the following:

- ext2fs File System Format
- ReiserFS Format
- Directories
- Network File System Formats

### ext2fs File System Format

The ext2 file system format is, in many ways, identical to traditional UNIX file system formats. The concepts of inodes, blocks, and directories are the same.

When a file system is created (the equivalent of formatting in other operating systems), the maximum number of files that can be created is specified. The inode density (together with the capacity of the partition) determines how many inodes can be created.

Remember that it is not possible to generate additional inodes later. You can only specify the inode density when creating the file system.
