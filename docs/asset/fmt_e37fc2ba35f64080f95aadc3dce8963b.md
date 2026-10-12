
在查询 `V$` 视图时，为了获取所需的所有信息，通常需要将两个或更多此类视图连接起来。例如，查询 `V$SESSTAT` 可以获取特定用户会话内事件的详细统计数据，但不会显示每个统计项的名称。要获取每个统计项的含义，你需要将 `V$SESSTAT` 连接到 `V$STATNAME`。以下代码清单展示了此类查询的示例。此查询将显示名为 Chris 的用户的所有会话统计信息。

```sql
select s.username, n.name, t.value
from v$session s, v$statname n, v$sesstat t
where s.sid=t.sid
and t.statistic#=n.statistic#
and s.username = 'CHRIS';
```

请记住，将任何视图连接到 `V$SYSSTAT` 将为您提供系统范围的性能信息，而将任何视图连接到 `V$SESSTAT` 将为您提供单个用户的性能信息。

### DBA 视图查询示例

对 DBA 视图的查询对于性能调优也很有用。例如，您可能希望了解哪些表中的行被链接或迁移了。下面的查询将为最近使用 `ANALYZE TABLE` SQL 命令进行分析的名为 Chris 的用户（其架构）提供该信息。

```sql
select table_name, chain_cnt
from dba_tables
where owner = 'CHRIS'
and chain_cnt != 0;
```

有关链接和迁移的更详细讨论见第 8 章“磁盘 I/O 调优”。

## Oracle 提供的调实用工具

Oracle 提供了一些调实用工具，形式为脚本和 PL/SQL 包，可用于帮助您识别潜在的数据库性能问题。以下是一些常用的 Oracle 提供的调实用工具列表：

- `UTLSTAT.SQL`/`UTLESTAT.SQL`（在下一节中讨论）

- `STATSPACK`（在下一节中讨论）

- `UTLOCKT.SQL`（第 9 章，“锁争用调优”）

- `CATBLOCK.SQL`（第 7 章，“锁争用调优”）

- `CATPARR.SQL`（第 5 章，“数据库缓冲池调优”）

- `DBMSPOOL.SQL`（第 4 章，“共享池调优”）

- `UTLCCHAIN.SQL`（第 8 章，“磁盘 I/O 调优”）

- `UTLXPLAN.SQL`（第 3 章，“SQL 应用调优与设计”）

这些脚本中有一些只需运行一次，以构建用于性能调优的表或视图。其他脚本则在每次执行调优操作时运行。所有这些脚本将在后续章节中详细讨论。然而，由于 `UTLBSTAT.SQL`/`UTLESTAT.SQL` 脚本和 `STATSPACK` 工具的输出涵盖了数据库性能的所有方面，因此在此处包含对其的初步介绍。

## UTLBSTAT.SQL 和 UTLESTAT.SQL

尽管很大程度上已被下一节中介绍的较新的 `STATSPACK` 工具所取代，但 Oracle 提供的 `UTLBSTAT.SQL` 和 `UTLESTAT.SQL` 脚本仍然是 Oracle 服务器性能调优的有用工具。这些脚本的目的是捕获并总结特定时间段内几乎所有的数据库和实例性能活动到单个报告中。由于在所有平台和操作系统上，运行 `UTLBSTAT.SQL` 和 `UTLESTAT.SQL` 脚本的过程及其输出内容都是相同的，因此它仍然是您需要了解的重要工具。

`UTLBSTAT.SQL` 中的 `B` 代表*开始*（beginning）。`UTLESTAT.SQL` 中的 `E` 代表*结束*（ending）。正如这些名称所暗示的那样，`UTLBSTAT.SQL` 脚本在调优测量期的开始时运行，而 `UTLESTAT.SQL` 在调优测量期的结束时运行。

在 Unix 系统上，这些脚本位于 `$ORACLE_HOME/rdbms/admin`；在 Windows 2000 系统上，位于 `%ORACLE_HOME%\rdbms\admin`。

### 运行 UTLBSTAT.SQL 脚本

在运行 `UTLBSTAT.SQL` 脚本之前，重要的是实例已运行足够长的时间，以便让 `V$` 动态性能视图填充有意义的统计数据。通常，这意味着您希望在数据库开放并经历至少 30 分钟正常用户活动后，等待并运行 `UTLBSTAT.SQL` 脚本。

当执行 `UTLBSTAT.SQL` 脚本时，它会执行以下操作：

