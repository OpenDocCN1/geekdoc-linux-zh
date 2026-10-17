
例如，在 CD 跟踪数据库中，如果用户输入了不合逻辑的数据，你可以使用触发器来引发异常。PostgreSQL 有一种名为 PL/pgSQL 的过程语言。虽然 MySQL 支持内置过程和触发器的数量有限制，但它没有任何过程语言。这意味着你不能在 MySQL 中创建自定义过程或触发器，尽管可以通过创性的客户端编程来实现相同的效果。

## 配置 MySQL

Ubuntu 包含一个免费且稳定的 MySQL 版本。MySQL 也可以从 `http://www.mysql.com` 网站获取。该软件提供源代码、二进制和适用于 Linux 的 APT 格式。你可以使用 Synapt 客户端将软件添加到你的系统中。添加（删除）软件的详细信息请参阅第 7 章。

安装 MySQL 后，你需要初始化权限表或权限，以访问数据库中的任何或所有数据库、表以及列数据。你可以通过以 root 身份执行 `mysql_install_db` 来实现。该命令会初始化权限表并创建一个 MySQL root 用户。

## 注意

MySQL 数据目录需要由运行 MySQL 的用户拥有（使用 `chown` 命令更改所有者）。此外，只有此用户应该拥有此目录的任何权限。换句话说，应该使用 `chmod` 将权限设置为 `700`。任何其他方式设置数据目录都会产生安全漏洞。

运行 `mysql_install_db` 产生类似于下面的输出：

```
sudo mysql_install_db
Preparing db table
Preparing host table
Preparing user table
Preparing func table
Preparing tables_priv table
Preparing columns_priv table
Installing all prepared tables
020916 17:39:05 /usr/lib/mysql: Shutdown Complete
```

该命令为 MySQL 使用做了准备并报告了有用信息。下一步是为 root 用户设置密码。

## 注意

默认情况下，MySQL root 用户没有密码。这是你必须修改的内容之一。

## 为 root 用户设置密码

要为 root 用户设置密码，你需要以 root 用户身份连接服务器；使用 MySQL 客户端。当你拥有 MySQL 提示符时，执行如下命令：

```
mysql> SET PASSWORD FOR 'root' = PASSWORD('secretword');
```

将 `secretword` 替换为你密码。你可以对其他用户名使用相同的命令来设置密码。

## 在 MySQL 中创建数据库

在 MySQL 中，你使用 `CREATE DATABASE` 语句创建数据库。要创建数据库，通过输入 `mysql -u -p` 连接服务器。之后，你将以 root 用户身份连接数据库并被提示密码。输入密码后，你将进入 MySQL 提示符。然后使用 CREATE DATABASE 命令。例如，以下命令创建一个名为 `animals` 的数据库：

```
sudo mysql -u -p
Enter password:
Welcome to the MySQL monitor.
Your MySQL connection id is 1 to server version: 3.23.58

Type 'help/' or '\h' for help. Type '\c' to clear the buffer.

mysql> CREATE DATABASE animals;
Query OK, 1 row affected (0.00 sec)
mysql>
```

另一种创建数据库的方法是以 root 用户身份使用 `mysqladmin` 命令，配合 `create` 关键字和新数据库名称。例如，创建一个名为 `reptiles` 的数据库如下命令行：

```
# mysqladmin -u root -p create reptiles
```

## 在 MySQL 中授予和撤销权限

你可能想要给自己授予一些权限，最终你可能还会向其他用户授予权限。权限（称为权利）在四个级别上授予和撤销：

- 全局级（Global-level）——这些权限允许访问服务器上的任何数据库。
- 数据库级（Database-level）——这些权限允许访问数据库中的所有表。
- 表级（Table-level）——这些权限允许访问数据库表中的所有列。
- 列级（Column-level）——这些权限允许访问数据库表中的单个列。

注意 列出所有可用权限超出了本章范围。请参阅 MySQL 文档获取更多信息。

## 配置 MySQL

要添加用户账户，您可以通过输入 `mysql -u root -p` 并按回车来连接数据库。随后您将以 root 用户身份连接，并提示输入密码（如果你像上一节中那样为 root 用户设置了密码，对吧？）。输入 root 密码后，您将进入 MySQL 提示符。

要向用户授予权限，请使用 `GRANT` 语句，其语法如下：

```sql
GRANT what_to_grant ON where_to_grant TO user_name IDENTIFIED BY 'password';
```

第一个选项 `what_to_grant` 是您要授予用户的权限。这些权限通过关键字指定。例如，`ALL` 关键字用于为指定用户授予全局、数据库、表和列级权限。

第二个选项 `where_to_grant` 指定了应授予权限的资源。第三个选项 `user_name` 是您想要授予权限的用户名。最后，第四个选项 `password` 是应分配给该用户的密码。如果该用户是已有密码的存在用户且您正在修改权限，则可以省略语句中的 `IDENTIFIED BY` 部分。

例如，要向名为 `sampledata` 的数据库授予名为 `foobar` 的用户所有权限，可以使用以下命令：

```sql
GRANT ALL ON sampledata.* TO foobar IDENTIFIED BY 'secretword';
```

用户 `foobar` 现在可以使用密码 `secretword` 连接到 `sampledata` 数据库，并且 `foobar` 拥有该数据库的所有权限，包括创建和删除表的能力。例如，用户 `foobar` 现在可以登录服务器（在本例中使用当前的主机名 `shuttle2`），并如下所示访问数据库：

```bash
$ mysql -h shuttle2 -u foobar -p animals
```

```
Enter password:
Welcome to the MySQL monitor. Commands end with ; or \
Your MySQL connection id is 43 to server version: 3.23
```

```sql
Type 'help'; or '\h' for help. Type '\c' to clear the buffer.
mysql>
```

> 注意
> 请参阅“MySQL 命令行客户端”章节以获取额外的命令行选项。

以后，如果您需要撤销 `foobar` 的权限，可以使用 `REVOKE` 语句。例如，以下语句将从用户 `foobar` 撤销所有权限：

```sql
REVOKE ALL ON ANIMALS FROM foobar;
```

## 第 21 章 管理数据库服务

高级数据库管理、权限和安全是非常复杂的话题，超出了本书的涵盖范围。请查看本章末尾的“参考”章节以获取在线文档链接。您还可以查看 Sams Publishing 出版的 Luke W 和 Laura Thompson 编写的《PHP and MySQL Development》一书。

## 配置 PostgreSQL

如果您不想使用 Ubuntu 自带的 PostgreSQL 版本，可以在 `http://www.postgresql.org` 获取最新的 PostgreSQL 二进制文件和源码。PostgreSQL 软件包以多个文件的形式分发。至少，您可能需要 `postgres`、`postgres-server` 和 `postgres-libs` 软件包。您应该查看 FTP 目录 `ftp://ftp.postgresql.org/pub/` 下的 `README` 文件，以确定是否还需要任何其他包。

如果您是从 Ubuntu 软件包进行安装的，系统会自动为您创建一个必要的 `postgres` 用户账户（即与在系统中运行服务器的用户同名的账户）：

```bash
$ fgrep postgres /etc/passwd
postgres:x:26:26:0:/var/lib/postgresql:/bin/bash
```
