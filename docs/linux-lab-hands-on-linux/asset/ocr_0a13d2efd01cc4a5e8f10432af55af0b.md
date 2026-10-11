Alternatively, *mysql* CLI to create a database using the *mysqladmin* command given as follows:

```
[root@netman opt] #mysqladmin -u root -p create allusers
```

+   For viewing the databases that are available for your *mysql* server, type the following command at the *mysql>* command prompt:

```
mysql> SHOW DATABASES;
```

The database appears as follows:

```
+-------------------+
| Database          |
+-------------------+
| information_schema |
| allusers          |
| mysql             |
| test              |
+-------------------+
4 rows in set (0.00 sec)
```

The databases shown here are named *information_schema*, *allusers*, *mysql*, and *test*. The *information_schema* database contains metadata about information in other databases on your server (such as the types of data, columns, or tables used in each). The *allusers* database is the one created in the previous step. The *mysql* database contains user access data. The *test* database is created automatically for creating test *mysql* databases.

+   Working with the database that you just created (*allusers*), you need to make *allusers* your current database. To do that, type the following command at the *mysql>* command prompt:

```
mysql> USE allusers;
Database changed
```

+   Creating a table for your database requires some planning and understanding of table syntax. You can type in the following commands and column information to try out creating a table. For more detailed information on creating tables and using different data types, refer to the section “Understanding MySQL Tables” later in this chapter.

To create a table called *name*, use the following CREATE TABLE command at the *mysql>* prompt:

```
mysql> CREATE TABLE name (
-> firstname varchar(20) not null,
-> lastname varchar(20) not null,
-> streetaddr varchar(30) not null,
-> city varchar(20) not null,
-> state varchar(20) not null,
-> zipcode varchar(10) not null
-> );
Query OK, 0 rows affected (0.00 sec)
```

You have now created a table called *name* for a database named *allusers*. It contains columns called *firstname*, *lastname*, *streetaddr*, *city*, *state*, and *zipcode*.