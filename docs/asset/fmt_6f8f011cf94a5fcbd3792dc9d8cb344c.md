
程序构建和安装后，你可能需要进行额外的配置。你应该查阅随软件提供的 `man` 手册页或 HOWTO 文档，以了解如何继续。

> **提示：** 对于包含 RPM spec 文件的某些 `tar.gz` 文件，你可以运行 `rpm -ta file.tar.gz`，`rpm` 命令将从该 tarball 构建一个 RPM。

为了尝试此程序，我下载了 whichman 包，该包包含允许你通过输入关键字查找手册页的工具。我下载的文件 `whichman-2.2.tar.gz` 被放置在我创建的名为 `/usr/src/which` 的目录中。然后我运行了 `gunzip` 和 `tar` 命令，分别使用 `whichman-2.2.tar.gz` 和 `whichman-2.2.tar` 作为参数。

我更改到新目录，`cd /usr/src/which/whichman-2.2`。然后我列出了其内容。README 文件包含有关包内容以及安装方法的信息。按照 README 文件的建议，我输入了 `make`，然后是 `make install`。`whichman`、`fwhich` 和 `ff` 命令被安装在 `/usr/bin` 中。（此时，你可以查看每个组件的 `man` 页，看看它做什么。）

我在 README 文件中最后发现的是需要进行一些配置。我在我的 `$HOME/.bashrc` 中添加了 `MANPATH` 变量，以标识要在 `whichman` 工具中搜索的计算机上的 `man` 页位置。我添加的行如下所示：

```bash
export MANPATH=/usr/share/man:/usr/man/man1:/usr/X11R6/man:/usr/share/doc/samba-2.2.3a/docs
```

如果你想知道，`whichman`、`fwhich` 和 `ff` 是你可以用来搜索 `man` 页的命令。它们分别可用于查找 `man` 页的多个位置、与你输入的名称相近的 `man` 页，或位于目录结构某一点下方的 `man` 页。

## 使用 Fedora 或 RHEL 运行应用程序

虽然操作系统很好（也是必需的），但人们使用台式计算机来运行应用程序。有一种普遍的看法认为，尽管 Fedora 或 RHEL 可以作为服务器很好地工作，但它们尚未准备好挑战微软在桌面领域的主导地位。我认为，如果你致力于这样做，Fedora 和 RHEL 可以在桌面上取代 Microsoft Windows，原因有以下几点：

- 现在每个类别的桌面应用程序都有可以在 Linux 上运行的开源产品。因此，*例如*，虽然 Adobe Photoshop 不能在 Linux 中原生运行，但你可以使用 GIMP 或其他应用程序在 Linux 中处理数字图像。

- 你必须拥有的 Windows 应用程序通常可以使用 Windows 模拟器或兼容性程序（如 QEMU 和...

### WINE

人们已做出特殊努力，使 Windows 游戏（Transgaming.com）和办公生产力应用程序（Codeweavers.com）能够在 Linux 上运行。

- 随着病毒和蠕虫在微软系统中肆虐，许多人现在认为 Linux 系统提供了更安全的替代方案，特别是当桌面系统主要用于网络浏览和电子邮件时。通过 Linux，部署数十或数百台桌面系统的公司可以对员工系统的功能和安全性进行大量控制。

从长远来看，随着 Linux 系统成为病毒和恶意软件更有利可图的目标，学习在软件选择、使用文件所有权/权限以及监控系统资源方面的良好实践将变得更加重要。然而，此类工具（包括 clamav 和 clamscan 等病毒扫描器）对于选择包含它们的任何 Linux 系统而言已经可用。（欲了解更多信息，请参阅 www.clamav.net 和 http://klamav.sourceforge.net。）

- 一个庞大的开发社区正在开发开源应用程序，以满足 Linux 社区的需求。如果您觉得有公司支持您的关键任务应用程序会更安心，那么针对 Red Hat 系统有一些强大的商业软件供应可供使用（参见 www.redhat.com/apps/isc_catalog）。

