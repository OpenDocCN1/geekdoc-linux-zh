HANDLER provides no protection against concurrent updates. It does not lock the table, so it's possible for the table to be modified while HANDLER has it open, and there is no guarantee that the modifications will be reflected in the rows that you read from the table.

# INSERT

```
INSERT [DELAYED | LOW_PRIORITY | HIGH_PRIORITY] [IGNORE] [INTO]
tbl_name [({col_list})]
    [VALUES|VALUE] ({expr [, expr] ...} [, (...)] ...]
    [ON DUPLICATE KEY UPDATE col_name={expr [, col_name={expr} ...]}

INSERT [DELAYED | LOW_PRIORITY | HIGH_PRIORITY] [IGNORE] [INTO]
tbl_name SET col_name={expr [, col_name={expr}] ...}
    [ON DUPLICATE KEY UPDATE col_name={expr [, col_name={expr} ...]}

INSERT [LOW_PRIORITY | HIGH_PRIORITY] [IGNORE] [INTO]
tbl_name [{col_list}]
    [SELECT ... | (SELECT ...)]
    [ON DUPLICATE KEY UPDATE col_name={expr [, col_name={expr} ...]
```

Inserts rows into an existing table tbl_name and returns the number of rows inserted. INSERT syntax has three forms.

The first form of INSERT requires a VALUES() list that specifies all values to be inserted. If no col_list is given, the VALUES() list must specify one value for each column in the table. If a col_list is given consisting of one or more comma-separated column names, one value per column must be specified in the VALUES() list. Columns not named in the column list are set to their default values. Multiple value lists may be specified, allowing multiple rows to be inserted using a single INSERT statement.

```
INSERT INTO absence (student_id, date) VALUES(14, '2008-11-03'), (34, NOW());
```

The col_list and VALUES() list may be empty, which can be used as follows to create a row for which all columns are set to their default values:

```
INSERT INTO t () VALUES();
```

The second form of INSERT inserts columns named in the SET clause to the values given by the corresponding expressions. Columns not named are set to their default values.

```
INSERT INTO absence SET student_id = 14, date = '2008-11-03';
INSERT INTO absence SET student_id = 34, date = NOW();
```

The word DEFAULT may be used in a VALUES() list or SET clause to set a column to its default value explicitly without knowing what the default value is. More generally, to refer to a column's default value in expressions, you can use DEFAULT(col_name). The following statement sets the column i to 0 if its default value is NULL, and to 1 otherwise:

```
INSERT INTO t SET i = IF(DEFAULT(1) IS NULL, 1, 0);
```