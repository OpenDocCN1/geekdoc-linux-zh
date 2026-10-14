
![](img/563fad4219fcb3a5c1f1e5cc91d831ce_1050_1.png)

在 Oracle 8i 中，数据库助手被进一步划分为 Oracle 数据库配置助手和 Oracle 迁移助手。你将在这里检查配置助手。迁移助手将在本章的稍后部分介绍。

# 附录 B Windows NT 上的 Oracle

## Oracle 数据库配置助手

配置助手可以帮助你创建、修改和删除数据库。配置助手是一个带有向导界面的图形化工具，能够允许你创建数据库。你也可以修改或删除现有的数据库。Windows NT 允许你在机器上同时运行多个 Oracle 数据库。每个数据库必须有一个唯一的数据库名称。Oracle 数据库助手为每个数据库创建一个唯一的 NT 服务。你可以使用 Windows 控制面板中的服务小部件管理每个服务（见图 B.5）。

图 B.5

Oracle 数据库配置助手选项

![](img/563fad4219fcb3a5c1f1e5cc91d831ce_1051_0.png)

检查以下数据库信息，并进行任何适当的更改。数据库名称在位于服务器时标识你的数据库，并且应该是唯一的。

| 数据库名称 | SID | 初始化参数 | 兼容字符集 |
| :--- | :--- | :--- | :--- |

在数据库配置助手的帮助下创建新数据库时，助手会提供关于你想要创建的数据库类型的各种选项（见图 B.6）。

图 B.6

Oracle 配置助手-数据库安装类型。

![](img/563fad4219fcb3a5c1f1e5cc91d831ce_1051_1.png)

选择你希望数据库运行的模式：

- 专用服务器模式 (Dedicated Server Mode)

  对于每个连接，数据库将将分配一个进程仅为该客户端服务。当预计客户端连接数较少，或每个客户端对数据库执行复杂、长时间运行的请求时，请使用此模式。将可以使用 Oracle 多线程服务器功能。

- 共享服务器模式 (Shared Server Mode)

  客户端连接共享分配的资源池。当有超过少数的用户需要同时连接到数据库并共享资源时，请使用此模式。将可以使用 Oracle 多线程服务器功能。

## Windows NT 服务与 Oracle 实例

在 Windows NT 上工作时，Oracle DBA 可能会发现 Windows NT 服务与 Oracle 实例之间的区别非常令人混乱。本节将消除这种困惑。

Windows NT 中的服务是安装在 Windows NT 注册中的可执行文件。NT 注册跟踪每个所创建服务的安全信息。Oracle 实例是一个术语，用于描述与 Oracle 服务配对的 SGA（系统全局区域）。

每个特定数据库至少会创建一个 Oracle 服务：一个用于运行数据库的服务，以及另一个可能的、每当操作系统本身启动时就启动数据库的服务。当创建 Oracle 服务时，可以在“控制面板/服务”下找到，并以 `OracleServices` 的格式命名（见图 B.7）。`sid`（系统标识符）标识该服务所指的实例。此外，如果服务是由 NT 实例管理器以自动启动模式创建的，你可能会找到 `OracleStartsid`。

> William Page 的第 #127 条提示：安装 Oracle 时，还会为用于命名管道 (nmp) 的 Oracle 监听器和用于 TCP/IP (tcp) 的 Oracle 监听器创建服务。Oracle 监听器字面上就像是 Oracle 服务器上的一只耳朵，监听想要联系 Oracle 的客户端。

图 B.7 Windows NT 服务

| 名称 | 状态 | 启动模式 | 类 |
| :--- | :--- | :--- | :--- |
| OracleService | 运行中 | 手动 | |
| OracleServiceORI | 已启动 | 自动 | |
| OracleAS4(Broker,home_web440) | 已启动 | 手动 | |
| Plug and Play | 已启动 | 自动 | |
| Remote Image | 已启动 | 自动 | |
| Remote AutoUpdate Manager | 已启动 | 自动 | |
| Remote Access Connection Manager | 已启动 | 手动 | RDP 配置 |

