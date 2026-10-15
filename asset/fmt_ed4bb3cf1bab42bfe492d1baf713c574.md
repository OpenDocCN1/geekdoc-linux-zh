
在安装 `MySQL` 期间，安装脚本会自动为你创建一个初始数据库。你还将有一个 `init.d` 脚本（通常在 `/etc/rc.d/init` 中），名为 `mysqld` 或 `mysql`，用于启动和停止服务器。通常，在发行版中找到数据库文件最简单的方法是在你的 `init.d` 目录中找到此脚本并查看。标准路径和定义位于脚本开头附近，很容易看到文件所处的位置。对于我们的 Red Hat RPM 二进制安装，数据目录被设置为 `/var/lib/mysql`。

安装后，你可以作为 `root` 身份使用 `/etc/rc.d/init/mysql start`（或你发行版的对应命令）手动启动服务器，或者使用指向 `/etc/rc.d/init/` 中脚本的符号链接，以确保 `mysql` 在运行级别 3 和 5 中自动启动，并在运行级别 0、1 和 6 中启动：

```bash
# ln -s /etc/rc.d/init/mysql /etc/rc.d/rc0/K97mysql
# ln -s /etc/rc.d/init/mysql /etc/rc.d/rc1/K97mysql
# ln -s /etc/rc.d/init/mysql /etc/rc.d/rc6/K97mysql
# ln -s /etc/rc.d/init/mysql /etc/rc.d/rc3/S97mysql
# ln -s /etc/rc.d/init/mysql /etc/rc.d/rc5/S97mysql
```

你可能希望使用你的系统调整准确数字以保持其唯一性，尽管这并非必须。

你可能正在使用一个具有 `ckconfig` 命令的系统，它提供了一种更简单的方法来设置服务运行的级别。例如，要将 `MySQL` 服务器设置为在级别 3 和 4 运行，你必须首先将 `mysql` 添加为 `ckconfig` 管理的服务，如下所示：

```bash
ckconfig -add mysql
```

现在我们将服务在级别 3 和 5 中设置为“开启”：

```bash
ckconfig -level 35 mysql on
```

并在其他级别中设置为“关闭”：

```bash
ckconfig -level 01246 mysql off
```

为了确认你的配置已正确更改，我们可以如下列出服务将运行的运行级别：

```bash
# ckconfig -list mysql
mysql 0:off 1:off 2:off 3:on 4:off 5:on 6:off
```

> 如果你有 `ckconfig`，我们建议你使用这种方法而不是创建符号链接，因为这种方法不容易出错。

在安装 `MySQL` 期间，安装脚本会自动为你创建一个初始数据库。你还会有一个 `init.d` 脚本（通常在 `/etc/rc.d/init`），名为 `mysqld` 或 `mysql`，用于启动和停止服务器。通常，在发行版中找到数据库文件最简单的方法是在你的 `init.d` 目录中找到此脚本并查看。标准路径和定义位于脚本开头附近，很容易看到文件所处的位置。对于我们的 Red Hat RPM 二进制安装，数据目录被设置为 `/var/lib/mysql`。

安装后，你可以作为 `root` 身份使用 `/etc/rc.d/init/mysql start`（或你发行版的对应命令）手动启动服务器，或者使用指向 `/etc/rc.d/init/` 中脚本的符号链接，以确保 `mysql` 在运行级别 3 和 5 中自动启动，并在运行级别 0、1 和 6 中启动：

```bash
# ln -s /etc/rc.d/init/mysql /etc/rc.d/rc0/K97mysql
# ln -s /etc/rc.d/init/mysql /etc/rc.d/rc1/K97mysql
# ln -s /etc/rc.d/init/mysql /etc/rc.d/rc6/K97mysql
# ln -s /etc/rc.d/init/mysql /etc/rc.d/rc3/S97mysql
# ln -s /etc/rc.d/init/mysql /etc/rc.d/rc5/S97mysql
```

你可能希望使用你的系统调整准确数字以保持其唯一性，尽管这并非必须。

你可能正在使用一个具有 `ckconfig` 命令的系统，它提供了一种更简单的方法来设置服务运行的级别。例如，要将 `MySQL` 服务器设置为在级别 3 和 4 运行，你必须首先将 `mysql` 添加为 `ckconfig` 管理的服务，如下所示：

```bash
ckconfig -add mysql
```

现在我们将服务在级别 3 和 5 中设置为“开启”：

```bash
ckconfig -level 35 mysql on
```

并在其他级别中设置为“关闭”：

```bash
ckconfig -level 01246 mysql off
```

为了确认你的配置已正确更改，我们可以如下列出服务将运行的运行级别：

```bash
# ckconfig -list mysql
mysql 0:off 1:off 2:off 3:on 4:off 5:on 6:off
```

> 如果你有 `ckconfig`，我们建议你使用这种方法而不是创建符号链接，因为这种方法不容易出错。

