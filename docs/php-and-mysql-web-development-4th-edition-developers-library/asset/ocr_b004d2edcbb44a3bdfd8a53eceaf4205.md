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

If `t1.name` is `CHAR(10)` and `t2.name` is `CHAR(15)` , the query won’t run as quickly as if they were both `CHAR(15)` . You can make them the same by changing `t1.name` using either of these commands:

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

+   * If you have a table that includes a `BLOB` column, you cannot convert the table to use the `MEMORY` engine because `MEMORY` tables do not support `BLOB` columns.

+   * If you have a `MyISAM` table that includes `FULLTEXT` or `SPATIAL` indexes, you cannot convert it to another engine because only `MyISAM` supports those types of indexes.