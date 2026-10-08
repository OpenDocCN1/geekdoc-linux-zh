

Oracle 提供了一个用于计算持续时间事件经过时间的函数。还可以生成关于不同类型事件发生频率的报告，例如连接事件。可用的统计数据包括执行不同事件所花费的最短时间、最长时间和平均时间。Oracle Trace API 在表 8-9 中列出并附有简要描述。

## Oracle VS 表

Oracle 提供了一组可用于访问共享全局区域（SGA）内内存结构的虚拟表。其中许多表包含持续更新的数据库性能信息。表 8-10 列出并描述了一些更有趣的 VS 表的内容。

### 表 8-9 Oracle Trace API

| 名称 | 功能 |
| --- | --- |
| epc_init | 初始跟踪调用；用于向 Oracle Trace 注册设施 |
| epc_add_reg_id | 为设施添加注册 ID |
| epc_remove_reg_id | 移除设施的注册 ID |
| epc_start_event | 记录持续时间事件的开始 |
| epc_end_event | 记录持续时间事件的结束 |
| epc_event | 记录异步事件 |
| epc_collect | 在设施内部启动收集 |
| epc_cancel | 停止由 epc_collect 启动的收集 |
| epc_bind | 将进程绑定到已激活的收集 |
| epc_flush | 将收集数据缓冲区写入磁盘 |
| epc_context | 按线程基础存储收集数据 |
| epc_delete_context | 指示线程结束 |
| epc_set_cf_items | 向另一个进程发送跨设施项目 |
| epc_cf_value | 为跨设施项目赋值 |
| epc_get_cf_items | 从另一个进程获取跨设施项目 |

### 表 8-10 Oracle VS 表

| VS 表 | 包含内容 |
| --- | --- |
| V$DATABASE | 来自控制文件的数据库信息 |
| V$FILESTAT | 文件读写统计 |
| V$INSTANCE | 当前实例的状态信息 |
| V$LIBRARYCACHE | 库缓存性能信息 |
| V$LICENSE | 许可限制信息 |
| V$PROCESS | 进程信息 |
| V$ROWCACHE | 数据字典性能信息 |
| V$SESSION | 会话信息 |
| V$SESSTAT | 每个当前会话的内存使用情况信息 |
| V$SGA | 系统全局区域摘要信息 |
| V$SGASTAT | 系统全局区域详细信息 |
| V$SYSSTAT | V$SESSTAT 中每个变量的当前系统范围值 |

要获取所有可用的 Oracle V$ 性能监控表列表，请执行以下 SQL 查询：`SELECT * FROM X$KQFVI;`

有关 V$ 表的更多信息，请查阅 Oracle 的《Oracle 服务器调优指南》和《Oracle 服务器参考手册》。

## GlancePlus Pak 2000

GlancePlus Pak 2000 是惠普（Hewlett-Packard）的一款产品。它包括性能管理、故障管理以及实时性能监控。它包含三个组件：

- MeasureWare
- GlancePlus
- ITO/Special Edition

MeasureWare 是一款 HP 产品，用于收集和记录资源及性能指标。MeasureWare 代理在正在监控的各个服务器系统上运行并收集数据。许多平台和操作系统都有相应的代理，包括 HP-UX、Solaris 和 AIX。

MeasureWare 代理收集数据，对其进行汇总、添加时间戳、记录日志，并在适当时发出警报。代理收集和报告各种各样的系统资源、性能指标和用户定义数据。随后，这些信息可以导出到电子表格或性能分析程序（如 PerfView）。这些数据可被这些程序用于生成警报，以预警潜在的性能问题。通过使用历史数据，你可以发现趋势，这有助于你在资源问题影响系统性能之前解决它们。

MeasureWare 收集系统、应用程序、进程和事务数据。MeasureWare 代理在三个不同级别收集数据：全局系统指标、应用程序和进程指标。全局和应用程序数据每五分钟汇总一次，而进程数据则每 分钟汇总一次。

