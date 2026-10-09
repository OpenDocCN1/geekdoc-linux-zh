Typically, well-known and tested Linux applications run for long periods of time with no problems. Some Linux systems running today have not been rebooted in months, and can possibly run several more months without having to restart.

# File System Problems

File system problems can cause software to fail. For example, if a file system loses information about a configuration file, the software may not start or it may start with default options. File system problems can cause data files or application files to be damaged, or directories to be corrupted.

**RAID** The best solution to file system problems is to have redundant disk drives. Usually this is done with some kind of Redundant Array of Inexpensive Disks (**RAID**) implementation. RAID can be software- or hardware-based. Hardware-based RAID is accomplished at the hardware level and does not take any processing power away from the Linux operating system. Software-based RAID relies on the computer’s processing power to accomplish its tasks.

There are six levels of RAID implementation. The most commonly used levels are RAID 0, 1, and 5.

**RAID 0** RAID 0 uses disk striping. One of the real bottlenecks of computer systems is the time it takes to read or write data from or to a hard drive. Disk striping is a technique for spreading data over multiple disk drives. Data is broken up and written to multiple disks concurrently, speeding up the read/write process. Disk striping stores data in one place only and does not offer any protection from disk failure. RAID 0 offers the highest possible performance.

**RAID 1** RAID 1 uses disk mirroring. Disk mirroring is a technique that writes the same data to multiple disks. If a disk malfunctions, the system can retrieve the data from the redundant disk. Disk mirroring is used when the data stored is critical and must be accessible at all times. Disk mirroring is slow on a single device, but on multiple hard disks is barely noticeable. RAID 1 offers good read performance, which will improve with the number of mirrors. Often it is possible to set read policies to optimize read performance within specific environments.

**RAID 2** RAID 2 spreads both data and parity information across multiple physical disks. RAID 2’s data-striping technique doesn’t use disk space efficiently and provides little disk space savings compared with full mirroring. RAID 2 implementations are uncommon.

**RAID 3** Similar to RAID 2, RAID 3 implements data striping but maintains all parity information on one disk for better performance. RAID 3’s disk usage, however, is still inefficient, making RAID 3 implementations rare.

**RAID 4** RAID 4 uses the same data-striping methodology as RAID 2 and RAID 3, but provides better performance by using larger disk blocks. RAID 4 also provides the same single-disk parity storage as RAID 3. RAID 4 is inefficient for transaction-based processing.

**RAID 5** RAID 5 allows you to use multiple hard disks, providing some redundancy (by writing data and parity information) and disk striping. RAID 5 requires three or more disk drives. If one of the disks fails, all data are still intact. If a spare disk is available, the data will be reconstructed with little or no down time. RAID 5 offers pretty good read performance, but typically poor write performance because of the parity calculation required. This problem is somewhat mitigated with modern hardware RAID controllers featuring large amounts of read cache.

RAID disk drives are often hot-swappable. This means that a disk drive can be replaced without having to shut down the computer system.

Some implementations use **RAID 0+1**, RAID level 0 combined with RAID level 1. This provides redundancy and striping by writing all data to four or more drives. RAID 0+1 provides higher performance than RAID 5.