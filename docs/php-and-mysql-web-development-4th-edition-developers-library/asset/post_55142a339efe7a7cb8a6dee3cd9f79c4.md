
The important thing with `CHANGE` is that you name the column you want to change and then specify the column’s new name and definition. Thus, you must specify the name twice if you don’t want to rename the column.

To rename a column without changing its data type, use `CHANGE old_name new_name` followed by the column’s current definition.

You can assign character sets to individual columns, so it’s possible to use the `CHARACTER SET` attribute in a column’s definition to change its character set:

```
ALTER TABLE t MODIFY c CHAR(20) CHARACTER SET ucs2;
```

An important reason for changing data types is to improve query efficiency for joins that compare columns from two tables. Indexes often can be used for comparisons in joins between similar column types, but comparisons are quicker when both columns are exactly the same type. Suppose that you’re running a query like this:

```
SELECT ... FROM t1 INNER JOIN t2 WHERE t1.name = t2.name;
```

If `t1.name` is `CHAR(10)` and `t2.name` is `CHAR(15)`, the query won’t run as quickly as if they were both `CHAR(15)`. You can make them the same by changing `t1.name` using either of these commands:

```
ALTER TABLE t1 MODIFY name CHAR(15);
ALTER TABLE t1 CHANGE name name CHAR(15);
```

**Convert a table to use a different storage engine.** To convert a table from one storage engine to another, use an `ENGINE` clause that specifies the new engine name:

```
ALTER TABLE tbl_name ENGINE = engine_name;
```

`engine_name` is a name such as `MyISAM`, `MEMORY`, or `InnoDB`. Lettercase does not matter.

One reason to change a storage engine is to make it transaction-safe. Suppose that you have a `MyISAM` table and discover that an application that uses it needs to perform transactional operations, including rollback in case failures occur. `MyISAM` tables do not support transactions, but you can make the table transaction-safe by converting it to an `InnoDB` or Falcon table:

```
ALTER TABLE tbl_name ENGINE = InnoDB;
ALTER TABLE tbl_name ENGINE = Falcon;
```

When you convert a table to use a different engine, the allowable or sensible conversions may depend on the feature compatibility of the old and new engines. For example, the following conversions are disallowed:

- If you have a table that includes a `BLOB` column, you cannot convert the table to use the `MEMORY` engine because `MEMORY` tables do not support `BLOB` columns.
- If you have a `MyISAM` table that includes `FULLTEXT` or `SPATIAL` indexes, you cannot convert it to another engine because only `MyISAM` supports those types of indexes.

There are circumstances under which you should not use `ALTER TABLE` to convert a table to use a different storage engine:

- `MEMORY` tables are held in memory and disappear when the server exits. It is not a good idea to convert a table to type `MEMORY` if you require the table contents to persist across server restarts.
- If you use a `MERGE` table to group a collection of `MyISAM` tables together, you should avoid using `ALTER TABLE` to modify any of the `MyISAM` tables unless you make the same change to all of them, and to the `MERGE` table as well. The proper functioning of a `MERGE` table depends on its having the same structure as all of its constituent `MyISAM` tables.
- An `InnoDB` table can be converted to use another storage engine. However, if the table has foreign key constraints, they will be lost because only `InnoDB` supports foreign keys.

**Rename a table.** Use a `RENAME` clause that specifies the new table name:

```
ALTER TABLE tbl_name RENAME TO new_tbl_name;
```

Another way to rename tables is with `RENAME TABLE`. The syntax looks like this:

```
RENAME TABLE old_name TO new_name;
```

One thing that `RENAME TABLE` can do that `ALTER TABLE` cannot is rename multiple tables in the same statement. For example, you can swap the names of two tables like this:

```
RENAME TABLE t1 TO tmp, t2 TO t1, tmp TO t2;
```

If you qualify a table name with a database name, you can move a table from one database to another by renaming it. Either of the following statements move the table `t` from the `sampdb` database to the `test` database:

```
ALTER TABLE sampdb.t RENAME TO test.t;
RENAME TABLE sampdb.t TO test.t;
```

You cannot rename a table to a name that already exists.

If you rename a `MyISAM` table that is part of a `MERGE` table, you must redefine the `MERGE` table to refer to the new name.

## 2.7 Obtaining Database Metadata

MySQL provides several ways to obtain information about databases and the objects in them (that is, database metadata):

