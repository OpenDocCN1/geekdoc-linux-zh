

由于裸设备不包含文件系统，因此在对这些设备发起读或写请求时，不会产生操作系统中介带来的额外开销。这使得针对该设备的 I/O 操作非常迅速，从而提升了数据库性能。然而，裸设备的日常管理通常比带有文件系统的设备更加困难。例如，在裸设备上无法使用 Unix 中用于列出设备内容（ls）或从一个设备复制文件到另一个设备（cp）的命令。历史上，这意味着数据库管理员（DBA）往往不得不牺牲管理便利性以换取更高的性能。

随着缓存控制器、更快的磁盘驱动器以及改进的逻辑卷管理器的出现，现代系统中裸设备与普通设备（cooked devices，即基于文件系统的设备）之间的性能差距已大大缩小。如今，选择使用裸设备还是普通设备，在很大程度上取决于个人偏好，而非性能需求。

## 调整 DBW0 性能

**数据库**写进程（DBW0）负责将数据库缓冲区从数据库缓冲区高速缓存（Database Buffer Cache）写入到数据库数据文件（Datafiles）中。正如您在第 5 章“调整数据库缓冲区高速缓存”中所见，DBW0 在数据库检查点（checkpoints）以及用户服务器进程在数据库缓冲区高速缓存中搜索空闲缓冲区时执行此写操作。调整数据库写进程的 I/O 活动是调整数据库整体磁盘 I/O 性能的一个重要方面。

### 测量 DBW0 的 I/O

**V$SYSTEM_EVENT** 和 **V$SYSSTAT** 动态性能视图以及 STATSPACK 和 **REPORT.TXT** 的输出可用于确定 DBW0 在履行满足写请求的义务时是否遇到任何困难。

#### 使用 V$SYSTEM_EVENT 测量数据库写进程性能

**V$SYSTEM_EVENT** 中系统事件“缓冲区忙等待”（buffer busy waits）、“数据文件并行写”（db file parallel write）、“空闲缓冲区等待”（free buffer waits）和“写完成等待”（write complete waits）的发生情况都是与 DBW0 相关的 I/O 性能问题的潜在指标。名为**缓冲区忙等待**的事件表示在数据库缓冲区高速缓存中经历缓冲区等待。其中一些等待可能由 DBW0 对脏缓冲区写入效率低下引起。名为**数据文件并行写**的事件表示 DBW0 在并行写入多个块时可能正在经历等待。这些等待可能是由于数据文件所在的设备较慢，或者 DBW0 跟不上其被要求执行的写请求速度。频繁的**空闲缓冲区等待**事件表示用户服务器进程在遍历 LRU 列表寻找空闲缓冲区以将脏缓冲区移动到脏列表（Dirty List）时经历了等待。**写完成等待**事件表示用户会话正在等待 DBW0 将缓冲区从数据库缓冲区高速缓存中写出。

以下查询展示了如何确定您数据库中这些事件的数值：

```sql
SQL> SELECT event, total_waits, average_wait
2  FROM v$system_event
3  WHERE event IN ('buffer busy waits',
4                  'db file parallel write',
5                  'free buffer waits',
6                  'write complete waits');
```

| EVENT | TOTAL_WAITS | AVERAGE_WAIT |
| :--- | :--- | :--- |
| db file parallel write | 239 | .034454825 |

该查询表明，自实例启动以来，等待 DBW0 执行并行写的情况已发生 239 次。但是，由于 AVERAGE_WAIT 列的值是以 1/100 秒为单位的，因此在此特定情况下，这些等待尚未构成显著影响。请注意，**缓冲区忙等待**、**空闲缓冲区等待**和**写完成等待**统计数据的输出缺失，表示自实例启动以来这些事件尚未发生。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_428_0.png)

### 使用 V$SYSSTAT 测量数据库写进程性能

`V$SYSSTAT` 视图中统计信息 *redo log space requests*（重做日志空间请求）、*DBWR buffers scanned*（DBWR 扫描的缓冲区）和 *DBWR lru scans*（DBWR LRU 扫描）的出现情况对于测量 DBW0 的性能也很有用。统计信息 *redo log space requests* 表示在日志切换后，等待重做日志可用时发生了等待。由于数据库检查点发生在日志切换时，LGWR 开始写入下一个重做日志之前，DBW0 和 LGWR 必须分别完成其在数据库缓冲区高速缓存和重做日志缓冲区中的写操作。如果 DBW0 未能足够快地将数据库缓冲区高速缓存的内容写出，可能会导致 *redo log space requests*。以下关于 `V$SYSSTAT` 的查询展示了该统计信息的示例输出：

```sql
SQL> SELECT name, value
2  FROM v$sysstat
3  WHERE name = 'redo log space requests';
```

| NAME | VALUE |
| :--- | :--- |
| redo log space requests | 5 |

![](img/832fbc6aca8b6075843ca6f2356c0a8d_429_0.png)

`V$SYSSTAT` 中 *redo log space requests* 的高值或持续增加的值可能表明 DBW0 未高效执行其写操作。

`V$SYSSTAT` 中的 *DBWR buffers scanned* 和 *DBWR lru scans* 统计信息也可用作数据库写进程有效性的指标。统计信息 *DBWR buffers scanned* 表示为了找到要写入的脏缓冲区而在数据库缓冲区高速缓存中检查的缓冲区总数。由于 DBW0 执行此操作，当 DBW0 被通知进行写入时，如果它正忙于在 LRU 列表中查找脏缓冲区，则其写入操作可能效率低下。将 *DBWR buffers scanned* 除以 *DBWR lru scans* 的值，将得出每次 LRU 扫描平均检查的缓冲区数量。以下关于 `V$SYSSTAT` 的查询展示了此计算：

