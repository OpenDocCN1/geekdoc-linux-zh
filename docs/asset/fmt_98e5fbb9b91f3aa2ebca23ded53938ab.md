
本书的第一部分旨在帮助你快速启动 Ubuntu。它提供了 Ubuntu 及其当前功能的介绍。详细列出了大约 30 分钟或更短的简化安装程序。安装程序提供了良好的注释，描述了每个步骤。然后你将学习桌面的基础知识和设置偏好。

第二部分涉及系统配置、网络连接和软件管理。常见的系统配置任务（如添加打印机和设置保护）以最简单的方法呈现，无需管理章节中描述的复杂细节。书中讨论了基础网络连接任务，以及设置局域网和无线连接。你将学习如何使用仓库更新和安装软件。软件更新程序检测更新并让你只需点击即可完成所有更新。

本书第三部分涉及 Linux 常用的两种 GUI：KDE 和 GNOME。详细描述了不同的功能和方面，如控制面板和配置工具。你随时可以打开一个终端窗口，在其中输入标准的 Linux 命令。

第四部分涵盖 Shell 命令和配置以及文件和目录管理。你可以使用标准的 Unix 命令行运行任何标准命令。书中检查 BASH Shell 及其各种文件和目录命令，以及配置文件。

第五部分讨论了可以在 Linux 系统上使用的文件、多媒体和互联网应用，如 OpenOffice 和 KOffice 等办公套件。提供了多种不同的编辑器，包括几种 GNOME 和 KDE 编辑器，以及 Vim。Linux 自动安装邮件、新闻、FTP 和网络浏览器应用程序。KDE 和 GNOME 都配备了一套邮件、新闻、FTP 客户端和网络浏览器。

第六部分演示了如何使用加密、身份验证和验证来实现安全保护。对 GNU 隐私卫 `GPG` 的涵盖告诉你如何实现基于公私钥的加密，以及如何配置 `PolicyKit` 来控制对管理工具的访问。`AppArmor` 和 `SELinux` 为所有的网络和系统资源提供了全面且精细的控制。网络安全主题涵盖

使用 `netfilter` `iptables` 进行防火墙和加密以保护系统，使用 Secure Shell `SSH` 提供安全的远程传输，以及使用 `Kerberos` 提供安全的身份验证。

第七部分讨论了系统和网络管理主题，包括用户、文件系统、设备和内核管理。详细描述了用于管理任务的配置文件文件以及如何进入这些文件。演示内容包括你可以用于这些任务的 GUI 工具，以及底层的配置文件和命令。首先，涵盖了基本的系统管理任务，如管理运行级别、监控系统和调度关机。还讨论了设置和控制用户组的方面。涵盖了不同的虚拟化方法，如全虚拟化 `KVM` 和半虚拟化 `Xen`。通过虚拟机管理器 `Virtual Machine Manager`，可以轻松地使用这两种方法安装和运行客操作系统。涵盖了不同的文件系统任务，如挂载文件系统、使用 `HAL` 和 `udev` 管理文件系统，以及配置 `RAID` 设备和 `LVM` 卷。设备通过 `udev` 和 `HAL` 自动检测。讨论了备份管理工具，包括 `BackupPC` 和 `Amanda`。详细讨论了用于互联网寻数的 `IPv6` 支持，展示了取代旧版 `IPv4` 的新 `IPv6` 格式。你还学习了 `IPv4` 动态主机配置协议 `DHCP` 服务器如何动态分配 IP 地址，以及 `IPv6` 自动寻址和重命名是如何工作的。

第八部分涵盖了本地网络服务，如 `CUPS` 打印服务器、网络文件系统以及 `Samba` Windows 服务器。介绍了用于 Unix 的网络文件系统 `NFS`。关于 `Samba` 的章节展示了如何访问 Windows 文件系统和打印机。

附录提供了获取 Ubuntu 磁盘镜像以及创建自己的 Ubuntu Live 和安装 CD/DVD 光盘的信息、网站和细节。

## 部分

## 入门

## 第 1 章：Ubuntu 简介

## 第 2 章：安装 Ubuntu

## 第 3 章：界面基础：登录、桌面与帮助

# 章节

## Ubuntu 简介

Ubuntu 目前是广受欢迎的终端用户 Linux 发行版之一（`www.ubuntu.com`）。它由 Ubuntu 基金管理，该基金会由 Canonical, Ltd.（`www.canonical.com`）赞助，这是一个支持和推广开源项目的商业 way。Ubuntu 项目由南非 Debian Linux 开发者 Mark Shuttleworth 发起。Ubuntu 基于 Debian Linux，Debian 是最老的 Linux 发行版之一，致力于整合尖端开发和特性（`www.debian.org`）。Debian Linux 是一个开源操作系统，依赖于全球范围内志愿者的协作。

