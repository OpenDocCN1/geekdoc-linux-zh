
## CHARACTER SET and COLLATE Attributes

When you specify the **CHARACTER SET** and **COLLATE** attributes, whether at the column, table, or database level, the following rules apply:

- The character set must be one that the server supports. To display the available character sets, use `SHOW CHARACTER SET`.
- For a definition that includes both **CHARACTER SET** and **COLLATE**, the character set and collation must be compatible. For example, with a character set of `latin2`, you could use a collation of `latin2_croatian_ci`, but not `latin1_bin`. To display the collations for each character set, use `SHOW COLLATION`.
- For a definition with **CHARACTER SET** but without **COLLATE**, the character set's default collation is used.
- For a definition with **COLLATE** but without **CHARACTER SET**, the character set is determined from the first part of the collation name.

To see how these rules apply, consider the following statement. It creates a table that uses several character sets:

```sql
CREATE TABLE mytbl
(
  c1 CHAR(10),
  c2 CHAR(40) CHARACTER SET latin2,
  c3 CHAR(10) COLLATE latin1_german1_ci,
  c4 BINARY(40)
) CHARACTER SET utf8;
```

The resulting table has `utf8` as its default character set. No **COLLATE** table option is given, so the default table collation is the default `utf8` collation (which is `utf8_general_ci`). The c1 column definition contains no **CHARACTER SET** or **COLLATE** attributes of its own, so the table defaults are used for it. The table-level character set and collation are not used for c2, c3, and c4: c2 and c3 have their own character set information, and c4 has a binary string type, so the character set attributes do not apply. For c2, the collation is `latin2_general_ci`, the default collation for `latin2`. For c3, the character set is `latin1`, as implied by the collation name `latin1_german1_ci`.

To see character set information for an existing table, use **SHOW CREATE TABLE**:

```text
mysql> SHOW CREATE TABLE mytbl\G
*************************** 1. row ***************************
   Table: mytbl
Create Table: CREATE TABLE `mytbl` (
  `c1` char(10) default NULL,
  `c2` char(40) character set latin2 default NULL,
  `c3` char(10) character set latin1 collate latin1_german1_ci default NULL,
  `c4` binary(40) default NULL
) ENGINE=MyISAM DEFAULT CHARSET=utf8
```

If `SHOW CREATE TABLE` does not display a column character set, it is the same as the table default character set. If it does not display a column collation, it is the default collation for the character set.

You can also add the `FULL` keyword to `SHOW COLUMNS` to cause it to display collation information (from which character sets can be derived):

```text
mysql> SHOW FULL COLUMNS FROM mytbl;
```

| Field | Type | Collation | Null | Key | Default |
|-------|------|-----------|------|-----|---------|
| c1    | char(10) | utf8_general_ci | YES | | NULL |
| c2    | char(40) | latin2_general_ci | YES | | NULL |
| c3    | char(10) | latin1_german1_ci | YES | | NULL |
| c4    | binary(40) | NULL | YES | | NULL |

The preceding discussion mentions column and table character set assignments, but character sets actually can be designated at the column, table, database, or server level. When MySQL processes a character column definition, it determines which character set to use for it by trying the following rules in order:

1. If the column definition includes a character set, use that set. (This includes the case where only a `COLLATE` attribute is present, because that implies which character set to use.)
2. Otherwise, if the table definition includes a table character set option, use that set.
3. Otherwise, use the database character set as a table default character set, which also becomes the column character set. If the database was never assigned a character set explicitly (for example, if it was created prior to MySQL 4.1), the database character set is taken from the server character set.

In other words, MySQL searches up through the levels at which character sets may be specified until it finds a character set defined, and then uses that for the column. The database always has a default character set, so the search process is guaranteed to terminate at the database level even if no character set is specified explicitly at any of the lower levels.

The character set name `binary` is special. If you assign the `binary` character set to a non-binary string column, that is equivalent to defining the column using the corresponding binary string type. The following pairs of column definitions each show two equivalent definitions:

```sql
c1 CHAR(10) CHARACTER SET binary
c1 BINARY(10)

c2 VARCHAR(10) CHARACTER SET binary
c2 VARBINARY(10)

c3 TEXT CHARACTER SET binary
c3 BLOB
```

If you specify **`CHARACTER SET`** *binary* for a binary string column, it is ignored because the type already is binary. If you specify **`CHARACTER SET`** *binary* for an **ENUM** or **SET**, it is used as is.

If you assign the **`binary`** character set as a table option, it applies to each string column that does not have any character set information specified in its own definition. MySQL provides some shorter attributes for defining character columns:

