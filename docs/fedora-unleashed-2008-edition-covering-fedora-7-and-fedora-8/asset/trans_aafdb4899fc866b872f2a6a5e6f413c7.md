
对数据库执行一些极其复杂的操作。此外，使用 SQL 子查询可以消除由于其他用户对同一数据集执行某些操作而导致在两个操作之间数据发生变更的潜在问题。在本版本的 Fedora 中，PostgreSQL 和 MySQL 均支持子查询。

## 过程化语言和触发器

*过程化语言* 是一种外部编程语言，可用于编写函数和存储过程。这使得你能够执行简单 SQL 不支持的操作。*触发器* 允许你定义一个事件，该事件将调用你编写的外部函数或存储过程。例如，如果使用包含某列意外值或超出范围值的 `INSERT` 语句，触发器可以引发异常。

例如，在 CID 跟踪数据库中，你可以使用触发器来在用户输入无意义数据时引发异常。PostgreSQL 拥有一种名为 PL/pgSQL 的过程化语言。虽然 MySQL 支持有限数量的内置存储过程和触发器，但它没有任何过程化语言。这意味着你无法在 MySQL 中创建自定义存储过程或触发器，尽管通常可以通过富有创意的客户端编程实现相同的效果。

## 配置 MySQL

Fedora 附带了一个免费且稳定的 MySQL 版本。你也可以从网站 http://www.mysql.com/ 获取 MySQL。该软件以源代码、二进制文件和适用于 Linux 的 RPM 格式提供。你可以在安装 Fedora 时选择安装 MySQL，或者稍后使用 `redhat-config-packages` 客户端将软件添加到系统中。有关添加（或移除）软件的详细信息，请参阅第 2 章。

安装 MySQL 后，你需要初始化*授权表*，即访问数据库及数据库内所有表和列数据的权限。你可以以 root 身份运行 `mysql_install_db` 来完成此操作。该命令会初始化授权表并创建一个 MySQL root 用户。

> **注意**
>
> MySQL 数据目录的所有者必须是 MySQL 运行所对应用户（使用 chown 命令更改所有权）。此外，只有该用户才能在此目录上拥有任何权限。（换句话说，使用 chmod 将权限设置为 700。）以其他方式设置数据目录会产生安全漏洞。

运行 `mysql_install_db` 应生成类似于以下内容的输出：

```bash
# mysql_install_db
Preparing db table
Preparing host table
Preparing user table
Preparing func table
Preparing tables_priv table
Preparing columns_priv table
Installing all prepared tables
020916 17:39:05 /usr/libexec/mysqld: Shutdown Complete
...
```

该命令为在系统中使用 MySQL 做准备，并报告有用的信息。下一步是为 MySQL root 用户设置密码，将在以下章节中讨论。

> **注意**
>
> 默认情况下，MySQL root 用户创建时没有密码。这是你必须首先更改的事项之一，因为 MySQL root 用户有权访问数据库的所有方面。下一节解释如何更改该用户的密码。

## 为 MySQL Root 用户设置密码

要为 root MySQL 用户设置密码，你需要以 root MySQL 用户身份连接到 MySQL 服务器；可以使用命令 `mysql -u root` 来完成。该命令使用 MySQL 客户端将你连接到服务器。当出现 MySQL 命令提示符时，发出如下命令为 root 用户设置密码：

```sql
mysql> SET PASSWORD FOR root = PASSWORD('secretword');
```

应将 `secretword` 替换为你希望用作 root 用户密码的内容。你可以使用相同的命令配合其他用户名来设置或更改其他数据库用户的密码。

输入密码后，你可以在命令提示符处键入 `exit` 退出 MySQL 客户端。

## 在 MySQL 中创建数据库

在 MySQL 中，你使用 `CREATE DATABASE` 语句来创建数据库。要创建数据库，你需要通过键入 `mysql -u root -p` 并按 Enter 键连接到服务器。这样做后，你将以 MySQL root 用户身份连接到数据库，并被提示输入密码。输入密码后，你将位于 MySQL 命令提示符处。然后使用 `CREATE DATABASE` 命令。例如，以下命令创建一个名为 `animals` 的数据库：

