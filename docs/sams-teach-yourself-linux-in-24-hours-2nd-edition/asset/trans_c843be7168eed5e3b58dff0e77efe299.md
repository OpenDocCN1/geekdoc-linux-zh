
![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_244_0.png)

## 第10小时
### 连接到互联网

在本小时中，您将学习如何使用称为 PPP 的串行线路点对点协议设置 Linux 系统以连接到互联网。连接到互联网是许多新 OpenLinux 用户在安装 OpenLinux、配置 OpenLinux 与计算机声卡配合使用以及配置 X Window 系统与计算机显卡配合使用后面临的最大障碍之一。按照本课的说明操作后，您可以通过互联网服务提供商（ISP）连接到互联网，并进行电子邮件、网页浏览和文件传输。

本小时向您展示如何以最简单、最基本的方式手动连接到您的 ISP。我还将为您指明信息来源，以便您进行故障排除或微调连接。然后您将学习如何使用两个易于使用的图形界面程序 kppp 和 xisp 来设置、启动和停止您的 PPP 连接。

我推荐您使用 PPP 连接，原因如下：

- 虽然它很复杂，但设置起来很容易。
- 您可以在多份 HOWTO 文档中找到有关该协议的文档和详细信息。
- 您可以在 comp.protocols.ppp 新闻组中阅读有关 PPP 的内容，并在 comp.os.linux.networking 新闻组中获取特定于 Linux 的信息。
- 它在连接的两端都提供安全性。
- 它是一种通用协议，几乎所有 ISP 都支持。
- OpenLinux 附带了多个可用于设置 PPP 连接的程序。
- 它足够灵活，可以适应不同类型的连接。

本小时首先列出 OpenLinux 的一些硬件和软件先决条件，然后询问您需要从 ISP 处获取的一些必要信息。使用这些信息，您首先将创建一个自定义脚本集，可用于手动启动或停止连接。然后我将向您展示如何使用两个图形界面程序设置 PPP 连接：用于 K 桌面环境的 kppp 客户端和用于 X11 的 xisp 图形界面客户端。

您还将了解一些方便的实用程序，可用于诊断连接，以及一些可用于监控会话的其他程序。

### 您需要的硬件

您可能已经拥有所需的所有硬件：调制解调器、如果调制解调器是外置的则需要调制解调器电缆，以及电话线。但是，您必须拥有可与 OpenLinux 一起使用的调制解调器。您不能使用以下任何调制解调器与 OpenLinux：

- 3Com/U.S. Robotics 56K V.90 Winmodem
- 3Com/U.S. Robotics 56K Winmodem PC Card
- 3Com/U.S. Robotics Sportster 33.6 Winmodem
- Aztech Systems 56K PCI modem
- Cardinal 56K Windows Fax modem
- Diamond SupraMax 56K ISA/PCI modems
- Hayes 56K Accura V.90 PCI Win modem
- Motorola FM56 ISA/PCI modems
- Mwave adapters (but might work as sound card)
- Viking Components 56K ISA Windows modem
- WinStorm 56K PCI Data/Fax Speaker phone modem
- Zoltrix Phantom/Spirit 56K modems
- Any other modem requiring Windows-only software

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_246_0.png)

> 如果您计划购买调制解调器用于 OpenLinux，请不要购买任何被视为 winmodem 的调制解调器。这些无用的垃圾最近由制造商引入计算机行业，以节省资金并增加硬件生产的利润。Winmodems 使用的芯片比“真正的”调制解调器少，并且依赖于特定于操作系统的软件驱动程序（以及计算机的 CPU）才能工作。不幸的是，许多计算机制造商（尤其是制造和销售笔记本电脑的制造商）不会告诉您提供的或内置调制解调器无法在 Windows 以外的任何操作系统上工作。注意！如果您不确定要购买什么调制解调器，请购买可与任何操作系统配合使用的外置调制解调器，而不仅仅是 Windows。

OpenLinux 的一大优点是它即使在较旧的计算机上也能很好地运行。虽然图形密集型应用程序（如 X）会占用较旧、较慢 PC 的性能，但您不需要 X11、华丽的显示监视器或 16MB VRAM 加速的 3D 显卡即可使用 PPP。然而，您确实需要一个工作的串行端口和调制解调器。

如果您能够在 Linux 下使用调制解调器拨号并使用 minicom 程序或 C-Kermit 连接，那么您很可能不会遇到任何问题。如果您使用的是带有 PC 卡调制解调器的笔记本电脑，并且 cardmgr PCMCIA 设备管理器识别并初始化了您的调制解调器，您应该没问题，因为在启动 OpenLinux 时，任何已识别的卡都会被识别并列出。

