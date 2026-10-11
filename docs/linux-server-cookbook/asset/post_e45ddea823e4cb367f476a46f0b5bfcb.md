
Table 11.2: Option groups and descriptions

| Option Group | Description |
| :--- | :--- |
| `[mysqld-10.4]` | For example, `[mariadb]`. Options read by **MariaDB Server**. |
| `[mariadb]` | Options read by **MariaDB Server**. |
| `[mariadb-X.Y]` | Options read by a specific version of **MariaDB Server**. For example, `[mariadb-10.4]`. |
| `[mariadbd]` | Options read by **MariaDB Server**. Available starting with **MariaDB 10.4.6**. |
| `[mariadbd-X.Y]` | Options read by a specific version of **MariaDB Server**. For example, `[mariadbd-10.4]`. Available starting with **MariaDB 10.4.6**. |
| `[galera]` | Options read by MariaDB Server, but only if it is compiled with Galera Cluster support. |

The default port used by the **MariaDB server** is 3306 on protocol **Transmission Control Protocol (TCP)**. The service will be listening in the interfaces matching the **bind-address** specified or in all interfaces if the specified IP is 0.0.0.0. The package includes the following three commands to start the service:

- **mariadbd**: The main service used by the service **mariadb.service**.
- **mariadbd-multi**: In systems running server *database services*, it is required to use this command instead the default one.
- **mariadbd-safe**: Used to start the service without *systemd*. This approach is needed to start troubleshooting or performing a recovery of a failed database server.

It is possible to use the option `--print-defaults` for the command **mariadbd** (or **mysqld**) to show on the screen the options read from the configuration files, as is shown in figure 11.10:

```
root@ubuntu:~# mariadbd --print-defaults
mariadbd would have been started with the following arguments:
--socket=/run/mysqld/mysqld.sock --pid-file=/run/mysqld/mysqld.pid --basedir=/usr
--bind-address=127.0.0.1 --expire_logs_days=10 --character-set-server=utf8mb4 --collation-server=utf8mb4_general_ci
```

Figure 11.10: Output example command mariadbd

The service **mariadbd** (or **mysqld**) is executed under the user **mysql** and the group **mysql**. When the service is started, the logs are redirected to **journald** or the file /var/log/mariadb/mariadb.log, depending on the configuration previously described. The following code shows an example of the information shown after starting.

```
Starting MariaDB 10.6.7 database server...
2022-09-18 21:06:11 0 [Note] /usr/sbin/mariadbd (server 10.6.7-MariaDB-2ubuntu1.1) starting as process 3083 ...
2022-09-18 21:06:11 0 [Note] InnoDB: Compressed tables use zlib 1.2.11
2022-09-18 21:06:11 0 [Note] InnoDB: Number of pools: 1
2022-09-18 21:06:11 0 [Note] InnoDB: Using crc32 + pclmulqdq instructions
2022-09-18 21:06:11 0 [Note] InnoDB: Initializing buffer pool, total size = 134217728, chunk size = 134217728
2022-09-18 21:06:11 0 [Note] InnoDB: Completed initialization of buffer pool
2022-09-18 21:06:11 0 [Note] InnoDB: 128 rollback segments are active.
2022-09-18 21:06:11 0 [Note] InnoDB: Creating shared tablespace for temporary tables
2022-09-18 21:06:11 0 [Note] InnoDB: Setting file './ibtmp1' size to 12 MB. Physically writing the file full; Please wait ... 
2022-09-18 21:06:11 0 [Note] InnoDB: File './ibtmp1' size is now 12 MB.
2022-09-18 21:06:11 0 [Note] InnoDB: 10.6.7 started; log sequence number 42479; transaction id 14
2022-09-18 21:06:11 0 [Note] InnoDB: Loading buffer pool(s) from /var/lib/mysql/ib_buffer_pool
2022-09-18 21:06:11 0 [Note] Plugin 'FEEDBACK' is disabled.
2022-09-18 21:06:11 0 [Note] InnoDB: Buffer pool(s) load completed at 220918 21:06:11
2022-09-18 21:06:11 0 [Warning] You need to use --log-bin to make --expire-logs-days or --binlog-expire-logs-seconds work.
2022-09-18 21:06:11 0 [Note] Server socket created on IP: '127.0.0.1'.
2022-09-18 21:06:11 0 [Note] /usr/sbin/mariadbd: ready for connections.
Version: '10.6.7-MariaDB-2ubuntu1.1' socket: '/run/mysql/mysql.sock' port: 3306 Ubuntu 22.04
```

Started MariaDB 10.6.7 database server.

A database system uses a storage engine to store the data on the disk. The storage engine has different features available, and the performance varies depending on the use case. *Table 11.3* shows the four more popular engines available for **MariaDB**:

Table 11.3: Engines and description list.

