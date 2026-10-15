
# 选择和安装不同的 Linux 发行版

本章介绍了 Ubuntu 的一些主要特性。它还描述了如何在你的计算机上安装 Ubuntu，或者运行 Ubuntu 的现场 CD 版本。

## Ubuntu 概述

尽管 Ubuntu 内部主要是一个 Debian 发行版，但 Ubuntu 对国际化和通用易用性的关注、定期的发布计划以及简化的安装过程，使其与 Debian 有了不同之处。

南非商人、互联网企业家兼代表马克·沙特（Mark Shuttle）通过 Canonical Limited (`www.canonical.com`) 赞助 Linux 上的 Ubuntu。一些最优秀、最才明的开源开发者（最初源自 Debian 项目）都在 Canonical 负责制作 Ubuntu 的团队中。该组织对免费发行版和快速开发的承诺为 Ubuntu 吸引了庞大的用户和开发社区。

## Ubuntu 版本

进入 2009 年，Ubuntu 项目已经产生了九个版本，这些版本遵循了 Ubuntu 承诺的每六个月一次的发布周期。每个版本都有一个源自发布月份的版本号，并以一种森林动物命名（这些动物可能与 Ubuntu 发源地南非的动物有所不同）：

- Warty Warthog（疣状野猪）—— 2004 年 10 月发布，Ubuntu 版本 4.10。
- Hoary Hedgehog（苍白豪猪）—— 2005 年 4 月发布，Ubuntu 版本 5.04。
- Breezy Badger（清风的獾）—— 2005 年 10 月发布，Ubuntu 版本 5.10。
- Dapper Drake（花丽鸭子）—— 2006 年 6 月发布，Ubuntu 版本 6.06。
- Edgy Eff（犀利的小精灵）—— 2007 年 4 月发布，Ubuntu 版本 6.10。
- Feisty Gawn（活泼的大鹅）—— 2007 年 10 月发布，Ubuntu 版本 7.10。
- Gutsby Goblin（胆大的小地精）—— 2008 年 4 月发布，Ubuntu 版本 8.04。
- Intrepid Beaver（无畏的海狸）—— 2008 年 10 月发布，Ubuntu 版本 8.10。

> 注意：除了定期发布外，Ubuntu 还会为需要可靠特性的用户发布 LTS（长期支持）版本。LTS 为桌面版本提供三年的支持，为服务器版本提供五年的支持。Ubuntu 8.04 是最近提供的 LTS 版本。

如果你是 Linux 的新手，Ubuntu 的设计初衷就是为了你而考虑。标准的 Ubuntu 桌面安装程序为大多数安装选项提供了一组默认设置。然而，Ubuntu 还提供了其他安装程序，在安装时包含更多个性化选择。如果你正在从 Debian（或其他另一个 Debian 派生版，如 KNOTPIX）过渡，你会发现与 Ubuntu 使用非常容易。你使用 Ubuntu 使用与 Debian 相同的方法来安装、删除包以及管理服务。

## 运行 Ubuntu Linux

从 Dapper Drake 版本开始，Ubuntu 项目为每个版本提供三张不同的 CD 或单张 DVD。CD 如下：

- **桌面安装 CD（Desktop Install CD）** —— 它会直接启动到 Ubuntu，你可以在那里尝试 Ubuntu（而不更改系统上的任何内容），或将 Ubuntu 安装到硬盘上。这与许多发行版提供的 CD 类似，不同之处在于，如果你决定这样做，它还提供了一种永久安装 Ubuntu Linux 的简单方法。（CD 包含在随附的 DVD 中。）
- **服务器安装 CD（Server Install CD）** —— 让你能够安装各种服务器配置，从基础服务器到 LAMP (`Linux/Apache/MySQL/Perl`) Web 服务器。
- **备用 CD（Alternate CD）** —— 允许你通过桌面图形安装程序提供的单行复杂菜单安装 Ubuntu 桌面系统（例如逻辑卷管理）。它还支持想要定制和出货基于 Ubuntu 系统的 OEM 公司，并提供了自定义服务器安装——但它不包含 CD。

开始使用 Ubuntu 很容易的，因为桌面 CD 会启动到一个功能完全的桌面系统。Ubuntu 安装在检测硬件、设置你的显卡环境（鼠标、键盘和显卡）方面做得非常好，并直接启动到 GNOME 桌面，而不更改你系统上的任何内容。它在桌面上包含一个图标，让你在只需经过几个配置屏幕（本章稍后讨论）后即可将 Ubuntu 安装到你的系统中。

接下来的章节描述了 Ubuntu 8.10 (`Intrepid Ibex`) 中的桌面和服务器特性。

## Ubuntu 安装程序

Ubuntu 安装程序帮助 Ubuntu 成为一个极其受欢迎的发行版，从发布之初就共享了 Ubuntu 对易用性的承诺。Ubuntu 的安装过程在检测硬件和系统配置信息方面做得非常出色。Ubuntu 的安装 CD “试驾”只需要几条额外信息即可将其软件包集安装到你的硬盘上。

其他 CD 具有更传统的、基于文本的安装程序，这对于任何 Debian 类系统的用户来说应该是熟悉的，并且被设计为可在任何具有 VGA 图形设备和 128MB 左右内存的系统上运行。本章关注图形化 Ubuntu 安装程序，但服务器 CD 和备用桌面 CD 上的文本安装程序也相当容易使用。

Ubuntu 安装程序中内置了许多易用性特性。例如，如果你不确定自己拥有的是哪种类型的键盘，你可以选择输入几个键（如安装程序提示的那样），并让它来判断出你拥有的键盘类型。你还可以在安装期间选择调整磁盘上分区的 own（如果你有一个只有一个 Windows 分区且不想完全删除它的硬盘，这是一个非常实用的功能）。

## 作为桌面的 Ubuntu

正如所承诺的，Ubuntu 8.10 包含了发布时可用的最新桌面特性。除了你预期的最新桌面组件（GNOME、OpenOffice.org 等）外，Ubuntu 8.10 还包含了用于安装应用程序和定制桌面体验的特性。以下是 Ubuntu 8.10 的一些特性：

- GNOME 桌面 —— GNOME 24 为此版本提供了桌面环境。Ubuntu 的默认主题 Human 是一棵冷静的棕色树，符合 Ubuntu 的配色方案。
- Flash 体验 —— 对 Flash 内容的处理包括改进的插件使用方式、对使用 Flash 的网站更好的体验，以及为选择替代方案的用户提供更多帮助。
- Firefox 3 —— 这一主要的 Firefox 版本提供了更高的安全性、易用性和性能。（详情请见第 6 章）。
- 打印驱动程序下载 —— 当你使用 Ubuntu 中的打印机设置而系统没有打印机驱动程序时，新工具将自动从 OpenPrinting 数据库获取所需的驱动程序。

