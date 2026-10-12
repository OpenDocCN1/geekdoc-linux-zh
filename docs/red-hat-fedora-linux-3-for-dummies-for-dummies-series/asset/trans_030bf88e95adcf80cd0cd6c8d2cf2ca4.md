

# 322 第六部分：附录

如果你只有一块 SCSI 硬盘，驱动器 0 或驱动器 1 通常是你的 C 盘，其他驱动器则按顺序排列。

如果你混合使用 IDE 和 SCSI 控制器，你的 C 盘可能位于其中任何一个上。本附录后面“探索 Windows 9x 或 Windows Me 硬件”和“探索 Windows NT、Windows 2000 或 Windows XP 硬件”这两节将向你展示如何识别你拥有哪些硬盘、它们的类型以及它们连接在哪个控制器上。

由于以下几个原因，我们建议将 Fedora Core 安装在一块单独的硬盘上，使其远离任何 Windows 操作系统。首先，你现在可以以远低于 100 美元（美国）的价格买到 80GB 的硬盘。其次，缩小 MS-DOS 和 Windows 的体积以便让 Fedora Core 以完整形式存在于现有硬盘上是一项相当艰巨（在最坏情况下几乎不可能完成）的任务。此外，虽然从技术上讲你可以将 Fedora Core 发行版拆分并安装在多块硬盘上，但这会使后续更新发行版变得困难。

![图片](img/41feae212f5c6612ff709354891f7b39_339_0.png)

### 关于内存字节的小知识

内存是决定计算机运行速度的最重要因素。计算机使用随机存取存储器 (RAM) 来存储和访问操作系统、程序和数据。Intel 处理器通常拥有以下数量的 RAM（主内存）：

- Linux 可以在少得惊人的内存上运行。经过一些配置且不启用图形界面，你可以在仅拥有 16MB 内存的旧 PC 上运行 Linux；32MB 内存会让操作轻松许多，并显著提升计算机速度。
- 许多人将内存较小的旧 PC 用作简单的网络服务器。

![图片](img/41feae212f5c6612ff709354891f7b39_339_1.png)

- 然而，如果你想运行带图形界面的 Linux，你需要 64MB 内存。
- 拥有 128MB 内存，Fedora Core 可以轻松运行多个图形程序（例如 OpenOffice.org）。
- 进行高强度计算需要 256MB 或更多内存（现在许多 PC 标配 512MB）。使用大型应用程序，如 VMware，拥有足够的内存至关重要。

VMware 虚拟计算机需要自己的 RAM 才能以合理速度运行；例如，运行 Windows 2000 虚拟计算机应至少分配 128MB 内存。如果你想运行多个 VMware 虚拟计算机实例，计划使用 512MB 内存。

![图片](img/41feae212f5c6612ff709354891f7b39_339_2.png)

你可以通过使用笔记本内置 CD-ROM 光驱，或 PCMCIA、USB 或专有 CD-ROM 光驱，在大多数笔记本电脑上安装 Fedora Core。如果你没有这些设备，可以尝试获取一个 PCMCIA 以太网控制器并进行网络安装，前提是网络上的另一个 Linux 系统已安装了 CD-ROM 光驱。如果采取此路径，请查阅 www.redhat.com/support 上的 Fedora Core 安装文档。你还需要一张 Fedora Core 支持的显卡。Fedora Core 支持大多数显卡，通常只有使用最新显卡硬件的前沿笔记本电脑才会出现问题。如果找不到特定驱动程序，你可以使用 Fedora Core 提供的通用 VGA、XGA 或 SVGA 驱动程序。

### 探索你的 Windows 9x 或 Windows Me 硬件

你不必去好莱坞就能被发现——前提是你是一块计算机硬件。Windows 提供了在你家中发现各个部件的工具。本节描述了如何使用 Windows 9x 或 Windows Me（微软仍会在一段时间内提供支持）进行发现过程。