检查串行端口识别的一种方法是使用 dmesg 程序，该程序显示启动 OpenLinux 时显示的启动消息。运行 dmesg 程序（通过 less 命令管道传输），并查找输出中描述串行端口的行，类似于以下内容：

```
# dmesg | less
...
ttyS0 at 0x03f8 (irq = 4) is a 16550A
ttyS1 at 0x02f8 (irq = 5) is a 16550A
ttyS3 at 0x02e8 (irq = 3) is a 16550A
...
```

使用 dmesg 很方便，特别是当启动消息滚动得太快而无法阅读时。这些行显示使用设备 ttyS0、ttyS1 和 ttyS3 找到了三个串行端口。另一个需要考虑的是调制解调器的速度。您可能还记得 2400 或 9600 波特调制解调器曾是触音拨号以来最伟大的创新。如果您仍在使用较旧的调制解调器，并且在型号价格下降之前拒绝升级到更新的 V.90 调制解调器，您仍然可以使用 PPP 连接到互联网；大多数旧调制解调器会自动与 ISP 调制解调器组中的更新型号同步。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_247_0.png)

> 想减少与 ISP 连接时出现问题的几率吗？了解您的 ISP 使用什么调制解调器，并为您的计算机系统购买相同型号。

如果您想收听广播电台、观看实时视频或通过电话连接升级您的 Red Hat Linux 系统，您想要的是您能负担得起的最快的调制解调器和互联网连接。虽然我不建议您尝试通过 1200 或（战栗）300 波特连接完成任何工作（这接近于自虐，但可以做到，正如 ATM 机所证明的那样），您可以在 9600 速度下使用电子邮件、FTP 和纯文本网页浏览。

由您决定，而且，OpenLinux 不就是关于自由选择吗？

### 您需要的 Linux 软件

为了设置您的 PPP 连接，您需要确保您的 Linux 内核支持 PPP。您可能已将 PPP 支持编译到内核中，或在启动 Linux 时作为模块加载。检查系统是否存在 PPP 支持的方法之一是再次使用 dmesg：

```
# dmesg | less
...
PPP: version 2.2.0 (dynamic channel allocation)
TCP compression code copyright 1989 Regents of the University of
California
PPP Dynamic channel allocation code copyright 1995 Caldera, Inc.
PPP line discipline registered.
...
```

您会看到类似的行。

> 默认情况下，OpenLinux 通过可加载的 Linux 内核模块加载 PPP 支持。如果您看不到 PPP，您必须重新编译内核以内置 PPP 支持，构建 PPP 模块并使用 insmod 命令加载驱动程序，或确保在 OpenLinux 安装期间选择了正确的 Linux 内核（其文件名中包含“modular”一词）。您还需要启用网络支持，尤其是 TCP/IP。有关详细信息，请参阅第 2 小时，“安装 Linux”。

您还需要 chat 程序，该程序位于 /usr/sbin 目录下，是 pppd 守护进程软件包的一部分。chat 程序在拨号过程中用于拨号并连接到 ISP 的调制解调器。除 chat 外，您还需要 pppd 守护进程，也安装在 /usr/sbin 目录中。如果安装了 pppd，您可以在 /etc 目录下找到一个 ppp 目录，其中包含以下文件中的一些或全部：

```
# ls /etc/ppp
chap-secrets   options        ppp-on-dialer
connect-errors pap-secrets    ppp-on
ip-up          ppp-off
```

如果您看不到 ppp-on 或 ppp-on-dialer 文件，您可以从 /usr/doc/ppp-2.2.0f 目录复制它们。

本小时中您学习到的第一个设置要求您对 ppp-on 文件进行更改，该文件是一个可执行脚本。接下来，您可能想检查 /etc 目录下是否存在 resolv.conf 文件。如果不存在，不用担心；这是一个包含一两行的简短文件，我会向您展示在文件中输入的内容。

最后，您可能想查看系统上是否有 ifconfig、minicom、netstat、ping 和 route 命令。您将在本章后面使用它们对连接进行一些测试。

> 需要查找命令吗？尝试使用 whereis 或 locate 命令，如下所示： whereis ifconfig 以查看 ifconfig 命令在系统上的位置，或 locate ifconfig 以打印使用 ifconfig 的任何文件或目录的列表。
