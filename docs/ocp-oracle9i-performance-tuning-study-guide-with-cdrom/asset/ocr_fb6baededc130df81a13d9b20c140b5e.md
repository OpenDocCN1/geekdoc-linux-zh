# **FIGURE 3.24** Composite partitioned *STUDENT_HISTORY* table

![](bbox=[0.125, 0.14, 0.85, 0.58])

When examining the above structure, several guidelines related to composite partitioning should be considered:

+   - The partitions are logical structures only; the table data is physically stored at the sub-partition level.

+   - Composite partitions are useful for historical, date-related queries at the partition level.

+   - Composite partitions are also useful for pararel operations (both query and DML) at the subpartition level.

+   - Partition-wise joins are also supported through the use of composite local indexes. Glocal local indexes are not supported.

The difference between local and global partitioned indexes is discussed later in the next section.