如果你拥有 Windows 9x 或 Windows Me 计算机，请使用本节来探索和显示有关你的计算机的信息。使用无处不在的控制面板。启动你的 Windows 计算机并遵循以下说明：

1. 点击 **Start** 按钮并选择 **Settings: Control Panel**。双击 **System** 图标并选择 **Device Manager** 选项卡。
2. 在屏幕顶部，选择 **View Devices by Connection**。此步骤向你显示所有组件及其相互关系。
3. 在 **System Properties** 对话框中的 **Control Panel** 的 **Device Manager** 选项卡上，选择 **View Devices by Type** 选项。

在列表中，注意某些图标前有加号 (+) 或减号 (−)。加号表示该项已折叠。减号表示该项已展开以显示所有子树。

4. 点击 **plus (+) sign** 以展开列表。

展开列表会显示每个计算机子系统。构成你的计算机的每个设备都会显示出来。右键点击某个设备并选择 **Properties** 选项以显示有关特定设备的信息。

你可以使用 Web 来了解你的计算机。计算机公司在其网站上提供关于其产品的详细信息。前往制造商的网页并查找你计算机的型号。到达你的页面后，寻找 **Specification**（或 **Specs**）链接。

### 探索你的 Windows NT、Windows 2000 或 Windows XP 硬件

发现运行 Windows NT、Windows 2000 和 Windows XP 系统的信息与在 Windows 9x 或 Windows Me 系统进行相同发现过程相似。过程相同，只是到达那里的方式略有不同：

在 Windows NT 和 Windows 2000 计算机上，请遵循以下步骤：

1. 点击 **Start** 按钮并选择 **Settings Control Panel**。然后，在 **Control Panel** 窗口中双击 **System** 图标。
2. 当 **System Properties** 窗口打开时，点击 **Hardware** 选项卡。然后，点击 **Device Manager** 按钮以打开 **Device Manager** 窗口。
3. 点击任何你想查看的硬件子系统的加号 (+)。子菜单打开，显示特定类型的所有设备。
4. **Right-click** 任何硬件子系统并选择 **Properties**。**Properties** 选项向你显示该特定设备的信息。

在 Windows XP 计算机上，请遵循以下步骤：

1. 点击 **Start** 按钮并选择 **My Computer** 选项。
2. **Double-click** **Control Panel** 图标。
3. **Double-click** **System** 图标，选择 **Hardware** 选项卡，然后双击 **Device Manager** 按钮。**Device Manager** 窗口打开。
4. 点击加号 (+) 以显示子系统内的设备。
5. **Right-click** 设备以打开一个菜单，你可以从中选择 **Properties** 选项。**Properties** 窗口打开并显示有关设备的信息。

# 附录 C
让文件档案记录你的一生

## 本附录内容

- 全面了解 Linux 文件和目录
- 导航 Linux 文件系统
- 创建、移动、复制和销毁目录和文件
- 更改文件所有权和权限

在本附录中，我们将大胆地深入 Linux 文件和目录结构。别担心：Linux 虽然过着有结构的生活，但它仍然灵活。经过一点介绍，你可以很快掌握 Linux 的生活方式。

我们还将向你介绍文件类型、子目录、路径和根目录。你还将看到回家的路——到你的主目录。一旦你熟悉了 Linux 文件和目录结构，我们将向你展示如何做出一些更改，例如如何复制和移动文件和目录，以及如何——天哪！——销毁它们。

## 理清 Linux 文件事实

Linux 文件类似于 Unix、DOS、Windows 和 Macintosh 文件。所有操作系统都使用文件来存储信息。文件允许你整理你的东西并分离你的信息。例如，构成本附录的文本存储在一个文件中——每个其他章节也是如此，每个章节都在自己的文件中。随着我们迅速处理长文件，请关注不断跳动的提示符。

## 存储文件

我们假设你知道文件是由文件名标识的信息的离散集合——并且 Linux 可以在目录中存储多个文件，只要文件名称不同。（Linux 将不同目录中同名文件分别存储。）

