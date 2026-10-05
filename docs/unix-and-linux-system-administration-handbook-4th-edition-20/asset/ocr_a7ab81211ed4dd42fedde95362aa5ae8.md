# Exhibit B Storage management layers

| Filesystems, swap areas, database storage |
|---|n| | Logical volumes |
| Partitions | RAID arrays | Volume groups |
| | Storage devices |

+   * **Partition** is a fixed-size subsection of a storage device. Each partition has its own device file and acts much like an independent storage device. For efficiency, the same driver that handles the underlying device usually implements partitioning. Most partitioning schemes consume a few blocks at the start of the device to record the ranges of blocks that make up each partition.

Partitioning is becoming something of a vestigial feature. Linux and Solaris drag it along primarily for compatibility with Windows-partition disks. HP-UX and AIX have largely done away with it in favor of Itanium-based volume management, though it's still needed on Itanium systems.

+   * **RAID array** (a redundant array of inexpensive/independent disks) combines multiple storage devices into one virtualized device. Depending on how you set up the array, this configuration can increase performance (by reading or writing disks in parallel), increase reliability (by duplicating or parity-checking data across multiple disks), or both. RAID can be implemented by the operating system or by various types of hardware.

+   As the name suggests, RAID is typically conceived as an aggregation of bare drives, but modern implementations let you use as a component of a RAID array that acts like a disk.

+   * **Volume groups** and logical volumes are associated with logical volume managers (LVMs). These systems aggregate physical devices to form pools of storage called volume groups. The administrator can then divide this into logical volumes in much the same way that disks of were divided into partitions. For example, a 750GB disk and a 250GB disk could be aggregated into a 1TB volume group and split into two 500GB logical volumes. At least one volume would include data blocks from both hard disks.