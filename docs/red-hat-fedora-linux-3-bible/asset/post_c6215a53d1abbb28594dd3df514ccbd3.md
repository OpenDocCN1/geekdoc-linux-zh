
# chkconfig mysqld on

This sets `mysqld` to start during most multiuser run states (levels 3, 4, and 5). To check that the service is turned on for those levels, type **chkconfig --list mysqld** from a Terminal window.

# Checking That MySQL Server Is Working

You can use the `mysqladmin` or `mysqldshow` commands to check that the MySQL server is up and running. Here’s an example of how to check information about the MySQL server using the `mysqladmin` command.

```bash
# mysqladmin -u root -P version proc
Enter password: ********
MySQLadmin  Ver 8.23 Distrib 3.23.58, for redhat-linux-gnu on i386
Copyright (C) 2000 MySQL AB & MySQL Finland AB & TCX DataKonsult AB
This software comes with ABSOLUTELY NO WARRANTY. This is free software,
and you are welcome to modify and redistribute it under the GPL license

Server version		3.23.58
Protocol version		10
Connection		Localhost via UNIX socket
UNIX socket		/var/lib/mysql/mysql.sock
Uptime:			2 day 10 hours 47 min 35 sec

Threads: 1  Questions: 184  Slow queries: 0  Opens: 1  Flush tables: 3
Open tables: 1 Queries per second avg: 0.001

+----+------+-----------+------+---------------------+------+------------------------+
| Id | User | Host      | db   | Command | Time | State | Info                 |
+----+------+-----------+------+---------------------+------+------------------------+
| 52 | root | localhost: |      | Query   | 0    |    | show processlist      |
+----+------+-----------+------+---------------------+------+------------------------+
```

Each of the two options to `mysqladmin` shown here provides useful information. The version information shows the `mysqladmin` version is 8.23 and the number assigned to this distribution of the `mysql` server is 3.23.58. The binary package was created for PC versions of Linux/GNU on the i386 processor. The connection to the server is through a UNIX socket (`mysql_.sock`) on the local host. The server has been up for 2 days, 10 hours, 47 minutes, and 35 seconds. Statistics show that there is one thread (connection to the server) currently active. There have been 184 requests to the server.

The `proc` option shows that one client is currently connected to the server. That client is logged into MySQL as the root user on the `localhost`. The client that has an Id of 52 (which tells you who the user is, allowing you to use that information, as the server’s administrator, if you wanted to disconnect the user) is currently querying the MySQL database.

If the server were not running at the moment, the `mysqladmin` command shown in the previous example would result in a failure message:
mysqladmin: connect to server at `localhost` failed.

Recommended remedies are to try to restart the server (by typing `service mysql restart`) or to make sure that the socket exists (`/var/lib/mysql/mysql.sock`).

# Working with MySQL Databases

The first time you start the MySQL server (using the start-up script described previously), the system creates the initial grant tables for the MySQL database. It does this by running the `mysql_install_db` command.

The `mysql_install_db` command starts you off with two databases: `mysql` and `test`. As you create data for these databases, that information is stored in the `/var/lib/mysql/mysql` and `/var/lib/mysql/test` directories, respectively.

Because the MySQL root user doesn't have to be the system's root user (provided you have the MySQL root user's password), you can be logged into Fedora as any user you choose. In the following examples, be sure to provide the MySQL root user password when you run the commands shown.

## Starting the `mysql` command

To get started creating databases and tables, you can use the `mysql` command. From any Terminal window, open the `mysql` database on your computer by typing the following:

```bash
$ mysql -u root -p mysql
Enter password: ********

Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 39 to server version: 3.23.58

Type 'help;' or '\h' for help. Type '\c' to clear the buffer

mysql>
```

Type in the root user's MySQL password as prompted. (If no password has been set, you can skip the `-p` option.) The `mysql>` prompt appears, ready to accept commands for working with the `mysql` default database on the localhost. If you are connecting to the MySQL server from another host computer, add `-h hostname` to the command line (where `hostname` is the name or IP address of the computer on which the MySQL server is running). Remember, you can also log in as any valid `mysql` login you created, regardless of which Linux login account you are currently logged in under.

As the MySQL monitor welcome text notes, be sure to end each command that you type with a semicolon (;) or \g. If you type a command and it appears to be waiting for more input, it's probably because you forgot to put a semicolon at the end.

Before you begin using the `mysql` interface to create databases, try checking the status of the MySQL server using the status command. The following is an example of output from the status command:

```mysql
mysql> status
--------------------
mysql  Ver 11.18_Distrib 3.23.58, for pc-linux-gnu (i686)
Connection id:          43
Current database:       mysql
Current user:           root@localhost
Current pager:          stdout
Using outfile:          ''
Server version:         3.23.58
Protocol version:       10
Connection:             localhost via UNIX socket
Client character-set:   latin1
Server character-set:   latin1
UNIX socket:            /var/lib/mysql/mysql.sock
Uptime:                 1 day 2 hours 57 min 19 sec

Threads: 1  Questions: 136  Slow queries: 0  Opens: 12
Flush tables: 1  Open tables: 6 Queries per second avg: 0.001
--------------------
```

The status information tells you about the version of the MySQL server (11.18) and the distribution (3.23.58). The output also reminds you of the current database (`mysql`) and your user name (`root@localhost`). You can see how long the server has been up (Uptime). You can also see how many threads are currently active and how many commands have been run to query this server (Questions).

## Creating a database with mysql

Within an interactive `mysql` session, you can create and modify databases and tables. If you are not already connected to a `mysql` session, type the following command (assuming the `mysql` user name of root):

```bash
$ mysql -u root -p
Enter password: ********
mysql>
```

The general steps for creating a MySQL database include creating the database name, identifying the new database as the current database, creating tables, and adding data to the tables. While you are connected to a mysql> session, you can run the following procedure to create a sample database.

1. To create a new database name, use the CREATE DATABASE command at the mysql> prompt. For example, to create a database named allusers, type the following:
   ```mysql
   mysql> CREATE DATABASE allusers;
   ```
   This action creates a database called allusers in the /var/lib/mysql directory. (While you don't have to use capitals for the commands just shown, it makes it easier to distinguish the commands from the database entities.)

   > **NOTE:** Alternatively, you could create a database from the command line using the mysqladmin command. For example, to create the database named allusers with mysqladmin, you could type the following: `mysqladmin -u root -p create allusers`

2. To see what databases are available for your mysql server, type the following at the mysql> command prompt:
   ```mysql
   mysql> SHOW DATABASES;
   +--------------------+
   | Database           |
   +--------------------+
   | allusers           |
   | mysql              |
   | test               |
   +--------------------+
   3 rows in set (0.00 sec)
   ```
   The databases shown here are named allusers, mysql, and test. The allusers database is the one created in the previous step. The mysql database contains user access data. The test database is created automatically for creating test mysql databases.

3. To work with the database you just created (allusers), you need to make allusers your current database. To do that, type the following at the mysql> command prompt:
   ```mysql
   mysql> USE allusers;
   Database changed
   ```

4. Creating a table for your database requires some planning and understanding of table syntax. You can type in the following commands and column information to try out creating a table. For more detailed information on creating tables and using different data types, refer to the section “Understanding MySQL Tables” later in this chapter.
   To create a table called names, use the following CREATE TABLE command at the mysql> prompt:
   ```mysql
   mysql> CREATE TABLE names (
   -> firstname varchar(20) not null,
   ```
