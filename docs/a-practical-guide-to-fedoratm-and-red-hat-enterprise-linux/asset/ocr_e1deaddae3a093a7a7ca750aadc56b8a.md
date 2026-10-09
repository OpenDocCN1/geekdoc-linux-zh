please. Typically, if you want to redirect the data, you will not specify any -v options so MariaDB does not display any messages. The next command includes an ORDER BY clause in the SELECT statement to sort the output. It uses the sel2 command file and sends the output through tail to strip the header.

```
$ cat sel2
use maxdb;
SELECT          *
FROM     people;
ORDER BY name;

$ mysql < sel2 | tail -n +2
bailey  NULL    2   1
max     NULL    4   0
percy   NULL    2   1
sam     2008-01-28 6   1
topsy   2012-11-01 4   0
zach    2009-03-24 6
```

**WHERE** The next example shows a SELECT statement with a WHERE clause. A WHERE clause causes SELECT to return only those rows that match specified criteria. In this example, the WHERE clause causes SELECT to return only rows in which the value in the store column is 4. In addition, this SELECT statement returns a single column (name). The result is a list of the names of the people who work in store number 4.

```
MariaDB [maxdb]> SELECT
->                    name
->              FROM people
->              WHERE store = 4;
+-------+
| name  |
+-------+
| topsy |
| max   |
+-------+
2 rows in set (0.00 sec)
```

The next example shows the use of a relational operator in a WHERE clause. Here the SELECT statement returns the names of people who work in stores with numbers greater than 2.

```
MariaDB [maxdb]> SELECT
->                    name
->              FROM people
->              WHERE store > 2;
+-------+
| name  |
+-------+
| topsy |
| max   |
| zach  |
| sam   |
+-------+
4 rows in set (0.00 sec)
```