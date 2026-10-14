

+------------------------------+
| root | 127.0.0.1 |            |
| | localhost |                 |
| debian-sys-maint | localhost |
| root | localhost |            |
| | testbox |                   |
| root | testbox |              |
+------------------------------+
6 rows in set (0.00 sec)

mysql>

MySQL 控制访问基于用户账户以及用户连接服务器的位置。 在 MySQL 中添加新用户账户与使用 SQL INSERT 语句一样简单：

```
mysql> insert into user (user,host,password) values ('rich','localhost','');
Query OK, 1 row affected (0.00 sec)
mysql> insert into user (user,host,password) values ('rich',
    -> 'testbox.localdomain','');
Query OK, 1 row affected (0.00 sec)
mysql>
```

因为我们不想为 user 表中的所有字段添加数据，所以必须指定我们要填充的字段。 在执行 INSERT 命令后，新用户账户已存在，但没有分配密码，这会阻止账户登录。 下一步是为用户账户分配新密码。

这是使用 SQL UPDATE 语句以及特殊的 MySQL PASSWORD() 函数完成的，该函数使用 MySQL 加密方法加密密码：

```
mysql> update user set password = PASSWORD('testing')
    -> where user = 'rich';
Query OK, 2 rows affected (0.00 sec)
mysql>
```

你可以使用 SELECT 命令查询 user 表并验证新用户条目是否已正确输入。 一旦创建了普通用户账户，你就可以开始为你的应用程序创建一些数据库对象了。

![](img/39e65eeb4f54001ede08c6114ae3cc6c_630_0.png)

> **自 MySQL 版本 5 起，你也可以使用 CREATE USER 命令一步添加新用户账户并分配密码：**
> 
> ```text
> mysql> create user 'mytest'@'localhost' identified by 'test';
> Query OK, 0 rows affected (0.00 sec)
> mysql>
> ```
> 
> **这会创建一个名为** `mytest` **的新用户账户，该账户可以从 localhost 登录，密码为** `test`。

创建用户账户后，使用 SQL GRANT 语句为用户授予数据库的权限：

```
mysql> grant select,insert,update on test.* to rich;
Query OK, 0 rows affected (0.00 sec)
mysql>
```

在 GRANT 语句中，你定义用户账户想要访问的所有表 [使用通配符 (*) 表示数据库中的所有表]，以及要授予的具体权限。

新用户账户 rich 现在可以登录到 MySQL 服务器并访问 test 数据库：

```
$ mysql test -u rich -p -s
Enter password:
mysql>
```

因为我没有为 rich 用户账户授予 CREATE 权限，所以我无法在数据库中创建新表。 我只能操作现有表。

## 在 PostgreSQL 中创建用户

在 PostgreSQL 中，用户账户称为登录角色。 postgres 管理员用户可以创建新的登录角色并向这些角色授予对数据库对象的用户权限。 请记住，Ubuntu 安装的 PostgreSQL 使用 Ubuntu 系统密码文件来验证登录角色，因此你的 PostgreSQL 登录角色必须与现有的 Ubuntu 系统用户账户匹配：

```
postgres=# create role rich login password 'test';
CREATE ROLE
postgres=# grant all on database test to rich;
GRANT
postgres=#
```

现在用户账户 rich 在 test 数据库中拥有完全权限：

```
rich@testbox:~$ psql test -q
test=>
```

rich 用户现在可以在 test 数据库中创建新表。

## 构建表

在数据库中，表存储实际数据。 表包含数据字段，这些字段定义要存储的各个数据元素。 在数据字段中，你必须定义数据的 数据类型，因为数据库服务器必须知道每个数据字段所需的存储空间。 MySQL 和 PostgreSQL 中常用的数据类型有

- char：固定长度的文本字符串；如果数据未填满固定长度，则会在存储的数据中添加空格
- varchar：可变长度的文本字符串；数据库服务器仅为指定的文本创建足够的存储空间
- integer：没有小数位 的整数
- floating point：具有不同小数位 的十进制数
- text：用于大量文本的数据存储类型
- binary large object (BLOB)：一种二进制数据存储类型，允许你存储图像、视频和音频剪辑以及 PDF 文件等二进制文件

