
# Managing Data with SQL 457

Debian and related distributions will prompt for this when you install the package, but you may need to do this manually with other distributions.

## Starting to Use MySQL

To begin a SQL session, you should first ensure that the server is running, as just described. You can then start the SQL client. In the case of MySQL, this program is called mysql:

```sql
$ mysql
```

If you've installed MySQL for learning purposes, it may have no databases defined. To learn what's defined, you can use the SHOW DATABASES command:

```sql
mysql> SHOW DATABASES;
+----------------------+
| Database             |
+----------------------+
| information_schema |
+----------------------+
1 row in set (0.00 sec)
```

> **NOTE:** This example illustrates an important feature of SQL: Commands are terminated by semicolons (;). There are a few exceptions to this rule, but if you forget the semicolon, you are likely to see a new prompt that reads `->` (at least in MySQL). You can use this to split your commands across multiple lines, if you like. If you forget the semicolon that terminates a command, you can enter it by itself on the `->` prompt line. SQL commands are conventionally shown in uppercase, but SQL commands are case-insensitive; you can type your commands in uppercase, lowercase, or any mix of case you use.

In this example, a database is already defined: `information_schema`. Define a database called test. If you see such a database, you can probably use it for your own tests; however, other users may be able to see and modify this database, so don't store important data in it. If you are not in charge of the SQL installation, you should double-check database, with whoever is in charge of it to be sure you use the test database—or any other database, for that matter.

## Creating Databases and Tables

If no database for testing purposes exists, you can create one with the CREATE DATABASE command, which takes a database name as an option:

```sql
mysql> CREATE DATABASE test;
Query OK, 1 row affected (0.00 sec)
```

Although SQL commands are case-insensitive, database names are not. Thus, be sure to create the database name using whatever case you intend to use refer to in the future.

If you type SHOW DATABASES; you'll see the database in addition to that already existed. Regardless of whether test (or some other database) existed you first started MySQL or had to be created, you can begin using with the USE command:

```sql
mysql> USE test;
```

Within each database, tables must be created and selected for use. The commands to do so are similar to the commands used to create and select. In a newly created database, no tables exist:

```sql
mysql> SHOW TABLES;
Empty set (0.00 sec)
```

The response Empty denotes an empty database. To fill the database with data, you must first decide on a table structure—what of data you want to record. For instance, Figure 9.2 shows various attributes of common objects: their names, colors, sizes, hardness, and values in dollars. To create a table that includes columns for these five attributes, you use a CREATE TABLE command, passing it various details:

```sql
mysql> CREATE TABLE objects (name VARCHAR(30), color VARCHAR(20),
-> size FLOAT, hardness ENUM('medium','hard'),
-> value DECIMAL(10,2));
Query OK, 0 rows affected (0.01 sec)
```

This example creates a table with five columns: name, color, size, hardness, and value. Each column has an associated data type, as described in Table 9.3. A few points worth noting about this table definition are as follows:

- The name and color columns are VARCHAR examples, whereas the name may be up to 30 characters, whereas the color may be up to 20 characters. These were defined as CHARs, each name would have to be precisely 30 characters in size, with each color precisely 20 characters. A limit of sets can be specified by using an ENUM rather than a VARCHAR. Presumably you wouldn't want to limit object names this way.
- The size column is a FLOAT, which is less than an integer data type, but a FLOAT can hold real number. Figure 9.2 includes sizes in inches and feet, and in practice you'll need to convert everything to one unit—probably inches in this case.
- Note the syntax for the ENUM: the list of values as a whole is the

## Managing Data with SQL

In this example, a database is already defined: information_schema. Define a database called test. If you see such a database, you can probably use it for your own tests; however, other users may be able to see and modify this database, so don't store important data in it. If you are not in charge of the SQL installation, you should double-check database, with whoever is in charge of it to be sure you use the test database—or any other database, for that matter.

## Creating Databases and Tables

If no database for testing purposes exists, you can create one with the CREATE DATABASE command, which takes a database name as an option:

```sql
mysql> CREATE DATABASE test;
Query OK, 1 row affected (0.00 sec)
```

