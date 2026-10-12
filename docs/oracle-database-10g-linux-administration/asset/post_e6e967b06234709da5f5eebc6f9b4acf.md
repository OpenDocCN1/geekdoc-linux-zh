
## The Index Clustering Factor

The index clustering factor is the relationship between the rows in each index leaf-level block and how many different table data blocks they make reference to. The cost-based optimizer (CBO) makes decisions on execution plans based on this relationship. If the clustering factor is high, the CBO will probably choose to do a full scan on the table rather than incur the additional I/O of using the index.

If the table is in a particular order in a column and there is an index on that same column, then the clustering factor would be low, since there would be many key values in the index pointing to the same table data block. Conversely, if the table was in sequence by a primary key value and there was an index on birthdate, for example, this index would probably have quite a poor clustering factor, since each birth-date key value would point to a row in a different data block. If Oracle were to range-scan across the index looking for all the employees with a particular birth date, Oracle might have to read each block in the underlying table several times, versus just doing a full scan on the table to begin with.

> **NOTE**
> A good clustering factor is when the clustering factor
> is close to the number of data blocks in the table. A
> poor clustering factor is when the clustering factor is
> close to the number of rows in the table.

> **TIP**
> The best range-scan performance is to have the table
> sorted and loaded in the sequence of a major query
> used by the application and have an index or multikey
> index but with the leading key column being the
> column that the table is in sequence by. Data design
> plays a key role in application performance.

If the clustering factor is not good, Oracle will only use the index for single-row lookups. If the application or SQL accessing the table by this index only does range scans, then Oracle will never use the index. Listing 17-3 shows the index_info.sql script that highlights key index information, including the clustering factor. Listing 17-4 shows some sample output from this script. Notice that both tables have 6000 rows and 101 blocks. Both also have the same key values and data values. The first difference to note is the number of key values per leaf block. TABLE1 has 1 key value per leaf block, while TABLE2 has 11 key values per leaf block. The real indicator here is that TABLE1’s clustering factor is very close to the number of blocks in the table, compared to TABLE2’s clustering factor, which is closer to the number of rows in the block. See the preceding Tip for more information on this, but the likelihood of Oracle 10g using the index on TABLE2 is remote at best. Oracle 10g would incur significant amounts of I/O to use this index versus just doing a full table scan.

## Listing 17-3: The Index_Info.sql script

```
* File:             Index_Info.sql
* Type:             SQL*Plus script
* Author:           Jonathan Lewis (www.jlcomp.demon.co.uk)
                    Enhanced by Dan Hotka
* Date:             May 9, 2003
*
* Description:
*
                    This script lists statistics about indexes.
*
*
* Modifications: 10-22-03 Added Table Block and Row info
*
/****/ 
column table_name format a15 heading 'Table'
column index_name format a15 heading 'Index'
column num_rows format 999,999 heading 'Rows'
column num_blocks format 999,999 heading 'Data Blocks'
column avg_data_blocks_per_key format 999,999 heading 'Data Blks per Key'
column avg_leaf_blocks_per_key format 999,999 heading 'Leaf Blks per Key'
column clustering_factor format 999,999 heading 'Clust Factor'

SELECT i.table_name, i.index_name, t.num_rows, t.blocks,
       i.avg_data_blocks_per_key, i.clustering_factor,
       to_char(o.created,'MM/DD/YYYY HH24:MI:SSSSS') Created
  FROM user_indexes i, user_objects o, user_tables t
 WHERE i.index_name = o.object_name
   AND i.table_name = t.table_name
 order by 1;
```

## Oracle 10g Partitioning

Partitioning is a way of dividing large amounts of data across multiple disk devices by a key value. The cost-based optimizer recognizes a partitioned object (tables and/or indexes) and can select the required data from just the correct partition (known as **partition pruning**) rather than searching the entire object. There are a couple of reasons for doing this: SQL performance and ease of maintenance.

Partitions can greatly aid in the maintenance of larger objects. Partitioning subdivides data across tablespaces. These tablespaces are the regular Oracle 10g type of tablespaces in that they can be backed up while available, restored without affecting the other partitions, loaded without affecting the other partitions, dropped, added, and so on.

SQL performance can be enhanced by considering how the data is partitioned and whether the SQL is specifically asking for a subset of the data that follows the partitioning boundaries.

The particular criteria used to partition data can have a dramatic effect on the performance of SQL used to query the data. Well-designed partitioning schemes can improve the performance of queries against subsets of the data many times over.

This section will cover the syntax and performance implications of Oracle 10g partitioning.

### Oracle 10g Partitioning Features

Oracle 10g offers four major kinds of partitioning. Each option has particular features and some limitations, and each type utilizes a key value known as the **partition key**. Indexes can be partitioned on the value of the partition key, or on a different value in the table, and can use the same partitioning parameters or different partitioning parameters.

There are two main reasons to consider partitioning: performance and maintenance. Performance can be enhanced by splitting the data and index structures across multiple physical devices. This allows for multiple processes to be using different parts of the objects without any contention with other processes. Smaller objects scan more quickly, and partitioning also allows for objects to be nicely split across hardware devices according to a key value. This is a way of “stripping” or putting different parts of the object on various devices. Performance is enhanced only if the applications and partitioning structures are planned carefully. Oracle’s optimizer can see what a SQL statement is going to request, and can also see the way that partitioning has been implemented. The application has no control over how a hardware device would do its striping. Other methods of data striping include using smaller database files assigned to a tablespace. Again, the application has little control over which datafile will contain the desired data.

Maintenance times can also be improved using partitioning. It is very easy to add and drop partitions, as well as back up and recover single partitions. Data that can be periodically purged can easily be both removed or re-added using partitioning if the need arises. Backup and recovery can happen more quickly because the objects themselves are smaller when partitioned (that is, each partition is like its own object, where the object itself becomes a logical entity, while the partition level is the actual object itself).

Range partitioning is where each partition is loaded with data that meets a certain range of numeric or date values. Hash partitioning evenly distributes the numeric or date partition key values across the available partitions on the basis of a hash value computed on the partition key. Composite partitioning is a combination of range and hash partitioning: the data are partitioned based on a range of values and are then assigned to subpartitions on the basis of a hash value. This feature gives Oracle the ability to store and access only parts of the data by the partitioning key, but the data can subsequently be evenly distributed across a series of subpartitions. List partitioning allows for the partitioning of character data.

> **NOTE**
> Oracle 10g supports the use of multiple block sizes for different tablespaces. The tablespaces of a partitioned object (table or index) must all have the same block size per object. However, the table and index can use different block sizes.

### Range Partitioning

Range partitioning distributes rows across the assigned tablespaces according to one or more columns in the table that become the partition key. Listing 17-5 shows an example of range partitioning syntax. Notice the PARTITION BY RANGE clause. This defines the partition key. Each partition is then named specifying the LESS THAN value, which dictates the data that will be stored in this partition.

> **TIP**
> Each partition can be accessed by its partition name (in place of the table name in the SQL statement). This would give the application the ability to function on other partitions when one partition is having a recovery issue.
