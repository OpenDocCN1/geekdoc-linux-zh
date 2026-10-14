
否则，您需要在安装期间创建一个 `postgres` 用户。该用户不应具有登录权限，因为只有 root 应该能够使用 `su` 变为该用户，且没有人会直接登录为该用户。（请参见第 14 章“管理用户”以获取有关如何向 Ubuntu 系统添加用户的更多信息）。添加用户后，您可以使用标准的 `dpkg -i` 命令对您下载的每个 PostgreSQL 软件包进行默认安装。

## 在 PostgreSQL 中初始化数据目录

安装软件包后，您必须初始化数据目录，且您必须是 root 用户。以下示例假设数据目录为 `/usr/local/postgresql/data`。

使用 `mkdir` 创建 `/usr/local/postgresql/data` 目录，并使用 `chown` 和 `chgrp` 修改目录所有权，使其属于 `postgres` 用户。然后使用 `su` 切换到 `postgres` 用户执行以下命令：

```bash
# mkdir /usr/local/postgresql/data
# chown postgres /usr/local/postgresql/data
# chgrp postgres /usr/local/postgresql/data
# su - postgres
# initdb -D /usr/local/postgresql/data
```

`initdb` 程序会初始化数据库并设置数据目录的权限。

> 警告
>
> `initdb` 程序将目录权限设置为 700。您不应将这些权限更改为其他值，以避免安全漏洞。

如果您决定使用 `/usr/local/postgresql/data` 以外的目录作为数据目录，应将 `postmaster` 命令中的目录替换为您实际使用的目录。

## 在 PostgreSQL 中创建数据库

在 PostgreSQL 中创建数据库非常简单，但必须由具有创建数据库权限的用户执行——例如，初始名为 `postgres` 的用户。随后您可以直接从 shell 提示符（不是客户端提示符，而是普通提示符）执行以下命令：

```bash
# su postgres
createdb database
```

其中 `database` 是您想要创建的数据库名称。`createdb` 程序实际上是一个包装器，使得无需登录并使用 SQL 即可更容易创建数据库。然而，您也可以在 SQL 中使用 `CREATE DATABASE` 语句创建数据库。例如：

```sql
CREATE DATABASE database;
```

在启动 postgres 客户端程序之前，您需要至少创建一个数据库。您应该在以 `postgres` 用户身份登录时创建此数据库。要登录该用户，您需要使用 `su` 变为 root，然后使用 `su` 变为 `postgres` 用户。要连接到新数据库，使用新数据库名称作为命令行参数启动 postgres 客户端程序，如下所示：

```bash
$ psql sampledata
```

## 在 PostgreSQL 中创建数据库用户

要创建数据库用户，您使用 `su` 从 Linux root 账户变为该用户。随后您可以使用 PostgreSQL 的 `createuser` 命令快速创建一个允许访问数据库或创建新数据库用户的用户，如下所示：

```bash
$ createuser madison
```

是否允许新用户创建数据库？(y/n) y

是否允许新用户创建更多用户？(y/n) y

CREATE USER

在这个示例中，创建了一个名为 phusion 的新用户，并允许其创建新的数据库和数据库用户（你应该仔细考虑谁被允许创建新数据库或额外的用户）。

你也可以使用 PostgreSQL 命令行客户端，通过输入 `psql` 加上数据库名称来创建新用户，然后使用 `CREATE USER` 命令来创建新用户。以下是一个示例：

```
CREATE USER foobar ;
```

PostgreSQL 允许你省略语句中的 `WITH PASSWORD` 部分。然而，这样做会导致创建的用户没有密码。这是一个安全漏洞，因此在创建用户时，你应该始终使用 `WITH PASSWORD` 选项。

当你完成在 `psql` 命令行客户端中的工作时，可以可以输入 `\q` 退出并返回到 shell 提示符。

## 在 PostgreSQL 中删除数据库用户

要删除数据库用户，请使用 `dropuser` 命令并结合用户名，这将从默认数据库中移除该用户的访问权限，如下所示：

