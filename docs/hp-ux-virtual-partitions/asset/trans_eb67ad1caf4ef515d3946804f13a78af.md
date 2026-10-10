

## 主菜单：输入命令或菜单

*   `bo p0`
*   是否与 IPL 交互（Y 或 N）?: `N`

从 *P0* 引导后，我们会看到如下示例中所示的 *欢迎使用 HP-UX 安装/恢复流程！* 菜单：

![](img/eff8b9287a5f38c5adf538f24aacf29e_49_0.png)

*欢迎使用 HP-UX 安装/恢复流程！* 菜单是显示的第一个菜单。它提供了系统中硬件的概要。如果您想查看更多详细信息，请选中屏幕右侧的 **H/W Details** 选项。这将带您进入硬件的详细说明列表。其中包括硬件路径、磁盘驱动器容量和 LAN 地址等项目。除了选择 *Install HP-UX*（安装 HP-UX）外，我们在本示例中不会执行其他任何功能。

当我们选择 *Install HP-UX*（安装 HP-UX）时，会看到如下示例中所示的 *用户界面和介质选项* 菜单：

## 用户界面和介质选项

此屏幕允许您从决定是否使用 Ignite-UX 服务器以及您的用户界面偏好的选项中进行选择。

源位置选项：

- [ *] 仅使用介质安装
- [ ] 启用网络的介质（允许使用 SD 仓库...）
- [ ] 基于 Ignite-UX 服务器的安装

- [ ] [推荐用于基本安装]
- [*] 高级安装（推荐用于磁盘和文件系统管理）

    使用所有默认值并继续

> **提示：** 如果您需要调整逻辑卷大小，或者希望在安装期间设置最终的网络参数，您需要使用高级模式（或远程图形界面）。

[ 确定 ] [ 取消 ] [ 帮助 ]

此菜单为您提供仅从介质安装、从介质结合网络上的软件仓库安装，或使用 Ignite-UX 产品的选项。在我们的示例中，我们将仅从介质进行安装。

接下来我们选择 *Advanced Installation*（高级安装），因为这在安装时提供了最大的灵活性。*Guided Installation*（引导式安装）会引导您完成基本的系统配置设置。它仅允许选择少数系统特定选项。*Advanced Installation*（高级安装）具有更大的灵活性，允许设置广泛的系统特定参数。我们将逐步介绍 *Advanced Installation*（高级安装）步骤。

现在显示的界面与 Ignite-UX 使用的界面类似。实际上，除了 Ignite-UX 使用图形用户界面（GUI）而终端用户界面为 TUI 外，它们是完全相同的。图 1-4 显示了此界面。

## 高级安装配置

