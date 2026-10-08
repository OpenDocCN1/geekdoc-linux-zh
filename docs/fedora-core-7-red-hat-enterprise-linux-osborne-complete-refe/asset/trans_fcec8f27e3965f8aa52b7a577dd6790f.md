
以及 TeX 和 Ghostscript 文档格式化程序。此外，还有许多开源软件项目采用 GNU 通用公共许可证（GPL）授权。这些软件应用程序中的许多都可以在不同的互联网站点上获取，这些站点列在表 1-4 中。第 4 章和第 29 章详细描述了从互联网站点下载软件应用程序并将其安装到系统上的过程。

根据 GNU 通用公共许可证的条款，原始作者保留版权，尽管任何人都可以修改软件并重新分发它，但前提是必须包含源代码、使其公开，并且免费提供。此外，对销售软件或免费赠送软件没有任何限制。一家经销商可能对软件收费，而另一家则可能免费提供。主要软件公司也正在提供其最流行应用程序的 Linux 版本。Oracle 提供了其 Oracle 数据库的 Linux 版本。（目前似乎没有 Microsoft 应用程序的相关计划。）

## Linux 软件

目前，所有 Linux 软件均可从在线存储库获取。你可以下载用于桌面、互联网服务器、办公套件和编程语言包等的软件应用程序。软件包主要通过启用 Yum 的存储库进行分发，其中最大的是官方 Fedora 存储库。桌面软件管理程序和更新程序会自动处理下载和更新。

此外，你还可以从第三方源下载以压缩归档或 RPM 包形式存在的软件。RPM 包是使用 Red Hat 包管理器归档的包。压缩归档文件的扩展名为 *.tar.gz* 或 *.tar.Z*，而 RPM 包的文件扩展名为 *.rpm*。无论直接从哪个站点下载的任何 RPM 包，都可以使用 GNOME 或 KDE 桌面环境下的 Pirut 包管理器通过点击按钮轻松安装。你也可以下载源代码版本并在系统上直接编译。这已成为一个简单的过程，几乎与安装已编译的 RPM 版本一样简单。

Red Hat 和 Fedora 还拥有大量镜像站点，你可以从中下载当前版本的软件包（fedoraproject.org/Download/mirrors.html）。如果连接主 FTP 站点时遇到问题，请尝试其镜像之一。

## Fedora 软件存储库

对于 Fedora，你可以使用软件更新程序从 Fedora Yum 存储库更新到最新软件（参见第 4 章）。对于 Red Hat Enterprise Linux，你可以使用 Red Hat Network 自动下载系统升级。Red Hat Enterprise 的更新由 Red Hat 直接处理，而 Fedora 的更新则使用 Fedora Yum 软件存储库。你的软件更新程序已配置为访问标准存储库。

Fedora 发行版提供了广泛的软件选择，范围从办公和多媒体应用程序到互联网服务器和管理服务（参见表 1-2）。虽然许多流行应用程序未包含在内，但相关软件站点提供了符合 Fedora 规范的版本。在安装过程中，Yum 被配置为访问 Fedora 存储库。

Fedora 存储库包含对 NTFS 文件系统的支持，该文件系统用于 Windows XP、NT 和 2000 系统。NTFS 支持由 *ntfs-3g* 包实现。你可以使用程序管理器直接安装它。你可以选择启用或禁用写入支持。请谨慎对待此选项。它应该有效，但并无保证。Livna 和 freshrpms 还提供了第三方 NTFS 支持包。它们互不兼容。请使用其中之一。

由于许可证限制，Fedora 发行版不包含针对 MP3、DVD 和 DivX 等常见操作的多媒体支持。Fedora 项目关联站点 rpm.livna.org/fedora 提供了对这些功能的支持。你可以从 www.fluendo.com 下载免费许可的 MP3 gstreamer 插件。你在那些站点找不到的任何软件通常都可以在 freshrpms.net 找到。Fedora 不提供官方 Nvidia 或 ATI 发布的 Linux 图形驱动程序的支持。可以在 rpm.livna.org/fedora 找到这些驱动程序的支持（参见第 4 章）。Fedora 包含通用的 X.org Nvidia 和 ATI 驱动程序，这些驱动程序可使你的显卡正常工作。

> 提示 软件管理工具，Program Manager 和 PUP，将列出所有已配置的 Yum 存储库中的软件。初始时，这些包括 Fedora、更新和开发存储库。如果你添加 rpm.livna.org 或 freshrpms.net 的配置，它们的软件也将被列出，并由 Program Manager 和 PUP 进行管理。

## 第三方 Linux 软件存储库

