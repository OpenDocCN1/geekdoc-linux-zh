
# 第 7 章 网络分析、故障排除与数据包嗅探

## 7.2 嗅探连接

![](img/33fc180c04c8f96c022bce6e62ae12fd_226_0.png)

## 普通网络分析器

在 SecurityFocus (www.securityfocus.com/tools/category/4) 上进行简单搜索即可发现安全嗅探器的多样性和数量。其中一些最著名的工具包括：

- Wireshark：Wireshark 是最好的嗅探器之一，作为一个免费的商业级图形界面（GUI）进行开发，它具有许多功能、良好的用户界面，可以解码超过 400 种协议，并正在积极开发和维护。它运行在基于 Unix 信息和计算（UNIX）的系统、Mac OS X 和 Windows 上。这是一个生产环境中极的嗅探器，可以在 www.wireshark.org 获取。
- WinDump：WinDump 是 tcpdump 的 Windows 版本，可以在 www.winpcap.org/windump 获取。它使用 WinPcap 库并运行在 Windows 95、98、ME、NT、2000 和 XP 上。
- Network General Sniffer：Network General Sniffer 是最流行的商业嗅探器之一。现在它是一套企业级网络捕获工具，在 www.networkgeneral.com 有完整的嗅探器产品线。

![](img/33fc180c04c8f96c022bce6e62ae12fd_226_1.png)

- Windows 2000 和 2003 Server Network Monitor：Windows 2000 Server 和 Windows 2003 Server 都有用于执行网络分析内置程序。它位于“管理工具”文件夹中，默认不安装；因此，必须从安装光盘添加。
- EtherPeek：EtherPeek 是由 WildPackets 开发的商业网络分析器。Windows 和 Mac 版本以及网络分析产品可以在 www.wildpackets.com 找到。
- Tcpdump：Tcpdump 是最老且最常用的网络嗅探器，由劳伦斯伯伯利国家实验室（LBNL）信息计算科学部门（ICSD）的网络研究小组（NRG）开发。它是一个命令行工具，运行在基于 UNIX 的系统上，在 www.tcpdump.org 积极开发和维护。
- Snoop：Snoop 是使用 Sun Solaris OS 开发命令行网络嗅探器。
- Snort：Snort 是一个使用网络嗅探的网络入侵检测系统（IDS），在 www.snort.org 积极开发和维护。更多信息请参阅《Nessus, Snort, & Ethical Power Tools: Customizing Open Source Security Applications》（Sygress Publishing: 1-59740-20-2）和《Snort Intrusion Detection and Prevention Toolkit》（Sygress, ISBN: 1597499097）。
- Dsniff：Dsniff 是一个非常流行的网络嗅探包。它是一系列程序集合，专门用于嗅探有趣的数据（例如密码）并促进嗅探过程（例如规避交换机）。它在 www.monkey.org/~dugs/dsn 积极维护。
- Ettercap：Ettercap 专为嗅探交换式网络设计。它具有数据包收集、操作系统指纹和字符注入等内置功能，运行在包括 Linux、Windows 和 Solaris 在内的多个平台上。它在 ettercap.sourceforge.org 积极维护。
- Analyzer：Analyzer 是一个用于 Windows 操作系统的免费嗅探器。它由都灵理工学院的 WinCap 和 WinDump 制作者积极开发，可以在 analyzer.polito.it 下载。
- Packetizer：Packetizer 是一个用于 Windows way系统的免费嗅探器，使用 Wireshark 的核心逻辑。它倾向于运行 Wireshark 当前发布版本或之前的版本。它由 Network Chemistry 在 www.network-chemistry.com/products/packetizer.php 积极维护。

![](img/33fc180c04c8f96c022bce6e62ae12fd_227_0.png)

- MacSniffer：MacSniffer 专为 Mac OS X 环境设计。它作为 tcpdump 的前端构建。该软件是共享软件，可以从 personalpages.tds/~/brian_hill/macsniffer.html 下载。

## 它是如何工作的？

本节提供了嗅探发生的概述，并提供了网络和协议如何工作的背景信息。然而，还有许多其他资源，包括最受欢迎且无疑是最好的资源之一 Richard Stevens 的《TCP/IP Illustrated, Vol. 1–3》。

