
# 附录 E：调制解调器与终端

## 终端与多端口串口卡

前面的章节展示了如何设置和使用调制解调器进行拨出。本附录的其余部分简要介绍了连接到 PC 串口端口的终端设置步骤。你还将找到 Linux 支持的多端口串口卡列表。
你可以通过阅读在线的 Text-Terminal-HOWTO 了解更多关于将终端连接到 Linux 系统的信息，该文档位于 http://tldp.org/HOWTO/Text-Terminal-HOWTO.html。

> 注意，你可能想使用其他 x86 PC（可能是较旧的奔腾 PC）作为连接到你 Linux 系统的终端。要将 PC 转换为终端，你只需要 PC 拥有一个串口通信包，如 Procomm Plus 或 Telix。

## 在串口端口上设置终端

要在串口端口上设置终端，你必须设置一个 `getty` 进程，就像设置拨入调制解调器一样。按照以下步骤操作：

1. 确保你使用正确的串口线将终端连接到串口端口。大多数终端需要空回调制器（null modem），因为 TD（传输数据）和 RD（接收数据）信号线从电缆的一端到另一端是反反的（关于串口线的进一步讨论请参见本章前面的章节）。
2. 设置你终端的通信参数。具体步骤取决于设备。
3. 以 root 身份登录并编辑 `/etc/init.d` 文件，在连接到终端的行上添加一行来启动 `getty` 进程。如果你在线路 `ttyS1` (COM2) 上有一个 VT102 兼容的终端，你可能需要在系统的 `/etc/init.d` 中添加该行：
   `S1:23:resp=/sbin/getty -L 9600 ttyS1 vt102`
4. 这假设终端运行在 9,600 的波特率下。如果终端设置为其他速率，请将 9600 更改为该数字。
5. 强制 `init` 进程重新检查 `/etc/init.d` 文件，如下所示：
   `init q`
6. 终端屏幕上应该出现登录提示，你应该能够使用现有的用户名进行登录。

## 在 Linux 中设置多端口串口卡

如果你计划用 Linux PC 和哑终端支持一个小微企业（终端比完整的 PC 便宜，尽管你可以用旧 PC 当终端），你需要的不仅仅两个串口端口。有了另一块串口卡，PC 可以连接四个串口端口。如果你需要四个以上的串口端口，就必须购买名为多端口串口卡的特殊串口 I/O 卡。这些卡通常支持 4 到 32 个串口。串口端口共享一个 IRQ，但每个端口都有唯一的 I/O 地址。

# 第 VI 部分：附录

许多多端口串口卡使用 16450 或 16550A UART。当你购买一个卡时，你可能想确保 UART 是 16550A 兼容的。

要为特定的多端口串口卡添加支持，你必须在 `/etc/rc.serial` 文件中添加相应的命令。该文件由 `/etc/rc.sysinit` 脚本在你的 Linux 系统启动时自动执行。关于在 `/etc/rc.serial` 文件中放置内容的特定信息，请咨询多端口串口卡的文档或联系供应商。Linux 内核串口驱动程序支持以下基于 16450 或 16550 UART 的多端口卡：

- Async-4 (4 端口)
- Arnet multiport-8 (8 端口)
- AST FourPort 及其克隆 (4 端口)
- Bell Technologies HUB6 (6 端口)
- Boca BB-1004 (4 端口), BB-1008 (8 端口), BB-2016 (16 端口)
- Boca IOAT66 (6 端口)
- Boca 2by4 (四个串口和两个并行端口)
- Byte Runner
- Compute ValuePort V4-ISA (与 AST FourPort 兼容)
- Digi PC/8 (8 端口)
- Dolphin (海豚)
- Globetek (环球科技)
- GTEK BBS-550 (8 端口)
- Hayes ESP
- Longline LCS-8880, LCS-8880+ (与 AST FourPort 兼容)
- Moxa C104, Moxa C104+ (与 AST FourPort 兼容)
- National Instruments NI-SERIAL
- PC-COMM (4 端口)
- Sealevel COMM-2 (2 端口), COMM-4 (4 端口), 以及 COMM-8 (8 端口)
- SIIG I/O Expander 2S IO1812 (4 端口)
- STB-4COM (4 端口)
- Twincom ACI/550
- Usenet Serial Board II (4 端口)
- VScom (以 Byte Runner 形式提供)

BB-1004 和 BB-1008 卡不支持使拨入调制解调器工作的载波检测 (CD) 和铃号 (RI) 信号。因此，你不能将 BB-1004 和 BB-1008 卡用于拨入调制解调器。

某些多端口串口卡使用特殊程序代替 16450 或 16550 UART。表 E-4 列出了几种智能多端口卡的 Linux 系统。它还显示了必须加载的驱动程序名称，以为特定类型的多端口串口卡添加支持。这些驱动程序位于你 Linux 系统 `/lib/modules/VERSION/kernel/drivers/char` 中，`VERSION` 为内核版本。

表 E-4 多端口串口卡 Linux 驱动程序

| 多端口串口卡 | Linux |
| :--- | :--- |
| 高级 (APC) | wave |
| 通用 | ipmain |
| 控制 | rocket |
| 周期 | cosa |
| Digi | easy |
| Hayes | esp |
| ISI | isicom |
| 同步 | syncl |
| MOXA | moxa |
| RIS | ser |
| 特别 | cca |
| Stallion | stallion |
| Winbond | 397 |
| PC/ | 8 |
| Moxa | 4 |
| National Instruments | 2 |
| PC-COMM | 6 |
| Sealevel | | |
| SIIG | | |
| STB-4COM | | |
| Twincom | | |
| Usenet | | |
| VScom | | |

