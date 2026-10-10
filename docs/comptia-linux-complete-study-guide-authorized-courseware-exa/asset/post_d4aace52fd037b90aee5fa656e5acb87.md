
![](img/f339a9f48c4b443e61c74acb4c9c3da4_518_0.png)

### Note
Although SQL commands are case-insensitive, database names are not. Thus, be sure to create the database name using whatever case you intend to use to refer to it in the future.

If you type `SHOW DATABASES;`, you’ll see the `test` database in addition to any that already existed. Regardless of whether `test` (or some other testing database) existed when you first started MySQL or had to be created, you can begin using it with the USE command:

```
mysql> USE test;
```

Within each database, tables must be created and selected for use. The commands to do so are similar to the commands used to create and select databases. In a newly created database, no tables exist:

```
mysql> SHOW TABLES;
Empty set (0.00 sec)
```

The response `Empty set` denotes an empty database. To fill the database with data, you must first decide on a table structure—what sort of data you want to record. For instance, Figure 9.2 shows various attributes of common objects: their names, colors, sizes, hardnesses, and values in dollars. To create a table that includes columns for these five attributes, you use a `CREATE TABLE` command, passing it various details:

```
mysql> CREATE TABLE objects (name VARCHAR(30), color VARCHAR(20),
    -> size FLOAT, hardness ENUM('soft', 'medium', 'hard'),
    -> value DECIMAL(10,2));
Query OK, 0 rows affected (0.01 sec)
```

This example creates a table with five columns: `name`, `color`, `size`, `hardness`, and `value`. Each column has an associated data type, as described in Table 9.3. A few points worth noting about this table definition are as follows:

- The `name` and `color` columns are both `VARCHAR` examples, but with different sizes: The name may be up to 30 characters, whereas the `color` may be up to 20 characters. If these were defined as `CHARs`, each name would have to be precisely 30 characters in size, and each color precisely 20 characters. A limited set of colors can be specified by using an `ENUM` rather than a `VARCHAR`. Presumably you wouldn’t want to limit object names this way.

- The `size` column is a `FLOAT`, which is less precise than an integer data type, but a `FLOAT` can hold real (non-integer) numbers. Figure 9.2 includes sizes in inches (including fractions of an inch) and feet, but in practice you’ll need to convert everything to one unit—probably inches, in this case.

