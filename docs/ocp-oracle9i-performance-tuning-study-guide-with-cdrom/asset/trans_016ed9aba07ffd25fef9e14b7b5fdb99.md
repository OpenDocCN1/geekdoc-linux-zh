
## 数据字典缓存

每当发出 SQL 或 PL/SQL 语句时，也必须检查数据字典，以确保语句中引用的表存在、列名和数据类型正确，并且发出该语句的应用程序用户对所涉及的段具有足够的权限。与语句本身一样，这些信息也被缓存在共享池中的 *Data Dictionary Cache*（数据字典缓存）内存中。该内存区域也使用 LRU 机制进行管理。

通过使用数据字典缓存，Oracle 服务器将数据字典信息缓存在与相关 SQL 语句不同的内存区域中。这在两方面很有用：

- 库缓存和数据字典缓存的 LRU 机制独立工作。这倾向于使数据字典信息在内存中停留更长时间。
- 后续发出与之前用户相似但不完全相同的语句的应用程序用户会受益于数据字典信息可能已在内存中的事实——即使实际语句不在内存中。

## 用户全局区域

用户全局区域（UGA）仅在使用共享服务器选项时存在于共享池中。在共享服务器体系结构中，*User Global Area*（用户全局区域）用于缓存应用程序用户会话信息。由于共享服务器体系结构使用几个不同的共享服务器进程来处理针对实例的 SQL 和 PL/SQL 活动，因此这些信息必须存储在共享位置中。由于启动事务的共享服务器进程可能不是结束该事务的进程，因此对与会话信息的访问必须存储在 UGA 中。在非共享（或专用）服务器情况下，此会话信息维护在应用程序用户的私有 *Process Global Area*（进程全局区域，PGA）中。

> **注意**
>
> 有关调优共享服务器配置的更多详细信息，请参阅本书第 6 章“调优其他 SGA 区域”。

## 测量共享池的性能

共享池性能的主要指标是缓存命中率。高缓存命中率表明您的应用程序用户经常在内存中找到他们发出的 SQL 和 PL/SQL 语句。*命中率*可以针对库缓存和数据字典缓存分别计算。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_250_0.png)

> 注意
>
> Oracle 建议先调优库缓存以最大化其命中率，然后再尝试调优数据库缓冲区缓存，因为库缓存未达到最佳命中率对性能的影响比数据库缓冲区缓存表现不佳的影响更大。

### 测量库缓存的性能

库缓存的性能通过计算其命中率来衡量。此命中率信息可以在四个地方找到：**V$LIBRARYCACHE** 动态性能视图、**STATSPACK** 和 **REPORT.TXT** 输出，以及性能管理器 GUI 工具的输出。

**Oracle 目标**
测量和调优库缓存命中率

### 使用 V$LIBRARYCACHE 监控库缓存

库缓存未命中可能发生在 SQL 语句处理的解析或执行阶段。与解析阶段相关的缓存命中率显示在 **V$LIBRARYCACHE** 的 **GETHITRATIO** 列中。与执行阶段相关的缓存命中率显示在 **V$LIBRARYCACHE** 的 **PINITRATIO** 列中。**V$LIBRARYCACHE** 的 **RELOADS** 和 **INVALIDATIONS** 列对于库缓存调优也很有用。这里包含了一个查询 **V$LIBRARYCACHE** 并显示这些列的示例查询，见 4.2 图。

**图 4.2 V$LIBRARYCACHE 示例查询**

```sql
SQL> SELECT namespace, gethitratio, pinhitratio, reloads, invalidations
  2  FROM v$librarycache
  3  WHERE namespace IN ('SQL AREA',
  4    'TABLE/PROCEDURE',
  5    'BODY',
  6    'TRIGGER');
```

| NAMESPACE | GETHITRATIO | PINHITRATIO | RELOADS | INVALIDATIONS |
| :--- | :--- | :--- | :--- | :--- |
| SQL AREA | .915877437 | .937549722 | 10 | 2 |
| TABLE/PROCEDURE | .799093656 | .807164634 | 0 | 0 |
| BODY | .7 | .625 | 0 | 0 |
| TRIGGER | 1 | 1 | 0 | 0 |

上图中 **NAMESPACE** 列显示了缓存代码的来源。表 4.3 展示了每种命名空间类型的定义。

