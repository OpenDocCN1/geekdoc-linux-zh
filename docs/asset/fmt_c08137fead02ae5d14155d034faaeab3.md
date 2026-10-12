
## 修改分区类型

默认情况下，所有使用 `fdisk` 创建的新分区都被分配类型为 Linux Native（Linux 原生，类型编号 `83`）。要更改分区类型，请使用 `t` 命令。

系统会提示你选择要操作的分区（你可以通过数字选择，如图 5.6 所示），然后会提示你输入类型 ID。要查看类型 ID 列表，此时请使用 `l` 命令查看图 5.6 所示的列表。

### 图 5.6: 在 `fdisk` 中更改分区类型

| ID | Name | Hex | Description | Type |
|---|---|---|---|-|
| 0 | Empty | 00 | Unallocated | - |
| 1 | Linux filesystem | 83 | Linux LVM2 PV | Linux LVM2 PV (physical-volume) |
| 2 | Linux swap | 82 | Linux-SWAP | Linux-SWAP |
| 3 | Linux ext | 8d | Linux filesystem | Linux filesystem |
| 4 | Linux hib | 8e | Linux logical | Linux logical |
| 5 | Linux raid | 81 | Linux raid | Linux raid |
| 6 | Linux lvm | f4 | Linux extended | Linux extended |
| 7 | NTFS/NTFS | 07 | NTFS/NTFS | NTFS/NTFS |
| 8 | FAT12 | 0c | FAT12 | FAT12 |
| 9 | FAT16 | 0b | FAT16 | FAT16 |
| 10 | FAT32 | 0c | FAT32 | FAT32 |
| 11 | HPFS | 0b | HPFS | HPFS |
| 12 | Solaris OS | 03 | Solaris OS | Solaris OS |
| 13 | Apple Mac | 07 | Apple Mac | Apple Mac |
| 14 | WFS | 0e | WFS | WFS |
| 15 | Hidden | 00 | Hidden partition | Hidden |

`Command (n for help): n`

最常用的分区类型如表 5.1 所示。

### 表 5.1: 常用分区类型

| ID | Type |
|---|---|
| 5 | Extended |
| 6 | DOS 16-bit (larger than 32MB) |
| 7 | OS/2 HPFS |
| b | Windows 95 FAT32 |
| c | Windows 95 FAT32 with Logical Block Addressing (LBA) |
| 82 | Linux Swap |
| 83 | Linux Native |

## 删除分区

有时你需要删除现有分区，以便为 Linux 安装创建一个或多个新分区。要执行此操作，只需使用 `d` 命令，并在提示时输入想要删除的分区号。

## 提交更改

在你操作 `fdisk` 时，你所做的任何更改都不会应用到物理磁盘。这是一种安全措施，这样如果你不小心删除了包含重要数据的分区，可以在永久删除该数据分区之前恢复到先前的配置。

因此，只有在退出时显式让 `fdisk` 执行时，更改才会被处理。所以，在退出 `fdisk` 之前，请仔细查看分区表，以确保操作完全符合你的预期。

## 图形化桌面与 X Windows

在这种环境中，可以拥有复杂的图形化桌面，并显示运行在维护良好、强大且易于管理的中央应用程序服务器上的程序。事实上，正是这种能力让 Unix/Linux 和 X Windows 在大型网络的专业系统管理员中赢得了良好的盛誉。

X Windows 环境引入的另一个概念是窗口化与界面的分离。在 X Windows 系统上，必须运行两个应用程序才能提供完整的图形用户界面（GUI）。第一个是 X 服务器（`X server`），它设置图形显示（例如分辨率、刷新率和色彩深度）、显示窗口，并跟踪鼠标移动、击键输入以及多个窗口。但 X 服务器并不提供菜单、窗口框，或者移动、切换、最小化或最大化窗口的机制。如果你查看图 6.1，就可以看到在没有窗口管理器的情况下 X 服务器看起来是什么样。

### 图 6.1：没有窗口管理器的 X 服务器显示

![](img/968f44a58bee05b3a080631d18e977c9_128_0.png)

## 第 6 章 • X Windows 概述

请注意图 6.1 中极其简单的设计。它没有花哨的背景颜色，没有复杂的窗口框或菜单控制，也没有其他构成完整 GUI 的功能。所有这些功能都由名为“窗口管理器”（`window manager`）的第二个应用程序提供。图 6.2 显示了一个运行 `fw95` 窗口管理器的完整 X Windows 桌面。注意窗口框、控制按钮、控制菜单以及任务栏（Taskbar）和虚拟桌面系统的功能。所有这些都由窗口管理器提供。

