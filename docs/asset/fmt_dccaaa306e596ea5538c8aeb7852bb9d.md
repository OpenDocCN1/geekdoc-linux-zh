
```
db2inst1@mensa:> db2 "restore itsdb from /db2backup taken at
2008022006143831 logarget /db2backup/logs"
DB200001 The RESTORE DATABASE command completed successfully.
```

```
db2inst1@mensa:> db2 "rollforward itsdb to end of backup overflow log path
(/db2backup/logs)"
```

## 重滚状态

| 输入数据库别名 | 返回状态的节点数 |
| :--- | :--- |
| itsoddb | 1 |

| 节点数 | 重滚状态 | 下一个读取的日志文件 | 已处理的日志文件 | 最后提交的事务 |
| :--- | :--- | :--- | :--- | :--- |
| 0 | DB working | S0000001.LOG | S0000000.LOG - S0000000.LOG | 2008-02-06-22.38.32.000000 UTC |

DB200001 The ROLLFORWARD command completed successfully.

```
db2inst1@mensa:> db2 "rollforward db itsdb stop"
```

## 重滚状态

| 输入数据库别名 | 返回状态的节点数 |
| :--- | :--- |
| itsoddb | 1 |

| 节点数 | 重滚状态 | 下一个读取的日志文件 | 已处理的日志文件 | 最后提交的事务 |
| :--- | :--- | :--- | :--- | :--- |
| 0 | not pending | S0000001.LOG - S0000000.LOG | 2008-02-06-22.38.32.000000 UTC |

DB200001 The ROLLFORWARD command completed successfully.

## 使用增量备份进行全数据库恢复

恢复增量备份映像的最佳方法是使用 `AUTO` 选项。DB2 将收集所需的备份映像（全量和增量备份）以恢复数据库：

```
db2 restore db itsdb incremental from /db2backup taken at 200802049192
```

如果你想知道恢复增量备份需要哪些备份映像，可以使用 `db2crst` 命令：

```
db2crst -d itsdb -t 2008020491912
```

该命令查询数据库历史记录，并生成备份映像的时间戳列表以及建议的恢复顺序。

## 重滚恢复

要使用重滚恢复方法，数据库必须配置为可恢复的数据库。在恢复操作结束时，数据库将处于重滚等待（rollforward pending）状态，这使你能够将数据库向前重滚到特定的时间点或日志末尾。

> 注意：使用 `RESTORE` 和 `ROLLFORWARD` 命令恢复和向前重滚数据库涉及多个步骤。或者，你可以使用 `RECOVER` 命令通过一个命令即可恢复并向前重滚数据库：

```
db2 recover database itsdb
```

`RECOVER` 命令读取数据库文件以获取恢复和向前重滚数据库的所有必要信息。

你可以使用命令检查重滚过程的进度：

```
db2 rollforward db itsdb query status
```

使用 `rollforward` 命令，你可以指定时间戳或日志结束点，这告诉数据库需要向前重滚多远。

重滚恢复有两种类型：

- 数据库向前重滚：

此过程将记录在数据库日志中的事务应用到数据库中。重滚工具会读取所需的日志（归档日志或活动日志文件）。已归档的日志将使用日志归档方法检索。将数据库向前重滚到尽可能远的最简单方法是使用以下命令：

```
db2 "rollforward db itsdb to end of logs and stop"
```

如果你需要将数据库向前重滚到特定的时间点，请使用以下命令：

```
db2 "rollforward db itsodb to 2008-02-06-20.15.30 using local time"
db2 "rollforward db itsodb query status"
db2 "rollforward db itsodb stop"
```

## 表重滚恢复

如果数据库启用了向前恢复，你可以选择备份、恢复和向前重滚表空间，而不是整个数据库。你可以对表空间进行重滚恢复到日志末尾或特定时间点。你指定的时间点必须大于或等于该表空间的最小恢复时间。6-22 显示了如何确定该时间。

## 示例 6-22 恢复到最小时间点

```
db2inst1mens:> db2 "restore db itsodb tablespace (userspace) online
from/db2backup taken 20080206145105"
DB200001 The RESTORE DATABASE command completed successfully.

---- 从另一个登录 shell 中，查找最小恢复时间 -----
db2inst1mensa:> db2 connect to itsodb
```

