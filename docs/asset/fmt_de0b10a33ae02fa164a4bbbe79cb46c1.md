
| | `sftp` | 使用类似 FTP 的命令执行安全文件传输，该命令可在 SSH1 和 SSH2 协议上运行。 |

| | `scp` | 在网络上的主机之间复制文件。它使用 SSH1 进行数据传输，并使用与 SSH1 相同的身份验证并提供相同的安全性。 |

| | | 如果身份验证需要，`Scp` 会提示输入密码或短语。 |

## SSH 命令选项

从 SSH 客户端开始，你可以配合 `ssh` 命令使用以下基本选项：

| 表 3-5 | 选项 | 描述 |

| :--- | :--- | :--- |

| | `-b` `bind_address` | 指定从多个地址或别名地址的机器传输的本地 IP 地址。 |

| | `-C` | 启用压缩。 |

| | `-D` `port` | 启用动态应用层端口转发。 |

| | `-f` | 身份验证后进入到后台运行。 |

## （续）表 3-5 选项描述

| 选项 | 描述 |

| :--- | :--- |

| `-g` | 允许远程主机连接到转发的端口。 |

| `-l` `username` | 使用指定的用户名登录。 |

| `-L` `listen-port:host:port` | 将本地端口转发到远程地址。这导致 `ssh` 在端口上监听连接，并通过连接到 `host:port` 将它们转发到另一端。 |

| `-p` `port` | 连接到指定的端口。服务器必须在相同的端口上。 |

| `-q` | 不显示任何警告消息。 |

| `-R` `listenport:host:port` | 将远程端口转发到本地地址。导致 `ssh` 在端口上监听连接，并通过连接到 `host:port` 将它们转发到另一端。 |

| `-x` | 禁用 X11 连接转发（默认）。 |

| `-X` | 启用 X11 连接转发。 |

## SSH 命令示例

以下是在 OES Linux 命令提示符中使用 SSH 客户端命令的一些示例：

- `root@DA2:-> ssh da4.da.com`

  在此示例中，用户 root 登录计算机 da4.da.com。

- `root@DA2:-> ssh -l admin da4.da.com`

- `root@DA2:-> ssh -l admin da4.da.com`

  在此示例中，用户 root 登录计算机 da4.da.com。

- `root@DA2:-> ssh -l admin da4.da.com`

- `root@DA2:-> ssh -l admin da4.da.com`

## 集成 Linux 版本的 Novell Open Enterprise Server

## NRM 管理任务对比

当你首次打开 OES NetWare 上的 NRM 和 OES Linux 上的 NRM 时，你会发现它们存在显著的差异：

图 3-1

![](img/1dca8e8a8784dadffa032dcfe0460e55_219_0.png)

虽然你可以在 OES NetWare 和 OES Linux 服务器上通过 NRM 执行许多相同的管理任务，但与 OES NetWare 上的 NRM 相比，OES Linux 上的 NRM 在功能上存在一些局限。

然而，有一些对于管理 Linux 服务器至关重要的任务（例如监控服务器进程），这些任务仅在 OES Linux 上的 NRM 中提供。

以下比较了 OES NetWare 和 OES Linux 上主要 NRM 特性的可用性：

| 表 3-6 | 任务 | OES 平台 |

|---|---|---|

| 监控和管理您的服务器健康状况： | | |

| 监控一个或多个服务器的健康状态。 | NetWare/Linux | |

| 构建一个可以对其执行组操作的服务器组。 | NetWare/Linux | |

| 访问 Novell eDirectory 健康检查和故障排除工具。 | NetWare | |

| 访问服务器和配置日志。 | NetWare/Linux | |

| 配置您的服务器： | | |

| 管理磁盘分区。 | NetWare | |

| 访问服务器控制台屏幕。 | NetWare/Linux | |

| 查看所有硬件适配器、硬件资源和处理器数据的信息。 | NetWare/Linux | |

| 上传并替换 NLM 程序、LAN 驱动程序或磁盘驱动程序。 | NetWare | |

| 上传、访问和替换文件 | NetWare/Linux | |

