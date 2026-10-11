
## Version
- The version number of the `.frm` file for the table.

## Row_format
- The row storage format. For MyISAM tables, this can be **Fixed** (fixed-length rows), **Dynamic** (variable-length rows), or **Compressed** (compressed and read-only). As of MySQL 5.0.3, the format for InnoDB tables can be **Redundant** (the original format) or **Compact** (a newer format that requires less storage).

## Rows
- The number of rows in the table. For some storage engines such as InnoDB, this is an approximate count.

## Avg_row_length
- The average number of bytes used by table rows.

## Data_length
- The actual size in bytes of the table data file.

## Max_data_length
- The maximum size that the table data file can grow to.

## Index_length
- The actual size in bytes of the index file.

## Data_free
- The number of unused bytes in the data file. If this number is very high, it might be a good idea to issue an `OPTIMIZE TABLE` statement for the table to defragment it.

## Auto_increment
- The next value that will be generated for an `AUTO_INCREMENT` column.

## Create_time
- The time when the table was created.

## Update_time
- The time when the table was most recently modified.

## Check_time
- For MyISAM tables, the time at which the table was last checked or repaired by `myisamchk`, `CHECK TABLE`, or `REPAIR TABLE`. The value is **NULL** if the table has never been checked or repaired.

## Collation
- The table's collation. The collation name implies the character set name.

## Checksum
- The table checksum value, **NULL** if one has not been calculated.

## Create_options
- Extra options that were specified as `table_option` values in the `CREATE TABLE` statement that created the table or subsequent `ALTER TABLE` statements.

## Comment
- The text of any comment specified when the table was created. For an InnoDB table, the Comment value shows foreign key definitions, and prior to MySQL 5.1.24, it also displays the amount of free space in the InnoDB tablespace in which the table is stored. (The table might be in the shared tablespace or have its own table-space.) As of 5.1.24, the free space is displayed as the `data_free` value.

# SHOW TABLE TYPES

```sql
SHOW TABLE TYPES
```

`SHOW TABLE TYPES` was the original syntax for the `SHOW ENGINES` statement. It is still recognized but is deprecated and its use produces a warning. See the entry for `SHOW ENGINES` for a description of the output.

# SHOW TABLES

```sql
SHOW [FULL] TABLES [(FROM | IN) db_name] [LIKE 'pattern' | WHERE where_expr]
```

Displays the names of the non-TEMPORARY tables in a database. The output includes only those tables for which you have some privilege. The LIKE clause may be included to display information only for tables with names that match the given pattern. A WHERE clause restricts output to rows that satisfy the given expression.

Beginning with MySQL 5.0.1, this statement also displays view names. The FULL keyword may be given as of MySQL 5.0.2 to display for each row whether the name refers to a table or a view.

The output from this statement includes the following columns:

- **Tables_in_db_name**
  - The table or view name.
- **Table_type**
  - `BASE_TABLE` or `VIEW` to indicate whether the name refers to a table or a view. This column is displayed only if the FULL keyword is given.

# SHOW TRIGGERS

```sql
SHOW TRIGGERS [FROM db_name] [LIKE 'pattern' | WHERE where_expr]
```

This statement displays information about the triggers in the default database, or in the named database if the FROM clause is given. The LIKE clause may be included to display information only for triggers from tables with names that match the given pattern. A WHERE clause restricts output to rows that satisfy the given expression.

`SHOW TRIGGERS` was introduced in MySQL 5.0.10. It requires the TRIGGER privilege as of 5.1.22, and the SUPER privilege before that.

# SHOW VARIABLES

```sql
SHOW [GLOBAL | SESSION] VARIABLES [LIKE 'pattern' | WHERE where_expr]
```

Displays a list of system variables and their values. These variables provide information about the server’s configuration and capabilities. Section 12.6.1, “Checking and Setting System Variable Values,” discusses the use of system variables. Appendix D describes each of the system variables.

