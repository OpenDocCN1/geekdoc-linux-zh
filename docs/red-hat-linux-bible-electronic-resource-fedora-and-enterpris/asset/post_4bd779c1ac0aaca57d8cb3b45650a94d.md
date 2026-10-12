
```
# mysqladmin variables | less
```

| Variable_name | Value |
|---|---|
| back_log | 50 |
| basedir | /usr/ |
| db_cache_size | 8388600 |
| db_log_buffer_size | 32768 |
| db_home | /var/lib/mysql/ |
| db_max_lock | 10000 |
| db_logdir |  |
| db_shared_data | OFF |
| db_tmpdir | /tmp/ |
|  | ... |
|  | ... |
| tmp_table_size | 33554432 |
| tmpdir | /tmp/ |
| version | 3.23.57 |
| wait_timeout | 28800 |

If you decide that the option and variable settings that come with the default MySQL system don't exactly suit you, you don't have to start from scratch. Sample my.cnf files that come with the mysql package can let you begin with a set of options and variables that are closer to the ones you need.

## Using sample my.cnf files

Sample my.cnf files are available in the `/usr/share/doc/mysql-server*` directory. To use one of these files, do the following:

- 1. Keep a copy of the old my.cnf file:
    ```sh
    # mv /etc/my.cnf /etc/my.cnf.old
    ```

- 2. Copy the sample my.cnf file you want to the `/etc/my.cnf` file. For example, to use the my-medium.cnf file, type the following:
    ```sh
    # cp /usr/share/doc/mysql-server*/my-medium.cnf /etc/my.cnf
    ```

- 3. Edit the new `/etc/my.cnf` file (as root user) using any text editor to further tune your MySQL variables and options.

The following paragraphs describe each of the sample my.cnf files:

### my-small.cnf

This options file is recommended for computer systems that have less than 64MB of memory and are only used occasionally for MySQL. With this options file, MySQL won't be able to handle a lot of usage but it won't be a drag on the performance of your computer.

For the mysqld server, buffer sizes are set low - only 64K for the `sort_buffer` and 16K for the `key_buffer`. The `thread_stack` is only set to 64K and `net_buffer_length` is only 2K. The `table_cache` is set to 4.

### my-medium.cnf

As with the small options file, the my-medium.cnf file is intended for systems where MySQL is not the only important application running. This system also has a small amount of total memory available - between 32MB and 64MB - however more consistent MySQL use is expected.

The `key_buffer` size is set to 16M in this file, while the `sort_buffer` value is raised to 512K for the mysqld server. The `table_cache` is set to 64 (allowing more simultaneous threads to be active). The `net_buffer_length` is raised to 8K.

### my-large.cnf

The my-large.cnf sample file is intended for computers that are dedicated primarily to MySQL service. It assumes about 512M of available memory.

Server buffers allow more active threads and better sorting performance. Half of the system's assumed 512M of memory is assigned to the `key_buffer` variable (256M). The `sort_buffer` size is raised to 1M. The `table_cache` allows more simultaneous users (up to 256 active threads).

### my-huge.cnf

As with the my-large.cnf file, the my-huge.cnf file expects the computer to be used primarily for MySQL. However, the system for which it is intended offers much more total memory (between 1G and 2G of memory).

Sort buffer size (`sort_buffer`) is raised to 2M while the `key_buffer` is set to consume 384M of memory. The `table_cache` size is doubled to allow up to 512 active threads.

## Starting the MySQL Server

For Red Hat Linux, the MySQL server is off by default. To turn it on, however, is fairly simple. The /etc/init.d/mysqld start-up script is delivered with the mysql-server package. To start the server, you can either run the mysqld start-up script manually or set it to start each time your system boots.

To start the MySQL server manually, type the following from a Terminal window as root user:

```
# service mysqld start
```

To have the MySQL server start each time the computer reboots, type the following (as root):

```
# chkconfig mysqld on
```

