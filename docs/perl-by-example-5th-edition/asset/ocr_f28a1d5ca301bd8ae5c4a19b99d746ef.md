# B.3.7 Dropping a Table

To drop a table is relatively simple. Just use the *drop command* and the name of the table:

```
mysql> drop table dog;
Query OK, 20 rows affected (0.11 sec)
```

# B.3.8 Dropping a Database

To drop a database, use the *drop database* command:

```
mysql> drop database pets;
Query OK, 1 row affected (0.45 sec)
```

# B.4 SQL Functions

The following functions are used to alter or format the output of a SQL query. Functions are provided for strings, numbers, dates, server and information, and so on. They return a result set. Functions are vendor specific, meaning functions supported by MySQL might not be supported by Microsoft SQL Server. See the MySQL documentation for a list of all functions supported.

When using *SELECT* with a function, the function, as it was called, is displayed as the name of the column in the result set as shown in Example B.36.

```
EXAMPLE B.36
1 mysql> SELECT avg(UnitPrice)
FROM order_details;
+--------------------+
| avg(UnitPrice)     |
+--------------------+
|          26.21851972 |
+--------------------+
1 row in set (0.01 sec)
2 mysql> SELECT avg(UnitPrice) as 'Average Price'
FROM order_details;
+--------------------+
| Average Price      |
+--------------------+
|          26.21851972 |
+--------------------+
1 row in set (0.00 sec)
```