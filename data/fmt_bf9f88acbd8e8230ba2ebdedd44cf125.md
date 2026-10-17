
- `dictionary lock`
- `enqueue`
- `Free List contention`
- `Immediate`
- `latch`
- `lock contention`
- `Willing-to-Wait`

## 复习题

1. 以下哪种闩锁类型允许用户在请求的闩锁未立即可用时继续执行其他处理？
   - A. `Immediate`
   - B. `Instant`
   - C. `Willing-to-Wait`
   - D. `Unwilling-to-Wait`

2. 以下哪种闩锁类型在尝试重新获取繁忙的闩锁之前会等待？
   - A. `Immediate`
   - B. `Instant`
   - C. `Willing-to-Wait`
   - D. `Unwilling-to-Wait`

3. 以下哪种机制用于保护对内存结构的访问？
   - A. `Enqueue`
   - B. `Lock`
   - C. `Latch`
   - D. `init.ora`

4. 用户服务器进程成功获取 `Willing-to-Wait` 闩锁而未等待的次数记录在 `V$LATCH` 中的哪个列？
   - A. `MISSES`
   - B. `GETS`
   - C. `SLEEPS`
   - D. `IMMEDIATE_GETS`

5. 用户服务器进程成功获取 `Immediate` 闩锁而未等待的次数记录在 `V$LATCH` 中的哪个列？
   - A. `MISSES`
   - B. `GETS`
   - C. `SLEEPS`
   - D. `IMMEDIATE_GETS`

6. 服务器进程在数据库缓冲池中查找空间以复制块时使用哪个闩锁？
   - A. `LRU` 闩锁
   - B. `Buffer Cache` 闩锁
   - C. `Cache Buffers LRU Chain` 闩锁
   - D. `Chain LRU` 闩锁

7. 以下哪个语句不会获取行锁？
   - A. `SELECT FOR UPDATE`
   - B. `INSERT`
   - C. `DELETE`
   - D. `DROP TABLE`

8. 数据库缓冲池 LRU 列表的理想命中率是多少？
   - A. 99 percent
   - B. 85 percent
   - C. 1 percent
   - D. 5 percent

9. 段块根据与表关联的什么值进入和离开 `Free List`？
   - A. `INITIAL/NEXT`
   - B. `PCTFREE/PCTUSED`
   - C. 表空间/数据文件
   - D. `MINEXTENTS/MAXEXTENTS`

10. 可以使用以下哪些动态性能视图检测自由列表争用？（选择所有适用的项。）
    - A. `V$SYSTEM_EVENT`
    - B. `V$SESSION`
    - C. `V$SESSION_WAIT`
    - D. `V$WAITSTAT`

11. 在多 CPU 服务器上，一个请求正在使用的闩锁的过程在释放 CPU 并再次尝试之前，会在 CPU 上做什么？
    - A. 睡眠
    - B. 转向其他处理
    - C. 自旋（Spin）
    - D. 超时

12. 哪个术语指的是确保用户在事务过程中始终看到数据库的一致视图的过程？
    - A. 数据并发性
    - B. 数据恒定性
    - C. 数据一致性
    - D. 数据争用

13. 默认情况下，大多数与 DML 相关的 Oracle 排他锁处于什么级别？
    - A. 表级别
    - B. 列级别
    - C. 块级别
    - D. 行级别

14. 当使用 `SELECT FOR UPDATE` 命令时，会在选定的行上获取什么类型的锁？
    - A. 表锁
    - B. 行排他锁
    - C. 表行共享锁
    - D. 排他锁

15. 以下哪种锁类型限制性最强？
    - A. 排他锁
    - B. 唯一锁
    - C. 排斥锁
    - D. 以上均无限制性

16. 在创建、删除或修改表时，会获取哪种锁类型？
    - A. 限制性锁
    - B. 排他锁
    - C. 显式锁
    - D. 共享锁

17. 查看以下代码段：

```sql
SQL> SELECT s.username
   2  FROM dba_blockers db, v$session s
   3  WHERE db.holding_session = s.sid;

USERNAME
------------
JOE
```

下列哪个陈述最能描述代码段中的信息？
    - A. Joe 是一个阻塞者。
    - B. Joe 是一个等待者。
    - C. Joe 无法获取锁。
    - D. 提供的信息不足以确定任何有意义的结果。

