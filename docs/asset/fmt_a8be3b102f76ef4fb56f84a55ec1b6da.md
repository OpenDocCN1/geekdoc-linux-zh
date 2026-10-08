
| 5 | Extended | 70 SpeedStor |

| 7 | NTFS/NTFS | 30 Partition type |

| 8 | AIX | 32 Partition 02/86 | 81 DOSBR |

| 9 | AIX | 41 PPC Boot | 82 Old Mis |

| 10 | boottable | 45 DNX.x | 83 LVM |

| 5/2 Boot Main | 49 2nd part | 85 Linux hidden |

| 6 | Win95 FAT32 (l-bf) | 52 Linux partition | e0 Linux Re., |

| 7 | Win95 FAT16 (l-bf) | 53 Linux partition | eb f6 Red.fs |

| 8 | WXFS FS (l-bf) | 54 Linux partition | de f9 Linux no. |

| 10 | OPIS | 55 CP/PK | 90 f2 secondary |

| 11 | Hidden | 60 Hidden DMX aux | 94 Ameeba BBT fd Linux auto |

| 12 | Company diagnost | 62 UnTrackDM | 97 E-Drive fx Last auto |

| 14 | Hidden FAT13 <5 | 65 Golden Home a0 BIOS/OS lx Step |

| 14 | Hidden FAT16 | 56 Golden Home a9 IBM Thinkpad bi fi BBT |

表 5.1 中所示的最常用分区类型。

# 表 5.1: 常用分区类型

| ID | 类型 |
|---|---|
| 5 | 扩展分区 (Extended) |
| 6 | DOS 16位位（大于 32MB） |
| 7 | OS/2 HPFS |
| b | Windows 95 FAT32 |
| c | 带逻辑块寻址 (LBA) 的 Windows 95 FAT32 |
| 82 | Linux 交换分区 (Swap) |
| 83 | Linux 原生分区

## 删除分区

有时您需要删除现有分区为为 Linux 安装创建一个或多个分区。执行此操作，只需使用 `d` 命令，并在提示时输入您想要删除的分区编号。

## 提交您的更改

在使用 `fdisk` 期间，没有任何安全措施，这意味着如果您不小心删除了包含重要数据的分区，您无法在永久删除包含数据的分区之前恢复到先前的配置。

出于此原因，在您退出时显式要求 `fdisk` 执行操作之前，您所做的更改实际上不会被处理。因此，在退出 `fdisk` 之前，请务必查看分区表，以确保您的操作完全符合您的意愿。如果您退出并提交更改，这些更改是永久的，且无法恢复。（理论上，您可以在在使用 `fdisk` 之前将磁盘的分区表保存到软磁盘中，并通过用保存的分区表替换新的分区表来从严重错误；然而，这是一个复杂的程序，并非万无一失。您最好还是小心，并在提交更改之前确保对分区表所做的更改完全符合您的意愿。）

退出 `fdisk` 的两种替代命令见表 5.2。

# 表 5.2: 退出 fdisk 的替代命令

| 命令 | 效果 |
| --- | --- |
| q | 退出 fdisk且不处理或保存任何更改。 |
| w | 处理并保存所有更改，然后退出 fdisk。这是一个永久性操作，请务必小心。 |

## 展望

最后，您已经准备好实际使用 Linux 了。作为在这条道路上的第一步，您将查看 X Windows 环境。X Windows 为包括 Linux 在内的所有 Unix 操作系统提供了一个高度灵活、由鼠标驱动的图形用户界面。

许多 Linux 教程从命令行开始，因为这确实是 Linux 的核心。但 X Windows 让新用户在彻底掌握 Linux 命令行之前，就能快速开始使用 Linux。

第 6 章“X Windows 概述”将向您展示 X Windows 提供什么，以及它如何与 Microsoft Windows 环境进行对比。然后，将转向 X Windows 的配置和使用，并查看一些常见的 X Windows 应用。

# 第三部分

## 在 Linux 中使用桌面环境

- 第 6 章：X Windows 概述
- 第 7 章：安装和配置 X Windows
- 第 8 章：使用 GNOME 和 X Windows
- 第 9 章：在 GNOME 和 X Windows 下应用程序
- 第 10 章：高级 GNOME 配置
- 第 11 章：使用 KDE
- 第 12 章：高级 X Windows 配置
- 什么是 X Windows？
- Microsoft Windows 对比 X Windows
- X 服务器、窗口管理器和桌面环境
- Motif 是什么？

