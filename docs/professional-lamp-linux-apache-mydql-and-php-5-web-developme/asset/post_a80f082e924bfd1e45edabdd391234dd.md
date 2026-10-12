
## Chapter 4

### Converting an Existing MyISAM Table

Creating a new InnoDB table from scratch is all fine and dandy, but you’ve got a handful of tables that you’d love to see use the InnoDB storage engine. What you need is a way to convert those tables from the default MyISAM table type. Luckily, changing the storage engine for a table in MySQL is a simple task—just use the `ALTER TABLE` command and re-specify the engine for a table. To convert the *New_Vehicles* table, which is currently using the default table type of MyISAM, you use the following:

```sql
ALTER TABLE New_Vehicles ENGINE=InnoDB;
```

Run this command against your database, and you will see this:

```
ERROR 1214 (HY000): The used table type doesn’t support FULLTEXT indexes
```

Instead of converting your tables as you’d expect, MySQL has given you an error message. As mentioned earlier, InnoDB tables do not currently support full-text indexing in MySQL. If you try to convert a MyISAM table with a defined full-text index to InnoDB, you will get this message. For the purposes of this exercise, you’re going to need to delete the full-text index so you can convert the table:

```sql
ALTER TABLE New_Vehicles DROP INDEX description;
```

And now you should be able to go ahead and convert the table:

```sql
ALTER TABLE New_Vehicles ENGINE=InnoDB;
```

This time, your query should succeed, and you will see something similar to the following:

```
Query OK, 4 rows affected (0.76 sec)
Records: 4  Duplicates: 0  Warnings: 0
```

### Foreign Keys

You wouldn’t switch a table from MyISAM to InnoDB without a good reason, and in most cases, foreign keys are as good a reason as any. Once you’ve set up your InnoDB table, it’s only a matter of adding a foreign key to the table to enforce referential integrity. While it sounds simple on the surface, there are a good number of options to consider when creating a foreign key.

The most basic format of the `ALTER TABLE` command to create a foreign key looks something like this:

```sql
ALTER TABLE [tablename] ADD CONSTRAINT [key_name] FOREIGN KEY ([indexed_column])
REFERENCES [foreign_table] ([id_column])
```

Starting out, you’re telling MySQL what table to change, and what to do (add a foreign key). Using `CONSTRAINT [key_name]`, you can optionally give the key a name, which is often a good idea if you plan on changing the key in the future. The name of the column that requires referential integrity follows in parentheses. After that is the `REFERENCES` keyword, the name of the foreign table that will be checked against, and the specific column in that foreign table to reference.

To apply this to the vehicle inventory database, add a foreign key named *refmd1* to the *New_Vehicles* table, to check the column *model_id* against the *model_id* column in the *Models* table:

```sql
ALTER TABLE New_Vehicles ADD CONSTRAINT refmd1 FOREIGN KEY (model_id) REFERENCES
Models (model_id);
```

Run this command in MySQL and you will see something similar to this:

```
ERROR 1005 (HY000): Can't create table './vehicleinventory/#sql-1591_2.fm' (errno: 150)
```

This time the error message is not as helpful as it could be in tracking down the cause. In this situation, the error was thrown because one of the tables involved in the foreign key does not use the InnoDB engine. You've already converted the *New_Vehicles* table to InnoDB, but the *Models* table is still MyISAM. In order for foreign keys to be properly created, both tables involved need to be using the InnoDB engine, so you must change them accordingly:

```sql
ALTER TABLE Models ENGINE=InnoDB;
```

And then add the foreign key:

```sql
ALTER TABLE New_Vehicles ADD CONSTRAINT refm1 FOREIGN KEY (model_id) REFERENCES Models (model_id);
```

Now your foreign key is protecting the *model_id* column in *New_Vehicles* from errant data . . . or is it? The easiest way to know for sure is to test it. Try to insert a line into *New_Vehicles* using a wildly incorrect *model_id*:

```sql
INSERT INTO New_Vehicles (model_id) VALUES (12345);
```

When you try to execute this query, it should return the following:

```
ERROR 1216 (23000): Cannot add or update a child row: a foreign key constraint fails
```

As expected, the foreign key check saw that the value was not in the *Models* table, and refused to allow the row to be inserted. You've managed to block any new rows with bad data, but what about existing rows that are being altered? Try this query:

```sql
UPDATE New_Vehicles SET model_id=12345 WHERE vehicle_id=1;
```

As you can see, the foreign key stops errant updates as well:

```
ERROR 1216 (23000): Cannot add or update a child row: a foreign key constraint fails
```

So the foreign key successfully protects the table from harmful INSERTS and UPDATES, but what happens when a value is changed in the *Models* table? Take a look at the following query, where you attempt to change an existing *model_id*:

```sql
UPDATE Models SET model_id=123 WHERE model_id=1;
```

When you run this query, you should get the following error:

```
ERROR 1217 (23000): Cannot delete or update a parent row: a foreign key constraint fails
```

This error simply reflects another of the behaviors associated with a simple InnoDB foreign key: you cannot modify a referenced column if its value is present in the referencing table. What if that behavior is not what you want? As luck would have it, you can specify the update and delete behavior of foreign keys to one of five different options: RESTRICT, CASCADE, SET NULL, NO ACTION, and SET DEFAULT. Here's a quick breakdown of what each behavior means:

-   **RESTRICT** is the default behavior. A referenced value cannot be changed or deleted.
-   **CASCADE** allows any updates to propagate down to the referencing table. If you updated the model_id in the Models table, it would cascade down to the New_Vehicles table and update any corresponding rows. Note that this can apply to deletes as well (if specified)—deleting a row in a parent table will automatically delete all rows in the child table that referenced that value.
-   **SET NULL** changes the value in the child table to NULL when you update the parent value.
-   **NO ACTION** simply tells the database to allow the change to the parent table and do nothing to the child table.
-   **SET DEFAULT** changes the values in the child table to their DEFAULT values when the parent values are changed or deleted.

Implementing these behaviors is a simple matter of adding the required `ON DELETE` or `ON UPDATE` clause to the end of the foreign key definition, like so:

```sql
ALTER TABLE [tablename] ADD CONSTRAINT [key_name] FOREIGN KEY ([indexed_column])
REFERENCES [foreign_table] ([id_column]) ON UPDATE [update behavior] ON DELETE
[delete behavior]
```

To change an existing key to support different update and delete behaviors, you first have to delete the old key, then recreate the foreign key using the new behaviors. To change the foreign keys on the New_Vehicles table to cascade any updates, and set NULL when a model is deleted, use the following:

```sql
ALTER TABLE New_Vehicles DROP FOREIGN KEY refmdl;
ALTER TABLE New_Vehicles ADD CONSTRAINT refmdl FOREIGN KEY (model_id) REFERENCES
Models (model_id) ON UPDATE CASCADE ON DELETE SET NULL;
```

Now every time a model_id is changed in the Models table, the new value will be propagated down to all rows in New_Vehicles that used the original value. Have a look for yourself:

```sql
UPDATE Models SET model_id=123 WHERE model_id=1;
SELECT * FROM New_Vehicles \G
```

The update will succeed, and return something similar to the following:

```
*************************** 1. row ***************************
vehicle_id: 1
model_id: 123
price: NULL
color: Dark Blue
description: Poplar SUV; great for moving people or cargo across town, or wherever
your adventures may take you.
modelyear: 2005
*************************** 2. row ***************************
vehicle_id: 2
model_id: NULL
price: NULL
color: Graphite Pearl
description: Last of the 2004 stock! Must sell! Loaded, all options!
modelyear: 2004
*************************** 3. row ***************************
vehicle_id: 3
model_id: 4
price: NULL
color: Radiant Red
description: Come drive this popular truck! 4WD, extended cab, many options.
modelyear: 2005
*************************** 4. row ***************************
vehicle_id: 4
model_id: 5
price: NULL
color: Daytona Sunset Orange Metallic
description: The all new C6 Corvette, the next generation of classic American sports cars. 400HP V8; Very fast!
modelyear: 2005
```

### Converting Back to MyISAM from InnoDB

You’ve given InnoDB tables and foreign keys a whirl, but you’ve decided that you’d much rather have full-text searching instead. Changing back to MyISAM is a relatively painless process. Usually it will involve only two steps: removing any InnoDB-specific features, such as foreign keys, and changing the storage engine type back to MyISAM with `ALTER TABLE`. To convert the New_Vehicles table back to MyISAM, do the following:

```sql
ALTER TABLE New_Vehicles DROP FOREIGN KEY refmid1;
ALTER TABLE New_Vehicles ENGINE=MyISAM;
```

At this point, the New_Vehicles table is back to using the MyISAM storage engine and you once again have the ability to add and use full-text indexing on that table.

## Controlling Access

One of the most important jobs you’ll have as a MySQL database administrator is controlling who can access the system and what resources they can access. In most situations, you’ll need only a handful of user accounts for each database, and those that you do need to create should only be given the minimal access required to perform their task. Luckily, MySQL provides you with a handful of ways to control who has access to your systems and to what resources exactly.

## User Administration

In order to help control the user accounts in your database, MySQL provides a couple of ways to maintain user accounts. Whether it’s an account for a co-developer, a tech-savvy client, or a web-based front end to the system, each user needs to have access specifically granted for the resources they require.