GlancePlus 是惠普提供的一款实时、图形化性能监控工具。它用于监控单个系统的性能和系统资源使用情况。你应该使用 GlancePlus 来判断性能问题是否可以孤立地归属于系统或数据库。既提供基于 Motif 的界面，也提供基于字符的界面。该产品可用于 HP-UX、Solaris 以及许多其他操作系统。

GlancePlus 收集与 MeasureWare 类似的信息，但采样频率更高。GlancePlus 可用于图形化查看当前 CPU、内存、交换（swap）和磁盘活动，以及系统级别的使用情况。它还可以显示应用程序和进程信息。如果 MeasureWare 代理已安装并处于活动状态，则可以显示事务信息。

ITO/Special Edition 是 ITO 的单系统版本。基于 Java 的图形用户界面允许你在事件浏览器中查看单个系统的事件。GUI 还提供了诊断工具。ITO/Special Edition 使用 ITO 的智能代理技术，该技术包括从各种来源收集数据和执行自动操作的能力。

要在 GlancePlus 或 MeasureWare 中监控应用程序，首先必须定义该应用程序。要定义关键应用程序，首先必须定义组成该应用程序的进程。这是通过在 `parrn` 文件中完成的（位于 `/var/opt/perf/parrn`），在其中列出构成应用程序的进程名称。如果确切名称有所不同，可以使用通配符。例如，可以使用 `ora*` 来定义基于所有以 `ora` 开头的进程的应用程序。GlancePlus 和 MeasureWare 对应用程序定义中列出的进程进行进程信息汇总。

可自定义的规则决定何时应作为警报发送系统性能问题。在 GlancePlus 中，这些规则由 GlancePlus Adviser 管理。在 Adviser 菜单上选择“Edit Adviser Syntax”选项后，你可以查看和修改所有警报条件。GlancePlus Adviser 语法文件（`/var/opt/perf/adviser.syntax`）包含症状和警报配置。也可以使用额外的语法文件。对于 MeasureWare，警报在位于 `/var/opt/perf/alarmdef` 的 `alarmdef` 文件中定义。

在 GlancePlus 中，警报会导致屏幕通知，其中颜色代表警报的严重程度。警报还可以触发自动执行的命令或脚本。除了发送警报外，GlancePlus 还可以通过使用其 EXEC 功能执行 UNIX 命令（如 `mailx`）来打印消息或通知你。

你还可以根据基于指标组合的条件发送警报。例如，CPU 瓶颈警报可以基于 CPU 使用率和 CPU 运行队列长度。MeasureWare 代理将这些警报提供给 PerfView 进行分析，并提供给 ITO 管理控制台。当达到阈值条件时，也可以发送 SNMP 陷阱。可以采取自动操作，或者操作员可以选择执行建议的操作。

可提供应用程序和事务级别的信息。事务必须由应用程序使用 ARM API 定义。以下是部分可用指标：

- 事务平均响应时间
- 事务响应时间分布
- 中止的事务数量
- 中止事务的响应时间

可以从 GlancePlus 和 MeasureWare 访问超过 600 个指标。使用产品的在线帮助功能可以查看指标完整列表。在安装了 GlancePlus Pak 2000 的系统上，这些信息也可以在目录 `/opt/perf/paperdocs/gp/C` 中找到。

Hewlett-Packard 还提供了另一款独立产品，即进程资源管理器（PRM），可用于控制用户或应用程序之间的 CPU、内存和磁盘使用率。PRM 还进行了一些针对 Oracle 的特殊集成。如果正在使用 PRM，GlancePlus 将显示 PRM 应用程序组在多大程度上保持在他们的资源权益范围内。从 GlancePlus 中，你还可以更改 PRM 进程组的权益。

虽然 MeasureWare 提供广泛的性能和资源信息，但其配置信息有限，且没有关于系统故障的数据。有关更多信息，请访问

