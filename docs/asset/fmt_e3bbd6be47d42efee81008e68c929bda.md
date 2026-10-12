
`alter system set timed_statistics=true;`

系统已更改。

+ 3. 运行脚本 `utlbstat.sql` 创建存储统计信息的临时表。

```sql
@ORACLE_HOME/rdbms/admin/utlbstat.sql
```

+ 4. 让数据库正常运行以便生成统计信息。

+ 5. 在你想监控的时间结束后，运行 `utlestat.sql` 以删除临时表并生成报告。

```sql
@ORACLE_HOME/rdbms/admin/utlestat.sql
```

## 6. 将 `TIMED_STATISTICS` 设置回 `FALSE`。

```sql
SQL> alter system set timed_statistics=false;
```

系统已更改。

在此阶段，已创建了 `report.txt` 文件并可以对其进行审查。如果为了运行脚本而更改了默认表空间，请记住将其改回 `SYSTEM`。

# STATPACK

`STATPACK` 是于 Oracle 8.1.6 中引入，旨在提供与 `UTLBSTAT` 和 `UTLESTAT` 类似的功能，但具有多项改进的特性。具体而言，`STATPACK` 提供了以下改进：

- 报告更易于阅读
- 识别资源密集型 SQL
- 统计信息永久存储在数据库表中
- 可以以不同的详细程度捕获统计信息

数据库统计由 `STATPACK` 捕获并存储在数据库表中。每当你捕获统计信息时，你都会获取一个快照。你可以捕获多个数据快照；它们会被无限保存。例如，在生产环境的一天中，你可以每三小时拍摄一个快照——每个快照都是一个唯一的标识符。在稍后的某个时刻，你可以让 `STATPACK` 创建一个详细说明快照 X 和 Y 之间活动的报告。这允许你收集统计信息，但你不一定非那时生成报告。唯一的限制是，像 `B/ESTAT` 一样，报告不能跨越数据库关闭。

`STATPACK` 生成的报告也更易阅读和理解。没有过多的冗余信息，格式更好，并且为你计算了许多比例。总的来说，这是一个用户友好得得多的报告。

`STATPACK` 确实需要更复杂的设置和操作程序，但它并不非常复杂。基本步骤要求你安装 `STATPACK`、收集统计信息并生成报告。细节将在后续章节中概述。

## 安装

第一步是安装 `STATPACK`：

- 1. 启动 `SQL*Plus` 并连接内部。然后向 `TOOLS` 表空间添加 50M。

```sql
SQL> alter database datafile
2  '/u04/oradata/rhdev1/tools01.dbf
3 resize 150M;
```

数据库已更改。

运行安装脚本 `statscre.sql`。这将创建一个用户 `PERFSTAT`，该用户拥有用于存储统计信息的表。系统将提示你输入默认数据库和临时表空间，请选择 `TOOLS` 和 `TEMP`。系统还会提示你输入用于 `STATPACK` 对象的表空间，请选择 `TOOLS`。

```sql
SQL> @$ORACLE_HOME/rdbms/admin/statscre.sql
... Installing Required Packages
```

指定 `PERFSTAT` 用户的默认表空间：`TOOLS`
...

指定 `PERFSTAT` 用户的临时表空间：`TEMP`

输入创建 `STATPACK` 对象的表空间：`TOOLS`

Oracle 9i 的创建脚本被重命名为 `spcreate.sql`。它位于相同的位置。大多数脚本是相同的，但它们不再使用 `stat` 前缀，而是使用 `sp` 前缀，例如，`statatauto.sql` 现在是 `spatauto.sql` 了。

安装可能需要几分钟来创建对象，并占用 `TOOLS` 表空间的约 30M。`PERFSTAT` 的默认密码是 `PERFSTAT`。

检查文件 `statpack.lis` 是否有错误。该文件位于你运行脚本的目录。假设没有错误，则安装完成。

## 注意事项

小心混合使用 `B/ESTAT` 和 `STATPACK`
你不能以同一个用户运行 `UTLBSTAT/UTLESTAT` 和 `STATPACK`。它们共享一个名为 `STAT$$WAITSTAT` 的表，该表会被每个实用程序覆盖。解决方案是继续以 `SYS` 身份运行 `UTLBSTAT/UTLESTAT`，但以用户 `PERFSTAT` 运行 `STATPACK`。

## 收集统计信息

下一步是以快照的形式收集统计信息：

