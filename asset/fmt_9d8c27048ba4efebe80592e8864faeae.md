
INSERT INTO table_name (column1,column4) VALUES('value1', 'value2');

你也可以使用单个 `INSERT` 语句填充多行数据，语法如下所示：

```
INSERT INTO table_name VALUES('value1', 'value2'),('value3', 'value4');
```

在这条语句中，`value1` 和 `value2` 被插入到第一行，`value3` 和 `value4` 被插入到第二行。

下面的示例展示了如何向 `cd_collection` 表插入 `Nevermind` 条目：

```
INSERT INTO cd_collection VALUES(9, 'Nevermind', 'Nirvana', '1991', 'NULL');
```

如果你不想包含评分（rating），MySQL 要求最后一列（评分）必须为 `NULL` 值。相比之下，PostgreSQL 允许你省略最后一列。当然，如果你中间的列为 `NULL`，则你需要在 `INSERT` 语句中显式地声明 `NULL`。

通常，`INSERT` 语句会被编码到前端程序中，这样向数据库添加数据的用户就不必担心涉及的 SQL 语句。

## 从数据库中检索数据

当然，将数据存储在数据库的主要目的是为了以后对这些数据进行查询、排序和生成报告。基础的数据检索是通过 `SELECT` 语句完成的，其语法如下：

```
SELECT column1, column2, column3 FROM table_name WHERE search_criteria;
```

语句的前两个部分——`SELECT` 和 `FROM` 部分是必须的。语句中的 `WHERE` 部分是可选的。如果省略它，将返回 `table_name` 中的所有行。

`column1, column2, column3` 表示你想查看的列。如果你想查看所有列，可以使用通配符 `*` 来显示匹配搜索条件的所有列。例如，以下语句显示了 `cd_collection` 表中的所有列：

```
SELECT * FROM cd_collection;
```

如果你只想查看表中所有 CD 的标题，可以使用如下所示的语句：

```
SELECT title FROM cd_collection;
```

若要选择 CD 的标题和年份，你将使用以下语句：

```
SELECT title, year FROM cd_collection;
```

如果你想要稍微更复杂一点，可以使用 SQL 打印 CD 标题后跟括号内的年份，这是惯例。MySQL 和 PostgreSQL 都提供了字符串连接函数来处理此类问题。然而，这两个系统的语法是不同的。

在 MySQL 中，你可以使用 `CONCAT()` 函数将标题和年份列合并为一个带括号的输出列。以下语句是一个示例：

```
SELECT CONCAT(title,' ',year) AS TitleYear FROM cd_collection;
```

该语句在名为 `TitleYear` 的单列下同时列出了标题和年份。注意 `CONCAT()` 函数中除了字段外两个字符串——这些字符串增加了空格和括号。

在 PostgreSQL 中，字符串连接使用双竖线 `||`。以下命令是上述 MySQL 命令的 PostgreSQL 等效写法：

```
SELECT (title||' '||year) AS TitleYear FROM cd_collection;
```

注意，括号是可选的，但它们使语句更易读。再次，中间和结尾的字符串（注意引号之间的空格）用于插入空格和括号。

当然，并不仅于此，你并不想要数据库中每一行的列表。相反，你想要找到符合某些特征的行。为了这一点，你需要在 `SELECT` 语句中添加 `WHERE` 子句。例如，假设你想找到 `cd_collection` 表中所有评分为 5 的 CD。你将使用如下语句：

```
SELECT * FROM cd_collection WHERE rating = 5;
```

使用图 21.2 中的表，你可以看到此查询将返回 Nirvana 的行。这是简单的，而且 SQL 能够处理比这更复杂的查询。复杂的查询可以使用逻辑运算符编写。例如，假设你想精炼查询，使其仅列出不是在 2003 年发行的 CD。你将使用如下查询：

```
SELECT * FROM cd_collection WHERE year != 2003;
```

