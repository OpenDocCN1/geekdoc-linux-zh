# ## Using RAID disks

RAID (Redundant Arrays of Independent Disks) is spreads the data used on a computer across multiple disks, while appearing to the operating system as if it is dealing with a single disk partition. Using the different RAID specifications, you can achieve the following advantages:

+   * **Improved disk performance** — RAID0 uses a feature called *striping*, where data is striped across multiple RAID partitions. Striping can improve disk performance by spreading the bits on a computer’s file system across multiple partitions, which are presumably on multiple hard disks. However, striping does not provide redundancy.

+   * **Mirroring** — RAID1 uses partitions from multiple hard disks as mirrors. That way, if one of the partitions becomes corrupted or the hard disk goes down, the data exists on a partition from another disk because it has continuously maintained an exact mirror image of the original partition.

+   * **Parity** — Although striping can improve performance, it can increase the chance of data loss, since any hard-disk crash in the array can potentially cause the entire RAID device to fail. Using a feature called *parity*, information about the layout of the striped data is kept so that data can be *reconstructed* if one of the disks in the array crashes. RAID3, 4, and 5 implement different levels of parity.

During installation of Fedora or RHEL, you can use the Disk Druid window to create RAID0, RAID1, and RAID5 disk arrays. The following procedures describe how to set up RAID disks during installation.

Before you begin creating RAID partitions when you install Fedora or RHEL, you will probably want to start with a computer that has two or more hard disks. The reason is that, if you don’t have multiple hard disks, you won’t get the performance gains that come from spreading the bits on your computer among multiple disks. Likewise, mirroring will be ineffective if all RAID partitions are on the same disk because the failure of a single hard disk would still potentially cause the mirrored partitions to fail as well.

For example, you might begin with 30GB of free disk space on your first hard disk (`/dev/sda`) and 30GB of free disk space on your second hard disk (`/dev/sdb`). During the Fedora or RHEL installation procedure, select to partition your disk with Disk Druid. Then follow this procedure:

+   1. From the Disk Setup (Disk Druid) window, click the RAID button. A RAID Options window appears.

+   2. Select **Create a Software RAID Partition**, and click OK. The Add Partition window appears.

+   3. With Software RAID selected as the File System Type, choose the drive you want to create the partition on and choose the *size* (in megabytes). Then click OK.

+   4. Repeat Steps 2 and 3 (presumably creating software RAID partitions on different hard disks until you have created all the RAID partitions you want to use).