
# 附录 B WINDOWS NT 上的 Oracle

## 在 Windows NT 上安装 Oracle 实例

在 Windows NT 上工作时，Oracle DBA 可能会发现 Windows NT 服务与 Oracle 实例之间的区别非常令人混乱。本节将消除这种困惑。

Windows NT 中的服务是安装在 Windows NT 注册中的可执行文件。NT 注册跟踪每个所创建服务的安全信息。Oracle 实例是一个术语，用于描述与 Oracle 服务配对的 SGA（系统全局区域）。

每个特定数据库至少会创建一个 Oracle 服务：一个用于运行数据库的服务，以及另一个可能的、每当操作系统本身启动时就启动数据库的服务。当创建 Oracle 服务时，可以在“控制面板/服务”下找到，并以 `OracleServices` 的格式命名（见图 B.7）。`sid`（系统标识符）标识该服务所指的实例。此外，如果服务是由 NT 实例管理器以自动启动模式创建的，你可能会找到 `OracleStartsid`。

> William Page 的第 #127 条提示：安装 Oracle 时，还会为用于命名管道 `nmp` 的 Oracle 监听器和用于 TCP/IP `tcp` 的 Oracle 监听器创建服务。Oracle 监听器字面上就像是 Oracle 服务器上的一只耳朵，监听想要联系 Oracle 的客户端。

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
| AUTOMATIC（自动） | 每次操作系统启动时，服务会自动启动 |
| MANUAL（手动） | 服务可以由用户或依赖服务手动启动 |
| DISABLED（已禁用） | 服务无法启动 |

> William Page 的第 #128 条提示：如果存在 `OracleStartsid` 服务，该服务不仅会被启动，而且实际数据库将在作为数据库内部用户的启动命令被下达时被打开。`OracleStarts` 服务会在 `ORANT\DATABASE\` 目录下创建一个 `startid.cmd` 文件。因此，当操作系统启动时，数据库也会启动，无需分别启动它们。

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

安装从将 Oracle8 CD 放入光驱器开始。Oracle 安装程序应该立即启动；如果没有启动，请前往 Windows 资源管理器（我的电脑），选择光驱器并运行 `SETUP.bat`。之后，按照提示输入信息。强烈建议在安装期间选择默认值。如果你选择自定义而非默认设置，请注意其可能产生的影响。在安装 Oracle8.1 时需要记住以下几点：

- 以管理员组身份登录你的 Windows NT。
- 停止所有 Oracle 应用程序（如果运行）。
- 停止所有 Oracle 服务（如果运行）。

Oracle8.1 的默认安装目录为 `C:\oracle`。如果你使用之前的版本创建了 Oracle Home，请将 `C:\oracle` 更改为 `C:\oracle\ora8`。

![](img/563fad4219fcb3a5c1f1e5cc91d831ce_1053_0.png)

可用产品如下：

- Oracle8 企业版 8.1.x
- Oracle8 客户端 8.1.x
- Programmer2000 8.1.x

> 注意：要查看组件描述，点击新安装旁边的 (+) 号显示组件名称，然后将鼠标悬停在组件名称上。

如果选择了自定义安装，将出现 Oracle 协议支持界面。选择你想要安装 Oracle 协议支持的协议。你必须在计算机上安装该协议的原生软件。

> 注意：如果安装了所选产品，将出现配置界面，Net8 配置助手和 Oracle 数据库配置助手将连续启动。

> William Page 的第 #129 条提示：如果 Oracle 通用安装程序检测到硬盘上有早期版本的 Oracle 数据库，它会询问你是否要将数据库迁移到 Oracle8 企业版 8.1.x。如果你选择，Oracle 迁移助手将在安装结束时启动并迁移到 Oracle8 企业版 8.1.x。

### 升级之前

Oracle8 带有 Oracle 迁移助手，它可以帮助你从 Oracle 7.1.x、7.2.x、7.3.x 或 Oracle8.0.x 迁移到 Oracle8 数据库。（见图 B.8）。

图 B.8 Oracle 迁移助手主界面

![](img/563fad4219fcb3a5c1f1e5cc91d831ce_1054_0.png)

迁移工具将提示用户输入迁移的具体需求（参见图 B.9）。

图 B.9 Oracle 数据迁移助手——可迁移的有效数据库列表

![](img/563fad4219fcb3a5c1f1e5cc91d831ce_1055_0.png)
