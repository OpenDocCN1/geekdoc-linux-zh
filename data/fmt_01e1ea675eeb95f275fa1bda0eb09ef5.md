
`SQL> ANALYZE TABLE EMP ESTIMATE STATISTICS 55;`

- A. 表和所有索引按 55% 估计统计信息。
- B. 仅对 EMP 表按 55% 估计。
- C. EMP 表和所有索引按 100% 计算统计信息。
- D. 仅对 EMP 表按 100% 计算统计信息。

- 8. 下列哪个值不是 `OPTIMIZER_MODE` 参数的有效值？
  - A. `COST`
  - B. `RULE`
  - C. `CHOOSE`
  - D. 以上均有效。

- 9. 如果初始化优化器设置为 `CHOOSE`，但没有收集统计信息，Oracle 将使用哪种优化器模式？
  - A. `COST`
  - B. `RULE`
  - C. `HINT`
  - D. 以上都不是

- 10. 下列哪个 Oracle 包可以用于分析对象？
  - A. `DBMS_PACKAGE`
  - B. `DBMS_STATS`
  - C. `DBMS_SYSTEM`
  - D. `DBMS_ANALYZE`

- 11. 执行 `ANALYZE` 命令后，哪个数据视图包含表行统计信息？
  - A. `DBA_ROWS`
  - B. `DBA_TABLE_ROWS`
  - C. `DBA_TABLES`
  - D. `DBA_STATISTICS`

- 12. 直方图有用是因为它们让优化器能够更好地了解索引列中的数据是否：
  - A. 排序的
  - B. 命名的
  - C. 输入的
  - D. 分布的

- 13. 优化器模式可以在哪些级别设置？
  - A. 实例 (`Instance`)
  - B. 会话 (`Session`)
  - C. 语句 (`Statement`)
  - D. 以上均可。

- 14. 存储预定义执行计划以便优化器提前知道哪种执行计划最好的称为：
  - A. 存储大纲 (`Stored outlines`)
  - B. 物化视图 (`Materialized views`)
  - C. 哈希簇 (`Hash cluster`)
  - D. 索引组织表 (`Index Organized Table`)

- 15. 如果不指定大纲属于哪个类别，它会被分配到哪个类别？
  - A. `SYSTEM`
  - B. `TEMP`
  - C. `USERS`
  - D. `DEFAULT`

- 16. 如果在物化视图基础的基础表发生提交时，物化视图就会完全刷新，那么该视图是用哪个选项创建的？
  - A. `REFRESH SYNC`
  - B. `REFRESH FAST`
  - C. `REFRESH COMPLETE`
  - D. `REFRESH TOTAL`

- 17. 如果要使用物化视图，哪个 `init.ora` 参数必须设置为 TRUE？

复习题 195

+   A. `FAST_REFRESH`
+   B. `QUERY_REWRITE`
+   C. `QUERY_REWRITE_ENABLED`
+   D. `MATERIALIZED_VIEWS`

+   18. 下列哪种类型的索引将被索引列的值和相关的行 ID 以二进制字符串的形式存储？

+   A. B-Tree 索引
+   B. 反向键 (`Reverse Key index`)
+   C. 位图索引 (`Bitmap index`)
+   D. 位运算索引 (`Bitwise index`)

+   19. 下列哪个因素不会使某列成为 B-Tree 索引的良好候选？

+   A. 列中的数据基数较低
+   B. 该列经常在 SQL 语句子句中使用。
+   C. 表上的大多数查询只返回表的一小部分行。
+   D. 以上都不是。

+   20. 索引组织表将超过索引 `PCTTHRESH` 的行数据存储在何种类型的段中？

+   A. 链段 (`Chain Segment`)
+   B. 溢出段 (`Excess Segment`)
+   C. 溢出段 (`Overflow Segment`)
+   D. 索引段 (`Index segment`)

+   21. Oracle9i 基于成本的优化器在确定 SQL 语句成本时使用了以下所有统计信息，：

+   A. 逻辑 I/O
+   B. 网络 I/O
+   C. CPU 成本
+   D. 执行的排序量

22. DBA 想要分析模式并仅对当前没有统计信息的表收集统计信息。应该使用哪个 `DBMS_STATS` 过程来执行此活动？

+   A. `GATHER_SCHEMA_STATS`，并将 `OPTIONS` 参数设置为 `GATHER EMPTY`
+   B. `GATHER_SCHEMA_STATS`，并将 `OPTIONS` 参数设置为 `GATHER AUTO`
+   C. `GATHER_SYSTEM_STATS`，并将 `OPTIONS` 参数设置为 `GATHER STALE`
+   D. `GATHER_SYSTEM_STATS`，并将 `OPTIONS` 参数设置为 `GATHER EMPTY`

23. 此示例中使用的是哪种分区类型？

```sql
SQL> CREATE TABLE student_history
2 (student_id NUMBER(10),
3 degree VARCHAR(3),
4 graduation_date DATE,
5 final_gpa NUMBER
6 PARTITION BY RANGE (graduation_date)
11 PARTITION p_1999 VALUES LESS THAN
12 (TO_DATE('01-JUN-1999', 'DD-MON-YYYY')) TABLESPACE hist_tab01,
13 PARTITION p_2000 VALUES LESS THAN
14 (TO_DATE('01-JUN-2000', 'DD-MON-YYYY')) TABLESPACE hist_tab02,
15 PARTITION p_2001 VALUES LESS THAN
16 (TO_DATE('01-JUN-2001', 'DD-MON-YYYY')) TABLESPACE hist_tab03,
17 PARTITION p_error VALUES LESS THAN
18 (MAXVALUE) TABLESPACE hist_tab04);
```

+   A. 哈希 (`Hash`)
+   B. 范围 (`Range`)
+   C. 复合 (`Composite`)
+   D. 列表 (`List`)

24. 给定下面的分区表，如果用户尝试向 `degree` 列中插入值为 `MD` 的行，会发生什么？

```sql
SQL> CREATE TABLE student_history
2 (student_id NUMBER(10),
3 degree VARCHAR2(3),
4 graduation_date DATE,
5 final_gpa NUMBER)
6 PARTITION BY LIST (degree)
7 (PARTITION p_undergrad VALUES ('BS','BA','BBA','BFA')
8 TABLESPACE hist_tab01,
9 PARTITION p_graduate VALUES ('MA','MBA','MFA','MS')
10 TABLESPACE hist_tab02,
11 PARTITION p_doctorate VALUES ('PHD')
12 TABLESPACE hist_tab03);
```
