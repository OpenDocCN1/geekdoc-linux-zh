

# Linux 生产力客户端与办公套件
## 第 28 章

891

# 数据库

我们几乎每天都会听到数据库供应商的名字——Oracle、Sybase、Informix，它们的受欢迎程度和销售额正如野火般增长。然而，在 Linux 上处理数据并不一定需要运行在昂贵的专有数据库系统中。Linux 上存在许多健壮且符合 SQL 标准的数据库。PostgreSQL 和 Postgres 是可用数据库的两个示例。

### 注意

SQL 代表结构化查询语言（Structured Query Language）。尽管 SQL 是访问数据库的标准语言，但不要将其视作一门编程语言。

SQL 是一种数据定义语言（DDL），用于定义数据库结构。它也是一种数据操作语言（DML），用于访问和修改存储在符合 SQL 标准的数据库中的数据。

SQL 的实现不相同，通常取决于数据库供应商增加的功能。通常会添加诸如程序控制或其他编程语言构造等额外功能来创建一个新产品，例如 Oracle 的 PL/SQL。

目前有多个标准，你应该努力选择符合 SQL-92 标准的数据库。92 表示该标准创建的年份。新的标准肯定会出现。请务必关注功能以确保向后兼容。这有助于维护旧数据库应用程序的实用性。

# PostgreSQL

PostgreSQL 是一个功能关系型数据库管理系统。它具有你对专业 RDBMS 所预期的所有功能，例如完全符合 SQL 标准和事务支持。PostgreSQL 已证明自己是开源世界的另一个成员，能够很好地支持数 GB 的数据库和高事务负载。它还处于活跃开发中，最近发布了 6.5 版本。

![](img/cbac72550c7126a22162e94d91a0c360_926_0.png)

# 图形、多媒体与生产力工具

# 第四部分

Postgres 是 PostgreSQL 前身，开发于加州大学伯克利分校，在 Michael Stonebreaker 教授的指导下。名称发生了变化，功能也得到了增加，这些都是通过全球数百名志愿者利用互联网完成的。

PostgreSQL 提供的优秀功能之一是事务支持。理解事务的概念非常重要，因为它在处理支付、贷记和收费等事务（例如在财务应用程序中）时，提供了至关重要的错误处理机制。

# 获取与安装 PostgreSQL

PostgreSQL 随许多 Linux 发行版一起提供，也可以在互联网 http://www.postgresql.org 获取。PostgreSQL 是一个开源产品，以源代码和二进制文件的形式提供。PostgreSQL 提供 RPM 格式，使安装变得非常简便。

以下是你需要的组件：

- postgresql——此软件包提供了大部分功能，包括后端数据库服务。
- postgresql-clients——这是一组实用程序，允许你在客户端/服务器模型中与后端数据库服务器进行交互。它为 C、C++ 和 Perl 接口提供了库。
- postgresql-devel——此软件包提供了库和头文件，允许你编译直接与数据库通信的应用程序。
- postgresql-data——此软件包提供初始数据库结构，允许用户立即开始使用 PostgreSQL。

# 它们是如何协同工作的？

PostgreSQL 使用客户端/服务器模型。后端数据库服务器运行在服务器机器上。你必须在这里分清服务器类型。这很容易混淆！数据库服务器处理由各种前端界面提出的所有 SQL 查询。

前端界面可以是 psql（以前称为 monitor）或支持 PostgreSQL API 的各种语言编写的程序。monitor 是一个交互式环境，类似于 shell，允许你从命令行执行 SQL 命令和 PostgreSQL 命令。你也可以在此区域管理数据库。API 支持 C、C++、Perl、Python、tcl，当然还支持通过 ODBC 和 JDBC 进行 SQL 连接。

两个区域（后端和前端）之间的通信由 postmaster 控制。postmaster 是一个持续运行的守护进程，管理连接和内存分配，并在建立连接时执行必要的初始化。基本上，前端向 postmaster 表明它需要数据库连接。postmaster 会进行必要的准备并连接到后端服务器。

# 为首次使用配置 PostgreSQL

在安装必要的组件后，必须进行一些配置。你需要确保 postmaster 守护进程正在运行，并将自己设置为 PostgreSQL 用户。然后你就可以开始创建数据库和操作数据了。

安装程序应该将详尽文档的副本放在你的系统中，可能位于 /usr/doc/postgresql-x.x.x，其中 x.x.x 是你使用的版本号。所有常见的启动问题在该处都有详细说明。

# 初始化与启动 postmaster

第一要工作是初始化。图 28.20 显示了某些信息。

![](img/cbac72550c7126a22162e94d91a0c360_928_0.png)

初始化后，你可以使用以下命令启动 postmaster 守护进程：

```bash
$ postgresql start
```

# 创建用户

使用 /usr/bin/createuser 命令将自己设置为用户，并回答问题：

```bash
$ createuser johndoe
Enter user:
```

# 创建数据库

现在，创建一个数据库。命名为 vegetable：

现在你已经有了数据库，进入 psql monitor 并与你的数据库交互：

```bash
$ psql vegetable
```

此时，你可以使用 SQL 命令与数据库交互以创建表和字段。

> 提示 如果对某个命令卡住了并需要帮助，请尝试 \?这将给出斜杠命令列表。

# 使用 PostgreSQL psql

尽管描述 SQL 语法超本书的范围，但请查看 psql monitor 中的几条条目及其结果。（注意：OCR 文本如下）。

psql monitor 环境对用户来说类似于 shell 或命令行。不是普通的 shell 提示符，而是如下提示符：

```bash
variable=>
```

# 短练习

在这个简短练习中，我们将创建一个表（PostgreSQL 称为 *class*）。这展示了在使用 psql monitor 时使用斜杠命令和 SQL 语句的方法。

首先列出数据库：

```bash
variable=> \l
```

| datname | datbase | datpath |
|---------|---------|----------|
| template1 | 100 | template1 |
| vegetable | 501 | vegetable |

尝试一些 SQL。使用 CREATE 语句创建一个名为 names 的表，并在其中存储蔬菜记录。该类将具有属性（也称为 *fields*）。

```bash
variable=> CREATE TABLE names (vegie_name varchar(40), quantity int);
CREATE
```

CREATE 让你语句已完成，但请通过列出表查看该语句的结果：

```bash
variable=> \d
```

| Database = vegetable |
+----------+------+-------+
| ! Owner | Relation | Type |
+----------+------+-------+
| johndoe | names | table |
+----------+------+-------+