**表 4.3 按命名空间类型划分的代码来源**

| 命名空间 | 代码来源 |
| :--- | :--- |
| SQL AREA | SQL 语句 |
| TABLE/PROCEDURE | PL/SQL 存储过程或函数 |
| BODY | PL/SQL 包体 |
| TRIGGER | PL/SQL 触发器 |

在 **V$LIBRARYCACHE** 中发现的 **NAMESPACE** 的其他值指用于确定缓存对象与语句之间依赖关系的信息。就数据库调优而言，这些值对您价值不大。

#### GETHITRATIO

在 **V$LIBRARYCACHE** 中，Oracle 使用术语 *get* 来指代一种称为 *Parse Lock*（解析锁）的锁，这种锁是在解析阶段针对引用该对象的语句所获取的。每次解析语句时，**V$LIBRARYCACHE** 视图中 GETS 的值增加 1。**GETHIT** 列存储应用程序发出的 SQL 和 PL/SQL 语句在内存中发现已解析副本的次数。当这种情况发生时，无需解析语句。用户的服务器进程只是执行内存中已有的副本。已解析语句（GETS）与无需解析的语句（GETHITS）的比率在 V$LIBRARYCACHE 的 GETHITRATIO 列中计算。在 4.2 图的示例输出中，我们的应用程序用户在 91.5% 的时间内发现他们发出的 SQL 语句已在库缓存中（即 GETHITRATIO）。此数值越高，应用程序的性能越好。

> 根据 Oracle 的说法，调优良好的 OLTP 系统可以期望库缓存 SQL 区域部分的 GETHITRATIO 达到 90% 或更高。由于针对 DSS 和数据仓库应用的查询具有临时性（ad hoc nature），因此这些应用的命中率通常较低。

#### PINHITRATIO

PINS 与 GETS 一样，也与锁有关。然而，虽然 GETS 与解析时发生的锁相关，但 PINS 与执行时发生的锁相关。这些锁是在访问对象时使用的短期锁。因此，每个库缓存 GET 在访问语句引用的对象之前，也需要一个相关的 PIN（共享模式或排他模式）。每次执行语句时，PINS 的值增加 1。V$LIBRARYCACHE 中的 PINHITRATIO 列指示已执行的语句在库缓存中发现相关已解析 SQL 的频率。在 4.2 图的示例输出中，这种情况发生的频率为 93.7%（即 PINHITRATIO）。

> Oracle 建议调优良好的 OLTP 系统力争使库缓存 SQL 区域部分的 PINHITRATIO 超过 90%。DSS 和数据仓库应用通常会较低。

#### RELOADS

RELOADS 列显示已执行的语句因库缓存已老化或使语句的已解析版本无效而必须重新解析的次数。可以通过比较已执行的语句数（**PINS**）与需要重新加载的语句数（**RELOADS**）来监控重新加载活动：

```sql
SQL> SELECT SUM(reloads)/SUM(pins) "Reload Ratio"
2 FROM v$librarycache;

Reload Ratio
----------
.001506251
```

在此示例中，我们的重新加载比率为 .0015，或 0.15%。这意味着我们很少重新解析之前加载到库缓存中的语句。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_253_0.png)

#### INVALIDATIONS

当缓存的 SQL 语句被标记为无效，因此即使它已在库缓存中，也被强制进行解析时，就会发生无效化。每当它们引用的对象以某种方式被修改时，缓存的语句就会被标记为无效。例如，重新编译之前由缓存 SQL 语句使用的视图将导致这些缓存语句被标记为无效。因此，后续使用此视图的语句需要被解析，即使该语句的精确副本可能已被缓存。**INVALIDATIONS** 的高值意味着应用程序的额外开销。因此，在权衡可能引起无效化的活动的预期好处时，应考虑这些活动。

### 使用 STATSPACK 监控库缓存

从上述对 V$LIBRARYCACHE 的查询中获得的许多信息也可以在 STATSPACK 实用程序的输出中找到。库缓存性能统计信息包含在 STATSPACK 标题为 **Instance Efficiency Percentages (Target 100%)**（实例效率百分比（目标 100%））的部分中。4.3 图所示的 STATSPACK 输出显示，被监控的数据库的库缓存命中率为 86.11%。

