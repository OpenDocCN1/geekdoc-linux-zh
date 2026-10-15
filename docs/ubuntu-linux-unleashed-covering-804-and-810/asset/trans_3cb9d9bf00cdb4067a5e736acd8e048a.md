

## 过程化语言和触发器

过程化语言是一种外部编程语言，可用于编写函数和过程。这使你能够执行简单 SQL 不支持的操作。触发器允许你定义一个事件，该事件将调用你编写的外部函数或过程。例如，触发器可用于在包含列的意外或超出范围值的 INSERT 语句时引发异常。

例如，在 CD 跟踪数据库中，你可以使用触发器在用户输入不合理数据时引发异常。PostgreSQL 有一种名为 PL/pgSQL 的过程化语言。尽管 MySQL 支持有限数量的内置过程和触发器，但它没有任何过程化语言。这意味着你无法在 MySQL 中创建自定义过程或触发器，尽管通常可以通过创造性的客户端编程实现相同的效果。

## 配置 MySQL

Ubuntu 自带一个免费且稳定的 MySQL 版本。MySQL 也可从网站 http://www.mysql.com 获取。软件以源代码、二进制和 Linux 的 APT 格式提供。你可以使用 Synaptic 客户端将软件添加到你的系统。有关添加（或删除）软件的详细信息，请参阅第 7 章。

在安装 MySQL 后，你需要初始化授权表或权限，以便访问任何或所有数据库以及数据库中的表和列数据。你可以通过以 root 身份发出 mysql_install_db 来执行此操作。此命令初始化授权表并创建 MySQL root 用户。

> **警告**
> 
> MySQL 数据目录需要由 MySQL 将要运行的用户拥有（使用 chown 命令更改所有权）。此外，只有此用户应对此目录具有任何权限。（换句话说，权限应使用 chmod 设置为 700。）以其他方式设置数据目录会造成安全漏洞。

运行 mysql_install_db 应生成类似以下内容的输出：

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
```

该命令为系统上的 MySQL 做准备并报告有用的信息。下一步是为 MySQL root 用户设置密码，这将在下一节中讨论。

## 警告

默认情况下，MySQL root 用户是无密码创建的。这是你必须首先更改的事情之一，因为 MySQL root 用户可以访问数据库的所有方面。以下部分解释了如何更改该用户的密码。

## 为 MySQL Root 用户设置密码

要为 root MySQL 用户设置密码，你需要以 root MySQL 用户身份连接到 MySQL 服务器；你可以使用命令 mysql -u root 来执行此操作。此命令使用 MySQL 客户端将你连接到服务器。当你获得 MySQL 命令提示符时，发出如下命令为 root 用户设置密码：

```
mysql> SET PASSWORD FOR root = PASSWORD('secretword');
```

secretword 应替换为你希望 root 用户的密码。你可以使用此相同命令为其他用户名设置或更改其他数据库用户的密码。

在输入密码后，你可以通过在命令提示符下键入 exit 来退出 MySQL 客户端。

## 在 MySQL 中创建数据库

在 MySQL 中，你使用 CREATE DATABASE 语句创建数据库。要创建数据库，请键入 mysql -u root -p 并按 Enter 连接到服务器。之后，你将以 MySQL root 用户身份连接到数据库并被提示输入密码。输入密码后，你将被置于 MySQL 命令提示符。然后你使用 CREATE DATABASE 命令。例如，以下命令创建一个名为 animals 的数据库：

```
sudo mysql -u root -p
Enter password:
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 1 to server version: 3.23.58

Type 'help;' or '\h' for help. Type '\c' to clear the buffer.

mysql> CREATE DATABASE animals;
Query OK, 1 row affected (0.00 sec)
mysql>
```

