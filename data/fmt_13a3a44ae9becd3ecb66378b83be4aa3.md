
# D. SWITCH_CURRENT_CONSUMER_GROUP

## 复习题

+ 15. 某些操作系统允许你确保 SGA 永不交换。在这种情况下，可以使用哪个 `init.ora` 参数？

+ A. `LOCK_SGA=TRUE`

B. `NOPAGE_SGA=TRUE`

C. `SGA_LOCK=TRUE`

D. `PIN_SGA=TRUE`

+ 16. 创建数据库时创建的默认资源计划之一被称为：

+ A. `DEFAULT_PLAN`

B. `SYSTEM_DEFAULT`

C. `SYSTEM_PLAN`

D. `PLAN_DEFAULT`

17. 下列哪个视图显示了分配给每个消费者组的用户信息？

+ A. `DBA_RSRC_CONSUMER_GROUP`

B. `DBA_RSRC_CONSUMER_GROUP_PRIVS`

C. `DBA_RSRC_CONSUMER_GROUPS_GRANTED`

D. `DBA_RSRC_CONSUMER_GROUPS`

18. 下列哪个视图显示当前实例中激活的资源计划？

+ A. `V$RSRC_ACTIVE_PLAN`

B. `V$RSRC_CURRENT_PLAN`

C. `V$RSRC_PLAN`

D. `V$RSRC_PLAN_ACTIVE`

19. 下列哪个视图显示 CPU 分配指令已分配给特定的资源计划？

+ A. `DBA_RSRC_PLAN_DIRECTIVES`

B. `DBA_RSRC_DIRECTIVES`

C. `DBA_RSRC_DIRECTIVE_CPU`

D. `DBA_RSRC_CPU`

20. “具有两个或多个 CPU 但只有一个内存。I/O、总线和磁盘资源由此服务器专门使用”描述的是哪种服务器架构？

A. 单处理器 (`Uniprocessor`)

B. 多进程处理 (`MPP`)

C. 对称多处理 (`SMP`)

D. 非统一内存访问 (`NUMA`)

## 复习题答案

- 1. D. 只有 Oracle9i 企业版包含资源管理器（Resource Manager）功能。

- 2. 对数据库资源有相同需求的用户可以归为一组，并分配相同的资源消费者组。

- 3. C. 线程是在单个操作系统进程内执行的独立指令序列。这种执行模型被 Windows 2000 等 Windows 操作系统采用。

- 4. D. CPU 利用率和活动会话数也可以使用资源计划指令进行定义。

- 5. 可以定义不同程度的 CPU 分配，最多分为多个级别。每当上一个级别剩余 CPU 时间时，每个后续级别都会获得 CPU 访问。

- 6. C. `DBMS_RESOURCE_MANAGER_PRIVS` 包中的 `ADMINISTER_RESOURCE_MANAGER` 过程可用于用户创建和管理资源管理器所需的权限。

- 7. A. 新的资源消费者组、资源计划和资源计划指令保留在待处理区域（pending area），直到它们通过验证并写入数据库。

- 8. B. 必须使用 `DBMS_RESOURCE_MANAGER` PL/SQL 包中的 `VALIDATE_PENDING_AREA` 过程在新的资源对象写入数据库之前进行验证。

- 9. A. `DBMS_RESOURCE_MANAGER` 包中的 `CREATE_CONSUMER_GROUP` 过程用于创建新的资源消费者组。

- 10. 交换（Swapping）是从内存中移除条目并将其写入磁盘的过程。交换是一种极其密集的操作，会对系统性能产生不利影响。应不惜代价避免这种情况。

- 11. D. `OTHER_GROUPS` 资源消费者组用于向不是当前实例级活动资源计划成员的用户分配资源权限。

- 12. B. 当用户发起到数据库的新连接时，指定为其初始 RCG 的资源消费者组将激活。

- 13. C. 实例的默认资源计划在实例启动时根据 `init.ora` 中的 `RESOURCE_MANAGER_PLAN` 参数确定。

- 14. A, B. `SWITCH_CONSUMER_CONSUMER_GROUP_FOR_USER` 通过用户名更改连接用户的当前资源消费者组。`SWITCH_CONSUMER_GROUP_FOR_SESS` 通过 SID 和 SERIAL# 更改连接用户的当前资源消费者组。

- 15. A. 在需要确保 SGA 永远不会被清除或交换的情况下，可以使用 `LOCK_SGA=TRUE` 参数。请咨询操作系统文档以查看是否可以使用此参数。

