
- `B. DBA_RSRC_CONSUMER_GROUP_PRIVS`
- `C. DBA_RSRC_CONSUMER_GROUPS_GRANTED`
- `D. DBA_RSRC_CONSUMER_GROUPS`

### 18. 下列哪个视图显示实例中当前活动的资源计划？
- `A. V$RSRC_ACTIVE_PLAN`
- `B. V$RSRC_CURRENT_PLAN`
- `C. V$RSRC_PLAN`
- `D. V$RSRC_PLAN_ACTIVE`

### 19. 下列哪个视图显示已分配给特定资源计划的 CPU 分配指令？
- `A. DBA_RSRC_PLAN_DIRECTIVES`
- `B. DBA_RSRC_DIRECTIVES`
- `C. DBA_RSRC_DIRECTIVE_CPU`
- `D. DBA_RSRC_CPU`

### 20. “具有两个或更多 CPU，但只有一个内存区域的服务器。I/O、总线磁盘资源由该服务器独占使用”描述的是哪种类型的服务器架构？
- `A. 单处理器（Uniprocessor）`
- `B. 大规模并行处理（MPP）`
- `C. 对称多处理（SMP）`
- `D. 非统一内存访问（NUMA）`

# 复习题答案

1. `D.` 只有 Oracle9i 企业版包含资源管理器功能。
2. `B.` 对数据库资源具有相同访问需求的用户可以组合在一起，并分配到相同的资源使用者组。
3. `C.` 线程是在单个操作系统进程内执行的独立指令序列。这种执行模型被 Windows 2000 等 Windows 操作系统所采用。
4. `B, D.` CPU 利用率和活动会话数也可以通过资源计划指令来定义。
5. `C.` 可以在多达八个级别上定义不同程度的 CPU 分配。每当前一个级别有多余的 CPU 时间时，下一个级别就会获得 CPU 访问权限。
6. `C.` `DBMS_RESOURCE_MANAGER_PRIVS` 包中的 `ADMINISTER_RESOURCE_MANAGER` 过程可用于为用户分配创建和管理资源管理器所需的权限。
7. `A.` 新的资源使用者组、资源计划和资源计划指令保存在挂起区域，直到它们被验证并写入数据库。
8. `B.` 在将新的资源管理器对象写入数据库之前，必须使用 `DBMS_RESOURCE_MANAGER` PL/SQL 包中的 `VALIDATE_PENDING_AREA` 过程来验证它们。
9. `A.` `DBMS_RESOURCE_MANAGER` 包的 `CREATE_CONSUMER_GROUP` 过程用于创建新的资源使用者组。
10. `A.` 交换（Swapping）是将整个进程从内存移除并写入磁盘的处理过程。交换是一种资源密集型操作，可能对系统性能产生不利影响。应不惜一切代价避免这种情况。
11. `D.` `OTHER_GROUPS` 资源使用者组用于将资源权限分配给不属于实例级别当前活动的资源计划的某个资源计划的成员的用户。
12. `B.` 当用户启动与数据库的新连接时，指定为其初始 RCG 的资源使用者组将处于活动状态。
13. `C.` 实例的默认资源计划在实例启动时根据 `init.ora` 中的 `RESOURCE_MANAGER_PLAN` 参数确定。
14. `A, B.` `SWITCH_CONSUMER_GROUP_FOR_USER` 通过用户名更改已连接用户的当前资源使用者组。`SWITCH_CONSUMER_GROUP_FOR_SESS` 通过 SID 和 `SERIAL#` 更改已连接用户的当前资源使用者组。
15. `A.` `LOCK_SGA=TRUE` 参数可用于希望确保 SGA 从未被分页或交换的情况。请咨询你的操作系统文档以查看是否可以使用此参数。
16. `C.` 每个数据库都包含至少一个资源计划，称为 `SYSTEM_PLAN`。该计划在数据库创建时创建。
17. `B.` `DBA_RSRC_CONSUMER_GROUP_PRIVS` 视图还包含有关这是否是用户的初始资源使用者组的信息。
18. `C.` `V$RSRC_PLAN` 视图将显示可用的资源计划中哪个在实例级别处于活动状态。
19. `A.` `DBA_RSRC_PLAN_DIRECTIVES` 视图将显示在每个八个分配级别上分配给每个资源计划的 CPU 量。
20. `C.` 这描述的是对称多处理器（SMP）服务器。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_595_0.png)

# 术语表

## A

