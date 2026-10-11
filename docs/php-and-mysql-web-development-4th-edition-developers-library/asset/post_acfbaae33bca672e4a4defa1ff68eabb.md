
| i          | c        |
|------------|----------|
| 1          | red      |
| 2          | blue     |
| -1         | tan      |
| 1904-01-01 | 100      |
| 2004-01-01 | 200      |

ORDER BY within an individual SELECT is used only if LIMIT is also present, to determine which rows the LIMIT applies to. It does not affect the order in which rows appear in the final UNION result.

If you want to run a UNION-type query on MyISAM tables that have the same structure, you could set up a MERGE table and query that. One reason this is useful is that it is simpler to write a query on a MERGE table than the corresponding UNION statement. A query on the MERGE table is similar to a UNION that selects corresponding columns from the individual tables that make up the MERGE table. That is, SELECT on a MERGE table is like UNION ALL (duplicates are not removed), and SELECT DISTINCT is like UNION or UNION DISTINCT (duplicates are removed).

## 2.11 Using Views

A view is a virtual table. That is, it acts like a table but actually contains no data. Instead, it is defined in terms of base (“real”) tables or other views and provides alternative ways to look at table data. Often this can simplify applications.

This section describes some applications for views. One thing it does not cover is the DEFINER clause that views have in common with stored programs and that can be used for security purposes to control access to view data. For information about DEFINER, see Section 4.5, “Security for Stored Programs and Views.”

A simple view can be nothing more than a way to select a subset of a table’s columns. Suppose that you often want to select only the last_name, first_name, city, and state columns from the president table, but you don’t want to write out all the columns like this:

```
SELECT last_name, first_name, city, state FROM president;
```

Nor do you want to use SELECT * . That’s easier to write, but * retrieves columns that you don’t want. The solution is to define a view that retrieves only the desired columns:

```
CREATE VIEW vpres AS
SELECT last_name, first_name, city, state FROM president;
```

Now the view acts as a “window” into just those columns that you want to see. This means that you can use SELECT * with the view and get back only the columns named in the view definition:

```
mysql> SELECT * FROM vpres;
```

| last_name  | first_name | city                | state |
|------------|------------|---------------------|-------|
| Washington | George     | Wakefield           | VA    |
| Adams      | John       | Braintree           | MA    |
| Jefferson  | Thomas     | Albemarle County    | VA    |
| Madison    | James      | Port Conway         | VA    |
| Monroe     | James      | Westmoreland County | VA    |
| ...        |            |                     |       |

If you include a WHERE clause, MySQL adds it to the view definition when executing the statement to further restrict the result:

```
mysql> SELECT * FROM vpres WHERE last_name = 'Adams';
```

| last_name | first_name | city      | state |
|-----------|------------|-----------|-------|
| Adams     | John       | Braintree | MA    |
| Adams     | John Quincy| Braintree | MA    |

The same is true if you add ORDER BY, LIMIT, and so forth. When you use a view, you can refer only to those column names named in the view definition. That is, you cannot refer to a column that is not part of the view, even if the column is part of the base table:

```
mysql> SELECT * FROM vpres WHERE suffix <> '';
ERROR 1054 (42S22): Unknown column 'suffix' in 'where clause'
```

The column names for a view by default are those named in the output column list of its SELECT statement. To provide column names explicitly, add a list of names in parentheses following the view name in the view definition:

```
mysql> CREATE VIEW vpres2 (ln, fn) AS
    -> SELECT last_name, first_name FROM president;
```

Now when you refer to the view, you must use the given column names rather than the names in the SELECT:

```
mysql> SELECT last_name, first_name FROM vpres2;
ERROR 1054 (42S22) at line 1: Unknown column 'last_name' in 'field list'
mysql> SELECT ln, fn FROM vpres2;
```

| ln        | fn     |
|-----------|--------|
| Washington| George |
| Adams     | John   |
| Jefferson | Thomas |
| Madison   | James  |
| Monroe    | James  |
| ...       |        |