```sql
SQL> SELECT scanned.value/scans.value
2  'Avg. Num. Buffers Scanned'
3  FROM v$sysstat scanned, v$sysstat scans
4  WHERE scanned.name = 'DBWR buffers scanned'
5  AND scans.name = 'DBWR lru scans';
```

| Avg. Num. Buffers Scanned |
| :--- |
| 20.2711864 |

![](img/832fbc6aca8b6075843ca6f2356c0a8d_430_0.png)

> 使用此查询，平均扫描缓冲区数量的高值或持续增加的值可能表明 DBW0 未高效执行其写操作。

### 使用 STATSPACK 测量数据库写进程性能

在 V$SYSTEM_EVENT 和 V$SYSSTAT 中发现的大部分数据库写进程性能信息也包含在 STATSPACK 功能的输出中。图 8.8 展示了包含与数据库写进程相关的等待事件信息的 STATSPACK 示例输出。

图 8.8 中的输出显示，在两次 STATSPACK 快照获取时间之间，发生了 56 次缓冲区忙等待事件。正如上一节所述，如果缓冲区忙等待、数据文件并行写、空闲缓冲区等待或写完成等待系统事件的等待时间显著，则表明数据库写进程可能导致性能瓶颈。图 8.9 展示了显示与数据库写进程相关的系统统计信息的 STATSPACK 示例输出。

#### 图 8.8 显示数据库写进程事件的 STATSPACK 输出

前 5 大等待事件

| 事件 | 等待次数 | 等待时间 (秒) | 总百分比 | 用户中心时间 |
| :--- | :--- | :--- | :--- | :--- |
| 控制文件顺序读取 | 79 | 0 | 26.26 | |
| 异步磁盘 I/O | 199 | 0 | 25.27 | |
| 控制文件并行写 | 214 | 0 | 23.68 | |
| 缓冲区忙等待 | 56 | 0 | 20.84 | |
| 日志文件并行写 | 9 | 0 | 2.01 | |

图 8.9 中的输出表明，在两次 STATSPACK 快照获取时间之间，发生了 DBWR LRU 扫描和重做日志空间请求。正如上一节所述，非零的 redo log space requests、DBWR buffers scanned 和 DBWR lru scans 统计数值表明数据库写进程可能从调整中受益。

#### 图 8.9 显示数据库写进程统计信息的 STATSPACK 输出

数据库 PROD 实例 prod 快照 1 - 2 的实例活动统计

| 统计信息 | 总数 | 每秒 | 每事务 |
| :--- | :--- | :--- | :--- |
| CR 块创建 | 1 | 0.0 | 0.3 |
| DBWR 检查点缓冲区写入 | 6 | 0.0 | 2.0 |
| DBWR 检查点 | 0 | 0.0 | 0.0 |
| **DBWR LRU 扫描** | **917** | **1.4** | **305.7** |
| ... | | | |
| 直接物理写 | 147 | 0.2 | 49.0 |
| 非检查点物理写 | 147 | 0.2 | 49.0 |
| 预取块 | 0 | 0.0 | 0.0 |
| 递归调用 | ... | | |
| **重做日志空间请求** | **9** | **0.0** | **3.0** |
| 重做排序标记 | 0 | 0.0 | |
| 重做大小 | 364,364 | 553.7 | 121,454.7 |
| 重做同步写 | 3 | 0.0 | 1.0 |

### 使用 REPORT.TXT 测量数据库写进程性能

本节中提到的所有事件和统计信息也可以在输出文件 REPORT.TXT 中找到。图 8.10 和 8.11 展示了 REPORT.TXT 中包含 V$SYSTEM_EVENT 视图事件和 V$SYSSTAT 视图统计信息的部分。

#### 图 8.10 显示 V$SYSTEM_EVENT 事件的 REPORT.TXT 示例

```sql
SQL> Rem 系统级后台进程等待事件 (PMON, SMON 等)
SQL> select nv.event "Event Name",
2 n1.event_count "Count",
3 n1.time_waited "Total Time",
4 round(n1.time_waited/n1.event_count, 2) "Avg Time"
5 from v$sysstat nv
6 where n1.event_count > 0
7 order by n1.time_waited desc;
```

| 事件名称 | 计数 | 总时间 | 平均时间 |
| :--- | :--- | :--- | :--- |
| dbwr ipc 消息 | 1708 | 50976 | 29.85 |
| smon 定时器 | 2 | 30042 | 15021 |
| pmon 定时器 | 79 | 20950 | 265.19 |
| **缓冲区忙等待** | **876** | **5583** | **6.37** |
| 控制文件顺序读取 | 400 | 2595 | 6.74 |
| 控制文件并行写 | 238 | 1250 | 5.25 |
| 日志文件并行写 | 766 | 1231 | 1.61 |
| 异步磁盘 I/O | 77 | 336 | 4.36 |
| LGWR 等待重做副本 | 111 | 204 | 1.84 |
| 直接路径写 | 140 | 196 | 1.4 |
| 直接路径读 | 140 | 118 | .84 |
| 日志文件单写 | 76 | 107 | 1.41 |
| 数据文件并行写 | 38 | 106 | 2.79 |
| 队列 | 2 | 99 | 49.5 |
| 闩锁空闲 | 21 | 54 | 2.57 |
| 数据文件顺序读取 | 2 | 27 | 13.5 |

