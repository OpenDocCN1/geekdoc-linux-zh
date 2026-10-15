
在文件管理器窗口的地址框中输入 FTP URL 以访问该站点。移动到存放 Gnome 文件的目录。然后选择文件并将其拖到另一个打开了目标本地目录的文件管理器窗口中。文件将会自动为你下载。使用 `ftp` 客户端进行下载时，请务必使用 `prompt` 命令关闭提示，并使用 `get` 一次下载所有文件。

一旦下载了 RPM 包，你可以使用带有 `-Uvh` 选项的 `rpm` 命令来安装它们，或者使用 GnomeRPM 工具。请先阅读安装说明。这些说明可以在 `readme` 或 `install` 文件中找到。你可能需要在安装某些包之前安装其他包。GnomeRPM 工具会告诉你软件包是否需要先安装其他包。它会将这些其他包列为依赖项，这意味着你想要安装的包依赖于这些包，并且需要先安装这些其他包。

要手动安装特定的 Gnome RPM 包，请使用带有 `-Uvh` 选项的 `rpm` 命令或类似 GnomeRPM 的 RPM 包工具（第 31 章）。此示例安装了游戏：

```
rpm -Uvh gnome-games-1.2.4-6.i386
```

许多最新的更新以源文件的形式提供，你可以下载并编译它们。这些通常是带有 `.tar.gz` 扩展名的压缩归档包。检查 `ftp.gnome.org`，这些文件目前位于 `pub/Gnome/stable/sources`。查看 Gnome 网站的公告。例如，Gnome 的新版本可能是：

```
ftp.gnome.org/pub/GNOME/stable/sources/gnome-core/gnome-core-1.4.0.tar.gz
```

一旦下载了归包，使用带有 `xzvf` 选项的 `tar` 命令进行解压和提取。在生成的目录中，使用 `./configure`、`make` 和 `make install` 命令对程序进行配置、编译和安装。

```
tar xzvf gnome-core-1.4.0.4.tar.gz
```

## 第 9 章：K 桌面环境：KDE

### 概述

K 桌面环境（KDE）是一个网络透明的桌面，包含了标准的桌面功能（如窗口管理器和文件管理器）以及涵盖大多数 Linux 任务的广泛应用程序集。KDE 是一个感知网络的系统，包含全套集成的网络/Internet 应用，包括邮件发送程序、新闻阅读器和浏览器。文件管理器兼具 Web 和 FTP 客户端，允许你直接从桌面访问 站点。KDE 旨在提供 MAC/OS 和 Windows 系统的桌面功能和易用性，同时结合 Unix 操作系统的强大功能和灵活性。

注意 KDE 2.2 版本已取代了早期的 KDE 1.1 版本。本章描述的是 2.2 版本。它与 1.1 版本有许多相似之处；但熟悉旧版 KDE 的用户会发现一些重要变化，例如新的文件管理器控制中心。

KDE 桌面由 KDE 项目开发发布，该项目是一个由全球数百名程序员组成的大型开放团体。KDE 是根据 GNU 通用许可许可证提供的完全免费开源软件，并免费提供源码。KDE 的开发由一个核心小组管理：KDE 核心团队。任何人都可以申请，但成员身份取决于能力。

KDE 应用程序使用多种支持技术开发。这些包括 `KIO`，它可以跨网络无缝且模块化地访问文件和目录。对于进程间通信，KDE 使用桌面通信协议（`DCOP`）。`Parts` 是 KDE 的组件对象模型，用于将一个应用程序嵌入另一个应用程序，例如在文档中嵌入电子表格。XML UI 使用 XML 生成菜单和工具栏等 GUI 对象。`KHTML` 是一个 HTML 4.0 渲染和绘图引擎。

为 KDE 编写的许多应用程序都可以从桌面轻松访问。这些包括编辑器、照片和图像应用、电子表格和办公应用。应用程序的名称通常包含字母 K，例如 `KWord` 或 `Kmail`。KDE 桌面还提供了各种工具，包括计算器、通知、记事本和软件软件包管理器。在系统管理层级，KDE 提供了几个用于配置你系统的工具。通过 `Kuser`，你可以管理用户，添加新用户或删除旧用户。使用几乎所有 Linux 任务的点对点（PPP）协议都可以在 KDE 桌面上执行。KDE 应用程序还内置了帮助应用程序。选择帮助菜单中的项目会启动 KDE 帮助查看器，它提供了一个类似 Web 的界面，带有用于浏览帮助文档的链接。KDE 2.2 版本包含了基于 KDE `KParts` 名为 `Koffice` 的办公应用程序。`Koffice` 包含了演示程序、插图软件、文字处理器以及其他组件（详情请见第 14 章）。此外，还有一个名为 KDE 的交互式开发环境（IDE），用于帮助程序员创建基于 KDE 的软件。

