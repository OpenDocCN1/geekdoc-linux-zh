
在 `wwww4` 目录下创建 `index.html` 文件，这是一个背景非白色的 HTML 页面。

在 `vServers` 部分，点击 Cherokee 管理面板左上角的“添加虚拟服务器”按钮（蓝色加号按钮）。在对话框的 `Nick` 文本字段中输入 `christos.dynu.com`，这是书中介绍的域名。同时在 Document Root 文本字段中输入你刚刚创建的目录 `/var/www4`。点击 `Add` 按钮确认设置。

点击窗口左侧服务器列表中的新虚拟服务器，将其他设置应用到该新虚拟服务器。在 `Basics` 选项卡中，在 Directory Indexes 文本字段中输入文件名 `index.html`。

在 `Host Match` 选项卡中，从 `Method` 下拉菜单中选择 `Matchname` 选项。

接下来进入 `Behavior` 标签页，并点击 `Rule Management` 按钮。会出现一组新的标签页（`Rule`、`Handler` 等等）。

在 `Rule` 标签页中，在 `Rule Type` 下拉菜单中选择 `Incoming IP/Port`。在出现的 `Incoming IP/Port` 下拉菜单中选择 `8181`。由于虚拟服务器是基于域名而非端口号（正如我们在上一章中所做的那样），你可以为此虚拟服务器分配更多端口。在 `Assign new IP/Port` 区域的下拉菜单中，选择端口 `8080`。

![](img/5bf591327968a4c0190eb6adbf83042b_150_0.png)

在 `Handler` 标签页中，在 `Handler` 下拉菜单中选择 `List & Send`，并删除 `Document root` 文本框中的任何条。这是一个备用的文档根路径。

![](img/5bf591327968a4c0190eb6adbf83042b_150_1.png)

你也可以通过点击窗口左侧 `Rule` 列表旁绿色圆形按钮来禁用 Cherokee 创建的任何预定义规则。你还可以将 `Default` 规则的处理器设置为 `None`，以避免将内容发布到你设置的规则之外。
接下来点击 `SAVE` 按钮确认设置。在出现的对话框中点击 `Graceful restart` 按钮。

### 创建第二个虚拟服务器

我们接下来创建一个匹配域名 `webserver.dynu.com` 的虚拟服务器。点击 `Add New Virtual Server` 按钮，并在 `Nick` 文本字段中输入域名 `webserver.dynu.com`。创建目录 `/var/www5` 以及在该目录下创建文件 `index.html`。在 `index.html` 文件中，输入用于显示简单彩色页面的 HTML 代码。在 `Document Root` 字段中输入 `/var/www5`。点击 `Add` 按钮，并在窗口左侧区域的服务器列表中选择新虚拟服务器的名称（`webserver.dynu.com`）。
在 `Basics` 标签页中，在 `Directory indexes` 字段中输入 `index.html`。在 `Host Match` 标签页中，选择 `Match Nickname` 方法并点击 `Behavior` 标签页中的 `Rule Management` 按钮。在新的标签页中，点击 `Rule` 页，在 `Route type` 下拉菜单中选择 `Incoming/Port`，并在 `Incoming IP/Port` 下拉菜单中选择 `8080`（本章使用的两个端口之一）。同样将 `Default` 规则的处理器设置为 `None`。与上虚拟服务器一样，你也可以分配另一个服务器使用的端口 `8181`。

在 `Handler` 标签页中，在 `Handler` 下拉菜单中选择 `List & Send`，并删除 `Document Root` 文本框中的任何条。最后点击窗口右上角的 `SAVE` 按钮确认设置。在出现的对话框中点击 `Graceful restart` 按钮。

### 测试虚拟服务器

此时，两个虚拟服务器正在同时运行，且每个虚拟服务器都在

![](img/5bf591327968a4c0190eb6adbf83042b_151_0.png) 提供不同的内容。在本例中，`christos.dynu.com` 应该提供一个绿色背景的 HTML 页面，而 `webserver.dynu.com` 应该提供一个红色背景的 HTML 页面。

