# Chapter 7 Writing MySQL Programs Using C

What you do with the row depends on your application. For example, you might print the column values or perform some statistical calculation on them.

+   3. When you are done with the result set, call *mysql_free_result()* to deallocate the memory it uses. If you neglect to do this, your application will leak memory. It’s especially important to dispose of result sets properly for long-running applications. Otherwise, you will notice your system slowly being taken over by processes that consume ever-increasing amounts of system resources.

The following example outlines how to process a statement that returns a result set:

```
```
MYSQL_RES *res_set;

if (mysql_query (conn, "SHOW TABLES FROM sampdb") != 0)
   print_error (conn, "mysql_query() failed");
else
   {
      res_set = mysql_store_result (conn); /* generate result set */
      if (res_set == NULL)
         print_error (conn, "mysql_store_result() failed");
      else
         {
            /* process result set, and then deallocate it */
            process_result_set (conn, res_set);
            mysql_free_result (res_set);
         }
   }
```
```

The example hides the details of result set processing within another function, *process_result_set()*, which we have not yet defined. Generally, operations that handle a result set are based on a loop that looks something like this:

```
```
while ((row = mysql_fetch_row (res_set)) != NULL)
   {
      /* do something with row contents */
   }
```
```

*mysql_fetch_row()* returns a MYSQL_ROW value, which is a pointer to an array of values. If the return value is assigned to a variable named *row*, each value within the row may be accessed as *row*[i], where *i* ranges from 0 to one less than the number of columns in the row. There are several important points about the MYSQL_ROW data type to note:

+   * MYSQL_ROW is a pointer type, so you declare a variable of that type as MYSQL_ROW *row, not as MYSQL_ROW *row*.

+   * Values for all data types, even numeric types, are returned in the MYSQL_ROW array as strings. If you want to treat a value as a number, you must convert the string yourself.