Ubuntu 提供了一个基于 Debian 的稳定、可靠且易于使用的 Linux 发行版。它被设计成一种每个人都可以轻松使用的 Linux 操作系统。Ubuntu 的名字意思是“对他人的仁心”。正如 Ubuntu 项目所描述的，“Ubuntu 是一个非洲词汇，意思是‘对他人的仁心’，或者‘因为大家的存在，我才成为了我’。这个发行版将 Ubuntu 精神带入了软件世界。”

官方 Ubuntu 哲学列出了以下原则：

- 每一个计算机用户都应该有自由为了任何目的下载、运行、复制、分发、学习、共享、更改和改进他们的软件，而无需支付许可。
- 每一个计算机用户都应该能够以他们选择的语言使用软件。
- 每一个计算机用户都应该获得使用软件的机会，包括受任何残疾影响的用户。

对语言的强调反映了 Ubuntu 的国际化范围。它旨在成为一个不关注任何单一市场的全球性发行版。语言支持通过其国际化项目（标记为 `i18n`）集成到 Linux 中。你可以在 `www.li18n.net`（Linux 基金会）和 `www.open11n.org` 等网站找到关于 `i18n` 的信息。

为所有用户提供软件涉及对残障用户的完全无障碍支持，以及使用在线存储库访问软件的无缝集成，只需点击一下即可为所有用户提供海量软件。Ubuntu 还充分利用自动设备检测的最新进展，大大简化了安装以及对可移动设备和附加存储的访问。

## 第一部分：入门

Ubuntu 旨在提供一个完全支持、可靠、开源免费、易于使用和修改的 操作系统。Linux 对其发行做出了以下承诺：

- Ubuntu 将始终免费，包括企业版和安全更新。
- Ubuntu 拥有来自 Canonical 以及全球数百家公司的全方位商业支持。
- Ubuntu 包含了免费软件社区能提供的最佳翻译和无障碍基础设施。
- Ubuntu CD 仅包含免费软件应用程序；鼓励你使用免费和开源软件，改进它们并传下去。

## Ubuntu 版本

Ubuntu 同时提供长期支持和短期支持版本。长期支持 `LTS` 版本。

安装 Ubuntu 已被大幅简化。系统会安装一组核心应用程序，你可以根据意向向其添加。安装完成后，可以从在线存储库下载额外的软件。安装界面数量减少，允许用户快速通过默认分区、用户设置和时间设置。显卡和网络连接等硬件现在会被自动配置和检测。

Ubuntu Linux 发行版可以在许多网站在线获取。Ubuntu 在 `http://www.ubuntu.com/getubuntu` 拥有自己的网站，你可以在那里下载当前版本的 Ubuntu。

## Linux

Linux 是一种用于 PC 和工作站的快速、稳定且开源的操作系统，具有专业级的互联网服务、广泛的开发工具、完全图形化的用户界面 `GUI` 以及从办公到多媒体的海量应用程序。Linux 是由 Linus Torvalds 在 20 世纪 90 年代初开发的。

大多数操作系统如 Windows 已经升级到 Linux。

## 第 1 章：Ubuntu 简介

与官方 Unix 操作系统不同，Linux 是根据自由软件基金指定的 GNU 公共许可证 `GPL` 免费分发的，任何想使用它的人都可以获得。Linux 在技术上是操作系统内核——核心操作部分——且仅存在一个官方 Linux 内核。

## 开源软件

Linux 是在互联网上作为协作开源努力开发的，因此没有公司或机构控制 Linux。为 Linux 开发的软件反映了这一背景。当 Linux 用户决定合作进行某个项目时，开发通常就会发生。软件被发布在互联网网站上，任何 Linux 用户都可以访问该网站并下载软件。

## 第一部分：入门

环境并且在范围内是全局，汇聚了世界各地的程序员。启动一个基于 Linux 的软件项目唯一需要一个网站。

大多数 Linux 软件都是以开源软件的形式开发的，其源代码随应用程序一起免费分发。互联网上的程序员为软件软件包的开发做出贡献，修改并纠正源代码，这些代码被包含在所有的发行版本中，并可以在互联网上免费获取。许多主要的软件开发工作也是开源项目，`KDE` 和 `GNOME` 桌面及其大多数应用也是如此。由 Sun 支持的 `OpenOffice` 办公是一个基于 StarOffice 办公套件（Sun 的 OpenOffice 商业版）的开源项目。你可以在 `www.opensource.org` 找到更多关于开源倡议（Open Source Initiative）的信息。