Although SQL commands are case-insensitive, database names are not. Thus, be sure to create the database name using whatever case you intend to use refer to in the future.

If you type SHOW DATABASES; you'll see the database in addition to that already existed. Regardless of whether test (or some other database) existed you first started MySQL or had to be created, you can begin using with the USE command:

```sql
mysql> USE test;
```

Within each database, tables must be created and selected for use. The commands to do so are similar to the commands used to create and select. In a newly created database, no tables exist:

```sql
mysql> SHOW TABLES;
Empty set (0.00 sec)
```

The response Empty denotes an empty database. To fill the database with data, you must first decide on a table structure—what of data you want to record. For instance, Figure 9.2 shows various attributes of common objects: their names, colors, sizes, hardness, and values in dollars. To create a table that includes columns for these five attributes, you use a CREATE TABLE command, passing it various details:

```sql
mysql> CREATE TABLE objects (name VARCHAR(30), color VARCHAR(20),
-> size FLOAT, hardness ENUM('medium','hard'),
-> value DECIMAL(10,2));
Query OK, 0 rows affected (0.01 sec)
```

This example creates a table with five columns: name, color, size, hardness, and value. Each column has an associated data type, as described in Table 9.3. A few points worth noting about this table definition are as follows:

- The name and color columns are VARCHAR examples, whereas the name may be up to 30 characters, whereas the color may be up to 20 characters. These were defined as CHARs, each name would have to be precisely 30 characters in size, with each color precisely 20 characters. A limit of sets can be specified by using an ENUM rather than a VARCHAR. Presumably you wouldn't want to limit object names this way.
- The size column is a FLOAT, which is less than an integer data type, but a FLOAT can hold real number. Figure 9.2 includes sizes in inches and feet, and in practice you'll need to convert everything to one unit—probably inches in this case.
- Note the syntax for the ENUM: the list of values as a whole is the

## Managing Data with SQL

In this example, a database is already defined: information_schema. Define a database called test. If you see such a database, you can probably use it for your own tests; however, other users may be able to see and modify this database, so don't store important data in it. If you are not in charge of the SQL installation, you should double-check database, with whoever is in charge of it to be sure you use the test database—or any other database, for that matter.

## Creating Databases and Tables

If no database for testing purposes exists, you can create one with the CREATE DATABASE command, which takes a database name as an option:

```sql
mysql> CREATE DATABASE test;
Query OK, 1 row affected (0.00 sec)
```

Although SQL commands are case-insensitive, database names are not. Thus, be sure to create the database name using whatever case you intend to use refer to in the future.

If you type SHOW DATABASES; you'll see the database in addition to that already existed. Regardless of whether test (or some other database) existed you first started MySQL or had to be created, you can begin using with the USE command:

```sql
mysql> USE test;
```

Within each database, tables must be created and selected for use. The commands to do so are similar to the commands used to create and select. In a newly created database, no tables exist:

```sql
mysql> SHOW TABLES;
Empty set (0.00 sec)
```

The response Empty denotes an empty database. To fill the database with data, you must first decide on a table structure—what of data you want to record. For instance, Figure 9.2 shows various attributes of common objects: their names, colors, sizes, hardness, and values in dollars. To create a table that includes columns for these five attributes, you use a CREATE TABLE command, passing it various details:

```sql
mysql> CREATE TABLE objects (name VARCHAR(30), color VARCHAR(20),
-> size FLOAT, hardness ENUM('medium','hard'),
-> value DECIMAL(10,2));
Query OK, 0 rows affected (0.01 sec)
```

This example creates a table with five columns: name, color, size, hardness, and value. Each column has an associated data type, as described in Table 9.3. A few points worth noting about this table definition are as follows:

- The name and color columns are VARCHAR examples, whereas the name may be up to 30 characters, whereas the color may be up to 20 characters. These were defined as CHARs, each name would have to be precisely 30 characters in size, with each color precisely 20 characters. A limit of sets can be specified by using an ENUM rather than a VARCHAR. Presumably you wouldn't want to limit object names this way.
- The size column is a FLOAT, which is less than an integer data type, but a FLOAT can hold real number. Figure 9.2 includes sizes in inches and feet, and in practice you'll need to convert everything to one unit—probably inches in this case.
- Note the syntax for the ENUM: the list of values as a whole is the

