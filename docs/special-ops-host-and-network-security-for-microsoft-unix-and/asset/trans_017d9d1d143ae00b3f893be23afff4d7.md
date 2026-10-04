

# 第 9 章 攻击与防御微软终端服务 (Terminal Services)

在客户端确认更新后的 ActiveX 控制下载对话框后，远程桌面连接将自动在该端口上建立连接。
提醒一点：如果你正在使用 TSAC，我不建议在与终端服务器相同的系统上运行 IIS Web 服务器。出于安全考虑，将应用程序隔离在不同的服务器上是一项良好的实践。

> 注意：
> 默认情况下，Windows 2000 的 TSAC 组件不提供更改连接端口的功能——它被硬编码为 3389。然而，通过一个简单的破解（hack），你可以配置它连接到备用的 TCP 端口。如果你将 TSWeb 目录从 Windows XP 服务器复制到你的 Windows 2000 服务器上，它将允许像 XP 一样更改 TCP 连接端口。

## MMC 嵌入程序 (Snap-in)

微软在 Microsoft 管理控制台 (MMC) 中包含了一个嵌入程序，以便在一个地方管理多个终端服务器。MMC 嵌入程序的组成组件如下：

- 一个 Mtsmmc.dll
- 一个名为 Tsmmmc.msc 的控制文件

此 MMC 嵌入程序的问题是，它没有机制让用户指定备用连接端口。只有留在默认端口 3389 的终端服务器才能通过此工具直接访问。
尽管有此缺陷，如果你在一天中通常需要连接到许多服务器，此工具将非常有用——只需点击每个连接即可直接进入控制台。图 9.8 显示了添加到 MMC 的两个服务器。

## 使用 Rdesktop Linux 客户端

Rdesktop 是一个 Windows 终端服务的开源客户端。它能够原生使用 RDP 协议以完成此任务。Rdesktop 目前运行在大多数带有 X Window 系统的 Unix 平台上。

![](img/729efc56f204a2ebffb8295c3a2dfdfb_486_0.png)

Rdesktop 由 Matt Chapman 编写，根据 GNU 通用许可证 (GPL) 免费提供。可以从 www.rdesktop.org 下载 rdesktop 源代码。在你的平台上运行 `make` 来编译源码以获取可执行文件。也可以从 www.sourceforge.com 下载预编译的 Linux 二进制文件。

图 9.9 显示了 Rdesktop 启动连接。

## 图 9.9 使用 Rdesktop 客户端连接

![](img/729efc56f204a2ebffb8295c3a2dfdfb_487_1.png)

一旦指定了服务器，应用程序将通过 TCP 3389 连接，就像远程桌面连接客户端一样（见图 9.10）。

www.synergy.com

## 图 9.10 Rdesktop 连接运行状态

![](img/729efc56f204a2ebffb8295c3a2dfdfb_488_0.png)

## Macintosh 客户端

甚至还有一个 Mac 的远程桌面连接客户端。你可以从 www.microsoft.com/mac/DOWNLOAD/MISC/RDC.asp 下载客户端和详细信息。

## 使用终端服务器工具

根据你的需求，有很多工具可以管理和保护网络中的终端服务器。有些仅在 TS 会话中运行，有些是命令行应用程序，有些是 GUI 应用程序。本节将讨论以下类别：

- Windows 2000 终端服务器命令
- 使用 TScmd.exe
- 终端服务器管理器 (Terminal Server Manager)
- 终端服务器配置
- 终端服务器组策略

## 使用 Windows 2000 终端服务器命令

微软提供了许多命令行工具，在终端服务器会话中非常有用。以下列出了微软提供的一些侧重于安全的命令行工具。每个工具都有多种用途；你应该尝试所有工具，以找到哪种最适合你。其中许多工具存在于 Windows XP 和 Windows Server 2003 中：

- Qinsta.exe (查询会话) 这有助于了解他们的会话是如何连接的，并且在你由于某种原因需要使用 Shadow（影子）功能“监视”时有用。它还可以使用 `/server:server_ip` 指令监控其他终端服务器。图 9.11 显示了 Query Session 命令。

## 图 9.11 Query Session 命令示例

![](img/729efc56f204a2ebffb8295c3a2dfdfb_489_0.png)

- Shadow：这允许你从 TS 会话监控并控制其他用户会话。执行此操作的能力取决于优先级最高的设置。Require Users Permission（需要用户权限）”设置也是如此，该设置决定了是否会询问用户许可以允许影子。一个有趣的事实是，Windows 2000 无法影子控制台，但在 Windows XP 和 Windows Server 2003 上可以影子并控制。

- Query termserver：此命令只能在 TS 会话中使用。它对于攻击者和管理员查找当前域内的其他终端服务器很有用。

- TSDiscon：此命令允许你在不注销用户的情况下断开会话。如果你需要清除会话或防止用户占用插槽，这将非常。

- TSKill：此命令用于强制用户注销系统。当用户会话挂起或需要立即终止时非常有用。

- Queryinsta：此命令可显示终端服务器上所有会话的信息。它对于识别哪些用户当前登录有用。

- Userinsta：此命令允许你通过 ID 查询特定会话的信息。这对于排查特定用户的问题可能有用。

- Shadowinsta：此命令允许你影子特定的会话。这对于实时监控用户正在做什么有用。

- Disinsta：此命令允许你断开特定的会话。这对于从系统中移除用户有用。

- Killinsta：此命令允许你杀死特定的会话。这对于终止不再响应的会话有用。

## 图 9.8 MMC 嵌入程序查看多个服务器

![](img/729efc56f204a2ebffb8295c3a2dfdfb_487_0.png)