开源软件受公共许可证保护，这些许可证防止商业公司通过添加自己的修改、对这些更改申请版权，并将软件作为自己的产品销售来控制该软件。最流行的公共许可证是 GNU `GPL`，Linux 正根据该许可证分发，它由自由软件基金提供。GNU `GPL` 保留了版权，免费许可软件，并要求软件及其对它的任何修改必须免费可用。创建了其他公共许可证以支持不同类型的开源项目的开发。GNU 较小公共许可证 `LGPL` 允许使用 GNU 软件库。Qt 许可证 `QPL` 允许开源开发者使用 Qt 库来扩展 `KDE` 桌面。

Linux 目前根据自由软件基金提供的 GNU 公共许可证许可，通常被称为 GNU 软件（见 `www.gnu.org`）。GNU 软件免费分发，前提是它免费分发给他人。GNU 软件提供了既可靠又有效的工具。许多受欢迎的 Linux 工具，如 C 编译器、编辑器和 GNU 软件应用程序。随你的 Linux 发行版安装的是 GNU C++ 和 Lisp 编译器、`Vi` 和 `Emacs` 编辑器、`BASH` 和 `TCSH` 壳，以及 Tex 和 Ghostscript 文档编辑器。许多开源项目根据 GNU `GPL` 许可。大多数这些应用程序可以在 Ubuntu 软件仓库中可用。第 6 章和第 7 章描述了从互联网网站下载软件并将其安装到系统中的过程。

在 GNU `GPL` 的条款下

## Ubuntu 版本

Ubuntu 以多个版本发布，每个版本都为不同的用户群或功能而设计（见表 1-1）。这些版本安装不同的软件集合，如 `KDE`、`Xfce` 桌面、教育软件和多媒体应用。ISO 镜像可以直接下载，也可以使用 BitTorrent 应用程序。

## 第 1 章：Ubuntu 简介 7

| Ubuntu 版本 | 描述 |
| :--- | :--- |
| 桌面安装 | 使用 GNOME 桌面的 LiveCD，`www.ubuntu.com/getubuntu`。 |
| 服务器安装 | 安装服务器软件（无桌面），`www.ubuntu.com/getubuntu`。 |
| 备用安装 | 安装增强功能，`www.releases.ubuntu.com`。 |
| Kubuntu | 使用 KDE 代替 GNOME 的 LiveCD，`www.kubuntu.org`。 |
| Xubuntu | 使用 Xfce 桌面代替 GNOME，`www.xubuntu.org`。适用于笔记本电脑。 |
| Edubuntu | 安装教育软件：桌面、服务器和附加 CD，`www.ubuntu.org`。 |
| Gubuntu | 仅使用开源软件；无法访问任何种受限软件，`www.ubuntu.com`。 |
| Ubuntu Studio | 带有多媒体和图形制作应用程序的 Ubuntu 桌面，`www.ubuntustudio.org`。 |
| Mythubuntu | 带有 MyTV 多媒体和数字视频录制器 `DVR` 的 Ubuntu 桌面，`www.mythubuntu.org`。 |

**表 1-1** Ubuntu 版本

Ubuntu 桌面版为终端用户提供标准功能。标准的 Ubuntu 版本提供一个使用 GNOME 桌面的 LiveCD。大多数用户会安装这个版本。这是你从 `www.ubuntu.com/getubuntu/download` Get Ubuntu 下载页面下载的 CD 镜像。

那些想要运行 Ubuntu 作为服务器以提供互联网服务（如网站）的人将使用 Ubuntu 服务器版。服务器版仅提供简单的命令行界面；它不安装桌面。它主要为运行服务器设计。请记住，你可以先安装桌面，稍后从带有桌面的系统从 Ubuntu 仓库下载服务器软件。你不需要安装服务器版来运行服务器。服务器版可以从 Get Ubuntu 下载页面下载。

想要增强型操作系统功能（如 `RAID` 阵列或文件系统加密）的用户使用备用版本。备用版本与桌面版和服务器版一起，可以直接从 `http://releases.ubuntu.com/hard/` 或 `http://releases.ubuntu.com/64/` 下载。

其他版本为某些用户组使用不同或专门的软件集合。版本的链接列在 `www.ubuntu.com` 网页上。从那里你可以下载它们的 live CDs。Kubuntu 版本使用 `KDE` 代替 `GNOME`。Xubuntu 使用 `Xfce` 桌面代替 `GNOME`。这是一个精简且高效的桌面，非常理想的笔记本电脑和较小电脑的低功耗使用场景。Edubuntu 版本提供教育软件，也可以与学校网络上的专用 Edubuntu 服务器配合使用。Gubuntu 版本是标准版本的修改版，仅包含开源软件，无法访问任何种商业软件，包括受限的供应商显卡驱动程序（如 Nvidia 或 ATI 的）。仅使用 X.org 开源显示驱动。Ubuntu Studio 版本是一个新版本，提供一组多媒体和图像制作软件。Mythbun 版本设计用于安装和运行 MyTV 软件，让你的 Ubuntu 作为多媒体 DVR 和视频播放系统运行。

