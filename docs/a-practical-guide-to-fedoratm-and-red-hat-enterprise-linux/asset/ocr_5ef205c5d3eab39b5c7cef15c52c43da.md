difference in the results of the query, but you must use JOIN in certain types of queries.

```
MariaDB [maxdb]> SELECT *
->              FROM people, stores
->              WHERE store = number;
```

| name | hired | store | hourly | name | number | city |
| headquarter | 2012-11-01 | 4 | 1 | new york | 4 |  | 
| max | 2012-02-12 | 4 | 0 | headquarter | 4 | new york |
| zach | 2009-03-24 | 6 | 0 | west coast | 6 | san francisco |
| sam | 2008-01-28 | 6 | 1 | west coast | 6 | san francisco |

4 rows in set (0.00 sec)

# Inner join

The preceding query demonstrates an *inner join*. If you like, you can use the keywords INNER JOIN in place of JOIN in this type of query. In each returned row, the value in people.store equals the value in stores.number. However, the stores table has a row with the value of 5 in the number column but no row exists in the people table with this value in the store column. As a result, these queries do not return a row with people.store and stores.number equal to 5.

# Table names

When working with a relational database, you can refer to a column in a specific table as table_name.column_name (e.g., stores.name in the example database). While you are working with a single table, a column name is sufficient to uniquely identify the data you want to work with. When you work with several tables, you might need to specify both a table name and a column name to uniquely identify certain data. Specifically, if two columns have the same name in two tables that are being joined, you must specify both the table and the column to disambiguate the columns. The following query demonstrates the problem.

```
MariaDB [maxdb]> SELECT *
->              FROM people, stores
->              WHERE store = number and
->                    name = 'max';
ERROR 1052 (23000): Column 'name' in where clause is ambiguous
```

In the preceding query, the column name is ambiguous: A column named name exists in both the people and stores tables. MariaDB cannot determine which table to use in the WHERE clause. The next query solves this problem. It uses people.name in the WHERE clause to specify that MariaDB is to use the name column from the people table.

```
MariaDB [maxdb]> SELECT *
->              FROM people, stores
->              WHERE store = number and
->                    people.name = 'max';
```

| name | hired | store | hourly | name | number | city |
| max | 2012-05-01 | 4 | 0 | headquarter | 4 | new york |

1 row in set (0.01 sec)