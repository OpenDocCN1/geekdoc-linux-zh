
iMonitor 在安装 OES Linux 时自动安装。由于它与 NRM 共享资源，必须在服务器上加载 `httpstkd` 守护进程才能访问 iMonitor。必须在运行级别 2 到 5 中启动 `novel-httpstkd` 守护进程来实现此。

安装后，使用网络中客户端计算机或服务器自身的 Web 浏览器访问 iMonitor。要从防火墙外的 Internet 连接访问 iMonitor，您将需要确保 TCP

通过防火墙开放端口 `8030` 指向您 Web 服务器的 IP 地址。端口 `8030` 是您访问 Web 管理界面的默认端口。如果您需要，可以更改此端口，只要不与 OES NetWare 服务器上的任何其他服务冲突即可。

要使用 iMonitor，您必须在 Linux 工作站上使用 Konqueror 或 Mozilla 等浏览器，或在 Windows 工作站上使用 Internet Explorer 或 Netscape Communicator。确保您的浏览器已启用 Java 或 JavaScript。

通过打开浏览器并输入服务器的域名或 IP 地址 (`8009`) 以及 iMonitor 端口 (`/nds`) 来直接访问 iMonitor。例如：`https://www.quills.com:8030/nds`

或 `https://192.168.1.100:8030/nds`

系统可能会提示您接受证书。在身份验证对话框中，输入具有此服务器管理权限的 eDirectory 完整用户名（开头带点）和密码，然后选择确定显示图 5.6 所示的屏幕。

## 图 5.6

显示 DSAgent 信息摘要的 iMonitor 主页。

![](img/7161dff7824fcf032c707a13fefe185d_151_0.png)

# 第 5 章：OES 管理工具

与 NRM 一样，您的 iMonitor 会话将保持开启，直到工作站上的所有浏览器窗口关闭。

## iMonitor 基础

iMonitor 的页面布局类似于 NRM 和 iManager。iMonitor 页面可能有四个框架：

- 头部——头部位于屏幕顶部。它提供了 eDirectory 树健康的信号灯（绿、黄、红）评估，此外还可以访问其他 iMonitor 工具和 iMonitor 配置。点击页头中的 NDS iMonitor 标题将带您进入关于 iMonitor 软件组件的描述页面。默认情况下，iMonitor 启动时始终显示 Agent 摘要页。
- 导航帧——导航帧位于屏幕左侧。它列出了分组组织的不同管理任务，您可以通过 iMonitor 执行这些任务。每个链接都会带您进入执行该任务的特定页面。
- 内容帧——内容帧占据屏幕中间右部分。当您在头部或导航帧中选择链接时，相应的信息将显示在内容帧中。
- （条件性）副本帧——需要时，副本帧将出现在 iMonitor 的左下角。当请求数据的存在另一个副本，或者当另一个副本对主内容帧中显示的信息有不同的视图时，就会发生这种情况。通过副本帧，您可以更改用于查看请求数据的副本。

您在 iMonitor 中看到的信息量和类型取决于您当前的 eDirectory 标识以及您当前正在使用的 DSAgent 版本。随着新版本 eDirectory 的发布，它们将不断更新以向 iMonitor 提供更多信息。因此，旧版本的 eDirectory 或 NDS 虽然仍可以通过 iMonitor 访问，但无法提供与 OES 提供的当前 eDirectory 版本同等详细程度。

## 运行模式

iMonitor 可以以两种模式之一运行。您不需要执行任何操作即可在两种模式之间进行切换；iMonitor 会自动处理。然而，理解这些模式对于正确解释 iMonitor 数据和导航 eDirectory 树至关重要。

- **直接模式**——当 iMonitor 在其运行的同一服务器上收集信息或执行操作时，使用直接模式。之前提到的以服务器为中心的 iMonitor 功能（包括 DSTrace、DSRepair 和后台调度程序）仅在直接模式下可用。直接模式允许您对所有 iMonitor 功能进行完全访问，并且比代理模式更快。
- **代理模式**——当 iMonitor 在其运行之外的服务器上收集或执行操作时，使用代理模式。代理模式使得从旧版本的 eDirectory 或 NDS 收集信息和统计成为可能。代理模式是 iMonitor 的默认方法，这意味着打开 iMonitor 后，如果被指示切换到不同服务器上的 iMonitor 实例，它将继续从指定的服务器运行，直到被显式指示切换。

