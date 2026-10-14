
errors, and for physical disk errors as well. You should not have to run chkdsk unless you are experiencing unusual file system problems. There are two common ways to run chkdsk:

- To have chkdsk scan and repair drive C: for filesystem errors, use the following syntax:
```
chkdsk C: /f
```

- To have chkdsk scan and repair drive C: for filesystem and physical media errors, use the following syntax:
```
chkdsk C: /f /r
```

Keep in mind that chkdsk cannot operate on volumes that are currently in use. If you need to run chkdsk on a volume currently in use (i.e. the System partition), you should execute one of the above commands, answer yes when prompted to run chkdsk during the next reboot, and then reboot the system. chkdsk will run at the time of the next reboot.

chkdsk scans a volume for filesystem errors and for physical errors.

## NTFS FAULT TOLERANCE

NTFS is one of the few filesystems that supports advanced volume configuration and fault tolerance. NTFS is compliant with the Redundant Array of Inexpensive Disks (RAID) standard. All of the advanced volumes, except volume sets, are RAID-compliant. There are two non-fault-tolerant configurations: volume sets and stripe sets. NTFS also provides two fault-tolerant configurations: mirror sets and stripe sets with parity. This section will discuss the attributes of all four configurations. In every case, the Disk Administrator is used to manage the various disk configurations. The different RAID levels are described in Table 4.5.

### Volume Sets

Volume sets are created from up to 32 areas of free space of varying size located on one or more physical volumes. Data is written to volume sets sequentially and a volume set performs almost identically to a single partition on a single disk. Volume sets are useful because they can be expanded without losing any of the data contained on them. However, volume sets do not provide any fault tolerance and if one of the disks contained in the volume set is damaged, the entire volume set is corrupted.

### Stripe Sets

Stripe sets are created from two or more areas of identically-sized free space on one or more physical volumes. Stripe sets are typically created from two or more identically-sized disks. When data is written to a stripe set, it is broken into equal-sized chunks and one chunk is written to each of the disks in the stripe set. Read and write accesses to a stripe set are very fast because the data is being streamed from multiple disks (and possibly multiple disk controllers). Stripe sets cannot be expanded without losing the data contained in the set. Stripe sets do not provide any fault tolerance, so a single disk failure will cause all of the data to be lost. A stripe set corresponds to RAID Level 0.

| Table 4.5 RAID Levels Supported on Windows 2000 |
|---|---| 
| RAID Level | Description |
| 0: (Striping) | RAID Level 0 allows you to combine two or more disks of equal size into a larger logical volume. Data is written in equal-sized chunks to each disk in the volume. There is no redundancy in this configuration, but disk reads and writes are faster because multiple disks are being accessed concurrently. |
| 1: (Mirroring) | RAID Level 1 allows data from one physical disk to be duplicated to a second physical disk. In the event that the primary disk fails, the secondary disk can take the place of the primary disk with no data loss. |
| 5: (Striping with Parity) | RAID Level 5 provides similar functionality to RAID Level 0. However, this level provides redundancy when a single disk fails. A RAID 5 volume can be established using three or more disks of equal size. The actual size of the volume will be the number of disks minus one multiplied by the size of the disk. The reason for the "loss" of one disk is to store parity information so data can be regenerated if a disk fails. While read performance is better with RAID 5, write performance is slower that RAID 0 because parity information is generated and stored with each write. |

### Mirror Sets

A mirror set is created from two identically-sized disks. In a mirror set, both disks contain the exact same data. In the event of a disk failure, the mirror set can be broken and the good disk can be brought on-line as if nothing had ever happened. Once the damaged disk is replaced, the mirror
