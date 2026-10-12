
## 17. 如果使用物化视图，必须将哪个 `init.ora` 参数设置为 `TRUE`？

- A. `FAST_REFRESH`
- B. `QUERY_REWRITE`
- C. `QUERY_REWRITE_ENABLED`
- D. `MATERIALIZED_VIEWS`

## 18. 以下哪种类型的索引将索引列的值和相关行 ID 存储为二进制字符串？

- A. `B-Tree` 索引
- B. 反向键索引
- C. 位图索引
- D. 按位索引

## 19. 以下哪个因素不会使一列成为 `B-Tree` 索引的良好候选项？

- A. 该列中的数据基数较低。
- B. 该列经常用于 SQL 语句的 `WHERE` 子句中。
- C. 对表的大多数查询只返回所有行的一小部分。
- D. 以上都不是。

## 20. 索引组织表将超过索引 `PCTTHRESHOLD` 的行数据存储在哪种类型的段中？

- A. 链段
- B. 超额段
- C. 溢出段
- D. 索引段

## 21. Oracle9i 基于成本的优化器在确定 SQL 语句的成本时使用以下所有统计信息，除了：

- A. 逻辑 I/O
- B. 网络负载
- C. CPU 成本
- D. 执行的排序量

## 22. DBA 希望分析一个模式并仅为当前没有统计信息的表收集统计信息。应该使用哪个 `DBMS_STATS` 过程来执行此活动？

- A. `GATHER_SCHEMA_STATS`，`OPTIONS` 参数设置为 `GATHER_EMPTY`
- B. `GATHER_SCHEMA_STATS`，`OPTIONS` 参数设置为 `GATHER_AUTO`
- C. `GATHER_SYSTEM_STATS`，`OPTIONS` 参数设置为 `GATHER_STALE`
- D. `GATHER_SYSTEM_STATS`，`OPTIONS` 参数设置为 `GATHER_EMPTY`

## 23. 此示例中使用的是哪种类型的分区？

```sql
SQL> CREATE TABLE student_history
   2 (student_id NUMBER(10),
   3 degree VARCHAR2(3),
   4 graduation_date DATE,
   5 final_gpa NUMBER)
   6 PARTITION BY RANGE (graduation_date)
  11 PARTITION p_1999 VALUES LESS THAN
  12 (TO_DATE('01-JUN-1999', 'DD-MON-YYYY')) TABLESPACE hist_tab01,
  13 PARTITION p_2000 VALUES LESS THAN
  14 (TO_DATE('01-JUN-2000', 'DD-MON-YYYY')) TABLESPACE hist_tab02,
  15 PARTITION p_2001 VALUES LESS THAN
  16 (TO_DATE('01-JUN-2001', 'DD-MON-YYYY')) TABLESPACE hist_tab03,
  17 PARTITION p_ERR0R VALUES LESS THAN
  18 (MAXVALUE) TABLESPACE hist_tab04);
```

- A. 哈希
- B. 范围
- C. 复合
- D. 列表

## 24. 给定下列分区表，如果用户尝试向学位列插入值为 *MD* 的行，会发生什么情况？

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
- C. Oracle 会允许插入该值，但 `COMMIT` 操作将失败。
- D. Oracle 会在插入该行时生成一个错误。

## 25. 当索引中的分区数与底层表的分区以一对一方式匹配时，分区化索引被称为 ______________________。

- A. 复合（Composite）
- B. 全局（Global）
- C. 局部（Local）
- D. 均匀（Uniform）

### 复习题答案

- C. 在使用 `TKPROF` 格式化用户跟踪文件后，格式化后的跟踪文件将包含查询解析（Parse）、执行（Execute）和获取（Fetch）阶段的 CPU 时间和经过时间的计时数据（假设 `init.ora` 参数 `TIMED_STATISTICS = TRUE`）。
- A. `TKPROF` 实用程序中的 `SYS=NO` 参数会导致原始跟踪文件中的任何递归 SQL 被省略在格式化后的跟踪文件之外。递归 SQL 语句的一个例子是在执行 SQL 语句期间对数据字典的调用。
- B. `ELAPSED` `TKPROF` 统计信息表示处理语句中所有解析、执行或获取调用所花费的总秒数。
- D. 如果 `init.ora` 参数 `TIMED_STATISTICS` 未设置为 `TRUE`，则格式化后的 `TKPROF` 文件中的所有计时值将为 0。
- A. 全表扫描会导致 Oracle 读取表的每一行。当对表执行全表扫描但查询只返回表中总行数中很少一部分时，应调查合适的索引策略。
- C. 将查询 `PLAN_TABLE` 以提供使用 `EXPLAIN PLAN` 语法生成的执行计划信息。`PLAN_TABLE` 是通过运行 `utlxplan.sql` 脚本创建的。
- C. 此语句将导致 Oracle 计算 `EMP` 表的统计信息，包括表本身及与该表相关的所有索引的统计信息。由于样本百分比大于 50%，因此将执行计算（compute）。
- A. `init.ora` 的有效优化器模式为 `RULE`、`CHOOSE`、`FIRST_ROWS` 和 `ALL_ROWS`。
- B. 即使在 `init.ora` 中优化器模式设置为 `CHOOSE`，如果不存在统计信息，也将使用基于规则（rule-based）的优化。
- B. `DBMS_STATS` 包可用于分析给定模式、索引或整个数据库中的所有对象。
- C. `DBA_TABLES` 数据字典视图还包含有关表使用的块数以及每行表平均长度的统计信息。
- D. 直方图通过将列数据分成片段并在分析每个片段内的数据，提供了关于数据分布的更好视图。
- D. 优化器模式可以使用 `init.ora` 参数 `OPTIMIZER_MODE` 在实例级别设置，使用 `ALTER SESSION` 命令在会话级别设置，或使用提示（hints）在语句级别设置。
- A. 存储轮廓（Stored outlines）对于任何与原始 SQL 语句完全匹配的后续 SQL 语句，都使用在创建时生成的执行计划。
- D. 除非指定类别，否则存储轮廓将存储在 `DEFAULT` 类别中。可以使用 `OUTLN_PKG.UPDATE_BY_CAT` 过程将存储轮廓移动到其他类别。
- C. `REFRESH COMPLETE` 选项导致物化视图在底层表的每次提交（commit）时进行刷新。`REFRESH FAST` 选项仅用自上次刷新以来添加的数据更新视图。
- C. 通过使用 `/*+ REWRITE */` 提示，也可以启用语句级别的物化视图。
- C. 位图索引将索引列值存储为 1 和 0 的二进制字符串。
- A. 高基数（high cardinality）列最适合 `B-Tree` 索引。低基数列更适合位图索引。
- C. Oracle 将长度超过 `PCTTHRESHOLD` 值的行存储在溢出段（overflow segment）中。行的第一部分，直到 `INCLUDING` 子句中指定的列，存储在索引中。行的剩余部分存储在溢出段中。
- B. 基于成本的优化器（CBO）在创建 SQL 执行计划时使用多个权重因子，包括逻辑 I/O、`CPU` 成本以及执行的排序量。它未将网络负载计入其计算中。
