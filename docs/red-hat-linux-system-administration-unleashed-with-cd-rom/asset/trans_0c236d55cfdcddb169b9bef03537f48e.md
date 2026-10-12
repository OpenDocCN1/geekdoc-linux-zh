
AMDOpts 中，你可以指定任何你选择的传递给 amd 的选项。此变量的一个良好用途示例是指定 /etc/amd.conf 文件中使用的标签的值。例如，为了使前面 manual pages 的 amd.conf 文件条目生效，你需要将 AMDOpts 设置为 -Tarch=linux 的值。在为你的环境设置了这些变量的适当值后，你现在可以通过发出以下命令启动 automount 守护进程：

```
/etc/rc.d/init.d/amd start
```

## 在系统启动时启动 Automount 守护进程

唯一剩下的步骤是确保 automount 守护进程在启动时启动，通过从运行级别目录创建适当的链接来启动和停止 amd。请注意 amd 依赖于 NFS 处于活动状态，因此在尝试运行 automount 守护进程之前，必须确保 NFS 已先启动。相反，在关闭 NFS 之前，先关闭 automount 守护进程是明智的。你可以手动创建适当的符号链接，或者如果你愿意，可以使用控制面板的一部分的运行级别编辑器为你创建它们。

最后，在转向 Linux autofs 之前，让我们先看看前面提到过的 amq 实用程序。此实用程序是 am-utils 软件包的一部分，是 automounter 查询工具。它与 automount 守护进程通信，并且可以根据提供的命令行选项执行许多有用的功能。表 15.5 显示了一些更常用的选项及其作用。

表 15.5 amq 选项

| 选项 | 描述 |
|---|---|
| -f | 请求 automounter 刷新内部缓存。 |
| -m | 打印已挂载文件系统的列表以及每个文件的引用数。 |
| -p | 打印本地运行的 amd 的 pid。 |
| -s | 打印系统范围的挂载统计信息。 |
| -u directory | 尝试卸载指定的目录。 |

amq 实用程序还有其他选项，有关文档请参阅 amq 的手册页。

## Linux Autofs

Linux autofs 包含 Berkeley automount 守护进程的大多数功能；然而，它是在内核空间中实现，而不是像 automount 守护进程那样在用户空间中实现。这意味着必须将 autofs 的支持编译到你的内核中。此外，你必须安装 automount 实用程序，它们包含在 Red Hat 安装介质上的 am-utils-6.0 rpm 软件包中。

假设你已将 autofs 支持编译到内核中并安装了适当的 am-utils 软件包，你可以开始配置 autofs 的任务。autofs 使用的配置文件没有 amd 的那么复杂，但有些相似。首先要考虑的配置文件是 /etc/auto.master 文件，即主配置文件。该文件由每个条目包含三个字段组成。第一个字段指定用于在映射文件中指定的文件系统的目录根，映射文件的名称在第二个字段中给出，而第三个字段指定的超时值用于确定何时卸载自动挂载的文件系统。下面是 Red Hat 附带的默认 auto.master 文件：

```
/etc/auto.master

# $Id: 755915.txt,v 1.7 1999/09/23 05:35:36 tschenk Exp $
# Sample auto.master file
# Format of this file:
# mountpoint map options
# For details of the format look at autofs(8).
/misc    /etc/auto.misc    --timeout 60
```

该文件指定将使用 /misc 作为挂载根目录，用于 /etc/auto.misc 中定义的文件系统，并且挂载在 60 秒不活动后超时。下面是随 Red Hat Linux 提供的 auto.misc 文件：

```
/etc/auto.misc

# $Id: 755915.txt,v 1.7 1999/09/23 05:35:36 tschenk Exp $
# This is an automounter map and it has the following format
# key [ -mount-options-separated-by-comma ] location
# Details may be found in the autofs(5) manpage

kernel    -ro,soft,intr    ftp.kernel.org:/pub/linux
cd        -fstype=iso9660,ro    :/dev/cdrom

# the following entries are samples to pique your imagination
#floppy    -fstype=auto    :/dev/fd0
#floppy    -fstype=ext2    :/dev/fd0
#ezfloppy  -fstype=ext2    :/dev/fd0
#jaz       -fstype=ext2    :/dev/sdc1
```

