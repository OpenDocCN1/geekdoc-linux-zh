

## 表 8-3 EMS 数据库资源

| 资源实例 | 描述 |
| :--- | :--- |
| status | 数据库状态 |
| allocated | 为数据库分配的磁盘空间 |
| used | 数据库实际使用的磁盘空间 |
| usage | 数据库实际使用的磁盘空间百分比 |

## 表 8-4 EMS 数据库服务器资源

| 资源实例 | 描述 |
| :--- | :--- |
| status | 数据库服务器状态 |
| connects | 当前活动的本地和远程连接数 |
| allowed_max_connects | 允许的最大同时连接数 |
| usage | 当前活动的最大连接数的百分比 |
| started | 数据库服务器开始执行的时间 |
| uptime | 服务器已运行的时长 |
| disk_reads | 物理读取次数 |
| disk_reads_per_sec | 每秒物理读取速率 |
| logical_reads | 逻辑读取次数 |
| logical_reads_per_sec | 每秒逻辑读取次数 |
| read_cache_hit_rate | 缓存中读取的百分比 |
| disk_writes | 物理写入次数 |
| disk_writes_per_sec | 每秒物理写入次数 |
| logical_writes | 逻辑写入次数 |
| logical_writes_per_sec | 每秒逻辑写入次数 |
| write_cache_hit_rate | 缓存中写入的百分比 |
| commits | 提交或中止的事务数量 |
| commits_per_sec | 每秒提交或中止的事务数量 |

尽管它提供了一些性能信息，例如每个数据库服务器的事务速率。

所有 EMS 监视器都支持多种通知方法，包括 SNMP、电子邮件、TCP 或 UDP 消息，或写入任意日志文件。EMS 监视器还可以直接通知 MC/ServiceGuard 发生的事件，从而可以立即启动适当的恢复操作。

EMS 还允许不同的操作员接收不同的事件或使用不同的通知标准。这些信息使用 EMS 配置 GUI 进行配置，该 GUI 是 SAM 的一部分。因此，系统操作员可以获得基本状态信息，而数据库管理员则接收更详细的性能警报。

图 8-1 显示了用于添加 bak1 数据库实例的数据库状态监控的 EMS GUI 屏幕。bak1 的状态为 ACTIVE。此资源的资源名称为 /rdms/database/status/bak1。

### 图 8-1 使用 EMS GUI 配置数据库状态监控。

![](img/eae88b61ada165139a1d9b546a34140b_246_0.png)

## 资源和性能监控工具

如前所述，大多数数据库性能问题是糟糕的数据库设计或编码不良的数据库查询的结果。导致性能问题的其他原因包括数据访问竞争（“热点”）、不足的硬件资源或配置不良的数据库服务器。本节介绍了各种用于定位数据库性能问题的工具和技术。

## 应用程序资源测量

由于测量应用程序的性能很困难，Hewlett-Packard 和 Tivoli Systems 联合开发了一套用于测量应用程序响应时间的开放 API。这套标准 API 称为应用程序资源测量（ARM）。如果应用程序已在关键位置修改以使用新的 API，则您可以测量和控制应用程序的端到端性能。在应用程序中调用 API 以标记事务的开始和结束。可以从 Tivoli 或 Hewlett-Packard 免费获得 ARM 的软件开发工具包（SDK），以简化此过程。表 8-5 列出并描述了可用的少数 ARM API。

Baan 已宣布其 ERP 应用的下一个版本将使用 ARM API 进行仪表化，这将使收集 Baan 的应用程序性能数据更加简单直接。

| **名称** | **功能** |
| :--- | :--- |
| arm_init | 为应用程序初始化 ARM 环境 |
| arm_getid | 命名应用程序中使用的每个事务类 |
| arm_start | 标记事务实例执行的开始 |
| arm_update | 更新关于事务实例的信息 |
| arm_stop | 标记事务的结束 |
| arm_end | 清理应用程序中 ARM 使用的内存 |

在收集应用程序数据后，可以通过性能管理工具（如 MeasureWare 和 HP PerfView）进行呈现。

## Oracle Trace

