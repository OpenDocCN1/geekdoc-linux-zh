When the column you want to use for sorting is produced by a summary function, you cannot refer to the function directly in the `ORDER BY` clause. Instead, give the column an alias and refer to it that way. The preceding query demonstrates this, where the `COUNT(*)` column is aliased as `count`. Another way to refer to such a column in an `ORDER BY` clause is by its position in the output. The previous query could have been written as follows instead:

```
SELECT state, COUNT(*) FROM president
GROUP BY state ORDER BY 2 DESC;
```

Referring to columns by position is allowable in MySQL, but problematic:

+   *   Use of column positions leads to less understandable queries because numbers are less meaningful than names.
+   *   If you add, remove, or reorder output columns, you must remember to check the `ORDER BY` clause and fix the column number if it has changed.
+   *   The syntax of referring to column positions in `ORDER BY` clauses is no longer part of standard SQL and should be considered deprecated.

Aliases have none of those problems.

If you want to group results using `GROUP BY` with a calculated column, you can refer to it using an alias or column position, just as with `ORDER BY`. The following query determines how many presidents were born in each month of the year:

```
mysql> SELECT MONTH(birth) AS Month, MONTHNAME(birth) AS Name,
       -> COUNT(*) AS count
       -> FROM president GROUP BY Name ORDER BY Month;
```

| Month | Name | count |
| :----------- | :----------- | :----------- |
| 1 | January | 4 |
| 2 | February | 4 |
| 3 | March | 4 |
| 4 | April | 4 |
| 5 | May | 2 |
| 6 | June | 1 |
| 7 | July | 4 |
| 8 | August | 4 |
| 9 | September | 1 |
| 10 | October | 6 |
| 11 | November | 5 |
| 12 | December | 3 |

`COUNT()` can be combined with `ORDER BY` and `LIMIT`. For example, to find the four most well-represented states in the `president` table, use this statement: