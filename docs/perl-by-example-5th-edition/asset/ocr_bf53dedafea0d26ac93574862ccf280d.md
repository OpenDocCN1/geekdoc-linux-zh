# EXAMPLE B.24

```
1 mysql> CREATE DATABASE gallerydb;
     Query OK, 1 row affected (0.03 sec)

2 mysql> show databases;
  +-----------------+
  | Database        |
  +-----------------+
  | gallerydb       |
  | mysql           |
  | northwind       |
  | phpmyadmin      |
  | test            |
  +-----------------+
  5 rows in set (0.00 sec)
```

# EXPLANATION

That's it. The database is now created. Note that just because we created the database, we are still not in that database. The USE command in the next example will make the new database the current default database.

# EXAMPLE B.25

```
1 mysql> USE gallerydb;
   Database changed
```

# EXPLANATION

We are now in the gallerydb database, and all the SQL commands will be executed on that database.

# B.3.2 SQL Data Types

After creating a database, you will add the tables that make up the database. Before creating a table, you have to decide what kind of data will be stored in it; for example, will you have rows of names, dates, part numbers, Social Security numbers, prices, and so on? The data type specifies what type of data the column can hold. The basic types are string, numeric, and date and time types. For a fully documented list, see http://dev.mysql.com/doc/refman/5.0/en/data-types.html.

Table B.3 contains the most common data types in SQL.