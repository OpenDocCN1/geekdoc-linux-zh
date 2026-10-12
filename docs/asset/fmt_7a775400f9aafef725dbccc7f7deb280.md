
order by name

```
| NAME | GETS | MISSED | SLEEPS | IMGETS | IMMISSES |
|---|---|---|---|---|---|
| cache buffer handles | 29183890 | 53376 | 59 | 0 | 0 |
| cache buffers chains | 4733033651 | 11848270 | 8659 | 85379432 | 1113 |
| cache buffers lru chain | 3717959 | 4304 | 4 | 136999082 | 146533 |
| cache protection latch | | 0 | 0 | 0 | 0 |
```

缓冲区锁（buffer latches）用于在连续操作期间保护缓冲区缓存中的数据块。Oracle 7 引入了另一个可调优的 init.ora 参数 `db_lru_latches`，允许你调整 LRU 锁的数量。对于具有大型缓冲区缓存和高 OLTP 系统应用社区的多处理器系统，可能会出现 LRU 锁的竞争。

在上例中，与获取次数（gets）相比，缺失（misses）和等待（sleeps）次数极低。例如，`cache buffer chains` 锁以模式 4 被获取了 47 亿次，而发生了 1180 万次缺失，缺失率小于 1%。如果您遇到了缓冲区缓存 LRU 竞争，请将 `db_lru_latches` 设置为小于等于可用处理器数量，以减少 LRU 锁的竞争。如果缓冲区缓存 LRU 竞争持续存在，则是热点缓冲区（hot buffers）的症状。应用程序可能持续访问同一组缓冲区，导致锁竞争。在这种情况下，你可以使用 `V$SESSION_WAIT` 来识别那些等待此锁的会话，并针对该事件到该 LRU 锁对应的缓冲区集进行参数协调。

## 5.3.2 REDO LOG BUFFER LATCHES 重做日志缓冲区锁

日志缓冲区（redo buffer）是 SGA 中包含 redo 记录（entries）的区域。该缓冲区是一个同步缓冲区，由 `LGWR` 定期刷新。`LGWR` 进程将 redo 记录写入重做日志文件。在将 redo 记录写入日志缓冲区之前，必须为该记录在日志缓冲区分配空间。日志缓冲区中的空间分配由分配锁（allocation latch）控制。然后使用重做拷贝锁（redo copy latch）或分配锁将 redo 记录复制到日志缓冲区中。每个实例只有一个重做分配锁；因此，为了避免重做瓶颈，应将重做分配锁保持在最少。

## 5.3 锁（Latches）与 Locks

init.ora 参数 `log_small_entry_max_size`（单位为字节）定义了在不获取重做拷贝锁的情况下，使用重做锁复制到日志缓冲器的最大重做记录大小。如果重做记录大于 `log_small_entry_max_size`，则必须使用重做拷贝锁将数据复制到日志缓冲区，并获取重做拷贝锁。如果重做记录小于或等于 `log_small_entry_max_size`，则通过重做锁进行复制，并在之后立即释放分配锁。因此，通过减小 `log_small_entry_max_size`，更多的拷贝将通过重做拷贝锁而非分配锁完成。你还可以通过 `log_small_entry_max_size=0` 来提高性能，显著减少锁的持有时间。

init.ora 参数 `log_simultaneous_copies` 调节用于并发写入日志缓冲区的重做拷贝锁的数量。为了在多处理器系统中获得良好的性能，你可以将 `log_simultaneous_copies` 设置为小于 CPU 数量的2 倍。如果 `log_simultaneous_copies=0`，所有写入器被视为小型，并在不使用拷贝锁的情况下写入日志缓冲区。在单处理器系统上，不使用重做拷贝锁，因为默认情况下一个进程就可以活动地写入日志缓冲区。默认情况下，`log_simultaneous_copies` = 系统中的处理器数量。建议将该参数设置在从默认值到系统 CPU 数量两倍之间的任何范围内。调优这两个参数的性能收益取决于系统的 redo 数量和事务活动量。如果 `LGWR` 在形成日志时需要获取所有重做拷贝锁，那么配置过重做锁可能不是一个好主意，因为 `LGWR` 获取所有锁的成本将会增加。因此，你需要平衡锁的数量与 `LGWR` 获取所有重做锁的频率。