虽然 Fedora 软件存储库应包含几乎应用程序，但你仍然可以从第三方存储库下载和安装软件。请首先检查你想要使用的软件是否已存在于 Fedora 存储库中。从“应用程序”菜单打开“添加/删除软件”，点击“搜索”菜单，然后使用模式搜索软件。如果不可用，则需要从第三方存储库下载。某些存储库支持 Yum，如 Livna、freshrpms 和 jpackage。它们的网站将提供符合 Fedora 规范的 Yum 配置文件，你可以将其作为 RPM 包下载并安装。然后，你可以使用软件管理器或 **yum** 命令直接从第三方存储库中选择、下载和安装软件。

几个第三方存储库使查找应用程序及其相关信息变得容易。特别值得注意的有 **sourceforge.net**、**www.gnu.org**、**rpmfind.net**、**freshrpms.net**、**www.gnomefiles.org** 和 **www.kde-apps.org**。下表列出了不同的 Linux 软件站点。表 1-3 列出了 Linux 软件的存储库和归档，以及几个专业站点，例如用于商业和游戏软件的站点。在下载软件包时，始终检查版本是否已打包适用于你的特定发行版。例如，**rpmfind.net**、**freshmeat.net** 和 **sourceforge.net** 也是查找 RPM 包的好地方。

## Linux 办公和数据库软件

许多专业级数据库和办公套件现已适用于 Linux。这些包括 Oracle 和 IBM 数据库，以及 OpenOffice 和 KOffice 套件。表 1-4 列出了办公套件和数据库的站点。大多数办公套件以及 Mysql 和 Postgresql 已包含在 Fedora 存储库中，并且可能是你的 Fedora 旋装版的一部分。许多其他站点为 Linux 提供免费个人版本的软件，其他则完全免费。你可以直接下载它们并将软件安装到你的 Linux 系统上。

## 互联网服务器

Linux 以及所有 Unix 系统最重要的功能之一，是其互联网客户端和服务器集合。互联网是在 Unix 系统上设计和开发的，并且

### 表 1-4：互联网站点

| URL | 互联网站点 |
| :--- | :--- |
| [fedoraproject.org/wiki/Distribution/Download](fedoraproject.org/wiki/Distribution/Download) | 最新 Fedora 版本的下载页面 |
| [fedoraproject.org/Download/mirrors.html](fedoraproject.org/Download/mirrors.html) | 列出 Fedora 镜像的页面 |
| [download.fedora.redhat.com/pub/fedora/linux/](download.fedora.redhat.com/pub/fedora/linux/) | 用于 Fedora 软件的 Fedora Yum 存储库 |
| [download.fedora.redhat.com/pub/fedora/linux/updates](download.fedora.redhat.com/pub/fedora/linux/updates) | 用于 Fedora 更新的 Fedora Yum 存储库 |
| [linux.duke.edu/projects/yum](linux.duke.edu/projects/yum) | Yellow Dog Updater, Modified (Yum) 更新工具，列出了用于更新 Fedora Linux 的 Yum 存储库 |
| [moim.connectiva.com.br/AptRpm](moim.connectiva.com.br/AptRpm) | 支持 APT 的 RPM 包的 APT-RPM Red Hat 存储库（参见第 4 章） |
| [rpm.livna.org/fedora](rpm.livna.org/fedora) | 由于许可证和其他限制而未包含在发行版中的 Fedora 应用程序。这是 Fedora 项目的官方扩展。 |
| [www.freshrpms.net](www.freshrpms.net) | Linux 多媒体应用程序和支持库；具体列出了 Fedora 版本的 RPM 包 |
| [sources.redhat.com](sources.redhat.com) | 由 Red Hat 托管的开源软件 |
| [torrent.fedoraproject.org](torrent.fedoraproject.org) | 用于通过 BitTorrent 下载 Fedora 发行版 ISO 镜像的 Fedora BitTorrent 站点 |

### 表 1-3：第三方 Linux 软件归档、存储库和链接

| URL | 互联网站点 |
| :--- | :--- |
| **sourceforge.net** | SourceForge，Linux 应用程序和软件存储库的开源软件开发站点 |
| **rpm.livna.org** | 专注于驱动程序的 Fedora Yum 兼容存储库 |
| **www.freshrpms.net** | 专注于 Linux 多媒体应用程序和支持库的 Fedora Yum 兼容存储库 |
| **jpackage.org** | 用于 Java 应用程序和工具的 Fedora Yum 兼容存储库。 |
| **www.gnomefiles.org** | GNOME 应用程序 |
| **www.kde-apps.org** | KDE 软件存储库 |
| **freshmeat.net** | 新的 Linux 软件 |
| **rpmfind.net** | RPM 包存储库 |
| **www.gnu.org** | GNU 归档 |
| **www.happypenguin.org** | Linux 游戏集 |
| **www.linuxgames.com** | Linux 游戏 |

