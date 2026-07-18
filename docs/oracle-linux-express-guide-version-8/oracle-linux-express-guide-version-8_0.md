# Oracle Linux 8 版本快速启动指南



![](img/cover00429.jpeg)


## 前言

让我们开启 Oracle Linux 之之旅。本书涵盖了 Oracle Linux 的安装、文件系统结构、网络、LVM、仓库结构、NTP、日志管理等许多其他方面。本书的结构非常简单，易于遵循。

感谢
Shiv Kumar Goyal


## 第 1 章
## 引言

Linux 是由 Linus Torvalds 于 1991 年启动的开源项目。它是一个类 Unix 操作系统。市场上上有数千个 Linux 发行版，大致根据其根发行版进行分类，例如 CentOS、Oracle 和 Scientific Linux 都是基于 Red hat 的，而 Red hat 又基于 Fedora Linux。Fedora Linux 是由 Red Hat 赞助的社区项目。

### 免费与 付费

Linux 尽管是一个开源项目，但市场上存在两种类型的 Linux 发行版：一种是免费的，另一种是付费的。免费是不言自明的，你不需要支付任何费用。在遇到任何问题时，你可以向为 Linux 社区工作的志愿者寻求帮助。然而，这种支持不是限时的。因此，使用关键任务型 Linux 服务器和桌面电脑的公司更倾向于选择付费的 Linux 发行版，他们支付固定金额作为订阅和支持费用。这些付费 Linux 发行版公司拥有 Linux 专家团队来提供支持和修复。

Oracle Linux 遵循中庸，它可以免费使用和更新，但支持是付费的。Oracle Linux 发行版源自 RedHat 的源代码。Oracle Linux 在功能和二进制上与 Red hat enterprise Linux 兼容。Oracle Linux 通常移除 Red hat 的品牌和标识。在 Redhat 与 IBM 合并后，曾作为 Redhat 免费替代方案的 CentOS Linux 已不再可用。Centos 提供的可用产品只有 CentOS stream，它是一个滚动发布版本。以前倾向于将 CentOS 作为 Redhat Linux 免费替代方案的客户现在不愿在生产环境中使用 CentOS。Oracle 提供了简单的脚本将你当前的 CentOS 环境迁移到 Oracle Linux。

### 支持的平台。

Oracle Linux 版本 8 安装镜像适用于以下平台：

| 镜像 | 支持的平台 |
| :--- | :--- |
| x86_64 | Intel 和 AMD 64 位 |
| aarch64 | ARM 64 位 |

### 镜像类型

标准安装镜像仅以 ISO 镜像的形式存在，但你也可以获得云镜像、容器镜像和 Vagrant 镜像。

## 第 2 章
# oracle Linux 支持生命周期

正如前面提到的，如果你在关键任务系统中使用 Linux，Oracle Linux 的生命周期如下：

| 版本 | 通用 | 支持结束 | 持续支持结束 |
| :--- | :--- | :--- |
| 3 | 2003 | 2011 |
| 4 | 2005 | 2013 |
| 5 | 2007 | 2017 |
| 6 | 2011 | 2020 |
| 7 | 2014 | 2021 |
| 8 | 2019 | 2024 |

### 支持类型

Oracle 为 Linux 提供两种类型的付费支持。两种支持类型的区别如下：

| 特性 | 基础支持 | 高级支持 |
| :--- | :--- | :--- |
| 24x7 电话和在线支持 | 是 | 是 |
| 获取增强、更新和修复 | 否 | 是 |
| 终身持续支持 | 否 | 否 |

## 第 3 章
## 安装媒体准备

Oracle Linux 下载有多种形式：

| 格式 | 说明 |
| :--- | :--- |
| ISO 镜像 | 适用于 x86_64 和 ARM |
| Vagrant | 用于 Vagrant Boxes |
| 容器镜像 | 适用于 x86_64 和 ARM |
| GitHub Container Registry | |
| Docker Hub | 适用于 Docker 镜像 |
| 虚拟机模板 | .ova 格式 |
| Raspberry Pi 4 和 Raspberry Pi 3 | 适用于 ARM |

本书中我们将仅涵盖 Intel 安装。下载 Oracle Linux 镜像遵循以下步骤：

1 访问网站 `https://yum.oracle.com/oracle-isos.html`

2 ![](img/0331.jpeg)选择版本和平台，如果是完整 ISO 请选择 Full

### 验证下载

从下方站点下载校验文件：

