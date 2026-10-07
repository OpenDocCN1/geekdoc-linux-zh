
日志参数也可以在命令行中心（Command Center）中更改。右键点击所有数据库下的数据库，选择“配置数据库”。在这里你可以更改日志参数、应用更改并保存。

## 3.4.2 更改归档日志路径

默认情况下，新数据库设置为循环日志。在这种日志类型下，仅允许数据库的全备和离线备份。对于恢复，数据库只能恢复到上一次离线备份，而无法恢复到故障点。

为了能够将数据库完全恢复到特定的时间点，必须启用归档日志。这些归档日志随后被 `restore` 命令用于恢复到当前时间点。第 6 章第 227 页“管理数据库”详细说明了归档日志路径的设置。

## 3.4.3 更改 db2diag.log 的路径

DB2 日志信息、管理事件或诊断文件 `db2diag` 中的错误。这是一个实例级日志文件，默认位于 `<instance home>/sqldb/db2dump`。定期检查此文件是一个良好的习惯。该文件通常包含有关多个 DB2 命令的附加信息，特别是那些与操作系统交互的命令（如创建表空间）。在 `db2diag.log` 文件中，你可以看到关于错误路径、权限问题、错误代码等信息。

`db2diag.log` 中记录的详细程度由 `DIAGLEVEL` `DBBM` 配置参数指定，范围从 0 到 4。默认值为 3。数字越大，记录的信息越多。设置为 4 可能会对数据库产生性能影响。

由于 `db2diag.log` 文件会不断增长，你需要维护 `db2dump` 目录。

```
示例 3-25 重定位 db2diag.log
db2inst@puget:> db2 get db config | grep DIAGPATH
诊断数据路径 (NEWLOGPATH) = /db26log1/ITSODB
DB2001 THE UPDATE DATABASE command completed successfully.
dbinst1@puget:~$ db2 get config for itsodb
```

## 3.5 添加数据库分区

如果分区数据库的负载过高，可以添加分区以利用并行环境。本节描述了这些步骤。

在分区数据库中，你可以使用 `addpartitionnum` 命令行处理器（CLP）或使用带有 `dbpartitionnum` 的 `db2start` 命令对已填充的数据库进行操作。

## 示例 3-27 添加 dbpartitioning 工具命令

```
db2inst1@mensa:~/sqllib export DB2NODE=2
db2inst1@mensa:~/sqllib db2 terminate
db2inst1@mensa:~/sqllib db2 add dbpartitionum without tablespaces
```

DB200001 ADD NODE 命令成功完成。

DB2 现在已经在 `/database` 中创建了目录结构，但由于 `without tablespaces` 关键字，分区 0 和 1 中的现有表空间并未在新分区中创建。用于 `IBMTEMPGROUP` 的数据库分区组已扩展到新的数据库分区 2，我们必须为新分区上的 `TEMSPACE1` 添加一个表空间容器。参见示例 3-28。

## 示例 3-28 为临时空间添加表空间容器

```
db2inst1@mensa:~"db2 alter tablespace tempspace add
('/db/db2inst1/NODE002/ITS008/TEMPSPACE1') on dbpartitionum (2)"
db200001 SQL 命令成功完成。
```

所有将从新分区中受益的数据库分区组都将进行修改，以便可以使用新分区。首先，我们在表空间 `SAMPLE_SNG` 中创建一张表，该表位于分区组 `SNG_01`（示例 3-29）。

## 示例 3-29 在 SNG_01 中创建表

connect to itsdb;

```
CREATE TABLE PART1(P_PARTKEY INTEGER NOT NULL,
P_NAME VARCHAR(55) NOT NULL,
P_MFR CHAR(25) NOT NULL,
P_BRAND CHAR(10) NOT NULL,
P_TYPE VARCHAR(25) NOT NULL,
P_SIZE INTEGER NOT NULL,
P_CONTAINER CHAR(10) NOT NULL,
P_RETAILPRICE FLOAT NOT NULL,
P_COMMENT VARCHAR(23) NOT NULL
) IN SAMPLE_SNG);
```

```
ALTER TABLE PART1 ADD PARTITIONING KEY (P_PARTKEY);
```