| Engine | Description |
| :--- | :--- |
| InnoDB | The default storage engine from **MariaDB 10.2**. For earlier releases, XtraDB was a performance-enhanced fork of InnoDB and is usually preferred. |
| XtraDB | The best option for **MariaDB 10.1** and earlier versions. |
| MyISAM | Oldest storage and the previous default one in the older version of **MySQL** and **MariaDB**. |
| Aria | An improved engine based on legacy **MyISAM**. |

The benefits of *InnoDB* are as follows:

- It is a transactional and well-suited for **Online Transactional Processing (OLTP)** workloads.
- It is **Atomicity, Consistency, Isolation**, and **Durability** (ACID) compliant.
- Performs well for mixed read-write workloads.
- Supports online Data Definition Language (DDL).

The **MariaDB server** package includes a tool to administrate the service named **mariadb-admin (mysqladmin)**. It can be used to:

- Monitor what **MariaDB** is doing.
- Get usage statistics and variables from the **MariaDB server**.
- Create and remove databases.
- Reset logs, statistics, and tables.
- Kill long-running queries.
- Stop the server.
- Reload the configuration.
- Start and stop secondary nodes (when high availability or replication is used).
- Check if the service is responding.

The syntax is `mariadb-admin action [arguments]`. Table 11.4 shows some of the popular actions available:

Table 11.4: Actions and description for command mariadb-admin (mysqladmin).

| Action | Description |
| :--- | :--- |
| create database_name | Create a new database |
| debug | Tell the server to write and debug information to log or journald. |
| drop database_name | Drop a database |
| extended-status | Return all status variables and their values |
| kill id | Kill a client thread |
| password newpw | Change the old password for the administrator to a new one. |
| ping | Check if the service is alive. |
| processlist | Show a list of active threads in the database server. |
| reload | Reload the privileges configuration. |
| refresh | Flush all tables and close and open the log files. |
| shutdown | Send a signal to the service to be stopped. |
| status | Gives a short status message from the server. |
| variables | Prints the variables available. |
| version | Returns version and the status from the server. |

Figures 11.11 to 11.15 show different examples of the usage of the command `mariadb-admin` with several commands, and the output is shown.

- The version and short status of the MariaDB server can be seen in figure 11.11:

```
root@ubuntu:~# mariadb-admin version
mariadb-admin Ver 9.1 Distrib 10.6.7-MariaDB, for debian-linux-gnu on x86_64
Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Server version		10.6.7-MariaDB-2ubuntu1.1
Protocol version		10
Connection		Localhost via UNIX socket
UNIX socket		/run/mysqld/mysqld.sock
Uptime:			44 min 30 sec

Threads: 1 Questions: 67 Slow queries: 0 Opens: 33 Open tables: 26 Queries:
per second avg: 0.025
```

![Figure 11.11](img/863afa537de4eed7deb11978bfbfa90e_344_0.png)

- A short status information about the server can be seen in figure 11.12:

```
root@ubuntu:~# mariadb-admin status
Uptime: 2786  Threads: 1  Questions: 68  Slow queries: 0  Opens: 33  Open tables: 26  Queries per second avg: 0.024
```

![Figure 11.12](img/863afa537de4eed7deb11978bfbfa90e_344_1.png)

- To check if the service is started, refer to figure 11.13:

```
root@ubuntu:~# mariadb-admin ping
mysqld is alive
```

![Figure 11.13](img/863afa537de4eed7deb11978bfbfa90e_344_2.png)

- To list the clients and the task performed, refer to figure 11.14:

```
root@ubuntu:~# mariadb-admin processlist
| Id | User  | Host    | db  | Command | Time | State     | Info                | Progress |
+----+-------+---------+-----+---------+------+------------+-----------------------+----------+
| 42 | root  | localhost |     | Query   | 0    | starting  | show processlist    | 0.000    |
```

![Figure 11.14](img/863afa537de4eed7deb11978bfbfa90e_344_3.png)

- To set a new password for the user root (by default is empty, only accessible from localhost), refer to figure 11.15:

```
root@ubuntu:~# mariadb-admin password Start123
```

![Figure 11.15](img/863afa537de4eed7deb11978bfbfa90e_344_4.png)

- To request the server to be stopped, refer to figure 11.16:

```
root@ubuntu:~# mariadb-admin shutdown
root@ubuntu:~# mariadb-admin ping
mariadb-admin: connect to server at 'localhost' failed
error: `Can't connect to local server through socket '/run/mysqld/mysqld.sock' (2)
Check that mariadb is running and that the socket: '/run/mysqld/mysqld.sock' exists'
```

![Figure 11.16](img/863afa537de4eed7deb11978bfbfa90e_344_5.png)

# MariaDB client and tasks

Client to access to **MariaDB server** is using part of the package **mariadb-client**. The command to access to the server is **mariadb** (or **mysql**), and Table 11.5 shows the common options available:
