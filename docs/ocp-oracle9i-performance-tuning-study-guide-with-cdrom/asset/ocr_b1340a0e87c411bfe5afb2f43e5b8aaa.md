# Monitoring indexes to determine usage

# Oracle Objective

# Identifying Unused Indexes

Depending on the execution plans the optimizer chooses, some application indexes may never be utilized while application users are performing their work. If an index is not being used, then dropping it may improve performance by eliminating the overhead of the index maintenance when DML is performed on the indexed table. Dropping unused indexes will also free up tablespace for use by other indexes. Oracle9i introduces a new data dictionary view, V$OBJECT_USAGE, that can be used to identify unused indexes. The technique for monitoring index usage is briefly described here:

You can use the following command to activate monitoring on an index called EMP_LAST_NAME_IDX:

```
ALTER INDEX hr.emp_last_name_idx MONITORING USAGE;
```

After a period of normal user activity, you can disable the monitoring using the following command:

```
ALTER INDEX hr.emp_last_name_idx NOMONITORING USAGE;
```

You can then query the INDEX_NAME and USED column in the V$OBJECT_USAGE dynamic performance view to determine whether the index was accessed during the monitoring period. A YES value in the USED column indicates that the index was accessed at least once during the monitoring period. A value of NO in the USED column indicates that the index was not accessed during the monitoring period and may be a candidate for dropping.

# Partitions

Another technique for reducing the amount of I/O during query execution is to divide the table data into smaller subsets, called *partitions*. Once properly partitioned, indexed, and analyzed, large table queries will benefit from the CBO’s ability to use partition elimination in order to skip table partitions that do not contain relevant data. In addition, many table maintenance