- 1. 与 `UTLBSTAT/UTLESTAT` 一样，建议将 `TIMED_STATISTICS` 设置为 `TRUE`。
`SQL> alter system set timed_statistics=true;`

系统已更改。

- 2. 以 `PERFSTAT` 用户身份连接。
`SQL> connect perfstat/perfstat`

已连接。

- 3. 执行 `STATPACK.SNAP` 来捕获快照。运行大约需要 30 秒。
`SQL> execute statpack.snap;`
`PL/SQL` 成功完成。

剩下的工作就是创建快照。此过程可以通过 `cron` 或作为 `DBMS_JOB` 使用 `ORACLE_HOME/rdbms/admin/statsauto.sql` 轻松地自动化。

## 生成报告

一旦你捕获了两个快照，就可以生成报告。报告会在你启动 `SQL*Plus` 的目录中创建。

- 1. 以 `PERFSTAT` 用户身份连接。
`SQL> connect perfstat/perfstat`

已连接。

- 2. 运行脚本 `statsrep.sql`。
`SQL> @ORACLE_HOME/rdbms/admin/statsrep`

- 3. 你将被提示输入一个起始快照 ID。选择一个可用的快照作为起点。

| DB Id | DB Name | Inst Num | Instance |
|---|---|---|--|
| 3801419294 | RH1DEV1 | | rh1dev1 |

完成

| Instance | DB Name | SnapId | Started |
|---|---|---|---|
| rh1dev1 | RH1DEV1 | 1 | 27 Apr 2001 |
| rh1dev1 | RH1DEV1 | 2 | 27 Apr 2001 |
| rh1dev1 | RH1DEV1 | 3 | 27 Apr 2001 |

已完成的快照

输入起始快照 ID：1

- 4. 选择一个结束快照 ID。由于像快照 一样，报告不能跨越数据库关闭。

输入结束快照 ID：3

- 5. 指定输出文件名。默认文件名，你可以给它一个更有意义的名字。

输入输出文件名 [st_3] : statpack1.txt

`STATPACK` 将在你的本地目录生成报告。报告将包含以下信息：

- 数据库识别
- 用于报告的快照
- 缓冲区和块大小
- 加载信息
- SGA 比例
- 等待事件
- 资源密集型 SQL 语句
- 实例统计信息
- 表空间 I/O
- 回滚段使用
- 锁统计信息
- 库缓存统计信息
- SGA 配置
- init.ora 参数

由 `UTLSTAT/UTLESTAT` 生成的信息。

# 调优内存结构

Oracle 的调优工具提供了有关数据库的信息。然而，如果没有准确的解释，这些信息没有意义。本节将讨论这些数字意味着什么。首先，讨论如何衡量这些值。

## 比例

长期以来，DBAs 使用内存比例是是如果在内存中未找到数据块，Oracle 必须去磁盘。因此，DBAs 认为数据库性能可以通过找到的次数与未找到的次数来衡量。结果，有很多衡量性能的公式。此外，每个类别都有一个应该实现的百分比。

仅根据这些比例调优数据库是危险的。数据库可能满足所有数值但性能仍然不佳。高百分比取决于应用程序的类型。另一方面，糟糕的比例是问题的良好指标。如果你注意到某个比例数值很低，它可以很好地指示问题。比例仅仅是性能的定量衡量。

关于比例的最后一点说明：它们假设数据库已经运行了一段时间。正常位于内存中的所有内容都必须被读取一次。这需要时间。因此，预计在数据库启动后不久，比例会较低。

## 数据库缓冲区缓存

数据库缓冲区缓存包含用户操作所需的每个数据块。当操作需要数据块时，它首先查看这里。如果找到了良好的副本，则使用该副本。否则，Oracle 必须去磁盘。数据库缓冲区的大小由 `DB_BLOCK_BUFFERS` 决定。

从 `V$SGA` 查询得到的数据库缓冲区值是：

```
Database Buffers = DB_BLOCK_BUFFERS * DB_BLOCK_SIZE
```

效率通过命中率衡量。这是物理读取的次数与在内存中找到当前或读取一致块的次数的对比。

该值通过以下方式得出：

```sql
SQL> select 1 - (phy.value / (cur.value + con.value))
from v$sysstat cur, v$sysstat con, v$sysstat phy
where cur.name = 'db block gets'
and con.name = 'consistent gets'
and phy.name = 'physical reads';
```
