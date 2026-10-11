# EXPLANATION

1 The SELECT statement will retrieve the team's name, the coach's name, and the number of wins for the team where the team and coach name are the same and the coach's ID is 4. The fields are prepended with the name of the table and a dot to identify the field and table. The join (inner join) means that all unmatched records are discarded. Only the rows that matched the criteria in the WHERE clause are displayed in the result set.

2 The SELECT statement will retrieve the team's name, the coach's name, and the number of wins for the team where the team and coach name are the same and the coach's title is Head Coach. Like the last example, the join (inner join) means only the rows that matched the criteria in the WHERE clause are displayed in the result set.

3 The SELECT statement will retrieve the team name, the coach name, and the team wins from both the teams and coaches tables where the team name and the coach name are the same and the coach's title starts with Head. The letters t and c are called aliases for the respective tables, teams and coaches. Aliases save a lot of typing.

Deleting Rows. The DELETE command allows you to remove rows from a table. The only real difference between DELETE and SELECT is that the DELETE removes records based on some criteria, whereas the SELECT retrieves those records and DELETE does not take field names.

# EXAMPLE 15.13

```
1 mysql> SELECT name FROM teams;
+----------------+
| name           |
+----------------+
| Fremont Tigers |
| Chico Hardhats |
| Bath Warships  |
| Bangor Ram     |
+----------------+
4 rows in set (0.00 sec)
```

```
2 mysql> DELETE FROM teams WHERE name = "Bath Warships";
Query OK, 1 row affected (0.20 sec)
```

```
3 mysql> SELECT name FROM teams;
+----------------+
| name           |
+----------------+
| Fremont Tigers |
| Chico Hardhats |
| Bangor Ram     |
+----------------+
4 rows in set (0.00 sec)
```