第 127 页的示例 3-30 显示了我们数据库 `ITSODB` 中针对 `SNG_01` 的语句。

## 示例 3-30 修改数据库分区组 SNG_01

db2inst1mena:\> db2 'alter database partition group sng_01 add

dbpartitionum(2) without tablespaces'

SQL1759 需要重新分配数据库分区组以更改无组 'SNG_01' 中对象的数据库分区，以包含某些添加的数据库分区或排除某些删除的数据库分区。SQLSTATE=01618

消息 SQL1759W只是一个警告，表示此数据库分区组中的所有表都将被重新分配，但所有表仍然可以访问。

然后，我们为 `SNG_01` 添加表空间容器（示例 3-31）。

## 示例 3-31 为 SNG_01 添加表空间容器

```
db2inst1mena:\> db2 "alter tablespace SAMPLE_SNG" add
('/db2inst1/NODE0002/ITSDB/SAMPLE_SNG") on dbpartitionum(2)
SQL1759 需要重新分配数据库分区组以更改无组 "SNG_01" 中对象的数据库分区，以包含某些添加的数据库分区或排除某些删除的数据库分区。SQLSTATE=01618
```

重新分配命令影响给定数据库分区组中的所有表空间和表。然而，重新分配是在线进行的，且所有表索引仍然可以完全访问。

要重新分配数据库分区组 `SNG_01` 中的所有数据，请登录到目录分区所在的主机，连接到数据库并执行重新分配命令。

## 示例 3-32 为 MPL_01 的重新分配命令

```
db2inst1mena:\> db2 redistribute database partition group sng_01 uniform
DB200001 REDISTRIBUTE NODEGROUP 命令成功完成。
```

> 注意：你也可以在 `REDISTRIBUTE` 命令中使用 `ADD DBPARTITIONS AT` 选项，它结合了 `ALTER DATABASE PARTITION GROUP` 和 `REDISTRIBUTE DATABASE PARTITION GROUP` 命令。

对于每个已处理的表，重新分配工具会将一个消息写入文件 `$INSTHOME/sqlib/redist/<dbname>.<part-group>.<time>` 中。参见示例 3-33。

## 示例 3-33 重新分配示例

数据重新分配工具：

指定了以下选项：

数据库分区组名称：SNG_01

数据重新分配选项：U

重新分配数据库分区组：均匀地

要添加的分区数：1

要添加的分区列表：

2

要删除的分区数：0

要删除的分区列表：

删除将与插入并行进行。

在以下执行数据重新分配操作：

| 开始 | 结束 | 表 (poolID;objectID) |
| :--- | :--- | :--- |
| 18.19.49 | | "DB2INST1","PART1" (4;2) |
| 18.19.49 | | "DB2INST1","PART1" (4;2) |

所有表已成功重新分配。

**重要：** 重新分配工具会发出 SQL 插入和删除操作；因此，确保有足够的日志空间。重新分配是一个极其耗时的过程，必须在应用程序未使用这些表时进行。

依赖于被重新分配表的 DB2 包被设置为无效。DB2 包在第一次收到 SQL 请求时会自动重新绑定以节省延迟时间，请使用 `rebind` 命令手动重新绑定这些包。

我们建议你通过执行 `runstats` 命令来更新统计信息并重新绑定受影响的包。

> 注意：关于添加数据库分区的更多信息请参阅《分区与集群指南》，SC23-5860。

添加逻辑数据库分区的另一种方法是使用添加数据库分区向导程序（第 129 页的图 3-14）。

![](img/f11f73c917561aadc89cbf81db6d9105_150_0.png)

图 3-14 为数据库添加分区

向导程序将引导你完成整个过程。

## 3.6 配置

DB2 有许多配置参数，用于指定系统资源的分配以及实例和数据库的整体配置。这些参数存储在数据库配置、数据库管理器配置和注册表中。

由于默认值是针对内存和存储较小的机器的，你可能需要对其进行修改以适应你的环境。配置的良好起点是配置顾问或 `AUTFIGURE` 命令。

如果你创建一个数据库，许多参数已设置为 `AUTOMATIC`，以便由自适应内存管理进行处理。