## Managing Data with SQL

In this example, a database is already defined: information_schema. Define a database called test. If you see such a database, you can probably use it for your own tests; however, other users may be able to see and modify this database, so don't store important data in it. If you are not in charge of the SQL installation, you should double-check database, with whoever is in charge of it to be sure you use the test database—or any other database, for that matter.

## Creating Databases and Tables

If no database for testing purposes exists, you can create one with the CREATE DATABASE command, which takes a database name as an option:

```sql
mysql> CREATE DATABASE test;
Query OK, 1 row affected (0.00 sec)
```

Although SQL commands are case-insensitive, database names are not. Thus, be sure to create the database name using whatever case you intend to use refer to in the future.

If you type SHOW DATABASES; you'll see the database in addition to that already existed. Regardless of whether test (or some other database) existed you first started MySQL or had to be created, you can begin using with the USE command:

```sql
mysql> USE test;
```

Within each database, tables must be created and selected for use. The commands to do so are similar to the commands used to create and select. In a newly created database, no tables exist:

```sql
mysql> SHOW TABLES;
Empty set (0.00 sec)
```

The response Empty denotes an empty database. To fill the database with data, you must first decide on a table structure—what of data you want to record. For instance, Figure 9.2 shows various attributes of common objects: their names, colors, sizes, hardness, and values in dollars. To create a table that includes columns for these five attributes, you use a CREATE TABLE command, passing it various details:

```sql
mysql> CREATE TABLE objects (name VARCHAR(30), color VARCHAR(20),
-> size FLOAT, hardness ENUM('medium','hard'),
-> value DECIMAL(10,2));
Query OK, 0 rows affected (0.01 sec)
```

This example creates a table with five columns: name, color, size, hardness, and value. Each column has an associated data type, as described in Table 9.3. A few points worth noting about this table definition are as follows:

- The name and color columns are VARCHAR examples, whereas the name may be up to 30 characters, whereas the color may be up to 20 characters. These were defined as CHARs, each name would have to be precisely 30 characters in size, with each color precisely 20 characters. A limit of sets can be specified by using an ENUM rather than a VARCHAR. Presumably you wouldn't want to limit object names this way.
- The size column is a FLOAT, which is less than an integer data type, but a FLOAT can hold real number. Figure 9.2 includes sizes in inches and feet, and in practice you'll need to convert everything to one unit—probably inches in this case.
- Note the syntax for the ENUM: the list of values as a whole is the

## EXERCISE 9.3

### Creating a Database

In this exercise, you will continue a small database. This exercise assumes you've performed the steps in "Creating Databases and Tables" and "Storing Data" and that you have a SQL database called test, which contains a table called objects. To complete this database, follow these steps:

- 1. If you're not running MySQL, do so by typing mysql.
- 2. If you're not using the test database, type USE test; to begin the test.
- 3. Type INSERT INTO objects VALUES('tree', 'green', 'medium', 200); (You may split this across lines, if you like). This entry is based on the second row of Figure 9.2, but note that the size value has been expressed in indexes.
- 4. Verify that you entered the data correctly by typing SELECT FROM objects; and verify-ing the new entry is present.
- 5. Repeat step 3 (and 4, if you like) for the remaining rows in Figure 9.2.

## Retrieving Data

The whole point of having a database is to be able to retrieve data from it. The main-mand for doing so has already been described: SELECT. This command's power lies in its ability to accept specifications of what to select. You can use a variety of keywords to select data that matches various criteria, such as exact matches or matches to a range of values. The overall form of SELECT may be described in this way:

```sql
SELECT field(s) FROM table [ WHERE conditions ] [ORDER BY field]
```

Previous of us have used an asterisk (*) as field(s), meaning that the-mand returns all the columns that match the remaining criteria. For instance, suppose you're interested only in the colors and values of objects. You can view this restricted set of data using SELECT:

```sql
mysql> SELECT value,color FROM objects;
+-----------------------+
| value | color |
+-----------------------+
| 10.00 | green |
| 200.00 | green |
+-----------------------+
```
