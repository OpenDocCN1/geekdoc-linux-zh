
## 表 5-1: Windows 对应的 Linux

| Windows 应用 | Linux 应用 | 如何获取 Linux 应用 | 费用 |
|---|---|---|---|
| Microsoft Office (办公软件套件) | OpenOffice (`openoffice.org`) | 包含在 Red Hat Linux CD 中 | 免费 |
|  | StarOffice | 包含在 Red Hat Linux CD 中 `www.sun.com/staroffice` | 免费 $75.95 |
| Microsoft Word (文字处理器) | AbiWord | 包含在 Red Hat Linux CD 中 | 免费 |
|  | Kword | 包含在 Red Hat Linux CD 中 | 免费 |
| Microsoft Excel (电子表格) | Gnumeric | 包含在 Red Hat Linux CD 中 | 免费 |
|  | Kspad | 包含在 Red Hat Linux CD 中 | 免费 |
| Microsoft Powerpoint (幻灯片) | Kpresenter | 包含在 Red Hat Linux CD 中 | 免费 |
| Microsoft Internet Explorer (网页浏览器) | Mozilla | 包含在 Red Hat Linux CD 中 | 免费 |
|  | Galeon | 包含在 Red Hat Linux CD 中 | 免费 |
|  | Konqueror | 包含在 Red Hat Linux CD 中 | 免费 |
|  | Opera | `www.opera.com` | 免费下载 |
| Microsoft Outlook (邮件阅读器) | Evolution | 包含在 Red Hat Linux CD 中 | 免费 |
|  | Kmail | 包含在 Red Hat Linux CD 中 | 免费 |
| Adobe Photoshop (图像编辑器) | The Gimp | 包含在 Red Hat Linux CD 中 | 免费 |
| Real Player (音频/视频播放器) | RealPlayer (Linux 版本) | `www.rpmfind.net` (搜索 RealPlayer 关键词) | 免费 |
| AutoCAD (计算机辅助设计) | LinuxCad | `www.linuxcad.com` | $89 |

后续章节描述了如何查找和使用专门为 Linux 创建的应用程序。

## 第 5 章：访问和运行应用程序 173

### 获取 Red Hat Linux

遗憾的是，你无法在普通的电脑商店里找到很多 Linux 应用程序。获取 Linux 应用最好的方法是从互联网上下载。你也可以从几个网站订购 CD-ROM 刻盘。

### 调查你的桌面

越来越多的高质量应用程序正随 Red Hat Linux 一起发布，主要作为 GNOME 或 KDE 桌面环境的一部分。换句话说，要开始寻找优秀的办公应用、游戏、多媒体播放器和通信工具，你不需要在桌面主菜单按钮之外寻找。

在开始在互联网上寻找需要的软件之前，先看看是否可以使用已经随 Red Hat Linux 安装的内容。接下来的章节描述了如何使用发布工具、玩游戏、处理多媒体以及在互联网上进行通信——这些程序要么是 Red Hat Linux 自带的，要么是很容易获取的。附录 B 包含了本书附带的 Red Hat Linux 版本的软件包列表。

### 在互联网上查找应用程序

以下是在互联网上寻找 Linux 应用的几个地方：

- **Freshmeat (`www.freshmeat.net`)** —— 该网站维护了一个庞大的 Linux 软件索引。在查找框中输入软件包名称，你就可以找到它在网络上的获取位置。它是检查 Linux 软件的首选网站之一。
- **SourceForge (`www.sourceforge.net`)** —— 该网站托管了数千万个开源软件项目。你可以从 SourceForge 网站下载项目的软件和文档。
- **Linux Applications 网站 (`www.linuxapps.com`)** —— 如果你还不知道正在寻找的应用程序，这里是一个极好的起点。该网站提供了超过 30 类的应用程序。Linux Applications 提供了每个应用程序的描述以及指向应用程序主页的链接。
- **Red Hat 应用索引 (`www.redhat.com/apps/marketplace`)** —— 你可以在此站找到 Red Hat Linux 的商业应用程序。该站提供了联系信息、价格以及每个应用程序的描述。
- **Tucows Linux 网站 (`linux.tucows.com`)** —— Tucows Linux 网站提供免费和商业性的 Linux 软件。该网站还提供有关 Linux 的新闻文章以及该站排名前 100 的软件下载列表。