KDE 由 Matthias Ethric 于 1996 年 10 月发起，拥有广泛的赞助商，包括 SuSE、Calder、Red Hat、O'Reilly、DLD、Delix、Live、Linux Verband 等。KDE 设计运行在任何 Unix 实现上，包括 Linux、Solaris、HP-UX 和 FreeBSD。KDE 官方网站为 `www.kde.org`，提供新闻更新、下载链接和文档。KDE 软件软件包可以从 KDE FTP 站点 `ftp.kde.org` 及其镜像站点下载。用户和开发者可以使用 KDE 邮件列表，包括公告、管理等。请查看 KDE Web 以订阅。目前 `apps.kde.com` 提供优秀的 KDE 应用程序。开发支持和文档可以从 `developer.kde.org` 获取。各种 KDE 网站列于表 9-1。

### 表 9-1：KDE 网站

| 网站 | 说明 |
| --- | --- |
| `www.kde.org` | KDE 网站 |
| `ftp.kde.org` | KDE FTP 站点 |
| `apps.kde.com` | KDE 软件仓库 |
| `developer.kde.org` | KDE 开发者站点 |
| `www.trolltech.com` | Qt 库网站 |
| `koffice.kde.org` | KOffice 办公套件 |
| `kde.themes.org` | KDE 桌面主题 |
| `lists.kde.org` | KDE 邮件列表 |

### Qt 与 Harmony

KDE 使用其 GUI 库 `Qt`，该库由 Troll Tech（`www.trolltech.com`）开发并支持。`Qt` 被认为是 Unix/Linux 系统上最好的 GUI 库之一。`Qt` 的优势在于依赖商业化开发和支持的 GUI 库，同时使用 `Qt` 库极大缩短了 KDE 的开发时间。Troll Tech 将 `Qt` 库作为可自由分发的开源软件提供。然而，存在某些限制：基于 `Qt` 的应用程序必须是免费开源的，且不能修改 `Qt` 库。如果你使用 `Qt` 库开发了一个应用程序并想出售它，你必须从 Troll Tech 购买许可证。换句话之，`Qt` 库适用于免费应用程序，但不适用于商业应用程序。

`Harmony` 项目正在开发 `Qt` 库的免费替代方案。`Harmony` 将包含所有的 `Qt` 功能，以及多线程和主题化等额外功能。`Harmony` 将完全兼容任何使用 `Qt` 库开发的 KDE 应用程序。`Harmony` 将根据 GNU 库通用许可许可证（LGPL）提供。更多信息请参见 `www.gnu.org/software/harmony`。

### KDE 桌面

KDE 的目标之一是用户提供一个一致的集成桌面，其中所有应用程序都使用 GUI 界面（图 9-1）。为此，KDE 提供了自己的窗口管理器（`kwm`）、文件管理器（`Konqueror`）、程序管理器和桌面面板（`Kicker`）。你可以在 KDE 中运行任何其他符合 X 窗口系统标准的应用程序（如 Netscape），以及任何 Gnome 应用程序。反之，你可以在任何其他 Linux 窗口管理器（包括 Blackbox、Afterstep 和 Enlightenment）中运行任何 KDE 应用程序。你甚至可以在 Gnome 中运行 KDE 应用程序。

![](img/6cd7e3ee37600d2fcd508ba45f870a38_163_0.png)

图 9-1：KDE 桌面

当你在 Red Hat 上启动 KDE 时，KDE 面板显示在屏幕底部。面板上显示有菜单和程序的图标，以及用于不同桌面界面的按钮。`K Menu` 按钮显示为一个带有齿轮且顶部有一个小箭头的大型 K 字；点击它可以打开一个菜单。这就是应用程序启动器（Application Starter）。点击此按钮可显示所有你可以运行的应用程序列表。可以通过此菜单访问 K Menu 操作。你可以找到 Internet、Systems（系统）、Multimedia 和 Utilities（工具）等不同类别的条目。这些子菜单列出了你可以使用的 KDE 应用程序。例如，要启动 KDE，请在 Internet 中选择 Main Client（主客户端）。要退出，可以在桌面上点击右键并从弹出菜单中选择注销（Logout）。你也可以点击 KDE 面板上锁定图标下方的图标。如果你在退出时离开了 KDE 或 X11 应用程序或窗口，它们在重新启动时会自动恢复。如果你只想锁定桌面，可以点击锁定图标，屏幕保护程序就会出现。要访问桌面，点击屏幕并提示输入登录密码。输入密码后，桌面就会出现。
