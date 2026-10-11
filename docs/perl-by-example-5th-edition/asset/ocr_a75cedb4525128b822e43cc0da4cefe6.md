# **EXPLANATION (CONTINUED)**

4  The `SELECT` statement retrieves the names of coaches from the table called `coaches` where the coach’s name contains a string starting with a `J`. The `%` sign is a wildcard representing any characters following the `J`.

5  The `SELECT` statement retrieves the name of the team where the number of wins is greater than 10 and the number of losses less than 10. The `&&` is called the logical **AND**. Both statements must be true or nothing will be selected.

6  The `SELECT` statement retrieves the names of coaches from the table called `coaches` where the ID is between 1 and 3. The `BETWEEN` clause creates a range criteria from which to select.

**Sorting Tables.** You can display the output of a query in a particular order by using the `ORDER BY` clause. Rows can be sorted either in ascending (the default) or descending (`DESC`) order where the values being sorted are either strings or numbers. You can limit the output of any query with the `LIMIT` clause.

# **EXAMPLE 13.13**

```
1  `mysql> SELECT * FROM teams ORDER BY name;`

    +----------------+----------+
    | name           | wins     | losses |
    +----------------+----------+
    | Bangor Rams    | 22       | 24     |
    | Bath Warships  | 32       | 3      |
    | Chico Hardhats | 19       | 25     |
    | Fremont Tigers | 24       | 26     |
    +----------------+----------+
    4 rows in set (0.00 sec)
```

```
2  `mysql> SELECT * FROM teams ORDER BY name DESC;`

    +----------------+----------+
    | name           | wins     | losses |
    +----------------+----------+
    | Fremont Tigers | 24       | 26     |
    | Chico Hardhats | 19       | 25     |
    | Bath Warships  | 32       | 3      |
    | Bangor Rams    | 22       | 24     |
    +----------------+----------+
    4 rows in set (0.00 sec)
```

```
3  `mysql> SELECT name, wins FROM teams ORDER BY wins LIMIT 2;`

    +----------------+----------+
    | name           | wins     |
    +----------------+----------+
    | Chico Hardhats | 19       |
    | Bangor Rams    | 22       |
    +----------------+----------+
    2 rows in set (0.00 sec)
```