| 表空间 ID | 名称 | 类型 | 内容 |
| :--- | :--- | :--- | :--- |
| 0 | SYSPACE | Database managed | All |
| 1 | TEMPORARY | System managed | System |
| users | userspace | Database managed | Regular |

command。在实用程序的运行期间，您可以使用 `LIST UTILITY` 命令来监控 `RESTORE` 和 `ROLLFORWARD` 实用程序。也可以使用管理视图 `SNAPUTIL` 和 `SNAPUTIL_PROGRESS` 或表函数 `SNAP_GET_UTIL` 和 `SNAP_GET_PROGRESS` 获取相同的信息。示例 6-23 显示了数据库分区 0 表空间以及随后的 rollforward 的输出。

## 示例 6-23 恢复和 rollforward

```
db2inst1@mensa:> db2 list
```

```
ID = 331
Type = RESTORE
Database Name = ITSODB
Partition Number = 0
Description = tablespace TSDATA2...
Start Time = 02/21/2008 15:23:01.033971
State = Executing
Invocation = User
```

```
db2inst1@mensa:> db2 list utilities show detail
```

```
ID = 331
Type = RESTORE
Database Name = ITSODB
Partition Number = 0
Description = tablespace TSDATA2...
Start Time = 02/21/2008 15:23:01.033971
State = Executing
Invocation = User
```

```
Progress Monitoring:
Completed Work = 54837248 bytes
Start Time = 02/21/2008 15:23:01.033976
```

```
db2inst1@mensa:> db2 "select UTILITY_TYPE, substr(UTILITY_DESCRIPTION,1,15), UTILITY_STATE,DBBPARTITIONNUM FROM SYBMADM.SNAPUTIL"
```

```
UTILITY_TYPE UTILITY_STATE DBBPARTITIONNUM
-------------------------------------------
RESTORE tablespace TSDA EXECUTE 0
record(s) selected.
```

```
db2inst1@mensa:> db2 "select SNAPSHOT_TIMESTAMP, UTILITY_STATE, PROGRESS_START_TIME, PROGRESS_TOTAL_UNITS, PROGRESS_COMPLETED_UNITS, DBBPARTITIONNUM FROM SYBMADM.SNAPUTIL_PROGRESS"
```

```
SNAPSHOT_TIMESTAMP UTILITY_STATE PROGRESS_START_TIME
PROGRESS_TOTAL_UNITS PROGRESS_COMPLETED_UNITS DBPARTITIONNUM

---------------------------------------------------------------------------------
---------------------------------------------------------------------------------
2008-02-21-15.23.523409 EXECUTE 2008-02-21-15.23.013976
54837248 0

1 record(s) selected.
```

```
db2inst1@mens:> db2 list utilities

ID = 332
Type = ROLLFORWARD RECOVERY
Database Name = ITS00B
Partition Number = 0
Description = Online Tablespace Rollforward Recovery: 7
Start Time = 02/21/2008 15:25:243220
State = Executing
Invocation Type = User
Progress Monitoring:
Estimated Percentage Complete = 0
```

```
db2inst1@mens:> db2 list utilities show detail

```

ID = 332

Type = ROLLFORWARD RECOVERY

Database Name = ITS00B

Partition Number = 0

Description = Online Tablespace Rollforward Recovery: 7

Start Time = 02/21/2008 15:25:243220

State = Executing

Invocation Type = User

Progress Monitoring:

Estimated Percentage Complete = 0

Phase Number = 1

Description = Forward

Total Work = 38614 bytes

Completed Work = 38614 bytes

Start Time = 02/21/2008 15:25:243220

Phase Number [Current] = 2

Description = Backward

Total Work = 5627893427 bytes

Completed Work = 0 bytes

Start Time = 02/21/2008 15:25:2098645

```

```

db2inst1@mensa:> db2 select UTILITY_TYPE, substr(UTILITY_DESCRIPTION,1,15),

UTILITY_STATE, DBBPARTITIONNUM from SYSIBADM.SNAPUTIL

```

```

UTILITY_TYPE UTILITY_STATE DBBPARTITIONNUM

ROLLFORWARD_RECOVERY Online Tablespa EXECUTE 0

record(s) selected.

```

```

