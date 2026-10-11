```
constrainst fails (`sampdb`.`child`, CONSTRAINT `child_ibfk_1` FOREIGN KEY (`par_id`) REFERENCES `parent` (`par_id`) ON DELETE CASCADE ON UPDATE CASCADE)
```

To test cascaded delete, see what happens when you delete a parent row:

```
mysql> DELETE FROM parent WHERE par_id = 1;
```

MySQL deletes the row from the parent table:

```
mysql> SELECT * FROM parent;

+--------+
| par_id |
+--------+
|      2 |
|      3 |
+--------+
```

In addition, it cascades the effect of the DELETE statement to the child table:

```
mysql> SELECT * FROM child;

+--------+----------+
| par_id | child_id |
+--------+----------+
|      2 |        1 |
|      2 |        2 |
|      2 |        3 |
|      3 |        1 |
+--------+----------+
```

To test cascaded update, see what happens when you update a parent row:

```
mysql> UPDATE parent SET par_id = 100 WHERE par_id =2;
mysql> SELECT * FROM parent;

+--------+
| par_id |
+--------+
|      3 |
|    100 |
+--------+
```

```
mysql> SELECT * FROM child;

+--------+----------+
| par_id | child_id |
+--------+----------+
|      3 |        1 |
|    100 |        1 |
|    100 |        2 |
|    100 |        3 |
+--------+----------+
```