除了这些特性外，Ubuntu 还包含了许多适用于桌面的广泛开源应用程序。领先领先的是最新版本的 OpenOffice.org（流行的办公套件）、GIMP（图像处理软件）和 Firefox（Web 浏览器）。

随 GNOME 项目一起来的许多配置和设置桌面偏好的工具非常符合 Ubuntu 的可访问性和易用性目标。GNOME 的可移动驱动器和媒体偏好窗口被设置为：当你使用 CD 或 DVD、连接外部硬盘或插入摄像头、打印机或扫描仪时立即启动应用程序。辅助技术偏好让每个视觉或身体残障的人都能使用放大镜和屏幕键盘。

图 17-1（在页）显示了这些 GNOME 工具和应用程序的一些示例。

## 作为服务器的 Ubuntu

许多对于桌面 Linux 系统没有用但对服务器很重要的特性已构建到 Ubuntu 默认服务器安装程序中，该安装程序可在 Ubuntu 服务器安装 CD（或完整的 Ubuntu 安装中使用。

作为中央计算资源，服务器需要增长，而 Ubuntu 服务器安装程序在安装期间创建 LVM 分区的功能使得你更容易在需要的地方随时为服务器添加磁盘空间。与本章稍后描述的图形化 Ubuntu 桌面安装程序不同，Ubuntu 服务器安装程序是非图形、面向终端的安装程序，无论服务器的图形能力如何，它都快速且易于使用。

# 图 17-1

使用 Ubuntu 的辅助技术和更简单的设备管理

![](img/10f390c781aed9212971eac7c34e3f1c_540_0.png)

默认软件安装在 32 位 PC 上支持高达 4GB 的内存，并还为 GFS 和 OCFS2 文件系统提供了内核支持。虽然 GFS 和 OCFS2 仍然是较新的文件系统，可能尚未准备好供您的生产系统使用，但您可以在 Ubuntu 中对其进行尝试。

