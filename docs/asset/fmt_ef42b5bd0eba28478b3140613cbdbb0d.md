
Minicom 启动并显示一个让你配置 Minicom 各个方面的对话框。进行你需要的更改，然后使用上下方向键高亮“Save as default”（保存为默认）；然后按回车。Minicom 将重置调制解器。

Minicom 程序类似于一个名为 Telix 的旧通信程序。在那个程序中，你可以按下 `Ctrl-A` 获取 Minicom 的注意。在你按下 `Ctrl-A` 后，如果按下 `Z`，将以文本窗口的形式显示帮助屏幕。

在帮助屏幕中，你可以获取有关其他 Minicom 命令的信息。在在线模式下，你可以使用 `ATDT` 命令拨打调制解器。特别是你可以使用 `ATDT` 命令拨打另一个调制解器的号码（例如你的互联网服务提供商的计算机或工作系统）。一旦获得登录提示符，你就可以像往一样登录。

当你退出另一个系统并想要退出 Minicom 时，按下 `Ctrl-A`，输入 `X` 退出程序。在 Minicom 提示处按回车。

## 设置 Linux 拨入

你可以将同一个调制解器用于拨入和拨出（当然，任何时刻只允许一种操作）。设置调制解器用于拨入涉及设置一个监控串口任何入电的程序；该程序提供登录提示符。你可以使用 `mgetty` 程序来实现此目的。

第 13 章描述了如何将 Red Hat Linux 设置为拨入 PPP 接收器。该描述还告诉你通过阅读 URL `http://www.iblio.org/pub/linux/HOWTO/Modem-HOWTO` 中最新的 Modem-HOWTO 来了解更多关于设置拨入调制解器的知识。你还应该阅读

`mget` 手册——在带有 GUI 屏幕的终端中输入 `kghostview/usr/share/doc/mget*/mget.ps` 即可阅读 `mget` 软件分发版附带的 PostScript 手册。如果系统中没有安装 `mget`，你将在其中一张光刻盘上找到 `mget` RPM（有关如何安装 RPM 的信息请参阅第 21 章）。

# 终端与多端口串口卡

之前的章节向你展示了如何在 Linux 中设置和使用调制解器进行拨号拨出。本附录的其余部分简要描述了连接到 PC 串口端口的终端的设置步骤。你还将找到 Linux 支持的多端口串口卡列表。

你可以通过阅读《Text-Terminal-HOWTO》了解更多关于将终端连接到 Linux 系统的知识，该文档在线地址为 `http://www.biblio.org/pub/linux/docs/HOWTO/Text-Terminal-HOWTO`。

> 注意，你可能想使用 x86 PC（尤其是旧的 486 和奔腾 PC）作为连接到你 Linux 系统的终端。要将 PC 转换为终端，PC 上只需要一个串口通信包，例如 Procomm Plus 或 Telix。

## 在串口端口上设置终端

要在串口端口上设置终端，你必须设置一个 `getty` 进程，就像你设置拨入调制解器一样。按照以下步骤操作：

1. 确保使用正确的串口线将终端连接到串口端口。大多数终端需要交叉调制线，电线中的 TD（传输数据）和 RD（接收数据）信号线从电缆的一端到另一端是反的。（有关串口线的进一步讨论，请参见本章前面的章节）。
2. 设置终端的通信参数。具体步骤取决于终端类型。
3. 以 root 身份登录并编辑 `/etc/initittab` 文件，添加一行在连接到终端的行上启动 `getty` 进程。如果你在 `ttyS1` (COM2) 行上有一个兼容 VT102 的终端，向你的系统 `/etc/initittab` 添加以下行：
   `s1:23:respawn:/sbin/getty -L 9600 ttyS1 vt102`
4. 强制 `init` 进程重新检查 `/etc/initittab` 文件，操作如下：
5. 终端屏幕上应该出现登录提示，你应该能够使用现有的用户名登录。

## 附录 E：调制解器与终端 983

## 在 Linux 中设置多端口串口卡

如果你计划用 Linux PC 和哑终端支持一家小微企业（终端比完整的 PC 便宜，尽管你也可以用旧 PC 当终端），你可能需要两个以上的串口端口。通过另一块串口卡，PC 可以支持四个串口端口。如果你需要四个以上的串口端口，你必须购买特殊的 I/O 板作为多端口串口卡。这些板卡通常支持 4 到 32 个串口端口。串口端口共享一个 IRQ，但每个端口都有唯一的 I/O 地址。

