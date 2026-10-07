

# 第 17 章在 Red Hat Linux 中管理数据库服务

创建 `/usr/local/postgresql/data` 目录（使用 `mkdir`）并更改目录所有权（使用 `chown` 和 `chgrp`），使其所有者为 `postgres` 用户。然后使用 `su` 切换到 `postgres` 用户，执行以下命令：

```
# mkdir /usr/local/postgresql
# chown postgres /usr/local/postgresql
# chgrp postgres /usr/local/postgresql
# su - postgres
-bash:2.05$ initdb -D /usr/local/postgresql/data
```

属于该数据库系统的文件将由用户 "postgres" 所有。该用户也必须拥有服务器进程。

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
> `initdb` 程序将数据目录的权限设置为 700。你不应将这些权限更改为其他任何值，以避免产生安全漏洞。

你可以使用以下命令启动 `postmaster` 程序（确保你当前是 `postgres` 用户）：

```
$ postmaster -D /usr/local/postgresql/data &
```

如果你决定使用 `/usr/local/postgresql/data` 以外的目录作为数据目录，则应将 `postmaster` 命令行中的目录替换为你正在使用的任何目录。

> 默认情况下，Red Hat Linux 将 PostgreSQL 数据目录设置为 `/var/lib/postgresql/data`。然而，这并不是存储数据的好地方，因为大多数人在 `/var` 分区中没有足够的空间来存储任何种重要数据。请注意，如果你将目录更改为其他内容（例如本节示例所示的 `/usr/local/postgresql/data`），你需要编辑位于 `/etc/rc.d/init.d` 的 PostgreSQL 启动文件以反映该更改。

# 在 PostgreSQL 中创建数据库

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

# 在 PostgreSQL 中创建数据库用户

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
> `initdb` 程序将数据目录的权限设置为 700。你不应将这些权限更改为其他任何值，以避免产生安全漏洞。

# 在 PostgreSQL 中创建数据库用户

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

# 在 PostgreSQL 中删除数据库用户

要删除数据库用户，你使用 `dropuser` 命令。当你需要移除用户时这非常有用。例如：

```
$ dropuser bball
```

# 在 PostgreSQL 中授予和撤销权限

与 MySQL 类似，PostgreSQL 中的授予和撤销权限是通过 `GRANT` 和 `REVOKE` 语句完成的。以下是授予权限的示例：

```
GRANT ALL PRIVILEGES ON database TO bball;
```

以下是撤销权限的示例：

```
REVOKE ALL PRIVILEGES ON database FROM bball;
```

# 数据库客户端

MySQL 和 PostgreSQL 使用客户端/服务器系统。简单来说，数据库服务器处理请求，而客户端处理输出。MySQL 和 PostgreSQL 都使用命令行客户端。命令行客户端是一种交互的原始方式，通常不被终端用户使用。然而，作为 DBA，你使用命令行客户端交互式地测试查询，而无需编写前端程序。在本章的后续章节中，你将了解一些图形客户端和 Web 界面。

以下章节将检查访问远程数据库的两种常用方法、本地访问数据库服务器的方法以及 Web 访问的概念。

> 注意
> 在设置数据库时，你应该考虑访问和权限问题。用户是否应该能够创建和删除数据库？还是只能使用现有数据库？用户是否能够向数据库添加记录并修改现有记录？用户是否被限于只读访问？其他世界如何？公众是否需要通过互联网访问你的数据库？作为 DBA，你必须确定这些问题的答案。

# 通过 SSH 访问数据库

本节将简要讨论两种远程数据库访问场景。在第一种场景中，用户通过 SSH 直接登录数据库服务器（利用加密会话的安全优势），然后在服务器上启动程序来访问数据库。在这种情况下，如图 17.4 所示，数据库客户端运行在数据库服务器本身。

![](img/446debe023486a07fde575245cf7a3ff_609_0.png)

图 17.4 用户从工作站（主机 cheetah）登录到位于主机 simba 的数据库服务器。数据库客户端运行在 simba 上。

在另一种场景中，如图 17.5 所示，用户通过 SSH 登录远程主机并启动程序访问数据库，但数据库实际上运行在另一个系统上。现在涉及三个系统——用户的工作站、运行数据库客户端的远程主机以及运行数据库服务器的远程主机。

