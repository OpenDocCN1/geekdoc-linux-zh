

高级数据库管理、权限和安全是非常复杂的主题，超出了本书的范围。有关在线文档的链接，请参阅本章末尾的“Reference”部分。你也可以查阅 Luke Welling 和 Laura Thompson 所著的 Sams Publishing 出版的《PHP and MySQL Development》一书。

## Configuring PostgreSQL

如果你不想使用 Ubuntu 捆绑的 PostgreSQL 版本，最新版的 PostgreSQL 二进制文件和源代码可在 http://www.postgresql.org 获取。PostgreSQL 软件包以多个文件形式分发。至少，你可能需要 postgresql、postgresql-server 和 postgresql-libs 软件包。你应该查看 FTP 目录 ftp://ftp.postgresql.org/pub/ 中的 README 文件，以确定是否需要其他软件包。

如果你是从 Ubuntu 软件包文件安装，一个必要的 postgres 用户账户（即在你的系统上运行服务器的用户的账户）会自动为你创建：

```
$ fgrep postgres /etc/passwd
postgres:x:26:26:PostgreSQL Server:/var/lib/pgsql:/bin/bash
```

否则，你需要在安装期间创建一个名为 postgres 的用户。该用户不应具有登录权限，因为只有 root 才能 su 成为该用户，并且不会有人直接以该用户登录。（有关如何在 Ubuntu 系统上添加用户的信息，请参阅第 10 章“管理用户”。）在添加用户后，你可以使用标准的 dpkg -i 命令以默认方式安装下载的每个 PostgreSQL 软件包。

## Initializing the Data Directory in PostgreSQL

安装软件包后，你需要初始化数据目录。为此，你必须先创建数据目录，并且必须是 root 用户。以下示例假设数据目录为 /usr/local/pgsql/data。

创建 /usr/local/pgsql/data 目录（使用 mkdir）并更改目录的所有权（使用 chown 和 chgrp），使其归用户 postgres 所有。然后使用 su 并以用户 postgres 的身份发出以下命令：

```
# mkdir /usr/local/pgsql
# chown postgres /usr/local/pgsql
# chgrp postgres /usr/local/pgsql
# su - postgres
-bash-2.05b$ initdb -D /usr/local/pgsql/data
```

此数据库系统所属的文件将由用户 "postgres" 拥有。该用户还必须拥有服务器进程。

数据库集群将使用 locale en_US.UTF-8 初始化。此区域设置将阻止对模式匹配操作使用索引。如果这是一个问题，请使用排序顺序设置为 "C" 重新运行 initdb。有关更多信息，请参阅管理员指南。

```
creating directory /usr/local/pgsql/data... ok
creating directory /usr/local/pgsql/data/base... ok
creating directory /usr/local/pgsql/data/global... ok
creating directory /usr/local/pgsql/data/pg_xlog... ok
creating directory /usr/local/pgsql/data/pg_clog... ok
creating template1 database in /usr/local/pgsql/data/base/1... ok
creating configuration files... ok
initializing pg_shadow... ok
enabling unlimited row size for system tables... ok
initializing pg_depend... ok
creating system views... ok
loading pg_description... ok
creating conversions... ok
setting privileges on built-in objects... ok
vacuuming database template1... ok
copying template1 to template0... ok
```

成功。你现在可以使用以下命令启动数据库服务器：

```
/usr/bin/postmaster -D /usr/local/pgsql/data
or
/usr/bin/pg_ctl -D /usr/local/pgsql/data -l logfile start
```

这将初始化数据库并将数据目录的权限设置为正确的值。

## CAUTION

> initdb 程序将数据目录的权限设置为 700。你不应将这些权限更改为其他任何值，以免造成安全漏洞。

你可以使用以下命令启动 postmaster 程序（确保你仍然是用户 postgres）：

```
$ postmaster -D /usr/local/pgsql/data &
```

如果你决定使用除 /usr/local/pgsql/data 以外的目录作为数据目录，你应该将 postmaster 命令行中的目录替换为你正在使用的目录。

