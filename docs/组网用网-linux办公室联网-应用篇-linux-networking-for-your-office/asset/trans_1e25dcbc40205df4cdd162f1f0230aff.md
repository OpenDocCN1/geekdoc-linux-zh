

NetBIOS 被 Windows for Workgroups 3.1、Windows 95、Windows 98、Windows NT、Windows 2000 以及 OS/2 使用。DOS 上也有 NetBIOS 工具可用。因此在 PC 世界中相当常见，尽管它越来越多地被用作 TCP/IP 之上的一个层。

## AppleTalk

像 Novell、IBM 和 Microsoft 一样，在互联网尚未渗透到大多数企业之前，Apple 也开发了自己的网络协议。Apple 将这些协议称为 AppleTalk，最初该术语既指网络协议，也指传输它们的硬件。然而，最终很明显，这种对 AppleTalk 术语的双重使用令人困惑，因此 Apple 开始仅将该术语用于指代网络协议。硬件随后被称为 LocalTalk。Apple 在其直到 1998 年生产的绝大多数计算机中都包含了 LocalTalk 硬件。

然而，即使在 1998 年之前，Apple 也在其计算机中包含了以太网，并且可以使用以太网作为 AppleTalk 的底层硬件。以这种方式使用时（有时称为 EtherTalk），AppleTalk 直接与以太网硬件通信。自 MacOS 7.5.2 起，Mac 也能够使用 TCP/IP 传输 AppleTalk。这种能力来自 Mac Open Transport 系统扩展，其结果是 AppleTalk 网络速度大幅提升。在许多方面，这两种传输 AppleTalk 的方法与 NetBIOS 和 NetBIOS over TCP/IP 相似，尽管细节差异很大，并且 Windows 和 Mac 协议彼此不兼容。

另一方面，Linux 与 NetBIOS 和 AppleTalk 兼容（或可以使其兼容）。要在 Linux 中使用 AppleTalk，您需要安装 Netatalk 包，它支持原始 AppleTalk。Netatalk 已被修改为可与 Open Transport 风格的 AppleTalk over TCP/IP 一起工作，该修改后的包被称为 Netatalk+asun，以补丁的主要创建者兼 Netatalk 当前维护者 Adrian Sun 命名。这些 Netatalk 包在 Linux 中提供 AppleTalk 文件服务器支持，但不提供客户端支持。如果您希望 Linux 计算机作为 AppleTalk 文件共享客户端运行，您需要使用 afpfs 包，该包目前处于 alpha 级别，因此不可靠。Netatalk 确实包含软件，可让 Linux 共享通过 AppleTalk 网络连接的打印机。

与 NetBIOS/NetBEUI 一样，AppleTalk 将网络划分为组（在 AppleTalk 中称为区域）和单台计算机。AppleTalk 协议包括一种自动为每台计算机分配唯一标识符的方法，因此您无需担心 IP 地址或其等价物，除非使用 AppleTalk over TCP/IP。计算机的 AppleTalk 名称与其 Internet 名称可能几乎没有相似之处，尽管与 NetBIOS 一样，出于简单起见，您可能希望将两者同步。

AppleTalk 在 Macintosh 网络之外并未流行起来，因此您很可能只有在想要为一台或多台 Mac 提供文件或打印服务时才需要使用 Netatalk。BeOS 确实用 AppleTalk 进行网络打印，因此您可能希望安装 Netatalk 以与 BeOS 计算机共享打印机。

## 混合协议

通常，可以在一台计算机或同一网络介质上混合使用两种或多种网络协议。例如，您可以在同一根以太网电缆上运行原始 NetBIOS、原始 AppleTalk 和 TCP/IP。然而，有时 Windows 计算机如果可用的选项太多会感到困惑。例如，在 Windows 中安装冗余网络协议有时会导致它无法看到 Linux Samba 服务器。因此，最好在任何给定网络上坚持使用尽可能少的协议。特别是，您应该使用 NetBIOS over TCP/IP 而不是原始 NetBIOS。将 Linux 配置为理解未使用的协议通常不会造成问题，但会消耗您可能更愿意用于其他功能的内存。

当然，在同一网络上使用 TCP/IP 堆栈更高层的多个协议并没有什么问题。例如，您可以在同一网络上运行 Web 服务器、NFS 服务器、Samba 服务器和邮件服务器，甚至可以从同一台计算机运行。您也可以在运行服务器的同一台计算机上混合使用 TCP/IP 客户端，并使用 Netscape 浏览网页，使用 Samba 打印到 Windows 主机打印机，并使用 ftp 下载文件。在一台计算机上运行如此多网络程序的主要危险是，您可能会产生如此多的进出该计算机的流量，以至于压倒您的网络硬件。大量网络流量并不是本身运行多个网络堆栈的结果，而是传输大量数据的结果。如果在运行 Netatalk、Samba 和 NFS 服务器时网络变慢，将机器从一种协议转换为另一种协议可能不会有所帮助。

如果发现网络变慢，您应该要么升级到更快的网络，要么使用路由器将网络划分为两个或多个段，并尽可能隔离这些段。如果您的网络很复杂，并且不确定在哪里分割，您可能希望查看网络诊断工具。Linux 发行版附带了一些此类工具，例如 netstat 命令，它列出打开的连接。您还可以找到其他工具，例如 netwatch，它提供网络段流量的实时显示。

## 总结

TCP/IP 堆栈是描述 Linux 或任何其他使用 TCP/IP 进行网络的 OS 中网络功能的一种方式。堆栈将网络操作分为四层，任何网络程序都在堆栈中的一层上运行。我们作为终端用户和网络管理员最感兴趣的程序工作在应用层，但其他层同样重要。

