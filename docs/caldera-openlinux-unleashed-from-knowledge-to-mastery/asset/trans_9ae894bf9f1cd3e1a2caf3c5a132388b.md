

通过添加、删除和修改 user、db 和 host 表中的条目，你可以告诉服务器哪些用户能够登录、他们可以访问哪些数据库以及他们可以从哪些主机连接。表 26.2 展示了这三个授权表的内容。字段名称后括号内的字符串指示该特定字段包含在三个权限表中的哪一个。

### 表 26.2 权限表

| 字段 | 描述 |
| :--- | :--- |
| Host (user, db, host) | 确定用户可以从哪台主机连接 |
| User (user, db) | 设置用户名称 |
| Db (db, host) | 确定这将影响哪个数据库 |
| Password (user, db) | 设置用户的密码 |
| Select_priv (user, db, host) | 允许用户选择（列出）数据库中的特定行——可以是 Y 或 N |
| Insert_priv (user, db, host) | 允许用户向数据库插入一行——可以是 Y 或 N |
| Update_priv (user, db, host) | 允许用户更新现有行——可以是 Y 或 N |
| Delete_priv (user, db, host) | 允许用户删除一行——可以是 Y 或 N |
| Index_priv (user, db, host) | 允许用户创建或删除索引——可以是 Y 或 N |
| Alter_priv (user, db, host) | 允许用户使用 ALTER TABLE 命令——可以是 Y 或 N |
| Create_priv (user, db, host) | 允许用户创建新的数据库和表——可以是 Y 或 N |
| Drop_priv (user, db, host) | 允许用户删除现有的数据库和表——可以是 Y 或 N |
| Grant_priv (user, db, host) | 允许用户向其他用户授予权限，但仅限你自己拥有的权限——可以是 Y 或 N |
| Reload_priv (user) | 允许用户使用 mysqladmin 程序执行以下命令：reload, refresh, flush-privileges, flush-hosts, flush-logs 和 flush-tables——可以是 Y 或 N |
| Shutdown_priv (user) | 允许用户使用 mysqladmin 执行 shutdown 命令——可以是 Y 或 N。 |
| Process_priv (user) | 允许用户使用 mysqladmin 执行 processlist 和 kill 命令——可以是 Y 或 N。 |
| File_priv (user) | 允许用户读写 MySQL 服务器本身可以读写的任何文件——可以是 Y 或 N。 |

当你尝试连接到你的 MySQL 服务器（或任何其他 MySQL 服务器）时，服务器通过检查权限表来确定是接受还是拒绝连接。以下是其工作原理的简要说明：

- 1. 首先，服务器检查 **user** 表，以确定你是否能够建立任何连接。如果在 *user* 表中存在一条记录，其用户名和对应的密码与你输入的相同，且该条目的主机名与你连接时所在的主机名相同，则允许连接。用户还从 *user* 表中获得其“全局”权限。
- 2. 当你登录时，*db* 和 *host* 表用于确定你是否被允许执行你尝试执行的操作。如果在 *db* 或 *host* 表中找不到特定用户的记录，则使用 *user* 表中的全局权限。

## 设置你的第一个 MySQL 权限

现在你将要利用你新学到的知识来设置你自己的权限。有两种方法可以做到这一点：使用 GRANT 语句或直接修改授权表。使用 GRANT 语句修改权限系统有一些优势。它对人类更易于理解，而且出错率也低得多。使用哪种方法取决于你。

你必须首先做的是以 root 用户身份连接到 MySQL 服务器，如下所示：

```
mysql -u root -p mysql
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 2 to server version: 3.23.4-alpha-log
Type 'help' for help.
mysql>
```

### 注意

请注意，如果你为 root 账户设置了密码，你必须使用 -p 参数调用 mysql。否则，你将收到以下消息：

```
bash# mysql -u root
ERROR 1045: Access denied for user: 'root@localhost'
(Using password: NO)
```

如果你不提供 -p 参数，mysql 会认为你不希望输入任何密码。

### 示例 1：超级用户

假设你想创建一个用户 `slackhacker`，该用户将拥有 root 权限——即访问一切。`slackhacker` 能够从任何主机连接到服务器，并希望使用 `topsecret` 作为他的/她的密码。

