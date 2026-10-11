+   ENABLE KEY'S

For a MyISAM table, re-enables updating for non-unique indexes that have been disabled with DISABLE KEY'S.

```
ALTER TABLE score ENABLE KEY'S;
```

+   IMPORT TABLESPACE

This action applies to InnoDB tables that use individual tablespaces. For such a table, it associates the tbl_name.ibd file in the table's database directory with the table. (Presumably, the table's former .ibd file previously had been removed with DISCARD TABLESPACE.) This action cannot be used in conjunction with other actions.

+   MODIFY [COLUMN] col_name col_definition [FIRST | AFTER col_name]

Changes the definition of a column. col_name names the column to be modified. The column definition col_definition is given, using the same format for column definitions as is shown in the entry for the CREATE TABLE statement, including any column attributes such as NULL, NOT NULL, and DEFAULT. FIRST and AFTER have the same effect as for ADD COLUMN.

```
ALTER TABLE student MODIFY name VARCHAR(40) DEFAULT '' NOT NULL;
```

+   ORDER BY col_list

Sorts the rows in the table according to the columns named in col_list, which should be a list of names or one or more columns in the table separated by commas. The default sort order is ascending. A column name may be followed by ASC or DESC to specify ascending or descending order explicitly. Sorting a table this way may improve performance of subsequent queries that retrieve rows in the same order. This is mostly useful for a table that will not be modified afterward, because rows will not remain in order if the table is modified after performing the ORDER BY operation.

```
ALTER TABLE score ORDER BY event_id, student_id;
```

+   RENAME [TO | AS] new_tbl_name

Renames the table tbl_name to new_tbl_name. If you rename an InnoDB table on which other tables depend for foreign key relationships, InnoDB adjusts the dependencies to point to the renamed table.

```
ALTER TABLE president RENAME TO prez;
```

Beginning with MySQL 5.1, ALTER TABLE supports partitioning modifications. The entry for CREATE TABLE defines the meaning of the partition scheme and partition definition terms used in the following action descriptions.