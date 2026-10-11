
have the FILE privilege, the output file must not already exist, and the file is created by the server on the server host with a world-accessible mode. Its ownership will be set to the account used to run the server. As of MySQL 5.0.19/5.1.6, the filename is evaluated using the character set named by the character_set_filesystem system variable.

INTO followed by a comma-separated list of variable names stores the results of the SELECT into the variables. Each variable can be either a user-defined variable of the form @var_name, or, within a stored program, a parameter or local variable. The query must select a single row of values and must name one variable per output column.

The FOR UPDATE and LOCK IN SHARE MODE clauses place locks on the rows that are examined during query execution. The locks remain in force until the current transaction is committed or rolled back. These locking clauses can be useful in multiple-statement transactions. If you use FOR UPDATE with a table for which the storage engine uses row-level locks (InnoDB), the examined rows are write-locked for exclusive use. Using LOCK IN SHARE MODE sets read locks on the rows, enabling other clients to read but not modify them. Note that if the query optimizer finds no index to use for examining rows, it must scan (and thus lock) all rows in the table.

The following statements demonstrate some ways in which the SELECT statement can be used. See Chapter 1, “Getting Started with MySQL,” and Chapter 2, “Using SQL to Manage Data,” for many other examples.

- Select the entire contents of a table:

  ```sql
  SELECT * FROM president;
  ```

- Select entire contents, but sort by name:

  ```sql
  SELECT * FROM president ORDER BY last_name, first_name;
  ```

- Select rows for presidents born on or after '1900-01-01':

  ```sql
  SELECT * FROM president WHERE birth >= '1900-01-01';
  ```

- Do the same, but sort in birth order:

  ```sql
  SELECT * FROM president WHERE birth >= '1900-01-01' ORDER BY birth;
  ```

- Determine which states are represented by rows in the member table:

  ```sql
  SELECT DISTINCT state FROM member;
  ```

- Select rows from member table and write columns as comma-separated values into a file:

  ```sql
  SELECT * INTO OUTFILE '/tmp/member.txt' FIELDS TERMINATED BY ',' FROM member;
  ```

- Select the top five scores for a particular grade event:

  ```sql
  SELECT * FROM score WHERE event_id = 9 ORDER BY score DESC LIMIT 5;
  ```

## SET

```text
SET [OPTION] assignment [, assignment ] . . .

assignment: var_name = expr
```

The *SET* statement is used to assign values to system variables, user-defined variables, or stored program local variables. Appendix D, “System, Status, and User Variable Reference,” provides information about system and user-defined variables. Section E.2.2, “Declaration Statements,” describes declaration syntax for stored program local variables. *SET* also is used for a few miscellaneous settings that are described later in this entry.

Other statements that begin with *SET* (*SET PASSWORD* and *SET TRANSACTION*) are described in separate entries later in this appendix.

When *SET* is used to assign values to variables, *var_name* in each assignment is the variable to be assigned a value and *expr* is the expression that indicates the value to assign to the variable. The assignment operator in a *SET* statement can be either `=` or `:=`.

*SET* can be used to assign values to user-defined variables, which are named using `@var_name` syntax:

```sql
SET @day = CURDATE(), @time = CURTIME();
```

*SET* also can assign values to system variables, many of which are dynamic and can be changed while the server is running. Dynamic system variables exist at two levels. Global system variables are server-wide and affect all clients. Session system variables (also called local system variables) are specific to a given client connection only. For variables that exist at both levels, a given client’s session variables are initialized from the values of the corresponding global variables when the client connects. It is necessary to have the *SUPER* privilege to modify a global variable, but any client can modify its own session variables.

The syntax for setting system variables has several forms. To set a global variable (for example, the global `sql_mode` value), use a statement having either of the following forms:

```sql
SET GLOBAL sql_mode = 'ANSI_QUOTES';
SET @@GLOBAL.sql_mode = 'ANSI_QUOTES';
```

To set a session variable, substitute the word `SESSION` for `GLOBAL`:

```sql
SET SESSION sql_mode = 'ANSI_QUOTES';
SET @@SESSION.sql_mode = 'ANSI_QUOTES';
```

You can also use `LOCAL` as a synonym for `SESSION`:

```sql
SET LOCAL sql_mode = 'ANSI_QUOTES';
SET @@LOCAL.sql_mode = 'ANSI_QUOTES';
```

