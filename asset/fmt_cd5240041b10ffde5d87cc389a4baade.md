
使用 `DATABASE CONFIGURATION` 显示当前值。

使用 `DATABASE CONFIGURATION USING <parameter>` 更改当前值。

使用 `RESET DATABASE CONFIGURATION` 将所有数据库参数重置为默认值。

使用 `CONFIGURE` 让 DB2 决定值。

示例 3-35 显示了 DBM 参数更改的示例。

```
db2 get db cfg
db2 update db cfg using DFT_MON_BUFPOOL on automatic
db2 get cfg show detail
db2 autoconfigure using mem_percent 60 apply db
```

## 3.6.3 数据库配置

为了分配和控制系统资源，DB2 为实例中的每个数据库使用独立的配置文件。该文件名为 `SQLDBON/database_path/$DB2INSTANCE/NODE0000/SQL00001`。

在分区的环境中，`SQLDBCON` 存在于每个数据库分区。因此，每个分区可以有不同的设置。

### 重要数据库配置参数

本节描述了重要的数据库配置参数以及推荐的设置。许多参数由 STMM 处理。我们将在第132页的第3.6节“DB2 配置”中讨论 STMM。

- **`AVG_APPLS`（可以设置为 `AUTOMATIC`）**

此参数让 DB2 了解您的系统中平均有多少个并发应用程序在运行。当设置为 1 时，DB2 会为每个应用程序提供缓冲区池中当前可用内存。更改此参数可能会对性能产生巨大影响。

- **`CATALOGCHE_SZ`**

此参数在内存中存储数据库、表空间、表和索引信息。DB2 在准备执行计划时会首先查找缓存。足够的内存可以避免高开销的磁盘 I/O。通过 `db2 get snapshot for database db_name` 命令并通过以下公式计算命中率：

`100 - ((Catalog cache inserts X 100) / Catalog cache lookups)`

- **`MAXFILOP`**

这是每个应用程序可以打开的文件数。默认值通常太低。打开文件和关闭文件会减慢 SQL 响应时间并消耗 CPU 周期。如果文件正在被关闭，请调整 `MAXFILOP` 的值，直到关闭操作停止。使用命令：

```
db2 get snapshot for database db_name
```

然后查看 "Number of files closed"（关闭的文件数）。如果值大于 0，则增加 `MAXFILOP` 的值。

- **`LOCKTIMEOUT`**

默认设置为 -1，这意味着连接可以一直等待获取所有资源。如果一个连接持有另一个应用程序所需的锁，就会发生死锁问题。为了防止出现过多的死锁，对于 OLTP，将此值设置为 10；对于 DSS，将此值设置为 60。

- **`LOGBUFSZ`**

DB2 在将日志记录写入磁盘之前使用一个缓冲区存储日志记录。如果该值设置为 0，会导致磁盘产生不必要的 I/O。在增加此参数值时，请考虑增加 `DBHEAP` 参数，因为日志缓冲区内存是从数据库堆分配的。

- **`SORTHEAP`（可以设置为 `AUTOMATIC`）**

每个排序操作都有由数据库管理器分配的独立内存量。此参数定义了可以使用的最大排序内存。在增加此值时，还需要检查并可能需要调整数据库管理器配置文件中的 `SHEAPATHRES_SHR` 参数。

- **`DATABASE_MEMORY`（可以设置为 `AUTOMATIC`）**

如果 `DATABASE_MEMORY` 设置为 `AUTOMATIC`，STMM 将根据系统的可用内存以及各种调优区域的需求进行调优。如果此参数设置为固定值，则该特定数据库的内存将限制在该值，STMM 将根据该内存调优各个区域。

- **`DFT_DEGREE`**

值 1 表示没有分区内并行性。值 -1（或 `ANY`）意味着优化器根据处理器数量和查询类型来决定分区内并行程度。

在 OLTP 系统上，请关闭分区内并行性。在 OLAP 系统上，考虑开启分区内并行性，以便大型查询能够利用多处理器系统中的多个 CPU。

