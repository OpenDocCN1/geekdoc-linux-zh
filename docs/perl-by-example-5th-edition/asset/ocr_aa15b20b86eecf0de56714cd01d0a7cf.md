# EXAMPLE B.42

```
```mysql> select NOW();
+---------------------+
| NOW()               |
+---------------------+
| 2006-03-21 00:32:37 |
+---------------------+
1 row in set (0.00 sec)

mysql> select CURDATE();
+---------------------+
| CURDATE()           |
+---------------------+
| 2006-03-21          |
+---------------------+
1 row in set (0.03 sec)

mysql> select CURTIME();
+---------------------+
| CURTIME()           |
+---------------------+
| 00:12:46            |
+---------------------+
1 row in set (0.01 sec)
```
```

**Formatting the Date and Time.** When retrieving dates and times from a table, you might find you want to format the output. For example, when selecting the dates of the orders from the orders table in the *northwind* database, the result set is not user friendly. Date values in SQL are always saved in MM/DD/YY(YY) format. The *DATE_FORMAT()* and *TIME_FORMAT()* functions (see Example B.43) are provided with a list of parameters (see Table B.7) used to specify how the output should be displayed.

# EXAMPLE B.43

```
```mysql> select DATE_FORMAT('2006-03-23', '%W %M %d, %Y') as Today;
+-------------------------+
| Today                   |
+-------------------------+
| Thursday March 23, 2006 |
+-------------------------+
1 row in set (0.00 sec)```
```