- Note the syntax for defining the ENUM: The list of values as a whole is enclosed in parentheses (()), and each enumerated value is enclosed in single quotes (') and separated from other values by a comma (,).

- The `DECIMAL` value includes a specification of the number of digits (10 in this example) and the number of digits after the decimal point (2 in this example), separated by a comma. Some implementations support a `MONEY` data type that can be used in this case, but MySQL lacks this data type, so `DECIMAL` is the best choice for the job. A `DECIMAL` type is better for currency than `FLOAT` because a `FLOAT` type is likely to introduce rounding errors due to the way numbers are encoded in a `FLOAT` value. Such errors are typically unacceptable in currency, although they may be tolerable in some applications.

If you need to create a table with other types of values, you should consult the documentation for your specific SQL implementation to see what data types it supports.

With the table created, you may want to verify that it's been created correctly. You can do so by typing `DESCRIBE objects;`. The result should be a summary of the fields you've just created for the objects table.

## Storing Data

You can now begin storing data in your database. To do so, use the `INSERT INTO` command:

```
mysql> INSERT INTO objects -> VALUES('lizard', 'green', 6, 'soft', 10.00);
```

This example creates an entry for the first row of Figure 9.2 (but with one error, which is deliberate). You can verify that the database now holds this information by typing `SELECT * FROM objects;`. The result is a listing of all the data in the objects table, which in this case should be just the one entry. (The next section, “Retrieving Data,” covers data retrieval in more detail.)

This example entered incorrect data for one field: The lizard is entered in the table as being 6 inches in size, rather than 5. You can correct this error by using `UPDATE`:

```
mysql> UPDATE objects SET size=5 WHERE name='lizard';
Query OK, 1 row affected (0.00 sec)
Rows matched: 1 Changed: 1 Warnings: 0
```

This example begins with the keyword `UPDATE` and the table name (objects). The example then tells MySQL what to update: `SET size=5`—in other words, set the size field to 5. The `WHERE` keyword begins a specification of which rows to change. In this case, with only one row present, you can use any data or even omit `WHERE` and the rest of the line up to the semicolon. In most cases, though, you must provide enough criteria to uniquely identify the column you want to change. In this example, the name of the object is unique—hence `name='lizard'`, which tells MySQL to change the data for all rows for which the name field is `lizard`.

Before you continue with data retrieval activities, you should complete a database. Exercise 9.3 will guide you through this process.

## EXERCISE 9.3

### Creating a SQL Database

In this exercise, you’ll continue creating a small database. This exercise assumes that you’ve performed the steps described in “Creating Databases and Tables” and “Storing Data” and that you therefore have a SQL database called `test`, which contains a table called `objects`, which contains one entry based on the first line in the matrix in Figure 9.2. To complete this database, follow these steps:

1. If you’re not currently running MySQL, do so by typing `mysql`.
2. If you’re not already using the `test` database, type `USE test;` to begin using the `test` database.
3. Type `INSERT INTO objects VALUES('tree', 'green', 120, 'medium', 200);`. (You may split this command across lines, if you like.) This entry is based on the second row of Figure 9.2, but note that the size value has been expressed in inches.
4. Verify that you entered the data correctly by typing `SELECT * FROM objects;` and verifying that the new entry is present.
5. Repeat step 3 (and step 4, if you like) for the remaining rows in Figure 9.2.

If you like, you can continue and enter more data; however, if you do so, some subsequent examples may not work as described.

## Retrieving Data

The whole point of having a database is to be able to retrieve data from it. The main command for doing so has already been described: `SELECT`. This command’s power lies in its ability to accept specifications of what to select. You can use a variety of keywords to select data that matches various criteria, such as exact matches or matches to a range of values.

The overall form of `SELECT` may be described in this way:

```
SELECT field(s) FROM table [ WHERE conditions ] [ORDER BY field]
```

Previous uses of `SELECT` have used an asterisk (*) as `field(s)`, meaning that the command returns all the columns that match the remaining criteria. You can instead specify columns by name. For instance, suppose you’re only interested in the colors and values of objects. You can view this restricted set of data using `SELECT`:

```
mysql> SELECT value, color FROM objects;
+-----------+-----------------
| value     | color           |
+-----------+-----------------
| 10.00     | green           |
| 200.00    | green           |
| 5.00      | white           |
| 1.00      | red             |
| 0.10      | yellow          |
+-----------+-----------------
5 rows in set (0.00 sec)
```

The `Field(s)` criteria appears as a comma-separated list of columns. In this example, the criteria were listed in the reverse order from their order in the database, and so they appear in the reverse order in the output.

A more interesting way to retrieve data is to use `WHERE conditions`. This tool has already been mentioned, in reference to updating data. You can use `conditions` to retrieve specific data in several ways:

**Exact matches**
Using a column name, an equal sign, and a value to match returns only those rows that match the specified value. For instance, typing `SELECT * FROM objects WHERE color='green';` returns the two entries for green objects (lizard and tree).

**Numeric tests**
You can retrieve data that match certain numeric criteria. For instance, to retrieve data on all objects that are greater than 10 inches in size, you can type `SELECT * FROM objects WHERE size>10;`.

**Alphabetic tests**
The greater-than (>) and less-than (<) operators work on letters as well as numbers. This fact can be used to retrieve data based on the first letter of a string, as in `SELECT * FROM objects WHERE name>'b';` to retrieve records for which the name begins with `b` or later letters in the alphabet. (Although this example uses a greater-than operator, it does in fact match the letter `b`.)

**Multiple tests**
You can combine multiple criteria using the `AND` or `OR` operators. For instance, to retrieve data on soft objects valued at more than $7.50, you can type `SELECT * FROM objects WHERE hardness='soft' AND value>7.50;`.

You can have MySQL return the data as an ordered list by specifying a field name after the `ORDER BY` keyword:

```
mysql> SELECT * FROM objects WHERE hardness='soft' ORDER BY value;
+------+-------+-----+----------+-------+
| name | color | size | hardness | value |
+------+-------+-----+----------+-------+
| banana | yellow |  8  | soft     |  0.10 |
| pillow | white  | 18  | soft     |  5.00 |
| lizard | green  |  5  | soft     | 10.00 |
+------+-------+-----+----------+-------+
3 rows in set (0.00 sec)
```