这些映射中的条目由三个字段组成，其中第一个称为 key。此 key 通常也是你将访问的子目录的名称，以使第三个字段中指定的设备或文件系统被挂载。正如你可能猜到的那样，第二个字段是要传递给 mount 程序的以逗号分隔的选项列表。具体来说，key 为 kernel 的行指定，如果用户尝试访问目录 /misc/kernel，automounter 将尝试以只读方式将由 ftp.kernel.org:/pub/linux 指定的 NFS 文件系统挂载到本地挂载点 /misc/kernel 上。下一行指定对 /misc/cd 的访问尝试将导致 automount 程序将本地设备 /dev/cdrom 以文件系统类型 iso9660 且只读访问的方式挂载。文件中的其余行是注释，但它们演示了如何使用 automounter 允许用户仅通过访问特定目录即可在没有 root 访问权限的情况下自动挂载可移动设备，例如软盘驱动器和 JAZ 驱动器。

假设条目如上所示，你可以通过运行位于 /etc/rc.d/init.d/autofs 的 autofs 脚本并使用 start 选项来激活 autofs 支持。完成此操作后，你现在可以像任何用户一样轻松访问 CD-ROM 驱动器和软盘驱动器。这里所示设置中唯一出现的问题是超时值相当长。/etc/auto.misc 中定义的所有文件系统指定的超时值为 60 秒。这意味着如果你将 CD-ROM 放入驱动器并 cd 到 /misc/cd，你必须 cd 离开此目录并等待 60 秒后才能卸载 CD-ROM。除非你有能力以 root 用户身份向 automount 程序发送信号。使用 sudo 的功能，你可以使用 killall 程序向 automount 程序发送 USR1 信号，这将导致它尝试立即卸载其已挂载的所有文件系统。

## 摘要

本章首先讨论了在网络上共享资源的一些原因，以及最常共享的两种资源是文件和打印机服务。它研究了如何使用 Red Hat 下的工具设置打印队列，如何向网络上的其他人授予打印机访问权限，以及如何从客户端系统访问这些共享打印机资源。然后它继续介绍 NFS 服务器和客户端的设置和配置，使用 Linux 内核 NFS 支持。本章还简要介绍了 Linux 下可用的两种替代网络文件系统 AFS 和 Coda，两者都是分布式文件系统，具有其他文件系统类型中没有的许多有趣功能。最后，它介绍了 Berkeley automount 守护进程，以及 Linux autofs 功能，这些功能使网络文件系统的管理变得更容易，并通过让用户在不授予 root 访问权限的情况下访问本地可移动媒体（如软盘、CD-ROM 驱动器和 JAZ 驱动器）来增强用户能力。

## 网络监控

### 本章内容

- 为何监控？ 436
- 监控系统 437
- 嗅探器 444
- 流量分析器 451

Linux 操作系统以其高度的网络集成而广为人知。Red Hat Linux 发行版开箱即用即提供完整的网络支持，包括文件、邮件和 Web 服务器等软件。然而，这种高水平的网络可用性是有代价的。联网服务器将自己暴露给外部世界，大大增加了系统攻击成功的可能性。此外，联网计算机系统可能难以正确配置。配置错误可能导致网络瓶颈、服务中断和各种其他问题。由于网络集成在 Linux 操作系统如此基础的层面上，因此诊断此类问题有时会非常困难。

网络监控允许你深入了解主机之间的低级事务。这样的功能对于计划管理联网 Linux 主机的任何个人来说都极其宝贵。本章介绍了网络监控软件和部署技术。你将了解执行网络监控的好处，如何执行此类活动，以及如何使用网络嗅探器和流量分析器。

### 为何监控？

当今的网络是复杂且动态的实体，容纳了多种不同类型的计算机系统和嵌入式电子设备。妥善管理这些不同的网络资源，确保良好的数据传输性能水平，并在联网设备之间保持良好的安全水平，可能是一项相当大的任务。使用一种称为网络监控的技术，管理员可以获得对其计算机网络活动的“内部视图”，以便快速、正确地诊断问题、全面审计安全问题并修复传输瓶颈。

*网络监控是从网络适配器设备捕获和检查原始数据包的过程。它绕过了监控计算机的协议栈，直接执行所有捕获和分析活动。数据包在进行任何形式的包验证或校验之前直接从线路上抓取。这允许监控软件执行各种活动，例如损坏的数据包检测、网络配置错误问题诊断等等。如果数据包在到达监控软件之前被允许通过监控系统的网络栈和数据包验证程序，这些事情是不可能完成的。*

监控还提供了宝贵的优势，即允许你检查网络上所有主机之间流动的数据流量，而不仅仅是专门发往执行监控活动的主机的流量。这是通过在监控系统的网络接口设备上启用一个称为 *promiscuous mode* 的功能来实现的。此功能允许网络设备看到穿越网络线路的所有流量。诸如网络瓶颈和 IP 地址冲突等问题只能
