```
```sql
mysql> SELECT * FROM student;
+--------+------+------------+
| name   | sex  | student_id |
+--------+------+------------+
| Megan  | F    | 1          |
| Joseph | M    | 2          |
| Kyle   | M    | 3          |
| Katie  | F    | 4          |
+--------+------+------------+
... 
```
```

The columns are displayed in the order that MySQL stores them in the table. This is the same order in which the columns are listed when you issue a DESCRIBE student statement. (The “...” shown at the end of the example indicates that the query returns more rows than are shown.)

You can explicitly name the column or columns you want to see. To select just student names, do this:

```
```sql
mysql> SELECT name FROM student;
+--------+
| name   |
+--------+
| Megan  |
| Joseph |
| Kyle   |
| Katie  |
+--------+
... 
```
```

If you name more than one column, separate them by commas. The following statement is equivalent to SELECT * FROM student, but names each column explicitly:

```
```sql
mysql> SELECT name, sex, student_id FROM student;
+--------+------+------------+
| name   | sex  | student_id |
+--------+------+------------+
| Megan  | F    | 1          |
| Joseph | M    | 2          |
| Kyle   | M    | 3          |
| Katie  | F    | 4          |
+--------+------+------------+
... 
```
```

You can name columns in any order:

```
```sql
SELECT name, student_id FROM student;
SELECT student_id, name FROM student;
```
```

You can even name a column more than once if you like, although generally that’s kind of pointless.

It’s also possible to select columns from more than one table at a time. This is called a “join” between tables. We’ll get to joins in Section 1.4.9.10, “Retrieving Information from Multiple Tables.”