
在 Linux 中，文件被组织在目录中，就像在 Windows 中一样。文件系统是一个大型互联目录集，每个目录都包含文件。标准目录是准备好可用的。你可以为自己创建目录，也可以将文件从一个目录移动到另一个。你甚至可以移动整个目录并对目录和文件设置权限，允许他人访问或限制他们访问自己。每个用户拥有的目录实际上与其他用户的目录连接。目录被组织成层次结构，从初始根目录开始。所有其他目录都完全派生自此根目录。

通过 K 桌面环境 `KDE` 和 GNU 对象模型环境 `GNOME`，Linux 现在拥有完全的 GUI 界面。你可以从任一界面执行所有操作。`KDE` 和 `GNOME` 功能完备，支持拖放操作，允许你将图标拖到桌面，并在应用程序面板上设置自己的菜单。它们都依赖于底层的窗口系统，这意味着只要它们安装在你的系统中，来自其中一个的应用程序就可以另一个桌面上运行。`GNOME` 和 `KDE` 网站对于文档、新闻以及你可以为这些桌面下载的软件非常有帮助。两个桌面都可以运行任何 X Window 系统程序，以及任何基于光标的程序如 `Emacs` `Vi`，这些程序被设计在 shell 环境中运行。同时，许多应用程序是专为 Linux 编写并包含在你的发行版中的。K 桌面有一套完整的互联网工具，以及编辑器、图形、多媒体和系统应用程序。`GNOME` 的应用程序稍少，但目前有许多正在开发中。访问 `www.gnome.org` 和 `www.kde.org` 网站查看最新进展。随着新版本的发布，它们将包含新软件。

# 第一部分：入门

## 开源软件

Linux 是作为互联网上的一次协作开源努力开发的，因此没有公司或机构控制 Linux。为 Linux 开发的软件反映了这一背景。开发通常在 Linux 用户决定合作进行某个项目时发生。软件发布在互联网站点上，任何用户都可以访问源码并下载软件。Linux 软件开发始终在互联网环境中运行，并具有全球范围内，招募来自各地的程序员。你启动一个基于 Linux 的项目唯一需要的是——

大多数 Linux 是作为开源软件开发的。这意味着应用程序的源代码随程序自由分发。互联网上的程序员可以对软件包的开发做出贡献，修改并纠正源代码。Linux 是一个开源操作系统。它的源代码包含了所有细节，并可以在互联网上免费获取。许多主要的软件开发工作也是开源项目，例如 `KDE` 和 `GNOME` 桌面及其大部分应用程序，其源代码免费可用。`Netscape Communicator` 浏览器包也已开源。由 Sun 支持的 `OpenOffice` 套件是一个基于 StarOffice 办公的开源项目（StarOffice 本质上是 Sun 的 OpenOffice 商业版本）。许多在 Linux 上运行的开源应用程序已将其网站设在 `SourceForge` (`sourceforge.org`)，这是一个专门为支持开源项目设计的托管平台。你可以在 `www.opensource.org` 找到更多关于开源运动的信息。

开源受公共许可证保护。这些许可证防止商业公司通过添加少量的自己的修改、对更改申请版权并将软件作为它们自己的产品出售来控制开源。最流行的公共许可证是由自由软件基金提供的 GNU 通用公共许可证 `GPL`。这是 Linux 发行时使用的许可证。通用公共许可证保留了版权，免费许可软件，并有权将对其所做的任何修改免费可用。还创建了其他公共许可证以支持不同类型开源项目的需求。GNU 语言许可公共许可证 `LGPL` 使得商业用途可以使用开源库，而不需要要求整个应用程序开源。

## 18 第 I 部分：入门指南

| URL | 互联网站点 |
|---|---|
| fedoraproject.org/wiki/Distribution/Download | 最新版 Fedora 版本的下载页面 |
| fedoraproject.org/Download/mirrors.html | Fedora 镜像列表页 |
| download.fedora.redhat.com/pub/fedora/linux/ | Fedora 软件的 Yum 仓库 |
| download.fedora.redhat.com/pub/fedora/linux/updates | Fedora 更新的 Yum 仓库 |
| linux.duke.org/projects/yum | 修改版 Yellow Dog Updater `Yum` 更新工具，包含更新 Fedora Linux 的 Yum 仓库列表 |
| moin.connectiva.com.br/AptRPM | 用于启用 APT 的 RPM 包的 Red Hat 仓库（第 4 章） |
| rpm.livna.org/fedora | 由于许可和其他限制，发行版未包含的 Fedora 应用。这是 Fedora 项目的官方扩展 |
| www.freshrpms.net | Linux 多媒体应用和软件库；专门列出 Fedora 版本的 RPM 包 |
| sources.redhat.com | Red Hat 托管的开源软件 |
| torrent.fedoraproject.org | Fedora BitTorrent 站点，用于通过 Torrent 下载 Fedora发行版 ISO 镜像 |