db2inst1@mensa:> db2 select SNAPSHOT_TIMESTAMP, UTILITY_STATE,

substr(PROGRESS_DESCRIPTION,1,10) desc, PROGRESS_START_TIME,

PROGRESS_TOTAL_UNITS, PROGRESS_COMPLETED_UNITS, DBBPARTITIONNUM

SYSIBADM.SNAPUTIL_PROGRESS

```

```

SNAPSHOT_TIMESTAMP UTILITY_STATE PROGRESS_START_TIME

PROGRESS_TOTAL_UNITS PROGRESS_COMPLETED_UNITS DBPARTITIONNUM

```

| SNAPSHOT_TIMESTAMP | UTILITY_STATE | PROGRESS_START_TIME | PROGRESS_TOTAL_UNITS | PROGRESS_COMPLETED_UNITS | DBPARTITIONNUM |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 2008-02-21-15.23.523409 | EXECUTE | 2008-02-21-15.23.013976 | 54837248 | 38614 | 0 |
| 2008-02-21-15.23.523409 | EXECUTE | 2008-02-21-15.23.013976 | 54837248 | 562347 | 0 |
对于 rollforward 恢复，有两个阶段：向前和向后。在向前阶段，读取日志文件并应用到数据库。在向后阶段，任何未提交的更改都将被回滚。

## 使用 Control Center 数据库恢复

恢复和 rollforward 已完全集成到 DB2 Control Center。您可以从图 13 所示的数据库菜单访问向导。恢复向导（图 14）将引导您完成恢复数据的步骤。例如，如果您想执行完整恢复或表空间恢复，可以选择哪个备份映像以及如何 rollforward。

## 在 Linux 上运行 DB2

> 注意：有关数据库恢复选项的详细说明，请参考《DB2 高可用性指南和参考》第 2 部分，“数据库恢复”。

## 6.1. 重定向恢复场景

使用重定向恢复，可以在将数据库恢复到原有数据库或另一个数据库时，更改存储在备份映像中的容器物理位置。重定向恢复通过带有 `REDIRECT` 参数的 `RESTORE` 命令或使用 Control Center 中的恢复向导执行。您需要使用 `SET TABLESPACE` 命令或向导重新定义要修改的每个表容器。在版本 9.5 中，您也可以从备份映像生成重定向恢复脚本并进行修改。

步骤：
1. 使用恢复程序生成重定向恢复脚本。必须调用 `REDIRECT` 和 `GENERATE` 选项。
2. 根据需要修改生成的重定向恢复脚本：
   - 恢复选项
   - 自动存储路径
   - 容器布局和路径
3. 运行修改后的重定向恢复脚本。

在分区数据库环境中，必须对每个分区执行这些步骤，因为表容器定义可能不同。

对于示例数据库 ITSDB，我们使用生成的重定向恢复脚本更改表空间的位置的大小。示例 6-24 显示了我们如何为分区数据库生成脚本。

## 示例 6-24 准备数据库并生成重定向恢复脚本

```

db2inst1@mensa:db2home/db2inst> db2 connect to itsdb

```

| Field | Value |
| :--- | :--- |
| Database server | DB2/LINUX64 9.5.0 |
| SQL authorization ID | DB2INST1 |
| Local database alias | ITSODB |

```

db2inst1@mensa:db2home/db2inst> db2 -tvf tscrt.sql

```

```

create tablespace TSDATA1 IBMDEFAULTGROUP managed by database using (file

'/tablespaces/db2inst1/itsdb/NODE0000/TSDATA1.000' 40M) on dbpartitionum(0)

using ('tablespaces/db2inst1/itsdb/NODE0001/TSDATA1.000' 40M) on

dbpartitionum(1)

DB200001 The SQL command completed successfully.

```

```

db2inst1@mensa:db2home/db2inst> db2 "create table TAB1 (id not null

primary key, name char(10) in tsdata1"

DB200001 The SQL command completed successfully.

```

```

db2inst1@mensa:db2home/db2inst> db2 "insert into tabl values (1, 'Tina')"

DB200001 The SQL command completed successfully.

```

```

db2inst1@mensa:db2home/db2inst> db2 "insert into tabl values (2, 'Jonas')"

DB200001 The SQL command completed successfully.

```
