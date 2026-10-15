

## Windows+BSD+Linux 安装指南，v1.1

FreeBSD/OpenBSD 等系统，以及 M. Bach 所著的《UNIX 操作系统设计》（The Design of the UNIX Operating System）一书，涉及 UNIX SVR4 内部原理。

### 3.1.4 OpenBSD：

BSD 家族除了占主导地位的“老大哥”FreeBSD 之外，还包括 OpenBSD、NetBSD、BSD/OS 和 Darwin 操作系统。OpenBSD 是一个功能完备、多平台的类 UNIX 操作系统，基于 Berkeley Networking Release 2（Net/2）和 4.4BSD-Lite。OpenBSD 团队致力于实现所谓的“默认安全”（secure by default）状态。这意味着 OpenBSD 用户应当感到放心，他们新安装的机器不会受到入侵。这一“默认安全”目标是通过在安全方面采取主动姿态来实现的。FreeBSD 的发行版追求在最为恶劣的条件下保持稳定性和可靠性，而 OpenBSD 的发行版则追求企业环境中的最佳安全性。OpenBSD 操作系统软件被称为“主动安全的类 UNIX 操作系统”。OpenBSD 内核经过大量安全特性的深度优化，从而为客户提供最为安全、难以被黑客攻破的实时系统。OpenBSD 项目网站可访问：http://www.openbsd.org。

OpenBSD 操作系统软件已将强加密技术集成到基础系统中。它提供了功能完备的 IPsec（因特网协议安全）实现，并支持 SSL（安全套接层）和 SSH（安全外壳）等常见协议。网络过滤和监控工具，如数据包过滤、NAT（网络地址转换）和桥接，也一并包含在内。为了满足高性能需求，基础系统还增加了硬件加密支持。OpenBSD 尽可能提供多种安全选项，让用户能够享受安全的计算体验，而不会感到负担。

### 3.1.5 NetBSD：

NetBSD 内核注重清晰的设计和良好的架构方案。NetBSD 从单一源代码树支持极为广泛的硬件平台，包括在所有平台上同步发布，尽管缺乏媒体曝光和商业支持，它依然持续吸引着用户和经验丰富的开发者——这完全归功于对代码质量的重视。NetBSD 操作系统内核以“可移植性”为目标，力求在尽可能多的平台上运行。NetBSD 项目网站可访问：http://www.netbsd.org

- 若要浏览官方 FreeBSD 手册，请访问：http://www.freebsd.org
- FreeBSD 的官方源代码可通过匿名 FTP 获取：ftp://ftp.FreeBSD.org/pub/FreeBSD/
- 如需对 FreeBSD、Linux 与 Microsoft Windows 2000 进行对比研究，请查阅此文档：http://people.freebsd.org/~murray/bsd_flier.html

下表展示了本指南所涵盖的每个操作系统的主要“目标”：

|   |   |
|---|---|
| Windows | 去问盖茨先生本人吧……或许问问我们的钱包…… |
| Linux | Linux 的目标是新颖、激动人心且前沿的特性，如超线程（HyperThreading）、USB、无线网卡等。 |
| FreeBSD | FreeBSD 的目标是稳定性和健壮性；优化内核代码库，以便在繁重网络负载下获得最佳性能。 |
| OpenBSD | OpenBSD 的目标是最佳安全性。它是最主动安全的类 UNIX 操作系统。 |
| NetBSD | NetBSD 的目标是可移植性。在尽可能多的平台上运行是其首要目标。 |

### 3.2 安装 Microsoft Windows

我将 Microsoft Windows 操作系统作为计算机上的“第一”操作系统。我的计算机上安装了 MS Windows 98（SE）。读者可以从下面列出的任何一款 Microsoft 操作系统中进行选择。假设你也想将 Microsoft Windows 98（SE）作为你的第一个操作系统。那么请阅读 B 节：安装 MS Windows 98（SE）中的信息，并按照该节所述进行操作之后，再继续安装 FreeBSD 4.8-RELEASE、OpenBSD 3.2-RELEASE 或 NetBSD 1.6.1。

因此，我们有以下各节：

- A 节：安装 MS Windows 95
- B 节：安装 MS Windows 98（SE）
- C 节：安装 MS Windows Millennium（ME）
- D 节：安装 MS Windows NT（4.0）
- E 节：安装 MS Windows 2000（Professional）
- F 节：安装 MS Windows XP（Home/Professional）

可以使用 Windows 的 fdisk 和 format 工具来对一块新的未格式化硬盘进行分区。我假设读者拥有一块新的未格式化硬盘，并希望对其进行分区，然后格式化以安装 Microsoft Windows 操作系统。下面提到的内容适用于 Microsoft Windows 95、Microsoft Windows 98（SE）和 Microsoft Windows Millennium（ME）。如果你打算安装 Windows NT、Windows 2000 或 Windows XP，则可以跳过本节，直接转到对应 D、E 和 F 节的部分。

### A 节：安装 MS Windows 95

### B 节：安装 MS Windows 98（SE）

### C 节：安装 MS Windows Millennium（ME）

下面提到的内容适用于 Microsoft Windows 95、Microsoft Windows 98（SE）和 Microsoft Windows Millennium（ME）。因此，如果你要安装其中任何一个系统，请务必通读此处描述 Fdisk 和 Format 工具，并解释如何使用它们对硬盘进行分区或重新分区的所有内容。这些内容描述了以下主题：

- 如何使用 Fdisk 和 Format 工具
- 使用 Fdisk 和 Format 工具之前的重要注意事项
- 如何对主硬盘进行分区和格式化

在安装操作系统之前，你必须首先在计算机的硬盘（磁盘 1）上创建一个主分区，然后在该分区上格式化一个文件系统。Fdisk 工具是一个基于 MS-DOS 的工具，可用于准备（分区）硬盘。你可以使用 Fdisk 工具创建、更改、删除或显示硬盘上的当前分区，然后

