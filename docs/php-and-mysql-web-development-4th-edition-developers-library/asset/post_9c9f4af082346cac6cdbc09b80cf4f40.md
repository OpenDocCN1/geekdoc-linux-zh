
table's indexing characteristics affect which file this will be. For a table with no or few indexes, it is likely that the data file will reach its size limit first. For a heavily indexed table, the index file may reach the limit first.

The presence of an `AUTO_INCREMENT` column implicitly limits the number of rows a table may have. For example, if the column is `TINYINT UNSIGNED`, the maximum value it may hold is 255, so that also becomes the maximum number of rows the table may hold. Larger integer types allow more rows. More generally, including any `PRIMARY KEY` or `UNIQUE` index in a table limits its row count to the maximum number of unique values in the index.

To determine the actual table size you can achieve, you must consider all applicable factors. The effective maximum table size likely will be determined by the smallest of those factors. Suppose that you want to create a MyISAM table. MySQL will allow the data and index files to reach 256TB each, using the default data pointer size. But if your operating system imposes a size limit on files of 2GB, that will be the effective limit for the table files. On the other hand, if your system supports files that can be larger than 256TB, the determining factor on table size then will be a MySQL factor, namely the internal data pointer size. This is a factor that you can control.

With respect to InnoDB tables that are stored in the shared tablespace, a single InnoDB table can grow as large as that tablespace and the tablespace can span multiple files to become quite large. But if, as is more likely, you have many InnoDB tables, they all share the same space and thus each is constrained in size not only by the size of the tablespace, but also by how much of the tablespace is allocated to other tables. Any individual InnoDB table can grow as long as the tablespace is not full. Conversely, when the tablespace fills up, no InnoDB table can grow any larger until you add another component to the tablespace to make it bigger. Alternatively, you can make the last tablespace component auto-extending, so that it will grow as long as it does not exceed the file-size limit of your system and disk space is available. See Section 12.7.3.1, “Configuring the InnoDB Tablespace,” for details on tablespace configuration.

Falcon tablespace files grow automatically from their initial size but are limited to 128TB. You can create additional tablespaces and move tables from one tablespace to another should a given tablespace become too “crowded.” Section 12.7.4, “Configuring the Falcon Storage Engine,” discusses Falcon tablespace creation.

### 11.2.8 Implications of Data Directory Structure for System Performance

The structure of the MySQL data directory is easy to understand because it uses the hierarchical structure of the filesystem in such a natural way. At the same time, this structure has certain performance implications, particularly regarding operations that open the files that represent database tables.

One consequence of the data directory structure is that, for storage engines that represent individual tables each with their own files, each open table can require a file descriptor. If a table is represented by multiple files, opening the table requires multiple file descriptors, not just one. The server caches descriptors intelligently, but a busy server can easily use up lots of them while servicing many simultaneous client connections or executing complex statements that reference several tables. This can be a problem, because file descriptors are a scarce resource on many systems, particularly those that set the default per-process descriptor limit fairly low. An operating system that imposes a low limit and makes no provision for increasing it would not make a good choice for running a high-activity MySQL server.

Another effect of representing each table by its own files is that table-opening time increases with the number of tables. Operations that open tables map onto the file-opening operations provided by the operating system, and as such are bound by the efficiency of the system's directory-lookup routines. Normally this isn't much of an issue, but it is something to consider if you'll need large numbers of tables in a database. For example, a MyISAM table is represented by three files. If you want to have 10,000 MyISAM tables, your database directory will contain 30,000 files. With that many files, you may notice a slowdown due to the time taken by file-opening operations. If this is cause for concern, you might want to think about using a type of filesystem that is highly efficient at dealing with large numbers of files. For example, XFS or JFS exhibit good performance even with large numbers of small files. If it is not possible to choose a different filesystem, it may be necessary to re-evaluate the structure of your tables in relation to the needs of your applications and reorganize your tables accordingly. Consider whether you really require so many tables; sometimes applications multiply tables needlessly. An application that creates a separate table per user results in many tables, all of which have identical structures. If you wanted to combine the tables into a single table, you might be able to do so by adding another column identifying the user to which each row applies. If this significantly reduces the number of tables, the application's performance improves.

As always in database design, you must consider whether this particular strategy is worthwhile for a given application. Reasons not to combine tables in the manner just described are as follows:

- Increased disk space requirements. Combining tables reduces the number of tables required (decreasing table-opening times), but adds another column (increasing disk space requirements). This is a typical time versus space tradeoff and you'd need to decide which factor is most important. If speed is paramount, you'd probably be willing to sacrifice a little extra disk space. If space is tight, it might be more acceptable to use multiple tables and live with a slight delay.
- Security considerations. These may constrain your ability or desire to combine tables. One reason to use a separate table per user is to enable access to each table for only a single MySQL account by means of table-level privileges. If you combine tables, data for all users will be in the same table.

MySQL has no provision for restricting access to particular rows to a given user; thus, you might not be able to combine tables without compromising access control. One possibility is to use views that select rows only for the current user, and grant access through the views. Alternatively, if all access to the data is controlled by your application (users never connect directly to the database), you can combine the tables and use application logic to enforce row-level access to the combined result.

Another way to create many tables without requiring so many individual files is to use InnoDB tables and store them in the InnoDB shared tablespace. In this case, the InnoDB storage engine associates only an .frm file uniquely with each table, and stores the data and index information for all InnoDB tables together. This minimizes the number of disk files needed to represent the tables, and it also substantially reduces the number of file descriptors required for open tables. InnoDB needs only one descriptor per component file of the tablespace (which is constant during the life of the server process), and briefly a descriptor for any table that it opens while it reads the table's .frm file.

A similar strategy can be used with Falcon, which enables the data and indexes of multiple tables to be stored in a single tablespace file.

### 11.2.9 MySQL Status and Log Files

In addition to database directories, the MySQL data directory contains a number of status and log files, as summarized in Table 11.1. The default location for each file is the server's data directory, and the default name for many of them is derived using the server host name, denoted as *HOSTNAME* in the table. The binary and relay logs are created as a numbered sequence of files, denoted by *nnnnn*. The table lists only the server-level status and log files. Individual storage engines may create their own logs or other files. For example, InnoDB and Falcon do this.

Table 11.1 MySQL Status and Log Files

| File Type | Default Name | File Contents |
| :--- | :--- | :--- |
| Process ID file | *HOSTNAME*.pid | The server process ID |
| Error log | *HOSTNAME*.err | Startup and shutdown events and error conditions |
| General query log | *HOSTNAME*.log | Connect/disconnect events and statement information |
| Binary log | *HOSTNAME*-bin.nnnnnn | Binary representation of statements that modify data |
| Binary log index | *HOSTNAME*-bin.index | List of current binary log files |
| Relay log | *HOSTNAME*-relay-bin.nnnnnn | Data modifications received by slave server from master |
| Relay log index | *HOSTNAME*-relay-bin.index | List of current relay log files |
| Master info file | master.info | Parameters for connecting to master server |
| Relay info file | relay-log.info | Status of relay log processing |
| Slow-query log | *HOSTNAME*-slow.log | Text of statements that take a long time to process |
