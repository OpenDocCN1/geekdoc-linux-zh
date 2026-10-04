# Open Source RDBMS (cont'd.)

| PostgreSQL | http://www.postgresql.org |
|---|---|

Perhaps the most sophisticated open-source database system. Tailored toward sophisticated multi-user applications. Better suited for write-intensive applications than MySQL.

| Interbase | http://www.interbase.com |
|---|---|

A robust open source database from Barland. As widely used as MySQL and PostgreSQL, but growing in popularity.

| ODBC | http://www.adbc.com |
|---|---|

Nat a database itself, but standard interface that allows you to connect to nearly any database (such as MS SQL Server or even MS Access).

This chapter will not attempt to turn you into a database or SQL specialist. In fact, if you are like web programmers, you will probably leave the relational modeling and the database programming to someone else. Instead, we will focus on how to connect your programmed database to Zope using the open-source database MySQL as an example. MySQL is widely used for web applications because it is simple and its high performance is well suited to the web.

# 12.3 The MySQL Database

Before attempting to work with MySQL under Zope, be sure that you have a MySQL server (version 3.22.32 or higher) running on your computer. (Please refer to the documentation included with MySQL to install and run the database server.) Once it is running, you will log in to the database server and create a data-base for use in Zope.

# 12.3.1 Starting MySQL Monitor

The MySQL monitor is a command line program that allows you to access and administer MySQL databases. (DOS prompt for Windows users), using the following command to run the MySQL monitor:

```
mysql -h host -u user -p
Enter password: ********
```

You'll need to enter the host parameter if the MySQL server is running on a different computer. For the user parameter, enter the username you use on the MySQL server. Once you have logged in, the following text appears: