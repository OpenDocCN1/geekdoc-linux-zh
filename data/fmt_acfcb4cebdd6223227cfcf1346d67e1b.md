
```text
Your MySQL connection id is 43 to server version: 3.23.58

输入 'help;' 或 '\h' 获取帮助。输入 '\c' 清空缓冲区。

mysql>
```

> 注意
> 请参阅“MySQL 命令行客户端”章节以获取额外的命令行选项。

稍后，如果你需要撤销 `foobar` 的权限，可以使用以下语句撤销用户 `foobar` 的所有权限：

```
REVOKE ALL ON ANIMALS FROM foobar;
```

高级数据库管理、权限和安全是复杂的课题，超出了本书的涵盖范围。请参阅本章末尾的“参考（References）”部分获取指向在线文档的链接。你也可以查看 Sams Publishing 出版的由 Luke Welling 和 Laura Thompson 编写的《PHP and MySQL Development》。

# 配置 PostgreSQL

如果你不想使用 Ubuntu 自带的 PostgreSQL 版本，可以在 www.postgresql.org 获取最新的 PostgreSQL 二进制文件和源码。PostgreSQL 软件包作为单独的文件分发。你至少需要 `postgresql` 软件包。无论你是否需要其他任何包，你都都应该在 FTP 目录中看到 `README` 文件。

如果你从 Ubuntu 软件包安装，系统会自动为你创建一个必要的 `postgres` 用户账户（即一个与你系统上运行的用户同名的账户）：

```
mathew@seymour:~$ grep postgres /etc/passwd
postgres:x:26:26:/var/lib/postgresql:/bin/bash
```

否则，你需要在安装期间创建一个名为 `postgres` 的用户。此用户不应在安装期间被创建（此处原文逻辑可能有误，通常指在安装过程中创建）。（注：此处原文存在逻辑重复）

如果这是一个已经拥有密码的现有用户且你正在修改权限，可以省略语句中的 `IDENTIFIED` 部分。例如，要对名为 `sampled` 的数据库向名为 `foobar` 的用户授予所有权限，可以使用以下命令：（此处重复了前文的示例）

```
GRANT ALL ON sampled.* TO foobar IDENTIFIED BY 'secretword';
```

用户 `foobar` 现在可以使用密码 `secretword` 连接到 `sampled` 数据库，并且 `foobar` 拥有该数据库的所有权限，包括创建和销毁表的能力。例如，用户 `foobar` 现在可以登录服务器（在本例中使用当前主机名 `shuttle2`），并按如下方式访问数据库：

```
mathew@seymour:- mysql shuttle2 -u foobar -p
Enter password:
Welcome to the MySQL monitor. Commands end with ; or \
Your MySQL connection id is 43 to server version: 3.23.58

输入 'help;' 或 '\h' 获取帮助。输入 '\c' 清空缓冲区。

mysql>
```

# 初始化 PostgreSQL 数据目录

在 PostgreSQL 中初始化数据目录

初始化数据目录并设置目录权限。

> 注意
> `initdb` 程序设置目录权限。

你可以以 `postgres` 用户身份运行以下命令：

```
postmaster -D /usr/local/data
```

如果你决定使用 `/usr/local/data` 以外的目录，请以 `postgres` 用户身份。

> 提示
> 默认情况下，PostgreSQL 会使用 `/var/lib/postgresql/data`。

# 在 PostgreSQL 中创建数据库

在 PostgreSQL 中创建数据库

在 PostgreSQL 中创建数据库非常简单，但必须由具有创建数据库的用户执行。你可以以 `postgres` 用户身份使用 `psql` 创建数据库，如下：

```
mathew@seymour:~ psql sampled
```

如果你在调用 `psql` 时没有指定数据库名称，它将尝试连接到与用户名同名的数据库。

`createdb` 程序是一个包装器，让你无需登录 `psql` 即可创建数据库。然而，你也可以在 `psql` 内部使用 `CREATE DATABASE` 语句。例如：

```
CREATE DATABASE database;
```

# 在 PostgreSQL 中创建数据库用户

在 PostgreSQL 中创建数据库用户

创建数据库用户需要使用 `postgres` 用户身份。你可以使用 PostgreSQL 的 `createuser` 命令快速创建一个允许访问数据库或创建新数据库的用户，如下：

```
matthew@seymour:~ createuser
允许新用户创建数据库吗？(y/n) y
允许新用户创建新用户吗？(y/n) y
CREATE USER
```

在此示例中，创建了名为 `phusion` 的新用户，并允许其创建数据库和数据库用户。（请仔细考虑谁被允许创建新数据库或额外的用户。）

你也可以通过 PostgreSQL 命令行客户端创建新用户，输入 `psql` 后使用 `CREATE USER` 语句。

> 注意
> PostgreSQL 允许你省略语句中的 `WITH PASSWORD` 部分。然而，这样做会导致创建的用户没有密码。这是一个安全漏洞，因此在创建用户时应始终使用 `WITH PASSWORD` 选项。

> 注意
> 当你完成 `psql` 命令行客户端的操作时，可以输入 `\q` 退出并返回 shell 提示符。

# 在 PostgreSQL 中删除数据库用户

删除数据库用户需要使用 `dropuser` 命令以及用户名称，该用户对默认数据库的访问将被移除，如下：

```
dropuser phusion
```

```
matthew@seymour:-$ dropuser msmith
DROP USER
```

你也可以通过 `psql` 登录数据库，然后使用 `DROP USER` 命令。这里有一个示例：

```
matthew@seymour:-$ psql demob
Welcome to psql, the PostgreSQL interactive terminal.

Type: \copyright for distribution terms
\h for help with SQL commands
\? for help on internal slash commands
\g or terminate with semicolon to execute query
\q to quit
```

```
demobdb# DROP USER msmith ;
DROP USER
demobdb# \q
```
