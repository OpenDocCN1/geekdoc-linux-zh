
`FreeBSD` (`freebsd.org`) 是 BSD 发行版中最受欢迎的。它可以作为服务器、工作站运行，也被用于网络设备。它以极高性能闻名。

`NetBSD` (`netbsd.org`) 以非常受欢迎而闻名，其版本可作为嵌入式系统运行。`NetBSD` 可以运行在从 32 位和 64 位 PC 到个人数字助理（PDA）的任何设备上。

`OpenBSD` (`openbsd.org`) 是网络服务器的流行系统，尽管也可以作为工作站运行。`OpenBSD` 的目标是实现最大的安全性。与受 BSD 许可证保护的 `FreeBSD` 和 `NetBSD` 不同，`OpenBSD` 主要受互联网系统协会 (ISC) 许可证保护。

`DragonFly BSD` (`dragonfly.org`) 最初基于 `FreeBSD`。它的目标是在对称多处理和并发等领域开发与 `FreeBSD` 不同的技术。其重点在于扩展内核功能。

其他基于 BSD 的自由（指无成本，且可以自由地对代码做任何事）操作系统包括 `Darwin`（`Mac OS X` 基于此）以及面向桌面的系统如 `PC-BSD` 和 `DesktopBSD`。`FreeBSD` 是一个 Live CD BSD 系统。源自 BSD 的专用操作系统包括：

`Mac OS X` (`apple.com/macos`) 由 Apple 生产，侧重于添加易于使用的图形化界面以随其系列电脑销售。还有 `Mac OS X Server` 产品可用。尽管 `Mac OS X` 最初基于 `Darwin`，但它被认为是一种带有开源组件的闭源操作系统。

# 第1章：从 BSD 系统开始

你可以在 DistroWatch 网站（`http://distrowatch.com/search.php?category=BSD`）找到更详尽的 BSD 发行版列表。除了提供这些 BSD 发行版的描述外，你还可以找到购买或下载这些软件的链接。

## 寻找 BSD 资源

尽管现在仍然存在一个 BSD 网站（`www.bsd.org`），但它很大程度上仅充当指向与特定 BSD 发行版相关资源的指针。以下章节包含了与 `FreeBSD`、`NetBSD` 和 `OpenBSD` 相关的有用链接。

## FreeBSD 资源

以下是来自 `FreeBSD` (`www.freebsd.org`) 的有用资源链接：

- `FreeBSD` 支持 (`freebsd.org/support.html`) — 你可以在这里找到 `FreeBSD` 社区和商业支持的联系。

- 获取 `FreeBSD` 软件 (`freebsd.org/where.html`) — 该网站列出了下载或购买 `FreeBSD` 安装 CD 或 DVD 的信息。这包括不同架构（`i386`, `amd64`, `powerpc` 等）的软件。

- `FreeBSD` 特性列表 (`freebsd.org/about.html`) — 描述了 `FreeBSD` 的关键特性。

- `FreeBSD` 新闻 (`freebsd.org/news/`) — 这是 `FreeBSD` 新闻的聚集地。这里有新闻提要、新闻稿、文章和开发状态的链接。你还可以找到与 `FreeBSD` 以及通用 BSD 相关的开发站点和论坛链接。

- `FreeBSD` 项目 (`freebsd.org/projects/`) — 提供有关 `FreeBSD` 开发项目的信息。除了 `FreeBSD` 的基础开发项目外，你还可以找到特殊项目（如 `Google Summer of Code`）以及与现有开源项目（如 `Java`, `GNOME`, `KDE` 和 `OpenOffice.org`）相关的 `FreeBSD` 计划的链接。

## NetBSD 资源

以下是来自 `NetBSD` 网站 (`www.netbsd.org`) 的有用资源链接：

- `NetBSD` 支持 (`netbsd.org/support`) — 提供有关社区和专业支持、支持的硬件、漏洞提交和安全的信息。

- 获取 `NetBSD` 软件 (`netbsd.org/releases`) — 该网站列出了下载 `NetBSD` CD 或 DVD 的信息。提供了通过 `Torrent`、`FTP` 和 `HTTP` 方法下载软件。

