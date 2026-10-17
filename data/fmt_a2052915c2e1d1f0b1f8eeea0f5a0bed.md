
链和迁移将在第 8 章“调优 I/O”中进行更详细的讨论。

## Oracle 提供的工具

Oracle 提供了一些调优工具，以脚本和 PL/SQL 包的形式存在，可以帮助你识别可能的数据库性能问题。这里列出了常用的 Oracle 提供的工具：

- `UTLBSTAT.SQL`/`UTSTAT SQL`（在后续章节讨论）
- `STATPACK`（在后续章节讨论）
- `UTLOCK.SQL`（第 9 章“调优竞争”）
- `CATBLOCK.SQL`（第 9 章“调优竞争”）
- `CATPRARR.SQL`（第 5 章“调优数据库缓冲缓存”）
- `DBMS_POOL.SQL`（第 4 章“调优共享池”）
- `UTCHAIN.SQL`（第 8 章“调优 I/O”）
- `UTLXPLAN.SQL`（第 3 章“SQL 应用调优与设计”）

## Oracle 使用其他调优工具

这些脚本中的某些仅运行一次，用于构建对性能调优有用的表或视图。其他脚本则会在每次执行调优练习时运行。所有这些脚本将在后面的章节中进行详细讨论。然而，由于 `UTLBAT.SQL`/`UTLESTAT SQL` 脚本和 `STATPACK` 工具的输出涵盖了数据库性能的所有方面，因此在此处对它们进行介绍性的讨论。

## UTLBSTAT.SQL 和 UTLESTAT.SQL

尽管很大程度上被下一节讨论的新版 `STATPACK` 工具所取代，但 Oracle 提供的 `UTLBAT.SQL` 和 `UTLESTAT.SQL` 脚本仍然是 Oracle Server 性能调优的工具。这些脚本的目的是捕获并总结特定时间范围内几乎所有的数据库和实例活动。由于运行生成的输出 `UTLBAT.SQL` 和 `UTLESTAT.SQL` 脚本的过程及其输出内容在所有平台和操作系统上都是相同的，因此它们对你来说仍然是重要的工具。

`UTLBAT` 中的 B 代表 beginning（开始）。`STATSTAT` 中的 E 代表 ending（结束）。正如这些名称所示，`UTLBAT.SQL` 脚本在调优测量期开始时运行，而 `UTLESTAT.SQL` 在调优测量期结束时运行。

这些脚本位于 Unix 上的 `%ORACLE_HOME%/rdbms/admin`，以及 Windows 2000 系统上的 `%ORACLE_HOME%\rdbms\admin`。

## 运行 UTLBAT.SQL 脚本

在运行 `UTLBAT.SQL` 脚本之前，重要的是实例运行时间足够长，以便 VS 性能视图填充有意义的统计数据。通常这意味着你希望在数据库打开至少 30 分钟正常用户活动后等待并运行 `UTLBAT.SQL` 脚本。

当执行 `UTLBAT.SQL` 脚本时，它将执行以下操作：

- 首先，将删除任何 `UTLBAT.SQL` 脚本准备创建的表——如果它们已经存在。如果之前执行 `UTLSTAT.SQL` 后没有执行 `UTLESTAT.SQL`，则这些表可能存在。由于表可能不存在，在执行 `UTLSTAT.SQL` 期间看到 `ORA-00942` 表或视图不存在的错误是正常的。

- 接下来，`UTLSTAT.SQL` 脚本将创建一系列临时表，这些表是特定时刻某些 V$ 视图内容的副本。例如，`UTLSTAT.SQL` 将创建一个名为 `stats$begin-event` 的表，它是 `$vsystem_event` 视图的副本。

在 SQL*Plus 中使用以下命令执行 `UTLSTAT.SQL` 脚本：

- Unix: `@ORACLE_HOME/rdbms/admin/utlstat.sql`
- Windows 2000: `@ORACLE_HOME%\rdbms\admin\utlstat.sql`

