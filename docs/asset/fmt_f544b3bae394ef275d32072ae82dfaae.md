
高级数据库管理、权限和安全是非常复杂的话题，超出了本书的范围。请参阅本章末尾的“参考”部分获取在线文档的链接。你也可以查看 Luke Welling 和 Laura Thompson 编写 Sams Publishing 出版的书籍《PHP and MySQL Development》。

# 配置 PostgreSQL

如果你不想使用 Fedora 捆带的 PostgreSQL 版本，最新的 PostgreSQL 二进制文件和源码可以在 `http://www.postgresql.org/` 获取。PostgreSQL RPM 包以多个文件的形式分发。至少，你可能需要 `postgresql`、`postgresql-server` 和 `postgresql-libs` RPM 包。你应该查看 FTP 目录 `ftp://ftp.postgresql.org/pub/` 中的 `README.rpm-dist` 文件来确定你是否需要其他包。

如果你正在安装 Fedora RPM 文件，系统会自动为你创建一个新的 `postgres` 用户账户（即在你的系统上运行服务器的用户名为该名的账户）：

```
$ fgrep postgres /etc/passwd

postgres:x:26:26:PostgreSQL Server:/var/lib/postgresql:/bin/bash
```

否则，你需要在安装后创建一个名为 `postgres` 的用户。该用户不应该拥有登录权限，因为只有 root 用户应该能够使用 `su` 变成该用户，没有人会直接以该用户身份登录。（请参阅第 14 节“管理用户”获取有关如何向 Fedora 系统添加用户的更多信息。）添加完用户后，你可以使用标准的 `rpm -i` 命令对下载的每个 PostgreSQL RPM 包进行默认安装。

# 初始化 PostgreSQL 中的数据目录

安装 RPM 包后，你需要初始化数据目录。要做到这一点，你必须首先创建数据目录并且必须是 root 用户。以下示例假设数据目录为 `/usr/local/pgsql/`。

创建 `/usr/local/pgsql/data` 目录（使用 `mkdir`）并更改目录所有权（使用 `chown` 和 `chgrp`），使其由 `postgres` 用户所有。然后使用 `su`，以 `postgres` 用户身份执行以下命令：

```
# mkdir /usr/local/pgsql
# chown postgres /usr/local/pgsql
# chgrp postgres /usr/local/pgsql
# su postgres
```

`-bash-2.05b -D /usr/local/pgsql/data`
属于此数据库系统的文件将由 `postgres` 用户所有。该用户也必须知道服务器进程。数据库集群将使用 locale `en_US.UTF-8` 初始化。此区域设置将防止在模式匹配时使用索引。如果担心这一点，请重新运行 `initdb` 并将排序顺序设置为 "C"。

```
creating directory /usr/local/pgsql/data... ok
creating directory /usr/local/pgsql/data/base... ok
creating directory /usr/local/pgsql/data/global... ok
creating directory /usr/local/pgsql/data/pg_xlog... ok
creating directory /usr/local/pgsql/data/pg_clog... ok
creating template1 in /usr/local/pgsql/data/base/1... ok
creating configuration files... ok
initializing pg_shadow... ok
enabling unlimited row size for system tables... ok
initializing pg_depend... ok
creating system views... ok
loading pg_description... ok
creating conversions... ok
setting privileges on built-in objects... ok
vacuuming database1... ok
copying template0... ok
```

成功。你现在可以使用以下命令启动数据库：这将初始化数据库并将数据目录的权限设置为正确值。

> 警告
> `initdb` 程序将数据目录的权限设置为 700。你不应将这些权限更改为其他值，以免产生安全漏洞。

可以使用以下命令启动 `postmaster`（确保你仍是 `postgres` 用户）：

```
$ postmaster -D /usr/local/pgsql/data &
```

如果你决定使用 `/usr/local/pgsql/data` 以外的目录作为数据目录，你应该将 `postmaster` 命令行中的目录替换为你正在使用的目录。

> 提示
> 默认情况下，Fedora 将 PostgreSQL 数据目录设置为 `/var/lib/postgresql/data`。然而，这不是存储数据的好地方，因为大多数人的 /var 分区没有足够的空间进行存储。请注意，如果你将数据目录更改为其他（在本节示例的 `/usr/local/postgresql/data`），你需要编辑位于 `/etc/rc.d/init` 的 PostgreSQL 启动文件（名为 `postgres`）以反映更改。

# 在 PostgreSQL 中创建数据库

在 PostgreSQL 中创建数据库非常简单，但必须由具有 PostgreSQL 创建数据库权限的用户执行——例如最初是名为 `postgres` 的用户。你可以直接从 shell 提示符（不是 PSQL 客户端提示符，而是普通的 shell 提示符）使用以下命令：

```
# postgres
-$ createdb database
```

其中 `database` 是你想要创建的数据库名称。

创建的数据库实际上是一个封装，使得无需登录并使用 `psql` 即可轻松创建数据库。不过，你也可以在 `psql` 内部使用 `CREATE DATABASE` 语句创建数据库。例如：

```
CREATE DATABASE database;
```

## 第 22 章 管理数据库服务

在启动 `psql` 客户端程序之前，你至少需要创建一个数据库。你应该在以 `postgres` 用户登录时创建此数据库。要以此该用户登录，你需要使用 `su` 切换到 root 用户，然后使用 `su` 切换到 `postgres` 用户。要连接到新数据库，你需要将新数据库名称作为命令行参数启动 `psql` 客户端程序，例如：

```
$ psql sampledata
```

如果你在调用 `psql` 时没有指定数据库名称，该命令将连接到与调用 `psql` 的用户名同名的数据库（即默认数据库）。

### 在 PostgreSQL 中创建数据库用户

要创建数据库用户，你需从 Linux root 账户开始，使用 `su` 切换到 `postgres` 用户。然后，你可以使用 PostgreSQL 的 `createuser` 命令快速创建一个允许访问数据库或创建新数据库用户的用户，如下所示：

```
$ createuser phusion

是否允许新用户创建数据库？(y/n) y

是否允许新用户创建更多新用户？(y/n) y

CREATE USER
```

在这个示例中，创建了新用户 `phusion`，并允许其创建新数据库和数据库用户（你应该仔细考虑谁有权创建新数据库或额外用户）。

你也可以使用 PostgreSQL 命令行客户端通过输入 `psql` 加上数据库名称来创建新用户，然后使用 `CREATE USER` 命令来创建新用户。这是一个示例：

```
CREATE USER foobar ;
```

> 注意
> PostgreSQL 允许你省略语句中的 `WITH PASSWORD` 部分。然而，这样做会导致创建的用户没有密码。这是一个安全漏洞，因此在创建用户时，你应该始终使用 `WITH PASSWORD` 选项。

> 注意
> 当你完成在 `psql` 命令行客户端中的工作时，可以输入 `\q` 退出并返回到 shell 提示符。

### 在 PostgreSQL 中删除数据库用户

要删除数据库用户，你使用 `dropuser` 命令配合用户名，这将从默认数据库中移除该用户的访问权限，如下所示：

```
$ $ dropuser msmith

DROP USER
```

你也可以通过 `psql` 登录到数据库，然后使用 `DROP USER` 命令。这是一个示例：

```
# $ psql demodb

欢迎使用 psql，这是 PostgreSQL 交互式终端。
