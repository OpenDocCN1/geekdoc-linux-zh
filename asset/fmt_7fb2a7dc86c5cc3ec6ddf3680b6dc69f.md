
| 统计项 | 总计 | 每事务 | 每次登录 | 每秒 |
|---|---|---|---|---|
| <snip> |  |  |  |  |
| 队列超时 | 5 | .05 | .63 | .02 |
| 队列等待 | 9 | .08 | 1.13 | .04 |
| 执行计数 | 80502 | 745.39 | 10062.75 | 387.05 |
| 空闲缓冲区检查次数 | 10 | .25 | 1.45 | .13 |
| 空闲缓冲区请求次数 | 17415 | 161.25 | 2176.88 | 83.73 |
| 即时 (CR) 块清除 | 427 | 3.95 | 52.38 | 2.05 |

## 图 5.8 显示缓冲区忙等待统计信息的 REPORT.TXT 输出

```sql
SQL> Rem System wide events for non-background processes (EMON,
SQL> Rem EMON, etc). Times are in hundredths of seconds. Each one of
SQL> Rem these is a context switch which costs CPU time. By looking at
SQL> Rem the Total Time you can often determine what is the bottleneck
SQL> Rem that processes are waiting for. This shows the total time spent
SQL> Rem waiting for a specific event and the average time per wait on
SQL> Rem that event.
SQL> select nl.event "Event Name",
2         nl.event_count "Count",
3         nl.time_waited "Total time",
4         round(nl.time_waited/nl.event_count, 2) "Avg Time"
5         from stats$event nl
6         where nl.event_count > 0
7         order by nl.time_waited desc;
```

| 事件名称 | 计数 | 总时间 | 平均时间 |
|---|---|---|---|
| SQL*Net 客户端消息 | 40057 | 35572 | .89 |
| 队列 | 21 | 4724 | 224.95 |
| 库缓存加载锁 | 18 | 3487 | 193.72 |
| 日志文件切换完成 | 39 | 2672 | 68.51 |
| 数据文件顺序读 | 290 | 2024 | 6.98 |
| 数据库名称 IPC 响应 | 29 | 1476 | 50.90 |
| 日志文件同步 | 98 | 1101 | 11.23 |
| 数据文件随机读 | 450 | 1059 | 2.35 |
| 日志缓冲区空间 | 162 | 1011 | 6.24 |
| 切换日志文件命令 | 5 | 651 | 130.20 |
| 缓冲区忙等待 | 170 | 246 | 1.45 |
| 控制文件顺序读 | 56 | 244 | 4.36 |
| 闩锁释放 | 119 | 195 | 1.64 |

## 使用 OEM 监控缓冲区高速缓存性能

OEM 控制台的 Performance Manager（性能管理器）组件也可用于监控缓冲区高速缓存（Buffer Cache）性能。图 5.9 展示了与缓冲区高速缓存相关的性能管理器输出示例。

图 5.9 中的输出显示，在 OEM 监控期间，缓冲区高速缓存的命中率（hit ratio）为 97.38%。

**图 5.9** OEM 性能管理器缓冲区高速缓存监控

![](img/832fbc6aca8b6075843ca6f2356c0a8d_297_0.png)

## 提升缓冲区高速缓存性能

现在您已经了解了数据库缓冲区高速缓存管理机制的工作原理以及如何监控其性能，接下来可以查看提升性能的方法。这些方法的目标是通过提高命中率来提升数据库缓冲区高速缓存的性能。这些技术分为五类：

- 增大其尺寸。
- 使用多个缓冲区池（Buffer Pools）。
- 将表缓存在内存中。
- 绕过缓冲区高速缓存。
- 恰当地使用索引。

### 增大尺寸

提升数据库缓冲区高速缓存性能最简单的方法是增加其尺寸。数据库缓冲区高速缓存越大，缓存的缓冲区被 LRU 列表（最近最少使用列表）移出缓存的可能性就越小。缓冲区存储在数据库缓冲区高速缓存中的时间越长，命中率就会越高。增加缓冲区高速缓存的尺寸还会降低由 `free buffer inspected`（空闲缓冲区检查）、`buffer busy waits`（缓冲区繁忙等待）和 `free buffer waits`（空闲缓冲区等待）系统统计报告中的等待次数。