- `SHOW` statements such as `SHOW DATABASES` or `SHOW TABLES`
- Tables in the `INFORMATION_SCHEMA` database
- Command-line programs such as `mysqlshow` or `mysqldump`

The following sections describe how to use each of these information sources to access metadata.

### 2.7.1 Obtaining Metadata with SHOW

MySQL provides a `SHOW` statement that displays database metadata in several forms. `SHOW` is helpful for keeping track of the contents of your databases and for reminding yourself about the structure of your tables. The following examples demonstrate a few uses for `SHOW` statements.

List the databases managed by the server:

```
SHOW DATABASES;
```

Display the `CREATE DATABASE` statement for a database:

```
SHOW CREATE DATABASE db_name;
```

List the tables in the default database or in a given database:

```
SHOW TABLES;
SHOW TABLES FROM db_name;
```

- `SHOW TABLES` doesn’t show `TEMPORARY` tables.

Display the `CREATE TABLE` statement for a table:

```
SHOW CREATE TABLE tbl_name;
```

Display information about columns or indexes in a table:

```
SHOW COLUMNS FROM tbl_name;
SHOW INDEX FROM tbl_name;
```

- The `DESCRIBE tbl_name` and `EXPLAIN tbl_name` statements are synonymous with `SHOW COLUMNS FROM tbl_name`.

Display descriptive information about tables in the default database or in a given database:

```
SHOW TABLE STATUS;
SHOW TABLE STATUS FROM db_name;
```

Several forms of the `SHOW` statement take a `LIKE 'pattern'` clause allowing a pattern to be given that limits the scope of the output. MySQL interprets `'pattern'` as an SQL pattern that may include the `'%'` and `'_'` wildcard characters. For example, this statement displays the names of columns in the `student` table that begin with `'s'`:

```
mysql> SHOW COLUMNS FROM student LIKE 's%';
```

| Field | Type | Null | Key | Default | Extra |
|:---|:---|:---|:---|:---|:---|
| sex | enum('F', 'M') | NO | | | |
| student_id | int(10) unsigned | NO | PRI | NULL | auto_increment |

To match a literal instance of a wildcard character in a `LIKE` pattern, precede it with a backslash. Generally, this is done to match a literal `"_"`, which occurs frequently in database, table, and column names.

Any `SHOW` statement that supports a `LIKE` clause can also be written to use a `WHERE` clause. The `SHOW` statement still displays a fixed set of columns, but `WHERE` provides more flexibility about specifying which rows to return. The `WHERE` clause should refer to the columns displayed by the `SHOW` statement. If the column name is a reserved word such as `KEY`, specify it as a quoted identifier. This statement determines which column in the *student* table is the primary key:

```
mysql> SHOW COLUMNS FROM student WHERE `Key` = 'PRI';
```

| Field | Type | Null | Key | Default | Extra |
|:---|:---|:---|:---|:---|:---|
| student_id | int(10) unsigned | NO | PRI | NULL | auto_increment |

It's sometimes useful to be able to tell from within an application whether a given table exists. You can use `SHOW TABLES` to find out (but remember that `SHOW TABLES` does not list `TEMPORARY` tables):

```
SHOW TABLES LIKE 'tbl_name*';
SHOW TABLES FROM db_name LIKE 'tbl_name*';
```

If the `SHOW TABLES` statement lists information for the table, it exists. It's also possible to determine table existence, even for `TEMPORARY` tables, with either of the following statements:

```
SELECT COUNT(*) FROM tbl_name;
SELECT * FROM tbl_name WHERE FALSE;
```

Each statement succeeds if the table exists, and fails if it doesn't. The first statement is most appropriate for `MyISAM` tables, for which `COUNT(*)` with no `WHERE` clause is highly optimized. It's not so good for `InnoDB` tables, which require a full scan to count the rows. The second statement is more general because it runs quickly for any storage engine. These statements are most suitable for use within application programming languages such as Perl or PHP because you can test the success or failure of the query and take action accordingly. They're not especially useful in a batch script that you run from `mysql` because you can't do anything if an error occurs except terminate (or ignore the error, but then there's obviously no point in running the query at all).

To determine the storage engine for individual tables, you can use `SHOW TABLE STATUS` or `SHOW CREATE TABLE`. The output from either statement includes a storage engine indicator.