### 图 6.2：运行窗口管理器的 Windows 显示

![](img/968f44a58bee05b3a080631d18e977c9_129_0.png)

窗口管理器以标准的预定义方式与 X 服务器通信，X 服务器与 X 应用程序之间的通信方式也是如此。这意味着具有不同界面特征的不同窗口管理器都可以以这种标准方式与 X 服务器通信。同样，可用的各种 X 服务器（提供对不同显卡、显示器和其他性能特的支持）也可以以标准化的方式与应用程序通信。

## Microsoft Windows 对比 X Windows

根据你所看到的关于 X Windows 的描述，人们自然会假设 Microsoft Windows 和 X Windows 几乎是同一东西。但现实情况是，它们在根本上是完全不同的。

例如，Microsoft Windows 是一个完整的操作系统，包含了从内核到外壳，再到窗口化环境等所有内容。而 X Windows 只是该操作系统拼图中的碎片：窗口化环境。另一个对比在于界面：Microsoft Windows 界面相当固定，而 X Windows 界面具有具有惊人的灵活性和可定制性的设计。

## 相似之处

那么，X Windows 和微软目前的操作系统之间有什么相似之处呢？主要的相似之处在于，它们都提供了图形界面，并使得处理多个窗口成为可能。在此基础上，它们允许用户使用键盘和纯字符以外的方法与信息进行交互。用户可以使用鼠标以及键盘，并可以创建结合菜单、表单、窗口和对话框的界面。

## 差异

这两个窗口系统之间存在许多差异。差异体现在以下领域：

- 界面的灵活性
- 对界面配置的精细控制
- 客户端-服务器技术

## 灵活的界面

X Windows 界面的灵活性是许多用户在该环境中的乐趣之一。如前所述，用户界面层与基础窗口层的分离，使得通过创建不同的窗口管理器为 X Windows 创建多个界面成为可能。

多个界面并非仅仅像某些 Microsoft Windows 界面定制工具所提供的那些细微外观差异；相反它们允许从一个窗口管理器到另一个窗口管理器对用户界面进行完全重新设计。

例如，图 6.3 显示了一个类似于 NeXT 操作系统界面的窗口管理器示例界面。对比图 6.4，它在相同的系统上运行相同的应用程序，但显示的用户界面不像任何流行的 PC 或 Macintosh 操作系统。

### 图 6.3：运行 Afterstep 的窗口管理器

![](img/968f44a58bee05b3a080631d18e977c9_131_0.png)

### 图 6.4：运行 Lestif 的窗口管理器

![](img/968f44a58bee05b3a080631d18e977c9_132_0.png)

这些示例仅代表 X Windows 窗口管理器提供的许多外观设计中的两种。为人知的窗口管理器将在本章后面稍要讨论。

## 精细控制

X Windows 环境的另一个优势是它对窗口化环境和界面的所有方面提供了精细控制。通过设置几十种配置，可以控制环境的所有方面，从背景和前景窗口颜色到光标颜色、默认字体和默认窗口大小。用户可以定义交互模式。例如，可以使用鼠标指针使窗口自动跳转到前景或将光标焦点切换到后台窗口。

此外，这些和其他功能可以按应用程序定义，创建不同的设置。

## 客户端-服务器环境

如之前提到的，X Windows 的核心是客户端-服务器模型。

## X 服务器、窗口管理器和桌面环境

现在你已经了解 X Windows 的位置，你需要理解基础组件：X 服务器、窗口管理器和桌面环境。这些组件代表了 X Windows 的强大。

### X 服务器

正如你所看到的，X 服务器处理若干任务：

- 对各种显卡的支持
- 分辨率、刷新率和色彩深度
- 基础窗口管理：显示和关闭窗口

### `XFree86` 4 有哪些新特性？

`XFree86` 4 版本包含了许多早期版本中没有的新特性。其中一些新功能借用了商业版 X 服务器的功能。这些特性包括以下内容：

- 统一的 X 服务器模块化架构设计
- 支持多块显卡
- 独立于操作系统
- `3D` 渲染
- 对 `FreeType` 支持

