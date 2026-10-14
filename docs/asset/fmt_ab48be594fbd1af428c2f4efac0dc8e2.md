
# 第 29 章 管理关系型数据库服务

为了防止数据损坏，数据库在访问数据时需要对其加锁。只要锁在，其他进程就无法访问数据。这意味着任何尝试访问数据的进程都必须等待当前进程完成。下一个在队列中的进程锁定数据直到它完成。当然，由于操作通常很快，锁的持续时间不会导致严重延迟。

旧版本的 MySQL 在表级进行锁定，这在高活动期间可能成为瓶颈。当某人写入行数据时，整个表会被锁定，其他人无法进入数据。如果你的表有 500,000 行（或记录），当访问其中一行时，所有 500,000 行都会被锁定。再次，在用户相对较少环境中，这不会引起严重的性能问题。

相比之下，PostgreSQL 在行级锁定。在 PostgreSQL 中，只有被访问的行被锁定。其他用户可以访问表的其余部分。这种行级锁定显著减少了高负载环境下的锁定影响。

Ubuntu 自带的 MySQL 版本允许选择使用表级或行级锁定。在 MySQL 术语中，MyISAM 表使用表级锁定，InnoDB 表使用行级锁定。

> **注意：**
> MySQL 数据锁定方法在 `www.mysql.com/doc/en/Internal_locking.html` 有更深入的讨论。

关于 PostgreSQL 锁定更多信息可以在 `www.postgresql.org/docs/9.1/static/sql-lock.html` 。

## 事务处理中的 ACID 遵循以保护数据完整性

MySQL 和 PostgreSQL 的另一个不同之处在于它们在防止数据损坏方面提供的保护程度。ACID 缩写通常描述数据保护的几个方面：

- 原子性——这意味着多个数据库操作被视为一个不可分割的（原子的）单元，通常称为事务。在事务中，要么所有单元操作要么全部执行，要么全不执行。换句话说，如果原子单元中的任何操作失败，整个原子单元都将取消。
- **一致性（Consistency）**——确保任何事务都不会导致数据库处于不一致状态。不一致状态可能由数据库客户端崩溃、网络故障和类似情况引起。一致性确保在这种情况下，任何可能导致数据库处于不一致状态的事务或部分完成的事务都会被回滚或撤销。
- **隔离性（Isolation）**——确保在相同数据上操作的多个事务彼此完全隔离。这防止了当两个用户同时尝试向同一记录写入数据时产生损坏。隔离性的处理方式通常可以由数据库程序员进行配置。处理隔离性的一种方法是之前之前讨论的锁机制。
- **持久性（Durability）**——确保在事务提交到数据库后，即使发生系统崩溃、网络故障或其他问题，该事务也不会丢失。这通常通过事务日志来实现。持久性意味着，例如，如果服务器崩溃，数据库在启动时可以检查日志并将任何尚未完成的事务提交到数据库。

PostgreSQL 遵循 ACID 标准，但 MySQL 同样允许你选择使用符合 ACID 标准的表。MyISAM 表不符合 ACID 标准，而 InnoDB 表符合。不符合 ACID 标准并非易事：所有额外的预防措施都会带来性能上的开销。

## SQL 子查询

子查询允许你将多个操作组合成一个原子单元，并允许这些操作访问彼此的数据。通过使用 SQL 子查询，你可以对数据库执行某些极其复杂的操作。此外，使用 SQL 查询可以消除由于另一个用户对同一组数据执行某些操作而导致两个操作之间数据发生变化的潜在问题。在当前的 Ubuntu 版本中，PostgreSQL 和 MySQL 都支持子查询，但在之前的版本中并非如此。

## 过程化语言与触发器

过程化语言是一种外部编程语言，你可以用它来编写函数和过程。通过过程化语言，你可以完成简单 SQL 无法完成的任务。触发器允许你定义在特定事件发生时触发的函数或过程。例如，在执行插入、更新或删除操作时，触发器可以根据数据的变化执行预定义的逻辑。

例如，在数据库中，你可以使用触发器在用户输入不符合预期的值时触发异常。PostgreSQL 拥有的过程化语言是 PL/pgSQL。虽然 MySQL 支持存储过程和触发器，但其功能并不完全相同。

## 配置 MySQL

一个免费且稳定的 MySQL 版本包含在 Ubuntu 中。你也可以从 mysql.com 获取。

