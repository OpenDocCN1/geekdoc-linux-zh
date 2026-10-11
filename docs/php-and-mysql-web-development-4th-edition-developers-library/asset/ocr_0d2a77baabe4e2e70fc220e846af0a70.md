# ### 1.4.9.3 Sorting Query Results

Every MySQL user notices sooner or later that if you create a table, load some rows into it, and then issue a `SELECT * FROM tbl_name` statement, the rows tend to be retrieved in the same order in which they were inserted. That makes a certain intuitive sense, so it’s natural to assume that rows are retrieved in insertion order by default. But that is not the case. If you delete and insert rows after loading the table initially, those actions likely will change the order in which the server returns the table’s rows. (Deleting rows puts “holes” in the table, which MySQL tries to fill later when you insert new rows.)

What you should remember about row retrieval order is this: There is no *guarantee* about the order in which the server returns rows, unless you specify that order yourself. To do so, add an `ORDER BY` clause to the statement that defines the sort order you want. The following query returns president names, sorted lexically (alphabetically) by last name:

```
```sql
mysql> SELECT last_name, first_name FROM president
   -> ORDER BY last_name;
```
```
+-----------+-----------+
| last_name | first_name |
+-----------+-----------+
| Adams | John |
| Adams | John Quincy |
| Arthur | Chester A. |
| Buchanan | James |
...
```
```

Ascending order is the default sort order in an `ORDER BY` clause. You can specify explicitly whether to sort a column in ascending or descending order by using the `ASC` or `DESC` keywords after column names in the `ORDER BY` clause. For example, to sort president names in reverse (descending) name order, use `DESC` like this:

```
```sql
mysql> SELECT last_name, first_name FROM president
   -> ORDER BY last_name DESC;
```
```
+-----------+-----------+
| last_name | first_name |
+-----------+-----------+
| Wilson | Woodrow |
| Washington | George |
| Van Buren | Martin |
| Tyler | John |
...
```
```

You can sort using multiple columns, and each column can be sorted independently in ascending or descending order. The following query retrieves rows from the `president` table, sorts them by reverse state of birth, and by ascending last name within each state:

```
```sql
mysql> SELECT last_name, first_name, state FROM president
   -> ORDER BY state DESC, last_name ASC;
```
```