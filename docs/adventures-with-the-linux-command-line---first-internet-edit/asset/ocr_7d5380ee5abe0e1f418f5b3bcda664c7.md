Now let's delete the rows in the Package_Files table.

```
sqlite> DELETE FROM Package_Files package_name = 'sqlite3';
```

We can confirm the deletion by running our query again and we see an empty result.

```
sqlite> .header on
sql> .mode column
sqlite> .width 12 50 -10
sqlite> SELECT FROM Package_Files WHERE package_name = 'sqlite3';
sqlite>
```

Since we have used an SQL stream that can restore the deleted rows, we can now put them back in the table. The .read command can read the stream and execute it as though came from standard input.

```
sqlite> .read insert_sqlite3.sql
```

Now when we run our query, we see that the rows have been restored.

```
sqlite> SELECT FROM Package_Files WHERE package_name = 'sqlite3'
package_name file size_bytes
------------------------------------------------------------
```

| package_name | file | size_bytes |
|---|---||
| sqlite3 | /usr/bin/sqldiff | 1103280 |
| sqlite3 | /usr/bin/sqlite3 | 1260976 |
| sqlite3 | /usr/share/doc/sqlite3/copyright | 1261 |
| sqlite3 | /usr/share/man/man1/sqlite3.gz | 3596 |
| sqlite3 | /usr/share/doc/sqlite3/changelog.Debian | 35 |

# Adding and Deleting Columns

SQL provides the ALTER TABLE statement to modify table's schema. To demonstrate this, we will add a couple of columns to the Package Descriptions table and fill them with values from the Package_Files table. We'll place the necessary SQL in the

```
-- add_column.sql

-- Add and populate columns to Package_Descriptions

ALTER TABLE Package_Descriptions ADD COLUMN INTEGER;
ALTER TABLE Package_Descriptions ADD COLUMN size INTEGER;
```

```
UPDATE Package_Descriptions
SET files = (SELECT COUNT(file)
      FROM Package_Files
      WHERE Package_Files.package_name =
      Package_Descriptions.package_name),
  size = (SELECT SUM(size_bytes)
      FROM Package_Files
      WHERE Package_Files.package_name =
      Package_Descriptions.package_name);
```

We'll execute the statements and examine resulting schema.

```
sqlite> .read add_column.sql
sqlite> .schema
CREATE TABLE Package_Descriptions (
  package_name VARCHAR(60),
```