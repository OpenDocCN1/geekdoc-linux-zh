
在 MySQL 的默认配置中，`root` 用户的密码为空。显然，这是一个重安全漏洞，你应该在第一次登录后通过添加密码来修复它。请注意，操作系统和 MySQL 的用户名和密码是分开且独立的。为了安全起见，让我们更改 MySQL `root` 密码。

### MySQL 的过去与未来

MySQL 最初由瑞典的 MySQL AB 于 1995 年开发，随后于 2008 年被 Sun Microsystems 收购，后者于 2009 年被 Oracle 收购——因此 MySQL 现在归 Oracle 所有。Oracle 是全球最大的数据库软件发行商，开源社区对 Oracle 继续保持 MySQL 开源的承诺非常担忧。因此，现在有一个名为“Maria”的 MySQL 数据库软件分支，它致力于保持该软件及其后续版本的开源。作为一名 Linux 管理员或黑客，你应该关注 Maria。

### 与 MySQL 交互

SQL 是一种用于与数据库交互的解释型编程语言。数据库通常是关系数据库，这意味着数据存储在多个相互作用的表中，每个表在列或多个列和行中具有值。

SQL 有多种实现，每种实现都有自己的命令和语法，但这里是一些常用命令：

- `select`: 用于检索数据
- `union`: 用于合并两个或多个 `select` 操作的结果
- `insert`: 用于添加新数据
- `update`: 用于修改现有数据
- `delete`: 用于删除数据

你可以为每个命令提供条件，以便更具体地说明你想执行的操作。例如，此行代码：

```
select user, password from customers where user='admin';
```

将返回这些值。

### 设置 MySQL 密码

要为 `root` 用户设置密码，我们使用以下命令：

```
mysql >update user SET password=PASSWORD('new_password') WHERE user='root';
```

这更改了 `root` 用户的密码。要验证更改，你可以使用新密码登录：

```
mysql -u root -p
```

```
| creditcardnumbers |
| performance_schema |
```
(4 rows in set (0.26 sec))

哈！我们发现了一个名为 `creditnumbers` 的待探索数据库。让我们连接它。

在 MySQL 中，与其他数据库管理系统 (DBMS) 一样，我们可以通过输入 `databasename` 来连接感兴趣的数据库。

```bash
mysql ~use creditcardnumbers;
Database changed
```

`Database changed` 响应表明我们现在连接到了 `creditcardnumbers` 数据库。

当然，不言而喻，数据库管理员不太可能配合到将数据库命名为 `creditcardnumbers` 这么易于识别的名字，因此你可能需要进行一些探索来找到感兴趣的数据库。

### 数据库表

我们现在已连接到 `creditcardnumbers` 数据库，可以进行一些探索看看它可能包含哪些信息。数据库中的数据组织成表，每个表可能包含一组不同的相关数据。我们可以通过输入以下命令来查看此数据库中有哪些表：

```bash
mysql >show tables;
+-----------------------------+
| Tables_in_creditcardnumbers |
+-----------------------------+
| cardnumbers |
+-----------------------------+
1 row in set (0.14 sec)
```

在这里，我们可以看到该数据库中只有一个表，名为 `cardnumbers`。通常情况下，数据库会有许多表，所以你可能需要进行更多窥探。在这个示例数据库中，我们很幸运能够将注意力集中在这张表上，以提取黑客的“金羊羊毛”！

现在我们已经有了想要检查的表，需要了解该表的结构。一旦我们知道了表的布局，就可以提取相关信息。

你可以使用 `describe` 语句查看表的结构，如下所示：

```bash
mysql >describe cardnumbers;
+------------------------------------------------------+
+-+
| Field Extra | | Type        | Null | Key  | Default |
+------------------------------------------------------+
+-+
| customers    | varchar(15) | YES  |        |
NULL         |             |      |        |
| address      | varchar(15) | YES  |        |
NULL         |             |      |        |
| city         | varchar(15) | YES  |        |
NULL         |             |      |        |
| state        | varchar(15) | YES  |        |
NULL         |             |      |        |
| cc           | int(12)     | NO   |        |
0            |             |      |        |
+------------------------------------------------------+
+-+
```

MySQL 响应了关于我们感兴趣的表结构的关键信息。我们可以看到每个字段的以及它所持的数据类型（通常是文本类型 `varchar` 或整数类型 `int`）。我们还可以看到它是否接受 `NULL` 值；如果存在的键（键连接表）；字段可能具有任何默认值；以及末端的任何额外信息（如注释）。

### 检查数据

要实际查看表中的数据，我们使用 `SELECT` 命令。`SELECT` 命令要求知道以下信息：

- 包含你想查看的数据表
- 该表中包含你想查看的数据列

我们按照以下格式进行布局：

```sql
SELECT columns FROM table
```

作为查看所有列数据的一种方便快捷方法，我们可以使用星号 `*` 作为通配符，而不是输入我们想要查看的每个列名。因此，要查看 `cardnumbers` 表中所有数据的导出，我们可以输入以下内容：

```bash
mysql >SELECT * FROM cardnumbers;
| customers | address | city | state | cc |
| :--- | :--- | :--- | :--- | :--- |
| Jones | 1 Wall St | NY | NY | 12345678 |
| Sawyer | 12 Piccadilly | London | UK | 234567890 |
| Doe | 25 Front St | Los Angeles | CA | 456789877 |
```

如你所示，MySQL 已将 `cardnumbers` 表中的所有信息显示在我们的屏幕上。我们找到了黑客的金羊羊毛！

### 带有 Metasploit 的 PostgreSQL

PostgreSQL（或简称 Postgres）是另一种开源关系型数据库，由于其易于扩展和处理重负载的能力，被用于非常大型面向互联网的应用程序。它于 1996 年 7 月发布，由一个名为 PostgreSQL Global Development Group 的大量开发者维护。

Kali 默认也预装了 PostgreSQL，但如果你使用的是其他 Linux 发行版，它很可能在你的存储库中，你可以通过以下命令进行安装：

```bash
kali >apt-get postgres install
```

作为一名黑客，你会发现 PostgreSQL 特别重要，因为它是最广泛使用的渗透测试和攻击框架 Metasploit 的默认数据库。Metasploit 使用 PostgreSQL 来存储其模块以及扫描和漏洞利用的结果，以便在渗透测试或攻击中方便使用。出于此，我们将在 Metasploit 的背景下使用 PostgreSQL。

对于 Linux 中几乎所有的服务，我们可以通过输入 `service application start` 来启动 PostgreSQL，如下：

```bash
kali >service postgresql start
```

在 Metasploit 运行后，让我们启动 Metasploit：

```bash
kali >msfconsole
```
