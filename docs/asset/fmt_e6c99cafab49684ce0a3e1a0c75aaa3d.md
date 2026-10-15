
### Atomicity
这意味着几个数据库操作被视为一个不可分割（原子）单元，通常称为事务。在事务中，要么所有单元操作都被执行，要么都不执行。换句话说，如果原子单元中的任何操作失败，则整个原子单元将被取消。

### Consistency
确保没有任何事务会导致数据库处于不一致状态。不一致状态可能由数据库客户端崩溃、网络故障和类似情况引起。一致性确保在这种情况下，任何会导致数据库处于不一致状态的事务或部分完成的事务都会被回滚，或撤销。

### Isolation
确保对同一数据进行操作的多个事务彼此完全隔离。这可以防止两个用户同时尝试写入同一记录时导致数据损坏。隔离的处理方式通常可以由数据库程序员配置。隔离处理的一种方式是通过锁定，如前所述。

### Durability
确保一旦事务已提交到数据库，即使系统崩溃、网络故障或其他问题发生，也不会丢失。这通常通过事务日志实现。持久性意味着，例如，如果服务器崩溃，数据库在重新启动时可以检查日志，并将尚未完成的事务提交到数据库中。

`PostgreSQL` 是 ACID 兼容的，但 MySQL 又一次让你可以选择使用 ACID 兼容的表或不使用。`MyISAM` 表不是 ACID 兼容的，而 `InnoDB` 表是。注意，ACID 兼容性并非易事：所有额外的预防措施都会带来性能开销。

## SQL 子查询

子查询允许你将多个操作组合成一个原子单元，并使这些操作能够访问彼此的数据。通过使用 SQL 子查询，你可以在数据库上执行极其复杂的操作。此外，使用 SQL 子查询消除了数据在两次操作之间因另一用户对同一数据集执行操作而发生变化的潜在问题。`PostgreSQL` 和 `MySQL` 在 Ubuntu 的此版本中都支持子查询，但在早期版本中并非如此。

## 过程语言和触发器

过程语言是一种外部编程语言，可用于编写函数和过程。这使你能够执行简单 SQL 不支持的操作。触发器允许你定义一个事件，该事件将调用你编写的外部函数或过程。例如，可以使用触发器在包含列的意外或超出范围的值的 `INSERT` 语句被给出时引发异常。

例如，在 CD 跟踪数据库中，你可以使用触发器在用户输入不合理的数据时引发异常。`PostgreSQL` 有一种名为 `PL/pgSQL` 的过程语言。尽管 `MySQL` 支持有限数量的内置过程和触发器，但它没有任何过程语言。这意味着你无法在 `MySQL` 中创建自定义过程或触发器，尽管通常可以通过创造性的客户端编程实现相同的效果。

## 配置 MySQL

Ubuntu 附带了一个免费且稳定的 `MySQL` 版本。`MySQL` 也可在网站 `http://www.mysql.com` 上获得。该软件以源代码、二进制和 APT 格式提供给 Linux。你可以使用 `Synaptic` 客户端将软件添加到你的系统。有关添加（或删除）软件的详细信息，请参阅第 7 章。

在安装 `MySQL` 后，你需要初始化授权表或权限以访问任何或所有数据库以及数据库中的表和列数据。你可以通过以 root 身份发出 `mysql_install_db` 来执行此操作。此命令初始化授权表并创建 `MySQL` root 用户。

> **CAUTION**
>
> `MySQL` 数据目录需要由 `MySQL` 将要运行的用户拥有（使用 `chown` 命令更改所有权）。此外，只有该用户应对此目录具有任何权限。（换句话说，权限应使用 `chmod` 设置为 `700`。）以任何其他方式设置数据目录都会造成安全漏洞。

运行 `mysql_install_db` 应生成类似以下内容的输出：

