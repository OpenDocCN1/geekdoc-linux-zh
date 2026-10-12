
| EVENT | TOTAL_WAITS | TIME_WAITED |
| --- | --- | --- |
| log file parallel write | 1345421 | 170490 |
| db file sequential read | 705663 | 373413 |
| db file scattered read | 283361 | 103910 |
| log file sequential read | 88430 | 53616 |
| log file sync | 49327 | 15485 |
| control file parallel write | 27688 | 4440 |
| db file parallel write | 15170 | 8 |
| file open | 10533 | 996 |
| control file sequential read | 2718 | 589 |
| db file single write | 1980 | 352 |
| refresh controlfile command | 229 | 81 |
| file identify | 214 | 10 |
| log file single write | 61 | 25 |
| log file switch completion | 42 | 601 |
| db file parallel read | 23 | 94 |
| control file single write | 8 | 216 |
| switch logfile command | 1 | 9 |

上述查询显示，文件 I/O 事件 `log file parallel write`、`db file sequential read` 和 `db file scattered read` 占据了进程事件等待的大部分。从典型的 I/O 速率来看，平均等待时间是合理的。`db file sequential read` 事件指的是前景进程正在等待从数据库进行顺序读取。`db file scattered read` 事件指的是数据库发出多块 I/O 请求的全表扫描。`log file parallel write` 事件指的是在设置 `init.ora` 参数 `timed_statistics=TRUE` 的情况下，将重做条目写入重做日志缓冲区；此时 `v$system_event` 视图中的 `TIME_WAIT` 列可以帮助判断 I/O 是否耗时过长。你应该检查磁盘利用率统计，以确定重做日志文件是否饱和以及是否存在竞争。如果你确定存在重做日志竞争，可能需要将重做日志迁移到专用磁盘上，或重新配置重做日志以增加分带程度。`log file sync` 事件指的是用户会话 `LGWR` 重做条目的时间。当用户会话提交事务时，会话的重做信息会被刷新到重做日志。用户进程将重做缓冲区条目写入重做日志，`LGWR` 会在完成后通知会话。查询系统事件可以帮助你识别资源竞争。你可以通过如下查询 `v$session_wait` 视图来进一步识别 I/O 事件的确切文件。

```sql
SQL> select event,
p1,
p2,
p3,
state
from v$session_wait;
```

`v$system_event` 或 `v$session_event` 中列出的每个事件都可以与给定会话的 `v$session_wait` 等待 ID（wait id）以及等待事件参数关联。因此，你可以在会话和等待进行期间使用 `v$session_wait` 视图来深入分析等待事件。`v$session_wait` 视图提供了事件列 `p1`、`p2` 和 `p3`，帮助你分析等待事件背后的原因。例如，对于 `db file sequential read` 事件，参数 `p1`、`p2` 和 `p3` 分别引用被读取文件的文件号、块数以及正在读取的块数。你可以将文件号与 `v$datafile` 视图关联，以确定正在从哪个 Oracle 文件读取。

使用 `v$system_event` 和 `v$session_wait` 视图提供的信息可以帮助你确定 `DBWR` 或 `LGWR` 是否正在等待 I/O 事件。如果会话花费了太多时间等待 I/O 事件，这表明存在 I/O 瓶颈。你还需要将等待统计数据与磁盘利用率统计（例如 `sar -d`）相关起来，以确定 I/O 是否分布在多个磁盘和多个控制器上。你应该努力消除 I/O 等待，确保 Oracle 数据文件和重做日志文件的配置和大小是最。识别并解决 I/O 竞争和瓶颈是确保 `DBWR` 和 `LGWR` 跟上工作负载的关键。`DBWR` 跟不上工作负载的主要迹象是 `buffer waits` 和 `write complete waits` 事件。如果你在这些事件上观察到大量的等待，说明 `DBWR` 跟不上负载。这可能是 I/O 竞争，或者是 writer（写入器）数量不足。通过检查 I/O 事件的等待时间以及 `V$FILESTAT` 和操作系统级别的统计数据（如 `iostat`），你可以判断原因是否为 I/O 竞争，你可能需要配置额外的 writer 来跟上负载。

## 5.6 监控锁（LATCH）

有两种锁请求：`wait` 和 `nowait`。`v$latch` 提供了锁的 `gets`、`misses` 和 `sleeps` 等统计信息。`GETS (wait)` 列报告进程尝试获取锁但必须等待的次数。`MISSES (wait)` 列报告进程获取锁失败的次数。`SLEEPS (wait)` 列报告进程在等待时进入睡眠的次数。`GETS (no wait)` 列报告进程在无需等待的情况下获取锁的次数。如果出现 `lock free` 事件，你可以通过查看 `v$system_event` 视图中 `lock free` 事件的等待时间来确定严重程度。`v$latch` 和 `v$event` 帮助你识别竞争。高 sleep 率表示锁竞争。你可以使用以下查询识别产生竞争的锁：

```sql
select name,
round(misses/(gets+.001))*100), 'MISS_RATIO',
round(sleeps/(gets+.001))*100), 'SLEEP_RATIO'
from v$latch
where (gets>0) AND ((misses/(gets+.001))*100) > 2) OR ((sleeps/(gets+.001))*100) > 2)
order by 2;
```

## 5.6 监控锁（Latching）

| NAME | GETS | MISSES | IMMEDIATE_RATIO |
| --- | --- | --- | --- |
| handle pool latch | 41405 | 0 | 0 |
| redo copy | 91328 | 0 | 0 |
| operations parent latch | 82914 | 8 | 1 |
| row cache | 47385 | 0 | 0 |
| redo allocation | 5967590 | 312 | 0 |
| redo writing | 47385 | 0 | 0 |
| session allocation | 12802 | 1 | 0 |
| user lock | 41385 | 0 | 0 |
| address | 3 | 0 | 0 |
| archive control | 58 | 0 | 0 |
| archive process latch | 61 | 0 | 0 |
| begin backup scan | 28 | 0 | 0 |
| cache buffers header | 840436 | 8 | 0 |
| cache buffers chains | 858018461+137152 | 2022 | 286070 |
| cache lru chain | 4613812 | 253 | 0 | 199195 |
| channel handle pool latch | 41405 | 0 | 0 |
| channel operations parent latch | 82914 | 8 | 1 |
| cost function | 1 | 0 | 0 |
| dml lock allocation | 5967590 | 312 | 0 |
| dropped object history latch | 519 | 0 | 0 |
| enqueue chains | 10638145 | 262 | 1 |
| enqueues | 11789123 | 2139 | 5 |
| event group latch | 41385 | 0 | 0 |
| file name translation table | 66 | 0 | 0 |
| global transaction | 91328 | 0 | 0 |

以下查询可以列出锁：

```sql
SQL> select name,
      gets,
      misses,
      sleeps,
      immediate_gets,
```