# 第 6 章 • Windows 概述

既然您已经成功安装了 Linux，您将通过直接进入 X Windows 环境开始学习过程。许多 Linux 忠实者在考虑 Windows 命令行的复杂细节和 Linux 配置之前，一想到 X Windows 就会不寒而栗。但正是 X Windows 让 Linux 成为 Windows 和 Mac OS 的良好替代品，成为文字处理、桌面出版和浏览万维网等日常任务的高效操作系统。

本章从描述 X Windows 到底是什么开始。X Windows 为 Unix 世界提供了一个图形用户界面 (GUI)。X Windows 提供了一种交付所有非通用用户界面范式的方法，如窗口、对话框、按钮和菜单。正是 X Windows 使得复杂的图形得以创建，让基于 Unix 的工作站成为许多工程和设计应用的首选，也是 X Windows 让 Linux 能够成为 PC 操作系统市场中强力的竞争者。

## 什么是 X Windows？

简单来说，X Windows 是 Unix（以及由此延伸的 Linux）的完整图形界面。但这并不代表全部。X Windows 是一个高度可配置的环境，为用户和编写在 X Windows 下运行软件的应用程序开发者提供了极其广泛的灵活选项。

X Windows 的核心概念是客户端-服务器框架。在实际操作中，这意味着 X Windows 提供了一个不绑定于单个处理器的环境。应用程序可以运行在网络上的不同服务器和机器上，并且可以显示在网络其他地方 X Windows 终端和工作站上。

这种应用程序运行地与显示地之间的分离，在 Windows 和 Macintosh 环境中是一个概念，因为那些环境将应用程序与显示器绑定。这种分离的好处是，在网络环境中，可以有一个在维护良好、强大且易于管理的中央应用程序服务器上运行复杂的图形显示应用程序。事实上，正是这种能力赋予了 Unix/Linux 和 X Windows 在大型网络专业系统管理员中如此良好的声誉。

X Windows 环境引入的另一个概念是窗口化与接口的分离。在 X Windows 系统上，必须运行两个应用程序才能提供完整的 GUI。第一个是 X 服务器，它设置图形显示（即分辨率、刷新率和色彩深度），显示窗口和鼠标移动、击键以及多个窗口。但 X 服务器不提供菜单、窗口边框或移动、切换、最小化或最大化窗口的机制。如果你查看图 6.1，你可以看到没有窗口管理器的 X 服务器长什么样。

# 图 6.1:

没有窗口管理器的 X 服务器显示

![](img/fd2d9aa645b3d05a8fce065954a79484_128_0.png)

| 显示 | 24/8 位 | 算法 |
| --- | --- | --- |
| 裁剪 | Root | Windows | 大小 |
| | | Next |
| | | Pview |
| | | Load |
| | | Save |
| | | Print |
| | | Colordata |
| | | | 0 文件 |

![](img/fd2d9aa645b3d05a8fce065954a79484_128_1.png)

# 第 6 章 • X Windows 概述

注意图 6.1 中极简的风格。没有花哨的颜色背景，没有复杂的窗口边框或菜单控制，也没有其他构成完整 GUI 的功能。所有这些功能都由名为“窗口管理器”的第二个应用程序提供。图 6.2 显示了运行 fvwm 窗口管理器的完整 X Windows 桌面。注意窗口框、控制按钮、控制菜单以及任务栏和虚拟桌面系统。窗口管理器提供了所有这些内容。

# 图 6.2:

运行窗口管理器的 Windows 显示

![](img/fd2d9aa645b3d05a8fce065954a79484_129_0.png)

窗口管理器以标准的、预定义的方式与 X 服务器通信，因为它为 X 应用程序服务。这意味着具有不同接口特征的窗口管理器可以用这种标准方式与 X 服务器通信。同样，可用的各种 X 服务器（支持不同的显卡、显示器和其他性能特性）也可以以标准化的方式与应用程序通信。

## Microsoft Windows 对比 X Windows

（注：此部分原文仅有标题，翻译未提供具体正文）

## X 服务器、窗口管理器和桌面环境

（注：此部分原文仅有标题，翻译未提供具体正文）

## Motif 是什么？