通过统一的 X 服务器，`XFree86` 4 允许在无需重新配置的情况下使用不同类型的显卡。通过 Metro Link 捐的运行时加载器，`XFree86` 4 不再依赖 Linux（或任何基于 Unix 的操作系统）的驱动库。通过 `GLX` 扩展，`XFree86` 现在通过 Silicon Graphics；`OpenGL` `3D` 图形语言支持 `3D` 渲染。通过 `FreeType` 支持，`XFree86` 现在可以管理 `TrueType` 字体。

`XFree86` 现在增强并增加了对更多平台的支持，包括基于 `Alpha`、`MIPS` 和 `PowerPC` 处理器的计算机。预计在 Intel `Itanium` `IA` `64` 位平台发布时，它将准备就绪。

在本文编写时，`XFree86` 4 版本不支持旧的 `XFree86Setup` 工具。`Xconfigurator` 和 `xf86config` 等替代工具是完全足够的替代方案。

### 商业 X 服务器

除了 `XFree86` 项目（它是使 Linux 成为完整且免费解决方案的重要部分）外，Linux 世界还有两个领先的商业 X 服务器：`Metro-X` 和 `Accelerated-X`。

这些产品的优势在于对各种芯片和显卡提供更广泛的支持，并且通常充分利用这些芯片和显卡的加速功能。此外，`Metro-X` 和 `Accelerated-X` 提供了更智能的配置，通常可以在几分钟内完成安装并运行。

### X 服务器、窗口管理器和桌面环境

来自 Metro Link 的 `Metro-X` 是一个高性能 X 服务器选项。`Metro-X` 的许多优点包括：如图 6.5 所示的设计良好的图形化界面、支持多头显示（标准配置支持四台不同的显示器）、支持某些品牌的触摸屏等。

#### 图 6.5：`Metro-X` 的配置窗口

![](img/968f44a58bee05b3a080631d18e977c9_136_0.png)

关于 `Metro-X` 服务器的完整信息（包括支持的显卡）可以在 Metro Link 的主页 `http://www.metrolink.com/` 上。`Metro-X` Linux 版价格为 39 美元。

`Accelerated-X` `X-Inside` 为 Linux 提供系列 X 服务器。这些包括 Linux 版 `Accelerated-X` 服务器、`3D` `Accelerated-X` 服务器、多头 `Accelerated-X` 服务器以及专门的笔记本电脑 `Accelerated-X` 服务器。`Accelerated-X` 服务器之所以意义重大，是因为笔记本电脑上的芯片组与桌面显卡中的芯片不同，而且 `LCD` 屏幕有自己一套被桌面端驱动程序忽略的特殊。

事实上，`XFree86` 对笔记本显示器的支持非常有限，一个小错误就可能导致你的 `LCD` 损坏。如果你计划将笔记本电脑作为 Linux 系统使用，请查看 Laptop `Accelerated-X` 服务器支持的系统列表，确认是否存在。

### 窗口管理器

`Accelerated-X` 支持来自 60 多个制造商的 400 多块显卡。多头 `Accelerated-X` 服务器支持多达 16 个屏幕，并在每个屏幕上都提供 `Accelerated-X` 的所有功能。

总的来说，`X-Inside` 的服务器价格具有竞争力。`Accelerated-X` 价格为 99.95 美元，笔记本服务器为 149.95 美元，多头服务器为 199.95 美元。完整信息可以在 `X-Inside` 网站 `http://www/.xinside.com/` 获取。

窗口管理器完善了 X 服务器未提供的 GUI 细节。除其他功能外，窗口管理器还包括窗口装饰（提供调整大小、移动、关闭和最小化窗口的方法）以及启动应用程序的机制（例如桌面菜单、控制面板和按钮栏）。

本节剩余部分简要介绍了 Linux 可用的一些主要窗口管理器，包括 `FWWM`、`fwm95`、`olvm` 等。Red Hat Linux 7.1 的默认窗口管理器是 `Sawfish`，但任何相对完整的安装都会包含。

#### `FWWM` 和 `fwm95`

在 20 世纪 90 年代中期，Linux 最常用的窗口管理器是 `FWWM` 或 `fwm95`。`FWWM` 这个名字很奇怪，因为没有人确定“F” 代表什么。有人说它代表“Free”（免费），有人说它代表“Fast”（快速），还有人认为它代表“Flexible”（灵活）。

