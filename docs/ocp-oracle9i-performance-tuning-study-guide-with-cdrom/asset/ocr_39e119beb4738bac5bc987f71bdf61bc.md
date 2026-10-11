Next, you need to copy the chained rows to a temporary table so that you can subsequently delete them from the SALES table, and then reinsert them into the SALES table:

```
SQL> CREATE TABLE temp<br>2 AS SELECT *<br>3 FROM sales<br>4 WHERE rowid IN (SELECT head_rowid<br>5 FROM chained_rows);
```

Table created.

```
SQL> DELETE FROM sales<br>2 WHERE rowid IN (SELECT head_rowid<br>3 FROM chained_rows);
```

5 rows deleted.

```
SQL> INSERT INTO sales<br>2 SELECT * FROM temp;
```

5 rows created.

Finally, you can reanalyze the SALES table with the COMPUTE STATISTICS option. Any non-zero value remaining in the CHAIN_CNT column of DBA_TABLES indicates that those rows are chained, not migrated, since deleting and reinserting those rows did not fix the row:

```
SQL> ANALYZE TABLE sales COMPUTE STATISTICS;
```

Table analyzed.

```
SQL> SELECT table_name, chain_cnt<br>2 FROM dba_tables<br>3 WHERE table_name = 'SALES';
```

TABLE_NAME CHAIN_CNT<br>------ ------<br>SALES 1