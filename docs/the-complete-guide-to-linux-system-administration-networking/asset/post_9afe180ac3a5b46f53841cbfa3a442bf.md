
series of configuration windows appear. The first is shown in Figure 10-4. The main purpose of this tool is to let you read the terms of use for Red Hat Network and to enter a proxy or authentication information if needed to access Red Hat Network from your location. (These are usually not necessary.)

![](img/43f64015de86d989e30eff5bb284fb96_467_0.png)

Figure 10-4 Starting to configure the Red Hat Network service for your system

To configure the overall settings for Red Hat Network, choose System Tools, then Red Hat Network on the GNOME main menu. A window with three tabs appears. The General tab is shown in Figure 10-5. In this tab, you see the name of the Red Hat Network server that the program will periodically check for updates. Click Refresh to update from the Internet the list of servers available for updates. You can use the fields below the server name if you must connect to Web servers through a proxy; you can provide the proxy server name and any user name and password that you must use to access the proxy server.

On the Retrieval/Installation tab, shown in Figure 10-6, you define what the Red Hat Network utility does with software package updates after they are retrieved from Red Hat Software. In the Package Retrieval Options section, you can specify that packages are not installed or upgraded after being downloaded (the default is to install them). Also by default, however, packages are not upgraded if you have made changes to the default configuration file. This avoids overwriting your configurations. Such packages are stored in the Package storage directory named at the bottom of the window, from which you can install them yourself after backing up any modified configuration files. You can also choose to download the source code rpm as well as the binary RPM. Typically only developers want to download these packages.

![](img/43f64015de86d989e30eff5bb284fb96_468_0.png)

Figure 10-5 The General tab of the Red Hat Network Configuration tool

![](img/43f64015de86d989e30eff5bb284fb96_468_1.png)

Figure 10-6 The Retrieval / Installation tab of the Red Hat Network Configuration tool

By default, all packages are verified using GPG—this is essentially the same as using the --checksig option on the rpm command as discussed in the previous section. Finally, in the Package Installation Options section of this tab, you can select to have the rpm files saved after installation (this takes extra disk space, of course—the default is to erase them after they have been installed). And you can enable rpm rollbacks, also at the cost of additional disk space. Rollbacks are useful if you are experimenting with a Linux system and are concerned that updates might interrupt your work.

Finally, in the Package Exceptions tab (see Figure 10-7), you can identify packages or files that you don’t want to have automatically updated by Red Hat Network. By default, the list includes only packages beginning with “kernel,” with the assumption that you don’t want your kernel upgraded without making that decision yourself. You can add other packages or even individual files based on which services you consider critical or don’t want to have altered without explicit action on your part.

![](img/43f64015de86d989e30eff5bb284fb96_469_0.png)

Figure 10-7 The Package Exceptions tab of the Red Hat Network Configuration tool

When you click OK in this configuration window, you are taken to the Red Hat Network update windows, where the server is contacted and upgrades to packages installed on your system are identified and downloaded.

The basic Red Hat Network service described here is part of a larger Red Hat Network architecture that Red Hat Software provides at an extra cost to customers who purchase Red Hat Enterprise Linux products. In addition to the basic service, Red Hat Software highlights the Management and Provisioning products within Red Hat Network’s offering.

By purchasing access to these services, you can add capabilities such as those in the following list to help keep your systems secure and up to date. The great advantage in these pay services is the ability to work with multiple Linux servers through a single interface, rather than trying to log in to multiple systems, collect data about what is installed or needing upgrading, and then coordinating it from a central location. Red Hat Network automates all of these functions:

- Manage upgrades across multiple systems, with timed deployment and different upgrade models and permissions assigned to the administrators of different Linux servers.
- Compare what is installed on one system against a default system profile or against another Linux system.
- Build systems from "bare metal" using a preconfigured set of packages and configuration files (only available through the Provisioning product).
- Use rollback features to maintain multiple levels of status so that you can take a system back to any point in time (only available through the Provisioning product).
- Provide complete automated updates for all applications rather than just critical operating system files (only available through the Provisioning product).