```text
/opt/ignite/bin/itool

    [ Basic ] [ Software ] [ System ] [ File System ] [ Advanced ]

Configurations: [ HP-UX B.11.11 Default. ->] [ Description... ]
Environments: [ Mission Critical OE-64bit ->] (HP-UX B.11.11)
[ Root Disk... ] SEAGATE ST318203LC, 0/0/1/1.2.0, 17366 M
File System: [ Logical Volume Manager (LVM) with VxFS ->]
[ Root Swap (MB)... ] 1024 Physical Memory (RAM) = 2048 MB
[ Languages... ] English [ Keyboards... ] [ Additional... ]

[ Show Summary... ] [ Reset Configuration ]
[ Go! ] [ Cancel ] [ Help ]
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_51_0.png)

*Advanced Installation*（高级安装）菜单允许您从菜单标签区域中进行选择，并且可以在它们之间来回切换，直到您对选择感到满意为止。

在菜单显示的顶部有五个标签区域：*Basic*（基本）、*Software*（软件）、*System*（系统）、*File System*（文件系统）和 *Advanced*（高级）。按 Tab 键可以突出显示每个标签区域。要选中突出显示的标签区域，请按下 Enter/Return 键。这将显示该标签区域的屏幕。在每个区域中，都有几个可以针对您的特定系统进行修改的参数。以下是每个标签区域的主要功能：

### Basic
- 基本 - 配置和环境信息。

### Software
- 软件 - 选择要安装的可选软件的能力。主要是与引导式安装下出现的相同选项。

### System
- 系统 - 网络参数。也可以通过 `set_params` 命令进行配置。

### File System
- 文件系统 - 磁盘空间分配。

### Advanced
- 高级 - 高级磁盘、文件系统、逻辑卷和卷组参数。

我们将从图 1-4 中所示的 *Basic*（基本）屏幕开始配置我们的系统。

以下讨论了几项特别重要的内容：

- **Configuration**（配置）- 我们使用 *HP-UX B.11.11 Default*（HP-UX B.11.11 默认）。在某些情况下，HP-UX 11i 被称为其原始名称 11.11。
- **Environments**（环境）- 在撰写本文时，有四个 11i 环境可供选择。这是 HP-UX 11i 软件分发方法的一项重大变化。运行环境是使安装 11i 更容易的软件包。我们将选择四个中的第一个，即如图 中所示的最高级或最复杂的运行环境：

![](img/eff8b9287a5f38c5adf538f24aacf29e_52_0.png)

- **Root Disk**（根磁盘）- 根磁盘的默认选择是第一个内部磁盘驱动器，在我们的示例中，该磁盘的路径为 0/0/1/2.0。
- **File System**（文件系统）- 我们被赋予选择 `rootdisk`（非 LVM）配合 HFS、逻辑卷管理器配合 HFS 或逻辑卷管理器配合 VxFS 的选项。如果您尚未审阅本章中逻辑卷管理器部分的内容，在做出此选择之前建议您这样做（LVM 是逻辑卷管理器）。我强烈主张尽可能使用逻辑卷管理器配合 VxFS。
- **Root Swap**（根交换区）- 系统自动选择两倍于主内存大小的数量，或最大 1024 MB。您需要非常仔细地考虑您的主要交换空间。我们示例中的 L-Class 系统有 2GB 内存，我们将采用默认的 1GB 交换空间，如所示。
- **Languages**（语言）- 我们将在系统中安装英语；但是，11i 系统有许多语言可供选择。
- **Additional**（附加）- 这是屏幕右下角的选择项，不是标签区域。在这里，您可以配置诸如第二个交换区、向根卷添加第二个磁盘驱动器以及禁用 DHCP 等设置。在 11i 中，DHCP（动态主机配置协议）与 Ignite-UX 服务器协同工作，自动分配系统名称、IP 地址等。

刚才讨论的 11i 与早期 11.x 版本之间的主要区别在于 *Operating Environments*（运行环境）。11i 是第一个提供 *Operating Environments*（运行环境）的 HP-UX 版本。

转到 *Software*（软件）标签区域，我们发现 11i 安装 CD-ROM 上的软件已被标记为待安装。由于我们选择了 *Mission Critical Operating Environment*（关键任务运行环境），因此有大量软件被自动选中作为此安装的一部分。

图 1-5 显示了我们在 *Software*（软件）标签区域中选中的一些软件。我们选择了 *All*（全部），以便可以看到作为 *Mission Critical Operating Environment*（关键任务运行环境）一部分选中的所有软件。我们可以向下滚动以查看其他软件。

```text
/opt/ignite/bin/itool

Basic || Software || System | File System || Advanced |

| Category | Marked? | Product | Description |
| --- | --- | --- | --- |
| All | Yes | GigEther-00 | PCI/HSC/EPP-HSCGigEther |
| HPUXAdditions | Yes | HPUXBaseAux | HP-UX Base OS Auxilary |
| OrderedApps | No | HprFabric-00 | PCI/HSC HyperFabric Driver |
| Uncategorized | No | J4258BA | Netscape Directory Server |
| | No | J4274AA | HP WebQoS Peak Packaged Ed |
| | No | RAID-00 | PCI RAID; Supptd HW=A5856A |
| | No | TermIO-00 | PCI MUX; Suppt HW=J3592A |

[ Change Depot Location... ]

[ Show Summary... ] | [ Reset Configuration ]

[ Go: ] [ Cancel ] (Help)
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_54_0.png)

您可能想要安装的其他软件可以从安装 CD 中选择。在示例中，前两项已作为 *Mission Critical Operating Environment*（关键任务运行环境）的一部分被自动选中。此时，我们可以在此窗口中选择 *Hyperfabric*（超结构）和 *Netscape Directory Server*（Netscape 目录服务器）等附加软件。请记住，此窗口中显示的软件位于 11i 的核心操作系统 CD-ROM 上。您可能稍后希望从 HP-UX 应用程序 CD 集安装应用程序软件。这是使用软件分发器完成的。本章后面将对用于安装所有 HP-UX 11i 软件的软件分发器产品进行概述。您可能需要查看此概述，以了解其大致概念

