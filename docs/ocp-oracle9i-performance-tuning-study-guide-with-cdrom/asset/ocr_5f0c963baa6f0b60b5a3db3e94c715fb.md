# Indexing Partitioned Tables

After a range, list, hash, or composite partitioned table has been created, it should be indexed in order to take maximum advantage of the performance enhancing benefits of partitioned tables. Proper indexing of partitioned tables will also improve the manageability of the indexes when performing routine index maintenance tasks described earlier in this chapter. There are two methods of classifying partitioned indexes. The first category, *local versus global* indexes, is related to whether the index’s partitioning structure matches that of the underlying, indexed table.

Local Partition Indexes Partitioned indexes are said to be local when the number of partitions in the index match the underlying table’s partitions on a one-to-one basis. Therefore, if a table contains four partitions, the local index on that table will also contain four partitions, each indexing one of the four table partitions. Figure 3.25 illustrates the relationship between a local partitioned index and its associated partitioned table. When examining the above structure, several guidelines related to local partition indexes should be considered:

+   - Local partitioned indexes can use any of the four partition types.
+   
+   - Oracle automatically maintains the relationship between the table’s partitions and the index’s partitions. If a table partition is merged, split, or dropped, the associated index partition will also be merged, split, or dropped.
+   
+   - Any bitmapped index built on a partitioned table must be a local index.

# FIGURE 3.25 Relationship between local partitioned indexes and tables

![](bbox=[0.28, 0.75, 0.82, 0.95])