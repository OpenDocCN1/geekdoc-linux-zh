
## 24. 给定下列分区表，如果用户尝试向学位列插入值为*MD*的行，会发生什么情况？

```sql
SQL> CREATE TABLE student_history
 2  (student_id NUMBER(10),
 3   degree VARCHAR2(3),
 4   graduation_date DATE,
 5   final_gpa NUMBER)
 6  PARTITION BY LIST (degree)
 7  (PARTITION p_undergrad VALUES ('BS','BA','BBA','BFA')
 8   TABLESPACE hist_tab01,
 9   PARTITION p_graduate VALUES ('MA','MBA','MFA','MS')
 10  TABLESPACE hist_tab02,
 11  PARTITION p_doctorate VALUES ('PHD')
 12  TABLESPACE hist_tab03);
```

- A. 它将被放入最后一个分区。
- B. Oracle 会自动创建一个分区，其分区值为 *MD*。
- C. Oracle 会允许插入该值，但 COMMIT 操作将失败。
- D. Oracle 会在插入该行时生成一个错误。

## 25. 当索引中的分区数与底层表的分区以一对一方式匹配时，分区化索引被称为 ______________________。

- A. 复合（Composite）
- B. 全局（Global）
- C. 局部（Local）
- D. 均匀（Uniform）

# 复习题答案

- C. 在使用 TKPROF 格式化用户跟踪文件后，格式化后的跟踪文件将包含查询解析（Parse）、执行（Execute）和获取（Fetch）阶段的 CPU 时间和经过时间的计时数据（假设 `init.ora` 参数 `TIMED_STATISTICS = TRUE`）。
- A. TKPROF 实用程序中的 `SYS=NO` 参数会导致原始跟踪文件中的任何递归 SQL 被省略在格式化后的跟踪文件之外。递归 SQL 语句的一个例子是在执行 SQL 语句期间对数据字典的调用。
- B. ELAPSED TKPROF 统计信息表示处理语句中所有解析、执行或获取调用所花费的总秒数。
- D. 如果 `init.ora` 参数 `TIMED_STATISTICS` 未设置为 TRUE，则格式化后的 TKPROF 文件中的所有计时值将为 0。
- A. 全表扫描会导致 Oracle 读取表的每一行。当对表执行全表扫描但查询只返回表中总行数中很少一部分时，应调查合适的索引策略。
- C. 将查询 PLAN_TABLE 以提供使用 EXPLAIN PLAN 语法生成的执行计划信息。PLAN_TABLE 是通过运行 `utlxplan.sql` 脚本创建的。
- C. 此语句将导致 Oracle 计算 EMP 表的统计信息，包括表本身及与该表相关的所有索引的统计信息。由于样本百分比大于 50%，因此将执行计算（compute）。
- A. `init.ora` 的有效优化器模式为 RULE、CHOOSE、FIRST_ROWS 和 ALL_ROWS。
- B. 即使在 `init.ora` 中优化器模式设置为 CHOOSE，如果不存在统计信息，也将使用基于规则（rule-based）的优化。
- B. DBMS_STATS 包可用于分析给定模式、索引或整个数据库中的所有对象。
- C. DBA_TABLES 数据字典视图还包含有关表使用的块数以及每行表平均长度的统计信息。
- D. 直方图通过将列数据分成片段并在分析每个片段内的数据，提供了关于数据分布的更好视图。
- D. 优化器模式可以使用 `init.ora` 参数 `OPTIMIZER_MODE` 在实例级别设置，使用 ALTER SESSION 命令在会话级别设置，或使用提示（hints）在语句级别设置。
- A. 存储轮廓（Stored outlines）对于任何与原始 SQL 语句完全匹配的后续 SQL 语句，都使用在创建时生成的执行计划。
- D. 除非指定类别，否则存储轮廓将存储在 DEFAULT 类别中。可以使用 OUTLN_PKG.UPDATE_BY_CAT 过程将存储轮廓移动到其他类别。
- C. REFRESH COMPLETE 选项导致物化视图在底层表的每次提交（commit）时进行刷新。REFRESH FAST 选项仅用自上次刷新以来添加的数据更新视图。
- C. 通过使用 /*+ REWRITE */ 提示，也可以启用语句级别的物化视图。
- C. 位图索引将索引列值存储为 1 和 0 的二进制字符串。
- A. 高基数（high cardinality）列最适合 B-Tree 索引。低基数列更适合位图索引。
- C. Oracle 将长度超过 PCTTHRESHOLD 值的行存储在溢出段（overflow segment）中。行的第一部分，直到 INCLUDING 子句中指定的列，存储在索引中。行的剩余部分存储在溢出段中。
- B. 基于成本的优化器（CBO）在创建 SQL 执行计划时使用多个权重因子，包括逻辑 I/O、CPU 成本以及执行的排序量。它未将网络负载计入其计算中。
- 22. A. DBA 应使用 GATHER_SCHEMA_STATS 过程，并将 OPTIONS 参数设置为 GATHER_EMPTY。这将仅收集尚未收集统计信息的表的统计信息。
- 23. B. 这是一个范围分区（Range partitioned）表的示例。
- 24. D. Oracle 不允许将 MD 值放入表中，并在插入时生成 ORA-14400 错误。
- 25. C. 局部分区索引具有与底层表分区以一对一方式匹配的分区键。

