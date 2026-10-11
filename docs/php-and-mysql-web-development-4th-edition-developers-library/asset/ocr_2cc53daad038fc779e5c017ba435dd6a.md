+   • Bytes_sent

The total number of bytes sent to all clients.

+   • Com_xxx

The server maintains a set of status variables that serve as counters to indicate the number of times particular types of statements (commands) have been executed. There are dozens of such variables, and they all have similar names, so they are not listed individually here. Each statement counter variable name begins with com_, and has a suffix that indicates the type of statement to which the counter corresponds. For example, Com_select and Com_drop_table indicate, respectively, how many SELECT and DROP TABLE statements the server has executed.

+   • Compression

Whether traffic sent via the client/server protocol uses compression. This variable was introduced in MySQL 5.0.16.

+   • Connections

The number of attempts to connect to the server (both successful and unsuccessful).

+   • Created_tmp_disk_tables

The number of on-disk temporary tables created by the server while processing statements.

+   • Created_tmp_files

The number of temporary files created by the server.

+   • Created_tmp_tables

The number of in-memory temporary tables created by the server while processing statements.

+   • Delayed_errors

The number of errors that have occurred while processing INSERT DELAYED rows.

+   • Delayed_insert_threads

The number of INSERT DELAYED handlers.

+   • Delayed_writes

The number of INSERT DELAYED rows that have been written.

+   • Flush_commands

The number of FLUSH statements that have been executed.

+   • Handler_commit

The number of requests to commit a transaction.

+   • Handler_delete

The number of requests to delete a row from a table.