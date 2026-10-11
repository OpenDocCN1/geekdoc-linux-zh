# EXPLANATION

+   1. A database called pets is created.
+   2. The pets database is selected and entered.
+   3. A table called dogs is created with fields and their data types. The *name*, *owner*, and *breed* will consist of a varying number of up to 20 characters. The *sex* is one character, either *f* or *m* for female or male. The *birth* and *death* columns are assigned date type.
+   4. The DESCRIBE command is like the SHOW command. It displays the layout of the new table.

Now we can insert some data into the new table.

# EXAMPLE B.27

```
mysql> INSERT INTO dog(name,owner,breed, sex, birth, death)
    -> VALUES('Pido', 'Mr. Jones', 'Mutt', 'M', '2004-11-12',
             '2006-04-02');
Query OK, 1 row affected (0.09 sec)
```

# B.3.4 Creating a Key

In real life, people can be identified by Social Security numbers, driver’s license numbers, and employee numbers; books can be identified by ISBN numbers; and a Web store order can be identified by a purchase order number. These identification numbers must be unique so that no two people have the same Social Security number, no two books have the same ISBN number, and so on. Keys are used to uniquely identify a record in a table. There are two types of keys: primary keys and foreign keys.

**Primary Keys.** Each table typically has a primary key. Primary keys are used to uniquely identify a record in the database. They must be unique, never change, occur only once per table, and are normally numeric types.

You can choose to manually generate this unique number for each record or let the database do it for you. If you let the database generate the primary key, it will generate a unique number, given a starting value (e.g., 1) and then for each new record, increment that number by 1. Even if a record is deleted, that number is never recycled. The database increments its internal counter, guaranteeing that each record will be given a unique “key.”

To set a field as a primary key, use the attribute PRIMARY KEY (*field_name*), and to tell the database to automatically create the unique number, use the AUTO_INCREMENT attribute following the field definition. The primary key cannot be null.

The following two examples describe a table called categories where the primary key is called CategoryID. It will automatically be incremented each time a new category is added to the table.