# 调整共享池

## 本章涵盖的 ORACLE 9i 性能调整考试目标：

- ✔ 测量和调整库缓存（Library Cache）命中率
- ✔ 测量和数据字典缓存（Dictionary Cache）命中率
- ✔ 调整共享池中的对象大小并固定（pin）对象
- ✔ 调整共享池保留空间
- ✔ 描述 UGA 和会话内存考虑事项
- ✔ 解释与共享池相关的其他调整问题

> 考试目标可能会随时在没有预先通知的情况下由 Oracle 独家酌情变更。请访问 Oracle 认证网站 (http://www.oracle.com/education/certification/) 查看当前的考试目标列表。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_241_0.png)

![](img/832fbc6aca8b6075843ca6f2356c0a8d_242_0.png)

上一章展示了如何识别和解决应用程序 SQL 代码中的性能瓶颈。这是数据库调整中非常重要的一部分，因为重写性能较差的 SQL 可以对基于 Oracle 的应用程序的性能产生巨大影响。然而，试图通过重写应用程序 SQL 来提高数据库性能往往不是一个选项，特别是在涉及生产应用程序或第三方应用程序（你可能无法访问其 SQL 代码）的情况下。在这种情况下，当涉及到调整时，你有以下选项：

- 对于购买的应用程序，你可以向供应商投诉并希望他们能解决性能差的问题。
- 你可以在交付的产品中添加自己的索引，希望它们能提高性能。
- 你可以调整 Oracle 的共享内存结构，即 SGA（系统全局区），并尝试通过最小化与 SQL 语句处理以及访问应用程序数据和索引块相关的开销来提高应用程序性能。

认识到第三个选项可能会带来最大的性能提升，在接下来的四章中，我们将讨论调整 Oracle SGA 组件的问题。本章涉及调整共享池；第 5 章“调整数据库缓冲区缓存”讨论调整数据库缓冲区缓存；第 6 章“调整其他 SGA 区域”涵盖调整大池（Large Pool）、Java 池和共享服务器 SGA 组件；第 7 章“调整重做机制”讨论调整重做日志缓冲区。

## 理解共享池

**共享池**是 SGA 中缓存应用程序用户最近发出的 SQL 和 PL/SQL 语句的部分。共享池由*最近最少使用*（LRU）算法管理。一旦共享池已满，该算法会通过淘汰最近最少访问的语句来为后续的 SQL 语句腾出空间。通过这种方式，Oracle 服务器将“热门”的 SQL 和 PL/SQL 语句保留在共享池中，而不常用的语句则被逐步淘汰。通过在内存中缓存这些经常使用的语句，发出与之前用户相同 SQL 或 PL/SQL 语句的应用程序用户将受益于此，因为该语句已经在内存中，随时可以执行。这对后续的应用程序用户非常有用，因为他们可以跳过在最初发出语句时产生的一些开销。

### 语句缓存的好处

当应用程序用户向 Oracle 实例发出 SQL 或 PL/SQL 语句时，在语句实际执行之前会发生几个操作。例如，让我们看看发出以下 SQL 语句时会发生什么：

```sql
SQL> SELECT last_name, first_name
  2  FROM customers
  3  WHERE customer_id = 2201;
```

首先，Oracle 将语句中的字符转换为其 ASCII 等价数字代码。接下来，这个 ASCII 字符字符串通过一个哈希算法，从而产生一个单一的哈希值。用户的服务器进程然后检查该哈希值是否已存在于共享池中。如果存在，用户的服务器进程使用语句的缓存版本来执行该语句。

如果共享池中不存在该哈希值，用户的服务器进程将进行语句的解析过程，然后执行它。这个额外的解析步骤会增加每个 SQL 操作的开销，因为解析步骤必须完成以下任务：

- 检查语句的语法正确性。