（注：此部分原文仅有标题，翻译未提供具体正文）

从基础窗口层，通过创建不同的窗口管理器，为 X Windows 创建多个界面成为可能。

多个界面并不像微软 Windows 界面的某些自定义工具那样仅提供外观上的细微差异；相反，它们允许从窗口管理器到用户界面进行完全的重新设计。

例如，图 6.3 显示了一个运行窗口管理器的示例窗口，其界面类似于 NeXT 操作系统的用户界面。与图 6.4 相比（后者在相同系统上运行并显示相同的应用程序），后者显示的用户界面不像任何流行的 PC 或 Macintosh 操作系统。

# 图 6.3：

Afterstep 窗口管理器

![](img/fd2d9aa645b3d05a8fce065954a79484_131_0.png)

# 图 6.4：

Lestif 窗口管理器

![](img/fd2d9aa645b3d05a8fce065954a79484_132_0.png)

这些示例仅代表了 X Windows 窗口管理器提供的许多外观设计中的两种。更为人知的窗口管理器将在本章稍后部分进行讨论。

## 精细化控制

X Windows 环境的另一个优势是它对窗口环境和界面的所有方面提供了精细的控制。通过设置几十种设置中的任何一种，就可以控制环境的所有方面，从背景和前景窗口颜色到光标颜色、默认字体和默认窗口大小。用户还可以定义交互模式。例如，可以使用鼠标指针使窗口自动跳转到前台，或将光标焦点切换到后台窗口。

此外，这些以及其他功能可以按应用程序为基础进行定义，为每个应用程序创建不同的设置，以便每个应用程序都能以最方便的方式启动。

还可以定义每次启动 X 环境时打开哪些窗口和应用程序，并让系统在启动 X Windows 时对使用哪种窗口管理器做出逻辑选择。

第 7 章“安装和配置 X Windows”将讨论基本的 Windows 窗口配置选项。

## 客户端-服务器环境

如前所述，X Windows 世界基于客户端-服务器模型工作，其中应用程序是 X 服务器的客户端，由服务器驱动物理显示。这使得 Windows 非常适用于网络环境，允许应用程序运行在网络上的某一台机器上，同时在另一台机器上显示其输出。

微软 Windows 直到最近才具备这种能力，现在通过其在在端多用户 Windows NT 和 2000 系统上的终端服务器服务以一种有限且昂贵的方式实现了这一点。在 Linux、Unix 和 X 世界中，即使是最低的系统也能在该 Windows 客户端-服务器模型中扮演客户端角色或服务器角色。

## X 服务器、窗口管理器和桌面环境

现在你已经对 X Windows 在整体中的位置有了了解，你需要理解 X Windows 的基本组件：X 服务器、窗口管理器和桌面环境。正是这些组件以及它们所代表的模块化提供了 X Windows 的强大和灵活性。

## X 服务器

正如你所看到的，X Windows 系统的核心是 X 服务器。X 服务器处理若干任务：

- 支持各种显卡和显示器任务
- X Windows 显示的分辨率、刷新率和色彩深度
- 基本窗口管理：显示和关闭窗口，跟踪鼠标移动和击键输入

# X 服务器、窗口管理器和桌面环境 97

具有这些基本能力的多个 X 服务器脱颖而出。在 Linux 世界中有三个主要选择：`XFree86`、`Metro-X` 和 `Accelerated-X`。

## XFree86

`XFree86` 是几乎所有非商业 Linux 发行版中的默认 X 服务器，因为它按照 Linux 相同的条款免费提供。提供完整的源代码，用户可以自由更改代码以满足其需求，并且任何人都可以重新分发。Red Hat Linux 7.1 带有 `XFree86` 4.0.3。每几个月发布一次小更新，可以从 XFree86 网站 `http://www.xfree86.org` 下载。

`XFree86` Web 服务器设计用于为兼容 Intel 的 x86 PC 常用硬件，以及带有 Compaq Alpha、PowerPC、Sparc 和 MIPS 处理器的计算机提供广泛支持。虽然它的性能并不总是完美的，但 `XFree86` 是 Linux 和其他基于 Intel 的 Unix 变体中 X 服务器的规范，因此是大多数人熟悉的 X 服务器。

