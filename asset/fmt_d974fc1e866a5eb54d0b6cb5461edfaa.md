
自 MySQL 版本 5 起，你也可以使用 `CREATE USER` 命令一步添加新用户账户并分配密码：

```
mysql> create user 'mytest'@'localhost' identified by 'test';
Query OK, 0 rows affected (0.00 sec)
mysql>
```

这会创建一个名为 `mytest` 的新用户账户，该账户可以从 localhost 登录，密码为 `test`。

创建用户账户后，使用 SQL `GRANT` 语句为用户授予数据库的权限：

```
mysql> grant select,insert,update on test.* to rich;
Query OK, 0 rows affected (0.00 sec)
mysql>
```

在 `GRANT` 语句中，你定义用户账户想要访问的所有表 [使用通配符 (*) 表示数据库中的所有表]，以及要授予的具体权限。

新用户账户 `rich` 现在可以登录到 MySQL 服务器并访问 `test` 数据库：

```
$ mysql test -u rich -p -s
Enter password:
mysql>
```

因为我没有为 `rich` 用户账户授予 `CREATE` 权限，所以我无法在数据库中创建新表。我只能操作现有表。

# 在 PostgreSQL 中创建用户

在 PostgreSQL 中，用户账户称为登录角色。`postgres` 管理员用户可以创建新的登录角色并向这些角色授予对数据库对象的用户权限。请记住，Ubuntu 安装的 PostgreSQL 使用 Ubuntu 系统密码文件来验证登录角色，因此你的 PostgreSQL 登录角色必须与现有的 Ubuntu 系统用户账户匹配：

```
postgres=# create role rich login password 'test';
CREATE ROLE
postgres=# grant all on database test to rich;
GRANT
postgres=#
```

现在用户账户 `rich` 在 `test` 数据库中拥有完全权限：

```
rich@testbox:~$ psql test -q
test=>
```

`rich` 用户现在可以在 `test` 数据库中创建新表。

# 构建表

在数据库中，表存储实际数据。表包含数据字段，这些字段定义要存储的各个数据元素。在数据字段中，你必须定义数据的数据类型，因为数据库服务器必须知道每个数据字段所需的存储空间。MySQL 和 PostgreSQL 中常用的数据类型有：

- `char`：固定长度的文本字符串；如果数据未填满固定长度，则会在存储的数据中添加空格

- `varchar`：可变长度的文本字符串；数据库服务器仅为指定的文本创建足够的存储空间

- `integer`：没有小数位的整数

- `floating point`：具有不同小数位的十进制数

- `text`：用于大量文本的数据存储类型

- `binary large object` (`BLOB`)：一种二进制数据存储类型，允许你存储图像、视频和音频剪辑以及 PDF 文件等二进制文件

MySQL 和 PostgreSQL 都使用 `CREATE TABLE` 语句在你当前连接的数据库中创建一个新表。`CREATE TABLE` 语句定义了数据字段名称和数据的数据类型，以及数据所需的任何特殊功能：

```
test> create table test1(
test> employeeid int primary key,
test> lastname varchar(20),
test> firstname varchar(20),
test> datehired date);
NOTICE: CREATE TABLE / PRIMARY KEY will create implicit index "test1_pkey" for table "test1"
CREATE TABLE
test> \dt
List of relations
Schema | Name | Type | Owner
--------+-------+-------+------
public | test1 | table | rich
(1 row)
test>
```

PostgreSQL 会自动为 `primary key` 数据字段创建一个索引文件。`\dt` 命令会显示数据库中的新表。

# 添加和查看数据

一旦你在数据库中创建了表，你就可以用它来存储你的数据。使用 SQL `INSERT` 语句为每个单独的数据记录指定数据集：

```
test> insert into test1 values ('1234','Blum','Rich','01/01/09');
INSERT 0 1
test> insert into test1 values ('1234','Blum','Barbara','01/15/09');
ERROR: duplicate key value violates unique constraint "test1_pkey"
test> insert into test1 values ('1235','Blum','Barbara','01/15/09');
INSERT 0 1
test>
```

请注意，PostgreSQL 不允许我添加另一个使用相同 `primary key` 值的数据记录。

在数据输入后，你将希望能够从表中提取信息。SQL `SELECT` 语句提供了执行此操作的接口：

```
test> select employeeid from test1 where firstname ~ 'Rich';
 employeeid
------------
 1234
(1 row)

test>
```

`WHERE` 子句定义了一个过滤器表达式，用于测试表中的每个数据记录。`SELECT` 语句仅返回与过滤器匹配的数据记录。

# 总结

本章讨论了如何使用你的 Ubuntu 服务器发行版实现一个数据库服务器。Ubuntu 为流行的 MySQL 和 PostgreSQL 数据库服务器包提供了默认安装。MySQL 数据库服务器作为 LAMP 服务器安装的一部分安装，而 PostgreSQL 数据库服务器则在服务器安装过程中选择数据库服务器选项时安装。本章逐步介绍了两个数据库服务器中使用的文件布局和命令。了解数据文件的位置以及如何访问显示在运行数据库服务器时可能发生的任何错误消息的日志文件非常重要。本章以使用 MySQL 和 PostgreSQL 的命令行界面创建数据库、用户和表，以及在服务器上存储和检索数据的简要概述结束。

本章结束了服务器部分。下一部分将深入探讨 Ubuntu 为开发你自己的应用程序提供的编程环境。下一章讨论使用 shell 脚本来使你作为系统管理员的生活更轻松，或只是帮助自动化你在 Ubuntu 工作站或服务器上可能执行的常见任务。

# 第 5 部分：Ubuntu 编程

- Chapter 25: Shell Scripts

- Chapter 26: Perl and Python

- Chapter 27: C Programming

- Chapter 28: Java

- Chapter 29: Ruby

- Chapter 30: PHP

## Shell Scripts

![](img/39e65eeb4f54001ede08c6114ae3cc6c_636_0.png)

### Secrets in This Chapter

- What are Shell Scripts?

- Shell Script Basics

- Creating Your Own Scripts

### Using Multiple Commands

在第 19 章“Ubuntu 命令行”中，你看到了如何使用 shell 的命令行界面 CLI 提示符输入命令并查看命令结果。shell 脚本的关键在于能够输入多个命令并处理每个命令的结果，甚至可能将一个命令的结果传递给另一个命令。shell 允许你将命令链接在一起成为一个步骤。

如果你想一起运行两个命令，你可以在同一提示符行中输入它们，用分号分隔：

```
$ date ; who
Mon Nov 03 19:44:35 EST 2008
rich :0 2008-11-03 18:23 (console)
rich pts/1 2008-11-03 18:24
rich pts/0 2008-11-03 18:42
barbara pts/2 2008-11-03 19:30
katie pts/3 2008-11-03 19:39
$
```

恭喜，你刚刚写了一个 shell 脚本！这个简单的脚本只使用了两个 shell 命令。`date` 命令先运行，显示当前日期和时间，然后是 `who` 命令的输出，显示当前登录到系统的是谁。使用这种技术，你可以串联任意多个命令，直到最大命令行字符数 255 个字符。
