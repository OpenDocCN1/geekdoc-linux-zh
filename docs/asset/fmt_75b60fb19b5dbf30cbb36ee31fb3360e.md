
最新的 PostgreSQL 二进制文件和源码可在 `http://www.postgresql.org` 获取。PostgreSQL RPM 以多个文件的形式分发。至少你可能需要 `postgresql`、`postgresql-server` 和 `postgresql-libs` RPM。你应该查看 FTP 目录 `ftp://postgresql.org/pub/` 中的 `README.rpm-dist` 文件来确定你是否需要任何包。

如果你是从 Red Linux RPM 文件安装，系统将自动为你创建一个 `postgres` 用户账户（即在你的系统上运行服务器的用户名的账户）：

```
$ fgrep postgres /etc/passwd
postgresql:x:26:26:PostgreSQL Server:/var/lib/postgresql:/bin/bash
```

否则，你需要在安装期间创建一个 `postgres` 用户。此用户不应具有登录权限，因为只有 root 能够使用 `su` 变成该用户，且没有人会直接登录该用户。（有关如何向 Red Hat Linux 系统添加用户的更多信息，请参阅第 9 章）。在你下载了的每个 PostgreSQL RPM 后，使用标准的 `rpm -i` 命令进行默认安装。

## 在 PostgreSQL 中初始化数据目录

安装 RPM 之后，你需要初始化数据目录。要做到这一点，必须首先创建数据目录，以下示例假设数据目录为 `/usr/local/postgresql/data`。

# 第 17 章 在 Red Hat Linux 中管理数据库服务

创建 `/usr/local/postgresql/data` 目录（使用 `mkdir`）并更改目录所有权（使用 `chown` 和 `chgrp`），使其所有者为 `postgres` 用户。然后使用 `su` 切换到 `postgres` 用户，执行以下命令：

```
# mkdir /usr/local/postgresql
# chown postgres /usr/local/postgresql
# chgrp postgres /usr/local/postgresql
# su - postgres
-bash:2.05$ initdb -D /usr/local/postgresql/data
```

属于该数据库系统的文件将由用户 `postgres` 所有。该用户也必须拥有服务器进程。

```
creating directory /usr/local/postgresql/data. ok
creating directory /usr/local/postgresql/data/base. ok
creating directory /usr/local/postgresql/data/global. ok
creating directory /usr/local/postgresql/data/pg_xlog. ok
creating directory /usr/local/postgresql/data/pg_clog. ok
creating template database in /usr/local/postgresql/data/base/1. ok
creating configuration files. ok
initializing pg_shadow. ok
enabling unlimited row size for system tables. ok
creating system views. ok
loading pg_description. ok
vacuuming database template1. ok
copying template1 to template0. ok
```

成功。你现在可以使用以下命令启动数据库服务器：

```
/usr/bin/postmaster -D /usr/local/postgresql/data
or
/usr/bin/pg_ctl -D /usr/local/postgresql/data -1 logfile start
```

这将初始化数据库并将数据目录的权限设置为其默认值。

> 注意事项
>
> `initdb` 程序将数据目录的权限设置为 700。你不应将这些权限更改为其他任何值，以避免产生安全漏洞。

你可以使用以下命令启动 `postmaster` 程序（确保你当前是 `postgres` 用户）：

```
$ postmaster -D /usr/local/postgresql/data &
```

如果你决定使用 `/usr/local/postgresql/data` 以外的目录作为数据目录，则应将 `postmaster` 命令行中的目录替换为你正在使用的任何目录。

> 默认情况下，Red Hat Linux 将 PostgreSQL 数据目录设置为 `/var/lib/postgresql/data`。然而，这并不是存储数据的好地方，因为大多数人在 `/var` 分区中没有足够的空间来存储任何种重要数据。请注意，如果你将目录更改为其他内容（例如本节示例所示的 `/usr/local/postgresql/data`），你需要编辑位于 `/etc/rc.d/init.d` 的 PostgreSQL 启动文件以反映该更改。

## 在 PostgreSQL 中创建数据库

在 PostgreSQL 中创建数据库非常简单，但必须由具有在 PostgreSQL 中创建数据库权限的用户执行——例如，最初的名为 `postgres` 的用户。你可以直接从 shell 提示符执行以下命令（注意不是 PSQL 客户端提示符，而是普通的 Red Hat Linux shell 提示符）：

```
# su postgres
bash-2.05b$ createdb database
```

其中 `database` 是你想要创建的数据库名称。

`createdb` 程序实际上是一个包装器，可以更容易创建数据库，而无需登录并使用 `psql`。不过，你也可以在 `psql` 中使用 `CREATE DATABASE` 语句创建数据库。以下是一个示例：

```
CREATE DATABASE database;
```

在启动 `psql` 客户端程序之前，你至少需要创建一个数据库。你应该在以 `postgres` 用户登录时创建此数据库。要登录此用户，你需要先成为 `root`，然后使用 `su` 切换到 `postgres` 用户。要连接到新数据库，你需要将新数据库名称作为命令行参数启动 `psql` 客户端程序，如下：

```
$ psql sampledat
```

## 在 PostgreSQL 中创建数据库用户

要创建数据库用户，你使用 `su` 从 Red Hat root 账户切换到 `postgres` 用户。然后你可以使用 PostgreSQL 的 `createuser` 命令快速创建一个允许访问数据库或创建新用户的用户，如下：

```
$ createuser bball
Shall the new user be allowed to create databases? (y/n) y
Shall the new user be allowed to create more new users? (y/n) y
```

名为 `bball` 的新用户被允许访问数据库并创建新用户。你也可以在 `psql` 中使用 `CREATE DATABASE` 语句创建数据库。以下是一个示例：

```
CREATE DATABASE database;
```

在启动 `psql` 客户端程序之前，你至少需要创建一个数据库。你应该在以 `postgres` 用户登录时创建此数据库。要登录此用户，你需要先成为 `root`，然后使用 `su` 切换到 `postgres` 用户。要连接到新数据库，你需要将新数据库名称作为命令行参数启动 `psql` 客户端程序，如下：

```
$ psql sampledat
```

> 注意事项
>
> `initdb` 程序将数据目录的权限设置为 700。你不应将这些权限更改为其他任何值，以避免产生安全漏洞。

## 在 PostgreSQL 中创建数据库用户

要创建数据库用户，你使用 `su` 从 Red Hat root 账户切换到 `postgres` 用户。然后你可以使用 PostgreSQL 的 `createuser` 命令快速创建一个允许访问数据库或创建新用户的用户，如下：

```
$ createuser bball
Shall the new user be allowed to create databases? (y/n) y
Shall the new user be allowed to create more new users? (y/n) y
```

名为 `bball` 的新用户被允许访问数据库并创建新用户。你也可以在 `psql` 中使用 `CREATE DATABASE` 语句创建数据库。以下是一个示例：

```
CREATE DATABASE database;
```