> 注意：要查看所有数据库配置参数的完整且详细描述，请参考信息中心：`http://publib.boulder.ibm.com/infocenter/db2luw/v95/index.jsp?topic=/com.mb2.luw.admin.config.doc/c0004555.html`

### 监控和更新数据库配置

您可以通过控制中心（Control Center）或 DB2 命令行来配置 DB2 数据库设置。

#### 控制中心

使用以下步骤更新数据库配置参数：

- 1. 启动控制中心并展开树结构到目标数据库。
- 2. 右键点击目标数据库名称打开弹出窗口并选择“Configure Parameters”（配置参数）（见第143页的图 3-23）。

![](img/f11f73c917561aadc89cbf81db6d9105_164_0.png)

图 3-23 从控制中心更改数据库参数

修改数据库配置有两个选项：

- Configure Parameters 选项：使用此选项更改特定参数。
- Configuration Advisor 选项：此选项等同于 `autoconfig`（自动配置）命令。

**使用 Configure Parameters 选项**

通过在控制中心选择 **Configure Parameters** 选项，会弹出以下窗口（见第144页的图 3-24）。选择参数后，窗口底部的 Hint（提示）处将显示该参数的简要描述。

## 数据库配置 - ITSCOB

选择参数的值字段来更改其值。

| 关键字 (Keyword) | 值 (Value) | 待定值 (Pending Value) | 待定单位 (Pending Va) |
|---|---|---|---|

| COUNTRY | | | |
| DATABASE_LEVEL | 0xc00 | | |
| DB_MEM_THRESH | 10 | | |
| DFT_DEGREE | | | |
| DFT_MTTY_TYPES | | | |
| DFT_QUERYOPT | | | |
| DFT_REFRESH_AGE | | | |
| DFT_SOLMWATH_NA | 1 | | |

图 3-24 更改数据库参数

在完成所有想要更改的操作，点击 OK，所有更改将应用到数据库（见图 3-25）。

![](img/f11f73c917561aadc89cbf81db6d9105_165_0.png)

图 3-25 更新后的确认窗口

#### 使用 Configuration Advisor 选项

Configuration Advisor 是一个智能工具，可以帮助您无需深入了解 DB2 的情况下配置数据库。只需向向导提供有关系统的信息（如负载和连接），向导就会提供更改建议。

![](img/f11f73c917561aadc89cbf81db6d9105_166_0.png)

图 3-26 Configuration Advisor 窗口

完成所有章节后，向导会提供更改建议。您可以选择立即应用或稍后保存。

#### 命令行

您可以使用命令行设置快速方便地执行命令：

- `GET DATABASE CONFIGURATION <db_name>` 显示当前值。
- `UPDATE DATABASE CONFIGURATION <db_name> USING <parameter>` 更改当前值。
- `RESET DATABASE CONFIGURATION <db_name>` 将所有参数重置为默认值。

第146页的示例 3-36 显示了数据库更新示例：

```bash
db2 get cfg for itsodb
db2 update cfg for itsodb using DBHEAP 1200
db2 get cfg for itsodb show detail
```

## 3.6.4 DB2 注册表和环境变量

DB2 的所有设置都存储在环境变量或注册表中。在 Unix 系统上，`DB2INSTANCE`、`DB2NODE`、`DB2PATH` 和 `DB2INSTPROF` 等环境变量通过 `export` 命令设置，并位于 `$INHOME/sqlib/` 中的 `dbprofile` 文件。

注册变量通过 `db2set` 命令设置并重启 DB2。如果注册变量需要布尔参数，`YES`、`1` 和 `ON` 都等同，`NO`、`0` 和 `OFF` 也等同。要设置实例级注册变量，请执行：

```bash
db2 set -i <instance_name> <command>
```

要设置全局注册变量，请执行：

```bash
db2 set -g <command>
```

您可以使用配置助手 (`db2ca`) 或 `db2set` 命令来配置参数和注册变量。更新注册表时，更改不会影响当前运行的 DB2 应用程序或用户。启动后的应用程序将使用新值。

### 重要注册变量

以下是重要的注册变量列表：

- **`DB2_DISABLE_FLUSH_LOG`=OFF**

在线备份完成后，最后一个活动日志文件将被截断、关闭并归档，确保您的在线备份有完整的归档日志用于恢复。