当你首次在 NT 上安装 Oracle 时，你会发现安装已经创建了一个名为 `orcl` 的 Oracle 实例。oracle 实例是 Oracle 提供的默认数据库。如果你在控制面板中打开“服务”，你会发现两个项：`OracleServiceord` 和另一个名为 `OracleStartor` 的服务。你会注意到在服务名称旁边，它标识该服务为“自动”。服务有三种不同的启动模式，如表 B.4 所示。

### 表 B.4 NT 服务模式

| 模式 | 描述 |
| :--- | :--- |
| AUTOMATIC (自动) | 每次操作系统启动时，服务会自动启动 |
| MANUAL (手动) | 服务可以由用户或依赖服务手动启动 |
| DISABLED (已禁用) | 服务无法启动 |

> William Page 的第 #128 条提示：如果存在 `OracleStartsid` 服务，该服务不仅会被启动，而且实际数据库将在作为数据库内部用户的启动命令被下达时被打开。`OracleStarts` 服务会在 `ORANT\DATABASE\` 目录下创建一个 `startid.cmd` 文件。因此，当操作系统启动时，数据库也会启动，无需分别启动它们。

## 在 Windows NT 上安装 Oracle 实例

Windows NT 中的服务是安装在 Windows NT 注册中的可执行文件。NT 注册跟踪每个所创建服务的安全信息。Oracle 实例是一个术语，用于描述与 Oracle 服务配对的 SGA（系统全局区域）。

每个特定数据库至少会创建一个 Oracle 服务：一个用于运行数据库的服务，以及另一个可能的、每当操作系统启动时就启动数据库的服务。当创建 Oracle 服务时，可以在“控制面板/服务”下找到，并以 `OracleServices` 的格式命名（见图 B.7）。`sid`（系统标识符）标识该服务所指的实例。此外，如果服务是由 NT 实例管理器以自动启动模式创建的，你可能会找到 `OracleStartsid`。

当你首次在 NT 上安装 Oracle 时，你会发现安装已经创建了一个名为 `orcl` 的 Oracle 实例。oracle 实例是 Oracle 提供的默认数据库。如果你在控制面板中打开“服务”，你会发现两个项：`OracleServiceord` 和另一个名为 `OracleStartor` 的服务。你会注意到在服务名称旁边，它标识该服务为“自动”。服务有三种不同的启动模式，如表 B.4 所示。

> William Page 的第 #127 条提示：安装 Oracle 时，还会为用于命名管道 (nmp) 的 Oracle 监听器和用于 TCP/IP (tcp) 的 Oracle 监听器创建服务。Oracle 监听器字面上就像是 Oracle 服务器上的一只耳朵，监听想要联系 Oracle 的客户端。

图 B.7 Windows NT 服务

| 名称 | 状态 | 启动模式 | 类 |
| :--- | :--- | :--- | :--- |
| OracleService | 运行中 | 手动 | |
| OracleServiceORI | 已启动 | 自动 | |
| OracleAS4(Broker,home_web440) | 已启动 | 手动 | |
| Plug and Play | 已启动 | 自动 | |
| Remote Image | 已启动 | 自动 | |
| Remote AutoUpdate Manager | 已启动 | 自动 | |
| Remote Access Connection Manager | 已启动 | 手动 | RDP 配置 |

## 在 Windows NT 上安装 Oracle 服务器

一如既往，在 Windows NT 上安装 Oracle 之前，务必关闭数据库。在 Windows NT 上安装 Oracle 时，有一些你需要考虑的事项。之前的课程可能教过你，在接下来的章节中将介绍一些内容。

### 安装之前

在 Windows NT 上安装 Oracle 之前，重要的是检查以下基础清单：

- 阅读 Oracle 提供的联机指南和 Readme 文件。
- 安装相应的网络硬件和软件。
- 确保光驱有足够的磁盘空间。
- 执行安装后任务。
- 使用导出功能备份 Windows 注册。
- 如果需要任何存储库（例如 Enterprise Manager），请创建它。

### 安装说明
