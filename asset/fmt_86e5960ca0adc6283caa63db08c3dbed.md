
| oradb | 4 | 1334 | 1334 |  |

| oradb | 5 | 1338 | 1338 |  |

| oradb | 6 | 1342 | 1342 |  |

| george | JUNGLE | 7 | 277:412 | 3056 |

| sam | SAMS | 10 | 181:245 | 28975 |

| sam | SAM | 12 | 187:282 | 1686 |

| lily | LILY | 13 | 29902 | 21430 |

| sam | SAM | 16 | 292:197 | 28959 |

| sam | SAM | 19 | 187:282 | 28989 |

12 rows selected.

```
SQL>
```

虽然 RDBMS MIB 定义了九个表，但只有五个是真正的供应商独立的。这些表显示在表 8-1 中。`rdbmsSrvParamTable` 也由主要数据库供应商提供，但此表中包含的服务器配置信息是特定于数据库的，并可能包含自定义参数。Informix 和 Oracle 不支持 MIB 中定义的其他三个表：`rdbmsDbParamTable`、`rdbmsDbLimitedResourceTable` 和 `rdbmsSrvLimitedResourceTable`。

在 RDBMS MIB 中定义了两种 SNMP 陷阱，`rdbmsStateChange` 和 `rdbmsOutOfSpace`，但只有 `rdbmsStateChange` 得到了一致的实现。当数据库或数据库服务器的状态更改为受限或不可用时，会发送该陷阱。您可能需要修改管理站上的陷阱配置文件以接收新的陷阱。

RDBMS MIB 主要用于监控，而不是管理。然而，其中的许多信息是静态配置信息，对于操作监控没有用处。主要数据库供应商还支持在 RFC 2248 中定义的 Network Services MIB，作为数据库进程信息的仓库。Network Services MIB 通常被简称为“Application MIB”，尽管互联网工程任务组（IETF）已经定义了具有该名称的不同 MIB。表 8-2 列出了 RDBMS MIB 中有用的字段，以及 Network Services MIB 中的应用表（`appTable`）。此表中仅包含 Oracle 和 Informix 均可用的 MIB 变量。

表 8-2 中列出的许多变量用于监控数据库或数据库服务器的状态。`appOperStatus` 字段可用于指示数据库服务器的操作状态：up、down、congested 或 restarting。`appInBoundAssociations` 变量可用于确定到数据库的当前活动连接数。`rdbmsRelState` 指示数据库的状态：active、available、restricted、unavailable 或 other。

一些数据库监控变量也可用于资源控制。`rdbmsDbInfoSizeAllocated` 和 `rdbmsDbInfoSizeUsed` 变量可用于确定数据库可用的空闲磁盘空间量，指示是否应分配更多空间。`appInboundAssociations` 可以与服务器信息表中的最大允许入站关联数进行比较。

您可以将这些变量与 Hewlett-Packard 的 Process Resource Manager (`PRM`) 结合使用，当活动用户过多时增加或限制系统资源授权。服务器信息表包括关于处理的事务数以及服务器执行的读和写次数的几个有趣统计。例如，逻辑读与物理读的比例可用于确定适当的缓存大小。然而，服务器信息表中的信息是聚合到数据库服务器层面的，因此这里不提供特定于数据库的统计信息（除非数据库服务器仅处理一个数据库）。数据库关系表用于将数据库与其服务器相匹配。

如果您希望监控 Informix，`rdbmsSrvLimitedResource` 表很有用，因为它包含当前已达成的资源限制和阈值。该表在 Oracle 中不受支持。RDBMS MIB 中其他有趣的变量通常对 Oracle 不可用，但对 Informix 可用，包括：

- `rdbmsDbInfoLastBackup`：指示上次数据库备份的时间戳。
- `rdbmsSrvInfoOutOfSpaces`：指示数据库服务器无法获取其所需磁盘空间的次数。
- `rdbmsRelActiveTime`：指示该数据库由数据库服务器激活的时间。

由于 MIB 定义很少改变，在您配置一些 MIB 变量进行监控后，该配置很可能适用于多个数据库版本。这有助于减轻对新的数据库软件版本重新认证的负担。