要直接通过修改来实现这一点，请输入以下命令：

```
mysql> INSERT INTO user values('localhost','slackhacker',PASSWORD('topsecret'),'Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y');
mysql> INSERT INTO user VALUES('%','slackhacker',PASSWORD('topsecret'),'Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y');
```

当你进行直接修改时，还必须告诉服务器重新加载表：

```
mysql> FLUSH PRIVILEGES;
```

> **警告**
>
> 请注意，你在 `PASSWORD` 函数内部输入密码。此函数将密码编码为不可读的形式，这样其他用户无法仅通过输入以下内容就看到你的密码：
>
> ```sql
> mysql> SELECT * FROM user WHERE(user='slackhacker');
> ```
>
> 你绝对不想要那样，对吗？所以务必使用 `PASSWORD` 函数。

> **注意**
>
> 请注意，你必须输入分号 (;) 来结束一个命令。

你可能想知道为什么我们为 `slackhacker@localhost` 和 `slackhacker@%`（意味着任何主机上的 `slackhacker`）分别输入了两行。如果我们不这样做，`mysql_install_db` 创建的用于 `localhost` 的匿名用户条目将被使用。原因是匿名用户条目具有更具体的 `Host` 字段值，因此在用户表排序顺序中更靠前。有关此信息的更多细节，请阅读 MySQL 文档，可以在 `www.mysql.com` 找到。

要使用 GRANT 表添加 **slackhacker** 用户，你应按如下操作：

```
mysql> GRANT ALL PRIVILEGES ON *.* TO slackhacker@localhost 
> IDENTIFIED BY 'topsecret' WITH GRANT OPTION;
mysql> GRANT ALL PRIVILEGES ON *.* TO slackhacker@'%' 
> IDENTIFIED BY 'topsecret' WITH GRANT OPTION;
```

如你所见，GRANT 语句更易于理解。因此，使用它们代替直接修改可能更明智。

### 示例 2：来自不同主机的不同数据库

用户根据从哪台主机连接，可能希望访问不同的数据库。这在 MySQL 中很容易做到。

在下面的示例中，我们将创建用户 **common**。**common** 希望能够从总共三台主机 *localhost*、*foreignhost* 和 *anotherhost* 连接。从 *localhost*，**common** 希望访问数据库 **admin**。从 *foreignhost*，他希望访问 **customers**，而从 *anotherhost*，他希望访问 **economy**。他还希望使用密码 **weakpass**。

首先，我们编辑 user 数据库，赋予 **common** 从这三个主机连接的权限：

```
mysql> INSERT INTO user (Host,User,Password)
> VALUES ('localhost','common',PASSWORD('weakpass'));
mysql> INSERT INTO user (Host,User,Password)
> VALUES ('foreignhost','common',PASSWORD('weakpass'));
mysql> INSERT INTO user (Host,User,Password)
> VALUES ('anotherhost','common',PASSWORD('weakpass'));
mysql> FLUSH PRIVILEGES;
```

这三个表允许 **common** 从三个主机 *localhost*、*foreignhost* 和 *anotherhost* 连接。我们将权限字段（所有的 Y）留空，这样它们将默认为 N。现在，我们将编辑 **db** 表，赋予 **common** 访问他的数据库的权限：

```
mysql> INSERT INTO db
> (Host,Db,User,Select_priv,Insert_priv,Update_priv,Delete_priv,
> Create_priv,Drop_priv)
> VALUES
> ('localhost','admin','common','Y','Y','Y','Y','Y','Y');
mysql> INSERT INTO db
> (Host,Db,User,Select_priv,Insert_priv,Update_priv,Delete_priv,
> Create_priv,Drop_priv)
> VALUES
> ('foreignhost','customers','common','Y','Y','Y','Y','Y','Y');
mysql> INSERT INTO db
> (Host,Db,User,Select_priv,Insert_priv,Update_priv,Delete_priv,
> Create_priv,Drop_priv)
> VALUES
> ('anotherhost','economy','common','Y','Y','Y','Y','Y','Y');
```