- The **`ASCII`** attribute is shorthand for **`CHARACTER SET`** *latin1*.
- The **`UCS2`** attribute is shorthand for **`CHARACTER SET`** *ucs2*.
- If you use the **`BINARY`** attribute for a non-binary string column, **ENUM**, or **SET**, it is shorthand for specifying the binary collation of the column’s character set. For example, assuming a table default character set of *latin1*, these definitions are equivalent:

```sql
c1 CHAR(10) BINARY
c2 CHAR(10) CHARACTER SET latin1 BINARY
c3 CHAR(10) CHARACTER SET latin1 COLLATE latin1_bin
```

If you specify the **`BINARY`** attribute for a binary string column, it is ignored because the type already is binary.

The general attributes **`NULL`** or **`NOT NULL`** can be specified for any of the string types. If you don’t specify either of them, **`NULL`** is the default. However, defining a string column as **`NOT NULL`** does not prevent you from storing an empty string (that is, *''*) in the column. In MySQL, an empty value is different from a missing value, so don’t make the mistake of thinking that you can force a string column to contain non-empty values by defining it **`NOT NULL`**. If you require string values to be non-empty, that is a constraint you must enforce within your own applications.

You can also specify a default value using a **`DEFAULT`** clause for all string data types except the **`BLOB`** and **`TEXT`** types. Section 3.2.3, “Specifying Column Default Values,” earlier in this chapter, described the rules that MySQL uses for assigning a default value if a column definition includes no **`DEFAULT`** clause.

## 3.2.5.6 Choosing String Data Types

When you choose a data type for a string column, consider the following questions:

**Are values represented as character or binary data?** For character data, non-binary string types are most appropriate. For binary data, use a binary string type.

**Do you want comparisons to be *lettercase-aware*?** If so, use one of the non-binary string types, because those store characters and are associated with a character set and collation.

The case sensitivity of non-binary string values for comparison and sorting purposes is controlled by the collation that you assign to them. If you want string values to be regarded equal regardless of lettercase, use a case-insensitive collation. Otherwise, use either a binary or case-sensitive collation. A binary collation compares character units using the numeric character codes. A case-sensitive collation compares character units using a specific collating order, which need not correspond to character code order. In either case, the lowercase and uppercase versions of a given character are considered distinct for comparisons. Suppose that ‘mysql’, ‘MYSQL’, and ‘?MySQL’ are strings in the latin1 character set. They are all considered the same if compared using a case-insensitive collation such as latin1_swedish_ci, but as three distinct strings if compared using the binary latin1_bin collation or case-sensitive latin1_general_cs collation.

If you want to use a string column both for case-sensitive and not case-sensitive comparisons, use a collation that corresponds to the type of comparison you will perform most often. For comparisons of the other type, apply the COLLATE operator to change the collation. For example, if mysql is a CHAR column that uses the latin1 character set, you can assign it the latin1_swedish_ci collation to perform case-insensitive comparisons by default. The following comparison is not case sensitive:

```sql
mysql = ‘ABC’
```

For those times when you need case-sensitive comparisons, use the latin1_general_cs or latin1_bin collation. The following comparisons are case sensitive (it doesn’t matter whether you apply the COLLATE operator to the left hand string or the right hand string):

```sql
mysql COLLATE latin1_general_cs = ‘ABC’
mysql COLLATE latin1_bin = ‘ABC’
mysql = ‘ABC’ COLLATE latin1_general_cs
mysql = ‘ABC’ COLLATE latin1_bin
```

Do you want to minimize storage requirements? If so, use a variable-length type, not a fixed-length type.

Will the allowable column values always be chosen from a fixed set of legal values? If so, ENUM or SET might be a good choice.

ENUM also can be useful if you have a limited set of string values that you want to sort in some non-lexical order. Sorting of ENUM values occurs according to the order in which you list the enumeration values in the column definition, so you can make the values sort in any order you want.

Are trailing pad values significant? If values must be retrieved exactly as they are stored without addition or removal of trailing spaces (or 0x00 bytes, for binary data types) during storage or retrieval, use a TEXT or VARCHAR column for non-binary strings and a BLOB or VARBINARY column for binary strings. This factor is important also if you are storing compressed, hashed, or encrypted values computed in such a way that the encoding method might result in trailing spaces. Table 3.12 shows how trailing padding is handled for storage and retrieval operations for various string data types.

As of MySQL 5.1.20, you can enable the PAD_CHAR_TO_FULL_LENGTH SQL mode to cause retrieved CHAR column values to retain trailing spaces. For BINARY columns prior to MySQL 5.0.15, short values are padded with spaces for storage and trailing spaces are stripped for retrieval.
