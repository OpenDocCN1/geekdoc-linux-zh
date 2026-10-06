
# 第 1 章：Ubuntu简介

Linux 发行版可在许多站点获取。Ubuntu 在 `www.ubuntu.com/get` 维护其站点，这是 Ubuntu 的站点。

作为一个操作系统，Linux 执行与 Windows 相同的功能。

Ubuntu 目前是最受欢迎的端用户 Linux 发行版之一（`www.ubuntu.com`）。它由 Ubuntu 基金会管理，基金会由 Canonical, Ltd.（`www.canonical.com`）赞助，Canonical 是一家支持和推广开源项目的商业机构。Ubuntu 项目由南非的基于 Debian 的开发者 Mark Shuttleworth 发起。Ubuntu 基于 Debian Linux，它是最老的 Linux 发行版之一，致力于整合尖端开发和功能（`www.debian.org`）。Debian Linux 是一个开源操作系统，依赖于全球范围内志愿者的协作。

Ubuntu 提供了一个稳定、可靠且易于使用的发行版。它被设计成一种每个人都可以轻松使用的 Linux 操作系统。Ubuntu 的名字意思是“对他人的仁爱”。正如 Ubuntu 项目描述的，“Ubuntu 是一个非洲词，意思是‘对他人的仁爱’，或‘因为有大家，才有我我’。”Ubuntu 发行版将 Ubuntu 精神带到了软件世界。

Ubuntu 官方哲学列出了以下原则：

- 每一个计算机用户都应该有自由为了任何目的下载、运行、复制、分发、学习、共享、更改和改进他们的软件，无需支付许可费用。
- 每一个计算机用户都应该能够以他们选择的语言使用软件。
- 每一个计算机用户都应该获得使用软件的所有机会，包括受任何类型残障影响的用户。

对语言的强调反映了 Ubuntu 的国际范围。它旨在成为一个全球发行版，不关注任何单一市场。语言支持已通过国际化项目集成到整个 Linux 中，用术语 i18n 表示。你可以在 `www.li18n.net`（Linux 基金会）和 `www.open18n.org` 等站点找到关于 i18n 的信息。

为所有用户提供软件涉及对残障用户的全方位支持，以及通过在线存储库进行软件访问的无缝集成，点击按钮即可为所有用户提供大量的软件。Ubuntu 还充分利用了自动检测领域的最新进展，极大地简化了安装以及对可移动设备和附加存储的访问。

# 第一部分：快速入门

Ubuntu 旨在提供一个完全支持、可靠、开源、免费且易于修改的 Linux 操作系统。Ubuntu 对其发行版做出以下承诺：

- Ubuntu 将始终免费，包括企业版发布和安全更新。
- Ubuntu 拥有 Canonical 以及全球数百家公司提供的全面商业支持。
- Ubuntu 包含了免费软件社区所能最好的翻译和可访问性基础设施。
- Ubuntu CD 仅包含免费软件应用程序；鼓励您使用免费和开源软件，改进它们并将其传递。

## Ubuntu 版本

Ubuntu 同时提供长期支持和短期发布版。长期支持 (LTS) 发布版（如 Ubuntu 8.04）每两年发布一次。短期发布版在 LTS 版本之后每六个月提供一次。它们的设计旨在为最新的硬件提供最新的应用程序和支持。每个版本都有自己的昵号，例如 8.04 LTS 版本的 *Hardy Heron*。长期发布版的桌面版支持三年，服务器支持五年，而短期发布版支持 18 个月。Canonical 还为购买其服务的公司提供有限的商业支持。

安装 Ubuntu 已显著简化。安装一组核心应用程序，您可以根据意愿添加它们。安装后，可以从在线存储库下载额外软件。安装界面层出不穷，允许用户快速通过默认分区、设置和时间设置。显卡和网络连接等硬件现在会自动进行配置和检测。

# 第一部分：入门

该环境是全球范围内的，汇聚了世界各地的程序员。启动一个基于 Linux 的软件项目唯一需要一个网站。

大多数 Linux 软件都是作为开源软件开发的，应用程序的源代码在互联网上免费分发。用户可以对软件包的开发做出自己的贡献，修改并纠正源代码，这些代码包含在所有的发行版本中，并可以在互联网上免费获取。许多主要的软件开发工作都是开源项目，例如 Sun 支持的 KDE 和 GNOME 桌面。OpenOffice 办公套件基于 StarOffice 办公套件（Sun 的 OpenOffice 商业版）构建的开源项目。你可以在 `www.opensource.org` 找到更多关于开源倡议的信息。

开源软件受公共许可证的保护，这些许可证防止商业需求通过添加自己的修改、对这些更改拥有版权以及将软件设定为自己的产品来控制该软件。最流行的公共许可证是 GPL，Linux 正根据该协议分发的，它由自由软件基金（Free Software Foundation）提供。GNU 保留版权，并免费许可软件，要求是软件及其对其进行的任何修改必须始终免费可用。还创建了其他公共许可证以支持不同类型开源项目的需求。GNU 宽松通用公共许可证（LGPL）允许开源开发者使用 GNU 许可的库。Qt 公共许可证（QPL）允许商业应用程序使用对 KDE 桌面至关重要的 Qt 库。你可以在 `www.opensource.org` 找到完整列表。