- 关于 `NetBSD` (`netbsd.org/about`) — 描述了 `NetBSD` 的关键特性。

- `NetBSD` 新闻 (`netbsd.org/changes/`) — 包含 `NetBSD` 的最新新闻。这包括 `NetBSD` 开发变更的持续列表。

- 软件包 (`netbsd.org/docs/software/packages.html`) — 查找有关 `NetBSD` 软件包集合 (`pkgsrc`) 的信息。这包括可用软件包、文档和支持平台的信息。

## OpenBSD 资源

以下是来自 `OpenBSD` 网站 (`www.openbsd.org`) 的有用资源链接：

- `OpenBSD` 支持 (`openbsd.org/support.html`) — 提供全球范围内适用于 `OpenBSD` 的商业支持和咨询信息。

- 获取 `OpenBSD` 软件 (`openbsd.org/ftp.html`) — 通过 `FTP`、`HTTP`、`ASF` 和 `RSYNC` 提供下载 `OpenBSD` CD 或 DVD 的信息链接。

- `OpenBSD` 项目目标 (`openbsd.org/project.html`) — 描述了 `OpenBSD` 项目的目标。

- `OpenBSD` 新闻 (`openbsd.org/press.html`) — 包含 `OpenBSD` 的媒体报道链接。

- 常见问题 (`cvs.openbsd.org/faq`) — 包含 `OpenBSD` 的常见问题 (`FAQ`) 列表。

## BSD 社区连接

如果你想与 `FreeBSD`、`OpenBSD` 或 `NetBSD` 社区交流，表 1-1 显示了与这些项目相关的最常用交流地的快速列表。

## 表 1-1：连接 BSD 社区的在线资源

| BSD 活动 | 互联网站点 |
|---|---|
| 邮件列表 | `lists.freebsd.org/maillist/listinfo`<br>`www.openbsd.org/mail.html`<br>`www.netbsd.org/mailinglists` |
| `IRC` 聊天 | `www.netbsd.org/community/#chat`<br>`www.freebsd.org/community/irc.html` |
| 论坛 | `www.bsdforums.org`<br>`www.bsdnexus.com`<br>`www.freebsdwiki.net` |
| 博客 | `planet.freebsdish.org` |

表 1-1：连接 BSD 社区的在线资源（续）

| BSD 活动 | 互联网站点 |
|---|---|
| 社区 `Wiki` | `wiki.netbsd.se` |
| `Usenet` 新闻组 | `News:comp.unix.bsd.freebsd.misc`<br>`News:comp.unix.bsd.freebsd.announce`<br>`News:comp.unix.bsd.netbsd.announce`<br>`News:comp.unix.bsd.netbsd.misc`<br>`News:comp.unix.bsd.misc` |
| 文档 | `www.freebsd.org/docs.html`<br>`www.openbsd.org/cgi-bin/man.cgi`<br>`netbsd.org/docs` |
| 新闻 | `news.vejas.lt` |

## 聚焦 BSD 命令

如今，BSD 中的许多重要任务既可以通过图形界面完成也可以通过命令行完成。然而，命令行一直以来并仍然是 BSD 高级用户的首选界面。

图形用户界面 (`GUI`) 看起来可能是直观的。有了一定的经验后，你可能可以弄出，例如如何添加用户、更改日期以及为 `GUI` 配置声卡。对于这些情况，我们会提到需要使用哪种图形工具。对于以下情况，你可能需要命令行：

- 几乎在出现任何问题时通过在线论坛提问来解决问题。此外，命令行工具提供更多反馈。

- 远程系统，如果你在管理服务器，你可能可以使用图形工具。尽管远程访问（使用 `X` 应用或 `VNC`）可能是可用的，但

- `GUI` 工具不支持的功能倾向于提供执行任务最基本的方法。更复杂的操作通常需要仅适用于：

- `GUI` 损坏或未安装——如果没有图形界面，或者安装的 `GUI` 运行不正常，你可能被迫从命令行工作。`GUI` 损坏可能由许多原因引起，例如当你使用仅二进制驱动程序时，内核升级导致驱动程序不兼容。此外，BSD 服务器甚至没有安装 `GUI`。

