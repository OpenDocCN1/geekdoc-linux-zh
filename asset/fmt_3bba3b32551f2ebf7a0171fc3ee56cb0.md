
### 7. DBA 和开发者正在为大学构建一个学生记录系统。他们决定使用以下语法创建一个 `STUDENT_HISTORY` 表。该表将如何分区？

```sql
SQL> CREATE TABLE student_history
2 (student_id NUMBER(10),
3 degree VARCHAR(3),
4 graduation_date DATE,
5 final_gpa NUMBER)
6 PARTITION BY RANGE (graduation_date)
7 SUBPARTITION BY HASH(student_id) SUBPARTITIONS 4
8 STORE IN (hist_tab01, hist_tab02, hist_tab03, hist_tab04)
9 (PARTITION p_1997 VALUES LESS THAN
10 (TO_DATE('01-JUN-1997', 'DD-MON-YYYY')),
11 PARTITION p_1998 VALUES LESS THAN
12 (TO_DATE('01-JUN-1998', 'DD-MON-YYYY')),
13 PARTITION p_1999 VALUES LESS THAN
14 (TO_DATE('01-JUN-1999', 'DD-MON-YYYY')),
15 PARTITION p_2000 VALUES LESS THAN
16 (TO_DATE('01-JUN-2000', 'DD-MON-YYYY')),
17 PARTITION p_2001 VALUES LESS THAN
18 (TO_DATE('01-JUN-2001', 'DD-MON-YYYY')),
19 PARTITION p_ERROR VALUES LESS THAN (MAXVALUE));
```

A. 哈希 (`Hash`)

B. 列表 (`List`)

C. 范围 (`Range`)

D. 复合 (`Composite`)

### 8. 实例级别同时可以有多少个数据库资源计划处于激活状态？

A. 全部

B. 都没有

C. 一个

D. 最多四个

### 9. 您的数据库处于 `ARCHIVELOG` 模式且发生了日志切换（log switch）。正在切换的在线重做日志尚未归档。会发生什么？

A. `LGWR` 将覆盖该日志。

B. 实例将崩溃。

C. 将创建额外的日志以适应日志请求。

D. `LGWR` 将等待 `ARC` 完成在线重做日志文件的归档。

### 10. 哪个命令不会导致 `DBWn` 写入脏块（dirty blocks）？

A. `ALTER TABLESPACE BEGIN BACKUP`

B. `SHUTDOWN IMMEDIATE`

C. `SHUTDOWN ABORT`

D. `ALTER SYSTEM SWITCHFILE`

### 11. 以下哪项不是性能的两个原则之一？

A. 向服务器添加内存

B. 增加应用程序可用的磁盘数量

C. 减少用户数量

D. 增加 `SGA` 的大小

### 12. 一初级 DBA 决定每天检查警日志（Alert log）以确定是否存在性能问题。DBA 可能会在警日志中发现哪些类型的信息（选择三项）？

A. 实例启动和关闭

B. 重做日志切换（Redo log switches）

C. 创建用户

D. 表空间创建

### 13. `SGA` 中留存最近执行的 SQL 的位置称为什么？

A. 大池 (`Large Pool`)

B. 数据库缓存 (`Database Cache`)

C. 重做日志缓冲区 (`Redo Log Buffer`)

D. 共享池 (`Shared Pool`)

### 14. 以下哪个命令不会引起排序？

A. `ORDER BY`

B. `ANALYZE TABLE`

C. `SELECT DISTINCT`

D. `INTERSECT`

E. 以上均可能导致排序。

### 15. 在创建资源组、资源计划时，以下哪项正确？（选择所有适用）

A. 参数必须带有 `=>`。

B. 参数必须包含引号。

C. 命令必须在一行内。

D. 以上均正确。

### 16. 当发生死锁时，哪个会会被回滚？

A. 引起死锁的会

B. 检测死锁的会

C. 工作量最少的会

D. 最后登录的会

### 17. DBA 有三个管理目标：恢复性、可靠性和可扩展性。Oracle 的哪个功能解决了哪个？

A. 性能

B. 可扩展性

C. 可靠性

D. 安全

### 18. 您对怀疑需要调优的 SQL 语句的执行计划感兴趣。您想保存这些信息。您首先应该做什么？

