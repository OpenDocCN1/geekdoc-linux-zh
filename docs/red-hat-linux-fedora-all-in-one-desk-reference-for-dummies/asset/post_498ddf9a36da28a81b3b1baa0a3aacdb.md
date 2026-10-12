
MySQL (pronounced My Ess Que Ell), is a popular relational database (the type of database that works as a collection of connected tables). You can use the Structured Query Language (SQL) to work with the database.

A Swedish company called MySQL AB develops MySQL (www.mysql.com). MySQL AB has released it as an open-source product.

To check whether MySQL is installed on your system, type rpm -q mysql. If a message informs you that the package is not installed, you can install it from the DVD using these steps:

- 1. Log in as root and insert the DVD into the DVD drive.

If you are using GNOME or KDE, the DVD should mount automatically. If not, type the following command in a terminal window to mount the DVD:

```
mount /mnt/cdrom
```

- 2. Type the following commands to install MySQL:

```
cd /mnt/cdrom/RedHat/RPMS
rpm -ivh mysql*
```

This installs all the packages you need to use MySQL on your system.

To use MySQL, you have to first log in as root and start the database server with the following command:

```
/etc/init.d/mysqld start
```

The database server mysqld is a daemon (a background process that runs continuously) that accepts database queries from the MySQL monitor.

Now you have to design a database, create that database in MySQL, and load it with the data. To illustrate how to create and load a database, I set up a simple book catalog database.

## Reviewing the steps to build the database

Follow this basic sequence of steps to build a database:

- 1. Design the database.

This involves defining the tables and attributes that will be used to store the information.

- 2. Create an empty database.

Before you can add tables, database systems require you to build an empty database.

### 3. Create the tables in the database.

In this step, you define the tables using the CREATE TABLE statement of SQL.

### 4. Load the tables with any fixed data.

For example, if you have a table of manufacturer names or publisher names (in the case of books), you want to load that table with information that's already known.

### 5. Back up the initial database.

This step is necessary to ensure that you can create the database from scratch, if necessary.

### 6. Load data into tables.

You may either load data from an earlier dump of the database or interactively through forms.

### 7. Use the database.

Make queries, update records, or insert new records using SQL commands.

## Designing the database

My simple example doesn't follow all the possible steps of database building. For the example, the database-design step is trivial because my book-catalog database includes only a single table. The attributes of that table are as follows:

- Book's title with up to 50 characters
- Name of first author with up to 20 characters
- Name of second author (if any) with up to 20 characters
- Name of publisher with up to 30 characters
- Page count as a number
- Year published as a number (such as 2002)
- International Standard Book Number (ISBN), as a 10-character text (such as 0764542583)

I store the ISBN without the dashes embedded in a typical book's ISBN. I also use the ISBN as the primary key of the table because each ISBN is a worldwide identification system for books. That means each book entry must have a unique ISBN, which we know to be true for books.

## Creating an empty database

To create the empty database in MySQL, use the mysqladmin program. For example, to create an empty database named books, I type the following command:

```
mysqladmin create books
```

You have to log in as root to run the mysqladmin program. As the name suggests, mysqladmin is the database administration program for MySQL.

In addition to creating a database, you can use mysqladmin to remove a database and shut down the database server and check the MySQL version. For example, to see the version information, type the following command:

```
mysqladmin version
```

## Using the MySQL monitor

After you create the empty database, all of your interactions with the database are through the mysql program — the MySQL monitor that acts as a client to the database server. You have to run mysql with the name of a database as an argument. The mysql program then prompts you for input. Here is an example:

```
mysql books
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 10 to server version: 3.23.49

Type 'help;' or '\h' for help. Type '\c' to clear the buffer.

mysql>
```

When creating tables or loading data into tables, a typical approach is to place the SQL statements (along with mysql commands such as \g) in a file and then run mysql with the standard input directed from that file. For example, suppose a file named sample.sql contains some SQL commands that you want to try out on a database named books. Then, you should run mysql with the following command:

```
mysql books < sample.sql
```

I use mysql in this manner to create a database table.

## Defining a table

To create a table named books, I edited a text file named makedb.sql and placed the following line in that file:

```
#
# Table structure for table 'books'
#
CREATE TABLE books (
  isbn CHAR(10) NOT NULL PRIMARY KEY,
  title CHAR(50),
  author1 CHAR(20),
  author2 CHAR(20),
  pubname CHAR(30),
  pubyear INT,
  pagecount INT
) \g
```

CREATE TABLE books is an SQL statement to create the table named books. The \g at the end of the statement is a mysql command. The attributes of the table appear in the lines enclosed in parentheses.

If a table contains fixed data, you can also include other SQL statements (such as INSERT INTO) to load the data into the table right after the table is created.

To execute the SQL statements in the makedb.sql file create the books table, I run mysql as follows:

```
mysql books < makedb.sql
```

Now the books database should have a table named books. (Okay, maybe I should have named them differently, but it seemed convenient to call them by the same name.) I can now begin loading data into the table.

## Inserting records into a table

One way to load data into the table is to prepare SQL statements in another file and then run mysql with that file as input. For example, suppose I want to add the following book information into the books table:

```
isbn = '156884798X'
title = 'Linux SECRETS'
author1 = 'Naba Barkakati'
author2 = NULL
pubname = 'IDG Books Worldwide'
pubyear = 1996
pagecount = 900
```

Then, the following MySQL statement loads this information into the books table:

```
INSERT INTO books VALUES
('156884798X', 'Linux SECRETS', 'Naba Barkakati', NULL,
'IDG Books Worldwide', 1996, 900) \g
```

On the other hand, suppose you have the various fields available in a different order (from the order in which the table's attributes are defined by the CREATE TABLE statement). In that case, you can use a different form of the INSERT INTO command to add the row, as shown in the following example:

```
INSERT INTO books (pubyear, author1, author2, title,
pagecount, pubname, isbn) values
(1996, 'Naba Barkakati', NULL, 'Linux SECRETS', 900, 'IDG
Books Worldwide', '156884798X')\g
```

Essentially, you have to specify the list of attributes as well as the values and make sure that the order of the attributes matches that of the values.

If I save all INSERT INTO commands in a file named additems.sql, then I can load the database from the mysql command line by using the source command like this (type mysql books to start the SQL client):

```
mysql> source additems.sql
```

## Querying the database

You can query the database interactively through the mysql monitor. (Of course, you do have to know SQL to do this operation.) For example, to query the books database, I start the SQL client with the following command:

```
mysql books
```

Then I would type SQL commands at the mysql> prompt to look up items from the database. When done, I type quit to exit the mysql program. Here's an example (all of which I typed in a terminal window):

mysql> select title from books where pubyear < 2000 \g

| title |
|-------|
| Linux SECRETS |
| Red Hat Linux SECRETS, 2nd Edition |

2 rows in set (0.00 sec)
mysql> quit
Bye