![](img/5bf591327968a4c0190eb6adbf83042b_152_0.png) 我们将使用 `www.webpagetest.org` 查看来自两个虚拟服务器的 HTML 页面。记住，我们没有使用端口转发服务器；因此，必须在 URL 中包含端口号：

`http://webserver.dynu.com:8080`

或者

`http://webserver.dynu.com:8181`

或者

`http://christos.dynu.com:8181`

或者

`http://christos.dynu.com:8080`

前两个 URL 应该显示红色的页面：

`/var/www5/index.html`

![](img/5bf591327968a4c0190eb6adbf83042b_152_1.png)

后两个 URL 应该显示绿色的页面：
`/var/www4/index.html`

![](img/5bf591327968a4c0190eb6adbf83042b_153_0.png)

## 第 13 章 数据库驱动的网站

在本章中，你将创建一个支持 PHP 的虚拟服务器，它通过 PHP 连接到 MySQL 数据库。这将允许客户端通过 Web 上的表单查询数据库。你将从在服务器上安装 MySQL 数据库开始，然后在命令行创建并测试数据库，最后创建一个连接 MySQL 数据库的 PHP 页面以及用于向远程用户显示表单的 PHP 页面。表单嵌入第一个 PHP 页面中。用户在第一个 PHP 页面提交请求的信息后，数据将发送到第二个 PHP 页面，由该页面查询数据库并将结果返回给用户。最后，你将在测试并在局域网和远程使用在线网络工具进行数据库查询。

### MySQL 安装

打开 Linux 终端并输入以下命令：

```bash
$ sudo apt-get install mysql-server mysql-client php5-mysql
```

在安装过程中，会出现一个简单的蓝色窗口询问 MySQL root 用户的密码。输入密码并按键盘上的回车键。

![](img/5bf591327968a4c0190eb6adbf83042b_155_0.png) 另一个窗口出现；重新输入你的密码。

安装完成后，在 Linux 终端中输入以下命令以 mysql 用户 root 登录 mysql（不要与 Linux 用户 root 混淆）。使用 `-p` 参数提供所需的密码，并使用 `-u` 指定用户：

```bash
sudo mysql -u root -p
```

为 `sudo` 命令输入用户密码，然后输入你在安装期间创建的 MySQL 密码。当你看到 mysql 提示符时，MySQL 已准备好供你输入命令：

```text
[sudo] password for christos:

Enter password:

Welcome to the MySQL monitor. Commands end with; or \g\nYour MySQL connection id is 39

Server version: 5.5.41-ubuntu0.14.10 (Ubuntu)

Copyright (c) 2000, 2014, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its affiliates. Other names可能是其所有者的商标。

Type 'help'; or 'h' for help. Type 'c' to clear the current input statement.

mysql>
```

![](img/5bf591327968a4c0190eb6adbf83042b_156_0.png)

### 从命令行创建 MySQL 数据库和表

使用 `create database` 命令创建一个名为 `bookstore` 的数据库：

```sql
mysql> create database bookstore;
```

注意，MySQL 命令也可以大写（例如 `CREATE DATABASE`），且所有命令都应以分号（`;`）结束。

输入 `use` 命令使用特定的数据库（在本例中为刚刚创建的数据库）：

```sql
mysql> use bookstore;
```

让我们为 `bookstore` 数据库添加一个名为 `books` 的表。使用 `create table` 命令创建 `books` 表：

```sql
mysql> create table books(book_id int auto_increment primary key, title varchar(255) not null, author varchar(255) not null);
```

或者

```sql
mysql> create table books(book_id int auto_increment, title(255) not null, author varchar(255) not null, primary key(book_id));
```

`books` 表包含一个名为 `book_id` 的字段，它是一个整数（`int`）数字。`auto_increment` 关键字表示在添加每个记录时 `book_id` 会自动递增（默认从 1 开始）。`primary key` 约束表示此字段唯一标识表中的每条记录。

表还将包含另外两个字段，`title` 和 `author`。它们都是 `varchar` 类型，存储指定最大长度的可变字符串。字段 `title` 和 `author` 可以存储 255 个字符。`not null` 指令强制字段不允许空值。

