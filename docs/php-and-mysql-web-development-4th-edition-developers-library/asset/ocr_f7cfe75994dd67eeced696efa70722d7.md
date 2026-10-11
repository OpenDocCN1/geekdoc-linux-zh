```
```C
if (mysql_stmt_store_result (stmt) != 0)
    {
        print_stmt_error (stmt, "Could not buffer result set");
        return;
    }
else
    {
        /* mysql_stmt_store_result() makes row count available */
        printf ("Number of rows retrieved: %lu\n",
                (unsigned long) mysql_stmt_num_rows (stmt));
    }

while (mysql_stmt_fetch (stmt) == 0)  /* fetch each row */
    {
        /* display row values */
        printf ("%d  ", my_int);
        printf ("%.2f  ", my_float);
        printf ("%*.*s  ", my_str_length, my_str_length, my_str);
        printf ("%04d-%02d-%02d %02d:%02d:%02d\n",
                my_datetime.year,
                my_datetime.month,
                my_datetime.day,
                my_datetime.hour,
                my_datetime.minute,
                my_datetime.second);
    }

mysql_stmt_free_result (stmt);         /* deallocate result set */
```
```

`select_rows()` prepares a `SELECT` statement, executes it, and retrieves the result. In this case, the statement contains no placeholders:

```
```sql
SELECT i, f, c, dt FROM t
```
```

That means we don't need to set up any `MYSQL_BIND` structures before executing the statement. But we're not off the hook. The bulk of the work in `select_rows()`, just as in `insert_rows()`, is setting up an array of `MYSQL_BIND` structures. The difference is that they're used to receive data values from the server **after** executing the statement rather than to set up data values to be sent to the server **before** executing the statement.

Nevertheless, the procedure for setting up the `MYSQL_BIND` array is somewhat similar to the corresponding code in `insert_rows()`: 

+   1.  Zero the array.
+   2.  Set the `buffer_type` member of each parameter to the appropriate type code.