要将 Ubuntu 作为瘦客户端服务器使用，需要在 Ubuntu 瘦客户端安装 Linux 终端服务器软件。您可以阅读 [如何对 Ubuntu 瘦客户端进行 LTSP 的指南](https://ubuntu.com/community/ThinClientHowTo)。

默认安装仅占用约 400MB 的磁盘空间，尽管这是一个非常精简的系统。除了基础软件包和核心实用程序外，您还获得了管理网络连接和文件系统的软件，但没有其他内容了。幸运的是，您拥有了应用程序管理工具（如 `apt-get`），因此只要连接互联网，只需一个 `apt-get` 命令即可向系统添加任何开源软件。

许多人安装的常见服务器类型是 LAMP 服务器系统，它使用 Linux 运行 Apache 服务器并提供 MySQL 数据库。它还支持 Perl 编程语言，许多 Web 应用都是用该语言编写的。Ubuntu Server 安装光盘为此类服务器系统提供了单独的程序，强调了 Ubuntu 对用户需求的关注（以及敏感性），无论他们是坐在桌面电脑系统前，还是集群化在机房内。

# Ubuntu 衍生版本 (Spin-Offs)

由于没有没有任何软件光盘能满足所有人的需求，已经从 Ubuntu 创建了一些衍生项目。以下是与 Ubuntu Linux 相关的三个合作伙伴项目：

- Kubuntu (`www.ubuntu.org`) — 该项目将最新版本的 KDE 桌面与每个 Ubuntu 版本结合起来。KDE 替换了 Ubuntu 默认使用的 GNOME 桌面。
- Xubuntu (`www.ubuntu.org`) — 该项目将 Ubuntu 的强大和易用与轻量级的 Xfce 桌面系统相结合，提供了一个对系统和图形资源要求较低的全功能版 Ubuntu。Xubuntu 功能强大，非常适合笔记本电脑。
- Eduntu (`www.eduntu.org`) — 该项目专注于制作一个适用于教室的 Ubuntu 版本。Eduntu 将 Ubuntu 与面向教育的软件（如 KDE Ubuntu 软件）以及用于创建廉价集群的软件（如 Linux Server Project）相结合。因此，Eduntu 可以以极低的成本为学校的整个计算机实验室配备运行的工作站。

其他 Ubuntu 衍生版本与主 Ubuntu 项目有不同程度的关联，包括 MythUbuntu（基于 MythTV 的多媒体播放器衍生版）、Ubuntu Mobile（为移动互联网设备设计的衍生版）和 Ubuntuuntu Remix（类似于 Ubuntu Mobile，但用于笔记本电脑）。Ubuntu spin（不含自由软件的 Ubuntu）已被放弃，转而专注于安装工具，让您在安装期间必须仅选择自由软件。

由于致力于帮助不同文化背景的人并支持多种语言和键盘类型，有 Ubuntu 社区支持来自世界各地的用户。这些包括 Ubuntu 中国 (`www.ubuntu.org.cn`)、Ubuntu 德国 (`www.ubuntu-forum.de`)、Ubuntu 瑞典 (`www.ubuntux.se`)、Ubuntu 印度尼西亚 (`www.ubuntuinux.or.id`)、Ubuntu 葡萄牙 (`www.ubuntu-pt.org`) 以及许多国际站点。

# Ubuntu 面临的挑战

尽管一声鹊起，Ubuntu 难免会有些痛苦。Ubuntu 面临的一些可能挑战：

- 与 Debian 平安共存 — 作为一个受 Debian 启发的发行版，Ubuntu 最初依赖于 Debian，并延续了 Debian Linux 中强调的许多许可、易用性和稳定性问题。Debian 社区的一些成员最初认为 Ubuntu 劫持了 Debian 项目的辛心工作。

# 安装 Ubuntu

将 Ubuntu 安装到硬盘，Ubuntu Server 至少需要 64MB 内存，Ubuntu 桌面安装需要 256MB 内存。然而，由于使用基于光盘的安装程序，至少需要 384MB 内存。

至于磁盘空间，您至少需要 4GB 空间来安装桌面系统，或者需要 500MB 磁盘空间安装最小化服务器。对于最小化服务器，您需要能够从命令行操作（不安装 GUI）。

如果您想在安装了 Windows 系统的桌面电脑上设置 Ubuntu 双启动，您可以在安装过程中调整分区大小。然而，先确保在 Windows 分区之外存在空闲空间更为简单。请参考第 8 章有关调整磁盘分区以为 Linux 安装留出空间的信息。

以下步骤描述了如何启动并安装 Ubuntu：

1. 插入 Ubuntu 安装光盘并重启电脑。您应该能看到 Ubuntu 的启动界面，如图 17-2 所示。

2. Ubuntu 桌面安装光盘提供了多种不同的选项，用于启动系统、测试安装光盘或系统内存等。它还提供了一些特殊的菜单和屏幕，你可以通过查看这些内容来激活在安装过程中如果你有特殊需求时可能帮助到你的功能。以下是你可以按下的功能键列表以及每个每个生成的菜单或屏幕的描述：

- 帮助 (`F1`) — 列出启动屏幕上可用的选项。
- 语言 (`F2`) — 允许你选择 Ubuntu 和 Ubuntu 安装程序使用的语言。
- 键布局 (`F3`) — 允许你指定 Ubuntu 和 Ubuntu 安装程序使用的键盘类型。
- 模式 (`F4`) — 允许你指定图形能力、从更新光盘添加额外的驱动程序，以及对正在启动或安装 Ubuntu 的系统进行特殊的 OEM 安装。
- 辅助功能 (`F5`) — 允许你在 Ubuntu 安装程序中激活各种与辅助功能相关的选项，包括屏幕放大器、屏幕键盘、各种提示的音频读读等。
- 其他选项 (`F6`) — 允许你修改用于启动 Ubuntu 的内核命令行，这可以让你禁用硬件系统（如电源控制）、开启更详细的调试等。

3. 若要在不修改任何这些选项的情况下继续，只需按 Enter 键启动 Ubuntu 并进入默认桌面。安装 Ubuntu 到你的硬盘的图标出现在屏幕左上角，如图 17-3 所示。

4. 当 Ubuntu 出现时，你可以在当前系统上尝试 Linux 而不对你的硬盘进行任何更改，或者将 Ubuntu 安装到你的系统中。要在你的计算机系统上安装 Ubuntu，双击 Install 图标开始安装过程。

## 图 17-3
Ubuntu 桌面和图形化安装程序的图标

![](img/10f390c781aed9212971eac7c34e3f1c_544_0.png)

## 第五部分 选择和安装不同的 Linux 发行版

5. 选择你想用于 Ubuntu 的语言。（默认是英语）。接受所选值并继续下一个屏幕，点击 Forward。你会被要求输入位置。

6. 选择你的位置。你的位置将完善所使用的语言（换句话，美国英语可能与加拿大英语不同），还将用于设置当前时间。如果显示的时间对于你的位置不正确，你可以点击 Set Time 按钮显示一个拨盘，允许你正确选择本地时间。接受所选值并继续下一个屏幕，点击 Forward。你会被要求输入键盘布局。

7. 选择你的键盘类型。接受所选值并继续下一个屏幕，点击 Forward。

你会被要求开始对你的硬盘分区。

> 注意 更改或删除磁盘分区可能会导致数据丢失。在选择分区方法之前，请仔细考虑你的选项。

8. 为你的硬盘分区选择以下选项之一。（有关磁盘分区的信息请参阅第 8 章）
- **引导 - 调整大小 (Guided - resize)** — 如果你想从现有分区获取磁盘空间用于安装 Ubuntu，请选择此项。移动滑块从所选分区获取磁盘空间。（如果你的硬盘被分为 Windows 且你想与 Ubuntu 实现双启动，可以使用此项）
- **引导 - 擦除磁盘 (Guided - erase disk)** — 这将擦除整个硬盘并自动重新分区。如果你有多个硬盘，它允许你选择使用哪一个。如果你准备好删除硬盘上的所有数据，请选择此方法。Ubuntu 安装程序将使用常用的 Linux 文件系统进行分区。
- **引导 - 使用最大空空间 (Guided - use the largest free space)** — 这允许你在已安装另一个操作系统的系统上安装 Ubuntu，只要你的系统磁盘上有足够的可用空间。第 8 章解释了如何对现有系统重新分区以为此操作腾出空间。
- **手动 (Manual)** — 这允许你手动创建自己的硬盘分区。如果你想保留现有分区不被擦除，这是最佳选择。如果你有特殊需求，例如创建分区来存放用户数据 (`/home`) 或服务器数据 (`/var`)，或者为你的硬盘的某个区域使用特定的文件系统类型，这也是最佳选择。手动分区被认为是一项更高级的技能。

如果你手动编辑了分区表，请继续下一步。否则，跳到第 10 步。

9. 在手动分区阶段，你可以指定关于如何在你安装 Ubuntu 的系统上使用分区的信息。你必须定义至少两个分区。一个分区用交换空间（swap），这是 Linux 系统用于管理虚拟内存的特殊分区格式。第二个分区用于存放 Ubuntu Linux 安装的顶层目录。

## 运行 Ubuntu Linux

在初始分区对话框中，选择你想要创建分区的空空间并点击 New Partition，这允许你指定想在分区上使用的文件系统类型，以及它是主分区还是扩展分区。单个磁盘驱动器上只能有四个主分区 — 若要在单个磁盘驱动器上创建四个以上的分区，必须将四个主分区之一定义为扩展分区，在该分区上可以定义其他（逻辑）分区。

10. 提供关于你想在该系统上创建的用户账户的信息。此账户将具有管理权限，因此你应该在此处创建你自己的账户。输入你的全名（例如，John Smith）、你将用于登录的用户名（例如，jsmith）以及该用户的密码。接受这些值并继续下一个屏幕，点击 Forward。

11. 如果安装程序询问你的硬盘中的任何信息，它会询问你是否想导入你的设置。选择你想要导入的内容并点击 Forward。

12. 一个确认屏幕总结了你选择的安装选项。要安装，点击 Install。你可以点击 Back 返回之前的屏幕并更改选择的值，或点击 Cancel 取消安装过程。如果你选择 Forward，Ubuntu 安装程序开始安装过程。

13. 安装完成后，桌面安装程序显示 Installation Complete 对话确认安装成功。当你看到这个时，可以点击 Continue 使用光盘尝试 Ubuntu，或点击 Restart Now 重启系统。

当你启动系统时，Ubuntu 会显示启动屏幕和进度对话框，随后是图形登录界面。恭喜 — 你正在运行 Ubuntu！

Ubuntu 会自动运行一个名为 Update Manager 的图形应用程序，通知你有可用更新并直接获取这些更新。如果有可用更新，Update Manager 会显示此类消息并在面板顶部提供一个图标，你可以点击它安装这些更新并保持系统最新。执行此（或任何其他）管理操作时你需要提供密码。你也可以通过选择 System Get Update 菜单手动检查更新。

# 运行 Ubuntu Linux

## 尝试桌面

使用最新的 GNOME 界面，菜单位于顶部面板上。你不会拥有你对一个功能完备的桌面系统所期的全部应用程序。不过，你可以轻松地从网上添加许多其他应用程序（后文会描述）。熟悉 Ubuntu GNOME 桌面的一个好方法是尝试其中的一些。

- 在左上角的面板上，可以通过“应用程序”（Applications）菜单访问以下类别的软件（我针对可以从其他地方获取的额外应用程序添加了一些注释）：

- 辅助工具（Accessories）——在这里，你可以选择一些属于 GNOME 项目的基础桌面实用程序。File Roller（归档管理器）提供了一个 GUI 界面，用于以各种格式和压缩类型备份个人文件。文本编辑器（Text Editor）启动图形化文本编辑器（这样你就不需要使用不直观的编辑器来编辑纯文本文档）。要进入 shell，可以从此菜单启动终端（Terminal）。其他辅助工具还包括计算器（Calculator）、字符映射（Character Map，用于映射特殊字符）和字典（Dictionary）。

- 游戏（Games）——在该菜单下，你有 17 款 GNOME 游戏可选。其中某些与你在 Windows 桌面上找到的游戏相似（例如：扫雷、纸牌接龙和数字大接龙）。还有类似俄罗斯方块的游戏（Gometro）和棋盘游戏（麻将）。你不会获得任何要求性更强的开源游戏（如 Tach Racer）或网络游戏（如 BZflag 坦克大战），但可以使用 Synaptic 软件包管理器（Synaptic Package Manager）轻松启用。

- 图形（Graphics）——Ubuntu 桌面安装了 GIMP 开源图像处理程序。它还包含了 F-Spot 照片管理器，用于管理照片集。要从扫描仪导入图像，Ubuntu 使用 Xsame 扫描应用程序。这里还包含了文档查看器，但可以使用 Synaptic 查看 Evince（可用于查看 PostScript 和 PDF 文件）以及更传统的 Adobe Acrobat。

- 互联网（Internet）——可以从此菜单启动标准的开源互联网客户端。Ekika 软件应用程序允许你从 Ubuntu 系统拨打 IP 语音电话。Evolution（一个资源密集但功能完备的邮件客户端和个人信息管理器）可用于读取和管理你的电子邮件。Firefox 是 Ubuntu 默认 Web 浏览器，Pidgin 用于即时消息。如果你需要连接到 Microsoft Windows 服务器（在需要访问 Microsoft Windows 环境的极少数情况下），此菜单还包括终端服务器客户端（Terminal Server Client）。

- 办公（Office）——Ubuntu 包含全套 OpenOffice.org 生产力应用。包括 OpenOffice.org Calc（电子表格）、Draw（绘图和流程图）、Impress（演示文稿）、Math（公式和方程）和 Writer（文字处理）。OpenOffice.org Database允许你创建和访问数据库。

- 音频与视频（Sound & Video）——Ubuntu 提供电影播放器、Sound Juicer CD 播放器和刻录、用于在线音频的 Rhythmbox 音乐播放器、Serpentine CD 创建器以及 SoundRecorder 音应用程序。与其他商业 Linux 发行版一样，

# 选择和安装不同的 Linux 发行版

Ubuntu 并没有预装播放 MP3 音乐所需的软件。然而，当你尝试从 Rhythmbox 或其他播放器播放 MP3 音乐时，系统会询问你是否从 Ubuntu 存储库添加这些功能。

Ubuntu（以及 GNOME 桌面）自带的电影播放器是 Totem Movie Player。需要额外的非开源代码才能启用视频播放器播放商业 DVD 电影。xine 和 MPlayer 等电影播放器需要无法自由分发的解码器，Ubuntu 默认不包含这些，但可以通过 Ubuntu 存储库添加。

- “地点”（Places）菜单跟踪你想去的地方，允许你连接到远程服务器，并让你看到（如果喜欢的话，还可以连接到）已打开的文档。还有一个在你的系统中搜索文件的选项。
- “系统”（System）菜单提供了更改桌面偏好和系统管理任务的选项。

# 添加更多软件

虽然 Ubuntu 允许从单张 Ubuntu CD 安装 2GB 的应用程序，但它毕竟只有 2GB。相比之下，其他包含多张 CD 的组合实现方案可以安装 7GB 或更多的应用程序。要向 Ubuntu 添加更多软件，你可以使用 Debian 打包工具（`apt-get`, `apt` 和 `dpkg`）。你也可以使用 Synaptic 软件包管理器来添加和删除软件包，它提供了一个友好的图形界面、帮助你查找包的强力搜索（Hardy Search）功能，以及相比命令行工具的其它易用性改进。

要打开 Synaptic 软件包窗口，选择 系统（System） > Synaptic 软件包管理器（Synaptic Package Manager）。图 17-5 显示了 Synaptic 软件包管理器窗口。

![](img/10f390c781aed9212971eac7c34e3f1c_549_0.png)

# 运行 Ubuntu Linux

使用 Synaptic 软件包管理器，你可以通过选择下一列中的“未安装”（Not Installed）项来安装软件，然后选择你想安装的包。选中一个或多个包后，选择“应用”（Apply），你选择的软件包将从网络存储库下载并安装。

在使用 Ubuntu 时，它会检查官方 Ubuntu 软件存储库以查找并下载你添加到 Ubuntu 的软件。有时，你可能想要官方发行版之外的社区构建软件，这些软件也被称为 Universe 和 Multiverse：

- Universe —— Universe）存储在 Universe 存储库中的软件包包含了尚未达到官方正式纳入项目标准的软件。虽然这些软件已由 Ubuntu 社区针对库进行了构建，并且在大多数情况下可以运行，但它们不提供支持或安全修复的保证。
- Multiverse —— Multiverse 存储库中的软件包包含非自由软件。

要使用 Universe 和 Multiverse 存储库，请遵循以下步骤：

1.  从 Synaptic 软件包主界面，选择 设置存储库（Settings Repositories）。将出现软件源（Software Sources），显示激活的软件存储库，如图 17-6 所示。

![](img/10f390c781aed9212971eac7c34e3f1c_550_0.png)

此时，你可以安装出现在新软件包列表中的软件包。（点击左侧列中的“未安装”，可以查看尚未从你的存储库列表中识别的任何仓库安装的软件包。）

## 获取更多关于 Ubuntu 的信息

Ubuntu 的流行导致了许多支持它的在线资源。学习 Ubuntu 或寻找特定问题答案的最佳地点之一是 Ubuntu 论坛网站 (`www.ubuntuforums.org`)。要开始参与该网站，我建议你参考 `http://ubuntuforums.org/faq.php?faq=policy` 中 Ubuntu 论坛常见问题解答指南和政策。

Ubuntu 制定了规则，并建议了获得技术支持问题的最佳方法。通过许多论坛，浏览感兴趣的话题并进行关键词搜索是寻找所需信息的好方法。

Ubuntu 论坛中有几个资源对于使用 Ubuntu 的人来说特别有用。我推荐以下内容：

- [常见问题解答 (FAQs)、教程 (HowTo)、技巧与提示](http://ubuntuforums.org/forumdisplay.php?f=100) —— 该论坛列出了许多人在安装 Ubuntu 后经常执行的步骤，例如为显卡或多媒体软件添加支持。
- [初学者交流 (Absolute Beginner Talk)](http://ubuntuforums.org/forumdisplay.php?f=73) —— 此论坛中的帖子可以帮助你理解什么是 Linux 以及 Ubuntu 是否符合你的需求。你可以在这里询问任何基础问题。
- [Ubuntu 咖啡馆 (Ubuntu Cafe)](http://ubuntuforums.org/forumdisplay.php?f=11) —— 为了感受 Ubuntu 社区的精神，你可以查看 Ubuntu 咖啡馆论坛，了解人们的想法。

Ubuntu 社区还拥有 wiki (`https://wiki.ubuntu.com`)，它持续地为使用 Ubuntu 的人积累有用内容。目前，该 wiki 包含了 Ubuntu 文档、社区信息、多语言支持、活动等多个领域。还有专门针对每个 Ubuntu 版本的区域。

## 总结

Ubuntu 是 Linux 发行版中的明日之星。Ubuntu 起于 Debian（最受推崇但对初学者来说具有挑战性的发行版之一），简化了软件包的和安装。它展示了对频繁、设计良好且受支持版本的承诺。今天，Ubuntu 不仅仅是 Debian 的衍生版，它有自己的社区、倡导者以及成熟的开发维护小组。

通过单张安装 CD，用户可以安装一组实用的桌面软件或精简的服务器系统。Ubuntu 的图形化安装程序通过将图形化安装程序与可以直接从 CD 运行的现场发行（live distribution）相结合，极大地简化了安装过程，这使得比以往任何时候都更容易测试和安装 Linux。

随着 Ubuntu 流行程度的增长，出现了一个活跃的开发者和用户社区。要参与 Ubuntu，一个很好的起点是社区论坛和 Ubuntu wiki。

## 第 18 章

## 运行 Fedora 和红帽企业 Linux (Red Hat Enterprise Linux)

2003年9月，世界领先的 Linux 发行版 Red Hat Linux 消失了。

创建 Red Hat Linux 的 Red Hat, Inc. 公司将其开发工作分为两个方向：生产 Fedora 操作系统（最初称为 Fedora Core）的 **Fedora 项目**，以及 **红帽企业 Linux (Red Hat Enterprise Linux)**。这种分裂源于试图通过一个操作系统更好地服务于两个不同的群体。Fedora 专注于鼓励感兴趣的开源开发社区，让他们帮助开发和测试有一天将进入红帽产品的软件。红帽企业版侧重于需要企业级计算解决方案的付费客户的需求。

| 本章内容 |
| :--- |
| 深入研究 Fedora |
| 继续推进 Fedora |
| 安装 Fedora |

**在 DVD-ROM 上** 本书附带的 DVD 中包含了 Fedora 10 GNOME 现场/安装 CD。你可以尝试该版本，并根据附录 A 中的描述以及本章稍后的“安装 Fedora”部分，从此 DVD 安装一个可运行的桌面系统。如果你没有 DVD，可以从互联网 (`http://fedaproject.org/get-fedora`) 下载软件并将其刻制到 CD 中，如附录 A 所示。

Fedora 和红帽企业 Linux 都源自红帽遗产的代码基础。这两个发行版有不同的目标，受众随着时间的推移可能会分得越来越远。但目前，Fedora 是一个社区驱动的发行版，旨在包含最新的 Linux 技术。Fedora 被作为红帽企业 Linux 版本的基础。

## 选择和安装不同的 Linux 发行版

尽管 Fedora 主要由红帽公司赞助并由红帽员工组成，但 Fedora 项目鼓励社区的领导和参与。最新的 Fedora 包含具有比红帽企业 Linux 更多的功能，但这些功能的稳定性保证较小，且不保证支持。关于 Fedora 方向的重大决策仍由红帽公司完全控制。同样，红帽拥有 Fedora 商标，并根据其法律顾问对 Fedora 做出决策。Fedora 的几乎所有财务支持都来自红帽。

Fedora 遵循红帽的传统。Red Hat Linux 的最后一个版本是 9。Fedora Core 1 和红帽企业 3 跟随红帽 9。在本文写作时，Fedora 10（已删除“Core”字样）和红帽企业 5.1 是这两个操作系统的最新版本。

红帽企业 Linux (RHEL) 实际上由桌面、服务器和工作站计算机系统产品代表，采用商业许可。红帽以订阅的形式将其所有的文档、培训和支持工作提供给客户。意图是让 RHEL 成为一个可靠的 Linux 系统，可以部署到整个企业中。

尽管放弃其旗舰产品 Red Hat Linux 引起了混乱，并且人们担心红帽可能会变得，但红帽仍然是生态系统中的主要参与者。Fedora 和 RHEL 之间的关系是红帽运营的核心。

## 深入研究功能

对于红帽和其他发行版为何如此流行，有许多观点。以下章节描述了被认为导致红帽成功的某些功能。

### 红帽安装程序 (Anaconda)

当许多 Linux 发行版让你苦于使用命令行来安装发行版时，红帽创建了自己的名为 Anaconda 的安装程序。Anaconda 包含了图形和文本的安装程序，是最老的持续更新版本之一。当你安装 Fedora 或企业版时，你将拥有：

- 一组适合你使用计算机的已安装软件包。
- 配置好的在线仓库。通过识别 Fedora 和第三方仓库，你可以从数千个软件包中选择下载并安装。
- 标准信息，如日期、时间、时区和语言。
- 配置好的鼠标、键盘、显卡和显示器。
- 适当分区的磁盘。
- 配置好的网卡和防火墙，以便立即连接局域网。
- 配置好的引导程序，以定义 Linux 如何启动。

除了易用之外，Anaconda 还加载了许多便于管理多个 RHEL 或 Fedora发行版安装的功能。例如，这些强大功能内置 Anaconda：

- **网络安装** —— 启动安装后，实际 Fedora 或 RHEL 发行版可以位于通过 Web 服务器 (`http`)、FTP 服务器 (`ftp`) 或 UNIX 服务器 (`NFS`) 访问的网络服务器。
- **Kickstart 安装** —— 不是坐在那里点击每一个 Fedora 系统的答案，但如果你要进行几十个或上百个这样的安装，自动化该任务可以节省大量时间。Anaconda 支持 kickstart 安装，你使用预配置的 kickstart 文件。
- **升级** —— 对于现有的 Fedora 系统，Anaconda 允许你升级到较版本的 Fedora 系统。许多用于保存配置文件备份和记录升级活动的优秀功能都内置在这一过程中。

随着 Fedora 最近的发布，Anaconda 引入了重大增强。特别是，Anaconda 现在整合了 `yum` 工具，用于收集、下载和安装软件包。在初始安装期间，你可以添加多个启用了 yum 的 Fedora 软件仓库，以便从这些仓库安装软件。

在本章的末尾，你将找到关于使用 Anaconda 安装程序安装 Fedora 的详细描述。

## 自定义版本（Spins）、安装集和 现场 CD

使用 `livecd-creator`，你可以选择在自己的现场 CD 中使用的软件包，以及你希望包含的设置（用户账户、桌面设置、网络配置等）。通过 `pungi`，你可以创建自定义的安装媒体，这样你的客户或朋友就可以安装你提供的精确系统了。

`livecd-creator` 和 `pungi` 都可以与 Anaconda 使用相同类型的 kickoff 文件运行，这允许你保存所选择的软件包和设置。因此，当新软件包可用时，只需使用 kickoff 文件重新运行构建命令，即可轻松更新你的自定义版本。

直接由 Fedora 项目本身或社区成员创建的自定义版本已经可用。例如，有包含游戏、电子设备工具、KDE 桌面和知识共享实式内容的 Fedora CD。

## RPM 软件包管理

所有 Hat 和 Fedora 发行版都使用 RPM 包管理（RPM）软件格式来存储和维护软件。Fedora 和 RHEL 包含一组工具，用于安装、升级、维护和查询 RPM 格式的软件包。本质上，安装的 RPM 软件软件包维护在数据库中，因此你可以列出软件包的内容、查看描述，甚至检查这些软件包中的文件。

使用 RPM，附加功能也可以包含在 Fedora 系统的维护中。以前必须知道如何处理 tar 包和 Makefile 来编译自己软件的用户，现在只需简单地安装 RPM 软件包来获取他们想要的功能。由于其他 Linux 发行版（如 SUSE 和 Mandrake）也使用 RPM 打包，你的 RPM 工具技能也可以帮助你管理这些发行版上的软件。诸如 `yum` (`www.linux.duke.edu/projects/yum`) 和 `apt4rpm` (`http://apt4rpm.sourceforge.net`) 等工具可更新指定的软件。

所述，`yum` 是在 Fedora 和 RHEL 中安装 RPM 软件包的基础。出于几个原因，`yum` 通常优于 `rpm` 命令。首先，它可以从网络仓库进行安装。其次，它可以找到并安装你请求的软件包所需的依赖项。第三，它被青睐是因为有相关的工具用于搜索和管理仓库。`yum` 还可以从本地媒体进行安装，并且与 `RPM` 不同，它可以自动解决依赖关系。

## 最新桌面技术

通过紧最新技术，Fedora 项目帮助用户发现桌面技术的最新创新。在过去的一年中，Fedora 发布了新的桌面技术，如 KDE 4.1 和 GNOME 桌面（在第 3 章描述）。

Fedora 是第一个将 KDE 4 作为其默认 KDE 环境的发行版。最明显的新功能包括新 Plasma 桌面能够将小组件直接放在桌面上。这允许照片查看器、系统监器和股票报价器等微应用程序直接位于桌面上。Photon 多媒体功能为 KDE 音乐和视频应用提供了一个单一框架。新的 Oxygen Arctic 为 KDE 桌面提供了新外观。一个名为 Dolphin 的轻级文件管理器现在被用默认文件管理器。

GNOME 桌面的目标是提供一个适用于从 Web 直接运行应用程序并在在线存储信息的桌面。这使得桌面成为 Facebook、Glick、Flickr、Netflix 以及其他在线服务的窗口。图 18-1 显示了在线桌面的示例。

默认情况下，在线桌面启动时会打开 Firefox 浏览器。它在屏幕左侧包含一个侧边栏——你经常在线运行的应用程序面板。

## 第五部分 选择和安装不同的 Linux 发行版

图 18-1

Fedora 提供了 GNOME 在线桌面。

![](img/10f390c781aed9212971eac7c34e3f1c_559_0.png)

## 系统配置工具

Red Hat 创建了一套简化的、图形化的工具，用于配置和管理 Red Hat 系统中的许多管理功能。使用这些工具，你可以添加打印机、配置网络、添加用户、使用声卡并调整显卡，这只是它们涵盖的功能中的一部分。

Red Hat 的图形化配置工具（在第 10 章描述）可以从“管理”菜单或从命令行启动。

> 注意：几个版本以前，这些工具命令名称的开头从 `redhat-config` 变为 `system-config`。例如，在 Fedora 中配置配置的工具现在被称为 `system-config-network`（不再是 `redhat-config-network`）。

## 运行 Fedora 和 Red Hat Enterprise Linux

## 进阶 Fedora

Fedora 在服务开源软件开发社区以及那些想要为了不同目的重新封装 Linux 的人员方面做得很好。如果你想以以下方式使用它，Fedora 特别出色：

- **个人桌面** —— 如果你处于技术端并想要最新的 Linux 技术，Fedora 可以是一个很棒的选择。你可能需要处理比其他 Linux 系统更多的软件更新和一些不完整的功能。然而，对于想要尝试最新桌面功能的用户来说，这是很小的代价。
- **个人服务器** —— 许多人将 Fedora 作为文件、打印或 Web 服务器，效果良好。SELinux 安全可以帮助 Fedora 成为最安全的平台之一，同时提供前端的服务器功能。
- **构建自己的 Linux 系统** —— 通过构建自己的现场或安装 CD，你可以重新封装 Fedora 以包含你需要的软件。你甚至可以为 Fedora 构建自己的软件软件包和仓库。由于 Fedora 允许分发，你不必担心潜在的版权或专利侵权。
- **开发软件** —— 许多人使用 Fedora 开发他们的开源项目。使用 Fedora，软件开发者可以在最新系统进行测试。对于企业级软件产品，开发者可以测试最终进入 Red Hat Enterprise Linux 的功能。Linus Torvalds 本人使用 Fedora，主要是因为它对 PowerPC 硬件的支持。

Fedora 项目致力于一个原则：Fedora 中的所有内容都应该是可以自由分发的，并且几乎都是开源的（固件驱动除外）。虽然提供非免费软件（特别是多媒体解码器）使得 Fedora 对普通用户的吸引力，但开源认为 Fedora 是一个可靠的发行版。

除了对开发社区有价值外，许多非技术人员也使用 Fedora。由 Fedora 项目收集的数据 (`http://fedoraproject.org/wiki/Statistics`) 显示，在 Fedora 9 发布的前10 周内，系统更新来自 70 万多个唯一的 IP 地址。由于许多 Fedora 系统位于 NAT 防火墙之后，一个 IP 下有多个系统，安装的 Fedora 9 系统数量可能多得多。

如果你对 Fedora 感兴趣，以下章节描述了如何参与。
要成为 Fedora 社区的正式成员，你可以访问加入 Fedora 页面 (`http://fedoraproject.org/join-fedora`)，它将引导你了解 Fedora 项目的机会并帮助你注册。

## 选择和安装不同的 Linux 发行版

## 日益增长的 Fedora 社区支持

FedoraProject.org 是关于 Fedora 项目涉及的计划、目标和倡议的官方信息网站。如果你想参与 Fedora 相关的项目，例如大使、营销、Live CD 或文档工作，FedoraProject.org 是寻求问题和开展倡议的焦点。

FedoraForum 提供了新闻、画廊以及（正如你可能猜到的那样）用于分享关于 Fedora 问题和信息的论坛。在撰写本文时，FedoraForum.org 已经拥有了超过 100,000 名成员。

非官方的 Fedora 常见问题（`www.fedorafaq.org`）已成为获取关于 Fedora 最常见、最困扰问题答案绝佳资源。该 FAQ 是学习如何获取所有所需物品（MP3 播放器、观看 DVD 电影、消息传递、视频播放器、访问 Windows NTFS 文件系统等）的好去处。

总的来说，可用软件总量的增加以及软件仓库更高的稳定性，意味着你可以获得比以往在 Red Hat 上使用 Fedora 更好的体验。

## 加入 Fedora 特别兴趣小组 (SIG)

Fedora 社区的人们聚集在一起形成特别兴趣小组（SIG），与 Fedora 追求共同的目标。某些小组继续使用邮件列表、IRC 频道上的定期会议以及 Fedora.org wiki 页面进行交流。以下是一些你可能感兴趣的 Fedora SIG：

- [每个孩子一台电脑 SIG](http://fedoraproject.org/wiki/OLPC) — 你可能听过过 OLPC 项目（`www.olpc.org`），旨在为世界地的儿童提供低成本笔记本电脑。但你可能不知道笔记本电脑内部的操作系统是 Fedora。Fedora OLPC SIG 正在探索 Fedora 项目为 OLPC 提供软件和基础设施支持的方法。

- [游戏 SIG](http://fedoraproject.org/wiki/SIGs/Games) — Fedora SIG 在封装开源游戏和解限制的商业游戏以使其在 Fedora 上运行方面做得非常出色。要参与其中，你可以加入 fedora-games-list 邮件列表，在 irc.freode.net 的 #fedora-games 频道进行聊天，或者查看 Fedora SIG wiki 页面。

- [艺术团队 (artTeam)](http://fedoraproject.org/wiki/Artwork) — Fedora 艺术团队为创意人士为 Fedora 贡献力量提供了途径。在鼓励使用开源工具的同时，艺术团队创建了标志、背景、横幅、海报和其他艺术作品来支持 Fedora。

## 运行 Fedora 和红帽企业 Linux

- [教育 SIG](http://fedoraproject.org/wiki/SIGs/Education) — Fedora 教育 SIG 致力于将更多教育应用引入 Fedora，然后制作 Fedora 教育发行版（Education Spin）以高效分发这些软件。

- [Spins SIG](http://fedoraproject.org/wiki/SIGs/Spins) — 创建 Spins SIG 的目的是帮助人们创建自己的 Fedora 变体（spin）。任何人都可以创建一个变体并提交给 Spins SIG 审批。如果符合 Fedora 项目的要求，该变体可以由 Fedora 托管，或者按照指令为 Fedora 制作变体（通常是启动性的）。

还有其他有趣的 SIG，如 Fedora 机器人 SIG、天文学 SIG、嵌入式系统 SIG 和商店 SIG。此外，你还可以加入一些改进文档、wiki、翻译和其他领域的努力。

## 论坛和邮件列表

如果你想融入 Fedora 社区的节奏，我建议从 Fedora 项目自己的邮件列表开始。你可以从红帽邮件列表页面（`http://redhat.com/mailman/listinfo`）选择你感兴趣的 Fedora 邮件列表。从 Fedora-list 或 Fedora-announce-list 邮件列表开始。

## Fedora 的成熟

大多数关注 Linux 的人都会认为， Fedora 已经成为一个强大且可行的 Linux 系统，而不仅仅是红帽企业 Linux（Red Hat Enterprise Linux）的测试版本。该项目持续增长和繁荣，当前的 Fedora 版本是这一伟大系列中的最新化身。图 18-2 显示了一个标准桌面。

虽然 Fedora 仍在为红帽企业 Linux 奠定基础，但它添加了一些强大的功能，以与其他 Linux 系统区分开来。以下是一些例子：

- PackageKit — 过去，Fedora 放弃了安装和更新软件的图形化工具（yum 和 pint），转而使用 PackageKit 设施。虽然 Fedora 仍在适应中，但 PackageKit 提供了简化的工具来获取新软件包和软件更新。面板中的 PackageKit 小程序会在更新可用时发出提醒，并允许你选择并安装它们。

- NetworkManager — NetworkManager 最近被添加为启动和停止网络连接的默认工具。通过启动 NetworkManager 服务并在面板中选择 NetworkManager 小程序，你可以看到检测到的无线设备并选择你想要连接哪一个。你也可以启动和停止有线网络接口。

图 18-2
Fedora 包含了 GNOME 或 KDE 桌面以及许多游戏。
![](img/10f390c781aed9212971eac7c34e3f1c_563_0.png)

- KVM 和 Xen 虚拟化 — 在一台计算机上运行多个操作系统的能力只是虚拟化为 Linux 带来承诺的开始。在当今的服务器计算模型中，通常整个服务器用于运行特定的应用程序，该程序可能与特定的操作系统绑定。结果是，如果不是高需求应用程序，计算机可能会闲置。

通过虚拟化，你有机会运行多个实例，包括整个系统或一个应用程序。这些实例（称为虚拟机）可以是 Linux、Windows 或任何运行在硬件上的其他操作系统。

## 运行 Fedora 和红帽企业 Linux

红帽公司（Red Hat, Inc.）为 Linux 内核中的 KVM 虚拟化软件投入了大量开发。它继续在 Fedora 和 RHEL 中支持 Xen。

- AIGLX 桌面特效 — 加速间接 GLX (AIGLX) 项目是 Fedora 社区与 X.Org 服务器项目之间的合作努力。通过支持 DRI 和 GLX 的显卡（访问 `http://fedoraproject.org/wiki/RenderingProject/aiglx` 获取支持信息），你可以看到惊艳的桌面特效。

如果 Fedora 是如此优秀的产品，你可能会疑惑为什么要购买红帽企业 Linux。选择 RHEL 而不是 Fedora 的主要原因是是对关键系统的支持保障。你可能需要比 Fedora 提供的更长的关键修复和安全补丁支持期。

我认识的许多人，特别是喜欢获取最新功能的人，将 Fedora 用于他们的个人桌面和服务器系统。他们不在意每隔一段时间升级一次，并且可以接受某种程度的不稳定性。如果你也有审美，Fedora 可能是非常适合你的 Linux 发行版。

## 安装 Fedora

由红帽赞助的 Linux 操作系统 Fedora 包含在本书 DVD 中。本章其余部分将引导你完成安装。

在计算机上安装 Fedora 之前，请确保你的硬件支持它。你还应该选择一种安装方法。这些主题将在后续章节讨论。

## 选择计算机硬件

本书附带标准 PC (x86) 版 Fedora。对于不同的硬件（如 PowerPC 或 64 位机器），请访问 Fedora 网页（`http://fedoraproject.org/get_fedora`）获取下载适用于你架构的 Fedora 信息。

- 处理器 — 文本模式需要 200 MHz 的 Pentium PC，GUI 需要 400 MHz 的 Pentium II。

- 内存 — 安装 Fedora 至少需要 64MB 内存。如果你运行图形模式，至少需要 192MB。图形模式的推荐内存为 512MB。

# 选择和安装不同的 Linux 发行版

- DVD 或 CD 驱动器 — 你需要能够从 DVD 或 CD 启动（后者需要按照 `http://fedoraproject.org/get-fedora` 的说明获取 Fedora 安装 CD）。如果你无法从 DVD 或 CD 启动，有方法可以从硬盘或使用 PXE 安装来启动安装，接下来的章节“选择安装方法”详细解释了这一点。

- 硬盘 — 在 Fedora 10 中没有预设安装，所有内容都是自定义安装的。因此，取决于你选择安装哪些包，你为 Fedora 桌面 CD 所需的磁盘空间建议范围从 600MB（安装精简版服务器版）到 7GB（安装所有软件包）。

- 键盘和显示器 — 至少在安装期间你需要键盘和显示器。（你可以通过网络 shell 界面或 X 终端在局域网（LAN）上非常良好地运行 Fedora）

正如前面提到的，尽管书中未包含在内内，但 Fedora 版本适用于 PC 和 64 位架构。红帽企业 Linux（你需要从 Red Hat 购买）适用于其他硬件，例如 Itanium、IBM PowerPC 和 IBM 主机。

书中描述的大部分软件在任何这些硬件环境中工作方式都相同。（访问 fedaproject.org 查找为不同计算机硬件架构提供 Fedora 的站点）

要启动 Fedora，你还需要拥有安装媒体，例如随书附赠的《Linux 圣经》2009 版 DVD（一套你欠自己的 CD）。你还必须将你的多余空闲硬盘（或额外添加的硬盘）留给 Linux，即一个预定义的 Linux 分区，或者在你的硬盘上任何现有分区之外留出空闲空间。

> 注意：如果你没有将整个硬盘都留给 Fedora 且你不了解分区，请参阅第 6 章，该章节描述了如何设置分区以允许多个操作系统在同一块硬盘上共存。在安装新操作系统或做出重大更改之前，请务必先进行备份。

# 选择安装方法

你也可以从几种不同类型的介质安装 Fedora。你仍然可以通过启动安装 DVD 来开始安装。然而在启动安装过程后，你可以在启动提示符处输入 `linux askmethod`，这将为你提供从以下位置安装 Fedora 选择：

# 运行 Fedora 和红帽企业 Linux

- 本地 DVD 或 CD-ROM — 这是安装 Fedora 最常用的方法，也是你在 Fedora 安装启动提示符处按回车键获得的方法。本节同时适用于 DVD 和 CD 安装。（如果 DVD 或 CD 无法启动，你可能需要更改 BIOS。）完成安装所需的所有软件包都在随书附赠的 DVD 上。对于随书 DVD 中包含的 live CD，你需要选择 Fedora 启动并安装该 live CD。

- HTTP — 允许你从网页地址 (`http://`) 安装。

- FTP — 允许从 FTP 站点 (`ftp://`) 安装。

- NFS 镜像 — 允许你使用网络文件系统 (`NFS`) 功能从另一台计算机或你网络上的任何共享目录进行安装。

- 硬盘 — 如果你在硬盘上复制了一个 Fedora 发行版的副本，你就可以从那里安装。（该发行版应位于一个你未在其上进行安装的硬盘分区上）。

> 注意：与早期的 Fedora 和红帽 Linux 版本不同，当前的 Fedora 版本不再支持软磁盘镜像，因为 Linux 2.6 内核太大，无法放入软磁盘。如果你没有可启动的 CD 或 DVD 驱动器，你将需要从其他介质（如 USB 闪存、PXE 服务器或硬盘）启动安装过程。

# 在多台计算机上安装

如果你在许多台配置相似的计算机上安装 Fedora，你可以使用 Kickstart 安装来节省一些时间，它允许你创建一组针对 Fedora 在安装过程中向你提问的解答。在你安装完 Fedora 系统后，`kickstart.ks` 会被复制到你的 `/root` 目录。你可以将该 kickstart 文件作为未来 Fedora 安装的依据，以便在随后的安装中做出相同的选择。

# 安装指南

Fedora 安装指南提供多种语言版本。要下载安装指南的归压缩包（tarball）或直接在线阅读，请参考此站点：

```