18. 如果你的应用程序有很多用户对表进行频繁插入，哪种类型的争用可能会成为问题？
    - A. 重做分配闩锁争用
    - B. 自由列表争用
    - C. 重做复制闩锁争用
    - D. 库缓存闩锁争用

19. 如果你想杀死用户 Jim 的会话，且 `V$SESSION` 显示其 `SID` 和 `SERIAL#` 分别为 20 和 2369，你应该发出什么命令来杀死该会话？
    - A. `ALTER SYSTEM KILL SESSION (20,2369);`
    - B. `ALTER SESSION KILL SYSTEM '20,2369';`
    - C. `ALTER SYSTEM KILL SESSION '20','2369';`
    - D. `ALTER SYSTEM KILL SESSION '20,2369';`

20. 当发生 Oracle 死锁时，解决后死锁信息记录在哪里？
    - A. 警报日志
    - B. `V$DEADLOCK`
    - C. 用户跟踪文件
    - D. `PMON` 跟踪文件

### 复习问题答案

1. A. 立即闩锁在等待闩锁可用时继续处理。愿意等待（`Willing-to-Wait`）闩锁会在尝试获取闩锁之间睡眠。

2. C. 愿意等待（`Willing-to-Wait`）闩锁在尝试获取之前请求过但处于忙碌状态的闩锁之前会睡眠。

3. C. 闩锁用于保护对内存结构（如 LRU 列表和重做日志缓冲区）的访问。

4. B. `V$LATCH` 的 `GETS` 列显示了愿意等待（`Willing-to-Wait`）闩锁在未等待情况下被获取的次数。

5. D. `V$LATCH` 的 `IMMEDIATE_GETS` 列显示了立即闩锁在未等待情况下被获取的频率。

6. C. 用户服务器进程在将块副本放入数据库缓冲区缓存时，会使用缓存缓冲区 LRU 链闩锁搜索 LRU 列表。

7. D. `DROP TABLE` 语句会导致在表上获取 DDL 锁，以确保在删除过程中没有会话可以访问该表。所有其他语句都会获取某种行级别的锁。

8. A. 数据库缓冲区缓存 LRU 列表的命中率至少应为 99%。

9. B. 当段块填满至 `PCTFREE` 时，它们会从自由列表中移除；当它们被清空至 `PCTUSED` 时，它们会被放回自由列表。

10. A, C, D. `V$SYSTEM_EVENT` 视图包含缓冲区忙等待事件的统计信息。`V$WAITSTAT` 包含有关自由列表块等待的统计信息。`V$SESSION_WAIT` 可以与 `DBA_SEGMENTS` 连接以确定哪些段正在经历自由列表争用。

11. C. 该过程会在 CPU 上自旋若干次，直到释放 CPU。自旋过程是一种内部等待机制。

12. C. Oracle 使用回滚段和 SCN 来确保用户始终看到数据库的读一致视图。

13. D. 虽然 Oracle 确实会在表级别获取共享锁，但对正在更改的数据的排他锁仅在行级别获取。

14. C. `SELECT FOR UPDATE` 命令获取表行共享锁，防止其他用户对选定行执行 DML。

15. A. 排他锁是限制性最强的类型，允许其他用户在锁释放之前仅执行 `SELECT` 语句。

16. B. 对表执行 DDL 要求在该表上获取排他锁。

17. A. 通过查询 `DBA_BLOCKERS` 与 `V$SESSION` 的连接，我们可以看出 Joe 已获取并持有某个对象的锁，而另一个会话正在请求该锁。Joe 是阻塞者，阻止了另一个会话获取该锁。

18. B. 自由列表争用可能成为问题，因为许多资源试图从段头获取信息，以确定哪些块可用于存储新插入的行。段头中的自由列表包含此信息。

19. D. 在使用 `ALTER SYSTEM` 命令杀死会话时，`SID` 和 `SERIAL#` 的值必须用单引号括起来，并用逗号分隔。

20. C. 检测到死锁且事务被回滚的用户将在 `init.ora` 中指定的 `USER_DUMP_DEST` 位置生成跟踪文件。

# 第 10 章

# 操作系统调优

**本章涵盖的 ORACLE9i 性能调优考试目标：**

- 描述不同的系统架构
- 描述操作系统调优的主要步骤
- 识别操作系统调优和数据库调优之间的相似性
- 理解虚拟内存和换页
- 解释进程和线程之间的区别
- 设置数据库资源管理器
- 将用户分配到资源管理器组
- 在组内创建资源计划