`FWWM` 是一个轻量级窗口管理器，提供多个桌面并允许事实性的定制。`FWWM` 的事实性定制可以在网页 `http://www.fvwm.org/` 上找到。`FWWM` 的事实性定制基于版本 2。

##### 图 6.6：一个 `FVWM` 示例

![](img/968f44a58bee05b3a080631d18e977c9_138_0.png)

在可用的 2.5 版本中，在 `--WM--WM-pos-the-----------style` 环境下使用的界面。

##### 图 6.7：`fwm95` 界面

![](img/968f44a58bee05b3a080631d18e977c9_139_0.png)

##### 图 6.8：`twm` 桌面

![](img/968f44a58bee05b3a080631d18e977c9_140_0.png)

##### 图 6.9：`olvm` 界面

![](img/968f44a58bee05b3a080631d18e977c9_141_0.png)

#### `Afterstep`

`Afterstep` 是原始 `FVWM` 代码的另一个变体。该产品基于一个名为 `Bowman` 的早期窗口管理器，设计旨在提供 NeXTSTEP 平台上 NeXTSTEP 窗口管理器的视觉效果。6.10 显示了一个 `Afterstep` 桌面。

提取自 NeXTSTEP 的主要特性包括标题栏、按钮和边界的外观、样式菜单的外观以及类似 NeXTSTEP 的图标和按钮栏。由于它基于 `FVWM` 版本 1 代码，因此该版本 `FVWM` 的任何模块都应该可以在 `Afterstep` 中工作。与 `fwm95` 和 `olvwm` 等窗口管理器不同，`Afterstep` 的组织化开发工作仍在进行。

`Afterstep` 主页地址为 `http://www.afterstep.org/`

##### 图 6.10：`Afterstep` 桌面

![](img/968f44a58bee05b3a080631d18e977c9_142_0.png)

#### `AmiWm`

如果你是 `Amiga` 电脑的前任用户并爱上了它的界面，那么 `AmiWm` 可能正适合你的窗口管理器。`AmiWm` 模拟了 `Amiga` 的工作台（如图 6.11 所示）。由于支持像 `Amiga` 那样的多屏幕显示，`AmiWm` 可以帮助前任 `Amiga` 用户轻松地过渡到 X Windows。

你可以在 `AmiWm` 的主页 `http://www.lysator.liu.se/~marcus/amiwm.html` 了解 `AmiWm` 并下载该软件。

##### 图 6.11：`Amiwm` 窗口管理器

![](img/968f44a58bee05b3a080631d18e977c9_143_0.png)

#### `Enlightenment`

`Enlightenment` 是一个宏大的项目，试图开发一个超越传统的窗口管理器。它提供了一个既实用又具有视觉吸引力的环境，并允许用户定义从功能到窗口管理器外观的所有内容。图 6.12 和 6.13 显示了 `Enlightenment` 环境的两种可能的配置。在帮助 `Enlightenment` 脱颖而出的众多特性中，它赋予了用户手工定制外观以及轻松嵌入新功能的能力。

`Enlightenment` 是一个野心勃勃的项目，提供了视觉上惊艳的界面，但对于新手用户来说，安装可能是一项挑战，通常需要用户自行编译并安装新库。`Enlightenment` 的主页位于 `http://www.enlightenment.org/`。请注意，作者认为 `Enlightenment` 处于早期的预发布阶段（本文的当前版本为 `0.16`），因此警告可能存在 Bug 和崩溃。尽管如此，这仍然是一个有趣的项目，也是窗口管理器中一个独特的概念。

##### 图 6.12：`Enlightenment` 窗口管理器

![](img/968f44a58bee05b3a080631d18e977c9_144_0.png)

##### 图 6.13：用户可以完全自定义 `Enlightenment` 环境

![](img/968f44a58bee05b3a080631d18e977c9_144_1.png)

#### `Sawfish`

`Sawfish` 窗口管理器是 GNOME 桌面环境的新默认管理器。与 `Enlightenment` 不同，`Sawfish` 最大化了配置每个窗口的能力，在这种情况下是通过使用 `LISP` 编程语言的工具实现的。作为 GNOME 桌面的一部分，`Sawfish` 控制集成在 GNOME 控制中心中，如图 6.14 所示。第 10 章“高级配置”详细涵盖了 GNOME 控制中心和 `Sawfish`。

##### 图 6.14：用户可以完全自定义 `Sawfish` 环境

![](img/968f44a58bee05b3a080631d18e977c9_145_0.png)