![](img/43f64015de86d989e30eff5bb284fb96_470_0.png)

For more information on the technology and products behind Red Hat Network, visit www.redhat.com/software/rhn/.

Managing software packages, either directly or through an update system such as Red Hat Network, is only a part of managing files in Linux. In the next section, you learn more about the underlying structure and utilities you can rely on to manage entire file systems in Linux.

## UNDERSTANDING THE FILE SYSTEM

When you installed Linux, the installed program created a root file system in which the operating system files were stored. The root file system may have been created on several partitions—for example, one for the /boot directory, one for the /home directory, one for the /usr directory, and another as the root directory, /. Linux uses ext3 or a similar file system as the default file system type for these partitions. After installation is completed, you might need to modify or add new Linux partitions or hard disks, or you might need to access data stored using non-Linux file system types. This section discusses how Linux file systems are constructed, how to create and manage Linux file systems, and how to access other types of file systems.

### Reviewing File System Types

You learned in Chapter 4, "Understanding Users and File Systems," that a file system is a collection of data structured in a certain way so that it can be efficiently accessed. A file system must include information about the data it is storing in order to permit efficient access. For example, you have learned about inodes and using the stat command to view inode information and other details about an existing file. Each inode contains information about a single file in the file system. The file system arranges inodes on the storage media to provide efficient access to that information, as well as to the data the inode refers to. The ext2 and ext3 file systems include a collection of information about the file system as a whole called the superblock. The superblock contains details such as the size of each block on the file system, the volume label, the date of the last integrity check, the amount of space reserved for the root user, and several other pieces of information. A duplicate copy of the superblock is stored at dozens of locations in a large file system. If a complete copy of the superblock cannot be found, the file system cannot be accessed.

The ext2 and ext3 file systems do not place files one after another, filling up each area of a hard disk in order. Instead, they place files at various points located throughout the entire area of the file system. This permits a file to grow in size without being as likely to be broken into pieces because it "runs into" space taken by another file. This means that the fragmentation problem of some other file systems, such as FAT, FAT32, and NTFS, is not present in ext2 and ext3 file systems—you never need to defragment your Linux file system.

The ext3 file system is just like the ext2 file system except that ext3 is a journaling file system: it stores information about each disk operation so that if an error occurs (such as the system being shut down), the file system does not become corrupted. This journaling adds a small amount of overhead, but is much better than risking file system corruption.

Two other journaling file systems are available for Linux. The Reiser file system (typically called ReiserFS), is the default file system on the SUSE, LinuxWorks/Linspire, Gentoo, and other Linux distributions. ReiserFS is in many ways similar to ext3, but uses a method of deciding where to place files that is reputed to be more efficient, leading to faster access times, especially when dealing with large numbers of files (such as a million files in a single directory). A good technical description of ReiserFS is available at www.namesys.com/v4/v4.html.

Another journaling file system available for Linux is called the Journaling File System (JFS). This file system was developed by IBM and is now distributed under the GPL—the same license as Linux itself. JFS was designed for IBM enterprise servers. It currently ships as part of most commercial Linux distributions. You can learn more about JFS by visiting http://oss.software.ibm.com/developerworks/opensource/jfs/.

The Linux kernel uses a virtual file system model. This is a method of accessing data that separates the file system type from the operation a program wants to perform. Virtually all programs want to perform the same types of operations on a file system: display the contents of a directory, open a file, read from a file, write to a file, and so on. When a program requests that the Linux kernel perform one of these operations, the kernel determines the type of the file system for which the operation has been requested. The kernel then has the driver for the appropriate file system type perform the operation. This model means that Linux can support any new file system type for which a driver is available. Dozens of file system types are supported, though Linux itself relies on those mentioned here for hard disk storage of regular files. Later in this section you will see how to work with different file system types.
