
如果您在 Oracle RAC 集群中运行，还会有一组用于整个集群的动态性能视图。这些是全局动态性能视图，被称为 gv$ 视图。gv$ 视图与 v$ 视图性质相似，但包含一个额外的列，即实例名。

视图 v$session 包含当前实例中运行的会话的信息。视图 gv$session 包含 RAC 集群中所有运行会话的信息。gv$ 视图非常有用，就像 v$ 视图一样。

动态性能视图的内容报告各种实例指标。例如，v$session 视图为实例中运行的每个会话包含一行，其大小会根据会话数量而变化。视图 v$sysstat 包含系统信息，且视图中的行数永远不会改变。许多视图本质上是计数器，值始终递增，而其他视图包含动态上下波动的数据。

使用 v$ 视图的一个例子是确定缓冲区缓存命中率。有关缓冲区缓存的统计信息可在动态性能视图 v$sysstat（系统统计）中找到。列 physical_reads 表示缓存未命中，而列 consistent_gets 和 db_block_gets 表示缓存命中。为了确定缓冲区缓存命中率，请使用以下公式：

```
1 - (physical_reads / (db_block_gets + consistent_gets))
```

这些值可在 v$sysstat 中找到，并可使用以下查询收集：

```
SQL> SELECT name, value FROM v$sysstat
WHERE NAME IN ('db block gets from cache', 'consistent gets from cache',
'physical reads cache');
```

| 名称 | 值 |
|---|---|
| 缓存中的 db 块获取 | 206884 |
| 缓存中的一致性获取 | 137869 |
| 缓存物理读取 | 12065 |

从这一点开始，只是一个数学问题，如下所示：

```
Cache Hit Ratio = 1 - (12065 / (206884 + 137869)) = 1 - .035 = .965 = 96.5%
```

此查询表示整体缓冲区缓存命中率。然而，请记住现在有多个缓冲区缓存。除了 DEFAULT 缓存外，还有标准块大小的 KEEP 和 RECYCLE 缓存。还有非标准缓存大小。以下查询为所有这些缓存提供缓存命中率：

```
SQL> SELECT name, 1 - (physical_reads / (db_block_gets + consistent_gets)) AS
"Cache Hit Ratio"
FROM v$buffer_pool_statistics;
```

| 名称 | 缓存命中率 |
|---|---|
| 默认 | .965642687 |

v$ 视图提供了大量优秀的信息，然而，使用查询手动检索这些信息可能非常耗时且繁琐。为了帮助完成此任务，Oracle 提供了一些 SQL 脚本，可帮助您计算多种不同的指标。这些脚本是 utlbstat.sql 和 utlestat.sql。在 Oracle 9i 中，这些脚本基本上已被 Statspack 取代。Statspack 是 Oracle 提供的包，它保存 v$ 和 gv$ 数据的快照，并将这些快照与后续快照进行比较，以便不仅提供缓存命中率等动态数据，还提供速率。在下一节中，您将学习如何在 Linux 上配置和使用 Statspack。

### 使用 AWR

自动工作负载库（AWR）是 Oracle 10g 中的一项新功能。AWR 是一种自动收集性能数据的方法。默认情况下，AWR 统计信息每小时收集一次并保留一周。AWR 统计收集设置可通过 DBMS_WORKLOAD_REPOSITORY 包进行查看和设置。

AWR 报告是通过运行 SQL 脚本 awrpt.sql 创建的，该脚本位于 $ORACLE_HOME/rdbms/admin。当运行 awrpt.sql 时，您必须选择开始和结束点。这些快照用于根据这些开始和结束点创建差异报告。AWR 与 Statspack 报告非常相似，因此请使用下一节来帮助解释 AWR 数据。

此外，还有几个过程可用于调整 AWR 数据收集之间的间隔以及 AWR 统计信息保留的时间。这些设置可通过 DBMS_WORKLOAD_REPOSITORY 包中的 MODIFY_SNAPSHOT_SETTINGS 过程进行设置。要更改设置，请使用以下 SQL 语句。