在 SQL 中，`!=` 意味着“不等于”。再次查看图 21.2 中的表，你可以看到此查询返回了 Nirvana 的行，但没有返回 2003 年发行的 Metallica 的行。

那么，如果你想列出所有评分为 3 或 4 的 CD 呢？这次，组合逻辑运算符：

```
SELECT * FROM cd_collection WHERE rating = 3 OR rating = 4;
```

此查询将返回 Pink Floyd 和 Metallica 的条目。然而，它不会返回 Nirvana 的条目，因为它是在 1991 年发行的。

## 提示

数据库程序员最常见的错误之一是混淆逻辑运算符。例如，在日常口语中，你可能会说“找到所有在 2003 年和 2004 年发布的 CD”。初一看，你可能认为如果将此语句交给数据库，它将返回所有行。事实上，它将不会返回任何行，因为一张 CD 不可能同时在 2003 年和 2004 年发行。形成此语句的正确方法是使用 `OR` 而不是 `AND`。

## 选择数据库：MySQL 对比 PostgreSQL

如果你正刚开始学习数据库，首先要研究哪种数据库适合你的需求。许多数据库软件包是免费的，有些则价值数万美元。本书不涵盖昂贵的数据库。相反，本章关注两个免费数据库：MySQL 和 PostgreSQL。

这两个数据库都非常强大，而且任何一个都可能满足你的需求。对于初学者来说，选择哪一个可能并不重要。然而，它们在某些方面具有独特的特性。

### 速度

直到最近，如果查询速度对你至关重要，选择是简单的：MySQL 以极快闻名。直到最近，PostgreSQL 相比之下很慢。

新版本的 PostgreSQL 在磁盘访问等速度方面有了改进。在某些情况下，对于密集访问，PostgreSQL 比 MySQL 快得多，正如我们在下一节所示。然而，MySQL 仍然非常快。

### 数据锁定

为了防止数据损坏，数据库在访问数据时需要对数据加锁。只要锁存在，任何其他进程无法访问该数据。这意味着其他尝试访问数据的进程必须等待当前进程完成。下一个进程锁定数据直到它结束，其余进程必须等待，以此类推。

当然，数据库操作通常完成很快，在同时访问数据库的用户较少的情况下，锁持续时间短，不会引起任何延迟。然而，在许多人同时访问数据库的环境中，锁定可能会产生问题，人们必须等待。

旧版本的 MySQL 在表级别锁定数据，这在密集访问期间被认为是瓶颈。这意味着当某人在表中写入某行数据时，整个表都会被锁定，其他人无法输入数据。如果你的表中有 500,000 行（或记录），当访问一行时，所有 500,000 行都会被锁定。再次，在并发用户相对较少的环境中，这不会引起严重的性能问题，因为大多数操作执行得非常快。

另一方面，PostgreSQL 在行级别锁定数据。在 PostgreSQL 中，只有当前正在访问的行被锁定。表的其他部分可以被其他用户访问。这种行级锁定显著减少了在大并发用户环境下锁定对性能的影响。

### 事务处理中的 ACID 特性以保护数据完整性

MySQL 和 PostgreSQL 在防止数据损坏的保护方面还有不同之处。ACID 缩写通常用于描述数据保护的几个方面：

- **原子性（Atomicity）**——这意味着多个数据库操作被视为一个不可分割的（原子）单元，通常称为*事务*。在事务中，要么执行所有的单元操作，要么一个都不执行。换句话说，如果原子单元中的任何操作失败，整个原子单元都将取消。
- **一致性（Consistency）**——确保任何事务都不会导致数据库处于不一致状态。不一致状态可能由数据库崩溃、网络故障和类似情况引起。一致性确保在某种情况下，任何可能导致数据处于不一致状态的事务或部分完成的事务都会被*回滚*或撤销。
- **隔离性（Isolation）**——确保在相同数据上操作的多个事务彼此完全隔离。这可以防止两个用户同时尝试向同一条记录写入数据时的数据损坏。隔离处理器通常可以由数据库程序员配置。正如之前讨论过的，处理隔离性的一种方法是通过锁来实现。
- **持久性（Durability）**——确保在事务提交到数据库后，即使发生系统崩溃、网络故障或其他问题，它也不会丢失。这通常通过事务日志来实现。例如，如果服务器崩溃，数据库可以在备份时检查日志，并将所有尚未完成的事务提交到数据库。