与 `Enlightenment` 一样，`Sawfish` 也是一个正在开发中的项目。本文当前版本为 `0.38`。欲了解更多，请访问 `Sawfish` 主页 `www.sawfish.org`。

## 桌面环境

桌面环境不仅仅是窗口管理器。桌面环境旨在提供一个完整、统一的图形用户界面（GUI）。使用简单的窗口管理器，无法保证应用程序与其他操作系统中的功能在外观和体验上保持的一致性，例如应用程序之间的拖放以及跨应用程序的数据嵌入。

Linux 有不同的桌面环境，它们提供了稳健、集成的 GUI，并为应用程序开发者提供了一个目标平台，以构建具有共同外观和体验的软件，并包含了拖放等集成功能。

这些桌面环境中的两个——K 桌面环境和 GNOME——是免费获取的，并已成为事实标准 Linux 桌面环境的竞争者。

### K 桌面环境

K 桌面环境 (KDE) 尝试提供通用桌面环境（在本节后半部分将讨论）的免费替代方案。在此项工作中，KDE 将一组应用程序（如文件管理器、终端模拟器和显示配置系统）与窗口管理器相结合，为 X 应用程序创建一致的外观和体验。6.15 显示了一个典型的 KDE 桌面。

#### 图 6.15：一个 KDE 桌面

![](img/968f44a58bee05b3a080631d18e977c9_146_0.png)

KDE 是许多 Linux 发行版的默认桌面环境，包括 Caldera、S.u.S.E. 和 Corel。它是大多数其他发行版的备选桌面环境。

KDE 规划的一部分是规范标准，并使开发环境使开发者能够创建在功能和外观上保持一致的应用程序。KDE 提供了一个极人吸引、看起来专业的工作环境，如果为 KDE 开发了必要的应用程序，它将成为商业桌面的良好前景。KDE 网站为 `http://www.kde.org/`；第 11 章“使用 KDE”详细涵盖了带有 Red Hat Linux 7.1 的 KDE 2.1.1。

### GNOME：GNU 网络对象环境

GNOME 是开发 Linux 桌面环境另一种尝试的结果。与包含内置窗口管理器的 KDE 不同，GNOME 是窗口管理器独立的。它提供了一个编程接口，允许窗口管理器开发者集成对 GNOME 的完整支持。

Red Hat Linux 7.1 将 GNOME 作为默认环境发布。该发行版包含其他窗口管理器，但由于默认安装使用 GNOME，本书将使用 GNOME 作为 Enlightenment。欲了解如何使用 GNOME，请参阅第 8 章。

### MWM

MWM，即 Motif 窗口管理器，是 Motif 发行版的一部分窗口管理器。Motif 作为完整环境将在下一节中详细讨论。

### 通用桌面环境

通用桌面环境 (CDE) 是一个野心勃勃的项目，旨在标准化各种 Unix 平台上的图形环境和开发区域，包括 AIX、Compaq Unix、HP/UX 和 Solaris。现在 CDE 通过 X-Inside 的桌面界面 (`http://www.xinside.com/`) 供 Linux 使用。该商业应用售价 49 美元，需要 X-Inside 的 Accelerated-X。

除了基于 Motif 的一致环境外，CDE 还提供了一套统一的工具和应用程序，以标准化管理程序并简化用户图形环境的管理。CDE 为 X 环境带来的增强功能包括拖放功能以及其他 GUI 操作系统中常见的文件夹和图标。

### 什么是 Motif？

如果你开始在网上寻找安装在 Linux 系统上的 X Windows 应用程序，你不可避免会遇到提到 Motif 库或 Motif 工具包的应用程序。

Motif 是一种 X Windows 的开发环境，由开放软件基金会 (OSF) 在 20 世纪 80 年代后期推出，为 X Windows 应用程序提供一致的策略。Motif 提供了一个部件工具包，开发者可以在开发应用程序中使用它。通过使用这些部件库，Motif 开发者产生的应用程序符合 Motif 的一致外观和体验策略。

Motif 最近以“开放”许可证重新发布，这意味着想要基于 Motif 库构建和发布应用程序的开发者不再需要为此特付费。然而，新 Open Motif 背后的组织 Open Group 仍在销售该语言和组件库的文档。许多 Linux 开发者认为 Motif 许可证意味着它不能为 Linux 等免费操作系统开发软件。

