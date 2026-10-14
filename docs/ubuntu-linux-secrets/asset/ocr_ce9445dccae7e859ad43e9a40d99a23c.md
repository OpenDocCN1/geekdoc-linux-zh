# The MySQL Software

A main component of a successful dynamic web page environment is a database for storing and accessing data. The most popular database platform used in the open-source world is the MySQL database server.

Much of the popularity of MySQL comes from it being the original default database used in the PHP programming language (however, PHP can now interface with many different database packages), as well as the speed of the MySQL database server.

The original MySQL database server was well known for being fast but not overly robust. It lacked many of the advanced features commonly found in commercial databases, such as transactions, foreign keys, and row-level record locking.

To solve this problem, the developers at MySQL redesigned MySQL to work with multiple storage engines. A storage engine is the core of the database server. It handles the database interface—storing, managing, and deleting data for the server.

MySQL now supports several different types of storage engines, each one with a different specialty. Table 21-3 lists the different storage engines available in MySQL.

| Table 21-3: The MySQL Storage Engines |
| Engine | Description |
| MyISAM | The original storage engine; speedy, but lacking many advanced database features |
| InnoDB | The newest, full-featured storage engine; although it supports many commercial-quality features, it's significantly slower than the MyISAM storage engine |
| Memory | Provides tables in memory |
| Merge | Combines multiple MyISAM tables into a single table |
| CSV | Stores data as comma-separated values in text files |

Many high-volume web application sites still use the original MyISAM storage engine for its speed qualities, forsaking advanced features for performance.

The following sections describe how to use the MySQL database server installed on the Ubuntu server.

# Accessing the Server

On the Ubuntu server you access the MySQL server via a command-line interface tool. The mysql program allows you to connect to the MySQL server, execute SQL commands, and view the results.

To connect to the default MySQL database using the root user account, type

```
mysql -u root -p
```

After entering the password, you should be at the MySQL prompt:

```
$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor. Commands end with : or \g.
```