```
$ dropuser msmith
DROP USER
```

你也可以通过 `psql` 登录数据库，然后使用 `DROP` 命令。这里是一个示例：

```
$ psql demodb
Welcome to psql, the PostgreSQL interactive terminal.
```

```
Type: \copyright for distribution terms
\h for help with SQL commands
\? for help on internal slash commands
\g or terminate with semicolon to execute query
\q to quit
```

```
demodb=# DROP USER msmith;
DROP USER
demodb=# \q
$
```

## 在 PostgreSQL 中授予和撤销权限

与 MySQL 类似，PostgreSQL 中的授予和撤销权限是通过 `GRANT` 和 `REVOKE` 语句完成的。语法与 MySQL 相同，但 PostgreSQL 不使用语句中的 `IDENTIFIED BY` 部分，因为正如之前讨论的，PostgreSQL 的密码在使用 `CREATE USER` 语句创建用户时进行分配的。以下是 `GRANT` 语句的语法：

```
GRANT what_to_grant ON where_to_grant TO user_name;
```

例如，以下命令授予用户 `foobar` 在 `sampledata` 数据库上的所有权限：

```
GRANT ALL ON sampleddata TO foobar;
```

要撤销权限，你使用 `REVOKE` 语句。这里是一个示例：

```
REVOKE ALL ON sampledata FROM foobar;
```

此命令移除了用户 `foobar` 在 `sampledata` 数据库上的所有权限。高级管理和用户配置是复杂的话题。本节无法涵盖 PostgreSQL 或权限和用户的所有方面。有关管理 PostgreSQL 的更多信息，请参阅 PostgreSQL 文档或参考关于 PostgreSQL 的书籍（Sams Publishing）。

## 数据库客户端

MySQL 和 PostgreSQL 都使用客户端/服务器系统来访问数据库。简单来说，数据库服务器处理进入数据库的请求，而数据库客户端负责将请求发送到服务器，并将服务器的输出获取给用户。

如果数据库服务器恰好位于用户正在使用的同一台机器上，用户也不会与数据库服务器直接交互。数据库服务器的所有请求都由数据库客户端处理，该客户端可能运行在与数据库服务器相同的机器上，也可能不在。

MySQL 和 PostgreSQL 都有命令行客户端。命令行客户端是与数据库交互的一种原始方式，通常不被终端用户使用。然而，作为 DBA（数据库管理员），你可以使用命令行客户端交互式地测试新查询，而无需为该目的编写前端程序。在本章的后续章节中，你将学习有关 MySQL 图形客户端以及适用于 MySQL 和 PostgreSQL 的 Web 数据库接口的知识。

接下来的章节将探讨访问远程数据库的两种常用方法、本地访问数据库服务器的方法，以及 Web 访问数据库的概念。

## 注意

在设置数据库时，你应该考虑访问和权限问题。用户是否应该能够创建和删除数据库？还是他们只能使用现有的数据库？用户是否能够向数据库添加记录并修改现有记录？用户是否应该被限制对数据库进行只读访问？其他世界呢？普通公众是否需要通过互联网对你的数据库进行任何访问？作为 DBA，你必须确定这些问题的答案。

## 数据库的 SSH 访问

本节简要讨论了两种远程数据库访问场景。在第一种情况下，用户通过 SSH 直接登录数据库服务器（以利用加密会话的安全优势），然后在服务器上启动一个程序来访问数据库。在这种情况下（如图 21.4 所示），数据库客户端运行在数据库服务器本身。

![](img/757e95bd85c59465935194247625328c_542_0.png)

图 21.4 用户从工作站（主机 cheetah）登录到位于主机 simba 的数据库服务器。数据库客户端运行在 simba 上。

在另一种情况下（如图 21.5 所示），用户通过 SSH 登录到远程主机并在上面启动一个程序来访问数据库，但数据库实际上运行在三个系统上——现在涉及到三个系统：用户的工作站、运行数据库客户端的远程主机以及运行数据库服务器的远程主机。