iMonitor 根据浏览器提交的 URL 请求选择模式。如果 URL 包含服务器查询，iMonitor 将使用代理模式。如果不存在服务器查询，iMonitor 将使用直接模式对本地 DSAgent 执行查询。

# 配置 iMONITOR

iMonitor 的默认配置适用于大多数环境。然而，iMonitor 提供了一个配置文件 `/etc/ndsimon.conf`，允许您自定义 iMonitor。它允许您更改 iMonitor 的通用执行情况，还可以自定义特定的 iMonitor 功能。欲了解有关 iMonitor 的更多信息，请参阅 OES 在线文档。

此页特意留空

# 开放企业服务器基础

- 6 SUSE Linux 服务器管理
- 7 Novell eDirectory 管理
- 8 用户与网络安全
- 9 OES 集群服务
- 10 Identity Manager 捆绑版

此页特意留空

# SUSE Linux 管理

### 快速访问

- 有效管理 SLES 需要对……的知识。在 SLES 安装中，包含 GRUB 菜单配置选项的文件称为 `menu.1st`，位于此 GRUB 根分区内。
- `menu.1st` 文件包含计算机的启动配置列表。这些配置通常至少包含一个正常配置和一个安全模式配置。所有这些配置条目都包含对所用内核的引用以及任意数量
- 在您启动 SLES 服务器后，操作系统将进行初始化，后台服务（包括 OES 守护进程）将在服务器提供登录提示之前启动。作为管理员，了解您的 SLES 服务器为了进入可可用状态而遵循的过程对您至关重要。
- GRUB 采用双阶段加载器过程，其中 GRUB 本身的配置存储在本地文件系统的 `/boot/grub` 目录下。该目录被称为 GRUB 根分区，包含了 GRUB 引导加载程序使用的配置文件。在 SLES 安装中，包含 GRUB 菜单配置选项的文件称为 `menu.1st`，位于此 GRUB 根分区内。`menu.1st` 的示例如图 6.1 所示。
- 对 SLES 进行有效的故障排除应包含位于 `/var/log` 的日志文件。

# 第 6 章：SUSE Linux 管理

SLES 管理是一个广泛而复杂的话。本章将讨论核心服务器管理任务和重要的 OES 组件概念。具体而言，本章将涵盖系统启动过程、进程管理、系统日志和内核管理。

除了这里提到的管理概念外，还有许多您感兴趣的 Linux 主题。Novell 教育有几个针对 Linux 的程序，将提供更全面的 Linux 管理见解。欲了解 Novell SUSE 认证选项的更多信息，请访问 Novell 教育网站：`http://www.novell.com/education`。

## SLES 启动程序

在您启动 SLES 服务器后，操作系统将进行初始化，后台服务（包括 OES 守护进程）将在服务器提供登录提示之前启动。作为管理员，了解您的 SLES 服务器为了进入可用状态而遵循的过程对您至关重要。

## 引导程序配置

默认情况下，SLES 安装使用通用统一引导加载程序 `GRUB` 将 Linux 内核加载到内存中。`GRUB` 通过将加载程序写入计算机系统第一块硬盘的主记录 `MBR` 来执行此任务。在通电自检 `POST` 过程之后，`GRUB` 将初始化并能够加载相应的内核。

### SLES 启动过程

这些可能的内核参数在初始化过程中会被使用。这些内核参数对于适当的硬件初始化是必要的，并且可以根据 SLES 服务器的特定需求进行自定义。表 6.1 显示了常用的内核参数。

#### 图 6.1

示例 SLES9 菜单。第一个配置文件。

![](img/7161dff7824fcf032c707a13fefe185d_159_0.png)

#### 表 6.1

常用内核参数

| 参数 | 描述 |
|---|--- |
| `acpi=off` | 当此参数设置为 off 时，高级配置和电源接口 `ACPI` 系统被完全禁用。 |
| `acpi=oldboot` | 设置为 oldboot 会禁用大部分 ACPI 组件，但保留与启动相关的组件。 |
| `apm=off` | 禁用高级电源管理。 |
| `ide=nodma` | 禁用所有 IDE 控制器的 DMA 模式。 |
| `noapac` | 此参数指示内核不使用计算机的可编程中断控制器 `APIC`。 |
| `nosmp` | 禁用支持 SMP 的内核的多处理器处理能力。 |
| `splash=silent` | 使启动消息隐藏在 SLES 启动界面之后。 |