- **`DB2DBDFT`=null`

此注册变量指定用于隐式连接的数据库别名。如果任何应用程序没有连接但包含 SQL 语句，它将连接到 `DB2DBDFT` 中指定的数据库。

- `DB2_PARALLEL_IO` Default=null

此变量允许 DB2 对特定表空间或所有表空间进行并行 I/O 操作。并行度由表空间内容器的预取单元大小（prefetch size）和区大小（extent size）决定。

- `DB2COMM` Default=null

此变量决定了与 DB2 通信时使用的协议。通常，服务器和客户端之间的 TCP/IP 协议接受 S/390 系统的通信。在 Linux 上，TCP/IP 是客户端/服务器通信唯一支持的协议。

- `DB2INSTANCE`（由 DB2 配置文件设置）

在执行 `db2profile` 脚本启用了针对 DB2 的变量后，该环境变量将被设置为当前实例的名称。

> 注意：所有注册表变量的详情请参阅信息 Center：
> `http://publib.builder.ibm.com/infocenter/db2luw/v95/index.jsp?topic=/com.ibm.db2.luw.admin.regvars.doc/doc/c0007340.html`

### 命令行上的 db2set

`db2set` 是设置注册表变量的命令。您可以使用命令提示符执行该命令（示例 3-37）。

示例 3-37 设置和删除注册表变量

### db2ca 图形工具

要启动图形工具，请执行命令 `db2ca &`。在主窗口中，选择配置（Configure）→ DB2 注册（DB2 Registry），如第 148 页图 3-27 所示。

![](img/f11f73c917561aadc89cbf81db6d9105_169_0.png)

图-3-27 从 db2ca 修改注册表

您将进入图 3-28 所示的面板，可以在那里更改注册表变量。

![](img/f11f73c917561aadc89cbf81db6d9105_169_1.png)

图-3-28 修改注册表变量

### 多页文件分配

对于系统管理表空间 (SMS)，我们建议您启用多页文件分配。这减少了格式化新页所需的时间。要启用此参数，请对每个数据库执行 `db2empfa` 命令。这需要独占访问，因为在现有的表空间中，所有空空间将填充到最后一个区。

要检查所有空页是否已填充到最后一个区，请执行命令：

```
db2 get db cfg for <dbname> | grep Multi-page
```

多页文件分配已启用 = YES。

在多分区环境中，请在每个数据库分区上执行 `db2empfa`。

## 3.7 安全性

在本节中，我们简要讨论了 DB2 的安全性。我们介绍了 Linux 层、实例层、数据库层和网络安全性。有关此主题的详细信息，请参阅：

- Linux、UNIX 和 Windows 的 DB2 安全与合规解决方案，SG24-7555
- 数据库安全指南，SC23-5850
- 数据库基础知识 → 安全项下的信息 Center。

### Linux 层的安全性

在 Linux 层上，安全性是以用户和组的形式进行管理的。用户有一个主组和一个多或少的专有用户 ID，运行所有 DB2 数据库实例的用户多或少属于该实例。数据库实例通过 TCP/IP 端口提供网络访问。Linux 层上 DB2 的安全性考虑是基于这一假设。

#### 文件系统权限

在创建实例时，DB2 将所有 DB2 内容放置在实例用户的家目录下。这些文件必须允许想要使用该实例的用户访问。

您创建的所有后续文件（例如表空间容器、事务日志、归档日志、备份、诊断日志等）不需要用户直接访问。因此，您可以将它们的权限限制为仅实例用户访问。

许多 Linux 系统默认将 `umask` 设置为 0022，这使得所有新创建的文件对所有人都是可的。如果担心安全性，请为实例用户将 `umask` 设置为 0027。

UDF（用户定义函数）和存储过程可以配置为在围栏（fenced）用户 ID 下运行，以保护 UDF 免受数据库管理器核心的影响。因此，崩溃的 UDF 不会导致数据库管理器崩溃。尽管在围栏用户 ID 下运行 UDF 和存储过程会给 UDF 调用增加开销。