## 附录 F：PC 卡 1001

PC 卡的最大长度可达 135.6 mm（略长 5.25 英寸），这意味着卡可以延伸到主机之外。此类扩展卡用于可插介质、收发器和天线等设备。

## PCMCIA 标准

所有规范都在 PCMCIA 标准中描述，该标准共有三个主要发布版本：

- PCMCIA 标准版本 1.0（1990年6月）：初始标准定义了68 针连接器以及 Type I 和 Type II PC 卡。该标准还定义了卡信息结构 (CIS)，它是 PC 卡互操作性的基础。PCMCIA 标准的第一个版本没有考虑任何 I/O 卡；仅考虑内存卡。

- PCMCIA 标准版本 2.0, 2.01, 2.1（1991-94年）：该标准的第二个版本为 68 针连接器定义了 I/O 接口。版本 2.01 定义了 PC 卡 AT 附加 (ATA) 规范，并提供了卡与插槽服务 (CSS) 规范的初始版本。版本 2.1 增强了 CSS 规范。

- PC 卡（1996年2月）：标准的当前版本有一个新名称：它现在被称为 PC 卡，而不是 PCMCIA 标准。该版本的标准增加了信息以提高不同类型 PC 卡之间的兼容性，并支持 3.3 伏运行、DMA 支持和 32 位 CardBus 主控等功能。

## PC 卡术语

由于所有笔记本电脑都采用了 PC 卡插槽，PC 卡市场已经历了增长。得益于 PCMCIA 标准，PC 设备可以在任何 PC 卡插槽中使用。在运行 PC 卡时，你会遇到一些特殊术语，包括以下：

- 卡信息结构 (CIS)：描述 PC 卡的特性和能力，以便操作系统或驱动程序能够配置该卡。

- CardBus：一种电气规范，描述了 32 位总线主控技术的使用，并使 PC 卡的运行速度最高达 33 MHz。

- 直接内存访问 (DMA)：与其他外围设备的含义相同；现在 PC 卡也可以使用 DMA 技术。

- 原地执行 (XIP)：允许操作系统和应用程序直接从 PC 运行，而无需加载到系统的 RAM 中，从而消除了对此类系统 RAM 的需求。

- 低电压运行：PC 卡以 3.3伏（以及 5 伏）运行的能力。卡有一个物理键，确保你不会无意中将 3.3 伏卡插入 5 伏插槽。

- 多功能能力 (Multif capability)：使 PC 卡支持多种功能。例如，3Com 的 C3562 是一个 Type II 规格的 PC、10Base-T 以太网卡和 28,800-bps 调制调器。

- 即插即用：允许你在系统开启时插入或移除 PC 卡（这被称为热插）。通过将电源连接引脚设置为最长，使得数据线在电源之前断开，你可以热插 PC 卡，随时插入或拔出卡。要停止服务，输入 `/etc/init.d/pcmia stop` 或 `service pcmia stop`。

- 电源管理：PC 卡通过卡服务规范与笔记本电脑的高级电源 (APM) 功能接口的能力。

- 缩放视频 (ZV)：PC 卡与系统视频控制器之间的连接，允许卡直接将视频数据写入视频控制器。

## 第六部分：附录

## Linux 的 PCMCIA 卡服务

PC 卡的标准化意味着 Linux 开发者可以获得为 PC 卡 编写驱动程序所需的编程信息。特别是，卡服务 (Card Services) 提供了一个独立于控制 PC 插槽（即 PC 卡的接收器或插槽）硬件的编程接口 (API)。

插槽服务规范 (Socket Services Specification) 是相关的规范，也提供了一个允许软件应用程序访问控制 PC 卡硬件的 API。

你不需要学习 PC 卡和插槽服务的 API。David Hands 已经在他的 PCMCIA Card Services for Linux 中完成了这些工作，这是一个软件包，你可以用它在 Linux 下访问 PC 卡设备。在所有情况下，你只需要：

### 激活卡服务

当你安装 Linux 时，系统上将安装 PCMCIA 卡服务。PCMCIA 软件位于 `pcmia-cs` RPM 中。

假设已安装 PCMCIA 支持，以下文件控制卡服务的激活：

- `/etc/init.d/pcmia` 是启动 PCMCIA 卡服务的 shell 脚本。本质上，执行命令 `/etc/init.d/pcmia start` 或 `service pcmia start` 在启动系统时激活卡服务。该脚本使用 `modprobe` 命令加载相应的 PCMCIA 驱动模块。脚本运行 `/sbin/cdrmarg` 程序，该程序处理所有的卡插入和拔出事件。运行 `cdrmarg` 程序允许你随时插入或拔出以交换 PC 卡。要停止服务，输入 `/etc/init.d/pcmia stop` 或 `service pcmia stop`。

- `/sysconfig/pcmia` 包含了 `/etc/init.d/pcmia` 脚本的几个变量。特别是，除非 `/etc/sysconfig/pcmia` 文件中出现 `PCMCIA=yes` 行，否则不会激活卡服务。以下行也指定了名称：
