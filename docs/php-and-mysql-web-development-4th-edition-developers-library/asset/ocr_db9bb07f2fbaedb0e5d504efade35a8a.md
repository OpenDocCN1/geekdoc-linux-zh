# 2.7.2 Obtaining Metadata with INFORMATION_SCHEMA

Another way to obtain information about databases is to access the `INFORMATION_SCHEMA` database. `INFORMATION_SCHEMA` is based on the SQL standard. That is, the access mechanism is standard, even though some of the content is MySQL-specific. This makes `INFORMATION_SCHEMA` more portable than the various SHOW statements, which are entirely MySQL-specific.

`INFORMATION_SCHEMA` is accessed through `SELECT` statements and can be used in a flexible manner. SHOW statements always display a fixed set of columns and you cannot capture the output in a table. With `INFORMATION_SCHEMA`, the `SELECT` statement can name specific output columns and a `WHERE` clause can specify any expression required to select the information that you want. Also, you can use joins or subqueries, and you can use `CREATE TABLE ... SELECT or INSERT INTO ... SELECT` to save the result of the retrieval in another table for further processing.

You can think of `INFORMATION_SCHEMA` as a virtual database in which the tables are views for different kinds of database metadata. To see what tables `INFORMATION_SCHEMA` contains, use `SHOW TABLES`. The output displayed here is from MySQL 5.1 (5.0 has fewer tables):

```
mysql> SHOW TABLES IN INFORMATION_SCHEMA;
```

| Tables_in_information_schema | 
| CHARACTER_SETS | 
| COLLATIONS | 
| COLLATION_CHARACTER_SET_APPLICABILITY | 
| COLUMNS | 
| COLUMN_PRIVILEGES | 
| ENGINES | 
| EVENTS | 
| FILES | 
| GLOBAL_STATUS | 
| GLOBAL_VARIABLES | 
| KEY_COLUMN_USAGE | 
| PARTITIONS | 
| PLUGINS | 
| PROCESSLIST | 
| REFERENTIAL_CONSTRAINTS | 
| ROUTINES | 
| SCHEMATA | 
| SCHEMA_PRIVILEGES | 
| SESSION_STATUS | 
| SESSION_VARIABLES | 
| STATISTICS | 
| TABLES | 
| TABLE_CONSTRAINTS |