## 解释以太网

以太网是用于计算机通信的最流行的标准。协议就像说某种特定的语言。以太网是围绕共享介质原理构建的，本地网段上的所有计算机都共享同一个通道。它被称为*广播*协议，因为它将数据发送到同一网络段上的所有其他计算机。这些信息被划分为可管理的单元块，称为数据包（packets）。

以太网地址也称为媒体访问控制（MAC）地址。MAC 地址是一个 48 位的数字，分为两部分：前 24 位识别供应商，后 24 位组成序列号。MAC 地址是唯一的，没有两台电脑具有相同的地址。然而，偶尔可能会发生制造错误，导致多个网卡具有相同的 MAC 地址。因此，大多数人会刻意更改 MAC 地址，这可以通过程序（`ifconfig`）实现。此外，某些适配器允许使用程序重新配置运行时地址。最后，通过正确的工具和技能，你可以将地址烧录到网卡中。

以下步骤允许你查看网卡的 MAC 地址：

- Windows 9x/ME：访问“开始|运行”并输入 `wincfg`。MAC 地址将显示为“适配器地址（Adapter Address）”。
- Windows NT、2000、XP：访问命令行并输入 `ipconfig /all`。MAC 地址将显示“物理地址（Physical Address）”。
- Linux 和 Solaris：在命令行执行 `ifconfig -a`。MAC 地址在 Linux 上显示为 HWaddr，在 Solaris 上显示为 ether。
- Macintosh OS X：在终端应用程序执行 `ifconfig -a`。MAC 地址将显示为 "Ether"。

你可以通过输入命令 `arp -a` 查看最近通信过的其他计算机的 MAC 地址。

> 注意：欺骗（Spoofing）是更改数据包信息（例如 IP 源地址、MAC 地址或电子邮件地址）的过程。这通常是为了伪装成另一个设备以利用信任关系或使攻击来源难以追踪。地址欺骗也用于 DoS 攻击（例如 Smurf 攻击），其中网络请求的返回地址被伪造成受害者的 IP 地址。

## 理解开放系统互连模型

国际标准组织（ISO）于 20 世纪 80 年代初开发了开放系统互连（OSI）模型，以描述网络协议和组件如何工作。它将网络功能划分为七层，每层代表一组相关的规范、功能和活动（见图 7.3）。虽然初看起来很复杂，但这些术语在网络、系统和开发中被广泛。

214 第 7 章 · 网络分析、故障排除、数据嗅探

### 图 7.3 对应 OSI 模型的七层。

![](img/33fc180c04c8f96c022bce6e62ae12fd_230_0.png)

注意

OSI 模型并不一定反映应用程序和系统的实际编写方式。事实上，某些安全工具利用协议实现上的差异，从计算机（包括其操作系统）以及可能安装的特定补丁和服务中提取信息。

“我们仍然在谈论七层模型，是因为它是一个便于讨论的模型，但这与任何现实世界的软件工程都完全没有关系。换句话说，它是一种讨论问题的方式，而不是实现它们的方式。这很重要。规范是讨论问题的基础，它们不是实现软件的基础。”

– Linus Torvalds，Linux 内核项目协调员，2005 年 9 月 29 日的一封电子邮件。

以下章节定义了 OSI 模型的七层。

## 第 1 层：物理层

OSI 模型的第一层是物理层，它规定了跨越传输介质（电缆或无线波）传输数据的电气和机械要求。它涉及在载体上发送和接收数据流，无论该载体使用的是电（电缆）、光（光纤）、无线电、红外还是激光（无线）信号。物理层规范包括：

- 电压变化
- 电压变化定时
- 数据速率
- 最大传输距离
- 传输介质的物理连接器（插头）
- 网络的拓扑结构或物理布局

物理层解决了许多复杂问题，包括数字信号与模拟信号、基带信号与宽带信号、数据是以同步还是异步方式传输，以及信号如何划分为通道（多路复用）。

设备在物理层运行处理信号（例如网卡上的收发器）、中继器、集线器以及连接电缆段的简单连接器。物理层处理的数据是 1（一）和 0（零）的位，这些位通过光脉冲或电电压变化表示，并由这些脉冲的状态（通常开启表示 1，关闭通常表示 0）决定。