许多多端口串口卡使用 16450 或 16550A UART。当你购买板卡时，你可能想确保 UART 兼容 16550A。

要添加特定的多端口串口卡，你必须在 `/etc/rc.serial` 文件中添加相应的命令。该文件在 Red Hat Linux 系统启动时由 `/rcsysinit` 脚本自动执行。有关在 `/etc/rc.serial` 文件中放置内容的特定信息，请咨询多端口串口卡的文档或联系供应商。Linux 内核串口端口驱动支持以下基于 16450 或 16550A 的多端口串口卡：

- AST FourPort 及其克隆 (4 端口)
- Accent Async-4 (4 端口)
- Arnet Multiport-8 (8 端口)
- Bell Technologies HUB6 (6 端口)
- Boca BB-104 (4 端口), BB-1008 (8 端口), BB-2016 (16 端口)
- Boca IOAT66 (6 端口)
- Boca 2by4 (四个串口和两个并行端口)
- Byte Runner
- Compute ValuePort V4-ISA (兼容 AST FourPort)
- Digi PC/8 (8 端口)
- Dolphin
- Globetek
- GTEK BBS-550 (8 端口)
- Hayes
- Longshine LCS-8880, Longshine LCS-8880+ (兼容 AST FourPort)
- Moxa C104, Moxa C104+ (兼容 AST FourPort)
- National Instruments NI-SERIAL
- PC-COMM (4 端口)
- Sealeavel Systems COMM-2 (2 端口), COMM-4 (4 端口), 和 COMM-8 (8 端口)
- SIIG I/O Expander 2S IO10812 (4 端口)
- STB-4COM (4 端口)
- Twincom ACI/550
- Usenet Serial Board II (4 端口)
- VScom (与 Byte Runner 相同的驱动)

## 第 VI 部分：附录

Boca BB-1004 和 BB-1008 不支持拨入调制解器所需的载波检测 (CD) 和振铃指示 (RI) 信号。因此，你无法配合拨入调制解器使用 BB-1004 和 BB-1008 板。某些多端口串口卡使用特殊处理器代替 16450 或 16550 UART。表 E-5 列出了 Red Hat Linux 支持的多端口串口卡。它还显示了为了支持特定类型的多端口串口卡必须加载的驱动模块。这些驱动模块位于你的 Red Hat Linux 系统的 `/lib/modules/VERSION/kernel/drivers/char` 目录，`VERSION` 为 Linux 内核版本。

## 表 E-5：多端口串口卡的 Linux 驱动

| 多端口串口卡 | Linux 驱动模块 |
| :--- | :--- |
| Computone IntelliPort II | `ip2main` |
| RocketPort | `rocket` |
| COSA 或 SRP 同步串口卡 | `cosa` |
| Cyclades-Y 和 Cyclades-Z 系列多端口串口卡 | `cyclades` |
| Digi International PC/Xe, PC/Xi, PC/Xr 和 PC/Xem | `epca` |
| Hayes | `esp` |
| ISI | `isicom` |
| Microagate | `synlink` |
| MOXA | `moxa` |
| MOXA | `moxa` |
| RISC | `riscom` |
| Special | `specialix` |
| Stallion | `stallion` |
| Winbond | `w8377` |

Boca BB-1004 和 BB-1008 不支持使拨入调制解器工作的载波检测 (CD) 和振铃指示 (RI) 信号。因此，你无法配合拨入调制解器使用 BB-1004 和 BB-1008 板。

某些多端口串口卡使用特殊处理器代替 16450 或 16550 UART。表 E-5 列出了 Red Hat Linux 支持的多端口串口卡。它还显示了为了支持特定类型的多端口串口卡必须加载的驱动模块。这些驱动模块位于你的 Red Hat Linux 系统的 `/lib/modules/VERSION/kernel/drivers/char` 目录，`VERSION` 为 Linux 内核版本。因此，对于内核版本 2.4.20-48，这些驱动模块在 `/lib/modules/2.4.20-48/kernel/drivers/char`。

## PC Card 物理规格

## PCMCIA 标准

所有这些规范均在 PCMCIA 标准中描述，该标准共有三个主要版本：