- 首先，它将删除 `UTLBSTAT.SQL` 脚本即将创建的任何表——如果它们已经存在。如果之前执行 `UTLBSTAT.SQL` 后未执行 `UTLESTAT.SQL`，这些表可能存在。由于这些表可能不存在，在执行 `UTLBSTAT.SQL` 期间看到 `ORA-00942` *表或视图不存在* 错误是正常的。

- 其次，`UTLBSTAT.SQL` 脚本创建一系列临时表，它们是当时某些 `V$` 视图内容的副本。例如，`UTLBSTAT.SQL` 将创建一个名为 `stats$begin_event` 的表，它是 `V$system_event` 视图的副本。

在 SQL*Plus 中，使用以下命令执行 `UTLBSTAT.SQL` 脚本：

- Unix：`@$ORACLE_HOME/rdbms/admin/utlbstat.sql`

- Windows 2000：`@%ORACLE_HOME%\rdbms\admin\utlbstat.sql`

### 运行 UTLESTAT.SQL 脚本

在运行 `UTLBSTAT.SQL` 和运行 `UTLESTAT.SQL` 之间，应该允许经过一段有意义的时间。通常，这段时间至少应为 15 分钟，但也可能是数小时甚至数天。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_91_0.png)

> 如果在运行 `UTLBSTAT.SQL` 和 `UTLESTAT.SQL` 之间的实例被关闭，您的结果将无法使用。这是因为这两个脚本使用的 `V$` 视图中的所有统计信息在实例关闭时被清除，然后在实例启动时重新填充。

当执行 `UTLESTAT.SQL` 脚本时，它会执行以下操作：

- 首先，它将删除 `UTLESTAT.SQL` 脚本即将创建的任何表——如果它们已经存在。如果之前执行 `UTLESTAT.SQL` 失败，这些表可能存在。由于这些表可能不存在，在执行 `UTLESTAT.SQL` 期间看到 `ORA-00942` *“表或视图不存在”* 错误是正常的。

- 其次，`UTLESTAT.SQL` 脚本创建一系列临时表，它们是 `UTLBSTAT.SQL` 所复制的相同 `V$` 视图内容的副本。然而，这次表的名字像 `stats$end_event`，并将包含当时存在的统计数据。

- 然后，它计算 `stats$begin` 表（由调优期开始的 `UTLBSTAT.SQL` 创建）中的统计信息与调优期结束的 `UTLESTAT.SQL` 创建的 `stats$end` 表中的统计信息之间的指标。

- 最后，它生成一个文本文件 `REPORT.TXT`，其中包含这些计算的结果。此文本文件包含大多数数据库调优活动所需的所有信息。

在 SQL*Plus 中，使用以下命令执行 `UTLESTAT.SQL` 脚本：

- Unix：`@$ORACLE_HOME/rdbms/admin/utlestat.sql`

- Windows 2000：`%ORACLE_HOME%\rdbms\admin\utlestat.sql`

生成的 `REPORT.TXT` 文件将写入用户当前目录中的操作系统文件。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_92_0.png)

> 标准的 `UTLBSTAT.SQL` 和 `UTLESTAT.SQL` 脚本在每个脚本的开头都包含 `CONNECT/AS SYSDBA` 字符串。如果您的数据库使用密码文件，那么您将需要编辑这些脚本，将 `CONNECT/AS SYSDBA` 命令更改为 `CONNECT SYS AS SYSDBA`，或其他某个 `SYSDBA` 用户名。然后，当脚本执行时，它们会动态提示您输入 `SYSDBA` 密码。

### 解读 REPORT.TXT 的内容

一旦由 `UTLBSTAT.SQL` 和 `UTLESTAT.SQL` 生成，生成的 `REPORT.TXT` 文件将包含 `UTLBSTAT.SQL` 执行时间和 `UTLESTAT.SQL` 执行时间之间的所有调优统计数据。`REPORT.TXT` 是一个简单的文本文件，可以使用任何编辑器查看。在初步检查时，解读 `REPORT.TXT` 文件的内容可能看起来是一项艰巨的任务。然而，通过练习和经验，您将能够以最小的努力迅速发现冗长的 `REPORT.TXT` 文件中的问题区域。本书其余部分将对 `REPORT.TXT` 文件的相关部分进行引用。在 Windows 2000 系统上的 Oracle9i 数据库中生成的示例 `REPORT.TXT` 文件的一部分显示在图 2.2 中。

## 图 2.2 REPORT.TXT 文件的示例片段