```bash
# mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 1 to server version: 3.23.58

Type 'help;' or '\h' for help.  Type '\c' to clear the buffer.

mysql> CREATE DATABASE animals;
Query OK, 1 row affected (0.00 sec)
mysql>
```

创建数据库的另一种方法是以 root 用户身份使用 `mysqladmin` 命令，配合 `create` 关键字和新数据库的名称。例如，要创建一个名为 `reptiles` 的新数据库，你可以使用如下命令行：

```bash
# mysqladmin -u root -p create reptiles
```

## 在 MySQL 中授予和撤销权限

你可能希望授予自己一些权限，最终你也很可能会希望将权限授予其他用户。权限（也称为权利）在四个级别上授予和撤销：

- **全局级别**—这些权限允许访问服务器上的任何数据库。
- **数据库级别**—这些权限允许访问数据库中所有表。
- **表级别**—这些权限允许访问数据库中表内的所有列。
- **列级别**—这些权限允许访问数据库表中单个列。

> **注意**
>
> 列出所有可用权限超出了本章的范围。有关更多信息，请参阅 MySQL 文档。

要添加用户帐户，你需要通过键入 `mysql -u root -p` 并按 Enter 键连接到数据库。然后你将作为 root 用户连接，并被提示输入密码。（你已按照上一节的说明为 root 用户设置了密码，对吧？）输入 root 密码后，你将位于 MySQL 命令提示符处。

要授予用户权限，你使用 `GRANT` 语句，其语法如下：

```sql
grant what_to_grant ON where_to_grant TO user_name IDENTIFIED BY `password`;
```

第一个选项 `what_to_grant` 是你授予用户的权限。这些权限通过关键字指定。例如，`ALL` 关键字用于授予指定用户的全局、数据库、表和列级别权限。

第二个选项 `where_to_grant` 指定应授予权限的资源。第三个选项 `user_name` 是你希望授予权限的用户名。最后，第四个选项 `password` 是应分配给该用户的密码。如果这是一个已存在的用户且已有密码，并且你正在修改权限，你可以省略语句中的 `IDENTIFIED BY` 部分。

例如，要将对名为 `sampledata` 的数据库的所有权限授予名为 `foobar` 的用户，你可以使用以下命令：

```sql
GRANT ALL ON animals.* TO foobar IDENTIFIED BY 'secretword';
```

用户 `foobar` 现在可以使用密码 `secretword` 连接到数据库 `sampledata`，并且 `foobar` 拥有该数据库的所有权限，包括创建和销毁表的能力。例如，用户 `foobar` 现在可以登录到服务器（在此示例中使用当前主机名——`shuttle2`），并像这样访问数据库：

```bash
$ mysql -h shuttle2 -u foobar -p animals
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 43 to server version: 3.23.58

Type 'help;' or '\h' for help.  Type '\c' to clear the buffer.

mysql>
```

> **注意**
>
> 有关额外的命令行选项，请参阅本章稍后的"MySQL 命令行客户端”部分。

稍后，如果你需要从 `foobar` 撤销权限，你可以使用 `REVOKE` 语句。例如，以下语句从用户 `foobar` 撤销所有权限：

```sql
REVOKE ALL ON animals FROM foobar;
```

高级数据库管理、权限和安全是非常复杂的主题，超出了本书的范围。请参阅本章末尾的“参考”部分，了解在线文档的链接。你还可以查看 Luke Welling 和 Laura Thompson 由 Sams Publishing 出版的书籍 *PHP and MySQL Development*。

## 配置 PostgreSQL

如果你不想使用 Fedora 附带的 PostgreSQL 版本，最新的 PostgreSQL 二进制文件和源代码可在 http://www.postgresql.org/ 获取。PostgreSQL RPM 以多个文件形式分发。至少，你可能需要 `postgresql`、`postgresql-server` 和 `postgresql-libs` RPM。你应该使用 FTP 目录 ftp://ftp.postgresql.org/pub/ 中的 `README.rpm-dist` 文件来确定是否需要其他软件包。

