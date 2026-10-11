
我们已经通过 SSH 在你的远程树莓派 Spy Pi 上拍摄了你的第一张照片，文件名为 `firstpicture.jpg`！

有关关于使用 RPi 摄像头软件工具的更多详情，请参阅：https://www.raspberry.com/documentation/computers/camera_software.html#rpicam-jpeg。
欢迎进一步探索这件多能武器。

## 从 MySQL/MariaDB 中提取信息

`MySQL` 是数据库驱动型 Web 应用程序最广泛使用的数据库。在现代 Web 技术时代，几乎每个网站都是由数据库驱动的，这意味着 `MySQL` 或另一个名为 `MariaDB` 的开源数据库存储了大多数网站的数据。

数据库是黑客的“金金羊毛”。它们包含了关于用户的关键信息以及如信用卡号等机密信息。出于这个原因，黑客通常针对数据库。

与 Linux 类似，`MySQL` 和 `MariaDB` 都是开源的并根据 `GPL`（GNU 公共许可证）授权，你会在几乎每个 Linux 发行版中找到预装的其中至少一个。

由于其免费、开源且强大的特性，`MySQL` 和 `MariaDB` 已成为许多 Web 应用的首选数据库，包括 `WordPress`、`Facebook`、`LinkedIn`、`X`（原 Twitter）、`Kayak`、`Walmart.com`、`Wikipedia` 和 `YouTube` 等热门网站。其他流行的内容管理系统（CMS）如 `Joomla`、`Drupal` 和 `Ruby on Rails` 也都使用 `MySQL`。你明白意思了。如果你想开发或攻击 Web 应用的后端，你应该了解一点 `MySQL`。

在接下来的章节中，我将假设你正在使用 `MySQL`，尽管这些命令对 `MariaDB` 或 `MySQL` 都有效；输出会略有不同。让我们开始吧。

## MySQL 的过去与未来

`MySQL` 最初于 1995 年由瑞典的 `MySQL AB` 开发，随后于 2008 年被 `Sun Microsystems` 收购，后者又于 2009 年被 `Oracle` 收购，因此 `MySQL` 现在归 `Oracle` 所有。`Oracle` 是全球最大的数据库软件发行商，因此开源社区对 `Oracle` 保持 `MySQL` 开源的承诺持有重大疑虑。结果是现在有一个名为“Maria”的 `MySQL` 数据库软件分支（fork），它致力于保持该软件及其后续版本的开源。作为一名 Linux 管理员或黑客，你应该关注 `MariaDB`。

## 启动 MySQL 或 MariaDB

幸运的是，Kali 已经安装了 `MySQL` 或 `MariaDB`（如果你使用的是其他发行版，可以从软件仓库或直接从 https://www.mysql.com/downloads/ 下载并安装 `MySQL`）。

要启动你的 `MySQL` 或 `MariaDB` 服务，请在终端中输入以下内容：

```
kali> systemctl start mysql
```

接下来，你需要通过登录来验证身份。输入以下内容，并在提示输入密码时直接按回车键即可：

```
kali sudo mysql -u root -p
```

```
Enter password:
Welcome to MariaDB monitor. Commands end with ; or \\
Your MariaDB connection id is 31
Server version: 11.4.4-MariaDB-3 Debian n/a
--snip---
Type 'help' or '\h' for help. Type '\c' to clear the current input statement
MariaDB([none]) >
```

在 `MySQL` 或 `MariaDB` 的默认配置中，root 用户的密码为空。显然，这是一个安全漏洞，你应该在第一次登录后通过添加密码来修复它。请注意，操作系统和 `MySQL` 的用户名和密码是分开且相互独立的。让我们现在更改 `MySQL` root 用户的密码以确保安全。

## 与 SQL 交互

`SQL` 是一种用于与数据库交互的解释型编程语言。数据库通常是关系型数据库，这意味着数据存储在多个相互作用表中，每个表在列或多个列中有值。
`SQL` 有多种实现方式，每种实现都有自己的命令和语法，但这里是一些常用命令：

- `select`: 获取数据
- `union`: 合并两个或多个查询的结果
- `insert`: 添加新数据
- `update`: 修改现有数据
- `delete`: 删除数据

你可以为每个命令提供条件来更具体地指定你想做什么。例如，该行
`select user, password from customers where user='admin';`
返回用户的值。

## 设置密码

从输出可以看出，root 账户没有密码。让我们分配一个密码。为了这样做，我们首先选择一个数据库。你系统上的 `MySQL` 会带有一些数据库。使用 `show databases;` 命令查看所有数据库：

```
mysql> show databases;
```

```
+--------------------++
| Database           |
+--------------------++
| information_schema |
| mysql               |
| performance_schema |
| sys                |
+--------------------++
4 rows in set (0.23 sec)
```

`MariaDB/MySQL` 默认带有四个数据库，其中（`information_schema` 和 `performance_schema`）是我们使用的管理数据库。我们将使用非管理数据库 `mysql`，它是为了你的目的而提供的。要使用 `mysql` 数据库，输入：

```
MariaDB([mysql]> use mysql;
```

```
Reading table information for completion of table and column name You can turn off this feature to get a quicker startup with -A
```

```
Database changed
```

该命令连接 `mysql`。现在，可以使用以下命令将 root 用户密码设置为 `hackers-aise`：

```
MariaDB([mysql]> set PASSWORD FOR 'root'@localhost = PASSWORD("hackers-aise");
```

该命令通过将用户的 root 密码设置为 `hackers-aise` 来更新用户。
要检查密码是否更改，我们可以再次运行之前的命令来检查账户密码：

```
mysql> select user, host, password from mysql.user;
```

```
+------------------------------------------------------+
| User        | Host      | Password                           |
+------------------------------------------------------+
| mariadb.sys | localhost | *FED2C7AF828E509C64D670F147E13922F6A8C4|
| root        | localhost | |
| mysql       | localhost | invalid |
+------------------------------------------------------+
3 rows in set (0.002 sec)
```

从输出可以看出，root 账户现在有密码了！注意密码经过了哈希处理（单向加密），因此只能看到密码的哈希值。

## 访问远程数据库

要访问本地上的 `MySQL` 数据库，我们使用以下语法：

```
kali> mysql -u <username> -p
```

如果没有提供主机名或 IP 地址，此命令将默认使用本地的 `MySQL` 实例。若要访问远程数据库，我们需要提供托管 `MySQL` 数据库的系统主机名或 IP 地址。这是一个示例：

```
kali> mysql -u root -p 192.168.1.101
```
