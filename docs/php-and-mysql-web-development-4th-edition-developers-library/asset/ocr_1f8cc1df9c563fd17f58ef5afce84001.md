CHARSET can be used as a synonym for CHARACTER SET. charset is the name of a character set supported by the server, and collation is the name of one of that character set's collations. These clauses can be specified together or separately. If both are given, the collation name must be compatible with the character set. If only CHARACTER SET is given, its default collation is used. If only COLLATE is given, the character set is implicit in the first part of the character set name. These rules apply at several levels:

+   *   To specify a default character set and collation for a database when you create it, use this statement:
+       `CREATE DATABASE db_name CHARACTER SET charset COLLATE collation;`
+       If no character set or collation is given, the server defaults are used for the database.
+   *   To specify a default character set and collation for a table, use CHARACTER SET and COLLATE table options at table creation time:
+       `CREATE TABLE tbl_name (...) CHARACTER SET charset COLLATE collation;`
+       If no character set or collation is given, the database defaults are used for the table.
+   *   Columns in a table can be assigned a character set and collation explicitly with CHARACTER SET and COLLATE attributes. For example:
+       `c CHAR(10) CHARACTER SET charset COLLATE collation`
+       If no character set or collation is given, the table defaults are used for the column. These attributes apply to the CHAR, VARCHAR, TEXT, ENUM, and SET data types.

It's also possible to sort string values according to a specific collation by using the COLLATE operator. For example, if c is a latin1 column that has a collation of latin1_swedish_ci, but you want to order it using Spanish sorting rules, do this:
`SELECT c FROM t ORDER BY c COLLATE latin1_spanish_ci;`

# 2.4.2 Determining Character Set Availability and Current Settings

To find out which character sets and collations are available, use these statements:

```
```
SHOW CHARACTER SET;
SHOW COLLATION;
```
```

Each statement supports a LIKE clause that narrows the results to those character set or collation names matching a pattern. For example, this statement lists the Latin-based character sets:

```
```
mysql> SHOW CHARACTER SET LIKE 'latin*';
+---------+---------------------------+---------------------+-------+
| Charset | Description               | Default collation   | Maxlen |
+---------+---------------------------+---------------------+-------+
| latin1  | cp1252 West European      | latin1_swedish_ci   |     1 |
| latin2  | ISO 8859-2 Central European | latin2_general_ci   |     1 |
...```

```