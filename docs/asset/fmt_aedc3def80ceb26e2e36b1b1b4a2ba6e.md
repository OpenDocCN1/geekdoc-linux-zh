
```
Query OK, 1 row affected (0.00 sec)
```

## 在 MySQL 中授予和撤销权限

你可能想给自己授予某些权限，最终你还会向其他人授予权限。权限（权利）在四个级别上授予和撤销：

- 全局级（Global level）这些权限允许访问服务器上的任何数据库。
- 数据库级（Database level）这些权限允许访问数据库中的所有表。
- 表级（Table level）这些权限允许访问表中的所有列。
- 列级（Column level）这些权限允许访问数据库表中的单列。

> 注意
> 列出所有可用权限超出了本章的范围。请查看 MySQL 文档获取更多信息。

要添加用户账户，通过输入 `mysql -u root -p` 连接数据库。

要向用户授予权限，使用 `GRANT` 语句，其语法如下：

```
GRANT what_to_GRANT ON where_to_GRANT TO user_name IDENTIFIED BY 'password';
```

第一个选项 `what_to_GRANT` 是你授予用户的权限。这些权限通过关键字指定。例如，`ALL` 关键字用于为指定用户授予全局、数据库、表和列权限。

第二个选项 `where_to_GRANT` 指定了应授予权限的资源。第三个选项 `user_name` 是你想授予权限的用户名。最后，第四个选项 `password` 是应该分配给该用户的密码。如果这是一个已有密码的现有用户且正在修改权限，可以省略语句中的 `IDENTIFIED BY` 部分。

例如，要向名为 `foobar` 的用户授予名为 `sampledata` 的数据库的所有权限，可以使用以下命令：

```
GRANT ALL sampledata.* TO foobar IDENTIFIED BY 'secretword';
```

### 配置 PostgreSQL

用户 `foobar` 现在可以使用密码 `secretword` 连接到 `sampledata` 数据库，并且 `foobar` 拥有该数据库的所有权限，包括创建和删除表的能力。例如，用户 `foobar` 现在可以登录到服务器（在本例中使用当前主机名——`shuttle2`），并像如下所示访问数据库：

```
$ mysql -h shuttle2 -u foobar -p animals
```

输入密码：
欢迎来到 MySQL 视器。命令以 `;` 或 `\` 结束。
您的 MySQL 连接 ID 为 43，服务器版本：3.2.58

输入 `'\help\';` 或 `'\h'` 获取帮助。输入 `'\c'` 清除缓冲区。

```
mysql>
```

> 注意
> 请参阅本章稍后的“MySQL 命令行客户端”章节以获取更多命令行选项。

稍后，如果你需要撤销 `foobar` 的权限，可以使用 `REVOKE` 语句。例如，以下语句将撤销用户 `foobar` 的所有权限：

```
REVOKE ALL ON animals FROM foobar;
```

高级数据库管理、权限和安全是非常复杂的话，超出了本书的范围。请参阅本章末尾的“参考”部分查看在线文档链接。你也可以查看 Luke Welling 和 Laura Thompson 出自 Sams Publishing 出版的书籍《PHP and MySQL Development》。

## 配置 PostgreSQL

如果你不想使用 Fedora 自带的 PostgreSQL 版本，最新的 PostgreSQL 二进制文件和源码可以在可以在 `http://postgresql.org/` 获得。PostgreSQL RPM 以多个文件的形式分发。至少你可能需要 `postgresql`、`postgresql-server` 和 `postgresql-libs` RPM。你应该查看 FTP 目录 `ftp://postgresql.org/pub/` 中的 `README.rpm-dist` 文件，以确定你是否需要任何其他包。

如果你是从 Fedora RPM 文件安装的，系统会自动为你创建一个必要的 `postgres` 用户账户（即一个与运行服务器的用户同名的账户）：

```
$ fgrep postgres /etc/passwd

postgresql:x:26:26:PostgreSQL Server:/var/lib/postgresql:/bin/bash
```

### 第 22 章 数据库服务管理

否则，你需要在安装期间创建一个名为 `postgres` 的用户。该用户不应该具有登录权限，因为只有 root 用户应该能够使用 `su` 切换到该用户，而且没有人会以该用户的身份登录。（请参考第 14 章“管理用户”。）在你添加用户后，你可以使用标准的 `rpm -i` 命令安装你下载的每个 PostgreSQL RPM 进行默认安装。

### 初始化 PostgreSQL 中的数据目录

安装 RPM 之后，你需要初始化数据目录。为了做到，你必须首先创建数据目录，并且必须是 root 用户。以下示例假设数据目录为 `/usr/local/postgresql/data`。

使用 `mkdir` 创建 `/usr/local/postgresql/data` 目录，并更改目录所有权（使用 `chown` 和 `chgrp`），使其属于用户 `postgres`。然后使用 `su` 切换并以 `postgres` 身份执行以下命令：

```
# mkdir /usr/local/postgresql
# chown postgres /usr/local/postgresql
# chgrp postgres /usr/local/postgresql
# su - postgres
bash-2.05bs initdb -D /usr/local/postgresql/data
```

属于该数据库系统的文件将由用户 "postgres" 所有。该用户也必须拥有服务器进程。

数据库集群将使用 locale `en_US.UTF-8` 初始化。此区域设置将防止在模式匹配操作中使用索引。如果这是你的问题，请在将排序顺序设置为 "C" 的情况下重新运行 `initdb`。更多信息请参阅《管理员指南》。

```
creating directory /usr/local/postgresql/data... ok
creating directory /usr/local/postgresql/data/base... ok
creating directory /usr/local/postgresql/data/global... ok
creating directory /usr/local/postgresql/data/pg_xlog... ok
creating directory /usr/local/postgresql/data/pg_clog... ok
creating template1 database in /usr/local/postgresql/data/base/1... ok
creating configuration files... ok
initializing pg_shadow... ok
enabling unlimited row size for system tables... ok
initializing pg_dependew... ok
creating system views... ok
loading pg_description... ok
creating conversions... ok
setting privileges on built-in objects... ok
vacuuming database template1... ok
copying template0... ok
```

### 配置 PostgreSQL 583

成功。你现在可以使用以下命令启动数据库服务器：

```
/usr/bin/postmaster -D /usr/local/postgresql/data
```

或

```
usr/bin/pg_ctl -D /usr/local/postgresql/data -l logfile start
```

这会初始化数据库并将数据目录的权限设置为正确值。

> 注意
> `initdb` 程序将数据目录的权限设置为 700。你不应将这些权限更改为其他任何值以以创建安全漏洞。

你可以使用以下命令启动 `postmaster` 程序（确保你是 `postgres` 用户）：

```
$ postmaster -D /usr/local/postgresql/data &
```
