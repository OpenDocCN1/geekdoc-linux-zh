START TRANSACTION implicitly releases any table locks that the client has acquired with LOCK TABLE but has not yet released. Executing START TRANSACTION while a transaction is in progress causes that transaction to be committed implicitly.

# STOP SLAVE

```
STOP SLAVE [slave_option [, slave_option] ...]
```

This statement, together with START SLAVE, controls the operation of replication threads on a slave server. See the description of START SLAVE for details.

# TRUNCATE

```
TRUNCATE [TABLE] tbl_name
```

TRUNCATE TABLE performs a fast truncation of table contents by dropping and re-creating the table. This is much faster than deleting each row individually. You must have the DROP privilege as of MySQL 5.1.16, and the DELETE privilege for older versions. For InnoDB, this statement is implemented as DELETE FROM tbl_name before MySQL 5.0.3. As of 5.0.3, InnoDB implements fast truncation directly. This statement is not transaction-safe. An error will occur should you issue a TRUNCATE TABLE statement within a transaction or while you are holding any explicit table locks.

# UNION

```
select_stmt
UNION [DISTINCT | ALL] select_stmt
[UNION [DISTINCT | ALL] select_stmt] ...
[ORDER BY col_[list] [LIMIT [skip_count,] show_count]]
```

UNION combines the results of multiple SELECT statements. Each SELECT statement must produce the same number of columns in its result set. The names of the columns in the final result are determined by the column names from the first SELECT. The data types of the columns are determined taking into account all values from the corresponding columns of the selected tables.

The UNION keyword can be followed by DISTINCT to eliminate duplicate rows or by ALL to preserve duplicates and return all selected rows. The implicit default is to eliminate duplicates if neither DISTINCT nor ALL is given. Any DISTINCT union operation (either explicit or implicit) takes precedence over any ALL union operations to its left:

```
mysql> SELECT 1 UNION ALL SELECT 2 UNION ALL SELECT 1;
-----
| 1 |
-----
| 1 |
| 2 |
| 1 |
-----
```