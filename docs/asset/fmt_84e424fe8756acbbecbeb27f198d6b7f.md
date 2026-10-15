
HA 监控器包含多个用于监控文件系统空间、网络接口状态、磁盘状态和 `MC/ServiceGuard` 集群状态的 `EMS` 监控器。`HA` 监控器还提供 `CPU` 负载和系统用户数量的监控。监控器还包括数据库监控。

`HP` 的 `ATM` 适配器和 `HyperFabric` 适配器也可以使用 `EMS` 进行监控。每个这些产品都包含一个 `EMS` 监控器。这些资源还与 `MC/ServiceGuard` 集成。例如，`HA ATM` 在发生故障时首先尝试执行本地恢复，但如果无法提供本地恢复，它会通知 `MC/ServiceGuard` 触发到备用节点的故障转移。

所有可以监控的不同资源都包含在一个单一的 `EMS` 资源层次结构中。包含系统硬件和内核资源的层次结构部分如图 3-3 所示。在 `EMS GUI` 中配置监控器请求时，您会看到整个资源层次结构。

## 监控功能

`EMS` 旨在用于高可用性环境。用户只能选择要监控的关键组件，因此资源监控器不会延迟轮询非关键组件的信息。这与 `IT/O` 等其他工具不同，后者通常从所有组件收集数据。`IT/O` 代理执行系统级命令，然后解析输出。因此，如果非关键组件挂起，`IT/O` 代理可能会不必要地延迟等待其响应。相比之下，`EMS` 监控器只查询关键组件。

`HP-UX` 上的多个系统组件已使用 `EMS` 事件管理库来提供监控。`IBM` 最近宣布了一套类似的称为 `Phoenix` 的事件管理例程，用于其 `AIX` 环境，希望其软件开发合作伙伴采用。`Sun` 未为 `Sun Solaris` 提供事件管理库。

`EMS` 是允许资源监控器向 `MC/ServiceGuard` 发送事件的唯一方法，这再次反映了其对高可用性的重视。`EMS` 还可以通过 `SNMP`、`opcmq`、`TCP`、`UDP` 和电子邮件发送通知，并可以写入控制台、指定文本文件或另一个应用程序。

`EMS` 提供了一些关键功能。它旨在为用户提供一种一致的方法来启用不同系统组件的监控，这是通过 `EMS SAM GUI`、`MC/ServiceGuard SAM GUI`、硬件请求管理器 `monconfig` 和一组 `EMS` 库例程完成的。

在配置监控条件时，您可以选择在每个轮询间隔、值更改或达到某个配置阈值时请求通知。轮询间隔可以从 30 秒到 1 天不等。

您可以配置随事件一起发送的附加信息，为使用 `EMS` 的特定环境提供定制。此外，当事件发生时，资源监控器可以包含额外的资源特定信息以帮助问题诊断。

`EMS` 是考虑到系统性能而创建的。只有当用户要求监控至少一个资源实例时，`EMS` 资源监控器才会运行。此外，同一监控器进程可以并发监控多个资源实例。提供 `EMS API` 以便监控器在适当的时间间隔检查资源。异步接收资源信息的监控器不需要使用这些 `API`，因此可以更高效地运行。这使得可以在微秒内接收事件通知，而无需承受频繁轮询的系统性能惩罚。

`EMS` 警报是为每个客户端单独配置的。其他产品（如 `MeasureWare`）的警报是系统范围的。`EMS` 比其他需要等待汇总时间间隔到期的工具能更快地检测问题。然而，`EMS` 没有持续时间或复合条件的概念，这些概念可以与警报相关联。

`EMS` 请求是按客户端进行的。目标“用户”可以接收定制的事件数据，而另一个“用户”可以为同一事件接收不同的数据。`EMS` 监控器数据使监控器能够为事件提供定制数据。

为了确保受监控的资源继续被监控，`EMS` 提供了“持久性客户端”。`EMS` 持久性客户端检测监控器失败并自动重启它。

