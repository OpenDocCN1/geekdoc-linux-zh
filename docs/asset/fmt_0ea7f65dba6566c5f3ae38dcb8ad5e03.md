
`apt-get install synaptic`

安装后，Synaptic 会将自己添加到 KDE 和 GNOME 系统配置菜单中，你可以从那里启动它。在提示你输入超级用户（SuperUser）密码后，Synaptic 将显示一个类似 YAST 的搜索界面，你可以浏览该界面以查看可用更新列表。左下角有四个软件包视图，包括你现在看到的搜索（Search）视图。部分（Sections）视图对应于 YAST 的设置，你可以在这里看到已安装和可用的软件包。点击状态（Status）显示此视图（见图 21.12）。

![](img/a5bd665678bc55d634220.png)

图 21.12 Synaptic 使管理软件包变得简单。具有可用更新的已安装软件包，复选框右上角有一个带有星号的填充。

## 使用 Red Carpet 更新你的系统

在较窄的左侧面板中，你会看到五个状态类别。要查看所有可用更新的软件包，点击“已安装（可升级）”（Installed (upgradable））。注意每个软件包左侧的复选框右上角填充了一个黄色的星号。点击任何软件包可以在右下角面板中查看描述。右键点击并在上下文菜单中选择“标记为升级”（Mark for Upgrade）。如果你想升级此列表上的所有内容，点击工具栏上的“标记所有升级”（Mark All Upgrades）。对于 RPM，Synaptic（以及 APT）同样可以通过添加和删除软件包来解决依赖关系问题，并在你提交更改之前通知你。

> 警告
> 务必检查 APT 是否在没有替换它们的情况下删除关键软件包，否则你可能会发现以后无法启动。在升级主要软件包之前，请备份你的系统和其他文件，如内核、引导程序、桌面环境、数据库等。

在提交任何新更新之前，点击自定义（Custom）视图按钮，然后点击“已标记更改”（Marked Changes）查看你正在安装、更新或删除的软件包列表。当你准备好运行 APT 时，点击工具栏上的“应用”（Apply）。APT 将下载所有标记的软件包并逐个安装。你将看到进度条并收到任何问题的通知。要在安装进行过程中获取更多信息，请前往设置、偏好，并勾选“在终端窗口中应用更改”。

## 使用 Red Carpet 更新你的系统

Ximian 最初是一家为 GNOME 桌面构建应用程序的公司，它做过非常棒的工作，尤其是 Evolution 个人管理器。Ximian 通过一个名为 Red Carpet 的更新产品开始从专注于 GNOME 扩展。由于 Ximian 在 SUSE 几个月前被 Novell 收，Novell 正在将 Ximian 产品整合到自己的产品线中。Red Carpet 现在是 ZENWorks Linux 管理的主要更新工具。在 Novell 的名下，Red Carpet 同样更新 Novel Open Enterprise Server。

与本章涵盖的其他工具一样，Red Carpet 简化了为你的发行版更新和安装软件的任务。某些术语有所不同。例如，Red Carpet 下载被称为“通道”（channel），你对它订阅新内容。尽管如此，你会发现 Red Carpet 易于理解和学习。

### 安装 Red Carpet

对于 APT，Red Carpet 无法通过 YaST 获取。要获取最新版本，请使用浏览器或 FTP 客户端访问 `ftp://ximian.com/pub/redcarpet2/`。选择你的版本和架构（32 位 Intel x86 或 64 位 x86_64）。

你将在该目录下看到几个 RPM 软件包。下载这三个：`red-<version>-architecture>.rpm`（这是在后台运行的守护进程）、`rug-<version>-architecture>.rpm` 和 `red-carpet-<version>-architecture>.rpm`。这三个文件的合并总大小约为 30MB，所以下载不需要很长时间。

## 第 21 章 保持系统为最新：软件包管理

你可以使用 YaST 安装这些软件包，但从命令行运行可能更好。以超级用户身份登录，切换到你的下载目录，并使用以下命令首先安装 Red Carpet 守护进程：

```
rpm red-<<architecture>.rpm
```

你将看到一些简短的活动，如果成功，rpm 程序将返回返回提示符。对命令行和 GUI 软件包重复此过程。

```
rpm rug-<<architecture>.rpm
```

```
rpm red-carpet-<<version>-<architecture>.rpm
```

每个软件包现在都应该在你的系统上安装并运行。Red Carpet 守护进程必须运行，其他程序才能工作，因此你的安装中还有最后一步。输入 `rcd` 完成安装。Red Carpet 守护进程现在将在后台运行。

### 从命令行运行 Red Carpet (rug)

使用 Red Carpet 更新系统最快的方法是通过 `rug` 命令实用工具。与安装新软件一样，你应该以超级用户身份使用 `rug` 登录。

只需在 shell 提示符处输入 `rug` 就会给你一个 `rug` 命令列表。当你第一次运行 `rug` 时，它会找到你的 RPM 数据库，这样它就知道系统中有哪些内容。要查看 Red Carpet 正在通过哪些通道更新系统，输入 `rug ch`。你会看到类似的内容：

```
subd? | Alias | Name

----------------+

redcarpet | Red Carpet 2

rcd-snaps | rcd snapshots

suse-92-x8664 | suse-92-x8664

suse-92-x8664-kernel | suse-92-x8664
```

现在如果你再次通过 `rug ch` 获取通道，你会看到：

| subd? | Alias | Name |
| :--- | :--- | :--- |
| Yes | redcarpet | Red Carpet 2 |
| I | rcd-snaps | rcd snapshots |
| Yes | suse-92-x8664 | suse-92-x8664 |

如果你没有订阅任何通道，你可以订阅 Red Carpet 以及 SUSE。

> 提示
> 为 APT 用户交付 SUSE 软件包的德国服务器也配置为 Red Carpet 服务。service-add http://open-carpet.org/services/gwd/

### 使用 Red Carpet GUI 更新

Red Carpet 图形界面应用程序的操作方式非常像 APT 的 Synaptic，而不是 YaST 的更新方式。它使用标签界面让你保持认知，而不会用一个页面上的大量材料淹没你。要在 KDE 中开始，前往系统、配置、Red Carpet。Red Carpet 会检查通道是否有新内容，并告诉你已安装应用程序是否有更新（或告诉你当前是新的）。

点击“可用软件”（Available Software）查看通道中你尚未安装的应用程序。使用“部分”（Section）按功能分解所有软件包，如果你正在寻找特定的内容，或者直接浏览字母列表。

如果你在这个标签上发现了想要的内容，选择它并点击“标记安装”。图标会出现，你的选择会被添加到侧的“等待操作”（Pending Actions）列表中（见图 21.13）。

当你确定了要安装或更新的应用程序后，点击“立即运行”（Run Now）开始。Red Carpet 将检查依赖性和所有执行列表。点击“继续”。

Red Carpet 下载并安装你的选择。完成后点击“确定”。你将返回主界面，可以在那里选择更多要安装的应用程序或退出。

> 提示
> SUSE Linux 发行版包含了这么多应用程序，有时你可能不知道自己安装了什么。即使你不是超级用户，Red Carpet 也能帮助你，只想看看是否安装了你在杂志上读到的那个应用程序。打开 Red Carpet 图形界面应用程序并点击“已安装的应用程序”（Installed Applications）。

![](img/a5bd665678bc55d634220eefc7819145_419_0.png)

**图 21.13** 在红毯（Red Carpet）中，你可以从左侧的等待操作（Pending Actions）列表中看到你所做的。

### 从源码编译软件

有些程序过于复杂或过于专业，程序员不愿费精力为它们创建 RPM。因此，程序员会将源代码归成 tar 包（tarball）并发送。通常，只需将代码提取到适当目录即可使应用程序运行，正如你在第 14 章“创建基础网站”中的某些博客工具以及第 17 章“安全文件传输”中的 Azure BitTorrent 客户端中所的那样。

其他程序在运行之前必须编译。本节将帮助你完成这一操作。在开始之前，你需要安装 GNU 编译器集合 (`gcc`) 来处理此任务。

首先，在编译新源码时，在你的主目录下创建一个名为 `source` 的新子目录。这将让你以用户身份编译代码，并防止任何坏的（甚至是恶意的）代码损坏你的系统。

现在的任务是将归档提取到新的 `~/source` 目录。你可以在 GNOME File Roller 或 KDE 的 Ark 中执行此操作，但在 shell 中会更快。切换到 `~/download` 文件夹（或你的源码包所在的位置）。根据原始文件的归档格式，输入以下命令之一：

```
tar xzvf <package>.tgz -C ~/source
```

```
tar xzvf <package>.tar.gz -C ~/source
```

```
tar xjvf <package>.bz2 -C /source
```

```
tar xjvf <package>.tar.bz2 -C /source
```

`tar/gzip` 归档使用了两种不同的扩展名，而最后两个是使用 BZip 归档的。`-C` 参数将归档文件提取到 `~/source` 目录。如果不确定使用了哪种归档方法，可以使用 `file` 命令帮助判断格式。输入 `file <package>`。

现在切换到 `~/source` 目录下解压后的包目录。寻找一个（通常全大写写以便你找到）名为 `README` 或 `INSTALL` 的文件。该文件将包含有关如何编译并使程序运行的详细说明。这些说明很可能是 Configure/Make/Make Install 过程的某种变体。这意味着你将首先运行一个名为 `configure` 的脚本，如下：

```
./configure
```

该脚本确认所有依赖项已满足且构建环境可靠。当脚本成功运行后，使用 gcc 自带的 `make` 工具编译程序：

```
make
```

最后，以超级用户（SuperUser）登录并使用相同的 `make` 工具安装程序：

```
make install
```

这将安全地安装你的新源码程序。

## 参考文献

- http://www.novell.com/coolsolutions/feature/11504.html—来自 Novell Cool Solutions 网站的全截屏 YaST 教程。
- http://www.suse.de/de-/YaST2-Package-Manager—旨在解释 YaST v8.1 带来的巨大变化，这里有很多关于 YaST 如何工作的良用信息。
- http://portal.suse.com/sdb/en/2003/04/82-susewatcher.html—SUSEwatcher 的文档，包括图标的说明。
- http://www.rpm.org—Red Hat 包管理系统的信息中心。该网站包含了 Ed Bailey 2000 年书籍《Maximum RPM》的在线版。
- http://linux01.gwdg.de/apt4rpm—在 SUSE Linux 上使用 apt 所需的所有信息。
- http://www.nongnu.org/synaptic—apt 的 Synaptic 图形界面。如果你等不及 apt 的新包，可以从这里下载当前源码。
- http://packman.links2linux.org—包含尚未纳入官方发行版中的包的优秀仓库。直接下载或使用 APT。
- http://speakeasy.rpmfind.net—RPMFind 搜索引擎的美国镜像站。
- http://rpmseek.com—在此处查找更多 RPM 包。
- http://freshmeat.net—Linux 及其他开源软件的巨大仓库，按接收日期组织。因此，“最新的肉类”位于顶部。

## 第五部分：高级系统管理

本部分包含

- **第 22 章** 管理启动过程和其他服务 399
- **第 23 章** 保护你的机器 417
- **第 24 章** 内核和模块管理 429
- **第 25 章** 设置网络和 Samba 443
- **第 26 章** 管理你的 Apache Web 服务器 459
- **第 27 章** 管理域名 477

## 第 22 章：管理启动过程和其他服务

### 本章内容

- 理解启动过程
- 系统服务与运行级别（Runlevels）
- 使用 YaST 运行级别编辑器在启动时控制服务
- 手动启动和停止服务
- 系统监控工具

要了解你的 Linux 如何工作，你需要...

### 理解启动过程

所有 x86 计算机——无论是运行 Intel 还是 AMD——启动方式都是相同的。BIOS 初始化风扇、微处理器芯片和电源。你的 BIOS 启动后，引导加载程序（bootloader）将接管该过程，直到内核启动。

当 BIOS 找到引导加载程序后，它会寻找 MBR，即硬盘上的第一个扇区。这是磁盘上最重要的扇区，因为引导加载程序代码（仅 446 字节）和分区表（64 字节）位于那里。在正确初始化硬件后，BIOS 可以将引导加载程序代码放入内存，并将启动过程移交给引导加载程序。位于 MBR 的引导加载程序代码只有一个工作——启动完整的引导加载程序（默认为 GRUB），并将其加载到内存。

#### 开始启动：从 BIOS 到引导加载程序

任何现代 BIOS 在搜索设备时都应该具有相当的灵活性，但它找到第一个可启动的卷后就会停止搜索。传统的顺序是软磁盘、硬盘、其他地方。近年来，可启动的光盘（CD-ROM）加入了 BIOS 选项并位于列表首位。这就是为什么在系统中添加新软件后，移除 SUSE 安装光盘是一个好主意。如果你不这样做，下次启动将进入光盘。这可能是因为光盘在其打开菜单上已将“从硬盘启动”设置为默认选项。

> 如果 BIOS 发现导致系统无法启动的硬件问题，它将通过一系列哔声向你报警。每个主板制造商都有不同的哔声生成系统，因此请查阅主板手册以了解代码，或联系你的 PC 供应商或制造商尝试解决问题。

### 理解启动过程

Linux 支持多种开源和专有的引导加载程序，但你通过 YaST 只能安装两个：高级统一引导加载程序 (GRUB) 和 Linux 加载器 LILO。自 v8.2 版本以来，GRUB 一直是 SUSE 的默认引导加载程序，而 LILO 仍在使用少数系统中运行，你可能想要使用它。

LILO 作为主要的 Linux 引导加载程序出现，似乎处于被 GRUB 取代的漫长过程中。LILO 能够很好地完成它的单项任务：引导到文件系统。它的配置性没有 GRUB 那么灵活。尽管如此，对于将根分区区安装在依赖 CPU 的 RAID 控制器（例如许多 Promise 或 Highpoint 控制器）、软件 RAID 或逻辑卷 (LVM) 管理磁盘的系统，它仍然是默认的引导加载程序。

这两种引导加载程序的主要区别在于它们找到和加载文件系统的方式。LILO 根据分区表所在的位置来查找文件系统。GRUB 可以读取并识别多种文件系统（ext2, ext3, ReiserFS, XFS, Minix 和 DOS）。

在 YaST 中，引导加载器模块位于“系统”页面。你可以在此界面将 LILO 设置为默认，并设置许多其他选项（见图 22.1）。如果你愿意，可以点击“编辑配置文件”直接编辑文件。

![](img/a5bd665678bc55d634220eefc7819145_426_0.png)

**图 22.1** GRUB 显示一个菜单，允许你从硬盘、软盘启动 SUSE Linux，或进入安全模式。安全模式会加载带有一组参数的内核版本，这使得在出现某些硬件问题时也能启动。如果你的电脑上还有另一个操作系统，GRUB 也会在启动菜单中列出该系统。8 秒后，GRUB 将启动菜单上的第一项；即 SUSE Linux。

> 注意
> 如果你愿意，在 GRUB 菜单的底部，你可以为内核指定选项。

你可以看到每个过程是如何在上一个过程的基础上构建的，允许不同的操作系统在同一块硬件上运行。

GRUB 菜单由 GRUB 配置文件控制，位于位于 `/boot/grub/menu.1`。图 22.2 显示了一个 `menu.1` 示例。

```
linux:" cat /boot/grub/menu.1

# Modified by YaST. Last modification on Sep 4 17:52:53 UTC 2005

ncolor white/blue black/light-gray

default 0

timeout 8

gfxmenu

change (hd0,0)/boot/message

### don't change this comment - YaST Identifier: Original name: linux###

SUSE LINUX 10.0

root (hd0,0)

kernel /boot/vmlinux root=/dev/sda2 uga=0x332 linux=0 resume=/dev/sda1

splash silent showpts

initrd /boot/initrd

### don't change this comment - YaST Identifier: Original name: floppy###

title floppy

chainloader (fd0)-1
```
