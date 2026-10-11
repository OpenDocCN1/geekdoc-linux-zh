
## 5.6 Administrative-Level Optimizations

The previous sections describe optimizations that can be performed by unprivileged MySQL users. Administrators who have control of the MySQL server or the machine on which it runs can perform additional optimizations. For example, some server parameters pertain to query processing and may be tuned, and certain hardware configuration factors have a direct effect on query processing speed. In many cases, these optimizations improve the performance of the server as a whole, and thus have a beneficial effect for all MySQL users.

In general, you should keep the following principles in mind when performing administrative optimizations:

- Accessing data in memory is faster than accessing data from disk.
- Keeping data in memory as long as possible reduces disk activity.
- Retaining information from an index is more important than retaining contents of data rows.

The most common way to apply these principles is to increase the size of the server's caches. The server has many parameters (system variables) that you can change to configure its operation. Several of these directly affect the speed of query processing. The most important parameters you can change are the sizes of the table cache and the caches used by the storage engines to buffer information for indexing operations. If you have memory available, allocating it to the server's caches enables information to be held in memory longer and reduces disk activity. This is good, because it's much faster to access information from memory than to read it from disk. You can configure the size of several caches:

1. When the server opens table files, it tries to keep them open so as to minimize the number of file-opening operations. To do this, it maintains information about open files in the table cache. The `table_cache` system variable (`table_open_cache` in MySQL 5.1) controls the size of this cache. If the server accesses lots of tables, the table cache fills up and the server closes tables that haven't been used for a while to make room for opening new tables. To assess how effective the table cache is, check the `Opened_tables` status indicator:

   ```sql
   SHOW STATUS LIKE 'Opened_tables';
   ```

   `Opened_tables` indicates the number of times a table had to be opened because it wasn't already open. (This value is also displayed as the `opens` value in the output of the `mysqladmin status` command.) If the number remains stable or increases slowly, it's probably set to about the right value. If the number grows quickly, it means the cache is too small and that tables often have to be closed to make room for opening other tables. If you have file descriptors available, increasing the table cache size will reduce the number of table opening operations.

2. The MyISAM key buffer is used to hold index blocks for index-related operations on MyISAM tables. Its size is controlled by the `key_buffer_size` system variable.

Larger values allow MySQL to hold more index blocks in memory at once, which increases the likelihood of finding key values in memory without having to read a new block from disk. The default size of the key buffer is 8MB. If you have lots of memory, that’s a very conservative value and you should be able to increase it substantially and see a considerable improvement in performance for index-based retrievals and for index creation and modification operations.

You can create additional key caches for MyISAM tables and assign specific tables to them. This can help query processing for those tables, as explained in Section 5.6.1, “Using MyISAM Key Caches.”

- The InnoDB storage engine has its own cache for buffering data and index values, and it also maintains a log buffer. The sizes for these resources are controlled by the `innodb_buffer_pool_size` and `innodb_log_buffer_size` system variables, respectively.
- Another special cache is the query cache, described later in Section 5.6.2, “Using the Query Cache.”

Instructions for setting system variables can be found in Section 12.6.1, “Checking and Setting System Variable Values.” When you change parameter values, follow these guidelines:

- Change one parameter at a time. Otherwise, you’re varying multiple independent variables and it becomes more difficult to assess the effect of each change.
- Increase system variable values incrementally. If you increase a variable by a huge amount on the theory that more is always better, you may run your system out of resources, causing it to thrash or slow to a crawl because you’ve set the value too high.
- Rather than experimenting with parameter tuning on your production MySQL server, it might be prudent to set up a separate test server.
- To get an idea of the kinds of parameter variables that are likely to be appropriate for your system, take a look at the `my-small.cnf`, `my-medium.cnf`, `my-large.cnf`, and `my-huge.cnf` option files included with MySQL distributions. (On Unix, you can find them under the share directory in binary distributions and under the support-files directory in source distributions. On Windows, they are located in the base installation directory, and the filename suffix is `.ini`.) These files will give you some idea of which parameters are best to change for servers that receive different levels of use, and also some representative values to use for those parameters.

Other strategies you can adopt to help the server operate more efficiently include the following:

- Run the server at runtime with the appropriate startup options. For details, see Section 12.7.1, “Selecting Which Storage Engines a Server Supports.”
- Keep grant table permissions simple. Although the server caches grant table contents in *memory*, if you have any rows in the `tables_priv`, `columns_priv`, or `procs_priv` tables, the server must check their contents when it does privilege checking for SQL statements. If those tables are empty, the server can optimize its privilege checking to skip those privilege levels.
- If you build MySQL from source, configure it to use static libraries rather than shared libraries. Dynamic binaries that use shared libraries save on disk space, but static binaries are faster. However, some systems require dynamic linking if you use the user-defined function (UDF) mechanism. On such systems, static binaries will not work.

### 5.6.1 Using MyISAM Key Caches

When MySQL executes a statement that uses indexes from MyISAM tables, it uses a key cache to hold index values. The cache enables disk I/O to be reduced: If key values needed from a table are found in the cache, they need not be read from disk again. However, the key cache is a finite resource and it is shared among all MyISAM tables by default. If key values are not found in the cache and the cache is full, contention results: Some values currently in the cache must be discarded to make room for new values. The next time the discarded values are needed, they must be read from disk again.

If you have an especially heavily used MyISAM table, it would be beneficial to ensure that its keys remain in *memory*, but contention in the cache works against this. Contentions can arise either when keys need to be read from the same table, or from other tables. You might avoid same-table contention by making the key cache large enough to hold all of a given table’s indexes completely, but keys from other tables would still contend for space in the cache.

MySQL offers a solution to this problem because it supports setting up multiple key caches and enables a table’s indexes to be assigned to and preload into a given cache. This can be useful if you have a table that uses especially heavily use and you have sufficient *memory* to load its indexes into the cache. This capability enables you to avoid both same-table and other-table contention: Create a cache that is large enough to hold a table’s indexes completely and devote the cache exclusively to the use of that table. No disk I/O is necessary after the keys have been loaded into the cache. Also, key values will never need to be discarded from the cache and key lookups for the table can be done in *memory*.

The following example shows how to set up a key cache for the `member` table in the `sampdb` database, using a cache with a name of `member_cache` and a size of 1MB. You must have the SUPER privilege to carry out these instructions.

1. Set up a separate key cache large enough to hold the indexes from the table:

   `mysql> SET GLOBAL member_cache.key_buffer_size = 1024*1024;`
