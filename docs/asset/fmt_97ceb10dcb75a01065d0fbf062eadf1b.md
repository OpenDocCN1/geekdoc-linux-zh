
关于并行 DML 配置程序的完整讨论超出了本文以及 Oracle 性能调优 OCP 考试的范围。然而，当你的服务器具有多个未充分利用 CPU、合适的 I/O 子系统以及支持并行执行的内存时，才应考虑并行执行。

# 适当使用索引

从应用程序 SQL 代码的角度来看，对数据库缓冲区缓存性能产生的另一个重大影响是确保通过适当使用索引来避免不必要的全表扫描。全表扫描越少，数据库缓存命中率就越高。鼓励使用索引的一种简单方法是在引用另一个表主键列（280 第 5 章）的表的外键列上建立索引。这不仅有助于提高多表连接的效率，还能最小化两个表之间密集使用缓冲区缓存的 FTS 排序合并连接。

## 总结

SGA 数据库缓冲区缓存的作用是缓存最频繁的段，以便应用程序用户在访问数据时能够尽可能地减少物理磁盘 I/O。数据库缓冲区缓存的大小由 `init.ora` 参数 `SGA_MAX_SIZE`、`DB_CACHE_SIZE`、`DB_KEEP_CACHE_SIZE` 和 `DB_RECYCLE_CACHE_SIZE` 指定。每个缓冲区缓存持有来自一个段的数据。缓冲区缓存的活动由 LRU 算法、脏列表（Dirty List）、用户服务器进程和数据库写入器（DBW0）管理。

数据库缓冲区缓存的性能通过命中率来衡量，比较实例执行的总读取次数与从磁盘执行的读取次数。对于调优良好的 OLTP 系统，预计命中率达到 90% 或更高。命中率可以通过查询 `V$SYSSTAT` 以及 `STATPACK` 和 `REPORT.TXT` 的输出来计算。缓冲区缓存性能的其他指标包括空闲缓冲区检查、缓冲区忙等待、空闲缓冲区等待统计以及使用 Oracle Enterprise Performance Manager 工具对缓冲区缓存性能进行图形表示。

提高数据库缓冲区缓存命中率的选项包括：增大缓冲区缓存、使用多个缓冲区池、在缓冲区缓存中缓存表、为 I/O 密集型操作绕过缓冲区缓存以及使用索引适当减少全表扫描。

## 考试要点

了解缓冲区缓存如何管理和利用。能够描述数据如何移入缓冲区缓冲区缓存以及管理位于其中的缓冲区缓存的 LRU 机制。

Copyright ©2002 SYBEX, Inc., Alameda, CA www.syex.com

# 关键术语 281

理解如何衡量缓冲区缓存性能。

了解如何使用动态性能视图、STATPACK 和 `REPORT.TXT` 的输出确定缓冲区缓存命中率。能够描述哪些辅助统计数据可以作为缓冲区缓存性能的指标。

理解如何创建和利用多个缓冲区池。能够动态和手动创建三种类型的缓冲区池。了解如何将段分配给各个缓冲区池并监控它们的性能。

描述表缓存的优势。了解如何在缓冲区缓存中缓存表，以及哪些类型的表是缓存的良好对象。

## 关键术语

在考试之前，请确保你熟悉以下内容：

| 关键术语 |

|-----------|

| 缓冲区缓存命中率 (Buffer Cache hit ratio) |

| 缓冲区池 (Buffer Pool) |

| 缓存 LRU 列表 (Cache LRU list) |

| 数据库缓存 (Database Cache) |

| 默认池 (Default Pool) |

| 脏列表 (Dirty List) |

| 留存池 (Keep Pool) |

| 回收池 (Recycle Pool) |

| 服务器进程 (Server Process) |

| 写入列表 (Write List) |

## 复习题

- 1. 缓冲区缓存使用了以下哪些机制？

  - A. LRU 列表
  - B. 脏列表
  - C. DBW0
  - D. 以上所有

- 2. 下列哪项不在缓冲区缓存中？

  - A. 表
  - B. 重做日志 (Redo logs)
  - C. 索引
  - D. 回滚段 (Rollback segments)

- 3. 下列哪个进程将段块从磁盘复制到缓冲区缓存中？

  - A. DBW0
  - B. LGWR
  - C. 服务器进程 (Server Process)
  - D. PMON

- 4. 除非发生全表扫描，用户的服务器进程将缓冲区放在 LRU 列表的哪一端？

  - A. MRU
  - B. LRU
  - C. 中间 (Middle)
  - D. 以上

