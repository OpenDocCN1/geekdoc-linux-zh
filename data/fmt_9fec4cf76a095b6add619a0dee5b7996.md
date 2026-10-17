
以下示例显示了一个多行 MySQL 解释器语句，其中包含主解释器提示符（`*mysql>*`）和次要解释器提示符（*->*）。该语句显示名为 `people` 的表中符合指定标准的行中三个列的值。

```
mysql> SELECT person,password,executeperm
-> FROM people
-> WHERE password IS NULL AND executeperm=true;
```

### 先决条件

安装以下软件包：

- `mysql`
- `mysql-server`

运行 `chkconfig` 以在系统进入多用户模式时启动 MySQL 守护程序（`mysqld`）：

```
# /sbin/chkconfig mysqld on
```

`mysqld` 初始化脚本启动 `mysqld`：

```
# /sbin/service mysqld start
Initializing MySQL database: Installing MySQL system tables... OK
091208 11:23:00 [Warning] Forcing shutdown of 2 plugins OK
Filling help tables...
...
Starting MySQL:                    [ OK ]
```

## 注意事项

与 Oracle 不同，创建用户时，MySQL 不会自动创建数据库。在 MySQL 中，用户和数据库不像在 Oracle 中那样紧密结合。

MySQL 拥有一组独立于 Linux 用户的用户。安装后，MySQL 管理员的名称为 `root`。由于 MySQL 的 `root` 用户与 Linux 的 `root` 用户不同，因此可以拥有不同的密码。

### 快速入门：设置 MySQL

你必须为名为 `root` 的 MySQL 用户分配密码

> 除非你使用 `mysql_secure_installation` 为名为 `root` 的 MySQL 用户分配密码，否则本节中的示例将不起作用。请参阅以下说明。

MySQL 安装时带有测试数据库、匿名用户，并且名为 `root` 的 MySQL 用户没有密码。为了更安全的设置，请删除匿名用户并为 MySQL `root` 分配密码。`mysql_secure_installation` 工具会提出一系列问题，允许你为名为 `root` 的 MySQL 用户分配密码并执行其他维护任务。如果你刚刚安装 MySQL，请在当前 `root` 密码的提示符处输入 `RETURN`（回车）。

```
# /usr/bin/mysql_secure_installation
...
Enter current password for root (enter for none):
OK, successfully used password, moving on...
Set root password? [Y/n] y
New password: Re-enter new password:
Password updated successfully!
Reloading privilege tables...
... Success!
Remove anonymous users? [Y/n] y
...
Disallow root login remotely? [Y/n] y
...
Remove test database and access to it? [Y/n] y
...
Reload privilege tables now? [Y/n] y
...
```

或者，你可以使用以下命令将 `mysql-password` 设置为名为 *root* 的 MySQL 用户的密码：

```
# /usr/bin/mysqladmin -u root password 'mysql-password'
```

## 选项

本节描述你可以在 `mysql` 命令行中使用的一些选项。带单个连字符的选项和带双连字符的选项是等效的。

- `--disable-reconnect`
    - 如果连接中断，不尝试再次连接到服务器。参见 `--reconnect`。
- `--host=hostname -h hostname`
    - 指定 MySQL 服务器的地址为 *hostname*。没有此选项时，MySQL 连接到本地系统（127.0.0.1）上的服务器。
- `--password[=passwd] -p[passwd]`
    - 指定 MySQL 密码为 *passwd*。为了提高安全性，不要在命令行上指定密码；MySQL 将会提示输入。默认情况下，MySQL 不使用密码。在此选项的短形式中，不要在 `-p` 和 *passwd* 之间加空格。
- `--reconnect`
    - 如果连接中断，尝试再次连接到服务器（默认）。使用 `--disable-reconnect` 禁用此行为。
- `--user=usr -u usr`
    - 指定 MySQL 用户为 *usr*。首次安装 MySQL 时，有一个用户 *root*，且该用户没有密码。
- `--verbose -v`
    - 增加 MySQL 显示的信息量。多次使用此选项可进一步提高详细程度。

### `.my.cnf` 配置文件

你可以使用 `~/.my.cnf` 文件设置 MySQL 选项。以下示例显示了 Max 的 `.my.cnf` 文件。`[mysql]` 指定 MySQL 组。下一行将 Max 的密码设置为 *mysqlpassword*。在此设置下，Max 不需要在命令行上使用 `-p`；MySQL 会自动登录。

```
$ cat /home/max/.my.cnf
[mysql]
password="mysqlpassword"
```

## 使用 MYSQL

### 添加用户

在开始使用数据库之前，请创建一个用户，以便你无需使用 MySQL root 用户进行操作。如果你添加的 MySQL 用户名与你的 Linux 用户名相同，那么在 MySQL 命令行中就不需要指定用户名。在以下示例中，Max 以 MySQL root（`-u root`）用户身份工作，创建一个名为 `maxdb` 的数据库，并添加一个名为 `max`、密码为 `mpassword` 的 MySQL 用户。`GRANT` 语句授予了 Max 操作 `maxdb` 数据库所需的权限。你必须以 MySQL root 用户身份来设置 MySQL 用户。`-p` 选项会使 MySQL 提示输入密码。当使用 MySQL 解释器时，Query OK 表示前面的语句在语法上是正确的。所有字符和日期数据都必须用单引号括起来。

```text
$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 12
Server version:  5.1.40 Source distribution

Type 'help;' or '\h' for help.  Type '\c' to clear the current input
statement.

mysql> CREATE DATABASE maxdb;
Query OK, 1 row affected (0.00 sec)

mysql> GRANT ALL PRIVILEGES
    -> ON maxdb.* to 'max'
    -> IDENTIFIED BY 'mpasswd'
    -> WITH GRANT OPTION;
Query OK, 0 rows affected (0.00 sec)

mysql> SELECT user, password
    -> FROM mysql.user;
+------+--------------------------------+
| user | password                       |
+------+--------------------------------+
| root | 4927a5e40a2cca3e             |
| max  | 0eb28ca55c1ee9fe             |
+------+--------------------------------+
2 rows in set (0.00 sec)

mysql> quit
Bye
$ 
```

在上面的示例中，创建数据库并设置新用户后，Max 查询 `mysql` 数据库的 `user` 表以显示 `user` 和 `password` 列。现在存在两个用户：`root` 和 `max`。Max 输入 `quit` 命令以退出 MySQL 解释器。