- 16. 每个数据库都包含至少一个资源计划，称为 `SYSTEM_PLAN`。该计划在数据库创建时创建。

- 17. B. `DBA_RSRC_CONSUMER_GROUP_PRVS` 视图还包含关于这是否为用户的初始资源消费者组的信息。

- 18. C. `V$SRC_PLAN` 视图将显示可用资源计划中哪一个处于实例级激活状态。

- 19. A. `DBA_RSRC_PLAN_DIRECTIVES` 视图将显示八个分配级别中的每个资源计划分配了多少 CPU。

- 20. C. 这描述了一个对称多处理器 (`SMP`) 服务器。

# 术语表

![](img/c36db8fbb4893c630ad429a99bfd63e3_594_0.png)

## A

**绝对方法（Absolute Method）** 一种通过指定每个资源允许的特定值为消费者组分配资源的方法。并行查询并行度资源是以这种方式分配的。

**活动会话池（Active Session Pool）** 资源管理器的一个组件，允许您限制与特定资源组关联的活动并发会话数。

**警报日志（Alert Log）** 由 Oracle 实例生成的文本文件，包含针对数据库的实例级活动。

**归档 redo日志（Archived Redo Log）** 在数据库处于归档日志模式（Archive Log Mode）时，在 redo日志切换时创建的 redo 日志副本。归档 redo 日志写入 `init.ora` 中 `LOG_ARCHIVE_DEST` 或 `LOG_ARCHIVE_DEST_n` 参数指定的位置。

**归档进程（ARC0）** 负责将 redo日志文件内容复制到目标位置归档日志的 Oracle 后台进程。

**归档（Archiving）** 在 redo日志被 `LGWR` 重用之前，将 redo日志内容复制到辅助位置的过程。

**异步（Asynchronous）** 一种不需要操作系统层协助的磁盘 I/O 方法。这些通常被称为“原始”设备。

**自动段空间管理（Automatic Segment-space Management）** 使用此功能的表空间利用数据文件头中的位图（而不是空闲列表）为存储在该表空间中的段分配空间。

**自动回滚管理（Automatic Undo Management）** 允许 Oracle 服务器动态地控制数据库中回滚段的数量和大小。

**自动跟踪（Autotrace）** 在 SQL*Plus 内部用于为 SQL 语句生成执行计划（Explain Plan）和资源使用信息的实用。

## B

**B-树索引（B-Tree Index）** 若干 Oracle 索引类型使用的平衡树索引结构。

**后台转储目标（BACKGROUND_DUMP_DEST）** `init.ora` 参数，指定 Oracle 后台进程生成的跟踪文件创建的目录。

**绑定变量（Bind Variables）** 用于存储 SQL 语句中传递的值的容器，因此实际值本身不包含在语句中。使用绑定变量可以增加共享池（Shared Pool）的比例。

**位图（Bitmap）** 用于指示列内容是否在位图索引中的二进制字符串。值 1 表示指定值存在于列中；值 0 表示其不存在（注：原文此处可能有误， "0 indicates that it does" 应为 "does not"）。

**位图索引（Bitmap Index）** 列内容的二进制映射。当在列上创建位图索引时。

**块（Blocks）** Oracle 数据库中最小 I/O 单位是块。每个块存储与段（例如表或索引）关联的数据。

**缓冲区顾问（Buffer Cache Advisor）** 允许 DBA 估计如果更改缓存大小，缓存命中率的潜在改进。

**缓冲区池（Buffer Pool）** 根据段的使用性质在缓存中缓存段。频繁访问的段可以缓存在 Keep 池中，不经常访问的段可以缓存在 Recycle 池中。所有其他段将缓存在 Default 池中。

**忙率（Busy Ratio）** 忙率用于确定应用程序请求共享服务器组件的频率。高忙率表明可能需要添加共享服务器资源（如分发器和共享服务器）。

## C

**缓存命中（Cache Hit）** 在内存中找到所需的对象，因此无需从磁盘读取（对于数据库缓冲区而言）或进行解析（对于共享池而言）。

**缓存缺失（Cache Miss）** 在内存中未找到所需的对象，因此必须从磁盘读取（对于数据库缓冲区而言）或进行解析（对于共享池而言）。

**缓存表（Cache Table）** 当通过全表扫描访问时，其缓冲区被放置在 LRU 列表最近使用一端的表。
