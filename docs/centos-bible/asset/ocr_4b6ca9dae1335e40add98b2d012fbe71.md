# **Part IV Networking**

As the MySQL monitor welcome text notes, be sure to end each command that you type with a semicolon (;) or \9. If you type a command and it appears to be waiting for more input, it's probably because you forgot to put a semicolon at the end.

Before you begin using the `mysql` interface to create databases, try checking the status of the MySQL server using the `status` command. The following is an example of output from the `status` command:

```
```
mysql> status

mysql  Ver 14.12 Distrib 5.0.45, for redhat-linux-gnu (i386) using
readline 5.0

Connection id:  26
Current database: mysql
Current user: root@localhost
Current pager: stdout
Using outfile: ''
Server version: 5.0.45
Protocol version: 10
Connection: localhost via UNIX socket
Server charset: latin1
Db charset: latin1
Client charset: latin1
Comm. charset: latin1
UNIX socket: /var/lib/mysql/mysql.sock
Uptime: 1 day 2 hours 57min 19 sec

Threads: 1 Questions: 136 Slow queries: 0 Opens: 12
Flush tables: 1 Open tables: 6 Queries per second avg: 0.001
```
```

The status information tells you about the version of the MySQL server (14.12) and the distribution (5.0.45). The output also reminds you of the current database (`mysql`) and your username (`root@localhost`). You can see how long the server has been up (Uptime). You can also see how many threads are currently active and how many commands have been run to query this server (Questions).

# Creating a Database with MySQL

Within an interactive `mysql` session, you can create and modify databases and tables. If you are not already connected to a `mysql` session, type the following command (assuming the MySQL username of `root`):

```
```
$ mysql -u root -p
Enter password: ********
mysql>
```
```