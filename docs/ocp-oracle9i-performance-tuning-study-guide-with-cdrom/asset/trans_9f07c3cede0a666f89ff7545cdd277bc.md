

这些考试中的题目仅包含在光盘中。这将为你提供一个关于实际考试中可能出现内容的完整概览。

+ 请记住使用随本书附带光盘中的产品。电子闪卡（electronic flashcards）和 EdgeTest 考试准备软件是专门为帮助你备考和通过考试而设计的。电子闪卡可以在你的 Windows 计算机或 Palm 设备上使用。

要掌握本书涵盖的所有内容，你需要定期且有纪律地投入精力。试着每天留出相同的时间段来学习，并选择一个舒适、安静的地方进行。如果你努力，你会惊讶于自己学习这些材料的速度。祝你好运！

## 光盘里有什么？

我们努力提供了一些真正出色的工具，以帮助你完成认证过程。当你为考试做准备时，以下所有工具都应该安装在你的工作站上。

### 面向 Oracle 认证 DBA 的 EdgeTest 准备软件

由 EdgeTek Learning Systems 提供，这款考试准备软件帮助你通过 Oracle9i 数据库：性能调优考试。在此测试中，你可以找到书中的所有题目，以及仅出现在光盘中的两份额外练习题。你可以参加评估测试（Assessment Test），按章节自测，参加一份或两份练习题，或者从所有题目中随机生成一份考试。

### PC 和 Palm 设备的电子闪卡

在读完《OCP：Oracle9i 性能调优学习指南》之后，请阅读每章末尾的复习题，并学习光盘中包含的练习题。但等等，还有更多！用光盘中包含的闪卡进行自测。如果你能通过这些难题并理解答案，你就知道自己为考试做好了准备。

闪卡包含超过 150 个专门编写的问题，旨在考验你并确保你为考试做好了准备。结合复习题、练习题和闪卡，你应该能充分准备考试。

### OCP：Oracle9i 性能调优学习指南 PDF 版

Sybex 现在在光盘中提供这本 Oracle 认证书，以便你可以用 PC 或笔记本电脑阅读。它采用 Adobe Acrobat 格式。光盘中还包含 Acrobat Reader 5。这对于经常乘飞机或乘坐公交、火车通勤且不想携带书本的读者非常有帮助，同时也适用于那些觉得在电脑上看书更舒适的读者。

### 如何联系作者

你可以通过电子邮件 jjohnson@gr.com 联系 Joe Johnson。

## 评估测试

1. 某些类型的操作系统参数可以由 DBA 进行调整。这些参数叫什么？
   - A. 内核参数
   - B. 基础参数
   - C. 初始化参数
   - D. 基本参数

2. 闩锁（Latches）保护对哪些 Oracle 结构的访问？
   - A. 数据文件
   - B. 控制文件
   - C. 表
   - D. 内存结构

3. 当你使用 EXPLAIN PLAN FOR… 语法在 SQL*Plus 中为 SQL 语句生成执行计划（Explain Plan）时，以下哪项是正确的？
   - A. 查询本身不会执行。仅创建执行计划。
   - B. 除非开启了 AUTOTRACE，否则信息不会存储在 PLAN_TABLE 中。
   - C. TKPROF 工具在 EXPLAIN PLAN FOR 语句后自动运行，以生成格式化输出。
   - D. 查询被执行并且执行计划被创建。

4. DBA 希望确保某些用户不受限制地访问所有服务器资源。DBA 应该将这些用户放入哪个默认资源组？
   - A. OTHER_GROUPS
   - B. SYS_GROUP
   - C. LOW_GROUP
   - D. DEFAULT_CONSUMER_GROUP

5. DBA_TABLES 视图中的 EMPTY_BLOCKS 列衡量的是什么？
   - A. 表中的总空块数
   - B. 表中高于高水位线（High Water Mark）的总空块数
   - C. 表中低于高水位线（High Water Mark）的总空块数
   - D. 以上都不是

6. 在默认的 Oracle9i 配置中，客户端连接的默认方法是什么？
   - A. 专用服务器（Dedicated Server）
   - B. 共享服务器（Shared Server）
   - C. 客户端/服务器（Client/Server）
   - D. ODBC

7. DBA 和开发人员正在为大学构建学生记录系统。他们决定使用以下语法创建一个 STUDENT_HISTORY 表。这个表将如何分区？

