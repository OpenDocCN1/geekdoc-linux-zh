
We recognize that you are eager to start the implementation of TruCluster Server right away. But wait. Take a minute and think about what you are about to do.

Take your eagerness to start and channel it into planning the devices that you will use for the initial Tru64 UNIX system disk and the eventual TruCluster Server system disks.

## 4.2.1 Planning the Tru64 UNIX System Disk

Very often, we hear from Systems Administrators – both experienced and inexperienced – that "Planning the initial Tru64 UNIX systems disk is not a big deal, especially if we will be installing and configuring TruCluster Server. After all, once the installation and configuration of TruCluster Server is complete, we’ll never use that original Tru64 UNIX system disk again. In fact, we can just "nuke" that old system disk and use that space for something constructive like another scratch area."

While it is true that the initial Tru64 UNIX system disk is used to build the TruCluster Server environment and then little used later, it should be retained and used as an "Emergency Repair" disk. Additionally, you can utilize the swap partition and/or configure a separate, local /tmp file system on this disk for use within the cluster to remove additional I/O from the shared buses, since both swap and /tmp are used on a per member basis as of this writing¹.

The Emergency Repair disk is essential to the repair and recovery of your cluster configuration should you encounter any problems in the future. For more information on the Emergency Repair disk, please refer to Chapter 22 on Cluster Maintenance and Recovery.

In any event, the importance in planning the Tru64 UNIX system disk should not be minimized. This system disk can still play an active role in the day-to-day operation of your cluster and can play an essential role in the recovery of a cluster should problems occur.

As an aside, while this discussion and the discussions in the Tru64 UNIX Installation guides suggest using a local disk for the initial Tru64 UNIX installation, this is not a hard and fast rule. Disk devices on the shared bus may also be used for the initial Tru64 UNIX installation system disk.

### 4.2.1.1 How Much Space Is Enough?

Determining the disk partition sizes for each of the operating system’s file systems is based on the software subsets that are to be installed and the usage of the file systems. The amount of space occupied by the software subsets can be easily determined ahead of time. This information is contained in the Release Notes for the version of the Tru64 UNIX that is to be installed. The amount of space to be used for each file system, based on actual daily usage, is usually discovered through experience so this information is usually harder to come by.

According to the Tru64 UNIX Installation guide, if you were to use a disk that is greater than 3 GB, the partition sizes used for: root (/) should be 384 MB, swap should be 384 MB, and /usr (including the /var) should be 2.235 GB. Based on the software subset sizes from the Tru64 UNIX Release Notes for version 5.1A, if all the software subsets from the Tru64 UNIX Operating System CD, the Associated Products Vol. 1 CD, and Associated Products Vol. 2 CD were to be installed, the amount of space used for the root (/) file system would be 122.35 MB, /usr would be 3004.86 MB, and /var would be 135.01 MB. We certainly do not recommend blindly installing everything from all of these CDs, but this information provides us with a baseline from which we have derived our own recommendations for partition sizes.

In the TruCluster Server Cluster Installation guide, HP strongly recommends, “that, unless prohibited by site policy, you load all subsets when installing the Tru64 UNIX system.” Alternatively, you might consider installing only those software subsets that are needed to support your hardware configuration and/or that you expect your users will need based on the requirements for the implementation of your system. This approach to installing Tru64 UNIX can enhance basic system security and availability, and will be discussed in more depth in Chapter 5.

Our recommendations for the partitions used for the initial Tru64 UNIX disk are presented in Table 4-1.

We know, you are looking at this table and thinking to yourself that the sizes of these partitions are quite large. Well, given that 18 GB hard drives are now under $1,000, think of this as you would a rather inexpensive insurance policy – you may not think you need it but when you do, you will be quite happy to have it. Actually, the sizes of these system disk partitions are closely representative of implementations on clustered systems that we have seen.

¹ See Chapter 21 on configuring a separate /tmp file system.

### 4.2.1.2 Partitioning and Disk Layout

Obviously, the disk that you will use for the initial Tru64 UNIX installation will most likely differ from the disk we will use in our examples. This is to be expected, as you will probably use the latest and greatest disks available for your configuration. With this in mind, please use the partition sizes in our examples and recommendations as a starting point. Additionally, when considering your own Tru64 UNIX system disk layout, be sure to include space for other software components that you

| Disk Partition | Size | File System Type | File System | Usage by Tru64 UNIX or TruCluster Server |
|---|---|---|---|---|
| a | 512 MB | AdvFS | / | Tru64 UNIX |
| b | 2 to 3 times size of memory | swap | swap | Optionally Both |
| f | 2 GB | AdvFS | /tmp* | Optionally Both |
| g | 3 to 4 GB | AdvFS | /usr | Tru64 UNIX |
| h | 1 to 2 GB | AdvFS | /var | Tru64 UNIX |

* - See Chapter 21 on configuring a separate /tmp file system.

Table 4-1: Standalone Operating System Disk Partition Layout
