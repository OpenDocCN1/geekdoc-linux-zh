Although SQL commands are case-insensitive, database names are not. Thus, be sure to create the database name using whatever case you intend to use refer to in the future.

If you type SHOW DATABASES; you'll see the database in addition to that already existed. Regardless of whether test (or some other database) existed you first started MySQL or had to be created, you can begin using with the USE command:

```
mysql> USE test;
```

Within each database, tables must be created and selected for use. The commands to do so are similar to the commands used to create and select. In a newly created database, no tables exist:

```
mysql> SHOW TABLES;
Empty set (0.00 sec)
```

The response Empty denotes an empty database. To fill the database with data, you must first decide on a table structure—what of data you want to record. For instance, Figure 9.2 shows various attributes of common objects: their names, colors, sizes, hardness, and values in dollars. To create a table that includes columns for these five attributes, you use a CREATE TABLE command, passing it various details:

```
mysql> CREATE TABLE objects (name VARCHAR(30), color VARCHAR(20),
-> size FLOAT, hardness ENUM('medium','hard'),
-> value DECIMAL(10,2));
```

Query OK, 0 rows affected (0.01 sec)

This example creates a table with five columns: name, color, size, hardness, and value. Each column has an associated data type, as described in Table 9.3. A few points worth noting about this table definition are as follows:

+   * The name and color columns are VARCHAR examples, whereas the name may be up to 30 characters, whereas the color may be up to 20 characters. These were defined as CHARs, each name would have to be precisely 30 characters in size, with each color precisely 20 characters. A limit of sets can be specified by using an ENUM rather than a VARCHAR. Presumably you wouldn't want to limit object names this way.
* The size column is a FLOAT, which is less than an integer data type, but a FLOAT can hold real number. Figure 9.2 includes sizes in inches and feet, and in practice you'll need to convert everything to one unit—probably inches in this case.
* Note the syntax for the ENUM: The list of values as a whole is enclosed in parentheses (()), and each enumerated value is enclosed in single quotes ('') and separated from other values by a comma (,).