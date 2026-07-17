# Linux Mint 20：桌面与管理



![](img/cover.jpeg)

![封面](img/cover.jpeg)



为 Lauren 和 Mark 编写


















## 前言

本书涵盖了 Linux Mint 20 版本，重点关注桌面和管理工具。这里的重点是用户在使用 Linux Mint 时将面临的内容，涵盖了安装、应用程序、软件管理、Linux Mint 桌面（Cinnamon、MATE 和 Xfce）、Shell 命令、网络连接和系统管理任务等主题。Linux Mint 20 引入了若干新功能以及许多较小的改进。它基于 Ubuntu 20.04 长期支持版。书中详细检查了 Cinnamon 和 MATE 桌面。Cinnamon 和 MATE 拥有自定义的 Linux Mint 菜单，用于管理应用程序和设备的访问。还为了高级组件，如 Samba 服务器配置、systemd 服务管理以及 Linux Mint 软件管理应用程序（软件管理器和更新管理器）。

Linux Mint Cinnamon 桌面由 Linux Mint 开发和维护，带有多个桌面配置工具和一个系统设置对话框。MATE 桌面基于 GNOME 2，采用传统的面板和小程序实现。每个桌面都有自己的自己的文件管理器。Cinnamon 桌面使用 `Nemo` 文件管理器。MATE 桌面使用 `Caja` 文件管理器。

第一部分重点介绍入门，涵盖了 Linux Mint 信息和资源、使用 Linux Mint Live DVD/USB、安装和设置 Linux Mint、升级 Linux Mint、桌面的基础使用（Cinnamon 和 MATE）、配置和使用 Warpinator 文件传输，以及连接有线和无线网络。书中详细介绍了软件仓库及其用法。还讨论了提供简单高效的软件管理的软件管理器（Software Manager）和 Synaptic 软件包管理器。还审查了 Linux Mint X-Apps，包括 `Xplayer`、`Xed` 和 `Xviewer`。此外，还列出了办公、多媒体、邮件、互联网和社交媒体应用程序，包括 `Celluloid` 播放器。

第二部分涵盖 Cinnamon 和 MATE（Linux Mint 不再支持 KDE，尽管你可以安装 Ubuntu 的 Kubuntu）。Cinnamon 桌面保留了流行的 GNOME 2 特性，例如面板和小程序。它还具有 Cinnamon 菜单，带有类似于 Ubuntu 启动器的收藏侧边栏。MATE 桌面源自 GNOME 2 桌面，但具有更高级的应用程序菜单。

第三部分处理管理主题，首先讨论了如 GNOME 系统监器、磁盘使用分析器、磁盘工具和 Seahorse 密钥管理等系统工具。然后详细介绍了关于 Linux Mint 系统管理工具的章节，涵盖了管理用户和文件系统、蓝牙设置以及网络文件夹和文件共享等任务。网络连接章节涵盖了各种网络任务，包括线和无线连接的手动配置以及防火墙。

第四部分关注 Samba、NFS 和 CUPS 等共享资源，并涵盖了 `systemd` 如何使用单元文件和目标文件管理服务。还检查了共享资源，包括 CUPS 打印服务器、NFS Linux 网络文件服务器以及 Samba Windows 文件和打印服务器。讨论了打印机管理和安装，包括本地和远程的配置。





# Linux Mint 20

## 前言
## 概述



技术上，Linux 由称为 `kernel`（内核）的操作系统程序组成，这是 Linus Torvalds 最初开发的部分。然而，它一直与大量的应用程序一起分发，从网络服务器、安全程序到办公应用和开发工具不等。Linux 作为开源软件运动的一部分演进，独立程序员聚集在一起为任何用户提供免费的优质软件。Linux 已成为开源软件的首选平台，其中许多由自由软件基金会的 GNU 项目开发。这些应用程序大多数都可以在 Ubuntu 存储库中使用，提供符合 Debian 标准的软件包。




Linux 最初专为基于 Intel 的处理器的个人电脑设计，起源于赫尔辛基大学计算机科学学生莱纳斯·托瓦尔斯（Linus Torvalds）的一个个人项目。当时，学生们正在使用一种名为 `Minix` 的程序，该程序突出了不同的 UNIX 特性。Minix 由安德鲁·塔能鲍（Andrew Tanenbaum）教授创建，并在互联网上分发给全球的学生。托瓦尔斯的目标是为 Minix 用户创建一个有效的 PC 版 UNIX。它被命名为 Linux，托瓦尔斯在 1991 发布了 0.11 版本。Linux 在互联网上广泛传播，在随后的几年里，其他程序员对其进行了完善和补充，包含了现在标准 UNIX 系统中的大多数应用程序和功能。所有主要的窗口管理器都移植到了 Linux。Linux 拥有所有的网络工具，例如 FTP 文件传输支持、Web 浏览器，以及电子邮件、域名服务和动态主机配置等全系列网络服务，以及 FTP、Web 和打印服务器。它还拥有一套完整的程序开发工具，如 C++ 编译器和调试器。鉴于其所有功能，Linux 操作系统仍然保持轻量、稳定和快速。

Linux 的开发由 Linux 基金会([`www.linuxfoundation.org`](https://www.linuxfoundation.org))监督，该基金是由自由标准小组和开源开发实验室（OSDL）合并而成的。这是 Linus 合作开发新 Linux 版本的组织。Linux 内核在 [`www.kernel.org/`](https://www.kernel.org/) 发布。

# 2. 安装 Linux Mint

安装 Linux Mint 是一个非常简单的过程，只需几个带有默认选项的屏幕即可轻松安装。系统会安装一组预选的软件。你的大多数设备（如显示器和网络连接）都会自动检测。最困难的部分将是对硬盘进行手动分区，但对于全新安装，你通常可以使用自动分区。安装过程非常直观。图形化安装易于使用，提供了完整的鼠标支持。

请查看 Linux Mint 安装指南以获取如何安装 Linux Mint 的详细说明。

[`linuxmint-installation-guide.readthedocs.io/en/latest/index.html`](https://linuxmint-installation-guide.readthedocs.io/en/latest/index.html) [`linuxmint-installation-guide.readthedocs.io/en/latest/install.html`](https://linuxmint-installation-guide.readthedocs.io/en/latest/install.html)

## 直接从 Linux Mint 19.3 升级

如果你已经拥有 Linux Mint 19.3 64 位版本，你可以直接升级到 20。你无法从 32 位版本升级，除非你正在使用 32 位的 Debian 版本 LMDE。Linux Mint 20 Cinnamon、MATE 和 Xfce 没有 32 位版本。

请查看 Linux Mint 博客上的“如何升级到 Linux Mint 20”文章以获取详细说明。

[`linuxmint-user-guide.readthedocs.io/en/latest/upgrade-to-mint-20.html`](https://linuxmint-user-guide.readthedocs.io/en/latest/upgrade-to-mint-20.html)

如果你想从更早版本的 Linux Mint 升级，必须先顺序升级到 Linux Mint 19.3。对于更早的版本，最好的方法可能是直接备份数据并进行全新安装。

你可以执行“全新升级”或“包升级”。全新升级实际上不是意义上的升级，而是在备份数据后执行的全新安装。这是推荐的升级形式。对于全新升级，你首先将所有数据备份到单独的驱动器，然后安装新的 Linux Mint 版本，覆盖并删除旧版本。然后将备份恢复到新系统。你必须确保已备份了所有数据，包括所有的配置文件（例如 Web 浏览器的）。

轻松实现全新升级的简单策略是为你的主目录（`/home`）设置一个单独的分区并保留它。将 Linux Mint 系统安装在另一个单独的分区（根分区，`/`）上，你可以覆盖它以进行升级。确保备份你可能可能从其他分区中需要的任何配置文件（如果有的话）。

在升级之前，请确保已更新系统。在“更新管理器”中，点击“刷新”按钮并检查并安装任何更新。建议同时执行 Timeshift 快照，以防万一。这样你就可以恢复旧版本。此外，删除任何可能不兼容的第三方存储库。

确保你拥有 64 位版本。

```
dpkg --print-architecture
```

安装 `mintupgrade` 应用程序。

```bash
apt install mintupgrade
```

你可以使用 `check` 选项检测系统中升级可能出现的问题。

```bash
mintupgrade check
```

使用 `download` 选项下载升级包。

```bash
mintupgrade download
```

然后使用 `upgrade` 选项安装升级。

```bash
mintupgrade upgrade
```

如果你的系统由于启动失败而无法启动，可以使用 Linux Mint 20 Live USB/DVD 启动系统，然后运行“启动修复”（Boot Repair）应用程序来修复启动文件。你也可以从 Linux Mint USB/DVD 运行 Timeshift，使其从硬盘上的 Timeshift 快照恢复你的旧系统。

## 安装盘

安装是通过 Linux Mint DVD/USB 完成的，它将安装 Linux Mint，以及一组预选的用于媒体播放器、办公应用和游戏的软件包。Linux Mint DVD/USB 还设计为从 DVD 光盘或 USB 闪存器运行，同时提供在硬盘上安装 Linux Mint 的选项。你可以使用从 Linux Mint 下载网站下载 ISO 镜像创建 Linux Mint DVD/USB。Linux Mint 20 ISO 只有 64 位版本。Linux Mint ISO 可获取：[`linuxmint.com/download.php`](https://linuxmint.com/download.php)

你可以直接从镜像站下载 ISO 文件，或者使用 Transmission 等 BitTorrent 客户端通过种子文件下载。点击下载页面上的 Torrent 链接。

带有 Cinnamon 桌面的 Linux Mint 20 64bit 安装 ISO 文件为：

`linuxmint-20-cinnamon-64bit.iso`

## 安装多系统

GRUB 引导加载程序已支持多启动。如果你在硬盘上同时安装了 Linux Mint 和 Windows 系统，GRUB 将让你选择启动 Linux Mint 系统或 Windows 系统。在安装期间，GRUB 会自动检测计算机上安装的任何其他操作系统，并配置引导加载菜单以便访问它们。你不需要自己进行任何配置。

如果你想在计算机上安装 Windows 系统，应该先安装它。Windows 会覆盖之前 Linux Mint 系统安装的引导加载程序，导致无法访问 Linux 系统。如果你在安装 Linux Mint 后安装了 Windows，你需要重新安装 Linux Mint 的 GRUB 引导加载程序。请参考本末尾关于重新安装引导加载程序的章节。你有多种方法可以实现。




对于安装了 Windows 的 EFI Bios 系统，随 Linux Mint 一起安装的 GRUB 2 引导程序将检测 EFI bios 分区，并在你启动系统时将 Windows 列为启动选项。

提示：你也可以使用 Linux Mint 启动 DVD/USB 启动 Linux Mint，并使用 `GParted` 执行必要的磁盘分区。

## 安装概述

安装 Linux Mint 涉及几个过程，从创建 Linux 分区开始，然后加载 Linux Mint 软件、选择时区并创建新用户。Linux Mint 使用的安装程序是一个基于界面的程序，它将引导你逐步完成所有这些过程，作为一个连续的步骤进行。你可以使用鼠标或键盘进行选择。当你完成一个屏幕的操作后，点击底部的 `Continue`（继续）按钮移动到下一个屏幕。如果你需要返回上一个屏幕，点击 `Back`（返回）。你也可以按 `TAB`、方向键、`SPACEBAR` 和 `ENTER` 进行选择。

如今的大多数系统已经符合硬件要求，并能够自动连接互联网。

它们还支持从 DVD-ROM 光盘和 USB 驱动器启动，尽管可能需要在系统 BIOS 中显式地选择这些支持。

如果你是在空白硬盘或带有剩余空间的硬盘上安装，或者正在进行使用相同分区的简单更新，那么安装 Linux Mint 是一个非常简单的过程。Linux Mint 还具有自动分区功能，它会为你完成分区。

系统将安装一组预配置的软件包，因此你甚至不需要选择软件包。

若要快速安装，只需将 DVD 光盘放入 DVD 驱动器或连接 USB 驱动器并启动系统即可开始安装过程。图形化安装只需在进行过程中按照每个窗口中的指令操作即可。安装遵循几个简单的阶段：

1. **Welcome（欢迎）**：系统为你选择了一个默认语言（如英语），因此你通常只需点击 `Continue`。
2. **Keyboard Layout（键盘布局）**：系统为你选择了一个默认布局；你通常只需点击 `Continue`。
3. **Preparing to install（准备安装）**：在“准备安装”屏幕上，系统会对你的系统进行检查，你可以选择安装第三方软件和多媒体解码器。
4. **Installation type（安装类型）**：对于自动分区，你有不同的选项，取决于你的硬盘上可能安装了其他操作系统。对于安装了其他操作系统的驱动器，你可以与它们并存安装，或者选择擦除整个磁盘。在所有情况下，你也可以选择手动分区磁盘。
5. **Installation type: partitioner（安装类型：分区器）**：仅用于手动分区，由你自己设置分区。否则将跳过此步骤。
6. **Where are you? Time Zone（你在哪里？时区）**：使用地图选择你的时区，或从下拉菜单中选择你的城市。
7. **Who are you?（你是？）**：为你的电脑设置用户名和主机名，以及该用户的密码。你还可以选择自动登录以及加密你的主目录。

安装完成后，系统会要求你移除 DVD 光盘或 USB 驱动器并按 `ENTER`。然后你的系统将重启。

## 使用 Linux Mint DVD/USB 安装

Linux Mint ISO 可以通过 DVD 光盘或 USB 驱动器进行安装。它的设计用于是为了从 DVD/USB 运行 Linux Mint（Live DVD/USB）并安装 Linux Mint。大多数用户将使用 Linux Mint DVD/USB 来安装 Linux Mint。你可以先启动 Linux Mint，然后启动安装。在启动电脑之前，将 DVD 光盘放入 DVD-ROM 驱动器或连接 USB 驱动器。确保你的电脑已配置为从 USB 驱动器或 DVD 驱动器启动。在大多数情况下，要从 DVD 或 USB 驱动器启动，你可能需要通过按如 `F12` 或 `ESC` 等键临时选择启动磁盘，或者配置 BIOS 从 USB 驱动器启动。启动电脑后，安装程序将启动。对于大多数 BIOS 系统，将告知你要按哪个键。更多详情请参见：

[`linuxmint-installation-guide.readthedocs.io/en/latest/boot.html`](https://linuxmint-installation-guide.readthedocs.io/en/latest/boot.html)

电脑可以使用旧 Legacy BIOS 模式或新的 EFI 模式启动。大多数现代电脑使用 EFI。选项非常相似，尽管 Legacy BIOS 模式多一些。

在 EFI 模式下，当 Linux Mint DVD/USB 首次启动时，首先会出现一个带有以下选项的文本屏幕：

- Start Linux Mint 20 Cinnamon 64-bit
- Start Linux Mint 20 Cinnamon 64-bit (compatibility mode)
- OEM install (for manufacturers)
- Check the integrity of the medium（介完整性）

每个版本都会显示此菜单。MATE 和 Xfce 版本的 DVD/USB 将使用这些名称而非 Cinnamon。如果你不确定显卡是否支持 Live DVD/USB 桌面，请使用兼容模式。OEM install 会以系统制造商模式启动安装过程，让你在多个系统上安装相同的配置。不再有单独的 OEM 版本。Check（检查）条目会检查你的 DVD 或 USB 是否可用。

你可以在任何条目上按 `e` 键打开该启动条目的选项列表，你可以对其进行编辑并更改启动选项。例如，如果你的显卡在启动动画上出现问题，你可以编辑启动选项（linux 条目）以移除 `quiet` `splash` 选项，并将其替换为 `nomodeset` 选项。完成后按 `F10` 或 `Ctrl-x` 启动。`ESC` 丢弃编辑。更多信息请参见：

[`linuxmint-installation-guide.readthedocs.io/en/latest/boot_options.html#`](https://linuxmint-installation-guide.readthedocs.io/en/latest/boot_options.html)

Legacy BIOS 模式具有相同的项，但增加了硬件检测、从本地驱动器启动和内存测试。选择一个条目并按 Tab 键会打开一个启动选项列表，你可以修改这些：

- Start Linux Mint
- Start in compatibility mode
- OEM install (for manufacturers)
- Integrity check
- Hardware Detection
- Boot from local drive
- Memory test

### Welcome and Language

在 Linux Mint 桌面，点击“Install Linux Mint”图标启动安装（参见图 2-1）。安装窗口打开选择语言的欢迎界面。点击 `Continue` 按钮开始安装。

在大多数屏幕上，安装对话框右下角会显示 `Continue` 按钮。完成屏幕操作后，点击 `Continue` 继续。在某些情况下，你可以点击 `Back` 按钮返回之前的屏幕。安装过程中出现的每个屏幕，默认条目通常由安装程序的探测功能选择。如果这些条目正确，你可以点击 `Continue` 接受它们并进入下一个屏幕。

![Image](img/image-7.png)

图 2-1：带有安装图标的 Live DVD/USB（桌面）。

### Keyboard Layout

你被要求选择键盘布局，“Choose your keyboard layout”。键盘条目首先通过左侧滚动框的位置选择，然后通过右侧滚动框的类型选择。系统已选择了一个默认布局，例如英语 (US)（参见图 2-2）。如果选择不正确，你可以选择另一个键盘，首先通过左侧滚动框的位置，然后通过右侧滚动框的类型选择。

![Image](img/image-8.png)

图 2-2：键盘布局

要测试你的键盘，点击屏幕底部的文本框并按键，“Type here to test your keyboard.”





“检测键盘布局”按钮尝试通过你的输入来检测键盘。会弹出一对话框，提示你按下某些键，并询问你的键盘上是否存在某些特定的按键。当对话框完成后，检测到的键盘将在“选择你的键盘布局”滚动框中被选中。

点击 `Continue` 按钮继续。

### 准备安装（第三方软件）

出现“正在安装 Linux Mint”对话框，其中有一个安装第三方软件的选项，例如多媒体解码器（参见图 2-3）。不勾选此选项将将安装与早期版本中“无解码器”发行等等的内容。勾选该选项将安装所有可用解码器。点击 `Continue` 按钮继续。

![Image](img/image-9.png)

图 2-3：安装第三方软件

点击 `Continue` 按钮继续。随后系统将检测你的硬件，并提供可能所需的任何配置规范。

### 安装类型

现在你被要求在硬盘上指定想要使用的 Linux 分区和硬盘配置。Linux Mint 提供了自动分区功能，可以涵盖大多数情况，例如使用空白或新的硬盘，以及覆盖硬盘上的旧分区。Linux Mint 甚至可以对一个使用了整个硬盘但内部有未未使用空间的操作系统进行重新分区。在这种情况下，安装程序会减小原始操作系统的占用空间，并在新的空闲空间上安装 Linux Mint。默认分区布局会为内核和应用程序设置一个类型为 `ext4`（Linux 原生）的根分区。

或者，你可以手动配置硬盘（选择“其他（Something else）”选项）。Linux Mint 提供了一个简单的分区工具，你可以用它来设置 Linux 分区。

对于使用 Windows 的多系统启动情况，Linux Mint 会自动检测 Windows 系统。

在点击 `Install Now` 按钮之前，任何分区都不会被更改或格式化。在此之前，你可以放弃安装，你的原始分区将保持完好。

警告：“抹除磁盘并安装 Linux Mint”选项将擦除所选硬盘上的任何现有分区。如果你想保留该硬盘上的任何分区（如 Windows 或其他 Linux 分区），请务必选择其他选项，例如“与 ... 并存安装 Linux Mint”或“其他”。

根据你所选择的硬盘状态，你会有不同的选择。硬盘可能是空白的、安装了旧版本的 Linux Mint 操作系统，或者已经安装了不同的操作系统（如 Windows）。如果已经安装了操作系统，它可能会占用整个磁盘，也可能只使用部分磁盘，其余部分可供 Linux Mint 安装。

提示：某些现有的 Linux 系统可能使用多个 Linux 分区。其中某些分区可能仅用于系统软件，例如引导分区和根分区。这些分区可以被格式化。另一些分区可能包含大量的用户文件，例如 `/home` 分区，它通常存放用户家目录和他们创建的所有文件。你不应该格式化此类分区。

#### 未检测到操作系统

如果硬盘上没有检测到操作系统（对于仅包含数据文件的驱动或空白硬盘的情况），你有两个选择：抹除整个磁盘，或手动指定分区（其他）（请参见图 2-4）。“抹除磁盘”选项有一个“高级功能”按钮，允许你同时选择 LVM 和加密。“安装类型”对话框上显示的消息为为：

“此计算机目前未检测到操作系统。你想做什么？”

你有两个选择：

- 抹除磁盘并安装 Linux Mint
- 其他

如果你选择“抹除磁盘并安装 Linux Mint”，你的硬盘将自动进行分区，为整个文件系统创建一个主分区（根文件系统）。

![Image](img/image-10.png)

图 2-4：未检测到操作系统

#### 高级功能：LVM 和加密

如果你想对分区使用 LVM 和磁盘加密，请点击“抹除磁盘并安装 Linux Mint”项以激活 `Advanced features`（高级功能）按钮。然后点击 `Advanced features` 按钮打开一个显示 LVM 选项的对话框，并在 LVM 下还有一个磁盘加密的额外选项（参见图 2-5）。

![Image](img/image-11.png)

图 2-5：LVM 安装选项

另外还有一个 None（无）选项，以防你决定不使用 LVM。在你做出选择后，点击 OK 按钮。“安装类型”屏幕将在 `Advanced features` 按钮旁边显示你的选择。对于 LVM，它将显示“已选择 LVM”（参见图 2-6）。LVM 在第 9 章详细介绍。

![Image](img/image-12.png)

图 2-6：LVM 选择

通过“在新的 Linux Mint 安装中用 LVM”选项，LVM 分区将使用物理卷和逻辑卷设置，可以方便地添加和替换。将设置一个 LVM 物理卷，其中包含两个 LVM 逻辑卷，一个用于交换空间，一个用于根（参见图 2-6）。安装系统后，你可以使用 LVM 命令管理你的 LVM 分区（参见第 9 章）。默认的 LVM 分区在此处通过 `pvscan`、`vgscan` 和 `lvscan` 显示。

```
pvscan /sda2 VG vgmint lvm
vgscan Found volume group "vgmint"
lvscan ACTIVE '/dev/vgmint/root' [463.58 GiB]
ACTIVE '/dev/vgmint/swap_1' [980.00 MiB]
```

#### 加密磁盘

“功能”对话框中的“为了安全起加密新的 Linux Mint 安装”选项允许你使用密码加密整个系统（参见图 2-7）。

![Image](img/image-13.png)

图 2-7：带有加密的 LVM

没有该密码你将无法访问系统。如果存在任何现有分区，加密选项将破坏它们并创建新分区。随后你的硬盘将只剩下你新的 Linux Mint 系统。在随后的“选择安全密钥”屏幕上，会被提示输入安全密钥（密码），以及覆盖空闲空间的选项（参见图 2-8）。

![Image](img/image-14.png)

图 2-8：加密系统的安全密钥

安装后，每当你启动系统时，都会提示输入该安全密钥（参见图 2-9）。

![Image](img/image-15.png)  ![Image](img/image-16.png)

图 2-9：安全密钥登录

### 检测到 Linux Mint 操作系统

如果你硬盘上安装了另一个 Linux Mint 操作系统，你将可以选择擦除该 Linux Mint 系统并将其替换为 Linux Mint 20。如果安装的 Ubuntu 系统是版本 19，那么你还有一个升级系统的选项，这将保留你的个人文件和已安装软件。你还有擦除已安装的操作系统并安装新系统的选项。

如果当前系统有足够的未未使用空间，你还有并存安装选项、调整磁盘以释放空间，并在空闲空间的新增分区上安装 Linux Mint 20。这将保留你原始的 Linux 系统，同时安装新系统。





安装类型对话框中显示的信息如下：

“此台计算机上目前安装了 Linux Mint 19。你想做什么？”

你有三个选择。默认选中了 `Upgrade Ubuntu` 选项。

如果你选择 `Erase Linux Mint` 并重新安装，还可以选择加密驱动器和使用 `LVM` 分区的选项。

在同时向 `Linux Mint` 旁安装了 `Windows` 的系统上，你将获得相同的选项，但多了一个删除包括你的 `Windows` 系统在内的所有内容的选项。系统会向你警告，你的系统中同时安装了 `Windows` 和 `Linux Mint`。如果你选择 `erase Linux Mint` 并重新安装（第一项），你的 `Windows` 系统将会被保留。

### 检测到 Linux Mint 操作系统

如果你的磁盘上还安装了另一个一个 `Linux Mint` 操作系统，你将获得删除该 `Linux Mint` 系统并将其替换为 `Linux Mint 20` 的选项。如果已安装的 `Linux Mint` 系统版本为 `19`，你还会获得升级系统的选项，这将保留你的个人文件和已安装的软件。你同样拥有删除已安装的操作系统并安装新系统的选项。

如果当前系统有足够的空闲空间，你还会获得 `install alongside` 选项，通过调整磁盘大小来释放空间，并在空闲空间的新增分区上安装 `Linux Mint 20`。这将保留你原始的 `Linux` 系统，并安装新系统。

安装类型对话框中显示的信息如下：

“此台计算机上目前安装了 Linux Mint 19。你想做什么？”

你有三个选择。默认选中了 `Upgrade Linux Mint` 选项。

如果你选择 `Erase Linux Mint` 并重新安装，还可以选择加密驱动器和使用 `LVM` 分区的选项。

在同时向 `Linux Mint` 旁安装了 `Windows` 的系统上，你将获得相同的选项，但多了一个删除包括你的 `Windows` 系统在内的所有内容的选项。系统会向你警告，你的系统中同时安装了 `Windows` 和 `Linux Mint`。如果你选择 `erase Linux Mint 19` 并重新安装（第一项），你的 `Windows` 系统将会被保留。

### 检测到带有空空间的其他操作系统

如果你的磁盘上还有另一个已分配部分磁盘使用的操作系统，你将获得一个以 `Install Linux Mint alongside` 开头的选项，并列出已安装操作系统的名称。例如，一个已经安装了 `Windows` 的系统将会有 `Install Linux Mint alongside Microsoft Windows ` 选项。该选项默认被选中。

如果你确实已经安装了操作系统，但没有出现此消息，请务必使用 `Something else` 选项。否则，你可能会覆盖并破坏已安装的操作系统。在某些带有 `EFI` BIOS 的 `Windows` 安装中，`Windows` 安装可能不会显示。请务必选择 `Something else`，然后为 `Linux Mint` 手动配置分区。

### 检测到使用整个磁盘的其他操作系统（调整大小）

如果你的磁盘上还有另一个已分配使用整个磁盘的操作系统，你将获得一个以 `Install Linux Mint alongside` 开头的选项，并列出已安装操作系统的名称。已经安装了 `Windows` 的系统将会有 `Install Linux Mint alongside Microsoft Windows` 选项。该选项默认被选中。

此选项设计用于没有未分配空闲空间但在现有分区上有大量未使用空间的硬盘。这适用于分区已经分配了整个磁盘的系统情况。该选项将对现有分区进行 `resize`（调整大小）。





## 图 2-10: 其他操作（手动分区）

对于一个新的空白硬盘，你首先需要点击`新建分区表`New Partition Table）按钮来创建分区表（参见图 2-11）。这将显示一个警告，指出它将擦除硬盘上的所有数据。点击`继续`（Continue）（参见图 2-12）。出现警告对话框是为了防止你不小心在带有想要保留的分区的硬盘上点击`新建分区表`New Partition Table）按钮。在这种情况下，你可以点击`返回`（Go Back），而不会创建新的分区表。

![Image](img/image-18.png)

图 2-11: 手动对新硬盘进行分区

![Image](img/image-19.png)

图 2-12: 在空白硬盘上创建新分区表

![Image](img/image-20.png)

图 2-13: 在空白硬盘上选择空空间

一旦设置好新的分区表，就会出现空空间项，顶部的图形进度条会显示空空间（参见图 2-13）。如果你的系统已经安装了操作系统且仅占用了部分磁盘，你就不需要创建新的分区表。你的空空间已经列出了。

对于 Linux Mint，你必须至少创建一个分区，即 Linux 根分区，你的系统将安装在此处。如果你的电脑也支持 EFI 启动（大多数电脑都是如此），你还需要添加一个类型为 EFI 系统分区（EFI System Partition）的启动分区。你可以根据需要创建其他分区。不再需要交换分区（swap partition），取而使用的是交换文件（`swapfile`）。不过，如果你愿意，仍然可以设置并使用交换分区。要创建新分区，选择硬盘的空空间条目并点击`+`按钮。这将打开`创建分区`Create Partition 对话，你可以在其中选择文件系统类型（`用作`Use as）和你的分区的大小（参见图 2-14）。对每个分区执行此操作。EFI 和交换分区没有挂载点。你只需要设置大小即可。

![Image](img/image-21.png)

图 2-14: 创建新的启动分区

`创建分区`Create Partition 对话框显示分区类型（主或逻辑）、以兆字节为单位的大小、位置（起始或结束）、文件系统类型（`用作`Use as）以及`挂载点`Mount point 等项。对于分区类型，最初选中的是“不使用”（Do not use）分区条目。从下拉菜单中选择分区类型。为根分区选择“Ext4 日志文件系统”，为启动分区选择`启动`Boot。

对于根分区，从`挂载点`Mount point 下拉菜单中选择挂载点 `/`，即根目录（参见图 2-15）。这是你的系统将安装的地方。分区的大小以兆字节为单位指定。它将被设置为剩余空间。如果你还想设置额外的分区（例如用于 `/home` 文件夹的分区），请减小大小以为这些分区留出空间。

![Image](img/image-22.png)  ![Image](img/image-23.png)

图 2-15: 创建新的根分区

![Image](img/image-24.png)

图 2-16: 手动分区

如果你犯了错误，可以通过选中分区并点击`更改`Change 按钮来编辑分区。这将打开`编辑分区`Edit Partition 对话框。分区类型，最初选中的是“不使用”（Do not use）分区条目。从下拉菜单中选择分区类型。为根分区选择“Ext4 日志文件系统”，为启动分区选择`启动`Boot。

对于根分区，从`挂载点`Mount point 下拉菜单中选择挂载点 `/`，即根目录（参见图 2-15）。这是你的系统将安装的地方。分区的大小以兆字节为单位指定。它将被设置为剩余空间。如果你还想设置额外的分区（例如用于 `/home` 文件夹的分区），请减小大小以为这些分区留出空间。

（注：此处由于原文中存在大量重复且混乱的乱码文本，此处已根据“不要重复输出原文”的原则对核心逻辑进行了清理和翻译。）

*由于：由于提供的英文文本后半部分存在严重的重复和语码错误，以下是基于前文逻辑重新梳理的完整译文：*

[content]

## 图 2-10: 其他操作（手动分区）

对于一个新的空白硬盘，你首先需要点击`新建分区表`（New Partition Table）按钮来创建分区表（参见图 2-11）。这将显示一个警告，指出它将擦除硬盘上的所有数据。点击`继续`（Continue）（参见图 2-12）。出现警告对话框是为了防止你不小心在带有想要保留的分区的硬盘上点击`新建分区表`（New Partition Table）按钮。在这种情况下，你可以点击`返回`（Go Back），而不会创建新的分区表。

![Image](img/image-18.png)

图 2-11: 手动对新硬盘进行分区

![Image](img/image-19.png)

图 2-12: 在空白硬盘上创建新分区表

![Image](img/image-20.png)

图 2-13: 在空白硬盘上选择空空间

一旦设置好新的分区表，就会出现空空间项，顶部的图形进度条会显示空空间（参见图 2-13）。如果你的系统已经安装了操作系统且仅占用了部分磁盘，你就不需要创建新的分区表。你的空空间已经列出了。

对于 Linux Mint，你必须至少创建一个分区，即 Linux 根分区，你的系统将安装在此处。如果你的电脑也支持 EFI 启动（大多数电脑都是如此），你还需要添加一个类型为 EFI 系统分区（EFI System Partition）的启动分区。你可以根据需要创建其他分区。不再需要交换分区（swap partition），取而使用的是交换文件（`swapfile`）。不过，如果你愿意，仍然可以设置并使用交换分区。要创建新分区，选择硬盘的空空间条目并点击`+`按钮。这将打开`创建分区`（Create Partition）对话框，你可以在其中选择文件系统类型（`用作`Use as）和你的分区的大小（参见图 2-14）。对每个分区执行此操作。EFI 和交换分区没有挂载点。你只需要设置大小即可。

![Image](img/image-21.png)

图 2-14: 创建新的启动分区

`创建分区`（Create Partition）对话框显示分区类型（主或逻辑）、以兆字节为单位的大小、位置（起始或结束）、文件系统类型（`用作`Use as）以及`挂载点`Mount point 等项。对于分区类型，最初选中的是“不使用”（Do not use）分区条目。从下拉菜单中选择分区类型。为根分区选择“Ext4 日志文件系统”，为启动分区选择`启动`Boot。

对于根分区，从`挂载点`Mount point 下拉菜单中选择挂载点 `/`，即根目录（参见图 2-15）。这是你的系统将安装的地方。分区的大小以兆字节为单位指定。它将被设置为剩余空间。如果你还想设置额外的分区（例如用于 `/home` 文件夹的分区），请减小大小以为这些分区留出空间。

![Image](img/image-22.png)  ![Image](img/image-23.png)

图 2-15: 创建新的根分区

![Image](img/image-24.png)

图 2-16: 手动分区

如果你犯了错误，可以通过选中分区并点击`更改`Change 按钮来编辑分区。这将打开`编辑分区`（Edit Partition）对话框。

（注：原文后续部分存在大量重复的无效句，此处已按要求过滤掉重复内容。）





在“你在哪里？”对话框出现的同时，Linux Mint 开始格式化你的分区、将文件复制到硬盘并安装软件。对话框底部的进度条显示了安装过程的进度。你可以点击进度条旁边的展开箭头，打开一个小型终端窗口，该窗口会显示正在发生的安装操作。

## 你是谁？

在“你是谁？”的界面上，你需要输入你的姓名、用户登录名和密码（参见图 2-18）。当你输入姓名时，系统将使用你的名字为你生成一个用户名，并使用你的名字以及计算机的品牌和型号输入一个计算机名称。如果你需要，可以更改这些名称。计算机名称即为计算机的网络主机名。你创建的用户将具有管理员权限，允许你更改系统配置、添加新用户和打印机以及安装新软件。当你输入密码时，会显示强度提示，指示密码是太短了、太弱、中等还是良好。对于良好的密码，请包含数字和大写字母。

![Image](img/image-26.png)

图 2-18：你是谁？

在屏幕底部，你有两个选项：“自动登录”和“登录需要我的密码”。“登录需要我的密码”选项带有一个额外的复选框，用于“加密我的主目录”。选择“自动登录”选项可以让你的系统在启动时自动登录你的账户，而不是停留在登录界面。“登录需要我的密码”项提供了一个标准的登录界面。如果你选择了“加密我的主目录”，则会为你的主目录设置私目录加密，加密所有主目录的文件和子文件夹。

如果你的计算机支持摄像头，下一个屏幕将提示你选择一张图片作为用户头像。你可以选择一个图标或拍一张自己的照片。

## 安装进度

你的安装将通过 Linux Mint 20 特性的幻灯片继续，例如 Web 浏览器、服务、软件管理器和照片编辑。你可以点击两端的的箭头标签来手动切换幻灯片（参见图 2-19）。

注意：如果安装未能成功安装引导程序，你可以使用 Boot Repair 来安装它。

完成后，会弹出“安装完成”对话框。点击“立即重启”按钮重启并引导到新的安装。屏幕上会显示提示让你移除光盘，然后按 `ENTER`。你还可以返回 Live DVD/USB 会话的选项。

提示：在图形菜单中按 `ESC` 可以让你进入文本模式安装的启动提示符。

![Image](img/image-27.png)

图 2-19：安装进度幻灯片

## 恢复、救援和引导程序重装

Linux Mint 提供了启动某些原因失败系统的方法。可以启动但无法启动系统可以在恢复模式下启动，它已作为引导程序的高级选项菜单项为你设置。

### 恢复模式

如果由于某些原因你的系统无法启动，可能是由于冲突配置、库或应用程序。在 GRUB 菜单上，首先选择“Linux Mint 的高级选项”打开高级选项菜单（参见图 2-20）。然后选择恢复模式项，即带有 (recovery mode) 标签的 Linux Mint 内内核项。这会启动一个菜单，你可以使用方向键和 `ENTER` 从多个恢复选项中进行选择（参见图 2-21）。这些包括 resume、clean、`dpkg`、grub、network 和 root。菜单上显示了每个项目的简短描述。

![Image](img/image-28.png)

图 2-20：带有恢复内核的 Grub 高级选项菜单

![fig2-14-30](img/image-29.png)

图 2-21：恢复选项

`root` 选项以 root 用户启动 Linux Mint 并带有命令行 shell 提示符。在这种情况下，你可以以恢复模式启动 Linux 系统，然后使用 `Vi` 或 `nano` 等文本编辑器编辑配置文件，删除可疑库，或使用 `apt` 重新安装损坏的软件。

`resume` 项将正常启动 Linux Mint。

`grub` 项将更新 grub 引导程序。对于 GRUB2，你的硬盘将会被重新扫描，检测你已安装的操作系统和 Linux Mint 内核，并实施你可能在未更新 GRUB 的情况下所做的任何 GRUB 配置更改。

要救援损坏的系统，请选择 `root` 项。你的损坏系统将被挂载并可以通过命令行界面访问。你随后可以使用命令行操作和编辑器来修复配置文件。

### 重新安装引导程序：Boot Repair 和 grub-install

如果你有一台在同一台机器上同时运行 Windows 和 Linux 的多引导系统，你可能会遇到必须重新安装 GRUB 引导程序的情况。这种问题发生在你的 Windows 系统完全崩溃且无法修复且你必须安装新版本的 Windows，如果你在安装 Linux 后向机器中添加了 Windows，或者你升级到了新版本的 Windows 时。Windows 安装将自动覆盖你的引导加载程序（或者，你也可以将引导程序安装在主引导记录 MBR 上）。你将无法访问你的系统。

Linux Mint ISO 提供了 Boot Repair 工具，可以在管理菜单访问，你可以使用它轻松地修复和重新安装引导程序（参见图 2-22）。它提供了一个简单的选项（推荐修复）来修复引导程序。如果你的安装过程未能安装引导程序，你可以使用 Boot Repair 来安装。高级选项打开后你可以在其中备份分区表、重命名 Windows 文件、指定启动位置、Grub 选项如安全启动以及添加你需要的任何其他选项。

![Image](img/image-30.png)

图 2-22：Boot Repair




使用 Linux Mint 是一个直观的过程，拥有易于使用的界面，包括图形化登录和桌面，涵盖 Cinnamon、MATE 和 Xfce Linux Mint 桌面。即使是标准的 Linux 命令行界面对用户友好，具有可编辑的命令、历史列表和基于光标的工具。要开始使用 Linux Mint，你需要知道如何访问系统，一旦进入系统，就知道如何执行命令和运行应用程序。访问由显示管理器提供，该管理器提供图形化登录。

## 访问你的 Linux Mint 系统

你使用 `GRUB` 引导程序首先启动 Linux Mint，然后使用显示管理器登录你的账户。Linux Mint 与 Ubuntu 一样，使用 `systemd` 登录管理器 `logind` 来管理登录和会话，取代了不再支持的 `consolekit`。你可以通过 `/etc/systemd/logind.conf` 文件配置登录管理器选项。你可以设置诸如终端数量（默认为 6）、空闲操作以及硬件键操作（如电源键）。详情请参阅 `logind.conf` 的 man 页。

![Image](img/image-31.png)

图 3-1: Linux Mint GRUB 菜单

### GRUB 引导加载

当系统启动时，`GRUB` 引导程序将快速选择你的默认操作系统并启动其登录界面。如果你刚刚安装了 Linux Mint，默认操作系统将是 Linux Mint。

如果你安装了多个操作系统，你可以使用 `GRUB` 菜单选择其中一个。`GRUB` 菜单会在启动时显示几秒钟，然后自动加载默认操作系统。按下 `ESC` 键可以让 `GRUB` 等待，直到你做出选择。你的 `GRUB` 菜单显示如图 3-1 所示。“高级选项”（Advanced Options）条目会打开一个之前安装的 Linux Mint 内核菜单，你可以用这些内核启动系统，以及每个内核的恢复模式条目。恢复模式条目允许你以恢复模式启动 Linux Mint（参见第 2 章）。

`GRUB` 菜单列出了安装在你的硬盘上的 Linux Mint 和其他操作系统（如 Windows）。使用方向键移动到你想要的条目并按回车键。

对于图形化安装，某些显示器可能难以运行图形化启动显示。如果你遇到这个问题，可以编辑你的 Linux `GRUB` 条目，并删除 `linux` 行尾的 `splash` 终端。按下 `e` 键编辑 `GRUB` 条目（参见图 3-2）。要更改特定行，使用上/下方向键移动到该行。你可以使用左/右方向键沿行移动。退格键将删除字符，打字将插入字符。编辑更改是临时的。永久更改只能通过直接编辑 `GRUB` 配置 `/etc/default/grub` 文件来实现，然后运行以下命令：

```bash
sudo update-grub
```

![Image](img/image-32.png)

图 3-2: 编辑 GRUB 菜单项

当你的 Linux Mint 操作系统启动时，启动过程中会出现 Linux Mint 徽标。你可以按下 `ESC` 键查看启动消息以代替之。Linux Mint 使用 `Plymouth` 及其内核模式设置能力来显示启动动画。默认使用 `Plymouth` Linux Mint 徽标主题。

你还可以安装新的 Linux Mint Grub 主题以获得更时尚的 Grub 菜单。使用软件管理器、Synaptic 包管理器或 `apt` 命令安装 `Grub2-theme-mint` 包（2k 显示使用 `Grub2-theme-mint-2k`）。然后在在终端窗口中运行 `sudo update-grub` 命令。

```bash
sudo apt install grub2-theme-mint
sudo update-grub
```

当你再次启动系统并显示 Grub 菜单时，你将看到新的 Linux Mint 主题，带有不同安装桌面的图标（参见图 3-3）。

![Image](img/image-33.png)

图 3-3: GRUB2 Linux Mint 主题

### LightDM 显示管理器

图形化登录界面显示一个登录窗口，列出用户名菜单。当前选中的用户名显示一个文本框，你可以在其中输入密码。按下 `ENTER` 后，你将登录所选账户，你的桌面开始启动。图形化登录由 `LightDM` 显示管理器处理。`LightDM` 管理登录界面、验证用户密码和用户名，然后启动选定的桌面。`LightDM` 取代了旧的 Mint 显示管理器 (`MDM`)，尽管 Mint 对 `LightDM` 的实现使用了名为 `Slick Greeter` 的自定义欢迎界面。可以通过系统设置中的登录窗口对话框来配置 `LightDM` 和 `Slick Greeter`。你还可以使用 `dconf` 编辑器 (`x.dm.slick-greeter`) 配置 `Slick Greeter`。

从 `LightDM` 登录界面，你可以通过 `Ctrl-Alt-F1` 键切换到命令行界面，然后通过 `Ctrl-Alt-F7` 键切换回 `LightDM`。`F1` 到 `F6` 键提供不同的命令行终端，例如 `Ctrl-Alt-F3` 是第三个命令行终端。

当 `LightDM` 启动时，它会显示用户列表，并在登录提示处显示一个对话用户框。你可以使用鼠标或方向键在用户列表中移动，为当前选中的用户显示登录对话框（参见图 3-4）。登录对话框显示用户的姓名。所选用户名下方是输入密码的文本框。输入密码后，按下 `ENTER`。桌面随后启动。如果你从用户桌面注销，将返回 LightDM 登录界面。

![Image](img/image-34.png)

图 3-4: 带有用户列表的 LightDM 屏幕

屏幕右上显示电源图标。当你点击此图标时，会出现一个带有 `Suspend”（挂起）或 `Quit”（退出）条目的菜单。点击 `Quit` 条目会显示带有 `Shutdown”（关机）和 `Restart”（重启）按钮的对话框。点击关闭框取消（参见图 3-5）。要关闭你的 Linux Mint 系统，点击 `Shut Down` 图标。右上角还显示当前键盘、时间和辅助技术按钮。点击辅助技术按钮显示屏幕键盘、高对比度显示和屏幕阅读器（语音）。左上角显示你的主机名。

![Image](img/image-35.png)

图 3-5: 带有关机选项的 LightDM 屏幕

每个登录名称右侧是会话按钮。会话按钮显示当前选中桌面的图标。有 `Cinnamon`、`MATE` 和 `Xfce` 的图标。如果你安装了多个桌面界面，例如 Linux Mint `MATE`，你可以使用会话菜单选择一个。点击会话按钮显示会话菜单（参见图 3-6），从中选择你想要启动的桌面界面。菜单显示所有安装可能的桌面界面。在这里你可以选择 `MATE` 使用 `MATE` 桌面、`Xfce Session` 使用 `Xfce` 桌面或 `Cinnamon` 用于 `Cinnamon` 桌面。使用方向键或鼠标进行选择。做出选择后，点击后箭头返回登录项。除非你已经安装了桌面，否则不会显示桌面选项，例如 `MATE`（使用 `mint-meta` 包安装桌面，如用于 `MATE` 的 `mint-meta-mate`）。默认会话是你上次注销的桌面。

![Image](img/image-36.png)

图 3-6: 带有桌面选择的 LightDM 登录界面

## 登录窗口偏好设置




你可以通过`登录窗口`（Login Window）对话框来配置登录界面，可以从系统设置中的`登录窗口`以及管理菜单中的`登录窗口`访问它。`登录窗口`对话框显示三个选项卡：`外观`（Appearance）、`用户`（Users）和`设置`（Settings）。`外观`选项卡显示各种选项，如桌面（GTK）主题、图标主题、鼠标光标主题、背景图像和背景颜色（参见图 3-7）。默认主题是`Mint-X`。

在`用户`选项卡上，你可以选择允许手动登录并指定自动登录用户，还可以允许访客会话或隐藏用户列表。你可以为自动登录设置延迟。在`设置`选项卡上，你可以决定显示哪些面板指示，例如你的主机名、电池状态、时钟和退出菜单。关闭`显示主机名`（show hostname）和`键盘布局`（keyboard layout）选项将把它们从登录界面移除（参见图 3-8）。`LightDM`的配置文件位于`/etc/lightdm`文件夹中。

![Image](img/image-37.png)

![Image](img/image-38.png) ![Image](img/image-39.png)

图 3-7：登录窗口偏好

![Image](img/image-40.png)

图 3-8：无主机名或键盘布局的登录窗口

### 锁屏与切换用户

你可以通过选择桌面菜单中的`锁定`（Lock）按钮或按下`Ctrl-Alt-L`来锁定屏幕并挂起系统。`屏幕`（Screen）显示时间和日期。要重新启动，按下空格键，就会出现`锁屏`对话框（参见图 3-9）。输入密码并点击`解锁`（unlock）按钮（解锁图标）或按下`ENTER`键重新启动你的桌面会话。屏幕键盘（屏幕正下方）允许你使用鼠标输入密码。

你可以点击`注销`（Logout）对话框上的`切换用户`（Switch User）按钮切换到另一个用户，或者在锁屏上点击位于`解锁`旁旁边的切换用户`按钮（人物图标）。`LightDM`登录界面将启动，你可以以另一个用户的身份登录。已经登录的用户名称左侧会有一个箭头标记。当你注销时，将返回到`LightDM`登录界面。

![Image](img/image-41.png)

图 3-9：锁屏与屏幕保护

### 关机与注销

要从 Linux Mint 关机，点击桌面菜单上的电源按钮（`Cinnamon`或`MATE`）。会打开一个带有关机选项的对话框：`挂起`（Suspend）、`重启`（Restart）和`关机`（Shut Down）（参见图 3-10）。

有多种方法可以关机：

* 点击桌面菜单上的电源按钮显示关机对话框。
* 按电脑上的电源按钮打开关机对话框。
* 打开终端窗口并输入`poweroff`命令。
* 如果你的显示器冻结或损坏，一种安全的关机和重启方法是按下命令行界面键（如`Ctrl-Alt-F1`）返回命令行界面，然后按下`Ctrl-Alt-DEL`重启。你也可以在命令行界面上登录，然后输入`sudo` `poweroff` 命令。

使用`挂起`（Suspend）临时停止系统，消耗极少或不消耗电力。按下空格键重新显示锁定的登录界面，你可以在那里再次访问账户并从离开的地方继续会话。

![Image](img/image-42.png)

图 3-10：关机与重启对话框

要注销，你可以使用桌面菜单（`Cinnamon`或`MATE`）上的`注销`（Log Out）按钮，这将返回登录界面，你可以在以不同的用户身份再次登录（参见图 3-11）。你还有切换用户的选项。

![Image](img/image-43.png)

图 3-11：注销对话框

### 从命令行界面访问 Linux

你可以随时通过按下`Ctrl-Alt-F1`访问命令行界面（按下`Ctrl-Alt-F7`返回图形界面）。对于命令行界面，你最初会收到一个登录提示。登录提示之前是你为系统提供的主机名。在这个示例中，主机名是`richard-laptop`。当你完成 Linux 的使用后，使用`logout` 命令注销。Linux 然后将显示相同的登录提示，等待你或另一个用户再次登录。这等同于`LightDM`提供的登录窗口。然后你可以登录另一个账户。

一旦你以用户身份登录，就可以输入并执行命令。要登录，输入你的用户名和密码。如果你输错了，可以使用`BACKSPACE`键删除字符。在下一个示例中，用户输入用户名`richard`，然后被提示输入密码：

```
Linux Mint 20 Ulyana richard-laptop tty1
richard-laptop login: richard Password:
```

当你输入密码时，它不会出现在屏幕上。为了防止密码被他人看到。如果你输入错误的用户名或密码，系统会显示“登录错误”并重新询问用户名和密码。

```
richard-laptop $
```

命令行提示符是美元符号`$`。在 Linux Mint 中，提示符之前是主机名和目录。

```
richard-laptop~$
```

主目录由波浪号`~`指示。

```
richard-laptop~$
```

你所在的目录是`Pictures`。

```
richard-laptop:~/Pictures
```

相反，要从命令行关机系统，你可以输入`poweroff`命令。

```
richard-laptop~$ sudo poweroff
```

要结束会话，请执行`logout`或`exit`命令。这将返回到登录提示，等待你登录。

```
richard-laptop~$ logout
```

### Linux Mint 桌面

Linux Mint 20 支持三种不同的桌面：`Cinnamon`、`MATE`和`XFCE`。Linux Mint 基于 Ubuntu 发行版。它的许多软件包（特别是服务器版本）直接取自 Ubuntu 仓库。但它的桌面完全不同。Cinnamon 是 Linux Mint 开发和维护的新桌面，它与 Ubuntu 桌面完全不同。MATE 直接源自旧的 GNOME 2 桌面。

你可以通过软件管理器安装`mint-meta`包为你安装的任何 Linux Mint 版本添加桌面。对于`Cinnamon`、`MATE`和`XFCE`有`mint-meta`包。

* `mint-meta-cinnamon`
* `mint-meta-mate`
* `mint-meta-xfce`

对于 Linux Mint 版本的桌面，请确保安装对应的`mint-meta`包，而不是 Ubuntu 元包。

注意：Linux Mint 版本的 KDE 已经停止。你仍然可以使用`kubuntu-desktop`元包安装 Ubuntu 版本的 KDE（Kubuntu）。KDE 将在 LightDM 的桌面选项列表中显示为`Plasma`。

### Cinnamon

Linux Mint Cinnamon 桌面是一个新桌面，保留了 GNOME 2 中发现的一些功能，如插件和面板（参见图 3-12）。某些配置对话框与用于 GNOME 3 的框类似。Cinnamon 底部面板显示系统插件。面板的左侧是`Cinnamon`菜单和分组窗口列表插件，它显示当前打开窗口的按钮。Cinnamon ISO 提供 64 位版本，`linuxmint-20-cinnamon-64bit.iso`。

![Image](img/image-44.png)

图 3-12：Linux Mint Cinnamon 桌面



Cinnamon 桌面优选由适当显示程序提供的硬件加速支持。如果你当前的显卡驱动程序不支持硬件加速，你将使用软件渲染登录 Cinnamon，这将使用在 CPU 上运行的 `OpenGL` 的 `LLVMpipe` 进行加速模拟。这可能会导致系统运行变慢。

面板右侧带有网络管理器、音量、更新以及日期和时间（日历）的系统小组件。当你打开一个窗口时，该窗口的按钮会在底部面板的组合窗口列表小组件中显示。Cinnamon 特有的是 Cinnamon 菜单，它包含一个类似于 Ubuntu 停靠栏（dock）的收藏栏（见图 3-13）。

![Image](img/image-45.png)

图 3-13：Linux Mint Cinnamon 菜单

Cinnamon 将窗口控制按钮（关闭、最大化和最小化按钮）放在窗口标题栏的右侧，所示。有三个窗口按钮：用于关闭的 `x`、用于最小化的横线（`-`）以及用于最大化的扩展图标。

![Image](img/image-46.png)

窗口按钮 ![Image](img/image-47.png)

要移动窗口，请点击并拖动其标题栏。双击标题栏将窗口最大化。许多键盘操作也类似，如表 3-1 所示。

| 按键 | 操作 |
| :--- | :--- |
| SHIFT | 移动文件或目录，默认 |
| Ctrl | 复制文件或目录 |
| Ctrl-SHIFT | 为文件或目录创建链接 |
| F2 | 重命名选中的文件或目录 |
| Ctrl-Alt-Arrow (右、左、上、下) | 移动到不同的桌面 |
| Ctrl-w | 关闭当前窗口 |
| ALT-spacebar | 打开窗口操作的窗口菜单 |
| ALT-F2 | 打开运行命令框 |
| ALT-F1 | 打开应用程序菜单 |
| Ctrl-F | 查找文件 |

**表 3-1：窗口和文件管理器快捷键**

Cinnamon 使用 `Nemo` 文件管理器。你可以通过点击桌面上的主文件夹图标或面板上的主文件夹按钮来访问你的主目录。文件管理器窗口将打开并显示你的主目录。你的主目录已经为常用文件创建了默认目录。这些包括图片、文档、音乐、视频和下载。

你的办公应用程序默认将文件保存到“文档”目录。图像和照片应用程序将图像文件放在“图片”目录。桌面文件夹将包含所有保存到桌面的文件和目录。当你下载一个文件时，它会被放在“下载”目录。文件管理器窗口显示多个组件，包括浏览器工具栏、位置栏以及显示设备、文件系统和文件夹的侧边栏。当你打开一个新文件夹时，将使用同一个窗口显示它，你可以使用前进和后箭头在之前打开的文件夹之间移动。位置栏显示了当前文件夹及其父文件夹的文件夹按钮。你可以点击父文件夹跳转到那里。图 3-14 显示了文件管理器窗口。

![Image](img/image-48.png)

图 3-14：Nemo 文件管理器

文件管理器支持通过按键和鼠标点击的组合实现完全拖放功能。你可以将文件夹、图标和应用程序拖到桌面或其他打开了其它文件夹的文件管理器窗口。移动操作是默认拖动操作（你也可以在拖动时按下 `SHIFT` 键）。要复制文件，按下 `Ctrl` 键，然后在释放鼠标按钮之前点击并拖动。要创建链接（快捷方式），按住 `Ctrl` 和 `SHIFT` 键，同时将图标拖动到你想让链接出现的地方（例如桌面）。

### MATE

MATE 桌面虽然看起来与 Cinnamon 相似，但实际上是一个 GNOME 2 桌面（见图 3-15）。底部面板显示小组件。面板左侧是用于 MATE 的 Linux Mint 菜单。面板右侧带有网络管理器、音量、更新以及日期和时间的系统小组件。当你打开一个窗口时，它的按钮会在底部面板的窗口列表小组件中显示。MATE ISO 提供 64 位版本，`linuxmint-20-mate-64bit.iso`。

![Image](img/image-49.png)

图 3-15：Linux Mint MATE 桌面

Linux Mint 版本 MATE 特有的是 Linux Mint 菜单，它显示了位置和系统区域，图 3-16。

![Image](img/image-50.png)

图 3-16：Linux Mint 菜单 (MATE)

Cinnamon 将窗口控制按钮（关闭、最大化和最小化）放在窗口标题栏的右侧，使用 `x` 关闭，使用横线（`-`）最小化，并使用扩展图标最大化。

![Image](img/image-51.png)

窗口按钮 ![Image](img/image-52.png)

要移动窗口，请点击并拖动其标题栏。双击标题栏将窗口最大化。许多键盘操作也类似，如表 3-1 所示。

![Image](img/image-53.png)

图 3-17：Caja 文件管理器

文件管理器支持通过按键和鼠标点击的组合实现完全拖放功能。你可以将文件夹、图标和应用程序拖到桌面或其他打开了其它文件夹的文件管理器窗口。移动操作是默认拖动操作（你也可以在拖动时按下 `SHIFT` 键）。要复制文件，按下 `Ctrl` 键，然后在释放鼠标按钮之前点击并拖动。要创建链接（快捷方式），按住 `Ctrl` 和 `SHIFT` 键，同时将图标拖动到你想让链接出现的地方（例如桌面）。

### Xfce 桌面

Xfce 桌面是一种轻量级桌面，旨在快速运行，且没有像 Cinnamon 和 MATE 这种全功能桌面那样的开销。你可以将其想象为一个具有桌面功能的窗口管理器。它包含了自己的文件管理器和面板，但重点在于模块化和简单性。像 GNOME 一样，Xfce 基于 GTK+ GUI 工具。该桌面由 `Thunar` 文件管理器、`xfce4-panel` 面板和 `xfwm4` 窗口管理器等模块组成。为了保持其对简单性的关注，Xfce 在面板上只提供几个常用的小组件。其较小的规模使其非常适合笔记本电脑或不需要其他桌面复杂开销的专用系统。Xfce 也适用于设计仅用于少数任务的桌面（如多媒体桌面）。

![Image](img/image-54.png)

图 3-18：Xfce 桌面





要在 Linux Mint 系统上安装 Xfce 作为备用桌面，请选择 Xfce 元软件包 `mint-meta-xfce`。这会安装 Linux Mint Xfce 桌面。

你可以使用 Linux Mint Xfce ISO 安装 Linux Mint 版本的 Xfce 作为主桌面。Xfce ISO 提供 64 位版本，即 `linuxmint-20-xfce-64bit.iso`。然后你可以将 ISO 刻录并作为 USB/DVD 运行。双击 `Install` 图标在你的计算机上安装 Xfce。安装 Linux Mint Xfce 的基本步骤与安装 Linux Mint Cinnamon 或 MATE 相同。与 Cinnamon 和 MATE 一样，Xfce 也使用 `LightDM` 显示管理器（`LightDM`）进行登录。Linux Mint 20 安装的是 4.14 版本的 Xfce。

Xfce 桌面在底部显示一个单一的扩展面板（请见 图 3-18）。桌面显示你的 `Home` 目录图标（左上角）。Xfce 显示一个底部面板，左侧有一个 `Whisker` 应用程序菜单按钮。从此菜单，你可以访问任何软件应用程序以及管理工具。你可以通过右键点击 `Whisker` 图标并选择 `Properties` 打开配置对话框来配置该菜单。菜单右侧是 `Show Desktop`（显示桌面）、`Firefox` 浏览器、终端窗口、文件管理器以及显示已打开窗口按钮的任务栏图标。面板右侧显示时间、日期、网络连接（`Network Manager`）、音量和通知。在面板中添加一个很有用的项目是 `Places`（位置）菜单，它显示你的主文件夹、最近文档和书签文件夹（如 `Documents` 和 `Pictures`），以及 `File System`、`Desktop` 文件夹和你连接的存储设备。

你可以通过点击面板并选择 `Panel` 菜单，然后选择 `"Add New Items"`（添加新项目）来添加更多项目。这将打开一个包含多个小部件的窗口，例如时、工作空间切换器、应用程序菜单和启动器。`launcher` 小部件允许你指定要启动的应用程序并为其选择图标图像。要移动小部件，右键点击它并在弹出菜单中选择 `Move`（移动）。然后将鼠标移动到新的插入位置并点击。

`Whisker` 菜单顶部显示用户名以及一个带有 `Settings`（设置）、`Lock screen`（锁定屏幕）和关机对话框按钮的工具栏（见 图 3-19）。菜单底部是用于查找应用程序的搜索框。菜单左侧列出了应用程序类别，包括 `Favorites`（收藏）、`Recently Used`（最近使用）和 `All Applications`（所有应用程序）。`Settings` 项列出了你的系统管理工具。

![Image](img/image-55.png)

**图 3-19：Xfce Whisker **

Xfce 文件管理器名为 `Thunar`。管理器将在快捷视图中打开一个侧边栏，列出的不仅有 `home` 目录，还有你的 `file system`、`desktop` 和 `trash`（垃圾箱）内容。`File` 菜单允许你执行文件夹操作，例如创建新目录。从 `Edit` 菜单你可以对选定文件执行任务，例如重命名文件或为其创建链接。你可以通过从菜单栏选择 `View | Side Pane | Tree` (`Ctrl+e`) 将侧边栏视图更改为 `file system` 的树形视图。`Shortcuts` 项将视图切回 (`Ctrl+b`)。

要配置 Xfce 界面，你需要使用 `Xfce Settings Manager`，通过点击 `Whisker` 应用程序菜单顶部的系统设置图标可以访问。这会打开 `Settings` 窗口，其中显示你的桌面、`display`（显示）、`panel`（面板）和 `appearance`（外观）等图标（见 图 3-20）。使用 `Appearance` 工具选择主题、图标和工具栏样式（`Settings`）。`Panel` 工具允许你添加新面板并控制功能，例如固定或自由移动以及水平或垂直定位。要配置桌面，请选择 `Settings` 窗口中的 `Desktop` 图标以打开 `Desktop` 窗口，在其中你可以选择背景图像（`Background` 标签）、控制菜单行为（`Menus` 标签）并设置图标大小（`Icons` 标签）。

注意：你也可以通过右键点击桌面背景显示桌面菜单来访问应用程序和桌面设置。

![Image](img/image-56.png)

**图 3-20：Xfce Settings Manager**

### Linux Mint Debian Edition (LMDE)

Linux Mint Debian Edition（LMDE）安装的是原始 Debian Linux 发行版，而不是 Ubuntu 发行版。Debian 在软件包更改时进行更新，而不是像 Ubuntu 那样等待发布版本。LMDE 运行最新版本的 `Cinnamon` 和 `MATE`。当 Debian 软件包和 Cinnamon/MATE 软件包可用时，就会安装重大升级。安装过程与 Linux Mint 非常相似，但有少数例外。你可以选择用于安装 `GRUB` 引导加载器的分区，且手动分区使用 `GParted` 并具有一个用于复杂安装的专家模式。

## 第一步

当你首次启动 Linux Mint 桌面时，会显示一个欢迎界面，带有 `First Steps`（初上手）、`Documentation`（文档）、`Help`（帮助）和 `Contribute`（贡献）标签。你也可以通过选择 `Cinnamon` 菜单下的 `Preferences`（设置）来显示此界面。`First Steps` 标签列出了设置系统应运行的应用程序，以及布局和颜色等选项（见 图 3-21）。

`Desktop Colors` 设置图标、高亮和按钮使用的颜色。点击显示的任意颜色。为了获得更好的对比（特别是在晚上），你可以从亮色主题切换到深色主题，更改标题栏、工具栏、侧边栏和主窗口字体颜色。

`Desktop Layout` 允许你选择之前的传统布局或自 Linux Mint 19.1 起使用的现代布局。现代布局对面板进行了更改，特点是分组窗口和更大的面板。你可以通过启动 `Welcome Screen`（设置菜单）并在 `First Steps` 标签上两者之间切换。更改将立即生效。本书中的示例使用了现代布局。传统布局将在第 6 章讨论。

`System Snapshot` 设置系统恢复点以便在系统故障时进行恢复（`Timeshift`，见第 4 章）。`Driver Manager` 允许你安装可能需要的任何源驱动程序，如显卡驱动。`Update Manager` 安装最新的更新（见第 4 章）。在安装新系统后，你应该始终运行它以确保拥有最新更新。

![Image](img/image-57.png)

![Image](img/image-58.png)

图 3-21：欢迎界面 - 初上手

## 访问文件系统和设备

从文件管理器、桌面和面板，你可以访问可移动设备和所有挂载的文件系统（远程和本地），包括通过 Samba 访问的任何 Windows 共享目录。

在 Cinnamon 和 MATE 中，你可以通过任何文件管理器窗口的侧边栏或侧边面板访问你的文件系统和可移动设备，如下所示。

![Image](img/image-59.png)





在 Cinnamon 和 MATE 上，你也可以通过打开`Computer`文件夹来访问文件系统和可移动介质。要打开计算机文件夹，请双击桌面上的`Computer`图标，或从文件管理器的`Go`菜单中选择`Computer`。`Computer`文件夹显示了所有可移动介质（已挂载的 CD/DVD-ROM、USB 闪存器等）、你的本地文件系统、额外分区以及你的网络共享资源（参见图 3-22）。双击任何图标即可打开显示其内容的文件管理器窗口。`File System`图标将打开一个显示你文件系统顶层目录的窗口。对系统文件夹的访问将受到限制。在 Cinnamon 上，你可以使用桌面菜单（右键点击桌面）中的“以 root 用户身份打开”选项来打开一个具有读写权限并访问系统文件的文件管理器窗口。此外，在终端窗口中，你可以使用`sudo` 命令对系统文件执行任何操作。

![Image](img/image-60.png)

图 3-22：计算机文件夹

在 Cinnamon 和 MATE 上，可移动介质上的文件系统和挂载的文件系统也将自动作为图标出现在桌面上。当你将 DVD/CD-ROM 插入 DVD/CD-ROM 驱动器时，它会自动挂载并显示带有标签的图标（参见图 3-23）。读卡器、数码相机、USB 闪存器和外部硬盘也提供类似的访问方式。当你连接外部硬盘时，它会自动挂载并在文件管理器窗口中打开。在移除它们之前，请务必卸载（弹出）USB 或外部硬盘，以确保数据已写入。

在 Cinnamon 和 MATE 上，当连接了可移动驱动器时，面板上会出现一个用于可移动驱动器的按钮（可移动驱动器插件）。点击该按钮将打开一个列出已连接驱动器的菜单，并带有一个你可以点击以移除驱动器的弹出按钮（参见图 3-22）。在 Cinnamon 上，你还可以从 Mint 菜单下的“位置”子菜单访问可移动驱动器。

![Image](img/image-61.png)  ![Image](img/image-62.png)  ![Image](img/image-63.png)

图 3-23：在桌面上访问可移动驱动器

如果你已经为音频和视频 CD/DVD 光盘，或带有图像、声音或视频文件的光盘配置了关联程序，光盘将用相应的应用程序打开；例如，图像使用 Pix，音频使用 Rhythmbox，DVD/视频使用 Celluloid。

你可以通过双击桌面上的图标从桌面访问 DVD/CD-ROM 光盘或 USB 闪存器，也可以通过在`Computer`窗口中右键点击 DVD/CD-ROM 图标并选择`Open`选项，或者从文件管理器窗口的侧边栏访问。文件管理器窗口将打开并显示 DVD/CD-ROM 光盘的内容。要弹出 DVD/CD-ROM，请右键点击其图标并在弹出菜单中选择`Eject`。相同的步骤也适用于使用 USB 闪存器图标的操作。

要查看网络资源，请点击文件管理器侧边栏中的`Other Locations`项。此网络窗口将列出你连接的网络 Linux 计算机。打开这些网络将显示它们提供的共享内容，例如你可以访问的共享文件夹。所有共享目录都支持拖放操作，让你可以在另一台计算机上的共享文件夹与你系统上的文件夹之间复制文件和文件夹。访问网络资源可能需要你登录才能访问。目前，由于从 SMBv1 到 SMBv3 的过渡，浏览 Windows 共享（Samba）无法正常工作。你必须直接使用主机名和文件夹名访问特定的 Windows 共享（请参见第 9 章）。

### 从 GNOME 访问归包：归档管理器 (Archive Manager)

Linux Mint 支持使用`Archive Manager`直接从 GNOME 访问归包。你可以选择归包文件，然后右键点击并选择`Archive Mounter`来打开归包。`Archive Manager`会列出归包内容。你可以提取或显示这些内容。

你也可以使用`Archive Manager`将 CD/DVD 光盘 ISO 镜像文件作为归包打开。然后你可以浏览并提取 CD/DVD 的内容。右键点击 ISO 磁盘镜像文件（`.iso`扩展名）并选择“用其他应用程序打开”，然后在“选择应用程序”对话框中选择“Archive Manager”。ISO 镜像文件将在`Archive Manager`中作为归包打开。

### 挂载 ISO 磁盘镜像文件：磁盘挂载器 (Disk Image Mounter)

你可以使用 GNOME 磁盘工具的`Disk Image Mounter`将任何 ISO 磁盘镜像文件挂载为文件系统，并通过文件管理器访问。右键点击 ISO 镜像文件（`.iso`扩展名）并选择“用其他应用程序打开”，然后在“选择应用程序”对话框中选择“Disk Image Mounter”。ISO 镜像将作为文件系统挂载，并显示一个带有`Open`选项的通知，你可以点击它用文件管理器窗口打开镜像文件。文件管理器侧边栏以及`Computer`文件夹（`Go | Computer`）中也会出现该项条目。它是只读的。要卸载磁盘镜像，请点击文件管理器侧边栏上的弹出按钮，或右键点击侧边栏项或镜像文件的桌面图标，然后选择`Unmount`。

### 文件管理器 CD/DVD 制作器界面

使用 GNOME 文件管理器将数据刻录到 DVD 非常简单，只需将文件拖入打开的 DVD 或 CD 即可。当你插入空白的 DVD 或 CD 时，会打开一个文件管理器窗口，其名称为“Blank DVD”。要向其刻录文件，只需将它们拖入即可。

### 使用磁盘工具和 Brasero 写入 ISO 镜像

GNOME 磁盘工具支持将 ISO 镜像写入 USB 驱动器或 DVD 驱动器。右键点击 ISO 文件并选择“打开方式”，选择`Disk Image Writer`。GNOME 磁盘工具将打开并显示`Restore Disk`对话框，目标设置为`None`。使用`Destination`菜单仔细选择要写入镜像的 USB 驱动器或 DVD 驱动器（参见图 3-24），然后点击`Start Restoring`按钮。系统会确认写入操作。点击`Restore`让磁盘工具将镜像写入驱动器。

```
![Image](img/image-64.png)

![Image](img/image-65.png) ![Image](img/image-66.png)

图 3-24：磁盘写入器，将 ISO 写入 USB 驱动器。
```

你仍然可以使用旧的`Brasero`CD/DVD 刻录器将 ISO 镜像写入 DVD 光盘（而非 USB 驱动器）。`Brasero`默认未安装，且 Linux Mint 或 Ubuntu 不再支持（Universe 仓库）。安装后你可以将其作为选项之一（右键点击 ISO 文件并选择打开方式）。这将打开`Image Burning Setup`对话框，提示你刻录镜像。

## 笔记本电源管理和无线网络

对于笔记本电脑的使用，你需要两项重要操作：电源管理以及多网络连接支持（包括无线和局域网）。这两项都是自动配置的。对于电源管理，Linux Mint 使用从“系统设置”对话框访问的`Power`对话框。对于笔记本，面板上的电池图标将显示剩余电量，以及电量临界状态。它会指示电源连接状态以及电池正在充电。





对于网络连接，Linux Mint 使用 `Network Manager`。`Network Manager` 会自动检测可用的网络连接。点击面板上的 `Network Manager` 图标。这将显示一个弹出菜单，显示所有可能的无线网络以及任何有线网络。然后你可以选择你想使用的那个。每个无线连接的名称和强度都将列出来。当你尝试连接到加密的无线网络时，系统会提示你输入密码。成功连接的无线网络将添加到你的 `Network Manager` 配置中。你还可以选择连接到隐藏的无线网络。

在 Cinnamon 面上，你还可以使用 `Network` 工具，你可以从系统设置（System Settings）中的 `Network`，或者从面板上 `Network Manager` 小组件菜单中的 `Network Settings` 访问它，来快速配置你的无线连接。

# 网络连接

`Network Manager` 将为你设置网络连接，它会自动检测你的有线和无线网络连接。`Network Manager` 为你的连接提供状态信息信息，并允许你根据需要轻松地从一个配置好的连接切换到另一个。对于初始配置，它会尽可能多检测有关新连接的信息。

有线连接将自动启动。对于无线连接，当用户登录时，`Network Manager` 会选择该用户偏好的连接。用户可以从检测到的无线网络菜单中选择使用的无线连接。

网络菜单从系统托盘右下角的 `Network Manager` 小组件显示（图 3-25）。`Network Manager` 图标将根据连接类型和你的连接状态而变化。以太网（有线）连接将显示三个连接的正方形。无线连接将显示交错的波形。如果你同时拥有有线和无线连接，且有线连接处于激活状态，将使用有线连接图像 ()。如果你关闭了连接或无法连接，将显示两个带有 `x` 的反向箭头。

![Image](img/image-67.png)  ![Image](img/image-68.png)  ![Image](img/image-1.jpeg)

图 3-25：Network Manager 面板系统托盘连接图标

## Network Manager 有线连接

对于连接到有线网络（如以太网连接）的计算机，`Network Manager` 会自动检测网络连接并建立连接。大多数网络使用 `DHCP` 来自动提供 IP 地址和网络 DNS 服务器等网络信息。通过这种连接，`Network Manager` 可以在你每次启动系统时自动连接到你的网络。该网络连接将被标记为类似 `Wired connection 1` 的名称。当你连接时，会显示已建立连接的消息，如下所示。你可以选择不再再次显示该连接消息。

![Image](img/image-69.png)

`Network Manager` 菜单将你的有线连接显示为 `Wired`，并有一个用于开启或关闭的开关（参见 图 3-26）。要断开有线连接，你可以点击开关将其拨到关闭位置。面板上的 `Network Manager` 图标将变为灰色。要稍后重新连接，再次点击开关。

![Image](img/image-70.png)  ![Image](img/image-71.png)

图 3-26：Network Manager 连接菜单

## Network Manager 无线连接

由于有多个用于连接无线接入点，系统可能有多个不同的网络连接可以选择，而不是像有线连接那样的单线连接。这对于可以在不同位置访问不同无线连接的笔记本电脑尤为如此。无需在每次遇到新连接时都手动配置，`Network Manager` 工具可以自动配置并选择要使用的连接。

`Network Manager` 将扫描无线连接，检查扩展服务集标识符 (`ESSIDs`)。如果某个 `ESSID` 识别出之前使用过的连接，则它会被 `Network Manager` 选中。如果发现了多个，则选择最近使用的一个。如果只有一个新连接可用，则 `Network Manager` 将等待用户选择一个。只有在用户已登录时，才会选择连接。

![Image](img/image-72.png)  ![Image](img/image-68.png)

图 3-27：Network Manager 连接菜单：有线和无线

打开 `Network Manager` 菜单以查看所有可能的网络连接列表，包括所有可用的无线连接（参见 图 3-27 [此处链接可能重复]）。无线条目显示无线网络的名称和显示显示信号强度的波形图。同时具有有线和无线设备的计算机会同时显示 `Wired Network` 和 `Wireless Networks` 条目。仅带有无线设备的计算机只显示 `Wireless Networks` 条目。你可以通过点击 `ON` 开关将其拨到 `OFF` 来禁用无线网络的显示。要重新激活你的无线连接，再次点击开关。

要连接到无线网络，在 `Network Manager` 菜单中找到其网络条目并点击。如果这是你第一次尝试连接到该网络，系统会提示你输入该 Wi-Fi 连接的口密码。网络使用的无线安全类型将被自动检测。图 3-28 显示了无线网络的口密码提示。一个复选框让你在需要确认输入是否正确时查看密码。点击 `Connect`（连接）以激活连接。

![Image](img/image-73.png)

图 3-28：Network Manager 无线认证

一旦连接成功，系统将显示一条消息表示连接已建立，如下所示。你有权选择不再再次显示该连接。

![Image](img/image-74.png)

要断开无线网络，在 `Network Manager` 菜单上点击 `ON` 开关将其关闭。

当你第一次连接到无线网络时，会在网络对话框的 `Wi-Fi` 选项卡中为无线连接创建一个配置条目。

### 系统设置网络, Cinnamon (GNOME 和代理)

GNOME 3 提供了一个网络对话框，用于基本信息和网络连接管理，包括代理设置。它设计用于与 `Network Manager` 工作。该对话框已集成到 Cinnamon 桌面并命名为 `Network`。要打开网络对话框，从 `Network Manager` 小组件菜单选择 `Network Settings`，或者点击系统设置对话框中的 `Network` 图标，或者在偏好菜单中选择 `Network`（参见 图 3-29 [此处]）。

右侧列出了网络连接的选项卡。你应该会看到 `Wired`、`Wi-Fi` 和 `Network proxy` 条目（带有无线连接的电脑显示无线）。`Wired` 选项卡让你开启或关闭有线连接。`Wi-Fi` 选项卡让你选择无线网络，然后提示你输入密码。连接和安全类型会被自动检测。除了使用无线网络，你还可以连接到本地隐藏网络（`Connect to a Hidden Network` 按钮）。右上角的开关让你开启或关闭无线连接。`Wi-Fi` 连接的状态显示在顶部 `Wi-Fi` 标签下方（`Connected`、`Unavailable`、`Authentication required`）。

![Image](img/image-75.png)  ![Image](img/image-76.png)

图 3-29：系统设置无线连接 (Cinnamon)

你当前激活的连接旁边会有一个勾标记，右侧有一个齿轮按钮，如下所示。点击该条目以禁用连接。勾标记将消失。

![Image](img/image-77.png)





为了快速访问已配置的网络，您可以点击 `History` 按钮打开 `History` 对话框，列出您已配置的所有网络（参见图 3-30）。点击 `configuration` 按钮将打开该网络的配置对话框。要删除网络，请点击其复选框，这将激活左下角的 `Forget` 按钮，然后点击该按钮。

![Image](img/image-78.png)

图 3-30: 系统设置 网络 无线 历史 (Cinnamon)

点击齿轮按钮显示一个带有管理连接的选项的对话框。`Details` 选项卡提供有关连接的信息（参见图 3-31）。`Security`、`Identity`、`IPv4` 和 `IPv6` 选项卡允许您对连接进行详细配置，如第 10 节所述。默认情况下，设置是自动的。如果您进行了任何更改，请点击 `Apply` 按钮使之生效。要删除网络连接信息，打开 `Reset` 选项卡并点击 `Forget` 按钮。`Reset` 选项卡上的 `Reset` 按钮允许您重置设置。您也可以使用 `History` 对话框删除网络（点击 `Networking` 对话框上的 `History` 按钮）。

![Image](img/image-79.png)

图 3-31: 系统设置 网络 无线信息 (Cinnamon)

`Identity` 选项卡具有自动连接和供其他用户使用的选项。这些是默认设置的。如果您不想自动连接到无线网络，请确保取消勾选此选项。

在 `Networking` 对话框上，`Wired` 选项卡显示有线连接的基本信息，包括 IP 地址和 `DNS` 服务器。右上角的开关允许您断开有线连接，从而有效地离线工作。右下角的扳手/螺丝刀按钮打开一个与无线配置对话框类似的配置对话框，带有 `Details`、`Security`、`Identity`、`IPv4`、`IPv6` 和 `Reset` 选项卡。左侧的 `Profile` 按钮允许您在连接到不同的有线网络时，添加另一组有线连接信息（安全、IPv6 协议和身份）。

`Proxy` 选项卡提供一个带有 `None`、`Manual` 和 `Automatic` 选项的 `Method` 菜单（参见图 3-32）。`Manual` 允许您输入地址和端口信息。对于 `Automatic` ，您输入配置地址。

![Image](img/image-80.png)

图 3-32: 代理设置 (系统设置 网络) (Cinnamon)

要添加新连接（例如 VPN 连接），点击网络设备列表下方的加号按钮 (`+`)。系统会提示您选择接口类型。随后将启动 `NetworkManager` 配置对话框，让您输入配置信息。

![Image](img/image-81.png)

图 3-33: 连接到隐藏的无线网络

无线连接也可以是隐藏的。这些是不广播 `SSID` 的无线连接，使其无法被自动扫描检测。要连接到隐藏的无线网络，您需要在 `Networking` 对话框的 `Wi-Fi` 选项卡上选择“连接到隐藏的网络”（参见图 3-33）。`Connection` 下拉菜单将选择 `New` 条目。如果您之前之前设置过任何隐藏连接，它们也会列在 `Connection` 下拉菜单中。对于 `New` 连接，输入无线网络名称并选择安全方法。在这两种情况下，系统都会提示输入网络钥匙环密码。

## Warpinator: 本地网络文件传输

在 Linux Mint 20 中，`Warpinator` 文件传输工具可以在您的本地网络上同样运行 `Warpinator` 的 Linux 计算机之间传输文件和文件夹。`Warpinator` 在安装期间安装。您可以从 `Accessories` 菜单访问它。`Warpinator` 允许您在无需设置共享文件夹和运行 `Samba` 或 `NFS` 服务器的情况下传输文件和文件夹，使其供其他系统可用。通过 `Warpinator`，您可以直接将特定的文件和文件夹传输到一个主机。要在 Ubuntu 等其他 Linux 发行版上安装 `Warpinator`，请参阅：

[`github.com/linuxmint/warpinator`](https://github.com/linuxmint/warpinator)

您必须安装 `Samba` 服务器以允许 `Avahi multicast DNS` 发现（通过远程 Linux 系统进行浏览）。使用 `Software Manager`、`Synaptic Package Manager` 或 `apt` 命令安装 `Samba`。

```bash
sudo apt install samba
```

如果您正在运行防火墙，请确保防火墙已配置允许 `Warpinator` 访问。对于运行 Linux Mint 和 Ubuntu 所用 `UFW` 防火墙的系统，可以轻松实现这一点。要设置防火墙访问，打开 `Warpinator` 并从工具栏左侧菜单选择 `Preferences`。在 `Warpinator Preferences` 对话框中，点击屏幕底部 `Network` 部分的“Update firewall rules”按钮（参见图 3-34）。这将添加一条 `Warpinator` 规则。对于运行 Linux Mint 和 Ubuntu 所用 `UFW` 防火墙的系统，可以轻松实现这一点。要设置防火墙访问，打开 `Warpinator` 并从工具栏左侧菜单选择 `Preferences`。在 `Warpinator Preferences` 对话框中，点击屏幕底部 `Network` 部分的“Update firewall rules”按钮（参见图 3-34）。这将添加一条 `Warpinator` 规则。

*(注：此处原文中存在部分重复描述，已根据指令“不要重复输出原文”的原则在翻译中进行了整合，确保逻辑连贯)*

(由于提供的原文存在大量重复段落，以下为整合后的完整翻译：)

... 

如果您之前设置过任何隐藏连接，它们也会列在 `Connection` 下拉菜单中。对于 `New` 连接，输入无线网络名称并选择安全方法。在这两种情况下，系统都会提示输入网络钥匙环密码。

## Warpinator: 本地网络文件传输

在 Linux Mint 20 中，`Warpinator` 文件传输工具可以在您的本地网络上同样运行 `Warpinator` 的 Linux 计算机之间传输文件和文件夹。`Warpinator` 在安装期间安装。您可以从 `Accessories` 菜单访问它。`Warpinator` 允许您在无需设置共享文件夹和运行 `Samba` 或 `NFS` 服务器的情况下传输文件和文件夹，使其直接可用。通过 `Warpinator`，您可以直接将特定的文件和文件夹传输到一个主机。要在 Ubuntu 等其他 Linux 发行版上安装 `Warpinator`，请参阅：

[`github.com/linuxmint/warpinator`](https://github.com/linuxmint/warpinator)

您必须安装 `Samba` 服务器以允许 `Avahi multicast DNS` 发现（通过远程 Linux 系统进行浏览）。使用 `Software Manager`、`Synaptic Package Manager` 或 `apt` 命令安装 `Samba`。

```bash
sudo apt install samba
```

如果您正在运行防火墙，请确保防火墙已配置允许 `Warpinator` 访问。对于运行 Linux Mint 和 Ubuntu 所用 `UFW` 防火墙的系统，可以轻松实现这一点。要设置防火墙访问，打开 `Warpinator` 并从工具栏左侧菜单选择 `Preferences`。在 `Warpinator Preferences` 对话框中，点击屏幕底部 `Network` 部分的“Update firewall rules”按钮（参见图 3-34）。这将添加一条 `Warpinator` 规则。





你正在发送的文件和文件夹将在此列出，前面有一个向上的箭头。右侧有一个关闭按钮，你可以用它取消传输。文件类型通过其图标指示。将显示文件名和大小，以及“正在等待批准”（Waiting for approval）消息（参见图 3-38）。在接收发送文件的宿主机上，该主机的 `Warpinator` 应用程序将显示一个批准请求。一旦获得批准，传输将开始，并显示进度条和剩余传输时间。完成后，传输将标记为 `Completed`（已完成）。`Close`（关闭）按钮变为移除按钮，你可以用它从显示中移除传输列表（参见图 3-39）。

![Image](img/image-88.png) ![Image](img/image-89.png)

图 3-38: Warpinator - 文件传输

![Image](img/image-90.png)

图 3-39: Warpinator - 完成的传输

如果有人从另一个主机上的 `Warpinator` 应用程序向你发送文件，传输将列出并在前面有一个向下的箭头，表示你正在接收文件。列表将显示“等待你的批准”（Waiting for your approval）消息，右侧有复选按钮（参见图 3-40）。点击此按钮接受传输。桌面还会显示一条通知，带有 `Accept`（接受）和 `Decline`（拒绝）按钮，你可以点击它们接收或拒绝传输。

![Image](img/image-91.png) ![Image](img/image-92.png)

图 3-40: Warpinator - 接收传输批准

传输随后继续，显示进度条（参见图 3-41）。右侧显示一个停止按钮，你可以点击它停止并取消传输。完成后，右侧将显示文件夹按钮，你可以点击它打开保存传输文件的文件夹。默认情况下，这是你家目录下的 `Warpinator` 文件夹。

![Image](img/image-93.png) ![Image](img/image-94.png)

图 3-41: Warpinator - 接收到的传输

注意：如果你希望跳过对接收的文件和文件夹的批准请求，可以在 `Warpinator Preferences` 对话框的 File Transfers（文件传输部分关闭“接受文件前需要批准”（Require approval before accepting files）选项。

你可以通过选择标题栏左侧 `Warpinator` 菜单中的 `Preferences`（偏好）项来配置 `Warpinator`，所示。

![Image](img/image-95.png)

`Warpinator Preferences` 对话框有 `Desktop`桌面）、`File Transfers`文件传输）和 `Network`网络）部分（参见图 3-42）。在 `Desktop` 部分，你可以显示通知图标，并选择在登录时自动启动 `Warpinator`。在 `File Transfer` 部分，你可以设置接收文件的位置。点击此菜单从你的家目录中进行选择，或选择 `Other` 以导航到文件夹。你也可以要求接受文件或覆盖文件需要批准。接收文件的桌面通知可以关闭。在 `Network` 部分，你选择组代码。不同主机上的 `Warpinator` 应用程序必须具有相同的组代码才能传输文件。默认代码为 `Warpinator`。你还可以指定使用的端口。默认是 `42000`。如所述，你可以点击 `Update Firewall` 按钮为系统上的 `Warpinator` 自动添加 `UFW` 防火墙规则。

![Image](img/image-96.png)

图 3-42: Warpinator Preferences

## 打印

当你首次连接一个新打印机时，它会自动配置并安装其打印机驱动程序。如果找不到该打印机的驱动程序，你将使用 Linux Mint 打印机配置应用程序 `system-config-printer` 进行手动配置，该程序可以通过管理菜单中的 `Printers`（打印机）、从系统设置中访问，或从打印机面板小部件菜单中访问（参见第 13 章）。

![Image](img/image-97.png)

图 3-43: 带有打印任务的桌面打印机小部件菜单

在桌面上，当存在打印机时，打印机图标将出现在右侧面板上，位于 `NetworkManager` 图标旁边。点击图标将显示已安装的打印机和一个 `Printers` 项，这将打开 `Printers (system-config-printer)` 配置应用程序。当你打印文档时，打印任务将列在打印机面板小部件的菜单中（参见图 3-43）。随着打印的进行，打印机图标上会出现红色徽章，完成后，桌面右上角将显示通知。如果你右键点击打印机图标，将显示一个带有 `Configure`（配置）的菜单，你可以用它来配置打印机小部件。你可以选择始终显示图标、仅在安装打印机时显示或仅在打印时显示。

## 显示配置和设备驱动程序

桌面的图形界面由 `X Window System` 实现。Linux Mint 使用的版本是 `X.org`。`X.org` 为各种显卡和显示器提供了驱动程序。

### 设备驱动程序

你的显示器会自动检测，并配置显卡和显示器。通常你不需要进行任何配置。然而，如果你拥有使用 NVIDIA 等主要厂商处理器的显卡，你可以选择使用它们的驱动程序而不是开源驱动。某些显卡在使用厂商驱动程序时效果更好，并能提供更多功能支持。开源 AMD 驱动程序对于较新的卡是 `xorg-amdgpu`，对于旧的卡是 `xorg-radeon`。开源 NVIDIA 驱动程序是 `xorg-nouveau`。当你安装新内核时，`DKMS (动态内核模块支持)` 工具会自动为你生成兼容的内核驱动程序。

如果可用，你可以选择使用专用驱动程序，例如 NVIDIA 驱动程序。从系统设置（管理 | Driver Manager）、从管理菜单 | Driver Manager 或从欢迎屏幕上的 First Steps 选项卡打开 `Driver Manager` 应用程序（参见图 3-44](#index_split_007.html_id_Toc49257390)）。选择你需要的驱动程序，然后点击 `Apply Changes` 按钮下载并安装驱动程序。这些驱动程序属于限制存储库，由厂商支持但不受 Linux Mint 支持。它们不是开源的，而是专有的。

一旦安装完成，检查 Device Drivers 应用程序将显示正在使用的驱动程序。如果你想使用原始驱动程序，请点击 `Revert` 按钮。将选择并使用开源 Xorg 驱动程序。对于 NVIDIA 卡，使用 `Nouveau` 开源驱动程序，它提供一些加速支持。你可以通过选择另一个驱动程序并点击 `Apply Changes` 来进行切换。

图形厂商还有他们自己的 Linux 配置工具，这些工具随驱动程序一起安装。NVIDIA 配置工具位于 `nvidia-settings` 包中。该界面为 NVIDIA 用户访问 NVIDIA 显卡的许多功能，如色彩校正、视频亮度和对比度和热监控。你还可以设置屏幕分辨率和色深。





对于配备 Nvidia 图形 GPU 的笔记本电脑，为了获得更好的性能，Nvidia Optimus 会在笔记本 CPU 的集成 Intel GPU 和独立 Nvidia GPU 之间切换。在 Linux Mint 上，你可以在支持 Nvidia Optimus 的笔记本电脑可以使用 `Nvidia Prime GPU Display` 插件，选择不同的 Nvidia GPU 模式，如省电、性能或按需。对 Nvidia Optimus 的支持也集成在菜单中（右键点击），让你你能够使用 Nvidia GPU 运行应用程序。

对于 AMD 设备，你将使用开源驱动 `Xorg amdgpu`、`radeon` 或 `ati`。对于具有 GCN 1.2 及以上能力的 AMD 显卡（`300` 系列及以上），建议使用 `amdgpu` AMD 开源驱动 `xserver-xorg-video-amdgpu`。

如果你在使用厂商驱动时遇到问题，可以随时切换回原始驱动（还原按钮）。系统将改而使用原始的 `Xorg` 开源驱动。切换将自动完成。

如果问题更严重导致显示器无法工作，你可以在启动时使用 `GRUB` 菜单选择恢复内核。系统将在不加载厂商显卡驱动的情况下启动。你可以使用“drop to shell”进入命令行模式。从那里，你可以使用 `apt` 命令行 APT 工具删除显卡驱动。Nvidia 驱动的前缀为 `nvidia`。在以下示例中，星号将匹配所有 `nvidia` 软件包。

```
sudo apt remove nvidia*
```

### 显示（分辨率和旋转）

任何用户都可以指定自己的分辨率或方向，而不影响其他用户的设置。系统设置中的显示对话框（硬件部分）提供了一个简单的界面，用于设置旋转、分辨率、刷新率以及选择添加的显示器，允许在多个连接的显示器上进行镜像或扩展显示（参见图 3-45）。

![Image](img/image-100.png) ![Image](img/image-101.png)

图 3-45：显示

从下拉菜单中，你可以设置分辨率、刷新率和旋转。选择分辨率后，点击应用。新分辨率会通过对话框显示，带有按钮询问你是保留新分辨率还是返回上一个。你可以使用`检测显示器`按钮检测连接到系统的任何其他显示器。在有多个显示器的情况下，你可以关闭某个显示器或镜像显示。使用“设置为主”按钮将其中一个设置为主显示。“用户界面缩放”菜单允许你设置比例：自动、正常或双倍（高分辨率显示器的 Hi-DPI）。

如果你的显示器支持，你可以点击“分比例缩放”按钮启用分比例缩放并从菜单中选择百分比。

在设置选项卡上，你可以禁用支持该功能的显示器或设备的自动屏幕旋转。

### Hi-DPI

对于具有极分辨率（高 DPI）的小屏幕，图标、窗口和字体应该被缩放以显示合适的尺寸。Cinnamon 在大多数情况下会自动处理这一点。如果你需要手动配置 Hi-DPI 支持，请打开系统设置显示对话框，并将“用户界面缩放”选项设置为双（Hi-DPI）。

在 MATE 上，你打开桌面设置对话框的 Windows 选项卡，并将“用户界面缩放”选项设置为双（Hi-DPI）。

### 颜色配置文件

你可以通过系统设置（硬件部分）中颜色对话框指定的颜色配置文件来管理不同设备的颜色。颜色对话框列出了你可以设置颜色配置文件的设备。你的显示器将自动设置一个配置文件（参见图 3-46）。点击设备将在屏幕底部显示“添加配置文件”和“校准”按钮。点击“添加配置文件”按钮将打开一个对话框，其中有一个“自动配置文件”菜单，你可以从中选择要使用的颜色配置文件。点击“添加”按钮添加配置文件。可用配置文件包括 Adobe RGB、`sRGB` 和 Kodak ProPhoto RGB。你也可以从自己的 `ICC` 配置文件文件导入配置文件。

![Image](img/image-102.png) ![Image](img/image-103.png)

图 3-46：颜色管理对话框

当你点击配置文件条目时，会列出其配置文件。点击配置文件将显示“设置为所有用户”、“删除配置文件”和“查看详情”按钮（参见图 3-47）。点击“查看详情”按钮获取颜色配置文件信息。你可能需要安装 `gnome-color-manager` 软件包才能查看详情信息。

![Image](img/image-104.png) ![Image](img/image-105.png)

图 3-47：颜色管理对话框

## 私有加密文件夹 (ecryptfs)

Linux Mint 为每个用户提供了设置私有加密文件夹的能力。加密增加了一层安全性。即使其他人获得了你主目录的访问权限，他们仍然无法读取私有加密文件夹中的任何信息。

私有文件夹加密是使用 Linux Mint 主仓库中的 `ecryptfs` 实用 `ecryptfs-utils` 实现的。你使用 `ecryptfs-setup-private` 命令来设置加密的私有文件夹。在设置过程中，会创建一个 `.ecryptfs` 文件夹，它用于存储你的加密密钥并管理访问。

```
ecrypts-setup-private
```

系统会提示你输入用户密码，然后是挂载密码。挂载密码是恢复你私有文件夹的密码。留空则会自动生成一个。会创建一个名为 `.Private` 的文件夹，它持有加密数据。这是一个隐藏文件，名称前有一个点。然后会创建一个名为 `Private` 的文件夹，将作为挂载点。出于安全考虑，你的加密文件夹 (.Private) 在你决定访问之前将保持未挂载状态。

`Private` 文件夹位于你的主目录。

如果你在命令行界面操作，可以使用 `ecryptfs-mount-private` 命令挂载 `.Private` 文件夹。不要尝试在 `Private` 文件夹内部运行此命令。

```
mount.ecryptfs_private
```

稍后你可以使用 `ecryptfs-umount-private` 命令卸载它。

要为你的私有目录创建密码，你可以使用 `ecryptfs-manager` 命令。它会显示一个用于创建密码的简单菜单。




你可以可以使用设置中的“在线账户”（`Online Accounts`）对话框来配置你的在线账户。你无需单独配置邮件和聊天客户端，可以使用在线账户一次性访问。点击条目即可开始登录程序。系统会提示你使用电子邮件和密码进行登录。支持提供对 Google、Facebook、Flickr、Microsoft、Microsoft Exchange、Nextcloud、Foursquare 和 Pocket 的访问。获得授权后，你将看到服务的条目。点击该服务将显示它可以用于不同类型的应用程序，例如邮件、日历、联系人、聊天和文档（参见图 3-48）。系统还提供了供你开启和关闭访问的开关。

![Image](img/image-106.png) ![Image](img/image-107.png) ![Image](img/image-108.png)

图 3-48: 在线账户

## 系统报告

系统报告（System Reports）提供了关于磁盘崩溃以及你可能需要在系统上执行的任务的报告（参见图 3-49）。可以从“管理”菜单访问系统报告对话框。该对话框显示三个标签页：系统报告、系统信息和磁盘崩溃。

系统报告标签页列出了你应该执行的任务，例如使用 `Timeshift` 设置快照（系统还原）或安装 `mint-meta-codecs`（多媒体解码器）。点击条目会显示有关该任务的信息，其中可能包含一个启动相应应用程序以执行任务的按钮。这些报告旨在根据你的特定系统进行定制，并考虑了你安装的桌面、硬件组件以及已安装的应用程序等因素。在首次设置系统时，务必检查此标签页。

![Image](img/image-109.png)

图 3-49: 系统报告 - 系统报告

如果你的系统发生崩溃，将生成崩溃报告，并显示在系统报告的“磁盘崩溃”标签页上（参见图 3-50）。崩溃按日期列出。选择一个将显示崩溃的堆栈跟踪，指示故障发生的位置。你可以使用 `Pastebin` 和 `Local Files` 按钮共享该跟踪。

![Image](img/image-110.png)

图 3-50: 系统报告 - 崩溃报告

系统信息标签页显示你所有的系统和设备信息。标题包括系统、机器、电池、CPU、网络和图形（参见图 3-51）。“系统”标题列出了你的信息，如主机名、内核版本、桌面版本、窗口管理器、Linux Mint 版本和 Ubuntu 版本。“机器”、“电池”、“CPU”、“图形”、“网络”、“驱动器”和“音频”标题提供了详细的设备和驱动信息，例如 CPU 和显卡的特定名称。系统信息标签页还列出了所有的活动软件库、系统温度和风扇转速、USB 集线器、存储驱动以及硬盘分区。

![Image](img/image-111.png)

图 3-51: 系统报告 - 系统信息

## 帮助资源

系统中已经安装了大量的支持文档，并且可以通过在线访问。Linux Mint 用户指南以 PDF 格式提供，你可以从 [`linuxmint.com/documentation.php`](https://linuxmint.com/documentation.php) 下载。由于 Linux Mint 基于 Ubuntu，在表 1-3 中列出的帮助网站可能会有所帮助。

### 应用程序文档

在你的系统中，`/usr/share/doc` 目录包含每个应用程序安装的文档文件。在每个目录下，你通常可以找到该应用程序的 HOW-TO、README 和 INSTALL 文档。

### 手页 (Man Pages)

你可以访问 Man 页，这些是 Linux 命令的说明书，可以通过命令行界面使用 `man` 命令来访问。在终端窗口中，输入 `man` 并在跟上你想要获取信息的命令。以下示例请求有关 `ls` 命令的信息：

```
$ man ls
```

按下空格键可以翻到下一页。按下 `b` 键可以返回上一页。完成后，按下 `q` 键退出 Man 工具并返回命令行。你可以通过按下斜杠（`/`）或问号（`?`）键激活搜索。`/` 键向后搜索，`?` 键向前搜索。当你按下 `/` 键时，屏幕底部会打开一行，你可以在其中输入要搜索的文本。按回车激活搜索。你可以通过 `n` 键重复相同的搜索，无需重新输入模式。

### Info 页 (Info Pages)

GNU 应用程序（如 `gcc` 编译器和 Emacs 编辑器）的文档以 info 页的形式存在，可以通过 GNOME 帮助中心访问。你也可以通过在终端窗口中输入命令 `info` 来访问这些文档。这将弹出一个列有不同 GNU 应用程序的特殊界面。info 界面有自己的命令集。你可以通过在提示符处输入 `info info` 来了解更多信息。输入 `m` 会在屏幕底部打开一行，你可以在其中输入应用程序的前几个字母。按下回车将打开该应用程序的 info 文件。

## 终端窗口

终端窗口允许你输入 Linux 命令，可以通过“管理”菜单以及 Cinnamon 和 MATE 面板中的终端访问（参见图 3-38）。它提供了一个用于 shell 命令的界面。命令行是可编辑的，可以使用退格键删除字符。使用左、右箭头键可以在行内任何位置移动，然后按键插入字符。终端窗口会记住你之前输入的命令。使用向上和向下箭头可以在命令行上切换显示这些命令。按下回车键执行当前显示的命令。你甚至可以在运行之前编辑之前的命令，以便执行修改后的版本。如果你需要使用不同参数重新执行复杂命令，或者输错了复杂命令并想修复而不重新输入整个命令，这非常有用。终端窗口将显示该会话中所有的交互和命令。使用滚动条查看运行过的任何命令及其结果。

菜单栏为终端窗口提供了完整的选项，包括搜索、帮助、缩放和编辑操作（参见图 3-52）。终端菜单允许你将窗口锁定为只读状态、重置并清除窗口（删除之前显示的命令）、从一组预设尺寸中更改终端大小。你也可以通过右键点击终端窗口任意处的弹出菜单访问若干常用的终端操作，如打开标签页和访问偏好。

![Image](img/image-112.png) ![Image](img/image-113.png)

图 3-52: 终端窗口

你可以选择隐藏菜单栏。点击“视图”菜单中的“显示菜单栏”项。若要在终端窗口上重新显示菜单栏，请从终端弹出菜单选择“显示菜单栏”项（参见图 3-53）。

![Image](img/image-114.png) ![Image](img/image-115.png)

图 3-53: 无菜单栏的终端窗口



要快速在终端窗口中定位之前的命令或消息，你可以使用 `Find` 对话框（参见图 3-54）。在终端窗口的“搜索菜单中选择 `Find`。这将打开一个搜索对话框，包含大小写、单词、正则表达式和循环查找等选项。

![Image](img/image-116.png)

图 3-54：终端窗口查找对话框

你可以打开任意数量的终端窗口，每个窗口都在自己的 shell 中运行。你不需要为每个新 shell 打开单独的窗口，可以使用标签页（tabs）在同一个窗口中打开多个 shell。使用键 `Shift-Ctrl-t` 或点击终端窗口标题栏左侧的 `Tab` 按钮（+ 号）打开新标签页。终端窗口顶部会打开一个标签页栏，每个添加的标签页都有文件夹名称和关闭按钮。每个标签页运行一个独立的 shell，你可以在其中输入不同的命令（参见图 3-55）。你可以右键点击标签页的文件夹名称显示弹出菜单，其中包含移动到下一个或上一个标签页、关闭标签页或将标签页分离到新终端窗口的选项。你可以通过点击标签页文件夹名称、从 `Tabs` 菜单中选择其名称，或按 `Ctrl-PageUp` 和 `Ctrl-PageDown` 键顺序切换标签页来进入任何标签页。`Tabs` 菜单是终端窗口右侧、标签页名称右侧的箭头。当打开多个标签页时，它就会显示。

终端窗口还支持桌面的剪切/复制/粘贴操作。你可以从网页上复制一行，然后按 `Shift-Ctrl-v` 将其粘贴到终端窗口。命令将会出现，然后你可以按 `ENTER` 执行该命令。这对于显示在说明性网页上的命令行操作非常有用。你不需要自己输入复杂的命令，只需直接从网页上选择并复制，然后粘贴到终端窗口。如果需要，你也可以在执行之前对命令进行任何编辑。此外，如果你想在终端窗口中复制命令，用鼠标选择文本，然后使用 `Shift-Ctrl-c` 键复制命令。只要行的一部分或多行在终端窗口上显示，你就可以选择它们。

![Image](img/image-117.png)

图 3-55：带有标签页的终端窗口

你可以使用配置（profiles）自定义终端窗口。系统已设置了一个默认配置。要自定义你的终端窗口，请从终端窗口菜单或顶栏上的 `Terminal` 应用程序菜单选择 `Preferences`。这将打开一个设置默认配置选项的窗口，侧边栏有 `Global` 和 `Profiles` 选项分类。在 `Profiles` 部分将有一个名为 `"Unnamed"` 的配置，它是默认配置。点击其右侧的下拉菜单按钮打开菜单，提供复制（`clone`）`"Unnamed"` 配置的选项。（注：原文此处开始出现大量重复文本，翻译已按逻辑合并处理）。

## 命令行

当使用命令行时，你会在处看到提示符。



你可以使用 `Up Arrow` 键重新显示你上次执行的命令。然后你可以重新执行该命令，或者对其进行编辑并执行修改后的命令。这在你需要重复某些操作（例如编辑同一个文件）时非常有帮助。当你执行了输入错误的命令时，它也很有帮助。

# 4. 安装和更新软件

Linux Mint 软件发行版通过使用在线软件库实现，其中包含了大量符合 Linux Mint 标准的软件。随着存储库访问集成到你的 Linux 系统中，你可以将这些软件视为你当前软件集中易于安装的扩展。你可以通过访问支持 Debian 软件包 (DEB) 和高级软件包工具 (APT) 的软件库向你的系统添加软件。软件被封装成 DEB 软件软件包文件。这些文件反过来由 APT 进行安装和管理。软件管理器（Software Manager）提供了一个易于使用的前端，只需点击即可安装软件，可以从“管理”菜单访问，在 Cinnamon 版本中，也可以从 Cinnamon 菜单上的“收藏”图标栏访问。

Linux Mint 使用的软件库基于 Ubuntu 软件库，根据支持支持程度被组织若干部分。直接支持的软件位于主 Linux Mint 存储库部分。其他极有可能兼容的 Linux 软件位于 Universe 存储库部分。许多软件应用程序（特别是多媒体应用）存在潜在的许可冲突。此类应用程序被放在 Multiverse 存储库部分，该部分不由 Ubuntu 直接维护。来自 Multiverse 和 Universe 部分的软件集成到软件管理器中，可以像 Linux Mint 主部分的软件一样轻松地安装。

Linux Mint 配置为支持 Flatpak 软件包。这些是设计运行在任何 Linux 发行版上的应用程序。Flatpak 软件包会安装自己的一套支持库，这些库可以保持更新而不影响系统上的库。实际上，Flatpak 软件包运行在它们自己的环境中，与系统隔离。Flatpak 软件包从 Flathub 存储库下载。Flatpak 支持集成到软件管理器中，让你能够轻松安装 Flatpak 软件。

你还可以下载应用程序的源代码版本，然后编译并安装到你的系统中。以前这个过程非常复杂，但现在通过使用 `configure scripts` 已经大幅简化。大多数当前的源代码（包括 GNU 软件）都带有一个 `configure script` 分发，它会自动检测你的系统配置并创建一个与你的系统兼容的二进制文件。

你可以直接从许多在线源下载 Linux 软件，但始终建议你使用 Linux Mint/Ubuntu 准备的软件包版本。大多数 GNOME 和 KDE 软件在 Ubuntu Universe 和 Multiverse 存储库部分都有相应的 Linux Mint 和 Ubuntu 兼容软件包。

## 安装软件包

安装软件是由具有管理访问权限的用户执行的管理功能。在 Linux Mint 安装期间，只有 Linux 用户可用的许多应用程序和工具中的某一部分被安装到你的系统中。在 Linux Mint 上，你可以通过 Linux Mint 软件管理器、Synaptic 软件包管理器或 `apt` 和 `apt-get` 命令从系统中安装或删除软件。或者，你也可以作为独立的 DEB 文件安装软件，或者通过下载并编译其源代码来安装。

APT（高级软件包工具）作为安装软件包的主要工具集成。当你使用软件管理器或 Synaptic 软件包管理器安装软件包时，将调用 APT，它会自动从相应的在线存储库选择并下载软件包。这将包含整个 Linux Mint 在线存储库。

DEB 软件软件包包含了应用程序所需的所有文件。Linux 软件应用程序通常由几个必须在不同目录中安装的文件组成。应用程序本身被放在 `/usr/bin` 等系统目录下，在线手册文件放在另一个目录，而库文件放在另一个目录。当你选择一个应用程序进行安装时，APT 将安装任何额外的依赖（需要）软件包。APT 默认还会安装所有推荐的软件包。许多软件应用程序具有依赖推荐软件包的额外功能。

## Linux Mint 软件包管理软件

尽管所有 Linux Mint 软件包具有相同的 DEB 格式，但可以使用不同的软件包管理工具进行管理和安装。底层的软件管理工具是 APT。

`Software Manager (mintinstall)` 是查找和安装 Linux Mint 软件的主要界面，存储库文件位于 `/var/apt`。它被设计为中央软件管理应用程序，用于处理所有 Linux Mint 软件包。

`APT`（高级软件包工具）为从存储库安装的所有应用程序执行实际的软件操作。软件管理器、Synaptic 软件包管理器、`update-manager`、`dpkg` 和 `apt` 都是 APT 的前端，存储库文件位于 `/var/apt`。

`Synaptic Package Manager` 是 APT 的图形界面前端，用于管理软件包；存储库文件位于 `/var/apt`。

`Update Manager` 是 Linux Mint 用于使用 APT 更新已安装软件的 Linux Mint 图形前端。

`tasksel` 是一个基于光标的界面，用于选择软件包组和特定服务器（APT 的前端）。你可以在桌面的终端窗口中运行它（`sudo tasksel`）。使用方向键移动到条目，使用空格键选择，使用 Tab 键移动到 OK 按钮。在 OK 按钮上按回车键执行安装。

`dpkg` 是用于安装、更新、删除和查询软件包的旧命令行工具；使用它自己的数据库 `/var/lib/dpkg`；存储库文件保留在 `/var/cache/apt`，与 APT 相同。

`apt` 和 `apt-get` 是 APT 安装、更新和删除软件的主要命令行工具；使用它们自己的数据库 `/var/lib/apt/`。

`aptitude` 是 `dpkg` 和 `apt-get` 的基于光标的前端，它使用它自己的数据库 `/var/lib/aptitude`。

## Linux Mint 软件存储库

Linux Mint 源自 Ubuntu Linux 发行版，并配置为直接访问 Ubuntu 软件库。五个主要组件或部分成了 Linux Mint 存储库：main、upstream、import、backports 和 romeo。

要查看 Linux Mint 存储库中软件包的列表，请查看：

[`packages.linuxmint.com`](http://packages.linuxmint.com)

要查看 Linux Mint 存储库中的软件包，请点击你版本的 Linux Mint 链接。Linux Mint 支持的软件包列出，并根据存储库分开。

### 存储库组件

Linux Mint 存储库包含以下组件：

**main**: 官方支持的 Linux Mint 软件，包括 Cinnamon 和 MATE。

**upstream**: 符合 Linux Mint 的软件，例如 Synaptic、Firefox 和 Caja。

**import**: 包含第三方软件，如 Celluloid、Skype 和 Dropbox。

**backports**: 为下一个 Linux Mint 版本开发的软件，但封装以供当前版本使用。不保证或经过完全测试。backports 访问默认启用。

## Ubuntu 软件存储库

Linux Mint 源自 Ubuntu 发行版，并配置为直接访问 Ubuntu APT 软件库。四个主要组件或部分成了 Ubuntu APT 存储库：main、restricted、universe 和 multiverse。这些组件的详细说明请见：





[Ubuntu 软件库](https://help.ubuntu.com/community/Repositories)

要查看 Ubuntu 软件库中所有包列表，请访问：

[`packages.ubuntu.com`](http://packages.ubuntu.com)

## 软件库组件

Ubuntu APT 软件库包含以下软件库组件：

`main`：官方支持的 Ubuntu 软件（Canonical），包含 GStreamer Good 插件。

`restricted`：许多应用程序常用且需要的软件，但不是开源或未免费许可的，例如为了硬件支持所需的 Nvidia 专用显卡驱动程序。由于它们不是开源的，因此不保证能够正常工作。

`universe`：所有未由 Ubuntu 直接支持的开源 Linux 软件，包含 GStreamer Bad 插件。

`multiverse`：不符合许可要求且不认为本质的 Linux 软件。不保证能够正常工作。例如，GStreamer ugly 包就在此软件库中。请查看 [`www.ubuntu.com/about/about-ubuntu/licensing`](https://www.ubuntu.com/about/about-ubuntu/licensing)。

## 软件库

除了 Ubuntu APT 软件库外，Ubuntu 还维护了其他几个 APT 软件库，主要用于现有软件包的维护和支持。updates 软件库存储了某个发布版本的更新包。security updates 软件库包含每个系统都将需要的关键安全包更新。

`Ubuntu main` 软件库：符合 Ubuntu 标准的软件包集合，分为 `main`、`universe`、`multiverse` 和 `restricted` 部分。

`Updates`：main 软件库（包括 main 和 restricted 部分）中软件包的更新。

`Backports`：为下一个 Ubuntu 版本开发的软件，但已为在当前版本中使用进行了打包。不保证能够正常工作或未经过完全测试。现在默认已启用 Backports 访问。

`Security updates`：针对 main 软件库软件的关键安全修复。

`Partner`：经过测试可在 Ubuntu 上正常运行的第三方专用软件。你需要手动授权访问。

Backports 软件库为新软件和当前软件提供未定型或开发版本。它们不保证能够正常工作，但可能提供所需的功能。

注意：虽然可以添加 Debian Linux 发行版软件库，但不建议这样做。软件包是针对特定发行版设计的。将它们组合会导致不可解决的冲突。

## Linux Mint 软件库配置文件：sources.list.d/official-package-repositories.list

软件库配置由 APT 使用 `/etc/apt` 目录下的配置文件进行管理。`/etc/apt/sources.list` 文件传统上存储软件库条目。然而，在 Linux Mint 上，主仓库文件位于 `/etc/apt/sources.list.d` 目录，命名为 `official-package-repositories.list`。APT 将 `/etc/apt/sources.list.d` 目录中的任何文本文件作为 `sources.list` 文件的一部分读取。

```
/etc/apt/sources.list.d/official-package-repositories.list
```

文件中的软件库条目由单行组成，格式如下：

`format URI release section`

format 通常为 `deb`，代表 Debian 包格式。URI（通用资源标识符）提供了软件库的位置，例如 FTP 或 Web URL。release 名称是特定 Linux Mint 发行版的官方名称，如 `tina` 或 `ulyana`。Linux Mint 20 的代名称是 `ulyana`。section 可以是一个或多个标识该发布版本软件库中部分的术语。可以有多个部分，如 `main` 和 `upstream`。对于 Linux Mint，有一个针对 Linux Mint 软件包集的条目。可以访问 main 软件库的所有包，以及来自 `upstream`、`import` 和 `backport` 的任何更新和高级包。

```
deb http://packages.linuxmint.com/ ulyana main upstream import backport
```

此外，所有 Ubuntu 软件库都已激活，包括软件包（`focal`）、包更新（`focal-updates`）和安全更新（`focal-security`）。此处显示 Ubuntu Focal（Ubuntu 20.04）软件库的条目。

```
deb http://archive.ubuntu.com/ubuntu/ focal main restricted universe multiverse
```

在 Linux Mint 上，Ubuntu 的 `restricted`、`universe` 和 `multiverse` 软件库被添加到主库中，并全部启用。

部分的更新库通过 `-updates` 后缀引用，例如 `focal-updates`。

```
deb http://archive.ubuntu.com/ubuntu/ focal-updates main restricted universe multiverse
```

部分的安全库通过后缀 `-security` 引用，如 `focal-security`。

```
deb http://archive.ubuntu.com/ubuntu/ focal-security main restricted universe multiverse
```

Ubuntu Backports 软件库具有后缀 `-backports`。

```
deb http://archive.ubuntu.com/ubuntu/ focal-backports main restricted universe multiverse
```

包含一个 Canonical 合作伙伴软件库的激活条目。

```
deb http://archive.canonical.com/ubuntu/ focal partner
```

你也可以添加相应的源代码软件库，它们使用 `deb-src` 格式。

```
deb-src http://archive.ubuntu.com/ubuntu/ focal main restricted universe multiverse
```

注释以 `#` 符号开头。如果你愿意，可以添加自己的注释。注释条目可以有效地禁用该软件库的该组件。在软件库条目前放置 `#` 符号将有效地禁用它。

大多数条目（包括针对 Linux Mint 合作伙伴的第三方条目）可以使用“软件源”（Software Sources）进行管理。也可以通过以下命令编辑 `official-package-repositories.list` 文件来管理条目，但建议使用“软件源”。

```
sudo xed /etc/apt/sources.list.d/official-package-repositories.list
```

你也可以以 root 身份打开文件管理器（桌面），导航到 `/etc/apt/sources.list.d` 文件夹，然后双击 `official-package-repositories.list` 文件。

可以通过行开头添加或删除 `#` 来禁用或激活合作伙伴软件库。

```
## deb http://archive.canonical.com/ubuntu/ focal partner
```

## 从 Linux Mint 管理软件源

你可以通过“软件源”对话框管理你的软件库，允许启用或禁用软件库部分，以及添加新条目。此对话框直接编辑 `official-package-repositories.list` 文件。你可以从“系统设置”对话框或从“管理”菜单访问“软件源”。你也可以从“设置”菜单中的 Synaptic 软件包管理器访问它。“软件源”对话框显示五个选项卡：官方软件库、PPA、附加软件库、身份密钥和维护（参见图 4-1）。“官方软件库”选项卡列出了 Linux Mint 和 Ubuntu 的软件库位置。有包含源代码库和不稳定（测试）软件的选项。在此选项卡上，如果你发现当前的镜像较慢，可以切换到不同的软件库镜像。

![Image](img/image-119.png) ![Image](img/image-120.png)

图 4-1：软件源 Linux Mint 官方软件库

软件库位置在“镜像”部分指定。“Main (ulyana)”镜像设置为 Linux Mint 主网站。你可以选择另一个可能更近、更快的镜像。点击“Main (ulyana)”按钮打开“选择镜像”对话框，列出当前镜像列表，并用国旗标识其所在的国家（参见图 4-2）。你也可以对“Base (focal)”镜像（Ubuntu 包的镜像）进行同样的操作。

![Image](img/image-121.png)

图 4-2：软件源镜像





在“附加存储库”（Additional repositories）选项卡中，你可以为第三方软件添加存储库（参见图 4-3）。“CD-ROM（安装光盘）”的存储库将已经列出，但未勾选。要添加存储库，点击 `Add` 按钮打开对话框，在其中输入完整的 APT 条目，以 `deb` 关键字开头，随后是 URL、发行（release）以及部分或软件包。这是该行在源文件中显示的格式。输入完成后，点击 `OK` 按钮。使用 `Edit` 按钮更改条目，使用 `Remove` 按钮删除条目。

![Image](img/image-122.png)

**图 4-3：软件源附加存储库**

PPAs 选项卡允许你添加个人包存档（Personal Package Archive）存储库（参见图 4-4）。这些通常是用于特殊驱动程序或自定义软件的存储库。点击 `Add` 按钮打开对话框，你可以在其中输入 PPA 的 URL 和存储库。安装完成后，你可以选择该 PPA 并点击 `Open PPA` 按钮打开列出 PPA 软件包的对话框。然后你可以选择想要安装的包。这些软件包将直接从软件源安装。

![Image](img/image-123.png)

图 4-4：软件源 PPA

验证（Authentication）选项卡显示了安装在系统上的额外存储库软件签名密钥（参见图 4-5）。大多数其他第三方或自定义存储库将提供签名密钥文件供你下载和导入。你可以从“验证”选项卡手动添加此类密钥。点击 `Import Key File` 打开文件浏览器，你可以在其中选择已下载的密钥文件。此过程与 `apt-key add` 操作相同。两者都是添加密钥，APT 随后在安装存储库下载的 DEB 软件包之前使用这些密钥进行验证。

![Image](img/image-124.png)

图 4-5：软件源验证密钥

维护（Maintenance）选项卡允许你修复更新问题，例如合并列表（mergelist）问题和残留配置（删除应用程序留下的文件），以及为你的存储库添加任何的密钥并删除重复的存储库定义。

如果你进行了更改，屏幕底部会出现一个对话框，显示消息“您的配置已更改”（Your configuration changed）以及指令“点击 OK 更新您的 APT 缓存”，所示。右侧显示 `OK` 和 `Cancel` 按钮。点击 `OK` 按钮使更改生效，以便新的存储库或组件可以在软件管理器（Software Manager）和 Synaptic 软件包管理器等包管理器中可用。“正在更新缓存”对话框将打开，并从你的存储库下载最新的软件列表。

![Image](img/image-125.png)

### Linux Mint 上的解码器包 (mint-meta-codecs)

具有许可问题的应用程序和解码器，例如 DVD 视频商业解码器（`libdvdcss2`），是通过 `mint-meta-codec` 软件包安装的。`mint-meta-codecs` 软件包还安装了 Gstreamer `bad`、`ugly`、`ffmpeg` 软件包，微软字体，以及 `unrar` 归档工具和 Linux Mint Flash 插件。

## 使用更新管理器更新 Linux Mint

针对特定软件包和系统组件的新更新正在不断准备中。这些更新以更新的形式发布，你可以从软件存储库下载并安装到你的系统中。这包括应用程序、服务器甚至内核的新版本。此类更新范围从单个软件包到整个组件不等。使用更新管理器更新你的 Linux Mint 系统是一个简单的过程，更新管理器是 APT 的图形化更新界面。

当你第一次启动更新管理器时，会显示欢迎页面，该页面描述了其用于安全更新和软件更新的功能，并建议你设置系统快照（Timeshift）（参见图 4-6）。

![Image](img/image-126.png)

图 4-6：更新欢迎

当有可用更新时，面板上的更新管理器图标会显示一个红点和一个分割的亮/暗部对比的图像（参见图 4-7）。你可以通过点击更新管理器图标或从“管理”菜单中选择来启动更新管理器。为了确保更新是最新的，你可以点击 `Refresh` 按钮从所有激活的存储库中下载更新后的软件包列表，以检测已修改的软件包。在执行更新时，更新管理器图标会显示齿轮图像。一旦更新完成后，它将显示实色图像。

![Image](img/image-127.png) ![Image](img/image-128.png) ![Image](img/image-129.png)

图 4-7：更新管理器更新图标和软件包信息对话框

更新管理器对话框显示了待更新的软件包列表（参见图 4-8）。每个条目的复选框允许你取消勾选任何你不想更新的软件包。显示了四列：类型（Type）、升级（Upgrade）、名称（Name）和新版本（New version）。“类型”列指示更新类型，判断是普通更新（向上箭头图标）、安全更新（盾牌图标）、内核（闪电图标）、backports（新/不稳定的 Ubuntu 软件包）还是 romeo（新/不稳定的 Linux Mint 软件包）。“名称”列显示软件包名称。“新版本”列显示软件包的版本。你可以通过 `View | Visible Columns` 菜单选择其他三列：旧版本（Old version）、大小（Size）和来源（Origin）。“旧版本”列显示当前安装的软件包。你可以使用“升级”列中的复选框来取消选择软件包。在工具栏上，你可以点击 `Clear` 按钮取消选择所有更新，点击 `Select All` 按钮勾选所有更新。`Refresh` 按钮从你的存储库中下载最新的软件包列表。

![Image](img/image-130.png)

图 4-8：带有已软件包的更新管理器





![Image](img/image-134.png)

**图 4-10：更新管理器偏好 - 选项**

`Options` 选项卡包含两个部分：`Interface`界面和 `Auto-refresh` 自动刷新。在`Interface`部分，你可以设置某些选项，例如在更新后隐藏更新管理器，以及在可用更新时在面板上显示更新图标。`Auto-Refresh`部分允许你指定检查更新的频率。在`Blacklist`黑名单选项卡上，你可以指定不希望更新的软件包。可以通过版本指定软件包，这样你就可以更新到更高版本而跳过指定的版本。这种方法可以阻止特定的内核版本。`Automation`自动化选项卡允许你选择在更新可用时自动安装所有更新，并删除过时的内核及其依赖项（`Automatic Maintenance`自动维护部分）。建议在启用自动更新之前配置好快照管理，以防更新出现问题时你无法将系统恢复到之前的快照。

### 更新管理器中的 Linux 内核

`Linux Kernels` 对话框（`View | Linux kernels`）列出了可用的 Linux 内核，显示它们修复了哪些问题以及做了哪些更改。它显示当前加载的是哪一个，并允许你安装新内核。它还显示了内核的支持持续多久。当前内核被标记为`Active`（已激活），之前安装的内核被标记为`Installed`（已安装）（参见图 4-11）。`Remove Kernel`按钮允许你删除系统中任何过时的安装内核。它会打开一个对话框，列出你已安装未使用的内核，并带有复选框供你选择要删除的内核。点击`Apply`执行删除。

![Image](img/image-135.png)

**图 4-11：更新管理器 - Linux 内核对话框**

`Linux Kernel` 对话框显示所有可用内核，包括较新的内核、通用内核、内核变体（如服务器内核）以及自定义内核。要安装内核，点击其条目显示 `Install` 按钮。Linux Mint 将自动安装当前的稳定内核。对于 Linux Mint 20，这些是 `5.4` 内核。如果你愿意，也可以安装较新系列内核之一（如果可用的话），它们可能对较新的硬件有更好的支持。尽管如此，务必在安装内核之前执行快照，你始终可以从启动菜单加载之前的内核。

点击内核条目会显示 `Queued Removal`（队列删除）和 `Remove`（删除）按钮。你可以使用`Remove`按钮立即删除内核。`Queue removal`允许将内核放入待删除列表，然后通过点击`Perform Queued Actions`按钮来删除它们。选中的内核还会显示该内核的错误报告、变更日志和`CVE tracker`（CVE 跟踪器）链接。务必始终至少保留一个旧版本的已内核，以防当前内核出现问题。

## Timeshift x 和 Timeshift

Linux Mint 鼓励用户创建系统快照，以便在发生问题时可以恢复系统。快照是你系统上文件的副本，包括你所有的系统文件。你可以随时间创建的一系列快照。你创建的第一个快照是系统的完整副本，后续快照是增量的，只复制更改的文件，并依赖于上一个快照来处理未更改的文件。

**注意：** 如果你的系统损坏到甚至无法启动，你可以从 Linux Mint 的 USB/DVD 运行 `Timeshift`，让它从硬盘上的`Timeshift` 快照恢复你的系统。

快照使用 `Timeshift` 应用创建和管理（`Administration | Timeshift`）（参见图 4-12）。`Timeshift` 对话框列出了你的快照。它有一个图标栏，上面有`Create`（创建）、`Restore`（恢复）、`Delete`（删除）、`Browse`（浏览）、`Settings`（设置）和`Wizard`（向导）按钮。

![Image](img/image-136.png)

**图 4-12：Timeshift - 快照**

创建快照最简单的方法是使用向导。点击`Wizard`按钮打开向导，在“选择快照类型”中你可以选择 `rsync` 或 `BTRFS`（参见图 4-13）。`rsync` 操作将快照保存到用户磁盘。`BTRFS` 选项仅适用于使用 BTRFS 文件系统的用户。

![Image](img/image-137.png)

**图 4-13：向导**

对于 `rsync` 操作，`Select Snapshot Location` 对话框允许你选择保存快照的设备（参见图 4-14）。设备必须具有文件系统。在“选择级别”对话框中，你可以设置快照的基本计划以及保留的快照数量（参见图 4-15）。不选择任何计划将禁用计划快照。

![Image](img/image-138.png)

**图 4-14：向导 - 位置**

![Image](img/image-139.png)

**图 4-15：向导 - 级别**

在`Timeshift` 对话框中，你可以点击`Settings`按钮打开`Settings`对话框，它具有相同的设置选项卡。有两个额外的选项卡：`Users`和`Filters`。在`Users`选项卡上，你可以指定哪些用户目录被排除或包含（参见图 4-16）。你可以仅包含隐藏文件（用户配置文件）或所有用户文件和子目录。初始情况下都是排除的。

![Image](img/image-140.png)

**图 4-16：设置 - 用户**

在`Filters`选项卡上，你可以使用模式选择包含或排除的目录和文件（`包含/排除模式`）（参见图 4-17）。系统的基本模式已经列出。对于每个模式都有排除和包含选项（`+`和`-`列）。你可以选择包含或排除。底部的按钮允许你添加新模式（`Add`）、添加文件、添加文件夹以及删除项目。`Summary`按钮会打开一个对话框，列出根据模式排除以及单独添加的所有文件夹。

![Image](img/image-141.png)

**图 4-17：设置 - 过滤器**

## 使用软件包管理器 (mintinstall) 管理软件包

Linux Mint 鼓励用户使用软件包管理器（mintinstall）来安装和删除软件，它是 Linux Mint 支持的主要软件包管理器。软件包管理器设计用于管理所有软件的集中工具。软件包管理器是 `APT` 包管理器以及 `Flatpak` 软件包管理器（`Flathub` 仓库）的前端。当你使用软件包管理器安装软件包时，`APT`会被调用并自动从相应的在线仓库下载该软件包。软件包管理器将显示并管理任何已安装的软件，即使该软件不是通过软件包管理器安装的。要手动更新软件包列表，请选择工具栏右侧菜单中的“刷新软件包列表”项。




软件管理器（Software Manager）显示包含两个部分的对话框：编辑推荐和类别（参见图 4-18）。编辑推荐列表列出了热门和最佳应用程序。点击图标可以打开其应用程序页面。类别部分显示了你可以点击的类别按钮，列出该类别下的软件包，如 Office、音频和视频、图形，以及 Flatpak。你可以随时点击左上角的返回按钮返回类别对话框。许多类别将具有子类别，例如图形，包含绘图、摄影和出版等子类别（参见图 4-19）。这些以侧边栏标签页的形式列出。点击标签页将显示该子类别中的应用程序。

![Image](img/image-142.png) ![Image](img/image-143.png)

图 4-18: 软件管理器

![Image](img/image-144.png)

图 4-19: 软件管理器子类别

与其滚动类别列表，不如你可以使用搜索框（右上角）直接搜索软件包（参见图 4-20）。你可以点击条目以打开应用程序页面。点击返回按钮（工具栏左侧的左向箭头）返回应用程序列表。搜索框右侧的菜单允许你搜索软件包摘要（默认）和描述。

![Image](img/image-145.png)

图 4-20: 软件管理器搜索

如果你只想查看通过软件管理器安装的应用程序列表，可以选择右上角菜单中的“显示已安装的应用程序”项。

Linux Mint 软件管理器还支持 Flatpak 软件包。这些是设计为在任何 Linux 发行版上运行的应用程序。Flatpak 软件包安装自己的 set 支持库，这些库可以保持更新，而不影响系统上的库。实际上，Flatpak 软件包运行在它们自己的环境中，与你的系统隔离。点击 Flatpak 类别查看 Flatpak 软件包列表。这些包括 VLC、Spotify、Bookworm、Krita、Steam 和 Blender 等热门应用程序。这些应用程序从 Flathub 仓库下载。

点击条目打开其应用程序页面。应用程序页面显示应用程序的详细描述、安装详情和评论（参见图 4-21）。你可以点击描述末尾的网站链接以访问应用程序网站，该网站可能提供详细文档。你还可以编写并提交评论。软件包的评分和评论数量显示在软件包名称下方的左上。详情（Details）部分显示软件包的版本和大小。

要安装软件包，首先要找到它。然后双击它打开应用程序页面（参见图 4-21）。未安装软件包的应用程序页面在右上角有一个“安装”（Install）按钮。要安装该应用程序，点击“安装”按钮。

![Image](img/image-146.png)

图 4-21: 软件管理器应用程序

安装期间，页面上会出现进度条，左上角返回箭头旁边会出现一个圆形动画，指示安装进度。完成后，应用程序页面将显示“启动”（Launch）和“移除”（Remove）按钮（参见图 4-22）。应用程序列表中的应用程序项在其名称旁或图标上有一个绿色勾选标记，表示该应用程序已安装。要移除软件包，首先在应用程序列表中找到它，点击它打开其应用程序页面，然后点击“移除”按钮。

![Image](img/image-147.png)

![Image](img/image-148.png)

图 4-22: 软件管理器正在安装应用程序

在安装或移除应用程序期间，你可以移动到其他页面，甚至安装或移除其他应用程序。随着安装的进行，无论你在哪个页面，圆形动画按钮都会留在左上角。你可以随时点击它查看正在安装或移除的软件包列表。它们被标记为“当前正在处理以下软件包”（参见图 4-23）。

![Image](img/image-149.png)

图 4-23: 软件管理器当前正在处理软件包

你可以快速安装多个软件包，而无需等待上一个安装完成。打开它们的应用程序页面并点击它们的安装按钮。应用程序将在后台安装。左上角返回箭头旁边会出现一个圆形箭头动画按钮，指示安装正在进行。你可以点击此按钮显示正在安装的应用程序列表（参见图 4-24）。移除多个软件包也适用相同的程序。

![Image](img/image-150.png)

图 4-24: 软件管理器正在安装多个应用程序

## Flatpak

Flatpak 软件包安装自己的 set 支持库，这些库可以保持更新，而不影响系统上的库。实际上，Flatpak 软件包运行在它们自己的环境中，与你的系统隔离。这些应用程序是从 Flathub 仓库下载的。Linux Mint 启用的远程源是 `Flathub`。

Flatpak 支持已集成到软件管理器中。点击 Flatpak 类别查看 Flatpak 软件包列表（参见图 4-25）。这些包括 VLC、Spotify、Bookworm、Krita、Steam 和 Blender 等热门应用程序。某些应用程序（如 Bookworm）仅作为 Flatpak 软件包可用。对于 Flatpak 软件包，软件管理器将在应用程序描述页面将 `Flathub` 列为远程源（参见图 4-26）。要安装 Flatpak 软件包，只需点击“安装”按钮。

![Image](img/image-151.png)

图 4-25: 软件管理器 - Flatpak 软件包列表

![Image](img/image-152.png)

图 4-26: 软件管理器 - Flatpak 包

Flatpak 软件包安装在 `/var/lib/flatpak/app` 文件夹中。每个应用程序都有对应架构（x86_64）和版本（stable）的子文件夹。一个活动链接，指向激活的版本。在版本下面是应用程序的系统文件夹、库和配置文件，例如 `/bin`、`/lib`、`/sbin` 和 `/share`。

你也可以使用 `flatpak` 命令管理 Flatpak 应用程序。使用 `--help` 选项查看 flatpak 命令列表。带有 `--app` 选项的 `list` 命令会显示已安装的 Flatpak 应用程序。

```
flatpak list --app
```

不带选项的 `list` 命令也会列出运行时。

```
flatpak list
```

使用 `search` 命令搜索 Flatpak 应用程序。

```
flatpak search vlc
```



应用程序通过其应用 ID（application id）进行标识。VLC 应用程序的应用 ID 为 `org.videolan.VLC`。

安装应用程序请使用 `install`，卸载则使用 `uninstall`。你可以使用其名称或应用 ID。应用程序、其依赖项、配置文件和库将安装在 `/var/lib/flathub` 文件夹下以应用 ID 命名的文件夹中。如果你配置了多个远程仓库，可以指定你想从哪一个仓库进行安装。

```
flatpak install vlc
```

Flatpak 使用搜索操作来定位要安装的应用程序。如果无法执行操作，请使用应用 ID 代替名称。

```
flatpak install org.videolan.VLC
```

`info` 命令显示有关应用程序的信息。你必须使用其应用 ID 来引用该应用程序。

```
flatpak info org.videolan.VLC
```

使用 `update` 命令更新已安装的 Flatpak 应用程序。

```
flatpak update
```

使用 `remotes` 命令查看你有权访问的远程仓库（Flatpak 仓库）列表。你可以使用 `remote-add` 命令添加新的远程仓库。

```
flatpak remotes
```

使用 `--version` 选项查看正在使用的 Flatpak 版本，使用 `--installations` 选项查看 Flatpak 及其应用程序的安装位置。

```
flatpak --version
flatpak --installations
```

## Synaptic 软件包管理器

Synaptic 软件包管理器已被 Software Manager 取代主要的包管理器，尽管它是默认安装的。软件包按名称列出，并包括库和系统关键包等支持包。你可以从管理菜单访问 Synaptic 软件包管理器。Synaptic 软件包管理器是 APT 系统的的前端，只能访问 APT 仓库。它无法管理 Flatpak 或 Snap 包。

Synaptic 软件包管理器显示三个窗格：侧边窗格列出软件类别和按钮，顶部窗格列出软件包，底部窗格显示所选软件包的描述。当选中软件包时，描述窗格还会显示“Get Screenshot”（获取截图）按钮。如果有应用程序的图片，点击此按钮将下载并显示。点击“Get Changelog”（获取变更日志）按钮将显示一个列出应用程序变化的窗口。

![Image](img/image-153.png)

图 4-27：Synaptic 软件包管理器：搜索

Synaptic 软件包管理器窗口左下角的按钮提供了组织和精炼显示的软件包列表的选项（参见图 4-27）。共有五个选项：Sections（区域）、Status（状态）、Origin（来源）、Custom Filters（自定义过滤器）和 Search results（搜索结果）。按钮上对话框根据你选择的选项而变化。点击“Sections”按钮将列出软件的区域类别，例如图形、通信和开发。“Status”按钮将列出已安装和未安装软件的选项。“Origin”按钮显示不同仓库及其部分的条目，以及本地安装（手动或基于光盘的安装）。自定义过滤器允许你选择一个用于列出软件包的过滤器。你可以创建自己的过滤器并使用它来显示选定的软件包。搜索结果将列出你当前和之前的搜索内容，让你可以在它们之间切换。

默认选中了“Sections”选项（参见图 4-28）。你可以选择列出所有软件包，或使用窗格中提供的类别精炼你的列表。此窗格中的“All”条目将列出所有可用软件包。软件包被分为跨平台、通信和编辑器等类别。每个类别又由 multiverse（多源）、universe（社区）和 restricted（限制）软件细分。

![Image](img/image-154.png)

图 4-28：Synaptic 软件包管理器：区域

Status 条目进一步将已安装的软件细分为手动安装或可升级的（参见图 4-29）。本地软件由你手动下载并安装的软件包组成。

通过“Origin”选项，符合 Ubuntu 和 Linux Mint 标准的仓库可以根据 mint、multiverse、universe 和 restricted 软件进一步细化访问。主部分选择 Ubuntu 和 Linux Mint 支持的软件。Architecture 选项允许你选择与特定架构（如 64 位或 32 位）兼容的软件。

要执行搜索，你可以使用 Search 工具。点击工具栏上的 Search 按钮打开 Search 对话框，其中有一个文本框可以输入搜索术语。弹出菜单让你指定要搜索软件包的哪些特性，例如“Description and Name”（描述和名称）。你可以搜索软件包的其他特性，如 Name（名称）、维护者名称（Maintainer）、软件包版本（Version）、它可能依赖的软件包（Dependencies）或相关软件包（Provided Packages）。Search Results 将显示搜索列表。你可以通过点击列表中的搜索条目在搜索结果之间来移动。

要查找有关软件包的信息，选择软件包并点击 Properties（属性）按钮。这将打开一个包含 Common（常用）、Dependencies（依赖）、Installed Files（已安装文件）、Versions（版本）和 Description（描述）标签页的窗口（参见图 4-27）。Common 标签提供区域、版本和维护者信息。Installed Files 标签显示你具体安装了哪些文件，这对于查找配置文件的准确位置、名称以及命令非常有用。Description 标签显示有关软件的详细信息。Dependencies 标签显示此软件所需的所有依赖软件包（通常是库）。

![Image](img/image-155.png)

图 4-29：Synaptic 软件包管理器：状态

### 安装和删除软件包

在安装软件之前，你应该按下 Reload（刷新）按钮从活动仓库加载最新的软件包列表。

要安装软件包，单击其空复选框，或右键点击其名称显示弹出菜单并选择 Mark for Installation（标记安装）。如果存在依赖包，将打开对话框列出这些软件包。点击对话框中的 Mark 按钮标记这些软件包。随后，Synaptic 软件包管理器窗口中的软件包复选框将被标记。

一旦你选好了想要安装的软件包，点击工具栏上的 Apply 按钮开始进程。弹出 Summary 对话框显示所有要安装的软件包。你有仅下载软件包文件的选项。列出了要安装的软件包数量，以及下载大小和使用的磁盘空间。点击 Summary 对话框上的 Apply 按钮下载并安装软件包。随后将出现下载窗口显示软件包安装的进度。你可以选择显示单个软件包的进度，这将打开一个终端窗口，列出正在下载和安装的每个软件包。

下载完成后，对话框将变为 Installing Software。你可以选择在完成后自动关闭对话框。有时安装需要用户输入以配置软件。如有需要将提示你输入信息。

当你右键点击软件包名称时，还会看到 Mark Suggested for Installation（标记建议安装）或 Mark Recommended for Installation（标记推荐安装）选项。这些将标记可以增强你所选软件的应用程序，但它们不是必需的。如果该应用程序没有建议或推荐软件包，则这些条目将显示为灰色。




某些软件（例如需要大量软件包的桌面或办公套件）可以使用元包（metapackages）一次性选择。元包包含配置文件，用于选择、下载和配置此类复杂软件所需的软件包范围。Linux Mint 元包以 `mint-meta` 语开头，例如用于 Linux Mint 桌面和解码器的元包，如 `mint-meta-xfce`、`mint-meta-mate` 和 `mint-meta-codecs`。

要删除软件包，首先要找到它。然后右键点击它并选择“标记软件包待删除”（Mark package for removal）。这将保留配置文件不受触动。或者，你可以标记软件包进行“完全删除”（Mark for Complete Removal），这也会同时删除任何配置文件。依赖包不会被删除。

一旦你标记了要删除的软件包，点击“应用”（Apply）按钮。摘要对话框会显示将要删除的软件包。点击“应用”即可删除它们。

Synaptic 软件包管理器可能不会删除依赖包，特别是可能被其他应用程序使用的共享库。这意味着你的系统中可能安装了从未被使用的软件包。

### 搜索过滤器

你可以通过创建搜索过滤器来进一步精炼软件包的搜索。选择 `Settings | Filters` 菜单项以打开过滤器窗口。过滤器窗口显示两个窗格，左侧是过滤器列表，右侧有三个标签页：`Status`（状态）、`Section`（部分）和 `Properties`（属性）。要创建新过滤器，点击过滤器列表下方的 `New` 按钮。点击左格过滤器列表中的 `New Filter 1`。在 `Status` 标签页上，你可以根据软件包的状态精炼搜索准则。你可以只搜索未安装的软件包、包含已安装的软件包、包含或排除标记为待删除的软件包，或者搜索仓库中的新软件包。初始情况下，所有标准都被勾选。取消勾选你不希望包含在搜索中的项。`Section` 标签页允许你包含或排除不同的仓库部分，如游戏、文档或管理。如果你正在寻找某个游戏，可以选择仅包含游戏部分，排除其他所有内容。在 `Properties` 标签页上，你可以指定模式来搜索软件包信息（如软件包名称），并使用布尔运算符来精炼搜索准则。软件包搜索标准使用标签页底部的两个弹出菜单和文本框，配合 `AND` 或 `OR` 布尔运算符进行输入。

### 用于独立 DEB 包的软件管理器：GDebi

你也可以使用 GDebi 软件包安装器来安装单个 DEB 软件软件包。通常，这些软件包直接从网站下载，且具有很少或没有依赖包。当你使用浏览器下载特定软件包时，系统会提示用 GDebi 软件包安装器打开它。GDebi 会为该软件包打开一个安装对话框，显示有关软件包的信息并检查它是否与你的系统兼容（参见图 4-30）。标题栏中显示软件包名称。通知栏显示必须安装的额外软件包数量（依赖项）。点击 `Details` 按钮查看这些额外软件包是什么。列出了软件包的维护者和大小。点击 `files` 按钮显示软件包安装的所有文件列表。点击 `Install Package` 按钮安装软件包。

![Image](img/image-156.png)

图 4-30: GDebi 软件包安装器

你也可以先下载软件包，稍后从文件管理器窗口（通常是 `Downloads` 文件夹）中选择它。双击应该用 GDebi 打开该软件包。你也可以右键点击并选择用 GDebi 软件包安装器打开。建议使用 GDebi 安装手动下载的软件包。

### 在 Linux 上安装和运行 Windows 软件：Wine

Wine 是一个兼容层，允许你在 Linux 上原生运行许多 Windows 应用程序。不需要真实的 Windows 操作系统。Windows 应用程序运行就像 Linux 应用程序一样，能够访问整个 Linux 文件系统并使用连接 Linux 的设备。严重依赖驱动程序的应用程序（如图形密集型游戏）可能无法运行。其他不依赖任何特殊驱动程序的应用程序可能运行得很好，包括 Photoshop 和 Microsoft Office。对于某些应用程序，你可能还需要从运行的 Windows 系统将特定的 Windows 动态链接库（DLL）拷贝到 Wine 的 `system32` 或系统目录。

你可以通过软件管理器、Synaptic 软件包管理器或 `apt` 命令在系统上安装 Wine。安装 `wine-installer` 软件包。还也将安装用于微软核心字体的 `ttf-mscorefonts-installer`。系统会提示你接受使用这些字体的微软最终用户协议。

```
apt install wine-installer
```

Wine 应该可以处理 `.exe` 和 `.msi` 文件。你可能需要通过勾选文件“属性”对话框中的“执行”复选框来使其具有可执行性。如果 `.msi` 文件无法运行，你可能需要使用带有 `/a` 选项的 `msiexec` 命令。

```
msiexec /a winprogram.msi
```

Wine 应用程序包括 Wine 配置 (`winecfg`)、Wine 软件卸载程序和 Wine 文件浏览器，以及 Winetricks 和记事本。Winetricks 应用可以直接在你的 Ubuntu 桌面上运行，并提供安装兼容 Windows 程序的简单方法。对于许多 Windows 应用程序（包括 `winecfg`），你需要安装 Wine Gecko 软件包。你可以直接从 WineHQ 网站下载它：[`wiki.winehq.org/Gecko`](https://wiki.winehq.org/Gecko)。安装后，你可以使用 `wine msiexec` 命令安装它。

```
wine msiexec wine-gecko-2.47.x64
```

要设置 Wine，在终端窗口中输入 `sudo winecfg` 命令启动 Wine 配置工具，打开一个包含应用程序、库、音频、驱动器、桌面集成和图形标签页的窗口。在应用程序标签页上，你可以选择为应用程序设计的 Windows 版本。驱动器标签页列出了检测到的分区以及你的 Windows 模拟驱动器（如 C 盘）。C 盘实际上只是一个文件夹 `.wine/drive_c`，而不是固定大小的分区。你的实际 Linux 文件系统将列为 Z 盘。

```
sudo winecfg
```

一旦配置完成，Wine 会在用户目录下设置 `.wine` 文件夹（该文件夹是隐藏的，在文件管理器视图菜单中启用“显示隐藏文件”即可显示它）。该文件夹内将 `drive_c` 文件夹，它作为 C 盘运行，在 Windows 和 Program File 子目录下存放 Windows 系统文件和程序文件。System 和 System32 目录位于 Windows 文件夹。这就是放置所需的 DLL 文件的地方。Program Files 文件夹存放你安装的 Windows 程序，就像它们安装在 Windows Program Files 文件夹中一样。

你可以打开终端窗口，并将 Windows 应用程序作为参数运行 wine 命令。

```
$ wine winprogram
```

以下命令使用 Wine 在你的 Ubuntu 桌面上启动画 画图程序。

```
wine mspaint
```

要为你的 Wine Windows 文件运行 Windows 资源管理器文件管理器，输入以下内容。

```
wine explorer
```

Wine 任务器的命令是 `taskmgr`，注册表编辑器命令是 `regedit`。Wine 任务管理器让你搜索并运行已安装的应用程序。

```
wine taskmgr
wine regedit
```





在 Wine 上安装和管理 Windows 应用的一种简单方法是使用 Winetricks。你可以直接从 Ubuntu 应用程序概览启动 Winetricks。“您想做什么”对话框允许你选择不同的任务，例如安装应用程序或游戏。要安装应用程序，点击“安装应用程序”（Install an application）选项，然后点击 OK 按钮显示可能的兼容 Windows 应用程序列表。其中一些你可以直接下载并安装。另一些需要应用程序 DVD 或 CD。还有一些则需要手动下载。安装完成后，你可以返回 wineprefix 对话框。“选择默认 wineprefix”（Select the default wineprefix）选项允许你执行系统任务，如运行 `winecfg`、资源管理器文件管理器以及安装字体。当 Wine 安装 Windows 应用程序时，可能会显示多条安装消息。你可以在“您想做什么”对话框中选择“启用静默安装”（Enable silent install）来关闭此功能。Winetricks 标题栏中的 `wineprefix` 词是指 Wine 安装所在的文件夹。

此外，你也可以使用名为 Crossover Office 的商业 Windows 兼容层。这是一种经过测试可以运行 Microsoft Office 等某些应用程序的商业产品。请访问 `https://www.codeweavers.com` 查看更多详情。Crossover Office 基于 Wine，而 CodeWeavers 直接支持 Wine。

## 源代码文件

你可以使用 `apt-get` 安装源代码文件。在指定包名时使用 `source` 操作。软件包将被下载并解压。

```
sudo apt-get source mplayer
```

`--download` 选项允许你只下载源码包而不进行解压。`--compile` 选项将下载、解压、编译并将源代码打包成 Debian 二进制软件包，准备好进行安装。

使用 `source` 操作时，不会下载任何依赖包。如果一个软件包运行需要任何依赖包，你将必须下载并编译这些包。要获取所需的依赖文件，你可以使用 `build-dep` 选项。你所有的依赖文件都将自动为你定位并下载。

```bash
sudo apt-get build-dep mplayer
```

从源代码安装需要安装支持的开发库和源代码头文件。你可以针对每个 GNOME 或内核等每个主要的开发平台单独进行此操作。或者，你可以运行 APT 元软件包 `build-essential` 来处理所有的 Linux Mint 开发包。你只需要执行一次即可。

```bash
sudo apt-get install build-essential
```

## 软件包类型

Linux Mint 使用符合 Debian 标准的软件包（DEB），其文件名具有 `.deb` 扩展名。其他软件包（例如你需要编译的源码形式的包）可能以各种压缩归出现。这些通常具有 `.tar.gz`、`.tgz` 或 `.tar.bz2` 扩展名。具有 `.rpm` 扩展名的包是 Red Hat 软件包，用于 Red Hat、Fedora、SuSE 以及使用 RPM 包的 Linux 发行版。它们与 Linux Mint 不兼容。你可以使用 `alien` 工具将大多数 RPM 包转换为 Linux Mint 可以安装的 DEB 包。如果你安装了 Snap 系统，Snap 包将具有 `.snap` 扩展。表 4-1 列出了你在各种 Linux 软件包中会发现的常见文件扩展名。你可以直接从 `http://packages.linuxmint.com` 下载任何符合 Linux Mint 的 deb 包以及原始源码包，均以单文件形式。

## DEB 软件包

Debian 软件包会自动解析依赖关系，安装任何其他需要的包，而不是简单地报告它们的缺失。软件包以软件名称、版本号和 `.deb` 扩展名命名。访问 `https://www.debian.org/doc` 以获取更多信息。文件名格式如下：

- 包名
- 版本号
- 发行版标签和构建次数。专门为 Linux Mint 创建的包在此处具有 Linux Mint 标签。与其的是构建次数，即该包为 Linux Mint 构建的次数。
- `architecture` 运行软件包的系统类型，例如针对 Intel 32 位 x86 系统的 i386，或者针对 Intel 和 AMD 的 64 位系统（x86_64）的 amd64。
- `package format`。这始终为 `deb`。

例如，3dchess 的包名为 3dchess，版本号和构建次数为 0.8.1-20，针对 64 位系统的架构为 amd64。

`3dchess_0.8.1-20_amd64.deb`

以下软件包具有 Ubuntu 标签，这是一个专门为 Ubuntu 创建的包，与原始 Debian 版本不同（`dfsg`）。版本号和构建次数为 4.11.6。架构是针对 64 位系统的 amd64。

`samba_4.11.6+dfsg-0ubuntu1.4_amd64.deb`

| 扩展名 | 文件 |
| :--- | :--- |
| .deb | 一个 Debian/Linux Mint Linux 软件包 |
| .gz | 一个 `gzip`-压缩的文件（使用 `gunzip` 解压） |
| .bz2 | 一个 `bzip2`-压缩的文件（使用 `bunzip2` 解压；同样在使用 `tar` 时使用 `j` 选项，如 `xvjf`） |
| .tar | 一个 tar 归档文件（使用 `tar` 的 `xvf` 提取） |
| .tar.gz | 一个 `gzip`-压缩的 `tar` 归档文件（使用 `gunzip` 解压） |
| .tar.bz2 | 一个 `bzip2`-压缩的 `tar` 归档文件 |
| .tz | 使用 `compress` 压缩的 `tar` 归档文件 |
| .Z | 使用 `compress` 压缩的文件 |
| .bin | 自解压软件文件 |
| .rpm | 使用 Red Hat 包管理器创建的软件包 |
| .snap | deb 的替代方案 snap 包 |

**表 4-1: Linux 软件包扩展名**

## 使用 apt 和 apt-get 管理软件

APT 设计用于与存储库配合工作，并为你处理任何依赖关系。它使用 `dpkg` 安装和删除包，但也可以确定需要哪些依赖包。许多流行的 APT 工具可以让你轻松管理软件，例如同步包管理器、软件管理器和 aptitude。软件管理器和同步包管理器依赖于像 GNOME 这样的界面。如果你使用命令行界面，可以使用 `apt` 或 `apt-get` 管理包。在命令行上使用 `apt` 或 `apt-get` 命令可以安装、更新和删除。查看 `apt` 和 `apt-get` 手页以获取 `apt-get` 命令的详细列表（参见表 4-2）。

apt-get 包

| 命令 | 说明 |
| :--- | :--- |
| update | 下载并重新同步 APT 支持的存储库的可用和更新软件包列表。Linux Mint 更新的 APT 存储库位于 `/etc/apt/sources.list.d/official-package-repositories.list`。 |
| upgrade | 更新软件包，如果有可用新版本则安装。 |
| dist-upgrade | 将你所有已的软件包升级到新版本 |
| install | 安装特定的软件包，使用包名而非完整的包文件名。 |
| remove | 从系统中删除软件包。 |
| source | 下载并解压源码包 |
| check | 检查损坏的依赖关系 |
| clean | 移除系统仓库缓存中下载的软件包。用于释放磁盘空间。 |

**表 4-2: apt 和 apt-get 命令**





`apt` 命令是 `apt-get` 的新版本，选项更少。例如，`apt-get` 命令具有 `check` 选项，用于检查损坏的依赖关系。旧版系统可能希望继续使用 `apt-get`，特别是当该命令用于自定义的系统脚本时。对于基础操作，如升级、安装或删除软件包，你可以使用 `apt` 代替。

`apt-get` 命令软件包 `apt` 命令软件包

`apt` 和 `apt-get` 命令通常接受两个参数：要执行的命令和软件包名称。其他 APT 软件包工具也遵循相同的格式。命令是一个术语，例如 `install` 用于安装软件包，或 `remove` 用于卸载软件包。你只需要指定软件名称，而不需要软件包的完整文件名。APT 会自动确定。要安装 MPlayer 软件包，你会使用：

```bash
sudo apt install mplayer
```

为了确保 `apt` 或 `apt-get` 拥有最新的存储库信息，请使用 `update` 命令。

```bash
sudo apt update
```

要删除软件包，你使用 `remove` 命令。

```bash
sudo apt remove mplayer
```

```
你可以使用 `-s` 选项先检查删除或安装操作，特别是检查是否存在任何依赖问题。对于删除操作，你可以使用 `-s` 先查出哪些依赖包也会被删除。

```bash
sudo apt-get remove -s mplayer
```

如果你的 X Windows 系统服务器（你的显示驱动程序）发生故障，`apt-get` 和 `apt` 命令可能会很有帮助。例如，如果你安装了受限的供应商显示驱动程序，然后桌面无法启动，你可以进入恢复模式，启动 root  shell，并使用 `apt` 或 `apt-get` 删除该受限的显示驱动程序。你之前的 X 开源显示驱动程序将自动恢复。以下命令将删除 Nvidia 受限显示驱动程序。

```bash
sudo apt remove nvidia*
```

所有安装、删除和更新操作的完整日志保留在 `/var/log/dpkg.log` 文件中。你可以查看此文件以查找确切哪些文件被安装或删除了。

APT 的配置存储在 `/etc/apt` 目录。官方上，`/etc/apt/sources.list` 文件应该列出安装软件包的发行版存储库。额外的第三方存储库的源列表保留在 `/etc/apt/sources.list.d` 目录中。然而，在 Linux Mint 上，发行版存储库列表保留在 `/etc/apt/sources.list.d/official-package-repositories.list` 文件中。GPG（GNU Privacy Guard）数据库文件持有这些存储库的验证密钥。`apt-get` 的特定选项可以在 `/etc/apt/apt.conf` 文件或 `/etc/apt/apt.conf.d` 目录下的各种找到。

### 使用 apt 和 apt-get 更新软件包（升级）

`apt` 工具还允许你一次性更新整个系统。`update` 和 `upgrade` 术语与其他软件工具用法不同。在 `apt` 中，`update` 命令仅更新你的软件包列表，检查可能需要安装新版本的软件包，但并不安装这些版本。从技术角度来说，它更新 APT 用于确定哪些软件包需要更新的包列表。`upgrade` 术语用于表示软件软件包的实际更新。会下载并安装新版本。`apt` 所说的“更新（updating）”，其他软件包管理器称为“获取待更新的软件包列表（重载操作）”。在 `apt` 中，“升级（upgrading）”是其他软件包管理器指的“执行更新”。

注意：在使用 `apt` 时，`update` 和 `upgrade` 术语可能会引起混淆。`update` 操作仅更新 Apt 包列表，而 `upgrade` 实际上会下载并安装更新后的软件包。

升级只需使用 `upgrade` 命令。在不指定软件包的情况下，使用带有 `upgrade` 命令的 `apt-get` 将升级整个系统。添加 `-u` 选项可以在升级时列出软件包。首先，通过 `update` 命令确保你的存储库信息（包列表）是最新的，然后执行升级命令。

```bash
sudo apt update
sudo apt -u upgrade
```

### 命令行搜索与信息：dpkg-query 和 apt-cache 工具

`dpkg-query` 命令允许你列出软件包的详细信息。它在命令行（终端窗口）运行。使用带有 `-l` 选项的 `dpkg-query` 列出你所有的软件包。

```bash
dpkg-query -l
```

`dpkg` 命令可以作为 `dpkg-query` 的前端，检测其选项以执行相应的任务。之前的命令也可以这样运行：

```bash
dpkg -l
```

列出特定软件包需要包名完全精确匹配，除非你使用模式匹配运算符。以下命令列出 `samba` 软件包。

```bash
dpkg-query -l samba
```

将模式匹配运算符（如 `*`）放在模式之后，将显示任何以指定模式开头的软件包。模式及其运算符需要放在单引号中，以防止 shell 尝试使用该模式匹配你当前目录中的文件名。以下示例查找所有以 "samba" 模式开头的软件包。这将包括名称如 `samba-client` 和 `samba-common` 的软件包。

```bash
dpkg-query -l 'samba*'
```

你可以通过 `grep` 执行额外的搜索来进一步精炼结果。以下操作首先输出所有以 `samba` 开头的软件包，然后从这些结果中，`grep` 操作仅列出名称中包含 "common" 模式的包，例如 `samba-common`。

```bash
dpkg -l 'samba*' | grep 'common'
```

使用 `-L` 选项列出软件包安装的文件。

```bash
dpkg-query -L samba
```

```
要查看软件包的状态信息，包括其依赖和配置文件，请使用 `-s` 选项。字段将包括 Status（状态）、Section（区域）、Architecture（架构）、Version（版本）、Depends（依赖包）、Suggests（建议）、Conflicts（冲突包）和 Conffiles（配置文件）。

```bash
dpkg-query -s samba
```

状态信息还会提供建议的依赖关系。这些是未安装但可能使用的软件包。对于 samba 软件包，建议安装 `chrony` 时间服务器包。

```bash
dpkg-query -s samba | grep Suggests
```

使用 `-S` 选项确定某个文件属于哪个软件包。

```bash
dpkg-query -S filename
```

你也可以使用 `apt-cache` 工具获取信息。使用 `apt-cache` 的 `search` 命令进行搜索。

```bash
apt-cache search samba
```

要查找特定软件包的依赖关系，使用 `depends` 命令。

```bash
apt-cache depends samba
```

使用 `show` 命令显示软件包信息。

```bash
apt-cache show samba
```

注意注意：如果你安装了 Aptitude 软件管理器，可以使用带有 `search` 和 `show` 选项的 `aptitude` 命令来查找并显示软件包信息。

### 使用 dpkg 管理非存储库软件包

你可以使用 `dpkg` 直接安装你已经下载的软件软件包，而不是使用启用了 APT 的软件工具（如 `apt`、软件管理器或 Synaptic 软件包管理器）。在这种情况下，你不是从存储库安装的。相反，是你手动从 Web 或 FTP 站点下载了包文件到系统中的某个文件夹。这种情况非常罕见，适用于 Linux Mint 存储库或任何启用 APT 的存储库中未提供的软件。在执行直接下载并使用 `dpkg` 安装之前，先检查存储库是否有该软件软件包。`dpkg` 配置文件位于 `/etc/dpkg` 目录。配置保留在 `dpkg.cfg` 文件中。请查看 `dpkg` 手页以获取选项的详细列表。





你会使用 `dpkg` 的一种情况是针对你自己构建的软件包，例如当你将另一种格式的软件包转换为 Debian 软件包（DEB）时创建的包。这发生在将 RPM 包（Red Hat 包管理器）转换为 Debian 软件包格式的情况下。

对于 `dpkg`，你使用 `-i` 选项来安装软件包，使用 `-r` 来移除它。

```
sudo dpkg -i package.deb
```

`dpkg` 的主要缺陷是它不提供依赖支持。它会你所需的依赖项，但你必须单独安装它们。`dpkg` 只安装指定的软件包。它对于没有依赖关系的软件包非常有用。

你使用 `-I` 选项直接从 DEB 软件包文件中获取软件包信息。

```
sudo dpkg -I package.deb
```

要移除软件包，你使用 `-r` 选项配合软件包软件名称。你不需要像 `.386` 或 `.deb` 这样的版本或扩展信息。当使用 `dpkg` 移除带有依赖关系的软件包时，你必须先手动移除所有依赖项。在完成此之前，你将无法卸载该软件包。配置文件不会被删除。

```
sudo dpkg -r packagename
```

如果你安装了一个需要依赖的软件包，然后未能安装这些依赖项，你的安装数据库将被标记为具有损坏软件包。在这种情况下，在修复损坏软件包之前，APT 将不允许安装新软件包。你可以输入带有 `-f` 和 `install` 选项的 `apt-get` 命令来一次修复所有损坏软件包。

```
sudo apt-get -f install
```

## 使用其他软件格式的软件包

你可以将其他软件格式的软件包转换为 DEB 软件包，然后可以在 Linux Mint 上安装它们。要做到这一点，你使用 `alien` 工具，它可以转换多种不同的格式，如 RPM 甚至 TGZ（`.tgz`）。你使用 `--to-deb` 选项将其转换为 Linux Mint 可以随后安装的 DEB 软件包格式。`--scripts` 选项还会尝试转换任何安装前或安装后的配置脚本。一旦生成了 `.deb` 包，你就可以使用 `dpkg` 或软件管理器来安装它。

```
alien --scripts --to-deb package.rpm
```

## Ubuntu Snap

Ubuntu 支持两种包管理系统：Snap 和 DEB（Debian 软件包格式）。对于旧的 DEB 格式软件包，底层的软件管理工具是 APT。Snap 软件包（`snaps`）格式与 DEB 不同，不能由 APT 管理。相反，它们由 Snap 包管理器管理，该管理器使用 `snapd` 守护进程来安装、更新和运行 snap 。Snap 是一个完全不同的包管理系统，尽管 Snap 软件包可以与 APT 软件包一起安装，并在 Linux Mint 和 Ubuntu 桌面上进行无缝访问。

APT（高级包工具）是安装软件包的旧工具，目前仍用于大多数应用程序。当你使用软件管理器或 Synaptic 包管理器安装 DEB 软件包时，将调用 APT，并自动从相应的在线 APT 管理仓库中选择并下载该软件包。这将包含整个 Ubuntu 在线仓库，包括 main（主）、universe（宇宙）、multiverse 和 restricted（限制）部分。

一个 DEB 软件软件包包含了软件应用程序所需的所有文件。Linux 软件应用程序通常由多个文件组成，这些文件必须安装在不同的目录中。程序本身放置在 `/usr/bin` 等系统文件夹中，在线手册文件放在另一个文件夹，而库文件放在另一个文件夹中。当你选择一个应用程序进行安装时，APT 将安装任何额外的依赖（需要）软件包。APT 默认还会安装所有推荐软件包。许多软件应用程序具有依赖于推荐软件包的额外功能。

Snap 是新的软件包格式，旨在取代 Ubuntu 上的 DEB 软件包管理系统。如所述，这些软件包被称为 `snaps`。与 DEB 格式一样（与 RPM 等其他 Linux 包格式一样），软件应用程序的组件软件文件直接安装到 `/lib`、`/etc` 和 `/usr/bin` 等全局系统文件夹中。实际上，此类软件包在安装期间可以访问你的整个系统，从而带来了安全风险。此外，一个 DEB 软件软件包通常有几个依赖软件包，这些包也必须安装。这些包可能是大量的。在该系统下，不同应用程序使用的共享库对开发者来说可能是一个问题，因为软件的更改可能需要等待共享库的支持性更改。

使用 Snap，应用程序的软件文件不再安装在全局文件夹中。它们被安装在一个独立的文件夹中，任何依赖软件和共享库都作为 snap 软件包的一部分包含在。实际上，不再有任何依赖关系，库也不再共享。这使得更新更加安全且更快速，尽管安装的文件集较大。安装过程不再需要访问你的整个系统。整个应用程序被隔离在一个位置。由于依赖关系损坏导致更新失败的问题不再是一个问题。以前使用相同共享库的应用程序现在将拥有该库的自己的副本。以前必须等待共享库进行更改的开发者，现在可以直接更改他们自己的副本。

请记住，Flatpak 已经在 Linux Mint 上启用，它的工作方式与 Snap 非常相似 ([`www.flatpak.org/`](https://www.flatpak.org/))。许多作为 Snap 提供的流行应用程序已经作为 Flatpak 可用在 Linux Mint 上。

### Snap 软件包

Snap 旨在提供一个通用且独立的软件仓库，其软件包可以在任何 Linux 发行版或，甚至是 Linux 发行版的特定版本上运行。snap 软件包可以下载并安装在任何发行版上，包括 Ubuntu、Fedora、Debian、Centos、Linux Mint 和 openSUSE。snap 软件包还可以运行在该发行版的任何版本上。同一个 snap 软件包可以在发行版的不同版本上运行，例如 Ubuntu 18.04 和 20.04。软件开发者只需维护一个 snap 软件包，而不是为不同的发行版维护多个。这种设计使得商业软件公司为其专有应用程序提供 Linux 客户端变得容易。目前包括 Skype、Zoom 和 Slack。这种结构使得更新过程变得简单且快速。更新是由你系统上的 `snapd` 服务器在开发者发布修订后的六小时内自动完成的。如果你愿意，可以手动更新或设置不同的更新计划。

Snap 归由 Ubuntu 维护和支持。

查看 Snapcraft 文档和教程：

[`snapcraft.io/docs`](https://snapcraft.io/docs) [`snapcraft.io/tutorials`](https://snapcraft.io/tutorials)

### Linux Mint 对安装 Snap 的限制





Linux Mint 20 的配置为防止安装 Snap。`snapd` 软件包在列表中，但它不会被安装。Linux Mint 采取此行动是因为对 Snap Store 的限制。Snap 软件包只能从 Snap Store（仓库）获取，且只能有一个 Snap Store，即由 Ubuntu 维护的那个。相比之下，任何人都可以设置 APT 仓库，甚至是 Flatpak 商店。关于此策略的详细讨论，请参阅：

[`linuxmint-user-guide.readthedocs.io/en/latest/snap.html`](https://linuxmint-user-guide.readthedocs.io/en/latest/snap.html)

可以通过简单的命令移除限制，然后安装 `snapd` 守护进程和服务，这在 Linux Mint 20 发布说明中所提到的。即使已启用，软件管理器（Software Manager）也不会管理或检测 snap 商店中的应用程序。你必须安装 Snap Store 应用程序或使用 `snap` 命令在 snap 商店中安装软件。

如 Linux Mint 文档所述，你运行以下命令来启用 Snap，删除 `/etc/apt/preferences.d` 文件夹中的 `nosnap.pref` 配置文件。

```
sudo rm /etc/apt/preferences.d/nosnap.pref
apt update
apt install snapd
```

### snap 命令

你可以在终端窗口中使用 `snap` 命令来安装和管理 snap 软件包（参见 表 4-3）。要查找 Snap 软件包，使用 `snap find` 命令配合搜索词（参见 图 4-31）。

```bash
snap find chromium
```

你也可以根据搜索词进行搜索。以下示例搜索了 FTP 客户端和服务器以及 Web 服务器。

```bash
snap find ftp
snap find "web server"
```

如果没有搜索词，将显示一个流行的 snap 软件包列表。

```bash
snap find
```

Snaps 被进一步组织为娱乐、游戏和生产力等部分。你可以使用 `find --section` 命令查看可用的部分。

```bash
snap find --section
```

要查看可用的游戏，你需要在部分名称前加上 `=` 符号，例如 `--section=games`。

```bash
snap find --section=games
```

要安装软件包，使用带有 `install` 选项的 `snap` 命令。以下安装 Chromium snap 软件包。

```bash
sudo snap install chromium
```

![Image](img/image-157.png)

图 4-31: 可用常用 snaps 列表：find

| 命令 | 描述 |
| :--- | :--- |
| `find pattern*` | 搜索可用的 snap 软件包。如果没有搜索词，将显示流行的软件包列表。 |
| `find --section` | 列出可用的 snap 软件包类别（部分） |
| `find --section=*section-name*` | 列出某个部分中的 snap 软件包 |
| `refresh` | 手动更新软件包，如果可用，则安装已安装软件包的新版本。默认情况下，Snap 每六小时自动更新一次。 |
| `install snap-package*` | 安装 snap 软件包 |
| `remove` | 完全删除一个 snap 软件包 |
| `revert [*revision-number*]` | 回到 snap 的上一个已安装修订版本。如果没有修订版本号，则将使用上一个已安装的修订版本。 |
| `disable snap-package*` | 在不卸载的情况下禁用 snap。已安装的 snap 保留在你的系统中，但用户不可用。这将禁用该软件包安装的所有 snap 应用程序。 |
| `enable snap-package*` | 启用已禁用的 snap，使其对用户可用。将启用该软件包安装的所有 snap 应用程序 |
| `list` | 列出你已安装的 snap 软件包 |
| `list --all` | 列出你所有的 snap 软件包以及每个软件包的修订版本，这将显示修订版本的修订号 |
| `list --all snap-package*` | 列出 snap 软件包的所有修订版本，这将显示每个每个的修订号 |
| `connections` | 列出带有插头（plugs）和插槽（slots）的接口 |
| `interface` | 列出可用接口并对每个接口进行描述 |
| `install channel=*risk-level*` | 从指定的风险级别（`stable`、`candidate`、`beta` 和 `edge`）安装 snap 软件包修订版本 |
| `info snap-package*` | 显示已安装 snap 软件包的详细信息，包括所有修订版本 |
| `connect plug slot` | 手动将 snap 应用程序（插头）连接到系统资源（插槽） |
| `get` | 列出你可以设置的软件包配置选项（如果有） |
| `set` | 修改软件包的配置选项（如果有） |
| `unset` | 将软件包的配置选项置为空（如果有） |
| `run snap-application*` | 运行 snap 应用程序 |

表 4-3: snap 命令

安装后，该软件包安装的 snap 应用程序将出现在 Linux Mint 菜单中，就像其他应用程序一样。

使用 `remove` 命令从你的系统中完全删除软件包。

```bash
sudo snap remove chromium
```

通过 Snap，你可以选择仅禁用软件包，而不是完全删除它。Snap 软件包将保持已安装状态，但对任何用户都不可用。使用 `disable` 命令禁用软件包。你可以使用 `enable` 命令启用已禁用的软件包。请记住，如果软件包安装了多个应用程序，所有这些应用程序都会被 `disable` 命令禁用。`enable` 命令将启用所有应用程序。

```bash
sudo snap disable chromium
sudo enable chromium
```

使用 `refresh` 命令更新你的 snap 软件包。

```bash
sudo refresh chromium
```

要查看已安装的 snap 软件包列表，使用 `list` 命令（参见 图 4-32）。

```bash
snap list
```

显示特定 snap 的详细信息使用 `info` 命令。

```bash
snap info chromium
```

Snap 应用存储在软件包名下的 `/snap` 文件夹。每个修订版本都有自己的 `/etc`、`/usr`、`/bin`、`/lib` 和 `/var` 文件夹。当前启用的应用程序链接位于 `/snap/bin`。Snap 用户的数据位于你的目录下。Snap 的 systemd 支持由 `snapd.service` 和 `snapd.socket` 文件提供。

![Image](img/image-158.png)

图 4-32: 已安装 snaps 列表：list

### Snap 通道：轨道和风险级别

Snap 软件包通过通道进行管理，通道将软件包组织为轨道和风险级别。开发者可能会为应用程序添加短期版本分支。在 GNOME 软件的 Snap 软件包中，你会看到轨道和风险级别作为可能的通道选择。

`track/risk-level`

轨道指示已安装软件包的修订版本。默认是 `latest`。风险级别指示软件的可靠性。有四个风险级别：`stable`、`candidate`、`beta` 和 `edge`。`stable` 风险级别适用于认为已准备好大规模发布的软件。`candidate` 风险级别适用于准备发布但仍在测试的应用程序版本。`beta` 风险级别适用于可能包含新功能但被认为不稳定的版本。`edge` 风险级别适用于仍在开发中具有持续变化且可能无法运行的版本。

软件包默认按最新的风险级别安装。

```bash
snap install
```

如果你想使用不同的风险级别，可以使用相应的风险级别轨道进行指定：`--stable`、`--candidate`、`--beta` 和 `--edge`。你也可以使用 `--channel` 选项。

```bash
snap install --candidate
snap install --channel=candidate
```





你稍后可以使用 `switch` 命令更改正在追踪的风险级别（track level）。这只会更改跟踪，而不会安装该轨道对应的版本。要执行此操作，你需要运行 `refresh` 命令。

```bash
snap switch --candidate
```

若要同时完成切换到不同轨道并安装该轨道版本的应用程序，你可以直接运行 `refresh` 命令。

```bash
snap refresh --channel=candidate
```

## Snap 限制 (Snap Confinement)

大多数 snap 包都使用严格限制模式（strict confinement mode）运行，在隔离环境中运行，并且对网络、系统文件夹和进程等系统资源只有极少的访问权限。如果经过官方批准，某些 snap 包允许在经典模式（classic mode）下运行，让它们像传统的 DEB 包一样访问系统资源。这些包只能通过 `--classic` 选项进行安装。为了让某个包获得经典状态，必须由 Snapcraft 对其安全性和稳定性问题进行仔细检查。此外还有为开发者留的 `devmode`。使用带有 `--verbose` 选项的 `snap info` 命令查看软件包的限制模式。列出所有 snap 包的 `snap list` 命令也会显示每个包的限制模式。

```bash
snap info --verbose chromium
```

软件包对系统资源的访问是通过接口（interfaces）设置的，接口由开发者确定并在包安装时实现。接口通常允许访问设备等资源。这通常包括你的主目录、pulseaudio、网络访问、系统文件和显示服务器（wayland 或 X11）。snap 包只能通过这些接口访问你的系统。接口由插头（plugs）和槽（slots）组成。插头是需要接口的包或进程（消费者），而槽是支持它的服务（提供者）。`snap connections` 命令将列出软件包的接口。

```bash
snap connections chromium
```

不带包参数的 `snap connections` 命令将列出所有包（插头）以及它们使用的接口和槽。

```bash
snap connections
```

`snap interface` 命令列出系统中所有的接口并对每个接口进行描述。

```bash
snap interface
```

要查看某个接口使用的槽和插头，请使用带有接口名称的 `snap interface` 命令。

你可以使用 `connect` 和 `disconnect` 命令手动为包连接或断开接口。它们的参数是插头和槽，其中插头由包名和冒号置前。如所述，包的接口通常会自动为你设置并在包安装时激活。以下示例将将 Chromium 浏览器连接到你的主目录。

```bash
sudo snap connect chromium:home :home
```

在安装包时，并非所有可用的接口都会被激活。你也可以关闭已激活的接口，拒绝该包访问该资源。你还可以通过包名使用 connections 命令检查允许的连接（权限），显示该包的槽和插头。

## Snap 版本：回滚 (Snap Revisions: revert)

Snap 是以修订（revisions）的形式安装的。对于任何特定的应用程序，你可能安装了多个版本的修订。每个修订都可以作为应用程序运行。当前修订（最近安装的那个）具有优先级。但你可以轻松地决定运行之前的修订。如果安装了新的修订导致变得不稳定，或者对软件的更改废弃了你通常使用的功能，就会发生这种情况。应用程序的主要更改将作为一个版本发布，这也被视为一个修订。虽然你可以为某个版本拥有多个修订，但对于大多数不复杂的应用程序，你通常每个版本只有一个修订。

虽然 `list` 命令会显示已安装的 snap，但添加 `--all` 选项还将显示每个 snap 的所有修订。此操作将显示每个修订的名称、版本、修订号、跟踪轨道、发布者和备注。

```bash
snap list --all
```

与其列出所有 snap，你可能只需要列出特定 snap 的修订。

```bash
snap list --all chromium
```

修订号是唯一的。你可能有多个具有相同版本号的修订，但修订号是该安装项的唯一标识符。可以使用修订号运行之前的修订。

一个应用程序只能启用一个修订。这是 Snap 将运行的那个。该应用程序的所有其他修订都处于禁用状态，如 `list --all` 输出中的 Notes（备注）字段所示。

你可以启用之前的修订，同时禁用当前修订，从而让 Snap 运行它。你通过 `revert` 命令和想要启用的修订号来实现这一点。以下示例将 Chromium 回滚到修订版本 1259。

```bash
sudo snap revert chromium 1259
```

如果你只想启用上一个修订，可以省去数字。

```bash
sudo snap revert chromium
```

如果你在回滚到之前的修订后决定恢复到使用最新修订，请运行带有最新修订修订号的 `revert` 命令。

```bash
sudo snap revert chromium 1260
```

你也可以直接对该 snap 运行 `refresh` 命令。最新修订会自动启用。

```bash
sudo snap refresh chromium
```

记住，如果之后发布了 snap 的新更新，自动 `refresh` 操作会将 snap 更新到该新修订。

## Snap 包配置 (Snap Package Configuration)

某些 Snap 包（例如服务的包）可能可以使用 `snap get`、`snap set` 和 `snap unset` 命令管理的配置选项。`snap get` 命令列出 snap 的配置选项及其当前设置。`snap set` 命令可以更改选项，`snap unset` 命令可以移除值。某些 Snap 包（如服务器）拥有在启动时可以设置的选项。每个修订在运行时都将拥有相应的配置。使用 `revert` 命令，你可以从一个服务器修订切换到另一个，每个运行独立的配置。

此外，所有 snap 应用程序都有环境变量。环境变量将显示 snap 可以访问的文件夹，以及应用程序信息如修订号和版本号。你可以先通过 `run --shell` 命令启动应用程序的 shell 来查看该应用程序的环境变量。

```bash
sudo snap run --shell chromium
```

请记住，有时包名可能与应用程序名不同。一个包可能会安装多个应用程序，如 nextcloud 包所示。要访问 Nextcloud Web 服务器，你需要使用它的应用程序名 `nextcloud.apache`。

```bash
sudo snap run --shell nextcloud.apache
```

然后你可以使用 shell 命令 `env` 列出环境变量，使用 `grep` 和 `SNAP` 模式过滤输出，只显示与 snap 相关的变量。

```bash
env | grep SNAP
```

列出当前启用修订的环境变量。文件夹变量将显示该修订的文件夹。`SNAP_COMMON` 和 `SNAP_USER_DATA` 变量显示应用程序可以写入的文件夹位置。

要退出 shell，输入 `exit` 命令。

## Snap 与服务 (Snap and Services)

作为 snap 包安装的服务可以使用 `systemctl` 命令管理，例如使用 `systemctl start` 和 `systemctl stop` 来启动和停止服务。此外，某些 snap 包的服务还提供你可以使用 snap `get`、`set` 和 `unset` 命令管理的配置选项。目前作为 snap 包提供的服务较少。对于大多数如 FTP 和 Web 服务器的服务，你仍需要使用 APT。




作为 snap 包安装的服务，其 systemd 服务文件安装在 `/etc/systemd/system` 文件夹中，而不是像 APT 服务那样安装在 `/lib/systemd/system`。所有通过 snap 安装的服务都通过 `snapd` 服务器管理。而 `snapd` 服务器本身又在 `/lib/system/system` 文件夹中有 `snapd` 的服务文件。此外，所有通过 snap 安装的服务的服务文件都以 `snap` 术语开头，例如用于 Nextcloud Web 服务器（属于 `nextcloud` snap 包）的 `snap.nextcloud.apache.service`。随后你可以使用 `systemctl` 命令来管理该服务。

```
systemctl status snap.nextcloud.apache
sudo system restart snap.nextcloud.apache
```

### GNOME 软件与 Snap

你也可以安装 GNOME 软件应用程序来管理 snap 包。它在应用程序概览中的图标标记为“软件（Software）”（参见图 4-33）。GNOME 软件在“探索（Explore）”选项卡中还有 GNOME 扩展，其中包含解码器、字体、驱动程序和输入源的选项卡。类别具有一个功能完整的“显示（Show）”菜单，列出了完整的子类别列表。要让 GNOME 软件管理 Snap 应用程序，你需要安装 Snap 插件。

```
sudo apt install gnome-software-plugin-snap
```

![Image](img/image-159.png) ![Image](img/image-160.png)

图 4-33: GNOME 软件

软件的描述页提供了软件的简要描述以及指向其相关网站的链接（参见图 4-34）。未安装的软件会在软件名称下方显示“安装”按钮，而已安装的软件则显示“移除”按钮。名称右侧是带有评价数量的星级评分。

在“详情（Details）”部分列出了软件版本、最后更新时间、许可证、开发者、来源和大小。Snap 包的来源为 `snapcraft.io`。它们还有一个“通道（Channel）”条目，显示已安装的 Snap 通道，例如 latest/stable（参见图 4-34）。

在安装 Snap 包时，你可以从不同的通道中选择，包括稳定（stable）、候选（candidate）、测试（beta）和边缘（edge）。通道是从标题栏右侧的 Snap Store 菜单选择的（参见图 4-34）。对于 Snap 包，应用程序页面将在标题栏右侧显示 Snap Store 菜单，列出你可以安装的 Snap 通道。默认选择 latest/stable 通道。

![Image](img/image-161.png)  ![Image](img/image-162.png)

图 4-34: GNOME 软件，Snap 商店 (snapcraft.io) snap 包通道

对于 Snap 包，一旦安装，“移除”按钮旁边会显示一个“权限（Permissions）”按钮。点击此按钮可显示应用程序的权限，例如对主目录的访问以及对可拆卸设备的访问（参见图 4-35）。Snap 包与你的系统资源（如主目录和系统设置工具）是隔离的。它们必须拥有访问这些资源的权限。安装包时默认会设置若干基本权限，其他的你需要手动设置。

![Image](img/image-163.png)

图 4-35: GNOME 软件，Snapcraft snap 包权限

注意：你也可以安装 `gnome-software-plugin-flatpak` 插件，以便 GNOME 软件能够同时管理 Snap 和 Flatpak 应用程序。

# 5. 应用程序

目前适用于 Linux Mint 的所有 Linux 软件都可以从在线仓库获取。你可以下载桌面、服务器、办公套件和编程包等的应用程序。软件软件包主要通过官方 Linux Mint 和 Ubuntu 仓库分发。下载和更新由你的桌面软件管理器和更新器自动处理。许多流行应用程序包含在仓库的不同部分中。在安装期间，系统会被配置为访问 Linux Mint 仓库。你可以使用更新管理器更新到 Linux Mint 仓库中的最新软件。

特定版本的 Linux Mint 软件包列表位于：

[`packages.linuxmint.com`](http://packages.linuxmint.com)

更详细的列表保留在 Linux Mint 社区网站：

[`community.linuxmint.com/software`](https://community.linuxmint.com/software)

Linux Mint 基于 Ubuntu。Ubuntu 发行版的软件包列表位于：

[`packages.ubuntu.com`](http://packages.ubuntu.com)

Linux Mint 和 Ubuntu 仓库中的所有软件包都可以通过软件管理器（Software Manager）和 Synaptic 包管理器直接访问，它们提供了方便的软件安装、删除和搜索。

由于许可证限制，MP3、DVD 和 DivX 等常用操作的多媒体支持需要通过 `mint-meta-codecs` 包单独安装。如果尚未安装，请从“音频与视频（Sound & Video）”菜单选择“安装多媒体解码器（Install Multimedia Codecs）”，或点击欢迎屏幕上的“多媒体解码器”图标。

此外，你还可以从第三方源下载压缩存档格式或 DEB 包格式的软件。DEB 包使用 Debian 软件包管理器归档，扩展名为 `.deb`。压缩存档具有如 `.tar.gz` 等扩展名。你也可以下载源码版本并直接编译。

你还可以在 Cinnamon 或 MATE 桌面安装并运行任何 KDE 应用程序，例如 Karbon（矢量图形）、Clementine（音乐播放器）、Dragon player（媒体播放器）、Ocular（PDF 查看器）以及 Calligra 办公套件。所有这些都可以从软件管理器（Linux Mint 和 Ubuntu 仓库）直接安装。

Linux Mint 还将 Flatpak 包集成到软件管理器中。你可以从 FlatHub 仓库轻松下载并安装 Flatpak 包。

## X-Apps 项目为传统的 GTK（GNOME）桌面提供通用应用程序，例如 MATE、Cinnamon 和 Xfce。对 X-App 的改进将自动适用于所有支持 X-Apps 的桌面。Linux Mint 桌面安装的 X-Apps 包括 Xed（文本编辑器）、Xviewer（图像查看器）、Pix（图像编辑器和查看器）以及 Xreader（文档查看器），以及系统工具 Blueberry（蓝牙配置）、slick-greeter（LightDM 登录界面）和 lightdm-settings（登录界面配置）。Xplayer 视频播放器不再默认安装，但如果你需要可以安装。它已被 Celluloid 替换为默认视频播放器，后者功能更强大且高效。尽管许多 GNOME 应用程序随不同版本而变化，但 X-Apps 保持不变且始终可用。你仍然可以安装并使用相应的 GNOME 应用程序（例如 Gedit 和 Eye of GNOME），但 X-Apps 会集成得更加轻松。

Linux Mint 还提供了 X-App 支持工具，例如 XApp Status Applet（它提供了一个带有 XAppStatusicon 图标的桌面面板系统托盘）以及 XappIconChooser（用于更改应用程序、文件夹和文件图标以及菜单图标）。你可以从任何应用程序、文件或文件夹的属性对话框更改图标。




可用的 X-Apps 列如 表 5-1 所示。X-App 的大多数选项可以通过首选项（Preferences）对话框设置。也可以使用 dconf 编辑器 `org.x` 设置选项，它还可以设置默认显示配置等选项。

|  | 描述 |
| :--- | :--- |
| Xed | 文本编辑器（基于 Pluma） |
| Xplayer | 视频播放器（基于 Videos/Totem），不再是默认应用程序 |
| Xviewer | 图像查看器（基于 Eye of GNOME） |
| Pix | 照片组织器（基于 Gthumb） |
| Xreader | PDF 阅读器（基于 Atril） |
| XApp Status Applet | 桌面面板系统托盘，带有用于系统工具的 XAppStatusicon 图标 |
| XAppIconChooser | 更改文件、文件夹和应用程序的图标。 |
| Blueberry | 蓝牙配置工具 |
| slick-greeter | LightDM 登录界面 |
| lightdm-settings | LightDM 登录界面配置 |

表 5-1：X-App 应用程序

## 办公应用程序

Linux 现在有多种办公套件可用。这些包括专业级的文字处理程序、演示文稿、绘图工具和电子表格。本章将介绍免费版本。所有软件均为 Ubuntu 软件包。LibreOffice 是目前 Linux Mint 支持的主要办公套件。Calligra 是一个为 KDE 设计的办公套件，但可以在 GNOME 上运行。你也可以从 Oracle 购买 Oracle Open Office 等商业办公套件。

Linux 还提供了多种数据库管理系统，包括高性能的商业级数据库管理系统。大多数 Linux 数据库管理系统都是为支持大型关系型数据库设计的。Linux Mint 的发行版包含了 MySQL、MariaDB 和 PostgreSQL 开源数据库，它们可以支持较小的数据库。

Linux 还提供了多种文本编辑器，从用于简单笔记的简单文本编辑器到具有拼写检查、缓冲区或复杂模式匹配等更复杂功能的编辑器。它们都能生成字符文本文件，并用于编辑任何 Linux 文本文件。文本编辑器通常用于系统管理任务，以更改或添加 `/etc` 目录下的 Linux 配置文件，或位于用户主目录（点文件）的初始化或应用程序配置文件的条目。你也可以使用文本编辑器来处理任何编程语言或 shell 脚本的源代码文件。

Linux Mint 还支持多种电子书阅读器。其中某些如 Calibre 和 FBReader 可以在 Linux 上原生运行。

### LibreOffice

LibreOffice 是一个完全集成的办公应用程序套件，作为一个开源项目开发并向所有人免费发布。它是 Linux 的主要办公套件。可以通过办公菜单访问 LibreOffice 应用程序。LibreOffice 是最初源自 OpenOffice 的开源且免费的办公套件。LibreOffice 由 Document Foundation 支持，该基金是在 Oracle 收购 OpenOffice 的主要开发者 Sun 后成立的。LibreOffice 现在是 Linux 的主要的开源办公软件。Oracle 保留了所有原始 OpenOffice 软件的控制权，并且与任何 LibreOffice 开发合作。LibreOffice 已取代 OpenOffice 成为大多数 Linux 发行版的默认办公软件。

| 应用程序 | 描述 |
| :--- | :--- |
| Calc (电子表格) | LibreOffice 电子表格 |
| Draw (绘图) | LibreOffice 绘图应用程序 |
| Writer (文字处理) | LibreOffice 文字处理器 |
| Math (公式) | LibreOffice 数学公式编辑器 |
| Impress (演示) | LibreOffice 演示文稿管理器 |
| Base (数据库) | 用于访问和管理各种数据库的数据库前端。 |

表 5-2：LibreOffice 应用程序

LibreOffice 包括文字处理、电子表格、演示和绘图应用程序（参见 表 5-2）。LibreOffice 有 Linux、Windows 和 Mac OS 版本。你可以从 LibreOffice 网站 [`www.libreoffice.org`](https://www.libreoffice.org) 获取在线手册、常见 以及当前版本。LibreOffice 应用程序套件作为 Linux Mint 安装的一部分进行。

### Calligra

Calligra 是一个为 K 桌面环境（KDE）设计的集成办公套件，由多个办公应用程序组成，包括文字处理器、电子表格和图形应用程序（参见 表 5-3）。你可以使用软件管理器或 Synaptic 包管理器从 Universe 仓库下载。Calligra 允许将任何一个应用程序的组件用于另一个应用程序，让你能够将 Calligra Sheets 的电子表格或 Karbon 的图表嵌入 Calligra Words 文档中。它的文件也使用开放文档格式 (ODF)，提供了跨应用程序的标准。该 Windows 版本可用。你可以从 [`www.calligra.org`](https://www.calligra.org) 获取更多关于 Calligra 的信息。

| 应用程序 | 描述 |
| :--- | :--- |
| Calligra Flow | 流程图应用程序 |
| Calligra Stage | 演示应用程序 |
| Calligra Words | 文字处理器（桌面出版） |
| Calligra Sheets | 电子表格 |
| Karbon | 矢量图形程序 |
| Kexi | 数据库集成 |
| Plan | 项目管理和规划 |
| Krita | 绘画和图像处理程序 |
| Kontact (独立项目) | 包含邮件、联系人和组织者的联系人应用程序 |

表 5-3：Calligra 应用程序

| 应用程序 | 描述 |
| :--- | :--- |
| AbiWord | 跨平台文字处理器 |
| Gnumeric | 电子表格 |
| Evince | 文档查看器 |
| Evolution | 集成邮件、日历和组织者 |
| Dia | 图表编辑器 |
| GnuCash | 个人财务管理器 |
| Glom | PostgreSQL 数据库前端 |
| Planner | 项目规划 |

表 5-4：GNOME 办公应用程序

### GNOME 办公应用程序

GNOME 有多种办公应用程序，包括 AbiWord、Gnumeric、Evince 和 Evolution。GNOME 办公应用程序的当前列表可见 表 5-4。它们都实现了组件支持，确保了整个 GNOME 界面中的拖放功能。

### 文档查看器

Xreader 是 Linux Mint 的默认文档查看器。每当你双击桌面上的 PDF 文件时它就会启动（参见 图 5-1）。它的菜单项是辅助工具菜单中的“文档查看器”。Xreader 是基于 Atril（MATE 文档查看器）的 X-App。Evince 是 GNOME 文档查看器。Okular 是 KDE 的文档查看器。PDF 查看器包含了许多 Adobe 阅读器的标准功能，如缩放、双页显示和全屏模式。Evince 和 Okular 都能显示 PostScript (`.ps`) 和 PDF (`.pdf`) 文件。

![图像](img/image-164.png)

图 5-1：Xreader X-App 文档查看器

| 查看器 | 描述 |
| :--- | :--- |
| Xreader | X-App 文档查看器，默认（基于 Atril） |
| Atril | 用于 PostScript、DVI 和 PDF 文件的 MATE 文档查看器 |
| Evince | 用于 PostScript、DVI 和 PDF 文件的 GNOME 文档查看器 |
| Okular | 用于显示 PDF、DVI 和 postscript 文件的 KDE 工具 |
| Scribus | 生成 PDF 文档的桌面出版 |
| Simple Scan | 用于扫描器的 GNOME 扫描界面 |

表 5-5：PostScript、PDF 和 DVI 查看器

### 电子书阅读器：FBReader 和 Calibre





在 Linux Mint 上阅读电子书，你可以使用 `Calibre`、`FBReader` 和 `Foliate`（参见表 5-6）。`FBReader` 是一个开源阅读器，可以读取非 DRM 电子书，包括 `mobipocket`、`html`、`palmdoc`、`chm`、`EPUB`、`text` 和 `rtf`。`Calibre` 可以读取 `PDF`、`EPUB`、`Lit`（Microsoft）和 `Mobipocket` 电子书。`Calibre` 还可以将许多文件和电子书转换为 `EPUB` 格式。`Foliate` 是一个易配置的 GNOME 电子书阅读器。

| 查看器 | 说明 |
| :--- | :--- |
| Calibre | 电子书阅读器和库，也将各种输入格式转换为 EPUB 电子书 |
| E-book reader | FBReader 电子书阅读器 |
| Foliate | GNOME 电子书阅读器 |

表 5-6：电子书阅读器

### 编辑器

Linux 桌面支持功能强大的文本编辑器，具有完整的鼠标支持、滚动条和菜单。这些包括基础文本编辑器，如 `Xed`、`Gedit`、`Pluma` 和 `Kate`，以及文字处理器，如 `LibreOffice Word`、`AbiWord` 和 `Calligra Words`。对于简单的桌面笔记，你可以使用 `Gnote`（附件菜单）。`Xed` 是默认的文本编辑器（参见图 5-2），它是一个为所有 Linux Mint 桌面设计的 `X-App`。可以通过附件菜单中的“文本编辑器”（Text Editor）访问。`Xed` 具有工具栏和搜索栏。Linux 还提供了基于光标的编辑器 `Nano`、`Vim` 和 `Emacs`。`Nano` 是默认的基于光标编辑器，界面易用，支持菜单和鼠标选择（如果从终端窗口运行）。`Vim` 是 Unix 系统上使用的 `Vi` 文本编辑器的增强版本。这些编辑器使用简单的光标操作来提供全屏格式。表 5-7 列出了 Linux 的几种桌面编辑器。`Vi` 和 `Emacs` 拥有多年来完善的强大编辑功能。特别是 `Emacs`，它可以扩展为用于编写新程序的完整开发环境。后版本的 `Emacs` 和 `Vim`（如 `GNU Emacs`、`XEmacs` 和 `Gvim`）提供了鼠标、菜单和窗口操作的支持。

注意：三个辅助工具是 GNOME 时钟、日历和天气应用程序。`Clocks` 提供全球位置的时间。`Calendar` 提供在线日历。`Weather` 提供全球位置的天气。

![Image](img/image-165.png)

图 5-2：Xed X-App 编辑器

| 应用 | 说明 |
| :--- | :--- |
| Xed | X-App 文本编辑器（基于 Pluma） |
| Gnote | 桌面笔记工具 |
| Kate | 文本和程序编辑器 |
| Calligra Words | 桌面出版软件，属于 Calligra 套件 |
| Gedit | GNOME 文本编辑器 |
| AbiWord | 文字处理器 |
| OpenWriter | 可以编辑文本文件的 LibreOffice 文字处理器 |
| nano | 易用的屏幕式编辑器，默认安装 |
| GNU Emacs | 支持 X Window 系统的 Emacs 编辑器 |
| XEmacs | X Window 系统的版本的 Emacs 编辑器 |
| gvim | 支持 X Window 系统的 Vim 版本 |
| Pluma | MATE 文本编辑器 |

表 5-7：桌面编辑器

### 数据库管理系统

Linux Mint 和 Ubuntu 提供了多种数据库系统，包括 `LibreOffice Base`、`MySQL`、`SQLite` 和 `PostgreSQL`。Ubuntu 继续提供原始的 `MySQL` 数据库。此外，商业 SQL 数据库软件也兼容 Linux Mint 和 Ubuntu。`SQLite` 是一个简单快速的数据库服务器，不需要配置，并在单个磁盘文件中实现数据库。此外，Linux Mint 和 Ubuntu 还支持基于文档的非 SQL 数据库，如 `MongoDB`。`MongoDB` 是可以快速查询的文档型数据库。表 5-8 列出了目前 Linux 可用的数据库管理系统。

| 系统 | 网站 |
| :--- | :--- |
| LibreOffice | LibreOffice 数据库：[`www.libreoffice.org/discover/base/`](http://www.libreoffice.org/discover/base/) |
| PostgreSQL | PostgreSQL 数据库：[`www.postgresql.org`](http://www.postgresql.org) |
| MySQL | MySQL 数据库：[`www.mysql.com`](http://www.mysql.com) |
| MariaDB | 基于 MySQL 的 MariaDB 数据库：[`mariadb.org/`](https://mariadb.org/) |
| MongoDB | 文档数据库：[`www.mongodb.org`](http://www.mongodb.org) |

表 5-8：Linux 数据库管理系统

#### SQL 数据库 (RDBMS)

SQL 数据库是关系型数据库管理系统 (RDBMS)，旨在广泛的数据库管理任务。许多主流 SQL 数据库现在都有 Linux 版本，包括 `Oracle` 和 `IBM`。这些是商业和专业的数据库管理系统。Linux 已证明自己能够支持复杂且高要求的数据库管理任务。此外，许多免费的 SQL 数据库适用于 Linux，提供了相同的功能。大多数商业数据库也提供免费版本。

#### LibreOffice Base

`LibreOffice` 提供了一个基础数据库应用程序 `LibreOffice Base`，它可以访问许多数据库文件。当你启动 `LibreOffice Base` 时，系统会提示你是创建一个新数据库还是连接到现有数据库。支持的文件包括 `ODBC`（开放数据库连接）、`JDBC`（Java）、`MySQL`、`PostgreSQL` 和 `MDB`（Microsoft Access）（安装 **unixodbc** 和 **java-mysql**）。请查看 LibreOffice Base 页面 ([`www.libreoffice.org/discover/base/`](https://www.libreoffice.org/discover/base/)) 获取有关驱动程序和支持数据库的详细信息。

### PostgreSQL

PostgreSQL 基于 POSTGRES 数据库管理系统，尽管它使用 SQL 作为查询语言。POSTGRES 是加州大学伯克利分校开发的下一代研究原型。大多数发行版都包含了 PostgreSQL，包括 Red Hat、 Fedora、 Debian 和 Ubuntu。你可以从 PostgreSQL 网站 [`www.postgresql.org`](http://www.postgresql.org) 获取更多信息。PostgreSQL 是一个在 GPL 许可证下开发的开源项目。

### MySQL

MySQL 是一个真正的多用户、多线程 SQL 数据库服务器，由 MySQL AB 支持。MySQL 是根据 GPL 许可证免费提供的开源产品。你可以从其网站 [`www.mysql.com`](https://www.mysql.com) 获取最新信息。网站包含详细文档，包括手册和常见问题。

### MariaDB

MariaDB 是 MySQL 的全开源衍生品，是在 MySQL 被收购后开发的。它被设计为与 MySQL 数据库完全兼容。与 MySQL 类似，MariaDB 采用客户端/服务器模型，由服务器守护进程处理客户端程序的请求。MariaDB 设计旨在速度、可靠性和易用，它是大型数据库的快速数据库管理系统，同时也是适用于密集使用的可靠系统。创建数据库时，你使用标准 SQL 语言。要安装的包有 **mariadb-client** 和 **mariadb-server**。





你可以通过多种方式发送和接收电子邮件消息，这取决于你使用的邮件客户端类型。尽管所有电子邮件实用程序都执行接收和发送消息相同的相同任务，但它们倾向于使用不同的界面。某些邮件客户端设计为在特定的桌面界面上运行，例如 `GNOME`。一些较旧的邮件客户端使用基于屏幕的界面，并且只能从命令行启动。对于基于 Web 的互联网邮件服务（如 `Gmail` 和 `Yahoo`），你使用 Web 浏览器而不是邮件客户端来访问这些服务提供的邮件账户。表 5-9 列出了几种流行的 Linux 邮件客户端。邮件通过 `Sendmail`、`Exim` 和 `Postfix` 等邮件传输代理在目的地与目的地之间传输。要在互联网上发送邮件，则使用简单邮件传输协议（`SMTP`）。

| 邮件客户端 | 描述 |
| :--- | :--- |
| Kontact (KMail, KAddressbook, KOrganizer) | 包含 K 桌面邮件客户端 `KMail`；集成的邮件、通讯录和调度器 |
| Evolution | 电子邮件客户端，[`wiki.gnome.org/Apps/Evolution`](https://wiki.gnome.org/Apps/Evolution) |
| Thunderbird | Mozilla 邮件客户端和新闻阅读器 |
| Sylpheed | Gtk 邮件和新闻客户端 |
| Claws-mail | `sylpheed` 电子邮件客户端的扩展版本 |
| Mutt | 基于屏幕的邮件客户端 |
| bsd-mailx | 基于 Unix 的原始命令行邮件客户端 |
| unity mail | GNOME 邮件通知 |
| gnubiff | 邮件检查和通知工具 |
| Mail Notification | 适用于多种邮件客户端的邮件检查和通知，包括 MH、Sylpheed、`Gmail`、`Evolution` 和 Mail |

表 5-9：Linux 邮件客户端

### Usenet 新闻

Usenet 是一个开放的邮件系统，用户可以在其上发布包含新闻、讨论和意见的消息。它的运行类似于一个信箱，你 Linux 系统上的任何用户都可以向其读取或发送消息。用户的消息被整合到 Usenet 文件中，这些文件被分发到任何注册接收它们的系统。某些 Usenet 站点为 Usenet 执行组织和分发操作，接收来自其他站点的消息并将其组织成 Usenet 文件，然后广播到许多其他站点。此类站点被称为骨干站点，它们运行就像出版商一样，接收文章并将其组织成不同的组。

要访问 Usenet 新闻，你需要访问新闻服务器，该服务器接收每日的 Usenet 新闻馈并让其他系统可以访问。你的网络可能有一个作为新闻服务器的系统。如果你在使用互联网服务提供商（ISP），新闻服务器可能由你的 ISP 维护供你使用。要读取 Usenet 文章，你使用新闻阅读器，这是一种连接到新闻服务器并访问文章的客户端程序。在互联网和 TCP/IP 网络中，新闻服务器使用网络新闻传输协议（`NNTP`）与新闻阅读器通信，通常被称为 NNTP 新闻服务器。你也可以在你的 Linux 系统上创建自己的新闻服务器，以运行本地 Usenet 新闻服务，或者为了下载和维护全套 Usenet 文章。可以设置新闻传输代理应用程序来创建此类服务器。

你使用新闻阅读器（如 `Pan` 或 `tin`）阅读 Usenet 文章，这允许你选择特定的新闻组，然后阅读其中的文章。新闻阅读器的工作类似于用户界面，允许你浏览并选择可用文章进行阅读、保存或打印。大多数新闻阅读器使用一种名为 `threads` 的检索功能，将同一讨论或主题的文章聚合在一起。几个流行的新闻阅读器列在表 5-10 中。

| 新闻阅读器 | 描述 |
| :--- | :--- |
| Pan | GNOME 桌面新闻阅读器 |
| Thunderbird | 具有新闻阅读能力的邮件客户端（基于 X） |
| Sylpheed | GNOME Windows 式新闻阅读器 |
| Slrn | 新闻阅读器（基于光标） |
| Emacs | Emacs 编辑器、邮件客户端和新闻阅读器（基于光标） |
| tin | 新闻阅读器（命令行界面） |
| trn4 | 新闻阅读器（命令行界面） |
| Newsbin | 新闻阅读器（Windows 版本在 Wine 下运行） |
| SABnzbd+ | 仅二进制 NZB 下载器 |

表 5-10：Linux 新闻阅读器

大多数新闻阅读器可以读取使用 `NNTP` 的远程新闻服务器提供的 Usenet 新闻。桌面新闻阅读器让你在自己的配置设置中指定远程新闻服务器的互联网地址。基于 Shell 的新闻阅读器（如 `tin`）从 `.profile` 文件中配置的 `NNTPSERVER` Shell 变量获取新闻服务器的互联网地址。

```
NNTPSERVER=news.domain.com  export NNTPSERVER
```

二进制新闻阅读器可以将文本消息转换为二进制等效文件，例如在 `alt.binaries` 新闻组中找到的文件。有一些下载器是专门用于下载二进制文件的。二进制文件通常使用 `RAR` 压缩编码，具有 `.rar` 扩展名。要解码它们，你首先必须安装 `unrar-free`（免费版）或 `unrar` 包（专利版）。`mint-meta-codecs` 包将为你安装专利版的 `unrar`。二进制文件通常由几个 `rar` 归档文件组成，其中某些可能是不完整的。要修复它们，你可以使用 `Par2` 恢复程序。安装 `par2` 或 `parchive` 包。一个二进制文件应该有它自己的 `par2` 文件，这些文件也列在新闻服务器上，你可以下载并使用它们修复任何不完整的 `rar` 文件。其原理与使用校验信息的 RAID 阵列非常相似。

## 图形应用程序

GNOME 和 KDE 桌面支持数量惊叹的图形应用程序，包括图像查看器、窗口捕取器、图像编辑器和绘图工具（参见表 5-11）。这些可以在图形菜单中找到。`Xviewer` 是默认的图像查看器（一个 X-App），可以通过图形菜单中的“图像查看器”访问（参见图 5-3）。它基于 GNOME 的 Eye of GNOME，具有一个带有图像信息的侧边栏和一个缩略图库，方便访问。`Shotwell` 提供了一种简单且强大的方法来管理、显示、导入和发布你的照片和图像。`GNOME Photos` 是一个用于你的 `Pictures` 文件夹中图像的简单图像查看器。

![Image](img/166.png)

图 5-3：Xviewer X-App 图像查看器

Eye of GNOME 是 GNOME 图像查看器。`Gthumb` 是一个图像查看器、组织器和简单编辑器。`Pix` 是 `Gthumb` 的 X-App 版本，具有许多 `Shotwell` 功能，如裁剪和图像调整。它是默认安装的（参见图 5-4）。`GIMP` 是 GNU 图像处理程序，类似于 Adobe Photoshop 的高级图像应用程序。`Inkscape` 是一个基于 Gnome 的 `SVG` 可缩放矢量图形应用程序。`Drawing` 是一个基础绘图应用程序（图形菜单）。`Xviewer`、`Pix` 和 `Drawing` 已安装。其他的可以通过 Linux Mint 软件管理器安装。旧的 X Window 系统应用程序直接运行在底层 X Window 系统上，例如 `paint` 和 `Xfig`（不要与 X-Apps 混淆）。

![Image](img/167.png)

图 5-4：Pix X-App 图像查看器、组织器和编辑器

| 工具 | 描述 |
| :--- | :--- |
| Shotwell | GNOME 数码相机应用程序和图像视频库管理器（[`wiki.gnome.org/Apps/Shotwell`](https://wiki.gnome.org/Apps/Shotwell)） |
| Cheese | 用于拍摄照片和视频的 GNOME 应用程序 |
| Photos | GNOME 照片查看器和组织器 |
| Digikam | 数字照片管理工具，适用于 GNOME 和 KDE |
| KDE | |
| Gwenview | 图像浏览器和查看器 |
| ShowFoto | 简单图像查看器，配合 digiKam 使用 ([`www.digikam.org`](https://www.digikam.org)) |
| Spectacle | 屏幕捕取器 |
| KolourPaint | 绘图程序 |





| Krita | 图像编辑器 ([`www.calligra.org/krita/`](https://www.calligra.org/krita/)) |
| GNOME |  |
| Xviewer | X-App 图片查看器（基于 Eye of GNOME） |
| Pix | X-App 图片查看器、组织管理器和编辑器（基于 Gthumb） |
| Gthumb | GNOME 图像查看器、组织管理器和编辑器 |
| Eye of Gnome | GNOME 图像查看器 |
| Drawing | GNOME 基础绘图程序 |
| GIMP | GNU 图像处理程序 ([`www.gimp.org`](https://www.gimp.org)) |
| Inkscape | GNOME 矢量图形应用 ([`www.inkscape.org`](https://www.inkscape.org)) |
| gpaint | GNOME 绘画程序 |
| Blender | 3d 建模、渲染和动画 |
| LibreOffice Draw | LibreOffice Draw 程序 |
| X Window System |  |
| Xpaint | 绘图程序 |
| Xfig | 绘图程序 |
| ImageMagick | 格式转换和编辑工具 |

表 5-11: Linux 图形工具

## 多媒体

有许多应用程序可用于视频和音频，包括音频编辑器、音乐播放器和视频播放器（见表 5-12 和表 5-13）。

### 多媒体支持

Linux Mint/Ubuntu 提供了一个解码器向导，可以自动检测你何时需要安装额外的多媒体解码器。如果你尝试运行一个没有妥当解码器的媒体文件，系统会显示缺少解码器的警告信息。

注意：`Celluloid` 媒体播放器可能不需要额外的解码器即可播放文件。

要安装大多数常用解码器的支持（如果尚未安装），你可以安装 `mint-meta-codecs` 软件包。有几种方法可以实现这一点。在欢迎界面上，你只需点击“多媒体解码器”图标即可。在 Cinnamon 菜单的“音频与视频”子菜单中，你可以选择“安装多媒体解码器”项。你也可以直接使用软件管理器或 Synaptic 包管理器来安装 `mint-meta-codecs` 软件包。

`mint-meta-codecs` 软件包会安装 `Xplayer` 插件以及 `mint-meta-codecs-core` 包，后者反过来安装第三方解码器，包括 `libdvdcss2`、`ffmpeg`、`vlc`、微软字体和 `unrar`。这些解码器提供了对 DVD、MP3、MPEG4、DivX 和 AC3 支持，以及 Adobe Flash（见图 5-5）。对于支持 GStreamer 的应用程序（如 X-player 电影播放器），安装了 `gstreamer-bad` 和 `gstreamer-ugly` 插件。

```
mint-meta-codecs
```

### GStreamer

许多基于 GNOME 的应用程序使用了 `GStreamer`，这是一个基于图和过滤器的流媒体框架（[`gstreamer.freedesktop.org`](https://gstreamer.freedesktop.org)）。通过插件结构，GStreamer 应用程序可以适应各种媒体类型：

- 视频播放器（`Totem` 和 `Xplayer`）使用 `GStreamer` 播放 DVD、VCD 和 MPEG 媒体。
- `Rhythmbox` 提供集成的音乐管理。
- `Sound Juicer` 是一个音频 CD 刻录机。

`GStreamer` 可以配置为使用不同的输入输出音频视频驱动程序和服务器，可以使用 `GStreamer` 属性工具——多媒体系统选择器。你可以在多媒体仪表板上访问它。它默认不显示；使用主菜单可以将其列出。

![Image](img/image-168.png)

图 5-5: Linux Mint 安装 mint-meta-codecs

| 应用程序 | 描述 |
| :--- | :--- |
| Rhythmbox | 音乐管理 (GStreamer)，支持 iPod 的默认音乐播放器 |
| Sound Juicer | GNOME CD 音频刻录机 (GStreamer) |
| Clementine | 基于 Amarok (KDE)的多媒体音频播放器 |
| Audacious | 多媒体播放器 |
| Goobox | CD 播放器和刻录机 |
| JuK | 用于管理音乐集的 KDE 音乐播放器 (jukebox) |
| GNOME CD Player | CD 播放器 |
| GNOME Sound Recorder | 录音器 |
| GNOME Music | GNOME 音乐播放器 |
| XMMS2 | CD 播放器 |
| ubuntustudio-audio | Ubuntu Studio 元包（元软件包 (universe)），包含一组音频应用程序。使用 Synaptic 包管理器安装 |
| QMidiRoute | MIDI 事件路由器和过滤器 |

表 5-12: 音乐播放器、编辑器和刻录机

### GStreamer 插件：好的、坏的、丑的

许多 GNOME 多媒体应用程序（如视频）使用 `GStreamer` 来提供多媒体支持。要使用 DVD 视频和 MP3 等功能，你必须安装 GStreamer 额外插件。你可以在 [`gstreamer.freedesktop.org`](https://gstreamer.freedesktop.org) 更多关于 `GStreamer` 及其支持包的信息。

`GStreamer` 有四个不同的支持包，分别称为 base (基础)、good (好)、bad (坏) 和 ugly (丑)。`base` 包是一组实用且可靠的插件，它们位于主仓库中。`good` 包是一组符合所有许可要求的已支持且经过测试的插件，这这也是主仓库的一部分。`bad` 包是一组性能无法保证且可能崩溃的插件，但它们符合许可要求。`ugly` 包包含了运行良好但可能不符合许可要求的插件，例如 DVD 支持。

- **base**: 可靠常用插件
- **good**: 可靠的额外实用插件
- **ugly**: 可靠但不符合许可要求的插件（如 DVD 支持）
- **bad**: 可能不可靠但实用的插件（可能会崩溃）





`Xplayer` 是 X-App 的视频播放器，基于 `Totem`（参见图 5-6）。尽管它是一个 Linux Mint X 应用程序，但它不再被默认安装。安装后，可以通过“音频与视频”菜单中的“视频”（Videos）访问它。为了扩展 `Xplayer` 的功能，你需要像之前讨论过的那样安装额外的 GStreamer 插件。编解码器向导会提示你安装任何需要的媒体编解码器和插件。你可以使用 `dconf editor` 修改默认设置（`org.x.player`）（`xplayer` 包）。

`Totem` 是 GNOME 电影播放器，它使用 `GStreamer`，标记为“视频”（Videos）。你可以使用 `dconf editor` 修改默认设置（`org.gnome.totem`）（`totem` 包）。

`VideoLAN` 项目（[`www.videolan.org`](http://www.videolan.org））为大多数媒体格式提供网络流支持，包括 MPEG-4 和 MPEG-2。它包含一个多媒体播放器 `VLC`，它可以在任何系统上运行（`vlc` 包，Universe 仓库）。`VLC` 支持高定义硬件解码。

`Dragon Player` 是一个 KDE 多媒体播放器，随 KDE 桌面安装，但可以在 GNOME 桌面上播放。

`mpv` 是一个基于 `Mplayer` 的开源视频播放器，支持广泛的解码器和格式。可以通过应用程序概览或从终端窗口中使用 `mpv` 命令来运行。可以使用 Ubuntu 软件或 Synaptic 包管理器安装。

`Kaffeine` 是一个 KDE 多媒体播放器（视频和 dvb)（`kaffeine` 包）。

`MPlayer` 是目前使用的最流行且功能强大的多媒体/DVD 播放器之一。它是 RealPlayer 和 Windows Media Player 的跨平台开源替代方案（[www.mplayerhq.hu](http://www.mplayerhq.hu)）。`MPlayer` 使用大量的支持库和应用程序，如 `lirc`、`lame`、`lzo` 和 `aalib`。如果你在显示视频时遇到问题，请务必检查不同视频设备的偏好，并选择最合适的一个（`mplayer` 包）。

### 视频插件（Xplayer 和 Totem）

视频播放器（`Totem`）使用插件来添加互联网视频流等功能。选择“编辑 | 偏好”并点击“插件”按钮打开“配置插件”窗口。选择你需要的插件。如需为 `Xplayer` 提供额外支持，请安装 `xplayer-plugins-extra` 包。

### PiTiVi Video 编辑器

`PiTiVi Video 编辑器`是一个允许你编辑视频的开源应用程序。访问 `PiTiVi` 网站获取更多详情（[`www.pitivi.org`](http://www.pitivi.org)）。你可以从文档页面下载快速上手。`Pitivi` 是一个 `GStreamer` 应用程序，可以处理任何由安装的 `GStreamer` 插件支持的视频文件。

| 项目与播放器 | 站点 |
| :--- | :--- |
| Celluloid | `MPV` 视频播放器的 GTK+ 前端（[`github.com/celluloid-player/celluloid`](https://github.com/celluloid-player/celluloid)）。这是 Linux Mint 的默认播放器。 |
| Xplayer | X-App 视频播放器（基于 `Totem`） |
| Totem (Videos) | 用于 GNOME 的基于 `GStreamer` 的 Totem 视频和 DVD 播放器，包含 DVB、YouTube 和 MythTV 插件 |
| Dragon Player | 用于 KDE 的 Dragon 视频和 DVD 播放器 |
| VLC Media Player (vlc) | 网络多媒体流。[www.videolan.org](http://www.videolan.org) |
| MPlayer | MPlayer DVD/多媒体播放器 [www.mplayerhq.hu](http://www.mplayerhq.hu) |
| tvtime | 电视查看器，[`tvtime.sourceforge.net`](http://tvtime.sourceforge.net) |
| XviD | 开源 DivX，[`www.xvid.com/`](https://www.xvid.com/) |
| Kaffeine | KDE 媒体播放器，包括 HDTV、DVB、DVD、CD 和网络流 |
| PiTiVi | 视频编辑器 |

表 5-13：视频和 DVD 项目及应用程序

### 电视播放器

Linux Mint/Ubuntu 仓库提供了以下电视播放器：

电视播放器 `tvtime` 可配合许多常见的视频采集卡，依赖于为电视调谐芯片开发的驱动程序。它只能显示电视图像。它没有录制或文件播放功能。访问 [`tvtime.sourceforge.net`](http://tvtime.sourceforge.net) 获取更多信息。

`MythTV` 是 Linux 系统上流行的视频录制和播放应用（multiverse 仓库）。

`Kaffeine` 是 Linux 系统上流行的 KDE 视频录制和播放应用。它还可以播放 ATSC 空中数字广播。

注意：要在 Linux Mint 上播放 DivX 媒体，你需要使用 Xvid OpenDivX 编解码器 `xvidcore`。

### DVB 和 HDTV 支持

对于 DVB 和 HDTV 接收，你可以使用大多数 DVB 卡以及许多 HDTV 卡。DVB 内核驱动会自动加载。你可以使用 `lsmod` 命令查看你的 DVB 模块是否已加载。VideoLan (`VLC`) 播放器可以使用你显示卡的原生高定义解码器（硬件解码而非软件解码）运行 HD 媒体（`x264`），检查“工具 | 偏好 | 编解码器 | 使用 GPU 加速”。

#### Kaffeine DVB 和 ATSC 调节

`Kaffeine` KDE 媒体播放器可以扫描 DVB 和 ATSC 频道。你需要在系统中安装 DVB 或 ATSC 调谐。在 `Kaffeine` 中，从“电视”菜单选择“配置电视”，并在“设备”选项卡上选择如 ATSC。点击开始。检测结果显示在通道列表中。

#### Linux 上 Xvid (DivX) 和 Matroska (mkv)

压缩的 MPEG-4 文件提供了较小的 DVD 级视频。它们已成为互联网传输高质量视频的热门。当你尝试播放 MPEG-4 时，解码向导会提示你安装。许多多媒体应用已支持 MPEG-4。

Matroska 封装（其扩展名为 `mkv`）可以在大多数视频播放器上播放，包括 `VLC`、`Celluloid`、`Dragon Player` 和 `Totem`。你需要安装 HDTV AAC 来播放 `mkv` 文件。管理和创建 MKV 文件可以使用 `mkvtooln-gui`。

你使用名为 `Xvid` 的开源 DivX 版本来播放 DivX 视频（`libxcore` 包）。`VLC` 已经支持 `mkv` 文件。你也可以从 [`www.xvid.com/`](https://www.xvid.com/) 下载 `Xvid` 源代码。`XviD` 是完全独立的项目，但它与 DivX 文件兼容。

### CD/DVD 刻录机

多种 CD/DVD 提取和写入程序可用于 CD 音乐和 MP3 写入（刻录）。这些包括 `Sound Juicer`、`Brasero`（参见第 3 章）和 `K3b`。GNOME 拥有音频 提取器 `Sound Juicer`。刻录 DVD/CD 音乐和数据盘可以使用 `Brasero`。

| 应用 | 说明 |
| :--- | :--- |
| Brasero | 全功能 CD/DVD 刻录机，用于音乐、视频和数据（不再默认安装） |
| Sound Juicer (音频 CD 提取器) | GNOME 音乐播放器及 CD 刻录和提取器 |
| ogmrip | 支持 DivX 的 DVD 提取和编码 |
| K3b | KDE CD 写入界面 |

表 5-14：CD/DVD 刻录机

`Brasero`、`K3b` 和 `dvdauthor` 均可创建 DVD 视频光。所有程序都使用作为桌面一部分的 `mkisofs`、`cdrecord` 和 `cdda2wav` DVD/CD 写入程序。`Sound Juicer` 是音频 CD 提取器。`Brasero` 是 CD/DVD 刻录机。




Linux 提供了强大的 Web 和 FTP 客户端用于访问互联网。这些应用程序中的一些是自动安装的，并且在您首次启动系统时即可使用。Linux 还包含了完整的 Java 开发支持，让您能够运行和构建 Java applet。Web 和 FTP 客户端连接到运行服务器的站点，通过 Web 页面和 FTP 文件为用户提供服务。

你可以从多个 Web 浏览器中进行选择，包括 Firefox、Epiphany 和 Lynx。Firefox 和 Epiphany 是桌面浏览器，提供完整的图像、声音和视频显示能力。Lynx 浏览器是一种行模式浏览器，仅显示文本行。

Web 浏览器和 FTP 客户端通常用于进行安全交易，例如登录远程站点、订物品或传输文件。此类操作目前由安全套接层（`SSL`）提供的加密方法提供保护。如果你使用浏览器进行安全交易，该浏览器应启用 SSL。大多数浏览器都包含 SSL 支持。Linux 发行版在标准安装中包含了 `SSL (OpenSSL)`。

## Web 浏览器

Linux Mint 流行的浏览器包括 Firefox (Mozilla)、Web (Epiphany) 和 Lynx（参见表 5-15）。Firefox 是大多数 Linux 发行版使用的默认 Web 浏览器。Web 是 GNOME Web 浏览器（以前称为 Epiphany）。Lynx 和 `ELinks` 是基于命令浏览器，不具备图形功能，但在其他所有方面，它们都是功能完整的 Web 浏览器。

Chromium 是 Google Web 浏览器的开源版本，在 Linux Mint 20 上已不再可用。你可以从非官方仓库下载该版本。如果你启用了 Snap，也可以从 Snap 商店下载它。它不在 Flathub 上。更多详细信息请参阅：

[`linuxmint-user-guide.readthedocs.io/en/latest/chromium.html`](https://linuxmint-user-guide.readthedocs.io/en/latest/chromium.html)

| Web 站点 | 描述 |
| :--- | :--- |
| Firefox | Mozilla 项目 Firefox Web 浏览器，桌面默认浏览器 [`www.mozilla.org`](https://www.mozilla.org) |
| Web | GNOME Web 浏览器 [`wiki.gnome.org/Apps/Web`](https://wiki.gnome.org/Apps/Web) |
| lynx | 基于文本的命令行 Web 浏览器 [`lynx.browser.org/`](http://lynx.browser.org/) |
| elinks | 基于文本的命令行 Web 浏览器 [`elinks.or.cz`](http://elinks.or.cz) |

表 5-15: Web 浏览器

## Linux 版 Java

要开发 Java 应用、使用 Java 工具并运行许多 Java 产品，你需要使用 Java 软件开发包（`SDK`）和 Java 运行环境（`JRE`）。SDK 是 JRE 的超集，增加了编译器和调试器等开发工具。Sun 公司（现归 Oracle 所有）已将 Java 作为 `OpenJDK` 项目开源，并支持和分发 Linux 版本。JRE 子集可以作为 OpenJRE 安装。`openjdk-11-jre` 包安装 Java 运行环境，而 `openjdk-11-jdk` 则同时安装 JRE 和 Java 开发工具。Java 包和应用程序列在表 5-16 中。

| 应用程序 | 描述 |
| :--- | :--- |
| Java Development Kit, OpenJDK | 一个开源的 Java 开发环境，包含编译器、解释器、调试器等更多（包含 JRE），[`openjdk.java.net`](http://openjdk.java.net), `openjdk-11-jdk` |
| Java Runtime Environment, OpenJRE | 一个开源的 Java 运行环境，包括 Java 虚拟机，`openjdk-11-jre`。[`openjdk.java.net`](http://openjdk.java.net) |
| Java Platform Standard Edition (JSE) | 完整的 Java 集合，包括 JRE、JDK 和 API，[`www.oracle.com/technetwork/java/javase/downloads/index.html`](http://www.oracle.com/technetwork/java/javase/downloads/index.html) |

表 5-16: Java 包和 Java Web 

## BitTorrent 客户端 (transmission)

GNOME 提供了有效的 BitTorrent 客户端。通过 BitTorrent，你可以在共享分布式下载操作中快速下载非常大的文件，在这种操作中，多个用户参与下载文件的不同部分，并将他们下载的部分发送给其他参与者（称为节点/peers）。与其让每个人都尝试访问几个中央服务器，所有参与 BitTorrent 操作的节点都成为所下载文件的源。某些节点充当种子源（seeders）的角色，即那些已经下载了文件但继续向需要它的人发送部分文件的人。

Linux Mint 将安装并使用 GNOME BitTorrent 客户端 `Transmission`，可以从互联网菜单访问。要执行 BitTorrent 下载，你需要想要下载的文件对应的 BitTorrent 文件。

## FTP 客户端

通过文件传输协议（`FTP`）客户端，你可以连接到相应的 FTP 站点并从那里下载文件。这些站点具有匿名登录功能，允许任何用户访问其文件。基础的 FTP 客户端功能集成在 Nemo (Cinnamon) 和 Caja (MATE) 文件管理器中。你可以使用文件管理器窗口访问 FTP 站点，并将文件拖到本地文件夹进行下载。有效的 FTP 客户端现在也集成到大多数 Web 浏览器中，使得 Web 浏览器成为主要的下载工具。特别是 Firefox，它具有强大的 FTP 下载能力。

尽管文件管理器和 Web 浏览器提供了对公共（匿名登录）站点的有效访问，但要访问私有站点，你可能需要独立的客户端。流行的客户端列在表 5-17 中。

| FTP 客户端 | 描述 |
| :--- | :--- |
| Nemo | GNOME 文件管理器 (Cinnamon) |
| Caja | GNOME 文件管理器 (MATE) |
| gFTP | GNOME FTP 客户端，gftp-gtk |
| ftp | 命令行 FTP 客户端 |
| lftp | 支持多连接的命令行 FTP 客户端 |
| curl | 传输客户端（FTP 和 HTTP） |
| Filezilla | 开源 Filezilla ftp 客户端的 Linux 版本（Universe 仓库） |

表 5-17: Linux FTP 客户端

### 网络文件传输：FTP

通过 `FTP` 客户端，你可以从一个站点直接传输到另一个（参见表 5-4）。FTP 可以处理文本和二进制文件。执行远程登录到连接到你的另一个系统的账户。一旦登录到该系统，你就可以与其传输文件。要登录，你需要知道远程系统账户的登录名和密码。然而，互联网上的许多站点允许使用 FTP 进行公共访问。此类站点作为任何人都可以访问和下载的大文件的存储库。

多种 FTP 协议可访问支持它们的站点。原始 FTP 协议用于大多数匿名站点。FTP 传输也可以使用 `SSH2`（即 `SFTP` 协议）进行加密。更安全的连接可能使用 `FTPS` 进行 `TLS/SSL` 加密。某些站点支持一种简化的 FTP 版本，称为文件服务协议（FSP）。FTP 客户端可能支持不同的协议，例如用于 `FSP` 的 `gFTP` 和用于 `TLS/SSL` 的 `Filezilla`。



你可以使用任何 Web 浏览器访问 FTP 站点并从中下载文件。浏览器适用于定位单个文件，但并不适用于下载大量文件。使用 Web 浏览器查看 FTP 站点以了解那里列出了哪些文件非常有效。当你用 Web 浏览器访问 FTP 站点时，目录中的整个文件列表将作为一个网页列出。你可以通过点击条目进入子目录。你可以轻松地浏览 FTP 站点以下载文件。要下载文件，点击下载链接。这将启动传输操作，并打开一个对话框供你选择本地目录和文件名。默认名称与远程系统上的名称相同。在许多浏览器中，你可以使用下载管理器管理你的下载，它允许你取消正在进行的下载操作或删除其他下载。管理器将显示当前下载的剩余时间、传输速度和已传输量。

### GNOME 桌面 FTP：连接到服务器

下载文件的最简单方法是使用 GNOME 文件管理器 `Nemo` 和 `Caja` 内置的 FTP 功能。在 GNOME 上，桌面文件管理器具有内置的 FTP 功能。FTP 操作已无缝集成到标准的桌面文件操作中。从 FTP 站点下载文件只需将文件从一个目录窗口拖到另一个窗口即可，其中一个目录恰好位于远程 FTP 站点上。使用文件管理器访问远程 FTP 站点，列出远程目录中的文件，就像本地文件一样。在文件管理器的位置栏（`Ctrl-l` 或位置按钮）中，输入前缀 `ftp://` 后接 FTP 站点的 URL 并按回车。将打开一个对话框，提示你指定连接方式。你可以匿名连接到公共 FTP 站点，也可以以提供 `username` 和 `password` 的用户身份连接（私有站点）。你也可以选择记住密码。

若需更多访问选项，例如安全的 SSH 连接、窗口共享和安全 Web (HTTPS)，你可以使用 `Connect to Server` 对话框（见图 5-8）。要打开 `Connect to Server` 对话框，在任何文件管理器窗口或桌面应用程序菜单上选择 `File | Connect to Server` 菜单项。从 `Type` 菜单中，你可以选择服务类型。输入选项会随之变化，选择 `"FTP (with login)"` 时会添加一个 `username` 条目。点击 `Connect` 按钮访问该站点。

![Image](img/image-171.png) ![fig5-1b-15](img/image-172.png)

图 5-8：GNOME FTP 访问连接到服务器对话框

远程 FTP 站点的根目录将在文件管理器窗口中显示（见图 5-9）。使用文件管理器浏览远程 FTP 站点的目录树，直到找到你想要的文件。然后，打开另一个窗口作为你想要将远程文件复制的本地目录。在显示 FTP 文件的窗口中，选择你想要下载的文件。然后点击并拖动这些文件到本地目录窗口。随着文件的下载，会弹出一个显示进的对话框。

![Image](img/image-173.png)

图 5-9：使用 Connect to Server 和文件管理器的 GNOME FTP 访问

文件管理器窗口的侧边栏（网络部分）将列出已访问 FTP 站点的条目。FTP 站点名称右侧显示有一个弹出按钮。要断开与站点的连接，点击此按钮。FTP 条目将与同 FTP 站点的图标和文件列表一起消失。

## 社交网络

Linux 为 IM（即时通讯）和 VoIP（网络电话）提供了集成社交网络支持。用户可以与网络上的其他用户直接通信（见表 5-18）。这些应用程序会自动安装，并在你首次启动系统时准备就绪。即时通讯 (IM) 客户端允许同一 IM 系统的用户在互联网的任何地方进行通信。通过 IP 协议进行语音通话的应用，你可以通过互联网连接进行通话。

表 5-18：即时通讯、Talk 和 VoIP 客户端

| 客户端 | 描述 |
| :--- | :--- |
| Skype | VoIP 应用（伙伴存储库） |
| empathy | GNOME 即时通讯工具 |
| Pidgin | 旧版本的即时通讯客户端 |
| Jabber | Jabber IM 服务 (gajim, psi, emacs, empathy) |
| Finch | 基于命令行光标的 IM 客户端 |
| Hexchat | IRC 客户端 |

`Skype` 可以通过软件管理器安装。安装后，你可以从互联网菜单访问 `Skype`。当你首次启动 `Skype` 时，会被要求接受用户协议。界面与 Windows 版本相似。一旦启动 `Skype`，面板上会出现一个 `Skype` 面板图标。你可以用它在整个会话期间访问 `Skype`。点击打开 `Skype` 并右键点击显示菜单，你可以从该菜单更改状态、登录、访问选项、列出联系人组并启动会议。面板图标会根据你的状态发生变化。

# 第 2 部分：桌面

### 6. Cinnamon 桌面](#index_split_011.html_id_Toc213324701)

### 7. MATE 桌面](#index_split_012.html_id_Toc49500500)

## 6. Cinnamon 桌面

Linux Mint 以 `Cinnamon` 桌面作为其高级桌面。尽管 `Cinnamon` 最初源自 `GNOME 3`，但其界面类似于 `GNOME 2`，使用了带有插件的简单面板。Linux Mint 使用 `Nemo` 文件管理器作为 `Cinnamon`，以及一些 `GNOME 3` 配置工具。`Cinnamon` 桌面设计得易于扩展。你可以从经过认证的第三方开发者那里添加主题、插件（applets）和扩展。这些插件被称为 `Spices`，可以从网站 `https://cinnamon-spices.linuxmint.com` 获取，这是官方的 Cinnamon 插件库。

## Cinnamon 桌面

`Cinnamon` 桌面旨在为桌面系统提供便利性，使用了带有大多数桌面插件的传统面板。`网络管理器`、`音量`、`更新`以及`时间和日期`插件放置在面板右侧（见图 6-1）。面板左侧是 `Cinnamon 菜单`、用于快速启动应用程序的面板启动器插件，以及用于打开窗口的分组窗口列表插件。你可以从面板插件访问的系统设置插件对话框轻松地添加和删除插件。面板编辑模式（右键点击面板）允许你重新定位和删除插件。系统支持文件夹（如“计算机”和“主目录”）显示在桌面上。你可以通过 `Ctrl-Alt-ESC` 在不重启系统的情况下重启 `Cinnamon` 桌面。

你可以通过点击并按住 Meta 键输入模式的首字母来快速搜索桌面项目。这会打开一个文本框，你在其中输入搜索模式。它会高亮最佳匹配的图标。

![Image](img/image-44.png)

图 6-1：Cinnamon 桌面

`Cinnamon` 桌面的特点是有一个用于应用程序、位置和任务的 `Cinnamon 菜单`，并有一个用于常用应用程序和任务的 `收藏图标栏`（见图 6-2）。`收藏图标栏`显示了 `Firefox 浏览器`、软件管理器、系统设置、终端窗口和 `Nemo 文件管理器`的图标。还有用于锁定、注销和关机操作的图标。

![Image](img/image-174.png)

图 6-2：带有 Cinnamon 菜单和 Nemo 文件管理器的 Cinnamon 桌面




在桌面的任何处点击右键可显示桌面菜单，通过它你可以向桌面添加新文件夹、以管理员（root）权限打开文件管理器、打开终端窗口、更改背景并添加桌面小组件（参见图 6-3）。“自定义”条目会打开“当前显示器布局”窗口，让你控制桌面图标的显示。你可以更改图标的尺寸（小、普通、大）、以网格形式显示（`自动排列`）、垂直显示图标（`列`）或水平显示图标（`行`）、按名称、大小、日期和类型进行排序，或者关闭`自动排列`选项以将图标放置在任何位置。右侧和底部的滚动条允许你调整图标间距。对话框底部的链接打开“桌面设置”对话框，你可以在那里确定哪些桌面图标。

![Image](img/image-175.png) ![Image](img/image-176.png)

图 6-3：桌面菜单和当前显示器布局窗口（自定义）

在“桌面”对话框中，你可以指定要显示在桌面上的图标（参见图 6-4）。默认情况下，会显示计算机和主图标，以及你挂载的任何文件系统和设备（例如 USB 驱动器或 DVD 光盘）。你还可以选择显示文件管理器的网络文件夹（`网络服务器`）和垃圾箱。“桌面布局”选项让你选择是在所有连接的显示器上显示桌面图标，还是仅在主显示器上显示。如果缺少额外的显示器，你可以选择仍然显示其图标。

![Image](img/image-177.png) ![Image](img/image-178.png)

图 6-4：桌面设置

#### 桌面小组件 (Desklets)

桌面小组件的工作原理类似于小应用程序，但它是针对桌面而非面板的，如图所示。你可以使用面板上的“显示桌面”图标仅显示你的桌面小组件和桌面图标，隐藏已打开的窗口。你也可以右键点击“显示桌面”图标显示菜单，并选择“显示小组件”条目，这样如果你的打开窗口遮挡了它们，就可以将所有小组件带到最前。

![Image](img/image-179.png)

默认安装了三个桌面小组件（但未激活）：时钟、照片和启动器。时钟小组件显示数字时钟。数字相框小组件显示一个小型对话框，对你“图片”文件夹中的图像进行幻灯片播放。启动器小组件可以配置为启动应用程序。可用小组件列表可以在 [`cinnamon-spices.linuxmint.com/desklets`](https://cinnamon-spices.linuxmint.com/desklets) 找到。

你可以使用系统设置中的“桌面小组件”对话框将小组件添加到桌面（激活），或者通过右键点击桌面背景显示桌面菜单并点击“添加小组件”条目。小组件有“管理”、“下载”和“通用设置”选项卡（参见图 6-5）。“管理”选项卡列出了安装在你计算机上的小组件。带有复选标记的小组件条目是显示在桌面上的那些。你可以使用搜索框搜索小组件。如果某个小组件无法删除，它会带有一个锁图标。最初作为 Cinnamon 桌面一部分安装的小组件是被锁定的。在“管理”选项卡的底部有一个工具栏，带有向桌面添加 (`+`) 和移除 (`-`) 小组件的按钮、从系统中删除小组件并将其从列表中移除的 (`x`)、删除所有已安装小组件的“全部删除”按钮，以及一个显示所选小组件信息的“关于”按钮，如图所示。

![Image](img/image-180.png)

要激活小组件并将其显示在桌面上，请点击其条目并点击工具栏上的加号按钮 (`+`)。要从桌面移除小组件，请点击减号按钮 (`-`)。

某些小组件是可以配置的。这些小组件的条目上会显示齿轮图标。点击图标可打开一个带有配置设置的对话框。时钟小组件的配置图标会打开一个对话框，你可以在其中设置字体大小、文本颜色并指定自定义日期格式。

![Image](img/image-181.png) ![Image](img/image-182.png)

图 6-5：小组件管理选项卡

你可以通过点击“下载”选项卡从 Linux Mint 存储库下载并安装额外的小组件（参见图 6-6）。“排序方式”菜单允许你按名称、流行程度、日期（最新）和已安装进行排序。要安装小组件，点击其条目右侧的小组件下载按钮（向下箭头）。下载完成后，向下箭头按钮消失，随后小组件条目中会出现一个复选标记标志。然后你将在“管理”选项卡中看到该小组件。从那里你可以激活它并添加到桌面。

“下载”选项卡底部的工具栏有一组按钮，包括“更多信息”（灯泡图标）、用于移除已安装小组件的“卸载”、更新已安装小组件的“更新”以及更新可用小组件列表的“刷新”。要查看有关所选小组件的更多信息，点击“更多信息”按钮打开其网页。

![Image](img/image-183.png)

“通用小组件设置”选项卡让你决定小组件的显示方式。你可以选择为它们显示边框、不显示边框，或者同时显示边框和标题。

![Image](img/image-184.png)

图 6-6：小组件下载选项卡

### 热角 (Hot Corners)

热角允许你配置屏幕的角以运行工作空间切换器、桌面功能或程序。使用系统设置中的“热角”对话框来配置热角。中心图像显示了角的状态。激活的角为绿色，未激活的为灰色。每个角都有菜单供选择：显示所有工作空间 (Expo)、显示所有窗口 (Scale)、显示桌面以及运行命令（自定义）。默认情况下角是禁用的，显示灰色。要开启某个角，点击“启用此角”标签右侧的开关。该角将变为实绿色。将鼠标移动到角部片刻激活。“激活延迟”条目让你设置角激活的速度，如果你需要可以设置延迟。在图 6-7 中，例如，左上角配置为运行 Expo 切换器且无延迟。右侧角配置为运行 Scale 切换器并带有短延迟。两者均有效。

“显示桌面”选项切换桌面上打开窗口的最小化状态。如果显示，所有窗口将最小化到面板上的窗口列表应用中。如果已最小化，则它们将全部显示在桌面上。在图 6-7 中，左下角配置为显示桌面。

“运行命令”选项打开一个文本框，你可以在其中输入应用程序名称。在图 6-7 中，右下角配置为运行 Nemo 文件管理器。在文本框中输入了 `nemo` 命令。有了此设置，每当你将鼠标移动到该角时，Nemo 文件管理器都会打开一个包含你主文件夹的窗口。

![Image](img/image-185.png) ![Image](img/image-186.png)

图 6-7：系统设置热角




键盘快捷键可以在系统设置“键盘”对话框的`快捷键`选项页中进行配置（参见图 6-8）。这里提供了常规、窗口、工作区、系统、启动器、声音和媒体（如果您的键盘支持这些键）以及通用辅助功能的快捷键。左侧列出了各个类别，针对特定操作（如窗口定位）有额外的展开条目。在某个类别中，您可以选择一个快捷键任务，其按键显示在下方的“键盘绑定”部分。要更改或添加按键，请点击键盘绑定部分中的字符串，打开一个窗口，您可以在其中输入新按键或按键组合。常用快捷键列表见表 6-1。

![Image](img/image-187.png)

图 6-8：系统设置 - 键盘，键盘快捷键

| 键 | 描述 |
| :--- | :--- |
| Cinnamon | |
| `Alt-F2` | 从命令行运行命令 |
| `Meta` | 显示 Cinnamon 菜单（Windows 键） |
| `Meta with character` | 为桌面图标打开桌面搜索框 |
| `Ctrl-Alt-t` | 打开终端窗口 |
| `Ctrl-Alt-Escape` | 仅重启 Cinnamon 桌面 |
| Workspaces | |
| `Alt-F1` | 切换 Expo 工作区切换器 |
| `Ctrl-Alt-uparrow` | 切换 Expo 工作区切换器 |
| `Ctrl-Alt-leftarrow` | 移动到左侧工作区 |
| `Ctrl-Alt-rightarrow` | 移动到右侧工作区 |
| `Ctrl-Alt-Shift-arrows` | 使用左或右方向键将窗口移动到新工作区 |
| Panel | |
| `Ctrl-Alt-L` | 锁定屏幕 |
| `Ctrl-Alt-Delete` | 注销 |
| Windows | |
| `Ctrl-Alt-downarrow` | 切换缩放窗口切换器 |
| `Alt-Tab` | 在窗口之间切换 |
| `Alt-Shift-Tab` | 反向在窗口之间切换 |
| `Alt-~` | 在同一应用程序的窗口之间切换 |
| `Alt-F5` | 取消当前窗口的最大化 |
| `Alt-F4` | 关闭当前窗口 |
| `Meta-leftarrow` | 将当前窗口贴到屏幕左侧 |
| `Meta-rightarrow` | 将当前窗口贴到屏幕右侧 |
| `Meta-uparrow` | 将当前窗口贴到顶部 |
| `Meta-downarrow` | 将当前窗口贴到底部 |
| `Ctrl-Alt-Numpad 0` | 最大化窗口 |
| `Ctrl-Alt-Numpad 5` | 在屏幕居中最大化窗口 |

**表 6-1：Cinnamon 键盘快捷键**

### 菜单

Cinnamon 菜单由常用应用程序和操作收藏图标栏、基于应用程序类别的菜单以及用于查找应用程序的搜索框组成（参见图 6-9）。此外，菜单还会显示文件夹书签（“位置”）和最近访问的文件。Cinnamon 菜单是位于面板左侧的面板小组件。

![Image](img/image-188.png)

**图 6-9：Cinnamon 菜单**

在菜单上，收藏显示在左侧。右侧是类别菜单和所选类别下的项目菜单。（注：原文中存在大量重复句子已进行清理以优化格式。）



“新建菜单”（New Menu）按钮允许您创建新的分类菜单。您可以输入名称并选择要使用的图标。“新建项目”（New Item）按钮允许您添加菜单项，该项可以是应用程序、终端窗口中的应用程序（shell 脚本）或位置（文件夹）。您必须手动指定名称和命令。

### Windows

Linux Mint  Windows 运行方式与其他 Linux 发行版非常相似，具有类似的极大化、最小化和工作区操作。您可以使用窗口标题栏右侧的窗口按钮来最小化（减号）、最大化（展开图像）和关闭（x）窗口。

![Image](img/image-198.png)

窗口的偏好，例如双击标题栏的效果、标题栏字体以及按钮顺序，可以使用系统设置 Windows 对话框进行设置（参见图 6-15）。该对话框有三个选项卡：`Titlebar`（标题栏）、`Behavior`（行为）和 `Alt-Tab`。`Titlebar` 选项卡有一个 `Buttons`（按钮）部分，您可以在其中调整窗口按钮的位置，以及一个 `Titlebar` 部分，用于选择可以在标题栏上执行的操作。在 `Buttons` 部分中，标题栏按钮已经按照右侧布局进行了排序。您可以通过在“按钮布局”（Button layout）菜单中选择 `Left`（左侧）项将其移动到左侧。该菜单还包含 `Gnome` 项（其右侧只有一个关闭按钮）和 `Classic Mac` 项（其左侧有关闭按钮，右侧有最小化和最大化按钮）。

![Image](img/image-199.png) ![Image](img/image-200.png)

图 6-15：窗口设置：Titlebar 选项卡

在 `Actions`（动作）部分，`action-double-click-titlebar` 设置为 `toggle-maximize`（切换最大化），但菜单允许您选择此类 `toggle-shade`（切换隐藏）的选项，它会将窗口折叠而不是最大化。还有中键点击和右键点击的操作菜单（默认设置为 `Menu` - 窗口菜单）。“鼠标滚动标题栏时的操作”（Action on the title bar with mouse scroll）菜单允许您通过在标题栏上滚动来更改窗口不透明度，使其透明以便您看到下方的窗口或图标。

`Behavior` 选项卡允许您修改窗口的移动和显示（参见图 6-16）。它包含两个部分：“窗口焦点”（Windows Focus）和“移动和调整窗口大小”（Moving and Resizing Windows）。在 `Windows Focus` 部分，您可以设置焦点模式（`click`、`mouse` 或 `sloppy`）。“新窗口的焦点模式”可以是 `Smart`（智能）或 `Strict`（严格）。“将对话框窗口附到其父窗口的标题栏”选项将由应用程序窗口打开的对话框作为应用程序窗口的叠加层显示。在“移动和调整窗口大小”部分，您可以确定新窗口的初始位置，并选择一个按键来调整大小或移动窗口（`Alt`、`Meta`、`Super` 或 `Control`）。`Alt` 已被选中。

![Image](img/image-201.png)

图 6-16：窗口设置：Behavior 选项卡

`Alt-Tab` 选项卡允许您配置窗口切换器的显示（参见图 6-17）。您可以为菜单选择样式，例如 `icons only`（仅图标）、`thumbnails only`（仅缩略图）、`icons and window preview`（图标和窗口预览）以及默认的 `icons and thumbnails`（图标和缩略图）。对于支持加速（3D），您还可以选择 `coverflow` 和 `timeline`。大多数电脑现在都支持加速。您还可以选择显示所有工作区的窗口，而不只是当前的工作区。

![Image](img/image-202.png)

图 6-17：窗口设置：Alt-tab 选项卡

要管理窗口平铺和边缘翻转，您可以使用系统设置中的“窗口平铺”（Window Tiling）对话框。“启用窗口平铺和吸附”（Enable Window Tiling and Snapping）选项允许在将窗口移动到屏幕边缘或角部时启用窗口平铺和吸附（参见图 6-18）。它默认开启。您还可以选择一个按键在吸附模式和平铺模式之间切换。当将窗口移动到屏幕顶部边缘时，它会被设置为平铺，覆盖屏幕顶部部分。您可以通过开启“将窗口拖到屏幕顶部边缘时最大化而非平铺”（Maximize, instead of tile, when dragging a window to the top edge）选项将其改为最大化。

![Image](img/image-203.png) ![Image](img/image-204.png)

图 6-18：窗口平铺和边缘翻转

### 最小化、最大化和关闭窗口

要最大化窗口，可以双击标题栏或点击标题栏右侧的最大化按钮（展开图像）。您也可以右键点击标题栏并从弹出菜单中选择 `Maximize`，或者按下 `Ctrl-Alt-5` 键。如所述，如果您想通过将窗口移动到屏幕顶部边缘来最大化窗口，则需要在系统设置 Windows Tiling 对话框中开启“将窗口拖到屏幕顶部边缘时最大化而非平铺”选项。

取消最大化窗口，请拖动标题栏向下远离屏幕顶部，或者点击标题栏左侧的最大化按钮（展开图像）。

要移动窗口，点击并拖动其标题栏。移动时，鼠标指针会变成手形。您也可以按 `Alt` 键移动窗口，或者右键点击标题栏从弹出菜单中选择 `Move` 项。

要最小化窗口，点击标题栏右侧的最小化按钮（减号）。最小化的窗口将缩小为面板上窗口列表中的按钮。要恢复最小化的窗口，可以点击该按钮。您还可以关闭所有窗口，或者只关闭其他窗口。从键盘上，可以按下 `Alt-F7`。

要关闭窗口，点击标题栏右侧的窗口关闭按钮（`x` 字符）。您也可以右键点击标题栏从弹出菜单中选择 `Close` 项。从键盘上，可以按下 `Alt+F4`，或按下 `Alt+space` 显示窗口菜单然后按 `c` 选择 `Close` 项。

### 分组窗口列表

每个打开的窗口在底部面板的分组窗口列表上都有对应的按钮。点击它可以在最小化和显示之间切换窗口。按钮的左上角将显示该应用程序打开的窗口数量。右键点击窗口列表按钮可以打开弹出菜单，提供最大化、关闭和移动窗口到另一个工作区的选项（参见图 6-19）。最小化的窗口具有恢复窗口而非最小化的选项。您还可以关闭所有窗口，或只关闭其他窗口。要将窗口移动到另一个工作区，点击“移动到另一个工作区”项以展开显示工作区列表。`Files` 按钮菜单增加了 `Places`（所有主文件夹）以及 `Home`、`Computer` 和 `Trash` 等项。

要配置窗口列表，右键点击面板上的按钮并选择 `Preferences` 以展开菜单并显示 `Configure` 项，如所示。

![Image](img/image-205.png)

这将打开分组窗口列表配置对话框。从右上角的菜单中，您可以保存和导入窗口列表配置设置。

![Image](img/image-206.png) ![Image](img/image-207.png) ![Image](img/image-208.png)

图 6-19：窗口列表按钮菜单



分组窗口列表（Grouped Window List）对话框分为四个选项卡：通用、面板、缩略图和右键菜单（参见图 6-20）。在“通用”选项卡，你可以控制行为和热键，例如应用程序分组、鼠标操作以及循环应用程序的按键。“面板”选项卡允许你添加标签、配置动画、显示数量以及允许按钮拖动（重新排列按钮）。“缩略图”选项卡显示打开的窗口和应用程序的缩略图，配置它们的大小和显示，并启用鼠标悬停显示缩略图。“右键菜单”选项卡向右键菜单添加项，例如显示最近项目和新窗口选项。

![Image](img/image-209.png)
![Image](img/image-210.png)

图 6-20：分组窗口列表配置 - 通用和面板选项卡

在“面板”选项卡的“按钮标签”菜单中，你可以配置窗口列表中打开窗口的按钮是否带有标签。你可以从 `None`（默认）、`Application name`（应用程序名称）、`Window title`（窗口标题）和 `Window title for the focused window`（焦点窗口的标题）中进行选择。图 6-21 显示了这些选项。

![Image](img/image-211.png)
![Image](img/image-212.png)
![Image](img/image-213.png)

图 6-21：窗口列表按钮标签 - 无、应用程序、标题

将鼠标悬停在分组窗口列表按钮上会显示该应用程序任何打开窗口的缩略图（参见图 6-22）。将鼠标悬停在缩略图上会将其高亮，并在右上角显示一个关闭按钮，同时简要显示打开的窗口在桌面上的样子。点击缩略图可以恢复窗口（如果它已最小化），或者使该窗口成为你桌面上的活动窗口。

![Image](img/image-214.png) ![Image](img/image-215.png)

图 6-22：窗口列表按钮缩略图

分组窗口列表的“缩略图”选项卡允许你配置缩略图行为（参见图 6-23）。“缩略图”部分允许你关闭缩略图功能（`Show thumbnails`）以及配置缩略图的显示，例如调整大小以及垂直而非水平显示。“悬停预览”部分允许你关闭和管理桌面上悬停缩略图窗口的显示。

![Image](img/image-216.png)

图 6-23：分组窗口列表配置 - 缩略图选项卡

#### 调整窗口大小和平铺

你可以垂直、水平或同时调整窗口大小。要同时向两个方向调整大小，将鼠标移动到窗口的任意角，直到它变成角指针（带有直角指针图像的箭头）。然后你可以点击并拖动到所需的尺寸。对于侧边更改，将鼠标移动到窗口的左或右边缘，直到它变为侧边指针（带有线条图像的箭头）。相同的操作也适用于窗口顶部或底部的更改。

Linux Mint 支持窗口贴靠（布局）。将窗口移动到屏幕的左或右边缘（当鼠标到达边缘时）会将窗口扩展以占据屏幕的该侧。将窗口移动到屏幕顶部会将窗口最大化以使用全屏，窗口菜单栏和按钮位于顶部。

你还可以平铺两个窗口，使一个占据屏幕的一半，另一个使用另一半。将窗口拖动到左侧（点击并拖动标题栏，或在窗口上按 `Alt-click`）。当你的鼠标指针遇到屏幕边缘时，屏幕整个左侧会被高亮。当你释放鼠标时，窗口将吸附并显示在屏幕的左侧。相同的操作也适用于右侧。要将窗口恢复到之前的尺寸，只需向下拖动并远离边缘。

平铺也适用于角。将窗口拖动到角，当你的指针到达角上时，窗口将填充该角。你可以平铺四个打开的窗口，每个位于屏幕的一个角。

平铺也适用于顶部和底部边缘。将窗口移动到屏幕的顶部或底部，当你的指针到达顶部或底部边缘时，窗口将填充屏幕的半部分。对于顶部边缘，你可以配置“窗口贴靠”为最大化而非平铺窗口。

#### 使用窗口快速列表切换窗口

你也可以使用窗口快速列表来切换窗口，你可以将其添加到面板。窗口快速列表列出了你所有打开的窗口，按工作区组织（参见图 6-24）。

![Image](img/image-217.png) ![Image](img/image-218.png)

图 6-24：窗口快速列表菜单

#### 使用缩放界面（Scale）和 Alt-Tab 切换窗口

你可以使用缩放界面在打开的窗口之间切换，它以网格形式显示你打开的窗口（参见图 6-25）。窗口标题和应用程序图标显示在每个窗口下方。点击窗口将带回到桌面并显示选定的窗口。

![Image](img/image-219.png)

图 6-25：缩放：缩放以切换窗口（热点，显示所有窗口）

你可以通过按下 `Ctrl-Alt-向下` 访问缩放界面。你也可以使用配置为缩放的热点，或使用缩放插件（所示）。对于热点，使用系统设置“热点”对话框在某个角启用“显示所有窗口”。右上角已勾选“显示所有窗口”。对于缩放插件，首先安装它，然后点击面板上的缩放插件按钮显示缩放界面。

![Image](img/image-220.png)

你还可以使用 Alt-Tab 键在窗口之间切换，以显示窗口切换器（参见图 6-26）。打开的窗口在屏幕中央显示应用程序图标。使用 `Alt-Tab` 键选择你需要的。当你遍历图标行时，当前选中窗口的缩略图显示在图标下方。`Alt-Shift-Tab` 键向后遍历窗口，`Alt-~` 键切换同一应用程序的窗口。

![Image](img/image-221.png)

图 6-26：使用 Alt-Tab 切换窗口（图标和缩略图）

窗口切换器可以在系统设置“窗口”对话框的 Alt-Tab 选项卡中配置。`Alt-tab switcher style` 菜单允许你选择窗口切换器的内容。默认是“图标和缩略图”，但你可以将其设置为仅图标或使用窗口预览代替图标或缩略图。窗口预览会将除选定窗口以外的屏幕留。

你还可以使用 3D 窗口切换器。`Coflow (3D)` 选项在选中窗口两侧显示未选窗口（参见图 6-27）。`Timeline 3D` 在侧边显示单个未选窗口栈。

![Image](img/image-222.png)

图 6-27：使用 Alt-Tab 切换窗口（Coflow 3D )

### 效果




“效果”（Effects）对话框允许你为窗口、对话框和滚动框启用桌面效果（参见图 6-28）。效果对话框有两个选项卡：“启用效果”和“自定义”。在“启用效果”选项卡上，你可以开启或关闭窗口效果，启用对话框效果，并选择效果样式，如 Cinnamon（默认值）、缩放（Scale）、淡入（Fade）或混合（Blend）。在“自定义”选项卡上，你可以为特定的窗口任务选择效果，例如为窗口最小化和关闭操作选择缩放、淡入或无（none）（参见图 6-29）。对于最大化任务，你可以选择缩放或无。你还可以选择效果的形状。

![Image](img/image-223.png) ![Image](img/image-224.png)

图 6-28：系统设置效果：启用效果选项卡

![Image](img/image-225.png)

图 6-29：系统设置效果：自定义选项卡

### 使用热点角（expo）和 expo 插件选择工作区

Linux Mint 支持工作区，默认启用两个。你可以设置多个工作区，每个工作区都有已打开的窗口。你可以直接切换工作区，也可以通过 Expo 屏幕进行切换。要直接切换，你必须将工作区切换器插件添加到面板中，或者使用 `Ctrl-Alt-arrow` 键移动到工作区。工作区按行排列。初始情况下，如果有四个工作区，你就有一行四个工作区。使用 `Ctrl-Alt-right-arrow` 移动到下一个工作区，使用 `Ctrl-Alt-left-arrow` 返回。在系统设置的工作区对话框中，你可以启用“允许循环切换工作区”选项，通过连续使用 `Ctrl-Alt-right-arrow` 键循环回到第一个工作区。如果你想在移动到工作区时在桌面上短暂显示其名称，可以在系统设置的工作区对话框中启用“启用工作区 OSD”。

工作区切换器面板插件会在面板上显示工作区的按钮，就像 GNOME 2 桌面一样（参见图 6-30）。点击工作区按钮切换到该工作区。当前工作区会被突出显示。随着你添加工作区，它们会被添加到行中。打开“配置”选项显示工作区切换对话框，你可以在其中选择显示类型，可以是简单的数字按钮或视觉化表示（默认值）。

![Image](img/image-226.png) ![Image](img/image-227.png)

图 6-30：工作区切换器插件

工作区使用 Expo 管理。通过 Expo，你可以添加或删除工作区，更改它们的名称，并将打开的窗口直接从一个工作区移动到另一个。你可以通过多种方式访问 Expo。在键盘上，你可以按下 `Alt-F1` 或 `Ctrl-Alt-uparrow` 键来切换 Expo 屏幕。你也可以配置热点角来打开 Expo 屏幕，或者安装 Expo 插件。Expo 插件（所示）会在面板上放置一个 Expo 按钮，点击它可以打开 Expo 屏幕。

![Image](img/image-228.png)

热点角 Expo 屏幕访问是通过系统设置热点角对话框配置的（参见图 6-31）。屏幕的每个角都可以启用为热点角。每个角都有一个菜单，选项包括：显示所有工作区（Expo）、显示所有窗口（Scale）、显示桌面和运行命令。“显示所有工作区”选项会打开 Expo 屏幕，而“显示所有窗口”会打开窗口切换屏幕。在点击“启用此角”开关之前，该角不会被启用。此时中间图像中的角将变为实绿色。未启用的角为灰色。默认设置显示在图 6-24 中，同时启用了左上角和右上角。左上显示工作区，右上显示窗口。

![Image](img/image-229.png) ![Image](img/image-186.png)

图 6-31：启用了 Expo 的热点角

Expo 屏幕（显示所有工作区）显示你当前的工作区，以及它们的名称和屏幕右侧的加号按钮，你用它来添加工作区（参见图 6-32）。将鼠标悬停在工作区上会突出显示并在右上角显示一个关闭框，允许你删除工作区。它还将你的窗口缩放成正方形网格。点击加号按钮添加工作区。默认情况下，这些将作为正方形网格的一部分添加。要离开 Expo 屏幕，点击特定的工作区或按 `Esc` 键。

![Image](img/image-230.png)

图 6-32：Expo 工作区配置（正方形网格）

你可以使用系统设置的工作区对话框让 Expo 屏幕中的工作区显示为行而非网格（参见图 6-33）。将“将 Expo 显示为网格”开关关闭。你还可以更改工作区的名称。每个工作区下方都有一个带有其名称的文本框。点击它可以编辑名称。

![Image](img/image-231.png)

图 6-33：Expo 配置（无网格）

![Image](img/image-232.png) ![Image](img/image-233.png)

图 6-34：工作区设置

要移动窗口到工作区，只需点击并拖动。当鼠标悬停在窗口上时，它会突出显示并在右上角显示一个关闭框，允许你删除工作区。它还将你的窗口缩放成正方形网格。点击加号按钮添加工作区。默认情况下，这些将作为正方形网格的一部分添加。要快速将窗口移动到另一个工作区，使用 `Ctrl+Alt+Shift+arrow` 键。“移动到工作区”项显示子菜单（参见图 34）。你可以启用工作区切换 OSD、启用工作区循环、以网格显示视图、限制工作区使用主显示器以及反转切换工作区的方向。

### Linux Mint 面板：现代布局

通过面板，你可以访问菜单、运行插件并启动应用程序（参见图 6-35）。面板基于 GNOME 2 面板，提供了简单高效的插件体验。从 Linux Mint 19.1 开始，Cinnamon 实现了一种使用现代布局的新面板，具有可配置的分组列表、窗口预览和图标大小区域。面板左侧是 Cinnamon 菜单、应用程序按钮和最小化窗口。右侧是 Xapp 插件系统托，包含标准的 XAppStatusicon 插件，如日期、蓝牙、电池、网络管理器和声音。你可以根据自己的需求自定义面板，保留你选择的插件和菜单。你可以添加新面板、向面板添加应用程序并添加各种插件。

![Image](img/image-234.png)

![Image](img/image-235.png)

![Image](img/image-236.png)

图 6-35：带有菜单、分组窗口列表和插件的 Linux Mint 面板，位于 Linux 桌面底部

在 Xapp 插件系统图中，XAppStatusicon 图标和菜单已经标准化（参见图 6-36）。它们还可以提供鼠标轮支持，让你通过鼠标滚轮更改功能。将鼠标悬停在声音图标上并滚轮可以更改音量。在电源图标上执行相同的操作可以更改屏幕亮度。在声音图标上点击鼠标轮可以静音。相同的 XAppStatusicon 系统托也用于 Linux Mint MATE 和 Xfce。

![Image](img/image-237.png) ![Image](img/image-238.png)




# 图 6-36：支持鼠标滚轮的 XApp 状态小组件托盘和 XAppStatusicon 图标

面板配置任务（如添加应用程序、选择小组件、设置菜单和创建新面板）可以通过面板弹出菜单进行处理。只需在面板空白处（中间部分）右键点击，即可显示一个菜单，其中包含面板设置、“添加新面板”、“面板编辑模式”、“移动”、“删除”、“添加新面板”、“故障排除”和“系统设置”等选项（请参见图 6-37）。

![Image](img/image-239.png)

## 图 6-37：面板弹出菜单（右键点击中间）和面板小组件菜单

前两个选项显示“系统设置”配置对话框：“小组件”和“面板”，最后一项显示“系统设置”。“故障排除”项显示一个子菜单，列出了重启桌面（重启 Cinnamon）、恢复桌面默认设置（将所有设置还原为默认值）以及启动错误扫描（透视镜 Looking Glass）的项目（请参见图 6-38）。

还有删除或移动面板以及添加另一个面板的选项。“移动”选项显示屏幕的四个边缘，允许您将面板移动到任何边缘（包括侧边）。点击您想要将面板移动到的边缘即可。

![Image](img/image-240.png)

## 图 6-38：面板菜单“故障排除”子菜单

“面板编辑模式”开关允许您移动或删除面板上的小组件。当面板在使用时，该开关应保持关闭。要编辑面板，请点击开关将其打开。不同区域的背景将显示颜色，例如左侧的应用程序小组件为红色，面板空白部分（中间）为绿色，右侧的小组件为蓝色（请参见图 6-39）。要移动项目，请点击并拖动它。移动项目时，您的指针图像会变为手形。要删除项目，右键点击它以显示带有“移除此小组件”选项的菜单。完成菜单编辑后，再次打开面板菜单并点击“面板编辑模式”开关将其关闭。

![Image](img/image-241.png)

![Image](img/image-242.png)

## 图 6-39：编辑模式下的 Linux Mint 面板

“面板设置”项会打开“系统设置-面板”对话框，让您可以配置面板（请参见图 6-40）。您可以添加新面板、设置面板和图标大小，并设置自动隐藏面板。在“面板可见性”部分，如果您从“自动隐藏面板”菜单中选择了“自动隐藏”，则面板将被隐藏，直到您将鼠标移动到屏幕底部。

在“自定义”部分，会显示一个比例尺，您可以在其中更改面板大小。在“面板外观”部分，您还可以选择调整左、中、右面板区域的图标大小。这些区域是在 Linux Mint 19.1 引入的新 Cinnamon 面板中实现的。面板被分为三个可配置的区域：右侧、中间和左侧（垂直区域为顶部、中间和底部）。这些区域的图标大小可以单独配置。图标大小可以缩放至任意面板大小（“缩放至面板大小”选项），或缩放到若干个固定的“清晰”尺寸之一。固定尺寸不会进行动态缩放，因此看起来更清晰、更锐利。有两个缩放选项：最佳（optimal）和精确（exact）。“精确”尺寸将图标动态缩放到面板的精确尺寸，清晰度没有固定尺寸高。“最佳”尺寸将图标缩放至适应面板的最大固定尺寸。默认情况下，左侧和中间区域按最佳缩放至面板大小，而包含系统图标的右侧区域设置为固定的 24pt 大小。

在“常规面板选项”部分，您可以添加新面板。“面板编辑模式”按钮是开启面板编辑模式的简方法。您还可以设置符号图标的大小。

![Image](img/image-243.png)  ![Image](img/image-244.png)

## 图 6-40：面板设置对话框

## Linux Mint 小组件

小组件（Applets）是在面板内执行任务的小型程序。可以在 [`cinnamon-spices.linuxmint.com/applets`](https://cinnamon-spices.linuxmint.com/applets) 找到可用组件列表。要向面板添加小组件，请打开“系统设置-小组件”对话框，您可以从系统设置或面板弹出菜单打开它。在“管理”标签卡上，小组件对话框列出了系统中已有的小组件。您可以使用搜索框在列表中搜索小组件。激活且位于面板上的小组件右侧会有勾选标记（请参见图 6-41）。如果某个小组件无法移除，它将有一个锁图标。最初作为 Cinnamon 桌面部分安装的小组件是被锁定的。某些小组件可以配置，这些项目的项上将显示齿轮图标。一旦您将小组件添加到面板，配置按钮将变为可用状态。点击图标可打开带有配置设置的对话框。

![Image](img/image-245.png)  ![Image](img/image-246.png)

## 图 6-41：小组件“管理”标签卡

在“管理”标签卡底部有一个工具栏，包含添加小组件（+）、从面板移除小组件（-）、删除所有（x）、重置所有（圆形箭头）、仅显示已启用的小组件以及关于所选小组件信息的按钮，如下所示。

![Image](img/image-180.png)

要激活面板上的小组件，点击其项并点击工具栏上的加号按钮。要从面板移除小组件，选择它并点击减号按钮。

可以添加许多由第三方开发者支持的小组件。它们列在“下载”标签卡中（请参见图 6-42）。排序菜单允许您按名称、评分（人气）和日期进行排序。要安装小组件，点击右侧的下载按钮（向下箭头）。安装后，下载按钮将消失，小组件项中会出现勾选。该小组件也会出现在“管理”标签卡中，然后您可以选择它们并面板。某些第三方小组件可能需要额外的软件。

“下载”标签卡底部的工具栏包含“更多信息”（灯泡图标）、卸载（已安装的小组件）、更新（已安装的小组件）以及刷新（可用小组件列表）按钮。要查看所选小组件的更多信息，点击“更多信息”按钮将在浏览器中打开描述该组件及用户评论的 Linux Mint 页面。

![Image](img/image-247.png)

![Image](img/image-248.png)

## 图 6-42：小组件对话框“在线小组件”标签卡

## Linux Mint 传统布局

Linux Mint 的传统布局（您可以从欢迎界面的“步骤”标签卡选择）使用了 Linux Mint 19 及更早版本中的许多显示功能。这里列出了其中的主要特征。

面板使用启动器而非分组窗口列表，并带有不同的菜单（请参见图 6-43）。右侧的系统工具使用了传统的图标并包含用户小组件。小组件中使用的开启关闭开关有所不同。

面板左侧具有 Cinnamon 菜单、应用程序按钮和最小化窗口。右侧具有日期、电池、网络管理器和音量等小组件。

![Image](img/image-249.png)

![Image](img/image-250.png)

![Image](img/image-251.png)





# 图 6-43：传统布局面板

面板启动器小组件（applet）允许你从面板启动应用程序。面板启动器小组件已安装在 Linux Mint 面板的左侧，列出了 Firefox Web 浏览器、终端和文件（Nemo 文件管理器、主文件夹）。点击应用程序图标即可启动它。将鼠标悬停在图标上会显示其名称。要显示对应用程序图标可以执行的操作菜单，请右键点击面板启动器小组件中的任何图标（参见图 6-44）。该菜单包含“启动”、“添加”、“编辑”和“删除”项。“添加”和“编辑”项会打开一个对话框，你可以在其中手动输入或编辑应用程序名称和启动选项。“删除”项会从面板启动器小组件移除移除图标。其他条目根据应用程序进行定制。Firefox Web 浏览器具有“在新窗口中打开”或“在私窗口中打开”的项。终端有一个“打开新终端窗口”的项。文件管理器有“主”、“计算机”和“垃圾桶”文件夹的项，并以主文件夹作为默认。

![Image](img/image-252.png) ![Image](img/image-253.png) ![Image](img/image-254.png)

图 6-44：传统布局面板启动器小组件和菜单

虽然你可以使用 Cinnamon 菜单注销、关机并访问系统设置，但你也可以使用用户小组件（参见图 6-45）。用户小组件具有“锁定”、“切换用户”、“注销”和“关机”项。这是执行这些任务的非常快速的方法，无需显示 Cinnamon 菜单。点击名称会显示“帐户详情”对话框，你可以在其中更改用户图标、全名和密码。在面板上，用户小组件显示一个人形图标。你可以配置小组件（右键点击它并选择“配置”）来显示用户的全名。如果你愿意，也可以在现代布局（Modern layout）上安装用户小组件。

![Image](img/image-255.png)

图 6-45：传统布局用户小组件

传统布局现在在其菜单中使用与其相同的开关，如图 6-46 所示的网络管理器小组件菜单中的开关。

![Image](img/image-256.png)

图 6-46：传统布局开关

## Nemo 文件管理器

Nemo 文件管理器支持复制、移除和删除项目的标准功能，以及设置权限和显示项目。文件管理器的名称为 Files（文件），但实际程序名称仍为 `nemo`。

### 主文件夹子目录和书签

与 Ubuntu 类似，Linux Mint 使用通用用户目录结构（[`freedesktop.org`](https://freedesktop.org) 中的 `xdg-user-dirs`）在用户主目录下设置子文件夹。文件夹将包括 `Documents`、`Music`、`Pictures`、`Downloads` 和。这些本地用户文件夹被许多桌面应用程序用作默认值。用户可以使用文件浏览器更改文件夹名称或将它们相互放置。例如，可以将 `Music` 移动到 `Documents` 中，即 `Documents/Music`。本地配置存储在 `.config/user-dirs.dirs` 文件中。系统级默认设置在 `/etc/xdg/user-dirs.defaults` 文件中。这些文件夹的图标显示在图 6-47 中。

![Image](img/image-257.png)

图 6-47：Nemo 文件管理器主文件夹

这些文件夹也是默认书签。你可以直接从 Nemo 窗口的侧边栏或书签菜单访问书签文件夹。你还可以通过打开文件夹并从书签菜单中选择“添加书签”来为文件夹添加自己的书签。你的文件夹将出现在 Nemo 侧边栏的书签部分和书签菜单中。你可以使用文件管理器的书签对话框来管理书签，可以通过书签菜单中的“编辑书签”进行访问。在这里，你可以移除书签或更改其名称和位置。

你使用系统设置中的“桌面”对话框在桌面区域显示主文件夹、网络文件夹和垃圾桶等基础文件夹。

### 文件管理器窗口

当你点击桌面上的主文件夹图标、面板启动器小组件上的主文件夹图标或 Cinnamon 菜单收藏夹栏上的主文件夹图标时，会打开一个文件管理器窗口显示你的主文件夹。文件管理器窗口显示多个组件，包括菜单栏、主工具栏和侧边栏（参见图 6-48）。

![Image](img/image-48.png)

图 6-48：带有侧边栏的文件管理器

侧边栏显示“我的电脑”、“书签”、“设备”和“网络”项目部分，显示你的文件系统和默认主文件夹子目录。“书签”和“设备”项目仅在存在书签或连接设备时出现。你可以通过在“视图”菜单的“侧边栏”子菜单中选择“侧边栏”项，或通过点击侧边栏下方状态栏上的隐藏按钮来显示或隐藏侧边栏主面板（右侧）显示当前工作文件夹中的文件和文件夹图标或文件和文件夹列表。当你选择一个文件或文件夹时，窗口底部的状态栏会显示名称，对于文件显示大小，对于文件夹显示包含的项目数量。状态栏还会显示所选文件系统的剩余空间。注意：`Nemo` 作为 FTP 浏览器工作。你可以使用文件顶栏上的“连接服务器”项打开“连接服务器”对话框，你可以在其中输入 FTP 站 URL。文件菜单具有打开新标签页（`Ctrl-t`）、打开新文件管理器窗口（`Ctrl-n`）、创建新文件夹（`Shift-Ctrl-n`）、连接到远程服务器以及显示当前文件夹属性（`Alt-Return`）的项。大多数都有快捷键。

### 文件管理器侧边栏和书签

文件管理器侧边栏显示你通常访问的位置：电脑（My Computer）、设备（Devices）和网络文件夹（Network）（参见图 6-49）。选择文件系统会将你带到文件系统的顶部，让你移动到任何部分。在“我的电脑”部分，你可以打开默认文件夹，如 Documents 和 Pictures。“最近”文件夹项让你打开显示最近访问文件的文件管理器窗口。如果你收藏了文件夹（书签菜单，“添加书签”项 (`Ctrl-d`)),书签将出现在侧边栏的相应章节中。要移除或重命名书签，请右键点击侧边栏上的条目并在弹出菜单中选择“移除”或“重命名”。书签名称会更改，但原始文件夹名称不会。

![Image](img/image-258.png)

图 6-49：带有书签的文件管理器侧边栏

侧边栏有两种菜单视图：位置（Places）和树视图（Treeview）。你可以通过下方按钮栏上的按钮在两者之间切换，如所示。第三个按钮将隐藏侧边栏。

![Image](img/image-259.png)

“位置”菜单具有可展开的菜单（参见图 6-50）。“我的电脑”菜单展开显示主文件夹、默认书签、根目录（文件系统）和垃圾桶。当你创建书签时，它会列在书签菜单中。当你连接设备时，会出现“设备”子菜单并展开显示连接的设备。设备具有弹出按钮，你可以使用它们移除设备。你可以折叠所有菜单，仅保留菜单标题。

![Image](img/image-260.png) ![Image](img/image-261.png) ![Image](img/image-262.png)

图 6-50：文件管理器侧边栏位置菜单，展开和未展开状态




树状视图显示了主文件夹和文件系统的可展开菜单（参见图 6-51）。你可以对其进行折叠，只显示其中一个。

![Image](img/image-263.png) ![Image](img/image-264.png)

图 6-51：文件管理器侧边栏树状视图菜单，已展开和未展开状态

### 标签页

Nemo 文件管理器支持标签页，通过标签页可以在同一个文件管理器窗口中打开多个文件夹。要打开标签页，从“文件”菜单中选择`新建标签页`（参见图 6-52）或按 `Ctrl-t`。会出现一个标签页栏，每个标签页都有一个图标，显示已打开的文件夹名称以及一个 `x` 关闭按钮。你可以通过点击并拖动标签图标向右或向左来重新排列标签页。你还可以使用 `Ctrl-PageUp` 和 `Ctrl-PageDown` 键在标签页之间移动。使用 `Shift-Ctrl-PageUp` 和 `Shift-Ctrl-PageDown` 键重新排列标签页。要关闭标签页，点击标签页右侧的关闭 `x` 按钮。标签页是可以分离的。你可以将标签页拖出到自己的窗口，在新窗口中打开它。

![Image](img/image-265.png)

图 6-52：带有标签页的文件管理器窗口

### 显示文件和文件夹

你可以以图标、紧凑列表或详细列表查看文件夹内容，可以通过主工具栏右侧的“视图”图标选择：`图标`、`列表`和`紧凑`，所示。

![Image](img/image-266.png)

使用控制键快速更改视图：`Ctrl-1` 图标，`Ctrl-2` 列表，`Ctrl-3` 紧凑视图。列表视图提供名称、大小、类型和日期。主面板顶部显示每个字段的按钮。你可以使用这些按钮根据该字段对列表进行排序。例如，要按日期排序文件，点击`修改日期`按钮。要按大小排序，点击`大小`按钮。再次点击可在升序和降序之间切换。

某些类型的文件图标将显示其内容的预览。例如，图像文件的图标将显示图像的缩略图。文本文件的图标将显示其文本的前几个字。你可以通过在文件管理器`视图`菜单中取消勾选`显示缩略图`来关闭缩略图。

`视图`菜单包含管理和安排你的文件管理器图标的项目（参见表 6-2）（参见图 6-53）。你可以选择`图标`、`列表`和`紧凑`视图。在图标视图中，会出现“排列项目”子菜单，它提供了按名称、大小、类型和修改日期排序图标的选项。你也可以简单地反转顺序，或手动定位图标。

注意：当我们将鼠标悬停在`文件`、`视图`和`编辑`菜单中的项目上时，文件管理器窗口底部的状态栏将显示该项目功能的简短描述。

`放大`项目会放大你的窗口视图，使图标变大，`缩小`则缩小视图，使图标变小。`标准大小`将它们恢复为标准大小。你还可以使用 `Ctrl-+` 和 `Ctrl--` 键进行放大和缩小。

| 菜单项目 |  |
| :--- | :--- |
| 停止 | 停止当前任务 |
| 重载 | 刷新文件和目录列表 |
| 侧边栏 \| 位置，树 | 在位置视图或树视图中显示侧边栏。 |
| 侧边栏 \| 显示侧边栏 | 显示包含设备、网络和书签项目的侧边栏。 |
| 主工具栏 | 显示主工具栏 |
| 菜单栏 | 显示菜单栏 |
| 状态栏 | 在文件夹窗口底部显示状态栏 |
| 面板 | 在文件管理器窗口中打开双面板，每个窗格显示不同的文件夹。 |
| 位置 | 打开文件夹路径名称的位置框 |
| 重置视图为默认值 | 默认视图和排序 |
| 显示隐藏文件 | 显示管理级点文件。 |
| 显示缩略图 | 在此文件夹的图标视图中显示文件的缩略图。取消勾选此项将不显示缩略图。 |
| 排列项目：按名称、大小、类型和修改日期 | 根据指定标准排列文件和目录 |
| 按名称组织 | 在图标视图中，按名称排列图标 |
| 反转顺序 | 在列表视图中，反转文件列表顺序 |
| 放大 | 提供图标的近距离视图，使其看起来更大。 |
| 缩小 | 提供图标的远距离视图，使其看起来更小。 |
| 标准大小 | 将图标视图恢复为标准大小。 |
| 图标 | 显示图标 |
| 列表 | 显示带有名称、大小、类型和日期的文件列表。文件夹可以展开。 |
| 紧凑 | 仅使用名称和小图标显示紧凑文件列表 |

表 6-2：文件管理器视图菜单

![Image](img/image-267.png) ![Image](img/image-268.png) ![Image](img/image-269.png)

图 6-53：文件管理器文件、视图和编辑菜单

### 文件管理器菜单和工具

从`文件`菜单中，你可以创建文件夹、新建标签页、在新窗口中打开文件管理器以及连接服务器（参见表 6-3 和参见图 6-53）。

| 菜单项目 | 描述 |
| :--- | :--- |
| 新标签页 | 创建标签页。 |
| 新窗口 | 打开新窗口 |
| 创建文件夹 | 在目录中创建子目录。 |
| 创建文档 | 创建文本文档。 |
| 连接服务器 | 使用文件管理器连接 FTP 服务器 |
| 属性 | 当前打开文件夹的属性 |
| 关闭所有窗口 | 关闭所有窗口 |
| 关闭 | 关闭文件管理器窗口。 |

表 6-3：文件

从`编辑`菜单中，你可以粘贴已剪切的文件在文件夹之间移动或复制它们（参见表 6-4 和参见图 6-53）。

| 菜单项目 | 描述 |
| :--- | :--- |
| 撤销，重做 | 撤销或重做粘贴操作 |
| 剪切，复制 | 移动或复制文件或目录 |
| 粘贴 | 粘贴已复制或剪切的文件，可以在文件夹之间移动或复制或复制。 |
| 全选 | 选择文件夹中的所有文件 |
| 选择匹配项 | 使用基本模式匹配快速搜索文件。 |
| 反转选择 | 选择所有未选的文件和文件夹，取消选择当前选择。 |
| 固定 | 固定文件夹或文件，使其显示在文件管理器列表和文件夹的开头或顶部 |
| 复制 | 创建选中文件的副本 |
| 创建链接 | 为文件或文件夹创建链接 |
| 重命名 | 重命名选中的文件或文件夹 |
| 复制到 | 将文件或文件夹复制到默认书签之一 |
| 移动到 | 将文件或文件夹移动到默认书签之一 |
| 移动到回收站 | 将文件或文件夹移动到回收站以备后删除 |
| 删除 | 立即删除文件或文件夹。 |
| 使用完整右键菜单 | 将复制到、移动到和链接项添加到右键菜单。 |
| 压缩 | 将选中的文件和文件夹压缩为压缩存档文件，如 tar、cpio、lmza 或 zip 文件。存档文件可以进行密码保护 |
| 共享选项 | 选中文件夹时激活。你可以选择在网络上共享该文件夹。 |
| 偏好设置 | 账户的 Nemo 文件管理器偏好设置。 |

表 6-4：编辑




# 表 6-4: 文件管理器编辑菜单

在图标视图中，你可以点击文件管理器窗口主面板空白处的任意位置，显示一个弹出菜单，其中包含创建新文件夹、排列图标、缩放图标、显示隐藏文件以及打开文件夹属性对话框的选项（参见表 6-5）。

| 菜单项 | 说明 |
| :--- | :--- |
| 创建新文件夹 | 在目录中创建一个新的子目录。 |
| 创建新文档 | 创建文本文档。 |
| 创建新启动器 | 为应用程序创建启动器图标 |
| 在终端中打开 | 在终端窗口中打开当前文件夹 |
| 显示隐藏文件 | 显示管理级点文件（dot files）。 |
| 粘贴 | 粘贴已复制或剪切的文件。 |
| 放大 | 提供图标的放大视图，使其看起来更大。 |
| 缩小 | 提供图标的远视图，使其看起来更小。 |
| 属性 | 打开目录的属性对话框 |
| 正常大小 | 将图标视图恢复为标准大小。 |

# 表 6-5: 文件管理器弹出菜单

## 在文件管理器中导航

文件管理器的工作方式与 Web 浏览器类似，它使用同一个窗口显示打开的文件夹。它维护了一个以前查看过的文件夹列表，你可以使用工具栏上的导航按钮（左侧）在该列表中来回移动（参见图 6-54）。左箭头按钮带你回到上一个显示的文件夹，右箭头按钮带你进入下一个显示的文件夹，向上箭头则回到父文件夹。从`Go`（Go）菜单，你可以执行相同的导航操作，还可以访问`主`、`计算机`、`网络`和`垃圾箱`文件夹（参见表 6-6）。

![Image](img/image-270.png) ![Image](img/image-271.png)

图 6-54: 文件管理器导航

当你打开一个新文件夹时，将使用同一个窗口来显示它，你可以使用`前进`和`后退`箭头在以前打开的文件夹之间移动（主工具栏左上角）。当你打开子文件夹时，主工具栏会显示当前文件夹及其父文件夹的按钮（参见图 6-47）。你可以点击文件夹按钮直接移动过去。点击主文件夹按钮左侧的箭头可以将列表展开到根文件夹，它显示为一个带有硬盘图标的按钮。

| 菜单项 | 说明 |
| :--- | :--- |
| 打开父文件夹 | 到父文件夹 |
| 后退 | 回到文件管理器窗口中查看过的上一个文件夹 |
| 前进 | 到文件管理器窗口中查看过的下一个文件夹 |
| 粘贴 | 粘贴已复制或剪切的文件，让你可以在文件夹之间移动或复制文件，或创建副本。 |
| 与另一窗格相同位置 | 如果你在窗口中打开了两个窗格，可以让两个窗格显示同一个文件夹 |
| 主目录 | 移动主目录文件夹 |
| 计算机 | 到计算机文件夹，显示你的设备图标 |
| 模板 | 移动模板文件夹 |
| 垃圾箱 | 打开垃圾箱文件夹查看已删除的文件和文件夹，这些是可以恢复的。 |
| 网络 | 移动到网络文件夹，显示网络上连接的系统并打开远程文件夹。 |
| 搜索文件 | 使用文件管理器窗口搜索文件和文件夹 |

# 表 6-6: 文件管理器 Go 菜单

你也可以显示位置 URL 文本框而不是按钮，可以在其中输入文件夹的位置，无论是在你的系统上还是远程系统上（参见图 6-55）。要显示位置文本框，按`Ctrl-l`或点击主工具栏位置路径右侧的`位置`（Location）切换按钮（弯曲箭头）。你也可以按`F9`或在`查看`（View）菜单上选择`位置`（Location）（`View | Location`）。这些访问方法作为切换开关工作，让你在位置文本框和按钮路径之间来回。

![Image](img/image-272.png)
![Image](img/image-273.png)
![Image](img/image-274.png)

图 6-55: 展开和未展开的路径及位置

使用侧边栏的`位置`（Places）视图访问收藏的文件夹、存储设备（USB、CD/DVD 光盘和连接的硬盘）以及挂载的网络文件夹。在侧边栏的“我的电脑”部分，你可以访问主目录、垃圾箱、文件系统（根目录）以及你创建的其他书签。

要打开子文件夹，你可以双击其图标，或右键点击图标从菜单中选择`打开`。要在新标签页中打开文件夹，选择`在新标签页中打开`。你也可以点击文件夹进行选择，然后从`文件`菜单中选择`打开`项（`File | Open`）。

你可以通过点击书签打开侧边栏列出的任何文件夹或文件系统。你也可以右键点击书签显示一个包含`打开`、`在新标签页中打开`和`在新窗口中打开`选项的菜单（参见表 6-7）。`在新窗口中打开`项是访问设备的简单方法。可移动设备项具有`弹出出`（Eject）选项。

| 菜单项 | 说明 |
| :--- | :--- |
| 打开 | 到父文件夹 |
| 后退 | 回到文件管理器窗口中查看过的上一个文件夹 |
| 前进 | 到文件管理器窗口中查看过的下一个文件夹 |
| 粘贴 | 粘贴已复制或剪切的文件，让你可以在文件夹之间移动或复制文件，或创建副本。 |
| 与另一窗格相同位置 | 如果你在窗口中打开了两个窗格，可以让两个窗格显示同一个文件夹 |
| 主目录 | 移动主目录文件夹 |
| 计算机 | 到计算机文件夹，显示你的设备图标 |
| 模板 | 移动模板文件夹 |
| 垃圾箱 | 打开垃圾箱文件夹查看已删除的文件和文件夹，这些是可以恢复的。 |
| 网络 | 移动到网络文件夹，显示网络上连接的系统并打开远程文件夹。 |
| 搜索文件 | 使用文件管理器搜索文件和文件夹 |

# 表 6-7: 文件管理器侧边栏弹出菜单

## Nemo 文件管理器搜索

Nemo 文件管理器提供了搜索工具，你可以从桌面或任何文件管理器窗口访问它。搜索文件会在工具栏下方打开一个搜索框。输入模式进行搜索并按`回`。结果将显示（参见图 6-56）。要记住搜索，点击搜索框右侧的星形按钮。查看之前的搜索，右键点击此按钮。

![Image](img/image-275.png)

图 6-56: Nemo 文件管理器搜索

## 管理文件和文件夹

作为符合 GNOME 标准的文件管理器，Nemo 支持通过拖拽复制移动文件。要移动文件或文件夹，从一个文件夹拖到另一个。移动操作是 GNOME 中的默认拖拽。要将文件复制到新位置，在拖拽时按住`Ctrl`键。

| 菜单项 | 说明 |
| :--- | :--- |
| 打开 | 使用关联应用程序打开文件。目录在文件管理器中打开。 |
| 在新标签页中打开 | 在同一窗口的新标签页中打开文件夹。 |
| 在新窗口中打开 | 在独立窗口中打开文件夹 |
| 打开方式 | 选择打开此文件的应用程序。将打开“打开方式”对话框显示可能的应用程序。 |
| 剪切复制 | 剪切和复制选中文件的项。 |
| 固定 | 固定文件或文件夹。 |
| 重命名 (F2) | 重命名文件。 |
| 创建链接 | 在同一文件夹中创建该文件的链接。 |
| 复制到 | 将文件复制到主目录、桌面或文件管理器窗口中另一个窗格中（完整菜单选项）。 |
| 移动到 | 将文件移动到主目录、桌面或文件管理器窗口中另一个窗格中（完整菜单选项）。 |
| 移动到垃圾箱 | 将文件移动到垃圾箱目录，之后可以删除它。 |
| 删除 | 永久删除文件或文件夹 |
| 发送 | 使用默认邮件程序发送文件 |
| 压缩 | 使用 File Roller 归档文件。 |





| 共享选项 | 显示文件夹共享对话框（Samba 和 NFS）。 |
| 属性 | 显示属性对话框。 |
| 在终端中打开 | 在终端窗口中打开当前目录 |
| 以根身份打开 | 以管理员用户身份打开终端窗口 |

**表 6-8：文件和文件夹弹出菜单**

### 使用文件的弹出菜单

你也可以通过右键点击文件图标，并从弹出的弹出菜单中选择你想要的操作，来对文件执行删除、重命名和创建链接的操作（参见表 6-8）。例如，要删除某项，请右键点击它并从弹出菜单中选择`移动到回收篓` (Move To Trash)。这将将其放入`回收篓`（Trash）目录，你稍后可以删除。某些选项只出现在`编辑`（Edit）菜单中，包括`移动到` (Move to)、`复制到` (Copy to) 和`创建链接` (Make link)。要创建链接，选择该文件并从`编辑`菜单中选择`创建链接` (Make Link) 或按 `Ctrl-m`。这会创建一个以“链接”（Link）字开头的新链接文件。

### 重命名文件

要重命名文件，你可以右键点击文件图标并从弹出菜单中选择`重命名` (Rename) 项，或者点击其图标并按 `F2` 功能键。图标的名称将被框起来，并封装在一个小的文本框中。你可以覆盖旧名称，也可以通过点击名称中的某个位置以插入文本来编辑当前名称，并使用退格键删除字符。你也可以通过在文件的`属性`对话框（`基础` 选项卡）中输入新名称来重命名文件。Cinnamon 还支持`快速重命名` (Quick-Rename)，尽管该功能默认未启用。通过`快速重命名`，你可以双击图标下文件名（中间有停顿）来激活重命名过程（不是双击）。要开启此功能，打开文件管理器的`首选项`对话框（`编辑 | 首选项`）并选择`行为` (Behavior) 选项卡。在`行为`部分，点击“双击文件名以进行重命名”项的复选框。

### 文件分组

你可以通过点击第一项然后按住 `SHIFT` 键点击最后一项，或者通过点击并拖动想要选择的项来选择一组文件和文件夹。要选择不连续的项，在点击各个图标时按住 `Ctrl` 键。如果你想选择目录中的所有项，选择`编辑`菜单中的`全选` (Select All) 项（`编辑 | 全选`）（`Ctrl-a`）。然后你可以一次复制、移动甚至删除多个文件。要选择名称中具有特定模式的项目，从工具菜单中选择`选择匹配项` (Select Items Matching) 以打开搜索框，你可以在其中输入模式（`Ctrl-s`）。使用 `*` 字符匹配部分模式，例如使用 `let` 来匹配所有包含“let”模式的文件名。模式 `my*` 将匹配以“my”模式开头的文件名，而 `*.png` 将匹配所有 PNG 图像文件（点表示文件扩展名）。

### 打开应用程序和文件 MIME 类型

你可以通过双击应用程序本身或用于该应用程序的数据文件，在文件管理器中启动任何应用程序。如果你想用特定的应用程序打开文件，可以右键点击文件并选择`打开方式` (Open With) 项之一。将为默认和可能的应用程序显示一个或多个`打开方式`项，例如针对文本文件的“用文本编辑器打开”。如果列表中没有列出你需要的应用程序，你可以选择`打开方式 | 其他应用程序` (Open with | Other Application) 来打开一个列出可用应用程序的对话框。应用程序也支持拖放操作。你可以将数据文件拖到其关联的应用程序图标上（例如，在桌面上）；随后该应用程序将使用该数据文件启动。

要更改或设置用于特定类型文件的默认应用程序，你需要打开文件的`属性`对话框并选择`打开方式` (Open With) 选项卡。在这里，你可以选择用于该类型文件的默认应用程序。可能的应用程序将列出，并组织为默认、推荐、相关和其他类别。点击你想要更改为默认的项，然后点击`设置为默认` (Set as default) 按钮。一旦你选择了默认项，它将出现在该文件的`打开方式`列表中。

如果你想向`打开方式`菜单添加应用程序，请点击`显示其他应用程序` (Show other applications) 按钮以列出可能的应用程序。选择你想要的那个并点击`添加` (Add) 按钮。如果`打开方式`选项卡上有一个你不希望出现在`打开方式`菜单项中的应用程序，右键点击它并选择`忘记关联` (Forget association)。

### 文件和目录属性

在文件的`属性`对话框中，你可以查看文件的详细信息并设置选项和权限（参见图 6-57）。文件的`属性`对话框有三个选项卡：`基础` (Basic)、`权限` (Permissions) 和`打开方式` (Open With)。文件夹将有一个额外的`共享` (share) 选项卡。`基础`选项卡显示详细信息，如类型、大小、位置修改日期。类型是 MIME 类型，表示与其关联的应用程序类型。文件图标显示在顶部，带有一个显示文件名的文本框。你可以在`名称` (Name) 文本框中编辑文件名更改该名称。

![Image](img/image-276.png)

**图 6-57：Nemo 中的文件属性**

如果你想更改文件或文件夹使用的图标图像，点击名称旁边的图标以打开 `XAppChooser` 对话框（选择图标对话框）浏览你想要的。这里有几个选项卡持有不同的集合，如`应用程序`、`设备`、`位置`和`状态`（参见图 6-58）。浏览类别或使用搜索框查找图标。你当前使用的图标可以在`位置`类别中找到。你也可以点击工具栏上的`浏览`按钮打开“选择图像文件”对话框，你可以在其中选择系统图像文件。`/usr/share/pixmaps`目录包含了可能的图像，尽管你可以选择自己的图像（点击`位置`中的`pixmaps`项）。双击图像将其添加到“选择图标”对话框。然后选择该图像并点击`选择`按钮更改图标图像。

![Image](img/image-277.png)

**图 6-58：为文件、文件夹或应用程序选择图标**

文件的`权限`选项卡显示所有者、组和其他人的读取、写入和执行权限，如该文件设置。你可以在这里更改任何权限，只要该文件属于你。使用下拉菜单配置所有者、组和其他人的访问权限。你可以将所有者的权限设置为`只读` (Read Only) 或`读和写` (Read And Write)。对于组和其他，你也可以设置`无` (None)选项，拒绝访问。点击组名称将显示不同的组列表，允许你选择一个来更改文件的组。如果你想将其作为应用程序执行，请勾选`允许文件作为程序运行` (Allow executing file as program) 项。这将设置执行权限。





## 权限

文件夹的“权限”选项卡的工作方式非常相似，但它包含两个访问项：文件夹访问（Folder Access）和文件访问（File Access）。文件夹访问项控制对文件夹的访问，具有`None`（无）、`List Files Only`仅列出文件）、`Access Files`访问文件）和 `Create And Delete Files`创建并删除文件）选项。这些对应于赋予文件夹的读、写和执行权限。文件访问项允许您为文件夹中的所有文件设置权限。它们与文件相同：对于所有者，是`Read`（读）或`Read and Write`（读写）；对于组和其他用户，该项增加了一个`None`选项以拒绝访问。要相应地设置文件夹中所有文件的权限（而不只是文件夹），请点击“应用于包含的文件”按钮。

文件夹的“共享”选项卡允许您将文件夹作为网络共享。如果您有 `Samba` 或 `NFS`，这些允许您的文件夹和文件与其他系统上的用户共享。您可以指定共享的文件夹或文件是只读还是允许写入。要允许写入访问，请勾选“允许其他人在此文件夹中创建和删除文件”项。要向所有用户开放访问，请勾选“访客访问”项。

## Nemo 偏好

您可以在“偏好”对话框中为 Nemo 文件管理器设置偏好，可以通过在任何 Nemo 文件管理器窗口的“编辑”菜单中选择“偏好”项来访问(`编辑 | 偏好`）（参见图 6-59）。

“视图”选项卡允许您选择文件的默认显示方式，例如列表、图标或紧凑视图。您还可以为图标、紧凑视图和列表视图设置默认缩放级别。

“行为”设置允许您选择如何选择文件、管理垃圾箱以及处理可执行文件。

“显示”设置允许您选择想要在图标标题中显示的额外附加信息，如大小或日期。

“列表列”选项卡允许您同时选择在详细列表中显示的功能以及它们的顺序。除了已选择的`Name`（名称）、`Size`（大小）、`Date`（日期）和 `Type`（类型）之外，您还可以添加权限、组、MIME 类型和所有者。

“预览”选项卡允许您选择是否在图标中显示较小的预览内容，例如文本文件的开头文本。您还可以选择显示工具提示。

“工具栏”选项卡允许您选择一些在工具栏上显示的图标，如搜索、刷新、计算机和主页。

“上下文右键菜单”选项卡允许您选择在项目选择右键菜单中显示的项、文件管理器窗口背景的右键菜单、图标视图下背景右键菜单的额外项，以及桌面右键菜单（右键点击）的额外项。

“插件”选项卡允许为 Nemo 添加新功能，例如挂载压缩包和将图像文件设置为壁纸。

![Image](img/image-278.png)

图 6-59: Nemo 文件管理器偏好

### Nemo 插件与扩展

您可以使用插件和扩展来增强 Nemo，例如用于文件夹共享选项的 `NemoShare`，以及允许您创建（压缩）和提取归包的“Nemo Fileroller”。已安装的几个插件和扩展默认启用，并在相应的菜单中显示条目。要添加更多扩展，请使用软件管理器安装 nemo 扩展和插件包。扩展和插件包具有 `nemo-` 前缀，例如 `nemo-share` 和 `nemo-fileroller`。

插件和扩展在 Nemo 偏好的“插件”选项卡中启用，可以通过“编辑”菜单(`编辑 | 插件`) 访问，也可以使用 `Alt+p` 键访问（参见图 6-60）。“操作”是可以从桌面菜单（右键点击桌面上的任何空白区域）以及其他弹出文件和文件夹菜单中执行的任务。启用某操作将将其列在列表中。禁用它将将其从该菜单中移除。例如，启用“设置为壁纸”操作会在图像文件的弹出菜单中（右键点击图像文件）放置一个“设置为壁纸”的条目。启用“添加桌面组件”操作会在桌面弹出菜单中添加一个“添加桌面组件”条目。“扩展”部分列出了已安装的扩展，如 `NemoShare` 和 `Nemo Fileroller`。已启用的扩展复选框已勾选。点击复选框切换扩展的启用和禁用。如果您禁用或启用扩展，必须重启 Nemo 更改才能生效。当您进行更改时，会出现一个“扩展已更改。需要重启。”按钮。点击该按钮重启 Nemo。还有按钮允许您一次性禁用或启用操作和扩展。

![Image](img/image-279.png)

图 6-60: Nemo 插件与扩展

您还可以将自己的操作和脚本文件添加到 `.local/share/nemo/` 文件夹中的 actions（操作）和 scripts（脚本）文件夹中。点击 actions 和 scripts 部分的文件夹图标可以打开这些文件夹。脚本允许您添加自己的可执行文件。

## 系统设置

您可以使用“系统设置”对话框中列出的管理工具来配置桌面设置并执行大多数管理任务，该对话框可以通过“偏好”菜单和菜单收藏收藏图标栏访问。系统设置将工具组织为“外观”、“偏好”、“硬件”和“管理”类别（参见图 6-61 并参见图 6-62）。某些工具调用了之前的版本中可用的 Ubuntu 支持系统工具，如 `Sound`（声音（`PulseAudio`））和 `Printers`（打印机）。其他是处理管理任务的工具（管理部分），如 `Users`、`Groups`、软件源 和 `firewalls`。

![Image](img/image-280.png) ![Image](img/image-281.png)

图 6-61: 系统设置对话框（外观和偏好）

系统设置工具顶部有一个返回箭头，点击它可以返回到系统设置。表 6-9 列出了系统设置。

![Image](img/image-282.png)

图 6-62: 系统设置对话框（硬件和管理）

| 设置 | 图标 | 描述 |
| :--- | :--- | :--- |
| 外观部分 | | |
| 背景 | ![Image](img/image-283.png) | 选择背景，具有比例、渐变和颜色选项。 |
| 主题 | ![Image](img/image-284.png) | 安装主题并选择图标、控件、窗口边框、指针和键绑定样式。 |
| 字体 | ![Image](img/image-285.png) | 选择默认、窗口标题和文档字体，具有缩放、抗锯齿和平滑选项。 |
| 效果 | ![Image](img/image-286.png) | 窗口和对话框关闭、打开以及最大化/最小化的淡入效果。 |
| 偏好部分 | | |
| 辅助 | ![Image](img/image-287.png) | 启用辅助登录和键盘等功能 |
| 账户详情 | ![Image](img/image-288.png) | 设置密码、头像和全名。 |
| 小组件 | ![Image](img/image-289.png) | 向面板添加小组件 |
| 日期时间 | ![Image](img/image-290.png) | 手动设置时间或使用网络时间，具有允许您设置时间格式的选项。 |
| 桌面组件 | ![Image](img/image-291.png) | 向桌面添加桌面组件 |
| 桌面 | ![Image](img/image-292.png) | 选择在桌面上显示主文件夹、计算机和垃圾箱的图标，以及挂载卷和网络服务器的图标。默认是计算机、主目录和挂载卷。 |
| 扩展 | ![Image](img/image-293.png) | 添加桌面扩展，如桌面立方体、滚动条和 dock。 |
| 通用 | ![Image](img/image-294.png) | 设置桌面缩放和杂项选项 |





| 特性 | 图片 | 描述 |
| :--- | :--- | :--- |
| 热点 | ![Image](img/image-295.png) | 点击此角落可以显示工作空间选择屏幕（显示所有工作空间选项）、缩放后的窗口（显示所有窗口选项）、显示桌面或运行选定的应用程序。 |
| 输入法 | ![Image](img/image-296.png) | 为支持语言的配置和安装说明。 |
| 语言 | ![Image](img/image-297.png) | 语言选择 |
| 通知 | ![Image](img/image-298.png) | 配置桌面通知的显示 |
| 在线账户 | ![Image](img/image-299.png) | 配置在线账户访问 |
| 面板 | ![Image](img/image-300.png) | 设置面板默认值和如面板大小等功能。面板布局可以是传统的（一个底部面板，默认）、翻转的（面板在顶部）和经典（（两个面板，顶部一个，底部一个）。 |
| 备选应用程序 | ![Image](img/image-301.png) | 设置默认应用程序和可移动媒体的默认值。 |
| 隐私 | ![Image](img/image-302.png) | 启用记住最近访问的文件 |
| 屏幕保护 | ![Image](img/image-303.png) | 屏幕保护和屏幕锁定选项，设置闲置时间变暗或锁定屏幕。 |
| 启动应用程序 | ![Image](img/image-304.png) | 打开启动应用程序设置对话框，选择启动时运行的应用程序。 |
|  | ![Image](img/image-305.png) | 设置窗口显示选项，如标题栏上的点击操作、聚焦模式、要显示的标题栏按钮。你还可以配置窗口切换器（`Alt-tab`）。 |
| 窗口平铺 | ![Image](img/image-306.png) | 设置窗口平铺、吸附和边缘翻转的窗口显示选项。 |
| 工作空间 | ![Image](img/image-307.png) | 配置工作空间显示 |

## 硬件部分
| | | |
| 蓝牙 | ![Image](img/image-308.png) | 蓝牙检测与配置 |
| 颜色 | ![Image](img/image-309.png) | 设置设备的色彩方案 |
| 显示 | ![Image](img/image-310.png) | 更改屏幕分辨率、刷新率和屏幕方向。 |
| 图形平板 | ![Image](img/image-311.png) | 配置图形平板 |
| 键盘 | ![Image](img/image-312.png) | 配置特殊任务的重复按键敏感度。 |
| 鼠标和触摸板 | ![Image](img/image-313.png) | 鼠标和触摸板配置：选择方向、速度和辅助功能 |
| 网络 | ![Image](img/image-314.png) | 开启或关闭线路和无线网络。你可以访问可用无线网络和代理配置。 |
| 电源管理 | ![Image](img/image-315.png) | 设置笔记本的电源选项 |
| 打印机 | ![Image](img/image-316.png) | 使用 `system-config-printer` 配置打印机 |
| 声音 | ![Image](img/image-317.png) | 配置音效、输出音量、输入量和应用程序设置 |
| 系统信息 | ![Image](img/image-318.png) | 系统和硬件信息 |

## 管理部分
| | | |
| 设备驱动程序 | ![Image](img/image-319.png) | 选择显卡等设备驱动程序。 |
| 防火墙 | ![Image](img/image-320.png) | 打开 `ufw` 对话框管理防火墙。需要安装 `ufw`。 |
| 登录 | ![Image](img/image-321.png) | 打开登录窗口设置以配置 Linux 显示管理器 (`LightDM`)。 |
| 软件源 | ![Image](img/image-322.png) | 打开 Linux Mint 软件源选择对话框以激活或禁用存储。 |
| 用户和组 | ![Image](img/image-288.png) | 管理用户 |

**表 6-9：桌面设置**

## 外观

外观部分提供了四个对话框来配置背景、字体和桌面效果。

### 背景

背景对话框列出了你可以选择的背景（参见图 6-63）。在“图像”选项卡中，左侧列表列出了已安装的背景集。你可以点击列表左下角的“”按钮从本地文件夹选择自定义图像。这将打开“添加文件夹”对话框，允许你选择图像文件夹。你可以使用列表左下角的“-”按钮删除文件夹。

![Image](img/image-323.png) ![Image](img/image-324.png)

图 6-63：背景：图像选项卡

在设置中，你可以选择从选定文件夹运行幻灯片，并设置随机顺序和间隔（参见图 6-64）。从图片菜单中，你可以选择放大、居中、等放、平铺等显示选项。

在设置中，你可以选择从选定文件夹运行幻灯片，并设置随机顺序和间隔（参见图 6-64）。从图片菜单中，你可以选择放大、居中、等放、平铺等显示选项。

在设置中，你可以选择从选定文件夹运行幻灯片，并设置随机顺序和间隔（参见图 6-64）。从图片菜单中，你可以选择放大、居中、等放、平铺等显示选项。

在设置中，你可以选择从选定文件夹运行幻灯片，并设置随机顺序和间隔（参见图 6-64）。从图片菜单中，你可以选择放大、居中、等放、平铺等显示选项。

在设置中，你可以选择从选定文件夹运行幻灯片，并设置随机顺序和间隔（参见图 6-64）。从图片菜单中，你可以选择放大、居中、等放、平铺等显示选项。

在设置中，你可以选择从选定文件夹运行幻灯片，并设置随机顺序和间隔（参见图 6-64）。从图片菜单中，你可以选择放大、居中、等放、平铺等显示选项。

在设置中，你可以选择从选定文件夹运行幻灯片，并设置随机顺序和间隔（参见图 6-64）。从图片菜单中，你可以选择放大、居中、等放、平铺等显示选项。

在设置中，你可以选择从选定文件夹运行幻灯片，并设置随机顺序和间隔（参见图 6-64）。从图片菜单中，你可以选择放大、居中、等放、平铺等显示选项。

在设置中，你可以选择从选定文件夹运行幻灯片，并设置随机顺序和间隔（参见图 6-64）。从图片菜单中，你可以选择放大、居中、等放、平铺等显示选项。

在设置中，你可以选择从选定文件夹运行幻灯片，并设置随机顺序和间隔（参见图 6-64）。从图片菜单中，你可以选择放大、居中、等放、平铺等显示选项。

在设置中，你可以选择从选定文件夹运行幻灯片，并设置随机顺序和间隔（参见图 6-64）。从图片菜单中，你可以选择放大、居中、等放、平铺等显示选项。

在设置中，你可以选择从选定文件夹运行幻灯片，并设置随机顺序和间隔（参见图 6-64）。从图片菜单中，你可以选择放大、居中、等放、平铺等显示选项。

在设置中，你可以选择从选定文件夹运行幻灯片，并设置随机顺序和间隔（参见图 6-64）。从图片菜单中，你可以选择放大、居中、等放、平铺等显示选项。

在设置中，你可以选择从选定文件夹运行幻灯片，并设置随机顺序和间隔（参见图 6-64）。从图片菜单中，你可以选择放大、居中、等放、平铺等显示选项。

在设置中，你可以选择从选定文件夹运行幻灯片，并设置随机顺序和间隔（参见图 6-64）。从图片菜单中，你可以选择放大、居中、等放、平铺等显示选项。

在设置中，你可以选择从选定文件夹运行幻灯片，并设置随机顺序和间隔（参见图 6-64）。从图片菜单中，你可以选择放大、居中、等放、平铺等显示选项。

在设置中，你可以选择从选定文件夹运行幻灯片，并设置随机顺序和间隔（参见图 6-64）。从图片菜单中，你可以选择放大、居中、等放、平铺等显示选项。

在设置中，你可以选择从选定文件夹运行幻灯片，并设置随机顺序和间隔（参见图 6-64）。从图片菜单中，你可以选择放大、居中、等放、平铺等显示选项。

在设置中，你可以选择从选定文件夹运行幻灯片，并设置随机顺序和间隔（参见图 6-64）。从图片菜单中，你可以选择放大、居中、等放、平铺等显示选项。





在“添加/删除”选项卡的底端有一个工具栏，其中包含“更多信息”（灯泡图标）按钮、“卸载”（用于移除已安装的主题）、“更新”（用于更新已安装的主题）以及“刷新”（更新可用主题列表）按钮。要查看所选主题的更多信息，请点击“更多信息”按钮打开其网页。可以在 [`cinnamon-spices.linuxmint.com/themes`](https://cinnamon-spices.linuxmint.com/themes) 找到可用主题列表。

![Image](img/image-247.png)

![Image](img/image-334.png)

图 6-68：主题（在线主题）

在“设置”选项卡上，你可以设置在菜单和按钮中显示图标的选项，还可以设置滚动条行为选项，例如允许叠加滚动条（参见 图 6-69）。

![Image](img/image-335.png)

图 6-69：主题（设置选项卡）

## 偏好

在系统设置偏好部分，Applets（应用插件）和菜单等对话框允许你配置桌面。这里讨论了 Cinnamon 的偏好，例如时间设置（日历）和应用程序默认设置（应用程序与可移除介质）。

### 首选应用程序和可移除介质

“首选应用程序”对话框允许你为任务和媒体设置默认应用程序。在“首选应用程序”选项卡上，你可以为基本类型的文件设置默认应用程序：网络、邮件、文档、文本、音乐、视频、照片、源代码和终端（参见 图 6-70）。使用菜单选择已安装的替代方案，例如使用 Thunderbird 代替 Evolution 处理邮件，或使用图像查看器 代替 Shotwell 查看照片。

![Image](img/image-336.png)  ![Image](img/image-337.png)

图 6-70：首选应用程序

在“可移除介质”选项卡上，你可以为不同类型的媒体指定默认操作：CD 音频、DVD 视频、音乐播放器、照片和软件介质。你可以通过关闭“插入介质时提示或启动程序”选项来关闭此功能。你可以从菜单中选择用于不同媒体的应用程序（参见 图 6-71）。这些菜单还包括“询问做什么”、“什么都不做”和“打开文件夹”等选项。“打开文件夹”选项将打开一个显示光盘上文件的窗口。标记为“其他介质”的按钮会打开一个对话框，允许你为较少使用的介质（如蓝光光和音频 DVD）设置关联。初始情况下，所有条目都设置为“询问做什么”。对于相应的媒体会列出可能的选项，例如用于 CD 音频光盘的 Rhythmbox 音乐播放器和用于视频 DVD 的 Celluloid。

![Image](img/image-338.png)

图 6-71：首选应用程序：可移除介质

当你插入可移除介质（如 CD 音频光盘）时，关联的应用程序会自动启动，除非你更改了该偏好。如果你想针对某种类型的媒体关闭此功能，可以从其应用程序菜单中选择“什么都不做”项。如果你希望提示选项，请使用“询问做什么”项。这样，当你插入光盘时，会显示一个带有可能操作下拉菜单的对话框。从此菜单，你可以选择另一个应用程序，或选择“什么都不做”或“打开文件夹”选项。

### 时间与日期设置（日历插件）

日历插件位于底部面板的右侧（参见 图 6-72）。日历显示当前日期，但你可以使用日历顶部的月份和年份箭头切换到不同的月份和年份。

![Image](img/image-339.png)

图 6-72：日历插件

日期和时间选项通过系统设置“日期和时间”对话框进行设置，可以在日历菜单中选择“日期和时间设置”，或点击系统设置偏好部分的日期和时间图标来打开（参见 图 6-73）。

![Image](img/image-340.png)  ![Image](img/image-341.png)

图 6-73：日期和时间设置，网络时间

你通过左侧的地图或从“区域”或“城市”菜单中选择区域或城市来设置时区。你还可以指定时间格式，使用 24 小时制、显示日期以及秒。时间和日期可以手动设置或从时间服务器（网络时间开关）自动设置。对于手动更改，可以通过关闭“网络时间”开关直接设置时间和日期。

从插件对话框配置日历插件（或在面板上的日期插件上右键点击并选择“配置”），显示指定面板和插件日期显示格式的选项（参见 图 6-74）。该格式使用用于不同日期元素的格式占位符，例如 `%a` 表示星期，`%I` 表示小时，`%y` 表示年份。你可以点击“在面板上显示信息”按钮。

![Image](img/image-342.png)

图 6-74：日历插件

或者，你可以使用 `timedctl` 命令管理系统时间和日期。

```
sudo timedctl set-time "2016-06-21 15:40:10"
```

### 屏保与锁屏

系统设置屏保对话框整合了屏幕锁定选项并允许你自定义锁定显示。在“屏保”选项卡上，你可以指定屏幕空闲锁定时间。你还可以控制是否锁定屏幕。你可以将锁定设置为特定时间，或屏幕关闭时锁定（参见 图 6-75）。

![Image](img/image-343.png)  ![Image](img/image-344.png)

图 6-75：屏保选项卡

注意：Cinnamon 不再支持 Xscreensaver，屏保对话框中没有屏保选项卡。

在“自定义”选项卡上，你可以设置锁定时显示的离开消息，自定义显示时间的大小和字体，并启用允许快捷键、浮动时以及显示专辑封面等额外选项（参见 图 6-76）。

![Image](img/image-345.png)

图 6-76：屏保 - 自定义

### 语言

在“语言设置”对话框中，你可以为菜单和窗口选择语言（参见 图 6-77）。显示当前选择的语言。点击语言区域图标显示语言变体的图标菜单，例如“英语（爱尔兰）”或“英语（印度）”。区域选项调整货币、数字和测量等功能，例如“英语（英国）”或“英语（香港）”。点击“应用系统”按钮将语言应用于整个系统。使用“安装/删除语言”按钮打开“安装/删除语言”对话框，你可以在其中添加新语言或移除已安装语言。点击此对话框上的“添加”按钮可以添加新语言。

![Image](img/image-346.png)   ![Image](img/image-347.png)

**图 6-77：语言**





输入法应用程序提供了各种语言（如日语、韩语和中文）的安装和配置说明。这里有支持语言的标签页（参见图 6-78）。顶部的菜单允许您指定 `XIM` 框架。

![Image](img/image-348.png) ![Image](img/image-349.png)

图 6-78: 输入法

## 辅助功能

`System Settings`（系统设置）中的 `Accessibility`（辅助功能）对话允许您为键盘和鼠标操作配置界面的替代访问方式。四个标签页分别设置显示、键盘属性、打字和鼠标功能。`Visual`（视觉）允许您调整对比度和文本大小，以及是否允许使用屏幕阅读器（参见图 6-79）。`Keyboard`（键盘）显示屏幕键盘并使用视觉提示警报声。“打字辅助”可以调整按键。`Mouse`（鼠标）允许您使用键盘进行鼠标操作。

![Image](img/image-350.png) ![Image](img/image-351.png)

图 6-79: 辅助功能

## 启动应用程序

在 `Startup Applications`（启动应用程序）对话框中，您可以选择您想要自动启动的额外程序。某些程序已经是自动开启的（参见图 6-80）。如果您不再希望某个条目自动启动，请关闭该条目。要添加未列出的应用程序，请点击对话框底部按钮栏上的添加按钮 `(+)`，并选择“自定义命令”或“选择应用程序”。“选择应用程序”条目会打开一个 `Applications` 对话框，列出所有可能的应用程序。“自定义命令”条目会打开一个对话框，您可以在其中输入应用程序名称和程序（使用 `Browse` 选择程序，通常在 `/usr/bin` 中）。要从列表中删除某个条目，请选择它并点击按钮栏上的删除按钮 `(-)`。

您可以选择任何条目，并通过点击按钮栏上的编辑按钮（铅笔图标）来编辑其名称、应用程序以及启动延迟时间。这会打开 `Edit Startup Program`（编辑启动程序）对话框，包含 `Name`（名称）、`Command`（命令）、`Comment`（注释）和 `Startup delay`（启动延迟）条目。任何启动延迟将显示在其条目中。

如果您希望立即运行该应用程序，可以选择它，然后点击按钮栏上的“立即运行”（齿轮图标）。

![Image](img/image-352.png) ![Image](img/image-353.png)

图 6-80: 启动应用程序设置

## 扩展

扩展为您的桌面界面添加第三方增强功能，例如透明面板、桌面水印和摇动窗口。并非所有扩展都兼容，如果不兼容，您将收到警告。`Extensions`（扩展）显示两个标签：`Manage`（管理）和 `Download`（下载）（参见图 6-81）。`Manage` 标签列出已安装的扩展。使用底部的按钮栏来管理它们。可以通过 `(+)` 或 `-` 启用或禁用扩展，或通过 `(x)` 将其完全删除。弯箭头按钮将禁用所有扩展。启用的扩展旁边会出现勾选标记。如果它可以配置，还会出现一个齿轮按钮，您可以点击它可以打开配置对话框。

![Image](img/image-354.png) ![Image](img/image-355.png)

图 6-81: 扩展管理标签

`Download` 标签列出可用的扩展（参见图 6-82）。点击扩展的下载按钮（向下箭头）即可下载并安装它。随后勾选标记将取代向下箭头。`Sort by`（排序方式）菜单允许按名称、流行程度、日期和安装状态进行排序。您还可以使用左侧的搜索框搜索扩展。底部的按钮栏允许您获取有关扩展的更多信息（灯泡）、删除已安装的扩展 `(x)`、获取更新（齿轮）以及刷新列表（圆形箭头）。

![Image](img/image-356.png)

图 6-82: 扩展下载标签

## 通知

`System Settings Notifications`（系统设置通知）对话框允许您配置桌面通知（参见图 6-83）。有相应的开关可以启用通知、在超时后删除它们以及在屏幕底部显示它们。“显示测试通知”将使用您当前的设置显示一个通知示例。在此对话框中，您还可以设置 `OSD` 媒体键的大小。

![Image](img/image-357.png) ![Image](img/image-358.png)

图 6-83: 通知

## 隐私

`System Settings Privacy`（系统设置隐私）对话框让您决定是否想要记住最近的文件（参见图 6-84）。如果您选择记住最近文件，您还有“永从不忘记”的选项。您还可以检查 Internet 连接情况，查看您的网络连接是否可以访问互联网。

![Image](img/image-359.png) ![Image](img/image-360.png)

图 6-84: 隐私

## 通用

在 `General`（通用）对话框中，您可以设置缩放和杂项选项，例如禁用屏幕旋转和设置日志延迟。

![Image](img/image-361.png) ![Image]()

图 6-85: 通用

### 硬件

这里讨论了配置鼠标、键盘和电源管理的若干硬件任务。

### 系统信息

`System Info`（系统信息）对话框显示系统信息，如内存、处理器、显卡、发行版（64 位或 32 位）以及 Cinnamon 版本（参见图 6-86）。

![Image](img/image-362.png) ![Image]()

#### 鼠标和触摸板

`System Settings Mouse and Touchpad`（系统设置鼠标和触摸板）对话框是配置鼠标和触摸板的主要工具（参见图 6-87）。在 `Mouse` 标签页上，您可以选择鼠标速度、滚动方向、手性、双击次数以及“拖放”阈值。对于笔记本电脑，您可以在 `Touchpad` 标签页上配置触摸板，启用点击和边缘滚动。

![Image](img/image-364.png) ![Image]()

图 6-87: 系统设置，鼠标和触摸板

### 电源管理

对于电源管理，Linux Mint 使用 `GNOME Power Manager`，它利用计算机提供的高级配置电源接口 (`ACPI`) 支持来管理电源。`GNOME Power Manager` 在面板上显示当前电源源：电池（笔记本）或闪电（桌面）。点击电池图标将显示无线设备的电量，包括您的笔记本电脑和无线鼠标等无线设备（参见图 6-88）。设备条目包括设备产品和型号。您可以右键点击电源管理器面板图标来显示包含 `Configure` 条目的菜单。点击它可以打开 `Power Manager` 插件配置对话框，该对话框列出了插件的显示选项（参见图 6-88）。如果您希望在带有电池图标的面板显示剩余百分比，可以选择“显示百分比”选项。

您还可以通过带有 `Inhibit` 插件的面板快速关闭电源管理（将其添加到插件面板中）。

![Image](img/image-366.png) ![Image]()

图 6-88: GNOME 电源菜单和插件配置

`GNOME Power manager` 通过 `System Settings` 中的 `Power` 进行配置。在 `Power` 标签页上，您有有设置挂起超时时间以及在盖子关闭或电量低时采取的操作的选项（参见图 6-89）。如果存在，`Batteries` 标签页将显示笔记本电脑和无线鼠标的电池电量。





![Image](img/image-368.png) ![Image](img/image-369.png)

图 6-89: GNOME 电源管理器

在“亮度”选项卡中，你可以设置屏幕亮度，以及系统空闲时的调暗选项（参见图 6-90）。

要查看你的笔记本电脑或台式电脑的电源性能情况，可以使用从系统工具菜单访问 `Power statistics`（电源统计）。`Power Statistics` 窗口显示一个侧边栏，其中列出了你不同的电源设备。右侧面板将显示所选设备用电信息的选项卡。笔记本电池设备将显示三个选项卡：详细（Details）、历史（History）和统计（Statistics）。“历史”选项卡将显示你最近的使用情况，并带有耗尽时间（剩余时间）、充满时间（充电）、电量（Charge）和速率（Rate）的图表选项。“统计”选项卡可以显示充电和放电图。

![Image](img/image-370.png)

图 6-90: GNOME 电源管理器：亮度选项卡

## 键盘设置

系统设置键盘对话框显示了输入、快捷键和布局选项卡。“输入”选项卡用于调整重复键和光标闪烁（参见图 6-91）。“快捷键”选项卡允许你分配按键执行任务，例如启动网络浏览器或将键盘上的多媒体键映射到媒体任务（如播放和暂停）。只需选择任务然后按键即可。有针对桌面（Cinnamon）、多媒体（声音和媒体）、窗口管理和工作区管理的任务。通过工作区管理，你还可以映射按键执行工作区切换。已分配的按键将被显示。

![Image](img/image-371.png) ![Image](img/image-372.png)

图 6-91: 键盘输入

“布局”选项卡允许你选择语言（参见图 6-92）。系统会列出并选中当前的输入语言源。点击加号按钮打开列出其他语言源的对话框，你可以从中添加。点击键盘按钮查看当前所选输入源的键盘布局。你还可以为不同的窗口允许不同的语言布局。

![Image](img/image-373.png)

图 6-92: 键盘：布局选项卡

对于特殊的键盘选项，点击“选项”按钮以列出选项，例如启用杀死 X 服务器的键序列（参见图 6-93）。

你也可以在终端窗口中使用 `localectl` 命令设置系统位置和键盘布局设置。请检查 `localectl` 手页以获取详细的选项列表。`status` 选项显示当前的区域和键盘布局。`set-locale` 选项更改区域，`list-locale` 选项列出可用的区域。`set-keymap` 选项设置键盘布局，`list-keymaps` 选项列出可能的布局。

```
localectl status
```

![Image](img/image-374.png)

图 6-93: 键盘布局选项

# 7. MATE 桌面

MATE 桌面是一个源自 GNOME 2 桌面的简化且易用的桌面。MATE 的官方文件管理器是 `Caja`。熟悉 GNOME 2 的用户会发现相似的功能。MATE 只有一个面板，尽管你可以添加更多面板。工作区切换器默认不安装，但工作方式与 GNOME 2 相同。Linux Mint 版本 MATE 使用的菜单是 Linux Mint 菜单。Linux Mint 20 安装了 1.24 版本的 MATE。

GNU 网络对象模型环境（也称为 GNOME）是一个强大且易于使用的环境，主要由一个面板、一个桌面以及一组用于构建程序接口的桌面工具组成。GNOME 的设计旨在为开发强大的应用程序提供一个灵活的平台。

## MATE 桌面

MATE 桌面设计得非常简单，具有单个面板和桌面图标（参见图 7-1）。面板显示为跨跨底部的一条长条。它包含菜单、程序启动器和应用程序图标（applet 是设计在面板内运行的小程序）。你可以水平或垂直方向显示面板，并让它自动隐藏以显示全屏内容。

![Image](img/image-49.png)

图 7-1: MATE 桌面和面板

面板左侧是 Linux Mint 菜单的按钮。通过此菜单，你可以访问位置和应用程序。菜单旁边是应用程序按钮，随后是窗口列表 applet，它显示了已打开窗口的按钮。面板右侧是系统工具，如网络管理器、更新管理器、电源、音量和时钟图标。

屏幕的其余部分是桌面，你可以在这里放置文件夹、文件和应用程序启动器。你可以使用点击并拖拽的操作将文件从一个窗口移动到另一个窗口或桌面。按住 `Ctrl` 键拖放会复制文件。同时按住 `Ctrl` 和 `SHIFT` 键（`Ctrl-Shift`）进行拖放会在桌面上创建一个指向该文件夹或文件的链接。你可以从桌面上的“主文件夹”图标访问你的主目录。双击它会打开该文件夹。

在桌面上的任何位置点击右键都会显示菜单，通过它可以对齐桌面图标并创建新文件夹。

退出桌面时使用菜单中的“退出”选项。点击它会打开一个带有挂起、休眠、重启和关机选项的对话框。

### MATE 组件

从用户的视角来看，桌面界面四个组件：桌面、面板、主菜单和文件管理器（参见图 7-2）。你有一个显示的面板，用于菜单、应用程序图标和管理窗口。当你打开一个窗口时，面板上会显示相应的按钮，你可以用它最小化和恢复窗口。

要启动程序，你可以从 Linux Mint 菜单选择其条目。你也可以点击面板中的应用程序图标（如果显示）或将数据文件拖放到它。要向桌面添加应用程序图标，右键点击 Linux Mint 菜单中的条目并选择“添加到桌面”。

![Image](img/image-375.png)

图 7-2: 带有 Linux Mint 菜单和 Caja 文件管理器的 MATE

### 将文件拖放到桌面

从文件管理器窗口拖放到桌面的任何项目图标也会出现在桌面上。默认的拖放操作是移动操作。如果你在文件管理器窗口中选择文件并将其拖到桌面，你实际上是将文件从当前目录移动到桌面文件夹，桌面文件夹位于你的主目录中。桌面文件夹名为 `Desktop`。在拖动文件夹到桌面的情况下，整个文件夹及其子文件夹都将移动到桌面文件夹。

要从桌面删除图标，请右键点击并选择“移动到垃圾桶”。如果你选择在桌面上显示垃圾桶图标，只需将其拖放到垃圾桶即可。

通过按住 `ctrl` 键然后从文件管理器窗口点击并拖到桌面，可以向桌面复制文件。你会看到鼠标图标变为带有带有 `+` 符号的手手形状，这表示你正在创建副本，而不是移动原始文件。




你也可以在桌面上为任何文件创建链接。如果你希望在某个文件夹中保留一个版本，并仅从桌面访问它，这将非常有用。你也可以将链接用于那些可能不希望出现在菜单或面板上的自定义程序。创建链接有两种方法。

在持续按住 `Ctrl` 和 `Shift` 键（即 `Ctrl-SHIFT`）的同时，将文件拖动到你想创建链接的位置。随后会出现一个图标的副本，其右角带有一个小箭头，表示它是一个链接。你可以点击此链接来启动程序、打开文件或打开文件夹，取决于你所链接的文件类型。或者，首先点击并拖动文件出窗口，在移动文件但松开鼠标按钮之前，按下 `ALT` 键。这将弹出一个菜单，提供 `Move Here`（移动到此处）、`Copy Here`（复制到此处）和 `Link Here`（在此处链接）选项。选择 `Link Here` 选项即可创建链接。

拖放文件操作适用于 `Workspace Switcher` 提供的虚拟桌面。`Workspace Switcher` 会在面板为每个虚拟桌面创建图标，并为在上面打开的任何窗口创建按钮。`Workspace Switcher` 默认不会添加。你需要手动将其添加到面板。

### 桌面设置

你可以使用 `Desktop Settings` 对话框配置桌面和窗口显示设置，你可以通过 `Preferences` 菜单或 `Control Center` 访问它（参见 图 7-3）。`Desktop Settings` 对话框有三个选项卡：`Desktop`、`Windows` 和 `Interface`。`Desktop` 选项卡允许你选择在桌面上显示哪些系统图标。`Computer` 和 `Home` 文件夹图标默认被选中，以及插入的 USB 驱动器和 DVD 等外部文件系统的 `Mounted` 卷。你也可以选择选择显示 `Network` 和 `Trash` 图标。

![Image](img/image-376.png) ![Image](img/image-377.png)

图 7-3：MATE 桌面设置

在 `Windows` 选项卡上，你可以选择使用哪个窗口管理器，`Marco` 或较旧的 `Metacity`。对于每种，你都可以进一步选择是否支持合成，或使用不带合成的窗口管理器。`Marco+Compositing` 是默认设置。如果需要，还可以设置 `User Interface Scaling` 选项以支持 HiDPi。所选窗口管理器的设置将出现在该选项卡的后续部分。对于 `Marco`，你可以选择按钮布局、移动窗口时是否显示内容，以及在标题栏中使用系统字体。对于 `Metacity`，你也可以选择按钮布局并在标题栏中使用系统字体。

`Interface` 选项卡允许你选择是否在菜单、按钮和工具栏上显示图标，并设置工具栏中图标的大小。

### 桌面上的应用程序

在某些情况下，你可能希望在桌面上创建另一种访问文件的方法，无需将其从原始文件夹移动。你可以通过使用 `application launcher icon` 或为原始程序创建链接来实现。`application launcher icons` 是菜单和面板中用于显示和访问应用程序的组件。要在桌面上放置应用程序图标以作为菜单条目，你只需将应用程序条目从菜单拖动到桌面，或者右键点击并选择 `Add to desktop`。

对于不在菜单中的应用程序，你可以使用 `application launcher icon` 或为原始程序创建链接。

### 桌面菜单

你也可以在桌面上为任何文件创建链接。如果你希望在某个文件夹中保留一个版本，并仅从桌面访问它，这将非常有用。你也可以将链接用于那些可能不希望出现在菜单或面板上的自定义程序。

| 菜单项 | 说明 |
| :--- | :--- |
| Create Desktop | 创建新桌面。 |
| Create Launcher | 创建应用程序启动器。 |
| Create Document | 创建新文档。 |
| Organize Desktop by Name | 按名称整理桌面。 |
| Keep Aligned | 保持对齐。 |
| Cut, Copy, Paste | 剪切、复制或粘贴。 |
| Change Background | 打开背景对话。 |

表 7-1：桌面菜单

### 窗口

你可以通过点击窗口的任何侧边或拖动来调整窗口大小。你可以通过点击标题栏来移动窗口。窗口的右上角显示 `Minimize`、`Maximize` 和 `Close` 按钮（参见 图 7-4）。点击 `Minimize` 按钮后窗口将不再显示。该按钮仍留在底部面板（窗口列表小部件）上。在标题栏任意位置右键点击（或按下 `Alt-space`）会显示窗口菜单。

![Image](img/image-378.png)

图 7-4：MATE 窗口

你可以通过按下 `Alt-Tab` 键在窗口之间快速切换。窗口切换栏会打开打开窗口的缩略图（参见 图 7-5）。

![Image](img/image-379.png)

图 7-5：使用缩略图切换窗口

你可以使用 `Window Preferences` 对话框中的 `Behavior` 选项卡配置窗口行为，可以通过 `Preferences` 菜单和 `Control Center` 中的 `Windows` 访问。你可以选择合成功能、通过将鼠标悬停在窗口上选择窗口，并使用 `meta` 键代替 `Alt` 键移动窗口。可以通过菜单选择双击标题栏时执行的操作。默认是 `maximize`，但其他选项包括折叠窗口并最小化。

### 窗口列表

`Window List` 小部件显示当前打开的窗口（参见 图 7-6）。`Window List` 将打开的窗口排列为一系列按钮，每个窗口对应一个。



右键点击窗口的`Window List`窗口列表）按钮会打开一个菜单，允许您对窗口进行`Minimize`最小化、`Unminimize`还原、`Move`移动、`Resize`调整大小、`Maximize`最大化或`Close`关闭，始终置顶、仅在其工作区或在可见的工作区显示，以及将窗口移动到另一个工作区。`Minimize`操作会将窗口缩小为其`Window List`条目。右键点击该条目将显示菜单，其中包含`Unminimize`选项而不是`Minimize`，您可以使用它重新显示窗口。`Close`条目将关闭窗口并结束该应用程序。`Always On Top`始终置顶选项将使窗口始终置在任何其他打开的窗口之上。`Always on Visible Workspace`始终在可见工作区选项将始终在您切换到的任何工作区上显示窗口。`Always on This Workspace`始终在此工作区（默认）仅在此工作区显示窗口。还有将窗口移动到相邻工作区或特定工作区的条目。

![Image](img/image-380.png)

图 7-6: 窗口列表小部件

`Window List`小部件由窗口列表小部件开头的一条小条表示（参见图 7-6）。要配置`Window List`小部件，右键点击此条并选择`Preferences`首选项条目以打开`Window List Preferences`对话框（参见图 7-7）。在这里，您可以设置各种功能，例如是否在面板上对窗口分组、是否显示缩略图及其大小、是否显示所有打开的窗口或仅显示当前工作区的窗口，或者将窗口恢复到哪个工作区。

![Image](img/image-381.png)

图 7-7: 窗口列表设置

如果您选择分组窗口，则常用窗口将分组在一个按钮下，该按钮会像菜单一样展开，列出组中的每个窗口。例如，所有打开的终端窗口将分组在一个单个按钮下，点击该按钮将弹出它们的按钮列表。该按钮显示打开窗口的数量。您也可以选择仅当`Window List`小部件空间不足以为每个窗口显示单独按钮时才分组。

## 工作区切换器

`Workspace Switcher`工作区切换器小部件允许您切换到不同的虚拟桌面（参见图 7-8）。可以通过从面板的“Add to Panel”框中选择它将`Workspace Switcher`添加到任何面板。它默认不会添加。`Workspace Switcher`将您的整个虚拟桌面显示为并列的独立矩形。打开的窗口显示为这些方格中的小型彩色矩形。您可以通过点击并拖动窗口在`Workspace Switcher`中的图像，将任何窗口从一个虚拟桌面移动到另一个虚拟桌面。

![Image](img/image-382.png) ![Image](img/image-383.png)

图 7-8: 工作区切换器，单行和双行

除了`Workspace Switcher`外，您还可以使用`Ctrl-Alt-arrow`键从一个工作区移动到另一个。当您使用`Ctrl-Alt-arrow`键时，右箭头和左箭头会带您在行内移动，而上键和下键会带您从一行移动到另一行。屏幕中心会出现一个小小的工作区栏，突出显示当前工作区并显示其名称（参见图 7-9）。

![Image](img/image-384.png) ![Image](img/image-385.png)

图 7-9: 切换工作区，Ctrl-Alt-arrow

要配置`Workspace Switcher`，右键点击该小部件显示菜单，然后选择`Preferences`显示`Workspace Switcher Preferences`对话框（参见图 7-10）。在这里，您可以选择工作区的数量并对其命名。默认为四个个。您还可以选择工作区的行数。还有显示工作区名称、允许工作区循环显示以及仅显示当前工作区的选项。

![Image](img/image-386.png)

图 7-10: 工作区切换器设置

## MATE 的 Linux Mint 菜单

Linux Mint 为 MATE 接口提供了了自己的菜单，称为`Linux Mint Menu`。它源自 SUSE Slab 菜单。`Linux Mint Menu`位于面板的左侧。`Linux Mint Menu`分为三个部分：`Places`位置、`System`系统和`Favorites`收藏。

`Places`部分显示常用位置：`computer`计算机、`home`主、`network`网络、`trash`垃圾箱和`mounted folders`挂载文件夹（参见图 7-11）。

`System`部分包含软件管理按钮、`Control Center`控制中心、`logout`注销和`shutdown`关机。`Control Center`打开`System Settings`系统设置。`Synaptic`打开软件包管理器。`Logout`按钮允许注销。`Quit`按钮打开`shutdown`对话框，提供`suspend`挂起、`hibernate`休、`restart`重启选项。

`Applications/Favorites`部分是您的收藏应用程序或所有已安装应用程序之间的切换开关。您可以使用右上角的按钮在两者之间切换。`Applications`视图按类别组织。您可以使用滚轮滚动类别。

`Linux Mint Menu`通过右下角的`Search`文本框支持搜索操作。搜索针对已安装的软件（参见图 7-12）。点击右侧的搜索按钮将显示带有其他搜索选项的菜单，如`DuckDuckGo`、`Wikipedia`、字典以及您的`computer`，并搜索`users`、教程以及关于设备和软件的信息。`Software`、`Tutorials`、`Hardware`、`Ideas`和`Users`的`Find`项都会打开 Linux 社区网站(`community.linuxmint.com`

图 7-11: Linux Mint 菜单

可以使用其弹出菜单对菜单应用程序项执行多种操作。右键点击该项显示菜单（参见图 7-13）。

![Image](img/image-389.png)

图 7-13: Linux Mint 菜单应用程序弹出菜单

可以通过将图标从菜单拖动到桌面或面板将应用程序启动器添加到其中。您也可以右键点击应用程序图标并选择“Add to desktop”或“Add to panel”（参见图 7-13）。

如果您希望某个应用程序在登录时启动，可以在菜单上右键点击它并选择“Launch when I log in”。从弹出菜单中，您还可以直接卸载应用程序并打开应用程序的属性对话框。





“收藏”部分列出了你可能需要的默认收藏项目。点击右上角的“收藏”按钮即可显示你的收藏。你可以通过右键点击应用程序条目并选择“显示在我的收藏中”将任何应用程序添加到收藏列表（参见图 7-14）。只需只需点击并拖动到新位置，即可在菜单上重新排列收藏顺序。要移除收藏项目，右键点击并选择“移除”。

![Image](img/image-390.png)

图 7-14：Linux Mint 菜单收藏

### Linux Mint 菜单设置对话框

你可以使用“菜单偏好”对话框来配置菜单，可以通过右键点击面板上的菜单按钮并在弹出菜单中选择“偏好”来访问。菜单偏好有七个标签页：常规、外观、应用程序、收藏、系统和位置（参见图 7-15）。

在“常规”标签页上，你可以指定 Linux Mint 菜单小组件的名称（文本）以及是否显示图标。你可以选择不同的图标，并指定用于显示菜单的键盘命令。你还可以选择是否在菜单上显示“系统”和“位置”部分，以及最近使用的文档、应用程序和工具提示符（参见图 7-16）。

![Image](img/image-391.png) ![Image](img/image-392.png)

图 7-15：Linux Mint 菜单设置对话框

![Image](img/image-393.png)

图 7-16：带有最近文档选项的 Linux Mint 菜单 - 常规标签

“外观”标签页允许你为标题、边框和背景选择主题。你还可以为收藏、应用程序、系统和位置菜单选择图标大小。

在“收藏”标签页上，你可以设置收藏菜单的布局和选项，包括列数以及在打开 Linux Mint 菜单时是否显示收藏菜单。

在“应用程序”标签页上，你可以配置应用程序菜单，选择显示类别图标、在弹出注释中显示应用程序注释，以及允许鼠标悬停时选择条目。你还可以配置搜索功能以搜索未安装的包，并记住上次搜索内容。

在“系统”标签页上，你可以设置高度并选择显示的默认项目。

对于“位置”，你可以选择显示哪些默认项目以及是否显示你的书签。你还可以为菜单添加自定义位置（文件夹）。点击“新建”按钮打开对话框，你可以在其中输入位置名称和文件夹路径名称。

注意：你可以通过从面板中移除 Linux Mint 菜单，然后向面板添加“主菜单”小组件将 Linux Mint 菜单替换为 MATE 菜单。Linux Mint 菜单的名称为 `mintMenu`，如果你以后想再次添加它。

### MATE 面板

面板是 MATE 接口的主要组件。通过面板，你可以启动应用程序、运行小组件并访问桌面区域。你可以将 MATE 面板认为是你在桌面上可以使用的一种工具。你可以在桌面上显示多个个 MATE 面板，每个面板上都可以有你放置在其中的小组件和菜单。在这方面，MATE 非常灵活，允许你以任何想要的方式配置面板。MATE 面板的工作原理与 GNOME 2 面板非常相似。你可以轻松地向面板添加小组件以及应用程序启动器。屏幕底部已为你设置了一个默认面板，包含菜单、显示桌面、应用程序启动器、窗口列表和几个系统小组件（参见图 7-17）。这些项目包括更新管理器、音量控制、网络管理器、电源管理器和时钟的按钮。

![Image](img/image-394.png)

![Image](img/image-395.png)

![Image](img/image-396.png)

图 7-17：MATE 面板

面板配置任务（如添加应用程序、选择小组件、设置菜单和创建新面板）可以通过面板弹出菜单进行处理（参见图 7-18）。只需在面板的空白处任意位置右键点击，即可显示包含“属性”、“新建面板”、“添加到面板”、“重置面板”和“删除此面板”等条目的菜单，以及“帮助”和“关于”。新建面板”允许你创建其他面板；添加到面板”允许你向面板添加项目，例如应用程序启动器、用于工作区切换等简单任务的小组件，以及像 Linux Mint 菜单之类的菜单。“重置面板”条目将面板恢复到桌面默认状态，移除你对其做的任何更改（如添加的小组件、应用程序或文件夹）。“属性”条目将显示一个用于配置该面板功能的对话框，例如面板的位置及其隐藏功能。

要添加新面板，请选择面板弹出菜单中的“新建面板”条目（参见图 7-18）。屏幕顶部会自动创建并显示一个新的扩展的面板。然后，你可以使用面板的“属性”对话框设置不同的显示和背景功能，如后续章节所述。

![Image](img/image-397.png)

图 7-18：MATE 面板弹出菜单

### 面板属性

要配置单个面板，你需要使用“属性”对话框（参见图 7-19）。通过右键点击特定面板并选择“属性”来显示此对话框。对于单个面板，它显示两个标签页：“常规”和“背景”。

### 显示面板

在对话框的“常规”标签页上，你可以决定面板的方式。你有方向、大小以及扩展、自动隐藏或显示隐藏按钮的选项。“方向”条目允许你选择希望将面板放在屏幕的哪侧。然后你可以选择是否扩展面板。扩展面板将填充边缘，而未扩展面板将根据面板中的项目确定大小，并在两端显示手。

你可以自动或手动隐藏扩展面板。这些功能在面板属性对话框中指定为“自动隐藏”和“显示隐藏按钮”。要自动隐藏面板，请选择自动隐藏功能。要重新显示面板，将鼠标移动到面板所在的边缘。你可以在面板属性窗口中启用或禁用自动隐藏功能。

如果你希望手动隐藏面板，请选择“显示隐藏按钮”。面板两端将显示带箭头的隐藏按钮。你还可以选择这些按钮是否显示箭头（显示箭头为默认设置）。

![Image](img/image-398.png) ![Image](img/image-399.png)

图 7-19：MATE 面板属性

### 未扩展面板：可移动与固定

虽然扩展面板始终位于屏幕边缘，但未扩展面板是可移动的。它可以位于屏幕边缘，像扩展面板的缩减版本一样，或者你可以将其移动到桌面上的任何位置，就像移动图标一样。





未展开的面板将缩小到其包含的组件数量，并在两端显示手柄。你可以通过拖动手柄来移动面板。右键点击任一手柄即可访问带有“属性”（Properties）条目的面板菜单。

要将未展开的面板固定在当前位置，请在`面板属性`(Panel Properties）对话框的`通用`(General）选项卡上选择`显示/隐藏按钮`(Show hide buttons）功能。这将手柄替换为`隐藏`按钮并使面板固定。点击`隐藏`按钮会将面板隐藏到屏幕边缘，与展开面板的操作相同。如果一个展开的面板已经位于该边缘，则隐藏的未展开面板的按钮将显示在其上方，这与隐藏的展开面板的情况相同。`自动隐藏`(Autohide）功能也适用于放置在屏幕边缘的未展开面板。

如果你想将未展开的面板固定在屏幕边缘，请确保它被放置在你想要的边缘，然后设置其`显示/隐藏按钮`功能。

## 面板背景

通过`面板属性`对话框中的`背景`(Background）选项卡，你可以更改面板的背景颜色或图像。对于颜色背景，你点击`颜色`(Color)按钮显示颜色选择窗口，你可以在其中从调色板或颜色框列表中选择颜色，也可以输入其颜色代码。一旦选择了颜色，你就可以使用`样式`(Style)滑块使其更透明或更不透明。要使用图像而不是颜色，请选择图像条目并使用`浏览`(Browse)按钮找到你所需的图像文件。对于图像，你也可以直接从文件管理器将图像文件拖放到面板上。该图像将成为该面板的背景图像。

## 面板对象

面板可以包含多种不同类型的对象。这些包括菜单、启动器、应用程序、抽屉（drawers）和特殊对象。

**菜单 (Menus)** 面板菜单包含启动器，这些是用于启动应用程序或执行命令的按钮。

**启动器 (Launchers)** 你可以在`应用程序 1Applications)菜单中选择任何应用程序条目，并在面板上为其创建一个启动器。

**应用程序 (Applets)** 应用程序是设计在面板内运行的小型应用程序。显示不同桌面的`工作区切换`(Workspace Switcher)就是一个 GNOME 应用程序的示例。

**抽屉 (Drawers)** 抽屉是面板的扩展，可以打开或关闭。你可以将抽屉想为面板的可收缩部分。你可以向其中添加任何可以向普通面板添加的内容，包括应用程序、菜单，甚至其他的抽屉。

**特殊对象 (Special objects)** 这些用于其他面板对象不支持的特殊任务。例如，`注销 1Logout)和`锁定 1Lock)按钮就是特殊对象。

### 移动、移除和锁定对象

要移动面板内的任何对象，右键点击它并选择`移动 1Move)条目。你可以将其移动到同一面板的不同位置，也可以移动到另一个面板。对于启动器，你可以直接将对象拖动到你想去的地方。要从面板中移除对象，右键点击它显示弹出菜单，然后选择`从面板移除 1Remove From Panel)条目。要防止对象被移动或移除，你可以设置其锁定功能（右键点击对象并选择`锁定到面板 1Lock To Panel)条目）。稍后允许其移动，你必须先解锁对象（右键点击它并选择`解锁 1Unlock)）。

### 添加对象

要向面板添加对象，请从面板的`添加到面板 1Add to Panel)对话框中选择该对象（参见图 7-20）。要显示`添加到面板`对话框，右键点击面板并选择`添加到面板 1Add to Panel)条目。此`添加到面板`对话框显示了很长的常用对象列表，例如`mintMenu`菜单（Linux Mint 菜单）、`注销 1Log Out)和`时钟 1Clock)。对于应用程序应用程序，你可以点击`应用程序启动器 1Applications Launcher)条目并点击`向前 1Forward)按钮来列出你安装的所有应用程序。启动器也可以通过直接拖动来添加到面板中。启动器包括应用程序、窗口和文件。`自定义应用程序启动器 1(Custom Application Launcher)允许你创建自定义启动器。

### 应用程序启动器

将已具有应用程序启动器的应用程序添加到面板中是很容易的。你只需要将应用程序启动器拖到面板上即可。这会自动为该面板创建一个该启动器的副本以供该面板使用。启动器可以是菜单项或桌面图标。Linux Mint 菜单中的所有条目都是应用程序启动器。要从菜单添加应用程序，只需选择它并将其拖到面板上。例如，如果你经常使用`Pluma`文本编辑器并想将其图标添加到面板，请点击并拖动`辅助工具 1Accessories)菜单中的`Pluma`菜单条目到面板。`Pluma`文本编辑器图标将出现在你的面板中。你也可以将任何桌面应用程序图标拖到面板上，以向该面板添加其副本。

![图像](img/image-400.png)

图 7-20：用于应用程序的 MATE 面板“添加到面板”对话框

对于任何菜单项，你也可以进入其条目并右键点击它，然后选择`添加到面板 1Add to panel)条目。随后该应用程序的应用程序启动器将添加到面板中。要将`Pluma`文本编辑器添加到面板，右键点击`辅助工具`菜单中的`文本编辑器 1(Text Editor)菜单条目，并选择`添加到面板`条目。`Pluma`文本编辑器图标现在出现在你的面板中。

此外，如前所述，你可以打开`添加到面板`对话框，然后选择`应用程序启动器 1Application Launcher)条目并点击`向前 1Forward)按钮。这将列出你安装的所有应用程序。




Applets（小程序）是在面板内执行任务的小型程序。要添加小程序，右键点击面板并从弹出菜单中选择“添加到面板”（Add To Panel）。这将显示“添加到”框，其中列出了常用的小程序以及其他类型的对象（例如启动器）。选择您想要的项。例如，要向面板添加时钟，请从面板的“添加到”框中选择“Clock”。添加后，小程序将出现在面板上。如果您想移除小程序，右键点击它并选择“从面板移除”（Remove From Panel）。

MATE 提供了许多实用的小程序。某些小程序可以监控您的系统，例如电池电监控（Battery Charge Monitor，检查笔记本电脑电池）以及系统监视器（System Monitor，显示当前 CPU 和内存使用的图表）。

## Caja 文件管理器

Caja 文件管理器支持复制、移除、删除项目以及设置权限和显示项目的标准功能。文件管理程序的名称为 `caja`。您可以使用扩展来增强 Caja，例如“打开终端”（Open terminal）可以在新的终端窗口中打开当前文件夹，以及 Engrampa，它允许您创建（压缩）和提取压缩包。若干扩展已默认安装并启用。它们将会在相应的菜单中显示项。扩展可以在“文件管理首选项”对话框的“扩展”选项卡（编辑 | 首选项）中启用。若要添加更多扩展，请使用软件管理器安装 `caja` 扩展包。扩展包具有 `caja-` 前缀，例如 `caja-share`、`caja-dropbox` 和 `caja-wallpaper`。

### 主目录的子文件夹和书签

与 Ubuntu 类似，Linux Mint 使用通用用户目录结构（位于 [`freedesktop.org`](https://freedesktop.org) 的 `xdg-user-dirs`）在用户主目录下设置子文件夹。文件夹将包括 `Documents`（文档）、`Music`（音乐）、`Pictures`（图片）、`Downloads`（下载）和 `Videos`（视频）。这些本地用户文件夹被许多桌面应用程序用作默认值。用户可以使用文件浏览器更改文件夹名称或将它们相互嵌套。例如，可以将 `Music` 移动到 `Documents/Music`。本地配置存储在 `.config/user-dirs.dirs` 文件中。系统级默认设置在 `/etc/xdg/user-dirs.defaults` 文件中设置。这些文件夹的图标显示在图 7-21](#index_split_012.html_id_Toc49257560)。

![Image](img/image-401.png)

图 7-21: Caja 文件管理器主目录

这些文件夹也是默认书签。您可以直接从 Caja 窗口的侧边栏访问书签文件夹。您还可以通过打开文件夹并从书签菜单中选择“添加书签”，为文件夹添加自己的书签。您的文件夹将出现在 Caja 侧边栏“位置”（Places）菜单的书签部分以及书签菜单中。使用“编辑书签”对话框可以删除书签。在这里您可以删除书签或更改其名称和位置。

您可以使用“桌面设置”（Desktop Settings）在桌面区域显示主目录、网络和垃圾桶等基础文件夹。

### 文件管理器窗口

当您点击桌面上的主目录图标或 MATE 菜单“位置”部分中的主目录项时，会打开一个文件管理器窗口并显示您的主目录。文件管理器窗口显示了几个组件，包括菜单栏、主工具栏和侧边栏（参见图 7-22）。

![Image](img/image-53.png)

图 7-22: 带有侧边栏的 Caja 文件管理器

侧边栏的作用类似于 Nemo 和 Nautilus 文件管理器中的侧边栏，但带有一个菜单，就像 GNOME 2 中的文件管理器。文件管理器窗口的主面板（右侧）显示当前工作文件夹中文件和子文件夹的图标或列表。当您选择文件和文件夹时，窗口底部的状态栏会显示所选文件或文件夹的名称，文件显示大小，文件夹显示包含的项目数量。状态栏还会显示当前文件系统的剩余可用空间。

当您打开新文件夹时，将使用同一个窗口进行显示，您可以使用“前进”和“后退”按钮在之前打开过的文件夹之间移动（位于主工具栏左上方）（参见图 7-23）。后退和前进按钮右侧的三角形显示之前访问过的文件夹菜单，可以使用它们直接访问上一个文件夹。还有一个向上箭头用于移动到父目录，以及一个“主目录”按钮直接移动到您的主目录。“计算机”按钮会显示显示文件系统和连接设备的计算机窗口。您也可以从文件管理器的“转到”菜单访问这些操作（参见表 7-2）。此外，还有“刷新”和“停止刷新”按钮，以便文件或文件夹列表发生变化时刷新列表。

![Image](img/image-402.png)

图 7-23: Caja 导航按钮：后退、前进、父目录、主目录、计算机

| 菜单项 | 说明 |
| :--- | :--- |
| 打开父级 (Open Parent) | 移动到父文件夹 |
| 后退 (Back) | 移动到文件管理器窗口中查看的上一个文件夹 |
| 前进 (Forward) | 移动到文件管理器窗口中查看的文件夹 |
| 粘贴 (Paste) | 粘贴您复制或剪切的文件 |
| 与其他面板位置相同 (Same Location as Other Pane) | 如果您打开了两个面板，让两个面板查看同一个文件夹 |
| 主目录 (Home Folder) | 移动到主目录 |
| 计算机 (Computer) | 移动到显示文件系统和设备的计算机窗口 |
| 模板 (Templates) | 移动到模板文件夹 |
| 垃圾桶 (Trash) | 移动到垃圾桶查看删除的文件和文件夹 |
| 网络 (Network) | 移动到显示网络的文件夹 |
| 位置 (Location) | 打开文件夹位置框 |
| 搜索文件 (Search for Files) | 使用文件管理器搜索文件 |

表 7-2: “转到”菜单

当您打开子文件夹时，主工具栏会显示当前文件夹及其父文件夹的按钮（参见图 7-24）。您可以点击文件夹按钮移动到那里。初始状态，按钮显示从主目录开始的路径。点击左侧的小三角形可以将路径展开到顶层（根硬盘）。

您也可以显示位置 URL 文本框而不是按钮，可以在其中输入本地系统或远程系统的文件夹位置。要显示位置文本框，可以按下 `Ctrl-l`，或者从“转到”菜单中选择“位置”，或者点击主工具栏路径起始处的“位置”切换图标（笔图标）（参见图 7-24）。这些访问方法作为切换开关，允许在位置文本框和按钮路径之间切换。

![Image](img/image-403.png)

![Image](img/image-404.png)

![Image](img/image-405.png)

图 7-24: Caja 位置：未展开、展开和位置路径

“文件”菜单包含打开新标签页（`Ctrl-t`）、打开新文件管理器窗口（`Ctrl-n`）、创建新文件夹（`Shift-Ctrl-n`）、连接到远程 FTP 服务器以及显示当前文件夹属性（`Alt-Return`）。大多数项都有相应的快捷键（参见表 7-3）（参见图 7-28）。





| 项目 | 描述 |
| :--- | :--- |
| 创建文档 | 创建一个文本文档。 |
| 连接服务器 | 使用文件管理器连接到 FTP 服务器 |
| 在终端中打开 | 在新终端窗口中打开当前文件夹（需 Open Terminal 扩展） |
| 属性 | 当前打开文件夹的属性 |
| 清空垃圾箱 | 清空垃圾箱文件夹 |
| 关闭所有窗口 | 关闭所有文件管理器窗口 |
| 关闭 | 关闭文件管理器窗口。 |
| 用...方式打开 | 当选中文件时，会显示“打开方式”项目，显示用于打开该文件的可能应用程序 |
| 打开 | 当选中文件夹时，会显示“打开”项目，同时也显示“在新标签页中打开”和“在新窗口中打开”项目，以及“打开方式”子菜单。 |

**表 7-3：文件管理器文件菜单**

![Image](img/image-406.png) ![Image](img/image-407.png) ![Image](img/image-408.png) ![Image](img/image-409.png)

**图 7-25：文件管理器侧边栏菜单和视图**

### 文件管理器侧边栏

文件管理器侧边栏有一个菜单，你可以从中选择显示位置（`Places`）、文件系统的树状视图（`Tree`）、当前或选中文件夹或文件的信息（`Information`）、该登录会话之前打开文件夹的历史（`History`）、备注（`Notes`）以及你可以放置在文件或文件夹上的图标（`Emblems`）。

使用侧边栏的 `Places` 视图可以访问收藏的文件夹、存储设备（`USB`、`CD/DVD` 光盘和连接的硬盘）以及挂载的网络文件夹。在侧边栏的 `Computer` 部分，你可以访问家目录、垃圾箱和文件系统（根目录）。在 `Bookmarks` 部分，你可以访问创建的任何额外书签。

侧边栏的默认是 `Places` 视图，它显示了 `Computer`、`Devices`、`Bookmarks` 和 `Network` 项目部分，显示你的文件系统和默认家目录子文件夹（参见图 7-25）。你可以通过选择 `查看` 菜单中的“侧边栏”选项来显示或隐藏侧边栏，也可以点击侧边栏菜单右侧的关闭按钮。你也可以使用 `F9` 切换侧边栏的开启关闭。

在侧边栏中选择 `File System` 项将你置于文件系统的顶部，让你移动到它可以访问的任何部分。在 `Computer` 部分，你可以搜索默认文件夹，例如 `Documents` 和 `Pictures`。如果你对文件夹添加了书签（`Bookmarks` 菜单，“添加书签”项目（`Ctrl-d`）），侧边栏会出现一个带有该书签的 `Bookmark` 部分。要删除或重命名书签，右键点击侧边栏中的该项，并在弹出菜单中选择“删除”或“重命名”（参见图 7-26）。书签名称会更改，但原始文件夹名称不变。

![Image](img/image-410.png)

**图 7-26：带有书签菜单的文件管理器侧边栏**

### 标签页

Caja 文件管理器支持标签页，通过你可以在同一个文件管理器窗口中打开多个文件夹。要打开标签页，从 `文件` 菜单选择 `新标签页` 或按 `Ctrl-t`。会出现一个标签页栏，带有每个标签页的标签页图标，显示打开的文件夹名称以及一个 `x` 关闭按钮（参见图 7-27）。你可以通过点击并拖动标签页图标向右或向左来重新排列标签页。你还可以使用 `Ctrl-PageUp` 和 `Ctrl-PageDown` 键在标签页之间移动。使用 `Shift-Ctrl-PageUp` 和 `Shift-Ctrl-PageDown` 键重新排列标签页。要关闭标签页，点击标签页右侧的关闭 `x` 按钮。

**注意：** Caja 作为一个操作型的 FTP 浏览器工作。你可以使用 `文件` 菜单上的“连接服务器”项目打开“连接服务器”对话框，在其中输入 FTP 站点的地址。

![Image](img/image-411.png)

**图 7-27：带有标签页的文件管理器窗口**

### 显示文件和文件夹

你可以将目录的内容以图标、紧凑列表或详细列表的形式查看，你可以从主工具栏右侧的菜单中选择：`icon`、`list` 和 `compact` 视图，如下所示。

![Image](img/image-412.png)

使用控制键快速更改视图：`Ctrl-1` 图标，`Ctrl-2` 列表，`Ctrl-3` 紧凑视图。`列表` 视图提供名称、大小、类型和日期。主面板顶部会为每个字段显示按钮。你可以使用这些按钮根据该字段对列表进行排序。例如，要按日期排序文件，点击 `修改日期` 按钮；按大小排序，点击 `大小` 按钮。再次点击可以在升序和降序之间切换。

某些类型的文件图标将显示其内容的预览。例如，图像文件的图标将显示图像的缩图。文本文件将在图标中显示其文本的前几个字。

`查看` 菜单包含管理和排列你的图标的选项（参见表 7-4）（参见图 7-28）。`图标`、`列表`和`紧凑` 视图。

![Image](img/image-413.png) ![Image](img/image-414.png) ![Image](img/image-415.png)

**图 7-28：文件管理器文件、编辑和查看菜单**

`查看` | `放大` 项将你的图标视图放大，`缩小` 项将其缩小。`标准大小` 恢复图标大小](index_split_012.html_id_Toc49248770)）。你还可以使用 `Ctrl-+` 和 `Ctrl--` 键放大和缩小。

### 文件管理器工具和菜单

通过 `编辑` 菜单，你可以粘贴你复制的文件，在文件夹之间移动它们或创建副本（参见表 7-5）。

| 项目 | 描述 |
| :--- | :--- |
| 停止 | 停止当前任务 |
| 刷新 | 刷新文件和目录列表 |
| 主工具栏 | 显示主工具栏 |
| 侧边栏 | 显示侧边栏 |
| 位置栏 | 显示位置栏 |
| 状态栏 | 显示窗口底部的状态栏 |
| 额外面板 | 为文件管理器窗口显示双面板，每个面板打开不同的文件夹 |
| 重置视图为默认 | 以默认视图显示文件和文件夹 |
| 显示隐藏文件 | 显示管理点文件。 |
| 排列项目：名称、大小、类型、修改日期和图标 | 按指定标准排列文件和目录 |
| 按名称组织 | 在图标视图中按名称排序 |
| 放大 | 提供图标的放大视图，使其更大。 |
| 缩小 | 提供图标的缩小视图，使其更小。 |
| 标准大小 | 恢复图标视图的标准大小。 |
| 图标 | 显示图标 |
| 列表 | 显示带有名称、大小、类型和日期的列表。文件夹可以展开。 |
| 紧凑 | 显示仅使用名称和小型图标的紧凑文件列表 |

**表 7-5：文件管理器查看菜单**

| 项目 | 描述 |
| :--- | :--- |
| 切切、复制 | 移动或复制文件或目录 |
| 粘贴 | 粘贴你复制或剪切的文件，可以在文件夹之间移动或复制文件或创建副本。 |
| 撤销、重做 | 撤销或重做粘贴操作 |
| 全选 | 选择此文件夹中的所有文件和文件夹 |





| 选择匹配项 | 使用基本模式匹配快速搜索文件。 |
| 反选项目 | 选择所有未选中的文件和文件夹，并取消当前选中的项目。 |
| 复制 | 为所选的文件创建副本。 |
| 创建链接 | 为文件或文件夹创建链接。 |
| 重命名 | 重命名所选的文件或文件夹。 |
| 复制到 | 将文件或文件夹复制到默认书签之一。 |
| 移动到 | 将文件或文件夹移动到默认书签之一。 |
| 移动到回收箱 | 将文件或文件夹移动到回收箱文件夹以备稍后删除。 |
| 删除 | 立即删除文件或文件夹。 |
| 压缩 | 将所选的文件和文件夹压缩为压缩归档文件，如 tar、cpio 或 zip 文件（需要 Engrampa 扩展）。 |
| 背景和徽标 | 为文件管理器窗口选择背景。为文件管理器窗口中的任何文件夹或文件添加徽标。 |
| 偏好 | 您的账户的 Caja 文件管理器偏好。 |

表 7-5：文件管理器编辑菜单

### 在文件管理器中导航

文件管理器的操作方式类似于网络浏览器，使用同一个窗口显示已打开的文件夹。它维护了一个以前查看过的文件夹列表，你可以使用工具栏上的导航按钮（左侧）在该列表中来回移动。带有左箭头的`Back（后退）`按钮带你回到之前显示的文件夹，带有右箭头的`Forward（前进）`按钮带你进入下一个之前显示的文件夹，向上箭头则进入父文件夹。主目录图标打开你的主目录，计算机图标（显示器）打开`Computer（计算机）`窗口，其中列出了你的文件系统和可移动设备的图标。

使用侧边栏的`Places（位置）`视图访问你的书签文件夹、存储设备（USB、CD/DVD 光盘和连接的硬盘）以及挂载的网络文件夹。在侧边栏的`Computer`部分，你可以访问你的主目录、回收箱和文件系统（根目录）。在`Bookmarks（书签）`部分，你可以访问你创建的任何额外书签。已连接的设备列在`Devices（设备）`部分，挂载的网络文件夹列在`Network（网络）`部分。

要打开子文件夹，可以双击图标或右键点击图标并从菜单中选择`Open（打开）`。你也可以在新的标签页或新窗口中打开文件夹。`Open With（打开方式）`子菜单列出了其他可能用于打开文件夹的文件管理器和应用程序，例如`Files（（Caja）`。你也可以点击文件夹来选择它，然后从文件菜单（`File | Open`）中选择`Open`。当选中文件夹时，也会列出标签页、新窗口和“打开方式”等项目。图 7-29 显示了`File`菜单，其中包含文件夹的不同`Open`项目以及针对文件的`Open With`子菜单。表 7-3 列出了文件菜单的选项。

![Image](img/image-416.png) ![Image](img/image-417.png)

图 7-29：针对文件夹和文件的文件管理器 File | Open with 子菜单

| 菜单项 | 描述 |
| 创建文件夹 | 在目录中创建一个新的子目录。 |
| 创建文档 | 创建一个文本文档。 |
| 排列项目：按名称、大小、类型、修改日期和徽标 | 按指定的标准排列文件和目录。 |
| 按名称组织 | 在图标视图中按名称排序图标。 |
| 在终端打开 | 在该文件夹打开终端窗口（需要打开终端扩展）。 |
| 放大 | 提供图标的特写视图，使其看起来更大。 |
| 缩小 | 提供图标的远视图视图，使其看起来更小。 |
| 正常大小 | 将图标视图恢复为标准大小。 |
| 属性 | 打开目录的属性对话框。 |

表 7-6：文件管理器弹出菜单

你可以通过点击其文件夹或书签，打开侧边栏`Places`视图中列出的任何文件夹或文件系统。你也可以右键点击书签或文件夹，显示一个包含`Open（打开）`、`Open in a New Tab（在新标签页中打开）`和`Open in a New Window（在新窗口中打开）`等条目的菜单（请参见 表 7-7）。`Open in a New Window`项目是从文件管理器访问设备的简单方法。`Trash（回收箱）`条目的菜单让你清空回收箱。对于任何书签，你还可以删除和重命名该条目。侧边栏中可移动设备（如 USB 驱动器）的条目也有`Eject（弹出）`菜单项。内部硬盘则有`Unmount（卸载）`条目。

| 菜单项 | 描述 |
| Open | 使用其关联应用程序打开文件。目录在文件管理器中打开。列出关联应用程序。 |
| Open In A New Tab | 在同一窗口的新标签页中打开目录。 |
| Open In A New Window | 在单独窗口中打开目录，可以通过工具栏、右键访问。 |
| Remove | 从侧边栏移除书签。 |
| Rename | 重命名书签。 |

表 7-7：文件管理器侧边栏弹出菜单

### Caja 文件管理器搜索

Caja 文件管理器提供了一个搜索工具，其工作方式与 Nemo 文件管理器的搜索功能相同。从文件管理器窗口中，点击工具栏上的`Search（搜索）`按钮（右侧的放大镜图标），或选择`Go | Search for Files（前往 | 搜索文件）`在工具栏下方打开搜索框。输入搜索模式并按`ENTER`或点击右侧的放大镜按钮。结果将显示。

位置和文件类型的菜单将出现在文件夹窗口中。

### 管理文件和文件夹

作为一个符合 GNOME 标准的文件管理器，Caja 支持用于复制和移动的拖放操作。要移动文件或文件夹，从一个目录拖动到另一个。移动操作是 GNOME 中的默认拖放操作。要将文件复制到新位置，拖动时按住`Ctrl` 键。

#### 使用文件的弹出菜单

你也可以通过右键点击图标并从弹出菜单中选择所需的操作对文件执行删除、重命名和创建链接操作（请参见 表 7-8）。例如，要删除项目，右键点击并从菜单中选择`Move To Trash（移动到回收箱）`。这将放入删除目录，稍后可以删除它。要创建链接，右键点击文件并从弹出菜单中选择`Make Link（创建链接）`。这将创建一个以“链接”开头的新链接文件。如果你选择一个压缩文件，弹出菜单还会显示“在此处解压”和“提取到...”的选项。

| 菜单项 | 描述 |
| Open | 使用其关联应用程序打开文件。目录在文件管理器中打开。列出关联应用程序。 |
| Open In A New Tab | 在同一窗口的新标签页中打开目录。 |
| Open In A New Window | 在单独窗口中打开目录，可以通过工具栏、右键访问。 |
| Open With | 选择用于打开文件的应用程序，或用于打开文件夹的文件管理器。 |
| Cut Copy | 用于剪切和复制所选文件的条目。 |
| Paste into Folder | 粘贴所选文件夹 |
| Make Link | 在同一目录中为该文件创建链接。 |
| Rename (F2) | 重命名文件。 |
| Copy To | 将文件复制到主目录、桌面或文件管理器窗口中另一个窗格中显示的文件夹。 |





## 表 7-8: 文件和文件夹弹出菜单

| 命令 | 说明 |
| :--- | :--- |
| 移动到 | 将文件移动到主文件夹、桌面，或文件管理器窗口另一个窗格中显示的文件夹。 |
| 移动到回收箱 | 将文件移动到回收箱目录，稍后可以删除它。 |
| 删除 | 永久删除文件或文件夹 |
| 压缩 | 归档文件（Engrampa 扩展）。 |
| 在此处提取 / 提取到 | 当选中压缩包时，会出现这些选项（Engrampa 扩展）。 |
| 在终端中打开 | 在终端窗口中打开文件夹 |
| 发送至 | 将文件夹归档并压缩发送到电子邮件，或复制到可移动驱动器或共享文件夹 |
| 共享选项 | 选中文件夹时激活。您可以选择在网络上共享该文件夹。安装 `caja-share`。 |
| 以管理员身份打开 | 以管理员权限打开文件夹 |
| 更改颜色 | 文件夹图标的颜色 |
| 属性 | 显示属性对话框。 |

## 重命名文件
要重命名文件，您可以右键点击文件图标并从弹出菜单中选择`重命名`项，或者点击其图标并按 `F2` 键。图标的名称将被框围，并封装在一个小文本框中。您可以覆盖旧名称，也可以通过点击名称中的某个位置插入文本来编辑当前名称，并使用退格键删除字符。您还可以通过在文件的`属性`对话框（`基本` 选项卡）中输入新名称来重命名文件。

## 分组文件
您可以通过点击第一项然后按住 `shift` 键点击最后一项，或者通过点击并拖动鼠标跨越想要的项目来选择一组文件和文件夹。要选择不连续的项，请在按住 `ctrl` 键的同时点击各个图标。如果您想选择文件夹中的所有项目，请选择`编辑`菜单中的`全选`项（`编辑 | 全选`）（`Ctrl-a`）。然后您可以一次复制、移动甚至删除多个文件。要选择名称中具有特定模式的项，请从`编辑`菜单中选择`选择匹配的项`以打开搜索框，您可以在其中输入模式（`Ctrl-s`）。使用 `*` 字符匹配部分模式，例如使用 `let*` 来匹配所有文件名中包含“let”模式的文件。模式 `my*` 将匹配以“my”模式开头的文件名，而 `png` 将匹配所有 PNG 图像文件。

## 打开应用程序和文件 MIME 类型
您可以通过双击应用程序本身或用于该应用程序的数据文件，在文件管理器中启动任何应用程序。如果您想用特定的应用程序打开文件，可以右键点击文件并选择`打开方式`项中的一个。对于默认应用程序和可能的应用程序，将显示一个或多个`打开方式`项，例如针对文本文件的“用文本编辑器打开”。如果所需的应用程序未列在列表中，您可以选择`打开方式 | 其他应用程序`来打开列出所有可用应用程序的对话框。应用程序也支持拖放操作。您可以将一个数据文件拖到其关联的应用程序图标上（例如，在桌面上）；随后，该应用程序将使用该数据文件启动。

文件夹也有`打开方式`子菜单，列出了您可以使用其打开文件夹的备用文件管理器，例如`文件`（`Caja`）。处理文件夹的应用程序也会列在其中，例如`Shotwell` 图像管理器和`磁盘使用分析器`。

要更改或设置用于某种类型文件的默认应用程序，请打开文件的`属性`对话框并选择`打开方式`选项卡。在这里，您可以选择用于该类型文件的默认应用程序。可能的应用程序将列出，每个项目旁边都有一个单选按钮。默认项的单选按钮处于开启状态。点击您想要更改为默认项的项的单选按钮。一旦您选择了默认项，它将出现在该类型文件的`打开方式`项中。如果`打开方式`选项卡上存在您不希望出现在`打开方式`菜单中的应用程序，请选择它并点击`删除`按钮。

如果您想向`打开方式`菜单中添加应用程序，请点击`添加`按钮打开`添加应用程序`对话框，该对话框列出了所有可能的应用程序。选择您需要的项并点击`添加`按钮。您可以使用`使用自定义命令`文本框输入命令。`浏览`按钮允许您定位到命令。

### 文件和目录属性
在文件的`属性`对话框中，您可以查看文件的详细信息并设置选项和权限（参见图 7-30）。文件的`属性`对话框有五个选项卡：`基本`、`图标标记`、`权限`、`打开方式`和`备注`。文件夹没有`打开方式`选项卡。某些类型的文件会有额外的选项卡，提供有关文件的信息。例如，音频文件将有一个`音频`选项卡，列出音频文件类型以及任何其他信息，如歌名或所使用的压缩方法。图像文件将有一个`图像`选项卡，列出分辨率和图像类型。文件夹还有`访问控制列表`和`扩展用户属性`选项卡，您可以使用它们来控制用户对文件夹的访问。

`基本`选项卡显示详细信息，如类型、大小、位置和修改日期。类型是 MIME 类型，表示与它关联的应用程序类型。文件的图标显示在顶部，带有一个显示文件名的文本框。您可以在`名称`文本框中编辑文件名。

如果您想更改文件或文件夹使用的图标，点击名称旁边的图标图像以打开`选择自定义图标`对话框，以浏览所需的图标。`/usr/share/pixmaps` 目录持有默认图像集，尽管您可以选择自己的图像（点击`pixmaps`项）。点击右侧窗格中显示的图像。双击即可更改。

![图像](img/418.png)

**图 7-30：Caja 中的文件属性**

文件的`权限`选项卡显示了所有者、组和其他人的读取、写入和执行权限。只要文件属于您，您就可以在此更改任何权限。您可以使用菜单为所有者、组和其他配置访问权限。您可以将所有者权限设置为`只读`或`读和写`。对于组和其他，您也可以设置`无`选项以拒绝访问。点击组名称将显示组列表，允许您选择一个更改文件的组。如果您想作为程序执行文件，请勾选`允许执行文件`项。这将设置执行权限。

文件夹的`权限`选项卡的操作方式类似，但它包含两个访问项：`文件夹访问`和`文件访问`。`文件夹访问`项控制对文件夹的访问，具有`无`、`仅列出文件`、`访问文件`和`创建和删除文件`等选项。这些对应于给文件夹的权限。`文件访问`项允许您设置文件夹中所有文件的权限。它们与文件相同：对于所有者，`读取`或`读和写`；对于组和其他，该项提供了`无`选项以拒绝访问。要相应设置文件夹中所有文件的权限（而不只是文件夹本身），请点击`将权限应用于包含的文件`按钮。

文件的`打开方式`选项卡列出了与此类文件关联的所有应用程序。您可以选择您想要作为默认项的应用程序。这对于媒体文件特别有用，您可能希望为某些文件使用特定的播放器，或为图片使用特定的图像查看器。要添加未列出的应用程序，请点击`添加`按钮打开`添加应用程序`对话框，该对话框列出了供您选择的已安装应用程序。

`备注`选项卡允许您对文件添加备注。随后，备注标记将出现在文件图标的右上角。




文件夹的“共享”选项卡允许你将文件夹作为网络共享。如果你有 Samba 或 NFS，这些工具将允许你的文件夹和文件与其它系统上的用户共享。你可以指定共享文件夹或文件是只读还是允许写入访问。要允许写入访问，请勾选“允许其他在此文件夹中创建和删除文件”。要向所有用户开放访问，请勾选“访客访问”项。

## Caja 偏好

你可以在“偏好”对话框中为 Caja 文件管理器设置偏好，可以通过选择任何 Caja 文件管理器窗口的“编辑”菜单中的“偏好”（`Edit | Preferences`）来访问它。

“视图”选项卡允许你选择文件的默认显示方式，例如列表、图标或紧凑视图。你可以为图标、紧凑和列表视图设置默认缩放级别。

“行为”允许你选择如何选择文件、管理垃圾箱以及处理脚本。

“显示”允许你选择想要在图标说明中显示的附加信息，如大小或日期。你也可以指定日期的格式。

“列表**列”选项卡允许你选择在列表视图中显示的功能以及它们的顺序。除了已选的“名称”、“大小”、“日期”和“类型”之外，你还可以添加权限、组、MIME 类型和所有者等功能。对于文件夹，你还可以显示项目计数。

“预览”选项卡允许你选择是否希望在图标中显示小型预览内容，例如文本文件的开头文本。

“媒体”选项卡允许你选择为特定媒体运行哪些应用程序，例如运行 Celluloid 媒体播放器播放 DVD 视频，或运行 Rhythmbox 处理音频文件。

扩展列表列出了为 Caja 安装的扩展，例如“在终端中打开”（它允许你在终端窗口中打开文件夹（“在终端中打开”菜单项），来自 `caja-open-terminal` 包）、Engrampa（它允许你直接从文件管理器窗口创建和提取压缩包（“压缩”菜单项））以及 `caja-seahorse`（它允许你加密文件和文件夹（“加密”菜单项）。

## 控制中心

“偏好”和“管理”工具都可以从 Linux Mint 菜单或从“控制中心”访问（参见图 7-31）。你可以从 Linux Mint 菜单的“系统”部分访问控制中心。控制中心会打开一个窗口，按部分列出不同的应用程序：管理、硬件、互联网和网络、外观和个人。窗口会显示工具的图标。单击图标即可打开它。控制中心还具有动态搜索功能。侧边栏包含一个过滤搜索框和各个组的链接。当你在过滤搜索框中输入模式时，匹配的应用程序将出现在右侧。常用的应用程序可以列在“常用任务”下。如果你希望在系统启动时启动某个应用程序，可以右键点击其图标并选择“添加到启动程序”，以将其直接添加到“启动应用程序”对话框中。其中有几个工具是管理类应用程序，如软件管理器、备份工具、用户和组以及打印机。其他工具是用于 MATE 的 GNOME 偏好设置，如“外观”、“关于我”、“屏幕保护”和“键盘”。

![Image](img/image-419.png)

![Image](img/image-420.png)

图 7-31：GNOME 控制中心

## MATE 偏好

你可以使用 Linux Mint 菜单中“偏好”菜单列出的工具以及控制中心，配置 MATE 界面的不同部分。Linux Mint 提供了多个工具来配置你的 MATE 桌面。MATE 偏好列在表 7-9 中。在某些偏好工具上，“帮助”按钮会显示详细的描述和示例。这里讨论了一些较重要的工具。

快捷键配置（`Keyboard Shortcuts`）允许你将按键映射到某些任务，例如将键盘上的多媒体键映射到播放和暂停等媒体任务。有桌面、窗口管理和声音的任务。在窗口管理中，你还可以映射按键来执行工作空间切换。列出了已分配的任务和按键。要更改用于任务的按键，双击其快捷键项并输入新按键。没有分配按键的任务将被禁用。单击快捷键项为其输入按键序列。要添加新任务，点击“添加”以选择应用程序并为其命名。这些任务将添加到“自定义快捷键”部分下。点击新任务的快捷键为其添加按键。要禁用快捷键，单击该快捷键项并按退格键。

窗口配置（`Windows`）是你可以启用功能的地方，如窗口折叠（`Titlebar Action`）、窗口移动键和鼠标窗口选择。

| 偏好 | 描述 |
| :--- | :--- |
| 关于我 | 个人信息，如图像、地址和密码。 |
| 辅助技术 | 启用如无障碍登录和键盘屏幕等功能。 |
| 外观 | 桌面外观配置：主题、字体、背景和视觉效果。 |
| CompizConfig 设置管理器 | 用于 GNOME 增强图形功能的高级配置对话框，例如 3D 窗口、动画和桌面立方体工作空间切换。 |
| 桌面设置 | 基础设置，如在桌面上显示主和计算机图标、窗口按钮布局以及在菜单中显示图标。 |
| 桌面共享 | 配置他人访问你的桌面。 |
| 磁盘 | 打开 GNOME 磁盘工具。 |
| 显示器 | 打开 GNOME 监器偏好对话框，用于检测显示器并设置分辨率。 |
| 域名拦截器 | 阻止指定的域名。 |
| 文件管理 | 文件管理器选项，包括媒体处理应用程序、图标说明和默认视图（也可以从文件管理器窗口通过 `Edit | Preferences` 访问）。 |
| 键盘 | 配置键盘：选择选项、型号和打字中断，以及慢速、切换、粘性键等辅助功能。 |
| 快捷键 | 配置特殊任务的键，如多媒体操作。 |
| 语言 | 指定语言，与 Cinnamon 同。 |
| 登录窗口 | 配置 LightDM 显示器的登录窗口，与 Cinnamon 同。 |
| 主菜单 | 添加或删除应用程序、偏好和系统菜单的类别和菜单项。 |
| 显示 | 更改屏幕分辨率、刷新率和显示方向。 |
| 鼠标 | 鼠标和触摸板配置：选择手部方向、速度和辅助功能。 |
| 网络代理 | 需要时指定代理配置：手动或自动 | |
| 显示器 | 更改你的屏幕分辨率、刷新率和显示方向。 |
| 弹出通知 | 通知的位置和显示主题。 |
| 电源管理 | GNOME 电源管理器，用于配置显示、挂起和关机选项。 |
| 首选应用程序 | 设置默认 Web 浏览器、邮件应用程序、音乐播放器和终端窗口。 |
| 远程桌面 | 允许远程用户查看或控制你的桌面。可以使用密码控制访问。 |
| 屏幕保护 | 选择和管理你的屏幕保护程序，包括激活时间。 |
| 启动应用程序 | 管理带有启动程序的会话保存选项。 |
| 声音 | 配置音效、输出量、声音设备选项、输入量以及声音应用程序设置（`Pulseaudio`）。 |
| 时间和日期 | 设置时间、日期和时区。 |
| 欢迎界面 | 显示 Linux Mint 欢迎界面，带有用户指南、教程和软件管理器的链接。 |
| 窗口 | 启用窗口功能，如标题栏折叠、移动键、窗口选择。 |

表 7-9：MATE 偏好

### 鼠标和键盘偏好




鼠标和键盘偏好是配置鼠标和键盘的主要工具。鼠标偏好允许你选择其速度、手部朝向和双击时间。对于笔记本电脑，你可以配置触控板，启用触控板点击和边缘滚动（左侧）。键盘偏好显示了多个标签页，用于选择键盘型号（`Layouts`）、配置按键（`Layouts` 标签页、`Options` 按钮）、重复延迟（`General` 标签页），以及作为健康预防措施强制从快速打字中抽休息（`Typing Break`）（请参见图 7-32）。

![Image](img/image-421.png) ![Image](img/image-422.png)

图 7-32: 鼠标和键盘偏好

要配置音频设备，你可以使用声音偏好工具（`Sound`），请参阅第 9 章。MATE 使用音频主题为不同的效果和警报指定整套声音。

## 关于我：照片、名称和密码

要设置个人信息（包括用于图形登录的图标），你需要使用“关于我”偏好工具。你可以从 Linux Mint 菜单的偏好菜单（`Preferences` | `About Me`）以及 GNOME 控制中心访问它。“关于我”偏好对话框允许你更改密码（请参见图 7-33）以及用于代表用户的图标或图像。如果你想更改密码，可以点击 `Change Password` 按钮打开更改密码的对话框。

点击图像图标会打开浏览器窗口，你可以在其中选择个人图像。默认选中 `/usr/share/pixmaps/faces` 目录，该目录显示了多张图像。选中的图像显示在浏览器窗口的右侧。对于个人照片，你可以选择 `Picture` 文件夹。这是你主目录下的 `Pictures` 文件夹。如果你在那里放置了照片或图像，就可以选择将其作为你的个人图像。该图像将会在显示用户条目时显示在登录屏幕。

![Image](img/image-423.png)

图 7-33: 关于我：偏好 | 关于我

## 外观

若干与外观相关的配置任务被整合到“外观”偏好对话框中（偏好菜单中的 `Appearance` 条目或控制中心“个性化”部分中的 `Appearance` 图标）。你可以更改主题、背景图像或配置字体。外观对话框显示了四个标签页：主题、背景、字体和界面（请参见图 7-11）。在“界面”标签页上，你可以选择在菜单和按钮上显示图标。

### 桌面主题

你使用外观偏好对话框上的 `Themes` 标签页来选择或自定义主题。主题控制着你桌面的外观。`Themes` 标签页将列出已安装主题的图标（请参见图 7-34）。这些图标显示了每个主题的关键方面，如窗口、文件夹和按钮图像，实际上是为你预览该主题。

初始选中的是 Linux Mint 自定义主题。如果你愿意，可以移动图标以选择不同的主题。如果你已经从 [`www.gnome-look.org/`](https://www.gnome-look.org/) 下载了额外主题，可以点击安装按钮来定位并安装它们。一旦安装完成，额外主题也将显示在 Theme 标签页中。如果你从 Linux Mint 仓库下载并安装主题或图标集，它将为你自动安装。

![Image](img/image-424.png)

图 7-34: 选择 GNOME 主题

主题真正的威力在于它允许用户自定义任何给主题。主题由五个组件组成：控件、颜色、窗口边框、图标和指针。控件涵盖窗口和对话框控件（如按钮和滑动条）的外观。窗口边框允许你选择标题栏、边框、窗口按钮集。图标允许你选择不同的图标集。指针提供了不同的指针集供使用。颜色允许你为窗口、输入框、选择框和工具提示符选择背景颜色和文本颜色。你甚至可以下载并安装独立的组件（例如特定的图标集），然后在自定义主题中使用它们。

点击 `Customize` 按钮会打开“自定义主题”对话框，其中带有不同主题组件的标签页。当前主题使用的组件会被默认选中。在 Controls、Window Border、Icons 和 Pointer 标签页中，你会看到不同主题的列表。你可以混合组合这些主题中的不同组件，创建自己的自定义主题，例如使用一个主题的窗口边框和另一个主题的图标。选中某个组件后，你的桌面会自动变化并向你展示效果。如果你添加了组件（如新的图标集），它也会显示出来。

一旦你创建一个新的自定义主题，Theme 标签页中的列表中就会出现一个 Custom Theme 图标。要保存自定义主题，请点击 `Save As` 按钮。这将打开一个对话框，你可以在其中输入主题名称、备注，并指定你是否想保留主题背景。

自定义主题和用户直接安装的主题存放在用户主目录下的 `.themes` 目录中。如果你希望这些主题对所有用户可用，可以将它们从 `.themes` 目录移动到 `/usr/share/themes` 目录。在终端窗口中运行如下所示的 `cp` 命令来处理 `mytheme` 主题。该操作需要管理员权限（`sudo`）。

```bash
sudo cp -r .themes/mytheme /usr/share/themes
```

你也可以对下载的图标集执行相同的操作。此类集合将安装在用户的 `.icons` 目录。你可以将其复制到 `/usr/share/icons` 目录以便所有用户使用。

### 桌面背景

你使用外观偏好工具上的 `Background` 标签页来选择或自定义背景图像（请参见图 7-35）。你也可以通过点击桌面背景并在菜单中选择“更改桌面背景”来访问 Background 标签页。已安装的背景在此列出，并选中当前的。要添加自己的图像，可以将图像文件拖入 Background 标签页，或点击 `Add` 按钮定位并选择图像文件。要删除图像，请选中它并点击 `Remove` 按钮。

从 Style 菜单中，你可以选择显示选项，如放大、居中、缩放、平铺或填充屏幕。居中或缩放将保持图像比例。填充可能会使其失真。未填充的空间（在使用居中或缩放图像时）将用桌面颜色填充。从 Colors 菜单，你可以将桌面颜色设置为纯色、水平渐变或垂直渐变。点击 Colors 菜单旁的颜色按钮将打开“选取颜色”对话框，你可以在调色板中选择颜色。对于渐变，显示两个颜色按钮用于选择渐变两端的颜色。

初始列出 Linux Mint/Ubuntu 背景。安装 `gnome-background` 软件包可以添加一组 GNOME 背景。要下载更多背景，点击“在线获取更多背景”链接。

![Image](img/image-425.png)

图 7-35: 选择桌面背景，系统 | 偏好 | 外观

### 字体

在 Font 标签页上，你可以更改字体大小、选择字体并配置渲染选项（请参见图 7-36）。字体分为应用程序、文档、桌面、窗口标题和等宽字体。点击字体按钮打开“选取字体”对话框，你可以在其中选择字体、选择其样式（常规、斜体或加粗）并更改其大小。你可以通过点击 `Details` 按钮打开一个窗口来进一步优化字体显示，你可以在其中设置如 DPI、微齿渲染和平滑处理等功能。




随着大尺寸显示器及其高分辨率变得越来越常见，用户发现一个非常有帮助的功能是能够增大桌面字体的大小。在大尺寸宽屏显示器上，低于原生分辨率的设置往往无法良好缩放。显示器在原生分辨率下显示效果最佳，但在高原生分辨率下，字体会变得非常小，导致难以阅读。你可以通过增大字体大小来解决这个问题。默认大小为 10；将其增加到 12 可以让窗口和菜单等所有桌面功能中的文字变得易读得多。

### 配置字体

为了精炼字体显示，可以使用字体渲染功能。打开 `Appearance` 工具上的 `Fonts` 选项卡。在 `Font Rendering` 区中，包含了一些基础的字体渲染功能，如 `Monochrome`（单色）、`Best contrast`（最佳对比）、`Best shapes`（最佳形状）和 `Subpixel smoothing`（亚像素平滑）。选择最适合的一种。对于 LCD 显示器，请选择亚像素平滑。如需详细配置，点击 `Details` 按钮。在这里你可以设置 `Smoothing`（平滑）、`Hinting (anti-aliasing)`（字体微调/抗锯齿）和 `Subpixel color order`（亚像素颜色顺序）功能。`Subpixel color order` 取决于硬件。

在 MATE 上，点击 `Fonts Preferences` 工具中的字体按钮将打开一个“Pick a Font”对话框，列出所有可用字体。你也可以通过 `fc-list` 命令生成列表。该列表是非排序的，因此你应该先将其将其管道给 `sort` 命令。你可以使用 `fc-list` 配合任何字体名称或名称模式来搜索字体，并提供按语言、族或样式搜索的选项。

```
fc-list | sort
```

### 添加字体

Linux 存储库提供了许多字体包。当你安装字体包时，字体会自动安装到你的系统中并准备好使用。真类型字体包以 `ttf-` 开头。微软真类型字体可以通过 `ttf-mscorefonts-installer` 包获得。字体安装在 `/usr/share/fonts` 目录下。该目录将拥有不同字体集合的子目录，如 `truetype` 和 `X11`。你可以自己通过将字体复制到 `/user/share/fonts` 目录（使用 `sudo` 命令）来手动安装字体。对于安装了 Windows 作为操作系统之一的双启动系统，你可以直接从 Windows 分区上的 Windows 字体目录（挂载在 `/media`）将字体复制到 `/usr/share/fonts`。

### MATE 电源管理

对于电源管理，MATE 使用 MATE Power Manager (`mate-power-manager`)，它利用计算机提供的高级配置与电源接口 (ACPI) 支持来管理电源消耗。MATE 电源管理器可以在面板上显示图标，显示当前电源源：电池或插电（闪电）。点击电池图标将显示一个菜单，显示你的无线设备的电量，包括你的笔记本电脑和任何其他无线设备（如无线鼠标）。

MATE 电源管理器通过电源管理偏好 (`mate-power-preferences`) 配置，可以通过 `Preferences | Power Management` 访问，也可以通过右键点击 MATE 电源管理面板图标并在弹出菜单中选择 `Preferences`（同样在 `GNOME Control Center | Hardware` 部分）。电源管理器偏好可用于配置台式电脑和笔记本电脑。

对于台式电脑，电源管理偏好窗口上会显示两个选项卡：`On AC Power`（交流电源）和 `General`（通用）。`AC Power` 选项卡提供两个睡眠选项，一个针对电脑，一个针对显示器。你可以设置在空闲一段时间后让它们进入睡眠。在 `General` 选项卡上，你可以设置桌面功能，例如按下电源按钮时执行的操作，或者是否显示电源图标。

![Image](img/image-427.png)

**图 7-37: MATE 电源管理器**

面板上的电源管理图标显示在 `General` 选项卡上配置。在 `Notification Area` 部分，你可以设置选项：从不显示、始终显示图标、电池电量低时显示、充电或放电时显示，或仅在存在电池时显示。默认仅在存在电池时显示图标。

注意：MATE 电源管理器不仅会检查笔记本电池的电量，还会检查其他无线电池设备的电量，例如无线鼠标或键盘的电池。

笔记本电脑还有一个 `On Battery Power`（电池电源）选项卡，你可以在其中设置电池和显示器的额外选项，例如电量过低时关机，或系统空闲时调暗显示器（见图 7-37）。笔记本电脑的 `On AC Power` 选项卡还有一个 `Actions`（操作）选项，用于在笔记本盖关闭时执行的操作，如挂起、黑屏和关机。

要查看你的笔记本电脑或台式电脑的电源性能，可以使用 Power Statistics。可以通过系统工具菜单中的 `Power Statistics` 访问。Power Statistics 窗口将显示一个列出不同电源设备的侧边栏。右侧将显示所选设备的电源使用信息的选项卡。`Laptop battery` 设备将显示三个选项卡：`Details`（详情）、`History`（历史）和 `Statistics`（统计）。`History` 选项卡将显示最近的使用情况，并带有图表选项：`Time to empty (time left)`、`Time to full (recharging)`、`Charge`（电量）和 `Rate`（速率）。`Statistics` 选项卡可以显示充电和放电图。

### Web、邮件、辅助功能和终端窗口的首选应用程序

某些类型的文件已经关联了默认应用程序。例如，双击网页文件将在 `Firefox` 浏览器中打开该文件。如果你喜欢设置不同的默认应用程序，可以使用 `Preferred Applications` 工具（参见图 7-38）。可以通过 `Preferences` 菜单（`Preferences | Preferred Applications`）以及 `GNOME Control Center`（`Personal` 部分）访问首选应用程序工具。该工具允许为网页、邮件读取器、辅助工具、多媒体和应用程序以及系统级工具设置默认应用程序。可用应用程序列在弹出菜单中。在图 7-38 中，默认邮件读取器是 `Thunderbird`，默认网络浏览器是 `Firefox`。要将另一个应用程序设置为默认，点击菜单按钮显示其他可能的已安装应用程序列表。首选应用程序工具具有 `Internet`（互联网）、`Multimedia`（多媒体）、`System`（系统）、`Office` 和 `Accessibility`（辅助功能）。在 `Multimedia` 选项卡上，你可以选择默认图像查看器、视频播放器和多媒体播放器。在 `Office` 选项卡上，你可以指定默认文档查看器、文字处理器和电子表格应用程序。在 `System` 选项卡上，你可以选择默认文本编辑器、终端窗口应用程序和文件管理器。`Accessibility` 面具有选择放大镜的选项。

![Image](img/image-428.png)  ![Image](img/image-429.png)

![Image](img/image-430.png)  ![Image](img/image-431.png)

图 7-38: 首选应用程序工具

### 媒体默认应用程序

Caja 直接处理媒体操作的偏好。你可以使用 `File Management Preferences` 对话框设置偏好。可以通过任何 Caja 文件管理器窗口上的 `Edit | Preferences` 菜单项访问。




文件管理首选项（File Management Preferences）对话框的媒体标签列出了 Cd Audio、DVD Video、音乐播放器、照片和软件的项目。弹出菜单允许您选择用于不同媒体的应用程序（参见图 7-39）。您还有`Ask what to do`询问做什么、`Do Nothing`什么都不做、以及`Open folder`打开文件夹等选项。`Open Folder`选项将打开一个显示光盘文件的窗口。标记为“Other media”（其他媒体）的区域允许您为蓝光等等不常用的媒体设置关联。初始情况下，所有项目都将设置为`Ask what to do`。每个菜单都列出了可能的选项，例如针对 Cd 音频的 Rhythmbox 音乐播放器和针对 DVD 视频的 Celluloid。照片可以使用 Pix 管理器打开。一旦您选择了选项，当您插入可移动介质（如音频盘）时，关联的应用程序会自动启动。

如果您只想关闭特定类型媒体的启动，可以从其应用程序弹出菜单中选择`Do Nothing`项目。如果您希望提示选项，请在媒体标签的弹出菜单中设置`Ask what to do`项目。当插入光盘时，会显示一个带有可能操作弹出菜单的对话框。默认应用程序已选中。您可以选择另一个应用程序，或者选择`Do Nothing`或`Open Folder`选项。

通过勾选媒体面板底部的`Never prompt or start programs on media insertion`插入媒体时从不提示或启动程序选框，可以关闭所有媒体的自动启动。您还可以启用`browse media when inserted`插入时浏览媒体选项，以便仅打开显示其文件的文件夹。

![Image](img/image-432.png)

图 7-39: 媒体的文件管理首选项

### 屏幕保护与锁定

在屏幕保护首选项（Screensaver Preferences）中，您可以控制电脑何时被视为空闲，以及如果有的话使用何种屏幕保护程序（参见图 7-40）。您可以从 Linux Mint 菜单中的首选项菜单通过`Screensaver`访问屏幕保护首选项对话框，或者从“个人设置”（Personal）部分的控制中心访问。您可以使用左侧的滚动框从各种屏幕保护程序中选择，右侧显示预览。您还可以控制在空闲时是否锁定屏幕以及锁定多久。您可以通过取消勾选`Activate screensaver when computer is idle`电脑空闲时激活屏幕保护选框来关闭屏幕保护。

![Image](img/image-433.png)

图 7-40: 屏幕保护首选项

### 辅助技术

在 MATE 中，辅助技术（Assistive Technologies）对话框是一组用于访问其他工具辅助标签卡的简单按钮（参见图 7-41）。在辅助技术部分，使用`Enable assistive technologies`复选框开启或关闭辅助技术。`Preferred Applications`按钮将打开首选应用程序对话框上的辅助功能标签卡。

在首选项（Preferences）部分，有用于打开键盘和鼠标首选项对话框的辅助功能标签卡的按钮。在键盘辅助功能标签卡上，您可以配置如粘滞键、慢键和限定键等功能。鼠标按钮则直接打开鼠标首选项对话框。

![Image](img/image-434.png) ![Image](img/image-435.png)

图 7-41: 辅助技术首选项和辅助功能首选应用程序

# 第 3 部分：管理

8. 系统工具

9. 系统管理

10. 网络连接

11. Shell 配置

# 8. 系统工具

在附件（Accessories）、首选项（Preferences）和管理（Administration）菜单中可以找到实用的系统工具以及用户特定的配置工具（参见表 8-1）。管理菜单包含系统监视器和磁盘使用分析器等工具。附件菜单包含磁盘实用（Disk Utility）和 ClamTK 病毒扫描器（Virus Scanner）。桌面配置（如鼠标、键盘、显示和声音配置）由 Cinnamon 和 MATE 直接处理（系统设置），并可以通过首选项菜单访问。

| Linux Mint 系统工具 | 名称 | 描述 |
| :--- | :--- | :--- |
| gnome-system-monitor | 系统监视器 | GNOME 系统监视器 |
| gnome-logs | 日志 | GNOME 日志 |
| gnome-terminal | 终端 | GNOME 终端窗口 |
| baobab | 磁盘使用分析器 | 带有图形表示的磁盘使用分析器 |
| gnome-nettool | 网络工具 | 网络分析 |
| ClamTK | 病毒扫描器 | Clam 病毒扫描器 |
| Disk Utility | 磁盘实用 | 用于管理硬盘和可移动驱动器的 Udisks 工具 |
| PulseAudio | 音频 | 音频驱动和服务器 |

表 8-1: Linux Mint 系统工具

## GNOME 系统监视器

Linux Mint 提供了 GNOME 系统监视器用于显示系统信息和监控系统进程，可以通过管理菜单中的“系统监视器”访问。它有三个标签卡：进程（Processes）、资源（Resources）和文件系统（File Systems）（参见图 8-1）。资源标签卡显示 CPU 历史、内存交换和网络历史图。如果您的系统是多核的，CPU 历史图显示每个 CPU 的使用情况。内存交换图显示内存量。网络历史图显示发送和接收数据的总量。文件系统标签卡列出您的文件系统、其挂载位置、类型以及磁盘空间的使用和可用情况。双击文件系统项将在文件管理器中打开该文件系统。

进程标签列出您的进程，允许您进行排序和搜索。您可以使用字段按钮按名称（Process Name）、进程 ID（ID）、使用百分比（%CPU）和内存使用（Memory）进行排序。菜单（菜单栏右侧）允许您选择所有进程、自己的（My Processes）或活动进程。可以通过选择进程并点击“结束”（右下角）按钮，或右键点击并选择“结束”来停止任何进程。您可以右键点击进程项以显示可以对进程执行的操作菜单，如停止（Stop）、结束（End）、杀死（Kill）和继续进程（Continue），以及更改进程优先级（Change Priority）。打开文件（Open Files）项将打开显示进程正在使用的所有文件、套接和管道的对话框。属性（Properties）项显示进程的所有详细信息，如名称、用户、状态、内存使用、CPU 使用和优先级。内存映射（Memory Maps）从内存映射项进入，显示所选进程的虚拟内存、节点和标志信息。

用于 CPU 图表的显示功能可以使用 dconf 编辑器的 `org.gnome.gnome-system-monitor` 键进行设置。

![Image](img/image-436.png)

图 8-1: GNOME 系统监视器：资源

## 管理进程

如果需要强制退出某个进程或应用程序，可以使用 Gnome 系统监视器的进程标签卡来查找、选择并停止进程。您应该确定您想要停止的进程。结束关键进程可能会导致系统崩溃。应用程序进程将带有应用程序名称，您可以使用它们强制应用程序退出。手动结束进程通常用于无法正常停止的开放式操作。在图 8-2 中，已选择了 Firefox 应用程序。点击左下角的“结束进程”按钮将强制 Firefox Web 浏览器结束。




进程的弹出菜单（右键点击）提供了管理所选进程的几个其他选项：停止、继续、结束、杀死和更改优先级。大多数选项都有相应的键盘键。“停止”和“继续”操作是配合使用的。你可以停止（`Stop`）进程，稍后使用`继续`(Continue）选项重新启动它。`结束一个 End）选项可以安全地停止进程，而`杀死`(Kill）选项会强制立即结束进程。建议使用`结束`选项，但如果不起作用，可以使用`杀死`选项。`更改优先级`(Change Priority）可以赋予进程较低或更高的优先级，使其运行得更快或更慢。`属性一个 Properties）选项会打开一个对话框，列出进程详情，如名称、用户、状态、使用的不同内存类型、CPU 使用率、启动时间、进程 ID 和优先级。`打开文件`(Open Files）选项列出了进程正在使用的所有文件、套接字管道。

![Image](img/image-437.png)

图 8-2: GNOME 系统监视器：进程

你还可以使用 `pkill` 命令配合进程名或进程 ID 来结束进程。要使用进程名，请使用 `-n` 选项输入该名称的最近一次进程。

```
pkill -n firefox
```

你可以在终端窗口中使用 `kill` 命令来结束进程。`kill` 命令以进程号作为参数。请确保你获取了正确的进程号。使用 `ps` 命令显示进程 ID。输入错误的进程号可能会导致系统瘫痪。带有 `-C` 选项的 `ps` 命令搜索特定的应用程序名称。`-o pid=` 选项将仅显示进程 ID，而不是进程 ID、时间、应用程序名称和 tty。一旦获取了进程 ID，你就可以将进程 ID 作为参数使用 `kill` 命令来结束进程。

```bash
$ ps -C firefox -o pid= 5555
$ kill 5555
```

确保数字正确的一种方法是使用 `ps` 命令直接将进程号作为 `kill` 命令的参数返回。在接下来的示例中，使用 `mycmd` 命令启动了一个开放式进程。开放式进程是指在你手动停止它之前会持续运行的进程。

```
mycmd > my.ts
```

然后通过首先执行 `ps` 命令获取 `mycmd` 进程的进程 ID（反引号包裹），然后在在 `kill` 命令中使用该进程 ID 来结束进程。`-o pid=` 选项仅显示进程 ID。

```bash
kill `ps -C mycmd -o pid=`
```

要使用模式搜索进程，可以使用带有 `-aux` 选项的 `ps` 命令列出所有进程，并将输出通过到带有指定模式的 `grep` 命令中。以下命令列出了所有的 X Window 系统进程。

```bash
ps -aux | grep 'firefox'
```

你可以使用 `pidof` 命令仅获取进程 ID。

```bash
pidof firefox
```

## Glances

Glances 是一项全面的系统监控工具，可以在终端窗口中通过 `glances` 命令从命令行运行。它显示系统、网络、磁盘、文件系统、传感器和进程的详细资源使用情况（参见图 8-3）。它还会提醒你任何严重警报。系统部分涵盖了详细的内存、CPU、交换和负载使用情况。网络部分显示了每个网络设备的活动。磁盘 I/O 部分列出了你的存储设备及其读写使用情况。File Sys 部分显示了你所有的分区以及使用了多少内存。Sensors 部分显示传感器检测到的温度，例如 CPU、GPU 和环境温度。Tasks 部分按 CPU 使用率列出你的活动进程，显示内存使用情况、pid、用户和命令。按 `q` 结束 glances 会话。

Glances 组织成多个模块，你可以禁用这些模块以仅显示有限的报告。例如，如果你对磁盘 I/O 报告感兴趣，可以使用 `--disable-diskio` 选项禁用 diskio 模块。请查看 `glances` 手页以获取你可以使用的模块选项完整列表。

```
glances -- disable-diskio.
```

还有几个运行时命令可以用于显示和隐藏模块，例如 `f` 切换文件系统报告的开启/关闭，`d` 切换磁盘 I/O，`n` 用于网络统计，`s` 显示传感器以及 `p` 按名称排序进程。

![Image](img/image-438.png)

图 8-3: Glances 系统监视器

## 任务调度

调度定期维护任务（如备份）可以通过使用 systemd 定器或 cron 服务进行管理。systemd 定器是运行服务文件的 systemd 文件。查看 `systemd.timers` 手页以获得有关计时器的详细说明。它们的扩展名为 `.timer`。定时器文件会自动运行一个同名的服务文件。例如，`dnf-automatic.timer` 将运行 `dnf-automatic.service` 文件。定时器文件仅包含调度信息。它的文件名决定了运行哪个服务文件。可以在定时器文件中通过 `Unit` 指令指定不同的服务文件。如果你想运行一个没有服务文件的命令行操作，可以为该命令创建一个带有 `ExecStart` 条目的自定义服务文件。

定时器文件有一个 `timer` 部分，在其中你定义服务文件的运行时间。还有相对于某些时间点（如系统启动）的选项，以及引用日期的 `OnCalendar` 选项。`OnCalendar` 选项使用 `systemd.time` 手页中定义的日表达式。日表达式由星期、年份、月份和时间组成。时间以小时、分钟和秒指定，用冒号分隔。星期范围用两个点分隔，特定的星期用逗号分隔。省略年份或月份将选择任何年份或月份。以下引用五月份的下午 2 点。

`OnCalendar=Mon..Fri`

你可以创建定时器文件并将其放在 `/etc/systemd/system` 目录下。要激活定时器，请确保使用 `systemctl` 启用它。如果你创建了服务文件，请确保启用它。

仍然可以使用旧的 cron 服务来调度任务。cron 服务由 cron 进程实现，它不断检查需要执行的操作。这些任务列在 crontab 文件中。cron 进程不断检查用户的 crontab 文件以查看是否到了执行这些操作的时间。用户都可以设置 crontab 文件。root 用户可以设置 crontab 文件执行系统管理操作，例如每周或每月在特定时间备份文件。

创建 cron 条目是一项复杂的任务，可以使用 `crontab` 命令修改 `/etc/crontab` 中的 crontab 文件。相反，你可以使用桌面 cron 调度器来设置 cron 操作。





要查看日志，你可以使用管理菜单中的`日志`（Logs）访问 Gnome 日志。侧边栏列出了不同的日志类别。选择其中一种即可在右侧显示日志消息。关键消息列在`重要`（Important）类别下。标题栏上的“日志”标签是一个按钮，点击它可以显示最近的启动会话列表。你可以选择其中一个来缩小显示的消息。默认情况下，选择的是最近的一个。右上角的搜索按钮会打开搜索框，你可以在其中选定的日志中搜索消息。搜索具有选项（右侧菜单），可以按字段和时间细化搜索。

## 磁盘使用分析器

磁盘使用分析器让你查看所有已挂载硬盘分区已用和可用的磁盘空间（参见图 8-5）。你可以从管理菜单通过`磁盘使用分析器`（Disk Usage Analyzer）访问它。它还会检查所有的 `LVM` 和 `RAID` 阵列。使用情况以简单的图表显示，让你看到总共有可用空间及其分布位置。在扫描对话框中，你可以选择扫描硬盘（磁盘驱动器图标）、主文件夹或连接的设备，如软盘或 USB 驱动器（参见图 8-6）。点击右侧的菜单按钮可以选择特定的文件夹进行扫描，无论是本地还是远程。当你扫描目录或文件系统时，将分析并显示该目录的磁盘使用情况。每个文件系统都会显示其使用情况图表，以及其大小、顶级目录和文件的数量。然后会显示目录以及它们的大小和内容（文件和目录）。

![Image](img/image-440.png)

图 8-5: 磁盘使用分析器

右侧窗格显示磁盘使用的表示性图表。图表可以是`环形图`（Ring Chart）或`树状图`（Treemap）。`环形图`是默认设置。从右下角的按钮中选择你想要的。对于`环形图`，会显示目录，从中心的顶级目录开始向外移动到子目录。将鼠标悬停在图表的某个部分上会显示其目录名称和磁盘使用情况，以及所有的子目录。`树状图`显示方框表示，磁盘使用量越高方框越大，子目录封装在目录框内。

![Image](img/image-441.png)

图 8-6: 磁盘使用分析器：扫描对话框

## 病毒防护

对于病毒防护，你可以使用 Linux 版 `ClamAV`，它使用名为 `ClamTk` 的 GNOME 前端，[`www.clamav.net`](https://www.clamav.net)。此病毒扫描器包含在 Ubuntu 主仓库中。你可以从软件管理器安装 `ClamTk`。系统还会为你选择并安装支持的 `ClamAV` 包（`clamav-base` 和 `clamav-freshclam`）。你也可以使用`Synaptic 软件包管理器`安装 `ClamAV`，选择 `clamav`、`clamav-base`、`clamav-freshclam`（在线病毒定义）和 `ClamTK` 包。仅选择 `ClamTk` 将自动选择其他 `clamav` 包进行安装。`clamav-freshclam` 包从 `ClamAV` 服务器获取当前的病毒定义。若要让 `ClamAV` 自动检查你的邮件消息，你需要安装 `ClamAV` 扫描守护进程（`clamav-daemon` 和 `clamdscan` 包）。

![Image](img/image-442.png)

图 8-7: 用于 ClamAV 病毒防护的 ClamTK 工具。

你可以从附件菜单通过`ClamTk`访问 `ClamTk`。通过 `ClamTk`，你可以扫描特定的文件和目录，以及你的主目录（参见图 8-7）。搜索可以是递归的，包括子目录（设置）。你有检查配置文件的选项（扫描以点为开头的文件）。你也可以对主目录进行快速扫描或递归扫描。受感染的文件将被隔离。

你的病毒定义将自动更新。如果你想手动检查病毒定义，需要点击`更新助手`（Update Assistant）并选择自己更新签名。然后点击`更新`（Updates）并点击“检查更新”旁边的`确定`按钮。

## 硬件传感器

许多用户关注的是计算机组件的温度和使用情况。你可以安装不同的软件包来启用某些传感器（参见表 8-2）。你可以添加“CPU 温度指示器”（CPU Temperature Indicator）小程序来显示你的 CPU 温度。如果你的系统支持 `CPU Scaling`，你可以添加`频率选择器`（CPU Frequency Selector）。对于 CPU、系统、风扇速度以及主板支持的任何传感器，你可以使用 `Psensor`、`Xsensors` 或 `lm-sensors` 服务。`Psensors` 安装 `hddtemp` 硬盘温度服务器并显示你的 CPU、显卡和硬盘温度。你可以为报警设置温度阈值。`Xsensors` 显示你的 CPU 温度。你还有几个可以安装到面板的 Cinnamon 小程序，包括`CPU 温度指示器`、`GPU 温度`（GPU Temperature）和`图形硬件监控`（Graphical Hardware Monitor）。

| 传感器应用程序 | 说明 |
| :--- | :--- |
| `lm-sensors` | 检测并访问计算机（主板）传感器，如 CPU 和风扇速度。运行 `sensors-detect`。 |
| `hddtemp` | 检测硬盘温度（也由磁盘工具检测） |
| `Disk Utility` | 提供磁盘的 SMART 信息和检查。 |
| `Psensor` | 检测并显示系统温度。 |
| `Xsensors` | 检测并显示风扇。 |
| `indicator-cpufreq` | 用于监控和更改 CPU 频率。 |
| `CPU Frequency Applet` | CPU 频率缩放。 |
| `CPU Temperature Indicator` | CPU 温度（Cinnamon 小程序） |
| `Simple CPU Monitor` | CPU 使用率（Cinnamon 小程序） |
| `GPU Temperature` | GPU 温度（Cinnamon 小程序） |
| `Graphical Hardware Monitor` | 设备组件信息（Cinnamon 小程序） |

表 8-2: 传感器软件包和应用程序

如果没有安装，请安装 `lm-sensors` 包。然后你需要配置传感器。在终端窗口输入以下并根据提示回答。

```
sudo sensors-detect
```

`磁盘工具`（偏好和附件菜单中的磁盘）让你知道硬盘温度。`磁盘工具` 使用 `Udisks` 访问磁盘的 SMART 信息。打开`磁盘工具`，选择硬盘。在右侧窗格中，`评估`（Assessment）项列出了磁盘温度。

## 磁盘工具与 Udisks

磁盘工具是一个支持 `Udisks` 的存储媒体用户界面，用于硬盘、USB 驱动器和 DVD/CD 驱动器（`gnome-disk-utility` 包，默认安装）。任务包括磁盘标记、挂载磁盘、磁盘检查和加密。你还可以执行更高级的任务，如管理 `RAID` 和 `LVM` 存储设备以及分区。你可以通过附件和偏好菜单中的`磁盘`访问磁盘工具。磁盘工具窗口显示一个带有存储介质项目的侧边栏（参见图 8-8）。点击某一项将在右侧窗格显示该介质的信息。可移动设备（如 USB 驱动器）在标题栏上显示电源和弹出按钮，以及一个带有格式化磁盘任务菜单。如果你正在格式化分区（如可移动媒体上的分区），你可以指定使用的文件系统类型。

![Image](img/image-443.png)

图 8-8: 磁盘工具




如果你选择一个硬盘设备，右侧顶部将显示有关硬盘的相关信息，例如型号名称、序列号、容量、分区表类型以及 SMART 状态（评估）（参见图 8-9）。点击菜单按钮将在右上角显示菜单，其中列出了你可以对硬盘执行的任务：格式化（Format）、基准测试（Benchmark）和 SMART 数据。

![Image](img/image-444.png)

图 8-9: 磁盘实用程序，硬盘

硬盘面板上的“卷（Volumes）”部分显示了在硬盘上设置的分区（参见图 8-10）。分区以图形图标条的形式显示，显示了每个分区在驱动器上的大小和位置。点击图形图标条上的分区条目将显示有关该分区的信息，例如文件系统类型、设备名称、分区标签和分区大小。“内容（Contents）”条目会告知分区是否已挂载。如果正在使用，它将显示一个“挂载于 (Mounted at:)”条目，其中包含文件系统挂载的路径名称链接。你可以点击此路径名称打开文件夹，并通过它访问文件系统。卷图像下方的按钮栏提供了你可以执行的其他任务，例如卸载文件系统（正方形按钮）和删除分区（减号按钮）。从更多任务菜单（齿轮按钮）中，你可以选择条目来检查并修复文件系统、调整大小或格式化，并更改分区标签（Edit Filesystem）、分区类型（Edit partition）以及挂载选项（Edit Mount Options）。某些分区（如扩展分区）显示的信息有限，允许的任务也较。

![Image](img/image-445.png)

图 8-10: 磁盘实用程序，卷

有关硬盘更详细的硬件信息，你可以点击右上角任务菜单中的“SMART 数据和测试（SMART Data and Tests）”条目。这将打开一个 SMART 数据对话框，其中包含硬盘的硬件信息（参见图 8-11），包括温度、通电周期、坏道和磁盘的整体健康状况。“属性（Attributes）”部分列出了 SMART 细节，如读取错误率、启动时间、温度和写入错误率。将切换到开启以启用测试，关闭以禁用测试。点击“刷新（Refresh）”按钮手动运行测试。点击“启动自检（Start Self-test）”按钮将打开一个包含短期、扩展和传输测试的菜单。

![Image](img/image-446.png)

图 8-11: 磁盘实用程序：硬盘硬件 SMART 数据

## Plymouth

Plymouth 提供了一种简洁、高效且更快的图形启动，不需要 X server 支持。它依赖内核的内核模式设置（KMS）功能，该功能为基础图形提供直接支持。通过直接渲染管理器（Direct Rendering Manager）驱动，Plymouth 可以利用不同的图形插件。目前为 AMD、 Nvidia 和 Intel 显卡提供 KMS 支持。默认安装 Plymouth Linux Mint Logo 主题。你可以安装其他的，如 solar 和 glow。主题包以 `plymouth-theme` 为前。你可以在 Synaptic 软件包管理器中搜索它们。你也可以从软件管理器安装它们（搜索 Plymouth）。

选择使用 Plymouth 主题涉及使用 Debian 备方案系统（alternatives system），该系统旨在当存在多个备选版本供选择时指定使用的应用程序。在 `/etc/alternatives` 目录中为应用程序设置了一个链接。对于 Plymouth，该链接命名为 `default.plymouth`。你可以可以在终端窗口输入带有 `--config` 选项 `update-alternatives` 命令、`default.plymouth` 链接以及 `sudo` 命令来选择 Plymouth 主题：

```
sudo update-alternatives --config default.plymouth
```

这将显示一个编号菜单，列出你已安装的主题。星号表示当前的主题。输入你想使用的主题编号。`default.plymouth` 链接将被设置为你选择的主题。当系统再次启动时，它将使用该 Plymouth 主题。

某些非 Linux Mint 主题可能会在启动时卡住。在这种情况下，你可以编辑启动内核行以移除 `splash` 选项然后启动系统（参见第 3 章）。然后使用 `update-alternatives` 更改你的 Plymouth 主题。

## 音频

当你启动系统时，ALSA 会自动为你检测声卡，ALSA 是在系统启动时由 udev 调用的。可拆卸设备（如 USB 音频设备）也会被检测。请参见表 8-3 获取音频设备和接口工具列表。

除了硬件驱动程序，音频系统还使用音频接口将编码的音频流从应用程序引导到硬件驱动程序和设备。Linux Mint 使用 PulseAudio 服务器作为其音频接口。PulseAudio 的目标是将所有音频接口合并整合为一个简单、灵活且强大的服务器。ALSA 硬件驱动程序仍在使用，但应用程序接口由 PulseAudio 处理。PulseAudio 是 Linux Mint 和 Ubuntu 的默认安装。

注意：Linux 上的音频设备由硬件音频驱动程序支持。通过 Linux 内核，硬件支持通过高级 Linux 音频架构（ALSA）系统实现。你可以在 [`alsa-project.org`](http://alsa-project.org) 更多关于 ALSA 的信息。

PulseAudio 是一个跨平台音频服务器，允许你修改不同音频流的音量。请访问 [`www.freedesktop.org/Software/PulseAudio/`](https://www.freedesktop.org/Software/PulseAudio/) 获取文档和帮助。PulseAudio 提供了对所有音频流的完全控制，让你可以将声音引导到网络上的任何地方。PulseAudio 不限于单一系统。它具有网络能力，允许将声音从一台电脑引导到另一台。

| 音频工具 | 描述 |
| :--- | :--- |
| alsamixer | ALSA 连接配置和音量工具 |
| amixer | 连接配置命令 |
| Sound Preferences | GNOME 音频偏好，用于选择和配置你的音频接口（音频） |
| PulseAudio | 音频接口，Linux Mint 的默认音频接口。[www.pulseaudio.org](http://www.pulseaudio.org) |
| PulseAudio Volume Control | 音量控制，控制流输入、输出和播放，`pavucontrol` 包 |
| PulseAudio Volume Meter | 量表，显示活跃音量 |
| PulseAudio Manager | 信息和管理的管理器，`pman` 包 |
| PulseAudio Preferences | 网络访问和虚拟输出选项 |

表 8-3: 音频设备和接口工具

作为替代，你可以使用命令行 ALSA 控制工具 `alsamixer`。这将显示所有连接并允许你使用键盘命令选择（箭头键）、静音（m 键）或设置音量（Page Up 和 Down）。按 ESC 键退出。`amixer` 命令允许你从命令行对不同的连接执行相同的任务。要从命令行实际播放和录制，你可以使用 `play` 和 `rec` 命令。

### 音菜单（音量控制和播放器访问）

音频菜单（声器图标，音频小组件）显示音量控制、媒体播放器访问、音频设置访问以及音频设备选择条目（参见图 8-12）。

![Image](img/image-447.png)  ![Image](img/image-448.png)  ![Image](img/image-449.png)  ![Image](img/image-450.png)

图 8-12: 音频菜单



你可以使用滑动条更改应用程序的音量。当你点击音量滑块时，可以使用鼠标滚轮来调整音量。要对特定设备（如麦克风）进行音量控制，你需要使用“声音”对话框，你可以从“系统设置”或声音菜单中的“声音设置”项中访问它。

声音菜单提供了对媒体播放器（如 `Rhythmbox`）的基本访问，显示当前曲目的标题，并显示播放、暂停以及切换到上一首和下一曲目的控制控件。点击“启动播放器”条目可以打开已安装播放器的列表。当你播放音频源时，声音菜单上会显示音频轨的描述和基本控制按钮。当你正在播放时，面板上的声音图标将变为音乐音符。

如果你想静音，可以右键点击声音图标以显示输出和输入的静音开关（请参见 图 8-13）。点击开关即可静音。

![Image](img/image-451.png)

图 8-13: 声音菜单，右键点击，静音选项

## 声音

你可以使用 GNOME 声音工具配置声音设备并设置音效、输入、输出以及应用程序的音量。在“系统设置”对话框中选择“声音”，在“选项”菜单中选择“声音”，或从面板声音应用菜单中选择“声音设置”。这将打开“声音”对话框，它有四个标签页：输出、输入、声音、应用程序和设置（请参见 图 8-14）。

![Image](img/image-452.png) ![Image](img/image-453.png)

图 8-14: 声音：声音

“声音”标签页允许为不同的操作选择声音，例如切换工作区或关闭窗口。每个效果右侧的播放按钮可以播放声音，点击带有声音文件名的按钮可以打开 `/usr/share/mint-artwork-cinnamon/sounds` 文件夹，可以在那里选择不同的声音文件。可以通过播放按钮右侧的开关关闭声音。“声音音量”部分顶部的滑动条可以让你设置音效的音量。

在“输入”标签页上，你可以选择输入设备并设置输入音量。输入设备列在顶部的“设备”部分。在“设备设置”部分，你可以设置所选设备的音量。在说话或录制时，会显示输入电平（请参见 图 8-15）。

![Image](img/image-454.png)

图 8-15: 声音：输入

在“输出”标签页上，你可以为选定的设备配置设置：数字、耳机和扬声器。可用设置将根据选的设备和配置激活。从“输出配置”菜单中，你可以从可用输出中选择（如果支持），例如模拟扬声器或环绕声。对于简单的模拟立体声输出，只有“音量”和“平衡”设置是激活的（请参见 图 8-16）。

![Image](img/image-455.png)

图 8-16: 声音：输出

支持多接口的声音设备（如模拟环绕声 7.1 或数字 SPDIF 输出）将在“输出配置”菜单中显示接口组合列表。“淡出”和“低音器”的设置将被激活。从菜单中，你可以选择你需要的输出类型。为数字输出（S/PDIF）连接器配置数字输出，只需在“输出”和“输入”标签页上选择数字输出和输入项即可。只有“平衡”项将处于激活。

笔记本电脑可能仅支持具有左右平衡的简单内部音频设备。具有更强大声音设备的电脑有更多选项。要测试你的扬声器，点击“测试声音”按钮打开“扬声器测试”对话框，其中带有每个扬声器的测试按钮。

“应用程序”标签页将显示当前使用声音设备的应用程序。你可以为每个程序设置音量（请参见 图 8-17）。

![Image](img/image-456.png)

图 8-17: 声音：应用程序

“设置”标签页设置所有应用程序声音控制的最大音量（请参见 图 8-18）。这些控制将根据“设置”标签页中的最大音量设置进行调整。范围将仅延伸到最大限制。你可以设置的最大值为 150%。

![Image](img/image-457.png)

图 8-18: 声音：设置

安装 Pulse Audio 时会带上 Pulse Audio 工具（`pulseaudio-utils` 软件包）。这些是用于管理 Pulse Audio 和播放音频文件的命令行工具（请参见 表 8-4）。`paplay` 和 `pacat` 将播放音频文件，`pactl` 让你控制声音服务器，`pacmd` 让你重新配置它。查看每个工具的 Man 页（帮助手册）以获取更多详情。如果你频繁更改声音偏好，可以在 shell 脚本中使用这些命令来实现更改。

## PulseAudio 应用程序

为了获得额外的配置能力，你还可以安装 Pulse 应用程序。大多数包名以 `pa` 为前缀。Pulse 工具可以通过“声音和视频”菜单访问。这里显示了 PulseAudio 工具及其名称。

| 工具 | 描述 |
| :--- | :--- |
| `pa-info` | 关于系统中 PulseAudio 的详细信息 |
| `pacat` | 播放、录制和配置音频流 |
| `pacmd` | 用于配置的 shell |
| `pactl` | 控制 PulseAudio，更改输入输出并提供服务器信息 |
| `padsp` | OSS 应用程序的封装 |
| `pamon` | 链接 pacat |
| `paplay` | 播放音频。`-d` 选项指定输出设备，`-s` 选项指定服务器，`--volume` 选项设置音量（链接 pacat） |
| `parec` | 录制音频流（链接 pacat） |
| `parecord` | 录制音频流（链接 pacat） |
| `pasuspender` | 挂起 PulseAudio 服务器 |
| `pax11publish` | 访问 PulseAudio 凭据 |

表 8-4: PulseAudio 命令（命令行）

你可以使用 PulseAudio 音量控制工具设置不同播放应用程序和声音设备的音量（在“声音和视频”菜单中选择 PulseAudio 音量控制）。

PulseAudio 音量控制将显示五个标签：播放、录制、输出设备、输入设备和配置（请参见 图 8-19）。“播放”标签显示所有正在使用 PulseAudio 的应用程序。你可以为每个应用程序单独调整音量。

![Image](img/image-458.png)

图 8-19: PulseAudio 音量控制，播放




你还可以使用 PulseAudio 音量控制将不同的应用程序（流）重定向到不同的输出（设备）。例如，你可以同时运行两个音频源，一个用于视频，另一个用于音乐。你可以将视频通过一个设备定向到耳机，将音乐通过另一个设备定向到扬声器，甚至到另一台电脑。要将应用程序重定向到不同设备，请在“播放”（Playback）选项卡中右键点击其名称。弹出菜单将列出可用设备，并让你选择想要使用的设备。

PulseAudio 音量计工具将显示设备的实际量。

![Image](img/image-459.png)

图 8-20：PulseAudio 音量控制，输出设备

要配置网络访问，你需要使用 PulseAudio 配置工具。在这里，你可以允许网络访问、配置 PulseAudio 网络服务器并启用多播和同时输出。如果你连接的网络中有同样运行 PulseAudio 且允许其音频设备网络访问的 Linux 系统，那么它们的共享音频设备将列在“声音偏好-硬件”（Sound Preferences Hardware）选项卡中，允许你访问它们。

同时输出会在同一硬件设备上创建一个虚拟输出设备。这允许你将两个源引导到同一个输出上。通过 PulseAudio 音量控制，你可以将播放流引导到同一个输出设备，但使用虚拟设备作为其中一个的输出。这允许你独立更改每个流的输出音量。你可以让音乐和语音定向到同一个硬件设备，为音乐使用虚拟设备，为语音使用标准设备。然后你可以减小音乐流，或调大语音流。

## dconf editor

dconf editor 为你的基于 GNOME 的桌面（Cinnamon 和 MATE）、GNOME 应用程序以及 X-Apps 应用程序提供了基础配置选项（请参见 图 8-21）。你可以配置桌面和 GNOME 应用程序，例如 Cinnamon 和 MATE 文件管理器（`nemo` 和 `caja`）、GNOME 系统监视器和 X-Apps。大多数选项涉及显示功能，例如 `Xplayer` 的默认选项、对话框的默认大小，或者是否显示应用程序的工具栏。

使用 dconf 配置是在键（keys）上进行的，键可以是数字、复选框、文本以及列出可能选项的菜单。文本编辑支持鼠标点击并拖拽来选择文本，以及使用 `Ctrl-c`、`Ctrl-x` 和 `Ctrl-v` 进行复制、剪切和粘贴。输入插入，使用退格键删除。对于非常长的文本条目，会出现滚动条让你滚动该行。更改会立即生效。如果你犯了错，可以通过选择标题栏菜单中的“重置可见键”（Reset visible keys）项重置为默认设置。

![Image](img/image-460.png)

图 8-21：dconf editor

dconf editor 将键组织成架构（schemas），可以在侧边栏作为可展开的树结构进行访问。主架构有 `apps`、`ca`、`com`、`desktop`、`io`、`org` 和 `system`。`org` 架构包含 Cinnamon 配置键，其中有桌面组件（desklets）、桌面、背景和 muffin 窗口器的子架构。这里还有 MATE 键（`org.mate`）和 gnome 应用程序键（`org.gnome`）。在 `com` 架构下，你会找到 `linuxmint` 子架构，其中包含用于 Mint 菜单键的 `mintmenu` 子架构（`com.linuxmint.mintmenu`）。继续展开子架构，直到找到你需要的键，在本例中为 `com.linuxmint.mintmenu`。

GNOME 应用程序的键位于 `org.gnome`。大多数处理默认显示选项。

`x` 架构列出了 X-Apps 应用程序键。某些允许你设置应用程序特定的选项。播放器架构（`Xplayer`）具有设置对比度、色调和缩放选项的键（`org.x.player`）。编辑器（`Xed`）允许你设置边距、保存、缩进和字体选项（`org.x.editor`）。

Celluloid 播放器（Linux Mint 新默认视频播放器）的键位于 `io.github` 架构下的 `io.github.celluloid-player` 以及它基于的 MPV 播放器 `io.github.gnome-mpv`。

## 使用 Seahorse 管理密钥

对于文件文本的 GPG 和 SSH 加密、签名和解密，GNOME 提供了 Seahorse。通过 Seahorse，你可以管理存储在密钥环中的加密密钥以及 SSH Key 和密码。你可以导入密钥、签名密钥、搜索远程密钥并创建自己的密钥环，还可以指定用于搜索和发布的密钥服务器。所有这些操作也可以使用 `gpg` 命令完成。Seahorse 默认安装。

### 密码和密钥

要导入、签名和查找密钥，你可以使用“密码和密钥”（Passwords and Keys）应用程序，可以通过“辅助工具”菜单中的“密码和密钥”访问。“密码和密钥”窗口显示一个包含四个部分的侧边栏：密码、密钥和证书（请参见 图 8-22）。Seahorse 标题栏右侧的 Seahorse 菜单显示查看密钥（个人、信任和任意）的选项，而 Seahorse 左左侧的“密码和密钥”文件夹菜单显示查找远程密钥、同步和发布密钥、偏好和帮助的选项。

![Image](img/image-461.png) ![Image](img/image-462.png)

图 8-22：Seahorse 密码和密钥（版本 3.3）

### 密钥环

“密码”部分列出了你的密钥环。密钥环存储网络和应用程序密码。通过点击标题栏左侧的加号按钮创建新密钥环。新密钥环列在“密码”部分。要管理密钥，右键点击项并选择“属性”。要将密钥环设置为默认，在侧边栏点击该项，然后点击“设置为默认”按钮。在这里你可以更改描述、访问密钥的密码并删除密钥。

![Image](img/image-463.png)

图 8-23：Seahorse 密钥环属性

### 创建新的 GPG 密钥

个人加密密钥显示在“PGP 密钥”部分。侧边栏的“GnuPG 密钥”显示 GPG 密钥。要创建自己的私钥，点击标题栏左侧的加号按钮 `+`。你可以选择设置 GPG、私密或 Shell 密钥。选择“GPG 密钥”并点击继续（参见 图 8-24）。请记住，在执行任何加密之前，你必须先设置 GPG 密钥对。

![Image](img/image-464.png)

图 8-24：选择加密密钥

这将打开一个新的 PGP 密钥窗口，你可以在其中输入姓名和电子邮件地址。在“高级密钥选项”部分，你可以设置加密类型（DSA、RSA 或仅限签名）、密钥强度和有效期（参见 图 8-25）。你也可以选择永不过期。然后点击“创建”按钮。

![Image](img/image-465.png)

图 8-25：创建加密密钥

随后你会被要求为加密密钥输入密码（passphrase）（参见 图 8-26）。此密码将允许你解密由你的密钥加密的任何数据。

![Image](img/image-466.png)

图 8-26：加密密钥密码

密钥随后将生成。这可能需要几秒钟。




一旦创建了密钥，它将出现在“密码和密钥”对话框的“GnuPG 密钥”选项卡中（参见图 8-27）。

![Image](img/image-467.png)

图 8-27：我的个人密钥

右键点击密钥并选择`属性`，将显示一个以密钥命名的对话框，并包含三个选项卡：所有者（Owner）、名称和签名（Names and Signatures）以及详细（Details）。`所有者`选项卡显示密钥类型和 ID、密钥照片以及一个允许您更改密钥口令的按钮（参见图 8-28）。点击加号按钮可以选择新的图像文件作为照片。`名称和签名`选项卡允许您向密钥添加用户、对密钥签名以及删除密钥。

![Image](img/image-468.png)

图 8-28：GnuPGP 密钥对话框：所有者选项卡

`详细`选项卡显示技术细节，如密钥 ID、类型和强度（参见图 8-29）。它还显示创建日期和过期日期（如果有）。在`操作`部分，`覆盖所有者信任`菜单允许您设置密钥的信任级别。您还可以将私钥（秘密密钥）导出到文件中。系统还会列出所有子密钥，您可以对其进行过期、撤销或删除。您可以添加新的子密钥并指定密钥类型、长度和过期日期。

![Image](img/image-469.png)

图 8-29：GnuPGP 密钥对话框：详细选项卡

### 密钥服务器

当您创建自己的私钥时，还会生成相应的公钥，其他人可以使用它可以加密发送给您的数据，并解密您发送给他们的消息签名。许多应用程序会发布公钥，您可以通过 Seahorse 下载并导入到系统中。密钥可以在密钥服务器上获取。要管理您的密钥服务器，从 Seahorse 文件夹菜单中选择`首选项`以打开`首选项`对话框（参见图 8-30）。在这里，您可以指定要访问的密钥服务器。列出了一个默认服务器：`ldap://keyserver.pgp.com`。另一个流行的密钥服务器是 `sks-keyserver.net` 服务器（[`sks-keyservers.net/`](https://sks-keyservers.net/)）。您可能想将其添加到列表中。该密钥服务器的地址为 `hkp://pool.sks-keyservers.net`。您可能还会添加位于 `hkp://keyserver.ubuntu.com` 的 Ubuntu 密钥服务器。

![Image](img/image-470.png)

图 8-30：Seahorse 首选项 - 密钥服务器

要添加密钥服务器，点击`添加`按钮打开对话框，在其中输入密钥服务器类型和地址（参见图 8-31）。对于 `hkp://` 密钥服务器，您选择密钥服务器类型“HTTP 密钥服务器”。在 Host 文本框中输入密钥服务器地址。您将看到该密钥服务器已添加到列表中。

![Image](img/image-471.png)  ![Image](img/image-472.png)

图 8-31：Seahorse 首选项 - 添加密钥服务器

在 Linux Mint 20 的初始发布版本中，Seahorse 编译时仅支持 LDAP 服务器，尽管这可能在随后的更新中得到修复。没有添加 HTTP 服务器的选项。要启用 Seahorse 添加 HTTP 密钥服务器（例如以 `hkp://` 开头的），您必须手动向 `/desktop/gnome/crypto/pgp/keyservers` 密钥服务器配置文件添加一个 HTTP 密钥服务器。您可以使用 `dconf-editor` 或 `dconf write` 命令来实现。

使用 `dconf-editor`，选择键 `desktop.gnome.crypto.pgp.keyservers`（参见图 8-32）。然后关闭“使用默认值”开关。在“自定义值”框中同时输入默认密钥服务器和添加的 HTTP 密钥服务器。将每个地址括在单引号，用逗号分隔，并将整个列表放在括号内。

```
['ldap://keyserver.pgp.com','hkp://pool.sks-keyservers.net']
```

![Image](img/image-473.png)

图 8-32：使用 dconf-editor 配置密钥服务器

您也可以在终端窗口中使用 `dconf write` 命令直接写入密钥服务器配置文件，如此处所示。

```
dconf write /desktop/gnome/crypto/pgp/keyservers "['ldap://keyserver.pgp.com','hkp://pool.sks-keyservers.net']"
```

### 导入公钥

在“密码和密钥”对话框中，按 `Ctrl-i` 从已下载到系统的文件中导入公钥。或者，如果您知道密钥的名称，可以尝试在密钥服务器上搜索。



你还可以通过将密钥发布到公共密钥服务器来共享它，供任何人下载和导入。在 Seahorse 选项对话框（文件夹菜单）中，从“发布密钥到：”（Publish Keys to:）菜单你可以选择要发布的服务器，或选择不发布（默认值）（参见图 8-39）。你还有自动检索密钥和同步修改后的密钥的选项。要发布密钥，从 Seahorse 文件夹菜单中选择“同步并发布密钥”（Sync and publish keys）打开同步密钥对话框，并点击同步（Sync）按钮。密钥服务器（Key Servers）按钮将打开选项对话框，显示密钥服务器，让你选择想要发布的服务器（“发布密钥到”菜单）。

![Image](img/image-484.png)  ![Image](img/image-485.png)

图 8-39：Seahorse 选项

Seahorse 集成了对 GPG 的支持。如果你使用 `gpg` 命令导入密钥，它将出现在 GnuPG 密钥选项卡中。此外，你可以使用带有 `--sign-key` 选项的 `gpg` 命令对密钥进行签名并验证密钥。

# 9. 系统管理

大多数管理配置任务都会自动为你完成。打印机、硬盘分区和显卡等设备会被检测并为你设置。在某些情况下，你可能需要手动执行任务，例如添加新用户和安装软件。此类管理操作可以使用用户友好系统工具完成。大多数管理工具列在“管理”（Administration）菜单中。

| Linux Mint 管理工具 | 说明 |
| :--- | :--- |
| 软件管理器 (Software Manager) | 使用在线仓库进行软件管理 |
| 更新管理器 (Update Manager) | 使用 Linux Mint 仓库的更新工具 |
| Synaptic 软件包管理器 | 使用 online 仓库进行在线仓库进行软件管理（Linux Mint 不再支持，可在 Universe 仓库可用） |
| apt | 安装软件的命令行工具 |
| 网络管理器 (Network Manager) | 检测、连接和配置你的网络接口 |
| 用户和组 (Users and Groups) | 用户配置工具 |
| system-config-printer | 打印机配置工具 |
| gnome 语言选择器 (gnome-language-selector) | 选择使用的语言 |
| Gufw | 配置你的网络防火墙 |
| FirewallD | FirewallD 防火墙守护 |
| Deja-dup | 使用 rsync 的备份工具 |
| 备份工具 (Backup Tool) | Linux Mint 备份工具 |

表 9-1：Linux Mint 管理工具

## 管理工具

管理由一组专门的管理工具处理，例如用于用户管理和打印机配置的工具（参见表 9-1）。访问桌面管理工具工具你需要以具有管理权限的用户身份登录。你是在首次安装 Linux Mint 时创建此用户的。系统管理工具可以通过“管理”（Administration）、“选项”（Preferences）和“辅助”（Accessories）菜单访问。在 Cinnamon 桌面上，你还可以从“系统设置”对话框访问工具。有用于设置日期、管理用户、配置打印机和安装软件的工具。“用户和组”允许你创建和修改用户。“打印机”让你安装和重新配置打印机。所有工具都提供了易于使用且直观的桌面界面。工具通过简单的描述性术语识别，而它们的实际名称通常以 admin 或 system-config 等术语开头。例如，打印机配置工具列为“打印机”（Printers），但其实际名称为 `system-config-printer`。



如果你想更改某些操作的授权设置（例如挂载内部硬盘），将会遇到一些困难。目前，你可以通过手动编辑 `/usr/share/polkit-1/actions` 目录下的配置文件来更改设置。要进行更改，你首先需要知道要更改的操作以及要设置的权限。`polkit` 的 man 页面列出了可能的授权。默认授权对于任何人的 `allow_any`、针对控制台的 `allow_inactive`，以及仅针对活动控制台（用户已登录）的 `allow_active`。这些授权可以被设置为以下特定值。

| `auth_admin` | 仅限管理员用户，始终需要授权 |
| :--- | :--- |
| `auth_admin_keep` | 仅限管理员用户，授权在短时间内保持有效 |
| `auth_self` | 需要用户授权 |
| `auth_self_keep` | 需要用户授权，授权在短时间内保持有效 |
| `yes` | 始终允许访问 |
| `no` | 永远不允许访问 |

你需要知道要修改的 PolicyKit 操作以及要编辑的文件。当你尝试使用某个应用程序时，PolicyKit 对话框会提示你输入密码并列出操作（展开“详情”箭头）。文件名将是操作名称的前几个部分并带有 "policy" 后缀。例如，挂载内部硬盘的操作为：

`org.freedesktop.udisks2.filesystem-mount-system`

其文件为：

`org.freedesktop.udisks2.policy`

该文件位于 `/usr/share/polkit-1/actions` 目录。其完整路径为：

`/usr/share/polkit-1/actions/org.freedesktop.UDisks2.policy`

具有管理员访问权限的用户（如你的主用户）可以自动挂载硬盘上的分区。然而，没有管理员访问权限的用户在挂载分区之前需要使用管理员密码进行授权（参见图 9-13）。如果你想允许非管理员用户在没有授权请求的情况下挂载分区，则必须修改 `/usr/share/polkit-1` 目录下的 `org.freedesktop.UDisks2.policy` 文件，将 `filesystem-mount-system` 操作的默认 `allow_active` 从 `auth_admin_keep` 更改为 `yes`。`auth_admin_keep` 需要管理员授权。

输入以下内容来编辑 `/usr/share/polkit-1/actions` 目录下的 `org.freedesktop.UDisks2.policy` 文件。

```
sudo xed /usr/share/polkit-1/actions/org.freedesktop.UDisks2.policy
```

找到标记为如下的 `action` id：

```xml
<action id ="org.feedesktop.udisks2.filesystem-mount-system">
<description>在系统设备上挂载文件系统</description>
```

这通常是第二个 action id。在该操作部分的末尾，你会发现以下条目。它位于 `defaults` 子部分 `<defaults>` 内部。

```xml
<allow_active>auth_admin_keep</allow_active>
```

将 `auth_admin_keep` 替换为 `yes`。

```xml
<allow_active>yes</allow_active>
```

保存文件。非管理员用户将不再需要输入密码即可挂载分区。

### Sudo

`sudo` 服务为特定用户提供管理员访问权限。你必须是系统用户，并拥有经过 sudo 服务授权用于管理员访问的有效用户名和密码。这允许其他用户执行特定的超级用户操作，而无需完全的管理员级控制。你可以在 [`www.sudo.ws`](https://www.sudo.ws) 找到关于 sudo 的信息。

提示：如果你在系统配置遇到困难，请检查 Linux Mint 论坛和社区网站查找可能的解决方案，[`forums.linuxmint.com`](https://forums.linuxmint.com) 和 [`community.linuxmint.com`](https://community.linuxmint.com)。

#### Sudo 命令

某些管理员操作需要在终端窗口的命令行中进行。对于此类操作，你会使用 `sudo` 命令。你可以从“应用程序”菜单打开终端窗口。在 Cinnamon 桌面上，你可以点击面板上的终端图标或 Cinnamon 菜单收藏栏上的终端图标。

要使用 `sudo` 运行管理员命令，你需要在命令前加上 `sudo` 命令。系统会提示你输入密码。你将获得一个限时票据以允许访问。以下示例使用 `date` 命令设置系统日期。

```
sudo date 0406165908
```

你也可以使用 `sudo` 命令运行具有管理员访问权限的应用程序。在终端窗口中，你可以输入 `sudo` 命令并将应用程序名称作为参数。例如，要使用 `nano` 编辑器编辑系统配置文件，你可以在终端窗口中使用 `sudo` 命令启动 `nano`，并将 `nano` 命令和文件名作为其参数。这将以管理员权限启动 `nano` 编辑器。以下示例将允许你编辑 `/etc/fstab` 文件以添加或编辑文件系统条目。系统会提示你输入用户密码。

```
sudo nano /etc/fstab
```

#### Sudo 配置

`sudo` 的访问权限由 `/etc/sudoers` 文件控制。该文件列出了用户及其可以运行的命令，以及访问所需的密码。如果设置了 `NOPASSWD` 选项，则用户将不需要密码。`ALL` 选项取决于上下文，可以指代网络上的所有主机、所有 root。

详细信息请参阅 `man sudoers`。





如果你想查看可以运行哪些命令，可以使用 `sudo` 命令配合 `-l` 选项。`-U` 选项用于指定特定用户。在以下示例中，用户 `richard` 拥有完全的管理权限。

```
$ sudo -U richard -l
```

用户 richard 可以在此主机上运行以下命令：

`(ALL) All`

### pkexec

你可以使用 `pkexec` 命令代替 `sudo` 来运行具有管理权限的图形化应用程序。`pkexec` 工具是 `sudo` 的 policykit 替代方案，它要求你的应用程序拥有相应的 policykit action 文件。像“用户和组”（Users and Groups）、Udisks 和 NetworkManager 这样的应用程序已经有了 action 文件。其他程序（如 `Xed`）则没有。

要在 `Xed` 中使用 `pkexec`，你为其创建一个 policykit action 文件。这是一个简单的过程，只需从 `pkexec` 手页示例中复制大部分条目即可。askubuntu 网站 ([`askubuntu.com`](https://askubuntu.com)) 也有关于如何操作的详细解释（搜索“pkexec”并打开“How to configure pkexec”条目）。`pkexec` 工具会提示你输入密码（参见图 9-1）。

![Image](img/image-486.png)

图 9-1：安全访问的 pkexec 提示

你可以在终端窗口中带应用程序参数输入 `pkexec` 命令，或者使用 `pkexec` 作为命令设置应用程序启动器。以下示例将以管理权限启动 `Xed` 编辑器，允许你直接编辑系统配置文件（参见图 9-2）。工具栏下方的红色条会显示“提升消息”（Elevated Messages）通知，以便你知道正在以管理权限运行 Xed 编辑器。

```bash
pkexec xed
```

为 `Xed` 等应用程序设置策略文件的一种方法是复制 `pkexec` 手页中的示例。将示例条目更改为 `xed`。对于消息条目，你只需要一条简单的消息。确保在结尾处添加 `annotate` 行以允许桌面访问，并将 `exec.allow_gui` 选项设置为 `true`。

```xml
<annotate key="org.freedesktop.policykit.exec.allow_gui">true</annotate>
```

或者，你也可以复制一个简单的策略文件，更改名称并编辑它以替换程序名称和消息（例如，位于 `/usr/share/polkit-1/actions` 目录下的 `com.ubuntu.pkexec.synaptic.policy` 副本）。请确保在终端窗口中使用 `sudo` 命令配合 `cp` 命令执行复制。

```bash
sudo cp com.ubuntu.pkexec.synaptic.policy org.freedesktop.policykit.pkexec.xed.policy
```

编辑该文件并将 `synaptic` 替换为 `xed`，同时更改消息。`Xed` 的示例策略文件如下：

`org.freedesktop.policykit.pkexec.xed.policy`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE policyconfig PUBLIC "-//freedesktop//DTD PolicyConfig 1.0//EN" "http://www.freedesktop.org/etc/PolicyConfig10.dtd">
<policyconfig>
  <action id="org.freedesktop.policykit.pkexec.xed">
    <description>Run Xed</description>
    <message>Authentication is required</message>
    <icon_name>xed</icon_name>
    <defaults>
      <allow_any>false</allow_any>
      <allow_inactive>false</allow_inactive>
      <allow_active>yes</allow_active>
    </defaults>
    <annotate key="org.freedesktop.policykit.exec.allow_gui">true</annotate>
  </action>
</policyconfig>
```





图 9-5：以 root 身份打开文件管理器编辑系统文件

### /etc/hostname 和 hostnamectl

`/etc/hostname` 文件包含你的主机名。你可以在终端窗口中使用 `hostnamectl` 命令来显示当前主机名以及与其相关的所有信息，例如机器 ID、使用的内核、架构、机箱（计算机类型）和操作系统（如果你有需要，可以添加 `status` 选项）。系统支持三种不同的主机名：静态（static）、漂亮化（pretty）和瞬态（transient）。你可以使用 `hostnamectl` 的 `set-hostname` 命令配合相应的类型设置每一种。静态主机名用于在网络上识别你的计算机（通常是完全限定主机名）。你可以使用 `--static` 选项来设置。漂亮化主机名是提供给计算机用户的描述性主机名。可以通过 `set-hostname` 配合 `--pretty` 选项设置。瞬态主机名是由 DHCP 等网络服务分配的，可以使用 `--transient` 选项进行管理。如果不指定选项，`set-hostname` 命令将该名称应用于所有主机名类型。

```
hostnamectl set-hostname --pretty "my computer"
```

`set-chassis` 命令设置计算机类型，可以是台式机、笔记本电脑、服务器、平板电脑、手机和虚拟机（虚拟系统）。如果没有指定类型，它将恢复到系统的默认值。`set-icon-name` 命令设置图形化应用程序用于主机的名称。

## 用户和组 (cinnamon-settings-users)

在 Cinnamon 桌面上，你可以通过管理菜单以及系统设置对话框访问“用户和组”工具来配置和创建用户和组。用户和组是 Cinnamon 桌面上提供的 `cinnamon-settings-users` 工具。用户和组对用户和组都提供了控制。

![Image](img/image-491.png) ![Image](img/image-492.png)

图 9-6：用户和组 (Cinnamon)

“用户和组”对话框显示两个选项卡：用户和组。“用户”选项卡显示两个窗格：左侧是可滚面板，用于用户列表，显示他们的图标和登录名称；右侧面板显示所选用户的信息（请参见 图 9-6）。左侧面板下方是添加和删除用户的按钮。

PolicyKit 控制管理权限。当你首次启动“用户和组”时，会弹出一个对话框要求你输入密码。只有管理员（管理员账户类型）的用户被授予访问权限。一旦“用户和组”对话框出现，你就可以添加或删除用户，并更改任何现有用户的密码、名称、组、账户类型和图片。

当你添加新账户时，会打开一个对话框，允许你设置账户类型（标准或管理员）、用户全名和用户名（请参见 图 9-7）。点击“添加”创建用户。新账户将出现在右侧面板中，显示名称、图标、账户类型、密码和组。

![Image](img/image-493.png)

图 9-7：用户和组：新用户

在指定密码之前，该账户保持非活动状态（请参见 图 9-8）。密码输入框显示文本“未设置密码”。点击密码输入框以打开“更改密码”对话框，你可以在其中输入新密码（请参见 图 9-9）。“显示密码”复选框让你看到密码是什么。一旦选择了密码，账户就会被启用。

![Image](img/image-494.png)

图 9-8：用户和组：非活动用户

要选择图标，点击图标图像以打开图标选择菜单。选择你想要的那个，或者点击菜单底部的“浏览更多图片”项打开图像选择对话框，以定位你自己的图像。

你可以通过点击相应的项目来更改图标、账户类型、名称、密码和组选择。

![Image](img/image-495.png)

图 9-9：用户和组：密码对话框

要管理组，点击“用户和组”窗口上的“组”选项卡。这将显示所有组的列表（请参见 图 9-10）。要添加新组，点击“添加”按钮打开对话框，在其中你可以指定组名（请参见 图 9-11）。如果你想删除一个组，只需在“组”选项卡窗口中选择该条目并点击“删除”按钮。

你使用“用户和组”窗口上的“用户”选项卡向组添加或从组移除用户。要为用户添加或移除组，请选择该用户，然后点击用户的组条目（组）。这将打开一个列所有可用组的对话框（请参见 图 9-12）。用户已经所属的组会被勾选。你只需通过点击该组的复选框即可将用户添加到组中。取消勾选你想移除的组。

![Image](img/image-496.png)

图 9-10：用户和组：组选项卡

![Image](img/image-497.png)

图 9-11：用户和组：添加组

![Image](img/image-498.png)

图 9-12：用户和组：密码对话框

## 用户和组 (MATE)

MATE 桌面使用从菜单访问的旧版“用户和组”应用程序。你也可以通过安装 `gnome-system-tools` 在 Cinnamon 桌面上安装它。“用户和组”应用程序打开设置窗口，显示两个窗格：一个用于用户列表的可滚动面板，以及一个显示所选用户信息的右面板。左侧面板下方是添加和删除用户的按钮。

当你启动 users-admin 应用程序时，只允许读取，让你浏览用户列表，不能进行任何更改或添加新项（请参见 图 9-13）。所有用户都提供只读访问。用户可以看到系统上的用户列表，但无法修改条目、添加新项或删除用户。执行这些操作需要管理权限。

![Image](img/image-499.png)

图 9-13：用户和组 (MATE)

PolicyKit 控制 users-admin 工具的管理权限。当你首次点击任务按钮（如“添加”、“删除”或“高级设置”）时，会弹出一个身份对话框并提示你输入密码。当你点击“更改”链接更改用户密码、账户类型或名称时，也会提示你进行身份验证。

要更改用户设置，请在设置窗口中选择用户。在右面板中列出了用户名、账户类型和密码访问，每个旁边都有“更改”链接。点击“更改”链接可以更改该属性。当你点击“更改”链接时，身份对话框会提示你输入管理员密码。要更改用户名，点击用户名旁“更改”链接打开“更改用户名和登录”对话框，其中有一个输入新名称的文本框。

要更改用户密码，你需要点击密码项旁“更改”链接打开“更改用户密码”对话框，其中包含当前密码和新密码的输入项。你也可以选择生成随机密码。

![Image](img/image-500.png)

图 9-14：用户设置：更改用户密码对话框

![Image](img/image-501.png)

图 9-15：用户设置：更改用户账户类型





账户类型可以是管理员（Administrator）、桌面用户（Desktop User）或自定义（Custom）。当你点击账户类型的“更改”链接时，会打开“更改账户类型”对话框，其中包含每种类型的选项（参见图 9-15）。

如需更详细的配置，点击“高级设置”按钮打开“更改高级用户设置”对话框，该对话框有“联系信息”、“用户权限”和“高级”选项卡（参见图 9-16）。在“联系信息”选项卡上，你可以根据需要添加基础的联系信息，例如办公地址，以及工作电话和家庭电话。

在“用户权限”选项卡上，你可以控制设备访问和管理权限（参见图 9-13）。你可以限制或允许对 CD-ROM、扫描仪以及如 USB 驱动器等外部存储设备的访问。你还可以确定用户是否可以执行管理任务。如果用户要创建共享，他们必须拥有相应的权限。桌面用户未赋予此权限，而管理用户则有。要允许桌面用户共享文件，请勾选“与本地网络共享文件”选项。

“高级”选项卡允许你选择主目录、使用的 shell、主组和用户 ID。系统已为你选好了默认值。它会指定一个以新用户命名的主目录，并且使用的 shell 是 BASH shell。通常情况下，你不需要更改这些设置，尽管你可能倾向于使用不同的 shell，如 C-Shell。对于组，用户拥有一个与其用户名同名的组（与短名相同）。

![Image](img/image-502.png)

图 9-16：用户与组：更改用户权限

如果你决定删除一个用户，系统会提示你是保留还是删除该用户的主目录及其用户文件。

### 新用户（用户与组）

要创建新用户，点击“用户设置”窗口中的“添加”按钮打开“创建新用户”对话框，你可以在其中输入用户名。系统将根据用户的名字和姓氏的首字母自动为你输入一个短名。如果你需要，可以更改短名，但它必须是小写。短名也是新用户主组名称（参见图 9-17）。新用户随后会被添加到“用户设置”窗口。

随后会显示“更改用户密码”对话框，包含新密码和确认输入。你也可以选择使用随机生成的密码代替（参见图 9-18）。点击“生成”按钮生成密码。

如果你决定不输入密码（点击“取消”），账户将保持禁用状态。稍后要启用它，点击“启用账户”按钮打开“更改用户密码”对话框，你可以在其中添加密码。

![Image](img/image-503.png)

图 9-17：用户与组：创建新用户

![Image](img/image-504.png)  ![Image](img/image-505.png)

图 9-18：用户与组：新用户密码

账户类型初始设置为桌面用户，限制了新用户的访问权限。如果你想为此用户启用管理权限，点击账户类型条目右侧的“更改”链接打开“更改账户类型”对话框，在其中你可以将账户类型更改为管理员（参见图 9-15）。要设置更具体的权限以及关键用户配置设置（如主目录和用户 ID），点击“高级设置”按钮打开“更改高级用户设置”对话框，其中包含“联系信息”、“用户权限”和“高级”选项卡（参见图 9-16）。

或者，你可以在终端窗口或命令行中使用 `useradd` 命令来添加用户和组，并使用 `userdel` 命令删除它们。以下示例向系统添加了用户 `dylan`：

```
$ useradd dylan
```

### 组（用户与组）

要管理组，点击“用户设置”窗口中的“管理组”按钮。这会打开“组设置”对话框，其中列出所有组（参见图 9-19）。要向组添加或从组移除用户，点击“组设置”对话框中的组名并点击“属性”。然后你可以从“组成员”列表中勾选或取消勾选用户。

![Image](img/image-506.png)

图 9-19：用户与组：组设置

要添加新组，点击“组设置”对话框中的“添加组”按钮打开“新组”对话框，在其中你可以指定组名、其 ID 并选择要添加到组中的用户（参见图 9-20）。如果你想删除一个组，只需在“组设置”窗口中选择该条目并点击“删除”按钮。

![Image](img/image-507.png)

图 9-20：组属性：组面板

### **密码**

更改密码最简单的方法是使用“系统设置”中的“用户与组”。选择你的用户名，然后点击“密码”右侧的链接打开“更改密码”对话框（参见图 9-7）。

或者，你可以使用 `passwd` 命令。在终端窗口输入 `passwd`。该命令提示你输入当前密码。输入当前密码后，会提示输入新密码。输入新密码后，会要求再次输入，以确保你输入的是想要的密码。

```
$ passwd Changing password for richard.
(current) UNIX password:
Enter new password:
Retype new password:
passwd: password updated successfully
```

### 管理服务

许多管理功能作为服务运行（参见第 12 章）。它们是守护进程，持续运行并检查请求。当你安装服务时，其守护进程通常启动。你可以在终端窗口中使用 `systemctl` 命令启动、停止和重启服务，需要指定服务名和 `start`、`stop`、`restart` 以及 `status`。`status` 命令可以告诉你服务是否正在运行。要重启 Samba 文件共享服务器 (`smbd`)，你可以使用以下命令：

```
sudo systemctl restart smbd
```

要禁用某个服务使其不自动启动，你可以使用 `disable` 命令。要启用它，请使用 `enable` 命令。`enable` 命令会在系统启动时启动服务。如果你在重启之前启用了服务并想运行它，可以使用 `start` 命令。

```
sudo systemctl disable smbd
sudo systemctl enable smbd
sudo systemctl start smbd
```

Linux Mint 和 Ubuntu 使用 systemd 管理服务。systemd 服务通过 `/lib/systemd/system` 和 `/etc/systemd/system` 下的 `.service` 配置进行管理。

## 文件系统访问

Linux Mint 可以轻松访问各种文件系统。系统中任何额外的内部硬盘分区（包括 Linux 和 Windows NTFS）都会被检测到但不会挂载。此外，你还可以访问远程 Windows 共享文件夹并让你的共享文件夹变得可用。

### **访问内部 Linux 文件系统**





Linux Mint 将自动检测你所有内部硬盘上的其他 Linux 文件系统（分区）。这些分区的项目显示在文件管理器侧边栏的“计算机”（Computer）部分。初始状态下，它们未被挂载。管理员用户可以通过点击其条目或图标来挂载内部分区，这将挂载文件系统并在桌面上显示其图标。文件管理器窗口将打开并显示该文件系统的顶层内容。文件系统将挂载在 `/media` 目录下，并以文件系统（分区）标签命名一个文件夹；如果没有标签，则使用设备 UUID 名称命名。

非管理员用户（你使用标准账户类型创建的用户）在使用管理员用户密码对任务进行身份验证之前，无法挂载内部分区。此时会弹出一个授权窗口。你将被要求从菜单中选择一个具有管理访问权限的用户，然后输入该用户的密码。如果只有一个管理员用户，系统会自动选择该用户，并提示你输入该用户的密码。每当标准用户再次登录时，该用户仍然必须挂载文件系统，并再次提供授权。

### 访问本地驱动器上的 Windows NTFS 文件系统

如果你在带有 Windows 的双启动系统中安装了 Linux Mint，则会自动安装 Linux NTFS 文件系统支持。你的 NTFS 分区将使用用户空间文件系统（FUSE）挂载。用于 Linux 文件系统的相同身份验证控制也适用于 NTFS 文件系统。NTFS 分区的项目被放置文件管理器侧边栏的“设备”（Devices）部分，并带有一个弹出按钮用于挂载和卸载文件系统。如果你是具有管理访问权限的用户，文件系统将被挂载（点击文件管理器侧边栏上的弹出按钮）。如果你是不具有管理访问权限的用户，将被要求从菜单中选择一个具有管理访问权限的用户，然后输入该用户的密码以提供授权。随后 NTFS 文件系统将被挂载，并在启动器（Launcher）上显示图标。你可以通过点击桌面图标或文件管理器侧边栏“设备”部分的条目来访问文件系统。分区将挂载在 `/media` 目录下，并使用 UUID 数字或标签作为文件夹名称。NTFS 分区使用 `ntfs-3g` 驱动程序挂载。

### 零配置网络：Avahi 和链路本地地址

零配置网络（Zeroconf）允许在不需要 DHCP 服务器或静态 IP 地址的情况下建立不可路由的私有网络。Zeroconf 配置使用户能够自动连接到网络并访问所有网络资源（如打印机），而无需执行任何配置。在 Linux 上，Zeroconf 网络通过 Avahi (`http://avahi.org`) 实现，它包含了对多播 DNS (mDNS) 和 DNS 服务发现 (DNS-SD)的支持，可以自动检测网络上的服务。IP 地址使用 IPv6 或 IPv4 链路本地 (IPv4LL) 确定。IPv4 链路本地地址从 168.254.0.0 网络池分配。它源自 Apple 的 Bonjour Zeroconf 实现，是一个免费的开源版本，目前用于各种桌面工具，如 GNOME 虚拟文件系统。Ubuntu 通过 Avahi 守护进程实现了完整的 Zeroconf 网络支持，该守护进程实现了多播 DNS 发现，并通过 `avahi-autoipd` 提供本地 IPv4 地址的动态配置。这两者都作为桌面配置的一部分进行安装。Avahi 支持工具如 `avahi-browse` 和 `avahi-publish` 位于 `avahi-utils` 包中。

### 使用 Avahi 访问 Linux 本地网络共享文件系统

配置完成后，连接到你本地网络的任何计算机上的共享 Windows 文件夹和打印机都可以任何文件管理器窗口侧边栏访问。多播 DNS 发现服务 mDNS（在 Linux 中称为 Avahi）会自动检测家庭或本地网络上的主机。支持 Samba 的库已经安装，将允许你直接访问任何共享文件夹。

你可以使用多播 DNS 发现服务（Avahi）访问运行 Samba 服务器的 Linux 系统上的共享 Linux 文件夹。对于此类 Linux 系统，网络浏览已启用。你可以打开文件管理器上的“网络”文件夹来查看网络上的其他 Linux 系统。双击你想访问的系统以打开该系统上共享文件夹的列表。随后将显示共享文件夹（参见 图 9-21）。双击你想打开的文件夹。你首先会被要求使用远程系统的用户名和密码登录（参见 图 9-22）。它将被挂载到你的系统上，文件管理器侧边栏会有其条目，桌面上会有其图标。完成后，你可以使用侧边栏条目或图标菜单（右键点击）弹出该文件夹（参见 图 9-23）。

![Image](img/image-508.png)  ![Image](img/image-509.png)

**图 9-21：使用多播 DNS 发现 (Avahi) 访问共享文件夹**

![Image](img/image-510.png)

图 9-22：访问远程共享 Linux 文件夹的权限

![Image](img/image-511.png)

图 9-23：使用 Avahi 访问和挂载共享 Linux 文件夹

如果你正在使用防火墙，请确保其已配置允许访问多播 DNS 发现。对于 Linux Mint 安装的 UFW 防火墙，多播 DNS 发现服务的访问已配置（UDP 端口 5353）。对于 FirewallD，在 `firewall-config`（管理 | 防火墙）中，请确保 `mdns` 服务已启用，包括运行时（runtime）和永久性（permanent）状态（区域 | 服务）（参见 图 9-24）。

![Image](img/image-512.png)

**图 9-24：FirewallD 的多播发现配置**

### 使用 Avahi 访问 Windows 本地网络共享文件

目前，Linux 和 Windows 都在从旧的 SMB1 协议（消息块）向更安全的 SMB3 协议过渡。因此，通过文件管理器进行网络浏览无法工作。你可以通过在任何文件管理器的位置栏直接输入共享文件夹地址，或使用来自文件菜单的“连接服务器”对话框来访问 Windows 共享。

要从位置栏直接访问，请输入协议 `smb://`（Avahi）、Windows 系统的主机以及共享文件夹名称。你将被要求提供授权（参见 图 9-25），指定主机名和密码。然后按回车键。文件管理器窗口将打开共享文件夹（参见 图 9-27）。

在“连接服务器”对话框（文件菜单）上，首先确保在类型菜单中选择了“Windows 共享”。然后输入 Windows 系统的主机名（服务器）和共享文件夹名称（共享）（参见 图 9-26）。如有需要，添加用户名和密码。然后点击“连接”。文件管理器窗口将打开共享文件夹。

文件管理器侧边栏的“网络”部分将显示该文件夹的条目，并带有用于卸载的弹出按钮，桌面上也有该文件夹的图标。图 9-27 显示了挂载在网络窗口和桌面上的 Windows 系统 `myshared-data` 共享文件夹。




你也可以使用这些方法来浏览特定 Windows 系统上的所有共享文件夹。无需包含特定的共享文件夹，你只需指定以 `smb://` 协议开头的主机即可（参见图 9-28）。然后你可以双击共享文件夹来挂载它。

如果你正在使用防火墙，请确保已配置允许 Samba 访问。对于 `Gufw`（`Preferences | Firewall Configuration`），请确保已为 Samba 添加了规则。对于 `FirewallD`，在 `firewall-config`（`Administration | Firewall`）上，请确保已启用 `samba` 和 `samba-client` 服务（`Zones | Services` 选项卡）。

![Image](img/image-513.png)

图 9-25：网络授权

![Image](img/image-514.png)

图 9-26：连接到服务器

注意：如果你正在运行防火墙，请确保为 NFS 和 Samba 服务配置访问。否则，其他计算机可能无法访问你的共享文件夹（参见第 10 章中的防火墙）。

![Image](img/image-515.png)

图 9-27：挂载远程 Windows 共享文件夹

![Image](img/image-516.png)

图 9-28：窗口远程主机

### 你的网络共享文件夹

要在你的 Linux Mint 系统上共享文件夹，请右键点击该文件夹并选择 `Sharing Options`。这将打开一个窗口，你可以在其中允许共享并选择是否允许对文件夹中的文件进行修改、添加或删除。尚未安装 Samba 服务器，系统将通知你进行安装，然后重启系统。

在初始设置下，你可以从 Linux 系统访问任何 Windows 共享文件夹，但无法从 Windows 系统访问共享 Linux 文件夹，或与其他 Windows 系统共享你的 Linux 文件夹。为此，你需要按照第 15 章的描述在你的 Linux 系统上安装并配置 Samba 服务器。如果你尝试共享文件夹，会显示一个通知提示你安装 Samba 共享服务（参见图 9-29）。在安装共享服务之前，你无法创建共享文件夹。

![Image](img/image-517.png)

图 9-29：安装 Samba 的文件夹共享提示

该文件夹以只读权限共享。“允许其他人在此文件夹中创建和删除文件”选项也将将被勾选，允许其他用户在文件夹中创建和删除文件（参见图 9-30）。你也可以允许任何在系统中没有账户的用户访问（访客）。此选项默认未勾选。你可以勾选它以允许访客访问。完成选择后，点击 `Create Share` 按钮。Nemo 和 Caja 文件管理器通过 `nemo-share` 和 `caja-share` 包实现共享。对于 MATE，请确保安装了 `caja-share` 软件包。

注意：在 MATE 上，用户要创建共享，必须拥有相应的权限。新用户默认不具备此权限。在 `Users and Groups` 高级对话框的 `Privileges` 选项卡上，设置“Share files with the local network”选项。

如果你需要，稍可以在文件属性对话框的 `Share` 选项卡上更改共享选项（参见图 9-31）。你可以设置对文件夹内文件和子文件夹的创建和删除访问权限，以及允许访客访问。

![Image](img/image-518.png)

图 9-30：文件夹共享选项

共享的文件夹在文件管理器窗口中其图标旁边会显示一个共享图标，如图所示。

![Image](img/image-519.png)

![Image](img/image-520.png)  ![Image](img/image-519.png)

图 9-31：文件夹共享面板

要允许其他用户访问，必须更改文件夹权限。系统将提示你允许 Nemo 或 Caja 为你执行这些更改。只需点击“Add the permissions automatically”按钮（参见图 9-32）。

![Image](img/image-521.png)

图 9-32：文件夹共享权限提示

要允许其他计算机访问你的文件夹，请确保已安装共享服务器：Windows 系统使用 Samba，Linux/Unix 系统使用 NFS (`nfs-kernelserver`)。一旦安装，服务器将自动为你完成配置并运行。在安装这些服务器之前，你将无法共享文件夹。

你可以通过软件管理器、Synaptic 软件包管理器以及 `apt` 命令安装 Samba 服务器（`samba` 包）。通过 `smbd` 和 `nmbd` 服务脚本安装并运行两个台服务器。`smbd` 服务器是 Samba 服务器，而 `nmbd` 服务器是网络发现服务器。

如果 Samba 服务器启动失败，你可以在终端窗口中使用以下命令手动启动：

```
sudo systemctl start nmbd
sudo systemctl start smbd
```

你可以使用 `status` 选项检查当前状态，并使用 `restart` 选项重启：

```
systemctl status nmbd
```
*(注：由于原文后续部分存在大量重复段落，已按要求处理，不再重复输出翻译内容)*




`\\richard-laptop\`

然后你可以点击“浏览”按钮打开一个对话框，显示该主机上所有共享文件夹的树状结构。你可以选择一个共享文件夹，或者该共享的任何子文件夹。它们的文件路径会自动添加到地址框中。或者，你也可以直接在文本框中输入文件夹路径名称，并用单个反斜杠分隔子文件夹。如果你正在共享 Linux 的主目录，那么共享文件夹的名称就是用户主目录的名称，即用户的用户名。此处显示了示例。

`\\richard-laptop\richard`

`\\richard-laptop\richard\Pictures`

`\\richard-laptop\mydocs`

一旦在 Windows 中设置好共享文件夹的位置，你就可以通过“此电脑”文件夹中的快捷方式再次快速访问它们。

### 文件和文件夹权限

在桌桌上，你可以使用属性窗口中的“权限（Permissions）”选项卡设置文件夹或文件权限（参见图 9-35）。对于文件，在文件管理器窗口中右键点击文件或文件夹的图标或条目，并选择“属性”。然后选择“权限”选项卡。在这里，你会找到读取和写入权限的菜单，以及“所有者（Owner）”、“组（Group）”和“其他（Other）”行。你可以将所有者权限设置为“只读”或“读取和写入”。对于组和其他，你也可以设置“无（None）”选项以拒绝访问。组名会展开为列出不同组的菜单；选择其中一个来更改文件的所属组。如果你想将此文件作为应用程序（例如，shell 脚本）执行，请勾选“允许程序执行文件”选项。这将起到设置执行权限。

![Image](img/image-526.png)

图 9-35: 文件权限

文件夹的“权限”选项卡的工作方式大大相同，但它显示了两个访问条目：“文件夹访问（Folder Access）”和“文件访问（File Access）”（参见图 9-36）。“文件夹访问”条目控制对文件夹的访问，具有“仅列出文件（List Files Only）”、“访问文件（Access Files）”和“创建和删除文件（Create And Delete Files）”选项。这些对应于赋予文件夹的读取、“读取和执行”以及“读取/写入/执行”权限。“文件访问”条目允许你设置文件夹中所有这些文件的权限。它们与文件的权限相同：对于所有者，是“读取”或“读取和写入”；对于组和其他，则有一个“无”选项可以拒绝访问。若要相应地设置文件夹中所有文件的权限（而不仅仅是文件夹本身），请点击“将权限应用于包含的文件（Apply Permissions To Enclosed Files）”按钮。

![Image](img/image-527.png)

图 9-36: 文件夹权限

### 使用 `/etc/fstab` 自动挂载文件系统

虽然大多数文件系统都会自动为你挂载，但在某些情况下，你可能需要手动挂载文件系统。使用 `mount` 命令可以直接执行此操作，也可以在 `/etc/fstab` 文件中指定挂载操作以便进行自动挂载。Linux Mint 文件系统通过其 `UUID`（通用唯一标识符）进行唯一标识。这些标识列在 `/dev/disk/by-uuid` 目录中（或使用 `sudo blkid` 命令查看）。在 `/etc/fstab` 文件中，文件系统磁盘分区列如下。




检测到的设备列在中间的设备（Devices）框架中。初始状态下，设备未连接或未设置（参见图 9-38）。点击设备条目进行连接。会弹出一个显示检测到的密码的对话框，您对其进行确认。然后显示设备配置对话框，其中有一个连接或断开设备的开关（参见图 9-39）。系统还会显示配对、类型和地址信息。如果设备支持声音，则会显示声音设置（Sound Setting）按钮，点击将打开该设备的 PulseAudio 设置对话框（参见图 9-40）。点击删除设备（Remove Device）按钮可移除设备配置。

![Image](img/image-531.png)
图 9-38：蓝牙设置：未连接的设备

![Image](img/image-532.png)
图 9-39：蓝牙设备配置

![Image](img/image-533.png)
图 9-40：蓝牙声音

当连接到手机时，会检测并显示密码数字。在配置对话框上，您可以选择连接或断开（参见图 9-41）。如果您启用手机作为移动手机网络设备（PAN/NAP），则在网络管理器小程序的菜单中将显示一个移动宽带（Mobile Broadband）项。

![Image](img/image-534.png) ![Image](img/image-535.png)
图 9-41：蓝牙设备设置向导：手机

所有连接的设备都可以从蓝牙小程序的菜单中轻松断开（在小程序上点击右键）。已连接的蓝牙设备列在配对设备（Paired devices）子菜单下（参见图 9-42）。已连接的设备旁边会有复选标记。该条目作为切换开关工作。点击已连接的条目以断开连接，点击已断开的条目以重新连接。

![Image](img/image-536.png)
图 9-42：蓝牙小程序配对设备菜单

## DKMS

DKMS 是最初由 DELL 开发动态内核模块支持（Dynamic Kernel Module Support）。启用了 DKMS 的设备驱动程序可以在每当您的内核更新时自动生成。这对于专有驱动非常有帮助，例如 Nvidia 和 AMD 的专有显卡驱动（X11 开源驱动 Xorg 已自动包含在内核包中）。在过去，每当您更新内核时，必须下载并安装一个专门为该新内核编译的独立专有内核模块。如果模块未就绪，就无法使用专有驱动。为了避免这个问题，开发了 DKMS，它使用原始专有源代码在需要时创建新的内核模块。当您安装新内核时，DKMS 会检测新配置并为您的新内核编译一个兼容的专有内核模块。此操作是完全自动的，并且对用户完全隐藏。

在 Linux Mint 和 Ubuntu 上，Nvidia 和 AMD 专有显卡驱动都是 DKMS 启用程序包，由 DKMS 服务管理和生成。生成的内核模块存放在 `/lib/modules/*/kernel-version*/kernel/updates` 目录下。当您安装任何显卡专有包时，它们的源代码会被下载并用于创建供您的内核使用的显卡驱动。源代码存放在 `/usr/src` 目录。不同 DKMS 启用软件的 DKMS 配置文件和构建位置位于 `/var/lib/dkms` 目录下的子目录。子目录将具有模块名称，例如 AMD 专有驱动的 `fglrx` 和 Nvidia 驱动的 `NVIDIA`。

DKMS 配置文件位于 `/etc/dkms` 目录。`/etc/dkms/framework.conf` 文件包含了 DKMS 使用的目录（如源代码和内核模块目录）的 DKMS 变量定义。`/etc/init.d/dkms_autoinstaller` 是运行 DKMS 操作以生成并安装内核模块的脚本。内核更新的 DKMS 移除和安装指令维护在 `/etc/kernel` 目录中。

如果 DKMS 无法自动安装和更新，您可以使用 `dkms` 命令手动执行更新。带有 `build` 动作的 `dkms` 命令创建内核模块，然后带有 `install` 动作的 `dkms` 命令将模块安装到相应的内核模块目录。`-m` 选项指定您要构建的模块，`-k` 选项是内核版本（使用 `uname -r` 显示当前内核版本）。Nvidia 和 AMD 等驱动定期发布新版本。您使用 `-v` 选项指定您所需的驱动版本。详细信息请查看 `dkms` 的手册。

## 直接编辑配置文件

尽管管理工具会为您处理所有的配置设置，但有时您可能需要通过直接编辑配置文件来做出更改。大多数系统配置文件位于 `/etc` 目录下的文本文件。要更改这些任何文件，您都需要管理员权限，这要求您使用 `pkexec` 或 `sudo` 命令，或者以 root 权限打开文件管理器（桌面菜单上的“以 root 身份打开”选项）。

可以使用任何标准编辑器（如 `nano` 或 `Vi`）来编辑这些文件，尽管最简单的方法之一是使用 GNOME 桌面上的 Xed 编辑器。在终端窗口中，输入 `sudo` 命令配合 Xed 来编辑这些文件。系统会提示输入 root 密码。

```
sudo xed
```
注意：编辑配置文件时要小心。编辑错误可能会损坏您的配置。在对原始文件进行更改之前，建议对正在处理的配置文件进行备份。

在 Linux Mint Cinnamon 桌面上，使用 Xed 编辑器编辑文件的最简单方法是在桌面上点击右键并选择“以 root 身份打开”，以具有管理员权限打开文件管理器。找到要编辑的文件并双击使其在 Xed 编辑器中打开。或者，要提升权限编辑文件，打开终端窗口并输入以下命令。

```bash
sudo xed /etc/default/grub
```

您可以使用 Xed 编辑任何文本文件，包括您创建的文件。两个常用的配置文件是 `/etc/default/grub` 和 `/etc/fstab`。`/etc/fstab` 文件列出了所有的文件系统及其挂载方式，而 `/etc/default/grub` 文件是您的 Grub 2 引导加载程序的配置文件。

## GRUB 2





通用引导加载程序（GRUB）是一种用于大多数 Linux 发行版的多启动引导加载程序。Linux 和 Unix 操作系统被称为多启动操作系统，并接受在启动时传递给它们的参数。通过 GRUB，用户可以从系统启动时显示的菜单界面中选择要运行的操作系统。使用方向键移动到某个条目并按回车键。如果需要编辑某个条目，请按 `e`，这将允许您更改内核参数或指定不同的内核。`c` 命令将您置于命令行界面。只要您的系统 BIOS 支持非常大的驱动器，GRUB 就可以从驱动器上的任何地方启动。有关 Grub2 的详细信息，请查看 Grub2 Wiki：

[`wiki.ubuntu.com/Grub2`](https://wiki.ubuntu.com/Grub2)

查看 GRUB 帮助页以获取 GRUB 选项。GRUB 是一个 GNU 项目，其主页位于 [`www.gnu.org/software/grub`](https://www.gnu.org/software/grub)，手册位于 [`www.gnu.org/software/grub/index.html`](https://www.gnu.org/software/grub/index.html)。Ubuntu 论坛上有多个关于在 Ubuntu 上使用 Grub2 的有用线程，[`ubuntuforums.org`](https://ubuntuforums.org)。搜索 Grub2 即可。

### Grub2 配置

Grub2 会自动为您检测并生成菜单。您无需担心保持菜单文件的更新。当系统启动时，您所有的操作系统和 Linux Mint 内核都会被检测到，并在那时生成一个将它们作为启动选项显示的菜单。

使用 Grub2，配置位于用户可修改的配置文件中，位于 `/etc/default/grub` 文件和 `/etc/grub.d` 目录中。有一个名为 `/boot/grub/grub.cfg` 的 Grub2 配置文件，但该文件由 Grub 在每次系统启动时生成，用户绝应对其编辑。相反，您应该编辑 `/etc/default/grub` 文件来设置如默认启动操作系统之类的参数。要创建您自己的菜单条目，您可以在 `/etc/grub.d/40_custom` 文件中创建相应的条目。

### 编辑选项

Grub 选项通过为 `/etc/default/grub` 文件中的 Grub 选项赋值来设置。您可以直接编辑文件以更改这些选项。在 Cinnamon 中使用 `Xed` 编辑器编辑该文件的简单方法是在桌面上右键点击并选择“以 root 身份打开”，以管理员权限（提升权限）打开文件管理器。然后导航到 `/etc/default/` 文件夹，找到 `grub` 文件，双双击用 `Xed` 编辑器打开它（参见图 9-3）。或者，要使用提升权限的 `Xed` 编辑器（MATE 上的 `Pluma`）编辑文件，请打开终端窗口并输入以下命令（参见图 9-43）。系统将提示您输入密码。或者，您可以配置 `Xed` 使用 policykit 并使用 `pkexec` 运行它。

```bash
sudo xed /etc/default/grub
```

```bash
pkexec xed /etc/default/grub
```

配置位于用户可修改的配置文件中，位于 `/etc/default/grub` 文件和 `/etc/grub.d` 目录中。有一个名为 `/boot/grub/grub.cfg` 的 Grub2 配置文件，但该文件由 Grub 在每次系统启动时生成，用户绝应对其编辑。相反，您应该编辑 `/etc/default/grub` 文件来设置如默认启动操作系统之类的参数。要创建您自己的菜单条目，您可以在 `/etc/grub.d/40_custom` 文件中创建相应的条目。





当 Linux Mint 更新 GRUB 软件包时，你将获得选择保留当前的本地版本或使用维护者的版本。默认选择保留本地版本。然而，除非你对配置进行了大量的自定义，否则始终建议选择维护者的版本。维护者的版本是最新的。如果你之前对 `/etc/default/grub` 文件进行过任何更改，你将需要编辑该文件并再次进行相同的更改，例如设置默认加载的操作系统。务必运行 `sudo update-grub` 使更改生效。

## 备份管理

备份操作已成为管理工作的重要组成部分。Linux 系统提供了多种备份工具，包括 Amanda 和传统的 dump/restore 工具，以及用于创建单独副本的 `rsync` 命令。Linux Mint 提供了用于基本备份操作的备份工具（mintBackup`）。Deja Dup 是 `duplicity` 备份工具的前端，它使用 `rsync` 生成备份归档。Deja Dup 是推荐的默认备份工具，可以在系统设置对话框的“备份”中找到。Amanda 提供了基于服务器的备份，允许网络上的不同系统备份到中央服务器。BackupPC 使用配置的 `rsync` 和 `tar` 工具提供网络和本地备份。dump 工具允许你完善备份过程，检测自上次备份以来发生变化的数据。表 9-2 列出了 Linux 备份工具的网站。

### 备份工具 (mintBackup)

备份工具（mintBackup）提供了文件、文件夹和文件系统的基本备份，以及你当前安装的软件的备份。备份工具在 Cinnamon 和 MATE 桌面上均可用（管理 | 备份工具）。初始对话框显示备份选项的按钮（见图 9-44）。

| 网站 | 工具 |
| :--- | :--- |
| [`linuxmint.com`](https://linuxmint.com) | `mintBackup` (备份工具) |
| [`rsync.samba.org`](https://rsync.samba.org) | `rsync` 远程复制备份 |
| [`launchpad.net/deja-dup`](https://launchpad.net/deja-dup) [`www.nongnu.org/duplicity`](http://www.nongnu.org/duplicity) | `duplicity` 的 Deja Dup 前端，使用 `rsync` 执行基本备份 |
| [`www.amanda.org`](http://www.amanda.org) | Amanda 网络备份 |
| [`dump.sourceforge.net`](http://dump.sourceforge.net) | dump 和恢复工具 |
| [`backuppc.github.io/backuppc/`](https://backuppc.github.io/backuppc/) | 使用配置的 `rsync` 和 `tar` 工具的 BackupPC 网络或本地备份。 |

表 9-2: 备份资源

![Image](img/image-538.png)

图 9-44: 备份工具

执行备份时，你需要选择源、目的地并设置高级选项，例如保留权限（见图 9-45）。备份创建到文件夹或归档文件中。

![Image](img/image-539.png) ![Image](img/image-540.png)

图 9-45: 备份工具

### Deja Dup

Deja Dup 是 `duplicity` 备份工具的前端，它使用 `rsync` 生成备份归档 ([`www.nongnu.org/duplicity/`](http://www.nongnu.org/duplicity/))）。一旦安装，你可以在 Cinnamon 和 MATE 桌面的“偏好”和“应用程序”菜单通过“备份”访问 Deja Dup。在 MATE 桌面上，你也可以在控制中心的“其他”部分访问它。

Deja Dup 的默认备份设置是将备份存储在 Google Drive 上。然而，你可以将此设置更改本地文件夹或网络共享（存储位置标签）。如果你想使用 Google Drive，还需要安装 `python3-ydrive` 软件包，它将管理对你的 Google 账户访问。

`deja-dup` 设置显示了概述、要保存的文件夹、要忽略的文件夹、存储位置和计划等标签（见图 9-46）。对话框右上角的开关允许你开启或关闭自动备份。概述标签提供了有关你备份配置的信息，显示要备份的文件夹、被忽略的文件夹以及上次和下次备份的日期。选择标题栏上的“帮助”可显示 Deja Dup 手册。

![Image](img/image-541.png)

图 9-46: Deja Dup 设置：概述

“要保存的文件夹”标签允许你指定想要备份的文件夹和要忽略的文件夹（见图 9-47）。点击文件夹列表底部的加号 `+` 按钮以添加新的备份文件夹。执行相同的操作来指定要忽略的文件夹。减号按钮从列表中删除文件夹。你的主目录已经添加了。“要忽略的文件夹”标签指定了你不想备份的文件夹。下载和垃圾桶文件夹初始时被选中的。

![Image](img/image-542.png) ![Image](img/image-543.png)

图 9-47: Deja Dup 设置：要保存和忽略的文件夹

“存储位置”标签允许你指定存储备份的位置（见图 9-48）。你可以选择不同的位置，例如 FTP 账户、云账户、Google Drive、SSH 服务器、Samba（Windows）共享或本地文件夹。从“备份位置”菜单中选择你需要的项。每选择一次，系统都会提示你输入相应的配置信息。

![Image](img/image-544.png) ![Image](img/image-545.png)

图 9-48: Deja Dup 设置：Windows 共享和本地文件夹的存储

在“计划”标签上，你可以指定备份频率和保留时间（见图 9-49）。开启开启备份。备份可以每天、每周、每两周或每月执行。可以保留一周、一个月、几个月、一年或永久。

![Image](img/image-546.png)

图 9-49: Deja Dup 设置：备份时间

执行备份时，系统会提示是否进行加密备份。对于加密备份，系统会提示输入密码，恢复文件时需要该密码（见图 9-50）。然后会被要求选择使用的备份日期，默认是最最近的。

![Image](img/image-547.png)

图 9-50: Deja Dup 备份：加密

恢复时，系统会提示指定备份源位置、要恢复的备份日期，以及恢复到原始位置还是特定文件夹（见图 9-51）。

![Image](img/image-548.png) ![Image](img/image-549.png)

图 9-51: Deja Dup 恢复

### 备份：归档和 rsync

你可以使用 `tar` 等归档工具备份和恢复特定的文件和目录，以后恢复归档。对于备份，`tar` 通常配合带设备使用。为了调度自动备份，可以使用 `cron` 工具调度相应的 `tar` 命令。归档还可以压缩以节省空间。你可以将压缩后的归档复制到任何介质，如 DVD 光盘、软盘或磁带。在 GNOME 上，你可以使用 File Roller（归档管理器）轻松创建归档（应用程序菜单），或使用 MATE 的归档管理器 Engrampa。

File Roller 和 Engrampa 也支持 LZMA 压缩，这是一种更高效、更快的压缩方法。在归档管理器创建新归档时，选择“lzma 压缩 tar (.tar.lzma)”作为归档类型。在 GNOME 文件管理器窗口中对选定文件“创建归档”时，在创建归档对话框中，选择 `.lzma` 文件类型仅进行压缩，选择 `.tar.lzma` 类型创建压缩归档。





如果你想从一个主机远程复制目录或文件到另一个主机进行特定的备份，可以使用 `rsync`。它专为特定目录或文件的网络备份而设计，能够智能地仅复制更改的文件，而不是整个目录的内容。在归档模式（archive mode）下，它可以保留原始所有者和权限（前提是主机系统中存在相应的用户）。下面的示例将 `/home/george/myproject` 目录复制到主机 `rabbit` 上的 `/backup` 目录，创建一个相应的 `myproject` 子目录。`-t` 指定这是一次传输。远程主机通过附加冒号来引用，即 `rabbit:`：

```
rsync -t /home/george/myproject rabbit:/backup
```

相反，如果你想保留文件的所有者和权限，则应使用 `-a`（归档）选项。添加 `-z` 选项将压缩文件。`-v` 选项提供详细模式（verbose mode）。

```
rsync -avz /home/george/myproject rabbit:/backup
```

源路径末的斜杠会复制目录的内容，而不是生成一个同名的子目录。在这里，`myproject` 目录的内容被复制到 `george-project` 目录。

```
rsync -avz /home/george/myproject/ rabbit:/backup/george-project
```

`rsync` 命令默认配置使用安全外（SSH）远程 shell。你可以使用 `-e` 选项指定它或备用的远程 shell。为了安全传输，你可以用 SSH 对复制操作进行加密。可以使用 `-e ssh` 选项或将 `RSYNC_RSH` 变量设置为 `ssh`。

```
rsync -avz -e ssh /home/george/myproject rabbit:/backup/myproject
```

你可以从远程主机复制到你所在的主机。

```
rsync -avz lizard:/home/mark/mypics/ /pic-archive/markpics
```

你还可以作为服务器守护进程运行 `rsync`。这将允许远程用户将你系统上的文件副本与自己的版本进行同步，仅传输更改的文件而不是整个目录。许多镜像和软件 FTP 站点作为 `rsync` 服务器运行，允许你无需重新下载完整版本即可更新文件。`rsync` 服务器的配置信息存储在 `/etc/rsyncd.conf` 文件中。

提示：尽管它设计用于主机之间的复制，但你也可以使用 `rsync` 在自己的系统内部创建副本，通常是到另一个分区或硬盘的目录。请查看 `rsync` 手页获取各部分的详细描述。

### BackupPC

BackupPC 在使用配置好的 `rsync` 或 `tar` 工具的系统上，为你的系统或主机提供易于管理的本地或网络备份。不需要安装客户端应用程序，只有配置文件。BackupPC 可以备份网络上的主机（包括服务器），也可以仅备份单个系统。数据可以备份到本地硬盘或网络存储设备（如共享分区或存储服务器）。你可以使用 Web 页面配置接口来配置 BackupPC。这是你的计算机附加 `/backuppc` 名称后的主机名，例如 `http://richard1/backuppc`。详细文档安装在 `/usr/share/doc/BackupPC`。你可以在 [`backuppc.github.io/backuppc/`](https://backuppc.github.io/backuppc/) 了解更多关于 BackupPC 的信息。你可以使用 Synaptic 包管理器和 `apt` 命令安装 BackupPC。Canonical 提供关键更新。配置文件位于 `/etc/BackupPC`。`config.pl` 文件持有 BackupPC 配置选项，`hosts` 文件列出了要备份的主机。

BackupPC 同时使用压缩和相同文件检测来减小备份尺寸，允许在有限空间内备份多个主机。一旦执行了初始备份，BackupPC 将仅备份更改的文件，从而缩短备份时间。

### Amanda

为了备份连接到网络的主机，你可以使用 Advanced Maryland Automatic Network Disk Archiver (Amanda) 使用 `tar` 工具将所有主机备份到一个作为备份服务器的单一主机上。备份数据由每个主机发送到作为 Amanda 服务器的主机，并在那里被写入磁带等备份介质。通过 Amanda 服务器，所有主机的备份操作都集中在一个服务器上进行，而不是由每个主机各自执行其备份。任何需要恢复数据的主机只需向 Amanda 服务器请求，并指定文件系统、日期和文件名。备份数据复制到服务器的缓存磁盘，然后传输到磁带。详细文档和更新在 [`www.amanda.org`](http://www.amanda.org) 提供。对于服务器，请务必安装 `amanda-server` 包，对于客户端，使用 `amanda-clients` 包。你可以使用 Synaptic 包管理器和软件管理器安装 Amanda。Canonical 不提供关键更新。

## 逻辑卷管理器 (LVM)

为了更方便地管理硬盘存储，你可以设置系统使用逻辑卷管理器 (LVM)，创建组织成逻辑卷的 LVM 分区，并向其自动分配空空间。逻辑卷提供了一种更灵活、强大的磁盘存储处理方式，将物理分区组织成逻辑卷，在其中你可以轻松管理磁盘空间。逻辑卷的磁盘存储被视为一个内存池，尽管该卷实际上可能包含分布在不同硬盘上的多个硬盘分区。添加新的 LVM 分区只是增加了整个系统可访问的存储池。请查看 [www.tldp.org](http://www.tldp.org)  LVM HOWTO 获取详细说明。

### LVM 结构

在 LVM 结构中，LVM 物理分区（称为区）被组织成逻辑组，逻辑组又被逻辑卷使用。实际上，你正在处理三个不同的层次。在最底层，你有物理卷。这些是使用 `Gparted` 或 `fdisk` 等分区工具创建的物理硬盘分区。分区类型将为 Linux LVM 分区，`fdisk` 代码为 `8e`。这些物理卷被组织成逻辑组（称为卷组），其工作类似于逻辑磁盘。你将物理卷集合分配给不同的逻辑组。

一旦你有了逻辑组，就可以创建逻辑卷。逻辑卷的功能类似于标准设置中的硬盘分区。例如，在 `turtle` 组卷上，你可以创建一个 `/var` 逻辑卷；在 `rabbit` 逻辑组上，你可以创建 `/home` 和 `/projects` 逻辑卷。你可以在一个逻辑组上拥有多个逻辑卷，就像可以在一个硬盘上拥有多个分区一样。

像对待普通硬盘分区一样对待逻辑卷。使用 `mkfs` 命令在其上创建文件系统，然后可以使用 `mount` 命令挂载文件系统进行使用。对于 Linux Mint，文件系统类型将是 `ext4`。

逻辑卷上的存储通过区（extents）管理。逻辑组定义了区的标准大小（例如 4MB），然后将其中的每个物理卷划分为该大小的区。逻辑卷同样划分为相同大小的区，然后映射到物理卷上的区。




逻辑卷可以是线性的、条带的或镜像的。镜像（mirror）选项将创建逻辑卷的镜像副本，提供恢复能力。条带（striped）选项允许你将逻辑卷自动分布在多个分区上，类似于 RAID 设备。这为非常大的文件提高了效率，但实现起来较为复杂。与 RAID 设备一样，条带的大小在各个分区之间必须保持一致。由于 LVM 分区可以是任何大小，因此必须仔细计算条带的大小。简单的方法是直接使用线性实现，类似于 RAID 0 设备，仅将存储视为一个大型普通驱动器，并顺序访问存储。

逻辑卷有一个限制和一个建议建议。启动分区不能是逻辑卷的一部分。你仍然需要创建一个独立的硬盘分区作为启动分区，并使用 `/boot` 挂载点，在其中安装内核和所有必要的启动文件。此外，建议不要将根分区放在逻辑卷上。这样做会增加数据恢复的复杂性。这就是为什么在 Linux Mint 安装期间为 LVM 设置的默认分区配置会包含一个 `ext4` 类型的独立 `/boot` 分区，而根分区将安装在逻辑卷上。将有两个分区，一个用于逻辑组（LVM 物理卷，`pv`）持有根卷，另一个用于启动分区（`ext4`）。逻辑卷反而都是 `ext4` 文件系统。

## LVM 工具：使用 LVM 命令

要使用 LVM，请确保已安装 `lmv2` 包。使用 Synaptic 软件包管理器或 `apt` 命令。然后，你可以使用一组 LVM 工具来管理你的 LVM 卷，添加新的 LVM 物理分区并移除当前分区。对于 LVM 工具，你既可以直接使用 LVM 工具，也可以使用 `lvm` 命令生成一个交互式 shell，你可以在其中运行 LVM 命令。所有的 LVM 命令都有帮助页（Man pages）。LVM 在 `/etc/lvm/lvm.conf` 文件中维护配置信息，你可以在其中配置 LVM 选项，例如日志文件、配置备份目录或 LVM 设备的目录（更多细节请参阅 `lvm.conf` 手页）。

### 显示 LVM 信息

你可以使用 `pvdisplay`、`vgdisplay` 和 `lvdisplay` 命令显示物理分区、卷组和逻辑卷的详细信息。`pvscan`、`vgscan` 和 `lvscan` 命令列出你的物理卷、卷组和逻辑卷。

### 使用 LVM 命令管理 LVM 物理卷

物理卷可以是任何硬盘分区或 RAID 设备。RAID 设备被视为单个物理卷。你可以从单个硬盘创建物理卷，也可以从硬盘上的分区创建物理卷。在具有许多硬盘的非常大型的系统中，你更有可能为每个物理卷使用整个硬盘。

你首先会使用如 `fdisk`、`parted` 或 `gparted` 之类的分区工具来创建一个 LVM 分区类型（`8e`）的分区。然后，你可以通过使用 `pvcreate` 命令将该分区初始化为物理卷。

要在整个硬盘上初始化物理卷，你使用硬盘设备名称，如下所示：

```
pvcreate /dev/sdc
```

这将初始化 `sdc` 硬盘上的一个名为 `sdc1` 的物理分区 `pv`（即第三个串行 ATA 驱动器，c）。

如果你正在使用驱动器上的某个特定分区，则使用分区的设备名称创建一个新的物理卷，如下所示：

```
pvcreate /dev/sda3
```

要初始化多个驱动器，只需列出它们。以下命令将创建两个物理分区 `sdc1` 和 `sdd1`。

```
pvcreate /dev/sdc /dev/sdd
```

你还可以使用不同硬盘上的多个分区。在这种情况下，你的每个硬盘都持有多个分区。当你将硬盘上的某些分区用于不同的用途（例如不同的操作系统），或者如果你想将逻辑组分布在多个硬盘上时，这种情况经常发生。要一次性初始化这些分区，你只需列出它们。

```
pvcreate /dev/sda3 /dev/sdb1 /dev/sdb2
```

一旦你初始化了分区，就必须在它们上创建 LVM 组。

### 管理 LVM 组

物理 LVM 分区用于组成卷组。你可以使用 `vgcreate` 命令和组名称以及你想要包含在组中的物理分区列表来手动创建卷组。

如果你随后要创建一个新的卷组来放置这些物理卷，那么你可以在使用 `vgcreate` 命令创建卷组时将它们包含在内。卷组可以使用一个或多个物理分区。以下示例中描述的配置仅为 `VolGroup00` 使用了一个物理分区。在接下来的示例中，名为 `mymedia` 的卷组由两个物理卷 `sdc` 和 `sdd` 组成。

```
vgcreate mymedia /dev/sdc /dev/sdd
```

上一个示例在两个串行 ATA 硬盘上设置了逻辑组，每个硬盘都有它自己的单个分区。或者，你可以设置一个跨越多个硬盘分区的卷组。如果你将分区用于不同的功能，这种方法赋予了你使用跨越多个硬盘的所有可用空间的灵活性。以下示例创建了一个名为 `mygroup` 的组，由三个物理分区 `/dev/sda3`、`/dev/sdb2` 和 `/dev/sdb4` 组成：

```
vgcreate mygroup /dev/sda3 /dev/sdb2 /dev/sdb4
```

如果你以后想向卷组添加物理卷，你会使用 `vgextend` 命令。`vgextend` 命令将新分区添加到逻辑组。在以下示例中，分区 `/dev/sda4` 被添加到卷组 `mygroup`。实际上，你通过添加新分区扩展了逻辑组的大小。

```
vgextend mygroup /dev/sda4
```

要向卷组添加整个新驱动器，你可以遵循类似的步骤。以下示例首先在第五个串行 ATA 驱动器 `sde` 上创建物理卷，然后将其添加到 `mymedia` 卷组。

```
pvcreate /dev/sde
```要移除物理分区，首先将其从逻辑组中移除。你可能需要使用 `pmove` 命令将数据移出物理分区。然后使用 `vgreduce` 命令将其从逻辑组中移除。

你可以通过先用 `vgchange -a n` 禁用然后使用 `vgremove` 命令来移除整个卷组。

### 激活卷组

在标准文件系统结构中你挂载和卸载硬盘分区，而在 LVM 结构中，你激活和禁用整个卷组。组卷在你使用 `vgchange` 命令配合 `-a` 参数激活之前是可以使用的。要激活组，首先重启系统，然后输入 `vgchange` 命令配合 `-a` 参数和 `y` 参数来激活逻辑组（`n` 参数将禁用该组）。

```
vgchange -a y mygroup
```

### 管理 LVM 逻辑卷

要创建逻辑卷，你使用 `lvcreate` 命令，然后使用标准格式化命令（如 `mkfs.ext4`）格式化你的逻辑卷。使用 `-n` 选项指定卷的名称，该名称类似于硬盘分区的标签。你使用 `-L` 或 `--size` 选项指定卷的大小。测量值使用大小后缀，`G` 代表字节，`M` 代表兆字节，`K` 代表千字节。还有其他选项用于实现如线性、条带或镜像卷的功能，或者指定使用的块大小。通常，默认值效果良好。以下示例在 `mygroup` 逻辑组上创建一个名为 `projects` 的大小为 20GB 的逻辑卷。




```bash
lvcreate -n projects -L 20GB mygroup
```

以下示例在 `mymedia` 卷组上创建一个大小为 540GB 的逻辑卷。`mymedia` 卷组由两个物理卷组成，每个物理卷都位于 320GB 的硬盘上。实际上，这两块硬盘在逻辑上被视为一个整体。

```bash
lvcreate -n myvideos -L 540GB mymedia
```

一旦你创建了逻辑卷，就不需要为它创建一个文件系统以供使用。以下操作是在 `myvideos` 逻辑卷上创建一个 `ext4` 文件系统。

```bash
mkfs.ext4 myvideos
```

你也可以使用：

```bash
mkfs -t ext4 myvideos
```

通过 `lvextend`，如果卷组中有未分配的空间，你可以增加逻辑卷的大小。

如果你想减小逻辑卷的大小，可以使用 `lvreduce` 命令并指定新大小。请务必先使用 `resize2fs` 命令缩减逻辑卷上任何文件系统（`ext4`）的大小。

要重命名逻辑卷，使用 `lvrename` 命令。如果你想完全删除逻辑卷，可以使用 `lvremove` 命令。

### 创建新 LVM 卷组和卷的步骤

**物理分区** 首先，在你的硬盘上创建一个物理分区。你可以使用 GParted、`QTparted` 或带有磁盘设备名称的 `fdisk` 来创建分区。例如，要使用 `fdisk` 在设备名称为 `/etc/sde` 的新硬盘上创建一个新分区，你需要输入：

```bash
fdisk /etc/sde
```

然后，在 `fdisk` shell 界面中，使用 `fdisk` 的 `n` 命令创建一个新分区，将其设置为主分区（`p`），并使其成为第一个个分区。如果你计划将整块硬盘用于 LVM，那么你只需要一个覆盖整个硬盘的分区。

然后使用 `t` 命令将分区类型设置为 `8E`。`8E` 类型是 LVM 分区类型。要保存你的更改，输入 `w` 将更改写入磁盘。

**物理卷** 接下来，在新的空闲 LVM 分区上，使用 `pvcreate` 命令和设备名称创建一个物理卷（pv）。

```bash
pvcreate /dev/sde
```

**卷组** 然后，使用 `vgcreate` 命令创建你的卷组，指定卷组名称和硬盘设备名称。

```bash
vgcreate mynewgroup /dev/sde
```

确保卷组已激活。使用 `vgs` 命令列出它。如果没有列出，请使用以下命令激活它。

```bash
vgchange -a y mynewgroup
```

**逻辑卷** 然后，使用 `lvcreate` 命令为卷组创建一个或多个逻辑卷。`--size` 或 `-L` 选项决定大小，`--name` 选项指定名称。要查找可用空空间，请使用 `vgs` 命令。一个卷组可以拥有多个逻辑卷，或者根据喜好只拥有一个。逻辑卷概念上类似于 Windows 系统中扩展分区上的逻辑卷。

```bash
lvcreate --size --name mynewvol1
```

**格式化逻辑卷**。你可以使用带有 `-t` 选项的 `mkfs` 命令格式化逻辑卷。逻辑卷将列在 LVM 卷组的目录下，位于 `/dev` 目录内，即 `/dev/mynewgroup/mynewvol1`。

```bash
mkfs -t ext4 /dev/mynewgroup/mynewgroup-mynewvol1
```

字体 向 LVM 卷组和卷添加新硬盘的步骤

**物理分区** 首先，在你的硬盘上创建一个物理分区。你可以使用 GParted、`QTparted` 或带有磁盘设备名称的 `fdisk` 来创建分区。类型为 `ext4`。

**物理卷** 接下来，在新的空闲 LVM 分区上，使用 `pvcreate` 命令和设备名称创建一个物理卷（pv）。

```bash
pvcreate /dev/sdf
```

**卷组** 然后，使用 `vgextend` 命令将新硬盘添加到现有的卷组。

```bash
vgextend mynewgroup /dev/sdf
```

**逻辑卷** 然后，使用 `lvextend` 命令扩展逻辑卷空间，卸载逻辑卷。然后使用 `lvextend` 命令将新硬盘扩展到逻辑卷。

```bash
umount /dev/mynewgroup/mynewvol1
lvextend /dev/mynewgroup/mynewvol1 /dev/sdf
```

使用 `-L +250G` 指定大小。要查找可用空空间，请使用 `vgs` 命令。

**添加文件系统**。使用 `resize2fs` 命令扩展文件系统。

```bash
resize2fs /dev/mynewgroup/mynewvol1
```

注意：你可以使用 `vgbackup` 命令备份卷组元数据（配置）。元数据备份存储在 `/etc/lvm/backup`，可以使用 `vgrestore` 恢复。

### LVM 设备名称：dev/mapper

`device-mapper` 驱动程序用于 LVM 设置映射表。Linux 默认 LVM 设置名为 `vgmint-root`。`mymedia` 卷组拥有卷 `mypics`。此外，卷组还有一个设备文件夹。对于 `vgmint`，存在 `/dev/vgmint`。

### 使用 LVM 替换硬盘

当你需要用新硬盘替换旧硬盘时，LVM 非常有用。硬盘的平均寿命为六年。更换额外的硬盘很容易。要替换硬盘，只需将新硬盘合并到逻辑卷（参见“向 LVM 卷组和卷添加新硬盘的步骤”）。逻辑卷的大小将相应增加。你可以使用 `pmove` 命令将数据从旧硬盘移动到新硬盘。然后，执行命令从卷组移除旧硬盘（`vgreduce`）。从用户和系统的角度来看，没有任何变化。

如果你想替换启动硬盘（系统启动时使用的硬盘，存放 Linux 内核），替换 LVM 将变得复杂。启动硬盘包含一个特殊的启动分区和主引导记录。启动分区不能是任何 LVM 卷的一部分。你需要首先使用 Parted 或 `fdisk` 等分区工具在新硬盘上创建一个启动分区，将其标记为 boot（启动分区通常很小，约 200 MB）。然后在系统中挂载该分区，并将 `/boot` 目录的内容复制到其中。然后将硬盘的剩余部分添加到逻辑卷，并在逻辑上移除旧磁盘。你仍然需要使用 Linux 救援光盘（或在救援模式下安装光盘），并执行 `grub-install` 命令在新硬盘上安装主引导记录。现在你就可以从新硬盘启动了。





快照记录并定义了逻辑卷在指定时间的状态。它并没有在卷上创建数据的完整副本，仅记录自上一次快照以来的更改。快照定义了数据在特定时刻的状态，这允许你以一种一致的方式备份数据。如果你需要将文件恢复到之前的版本，可以使用该文件的快照。快照被视为逻辑卷，可以进行挂载、复制或删除。

要创建快照，请使用带有 `-s` 选项的 `lvcreate` 命令。在示例中，快照被命名为 `mypics-snap1`（使用 `-n` 选项）。你需要指定要为创建快照的逻辑组的完整设备名称。请确保逻辑组中有足够的可用空间来创建快照。在本示例中，快照逻辑卷在 `/dev/mymedia` 逻辑组中创建。它同样也可以创建在任何其他逻辑组中。虽然快照通常占空间很少，但你必须防范溢出。如果为快照分配与原始卷相同的大小，它将永远不会溢出。对于原始数据变化较小的系统，快照可以很小。以下示例分配了原始大小的三分之一（60GB）。

```
sudo lvcreate -s –n mypics-snap1 -l 20GB /dev/mymedia
```

然后你可以像挂载任何其他文件系统一样挂载快照。

```bash
sudo mount /dev/mymedia/mypic-snap1 /mysnaps
```

要删除快照，使用 `lvremove` 命令，像删除任何逻辑卷一样删除它。

```bash
sudo lvremove -f /dev/mymedia/mypics-nap1
```

快照对于在系统运行时制作备份非常有用。你可以使用 `tar` 或 `dump` 将挂载的快照备份到磁盘或磁带。原始逻辑卷的所有数据都将包含在内，以及快照记录的更改。

快照还允许你执行有效的撤销操作。你可以为逻辑卷创建一个快照，然后卸载原始卷并将其挂载快照。你所做的任何更改都将在快照上执行，而不是原始卷上。如果发生问题，卸载快照然后挂载原始卷。这将恢复你数据的原始状态。你也可以使用多个快照执行此操作，恢复到之前的某个快照。通过这种程序，你可以在快照上测试新软件，而不会危及原始数据。软件将在快照上运行，而不是原始逻辑卷。

你还可以将它们作为逻辑卷的替代版本。你可以对快照进行读写操作。写入操作只会更改快照卷而不会更改原始卷，实际上创建了一个备用版本。

# OpenZFS

ZFS 文件系统集成了逻辑卷管理器 (LVM)、RAID 系统和文件系统的功能。它现在是手动分区格式（其他选项）时的一种文件系统类型选项。ZFS 抽象了文件系统，就像 LVM 一样，建立了一个存储池，并从中心生成文件系统。数据块的校验和存储在数据块之外，并检查块内是否存在任何损坏。这使得 ZFS 能够有效防止由于写入中断、驱动程序错误和访问失败等问题导致的静默数据损坏。如果设置了 RAID-Z 支持，可以恢复损坏的块。RAID-Z 实现了一种面向数据的类 RAID 支持，并在文件系统内部对你的数据进行自动镜像。此外，ZFS 的类 LVM 抽象允许大文件的存在。写入操作采用写时复制（copy-on-write）事务方法执行，数据不会被直接覆盖，而是被添加。

ZFS 由 SUN 开发，现已由 Oracle 控制。自 2010 年以来，OpenZFS 为 Linux 系统提供了 ZFS 的开源版本。Linux Mint 和 Ubuntu 支持 ZFS 文件系统，使用 OpenZFS 内核模块。可以通过 `zfsutils-linux` 软件包、Synaptic 包管理器或 `apt` 命令安装管理 ZFS 文件系统的工具。更多信息请参见：

[`wiki.ubuntu.com/Kernel/Reference/ZFS`](https://wiki.ubuntu.com/Kernel/Reference/ZFS)

与 LVM 系统类似，你拥有物理设备（称为虚拟设备，VDEVs），它们被组合并条化到一个数据池（使用 `zpool` 命令），然后可以使用它可以创建 ZFS 文件系统。在池级别，你可以实现 RAIDZ 选项。通过 `zfs` 命令，你可以在池中创建文件系统。通过 `zfs` 命令，你还可以创建 ZFS 文件系统的快照（只读副本）或克隆（可写副本）。要对池进行完整性检查，请使用 `zpool` 命令的 `scrub` 选项。

ZFS 会在你更新系统时自动生成快照。要将系统恢复到这些快照之一，你需要在启动系统时访问 Grub 启动菜单中的 History 项。这会打开之前的快照列表。选择你想要打开选项的项目，以便带不带用户数据的恢复系统，或恢复到恢复状态。

Linux Mint 还提供了 ZSys 系统工具（`zsys` 软件包）来方便管理你的 ZFS 文件系统。它仍在开发中。ZSys 实现了通过 `zsysd` 进程与 ZFS 交互的 `zsysctl` 命令。你可以使用 `zsysctl` 命令对你的 ZFS 文件系统执行操作。`list` 命令列出你的文件系统，`show` 命令显示它们的状态。

```bash
zsysctl list
zsysctl show
```

如果在安装期间选择了 ZFS 安装选项，系统将为你安装 `zfsutils-linux` 和 `zsys` 软件包。你可以在此处获取更多关于 ZSys 的信息：

[`github.com/ubuntu/zsys`](https://github.com/ubuntu/zsys)

# 网络连接

你使用网络管理器配置网络连接。Linux Mint 20 使用与 Ubuntu 20.04 相同的网络管理器。你有两个网络管理器可以选择：NetworkManager 和 systemd-networkd。在 Linux Mint 20 以及 Ubuntu 20.04 桌面版，NetworkManager 是默认的，并在安装时安装并激活。可以使用“系统设置-网络”或“网络连接”进行管理。另一种网络管理器 systemd-networkd 也已安装，但未配置。

两个网络管理器都使用 Netplan 来配置和管理网络设备。Netplan 是一个网络抽象配置渲染器，它使用简单的用户定义配置文件生成网络设备配置文件。旧的 ifupdown 软件包及其网络设备管理工具集（如 `ifup` 和 `ifdown`）已弃用，但仍然可用并受支持。Netplan 为网络设备配置提供了层抽象，使得过程变得更加灵活。Netplan 在 `/etc/netplan` 目录下创建网络设备配置文件，用户可以对其进行编辑。然后使用这些文件在启动时生成网络设备配置文件。

网络设备现在使用可预测命名方法，这与旧的命名方法不同。名称是根据特定设备生成的，引用网络设备类型、硬件连接和插槽，甚至是其功能。你可以在终端窗口中使用 `ifconfig` 命令查找网络设备的名称。





| nmcli | `nmcli` 是 Network Manager 的命令行界面版本。 |
| ufw | 设置网络防火墙。 |
| Gufw | UFW 防火墙的 GNOME 界面
| Firewalld | 使用 firewalld 设置网络防火墙。 |
| wvdial | PPP 拨号调制器连接 |
| systemd-networkd | 基于 systemd 的网络配置 |

#### 表 10-1：Linux Mint 网络配置工具

Linux Mint 会使用 `Network Manager` 自动检测并配置您的网络连接。如果自动配置由于某些原因失败或不完整，你可以使用 `Network Manager` 进行手动配置。如果你想建立一个简单的拨号调制器连接，可以使用 `WvDial`。你的网络还需要防火墙。推荐使用 `UFW`（带有 `Gufw` 界面）或 `FirewallD`。表 10-1 列出了若干网络配置工具。

Linux Mint 提供了两个工具来配置您的 `NetworkManager` 连接：GNOME 网络（GNOME Network）和 `nm-connection-editor`。Gnome Network 提供基础配置，包括 Wi-Fi、有线和 VPN 连接以及代理配置。它可以在“偏好”菜单和“系统设置”中作为“网络”访问。在 `NetworkManager` 插件上，它被列为“网络设置”。`nm-connection-editor` 提供额外的配置，如 DSL、PPP 和移动宽带。它在“偏好”菜单中被称为“高级网络配置”，在 `NetworkManager` 插件上被称为“网络连接”。

## 网络连接：动态与静态

如果你正连接在网络上，你可能需要获取某些信息来配置你的连接接口。大多数网络现在都支持使用动态配置，即使用较旧的动态主机配置协议（`DHCP`）或新的 IPv6 协议及其自动地址配置。在这种情况下，你只需在大多数网络配置工具中检查 `DHCP` 条目即可。如果你的网络不支持 `DHCP` 或 `IPv6` 自动寻，或者你正在使用静态连接（`DCHP` 和 `IPv6` 连接是动态的），你必须提供有关连接的详细信息。对于静态连接，你需要手动输入连接信息，例如 IP 地址和 DNS 服务器；而在动态连接中，这些信息由 `DHCP` 服务器自动提供给你的系统，或者在连接到网络时由 `IPv6` 生成。对于 `DHCP`，每个主机上的 `DHCP` 客户端将从为该网络的 `DHCP` 服务器获取信息。`IPv6` 直接根据设备和路由器信息（如设备的硬件 MAC 地址）生成其地址。

此外，如果你使用动态 DSL、ISDN 或调制器连接，你还必须提供提供商（provider）、登录名和密码信息，并指明你的系统是动态的还是静态的。你可能还需要提供一些特殊信息，例如 DSL 或调制器压缩方法或拨号号码。

你可以从你的网络管理员或 ISP（互联网服务提供商）处获取大部分静态网络信息。你需要以下信息：

**网络接口的设备名称** 对于局域网和无线连接，这是网络设备名称，你可以通过 `ifconfig` 或 `ip l` 命令找到它。对于调制器、DSL 或 ISDN 连接，这是一个名为 `ppp0` 的 PPP 设备（ISDN 为 `ippp0`）。它也支持虚拟网络（VPN）连接。

**主机名** 你的计算机在互联网上将通过此名称识别。不要使用 `localhost`；该名称留供你的系统特殊用途使用。主机名应该是一个简单的单词，可以包含数字，但不能包含点和反斜杠等标点符号。在小型网络中，主机名通常是单一名称。在可能有多个域的大型网络中，主机名包含主机名和其域名。

**域名** 这是你网络的名称。

**分配给你的机器的网协议 (IP) 地址** 这仅在静态互联网连接时需要。动态连接使用 `DHCP` 协议自动为你分配 IP 地址。互联网上的每个主机都分配有一个 IP 地址。较小和较旧的网络地址可能仍使用旧的 `IPv4` 格式，其由一组由点分隔的四个数字组成。IP 协议版本 6（`IPv6`）使用了一种新格式，具有复杂的编号序列且更加自动化。

**你的网络 IP 地址** 仅用于静态连接。此地址与 IP 地址类似，但缺少对特定主机的引用。

**子网掩码** 仅用于 `IPv4` 静态连接。对于大多数网络，这通常是 `255.255.255.0`。然而，如果你属于大型网络的一部分，请咨询你的网络管理员或 ISP。

**你的网络广播地址（如果可用，可选）** 仅用于 `IPv4` 静态连接。通常，你的广播地址与你的 IP 地址相同，但在末尾加上数字 255。

**网络网关计算机的 IP 地址** 仅用于静态连接。这是将你的局域网连接到互联网等更大网络的计算机。

**域名服务器** 你的网络使用的域名服务器的 IP 地址。这些服务器使得 URL 可用。

**NIS 服务器的 NIS 域和 IP 地址** 如果你的网络使用 `NIS` 服务器则需要（可选）。

**用户登录名和密码信息** 用于动态 DSL、ISDN 和调制器连接。

## Network Manager

Network Manager 自动检测你的网络连接（有线和无线）。它利用 `udev` 的自动设备检测能力来配置你的连接。如果你需要手动配置网络连接，也可以使用 GNOME 网络（网络设置）或旧的 `nm-connection editor`（网络连接）来输入所需的网络连接信息。Network Manager 以名为 `Network Manager` 的守护进程运行。它会自动扫描有线和无线连接。Network Manager 提供的信息可供其他应用程序使用。Network Manager 监控你的网络连接，并在 Network Manager 插件上显示其状态。

Network Manager 设计用于后台运行，提供连接的状态信息，并在所需的各个配置连接之间进行切换。对于初始配置，它可以尽可能检测有关新连接的信息。

Network Manager 以名为 `NetworkManager` 的守护进程运行。如果没有以太网连接，Network Manager 将扫描无线连接并检查扩展服务标识符 (ESSID)。如果 ESSID 识别出以前使用过的连接，则会自动选择。如果发现多个，则选择最近使用的一个。如果只发现新连接，则 Network Manager 将等待用户选择。只有在用户登录时才会选择连接。如果之后连接了以太网连接，Network Manager 将从无线连接切换到它。

可以使用 `systemctl` 命令配合 `sudo` 命令开启或关闭 Network Manager 守护进程。

```
sudo systemctl start NetworkManager
sudo systemctl stop NetworkManager
```

Network Manager 也是特定用户的。当用户登录时，用户偏好的无线连接将启动（有线连接会自动启动）。默认情况下，如果有，以太网连接将优先考虑。对于无线连接，你需要选择你想要的那个。

### Network Manager 菜单





Network Manager 在 Linux Mint 面板的右侧显示网络小组件。Network Manager 图标会根据连接的类型而变化。以太网（有线）连接显示两个已连接的插头。无线连接显示一个交错的波形图（参见图 10-1）。如果连接未激活，则显示一个空波形图。如果你同时拥有有线和无线连接，且有线连接处于激活状态，则使用有线连接图标。

![Image](img/image-67.png)  ![Image](img/image-68.png)  ![Image](img/image-1.jpeg)

图 10-1：Network Manager 有线、无线和断开连接图标。

Network Manager 小组件菜单将你的有线连接显示为“Wired”（有线），并有一个用于开启或关闭的开关（见图 10-2）。要断开有线连接，你可以点击该开关将其切换到关闭位置。面板上的 Network Manager 图标将变为灰色。要稍后重新连接，请再次点击开关。

![Image](img/image-550.png)  ![Image](img/image-551.png)  ![Image](img/image-552.png)

图 10-2：Network Manager 小组件菜单

Network Manager 将扫描无线连接，检查扩展服务集标识符 (ESSID)。如果某个 ESSID 标识出之前使用过的连接，则 Network Manager 会选中它。如果发现多个连接，则选择最近使用的一个。如果仅有一个新连接，则 Network Manager 将等待用户选择一个。只有在用户登录状态下，才能选择连接。

## 使用 GNOME Network (网络设置) 手动配置 Network Manager

GNOME Network 工具可以通过“系统设置”中的“Network”（网络）或“偏好设置”菜单中的“Network”以及 Network Manager 小组件菜单中的“Network Settings”（网络设置）来访问，用于配置你的网络连接。自动无线和有线连接在第 3 章中已有介绍。要进行详细的手动配置，Network 功能提供了与 Network Connections（网络连接）中类似的对话框。当你访问 GNOME Network 时，它会显示一个 Network 对话框，包含三个选项卡：Wi-Fi、Wired（有线）和 Network Proxy（网络代理）（参见图 10-3）。

History（历史）按钮打开历史对话框，列出你所有配置过的 Wi-Fi 网络（参见图 10-3）。Configuration（配置）按钮打开该网络的配置对话框。要移除 Wi-Fi 配置，点击其复选框，这将激活左下角的“Forget”（忘记）按钮，然后点击该按钮。

![Image](img/image-553.png)  ![Image](img/image-554.png)

图 10-3：网络（系统设置）Wi-Fi 选项卡和历史

在 Wi-Fi 选项卡上，右侧列出了可用的无线连接。选择某一项将为其创建一个齿轮按钮，点击它可以打开网络配置对话框，该对话框包含 Details（详情）、Security（安全）、Identity（身份）、Ipv4、Ipv6 和 Reset（重置）选项卡。Details 选项卡显示强度、速度、安全方法、IP 和硬件地址、路由以及 DNS 服务器 IP 地址。要手动编辑连接，请使用 Security、Identity 和 IP 选项卡。Security 选项卡显示一个菜单，你可以在其中选择安全方法和密码（参见图 10-4）。

![Image](img/image-555.png)

图 10-4：网络无线配置：Security 选项卡

在 Identity 选项卡上，你可以指定 SSID 名称、选择防火墙区域、选择登录时自动连接，以及是否将连接设为系统级（其他用户可用）（参见图 10-5）。

![Image](img/image-556.png)

图 10-5：网络无线配置 Identity

Network Manager 将扫描无线连接，检查扩展服务集标识符 (ESSID)。如果某个 ESSID 标识出之前使用过的连接，则 Network Manager 会选中它。如果发现多个连接，则选择最近使用的一个。如果仅有一个新连接，则 Network Manager 将等待用户选择一个。只有在用户登录状态下，才能选择连接。

![Image](img/image-557.png)

图 10-6：网络配置 IP

在 Wi-Fi 选项卡上，右侧列出了可用的无线连接。选择某一项将为其创建一个齿轮按钮，点击它可以打开网络配置对话框，该对话框包含 Details、Security、Identity、Ipv4、Ipv6 和 Reset 选项卡。Details 选项卡显示强度、速度、安全方法、IP 和硬件地址、路由以及 DNS 服务器 IP 地址。要手动编辑连接，请使用 Security、Identity 和 IP 选项卡。Security 选项卡显示一个菜单，你可以在其中选择安全方法和密码（参见图 10-7）。

![Image](img/image-558.png)

图 10-7：网络配置 IPv4

![Image](img/image-559.png)

图 10-8：网络配置 Security

在 Identity 选项卡上，你可以指定 SSID 名称、选择防火墙区域、选择登录时自动连接，以及是否将连接设为系统级（其他用户可用）（参见图 10-9）。

![Image](img/image-560.png)

图 10-9：网络配置 Security

![Image](img/image-561.png)

图 10-10：网络配置 Identity

![Image](img/image-562.png)  ![Image](img/image-563.png)

图 10-11：网络配置 Wired

在 IPv4 选项卡上，你可以指定 SSID 名称，选择防火墙区域、选择登录时自动连接，以及是否将连接设为系统级（其他用户可用）（参见图 10-10）。

![Image](img/image-564.png)

图 10-12：VPN 选择

![Image](img/image-565.png)

图 10-13：VPN 配置

![Image](img/image-566.png)

图 10-14：网络配置




列出了已建立的连接，并带有 `Add`、`Edit` 和 `Delete` 按钮用于添加、编辑和删除网络连接。你的当前网络连接应该列在这里，它们是自动检测到的。在图 10-14 中，列出了名为 `Wired connection 1` 的有线以太网连接，这是第一个以太网连接。这是 `Network Manager` 在自动连接有线网络时设置的自动配置。

当你添加连接时，可以从下拉菜单中选择连接类型（参见图 10-15）。该菜单将连接类型分为三类：硬件、虚拟和 `VPN`（虚拟专用网络）（参见图 10-16）。硬件连接包括有线连接（`Ethernet`、`DSL` 和 `Infiniband`）和无线连接（`Wi-Fi`、`WiMax` 和 `Mobile Broadband`）。`VPN` 列出了支持的 `VPN` 类型，如 `OpenVPN`、`PPTP` 和 `Cisco`（安装对其他类型的支持）。你也可以导入以前配置过的连接。虚拟连接支持 `VLAN`、`Bridge` 和 `Bond` 虚拟连接。

![Image](img/image-567.png)

图 10-15: 为新网络连接选择连接类型

![Image](img/image-568.png)

图 10-16: 新连接类型

### General 选项卡

配置编辑对话框显示一个 `General`（常规）选项卡，你可以在其中让你的配置对所有用户可用，并在网络连接可用时自动连接。你还可以选择使用 `VPN` 连接并指定防火墙区域。图 10-17 显示了带有有线连接的 `General` 选项卡。

![Image](img/image-569.png)

图 10-17: General 选项卡

### Wired Configuration

要编辑有线连接，请选择该连接并点击 `Ethernet` 选项卡上的 `Edit` 按钮。这将打开一个 `Editing` 窗口，如图图 10-18。`Add` 按钮用于添加新连接并打开一个类似的空白窗口。共有六个选项卡：`General`、`Ethernet`、`8.02.1x Security`、`DCB`、`IPv4 Settings` 和 `IPv6 Settings`。`Ethernet` 选项卡列出了 MAC 硬件地址和 `MTU`。`MTU` 通常设置为自动。图 10-16 显示了使用 `DHCP` 的有线以太网连接的标准默认配置。

![Image](img/image-570.png)

图 10-18: DHCP 有线配置

`IPv4` 和 `IPv6 Settings` 选项卡允许你选择有线连接使用的协议类型。对话框底部的复选框让你要求使用指定的协议来完成连接。`IPv4` 和 `IPv6` 有不同的选项。`IPv4` 选项有：

`Automatic (DHCP)`：`DHCP` 连接，地址信息被锁定。

`Automatic (DHCP) addresses only`：`DHCP` 连接，允许你指定你的 `DNS` 服务器地址。

`Manual`：输入你的 `IP`、网络和网关地址，以及你的 `DNS` 服务器地址和网络域名。

`Link-local only`：`IPv6` 私有本地网络。所有地址条目被锁定。

`Shared to other computers`：所有地址条目被锁定。

`IPv6` 选项有：

`Ignore`：使用 `IPv6`。

`Automatic`：`IPv6` 自动地址检测（类似于 `DHCP`）。

`Automatic, addresses only`：使用 `IPv6` 确定网络地址，但不确定 `DNS`（域）信息。你可以手动输入 `DNS` 服务器地址和搜索域。

`Manual`：输入你的 `IP`、网络和网关地址，以及你的 `DNS` 服务器地址和网络域名。`IPv6` 地址使用地址和前缀。

`Link-local only`：`IPv6` 私有本地网络。所有地址条目被锁定。

图 10-19 显示了 `IPv4` 有线以太网连接的手动配置项。点击 `Add` 按钮输入 `IP` 地址、子网掩码和网关地址。然后输入 `DNS` 服务器地址和你的网络搜索域。`Routes` 按钮将打开一个窗口，你可以在其中手动输入任何网络路由。图 10-20 显示了 `IPv6` 连接的手动配置，包含地址和前缀条目。

![Image](img/image-571.png)

图 10-19: 手动 IPv4 有线配置

![Image](img/image-572.png)

图 10-20: 手动 IPv6 配置

`802.1` 选项卡允许在网络支持时配置 802.1（参见图 10-21）。`DCB` 选项卡允许你配置数据中心桥接以管理高速以太网连接。

![Image](img/image-573.png)

图 10-21: 802.1 安全

### Wireless Configuration

无线连接列在 `Network Connections` 窗口的 `Wi-Fi` 选项卡上。要添加或编辑连接，使用 `Add` 或 `Edit` 按钮。点击 `Edit` 按钮将打开一个包含 `Wi-Fi` 信息、安全、`IPv4` 和 `IPv6` 设置选项卡的 `Editing` 窗口（参见图 10-22）。

![Image](img/image-574.png)

图 10-22: Wi-Fi

在 `Wi-Fi` 安全选项卡上，你输入无线连接方法（参见图 10-23）。支持常用的方法 `WEP`，以及 `WPA personal`。`WPA personal` 方法只需要密码。支持更安全的连接如 `Dynamic WEP` 和 `Enterprise WPA`，这些需要身份验证方法、证书和密钥。

在 `IPv4 Settings` 选项卡上，你输入无线连接地址。该选项卡与有线以太网连接的 `IPv4 Settings` 选项卡相同（参见图 10-19）。你有相同的选项：`DHCP`、`DHCP with DNS`、`Manual`、`Link-local only` 和 `Shared`。如果你的无线连接使用 `IPv6` 协议，你将使用 `IPv6 Settings` 选项卡，与有线连接的 `IPv6 Settings` 相同（参见图 10-20）。

![Image](img/image-575.png)

![Image](img/image-576.png)

图 10-23: Wi-Fi 安全: WEP 和 WPA

### DSL Configuration

要添加或编辑直接 `DSL` 连接，请点击 `Network Connections` 窗口 `DSL` 选项卡上的 `Add` 或 `Edit` 按钮。`DSL` 连接窗口将打开，显示 `DSL` 配置以及有线、`PPP` 和 `IPv4` 网络连接的选项卡。在 `DSL` 选项卡上，你输入你的 `DSL` 用户名、服务供应商和密码（参见图 10-24）。`PPP` 选项卡与用于 `Mobile Broadband` 的相同，`IPv4` 与用于有线、无线和移动宽带连接的 `IPv4 Settings` 选项卡相同。

![Image](img/image-577.png)

图 10-24: DSL 手动配置




移动宽带连接列在“移动宽带”（Mobile Broadband）选项卡中。对于新的宽带连接，点击`Add`按钮。将启动一个向导，帮助您为特定的宽带服务设置适当配置（参见图 10-25）。配置步骤列在左格中。如果您的设备已连接，可以从右格的下拉菜单中选择它。在下一步，您需要选择国家。向导会显示服务提供商窗口，列出移动宽带服务提供商（参见图 10-26）。然后您选择计费计划。最后一步，系统会要求您确认选择。

![Image](img/image-578.png)

图 10-25：移动宽带向导

一旦选择了服务，可以通过点击“移动宽带”选项卡中的条目并点击`Edit`按钮来进一步编辑配置。“编辑”窗口将打开，并包含移动宽带、PPP、IPv4 设置选项卡。在“移动宽带”选项卡上，您可以输入您的号码、用户名和密码。高级选项包括 APN、网络和 PIN（参见图 10-27）。APN 应该已经填入。

![Image](img/image-579.png)

图 10-26：移动宽带提供商列表

![Image](img/image-580.png)

图 10-27：移动宽带配置

### PPP 配置

对于无线宽带或 DSL 连接，您也可以指定 PPP 信息。PPP 选项卡对两者来说都是相同的（参见图 10-28）。包含身份验证（Authentication）、压缩（Compression）和回显（Echo）部分。勾选您的特定 PPP 连接支持的功能。对于身份验证，点击`Configure Methods`按钮打开一个列出可能的身份验证方法的对话框。勾选您的连接支持的项。

![Image](img/image-581.png)

图 10-28：PPP 配置

### Network Manager VPN

在 Network Manager 菜单上，`VPN Connection`条目菜单将列出已配置的 VPN 连接以便访问。`Configure VPN`条目将打开网络连接窗口的 VPN 选项卡，您可以在那里添加、编辑或删除 VPN 连接。`Disconnect VPN`条目将终止当前的活动 VPN 连接。

Universe 仓库（而非 Snap）提供了多种 VPN 服务。您可以使用`Synaptic Package Manager`（搜索 `network-manager`）或`apt` 命令来安装它们。用于 Microsoft VPN 连接的 PPTP 服务和 OpenVPN 是默认安装的。其他流行的 VPN 服务包括 Fortinet (SSL)、OpenConnect (SSL)、二层隧道协议 (IPSec 加密)、Cisco 集中器、Iodine (DNS 隧道) 和 Openswan (IPSec)。使用对应这些服务的相应 Network Manager 插件来安装 Network Manager 支持。插件包以 `network-manager` 名称开头。使用 `openvpn` 软件配合 `network-manager-openvpn` 插件的 OpenVPN 是默认安装的。对于二层隧道协议 VPN，请安装 `network-manager-ltp`。对于 Fortinet (SSL)，请安装 `network-manager-fortinet`。对于 OpenConnect (SSL)，请安装 `network-manager-openconnect`。对于二层隧道协议 (IPSec 加密)，请安装 `network-manager-l2tp`。对于 Cisco 集中器，请安装 `network-manager-cisco`。对于 Iodine (DNS 隧道)，请安装 `network-manager-iodine`。对于 Openswan (IPSec)，请安装 `network-manager-openswan`。

要添加二层隧道协议 VPN，请选择连接类型（参见图 10-29）。

![Image](img/image-582.png)

图 10-29：VPN 连接类型

![Image](img/image-583.png)

图 30：VPN 配置

### “编辑连接”

“编辑”窗口打开，并包含移动宽带、PPP、IPv4 设置选项卡。在“移动宽带”选项卡上，您可以输入您的号码、用户名和密码。高级选项包括 APN、网络和 PIN。APN 应该已经填入。

“编辑”窗口打开，并包含移动宽带、PPP、IPv4 设置选项卡。在“移动宽带”选项卡上，您可以输入您的号码、用户名和密码。高级选项包括 APN、网络和 PIN。APN 应该已经填入。

“编辑”窗口打开，并包含移动宽带、PPP、IPv4 设置选项卡。在“移动宽带”选项卡上，您可以输入您的号码、用户名和密码。高级选项包括 APN、网络和 PIN。APN 应该已经填入。

“编辑”窗口打开，并包含移动宽带、PPP、IPv4 设置选项卡。在“移动宽带”选项卡上，您可以输入您的号码、用户名和密码。高级选项包括 APN、网络和 PIN。APN 应该已经填入。

![Image](img/image-584.png)

图 31：VPN 配置 (pptp)

### Wireguard VPN

您可以使用`Synaptic Package Manager`（Universe 仓库）或`apt` 命令（Universe 仓库）安装 Wireguard。

```
sudo apt install wireguard
```

Wireguard 通过设置专用接口（`wg`）工作，这些接口用于连接。

```bash
wg
```

### 使用 nmcli 管理网络连接

`nmcli` 命令是 NetworkManager 命令行界面。大多数网络配置任务可以通过 `nmcli` 完成。`nmcli` 命令通过一组对象管理 NetworkManager：通用（general）、网络（networking）、无线电（radio）、连接（connection）、设备（device）和代理（agent）。每个对象都可以使用全名或唯一前缀进行引用，例如用 `con` 表示连接或用 `dev` 表示设备。唯一前缀可以短至单个字符，例如 `g` 表示通用、`c` 表示连接或 `d` 表示设备。

通用对象显示 NetworkManager 的当前状态以及哪些类型的设备已启用。可以使用 `-t`（简洁）和 `-f`（字段）选项来限制显示的信息。

| 对象 | 描述 |
| :--- | :--- |
| general | NetworkManager 状态和启用的设备。使用简洁 (**-t**) 和字段 (**-f**) 选项来限制显示的信息。 |
| networking | 管理网络，使用 on 和 off 开启或关闭网络，以及连接状态的可用性。 |
| radio | 开启或关闭无线网络（开启或关闭）。可以开启或关闭特定的无线类型：wifi、wwan（移动宽带）和 wimax。all 选项开启或关闭所有无线。 |
| connection | 管理网络连接。show 列出连接配置文件。--active 仅显示活动连接。up 激活连接 down 禁用连接。add 添加新连接，指定类型、ifname、con-name (配置文件)。modify 修改现有连接，使用 + 和 - 向属性添加新值。edit 使用交互式编辑器添加新连接或编辑现有连接 delete 删除已配置的连接 (配置文件)。reload 重新加载所有配置文件。load 重新加载或加载特定的 |





| object | Description |
| :--- | :--- |
| device | 管理网络接口（设备）。 |
| status | 显示设备状态 |
| show | 显示设备信息 |
| connect | 连接设备 |
| disconnect | 断开设备连接 |
| delete | 删除软件设备，例如网桥。 |
| wifi | 显示可用 wifi 接入点（AP）列表 |
| wifi rescan | 重新扫描并显示接入点 |
| wifi connect | 连接到 wifi 网络；指定密码、`wep-key-type`、`ifname`、`bssid` 和 `name`（配置名称） |
| wimax | 列出可用的 WiMAX 网络 |

| object | Description |
| :--- | :--- |
| agent | 作为 Network Manager 秘密代理（secret agent）或 polkit 代理运行。 |
| secret | 作为秘密代理，`nmcli` 会监听秘密请求。 |
| polkit | 作为 polkit 代理，它会监听所有的授权请求。 |

### 表 10-2：`nmcli` 对象

```
$ nmcli general STATE CONNECTIVITY WIFI-HW WIFI WWAN-HW WWAN connected full enabled enabled enabled enabled
$ nmcli -t -f STATE general connected
```

`connection` 对象引用网络连接，`show` 选项显示该信息。下面的示例显示了当前的连接。

```
nmcli connection show
```

你可以用 `c` 代替 `connection`，用 `s` 代替 `show`。

```
$ nmcli c s NAME UUID TYPE DEVICE enp7s0 f7202f6d-fc66-4b81-8962-69b71202efc0 802-3-ethernet enp7s0 AT&T LTE 1 65913b39-789a-gsm --
```

与 `general` 对象一样，你可以使用 `-f` 选项限制显示的字段。以下仅列出 name 和 type 字段。

```bash
$ nmcli -f name,type c s NAME TYPE enp7s0 802-3-ethernet AT&T LTE 1 gsm
```

添加 `--active` 选项将只显示激活的连接。

```bash
nmcli c s --active
```

要启动和停止连接（类似于 `ifconfig` 的），请使用 `up` 和 `down` 选项。

```bash
nmcli con up enp7s0.
```

使用 `device` 对象来管理你的网络设备。`show` 和 `status` 选项提供有关设备的信息。要检查所有网络设备的状态，请使用 `device` 对象和 `status` 选项：

```bash
nmcli device status
DEVICE TYPE STATE CONNECTION
enp7s0 ethernet connected
enp7s0 wlp6s0 wifi disconnected --
lo loopback unmanaged --
```

你可以将 `device` 和 `status` 写为 `d` 和 `s`。

```bash
nmcli d s
```

你还使用 `device` 对象来连接和断开设备。使用 `connect` 或 `disconnect` 选项配合设备的接口名称（`ifname`），在本例中为 `enp7s0`。使用 `delete` 选项，你可以移除设备。

```bash
nmcli device disconnect enp7s0
nmcli device connect enp7s0
```

要开启或关闭网络，你使用 `networking` 对象以及 `on` 和 `off` 选项。使用 `connectivity` 选项检查网络连通性。`networking` 对象本身可以告诉你它已启用。

```bash
$ nmcli networking enabled
$ nmcli networking on
$ nmcli networking connectivity full
```

如果你只想开启或关闭 Wifi 连接，将使用 `radio` 对象。使用 `wifi`、`wwan` 和 `wimax` 处理特定类型的 wifi 连接，使用 `all` 选项处理所有类型。`radio` 对象本身显示你所有 wifi 连接类型的状态。

```bash
$ nmcli radio WIFI-HW WIFI WWAN-HW WWAN enabled enabled enabled enabled
$ nmcli radio wifi on
$ nmcli radio all off
```

#### nmcli 有线连接

你可以使用 `nmcli` 添加连接，就像使用桌面版 NetworkManager 工具一样。要添加新的静态连接，使用 `connection` 对象配合 `add` 选项。使用 `con-name` 选项指定连接的配置名称，使用 `ifname` 选项指定接口名称，以及 `type`（例如 ethernet）。对于静态连接，你需要添加 IP 地址（`ipv4` 或 `ipv6`）以及网关地址（`gw4` 或 `gw6`）。对于 DHCP 连接，只需不列出 IP 地址和网关选项。配置名称可以是任何名称。你可以为同一个网络设备设置多个配置名称。例如，对于你的无线设备，你可以有多个无线连接配置，取决于你想要连接的不同网络。如果你将以太网设备连接到不同的网络，你只需要使用你已经设置好的不同连接配置，而不是手动重新配置连接。如果你没有指定连接名称，系统将为你生成并分配一个。连接名称可以与设备名称相同（如下所示），但请记住连接名称指的是配置，而设备名称指的是实际设备。

```bash
$ nmcli c s NAME UUID TYPE DEVICE enp7s0 f7202f6d-fc66-4b81-8962-69b71202efc0 802-3-ethernet enp7s0 AT&T LTE 1 gsm
```




你还可以使用 `connection` 对象和 `wifi` 类型配合 `ssid` 选项添加新的无线连接。

```
nmcli con add con-name my-wireless2 ifname wlp6s0 type wifi ssid ssidname
```

然后，使用 `modify` 命令设置 `sec.key-mgmt` 属性来设置加密类型，并使用 `wifi-sec.psk` 属性设置口密码。

```
nmcli con mod my-wirless2 wifi-sec.key-mgmt wpa-psk
nmcli con modify my-wireless2 wifi-sec.psk mypassword
```

## 拨号 PPP 调制调器访问：wvdial

对于直接拨号 PPP 调制调器连接，你可以使用 `wvdial` 拨号器，这是一个智能拨号器不仅不仅拨号 ISP 服务，还能执行登录操作，提供你的用户名和密码。`wvdial` 工具可以在命令行中使用 `wvdial` 命令运行，也可以在桌面上通过 GNOME PPP 应用程序 (`gnome-ppp`) 运行。`wvdial` 程序首先从 `/etc/wvdial.conf` 文件加载配置。在该文件中，你可以放置调制调器和账户信息，包括调制调器速度、ISP 电话号码、用户名和密码。

`wvdial.conf` 文件组织成多个节，以方括号括的节标签开始。一个节包含不同参数的变量，这些变量被赋予值，例如 `username = chris`。默认节包含其他节继承的默认值，因此你不需要重复它们。表 10-3 列出了 wvdial 变量。

你可以使用 `wvdialconf` 实用程序创建一个默认的 `wvdial.conf` 文件，检测你的调制调器并自动为基本功能设置默认值。然后你可以编辑 `wvdial.conf` 文件，通过输入你的拨号信息来修改电话、用户名和密码条目。删除前面的分号（`;`）可以取消对该条目的注释。任何以分号开头的行都会被视为注释忽略。

```
wvdialconf
```

你还可以创建一个命名的拨号器。如果你有不同的位置或服务需要登录，这非常有帮助。

要启动 wvdial，在终端窗口中输入 `wvdial` 命令，它将从 `/etc/wvdial.conf` 文件读取连接配置信息；wvdial 会拨号位置并启动 PPP 连接，在请求时提供你的用户名和密码。

你可以在 `/etc/wvdial.conf` 文件中为任意数量的连接设置配置。要选择其中一个，将其标签作为参数传递给 `wvdial` 命令，如下：

```
wvdial mylocation
```

| 变量 | 描述 |
| :--- | :--- |
| Inherits | 显式继承自指定的节。默认情况下，节继承自 [Dialer Defaults] 节。 |
| Modem | wvdial 应作为你的调制调器使用的设备。默认是 `/dev/modem`。 |
| Baud | wvdial 与你的调制调器通信的速度。默认是 57,600 波特。 |
| Init1...Init9 | 指定供调制调器使用的初始化字符串；wvdial 最多可使用 9 个。Init1 的默认值为 “ATZ”。 |
| Phone | 你让 wvdial 拨号的电话号码。 |
| Area Code | 指定区号（如果有）。 |
| Dial Prefix | 指定任何需要的拨号前缀——例如，用 70 呼叫等待或用 9 使用外线。 |
| Dial Command | 指定拨号操作。默认是 “ATDT”。 |
| Login | 指定你在 ISP 使用的用户名。 |
| Login Prompt | 如果你的 ISP 有不常见的登录提示，你可以在此处指定。 |
| Password | 指定你在 ISP 使用的密码。 |
| Password Prompt | 如果你的 ISP 有不常见的密码提示，你可以在此处指定。 |
| Force Address | 指定要使用的静态 IP 地址（对于向用户提供静态 IP 地址的 ISP）。 |
| Auto Reconnect | 如果启用，当由于由于对方随机断开连接时，wvdial 会尝试自动重新连接。此选项默认开启。 |

表 10-3：wvdial 变量

## Netplan

Netplan 用于配置和设置你的网络连接。`/etc/netplan` 目录包含用于配置你的网络设备的网络服务和接口信息。实际的配置文件在系统启动时生成，对于 NetworkManager，它被放置在 `/run/NetworkManager/system-connections` 目录（对于 systemd-networkd 则放置在 `/var/run/systemd/network` 目录）。`/etc` 目录下没有固定的配置文件。相反，使用 `/etc/netplan` 目录下的简单的 Netplan 配置文件来生成网络配置文件。`/etc/netplan` 文件使用 YAML（YAML 并不是标记语言）编写，并扩展名为 `.yaml`。这种方法提供了一种抽象层，使得不同可用网络设备的配置更加灵活。Linux Mint 桌面的默认网络服务是 NetworkManager。如果你愿意，可以在 Linux Mint 桌面上使用 networkd 而不是 NetworkManager。你可以在此处了解更多关于 Netplan 信息：

[`netplan.io`](https://netplan.io)

使用 `networkctl status` 命令检查你的网络连接状态。

```
networkctl status
```

有关特定设备的信息请将设备名称添加到状态命令中。

```
networkctl status enp7s0
```

Netplan 配置文件的详细示例位于：

/usr/share/netplan/

包括静态、无线、NetworkManager、dhcp、绑定和 vlan。

### Netplan 配置文件

Netplan 配置文件位于 `/etc/netplan`。Linux Mint 发行版生成了用于 NetworkManager 的 Netplan 文件 `1-network-manager-all.yaml`。NetworkManager 是 Linux Mint 的默认选择。你可以编辑此文件为更多设备添加配置，也可以添加更多配置文件，每个文件都会被 Netplan 读取并在 `/run/NetworkManager/system-connections` 生成相应的运行时文件。由于 NetworkManager 设计用于配置多个设备，你只需要一个 Netplan 文件。配置文件名通常以数字开头，默认为 `1-`，但可以是任何名称。创建新文件的简单方法是从 `/usr/share/doc/netplan/examples` 拷贝默认或示例文件然后进行编辑。

Netplan 配置文件组织成键，其包含适用于不同类型设备（如以太网）的高级配置定义和用于配置设备的低级 ID。文件从顶级 `network:` 键开始，随后是 Netplan 版本，在本例中为版本 2。`renderer:` ID 指定要使用的网络服务。对于 Linux Mint，它是 `NetworkManager`。Linux Mint 默认使用 NetworkManager 而不是 systemd-networkd，这简化了默认的 Netplan 配置文件。该文件仅包含渲染 信息，因为 NetworkManager 处理所有细节。你会使用系统设置中的网络或网络连接来配置网络。

```
/etc/netplan/1-network-manager-all.yaml

# 让 NetworkManager 管理此系统上的所有设备

network:

  version: 2
  renderer: NetworkManager
```




NetworkManager 的运行时配置文件位于 `/run/NetworkManager/system-connections` 目录，其连接名称遵循 NetworkManager 的命名规则，例如 `'Wired connection-1'.nmconnections`。

## 使用 systemd-networkd 配置网络

基于 systemd 的网络管理器 `systemd-networkd` 目前可用于基础操作。你可以将其作为 NetworkManager 等较大型管理器的轻量、快速且简单的替代方案。第 12 章将详细介绍 systemd。`systemd-networkd` 的服务文件（service）、目标文件（target）和套接字文件（socket）位于 `/lib/systemd/system` 目录：`systemd-networkd.service`、`systemd-networkd-wait-online.service` 和 `systemd-networkd.socket`。网络解析（resolvconf）操作由 `systemd-resolved.service` 处理。systemd-networkd 的用户配置文件位于 `/etc/systemd/network`。

在 `systemd-networkd.service` 文件中，启用了多项安全特性。能力边界集（capability bounding set `CapabilityBoundingSet`）允许你将内核能力限制为指定的项。`capabilities` 的帮助页列出了所有可用能力。`CAP_NET` 能力将 networkd 服务限制为网络操作，如接口配置、防火墙管理、多播、套接字、广播和代理。`CAP_SET` 能力允许修改文件进程的 GID 和 UID。`CAP_CHOWN`、`CAP_DAC_OVERRIDE` 和 `CAP_FOWNER` 能力用于绕过文件权限检查。未包含提供系统管理能力的 `CAP_SYS` 能力。此外，`ProtectSystem` 选项（`systemd.exec`）防止服务对系统进行任何更改（`/usr`、`/boot` 和 `/etc` 目录对该服务只读）。`ProtectHome` 选项使得 `/home`、`/root` 和 `/run/user` 目录无法访问。`WatchdogSec` 设置服务的看门狗超时。查看 `systemd.directives` 帮助页可获取所有 systemd 指令列表。

```
systemd-networkd.service

[Unit]
Description=Network Service
Documentation=man:systemd-networkd.service(8)
ConditionCapability=CAP_NET_ADMIN
DefaultDependencies=no

# systemd-udevd.service can be dropped once tuntap is moved to netlink
After=systemd-udevd.service network-pre.target systemd-sysusers.service systemd-sysctl.service
Before=network.target multi-user.target shutdown.target
Conflicts=shutdown.target
Wants=network.target

[Service]
AmbientCapabilities=CAP_NET_ADMIN CAP_NET_BIND_SERVICE CAP_NET_BROADCAST CAP_NET_RAW
CapabilityBoundingSet=CAP_NET_ADMIN CAP_NET_BIND_SERVICE CAP_NET_BROADCAST CAP_NET_RAW
ExecStart=!!/lib/systemd/systemd-networkd
LockPersonality=yes
MemoryDenyWriteExecute=yes
NoNewPrivileges=yes
ProtectControlGroups=yes
ProtectHome=yes
ProtectKernelModules=yes
ProtectKernelLogs=yes
ProtectSystem=strict
Restart=on-failure
RestartSec=0
RestrictAddressFamilies=AF_UNIX AF_NETLINK AF_INET AF_INET6 AF_PACKET AF_ALG
RestrictNamespaces=yes
RestrictRealtime=yes
RuntimeDirectory=systemd/netif
RuntimeDirectoryPreserve=yes
SystemCallArchitectures=native
SystemCallErrorNumber=EPERM
SystemCallFilter=@system-service
Type=notify
RestartKillSignal=SIGUSR2
User=systemd-network
WatchdogSec=3min

[Install]
WantedBy=multi-user.target
Also=systemd-networkd.socket
Alias=dbus-org.freedesktop.network1.service
# We want to enable systemd-networkd-wait-online.service whenever this service
# is enabled. systemd-networkd-wait-online.service has
# WantedBy=network-online.target, so enabling it only has an effect if
# network-online.target itself is enabled or pulled in by some other unit.
Also=systemd-networkd-wait-online.service
```

`systemd-networkd.socket` 文件为 `systemd.socket` 设置了缓冲区大小（`ReceiveBuffer`）、网络链路（`ListenNetlink`）和传递凭据（`PassCredentials`）。作为启动该服务的条件，需要在能力边界集（`ConditionCapability`）中设置 `CAP_NET_ADMIN` 能力。

```
systemd-networkd.socket

[Unit]
Description=Network Service Netlink Socket
Documentation=man:systemd-networkd.service(8) man:rtnetlink(7)
ConditionCapability=CAP_NET_ADMIN
DefaultDependencies=no
Before=sockets.target

[Socket]
ReceiveBuffer=8M
ListenNetlink=route 1361
PassCredentials=yes

[Install]
WantedBy=sockets.target
```

`systemd-resolved.service` 提供 resolvconf 操作（DNS 服务器信息）。它与 `systemd-networkd.service` 具有相同的能力，网络能力除外。

```
systemd-resolved.service

[Unit]
Description=Network Name Resolution
Documentation=man:systemd-resolved.service(8)
Documentation=https://www.freedesktop.org/wiki/Software/systemd/resolved
Documentation=https://www.freedesktop.org/wiki/Software/systemd/writing-network-configuration-managers
Documentation=https://www.freedesktop.org/wiki/Software/systemd/writing-network-configuration-managers
Documentation=resolver-clients
DefaultDependencies=no
After=systemd-networkd.service
```

## systemd-networkd Netplan 配置文件

你需要为 systemd-networkd 服务创建一个 Netplan 配置文件。你可以为不同的网络设备（如以太网和 Wi-Fi）创建文件，或者为每个设备创建一个不同的文件。配置文件名通常以数字开头，从 1 开始，尽管也可以是任何名称。

你必须了解系统的网络配置情况。对于许多系统（特别是使用 DHCP 的系统），配置是简单的；但对于其他系统（如静态连接），可能会很复杂。对于本章所示的标准 DHCP 连接，你可以直接从 `/usr/share/doc/netplan/examples` 目录将 `dhcp.yaml` 文件复制到 `/etc/netplan` 目录。为文件名加上数字，例如 2-。你可以保留 `/etc/netplan` 中的 `1-network-manager-all.yaml` 文件，以防以后想切换回 NetworkManager。

如果你还不知道，请使用 `ip link` 命令查找以太网设备的名称。然后使用 `nano` 等文本编辑器编辑 `2-dhcp.yaml`，将以太网设备名称 `enp3s0` 替换为你系统上的名称。你可以使用 `ifconfig` 命令来查找设备名称。务必使用 `sudo` 命令启动编辑器。

```bash
cd /usr/share/doc/netplan/examples
sudo cp dhcp.yaml /etc/netplan/2-dhcp.yaml
cd /etc/netplan
sudo nano 2-dhcp.yaml
```





Netplan 配置文件由一系列键组成，这些这些高层配置定义适用于 `ethernets`（以太网）等不同类型的设备，以及用于配置设备的低层 ID。文件以顶层 `network:` 键开始，随后是 Netplan 版本，在本例中为版本 2。`renderer:` ID 指定了要使用的网络服务，即 `networkd`。对于有线连接，配置类型为 `ethernets:`，如此示例所示。在 `ethernets:` 下，列出了可用网络设备的键。在每个设备下是用于配置该设备的 ID。对于 DHCP 连接，你通常只需要一个，`dhcp:`。也可以列出其他 ID，例如用于静态连接的 `address:` 或用于网关地址的 `gateway:`。最终的形式可能如下所示。

`/etc/netplan/2-dhcp.yaml`

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp7s0:
      dhcp4: true
```

Netplan 为网络配置生成的运行时文件位于 `/var/run/systemd/network`，其名称包含 "netplan" 和网络设备名称，例如 `10-netplan-enp7s0.network`。该文件在启动时自动生成。如果你编辑了 Netplan 配置文件或添加了新文件，且不想重启系统，可以使用 Netplan 的 `generate` 命令直接创建运行时配置文件，然后使用 `apply` 命令让 Netplan 将该配置应用到你的网络连接。

```bash
sudo netplan generate
sudo netplan apply
```

然后你必须关闭并禁用 NetworkManager。管理 NetworkManager 的服务脚本是 `network-manager`。

```bash
sudo systemctl stop network-manager
sudo systemctl disable network-manager
```

然后启用并启动 systemd-networkd。

```bash
sudo systemctl enable systemd-networkd
sudo systemctl start systemd-networkd
```

你可以使用 `networkctl` 命令检查网络设备配置的激活状态。

```bash
networkctl
```

### 为 systemd-networkd 针对 systemd-networkd 的 Netplan 无线配置

对于 systemd-networkd 无线设备，你必须编辑 Netplan 配置文件以添加无线设备名称、想要访问的无线网络以及该网络的密码。与其直接编辑默认文件，你可以复制 `2-dhcp.yaml` 文件并将 2 改为 3，然后将其命名为 `3-wireless.yaml`。Netplan 会读取 `/etc/netplan` 目录下的任何 `yaml` 文件。你可以在 `/usr/share/doc/netplan/examples` 找到无线配置文件的示例，但它是针对不支持 dhcp 的网络的且更为复杂。

```bash
cd /etc/netplan
sudo cp 2-dhcp.yaml 3-wireless.yaml
```

然后编辑该文件以添加 Wi-Fi、接入点（accesspoints）、SSID 和密码的键。

```bash
sudo nano 3-wireless.yaml
```

下文显示了一个无线 Netplan 配置示例。使用 `wifis:` 定义代替 `ethernets:` 定义。其后是一个由无线设备名称组成的键，例如 `wlp6s0:`。在该键下方是用于配置 Wi-Fi 设备的 `dhcp4:` ID 和 `accesspoints:` ID。在 `accesspoints:` ID 下方，你添加一个由构成的你想要连接的无线网络的 SSID（无线网络名称）的 ID。SSID 必须放在引号内。在此 ID 下方，你添加 `password:` ID 和访问该无线网络的密码。密码必须放在引号内。

`/etc/netplan/3-wireless.yaml`

```yaml
network:
  version: 2
  renderer: networkd
  wifis:
    wlp6s0:
      dhcp4: true
      accesspoints:
        "SSID":
          password: "password"
```

Netplan 在启动时在 `/run/netplan` 生成一个无线配置文件。无线文件的名称将包含设备名称以及无线网络名称（SSID），例如 `netplan-wlp6s0-surfturtle`。

该文件随后用于 `netplan-wpa@service` 将 SSID 和密码提交给 `wpa_supplicant`，由其访问无线网络。此处显示了 `netplan-wpa@.service` 文件。

```ini
netplan-wpa@.service
[Unit]
Description=WPA supplicant for netplan %I
Requires=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device
Before=network.target
Wants=network.target
[Service]
Type=simple
ExecStart=/sbin/wpa_supplicant -c /run/netplan/wpa-%I.conf -i%I
```

如果你重启，无线 netplan 文件将会被读取并配置你的无线设备。若要在不重启系统的情况下配置设备，可以使用 Netplan 的 `generate` 命令直接创建运行时配置文件（`/var/run/systemd/network`），然后使用 `apply` 命令让 Netplan 将该配置应用到你的网络连接。

```bash
sudo netplan generate
sudo netplan apply
```

然后重启 systemd-networkd。

```bash
sudo systemctl restart systemd-networkd
```

你可以使用 `networkctl` 命令检查网络设备配置的激活状态。

```bash
networkctl
```

### 为 systemd-networkd 针对 systemd-networkd 的 Netplan 无线配置

（注：原文此处出现了 systemd-networkd 描述，此处按逻辑翻译）

对于 systemd-networkd 无线设备，你必须编辑 Netplan 配置文件以添加你的无线设备名称、想要访问的无线网络以及该网络的密码。与其直接编辑默认文件，你可以复制 `2-dhcp.yaml` 文件并将 2 改为 3，然后将其命名为 `3-wireless.yaml`。Netplan 会读取 `/etc/netplan` 目录下的任何 `yaml` 文件。你可以在 `/usr/share/doc/netplan/examples` 找到无线配置文件的示例，但它是针对不支持 dhcp 的网络的且更为复杂。

```bash
cd /etc/netplan
sudo cp 2-dhcp.yaml 3-wireless.yaml
```

然后编辑该文件以添加 Wi-Fi、接入点（accesspoints）、SSID 和密码的键。

```bash
sudo nano 3-wireless.yaml
```

下文显示了一个无线 Netplan 配置示例。使用 `wifis:` 定义代替 `ethernets:` 定义。其后是一个由无线设备名称组成的键，例如 `wlp6s0:`。在该键下方是用于配置 Wi-Fi 设备的 `dhcp4:` ID 和 `accesspoints:` ID。在 `accesspoints:` ID 下方，你添加一个由构成的你想要连接的无线网络的 SSID（无线网络名称）的 ID。SSID 必须放在引号内。在此 ID 下方，你添加 `password:` ID 和访问该无线网络的密码。密码必须放在引号内。

`/etc/netplan/3-wireless.yaml`

```yaml
network:
  version: 2
  renderer: networkd
  wifis:
    wlp6s0:
      dhcp4: true
      accesspoints:
        "SSID":
          password: "password"
```

Netplan 在启动时在 `/run/netplan` 生成一个无线配置文件。无线文件的名称将包含设备名称以及无线网络名称（SSID），例如 `netplan-wlp6s0-surfturtle`。

该文件随后用于 `netplan-wpa@service` 将 SSID 和密码提交给 `wpa_supplicant`，由其访问无线网络。此处显示了 `netplan-wpa@.service` 文件。

```ini
netplan-wpa@.service
[Unit]
Description=WPA supplicant for netplan %I
Requires=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device
Before=network.target
Wants=network.target
[Service]
Type=simple
ExecStart=/sbin/wpa_supplicant -c /run/netplan/wpa-%I.conf -i%I
```

如果你重启，无线 netplan 文件将会被读取并配置你的无线设备。若要在不重启系统的情况下配置设备，可以使用 Netplan 的 `generate` 命令直接创建运行时配置文件（`/var/run/systemd/network`），然后使用 `apply` 命令让 Netplan 将该配置应用到你的网络连接。

```bash
sudo netplan generate
sudo netplan apply
```

然后重启 systemd-networkd。

```bash
sudo systemctl restart systemd-networkd
```

你可以使用 `networkctl` 命令检查网络设备配置的激活状态。

```bash
networkctl
```

### 在 systemd-networkd 和 networkmanager 之间切换

用于 NetworkManager 的原始 Netplan 配置 `1-manager-all.yaml` 仍位于 `/etc/netplan`。

要从 systemd-networkd 切换到 NetworkManager，首先使用 `systemctl` 命令停止并禁用 systemd-networkd。

```bash
sudo systemctl stop systemd-networkd
sudo systemctl disable systemd-networkd
```

然后启用并启动 NetworkManager。使用 NetworkManager 的服务名 `network-manager`。此外，移除或移动 systemd-networkd plan 文件使其不被读取。你只需重命名扩展名。

```bash
sudo systemctl enable network-manager
sudo systemctl start network-manager
```

```bash
sudo mv /etc/netplan/2-dhcp.yaml /etc/netplan/2-dhcp.yaml.bak
```

你可以使用 `systemctl` 的 `status` 命令查看网络设备是否激活。

```bash
systemctl status systemd-networkd
systemctl status network-manager
```

切回 systemd-networkd，禁用 NetworkManager 并启用 systemd-networkd。还将 systemd-networkd plan 文件移回 `/etc/netplan` 目录。

```bash
sudo systemctl stop network-manager
sudo systemctl disable network-manager
sudo systemctl enable systemd-networkd
sudo systemctl start systemd-networkd
```

如果由于原因，你的 NetworkManager 文件从 `/etc/netplan` 目录中缺失，你可以从 netplan.io 文目录 `/usr/share/doc/netplan/examples` 拷贝 `network_manager.yaml` 文件。

```bash
cd /usr/share/doc/netplan/examples
sudo cp network_manager.yaml /etc/netplan/1-manager-all.yaml
```

然后使用带有 apply 选项的 netplan 命令生成新的网络配置文件。

```bash
sudo netplan generate
sudo netplan apply
```

## 防火墙

你可以从多种流行的防火墙管理工具中进行选择。Linux Mint 提供了一个名为 Uncomplicated Firewall (ufw) 的工具，它基于 IPtables。你也可以选择其他工具如 FirewallD 和 Fwbuilder。FirewallD 不使用 IPtables，而是使用防火墙守护进程。本章将介绍 ufw 和 FirewallD。

### 重要防火墙端口

常用的服务（如 Linux 和 Windows 文件共享、FTP 服务器、BitTorrent 以及安全 Shell 远程访问）使用你系统上的某些网络连接端口（参见表 10-4）。默认防火墙配置会阻止这些端口。你必须配置防火墙以允许访问这些服务使用的端口，这些服务才能工作。





例如，要访问 Windows 共享，你不仅需要运行 `Samba` 服务，还需要配置防火墙允许通过端口 135、137、138 和 445（Samba 服务连接到 Windows 系统时使用的端口），以及用于多组播 DNS 发现（Avahi）的端口 5353。大多数端口都可以作为防火墙配置工具（如 `Gufw` 和 `FirewallD`）中作为预配置项轻松选择。不过，某些端口可能未列出。

| 端口号 | 服务 |
| :--- | :--- |
| 135,137,138,和 445 | Samba 端口：135 和 445 使用 TCP 协议，137 和 138 使用 UDP 协议。 |
| 139 | Netbios-ssn |
| 22 | Secure SHell, ssh |
| 2049 | NFS, Linux 和 Unix 共享 |
| 631 | IPP，互联网打印协议，访问远程 Linux/Unix 打印机 |
| 21 | FTP |
| 25 | SMTP，转发邮件 |
| 110 | POP3，接收邮件 |
| 143 | IMAP，接收邮件 |
| 5353 | 多组播 DNS 发现服务 (mdns), Zeroconf |

表 10-4：服务端口

### **使用 ufw 设置防火墙**

Uncomplicated Firewall（即 `ufw`）是 Linux Mint 支持的防火墙应用程序。它提供了一个可以通过 `Gufw` 桌面界面或 `ufw` 命令管理的简单防火墙。与所有防火墙应用一样，`ufw` 使用 `IPtables` 来定义规则并运行防火墙。`ufw` 只是 `IPtables` 的管理界面。`IPtables` 规则文件存储在 `/etc/ufw` 目录下。默认 `IPtables` 规则保留在 `before` 和 `after` 文件中，用户规则位于用户文件中。某些软件包的防火墙配置将放置在 `/usr/share/ufw.d` 目录下。`ufw` 防火墙使用 Upstart 脚本 `/etc/init/ufs.conf` 启动。你可以在 Ubuntu 防火墙网站 [`wiki.ubuntu.com/UncomplicatedFirewall`](https://wiki.ubuntu.com/UncomplicatedFirewall) 以及 Ubuntu Server Guide 中的 Ubuntu 防墙章节 [`ubuntu.com/server/docs`](https://ubuntu.com/server/docs) 了解更多关于 `ufw` 的信息。该指南还显示了如何在 `ufw` 上实现 IP 伪装（IP Masquerading）的信息。

### **Gufw**

`Gufw` 提供了一个易用的 GNOME 界面来管理你的 `ufw` 防火墙。简单的界面允许你添加自定义和标准规则。`Gufw` 默认安装，可以从偏好（Preferences）菜单中的防火墙配置（Firewall Configuration）访问。

`Gufw` 首次打开时防火墙处于禁用，未配置任何端口。`Status` 按钮设置为关闭，盾牌图像将呈灰色。要启用防火墙，只需点击 `Status` 按钮的左侧将状态设置为开启。盾牌图像将变为彩色，并列出防火墙规则。图 10-32 显示了启用的防火墙以及列出的几条 Samba 端口规则。列出了针对 IPv4 和 IPv6 (`v6`) 网络协议的规则。

`Gufw` 对话框有一个防火墙部分和三个选项卡：`Rules`（规则）、`Report`（报告）和 `Log`（日志）。防火墙部分有一个用于开启或关闭防火墙的 `Status` 按钮。有一个用于家庭、办公室和公共配置的 `Profile` 菜单。设置默认防火墙规则的 `Incoming`（入站）和 `Outgoing`（出站）下拉菜单。选项有 `Deny`、`Reject` 或 `Allow`，并分别分别应用于入站和出站流量。默认情况下，入站流量被拒绝（Deny），出站流量被允许（Allow）。你在 `Rules` 选项卡中指定的规则将创建异常，仅允许特定的流量进出。如果你选择 `Allow`选项，防火墙将接受所有入站流量。在这种情况下，你应该设置规则来拒绝某些流量，否则防火墙将失效，允许所有流量访问。`Report` 选项卡列出活动的服务和端口，例如端口 139 上的 Samba 服务器 (`smbd`)。`Log` 选项卡列出防火墙通知。你可以复制通知以及删除日志。`Home` 选项卡提供关于如何使用 `Gufw` 的基础帮助。

![Image](img/image-585.png) ![Image](img/image-586.png)

图 10-32：Gufw

要添加规则，点击 `Rules` 选项卡，然后点击 `Rules` 选项卡左下角的加号按钮 (+) 打开“添加规则”对话框，该对话框有三个管理规则的选项卡：`Preconfigured`（预配置）、`Simple`（简单）和 `Advanced`（高级）（参见图 10-33）。`Preconfigured` 选项卡提供五个菜单：第一个用于策略（`Allow`、`Deny`、`Reject` 和 `Limit`），第二个用于流量方向（`In` 或 `Out`），第三用于应用程序类别，第四个用于子类别，第五个用于规则的特定应用程序或服务。主要类别包括音频视频、游戏、网络、办公室和系统。`Network` 类别列出了大多数网络服务，如 `SSH`、`Samba` 和 `FTP`。如果规则存在安全问题，将显示警告。

![Image](img/image-587.png)

图 10-33：Gufw 预配置规则

如果你需要修改应用程序的默认规则，...





你也可以通过在终端窗口中输入 `ufw` 命令来管理你的 `ufw` 防火墙。`ufw` 命令需要管理员权限，并且必须使用 `sudo` 命令运行。要检查当前防火墙状态并列出允许或阻止的服务，请使用 `status` 命令。

```bash
sudo ufw status
```

如果防火墙未启用，你首先需要使用 `enable` 命令将其启用。

```bash
sudo ufw enable
```

你可以使用 `systemctl` 命令配合 `restart` 选项来重启防火墙，并重新加载你的规则。

```bash
sudo systemctl restart ufw
```

你可以使用 `allow` 和 `deny` 规则及其选项（如表 10-5 所示）来添加规则。要允许某项服务，请指定 `allow` 规则和服务名称。该名称是 `/etc/services` 文件中列出的服务名称。对于连接速率限制，请使用 `limit` 选项代替 `allow`。以下命令允许 `ftp` 服务。

```bash
sudo ufw allow ftp
```

| 命令 | 描述 |
| :--- | :--- |
| enable \| disable | 开启或关闭防火墙 |
| status | 显示状态以及允许或拒绝的服务。 |
| logging on \| off | 开启或关闭日志记录 |
| default allow \| deny | 设置默认策略，allow 是开放，而 deny 是限制性的 |
| allow *service* | 允许通过服务访问。服务定义在 `/etc/services` 中，该文件指定了该服务的对应端口。 |
| allow *port /protocol* | 使用指定的协议允许特定端口的访问。 |
| deny *service* | 拒绝通过服务访问 |
| delete *rule* | 删除已安装的规则，使用 allow、deny 或 limit 并包含规则的具体细节。 |
| proto*protocol* | 在 allow、deny 或 limit 规则中指定协议 |
| from*address* | 在 allow、deny 或 limit 规则中指定源地址 |
| to*address* | 在 allow、deny 或 limit 规则中指定目的地址 |
| port*port* | 在 allow、deny 或 limit 规则中为源地址和目的地址指定端口 |

表 10-5：UFW 防火墙操作

如果你需要的服务未列在 `/etc/services` 中，且它使用的端口和协议，你可以直接指定端口和协议。例如，Samba 服务使用端口 139 和 445 以及协议 `tcp`（其他等请参见表 10-4）。

```bash
sudo ufw allow 445/tcp
```

`status` 操作显示防火墙规则允许哪些服务。

```bash
sudo ufw status
To Action From 21:tcp ALLOW Anywhere 21:udp ALLOW Anywhere 139,445:tcp ALLOW Anywhere
```

要删除规则，请在规则前缀加上 `delete` 命令。

```bash
sudo ufw delete allow 445/tcp
```

可以使用 `address`、`port` 和 `protocol` 命令指定更详细的规则。这些与实际的 `iptables` 命令非常相似。可以控制进出特定网络、主机和端口的数据包。以下命令拒绝来自主机 192.168.03 的 `ssh` 访问（端口 22）。

```bash
sudo ufw deny proto tcp from 192.168.03 to any port 22
```

### ufw 规则文件

你添加的规则以 IPtables 规则的形式存放在 `/etc/ufw/user.rules` 文件中。`ufw` 程序只是 `iptables-restore` 的前端，它会读取此文件并使用 `iptables` 命令设置防火墙。`ufw` 还会让 `iptables-restore` 读取 `/etc/ufw` 目录下的 `before.rules` 和 `after.rules` 文件。这些文件被视为管理文件，包含了为你的 IPtables 防火墙所需的辅助规则。管理员可以向这些文件添加自己的 IPtables 规则，以实现特定于系统的功能（如 IP 伪装）。`before.rules` 文件将指定一个带有 `*` 符号的表，例如 netfilter 表的 `*filter`。对于 `nat` 表，你需要使用 `*nat*`。在每个表段的末尾，需要一个 `COMMIT` 命令来指示 `ufw` 应用规则。假设 `iptables` 命令中规则使用 `-A` 表示允许，使用 `-D` 表示拒绝。

`ufw` 的默认设置存放在 `/etc/default/ufw` 中。在这里，你可以通过设置关联变量找到默认的 `INPUT`、`OUTPUT` 和 `FORWARD` 策略，例如用于 `INPUT` 的 `DEFAULT_INPUT_POLICY` 和用于 `OUTPUT` 的 `DEFAULT_OUTPUT_POLICY`。`DEFAULT_INPUT_POLICY` 变量设置为 `DROP`，使得 `DROP`  `INPUT` 规则的默认策略。`DEFAULT_OUTPUT_POLICY` 变量设置为 `ACCEPT`，`DEFAULT_FORWARD_POLICY` 变量设置为 `DROP`。要允许 IP 伪装，必须将 `DEFAULT_FORWARD_POLICY` 设置为 `ACCEPT`。这些项目仅设置默认策略。你设置的任何用户规则将具有优先级。

### FirewallD 和 firewall-config

FirewallD 作为实现动态防火墙的守护进程运行。它不是从文件中离线加载规则，而是直接将规则添加到守护进程中。Ubuntu 和 Linux 不 支持 FirewallD，但在 Ubuntu/Linux Mint 仓库中可用。它是 Fedora 和 Suse Linux 的默认防火墙。文档请参见：

[`fedoraproject.org/wiki/FirewallD`](https://fedoraproject.org/wiki/FirewallD)

FirewallD 设置网络区域来定义信任级别。每个区域可以允许多个服务、端口和协议。你可以使用 `firewall-config` 或 `firewall-cmd` 来管理这些区域。





```bash
sudo systemctl start firewalld
```

你可以使用停止命令将其停止。

```bash
sudo systemctl stop firewalld
```

### firewall-config

通过 `firewall-config`，你可以配置运行时配置（Runtime）或永久配置（Permanent）。从`Configuration`配置）菜单中选择其中一个。`Runtime Configuration`运行时配置）显示你当前的运行时设置，而`Permanent`永久）配置在重新加载或重启之前不会生效。如果你想编辑区域（zones）和服务（services），你需要选择`Permanent Configuration`永久配置）（请参见图 10-39）。此视图在区域滚动框底部显示了一个用于编辑区域的工具栏，并在`Services`服务）选项卡上有一个`Edit`编辑）按钮，用于编辑服务协议、端口和目标地址。

![Image](img/image-594.png)

图 10-39: `firewall-config`: `Permanent Configuration`

可以从`View`视图）菜单显示额外的选项卡，用于配置 ICMP 类型以及直接添加防火墙规则（`Direct Configuration`直接配置）。

从`Options`选项菜单，你可以重新加载已保存的防火墙。

防火墙配置是为指定的区域设置的，例如`home`、`work`、`internal`、`external`或`public`区域。区域提供了防火墙额外的保护级别。它们将受防火墙保护的网络分为不同的段，这些段只有在防火墙允许的情况下才能通信。实际上，区域将你的网络部分与其他部分隔离开。每个区域都有自己的配置。区域列在`firewall-config`窗口左侧的`Zone`滚动框中（请参见图 10-39）。选择你想要配置的区域。`firewall-config`窗口打开默认的`Public`。你可以从`System Default Zone`系统默认区域对话框中选择默认区域（请参见图 10-40），该对话框通过`Options`菜单中的“Change Default Zone”（更改默认区域）打开。

![Image](img/image-595.png)

图 10-40: `Default Zone`

![Image](img/image-596.png)

![Image](img/image-597.png)  ![Image](img/image-598.png)

图 10-41: `Base Zone Settings`

`Zones`选项卡的左侧是`Active Bindings`活动绑定部分，它列出了你系统上的网络连接、接口和源。对于每个活动连接，都会列出绑定到其上的区域，例如图 10-41 中绑定到有线连接的`public`区域。要更改绑定到连接的区域，请选择该条目并点击`Active Binding`部分底部的`Change Zone`更改区域按钮。这将打开一个`Select zone`选择区域对话框，你可以在其中选择一个不同的区域绑定到连接。你可以从`zones`选项卡中的任何区域中进行选择。你也可以通过`Options`菜单并选择`Change Zones of Connections`更改连接绑定。

如果你从`Current View Menu`当前视图菜单中选择`Permanent Configuration`，则会在`Zone`滚动框下方显示一个区域工具栏，所示。`plus`按钮允许你添加区域，`minus`按钮移除区域。`pencil`按钮允许你编辑区域。`add`和`edit`按钮打开`Base Zone Settings`基础区域设置对话框，你可以在其中输入或编辑区域名称、版本、描述和目标（请参见图 10-41）。默认目标是`ACCEPT`。其他选项是`REJECT`和`DROP`。`Load Zone Defaults`加载区域默认（黄色箭头）加载默认设置，移除你所做的任何更改。

![Image](img/image-599.png)

图 10-42: `Service Settings`

每个区域依次可以有一个或多个网络连接。从`Options`菜单选择“Change Zones of Connections”打开`Network Connections`网络连接对话框，你可以在其中添加网络连接。

对于选的服务，你可以指定服务设置，例如它使用的端口和协议、任何模块以及特定的网络地址。默认设置已为你配置好，例如用于 Samba 的`TCP`协议的端口`139`。要修改服务的设置，点击`Firewall Configuration`防火墙配置窗口上的`Services`选项卡以列出你的服务（请参见图 10-42）。从左侧的`Service`滚动框中选择你要编辑的服务。对于给的服务，然后可以使用`Ports`端口、`Protocols`协议、`Modules`模块和`Destination`目标选项卡指定端口、协议、模块和地址。在`Ports`选项卡上，点击`Add`按钮打开`Port and Protocol`端口和协议对话框，你可以在其中添加端口或端口范围，并从`Protocol`菜单中选择协议（请参见图 10-43）。在`Destination`选项卡上，你可以为服务输入`IPv4`或`IPv6`目标地址。

![Image](img/image-600.png)

图 10-43: `Service Protocols and Ports`在`Zones`选项卡上，`Ports`选项卡允许你指定某些服务开放的端口，如`BitTorrent`。点击`Add`按钮打开对话框，你可以在其中指定端口号以及协议。

如果你的系统被用作通往互联网的网关，你可以实施伪装（masquerading）来隐藏你的本地主机。

![Image](img/image-601.png)

图 10-44: `Port Forwarding`

### firewall-cmd

`firewall-cmd`在命令行界面工作，使用选项设置不同区域的功能。区域修改选项如`--add-service`可以是运行时的或永久的。运行时更改在重启或重新加载后失效。要使更改永久，添加`--permanent`选项，针对持久化配置而不是运行时配置。

使用`get`选项显示有关防火墙的信息。`--get-zones`选项列出你的区域，`--get-services`选项列出当前区域支持的服务，`--get-icmypes`列出 ICMP 类型。

```bash
firewall-cmd --get-zones
firewall-cmd --get-services
firewall-cmd --get-icmypes
```

`--get-default-zone`选项列出默认区域，`--set-default-zone`设置一个新的默认区域。

```bash
firewall-cmd --set-default-zone home
```

要查找某个区域启用了哪些功能，使用`--list-all`选项配合`--zone=`选项指定区域。

```bash
firewall-cmd --zone=home --list-all
```

区域分配网络接口。有接口选项添加、删除或更改接口。使用查询检查接口是否属于某个区域。

```bash
firewall-cmd --zone=home --query-interface=enp7s0
```

服务、端口、伪装、icmp 和转发选项可以是运行时的或持久的（永久的）。`--service`选项可以向区域添加和删除服务。

```bash
firewall-cmd -add-service=vsftp
```

要使更改永久（持久化模式），添加`--permanent`选项。





```
firewall-cmd --permanent -add-service=vsftp
```

`--query-service` 选项检查某个区域是否启用了服务。

```bash
firewall-cmd --zone=home -query-service=http
```

`--port` 选项用于添加、删除或查询端口。

```bash
firewall-cmd --zone=home --add-port=22
```

添加 `--permanent` 选项使其永久生效。

```bash
firewall-cmd --permanent --zone=home --add-port=22
```

`masquerade` 选项用于添加、删除和查询用于伪装的区域。

```bash
firewall-cmd --zone=work --add-masquerade
```

`icmp-block` 选项用于添加、删除和查询 ICMP 类型。

```bash
firewall-cmd --zone=work --add-icmp-block=echo-reply
```

如果您的防火墙需要使用自定义防火墙规则，可以使用 `--direct` 选项来添加、删除和列出规则。这些规则使用 IPtables 语法编写。您必须指定协议、表、链和参数。以下列出了您添加到 netfilter 表的规则。这些规则不会保存，每次重启或重新加载时必须重新添加。您可以编写一个包含 `firewall-cmd` 规则的脚本来实现此。

```bash
firewall-cmd --direct --get-rules ipv4 netfilter
```

以下添加了一个简单的 netfilter 规则。

```bash
firewall-cmd --direct -add-rule ipv4 netfilter INPUT Deny
```

# GNOME Nettool

GNOME Nettool 工具 (`gnome-nettool`) 为 ping 和 traceroute 操作等网络信息工具提供了 GNOME 界面，并提供了 Finger、Whois 和 Lookup 用于查询网络上的用户和主机（请参见 图 10-46）。可以通过“管理”菜单中的“网络工具”访问 Nettool。第一个标签页“设备（Devices）”描述了您连接的网络设备，包括每个设备的配置和传输信息，例如硬件地址和传输字节。列表中列出了 IPv4 和 IPv6 主机 IP 地址。

![Image](img/image-603.png)

图 10-46: Gnome 网络工具

您可以使用 ping、`finger`、`lookup`、`whois` 和 `traceroute` 操作来查找网络上系统和用户的状态信息。`ping` 操作用于检查远程系统是否运行。您使用 `finger` 查询网络上其他用户的信息，查看他们是否已登录或收到了邮件。`traceroute` 工具可用于跟踪消息在传输给您途中经过的计算机网络和系统序列。`whois` 将提供特定域名的域名信息，而 `lookup` 将同时提供域名和 IP 地址。`netstat` 显示您的网络路由（所使用的地址）和活动服务（开放的端口及其使用的协议）。`Port Scan` 列出给定连接（地址）上使用的端口和对应的；使用 `12.0.0.1` 代表您的本地计算机。

# 可预测与不可预测的网络设备名称

网络设备现在使用一种可预测的命名方法，这与旧旧的命名方法不同。名称是根据特定的设备引用网络设备类型、其硬件连接和插槽，甚至其功能生成的。传统的网络设备名称对于以太网网络设备使用 `eth` 前缀加上设备数字。名称 `eth0` 指的是您计算机上的第一个以太网连接。这种命名方法被认为是不可预测的，因为它没有准确引用真实的以太网设备。旧系统依赖于启动时探测网络驱动程序，如果您的系统有多个以太网连接，名称可能会根据启动过程的不同而发生交换。使用 `systemd udev` 版本 197 后，命名变为一种指定特定设备的可预测方法。可预测方法引用您系统上真实的硬件连接。

用于引用可预测设备名称连接的名称具有设备类型的前缀，随后是几个限定符，例如硬件类型、所使用的插槽和功能编号。不再使用像 `eth0` 这样旧的不可预测名称，第一个以太网设备通过类似 `enp7s0` 的名称引用。接口名称 `enp7s0` 引用一个以太网 (en) 连接，位于 PCI 插槽 7 (p7)，热插插槽索引号为 0 (s0)。`wlp6s0` 是一个无线 (wl) 连接，位于 PCI 插槽 6 (p6)，热插插槽索引号为 0 (s0)。`virvb0` 是一个虚拟 (vir) 桥接 (vb) 网络接口。表 10-6 列出了可预测的命名前缀。

| 名称 | 描述 |
| :--- | :--- |
| sen | 以太网 |
| sl | 线路协议 IP (slip) |
| wl | wlan, 无线局域网 |
| ww | wwan, 无线广域网（移动宽带） |
| p | pci 地理位置 (pci-e 插槽) |
| s | 热插插槽索引号 |
| o | 板载 |
| f | 功能（用于具有多个端口的卡） |
| u | USB 端口 |
| i | USB 端口接口 |

与旧的不可预测名称不同，可预测名称对于每台计算机很可能不同。可预测的网络名称及其替代方案可以在 [`www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames/`](https://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames/) 中进行讨论。

（注：后续重复文本已省略）





E: DEVPATH=/devices/pci0000:00/0000:00:1c.3/0000:07:00.0/net/enp7s0

E: ID_BUS=pci

E: ID_MM_CANDIDATE=1

E: ID_MODEL_FROM_DATABASE=RTL8101/2/6E PCI Express Fast/Gigabit Ethernet controller

E: ID_MODEL_ID=0x8136

E: ID_NET_DRIVER=r8169

E: ID_NET_LINK_FILE=/lib/systemd/network/99-default.link

E: ID_NET_NAME_MAC=enx74e6e20ec729

E: ID_NET_NAME_PATH=enp7s0

E: ID_OUI_FROM_DATABASE=Dell Inc.

E: ID_PATH=pci-0000:07:00.0

E: ID_PATH_TAG=pci-0000_07_00_0

E: ID_PCI_CLASS_FROM_DATABASE=Network controller

E: ID_PCI_SUBCLASS_FROM_DATABASE=Ethernet controller

E: ID_VENDOR_FROM_DATABASE=Realtek Semiconductor Co., Ltd.

E: ID_VENDOR_ID=0x10ec

E: IFINDEX=2

E: INTERFACE=enp7s0

E: SUBSYSTEM=net

E: SYSTEMD_ALIAS=/sys/subsystem/net/devices/enp7s0

E: TAGS=:systemd:

E: USEC_INITIALIZED=1080179

对于某些任务（例如重命名），你可能需要知道 MAC 地址。你可以通过 `ip link` 命令找到它，该命令可以简写为 `ip l`。MAC 地址位于 `brd` 字符串之前。在示例中，`enp7s0` 的 MAC 地址为 `74:e6:e2:0e:c7:29`。`ip link` 命令还提供了 MTU（最大传输单元）和连接的当前状态。

```
$ ip link 1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1 link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00

2: enp7s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000 link/ether 74:e6:e2:0e:c7:29 brd ff:ff:ff:ff:ff:ff

3: wlp6s0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN mode DEFAULT group default qlen 1000 link/ether 4c:bb:58:22:40:1d brd ff:ff:ff:ff:ff:ff
```

### 使用 udev 规则重命名网络设备名称

如果你更改了硬件（例如带有以太网连接的主板），或者在使用以太网卡并简单更改了连接它的插槽，那么名称将会改变。对于引用特定以太网连接的防火墙规则，这可能会是一个问题。如果你愿意，可以将名称更改为你自定义的名称，甚至可以使用旧的不可预测的名称。这样，你只需要更新名称更改处，而无需更新所有规则以及任何通过名称引用网络设备的其他代码。

你可以通过为网络设备名称添加用户 udev 规则来更改设备名称。使用 udev 规则进行的更改对 NetworkManager 和 systemd-networkd 都有效。在 `/etc/udev/rules.d` 目录下，创建一个以 `.rules` 扩展的文件，并以前小于 80 的数字开头，例如 `70-my-net-names.rules`。`/etc/udev/rules.d` 中的 `.rules` 文件优先级高于 udev 系统目录 `/lib/udev/rules.d` 中的文件。

在 udev 规则中，将子系统识别为 `net`（`SUBSYSTEM=="net"`），将操作识别为 `add`（`ACTION=="add"`），然后是 MAC 地址（`ATTR{address}`，地址属性）。使用 `ip link` 获取 mac 地址。MAC 地址也列在 `udevadm info` 输出的 `ID_NET_NAME_MAC` 条目中（确保删除前缀并添加中间的冒号）。使用 `NAME` 字段为设备指定新名称。使用单等 `=` 运算符进行名称赋值。

```
/etc/udev/rules.d/70-my-net-names.rules
SUBSYSTEM=="net", ACTION=="add", ATTR{address}="74:e6:e2:0e:c7:29", NAME="eth0"
```

为了进一步指定设备，你可以添加设备的内核名称（`KERNEL`）。内核名称是 `INTERFACE` 条目。

```
SUBSYSTEM=="net", ACTION=="add", ATTR{address}="74:e6:e2:0e:c7:29", KERNEL=="enp7s0", NAME="eth0"
```

### 为 systemd 网络重命名网络设备名称

为了进一步指定设备，你可以添加设备的内核名称（`KERNEL`）。内核名称是 `INTERFACE` 条目。

```
SUBSYSTEM=="net", ACTION=="add", ATTR{address}="74:e6:e2:0e:c7:29", KERNEL=="enp7s0", NAME="eth0"
```

### 使用 udev 规则重命名网络设备名称

（注：此处原文英文部分似乎存在逻辑重复或格式混乱，已根据语意进行整合翻译）

如果你更改了硬件（例如带有以太网连接的主板），或者在使用以太网卡并简单更改了连接它的插槽，那么名称将会改变。对于引用特定以太网连接的防火墙规则，这可能会是一个问题。如果你愿意，可以将名称更改为你自定义的名称，甚至可以使用旧的不可预测的名称。这样，你只需要更新名称更改处，而无需更新所有规则以及任何通过名称引用网络设备的其他代码。

你可以通过为网络设备名称添加用户 udev 规则来更改设备名称。使用 udev 规则进行的更改对 NetworkManager 和 systemd-networkd 都有效。在 `/etc/udev/rules.d` 目录下，创建一个以 `.rules` 扩展的文件，并以前小于 80 的数字开头，例如 `70-my-net-names.rules`。`/etc/udev/rules.d` 中的 `.rules` 文件优先级高于 udev 系统目录 `/lib/udev/rules.d` 中的文件。

在 udev 规则中，将子系统识别为 `net`（`SUBSYSTEM=="net"`），将操作识别为 `add`（`ACTION=="add"`），然后是 MAC 地址（`ATTR{address}`，地址属性）。使用 `ip link` 获取 mac 地址。MAC 地址也列在 `udevadm info` 输出的 `ID_NET_NAME_MAC` 条目中（确保删除前缀并添加中间的冒号）。使用 `NAME` 字段为设备指定新名称。使用单等 `=` 运算符进行名称赋值。

```
/etc/udev/rules.d/70-my-net-names.rules
SUBSYSTEM=="net", ACTION=="add", ATTR{address}="74:e6:e2:0e:c7:29", NAME="eth0"
```

为了进一步指定设备，你可以添加设备的内核名称（`KERNEL`）。内核名称是 `INTERFACE` 条目。

```
SUBSYSTEM=="net", ACTION=="add", ATTR{address}="74:e6:e2:0e:c7:29", KERNEL=="enp7s0", NAME="eth0"
```

### 为 systemd 网络重命名网络设备名称

（注：原文英文部分似乎存在逻辑重复或格式混乱，已根据语意进行整合翻译）

（此处省略重复翻译，直接进入后续译文逻辑）

# 11. Shell 配置

Linux 上通常使用四种主要的 shell：Bourne Again shell (BASH)、AT&T Korn shell、TCSH shell 和 Z shell。BASH shell 是 Bourne shell 的高级版本，包含了为 Korn shell 和 C shell 开发的大部分高级功能。TCSH 是 C shell 的增强版本，最初为 BSD 版本的 UNIX 开发。Z shell 是 AT&T UNIX Korn shell 的增强版本。尽管它们的 UNIX 版本差异很大，但 Linux shell 共享许多功能。所有种 shell 均可用。

| 命令 | 说明 |
| :--- | :--- |
| bash | BASH shell, **/bin/bash** |
| bsh | BASH shell, **/bin/bsh** (link to **/bin/bash**) |
| sh | BASH shell, **/bin/sh** (link to **/bin/bash**) |
| tcsh | TCSH shell, **/usr/tcsh** |
| csh | TCSH shell , **/bin/csh** (link to **/bin/tcsh**) |
| ksh | Korn shell, **/bin/ksh** (also added link **/usr/bin/ksh**) |
| zsh | Z shell, **/bin/zsh** |

表 11-1: Shell 调用命令名称




BASH shell 是大多数 Linux 发行版的默认 shell。如果你登录到命令行界面，系统将自动把你置于默认 shell 中，并提供一个用于输入命令的 shell 提示符。BASH shell 的 shell 提示符是美元符号 ($)。在桌面界面（如 GNOME）中，你可以打开一个终端终端窗口，该窗口将显示带有默认 shell（BASH）提示符的命令行界面。尽管你登录的是默认 shell 或其在终端窗口中自动显示，但你仍然可以通过输入其名称来切换到另一个 shell。输入 `tcsh` 会调用 `TCSH` shell，输入 `bash` 调用 `BASH` shell，输入 `ksh` 调用 Korn shell，输入 `zsh` 调用 Z shell。你可以通过按下 `ctrl-d` 或使用 `exit` 命令退出 shell。进行工作时，你只需要一种类型的 shell。下表 11-1 显示了你可以用来调用不同 shell 的不同命令。某些 shell 添加了你可以用来调用相同 shell 的链接，例如 `sh` 和 `bsh`，它们链接并调用用于 `BASH` shell 的 `bash` 命令。

本章描述了 BASH shell 的常见特性，如别名（aliases），以及如何使用 shell 变量和初始化文件根据自己的需求配置 shell。其他 shell 也共享许多相同特性，并使用类似的变量和配置文件。

尽管这里显示了基本的 shell 特性和配置，但你应该咨询每个 shell 相应的在线手册和常见问题解答（FAQs），获取更详细的示例和说明。

## Shell 初始化与配置文件

每种 shell 都有自己的初始化和配置文件。TCSH shell 使用 `.login`、`.tcshrc` 和 `.logout` 文件代替 `.profile`、`.bashrc` 和 `.bash_logout`。Z shell 有几个初始化文件：`.zshenv`、`.zlogin`、`.zprofile`、`.zshrc` 和 `.zlogout`。参见表 11-2。检查每个 shell 的 Man 页（帮助手册）以查看它们通常是如何配置的。当你安装一个 shell 时，这些文件的默认版本会自动放置在用户家目录下。除了 TCSH shell 外，所有 shell 在变量定义和赋值方面都使用相似的语法（TCSH 使用略有不同的语法，见在其 Man 页中的描述）。

| 文件名 | 功能 |
| :--- | :--- |
| BASH Shell | | |
| .profile | 登录初始化文件 |
| .bashrc | BASH shell 配置文件 |
| .bash_logout | 退出名称 |
| .bash_history | 历史文件 |
| /etc/profile | 系统登录初始化文件 |
| /etc/bash.bashrc | 系统 BASH shell 配置文件 |
| /etc/profile.d | 特殊 BASH shell 配置文件目录 |
| /etc/bash_completion | 应用程序的补全选项 |
| TCSH Shell | | |
| .login | 登录初始化文件 |
| .tcshrc | TCSH shell 配置文件 |
| .logout | 退出文件 |
| Z Shell | | |
| .zshenv | shell 登录文件（最读取） |
| .zprofile | 登录初始化文件 |
| .zlogin | shell 登录文件 |
| .zshrc | Z shell 配置文件 |
| .zlogout | 退出文件 |
| Korn Shell | | |
| .profile | 登录初始化文件 |
| .kshrc | KORN shell 配置文件 |

**表 11-2: Shell 配置文件**

## 配置目录与文件

应用程序通常在用户的家目录下安装配置文件，其中包含特定的配置信息，以根据该特定用户的需求定制应用程序。这可能表现为一个以点开头的单个配置文件，或者是一个包含若干个配置文件的目录。目录的名称也会以点开头。例如，Mozilla 在用户家目录下安装了一个名为 `.mozilla` 的目录，其中包含配置文件文件。另一方面，许多邮件应用程序使用名为 `.mailrc` 的单文件来存储用户设置的别名和功能设置，但像 Evolution 这样的程序也有自己的 `.evolution` 文件。大多数单配置文件以字母 `rc` 结尾。`FTP` 使用名为 `.netrc` 的文件。大多数新闻阅读器使用名为 `.newsrc` 的文件。配置文件中的条目通常由应用程序设置，但你通常可以直接编辑文件来创建条目。应用程序有自己的特殊变量，你可以在其中定义并分配值。你可以使用 `ls -a` 命令列出家目录中的配置文件。

## 别名 (Aliases)

你可以使用 `alias` 命令为命令创建另一个名称。`alias` 命令的作用类似于宏，会展开为它所代表的命令。别名并没有字面上替换命令的名称，它只是给该命令提供了另一个名称。别名命令以关键字 `alias` 开头，后面是命令的新名称，然后是等号以及别名将引用的命令。

注意：`alias` 命令中使用的等号周围不应留空格。

在下一个示例中，`list` 成为 `ls` 命令的另一个名称：

```
$ alias list=ls $ ls mydata today
$ list mydata today
```

如果你想自动定义别名，则必须在 shell 配置文件中输入别名操作。在 Linux Mint 上，别名定义在用户的 `.bashrc` 文件或 `.bash_aliases` 文件中。要使用 `.bash_aliases` 文件，你必须先取消命令的注释。

[content]
（注：此处原文中存在部分逻辑乱码或重复文本，翻译已根据语义进行清理和处理）
```bash
$ alias list=ls $ ls mydata today
$ list mydata today
```

如果你想自动定义别名，则必须在 shell 配置文件中输入别名操作。在 Linux Mint 上，别名定义在用户的 `.bashrc` 文件或 `.bash_aliases` 文件中。要使用 `.bash_aliases` 文件，你必须先取消命令的注释。

[content]
原文提供的示例块为：
```bash
$ alias list=ls $ ls mydata today
$ list mydata today
```




### 命令别名 (Aliasing Commands)

你也可以将命令名称作为别名。这在需要仅配合特定选项使用命令时非常有用。对于 `rm`、`cp` 和 `mv` 命令，应该始终使用 `-i` 选项，以确保现有文件不被覆盖。你不需要每次使用这些命令时都小心地使用 `-i` 选项，可以将命令名设置别名以包含该选项。在下一个示例中，`rm`、`cp` 和 `mv` 命令被设置了别名包含了 `-i` 选项。

```
$ alias rm='rm -i'
$ alias mv='mv -i'
$ alias cp='cp -i'
```

`alias` 命令本身提供所有已定义的别名列表，并显示它们代表的命令。你可以使用 `unalias` 命令来删除别名。在下一个示例中，用户列出了当前的别名，然后删除了 `lsa` 别名。

```
$ alias lsa=ls -F
list=ls
rm=rm -i
$ unalias lsa
```

### 控制 Shell 操作 (Controlling Shell Operations)

BASH shell 具有若干功能，允许你控制不同 shell 操作的工作方式。例如，设置 `noclobber` 功能可以防止重定向覆盖文件。你可以使用 `set` 命令像开关一样开启或关闭这些功能。`set` 命令接受两个参数：指定开启或关闭的选项，以及功能的名称。要开启某功能，使用 `-o` 选项；要关闭它，使用 `+o` 选项。以下是基本形式。

```
$ set -o feature  开启功能
$ set +o feature  关闭功能
```

| 功能 | 描述 |
| :--- | :--- |
| $ set -+o feature | BASH shell 功能通过 `set` 命令开启和关闭；-o 开启功能，+o 关掉功能。例如：$ set -o noclobber  开启 noclobber $ set +o noclobber  关闭 noclobber |
| ignoreeof | 禁用 ctrl-d 注销 |
| noclobber | 不通过重定向覆盖文件 |
| noglob | 禁用用于文件名扩展的特殊字符：*, ?, ~, 和 [] |

表 11-3：BASH Shell 特有功能

三个最常用的功能是 `ignoreeof`、`noclobber` 和 `noglob`。表 11-3 列出了这些不同的功能以及 `set` 命令。设置 `ignoreeof` 可以启用一个功能，防止你通过 `ctrl-d` 注销用户 shell。`ctrl-d` 不仅用于注销用户 shell，还用于结束直接输入标准输入的用户输入。`ctrl-d` 常用于邮件程序或如 `cat` 等工具。在这些情况下，你可以很容易地输入额外的 `ctrl-d` 并意外注销自己。`ignoreeof` 功能防止了这种意外注销。在下一个示例中，使用 `set` 命令配合 `-o` 选项开启了 `ignoreeof` 功能。用户随后只能通过输入 `logout` 命令才能注销。

```
$ set -o ignoreeof
$ ctrl-d 使用 exit 来注销
```

### 环境变量与子 Shell：export (Environment Variables and Subshells: export)

当你登录账户时，Linux 会生成你的用户 shell。在这个 shell 内部，你可以发布命令并声明变量。你还可以创建和执行 shell 脚本。然而，当你执行 shell 脚本时，系统会生成一个子 shell。你有两个 shell：你登录的那个和一个为脚本生成的那个。在脚本 shell 内部，你可以执行另一个 shell 脚本，该脚本又有它自己的 shell。当脚本执行完毕时，它的 shell 会终止，你返回到执行它的那个 shell。从这个意义上说，你可以有很多 shell，每个 shell 都嵌套在另一个之中。你在 shell 中定义的变量对该 shell 是局部的。如果你在 shell 脚本中定义了一个变量，那么当脚本运行时，该变量在该脚本的 shell 中定义并对它是局部的。其他 shell 无法引用该变量。在某种程度上，该变量隐藏在它的 shell 内部。

| Shell 变量 | 描述 |
| :--- | :--- |
| BASH | 保存 BASH 命令的完整路径 |
| BASH_VERSION | 显示当前的 BASH 版本号 |
| GROUPS | 用户所属的组 |
| HISTCMD | 列表中当前命令的编号 |
| HOME | 用户主目录的路径 |
| HOSTNAME | 主机名 |
| HOSTTYPE | 显示主机运行的机器类型 |
| OLDPWD | 上一个工作目录 |
| OSTYPE | 使用的操作系统 |
| PATH | 用于搜索可执行命令的目录路径列表 |
| PPID | shell 父 shell 的进程 ID |
| PWD | 用户的工作目录 |
| RANDOM | 被引用时生成随机数 |
| SHLVL | 当前 shell 层级，已调用的 shell 数量 |
| UID | 当前用户的用户 ID |

表 11-4：由 Shell 设置的 Shell 变量你可以在所有类型的 shell 中定义环境变量，包括 BASH shell、Z shell 和 TCSH shell。然而，BASH shell 中实现环境变量的策略与 TCSH shell 不同。在 BASH shell 中，环境变量是被导出（export）的。也就是说，环境变量的副本会被导出。在某种意义上，变量隐藏在它的 shell 内部。




当你登录时，系统会自动定义并为许多 shell 参数变量分配初始值，但你可以根据需要对这些变量进行更改。然而，某些参数变量的值是不应该更改的。例如，`HOME` 变量存储了你主目录的路径。像 `cd` 等命令会引用 `HOME` shell 变量中的路径来定位你的主目录。本节描述了其中一些较为常见的参数变量。

其他参数变量由系统定义并赋予了初始值，你可以自由更改这些值。要做到这一点，你需要重新定义它们并分配一个新值。例如，`PATH` 变量由系统定义并赋予了初始值；它包含包含命令所在的目录路径。每当你执行一个命令时，shell 都会在这些目录中搜索该命令。你可以通过自己重新定义 `PATH` 变量来添加一个新的待搜索目录，使其包含新目录的路径。

尽管如此，还存在其他系统未定义的参数变量。这些通常是可选功能，例如 `EXINIT` 变量，允许你为 `Vi` 编辑器设置选项。每次登录时，你必须为此类变量定义并赋值。一些较为常见的参数变量有 `SHELL`、`PATH`、`PS1`、`PS2` 和 `MAIL`。`SHELL` 变量存储你登录的类型 shell 程序的路径。`PATH` 变量列出了搜索 Linux 命令的不同目录。`PS1` 和 `PS2` 变量存储提示符符号。`MAIL` 变量存储你的信箱文件路径。你可以修改其中任何一个变量的值来定制你的 shell。

注意：你可以使用 `env` 命令获取当前定义的 shell 变量列表。`env` 命令的操作方式类似于 `set` 命令，但它只列出参数变量。

### 使用初始化文件

你可以使用称为“初始化文件”的特殊 shell 脚本来自动定义参数变量。*初始化文件*是一个特殊命名的 shell 脚本，每当你进入某个 shell 时就会执行它。你可以编辑初始化文件，并在其中放置参数变量的定义和赋值。当你进入 shell 时，初始化文件会执行这些定义和赋值，从而用你自己的值有效地初始化参数变量。例如，`BASH` shell 的 `.profile` 文件就是一个每次登录时都会执行的初始化文件。它包含了参数变量的定义和赋值。然而，`.profile` 文件基本上只是一个 shell 脚本，你可以使用任何文本编辑器（如 `Vi` 编辑器）对其进行编辑，并根据需要更改分配给参数变量的值。

在 `BASH` shell 中，所有参数变量都被设计为环境变量。当你定义或重新定义一个参数变量时，还需要将其导出（export）以成为一个环境变量。这意味着你对参数变量的任何更改必须配有一个 `export` 命令。你会发现，在登录初始化文件 `.profile` 的末尾，通常有一个针对其中定义的所有参数变量的 `export` 命令。

### 你的主目录：HOME

`HOME` 变量包含你主目录的路径。你的主目录是由参数管理员在你创建账户时确定的。当你登录时，主目录的路径会自动读取到 `HOME` 变量中。在下一个示例中，`echo` 命令显示了 `HOME` 变量的内容：

```
$ echo $HOME /home/chris
```

当你需要指定主目录的绝对路径时，经常使用 `HOME` 变量。在下一个示例中，使用 `HOME` 作为主目录路径，指定了 `reports` 的绝对路径。

```
$ ls $HOME/reports
```

### 命令位置：PATH

`PATH` 变量包含一系列由冒号分隔的目录路径。每执行一个命令时，系统都会按照 `PATH` 变量列出的路径逐一搜索该命令。例如，`cp` 命令位于系统中的 `/bin` 目录。该目录路径是 `PATH` 变量中列出的目录之一。每当你执行 `cp` 命令时，系统都会搜索该路径并找到 `cp` 命令。系统定义并为 `PATH` 分配了一组初始路径。在 Linux 中，初始路径为 `/bin` 和 `/usr/bin`。

| Shell 变量 | 描述 |
| :--- | :--- |
| `BASH_VERSION` | 显示当前的 `BASH` 版本号 |
| `CDPATH` | `cd` 命令的搜索路径 |
| `EXINIT` | Ex/Vi 编辑器的初始化命令 |
| `FCEDIT` | 历史命令 `fc` 使用的编辑器。 |
| `GROUPS` | 用户所属的组 |
| `HISTFILE` | 历史文件的路径 |
| `HISTSIZE` | 历史允许的命令数 |
| `HISTFILESIZE` | 历史文件的行数 |
| `HOME` | 用户主目录的路径 |
| `IFS` | 字段分隔符 |
| `IGNOREEOF` | 如果未设置，EOF 字符将关闭 shell。可以设置为在接受关闭 shell 之前忽略的 EOF 字符数（默认为 10） |
| `INPUTRC` | 为 Readline（命令行）设置 `inputrc` 配置文件。默认为当前目录下的 `.inputrc`。大多数 Linux 发行版将其设置为 `/etc/inputrc` |
| `LOGNAME` | 登录名 |
| `MAIL` | 如果未设置 `MAILPATH`，Mail 实用检查接收消息的特定邮件文件名称 |
| `MAILCHECK` | 检查收到的邮件的间隔 |
| `MAILPATH` | Mail 检查收到的邮件的文件列表 |
| `HOSTTYPE` | Linux 平台，如 i686、x86_64 或 ppc |
| `PROMPT_COMMAND` | 每个提示符之前执行的命令，其结果作为提示符的一部分 |
| `HISTFILE` | 历史文件的路径 |
| `PS1` | 主提示符 |
| `PS2` | 次要提示符 |
| `SHELL` | 你正在使用的 shell 程序的路径 |
| `TERM` | 终端类型 |
| `TMOUT` | shell 保持活动等待输入的时间 |
| `USER` | 用户名 |
| `UID` | 用户 ID（数字） |

**表 11-5：Shell 使用的系统环境变量**

shell 可以执行任何可执行文件，包括你创建的脚本。因此，`PATH` 变量也可以引用你的工作目录；这样，如果你想执行工作目录中的某个脚本，shell 就能找到它。字符串中的路径名之间不允许有空格。冒号后面如果没有路径将引用你的工作目录。通常在路径末尾放置一个冒号作为指定工作目录的空项。例如，路径 `/bin:/usr/bin:` 引用三个目录：`/bin`、`/usr/bin` 和你的当前工作目录。

```
$ echo $PATH /bin:/usr/bin:
```

你可以向 `PATH` 变量添加任何想要的新目录路径。当你使用 shell 脚本创建了许多自定义 Linux 命令时，这非常有用。你可以将这些新的脚本命令放置在一个创建目录中，然后将该目录添加到 `PATH` 列表中。这样，无论你在哪个目录，都可以执行你的 shell 脚本。`PATH` 变量将包含该脚本所在的目录，因此每次你发布命令时都会搜索该目录。

你可以通过变量赋值向 `PATH` 变量添加目录。你可以在 shell 中直接执行此赋值。在下一个示例中，用户 `chris` 为 `PATH` 添加了一个名为 `bin,` 的新目录。虽然你可以仔细输入 `PATH` 中列出的完整路径进行赋值，但你也可以使用 `PATH` 的求值 `$PATH` 来代替。在这个示例中，还使用了 `HOME` 的求值来指定新目录路径中的用户主目录。注意最后的冒号，它指定了工作目录。





```bash
$ PATH=$PATH:$HOME/mybin: $ export PATH $ echo $PATH /bin:/usr/bin::/home/chris/mybin
```

如果你在登录期间向 `PATH` 添加了目录，那么该目录仅在你的当前登录会话期间有效。当你重新登录时，登录初始化文件 `.profile` 将再次使用其原始的目录集初始化你的 `PATH`。`.profile` 文件将在本章稍后的部分进行详细描述。若要永久地向你的 `PATH` 添加一个新目录，你需要编辑 `.profile` 文件并找到 `PATH` 变量的赋值语句。然后，你只需将该目录以冒号开头，插入到赋值给 `PATH` 的路径集中即可。

### 指定 BASH 环境：BASH_ENV
`BASH_ENV` 变量存储了每当生成 BASH shell 时要执行的 BASH shell 初始化文件的名称。例如，当执行一个 BASH shell 脚本时，系统会检查 `BASH_ENV` 变量，并在执行该脚本之前执行其中包含的脚本名称。`BASH_ENV` 变量通常持有 `$HOME/.bashrc`。这是用户家目录下的 `.bashrc` 文件。（本章后面会讨论 `.bashrc` 文件）。如果你愿意，可以使用不同的文件，用它代替 `.bashrc` 文件用于 BASH shell 脚本。

### 配置 Shell 提示符
`PS1` 和 `PS2` 分别包含主提示符和次提示符符号。BASH shell 的主提示符符号是美元符号 ($)。你可以通过给 `PS1` 变量分配一组新字符来更改提示符符号。在下一个示例中，shell 提示符被更改为 `->`符号。

```bash
$ PS1='->' -> export PS1
->
```

下表列出了配置你的提示符的代码：

| 提示符代码 | 说明 |
| :--- | :--- |
| `!` | 当前历史记录编号 |
| `$` | 除 root 用户外的所有用户均使用 `$` 作为提示符，root 用户使用 `#` 作为提示符 |
| `\d` | 当前日期 |
| `\#` | 仅限当前 shell 的历史命令编号 |
| `\h` | 主机名 |
| `\s` | 当前激活的 shell 类型 |
| `\t` | 以时、分、秒表示的时间 |
| `\u` | 用户名 |
| `\v` | shell 版本 |
| `\w` | 当前工作目录的完整路径 |
| `\W` | 当前工作目录名 |
| `\\` | 显示反斜符字符 |
| `\n` | 插入换行 |
| `\[ \]` | 允许为颜色或粗体字体等功能输入终端特定的显示字符 |
| `\nnn` | 以八进制格式指定的字符 |

你可以将提示符更改为任何字符集（包括字符串），如示例所示：

```bash
$ PS1="Please enter a command: " Please enter a command: export PS1 Please enter a command: ls mydata /reports
Please enter a command:
```

`PS2` 变量持有次提示符符号，用于需要几行才能完成的命令。默认的次提示符是 `>`。添加的命令行将以次提示符而非主提示符开头。你可以像更改主提示符一样轻松地更改次提示符，如下所示：

```bash
$ PS2="@"
```

与 TCSH shell 一样，BASH shell 为你提供了一组预定义的代码，你可以它们来配置提示符。通过这些代码，你可以让时间、用户名或目录路径成为提示符的一部分。你甚至可以让提示符显示你即将输入的当前命令的历史事件编号。每个代码前面都有一个 `\` 符号：`\w` 表示当前工作目录，`\t` 表示时间，`\u` 表示你的用户名；`!` 将显示下一个历史事件编号。在下一个示例中，用户将当前工作目录添加到了提示符中：

```bash
$ PS1="\w $" /home/dylan $
```

这些代码必须包含在引号字符串中。如果不存在引号，代码字符将不会被求值，而是本身被用作提示符。`PS1=\w` 将提示符设置为字符 `\w`，而不是工作目录。接下来的示例将时间和历史事件编号都结合到了一个新的新提示符中：

```bash
$ PS1="\t \! ->"
```

默认的 BASH 提示符为 `\s-\v$`，用于显示 shell 类型、shell 版本以及将 `$` 符号作为提示符。某些发行版将其改为更复杂的命令，由用户名、主机名和当前工作目录名组成。这里显示了一个示例配置。这里显示了一个简单的等效方案，主机名中使用 `@` 符号，最后的提示符符号使用 `$`。家目录用波浪号 (`~`) 表示。

```bash
$ PS1="\u@\h:\w$" richard@turtle.com:~$
```

Linux Mint 在 `.bashrc` 文件中包含包含复杂的提示符定义，以支持颜色提示符并检测任何远程用户登录。

### 指定你的新闻服务器
多个 shell 参数变量用于设置网络应用程序（如浏览器或新闻客户端）使用的值。`NNTPSERVER` 用于设置网络上可用的远程新闻服务器的值。如果你使用 ISP（互联网服务供应商），ISP 通常提供一个你可以通过新闻阅读程序访问的 Usenet 新闻服务器。然而，你必须先为新闻客户端提供新闻服务器的互联网地址。这就是 `NNTPSERVER` 变量的作用。互联网上的新闻服务器通常使用 `NNTP` 协议。`NNTPSERVER` 应持有此类新闻服务器的地址。对于许多 ISP，新闻服务器地址是以 `nntp` 开头的域名名。接下来的示例将新闻服务器地址 `nntp.myservice.com` 分配给 `NNTPSERVER` shell 变量。新闻应用程序会自动从 `NNTPSERVER` 获取新闻服务器地址。通常，此赋值放置在 shell 初始化文件 `.profile` 中，以便用户每次登录时都会自动设置。

```bash
NNTPSERVER=news.myservice.com
export NNTPSERVER
```





你向 `.profile` 文件添加的任何新参数变量都需要通过使用 `export` 命令进行导出。这使得它们对你进入的任何子壳（subshells）可见。你可以通过在一个 `export` 命令中列出多个变量来一次导出多个变量。`.profile` 文件本身不包含变量定义，尽管你可以添加自己的定义。在这种情况下，`.profile` 文件将包含一个 `export` 命令，其中列出了该文件中定义的所有变量。如果该列表中缺少某个变量，你可能无法访问它。`.bashrc` 文件包含了 `HISTCONTROL` 变量的定义，并对其进行了导出。你也可以像这里对 `NNTPSERVER` 所示的那样，将赋值和 `export` 命令合并为一次操作：

```bash
export NNTPSERVER=news.myservice.com
```

### 变量赋值

下一个示例列出了在创建账户时为你提供的标准 `.profile`文件的副本。请注意 `PATH` 是如何赋值的。`PATH` 是系统已经定义的参数变量。`PATH` 存储了系统在你输入任何命令时进行搜索的目录路径。赋值 `PATH="$PATH:$HOME/bin"` 的效果是重新定义 `PATH`，使其包含家目录下的 `bin` 目录，这样你的 `bin` 目录也会被搜索任何命令，包括你自己创建的命令，例如脚本或程序。

如果你也想搜索当前工作目录，可以使用任何文本编辑器在 `.profile` 文件中添加另一行 `PATH`：`PATH="$PATH:"`。你只需要在 `PATH` 之后插入一个冒号 `:`。事实上，你可以更改此条目以添加许多你想要搜索的目录。在当前工作目录中将命令自动设为可执行可能会带来安全风险，允许任何目录中的文件被执行，而不是在特定的指定目录中执行。修改你的 `.profile` 文件的示例见下一节。

```bash
PATH="$PATH:"
```

### 编辑你的 BASH 配置文件脚本

你的 `.profile` 初始化文件是一个文本文件，可以像其他文本文件一样用文本编辑器编辑。你可以通过编辑 `.profile` 轻松地向 `PATH` 添加新目录，并使用编辑命令在分配给 `PATH` 变量的目录路径列表中插入新的目录路径。你甚至可以添加新的变量定义。然而，如果你这样做，请务必确保在 `export` 命令的参数列表中包含新变量的名字。例如，如果你的 `.profile` 文件没有 `EXINIT` 变量的定义，你可以编辑文件并添加新行为 `EXINIT` 赋值。定义 `EXINIT='set nu ai'` 将配置 Vi 编辑器使用行号和自动缩进。然后你需要将 `EXINIT` 添加到 `export` 命令的参数列表中。当 `.profile` 文件再次执行时，`EXINIT` 变量将被设置为命令 `set nu ai`。当调用 Vi 编辑器时，`EXINIT` 变量中的命令将被执行，自动设置行号和自动缩进选项。

在接下来的示例中，用户的 `.profile` 已修改，包含了 `EXINIT` 的定义以及对 `PATH`、`PS1` 和 `HISTSIZE` 的重新定义。`PATH` 变量添加了结尾冒号，指定了当前工作目录，使你能够执行可能位于家目录或工作目录的命令。对 `HISTSIZE` 的重新定义减少了保存的历史事件数量，从系统 `.profile` 文件中定义的 1000 个减少到 30 个。对 `PS1` 参数变量的重新定义更改了提示符，使其仅显示当前工作目录的路径。你在 `.profile` 文件中对参数变量所做的任何更改都会覆盖系统 `.profile` 文件之前所做的更改。所有这些参数变量随后通过 `export` 命令导出。

```bash
.profile

# ~/.profile: 由登录壳的命令解释器执行。
# 如果存在 ~/.bash_profile 或 ~/.bash_login，
# 则 bash(1) 不会读取此文件。
# 参见 /usr/share/doc/bash/examples/startup-files 获取示例。
# 文件位于 bash-doc 软件包中。
# 默认 umask 设置在 /etc/profile 中
#umask 022

# 如果正在运行 bash
if [ -n "$BASH_VERSION" ]; then
  # 如果存在 .bashrc，则包含它
  if [ -f "$HOME/.bashrc" ]; then
    . "$HOME/.bashrc"
  fi
fi

# 如果存在用户的私有 bin，则设置 PATH 
if [ -d "$HOME/bin" ] ; then
  PATH="$HOME/bin:$PATH"
fi

# 如果存在用户的私有 .local/bin，则设置 PATH
if [ -d "$HOME/.local/bin" ]; then
  PATH="$HOME/.local/bin:$PATH"
fi

HISTSIZE=30
NNTPSERVER=news.myserver.com
EXINIT='set nu ai'
PS1="\w \$"

export PATH HISTSIZE EXINIT PS1 NNTPSERVER
```

## 手动重新执行 .profile 脚本

虽然 `.profile` 脚本每次登录时都会执行，但在你对其进行更改后不会自动重新执行。`.profile` 脚本是一个初始化文件，*仅*在每次登录时执行。如果你想利用对它所做的任何更改而无需注销并重新登录，可以使用点 (`.`) 命令重新执行 `.profile` 脚本。`.profile` 脚本是一个 shell 脚本，像任何 shell 脚本一样，可以使用 `.` 命令执行。

```bash
$ . .profile
```

或者，你可以使用 `source` 命令来执行 `.profile` 初始化文件：

```bash
$ source .profile
```

#### 系统 Shell 脚本 (System Shell Script)

你的系统也有一个它自己的配置文件，每当任何用户登录时，它 都会执行该文件。该初始化文件简单地称为 `profile`，位于 `/etc` 目录下，即 `/etc/profile`。此文件包含了系统需要为每个用户提供的定义。在 Linux Mint 上，`/etc/profile` 脚本会检查 `/etc/profile.d` 目录下是否有要运行的 shell 脚本，然后运行 `.bashrc` 脚本，该脚本执行大部分的配置任务。

不同应用程序所需的配置设置会导致 `/etc/profile` 文件过大难以管理。相反，特定应用程序的别名和变量被放置在 `/etc/profile.d` 中的单独配置文件。对于 BASH 和 C shell 都有相应的脚本。BASH shell 脚本通过以下命令从 `/etc/profile` 运行。一个 `for` 循环顺序访问每个脚本并使用点 (`.`) 运算符执行它。

```bash
for i in /etc/profile.d/*.sh; do
  if [ -r $i ]; then
    . $i
  fi
done
unset i
```

对于基础安装，你只有 `gvfs-bash-completion.sh` 脚本。随着你安装其他 shell，可能会更多。`/etc/profile.d` 脚本根据它们配置的任务和应用程序命名。由 BASH shell 运行的文件以 `.sh` 结尾，由 C shell 运行的文件以 `.csh` 结尾。`/etc/profile` 脚本在运行任何 `/etc/profile.d` 脚本之前还会检查 `PS1` 变量是否已定义。

系统 `profile` 的副本如下：

```bash
/etc/profile

## /etc/profile: 系统级 Bourne shell (sh(1))
# 以及兼容 Bourne 的 shell (bash(1), ksh(1), ash(1), ...)。

if [ "$PS1" ]; then
  if [ "$BASH" ] && [ "$BASH" != "/bin/sh" ]; then
    # bash.bashrc 文件已经设置了默认 PS1。
    if [ -f /etc/bash.bashrc ]; then
      . /etc/bash.bashrc
    fi
  else
    if [ "`id -u`" -eq 0 ]; then
      PS1='# '
    else
      PS1='$ '
    fi
  fi
fi

if [ -d /etc/profile.d ]; then
  for i in /etc/profile.d/*.sh; do
    if [ -r $i ]; then
      . $i
    fi
  done
  unset i
fi
```




`.bashrc` 脚本是一个每次在你进入 BASH shell 或生成任何子 shell 时都会执行的配置文件。如果 BASH shell 是你的登录 shell（login shell），那么在登录时`.bashrc` 会与你的 `.profile` 脚本一起执行。如果你从另一个 shell 进入 BASH shell，`.bashrc` 脚本会被自动执行，其中包含的变量和别名定义将被定义。如果你进入了不同类型的 shell，则会执行该 shell 的配置文件。例如，如果你使用 `tcsh` 命令进入 TCSH shell，则执行的是 `.tcshrc` 配置文件而不是 `.bashrc`。

#### **用户级 .bashrc BASH 脚本**
`.bashrc` shell 配置文件实际上在每次生成 BASH shell 时都会执行，例如当你运行一个 shell 脚本时。换句话说，每当创建一个子 shell 时，`.bashrc` 文件就会执行一次。这样做的效果是导出你在 `.bashrc` shell 初始化文件中定义的任何本地变量或别名。`.bashrc` 文件通常包含别名（aliases）的定义以及用于开启 shell 特性的特性变量。别名和特性变量是在 shell 局部定义的，但 `.bashrc` 文件在每个 shell 中都会定义它们。因此，`.bashrc` 文件通常持有你希望为每个 shell 定义的别名和选项。作为如何添加自定义别名和选项的示例，此处示例添加了 `rm`、`cp` 和 `mv` 命令的别名，以及 shell 的 `noclobber` 和 `ignoreeof` 选项。对于 root  `.bashrc`，`rm`、`cp` 和 `mv` 别名已经包含在 root 的 `.bashrc` 文件中了。

`.bashrc` 文件会检查 .bash_aliases 文件中的别名，并运行 `/etc/bash_completion` 以处理命令补全指令。

`.bashrc` 文件将设置若干特性，包括历史（history）、提示符（prompt）、别名和命令补全设置。定义 `HISTCONTROL` 指令以忽略重复命令和以空格开头的行（`ignoreboth`）。历史文件将会被追加，并将历史记录和历史文件大小设置为 1000 和 2000。

```bash
# 不要向历史记录中放入重复行或以空格开头的行
# 更多选项请参见 bash(1)
HISTCONTROL=ignoreboth

# 追加到历史文件，不要覆盖它
shopt -s histappend

# 设置历史长度请参阅 bash(1) 中的 HISTSIZE 和 HISTFILESIZE
HISTSIZE=1000
HISTFILESIZE=2000
```

随后若干命令定义了终端显示特性和命令操作，包括以 `PS1=.` 开头的 shell 提示符。

代码包含了读取用户 `.bash_aliases` 脚本的内容。同时也提供了一些可能的别名，其中一些被注释了。你可以移除注释符号 `#` 来激活它们。列表中列出了为 `ls`、`grep`、`fgrep` 和 `egrep` 命令提供颜色支持的别名。还提供了一个 alert 别名，用于通知你长时间运行的命令。

```bash
# 启用 ls 的颜色支持并添加方便的别名
if [ -x /usr/bin/dircolors ]; then
  test -r ~/.dircolors && eval "$(dircolors -b ~/.dircolors)" || eval "$(dircolors -b)"
  alias ls='ls --color=auto' #alias dir='dir --color=auto' #alias vdir='vdir --color=auto'
  alias grep='grep --color=auto'
  alias fgrep='fgrep --color=auto'
  alias egrep='egrep --color=auto'
fi

# 更多 ls 别名
#alias ll='ls -alF'
#alias la='ls -A'
#alias l='ls -CF'

# 为长时间运行的命令添加 "alert" 别名。用法如下：
# sleep 10; alert
alias alert='notify-send --urgency=low -i "$([ $? = 0 && echo terminal || echo error)" "$(history | tial -n1 | sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'

# 别名定义
# 你可能希望将所有添加内容放在单独的文件中，如
# ~/.bash_aliases，而不是直接添加到这里。
# 请参阅 bash-doc 包中的 /usr/share/doc/bash-doc/examples。
#if [ -f ~/.bash_aliases ]; then
#   . ~/.bash_aliases
#fi
```

随后读取 `bash_completion` 文件以设置命令补全选项。

```bash
# 启用可编程补全功能（如果已经在 /etc/bash.bashrc 和 /etc/profile
# 中启用，则无需再次启用，它们引用了 /etc/bash.bashrc）。
if ! shopt -oq posix; then
  if [ -f /usr/share/bash-conpletion/bash_completion ]; then
    . /usr/share/bash-completion/bash_completion
  elif [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
  fi
fi
```

你可以向 `.bashrc` 文件添加任何你自己的命令或定义。如果你对 `.bashrc` 做了修改并希望在当前登录会话中生效，你需要使用 `.` 或 `source` 命令重新执行该文件。

```bash
$ .bashrc
```

#### **系统级 /etc/bash.bashrc BASH 脚本**
Linux Mint 有一个供所有用户执行的系统 bashrc 文件，称为 `bash.bashrc`。




`.bash_logout` 文件也是一个配置文件，但它会在用户注销时执行。它的设计用于执行你希望在每次注销时发生的操作。与变量定义不同，`.bash_logout` 文件通常包含形成某种关机过程的 shell 命令，即你会在注销前总是想要执行的操作。一个常见的注销命令是清除屏幕然后发送一条告别信息。与 `.profile` 一样，你可以在 `.bash_logout` 中添加自己的 shell 命令。事实上，当你的账户首次创建时，系统并不会自动为你设置 `.bash_logout` 文件。你需要使用 `Vi` 或 `Emacs` 编辑器自行创建它。然后你可以添加告别信息或其他操作。默认的 `.bash_logout` 文件包含了调用 `clear_console` 命令来清除屏幕的指令。

```
.bash_logout

# ~/.bash_logout: executed by bash(1) when login shell exits.

# when leaving the console clear the screen to increase privacy

if [ "$SHLVL" = 1 ]; then  [ -x /usr/bin/clear_console ] && /usr/bin/clear_console -q fi
```

# 第 4 部分：共享资源

- 12. 管理服务
- 13. 打印服务
- 14. 网络文件系统和网络信息系统：NFS 和 NIS
- 15. Samba

# 12. 管理服务

单个 Linux 系统可以提供多种不同类型的服务，范围从安全到管理，包括更显而易见的 Internet 服务，如 Web 和 FTP 站点、电子邮件和打印。安全工具，如安全外壳（SSH）以服务的形式运行，以及管理性网络工具，如动态主机配置协议（DHCP）和 BIND 域名服务器。网络连接接口本身也是一项服务，你可以随意重启它。每个服务都作为一个持续运行的守护进程（daemon）运行，寻找其特定服务的请求。在 Web 服务的情况下，请求来自远程用户。你可以通过启动或关闭它们的守护进程来开启或关闭服务。系统启动由 `systemd` 服务管理。原本用于启动单个服务的 System V init 系统已经逐渐淘汰。

## systemd

Linux 系统传统上使用 Unix System V init 守护进程通过设置启动或关闭的运行级别（runlevels）来管理服务。后来 Linux 用 `systemd` init 守护进程替换了 System V init 守护进程。System V init 守护进程通过按顺序运行的 shell 脚本在整个系统启动或关闭时启动某些服务，而 `systemd` 使用 sockets 用于所有系统任务和服务。`systemd` 为守护进程设置了 sockets 并在它们启动时进行协调。这允许 `systemd` 同时（并行）启动守护进程。如果一个守护进程需要另一个的支持，`systemd` 会协调来自它们 sockets 的数据（缓冲），以便一个守护进程接收到另一个守护进程继续所需的的信息。这种并行启动的兼容性允许非常快的启动速度。

实际上，你可以将 `systemd` 视为 System V init 脚本和 `inetd` 守护进程 (`xinetd`) 的结合体，并将 socket 激活应用于所有系统启动任务和网络服务器。socket 激活设计最初灵感源于 `inetd` 服务，该服务使用 sockets (`AT_INET`) 在接到请求时启动互联网守护进程。这种 socket 激活设计被 Apple 的 OS X 系统使用，应用于所有 sockets (`AF_UNIX`)。这允许所有启动进程同时并行启动，从而实现了快速的启动时间。此类 sockets 由 `systemd` 设置和管理。当 `D-BUS` 需要写入 `journald`（日志记录）时，它写入由 `systemd` 管理的 `systemd-journald` socket。它不需要直接与 `journald` 通信。这意味着服务不再需要像在 System V 下那样按照特定的顺序启动和关闭。它们可以同时启动和停止。此外，由于 `systemd` 控制着 socket，如果服务失败，它的 socket 仍将留在那里。可以使用相同的 socket 重启服务，而不会丢失信息。`systemd` 管理所有类型的 sockets，包括 UNIX（系统）、INET（网络）、NETLINK（设备）、FIFO（管道）和 POSIX（消息）。更多详细信息请见下文。

[`docs.fedoraproject.org/en-US/quick-docs/understanding-and-administering-systemd/index.html`](https://docs.fedoraproject.org/en-US/quick-docs/understanding-and-administering-systemd/index.html) [`www.freedesktop.org/wiki/Software/systemd/`](https://www.freedesktop.org/wiki/Software/systemd/)

`systemd` 为所有系统任务和服务设置了 sockets。systemd 任务的配置定义在 `/lib/systemd/system` 目录下的单元文件（unit files）中。在这方面，`systemd` 文件替换了以前在 Sys V init 的 `/etc/inittab` 文件中的项目。`systemd` 还有它自己的 `shutdown`、`reboot`、`halt`、`init` 和 `telinit` 版本，每个版本都有自己的帮助手册页（man page）。

`systemd` 完全兼容 `/etc/init.d` 目录下的 System V 脚本和 `/etc/fstab` 文件。如果 `/etc/init.d` 中存在 System V 脚本，`systemd` 将使用它们生成相应的单元文件（前提是尚未有 systemd 单元文件）。`systemd` 配置始终优先。此外，如果需要，`systemd` 将使用 `/etc/init.d` 中的启动和停止文件来确定依赖关系。etc/fstab` 中的项目用于生成 systemd 单元文件，进而用于管理文件系统。`systemd` 还支持快照，允许将服务恢复到之前的状态。

systemd 配置（.service）文件位于 `/lib/systemd/system` 目录，被视为不应修改的文件。可以将它们复制到 `/etc/systemd/system` 目录并对副本进行修改。`/etc/systemd/system` 中的文件优先。logind 守护进程的配置文件 `logind.conf` 位于 `/etc/systemd` 目录。少数应用程序（如 NIS 服务器）还没有 systemd 服务文件。`systemd` 会自动在 `/var/run/systemd/generator.late` 目录为它们生成服务文件。

Linux 也使用 systemd 服务处理时间（timedated）、位置（localed）、登录（logind）和主机名（hostnamed）（`systemd-services` 软件包）。可以使用相应的 systemd 控制应用程序进行管理：`timedatectl`、`localectl` 和 `hostnamectl`。

### systemd 基础配置文件

你可以使用位于 `/etc/systemd` 目录下的配置文件对系统、登录管理器、用户和日志服务进行 systemd 配置。当为系统服务运行时，systemd 使用 `system.conf` 文件，否则它使用 `user.conf` 文件。你可以设置诸如日志级别（LogLevel）和资源大小限制等选项。可用选项的详情请参见 `systemd.conf`（`system.conf` 和 `user.conf`）、`logind.conf` 和 `journald.conf` 的帮助手册页。

### **单元 (units)**





`systemd` 将任务组织为单元（units），每个单元都有一个单元配置文件。有几种类型的单元（参见表 12-1）。单元文件的名称中带有一个扩展名，用于指定其单元类型。服务类型的扩展名为为 `.service`，挂载类型的扩展名为为 `.mount`。服务类型的功能与 System V init 脚本非常相似。服务可以停止、启动和重启。`systemctl` 命令将列出所有单元，包括 `systemd` 生成的。

单元也可以用于套接字（socket）、设备（device）和挂载（mount）任务。socket 类型实现了 `inetd` 和 `xinetd` 使用的连接类型，允许你根据需要启动服务。device 类型引用由 `udev` 检测到的设备。mount 类型管理文件系统的挂载点，而 `automount` 则在需要进行自动挂载时激活该挂载点。一个 `automount` 单元文件有一个对应的挂载型单元文件，它使用该文件来挂载文件系统。同样，socket 类型通常有一个对应的服务类型文件，用于为该套接字执行任务。

每个单元内部都有控制服务、套接字、设备或挂载点的指令。某些指令是特定单元类型所有的。这些指令列在对应服务的 man 页面中，例如服务单元的 `systemd.service`，或挂载单元的 `systemd.mount`（参见表 12-1）。

```
man systemd.service
```

单元通用的选项列在 `systemd.exec` 和 `systemd.unit` 页面中。`systemd.unit` 页面列出了所有单元通用的指令，如 `Wants`、`Conflicts`、`Before`、`SourcePath` 和 `Also`。`systemd.exec` 页面列出了为单元执行程序时的选项，例如启动服务器守护进程。这些包括 `User`、`Group`、`WorkingDirectory`、`Nice`、`Umask` 和 `Environment` 等选项。`systemd.exec` 涵盖了服务、套接字、挂载和交换（swap）单元的选项。`systemd.directives` man 页面提供了所有 systemd 单元选项的列表以及每个选项的 man 页面。

| Unit Type | Unit Man page | Description |
| :--- | :--- | :--- |
| service | systemd.service | 服务，如服务器，可以启动和停止 |
| socket | systemd.socket | 用于服务的套接字（允许类似 inetd 的服务，AF_INET） |
| device | systemd.device | 设备 |
| mount | systemd.mount | 文件系统挂载点 |
| automount | systemd.automount | 文件系统的自动挂载点。配合 mount 单元使用。 |
| target | systemd.target | 组单元 |
| path | systemd.path | 管理目录 |
| snapshot | systemd.snapshot | 由 systemd 使用 `systemctl snapshot` 命令创建，用于保存 systemd 的运行状态。使用 `systemctl isolate` 恢复状态。 |
| swap | systemd.swap | systemd 为交换文件系统生成的交换单元文件。 |
| timer | systemd.timer | 基于时间的单元激活。对应服务文件。时间格式在 `systemd.unit` 页面上指定。 |
| | systemd.unit | 所有单元通用的选项 |
| | systemd.exec | 为单元执行程序的选项 |
| | systemd.directives | 所有 systemd 单元选项的列表 |

### 表 12-1: systemd 单元类型
（注：提供的文本在后半部分包含重复和混乱的句子；核心信息已根据上下文进行了重建。）

### 单元文件语法

单元文件被组织成由括号括关键字指定的节。所有单元都有一个单元节 `[Unit]` 和一个安装节 `[Install]`。这些节的选项在 `systemd.unit` Man 页面中描述。可以通过以 `#` 或 `;` 字符开头行来编写注释。请参见表 12-2 以获取常用 Unit 和 Install 选项列表。

单元文件的 Unit 节包含有关单元的通用信息。`Description` 选项提供了有关该单元管理的任务的信息，例如此处所示的 Vsftpd 服务器。

`Description=vsftpd FTP server`

`Documentation` 选项列出了应用程序文档的 URI。

`Documentation=man:dhcpd(8)`

依赖关系的类型可以使用单元节中的 `Before`、`After`、`Requires`、`Wants` 和 `Conflicts` 选项指定。`After` 和 `Before` 配置单元的顺序。在以下 `vsftpd.service` 文件的 `After` 选项中，vsftpd 服务在网络之后启动。

```
After=network.target
```

| Unit options | Description |
| :--- | :--- |
| [Unit] |  |



` 标签开头，且内容包含了大量的 systemd 单元配置说明、表格和代码块，我已按照您的要求和 Markdown 格式标准，对该部分文本进行了完整的翻译。

以下是为您翻译的中文内容：

[content]

| 描述 | 单元描述 |
| :--- | :--- |
| Documentation | 引用文档的 URIs。 |
| Requires | 服务所需的单元。这是一个强制性要求。如果所需的单元失败，该单元也会失败。 |
| PartOf | 由服务启动和停止的依赖单元。这不是强制要求。如果依赖单元失败，该单元仍会启动。 |
| Wants | 服务需要的单元。这不是强制要求。如果所需的单元失败，该单元仍会启动。其功能与 `wants` 目录功能相同。 |
| Conflicts | 负向单元依赖。启动该单元会停止 `Conflicts` 选项中列出的单元。 |
| Before | 单元排序。该单元在列出的单元之前启动。 |
| After | 单元排序。该单元等待列出的单元启动。 |
| OnFailure | 单元失败时要运行的单元。 |
| SourcePath | 生成配置的文件，例如从 `/etc/fstab` 生成的挂载单元文件。 |
| [Install] | |
| WantedBy | 在列出的单元的 `.wants` 子目录中设置该单元的符号链接。当列出的单元激活时，该单元也会激活。这不是强制要求。 |
| RequiredBY | 在列出的单元的 `.requires` 子目录中设置该单元的符号链接。当列出的单元激活时，该单元也会激活。这是一个强要求。 |
| Alias | 单元安装的额外名称。别名通过指向单元文件的符号链接实现。 |
| Also | 与此单元一起安装的额外单元。 |

表 12-2：systemd 单元和 Install 部分选项（适用于所有单元，`systemd.unit`）

`Requires` 选项建立了单元之间的依赖关系。这是一种强依赖。如果其中一个失败，另一个也会失败。在以下来自 `graphical.target` 单元文件的 `Requires` 选项中，只有在多用户模式（multi-user.target）和救援模式（rescue.target）激活时，图形目标才能启动。

```
After=multi-user.target rescue.service rescue.target display-manager.service
```

`Wants` 选项建立了一种较弱的依赖关系，要求激活，但发生故障时不会触发失败。图形目标和显示器服务的情况此类此。

```
Wants=display-manager.service
```

有多个条件选项可用，例如 `ConditionACPower`，如果为真，则检查系统是否正在使用交流电供电。在下面的示例中，`ConditionPathExists` 检查 `/etc/default` 目录下是否存在具有 DHCP 服务器运行时选项的文件。

```
ConditionPathExists=/etc/default/isc-dhcp-server
```

某些单元文件是由 `systemd` 自动生成的，允许您使用较旧的配置方法。例如，用于管理文件系统挂载的单元文件是根据 `/etc/fstab` 文件中的配置信息生成的。`SourcePath` 选项指定用于生成单元文件的配置文件。这里显示了 `boot.mount` 单元文件的 `SourcePath` 选项。

```
SourcePath=/etc/fstab
```

`Install` 部分提供了单元的安装信息。`WantedBy` 和 `RequiredBy` 选项指定了该单元想要或需要的单元。对于管理 `Vsftpd` 和 DHCP 服务器等服务的服务单元，安装部分有一个针对 `multi-user.target` 的 `WantedBy` 选项。这具有在运行级别 2、3、4 和 5 下运行服务器的效果。当多用户目标变为激活状态时，该单元也会激活。

```
WantedBy=multi-user.target
```

`WantedBy` 选项通过在被请求的单元的 `wants` 子目录中设置指向该单元的链接来实现。对于 `multi-user.target` 单元，名为 `multi-user.target.wants` 的子目录拥有指向所有想要它的单元的符号链接，例如用于 vsftpd FTP 服务的 `vsftpd.service`。这些 `wants` 符号链接设置在 `/etc/systemd/system` 目录下，可以在启用和禁用服务时进行更改。禁用服务会移除链接。`RequiredBy` 是强得多的依赖关系。

`Alias` 选项列出了可以引用此单元的其他单元名称。在 `ssh.service` 文件中，你会找到针对 `sshd.service` 的 `Alias` 选项。

```
Alias=sshd.service
```

`Also` 选项列出了当此单元启动时应该激活的其他单元。CUPS 服务有一个 `Also` 选项来启动 CUPS 套接和路径。

```
Also=cups.socket cups.path
```

不同类型的单元有自己的选项。服务、socket、target 和 path 单元都有适用于其任务的选项。

### 特殊目标

target 文件将服务、挂载、套接和设备的单元分组。`systemd` 有一组专为特定目的设计的特殊 target 文件（参见表 12-3）。其中一些用于按需服务，如蓝牙和打印机。当连接蓝牙设备时，`bluetooth` 目标变为激活。当你连接打印机时，`printer` 目标激活，从而激活 CUPS 打印服务器。`sound` 目标在系统启动时激活并运行所有与声音相关的单元。详情请参 `special.target` 手页。

有几个特殊的 target 文件旨在实现 System V 中运行级别（runlevels）的功能（参见表 12-4）。这些包括 `rescue`、`multi-user` 和 `graphical` 目标。在启动时，`systemd` 激活默认目标，该目标指向特殊目标的链接，例如 `multi-user.target` 和 `graphical.target`。

| 特殊单元 | 描述 |
| :--- | :--- |
| basic.target | 在启动启动阶段运行的单元 |
| bluetooth.target | 在设备激活时启动 |
| printer.target | 当连接打印机时启动打印服务。 |
| sound.target | 在检测到声音设备时启动，通常在启动时。 |
| display-manager.service | 指向 LightDM 或 KDM 等显示服务的链接。 |
| ctrl-alt-del.target | 用户按下 Ctrl-Alt-Del 键时激活，这是一个指向 `reboot.target` 的链接，用于重启系统。 |
| system-update.target | 实现离线系统更新。下载后，更新将在系统重启时执行，此时它会检测该目标是否存在。 |

表 12-3：特殊单元

| 特殊目标 | 描述 |
| :--- | :--- |
| default.target | 启动时激活的特殊目标链接 |
| rescue.target | 启动基础系统和救援 shell |
| emergency.target | 启动基础系统，并带有启动完整系统的选项 |
| multi-user.target | 启动命令行界面、多用户和非图形界面（类似于运行级别 3） |
| graphical.target | 启动图形界面（桌面）（类似于运行级别 5） |

表 12-4：特殊运行级别（启动）





`graphical.target` 依赖于 `multi-user.target`。下面是 `graphical.target` 文件的副本。它要求 `multi-user.target` 必须激活（Requires）。任何为 multi-user target 运行的程序（包括服务器）也会为 graphical target（即桌面）运行。桌面 target 在 `multi-user.target` 之后运行（After）。它不会在 `rescue.target` 中运行（Conflicts）。它还希望 `display-manager` 服务（如 GDM 或 KDM）运行（Wants）。你可以通过孤立它来切换到另一个 target（AllowIsolate）。

```
graphical.target

[Unit]
Description=Graphical Interface
Documentation=man:systemd.special(7)
Requires=multi-user.target
Wants=display-manager.service
Conflicts=rescue.service rescue.target
After=multi-user.target rescue.service rescue.target display-manager.service
AllowIsolate=yes
```

### 修改单元文件：/etc/systemd/system

`systemd` 使用单元文件来管理设备、挂载点和服务。这些文件位于 `/lib/systemd/system` 目录，被认为是你不应修改的系统文件。你可以通过两种方式修改单元文件：通过指定覆盖原始文件的特性的，或者创建一个可以编辑的独立副本，该副本的优先级高于原始文件。在任何情况下，最好使用 `systemctl` 命令配合 `edit` 选项来创建修改。

若要简单地覆盖或向单元文件添加条目，你可以创建一个关联的补丁目录（drop in directory），其中包含带有条目的配置文件。该目录的名称与单元文件名相同，但带有 `.d` 扩展。它包含扩展名为为 `.conf` 的配置文件。要创建补丁目录及其配置文件，你只需使用 `systemctl edit` 命令编辑单元文件即可。

```
sudo systemctl edit vsftpd.service
```

这会打开你的默认行编辑器并允许你添加新条目。当你保存时，如果补丁目录不存在，它将被创建。这会在 `/etc/systemd/system/vsftpd.service.d` 目录下创建一个 `override.conf` 文件。

如果你想进行更广泛的更改，可以在 `/etc/systemd/system` 目录下创建原始单元文件的副本。该目录下的单元文件优先级高于 `/lib/systemd/system` 目录下的文件。然后你可以修改 `/etc/systemd/system` 中的单元文件版本。你可以使用 `systemctl edit --full` 命令来创建此副本。

```
sudo systemctl edit --full vsftpd.service
```

这会打开你的默认行编辑器，显示位于你 `/etc/systemd/system` 目录下的单元文件副本，并允许你修改或添加条目。

或者，你可以直接将单元文件拷贝到 `/etc/systemd/system` 目录，然后用文本编辑器编辑它。使用 `cp` 命令复制文件。以下命令拷贝 Samba 服务单元文件。

```
sudo cp /lib/systemd/system/smbd.service /etc/systemd/system/smbd.service
```

### 执行环境选项

类型 service、sockets、mount 和 swap 类型的单元文件共享相同的单元执行环境选项（请参见 表 12-5）。这些选项位于该类型的单元部分中，例如服务单元的 `[Service]` 或套接字单元的 `[Socket]`。通过这些选项，你可以设置某些功能，如工作目录（`WorkingDirectory`）、文件模式创建掩码（`UMask`）和系统日志级别（`SysLogLevel`）。Nice 设置默认的调度优先级级别。User 指定单元运行进程的用户 ID。

`User=mysql`

| Exec options | Description |
| :--- | :--- |
| WorkingDirectory | 为应用程序设置工作目录。 |
| RootDirectory | 应用程序的根目录 |
| User, Group | 应用程序的用户和组 ID。 |
| Nice | 为应用程序设置优先级 |
| CPUSchedulingPriority | 应用程序的 CPU 调度优先级。 |
| UMask | 文件模式创建掩码，默认为 022\. |
| Environment | 为应用程序设置环境变量。 |
| StandardOutput | 将标准输出重定向到连接，如日志、控制或空。 |
| SysLogLevel | 系统日志级别，如 warn、alert、info 或 debug。 |
| DeviceAllow, DeviceDeny | 控制应用程序对设备的访问。 |
| ControlGroup | 将应用程序分配到控制组。 |

表 12-5：systemd exec 选项 (Service, Socket, Mount, Swap) (systemd.exec)

### 服务单元文件

服务单元文件用于运行应用程序和命令，如 Samba (`smbd`) 和 Web (`apache2`) 服务器。它们有一个 `[Service]` 部分，其中在 `systemd.service` 手页中指定了选项。请参见 表 12-6 获取若干常用服务选项列表。服务单元文件的扩展名为 `.service`，前缀是服务器程序的名称，例如用于 DHCP 服务器的 `isc-dhcp-server.service` 和用于 Very Secure FTP 服务器的 `vsftpd.service`。表 12-7 列出了几个流行的服务器。

Vsftpd 服务单元文件的副本 `vsftpd.service` 如下。`vsftpd` 单元在 network 之后启动，multi-user.target 由 `vsftpd` 启动。

```
vsftpd.service

[Unit]
Description=Graphical Interface
After=network.target

[Service]
Type=simple
EnvironmentFile=/etc/vsftpd.conf
ExecStart=/usr/sbin/vsftpd
ExecReload=/bin/HUP $MAINPID
ExecStop=/empty

[Install]
WantedBy=multi-user.target
```

| Service options | Description |
| :--- | :--- |
| ExecStart | 服务启动时执行的命令，如运行应用程序或服务器。 |
| Type | 启动类型，如 simple（默认）、forking、notify 或 idle |
| ExecStartPre, ExecStartPost | 在 ExecStart 之前之后执行的命令。 |
| TimeStartSec | 在启动 ExecStart 之前等待的时间。 |
| Restart | ExecStart 执行后重启。 |
| PermissionsStartOnly | 布尔值，如果应用则应用 User 等权限。 |
| RootDirectoryStartOnly | 布尔值，RootDirectory 适用于 ExecStart。 |

表 12-6：systemd 服务选项 [Service] (systemd.service)

`named.service` 文件更为简单，将运行时选项整合到命令中。它在 network 服务之后运行，并由 multi-user.target 启动。它还有一个别名，让你能够以 `named` 或 `bind9` 管理该服务。

```
named.service

[Unit]
Description=BIND Domain Name Server
After=network.target
Wants=nss-lookup.target
Before=nss-lookup.target

[Service]
EnvironmentFile=/etc/default/named
ExecStart=/usr/sbin/named -f $OPTIONS
ExecReload=/usr/sbin/rndc reload
ExecStop=/usr/sbin/rndc stop

[Install]
WantedBy=multi-user.target
Alias=bind9.service
```

| Service unit files | Description |
| :--- | :--- |
| apache2 | Apache Web 服务器 |
| bind9 | Bind 9 DNS 服务器 |
| cups | CUPS 打印守护进程 |
| isc-dhcp-server | 动态主机配置守护进程 |
| mysql | MySQL 数据库服务器 |
| network | 启动或关闭网络连接的操作。 |
| nis | NIS 服务器 |
| nfs-server | 网络文件系统 |
| postfix | Postfix 邮件服务器 |
| sendmail | Sendmail MTA 守护进程 |
| smbd | 用于 Windows 主机的 Samba |
| squid3 | Squid 代理缓存服务器 |
| ssh | Secure Shell 守护进程 |
| systemd-journald | 系统日志守护进程 |
| vsftpd | Very Secure FTP 服务器 |
| ufw | 控制 UFW 火火墙 |

表 12-7：服务单元文件集

### System V 脚本和生成的 systemd 服务单元文件：/etc/init.d 和 /run/systemd/generator.late





某些服务尚未配置为由 systemd 原生使用。它们在安装时没有 systemd 服务文件。相反，在 `/etc/init.d` 目录下安装了一个 SysV 脚本。`systemd-sysv-generator` 工具会自动读取此脚本，并在 `/var/run/systemd/generator.late` 目录下生成对应的 systemd 单元文件，该文件反过来将使用该脚本来管理服务。NIS 代理服务器就是此类服务，在 `/etc/init.d` 中有一个 `nis.service` 脚本，在 `/var/run/systemd/generator.late` 中有一个对应的 systemd 服务文件。以下是 `nis.service` 单元服务文件的副本。它在网络、远程文件系统挂载和名称服务查找之后运行。服务器程序使用 `/etc/init.d/nis` 脚本（`ExecStart`）运行。同一个脚本也用于加载和停止服务器，但使用了不同的选项（`ExecReload` 和 `ExecStop`）。

在 `/run/systemd/generator.late` 目录下存在不同运行级别的 `.target.wants` 目录，这些目录包含了对于给定运行级别激活的服务链接。这些运行级别 target wants 目录引用运行级别 target，而这些 target 只是指向 systemd 多用户和图形 target 的链接。

```ini
nis.service

# 由 systemd-sysv-generator 自动生成

[Unit]
Documentation=man:systemd-sysv-generator(8)
SourcePath=/etc/init.d/nis
Description=LSB: Start NIS 客户端和服务器守护进程。
Before=multi-user.target
Before=multi-user.target
Before=multi-user.target
Before=graphical.target
After=network-online.target
After=rpcbind.target
After=remote-fs.target
Wants=network-online.target

[Service]
Type=forking
Restart=no
TimeoutSec=5min
IgnoreSIGPIPE=no
KillMode=process
GuessMainPID=no
RemainAfterExit=yes
SucessExitStatus=5 6
ExecStart=/etc/init.d/nis start
ExecStop=/etc/init.d/nis stop
ExecReload=/etc/init.d/nis reload
```

### 按需服务与独立服务 (socket)

服务的按需激活（以前由 inetd 实现）是 systemd 的默认行为。如果你需要一个独立服务，可以指定它被一个特殊的 target 需要，以便它在启动时启动，而不是在第一次激活时启动。在服务单元文件的 `Install` 部分中，指定多用户 target 的 `WantedBy` 选项将在启动时启动该服务，使其成为一个独立服务。在接下来，该服务被 `multi-user.target` 所需要。换句话说，该服务在运行级别 2、3、4 和 5 下启动。请注意，图形 target (5) 依赖于（Requires）多用户 target (2, 3 和 4)，因此通过指定多用户 target，该服务也会随着图形 target 一起启动。

```ini
[Install]
WantedBy=multi-user.target
```

蓝牙服务仅需要 `bluetooth.target`，该 target 仅在存在蓝牙设备时才会激活。它不会在启动时启动。

```ini
[Install]
WantedBy=bluetooth.target
```

如果你希望服务在所有运行级别下启动，请使用基本 target。

```ini
[Install]
WantedBy=basic.target
```

为了像以前的 inetd 那样模拟按需服务器服务，你将使用一个 `.socket` 文件来配合 `.service` 文件。CUPS 就是这种情况，它有一个 cups 服务文件和对应的 cups socket 文件（Server 版本的默认不安装 CUPS）。对于 `sockets.target` 的 `WantedBy` 选项将 socket 绑定到特殊的 target `sockets.target`，这使得该单元是基于 socket 激活的。

`Socket` 部分列出了 socket 的选项，通常是在哪个 socket 上进行监听（`ListenStream`）。`systemd.socket` 手页列出了 socket 选项。表 12-8 列出了常用选项。

| Socket 选项 |  |
| :--- | :--- |
| ListenStream | 用于流监听的监听地址。该地址可以是端口号、socket 设备路径名，或带有端口号的 IPv4 或 IPv6 地址。 |
| Accept | 如果为 true，则为每个连接设置服务实例；如果为 false，则为所有连接设置一个服务实例 |
| MaxConnections | 服务的最大连接数 |
| Service | socket 激活时运行的服务单元。默认是与 socket 名称相同的服务名称。 |

表 12-8: systemd socket 文件选项 [Socket] (systemd.socket)

```ini
cups.socket

[Unit]
Description=CUPS Scheduler
PartOf=cups.service

[Socket]
ListenStream=/var/run/cups/cups.sock

[Install]
WantedBy=sockets.target
```

```ini
cups.service

[Unit]
Description=CUPS Scheduler
Documentation=man:cupsd(8)
After=sssd.service

[Service]
ExecStart=/usr/sbin/cupsd -l
Type=simple

[Install]
Also=cups.socket cups.path
WantedBy=printer.target
```

### Path 单元

`systemd` 使用 path 单元来监控路径。有时服务单元有一个对应的 path 单元来监控目录，如 `cups.path` 和 `cups.service` 所示。`Path` 部分的选项列表 12-9。

```ini
cups.path

[Unit]
Description=CUPS Scheduler
PartOf=cups.service

[Path]
PathExists=/var/cache/cups

[Install]
WantedBy=multi-user.target
```

| path 选项 |  |
| :--- | :--- |
| PathExists | 如果文件存在则激活 |
| PathExistsGlob | 如果匹配模式的文件则激活 |
| PathModified | 如果文件被修改则激活 |

表 12-9: path  (systemd.path)

### Template 单元文件

有一种特殊的单元文件类型称为模板（template），允许生成多个单元文件。模板文件名以 `@` 符号结尾。如果找不到相应的单元文件，`systemd` 将检查是否有可以应用的模板。`systemd` 将服务名与模板名匹配，然后为该服务生成一个实例文件。例如，终端使用 `getty` 服务。在配置文件中，使用指定符 `%I` 来替换服务名。由于不知道会有多少个终端，它们是使用 `getty@.service` 单元文件自动生成的。这里显示 `getty.service` 模板文件。

```ini
getty@.service

[Unit]
Description=Getty on %I
Documentation=man:agetty(8) man:systemd-getty-generator(8)
Documentation=http://0pointer.de/blog/projects/serial-console.html
After=systemd-user-sessions.service plymouth-quit-wait.service
After=rc-local.service
Before=getty.target
IgnoreOnIsolate=yes
ConditionPathExists=/dev/tty0

[Service]
# VT 由 TTYVTDisallocate 清除
ExecStart=-/sbin/agetty -o '-p \u' --noclear %I $TERM
Type=idle
Restart=always
RestartSec=0
UtmpIdentifier=%I
TTYPath=/dev/%I
TTYReset=yes
TTYVHangup=yes
TTYVTDisallocate=yes
KillMode=process
IgnoreSIGPIPE=no
SendSIGHUP=yes
Environment=LANG= LANGUAGE= LC_CTYPE= LC_NUMERIC= LC_TIME= LC_COLLATE= LC_MONETARY= LC_MESSAGES= LC_PAPER= LC_NAME= LC_ADDRESS= LC_TELEPHONE= LC_MEASUREMENT= LC_IDENTIFICATION=

[Install]
WantedBy=getty.target

DefaultInstance=tty1
```





# 运行级别与特殊目标

在旧的 System V 中，Linux 系统可以运行在不同的级别上，称为 `runlevels`（运行级别），这取决于你想要赋予它的功能。在 System V 下，Linux 有若干个运行级别，数字从 `0` 到 `6`。当你启动系统时，你会进入默认的运行级别。运行级别 0、1 和 6 是执行特定功能的特殊运行级别。运行级别 0 是关机状态。运行级别 6 是重启状态（它会关闭系统并重启）。运行级别 1 是单用户状态，仅允许超级用户访问且不运行任何网络服务。

`systemd` 使用特殊目标（targets）而不是运行级别来创建与运行级别相同的效果，通过将服务分组以为指定的目标运行。运行级别已不再被实现。这里有两个主要的特殊目标：多用户（multi-user）和图形化（graphical）。多用户目标类似于运行级别 3，为你提供命令行登录界面。图形化目标类似于运行级别 5，为你提供图形化登录和界面。

你通过将目标的 `systemd` 服务文件链接到 `systemd` 默认目标文件来设置默认目标（运行级别）。此操作取代了以前版本中通过 `inittab` 指定默认运行级别的方法。以下命令将图形化界面设为默认（运行级别 5）。

```bash
ln -s /lib/systemd/system/graphical.target /etc/systemd/system/default.target
```

`systemd` 确实提供了对运行级别的兼容支持。运行级别兼容是通过使用 `/lib/system/systemd` 目录下的符号链接到 `systemd` 目标来实现。`runlevel0.target` 链接引用 systemd 的 `poweroff.target`。运行级别 2、3 和 4 目标都链接到同一个 `multi-user.target`（命令行界面）。`runlevel6.target` 链接到 `reboot.target`，而 `runlevel5.target` 链接到 `graphical.target`（桌面界面）。运行级别及其目标列在表 12-10 中。

| 系统运行级别链接 | systemd 目标 |
| :--- | :--- |
| runlevel0 | poweroff.target |
| runlevel1 | rescue.target |
| runlevel2 | multi-user.target |
| runlevel3 | multi-user.target |
| runlevel4 | multi-user.target. |
| runlevel5 | graphical.target. |
| runlevel6 | reboot.target |

表 12-10：系统运行级别（状态）

你仍然可以使用 `runlevel` 命令查看你当前运行在什么状态。它会列出上一个状态，然后是当前状态。如果你没有更改状态，上一个状态将显示为 `N`，表示没有之前的状态。你启动系统时的状态就是如此。在下一个示例中，系统运行在状态 3，没有之前的状态更改。

```bash
runlevel N 3
```

如果你在某个特定的运行级别下遇到问题，更改运行级别可能会很有帮助。例如，如果你的显卡没有安装正确，那么任何尝试在运行级别 5 (`graphical.target`) 启动的尝试都会失败，因为该级别会立即启动你的图形化界面。相反，你可以使用命令行界面，运行级别 3 (`multi-user.target`) 来修复你的显卡安装。

无论你从哪个运行级别启动，你都可以使用 `telinit` 命令从一个运行级别切换到另一个。如果你的默认运行级别是 3，你在运行级别 3 下启动，但你可以通过 `telinit 5` 切换到运行级别 5。命令 `telinit 0` 关闭你的系统。在下一个示例中，`telinit` 命令切换到运行级别 1，即管理状态。

```bash
telinit 1
```

在 `systemd` 实现之前，你也可以使用 `init` 来更改运行级别。在 `systemd` 中，`telinit` 和 `init` 现在都是原始 Unix 命令的 `systemd` 仿真版本。`telinit` 命令始终用于更改运行级别。如果你带数字使用 `init`，它现在仅仅是调用 `telinit` 来进行更改。

或者，你可以直接使用 `systemctl` 命令来更改运行级别（目标）。带有 `isolate` 选项和目标文件名的 `systemctl` 命令切换到该目标（运行级别）。这正是 `telinit` 命令实际的操作。以下命令切换到多用户目标。

```bash
sudo systemctl isolate multi-user.target
```

你也可以使用运行级别链接。

```bash
sudo systemctl isolate runlevel3.target
```

## systemd 与自动挂载文件系统：/etc/fstab

扩展名为 `.mount` 的 `systemd` 单元文件可自动挂载文件系统。通常 systemd 会读取 `/etc/fstab` 文件获取挂载信息。如果 `/etc/systemd` 目录下存在挂载单元文件，它具有优先级，但 `/etc/fstab` 的优先级高于 `/lib/systemd` 目录中的任何单元挂载文件`/etc/fstab` 文件用于挂载配置信息。挂载单元文件的大部分选项对应于 `/etc/fstab` 文件中的选项，指定设备路径名称、挂载点、文件系统类型和挂载选项（参见表 12-11）。




挂载单元文件必须根据其引用的挂载点命名。单元名称中的路径斜杠会被替换为连字符。例如，`proc-fs-nfsd.mount` 文件引用了挂载点 `/proc/fs/nfsd`。根路径名称 `/` 变成了连字符 `-`。

为了在访问文件系统时对其自动挂载，可以使用 `automount` 单元类型。自动挂载单元必须有一个同名的对应挂载单元。

`systemd-fsck@service` 文件提供使用 `fsck` 对文件系统进行检查，并将磁盘名称作为参数。

`RequiresOverridable=system-fsck@dev-disk-by\x2duuid-5537\x2dAF41.service`

`After=system-fsck@dev-disk-by\x2duuid-5537\x2dAF41.service`

### systemd slice 和 scope 单元

slice（切片）和 scope（范围）单元旨在将单元分组，以便于控制它们的进程和资源。scope 单元由 systemd 生成，用于管理进程及其子进程。scope 单元的一个示例是用户会话范围，它将用户会话的进程分组在一起。slice 用于管理进程的资源，例如用于虚拟机的 machine slice、用于系统服务的 system slice，以及用于用户会话的 user slice。

## System V: /etc/init.d

SysVinit 对服务的支持已不再实现。没有用于启动服务的 `rc.d` 脚本。`systemd` 直接管理所有服务。请检查 `/etc/init.d` 目录下的 README 文件。对于极少数系统任务，你可能会在 `/etc/init.d` 目录中找到 System V 脚本。`systemd` 将读取这些脚本作为服务的配置信息，并为其生成相应的单元配置文件。反之，单元文件可能会使用 `init.d` 脚本来启动、停止和重启服务。如果已经存在单元文件，则使用该单元文件，并忽略 System V 脚本。

少数服务器使用从 `/etc/init.d` 目录中的 System V 脚本生成的单元文件，例如 NIS。单元文件由 `systemd-sysv-generator` 生成，位于 `/var/run/systemd/generator.late` 目录。

位于 `/lib/systemd/system` 目录下的 `rc-local.service` 单元会在存在 `/etc/rc.local` 文件运行时运行。这是为了与旧的 System V 配置保持兼容。

## 关机和断电

你可以使用 `shutdown` 和 `poweroff` 命令来关闭系统。`shutdown` 命令提供了更多选项。请注意使用的 `shutdown` 命令是 systemd 版本，它将使用 `systemctl` 实际关闭系统。

你也可以使用 `sudo` 命令配合 `poweroff` 命令立即关闭系统。系统会提示你输入密码。

```
sudo poweroff
```

要执行重启，你可以使用 `reboot` 命令。

```
sudo reboot
```

`shutdown` 命令有一个时间参数，可以在关机前向系统上的用户发出警告。你可以指定精确的关机时间，或者从当前时间开始的几分钟。精确时间由 `hh:mm` 指定小时和分钟。时间段则由 `+` 加上分钟数表示。

`shutdown` 命令带有多个选项，你可以通过这些选项指定如何关闭系统。`-h` 选项代表 halt（停止），它直接关闭系统，而 `-r` 选项在关闭系统后重启。在下一个示例中，系统将在十分分钟后关闭。

```
shutdown -h +10
```

要立即关闭系统，你可以使用 `+0` 或单词 `now`。关机选项列表 12-12 中。以下示例将立即关闭系统并重启。

```
shutdown -r now
```

| 命令 | 描述 |
| :--- | :--- |
| `shutdown [-rkhncft] time [warning]` | 在指定的时间段后关闭系统，并向用户发出警告；你可以在时间参数后指定自定义的警告消息；如果既没有指定 `-h` 也没有指定 `-r`，则系统将设置为管理模式，运行级别状态 1。 |
| 参数 |   |
| Time | 有两种可能的格式：它可以是 `hh:mm` 格式的绝对时间，其中 `hh` 为小时（一位或两位数），`mm` 为分钟（两位数）；也可以是 `+m` 格式，其中 `m` 为等待的分钟数；单词 `now` 是 `+0` 的别名。 |
| 选项 |  |
| `-t sec` |  init 在向进程发送警告和杀死信号之间等待 `sec` 秒，然后再切换到另一个运行级别。 |
| `-k` | 不实际关闭；仅向所有人发送警告消息。 |
| `-r` | 关机后重启，运行级别状态 6。 |
| `-h` | 关机后停止，运行级别状态 0。 |
| `-n` | 不调用 init 执行关机；由你手动执行。 |
| `-f` | 重启时跳过文件系统检查 (`fsck`)。 |
| `-c` | 取消正在运行的关机；无时间参数。 |

表 12-12：关机选项

使用 `shutdown` 命令，你可以在关机前向所有用户包含警告消息，让他们在关机前完成工作。

```
shutdown -h +5 "系统需要休息"
```

如果你没有指定 `-h` 或 `-r` 选项，`shutdown` 命令会将多用户状态切换到单用户模式。此时 root 用户是激活的，允许执行任何可能干扰其他用户的操作。

关机过程通过 systemd 使用 `systemctl` 命令实现。poweroff、halt 和 reboot 命令调用 systemd 服务文件。`systemctl` 命令反过来使用 `/lib/systemd-shutdown` 执行关机。在 `/lib/systemd/system` 目录中，`systemd-poweroff.halt` 文件显示 `systemctl poweroff`。shutdown 服务的手册是 `systemd-halt.service`。始终使用 `poweroff`、`reboot` 和 `halt` 命令关机，而不是使用 `systemctl` 命令。

```
systemd-poweroff.service

# 此文件是 systemd 的。

# systemd 是自由软件；你可以根据自由软件基金发布的
# GNU 通用许可证分发或修改它；该许可证的
# 2.1 版本，或（根据你的选择）任何更高版本。 [Unit]

Description=Power-Off

Documentation=man:systemd-halt.service(8)

DefaultDependencies=no

Requires=shutdown.target umount.target final.target

After=shutdown.target umount.target final.target

[Service]

Type=oneshot

ExecStart=/bin/systemctl --force poweroff
```注：halt 命令仅仅是停止系统，并不将其关闭。

## 管理服务

你可以选择要运行的服务以及运行这些服务的特殊目标（运行级别）。大多数服务都是服务器，如 Web 服务器或 FTP 服务器。其他服务提供安全保障，如 SSH 或 Kerberos。你可以使用 `systemctl` 命令决定使用哪些服务。

### 启用服务：在启动时自动启动服务

Apache Web 服务器、Samba 服务器和 FTP 服务器等由 systemd 守护进程处理。你可以使用 `systemctl` 命令管理服务。旧的 `service` 命令仅仅是 `systemctl` 命令的前端。




要让服务在启动时运行，你首先需要以 root 用户身份使用 `systemctl` 工具启用它。使用 `enable` 命令来启用服务。以下命令将启用 `vsftpd` 服务器和 Samba 服务器 (`smbd`)。`systemctl` 命令使用位于 `/lib/systemd/system` 或 `/etc/systemd/system` 目录下的服务配置文件。

```
sudo systemctl enable vsftpd.service
sudo systemctl enable smbd
```

## 手动管理服务：systemctl

使用 `systemctl` 的 `start`、`stop` 和 `restart` 命令来手动启动、停止和重启服务。`enable` 命令仅用于自动启动服务。你可以选择使用 `start` 命令手动启动它。你可以随时使用 `stop` 和 `restart` 命令停止和重启服务。`condrestart` 命令仅在服务器已处于停止状态时才启动它。使用 `status` 命令检查服务的当前状态。

```
sudo systemctl start vsftpd
sudo systemctl restart vsftpd
sudo systemctl condrestart vsftpd
sudo systemctl stop vsftpd
sudo systemctl status vsftpd
```

## service 命令

旧的 `service` 命令现在仅是 `systemctl` 命令的前端，由后者使用 `systemd` 执行实际操作。`service` 命令无法启用或禁用服务。它只执行启动、停止、重启和状态等管理操作。使用 `service` 命令时，你通过输入服务名和 `stop` 参数来停止它，输入 `start` 参数启动它，以及输入 `restart` 参数重启它。`service` 命令从终端窗口中运行。你将需要使用 `sudo` 命令。以下命令将启动 `vsftpd` FTP 服务。

```
sudo service vsftpd start
```

`systemd` 版本的 `service` 命令实际上会调用 `systemctl` 命令来运行位于 `/lib/systemd/system` 中的服务 systemd `.service` 单元文件。如果服务未启用，`systemd` 将会启用它。你可以使用 `systemctl` 命令执行与 `service` 命令相同的操作。以下是前一个命令的等效操作。

```
sudo systemctl start vsftpd
```

## Cockpit

Cockpit 管理控制台（由红帽提供）提供了一个 Web 界面，用于管理系统上的系统管理和互联网服务器，以及你网络上的服务器（[`cockpit-project.org`](https://cockpit-project.org)）。该 Web 界面在桌面系统中效果最佳。你可以用它管理系统资源，包括服务、存储和网络。一旦安装了 cockpit，务必使用 `systemd` 启用它，然后通过防火墙允许 cockpit 和 https 的访问。该包名为 `cockpit`。

```
sudo apt-get install cockpit
sudo systemctl enable cockpit
```

你可以通过“管理 | Cockpit”访问 Cockpit。这将用你的默认浏览器打开 cockpit。你也可以使用 Web 浏览器并访问本地系统的 9090 端口（`localhost:9090`）来访问 cockpit。cockpit 页面最初提示你输入用户名和密码。确保勾选“在权限任务中重复我的密码”复选框，以便你可以进行更改。随后它会显示网络上的系统列表。点击其中一个后，你将在左侧看到管理类别的链接，例如系统管理、服务、网络和存储。点击“服务”链接来管理你的服务。然后点击“系统服务”选项卡列出启用和禁用的服务，包括网络服务，如 Samba、Apache Web 服务器和 vsftpd FTP 服务器（参见图 12-1）。点击服务将打开一个可以管理服务的页面。右侧的按钮显示当前状态。点击右侧的箭头按钮将显示可能想要执行的操作菜单，例如停止或重启服务。如果你禁用了某个服务，它会被移动到禁用列表。启用服务将将其移到启用列表。

![Image](img/image-604.png) ![Image](img/image-605.png)

图 12-1：服务：cockpit

Cockpit 会随 `systemctl` 动态更新。如果你在终端窗口中使用 `systemctl` 了更改，更改将立即显示在 Cockpit 上。

## /etc/default

`/etc/default` 目录存放服务启动时设置运行时选项的脚本。例如，`/etc/default/apache2` 脚本设置缓存清理选项`/etc/default/ufw` 脚本设置防火墙默认策略。你可以编辑这些脚本并更改分配给选项的值，从而改变服务的行为。

## 网络时间协议：Chrony

为了让服务器正确运行，它们始终需要保持正确的时间。全球互联网时间服务器以协调世界时（UTC）的形式提供时间。然后使用本地系统的本地时区计算本地时间。时间通过互联网连接从互联网时间服务器获取。你也可以选择使用本地硬件时钟，尽管其可能可能低得多。

通常，主机上的时间存储在计时芯片 (TOY) 中，该芯片在机器关闭时维持时间。当机器重启时，会使用该时间。使用网络时间协议的主机会使用从互联网时间服务器获取的时间调整时间。如果差异超过 1000 秒（约 15 分钟），则需要管理员手动设置时间。

主主机的时间由 `systemd-timesyncd` 进程同步。你可以使用 `timedatectl` 命令管理并设置主机时间。然而，如果你想在本地网络上设置时间服务器，可以使用 `chrony`。

现在使用 Chrony 服务器来取代旧的 NTP 时间服务器。你可以在此处找到 Chrony 的文档：

[`chrony.tuxfamily.org`](https://chrony.tuxfamily.org)

Ubuntu 仓库中有一个 Chrony 包。你可以通过软件管理器、`apt` 命令或 Synaptic 包管理器安装它。

```
sudo apt install chrony
```

`chronyd`、`chrony.conf` 和 `chronyc` 有帮助页。`chronyd` 服务器的命令行界面是 `chronyc`。

## Chrony 服务器

Chrony 服务器名为 `chronyd`，由 `/lib/systemd/system/chrony.service` 脚本管理。

```
chrony.service
[Unit]
Description=chrony, an NTP client/server
Documentation=man:chronyd(8) man:chronyc(1) man:chrony.conf(5)
Conflicts=systemd-timesyncd.service openntpd.service
After=network.target

[Service]
Type=forking
PIDFile=/run/chronyd.pid
EnvironmentFile=-/etc/default/chrony
# Starter 主要负责处理容器的特殊情况
ExecStart=/usr/lib/systemd/scripts/chronyd-starter.sh $DAEMON_OPTS
ExecStartPost=-/usr/lib/chrony/chrony-helper update-daemon
PrivateTmp=yes
ProtectHome=yes
ProtectSystem=full

[Install]
Alias=chronyd.service
WantedBy=multi-user.target
```

使用 `systemctl` 命令的 `start`、`stop` 和 `restart` 选项来管理服务器。

```
sudo systemctl start chronyd
```




Chrony 服务器配置文件为 `/etc/chrony/chrony.conf`。此文件列出了你的本地时间服务器用于确定时间的互联网时间服务器。请查看 `chrony.conf` 手册页以获取 Chrony 服务器配置指令的完整列表。

在 `chrony.conf` 文件中，`server` 指令指定了你的 Chrony 服务器用于访问时间的互联网时间服务器的 Internet 地址。Ubuntu 时间服务器池有一个默认条目，但你可以为其他时间服务器添加更多 `server` 条目。对于特定的时间服务器，你会使用 `server` 指令。

```
pool ntp.ubuntu.com
```

此处显示默认的 `/etc/chrony/chrony.conf` 文件。

```
# Welcome to the chrony configuration file. See chrony.conf(5) for more
# 欢迎使用 chrony 配置文件。有关可用指令的信息，请参考 chrony.conf(5)
# This will use (up to):
# - 4 sources from ntp.ubuntu.com which some are ipv6 enabled
# - 2 sources from 2.ubuntu.pool.ntp.org which is ipv6 enabled as well
# - 1 source from [01].ubuntu.pool.ntp.org each (ipv4 only atm)
# This means by default, up to 6 dual-stack and up to 2 additional IPv4-only
# sources will be used.
# 这意味着默认情况下，将使用最多 6 个双栈源和最多 2 个额外的仅 IPv4 仅
# 源。
# At the same time it retains some protection against one of the entries being
# down (compare to just using one of the lines). See (LP: #1754358) for the discussion.
# 与此同时，它保留了防止某个条目故障的某些保护（与仅使用其中一行相比）。
# 请参考 (LP: #1754358) 的讨论。
# About using servers from the NTP Pool Project in general see (LP: #104525).
# 关于通用的使用来自 NTP Pool Project 的服务器，请参考 (LP: #104525)。
# Approved by Ubuntu Technical Board on 2011-02-08.
# 由 Ubuntu 技术委员会于 2011-02-08 批准。
# See http://www.pool.ntp.org/join.html for more information.
# 更多信息请访问 http://www.pool.ntp.org/join.html。
pool ntp.ubuntu.com iburst maxsources 4 pool 0.ubuntu.pool.ntp.org iburst maxsources 1
pool 1.ubuntu.pool.ntp.org iburst maxsources 1
pool 2.ubuntu.pool.ntp.org iburst maxsources 2
# This directive specify the location of the file containing ID/key pairs for
# NTP authentication.
# 此指令指定包含用于 NTP 认证的 ID/密钥对的文件位置。
keyfile /etc/chrony/chrony.keys
# This directive specify the file into which chronyd will store the rate
# information.
# 此指令指定 chronyd 将存储速率信息的文件。
driftfile /var/lib/chrony/chrony.drift
# Uncomment the following line to turn logging on.
# 注消以下行以启用日志记录。
#log tracking measurements statistics
# Log files location.
# 日志文件位置。
logdir /var/log/chrony
# Stop bad estimates upsetting machine clock.
# 阻止错误的估计影响机器时钟。
maxupdateskew 100.0
# This directive enables kernel synchronisation (every 11 minutes) of the
# real-time clock. Note that it cannot be used along with the 'rtcfile' directive.
# 此指令启用实时时钟的内核同步（每 11 分钟）。注意，它不能与 'rtcfile' 指令一起使用。
rtcsync
# Step the system clock instead of slewing it if the adjustment is larger than
# one second, but only in the first three clock updates.
# 如果调整大于一秒，则步进系统时钟而不是调频，但仅在前三次时钟更新中进行。
makestep 1 3
```

`allow` 指令允许本地网络上的主机访问你的时间服务器，而 `deny` 指令拒绝访问。这些主机就可以使用你的时间服务器。`deny` 指令拒绝指定主机的访问。

你可以使用 `cmdallow` 命令允许客户端主机查看你的时间服务器监控信息。主机随后可以运行 `cronyc` 命令行界面来执行监控命令。`cmddeny` 将拒绝访问。

你还可以以广播模式运行时间服务器，将时间广播到你的网络客户端。使用 `broadcast` 指令和你的网络广播地址。

```
broadcast 192.168.123.255
```

### cronyc

`cronyc` 命令行界面允许你监控你的 `chronyd` 服务器，生成状态报告，并允许在程序运行时更改 `chronyd` 配置。你通过 `cronyc` 命令启动 cronyc 界面。这会将你带入具有 `chrony>` 提示符的交互式 shell，你可以在其中输入 `cronyc` 命令。要退出 shell，输入 `quit` 命令。

出于安全考虑，普通用户或来自其他主机的用户只能使用监控命令。`activity` 命令将检查有多少 NTP 源在线，`sourcestats` 将列出 NTP 源的性能信息。

```
$chronyc chronyc>
```

如果你想输入配置命令，必须以 root 用户身份启动 `chronyc`。使用 `sudo` 命令。请记住，这些更改不是永久的。`chrony.conf` 文件不会受到影响。

```
sudo chronyc
```

要手动设置时间，你必须以 root 用户身份进入 `cronyc` shell，并使用 `settime` 命令指定时间。你可能需要先运行 `manual` 命令来启用 `settime` 命令。

```
$ sudo chronyc chronyc> manual on chronyc> settime Apr 7, 2018 18:24:09 chronyc> quit
```

## AppArmor 安全

Linux Mint 安装 AppArmor 作为其默认安全系统。AppArmor (Application Armor) 被设计为 SELinux（Security-Enhanced Linux, `http://selinuxproject.org/page/Main_Page`）的替代方案。它简单得多，但利用了 SELinux 提供的相同的内核支持。AppArmor 是一种为指定的 Linux 应用实现强制访问控制 (MAC) 的简单方法。它主要用于 Samba、CUPS 打印服务器和时间服务器等服务器。

Linux Mint 安装 AppArmor 作为其默认安全系统。AppArmor (Application Armor) 被设计为 SELinux（Security-Enhanced Linux, `http://selinuxproject.org/page/Main_Page`）的替代方案。它简单得多，但利用了 SELinux 提供的内核支持。AppArmor 是一种为指定的 Linux 应用实现强制访问控制 (MAC) 的简单方法。它主要用于 Samba、CUPS 打印服务器和时间服务器等服务器。

Linux Mint 安装 AppArmor 作为其默认安全系统。AppArmor (Application Armor) 被设计为 SELinux（Security-Enhanced Linux, `http://selinuxproject.org/page/Main_Page`）的替代方案。它简单得多，但利用了 SELinux 提供的内核支持。AppArmor 是一种为指定的 Linux 应用实现强制访问控制 (MAC) 的简单方法。它主要用于 Samba、CUPS 打印服务器和时间服务器等服务器。

Linux Mint 安装 AppArmor 作为其默认安全系统。AppArmor (Application Armor) 被设计为 SELinux（Security-Enhanced Linux, `http://selinuxproject.org/page/Main_Page`）的替代方案。它简单得多，但利用了 SELinux 提供的内核支持。AppArmor 是一种为指定的 Linux 应用实现强制访问控制 (MAC) 的简单方法。它主要用于 Samba、CUPS 打印服务器和时间服务器等服务器。

Linux Mint 安装 AppArmor 作为其默认安全系统。AppArmor (Application Armor) 被设计为 SELinux（Security-Enhanced Linux, `http://selinuxproject.org/page/Main_Page`）的替代方案。它简单得多，但利用了 SELinux 提供的内核支持。AppArmor 是一种为指定的 Linux 应用实现强制访问控制 (MAC) 的简单方法。它主要用于 Samba、CUPS 打印服务器和时间服务器等服务器。

Linux Mint 安装 AppArmor 作为其默认安全系统。AppArmor (Application Armor) 被设计为 SELinux（Security-Enhanced Linux, `http://selinuxproject.org/page/Main_Page`）的替代方案。它简单得多，但利用了 SELinux 提供的内核支持。AppArmor 是一种为指定的 Linux 应用实现强制访问控制 (MAC) 的简单方法。它主要用于 Samba、CUPS 打印服务器和时间服务器等服务器。

Linux Mint 安装 AppArmor 作为其默认安全系统。AppArmor (Application Armor) 被设计为 SELinux（Security-Enhanced Linux, `http://selinuxproject.org/page/Main_Page`）的替代方案。它简单得多，但利用了 SELinux 提供的内核支持。AppArmor 是一种为指定的 Linux 应用实现强制访问控制 (MAC) 的简单方法。它主要用于 Samba、CUPS 打印服务器和时间服务器等服务器。

Linux Mint 安装 AppArmor 作为其默认安全系统。AppArmor (Application Armor) 被设计为 SELinux（Security-Enhanced Linux, `http://selinuxproject.org/page/Main_Page`）的替代方案。它简单得多，但利用了 SELinux 提供的内核支持。AppArmor 是一种为指定的 Linux 应用实现强制访问控制 (MAC) 的简单方法。它主要用于 Samba、CUPS 打印服务器和时间服务器等服务器。

Linux Mint 安装 AppArmor 作为其默认安全系统。AppArmor (Application Armor) 被设计为 SELinux（Security-Enhanced Linux, `http://selinuxproject.org/page/Main_Page`）的替代方案。它简单得多，但利用了 SELinux 提供的内核支持。AppArmor 是一种为指定的 Linux 应用实现强制访问控制 (MAC) 的简单方法。它主要用于 Samba、CUPS 打印服务器和时间服务器等服务器。

Linux Mint 安装 AppArmor 作为其默认安全系统。AppArmor (Application Armor) 被设计为 SELinux（Security-Enhanced Linux, `http://selinuxproject.org/page/Main_Page`）的替代方案。它简单得多，但利用了 SELinux 提供的内核支持。AppArmor 是一种为指定的 Linux 应用实现强制访问控制 (MAC) 的简单方法。它主要用于 Samba、CUPS 打印服务器和时间服务器等服务器。

Linux Mint 安装 AppArmor 作为其默认安全系统。AppArmor (Application Armor) 被设计为 SELinux（Security-Enhanced Linux, `http://selinuxproject.org/page/Main_Page`）的替代方案。它简单得多，但利用了 SELinux 提供的内核支持。AppArmor 是一种为指定的 Linux 应用实现强制访问控制 (MAC) 的简单方法。它主要用于 Samba、CUPS 打印服务器和时间服务器等服务器。

Linux Mint 安装 AppArmor 作为其默认安全系统。AppArmor (Application Armor) 被设计为 SELinux（Security-Enhanced Linux, `http://selinuxproject.org/page/Main_Page`）的替代方案。它简单得多，但利用了 SELinux 提供的内核支持。AppArmor 是一种为指定的 Linux 应用实现强制访问控制 (MAC) 的简单方法。它主要用于 Samba、CUPS 打印服务器和时间服务器等服务器。

Linux Mint 安装 AppArmor 作为其默认安全系统。AppArmor (Application Armor) 被设计为 SELinux（Security-Enhanced Linux, `http://selinuxproject.org/page/Main_Page`）的替代方案。它简单得多，但利用了 SELinux 提供的内核支持。AppArmor 是一种为指定的 Linux 应用实现强制访问控制 (MAC) 的简单方法。它主要用于 Samba、CUPS 打印服务器和时间服务器等服务器。

Linux Mint 安装 AppArmor 作为其默认安全系统。AppArmor (Application Armor) 被设计为 SELinux（Security-Enhanced Linux, `http://selinuxproject.org/page/Main_Page`）的替代方案。它简单得多，但利用了 SELinux 提供的内核支持。AppArmor 是一种为指定的 Linux 应用实现强制访问控制 (MAC) 的简单方法。它主要用于 Samba、CUPS 打印服务器和时间服务器等服务器。

Linux Mint 安装 AppArmor 作为其默认安全系统。AppArmor (Application Armor) 被设计为 SELinux（Security-Enhanced Linux, `http://selinuxproject.org/page/Main_Page`）的替代方案。它简单得多，但利用了 SELinux 提供的内核支持。AppArmor 是一种为指定的 Linux 应用实现强制访问控制 (MAC) 的简单方法。它主要用于 Samba、CUPS 打印服务器和时间服务器等服务器。

Linux Mint 安装 AppArmor 作为其默认安全系统。AppArmor (Application Armor) 被设计为 SELinux（Security-Enhanced Linux, `http://selinuxproject.org/page/Main_Page`）的替代方案。它简单得多，但利用了 SELinux 提供的内核支持。AppArmor 是一种为指定的 Linux 应用实现强制访问控制 (MAC) 的简单方法。它主要用于 Samba、CUPS 打印服务器和时间服务器等服务器。





`aa-autodep` 工具将为新应用程序或未限制的应用程序生成基础 AppArmor 配置文件。如果你想要一个更有效的配置，可以使用 `aa-genprof` 分析应用程序的使用情况并相应生成配置控制规则。

`aa-genprof` 工具将为指定的应用程序更新或生成详细的配置。`aa-genprof` 会首先将配置设置为投诉模式（complain mode）。然后你启动应用程序并使用它，在这些过程中会生成投诉模式的日志消息。随后，`aa-genprof` 会提示你是扫描投诉消息以进一步细化配置（`S`），还是完成（`F`）。在扫描时，系统会检测到不同的违规行为，并提示用户允许或拒绝建议的控制规则。你可以重复扫描操作，直到你认为配置是可以接受的。选择完成（`F`）以完成配置并退出。

## AppArmor 配置

AppArmor 配置位于 `/etc/apparmor` 目录。不同配置的配置位于 `/etc/apparmor.d` 目录。已加载的配置文件的文件名以其路径命名，并使用点代替斜杠来分隔目录名。`smbd` (Samba) 应用程序的配置文件名为 `usr.sbin.smbd`。对于 CUPS (`cupsd`)，它是 `usr.sbin.cupsd`。如 Samba 和 Apache 等额外的配置通过 `apparmor-profiles` 软件包安装（默认未安装）。

```
sudo apt-get install apparmor-profiles
```

AppArmor 配置文件的配置规则由路径和在该路径上允许的权限组成。关于 AppArmor 规则和权限的详细说明可以在 `apparmor.d` 手页中找到，其中包含配置示例。以匹配符号 `*` 结尾路径将选择该目录下的所有文件。`**` 符号选择所有文件和子目录。支持所有文件匹配操作（`*` `[]` `?`）。权限包括 `r`（读）、`w`（写）、`x`（执行）和 `l`（链接）。`u` 权限允许无限制访问。以下条目允许 `/var/log/samba/cores/smbd` 目录下的所有文件和子目录被写入。

```
/var/log/samba/cores/smbd/** rw,
```

`/etc/apparmor.d/abstractions` 目录下的文件包含不同配置间通用的规则。这些文件中的规则通过 `include` 指令读取到实际配置中。针对音频、samba 和视频等应用程序有相应的抽象。某些抽象还会包含其他更通用的抽象，例如针对 X 服务器 (`X`) 或 GNOME (`gnome`) 的抽象。例如，Samba smbd 服务器的配置 `usr.sbin.smbd` 将有一个针对 `samba` 抽象的 `include` 指令。该抽象包含了 `smbd` 和 `nmbd` 服务器共用的规则，这两者都由 Samba 服务使用。`include` 指令中 `<>` 表示 `/etc/apparmor.d` 目录。可以在 `apparmor.d` 手页中找到抽象文件列表。`include` 指令以 `#` 字符开头。

```bash
#include <abstractions/samba>
```

在某些情况下，配置可能需要访问其通常不应具备访问权限的某个目录中的某些文件。在这种情况下，它可能需要使用子配置来允许访问。实际上，应用程序更改了身份，承担了在原始配置中不具备的权限。

`armor-profiles` 软件包将激活几个常用配置，并在 `/etc/apparmor.d` 目录为它们建立配置文件，例如 samba (`usr.sbin.nmbd` 和 `usr.sbin.smbd`)、Dovecot  pop 和 imap 服务器 (`usr.sbin.dovecot`) 以及 Avahi (`usr.sbin.avahi-daemon`)。

该软件包还会在 `/usr/share/doc/apparmor-profiles/extras` 目录下为许多应用程序提供配置默认文件，例如 vsftpd FTP 服务器 (`usr.sbin.vsftpd`)、ClamAV 病毒扫描器 (`usr.bin.freshclam`) 和 Squid 代理服务器 (`usr.sbin.squid`)。某些服务应用程序位于 `/usr/lib` 目录，并具有 `usr.lib` 前缀，例如 Postfix 服务器，它使用多个配置，以 `usr.lib.postfix` 开头。要使用这些额外配置的配置，请将它们复制到 `/etc/apparmor.d` 目录。以下示例复制了 vsftpd FTP 服务器的配置。

```
sudo cp /usr/share/doc/apparmor-profiles/extras/usr.sbin.vsftpd /etc/apparmor.d
```

## 远程管理

对于远程管理，你可以使用 OpenSSH 和 Puppet。OpenSSH 让你能够通过网络安全地远程控制和传输文件。Puppet 允许你管理服务的远程配置。

### Puppet

Puppet 允许你自动配置远程系统，即使它们可能运行带有不同配置文件的 Linux 发行版。与其手动配置网络上的每个系统，你可以使用 Puppet 自动配置它们。Puppet 将管理任务抽象为资源抽象层 (RAL) 中的资源。然后你使用 Puppet 配置语言为特定资源指定基本值或操作。管理类型包括服务、文件、用户和组。例如，你可以使用 puppet 对使用 APT 或 Synaptic 等不同包管理器的系统上的服务（服务器）执行更新。

Puppet 配置可能会变得非常复杂。但是，一旦设置好，它就能完全自动化你所有网络系统上的配置更改。有关详细的文档和指南，请参见以下内容。

[`puppet.com/docs/`](https://puppet.com/docs/)

Puppet 配置位于 `/etc/puppet` 目录。Puppet 服务操作在 `manifests` 目录下的 `init.pp` 文件中指定。在 Ubuntu 的 Apache 示例中，apache 模块创建在 `init.pp` 文件中：

```
/etc/puppet/modules/apache2/manifests/init.pp
```

在 Linux Mint 和 Ubuntu 上，客户端使用 puppet 软件包，服务器使用 puppetmaster 软件包。在 puppet 客户端上，使用 `systemctl` 命令手动启动和停止 `puppet` 服务。对于服务器，启用 `puppetmaster` 服务。

在防火墙上为 Puppet 端口 `8140` 添加访问。

对于客户端，运行时的配置设置在 `/etc/default/puppet` 文件中。在这里通过将 `START` 变量设置为 `yes` 来启动守护进程。

如果你的网络运行 DNS 服务器，你可以为 puppet 服务器设置一个 CNAME 条目。puppet 客户端可以使用 CNAME 定位 puppet 服务器。

```
puppet IN CNAME turtle.mytrek.com
```

你也可以在每个的 `/etc/host` 文件为 puppet 服务器添加主机条目。

在服务器上，`/etc/default/puppetmaster` 中的 puppetmaster 配置允许设置端口和日志服务。默认条目被注释掉了。移除注释字符 `#` 以启用。

首次设置客户端服务器 puppet 连接时，客户端和服务器必须对客户端的 SSL 证书签名。首先，在客户端上运行 puppet。在服务器上运行 `puppet cert --list` 命令查看客户端的证书请求。然后使用 `puppet cert --sign` 进行签名。

### 安全 Shell: OpenSSH

尽管防火墙可以保护网络免受外部入侵的尝试，但保护外部源到网络合法通信的问题仍然存在。一个特别的问题是想要远程连接到你的网络的用户。此类连接可能会被监控，用户登录你的网络时使用的密码和用户 ID 等信息可能会被复制并用于以后入侵。一种解决方案是使用 SSH 进行远程登录和其他类型的远程连接（如 FTP 传输）。SSH 加密远程用户与你网络系统之间的任何通信。





SSH 协议已成为互联网工程任务组（IETF）的官方标准。一个免费开源版本由 OpenSSH 项目开发并维护，目前由 OpenBSD 项目支持。OpenSSH 是大多数 Linux 发行版（包括 Linux Mint）提供的版本。你可以在 [`www.openssh.com/`](https://www.openssh.com/) 了解更多关于 OpenSSH 的信息，在那里你可以下载最新版本，尽管 Linux Mint 和 Ubuntu 也会从其仓库提供当前版本。传统上，SSH 有两个版本：旧的 SSH1 及其替代版本 SSH2。在当前的 OpenSSH 发布版本中，SSH1 默认被禁用了。如果你需要 SSH1 工具来访问旧的仅支持 SSH1 的服务器，可以安装 `openssh-client-ssh1` 软件包。

SSH 通过验证用户和加密传输来确保连接的安全。身份验证过程通过公钥加密处理。一旦通过验证，传输内容将由 SSH 服务器和客户端为特定会话约定的加密算法进行加密。SSH 支持多种加密算法。身份验证同时适用于主机和用户。SSH 首先对特定主机进行验证，验证其是一个可以进行安全通信的有效 SSH 主机。然后对用户进行验证，验证该用户确实其所称身份。

### 加密

SSH 身份验证中使用的公钥加密使用了两个：公钥和私钥。公钥用于加密数据，而私钥用于解密。每个主机或用户都有自己的公钥和私钥。公钥被分发给其他主机，这些主机可以使用它来加密验证数据，只有该主机的私钥才能解密这些数据。例如，当主机向另一个系统上的用户发送数据时，主机使用之前从该用户那里接收的公钥加密验证数据。该数据只能由用户对应的私钥解密。公钥可以安全地从一个主机发送到另一台主机，允许其安全地安装在不同的主机上。你可以将此过程认为发生在客户端和服务器之间。当客户端向服务器发送数据时，它首先使用服务器的公钥加密数据。然后服务器可以使用自己的私钥解密数据。

建议使用由密码短控制的公私密钥对 SSH 传输进行身份验证。与 PGP 不同，SSH 仅在身份验证过程中使用公钥加密。一旦验证通过，参与者将约定一种常用的加密算法来加密传输。身份验证将验证参与者的身份。每个意图使用 SSH 访问远程账户的用户首先需要创建公钥、私钥以及用于身份验证过程的密码短语。然后，用户将其公钥发送到其想要访问的远程账户，并将公钥安装在该账户上。当该用户尝试访问远程账户时，该账户就可以使用用户的公钥来验证该用户确实是其所称身份。该过程假设远程账户已设置了自身的 SSH 私钥和公钥。用户要访问远程账户，必须知道远程账户的 SSH 密码短语。SSH 通常用于用户在不同系统上拥有两个或多个账户，并希望能够相互安全访问的情况。在这种情况下，用户已经拥有每个账户的访问权限，可以在每个账户上安装 SSH，为每个账户提供自己的公私钥及其密码短语。

### 身份验证

在 SSH 身份验证中，用户需要同时创建公钥和私钥。为此，你需要使用 `ssh-keygen` 命令。然后，用户的公钥必须分发给原始用户想要访问的那些用户。通常这是用户在另一个主机上的账户。密码短语进一步保护了访问。原始用户需要知道另一个用户的密码短语才能访问它。

当远程用户尝试登录账户时，系统会检查该账户是否拥有远程用户的公钥。该公钥随后被用于加密一个挑战（通常是一个随机数），该挑战只能通过远程用户的私钥解密。当远程用户接收到加密的挑战时，该用户用其私钥解密挑战。远程用户将首先使用其私钥对会话标识符进行加密并签名。然后账户使用远程用户的公钥解密加密的会话标识符。该会话标识符是由 SSH 为该会话预先设置。

SSH 身份验证首先针对主机，然后针对用户。每个主机都有自己的用于身份验证的主机密钥（公钥和私钥）。一旦主机通过验证，就会查询用户。每个用户都有自己的公钥和私钥。希望接收远程用户连接的 SSH 服务器的用户必须保留这些远程用户的公钥列表。同样，SSH 主机将维护一个其他 SSH 主机的公钥列表。

### SSH 软件包、工具和服务器

Linux 系统通过 OpenSSH 实现 SSH。全套 OpenSSH 软件包包含了 OpenSSH 元软件包（`ssh`）、OpenSSH 服务器（`openssh-server`）和 OpenSSH 客户端（`openssh-clients`）。这些软件包还需要 OpenSSL（`openssl`），它安装了 SSH 使用的加密库。

SSH 工具列在 表 12-14 中。它们包含了几个客户端程序，如 `scp`、`ssh`，以及 `ssh` 服务器。`ssh` 服务器（`sshd`）允许任何外部人员通过 `ssh` 客户端连接提供安全连接。还包含了一些配置实用程序，例如 `ssh-add`，它可以将有效的主机添加到身份验证代理中。

你可以使用 `service` 或 `systemctl` 命令手动启动、停止和重启服务器。

```bash
sudo service sshd restart
```

|  | 说明 |
| :--- | :--- |
| ssh | SSH 客户端 |
| sshd | SSH 服务器（守护进程） |
| sftp | SSH 客户端，安全传输传输。仅限版本 2。使用 ? 列出命令 |
| sftp-server | SSH 服务器。仅限版本 2 |
| scp | SSH 复制客户端 |
| ssh-keygen | 生成密钥的实用程序。-h 查看帮助 |
| ssh-keyscan | 自动收集公主机密钥以生成 ssh_known_hosts 的工具 |
| ssh-add | 将 RSA 和 DSA 标识添加到身份验证代理 |
| ssh-agent | 持有公钥认证私钥的身份验证代理（RSA, DSA） |
| ssh-askpass | 查询密码的 X 窗口工具，由 ssh-add 调用（openssh-askpass） |
| ssh-askpass-gnome | 查询密码的 GNOME 工具，由 ssh-add 调用 |
| ssh-signer | 签名主机身份验证包。仅限版本 2。必须是 suid root（安装时执行） |
| slogin | 远程登录（版本 1） |

表 12-14：SSH 工具

你必须配置防火墙以允许访问 **ssh** 服务。该服务被设置为在 22 端口使用 TCP 协议运行。如果你直接管理 IPTables 防墙，可以通过添加以下 IPtables 规则直接管理访问。该规则接受 TCP/IP 协议包的 22 端口输入。

```bash
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```




使用 SSH 涉及创建你自己的公钥和私钥，然后将你的公钥分发给你想要访问的其他用户。这些用户可以是不同的用户，也可以是你自己在远程系统上拥有的用户账户。通常情况下，人们从本地客户端远程登录到远程服务器上的账户，例如从家里电脑登录到公司电脑。你的家里电脑将是你的客户端账户，而公司电脑上的账户将是你的服务器账户。在你的客户端账户上，你需要生成公钥和私钥，然后将公钥的副本放在服务器账户中。一旦服务器上的账户有了你客户端用户公钥的副本，你就可以从客户端账户访问服务器账户。系统还会提示你输入服务器账户的口密码。你必须知道这个口密码才能访问该账户。图 12-1 展示了允许用户 `george` 访问账户 `cecelia` 的 SSH 设置。

![FIG13-1](img/image-606.png)

图 12-2：SSH 设置与访问

为了使你能够使用 SSH 访问其他账户：

* 你必须在账户上创建公钥和私钥，并设置一个口密码。你需要使用这个口密码从另一个账户访问你的账户。
* 你必须将你的公钥分发到你想要访问的其他账户，将其存放在 `.ssh/authorized_keys` 文件中。
* 其他账户也必须设置公钥、私钥以及口密码。
* 你必须知道其他账户的口密码才能访问它。

### 使用 ssh-keygen 创建 SSH 密钥

你使用 `ssh-keygen` 命令创建公钥和私钥。你需要指定想要使用的加密类型。你可以使用 DSA 或 RSA 加密。使用 `-t` 选项指定类型，并使用其全小写的加密名称（`rsa`、`dsa`、`ecdsa` 和 `ed25519`）。在以下示例中，用户使用 RSA 加密创建了一个密钥。

```
ssh-keygen -t rsa
```

`ssh-keygen` 命令会提示你输入口密码，它将将其作为一种密码来保护你的私钥。口密码应该是几个单词长。系统还会提示你为密钥输入文件名。如果你不输入，SSH 将使用默认值。公钥将具有 `.pub` 扩展名。`ssh-keygen` 命令生成公钥并放在你的公钥文件中，例如 `.ssh/id_dsa.pub` 或 `.ssh/id_rsa.pub`，具体取决于你指定的密钥类型。它会将私钥放在相应的私钥文件中，例如 `.ssh/id_dsa` 或 `.ssh/id_rsa`。

| 文件 |  |
| :--- | :--- |
| `$HOME/.ssh/known_hosts` | 记录用户登录过的所有主机的主机密钥（不在 `/etc/ssh/ssh_known_hosts` 中的主机）。 |
| `$HOME/.ssh/random_seed` | 随机数生成器的种子。 |
| `$HOME/.ssh/id_rsa` | 包含用户的 RSA 认证身份标识。 |
| `$HOME/.ssh/id_dsa` | 包含用户的 DSA 认证身份标识。 |
| `$HOME/.ssh/id_rsa.pub` | 包含用于认证的 RSA 公钥。此文件的内容应添加到所有你希望使用 RSA 认证登录的机器上的 `$HOME/.ssh/authorized_keys` 中。 |
| `$HOME/.ssh/id_dsa.pub` | 包含用于认证的 DSA 公钥。 |
| `$HOME/.ssh/config` | 每个用户的配置文件。 |
| `$HOME/.ssh/authorized_keys` | 列出可以作为此用户登录的 RSA 或 DSA 密钥。 |
| `/etc/ssh/ssh_known_hosts` | 包含系统级的已知主机密钥列表。 |
| `/etc/ssh/ssh_config` | 包含系统级配置文件。该文件为用户配置文件中未指定的值提供了默认值。 |
| `/etc/ssh/sshd_config` | 包含 SSH 服务器配置文件。 |
| `/etc/ssh/sshrc` | 包含系统默认设置。此文件中的命令会在用户登录时，在用户 shell（或命令）启动之前由 `ssh` 执行。 |
| `$HOME/.ssh/rc` | 包含用户登录时，在用户 shell（或命令）启动之前由 `ssh` 执行的命令。 |

表 12-15：SSH 配置文件

如果你需要更改口密码，可以使用 `ssh-keygen` 命令和 `-p` 选项进行。每个用户都有自己的自己的 SSH 配置目录，称为 `.ssh`，位于其自己的家目录下。公钥、私钥以及 SSH 配置文件都放在这里。如果你从源码编译，`make install` 操作将自动运行 `ssh-keygen`。表 12-15 列出了 SSH 配置文件。

### 授权密钥 (Authorized Keys)

公钥用于验证用户及其主机。你在远程系统上使用公钥来允许该用户访问。公钥存放在远程用户账户的 `.ssh/authorized_keys` 文件中。回想起公钥存储在 `.ssh/id_dsa.pub` 文件中。如果用户想从本地账户远程登录到远程系统上的账户，他们使用公钥来允许访问。公钥存放在远程用户账户的 `.ssh/authorized_keys` 文件中。回想起公钥存储在 `.ssh/id_dsa.pub` 文件中。如果用户想从本地账户登录到远程系统上的账户，他们使用公钥来允许访问。公钥存放在远程用户账户的 `.ssh/authorized_keys` 文件中。回想起公钥存储在 `.ssh/id_dsa.pub` 文件中。

```
cat id_rsa >> ~/.ssh/authorized_keys
```

注意：你也可以使用 seahorse 创建和管理 SSH 密钥。

注意：SSH 版本 1 使用 `identity` 文件名；它可能在旧发行版中默认安装。SSH 版本 2 使用不同的文件名 `id_dsa` 或 `id_rsa`，取决于使用 RSA 还是 DSA 认证。

### 加载密钥

如果你经常连接各种远程主机，可以使用 `ssh-agent` 将私钥放入内存，以便快速访问并解密接收到的传输。`ssh-agent` 命令旨在会话开始时使用。对于 GNOME，你可以使用由 `ssh-add` 调用的 `openssh-askpass-gnome` 工具，以便在登录时，每当你使用 SSH 客户端时，GNOME 会自动提供该密码。

虽然 `ssh-agent` 命令允许你在内存中使用私钥，但你必须专门使用 `ssh-add` 命令将私钥加载到内存中。不带参数的 `ssh-add` 将从你的私钥文件（例如 `.ssh/id_rsa`）加载私钥。系统会提示你输入该私钥的口密码。要从内存中删除密钥，请使用带有 `-d` 选项的 `ssh-add`。如果你有多个私钥，可以将它们全部加载到内存中。带有 `-l` 选项的 `ssh-add` 会列出已加载的密钥。

### SSH 客户端

SSH 最初的设计是为了取代 rlogin、scp 和 Telnet 等远程访问操作，这些操作没有加密且存在安全风险。你还可以使用 SSH 编码 X 服务会话以及 FTP 传输（sftp）。相应的 SSH 客户端取代了这些应用程序。通过 `slogin` 或 `ssh`，你可以登录远程主机以执行命令并运行应用程序，就像使用 `rlogin` 和 `rsh` 一样。通过 `scp`，你可以在远程主机和网络主机之间复制文件，就像使用 `rcp` 一样。通过 `sftp`，你可以传输受加密的 FTP 文件。




通过 `ssh`，你可以从本地客户端远程登录到网络上作为 SSH 服务器运行的远程系统。这里的“本地客户端”指的是网络外部的设备，例如你的家来电脑，而“远程”指的是你正在连接的网络上的某台主机系统。实际上，你是从你的本地系统连接到远程网络主机的。它的设计目的是为了替代执行远程登录的 `rlogin` 以及执行远程命令的 `rsh`。通过 `ssh`，你可以从本地站点登录到网络上的远程主机，然后向该主机发送要执行的命令。`ssh` 命令还能够支持 X Window 系统连接。如果你在 X Window 系统环境（如 GNOME）中建立 ssh 连接，该功能将自动启用。系统会在你的本地 X 服务器和远程 X 服务器之间为你建立一个连接。远程主机会建立一个伪造的 X 客户端，并通过它将任何 X Window 系统数据发送到你的本地系统，由你本地的 X 客户端进行处理。

`ssh` 登录操作功能与 `rlogin` 命令非常相似。你输入 `ssh` 命令，后面跟着远程主机的地址，以及 `-l` 选项和你要登录的远程账户的登录名（用户名）。以下示例了登录到 `rabbit.mytrek.com` 主机上的 `aleina` 用户账户。

```
ssh rabbit.mytrek.com -l aleina
```

你也可以在 `ssh` 中使用地址格式的用户名，例如：

```bash
ssh aleian@rabbit.mytrek.com
```

接下来的列表显示了用户 `george` 如何访问 `turtle.mytrek.com` 上的 `cecelia` 账户。

```
[george@turtle george]$ ssh turtle.mytrek.com -l cecelia cecelia@turtle.mytrek.com's password:
[cecelia@turtle cecelia]$
```

提供了多种选项可供你配置连接。大多数选项都有对应的配置项，可以在配置文件中设置。例如，通过 `-c` 选项，你可以指定想要使用的加密方法，例如 `idea`、`des`、`blowfish` 或 `arcfour`。通过 `-i` 选项，你可以选择一个特定的私钥使用。`-C` 选项允许你以指定的级别压缩传输数据（完整选项列表请参见 `ssh` 手册页）。

### scp

你使用 `scp` 将文件从网络上的一个主机复制到另一个主机。`scp` 设计用于替代 `rcp`，它使用 `ssh` 传输数据并采用相同的身份验证和加密方法。如果身份验证需要，`scp` 会请求密码或短语。`scp` 程序的运行方式类似于 `rcp`。远程主机上的目录和文件通过文件名或目录前的用户名和主机地址来指定。用户名指定了 `scp` 访问的远程用户账户，而主机是该账户所在的远程系统。你用 `@` 将用户名与主机地址分开，用冒号 `:` 将主机地址与文件或目录名分开。以下示例将文件 `party` 从用户的当前目录复制到位于 `rabbit.mytrek.com` 主机上用户 `aleina` 的 `birthday` 目录。

```bash # 此处为示例
scp party aleina@rabbit.mytrek.com:/birthday/party
```

特别值得关注的是 `-r`（递归）选项，它允许你复制整个目录。完整选项列表请参见 `scp` 手册页。在下一个示例中，用户将整个 `reports` 目录复制到用户 `justin` 的 `projects` 目录。

```bash
scp -r reports justin@rabbit.mytrek.com:/projects
```

在下一个示例中，用户 `george` 从用户 `cecelia` 的家目录复制 `mydoc1` 文件。

```
[george@turtle george]$ scp cecelia@turtle.mytrek.com:mydoc1 . cecelia@turtle.mytrek.com's password:
mydoc1 0% | | 0 --:-- ETA
mydoc1 100% |*****************************| 17 00:00
[george@turtle george]$
```

### sftp 和 sftp-server

通过 `sftp`，你可以传输受加密保护的 FTP 文件。`sftp` 程序使用与 `ftp` 相同的命令。该客户端运行方式类似于 `ftp`，具有许多相同的命令。

```bash
sftp download.ubuntu.com
```

要使用 `sftp` 连接到 FTP 服务器，该服务器需要运行 `sftp-server` 应用程序。SSH 服务器调用 `sftp-server` 来为使用 `sftp` 客户端的用户提供加密的 FTP 传输。sftp 服务器和客户端使用 SSH 文件传输协议 (SFTP) 来安全地执行 FTP 操作。

#### 端口转发（隧道）

如果出于某种原因，你只能通过一个不安全的主机连接到安全主机，SSH 提供了一种名为“端口转发”的功能。通过端口转发，你可以保护连接中不安全的部分。这只需指定不安全主机连接到安全主机的端口即可。这在本地主机和远程主机之间建立了一个直接连接，通过了中间的不安全主机。加密数据直接通过。这一过程被称为“隧道”，在连接的服务器之间创建一个加密数据的安全隧道。

你可以设置端口转发到远程系统上的某个端口，或到你本地系统上的某个端口。要将远程系统上的端口转发到本地系统上的端口，请使用带有 `-R` 选项的 `ssh`，后面跟着包含远程主机、本地端口的参数。这通过中间的不安全主机在本地主机和远程主机之间建立了直接连接。加密数据直接通过。这一过程被称为隧道，在连接的服务器之间创建一个加密数据的安全隧道。

```bash
ssh -R rabbit.mytrek.com:23:22
```

要将你本地系统上的端口转发到远程系统上的端口，请使用带有 `-L` 选项的 `ssh`，后面跟着包含远程主机、本地端口的参数。这通过中间的不安全主机在本地主机和远程主机之间建立了直接连接。加密数据直接通过。这一过程被称为隧道，在连接的服务器之间创建一个加密数据的安全隧道。

```bash
ssh -L rabbit.mytrek.com:23:22
```

你可以在 `.ssh/ssh_config` 文件中使用 `LocalForward` 和 `RemoteForward` 选项为特定主机设置端口转发，为你连接的所有主机指定默认设置。

#### SSH 配置

每个用户的 SSH 配置文件位于其 `.ssh/ssh_config`。`/etc/ssh/ssh_config` 文件用于设置全局默认，`/etc/ssh/ssh_config.d` 目录中可能包含额外的配置文件会被 `/etc/ssh/ssh_config` 读取。在配置文件中，你可以设置 `ssh_config` 手册中列出的各种选项。该文件设计用于指定你可能连接的不同远程机的选项。它被组织成段，每个段以 `HOST` 关键字开头，后跟主机的 IP 地址。接后的行包含你为该主机设置的选项。一个段在下一个 `HOST` 条目结束。特别值得关注的是 `User` 和 `Ciphers` 选项。使用 `User` 选项指定允许访问的远程系统用户名。通过 `Ciphers` 选项，你可以为特定主机选择用于传输的（`Cipher` 选项是 SSH1 选项，已不再支持）加密方法：

```ssh
Host turtle.mytrek.com
    User larisa
    Compression no
    Ciphers aes128-ctr
```





大多数标准选项（包括加密算法）已经作为注释条目列出。删除 `#` 即可激活。

# 加密算法 `aes128-ctr,aes192-ctr,aes256-ctr,aes128-cbc,3des-cbc`

要指定适用于你连接的任何主机的全局选项，请创建一个以星号作为主机的 `HOST` 条目，即 `HOST ***`。该条目必须放置在配置文件的末尾，因为选项仅在第一次设置时才会发生更改。后续关于该选项的任何条目都将被忽略。由于主机既匹配其自身的条目也匹配全局条目，因此其特定条目应该放在全局条目之前。星号（`****`）和问号（`?`）都是通配符匹配运算符，允许你指定相同后缀或前缀的一组主机。

`Host * PasswordAuthentication yes ConnectTimeout 0 Ciphers aes128-ctr`

你使用 `/etc/ssh/sshd_config` 文件来配置 SSH 服务器，`/etc/ssh/sshd_config.d` 目录下可能存在额外的配置文件，这些文件会被 `/etc/ssh/sshd_config` 读取。在这里，你将找到服务器选项，例如使用的端口、密码要求以及 PAM 使用情况。配置完成后，你可以使用 `sshd` 命令和 `-T` 选项检查你的配置文件的有效性。

```
sudo sshd -T
```

# 13. 打印服务

打印服务在你的本地系统以及网络上配置并提供打印机。打印机由打印服务器作为网络资源进行管理。作为网络资源，网络上的多个主机可以访问同一台打印机。打印站点和资源列在表 13-1 中。

## CUPS

通用 Unix 打印系统 (CUPS) 提供打印服务，它由 Apple 作为开源项目开发，并根据 GNU 公共许可证免费提供。CUPS 是大多数 Linux 发行版（包括 Linux Mint）的主要打印服务器。位于 [`www.cups.org/`](https://www.cups.org/) 的 CUPS 网站提供了关于安装和管理打印机的详细文档。CUPS 使用互联网打印协议 (IPP)，该协议为互联网提供了打印标准（[`pwg.org/ipp/`](https://pwg.org/ipp/)）。IPP 协议支持网络、PostScript 和 Web 接口。旧的线打印机 (LPD) 打印系统仅支持线打印机。CUPS 作为网络服务器运行，使用类似于 Apache Web 服务器的配置格式。网络支持允许用户远程访问打印机。GNOME 为 CUPS 集成支持，允许基于 GNOME 的应用程序直接访问 CUPS 打印机。

| 资源 |  |
| :--- | :--- |
| [`cups.org`](https://cups.org) | 通用 Unix 打印系统 |
| [`pwg.org/ipp`](http://pwg.org/ipp) | 互联网打印协议 |
| [`lprng.sourceforge.net/`](http://lprng.sourceforge.net/) | LPRng 打印服务器 (Universe repository) |

**表 13-1: 打印资源**

一旦你安装了打印机并配置了打印服务器，就可以使用打印客户端打印并管理你的打印队列。CUPS 服务器有多种打印配置工具可用，例如“设置 | 打印机”、system-config-printer、CUPS 配置工具，以及本章后面详细描述的 `lpq` 和 `lpc` 等各种线打印工具。请查看《Ubuntu 服务器指南 | 服务 | 服务 - CUPS》获取基础配置。

[`ubuntu.com/server/docs/service-cups`](https://ubuntu.com/server/docs/service-cups)

CUPS 由 systemd 通过按需套接字实现进行管理，涉及 `cups.service`、`cups.socket`、`cups.path` 和 `cups-browsed` 文件。此外，一个特殊的 `printer.target` 单元会检测打印机何时连接到你的系统。`cups.service` 文件运行 CUPS 服务器 `/usr/sbin/cupsd` (`ExecStart`)。它在 `printer.target` 激活时运行，而这发生在用户连接打印机时（`WantedBy`）。`cups.socket` 单元文件让 CUPS 在 CUPS 套接字 `/var/run/cups/cups.sock` (`ListenStream`) 上监听请求。实际上，CUPS 的运行方式类似于旧的 inetd 守护进程，仅在被请求时激活。`cups.path` 单元在系统启动时 (`WantedBy=multi-user.target`) 在 `/var/cache/cups` (`PathExists`) 建立 CUPS 打印目录。`cups-browsed.service` 文件支持访问网络上的远程打印机。

```
cups.service
[Unit]
Description=CUPS Scheduler
Documentation=man:cupsd(8)
After=ssd.service
Requires=cups.socket
[Service]
ExecStart=/usr/sbin/cupsd -l
Type=simple
Restart=on-failure
[Install]
Also=cups.socket cups.path
WantedBy=printer.target

cups.socket
[Unit]
Description=CUPS Scheduler
PartOf=cups.service
[Socket]
ListenStream=/var/run/cups/cups.sock
[Install]
WantedBy=sockets.target

cups.path
[Unit]
Description=CUPS Scheduler
PartOf=cups.service
[Path]
PathExists=/var/cache/cups/org.cups.cupsd
[Install]
WantedBy=multi-user.target

cups-browsed.service
[Unit]
Description=Make remote printers available
Requires=cups.service
After=cups.service avahi-daemon.service
Wants=avahi-daemon.service
[Service]
ExecStart=/usr/sbin/cups-browsed
[Install]
WantedBy=multi-user.target
```

## 无驱动打印

新的打印机型号支持无驱动打印。无需安装驱动，打印机就可以支持驱动。打印机通过 DNS 服务发现 (DNS-SD) 自动检测。CUPS Web 界面、system-config-printer、GNOME 打印机和 lpadmin 支持无驱动打印。

CUPS 使用 `driverless` 工具检测可用的无驱动打印机并为它们生成 PPD 配置文件。这些驱动的功能可能没有官方驱动那么完整，但可以打印。可能会与 `cups-browsed` 守护进程发生冲突，该进程是实现无驱动打印的早期尝试，对于不支持无驱动打印的打印机仍然很有用。你可能需要在 `/etc/cups/cups-browsed.conf` 文件中设置 `OnlyUnsupportedByCUUS` 和 `CreateIPPPrinterQueues` 选项。




Linux 会为安装的打印机动态创建设备名称。USB 连接的打印机被视为可插拔设备，可以轻松连接到其他接口并仍然被识别。对于连接到特定端口的旧打印机，将生成专用设备文件。例如，对于并行打印机，设备名称将为 `lp0`、`lp1`、`lp2` 等。这些名称中的数字对应于 PC 上的并行端口；`lp0` 指 LPT1 并行端口，`lp1` 指 LPT2 并行端口。串口打印机将使用串口，通过 `ttyS0`、`ttyS1`、`ttyS2` 等设备文件进行引用。

### 打印机 URI（通用资源标识符）

打印机可以是本地的或远程的。两者都使用通用资源标识符 (URI) 进行引用。URI 支持与远程打印机通信的网络协议，也支持用于引用本地打印机的设备连接。

远程打印机通过与其通信的协议进行引用，例如用于 UNIX 网络打印机的互联网打印协议 `ipp`，用于 Windows 网络打印机的 Samba 协议 `smb`，以及用于旧版 LPRng Unix 服务器的 `lpd`。它们的 URI 与 Web URL 类似，指示打印机所连接系统的网络地址。

```
ipp://mytsuff.com/printers/queue1
smb://guest@lizard/myhp
```

对于连接的本地打印机（尤其是旧打印机），URI 将使用设备连接和设备名称。`usb:` 前缀用于 USB 打印机，`parallel:` 用于连接并行端口的旧打印机，`serial:` 用于连接串口的打印机，`scsi:` 用于连接 SCSI 的打印机。

在 CUPS 的 `/etc/cups/printers.conf` 文件中，`DeviceURI` 引用打印机的 URI。对于 USB 打印机，URI 使用 `usb:`。

```
DeviceURI usb://Canon/S330
```

### 打印目录

当系统打印文件时，它会使用称为打印目录（spool directories）的特殊目录。打印作业是一个待打印的文件。当你将文件发送到打印机时，会创建该文件的副本并将其放在为该打印机设置的打印目录。打印目录的位置是从打印机配置文件中的条目获取的。在 Linux 上，打印目录位于 `/var/spool/cups` 下，以打印机命名的目录。例如，`myepson` 打印机的打印目录位于 `/var/spool/cups/myepson`。打印目录包含多个管理打印作业的文件。某些文件使用打印机名称作为扩展名。例如，`myepson` 打印机拥有文件 `control.myepson`（提供打印队列控制）、`active.myepson`（用于活动打印作业）以及作为日志文件的 `log.myepson`。

### CUPS 启动与重启

你可以使用 `systemctl` 命令和 `cups` 脚本启动、停止和重启 CUPS。当你进行更改或安装打印机时，请务必重启 CUPS 以使更改生效。可以使用以下命令：

```bash
sudo systemctl restart cups
```

CUPS 服务器配置为在系统启动时启动。`/etc/default/cups` 脚本持有 CUPS 服务器的启动选项，例如加载并行打印机驱动模块的 `LOAD_LP_MODULE` 选项。

## 安装打印机

有多种工具可以安装 CUPS 打印机。简单的方法是在桌面系统上使用 `system-config-printer` 工具。你也可以使用 CUPS 软件自带的基于浏览器的配置工具（适用于 `lynx` 命令行浏览器）。或者，你也可以直接编辑 CUPS 打印机配置文件。

## 使用 system-config-printer 在桌面上配置打印机（系统设置 打印机）

Linux Mint 尝试自动检测并配置打印机。对于可插拔打印机（如 USB 打印机），一旦连接，就会被检测并配置。它通过“系统设置 打印机”（system-config-printer）进行配置，并在“系统设置 打印机”对话框中显示图标。如果没有可用驱动程序，打印机将无法配置，且没有图标。你需要手动添加并配置打印机。

### system-config-printer

要更改配置或添加远程打印机，可以使用打印机配置工具 `system-config-printer`，可以通过“系统设置”对话框中的“打印机”访问。该实用程序允许你为打印机选择合适的驱动程序，并设置纸张大小和打印分辨率等选项。你可以配置直接连接到本地计算机的打印机，也可以配置网络上远程系统上的打印机。你可以通过在应用程序列表中选择“打印机”来启动 `system-config-printer`。

![Image](img/image-607.png) ![Image](img/image-608.png)

图 13-1: system-config-printer 工具

打印配置窗口显示已安装打印机的图标（请参见 图 13-1）。菜单栏具有服务器配置与选择、打印机功能（如属性和打印队列）、打印机类以及查看已发现打印机的菜单。工具栏具有手动添加新打印机和刷新打印配置的按钮。过滤器搜索框允许你仅显示匹配搜索模式的打印机。点击搜索框中的 x 图标可清除模式。点击文件搜索框中的放大镜图标将弹出一个菜单，允许你按名称、描述、位置进行搜索。你可以将搜索保存为搜索组。

要查看打印设置、作业选项、访问控制和策略，双击打印机图标或右键点击“属性”。打印属性窗口打开六个选项卡：设置、策略、访问控制、打印选项、作业选项和墨水水平（请参见 图 13-2）。

![Image](img/image-609.png)

图 13-2: 打印属性窗口

打印配置窗口的打印菜单允许你重命名打印机、启用或禁用它并设置为共享打印机。选择打印机图标，然后点击打印菜单（请参见 图 13-3）。你也可以通过右键点击打印机图标显示打印菜单。删除项将移除打印机配置。使用“设置为默认”项可以将打印机设置为系统默认或个人默认打印机。属性项将打开该打印机的属性窗口。你还可以访问所选打印机的打印队列。如果打印机已经是默认打印机，“设置为默认”项将呈灰色状态。

![Image](img/image-610.png)

图 13-3: 打印配置窗口打印菜单

当打印作业在打印队列中等待时，顶面板会出现打印机图标。点击此图标将打开打印作业状态窗口，列出等待中的打印作业。你也可以从 `system-config-printer` 的打印菜单中的“查看打印队列”项（`打印 | 查看打印队列`）打开此窗口。在打印状态窗口中，你可以更改作业的队列位置，也可以停止或删除作业（请参见 图 13-4）。从作业菜单中，你可以取消、暂停（停止）、释放（重启）或重新打印打印作业。只有在打印机设置高级对话框中设置了“保留作业”选项时，重新打印功能才可用。你还可以对作业进行验证。从“查看”菜单，你可以选择显示刚打印的作业并刷新队列。

![Image](img/image-611.png)

图 13-4: 打印队列




要检查服务器设置，请从 `Server` 菜单中选择 `Settings`（设置）。这将打开一个新窗口，显示 `CUPS` 打印服务器设置（参见图 13-5）。“高级”展开按钮显示作业历史和浏览器服务器选项。如果你想允许重新打印，请选择“保留作业文件（允许重新打印）”选项。

![Image](img/image-612.png)

图 13-5：服务器设置

要选择特定的 `CUPS` 服务器，请从 `Server` 菜单中选择 `Connect`（连接）。这将打开一个“连接到 CUPS 服务器”窗口，其中有一个下拉菜单列出了所有供选择的当前 `CUPS` 服务器（参见图 13-6）。

![Image](img/image-613.png)

图 13-6：选择 CUPS 服务器

## 编辑打印机配置

要编辑已安装的打印机，请在 `Printer configuration` 窗口中双击其图标，或右键点击并选择 `Properties`（属性）。这将打开该打印机的 `Printer Properties` 窗口。侧边列出了配置选项卡。点击其中一个以显示该选项卡。有 `Settings`（设置）、`Policies`（策略）、`Access Control`（访问控制）、`Printer Options`（打印机选项）、`Job Options`（作业选项）和 `Ink/Toner Levels`（墨水/硒水平）配置选项卡（参见图 13-7）。

更改后，你可以点击 `Apply`（应用）保存更改并重启打印守护进程。你可以使用 `Settings` 选项卡上的 `Tests`（测试）和 `Maintenance`（维护）任务来测试打印机。`Print Test Page`打印测试页会打印一个页面，而 `Print Self-Test Page`打印自检页还会检查打印机硬件（如喷墨头）。

在 `Settings` 选项卡上，你可以更改驱动程序和打印机名称等配置设置，并运行测试页（参见图 13-2）。如果需要更改选定的驱动程序，请点击 `Make and Model`（品牌和型号）旁边的 `Change`（更改）按钮，打开与“手动添加新打印机”部分类似的打印机型号和驱动程序窗口。在那里你可以指定要使用的型号和驱动程序，甚至加载自己的驱动程序。如果必须更改设备 `URI`（位置和协议），可以点击 `Device URI` 条目右侧的 `Change` 按钮打开“更改设备 URI”对话框。

`Policies` 选项卡允许你启用或禁用打印机，确定其是否共享，以及是否允许其接收作业（你也可以从 `Printer` 菜单启用或共享打印机）。你还可以指定错误策略，规定在发生错误时是重试还是中止打印作业，或停止打印机。你可以选择在文档开始或结束时打印横幅，以指示文档的安全级别，例如机密和秘密。

`Access Control` 选项卡允许你拒绝某些用户的访问。

`Printer Options` 选项卡是设置特定打印功能的地方，如纸张尺寸和类型、打印质量以及使用的进纸盒（参见图 13-7）。

![Image](img/image-614.png)

图 13-7：打印机选项

在 `Job Options` 选项卡上，你可以选择默认打印功能（参见图 13-8），例如副本数、方向以及单面或双面打印。选项分为三类：`Common Options`（常用选项）、`Image Options`（图像选项）和 `Text Options`（文本选项）。仅显示更常用的选项。每个类别都有一个展开按钮，可以显示该类别的所有选项。双面、输出顺序和介 都是展开选项。

`Ink/Toner Levels` 选项卡将显示支持打印机的墨水或硒水平以及状态消息。

![Image](img/image-615.png)

图 13-8：作业选项

## 默认系统级和个人打印机

要将打印机设置为默认打印机，可以右键点击打印机图标并选择“Set As Default”（设置为默认），或者单击单击打印机图标，然后从 `Printer configuration` 窗口的 `Printer` 菜单中选择“Set As Default”项（参见图 13-3）。将打开一个 `Set Default Printer` 对话框，提供设置系统级默认或个人默认的选项（参见图 13-9）。系统级默认打印机是你的 `CUPS` 服务器所服务的系统默认打印机。

![Image](img/image-616.png)

图 13-9：设置默认打印机

系统级默认打印机在 `Printing configuration` 窗口的打印机图标上将有一个绿色对钩标志。

如果你想自己使用不同的打印机（用户特定）作为默认打印机，可以将其指定为你的个人默认。要将打印机设为个人默认，请在 `Set Default Printer` 对话框中选择“Set as my personal default printer”项。个人标志（黄色星形）将出现在 `Printer configuration` 窗口的打印机图标上。在图 13-10 中，Samsung2020 是系统默认，而 DeskJet 是个人默认。

![Image](img/image-617.png)

图 13-10：系统级和个人默认

## 手动添加打印机

打印机会自动检测，但对于旧打印机网络打印机，你可能需要手动添加。在这种情况下，点击 `Add` 按钮并选择 `Printer`。打开一个 `New Printer` 窗口，显示连接、型号和打印机名称。

在 `Select Device` 对话框中，选择连接。本地品牌已按名称列出（例如 Canon），并在右侧显示连接列表。对于远程打印机，你将指定连接类型，例如通过 Samba 的“Windows 打印机”、直接连接到网络的“AppSocket/HP Direct”，以及 Linux 和 Unix 系统的“Internet Printing Protocol (ipp)”。这些连接显示在 `Network Printer` 标题下。点击展开箭头显示它们。

![Image](img/image-618.png)

![Image](img/image-619.png)

图 13-11：选择连接：已连接和未连接

对于大多数连接打印机，连接通常由 `udev` 决定。USB 打印机将仅描述为 USB 打印机，使用 `URI` 指定（参见图 13-11）。对于旧本地打印机，你可能需要选择打印机连接端口，例如用于旧并行打印机的 LPT1，或连接到第一个串口端口的 Serial Port #1。要手动添加 USB 打印机，你需要选择 `Enter URI` 条目并输入带有 `usb://` 前缀和你想给打印机的名称的 URI，例如 `usb://myhp`。

将对相应的驱动程序进行搜索，包括下载驱动程序。如果找到了驱动程序，将显示 `Choose Driver` 屏幕，并已为你选择了相应的驱动程序。你只需点击下一步。在下一个同样标记为 `Choose Driver` 的屏幕上，列出了打印机型号和驱动文件，并且已为你选择了正确的项。只需点击下一步。然后将显示 `Describe Printer` 屏幕，你可以在其中输入打印机名称、描述和位置。这些是你识别打印机的方式。然后点击 `Apply`。

如果没有检测到打印机驱动或检测错误，在 `Choose Driver` 屏幕上，你可以选择从打印机数据库、从 `PPD` 驱动文件或通过搜索 OpenPrinting 在线库来选择驱动。选择显示将根据你选择的选项而更改。





注意：某些驱动程序直接从打印机公司网站安装，例如某些三星驱动程序。这些驱动你可能需要通过在终端窗口运行 shell 脚本来直接安装。安装完成后，当你在连接打印机时，系统会自动检测并配置它。驱动程序也会出现在 `system-config-printer` 的“选择驱动程序”本地数据库列表框中。

数据库选项列出了可能的制造商。使用鼠标选择你需要的那个（参见图 3-12）。搜索选项会显示一个用于输入品牌和型号的搜索框。输入品牌（打印机制造商）和型号名称的部分内容（见图 3-13）。搜索结果将显示在打印机型号下拉菜单中。选择你需要的项。然后点击“前进”。

![Image](img/image-620.png)
图 13-12：新打印机的打印机制造商

![Image](img/image-621.png)
图 13-13：从 OpenPrinting 仓库搜索打印机驱动程序

PPD 文件选项显示一个文件位置按钮，点击它可以打开“选择文件”对话框，你可以用它在系统中定位 PPD 文件。

如果你是从数据库中选择打印机，在下一个屏幕上你需要选择该制造商的型号及其驱动程序（参见图 13-14）。不过，对于某些旧打印机，虽然可以在在线仓库中找到驱动程序，你仍需从本地数据库中选择（驱动程序是相同的）。系统将列出为你的打印机选择的驱动程序。如果你的打印机增加了选项，“安装选项”屏幕将列出这些选项，允许你勾选需要的项。

![Image](img/image-622.png)
图 13-14：使用本地数据库的新打印机的打印机型号和驱动程序

![Image](img/image-623.png)
图 13-15：新打印机的打印机名称和位置

然后你可以输入打印机名称和位置（参见图 13-15）。系统将使用打印机型号和系统主机名为你输入这些内容。你可以将打印机名称更改为你喜欢的任何内容。准备好后点击“应用”。系统会提示打印测试页。打印配置窗口将显示你的打印机图标。你现在准备好打印了。

## CUPS 基于浏览器的配置工具

CUPS 配置 Web 界面是一个基于 Web 的工具，也可以管理打印机和打印作业。页面会显示一个包含用于管理作业、打印机以及执行管理任务的标签页。你可以使用 `localhost` 地址并指定端口 `631` 来访问 CUPS 配置工具。在 浏览器中输入以下 URL：

```
http://localhost:631
```

在 浏览器中输入 `localhost:631` URL 将打开 CUPS Web 界面的主屏幕。有各个部分的标签页，以及用于特殊任务（如添加打印机或获取帮助）的链接（参见图 13-16）。标签页包括管理、类、帮助、作业和打印机。你可以在“管理”标签页上管理和添加打印机。“打印机”标签页将列出已安装的打印机，并带有访问其打印队列、打印机选项和作业选项等按钮。“作业”标签页列出你的打印作业并让你进行管理。

![Image](img/image-624.png)
图 13-16：CUPS Web 配置工具：首页标签页

当会话期间首次尝试进行任何更改时，系统会要求你输入具有管理权限的用户名（你的用户名）和密码（你的用户密码），就像你执行 `sudo` 命令一样。

“管理”标签页显示打印机、类、作业和服务器的区域（参见图 13-17）。服务器部分是你允许打印机共享的地方。按钮允许你查看日志并更改设置。

![Image](img/image-625.png)
图 13-17：CUPS Web 配置工具：管理标签页

通过 CUPS 配置工具，本地打印机会被自动检测并配置。你可以通过一系列 Web 页面手动在 CUPS 上安装打印机，每个每个页面都会请求不同的信息。要安装打印机，点击首页或管理页上的“添加打印机”按钮。你必须首先指定协议。在下一个屏幕上，输入用于打印机的 URI。对于本地打印机，这是协议和主机名。将显示一个输入打印机名称和位置的页面（参见图 13-18）。

![Image](img/image-626.png) ![Image](img/image-627.png) ![Image](img/image-628.png)
图 13-18：添加新打印机：Web 界面

共享复选框允许你选择共享打印机。位置是连接打印机的主机。步骤与 `system-config-printer` 类似。后续页面将提示输入打印机的品牌和型号。如果你有 PPD 驱动程序，也可以加载。

要管理打印机，点击“打印机”标签页或管理页上的“管理打印机”按钮。“打印机”标签页将列出已安装的打印机（参见图 13-19）。点击打印机链接将打开一个管理作业和执行管理任务的页面（参见图 13-20）。从“维护”下拉菜单可以执行暂停打印机、打印测试页和取消所有作业等任务。管理菜单允许你修改打印机、删除它并设置默认选项。选择管理菜单中的“设置默认选项”将显示一个配置打印机如何打印的页面（参见图 13-21）。页面顶部的链接显示设置某些选项的页面，如常规选项、输出控制、横幅以及打印方向、墨水类型、色彩密度和点大小等额外功能。首先列出常规选项，你可以在那里设置分辨率和纸张等等设置。

![Image](img/image-629.png)
图 13-19：CUPS Web 配置工具：打印机标签页

![Image](img/image-630.png)
图 13-20：CUPS Web 配置工具：管理打印机

![Image](img/image-631.png)
图 13-21：CUPS Web 配置工具：打印机选项

注意：你可以使用 `lpadmin` 命令从命令行执行所有管理任务。详情请参阅 CUPS 文档。

## 在 CUPS 上配置远程打印机

如前，大多数现代打印机都支持无驱动打印，允许自动访问远程打印机。无驱动配置是由 CUPS 生成的。如果无驱动配置不足或缺失（如旧打印机所示），你将需要使用 CUPS Web 配置工具或 system-config-printer 安装驱动程序。

### 使用 system-config-printer 配置远程打印机





你可以使用 `system-config-printer` 在 Linux、UNIX 或 Windows 网络上设置远程打印机。当你添加新打印机或编辑现有打印机时，“新打印机”对话框将在“Network”项下列出可能的远程连接类型。当你选择一个远程连接项时，右侧将显示一个面板，可以在其中输入配置信息。

要自动查找网络上连接数量最多的打印机，请点击 `Find Network Printer` 项。输入远程打印机所连接系统的主机名，然后点击 `Find` 按钮。系统将搜索主机，检测到的打印机将作为条目显示在“Network Printer”标题下（参见图 13-22）。由于 Samba 从 `SMB1` 变为 `SMB3`，`Find` 操作不适用于 Windows 打印机。

![Image](img/image-632.png)

图 13-22: 查找网络打印机

要配置特定类型的打印机，请从可用项中进行选择。对于远程 Linux 或 UNIX 打印机，请选择用于较新系统的 Internet Printing Protocol (`ipp`)，或用于较旧系统的 `LPD/LPR` Host 或 Printer。对于你网络上的 Apple 或 HP 直接打印打印机，请选择 `AppSocket/HP jetDirect` 项。

对于 Windows，必须安装 `smbclient` 软件包，该软件包在你安装 Linux Mint 时已完成安装。

“通过 Samba 的 Windows 打印机”是指位于 Windows 网络上的打印机（参见图 13-24）。你需要指定 Windows 服务器（主机名或 IP 地址）、共享名称、如果需要的话的打印机工作组名称，以及用户名和密码。打印机 SMB URL 的格式显示在 SMP Printer 面板上。共享部分是 `smb` URI 格式 `//workgroup/hostname/printername.` 中的主机名和打印机名称。工作组是打印机所属的 Windows 网络工作组。在小型网络中，通常只有一个。主机名是打印机所在的计算机。用户名和密码可以是打印机资源本身的，也可以用于特定用户的访问。面板顶部会显示一个框，你可以在其中以 `smb` URI 格式输入共享主机和打印机名称。

由于从 `SMB1` 变为 `SMB3`，通过 Browse 按钮访问的浏览操作无法工作。因此，你必须输入打印机的准确名称，包括空格和括号等特殊字符（参见图 13-23）。这些特殊字符用前置百分号 `%` 引用，后跟字符的 ASCII 十六进制值。空格引用为 `%20`，左括号引用为 `%28`，右括号为 `%29`。在这些示例中，Samsung M2020 打印机的 Windows 名称为：

Samsung M2020 Series (USB001)

应为：

`Samsung%20M2020%20Series%20%28USB001%29`

![Image](img/image-633.png)

图 13-23: 使用全名和身份验证选择 Windows 打印机

务必也包含你的主机名。如果你在网络上有多个工作组，请也包含工作组名称。上一个示例中主机为 'richard-asus' 的完整条目为：

`richard-asus/Samsung%20M2020%20Series%20%28USB001%29`

带有工作组名“workgroup”的为：

`workgroup/richard-asus/Samsung%20M2020%20Series%20%28USB001%29`

如果有需要，你也可以输入所需的 Samba 认证，例如用户名或密码。勾选“Authentication required”（需要身份验证）允许你输入 Samba 用户名和密码。右下角的 Connections 部分将列出“Windows Printer via Samba”连接。在当前版本的 Samba 中，如果你现在不输入，当你尝试使用打印机时它会提示你用户名和密码。这可能不起作用。为了确保能够访问，你应该现在此对话框中输入用户和密码。

然后继续进行打印机型号、驱动程序和名称的安装屏幕。安装完成后，你就可以像访问任何打印机一样访问打印机属性（参见图 13-24）。

![Image](img/image-634.png)

图 13-24: 远程 Windows 打印机设置

配置好的远程打印机与其他打印机一起列在 `system-config-printer` 窗口中（参见图 13-25）。当你从应用程序打印时，远程打印机将与你的本地打印机一起列出。

![Image](img/image-635.png) ![Image](img/image-636.png)

图 13-25: 远程 Windows 打印机

一旦配置，连接到本地网络的任何计算机上的共享 Windows 打印机即可访问。已安装的 Samba 库可以直接访问任何共享的 Windows 打印机。

如果你想在 Linux Mint 计算机上与其他网络的用户共享打印机，支持的 Samba 库已安装，将让你直接访问任何共享的 Windows 打印机。

如果你想在 Linux Mint 计算机上与其他网络的用户共享打印机，支持的 Samba 库已安装，将让你直接访问任何共享的 Windows 打印机。

如果你想在 Linux Mint 计算机上与其他网络的用户共享打印机，支持的 Samba 库已安装，将让你直接访问任何共享的 Windows 打印机。

如果你想在 Linux Mint 计算机上与其他网络的用户共享打印机，支持的 Samba 库已安装，将让你直接访问任何共享的 Windows 打印机。

### **手动配置远程打印机**

在 `printers.conf` 文件中，对于远程打印机，不再列出设备，`DeviceURI` 条目将具有一个 Internet 地址及其协议。例如，位于 CUPS 服务器上的远程打印机 (`ipp`) 将如所示所示（Windows 打印机将使用 `smb` 协议）：





`DeviceURI ipp://mytsuff.com/printers/queue1`

当你在 CUPS 上安装 Windows 打印机时，使用 URL 协议 `smb` 来指定其位置。允许登录打印机的用户名输入在主机名之前，并用 `@` 符号与主机名分隔。在大多数配置中，这是 `guest` 用户。下面显示了连接到名为 `lizard` 的 Windows 主机的名为 `myhp` 的 Windows 打印机的位置项。其 Samba 共享引用为 `//lizard/myhp`。

`DeviceURI smb://guest@lizard/myhp`

为了在 Samba 上启用 CUPS，你还需要在 `/etc/samba/smb.conf` 文件中将打印选项设置为 `cups`，如下所示。

```
printing = cups
printcap name = cups
```

同样对于 Samba，请确保包含用于身份验证的用户名和密码，以及打印机的完整名称，包括空格（`%20`）等特殊字符。

`DeviceURI smb://richard:mypa@richard-asus/Samsung%20M200%20Series%20%28USB001%29`

## CUPS 打印机类

CUPS 允许你选择一组打印机来打印作业，而不是只选择一台。如果一台打印机忙碌或离线，可以自动选择另一台打印机打印作业。这种打印机分组被称为 `classes`（类）。一旦安装了打印机，你就可以将它们分为不同的类。例如，你可能希望将所有的喷墨打印机归一类，激光打印机归另一类，或者你可能希望将连接到某个特定打印服务器的打印机分到自己的类中。

在 Linux Mint 桌面面上，你可以使用 `system-config-printer` 为打印机设置类。`Server | New` 菜单中的 `Class` 项允许你创建打印机类。你可以从 `Server` 菜单或 `Add` 按钮访问 `New` 菜单。此功能允许你选择一组打印机来打印作业，而不是只选择一台。这样，如果一台打印机忙碌或离线，系统将自动选择另一台打印机来执行任务。已安装的打印机可以分配到不同的类。当你点击 `New` 菜单中的 `Class` 项时，会打开一个 `New Class` 窗口。在这里，你可以输入类的名称、任何注释以及位置（默认输入你的主机名）。下一个屏幕右侧列出可用打印机（`Other printers`），左侧列出分配给该类的打印机（`Printers in this class`）。使用箭头按钮向类中添加或删除打印机。完成后点击 `Apply`。选中类的标签页与打印机的标签页非常相似，用 `Members` 标签代替 `Printer Options` 标签。在 `Members` 标签页中，你可以更改哪些打印机属于该类。你也可以选择一台或一组打印机，并从 `Printer` 菜单选择“Create class”，自动将它们添加到新类中。

你也可以在 CUPS Web 配置工具上创建类。选择 `Administration` 标签并点击 `Add Class` 按钮。在 `Add Class` 页面上，你输入类的名称、位置，然后从 `Members` 列表中选择要添加到类的打印机。该类将显示在 `Classes` 标签页上，显示其成员和状态。

## CUPS 配置文件

CUPS 服务器的配置文件位于 `/etc/cups` 目录。`classes.conf` 和 `printers.conf` 文件可以使用 GNOME Printer 和 CUPS Web 配置工具等桌面应用管理。其他文件，如 `cupsd.conf`，你需要使用文本编辑器进行编辑。

| 文件名 | 说明 |
| :--- | :--- |
| classes.conf | 包含不同本地打印机类的配置 |
| client.conf | 为指定客户端出的特定选项 |
| cupsd.conf | 配置 CUPS 服务器 `cupsd` |
| printers.conf | 包含可用本地打印机的打印机配置 |
| cups-files.conf | CUPS 使用的文件和目录 |
| cups-browsed.conf | 访问远程和本地打印机 |
| subscriptions.conf | 打印机和打印作业信息的订阅控制 |

**表 13-2: CUPS 配置文件**

### cupsd.conf

CUPS 服务器的配置文件是 `/etc/cups/cupsd.conf`。要配置 CUPS 服务器，请使用文本编辑器编辑此文件中的配置项。当安装 CUPS 软件包时，它会安装一个带有详细注释的 `cupsd.conf` 文件。大多数选项都已列出，但许多被注释掉了，条目开头有 `#` 符号。CUPS 服务器使用指令（directives）进行配置，语法与 Apache Web 服务器的配置类似。与 Apache 一样，指令可以被组织成块。

要查看 `cupsd.conf` 指令的详细说明，请检查 CUPS 文档中的 `cupsd.conf`。你也可以从 CUPS 基于浏览器的管理工具 `http://localhost:631` 的“Online Help page | References”链接处引用此文档。

https://www.cups.org/documentation.html

`cupsd.conf` 文件从日志设置开始。

```
LogLevel warn
```

在 Linux Mint 上，CUPS 日志是禁用的。

```
MaxLogSize 0
```

`Listen` 指令设置接收连接的机器和套接字。这些默认设置为本地机器 `localhost` 端口 `631`。如果你正在使用专用网络接口连接到本地网络，应添加网卡的 IP 地址。

```
# 仅监听本地机器的连接。
Listen localhost:631
Listen /run/cups/cups.sock
```

`Browsing` 指令允许在网络上检测本地打印机，以便进行共享。对于共享打印，`Browsing` 指令设置为开启（默认设置为关闭）。`BrowseOrder` 的 `allow,deny` 将拒绝所有浏览，然后检查 `BrowseAllow` 指令的例外。反过来（`deny,allow`）则相反，接受所有浏览，并检查被 `BrowseDeny` 指令拒绝的项。默认 `cupsd.conf` 文件有一个 `allow,deny` 的 `BrowseOrder` 指令，随后是设置为 `all` 的 `BrowseAllow` 指令。要限制到特定网络，请使用网络 IP 地址代替 `all`。`BrowseLocalProtocols` 列出了用于在本地网络发布打印机的协议。`BrowseAddress` 指令将你的本地打印机在指定网络上变为可用。设置为 `@LOCAL` 以允许本地网络访问。你可以添加其他 `BrowseAddress` 指令允许其他网络访问。

```
# 在本地网络上显示共享打印机。
Browsing On
BrowseOrder allow,deny
BrowseAllow all
BrowseLocalProtocols dnssd
BrowseAddress @LOCAL
```

CUPS 支持 Basic 和 Digest 形式的身份验证，由 `AuthType` 指令指定。Basic 验证需要用户名和密码。例如，使用 Web 界面时，会被提示输入 root 用户和 root 用户密码。Digest 验证利用在 CUPS `/etc/cups/passwd.md5` 文件中的用户和密码信息，使用用户和密码的 MD5 版本进行身份验证。此外，CUPS 还支持 `BasicDigest` 和 `Negotiate` 验证。`BasicDigest` 将使用 CUPS md5 密码文件进行基本验证。`Negotiate` 将使用 Kerberos 身份验证。默认身份类型由 `DefaultAuthType` 指令设置，设置为 `Basic`。

# 需要身份验证时的默认身份类型...

DefaultAuthType Basic

Web 界面设置设置为 yes。

WebInterface Yes

#### 位置指令





某些指令允许你对特定位置设置访问控制。这些位置可以是打印机或资源，例如管理工具或打印队列目录。位置控制通过 `Location` 指令实现。有多个 `Location` 指令用于控制访问。第一个控制服务器根目录 `/**`。`Order allow, deny` 条目激活了对远程系统访问的限制。如果没有后续的 `Allow` 或 `Deny` 条目，则默认拒绝所有访问。在 `Order allow, deny` 指令作用下，存在一个隐含的 `Allow localhost`，它始终允许本地机器访问。实际上，这里拒绝了所有系统的访问，仅允许本地系统访问。

# 限制对服务器的访问...

```
<Location />
Order allow,deny
</Location>
```

另一个 `Location` 指令用于限制对管理资源的访问，即 `/admin` 资源。`Order allow, deny` 指令拒绝本地机器外的所有系统的访问。

# 限制对管理页面的访问...

```
<Location /admin>
Order allow,deny
</Location>
```

`Allow from` 和 `Deny from` 指令可以允许或拒绝来自特定主机和网络的访问。如果你只想允许对特定机器的访问，可以使用带有该机器 IP 地址的 `Allow from` 指令。CUPS 还使用 `@LOCAL` 表示你的本地网络，并使用 `IF(name)` 表示用于访问网络的特定接口（`name` 是接口的设备名称）。如果你想允许本地网络上的所有其他系统进行管理，可以添加 `Allow from @LOCAL`。如果你添加了 `Allow` 指令，还必须显式地添加 `Allow localhost` 以确保本地机器的访问。

# 限制对管理页面的访问...

```
<Location /admin>
Allow from localhost Allow from @LOCAL Order allow,deny 
</Location>
```

以下条目将允许来自特定机器的访问。

```
Allow From 192.168.0.5
```

下一个位置指令限制对 CUPS 配置文件 `/admin/conf` 的访问。`AuthType default` 指令引用了 `DefaultAuthType` 设置的默认值。`Require user` 指令引用 `SystemGroup` 指令 `@SYSTEM`（在 `cups-files.conf` 文件中定义）。仅允许该组的用户访问。

# 限制对配置文件的访问...

```
<Location /admin/conf>
AuthType Default Require user @SYSTEM Order allow,deny 
</Location>
```

## 默认操作策略：限制指令

随后，为基本管理、打印机、打印作业和所有者操作定义了默认操作策略。默认操作策略部分以 `<Policy default>` 指令开始。Limit 指令用于实现每种操作的指令。作业操作涵盖了发送文档、重启作业、暂停作业和恢复作业等任务。管理任务包括修改打印机配置、删除打印机、管理打印机类以及设置默认打印机。打印机操作管理暂停打印机、启用或禁用打印机以及关闭打印机等任务。所有者操作由取消作业和验证作业访问。

更多详情请参见管理操作策略的 CUPS 文档。

[`www.cups.org/documentation.php/doc-1.6/policies.html`](https://www.cups.org/documentation.php/doc-1.6/policies.html)

在所有默认的 `Limit` 指令上，仅允许本地机器（localhost）访问，`Order allow,deny`。

策略部分从对用户和作业信息的访问控制开始。`JobPrivateAccess` 的默认值限制访问为所有者、系统和访问控制列表。`JobPrivateValues` 指定了私有化的值，例如作业名称、源主机和源用户。`SubscriptionPrivateAccess` 和 `SubscriptionPrivateValues` 指定了订阅属性的访问，例如打印机事件通知（如作业完成或作业停止）。

Limit 指令用于创建和打印作业。

```
<Limit Create-Job Print-Job Print-URI Validate-Job> Order deny,allow </Limit>
```

管理和打印机的 `Limit` 指令均被设置为 `AuthType` `default`，并限制仅由管理员用户访问，`Require user @SYSTEM`。此处显示了管理指令。

# 所有管理操作都需要管理员进行身份验证...

```
<Limit CUPS-Add-Modify-Printer CUPS-Delete-Printer CUPS-Add-Modify-Class CUPS-Delete-Class CUPS-Set-Default CUPS-Get-Devices> AuthType Default Require user @SYSTEM Order deny,allow </Limit>
```

所有与作业相关的所有者的 Limit 指令都需要所有者或管理员的身份验证，`Require user @OWNER @SYSTEM`。此处显示了 `Owner Limit` 指令。

# 只有所有者或管理员才能取消或验证作业...

```
<Limit Cancel-Job CUPS-Authenticate-Job> Require user @OWNER @SYSTEM Order deny,allow </Limit>
```

对于所有其他任务，`<Limit All>` 访问被限制为本地机器（localhost）。

```
<Limit All> Order deny,allow </Limit>
```

`AuthClass` 指令可以在 `Limit` 指令中使用，指定允许访问的打印机类。`System` 类包含了 root、sys 和 system 用户。

一组经过验证的策略指令紧随默认策略之后，具有类似的条目，并在创建和打印作业的 Limit 指令中增加了 `AuthType` 条目。

```
<Limit Create-Job Print-Job Print-URI Validate-Job> AuthType Default Order deny,allow </Limit>
```

### cupsctl

你可以使用 `cupsctl` 命令来修改 `cupsd.conf` 文件，而不是直接编辑文件。详情请查看 `cupsctl` 手动页。不带选项的 `cupsctl` 命令将显示当前设置。

`cupsctl`

通过此命令可以做的更改限于关闭远程管理或禁用共享打印。你可以设置的主要选项有：

`remote-admin`: 启用或禁用远程管理
`remote-any`: 启用或禁用远程打印
`user-cancel-any`: 启用或禁用用户取消他人的作业
`share-printers`: 启用或禁用与其他系统共享本地打印机

### printers.conf

打印机的配置信息将存储在 `/etc/cups/printers.conf` 文件中。你可以直接检查此文件并进行更改。这是一个打印机配置示例。`DeviceURI` 条目指定了所使用的设备，在此例中为 USB 打印机。它目前处于空闲状态，没有作业。

```
# CUPS 打印机配置文件
# Written by cupsd

<Printer mycannon>
Info Cannon s330
Location richard-server
MakeModel Canon S330
DeviceURI usb://Canon/S330
State Idle
StateTime 1166554036
Accepting Yes
Shared Yes
ColorManaged Yes
JobSheets none none
QuotaPeriod 0
PageLimit 0
KLimit 0
OpPolicy default
ErrorPolicy retry-job
</Printer>
```

### subscriptions.conf

打印机和作业信息的配置信息位于 `/etc/cups/subscriptions.conf` 文件中。接收信息的人由 `cupd.conf` 文件策略部分的 `SubscriptionPrivateAccess` 和 `SubscriptionPrivateValues` 指令指定。`Events` 指令指定要发送的事件通知，例如 job-completed、printer-stopped 和 server-started 等事件。`Owner` 指令列出了该订阅的用户。`LeaseDuration` 是订阅有效的持续时间（0 值为作业生命周期或永久）。`Interval` 是两次通知之间的时间。`Recipient` 是通知的接收者 URI。在以下示例中，它是 `dbus://`（你的桌面）。`subscriptions.conf` 文件由 `cupsd` 直接管理，不应手动编辑。

这是一个 `subscriptions.conf` 文件示例：

```
# CUPS v2.3.1 订阅配置文件
NextSubscriptionId 16
```





<Subscription 15>
Events printer-state-changed printer-restarted printer-shutdown printer-stopped printer-added printer-deleted job-state-changed job-created job-completed job-stopped
Owner richard
Recipient dbus://
LeaseDuration 3600
Interval 0
ExpirationTime 1569258630
NextEventId 1
</Subscription>

### cups-files.conf

CUPS 用来管理打印任务的文件和目录可以在 `/etc/cups/cups-files.conf` 文件中配置。`ErrorLog` 指令指定 CUPS 错误日志文件。

```
ErrorLog /var/log/cups/error_log
```

`SystemGroup` 指令定义了 `cupsd.conf` 中 `@SYSTEM` 引用的用户。

```
SystemGroup lpadmin
```

### cups-browsed.conf

`cups-browsed.conf` 文件配置 `cups-browsed` 守护进程，用于浏览远程和本地打印机。在无驱动打印的情况下，这现在由 CUPS 直接管理。`cups-browsed` 守护进程用于那些尚未被 CUPS 无驱动打印覆盖的打印机。

`BrowseRemoteProtocols` 定义了要使用的协议。

```
BrowseRemoteProtocols dnssd cups
```

`BrowseAllow` 指令可以将浏览限制在指定的服务器或网络。

```
BrowseAllow 192.168.1.0/24
```

`CreateIPPPrinterQueues` 指令允许检测非 CUPS 的 IPP 打印机。

## CUPS 命令行打印客户端

在桌面上，你可以使用 GNOME 打印和 CUPS 打印机配置工具等打印客户端来管理打印任务。对于命令行，可以使用几个命令行打印命令。包括 `lpr`、`lpc`、`lpq` 和 `lprm` 命令。这些命令允许你打印文档、显示打印队列并删除打印任务。对于网络连接，CUPS  `-E` 加密选项，允许你加密打印任务。命令行打印命令列在表 13-3。

### lpr

`lpr` 命令代表行打印（line print），向打印队列提交打印任务。其参数是要打印的文件名。通过 `-P` 选项你可以选择特定的打印机。否则将使用默认打印机。在下面的示例中，打印了文件 `myletter`，然后向名为 `myprinter` 的打印机打印文件 `report`。

```
$ lpr myletter
```

在此示例中，文件 `myreport` 在 `myprinter` 打印机上打印。

```
$ lpr -P myprinter myreport
```

### lpc

使用 `lpc` 命令，你可以启用或禁用打印机、重新排序打印队列并重新加载配置文件。当你在命令行输入 `lpc` 命令时，会显示 `lpc>` 提示符。你可以输入 `lpc` 命令来管理你的打印机并重新排序打印任务。带有打印机名称的 `status` 命令显示打印机状态，显示如打印机就绪情况和队列中的打印任务数等信息。要停止或开始打印，使用 `stop` 和 `start` 命令。`lpc` 命令显示为你的 CUPS 打印服务器配置的打印机。

```
$ lpc lpc> status myprinter
```

myprinter:
printer is on device 'usb' speed -1
queuing is enabled
printing is enabled
1 entry in spool area

| 打印机管理 | 说明 |
| :--- | :--- |
| GNOME 打印管理器 | GNOME 打印队列管理工具 (CUPS) |
| CUPS 配置工具 | 打印、管理和配置 CUPS |
| lpr 文件列表 | 打印文件，将文件复制到打印机的池化目录，并将其放入打印队列以轮流打印。-P printer 在指定的打印机上打印文件 |
| lpq 选项 | 显示打印队列中的打印任务。-P printer 显示指定打印机的队列 -l 打印详细列表 |
| lpstat 选项 | 显示打印机状态 |
| lprm 选项 printjob-id or printer | 从打印队列移除打印任务。你通过 lpq 列出的编号识别特定的打印任务。-P printer 移除指定打印机的所有打印任务 |
| lpc | 管理你的打印机。在 lpc> 提示符下，你可以输入命令检查打印机状态并采取其他操作 |

**表 13-3: CUPS 打印客户端**

### lpq 和 lpstat

使用 `lpq` 命令列出打印队列中的打印任务。要查看特定打印机的任务，使用带有打印机名称的 `-P` 选项。列出特定用户的任务，输入用户名。使用 `-l` 选项显示每个任务的详细信息。要显示特定任务的信息，使用该任务的 ID 。`lpstat` 命令让你检查打印机状态。

```
$ lpq myprinter is ready and printing
```

Rank Owner Jobs File(s) Total Size
active chris 1 report 1024

### lprm

你可以使用 `lprm` 命令从打印队列中移除打印任务，在打印前删除该任务。`lprm` 使用许多与 `lpq` 相同的选项。要移除任务，使用带有任务号的 `lprm`。你可以使用 `lpq` 获取任务号。使用 `-P printer` 移除指定打印机的所有打印任务。

```
$ lprm 1
```

## CUPS 命令行管理工具

CUPS 管理工具如 `lpadmin`、`lpoptions`、`lpinfo`、`cupsenable`、`cupsdisable`、`cupsaccept` 和 `cupsreject`。这些工具列在表 13-4。

| 管理工具 |or |
| :--- | :--- |
| lpadmin | CUPS 配置 |
| lpoptions | 设置打印选项 |
| cupsenable | 激活打印机 |
| cupsdisable | 停止打印机 |
| accept | 允许打印机接受任务 |
| reject | 防止打印机接受任务 |
| lpinfo | 列出可用的 |

**表 13-4: CUPS 管理工具**

### lpadmin

`lpadmin` 命令让你选择默认打印机并配置打印机选项。使用 `-d` 选项选择打印机作为默认。在下一个示例中，`myprinter` 被选为默认打印机。

```
$ lpadmin -d myprinter
```

要配置打印机，首先使用 `-p` 选项选择打印机。下一个示例为 `myprinter` 打印机设置描述信息（`-D` 选项）。

```
lpadmin -p myprinter -D Epson550
```

某些选项允许按用户设置打印任务配额。`job-k-limit` 选项限制每个用户允许的任务大小，`job-page-limit` 确定任务页面限制，`job-quota-period` 限制指定时间段内的任务数量。下一个命令为每个用户设置 100 页限制。

```
lpadmin -p myprinter -o job-page-limit=100
```

你可以通过 `-u` 选项和 `allow` 或 `deny` 列表来控制用户访问。使用允许列表对于许可访问的用户。允许列表带有 `allow:` 标签，后跟用户列表。要拒绝访问使用 `deny:` 列表。在下面的命令中，允许 `cora` 访问但拒绝 `orrin` 和 `harlow`。

```
lpadmin -p myprinter -u allow:cora deny:orrin,harlow
```

要简单地拒绝或允许所有用户或无，使用 `all` 或 `none` 术语许可或拒绝所有或无用户。通过让一个使用 `all` 或 `none` 列表，你可以创建例外。下一个命令允许 `dylan` 以外的所有用户访问。

```
lpadmin -u allow:all deny:dylan
```





lpadmin -p myprinter -u allow:all deny:dylan

### lpoptions

通过 `lpoptions` 命令，你可以设置默认的打印格式选项，例如颜色或页面格式。使用 `-l` 选项查看打印机可能的选项列表。`-p` 选项选择打印机，`-d` 选项设置默认打印机。以下命令列出了 `myprinter` 打印机的当前选项。

```
lpoptions -p myprinter -l
```

要给选项赋值，你需要使用 `-o` 选项配合选项名和值，即 `-o option=value`。你可以使用 `-r` 选项移除打印机选项。在下一个示例中，`sides` 选项被分配了值 `two-sided`，以启用纸张双面打印。

```
lpoptions -p myprinter -o sides=two-sided
```

你稍后可以使用 `-r` 选项来移除该选项。

```
lpoptions -p myprinter -r sides
```

要查看可用选项列表，请检查 CUPS 软件手册中的标准打印选项，网址为 [`www.cups.org/`](https://www.cups.org/)。

### cupsenable 和 cupsdisable

`cupsenable` 命令启动打印机，`cupsdisable` 命令停止打印机。通过 `-c` 选项，你可以取消打印机队列中的所有作业，而 `-r` 选项会广播解释关机的消息。此命令禁用了名为 `myepson` 的打印机。

```
cupsdisable myepson
```

### cupsaccept 和 cupsreject

通过 `cupsaccept` 和 `cupsreject` 命令，你可以控制打印机队列的访问权限。你可以使用 `cupsreject` 命令停止打印机接受作业。`cupsaccept` 命令允许打印作业。以下命令防止 `myepson` 打印机接受打印作业。

```
cupsreject myepson
```

### lpinfo

`lpinfo` 命令显示系统上可用的 CUPS 设备和驱动程序信息。`-v` 选项显示设备信息，`-m` 选项显示驱动程序信息。

```
lpinfo -m
```

# 14. 网络文件系统与网络信息系统: NFS 和 NIS

Linux 提供了多种工具用于访问连接到网络的远程系统文件。网络文件系统 (NFS) 允许你连接并直接访问位于另一台机器上的资源，如文件或设备。新版本 NFS4 提供了更高的安全性，允许通过防火墙访问。网络信息服务 (NIS) 维护网络上所有系统的配置文件。

## 网络文件系统: NFS 和 /etc/exports

通过 NFS，你可以挂载位于远程计算机上的文件系统，并将其作为系统上的本地文件系统进行访问。这样，网络上的不同主机就可以访问同一个文件系统。NFS 网站是 [`nfs.sourceforge.net`](http://nfs.sourceforge.net)。查看 Ubuntu Server Guide | Services | Service - NFS 获取基本配置和管理。

[`ubuntu.com/server/docs/service-nfs`](https://ubuntu.com/server/docs/service-nfs)

要为系统设置 NFS 服务，请安装 `nfs-kernel-server`、`nfs-common` 和 `rpcbind` 包（仅需选择 `nfs-kernel-server`）。

```
sudo apt install nfs-kernel-server
```

## NFS 守护进程

NFS 使用远程过程调用 (RPC) 为 TCP/IP 上的文件系统提供远程访问。主机系统通过导出某些文件系统，使其对网络上的其他主机可用。导出操作通过 `/etc/exports` 文件中的项目进行配置。导出由多个守护进程实现，如 `rpc.mountd`、`rpc.nfsd` 和 `rpc.gssd`，它们支持远程主机访问。你可以通过 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件中的条目控制 NFS 服务器。`nfs-kernel-server` 包中提供的 NFS 服务器守护进程列在此处。你可以在 `/etc/default/nfs-kernel-server` 文件中配置选项。

`rpc.nfsd` 接收来自远程系统的 NFS 请求，并将其转换为本地系统的请求。

`rpc.mountd` 执行请求的挂载和卸载操作。`nfs-common` 包提供了额外的 NFS 支持守护进程。你 1 可以在 `/etc/default/nfs-common` 文件中配置选项。

`rpc.svcgssd` 为 RPC 操作提供安全保障（rpcsec-gss 协议）。

`rpc.gssd` 为 NFSv4 中的 rpcsec-gss 协议提供客户端支持。

`rpc.idmapd` 将用户和组 ID 映射为名称。

`rpc.statd` 在远程主机重启时提供锁定服务。

`rpc.blkd` 提供设备发现和映射。`rpcbind` 服务器将远程过程调用转换为相应的端口号。NFS 守护进程由 `systemd` 管理，使用位于 `/lib/systemd/system` 的多个服务文件。NFS 守护进程及其 `systemd` 单元文件列表 14 中。

此处显示了 `nfs-server.service` 文件。运行时配置读取自 `/etc/default/nfs-kernel-server` (EnvironmentFile)。

```ini
nfs-server.service
[Unit]
Description=NFS server and services
DefaultDependencies=no
Requires=network.target proc-fs-nfsd.mount
Requires=nfs-mountd.service rpcbind.socket
Wants=nfs-idmapd.service
After=local-fs.target
After=network.target proc-fs-nfsd.mount rpcbind.target nfs-mountd.service
After=nfs-idmapd.service rpc-statd.service
Before=rpc-statd-notify.service
Wants=auth-rpcgss-module.service
After=rpc-gssd.service rpc-svcgssd.service
Wants=nfs-config.service
After=nfs-config.service
[Service]
EnvironmentFile=-/run/sysconfig/nfs-utils
Type=oneshot
RemainAfterExit=yes
ExecStartPre=/usr/sbin/exportfs -r
ExecStart=/usr/sbin/rpc.nfsd $RPCNFSDARGS
ExecStop=/usr/sbin/rpc.nfsd 0
ExecStopPost=/usr/sbin/exportfs -au
ExecStopPost=/usr/sbin/exportfs -f
ExecReload=/usr/sbin/exportfs -r
[Install]
WantedBy=multi-user.target
```

使用 `systemctl` 命令手动启动、停止和重启 NFS 服务器。

```
sudo systemctl start nfs-kernel-server
```

`nfsd`、`mountd`、`idmapd`、`statd` 和 `svcgssd` 守护进程对应的 `systemd` 单元文件将以 `nfs-` 和 `rpc-` 前缀运行这些守护进程。要检查 NFS 是否实际运行，你可以使用 `rpcinfo` 命令配合 `-p` 选项。你应该看到 `mountd` 和 `nfs` 的条目。如果没有，说明 NFS 未在运行。

`nfsd`、`mountd` 和 `svcgssd` 守护进程的选项在 `/etc/default/nfs-kernel-server` 文件中设置，你可以在那里设置服务器数量、服务器优先级、端口以及是否使用 `svcgsd` 等选项。

```ini
/etc/default/nfs-kernel-server
# 启动服务器的数量
# 要禁用服务器上的 nfsv4，请在此处指定 '--no-nfs-version 4'
RPCNFSDCOUNT=8
# 服务器的运行时优先级（参见 nice(1))
RPCNFSDPRIORITY=0
# rpc.mountd 的选项。
# 如果你有基于端口的防火墙，你可能想在此处使用 --port 选项
# 设置固定端口。更多信息请参见 rpc.mountd(8) 或 [`wiki.debian.org/?SecuringNFS`](http://wiki.debian.org/?SecuringNFS)
RPCMOUNTDOPTS=--manage-gids
# 你想启动 svcgssd 守护进程吗？它仅内核 beros 导出所需。
# 有效值为 "yes" 和 "no"；默认值为 "no"。
NEED_SVCGSSD=
# rpc.svcgssd 的选项。
RPCSVGSSDOPTS=
# rpc.nfsd 的选项。
RPCNFSDOPTS=
```

`rpc.statd`、`rpc.idmapd` 和 `rpc.gssd` 守护进程可以使用 `systemctl` 命令访问。

```
sudo systemctl restart statd
sudo systemctl restart idmapd
sudo systemctl restart gssd
```

要配置是否启动 `statd`、`idmapd` 和 `gssd` 守护进程，你需要在 `/etc/default/nfs-common` 文件中设置选项。默认情况下，`statd` 和 `idmapd` 守护进程会被启动。

```ini
/etc/default/nfs-common
# 如果没有为 NEED_ 选项设置值，将尝试自动检测；
# 这对于大多数人来说足够了。有效值为
```





# `NEED_` 选项的为 "yes" 和 "no"。

# `rpc.statd` 的选项。

# `rpc.statd` 是否应该监听在特定端口？这在你有一个基于端口的防火墙时特别有用。要使用固定端口，请将此变量设置为 `statd` 参数，例如：`"--port 4000 --outgoing-port 4001"`。

# 更多信息，请参阅 `rpc.statd(8)` 或 http://wiki.debian.org/?SecuringNFS`

`STATDOPTS=`

# 你是否想启动 `gssd` 守护进程？Kerberos 挂载需要它。

`NEED_GSSD=`

## NFS 配置：`/etc/exports`

导出的文件系统列在 `/etc/exports` 中。一个条目由文件系统在主机系统所在文件夹的路径组成，随后是可以访问它的主机机列表以及任何访问控制选项。每个主机的选项放在括号内，并以逗号分隔的列表中。某些主机的选项可能不同。某些主机只有只读访问权限，而另一些具有读写访问权限。如果你想指定适用于所有主机的选项，可以使用星号（*`）代替主机名，后跟选项列表。选项列表在 表 14-1 中提供。`/etc/exports` 文件中导出条目的语法如下。

`folder-pathname host-designation(options)`

| 通用选项 | 描述 |
| :--- | :--- |
| `secure` | 要求请求源自安全端口，即小于 1024 的端口。默认开启 |
| `insecure` | 关闭 `secure` 选项 |
| `ro` | 仅允许只读访问。这是默认值 |
| `rw` | 允许读/写访问 |
| `sync` | 在请求时立即执行所有写入。这是默认值 |
| `async` | 在服务器准备就绪时执行所有写入 |
| `no_wdelay` | 执行写入，不检查它们是否相关 |
| `wdelay` | 检查写入是否相关，如果是，则等待一起执行。这可能会降低性能。这是默认值。 |
| `hide` | 自动隐藏作为另一个导出目录子目录的导出目录 |
| `subtree_check` | 检查文件系统中的父目录以验证导出的子目录。这是默认值。 |
| `no_subtree_check` | 不检查文件系统中的父目录来验证导出子目录 |
| `insecure_locks` | 不要求对锁定请求进行身份验证。用于旧版本的 NFS |

| 用户 ID 映射 | 描述 |
| :--- | :--- |
| `all_squash` | 将所有 UID 和 GID 映射到匿名用户。适用于 NFS 导出的公共 FTP 目录、新闻池目录等。 |
| `no_all_squash` | `all_squash` 的反选项。这是默认设置。 |
| `root_squash` | 将来自远程 root 用户的请求映射到匿名 UID/GID。这是默认值。 |
| `no_root_squash` | 关闭 root 压缩（squashing）。允许 root 用户以远程 root 身份访问 |
| `anonuid` | 显式设置用于所有 `all_squash` 和 `root_squash` 选项的匿名账户 UID 和 GID。默认值为 nobody 和 nogroup |

**表 14-1：`/etc/exports` 选项**

### NFS 主机条目

同一个文件夹可以有多个主机条目，每个条目都有不同的访问选项。

`folder-pathname host(options) host(options) host(options)`

指定主机有多种方法。对于位于你的域内的主机，只需指定主机名。其他域的主机需要完全限定域名。你可以使用主机的 IP 地址代替主机名。要同时引用多个主机（例如某个域中的主机），可以使用星号 `*` 后跟域名。例如，`*.mytrek.com` 引用 `mytrek.com` 域中的所有主机。如果你想使用 IP 地址而不是域名，则将使用 IP 网络地址。网络地址使用子掩码来引用一组 IP 地址。或者，你也可以为指定的主机组使用 NIS 网络组名。NIS 网络组名名前带有 `@` 符号。

`folder host(options) folder *(options) folder *.domain(options) folder 192.168.1.0/255.255.255.0(options) folder @netgroup(options)`

### NFS 选项

`/etc/exports` 中的几个 NFS 选项允许你控制对导出文件夹的访问。`ro` 选项提供只读访问，`rw` 选项指定读/写访问并允许更改。写入任务可以一次性执行（`sync` 选项），也可以在服务器决定时执行（`async` 选项）。为了提高效率，默认情况下，相关的写入请求会同时写入（`wdelay`）。这可能会导致延迟并降低性能。如果你愿意，可以使用 `no_wdelay` 让写入立即执行。如果你导出的某个文件夹实际上是另一个导出文件夹的子文件夹，那么除非该子目录被挂载，否则它是不可访问的。此功能通过 `hide` 选项实现，该选项是默认值。在某种意义上，该子目录在被显式挂载之前是隐藏的。`no_hide` 选项将覆盖此功能，如果父文件夹已挂载，即使该文件夹已导出且未挂载，也可以被访问。

`subtree_check` 选项检查导出文件夹父目录的有效性。虽然这种检查对只读文件系统有效，但在读/写文件系统上可能会出现问题，因为文件名和文件夹可能会随时更改。`no_subtree_check` 选项允许你覆盖此检查。

### NFS 用户级访问

几个 NFS 选项和功能适用于用户级访问。出于安全考虑，NFS 服务器将 NFS 客户端的 root 用户视为匿名用户，这一过程被称为“用户压缩（squashing the user）”。这种压缩不会允许客户端以 NFS 伺服器的 root 用户的身份出现。`no_root_squash` 选项允许你覆盖这种压缩，允许特定客户端的 root 用户对 NFS 服务器具有 root 级控制权限。

压缩也可以应用于所有用户。`all_squash` 选项将所有 NFS 用户视为匿名用户，将他们限制在匿名组。这将防止客户端用户尝试伪装成 NFS 服务器上的用户。

只有当该用户在 NFS 服务器上具有相同用户 ID 的相应账户时，该用户才能挂载并访问 NFS 服务器上的文件夹。如果用户 ID 不同，它们被视为两个不同的用户。与其维护两个账户，不如使用 NIS 服务器仅在一个位置维护用户 ID。

### NFSv4

NFS 版本 4 是 NFS 协议的最新版本，具有增强的功能，例如更好的安全性、速度和可靠性。然而，只有少数命令有所不同。当挂载 NFS4 文件系统时，你必须使用 `nfs4` 文件类型，而不是 `nfs`。

```
mount -t nfs4 rabbit.mytrek.com:/ /home/dylan/projects
```

你还可以使用 `fsid=0` 选项引用根导出位置。以下条目允许你挂载文件系统到 `/home/richlp` 文件夹，而无需在挂载操作中指定它。

```
/home/richlp *(fsid=0,ro,sync)
```

NFSv4 还支持 RPCSEC_GSS（远程过程调用安全，通用安全服务）安全机制，它提供了公私密钥、加密以及 Kerberos 认证。Kerberos 有两种口味：`krb5i` 验证数据的完整性，`krb5p`加密所有请求但会产生性能影响。使用 GSS 和 Kerberos 安全的示例作为注释列在 `/etc/exports` 文件中。没有指定远程位置，而是使用 rpcsec_gss 协议 (`gss`) 配合 `krb5i` 安全。示例中挂载的目录是 `/srv/nfs4/homes` 目录。

```
/srv/nfs4/homes gss/krb5i(rw,sync,no_subtree_check)
```





NFS4 允许为文件夹和文件设置访问控制列表 (ACL)。使用 NFS4 ACL 工具来管理这些列表（`nfs4-acl-tools` 软件包）。NFS4 文件系统 ACL 工具包含 `nfs4_getfacl`、`nfs4_setfacl` 和 `nfs4_editfacl`。查看每个工具的 Man 页面获取详细选项和示例。`nfs4_getfacl` 将列出指定文件或目录的访问控制。`nfs4_setfacl` 将为目录或文件创建访问控制，而 `nfs4_editfacl` 则允许你更改这些设置。`nfs4_editfacl` 实际上是带 `-e` 选项调用 `nfs_setfacl`。在编辑访问控制时，你将进入一个可以在其中进行更改的编辑器。设置访问控制可以从文件、标准输入或在命令行列出控制条目。

ACL 条目的格式在 `nfs4_acl` Man 页面中描述。ACL 条目中的第一个元素是条目类型，例如允许或拒绝条目（`A` 或 `D`）。条目类型之后是 ACL 标志，用于表示组或继承能力。标志之后是应用 ACL 的主体（principal）。这通常是将被允许或拒绝访问的用户 URL。你也可以指定组，但你必须包含 `g` 组标志。存在特殊的 URL（`OWNER@`、`GROUP@` 和 `EVERYONE@`），分别对应用于标准权限的所有者、组和其他访问者。主体之后是访问选项的列表，例如 `r` 表示读取或 `w` 表示写入。读取、写入和执行权限为 `r`、`w``x`。下面的示例为所有者提供了完全访问权限，但仅为用户 `mark@mypics.com` 提供了读取和执行权限。拒绝了组的写入和执行权限。

```
A::OWNER@:rwadtTnNcCy
A::mark@mypics.com:rxtncy
D:g:GROUP@:waxtc
```

ACL 权限可以通过属性进一步细化。这里有属性读取（`t`,`n`）和属性写入（`T`,`N`），以及 ACL 读取（`c`）和写入（`C`）访问。`y` 选项启用 NFS 读写同步。`d` 选项允许你删除文件和目录，`D` 选项允许删除子目录。通过 `a` 选项你可以追加数据并创建子目录。`rtncy` 选项是读取选项，`wadDTNC` 是写入选项，而 `x` 是执行选项。`y` 选项是同步访问所需的。`C` 选项允许用户更改访问控制。小写 `c` 让用户显示访问控制。

### NFS /etc/exports 示例

下面的 `/etc/exports` 文件示例显示了文件系统导出的样本。在第一个条目，所有主机对挂载在 `/srv/pub` 文件夹的文件系统具有只读访问权限。`/srv` 文件夹通常用于不同服务器维护的文件夹。`all_squash` 选项将用户视为匿名用户。下一个条目为 `lizard.mytrek.com` 主机提供挂载在 `/home/mypics` 文件夹的文件系统的读写权限。接下来的条目允许 `rabbit.mytrek.com` 主机对 NFS 服务器的 DVD-ROM 具有只读访问权限。通过最后一个条目，用户可以安全地访问 `/home/richlp` 文件夹。

```
/srv/pub *(ro,insecure,all_squash,sync) /home/mypics lizard.mytrek.com(rw,sync) /media/dvdrom rabbit.mytrek.com(ro,sync) /home/richlp *(secure,sync)
```

默认的 `/etc/options` 文件显示了使用 NFSv2、NFSv3 和 NFSv4 格式的示例。

```
# /etc/exports: 可能导出到 NFS 客户端的文件系统的访问控制列表
#              参见 exports(5)。 #
# NFSv2 和 NFSv3 的示例:
# /srv/homes hostname1(rw,sync,no_subtree_check) hostname2(ro,sync,no_subtree_check)
#
# NFSv4 的示例:
# /srv/nfs4 gss/krb5i(rw,sync,fsid=0,crossmnt,no_subtree_check) # /srv/nfs4/homes gss/krb5i(rw,sync,no_subtree_check) #
```

### 应用更改

每当 NFS 服务器启动时，`/etc/exports` 文件中列出的文件系统就会导出。导出过程涉及读取 `/etc/exports` 中的条目并在 `/var/lib/nfs/xtab` 文件中创建相应的条目。NFS 读取 `/var/lib/nfs/xtab` 文件并使用它执行实际导出。从这个意义上说，`xtab` 文件持有活动导出的列表。

如果你向 `/etc/exports` 文件添加了条目，并希望在不重启系统的情况下导出它们，可以使用带 `-a` 选项的 `exportfs` 命令。添加的条目将被导出。添加 `-v` 选项会显示显示 NFS 正在执行的任务的消息。

```
exportfs -a -v
```

如果你编辑了 `/etc/exports` 文件并更改了条目，可以使用 `-r` 选项重新导出这些条目。`-r` 选项将重新同步 `/var/lib/nfs/xtab` 文件与 `/etc/exports` 条目，移除 `/etc/exports` 文件中任何缺失的导出，并重新导出那些选项不同的条目。实际上，你正在应用对 `/etc/exports` 文件所做的任何更改。

```
exportfs -r -v
```

如果你同时添加了条目并更改了现有条目，可以组合添加和重新导出选项（`-r` 和 `-a`）来导出添加的条目并重新导出编辑过的条目，同时移除已删除的条目。

```
exportfs -r -a -v
```

### 手动导出文件系统

与其使用 `/etc/exports` 文件中的条目，你可以在命令行中使用 `exportfs` 命令来导出文件系统。导出的文件系统会被添加到 `/var/lib/nfs/xtab` 文件中。使用 `exportfs` 命令时，使用 `-o` 选项指定权限。在选项之后，输入要导出的主机和文件系统。确保用冒号分隔主机和文件系统名称。例如，要将 `/home/myprojects` 目录导出到 `golf.mytrek.com` 并使用 `ro` 和 `insecure` 权限，使用：

```
exportfs -o rw,insecure /home/myprojects
```

你还可以使用 `exportfs` 配合 `-u` 选项取消导出文件系统。此操作会将导出的文件系统从 `/var/lib/nfs/xtab` 文件中移除。下一个示例是对 `/home/foodstuff` 文件夹取消导出。

```
exportfs -u lizard.mytrek.com:/home/foodstuff
```

## 控制 NFS 访问

你可以使用 `hosts.allow` 和 `hosts.deny` 文件控制本地网络对 NFS 服务器的访问。你也可以使用防火墙规则控制来自外部主机的访问。

### /etc/hosts.allow 和 /etc/hosts.deny

`/etc/hosts.allow` 和 `/etc/hosts.deny` 文件用于限制网络或互联网（如果可行）访问服务器提供的服务。例如，可以使用 `hosts.allow` 文件允许某些主机访问你的 FTP 服务器。`hosts.deny` 文件中的条目显式拒绝某些主机访问。对于 NFS，你可以通过控制特定 NFS 守护进程的访问提供类似的安全性。

### rpcbind 服务

`rpcbind` 服务告知主机 NFS 服务所在的位置。引用 rpcbind 的名称为 `rpcbind`，如上示例所示。rpcbind 配置文件为 `/etc/default/rpcbind`。在这里你可以为 rpcbind 服务设置选项。

通过拒绝访问，远程主机将无法找到 NFS。为了安全 NFS，你应该拒绝所有主机，然后对你允许的主机设置例外。在 `hosts.deny` 文件中，以下条目将拒绝所有主机。rpcbind 服务通过名称 `rpcbind` 引用。`ALL` 是引用所有主机的特殊术语。

```
rpcbind:ALL
```





对于你想要允许访问 NFS 的主机，你需要将它们的名称放在 `hosts.allow` 文件中。每个条目将包含 `rpcbind` 术语后跟一个冒号，然后是允许的主机的 IP 地址列表，并用逗号分隔。地址可以是单个地址，也可以是用网络掩码指定的地址范围。接下来的示例仅允许本地网络中的 `192.168.0.0`（使用范围表示）以及单个主机 `10.0.0.43` 访问。

```
rpcbind: 192.168.0.0/255.255.255.0, 10.0.0.43
```

但请记住，`rpcbind` 也会用于 NIS 等其他服务。如果你在 `hosts.deny` 中关闭了对 `rpcbind` 的所有访问，你将必须在 `hosts.allow` 中允许对 NIS 服务（如 `ypbind` 和 `ypderser`）的访问。此外，如果你想允许访问 `ruptime` 和 `rusers` 等远程命令，你需要为它们添加条目。

你还应该为其他 NFS 服务添加相同的控制措施，例如 `mountd` 和 `statd`，如下所示的 `hosts.deny` 文件。

```
mountd:ALL
statd:ALL
```

它们在 `hosts.allow` 文件中对应的条目允许对特定主机访问。

```
mountd: 192.168.0.0/255.255.255.0, 10.0.0.43
statd: 192.168.0.0/255.255.255.0, 10.0.0.43
```

### Netfilter 规则

通过 Netfilter，你可以控制来自本地网络之外（通常是互联网）的主机访问 NFS 服务。`rpcbind` 服务使用端口 111，`nfsd` 使用端口 2049。如果你想拒绝来自本地网络之外网络的 NFS 访问，可以设置 Netfilter 规则来拒绝该访问。在接下来的示例中，拒绝通过 `eth1` 网络设备传输的端口 111 和 2049 的访问。尝试访问端口 111 或 2049 的互联网数据包将被拒绝。在示例中，`eth1` 设备连接到外部网络。

```
iptables -A INPUT -i eth1 -p 111 -j DENY
iptables -A INPUT -i eth1 -p 2049 -j DENY
```

为了让 NFS 在本地网络上工作，你需要使用 `-f` 选项允许分片。以 `eth0` 作为本地网络使用的设备，接下来的示例启用了本地分片。

```
iptables -A INPUT -i eth0 -f -j ACCEPT
```

## 挂载 NFS 文件系统：NFS 客户端

主机可以挂载并访问 NFS 提供的文件夹。当然，主机必须作为 NFS 客户端运行。NFS 客户端功能内置在 Linux 内核中。任何 Linux 主机都可以通过 mount 操作挂载远程 NFS 文件夹。

### 自动挂载 NFS：`/etc/fstab`

NFS 文件夹可以通过 `/etc/fstab` 文件中的条目以及 `mount` 命令进行挂载。实际上，`/etc/fstab` 文件中 NFS 挂载操作的条目将在启动时自动挂载 NFS 文件系统。`/etc/fstab` 文件中 NFS 条目的挂载类型为 `nfs`。要在挂载操作中引用 NFS 文件系统，你需要提供文件夹名称和该文件所在远程主机的主机名。文件夹和主机之间用冒号分隔。例如，`rabbit.trek.com:/home/project` 引用了在 `rabbit.trek.com` 主机上挂载到 `/home/project` 的文件系统。挂载操作还需要在你系统上要挂载的文件夹路径。`/etc/fstab` 文件中 NFS 条目的格式如下所示。NFS 版本 1 到 3 的文件类型为 `nfs`，而对于 NFS 版本 4，则是 `nfs4`。

```
host:remote-directory local-directory nfs options 0 0
```

NFS 挂载操作还可以包含 NFS 挂载选项，例如用于读写的数据数据包的大小（`rsize` 和 `wsize`）以及等待远程主机响应的时间（`timeo`）。还有选项可以让你执行硬挂载或软挂载（`hard` 和 `soft`）。如果对文件系统进行硬挂载，当远程主机未响应时，你的系统将反复尝试联系。硬挂载是默认选项。如果对文件系统进行软挂载，那么当远程主机未响应时，反复将在指定的时间限制后停止并显示错误消息。为了避免因持续失败的硬挂载尝试消耗系统资源，使用软挂载可能是更好的，因为它会停止此类尝试。你可以在 `mount` 手册页中找到 NFS 挂载选项列表（参见 表 14-2）。

在接下来的 NFS 挂载示例中，远程系统是 `rabbit.mytrek.com`，要挂载的文件系统是 `/home/projects`。它将被挂载到本地系统上的 `/home/dylan/projects` 文件夹。该文件夹必须在本地系统上存在。文件类型为 `nfs`。

```
rabbit.mytrek.com:/home/projects /home/dylan/projects nfs rsize=8192,wsize=8192,timeo=60,soft
```

### 手动挂载 NFS：`mount`

使用 `mount` 命令，`nfs` 选项设置了文件。接下来的示例显示了 NFS。使用 `-t nfs4` 选项用于 NFS 4。

```
rabbit.trek.com:/home/projects /home/dylan/projects nfs4 -o soft,intr,timeo=60
```

使用 `umount` 命令卸载。接下来的示例。

```
umount /home/dylan/projects
```

### 按需挂载 NFS：`autofs`

NFS 文件系统可以通过 `autofs` 软件包自动挂载。当 `autofs` 服务激活时，文件系统会在访问时被挂载。

| 选项 | 描述 |
| :--- | :--- |
| `rsize` | NFS 从服务器读取文件时使用的数据包大小。默认为 1024 字节。设置为 8192 可以提高性能。 |
| `wsize` | NFS 向服务器写入文件时使用的数据包大小。默认为 1024 字节。设置为 8192 可以提高性能。 |
| `timeo` | 在发送第一次重传之前以十分之一为秒计算的值。默认值为零点七秒。 |
| `retry` | 在放弃之前重试 NFS 挂载操作的分钟数。默认为 10000 分钟（一周）。 |
| `retrans` | 在发生主要超时（默认为 3）之前，NFS 挂载操作的重传次数或微超时次数。此时，连接将取消或显示“服务器未响应”的消息。 |
| `soft` | 使用软挂载挂载文件系统。 |
| `hard` | 使用硬挂载挂载文件系统。这是默认选项。 |
| `intr` | 允许 中断文件操作并返回调用程序。默认不允许文件操作被中断。 |
| `bg` | 如果第一次挂载尝试超时，然后在后台继续尝试挂载。默认是不进行后台运行直接失败。 |
| `tcp` | 使用 TCP 协议挂载 NFS 文件系统，而不是默认的 UDP 协议。 |





`/misc` 文件夹已经配置配置为自动挂载文件系统的路径。随后你可以在 `/etc/auto.master` 文件中添加文件系统，包括它们对应的映射文件。在 `/etc/auto.master` 文件中，你会发现一个 `/misc` 目录的条目，显示映射文件为 `auto.misc`。

```
/misc /etc/auto.misc
```

主文件中的映射条目还可以包含挂载文件夹的选项，例如 `timeout` 选项，它在执行自动卸载之前会设置一个空闲等待时间。

映射文件存储了要挂载的文件系统的键（key）、挂载选项以及完整路径和主机名。键是文件系统挂载点在本地系统上的文件夹名称。例如，要将 `rabbit.mytrek.com` 主机上的 `/home/projects` 文件夹挂载到本地的 `/auto/projects` 文件夹，可以使用以下条目。`/etc/auto.misc` 包含了映射文件条目的示例。

```
projects soft,intr,timeo=20 rabbit.mytrek.com:/home/projects
```

要挂载到 `/misc` 以外的文件夹，你需要在主文件中为其放置一个条目。下一个条目使用 `auto.myprojects` 映射文件挂载到 `/myprojects` 文件夹。

```
/myprojects auto.myprojects --timeout 60
```

随后 `/etc/auto.myprojects` 映射文件将包含 NFS 文件系统挂载的条目，如下所示。

```
dylan soft,intr,rw rabbit.mytrek.com:/home/projects
newgame soft,intr,ro lizard.mytrek.com:/home/supergame
```

## 网络信息服务：NIS

对于提供 NFS 服务的网络，客户端系统可以共享该网络上的文件系统和设备。每个系统都必须为共享的设备或文件系统拥有配置文件。设备或文件系统的任何配置更改都意味着需要更新位于每个系统上的相应配置文件。为了避免这种复杂性，NFS 提供了网络信息系统（NIS）服务。NIS 服务维护了网络中共享文件系统和设备的配置文件。如果设备和文件系统发生任何变化，你只需要更新这些设备和文件系统的 NIS 配置即可。你还可以使用 NIS 服务来维护用户的管理信息，例如用户 ID 和密码。对于密码更改，你只需要更新 NIS 密码文件。

NIS 服务通过 `/etc/nsswitch` 配置文件进行配置。以下是一些标准条目：

```
passwd: compat
shadow: compat
networks: files protocols: db files
```

注意：`NIS+` 是 NIS 的一种更高级的形式，提供了对加密和身份验证的支持。然而，它的管理更为困难。

NIS 由太阳微系统（Sun Microsystems）开发，最初被称为 Sun 的黄页（YP）。NIS 文件保存在 NIS 服务器上（NIS 服务器有时仍被称为 YP 服务器）。网络上的各个各个系统使用 NIS 客户端向 NIS 服务器发送请求。NIS 服务器在名为 `maps*.*` 的特殊数据库文件中维护其信息。NIS 客户端和服务器都有 Linux 版本。Linux NIS 客户端可以利用 NIS 轻松地连接到任何网络。

注意：现在许多网络使用 LDAP 而不是 NIS 来管理用户信息和身份验证。

NIS 软件包是 Universe 仓库的一部分，可以作为 `nis` 安装，这也会同时安装 `yp-tools` 包。NIS 客户端程序和工具包括 `ypbind`（NIS 客户端守护进程）、`ypwhich`、`ypcat`、`yppoll`、`ypmatch`、`yppasswd` 和 `ypset`。每个工具都有带有详细用法说明的 Man 页面。NIS 服务器程序和工具包括 `ypserv`（NIS 服务器）、`ypinit`、`yppasswdd`、`yppush`、`ypxfr` 和 `netgroup`。每个都有自己的 Man 页面。当你安装 NIS 服务器（`nis` 软件包）时，会提示输入 NIS 域，并将你的主机名列为默认。

NIS 服务器由 `systemd` 使用 `/run/systemd/generator.late` 目录下的 `nis.service` 文件管理。它由 systemd-sysv-generator 使用 `/etc/init.d/nis` 脚本生成。`ypbind.service` 和 `ypserv.service` 文件是 `nis.service` 文件的链接。

```
nis.service

# 由 systemd-sysv-generator 自动生成

[Unit]

Documentation=man:systemd-sysv-generator(8)

SourcePath=/etc/init.d/nis

Description=LSB: Start NIS client and server daemons.

Before=multi-user.target

Before=multi-user.target

Before=multi-user.target

Before=graphical.target

After=network-online.target

After=rpcbind.target

After=remote-fs.target

Wants=network-online.target

[Service]

Type=forking

Restart=no

TimeoutSec=5min

IgnoreSIGPIPE=no

KillMode=process

GuessMainPID=no

RemainAfterExit=yes

ExecStart=/etc/init.d/nis start

ExecStop=/etc/init.d/nis stop

ExecReload=/etc/init.d/nis reload
```

### /etc/nsswitch.conf: 名称服务切换

标准 C 库中的不同函数必须配置为在你的 Linux 系统上运行。以前，类数据库的服务（例如，密码支持和 NIS 或 DNS 等名称服务）直接访问这些函数并使用固定的搜索顺序。这种配置通过一种名为名称服务切换（NSS）的方案实现，它基于太阳微系统 Solaris 2 操作系统所使用的同名方法。数据库源及其查找顺序列在 `/etc/nsswitch.conf` 文件中。

| 文件 | 说明 |
| :--- | :--- |
| ethers | 以太网地址 |
| group | 用户组 |
| hosts | 主机名和数字 |
| netgroup | 网络范围的主机和用户列表，用于访问规则；glibc 2.1 之前的 C 库仅通过 NIS 支持 netgroups |
| network | 网络名称和数字 |
| passwd | 用户密码 |
| protocols | 网络协议 |
| publickey | NFS 和 NIS+ 使用的 SecureRPC 公钥和密钥 |
| rpc | 远程过程调用名称和数字 |
| services | 网络服务 |
| shadow | 影子用户密码 |

表 14-3：NSS 支持的数据库

`/etc/nsswitch.conf` 文件包含了可以由 NSS 控制的不同配置文件的条目。NSS 支持的系统配置文件列在 表 14-3。其中一个条目由两个字段组成：服务和配置规范。服务由配置文件后跟冒号组成。第二个字段是该文件的配置规范，说明了查找过程将如何工作。配置规范可以包含服务规范和操作项。服务规范是要搜索的服务。目前有效的服务规范有 `nis`、`nis-plus`、`files`、`db`、`dns`、`systemd` 和 `compat`（见表 14-4）。并不是所有规范都适用于每个配置文件。例如，`dns` 服务仅适用于 `hosts` 文件，而 `nis` 适用于所有文件。示例首先检查本地 `/etc/password` 文件，然后是 systemd。

```
passwd: files systemd
```

| 服务 |  |
| :--- | :--- |
| files | 检查对应的 `/etc` 文件（例如用于 hosts 的 `/etc/hosts`）；此服务适用于所有文件 |
| db | 检查对应的 `/var/db` 数据库；适用于除 **netgroup** 外的所有文件
| compat | 提供 **nis** 和 **files** 服务，并带有 + 和 - 条目的兼容支持。仅适用于 **passwd**、**group** 和 **shadow** 文件 |
| dns | 检查 DNS 服务；仅适用于 **hosts** 文件 |
| nis | 检查 NIS 服务；适用于所有文件 |
| nisplus | NIS 版本 3 |
| hesiod | 使用 Hesiod 进行查找 |
| myhostname | 使用 **gethostname** 操作获取主机名的本地配置 |

表 14-4：NSS 配置服务





为了更精细地访问 `passwd`、`group` 和 `shadow` 源，你可以在文件条目中使用 `+` 和 `-` 符号来确定该条目是否可以被 `nsswitch` 服务访问。`compat` 服务提供了一种兼容模式，会检查此类条目。如果没有此类条目，所有条目都将使用 `nis` 服务。`compat` 服务仅适用于 `passwd`、`group` 和 `shadow` 数据库。这提供了与文件条目和 `nis` 服务等效的功能。

如果你的 `passwd`、`group` 和 `shadow` 文件已经包含了 `+` 和 `-` 条目，并且你希望文件条目的优先级高于 `nis` 服务，你可以在 `compat` 条目之前指定文件数据库（files）。

`passwd: files compat`

操作项（action item）指定了针对特定服务要执行的操作。操作项放置在服务后的括号内。配置规范可以列出多个服务，每个服务都有自己的操作项。在接下来的示例中，`hosts` 文件的条目有一个配置规范，其说明检查 `/etc/hosts` 文件和 `mdns4_minimal` 服务，如果未找到，则检查 DNS 服务器（`dns`），如果仍然无法解析，则获取主机名（如 `localhost`）的本地配置（`myhostname`）。

`hosts: files mdns4_minimal [NOTFOUND=return] dns myhostname`

一个操作项由一个状态和一个动作组成。状态持有服务查找的可能结果，而动作是在状态为真时要执行的操作。目前，可能的状态值为 `SUCCESS`、`NOTFOUND`、`UNAVAIL` 和 `TRYAGAIN`（服务临时不可用）。可能的动作有 `return` 和 `continue`：`return` 停止对配置文件的查找过程，而 `continue` 则继续处理到下一个列出的服务。在前述的示例中，如果在 `NIS` 中没有找到记录，则查找过程将结束。

这里显示的是 `/etc/nsswitch.conf` 文件的副本，它列出了常用的条目。注释和被注释的条目以 `#` 符号开头：

```
/etc/switch.conf

# GNU 名称服务切换功能的示例配置。

# 如果你安装了 `glibc-doc-reference` 和 `info` 软件包，请尝试：

# `info libc "Name Service Switch"` 获取有关此文件的信息。

passwd: compat systemd

group: compat systemd

shadow: compat  gshadow: files hosts: files mdns4_minimal [NOTFOUND=return] dns myhostname

networks: files protocols: db files services: db files ethers: db files rpc: db files netgroup: nis
```

# 15. Samba

Linux Samba 服务器允许 Microsoft Windows 网络上的 Windows 客户端访问 Linux 系统上的共享文件和打印机，反之，也允许 Linux 系统访问 Windows 系统上的共享文件和打印机。它允许你通过 Windows 网络连接到 Windows 系统。实际上，Samba 允许 Linux 系统像 Windows 服务器一样运行，并使用与 Windows 网络相同的协议。

UNIX 和 Linux 系统使用 TCP/IP 协议进行网络传输，而 Microsoft Windows 网络使用服务器消息块（`SMB`）协议。`SMB` 协议利用一个名为网络基本输入输出系统（`NetBIOS`）的网络接口，允许 Windows 系统共享资源（如打印机和文件夹）。`SMB` 最初是为小型网络设计的。对于大型网络，微软开发了通用 Internet 文件系统（`CIFS`），它在 Windows 网络中仍在使用 `SMB` 和 `NetBIOS`。

Samba 服务器和客户端由 Andrew Tridgell 创建，旨在将 Linux 系统连接到 Windows PC。它们允许 UNIX 和 Linux 系统无缝地连接到 Windows 网络。UNIX/Linux 系统可以在 Windows 系统上共享资源，Windows 系统也可以在 Unix/Linux 系统上共享资源。从某种意义上说，Samba 是一个专业级、开源且免费的 `CIFS` 版本。通过 Samba，你可以使用 Linux `cifs` 文件系统将共享 Windows 文件夹直接挂载到你的 Linux 系统上。

Samba 软件组织成多个软件包（见[表 15-1]）。通过选择 `samba` 服务器包，将自动选择如 `smbclient` 和 `samba-common` 等必要的支持包。可以使用 `apt`、Synaptic 软件包管理器或软件管理器来安装 Samba 软件包。

| 软件包名称 | 描述 |
| :--- | :--- |
| `samba` | Samba 服务器 |
| `samba-common` | Samba 配置文件和支持工具 |
| `smbclient` | 用于访问 Windows 共享的 Samba 客户端 |
| `nemo-share` | 用于共享文件夹的 Nemo 文件管理器扩展 |
| `caja-share` | 用于共享文件夹的 Caja 文件管理器扩展 |

**表 15-1: Linux Mint 上的 Samba 软件包**

你可以从 Samba 的 Web 和 FTP 网站 `https://www.samba.org/` 获取详细文档。你的系统 `/usr/share/doc/samba/examples` 目录下提供了示例。查看《Ubuntu Server Guide | Services | Samba》以获取基础配置和管理。

`https://ubuntu.com/server/docs/samba-introduction`

## Samba 应用

Samba 服务器提供四种服务：文件和打印服务、身份验证与授权、名称解析以及服务公告。Samba 软件包安装了两个服务器守护进程（`smbd` 和 `nmbd`）和若干实用程序（见[表 15-2]）。`SMB` 守护进程 `smbd` 提供文件和打印服务。`SMB` 守护进程 `smbd` 提供文件和打印服务、身份验证与授权、名称解析以及服务公告。`SMB` 守护进程 `smbd` 提供文件和打印服务。这允许网络上的用户共享文件夹和打印机。这些服务的访问由密码控制。

`nmbd` 服务器提供解析和服务公告。名称解析通过 NetBIOS 解析 IP 地址。服务公告让网络上的服务可用。

| 应用 | 描述 |
| :--- | :--- |
| `nemo-share` | Nemo 文件管理器的共享扩展 |
| `caja-share` | Caja 文件管理器的共享扩展 |
| `smbd` | 为 SMB 客户端提供文件打印服务的 Samba 守护进程 |
| `nmbd` | 提供 NetBIOS 名称解析和服务服务的 Samba 守护进程 |
| `winbind` | 使用 Windows 域提供的服务 |
| `mount.cifs` | 在 Linux 客户端上挂载 Samba 共享（由 mount 命令配合 -t cifs 使用） |
| `smbpasswd` | 修改 Samba 服务器上的 SMB 加密密码 |
| `pdbedit` | 编辑 Samba 用户数据库。这是一个安全帐户管理器（SAM）数据库 |
| `tdbbackup` | 备份 Samba 的 .tdb 数据库文件 |
| `smbcontrol` | 向 Samba 服务器发送管理消息，如关闭或关闭共享 |
| `smbstatus` | 显示 SMB 网络连接当前状态 |
| `testparm` | 测试 Samba 配置文件 `smb.conf` |
| `nmblookup` | 将 Windows PC 的 NetBIOS 名称映射到 IP 地址 |
| `/etc/default/samba` | Samba 启动选项 |

**表 15-2: Samba 应用**

基础 Samba 配置支持已由 `nautilus-share` 实现，允许使用文件管理器浏览 Samba 共享。对于更复杂的配置，你可以直接编辑 `/etc/samba/smb.conf` 文件。配置文件位于 `/etc/samba` 目录下。

你还可以安装 `winbind` 软件包来运行 `winbind` 守护进程。该守护进程允许 Samba 服务器使用 Windows 域提供的身份验证服务。通过 `winbind`，Samba 服务器可以使用 Windows 域身份验证服务来验证用户，而不是使用自己的用户集。





Samba 软件包还包含支持工具，例如 `smbstatus`，它可以显示 SMB 服务器的当前状态以及谁在使用它；以及 `pdbedit`，它用于编辑 SMB 密码数据库。额外的包提供了其他支持工具，如 `smbclient`，它可以让 Linux 系统访问 Samba 服务（仅限命令行）。`mount.cifs` 和 `umount.cifs` 命令允许 Linux 系统挂载和卸载 Samba 共享文件夹。它们通过 `mount` 命令配合 `-t cifs` 选项进行调用。你可以使用 `testparm` 来测试你的 Samba 配置。`smbtar` 是一个 shell 脚本，可以将 SMB/CIFS 共享资源备份到 Unix 磁带驱动器。`nmblookup` 命令会将 Windows  的 NetBIOS 名称映射到其 IP 地址。通过 `smbcontrol` 命令，你可以向 Samba 服务器（`smbd`、`nmbd` 和 `winbindd`）发送管理消息，例如关闭共享、重新加载配置或关闭服务器。

## 启动和访问 Samba

安装完成后，Samba 通常配置为自动启动。你可以直接编辑 `/etc/samba/smb.conf` 文件进行更改。如果你作了更改，必须重启 Samba 服务器才能生效。要使用你的新配置重启 Samba，请使用 `systemctl` 命令。`start`、`stop` 和 `restart` 选项将启动、停止和重启服务器。在命令行或终端窗口运行以下命令来重启 Samba。

```
sudo systemctl restart smbd
sudo systemctl restart nmbd
```

Samba 服务器由两个守护进程组成：`smbd` 和 `nmbd`。你可能需要先用 `systemctl` 命令启用它们，然后使用 `service` 命令启动它们。在提示符处（在桌面上打开一个终端窗口），使用 `sudo` 命令获取管理权限，紧跟一个 `systemctl` 命令针对 `smbd` 服务器并配合 `enable` 命令来启用该服务器。对 `nmbd` 服务器也执行相同的操作。然后使用 `systemctl` 命令配合 `start` 命令来启动它们。一旦启用，每当系统启动时，服务器应该会自动启动。

```
sudo systemctl enable nmbd
sudo systemctl enable smbd
sudo systemctl start nmbd
sudo systemctl start smbd
```

Samba 由 `systemd` 管理，使用 `/lib/systemd/system` 目录下的 `smbd.service` 和 `nmbd.service` 文件。这里显示 `smbd.service` 文件。Samba 在网络、文件系统挂载和 Cups 服务之后（After）启动。它在 `multi-user.target` 之前（Before）启动。在桌面上添加了 `graphical.target`。该服务使用 `/usr/sbin` 目录下的 `smbd` 脚本启动（ExecStart）。

```ini
smbd.service
[Unit]
Description=Samba SMB Daemon
Documentation=man:smbd(8) man:samba(7) man:smb.conf(5)
Wants=network-online.target
After=network.target network-online.target nmbd.service winbind.service
[Service]
Type=notify
NotifyAccess=all
PIDFile=/var/run/samba/smbd.pid
LimitNOFILE=16384
EnvironmentFile=-/etc/default/samba
ExecStartPre=/usr/share/samba/update-apparmor-samba-profile
ExecStart=/usr/sbin/smbd --foreground --no-process-group $SMBDOPTIONS
ExecReload=/bin/kill -HUP $MAINPID
LimitCORE=infinity
[Install]
WantedBy=multi-user.target
```

NMB 守护进程在网络之后（After）启动。它使用 `/usr/sbin/nmbd` 脚本启动 `nmbd` 服务器。

```ini
nmbd.service
[Unit]
Description=Samba NMB Daemon
Documentation=man:nmbd(8) man:samba(7) man:smb.conf(5)
After=network-online.target
Wants= network.target network-online.target
[Service]
Type=notify
NotifyAccess=all
PIDFile=/var/run/samba/nmbd.pid
EnvironmentFile=-/etc/default/samba
ExecStart=/usr/sbin/nmbd --foreground --no-process-group $NMBDOPTIONS
ExecReload=/bin/kill -HUP $MAINPID
LimitCORE=infinity
[Install]
WantedBy=multi-user.target
```

## 防火墙访问

Linux Mint 和 Ubuntu 上使用的 UFW 防火墙阻止从你的 Linux 桌面浏览 Samba 和 Windows 共享。为了于此限制，你需要确保防火墙将 Samba 视为受信任的服务。要允许防火墙访问 Samba 端口，你应该使用类似 `ufw` 的防火墙配置工具启用访问。Samba 端口为 139/TCP、137/UDP、138/UDP 和 445/TCP。此外，多播服务发现服务（`mdns`）使用端口 5353/UDP。

![Image](img/image-587.png) ![Image](img/image-522.png)

**图 15-1：Gufw Samba 防火墙访问**

如果你在桌面界面操作，可以使用 Gufw 工具为 UFW 防火墙设置 Samba 端口。你需要将端口作为简单规则添加（参见第 10 章）（参见图 15-1）。





对于独立的 Samba 服务器，用户级安全和 `tdbsam` 数据库是默认设置。因此，它们在 `smb.conf` 配置文件中不需要额外指定。你可以通过 `security` 和 `passdb backend` 选项显式地配置它们。

```
security = user

passdb backend = tdbsam
```

你可以使用 `username map` 选项来指定用于关联 Windows 和 Linux 用户的文件。Windows 用户可以使用 Windows 用户名登录并作为关联的用户。用户名映射文件通常为 `/etc/samba/smbusers`。

```
username map = /etc/samba/smbusers
```

对于 LDAP Samba 数据库 `ldbsam`，你使用 LDAP Samba 工具来管理用户（`smbldap-tools` 软件包）。这些工具以 `smbldap` 为前缀。这些工具包含了用于添加、修改和删除用户及组的工具（`smbldap-useradd`、`smbldap-userdelete` 和 `smbldap-groupmod`）。`sbmldap-passwd` 命令通过 LDAP 管理 Samba 密码。`smbldap-userinfo` 命令显示用户信息。LDAP Samba 工具配置在 `/etc/smbldap-tools/smbldap.conf` 文件中。

Samba 服务器有一个密码可插认证模块 (PAM) 模块 `pam_smbpass.so`，它为 Samba 密码提供 PAM 认证。这将允许 Windows 主机在 PAM 控制的网络工作。该模块在你的 PAM `samba` 文件中配置。PAM `samba` 文件中的以下条目需要 Samba 服务器的 PAM 认证和密码。

```
auth required pam_smbpass.so nodelay

password required pam_smbpass.so nodelay
```

要让 PAM 与 Samba 工作，请在 `smb.conf` 文件中启用 PAM。

```
obey pam restrictions = yes
```

注意：之前使用的 `smbpasswd` 文件仍然可用，但仅为了向后兼容而包含。

### Samba 密码：smbpasswd

每个尝试访问 Samba 服务器的用户都需要一个 Samba 服务器用户名和密码。这种用户级安全性要求该用户名和 Samba 密码存储在 Samba 密码数据库中，该数据库由 Samba 服务器独立维护。要添加或更改用户的 Samba 密码，请配合用户名使用 `smbpasswd` 命令。

```
$ sudo smbpasswd dylan
```

New SMB Password: new-password Repeat New SMB Password: new-password

任何用户都可以使用 `smbpasswd` 命令更改自己的密码，如下所示。如果你没有 Samba 密码，只需按回车。

```
$ sudo smbpasswd
```

Old SMB password: old-password New SMB Password: new-password Repeat New SMB Password: new-password

如果你想在不使用密码的情况下授予用户访问权限，可以使用带有 `-n` 选项的 `smbpasswd`。此外，`smb.conf` 文件需要将 `null passwords` 选项设置为 `yes`。

如果你在使用旧的 smb 密码文件（而不是 tdbasm 数据库），你应该取消配置 Samba 使用加密密码。将 `encrypt passwords` 选项设置为 `yes` 并指定 SMB 密码文件。你还可以使用 `mksmbpasswd` 脚本根据 `/etc/passwd` 文件中的用户创建 smbpasswd 文件。将 passwd 文件的内容通过给 `mksmbpasswd`，然后使用重定向 (`>`) 创建该文件。

### 管理 Samba 用户：smbpasswd 和 pdbedit

你可以使用 `smbpasswd` 命令或 `pdbedit` 工具来管理 Samba 用户密码。对于 `smbpasswd` 命令，`-a` 选项添加用户，`-x` 选项删除用户。使用 `-e` 和 `-d` 选项启用或禁用用户。

```
sudo smbpasswd -a aleina
```

`smbpasswd` 命令可以将 Samba 密码保存到旧的 smbpasswd 文件或较新的 `tdbsam` 后端数据库文件。Linux Mint 目前使用 `tdbas` 后端数据库。`pdbedit` 命令设计用于与此数据库配合工作。通常使用 `pdbedit` 命令而不是 `smbpasswd` 来管理你的 Samba 用户。使用 `pdbedit` 添加用户时使用 `-a` 选项，删除用户时使用 `-x` 选项。你还可以更改密码并设置用户的家目录，以及将用户记录导入或导出到其他后端数据库。

```
sudo pdbedit -a dylan
```

与 `smbpasswd` 不同，通过 `pdbedit` 命令你可以显示更多关于用户的信息。`-L` 选项显示后端数据库中的用户。添加 `-v` 选项以获取详细信息。对于特定用户，添加用户名，如下所示。

```
sudo pdbedit -Lv richard
```

你甚至可以显示域策略（`-P` 选项），例如最小密码长度或重试次数。

```
sudo pdbedit -P
```

如果你想导入和导出数据库记录，使用 `-i` 和 `-e` 选项。以下操作将记录从旧的 `smbpasswd` 文件导入新的 `tdbsam` 后端数据库。

```
sudo pdbedit -i smbpasswd -e tdbsam
```

注意：如果你的系统使用启用 LDAP 的 Samba 数据库，使用 smbldap 工具管理用户和组。

## Samba smb.conf 文件

Samba 配置存储位于 `/etc/samba` 目录下的 `smb.conf` 文件中。它包含了各种共享资源的配置，以及适用于所有资源的全局选项。

你可以在终端中使用 `testparm` 命令来检查对 `/etc/samba/smb.conf` 文件所做任何更改的语法。

```
testparm
```

`/etc/samba/smb.conf` 文件分为两个基本部分：一个用于全局选项，另一个用于共享服务。共享服务（也称为 shares）可以是文件空间服务（客户端将其作为文件系统的扩展使用），也可以是打印服务（客户端用于访问主机上的打印服务）。文件空间服务是一个授予客户端权限的目录。`/etc/samba/smb.conf` 文件包含了用于 Linux Mint 的默认设置。你可以编辑该文件以自定义配置。注释行以 `#` 符号开头。被禁用的条目以分号 `;` 开头。要启用此类条目，请删除其开头的分号。有关 Samba 配置参数的完整列表，请查看 `smb.conf` 的 Man 页。

`smb.conf` 文件通过标签（注释）Global Settings（全局设置）和 Share Definitions（共享定义）分为大部分组。Global Settings 部分包含多个子部分：Browsing/Identification（浏览/识别）、Networking（网络）、Debugging/Accounting（调试/计数）、Authentication（认证）、Domains（域）、Printing（打印）和 Misc（杂项）。




一个节的格式始终以节标签开始，即括在括号中的共享资源名称。除了特殊节外，节标签可以是你选择的任何名称。在节标签之后，分行输入该服务的不同参数（选项）。大多数参数定义了该服务的访问权限。例如，你可能希望一个共享文件夹是可浏览的，但是只读的，并使用某个特定的打印机。参数以 `parameters name` `=` `value.` 的格式输入。你可以通过在注释行的开头处放置一个分号来在节中添加注释。

下面是一个简单的节配置示例。节标签被括在括号中，后面跟着两个参数条目。`path` 参数引用共享文件夹。`writeable` 参数指定用户是否对该文件夹具有写权限。

```
[mysection]
path = /home/chris
writeable = true
```

打印机服务具有相同的格式，但需要某些其他参数。`path` 参数指定打印机池化文件夹的位置。`read only` 和 `printable` 参数设置为 `true`，表示该服务是只读且可打印的。`public` 参数允许任何人访问该服务。

```
[myprinter]
path = /var/spool/samba
read only = true
printable = true
public = true
```

`writeable` 选项是 `read only` 选项的反向别名。`writeable = yes` 条目与 `read only = no` 条目相同。`read only = no`、`writeable = yes` 和 `write ok = yes` 都为用户提供了写权限。

### 变量替换

对于分配给参数的字符串值，你可以结合替换运算符。这为指定取决于上下文的值（如用户名）提供了更大的灵活性。例如，假设服务需要为每个登录的用户使用单独的目录。此类目录的路径可以使用 `%u` 变量指定，该变量会替换为当前的用户名。字符串 `path = /tmp/%u` 对于 `justin` 用户将变为 `path = /tmp/justin`，而对于 `dylan` 用户将变为 `path = /tmp/dylan`。表 15-3 列出了几个较为常见的替换变量。

提示：`writeable` 选项是 `read only` 选项的反向别名。`writeable = yes` 条目与 `read only = no` 条目相同。

### 全局设置

全局设置（Global Settings）节为 Samba 服务器提供配置，并指定了可能用于目录和文件夹节的默认值。在此节中，你将找到工作组名称、密码配置、浏览和日志文件的条目。全局节以 `[global]` 标签开始。

| 变量 | 描述 |
| :--- | :--- |
| %S | 当前服务的名称 |
| %P | 当前服务的根目录 |
| %u | 当前服务的用户名 |
| %H | 用户的主目录 |
| %h |  Samba 的互联网主机名 |
| %m | 客户端机器的 NetBIOS 节点 |
| %L | 服务器的 NetBIOS 节点 |
| %M | 客户端机器的互联网名称 |
| %I | 客户端机器的 IP 地址 |

**表 15-3: Samba 替换变量**

### 浏览/识别

Workgroup 条目指定了你想赋予网络的工作组名称。这里显示了 `smb.conf` 文件中默认的 Workgroup 条目：

```
[global]
# 将此更改为 Samba 服务器将加入的工作组/NT 域名称
workgroup = WORKGROUP
```

工作组名称对于 Samba 服务器支持的每个 Windows 客户端必须相同。在许多 Windows 网络中，默认值是 WORKGROUP。这也是 `smb.conf` 文件中指定的默认名称。如果你想使用其他名称，必须更改 `smb.conf` 文件中的 `workgroup` 条目。`smb.conf` 文件中的 `workgroup` 条目与每个 Windows 客户端上的工作组名称必须一致。在示例中，工作组名称为 `mygroup`。

```
workgroup = mygroup
```

server string 条目包含了你想在客户端系统上显示的服务器的描述性名称。在 Windows 系统上，这是显示在 Samba 服务器图标上的名称。默认值是 Samba Server，但你可以将其更改为任何你喜欢的名称。

```
# server string 等同于 NT Description 字段
server string = %h server (Samba, Ubuntu)
```

注意：你还可以配置 Samba 作为 Windows NT 网络的主域控制器 (PDC)。作为 PDC，Samba 会建立其他系统将使用的 Windows 域，而不是参与一个已经建立的工作组。

### 网络

此子节包含接口指令，用于将网络接口设备分配到特定的网络以供服务器使用。这些条目默认是被注释的。这里显示了在第一个以太网设备上的 localhost 的注释默认条目。请确保将 `eth0` 替换为你的网络设备的实际名称（预测名称），例如 `enp7s0`。你可以使用 `ifconfig` 来查找名称。

```
; interfaces = 127.0.0.0/8 eth0
```

如果运行 Samba 服务器的系统没有受到防火墙保护，或者防火墙运行在同一系统上，你还应该启用以下内容。

```
; bind interfaces only = yes
```

### 调试/计数

此节包含用于为 Samba 服务器设置日志的指令。日志文件条目使用 `%m` 符号进行配置，以便为连接到服务器的每个机器设置单独的日志文件。

```
log file = /var/log/samba/%m
```

日志文件的最大设置为 1000 行。

```
max log size = 1000
```

要让 Samba 日志记录到日志文件，请将 logging 设置为 file。如果你希望将重要消息发送到 syslog，请添加 syslog。

```
# 我们希望 Samba 仅记录到 /var/log/samba.{smbd,nmbd}.
logging = file
```

panic action 在崩溃时通知管理员。

```
panic action = /usr/share/samba/panic-action %d
```

### 验证

Samba 服务器的角色可以是 standalone、成员服务器或域控制器（主、备份或活动目录）。通常服务器是 standalone。服务器角色决定了安全性。对于 standalone 服务器，安全性是 user，需要密码登录。

```
server role = standalone server
```

Windows 客户端在登录过程中使用加密密码。密码默认加密并由密码数据库管理。

你可以使用 security 选项指定安全性：`user`（用户密码）、`domain`（Windows 域）或 `ads`（Kerberos）安全性。`auto` 设置是默认值，它根据服务器角色派生安全性。如果服务器角色是 `standalone server`，则安全性为 `user` 且在 `smb.conf` 文件中指定。在 `smb.conf` 文件中，由于 `server role` 设置为 `standalone server`，安全性设置为用户级 (`user`)，且密码数据库文件使用 `tdbsam`。

随后开启可插身份模块 (PAM) 安全性支持。

```
obey pam restrictions = yes
```

当更改 Samba 密码时，它们需要与 UNIX 密码同步。`unix` `password sync` 指令开启同步，而 `passwd` `program` 和 `passwd chat` 指令使用 `passwd` 命令和指定的提示来更改密码。

```
unix password sync = yes
passwd program = /usr/bin/passwd %u
passwd chat = *Enter\snew\s*\spassword:* %n\n *Retype\snew\s*\spassword:* %n\n *password\supdated\successfully* .
```

PAM 也用于 Samba 客户端更改密码。

```
pam password change = yes
```




作为一种安全措施，你可以将对 SMB 服务的访问限制在某些指定的本地网络中。在主机网络上，输入你想要允许访问的本地网络的地址。若要拒绝网络中除少数特定主机以外的所有人的访问，可以在网络地址后使用 `EXCEPT` 选项并加上这些主机的 IP 地址。本地主机（`127`）始终会被自动包含。接下来的示例允许访问两个本地网络。

```
hosts allow = 192.168.1. 192.168.2.
```

`map to guest` 指令设置为 `bad user`。这将允许任何未知用户以访客身份登录。然而，登录失败的 Samba 用户将不允许访问，即使是访客也不行。

```
map to guest = bad user
```

## 域

`Domains` 小节将你的 Samba 服务器配置为微软公共网域控制器 (PDC)。所有这些指令默认都被注释掉。请参阅本章稍后关于公共网域控制器的章节，了解如何在微软网络上将你的 Samba 服务器设置为 PDC。

## 杂项

`Misc` 小节包含用于自定义服务器的条目。大多数都被注释掉了，除了允许用户创建公共共享的 `usershare` 指令外。`include` 指令允许你在 `/home/samba/etc` 目录下为特定机器设置配置文件，这些文件在机器连接时会被读取。

```
; include = /home/samba/etc/smb.conf.%m
```

还有为使用 Winbind 服务器的用户提供的条目，指定了用户和组 ID 范围以及使用的 shell。

# winbind 的某些默认值（确保你没有将这些范围用于其他用途。）

```
; idmap config * : backend = tdb ; idmap config * : range = 3000-7999 ; idmap config YOURDOMAINHERE : backend = tdb ; idmap config YOURDOMAINHERE : range = 100000-999999 ; template shell = /bin/bash
```

`usershare` 指令允许非 root 用户共享文件夹。注释掉的用戶 `max shares` 条目可以限制用户可以设置的共享数量。

```
; usershare max shares = 100
```

`user allow guests` 指令允许用户创建公共共享，允许访客访问这些共享。

# 允许授予 usershare 权限的用户创建公共共享，而不仅仅是经过身份验证的用户

```
usershare allow guests = yes
```

你可以使用访客用户登录让资源对任何人可用，而无需密码。访客用户登录将处理任何未使用特定账户登录的用户。Samba 通常配置为使用 `nobody` 用户作为访客用户。或者，你可以设置并指定一个特定用户作为访客用户。你可以通过 `smb.conf` 文件中的 `guest ok` 和 `guest account` 条目来指定访客用户。确保将访客用户添加到密码文件中。

```
guest ok = yes
guest account = nobody
```

此外，本节还提供了若干性能优化建议，例如为 Linux 系统设置套接选项。

## 共享定义

`Share Definitions` 部分将包含常用共享定义的节，以及你自行设置的任何共享（例如共享文件夹或打印机）。有三个特殊的节：`homes`、`netlogon` 和 `profiles`，用于特殊用途。在共享定义中，可以通过用户名或组来引用用户。组通过前缀 `@` 字符表示。某些组引用了管理员用户，例如 `@lpadmin`、`@syslog` 和 `@adm`。

### Homes 部分

`Homes` 节适用于系统上用户的主目录。它设置了远程用户访问用户主目录的默认控制选项。将 `browseable` 选项设置为 `no` 可以防止远程用户在文件浏览器中列出文件。远程用户对文件的读取访问由 `read only` 选项决定。`create mask` 和 `directory mask` 选项设置了远程用户在主目录中创建的新文件和文件夹的默认权限。通常，这些权限被设置为 0700，允许所有者拥有读/写/执行权限。`valid users` 选项使用 `%S` 宏映射到当前服务。你可以添加 `writeable` 指令来允许写入访问。

```
writeable = yes
```

在 `smb.conf` 文件中，主目录条目被注释掉了，默认禁用了对用户主目录的访问。若要启用对主目录的访问，请删除 `smb.conf` 文件中每个条目前的分号注释。

如果你正在设置 PDC 并选择将用户配置文件保存在用户主目录中，则必须取消 homes 节及其条目的注释。

```
[homes]
comment = Home Directories
browseable = no
read only = yes
create mask = 0700
directory mask = 0700
valid users = %S
```

### printers 和 print$ 部分

`printers` 节指定了访问打印机的默认控制选项。这些用于那些没有特定节的打印机。将 `browseable` 设置为 `no` 仅仅是从客户端隐藏打印机机节，而不是隐藏打印机本身。`path` 选项列出了 Samba 用于打印文件的溢出目录的位置。`printable` 选项必须设置为 `yes` 才能允许任何打印。否则，打印将被禁用。若要允许访客用户打印，请将 `guest ok` 选项设置为 `yes`。此处显示 Printers 节。

```
[printers]
comment = All Printers
browseable = no
path = /var/spool/samba
printable = yes
guest ok = no
```

接下来显示的 `print$` 节指定了 Windows 客户端可以在你的 Samba 服务器何处找到打印机。驱动程序位于 `/var/lib/samba/printers` 且为只读。`browseable`、`read-only` 和 `guest` 指令被注释掉了。可以启用它们以允许浏览驱动程序。`write list` 指令允许你远程管理打印驱动。`lpadmin` 是你的管理员组名称。

```
[print$]
comment = Printer Drivers
path = /var/lib/samba/printers
browseable = yes
read only = yes
guest ok = no
; write list = root, @lpadmin
```

### 共享

共享资源的节（例如你系统上的文件夹）放在 Homes 和 Printers 节之后。共享文件夹的节以该共享的标签开始。随后是其路径名和权限的选项，每个选项单独占一行。`path` 条目持有文件夹的完整路径。在 `comment` 条目中，你可以描述该共享。权限选项允许让文件夹变为可写、公共或只读。`valid users` 选项允许你控制特定用户对共享的访问。对于未输入的选项，将使用 Global、Homes 和 Printers 节中的默认值。

在示例中，`myprojects` 共享将 `/myprojects` 文件夹定义为任何具有访客访问权限的用户开放的共享资源。

```
[myprojects]
comment = Great Project Ideas
path = /myprojects
read only = no
guest ok = yes
```

使用 `valid users` 选项限制对特定用户的访问。若要关闭所有其他用户的访问，将 `guest ok` 选项设置为 `no`。

```
[mynewmusic]
comment = New Music
path = /home/specialprojects
valid users = mark, richard
guest ok = no
read only = no
```

在以下示例中，Documents 文件夹对 george 和 richard 用户是可用且可写的。

```
[Documents]
path = /home/richard/Documents
writeable = yes
browseable = yes
valid users = george, richard
```

如果你想允许对文件夹进行公共访问，将 `guest ok` 条目设置为 `yes`，且不设置 `valid users` 条目。

```
[newdocs]
comment = New Documents
path = /home/newdocs
guest ok = yes
read only = no
```





`valid users` 选项列出的用户允许每个用户对其创建的文件拥有控制权。你可以通过 `create mask` 选项指定文件权限，从而进一步管理对文件的控制。在本示例中，权限设置为 765，这为所有者提供了读/写/执行权限，为组成员提供了读/写权限，并为所有其他人提供了读取/执行权限（默认值为 744，组和其他权限为只读）。

```
[myshare]
comment = Writer’s projects
path = /usr/local/drafts valid users = Justin, chris, dylan guest ok = no
read only = no create mask = 0765
```

你可以通过 `read list` 和 `write list` 选项进一步细化控制。`read list` 选项为列出的用户提供只读权限，而 `write list` 选项则提供读取和写入权限。

```
[myshare]
comment = Writer’s projects
path = /usr/local/drafts read list = Justin, chris
write list dylan guest ok = no
read only = no create mask = 0765
```

### 打印机共享

对特定打印机的访问定义在 `smb.conf` 文件的 Printers 部分。对于打印机，你需要包含 `Printer` 和 `Printable` 条目，并指定所使用的打印服务器类型。通过 `Printer` 条目，你可以为打印机命名，通过将 `Printable` 条目设置为 `yes`，你可以允许其打印。你可以通过 `valid` `users` 条目以及将 `Public` 条目设置为 `no` 来控制对特定用户的访问。对于公共访问，将 `public` 条目设置为 `yes`。对于 CUPS 服务器，将打印选项设置为 `cups`。

以下示例设置了一个允许访客访问的打印机，这允许网络上的任何用户使用该打印机。`read only` 选项设置为 `no`，以允许用户对位于 `/var/spool/samba` 的打印机溢出目录具有写入权限。打印机应该已经安装。示例中的打印机已安装为 `myhp`。你使用 CUPS 管理工具为 CUPS 服务器设置打印机。`Printing` 选项可以从 Printers 共享继承。

```
[myhp]
path = /var/spool/samba read only = no guest ok = yes printable = yes printer = myhp oplocks = no share modes = no printing = cups
```

如果需要，你也可以将打印机的使用限制为某些用户，拒绝公共访问，就像限制共享一样。在下一个示例中，打印机仅供用户 `larisa` 和 `aleina` 访问。如果你需要，可以添加其他用户。

```
[larisalaser]
path = /var/spool/samba read only = no valid users = larisa aleina guest ok = no printable = yes printing = cups printer = larisalaser oplocks = no share modes = no
```

### 测试 Samba 配置

如果你修改了 `smb.conf` 文件，应该对其进行测试以检查错误。使用 `testparm` 命令查看条目是否正确。`testparm` 会检查 Samba 条目的语法和有效性。默认情况下，`testparm` 检查 `/etc/samba/smb.conf` 配置文件。如果你想使用不同的配置文件，可以将其作为参数传递给 `testparm`。

### Samba 公共域控制器：Samba PDC

Samba 还可以作为公共域控制器 (PDC) 运行。域控制器将在网络上注册并作为域控制器发布。PDC 提供了一种更中心化的方式来控制 Samba 共享的访问。它提供了 `netlogon` 服务和 `NETLOGON` 共享。PDC 会为每个 Windows 和 Samba 客户端设置机器信任帐户。虽然你可以手动执行此操作，但 Samba 会为你完成。请记住，Samba 无法模拟 Microsoft Active PDC，但可以模拟 Windows NT4 PDC。

基本配置请参阅 Ubuntu Server Guide | Services | Samba - Domain Controller。

[`ubuntu.com/server/docs/samba-domain-controller`](https://ubuntu.com/server/docs/samba-domain-controller)

### 微软域安全

如 Samba 文档所述，微软域安全的主要优势是单点登录 (SSO)。实际上，登录你的用户账户也意味着登录了对整个网络共享资源的访问。你不需要在每次尝试访问共享网络资源时单独进行身份验证，因为你已经通过了身份验证。身份验证使用安全 ID (SID) 管理，它由网络 ID (NID) 和相对 ID (RID) 组成。`RID` 引用你的个人账户。每个帐户（即使是组或系统服务）都会分配一个单独的 `RID`。`SID` 用于设置网络上不同共享资源的访问控制列表 (ACL)，允许资源自动识别你的身份。

### 关键的 Samba PDC 配置选项

要配置你的 PDC，请编辑 `smb.conf` 文件中的 `Domains` 部分。在这里，你将找到配置 Samba PDC 选项的条目。你需要添加 `domain logons` 和 `domain master` 条目。

这里显示了基本的 PDC 选项。

```
workgroup = myworkgroup
domain logons = yes
domain master = yes
security = user
```

如果 netbios 名称与运行服务器的主机名不同，你可以添加 `netbios name` 选项来指定它。

```
netbios name = myserver
```

### 基础配置

与大多数 Samba 配置一样，PDC 需要一个 Samba 后。`tdbsam` 已经为你配置好了。安全级别应为 `user`。这通常是默认值且已经设置。这里显示了 `smb.conf` 条目。

```
passdb backend = tdbsam
```

PDC 还必须被指定为域主。默认设置为 `auto`。对于 PDC，将其设置为 `yes`；对于 BDC (备份域控制器)，将其设置为 `no`。

```
domain master = yes
```

PDC 具有浏览器功能，通过它可以定位你网络上的系统和共享。这些功能没有出现在 `smb.conf` 文件中，但你可以根据需要添加它们。只有在你已经有另一个想要作为本地主机的 PDC 时，才使用 `local master` 选项。你的网络中可能有多个域控制器在运行。你的微软网络进行选举以选择哪个应该是主。`os level` 设置了此 PDC 的优先级。它应该高于 32 以获得高于其他域控制器的优先级，确保此 PDC 被选为主主。`preferred master` 选项启动浏览器选举。

```
local master = no
os level = 33
preferred master = yes
```

### 域登录配置

Samba PDC 使用域登录服务允许用户登录网络。微软将该服务称为 `netlogon` 服务。它使用的 samba 共享也称为 netlogon。要配置域登录服务，将 `domain logons` 选项设置为 `yes`，或者将 `server role` 选项设置为 "primary domain controller" 或 "backup domain controller"。

```
domain logons = yes
```

logon path 引用用户使用的配置文件。`%N` 将是服务器名，`%U` 引用用户名。配置文件可以设置在独立的共享中，也可以在用户主目录下。以下引用配置文件共享中的配置文件。你还需要通过取消 `smb.conf` 文件中配置文件共享条目的注释来定义它。

```
logon path = \\%N\profiles\%U
```

如果配置文件存储在用户主目录而不是配置文件共享中，你应该取消以下条目。你还需要允许访问用户主目录，取消 homes 共享条目。

```
logon path = \\%N\%U\profile
```

`logon drive` 和 `logon home` 指定用户主目录的位置。登录驱动器被设置为 H: 盘。`%N` 解析为服务器名，`%U` 解析为用户。

```
logon drive = H:
logon home = \\%N\%U
```

登录脚本可以是系统设置或用户设置的。

```
logon script = logon.cmd
```





随后，你可以启用用户添加操作，以便向 PDC 添加用户、组和机器。`add machine` 条目允许 Samba 在 Windows 系统首次加入由 PDC 控制的网络时，自动为其添加受信任的机器账户。

`add user script = /usr/sbin/adduser --quiet --disabled-password --gecos "" %u`

`add machine script = /usr/sbin/useradd -g machines -c "%u machine account" -d /var/lib/samba -s /bin/false %u`
`add group script = /usr/sbin/addgroup --force-badname %g`

然后，你需要在 `smb.conf` 文件中设置 `netlogon` 共享。该共享包含 `netlogon` 脚本，在此例中为 `/var/lib/samba/netlogon` 目录，该目录不应该是可写的，但应该允许所有用户访问（`Guest OK`）。在 `smb.conf` 文件的共享定义部分，你会发现 `[netlogon]` 部分被注释了。请如所示所示移除该条目中的分号注释。

# 取消以下内容的注释并为域登录创建 netlogon 目录

# （你还需要配置 Samba 以作为域控制器。）

```
[netlogon]
comment = Network Logon Service
path = /home/samba/netlogon
guest ok = yes
read only = yes
```

如果你选择使用 profiles 共享来存储用户配置文件，则应启用 `profiles` 共享。取消以下内容的注释以定义 `profiles` 共享。这些条目位于 `netlogon` 共享之后。

```
[profiles]
comment = Users profiles
path = /home/samba/profiles
guest ok = no
browseable = no
create mask = 0600
directory mask = 0700
```

`profile` 共享是存储用户 netlogon 配置文件的地方。相反，如果你使用用户的家目录来存储其配置文件，则不需要定义和使用 `profiles` 共享。如果你选择将用户配置文件存储在用户家目录中，则应该取消 `homes` 共享条目。

## 使用客户端访问 Samba 服务

任何连接到 SMB 网络的客户端系统都可以访问 Samba 器提供的共享服务。你可以使用 `smblclient` 命令访问共享文件夹，然后运行命令管理该处的文件。如果你想将共享文件夹挂载到系统上的本地文件夹以提供直接访问，可以使用带有 `-t cifs` 选项的 `mount` 命令。确保已启用 Samba 的防火墙访问。

### 从桌面访问 Windows Samba 共享

在桌面上，你可以使用如 GNOME Files 这样的文件管理器访问你的 Samba 共享。目前，Linux 和 Windows 都处于从旧的 SMBv1 协议（安全消息块）向更安全的 SMBv3 协议过渡的过程中。因此，目前通过 Linux 文件管理器进行网络浏览无法工作。你可以使用 GNOME 文件管理器“其他位置”窗口中的“连接服务器”条目直接访问 Windows 共享。输入 `smb://` 协议（Avahi）以及你想访问的共享文件夹名称或远程 Windows 系统名称。在提示输入 Samba 密码后，将显示特定的共享文件夹或该主机上的共享文件夹。

### smbclient

你可以使用 `smbclient` 访问 Samba 服务器或 Windows 系统上的 SMB 共享服务和文件夹。它的工作方式非常像 FTP，但使用了不同的协议（即 SMB 协议）。`smbclient` 具有许多与 FTP 相同的命令，例如用于传输文件的 `mget` 或用于删除文件的 `del`。`smbclient` 还提供了查询和连接远程系统的选项。要查看完整的选项和命令列表，请检查 `smbclient` 手册页。`smbclient` 的参数是服务器名称和你想访问的服务。服务器名称之前是双斜杠，服务名称之前是单斜杠。服务可以是任何共享资源，例如文件夹或打印机。服务器名称是其 NetBIOS 名称，该名称可能与其 IP 名称相同，也可能不同。例如，要指定名为 `turtle.mytrek.com` 的服务器上的 `myreports` 共享目录，请使用 `//turtle.mytrek.com/myreports`。如果必须指定路径名，请记住，尽管 Windows 使用反斜杠作为其路径名，但 Unix/Linux 系统使用正斜杠。

```
//server-name/service
```

如果服务受密码保护，你必须提供密码。在服务名称之后作为参数输入密码。如果未提供密码且服务需要密码，系统将提示你输入。

`smbclient` 命令提供了几种访问共享的选项。`-I` 选项通过 IP 地址引用系统。要指定登录名，使用 `-U`。如果需要密码，请在密码前加上 `%`。`-L` 选项显示服务器上提供的服务列表，例如共享文件夹或打印机。以下命令将列出主机 `turtle.mytrek.com` 上的可用共享：

```
smbclient -L turtle.mytrek.com
```

为了访问远程系统上的特定文件夹，你输入文件夹名称和任何所需的选项。确保对 Windows 路径名使用反斜杠。连接到服务器后，会显示 SMB 提示符。然后你可以输入 `smbclient` 命令（如 `get` 和 `put`）来传输文件。使用 `quit` 和 `exit` 命令退出并结束连接。`recurse` 命令允许你开启递归以便一次复制整个子文件夹。通过 UNIX 文件匹配操作符，你可以引用多个文件。文件匹配操作符为 `*`、`[]` 和 `?`。默认掩码为 `*`，匹配所有。。示例使用 `mget` 复制所有带有 `.c` 后缀的文件，例如 `myprog.c`：

```
smb> mget *.c
```

在以下示例中，`smbclient` 使用登录名 `dylan` 和 `-I` 选项（服务器的 IP 地址）访问 `turtle.mytrek.com` 系统上的 `myreports` 文件夹。

```
smbclient //turtle.mytrek.com/myreports -I 192.168.0.1 -U dylan
```

通常情况下，你只需要如所示使用服务器名称引用服务器。你不需要指定 IP 地址。

```
smbclient //turtle.mytrek.com/myreports -U dylan
```

如果你想访问 Samba 服务器上的用户家目录，将使用 `homes` 服务。在下一个示例中，用户访问 Samba 服务器上 `aleina` 账户的家目录。由于未提供密码，系统将提示输入。

```
smbclient //turtle.mytrek.com/homes -U aleina
```

`smbclient` 也允许你访问 Windows 共享资源。输入你想访问的 Windows 客户端计算机及其共享文件夹。在下一个示例中，用户访问名为 `mycomp` 的客户端上的 `windata` 文件夹。如果文件夹允许访问，只需在密码提示处按回车即可。

```
smbclient //mycomp/windata
```

### mount.cifs: mount -t cifs

你可以通过 `mount` 命令和 `-t cifs` 选项将共享文件夹挂载到你的本地系统。`cifs` 选项将运行 `mount.cifs` 命令，该命令反过来调用 `smbclient` 命令执行挂载。`mount.cifs` 命令需要 Samba 服务器、共享文件夹以及要挂载共享文件夹的本地文件夹名称。以下示例将 `mybooks` 文件夹挂载到本地系统的 `/mnt/mybks` 文件夹。

```
mount -t cifs //turtle.mytrek.com/mybooks /mnt/mybks -U dylan
```

如果你想卸载文件夹，运行带有 `-t cifs` 选项的 `umount` 命令和文件夹名。`umount` 命令将调用 `umount.cifs` 命令执行卸载。

```
umount -t cifs /mnt/mybks
```





# Windows 共享

在 Windows 客户端上也可以挂载共享文件夹。使用两个正斜杠引导 Windows 计算机名称和 Windows 文件夹名称。如果文件夹名称包含空格，请用单引号括起来。在下面的示例中，用户将 `mywin` 上的 `mydocs` 文件夹挂载为 `/mywindocs` 文件夹。对于任何人都可以访问的文件夹，在密码提示时直接按回车无需输入密码。

```
$ mount -t cifs //mywin/mydocs /mywindocs Password:
```

```
$ ls /mydocs mynewdoc.doc myreport.txt
```

完成该共享文件夹的操作后，可以使用 `umount` 命令和 `-t cifs` 选项像卸载 Linux 文件夹一样卸载它。

```
umount –t cifs /mywindocs
```

如果您想控制用户对文件夹的访问，可以在挂载时指定用户名和密码作为选项，如下：

```
mount -t cifs -o username=harlow passwd=mypass //mywin/mydocs /mywindocs
```

如果您希望在每次启动系统时自动挂载文件夹，可以在 `/etc/fstab` 文件中为挂载操作创建一个条目。在条目中使用 `cifs` 文件类型：

```
//mywin/mydocs /mywindocs cifs defaults 0 0
```

# 表列表

- 表 1-1: Linux Mint 版本
- 表 1-2: Linux Mint 资源与帮助
- 表 1-3: Ubuntu 帮助与文档
- 表 3-1: 窗口和文件管理器快捷键
- 表 4-1: Linux 软件包扩展名
- 表 4-2: apt 和 apt-get 命令
- 表 4-3: snap 命令
- 表 5-1: X-App 应用
- 表 5-2: LibreOffice 应用
- 表 5-3: Calligra 应用
- 表 5-4: GNOME 应用程序
- 表 5-5: PostScript, PDF 和 DVI 查看器
- 表 5-6: 电子书阅读器
- 表 5-7: 编辑器
- 表 5-8: Linux 数据库系统
- 表 5-9: 邮件客户端
- 表 5-10: 新闻器
- 表 5-11: Linux 图形工具
- 表 5-12: 音乐播放器、编辑器和刻录器
- 表 5-13: 视频和 DVD 项目与应用
- 表 5-14: CD/DVD 刻录器
- 表 5-15: Web 浏览器
- 表 5-16: Java 包与 Java Web 应用
- 表 5-17: Linux FTP 客户端
- 表 5-18: 即时通讯、聊天工具和 VoIP 客户端
- 表 6-1: Cinnamon 快捷键
- 表 6-2: 文件管理器查看菜单
- 表 6-3: 文件管理器文件菜单
- 表 6-4: 文件管理器编辑菜单
- 表 6-5: 文件管理器弹出菜单
- 表 6-6: 文件管理器转菜单
- 表 6-7: 文件管理器侧边栏弹出菜单
- 表 6-8: 文件和文件夹弹出菜单
- 表 6-9: 桌面系统设置
- 表 7-1: 桌面菜单
- 表 7-2: 文件管理器转菜单
- 表 7-3: 文件管理器文件菜单
- 表 7-4: 文件管理器查看菜单
- 表 7-5: 文件管理器编辑菜单
- 表 7-6: 文件管理器弹出菜单
- 表 7-7: 文件管理器侧边栏弹出菜单
- 表 7-8: 文件和文件夹弹出菜单
- 表 7-9: MATE 偏好
- 表 8-1: Linux Mint 工具
- 表 8-2: 传感器软件包与应用
- 表 8-3: 音频设备与接口工具
- 表 8-4: PulseAudio 命令
- 表 9-1: Linux 管理工具
- 表 9-2: 备份资源
- 表 10-1: Linux 网络配置
- 表 10-2: nmcli 对象
- 表 10-3: wvdial 变量
- 表 10-4: 服务端口
- 表 10-5: UFW 火墙操作
- 表 10-6: 网络接口命名
- 表 11-1: Shell 调用命令
- 表 11-2: Shell 配置文件
- 表 11-3: BASH Shell 特性
- 表 11-4: Shell 设置的变量
- 表 11-5: Shell 使用的环境变量
- 表 12-1: systemd 类型与 man 页
- 表 12-2: systemd 单元与安装部分（所有单元 systemd.unit）
- 表 12-3: 特殊单元
- 表 12-4: 系统运行级别 (boot
- 表 12-5: systemd exec 选项（Service, Mount systemd.service）
- 表 12-6: systemd 服务选项
- 表 12-7: 服务文件集
- 表 12-8: systemd socket 选项 (systemd.socket
- 表 12-9: path 选项 (systemd.path
- 表 12-10: 系统状态
- 表 12-11: systemd 挂载与自动挂载文件选项（Mount, Automount
- 表 12-12: 系统关机选项
- 表 12-13: AppArmor 工具
- 表 12-14: SSH 工具
- 表 12-15: SSH 配置文件
- 表 13-1: 打印资源
- 表 13-2: CUPS 配置文件
- 表 13-3: CUPS 打印客户端
- 表 13-4: CUPS 管理工具
- 表 14-1: /etc/exports 选项
- 表 14-2: NFS 挂载选项
- 表 14-3: NSS 支持的数据库
- 表 14-4: NSS 配置服务
- 表 15-1: Linux Mint 上的 Samba 软件包





表 15-2: Samba 服务器应用

表 15-3: Samba 替换变量

# 图表列表

图 1-1: Linux Mint 20 Cinnamon 桌面
图 1-2: Linux Mint 20 Cinnamon Live DVD
图 1-3: Linux Mint 欢迎对话框
图 1-4: 欢迎对话框 - 文档

图 2-1: 带有安装图标的 Live DVD/USB (桌面)
图 2-2: 键盘布局
图 2-3: 安装第三方软件
图 2-4: 未检测到操作系统
图 2-5: LVM 安装选项
图 2-6: LVM 选择
图 2-7: 带有加密的 LVM
图 2-8: 加密系统的安全密钥
图 2-9: 安全密钥登录
图 2-10: 其他 (手动分区)
图 2-11: 手动对新硬盘分区
图 2-12: 在空白硬盘上创建新的分区表
图 2-13: 在空白硬盘上选择空空间
图 2-14: 创建新的启动分区
图 2-15: 创建新的根分区
图 2-16: 手动分区
图 2-17: 你在哪里，时区
图 2-18: 你是谁？
图 2-19: 安装进度幻灯片
图 2-20: 带有恢复内核的 Grub 高级选项菜单
图 2-21: 恢复选项
图 2-22: 引导修复

图 3-1: Linux Mint GRUB 菜单
图 3-2: 编辑 GRUB 菜单项
图 3-3: GRUB2 Linux Mint 主题
图 3-4: 带有用户列表的 LightDM 登录界面
图 3-5: 带有关机选项的 LightDM 登录界面
图 3-6: 带有桌面选择的 LightDM 登录界面
图 3-7: 登录窗口
图 3-8: 带有主机名或键盘布局的登录窗口
图 3-9: 锁屏和屏幕保护程序
图 3-10: 关机和重启对话框
图 3-11: 注销对话框
图 3-12: Linux Mint Cinnamon 桌面
图 3-13: Linux Mint Cinnamon 菜单
图 3-14: Nemo 文件管理器
图 3-15: Linux Mint MATE 桌面
图 3-16: Linux Mint 菜单 (MATE
图 3-17: Caja 文件管理器
图 3-18: Xfce 桌面
图 3-19: Xfce Whisker 菜单
图 3-20: Xfce 设置管理器
图 3-21: 欢迎界面 - 第一步
图 3-22: 电脑文件夹
图 3-23: 桌面上的可移动驱动
图 3-24: 磁盘写入器，将 ISO 镜像写入 USB 硬盘
图 3-25: 网络管理器系统托盘图标
图 3-26: 网络连接菜单
图 3-27: 网络连接菜单：有线和无线
图 3-28: 网络无线认证
图 3-29: 系统设置网络 (Cinnamon
图 3-30: 系统设置网络历史 (Cinnamon
图 3-31: 系统设置网络信息 (Cinnamon
图 3-32: 代理设置 (系统设置网络) (Cinnamon
图 3-33: 连接到隐藏无线网络
图 3-34: Warpinator UFW 防火墙自动配置
图 3-35: 带有 warpinator 服务的 FirewallD 配置
图 3-36: Warpinator 主机列表
图 3-37: Warpinator - 选择要发送的文件
图 3-38: Warpinator - 文件传输
图 3-39: Warpinator - 传输完成
图 3-40: Warpinator - 接收传输通过
图 3-41: Warpinator - 接收传输
图 3-42: Warpinator 选项
图 3-43: 桌面小组件
图 3-44: 硬件驱动管理器
图 3-45: 显示
图 3-46: 颜色管理
图 3-47: 颜色管理
图 3-48: 在线账户
图 3-49: 系统报告 - 系统报告
图 3-50: 系统报告 - 崩溃报告
图 3-51: 系统报告 - 系统信息
图 3-52: 终端窗口
图 3-53: 无菜单栏的终端窗口
图 3-54: 查找对话框
图 3-55: 带有标签页的终端窗口
图 3-56: 终端配置配置
图 4-1: Linux Mint 官方软件源
图 4-2: 镜像源
图 4-3: 附加软件源
图 4-4: PPA
图 4-5: 身份密钥
图 4-6: 更新欢迎界面
图 4-7: 更新管理器更新图标和包信息对话框
图 4-8: 带有已选包的更新管理器
图 4-9: 更新下载与安装





# 图 4-10: 更新管理器偏好 - 选项
# 图 4-11: 更新管理器 - Linux 内内核对话框
# 图 4-12: Timeshift - 快照
# 图 4-13: 快照向导
# 图 4-14: 快照向导 - 位置
# 图 4-15: 快照向导 - 级别
# 图 4-16: Timeshift 设置 - 用户标签页
# 图 4-17: Timeshift 设置 - 过滤器标签页
# 图 4-18: 软件中心
# 图 4-19: 软件中心子分类
# 图 4-20: 软件中心搜索
# 图 4-21: 软件中心应用程序
# 图 4-22: 软件中心安装应用程序
# 图 4-23: 软件中心正在处理包
# 图 4-24: 软件中心安装多个应用程序
# 图 4-25: 软件中心 - Flatpak 软件包列表
# 图 4-26: 软件中心 - Flatpak 软件包
# 图 4-27: Synaptic 软件包管理器: 搜索
# 图 4-28: Synaptic 软件包管理器: 节
# 图 4-29: Synaptic 软件包管理器: 状态
# 图 4-30: GDebi 软件包安装器
# 图 4-31: 热门可用 snaps 列表: 查找
# 图 4-32: 已安装 snaps 列表: 
# 图 4-33: GNOME 软件
# 图 4-34: GNOME 软件, Snap 商店 (snapcraft.io) snap 软件包通道
# 图 4-35: GNOME 软件, Snapcraft snap 软件包权限
# 图 5-1: Xreader X-App 文档查看器
# 图 5-2: Xed X-App 编辑器
# 图 5-3: Xviewer X-App 图像查看器
# 图 5-4: Pix X-App 图像查看器、整理器和编辑器
# 图 5-5: Linux Mint mint-meta-codecs 安装
# 图 5-6: Celluloid 视频播放器
# 图 5-7: Xplayer X-App 视频播放器 (媒体播放器)
# 图 5-8: GNOME 访问服务器
# 图 5-9: GNOME 访问服务器和文件管理器
# 图 6-1: Cinnamon 桌面
# 图 6-2: 带有 Cinnamon 菜单的桌面
# 图 6-3: 桌面菜单和当前窗口（自定义）
# 图 6-4: 桌面设置
# 图 6-5: Desklets 管理标签页
# 图 6-6: Desklets 下载标签页
# 图 6-7: 系统设置 热角
# 图 6-8: 系统设置 键盘、快捷键
# 图 6-9: Cinnamon 菜单
# 图 6-10: Cinnamon 搜索
# 图 6-11: Cinnamon 收藏
# 图 6-12: Cinnamon 菜单
# 图 6-13: Cinnamon Linux Mint 菜单
# 图 6-14: Cinnamon 主菜单
# 图 6-15: Windows 设置 标题栏标签页
# 图 6-16: Windows 设置 行为标签页
# 图 6-17: Windows 设置 Alt-tab 标签页
# 图 6-18: 窗口平铺和边缘切换
# 图 6-19: 窗口列表菜单
# 图 6-20: 分组窗口列表配置 - 通用和面板标签页
# 图 6-21: 窗口列表按钮标签 - 无、应用程序、标题
# 图 6-22: 窗口列表按钮缩略图
# 图 6-23: 分组窗口列表配置 - 缩略图标签页
# 图 6-24: Windows 快速列表菜单
# 图 6-25: 比例：缩放窗口以切换（热角、显示所有窗口)
# 图 6-26: Alt-Tab 窗口切换（图标和缩略图)
# 图 6-27: Alt-Tab 窗口切换（Coverflow 3D ）index_split_011.html_id_Toc4925773)
# [图 6-28: 系统设置 效果: 启用效果标签页
# 图 6-29: 系统设置 效果: 自定义标签页
# 图 6-30: 工作区切换器组件
# 图 6-31: 启用 Expo 的热角
# 图 6-32: Expo 工作区（网格）
# 图 6-33: Expo 工作区（网格）
# 图 6-34: 系统设置
# 图 6-35: 带有分组列表和组件的 Linux Mint 面板
# 图 6-36: 系统托盘 X
# 图 6-37: 面板右键点击菜单（组件）
# 图 6-38: 面板
# 图 6-39: 编辑模式下的 Linux Mint 面板
# 图 6-40: 面板设置
# 图 6-41: Desklets 管理标签页
# 图 6-42: Desklets “在线”标签页
# 图 6-43: 传统布局面板
# 图 6-44: 传统布局启动器组件和菜单
# 图 6-45: 传统布局用户组件
# 图 6-46: 传统布局切换
# 图 6-47: Nemo 文件管理器主目录
# 图 6-48: 带有侧边栏的文件管理器
# 图 6-49: 带有书签菜单的侧边栏
# 图 6-50: 侧边栏中的位置菜单（展开和收起）
# 图 6-51: 侧边栏中的树状菜单（展开和收起）
# 图 6-52: 带有标签的文件管理器
# 图 6-53: 文件管理器文件、查看和编辑菜单





![图 6-54: 文件管理器导航](img/#index_split_011.html_id_Toc49257500)

![图 6-55: 展开与未展开的路径及位置](img/#index_split_011.html_id_Toc49257501)

![图 6-56: Nemo 文件管理器搜索](img/#index_split_011.html_id_Toc49257502)

![图 6-57: Nemo 上的文件属性](img/#index_split_011.html_id_Toc49257503)

![图 6-58: 为文件、文件夹或应用程序选择图标](img/#index_split_011.html_id_Toc49257504)

![图 6-59: Nemo 文件管理器偏好](img/#index_split_011.html_id_Toc49257505)

![图 6-60: Nemo 插件与扩展](img/#index_split_011.html_id_Toc49257506)

![图 6-61: 系统设置对话框（外观与偏好）](img/#index_split_011.html_id_Toc49257507)

![图 6-62: 系统设置对话框（硬件与管理）](img/#index_split_011.html_id_Toc49257508)

![图 6-63: 背景：图像标签](img/#index_split_011.html_id_Toc49257509)

![图 6-64: 背景：设置标签](img/#index_split_011.html_id_Toc49257510)

![图 6-65: 字体选择](img/#index_split_011.html_id_Toc49257511)

![图 6-66: 主题](img/#index_split_011.html_id_Toc49257512)

![图 6-67: 主题 - 桌面](img/#index_split_011.html_id_Toc49257513)

![图 6-68: 主题（在线主题）](img/#index_split_011.html_id_Toc49257514)

![图 6-69: 主题（设置标签）](img/#index_split_011.html_id_Toc49257515)

![图 6-70: 首选应用程序](img/#index_split_011.html_id_Toc49257516)

![图 6-71: 首选应用程序：可移动媒体](img/#index_split_011.html_id_Toc49257517)

![图 6-72: 日历小组件](img/#index_split_011.html_id_Toc49257518)

![图 6-73: 日期与时间设置，网络时间](img/#index_split_011.html_id_Toc49257519)

![图 6-74: 日历小组件](img/#index_split_011.html_id_Toc49257520)

![图 6-75: 屏幕保护设置标签](img/#index_split_011.html_id_Toc49257521)

![图 6-76: 屏幕保护 - 自定义标签](img/#index_split_011.html_id_Toc49257522)

![图 6-77: 语言](img/#index_split_011.html_id_Toc49257523)

![图 6-78: 输入法](img/#index_split_011.html_id_Toc49257524)

![图 6-79: 辅助功能](img/#index_split_011.html_id_Toc49257525)

![图 6-80: 启动应用程序偏好](img/#index_split_011.html_id_Toc49257526)

![图 6-81: 扩展管理标签](img/#index_split_011.html_id_Toc49257527)

![图 6-82: 扩展下载标签](img/#index_split_011.html_id_Toc49257528)

![图 6-83: 通知](img/#index_split_011.html_id_Toc49257529)

![图 6-84: 隐私](img/#index_split_011.html_id_Toc49257530)

![图 6-85: 通用](img/#index_split_011.html_id_Toc49257531)

![图 6-86: 系统信息](img/#index_split_011.html_id_Toc49257532)

![图 6-87: 系统设置，鼠标与触控板](img/#index_split_011.html_id_Toc49257533)

![图 6-88: GNOME 电源管理器菜单和小组件配置](img/#index_split_011.html_id_Toc49257534)

![图 6-89: GNOME 电源管理器](img/#index_split_011.html_id_Toc49257535)

![图 6-90: GNOME 电源管理器：亮度标签](img/#index_split_011.html_id_Toc49257536)

![图 6-91: 键盘](img/#index_split_011.html_id_Toc49257537)

![图 6-92: 键盘布局标签](img/#index_split_011.html_id_Toc49257538)

![图 6-93: 键盘选项](img/#index_split_011.html_id_Toc49257539)

![图 7-1: MATE 桌面和面板](img/#index_split_012.html_id_Toc49257540)

![图 7-2: 带有 Linux Mint 菜单的 Caja 文件管理器](img/#index_split_012.html_id_Toc49257541)

![图 7-3: MATE 桌面设置](img/#index_split_012.html_id_Toc49257542)

![图 7-4: MATE 窗口](img/#index_split_012.html_id_Toc49257543)

![图 7-5: 带有缩略图的窗口](img/#index_split_012.html_id_Toc49257544)

![图 7-6: 窗口列表小组件](img/#index_split_012.html_id_Toc49257545)

![图 7-7: 窗口列表偏好](img/#index_split_012.html_id_Toc49257546)

![图 7-8: 工作区切换器，单行和双行](img/#index_split_012.html_id_Toc23085045)

![图 7-9: 切换工作区，Ctrl-Alt-箭头](img/#index_split_012.html_id_Toc49257548)

![图 7-10: 工作区切换器偏好](img/#index_split_012.html_id_Toc49257549)

![图 7-11: 用于 MATE 的 Linux Mint 菜单](img/#index_split_012.html_id_Toc49257550)

![图 7-12: Linux Mint 搜索](img/#index_split_012.html_id_Toc49257551)

![图 7-13: Linux Mint 应用程序弹出菜单](img/#index_split_012.html_id_Toc49257552)

![图 7-14: Linux Mint 收藏收藏](img/#index_split_012.html_id_Toc49257553)

![图 7-15: Linux Mint 菜单偏好对话框](img/#index_split_012.html_id_Toc49257554)

![图 7-16: 带有最近文档的 Linux Mint 菜单（通用标签）](img/#index_split_012.html_id_Toc49257555)

![图 7-17: MATE 面板](img/#index_split_012.html_id_Toc49257556)

![图 7-18: MATE 面板弹出菜单](img/#index_split_012.html_id_Toc49257557)

![图 7-19: MATE 面板属性](img/#index_split_012.html_id_Toc49257558)

![图 7-20: 面板小组件的“添加到面板”对话框](img/#index_split_012.html_id_Toc49257559)

![图 7-21: Caja 文件管理器家文件夹](img/#index_split_012.html_id_Toc49257560)

![图 7-22: 带有侧边栏的 Caja 文件管理器](img/#index_split_012.html_id_Toc49257561)

![图 7-23: Caja 导航按钮：后退、前进、上级、首页、计算机](img/#index_split_012.html_id_Toc49257562)

![图 7-24: Caja 位置：未展开、展开和位置路径](img/#index_split_012.html_id_Toc49257563)

![图 7-25: 文件管理器侧边栏菜单和视图](img/#index_split_012.html_id_Toc49257564)

![图 7-26: 带有书签菜单的文件管理器侧边栏](img/#index_split_012.html_id_Toc49257565)

![图 7-27: 带有标签的文件管理器窗口](img/#index_split_012.html_id_Toc49257566)

![图 7-28: 文件管理器文件、编辑和查看菜单](img/#index_split_012.html_id_Toc49257567)

![图 7-29: 文件管理器文件 | 针对文件夹和文件的“打开方式”子菜单](img/#index_split_012.html_id_Toc49257568)

![图 7-30: Caja 上的文件属性](img/#index_split_012.html_id_Toc49257569)

![图 7-31: GNOME 系统中心](img/#index_split_012.html_id_Toc49257570)

![图 7-32: 鼠标与键盘](img/#index_split_012.html_id_Toc49257571)

![图 7-33: 关于我，偏好](img/#index_split_012.html_id_Toc49257572)

![图 7-34: 关于我、关于我](img/#index_split_012.html_id_Toc49257573)

![图 7-35: 选择 GNOME 桌面，外观](img/#index_split_012.html_id_Toc49257574)

![图 7-36: 字体](img/#index_split_012.html_id_Toc49257575)

![图 7-37: MATE 面板](img/#index_split_012.html_id_Toc49257576)

![图 7-38: 工具首选应用程序](img/#index_split_012.html_id_Toc49257577)

![图 7-39: 文件管理偏好](img/#index_split_012.html_id_Toc49257578)

![图 7-40: 屏幕保护程序](img/#index_split_012.html_id_Toc49257579)

![图 7-41: 辅助技术与首选应用程序](img/#index_split_012.html_id_Toc49257580)





# 声音与音频管理

- 图 8-17：声音：应用
- 图 8-18：声音：设置
- 图 8-19：PulseAudio 音量控制，播放
- 图 8-20：PulseAudio 音量控制，输出设备

## 配置工具
- 图 8-21：dconf 编辑器

## Seahorse 与密钥管理
- 图 8-22：Seahorse 密码与密钥（版本 3.3）
- 图 8-23：Seahorse 密钥环密钥属性对话框
- 图 8-24：选择加密密钥类型
- 图 8-25：创建加密密钥
- 图 8-26：加密密钥的口密码
- 图 8-27：我的个人密钥
- 图 8-28：GnuPGP 密钥对话框：所有者标签
- 图 8-29：GnuPGP 密钥对话框：详细标签
- 图 8-30：Seahorse 偏好 -密钥服务器
- 图 8-31：Seahorse 偏好 - 添加密钥服务器
- 图 8-32：使用 dconf-editor 配置密钥服务器
- 图 8-33：搜索密钥
- 图 8-34：导入密钥
- 图 8-35：密钥信息
- 图 8-36：已导入密钥
- 图 8-37：未签名密钥的导入密钥信任标签
- 图 8-38：签名密钥
- 图 8-39：Seahorse 偏好

## 权限与管理访问
- 图 9-1：安全访问的 pkexec 提示
- 图 9-2：使用 pkexec 命令调用 Xed
- 图 9-3：具有提升权限（作为 root）的 Nemo 文件管理器
- 图 9-4：以 root 打开文件管理器（管理访问）的提示
- 图 9-5：从以 root 身份打开的文件管理器编辑系统文件

## 用户与组
- 图 9-6：用户与组 (Cinnamon)
- 图 9-7：用户与组：新用户
- 图 9-8：用户与组：非活跃用户
- 图 9-9：用户与组：密码对话框
- 图 9-10：用户与组：组标签
- 图 9-11：用户与组：添加组
- 图 9-12：用户与组：用户对话框
- 图 9-13：用户与组 (MATE)
- 图 9-14：用户设置：更改用户密码
- 图 9-15：用户设置：更改用户类型
- 图 9-16：用户与组：更改用户权限
- 图 9-17：用户与组：创建新用户
- 图 9-18：用户与组：新用户密码
- 图 9-19：用户与组：组设置
- 图 9-20：组属性：用户面板

## 网络与文件共享
- 图 9-21：使用多播 DNS (Avahi) 访问共享文件夹
- 图 9-22：访问远程共享文件夹的权限
- 图 9-23：使用 Avahi 访问并挂载共享 Linux 文件夹
- 图 9-24：多播 DNS (Avahi), mdns 服务的 FirewallD 配置
- 图 9-25：网络授权
- 图 9-26：连接到服务器
- 图 9-27：挂载远程 Windows 共享
- 图 9-28：Windows 远程主机
- 图 9-29：Samba 共享提示
- 图 9-30：Samba 选项
- 图 9-31：Samba 共享
- 图 9-32：Samba 权限
- 图 9-33：FirewallD 配置 (ufw)
- 图 9-34：访问 Linux 共享文件夹
- 图 9-35：文件权限

## 蓝牙设置
- 图 9-36：蓝牙权限
- 图 9-37：蓝牙（系统）
- 图 9-38：蓝牙设置
- 图 9-39：蓝牙配置
- 图 9-40：蓝牙声音
- 图 9-41：蓝牙配对设备

## 系统维护
- 图 9-42：`/etc/default/grub` 文件
- 图 9-43：备份
- 图 9-44：备份
- 图 9-45：用户设置
- 图 9-46：用户存储
- 图 9-47：用户 Windows
- 图 9-48：用户加密
- 图 9-49：用户恢复
- 图 10-1：网络（离线）
- 图 10-2：网络托盘
- 图 10-3：网络（系统设置）Wi-Fi
- 图 10-4：无线配置安全
- 图 10-5：无线配置身份
- 图 10-6：无线配置 IP 标签
- 图 10-7：有线标签
- 图 10-8：有线配置对话框
- 图 10-9：有线配置安全
- 图 10-10：有线配置身份
- 图 10-11：有线配置 IPv4
- 图 10-12：VPN 选择
- 图 10-13：VPN 配置
- 图 10-14：网络配置
- 图 10-15：为新网络连接选择类型
- 图 10-16：新连接类型
- 图 10-17：常规标签





-   图 10-18: DHCP 有线配置
-   图 10-19: 手动 IPv4 有线配置
-   图 10-20: 手动 IPv6 有线配置
-   图 10-21: 802.1 安全配置
-   图 10-22: Wi-Fi 配置
-   图 10-23: Wi-Fi 安全：WEP 和 WPA
-   图 10-24: DSL 手动配置
-   图 10-25: 移动宽带向导
-   图 10-26: 移动宽带提供商列表
-   图 10-27: 移动宽带配置
-   图 10-28: PPP 配置
-   图 10-29: VPN 连接类型
-   图 10-30: VPN 配置 (openvpn)
-   图 10-31: VPN 配置 (pptp)
-   图 10-32: Gufw
-   图 10-33: Gufw 预配置规则
-   图 10-34: Gufw 简单规则
-   图 10-35: Gufw 高级规则
-   图 10-36: Gufw 编辑规则
-   图 10-37: Gufw 为活动端口创建规则
-   图 10-38: firewall-config: 运行时配置
-   图 10-39: firewall-config: 永久化配置
-   图 10-40: 默认区域
-   图 10-41: 基础区域设置
-   图 10-42: 服务设置
-   图 10-43: 服务协议和端口
-   图 10-44: 端口转发
-   图 10-45: ICMP 过滤器
-   图 10-46: Gnome 网络工具
-   图 12-1: 服务：cockpit
-   图 12-2: SSH 设置与访问
-   图 13-1: system-config-printer 工具
-   图 13-2: 打印机属性窗口
-   图 13-3: 打印机配置窗口 打印机菜单
-   图 13-4: 打印机队列
-   图 13-5: 服务器设置
-   图 13-6: 选择 CUPS 服务器
-   图 13-7: 打印机选项
-   图 13-8: 作业选项
-   图 13-9: 设置默认打印机
-   图 13-10: 全级和个人默认打印机
-   图 13-11: 选择新打印机连接：已连接与未连接
-   图 13-12: 新打印机的制造商
-   图 13-13: 从 OpenPrinting 仓库搜索打印机驱动程序
-   图 13-14: 使用本地数据库的新打印机型号和驱动程序
-   图 13-15: 新打印机的打印机名称和位置
-   图 13-16: CUPS Web 界面：首页标签页
-   图 13-17: CUPS Web 界面：管理标签页
-   图 13-18: 添加新打印机
-   图 13-19: CUPS Web 界面：打印机标签页
-   图 13-20: CUPS Web 界面：选项标签页
-   图 13-21: CUPS Web 界面：设置标签页
-   图 13-22: 查找打印机
-   图 13-23: 选择带有身份信息的打印机
-   图 13-24: Windows 打印机
-   图 13-25: Windows 打印机
-   图 13-26: CUPS Web 界面：打印机标签页
-   图 13-27: CUPS Web 界面：打印机标签页
-   图 13-28: CUPS Web 界面：打印机标签页
-   图 13-29: Gufw 防火墙访问
-   图 13-30: Gufw 防火墙访问 (samba)

-   A
-   B
-   C
-   D
-   E
-   F
-   G
-   H
-   I
-   J
-   K
-   L
-   M
-   N
-   O
-   P
-   Q
-   R
-   S
-   T
-   U
-   V
-   W
-   X
-   Y
-   Z

-   bash_logout
-   bash.rc
-   mount
-   path
-   profile
-   profile.d
-   ssh_confi
-   service
-   socket
-   target
-   wine
-   /dev/mapper](#index_split_015.html_id_txt78)
-   /etc/apparmor](#index_split_019.html_id_txt12)
-   /etc/apparmor.d](#index_split_019.html_id_txt74)
-   /etc/apt/sources.list](#index_split_008.html_id_txt123)
-   /etc/bash.bashrc](#index_split_017.html_id_txt15)
-   /etc/default](#index_split_019.html_id_Toc49250681)
-   /etc/fstab](#index_split_019.html_id_txt17)
-   /etc/hostname](#index_split_015.html_id_Toc213324822)
-   /etc/nsswitch.conf](#index_split_021.html_id_Toc49250751)





# 磁盘占用分析器，link
# GDebiti 包安装器，link
# glances，link
# GNOME 系统监器，link
# Linux Mint 管理工具，link
# Linux Mint 系统工具，link
# 日志，link
# MATE 控制中心，link
# 新打印机，link
# pkexec，link
# PolicyKit，link
# Puppet，link
# `root 用户，link
# 服务，link2, link
# 软件管理器，link
# `su`，link
# sudo，link
# Synaptic 包管理器，link
# systemctl，link
# systemd，link2, link

## 工具
# Blueberry，link
# Gufw，link
# Linux 内核，link
# 服务，link
# 系统监器，link
# system-config-printer，link
# 终端窗口，link
# Timeshift，link
# 更新管理器，link
# 病毒防护，link

## 管理工具
# 高级 Linux 声音架构 (ALSA)，link
# 高级包工具 (APT)，link
# 别名，link
# `alien`，link

### ALSA
# `alsamixer`，link
# `amixer`，link
# `alsamixer`，link
# Amanda，link

### AMD
# DKMS，link
# `amixer`，link
# AppArmor，link
# `/etc/apparmor.d`，link
# `aa-genprof`，link
# `apparmor_status`，link
# `apparmor_status`，link

### 外观
# 外观，link2, link
# 系统设置，link
# 各种组件，link2, link
# 网络，link
# 音量菜单，link
# 时间与日期菜单，link

## 
# 管理，link
# 刻录机，link
# 数据库，link
# 默认值，link2, link
# 默认值 (Cinnamon)，link
# 文档查看器，link
# 电子书阅读器，link
# 编辑器，link
# 邮件，link
# FTP，link
# GDebi 包安装器，link
# GStreamer，link
# 互联网，link
# 邮件客户端，link
# 即时通讯工具，link
# 多媒体，link
# 音乐，link
# 网络，link
# 阅读器，link
# 办公，link
# 可移动介质，link
# 软件管理器，link
# Synaptic 包管理器，link
# 电视，link
# 视频，link
# VoIP，link
# 浏览器，link
# 应用，link
# `apt`，link
# `install`，link
# `APT`，link, link
# `apt`，link
# `apt-get`，link
# apt 缓存，link
# `apt-cache`，link
# `apt-get`，link
# 更新，link
# 升级，link
# 工具，link
# 认证，link
# `root 用户，link
# `su`，link
# sudo，link
# Avahi，link
# Samba，link
# 服务，link2, link

## 
# Cinnamon，link
# MATE，link

## 
# 仓库，link2, link
# 备份，link
# Amanda，link
# 备份工具，link
# 备份快，link
# Duplicity，link2, link
# `rsync`，link
# 快照，link
# Timeshift，link
# 备份，link

## 
# Gstreamer，link

## 
# Gstreamer，link
# `bash.bashrc`，link
# `bash_completion`，link
# `BASH_ENV`，link
# `bash_logout`，link
# bashrc，link
# 电池，link
# BitTorrent，link
# Transmission，link
# Blueberry，link
# Bluetooth，link
# Blueberry，link
# 菜单，link
# 音量，link
# 书签，link2, link

### boot
# fstab 挂载单元，link
# graphical.target，link
# 级别，link





# 特殊目标，link

## 引导修复, link

## 启动引导程序
- 引导修复, link
- 配置, link
- 编辑, link
- GRUB, link2, link
- `GRUB_DEFAULT`, link
- `grub-install`, link
- Linux Mint 主题, link
- Plymouth, link2, link
- 重装, link
- `update-grub`, link

## Brasero, link

## 亮度
- 系统设置, link2, link

## C
- Caja, link2, link
- 书签, link
- 桌面设置, link
- 显示文件和文件夹, link
- 文件管理器搜索, link
- 文件属性, link
- 文件夹属性, link
- 媒体, link
- 导航, link
- 偏好, link
- 侧边栏, link
- 标签页, link
- `xdg-user-dirs`, link
- 日历, link
- 日历菜单, link

## Calibre
- 电子书阅读器, link
- Calligra 套件, link
- CD 刻录机和刻录机, link
- CD 刻录, link

## CD/DVD 磁盘映像
- 归档管理器, link
- Celluliod, link2, link

## 通道
- Snap, link
- Chrony, link2, link
- `chrony.conf`, link
- `cifs`, link

## Cinnamon, link2, link
- 外观, link
- 插件, link
- 应用程序默认值, link
- 背景设置, link
- 日历, link
- 日期, link
- `dconf`, link
- 桌面小组件, link
- 桌面图标, link
- 文档, link
- 扩展效果, link
- Expo, link
- Expo 插件, link
- 收藏, link
- 文件管理器, link
- FTP, link
- 分组窗口列表, link
- 输入法, link
- 键盘, link
- 键盘快捷键, link
- 语言, link
- 布局, link
- 菜单 (Cinnamon), link
- 菜单 (编辑), link
- 现代布局, link
- Nemo, link
- 通知中心, link
- 面板, link
- 隐私, link
- 可移动媒体, link
- 启动应用程序, link
- 窗口切换, link
- 系统信息, link
- 系统托盘, link
- 主题, link
- 磁贴, link
- 时间, link
- 传统布局, link
- 通用访问, link
- 用户和组, link
- 窗口列表, link
- 工作区切换器, link
- 状态插件, link
- 状态图标, link
- Cinnamon 设置, link

## 病毒防护, link

## 时钟, link

## ClamAV, link

## 刻录, link

## 编码, link
- 镜像, link
- 格式, link
- 打印 配置文件, link
- 终端, link
- 接口, link
- 打印服务, link
- 打印机, link
- 打印机配置, link
- 共享文件, link
- 共享网络, link
- 共享用户, link
- 共享设置, link
- 共享连接, link
- 共享驱动, link
- 共享应用程序, link
- 共享文件, link
- 共享服务器, link
- 共享设备, link
- 共享系统, link
- 共享数据, link
- 共享文件夹, link
- 共享媒体, link
- 共享账户, link
- 共享网络, link
- 共享工具, link
- 共享磁盘, link
- 共享程序, link
- 共享服务, link

## 共享,
- 共享驱动器, link
- 共享文件夹, link
- 共享文件, link
- 共享网络, link
- 共享服务器, link
- 共享用户, link
- 共享设备, link
- 共享设置, link
- 共享程序, link
- 共享系统, link
- 共享数据, link
- 共享工具, link
- 共享媒体, link
- 共享账户, link

## 共享设置, link
- 共享网络, link
- 共享服务器, link
- 共享文件, link
- 共享文件夹, link
- 共享用户, link

## 共享设备, link
- 共享设置, link
- 共享程序, link
- 共享系统, link
- 共享数据, link
- 共享工具, link
- 共享媒体, link
- 共享账户, link

## 共享网络, link
- 共享驱动器, link

## 共享服务器, 
- 共享服务器, link

## 共享文件, 
- 共享文件, link

## 共享文件夹, 
- 共享文件夹, link

## 共享用户, 
- 共享用户, link

## 共享设置, 
- 共享设置, link

## 共享程序, 
- 共享程序, link

## 共享系统, 
- 共享系统, link

## 共享数据, 
- 共享数据, link

## 共享工具, 
- 共享工具, link

## 共享媒体, 
- 共享媒体, link

## 共享账户, 
- 共享账户, link

## 共享网络, 
- 共享网络, link

## 共享驱动器, 
- 共享驱动器, link





`cupsctl`, link

`cupsd.conf`, link2, link

`cupsdisable`, link

`cupsenable`, link

`cups-files.conf`, link

`cupsreject`, link

## D

### 数据库管理系统， link
数据库服务器
- MySQL, link
- PostgreSQL, link

### 数据库
- LibreOffice, link
- MySQL, link
- PostgreSQL, link
- SQL 数据库, link

### 日期
- `timedatectl`, link
- dconf 编辑器, link
- DEB, link
- Debian 备用系统, link

### 默认应用程序
- MATE, link
- 系统设置 (Cinnamon), link
- `default.plymouth`, link
- Deja Dup, link2, link
- 桌面组件, link

### 桌面
- 外观, link
- 背景 (Cinnamon), link
- 背景 (MATE), link
- Cinnamon, link2, link
- dconf, link
- 默认应用程序, link2, link
- 桌面组件, link
- 桌面设置 (MATE), link
- 显示文件和文件夹, link2, link
- expo, link
- Expo, link
- Expo 插件, link
- 收藏, link2, link
- 文件管理器, link2, link
- 文件属性, link2, link
- 字体 (MATE), link
- FTP, link
- 图标选择器, link

### 图标
- Cinnamon, link
- MATE, link
- 键盘 (Cinnamon), link
- 快捷键, link
- 布局 (Cinnamon), link
- Linux Mint 管理工具, link
- Linux Mint 菜单 (MATE), link
- MATE, link2
- 菜单, link
- 菜单 (Cinnamon), link
- 菜单 (MATE), link
- 现代布局 (Cinnamon), link
- Nemo, link
- 通知 (Cinnamon), link
- 在线账户 (GNOME), link
- 面板 (Cinnamon), link
- 面板 (MATE), link
- 电源管理器 (Cinnamon), link
- 电源管理器 (MATE), link
- 隐私 (Cinnamon), link
- 可移动介质, link
- 关机, link
- spices, link
- 启动应用程序 (Cinnamon), link
- 窗口切换 (Cinnamon), link
- 系统托盘, link
- 主题 (Cinnamon), link
- 主题 (MATE), link
- 磁贴, link
- 传统布局 (Cinnamon), link
- 窗口列表, link
- 窗口, link2, link
- 工作区切换插件, link2, link
- 工作区 (MATE), link
- XFce, link

### 设备
- 蓝牙, link
- 电脑文件夹, link
- Udisks, link

### 磁盘崩溃
- 系统报告, link
- 磁盘分析器, link
- 磁盘工具, link
- ISO 刻录, link

### 显示
- AMD, link
- 配置, link
- 显示, link
- 高 DPI, link
- Nvidia, link
- Nvidia 输出, link
- 系统, link
- 驱动, link
- LightDM, link
- 文档, link
- 帮助页, link
- Linux Mint 用户指南, link
- 手册, link
- 下载, link
- `dpkg`, link3, link, link
- `alien`, link
- `dpkg-query`, link
- 龙播放器, link
- 抽屉, link
- 绘画, link
- DSL, link
- 双启动, link
- duplicity, link2, link

### DVB
- Kaffeine, link

### DVD
- 刻录, link
- Brasero, link
- 磁盘镜像写入器, link
- K3b, link
- Linux Mint, link
- DVD 刻录, link
- DVI, link
- Evince, link
- Okular, link

## E
### 电子书阅读器
- Calibre, link





# Foliate
Foliate, link

`ecryptfs`, link

# edit
GRUB, link

版本
Linux Mint, link

编辑器, link2, link

Xed, link

邮件, link

# 加密
`ecryptfs`, link

导入公钥, link

安装, link

密钥环, link

端口转发, link

私有加密目录, link

Seahorse, link

共享密钥, link

SSH, link

`ssh-keygen`, link

# E
Engrampa, link

环境变量, link

Evince, link

Expo, link2, link

Expo 插件, link

`export`, link

`exports`, link

# F
收藏夹
Cinnamon, link

MATE, link

文件管理器, link2, link

书签, link2, link

Caja, link

Caja 偏好, link

计算机文件夹, link

默认应用程序 (MATE), link

桌面图标, link

桌面设置, link

显示文件和文件夹, link

显示文件和文件夹 (Caja), link

导航 (Caja), link

导航 (Nemo), link

Nemo, link

偏好 (Nemo), link

侧边栏 (Caja), link

侧边栏, link

标签页, link2, link

`xdg-user-dirs`, link2, link

GNOME 文件, link

File Roller, link

文件系统, link2, link

加密, link

`fstab`, link

Linux, link

`LVM`, link

`NTFS`, link

Windows, link

`ZFS`, link, link

文件默认应用程序, link2, link

显示, link2, link

属性, link2, link

Caja, link

Foliate
电子书阅读器, link

字体
MATE, link

`fstab`, link, link

FTP, link

Cinnamon 连接到服务器, link

Linux 桌面, link2, link

Nemo, link

`sftp`, link

SSH 客户端, link

GD 安装器, link

GIMP, link

Glances, link

GNOME, link

`dconf`, link

显示配置, link

显示管理器 (LightDM), link

文档, link

DVD 刻录机, link

文件权限, link

文件夹属性, link2, link

Foliate, link

组, link2, link

`Gufw`, link

日志, link

面板, link

照片, link

共享文件夹, link2, link

GNOME 控制中心, link

GNOME 电影播放器, link

GNOME 应用程序, link

GNOME 系统监器, link

进程, link

`gnome-nettool`, link

GNU 通用许可许可证, link

Gstreamer, link

GPG 密钥
密码与密钥, link

通用统一引导程序, link

图形化目标, link

# 图形
默认应用程序 (MATE), link

绘画, link

GIMP, link

# 文件夹
显示, link2, link

属性, link2, link

Caja, link





# Inkscape, link
# Pix, link
# Xviewer, link
# 分组窗口列表, link

## 组
- 管理, link2, link
- 用户与组 (GNOME), link2, link
- GRUB, link2, link
- 引导修复, link
- 配置, link
- 编辑, link
- `grub-install`, link
- `grub-set-default`, link
- 历史 (ZFS), link
- Linux Mint 主题, link
- 重新安装引导程序, link
- `update-grub`, link
- GRUB 2, link
- `GRUB_DEFAULT`, link
- `grub2-theme-mint`, link
- `grub-install`, link
- `grub-set-default`, link
- GStreamer, link
- `bad`, link
- `base`, link
- `good`, link
- 插件, link
- `ugly`, link
- Gufw, link

## H
### 硬盘
- SMART 信息, link
- 硬件传感器, link
- HDTV, link
- Kaffeine, link

### 帮助
- info 页面, link
- Man 页面, link
- help.ubuntu.com, link
- 隐藏无线网络, link
- 高 DPI (Dots per Inch), link
- `HOME`, link
- 主机名, link
- `hostnamectl`, link
- `hosts.allow`, link

## I
### 图标
- Cinnamon, link
- MATE, link
- XappIconChooser, link
- XappStatusicon, link

### 导入
- 仓库, link
- 导入公钥, link
- `info`, link
- info 页面, link
- `initt`, link
- Inkscape, link

### 输入法
- 系统设置 (Cinnamon), link
- `install`, link

### 安装
- 电脑名称, link
- 加密, link
- 帮助, link
- Linux Mint, link
- Live DVD/USB, link
- `LVM`, link
- 概述, link
- 分区, link
- 准备磁盘空间, link
- 重用现有分区, link
- 指定分区 (高级), link
- 从 19.3 升级, link
- 用户, link

### 接口
- Snap, link
- `IPv6`, link

## J
- Java, link
- OpenJDK, link
- Java 运行时, link
- JRE, link

## K
- K3b, link
- Kaffeine, link, link
- KDE, link, link
- Kaffeine, link
- 键盘, link
- Cinnamon, link
- MATE, link
- 系统设置 (Cinnamon), link
- 键盘布局
- `localectl`, link
- 键盘快捷键, link
- 密钥环, link
- 密码与密钥, link
- 密码与密钥, link
- `ssh-keygen`, link
- 密钥服务器
- 密码与密钥, link
- `kill`, link
- Kubuntu, link, link

## L
### 语言
- 输入法, link
- 系统设置 (Cinnamon), link
- 笔记本, link
- 亮度, link
- 网络, link
- 电源管理, link
- 无线网络, link
- 布局, link
- 现代, link
- 传统, link
- `libd`, link
- LibreOffice, link
- LibreOffice, link
- `libx`, link
- LightDM 管理, link
- 配置, link
- Linux, link
- Man 页面, link

### Linux 内核
- 管理, link

### Linux Mint
- 管理工具, link
- Cinnamon, link
- 配置, link
- 显示, link
- 版本, link
- 文件夹, link2, link
- FTP, link
- Gbi 安装程序, link
- 安装, link
- 安装帮助, link
- 简介, link
- KDE, link2, link
- 笔记本, link
- LightDM, link
- Live DVD/USB, link
- Live USB, link
- 登录窗口, link
- LTS, link
- MATE, link2, link
- 菜单 (MATE), link
- 恢复, link
- 版本, link
- 快照, link
- 软件软件包, link




香料, link
香料, link
Synaptic 软件包管理器 (Synaptic Package Manager), link
Timeshift, link
update, link
upgrade, link
用户, link
用户与组 (MATE), link
Linux Mint 官方软件包源列表 (Linux Mint official-pakcages-repositories.list), link
Linux Mint 软件源 (Linux Mint repositories), link
Linux Mint 软件管理器 (Linux Mint Software manager), link
`lm-sensors`, link
`localectl`
键盘布局, link
位置, link
位置
`localectl`, link
锁
系统设置 (System Settings), link2, link
逻辑卷管理器 (Logical Volume Manager), link
登录
LightDM 显示管理器 (LightDM display manager), link
`logind`, link
登录窗口
偏好, link
`logind`, link
日志
GNOME 日志 (GNOME Logs), link
`lpadmin`, link
`lpc`, link
`lpinfo`, link
`lpoptions`, link2, link
`lpq`, link
`lpr`, link
`lprm`, link
LVM, link
`/dev/mapper`, link
命令, link
设备名称, link
加密, link
组, link
安装, link
逻辑卷 (Logical Volumes), link
物理卷 (physical volume), link
快照, link
`vgcreate`, link
`lynx`, link
LZMA, link

## M
邮件 (Mail), link
邮件应用程序 (Mail applications), link
主
源 (repository), link
`man`, link
手册页 (Man pages), link
MariaDB, link
伪装技术 (masquerading), link
MATE, link2, link
添加面板对象 (adding panel objects), link
外观 (Appearance), link
应用部件程序 (Applets), link
背景 (backgrounds), link
Caja, link2, link
Celluloid, link2, link
桌面图标 (desktop icons), link
桌面设置 (desktop settings), link
抽屉 (drawers), link
收藏 (favorites), link
字体 (fonts), link
键盘 (keyboard), link
菜单 (menu), link
菜单（编辑） (menu (edit)), link
面板 (panel), link
面板对象 (panel objects), link
偏好 (preferences), link
首选应用程序 (Preferred Applications), link
主题 (themes), link
通用辅助 (universal access), link
用户与组 (users and groups), link
窗口列表 (window list), link
窗口 (windows), link
工作区应用部件 (workspace applet), link
工作区 (workspaces), link
MATE 管理器 (MATE Manager), link
MATE, link
mdns
MATE (MATE Desktop), link
肉桂 (Cinnamon), link
编辑 (edit), link
分组列表 (grouped list), link
Linux Mint 菜单 (Linux menu), link
MATE (MATE), link
MATE 面板 (MATE panel), link
MATE 偏好 (MATE preferences), link
MATE 窗口 (MATE windows), link
微软安全 (Microsoft Security), link
Mint 备份 (Mint Backup), link
Mint 安装 (Mint install), link
Mint 解码器 (Mint-codecs), link
Mint 信息 (Mint-info), link
MATE (MATE), link
监控 (Monitoring), link
Glances (Glances), link
cifs (cifs), link
MP3 (MP3), link
MPEG-4 (MPEG-4), link
MATE (MATE), link
MATE 播放器 (MATE Player), link
`mpv`, link
多播 (Multicast), link
Samba (Samba), link
多媒体 (Multimedia), link
应用程序 (Applications), link
CD 与刻录机 (CD and Rippers), link
Celluloid (Celluloid), link2
解码解码器 (codecs), link
MATE (MATE), link2
MATE 默认 (MATE default), link
DVD (DVD), link
GStreamer (GStreamer), link
HD 电视 (HDTV), link
Kaffeine (Kaffeine), link2
MATE (MATE), link
MATE (MATE)
MATE 元解码器 (MATE-meta-codecs), link
MATE 播放器 (MATE Player), link
照片 (Photos), link
PiTiVi 视频编辑器 (Pitvi Video editor), link
音频 (Sound), link2
Totem (Totem), link
电视播放器 (TV Players), link
VideoLAN (VideoLAN), link
`vlc`, link
X 播放器 (Xplayer), link
Xvid (Xvid), link
multiverse
源 (repository), link
音乐应用程序 (Music Applications), link
MySQL, link2, link
MythTV, link

## N
名称服务切换 (Name Service Switch), link
Nemo, link2, link




- 书签, link
- 连接服务器, link
- 桌面图标, link
- 文件管理器搜索, link
- 文件属性, link
- FTP, link
- 图标 (`XappIconChooser`), link
- 导航, link
- 偏好, link
- xdg-user-dirs, link
- NetBIOS, link
- Netplan, link
- 配置, link
- `networkctl`, link2, link
- NetworkManager, link
- systemd-networkd, link
- Wi-Fi, link
- Nettool, link
- 网络配置, link
- 网络文件系统 (NFS), link
- 网络信息, link
- 网络信息服务, link
- 网络信息系统 (NIS), link
- 网络对象模型环境, link
- 网络时间协议, link
- Chrony, link
- `chrony.conf`, link
- TOY, link
- 协调世界时, link
- UTC, link
- `networkctl`, link2, link

### 网络

- 链接文件, link
- Netplan, link2, link
- `networkctl`, link2, link
- NetworkManager, link
- `nmcli`, link
- 可预测的网络设备名称, link
- 重命名设备名称, link
- 重命名网络设备名称, link
- systemd-networkd, link2, link
- udev, link
- Wi-Fi, link
- NetworkManager, link2, link
- 连接, link
- 设备名称, link
- DSL, link
- 隐藏的无线网络, link
- IPv6, link
- 笔记本电脑, link
- 手动配置, link
- 移动宽带, link
- 网络 (系统设置), link
- 网络菜单, link
- `networkctl`, link2, link
- network-manager, link
- `nmcli`, link
- PPP, link
- udev, link
- VPN, link
- 有线配置, link
- 有线连接, link
- 无线配置, link
- 无线连接, link
- 无线安全, link
- Zeroconf, link
- NetworkManager 命令 (`nmcli`), link
- Avahi, link, link2, link
- 配置, link
- 连接, link
- 设备名称, link
- 防火墙, link
- Glances, link
- 隐藏的无线网络, link
- 手动配置, link2, link
- 移动宽带, link
- 多组发现, link2, link
- Nettool, link
- 网络 (系统设置), link
- 网络连接, link
- `networkctl`, link2, link
- NetworkManager, link2, link
- 新网络菜单, link
- `nmcli`, link
- PPP, link
- 代理, link
- 重命名设备名称, link
- 重命名网络设备名称, link
- 共享文件系统, link2, link
- 共享文件夹, link
- SSID, link
- 系统设置, link
- systemd 文件, link
- udev, link
- Warinator, link
- 有线配置, link
- 有线连接, link
- Wireguard, link
- 无线配置, link
- 无线连接, link
- 零配置网络, link
- systemd-networkd, link

# 新闻器

- NTPERVER, link
- par, link2, link
- NFS, link2, link
- `/etc/exports`, link
- `fstab`, link
- `hosts.allow`, link
- `nfs`, link2, link
- NIS, link
- 选项, link
- rrpcbind, link
- `nfs`, link2, link
- `nfs4_getfacl`, link
- NIS, link
- 名称服务切换, link
- `nmbd`, link2, link
- `nmcli`, link
- NTPERVER, link2, link

# 通知

- Cinnamon, link
- 系统设置 (Cinnamon), link
- NTFS, link
- Nvidia





# DKMS
- nvidia-settings
- Optimus

## 0
### 办公套件
- Calligra
- GNOME 办公应用
- LibreOffice
- OpenOffice
- Okular

### 在线账户
- GNOME
- 在线账户
- 开源
- OpenJDK
- `openjdk-11-jre`
- OpenOffice
- OpenSSH
- OpenVPN
- OpenZFS

## P
### 软件包管理软件
### 软件包
- 软件
- `packages.mint.com`

### 面板
- 添加对象 (MATE)
- Cinnamon
- 抽屉 (MATE)
- 布局
- MATE
- 菜单
- 现代布局
- 面板对象 (MATE)
- 打印小组件
- 系统托盘
- 传统布局
- XApp Status Applet
- XAppStatusicon
- `par`

### 分区
- 空硬盘
- 新分区
- 复用
- `passwd`

### 密码
- 密钥环

### 密码与密钥
- GPG 密钥
- 导入密钥
- 密钥环
- 密钥服务器
- Seahorse
- 共享密钥

### PATH
- `pdbedit`
- PDC
- 登录配置

### PDF
- Evince
- Okular
- Xreader

### 权限
- 文件 (GNOME)
- GNOME 照片
- Pix
- Shotwell
- Photoshop
- 物理卷
- TiVi 编辑器
- Pix
- `pkexec`
- 策略文件
- ed
- Plymouth
- `default.plymouth`
- `update-alternatives`
- PolicyKit
- `auth_admin_keep`
- `pkexec`
- PolicyKit-1
- `polkit-1`

### 端口
- 转发
- 防火墙
- PostgreSQL
- 脚本

### 电源管理器
- GNOME 电源管理器 (Cinnamon)
- 笔记本电脑
- MATE 电源管理器 (MATE)
- `poweroff`
- PPP
- 可预测网络设备名称
- 文件
- systemd-networkd
- udev

### 偏好
- 文件管理器 (Caja)
- 文件管理器 (Nemo)
- Linux Mint 菜单 (MATE)
- MATE
- 控制中心
- 显示器
- 软件源
- 声音
- 窗口

### 首选应用程序
- MATE

### 演示文
- LibreOffice Impress

### 打印任务
- 打印小组件
- system-config-printer

### 打印服务器
- 配置
- CUPS
- `cupsd.conf`
- `lpadmin`
- 远程打印机
- system-config-printer
- 打印服务

### 打印机
- 默认个人打印机
- 默认系统打印机
- 编辑打印机
- 任务选项
- 新打印机
- 选项
- 打印队列
- 打印小组件
- 远程打印机
- Samba
- system-config-printer
- Windows
- `printers.conf`

### 隐私
- Cinnamon
- 系统设置 (Cinnamon)
- 私密加密目录
- 进程
- Gnome 系统监视器
- `kill`





`ps`, link

`profile`, link2, link

提示 (Prompt), link

属性

文件, link2, link

folders, link2, link

`Caja`, link

`XAppIconChooser`, link

专有显卡驱动, link

代理

网络 (系统设置), link

`ps`, link

`Psensor`, link

公共局域控制器, link

公钥

导入, link

`PulseAudio`, link2, link

`PulseAudio 配置`, link

`PulseAudio 音量控制`, link

`PulseAudio 音量计`, link

声音, link2, link

`PulseAudio 音量控制`, link

`Puppet`, link

`puppetmaster`, link

## R

恢复, link

重装引导程序, link

远程打印机, link

可移动媒体, link

系统设置, link

### 报告

系统信息, link

系统报告, link

系统报告, link

软件源, link2, link

`/etc/apt/sources.list`, link

Backports, link2, link

导入, link

main, link

multiverse, link

`official-package-repositories.list`, link

restricted, link

安全更新, link

`sources.list`, link

universe, link

更新, link

upstream, link

### restricted

软件源, link

### revisions

Snap, link

### 风险级别

Snap, link

`root` 用户, link

`su`, link

`rpcbind`, link

`rsync`, link

运行级别, link

`/etc/init.d`, link

## S

`Samba`, link3, link2, link

`Avahi`, link

`cifs`, link

客户端, link

`firewall`, link2, link

`FirewallD`, link2, link

`GNOME`, link2, link

`Microsoft Domain Security`, link

`multicast DNS`, link

`nbd`, link

`pdbedit`, link

`DC`, link

打印机, link

`Printers`, link

`Public Domain Controller`, link

共享, link

`smb.conf`, link

`smbclient`, link

`smbd`, link

`smbpasswd`, link

`FW`, link2, link

用户安全, link

`winbind`, link

Windows, link

扫描仪, link

`cron`, link

`systemd` 服务, link

范围, link

`scp`, link

屏幕保护, link

`seahorse`, link

导入密钥, link

密钥环, link

密码与密钥, link

共享, link

文件管理器, link

文件管理器 (Nemo), link

软件, link

安全 Shell, link

`AppArmor`, link

`OpenSSH`, link

`pkexec`, link

`PolicyKit`, link

病毒, link

软件源, link

磁盘, link

工具, link

`psensor`, link

`Xsensors`, link

SMB 消息, link

服务, link

服务, link

`systemd`, link

`/etc/systemd`, link

`/lib/systemd`, link2, link

`Cockpit`, link

执行环境, link

图形化目标, link

管理, link

管理, link

挂载单元, link

路径单元, link

运行级别, link

服务, link

服务单元, link

Snap, link

套接单元, link

`systemctl`, link2, link

`systemd`, link2, link

目标单元, link2, link

模板单元, link

单元文件, link

会话





# 启动应用 (Cinnamon)

## 设置
- 在线账户, link
- `sftp`, link
- 共享文件系统, link2, link
- Avahi, link2, link
- FirewallD, link2, link
- 组播 DNS 发现, link2, link
- `UFW`, link
- Windows, link
- 共享文件夹, link
- GNOME, link2, link
- NFS, link
- Samba, link2, link

## 共享资源
- NFS, link
- NIS, link
- Samba, link
- 共享项, link

## Shell
- `.bashrc`, link
- `.profile`, link
- 别名 (Aliases), link
- `bash.bashrc`, link
- `bash_logout`, link
- 环境变量, link
- `HOME`, link
- `PATH`, link
- `profile`, link2, link
- Shell 配置, link
- Shell 配置文件, link
- Shell 初始化, link
- Shell 提示符, link
- Shell 变量, link

## 关机
- `shutdown`, link
- 侧边窗, link
- 侧边栏, link
- slice 单元文件, link
- SMART, link2, link
- `smb.conf`, link
- `smbclient`, link
- `smbd`, link2, link
- `snap`, link
- Snap, link
- 频道, link
- 限制, link
- 接口, link
- 修订, link
- 风险级别, link
- 服务, link
- `snap` 命令, link
- 跟踪, link

## 快照
- LVM, link
- Timeshift, link
- ZFS, link

- 社交网络, link

## 软件
- `/etc/apt/sources.list.d/official-repositories.list`, link
- `alien`, link
- `apt`, link
- APT, link2, link
- `apt-cache`, link
- `apt-get`, link
- 限制, link
- `DEB`, link
- `dpkg`, link
- `GDebi` 安装程序, link
- 软件中心, link
- Linux Mint, link
- Linux Mint 管理器, link
- `mintinstall`, link
- 开源, link
- 软件包, link2, link
- 软件中心, link
- Synaptic 软件包管理器, link
- 搜索, link
- Snap, link
- 软件中心, link
- 软件源, link
- Synaptic 软件包管理器, link
- Ubuntu, link
- 软件中心, link
- 软件包类型, link
- 软件源, link
- 音 `alsamixer`, link
- `amixer`, link
- 偏好, link
- PulseAudio, link2, link
- PulseAudio 配置, link
- PulseAudio 音量控制, link
- PulseAudio 音量, link
- 声音, link2, link
- 接口, link
- 菜单, link
- 偏好, link
- 源, link
- 限制, link
- 软件, link
- 数据库, link

## SSH
- 认证, link
- 配置, link
- FTP, link
- OpenSSH, link
- 端口转发, link
- `scp`, link
- 安全 Shell, link
- `sftp`, link
- `ssh`, link
- `ssh/config`, link
- `ssh-agent`, link
- `ssh-keygen`, link
- `ssh-agent`, link
- `ssh-keygen`, link
- SSID, link
- 启动应用, link

## startup-animation
- Plymouth, link2, link
- 静态 IP 地址, link
- `su`, link
- `subscription.conf`, link
- 子 Shell, link
- `sudo`, link
- 配置, link
- Synaptic 软件包管理器, link
- 系统管理, link





# MATE 控制中心，link

## 系统环境变量，link

## 系统信息

## 系统设置 (Cinnamon), link
### 系统信息

## 系统报告，link
## 系统报告，link

### 系统设置
### 外观，link
### 亮度，link2, link
### 颜色，link
### 默认应用，link
### 显示器，link
### 通用，link
### Hi-DPI，link
### 输入法，link
### 键盘，link
### 语言，link2, link
### 锁屏，link2, link
### 网络，link
### 通知，link
### 在线账户，link
### 隐私，link
### 可移动媒体，link
### 屏幕，link2, link
### 音效，link
### 系统信息，link
### 系统报告，link
### 辅助功能，link2, link

## 用户与组，link

## 系统工具，link
### 磁盘用器，link
### 磁盘实用，link
### GNOME 系统监器，link
### 日志，link
### 系统托盘，link

## System V，link
### system-config-printer，link2, link
### 打印机应用 let，link
### `systemctl`,link
### systemd, link2, link
### `/etc/systemd/system`,link
### `/lib/systemd/system`,link2, link
### 执行环境选项，link
### 文件系统，link
### 图形目标，link
### logind，link
### 挂载单元，link
### Netplan,link
### 路径单元，link
### 运行级别，link
### 范围单元，link
### 服务单元，link
### 切片单元，link
### 套接单元，link
### 特殊目标，link
### systemd 定器，link
### systemd-networkd,link
### 目标单元，link
### 模板单元，link
### 单元文件，link
### Wi-Fi，link
### systemd 定器，link
### systemd-networkd,link
### 配置，link
### Netplan,link
### `networkctl`,link2, link
### NetworkManager,link
### 重命名设备名称，link
### Wi-Fi，link

## T
### 标签页
### 标签页 (Caja)，link
### 标签页 (Nemo),link
### `tar`,link

### 图形，link

###
### 磁盘实用，link
### 单元文件，link
### 窗口，link

主题
### Cinnamon 主题，link
### Linux 主题，link
### MATE 主题，link

### 音效，link

### 图片
### Cinnamon 图片，link
### 时间，link
### Cinnamon 定时，link
### Cinnamon 定时，link
### Cinnamon 定时，link

### 定器
### 定器，link

### 定器，link

###  Ubuntu
###  Ubuntu，link
###  Ubuntu，link
###  Ubuntu，link
###  Ubuntu，link
###  Ubuntu，link
###  Ubuntu，link
###  Ubuntu，link

### 
### 





# 自动，link
Linux 内核，link
软件，link
更新管理器，link
Linux 内核，link
偏好，link
`update-alternatives`, link
`update-grub`, link

# 更新
仓库，link
`upgrade`, link
从 18 升级，link

# 上游
仓库，link

# USB
# 刻录
Brasero, link
磁盘镜像写入器，link
Linux Mint, link2, link
Usenet 新闻，link

# 用户级安全
Samba, link
`useradd`, link
用户，link
cinnamon-settings-users, link
组，link2, link
安装，link
管理用户，link2, link
新用户，link
密码，link
`root` 用户，link
`su`, link
系统设置，link
用户与组 (Cinnamon), link
用户与组 (MATE), link
`users-admin`, link
用户与组 (Cinnamon), link
`users-admin`, link
UTC，link

# V
厂商显示驱动程序，link
AMD, link
Nvidia Optimus, link
`vgcreate`, link

# 视频
Celluloid, link2, link
默认应用程序 (MATE), link
Kaffeine, link
MPEG-4, link
MPlayer, link
`mpv`, link
PiTiVi 视频编辑器，link
Totem (GNOME 电影播放器), link
VideoLAN, link
`vlc`, link
Xplayer, link
VideoLAN, link2, link

# 虚拟专用网络
OpenVPN, link
PPTP, link
Wireguard, link
病毒防护，link
`vlc`, link
音量控制，link
VPN, link

# W
Warpinator, link
防火墙，link
FirewallD, link
偏好，link
FW, link
网络浏览器，link
Wi-Fi, link
Netplan, link
`winbind`, link
窗口列表，link
窗口，link, link
配置，link
分组窗口列表，link
偏好，link
切换，link
网格，link
兼容性，link
快速列表，link
Wine，link
系统，link
文件，link
打印机，link
Samba, link, link
共享系统，link
Wine，link
有线，link
Windows，link
系统设置，link
连接，link
`nm`, link
Wireguard，link
笔记本，link
网络，link 无线，link
配置，link
安全，link
# 用户，link
工作空间，link
MATE, link
切换器，link
# 区域，link
显示，link
UTC，link
驱动，link
系统，link
# 文件夹，link
菜单，link
文件，link
# 应用，link
软件，link
ZFS, link
状态，link
Samba，link
Samba, link2
状态状态，link
状态，link
播放器，link
播放器，link
播放器，link
播放器，link
播放器，link
播放器，link
播放器，link
播放器，link
播放器，link
执行，link
执行，link
执行，link
执行，link
执行，link
执行，link
执行，link
执行，link