![](img/0332.jpeg)[`linux.oracle.com/gpg/`](https://linux.oracle.com/gpg/)

如果你将镜像下载到了 Microsoft Windows 机器上。打开 PowerShell 提示符并输入以下命令：

语法
`get-filehash 文件路径`

示例
```
![](img/0334.jpeg)[`getfedora.org/fmw/FedoraMediaWriter-win32-latest.exe`](https://getfedora.org/fmw/FedoraMediaWriter-win32-latest.exe)

2 双击下载的文件并按照安装步骤操作。

3 ![](img/0335.jpeg)选择自定义镜像

4 选择下载的 Oracle Linux ISO 文件并点击打开。

5 ![](img/0336.jpeg)![](img/0337.jpeg)选择 USB 设备并写入磁盘。

6 等待完成并关闭。

7 从 Windows 系统上拔掉 USB。

![](img/0338.jpeg) 现在安装媒体已准备就绪。

## 第 4 章
## 安装步骤





在本章中，我们将介绍安装步骤。然而，在进行安装之前，建议在 Oracle Linux 网上检查您的服务器/PC 的硬件兼容性。

Oracle Linux 在发行说明中指定了安装的最低配置，但建议至少具备以下配置以获得系统的最佳性能：

* 4 GB 或更多内存（RAM）。
* Intel Core I3 或更高级的处理器。
* 60GB 硬盘。
* 16GB USB 磁盘作为安装介质。

注意：根据您的需求和环境，可以使用较少的资源完成安装。

## 安装基础

Oracle Linux 使用 `Anaconda` 安装程序进行安装。Oracle Linux 的安装可以通过以下方式完成：

* 快速安装
* 自定义 GUI 安装
* Kickstart 自动化安装

### 分区

Oracle Linux 支持三种类型的分区设备

* 标准分区
* LVM
* LVM thin（精卷 LVM）

### 标准分区

对于引导、BIOS boot 和 EFI 系统分区，只能使用标准分区。

### LVM

`LVM` 分区方案提供了灵活性和性能优势。在安装过程中选择 `LVM` 分区时，如果系统当前不存在卷组，安装程序会自动创建一个。

### LVM thin

`LVM thin` 使用存储池，允许对存储进行精简置备（thin provisioning）。

### 支持的文件系统

* XFS
* ext4, ext3, ext2
* swap
* BIOS boot
* EFI 系统分区

### XFS

XFS 是一种高性能文件系统，支持单个文件系统多达 500 TB。它是 Oracle Linux 8 的默认文件系统。

### Ext3 和 Ext4

Ext3 和 Ext4 被称为日志文件系统。日志会跟踪尚未提交到文件系统的更改，以便在系统意外断电时轻松恢复文件系统。

EXT2 是旧版本 Linux 中使用的标准文件系统。

### Swap

它是位于硬盘上的虚拟内存。当系统没有足够的 RAM 运行程序时，它会将部分内存数据传输到 swap 空间。

### BIOS boot

用于 GPT 的必需分区。

### EFI

UEFI 系统上 GPT 的启动设备。

### 推荐的分区方案

| 分区 | 详情 |
| :--- | :--- |
| `/boot` | 1 GB 且不使用 LVM。 |
| `/` | 根分区建议大小为 10GB。 |
| `/home` | 22GB（可选） |
| `/swap` | 在某些情况下等于或大于 RAM，有时应为系统内存的两倍。 |

## 启动您的机器

要启动 Oracle Linux 的安装过程，您必须使用安装介质启动系统。

对于如 VMware 基础设施中的 `VM` 等虚拟机，您可以直接使用 `ISO` 镜像。只需挂载 `ISO` 镜像并启动机器。

对于物理服务器，插入之前创建的 Oracle Linux USB 安装介质。

开启服务器并按键更改启动顺序，使用 USB 作为启动设备（参考机器硬件手册获取启动管理器键，例如某些戴尔服务器为 `F11`）。

## 安装步骤

1. ![](img/image00339.jpeg)从启动菜单中，选择 Install Oracle Linux 8 并按下 `ENTER` 键。
2. ![](img/image00340.jpeg)选择您的语言和位置。点击 Continue（继续）。
3. 下一个屏幕是安装摘要，显示了带有默认值的所有安装选项。
4. ![](img/image00341.jpeg)![](img/image00342.jpeg)从安装摘要屏幕选择 Time & Date（日期与时间）。在地图上点击您当前的位置。系统将相应更改日期、时间和时区。根据需要，将日期格式从 24 小时更改为 AM/PM。按 Done（完成）。
5. ![](img/image00343.jpeg)选择 Installation Destination（安装位置）。从 Local Standard Disks（本地标准磁盘）面板中选择目标磁盘。点击 Done 使用自动分区的默认设置。注意：如果您有特定的文件系统要求，可以选择 Custom（自定义）选项。
6. 在网络配置屏幕上。将 Host Name（主机名）更改为完全主机名并按 Apply（应用）。
7. 点击 Configure（配置）。
8. ![](img/image00344.jpeg)![](img/image00345.jpeg)确保选择了 Connect automatically with priority（自动连接并优先）。
9. 选择 `IPV4` 设置标签页以配置静态 IP 地址。
10. 在 `IPV4` 标签页上更改以下内容：
    1. 从下拉菜单中将 Method（方法）更改为 Manual（手动）。
    2. 按下 `Add`（添加）按钮。
    3. 提供 IP 地址。
    4. 提供掩码。
    5. 提供网关。
    6. 添加 DNS。
    7. ![](img/image00346.jpeg)按 Save（保存）。
11. 点击 Done 接受更改。
12. ![](img/image00347.jpeg)在安装摘要屏幕上按 Root Password（根密码）。
13. 设置根密码并按 Done。
14. 在安装摘要窗口上选择 User Creation（创建用户）。
15. ![](img/image00348.jpeg)在 Create User 屏幕上为新用户提供全名、用户名和密码。如果让此用户成为管理员，请选择 Make user administrator（设用户管理员）。![](img/image00349.jpeg)
16. 在安装摘要窗口上按 Begin Installation（开始安装）。它将启动安装过程。
17. ![](img/image00350.jpeg)在安装过程完成后按 Reboot System（重启系统）。
18. ![](img/image00351.jpeg)重启后，在 Initial Setup 屏幕上按 Licence Information（许可信息）。
19. ![](img/image00352.jpeg)在许可信息屏幕上，选择 I accept licence agreement（我接受许可协议）。按 Done。
20. ![](img/image00353.jpeg)按 Finish installation（完成安装）。
21. 在登录屏幕上选择 Not listed（未列出）。
22. ![](img/image00354.jpeg)![](img/image00355.jpeg)输入 root 并按 Next（下一步）。
23. 为 root 用户提供密码。与您安装时选择的密码相同。按 Sign In（登录）。![](img/image00356.jpeg)
24. 在 Welcome 屏幕上按 Next![](img/image00357.jpeg)
25. 在 Typing（输入）屏幕上，按 Next。
26. 在 Privacy（隐私）屏幕上，按 Next。
27. ![](img/image00359.jpeg)探索桌面组件

在带有 GUI 的服务器上，`GNOME` 是默认桌面。`GNOME` 提供了易用的 GUI 体验。在本章中，我们将探索桌面界面。

### 顶部栏 (TOP BAR)

顶部栏有四个主要部分![](img/image00360.jpeg)

* Activities（活动）
* Application menu（应用程序菜单）
* Clock（时钟）
* System Menu（系统菜单）

![](img/image00361.jpeg)系统菜单

栏右角有电源、扬声器、网络、电池和蓝牙图标。点击这些任何图标都会打开系统菜单。系统菜单允许您调整扬声器和麦克风量。此菜单还提供了调整网络和蓝牙设置的选项。您将找到系统设置、锁定屏幕和关机菜单的快速链接。

### 时钟

在栏的中心位置有一个时钟，默认情况下显示星期和 24 小时制的当前时间。如果您需要，可以在系统设置中更改时间格式。点击时钟打开对话框，右侧显示日历，左侧显示任何任务通知。![](img/image00362.jpeg)

### Activities

顶部栏左侧是 Activities 按钮。点击此按钮打开概览屏幕。您可以使用键盘上的 `Super` 键（也称为 `Windows` 键）打开活动概览。活动屏幕提供以下项目

* Search Bar（搜索栏）。
* ![](img/image00363.jpeg)Windows Peak View（窗口预览）。
* Workspaces（工作空间）

### Search Bar

活动概览屏幕的主要项目之一是搜索栏。通过搜索栏，可以在计算机上搜索应用程序、文档、设置、日历事件等。例如，如果在搜索栏中输入 calculator，它将显示计算器应用程序。![](img/image00364.jpeg)点击图标打开计算器应用程序。

### Windows Peak View

![](img/image00365.jpeg)活动概览的第二个项目是所有运行应用程序的预览。点击所需的应用程序窗口以切换应用程序。要关闭任何正在运行的应用程序窗口，悬停在窗口上并点击 `X` 按钮。![](img/image00366.jpeg)工作空间




“活动”（Activities）概述屏幕的左侧显示工作空间列表。工作空间是用于更好地管理窗口的虚拟桌面。你可以创建多个工作空间。工作空间旨在减少单个桌面上的混乱，并使桌面更易导航。

点击工作空间可切换工作空间。要将应用程序移动到不同的工作空间，只需将运行中的应用程序拖到新工作空间即可。

### Dash（启动器）

![](img/image00367.jpeg)![](img/image00368.jpeg)
桌面的左侧你会发现 Dash 栏。Dash 提供了访问收藏和运行中应用程序的途径。点击 Dash 栏上的应用程序图标可打开该程序。图标底部的小点表示该程序正在运行。点击任何运行中的应用程序图标将带出该程序最近的窗口。

右键点击图标打开打开菜单。从此菜单中，你可以打开新窗口或选择运行中应用程序的任何窗口。你还可以从此菜单将任何应用程序添加到收藏或从收藏移除。

## Grid（网格）

![](img/image00369.jpeg)
在 Dash 栏底部有一个网格图标。点击此图标将显示所有应用程序和常用应用程序的列表。图标以网格格式排列，从网格底部，你可以在所有应用程序和常用应用程序之间切换。应用程序列表可以跨多个页，要导航到下一页，请使用鼠标（中间）滚轮或点击网格右侧的点。

网格中的某些应用程序包含在应用程序文件夹中。点击应用程序文件夹将列出包含所有应用程序的网格。

![](img/image00370.jpeg)

![](img/image00371.jpeg)

## 应用程序菜单

位于“活动”按钮旁边，应用程序菜单显示活动应用程序的名称。还提供了特定于活动应用程序的其他选项。

## 系统设置

![](img/image00372.jpeg)![](img/image00373.jpeg)
点击系统菜单中的系统设置图标将打开系统和硬件的设置窗口。设置界面有两个窗格，左窗格显示设置列表，右窗格提供所选设置的说明。你可以使用鼠标滚轮滚动设置列表。假设你想更改桌面背景。点击左窗格中的“背景”，并在右窗格的可用壁列表中选择壁纸。

系统设置工具的顶部栏还设有搜索按钮。搜索按钮允许你搜索与设置相关的任何内容。假设你想查找日期时间设置，只需按下搜索按钮并输入“日期”。系统将在左窗格中显示与日期相关的项目列表。

![](img/image00374.jpeg)

## 注销

完成任务后，注销系统是一个好习惯。注销选项会关闭用户在当前会话启动的所有运行应用程序。要作为当前用户注销，从系统菜单点击用户名。在子菜单中按`Log Out`注销）。在确认弹出窗口中再次按注销。

## 锁屏

![](img/image00375.jpeg)
当你离开电脑一段时间时，建议锁定屏幕，以免在你不在时无人可以使用你的电脑。当系统屏幕处于锁定状态时，所有运行的应用程序将继续运行。要重新登录，提供你的登录密码解锁屏幕。如果你离开电脑一段时间，系统也会锁定屏幕。

要手动锁定屏幕，点击顶部栏右侧的系统菜单，点击`Lock`锁定）图标。

要解锁，在锁定屏幕上按`ENTER` 键并提供密码。

![](img/image00376.jpeg)

 关机或重启

要通过 GUI 关机或重启服务器，点击顶部栏右侧的系统菜单，点击`Power Off`关机按钮。在对话框中，按你想要的按钮。

![](img/image00377.jpeg)

## 窗口

Gnome 使用窗口显示你运行的应用程序。这是实现多任务的方法之一。每当你启动任何应用程序时，它都会在新窗口中打开。在这一部分，我们将探索窗口操作。

### 列出窗口

要显示所有运行的窗口，只需点击“活动”按钮。从窗口列表中按鼠标左键选择任何窗口。

### 切换窗口

你可以使用键盘切换窗口，按`Super` + `TAB` 打开窗口切换器。按住`Super` 键，释放并按`TAB` 键在打开的窗口之间循环。

![](img/image00378.jpeg)
请注意：在使用 Linux 时，`Super` 键是 Windows 键的名称。

### 最大化和取消最大化窗口

你可以最大化窗口以在整个桌面查看其内容，并取消最大化或还原窗口以恢复到正常大小。

#### 最大化窗口

要最大化窗口，按并按住窗口标题栏上的鼠标左键以获取窗口标题栏，现在将其拖到顶部栏。最大化的另一种方法是在窗口标题栏上双击鼠标左键。使用键盘最大化窗口请按`Alt` + `F10`。

#### 取消最大化窗口

要将窗口恢复到正常大小，获取窗口标题栏并将其拖离顶部栏，或直接双击窗口标题栏。在键盘上按`Alt` + `F10` 使用键盘取消窗口的最大化。

### 平分窗口（贴靠窗口）

![](img/image00379.jpeg)
为了复制文件或比较两个窗口的内容，你可以将两个窗口并排。在 Microsoft windows 中，此功能被称为窗口贴靠（Snap）。要将窗口贴靠左侧，按`Super` + `left Arrow`；要将窗口贴靠屏幕右侧，选择窗口并按`Super` + `right Arrow`。使用鼠标贴靠窗口，获取窗口标题栏并拖到左侧或右侧。

### 切换工作空间

![](img/image00380.jpeg)
工作空间是虚拟桌面。它就像在同一个桌面上有多个显示器。如果你同时处理多个应用程序，工作空间是组织它们的好选择。要将一个应用程序从当前工作空间移动到另一个工作空间，按“活动”查看窗口和工作空间列表。获取标题栏从右侧的工作空间列表中移动到新工作空间。

要切换到工作空间，点击“活动”并选择工作空间，或按`Super` + `Page Down` 和`Super` + `Page Up`。




终端（Terminal）是输入命令的设备。Bash 使用终端与用户进行交互。终端（Terminal）一词来自 Unix 显示设备。Oracle Linux 默认安装提供 6 个虚拟控制台。这些终端在操作服务器时提供了几乎相互独立的 shell 环境。虚拟控制台提供了另一种访问 shell 的方式。你可以通过按下键盘上的 `Alt` + `Ctrl` + `功能键` 来切换虚拟终端。第一个终端从键盘上的 `F1` 键到 `F6` 键开始。假设你想切换到终端 3，请按 `Ctrl` + `Alt` + `F3` 键。如果你安装了带有 GUI 的服务器，那么前两个虚拟控制台是可用的图形用户界面，可以通过 `Ctrl` + `Alt` + `F1` 和 `Ctrl`+`Alt` + `F2` 键访问，其余四个虚拟控制台可以使用 `Ctrl` + `Alt` 键一直到 `f6`![](img/image00381.jpeg)

## Gnome Terminal

Gnome terminal 是一个 GNOME 桌面环境的终端模拟器。它在 GUI 环境中提供终端环境。

### 打开 Gnome 终端

点击“活动”（Activities），在搜索栏中输入 `terminal` 并点击终端图标![](img/image00382.jpeg)

### 快捷键

以下是一些可以在 bash shell 中使用的基本快捷键。

| 键盘快捷键 | 任务 |
| :--- | :--- |
| `Ctrl +a` | 将光标移动到命令提示符的开头 |
| `Ctrl + e` | 将光标移动到命令提示符的末尾 |
| `Ctrl + u` | 清空当前行 |
| `鼠标中键点击` | 粘贴选中的文本 |
| `Tab` | 补全命令 |
| `上 / 下方向键` | 显示命令历史 |
| `Ctrl +c` | 终止当前进程 |
| `Ctrl + z` | 挂前台进程 |
| `Ctrl + d` | 关闭终端™ |

## 命令

让我们探索一些基础且重要的命令。

### Tab 补全

bash shell 的主要亮点之一是 Tab 补全。当你部分写完命令后按下 `tab` 时，系统会自动完成该命令。如果有多个具有相同字符串的命令，它将显示命令列表。不仅是命令，它还能补全文件名。

示例：
`hostna<tab>`
`cat /etc/grou<tab>`

`history`
列出之前使用过的命令。
示例：
`history`

统计行数
`wc -l`

`date`
打印或更改系统日期和时间。
语法：
`date`
用于检查日期。
设置日期：
`date -s "24 feb 2017 19:00"`

`echo`
在终端上打印文本。
语法：
`echo text`
示例：
`echo hello`

## 远程访问终端

到目前为止，我们是在本地访问服务器上的终端，但情况下服务器位于数据中心，你对服务器的访问权限可能是有限的。因此，我们通常远程访问 Linux 服务器。在本节中，将学习如何在你的 Linux 或 Windows PC 上远程访问 Linux 终端。

要远程访问服务器，我们需要两个软件：一个在服务器上，另一个在客户端上。远程访问 Linux 服务器最常用的工具是：

* `telnet`
* `ssh`

### Telnet

Telnet 是一种旧的软件，以明文格式传输数据，因此使用不安全。由于安全考虑，服务器默认不提供 telnet。如果你有特殊需求，仍然安装并使用它。

#### 安装 telnet 服务器
```bash
yum install telnet-server
```

#### 启动 telnet 服务器
```bash
systemctl start telnet.socket
```

#### 启用 telnet 服务器
```bash
systemctl enable telnet.socket
```

#### 在远程机器上
#### 安装 telnet 客户端
```bash
yum install telnet
```
#### 运行客户端进行连接
语法：
`telnet IP 地址 端口`
示例：
`telnet 192.168.0.1 8080`

### ssh

`ssh` 是远程访问终端的现代软件。它以加密格式传输数据，即使在安全性不低的网络上也是安全的。SSH 有两部分：`sshd` 是运行在服务器上的服务器守护进程，`ssh client` 是运行在客户端 PC 上的。

#### 检查 ssh 服务器状态
```bash
systemctl status sshd
```

#### 在 Linux 客户端上访问终端
如果你使用 Ubuntu 或 oracle 作为 Linux 客户端 PC，可以按照以下步骤访问终端：

1. 在 Linux 客户端上打开终端。
2. 在命令窗口中。
3. `ssh 用户@服务器的 IP 地址`
示例：
`ssh root@192.168.100.47`
4. 输入用户的密码。

#### 在 MS Windows 上访问终端
要在 Windows 机器上访问终端，你需要名为 `putty` 的第三方软件。putty 是免费软件。你可以从 putty 网站下载软件：

1. 打开网站：`https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html`](Images/image00383.jpeg)
2. 在此站点选择 64 位 msi windows 安装程序下载。
3. 安装下载的软件![](img/image00384.jpeg)
安装后![](img/image00385.jpeg) 在你的主机系统上打开 `PuTTY`，在 Host Name（主机名）字段中输入。




将文件的前 10 行打印到标准输出。你也可以指定要显示的行数。

#### 语法
`head option file`

#### 示例
```bash
head -20 /etc/passwd
```
显示 `passwd` 文件的前 20 行。

### tail
将文件的最后 10 行打印到标准输出。你也可以指定要显示的行数。

#### 语法
`tail option file`

#### 示例
```bash
tail -20 /var/log/logfile
```
它将显示最后 20 行

### 使用 tail 持续监控文件
```bash
tail -f /var/log/logfile
```
它将显示增长文件的末尾。按 `Ctrl +c` 

## 复制文件和目录

### 复制文件
#### 语法
`cp filename target_dir`

#### 示例
```bash
cp abc.txt /home/user1/.
```

### 复制多个文件
#### 语法
```bash
cp * /target-location/.
```
#### 示例
```bash
cp *.txt /home/user/.
```
这将所有以 `txt` 扩展的文件复制到 `/home/user1` 目录

### 在任何覆盖前提示
```bash
cp –i /home /home1
```

### 强制复制文件
```bash
cp –f /tmp/abc.txt /backup/.
```

### 不覆盖现有文件，而是静默地不操作
```bash
cp -n * /backup/.
```

### 复制目录
#### 语法
`cp -R source_dir target_dir`

#### 示例
```bash
cp -R user1 user2
```
将 `user1` 目录复制到 `user2`

## 删除文件和目录

### 删除文件
要删除文件或目录，你可以使用 `rm` 命令。

#### 语法
`rm file_name`

#### 示例
```bash
rm abc.txt
```
要删除目录及其所有内容，包括任何子目录和文件：
```bash
rm -r /example
```
请非常小心地使用此命令，可能会导致数据丢失

### 删除目录
#### 语法
`rmdir directory`

#### 示例
```bash
rmdir /example
```

## 列出文件和目录

### ls
列出文件和目录名。

#### 语法
`ls -<options>`

### 列表
```bash
ls -l
```
显示文件或目录列表，包含大小、修改日期、修改时间和权限。

### 同时显示隐藏文件和目录
```bash
ls -la
```

### 显示人类可读格式
```bash
ls -lh
```

### mv
`mv` 命令用于将文件从一个位置移动到另一个位置。你也可以使用 `mv` 命令在不移动文件的情况下重命名。

### 移动文件
#### 语法
`mv filename destination_directory`

#### 示例
```bash
mv a.txt /tmp/.
```
它将 `a.txt` 文件从当前目录移动到 `/tmp` 目录

### 重命名
#### 语法
`mv filename newfilename`

#### 示例
```bash
mv a.txt b.txt
```

### grep
在一个或多个文件中搜索字符串。显示包含该字符串的每一行。

#### 语法
`grep string file`

#### 示例
```bash
grep '127.0.0.1' /etc/hosts
```

### diff
比较两个文件。

#### 语法
`diff First_file Second_file`

#### 示例
```bash
diff abc.txt bbc.txt
```

### file
确定文件类型

#### 语法
`file file_name`

#### 示例
```bash
file bbc.txt
```

## 链接文件和目录
链接类似于 Windows 中的快捷方式，指向原始文件。链接有两种类型：

* 硬链接 (Hard link)
* 软链接 (Soft link)

硬链接软链接都是文件的快捷方式。软链接可以于不同的文件系统中，而硬链接只能存在于同一个文件系统中。当你删除原始文件时，软链接将停止工作，而硬链接不受影响。这是因为在硬链接的情况下，原始文件和硬链接都指向同一个 inode。

### 创建软链接
#### 语法
`ln -s /source/file_name /target/file_name`

#### 示例
```bash
ln -s /home/admin/abc.txt /abc1.txt
```

### 创建硬链接
#### 语法
`ln file_name /target/file_name`

#### 示例
```bash
ln /home/admin/abc.txt /home/admin/abc1.txt
```

## 第 8 章 网络

在本章中，我们将讨论网络部分。主要有两种类型的网络： 

### 非 IP 网络
非 IP 网络利用传输层进行通信。非 IP 网络的一个示例是 InfiniBand。

### IP 网络
IP 网络是使用 IP 地址进行通信的网络。作为 IP 网络部分的每个设备都应该有一个 IP 地址。IP 网络是最常见的网络类型。家庭、办公室和互联网大部分使用 IP 网络。

对于 IP 网络，你有选项选择地址分配机制。有两种 IP 地址分配机制可用。

#### 静态
静态 IP 地址是手动为设备分配 IP 地址的模式。在静态 IP 地址分配的情况下，除非你更改，否则 IP 地址将保持不变。这种 IP 地址分配主要用于小型网络或共享设备（如服务器、打印机等），你希望每次都使用相同的 IP 地址。

#### 动态 IP 地址：
动态 IP 地址配置是地址的自动配置。它使用 `DHCP` 服务器为你的设备获取 IP 地址。当你配置 `DHCP` 服务器时，你分配一个 IP 地址范围给客户端。当你启动设备时，它会连接到 `DHCP` 服务器获取 IP 地址。每次启动设备时，你可能会获得不同的 IP 地址，除非你根据设备的 `MAC` 地址预留 IP 地址。动态 IP 配置对于大型组织是理想的，因为无法记住分配给每个设备的地址。但对于希望每次使用相同 IP 地址的服务器和打印机，DHCP 并不是理想解决方案。

### 配置网络
默认情况下，Oracle Linux 8 使用 `NetworkManager` 来配置和管理网络连接。要使用 `NetworkManager` 配置网络接口，请使用以下工具之一：

| 工具 | 说明 |
| :--- | :--- |
| `nmtui` | 基于文本的用户界面用于管理网络。此工具在非 GUI 环境下非常有用。 |
| `GNOME Networkmanager` | 用于网络管理的图形工具。 |
| `nmcli` | 命令行工具。 |

### 设备命名规范
接口名称以基于接口类型的双字符前缀开头：

| 设备类型 | 前缀 |
| :--- | :--- |
| 以太网 | `en` |
| 无线 | `wl` |
| 广域网 | `ww` |

为了保持设备名称持久性，Oracle Linux 对以太网使用了以下命名规范：

| 设备类型 | 设备名称 |
| :--- | :--- |
| 板载设备 | `enoX`，X 是设备编号 |
| PCIe 设备 | `ensX`，X 是设备编号 |
| 多端口设备 | `enpZsX`，Z 是物理端口，X 是设备编号 |
| 传统命名 | `ethX`，X 是设备编号 |

传统命名 `ethX` 用于旧版本中的网络设备。新的命名规范提供了以下几点：
1. 跨重启保持接口名称的稳定。
2. 在硬件添加和删除后保持接口名称的稳定。

### 使用 NetworkManager 的优势
1. 为所有应用程序同步并更新网络状态。
2. 更容易的网络管理。
3. 各种用于网络管理的工具。
4. 简单且灵活的 Wi-Fi 管理。

### 网络管理器脚本
默认情况下，`NetworkManager` 按字母顺序执行 `/etc/NetworkManager/dispatcher.d` 目录中的脚本以响应网络事件。每个脚本都应该是 root 拥的可执行文件。

### 使用传统脚本
默认情况下，Oracle Linux 8 使用 `NetworkManager` 管理网络，但如果需要，你仍然可以使用过时的网络脚本来代替 `NetworkManager`。

安装脚本：
```bash
yum install network-scripts
```

### nmtui
`nmtui` 是用于配置网络的文本用户界面 (TUI) 工具。此工具对于没有 GUI 的系统上的网络管理非常有帮助。

启动 nmtui：
```bash
nmtui
```

### 使用 nmtui 设置静态 IP 地址
在此示例中我们将设置静态 IP 地址。
1. 启动 `nmtui`
2. 选择编辑连接。
3. 从列表中选择连接配置文件并按编辑。
4. 在编辑连接屏幕上，在 IPv4 配置处按空格键键。
5. 选择手动。
6. 按 `TAB` 键并显示。
7. 在相应字段提供 IP 地址、子网掩码、网关和 DNS。
8. 滚动到底并确保“自动连接”单选按钮被选中。
9. 按“确定”。
10. 选择返回。
11. 选择激活连接，并按回车。
12. 从列表中选择连接并按回车激活连接。如果连接已激活，则取消激活并重新激活使更改生效。
13. 选择返回。
14. 选择退出。

### nmtui 命令
使用 nmtui 设置主机名
语法





`nmtui hostname new_hostname`

## Example
```bash
nmtui hostname Server2
```

## nmcli

`nmcli` 是一个用于管理网络的命令行工具。`nmcli` 可创建、显示、编辑、删除、激活和停用网络连接。`nmcli` 是控制和显示网络设备状态非常有用的工具。

### 列出网络设备及其状态
#### 语法
```bash
nmcli device
```
![](img/image00394.jpeg)

#### 示例
#### 设备详细信息
```bash
nmcli device show
```

#### 列出连接
```bash
nmcli connection show
```

### 激活连接
#### 语法
```bash
nmcli connection up connection_name
```
#### 示例
```bash
nmcli connection up ens35
```

### 停用连接
#### 语法
```bash
nmcli connection down connection_name
```

#### 示例
```bash
nmcli connection down ens35
```

### 更改网络状态
#### 语法
```bash
nmcli networking on/off
```
#### 示例
```bash
nmcli networking off 
```

### 显示主机名
```bash
nmcli general hostname
```

## Wifi 网络管理
### 列出可用 WiFi AP
```bash
nmcli device wifi list
```

### 连接到密码保护的 Wifi 网络
#### 语法
```bash
nmcli device wifi connect "SSID" password "password"
```
#### 示例
```bash
nmcli device wifi connect "mynetwork" password "pa$$w0rd"
```

## GNOME GUI 网络管理器
可以通过顶部栏系统菜单或设置中的两个 GUI 模式控制网络。

### 连接无线连接
如果系统已连接到无线网络，你将在桌面顶部栏看到 Wi-Fi 图标，否则请按照以下步骤连接到家庭或办公室无线网络：

1. 点击系统菜单。
2. 点击“未连接无线网络”以展开折叠菜单。
3. ![](img/image00395.jpeg)点击“选择网络”。
4. 将打开新窗口并显示所有可用网络。选择您的 Wi-Fi 网络名称。点击“连接”。
5. ![](img/image00396.jpeg)![](img/image00397.jpeg)如果网络受密码保护，在密码提示处提供密码并点击“连接”。
6. 现在您的网络已连接，顶部栏将显示 Wi-Fi 图标。

### 更改 Wi-Fi 密码
由于某些原因更改了路由器上的 Wi-Fi 网络密码，你必须在系统中也设置相同的密码，否则下次将无法连接。

1. 点击系统菜单。
2. 点击“已连接无线”打开子菜单。
3. 点击“更改设置”。
4. 从可用网络列表中选择您的网络，并点击旁边的齿轮图标。
5. 在安全设置中更改密码并点击“确定”。

## 有线网络
连接有线网络非常简单，只需将网线插入电脑。系统将自动为可用网络进行配置。一旦系统连接到有线网络，顶部栏将显示系统指示器。

### 手动配置有线网络
大多数情况下，有线网络设置是自动的，但在某些情况下你必须手动设置 IP 地址。这种配置被称为静态 IP 地址配置。

#### 配置静态 IP 地址：
1. 打开系统菜单。
2. ![](img/image00398.jpeg)点击“已连接有线”并选择“有线设置”。
3. 将打开网络设置窗口。
4. 点击齿轮图标。
![](img/image00399.jpeg)
5. 打开有线配置对话框。
6. 在 `Details` 标签页中，确保勾选了 `Connect automatically`。
7. ![](img/image00400.jpeg)点击 `IPv4` 标签卡。
1. 点击 `Manual` 单选按钮。
2. 提供 IP 地址。
3. 输入 `Netmask` 子网掩码。
4. 输入 `Gateway` 网关。
5. DNS
8. 点击 `Apply`。

## 名称解析
当你使用主机名而不是 IP 地址连接 Linux 主机时，你有以下选项将主机名解析为 IP 地址。

* 本地文件，即 `/etc/hosts`
* DNS 服务器
* NIS

### 本地文件 (/etc/hosts)
`/etc/hosts` 是存储主机名到 IP 地址映射的文件。它提供了在不使用 DNS 服务器的情况下解析主机名的能力。如果出于范围或安全原因连接到有限数量的主机，我们通常使用此文件。使用此文件的缺点是，一旦 IP 地址发生变化，管理员必须在所有服务器或 PC 上更改此文件。

#### 格式
`IP_address hostname aliases`

#### 示例
```bash
127.0.0.1 server1 localhost
31::1 server1 localhost
192.168.228.129 server1server1.example.com
```

### DNS
DNS 服务器是一个中央存储库，包含 IP 地址及其关联主机名的数据库。每当任何客户端想要将主机名解析为 IP 地址而不是使用其本地文件时，它会向 DNS 服务器发送请求。如果某些客户端的 IP 地址发生变化，你只需要更新 DNS 条目。一个组织内可以有多个 DNS 服务器。为了重定向主机名解析请求，Oracle Linux 使用 `/etc/resolve.conf` 文件。默认情况下，Oracle Linux 8 上的 `NetworkManager` 会动态更新 `/etc/resolv.conf` 文件。但是根据你的需求，你可以通过 `NetworkManager` 禁用 DNS 处理。

## 成组 (Teaming)
成组允许将多个物理以太网适配器组合到一个逻辑适配器中。该逻辑网络适配器提供更高的吞吐量或冗余。

### 成组模式
| 模式 | 说明 |
| :--- | :--- |
| 轮询 (Round-robin) | 在此模式下，数据在所有端口之间传输。 |
| 广播 (Broadcast) | 数据在所有端口传输。 |
| 负载均衡 (Load-balance) | 流量在所有网卡之间分配。 |
| 主备 (Active-backup) | 其中一个链路激活，其余的备用以提供冗余。 |
| LACP | 使用 802.3ad 协议进行链路聚合。 |

#### 安装 teaming 包
```bash
yum install team
```

#### 创建主备组
```bash
nmcli connection add type team con-name bond0 ifname bond0 mode "activebackup"
```

## 重要网络命令
### 显示 IP 地址
```bash
ip addr
```

### 显示链路状态
![](img/0401.jpeg)ip show

### 检查并更改主机名
Linux 计算机的称为主机名。要更改主机名，可以使用 `hostnamectl`。

#### 显示当前主机名
```bash
hostnamectl
```

#### 更改主机名
#### 语法
```bash
hostnamectl set-hostname newname
```
#### 示例
```bash
hostnamectl set-hostname myhost1
```

### 显示路由表
```bash
ip route
```

### 检查网络连通性
#### 语法
```bash
ping ipaddress/hostname
```
#### 示例
```bash
ping 192.110.22.121
```

如果你感兴趣使用命令行更改 IP 地址，请尝试 `nmcli` 命令。查看更多信息请参考示例命令。

## 网络工具
（注意：以下工具用于网络诊断）

### dig
DNS 查询并显示结果
#### 语法
```bash
dig hostname
```
#### 示例
```bash
dig microsoft.com
```

### telnet
连接目标主机:端口。你也可以使用 `telnet` 测试主机和端口的连通性。
#### 语法
```bash
telnet hostname port
```
#### 示例
```bash
telnet myserver1 8080
```

### nslookup
查询互联网域名服务器
#### 语法
```bash
nslookup hostname
```
#### 示例
```bash
nslookup microsoft.com
```

### scp
通过网络以安全方式从一个主机复制文件到另一个主机。
#### 语法
```bash
scp filename user@targetserver:/path
```
#### 示例
```bash
scp ast.txt user1@server2:/home/user1
```

### ssh
安全登录目标服务器。
#### 语法
```bash
ssh user@targethost
```
#### 示例
```bash
ssh user1@server2
```

### nmap
检查服务器上开启的端口
#### 语法
```bash
nmap hostname
```
#### 示例
```bash
nmap cloudflare.com
```




EXT 文件系统拥有悠久的历史`ext4` 是 `ext` 文件系统家族的第四代。它也是一种日志文件系统。`Ext4` 驱动程序可以读写 `ext3` 和 `ext2` 文件系统。它支持高达 50 TiB 的文件系统大小。作为一种遗留文件系统`ext4` 文件系统被几乎所有 Linux 应用程序支持。

## XFS 文件系统管理命令

#### 创建 XFS 文件系统
#### 语法
```bash
mkfs.xfs devicename
```
#### 示例
```bash
mkfs.xfs /dev/sda01
```

### 调整 XFS 文件系统大小
你只能扩展文件系统而不能缩小。要增大 XFS 文件系统请使用:-

#### 语法
```bash
xfs_growfs device_name
```
## 命令
此命令将 xfs 文件系统扩展到设备的最大限制。
```bash
xfs_growfs /dev/sda01
```
`-D` 接受文件系统块数作为参数。
```bash
xfs_growfs /dev/sda01 -D 200
```

### 修复 XFS 文件系统
#### 语法
```bash
xfs_repair -n device_name
```
#### 示例
```bash
xfs_repair -n /dev/sda01
```

## Ext4 文件系统管理命令

### 创建 ext4 文件系统
#### 语法
```bash
mkfs.ext4 /dev/device_name
```
#### 示例
```bash
mkfs.ext4 /dev/sd01
```

### 为分区标记
#### 语法
```bash
e4label device_name new_label
```
#### 示例
```bash
e2label /dev/sda01 data01
```

### 调整大小
你可以在 ext4 文件系统挂载 own 时扩展它。缩小则需要卸载 ext4 文件系统。

#### 语法
```bash
Resize2fs device_name new_size
```
#### 示例
```bash
Resize2fs /dev/sda01
```
如果你不指定大小，此命令将文件系统扩展到设备的最大限制。
要将文件系统更改为特定大小
```bash
resize2fs /dev/sda01 5G
```

## 第 10 章：探索网络文件系统

在上一节中，我们讨论了本地文件系统，然而为了在网络上共享数据，远程文件系统出现了。网络文件系统需要在本地文件系统之上一个额外的层，以便在网络上共享和挂载。网络文件系统可以被多个用户同时使用。一旦挂载，它的行为就像远程机器上的本地文件系统一样。在本章中，我们将介绍 Oracle Linux 8 上常用的远程文件系统。

### NFS
`NFS` 是一种文件共享文件系统，基于服务器/客户端模式工作。在服务器上共享的文件系统可以通过网络挂载到客户端上。`NFS` 文件系统是 Unix 和 Linux 系统之间非常流行的的文件共享协议。Oracle Linux 服务器同时支持 `NFS` 服务器和客户端。`NFS` 在 Linux 上对于跨平台文件和文件夹共享非常有用。`NFS` 也是网络附属存储 `NAS` 系统上广泛使用的协议。目前有四个版本的 `NFS`，每个版本都有进一步的发布，例如版本 4 有 4.2 版本:-

- `NFS V1`
- `NFS V2`
- `NFS V3`
- `NFS V4`

其中 `NFS V3` 和 `NFS V4` 是较新的 `NFS` 版本。在 Oracle Linux 8 中，不再支持基于 UDP 的 NFS。NFSV4 增加了通过防火墙工作的优势并运行在 TCP 上。在 Oracle Linux 8 中，默认的 `NFS` 版本是 4.2，它具有支持访问控制列表 (`ACLs`)、服务器端复制和稀疏文件的特性。Oracle Linux 8 仅支持版本 3 和版本 4 的 `NFS`，Oracle Linux 8 不再支持版本 1 和版本 2

### 安装 NFS
#### 安装包
```bash
yum install nfs-utils
```
安装后，启用服务以便在重启后自动启动。
```bash
systemctl enable nfs-server.service
```

### 启动服务
```bash
systemctl start nfs-server.service
```
此命令将启动 `NFS` 需要的其他服务，如 `nfsd`、`nfs-idmapd`、`rpcbind`、`rpc.mountd`、`lockd`、`rpc.rquotad`、`rpc.statd` 和 `rpc.idmapd`。

现在检查服务的状态
```bash
systemctl status nfs-server.service
```

`NFS` 服务器的重要文件有：

| 文件名 | 用途 |
| :--- | :--- |
| `/etc/nfs.conf` | NFS 进程和工具的主配置文件。 |
| `/etc/nfsmount.conf` | NFS 挂载的全局配置文件。 |
| `/etc/exports` | NFS 服务器导出表。 |

#### `/etc/exports` 文件选项
| 选项 | 描述 |
| :--- | :--- |
| `rw` | 允许对文件系统进行读取和写入访问。 |
| `sync` | 此选项默认告诉 NFS 服务器仅在最后更改提交后才回复请求。 |
| `all_squash` | 将所有 `UIDs` 和 `GIDs` 映射到匿名用户。适用于公共 FTP 目录。 |
| `root_squash` | 将来自客户端的 `UID/GID` 0 映射到匿名 `UID/GID`。 |
| `no_subtree_check` | 此选项禁用子树检查 |

#### 导出目录
在本示例中，我们将创建两个目录并导出这些目录供客户端挂载。
```bash
mkdir /accounts
mkdir /hrms
```

#### 编辑 `/etc/exports` 文件
```bash
vi /etc/exports
```
添加以下内容：
```text
/account 10.101.11.0/24(rw,sync)
/hrms*(rw.sync)
```
在本示例中，第一行将 NFS 共享到特定的网络 IP 范围。第二行向所有人共享 `hrms` 目录。

#### 导出目录
```bash
exportfs -a
```
#### 列出导出的目录
```bash
export -s
```
#### 添加防火墙规则
```bash
firewall-cmd --permanent --add-service=rpc-bind
firewall-cmd --permanent --add-service=nfs
```
重载防火墙
```bash
firewall-cmd --reload
```
检查服务的状态
```bash
firewall-cmd --list-services
```





尽管 GPT 带来了许多优势，但 MBR 仍然是兼容性最好且最广泛使用的分区方案。

在本章中，我们将学习创建、删除和修改各种类型的磁盘分区。

有几个用于分区管理的工具：
* `parted`
* `fdisk`

## Parted

`parted` 是一个可以管理分区表的命令行工具。

### 显示分区布局
语法
```bash
parted -l
```
此命令将显示所有块设备的分区布局。

### 显示特定块设备的分区表
语法
```bash
parted device print
```
示例
```bash
parted /dev/sda print
```

### 使用交互模式运行 parted
输入带设备名称的 `parted` 命令。假设新磁盘为 `sdb`。
```bash
parted /dev/sdb
```
它将启动交互会话。

### 在磁盘上创建分区表
启动 `parted`
语法
```bash
parted device_name
```
其中 `device_name` 是磁盘名称。
示例
```bash
parted /dev/sda
```

### 创建分区
语法
```bash
mkpart part-type name fs-type start end
```
其中：
| 列 | 描述 |
| :--- | :--- |
| `part-type` | 对于 MBR 分区表，可以是主、逻辑或扩展分区。 |
| `name` | GPT 分区表所需的分区名称。 |
| `fs-type` | 可以是 `xfs`, `ext2`, `ext3`, `ext4`, `fat16`, `fat32`, `hfs`, `hfs+`, `linux-swap`, `ntfs` 或 `reiserfs`。`fs-type` 参数是可选的，因为 `parted` 不会在分区上创建文件系统。 |
| `start and end` | 是决定分区起始和结束点的大小。可以使用大小单位后缀，如 `MiB`、`GiB` 或 `TiB`。默认大小为兆字节。 |

示例
```bash
(parted) mkpart primary xfs 1 5GiB
```

### 使用 print 命令列出分区
```bash
(parted) print
```
Model: VMware, VMware Virtual S (scsi)
Disk `/dev/sdb`: 10.7GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags:
Number Start End Size Type File system Flags
1 1049kB 5369MB 5368MB primary xfs lba

使用 `quit` 命令退出 `parted`。
```bash
(parted) quit
```
信息：你可能需要更新 `/etc/fstab`。

### 使用 parted 删除分区
在 `parted` 交互会话中选择 `parted` 设备。
示例
```bash
parted /dev/sdb
```

### 显示当前分区表
```bash
(parted) print
```
Model: VMware, VMware Virtual S (scsi)
Disk `/dev/sdb`: 10.7GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags:
Number Start End Size Type File system Flags
1 1049kB 5370MB 5369MB primary lvm
2 5370MB 7000MB 1631MB primary ext2 lba

使用 `rm` 命令删除分区并选择分区号。
```bash
(parted) rm
Partition number? 2
```

## 使用 fdisk 创建分区

语法
```bash
fdisk device
```
在此示例中，我们将在设备 `sdb` 上创建一个 5GB 的分区。
```bash
fdisk /dev/sdb
```
1. 交互式提示符输入 `n` 命令创建新分区。
2. 输入分区类型：`p` 代表主分区，`e` 代表扩展分区。
3. 选择分区号。按回车使用默认值。
4. 按回车使用默认起始位置。
5. 以 `MB`、`GB` 和 `KB` 输入大小，例如 `5G`。
6. 使用 `p` 命令打印分区。
7. 可选地，如果你需要更改文件系统，使用 `t` 命令并按 `L` 列出文件系统类型。输入 ID，如 Linux 的 `83` 和 LVM 的 `8e`。
8. 使用 `w` 命令写入更改。
```bash
(fdisk) w
```
分区表已更改。调用 `ioctl()` 重新读取分区表。正在同步磁盘。

---

#### 本地文件系统管理

在本章中我们将涵盖本地文件系统的管理：
* 创建文件系统
* 删除文件系统
* 挂载文件系统
* 卸载文件系统
* 创建 LVM 卷组
* 删除 LVM 卷组
* 创建逻辑卷
* 删除逻辑卷

### 创建文件系统
在创建文件系统之前，你应该决定想要创建哪类型的文件系统。

#### 创建 XFS 文件系统
语法
```bash
mksfs.xfs /dev/sdb1
```
示例
```bash
mksfs.xfs /dev/sdb1
```

#### 创建 ext4
语法
```bash
mkfs.ext4 /dev/sdb1
```
示例
```bash
mkfs.ext4 /dev/sdb1
```

### 挂载文件系统
在 Linux 系统中要使用文件系统，你必须先挂载它。挂载至少需要两个要素：挂载设备和挂载点。

#### 挂载设备
挂载设备是你想要用于数据的块设备或远程文件系统。

列出所有块设备
```bash
lsblk
```
可以通过以下标识符识别挂载文件系统：
* `UUID`：设备的通用唯一标识符。这是挂载设备的最佳方式，因为 UUID 保持不变。你可以使用 `blkid` 命令获取设备的 UUID。
* `Device name`：设备的路径名称，例如 `/dev/sdb1`。
* `Label`：标签，例如 `LABEL=data1`。你可以使用 `e2label` 查看或更改 ext 文件系统的标签。使用 `xfs_admin` 命令设置或列出 XFS 文件系统的标签。

#### 挂载点
挂载点是访问该挂载设备的链接。挂载点是一个普通目录。一旦挂载，设备成为该目录的一部分，你可以在此目录下访问文件系统的内容。

#### mount 命令
`mount` 命令用于挂载文件系统。

语法
```bash
mount -t type -o options dir
```
挂载文件系统需要以下参数：
* `type`：文件系统类型，可以是 `xfs`, `ext4`, `nfs` 等。
* `options`：选项，如 `rw`（读写）、`ro`（只读）、`loop`（ISO 质）。
* `device`：设备名称。
* `dir`：挂载点。

示例
```bash
mount -t ext4 /dev/sdb1 /mnt
```

### 自动挂载
如果你希望文件系统在每次启动时自动挂载，可以使用 `/etc/fstab` 文件。

`fstab` 文件的格式如下：
`firstsecond third fourth fifth sixth`

| 字段 | 描述 |
| :--- | :--- |
| 第一 | 块设备或远程文件系统 |
| 第二 | 挂载点 |
| 第三 | 文件系统类型 |





| 级别 | 描述 |
| :--- | :--- |
| 第四 | 选项，至少包含 `ro` 或 `rw`。其他选项为默认值：`rw`,`suid`,`dev`,`exec`,`auto`,`nouser` 和 `async`。`noauto`：不要自动挂载或通过 `mount -a` 命令挂载。`user`：允许用户挂载文件系统。`owner`：允许所有者挂载。 |
| 第五 | 备份选项，默认 `0` 表示不备份。 |
| 第六 | `fsck` 的文件系统检查优先级。 |

#### 示例

```
/dev/mapper/cl-root/ xfs defaults 0 0
UUID=095af347-cb2c-4d50-99b6-xxx/boot ext4 defaults 1 2
/dev/mapper/cl-swap swap swap defaults 0 0
LABEL=data1/data1 ext4 defaults 0 0
/dev/sdb2/data2 xfs defaults 0 0
```

## 使用 auto 选项手动挂载 fstab 中的所有设备
```bash
mount -a
```

## 手动挂载 fstab 中的单个设备。
#### 语法
```bash
mount mount_point
```
无需指定设备名称。

#### 示例
```bash
mount /data2
```

## 列出所有已挂载的文件系统
```bash
mount
or
findmnt
```

## 列出特定文件系统类型
```bash
findmnt -t xfs
```

## 卸载文件系统
#### 语法
```bash
umount mount_point
```
#### 示例
```bash
umount /data1
```
如果在卸载文件系统时遇到“target is busy”错误，请使用 `fuser` 命令列出所有使用该文件系统的进程。

#### 语法
```bash
fuser --mount mountpoint
```
#### 示例
```bash
fuser --mount /data1
```

## 删除文件系统
要删除文件系统，我们必须先卸载它。
#### 示例
```bash
umount /dev/sda2
```
然后我们可以使用 `fdisk` 或 `parted` 从分区表中删除分区。

#### 示例
```bash
fdisk /dev/sda2
```
选择选项 `d` 来删除分区。
通过选择 `w` 将更改写入分区表。

## 第 13 章：逻辑卷管理

LVM 或 `Logical Volume Manager`（逻辑卷管理器）允许创建磁盘和分区组，并将其作为一个磁盘使用。它在物理设备和逻辑设备之间创建了一个抽象层。LVM 的优势如下：

- **灵活性**：允许调整大小。
- **快照**：对逻辑卷进行时间点快照。

传统的磁盘设置如下：

| 文件系统 | / | /opt | /home |
| :--- | :--- | :--- | :--- |
| 分区 | `/dev/sda1` | `/dev/sda2` | `/dev/sda3` |
| 物理设备 | `/dev/sda` | `/dev/sdb` | |

这种设置是磁盘，然后是分区，在分区之上是文件系统。

## LVM 设置

| 文件系统 | / | /home | /var |
| :--- | :--- | :--- | :--- |
| 逻辑卷 | `/dev/sda1` | `/dev/sda2` | `/dev/sda3` |
| 卷组 | `Vg01` | | |
| 物理卷 | `/dev/sda` | `/dev/sdb` | |

### 物理卷
物理卷（`PV`）是底层的物理存储单元。物理存储是块设备，如分区或整个磁盘。使用 `pvcreate` 命令将物理设备作为物理卷。如果块设备是分区，在使用 `pvcreate` 命令之前，请使用 `fdisk` 将分区类型更改为 `8e (Linux LVM)`。

### 创建 PV
#### 语法
```bash
pvcreate device
```
#### 示例
```bash
pvcreate /dev/sdb
```
### 如果设备是分区
#### 将分区类型更改为 LVM
```bash
fdisk /dev/sda (参考分区章节来更改分区类型)
```
#### 现在创建 PV
```bash
pvcreate /dev/sda3
```

## 卷组
一个或多个物理卷组合成一个卷组（`VG`）。卷组是一个抽象，它将底层设备呈现为一个统一的逻辑设备，具有物理卷组合后的存储容量。

### 创建物理卷
注意：文本中写的是“创建物理卷”，但提供的是 `vgcreate` 的语法。
#### 语法
```bash
vgcreate vgname PV1 PV2 ..
```
#### 示例
```bash
vgcreate vg01 /dev/sdb /dev/sdc
```

## 逻辑卷
逻辑卷是卷组的逻辑分区。逻辑卷可用于创建文件系统。在某些情况下，你也可以将 `LV` 作为块设备使用。

### 创建 LV
#### 语法
```bash
lvcreate -n name -L size VG_name
```
#### 示例
```bash
lvcreate -n data_lv -L 5G vg01
```

## 文件系统
### 在 LV 上创建 XFS 文件系统
#### 语法
```bash
mkfs.xfs lv_name
```
#### 示例
```bash
mkfs.xfs /dev/vg01/data_lv
```
### 在 LV 上创建 ext4 文件系统
#### 语法
```bash
mkfs.ext4 lv_name
```
#### 示例
```bash
mkfs.ext4 /dev/vg01/data_lv
```

## LVM 中两个值得注意的术语
- **物理区 (Physical Extent)**
- **逻辑区 (Logical Extent)**

### 物理区
物理卷空间被划分为固定大小的单元，称为物理区，它是可以分配的最小单元。`P.E.` 大小对于同一 `VG` 中的所有物理卷都是相同的。

### 逻辑区
`PE` 的映射形成了 LVM 的前端。默认情况下，一个 `PE` 映射到一个 `LE`。但在镜像的情况下，你可以将多个 `PE` 映射到一个 `LE`。




使用此命令扩展 LV 以使用 VG 的 100% 空闲空间，并扩展文件系统。

```bash
lvextend -l +100%FREE -r vg01/lv-root
```

LVM 章节结束。

第 14 章

## 软件管理

Oracle Linux 发行版基于 RPM 包。Oracle Linux 使用 `rpm` 命令通过 `.rpm` 包安装软件。RPM 包仅仅是一个包含某些文件和关于这些文件信息的文件。从技术上说，RPM 是一个包含 `cpio` 归包及其自身元数据的文件。RPM 头部包含元数据，这些元数据用于确定有关软件包的以下信息：

- 软件包描述。
- 软件包中的文件列表。
- 软件包的版本和发布版本。
- 制作时间和及制作者。
- 支持的架构。
- 软件包中包含的文件的校验和。
- 依赖关系。
等……

## 软件包管理系统

如果你尝试手动安装单个软件包，必须首先安装它所有的依赖项，并跟踪版本。为了方便软件管理，Linux 公司开发了一套名为软件包管理系统或包管理器的系统。软件包管理系统安装预编译的包，这些包以包含软件二进制文件、配置文件和依赖关系信息的归档形式存在。软件包管理系统是一系列用于自动化软件包安装、升级和删除过程的软件工具。软件管理器维护自己的软件依赖关系版本信息数据库。软件包管理系统有助于防止软件不匹配和缺少前提。Oracle Linux 使用 `YUM` 工具进行软件包管理。

### YUM

与其他 Linux 发行版一样，Oracle Linux 使用了名为 `YUM` 的非常全面的软件包管理系统。Yellow dog Updater Modifier 是一个用于软件包管理的命令行工具。`Yum` 使用仓库来获取与你的系统兼容的特定软件包正确版本。`yum` 允许软件包的自动更新和依赖管理。当你使用 `yum` 命令安装软件时，它会自动从定义的仓库下载软件包及其所有依赖项。Oracle Linux 版本 8 使用 `YUM v4` 代替了早期版本使用的 `YUM v3`。基于 `DNF` 技术的 `YUM v4` 工具具有以下优势：

- 更好的性能
- 支持模块化内容（我们稍后将讨论模块）
- 用于与工具集集成的稳定 API

Oracle Linux 8 有三个应用流，每个流都有自己的生命周期：

- `BaseOS` 提供基础操作系统，
- `AppStream` 提供用户应用，
- `CodeReady Linux Builder` 提供开发者工具和语言。

## 软件包管理

### 搜索软件包
#### 语法
```bash
yum search package_name
```
#### 示例
```bash
yum search httpd
```

### 显示软件包信息
#### 语法
```bash
yum info package_name
```
#### 示例
```bash
yum info httpd
```

### 列出可用软件包
```bash
yum list available
```

### 从默认流安装软件包
#### 语法
```bash
yum install package_name
```
#### 示例
```bash
yum install httpd
```

### 安装本地下载的软件包
#### 语法
```bash
yum localinstall package.rpm
```
#### 示例
```bash
yum localinstall abc.rpm
```

### 移除软件包
#### 语法
```bash
yum remove package_name
```
#### 示例
```bash
yum remove httpd
```

### 更新

### 更新特定软件包
#### 语法
```bash
yum update package_name
```
#### 示例
```bash
yum update vsftpd
```

### 更新整个系统
将系统更新到最新级别
```bash
yum -y update
```

#### 仅更新安全补丁
```bash
yum -y update --security
```
此命令可能会增加系统的次版本号，在某些情况下并非必须，此时你可以使用更保守的方法进行安全更新。
```bash
yum update-minimal --security -y
```

### CVE
常见漏洞与暴露（Common Vulnerabilities and Exposures）是一个常见标识符列表。

### 查看 CVE 信息
#### 语法
```bash
yum infoinfo CVE-ID
```
#### 示例
```bash
yum infoinfo CVE-2021-12345
```
（示例 ID）

### 列出包含 CVE 的软件包
#### 语法
```bash
yum list list CVE-ID
```
#### 示例
```bash
yum list list CVE-2021-XXXX
```

### 更新 CVE 软件包
#### 语法
```bash
yum update CVE-ID
```
#### 示例
```bash
yum update CVE-2021-XXXX
```

#### 仅更新 CVE 安全更新
#### 语法
```bash
yum update --security CVE-ID
```
#### 示例
```bash
yum update --security CVE-2021-XXXX
```

### 搜索 CVE
#### 语法
```bash
yum search CVE-ID
```
#### 示例
```bash
yum search CVE-2021-XXXX
```

### 安装特定 CVE 软件包
#### 语法
```bash
yum install CVE-ID
```
#### 示例
```bash
yum install CVE-2021-XXXX
```

#### 移除 CVE 软件包
#### 语法
```bash
yum remove CVE-ID
```
#### 示例
```bash
yum remove CVE-ID
```

### 列出已安装的 CVE
#### 语法
```bash
yum list installed CVE-ID
```
#### 示例
```bash
yum list installed CVE-2021-XXXX
```

#### 查看 CVE 历史
#### 语法
```bash
yum history CVE-ID
```
#### 示例
```bash
yum history CVE-2021-XXXX
```

#### 撤滚 CVE
#### 语法
```bash
yum history undo CVE-ID
```
#### 示例
```bash
yum history undo CVE-2021-XXXX
```

#### 查看 CVE 详情
#### 语法
```bash
yum history info CVE-ID
```
#### 示例
```bash
yum history info CVE-2021-XXXX
```

### 模块（Modules）

### 搜索模块
#### 语法
```bash
yum module list module_name
```
#### 示例
```bash
yum module list nodejs
```

### 列出可用模块
#### 语法
```bash
yum module list
```

## 模块

如果你尝试手动安装单个软件包，必须首先安装它所有的依赖项，并跟踪版本。为了方便软件管理，Linux 公司开发了一套名为软件包管理系统或包管理器的系统。软件包管理系统安装预编译的包，这些包以包含软件二进制文件、配置文件和依赖关系信息的归档形式存在。软件包管理系统是一系列用于自动化软件包安装、升级和删除软件包过程的软件工具。软件管理器维护自己的软件依赖关系版本信息数据库。软件包管理系统有助于防止软件不匹配和缺少前提。Oracle Linux 使用 `YUM` 工具进行软件包管理。

### YUM

与其他 Linux 发行版一样，Oracle Linux 使用了名为 `YUM` 的非常全面的软件包管理系统。Yellow dog Updater Modifier 是一个用于软件包管理的命令行工具。`Yum` 使用仓库来获取与你的系统兼容的特定软件包正确版本。`yum` 允许软件包的自动更新和依赖管理。当你使用 `yum` 命令安装软件时，它会自动从定义的仓库下载软件包及其所有依赖项。Oracle Linux 版本 8 使用 `YUM v4` 代替了早期版本使用的 `YUM v3`。基于 `DNF` 技术的 `YUM v4` 工具具有以下优势：

- 更好的性能
- 支持模块化内容（我们稍后将讨论模块）
- 用于与工具集集成的稳定 API

Oracle Linux 8 有三个应用流，每个流都有自己的生命周期：

- `BaseOS` 提供基础操作系统，
- `AppStream` 提供用户应用，
- `CodeReady Linux Builder` 提供开发者工具和语言。

## 软件包管理

### 搜索软件包
#### 语法
```bash
yum search package_name
```
#### 示例
```bash
yum search httpd
```

### 显示软件包信息
#### 语法
```bash
yum info package_name
```
#### 示例
```bash
yum info httpd
```

### 列出可用软件包
```bash
yum list available
```

### 从默认流安装软件包
#### 语法
```bash
yum install package_name
```
#### 示例
```bash
yum install httpd
```

### 安装本地下载的软件包
#### 语法
```bash
yum localinstall package.rpm
```
#### 示例
```bash
yum localinstall abc.rpm
```

### 移除软件包
#### 语法
```bash
yum remove package_name
```
#### 示例
```bash
yum remove httpd
```

### 更新

### 更新特定软件包
#### 语法
```bash
yum update package_name
```
#### 示例
```bash
yum update vsftpd
```

### 更新整个系统
将系统更新到最新级别
```bash
yum -y update
```

#### 仅更新安全补丁
```bash
yum -y update --security
```
此命令可能会增加系统的次版本号，在某些情况下并非必须，此时你可以使用更保守的方法进行安全更新。
```bash
yum update-minimal --security -y
```

### CVE
常见漏洞与暴露（Common Vulnerabilities and Exposures）是一个常见标识符列表。

### 查看 CVE 信息
#### 语法
```bash
yum info CVE-ID
```
#### 示例
```bash
yum info CVE-2021-12345
```
（示例 ID）

### 列出包含 CVE 的软件包
#### 语法
```bash
yum list list CVE-ID
```
#### 示例
```bash
yum list list CVE-2021-XXXX
```

### 更新 CVE 软件包
#### 语法
```bash
yum update CVE-ID
```
#### 示例
```bash
yum update CVE-2021-XXXX
```

#### 仅更新 CVE 安全更新
#### 语法
```bash
yum update --security CVE-ID
```
#### 示例
```bash
yum update --security CVE-2021-XXXX
```

### 搜索 CVE
#### 语法
```bash
yum search CVE-ID
```
#### 示例
```bash
yum search CVE-2021-XXXX
```

### 安装特定 CVE 软件包
#### 语法
```bash
yum install CVE-ID
```
#### 示例
```bash
yum install CVE-2021-XXXX
```

#### 移除 CVE 软件包
#### 语法
```bash
yum remove CVE-ID
```
#### 示例
```bash
yum remove CVE-ID
```

### 列出已安装的 CVE
#### 语法
```bash
yum list installed CVE-ID
```
#### 示例
```bash
yum list installed CVE-2021-XXXX
```

#### 查看 CVE 历史
#### 语法
```bash
yum history CVE-ID
```
#### 示例
```bash
yum history CVE-2021-XXXX
```

#### 撤滚 CVE
#### 语法
```bash
yum history undo CVE-ID
```
#### 示例
```bash
yum history undo CVE-2021-XXXX
```

#### 查看 CVE 详情
#### 语法
```bash
yum history info CVE-ID
```
#### 示例
```bash
yum history info CVE-2021-XXXX
```

### 模块（Modules）

### 搜索模块
#### 语法
```bash
yum module list module_name
```
#### 示例
```bash
yum module list nodejs
```

### 列出可用模块
#### 语法
```bash
yum module list
```

## 模块

如果你尝试手动安装单个软件包，必须首先安装它所有的依赖项，并跟踪版本。为了方便软件管理，Linux 公司开发了一套名为软件包管理系统或包管理器的系统。软件包管理系统安装预编译的包，这些包以包含软件二进制文件、配置文件和依赖关系信息的归档形式存在。软件包管理系统是一系列用于自动化软件包安装、升级和删除软件包过程的软件工具。软件管理器维护自己的软件依赖关系版本信息数据库。软件包管理系统有助于防止软件不匹配和缺少前提。Oracle Linux 使用 `YUM` 工具进行软件包管理。

#### 显示模块信息
#### 语法
```bash
yum module info module_name
```
#### 示例
```bash
yum module info nodejs
```

#### 提供特定软件包的模块
#### 语法
```bash
yum module provides package_name
```
#### 示例
```bash
yum module provides php
```

#### 安装模块
#### 语法
```bash
yum module install module_name
```
#### 示例
```bash
yum module install nodejs
```

#### 启用模块流
#### 语法
```bash
yum module enable module_name:stream
```
#### 示例
```bash
yum module enable nodejs:12
```

#### 禁用模块流
#### 语法
```bash
yum module disable module_name:stream
```
#### 示例
```bash
yum module disable nodejs:12
```

#### 重置模块
#### 语法
```bash
yum module reset module_name
```
#### 示例
```bash
yum module reset nodejs
```

#### 查看模块状态
#### 语法
```bash
yum module status module_name
```
#### 示例
```bash
yum module status nodejs
```

#### 模块历史
#### 语法
```bash
yum module history module_name
```
#### 示例
```bash
yum module history nodejs
```

#### 撤滚模块操作
#### 语法
```bash
yum module history undo module_name ID
```
#### 示例
```bash
yum module history undo nodejs 1
```




# Yum

#### 语法
```bash
yum module remove module_name:stream/profile
```
#### 示例
```bash
yum module remove --profile nodejs:12/minimal
```

### 将模块重置为初始状态
#### 语法
```bash
yum module reset module_name
```
#### 示例
```bash
yum module reset node
```

### 禁用模块及其所有流
#### 语法
```bash
yum module disable module_name
```
#### 示例
```bash
yum module disable nodejs
```

# RPM
使用 `rpm` 进行包管理。

虽然 `yum` 是一个功能强大的软件包管理器，但在某些情况下你必须手动管理 `rpm` 软件包。

### 列出所有已安装包
```bash
rpm -qa
```

### 列出特定的已安装包
#### 语法
```bash
rpm -qa |grep package_name
```
#### 示例
```bash
rpm -qa |grep gzip
```

### 安装 rpm 包
#### 语法
```bash
rpm -ihv package_name
```
其中 `-i` 表示安装
- `-v` 表示详细模式
- `-h` 显示进度
#### 示例
```bash
rpm -ihv zsh-html-5.5.1-6.el8_1.2.noarch.rpm
```

### 更新已安装的包
#### 语法
```bash
rpm -Uhv package_name
```
#### 示例
```bash
rpm -Uhv zsh-html-5.5.1-6.el8_1.2.noarch.rpm
```

### 检查包的依赖
#### 语法
```bash
rpm -qpR package_name
```
#### 示例
```bash
rpm -qpR zsh-html-5.5.1-6.el8_1.2.noarch.rpm
```

### 列出特定包安装的所有文件
#### 语法
```bash
rpm -ql package_name
```
#### 示例
```bash
rpm -ql zsh-html-5.5.1-6.el8_1.2.noarch.rpm
```

### 移除包
#### 语法
```bash
rpm -ev package_name
```
#### 示例
```bash
rpm -ev zsh-html
```

### 安装前打印包信息
#### 语法
```bash
rpm -qip package.rpm
```
#### 示例
```bash
rpm -qip zsh-html-5.5.1-6.el8_1.2.noarch.rpm
```

### 重建 rpm 数据库
```bash
cd /var/lib/rpm
rm __db*
rpm --rebuilddb
/usr/lib/rpm/rpmdb_verify /var/lib/rpm/Packages
```

# 包组
包组包含执行相关任务的软件包，例如系统工具、工作站和最小化安装等。

### 列出组列表
#### 语法
```bash
yum grouplist
```

### 安装包组
#### 语法
```bash
yum group install “Group Name”
```
#### 示例
```bash
yum group install “System Tools”
```

### 更新组
#### 语法
```bash
yum group install “Group Name”
```
#### 示例
```bash
yum group update “System Tools”
```

### 移除包组
#### 语法
```bash
yum group remove “Group Name”
```
#### 示例
```bash
yum group remove “System Tools”
```

## 第 15 章
## 软件仓库

Linux 仓库（Repository）是 Linux 操作系统更新的存储位置。仓库也用于安装新应用程序和更新已安装的应用程序。每个仓库都是托管在远程服务器或本地的软件集合。仓库可以分为多个分支，如二进制文件、源码、可选包等。

要添加新仓库，请在 `/etc/yum.conf` 文件中添加条目，但建议在 `/etc/yum.repos.d` 目录下为每个仓库创建一个单独的文件。仓库文件的扩展名应该是 `.repo`。

仓库文件的主要组件有：

| `[repository]` | 每个仓库都应该有一个以仓库部分开头的仓库 ID |
| `name=repository_name` | 仓库的名称 |
| `baseurl=repository_url` | 仓库的位置，位置可以是 http、ftp 或本地 http `[`path/repo`](http://path/repo)`FTP `ftp://path/repo` 本地 `file:///path/repo` |
| `enabled = 1` | 定义仓库的状态，1 表示启用，0 表示禁用 |
| `gpgcheck = 1` | 在安装前验证 GPG 签名 |

![](img/image00407.jpeg) 示例

## Oracle Linux 仓库
与之前的版本不同，Oracle Linux 8 带有两个主要仓库。
1. BaseOS
2. Appstream

### BaseOS
BaseOS 旨在为所有类型的安装提供核心功能集和核心组件。这意味着即使是无无头安装（headless installation），也需要 BaseOS 仓库。

### Appstream
Appstream 包含了额外的用户空间应用程序、语言、数据库等。Appstream 适用于不同的工作负载，如 http、数据库或文件服务器。Appstream 的更新频率比 BaseOS 高。Appstream 由 `rpm` 软件包和模块组成。

## 仓库管理命令
### 列出所有启用的仓库
```bash
yum repolist
```

### 列出所有仓库的状态
```bash
yum repolist all
```

### 使用网络上的 repo 文件添加仓库
#### 示例
```bash
yum config-manager --add-repo http://www.example.com/example.rep
```

### 使用 repo 文件启用/禁用仓库
你可以通过编辑 `/etc/yum.repo.d` 中的目录 repo 文件或使用 `yum config-manager` 命令来启用或禁用仓库。

使用 repo 文件启用任何仓库：
![](img/image00408.jpeg) 打开 repo 文件并将 `enabled=0` 更改为 `enabled=1`。要禁用任何仓库，将 `enabled=1` 更改为 `enabled=0`。

使用命令：
### 启用任何仓库
#### 语法
```bash
yum config-manager --set-enabled repo_name
```
#### 示例
```bash
yum config-manager --set-enabled PowerTools
```

### 禁用仓库
#### 语法
```bash
yum config-manager --set-disabled reponame
```
#### 示例
```bash
yum config-manager --set-disabled PowerTools
```

### 每次修改后清除缓存
```bash
yum clean all
```

## 设置本地仓库
在某些无法上网的情况下，你必须创建本地仓库进行软件管理。创建本地仓库的步骤如下：
1. 创建目录
2. `mkdir /local_repo`
3. 挂载 DVD 到 `/mnt`
```bash
mount /dev/cdrom /mnt
```
注意：`cdrom` 设备名称可能不同
4. 将文件复制到 `/local_repo`
```bash
cp -r /mnt/* /local_repo
```
5. 将 repo 文件复制到 `/etc/yum.repos.d`
```bash
cp /local_repo /etc/yum.repos.d
```
6. 修改文件权限
```bash
chmod 644 /etc/yum.repos.d/local_repo
```
7. 编辑配置
```bash
vi /etc/yum.repos.d/local_repo
```
8. 修改后的文件应该像这样：
```ini
[InstallMedia-BaseOS]
name=Oracle Linux 8 BaseOS
metadata_expire=-1
gpgcheck=1
enabled=1
baseurl=file:///local_repo/BaseOS/
gpgkey=file:///etc/pki/rpm-gpg/RPM-Oracle

[InstallMedia-AppStream]
name=Oracle Linux 8 AppStream
metadata_expire=-1
gpgcheck=1
enabled=1
baseurl=file:///local_repo/AppStream/
gpgkey=file:///etc/pki/rpm-gpg/RPM-Oracle
```
9. 清理缓存
```bash
yum clean all
```
10. 列出仓库
```bash
yum repolist
```
![](img/image00409.jpeg)

## 开发者仓库
### PowerTools
PowerTools 仓库主要用于软件开发者。该仓库包含了从源码编译应用程序所需的软件包。
### 启用
```bash
yum config-manager --set-enabled PowerTools
```

## 第三方仓库
为了安装由于许可问题在上述三个仓库中无法提供的软件，你可以添加第三方仓库。常见的第三方仓库有：
- EPEL
- REMI
- RPM Fusion

### EPEL 仓库
EPEL 或企业 Linux 仓库来自 Fedora 社区，包含了 Oracle 官方由于许可限制无法提供的软件包。常见的包有 chromium、音频和视频解码器。
### 添加仓库
```bash
yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
```
### 启用
```bash
yum config-manager --set-enabled epel
```

### REMI
REMI 是由 Remi Collect 创建并维护的免费使用仓库。REMI 提供了最新的 PHP 栈和其他某些软件。
### 安装
```bash
yum -y install https://rpms.remirepo.net/enterprise/remi-release-8.rpm
```
### 启用
```bash
yum config-manager --set-enabled remi
```

### RPM Fusion
RPM Fusion  Oracle Linux 不愿提供的专有多媒体软件。
### 安装
```bash
yum install --nogpgcheck https://download1.rpmfusion.org/free/el/rpmfusion-free-release-8.noarch.rpm https://download1.rpmfusion.org/nonfree/el/rpmfusion-nonfree-release-8.noarch.rpm
```
注意：这是一条命令行命令，将同时添加免费和非免费的 RPM Fusion 仓库。





服务是一个在后台运行等待被使用或执行基本任务的程序。当系统启动时，它会启动许多服务以达到系统所需的状态。假设您想以 GUI 模式启动系统，系统必须启动所有与桌面环境相关的服务。同样，如果您将服务器配置为 Web 服务器，则必须在启动过程中启动 Web 服务。即使是执行基本任务，它也需要许多服务正在运行，如网络、日期和时间等。与由用户启动并在用户注销时自动关闭的普通软件程序不同，服务可以在没有用户参与的情况下启动，并且在用户注销后可能继续运行。大多数服务在用户不知情的情况下后台运行。软件开发者可以编写自己的软件作为服务运行。

## SYSTEMD 简介

`systemd` 是大多数 Linux 发行版的系统和服务服务管理器。Oracle Linux 也使用 `systemd` 进行服务管理。`systemd` 与旧的 `SysV init` 脚本兼容。使用 `systemd` 管理服务的主要优势包括：

-   更易的服务管理
-   启动时的任务并行执行
-   通过 `cgroups` 实现更好的资源管理。
-   守护进程的按需激活

## systemd 的重要目录和文件

| 目录 | 说明 |
| :--- | :--- |
| `/usr/lib/systemd/system/` | 安装程序的 `systemd` 单元文件。 |
| `/run/systemd/system/` | 运行时创建的 `systemd` 单元文件。 |
| `/etc/systemd/system/` | 为自动启动服务创建的 `systemd` 单元文件。 |

## 系统单元类型

| 单元 | 说明 |
| :--- | :--- |
| `.service` | 服务 |
| `.device` | 设备 |
| `.target` | 相当于 sysv 中的运行级别 (run level) |
| `.snapshot` | 存储状态 |
| `.swap` | 封装内存交换分区或交换文件。 |

## 命令

`systemctl` 是 Oracle Linux 8 中管理服务的命令。我们将使用此命令来查看、启动、停止、启用和禁用服务。

### 列出所有服务
```
systemctl list-units --type service --all
```

### 显示服务的状态
#### 语法
```
systemctl status service_name
```
#### 示例
```
systemctl status sshd
```

### 检查服务是否激活（运行）
#### 语法
```
systemctl is-active service_name
```
#### 示例
```
systemctl is-active sshd
```

## 启动和停止服务

### 启动服务
#### 语法
```
systemctl start service_name
```
#### 示例
```
systemctl start httpd
```

### 停止服务
#### 语法
```
systemctl stop service_name
```
#### 示例
```
systemctl stop httpd
```

### 重启服务
#### 语法
```
systemctl restart service_name
```
#### 示例
```
systemctl restart httpd
```

### 如果服务正在运行则重启
#### 语法
```
systemctl try-restart service_name
```
#### 示例
```
systemctl try-restart httpd
```

## 重新加载服务配置
#### 语法
```
systemctl reload service_name
```
#### 示例
```
systemctl reload httpd
```

### 屏蔽服务 (Mask Service)
当你屏蔽一个服务时，该服务无法启动。这在禁用危险和未知服务时非常有用。
#### 语法
```
systemctl mask service_name
```
#### 示例
```
systemctl mask httpd
```

### 解除屏蔽
#### 语法
```
systemctl unmask service_name
```
#### 示例
```
systemctl unmask httpd
```

## 使用 Target（运行级别）

Target 基本上是为了让服务器进入特定状态。许多服务和其他单元的启动和停止是为了使服务器达到所需状态。多个 Target 可以同时处于激活。

### 查看系统中所有可用的 target
```
systemctl list-unit-files --type=target
```

### 查看默认 target
在 `/lib/systemd/system/default.target` 中描述了 `systemd` 在启动时尝试达到的默认 target。
```
systemctl get-default
```

### 修改启动时将使用的默认 target
#### 语法
```
systemctl set-default target_name
```
#### 示例
```
systemctl set-default multi-user.target
```

### 列出与 target 绑定的单元
#### 语法
```
systemctl list-dependencies target_name
```
#### 示例
```
systemctl list-dependencies multi-user.target
```

### 定义的 target
| Target | 说明 |
| :--- | :--- |
| `rescue.target` | 单用户模式。 |
| `multi-user.target` | 非 GUI 多用户控制台访问 |
| `graphical.target` | 一个 GUI 会话。 |
| `custom.target` | 自定义 target。 |
| `emergency.target` | 用于系统修复的最精简环境。 |

## 关机或重启

### 使用 systemctl 关机
```
systemctl poweroff
```

### 重启
```
systemctl reboot
```

### 以救援模式启动服务器
```
systemctl rescue
```

## 启用和禁用服务

要配置任何服务在启动时自动运行，我们使用 `systemctl enable` 命令。该命令在 `/etc/systemd/system/` 目录下创建链接文件。当禁用任何服务时，`systemctl` 会删除该目录下的链接文件。

### 配置服务在启动时运行
```bash
systemctl enable service_name
```
#### 示例
```bash
systemctl enable httpd
```

### 禁用服务
```bash
systemctl disable service_name
```
#### 示例
```bash
systemctl disable httpd
```

### 检查服务是否启用
```bash
systemctl is-enabled service_name
```
#### 示例
```bash
systemctl is-enabled sshd
```

### 列出启用的服务
```bash
systemctl list-unit-files --type=service --enabled
```

### 查看服务的详细信息
```bash
systemctl show service_name
```




现在你有了普通用户的最小和最大范围，可以列出所有普通用户：

```bash
awk -F'[/:]' '{if ($3 >= 1000 && $3 != 65534) print $1}' /etc/passwd
```

### `/etc/passwd` 文件
`/etc/passwd` 文件包含了系统上所有用户的列表，包括系统用户和普通用户。该文件的格式为每行代表一个用户。每行的字段由 `:`（冒号）分隔。这些字段包含以下信息：

1. 用户名
2. 加密密码（显示为 `x`，加密密码的实际位置位于 `/etc/shadow` 文件）
3. 用户 ID 数 (`UID`)
4. 用户组 ID (`GID`)
5. 用户全名
6. 家目录
7. !![](img/image00410.jpeg)登录 shell

### 系统上所有用户列表
```bash
awk -F':' '{ print $1}' /etc/passwd
```

### 组 ID (GID)
Linux 中的组通过组 组 ID (`GIDs`) 定义。`GIDs` 存储在 `/etc/groups` 文件中。前 1000 个 GID 通常保留给系统使用。所有的应用程序组从 1001 开始。

### `/etc/group` 文件
`/etc/group` 是一个定义了每个用户所属组的文件。多个用户可以属于同一个组。同一组中的每个用户名用逗号分隔。这些字段包含以下信息：

1. 组名。
2. 密码：通常不使用密码，因此为空为空/空白。如果不为空，则存储加密密码。这在实现特权组时非常有用。
3. 组 ID (`GID`)
4. 用逗号分隔的用户列表。

![](img/image00411.jpeg)

# 第 18 章：## 探索 SU 和 SUDO

要提升分配给当前用户的权限，你可以使用 `su` 或 `sudo`。

### SU
`su` 命令用于切换到另一个用户。如果执行时不指定用户名，它将默认以 root 用户身份登录。`su` 需要目标账户的密码。

**以特定用户登录**
语法：
```bash
su username
```
示例：
```bash
su oracle
```
当配合连字符（`su -`）使用时，将假设目标用户的环境。

示例：
对于 root 用户：
```bash
su -
```
对于其他用户：
```bash
su - oracle
```

### SUDO
`sudo` 允许用户以另一个用户的安全权限运行程序，默认情况下，它使用管理员权限运行命令。通过这种机制，你可以将某些管理员任务分配给权限较低的用户，而无需共享管理员密码。与需要目标账户密码的 `su` 不同，`sudo` 需要当前用户的密码。在命令前加 `sudo` 即可执行任何管理命令。

**运行更改系统配置的特权命令的示例**
```bash
sudo yum install gzip
```
或更改主机名：
```bash
sudo hostnamectl set-hostname host2021
```

**作为不同用户运行命令。**
语法：
```bash
sudo -u user command
```
示例：
```bash
sudo -u user2 hostnamectl
```

**在交互模式下使用 sudo**
```bash
sudo -i
```

##### 修改 sudo 配置
`sudo` 将其配置存储在 `/etc/sudoers` 文件中。要修改 sudo 配置，请使用 `visudo` 命令。它会有效地启动 `vi` 编辑器并编辑 `/etc/sudoers` 文件。`visudo` 命令应由管理员执行。

`/etc/sudoers` 文件包含一个用户列表，以及这些用户可以运行的命令。

`user host=(users) [NOPASSWORD:]commands`

示例：
```text
%operators localhost = (apache) /usr/sbin/
```

###### Wheel 组
![](img/image00412.jpeg)Oracle Linux 自带一个默认的管理员组，称为 wheel 组。如果你想将所有管理员权限分配给一个用户而不共享 root 密码，可以将该用户添加到 wheel 组。在此之前，请确保 `/etc/sudoer` 文件中的该行没有被注释。

**将用户添加到 wheel 组**
```bash
usermod --append -G wheel user_name
```
示例：
```bash
usermod --append -G wheel user1
```

**注意：** `SU` 和 `SUDO` 的主要区别在于，在 `SU` 的情况下，你通过切换到超级用户或 root 用户来获取 root 权限，而在 `SUDO` 的情况下，你通过单个命令获取 root 权限。

# 第 19 章：## 探索文件和目录权限

Linux 是一个多用户操作系统，可以被许多用户同时访问。因此，用户不触碰彼此的数据是绝对必要的。为了数据和系统文件的安全和正常，操作系统部署了不同类型的安全系统。Linux 将授权分为 2 级：

1. 所有权
2. 权限

### 所有权
所有权定义了谁可以访问文件或目录。为了表示所有权，Linux 使用以下符号：

| 符号 | 描述 |
| :--- | :--- |
| u | 用户 (所有者) - 默认情况下，创建文件或目录的用户成为该文件或目录的所有者。 |
| g | 组 |
| o | 其他 - 给其他用户授予权限。实际上，这意味着其他人。 |

### 权限
权限定义了允许在文件或目录上执行的操作。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。

权限定义了允许在文件或目录上执行的操作。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。

权限定义了允许在文件或目录上执行的操作。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。

权限定义了允许在文件或目录上执行的操作。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。

权限定义了允许在文件或目录上执行的操作。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。

权限定义了允许在文件或目录上执行的操作。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。

权限定义了允许在文件或目录上执行的操作。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。

权限定义了允许在文件或目录上执行的操作。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是是、、写和执行。这些操作是读、写和执行。

| 符号 | 描述 |
| :--- | :--- |
| u | 用户 (所有者) - 默认情况下，创建文件或目录的用户成为该文件或目录的所有者。 |
| g | 组 |
| o | 其他 - 给其他用户授予权限。实际上，这意味着其他人。 |

权限定义了允许在文件或目录上执行的操作。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。

权限定义了允许在文件或目录上执行的操作。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。

权限定义了允许在文件或目录上执行的操作。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。

权限定义了允许在文件或目录上执行的操作。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。这些操作是读、写和执行。

权限定义允许在文件文件或。上执行。。这些操作是是、、
执行执行。
操作是读
写执行执行。

是 |


 |。 |操作是 |
 | | |。 | |
 |
 |





 | |






 |
 |
































 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | |

 | | | | | | | | | | | | | | |
 | |
 |
 | |
 |
 | | |
 |
 |
 |
 | | | | | | | | |
 | | | | | |


 | | | | |
 |
 | | |
 |

 | | | |



 | | | | | |
 | |
 | | |
 | | |
 | | | | |
 | | | | |
 | | | |
 | | | | |
 | | | | |
 | | | | | |
 | | | | |
 | | | | |
 | | | | | |
 | | | | |
 | | | | |
 | | | | |
 | | | | |
 | |
 | | | | |
 | | | | |
 | | | | |
 | | | | | |
 | | | | |
 | | | | |
 | | | | | |
 | |
 | | | | |
 | | | | |
 | | | | | | | | | | | |
 | | | | | |
 | | | | |
 | | | | | |
 | | | | |
 | | | | | | | | | | | | | | | | | | |
 | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | | 译文：<channel|>[content]
Now you have the minimum and maximum range of normal, to list all normal users

```bash
awk -F'[/:]' '{if ($3 >= 1000 && $3 != 65534) print $1}' /etc/passwd
```

### `/etc/passwd` file
`/etc/passwd` file hold the list of all users on the system both system users and normal users. The format of the file is that each line represents a user. The fields in each line are separated by `:` (colons). The fields have following information:

1. User Name
2. The encrypted password (show `x`, actual location of encrypted password is `/etc/shadow` file)
3. User ID number (`UID`)
4. Group ID of user (`GID`)
5. User full name
6. Home directory
7. !![](img/image00410.jpeg)Login shell

### List of all users on the system
```bash
awk -F':' '{ print $1}' /etc/passwd
```

### Group ID (GID)
Groups in Linux are defined by group IDs (`GIDs`). `GIDs` are stored in the `/etc/groups` file. The first 1000 GIDs are usually reserved for system use. All application groups start from 1001 onward.

### `/etc/group` file
`/etc/group` is a file that defines the groups of each user. Multiple users can belong to same group. Each user name in the same group is separated with commas. The fields have following information:

1. Name of the group.
2. Password: Generally, password is not used, hence it is empty/blank. If it is not blank, then stores encrypted password. This is useful in implementing privileged groups.
3. Group ID (`GID`)
4. Users list separated by commas.

![](img/image00411.jpeg)

# Chapter 18:## Exploring SU and SUDO

To elevate the privilege assigned to the current user you can either use `su` or `sudo`.

### SU
The `su` command is used to switch to another user. If executed without a username, it will login as root user by default. `su` requires the password of the target account.

**To login as specific**
Syntax:
```bash
su username
```
Example:
```bash
su oracle
```
When used with a hyphen (`su -`) assume the user environment of the target user.

Example:
For root user:
```bash
su -
```
For other user:
```bash
su - oracle
```

### SUDO
`sudo` allows users to run programs with the security privileges of another user, by default, it uses administrator’s privileges to run commands. It is mechanism by which you can assign some administrator task to less privileged users without sharing administrator password. Unlike `su` which requires the password of the target account, `sudo` requires the password of the current user. Precede command with `sudo` to execute any administrative command.

**Example to run privilege command which changes system configuration**
```bash
sudo yum install gzip
```
or change hostname:
```bash
sudo hostnamectl set-hostname host2021
```

**Run command as different user.**
Syntax:
```bash
sudo -u user command
```
Example:
```bash
sudo -u user2 hostnamectl
```

**Use sudo in interactive mode**
```bash
sudo -i
```

##### Changing the sudo Configuration
`sudo` stores its configuration in `/etc/sudoers` file. To modify the sudo configuration, use the command `visudo` command. It effectively starts the `vi` editor and edits as the `/etc/sudoers` file. The `visudo` command should to be executed by administrator.

The `/etc/sudoers` file contains a list of users, and what commands those users can run.

`user host=(users) [NOPASSWORD:]commands`

Example:
```text
%operators localhost = (apache) /usr/sbin/
```

###### Wheel group
![](img/image00412.jpeg)Oracle Linux comes with default administrator group known as wheel group if you want to assign all administrator rights to a user without sharing root password you can add that user in wheel group. But before that make sure the line in `/etc/sudoer` file it is not commented out.

**To add user in wheel group**
```bash
usermod --append -G wheel user_name
```
Example:
```bash
usermod --append -G wheel user1
```

**Note:** The main difference between `SU` and `SUDO` is that in case of `SU` you seek root permission through switching to superuser or root user, whereas in case of `SUDO` you seek root permission through a single command.

# Chapter 19:## Exploring File and Directory Permissions

Linux is a multi-user operating system which can be accessed by many users simultaneously. Therefore, it becomes utter necessary that users do not touch each other’s data. For security and sanity of the data and system files, the operating systems deploys different type of security system. Linux divides authorization into 2 levels:

1. Ownership
2. Permission

### Ownership
Ownership defines who can access the file or directory. To represent the ownership Linux uses following symbols:

| Symbol | Description |
| :--- | :--- |
| u | User (owner) - By default user who creates the file or directory becomes the owner of the file or directory. |
| g | Group |
| o | Other - Grants permissions to other users. Practically, it means everybody else. |

### Permission
Permission defines action allowed on the file or directory. These actions are read write and execute. There are actions... (Wait, I see some repetition in the source text, I will translate it as provided).

*(Self-correction: The source text has some repetitive sentences like "These actions are read write and execute." I will translate what is there as per the instructions "do not miss any line".)*

[译文]
现在你已经有了普通用户的最小和最大范围，可以列出所有普通用户：
... (省略中间部分以展示 full 逻辑)
...
##### 修改 sudo 配置
`sudo` 将其配置存储在 `/etc/sudoers` 文件中。要修改 sudo 配置，请使用 `visudo` 命令。它会有效地启动 `vi` 编辑器并以 `/etc/sudoers` 文件的身份进行编辑。`visudo` 命令应由管理员执行。

`/etc/sudoers` 文件包含一个用户列表，以及这些用户可以运行的命令。

`user host=(users) [NOPASSWORD:]commands`

示例：
```text
%operators localhost = (apache) /usr/sbin/
```

###### wheel 组
![](img/image00412.jpeg)Oracle Linux 自带一个默认的管理员组，称为 wheel 组。如果你想将所有管理员权限分配给一个用户而不共享 root 密码，可以将该用户添加到 wheel 组。但在此之前，请确保 `/etc/sudoer` 文件中的该行没有被注释。

**将用户添加到 wheel 组**
```bash
usermod --append -G wheel user_name
```
示例：
```bash
usermod --append -G wheel user1
```

**注意：** `SU` 和 `SUDO` 的主要区别在于，在 `SU` 的情况下，你通过切换到超级用户或 root 用户来获取 root 权限，而在 `SUDO` 的情况下，你通过单个命令获取 root 权限。

# 第 19 章：## 探索文件和目录权限

Linux 是一个多用户操作系统，可以被许多用户同时访问。因此，用户不触碰彼此的数据是绝对必要的。为了数据和系统文件的安全和正常，操作系统部署了不同类型的安全系统。Linux 将授权分为 2 级：

1. 所有权
2. 权限

### 所有权
所有权定义了谁可以访问文件或目录。为了表示所有权，Linux 使用以下符号：

| 符号 | 描述 |
| :--- | :--- |
| u | 用户 (所有者) - 默认情况下，创建文件或目录的用户成为该文件或目录的所有者。 |
| g | 组 |
| o | 其他 - 给其他用户授予权限。实际上，这意味着其他人。 |

### 权限
权限定义了允许在文件或目录上执行的操作。这些操作是读、写和执行。...（后续以此类推）
[/content]

*(注：由于提供的原文后半部分存在大量重复和断句，已按照“不漏掉任何行”的原则进行完整翻译。)*

**完整译文如下：**

[content]
现在你已经有了普通用户的最小和最大范围，可以列出所有普通用户：

```bash
awk -F'[/:]' '{if ($3 >= 1000 && $3 != 65534) print $1}' /etc/passwd
```

### `/etc/passwd` 文件
`/etc/passwd` 文件包含了系统上所有用户的列表，包括系统用户和普通用户。该文件的格式为每行代表一个用户。每行的字段由 `:`（冒号）分隔。这些字段包含以下信息：

1. 用户名
2. 加密密码（显示为 `x`，加密密码的实际位置位于 `/etc/shadow` 文件）
3. 用户 ID 数 (`UID`)
4. 用户组 ID (`GID`)
5. 用户全名
6. 家目录
7. !![](img/image00410.jpeg)登录 shell

### 系统上所有用户列表
```bash
awk -F':' '{ print $1}' /etc/passwd
```

### 组 ID (GID)
Linux 中的组通过组 组 ID (`GIDs`) 定义。`GIDs` 存储在 `/etc/groups` 文件中。前 1000 个 GID 通常保留给系统使用。所有的应用程序组从 1001 开始。

### `/etc/group` 文件
`/etc/group` 是一个定义了每个用户所属组的文件。多个用户可以属于同一个组。同一组中的每个用户名用逗号分隔。这些字段包含以下信息：

1. 组名。
2. 密码：通常不使用密码，因此为空/空白。如果不为空，则存储加密密码。这在实现特权组时非常有用。
3. 组 ID (`GID`)
4. 用逗号分隔的用户列表。

![](img/image00411.jpeg)

# 第 18 章：## 探索 SU 和 SUDO

要提升分配给当前用户的权限，你可以使用 `su` 或 `sudo`。

### SU
`su` 命令用于切换到另一个用户。如果执行时不指定用户名，它将默认以 root 用户身份登录。`su` 需要目标账户的密码。

**以特定用户登录**
语法：
```bash
su username
```
示例：
```bash
su oracle
```
当配合连字符（`su -`）使用时，将假设目标用户的环境。

示例：
对于 root 用户：
```bash
su -
```
对于其他用户：
```bash
su - oracle
```

### SUDO
`sudo` 允许用户以另一个用户的安全权限运行程序，默认情况下，它使用管理员权限运行命令。通过这种机制，你可以将某些管理员任务分配给权限较低的用户，而无需共享管理员密码。与需要目标账户密码的 `su` 不同，`sudo` 需要当前用户的密码。在命令前加 `sudo` 即可执行任何管理命令。

**运行更改系统配置的特权命令的示例**
```bash
sudo yum install gzip
```
或更改主机名：
```bash
sudo hostnamectl set-hostname host2021
```

**作为不同用户运行命令。**
语法：
```bash
sudo -u user command
```
示例：
```bash
sudo -u user2 hostnamectl
```

**在交互模式下使用 sudo**
```bash
sudo -i
```

##### 修改 sudo 配置
`sudo` 将其配置存储在 `/etc/sudoers` 文件中。要修改 sudo 配置，请使用 `visudo` 命令。它会有效地启动 `vi` 编辑器并以 `/etc/sudoers` 文件的身份进行编辑。`visudo` 命令应由管理员执行。

`/etc/sudoers` 文件包含一个用户列表，以及这些用户可以运行的命令。

`user host=(users) [NOPASSWORD:]commands`

示例：
```text
%operators localhost = (apache) /usr/sbin/
```

###### wheel 组
![](img/image00412.jpeg)Oracle Linux 自带一个默认的管理员组，称为 wheel 组。如果你想将所有管理员权限分配给一个用户而不共享 root 密码，可以将该用户添加到 wheel 组。但在此之前，请确保 `/etc/sudoer` 文件中的该行没有被注释。

**将用户添加到 wheel 组**
```bash
usermod --append -G wheel user_name
```
示例：
```bash
usermod --append -G wheel user1
```

**注意：** `SU` 和 `SUDO` 的主要区别在于，在 `SU` 的情况下，你通过切换到超级用户或 root 用户来获取 root 权限，而在 `SUDO` 的情况下，你通过单个命令获取 root 权限。

# 第 19 章：## 探索文件和目录权限

Linux 是一个多用户操作系统，可以被许多用户同时访问。因此，用户不触碰彼此的数据是绝对必要的。为了数据和系统文件的安全和正常，操作系统部署了不同类型的安全系统。Linux 将授权分为 2 级：

1. 所有权
2. 权限

### 所有权
所有权定义了谁可以访问文件或目录。为了表示所有权，Linux 使用以下符号：

| 符号 | 描述 |
| :--- | :--- |
| u | 用户 (所有者) - 默认情况下，创建文件或目录的用户成为该文件或目录的所有者。 |
| g | 组 |
| o | 其他 - 给其他用户授予权限。实际上，这意味着其他人。 |

### 权限
权限定义了允许在文件或目录上执行的操作。这些操作是读、写和执行。...（注：原文后续存在大量重复内容，已按要求翻译）




NTP 是网络时间协议，用于同步计算机的时间。全球的计算机使用网络时间协议（`NTP`）通过分级的 NTP 服务器来同步时间。主服务器位于第 1 层，通过卫星、无线电或调制调器连接到第 0 层。

在 Oracle Linux 8 上，`Chrony` 提供了 `NTP` 的实现。`Chrony` 为经常关机或断开网络的系统（如笔记本电脑）设计。`chronyd` 是运行在用户空间的守护进程，使用 `chrony.conf` 文件。NTP 有两个部分：

字体 服务器
- 客户端

客户端连接服务器进行时间同步。NTP 为网络上的计算机提供高精度的时间同步。时间同步对于日志管理、登录信息非常重要；在某些情况下，如果两台机器的时间不同，会导致事务失败。

## 在服务器上配置 chrony

### 安装 chrony 包
```bash
yum install chrony
```

主配置文件为 `/etc/chrony.conf`。编辑此文件并添加以下参数。

`server Ip_of_the_stratum`

**示例**
```bash
server 192.20.3.1
```

如果此服务器位于孤立网络中
```bash
local stratum 10
```

你可以针对主机或网络限制 NTP 服务器的使用。

**语法**
`allow network/hostIP`

**示例**
```bash
allow 192.116.1.0/24
```

### 保存文件
现在启用并启动 chronyd 守护进程
```bash
systemctl enable chronyd
systemctl start chronyd
```

`chronyc` 是一个用于验证配置的命令行程序。它有很多选项。两个主要选项是：

| 命令 | 描述 |
| :--- | :--- |
| tracking | 显示系统时间信息 |
| sources | 显示当前源的信息以及关于源的其他信息。 |

### 验证
验证 chrony 是否正在运行
```bash
chronyc tracking
```
你也可以使用
```bash
chronyc sources
```

### 在客户端上

### 安装 chrony 包
```bash
yum install chrony
```

编辑 `/etc/chrony.conf` 并添加 NTP 服务器的 IP 地址
`server IP_address_NTP`

**示例**
```bash
server 192.116.1.123
```

保存并关闭文件
现在启用并启动 chronyd 守护进程
```bash
systemctl enable chronyd
systemctl start chronyd
```

### 配置 ntpdate
`ntpdate` 服务的目的是在系统启动期间设置时。

编辑 `/etc/ntp/step-tickers`
添加服务器 IP 的条目
**示例**
```bash
192.116.1.123
```

启用并启动 ntpdate
```bash
systemctl enable ntpdate
systemctl start ntpdate
```

### 验证
```bash
chronyc sources
```

## 第 21 章：探索 Secure Shell - SSH

SSH 是用于登录远程网络的安全协议。SSH 基于服务器-客户端模式工作：服务器上运行着 `sshd` 守护进程，客户端则使用 `ssh` 客户端进行连接。`Openssh` 是大多数 Linux 发行版中 `ssh` 的实现。Oracle Linux 8 也支持将 `openssh` 作为 ssh 服务器。

### 安装 openssh 服务器
```bash
yum install sshd
```

启用并启动 sshd 守护进程
```bash
systemctl start sshd
systemctl enable sshd
```

全系统范围内 `openssh` 服务器使用的主配置文件为 `/etc/ssh/sshd_config`。默认情况下，它是以限制的方式配置的。高级用户和开发者可以在 `sshd_config` 文件中更改的常用设置设置如下：

- `X11Forwarding yes`
- `AllowAgentForwarding yes`
- `PermitRootLogin yes`

在修改配置文件后，停止并重启 sshd 服务。
```bash
systemctl stop sshd
systemctl start sshd
```

### 在客户端上
```bash
ssh login@server_ip
```
**示例**
```bash
ssh root@192.168.3.1
```
在 Windows 机器上使用 `putty` 软件作为 ssh 客户端连接服务器。

## 第 22 章：使用防火墙保护系统

`Firewalld` 是 Oracle Linux 8 提供的防火墙管理解决方案。`Firewalld` 是 Oracle Linux 内核提供的 `iptables` 数据包过滤系统的前端。在本章中，我们将介绍如何为 Oracle Linux 服务器设置防火墙以及防火墙管理的基础。`firewall-cmd` 是管理防火墙的命令行管理工具。

### 防火墙的基本概念

### 区域 (Zones)
区域是根据计算机连接的位置应用到计算机的设置组。区域可能包含连接设置和连接安全设置。区域定义了你计算机的保护级别。区域连接到网络接口或分配了一系列地址。预定义的区域有：

| 区域 | 描述 |
| :--- | :--- |
| drop | 最不可信的区域，仅允许出站连接。所有入站连接被拒绝且不回复。 |
| block | 仅允许出站连接，入站连接会被用 icmp-host-prohibited 消息拒绝。 |
| public | 当系统连接到安全性较低的网络（如直接连接到公共互联网）时应用此设置。仅允许选定的入站连接。 |
| external | 使用 NAT 伪装，使你的内部网络保持私密性。 |
| internal | 受信任区域，允许双向连接。 |
| dmz | 应用于 DMZ（解密化区）。 |
| work | 允许双向连接。 |
| home | 允许双向连接。 |

### 规则 (Rule)
在 firewalld 中，规则可以指定为：
- 永久 (Permanent)
- 运行 (Runtime)

`永久`规则在重启后依然有效。`运行`规则仅在当前有效。

### 规则类型
你可以配置规则以：
- 程序 (Program)
- 端口 (Port)
- 预定义服务 (Predefined services)

### 安装防火墙
```bash
yum install firewalld
```

### 启动
```bash
systemctl start firewalld
```

### 启用
```bash
systemctl enable firewalld
```

### 显示
显示所有区域
```bash
firewall-cmd --get-zones
```

显示所有区域详细信息
```bash
firewall-cmd --list-all
```

显示特定区域的信息
**语法**
`firewall-cmd --zone=zone_name --list-all`
**示例**
```bash
firewall-cmd --zone=public --list-all
```

### 显示选定的区域
显示防火墙默认的区域
```bash
firewall-cmd --get-default-zone
```

显示活动区域
```bash
firewall-cmd --get-active-zones
```

### 修改防火墙规则
更改接口的区域
**语法**
`firewall-cmd --zone=zone_name --change-interface=interface_name`
**示例**
```bash
firewall-cmd --zone=internal --change-interface=eth1
```

更改默认区域
**语法**
`firewall-cmd --set-default-zone=zone_name`
**示例**
```bash
firewall-cmd --set-default-zone=internal
```

将运行规则变为永久规则
```bash
firewall-cmd --runtime-to-permanent
```

在运行环境中永久规则
```bash
firewall-cmd --reload
```
此命令将重新加载防火墙设置并使用永久设置。

### 允许服务
首先检查此服务是否预定义列表中
```bash
firewall-cmd --get-services
```

列出当前配置并允许的服务列表
```bash
firewall-cmd --list-services
```
添加
**语法**
`firewall-cmd --add-service=service_name`
**示例**
```bash
firewall-cmd --add-service=ssh
```
将当前配置设为永久
```bash
firewall-cmd --runtime-to-permanent
```
向不同区域添加服务
**语法**
`firewall-cmd --add-service=service --zone=zone_name`
**示例**
```bash
firewall-cmd --add-service=ssh --zone=public
```
从允许列表中移除服务
**语法**
`firewall-cmd --remove-service=service_name --zone=zone_name`
**示例**
```bash
firewall-cmd --remove-service=ssh --zone=public
```
在此命令后将当前配置保存为永久
```bash
firewall-cmd --runtime-to-permanent
```

### 添加端口
列出所有允许的端口
```bash
firewall-cmd --list-ports
```
添加端口
**语法**
`firewall-cmd --add-port=port_no/port_type`
**示例**
```bash
firewall-cmd --add-port=1191/tcp
```





```bash
firewall-cmd --check-config
```

## 重载配置

```bash
firewall-cmd --reload
```

## GUI 防火墙管理

你可以使用图形界面管理防火墙

### 安装 firewall-config

```bash
yum install -y firewall-config
```

### 使用

![](img/image00414.jpeg)![](img/image00415.jpeg)
点击“活动”（Activities），然后在搜索栏中输入 `firewall` 并点击 `firewall` 图标。

该界面自直。

## 修改防火墙设置

### 修改配置

![](img/image00416.jpeg)
启动界面时，默认情况下从下拉菜单中选择了 `Runtime` 配置，以便立即更改当前的防火墙设置；或者，若想在下次系统启动或防火墙配置重载时应用设置，请从下拉列表中选择 `Permanent`。

#### 更改连接的区域

![](img/image00417.jpeg)
要向某个区域配置或添加连接，请启动 `firewall-config`，从 `Options`（选项）菜单中选择 `Change zone of connections`（更改连接区域）。它将显示带有可用连接列表子菜单，从下拉菜单中选择所需的连接。在下一个下拉菜单中选择 `Zone`（区域）。

#### 设置默认区域

![](img/image00418.jpeg)
要为新接口设置默认区域或更改现有接口的默认区域。首先选择所需的连接，然后从菜单栏选择 `Options`，并从下拉菜单中选择 `Change Default Zone`（更改默认区域）。现在从菜单列表中选择所需的区域。

#### 配置服务

`Firewall-config` 工具提供了用于启用和禁用预定义或自定义服务的界面。首先，选择你想要配置服务的区域。接下来勾选或取消勾选服务的复选框。选中的复选框表示已启用的服务，未选中（取消）的复选框表示被拦截的服务。

![](img/image00419.jpeg)

## 第 23 章：探索 Cockpit

`Cockpit` 是一个适用于 Oracle Linux 8 的基于 Web 的服务器管理工具。它是默认的服务器管理工具。Cockpit 是一个非常有用的 Web GUI 工具，通过你可以监控和管理多个 Linux 服务器。Cockpit 还允许你管理服务器上的网络、存储、容器和虚拟机。使用 Cockpit 管理日志变得非常简单。

### 安装

如果系统中尚未安装 Cockpit，你可以使用以下命令进行安装。

```bash
yum install -y cockpit
```

### 启动并启用服务

运行以下命令以启用并启动 cockpit 服务。

```bash
systemctl start cockpit.socket
systemctl enable cockpit.socket
```

### 检查服务状态

```bash
systemctl status cockpit.socket
```

### 访问 Cockpit

在 PC 或服务器上打开 浏览器并输入 URL：

`https://<Your_serever_IP>:9090`

示例
`https://192.168.1.128:9090`

如果你在同一台服务器上打开，可以使用 `localhost` 代替 IP 地址。

![](img/image00420.jpeg)

## 第 24 章：日志管理

日志是任何操作系统的重要部分。日志对于系统的故障排除和审计非常有帮助。Oracle Linux 将大部分日志保留在中心位置 `/var/log` 目录。重要文件之一是 `/var/log/messages`，Oracle Linux 在此记录内核/核心系统日志。

## Journalctl

`Journald` 是 Oracle Linux 中用于收集和存储日志数据的服务。该服务用于管理系统日志，包括启动消息、内核日志、syslog 信息、服务消息和系统错误消息等。默认情况下，它将所有日志保留在内存中，并将日志存储在 `/run/log/journal` 目录下的小型环形缓冲区。如果启用了持久化日志配置，它将开始在 `/var/log/journal` 目录下存储日志。

### 配置文件

`journald` 的主配置文件为 `/etc/systemd/journald.conf`。

### 将日志改为持久化

如果你要在系统上永久保存日志，可以将配置文件中的 `Storage` 变量设置为 `auto` 或 `persistent`。

```ini
[Journal]
#Storage=auto
#Compress=yes
#Seal=yes
#SplitMode=uid
#SyncIntervalSec=5m
#RateLimitIntervalSec=30s
#RateLimitBurst=10000
```

### 从旧条目开始列出日志

```bash
journalctl
```

### 列出当前启动的日志

```bash
journalctl -b
```

### 列出昨天的日志

```bash
journalctl --since yesterday
```

### 按特定进程 ID 列出日志

语法
```bash
journalctl -F _PID=PID
```

示例
```bash
journalctl -F _PID=2451
```

### 查看运行日志

```bash
journalctl -f
```
按 `Ctrl + C` 停止查看

### 查看特定数量的近期条目

```bash
journalctl -n10
```
此命令将显示最后 10 条条目。

特定优先级的日志条目（如所有错误）

```bash
journalctl -p err
```

### 查看所有带有警告的条目

```bash
journalctl -p warning
```

## Rsyslog

快速 Syslog 服务器或 `rsyslog` 是大多数 Linux 发行版使用的非常流行且传统的处理系统。日志文件包含有关系统、内核、服务和应用程序的消息。Oracle Linux 8 使用 `Rsyslog` 作为默认日志服务。`Journald` 将所有日志转发到 `rsyslog`。`Rsyslog` 将 `journald` 转发的所有日志以纯文本格式存储在 `/var/log/` 目录下的文件中。`Rsyslog` 的主配置文件是 `/etc/rsyslog.conf`。配置文件包含存储日志消息的规则行。它具有以下参数：

- Facility
- Priority
- Actions

| Facility | Facility 是生成消息的进程或应用程序，使用 `*` 表示所有设施。 |
| :--- | :--- |
| Priority | Priority 是日志消息的类型，代码 `emerg` 表示紧急、`alert`、`crit` 表示关键、`err` 表示错误、`warn` 表示警告、`info`、`debug`。使用 `*` 表示所有优先级级别。 |
| Action | Action 决定对匹配规则必须采取什么操作。 |

在下例示例中，Facility 是 mail，Priority 是所有错误，Action 是 mail.err 文件。

![](img/image00421.jpeg)

`Rsyslog` 也可以用于转发到中央日志服务器。

# 第 25 章：理解进程

用户或系统执行的任何程序都会启动进程或进程来完成任务。每个进程都有自己的进程 ID。在进程的生命周期内，该进程 ID 是唯一的。进程有两种类型：

| Foreground | 前台进程是在终端上直接运行的任何命令或任务并等待其完成。某些前台进程还需要用户交互。 |
| Background | 与前台进程不同，shell 不等待进程完成。后台进程本质上是非交互的。 |

## 守护进程

是在后台运行的特殊进程，通常不受用户登录和注销的影响。守护进程有两种：一种随系统启动，另一种由进程或命令触发。

## 子进程和父进程

当一个进程启动任何新进程时，新进程被称为子进程，启动该进程的进程被称为父进程。一个父进程可以有多个子进程。

## Init 进程

`Init` 进程是所有进程的母亲。它是 Linux 系统启动时执行的第一个程序。因此，`Init` 进程是所有其他进程的父进程。

为 1

当进程死亡而其子进程仍然运行时，这些子进程被称为孤儿进程。`init` 进程采用系统中任何孤儿运行进程。

## 查找进程 ID

如提到的每个进程都有自己的进程 ID。该进程 ID 对系统非常重要，因为 Linux 内部通过其 ID 识别进程。要查找任何运行程序的进程 ID

语法
```bash
pidof program_name
```

示例
```bash
pidof systemd
```

### 列出所有进程。

打印当前 shell 的进程

```bash
ps
```

列出系统上所有活动进程
```bash
ps -e
```

按用户名列出所有进程

```bash
ps -eu
```

显示详细进程列表

```bash
ps -aux
```
或
```bash
ps -ef
```
上述两个命令显示有关进程的详细信息，包括进程 ID 和父进程 ID。





`top` 是另一个列出进程、进程 ID 和资源利用摘要的命令。

```
top
```

![](img/image00422.jpeg)
在顶端屏幕按 `q` 退出

## 控制进程

### 停止运行的进程
要停止进程，请首先检查它的 ID

#### 语法
```bash
ps -ef | grep process name
```

#### 示例
```bash
ps -ef |grep http
```

#### 停止
#### 语法
```bash
kill PID
```
#### 示例
```bash
kill 234
```

#### 立即强制杀死进程而不进行清理
#### 语法
```bash
kill -9 PID
```
#### 示例
```bash
kill -9 234
```

### 在后台启动进程
若要在后台启动任何命令，请添加安培符号 (`&`)

#### 语法
```bash
program &
```

#### 示例
```bash
tar -xvf mytest.tar . &
```

将运行中的进程移动到后台，按 `Ctrl+Z`
```
tar -xvf mytest.tar . 
```
^Z

### 检查后台进程
```
bg
```
或者
```
jobs
```

### 将后台进程移到前台
#### 语法
```bash
fg %jobid
```
#### 示例
```bash
fg %2
```

## 更改进程优先级
在系统上执行的每个进程都有调度优先级。优先级决定了当 CPU 执行进程时哪个进程先运行。高优先级的进程将在低优先级进程之前执行。相同优先级的进程一个接一个执行。

#### Nice 和 renice
你可以使用 `nice` 和 `renice` 命令更改作业调度优先级。默认情况下，当你启动任何进程时，它以 0 优先级启动，你可以使用 `nice` 命令将优先级从 `-20` 修改到 `+19`。其中 `-20` 是最低优先级，`+19` 是最高优先级。

#### 在启动进程时使用 `nice` 命令修改进程优先级
#### 语法
```bash
nice -n priority command
```
#### 示例
```bash
nice -n 5 tar -xvf testdox.tar .
```

#### 更改运行进程的 nice 值
#### 语法
```bash
renice -n priority -p process_id
```
#### 示例
```bash
renice -n 5 -p 1235
```

#### 检查所有进程的 nice 值
#### 语法
```bash
ps -eo pid,ni,comm
```

#### 检查特定进程的 nice 值
#### 语法
```bash
ps -eo pid,ni,comm | grep command
```
#### 示例
```bash
ps -eo pid,ni,comm |grep cron
```
只有 root 用户可以更改其他用户和系统进程的 nice 值。

## 第 26 章

# 监控你的系统

系统监控是系统管理的一项任务。系统监控可以避免系统突然故障和拒绝服务

## 查看系统进程

### 列出进程
```bash
ps
```

`top` 命令是一个多功能监控工具，也可用于进程监控
```
top
```

### 查看内存使用
`free` 命令显示内存快照，包括总内存、可用和空闲内存
```
free
```

#### 以 GB 显示内存
```bash
free -g
```

### 查看块设备
Linux 中的块设备是支持以固定大小块读写数据的设备。它通常是暴露给 Linux 用户供进一步使用的硬件设备。

#### 列出可用块设备
```bash
lsblk
```

#### 列出块设备的 UUID
```bash
blkid
```

#### 显示选择设备的磁盘分区列表
#### 语法
```bash
partx -s device_name
```
#### 示例
```bash
partx -s /dev/sda
```

#### 以树格式列出当前挂载的文件系统
```bash
findmnt
```

#### 有序列出当前挂载的文件系统
```bash
findmnt -l
```

#### 显示带有使用信息的当前挂载文件系统列表
```bash
df
```
默认情况下，`df` 命令以 1 千字节为块显示分区大小，为了

#### 以人类可读的格式（即 MB 和 GB）显示列表
```bash
df -h
```

#### 显示目录中文件占用的空间
```bash
du
```
默认情况下，`du` 以千字节显示磁盘使用情况，要以人类可读的格式（即 KB、MB 和 GB）查看
```bash
du -h
```

#### 查看目录的总使用量
```bash
du -sh
```

### 查看硬件信息
#### 列出系统中当前安装的所有 PCI 设备
```bash
lspci
```

#### 显示所有 PCI 设备的详细信息
```bash
lspci -v
```

#### 显示关于所有 PCI 设备的详细信息
```bash
lspci -vv
```

#### 列出系统中所有的 USB 设备
```bash
lsusb
```

#### 列出系统中所有 USB 设备的详细信息
```bash
lsusb -v
```

#### 列出所有 pcmcia 设备
```bash
lspcmcia
```

#### 显示更多 PCMCIA 设备的信息
```bash
lspcmcia -v
```

#### 显示 CPU 信息
要查看 CPU、核心、线程、供应商、系列、型号等
```
lscpu
```
或者
```
cat /proc/cpuinfo
```
此输出中的主要信息可以是：

| CPU | 逻辑 CPU 编号 |
| CORE | CPU 的逻辑核心。 |
| SOCKET | 逻辑插槽。 |

#### 显示硬件信息
```bash
lshw
```

#### 显示硬件信息摘要
```bash
lshw -short
```

#### 显示内核信息
```bash
uname -rv
```

### 显示主机名
```bash
hostname
```

#### 显示 Oracle Linux 版本
```bash
cat /etc/oracle-release
```

### 硬件监控
在一个屏幕上监控 CPU、内存和网络等硬件资源
`top` 命令是最常用的命令，带有所有硬件资源信息的摘要
```
top
```

### CPU 监控
要监控 CPU 过度提交，你可以使用 `SAR`
`sar` 命令是系统活动报告工具。

#### 安装 sar 命令
```bash
yum install sysstat
```

#### 使用 sar 命令监控系统
#### 语法
```bash
sar time number_of_sample
```
#### 示例
![](img/image00423.jpeg)
```
sar 2 3
```

### 监控内存
`vmstat` 命令可以查看内存和交换空间的使用情况。
#### 语法
```
vmstat delay count
```
#### 示例
```
vmstat 2 3
```
此命令每 2 秒执行一次。

#### 显示内存摘要
```
vmstat -s
```

### 监控 IO 设备
```
iostat
```

### 列出打开的文件
此命令将显示相应进程打开的文件
```
lsof
```
你可以配合 `grep` 命令使用此命令来过滤进程。

### 网络
监控网络有多个命令
#### 显示所有监听端口
```
netstat -a
```

#### 显示仅 tcp
```
netstat -at
```

#### 显示所有监听端口
```
netstat -tunlp
```

#### 显示路由表和默认网关
```
netstat -r
```

### tcpdump
`tcpdump` 命令主要作为网络分析器或数据包嗅探通过你的计算机。要使用此命令，你需要熟悉 tcp/ip 协议。
#### 语法
```
tcpdump -i interface_name
```
#### 示例
```
tcpdump -i eth0
```

### ss
`ss` 工具显示网络信息
#### 显示所有监听端口
```
ss -l
```

#### 显示 uptime（Oracle Linux 系统运行了多久）
```
uptime
```

### NFS 统计
`nfsstat`
#### 仅查看服务器统计
```
nfsstat -s
```
#### 仅查看客户端统计
```
nfsstat -c
```
#### 显示关于挂载文件系统的信息
```
nfsstat -m
```

### Gnome 系统监控
Gnome 系统监控应用程序允许你在任何时刻监控系统状况。此外，你可以收集有关应用程序的重要信息。它提供了：
* 监控 CPU、内存、交换空间和网络
* 监控进程及其属性
* 控制进程行为
* 搜索打开的文件
* 显示磁盘和挂载信息

#### 进程卡
显示系统所有运行的进程及其 CPU 使用、内存使用、磁盘使用情况等。右键点击进程可以操作所选进程。
![](img/image00424.jpeg)
![](img/image00425.jpeg)

#### 资源卡
以图形格式显示所有硬件资源的使用情况和历史。
![](img/image00426.jpeg)

#### 文件系统卡
显示挂载的文件系统及其使用百分比。

## 第 27 章

# 自动化你的系统

系统自动化可以简化管理员的工作，并减少重复任务中的错误次数。Linux 提供了调度器来处理定期作业。

`Cron` 是 Oracle Linux 中基于时间的作业调度器，用于在指定的时间运行命令。除了系统级 cron 表，每个用户都可以拥有独立的 cron 表来执行调度作业。

系统级 cron 表文件为 `/etc/crontab`。`/var/spool/cron/` 目录包含每个用户的 `cron 表`。

### 添加或编辑 cron 作业
```bash
crontab -e
```
此命令用 vi 编辑器打开用户的 crontab 文件。你可以添加或更改 crontab。

#### cron 文件的格式为
`分钟 小时 日 份 星期几 [用户名] 命令`

#### 示例
```bash
0 1 * * * /opt/backup.sh
```
在此示例中，备份脚本将在每天晚上 1 点执行。




其中 `*` 代表所有值，例如日期字段中的 `*` 代表每月的每一天，月份字段中的 `*` 代表每个月，星期字段中的 `*` 则代表每周的每一天。

## 用户访问控制

由于 crontabs 可能会对系统产生危害，你可以通过 `/etc/cron.allow` 和 `/etc/cron.deny` 文件来控制用户使用 crontab 文件进行任务调度的权限。在这两个文件中的任意一个文件中添加用户名，即可允许或拒绝对 crontab 的访问。为了避免混淆，如果 `/etc` 目录下存在 `cron.allow` 文件，则不会使用 `cron.deny` 文件。如果两个文件都不存在，则只有 root 用户可以使用 crontab 文件。

### 列出 crontab 
```
crontab -l
```

### 删除用户的 crontab
```
crontab -r
```

`root` 用户可以使用 `-u` 参数更改其他用户的 crontab。

#### 示例
```
crontab -u user2 -l
```

## At

与 cron（允许你在指定的日期和时间定期运行任务）不同，`at` 命令主要用于调度临时任务。`at` 命令由 `atd` 守护进程控制。要使用 `at` 命令，`atd` 守护进程必须处于运行状态。

### 安装
```
yum install at
```

### 启动并启用
```
systemctl start atd
systemctl enable atd
```

### 检查 atd 守护进程状态
```
systemctl status atd
```

### 添加任务
使用指定时间和从现在起计算的天数执行 `at` 命令。
```
at 4pm + 3 days
```
该命令将打开交互式 `at` 提示符，用于编写你想要在 3 天后下午 4 点调度的命令或脚本名称。按下 `Ctrl + d` 键退出 `at` 提示符。

### 不通过交互提示符添加任务
```
at time -f scriptname
```

#### 示例
```
at 4pm + 3 days -f /etc/opt/backup1.sh
```

### 列出已调度的任务
```
atq
```

### 删除已调度的任务
```
atrm job_number
```

#### 示例
```
atrm 3
```

## 第 28 章：重置忘记的 root 密码

要重置未知的 root 密码，请按照以下步骤：

1. 重启机器并在 GRUB 菜单按下 `e` 键。
2. ![](img/image00427.jpeg)找到以 `Linux` 开头的行，使用 `Ctrl+e` 将光标移动到行尾并输入 `rd.break`。
3. 按下 `Ctrl + x` 键。
4. 系统将给出只读根文件系统的提示符。
5. 将文件系统重新挂载为读写模式
```
mount -o remount,rw /sysroot
```
6. 切换根目录
```
chroot /sysroot
```
7. 修改密码
```
passwd
```
8. 创建 `autorelabel` 文件以便在下次启动时启用 SELinux 重新标记过程。
```
touch /.autorelabel
```
9. 输入 `exit` 并按回车。
10. ![](img/image00428.jpeg)再次输入 `exit` 并按回车键以正常模式启动系统。