表 1-2 软件仓库

启用或禁用支持。请谨慎使用此选项。它应该可以工作，但不保证。此外还有来自 Livna 和 freshrpms 的第三方 NTFS 支持包。它们互不兼容，请二选一使用。

由于由于许可限制，Fedora 不包含对 MP3、DVD 和 DivX 等常用操作的多媒体支持。Fedora 项目关联站点 `rpm.livna.org/fedora` 为这些功能提供了支持。你可以从 fluent.com 下载受许可保护的 MP3 gstreamer。如果你在所有站点都未找到某款软件，可以在 `freshrpms.net` 找到。Fedora 不提供与官方 Nvidia 或 ATI 相关的 Linux 驱动程序支持。相关支持可以在 `rpm.livna.org/fedora` 找到（见第 4 章）。Fedora 包含了通用 XOrg Nvidia 和 ATI 驱动，这将使你的显卡工作。

> 提示：软件管理工具 `Program Manager` 和 `PUP` 将列出所有已配置 Yum 仓库中的软件。初始包含 Fedora、update 和开发部分。如果你需要 `rpm.livna.org` 或 `freshrpms.net` 的配置，它们的软件也将由 `Program Manager` 和 `PUP` 列出并管理。

### 第三方 Linux 软件仓库

尽管大多数应用都包含在 Fedora 仓库中，但你也可以从第三方仓库下载并安装软件。请先检查所需的软件是否已经在 Fedora 仓库中。打开“添加/删除软件”。

# 第 1 章：Red Hat Fedora Linux 19 简介

从应用程序菜单点击搜索菜单，然后使用模式搜索软件。如果无法找到，则可以从第三方仓库下载。某些仓库支持 `Yum`，例如 Livna、`freshrpms` 和 `jpackage`。它们的站点拥有符合 Fedora 标准的 Yum 配置文件，你可以下载并将其作为 RPM 包安装。然后，你可以使用软件管理器或 `yum` 命令直接从第三方仓库选择、下载并安装。

多个第三方仓库可以让你轻松定位应用并找到相关信息。特定的站点包括 `sourceforge.net`、`w.gnu.org`、`rpmfind.net`、`freshrpms.net`、`w.gnomefiles.org` 和 `w.kde-apps.org`。下表列出了 Linux 软件的不同集合。Linux 软件的仓库和存档列于表 1-3，包含针对商业和游戏软件的专门站点。在下载软件包时，请务必检查版本是否针对你的特定发行版封装的。`rpmfind.net`、`freshmeat.net` 和 `sourceforge.net` 也是寻找 RPM 包的好去处。

## Linux 办公和数据库软件

Linux 可许多专业级数据库和办公套件。这些包括 Oracle 和 IBM 数据库，以及 `OpenOffice` 和 `KOffice` 套件。表 1-4 列出了办公套件和数据库的列表。大多数办公套件以及 `Mysql` 和 `Postgresql` 已经包含在 Fedora 仓库中，并可能是 Fedora spin 的一部分。其他许多站点提供了 Linux 免费版本，有些甚至是完全免费的。你可以直接下载并在你的 Linux 系统上安装软件。

## 互联网服务器

与所有 Unix 系统一样，Linux 最重要的特性之一是其系列互联网客户端和服务器。互联网是在 Unix 系统上设计和开发的，并且

| URL | 互联网站点 |
|---|---|
| sourceforge.net | SourceForge，Linux 应用和软件的开源软件开发站点及仓库 |
| rpm.livna.org | 专注于驱动程序的 Fedora 符合 Yum 的仓库 |
| www.freshrpms.net | 专注于 Linux 多媒体应用和软件库的 Fedora 符合 Yum 的仓库 |
| jpackage.org | 用于 Java 应用和工具的 Fedora 符合 Yum 的仓库 |
