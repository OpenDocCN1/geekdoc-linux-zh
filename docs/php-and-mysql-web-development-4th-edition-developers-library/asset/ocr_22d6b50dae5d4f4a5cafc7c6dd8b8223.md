# 2.14 Foreign Keys and Referential Integrity

The preceding example shows how to arrange for deletes or updates of a parent row to cause cascaded deletes or updates of any corresponding child rows. The ON DELETE and ON UPDATE clauses allow for other actions. For example, one possibility is to let the child rows remain in the table but have their foreign key columns set to NULL. To do this, it's necessary to make several changes to the definition of the child table:

+   - Use on DELETE SET NULL rather than ON DELETE CASCADE. This tells InnoDB to set the foreign key column (`par_id`) to NULL instead of deleting the rows.
+   - Use on UPDATE SET NULL rather than ON UPDATE CASCADE. This tells InnoDB to set the foreign key column (`par_id`) to null when matching parent rows are updated.
+   - The original definition of child defines `par_id` as NOT NULL. That won't work with ON DELETE SET NULL or ON UPDATE SET NULL, so the column definition must be changed to allow NULL.
+   - The original definition of child also defines `par_id` to be part of a PRIMARY KEY. However, a PRIMARY KEY cannot contain NULL values. Changing `par_id` to allow NULL therefore also requires that the PRIMARY KEY be changed to a UNIQUE index. UNIQUE indexes enforce uniqueness except for NULL values, which can occur multiple times in the index.

To see the effect of these changes, re-create the parent table using the original definition and load the same initial rows into it. Then create the child table using the new definition shown here:

```
CREATE TABLE child
(
  par_id INT NULL,
  child_id INT NOT NULL,
  UNIQUE (par_id, child_id),
  FOREIGN KEY (par_id) REFERENCES parent (par_id)
  ON DELETE SET NULL
  ON UPDATE SET NULL
) ENGINE = InnoDB;
```

With respect to inserting new rows, the child table behaves similarly to the original definition. That is, it allows insertion of rows with `par_id` values found in the parent table, but disallows entry of values that aren't listed there:

```
mysql> INSERT INTO child (par_id,child_id) VALUES(1,1),(1,2);
mysql> INSERT INTO child (par_id,child_id) VALUES(2,1),(2,2),(2,3);
mysql> INSERT INTO child (par_id,child_id) VALUES(3,1);
mysql> INSERT INTO child (par_id,child_id) VALUES(4,1);
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`sampdb`.`child`, CONSTRAINT `child_ibfk_1` FOREIGN KEY (`par_id`) REFERENCES `parent` (`par_id`) ON DELETE SET NULL ON UPDATE SET NULL)
```