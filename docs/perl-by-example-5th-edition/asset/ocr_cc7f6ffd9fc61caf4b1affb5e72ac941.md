# EXAMPLE B.1

```
1    mysql> SHOW databases;
      +----------------+
      | Database       |
      +----------------+
      | mysql          |
      | northwind      |
      | phpmyadmin     |
      | test           |
      +----------------+
4 rows in set (0.03 sec)
```

The USE Command. The USE command makes the specified database your default database. From that point on, all SQL commands will be performed on the default database. This is one of the few commands that does not require a semicolon to terminate it.

# FORMAT

USE database_name;

# EXAMPLE B.2

```
1    mysql> USE northwind;
       Database changed
```

# EXPLANATION

The USE command changes the database to northwind. The command-line client will report that the database has been changed.

# B.1.5 SQL Database Tables

A database usually contains one or more tables. Each table is identified by a name, such as Customers or Orders. The SHOW TABLES IN command displays all the tables within a database, as shown in Figure B.5. The SELECT * FROM command lists all the fields and rows in a specified table. Tables contain rows, called records, and columns, called fields. The table in Figure B.6 contains three records (one for each shipper) and three columns (ShipperID, CompanyName, and Phone).