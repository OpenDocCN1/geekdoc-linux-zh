# Using a Database

| Database |
| information_schema |
| mysql |
| 2 rows in set (0.00) |

```
mysql>
```

This feature can come handy when you're working with long commands. You can enter part of the command on a line and press the Enter key, then continue on the next line. This can continue for as many lines as you like until you use the semicolon to indicate the end of the command.

> Throughout this chapter you'll see me upper-case letters for SQL commands. This has become a common way to write SQL commands, however, the mysql program allows you to specify SQL commands using either upper-case or lower-case.

# Creating MySQL database objects

Before you can start writing your shell scripts to interact with a database, you'll need a few database objects to work with. At a minimum, you'll want to:

+   - A unique database to store your application data
- A unique user account to access the database from your scripts
- One or more data tables to organize your data

You build all of these objects using the mysql program. The mysql program interfaces directly with the MySQL server, using SQL commands to create and modify any of the objects.

You can send any type of SQL commands to the MySQL server using the mysql program. This section walks through the different SQL statements you'll need to build the basic database objects for your shell scripts.

# Creating a database

The MySQL server organizes data into databases.A database usually holds the data for a single application, separating from other applications that use the database server. Creating a separate database for each shell script helps eliminate confusion and data mix-ups.

The SQL statement required to create a new database is:

```
CREATE DATABASE name;
$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor. Commands end with ; or \
```

That's pretty. Of course, you must have the proper privileges to create new databases on the MySQL server. The easiest way is to log in as the root user account: