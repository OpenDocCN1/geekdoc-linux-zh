
![](img/6d8286a85e2d8ad63e16f1801102da59_52_0.png)

## Understanding the Standard Tree Structure

The tree-like structure for UNIX file systems starts at the root level. **Root** is the name of the file at this basic level, and it is denoted by the slash character (/). The slash represents the **root directory**.

A **directory** is a special kind of file that can contain other files and directories. Regular files store information, such as records of employee names and addresses or payroll information, while directory files store the names of regular files and the names of other directories, which are called **subdirectories**. The subdirectory is considered the **child** of the **parent** directory because the child directory is created within the parent directory. In Figure 2-1, the root directory (/) is the parent of all the other directories. The home directory, for example, is the parent of the jean, tricia, and joseph subdirectories.

## Using UNIX Partitions

The section of the disk that holds a file system is called a **partition**. One disk may have many partitions, each separated from the others so that it remains unaffected by external disturbances such as structural file problems associated with another partition. When you install UNIX on your computer, one of your first tasks is deciding how to partition your hard drive.

UNIX partitions are identified with names; for example, Linux uses “hda1” and “hda2.” In this case, the first two letters tell UNIX the device type: “hd,” for instance, means hard disk. The third letter, “a,” for instance, indicates whether the disk is the primary or secondary disk (a=primary, b=secondary). Partitions on a disk are numbered starting with 1. The name “hda1” tells UNIX that this is the first partition on the disk, and the name “hda2” indicates it is the second partition on the same disk. If you have a second hard disk with two partitions, the partitions are identified as “hdb1” and “hdb2.” Computer storage devices such as hard disks are called peripheral devices. Computer **peripherals**, like hard disks, connect to the computer through *electronic interfaces*. The two most popular hard disk interfaces are the **IDE** (Integrated Drive Electronics) and **SCSI** (Small Computer System Interfaces). On PCs, IDE hard disk drives are more common than SCSI (pronounced “scuzzy”). SCSI is faster and more reliable. It is used on large servers. If you have a primary SCSI hard disk with two partitions, the two partitions are named “sda1” and “sda2.” Figure 2-2 shows two partition tables: one with an IDE drive and the other with a SCSI drive.

```text
Disk /dev/hda: 128 heads, 63 sectors, 767 cylinders
Units = cylinders of 8064 * 512 bytes

Device Boot Begin Start End Blocks Id System
/dev/hda1 * 1 1 242 975712+ 6 DOS 32-bit >=32M
/dev/hda2 243 243 767 2116899 5 Extended
/dev/hda3 243 243 275 127024+ 83 Linux native
/dev/hda6 276 276 750 1028224+ 83 Linux native
/dev/hda7 751 751 767 68512+ 82 Linux swap

Command (m for help): _
This partition table is from a Linux system with an IDE drive
```

```text
Disk /dev/sda: 255 heads, 63 sectors, 1106 cylinders
Units = cylinders of 16065 * 512 bytes

Device Boot Begin Start End Blocks Id System
/dev/sda1 1 1 64 514048+ 83 Linux native
/dev/sda2 65 65 1106 8369865 5 Extended
/dev/sda5 65 65 1084 8193118+ 83 Linux native
/dev/sda6 1085 1085 1100 128488+ 82 Linux swap

Command (m for help): _
This partition table is from a Linux system with a SCSI drive
```

![](img/6d8286a85e2d8ad63e16f1801102da59_53_0.png)

Note that the first table in Figure 2-2 identifies “hda” as the device, which indicates an IDE drive. The second table identifies “sda” as the device, which indicates a SCSI drive.

## Setting Up Hard Disk Partitions

Partitioning your hard disk provides organized space to contain your file systems. If one file system fails, you can work with another. This section provides general guidelines on how to partition hard disks. These recommendations are suggestions only. How you partition your hard drive may vary depending on your system’s configuration, number of users, and planned use. Partition size is measured in megabytes (MB, about a million characters) or gigabytes (GB—about a billion characters). You should have at least three separate partitions to store your file systems: root, swap, and /usr.

Begin by setting up a partition for the root file system. A partition must be mounted before it becomes part of the file system. The kernel mounts the root file system when the system starts. The kernel has no other information about the computer’s other file systems, so all the information and programs the kernel needs to start the system must be present on the root partition. To protect this critical information, separate partitions are often used for other system data.

The root partition can be small to leave space for other file systems. A corrupted root file system makes the system unbootable. Red Hat and most Linux distributors recommend a root partition size of no more than 120 MB.

After creating the root partition, you should set up the **swap** partition. The swap partition acts like an extension of memory, so that UNIX has more room to run large programs. Linux distributors suggest that your swap space be twice the size of your computer’s internal memory (RAM). For example, if your computer has 64 MB of RAM, you should allocate 128 MB for the swap partition. See Appendix C, “Installing Red Hat 6.x,” for more information.

The **/usr** partition stores all the non-kernel operating system programs that make the computer useful. These programs include software development packages that support computer programming, networking, Internet access, graphical screens (including X-Windows), and the large number of UNIX **utilities** (programs that perform utilitarian operations like copying files, listing directories, and communicating with other users). The usr partition should be the largest of the three partitions, at least 600 MB.

In addition to these three separate partitions, you can create a **/home** partition, the home directory for all users’ directories. A separate /home partition makes many system administration tasks such as backing up data more efficient.

For example, Dominion Consulting partitions a PC with 32 MB of RAM and allocates 2 GB of hard disk space for UNIX, allowing 120 MB for the root partition, 1400 MB for the /usr partition, 32 MB for the swap partition, and 448 MB for the /home partition.

## The /usr Partition

The /usr partition is a large partition that stores most operating system files and programs. Most Linux distributors, including Red Hat, offer you the option to “install everything” from their CD-ROM and store most of these files in the /usr partition. This is true of other UNIX systems as well. Software development tools such as language compilers, shared libraries, and header files needed for program creation are also stored in a hierarchy of subdirectories starting at /usr.

## The /home Partition

The /home partition is the storage space for all users’ work. If the root partition (or any other partition) crashes, having a /home partition ensures that you do not lose all the users’ information. Although regular user accounts are restricted from reading information in other partitions, you own and can access most files in your home directory. You can grant or deny access to your files as you choose. See “Setting File Permissions” later in this chapter for more information on file ownership.

The size of the partition on a system for all users’ home directories depends on how many users the system supports. Thirty users probably need a total of 3000 MB, that is, 3 GB (3 billion characters). This scheme gives users an average of 100 MB each to store their work. The space allocated depends on how much data each user needs to store.

## The swap Partition

Swap partitions support virtual memory. Virtual memory means you have an unlimited memory resource—swap partitions try to meet this goal by providing swap space on disk and treating it like an extension of memory (RAM). It is called swap space because the system can use it to swap information between disk and RAM. Setting up swap space makes your computer run faster and more efficiently. If your computer has 16 MB of RAM or less, you must allocate some disk space to a swap partition. Even if your computer has more than 16 MB of RAM, swap space is recommended for all UNIX systems. The minimum amount of swap space should equal your RAM.

> tip
>
> You can create and use more than one swap partition on Linux. Having multiple swap partitions spread across several hard disks can sometimes improve application performance on busy systems.

## Exploring the Root File System

The root (/) file system is mounted by the kernel when the system starts. To mount a file system is to connect it to the directory tree structure. The system administrator uses the mount command to mount a file system. The syntax of the mount command is:
