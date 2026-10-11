![](bbox=[0.17, 0.11, 0.27, 0.19])

In addition to the above partitioned index types, traditional non-partitioned B-Tree indexes can also be built on partitioned tables. These indexes are referred to as global, prefixed non-partitioned indexes.

# How the Partitioned Tables Affect the Optimizer

Once partitioned tables and indexes have been created, it is up to the cost-based optimizer to decide how to use them effectively when executing application queries. Because the Oracle9i CBO is very “partition aware,” it can eliminate partitions that will not be part of the query result. For example, suppose the following query were performed on the Range partitioned STUDENT_ HISTORY table:

```
SQL> SELECT *
2 FROM student_history
3 WHERE graduation_date = '16-MAY-97';
```

Because of the presence of the table and index partitions, the CBO will know that only one partition (P_1997) will need to be accessed to satisfy the query. No other partitions will even need to be considered. This quick elimination of unneeded partitions to improve query performance is referred to as partition pruning.

![](bbox=[0.17, 0.58, 0.27, 0.66])

The CBO cannot prune table partitions if the query applies a function to the partition key column. The CBO cannot prune index partitions if the query applies a function to the partition key column on a non-function based index.

Partitioned tables and indexes also help the CBO develop effective execution plans by influencing the manner in which joins are performed between two or more partitioned tables. When performed in parallel using Oracle Parallel Query, there are two possible join methods that are considered by the CBO: full partition-wise joins and partial partition-wise joins. Partition-wise joins occur any time two tables are joined on their partition key columns. Partition-wise joins can be performed either serially or in parallel. Partial partition-wise joins occur any time two tables are joined on the partition key columns of one of the two tables. Partial partition-wise joins can only be performed in parallel. Each of these join types reduces the overall CPU and memory utilized to service a query, particularly on very large partitioned tables.