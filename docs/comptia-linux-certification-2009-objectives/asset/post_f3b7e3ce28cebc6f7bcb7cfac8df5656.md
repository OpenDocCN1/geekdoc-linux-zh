
- Objective 2.1
- Topic C
  - Objective 1.4
  - Objective 2.4
  - Objective 2.7
- Topic D
  - Objective 2.7

## TOPIC A

## Create Partitions

  Before you work with the Linux file systems, you should partition the hard disk of your system. Proper partitioning of the hard disk will ensure that users have enough space to store their data. In this topic, you will create and manage disk partitions.

  The hard disk is the most critical component for data storage in any system. Without effective disk partitioning, data on the disk will be unorganized and cluttered. Improper disk partitioning may lead to a system crash. As a Linux+ administrator, it is your responsibility to ensure that the disks are partitioned properly such that users have enough space to store their data in an efficient manner.

## Filesystems

**Definition:**

  A *filesystem* is a method that is used by an operating system to store, retrieve, organize, and manage files and directories on mass storage devices. A filesystem maintains information, such as the date of creation and modification of individual files, their file size, file type, and permissions, and it provides a structured form for data storage. A filesystem by itself does not interpret the data contained in files, because this task is handled by specific applications.

  Filesystems vary depending on several parameters, such as the purpose of the filesystems, the information they store about individual files, the way they store data, and data security.

**Example:**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_100_0.png)

*Figure 3-1:* *Files are stored in directories.*

## Filesystem Labels

  Filesystem labels are assigned to filesystems for easy identification. The labels may be up to 16 characters long and can be displayed or changed using the `e2label` command.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_101_0.png)

Figure 3-2: An example of a filesystem label.

### Syntax

  The syntax for setting filesystem labels is `e2label /dev/{device name}{partition number}`. They can also be set using the `tune2fs -L volume label` command.

## Filesystem Types

  Linux supports many filesystem types. Some common filesystem types are described in the following table.

| Filesystem Type | Description |
| :--- | :--- |
| ext2 | This used to be the native Linux filesystem of some of the previous releases. It is still supported in the current releases of Linux. |
| ext3 | This is an improved version of ext2 and is the native Linux filesystem now. In case of an abrupt system shutdown, ext3 is much faster in recovering data and ensures data integrity. You can easily upgrade your filesystem from ext2 to ext3. |
| reiserfs | This can handle small files efficiently. It handles files smaller than 1K and is faster than ext2. If appropriately configured, it can store more data than ext2. |
| vfat | This is a 32-bit filesystem and supports long file names. It is compatible with the FAT filesystem of Microsoft Windows XP and Microsoft Windows NT. |
| XFS | This is a 64-bit, high-performance journaling filesystem that provides fast recovery and can handle large files efficiently. |
| JFS (Journaled File System) | This is a 64-bit journaling filesystem that is fast and reliable. It is better equipped to handle power failures and system crashes. |
| swap | This is not a true filesystem, but rather is a portion of the hard disk that is used in situations when Linux runs out of physical memory and needs more of it. Linux pushes some of the unused files from RAM to swap to free up memory. |
| ISO 9660 | This is a filesystem standard defined by the International Standardization Organization (ISO), also called as CDFS (Compact Disc File System). Linux allows you to access DVD's and CD's that use this filesystem. |

## Access Other Filesystems

  Linux allows you to access other file systems and mount them when required. However, you cannot install Linux on these filesystems.

| Filesystem | Description |
| :--- | :--- |
| FAT | The FAT (File Allocation Table) filesystem is compatible with different operating systems, including all versions of Windows, MS-DOS, and UNIX. It is primarily used for reformatting floppy disks. |
| NTFS | NTFS (NT File System) is the recommended filesystem for Windows-based computers. NTFS provides many enhanced features over FAT or vfat, including file- and folder-level security, file encryption, disk compression, and scalability to very large drives and files. |

## Partitions

**Definition:**

  A *partition* is a section of the hard disk that logically acts as a separate disk. Partitions enable you to convert a large hard disk to smaller manageable chunks leading to better organization of information. A partition must be formatted and assigned a filesystem before data can be stored on it. Partitions are identified using a partition table, which is stored in the boot record. The partition table can contain entries for a maximum of four primary partitions. Partitions can be classified into primary and extended partitions. The size of each partition can vary, but cannot exceed the total free space of the hard disk.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_102_0.png)

Partitions

### Example:

![](img/477ccb2f05b6ba1b2d563ea74f18c197_103_0.png)

Figure 3-3: Partitions on a hard disk.

## Hard Disk Size Specification

  Before proceeding with the installation process, you need to plan the hard disk layout based on your requirements. Each partition has a recommended size specification. The following table lists the recommended size specification for partitions.

| Partition | Recommended Size |
| :--- | :--- |
| / | Minimum 1 GB. |
| /boot | 100 MB. |
| swap | Double the RAM size. |
| /var | Minimum 250 MB. If the possibility of the installation of many applications exists in the future, allocate the appropriate size. |
| /home | Varies based on the number of users. |

## Disk Partitioning

  Most operating systems, including Linux, use disk partitions. Data of different types can be stored in separate locations on the hard disk. The partition size can be specified by a user. However, the filesystem size must be considered before specifying the partition size. Disk partitioning enables the user to separate system files from user accessible ones. Corrupted partitions do not affect the other partitions, and they can be recovered separately.

## Partition Types

![](img/477ccb2f05b6ba1b2d563ea74f18c197_103_1.png)

  There are three types of partitions: primary, extended, and logical. Functioning of the hard disk depends on the types of partitions on it. The recommended protocol for partitioning a hard disk is three primary partitions and one extended partition with any number of logical partitions within.

  Each partition has a set of specific features. The three types of partitions are described in the table.

| Partition Type | Description |
| :--- | :--- |
| *Primary* | A maximum of four primary partitions are allowed. The swap filesystem and the boot partition are normally created in a primary partition. |
| *Extended* | There can be only one extended partition, which can be further subdivided. This partition type does not contain any data and has a separate partition table. |
| *Logical* | A logical partition is created within an extended partition. There is no restriction on the number of logical partitions, but it is advisable to limit it to 12 logical partitions per disk drive. |

## The fdisk Utility

**Definition:**

  An *fdisk* is a menu-driven utility program that is used for creating, modifying, or deleting partitions on a disk drive. Using `fdisk`, a new partition table can be created, or existing entries in the partition table can be modified. The `fdisk` utility understands the DOS and Linux type partition tables. Depending on the partition table created, the DOS FDISK or the Linux `fdisk` program is invoked. The `fdisk` utility also allows you to specify the size of partitions.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_104_0.png)

**Example:**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_104_1.png)

### Syntax

  The syntax of the `fdisk` utility is `fdisk [option] [device_name]`.