PostgreSQL 符合 ACID 标准，但同样，MySQL 允许你选择使用符合 ACID 标准的表或不符合的。`MyISAM` 表不符合 ACID 标准，而 `InnoDB` 表符合。请注意，实现 ACID 合规性绝非易事：所有额外的预防措施都会产生性能开销。

## SQL 子查询

子查询允许你将多个操作组合成一个原子单元，并允许这些操作相互访问对方的数据。通过使用 SQL 子查询，你可以在数据库上执行极其复杂的操作。此外，使用 SQL 子查询消除了由于另一个用户对相同数据集执行某些操作而导致两次操作之间数据发生潜在问题。在当前的 Ubuntu 版本中，PostgreSQL 和 MySQL 都支持子查询，但在之前的版本中并非如此。

## 过程语言与触发器

过程化语言是一种外部编程语言，可用于编写函数和过程。这允许你执行简单 SQL 不支持的操作。触发器允许你定义一个事件，该事件将调用你编写的外部函数或过程。例如，如果提供的 `INSERT` 语句包含某个列的意外值或超出范围的值，可以使用触发器来捕获异常。

例如，在 CD 跟踪数据库中，如果用户输入了不合理的数据，你可以使用触发器来捕获异常。PostgreSQL 有一种名为 `PL/pgSQL` 的过程化语言。虽然 MySQL 支持有限的内置过程和触发器，但它没有任何过程化语言。这意味着你无法在 MySQL 中创建自定义过程或触发器，尽管通常可以通过客户端编程实现相同的效果。

## 配置 MySQL

一个免费且稳定的 MySQL 版本。你也可以从网站 http://www.mysql.com 获取 MySQL。该软件提供源码、二进制文件和适用于 Linux 的 APT 格式。你可以使用 `Synaptic` 将软件添加到你的系统中。有关添加（或删除）软件的详情，请参阅第 7 章。

安装 MySQL 后，你需要初始化授权表或权限，以访问所有数据库、表以及数据库中的表和列数据。你可以通过以 root 身份运行 `mysql_install_db` 来实现此操作。该命令初始化授权表并创建一个 MySQL root 用户。

> **注意**
> MySQL 数据目录需要由运行 MySQL 的用户所有（使用 `chown` 命令更改所有者）。此外，此用户应该拥有该目录的任何权限。（换句话说，应通过 `chmod` 将权限设置为 700。）任何其他方式设置数据目录都会产生安全漏洞。

运行 `mysql_install_db` 应产生类似的输出：

```
sudo mysql_install_db

Preparing db table

Preparing host table

Preparing user table

Preparing func table

Preparing tables_priv table

Preparing columns_priv table

Installing all prepared tables

020916 17:39:05 /usr/libexec/mysqld: Shutdown Complete
```

该命令为 MySQL 在系统上的使用做好准备并报告有用信息。下一步是为 MySQL root 用户设置密码，将在下一节中讨论。

> **注意**
> 默认情况下，创建 MySQL root 用户没有密码。这是你必须更改的首要事项之一，因为 MySQL root 用户拥有数据库所有方面的权限。下一节将解释如何更改用户密码。

## 为 MySQL root 用户设置密码

要为 MySQL root 用户设置密码，你需要以 MySQL root 用户身份连接到 MySQL 服务器；你可以使用命令 `mysql -u root` 来执行。该命令使用 MySQL 客户端连接到服务器。当你进入 MySQL 命令提示符时，执行如下命令来为 root 用户设置密码：