### 3.6.1 STMM：自适应内存管理

在第 9 版本中，DB2 引入了一项新功能自适应内存管理（STMM），通过自动设置多个内存配置参数的值极大简化了数据库内存配置。STMM 管理以下 DB2 消费者的内存：

- 缓冲区池
- 包缓存
- 锁内存
- 排序内存

这些区域的调优可以单独开启。调优是在同一系统的不同数据库和不同实例之间进行的。调优内存可以被限制。如果无法从操作系统分配更多调优内存，或者内存达到了定义的限制，则将从不需要那么多内存的区域提取可用内存。例如，如果 STMM 发现某个缓冲区池需要更多内存，它可以从另一个池中提取。

调优频率根据工作负载确定，每个调优步骤都会记录在 `dbdiag.log` 和 `stmml` 目录。

STMM 也适用于分区数据库，但这种情况下每个系统的硬件必须相同。而且工作负载和数据必须均匀分布，因为调优参数是在称为调优分区的指定的指定的，然后分到其他分区。

第 134 页的图 3-19 展示了内存空间如何在各个区域之间进行分配。

## Linux

![](img/f11f73c917561aadc89cbf81db6d9105_155_0.png)

图 3-19 STMM

对于新创建的数据库，自调优功能默认开启。我们可以从示例 3-34 显示的数据库配置参数看出这一点。

示例 3-34 为 STMM 调优参数

```
db2inst@puget: db2 get db config for innodb | grep -i automatic
Size of database shared memory (4KB) (DATABASE_MEMORY) = AUTOMATIC
Max storage for lock list (4KB) (LOCKLIST) = AUTOMATIC
(MAXLOCKS) = AUTOMATIC
Percent. of lock lists per application = AUTOMATIC
Package cache size (4KB) (PCKCACHE) = AUTOMATIC
Sort heap for shared parts (4KB) (SHEATHRES_SH) = AUTOMATIC
Sort list heap (4KB) (SORTHEAP) = AUTOMATIC
Database heap (4KB) (DBHEAP) = AUTOMATIC
SQL statement heap (4KB) (STMTHEAP) = AUTOMATIC
Default application heap (4KB) (APPLHEAPS) = AUTOMATIC
Application Memory Size (4KB) (APPL_MEMORY) = AUTOMATIC
Statistics heap (4KB) (STAT_HEAP_SZ) = AUTOMATIC
Number of asynchronous page cleaners (NUM_IOCLEANERS) = AUTOMATIC
Number of I/O servers (NUM_IOSERVERS) = AUTOMATIC
Default prefix size (pages) (DFT_PREFETCH_SZ) = AUTOMATIC
```

134 在 Linux 上上手运行 DB2

Max number of active applications (MAXAPPLS) = AUTOMATIC

Average number of active applications (AVG_APPLS) = AUTOMATIC

要关闭特定区域的 STMM，请使用此命令：

```
UPDATE DATABASE CONFIGURATION USING <parameter> MANUAL
```

你可以通过执行此命令来通用关闭 STMM：

```
UPDATE DATABASE CONFIGURATION USING SELF_TUNING_MEM
```

可以使用 `SIZE AUTOMATIC` 选项单独为启用或禁用缓冲池的 STMM：

```
ALTER BUFFERPOOL ibdefaultbp SIZE AUTOMATIC
```

```
CREATE BUFFERPOOL <bpname> SIZE AUTOMATIC
```

STMM 可以以两种模式运行：

- 你可以限制内存调优可用大小小于此值。如果某个区域需要 `DATABASE_MEMORY` 参数，那么 STMM 将不会让数据库使用的内存超过此值。如果某个区域由于需求增加而需要增加内存，另一个内存需求较小的区域将相应地减少。
- 你可以通过将 `DATABASE_MEMORY` 参数设置为 `AUTOMATIC` 来保持可用调优内存大小不受限。在这种情况下，操作系统中的可用内存限制了调优的可用内存。STMM 会为操作系统进程留出缓冲区，以防止发生分页（paging）。
- 你还可以通过设置数据库管理器配置参数 `INSTANCE_MEMORY` 的值来限制实例使用的内存。如果你不想限制它，可以将其值保持为 `AUTOMATIC`。

