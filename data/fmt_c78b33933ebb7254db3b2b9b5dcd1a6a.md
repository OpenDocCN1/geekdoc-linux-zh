
# FIGURE 8.9 output showing Database Writer

| Statistic | Total | Per Second |
| --- | --- | --- |
| CR created | 1 | 0.3 |
| DBWR written | 0 | 0.0 |
| DBWR checkpoints | 0 | 0.0 |
| lru scans | 917 | 1.4 |
| physical writes | 147 | 0.2 |
| physical checkpoint | 147 | 0.2 |
| prefetched blocks | 0 | 0.0 |
| redo space requests | 9 | 0.0 |
| redo ordering | 0 | 0.0 |
| redo size | 364,364 | 55.7 |
| redo sync | 121,454 | 1.7 |
| sync writes | 3 | 0.0 |

# 使用 REPORT.TXT 测量数据库写入

本节中提到的所有事件和统计数据也可以在 `REPORT.TXT` 中找到。图 8.10 和 8.1 显示显示包含 `V$SYSTEM_EVENT` 视图事件和 `V$SYSSTAT` 视图统计数据的 `REPORT.TXT` 部分。

# FIGURE 8.10 REPORT.TXT showing V$SYSTEM_EVENT events

```
SQL> system wait events for background processes (PMMON, SMON, etc)
SQL> select nl.event_name "Event Name",
      nl.event_count "Count",
      nl.time_waited "Total Time",
      round(nl.time_waited/nl.event_count, 2) "Avg Time"
from vstat_event nl
where nl.event_count > 0
order by nl.time_waited desc;
```

| Event Name | Count | Total | Avg Time |
| --- | --- | --- | --- |
| rdbms ipc message | 1708 | 50976 | 29.85 |
| smon timer | 79 | 30042 | 380.27 |
| pmon timer | 876 | 55593 | 63.37 |
| control file sequential read | 400 | 2695 | 6.74 |
| control file parallel write | 238 | 1230 | 5.25 |
| log file parallel write | 766 | 1231 | 1.61 |

# 图 8.11 显示 V$SYSSTAT 统计信息的示例 REPORT.TXT

```sql
SQL select nl.name "Statistic",
      nl.change "Value",
      round(nl.change/trans.change,2) "Per Transaction",
      round(nl.change/((start_users + end_users)/2)/2) "Per Logon",
      round(nl.change/((to_number(to_char(end_time,'U'))*60*60*24 + 
      to_number(to_char(start_time,'U'))*60*60*24 - 
      to_number(to_char(end_time,'S'))'))/86400),2) "Per Day"
  from
      stats$ nl,
      stats$ trans,
      statsdate
  where
      trans.name='user' commits
      and nl.change > 0
  order by nl.name;
```

| 静态 | 事务总计 | 每次登录 | 每秒 | 每天 |
| --- | --- | --- | --- | --- |
| DBWR 缓冲区写入 | 19726 | 162.65 | 2465.75 | 94.84 |
| DBWR 检查点 | 21 | .19 | 2.13 | 1 |
| DBWR 写入中 | 506 | 4.69 | 63.25 | 2.43 |
| DBWR 缓冲区扫描 | 388 | 3.59 | 45.8 | 1.87 |
| SQL*Metric 计数释放 | 40032 | 370.67 | 5004.25 | 192.46 |
| 后台检查点完成 | 19 | .17 | 2.43 | 1 |
| 后台检查点启动 | 21 | .19 | 2.63 | 1 |
| redo 空间请求 | 192 | 1.78 | 24 | .92 |

图中缓冲区等待等待（buffer wait event）事件的存在以及 DBWR 缓冲区扫描和 redo 日志统计非零值表明，调优可能会提高数据库写入器（Database Writer）的性能。

# 改进 DBW0 I/O

可以使用 `init.ora` 参数调优 `DBW0` 活动的性能：

- `DBWR_IO_SLAVES`
- `DBWR_WRITER_PROCESSES`

接下来的章节将描述这些参数，以及使用它们来改进数据库写入器 I/O 的技术。

| Oracle 目标 | 配置实例使用 I/O 从属进程 |

# DBWR_IO_SLAVES

此 `init.ora` 参数指定了在实例启动时启动的数据库写入器进程数。该参数的默认值为 0。

## 394 第 8 章 • 调优磁盘 I/O

该参数的最大值取决于操作系统。在用于名为 `PROD` 实例的 Unix 服务器上，`DBW0` 从属后台进程的命名规范如下所示：

- 第一个 `DBW0` I/O 从属进程：`ora_i101_PROD`
- 第二个 `DBW0` I/O 从属进程：`ora_i102_PROD`
- 第 n 个 `DBW0` I/O 从属进程：`ora_in_PROD`

![](img/c36db8fbb4893c630ad429a99bfd63e3_432_0.png)

I/O 从属进程名称的每个部分都有意义。对于名为 `ora_i103_PROD` 的进程，其中间部分的名称 `i103` 可以这样解释：第一个字符 `i` 表示该进程是从属（slave），第二个字符 `1` 表示该进程正在使用 1 号适配器（内存池），最后两个字符 `03` 表示这是使用该适配器的第三个从属进程。

数据库写入器从属进程与真实的 `DBW0` 本身相似，区别在于它们只能执行写入操作，而不能像 `DBW0` 那样从数据库缓冲区缓存的 LRU 列表中移动数据块。这些从属进程的目的是在仅支持同步 I/O 的系统上模拟异步 I/O。请参阅接下来的侧边栏以获取有关异步 I/O 的解释。

在配置 I/O 从属进程后，`DBW0` 将为 I/O 请求分配给每个从属进程。如果在发出 I/O 请求时所有可用从属进程都忙碌，`DBW0` 将生成额外的进程——其数量受 `init.ora` 中 `DBWR_IO_SLAVES` 参数值的限制。如果在请求时没有可用的 I/O 从属进程，则会导致等待。

![](img/c36db8fbb4893c630ad429a99bfd63e3_432_1.png)

任何数据库写入器生成 I/O 从属进程外，其他执行磁盘 I/O 的后台进程（例如：日志写入器、归档器和恢复管理器）也会创建 I/O 从属进程来支持它们的 I/O 活动。例如，将 `DBWR_IO_SLAVES` 设置为非零值还将产生四个日志写入器从属进程。

![](img/c36db8fbb4893c630ad429a99bfd63e3_432_2.png)

恢复管理器（Recovery Manager）工具磁带 I/O 活动的从属进程也可以通过在 `init.ora` 中设置 `BACKUP_TAPE_IO` 为非零值来生成。

通过在 `init.ora` 中设置 `BACKUP_TAPE_IO` 为非零值，也可以生成恢复管理器工具磁带 I/O 活动的从属进程。

# I/O 从属进程模拟异步 I/O 395

正如前面的侧边栏所述，设备可以配置为原始的（raw）或调式的（cooked）。原始设备通常更快，因为从 `DBWR` 的角度来看，对调式设备的写入需要等待操作系统的信号。以下图示说明了这一点。

| 请求发生 | 处理 | 请求发生 | 处理 | 请求发生 | 处理 |
| --- | --- | --- | --- | --- | --- |
| DBWR | 等待信号 | | 完成 | | 完成 |
| DBWR | 等待信号 | | 完成 | | 完成 |
| DBWR | 等待信号 | | 完成 | | 完成 |
