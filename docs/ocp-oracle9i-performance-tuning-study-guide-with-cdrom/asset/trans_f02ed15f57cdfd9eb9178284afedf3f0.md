
## 图 4.3 显示库缓存命中率的 STATSPACK 输出

| 实例效率百分比（目标 100%） | | | |
| :--- | :--- | :--- | :--- |
| Buffer Nowait %: | 100.00 | Redo Nowait %: | 100.00 |
| Buffer Hit %: | 100.00 | In-memory Sort %: | 97.96 |
| Library Hit %: | 88.11 | Soft Parse %: | 79.01 |
| Execute to Parse %: | 42.96 | Latch Hit %: | 100.00 |
| Parse CPU to Parse Elapsed %: | | Non-Parse CPU: | |

| 共享池统计信息 | 开始 | 结束 |
| :--- | :--- | :--- |
| 内存使用率 %: | 27.49 | 28.35 |
| 执行次数 >1 的 SQL 占比 %: | 53.78 | 58.42 |
| 执行次数 >1 的 SQL 内存占比 %: | 63.47 | 79.74 |

STATSPACK 还包含第二部分，标题为 *Library Cache Activity for DB*（数据库库缓存活动），显示了与前一部分中所示的 V$LIBRARYCACHE 查询中出现的相同的关于失效（invalidations）和重新加载（reloads）的信息。图 4.4 展示了来自名为 PROD 的数据库的示例 STATSPACK 输出。

## 图 4.4 显示库缓存失效和重新加载的 STATSPACK 输出

| 数据库: prod 实例: prod 库缓存活动 快照: 1 - 2 | | | | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| -> "Pct Misses"（缺失百分比）应该非常低 | | | | | | |
| | 获取 (Get) | 缺失 % (Pct) | 固定 (Pin) | 缺失 % (Pct) | 重新加载 (Invali-) | |
| **命名空间 (Namespace)** | **请求次数 (Requests)** | **缺失 % (Miss)** | **请求次数 (Requests)** | **缺失 % (Miss)** | **重新加载次数 (Reloads)** | **失效次数 (dations)** |
| BODY | 7 | 0.0 | 7 | 0.0 | 0 | 0 |
| SQL AREA | 72 | 2.8 | 438 | 11.4 | 2 | 0 |
| TABLE/PROCEDURE | 219 | 0.5 | 390 | 16.9 | 0 | 0 |

STATSPACK 的这一部分还展示了关于库缓存获取比率（Get ratio）的信息。然而，在 STATSPACK 输出中，性能是通过缺失比率（miss ratio）而不是之前描述的命中比率来表示的。图 4.4 显示 SQL AREA 命名空间的获取请求活动的 Pct Miss（缺失百分比）值为 2.8，即 2.8%。相反，这意味着在监控期间，库缓存中 SQL AREA 部分的命中率达到了 97.2%——这很好地符合了 Oracle 推荐的 90% 的指导标准。

### 使用 REPORT.TXT 监控库缓存

通过运行 UTIBSTAT.SQL 和 UTLESTAT.SQL 生成的 REPORT.TXT 文件还包含一个部分，显示库缓存的 GETHITRATIO（获取命中率）、PINHITRATIO（固定命中率）、RELOADS（重新加载次数）和 INVALIDATIONS（失效次数）信息。图 4.5 展示了 REPORT.TXT 文件的相关部分。

## 图 4.5 显示库缓存统计信息的 REPORT.TXT 输出

```sql
SQL> column library  format a12 trunc;
SQL> column pnhitratio  heading 'PINHITRATIO';
SQL> column gethitratio  heading 'GETHITRATIO';
SQL> column invalidations  heading 'INVALIDATI';
SQL> set numwidth 10;
SQL> rem Select Library Cache statistics. The pin hit rate should be high.
SQL> select name\space library,
3          gets,
3        round((decode(gethits,0,1,gethits)/decode(gets,0,1,gets),3)
3        gethitratio,
3        pns,
3        round((decode(pnhits,0,1,pnhits)/decode(pins,0,1,pins),3)
3        pnhitratio,
3        reloads, invalidations
9        from stats$libt;
```