A. 运行 `TKPROF`。

B. 使用 `Explain plan for...` 语法运行。

C. 在 `SQL*Plus` 中设置 `AUTOTRACE`。

D. 运行 `uxplan`。

### 19. 您使用以下语法创建一个表：

```sql
CREATE TABLE EMP_HOLD SELECT * FROM EMP NOLOGGING;
```

为了确保 `EMP_HOLD` 的恢复性，在该语句后应该做什么？

A. 停止并启动 实例。

B. 执行 `COMMIT`。

C. 执行热备或冷备。

D. 手动切换日志。

### 20. 以下是收集数据库缓存命中率的方法，除了哪个？

A. `UTLSTAT/LBSTAT`

B. `STATSPACK`

C. `V$SYSSTAT`

D. `V$DB_CACHE`

### 21. 一个组织决定增加与他们的应用程序交互的用户数量。这是哪种调优周期变更？

A. 设计

B. 配置

C. 工作负载

D. 应用设计

### 22. 关于 `V$SESSION` 和 `V$SYSSTAT` 视图之间的差异，以下哪些述是错误的？（选择两个）

A. `V$SESSION` 显示会话统计，`V$SYSSTAT` 显示实例级统计。

B. `V$SESSION` 包含用户名，`V$SYSSTAT` 不包含。

C. `V$SESSION` 显示已连接会话，`V$SYSSTAT` 显示自实例启动以来所有会话的累计统计。

D. `V$SESSION` 和 `V$SYSSTAT` 的统计在实例启动后最准确。

### 23. Oracle 建议将 CPU 利用率保持在百分之几以下获得获得性能？

A. 70

B. 80

C. 90

D. 100

### 24. 如果尺寸合理，共享池将在 90% 以上的时间内缓存应用程序 SQL 和 PL/SQL。这对于以下原因很重要？（选择三项）

A. 减少整体内存开销

B. 减少 I/O

C. 减少 CPU 利用率

D. 最小化锁定

### 25. 哪个 GUI 工具最适合监控 Oracle 的锁定机制？

A. Top Sessions

B. Lock Monitor

C. Trace Data Viewer

D. SQL Analyze

### 26. 在对数据库进行调优工作之前，应该建立基准。这些基准应该在哪些领域建立？（选择三项）

A. 响应时间

B. 内存芯片数量

C. CPU 利用率

D. 服务器电源供应数量

E. 物理 I/O 和内存消耗

### 27. 从以下查询中可以观察到什么？

```sql
SQL> SELECT owner, segment_type,
2 segment_name, buffer_pool
3 FROM dba_segments;
```

| OWNER | SEGMENT_TYPE | SEGMENT_NAME | BUFFER_ |
| :--- | :--- | :--- | :--- |
| APPS | TABLE | EMPLOYEE | DEFAULT |
| APPS | TABLE | REGION | KEEP |
| APPS | TABLE | DIVISION | RECYCLE |
| APPS | INDEX | EMPLOYEE_FIRST_NAME_IDX | DEFAULT |
| APPS | INDEX | EMPLOYEE_ID_PK | RECYCLE |
| APPS | TABLE | SALES_HISTORY | RECYCLE |

A. `REGION` 表可能是一个非常大且不经常使用的表。

B. `DIVISION` 表的块将被放置在 LRU 单元的 MRU 端。

C. `REGION` 表可能是一个小的代码表。

D. 我们希望在数据库缓冲区缓存中保留 `SALES_HISTORY` 表的块。

### 28. 这些进程中哪一个负责将数据从在线重做日志（Online Redo Logs）复制到归档日志（archive logs）？

A. `ARCO`

B. `LGWR`

C. `DBW0`

D. `PMON`

### 29. 你想根据唯一列创建一个分区表。你想确保 Oracle 能够每个分的行分布得相当均匀。哪种类型的分区方案可以确保给定分区之间具有高度的分布？

A. 哈希（Hash）

B. 范围（Range）

C. 列表（List）

D. 这些分区类型的效果都一样好。

### 30. DBA 正在调查一个非常大的 SQL 语句的问题，需要查看执行时的完整 SQL 语句。找到 SQL 完整文本的最佳方法是：

A. `V$SQLAREA`

B. `V$SQLTEXT`

C. `V$SQL`
