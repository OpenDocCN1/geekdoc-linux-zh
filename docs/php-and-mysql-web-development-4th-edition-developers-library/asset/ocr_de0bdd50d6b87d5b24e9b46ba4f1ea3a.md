# SHOW BINLOG EVENTS

```
```
SHOW BINLOG EVENTS [IN 'file_name'] [FROM position]
    [LIMIT [skip_count,] show_count]
```
```

This statement is used on replication master servers to display events in a binary log file. Events correspond roughly to SQL statements.

The output from this statement includes the following columns:

+   * **`Log_name`**
+     * The binary log filename.
+   * **`Pos`**
+     * The position of the event within the log file.
+   * **`Event_type`**
+     * The type of event, such as Query for a statement that is to be executed.
+   * **`Server_id`**
+     * The ID of the server that logged the event.
+   * **`End_log_pos`**
+     * The position of the next byte after the event in the log file.
+   * **`Info`**
+     * Event information, such as the statement text for a Query event.

This statement requires the REPLICATION SLAVE privilege.

# SHOW CHARACTER SET

```
```
SHOW CHARACTER SET [LIKE 'pattern' | WHERE where_expr]
```
```

Displays a list of the character sets supported by the server. A LIKE clause may be included to display information only for character sets with names that match the given pattern. A WHERE clause restricts output to rows that satisfy the given expression.

The output from SHOW CHARACTER SET includes the following columns:

+   * **`Charset`**
+     * The short character set name. This is the name that can be used in SQL statements.
+   * **`Description`**
+     * A descriptive character set name.
+   * **`Default collation`**
+     * The name of the default collation for the character set.
+   * **`Maxlen`**
+     * The length of the “widest” character in the character set, in bytes. For multi-byte character sets, this value is greater than one. For non-multi-byte sets, all characters take a single byte, so the value is one.