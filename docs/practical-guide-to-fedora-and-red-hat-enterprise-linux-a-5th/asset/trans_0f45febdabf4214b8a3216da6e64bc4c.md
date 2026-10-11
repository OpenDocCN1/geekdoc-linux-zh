

仅由一个设施（facility）和优先级（priority）组成的选择器，例如 `kern.info`，会使相应的操作应用于来自该设施且具有该优先级**或更高**（更紧急）的每条消息。使用 `:` 来指定单一优先级；例如，`kern:=info` 将操作应用于具有 **info** 优先级的内核消息。感叹号指定不匹配某个优先级，因此 `kern.!:info` 匹配优先级低于 **info** 的内核消息，而 `kern.:=!info` 匹配优先级不为 **info** 的内核消息。

一行中包含多个选择器（以分号分隔），如果其中任何选择器匹配，则应用该操作。在包含多个选择器的一行中，每个选择器都会约束匹配条件，后续选择器通常会进一步收紧这些约束。例如，选择器 `mail.info;mail.!err` 匹配具有 **info**、**notice** 或 **warning** 优先级的邮件子系统消息。

你可以用星号替换选择器的任何部分以匹配任意内容。选择器的任何部分中使用关键字 `none` 表示不可能匹配。选择器 `*.!crit;kern.none` 匹配所有关键级别（critical）或更高优先级的消息，但不包括来自内核的消息。

**操作** 操作指定了 `rsyslogd` 如何处理匹配选择器的消息。最简单的操作是普通文件，通过其绝对路径名指定；`rsyslogd` 会将消息追加到这些文件中。如果你希望将消息发送到系统控制台，请指定 `/dev/console`。如果你需要消息的硬拷贝记录，可以指定代表专用打印机的设备文件。

你可以通过指定用户名（例如 `root`）或逗号分隔的用户名列表，将重要消息写入特定用户的终端。使用星号可以将非常重要的消息写入所有已登录的终端。

要将消息转发到远程系统上的 `rsyslog`，请在系统名称前加上 @ 符号。将内核的关键消息转发到另一个系统是个好主意，因为这些消息通常出现在系统崩溃之前，可能未被保存到本地磁盘。`syslog.conf` 中的以下行将关键内核消息发送到 `grape`：

```
kern.crit            @grape
```

由于 `rsyslogd` 默认未配置为启用网络日志记录，你必须编辑远程系统上的 `/etc/sysconfig/rsyslog` 文件（在本例中为 **grape**），以便 `rsyslogd` 使用 `-r` 选项启动。修改 `rsyslog` 文件后，使用 `rsyslog` 初始化脚本重启 `rsyslogd`。

## MySQL

MySQL（My Structured Query Language）是全球最流行的开源数据库。它是 LAMP（Linux, Apache, MySQL, PHP/Perl/Python，一个开源企业软件栈）中的 M。许多编程语言提供了与 MySQL 的接口（例如，C、PHP、Perl）。

Michael Widenius 和 David Axmark 于 1994 年开始开发 MySQL。如今，MySQL 数据库由 Sun Microsystems 拥有和支持（截至 2009 年，Oracle Corporation 已开始收购 Sun Microsystems 的流程）。

**本节解释如何设置和使用 MySQL；它不解释 SQL。**

> SQL（结构化查询语言）是用于处理包括 MySQL 在内的 SQL 数据库的语言。本章解释如何在 Fedora/RHEL 环境中安装和设置 MySQL。尽管该说明包含一些 SQL 语句，但不尝试解释 SQL。请参阅 dev.mysql.com/doc 获取 SQL 文档。

### 更多信息

- 主页：www.mysql.com
- MySQL 文档：dev.mysql.com/doc
- 简介：dev.mysql.com/tech-resources/articles/mysql_intro.html
- 备份数据库：www.webcheatsheet.com/SQL/mysql_backup_restore.php

### 术语

本节简要介绍使用关系型数据库时的一些基本术语。另见第 589 页的图 16-4。

- **database**（数据库）：由一个或多个表组成的持久数据结构集合。
- **table**（表）：关系数据库中的一组行。
- **row**（行）：表中一列的有序集合。也称 *record*（记录）。
- **column**（列）：表中每行一个值的同一类型值的集合。也称 *field*（字段）。

### 语法和约定

MySQL 程序由一个或多个语句组成，每个语句以分号（;）结尾。虽然语句中的关键字不区分大小写，但本书为了清晰起见，将关键字显示为大写字母。数据库和表名称区分大小写。

以下示例显示了一个多行 MySQL 解释器语句，其中包含主解释器提示符（*mysql>*）和次要解释器提示符（*->*）。该语句显示名为 people 的表中符合指定标准的行中三个列的值。

```
mysql> SELECT person,password,executeperm
-> FROM people
-> WHERE password IS NULL AND executeperm=true;
```

### 先决条件

安装以下软件包：

- mysql
- mysql-server

运行 chkconfig 以在系统进入多用户模式时启动 MySQL 守护程序（**mysqld**）：

```
# /sbin/chkconfig mysqld on
```

**mysqld 初始化脚本** 启动 **mysqld**：

```
# /sbin/service mysqld start
Initializing MySQL database: Installing MySQL system tables... OK
091208 11:23:00 [Warning] Forcing shutdown of 2 plugins OK
Filling help tables...
...
Starting MySQL:                    [ OK ]
```

### 注意事项

与 Oracle 不同，创建用户时，MySQL 不会自动创建数据库。在 MySQL 中，用户和数据库不像在 Oracle 中那样紧密结合。

MySQL 拥有一组独立于 Linux 用户的用户。安装后，MySQL 管理员的名称为 **root**。由于 MySQL 的 **root** 用户与 Linux 的 **root** 用户不同，因此可以拥有不同的密码。

### 快速入门：设置 MySQL

**你必须为名为 root 的 MySQL 用户分配密码**

> 除非你使用 **mysql_secure_installation** 为名为 **root** 的 MySQL 用户分配密码，否则本节中的示例将不起作用。请参阅以下说明。

MySQL 安装时带有测试数据库、匿名用户，并且名为 **root** 的 MySQL 用户没有密码。为了更安全的设置，请删除匿名用户并为 MySQL **root** 分配密码。**mysql_secure_installation** 工具会提出一系列问题，允许你为名为 **root** 的 MySQL 用户分配密码并执行其他维护任务。如果你刚刚安装 MySQL，请在当前 **root** 密码的提示符处输入 **RETURN**（回车）。

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

### 选项

本节描述你可以在 `mysql` 命令行中使用的一些选项。带单个连字符的选项和带双连字符的选项是等效的。

- `--disable-reconnect`
    - 如果连接中断，不尝试再次连接到服务器。参见 `--reconnect`。
- `--host=hostname -h hostname`
    - 指定 MySQL 服务器的地址为 *hostname*。没有此选项时，MySQL 连接到本地系统（127.0.0.1）上的服务器。
- `--password[=passwd] -p[passwd]`
    - 指定 MySQL 密码为 *passwd*。为了提高安全性，不要在命令行上指定密码；MySQL 将会提示输入。默认情况下，MySQL 不使用密码。在此选项的短形式中，不要在 -p 和 *passwd* 之间加空格。
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