在安装 MySQL 之后，你需要初始化数据库表或权限。请参阅第 9 章“管理软件”获取有关添加或删除软件的详细信息。你可以通过以 root 身份运行 `mysql_installdb` 来。

> **注意：**
> MySQL 数据目录需要由 MySQL 进程所有（你可能需要使用 `chown` 命令更改所有者）。此外，只有该用户应该拥有此目录（也就是说，应该使用 `chmod` 将权限设置为 `700`）。任何其他方式设置权限都会产生安全漏洞。

运行 `mysql_installdb` 可能会如下输出：

```
matthews@eymour:-$ sudo mysql_installdb
Preparing db table
Preparing host table
Preparing user table
Preparing func table
Preparing tables_priv table
Preparing columns_priv table
Installing all prepared tables
02916 17:39:05 /usr/libexec/mysql: Shutdown Complete
```

该命令为系统准备 MySQL 并提供了帮助信息。下一步是为用户设置密码，将在下节中讨论。

> **注意：**
> 默认情况下，MySQL root 用户没有密码。这是你必须更改的内容之一，因为 MySQL root 用户可以访问数据库的所有方面。下节将解释如何更改用户密码。

## 为 MySQL root 用户设置密码

要为 MySQL root 用户设置密码，你需要以 root 用户身份连接到 MySQL 服务器；你可以使用命令 `mysql -u root`。此命令通过 MySQL 客户端连接到服务器。当你拥有 MySQL 命令提示符时，使用如下命令为 root 用户设置密码：

```
mysql SET PASSWORD FOR root = PASSWORD('*secretword');
```

`secretword` 应该替换为你为 root 用户设置的密码。你可以使用相同的命令配合其他用户名为其他数据库用户设置或更改密码。

输入密码后，可以在提示符处输入 `exit` 退出 MySQL 客户端。

## 在 MySQL 中创建数据库

在 MySQL 中，你使用 `CREATE DATABASE` 语句创建数据库。要创建数据库，通过输入 `mysql -u root -p` 并按回车连接到服务器。这样做之后，你以 root 用户身份连接到数据库并被提示密码。输入密码后，你将进入 MySQL 命令提示符。然后你使用 `CREATE DATABASE` 语句。

> **注意：**
> 请参“MySQL 命令行客户端”章节以获取额外的命令行选项。

稍后，如果你需要从 `foobar` 撤销权限，可以使用 `REVOKE` 语句。例如，以下语句撤销了用户 `foobar` 的所有权限：

```
REVOKE ALL ON animals FROM foobar;
```

高级数据库管理、权限和安全是复杂的课题，超出了本书的涵盖范围。请查看本章末尾的“参考文献”部分获取在线文档的链接。你也可以查看 Sams Publishing 出版的 Luke Welling 和 Laura Thompson 编写的书籍《PHP and MySQL Web Development》（ISBN: 0-672-32919-6）。

## 配置 PostgreSQL

如果你不想使用 Ubuntu 自带的 PostgreSQL 版本，可以在 www.postgresql.org 获取 PostgreSQL 的二进制文件和源码。PostgreSQL 软件包以多个文件的形式分发。至少，你可以使用 `postgresql` 软件包。你应该查看 FTP 目录 `ftp.postgresql.org/pub/` 下的 `README` 文件，以确定你是否需要其他其他包。

如果你是从 Ubuntu 软件包进行安装，系统会自动创建一个必要的 `postgres` 用户账户（即，用户名为你系统上运行服务器的用户）：

```
matthew@seymour:~$ grep postgres /etc/passwd
postgresql:x:26:26:PostgreSQL Server:/var/lib/postgresql:/bin/bash
```

否则，你需要在安装期间创建一个用户账户。该用户不应具有登录权限，因为只有 `root` 用户应该可以使用它来切换到该用户，而且没有人会直接以该用户身份登录（有关如何向 Ubuntu 系统添加用户的更多信息，请参阅第 12 章“管理用户”）。在添加用户后，你可以使用 `dpkg -i` 命令对你下载的每个 PostgreSQL 软件包进行默认安装。

## 在 PostgreSQL 中初始化数据目录

安装会初始化数据库，并将数据目录的权限设置成正确的值。

> **注意：**
> `initdb` 程序将数据目录的权限设置为 `700`。你不应该将这些权限更改为其他任何值，以避免创建安全漏洞。
