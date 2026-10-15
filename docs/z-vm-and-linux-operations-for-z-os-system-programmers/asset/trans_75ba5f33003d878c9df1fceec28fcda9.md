

## 2.5.3 其他帮助选项

另外五个选项会影响帮助显示：SCREEN、NOSCREEN、TYPE、NOTYPE 和 EXTEND。这些选项控制文件和错误消息的显示以及命令的搜索顺序。有关这些选项的完整描述，请参阅 z/VM: CMS Commands and Utilities Reference，SC24-6073。

## 2.5.4 获取帮助的其他方式

您也可以直接获取特定命令的帮助，而无需经过我们讨论的各种帮助导航形式。如果您知道想要帮助的命令，或想直接导航到该命令，请指定命令类型为：

Help CP MENU    显示可用的 CP 命令的完整菜单。
Help CP command    显示指定 CP 命令的格式。

Figure 2-9 Output of help cms erase (related

## 2.5.7 退出帮助系统

要在 CMS 中随时退出帮助系统，请使用 PF3 或在命令行输入 quit。这两种操作都会带您返回到之前的视图。请注意，如果您已深入帮助菜单层级并希望逐级返回，可能需要多次发出 quit 命令。

作为替代方案，您可以使用 PF4 通过一次按键完全离开帮助系统。

> z/OS 类比：z/VM 中导航 HELP 菜单与 z/OS 中导航 ISPF HELP 菜单类似。

## 2.6 z/VM 中的网络选项

System z 品牌提供许多解决方案来改善您的网络连接。关于网络的一些关键方面是 System z 和 z/VM 上实现的功能，即 OSA 适配器、HiperSocket 和 VSWITCH。

### 2.6.1 OSA 适配器

Open Systems Adapter（OSA）是一种网络控制器，可安装在大型机 I/O 机箱中。该适配器集成了多个硬件功能并支持多种网络传输协议，包括快速以太网、千兆以太网、10 千兆以太网、异步传输模式（ATM）和令牌环。

有多个版本的 OSA 可用：OSA-Express、OSA-Express2 和 OSA-Express3。每个版本的功能略有不同。较旧的 OSA-2 卡已被更新的 OSA-Express 和 OSA-Express2 卡取代且不再提供，但许多旧大型机仍在使用它们。

z/VM 系统或其任何客户操作系统可以通过直接将特定的 OSA 地址专用于该系统来提供网络连接。这可以通过用户目录中的 DEDICATE 语句完成，或通过将设备附加到客户用户 ID。

### 2.6.2 HiperSockets

HiperSockets 技术可用于 System z 服务器。HiperSockets 是一种集成的任意到任意虚拟 TCP/IP 网络，可在多个 LPAR 或 z/VM 客户机之间提供互连。通过 HiperSockets，您可以连接在同一 System z 上运行的任何服务器，并由于低延迟而改善响应时间。

HiperSockets 是为通过内存总线提供高度可用、高速网络连接而开发的。它可用于应用程序或基础设施场景，其中网络因在同一 System z 服务器上运行的服务器之间交换大量数据而承受压力。它还提供更高的安全性，因为数据包不会离开主机，因此无法在 LAN 上被嗅探。

Figure 2-10 on page 46 显示了在应用程序服务器场景中 HiperSockets 的一种可能实现。当您使用 Linux for System z 技术来构建应用程序环境时，通常会计划采用三层架构：

- ► 前端层是 HTTP 服务器。
- ► 中间层是应用程序服务器。
- ► 后端层是数据库服务器。

采用建议的架构后，环境可以规划为：

- ► 在 Linux for System z 下的 IBM HTTP Server（由 Apache 提供支持）
- ► 在 Linux for System z 下的 IBM WebSphere Application Server
- ► 在 z/OS 下的 DB2® 服务器

如果浏览器通过网络启动会话，则三层之间会开始通信。为避免网络流量，实现 HiperSockets 解决方案可以提供帮助。借助 HiperSockets 提供的优势，层与层之间的网络流量将在 System z 服务器中以内存速度交换。