This sets mysqld to start during most multiuser run states (levels 3, 4, and 5). To check that the service is turned on for those levels, type `chkconfig --list mysqld` from a Terminal window.

## Checking That MySQL Server Is Working

You can use the `mysqladmin` or `mysqlshow` commands to check that the MySQL server is up and running. Here’s an example of how to check information about the MySQL server using the `mysqladmin` command.

```
# mysqladmin -u root -p version proc
Enter password: *******
mysqladmin  Ver 8.23 Distrib 3.23.57, for pc-linux-gnu on i686
Copyright (C) 2000 MySQL AB & MySQL Finland AB & TCX DataKonsult AB
This software comes with ABSOLUTELY NO WARRANTY. This is free software,
and you are welcome to modify and redistribute it under the GPL license

Server version                 3.23.57
Protocol version               10
Connection                     Localhost via UNIX socket
UNIX socket                    /var/lib/mysql/mysql.sock
Uptime:                        2 days 10 hours 47 min 35 sec

Threads: 1  Questions: 184  Slow queries: 0  Opens: 1  Flush tables: 3
Open tables: 1  Queries per second avg: 0.001

+-----------------------------------+-----------------------------------+
| Id | User | Host | db | Command| Time | State | Info |
+-----------------------------------+-----------------------------------+
|  52 | root | localhost| mysql| Query | 0 | | show processlist |
+-----------------------------------+-----------------------------------+
```

| Id | User | Host | db | Command | Time | State | Info |
|---|---|---|---|---|---|---|---|
| 52 | root | localhost | mysql | Query | 0 |  | show processlist |

Each of the two options to `mysqladmin` shown here provides useful information. The version information shows the `mysqladmin` version is 8.23 and the number assigned to this distribution of the mysql server is 3.23.57. The binary package was created for PC versions of Linux/GNU on the i686 processor. The connection to the server is through a UNIX socket (`mysql.sock`) on the local host. The server has been up for 2 days, 10 hours, 47 minutes, and 35 seconds. Statistics show that there is one thread (connection to the server) currently active. There have been 184 requests to the server.

The `proc` option shows that one client is currently connected to the server. That client is logged into MySQL as the root user on the localhost. The client that has an Id of 52 (which
you could use, as the server's administrator, if you wanted to disconnect the user) is currently querying the MySQL database.
If the server were not running at the moment, the `mysqladmin` command shown above would result in a failure message:

```
mysqladmin: connect to server at 'localhost' failed.
```

Recommended remedies are to try to restart the server (by typing `/etc/init.d/mysqld restart`) or to make sure that the socket exists (`/var/lib/mysql/mysql.sock`).

## Working with MySQL Databases

The first time you start the MySQL server (using the start-up script described previously), the system creates the initial grant tables for the MySQL database. It does this by running the `mysql_install_db` command.

> NOTE: If for some reason the grant tables are not initialized, you can run the `mysql_install_db` command yourself (as root user). Running the command more than once won't hurt anything.

The `mysql_install_db` command starts you off with two databases: `mysql` and `test`. As you create data for these databases, that information is stored in the `/var/lib/mysql/mysql` and `/var/lib/mysql/test` directories, respectively.

### Starting the mysql command

To get started creating databases and tables, you can use the `mysql` command. From any Terminal window, open the `mysql` database on your computer by typing the following:

```
# mysql -u root -p mysql
Enter password: ********

Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 39 to server version: 3.23.57
Type 'help;' or '\h' for help. Type '\c' to clear the buffer
mysql>
```

Type in the root user's MySQL password as prompted. The `mysql>` prompt appears, ready to accept commands for working with the `mysql` default database on the localhost. If you are connecting to the MySQL server from another host computer, add `-h hostname` to the command line (where `hostname` is the name or IP address of the computer on which the MySQL server is running). Remember, you can also log in as any valid `mysql` login you created, regardless of which Linux login account you are currently logged in under.
