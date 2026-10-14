# 14.1.1.1 Physical Disk

Physical disks are just what you think they are: hard disk drives. However, a physical disk in LSM terms can be just a partition on a disk. One or more disks/partitions can be managed by LSM in a “pool” or disk group. A disk group is a bunch of disks/partitions grouped together, generally by their intended function (i.e., a database disk group). While you can have more than one disk group, there must be at least one disk group, the root disk group (rootdg). See Figure 14-4.

When a disk/partition is brought under the LSM’s control, it can be treated as one of three types of LSM disks:

+   - sliced disk
+   - simple disk
+   - nopriv disk

A sliced disk is the default disk type that is used when an entire unused disk is brought under the LSM’s control. The sliced disk consists of two partitions: one partition is used for private LSM metadata, and the other partition is used for user data (also known as public data). The default size for the private metadata partition is 4096 blocks.

A simple disk is the default disk type that is used when an unused partition of a disk is brought under the LSM’s control. The simple disk consists of the single partition with the beginning of the partition used for private LSM metadata; the remainder of the partition is used for user data.

A nopriv disk is the default disk type that is used when a disk or partition that contains user data is encapsulated into LSM. The nopriv disk does not contain any LSM-specific data.

# 14.1.1.2 Subdisk

A subdisk is a set of contiguous disk blocks on a physical disk. A subdisk can be the whole disk or just a part of a disk.

# 14.1.1.3 Plex

A plex is composed of one or more subdisks. There are two categories of plexes:

+   - Data
+   - Log

A data plex is used to hold the volume’s data and can be:

+   - Concatenated (writes to the subdisks are done sequentially).
+   - Striped (RAID0).
+   - RAID5 plex.

A concatenated plex can be composed of subdisks of different sizes. Striped and RAID5 plexes should be composed of subdisks that are sized in multiples of the stripe width (64K by default) to avoid splitting I/O requests unnecessarily.

Figure 14-5 illustrates the differences between a concatenated plex and striped plex.