当你购买商业应用程序时，通常会在 CD 上获得该程序。安装过程通常会被简化，并提供纸质文档。当然，当你下载软件时，你会获得即时的满足——而当你购买它时，必须等待包裹邮寄到达。

> **提示：** 有时软件软件包会同时以 `libc5` 和 `libc6` 格式提供。该标识指的是应用程序使用的 C 语言语言库版本。如果你有选择，请选择 `libc6` 软件包。这些包兼容 Red Hat Linux 7 及更高版本（或任何 Linux 内核 2.2 及更高版本）。事实上，所有主要的 Linux 发行版现在都使用 `libc6`。

如果你已经对想要的软件有了一些了解，可以直接去互联网上许多持有 Red Hat 软件的 FTP 站点。以下是进入 Linux FTP 站点的几种方法：

- **Rpmfind (`www.rpmfind.net`)** —— 该站提供已封装为 Red Hat 包管理 (`RPM`) 格式的开源软件。从该网站进行关键词搜索，从搜索结果中下载相应的 `RPM`。
- **Red Hat 镜像站 (`www.redhat.com/mirrors.html`)** —— 转到此页面获取可下载的 Red Hat 软件的 FTP 站点列表。这些站点大多数还有多种供 Red Hat 使用的免费软件和共享软件。
- **Sunsite (`ftp.metalab.unc.edu`)** —— 北卡罗来纳大学恰皮尔山分校的 Metalab 维护此软件。
- **Free Foundation (`ftp.gnu.org`)** —— Free Foundation 提供了此软件。
- **Linux (`ftp.redhat.com`)** —— Red Hat 提供了许多软件包。

174 Part II：使用 Red Hat Linux

### 下载软件

第 5 章：访问和运行应用程序 175

> **注意：** 以下步骤假设你已连接互联网。

#### 使用 Netscape 下载

你可以使用浏览器（如 Mozilla）或 FTP 程序（如 `ncftp`）从互联网下载软件。浏览器更直观，但 FTP 程序有更多选项。

#### 使用 ncftp 下载

如果你想使用基于文本的方式下载文件（而不是 Netscape），可以使用 Red Hat Linux 的任何 FTP 命令。我喜欢使用的一个 FTP 客户端是 `ncftp` 命令。以下是 `ncftp` 过程的示例：

1. 从 shell 或终端窗口输入 `ncftp location`，其中 `location` 是 FTP 站点的名称。例如：

```
$ ncftp metalab.unc.edu
```

```
or
$ ncftp -u jake ftp.myveryownership.com
```

如果没有用户名（如第一个示例），`ncftp` 将以匿名用户身份登录。

如果有用户名（例如 `jake`），系统会提示输入该 FTP 站对应用户的密码。

2. 当你的登录被接受后，你可以使用这些命令来查找你正在寻找的软件包或文档：

- `ls` — 列出当前目录的内容。
- `cd dir` — 将当前目录更改为子目录 `dir`。如果你愿意，可以使用两个点 (`cd ..`) 返回上一级目录。例如，`cd /pub/Linux/apps/doctools`。

3. 输入 `binary`（以确保文件以二进制文件格式下载）。

4. 要从当前工作目录下载文件，输入 `get 文件应用程序名称`。例如，要下载 `whichman` 应用程序，当前目录是 `/pub/Linux/apps/doctools`，请输入：

```
get wichman-2.0.tar.gz
```

5. 当下载完成后，输入 `exit`。

> 提示：在启动 `ncftp` 命令之前，确保你的当前目录是你想要下载文件的目录。或者，你也可以在 `ncftp` 内部使用 `lcd` 命令更改目录。例如，要切换到 `/tmp/appabb`，输入 `lcd /tmp/appabb`。

