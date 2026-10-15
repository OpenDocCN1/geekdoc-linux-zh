
与 `OLTP` 系统一样，如果使用 `CBO`，也应在使用每次数据加载后收集数据库统计信息。

# 调优混合系统：OLTP 和 DSS

某些系统是 `OLTP` 和 `DSS` 的结合。这些*混合*系统可能带来重大挑战，因为帮助一种系统类型的调优选项通常会妨碍另一种系统类型。然而，通过仔细使用索引和资源管理，通常可以实现一定程度的共存。随着对这两种系统的需求增长，你可能最终需要将这两种类型的系统拆分为两个独立的环境，以满足两个用户群体的需求。

# 摘要

了解如何使用 `TKPROF`、`执行计划`、`STATSPACK` 和 `AUTOTRACE` 来分析应用程序 `SQL` 处理对于每个 `DBA` 来说都很重要。这些工具不仅允许你了解应用程序 `SQL` 是如何执行的，还了解与这些执行相关的资源成本。

数据库性能的一个主要决定因素是 Oracle 优化器做出良好的 `SQL` 执行选择的程度。这些选择受优化器模式和数据库统计信息的存在或缺失的影响。这些统计信息可以在段、模式或数据库级别收集。统计信息也可以在数据库之间移动，以便可以使用现实数据测试优化器的行为。

有各种方法可用于提高应用程序性能。这些方法包括存储大纲、物化视图、`B-Tree` 索引、位图索引、基于函数的索引、压缩索引、Reverse Key 索引、索引组织表、索引集群和哈希集群。这些选项的适用性随所管理系统的类型而变化。`OLTP` 系统的索引策略与 `DSS` 环境不同。

### 考试要点

描述 `SQL` 分析的工具。了解如何使用 `TKPROF`、`AUTOTRACE`、执行计划（Explain Plans）和 `STATSPACK` 来执行 `SQL` 分析。知道如何根据潜在的性能调优改进来解释这些工具的输出。

理解优化器的作用。了解 Oracle 优化器的重要性以及如何管理其行为。理解数据库可以运行的优化器模式，以及每种模式如何受数据库统计信息的存在或缺失的影响。

了解不同的索引策略。能够描述每种索引类型及其如何用于改进 `SQL` 执行。理解每种索引类型适用的情况。

了解不同的调优要求。理解 `OLTP`、`DSS` 和混合系统之间的调优目标有何不同。能够将本章讨论的所有调优考虑因素置于每种这些调优环境的框架内。

## 关键术语

在参加考试之前，请确保你熟悉以下术语：

- Autorace
- Bitmap
- 数据块 (blocks)
- B-Tree
- 基数 (Cardinality)
- 集群 (cluster)
- 复合分区 (composite partitioning)
- 压缩 (Compressed)
- 基于成本的优化器 (CBO)
- 决策支持系统 (DSS)
- 执行 (Execute)
- 执行计划 (Explain Plan)
- 获取 (Fetch)
- 基于函数的索引 (Function-based indexes)
- 获取 (Get)
- 哈希集群 (Hash clusters)
- 哈希分区 (Hash partitions)
- 堆表 (Heap Tables)
- 提示 (Hints)
- 直方图 (Histogram)
- 索引集群 (Index clusters)
- 索引组织表 (IOTs)
- 列表分区 (List partitions)
- 映射表 (Mapping Table)
- 物化视图 (Materialized views)
- 在线事务处理
- 解析 (Parsing)
- 分区裁剪 (partition pruning)
- 分区 (partitions)
- 计划等价 (plan equivalence)
- 私有概要文件 (Private Outline)
- 范围分区 (Range partitioning)
- 反向键索引 (RKI)
- 基于规则的优化器
- 存储的概要文件 (stored outlines)
- TKPROF

## 复习题

1. 以下哪个工具可以让你查看 `SQL` 语句在解析、执行和获取上花费了多少 `CPU` 时间？

   - A. `AUTOTRACE`
   - B. 执行计划 (Explain Plan)
   - C. `TKPROF`
   - D. 物化视图

