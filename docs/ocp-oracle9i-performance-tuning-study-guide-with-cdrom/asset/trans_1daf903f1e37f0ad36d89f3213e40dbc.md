
### 19. 以下哪项操作**不会**导致数据库生成重做日志条目？

- A. 停止并启动 Oracle 实例。
- B. 发出 COMMIT 语句。
- C. 执行热备份或冷备份。
- D. 执行手动日志切换。

### 20. 以下都是收集数据库缓冲区命中率测量值的方法，除了哪一项？

- A. UTLBSTAT/UTLLESTAT
- B. STATSPACK
- C. V$SYSSTAT
- D. V$DB_CACHE

### 21. 一个组织决定增加与他们的 Oracle 应用程序交互的用户数量。这属于哪种类型的调优生命周期变更？

- A. 设计变更
- B. 配置变更
- C. 工作负载变更
- D. 应用程序设计变更

### 22. 关于 V$SESSTAT 和 V$SYSSTAT 视图之间差异的下列陈述中，哪些是不正确的？（选择两项。）

- A. V$SESSTAT 显示每个会话的统计信息，V$SYSSTAT 显示实例范围的统计信息。
- B. V$SESSTAT 包含用户名，V$SYSSTAT 不包含。
- C. V$SESSTAT 显示已连接会话的统计信息，V$SYSSTAT 显示自实例启动以来所有已连接会话的累计统计信息。
- D. V$SESSTAT 和 V$SYSSTAT 中的统计信息在实例启动后立即最准确。

### 23. Oracle 建议 CPU 使用率保持在什么百分比以下以获得最佳性能？

- A. 70
- B. 80
- C. 90
- D. 100

### 24. 如果共享池（Shared Pool）大小设置得当，在 OLTP 系统中，它将在内存中缓存应用程序的 SQL 和 PL/SQL，命中率达到 90% 或更高。这对以下哪些原因很重要？（选择三项。）

- A. 减少总体内存开销
- B. 减少 I/O
- C. 减少 CPU 使用率
- D. 最小化锁定

### 25. 以下哪个 GUI 工具最适合监控 Oracle 的锁定机制？

- A. Top Sessions
- B. Lock Monitor
- C. Trace Data Viewer
- D. SQL Analyze

### 26. 在对数据库进行调优工作之前，应建立基准。应在哪些领域进行这些基准测试？（选择三项。）

- A. 响应时间
- B. 内存芯片数量
- C. CPU 使用率
- D. 服务器电源数量
- E. 物理 I/O 和内存消耗

### 27. 从以下查询中可以得出什么观察结果？

```sql
SQL> SELECT owner, segment_type,
       2  segment_name, buffer_pool
       3  FROM dba_segments;

OWNER SEGMENT_TYPE SEGMENT_NAME              BUFFER_
----- ------------ ------------------------- --------
APPS  TABLE  EMPLOYEE                       DEFAULT
APPS  TABLE  REGION                          KEEP
APPS  TABLE  DIVISION                        RECYCLE
APPS  INDEX  EMPLOYEE_FIRST_NAME_IDX         DEFAULT
APPS  INDEX  EMPLOYEE_ID_PK                  RECYCLE
APPS  TABLE  SALES_HISTORY                   RECYCLE
```

- A. REGION 表可能是一个非常大且不经常使用的表。
- B. DIVISION 表的块将被放置在 LRU 列表的 MRU 端。
- C. REGION 表可能是一个小型代码表。
- D. 我们希望在数据库缓冲区中保留 SALES_HISTORY 表的块。

### 28. 下列哪个进程负责将数据从联机重做日志复制到归档日志？

- A. ARC0
- B. LGWR
- C. DBW0
- D. PMON

### 29. 你想基于一个唯一列创建分区表。你希望确保 Oracle 在各分区之间保持相当均匀的每分区行数分布。哪种类型的分区方案能确保给定分区之间的高度分布？

- A. 哈希（Hash）
- B. 范围（Range）
- C. 列表（List）
- D. 这些分区类型的工作效果都一样好。

### 30. DBA 正在调查一个非常大的 SQL 语句的问题，需要查看该 SQL 语句执行时的完整文本。查找完整 SQL 文本的最佳视图是：

- A. V$SQLAREA
- B. V$SQLTEXT
- C. V$SQL
- D. V$SQL_PLAN

### 31. DBA 有兴趣为运行第三方应用程序的客户端设置跟踪。由于他无法直接访问应用程序代码或客户端会话，启动此跟踪会话的正确方法是使用什么？