The LIKE clause may be included to display information only for variables with names that match the given pattern. A WHERE clause restricts output to rows that satisfy the given expression.

The server can display the values of system variables at the global (server-wide) or session (client-specific) level. By default, SHOW displays the session-level value for any given variable, or the global value if no session value exists. To display global or session values explicitly, specify a level indicator:

```sql
SHOW GLOBAL VARIABLES;
SHOW SESSION VARIABLES;
```

LOCAL is a synonym for SESSION. It is also possible to retrieve the values of individual dynamic variables with SELECT:

```sql
SELECT @@GLOBAL.sql_mode, @@SESSION.sql_mode, @@LOCAL.sql_mode;
```

Using SELECT has the advantage that you can more easily manipulate the query result in certain contexts.

As of MySQL 5.1.12, you can also examine the INFORMATION_SCHEMA tables named GLOBAL_VARIABLES and SESSION_VARIABLES to obtain system variable information.

# SHOW WARNINGS

```sql
SHOW WARNINGS [LIMIT [skip_count,] show_count]
SHOW COUNT(*) WARNINGS
```

`SHOW WARNINGS` displays error, warnings, and notes generated by the most recent statement that generates such messages. If that statement executed successfully, `SHOW WARNINGS` returns an empty set.

`SHOW COUNT(*) WARNINGS` displays the value of the `warning_count` system variable that counts the number of messages. (A related variable, `error_count`, counts only errors.) It is possible for the value of `warning_count` to be larger than the number of messages displayed by `SHOW WARNINGS`. The `max_error_count` system variable limits the number of messages that can be stored for display by `SHOW WARNINGS`, but `warning_count` counts all messages regardless of whether they are stored.

The LIMIT clause can be used to restrict the number of rows returned by `SHOW WARNINGS`. Its syntax is the same as the LIMIT clause for SELECT.

# START SLAVE

```sql
START SLAVE [slave_option [, slave_option] ...]
START SLAVE [SQL_THREAD] UNTIL MASTER_LOG_FILE = 'file_name', MASTER_LOG_POS = position
START SLAVE [SQL_THREAD] UNTIL RELAY_LOG_FILE = 'file_name', RELAY_LOG_POS = position
```

This statement, together with `STOP SLAVE`, controls the operation of replication threads on a slave server. With no options, `START SLAVE` initiates and `STOP SLAVE` terminates both the slave I/O and SQL threads. `slave_option` values may be specified to indicate which threads to start or stop:

- **I/O_THREAD**
  - Start or stop the I/O thread that reads events from the master server and stores them in the relay log.
- **SQL_THREAD**
  - Start or stop the SQL thread that reads events from the relay log and executes them.

If no thread or SQL_THREAD is named, an UNTIL clause can be used. Depending on which pair of log file and position options are named in the clause, the slave runs until its SQL thread reaches the given position in the master binary log or slave relay log. If the SQL thread is already running, the server ignores the UNTIL clause and generates a warning. If the clause includes the SQL_THREAD option, the server starts only the SQL thread; otherwise, it starts both threads.

# START TRANSACTION

```sql
START TRANSACTION [WITH CONSISTENT SNAPSHOT]
```

Begins a transaction by disabling autocommit mode until the next COMMIT or ROLLBACK statement. Statements executed while autocommit is disabled thus will be committed or rolled back as a unit.

After the transaction has been committed or rolled back, autocommit mode is restored to the state it was in prior to START TRANSACTION. To manipulate autocommit mode explicitly, use `SET autocommit`. The autocommit variable is described in Appendix D.

The WITH CONSISTENT SNAPSHOT clause can be used to cause the transaction to begin with a consistent read. For InnoDB, this clause does not change the current isolation level, so it is effective only if the level is REPEATABLE READ or SERIALIZABLE. For Falcon, WITH CONSISTENT SNAPSHOT provides a consistent read using the REPEATABLE READ isolation level, regardless of the current level.
