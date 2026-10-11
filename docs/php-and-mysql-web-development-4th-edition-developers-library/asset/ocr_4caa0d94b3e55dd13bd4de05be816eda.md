keyword comes into play if the action could produce duplicate key values in a unique index in the altered table. Without IGNORE, the effect of the ALTER TABLE statement is canceled. With IGNORE, the rows that duplicate values for unique key values are deleted.

Except for table renaming operations, ALTER TABLE works by creating from the original table a new one that incorporates the changes to be made. If an error occurs, the new table is discarded and the original remains unchanged. If the operation completes successfully, the original table is discarded and replaced by the new one. During the operation, other clients may read from the original table. Any clients that try to update the table are blocked until the ALTER TABLE statement completes, at which point the updates are applied to the new table.

action values specify alteration actions, each of which is performed in turn. Some actions cannot be combined with other actions, as indicated in the action descriptions.

For index-definition actions that include index_type or index_option clauses, some storage engines allow you to specify the indexing algorithm or other index definition modifiers. See the entry for CREATE INDEX for details about which indexing values are allowed in different versions of MySQL. For additional information about index creation, see Section 2.6.4, “Indexing Tables.”

An action value may be any of the following:

+   *   table_option

Specifies a table option of the kind that may be given in the table_option part of a CREATE TABLE statement.

```
```
ALTER TABLE score ENGINE = MyISAM CHECKSUM = 1;
ALTER TABLE sayings CHARACTER SET utf8;
```
```

Any version-specific or storage engine-specific constraints on the availability of a given table option are as described in the entry for CREATE TABLE. If you attempt to change a table to use a storage engine that is not available, the effect of the ALTER TABLE statement is subject to the setting of the NO_ENGINE_SUBSTITUTION SQL mode. It is not allowable to alter a table to use the MERGE or BLACKHOLE engines as of MySQL 5.0.23/5.1.11 because changes could cause data loss.

The [DEFAULT] CHARACTER SET table option changes the default table character set but does not convert existing the columns to that character set. To perform the latter operation, use a CONVERT TO CHARACTER SET action.

```
```
ALTER TABLE IGNOREs the DATA DIRECTORY and INDEX DIRECTORY table options.
```
```

+   *   ADD [COLUMN] col_name col_definition [FIRST | AFTER col_name]

Adds a column to the table. col_name is the column name. col_definition is the column definition; it has the same format as that used for the CREATE TABLE statement. The column becomes the first column in the table if the FIRST keyword is given or is placed after the named column if AFTER col_name is given. If the column placement is not specified, the column becomes the last column of the table.