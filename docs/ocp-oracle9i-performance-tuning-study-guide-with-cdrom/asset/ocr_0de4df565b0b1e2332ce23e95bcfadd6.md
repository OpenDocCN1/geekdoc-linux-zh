of a student record with a graduation date of 01-JUN-2001 or later will cause that record to be stored in the P_ERROR partition.

+   - The value specified in the LESS THAN clause must be a literal, a date, or a constant padded by the TO_DATE function. Date values must also use the TO_DATE function to include the century.
+   - Range-partitioned tables cannot contain columns with LONG or LONG RAW datatypes.
+   - Updates that would cause a record to move across partition boundaries are not allowed unless the ENABLE ROW MOVEMENT clause is specified at table creation. Without this clause, attempting to update a student’s graduation date from 16-MAY-95 to 16-MAY-96 would require that the record be moved from partition P_1995 to P_1996 and would not be allowed.
+   - Attempts to insert records that do not fit into any defined partition ranges will cause an ORA-14400: *Insert partition key is beyond highest legal partition key error*. If the P_ERROR partition with the MAXVALUE clause had not been specified, the insertion of a student record with a graduation date of 01-JUN-2001 or later, or value of NULL, would not be allowed.

The selection of GRADUATION_DATE as the table’s partition key is probably ineffective if the number of students who graduate varies considerably each year. If this is the case, then the number of rows stored within each partition will become uneven, with some partitions growing much larger than other partitions. While not always detrimental to performance, this unevenness can cause par-allel operations like Parallel Query and Parallel DML to perform poorly. If this is the case, then Hash partitioning could be considered in place of Range partitioning.

![](bbox=[0.15, 0.74, 0.28, 0.8])

> “Parallel operations are described in greater detail in Chapter 10, ‘Operating System Tuning.’”

# ### LIST PARTITIONING

*List partitions* are similar to Range partitions except they are based on a set of specified values rather than a range of values. For example, suppose