归根结底，大多数人要完全摒弃他们的 Microsoft Windows 操作系统需要付出一些努力。但是，如果您致力于将 Fedora 作为您唯一的应用程序平台，有几种方法可以简化这种过渡。仿真程序可以让您运行许多为其他操作系统创建的程序。转换程序可以帮助您将图形和文字处理数据文件从其他格式转换为 Linux 应用程序支持的格式。

> 交叉引用：有关导入和导出文字处理及图形文件的信息，请参阅第 6 章。

如果您在个人电脑上运行 Linux，很有可能您已经为 Microsoft Windows 95、98、ME、XP、NT、2000 或 Vista 操作系统付过费。您可以在与 Windows 不同的个人电脑上运行 Linux，或者在同一台个人电脑的硬盘上不同的分区中分别安装 Windows 和 Linux。后者要求您每次想要切换操作系统时都重启电脑。（有关设置 Linux/Windows 双启动系统的信息，请参阅第 2 章。）最近，增加了一种第三种选择，即您可以在 Linux 桌面上运行虚拟 Windows 系统（参见本章后面关于 Xen 和 KVM 的描述）。

下一节描述了在 Fedora 中运行的应用程序，您可以使用这些应用程序来替代您习惯使用的 Windows 应用程序。

### 在 Linux 中寻找常见的桌面应用程序

如果您打算将 Linux 用作桌面计算机系统，您必须能够编写文档、处理图形和计算数字。您可能还有其他喜欢的应用程序，例如音乐播放器、网络浏览器和电子邮件阅读器。

> 注意：使用 WINE 技术，CodeWeavers, Inc. 的人提供了一款 CrossOver Office 产品，它允许您在 Linux 中安装和运行 Microsoft Office。请参见本章后面关于“使用 WINE 运行 Windows 应用程序”的部分。

为了给您一个关于可用桌面应用程序的快照，表 5-3 列出了流行的 Windows 应用程序、等效的 Linux 应用程序以及您可以找到这些 Linux 应用程序的位置。虽然这些应用程序中的许多尚未达到其 Windows 对应物的复杂程度，但它们可以是具有成本效益的替代方案。

#### 表 5-3：与 Windows 等效的 Linux 应用程序

| Windows 应用程序 | Linux 应用程序 | 获取 Linux 应用程序的位置 | 费用 |
| :--- | :--- | :--- | :--- |
| Microsoft Office（办公生产力套件） | OpenOffice.org (openoffice.org) | 包含在 Fedora DVD 上 | 免费 |
| | Koffice | 包含在 Fedora DVD 上 | 免费 |
| | StarOffice | www.sun.com/staroffice | $69.95 |
| Microsoft Word（文字处理器） | OpenOffice.org Writer | 包含在 Fedora DVD 上 | 免费 |
| | AbiWord | 包含在 Fedora DVD 上 | 免费 |
| | kword | 包含在 Fedora DVD 上 | 免费 |
| Microsoft Excel（电子表格） | OpenOffice.org Calc | 包含在 Fedora DVD 上 | 免费 |
| | gnumeric | 包含在 Fedora DVD 上 | 免费 |
| | kspread | 包含在 Fedora DVD 上 | 免费 |
| Microsoft PowerPoint（演示文稿） | OpenOffice.org Impress | 包含在 Fedora DVD 上 | 免费 |
| | kpresenter | 包含在 Fedora DVD 上 | 免费 |
| Microsoft Internet Explorer（网络浏览器） | firefox | 包含在 Fedora DVD 上 | 免费 |
| | seamonkey | 包含在 Fedora DVD 上 | 免费 |
| | epiphany | 包含在 Fedora DVD 上 | 免费 |
| | konqueror | 包含在 Fedora DVD 上 | 免费 |
| | opera | www.opera.com | 免费下载 |
| Microsoft Outlook（电子邮件阅读器） | evolution | 包含在 Fedora DVD 上 | 免费 |
| | kmail | 包含在 Fedora DVD 上 | 免费 |
| | thunderbird | 包含在 Fedora DVD 上 | 免费 |
| | Seamonkey Mail | 包含在 Fedora DVD 上 | 免费 |
| Adobe Photoshop（图像编辑器） | The Gimp (gimp) | 包含在 Fedora DVD 上 | 免费 |
