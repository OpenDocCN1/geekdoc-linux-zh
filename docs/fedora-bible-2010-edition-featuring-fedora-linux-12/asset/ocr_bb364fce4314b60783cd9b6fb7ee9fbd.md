# # Starting the MySQL Server

For Fedora, the MySQL server is off by default. Turning it on is fairly simple. The /etc/init.d/mysql startup script is delivered with the mysql-server package. To start the server, run the mysqld startup script to have it start immediately, and then set it to start each time your system boots.

To start the MySQL server immediately, type the following from a Terminal window as root user:

```
# service mysqld Start
```

To set the MySQL server to start each time the computer boots, type the following (as root):

```
# chkconfig mysqld on
```

This sets mysqld to start during most multiuser run states (levels 2, 3, 4, and 5). To check that the service is turned on for those levels, type chkconfig --list mysqld from a Terminal window.

# # Checking That MySQL Server Is Working

You can use the mysqladmin or mysqlsh commands to check that the MySQL server is up and running. Here’s an example of how to check information about the MySQL server using the mysqladmin command.

```
# mysqladmin -u root -p version proc
Enter password: ******
mysqladmin  Ver 8.4.2 Distrib 5.1.39, for redhat-linux-gnu on i386
Copyright (C) 2000-2008 MySQL AB, 2008 Sun Microsystems, Inc.
This software comes with ABSOLUTELY NO WARRANTY. This is free software, and you are welcome to modify and redistribute it under the GPL license

Server version		5.1.39
Protocol version	10
Connection		Localhost via UNIX socket
UNIX socket		/var/lib/mysql/mysql.sock
Uptime:			2 days 10 hours 47 min 35 sec

Threads: 2  Questions: 184  Slow queries: 0  Opens: 15  Flush tables: 1  Open tables: 8  Queries per second avg: 0.25
--------------------------------------------------
| Id | User | Host | db | Command | Time | State | Info |
--------------------------------------------------
| 3  | root | localhost | | Query | 0 | | show processlist |
--------------------------------------------------
```