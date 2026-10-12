
| NAME | GETS | MISSES | IMMEDIATE_RATIO |
| --- | --- | --- | --- |
| Active queue latch | 4365 | 0 | 0 |
| Checkpoint queue latch | 297731 | 191 | 0 |
| Direct I/O | 2 | 0 | 0 |
| JOX SGA latch | 15669 | 0 | 0 |
| NLS data objects | 9 | 0 | 0 |
| Token Manager | 12802 | 1 | 0 |
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

# 272

# 第 5 章 - 在 OLTP 系统上调优

| global tx free list | 28 | 0 | 0 | 0 | 0 |
| global tx hash mapping | 1148 | 0 | 0 | 0 | 0 |
| job_queue_processes parameter latch | 1389 | 0 | 0 | 0 | 0 |
| ktm global data | 303 | 0 | 0 | 0 | 0 |
| kwgit: protect wakeup time | 13378 | 0 | 0 | 0 | 0 |
| latch wait list | 3329 | 104 | 4 | 3240 | 26 |
| library cache | 6026323 | 55025 | 371 | 617493 | 411 |
| library cache load lock | 213136 | 8 | 5 | 0 | 0 |
| list of block allocation | 3714302 | 5 | 0 | 0 | 0 |
| loader state object freelist | 1350 | 0 | 0 | 0 | 0 |
| longterm free list | 623022 | 0 | 0 | 0 | 0 |
| message operations parent latch | 3 | 0 | 0 | 0 | 0 |
| messages | 4847631 | 7 | 4 | 0 | 0 |
| mostly latch-free SCN | 1 | 0 | 0 | 0 | 0 |
| multiblock read objects | 678482 | 13 | 0 | 4 | 0 |
| ncodef allocation latch | 13889 | 20 | 19 | 41383 | 2 |
| process allocation | 41385 | 0 | 0 | 0 | 0 |
| process group creation | 82361 | 52 | 12 | 3 | 0 |
| redo allocation | 12772768 | 8 | 0 | 1004037 | 193083 |
| redo copy | 280 | 0 | 0 | 0 | 0 |
| redo writing | 4795087 | 20859 | 4 | 0 | 0 |
| row cache objects | 30356649 | 26629 | 3518 | 14077 | 58 |
| sequence cache | 239836 | 6 | 0 | 0 | 0 |
| session allocation | 17078666 | 19113 | 6821 | 0 | 0 |
| session idle bit | 5097411 | 16 | 3 | 998 | 0 |
| session switching | 2793 | 0 | 0 | 0 | 0 |
| session timer | 43159 | 0 | 0 | 0 | 0 |
| shared java pool | 3995 | 0 | 0 | 0 | 0 |
| shared pool | 13913277 | 26901 | 1378 | 0 | 0 |
| extent pool | 1192 | 0 | 0 | 0 | 0 |
| temporary table state object allocation | 25 | 0 | 0 | 0 | 0 |
| transaction allocation | 512791 | 151 | 0 | 0 | 0 |
| transaction branch allocation | 1405 | 0 | 0 | 0 | 0 |
| undo global data | 6152661 | 659 | 0 | 0 | 0 |
| user lock | 166364 | 1973 | 502 | 0 | 0 |
| virtual circuit queues | 8288 | 0 | 0 | 0 | 0 |

## 5.6 监控 销锁（Latching）

### 5.6.1 识别闩锁竞争的来源

闩锁竞争（Latch contention）是一种症状，而不是某种直接的问题。换句话说，没有任何魔术棒可以挥一挥就消除闩锁竞争，调整 `init.ora` 参数也不会消除闩锁竞争。闩锁竞争通常源于性能问题，例如 SQL 重用、频繁执行 DDL 语句以及低效的 SQL。为了识别闩锁竞争的源头，你需要查询 `V$SESSION_WAIT` 事件的 `P1`、`P2` 和 `P3` 参数，以确定会话正在等待的闩锁号。例如，如果会话正在等待一个库缓存闩锁（library cache latch），你可以通过引用 `V$LATCH_CHILDREN` 视图来确定 `library cache` 指的是哪个子闩锁，该视图维护了子闩锁的统计信息。`V$LATCH_PARENT` 视图提供了统计信息。

在某些情况下，Oracle 需要获取父级闩锁（parent latch），这在实际上是特定闩锁的子闩锁（child latches）。例如，在某些库缓存事件期间，Oracle 需要在执行游标期间获取所有的库缓存子闩锁（即父级闩锁）。

### 5.6.2 最小化闩锁竞争的影响

## 5.7 调优回滚段（Rollback Segments）

回滚段存储更改前的数据镜像（pre-image）。回滚段包含更改前的数据。在事务回滚、执行回滚语句或异常终止时，它用于恢复数据。回滚段还用于创建自数据数据以来产生的读一致性视图。事务（非只读事务）由 Oracle 从 `init.ora` 参数 `rollback_segments` 指定的回滚段池中分配。两个 `init.ora` 参数 `transactions_per_rollback_segment` 和 `max_rollback_segments` 规定了

## 5.7 调整回滚段（Rollback Segments）

在实例启动时，在 SGA 回滚缓存中上线的回滚段数量。这两个参数并不限制事务可以使用的回滚段数量。除了用户私有和公共回滚段外，Oracle 始终维护 SYSTEM 回滚段。实例启动时将上线的回滚段最小数量由以下值定义：
```
