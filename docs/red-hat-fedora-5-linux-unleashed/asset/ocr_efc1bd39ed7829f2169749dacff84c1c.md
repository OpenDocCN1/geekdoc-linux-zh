# Procedural Languages and Triggers

A *procedural language* is an external programming language that can be used to write functions and procedures. This allows you to do things that aren't supported by simple SQL. A *trigger* allows you to define an event that will invoke the external function or procedure you have written. For example, a trigger can be used to cause an exception if an INSERT statement containing an unexpected or out-of-range value for a column is given.

For example, in the CD tracking database, you could use a trigger to cause an exception if a user entered data that did not make sense. PostgreSQL has a procedural language called PL/pgSQL. Although MySQL has support for a limited number of built-in procedures and triggers, it does not have any procedural language. This means you cannot create custom procedures or triggers in MySQL, although the same effects can often be achieved through creative client-side programming.

# Configuring MySQL

A free and stable version of MySQL is included with Fedora. MySQL is also available from the website [http://www.mysql.com/](http://www.mysql.com/). The software is available in source code, binary, and RPM format for Linux. You can elect to have MySQL installed when you install Fedora or later use the *system-config-packages* client to add the software to your system. See Chapter 7 for the details on adding (or removing) software.

After you install MySQL, you need to initialize the *grant tables*, or permissions to access any or all databases and tables and column data within a database. You can do this by issuing `mysql_install_db` as root. This command initializes the grant tables and creates a MySQL root user.

![](bbox=[0.15, 0.6, 0.92, 0.7])

Running `mysql_install_db` should generate output similar to the following:

```
# mysql_install_db
Preparing db table
Preparing host table
Preparing user table
Preparing func_table
Preparing tables_priv table
Preparing columns_priv table
Installing all prepared tables
020916 17:39:05 /usr/libexec/mysqld: Shutdown Complete
```