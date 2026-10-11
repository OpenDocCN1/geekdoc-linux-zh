
-   `ssl_session_cache_mode`
    The type of SSL caching used by the server.
-   `ssl_session_cache_overflows`
    The number of sessions removed from the cache because it was full.
-   `ssl_session_cache_size`
    The number of sessions that can be stored in the SSL session cache.
-   `ssl_session_cache_timeouts`
    The number of sessions that have timed out.
-   `ssl_sessions_reused`
    Whether the session was reused from an earlier session.
-   `ssl_used_session_cache_entries`
    The number of sessions in the session cache.
-   `ssl_verify_depth`
    The SSL verification depth.
-   `ssl_verify_mode`
    The SSL verification mode.
-   `ssl_version`
    The SSL protocol version of the connection.

### D.4 User-Defined Variables

User-defined variables (or, more simply, “user variables”) can be assigned values, and you can refer to those variables in other statements later.

User-defined variable names consist of '@' followed by an identifier and follow rules similar to those for legal identifiers (see Section 2.2, “MySQL Identifier Syntax and Naming Rules”). However, a user variable name can contain '.' without needing to be quoted, unlike identifiers. User variable names are case sensitive before MySQL 5.0, and not case sensitive thereafter.

User variables can be assigned values with the = or := operators in SET statements or with the := operator in other statements such as SELECT. Multiple assignments can be performed in a single statement.

```sql
mysql> SET @x = 0, @y = 2;
mysql> SET @color := 'red', @size := 'large';
mysql> SELECT @x, @y, @color, @size;
```

| @x | @y | @color | @size |
|----|----|--------|-------|
| 0  | 2  | red    | large |

```sql
mysql> SELECT @count := COUNT(*) FROM member;
+-------------------------+
| @count := COUNT(*) |
+-------------------------+
|                   102 |
+-------------------------+
```

User variables can be assigned integer, decimal, floating-point, string, or NULL values, and can be assigned from arbitrary expressions, including those that refer to other variables. If you access a user variable that has not yet been assigned a value explicitly, its value is NULL.

User variable values do not persist across sessions with the server. That is, values are lost when a connection terminates.

In SELECT statements that return multiple rows, variable assignments are performed for each row. The final value is the value assigned for the last row.

String-valued user variables have the same character set and collation as those of the value they are assigned:

```sql
mysql> SET @s = CONVERT('abc' USING latin2) COLLATE latin2_czech_cs;
mysql> SELECT CHARSET(@s), COLLATION(@s);
+------------+------------------+ 
| CHARSET(@s) | COLLATION(@s) | 
+------------+------------------+ 
| latin2     | latin2_czech_cs| 
+------------+------------------+
```

## SQL Syntax Reference

This appendix describes the syntax for SQL statements provided by MySQL. It has three parts:

-   SQL statements other than those for compound statements.
-   SQL statements that are used for compound statements, which are written using `BEGIN` and `END` and can be used for writing stored programs that are stored on the server side (functions, procedures, triggers, and events).
-   The syntax for writing comments in SQL code. Comments are used to write descriptive text that is ignored by the server, and to hide MySQL-specific keywords that will be executed by MySQL but ignored by other database servers.

Statement syntax descriptions use the following conventions:

-   Square brackets `([])` indicate optional information.
-   Vertical bars `(|)` separate alternative items in a list. If a list is enclosed in square brackets, one alternative may be chosen. If a list is enclosed in curly brackets `({})`, one alternative must be chosen.
-   Ellipsis notation `(...)` indicates that the term preceding the ellipsis may be repeated.
-   `n` indicates an integer.
-   `'str'` indicates a string value. A quoted value such as `'file_name'` or `'pattern'` indicates a more-specific kind of value such as a filename or a pattern.

Unless otherwise indicated, the statements listed in this appendix have been present in MySQL at least as early as MySQL 5.0.0. Statements that were introduced or that changed in meaning since then are noted.

Some statements have become deprecated, are scheduled to be removed, or (in my opinion) have extremely limited utility, so I have not included them here:

-   BACKUP TABLE
-   LOAD DATA FROM MASTER
-   LOAD TABLE tbl_name FROM MASTER
-   RESTORE TABLE
-   SHOW AUTHORS
-   SHOW CONTRIBUTORS

I have also not covered statements or statement clauses that relate to plugins, user-defined functions (UDFs), XA transactions, or that are specific to MySQL Cluster.

There are some general synonyms that always hold, so I list them here rather than every place in which they can be used:

To specify a character set, you can use any of the following formats:

```sql
CHARACTER SET charset
CHARSET = charset
CHARSET charset
```

These synonymous forms can be used in table and column definitions, and in the CREATE DATABASE and ALTER DATABASE statements.

As of MySQL 5.0.2, SCHEMA and SCHEMAs are synonyms for DATABASE and DATABASES, respectively, and can freely be substituted in statements anywhere you might use the latter two keywords. For example, you can create a database with either CREATE DATABASE or CREATE SCHEMA.

### E.1 SQL Statement Syntax (Non-Compound Statements)

This section describes the syntax and meaning of each of MySQL’s SQL statements, other than those for writing compound statements (see Section E.2, “Compound Statement Syntax,” for the latter). A statement fails if you do not have the necessary privileges to perform it. For example, USE db_name fails if you have no permissions for accessing the database db_name.

### ALTER DATABASE

```sql
ALTER DATABASE [db_name] db_attr ...
ALTER DATABASE db_name UPGRADE DATA DIRECTORY NAME
```

This statement changes database attributes or upgrades the database directory name encoding. It requires the ALTER privilege for the database.

For the first syntax, the allowable db_attr database attribute values are the same as those listed in the entry for CREATE DATABASE. The statement applies to the default database if the database name is omitted. If there is no default database, an error occurs.

The UPGRADE DATA DIRECTORY NAME syntax is for use when you upgrade to MySQL 5.1 or later from an older version. It re-encodes the name of the database directory if necessary to the filesystem encoding currently used by MySQL if the name contains special characters. This syntax was introduced in MySQL 5.1.23.

### ALTER EVENT

```sql
ALTER
  [DEFINER = definer_name]
  EVENT event_name
  [ON SCHEDULE schedule]
  [ON COMPLETION [NOT] PRESERVE]
  [RENAME TO new_event_name]
  [ENABLE | DISABLE [ON SLAVE]]
  [COMMENT 'str']
  [DO event_stmt]
```

Alters an existing event to have the given definition. The RENAME TO clause renames the event. The other clauses are described in the entry for CREATE EVENT. You must have the EVENT privilege for the database to which the event belongs. (Prior to MySQL 5.1.12, you must have the SUPER privilege or be the event's definer.)
ALTER EVENT was introduced in MySQL 5.1.6.

### ALTER FUNCTION, ALTER PROCEDURE

```sql
ALTER {FUNCTION | PROCEDURE} routine_name [characteristic] ...

characteristic:
  [NOT] DETERMINISTIC
  | LANGUAGE SQL
  | SQL SECURITY {DEFINER | INVOKER}
  | COMMENT 'str'
```

These statements alter the characteristics of stored routines. The characteristics are as described in the entry for the CREATE FUNCTION and CREATE PROCEDURE statements.
As of MySQL 5.0.3, these statements require the ALTER ROUTINE privilege for the given routine.

### ALTER SERVER

```sql
ALTER SERVER server_name OPTIONS { option [, option] ...}
```

Modifies the definition for the FEDERATED table server named server_name and updates the corresponding row of the mysql.servers table. Omitted options retain their previous values. You must have the SUPER privilege.
See the description of CREATE SERVER for the OPTIONS clause allowable values. This statement was introduced in MySQL 5.1.15.

### ALTER TABLE

```sql
ALTER [IGNORE] TABLE tbl_name action [, action] ...
```

ALTER TABLE enables you to rename tables or modify their structure. To use it, specify the table name along with one or more actions to be performed on the table. The IGNORE