### 2.11 Using Views

A view can be used to perform calculations automatically. In Section 1.4.9.6, “Working with Dates,” we developed a statement that determines the age of presidents at death. The same calculation can be incorporated into a view definition:

```
mysql> CREATE VIEW pres_age AS
mysql>    SELECT last_name, first_name, birth, death,
mysql>           TIMESTAMPDIFF(YEAR, birth, death) AS age
mysql>    FROM president;
```

This view includes an age column that is defined as a calculation, and selecting that column from the view retrieves the results of the calculation:

```
mysql> SELECT * FROM pres_age;
```

| last_name | first_name | birth    | death    | age |
|-----------|------------|----------|----------|-----|
| Washington| George     | 1732-02-22 | 1799-12-14 | 67  |
| Adams     | John       | 1735-10-30 | 1826-07-04 | 90  |
| Jefferson | Thomas     | 1743-04-13 | 1826-07-04 | 83  |
| Madison   | James      | 1751-03-16 | 1836-06-28 | 85  |
| Monroe    | James      | 1758-04-28 | 1831-07-04 | 73  |
| ...       |            |          |          |     |

By including the age calculation in the view definition, it's no longer necessary to write out the formula to see the age values. The view hides the details.

A view can refer to multiple tables, which makes it easier to run queries that involve joins. The following view looks up scores, joining them with student and grade event information:

```
mysql> CREATE VIEW vstudent AS
mysql>    SELECT student.student_id, name, date, score, category
mysql>    FROM grade_event INNER JOIN score INNER JOIN student
mysql>    ON grade_event.event_id = score.event_id
mysql>       AND score.student_id = student.student_id;
```

When you select from the view, MySQL executes the join and returns information from multiple tables:

```
mysql> SELECT * FROM vstudent;
```

| student_id | name   | date       | score | category |
|------------|--------|------------|-------|----------|
| 1          | Megan  | 2008-09-03 | 20    | Q        |
| 3          | Kyle   | 2008-09-03 | 20    | Q        |
| 4          | Katie  | 2008-09-03 | 18    | Q        |
| 5          | Abby   | 2008-09-03 | 13    | Q        |
| 6          | Nathan | 2008-09-03 | 18    | Q        |
| 7          | Liesl  | 2008-09-03 | 14    | Q        |
| 8          | Tan    | 2008-09-03 | 14    | Q        |
| ...        |        |            |       |          |

The view makes it trivial to retrieve the scores for a particular student by name:

```
mysql> SELECT * FROM vstudent WHERE name = 'Emily';

+------------+-------+------------+-------+----------+
| student_id | name  | date       | score | category |
+------------+-------+------------+-------+----------+
|         31 | Emily | 2008-09-03 |    11 | Q        |
|         31 | Emily | 2008-09-06 |    19 | Q        |
|         31 | Emily | 2008-09-09 |    81 | T        |
|         31 | Emily | 2008-09-16 |    19 | Q        |
|         31 | Emily | 2008-09-23 |     9 | Q        |
|         31 | Emily | 2008-10-01 |    76 | T        |
+------------+-------+------------+-------+----------+
```

Some views are updatable, which means that you can insert, update, and delete rows in the underlying table by means of operations on the view. Here is a simple example:

```
mysql> CREATE TABLE t (i INT);
mysql> INSERT INTO t (i) VALUES(1), (2), (3);
mysql> CREATE VIEW v AS SELECT i FROM t;
mysql> SELECT i FROM v;

+---+
| i |
+---+
| 1 |
| 2 |
| 3 |
+---+

mysql> INSERT INTO v (i) VALUES(4);
mysql> DELETE FROM v WHERE i < 3;
mysql> SELECT i FROM v;

+---+
| i |
+---+
| 3 |
| 4 |
+---+

mysql> UPDATE v SET i = i + 1;
mysql> SELECT i FROM v;

+---+
| i |
+---+
| 4 |
| 5 |
+---+
```
