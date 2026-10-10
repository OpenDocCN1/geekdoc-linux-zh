![](bbox=[0.08, 0.06, 0.57, 0.2])

Selecting a disk space segment for mirroring

operation in the event of a controller card failure. For example, to provide maximum speed and reliability, Eric used two 60 GB drives attached to separate controller cards on the UASHOST server to duplex the SYS and CORP partitions (see Figure 3-6). If one of the drives or controllers fails, the system continues reading and writing to the other drive. When the problem is fixed, NetWare automatically rebuilds the new drive so that the two drives are the same.

![](bbox=[0.09, 0.36, 0.78, 0.71])

Duplexing partitions

The process of using Remote Manager to enable duplexing is the same as mirroring; the only difference is that the two partitions are located on disks attached to different controller cards.

# Storage Pools

After a disk has been partitioned, the next job in setting up an NSS file system is creating one or more storage pools. As shown in Figure 3-7, storage pools are created from disk partitions and can be extended by adding disk partitions. When a disk partition is added to a storage pool, the amount of free space in the pool is increased by the size of the disk partition. If you're adding a new disk partition from a second drive to an existing storage pool, you should consider mirroring or duplexing the new partition on another disk to