## 运行 UTLSTAT.SQL 脚本

运行 `UTLSTAT.SQL` 和运行另一个脚本之间应该留出有意义的时间。通常，这段持续时间至少为 15 分钟，但可能持续几个小时或几天。

![](img/c36db8fbb4893c630ad429a99bfd63e3_90_0.png)

如果你在运行 `UTLSTAT.SQL` 和 `UTLESTAT.SQL` 之间关闭了实例，那么你的结果将不可用。这是因为这些脚本使用的 V$ 视图中的所有统计数据在实例关闭时会被清除，并在实例启动时重新填充。

当执行 `UTLSTAT.SQL` 脚本时，它将执行以下操作：

- 首先，它将删除任何 `UTLSTAT.SQL` 脚本要创建的表——如果它们已经存在。如果之前执行 `UTLSTAT.SQL` 失败，则这些表可能存在。在执行 `UTLSTAT.SQL` 期间看到 `ORA-00942` “表或视图不存在”错误是正常的。

- 接下来，`UTLSTAT.SQL` 脚本将创建一系列临时表，这些表是 `UTLSTAT.SQL` 复制的 V$ 视图内容的副本。然而，这次表的名称类似于 `stats$end_event`，并将包含它们在该时刻存在的统计数据。

然后，它计算由 `UTLSTAT.SQL` 在调优期开始创建的 `stats$begin` 表与由 `UTLESTAT.SQL` 在调优期结束创建的 `stats$end` 表之间的指标。

最后，它会生成一个文本文件 `REPORT.TXT`，其中包含这些计算的结果。该文本文件包含了大多数数据库调优活动所需的信息。

在 SQL* 中使用以下命令执行 `UTLESTAT.SQL` 脚本：

- Unix: `@ORACLE_HOME/rdbms/admin/utlstat.sql`
- Windows 2000: `@ORACLE_HOME%\rdbms\admin\utlstat.sql`

生成的 `REPORT.TXT` 文件将写入用户当前目录下的操作系统文件。

![](img/c36db8fbb4893c630ad429a99bfd63e3_91_0.png)

> 标准的 `UTLSTAT.SQL` 和 `UTLESTAT.SQL` 脚本在每个脚本的开头都包含 `CONNECT/AS SYS`。如果你的数据库使用了密码文件，则你必须编辑这些脚本中的每一个，将 `CONNECT/AS SYS` 命令改为 `CONNECT AS SYS` 或其他用户名。然后执行脚本，它们将动态提示你输入密码。

## 解析 REPORT.TXT 的内容

一旦由 `UTLSTAT.SQL` 和 `UTLESTAT.SQL` 生成，`REPORT.TXT` 文件将包含 `UTLSTAT.SQL` 运行到 `UTLESTAT.SQL` 运行期间的所有统计数据。解读 `REPORT.TXT` 内容似乎是一项艰巨的任务，但通过实践和经验，你可以很快解决问题。该文件包含了大多数数据库调优活动所需的所有信息。

Figure 2.2

它计算了由 `UTLSTAT.SQL` 在调优期开始创建的 `stats$begin` 表和 `UTLESTAT.SQL` 在调优期结束创建的 `stats$end` 表之间的指标。

```
select ck

count = 100
```

一旦由 `UTLSTAT.SQL` 和 `UTLESTAT.SQL` 生成，`REPORT.TXT` 文件将包含 `UTLSTAT.SQL` 运行到 `UTLESTAT.SQL` 运行期间的所有统计数据。解读 `REPORT.TXT` 内容似乎是一项艰巨的任务，但通过实践和经验，你可以很快解决问题。该文件包含了大多数数据库调优活动所需的所有信息。

Figure 2.2

它计算了由 `UTLSTAT.SQL` 在调优期开始创建的 `stats$begin` 表和 `UTLESTAT.SQL` 在调优期结束创建的 `stats$end` 表之间的指标。

```
select ck

count = 100
```