LIBRARY     GETS GETHITRATIO  PINS PINHITRATIO  RELOADS INVALIDATI
------  --------  -----------  ----------  -----------  ---------
BODY       10        1           10        1        0       0
CLUSTER      176        .989         238        .994       0       0
INDEX      0         1           0         1        0       0
JAVA DATA    0         1           0         1        0       0
JAVA RESOURCE 0         1           0         1        0       0
JAVA SOURCE 0         1           0         1        0       0
OBJECT       0         1           0         1        0       0
PIPE         0         1           0         1        0       0
SQL AREA     3669        .939        88360        .992       36      0
TABLE/PROC 1224        .859         7653        .994       43      0
TRIGGER      82        .89          82        .829       5       0

这些信息本质上与 V$LIBRARYCACHE 视图中包含的信息相同。然而，与对 V$LIBRARYCACHE 的查询（它显示自实例启动以来的库缓存统计信息）不同，REPORT.TXT 中包含的库缓存统计信息仅涵盖执行 UTLBSTAT.SQL 和 UTLESTAT.SQL 脚本之间的时间段。

### 使用企业经理监控库缓存

Oracle Enterprise Manager GUI 工具中的性能管理器组件包含多个库缓存性能信息源。第一个如图中所示，是位于性能管理器实用工具内存类别中的 SGA 概览选项的输出。

图 4.6 中显示的输出表明，右上角面板中显示的共享池空闲百分比（Shared Pool % Free）值接近 100%。这表明共享池仍有足够的空间来缓存额外的应用程序 SQL 语句。

性能管理器的另一个有用组件是“库缓存命中率 %”（Library Cache Hit %），它位于性能管理器实用工具的数据库实例类别中。图 4.7 显示了该实用工具的示例输出。

## 图 4.6 OEM 性能管理器中的 SGA 概览

![](img/832fbc6aca8b6075843ca6f2356c0a8d_256_0.png)

## 图 4.7 OEM 性能管理器中的库缓存命中率 %

![](img/832fbc6aca8b6075843ca6f2356c0a8d_256_1.png)

图 4.7 展示了在特定时间间隔内监控后的库缓存命中率图表。该图表显示，库缓存命中率在监控期的大部分时间内保持在 100% 左右，但在监控期开始附近短暂降至大约 90%。

性能管理器中 SQL 类别下的工具也有助于监控库缓存活动。特别是，SQL 类别中的“SQL 硬解析分析”（SQL Hard Parse Analysis）选项显示了应用程序 SQL 语句发生解析的频率。图 4.8 展示了“SQL 硬解析分析”选项的示例输出。

## 图 4.8 OEM 性能管理器中的 SQL 硬解析分析

![](img/832fbc6aca8b6075843ca6f2356c0a8d_257_0.png)

图 4.8 中的输出显示了当前 SGA 大小的分解，以及硬解析代码的 SQL 片段和每个数据库会话的硬解析次数。如果某个用户会话显示出高硬解析计数的证据，则应检查由该用户执行的应用程序代码，寻找可能增强 SQL 重用而非硬解析的改进方法。本章后文将描述鼓励 SQL 代码重用的技术。

## 衡量数据字典缓存性能

与库缓存类似，数据字典缓存有效性的衡量标准也是通过命中率来表述的。这个字典缓存命中率显示了应用程序在内存中找到所需数据字典信息的频率，而不是不得不从磁盘读取。这种命中率信息包含在一个名为 **V$ROWCACHE** 的动态性能视图中。**STATSPACK** 和 **REPORT.TXT** 的输出也包含与数据字典缓存命中率相关的统计信息。

**Oracle 目标**：衡量和调整**字典缓存**命中率

### 使用 **V$ROWCACHE** 监控数据字典缓存

**V$ROWCACHE** 视图中包含的两个列，**GETS**（获取次数）和 **GETMISSES**（获取缺失次数），可用于计算数据字典缓存的命中率。该视图中的统计信息通常不会单独检查，而是使用此处所示的查询以聚合形式进行检查：

```sql
SQL> SELECT 1 - (SUM(getmisses)/SUM(gets))
  2   "Data Dictionary Hit Ratio"
  3   FROM v$rowcache;

Data Dictionary Hit Ratio
-------------------------
               .969700203
```

此查询的结果表明，您的应用程序在 96.9% 的情况下能够找到已经位于内存中的所需数据字典信息。

**提示** 如果整体数据字典缓存命中率低于 85%，Oracle 建议考虑调整共享池。

### 使用 **STATSPACK** 监控数据字典缓存

数据字典缓存性能指标也可以找到在 **STATSPACK** 实用程序输出中标题为 **Dictionary Cache**（字典缓存）的部分中。