虽然在写本文时对 MIPS 的支持还不完全，但根据 `XFree86` 项目网站，MIPS HOWTO `http://os.sgi.com/mips/mips-howto.html` 提供了大量的文档。

`XFree86` 支持的流行显卡芯片组包括 Tseng 的 ET3000、4000 和 6000，Trident 全系列芯片，Cirrus Logic 大多数产品，Chips and Technologies 显卡芯片以及许多其他。你可以在 `XFree86` 项目的驱动页面 `http://www.xfree86.org/4.0.3/Status.html` 上找到支持硬件的完整列表。如果你使用的是更高版本，请相应替换 4.0.3。

虽然 `XFree86` 4 X 服务器在使 Linux 成为完整的免费的类 Unix 操作系统方面迈了一步，但它确实存在一些缺点，使其对企业或关键任务任务的吸引力较低。幸运的是，Red Hat Linux 7.1 有一个非常出实用程序，极大减轻了配置 `XFree86` 的工作。事实上，Free86 对笔记本显示的支持非常有限，一个错误可能意味着你的 LCD 损坏。如果你计划将笔记本作为 Linux 系统长期使用，查看 Laptop Accelerated-X 服务器支持的系统列表，看看你的设备是否在。

## XFree86 4 有什么新？

`XFree86` 第 4 版本包含了早期版本中未发现的新功能。其中一些新功能包括：

- 统一的服务器架构设计
- 支持多显卡
- 独立于操作系统
- 3D 渲染
- FreeType 支持

通过统一的服务器，`XFree86` 4 不再依赖驱动库（或任何其他操作系统）。通过 GLX 扩展，`XFree86` 现在支持通过 Silicon Graphics 的 OpenGL 进行 3D 渲染。有了 FreeType 支持，`XFree86` 现在可以管理 TrueType 字体。

`XFree86` 现在增强并增加了对更多平台的支持，包括基于 Alpha、MIPS 和 PowerPC 处理器的平台。预计它将为 Intel Itanium 64 位平台就绪。

## 商业 X 服务器

除了作为 Linux 完整免费解决方案部分的 `XFree86` 项目外，Linux 世界有两个领先的商业 X 服务器：`Metro-X` 和 `Accelerated-X`。这些产品的优势在于对各种图形芯片和卡的更广泛支持，并且通常充分利用这些芯片卡的加速特性。此外，`Metro-X` 和 `Accelerated-X` 提供了更智能的配置，通常可以在几分钟内安装并运行。

## X 服务器、窗口管理器和桌面环境

来自 Metro Link 的 `Metro-X` 是一种高性能 X 服务器选项。`Metro-X` 的许多优势包括一个设计良好的图形配置界面（如图 6.5 所示）、支持多头显示（标准配置支持四个不同的显示器）、支持某些品牌的触摸屏。关于 `Metro-X` 服务器的完整信息（包括支持的显卡）可以在 Metro Link 主页 `http://www.metrolink.com/` 上找到。`Metro-X` Linux 版售价 39 美元。

# 图 6.5：

`Metro-X` 的配置窗口

![](img/fd2d9aa645b3d05a8fce065954a79484_136_0.png)

`Accelerated-X` X-Inside 实际上为 Linux 提供了一系列 X 服务器。这些包括 Linux 的 `Accelerated-X` 服务器、3D `Accelerated-X` 服务器、多笔记本 `Accelerated-X` 服务器以及专门的 Laptop `Accelerated-X` 服务器。笔记本 `Accelerated-X` 服务器意义重大，因为笔记本上的芯片组与桌面显卡不同，且 LCD 屏幕有自己的一套被桌面驱动程序忽略的 own。

`Accelerated-X` 支持来自 60 多家制造商的 400 多块显卡。多头 X 服务器支持多达 16 个屏幕，并在每个屏幕上提供 `Accelerated-X` 的所有功能。

总体而言，X-Inside 的服务器价格具有竞争力。`Accelerated-X` 售价 99.95 美元，笔记本服务器为 149.95 美元，多头版本为 199.95 美元。详细信息可用 X-Inside 网站 `http://www.xinside.com`。

## 窗口管理器

窗口管理器完善了 X 服务器提供的优质 GUI 功能。除此外，窗口管理器包括窗口装饰（提供调整大小、移动、关闭和最小化窗口的方法）以及启动应用程序的机制（如桌面菜单、控制面板和按钮栏）。