- **PCMCIA 标准版本 1.0（1990年6月）**——初始标准定义了 68 针连接器以及 I 型和 II 型 PC 卡。该标准还定义了卡信息结构（CIS），这是 PC/O 卡操作性的基础。PCMCIA 标准的第一个版本没有考虑 I/O 卡；仅考虑了内存卡。
- **PCMCIA 标准版本 2.0, 2.1, 2.1（1991–94年）**——标准的第二个版本为 68 针连接器定义了 I/O 接口。版本 2.01 增加了 PC 卡附件（ATA）规范，并提供了卡片与插槽服务（CSS）规范的初始版本。2.1 版本进一步增强了 CSS 规范。
- **PC Card 标准（1995年2月）**——该标准的当前版本有了一个新名称：它是 PC Card 标准，而不是 PCMCIA 标准。该版本的标准增加了信息以提高不同类型 PC 卡之间的兼容性，并支持 3.3 特运行、DMA 支持和 32 位 CardBus 总线主等功能。

## PC 卡术语

由于所有笔记本电脑都采用了 PC Card 插槽，PC 卡市场经历了了爆炸式增长。得益于 PCMCIA 标准，PC 设备可以在任何 PC Card 插槽中使用。当你使用 PC 卡时，你会遇到一些特殊术语，包括：

- **卡信息结构 (CIS)**——这描述了 PC 卡的特性和功能，以便操作系统或驱动程序能够配置该卡。
- **CardBus**——这是一种电气规范，定义了 32 位总线技术的使用，使 PC 卡的运行速度可达 33 MHz。
- **直接内存访问 (DMA)**——这与其他外围设备的含义相同；现在 PC 卡可以使用 DMA 技术。
- **原地执行 (XIP)**——这指的是一种允许系统和应用程序直接从 PC 卡运行而无需加载到 RAM 中的功能，这消除了对大量系统 RAM 的需求。
- **低电压运行**——指 PC 卡在 3.3 伏（以及 5 伏）下运行的能力。连接器具有物理防呆键，确保你不会无意中将 3.3 伏卡插入 5 伏插槽。
- **多功能能力**——这使得 PC 卡支持多个功能。例如，3Com 3562 在一个 II 型规格的 PC 卡中集成了 10Base-T 以太网卡和 28,800 调制解调器。
- **即插即用**——允许你在系统开启时插入或移除 PC 卡（这被称为*热插*）。你可以通过让电源连接引脚最长，使得数据线在断电之前断开，从而实现 PC 卡的热插拔。
- **电源管理**——指 PC 卡通过卡片服务规范（Card Services Specification）与笔记本电脑的高级电源管理（APM）功能接口的能力。
- **缩放视频 (ZV)**——指 PC 卡与系统视频控制器之间的连接，允许卡片直接将视频数据写入视频控制器。

## Linux 的 PCMCIA 卡片服务

PC 卡的标准化意味着 Linux 开发者可以获取编写 PC 卡驱动程序所需的编程信息。特别是，卡片服务规范提供了一个独立于控制 PC 卡插槽（PC 卡的插座或插槽）硬件的应用程序编程接口（API）。

插槽服务规范（Socket Services Specification）是一个相关规范，也提供了一个允许应用程序访问控制 PC 卡插槽硬件的 API。

你不需要学习 PC 卡和插槽服务的 API。David Hines 已经在他的 PCMCIA Card Services for Linux 中完成了这些工作，这是一个你可以用它在 Linux 环境下访问 PC 设备的软件包。你只需要在需要时开启 PCMCIA 服务即可。

## 激活卡片服务

如果在按照第 2 章概述的步骤安装 Red Hat Linux 时选择了“笔记本支持”（Laptop Support）包组，则系统中将安装 PCMCIA 卡片服务。如果你没有安装笔记本支持包组，可以通过从第一张光盘安装 `kernel-pcmia-rpm` 来安装 PCMCIA 服务（第 21 章提供了有关如何安装 RPM 的信息）。

假设已安装 PCMCIA，以下文件控制着卡片服务的激活：

- `/etc/init.d/pccmia` 是启动 PCMCIA 卡片服务的 shell 脚本。基本上，命令 `/etc/init.d/pccmia start`（或 `service pcmia start`）会在系统启动时激活卡片服务。该脚本使用 `modprobe` 命令加载适当的 PCMCIA 驱动模块。脚本运行 `/sbin/cardmgr` 程序，该程序处理所有的卡插入和拔出事件。运行 `cardmgr` 程序允许你交换 PC 卡，以便你可以随时插入或弹出卡。要停止卡，请输入 `/etc/init.d/pccmia stop` 或 `service pcmia stop`。
- `/etc/sysconfig/pccmia` 包含 `/etc/init.d/pccmia` 脚本使用的若干变量。特别是，除非 `/etc/sysconfig/pccmia` 中出现 `PCMCIA=yes` 行，否则卡片服务不会激活。