### 理解软件包名称和格式

你刚刚从互联网下载了一个巨大的文件，其中包含许多名称、数字、点、gz 和 tars。这些都意味着什么？嗯，将其分解开，其实并不复杂。

大多数包含 Linux 应用程序的归档文件遵循 GNU 风格软件包命名规范。以下示例说明了软件包命名格式：

```
myappapp-4.2.3.i386.rpm
myappapp-4.2.3.tar.gz
myappapp-4.2.3.src.tar.gz
myappapp-4.2.3.bin.SPARC.tar.gz
myappapp-4.2.3.bin.ELF.static.tar.gz
```

这些示例代表同一个软件应用程序的不同软件包。该软件包的名称是 `mycoolapp`。软件包后面跟着一组代表软件包版本的数字。在这种情况下，它是版本 4.2（主版本号为 4，后面是次要版本号和补丁级别 2.3）。版本号之后是一个点，后面是一些可选部分，最后是关于文件如何归档和压缩的指示。

第一行显示了一个 Red Hat 软件包管理器 (`.rpm`) 格式的软件包。`.rpm` 之前的 `.i386` 表示该软件包包含为运行 Intel i386 架构计算机（换句话说，PC）构建的二进制文件。查看侧边栏“RPM 与从源码编译”了解使用预构建 RPM 软件包与自己编译程序的优缺点。

在上述示例的接下来的两行中，每个文件都包含软件包的源代码。组成软件包的文件是使用 `tar` 命令归档的（`.tar`）并使用 `gzip` 命令压缩的（`.gz`）。当你准备好安装应用程序时，使用这两个命令来扩展和解压缩软件包。

在版本号和 `.tar.gz` 后缀之间会有用点隔开的可选标签，它们提供了关于软件包内容的特定信息。特别是，如果软件包是二进制版本，这些信息提供了有关二进制文件将在何运行的细节。在第三行中，添加了可选的 `.src` 标签，是因为开发者想要区分此软件包的源代码和二进制版本。在第四行中，`.bin.SPARC` 表示它是一个二进制软件包，可以在 SPARC 工作站上运行。最后一行表示它是一个二进制软件包，由静态链接的 ELF 可执行文件组成。

### RPM 与从源码编译

使用 RPM 格式创建的二进制文件可以使用 Red Hat 工具轻松安装、管理和卸载。这是 Red Hat Linux 初学者的推荐安装方法。然而，有时从源代码构建应用程序可能更好。以下是双方的观点：

- **RPM** — 从 RPM 归档文件安装应用程序非常简单。应用程序安装后，可以使用 shell 命令和 GUI 来管理、验证、更新和删除 RPM 应用程序。你不需要了解任何关于 Makefile 或编译器的知识。当你安装 RPM 软件包时，RPM 工具甚至会检查该软件包所需的其他软件包是否已安装。Red Hat 发布了 RPM，其他 Linux 发行版也开始发布它们的软件。因此，Linux 应用程序已经或将以 RPM 格式可用。
- **源代码** — 将源代码软件包转换为 RPM 二进制文件有时需要一段时间。如果你使用 RPM，你可能会发现软件是好几个版本之前的了，而你本可以下载源代码并运行几个 `tar` 和 `make` 命令。此外，通过修改源代码，你可能定制应用程序以更好地符合你的需求。当在计算机上编译源代码时，它更有可能被优化以在你的计算机上高效运行。

以下是软件包名称各部分的分解：

- `name` — 这通常是一个标识应用程序的全小写字符串。
- `dash (-)`
- `version` — 显示为从左到右的主版本到次要版本号。
- `dot (.)`
- `src or bin` — 这是可选的，如果没有给出指示，通常默认为 `src`。
- `dot (.)`
- `type of binary` — 这是可选的，可以包含几个不同的标签来描述二进制归档的内容。例如，`i386` 表示旨在用于 Intel 架构（386, 486, Pentium）的二进制文件。
- `dot (.)`
- `archive type` — 通常是 `tar` (`.tar`)
- `compression type` — 通常是 `gzip` (`.gz`)