**绝对方法（Absolute Method）** 一种通过指定每个资源允许的具体值来向使用者组分配资源的方法。并行查询的并行度资源就是这样分配的。

**活动会话池（Active Session Pool）** 资源管理器的一个组件，允许你限制与特定资源组关联的活动并发会话的数量。

**警报日志（Alert Log）** 由 Oracle 实例生成的文本文件，包含有关针对数据库的实例级别活动的信息。

**归档重做日志（Archived Redo Log）** 当数据库处于归档日志模式时，在重做日志切换时创建的重做日志的副本。归档重做日志写入 `init.ora` 中由 `LOG_ARCHIVE_DEST` 或 `LOG_ARCHIVE_DEST_n` 参数指定的位置。

**归档进程（Archiver, ARC0）** 负责将重做日志文件的内容复制到归档目的地中归档日志的 Oracle 后台进程。

**归档（Archiving）** 在 LGWR 重新使用重做日志之前，将重做日志的内容复制到次要位置的过程。

**异步（Asynchronous）** 一种执行磁盘 I/O 的方法，不需要操作系统层的协助。这些通常被称为“裸”设备。

**自动段空间管理（Automatic Segment-space Management）** 使用此功能的表空间利用表空间数据文件头中的位图（而不是空闲列表）来分配空间给存储在该表空间中的段。

**自动撤销管理（Automatic Undo Management）** 允许 Oracle 服务器动态控制数据库中回滚段的数量和大小。

**Autotracer** 一种在 SQL*Plus 内部为 SQL 语句生成执行计划和资源使用信息的实用工具。

## B

**B树索引（B-Tree Index）** 多种 Oracle 索引类型使用的平衡树索引结构。

**背景转储目标目录（BACKGROUND_DUMP_DEST）** 指定由 Oracle 后台进程生成的跟踪文件应创建所在的目录的 `init.ora` 参数。

**绑定变量（Bind Variables）** 在 SQL 语句中保存传入值的容器，因此语句中不包含实际值本身。使用绑定变量可以提高共享池命中率。

**位图（Bitmap）** 在位图索引中用于指示列内容的二进制字符串。值为 1 表示指定值存在于该列中；值为 0 表示不存在。

**位图索引（Bitmap Index）** 索引列内容的二进制映射。在创建表列的位图索引时使用。

**块（Blocks）** Oracle 数据库中 I/O 的最小单位是一个 Oracle 块。每个块存储与特定段类型（例如表或索引）相关的数据。

**缓冲区缓存顾问（Buffer Cache Advisor）** 允许数据库管理员（DBA）评估如果对数据库缓冲区缓存的大小进行更改，缓冲区缓存命中率可能获得的改进。

**缓冲区池（Buffer Pool）** 根据段的使用性质，用于在数据库缓冲区缓存中缓存段缓冲区。经常访问的段可以缓存在 Keep 池中，不常访问的段可以缓存在 Recycle 池中。所有其他段将缓存在 Default 池中。

**忙碌比（Busy Ratio）** 忙碌比用于确定应用程序用户请求共享服务器组件的频率。高忙碌比表明可能需要增加共享服务器资源（例如调度程序和共享服务器）。

## C

**缓存命中（Cache Hit）** 在内存中找到所需对象，因此无需从磁盘读取（对于数据库缓冲区缓存而言）或解析（对于共享池而言）的过程。

**缓存未命中（Cache Miss）** 在内存中未找到所需对象，因此需要从磁盘读取（对于数据库缓冲区缓存而言）或解析（对于共享池而言）的过程。

**缓存表（Cache Table）** 即使通过全表扫描访问，其缓冲区也会放置在 LRU 列表最近使用端的一张表。

**基数（Cardinality）** 衡量存储在表列中数据变异程度的指标。如果列包含许多不同的值，则称其具有高基数。如果列包含很少的不同值，则称其具有低基数。

**检查点进程（Checkpoint Process (CKPT)）** 在数据库检查点事件时更新控制文件和数据文件头的 Oracle 后台进程。

**簇（Cluster）** 一种物理存储方法，允许将一个或多个表的数据存储在同一物理块中，并围绕一个共同值（簇键）进行聚集。

**复合分区（Composite Partitioning）** 一种使用范围分区和哈希分区组合来存储表数据的表分区技术。

**压缩（Compressed）** 一种通过为每个索引键存储一个值以及与该索引关联的所有 ROWID 来最小化磁盘使用和磁盘 I/O 的索引类型。

**争用（Contention）**