使用 `show tables` 命令显示 `bookstore` 数据库包含的表。你只创建了一个名为 `books` 的表：

```sql
mysql> show tables;
```

命令输出如下：

```text
mysql> show tables;
+----------------------+++
| Tables_in_bookstore |
+----------------------+
| books               |
+----------------------+
1 row in set (0.01 sec)
```

```sql
mysql>
```

使用 `describe` 命令显示表结构：

```sql
mysql> describe books;
```

命令输出如下：

```text
mysql> describe books;
+-----------+-------------+------+------+-------+------+
| Field | Type | Null | Key | Default | Extra |
+-----------+-------------+------+------+-------+------+
| book_id | int(11) | NO | PRI | NULL | auto_increment | |
| title | varchar(255) | NO | | NULL | | |
| author | varchar(255) | NO | | NULL | | |
+-----------+-------------+------+------+-------+------+
3 rows in set (0.05 sec)
```

```sql
mysql>
```

### 从命令行向数据库插入数据

使用 `insert` 命令向 `books` 表插入三条记录。请记住，`book_id` 字段是自动递增的，你不需要输入 `book_id` 值。

```sql
mysql> insert into books (title, author) values ('Waving The Web', 'Tim Berners Lee');
mysql> insert into books (title, author) values ('Just for Fun', 'Linus Torvalds');
mysql> insert into books (title, author) values ('How the Web was Born', 'Gillies & Cailliau');
```

要查看这三条记录，使用 `select` 命令。你可以指定要查看的记录，或者使用星号 `'*'` 通配符选择任何记录：

输出所示：

```sql
mysql> select * from books;
+-----------+--------------------------+----------------+
| book_id   | title                    | author           |
+-----------+--------------------------+----------------+
| 1 | Weaving The Web         | Tim Berners Lee  |
| 2 | Just for Fun             | Linus Torvalds   |
| 3 | How the Web was Born     | James Gillies and Robert Cailliau |
+-----------+--------------------------+----------------+
3 rows in set (0.07 sec)
```

### 从命令行查询数据库

你可以使用 `select` 命令查询数据库。执行一个特定的查询，你也将通过在线网络工具重复此操作，远程查询你站点的数据库。例如，查看包含关键字 Web 的书籍标题和作者。

```sql
mysql> select title, author from books where title like "%Web%"
```

SQL 的 `like` 运算符用于 `where` 子句，以便在字段中搜索特定模式。在上一个示例中，`like` 与 `%` 通配符字符配合，它可以匹配任何字符序列或空。另一个通配符字符下划线 `_` 精确匹配一个字符。因此，查询结果是任何包含 Web 关键字的标题和作者配对。

如预期的那样，数据库中有两个标题包含 Web 关键字：

```sql
mysql> select title, author from books where title like "%Web%"
+------------------------------------------------+
| title | author |
+------------------------------------------------+
| Weaving The Web | Tim Berners Lee |
| How the Web was Born | James Gillies and Robert Cailliau |
+------------------------------------------------+
2 rows in set (0.02 sec)
mysql>
```

要退出 MySQL 输入：

```sql
mysql> \c
```

然后输入：

```sql
mysql> exit
```

### 创建启用 PHP 的虚拟服务器

在 Linux 终端中，启动 `cherokee-admin`：

```bash
$ sudo cherokee-admin -b
```

从局域网的任一计算机上打开浏览器，并在地址栏输入：
`http://192.168.1.101:9090`

其中 `192.168.1.101` 是 Web 服务器的私有 IP 地址。

在出现的对话窗口中，在 Username 处输入 `admin`，并在 Password 处输入 `cherokee-admin` 输出返回的次性密码，以进入 Cherokee 管理面板。

在 `vServers` 部分，点击 `Add New Virtual Server` 按钮（蓝色加号按钮）创建一个新的虚拟服务器。在 `Add New Virtual Server` 对话窗口中，为服务器输入别名（例如 `Bookstore`），并提供文档根目录 `/var/www6`，该目录之前已使用以下命令创建：

```bash
$ sudo mkdir /var/www6
```
