
3306/tcp open mysql syn-ack MySQL 5.0.51-24+lenny2

`mysql-info`:

`Protocol`: 10

`Version`: 5.0.51-24+lenny2

`Thread ID`: 38

`Capabilities flags`: 43564

`Some Capabilities`: Support4Auth, SupportsTransactions, Speaks41ProtocolNew, LongColumn SwitchToSSLHandshake, ConnectWithDatabase, SupportsCompression

`Status`: Autocommit

`Salt`: `@((nTOV)>RGIwde--)=G`

在这里你可以在 `mysql-info.nse` Nmap 脚本下 MySQL 特有的信息。该服务似乎在使用第 10 版本的 MySQL 协议，这与软件版本不同。软件版本为 5.0.51-24+lenny2，这还告诉你该主机的底层操作系统是 Debian。（Linux 是 Debian 5 的代号）。在该块信息中，你可以看到 `Salt: @((nTOV)>RGIwde--)=G`，这是一个用于哈希的伪名字符串。每次连接到数据库时 Salt 都会不同。还有其他信息告诉该服务支持什么，例如使用 SSL 加密。你可以使用 Netcat 收集其中的一些信息。使用 Netcat 连接 TCP 端口 3306 的结果。你可以看到 Nmap 报告的相同版本，紧接着是一个新的 `Salt` 值。

```
?
5.0.51-24+lenny2*ets$8-?-1[CUGVI/I
```

你应该尝试使用 MySQL 客户端连接到 MySQL 数据库。你通常需要在 Linux 发行版上安装一个（尽管 Kali 已经包含了它）。你可以使用 `mysql -h <TargetIP>` 命令连接到 MySQL 服务，它将尝试以你当前在本地登录的相同身份登录数据库。换句话说，如果你在 Kali Linux 虚拟机中以 root 用户运行此命令，它将尝试以 root 身份登录且无需密码。这通常会向你显示类似下面的消息：

```
ERROR 1045 (28000): Access denied for user 'root'@'192.168.56.1' (using password: NO)
```

要为用户提供密码，你将指示 MySQL 提示输入密码（或在命令行中提供，但这不是推荐的做法，因为会将密码暴露给他人）。要提供密码，使用 `-p` 选项。系统将提示你输入密码，如下：

```
Enter password:
ERROR 1045 (28000): Access denied for user 'root'@'192.168.56.1' (using password: YES)
```

MySQL root 账户通常未配置为在提供过多错误密码后自动锁定，因此可以被暴力破解。你可能不知道账户是否已锁定，或者它可能会显示错误，所以作为为客户工作，你将希望将这种方法作为任何暴力破解攻击。如果你针对的是客户生产环境部分的数据库，并且你禁用了该账户（无论无意还是故意），那么这可能被视为拒绝服务攻击的形式，应该尽可能避免。（在这种情况下，诚恳道歉无疑是恰当的。如果你的客户密切关注他们的内部网络，那么他们可能在你准备道歉之前就联系你了！）

记住，要谨慎使用此类方法，并在影响有限的情况下使用。对 MySQL 数据库的 root 用户进行暴力破解可能会导致账户被禁用。但在禁用时，数据库会通知你它已被禁用，这使得黑客检测该状态变得困难。

你可以使用密码 `sneaky` 以 root 用户登录书中的 MySQL 数据库。登录成功后，你会看到类似下面的提示：

```
Welcome to the MySQL monitor. Commands end with ; or g.
Your connection id is 47
Server version: 5.0.51a-24+lenny2 (Debian)
```

Copyright (c) 2000, 2019, Oracle and/or its affiliates. All rights reserved.

# 第 11 章 数据库 365

Oracle 是 Oracle 公司和/或其关联公司的注册商标。其他名称可能是其各自所有者的商标。

输入 'help'; 或 '\h' 获取帮助。输入 '\c' 清除当前语句。

```
mysql>
```

每当你输入一个 SQL 语句时，请确保用分号 (`;`) 结束语句。这不是 MySQL 客户端程序的特殊之处，而是 SQL 语言的一个基本特征。如果你不可避免地忘记正确结束语句，你会看到一个新行让你继续。只需输入分号并按回车。最终，你会习惯这种行为。一旦登录 MySQL 数据库，你会发现服务器上有多个数据库。要开始，使用 `show databases;` 命令，用分号结束。

```
mysql> show databases;
+----------------------+
| Database             |
| information_schema   |
| merchant             |
| mysql                |
+----------------------+
3 rows in set (0.00 sec)
```

在前面的示例中，你看到了三个数据库。其中两个是系统创建的。有时，你会访问一个 MySQL 实例但对其结构一无所知。在这些对数据访问有限的情况下，你需要先了解数据库的结构。你可以通过查询 MySQL 的系统数据库来实现——特别是 `information_schema`，它包含了前面讨论的数据库架构。一旦你发现了表名和这些表的列数，就可以开始提取有意义且潜在敏感的信息。

使用 `mysql` 选择并开始与 `mysql` 数据库交互。你会看到类似这样的短消息：

```
Database changed
```

你可以使用 `show tables;` 命令显示当前选择数据库中的表，结果如下：

```
mysql> show tables;
+----------------------------------------------------------------+
| Tables_in_mysql                                                |
+----------------------------------------------------------------+
| columns_priv                                                   |
| db                                                             |
| event                                                          |
| func                                                           |
| general_log                                                    |
| help_category                                                  |
| help_keyword                                                   |
| help_relation                                                  |
| help_topic                                                     |
| host                                                           |
| ndb_binlog_index                                               |
| plugin                                                         |
| proc                                                           |
| procs_priv                                                     |
| servers                                                        |
| slow_log                                                       |
| tables_priv                                                    |
| time_zone                                                      |
| time_zone_leap_second                                          |
| time_zone_name                                                 |
| time_transition                                                |
| time_transition_type                                           |
| user                                                           |
+----------------------------------------------------------------+
23 rows in set (0.00 sec)
```