在安装 `MySQL` 期间，安装脚本会自动为你创建一个初始数据库。你还会有一个 `init.d` 脚本（通常在 `/etc/rc.d/init`），名为 `mysqld` 或 `mysql`，用于启动和停止服务器。通常，在发行版中找到数据库文件最简单的方法是在你的 `init.d` 目录中找到此脚本并查看。标准路径和定义位于脚本开头附近，很容易看到文件所处的位置。对于我们的 Red Hat RPM 二进制安装，数据目录被设置为 `/var/lib/mysql`。

安装后，你可以作为 `root` 身份使用 `/etc/rc.d/init/mysql start`（或你发行版的对应命令）手动启动服务器，或者使用指向 `/etc/rc.d/init/` 中脚本的符号链接，以确保 `mysql` 在运行级别 3 和 5 中自动启动，并在运行级别 0、1 和 6 中启动：

```bash
# ln -s /etc/rc.d/init/mysql /etc/rc.d/rc0/K97mysql
# ln -s /etc/rc.d/init/mysql /etc/rc.d/rc1/K97mysql
# ln -s /etc/rc.d/init/mysql /etc/rc.d/rc6/K97mysql
# ln -s /etc/rc.d/init/mysql /etc/rc.d/rc3/S97mysql
# ln -s /etc/rc.d/init/mysql /etc/rc.d/rc5/S97mysql
```

## 安装后配置

假设一切顺利，`MySQL` 现在已安装。测试一下：

```bash
$ mysql -u root
```

如果你收到“Welcome to the MySQL monitor”消息，说明服务器已启动。一旦你启动了用户，我们可以收紧权限，只允许应用程序功能所必需的用户和权限。`MySQL` `root` 与系统 `root` 或超级用户之间没有关系。`MySQL` 安装不受系统密码保护。任何账户的用户都可以登录。有很多方法可以设置 `root` 密码，最简单的是使用：

```bash
$ mysqladmin -u root password
```

这将设置初始密码为 `newpassword`。然而，这种方法存在问题，明文将留在 shell 历史中，并在命令执行时可能被使用 `ps` 命令的人看到。一种更好的方法是再次使用 `MySQL` 监视器，发送某些更改密码的 SQL 命令。

```bash
$ mysql -u root
Welcome to the MySQL monitor. Commands end with; \
Your MySQL connection id is 4

Type 'help'; or '\h' for help. Type '\c' to clear the buffer.

mysql> SET password='secretpassword';
Query OK, 0 rows affected (0.15 sec)
```

选择只有你知道的密码，我们之前用于显示用户密码的示例“`secretpassword`”需要设置。现在让我们查看权限表以验证密码已设置：

```sql
mysql> SELECT user, host, password FROM mysql.user;
+------------------------------------------+
| user | host      | password             |
+------------------------------------------+
| root | localhost | 2dxf8ec23age6ed |
| root | gwl       |                       |
|      | localhost |                       |
|      | gwi        |                       |
+------------------------------------------+
4 rows in set (0.07 sec)

mysql>
```

# 第 8 章

请注意，我们仅在从 `localhost` 连接时才为 `root` 创建了密码。`MySQL` 不仅可以存储针对用户的权限，还可以存储基于主机名的连接类的权限。此外，请注意我们使用分号（`;`）来结束 SQL 命令。从严格意义上说，这并不是实际 SQL 命令的一部分；它用于告诉 `MySQL` 客户端程序我们已经准备好执行 SQL 语句了。

加固安装的下一步是删除 `MySQL` 默认安装的那些不必要的用户。以下命令将从权限表中所有非 `root` 用户：

```mysql
mysql> DELETE FROM mysql.user WHERE user != 'root';
Query OK, 2 rows affected (0.11 sec)
```

下一条命令删除除了来自 `localhost` 以外的任何主机的登录权限：

```mysql
mysql> DELETE FROM mysql.user WHERE host != 'localhost';
Query OK, 1 row affected (0.06 sec)
```

最后，使用以下命令检查是否有遗留的登录：

```mysql
mysql> SELECT user, host, password FROM mysql.user;
+------------------------------------------+
| user | host | password |
+------------------------------------------+
| root | localhost | 2df8e9c23age66ed |
+------------------------------------------+
1 row in set (0.11 sec)
mysql> exit
```

如你从前面的输出所示，我们现在只有一个只能从 `localhost` 连接的登录账户。

现在是见真章的时刻了：我们还能使用设置的密码登录吗？注意，这次我们提供了 `-p` 参数，它告诉 `MySQL` 必须提示输入密码：

```bash
$ mysql -u root -pn
Enter password:
Welcome to the MySQL monitor. Commands end with or \g.
Your MySQL connection id is =
Type 'help'; or '\h' for help. Type '\c' to clear the buffer.
mysql>
```

我们现在拥有了一个运行中的 `MySQL` 版本，它已被锁定，只有使用我们设置的密码的 `root` 用户才能连接到数据库服务器，且 `root` 用户只能从本地机器连接。

我们的下一步是添加回我们需要的一个或多个用户。与 Linux 系统一样，除非绝对必要，否则使用 `root` 账户登录 `MySQL` 并不是一个好主意，所以你应该为日常使用创建一个普通用户。

# MySQL