### 监控器发现和配置

`EMS` 为可监控资源的发现和配置提供了一致的 `GUI`。可从 `SAM` 获取的 `EMS GUI` 可以自动发现系统上可用的资源监控器集合。资源实例可能因硬件和软件配置不同而因系统而异。使用 `EMS`，您可以定义指示何时应发送通知事件的的条件。通知可以在定期间隔、组件状态更改或满足阈值条件时发送。`EMS` 还允许您配置应发送事件的位置。

#### 图 3-3 EMS 资源层次结构

```
/system/numUsers
/system/jobQueue1Min
/system/jobQueue5Min
/system/jobQueue15Min
/system/events/memory/<instance>
/system/status/memory/<instance>
/system/filesystem/availMb/<filesystem_name>
/system/kernel_resource/process_management/nproc
/system/kernel_resource/file_system/nfiles
/system/kernel_resource/file_system/nfile
/system/kernel_resource/misc/ncllout
/system/kernel_resource/system_v_ipc/shared_memory/shmni
/system/kernel_resource/system_v_ipc/semaphore/semni
/system/kernel_resource/system_v_ipc/semaphore/semns
/system/kernel_resource/system_v_ipc/message/msgmni
/system/kernel_resource/system_v_ipc/message/msgseg
/system/kernel_resource/system_v_ipc/message/msgtql
/storage/events/disks/default/<path>
/storage/events/tape/SCSI_tape/<path>
/storage/events/disk_arrays/High_Availability/<path>
/storage/events/disk_arrays/FW_SCSI/<path>
/storage/events/enclosures/ses_enclosure/<path>
/storage/status/disks/default/<path>
/storage/status/tape/SCSI_tape/<path>
/storage/status/disk_arrays/High_Availability/<path>
/storage/status/disk_arrays/AutoRAID/<ID>
/storage/status/disk_arrays/FW_SCSI/<path>
/storage/status/enclosures/ses_enclosure/<path>
/adapters/status/FC_adapter/<path>
/adapters/events/FC_adapter/<path>
/net/interfaces/lan/status/<interface_name>
/net/interfaces/switched/atm/<emulated_lan_name>
/net/interfaces/clic/status/<instance>
/net/subnetwork/osi/x25subnet/status/<x25_instance>
```

## EMS 要求在每个本地节点上发起监控请求

`EMS` 要求监控请求必须在每个本地节点上发起；然而，这也允许针对本地系统定制监控请求，从而只需监控关键资源。由于缺乏轻松实现跨多个系统监控的能力，不应将 `EMS` 视为一个企业级框架。

使用 `EMS GUI` 来配置每个被监控的资源实例可能会耗费大量时间。`EMS` 配置 `GUI` 支持使用通配符以简化配置。此外，随在线诊断工具 `Online Diagnostics` 提供的 `EMS` 硬件监控器已预先配置好。如果您正在使用 `IT/O`，有一个名为 `monvols` 的工具可以帮助您配置所选系统的所有逻辑或物理卷。当从 Web 上的 `http://www.software.hp.com/products/EMS` 下载 `EMS` 开发人员工具包 `Developer's Kit` 时，`monvols` 工具以及其他 `EMS` 工具和模板均可免费获取。但请注意，`monvols` 仅适用于 `HP-UX 10.20`。

要配置大多数 `EMS` 监控器，您需要使用 `SAM`。从其资源管理 `Resource Management` 功能区域，您可以选择事件监控服务 `Event Monitoring Service` 以启动 `EMS GUI`，然后添加一个新的监控请求。初始配置界面如图 3-4 所示。

### 图 3-4 初始 EMS 配置界面

![](img/eae88b61ada165139a1d9b546a34140b_45_0.png)

`MC/ServiceGuard` 提供了一个 `GUI`，以及命令行和配置文件选项，用于将包配置为依赖于 `EMS` 资源。在这种情况下，事件通知直接从资源监控器发送到 `MC/ServiceGuard`。