If none of `GLOBAL`, `SESSION`, or `LOCAL` are present, the *SET* statement modifies the session-level variable:

```sql
SET sql_mode = 'ANSI_QUOTES';
SET @@sql_mode = 'ANSI_QUOTES';
```

To check the value of system variables, use the SHOW VARIABLES statement. You can also retrieve individual system variable values by using SELECT:

```sql
SELECT @@GLOBAL.sql_mode, @@SESSION.sql_mode, @@LOCAL.sql_mode;
```

Section 12.6.1, “Checking and Setting System Variable Values,” further discusses the use of system variables.

The following list describes miscellaneous settings that can be controlled with SET.

- SET CHARACTER SET ({charset} | DEFAULT)

  Sets the character_set_client and character_set_results session variables to the named character set, and sets the character_set_connection session variable to the value of character_set_database. These variables affect conversion of character data sent to and from the server. A charset value of ucs2, utf8, or utf32 does not work.

  SET CHARACTER SET DEFAULT restores the default character set mapping.

- SET NAMES ({charset} | '{charset}' | DEFAULT)

  Sets the character_set_client, character_set_connection, and character_set_results session variables to the named character set, and sets collation_connection to the default collation for character_set_connection. These variables affect conversion of character data sent to and from the server. A charset value of ucs2, utf8, or utf32 does not work.

  SET NAMES DEFAULT restores the default character set mapping.

## SET PASSWORD

```text
SET PASSWORD [FOR account] = PASSWORD('pass_val')
SET PASSWORD [FOR account] = OLD_PASSWORD('pass_val')
SET PASSWORD [FOR account] = 'encrypted_pass_val'
```

SET PASSWORD changes the password for a MySQL account. You can always change your own password, unless you have connected as an anonymous user. To change the password for another account, you must have the UPDATE privilege for the mysql database.

With no FOR clause, the statement sets the password for the current account. With a FOR clause, it sets the password for the named account, which should be given in ‘user_name'@'host_name' format, as described in Section 12.4.1.1, “Specifying Account Names.”

The password value, ‘pass_val' should be encrypted using PASSWORD() for standard encryption or OLD_PASSWORD() for the older (pre-MySQL 4.1) encryption. If you use neither function, ‘encrypted_pass_val' should be given as an already-encrypted password string.

```sql
SET PASSWORD = PASSWORD('secret');
SET PASSWORD FOR 'paul' = PASSWORD('secret');
SET PASSWORD FOR 'paul'@'localhost' = PASSWORD('secret');
SET PASSWORD FOR 'bill'@'%.bigcorp.com' = PASSWORD('old-sneep');
```

## SET TRANSACTION

`SET [GLOBAL | SESSION] TRANSACTION ISOLATION LEVEL level`

This statement sets the isolation level for transaction processing:

- With the `GLOBAL` option, it sets the global (server-wide) isolation level, which becomes the default level for all clients that connect thereafter.
- With the `SESSION` option, it sets the session (client-specific) isolation level, which becomes the level for subsequent transactions within the current session.
- With neither option, it sets the isolation level only for the next transaction within the current session.

The `SUPER` privilege is required to set the global isolation level. Any client can change its own session or next-transaction isolation level. The transaction level indicated by `level` should be one of the following values:

- `READ UNCOMMITTED`

  A transaction can see row modifications made by other transactions even if they have not been committed.

- `READ COMMITTED`

  A transaction can see row modifications made by other transactions only if they have been committed.

- `REPEATABLE READ`

  If a transaction performs a given `SELECT` twice, the result is repeatable. That is, it gets the same result each time, even if other transactions have changed or inserted rows in the meantime.

- `SERIALIZABLE`

  This isolation level is similar to `REPEATABLE READ` but isolates transactions more completely: Rows selected by one transaction cannot be modified by other transactions until the first transaction completes. This level is supported by InnoDB but not yet by Falcon.

The `SET TRANSACTION` statement applies to the InnoDB and Falcon storage engines. The default isolation level is `REPEATABLE READ`. Non-transactional storage engines do not have isolation levels. Section 2.13.3, “Transaction Isolation,” further discusses transaction isolation and isolation levels.

## SHOW

- `SHOW BINLOG EVENTS`
- `SHOW CHARACTER SET`
- `SHOW COLLATION`