Kubuntu 和 Edubuntu 版本可以直接从 `http://releases.ubuntu` 下载。

Gubuntu、Mythubuntu、Xubuntu 和 Ubuntu Studio 都可用，以及其他版本和 Ubuntu 发布，位于 `cdimage.ubuntu.com` 的 cdimage 服务器。

注意所有版本都以 LiveCD 或 DVD 安装的形式发布，其中有两种：32 位 x86 和 64 位 x64 版本。旧电脑可能支持 32 位版本，而大多数电脑支持 64 位版本。检查你的电脑硬件规格以确定。64 位版本运行速度更快，大多数计算机软件现在都有 64 位包可用。表 1-2 列出了你可以从那里下载各种版本镜像的网站。

`http://releases.ubuntu.com` 和 `www.cdimage.ubuntu.com` 还持有它们提供的版本的 BitTorrent 和 Jigdo 下载文件。

> 注意 Ubuntu 还提供了不同类型的硬盘安装。这些包括用于仅安装服务器的服务器磁盘，以及用于安装期间支持特定类型文件系统和功能的备用磁盘（如 `RAID` 和 `LVM` 文件系统）。

| URL | 网站 |
| :--- | :--- |
| `www.ubuntu.com/getubuntu` | 桌面和服务器的主要下载站点。 |
| `http://releases.ubuntu.com/8.04 www.cdimage.ubuntu.com` | 备用、服务器、桌面 CD 和安装 DVD 下载站点，以及 BitTorrent 文件。 |
| `http://release.ubuntu.com` | 包括 Kubuntu 和 Edubuntu 在内的 Ubuntu 版本下载站点。也查看它们各自的网站。 |
| `www.cdimage.ubuntu.com` | 包括 Xubuntu、Mythubuntu、Gubuntu 和 Ubuntu Studio 在内的所有 Ubuntu 版本下载站点。也查看它们各自的网站。包括 Kubuntu、Ubuntu 和 Edubuntu。 |
| `https://launchpad.net` | Ubuntu 镜像。 |
| `http://torrent.ubuntu.com` | 用于下载 Ubuntu 发行版 ISO 镜像的 BitTorrent 站点。 |

表 1-2 Ubuntu CD ISO 镜像位置

## Ubuntu 8.04 LTR

Ubuntu 8.04 包含以下特性：

- 针对用户的 `PolicyKit` 授权，允许对管理工具以及存储和媒体设备进行受限的控制管理访问。
- Brasero GNOME CD/DVD 刻录机。
- 内核包含基于内核的虚拟机 `KVM` 支持。`KVM` 使用硬件虚拟处理器（如 Intel 虚拟化技术 `VT` 和 AMD 安全虚拟机 `SVM` 处理器）来支持硬件级的虚拟机操作系统。大多数标准的 Intel 和 AMD 处理器都提供此支持。
- 使用虚拟机（Virtual Machine）管理和安装 `KVM` 和 `Xen` 虚拟机。
- `java-gci-compat` 集合提供了 Java 运行时环境兼容性。它由 GNU Java 运行时 `libc`、`Eclipse Java` 编译器 `ec` 以及一组封装器和链接 `java-gci-compat` 组成。
- 新应用程序，如 Transmission Torrent 客户端、`Vinagre` 虚拟网络客户端以及世界时钟插件。
- 能够自动检测可移动设备，如 USB 打印机、相机和读卡器。CD/DVD 磁盘被视为可移动设备，并在插入时自动显示。
- 使用 GNOME 虚拟文件系统 `gvs`（取代了 `gnomefs`）访问网络主机上的所有可移动设备和共享目录，包括 Windows 文件夹。
- 计算机上的任何 NTFS Windows 文件系统都会自动检测并使用 `nfs-3` 进行挂载。挂载的文件系统位于 `media` 目录。
- 完整的 `IPv6` 网络协议支持，包括自动寻址和编号。
- 网络监控器会自动检测网络连接。
- 通过来自 `www.freedesktop.org` 的硬件抽象层 `HAL` 向应用程序提供热插设备的信息。这使得 GNOME 等桌面能够显示和管理可移动设备。
- 所有设备在逻辑上被视为可移动设备并由 `udev` 自动配置。设备无法移除。此特性使 Linux 能够适应各种设备，如数码相机、`PDA` 和手机。`PCMCIA` 和网络设备由 `udev` 直接管理。
