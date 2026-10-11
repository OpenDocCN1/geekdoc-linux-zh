and so on. Then bind these structures to the statement by calling `mysql_stmt_bind_param().`

+   4.  Invoke `mysql_stmt_execute()` to execute the statement.

+   5.  If the statement modifies data rather than producing a result set (for example, if it is an `INSERT` or `UPDATE`, call `mysql_stmt_affected_rows()` to determine the number of rows affected by the statement.

+   6.  If the statement produces a result set, call `mysql_stmt_result_metadata()` if you want to obtain metadata about the result set. To fetch the rows, you use `MYSQL_BIND` structures again, but this time they serve as receptacles for data returned from the server rather than a source of data to send to the server. You must set up one `MYSQL_BIND` structure for each column in the result set. They contain information about the values you expect to receive from the server in each row. Bind the structures to the statement handler by calling `mysql_stmt_bind_result()`, and then invoke `mysql_stmt_fetch()` repeatedly to get each row. After each fetch, you can access the column values for the current row.

An optional action you can take before calling `mysql_stmt_fetch()` is to call `mysql_stmt_store_result()`. If you do this, the result set rows are fetched all at once from the server and buffered in memory on the client side. Also, the number of rows in the result set can be determined by calling `mysql_stmt_num_rows()`, which otherwise returns zero.

After fetching the result set, call `mysql_stmt_free_result()` to release memory associated with it.

+   7.  If you want to re-execute the statement, return to step 4.

+   8.  If you want to prepare a different statement using the handler, return to step 2.

+   9.  When you're done with the statement handler, dispose of it by calling `mysql_stmt_close()`. If the client connection closes while the server still has prepared statements associated with the connection, the server disposes of them automatically.

A client application can prepare multiple statements, and then execute each in the order appropriate to the application.

The following discussion describes how to write a simple program that inserts some rows into a table and then retrieves them. The part of the program that processes `INSERT` statements illustrates how to use placeholders in a statement and transmit data values to the server to be bound to the prepared statement when it is executed. The part that processes a `SELECT` statement shows how to retrieve a result set produced by executing a prepared statement. You can find the source for this program in the `prepared.c` and