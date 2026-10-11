order to determine into which partition a newly inserted row should be placed.

**Hash Values**  The value that is returned from a hashing algorithm after a value is passed into that algorithm.

**Heap Table**  A table whose rows are not stored in any particular order. Instead, the row storage order is determined by the order in which available blocks came on and off the free list.

**High Water Mark**  The block ID of the highest block number used to store data for a table. All blocks up to the high water mark block are read during a full table scan.

**Hints**  Keywords which, when embedded within comments in SQL statements, cause the Oracle optimizer to behave in a specified manner.

**Histogram**  Statistics that are used to inform the Cost Based Optimizer of the actual distribution of data within a particular column.

**Hit Ratio**  A calculation of how frequently users are finding their requested SQL and data buffers to already be cached in memory.

**Immediate Latch**  A latch type that immediately retries obtaining a previously busy latch without waiting.

**Index Cluster**  A technique for storing the data from one or more tables in the same physical block.

**Index Organized Table (IOT)**  A table whose data is physically stored in the same B-Tree structure found in indexes.

**init.ora**  The physical file that contains the database and instance configuration parameters.

**Instance**  The collection of memory structures associated with an Oracle database. These structures include the System Global Area and all the Oracle background processes (e.g., PMON, SMON, etc.).