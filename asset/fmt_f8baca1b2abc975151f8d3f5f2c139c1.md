
您可以使用 `db2_all` 命令检查设置。在示例 3-5 中，`db2_all` 命令用于查询两个物理节点上的日期。

## 示例 3-5 db2_all 示例命令

```
db2inst1@udb1nx02:"/sqllib> db2_all date

Mon Oct 21 17:06:28 PDT 2002
udb1nx02: date completed ok

Mon Oct 21 17:06:28 PDT 2002
udb1nx02: date completed ok

Mon Oct 21 17:16:35 PDT 2002
udb1nx05: date completed ok

Mon Oct 21 17:16:35 PDT 2002
udb1nx05: date completed ok
```

现在您可以在多主机、多分区环境中启动 DB2。为此，在任意主机上输入 `db2start` 命令。参考示例 3-6。

## 示例 3-6 启动具有四个分区的 DB2 实例

```
db2inst1@udb1nx02:> db2start
11-01-2002 15:10:51  1  0  SQL1063N  DB2START processing was successful.
11-01-2002 15:10:51  0  0  SQL1063N  DB2START processing was successful.
11-01-2002 15:10:52  3  0  SQL1063N  DB2START processing was successful.
11-01-2002 15:10:53  2  0  SQL1063N  DB2START processing was successful.
SQL1063N  DB2START processing was successful.
```

> 注：`db2_all` 是 DB2 提供的一个 shell 脚本，允许您向一个或所有数据库分区发送命令。

### 3.3 创建数据库

创建数据库时，将为您完成以下任务：

- 设置数据库所需的所有系统目录表
- 在创建新数据库期间，DB2 分配三个表空间：`SYSCATSPACE`、`USERSPACE1` 和 `TEMP SPACE1`。表空间 `SYSCATSPACE` 包含所有系统目录表。这些目录表实际上是一个存储库，用于保存有关数据库中所有对象的相关信息和统计数据。`USERSPACE1` 包含用于保存用户创建表的表。DB2 需要一个系统临时表空间（`TEMP SPACE1`）来支持排序数据、连接表、创建索引等活动。
- 分配数据库恢复日志
- DB2 恢复日志跟踪对数据库所做的所有更改。它也称为事务日志。它与恢复历史文件一起使用，以在发生故障时恢复数据。
- 创建数据库配置文件并设置默认值

数据库配置文件用于向 DB2 提供信息，例如它可以使用多少内存、日志需要存储在哪里以及 DB2 优化器相关信息。

- 将数据库实用程序绑定到数据库

包含 SQL 语句的程序必须绑定到数据库。此绑定过程用于 DB2 实用程序，如 `import` 和 `load`。

在现有实例中创建数据库有两种方法：

- DB2 Create Database Wizard，这是一个基于 JAVA 的图形工具
- 从命令行处理器窗口使用 `create database` 命令

在创建多分区数据库之前，您应考虑哪个分区将成为目录节点。在分区数据库环境中，`create database` 命令会影响 `db2nodes.cfg` 文件中列出的所有数据库分区。发出此命令的数据库分区节点将成为新数据库的目录数据库分区。

> 提示：在具有多个分区的<|message|> 上，每条命令或 SQL 语句默认情况下都会在该主机的第一个分区上运行。要在其他分区上运行命令或 SQL 语句，您需要通过设置 `DB2NODE` 变量来指定节点。

> 例如，主机 `udb1nx02` 具有分区号 0 和 1。如果您发出 `export DB2NODE=1` 命令，并且它继续或随后执行 `db2 terminate` 命令，则每条语句现在将在分区 1 上运行。

您必须具有 `sysadm` 或 `sysctrl` 授权才能创建新数据库。在创建数据库之前，请在您希望存储数据库文件的所有文件系统或目录上设置正确的权限。默认情况下，数据库将在由数据库管理器配置变量 `dftdbpath` 确定的路径中创建并编目。您可以通过输入以下命令将其更改为您想要的默认路径：

