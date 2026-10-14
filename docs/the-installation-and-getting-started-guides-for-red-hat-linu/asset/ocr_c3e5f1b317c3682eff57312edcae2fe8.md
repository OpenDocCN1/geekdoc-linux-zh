# Appendix B: An Introduction to Disk Partitions

clutter. On the technical side, some filesystems were never designed to support larger drives. Or the filesystems could support larger drives, but the overhead imposed by the filesystem became excessive. The solution to this problem was to divide disks into partitions. Each partition can be accessed as if it was a separate disk. This is done through the addition of a partition table.

Please Note: While the diagrams in this chapter show the partition table as being separate from the actual disk drive, this is not entirely accurate. In reality, the partition table is stored at the very start of the disk, before any filesystem or user data. But for clarity, we'll keep it separate in our diagrams.

![](bbox=[0.22, 0.42, 0.72, 0.73])

# Figure B-5: Disk Drive with Partition Table

As Figure B-5 shows, the partition table is divided into four sections. Each section can hold the information necessary to define a single partition, meaning that the partition table can define no more than four partitions.