2. 在语句 `tkprof ora_1234.trc trace.txt sys=no explain=joed/sidney@PROD` 中，`sys=no` 的作用是什么？

   - A. 导致原始跟踪文件中的任何递归 `SQL` 都被省略在格式化后的跟踪文件中。
   - B. 强制不计算汇总统计信息。
   - C. 限制包含在结果格式化跟踪中的 `SQL` 语句数量。
   - D. 为跟踪文件中的每个语句生成执行计划。

3. 哪个 `TKPROF` 统计信息提供了处理所有 Parse、Execute 或 Fetch 调用的总秒数？

   - A. `COUNT`
   - B. `ELAPSED`
   - C. `CURRENT`
   - D. `ROWS`

4. 为了使 `TKPROF` 输出包含计时信息，必须将哪个 `init.ora` 参数设置为 `TRUE`？

   - A. `TIMINGS`
   - B. `TIME_QUERY`
   - C. `STATISTICS`
   - D. `TIMED_STATISTICS`

5. 执行计划显示正在访问表中的所有数据块以满足查询。这种类型的表访问叫什么？

   - A. 全表扫描 (Full table scan)
   - B. 嵌套循环 (Nested loop)
   - C. 范围扫描 (Range scan)
   - D. 以上都不是

6. 在对 `SQL` 语句运行执行计划后，你应该查询哪个表来获取信息？

   - A. `SQL_PLAN`
   - B. `SQL_PLAN_TABLE`
   - C. `PLAN_TABLE`
   - D. `EXECUTION_PLAN`

7. 执行以下 `SQL` 语句的结果是什么？

```sql
SQL> ANALYZE TABLE EMP ESTIMATE STATISTICS
   2 SAMPLE 55 PERCENT;
```

   - A. Oracle 将基于 55% 的行样本估算 `EMP` 表及其上所有索引的统计信息。
   - B. Oracle 将仅基于 55% 的行样本估算 `EMP` 表的统计信息。
   - C. Oracle 将计算 `EMP` 表及其上所有索引在 100% 行上的统计信息。
   - D. Oracle 将仅计算 `EMP` 表在 100% 行上的统计信息。

8. 以下哪个不是 `init.ora` 参数 `OPTIMIZER_MODE` 的有效值？

   - A. `COST`
   - B. `RULE`
   - C. `CHOOSE`
   - D. 以上都是有效值。

9. 如果 *init.ora* 优化器模式设置为 **CHOOSE**，但尚未为应用程序的表和索引收集统计信息，Oracle 将使用哪种优化器模式？

   - A. **COST**
   - B. **RULE**
   - C. **HINT**
   - D. 以上都不是

10. 以下哪个 Oracle 包可用于分析特定模式中的所有对象？

    - A. **DBMS_PACKAGE**
    - B. **DBMS_STATS**
    - C. **DBMS_SYSTEM**
    - D. **DBMS_ANALYZE**

11. 在 **ANALYZE** 命令之后，以下哪个数据字典视图将包含表中行数多少的统计信息？

    - A. **DBA_ROWS**
    - B. **DBA_TABLE_ROWS**
    - C. **DBA_TABLES**
    - D. **DBA_STATISTICS**

12. 直方图很有用，因为它们允许优化器更好地了解索引列中的数据是否 ____________________ 均匀。

    - A. 排序
    - B. 命名
    - C. 输入
    - D. 分布

13. 优化器模式可以在以下哪个级别设置？

    - A. 实例
    - B. 会话
    - C. 语句
    - D. 以上所有

14. 能够存储预定义的执行计划，以便优化器提前知道哪个执行计划是最佳的，这种能力叫什么？

    - A. 存储的概要文件
    - B. 物化视图
    - C. 哈希集群
    - D. 索引组织表

15. 如果不指定存储的概要文件所属的类别，它将默认被分配到哪个类别？

    - A. SYSTEM
    - B. TEMP
    - C. USERS
    - D. DEFAULT

16. 如果物化视图在基于它的某个表发生提交时每次都完全刷新，那么创建该视图时使用了哪个选项？

    - A. REFRESH SYNC
    - B. REFRESH FAST
    - C. REFRESH COMPLETE
    - D. REFRESH TOTAL