| 监控系统磁盘空间和内存资源。 | NetWare/Linux（仅限内存） | |

| 访问卷和 DOS 分区上的文件。 | NetWare | |

| 管理服务器连接。 | NetWare | |

| 配置 Set 参数。 | NetWare | |

| 为运行控制台命令设置计划。 | NetWare | |

| 关闭、重启或重置服务器。 | NetWare/Linux | |

| 排除服务器问题： | | |

| 查找 CPU 占用者。 | NetWare | |

| 运行并查看一个或多个服务器的清单报告。 | NetWare | |

| 查找高内存占用用户。 | NetWare/Linux | |

| 从源头追踪。 | NetWare | |

| 定位服务器进程占用者。 | NetWare | |

| 查找磁盘空间占用者。 | NetWare | |

| 查看谁正在使用打开的文件。 | Linux | |

| 监控服务器进程。 | | |

当你在服务器上安装并加载了其他产品和实用程序时，你可以通过 NRM 执行附加任务：

- 管理和监控 Novell Cluster Services™

- 监控 IPP 打印服务健康

- 管理 IP 地址

- 监控 Novell 许可证 (NetWare)

## 共存与兼容性问题

以下提供了关于 Linux 或 NetWare 版本的 NRM 与包含 NetWare 或 Linux 平台的现有网络的兼容性和共存性信息：

- 所有 NRM 管理功能在 NetWare 操作系统上均可用，组监控操作除外。

当你创建一个组时，可以从运行 NetWare 6.0 或更高版本的 NetWare 服务器获取服务器健康状态，也可以从运行 Novell OES 的 Linux 服务器获取。

- 你只能在安装了 OES 服务的服务器上访问 Linux 版 NRM。

- OES 包含的 NRM 版本只能运行在 NetWare 6.5 SP3 服务器上。

- 未运行 `owcimod` 模块或未运行 NetWare 6 或 6.5 的 Linux 服务器只能报告 Up/Down（开启/关闭）状态。

- 下表总结了 NetWare 版 NRM 与各种操作系统的兼容性：

| 表 3-7 | 监控类型 | 操作系统 | 兼容版本 |

| --- | --- | --- | --- |

| | Ping | 任意 | 不适用 |

| | NRM | NetWare | - NetWare  OES - NetWare 6.5 SP3 |

| NRM | Linux | - SUSE® LINUX  OES 可获取完整健康状态 - SUSE LINUX Enterprise Server 9 SP1 只能获取 Up/Down 状态 |

## 如何在 OES NetWare 上使用 NRM

`NRM` (`portal.nlm`) 提供了 NetWare 上 Monitor 的所有功能，以及服务器控制台上可用其他实用程序的一些功能；然而，NRM 通过 Web 浏览器提供了这些功能。

要在 OES NetWare 上使用 NRM，你需要熟悉以下内容：

- NRM 优势

- OES NetWare 服务器上的管理任务

- OES SP1 和 SP2 中 NetWare 6.5 版 NRM 的新特性

- 系统要求

- 如何登录 NetWare 版 NRM

- 如何退出 NetWare 版 NRM

## 集成 Linux 版本的 Novell Open Enterprise Server

- 重启 NRM 或 HTTP 接口

- 访问并管理其他 NetWare 服务器

- OES NetWare 上的 NRM 局限性

![](img/1dca8e8a8784dadffa032dcfe0460e55_223_0.png)

有关 OES NetWare 上的 NRM 的完整信息，请参阅《Novell NetWare 远程管理指南》(`remotemgr.pdf`)。

你可以从 `http://www.novell.com/documentation/` 或从 3077 课程 CD 上的 `OES_Docs` 目录访问该指南。

## NRM 优势

在 OES NetWare 上使用 NRM 而非 Monitor 或 RConsole 进行服务器管理具有以下优势：

- 比其他管理工具更快速地访问信息。

- 默认安装在所有 NetWare 服务器上，且大多数操作不需要特殊配置。

- 不需要特殊的客户端。

- 提供图形化界面，使诊断信息更易理解、更易管理。

- 提供其他实用程序中未包含的功能。
