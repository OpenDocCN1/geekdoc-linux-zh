
Solaris breaks disks into pieces called partitions, or slices. A Solaris disk can be divided into a maximum of seven partitions.

Why would you want to divide the disk into multiple partitions? Some administrators don’t; they use the entire disk with one partition. By using one partition, all the space on the disk is available for anyone to use. When the system administrator creates a partition, the space in that partition is available only to the file system that is mounted on it. If another file system on the same disk runs out of space, it cannot borrow space from the other partition without repartitioning the disk. However, partitioning can provide some advantages. The following list describes some of the reasons why you might want to consider partitioning disks:

- Partitions allow finer control over such tasks as creating backups. UNIX commands, such as `ufsdump`, work on entire file systems. For backups, you might want to separate data and swap space from the application software so that backups are completed faster with a `ufsdump`. For example, you might want to back up only data on a daily basis. On the other hand, you’ll need to take down the system to single-user mode to back up / and /usr, so separating the data will make your backup complete much more quickly and result in less downtime.
- If one file system becomes corrupted, the others remain intact. If you need to perform a recovery operation, you can restore a smaller file system more quickly. Also, when data is separated from system software, you can modify file systems without shutting down the system or reloading operating system software.
- Partitions allow you to control the amount of disk storage allocated to an activity or type of use.
- If file systems are mounted remotely from other systems, you can share only the data that needs to be accessed, not the entire system disk.

The installation process gives you the option of creating partitions. Start with the default partition scheme supplied with the installation program, which is to set up a file system for root (/), /usr, and swap. This scheme sets up the required partitions, and provides you with the sizes required, based on the software cluster you select to install. The following is a typical partitioning scheme for a system with a single disk drive:

- **root (/) and /usr.** Solaris normally creates two partitions for itself: root (/) and /usr. The installation program determines how much space you need. Most of the files in these two partitions are static. Information in these file systems will not increase in size unless you add software packages later. If you plan to add third-party software after the installation of Solaris, make sure you increase this partition to accommodate the additional files you plan to load. If the root (/) file system fills up, the system will not operate properly.
- **swap.** This area on the disk doesn't have files in it. In UNIX, you're allowed to have more programs than will fit into memory. The pieces that aren't currently needed in memory are transferred into swap to free up physical memory for other active processes. Swapping into a dedicated partition is a good idea for two reasons: swap partitions are isolated so that they aren't put on tape with the daily backups, and a swap partition can be laid out on a disk in an area to optimize performance.
- **/home.** On a single-disk system, everything not in root (/), /usr, or swap should go into a separate partition. /home is where you would put user-created files.
- **/var (optional).** Solaris uses this area for system log files, print spoolers, and email. The name /var is short for variable because this file system contains system files that are not static, but are variable in size. One day, the print spooler directory might be empty; another day, it might contain several 1MB files. This separate file system is created to keep the root (/) and /usr file systems from filling up with these files. If the /var file system does not exist, make sure you make root (/) larger.

- **/opt (optional).** By default, the Solaris installation program loads optional software packages here. Also, third-party applications are usually loaded into /opt. If this file system does not exist, the installation program puts the optional software in the root file system. If the /opt file system does not exist, make sure you make root (/) larger.

File systems provide a way to segregate data, but when a file system runs out of space, you can’t increase it or “borrow” from a file system that has some unused space. Therefore, the best plan is to create a minimal number of file systems with adequate space for expansion. See Chapter 6 and Chapter 7, “Solaris File Systems: Advanced Topics,” for additional information on planning and creating file systems.

## Basic Considerations for Planning Partition Sizes

Planning disk and partition space depends on many factors: the number of users, the application requirements, and the number and size of files and databases. Following are some basic considerations for determining your disk space requirements:

- Allocate additional disk space for each language selected (for example, Chinese, Japanese, Korean).
- If you need printing or mail support, create a partition for a separate /var file system and allocate additional disk space. You need to estimate the number and size of email messages and print files to size this partition properly.
- Allocate additional disk space on a server that will provide home file systems for users. Again, the number of users and the size of their files will dictate the size of this file system. By default, home directories are usually located in the /export file system.
- Allocate additional disk space on an operating system server for diskless clients or Solstice AutoClient systems.
- Make sure you allocate enough swap space. Factors that dictate the amount of swap space are the number of users and the application requirements. Consult with your application vendor for swap-space requirements. Vendors usually give you a formula to determine the amount of swap space you need for each application.
- Determine the software packages you will be installing, and calculate the total amount of disk space required. When planning disk space, remember that the Solaris Interactive Installation program lets you add or remove individual software packages from the software cluster you select.
- Create a minimum number of file systems. By default, the Solaris Interactive Installation program creates only root (/), /usr, and swap, although /export is also created when space is allocated for operating system services. Creating a minimum number of file systems helps with future upgrades and file system expansion because separate file systems are limited by their slice boundaries. Be generous with the size of your file systems, especially root (/) and /usr. These file systems cannot be increased without completely reloading the operating system.
- Calculate additional disk space for copackaged or third-party software.

## Partition Arrangements on Multiple Disks

Although a single large disk can hold all partitions and their corresponding file systems, two or more disks are often used to hold a system's partitions and file systems.

For example, a single disk might hold the root (/) file system, a swap area, and the /usr file system; and a second disk might be used for the /export/home file system and other file systems containing user data. In a multiple-disk arrangement, the disk containing the root (/) and /usr file systems and swap space is referred to as the system disk. Disks other than the system disk are called secondary disks or nonsystem disks.

> NOTE
You cannot split a partition between two or more disks.

Locating a system's file systems on multiple disks allows you to modify file systems and partitions on the secondary disks without shutting down the system or reloading the operating system software. Also, multiple disks allow you to distribute the workload as evenly as possible among different I/O systems and disk drives, such as distributing the /home and swap partitions evenly across disks.

Having more than one disk increases input/output (I/O) volume. By distributing the I/O load across multiple disks, you can avoid I/O bottlenecks.

> NOTE
A good way to improve system performance is to create more than one swap partition, and assign each of them to separate disk drives. When the system needs to access swap, the disk I/O is spread across multiple drives.

## DEVICE DRIVERS

A computer typically uses a wide range of peripheral and mass-storage devices, such as a SCSI disk drive, a keyboard, a mouse, and some kind of magnetic backup medium. Other commonly used devices include CD-ROM drives, printers, and plotters.

Solaris communicates with peripheral devices through device files. Before Solaris can communicate with a device, it must have a device driver, a low-level program that allows the kernel to communicate with a specific piece of hardware. The driver serves as the operating system's “interpreter” for that piece of hardware.

When a system is booted for the first time, the kernel creates a device hierarchy to represent all devices connected to the system. Devices are described in three ways in the Solaris environment, using three distinct naming conventions: the physical device name, the instance name, and the logical device name. System administrators need to understand the device names when using commands to manage disks, file systems, and other devices.

### Physical Device Name

A physical device name represents the full device pathname of the device. Physical device files are found in the /devices directory and have the following naming convention:

```
/devices/sbus@1,f8000000/esp@0,40000/sd@3,0:a
```