#### 表 8-1 供应商独立的 RDBMS MIB 表

| 表名 | 描述 |
| :--- | :--- |
| `rdbmsDbTable` | 关于系统中安装的数据库的信息 |
| `rdbmsDbInfoTable` | 关于系统中数据库的更多（动态）信息 |
| `rdbmsSrvTable` | 系统中正在运行或安装的数据库服务器表 |
| `rdbmsSrvInfoTable` | 数据库服务器统计表 |
| `rdbmsRelTable` | 显示数据库到服务器的关系（或映射）的表 |

#### 表 8-2 有用的 RDBMS MIB 字段

| 变量 | MIB 表 | 描述 |
| :--- | :--- | :--- |
| `appUptime` | `appTable` | 数据库已运行时间 |
| `appOperStatus` | `appTable` | 数据库服务器状态 |
| `appInboundAssociations` | `appTable` | 当前活动的本地和远程对话数 |
| `rdbmsSrvInfoStartupTime` | `rdbmsSrvInfoTable` | 上次服务器重启的时间戳 |
| `rdbmsSrvInfoFinished-Transactions` | `rdbmsSrvInfoTable` | 已提交或中止的事务数 |
| `rdbmsSrvInfoDiskReads` | `rdbmsSrvInfoTable` | 服务器执行的物理读次数 |
| `rdbmsSrvInfoLogicalReads` | `rdbmsSrvInfoTable` | 服务器执行的逻辑读次数 |
| `rdbmsSrvInfoDiskWrites` | `rdbmsSrvInfoTable` | 服务器执行的物理写次数 |
| `rdbmsSrvInfoLogicalWrites` | `rdbmsSrvInfoTable` | 服务器执行的逻辑写次数 |
| `rdbmsSrvInfoHighWater-InboundAssociations` | `rdbmsSrvInfoTable` | 服务器处理的最大同时入站关联数 |
| `rdbmsSrvMaxInbound-Associations` | `rdbmsSrvInfoTable` | 允许的最大同时入站关联数 |
| `rdbmsDbInfoSizeAllocated` | `rdbmsDbInfoTable` | 为该数据库分配的磁盘空间 |
| `rdbmsDbInfoSizeUsed` | `rdbmsDbInfoTable` | 该数据库实际使用的磁盘空间 |
| `rdbmsRelState` | `rdbmsRelTable` | 数据库状态 |

这些 MIB 提供了有助于配置管理、资源管理和故障管理的信息。对于性能管理，可以通过监控 RDBMS MIB 中的性能指标来计算 I/O 速率。随时间收集 I/O 速率提供了一种跟踪 I/O 性能的简单方法。

尽管 MIB 数据易于访问，但浏览 MIB 是一个手动过程，通常需要你轮询所需的信息。手动查询仅捕获快照。与许多指标一样，你真的需要在一段时间内收集信息，以便进行比较。

### 数据库供应商工具

本节介绍了数据库供应商提供的一些监控功能。后面的章节将讨论由第三方提供的复杂数据库监控工具。

#### Oracle Enterprise Manager

Oracle 开发了一个名为 Oracle Enterprise Manager (`OEM`) 的数据库管理平台，用于数据库管理。`OEM` 包含用于监控网络和数据库对象、在多个系统上安排任务以及分发软件的工具。Oracle Diagnostics Pack、Oracle Tuning Pack 和 Oracle Change Management Pack 是提供额外功能（如数据库调优和容量规划）的可选软件包。`OEM` 有许多不同的组件，包括以下内容：

- **控制台**：包含映射和事件管理功能。导航器窗口显示对象层次结构，例如监听器、命名服务器和数据库，你可以选择并在地图上显示它们。你可以使用过滤来减少显示的物体数量。你可以通过将对象从导航器层次结构拖入 Map 窗口来创建 Map 窗口，以仅显示你需要监控的重要对象。创建并定制地图后，你可以通过菜单选项随时保存和调用它们。控制台还可用于监控活动任务及任务历史。事件窗口显示发生在数据库、监听器和节点上的事件。你可以确认事件或查看事件历史，其中包含确认该事件的管理员姓名。
