
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

![图 11.11](img/863afa537de4eed7deb11978bfbfa90e_344_0.png)

- 图 11.12 中可以看到关于服务器的简短状态信息：

```
root@ubuntu:~# mariadb-admin status
Uptime: 2786  Threads: 1  Questions: 68  Slow queries: 0  Opens: 33  Open tables: 26  Queries per second avg: 0.024
```

![图 11.12](img/863afa537de4eed7deb11978bfbfa90e_344_1.png)

- 若要检查服务是否已启动，请参阅图 11.13：

```
root@ubuntu:~# mariadb-admin ping
mysqld is alive
```

![图 11.13](img/863afa537de4eed7deb11978bfbfa90e_344_2.png)

- 若要列出客户端及其执行的任务，请参阅图 11.14：

```
root@ubuntu:~# mariadb-admin processlist
| Id | User  | Host    | db  | Command | Time | State     | Info                | Progress |
+----+-------+---------+-----+---------+------+------------+-----------------------+----------+
| 42 | root  | localhost |     | Query   | 0    | starting  | show processlist    | 0.000    |
```

![图 11.14](img/863afa537de4eed7deb11978bfbfa90e_344_3.png)

- 若要为用户 `root` 设置新密码（默认为空，仅可从本地主机访问），请参阅图 11.15：

```
root@ubuntu:~# mariadb-admin password Start123
```

![图 11.15](img/863afa537de4eed7deb11978bfbfa90e_344_4.png)

- 若要请求停止服务器，请参阅图 11.16：

```
root@ubuntu:~# mariadb-admin shutdown
root@ubuntu:~# mariadb-admin ping
mariadb-admin: connect to server at 'localhost' failed
error: `Can't connect to local server through socket '/run/mysqld/mysqld.sock' (2)
Check that mariadb is running and that the socket: '/run/mysqld/mysqld.sock' exists'
```

![图 11.16](img/863afa537de4eed7deb11978bfbfa90e_344_5.png)

### MariaDB 客户端和任务

访问 `MariaDB` 服务器的客户端使用 `mariadb-client` 包的一部分。访问服务器的命令是 `mariadb`（或 `mysql`），表 11.5 展示了常用选项：

| 选项 | 描述 |
| :--- | :--- |
| `-e`, `-execute=name` | 执行语句并退出。 |
| `-h`, `-host=name` | 连接到指定的主机，而不是使用 `Unix Socket`。 |
| `--max-allowed-packet=num` | 发送到服务器或从服务器接收的最大数据包长度。默认值为 `16 MB`，最大值为 `1 GB`。在导入大文件时使用此选项非常有用。 |
| `-p`, `-password[=name]` | 连接服务器时使用的密码。 |
| `-P`, `-port=num` | 用于连接端口，替代默认的 `3306`。 |
| `--print-defaults` | 输出客户端选项列表。 |
| `-u`, `-user=name` | 如果登录用户不是当前用户，则指定登录用户名。 |
| `-v`, `-verbose` | 显示更多信息。 |
| `-V`, `-version` | 输出版本信息并退出。 |

表 11.5：`mariadb` (`mysql`) 命令的常用选项

客户端可以以两种不同的模式工作：

-   **交互模式：** 连接到数据库服务器后，用户可以编写多条语句来操作服务器，并通过编写 `QUIT` 命令来退出客户端。
-   **一次性模式：** 客户端从标准输入读取一条或多条语句，将它们发送到服务器执行，然后退出客户端执行。

客户端允许指定一个参数来指定要使用的数据库。如果未指定，则与服务器的连接将不使用数据库，用户需要手动（使用 `USE` 语句）指定要操作的数据库。用户可以在数据库之间切换。

图 11.17 显示了以 `root` 用户身份从数据库服务器运行客户端是不必要的，并且也不需要提供用户名和密码。

```
root@ubuntu:~# mariadb
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 31
Server version: 10.6.7-MariaDB-2ubuntu.1 Ubuntu 22.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
```

> 图 11.17：命令 `mariadb` 的输出示例

`MariaDB`（和 `MySQL`）允许使用 `CREATE USER` 语句创建用户。其简单语法如下：

```
CREATE [OR REPLACE] USER user_specification [authentication_options]
```

图 11.18 展示了如何创建名为 `agonzalez` 的用户，密码为 `P@ssw0rd`。

该用户将仅从 IP `192.168.122.226` 通过该密码访问。

```
MariaDB [(none)]> CREATE USER agonzalez@192.168.122.226 IDENTIFIED BY 'P@ssw0rd';
Query OK, 0 rows affected (0.007 sec)
```

> 图 11.18：在 `MariaDB` 上创建用户的示例

客户端可以使用指定的认证参数并从允许的主机进行连接。可以指定字符 `%` 以接受来自所有源 IP 地址的连接。图 11.19 显示了从远程系统连接到数据库的示例：

```
[agonzalez@rhel ~]$ mysql -uagonzalez -pP@ssw0rd -h192.168.122.43
Welcome to the MariaDB monitor. Commands end with ; or \g.
Your MariaDB connection id is 31
Server version: 10.6.7-MariaDB-2ubuntu1.1 Ubuntu 22.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
```
