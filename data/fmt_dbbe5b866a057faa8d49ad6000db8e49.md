
这将创建一个名为 `toys.pgql` 的文本文件，其中 `toys` 数据库的备份。另一个名为 `pg_dumpall` 的工具可以创建位于 `/var/lib/pgql` 下所有数据库的备份。

## 恢复数据库

PostgreSQL 自带一个名为 `pg_dump` 的工具来创建数据库备份。它的语法是 `pg_dump database`

其中 `database` 是你想备份的数据库名称。备份的内容将显示在终端中，你需要将其重定向到文件保存。要创建 `toys` 数据库的备份，请使用：

```
pg_dump > toys.pgql
```

这将创建一个名为 `toys.pgql` 的文本文件，其中 `toys` 数据库的备份。另一个名为 `pg_dumpall` 的工具可以创建位于 `/var/lib/pgql` 下所有数据库的备份。

## 配置 PostgreSQL

PostgreSQL 在其数据目录 `/var/lib/postgresql` 中也有配置文件。最常用的两个文件是 `postgresql.conf` 和 `pg_hba.conf`。第一个文件 `postgresql.conf` 是主配置文件，可用于调整 PostgreSQL 以提高性能。选项被分为不同的部分，例如位置、资源使用和查询优化。许多高级选项都设置了默认值，起初可能无法满足你的需求。但如果你花时间更改这些选项的值，当 PostgreSQL 重载时将看到巨大的性能提升。作为开始，你可以尝试配置文件的查询优化部分来检查是否有帮助。每当更改文件选项时，记得重新加载 PostgreSQL 以告知服务器进程。
更多可以通过 `postgresql.conf` 文件配置的属性，可以在此处选择：http://www.postgresql.org/docs/8.1/interactive/runtime-config.html。

### pg_hba.conf

`pg_hba.conf` 文件列出了连接 PostgreSQL 服务器的主机或网络。该文件配置哪些用户从哪些机器连接到数据库以及它们使用的连接方法。文件的每行分为五列：`host`、`database`、`user`、`cidr-address` 和 `method`。

- `host` 列定义了什么类型的主机可以连接到服务器。通常你在这里指定以告诉 PostgreSQL 匹配传入的 TCP/IP 连接。如果你需要更严格的方法，还有其他可用选项，你可以在此处找到：http://www.postgresql.org/docs/8.1/interactive/client-authentication
- `database` 是你想让远程机器连接的数据库名称。最好使用默认的 `all`，但如果你知道远程用户需要哪个数据库，可以指定它。你可以通过逗号分隔来指定多个数据库。
- `user` 列出了允许连接指定数据库的 PostgreSQL 角色。对于 `database`，你可以通过逗号分隔来指定多个用户。

* `cidr-address` 指定要连接到此服务器的机器的 IP 地址范围。例如，如果你想允许网络 `10.0.0.0` 中的主机，你将在此处使用 `10.0.0.0/24`。如果允许 IP 地址为 `10.0.0.25` 的机器，你将使用 `10.0.0.25/32`。

* `method` 允许你指定 PostgreSQL 如何对连接到它的主机进行身份验证。你可以使用 `trust` 允许无验证连接，或使用 `reject` 拒绝它们。

例如，要允许网络 `192.168.1.0` 的用户以 `toymaster` 角色连接到 `toys` 数据库，你需要添加此行：

```
host toys toymaster  192.168.1.0/24  md5
```

这告诉 PostgreSQL 使用 TCP/IP 通过 `toymaster` 用户连接到 `toys` 数据库。这些主机必须属于 `192.168.1.0` 网络。在进行身份验证时，服务器必须首先检查 PostgreSQL 用户是否存在。如果存在，服务器将从远程主机接收 MD5 加密的密码。当主机的密码与服务器的密码数据库匹配时，即允许使用 `toys` 数据库。

你可以通过更改 ID 为其他内容来改变身份验证的行为，从而强制你为 PostgreSQL 创建相同的系统用户。例如，你可以使用 `md5`，这样远程主机在连接之前无需检查是否存在相同的系统用户即可识别自己。对于任何配置文件的更改，你都需要重新加载服务器使修改生效。