底线情况是，要释放你 BSD 系统的全部威力，你必须能够使用 `shell` 命令。成千上万的命令可用于监控和管理系统的各个方面。

但无论你是 BSD 大师还是新手，一个巨大的挑战横在面前。你该如何记住你所需的关键命令和选项，当命令 `shell` 可能只向你：

`BSD UNIX 工具箱` 不仅仅是另一个命令参考书或手册页的重述。相反，本书按照你使用命令的方式介绍了 BSD 系统中的命令。换句话说，我们没有按字母顺序列出命令，而是将用于文件系统、连接网络和管理进程的命令分在不同的章节中，以便你根据你想做什么来访问命令，而不仅仅根据它们是如何命名的。

同样，我们不会提供每个命令可用选项的列表。相反，我们将向你展示使用每个命令的最重要且实用的选项的运行示例。从那里，如果你需要更多选项，我们将告诉你快速查找的方法，即通过手册页、`info` 设施和 `help` 选项。

## 寻找命令

书中描述的所有命令在你运行它们时可能并未安装。你可能输入一个命令并看到类似下面的消息：

```
mycommand: command not found
```

这可能由以下原因引起：

- 你拼写错误了命令名称。

- 命令不在你的 `PATH` 中。

- 你可能需要 `root` 用户权限命令才会出现在 `PATH` 中。

- 你的电脑上没有安装该命令。

表 1-2 显示了一些你可以运行的命令，用于查找你想使用的命令。

## 第一章：从 BSD 系统开始

| 表 1-2：查找命令 |
| :--- | :--- |

| 命令与示例输出 | 描述 |
| :--- | :--- |
| `$ type mount`<br>`mount is /sbin/mount` | 显示 `PATH` 中第一个 `mount` 命令。 |
| `$ whereis mount`<br>`mount:/sbin/mount`<br>`/usr/share/man/man/mount.8.gz` | 显示 `mount` 的二进制文件和帮助页（`man page`）。 |
| `$ locate xrdb.1.gz`<br>`/usr/local/man/manl/xrdb.1.gz` | 在文件系统的任何地方查找 `xrdb.1.gz`。 |
| `$ which umount`<br>`/sbin/umount` | 在你的 `PATH` 或别名中查找 `umount` 命令。 |
| `$ pkg_info -W convert`<br>`/usr/local/bin/convert`<br>`installed by package ImageMagick-6.3.6.9` | 查找 `convert` 命令来自哪个软件包。 |

如果你怀疑所需的命令没有安装，可以搜索 `ports` 数据库查找该命令所属的包。如果你找到了正确的包（例如 `bzflag`）但它尚未安装，可以以 `root` 身份输入以下命令从互联网安装：

```bash
# find /usr/ports | grep ImageMagick
/usr/ports/graphics/ImageMagick

# pkg_add -r ImageMagick
```

刚刚显示的命令从 BSD 软件仓库获取 `ImageMagick` 二进制包（`tar bzip2` 格式）并从本地系统进行安装。有关安装软件的其他方法（例如使用 `ports` 系统），请参阅第二章。

## BSD 中的命令参考信息

原始的 BSD、Linux 和 UNIX 文档都是通过手动页（manual pages）完成的，通常称为 `man`。稍后 `info` 设施引入了一项稍微复杂的文档工作。在每个命令内部，几乎总是可以找到帮助消息。

这些参考信息是面向组件的——换句话说，BSD 系统的每个命令、文件格式、系统调用、设备和其他组件都有单独的 `man` 页。与整个软件软件包结合得更紧密的文档通常存储在 `/usr/local/share/doc` 目录的子目录下。

三个参考功能——`man` 页、`info` 文档和帮助消息——在 BSD 系统中均可用。

## 第一章：从 BSD 系统开始

### 使用帮助消息

`-h` 或 `--help` 选项通常用于显示命令的帮助消息。示例说明了如何显示 `ogg123` 命令的帮助：