### 使用不同的归档和文档格式

许多归档格式与特定的发行版相关联（如 Red Hat、Debian，或 Sparc）使用 `tar/gzip` 方法归档。然而，你可能会在 Linux FTP 站点看到具有不同后缀的文件。

> 注意：由于我们使用的是 Red Hat Linux，我们安装的大多数软件都是 RPM 格式。除非你想自己构建软件——RPM 是要寻找的格式。

#### 表 5-2：Linux 归档格式

| 格式 | 后缀 | 描述 |
| :--- | :--- | :--- |
| Gzip 文件 | `.gz` 或 `.z` | 使用 `gzip` 工具压缩的文件。可以使用 `gzip` 或 `gunzip` 工具解压缩（它们是相同的）。 |
| Tar 文件 | `.tar` | 使用 `tar` 命令归档的文件。`tar` 用于将多个文件汇到一个归档文件中。你可以使用 `tar` 的不同选项将归档扩展为单独的文件。 |
| Bzip2 | `.bz2` | 使用 `bzip2` 程序压缩的文件。 |
| Tar/压缩 | `.tar` 或 `.tz` | 使用 `tar` 归档并使用 `compress` 命令压缩。（`compress` 命令不是 GNU 的，因为它有专利。） |
| Linux 软件地图 | `.lsm` | 归档内容的文本。 |
| Debian 二进制软件包 | `.deb` | Debian 发行版使用的二进制软件包。（在本章后面将介绍如何将 Debian 转换为 Red Hat 格式。） |
| Red Hat 软件包管理 | `.rpm` | Red Hat Linux 使用的二进制软件包。该格式也其他 Linux 发行版。 |

#### 表 5-3：Linux 文档格式

| 格式 | 后缀 | 描述 |
| :--- | :--- | :--- |
| 超文本标记语言 | `.html` 或 `.htm` | 超文本格式，供 Web 浏览器程序（如 Netscape Communicator）阅读。 |
| PostScript | `.ps` | PostScript 格式，用于在 PostScript 打印机上输出。 |
| SGML | `.sgml` | SGML，一种标准文档格式。SGML 通常用于生成以后输出到多种格式的文档。 |
| DVI | `.dvi` | DVI，LaTeX 文本处理工具的输出格式。使用 `dvips` 和 `dvilj` 命令将这些文件转换为 PostScript 或惠普的 PCL。 |
| 纯文本 |  | 不带后缀的文件通常是纯文本文件（ASCII 格式）。 |

#### 表 5-3（续）

| 格式 | 后缀 | 描述 |
| :--- | :--- | :--- |
| 纯文本 |  | 不带后缀的文件通常是纯文本文件（ASCII 格式）。 |

如果你不确定某个文件的格式，可以使用如下方式使用 `file` 命令：

```bash
$ file archive-file
```

该命令会告诉你它是一个 GNU tar 文件、RPM、gzip 还是其他格式。（如果一个文件被重命名并丢失了后缀，这是一个非常有用的技巧。）

### 使用 alien 命令转换软件包

如果有一个非 RPM 格式的软件包可供，而你又想在你的 Red Hat Linux 系统上使用它，你可能可以使用 `alien` 命令将该软件包转换为 RPM 格式。`alien` 命令可以将软件包从 Debian (`.deb`)、Stampede (`.slp`)、Slackware (`.slp`) 或 Red Hat 软件包管理 (`.rpm`) 转换为任何其他格式。

将软件包从其他格式转换为 RPM 的用处是，你随后就可以使用各种 RPM 工具来管理软件包。例如，我从 Debian FTP 站点（`http://ftp.us.debian.org`）下载了 `bsdgames` 软件包。然后我将这个 `.deb` 格式的软件包转换为 RPM 格式，如下：
