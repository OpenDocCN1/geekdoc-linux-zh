```
```text
mysql> DESCRIBE mytbl;
+-------+----------------+-----+------+---------+
| Field | Type           | Null| Key  | Default | Extra
+-------+----------------+-----+------+---------+
| i     | int(1) unsigned| NO  |      | 0       |       |
| t     | time           | YES |      | NULL    |       |
| d     | decimal(10,5)  | NO  |      | 0.00000 |       |
+-------+----------------+-----+------+---------+
```
```

The allowable cast types are BINARY (binary string), CHAR, DATE, DATETIME, TIME, SIGNED, SIGNED INTEGER, UNSIGNED, UNSIGNED INTEGER, and DECIMAL.

It is also possible to provide explicit column definitions in the CREATE TABLE part, to be used for the columns retrieved by the SELECT part. Columns in the two parts are matched by name, so provide aliases in the SELECT part as necessary to cause them to match properly:

```
```text
mysql> CREATE TABLE mytbl ( i INT UNSIGNED, t TIME, d DECIMAL(10,5))
    -> SELECT
    -> 1 AS i,
    -> CAST(CURTIME() AS TIME) AS t,
    -> CAST(PI() AS DECIMAL(10,5)) AS d;
mysql> DESCRIBE mytbl;
+-------+--------------+------+-----+---------+-------+
| Field | Type         | Null| Key | Default | Extra
+-------+--------------+------+-----+---------+-------+
| i     | int(10) unsigned| YES|     | NULL    |       |
| t     | time         | YES |     | NULL    |       |
| d     | decimal(10,5)  | YES |     | NULL    |       |
+-------+--------------+------+-----+---------+-------+
```
```

The technique of providing explicit definitions enables you to create numeric columns with specified precision and scale, character columns that have a different width than that of the longest value in the result set, and so forth. Also note that the Null and Default attributes for some of the columns are different in this example from those in the previous one. You can provide explicit definitions for those attributes in the CREATE TABLE part if necessary.

# 2.6.2.5 Using MERGE Tables

The MERGE storage engine enables you to perform queries on a set of MyISAM tables simultaneously by treating them all as a single logical unit. As described earlier in Section 2.6.1, “Storage Engine Characteristics,” MERGE can be applied to a collection of MyISAM tables that all have identical structure. The columns in each table must be defined with the same names and types in the same order, and the indexes must be defined in the same way and in the same order.