在 Oracle9i 中，数据库缓冲区高速缓存的尺寸由多个 `init.ora` 参数决定。这些参数的描述如表 5.4 所示。

**表 5.4** 影响缓冲区高速缓存尺寸的 `init.ora` 参数

| 参数名称 | 描述 |
| :--- | :--- |
| `DB_BLOCK_SIZE` | 定义数据库的主要块大小。Oracle9i 支持多种块大小，允许特定表空间的块大小与此大小不同。 |
| `DB_CACHE_SIZE` | 确定主要块大小（由 `DB_BLOCK_SIZE` 确立）对应的默认缓冲区池（Default Buffer Pool）的尺寸。默认尺寸为 48M。 |
| `DB_KEEP_CACHE_SIZE` | 确定 Keep 缓冲区高速缓存（Keep Buffer Cache）的尺寸。默认尺寸为 0KB。它也使用主要块大小作为其缓冲区大小。Keep 缓存将在下一节“使用多个缓冲区池”中讨论。 |
| `DB_RECYCLE_CACHE_SIZE` | 确定 Recycle 缓冲区高速缓存（Recycle Buffer Cache）的尺寸。默认尺寸为 0KB。它也使用主要块大小作为其缓冲区大小。Recycle 缓存将在下一节“使用多个缓冲区池”中讨论。 |
| `DB_2K_CACHE_SIZE` | 如果 2KB 不是主要块大小，则指定具有 2KB 块大小的段（segments）的缓冲区高速缓存尺寸。 |
| `DB_4K_CACHE_SIZE` | 如果 4KB 不是主要块大小，则指定具有 4KB 块大小的段的缓冲区高速缓存尺寸。 |
| `DB_8K_CACHE_SIZE` | 如果 8KB 不是主要块大小，则指定具有 8KB 块大小的段的缓冲区高速缓存尺寸。 |
| `DB_16K_CACHE_SIZE` | 如果 16KB 不是主要块大小，则指定具有 16KB 块大小的段的缓冲区高速缓存尺寸。 |
| `DB_32K_CACHE_SIZE` | 如果 32KB 不是主要块大小，则指定具有 32KB 块大小的段的缓冲区高速缓存尺寸。 |

数据库主要块大小由 `DB_BLOCK_SIZE` 参数以字节为单位指定。该值在数据库创建时设置，只能通过重新创建数据库来更改。`DB_BLOCK_SIZE` 的默认值因平台而异。在大多数 Unix 系统中，它介于 2KB 和 8KB 之间。Windows 2000 系统的默认块大小为 2KB。无论默认值如何，大多数系统都可以使用 2KB、4KB、8KB、16KB 或 32KB 的块大小。并非所有表空间都需要具有相同的块大小。第 2 章“调优信息源”中讨论的粒度（granules）概念，允许 Oracle9i 数据库中的表空间具有不同的块大小。然而，SYSTEM 和 TEMP 两个表空间将始终使用 `init.ora` 参数中由 `DB_BLOCK_SIZE` 定义的主要块大小，任何未明确指定不同块大小创建的其他表空间也将如此。尽管数据库缓冲区高速缓存可以存储各种尺寸的缓冲区，但仍应根据此主要块大小进行调优。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_299_0.png)

> 不要使用 `DB_nK_CACHE_SIZE` 参数来定义主要块大小的缓冲区高速缓存尺寸。始终使用 `DB_CACHE_SIZE` 参数来设置主要块大小的缓冲区高速缓存尺寸。

为了提升性能，可以将缓冲区高速缓存划分为最多三个不同的区域，称为默认池（Default）、保留池（Keep）和回收池（Recycle）池，使用表 5.4 中所示的 `init.ora` 参数实现。这些参数中每一个的尺寸都可以通过在参数指定的数值后附加相应字符（K、M 或 G）来表示为千字节、兆字节或吉字节。默认情况下，只配置了 *默认池*，因为回收池和 *保留池* 都被分配为零字节。多个缓冲区池的使用将在后续章节“使用多个缓冲区池”中讨论。就性能而言，增加默认缓冲区池的尺寸通常能提高缓冲区高速缓存的命中率。默认池的尺寸可以通过动态调整或通过实例关闭和启动来调整。