```
mysql> SET PASSWORD FOR root = PASSWORD('secretword');
```

`secretword` 应该替换为你任何想要作为 root 用户密码的字符串。你可以对其他用户名使用相同的命令来设置或更改其他数据库的密码。

输入密码后，你可以通过输入退出 MySQL 客户端。

## 在 MySQL 中创建数据库

在 MySQL 中，你使用 `CREATE` 语句创建数据库。要创建数据库，使用 `mysql -u root -p` 连接到服务器。输入 root 密码后，你将进入 MySQL 命令提示符。

```
mysql> CREATE DATABASE animals;
```

## 在 MySQL 中授予和撤销权限

你可能给自己授予权限，最终你还会向其他用户授予权限。权限（也称为*权利*）在四个级别上授予和撤销：

- 全局级——这些权限允许访问服务器上的任何数据库。
- 数据库级——这些权限允许访问数据库的所有表。
- 表级——这些权限允许访问表中的所有列。
- 列级——这些权限允许访问数据库表中的单个列。

> **注意**
> 所有可用权限超出了本章的范围。请查看 MySQL 文档获取更多信息。

要添加用户账户，你通过输入 `mysql -u root -p` 连接数据库。当你以 root 用户身份连接并提示密码时，要授予用户权限，请使用 `GRANT` 语句，其语法如下：

```
GRANT what_to_grant ON where_to_grant TO user_name IDENTIFIED BY 'password';
```

第一个选项 `what_to_grant` 是你授予用户的权限。这些权限通过关键字指定。例如，`ALL` 关键字用于向指定用户授予全局、数据库、表和列级权限。

第二个选项 `where_to_grant` 指定应授予权限的资源。第三个选项 `user_name` 是你想要授予权限的用户名。第四个选项 `password` 是应分配给该用户的密码。如果存在已有密码的现有用户且正在修改权限，可以省略语句中的 `IDENTIFIED BY` 部分。

用户 foobar 现在可以使用密码 `secretword` 连接到数据库 `sampledata`，且 foobar 拥有该数据库的所有权限，包括创建和销毁表的权限。例如，用户 foobar 现在可以登录到服务器（在本例中使用当前的主机名——`shuttle2`），并按如下方式访问数据库：

```
$ mysql -h shuttle2 -u foobar -p animals

Password:

Welcome to the MySQL monitor. Commands end with ; \g.

Your MySQL connection is 43 to server version: 3.23.58

Type 'help'; or '\h' for help. Type '\c' to clear the buffer.

mysql>
```

> **注意**
> 请参阅“MySQL 命令行客户端”章节以获取更多命令行选项。

稍后如果你需要撤销 foobar 的权限，可以使用 `REVOKE` 语句。例如，以下语句撤销了用户 foobar 的所有权限：

```
REVOKE ALL ON animals FROM foobar;
```

高级数据库管理、权限和安全是非常复杂的话题，超出了本书的讨论范围。请参阅本章末尾的“参考”章节以获取在线文档链接。你也可以查看 Luke Welling 和 Laura Thompson 编写的 Sam Publishing 出版的《PHP and MySQL Development》。

## 配置 PostgreSQL

如果你不想使用 Ubuntu 自带的 PostgreSQL 版本，可以在 http://www.postgresql.org 获取最新的 PostgreSQL 二进制文件和源码。PostgreSQL 软件包以多个文件的形式进行分发。你至少可能需要 `postgresql`、`postgresql-server` 和 `postgresql-libs` 软件包。你应该查看 FTP 目录 http://ftp.postgresql.org/pub/ 中的 `README` 文件来确定你是否需要其他软件包。

如果你是从 Ubuntu 软件包进行安装的，系统会自动为你创建一个必要的 `postgres` 用户账户（即一个与你系统上运行的用户同名的账户）：

```
$ fgrep postgres /etc/passwd

postgres:x:26:26:/var/lib/postgresql:/bin/bash
```
