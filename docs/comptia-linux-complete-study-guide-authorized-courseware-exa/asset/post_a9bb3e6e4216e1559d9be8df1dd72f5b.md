
# Managing Data with SQL

The Structured Query Language (SQL), as its expanded name suggests, is a language used for retrieving data from a database. In practice, SQL is implemented in several different database products. Thus, you should know a little about the SQL products that are available for Linux. With a SQL package installed, you can begin learning about the principles of SQL use and move on to actual data storage and retrieval.

## Picking a SQL Package

SQL is a language for accessing data, and specific SQL packages implement that language. This distinction is similar to that between a network protocol (such as SMTP) and the servers that implement it (such as sendmail, Postfix, and Exim). In principle, you can use any SQL package to satisfy your SQL database needs. In practice, specific products that store data using SQL may work better with (or even require) particular packages. Some of the more common choices in Linux include the following:

- **MySQL** Oracle owns this SQL implementation, which has been released under the GPL. Most major Linux distributions include MySQL in their package databases. For a complete installation, you’ll probably need to install multiple packages, such as a client, a server, and perhaps development tools. You can learn more at http://www.sun.com/software/products/mysql/.
- **PostgreSQL** This SQL implementation evolved from the earlier Ingres software (the name *PostgreSQL* is a compressed form of *post-Ingres SQL*). It’s available under the BSD license and is available as multiple packages in most Linux distributions. As with MySQL, you’ll most likely have to install a client, a server, and perhaps additional support packages. PostgreSQL is headquartered at http://www.postgresql.org.
- **SQLite** This package, based at http://www.sqlite.org, is a library that implements SQL. As such, it’s not a standalone database; instead, it’s intended as a way to provide programs with a way to store data using a SQL interface within the program. If you install a program that uses SQLite, your distribution’s package manager should install the relevant libraries for you. If you want to write a program that requires database access and you don’t want to install a complete client/server SQL package such as MySQL or PostgreSQL, SQLite may be just what you need.

There are literally dozens more SQL database products for Linux. For the purpose of learning SQL, MySQL or PostgreSQL should do fine, or you can use another full implementation if you prefer. If you have a specific purpose in mind for using SQL, though, you should research SQL packages in more detail. You may need a particular product for compatibility with other software, or you may need a SQL package that provides specific features.

As just noted, some SQL packages, including MySQL and PostgreSQL, operate on a client-server model: One program (the server) manages the database, while another (the client) provides users and programs with access to the database. Such implementations can work over a network, enabling users at multiple client systems to access a centralized database server.

## Understanding SQL Basics

SQL is a tool for accessing databases, and more specifically, relational databases. Figure 9.2 illustrates data in a relational database. Each row (sometimes known as a tuple) represents a single object or other item, and each column (sometimes referred to as an attribute or field) represents a specific feature. The combination of rows and columns is referred to as a table. Each database may contain multiple tables, and SQL supports multiple databases. Thus, to access data, you must first select a database and a table, as described in more detail shortly.

The data in a table are unordered, at least conceptually. (In practice, of course, data will be stored in some order on disk, but this order is arbitrary.) You can impose an order on query results, as described shortly; for instance, you may retrieve data from the database represented by Figure 9.2 and order the results according to cost (the final column).

![](img/f339a9f48c4b443e61c74acb4c9c3da4_515_0.png)

A database enables retrieval of information that matches specific criteria. You can search for all the green objects in Figure 9.2, for instance. You can also insert, delete, and update information in a table. SQL supports multiple tables, so you can have, for instance, different tables for property in your office and for employees who work in your office.

Columns (attributes) in a database hold specific types of data, and swapping them around makes little sense. For instance, it's clear that the second column in Figure 9.2 is a color, whereas the final column is a price or value, expressed in dollars. It would make little sense to enter green as a value or $1.00 as a color. The restrictions placed on what may appear in a column are known as a domain or a data type: The domain for the second column is a set of color names, whereas the domain for the final column is a numeric value expressed in dollars. Table 9.3 summarizes some common SQL data types.

### Table 9.3 Common SQL Data Types

| Data Type Name | Purpose |
| :--- | :--- |
| INTEGER (a.k.a. INT) | 4-byte integer value |
| SMALLINT | 2-byte integer value |
| DECIMAL | Precision storage of decimal values |
| NUMERIC | Precision storage of decimal values |
| FLOAT | Floating-point number |
| DOUBLE PRECISION | Floating-point number stored with twice the precision of FLOAT |
| DATETIME | A date and time |
| DATE | A date |
| TIME | A time, in *HH:MM:SS* format; may be a time of day or a period of time |
| CHAR | One or more characters |
| VARCHAR | A variable number of characters |
| ENUM | An enumerated list, such as one of *small*, *medium*, or *large* |
| SET | Data that may have zero or more values, as in any of the set of *nuts*, *sprinkles*, *fudge*, and *cherry* for ice cream toppings |

Additional data types exist; Table 9.3 is intended to give you a feel for what’s available and to list some of the data types you’re likely to encounter. Some implementations support unique data types, too. Each of these data types has its own features. For instance, the numeric data types (INTEGER, DECIMAL, and so on) can be manipulated by arithmetic operators.

## Using MySQL

To learn about SQL, you should have access to a SQL database. For purposes of demonstration, I’m using MySQL as a reference. Other SQL implementations are similar to what I describe here, but some details differ. One of these details is how to start the database. In the case of MySQL, your distribution should include a SysV or other startup script for the SQL server. This server may also need to be configured with its own root password. Debian and related distributions will prompt for this when you install the package, but you may need to set this manually with other distributions.

### Starting to Use MySQL

To begin a SQL session, you should first ensure that the server is running, as just described. You can then start the SQL client. In the case of MySQL, this program is called `mysql`:

```
$ mysql
```

If you've just installed MySQL for learning purposes, it may have no databases defined. To learn what's defined, you can use the `SHOW DATABASES` command:

```
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
+--------------------+
1 row in set (0.00 sec)
```

![](img/f339a9f48c4b443e61c74acb4c9c3da4_517_0.png)

In this example, one database is already defined: `information_schema`. Some installations define a database called `test`. If you see such a database, you can probably use it for your own tests; however, other users may be able to see and modify this database, so don't store important data in it. If you're not in charge of the SQL installation, you should double-check with whoever is in charge of it to be sure you can use the `test` database—or any other database, for that matter.

### Creating Databases and Tables

If no database for testing purposes exists, you can create one with the `CREATE DATABASE` command, which takes a database name as an option:

```
mysql> CREATE DATABASE test;
Query OK, 1 row affected (0.00 sec)
```