> 注意：Open Group 是一个致力于软件标准的行业组织。他们与开源许可的赞助商无关。事实上，他们承认 Motif 许可证不符合开源要求。

除了工具包和库之外，Motif 发行版还包含了自己的窗口管理器 MWM，原始的 FVWM 外观和体验因此获得了专利。图 6.16 显示了一个示例 MWM 桌面。

#### 图 6.16：一个 MWM 桌面

![](img/968f44a58bee05b3a080631d18e977c9_149_0.png)

### 我需要 Motif 吗？

对于大多数 Linux 用户来说，可能不需要使用 Motif。应该考虑使用 Motif 的用户包括：

- 想要使用 Motif 工具包开发应用程序的开发者。
- 想要运行需要 Motif 库的应用程序的用户。大多数使用 Motif 库的商业应用程序要么在程序中嵌入必要的 Motif 代码（因此用户无需拥有许可证），要么包含了一个完整的运行时库版本。

你可以从 Open Group 网站 `http://www.opengroup.org/` 下载 Open Motif。Metro Link 目前销售一个包含多个不同版本 Motif 工具的包，价格从 99 美元起。

### Motif 的替代方案

与 Linux 世界中的许多其他事物一样，人们正努力制作一个可以免费获取的 Motif 替代替代品，以便让 Linux 开发者和用户无需购买 Motif。Lestiff 项目开发了一个与 Motif 1.2 及以下版本兼容的产品，并遵循 GNU 公用许可证。

Lesstif 尚未达到完全成熟（本文写作时的版本为 0.92.26），但 Lestiff 也可以用于开发某些应用程序和运行某些软件。Lestiff 主页（`http://www.lestiff.org/`）上的 Lestiff FAQ 很快指出 Lestiff 仍然不完整。尽管如此，某些使用 Motif 的应用程序仍可以在 Lestiff 0.92.26 上运行，包括 Mosaic 2.7 和 GNUCash 财务管理器。

你可以免费下载 Motif。那么问题就是：“既然 Motif 已经免费了，为什么还需要 Lestiff？”自由软件基金会认为，新的 Motif 许可证禁止其在大多数当前的 Linux 发行版上使用，因此 Motif 并不是真正的免费。因此，仍然需要 Lestiff 作为 Motif 的替代方案。

### 展望

关于 X Windows 的这段讨论是你向上手使用 Linux 操作系统的第一步。

在接下来的两个章节中，你将使用 Red Hat Linux 7.1 的默认桌面环境：GNOME，掌握 X Windows 接口的基础。你将学习安装 X Windows，并开始尝试使用一些常用的 X Windows 和 GNOME 应用程序。

第 7 章“安装和配置 X Windows”将作为安装和配置 X Windows 的逐步指南。

# 第七章

# 安装和配置 X Windows

- 获取 X Windows
- 准备配置 X Windows
- 使用 Xconfigurator 配置 XFree86
- 使用 Xf86config 配置 XFree86
- 测试你的配置

现在你已经对 X Windows 的内容有了初步了解，是时候安装并配置软件了，以便你的系统能够尽快启动并运行 X Windows。

本章讨论了如果你没有或无法安装与你的 Linux 发行版附带的 X Windows 版本，如何为你的系统获取 X Windows。随后，它描述了如何配置 XFree86，使其在你的计算机上运行得最佳。

## 获取 X Windows

如果你使用的是本书附带的 Red Hat Linux 7.1 拷贝，并且在安装 Linux 时选择了安装了第 4 章“安装 Red Hat Linux 7.1”中建议的全部关键（原文误，应为关键）X Windows 组件，那么你就不需要阅读这一节，因为你已经获取并安装了 X Windows 文件。你可以直接跳到“准备配置 X Windows”部分。

### 从 Red Hat Linux 7.1 CD-ROM 安装

如果你使用的是 Red Hat Linux 7.1 但在安装 Linux 时没有安装 X Windows，那么安装 X Windows 是相当简单的过程。概述的程序依赖于第 14 章“处理文件”中描述的技术来访问你的 CD-ROM 驱动器。

### 使用 rpm

在本节中，你将使用 `rpm`（Red Hat 软件包管理器），这是一个随 Red Hat Linux 以及其他几个发行版提供的工具，用于管理 Red Hat 风格的软件包。

`Rpm` 允许你安装新包、卸载已安装的包并查看包的信息（例如包含哪些文件）。

要安装包，使用以下命令：

```