要确定重做日志缓冲区锁（如重做分配锁和重做拷贝锁）的命中率和缺失率，可以通过以下查询查询 `v$latch` 视图。

```sql
select name,
sum (gets) 'Gets',
sum (misses) 'Misses',
sum (immediate_gets) 'IM_Gets',
sum (immediate_misses) 'IM_Misses'
from v$latch
where name like '%redo%'
group by name;
```

| NAME | Gets | Misses | IM_Gets | IM_Misses |
| --- | --- | --- | --- | --- |
| redo allocation | 35632016 | 41445 | 0 | 0 |
| redo copy | 1481 | 1114 | 42372547 | 4001 |
| redo writing | 1487858 | 13 | 0 | 0 |

* Oracle8 中

在此例中，重做锁统计信息显示了一些等待和立即请求的缺失。重做锁用于协调 redo 日志的写入。然而，此例中相对于获取的缺失百分比极低。缺失通常在高并发期间发生；相对于获取的缺失百分比应该是低的。如果你的统计信息显示重做锁竞争（高缺失），你应该增加重做拷贝锁的数量（在多处理器系统上），并设置 `log_size=0` 以减少持有重做锁的时间。如果你在 Oracle7 中仍遇到竞争，请尝试在请求重做锁之前预建重做日志。

## 5.4 监控 redo 缓冲区

### 5.3.4 SHARED LATCHES 共享锁

Oracle8 通过采用共享锁（shared latches）提高了锁的利用率。共享锁允许多个进程使用底层同步机制并发访问内存区域。在 Oracle8 中，父级和子级 redo拷贝都是共享的。这增加了 redo 吞吐量，因为多个进程可以同时以共享模式获取 redo。共享锁可能在所有平台上不支持，例如不支持原子比较交换（atomic compare-swap）的平台。Sun4 架构支持共享锁。在未来的发布中，额外的锁将使用共享模型以提高并发性。

### 5.3.3 VECTOR POSTING 向量投放

Oracle8 第 8.0 版本提供了一种名为向量投放（vector posting）的性能增强。向量投放允许一组进程。没有向量投放的情况下，`LGWR` 需要单独投放每个进程。通过使用向量投放，`LGWR` 可以一次性投放所有进程。对于信号量（semaphores），启用向量投放可能需要增加信号量的大小。在 Oracle8 中，`log_simultaneous_copies` 参数已废弃。这决定了产生多少 redo。要启用向量投放，init.ora 参数 `use_vector_post=TRUE`。对于具有重度 OLTP 工作负载的系统，向量投放带来了 3%-5% 的收益。

## 5.5 监控 DBWR 和 LGWR

为了最大化 `DBWR` 和 `LGWR` 进程的性能，避免 `DBWR` 或 `LGWR` 导致用户进程出现长时间等待是非常重要的。此外，确保 `DBWR` 和 `LGWR` 都能跟上工作负载以避免递归等待情况也同样重要。导致 `DBWR` 或 `LGWR` 缓慢的主要原因之一是 I/O 竞争。如果数据文件和重做日志分布不当，`DBWR` 和 `LGWR` 可能会花费大部分时间等待 I/O 完成。这会导致前景进程等待检查点（checkpoints）和缓冲区刷新（buffer flushes）等事件。你可以通过查询 `v$system_event`, `v$session_event`, 和 `v$session_wait` 视图来确定进程是否正在等待 I/O。`v$system_event` 视图报告所有会话的事件等待总数。`v$session_event` 视图报告每个会话的事件等待总数。`v$session_wait` 视图报告会话刚刚完成等待或当前正在等待的事件。这些视图对于精确定位竞争非常有用。例如，以下查询列出了文件 I/O 事件的等待总数和等待时间。

```sql
SQL> select event,
total_waits,
time_waited
from v$system_event
where event like '%file%'
 by total_waits desc;
```