- 5. 每每次访问缓冲区缓存上的缓冲区，它都会移动到 LRU 列表的哪个部分？

  - A. MRU
  - B. LRU
  - C. 中间 (Middle)
  - D. 以上

- 6. 缓冲区缓存中的副本与磁盘段不匹配的缓冲区称为什么？

  - A. 固定缓冲区 (Pinned buffer)
  - B. 空闲缓冲区 (Free buffer)
  - C. 脏缓冲区 (Dirty buffer)
  - D. 回滚缓冲区 (Rollback buffer)

- 7. 用户服务器进程在缓冲区缓存中定位空闲缓冲区时使用什么机制？

  - A. LRU 列表
  - B. 脏列表
  - C. DBW0
  - D. 全部

- 8. DBW0 何时写入脏缓冲区？

  - A. 脏列表达到阈值长度时
  - B. 用户服务器进程搜索 LRU 长时间未找到空闲缓冲区时
  - C. 检查点时
  - D. 以上

- 9. 选择衡量缓冲区缓存性能的主要指标：

  - A. 平均 LRU 列表长度
  - B. 最大脏列表缺失率
  - C. 数据库缓存命中率
  - D. 以上所有

- 10. 使用哪个动态性能视图计算缓冲区缓存命中率？

  - A. V$BUFFERCACHE
  - B. V$SYSTEMSTATS
  - C. V$SYSSTAT
  - D. V$SGASTAT

- 11. 根据 Oracle 的规定，调优良好的 OLTP 系统数据库缓存应具有什么比例？

  - A. 10% 或更少
  - B. 50%
  - C. 60–80%
  - D. 90% 或更高

- 12. 下列哪些缓冲区缓存池是必须的？

  - A. 留存池 (Keep Pool)
  - B. 默认池 (Default Pool)
  - C. 回收池 (Recycle Pool)
  - D. 以上都是必须的

- 13. 当用户发出 COMMIT 语句时，哪个 Oracle 进程最终会将数据库缓冲区中的信息写入磁盘？

  - A. SMON
  - B. DBWO
  - C. PMON
  - D. LGWR

- 14. 给定来自 `V$DB_CACHE_ADVICE` 的以下查询输出，在不浪费资源的情况下，数据库缓冲缓存的最佳大小是多少？

| NAME | SIZE_FOR_ESTIMATE | ESTD_PHYSICAL_READS |
| --- | --- | --- |
| DEFAULT | 10.1797 | 7686 |
| DEFAULT | 20.3594 | 6664 |
| DEFAULT | 30.5391 | 6028 |
| DEFAULT | 40.7188 | 5785 |
| DEFAULT | 50.8984 | 5497 |
| DEFAULT | 61.0781 | 5342 |
| DEFAULT | 71.2578 | 4915 |
| DEFAULT | 81.4375 | 4867 |
| DEFAULT | 91.6172 | 4866 |
| DEFAULT | 101.7969 | 4866 |
| DEFAULT | 111.9766 | 4866 |
| DEFAULT | 122.1563 | 4866 |

  - A. 70MB
  - B. 50MB
  - C. 100MB
  - D. 132MB

- 15. 下列哪些参数*不*影响数据库缓冲缓存的大小？

  - A. DB_KEEP_CACHE_SIZE
  - B. DB_BLOCK_SIZE
  - C. DB_MAX_CACHE_SIZE
  - D. DB_RECYCLE_CACHE_SIZE

- 16. 为什么增大数据库缓冲缓存的大小会提高性能？

  - A. 服务器进程在需要时更容易找到空闲缓冲区。
  - B. 缓冲区不太可能被 LRU 机制过早地移出缓存。
  - C. 以上两项都是正确的。
  - D. 以上都不正确。

- 17. 下列哪些缓冲池（Buffer Pools）可以用于缓存你确定的为频繁访问的段？

  - A. Kept
  - B. Keep
  - C. Cache
  - D. Pin

- 18. 下列哪些视图可以用于确定哪些段可能是 Keep 池的良好候选者？

  - A. V$BH
  - B. DBA_OBJECTS
  - C. V$CACHE
  - D. 以上任一

- 19. 选择数据库缓冲缓存中可用的三种组件池类型。

  - A. Default
  - B. Common
  - C. Keep
  - D. Recycle

- 20. 那些缓冲区即使在进行全表扫描时也会被放置在 LRU 列表最近使用末端的表称什么名称？

  - A. Pinned tables
  - B. Cache tables
  - C. Kept tables
  - D. 以上都不是

## 复习题答案
