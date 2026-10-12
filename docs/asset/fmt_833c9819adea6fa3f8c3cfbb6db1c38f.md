
一旦文件处理完毕，`mysql` 将退出。

## mysqladmin

这是主要的管理实用程序。除了标准的 `-u` 用户和通过 `-p` 请求提示输入密码外，你还需要四个主要命令：

| | 描述 |
|---|---|
| create databasename | 创建新数据库 |
| drop databasename | 删除数据库 |
| password newpassword | 修改密码（如我们之前看到的） |
| status | 提供服务器状态 |
| version | 提供服务器版本号以及其运行了多久 |
如果你在不带参数的情况下调用它，它将提供一份它接受的命令的有用列表。

## mysqlbug

希望你永远不需要这个工具！它会收集有关你安装的信息，并设置一个标准报告，一旦你编辑了问题的细节，就可以将其邮件给维护者。

## mysqldump

这是一个非常实用的实用程序，允许你将数据库（所有表或选定的表）导出到文件中。它向文件中写入 SQL 命令，可以通过像我们之前看到的那样将输入重定向到 `mysql` 来执行，或者使用我们很快就会遇到的 `mysqlimport`。参数是数据库，以及可选的该数据库中一个或多个表的列表。除了标准的 `-u` 和 `-p` 选项外，你会发现非常有用的两个选项是：

```
--add-drop-table 在输出文件中添加 SQL 命令，在创建这些命令之前删掉（删除）任何表
-t 仅导出表数据
-d 仅导出表结构
```

信息产生在标准输出上，因此你可能需要将其重定向到文件。
你可以使用此实用程序进行定期备份，或导出数据用于。

你也可以让 `mysql` 处理来自文件中的命令，只需像这样从文件重定向标准输入即可：

```
$ mysql -u rick -pbar foo < sqlcommands.sql
```

一旦文件处理完毕，`mysql` 将退出。

## mysqlshow

这是一个非常实用的实用程序，可以显示有关服务器、数据库或表的有用信息，取决于你提供的参数：

- 不带参数时，它列出所有数据库。
- 提供数据库作为参数时，它列出该数据库中的表。
- 同时提供数据库和表名时，它列出该表的列。
- 数据库、表和列时，它列出列的详细信息。

通常提供列名意义不大，因为每个列的所有信息都在表级别显示。

## 创建用户并赋予权限

除了备份重要数据外，最常见的管理需求是设置用户权限。从 MySQL 3.2 版本开始，用户权限应该通过两个命令管理：`grant` 和 `revoke`。这两个命令都在 `mysql` 命令内部运行。

## grant

MySQL 的 `grant` 命令与 SQL2 标准相似，但有一些重大差异。通用格式为：

```
grant privilege on object to user [user-password] [option];
```

有几种可以授予的权限，如下：

| privilege | 描述 |
| --- | --- |
| Alter | 修改表和索引 |
| Create | 创建数据库和表 |
| Delete | 从数据库删除数据 |
| Drop | 删除数据库和表 |
| Index | 管理索引 |
| Insert | 向数据库添加数据 |
| Select | 获取数据 |
| Update | 修改数据 |
| All | 全部 |

还有一些管理权限，但这里不涉及。

授予这些权限的对象标识为：

```
databas.tablename
```

而 `*` 匹配所有，所以 `rick.*` 匹配 `rick` 数据库中的所有内容。由于 MySQL 实现的方式，你可以对尚未创建的数据库授予权限。这看起来可能有点奇怪，但实际上这赋予了用户创建该数据库的权利。指定的用户名可以是现有用户的用户名，或者如果你愿意，也可以新用户名，从而自动创建该用户。MySQL 服务器的客户端用户始终识别为 `username@host`，即使是本地机器也是如此，在这种情况下你应该将主机设置为 `localhost`。

# 第 5 章

该特殊标识符代表任何主机。不过，如果你愿意，可以多次调用 `grant` 命令，为用户想要访问服务器的每台机器各调用一次。如果你想为某个域中的一组主机授予权限，只需对主机使用 `*`，并按如下方式指定域：

```sql
rick@*.docbox.co.uk
```

注意，我们现在需要引号。

使用 `identified by` 子句可以为用户名设置密码。通常情况下，如果你正在创建一个新用户，应该立即设置密码；否则将让你的数据库处于不安全状态。

## with grant

`with grant` 选项允许用户传递你刚刚授予给他们的权限。通常情况下你不会使用这个选项，除非你正在设置管理员账户。

理论部分就到此为止，让我们创建一个用户 `rick`，他可以从任何机器连接，将他的密码设置为 `foo`，并允许他创建一个名为 `foo` 的数据库。我们需要的命令是：

```sql
mysql> grant all on foo to rick@'%' identified by 'bar';
```

记住 SQL 命令末尾必须有分号 `;`。

这将创建一个密码为 `bar` 的用户 `rick`。该用户可以从任何机器连接，并创建和管理数据库 `foo`。一旦你授予了 `rick` 创建 `foo` 数据库的权限，他就可以使用标准的 `create database` SQL 命令来物理创建它。

## revoke, delete

在我们查看权限时，查看如何撤销权限也是明智的。通常使用 `revoke` 命令完成，其语法如下：

```sql
revoke a-privilege on an-object from a-user;
```

格式与 `grant` 命令相似。例如：

```sql
revoke insert on foo. from rick@'%';
```

然而，有一个细微的异常之处：即使你撤销了用户的所有权限，他们仍然对你的数据库拥有连接权限，这可能不是你想要的。要彻底删除该用户，你还必须从 MySQL 数据库的 `user` 表中删除他们，然后强制 `mysql` 重新加载表，如下所示：

```sql
use mysql;
delete from user where User = "rick" and Host = "%%";
mysql> flush privileges;
```

## Passwords

如果你忘记指定密码，可以以后再设置。你需要以 `root` 身份登录，并选定 `mysql` 数据库。如果你输入：

```sql
mysql> select host, user, password from user;
```

你应该得到类似这样的列表：

| host | user | password |
|---|---|---|
| localhost | root | 67457e226a1a15bd |
| % | rick | 7c9e0a41222752fa |
| .% | foo | |

2 rows in set (0.00 sec)

假设你想为用户 `foo` 分配密码 `bar`；你可以这样操作：

```sql
mysql> update user set password='bar' where user='foo';
```

再次显示 `mysql.user` 表中的相关列：

```sql
mysql> select host, user, password from user;
```

| host | user | password |
|---|---|---|
| localhost | root | 67457e226a1a15bd |
| % | rick | 7c9e0a41222752fa |
| .% | foo | |

2 rows in set (0.00 sec)
mysql>

不出所然，它在那里；与我们之前为用户 `rick` 定义的相同的加密密码。

## Creating a Database

让我们操作一下一个名为 `rick` 的数据库。首先，作为 `mysql root` 用户，我们必须赋予自己创建数据库的权限：

```sql
mysql> grant all on rick.* to mysql@% identified by "bar";
```

这将赋予用户 `rick` 从所有机器访问对 `rick` 数据库的所有权限。

我们现在可以退出 `mysql`，以用户 `rick` 的身份重新启动并创建数据库：

```sql
mysql> quit
Bye
$ mysql -u rick
mysql> create database rick;
```

然后我们使用 `use` 命令切换到 `rick` 数据库：

```sql
mysql> use rick
```

现在我们就可以创建任何需要的表了。

你可能还记得在 PostgreSQL 章节中，我们使用 `children` 表作为示例。创建它的 SQL 如下：
