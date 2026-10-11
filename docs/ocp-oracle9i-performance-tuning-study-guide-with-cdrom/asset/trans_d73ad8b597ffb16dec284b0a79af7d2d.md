
# 目标：Oracle

## 描述检查点的工作机制

数据库检查点事件代表数据库处于一致状态的某个时刻。检查点非常重要，因为在实例故障之后，实例恢复期间只需要恢复自上次检查点以来发生的那些事务。检查点分为两种类型：*增量和完整*。当发生增量检查点时，会执行以下操作：

-   CKPT 后台进程立即更新控制文件头。
-   CKPT 后台进程在新的重做日志切换时，再次更新控制文件头和数据文件头。

当发生完整检查点事件时，数据库中会发生以下操作：

-   DBW0 后台进程将所有包含已提交事务的数据库缓冲池（Database Buffer Cache）中的缓冲区写入磁盘。
-   LGWR 后台进程将重做日志缓冲区（Redo Log Buffer）中的所有内容写入联机重做日志（Online Redo Log）。
-   CKPT 后台进程更新数据库控制文件和数据文件头，以指示检查点事件已经发生。

数据库在以下情况下会发生检查点：

-   使用除 ABORT 以外的任何方法关闭实例时。
-   当联机重做日志从当前日志切换到序列中的下一个重做日志时。
-   当 DBA 发出 ALTER SYSTEM CHECKPOINT 命令时。
-   当使用 ALTER TABLESPACE ... BEGIN BACKUP 命令将表空间置入热备份模式，或当表空间被置为离线时。此检查点是完整检查点的一种特殊形式，称为完整表空间检查点。在此类检查点期间，只有属于处于热备份模式的表空间的脏缓冲区会被写入磁盘。
-   当 init.ora 参数 FAST_START_MTTR_TARGET 指定的值被超过时。

监控检查点活动很重要，因为过多的检查点会导致不必要的 I/O，而过少的检查点会使数据库面临漫长的实例恢复时间。下一节描述测量数据库检查点性能的技术。

## 测量检查点性能

要在与检查点事件相关的 I/O 开销及其实例恢复收益之间取得适当平衡，需要利用 V$SYSTEM_EVENT 和 V$SYSSTAT 动态性能视图的内容、STATSPACK、REPORT.TXT、告警日志以及 OEM 性能管理器来监控检查点活动。

### 使用 V$SYSTEM_EVENT 测量检查点性能

偶尔，检查点事件会启动，但由于第二个检查点请求紧随第一个请求之后发生，导致未能成功完成。您可以通过查询 V$SYSTEM_EVENT 中的统计项 *log file switch (checkpoint incomplete)* 来检测已启动但未完成的检查点。该动态性能视图报告自实例启动以来各种事件发生的等待次数。表 7.2 描述了在此查询中使用的 V$SYSTEM_EVENT 列的内容。

**表 7.2 V$SYSTEM_EVENT 中选定列的描述**

| 列名 | 描述 |
| :--- | :--- |
| EVENT | 与等待相关联的事件名称 |
| TOTAL_WAITS | 此事件发生等待的总次数 |
| AVERAGE_WAIT | 等待此事件的平均时间，以百分之一秒为单位 |

图 7.5 展示了一个针对 V$SYSTEM_EVENT 的示例查询，显示了数据库中发生的与检查点活动相关的等待。

### 图 7.5 V$SYSTEM_EVENT 中显示的检查点活动

```sql
SQL> SELECT event, total_waits, average_wait
   2  FROM V$SYSTEM_EVENT
   3  WHERE event LIKE '%check%'
   4  or event LIKE '%log file switch%';

EVENT                          TOTAL_WAITS AVERAGE_WAIT
checkpoint completed              1         10
log file switch (checkpoint incomplete) 54         38
```

V$SYSTEM_EVENT 视图中发现的两个事件是检查点性能的指示器：*checkpoint completed* 和 *log file switch (checkpoint incomplete)*。

**Checkpoint Completed**
此事件显示了为检查点完成其活动而发生等待的频率。该事件的高值或持续增加的值表明需要对检查点进行调优。图 7.5 中的输出显示，一个 **Checkpoint Complete** 事件必须等待 10 个百分之一秒才能完成。