现在你已经了解了如何在系统层面管理 MySQL 和 PostgreSQL，是时候学习数据库层面的管理了。接一节将介绍涵盖 CRUD 的一些基础数据库语言。

### CRUD 与数据库

CRUD 是 Create（创建）、Read（读取）、Update（更新）和 Delete（删除）的缩写，是软件的四大功能。几乎所有软件都会创建、读取、更新和删除，有些以列表和数据结构的形式存在。数据库也不例外，因为它们也是软件，专门负责存储。

CRUD 直接对应于 SQL，包括 MySQL 和 PostgreSQL。每当一个对象被创建、查看、更新或销毁时，都会使用相应的 SQL 语句执行该操作。表 12-1 显示了 CRUD 与 SQL 的对应关系。

表 12-1. CRUD 到 SQL 的映射

| CRUD 阶段 | SQL 语句 |
|---|---|
| CREATE | CREATE |
| READ | SELECT |
| UPDATE | UPDATE |
| DELETE | DELETE |

作为管理 MySQL 和 PostgreSQL 等 RDBMS 的管理员，我们真的需要学习所有的 SQL 吗？并不需要，因为一旦通过 CRUD 了解了基础，它就能很大程度上应付你。对于大多数用途，只有编写数据库支持软件的开发者才需要学习更多语言。

在本节中，你将学习使用 MySQL 和 PostgreSQL 的四个 SQL 语句的基础知识。
现在你可以从两个系统中选择一个进行练习，然后用另一个系统重复一遍。

### 创建

使用 SQL 创建任何内容通常涉及两条语句：`CREATE TABLE` 和 `INSERT`。通过 `CREATE TABLE` 命令，我们可以在数据库中创建表以及如键之类的辅助结构。当表被创建后，我们可以使用 `INSERT` 向其中添加条目。

接下来的练习将为一个虚构的故事创建一个数据库，涵盖 PVC Toys，该公司存储作为热门游戏和电影角色的收藏雕像和人偶。你将发布 SQL 语句来创建它们，稍后在其中添加和删除条目。

首先，你将在 `Toys` 数据库中创建一个表，以添加属性等信息。表是数据库存储信息的 Basic要求之一。要创建一个表，你将使用 `CREATE TABLE` 命令，其语法如下：

```
CREATE TABLE table_name (
  attribute_1 attribute_1 type,
  attribute_2 attribute_2 type,
  attribute_N attribute_N type
);
```

`table_name` 参数是要要创建的表名。`attribute_1` 是表中第一个属性的，`attribute_type` 是该属性将要持有的数据类型。表 12-2 总结了我们在 `toys` 数据库中制作 `statues` 表的计划。

表 12-2. statues 表的结构

| 属性名称 | 属性类型 |
|---||---|
| statuecode | integer |
| statename | varchar(100) |

`statuecode` 属性将接收表中已有的许多条目，为其选定的数据类型是 `integer`。这将有助于跟踪有多少条目，并为你提供一个唯一标识。`statename` 属性将接收许多雕像和人偶的名字，我们选择 `varchar` 作为可以接受最多 100 个字母的数据类型。`varchar` 数据类型实际上可以持有多达 255 个字符，但目前 100 个足够了。表 12-2 中的符号告诉 `CREATE TABLE` 命令 `statename` 属性在字母数量上的大小。这对于你的玩具来说应该足够了！

列表 12-3. 你的第一个 CREATE TABLE 命令

```
CREATE TABLE statues (
  statuecode integer,
  statename varchar(100)
);
```

# 第 12 章 开源数据库

你在这里可以看到 `attribute_1` 是 `statecode`，而 `attribute_1_type` 是 `integer`。同样，`attribute2` 是 `statename`，其类型是 `varchar`。我们填入属性名称来创建 `statues` 表。在你正在运行的数据库终端上运行此命令，表将被创建，如图 12-7 所示。

```
CREATE TABLE statues (
statuecode integer,
statename varchar(100)
);
```

图 12-7. 创建表
