Global Partition Indexes Partitioned indexes are said to be global when the number of partitions in the index do not match the underlying table’s partitions on a one-to-one basis. For example, if a table contains four partitions, its global index may be comprised of only two partitions, each of which may encompass one or more of the table partitions. Figure 3.26 illustrates the relationship between a global partitioned index and its associated partitioned table.

# FIGURE 3.26 Relationship between global partitioned indexes and tables

![](bbox=[0.3, 0.3, 0.76, 0.53])

When examining the above structure, several guidelines related to global partition indexes should be considered:

+   - Although global indexes can be built on a range, list, hash, or composite partitioned table, the global partitioned index itself must be Range partitioned.
+   
+   - The highest partition of a global index must be defined using the MAXVALUE parameter.
+   
+   - Performing maintenance operations on partitioned tables can cause their associated global indexes to be placed into an invalid state. Indexes in an invalid state must be rebuilt before users can access them.

![](bbox=[0.13, 0.81, 0.2, 0.88])

To avoid inadvertent index invalidation, Oracle recommends the use of local indexes over global indexes whenever possible.