To start the MySQL server immediately, type the following from a Terminal window as root user:

```
# service mysqld start
```

To set the MySQL server to start each time the computer reboots, type the following (as root):

```
# chkconfig mysqld on
```

This sets mysqld to start during most multiuser run states (levels 3, 4, and 5). To check that the service is turned on for those levels, type chkconfig --list mysqld from a Terminal window.

# ## Checking That MySQL Server Is Working

You can use the mysqladmin or mysqlshow commands to check that the MySQL server is up and running. Here’s an example of how to check information about the MySQL server using the mysqladmin command.

```
# mysqladmin -u root -p version proc
Enter password: ******
mysqladmin Ver 8.41 Distrib 5.0.45, for redhat-linux-gnu on i386
Copyright (C) 2000-2006 MySQL AB

This software comes with ABSOLUTELY NO WARRANTY. This is free software,
and you are welcome to modify and redistribute it under the GPL license

Server version		5.0.45
Protocol version		10
Connection		Localhost via UNIX socket
UNIX socket		/var/lib/mysql/mysql.sock
Uptime:				2 days 10 hours 47 min 35 sec

Threads: 2 Questions: 184 Slow queries: 0 Opens: 11 Flush tables: 1 Open
tables: 0 Queries per second avg: 0.004
```

Each of the two options to mysqladmin shown here provides useful information. The version information shows the mysqladmin version is 8.41 and the number assigned to this distribution of the mysql server is 5.0.45. The binary package was created for PC versions of Linux/GNU on the i386 processor. The connection to the server is through a UNIX socket (mysql.sock) on the local host. The server has been up for 2 days, 10 hours, 47 minutes, and 35 seconds. Statistics show that there is one thread (connection to the server) currently active. There have been 184 requests to the server.