```
sudo mysql_install_db
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

该命令为系统上的 `MySQL` 做准备并报告有用的信息。下一步是为 `MySQL` root 用户设置密码，这将在下一节中讨论。

> **CAUTION**
>
> 默认情况下，`MySQL` root 用户是创建时没有密码的。这是你必须首先更改的事情之一，因为 `MySQL` root 用户可以访问数据库的所有方面。以下部分解释了如何更改该用户的密码。

## 为 MySQL Root 用户设置密码

要为 root `MySQL` 用户设置密码，你需要以 root `MySQL` 用户身份连接到 `MySQL` 服务器；你可以使用命令 `mysql -u root` 来执行此操作。此命令使用 `MySQL` 客户端将你连接到服务器。当你拥有 `MySQL` 命令提示符时，发出类似以下命令来为 root 用户设置密码：

```
mysql> SET PASSWORD FOR root = PASSWORD('secretword');
```

`secretword` 应替换为你希望 root 用户的密码。你可以使用此相同命令为其他用户名设置或更改其他数据库用户的密码。

在输入密码后，你可以通过在命令提示符下键入 `exit` 来退出 `MySQL` 客户端。

## 在 MySQL 中创建数据库

在 `MySQL` 中，你使用 `CREATE DATABASE` 语句来创建数据库。要创建数据库，请键入 `mysql -u root -p` 并按 Enter 连接到服务器。完成后，你将以 `MySQL` root 用户身份连接到数据库并被提示输入密码。输入密码后，你将被置于 `MySQL` 命令提示符下。然后你使用 `CREATE DATABASE` 命令。例如，以下命令创建一个名为 `animals` 的数据库：

```
sudo mysql -u root -p
Enter password:
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 1 to server version: 3.23.58
Type 'help;' or '\h' for help. Type '\c' to clear the buffer.
```

```
mysql> CREATE DATABASE animals;
Query OK, 1 row affected (0.00 sec)
mysql>
```

另一种创建数据库的方法是作为 root 用户使用 `mysqladmin` 命令，使用 `create` 关键字和新数据库的名称。例如，要创建一个名为 `reptiles` 的新数据库，你可以使用如下命令行：

```
# mysqladmin -u root -p create reptiles
```

## 在 MySQL 中授予和撤销权限

你可能希望为自己授予一些权限，最终你可能还希望为其他用户授予权限。权限，也称为权利，在四个级别上授予和撤销：

- Global-level—这些权利允许访问服务器上的任何数据库。
- Database-level—这些权利允许访问数据库中的所有表。
- Table-level—这些权利允许访问数据库中表中所有列。
- Column-level—这些权利允许访问数据库表中单个列。

> **NOTE**
>
> 列出所有可用权限超出了本章的范围。有关更多信息，请参阅 `MySQL` 文档。

要添加用户账户，请键入 `mysql -u root -p` 并按 Enter 连接到数据库。然后你将以 root 用户身份连接并被提示输入密码。输入 root 密码后，你将被置于 `MySQL` 命令提示符下。

要向用户授予权限，你使用 `GRANT` 语句，其语法如下：

```
grant what_to_grant ON where_to_grant TO user_name IDENTIFIED BY 'password';
```

第一个选项，`*what_to_grant*`，是你授予用户的权限。这些权限使用关键字指定。例如，`ALL` 关键字用于授予指定用户的全局、数据库、表和列级权利。

第二个选项，`*where_to_grant*`，指定应授予权限的资源。第三个选项，`*user_name*`，是你想要授予权限的用户名。最后，第四个选项，`*password*`，是应分配给此用户的密码。如果这是已有用户且已拥有密码并且你正在修改权限，则可以省略语句中的 `IDENTIFIED BY` 部分。

例如，要向名为 `foobar` 的用户授予名为 `sampledata` 的数据库的所有权限，你可以使用以下命令：

```
GRANT ALL ON animals.* TO foobar IDENTIFIED BY 'secrettword';
```

用户 `foobar` 现在可以使用密码 `secrettword` 连接到数据库 `sampledata`，并且 `foobar` 在数据库上拥有所有权限，包括创建和销毁表的权限。例如，用户 `foobar` 现在可以登录到服务器（使用当前主机名——本例中为 `shuttle2`），并像这样访问数据库：
