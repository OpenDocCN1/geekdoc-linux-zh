
`psql`客户端会传递账户的系统信息并将其发送到 PostgreSQL 服务器进行验证。遗憾的是，这意味着必须以系统账户身份登录才能访问 PostgreSQL 管理员账户。此最简单的方法是使用 Linux 命令：

```
linux:~ su postgres
postgres@linux:~root> psql -U postgres
无法更改目录 "root"
欢迎使用 psql 8.1.5，这是 PostgreSQL 交互式终端。
```

- 输入：`|` 用于分发条款的版权信息
- `\h` 获取 SQL 命令的帮助
- `\?` 获取 psql 命令的帮助
- `\g` 或以分号结束以执行查询
- `\q` 退出

```
postgres=#
```

# 实现 PostgreSQL

现在你已经以 `postgres` 数据库超级用户账户身份登录了。与 MySQL 的 `show` 命令类似，PostgreSQL 使用系列特殊的非 SQL 元命令（meta-commands）来查看数据库信息。最常用的四个元命令是：

- `\l` 列出数据库
- `\c` 连接到数据库
- `\dt` 列出数据库内的表
- `\q` 退出数据库

以 `postgres` 超级用户身份登录时，你可以为 PostgreSQL 服务器创建一个新数据库。使用标准的 `CREATE DATABASE` SQL 命令来创建新数据库：

```
postgres=# create database test;
CREATE DATABASE
postgres=# \c test
你现在已连接到数据库 'test'。
test=#
```

创建数据库后，使用 `\c` 元命令连接它。只有在连接到数据库时，你才能创建数据库对象。

PostgreSQL 中的用户账户被称为“登录角色”（Login Roles）。`postgres` 超级用户可以创建新的登录角色，并向它们授予数据库对象的权限。但请记住，openSUSE 的 PostgreSQL 实现使用 openSUSE 系统密码文件来验证登录角色，因此你的 PostgreSQL 登录角色必须与现有的 openSUSE 用户账户匹配：

```
test=# create role login password 'testing';
CREATE ROLE
test=# grant all on test to rich;
GRANT
test=#
```

现在你可以使用系统账户 `rich` 登录 `test` 数据库：

```
rich:-> psql test
```

欢迎使用 psql 8.1.5，这是 PostgreSQL 交互式终端。

```
输入: \ 用于分发条款的版权信息
\h 获取 SQL 命令的帮助
\? 获取 psql 命令的帮助
\g 或以分号结束以执行查询
\q 退出
```

```
test=>
```

因为我已经以用户 `rich` 的身份登录了 openSUSE，我只需要运行 `psql` 加上数据库名称即可连接。随着新数据库的创建以及拥有数据库权限的用户账户，你已经准备好开始处理数据了！

## 创建表

当你进入 PostgreSQL 数据库后，可以使用标准的 `CREATE TABLE` 命令来创建表。例如：

```
test=> create table employees (
empid int primary key,
lastname varchar,
firstname varchar,
salary float4
);
NOTICE:  表 "employees" 已创建
```

创建表后，使用 `\dt` 命令查看表是否存在：

```
test=> \dt
           关系
Schema | Name      | Type
+------+-------------+-------
public | employees | table
```

# 使用 openSUSE 数据库客户端

![](img/c9db7a0f830c3bc4a085bc553b89ff25_631_0.png)

图 29.6 查看数据

如果你有使用 Microsoft Access 创建数据库的经验，那么你会觉得 OpenOffice.org 非常熟悉。

## Base

虽然 OpenOffice.org 是一个功能完整的数据库应用程序，但有时你只需要一个简单的数据库客户端来创建几个存储数据的表。Base 是一个更简单的数据库客户端，提供了基础功能，而没有 OpenOffice.org 的那些复杂功能。它还具有使用 JDBC 连接 MySQL 或 PostgreSQL 数据库服务器的能力，默认配置使用自己的数据库文件（如果你记得旧的 Base 产品，这听起来可能很熟悉）。可以使用 YaST 软件管理轻松安装。在软件管理中搜索 Base。必须安装以下三个包：

- 核心应用程序
- sqlite 驱动程序
- xbase 驱动程序

安装 Base 后，它将出现在与 Base 相同的菜单区域（位于 Office 部分下）。第一次运行 Base 时，它会通过一个安装向导，允许你设置几个默认值：

- 单窗口模式 (SDI) 或多窗口模式 (MDI)
- 旧的脚本方法或较新的宏方法
- 插入、更新和删除功能

安装向导完成后，将出现带有数据库的主窗口。点击“新建”按钮将启动连接向导，如图 29.7 所示。

![](img/c9db7a0f830c3bc4a085bc553b89ff25_632_0.png)

图 29.7 连接向导

向导提示输入与特定数据库相关的信息：

- 存储数据库文件的目录
- 数据库名称
- 对象存储位置（在数据库文件中或单独存储）
- 数据库驱动程序
- 存储单个表的目录

一旦你完成了向导中的信息，就会出现主窗口，如图 29.8 所示。如图 29.8 所示，图形化显示包含与 Base 程序相同的元素（表、查询和报告）；然而，它们并不那么华丽。与 Base 一样，有简单的视图用于设计新表、查询和报告。虽然没有 Base 华丽，但 Base 提供了个人数据库系统的所有基础功能。如果你在性能较的系统上运行 openSUSE，Base 可能正符合你的需求。

![](img/c9db7a0f830c3bc4a085bc553b89ff25_633_0.png)

## 参考文献

- http://www.mysql.com/ — MySQL 首页，包含新闻、下载和文档。