Oracle 有一个名为 Oracle Trace 的 API，它与 ARM API 相似，但 Oracle Trace 仅适用于 Oracle 环境。Oracle7 服务器版本 7.3.2 和 SQL*NET 版本 2.3 已经包含了 Oracle Trace 调用。Oracle Trace 可用于对 Oracle 应用程序进行仪表化以获取性能数据。这组 API 还可用于检测应用程序中发生的以下两种类型的事件：

- **持续时间或事务事件**：具有与之相关的开始和停止时间。
- **异步事件**：指特殊情况，如错误。

表 8-6 和 8-7 分别展示了为 Oracle Trace 仪表化的 Oracle Server 7.3 的持续时间和异步事件。

操作员可以使用异步事件来创建数据库访问的审计跟踪，例如。可以研究各种数据库事务的持续时间随时间的变化，以查找趋势。

修改以包含对 Oracle Trace 例程调用的应用程序称为*设施*。用户配置设施定义文件，以定义在跟踪应用程序时要收集哪些指标或*项目*。表 8-8 显示了默认情况下每个事件可用的项目。

还可以使用额外的跨设施项目，例如 Oracle7 服务器事务 ID，来关联从多个应用程序收集的数据。

在对应用程序进行仪表化后，可以从 OEM 控制台启用性能分析。实际上，Oracle Trace 管理器可以自动发现使用 Oracle Trace API 进行仪表化的应用程序。可以启动或停止跟踪，并且可以查看过去或当前活动跟踪的数据。应用程序还可以从内部开始和停止跟踪。可以在同一跟踪中包含多个设施。当跟踪（称为*集合*）停止时，数据将写入集合文件。

除了从 GUI 查看跟踪信息外，还可以针对集合文件运行报告。otrcrep 命令生成详细的跟踪报告，显示与集合中涉及的每个设施的每个事件的所有出现相关的所有项目的统计数据。例如，可以针对特定事件或特定进程生成报告。数据还可以导出到 Oracle7 服务器数据库，其中可以使用 SQL 脚本查询数据。Oracle 提供了一组示例脚本来说明如何执行此操作。

## 表 8-6 Oracle Trace 持续时间事件

| 事件 | 描述 |
| :--- | :--- |
| Parse Start | 包含 SQL 查询信息（查询的实际文本）的事件的开始 |
| Parse End | 包含 SQL 查询信息的事件的结束 |
| Execute Start | 包含执行 SQL 查询计划信息的事件的开始 |
| Execute End | 包含执行 SQL 查询计划信息的事件的结束 |
| Fetch Start | 包含实际行检索信息的事件的开始 |
| Fetch End | 包含实际行检索信息的事件的结束 |
| LogicalTX Start | 标记第一次执行可能更改数据库状态的数据库更新的事件的开始 |
| LogicalTX End | 标记第一次执行可能更改数据库状态的数据库更新的事件的结束 |
| PhysicalTX Start | 标记数据库状态发生确定性变化的事件的开始 |
| PhysicalTX End | 标记数据库状态发生确定性变化的事件的结束 |

## 表 8-7 Oracle Trace 异步事件

| 事件 | 描述 |
| :--- | :--- |
| Connection | 记录到数据库的每个连接 |
| Disconnect | 记录与数据库的每个断开连接 |
| ErrorStack | 核心转储的代码堆栈 |
| Migration | 共享服务器进程之间的会话迁移 |
| ApplReg | 应用程序上下文信息 |
| RowSource | 行信息 |
| SQLSegment | SQL 语句的文本 |
| Wait | 记录通用的 WAIT 事件；上下文在事件字符串中提供 |

## 表 8-8 Oracle Trace 标准项目

| 名称 | 描述 |
| :--- | :--- |
| UCPU | 用户模式下的 CPU 时间量 |
| SCPU | 系统模式下的 CPU 时间量 |
| INPUT_IO | 文件系统执行输入的次数 |
| OUTPUT_IO | 文件系统执行输出的次数 |
| PAGEFAULTS | 硬错误和软错误的缺页次数 |
| PAGEFAULT_IO | 硬缺页次数 |
| MAX_RSSIZE | 使用的最大驻留集大小 |

