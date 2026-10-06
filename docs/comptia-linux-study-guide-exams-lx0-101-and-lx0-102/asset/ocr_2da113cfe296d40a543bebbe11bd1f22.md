# Designing a Hard Disk Layout

Partitions can be mounted just anywhere in the Linux directory tree, including directories on the root partition as well as directories on mounted partitions. For instance, if /home is a separate partition, you can have a /home/morehomes directory that serves as a mount point for another partition.

The upcoming section "Mounting and Unmounting Filesystems" describes the commands and configuration files that are used for mounting partitions. For now, you should be concerned only with what constitutes a good filesystem layout (that is, what directories you should split off into their partitions) and how to create these partitions.

# Common Partitions and Filesystem Layouts

So, what directories are commonly split into separate partitions? Table 3.4 summarizes some choices. Note that typical sizes for many of these partitions vary greatly depending on how the system is used. Therefore, it's impossible to make recommendations on partition size that will be universally acceptable.

TABLE 3.4 Common partitions and their uses

| Partition (mount point) | Typical size | Use |
|---|---|---|
| Swap (not mounted) | One to two times the system RAM | Serves as an adjunct to system RAM; is slow but enables the computer to run more or larger programs. |
| /home | 200MiB–3TiB (or more) | Holds users' data files. Isolating it on a partition preserves user data during a system upgrade. Size depends on the number of users and their data storage needs. |
| /boot | 100–500MiB | Holds critical boot files. Creating it as a partition circumvents limitations of older BIOSs and boot loaders, which often cannot boot a kernel from a point above a value 504MiB and 2TiB. |
| /usr | 500MiB–25GB | Holds most Linux program and data files; this is sometimes the largest, although /home is larger on systems with many users or if users store large data files. Changes implemented in 2012 are making it harder to create a separate /usr partition in many distributions. |
| /usr/local | 100MiB–3GB | Holds Linux program and data files that are unique to this installation, particularly those that you compile yourself. |
| /opt | 100MiB–5GB | Holds Linux program and data files that are associated with third-party packages, especially commercial ones. |