```bash
$ ogg123 --help | less
ogg123 from vorbis-tools 1.1.1
by the Xiph. Foundation (http://www.xiph.org/)

Usage: ogg123 [<options>] <input file> ...

-h, --help this help
-V, --version display Ogg123 version
-d, --device d uses 'd' as an output device
Possible devices are ('=live, '=file):
oss* null* raw@ au
-f, --file=filename Set the output filename for a previously
specified file device (with -d).
```

之前的输出显示了如何使用 `ogg123` 命令并列出了可用的选项。将输出通过到 `less` 命令可以让你对内容进行分页查看。

### 使用 man 页

假设你想查找与某个单词相关的命令的 `man` 页。使用 `apropos` 命令搜索 `man` 数据库。这会显示 `NAME` 行中包含 `crontab` 的 `man` 页：

```bash
$ apropos crontab
contab(1) - maintain crontab files for individual users (V3)
contab(5) - tables for driving cron
```

`apropos` 的输出在这里显示了包含 `crontab` 的每个 `NAME` 行。数字显示了 `man` 页所在的章节（我们稍后会讨论这些章节）。

`whatis` 命令是仅单独显示包含你输入单词的命令的 `NAME` 行的方法：

```bash
$ whatis cat
cat (1) - concatenate files and print on the standard output
```

显示某个术语 `man` 页的最简单方法是使用 `man` 命令和 `man` 名称。例如：

```bash
$ man
FIND(1) FreeBSD General Commands FIND(1)
NAME walk -- a file hierarchy
```

## 第一章：从 BSD 系统开始

语法 (`SYNOPSIS`)

```
find [-H] [-L] [-P] [-Exdsx] [-f pathname] [pathname ...] expression
```

上面的命令显示了 `find` 命令的 `man` 页。正如你在之前的示例中看到的，某些术语有多个 `man` 页。例如，`crontab` 命令有一个 `man` 页，`crontab` 文件也有一个。`man` 页被组织在不同的章节中，如表 1-3 所示。

### 表 1-3：man 页章节

| 章节 | 描述 |
| --- | --- |
| 1 | 通用用户命令 |
| 2 | 系统调用 |
| 3 | 编程例程 / 库函数 |
| 4 | 设备 |
| 5 | 配置文件和文件格式 |
| 6 | 游戏 |
| 7 | 其他 |
| 8 | 管理命令和守护进程 |
| 9 | 内核接口 |

下面的代码显示了 `man` 命令的一些其他有用选项示例。

```bash
$ man -a mount               显示与组件相关的所有 man 页
$ man 5 crontab             显示组件的第 5 节 man 页
$ man mount -P more          使用 more 而不是 less 进行分页
$ man -f mount                与 whatis 命令相同
$ man -k mount               与 apropos 相同
```

互联网上也可以找到 `man` 页：

```
http://freebsd.org/man
http://openbsd.org/man
http://netbsd.org/man
```

## 第一章：从 BSD 系统开始

### 使用 info 文档

遵循早期 UNIX 系统的传统，`FreeBSD` 提供了一个名为 `sysinstall` 的文本安装设施。该安装程序面向关注功能和灵活性而非图形界面的人士。初始化后运行 `sysinstall` 可以添加更多包并配置网络设置。

```bash
$ info ls
```

### 表 1-4：info 移动

| 按键 | 移动 |
| --- | --- |
| `?` | 显示帮助 |
| `L` | 返回上一页 |
| `n, p, u` | 进入下一页 |
| `Tab` | 进入下一项 |
| `Enter` | 进入光标处 |
| `R` | 遵循交叉引用 |
| `Q` | 退出 |

软件包中特别丰富的文本包括 `gimp`, `festival`, `libc`, `automake`, `zsh`, `sed`, `tar` 和 `bash`，存储在 `/usr/share`。

## 总结

尽管你可以从头到尾阅读这本书，但这旨在作为 BSD 系统中对高级用户最有用的数百个功能的参考。

事实上，下一章将介绍如何获取和安装软件。

## 2

# 安装 FreeBSD 和添加软件

### 本章内容

* 安装 `FreeBSD`
* 获取软件包
* 使用 `ports` 获取和安装软件

## 安装 FreeBSD 之前