> 注意：某些 Linux 内核不允许你将 `DATABASE_MEMORY` 数据库参数的值设置为 `AUTOMATIC`。RHEL5 和 SUSE 10 SP1 支持 `AUTOMATIC` 值。对于所有经过验证 Linux 发行版，如果内核不支持此功能，将返回 `COMPUTED`。

## 3.6.2 数据库管理器配置参数

数据库管理器配置 (`DBM cfg`) 参数存储在 `$INHOME/sqlib/` 下名为 `db2system` 的文件中。要修改这些参数，请使用图形界面、控制中心或 DB2 命令行界面。

## 重要的 DBM cfg 参数

以下是重要的 DBM cfg 参数：

- `DFTDBPATH`

默认情况下，此参数设置为 `$INHOME`。我们建议将其设置为你所需的路径。在分区的环境中，`$INHOME` 通常位于 NFS 文件系统上，但 DB2 不支持将 NFS 作为数据库路径。

- `DFT_MONSWITCHES`

将所有监控开关设置为 `ON` 以让 DB2 收集统计数据。使用快照（snapshot）命令显示有关 DB2 行为的详细信息。

- `DIAGLEVEL`

为了确定问题，将 `DIAGLEVEL` 设置为 4。DB2 将所有错误、警告和信息消息写入 `DIAGPATH` 定义的路径下的 `db2diag.log`。默认值为 3。请注意，日志级别 4 可能会对性能产生严重影响。

- `MON_HEAP_SZ`（可以设置为 `AUTOMATIC`）

用于维护数据库系统监视数据私有视图所需的内存由 `MON_HEAP_SZ` 配置参数分配。监控活动所需的内存量在很大程度上取决于监控应用程序和事件监视器的数量、设置的开关以及数据库活动的水平。

- `SHEATHRES`

对于私有排序，此参数是实例级范围内在任何时刻私有排序可以消耗内存的软限制。对于共享排序，此参数是数据库级范围内在任何时刻共享排序消耗内存内存的硬限制。达到此限制后，将不再允许进行共享排序。

- `NUM_POOLAGENTS`（可以设置为 `AUTOMATIC`）

对于应用程序并发连接的决策支持系统 (DSS) 环境，请将此值设小。对于具有许多并发连接应用程序的在线事务处理 (OLTP)，请将此值设大一些，以防止创建额外的 `db2agents`，这是非常耗时的。

- `INTRA_PARALLEL`

对于 OLTP 环境，将此值设置为 `NO`，因为吞吐量比并行工作更重要。OLTP 查询更新或插入少数行，因此将此工作拆分到多个进程中没有意义。在 DSS 环境中，查询通常一次连接多个表。我们建议将此值设置为 `YES`。

- `MAX_QUERYDEG`

对于 OLTP，将此值设置为 1。对于 DSS，DB2 可以将工作拆分到多个进程中。

- `INSTANCE_MEMORY`（可以设置为 `AUTOMATIC`）

如果设置为 `AUTOMATIC`，它将在实例启动时计算。

- `JAVA_HEAP_SIZE`

`JAVA_HEAP_SIZE` 定义了用于 Java 定义函数 (UDF) 的堆大小。

- `SVCNAME`

`SVCNAME` 定义了实例使用的端口。

## 监控和更新 DBM 配置

你可以通过控制中心或 DB2 命令行来配置设置。

## 控制中心

使用以下步骤设置 DBM 配置：

1. 启动控制中心并扩展树到所需的实例。
2. 右键点击实例名称打开弹出窗口并选择参数（图 3-20）。

![](img/f11f73c917561aadc89cbf81db6d9105_159_0.png)

图 3-20 配置参数

3. 进行你的更新并勾选（动态）选项（图 3-21）。
4. 在完成所有所需的更改后，点击确定，更改将应用（图 3-22）。

![](img/f11f73c917561aadc89cbf81db6d9105_160_0.png)

图 3-21 修改参数

## 命令行

更改 DBM 配置设置的命令可以由命令行处理器方便地输入。