```
SQL> DBMS_WORKLOAD_REPOSITORY.MODIFY_SNAPSHOT_SETTINGS( retention => minutes,
interval => minutes, topnsql => number, dbid => number or NULL);
```

通过设置快照设置，您可以调整 AWR 以更好地满足您的需求。保留期越长、间隔越短，您使用的空间就越多。

### 使用 Statspack

v$ 和 gv$ 视图中存储的所有值都表示某一时间点的该值。许多值在单个时间点上几乎没有用，例如每个 Oracle 数据类型发生的 I/O 数量的计数。对此数据的更合理表示方法是在两个时间点进行此测量，将较晚值减去较早值，然后除以两次测量之间的时间。这将提供每个时间段的 I/O 速率。当您可以查明每秒执行了多少 I/O 时，I/O 性能才更有意义。

Statspack 通过拍摄动态性能数据的快照并将该信息存储在表中来帮助解决此问题。在稍后的时间，可以拍摄另一个快照。Statspack 还包括一个实用程序，用于在两个快照之间取差值并为您计算速率和统计信息。几页后，您将看到这是如何完成的以及提供什么样的数据。

**配置 Statspack**  Statspack 需要创建多个 Oracle 表，因此您必须为此数据存储提供 Statspack 空间。因此，设置 Statspack 的第一步是创建表空间。接下来，连接到 Oracle 并安装 Statspack 包。这些步骤如下所示：

- 1. 为统计信息创建足够大的表空间（主要用于范围数量）。
- 2. 使用 SQLPLUS 安装 Statspack。
  - a. 启动 SQLPLUS。
  - b. 在 SQL> 提示符下，输入 `@?/rdbms/admin/spcreate`。
  - c. 提示时，指定要存储统计信息的表空间。
  - d. 为 perfstat 用户提供密码。
  - e. 提示时，指定临时表空间。

一旦 Statspack 表和 perfstat 用户配置完成，您就可以开始使用 Statspack。如何操作在下一节中显示。

**使用 Statspack**  使用 Statspack 涉及以 perfstat 用户身份连接到 Oracle 实例并运行快照。每当您有两个或多个想要比较的快照时，运行 spreport 过程以创建 Statspack 报告。这些步骤如下所示，命令序列显示为子步骤：

- 1. 以 perfstat 身份连接到 SQLPLUS。
  - a. `sqlplus /nolog`
  - b. `SQL> CONNECT perfstat/perfstat`
  - c. `SQL> EXECUTE statspack.snap;`
- 2. 根据需要继续并拍摄快照。

Statspack 报告在两个不同的快照上运行。要查找有哪些快照可用，请使用以下查询：

- 以 perfstat 身份连接到 SQLPLUS。
  - sqlplus /nolog
  - SQL> CONNECT perfstat/perfstat
  - SQL> VARIABLE snap NUMBER;
  - SQL> Begin :snap := statspack.snap; end;
  - SQL> /
  - SQL> print snap;

这将提供可用于创建 Statspack 报告的 Statspack ID 列表。创建 Statspack 报告是通过使用 spreport 过程完成的。spreport 函数也作为 perfstat 用户从 sqlplus 中运行。Spreport 将要求输入开始和结束快照，并将根据这些快照的差异创建报告。运行 spreport 如下所示：

- 以 perfstat 身份连接到 SQLPLUS。
  - Sqlplus /nolog
  - SQL> CONNECT perfstat/perfstat
  - SQL> @?/rdbms/admin/spreport

系统会提示您输入开始和结束快照。报告将为您保存，如下所示：

```
SQL> @?/rdbms/admin/spreport

Current Instance
----------------

DB Id    DB Name      Inst Num Instance
------------------------- --------------- -------- ----------
1053994617 ORCL                  1 orcl

Instances in this Statspack schema
----------------------------------

DB Id    Inst Num DB Name      Instance       Host
------------------------- --------------- -------------- -------------------
1053994617    1 ORCL       orcl       ptc6.perfuning.com

Using 1053994617 for database Id
```
