# 14.2 Performing Database Maintenance with the Server Running 741

The locking protocol to use depends on whether you need read-only access or read/write access to the table's files:

+   - For operations that just check or copy the files, read-only access is sufficient.
+   - For operations that modify the files, such as table repair or replacing damaged files with good ones, you need read/write access.

The locking protocols use the LOCK TABLE and UNLOCK TABLE statements to acquire and release locks. They also use FLUSH TABLE to tell the server to flush any pending changes to disk and as a means of informing the server that it will need to reopen the table when next it accesses it. The examples use the FLUSH TABLE syntax that takes a table-name argument and flushes only that specific table.

You must perform all the LOCK, FLUSH, and UNLOCK statements from within a single session with the server. For example, you cannot connect to the server with the mysql program, lock a table, and then quit, intending to connect again later to unlock the table. That doesn't work because when you quit mysql, the server releases the lock automatically. At that point, the server considers itself free to use the table again, with the result that it is no longer safe for you to work with the table files.

One easy way to perform the locking procedures is to keep two windows open. This enables you to leave mysql running in one window while you work with the table files in the other. If you're not using a windowing environment, you can suspend and resume mysql using your shell's job control facilities while you work with the table.

The internal-locking techniques described here for locking individual tables apply only when working with table files for storage engines such as MyISAM that represent each table with its own unique files. They do not apply to storage engines such as InnoDB or Falcon that store information about multiple tables in a given file. For example, InnoDB by default represents all InnoDB tables together within the files that make up its shared tablespace. (Even when configured to use individual per-table tablespaces, InnoDB still stores some information about each table in its data dictionary, which is stored in the shared tablespace.)

# 14.2.1.1 Locking a Table for Read-Only Access

The read-only locking protocol is appropriate for operations that need only to read a table's files, such as making copies of the files or checking them for inconsistencies. It's sufficient to acquire a read lock in this case; the server will prevent other clients from modifying the table, but will allow them to read from it. This protocol should not be used when you need to modify a table.

+   1. In window A, invoke mysql and issue the following statements to obtain a read lock and flush the table:

```
```
mysql db_name
mysql> LOCK TABLE tbl_name READ;
mysql> FLUSH TABLE tbl_name
```
```