- A. 在 `init.ora` 文件中设置 SQL_TRACE=TRUE。
- B. 对他想要跟踪的会话执行 DBMS_SYSTEM.SET_SQL_TRACE_IN_SESSION。
- C. 对客户端会话执行 ALTER SESSION SET SQL_TRACE=TRUE。
- D. 无法直接跟踪另一个客户端会话。

### 32. DBA 正在制定数据库性能调优的部门准则。这些准则应包括以下哪些项目？（选择三项。）

- A. 性能调优是一个迭代过程。
- B. 当对系统架构进行修改时，可能需要进行性能调优。
- C. 性能调优计划可能因运行的系统类型不同而有所不同。
- D. 在开始调优工作之前，应为系统建立性能基准。
- E. 性能调优只需执行一次。

### 33. 查询哪个视图可以看到数据库缓冲区收集的建议结果？

- A. V$DB_CACHE_ADVICE
- B. V$SYSSTAT
- C. V$SGASTAT
- D. V$SGA

### 34. 下列哪项不属于 Oracle 的重做机制？

- A. 日志写入器（Log Writer）
- B. 数据库写入器（Database Writer）
- C. 检查点（Checkpoints）
- D. 归档重做日志（Archive Redo Logs）

### 35. 为了改进现有应用程序的性能，DBA 正在考虑向数据库服务器添加额外的 CPU。哪种类型的应用程序 SQL 最能从多个 CPU 的存在中受益？

- A. DML 语句
- B. 并行语句
- C. DDL 语句
- D. 任何 PL/SQL 包和过程

### 36. 用于定义某些类型分区表的最大值（high value）的特殊关键字是什么？

- A. UPPER
- B. MAXVALUE
- C. MAXIMUM
- D. UBOUND

### 37. 在以下哪种情况下最可能使用 Java 池（Java Pool）？

- A. 当使用利用 JavaScript 的应用程序时
- B. 当使用 Java Applet 时
- C. 当访问使用 Java 存储过程的应用程序时
- D. 当使用 JDBC 连接时

### 38. Oracle 的默认锁定机制在行级别。这种级别的锁定有助于保证什么的高度程度？

- A. 数据一致性
- B. 数据并发性
- C. 数据准确性
- D. 数据可扩展性

### 39. 本地管理表空间和字典管理表空间在什么方面有所不同？

- A. 本地管理表空间使用系统表来跟踪已分配和未分配的空间，而字典管理表空间不使用。
- B. 本地管理表空间不能用于存储应用程序表和索引，而字典管理表空间可以。
- C. 本地管理表空间使用其数据文件中的位图来跟踪已分配和未分配的空间，而字典管理表空间不使用。
- D. 本地管理表空间只能利用数据库的主要块大小，而字典管理表空间可以使用不同的块大小。

### 40. 缓存在共享池中的编译后的 SQL 代码版本的另一个名称是什么？

- A. 动态链接库
- B. P-Code
- C. script
- D. S-Code

### 41. 哪种优化方法考虑许多不同的执行计划，然后选择相对执行成本最低的那个？

- A. 基于规则的优化
- B. 基于值的优化
- C. 基于成本的优化
- D. 基于性能的优化

### 42. Oracle 建议你在设置 Oracle 服务器时使用符合 OFA 的架构。OFA 代表什么？

- A. Oracle Flexible Architecture
- B. Oracle FailSafe Architecture
- C. 最优灵活架构（Optimal Flexible Architecture）
- D. 最优故障安全架构（Optimal FailSafe Architecture）

### 43. DBA 想要将数据库缓冲区缓存的大小增加 100MB。目前，SGA 的总体大小为 256MB，SGA_MAX_SIZE 已设置为 300MB，机器上可供 Oracle 使用的总系统内存为 300MB。DBA 应该怎么做？

- A. 发出 ALTER SYSTEM 命令来动态修改 SGA_MAX_SIZE 和 DB_CACHE_SIZE。
- B. 发出 ALTER DATABASE 命令来动态修改 SGA_MAX_SIZE 和 DB_CACHE_SIZE。
- C. 关闭数据库，修改 SGA_MAX_SIZE 和 DB_CACHE_SIZE 参数，然后重启实例。
- D. DBA 无法将数据库缓冲区缓存的大小增加 100MB。

### 44. 下列哪项不会是一个可能需要进一步调优的 SQL 语句的特征？

- A. 消耗过多 CPU 资源的语句
- B. 解析、获取或执行时间很长的语句
- C. 从 SGA 读取数据块过多而从磁盘读取过少的语句
- D. 访问许多数据块但只返回几行数据的语句

### 45. 你正在设置一个新数据库。你已设置用于排序的临时文件（tempfiles），并且希望确保在数据库中创建的用户不会使用系统表空间作为其默认临时表空间。你可以发出什么命令来防止这种情况？