```sql
SQL> CREATE TABLE student_history
 2  (student_id       NUMBER(10),
 3  degree           VARCHAR2(3),
 4  graduation_date DATE,
 5  final_gpa        NUMBER)
 6  PARTITION BY RANGE (graduation_date)
 7  SUBPARTITION BY HASH(student_id) SUBPARTITIONS 4
 8  STORE IN (hist_tab01, hist_tab02, hist_tab03, hist_tab04)
 9  (PARTITION p_1997 VALUES LESS THAN
10  (TO_DATE('01-JUN-1997', 'DD-MON-YYYY'))),
11  PARTITION p_1998 VALUES LESS THAN
12  (TO_DATE('01-JUN-1998', 'DD-MON-YYYY'))),
13  PARTITION p_1999 VALUES LESS THAN
14  (TO_DATE('01-JUN-1999', 'DD-MON-YYYY'))),
15  PARTITION p_2000 VALUES LESS THAN
16  (TO_DATE('01-JUN-2000','DD-MON-YYYY')) ,
17  PARTITION p_2001 VALUES LESS THAN
18  (TO_DATE('01-JUN-2001','DD-MON-YYYY')) ,
19  PARTITION p_ERROR VALUES LESS THAN (MAXVALUE));
```

   - A. 哈希（Hash）
   - B. 列表（List）
   - C. 范围（Range）
   - D. 复合（Composite）

8. 数据库的资源计划中，在实例级别同一时间最多可以有多少个处于活动状态？
   - A. 全部
   - B. 无
   - C. 一个
   - D. 最多四个

9. 你的数据库处于 ARCHIVELOG 模式，并发生了日志切换。正在切换到的在线重做日志尚未归档。会发生什么？
   - A. LGWR 将覆盖该日志。
   - B. 实例将崩溃。
   - C. 将自动创建额外的在线日志以满足日志切换请求。
   - D. LGWR 进程将等待 ARC0 完成在线重做日志文件的归档。

10. 以下哪个命令不会导致 DBW0 写入脏块（dirty blocks）？
    - A. ALTER TABLESPACE DATA BEGIN BACKUP
    - B. SHUTDOWN IMMEDIATE
    - C. SHUTDOWN ABORT
    - D. ALTER SYSTEM SWITCH LOGFILE

11. 以下哪项不是性能调优的两个基本原则之一？
    - A. 增加服务器的内存
    - B. 增加应用程序可用的磁盘数量
    - C. 减少用户数量
    - D. 增加 SGA 的大小

12. 初级 DBA 决定每天检查 Alert 日志，以确定数据库中是否存在性能问题。初级 DBA 可能会在 Alert 日志中找到以下哪些类型的信息（选择三项）？
    - A. 实例启动和关闭
    - B. 重做日志切换
    - C. 数据库用户创建
    - D. 表空间创建

13. 在 SGA 中，Oracle 保存最近执行的 SQL 的位置叫什么？
    - A. 大池（Large Pool）
    - B. 数据库缓冲区缓存（Database Buffer Cache）
    - C. 重做日志缓冲区（Redo Log Buffer）
    - D. 共享池（Shared Pool）

14. 以下哪个命令不会导致排序？
    - A. ORDER BY
    - B. ANALYZE TABLE
    - C. SELECT DISTINCT
    - D. INTERSECT
    - E. 以上所有都可能导致排序发生。

15. 当创建资源消费者组（resource consumer group）、资源计划（resource plan）或资源计划指令（resource plan directive）时，以下哪项是正确的？（选择所有适用项。）
    - A. 每个参数前必须加上 =>。
    - B. 每个参数必须用引号括起来。
    - C. 命令必须在一行中键入。
    - D. 以上所有都正确。

16. 当发生死锁情况时，为了解决死锁，哪个会话的语句将被回滚？
    - A. 导致死锁的会话
    - B. 检测到死锁的会话
    - C. 完成工作量最少的会话
    - D. 最后登录的会话

17. 一位 DBA 管理数据库有三个目标：可恢复性（recoverability）、可靠性（reliability）和可扩展性（scalability）。Oracle 的共享服务器（Shared Server）功能将解决这三个目标中的哪一个？
    - A. 性能
    - B. 可扩展性
    - C. 可靠性
    - D. 安全性

18. 你希望为若干你认为需要调优的 SQL 语句生成执行计划。你想保存计划信息以便日后评估。你应该做的第一件事是什么？
    - A. 运行 TKPROF。
    - B. 使用“Explain plan for...”语法运行 SQL 语句。
    - C. 在你的 SQL*Plus 会话中开启 AUTOTRACE。
    - D. 运行 utlxplan.sql。

19. 你使用以下语法创建一个表：
    CREATE TABLE EMP_HOLD AS SELECT * FROM EMP NOLOGGING;
    为了确保护 EMP_HOLD 表的可恢复性，执行此语句后应该做什么？