使用围栏用户 ID 还有另一个用途。它允许它们在与数据库管理器不同的用户 ID 下运行。因此，它们无法直接访问数据库实例的文件。它还可以防止溢出占用过数据库资源。

围栏用户 ID 在创建实例期间定义。

#### 权限

DB2 实例级权限 `SYSADM`、`SYSMAINT` 和 `SYSMON` 通过操作系统组授予。每个 DB2 实例级权限都为实例的数据库提供特定程度的访问和权限。在数据库管理器配置中，您可以定义哪些 Linux 组分配给哪些权限。授权组在数据库管理器配置中指定，如示例 3-38 所示。

示例 3-8 实例级权限

```
db2inst11> db2 get dbm config | grep _GROUP
SYSADM group name (SYSADM_GROUP) = DB2ADM1
SYSCTRL group name (SYSCTRL_GROUP) =
SYSMAINT group name (SYSMAINT_GROUP) =
SYSMON group name (SYSMON_GROUP) =
```

### 网络层安全性

如果启用了网络，数据库管理器会打开一个 TCP/IP 端口，供 DB2 客户端通信。默认情况下，服务器之间的通信是不加密的。如果您需要保护数据，可以启用安全套层 (SSL) 或身份验证。

身份验证类型在数据库管理器配置中定义，如示例 3-39 所示。

示例 3-39 数据库管理器中的身份验证

```
db2inst1> db2 get dbm config | grep AUTHICATION
Database authentication (AUTHENTICATION) = SERVER
```

### 数据库层安全性

在数据库层，可以使用权限和授权控制访问。DB2 提供的安全性机制包括：

- 管理员的权限
- 用于限制访问数据的视图
- 用于限制访问 DB2 对象的权限
- 用于限制访问函数的包
- UDF 和存储过程
- 提供比 Linux 组更详细的安全实现方式的角色
- 即使是 DBA 也能保护数据的加密
- 基于标签的访问控制 (LBAC) 用于限制列和行级访问
- 用于解决多层架构引入问题的信任上下文

#### 权限

在数据库层，可以对以下类型授予权限：

- 模式
- 表空间
- 表和视图
- 包
- 序列
- 过程

权限可以授予：

- Linux 用户
- Linux 组
- DB2 角色
- PUBLIC

授予权限时请使用 `GRANT` 语句。

#### 加密

如果您需要保护敏感数据（如信用卡信息），可以使用内置函数 `ENCRYPT`、`DECRYPT_BIN` 和 `DECRYPT_CHAR`。加密允许您保护数据免受数据库管理员的访问。

#### 默认值

当最初创建数据库时，将以下权限授予 PUBLIC：

- CREATE TABLE
- BINDADD
- CONNECT
- IMPSCHEMA
- 对 NULLID 模式下创建的所有包的 BIND
- 对 NULLID 模式下创建的所有包的 EXECUTE
- SQLJ 模式的 CREATEIN
- NULLID 模式的 CREATEIN
- USSPACE1 表空间的 USE
- 对 SYIBM 表的 SELECT
- 对 SYSCAT 视图的 SELECT
- 对 SYSSTAT 视图的 SELECT
- 对 SYSSTAT 视图的 UPDATE
- 对 SQLJ 模式下所有过程的 GRANT EXECUTE
- 对 SYSPROC 模式下所有函数和过程的 GRANT EXECUTE

如果您不需要这些权限，可以在 CREATE DATABASE 命令中指定 `RESTRICTIVE` 选项。

## 3.8 客户端配置

在本节中，我们讨论如何使用图形工具 Configuration Assistant 或 DB2 命令行处理器安装和配置 DB2 客户端。

DB2 客户端提供对 DB2 数据库服务器的访问。在 DB2 9.5 中，有三种 DB2 数据服务器客户端可用：

- IBM Data Server Client 这是一个完整安装。它包含了所有组件，以及图形和非图形工具，用于管理 DB2 系统和使用 DB2 开发应用程序。该客户端还包括适用于 Eclipse 和 Microsoft® Visual Studio® 2005 开发环境的插件。

如果您需要数据库管理支持以及使用应用程序编程接口（API）进行应用程序开发，请使用此客户端。

## IBM Data Runtime Client
