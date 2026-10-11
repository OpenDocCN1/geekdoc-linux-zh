
## E RAID (Redundant Array of Independent Disks)

### E.1 What is RAID?

The basic idea behind RAID is to combine multiple small, inexpensive disk drives into an array which yields performance exceeding that of one large and expensive drive. This array of drives will appear to the computer as a single logical storage unit or drive.

RAID is a method in which information is spread across several disks, using techniques such as **disk striping** (RAID Level 0) and **disk mirroring** (RAID level 1) to achieve redundancy, lower latency and/or higher bandwidth for reading and/or writing to disks, and maximize recoverability from hard-disk crashes.

The underlying concept in RAID is that data may be distributed across each drive in the array in a consistent manner. To do this, the data much first be broken into consistently-sized "chunks" (often 32K or 64K in size, although different sizes can be used). Each chunk is then written to each drive in turn. When the data is to be read, the process is reversed, giving the illusion that multiple drives are actually one large drive.

#### E.1.1 Who Should Use RAID?

Those of you who need to keep large quantities of data on hand (such as an average administrator) would benefit by using RAID technology. Primary reasons to use RAID include:

-   enhanced speed
-   increased storage capacity
-   greater efficiency in recovering from a disk failure

#### E.1.2 RAID: Hardware vs. Software

There are two possible approaches to RAID: Hardware RAID and Software RAID.

##### Hardware RAID

The hardware-based system manages the RAID subsystem independently from the host and presents to the host only a single disk per RAID array.

An example of a hardware RAID device would be one that connects to a SCSI controller and presents the RAID arrays as a single SCSI drive. An external RAID system moves all RAID handling “intelligence” into a controller located in the external disk subsystem. The whole subsystem is connected to the host via a normal SCSI controller and appears to the host as a single disk.

RAID controllers also come in the form of cards that act like a SCSI controller to the operating system, but handle all of the actual drive communications themselves. In these cases, you plug the drives into the RAID controller just like you would a SCSI controller, but then you add them to the RAID controller’s configuration, and the operating system never knows the difference.

##### Software RAID

Software RAID implements the various RAID levels in the kernel disk (block device) code. It also offers the cheapest possible solution: Expensive disk controller cards or hot-swap chassis^1 are not required, and software RAID works with cheaper IDE disks as well as SCSI disks. With today’s fast CPUs, software RAID performance can excel against hardware RAID.

The MD driver in the Linux kernel is an example of a RAID solution that is completely hardware independent. The performance of a software-based array is dependent on the server CPU performance and load.

#### E.1.3 Some Features of RAID

For those interested in learning more about what software RAID has to offer, here is a brief list of few of those features:

-   Threaded rebuild process
-   Fully kernel-based configuration
-   Portability of arrays between Linux machines without reconstruction
-   Backgrounded array reconstruction using idle system resources
-   Hot-swappable drive support
-   Automatic CPU detection to take advantage of certain CPU optimizations

^1 A hot-swap chassis allow you to remove a hard drive without having to power-down your system.

##### Levels and linear support

RAID also offers levels 0, 1, 4, 5, and linear support. These RAID types act as follows:

-   *Level 0* -- RAID level 0, often called "striping," is a performance-oriented striped data mapping technique. That means the data being written to the array is broken down into strips and written across the member disks of the array. This allows high I/O performance at low inherent cost but provides no redundancy. Storage capacity of the array is equal to the total capacity of the member disks.
-   *Level 1* -- RAID level 1, or "mirroring," has been used longer than any other form of RAID. Level 1 provides redundancy by writing identical data to each member disk of the array, leaving a "mirrored" copy on each disk. Mirroring remains popular due to its simplicity and high level of data availability. Level 1 operates with two or more disks that may use parallel access for high data-transfer rates when reading, but more commonly operate independently to provide high I/O transaction rates. Level 1 provides very good data reliability and improves performance for read-intensive applications but at a relatively high cost^2. Array capacity is equal to the capacity of one member disk.
-   *Level 4* -- Level 4 uses parity^3 concentrated on a single disk drive to protect data. It’s better suited to transaction I/O rather than large file transfers. Because the dedicated parity disk represents an inherent bottleneck, level 4 is seldom used without accompanying technologies such as write-back caching. Although RAID level 4 is an option in some RAID partitioning schemes, it is not an option allowed in Red Hat Linux RAID installations^4. Array capacity is equal to the capacity of member disks, minus capacity of one member disk.
-   *Level 5* -- The most common type of RAID. By distributing parity across some or all of an array's member disk drives, RAID level 5 eliminates the write bottleneck inherent in level 4. The only bottleneck is the parity calculation process. With modern CPUs and software RAID, that isn't a very big bottleneck. As with level 4, the result is asymmetrical performance, with reads substantially outperforming writes. Level 5 is often used with write-back caching to reduce the asymmetry. Array capacity is equal to the capacity of member disks, minus capacity of one member disk.
-   *Linear RAID* -- Linear RAID is a simple grouping of drives to create a larger virtual drive. In linear RAID, the chunks are allocated sequentially from one member drive, going to the next drive only when the first is completely filled. This grouping provides no performance benefit, as it is unlikely that any I/O operations will be split between member drives. Linear RAID also offers no redundancy, and in fact decreases reliability -- if any one member drive fails, the entire array cannot be used. The capacity is total of all member disks.

^2 RAID level 1 is at a high cost because you write the same information to all of the disks in the array, which wastes drive space. For example, you have RAID level 1 set up so that your "root" partition spans across two 4G drives. You have 8G total but are only able to access 4G of that 8G. The other 4G acts like a mirror of the first 4G.

^3 Parity information is calculated based on the contents of the rest of the member disks in the array. This information can then be used to reconstruct data when a disk in the array fails. The reconstructed data can then be used to satisfy I/O requests to the failed disk, and to repopulate the failed disk after it has been repaired or replaced.

^4 (Footnote reference in original text, likely indicates a specific constraint in Red Hat Linux documentation)

### E.1.4 Creating RAID Partitions

RAID is available in both the GUI and kickstart installation modes. You can use `fdisk` or Disk Druid to create your RAID configuration, but these instructions will focus mainly on using Disk Druid to complete this task.

Before you can create a RAID device, you must first create RAID partitions, using the following step-by-step instructions.

**Tip: If You Use fdisk**

If you are using `fdisk` to create a RAID partition, bear in mind that instead of creating a partition as type `83`, which is Linux native, you must create the partition as type `fd` (Linux RAID).

-   Create a partition. In Disk Druid, choose **Add** to create a new partition (see Figure E–1, *Creating a New RAID Partition*).

**Figure E–1 Creating a New RAID Partition**

![](img/eda1471ab4ce718c791c97a85559a478_338_0.png)

-   You will not be able to enter a mount point (you will be able to do that once you’ve created your RAID device).
-   Enter the size that you want the partition to be.