Linux 目前受自由软件基金提供的 GNU 公共许可证版权保护，它通常被称为 GNU 软件（见 `www.gnu.org`）。GNU 软件是分发的，并免费分发给他人。GNU 软件已被证明是既可靠又有效的。许多流行的 Linux 工具（如 C 编译器、shell 和编辑器）都是 GNU 应用程序。与你的 Linux 发行版一起安装的 GNU C++ 和 Lisp 编译器、Vi 和 Emacs 编辑器、BASH 和 TCSH 壳，以及 Tex 和 Ghostscript 文档编辑器。此外，许多开源软件项目都根据 GPL 许可。这些应用程序大部分可以在 Ubuntu 软件仓库中找到。第 6 章和第 7 章描述了从互联网网站下载软件并将其安装到系统中的过程。

根据 GPL 条，原作者保留版权，尽管任何人都可以修改并重新分发软件，前提是源代码被包含、公开并免费提供。此外，对于销售软件或免费赠送软件没有限制。一个分发者可以对软件收费，而另一个可以免费提供。大型软件公司也为它们最流行的应用程序提供 Linux 版本。Oracle 提供了其 Oracle 数据库的 Linux 版本。（目前似乎还没有 Microsoft 应用程序的计划，但你可以使用 Wine 这个 Windows 兼容层直接在 Linux 上运行许多 Microsoft 应用程序。）

## Ubuntu 版本

Ubuntu 以多个版本的形式发布，每个版本都为不同的用户群或功能设计（见表 1-1）。不同版本安装不同的软件集合，如 KDE、XF 桌面、服务器、教育软件和多媒体应用程序。ISO 镜像可以直接可以直接下载，也可以使用 Torrent 应用程序下载。

### 第 1 章：Ubuntu 简介 7

| Ubuntu 版本 | 说明 |
|---|---|
| 桌面安装 | 使用 GNOME 桌面的 LiveCD，`www.ubuntu.com/getubuntu`。 |
| 服务器安装 | 安装服务器软件（不含桌面），`www.ubuntu.com/getubuntu`。 |
| 备用安装 | 安装增强功能，`www.releases.ubuntu.com`。 |
| Kubuntu | 使用 KDE 代替 GNOME 的 LiveCD，`www.ubuntu.org`。 |
| Xubuntu | 使用 Xfce 桌面代替 GNOME，`www.ubuntu.org`。适用于笔记本电脑。 |
| Edubuntu | 安装教育软件：桌面、服务器和服务器附加 CD，`www.ubuntu.com`。 |
| Goubuntu | 仅使用开源软件；无法访问任何种受限软件，`www.ubuntu.com`。 |
| Ubuntu Studio | 带有多媒体和图形应用程序的 Ubuntu 桌面，`www.ubuntustudio.org`。 |
| Mythbuntu | 带有 MyTV 多媒体和数字视频录制机 (DVR) 应用程序的 Ubuntu 桌面，`www.mythubuntu.org`。 |

**表 1-1** Ubuntu 版本

Ubuntu Desktop 为终端用户提供标准功能。标准的 Ubuntu 版本提供了一个使用 GNOME 桌面的 LiveCD。大多数用户会安装这个版本。这是你从 `www.ubuntu.com/getubuntu/download` 的 Get Ubuntu 下载页面下载的 CD 镜像。

想要将 Ubuntu 作为服务器提供如网站等互联网服务的用户将使用 Ubuntu 服务器版。服务器版仅提供简单的命令行界面；它不安装桌面。它是专门为运行服务器而设计的。请记住，你可以先安装桌面，以后从 Ubuntu 仓库下载服务器软件，在带有桌面的系统中运行它们。你不需要为了安装和运行服务器而安装服务器版。服务器版可以从 Get Ubuntu 下载页面下载。

想要 RAID 或文件系统加密等增强操作系统功能的用户可以使用备用版本。备用版本与桌面版和服务器版一起，可以直接从 `http://releases.ubuntu.com/hardy` 或 `http://releases.ubuntu.com/0.04` 下载。

其他版本使用不同的桌面或针对某些用户群的特殊软件集合。版本的链接列在 `www.ubuntu.com` 页面上。从那里你可以下载它们的免费/安装 CD。Kubuntu 版本使用 KDE 代替 GNOME。这是一个精简且高效的桌面，非常适合笔记本电脑和较小电脑的低功耗使用。Edubuntu 提供教育软件，还可以与专用服务器配合使用，为学校网络提供教育软件。Goubuntu 是标准版本的修改版，仅包含开源软件，无法访问受限软件，包括来自 Nvidia 或 ATI 的受限驱动程序。Ubuntu Studio 版本是一个新版本，提供了多媒体和视频制作软件。Mythbuntu 设计用于作为多媒体和视频播放系统安装 Ubuntu。Kubuntu 和 Edubuntu 版本均可用。

请注意，所有这些版本都以 LiveCD 或 DVD 安装的形式发布，其中有两个：32 位 x86 和 64 位 x86。旧旧电脑可能只支持 32 位版本，而大多数现代电脑支持 64 位。检查你的硬件规格以确保。64 位版本运行速度更快，大多数计算机软件现在都有稳定的 64 位包。表 1-2 列出了你可以从那里下载各种版本镜像的站点。

`http://releases.ubuntu.com` 和 `www.cdimage.ubuntu.com` 还持有提供的版本的 BitTorrent 和 Jigdo 下载文件。

Ubuntu 还提供了针对硬盘不同安装类型的发行。其他包括用于安装所有服务器的服务器盘，以及在安装期间支持特定文件系统和功能（如 RAID 和 LVM 文件系统）的备用盘。

| URL | 网站 |
|---|---|
| `www.ubuntu.com/getubuntu/download` | 桌面和服务器的主要下载站点。 |