**Log File Switch (Checkpoint Incomplete)**
此事件显示了在上一个日志切换的检查点有机会完成之前，联机重做日志从当前日志切换到下一个日志的频率。当这种情况发生时，正在进行的检查点会被放弃，并开始一个新的检查点。由于不完整的检查点会导致无法提供恢复收益的额外 I/O，因此该事件的频繁发生表明应该对检查点活动进行调优。图 7.5 中的输出显示，导致不完整检查点的日志切换发生了 54 次，平均等待时间为 38 个百分之一秒。

另一个检查点性能的指示器可以在 V$SYSSTAT 动态性能视图中找到。两个统计项，**background checkpoints started** 和 **background checkpoints completed**，可用于确定所有已启动的检查点是否实际完成了。这两个统计项之间的差异表明检查点已启动但未完成。与 **log file switch (checkpoint incomplete)** 事件一样，这种情况在检查点发生得太频繁时就会出现。图 7.6 展示了使用 V$SYSSTAT 动态性能视图呈现此问题的示例。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_380_0.png)

图 7.6 中的输出显示启动了 36 个检查点，且 36 个检查点成功完成。只要这两个值的差值大于 1，就应考虑进行检查点调优。

> 注意
>
> 如果在检查点正在进行时执行查询，后台检查点启动的数量和后台检查点完成的数量偶尔会相差一个检查点。这不一定表示存在检查点性能问题。

### 使用 STATSPACK 和 REPORT.TXT 测量检查点性能

图 7.6 中的查询所显示的检查点活动也包含在 STATSPACK 选项和 REPORT.TXT 文件的输出中。图 7.7 展示了 STATSPACK 报告中该部分的示例。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_380_1.png)

图 7.8 展示了包含检查点信息的 REPORT.TXT 文件的示例输出。

### 图 7.8 REPORT.TXT 输出中显示的检查点活动

```sql
SQL> select nl.name 'Statistic',
2 nl.change 'Total',
3 round(nl.change/trans.change,2) 'Per Transaction',
4 round(nl.change/((start_users + end_users)/2),2) 'Per Logon',
5 round(nl.change/to_char(end_time, '0')*60*60*24 -
6 to_number(to_char(end_time, 'SSSSS'))) -
7 to_number(to_char(end_time, 'SSSSS'))) -
8 to_number(to_char(start_time, 'SSSSS')))
9 , 2) 'Per Second'
10 from v$sysstat nl,
11 v$sysstat tr,
12 v$sysstat sdate
13 where trans.name='user commits'
14 and nl.change != 0
15 order by nl.name;
```

| 统计项 | 总计 | 每事务 | 每登录 | 每秒 |
| :--- | :--- | :--- | :--- | :--- |
| CPU used by this session | 5070 | 54.43 | 794.75 | 20.26 |
| CPU used when call started | 5070 | 54.43 | 794.75 | 20.26 |
| CR blocks created | 790 | 7.31 | 90.75 | 3.0 |
| DBWR checkpoint buffer writ | 19716 | 182.65 | 2465.75 | 94.04 |
| DBWR checkpoints | 21 | .19 | 2.63 | .1 |
| DBWR revised bseg=write | 506 | 4.69 | 63.25 | 2.43 |
| DBWR txsn table writes | 308 | 3.59 | 40.5 | 1.87 |
| DBWR undo block writes | 4876 | 46.07 | 632 | 23.92 |
| SQL*Net roundtrips to/from | 40032 | 370.67 | 5004 | 192.46 |
| background checkpoints comp | 17 | .19 | 2.63 | .1 |
| background checkpoints star | 22 | .19 | 2.63 | .1 |
| background timeouts | 192 | 1.78 | 24 | .92 |
| branch node splits | 1 | .01 | .13 | 0 |
| buffer is not pinned count | 171752 | 1590.3 | 21469 | 825.73 |

这两个图中的输出都显示，虽然启动了 22 个检查点，但只有 17 个检查点运行至完成。这表明其中 4 或 5 个检查点未完成，因为它们被随后的检查点事件中断。这表明该实例应该对其检查点活动进行调优。

### 使用告警日志测量检查点性能

告警日志也包含有关检查点活动的重要信息。如果在告警日志中发现以下消息，则表明重做日志切换过快，未给予已启动的检查点足够的时间以正常完成：

```text
Thread 1 advanced to log sequence 293
Current log# 1 seq# 293 mem# 0: /u03/oradata/PROD/log1a.dbf
Current log# 1 seq# 293 mem# 1: /u04/oradata/PROD/log1b.dbf
Thread 1 cannot allocate new log, sequence 294
Checkpoint not complete
```

