
servers. Instead of running a heavy Web server off just one computer, then, LVS spreads the work across several computers. Provided the LVS router has fast enough network interfaces, the result is an improvement in speed and reliability.

LVS provides for floating server IP addresses. The LVS router has a fixed IP address for the outside world. The IP address will be assigned to either the primary LVS router or its backup and will automatically be transferred if the machine to which it is assigned goes down (a process known as failover). In this instance, the IP address and the routing tables are synced over the downed machine by the lvs daemon, which handles communication between the two machines. The pulse daemon runs on all LVS machines to allow the secondary node to determine whether the primary node is active. The ipvadm command is the command-tool for administering the LVS machines in the cluster.

# Figure 2.1 LVS cluster topology

![](img/4fb617eb648f87def380ef5d92052d01_54_0.png)

# Chapter 2 Installing Linux

The rest of the cluster consists of real server machines to which FTP or HTTP services are requested via the LVS machines' second network card. The LVS router runs one daemon for each FTP or HTTP server running on each real server. This LVS router daemon will connect to the port of the real server to ensure that the system is still available to take the FTP or HTTP requests. Load balancing between the real servers may be simple based on server's turn it is, or can be sophisticated enough to qualify as true load balancing. For more information about this type of cluster, refer to http://www.linuxvirtualserver.org Web site.

# Disk Subsystems

Disk I/O is another potential bottleneck for systems that require very high performance. Disk access is measured in milliseconds, RAM in nanoseconds. The two basic techniques for making disk I/O more efficient are RAID (Redundant Arrays of Inexpensive Disks) and disk caching, both described below. The method you choose depends entirely on your specific situation. A RAID array, which requires a significant hardware investment, may or may not give you significant gain; maximizing your disk cache is almost always a good thing.

There are six different levels of RAID, all of which use multiple hard disks connected to a single computer to improve speed, reliability, or both. Levels 1–5 are primarily concerned with reliability (data redundancy) and allows multiple copies of the same data on different drives so that if one drive fails, the data is not lost. The different levels vary in performance as measured in read and write times:

- RAID0: This level is specifically aimed at increasing performance and provides no redundancy. In RAID0, data is striped across multiple disks. Striping by several drives appears to the computer system as a single drive. On these drives, the data is distributed into small partitions, intermixed in such a way that the virtual drive seen by the computer is composed of stripes from each drive. This allows simultaneous reads from multiple drives, which can give a significant performance boost.

- RAID1: This level performs mirroring of data, meaning that the same data is stored on all drives. Reads tend to be faster than with a single drive since data can be read simultaneously from both drives. Read-balancing had some problems in Linux kernels, although this has been iron out in the 2.4 kernels. If you wish to take advantage of this, you should probably consider a kernel upgrade. Writes tend to be slower since two copies of the data must be written. RAID1 may mirror data between two local drives or between two different hosts.

- RAID2: Not supported in Linux, RAID2 uses error correction to compensate for drives that do not have built-in error detection. Since most drives include correction now, RAID2 is seldom used.

- RAID3: Not supported in Linux, RAID3 strips the data across all drives at the byte level. Parity information is stored on one of the disks in the array to protect against data loss in the event of a single disk failure.

- RAID4: Similar to RAID3, except that the data is striped at the block level. Parity is maintained on one disk as in RAID3. This causes the parity disk to be the bottleneck.

- RAID5: Similar to RAID4, except that parity is split between all the disks in the array. RAID5 array can withstand a single disk failure. Write performance is significantly slower since a single write operation requires old data and parity to be read from each disk, the new parity to be calculated, and the new data and parity to be written to each disk. The improvement in reading from striping across multiple spindles goes a way offsetting the overhead of performing the write calculations. It is not unusual for a well-configured RAID5 array to perform as better than the individual disks.