正如我们之前暗示的，我们可以创建具有从不同机器不同连接权限的用户；特别是，出于安全考虑，我们允许 `root` 用户仅从本地机器连接。为了本章的目的，我们将创建一个新用户 `rick`，他拥有相当广泛的权限。`rick` 将能够通过不同的方式进行连接：

- 他可以从本地主机连接。
- 他可以从 IP 地址范围在 `192.168.0.0` ↔ `192.168.0.255` 之间的任何机器连接。
- 他可以从 `wiley.com` 域内的任何机器连接。

以安全方式实现此点的最方法是创建具有三个不同连接来源的三个不同用户。如果我们愿意，甚至可以根据他们连接的位置设置三个不同的密码。

我们通过 `grant` 命令创建用户并分配权限。在这里，我们创建了上述列出的三个不同连接来源的用户。`IDENTIFIED BY` 是设置密码的一种略显奇怪的语法。注意引号的使用方式；必须精确使用所示的单引号字符，否则我们无法完全按照意图创建用户。

以 `root` 身份连接到 `MySQL`，然后执行以下序列操作：

1. 为 `rick` 创建本地登录账户：

```mysql
grant ALL ON *.* TO rick@localhost IDENTIFIED BY 'secretpassword';
Query OK, 0 rows affected (0.33 sec)
```

2. 然后我们创建一个来自 `192.168.0.0` C 类子网任何位置的登录。注意我们必须使用单引号包裹 IP 范围：

```mysql
grant ALL ON *.* TO rick@'192.168.0.0/255.255.255' IDENTIFIED BY 'secretpassword';
Query OK, 0 rows affected (0.00 sec)
```

3. 最后，我们创建一个登录账户，让 `rick` 可以从 `wiley.com` 域内的任何机器连接：

```mysql
grant ALL ON *.* TO rick@'%.wiley.com' IDENTIFIED BY 'secretpassword';
Query OK, 0 rows affected (0.00 sec)
```

我们现在可以查看表来检查条目：

| user | host | password |
| :--- | :--- | :--- |
| `root` | `localhost` | `2dxf8e8c7cade6` |
| `rick` | `localhost` | `3742g6348q837d9` |
| `rick` | `%.wiley.com` | `3742g6348q837d9` |
| `rick` | `192.168.0.0/255.255.255.050` | `3742g6348q837d9` |

```mysql
mysql> SELECT user, host, password FROM mysql.user;
4 rows in set (0.06 sec)
mysql>
```

自然，你需要根据你的本地配置调整上述命令和密码。你会发现 [后续文本将根据提供的 OCR 片段的逻辑继续]。

## 第 8 章

| 命令 | 替代简写 | 含义 |
|---|---|---|
| `help` `?` | `\h` 或 `\?` | 显示命令列表。 |
| `edit` | `\e` | 编辑命令。使用的编辑器由环境变量 `$EDITOR` 决定。 |
| `exit` or `quit` | `\q` | 退出 `MySQL` 客户端。 |
| `go` | `\g` | 执行命令。 |
| `source <filename>` | `\.` | 从给定的文件执行 SQL。 |
| `status` | `\s` | 显示服务器状态信息。 |
| `system <command>` | `\!` | 执行系统命令。 |
| `tee <filename>` | `\T` | 将所有输出复制追加到指定的指定。 |
| `use <database>` | `\u` | 使用指定的数据库。 |

`SQL92` 是目前使用的 ANSI 标准版本。它的目的是为 SQL 数据库的工作方式建立统一性，便于不同数据库产品之间的互操作性和通信。

## mysqladmin

该工具是快速进行 `MySQL` 数据库管理工具。除了常规参数外，还支持以下命令：

| 命令 | 含义 |
|---|---|
| `create <database_name>` | 创建新数据库。 |
| `drop <database_name>` | 删除数据库。 |
| `password <new_password>` | 更改密码（如我们之前看到的）。 |
| `reload` | 重新加载控制权限的权限表。 |
| `status` | 提供服务器状态。 |
| `shutdown` | 关闭服务器。 |
| `variables` | 显示控制 `MySQL` 操作的变量及其当前值。 |
| `version` | 提供服务器版本号及其运行时间。 |

在命令行提示符中不带任何参数调用 `mysqladmin`，可以查看完整的选项列表。你可能需要配合 `less` 命令使用。

## MySQL

如果运气足够好，你永远不会有机会使用它。顾如其名，此工具会创建一个错误报告，并发送给 `MySQL` 的维护者。在发送之前，你可能希望编辑生成的文件，以提供对开发者可能有用的额外信息。

这是一个非常有用的实用程序，允许你将部分或整个数据库导出为一组 SQL 命令，这些命令可以重新读入 `MySQL` 甚至另一个 SQL RDBMS 中。它接受标准用户和密码信息以及数据库和表名作为参数。下表中的附加选项极大扩展了它的实用性：

| `-add-drop-table` | 在输出文件中添加 SQL 命令，在创建表的命令之前删除（移除）任何表。 |
| `-e` | 使用扩展插入语法。这是非标准 SQL，但如果你正在导出大量数据，这将有助于你的数据库转储在尝试将其读入 `MySQL` 时重载得更快。 |