```
db2 update dbm cfg using DFTDBPATH /database
```

#### 3.3.1 创建数据库向导

如果您以单分区模式安装了 DB2，那么创建数据库最简单的方法是使用创建数据库向导。DB2 实例已在 DB2 安装期间创建，如 2.3“安装 DB2”第 52 页所述。创建数据库向导也可以用于创建多分区数据库。您可以从控制中心启动“创建数据库向导”，如图3-2所示。

![](img/d95c931f4f3da4a6bd0ee55148fefad7_99_0.png)

图3-2 控制中心中的创建数据库向导

- 展开对象树，直到找到Databases文件夹。
- 右键单击Databases文件夹，然后从弹出菜单中选择Create --> Database Using Wizard。参见图3-2。

图3-3 创建数据库向导的起始窗口

图3-3展示了“创建数据库向导”窗口，我们需要在此命名数据库和数据库目录。所有与数据库相关的文件都将存储在此目录路径下，例如，对于此实例中的第一个数据库：

```
/database/DB2INSTANCE/NODE0000/SQL00001/
```

创建数据库后，执行以下命令以查看数据库存储在哪个目录中：

```
db2 list database directory on /database
```

示例3-7 list database directory的输出

```
db2inst1@db2blnx02:~> db2 list db directory on /database

Local Database Directory on /database

Number of entries in the directory = 1

Database 1 entry:
```

数据库别名 = ITSOSJ

数据库名称 = ITSOSJ

数据库目录 = SQL00001

数据库发布级别 = a.00

注释 = ITSO San Jose

目录条目类型 = Home

编目数据库分区号 = 0

数据库分区号 = 0

![](img/d95c931f4f3da4a6bd0ee55148fefad7_101_0.png)

图3-4 表空间容器定义

在此窗口（图3-4）中，我们需要决定DB2应将默认表空间`userspace1`存储在哪里，以及它应是什么类型。SMS（系统管理存储）表示表空间容器是给定路径下的一个目录，所有数据将以文件形式存储在其中。DMS（数据库管理存储）表示表空间容器是一个由DB2控制的预分配文件。

在接下来的两个窗口中，我们需要决定编目表空间`syscatspace`和临时表空间`temspace1`的位置。我们建议您将`temspace1`分配到不同的文件系统中。更多细节请参考第36页2.2.2“存储规划”中的描述。

图3-5 表空间I/O定义

调整此数据库的性能（图3-5）是一个重要的窗口，您需要在此决定DB2应如何读写数据。我们建议您选择Prefetch size为Extend size的倍数，以便DB2在需要数据之前从磁盘读取数据（预取）。每次DB2需要表中的数据时，它都会发出一个I/O请求。这样的请求会从磁盘请求一个extent。如果您允许DB2一次获取更多数据，那么您将减少I/O等待时间。

图3-6 验证生成的SQL

完成所有预览窗口后，如果您选择Show Command，向导将呈现一个窗口（图3-6），其中包含生成的数据库命令以及您指定的所有设置。通过关闭此窗口并单击Finish，DB2将为您创建数据库。随后将显示一条包含配置选项的数据库创建成功确认消息，如图3-7所示。

图3-7 创建数据库的确认

# 图3-9 指定新的日志路径

在图3-9中，我们将日志路径更改为新位置，同时开启新的镜像日志功能。我们为主日志路径和辅助日志路径选择了不同的文件系统。

在所有连接被释放并发出新连接或`activate database`命令后，新路径将生效。更快地更改并激活新路径的方法是执行以下命令：

```
db2 connect to itsosj
db2 update db cfg for itsodb using NEWLOGPATH /db2log1/db2inst1/itsosj
```

```
db2 update db cfg for itsodb using MIRRORLOGPATH
/db2log2/db2inst1/itsosj
```

```
db2 deactivate database itsosj
db2 activate database itsosj
```

要完成数据库配置，请再次打开控制中心，并按您的需要配置数据库。