RAID can be implemented in hardware or software. The hardware implementations are extremely fast and costly. The software implementations, on the other hand, are relatively inexpensive. As kernel 2.2, which is standard for Red Hat 7.0, RAID0, RAID1, and RAID4 can be configured. There is also an option to auto-detect RAID; this works by detecting any partitions created with partition ID of 0fd, as opposed to the usual partition type code of 83 (You can check or change partition type with the Linux disk utility, as described in Chapter 1.)

To see what RAID support you have already installed, look at /proc/mdstat. If you are not running any of the RAID modules that exist in /lib/modules/block, the file will not exist or will contain the following:

Personalities: []
read_ahead not set
unused devices: none

![](img/4fb617eb648f87def380ef5d92052d01_56_0.png)

# Selecting Hardware 29

If you have any RAID modules running, you'll see the RAID level(s) listed between the brackets after Personalities. NOTE: Just because RAID support is present on your system doesn't necessarily mean that it is being used. It's also possible to use RAID on some disks but not on others. Let's assume a case where to stripe data (RAID0) across two partitions that you marked as RAID when you created them. We are using IDE here, but SCSI also works. Now you need to configure the /etc/raidtab file for your particular configuration. On the standard Red Hat 7.0 system, this file won't exist until you create it. There are several examples you can use; look at the raidtab file for one of them. Listing 2.1 is a sample /etc/raidtab file, tailored to our scenario.

# Listing 2.1 A Sample /etc/raidtab

| Field | Value | Comment |
| :--- | :--- | :--- |
| raiddev | /dev/md0 | RAID device name |
| raid-level | 0 | RAID level |
| nr-disks | 2 | # of raid disks |
| persistent-superblock | 1 | use superblock |
| chunk-size | 8 | stripe size bytes |
| device | /dev/da9 | partition |
| raid-disk | 0 | index |
| device | /dev/db6 | partition |
| raid-disk | 1 | index |

The /etc/raidtab file uses C-style comments—anything between /* and */ is a comment and is ignored by the system. Important elements of Listing 2.1 include:

- raid-level: The RAID level, as described above.
- nr-disks: The number of disks in the RAID array.
- chunk-size: The number of bytes that go into each stripe.
- device: For each disk (up to the value specified for nr-disks), you must specify a Linux partition device file to be used in the disk array. These partitions don't need to be in equivalent positions on the physical disks—for instance, in Listing 2.1, the array uses /dev/da9 and /dev/db6.
- raid-disk: For each device, you must specify the position in the RAID array—which device is the first in the striping sequence, which is second, and so on. These values are numbered starting with 0.

# Selecting Hardware 31

Now we have our raidtab file set up, we've created the partitions to be auto-detected. Auto-detection is configured into the Red Hat 7.0 kernel by default. Now use the insmod command to start RAID-0 as follows:

```
# insmod raid0
```

Finally, you need to run the mkraid command to configure your RAID-0 array and format the disk for use.

```
# mkraid
# mkext2 /dev/md0
```

WARNING: Issuing the mkraid command destroys any data that might have existed on the partitions specified in the /etc/raidtab file. If you want to convert existing partitions to a RAID configuration, you must first back them up, then do the conversion and restore data.

Disk Caching Disk caching uses system memory to cache disk I/O (input/output). Caching data from the disk into RAM improves performance significantly because RAM access is much faster than disk access. The disk cache stores the most recently used data from the hard drive in a memory buffer that was allocated when the system started. When a program makes a disk read request, the disk caching software intercepts the call and checks the cache buffer to see if it contains the required data. If so, the data is read from memory instead of the disk. Buying hard drives with lower access times and activating disk caching in your BIOS settings will give you significant performance gains.

The effectiveness of a cache is pretty much determined by its size. If the cache is too small, the data is often flushed before it is even reused, rendering the cache useless. A cache that is too large uses free memory and can cause the system to swap to disk, which is also slow. Linux uses all free RAM as a buffer cache, but this cache is automatically reduced in size when additional memory is required by an application. There is no configuration required.

# Types of Hardware to Avoid

Just as there are types of hardware that can make your system more efficient or easier to use, there are types that can make it less so. Some hardware devices will actually slow the system down, while others simply will be hard to support.
