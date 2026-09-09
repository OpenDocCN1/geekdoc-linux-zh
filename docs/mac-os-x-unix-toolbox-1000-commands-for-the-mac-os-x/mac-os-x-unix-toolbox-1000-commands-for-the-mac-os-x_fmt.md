
# MAC OS X UNIX 工具箱：Mac OS X 1000+ 条命令

> 献给 Hope，感谢你依然爱我。
>
> — Thomas Myer

# 关于作者

Thomas Myer 目前居住在德克萨斯州奥斯汀，在那里经营 Triple Dog Dare Media，这是一家构建 `CodeIgniter` 应用、编写技术文档和文案的咨询集团，他也担任派遣系统分析师。他是《Lead Generation on the Web》、《No Nonsense XML Web Development with PHP》、《Professional CodeIgniter》以及《From Geek to Peak: Your First 365 Days as a Technical Consultant》的作者，并撰写了数十关于技术和商业的文章。如果你对本书有任何反馈，或希望讨论任何与 Web 开发、写作或营销相关的内容，可以通过他的网站 www.tripletogs.com 与他联系。

Christopher Negus 是《Fedora and Red Hat Linux Bibles》以及《BSD UNIX Toolbox》的作者。Chris 曾在 BSD UNIX Toolbox 的开发团队工作过八年。

（注：原文中 Christopher Negus 的介绍存在大量重复，此处已按要求保留并翻译重复内容）

# 鸣谢

| 角色 | 姓名 |
| :--- | :--- |
| 采购编辑 | Jenny Watson |
| 副总裁兼执行出版 | Barry Pruett |
| 技术编辑 | Jim Min |
| 项目协调 | Linsey Stanford |
| 排版员 | Daniel |
| 校对 | Copy Editor |
| 校对 | Luann Rouff |
| 出版服务 | Tim Tate |
| 编辑经理 | Richard Swad |
| 副总裁 | Wiley |

# 鸣谢

感谢团队的……感谢我一直耐心的妻子……本书。

# 引言

- 备份到 CD 或 DVD 110
- 共享 `screen` 会话 186
- 使用远程 Windows 桌面 186
- 使用远程桌面和应用程序 187
- 使用 VNC 共享你的桌面 188
- 总结 189

# 第 14 章：锁定安全 191

- 在 `vi` 中移动 201
- 使用杂项命令 204
- 使用 `Ex` 命令 205
- 总结 206

# 附录 B：Shell 字符和变量 207

- 特殊 Shell 字符 207
- 检查网站上的链接 240
- 初始化脚本并加载包 242
- 处理 `@links` 数组 244
- 扩展脚本 246

# 索引 247

# 引言

Mac OS X UNIX Toolbox 部分基于 Chris Negus 和 François Caen 编写的 BSD UNIX Toolbox。当 Wiley 要求我将他们的成果扩展到 Mac OS X 世界时，我非常乐意这样做，因为原作是一份非常优秀的资源。

从一开始开始，我就决定尽可能保留原书的精神和结构。坦率地说，在 Mac OS X 上，Unix 方面的体验大约有 90% 与 BSD 或 Linux 环境相同，因此在很大程度上我能够遵循这一约定。但在某些情况下，我需要对某些章节进行删减，而在其他情况下，我必须额外添加内容。

最后，你手里拿着的是一本超过 1000 页的手册。（注：OCR 显示为“1000,”，但上下文是指字数或页数。我将保留 OCR 的文本逻辑）。

最后，你手里拿着的是一本超过 1000 的……（等等，OCR 文本到此结束了）。

# 序言

- 锁定安全性——设置防火墙和系统日志来保护您的 Mac OS 系统安全。
- 获取参考信息——使用书末的附录来获取更多关于 shell（如元字符和 shell 变量）以及个人配置文件的详细信息。

如果你操作得当，那么使用这本书将比在 Google 上搜索你需要的命令或 GUI 工具要方便得多。

在你掌握了书中描述的许多功能后，你将获得以下优势：

- 几百种命令——通过将大量信息压缩在很小的空间内，你将拥有数百个实用的命令，总计超过 1000 行，并能以一种便携的形式随身携带。
- 可迁移的知识——你在 Mac OS X 系统中使用的大多数相同命令和选项在 UNIX 类系统上的工作方式完全相同。然而，不同的 UNIX 系统提供了不同的图形化管理工具；即使在特定的发行版中，图形化工具的更新也比命令更频繁。
- 快速解决问题——当你启动桌面并打开图形化管理工具时，你已经运行了六个命令并解决了问题。
- 持续的价值——书中描述的许多命令在早期 UNIX 系统中就被使用了，因此你正在获得反映了 30 多年计算机专家经验的工具。

Mac OS X 系统中使用命令的完整文档由数千页 man pages、info 文本和消息组成，你肯定会经常查阅书中以外的内容。幸运的是，Mac OS X 和 UNIX 系统本身就安装了许多有用的信息。第 1 章描述了如何访问这些信息，这些信息可能已经安装在你的系统中，或者可以轻松地安装。

# 本书的结构

这本书既不是一本参考书（按字母顺序列出内容），也不是一份指南（提供完成任务的逐步程序）。相反，本书是按主题组织的，并包含了你可能会用到的最有用的命令和选项。

第 1 章让你对 Mac OS X 有一个基本的了解，以及它与源自 BSD 的操作系统（如 FreeBSD、NetBSD 和 OpenBSD）之间的关系。然后，它描述了一些支持你阅读本书体验的大量资源，例如 man pages、info 资料和帮助文本。第 2 章快速概述了 Mac OS X 环境以及你如何设置它以方便地访问 UNIX 工具。它还简要介绍了 Fink，这是一种包管理器，它可以让你安装书中提到的其他工具。

第 3、4、5、6 章描述了普通用户在 Mac OS 系统上可能会发现的命令。第 3 章描述了使用 shell 的工具，第 4 章是处理文件的命令，第 5 章描述了如何处理文本。第 6 章将带你了解更高级的脚本并引入 AppleScripting。

从第 7 章开始，我们进入与系统管理相关的主题。第 7 章涵盖了创建和检查文件系统，第 8 章描述了数据备份的命令。第 9 章解释了如何运行进程，第 10 章描述了管理基本组件（如硬件模块、CPU 使用和内存使用）的管理工具。

第 11 章引入了管理网络资源的章节，重点是如何设置和使用网络接口。第 12 章涵盖了用于文件传输、共享和电子邮件的文本命令。第 13 章介绍了用于进行系统管理的工具。

第 14 章涵盖了如何使用防火墙和日志等功能锁定安全性。随后是六个附录，提供了文本编辑、shell 特性（元字符和变量）、个人配置文件、AppleScript 命令、快速 Perl 入门以及通过 Fink 可获得的一些你可能想探索的有趣软件包的其他参考信息。

# 使用本书所需的

这绝对不是一本你可以在下次假期时蜷缩在沙发读的书。它不是为了娱乐你。在过程中，我完全预期你是坐在屏幕前的。

## 在 Mac OS X 上开启 UNIX 之旅

你是 Mac 老手了吗？你是否偶尔会使用底层的 UNIX？还是每天使用多次？或者从未听说过它？无论你的技能水平如何，一本介绍在 Mac OS X 上高效使用、检查、修复、保护和增强 UNIX 的方法的书，都将是一份无价的资源。

《Mac OS UNIX Toolbox》就是这份资源。

《Mac OS UNIX Toolbox》主要面向 Mac OS X 用户和管理员。我们将告诉你你所需的内容、如何快速定位和获取软件、监控系统的健康与安全，以及访问网络资源。简而言之，我们直接介绍了使用 UNIX 系统最有效的方法。

我们《Mac OS UNIX Toolbox》的目标是将大量关于 UNIX 工具和系统的有用信息封装成一个你可以随身携带的小型工具包。为此，我们描述了以下内容：

- 大量的命令行示例，提供使用 BSD 系统既实用又清晰的方法
- GUI 工具——配置你系统的图形化管理工具的快速指点
- 软件包——查找和下载海量应用程序的简短步骤
- 在线资源——列出了寻找 BSD 论坛、邮件列表、IRC 通道和其他在线资源的最佳地点
- 本地文档——用于从 man pages、doc 目录、帮助命令以及 BSD 系统上的其他资源收集更多信息的工具

## 本章内容

### 寻找 Mac Os X 资源

### 快速且强大的命令

- 许多实用工具的便捷参考

## 像 Mac Os X 大师一样工作

# 第一章：在 Mac OS X 上开启 UNIX 之旅

由于你不是 Mac OS X 的初学者，你不会看到很多窗口、图标和菜单的截图。然而，你将看到的是获取所需信息的快捷路径，以便充分利用 Mac OS X 上的 UNIX。

如果这听起来对你有用，请继续读下去。

### 关于 FreeBSD、NetBSD 和 OpenBSD

Mac OS X 是一个现代操作系统，它结合了基于 UNIX 的操作系统的强大功能与 Macintosh 界面的简单优雅。这部分开源代码（在此称为 Darwin）是各种 BSD 项目的直接后代。它部分基于 BSD 4.4 Lite，但许多库和实用程序来自 FreeBSD 和 NetBSD。由于这段历史，深入研究 BSD 的历史是有用的。

在 20 世纪 70 年代初，AT&T 将 UNIX 源代码发布给几所学院和大学，允许他们根据自己的意愿开始更改、调整和改进这些代码。这一决策导致了今天每一个自由和开源操作系统的开发，其中基于伯克利软件发行版（BSD）的系统尤为突出。

如果你想了解细节，BSD 的历史很容易通过 Google 找到。对于你的需求，以下是亮点：

- BSD 最初作为 AT&T 第六版的一套软件插件存在。
- 多年来，BSD 开发者开辟了独立的发展道路，通过重写软件旨在替换所有 AT&T 受版权保护的代码。
- 20 世纪 90 年代初，AT&T 的 UNIX 系统实验室起诉了 BSD 开发者（Berkeley Software Design, Inc.）侵犯版权。
- 尽管诉讼最终得以解决（仅需修改 BSD 代码中的少数文件），但 Linux 操作系统能够成为开源软件开发的领导者，而关于“自由 BSD”是如何被构想的问题依然存在。
- 1995 年，伯克利发布的 BSD 最终版本以 4.4BSD-Lite release 2 的名称发布。如今的 BSD 系统（包括 FreeBSD、NetBSD 和 OpenBSD）在某种程度上都基于 4.4BSD-Lite。

操作系统以稳定性和安全性而闻名。BSD 开发于一个计算资源（磁盘空间、网络带宽和内存）按今天的标准来看非常匮乏的时代，因此 BSD 系统是通过高效的命令运行的，而不是今天常见的臃肿应用程序和简化的图形界面。

由于 BSD 系统的本质性，运行这些系统的人需要高水平的专业知识。当 X Window 系统上的简化图形用户界面开始出现时，为了有效操作 BSD 系统，你仍然需要了解内核、设备驱动程序、模块和守护进程（`daemons`）等。由于安全优于使用，BSD 专家需要知道如何处理许多功能可能未安装或默认关闭的情况。

如果你是使用过 Linux 的人，过渡到 BSD 系统不应该太难。然而，BSD 系统往往比 Linux 更具一致性。BSD 中的许多工具都有完善的文档，系统本身也非常稳定。此外，BSD 非常灵活，你可以将其用于许多不同的用途，从台式电脑到服务器。

BSD 中的许多工具都有完善的文档。

以下是流行的 BSD 发行版：

- FreeBSD (www.freebsd.org)
- NetBSD (www.netbsd.org)
- OpenBSD (www.openbsd.org)
- DragonBSD (www.dragonbsd.org)
- Mac OS X (www.apple.com/macos/)
- SunOS (www.sun.com)
- Solaris (www.oracle.com/solaris/)

## 聚焦 Mac OS X 命令

Mac OS X 许多重要任务都可以通过图形界面和命令行完成。然而，命令行一直以来且仍然是 UNIX 高级用户的首选界面。

图形用户界面（GUI）的设计初衷是直观的。具有某些计算机经验的你可能可以自己发现例如如何添加用户、更改日期以及配置声卡。对于这些情况，我们会提到可以使用什么工具完成工作。然而，对于以下情况，你可能需要依赖命令行：

- 几乎会发生任何问题——在在线论坛提问以解决你遇到的某些 UNIX 问题，你得到的帮助几乎全是以命令的形式提供的。此外，当配置设备或访问文件和目录出现问题时，命令行工具通常能提供更多的反馈。
- 远程系统管理——如果你正在管理远程服务器，可能没有图形工具可用。虽然可以使用远程 GUI 访问（使用 X 或 VNC）和基于 Web 的管理工具，但它们的运行速度通常比命令行执行的操作要慢。
- GUI 不支持的功能——GUI 管理工具需要提供执行任务最基本的方法。更复杂的操作通常需要只有在命令行才提供的选项。

底线情况是，为了释放你的 Mac OS 系统的全部威力，你必须能够使用 shell 命令。有成千上万条命令可用于监控和管理你系统的各个方面。

然而，无论你是 UNIX 大师还是新手，都面临着一个挑战：当一个命令可能只向你显示以下内容时，你如何记住你需要的最关键的命令和选项？

Mac OS X UNIX 工具箱不仅仅是另一个命令参考书或页面的刷新。本书根据你实际使用命令的方式介绍了 Mac OS X 上的命令。换句话说，我们没有按照字母顺序列出命令，而是将用于文件系统操作、连接网络和管理进程的命令组合在一起，这样你就可以根据想做什么来查找命令，而不仅仅通过它们的名称。

同样，我们也不会仅仅向你列出每个命令的所有可用选项。相反，我们为每个命令提供了最重要且实用的选项的运行示例。从那里，如果你需要更多选项，我们将介绍如何从 man 页面（帮助页）、info 设施和 help 选项中快速查找的方法。

## 查找命令

书中描述的所有命令都应该在你准备好运行它们时已经安装完毕。然而，请注意，本书基于 Mac OS X 的最新版本（版本 10.5，称为 Leopard），如果你运行的是 Tiger (10.4)，你可能没有安装某些内容。

你可能会输入一个命令并看到类似下面的消息：

```
mycommand: command not found
```

这可能是由于以下原因发生的：

- 你拼错了命令名称。
- 该命令不在你的 `PATH` 中。
- 你可能需要作为 root 用户才能让命令出现在你的 `PATH` 中。
- 电脑上没有安装该命令。

表 1-1 显示了你可以运行的查找要用命令的命令。

### 表 1-1：查找命令

| 命令和示例输出 | 描述 |
|---|---|
| `$ type mount`<br>`mount is /sbin/mount` | 显示 `PATH` 中的第一个 `mount` 命令。 |
| `$ whereis /sbin/mount`<br>`mount: /usr/share/man/mount8.gz` | 显示 `mount` 的二进制文件和 man 页面。 |
| `$ locate xrdb.1.gz`<br>`/usr/local/man/man1/xrdb.1.gz` | 在文件系统的任何地方查找 `xrdb.1.gz`。 |
| `$ which umcount`<br>`sbin/umcount` | 在你的 `PATH` 或别名中任何地方查找 `umcount` 命令。 |
| `$ pkg_info -W convert`<br>`/usr/local/bin/convert`<br>`was installed by package ImageMagick-3.6.3.9` | 查找 `convert` 命令来自哪里 |

如果你怀疑需要的命令没有安装，最好的补救办法可能是升级到最新版本的 Mac OS X。

### 命令参考——UNIX 中的信息

原始的 BSD、Linux 和 UNIX 文档都是在手册页（manual pages）上完成的，通常称为 man pages。稍后，info 家族出现了一项稍微复杂一点文档工作。在每个命令内部，几乎随处都有帮助信息。

这些参考信息是面向组件的——换句话说，对于 BSD 系统的每个命令、文件格式、系统调用、设备和其他组件都有单独的 man 页面。与整个软件软件包对齐更紧密的文档通常存储在 `/usr/local/share/doc` 目录的子目录下。

所有参考功能——man 页面、info 文档和帮助消息——在 BSD 系统中可用。

### 使用帮助消息

`-h` `--help` 选项通常用于显示命令的帮助消息。下面的示例说明了如何为 `man` 命令显示帮助：

```
$ man --help
man, version 1.6c

usage: man [-adfhkktW] [section] [-M path] [-P pager] [-S list]
[-m system] [-p string] name ~

a : 查找所有匹配条目
c : 不使用 cat
d : 打印调试信息块
D : 同 -d，但也显示页面
f : 等同 whatis(1)
h : 打印此帮助消息
k : 等同 apropos(1)
k : 在所有页面中搜索字符串
t : 用于格式化页面以打印
w : 打印将显示的 man 页面位置
  (如果未给出名称：打印将搜索的目录)
W : 同 -w，但显示文件名
```



# 第1章：在 Mac OS X 上开启 UNIX

- GUI 不支持的功能——GUI 管理工具需要提供执行任务最基本的方法。更复杂的操作通常需要只有在命令行才提供的选项。

底线情况是，为了释放你的 Mac OS 系统的全部威力，你必须能够使用 shell 命令。有成千上万条命令可用于监控和管理你系统的各个方面。

然而，无论你是 UNIX 大师还是新手，都面临着一个挑战：当一个命令可能只向你显示以下内容时，你如何记住你需要的最关键的命令和选项？

Mac OS X UNIX 工具箱不仅仅是另一个命令参考书或页面的刷新。本书根据你实际使用命令的方式介绍了 Mac OS X 上的命令。换句话说，我们没有按照字母顺序列出命令，而是将用于文件系统操作、连接网络和管理进程的命令组合在一起，这样就可以根据想做什么来查找命令，而不仅仅通过它们的名称。

同样，我们也不会仅仅向你列出每个命令的所有可用选项。相反，我们为每个命令提供了最重要且实用的选项的运行示例。从那里，如果你需要更多选项，我们将介绍如何从 man 页面（帮助页）、info 设施和 help 选项中快速查找的方法。

## 查找命令

书中描述的所有命令都应该在你准备好运行它们时已经安装完毕。然而，请注意，本书基于 Mac OS X 的最新版本（版本 10.5，称为 Leopard），如果你运行的是 Tiger (10.4)，你可能没有安装某些内容。

你可能会输入一个命令并看到类似下面的消息：

```
mycommand: command not found
```

这可能是由于以下原因发生的：

- 你拼错了命令名称。
- 该命令不在你的 `PATH` 中。
- 你可能需要作为 root 用户才能让命令出现在你的 `PATH` 中。
- 电脑上没有安装该命令。

表 1-1 显示了你可以运行的查找要用命令的命令。

### 表 1-1：查找命令

| 命令和示例输出 | 描述 |
|---|---|
| `$ type mount`<br>`mount is /sbin/mount` | 显示 `PATH` 中的第一个 mount 命令。 |
| `$ whereis /sbin/mount`<br>`mount: /usr/share/man/mount8.gz` | 显示 mount 的二进制文件和 man 页面。 |
| `$ locate xrdb.1.gz`<br>`/usr/local/man/man1/xrdb.1.gz` | 在文件系统的任何地方查找 `xrdb.1.gz`。 |
| `$ which umcount`<br>`sbin/umcount` | 在你的 `PATH` 或别名中任何地方查找 `umcount` 命令。 |
| `$ pkg_info -W convert`<br>`/usr/local/bin/convert`<br>`was installed by package ImageMagick-3.6.3.9` | 查找 convert 命令来自哪里 |

如果你怀疑需要的命令没有安装，最好的补救办法可能是升级到最新版本的 Mac OS X。

## 命令参考——UNIX 中的信息

原始的 BSD、Linux 和 UNIX 文档都是在手册页（manual pages）上完成的，通常称为 man pages。稍后，info 家族出现了一项稍微复杂一点文档工作。在每个命令内部，几乎随处都有帮助信息。

这些参考信息是面向组件的——换句话说，对于 BSD 系统的每个命令、文件格式、系统调用、设备和其他组件都有单独的 man 页面。与整个软件软件包对齐更紧密的文档通常存储在 `/usr/local/share/doc` 目录的子目录下。

所有参考功能——man 页面、info 文档和帮助消息——在 BSD 系统中可用。

### 使用帮助消息

`-h` `--help` 选项通常用于显示命令的帮助消息。下面的示例说明了如何为 `man` 命令显示帮助：

```
$ man --help
man, version 1.6c
```

```
usage: man [-adfhkktW] [section] [-M path] [-P pager] [-S list]
[-m system] [-p string] name ~
```

```
a : 查找所有匹配条目
c : 不使用 cat
d : 打印调试信息块
D : 同 -d，但也显示页面
f : 等同 whatis(1)
h : 打印此帮助消息
k : 等同 apropos(1)
k : 在所有页面中搜索字符串
t : 用于格式化页面以打印
w : 打印将显示的 man 页面位置
  (如果未给出名称：打印将搜索的目录)
W : 同 -w，但显示文件名
```

```
C file : 使用 'file' 作为配置文件
M path : 将手册页的搜索路径设置为 'path'
P pager : 使用程序 'pager' 显示页面
list : 冒号分隔的区域列表
m system : 搜索替代系统的 man 页面
p string : 字符串告诉要运行哪些预处理器
ne - [nreg(1) p - pic(1) t - tbl(1)
g - grap(1) r - refer(1) v - vgrind(1)
```

前面的输出显示了如何使用 `man` 命令并列出了可用的选项。

### 使用 man 页面

假设你想查找与某个单词相关的命令的 man 页面。使用 `apropos` 命令搜索 man 页面数据库。这显示了 man 页面 NAME 行中包含 crontab 的 man 页面：

```
$ apropos crontab
crontab(1) - maintain crontab files for individual users (V3)
crontab(5) - tables for crontab
```

`apropos` 命令显示包含 crontab 的 man 页面。

如果你怀疑需要的命令没有安装，最好的补救办法可能是升级到最新版本的 Mac OS X。

### 使用 info 文档

在某些情况下，开发者将命令、文件格式、设备或其他组件的更完整描述放在 info 数据库中。你可以通过输入 `info` 命令或按特定组件来进入 info 数据库：

```
$ info ls
```

之前的命令显示了 `ls` 命令的信息。使用上、下、左、右箭头以及 Page Up 和 Page Down 来移动。Home 和 End 键分别跳转到节点的开始和结束。当你显示 info 屏幕时，可以使用表 1-3 所示的按键进行操作。

info 数据库中拥有特别大量文本的软件包包括 gimp, festival, libc, automate, zsh, tar 和 bash。info 数据库使用的文件存储在 `/usr/share/info` 目录。

### 总结

虽然你完全可以喜欢从头到尾阅读这本书，但它被设计作为参考工具，介绍 Mac OS X 系统中对高级用户和系统管理员最有用的数百个功能。因为信息



# 使用 man 页面

假设你想查找与某个单词相关的命令的 man 页面。使用 `apropos` 命令搜索 man 页面数据库。这显示了 man 页面 NAME 行中包含 `crontab` 的 man 页面：

```
$ apropos crontab
crontab(1) - maintain crontab files for individual users (V3)
crontab(5) - tables for crontab
```

`apropos` 命令显示包含 `crontab` 的 man 页面。

如果你怀疑需要的命令没有安装，最好的补救办法可能是升级到最新版本的 Mac OS X。

## 使用 info 文档

在某些情况下，开发者将命令、文件格式、设备或其他组件的更完整描述放在 info 数据库中。你可以通过输入 `info` 命令或按特定组件来进入 info 数据库：

```
$ info ls
```

之前的命令显示了 `ls` 命令的信息。使用上、下、左、右箭头以及 Page Up 和 Page Down 来移动。Home 和 End 键分别跳转到节点的开始和结束。当你显示 info 屏幕时，可以使用表 1-3 所示的按键进行操作。

info 数据库中拥有特别大量文本的软件包包括 `gimp`、`festival`、`libc`、`automate`、`zsh`、`tar` 和 `bash`。info 数据库使用的文件存储在 `/usr/share/info` 目录。

## 总结

虽然你完全可以喜欢从头到尾阅读这本书，但它被设计作为参考工具，介绍 Mac OS X 系统中对高级用户和系统管理员最有用的数百个功能。因为信息是按主题组织的，而不是按字母顺序，因此你不需要预先知道命令就能找到完成任务所需的内容。

本书中描述的大部分功能在 Mac OS X 上以及 FreeBSD、NetBSD、OpenBSD 和其他 BSD 系统上的运行同样良好。事实上，这里描述的许多命令用得非常广泛，你可以在大多数 Linux 和 UNIX 系统上完全按照这里的描述那样使用它们。

然而，在 Mac OS X 上工作时存在一些差异，下一章将为任何刚接触 Mac OS X UNIX 世界的新手提供简要介绍。

# 第 1 章：在 Mac OS X 上开启 UNIX

# 第 2 章：刚接触 Mac OS X？

## 本章内容

- 了解 Mac OS X 上的 UNIX
- 查找终端
- 文件夹结构
- 你的主目录
- Spotlight（聚焦搜索）
- 获取和使用 Fink
- 挂载与卸载
- 学习喜爱 `launchd`

对大多数人来说，并没有太大区别。会有一两个发生变化的地方——你绝对会喜欢。对于其他人来说，会有一堆需要适应的事情——但希望你能学会了解这些变化。

本章的目标非常简单：为你提供一次 Mac OS X 上 UNIX 的引导之旅。在本章结束时，你应该已经熟悉你的环境，我们将在过程中花一些时间进行自定义和添加，以提高你的工作效率。

## 什么是 Mac OS X UNIX？

Mac OS X 10.5 (Leopard) 被营销为“一个开放品牌 UNIX 3 注册版，符合 SUS3 和 POSIX 1003.1 规范的 API、Shell 实用程序和线程。”用通俗易懂的话说，Leopard 可以编译并运行所有现有的 UNIX 代码。

此外，Leopard 在同一平台上同时支持 64 位和 32 位应用程序。所有主要的图形库（Cocoa、X11 和 OpenGL）都是可用的。Leopard 还针对多核进行了优化，能够极大地改进调度、内存管理和处理器亲和性算法。

简而言之，你完全支持 Mac OS X 上的 UNIX。它不是某种插件或事后添加的东西。其核心——一组被称为 Darwin 的开源技术，构成了 Mac OS X 上 UNIX 体验的基础。Darwin 本身并不是 Mac OS X，因为它缺乏一些让 Mac OS 体验区别于其他 UNIX 变体的专用部分（例如 Aqua 界面、Carbon、Cocoa、OpenGL、Quartz，以及 QuickTime、iLife 软件套、Safari 和 Xcode 开发环境等）。

Mac OS X 的内核是 `xnu`，它由一个基于 Mach 的核心、一个面向对象的运行时环境和一个基于 BSD 的操作系统组成。Mac 提供了关键的底层服务，其中大多数服务对应用程序和用户是透明的。例如，它处理硬件抽象、进程管理、抢占式多任务、虚拟内存管理、内核调试、控制台 I/O 等。

我们在这里不会花精力研究 BSD 的部分，因为书的大部分内容将致力于该操作系统固有的许多命令和结构。目前，只需说它们有足够的相似之处，让大多数知识丰富的用户感到非常舒适。本章其余部分涵盖了部分差异。

## 查找终端和实用程序

在第 3 章中，你将使用 Terminal（终端），它是你进入命令行提示符的实用程序。但现在，你会发现没有直观的方法找到 Terminal。桌面上没有快捷方式，Dock 栏上没有图标，也没有任何指向 Terminal 提示符的东西。我们现在纠正这一点。

打开 Finder（访达），并双击导航栏中的 Macintosh HD 项目。

接下来，双击右侧的 Applications（应用程序）文件夹。向下滚动到 Applications 下方的 Utilities（实用工具）文件夹并双击打开。

最后，双击 Terminal 图标打开 Terminal 应用程序窗口。

Terminal 应用程序窗口现在位于你的 Dock 栏中，但谁想每次都重复这一长系列步骤呢，特别是考虑到你可能会作为一个 UNIX 极客频繁使用 Terminal？

不用担心，将 Terminal 添加到 Dock 栏非常简单。只需控制键点击（如果你有多按钮鼠标，则右键点击）Terminal 图标，并在上下文菜单中选择“保留在 Dock 中”，如图 2-4 所示。这将让 Terminal 触手可及。

这里另一个实用的技巧：将整个 Utilities 文件夹作为一个项目堆栈添加到你的 Dock 栏中。只需从 Finder 将 Utilities 文件夹拖到 Dock 栏的右侧并将其放在上面。然后你可以点击该堆栈以显示 Utilities 文件夹中每个项目的快捷方式。

![图 2-1：要查找 Terminal，首先点击 Macintosh HD](img/d850b48b6750d726fcc813a2a895d7cc_38_0.png)

![图 2-2：选择实用工具](img/d850b48b6750d726fcc813a2a895d7cc_38_1.png)

![图 2-3：Terminal 应用程序窗口](img/d850b48b6750d726fcc813a2a895d7cc_39_0.png)

![图 2-4：保留在 Dock 中](img/d850b48b6750d726fcc813a2a895d7cc_39_1.png)

![图 2-5：点击堆栈](img/d850b48b6750d726fcc813a2a895d7cc_40_0.png)

![图 2-6：列表](img/d850b48b6750d726fcc813a2a895d7cc_40_1.png)

## 目录结构

在你已经在 Dock 上设置好了 Terminal 和你的 Utilities 文件夹后，让我们快速查看目录结构。在 Terminal 中输入以下命令：

```
ls -a /
```

你会看到很多文件夹。

### 表 2-1：Mac OS X 根目录或目录（续）

| 文件或文件夹 | 描述 |
| --- | --- |
| /Users | 包含系统用户的主目录（root 用户主目录为 `/var/root`） |
| /usr | 包含 BSD UNIX 应用程序和支持文件 |
| /var | 包含经常修改的文件，如日志文件。指向 `/private/var` 的符号链接 |
| /Volumes | 包含所有可见的挂载文件系统，包括可移动介质和挂载的磁盘映像 |

## 你的主目录

所有用户在 `/Users` 下都有一个自己的主目录。如果你的用户名是 `smith`，那么你的主目录就是 `/Users/tsmith`。你也可以使用波浪号 (`~`) 作为该路径的简写形式。几乎任何对波浪号的使用都是允许的，例如：

```
cd -
cd ~/documents
cp ~/*.doc ~/documents
```

你将在第 3 到第 5 章中学习更多关于这些的内容，但现在，了解你的主目录里有什么是很重要的。Mac OS X 在你的主目录中创建了一系列标准的文件和文件夹。表 2-2 提供了这些文件和文件夹的摘要。

### 表 2-2：你主目录中的文件和文件夹

| 文件或文件夹 | 描述 |
| --- | --- |
| Desktop | 桌面上所有的文件和文件夹 |
| Documents | 这是你在 Pages、Keynote、Numbers 以及许多应用程序中处理文档的默认位置。大多数用户会为其他任务创建层级子文件夹。 |
| Downloads | 这是使用 Safari 下载内容的默认位置。 |
| Library | 这是本地用户应用程序的支持文件列表。这也是邮件下载和通讯录中地址存储的地方。这与位于 `/Library` 的全局支持文件不同。 |
| Movies | iMovie 保存的电影的默认位置 |
| Music | iTunes 使用的音乐和媒体文件的默认位置 |
| Pictures | iPhoto 中照片和其他图像文件的默认位置 |
| Public | 当你开启“文件共享”时共享的文件夹 |
| Sites | 当你开启“网络共享”时使用的文件夹 |

将文件存储在正确的位置是个好主意，但你可以在你的主目录内（在一定范围内）创建任何你想要的结构。例如，如果你创建了许多工作流，你可能想创建一个 Workflows 目录。你也可以创建自己的 Applications 文件夹，并在那里使用用户特定的应用程序。

你的主目录中还包含许多“点文件”，例如 `.profile` 等。在接下来的几章中我们将检查这些，因为我们将查看 BASH (Bourne Shell) 等其他 Shell。

## Spotlight（聚焦搜索）

Spotlight 是 Mac OS X 的搜索引擎。要使用它，只需按下 `⌘-space`（空格键）或点击屏幕右上角的放大镜图标。输入一个搜索词，Mac OS X 将对应用程序、音频文件、iCalendar、书签、图像、演示文稿、邮件、PDF、文字处理文档、脚本文件、vCard 文件、HTML 文档等进行搜索，并为你提供一份与初始查询匹配的结果列表。

![图 2-7：Spotlight 是 Mac OS 的搜索引擎](img/d850b48b6750d726fcc813a2a895d7cc_45_0.png)

如果你需要一个带有高级选项的详细 Spotlight 搜索窗口（例如按文件类型、位置、日期、名称、内容等搜索），请按下 `Option-⌘-space`。

作为一名 UNIX 高级用户，你会欣赏这种基于高级元数据的搜索功能，尽管你可能永远不会使用它，因为你可能更习惯使用传统的 `locate` 和 `find` 命令。

你也可以使用命令行通过 `mdfind` 运行搜索，例如：

```
mdfind mac os x
/Users/myerman/Desktop/mac_os_x_toolbox/478363c03.doc
/Users/myerman/Desktop/478363c02_new.doc
/Users/myerman/Documents/Microsoft User Data/Work File A_94721220
/Users/myerman/Desktop/mac_os_x_toolbox/478363c02.doc
/Users/myerman/Library/Caches/Metadata/Safari/History:%2F%2Fwww.google.com%2Fsearch?hl=en&client=safari&ls=en-us&q=mac+os+x+sites+folder&Search=a&q=_webhistory._
```

你会发现 Spotlight 命令行搜索是 `locate` 或 `find` 的极佳替代方案。然而，了解 Mac OS 如何存储特定文件的所有元数据是值得的。`mdls` 工具可以让你深入了解 Spotlight 为某个文件存储的属性：

```
mdls ~/desktop/mac_os_x_toolbox*
kMDItemItemCreationDate = 2008-11-02 12:10:22 -0600
kMDItemItemContentModificationDate = 2008-11-13 16:43:09 -0600
kMDItemItemContentType = "public.folder"
kMDItemItemContentTypeTree = (
"public.folder",
"public.directory",
"public.item"
)
kMDItemItemDisplayName = "mac_os_x_toolbox"
kMDItemFFSContentChangedDate = 2008-11-13 16:43:09 -0600
kMDItemFSCCreationDate = 2008-11-02 12:10:22 -0600
kMDItemFSCreatorCode = ""
kMDItemFSSinderFlags = 0
kMDItemFSHasCustomIcon = 0
kMDItemFFSIsInvisible = 0
kMDItemFFSIsStationary = 0
kMDItemFSLabel = 0
kMDItemFFSName = "mac_os_x_toolbox"
kMDItemFFSNodeCount = 24
kMDItemFSSowernerGroupID = 501
kMDItemFSOOwnerUserID = 501
kMDItemFSizeCode = (null)
kMDItemFSTypeCode = ""
kMDItemKind = "Folder"
kMDItemLastUsedDate = 2008-11-14 14:40:07 -0600
kMDItemUsedDates = (
2008-11-02 00:00:00 -0500,
2008-11-03 00:00:00 -0600,
2008-11-08 00:00:00 -0600,
2008-11-10 00:00:00 -0600,
2008-11-12 00:00:00 -0600,
2008-11-13 00:00:00 -0600,
2008-11-14 00:00:00 -0600)
```

所有这些信息只是你可以运行的查询类型的一个示例。例如，要对“mac os x”运行之前的搜索但将结果限制为文件夹，请使用以下命令：

```
mdfind kMDItemKind == 'Folder' 'mac os x'
/Users/myerman/Desktop/mac_os_x_toolbox/art
/Applications
/Applications/Utilities
/Users/myerman/Desktop
/Users/myerman/Desktop/mac_os_x_toolbox
/Users/myerman/Library/Caches/TemporaryItems
```

## 获取和使用 Fink

Fink 是一个可以在 `kink.sourceforge.net` 下载的开源项目。它是任何在 Mac OS X 上的 UNIX 极客都不应缺少的绝佳工具。它允许你安装从 BSD 或 Linux 移植到 Mac OS X 环境的工具、实用程序和其他插件。

当你下载 Fink 时，双击 DMG 文件并按照安装向导提供的提示操作。

![图 2-8：安装向导](img/d850b48b6750d726fcc813a2a895d7cc_47_0.png)

在安装过程中，Fink 会询问你是否可以添加到 `.profile`。一旦完成，可以通过终端访问其功能：

```
fink -h
```

![图 2-9：添加到 .profile 文件](img/d850b48b6750d726fcc813a2a895d7cc_47_1.png)

## 挂载和卸载驱动

Mac OS X 的优点之一是它会自动挂载驱动。例如，将 USB 优盘插入你的 iMac 或 MacBook Pro。几秒钟后，你会看到桌面上出现一个驱动图标。

![图 2-10：驱动图标出现在桌面上](img/d850b48b6750d726fcc813a2a895d7cc_48_0.png)

现在进入终端，并在 `/Volumes` 目录下运行 `ls` 命令：

```
ls /Volumes
Macintosh HD TDMTHUMB
```

如你所见，它已经挂载了！无需手动挂载驱动器。现在运行 `df -h`：



```
df -h
| Filesystem | Size | Used | Avail | Capacity | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /devdisk2 | 149Gi | 86Gi | 62Gi | 59% | / |
| devfs | 107Ki | 107Ki | Ki | 100% | /dev |
| fdescc | 1.0Ki | 1.0Ki | Ki | 100% | /dev |
| map -hosts | Ki | Ki | Ki | 100% | /net |
| map_home | Ki | Ki | Ki | 100% | /home |
| /dev/disk1 | 974Mi | 578Mi | 396Mi | | /Volumes/TDMTHUMB |
```

要卸载驱动器，只需点击桌面上的驱动器图标并选择“弹出”（Eject）选项。你也可以点击 Finder 窗口中项目名称旁边的弹出图标（见图 2-11）。你将在第 12 章中学习如何通过命令行卸载驱动器。

![](img/d850b48b6750d726fcc813a2a895d7cc_49_0.png)

图 2-11：要卸载驱动器，点击弹出图标

## 学习喜爱 launchd

从 Mac OS X 10.4 (Tiger) 开始，Apple 引入了新的系统启动程序 `launchd`。`launchd` 守护进程接管了许多来自 `cron`、`xinetd`、`mach_init` 和 `init` 的任务，这些程序在传统上负责处理系统初始化、调用脚本、运行启动项以及为用户准备好系统环境。

所有这些系统在 Mac OS X 上仍然存在，但在许多情况下，`launchd` 取代了它们。然而，`launchd` 守护进程不仅仅是视觉上的变化。首先，它为你提供了一种自动启动程序的方法（你不再需要查看它和其他地方，更不用说维护独立的配置文件了）。其次，它极大提升了系统性能。最后，它提供了一种更安全的方法来处理新进程。

例如，当非 root 用户启动程序时，`launchd` 守护进程将以非 root 用户权限处理这些任务，从而提供了额外的安全保障。从性能角度来看，这个新的 `launchd` 仅在启动时使用系统资源，并且可以根据需要独立关闭和重启。

这对你意味着什么呢？在对某些任务做出本能反应之前，你可能需要停下来思考一下。例如，没有必要编写监控文件夹的脚本——`launchd` 已经自动完成这一点。也没有需要通过重启系统来启动新任务，因为 `launchctl`（启动作业控制器）能够让用户保持在自己的工作流中。

你将在第 9 章中学习更多关于 `launchd` 的知识。现在只要知道它在那里并且可能代表你的一种新工作方式即可。

### 总结

在本章中，你学习了关于 Mac OS X 的一些知识，以及它与你可能熟悉的 UNIX 版本之间的区别。无论你来自另一个 BSD 变体、UNIX、System V 还是其他 UNIX 类型，你都会发现 Mac OS X 中的大多数内容仍然是一样的。

到本章结束时，你应该能够方便地在 Dock 栏中访问终端，你的“应用程序”（Utilities）文件夹应该位于方便的堆栈中，并且你应该熟悉目录结构和你的主目录。你还下载了 Fink 以根据需要访问额外的程序和工具，希望你对自动挂载和 `launchd` 有了更好的理解。

现在是时候更熟悉终端和 shell 了。

# 第 3 章：使用 Shell

使用 shell 命令解释器（通常直接称为 shell）可以追溯到第一代 UNIX 系统的早期。除了运行命令的明显用途外，shell 还有许多内置功能，如环境变量、别名（aliases）以及用于编程的各种函数。

Mac OS X 系统有几种不同的 shell 可供选择。过去，`tcsh` 被用作默认 shell。最近，Bourne Again Shell (`bash`) 已成为默认 shell。

本章提供的信息将帮助你使用许多 UNIX shell，特别是 `bash` shell。

| 本章内容 |
| :--- |
| 评估 shell |
| 使用 shell |
| 获取超级能力 |
| 使用环境变量 |
| 创建简单的 shell 脚本 |

## 终端窗口与 shell 访问

从 Mac OS X 图形界面访问 shell 的常用方法是使用终端窗口。在 Mac OS X 上，打开“应用程序”（Applications）文件夹，然后进入“实用工具”（Utilities）文件夹，双击“终端”。这将打开一个终端窗口。

## 命令历史编辑

```bash
ls -CF *doc
$ !CF?
运行包含 CF 字符串的上一条命令
ls -CF *doc
$ !
运行上一个 ls 命令
ls -CF *doc
$ !ls:-B/CF/\n
运行上一个 ls 命令，将 CF 替换为 l
ls -l *doc
```

编辑命令历史的另一种方法是使用 `fc` 命令。通过 `fc`，你可以使用 `vi` 编辑器打开选定的命令历史。编辑后的命令会在退出编辑器时运行。可以通过设置 `FCEDIT` 变量（例如 `FCEDIT=ged`）或在 `fc` 命令行切换不同的编辑器。例如：

```bash
$ fc 978
编辑并运行第 978 号命令
$ fc
编辑并运行上一条命令
$ fc -e /usr/local/bin/nano 989
使用 nano 编辑第 989 号命令
```

（如果尚未安装 nano 等文本编辑器，可以使用 `pkg_add -r` 安装你需要的编辑器。第 5 章描述了若干种文本编辑器以及你所在的软件包。）

使用 `Ctrl+R` 搜索字符串历史。例如，输入 `Ctrl+R` 后输入字符串 `ss`，将得到如下：

```bash
### <Ctrl-r>
(reverse-i-search):ss: sudo /usr/bin/less /var/log/messages
```

按下 `Ctrl+R` 在历史列表中反向搜索 `ss` 的其他出现位置。

注意：默认情况下，`bash` 命令历史编辑使用 emacs 风格的命令。如果你更喜欢 `vi` 编辑器，可以使用 `set` 命令将编辑器设置为 `vi`，从而对历史进行 vi 风格编辑。操作如下：

```bash
set -o vi
```

### 使用行补全

你可以使用 `Tab` 键完成命令行上不同类型的信息。以下是一些示例，你输入部分名称后按 `Tab` 键，以尝试补全你在命令行上想要的信息：

```bash
$ tracer<Tab>
命令补全：补全为 traceroute 命令
$ cd /Users/myerman<Tab>
文件补全：补全为 /Users/myerman 目录
$ cd -myer-<Tab>
用户主目录补全：补全为 /Users/myerman
$ echo $<Tab>
环境变量补全：补全为 $PATH
$ ping @<Tab>
主机补全：显示来自 /etc/hosts 的主机
@davinci.example.com
@ritchie.example.com @thompson.example.com
@localhost
@zooey
```

### 重定向 stdin 和 stdout

与大多数 UNIX 系统一样，Mac OS X 支持 `stdin`、`stdout` 和 `stderr`。标准输入（`stdin`）通常是接受用户交互命令的键盘，但也可以是一个包含命令的文件或单独进程。标准输出（`stdout`）通常是屏幕，但 `stdout` 可以重定向到某种文件。如果你从初始命令中重定向大量数据，或者创建数据的进程在持续运行，这将非常有用。标准错误（`stderr`）由可以与其他输出分离的消息组成。

让我们运行一个简单的示例来解释这三种状态。在 shell 中输入内容会使其以交互方式运行——这在 UNIX 世界中被称为标准输入。产生的进程有两个输出流：用于普通命令输出的 `stdout` 和用于错误输出的 `stderr`。在以下示例中，当找不到 `/tmp` 时，错误消息将到 `stderr`，但链接 `/tmp`（已找到）的输出将到 `stdout`：

```bash
$ ls /tmp
ls: No such file or directory
/tmp/
gconfd-fcaen keyring-b41WuB keyring-ItEWbz mapping-fcaen orbit-fcaen
```

默认情况下，所有输出都定向到屏幕。使用大于符号（`>`）将输出重定向到文件。具体来说，你可以将标准输出流（使用 `>`）或标准错误流（使用 `2>`）重定向到文件。

在以下示例中，`stdout` 被重定向到文件 `output.txt`，而 `stderr` 仍然定向到屏幕：

```bash
$ ls /tmp /tmp > output.txt
ls: /tmp: No such file or directory
```

在下一个示例中，`stderr`（流 2）被定向到 `errors.txt`，而 `stdout` 到屏幕：

```bash
$ ls /tmp /tmp 2> errors.txt
/tmp/
gconfd-fcaen keyring-b41WuB keyring-ItEWbz mapping-fcaen orbit-fcaen
```

最后，要追加到文件而不是覆盖，请使用双大于符号：

```bash
$ ls /tmp >> output.txt
```

## 别名

使用刚刚显示的别名，输入 `fi string` 会导致当前目录及其子目录变为包含你输入的字符串的 `.bashrc`。你可以按照如下方式向 `.bashrc` 文件中添加别名：

```bash
### alias la='ls -la' >> ~/.bashrc
```

使用 `unalias` 命令从当前 `bash` 会话中移除别名：

```bash
### unalias la
取消之前设置别名的 la 命令
### unalias -a
取消所有别名命令
```

## 跟踪文件

要观察纯文本文件内容随时间推移的增长，你可以使用 `tail` 命令。例如，你可以按照如下方式查看消息添加到 `/var/log/install.log` 文件的情况：

```bash
### tail -f /var/log/install.log
```

按下 `Ctrl+C` 退出 `tail` 命令。

## 获取超级权限

当你打开 shell 时，你能够根据你的用户/组 ID 以及为这些组件设置的权限运行命令并访问文件和目录。许多系统功能限制为 root 用户（也称为超级用户）。

在 Mac OS X 上，默认禁用了 root 用户。如果你需要以 root 身份执行某些操作，请使用 `sudo` 命令。

`sudo` 命令为 root 用户以外的用户提供了非常细粒度的权力授权。当你有多个用户时，`sudo` 功能是授予特定提升权限并记录用户使用权限执行的所有操作的绝佳工具。除非另有说明，`sudo` 以 root 身份运行。

只需在你想运行的命令前面加上 `sudo` 命令即可：

```bash
$ sudo /usr/bin/less /var/log/apache2/error_log
Password:
```

用户输入自己的密码后，就可以分页查看 `/var/log/apache2/error_log` 文件。此时还会设置一个时间戳。在接下来的五分钟内（默认），该用户可以输入之前的命令行，它将执行而无需提示密码。

## 使用环境变量

对你的 shell 环境有用的少量信息存储在环境变量中。按照惯例，环境变量名称均为大写（尽管这不是强制性的）。如果你使用 `bash` shell，某些环境变量可能会在各种 `bash` 启动脚本中设置：`/etc/profile` 和 `~/.bash_profile`（如果存在）。

要按字母顺序显示已为你的 shell 设置的所有环境变量，输入以下内容：

```bash
$ set
Apple_PubSub_Socket_Render=/tmp/launch-HxisSD/Render
BASH=/bin/bash
BASH_ARGC=
BASH_ARGV=
BASH_LINENO=
BASH_SOURCE=
BASH_VERSINFO={[0]=*3 [1]=*2 [2]=*17 [3]=*1 [4]=release [5]=i386-apple-darwin.9}
BASH_VERSION=3.2.17(1)-release
COLUMNS=153
COMMAND_MODE=unix2003
```

输出仅包含你将看到的环境变量的示例。你也可以自己设置或重置任何变量。例如，为变量 `ABC` 赋值值 `123`（然后显示 `ABC` 的内容），输入以下内容：

```bash
$ ABC=123
$ echo $ABC
123
```

变量 `ABC` 仅存在于创建它的 shell 中。如果你从 shell 启动命令（`ls`, `cat`, `firefox` 等），该新进程将看不到该变量。启动一个新的 `bash` 进程并测试此：

```bash
$ bash
$ echo $ABC
$
```

你可以通过 `export` 使变量成为环境的一部分并可被子进程继承：

```bash
$ export ABC=123
$ bash
$ echo $ABC
123
```

你还可以将字符串连接到现有变量：

```bash
### export PATH=$PATH:/home/fca
```

列出你的 `bash` 环境变量使用以下：

```bash
### env
```

当你准备好创建环境变量时，避免使用系统已常用的名称。查看附录 B 获取环境变量列表。

## 创建简单的 Shell 脚本

Shell 脚本适用于自动化重复任务。`Bash` 和其他 shell 包含了编程语言中常见的循环、测试语句等。主要区别在于只有一种类型的变量。在稍后的第 6 章，你将学习更多关于 shell 脚本的知识，但这里有一些示例。

### 编辑和运行脚本

Shell 脚本是文本文件。你可以使用你喜欢的编辑器（如 `vi`）创建它们。为了运行，shell 脚本必须是可执行的。例如，如果你创建一个名为 `myscript.sh` 的 shell 脚本，可以通过如下方式使其可执行：

```bash
$ chmod +x myscript.sh
```

另一种方法，你可以用 `bash` 命令在它前面加上路径来运行。注意，shell 脚本的第一行应该是这样的：

```bash
#!/bin/bash
```

当你运行它时，如果 `myscript.sh` 不在你的 `PATH` 中，可能会得到以下结果：

```bash
$ myscript.sh
bash: myscript.sh: command not found
```

在这个示例中，包含 `myscript.sh` 的目录不在 `PATH` 中。要修复这个问题，你可以编辑 `PATH`，将脚本复制到 `PATH` 中的目录，如下所示：

```bash
$ mkdir /bin; cp myscript.sh /bin; PATH=$PATH:/bin
$ /bin/myscript.sh
$ /tmp/myscript.sh
```

避免将 `.` 放入 `PATH` 以从当前目录运行。这种技术可能会导致具有同名的命令（如 `ls` 或 `cat`）被意外执行。

### 为你的脚本添加内容



虽然 shell 脚本可以是简单的命令序列，也可以像任何编程语言一样使用。本节描述了如何使用复合命令，例如 `if/then` 语句、`case` 语句和 `for/while` 循环。下面的示例代码将字符串 `abc` 赋值给变量 `MYSTRING`。它测试输入以确定是否等于 `abc` 并根据测试结果操作。测试发生在括号 `[ ]` 之间：

```bash
MYSTRING=abc
if [ $MYSTRING = abc ]; then
  echo "The variable is abc"
fi
```

取反测试，使用 `!=` 代替 `=`，如下所示：

```bash
if [ $MYSTRING != abc ]; then
  echo "$MYSTRING is not abc"
fi
```

以下是数字测试示例：

```bash
MYNUMBER=1
if [ $MYNUMBER -eq 1 ]; then echo "MYNUMBER equals 1";
if [ $MYNUMBER -lt 2 ]; then echo "MYNUMBER <2";
if [ $MYNUMBER -le 1 ]; then echo "MYNUMBER <=1";
if [ $MYNUMBER -gt 0 ]; then echo "MYNUMBER >0";
if [ $MYNUMBER -ge 1 ]; then echo "MYNUMBER >=1";
```

让我们看看文件名的一些测试。在这个示例中，你可以检查文件是否存在 (`-e`)、是否为普通文件 (`-f`) 或是目录 (`-d`)。这些检查通过 `if/then` 语句完成。如果没有匹配，则使用 `else` 语句产生结果：

```bash
filename="$HOME"
if [ -e $filename ]; then echo "$filename exists"; fi
if [ -f "$filename" ]; then
  echo "$filename is a regular file"
elif [ -d "$filename" ]; then
  echo "$filename is a directory"
else
  echo "I have no idea what $filename is"
fi
```

表 3-1 显示了你可以对文件、字符串和变量执行的测试示例。

### 表 3-1：测试表达式的操作符

| 操作符 | 执行的测试 |
| --- | --- |
| `-a file` | 检查文件是否存在（同 `-e`） |
| `-b file` | 检查是否为特殊设备 |
| `-c file` | 检查是否为字符特殊设备（如串口设备） |
| `-d file` | 检查是否为目录 |
| `-e file` | 检查文件是否存在（同 `-a`） |
| `-f file` | 检查文件是否存在且为普通文件（例如，不是目录、套接字、管道、链接或设备文件） |
| `-g file` | 检查是否设置了组 ID 位 |
| `-h file` | 检查是否为符号链接（同 `-L`） |
| `-k file` | 检查是否设置了粘滞位 |
| `-L file` | 检查是否为符号链接（同 `-h`） |
| `-n string` | 检查字符串长度是否大于 0 字节 |
| `-O file` | 检查你是否拥有该文件 |
| `-p file` | 检查是否为命名管道 |
| `-r file` | 检查你是否可读取该文件 |
| `-s file` | 检查文件是否存在且大于 0 字节 |

### 表 3-1：测试表达式的操作符（续）

| 运算符 | 执行的测试 |
| --- | --- |
| `-S file` | 检查文件是否存在并为套接字 (socket) |
| `-t fd` | 检查文件描述符是否连接到终端 |
| `-u file` | 检查文件是否设置了设置用户 ID (set-user-id) 位 |
| `-w file` | 检查你是否有权限写入该文件 |
| `-x file` | 检查你是否有权限执行该文件 |
| `-z string` | 检查字符串长度是否为 0（零）字节 |
| `expr1 -a expr2` | 检查第一个和第二个表达式是否均为真 |
| `expr1 -o expr2` | 检查两个表达式是否有一个为真 |
| `file1 -nt file2` | 检查第一个文件是否比第二个文件新（使用修改时间） |
| `file1 -ot file2` | 检查第一个文件是否比第二个文件旧（使用修改时间） |
| `file1 -ef file2` | 检查两个文件是否通过链接关联（硬链接或符号链接） |
| `var1 = var2` | 检查第一个变量是否等于第二个变量 |
| `var1 -eq var2` | 检查第一个变量是否等于第二个变量 |
| `var1 -ge var2` | 检查第一个变量是否大于或等于第二个变量 |
| `var1 -gt var2` | 检查第一个变量是否大于第二个变量 |
| `var1 -le var2` | 检查第一个变量是否小于或等于第二个变量 |
| `var1 -lt var2` | 检查第一个变量是否小于第二个变量 |
| `var1 != var2` | 检查第一个变量是否等于第二个变量 |

另一个常用的构造是 `case` 命令。使用 `case` 语句可以测试不同的情况并根据结果采取操作。与编程语言中的 `switch` 语句类似，`case` 语句可以代替多个嵌套的 `if` 语句：

```bash
case "$VAR" in
  1)
    { action1 };;
  string2)
    { action2 };;
  *)
    { default action };;
esac
```

你可以在 `/etc/rc.d/` 目录下的系统启动脚本找到 `case` 的用法示例。每个脚本根据传递给它的参数执行操作，并通过一个大型 `case` 结构进行选择。

bash shell 提供了标准的循环构造，接下来的几个示例对其进行了说明。在第一个示例中，`NUMBER` 变量的所有值（0 到 9）都出现在该行中：

```bash
for NUMBER in 0 1 2 3 4 5 6 7 8 9
do
  echo The number is $NUMBER
done
```

在接下来的示例中，`ls` 命令的输出（文件列表）提供了 `for` 语句所作用的变量：

```bash
for FILE in $(/bin/ls); do echo $FILE; done
```

与其向 `for` 语句提供整个值列表，你也可以增加一个值并通过 `while` 循环继续执行，直到满足某个条件。在下面的示例中，`VAR` 初始化为 0，`while` 循环持续增加，直到 `VAR` 的值变为 3：

```bash
VAR=0
while [ $VAR -lt 3 ]; do
  echo $VAR
  VAR=$[$VAR+1]
done
```

与上述 `while` 语句获得相同结果的另一种方法是使用 `until` 语句，如下例所示：

```bash
VAR=0
until [ $VAR -eq 3 ]; do echo $VAR; VAR=$[$VAR+1]; done
```

如果你刚开始学习 shell 编程，请参考 [Bash 入学者指南](http://tldp.org/LDP/Bash-Beginners-Guide/html/index.html)。你可以使用此指南配合 `bash man` 手页等参考资料，逐步学习许多 shell 脚本技术的示例。如果你使用 C shell (csh)，请参阅 [C Shell 简介](http://docs.freebsd.org/44doc/usd/04.csh/paper.html) 获取更多信息。

### 总结

尽管 Mac OS X 的界面非常强大，但 shell 仍然是 UNIX 高级用户的首选界面。所有用户默认使用 bash shell。它包含了许多实用的功能，用于记忆命令（history）、补全命令、分配别名（aliases）以及重定向命令的输入和输出。你可以使用简单的 shell 脚本技术创建你自己的强力命令。

## 文件操作

Mac OS X 文件系统中的一切都可以被视为一个文件。这包括数据文件、目录、设备、命名管道、链接和其他类型的文件。每个文件都关联有一组信息，决定了谁可以访问文件以及如何访问。本章涵盖了许多探索和处理文件的命令。

- 本章内容
- 设置权限
- 遍历文件系统
- 创建和复制文件
- 使用硬链接/符号链接
- 修改文件属性
- 搜索文件
- 列出并验证文件

### 理解文件类型

到目前为止，目录和普通文件是你最常用的文件。然而，在使用 Mac OS X 时，你会遇到几种类型的文件。从命令行来看，你有许多方法创建、查找和列出不同类型的文件。

提供访问计算机硬件组件权限的文件被称为设备文件。包括字符设备和块设备。你可以使用硬链接和软链接使得同一个文件从不同的位置被访问。普通用户也会使用（尽管不那么直接）命名管道和套接字，它们提供了通信的访问点。

### 普通文件

目录和普通文件是你最常用的文件。然而，在使用 Mac OS X 时，你会遇到几种类型的文件。从命令行来看，你有许多方法创建、查找和列出不同类型的文件。

普通文件由数据文件（文档、图像、归档等）和命令（二进制文件和脚本）组成。你可以使用 `file` 命令来确定文件的类型。在下面的示例中，你进入包含配置文件的目录并使用 `file` 查看其中的文件类型：

```bash
$ cd ~/library/safari
$ file *
Bookmarks.plist: Apple binary list
Downloads.plist:   data
History.plist:      Apple binary list
LastSession.plist: data
WebIcons.db:      SQLite database (Version 3)
```

`file` 命令显示了与 Safari 相关的各种类型文件。它可以查看文件是否包含 HTML 标记（用于网页）、纯文本或图像。

普通文件可以由任何保存数据的应用程序创建。如果你只想创建空白文件，有很多方法。这里是两个示例：

```bash
$ touch /tmp/newfile.txt          # 创建一个空白文件
$ cat /dev/null > /tmp/newfile.txt      # 创建一个空文件
```

使用长格式列表是另一种查看文件类型的方法：

```bash
$ ls -l /tmp/newfile2.txt      # 列出文件以查看类型
-rw-rw-r-- 1 root chris 05 Sep 15 14:19 newfile2
```

权限信息中的第一个字符如果是横杠（`-rw-rw-r--`），则该项目是一个普通文件。（权限将在本章后面的“设置文件/目录权限”部分解释。）命令也是普通文件，但通常保存为可执行文件。这里有一些示例：

```bash
$ ls -l /usr/bin/apropos
-xr-xr-x 1 root wheel 2248 Jan 12 2007 /usr/bin/apropos
$ file /usr/bin/apropos
/usr/bin/apropos: Bourne shell script text executable
$ file /bin/ls
```

```
/bin/ls: Mach-O universal binary with 2 architectures
/bin/ls (for architecture i386)          Mach-O executable i386
/bin/ls (for architecture ppc7400)     Mach-O executable ppc
```

`apropos` 命令根据所有者、组和其他人的 `x` 设置可以执行。通过运行 `file` 查看 `apropos`，你可以看到它是一个 shell 脚本。与之前提到的二进制执行文件相反。

### 使用目录

目录是文件和子目录的容器。目录按照从根目录 (`/`) 到多个子目录的层次级结构设置，并斜杠 (`/`) 分隔。在 Finder 中访问时，目录被称为文件夹。

# 第 4 章：文件操作

为了为存储你的数据创建新目录，你可以使用 `mkdir` 命令。

以下是使用 `mkdir` 以不同方式创建目录的示例：

```bash
$ mkdir /tmp/new         # 在 /tmp 中创建 "new" 目录
$ mkdir -p /tmp/a/b/c    # 根据需要为 "new" 创建父目录
$ mkdir -m 700 /tmp/new2  # 创建具有 drwx------ 权限的 new2
```

第一个 `mkdir` 命令只是简单地将新目录添加到现有目录中。第二个示例根据需要创建目录（子目录 a、b 和 c）以生成最终的 new 目录。最后一个命令添加了 `-m` 选项，用于设置目录权限。

你可以通过以下方式识别该文件是否为目录，因为目录的 10 字符权限字符串的第一个字符是 `d`：

```bash
$ file /tmp/new
/tmp/new: directory
$ ls -ld /tmp/new
drwxr-xr-x 2 chris chris 4096 Sep 5 14:53 /tmp/new
```

注意，如果你想进入（`cd`）该目录，则执行位 (`x`) 必须开启。

### 使用符号链接和硬链接

与其复制文件和目录，不如建立链接以便从多个位置访问同一个文件。Mac OS 同时支持软链接（通常是符号链接）和硬链接。

当你运行命令打开一个指向文件的符号链接，或切换到某个目录的目标时，你运行的命令将作用于你链接指向的目标文件或目录。链接本身拥有一套权限和所有权，但你无法从符号链接上看到这些权限。符号链接可以存在于与目标不同的分区上。即使目标不存在，符号链接也可以存在。

> 注意：当你使用如 `tar` 等命令备份包含符号链接的文件时，有多种方法可以选择是否备份实际文件。如果你备份了实际文件，恢复文件可能会导致链接被覆盖（这可能不是你想要的）。请参阅 `tar` 页面以获取有关备份符号链接的不同方法的详细信息。

硬链接只能用于文件，不能用于目录，它基本上是为同一个物理文件提供多个名称的方法。每个物理文件都至少有一个硬链接，这通常被认为是文件本身。任何指向该单个物理文件的额外名称（硬链接）必须与原始文件位于同一个分区上（事实上，判断文件是否为硬链接的一种方法是它们具有相同的 inode 编号）。

更改指向文件的任何硬链接的权限、所有权、日期/时间戳或内容，会导致所有其他链接也随之更改。然而，删除一个链接不会删除文件；它将一直存在，直到最后一个链接（从技术上说，硬盘上的最后一个节点）被删除。

以下是使用 `ln` 命令创建硬链接和符号链接的一些示例：

```bash
$ touch myfile
$ ln myfile myfile-hardlink
$ ln -s myfile myfile-symlink
$ ls -li myfile*
```

注意，在创建硬链接和符号链接后，你使用 `ls -li` 命令列出结果。`-li` 选项显示与每个文件相关的 inode。你可以看到 `myfile` 和 `myfile-hardlink` 具有相同的 inode 号 `292007`（表示完全相同的文件 inode 编号）；`myfile-symlink` 符号链接具有不同的 inode，尽管硬链接显示为文件 (`-`)，但符号链接被识别为链接 (`l`) 且具有完全开放的权限。在你尝试访问链接指向的文件或列出链接目标之前，你无法知道是否可以访问。

### 使用设备文件

当应用程序需要与计算机的硬件通信时，指向设备文件的直接数据存储在 `/dev` 目录中。历史上，设备通常分为块设备（如存储介质）和字符设备（如串口和终端设备）。然而，Mac OS 只使用字符设备与硬件通信。

以下是设备文件的示例：

```bash
$ ls -l /dev/
crw-rw-r-- 1 root operator 0, 94 Jan 29 19:12 ac0   # CD 驱器
crw-rw-r-- 1 root operator 0, 85 Jan 29 19:12 ad0   # 硬盘
crw-------- 1 chr tty 0, 100 Jan 31 06:07 tty0      # 远程登录终端
crw------ 1 chr tty 0, 60 Jan 30 07:18 tty1         # 第一个虚拟终端
crw------- 1 root wheel 0, 61 Jan 29 19:12 tty1     # 第二个虚拟终端
```

### 使用命名管道和套接字

当你允许一个进程向另一个进程发送信息时，你可以简单地将输出管道 (`|`) 到另一个进程的输入。然而，为了在文件系统中提供一个进程可以与其他进程通信的存在，你可以创建命名管道或套接字。命名管道通常用于本地系统的进程间通信，而套接字可以用于进程跨网络通信。

命名管道和套接字通常由 `/tmp` 目录下的应用程序设置。这里是一些命名管道和套接字的示例：

```bash
$ ls -l /tmp/.TV-chris/vtftime-local /.X11-unix/X0
prw---- 1 chris chris Sep 26 2020 /tmp/TV-chris/vtvtifo-local
srwx---- 1 chris wheel Sep 4 ...
```

# 第 4 章：文件操作

### 表 4-1：更改目录和文件访问权限（续上）

| chmod（八进制或字母） | 原始权限 | 新权限 | 描述 |
| --- | --- | --- | --- |
| `chmod 0711` | 任意 | `drwx-x--x` | 对于所有者权限与 `0700` 相同。所有其他人都可以进入该目录，但不能查看或更改目录中的文件。这对于服务器加固非常有用，你可以防止他人列出目录内容，但如果有人已经知道某个文件在目录中，则允许其访问该文件。 |
| `chmod go+r` | `drwx------` | `drxr--r--` | 为目录添加读取权限可能不会产生预期的结果。如果没有执行权限（`x`），其他人无法查看该目录中任何文件的内容。 |



# 文件权限与操作

## chmod 权限示例

| chmod 命令（八进制或字母） | 原始权限 | 新权限 | 描述 |
| --- | --- | --- | --- |
| `chmod 0777` | 任意 | `drwxrwxrwx` | 所有权限完全开放。世界上任何地方的任何人都可以读取、写入或执行此文件。显然，这完全不安全。 |
| `chmod 0000` | 任意 | `d-------` | 所有权限均关闭。这有助于保护目录不受意外更改，但以非 root 用户运行的备份程序可能无法备份该目录的内容。 |
| `chmod 666` | 任意 | `-rw-rw-rw-` | 完全开放文件的读取/写入权限。 |
| `chmod go-rw` | `-rw-rw-rw-` | `-rw------` | 除了所有者外，不允许任何人查看、更改或删除该文件。 |
| `chmod 644` | 任意 | `-rw-r--r-` | 仅所有者可以更改或删除文件，但所有人都可以查看。 |

模式行中的 `0` 通常可以省略（例如，你可以使用 `777` 代替 `0777`）。占位符具有特殊含义。它是一个八进制数字，用于在命令（可执行文件）上指示该命令可以作为 set-UID 程序运行 (`4`)、作为 set-GID 程序运行 (`2`)，或变为粘滞程序 (`1`)。使用 set-UID 和 set-GID 时，命令将以指定的用户或组权限运行（而不是以启动命令的用户或组的权限运行）。

> **警告！** SUID 不应用于 shell 脚本上。由 root 用户运行的 shell 脚本容易受到攻击，可能导致攻击者获得 root 权限的 shell 访问。

在目录上设置粘滞位（sticky bit）可以防止用户删除或重命名他们不拥有的文件（`/tmp` 是一个示例）。在正确的权限设置下，用户可以更改粘滞目录中他们不拥有的文件。在粘滞目录上，最后一个权限字符是 `t` 而不是 `x`。开启粘滞位的命令曾用于使命令即使在未使用时也保留在内存中。这是一个旧的 UNIX 特性，在大多数现代 BSD、UNIX 和 Linux 系统中不再支持。

`-R` 选项是 `chmod` 命令的一个方便功能。使用 `-R`，可以递归地更改从文件系统某点开始的所有文件和目录的权限。以下是一些示例：

```bash
chmod -R 700 /tmp/test   # 仅打开 /tmp/test 下的权限
chmod -R 000 /tmp/test   # 关闭 /tmp/test 下的所有权限
chmod -A +rwx /tmp/test  # 对 /tmp/test 下所有内容打开所有权限
```

注意，`-R` 选项包含你所指的目录。例如，前面的权限将更改 `/tmp/test` 目录本身，而不仅仅是该目录下方的文件和目录。

## 设置 umask

赋予文件或目录的权限最初是在项创建时分配的。这些权限的设置方式取决于用户当前的 `umask` 值。使用 `umask` 命令，你可以设置在创建文件和目录时赋予的权限：

```bash
$ umask 0066  # 使目录变为 drwx-x-x，文件变为 --rw-----
$ umask 0077  # 使目录变为 drwx------，文件变为 --rw-r---
$ umask 0022  # 使目录变为 drwxr-xr-x，文件变为 -rw-r--r-
$ umask 0777  # 使目录变为 d---------，文件变为 r--------
```

## 更改所有权

当你创建一个文件或目录时，你的用户账户会被分配给该文件或目录。你的主组也是如此。作为 root 用户，你可以使用 `chown` 和 `chgrp` 命令分别将文件的所有者（用户）和组更改为不同的用户或组。以下是一些示例：

```bash
chown chris test/              # 将所有者改为 chris
chown chris:market test/       # 将所有者改为 chris，组改为 market
chgrp market test/             # 将组改为 market
chown -R chris test/           # 将 test/ 下的所有文件所有者改为 chris
```

递归选项 (`-R`) 在你需要更改整个目录结构的所有权时非常有用。在 `chmod` 中，递归地使用 `chown` 会更改指定目录及其内容的权限。例如，当某人离开公司或停止使用你的网络服务时，你可能会递归使用 `chown`。你可以使用 `chown -R` 将他们的 `/Users` 目录重新分配给另一个用户。

## 遍历文件系统

更改目录 (`cd`)、检查当前目录 (`pwd`) 和列出目录内容 (`ls`) 的基本命令对于普通 shell 用户来说是为人知的，因此本节重点关注这些命令中一些不常用的选项，以及在文件系统中切换的技巧。

```bash
cd /       # 切换到根目录
cd ..      # 切换到父目录
cd ~       # 切换到主目录
```

---

# 第 4 章：文件操作

## dd 命令复制数据

`dd` 命令是另一种复制数据的方法。此命令在 Mac OS X 上非常强大，一切皆文件，包括硬件外围设备。这是一个示例：

```bash
$ dd if=/dev/zero of=/tmp/nullfile count=1
1+0 records in
1+0 records out
512 bytes transferred in 0.000253 secs (2022113 bytes/sec)
```

`/dev/zero` 是一个生成空字符的特殊文件。在上面的示例中，`dd` 命令将 `/dev/zero` 作为输入文件并输出到 `/tmp/nullfile`。`count` 是块的数量。默认情况下，一个块为 512 字节。结果是一个充满空字符的 512 字节的文件。你可以使用 `less` 或 `vi` 查看文件内容，但查看该文件的更好工具是 `od`（八进制转储）：

```bash
$ od -vt xi /tmp/nullfile
```

这里是 `dd` 命令的另一个示例。它将块大小设置为 2 字节，并复制 10 个块（字节）：

```bash
$ dd if=/dev/zero of=/tmp/nullfile count=10 bs=2
10+0 records in
10+0 records out
20 bytes transferred in 0.000367 secs (54507 bytes/sec)
```

> **警告！** 以下 `dd` 命令将覆盖你的磁盘分区内容。为了安全起见，请使用示例数据设备，例如 USB 闪存，我们假设它可以被覆盖而不会损坏你硬盘的内容。如果你对正在使用的设备有任何疑问，请不要尝试这些命令。

以下命令将第二个驱动器的第一个分区复制到第一个 USB 驱动器。这对于将小分区备份到 USB 闪存非常有用。以下命令将覆盖你的 USB 驱动器内容：

```bash
$ dd if=/dev/da11 of=/dev/da0s
```

下一个示例为主主 IDE 硬盘的第一个分区创建压缩备份。通常在进行此类备份之前，应该卸载该分区：

```bash
umount /dev/da0s1 | gzip > bootpart.gz
dd if=diskboot.img of=/dev/da0s1
```

以下命令将启动镜像（`diskboot.img`）复制到你的 USB 闪存（假设驱动器显示为 `/dev/da0`）：

```bash
$ dd if=diskboot.img of=/dev/da0
```

此示例将第二个 IDE 硬盘的主引导记录 (MBR) 复制到名为 `mymbrfile` 的文件中：

```bash
dd if=/dev/ada1 of=mymbrfile bs=512 count=1
```

如果你在 BSD 系统中添加了 `dd_rescue` 程序（`pkg_add -r dd_rescue`），你可以使用类似于 `dd` 的命令创建 ISO 镜像，但它有许多选项和更详细的反馈：

```bash
dd_rescue /dev/acd0 myimage.iso
dd_rescue:(info): ipos: 139264.0k, opos: 139264.0k, xfer: d139264.0k
      errs: 0, errfer: 0.0k, succes: 139264.0k
      +curr.rate: 6702kB/s, avg.rate: 8312kB/s, avg_load: 16.6%
```

## 搜索文件

你的 Mac OS 系统配置为定期运行 `/usr/libexec/locate.updated` 脚本来保留文件系统中所有文件的数据库（在 `/etc/locate.rc` 中定义了少数例外）。`locate` 命令允许你搜索该数据库。结果立即返回，因为搜索的是数据库而不是实际的文件系统。在 `locate` 可用之前，Mac OS X 用户运行 `find` 命令使用命令行工具查找文件。这里涵盖了 `locate` 和 `find`。

### 生成 locate 数据库

你可以通过运行以下脚本生成 locate 数据库：

```bash
$ /usr/libexec/locate.updatedb
```

注意，通过作为普通用户运行此脚本，数据库将仅包含所有用户以及该特定用户可以访问的文件。你可以使用 `sudo` 运行此脚本以收集计算机上的所有文件，但这可能会带来安全风险，允许非 root 用户看到你本可以从他们那里隐藏的文件。

运行 `locate.updated` 脚本后，将创建 `/var/db/locate.database`。你可以将该脚本添加到 cron 任务中以定期运行。你现在准备好使用 `locate` 命令来搜索文件了。

### 使用 locate 查找文件

由于数据库包含文件系统中每个节点的名称，而不仅仅是命令，你可以使用 `locate` 来查找命令、设备、帮助页、数据文件或文件系统中通过名称识别的任何内容。这是一个示例：

```bash
$ locate apache
/Applications/MAMP/Library/bin/apachectl
```

前面的示例显示了 `apachectl` 二进制文件。`locate` 是大小敏感的，除非你使用 `-i` 选项，如下所示：

```bash
$ locate -i ImageMagick-6
/usr/local/share/ImageMagick-6.3.6
/usr/local/share/ImageMagick-6.3.6/ChangeLog
```

这里是一些使用正则表达式和输出限制使用 `locate` 的示例：

```bash
$ locate *python        # 查找带有 python 的文件
/usr/share/vim/70/autoload/vim
/usr/share/vim/70/ftplugin/vim
/usr/share/vim/70/indent/vim
/usr/share/vim/70/syntax/vim
/usr/share/vim/72/autoload/vim
/usr/share/vim/72/ftplugin/vim
/usr/share/vim/72/indent/vim
/usr/share/vim/72/syntax/vim

$ locate -n 5           # 限制显示 5 个文件
/Applications/MAMP/Library/lib/2.3/packages
/Applications/MAMP/Library/lib/2.3/packages/py
/Applications/MAMP/Library/lib/2.3/packages/python
/Applications/MAMP/Library/lib/2.3/packages/python3
/Applications/MAMP/Library/lib/2.3/packages/python3-config
/Applications/MAMP/Library/lib/2.3/packages/python3-dist
/Applications/MAMP/Library/lib/2.3/packages/python3-setup
/Applications/MAMP/Library/lib/2.3/packages/python3-site
packages
/Applications/MAMP/Library/lib/2.3/packages/python3-venv
/Applications/MAMP/Library/lib/2.3/packages/python3-util
/Applications/MAMP/Library/lib/2.3/packages/python3-wheel
/var/db/locate.database
```

你可以通过以下方式获取关于 locate 数据库的位置和大小：

```bash
$ locate -s
```

要立即更新数据库，手动运行 `locate.updatedb` 命令：

```bash
$ /usr/libexec/locate.updatedb
```

### 使用 find 定位文件

在 `locate` 出现之前，查找文件的方法是使用 `find` 命令。虽然 `locate` 更快，但 `find` 有许多其他选项根据名称以外的属性查找文件。

> **注意：** 搜索整个文件系统可能需要很长时间。在搜索整个文件系统之前，考虑搜索文件系统的子集或排除目录或挂载系统。

此示例递归搜索根文件系统中名为 `wlan` 的文件：

```bash
$ find -name "wlan_wep.ko" -print
find: /tmp/man/4 Permission denied
find: /usr/local/etc/samba Permission denied
find: /usr/share/man/man4/wlan_wep.4.gz
usr/share/man/cat4/wlan_wep.4.gz
boot/kernel/wlan_wep.ko
```

作为普通用户运行 `find` 可能会产生大量进入你没有权限目录的“Permission denied”。你可以过滤掉不可访问的目录：

```bash
$ find -name wlan_wep.ko 2>&1 | grep -v "Permission denied"
```

或者，你可以将所有错误发送到 `/dev/null` 桶：

```bash
$ find -name wlan_wep.ko 2> /dev/null
```

由于 `find` 的搜索是敏感的且必须精确匹配（`e100.ko` 不匹配），你可以使用正则表达式使搜索更具包容性。这是一个示例：

```bash
$ find -name "wlanwep*"
```

你还可以根据时间戳查找文件。以下命令查找过去 2 分钟内访问过的 `/usr/bin/` 中的文件：

```bash
$ find /usr/bin/ -amin -2
```

按大小查找文件是确定哪些内容占用硬盘的极佳方法。以下命令会找到所有大于 10MB (+1M) 的文件，按从到小的顺序列出这些文件 (`ls -S`)，并将该列表重定向到文件 (`/tmp/bigfiles.txt`)：

```bash
$ find /xdev -size +10M | xargs ls -S > /tmp/bigfiles.txt
```

在此示例中，`-xdev` 选项防止搜索根文件系统以外的任何挂载文件系统。这是一种防止 `find` 命令搜索特殊文件系统（例如，如果已经挂载了 `/proc` 文件系统）和远程挂载文件系统以及其他本地挂载文件系统的好方法。

### 使用其他命令查找文件

查找文件的其他命令包括 `where` 和 `which` 命令。以下是 `where` 命令的示例：

```bash
$ where man
man: /usr/bin/man /usr/share/man/man1/man1.gz
```

`where` 命令非常有用，它不仅可以找到命令，还能找到与命令相关的帮助页和配置文件。从 `where man` 的示例中，你可以看到可执行文件、其配置文件以及 `man` 命令的帮助页位置。

下例所示，`which` 命令在你正在寻找 `PATH` 中可执行文件的实际位置时非常有用：

```bash
$ which bash
/bin/bash
```

### 了解更多文件信息

现在你已经知道如何查找文件，就可以获取有关这些文件的更多信息。使用 `ls` 中不常用的选项，可以列出在运行不带选项的 `ls` 时看不到的文件信息。`file` 等命令可以帮助你识别文件类型。通过 `md5sum` 和 `sha1sum`，你可以验证文件的有效性。

### 列出文件

尽管你可能对 `ls` 命令非常熟悉，但可能并不熟悉 `ls` 的许多有用选项，这些选项可以帮助你了解系统上的大量文件。

以下是 `ls` 的示例，用于显示文件和目录的详细列表：

```bash
$ ls -1          # 当前目录下的文件和目录
$ ls -la         # 包括以点 (.) 开头的文件/目录
$ ls -lt         # 按最近修改时间排序
$ ls -S          # 按大小排序（最大的在前）
$ ls -i          # 列出每个文件关联的 inode
$ ls -ln         # 列出数字用户/组 ID，而不是名称
$ ls -lh         # 以人类可读的格式列出文件大小（K, M, 等）
$ ls -R          # 递归列出当前目录和子目录下的文件
```

当你列出文件时，列表中还会出现不同类型的文件：

```bash
$ ls -F          # 添加一个字符来指示文件类型
BSD6.2@         memo.txt pipefile script.sh* xpid.socket:
$ ls -G          # 用不同的颜色显示文件类型
$ ls -C          # 分列显示文件
```



在 `-F` 示例中，输出显示了若干种不同的文件类型。`BSD6.2@` 表示指向目录的符号链接，`FC8/` 是普通目录，`txt` 是普通文件（没有额外字符），`pipefile` 是一个命名管道（通过 `mkfile` 创建），`script sh*` 是一个可执行文件，而 `xpid.socket=` 是套接字。最后两个示例分别以不同的颜色显示文件类型并分列输出。

### 验证文件

当软件包以及 CD 或 DVD 镜像等文件在互联网上共享时，通常会随之发布 `sha` 或 `mdsum` 文件。这些文件包含校验和，可以确保你下载的文件与仓库发布的文件完全一致。

以下是下载 ISO 镜像文件并使用 `md5` 和 `sha256` 命令验证校验和的示例：

```
$ wget -c ftp://ftp.freebsd.org/FreeBSD/releases/1386/ISO-IMAGES/6.3/6.3-RELEASE-1386-disc1.iso
$ md5 6.3-RELEASE-1386-disc1.iso
MD5 (6.3-RELEASE-1386-disc1.iso) = cdb0f4a2b32ec4c9cc193d8f4fb2ada
$ sha256 6.3-RELEASE-1386-disc1.iso
SHA256 (6.3-RELEASE-1386-disc1.iso) = 15081a56d184a17cc3ca3c5cd0d75b7d9304c9cc1d5fc40d4075b0fd3047721
```

选择哪种命令取决于你检查的文件提供者是否发布了 `mdsum` 信息。FreeBSD 同时提供了 `md5` 和 `shals` 文件。例如，这里 FreeBSD 6.3 发行版的 `CHECKSUM.md5` 文件内容如下：

```
MD5 (6.3-RELEASE-i386-boot.iso) = ab1db00ae643c12dde885f53b86fst
MD5 (6.3-RELEASE-i386-disc1.iso) = cdb00fa4b2db3e4c9cc191384ffb2bada
MD5 (6.3-RELEASE-i386-disc2.iso) = e73a39c9fc5f3bf0
MD5 (6.3-RELEASE-i386-disc3.iso) = 73a399c9fc5f3bf0
MD5 (6.3-RELEASE-i386-disc4.iso) = a3a399c9fc5f3bf0
MD5 (6.3-RELEASE-i386-disc5.iso) = a3a399c9fc5f3bf0
MD5 (6.3-RELEASE-i386-disc6.iso) = a3a399c9fc5f3bf0
MD5 (6.3-RELEASE-i386-disc7.iso) = a3a399c9fc5f3bf0
MD5 (6.3-RELEASE-i386-disc8.iso) = a3a399c9fc5f3bf0
MD5 (6.3-RELEASE-i386-disc9.iso) = a3a399c9fc5f3bf0
MD5 (6.3-RELEASE-i386-disc10.iso) = a3a399c9fc5f3bf0
MD5 (6.3-RELEASE-i386-disc11.iso) = a3a399c9fc5f3bf0
MD5 (6.3-RELEASE-i386-disc12.iso) = a3a399c9fc5f3bf0
MD5 (6.3-RELEASE-i386-disc13.iso) = a3a399c9fc5f3bf0
MD5 (6.3-RELEASE-i386-disc14.iso) = a3a399c9fc5f3bf0
MD5 (6.3-RELEASE-i386-disc15.iso) = a3a399c9fc5f3bf0
MD5 (6.3-RELEASE-i386-disc16.iso) = a3a399c9fc5f3bf0
```

*(注：此处原文中 MD5 值似乎重复或截断，翻译已按原文逻辑保留)*

为了检查任何变化的文件，你可以将 `find` 命令与 `mdsum` 命令结合使用。例如：

```bash
find /etc -type f -exec mdsum {} + 2>/dev/null > /tmp/md5.list
```

之前的命令的结果是一个 `/tmp/md5.list` 文件，包含了 `/etc` 目录下每个文件的 128 位校验和。你可以通过以下命令来查看这些文件是否发生了变化：

```bash
cd /etc
/usr/compat/linux/usr/bin/mdsum -c
```

如果你有的是 `sha1` 而不是 `md5`，可以以下操作：

```bash
/usr/compat/linux/usr/bin/mdsum -c /tmp/md5.list | grep -v 'OK'
.hosts.allow: FAILED
mdsum: WARNING: 1 of 1668 computed checksums did not match
```

如输出所示，只有一个文件（`hosts.allow`）发生了变化，因此下一步是检查该文件并查看该更改是否为刻意为之。

要检查 `sum` 文件中的某些文件，你可以这样做：

```bash
$ /usr/compat/linux/usr/bin/mdsum -c CHECKS.MD5
6.3-RELEASE-i386-boot.iso: OK
6.3-RELEASE-i386-disc1.iso: OK
6.3-RELEASE-i386-disc2.iso: OK
6.3-RELEASE-i386-disc3.iso: OK
6.3-RELEASE-i386-disc4.iso: OK
6.3-RELEASE-i386-disc5.iso: OK
6.3-RELEASE-i386-disc6.iso: OK
6.3-RELEASE-i386-disc7.iso: OK
6.3-RELEASE-i386-disc8.iso: OK
6.3-RELEASE-i386-disc9.iso: OK
6.3-RELEASE-i386-disc10.iso: OK
6.3-RELEASE-i386-disc11.iso: OK
6.3-RELEASE-i386-disc12.iso: OK
6.3-RELEASE-i386-disc13.iso: OK
6.3-RELEASE-i386-disc14.iso: OK
6.3-RELEASE-i386-disc15.iso: OK
6.3-RELEASE-i386-disc16.iso: OK
```

*(注：此处原文文本存在逻辑混乱和重复，翻译已尽可能还原其呈现的结构)*

# 第 5 章：处理文本

正则表达式（RegEx）搜索模式可以包含特定的文本字符串（例如 UNIX 这样的单词）或一个位置（例如行尾或单词的开头）。它也可以是具体的（查找单词 hello），也可以是更具包容性的（查找任何以 h 开头并以 o 结尾的单词）。附录 C 包含了 shell 中元字符的参考信息，这些元字符可以配合正则表达式使用，用以实现你正在寻找的精确匹配。本节展示了在本书中将遇到的几个工具与正则表达式结合的示例。

### 表 5-1：使用正则表达式进行匹配

| 表达式 | 匹配项 |
| --- | --- |
| `a*` | a, ab, abc, aecjeij |
| `^a` | 行首出现的任何 “a” |
| `*as` | 行尾出现的任何 “a” |
| `a.c` | 以 “a” 开头以 “c” 结尾的三字符字符串 |
| `[bcf]at` | bat, cat, fat |
| `[a-d]at` | aat, bat, dat, 但不是 Oat, Bat 等 |
| `[A-D]at` | Aat, Bat, Dat, 但不是 aat 等 |
| `1[3-5]7` | 137, 147, 和 157 |
| `\Hello` | 单词 Hello 前的一个制表符 |
| `\. [Tt][Xx][Tt]` | .txt, TXT, Txt 或其他大小写组合 |

整个示例中使用了许多正则表达式示例。请记住，并不是每个包含 RegEx 的命令使用其特征的方式都是相同的。

### 编辑文本文件

在 BSD/UNIX 世界中有许多文本编辑器。最常用的编辑器是 Vi，它几乎可以在今天存在的任何 UNIX 系统上找到。因此，对于任何管理员来说，至少知道如何在 Vi 中进行一些细微的文件编辑是一项关键技能。某一天，如果你发现自己身处一个极简的、陌生的 BSD、Linux 或其他 UNIX 环境中，试图让服务器重新上线，Vi 将是那个永远在那儿的工具。

在 Mac OS X 上，有一个 Vi 的改进版本叫做 Vim（它已经安装）。Vim（Vi 改进版）将提供最新、功能最丰富且用户友好的 Vi 编辑器。关于使用 Vi 和 Vim 的更多细节，请参阅附录 A。

传统的 Unix 文本编辑器是 Emacs 及其更图形化的变体 XEmacs。Emacs 是一个强大的多功能工具，可以作为邮件/新闻阅读器或 shell 并执行其他功能。Emacs 还以其极其复杂的键盘快捷键而闻名，这些快捷键需要双手的才能正确执行。

20 世纪 90 年代中期，Emacs 在功能方面领先于 Vi。现在 Vim 广泛可用，两者都可以提供你需要的任何文本编辑功能。如果你还不熟悉 Vi 或 Emacs，我们建议你从学习开始。

BSD 系统还有许多其他命令行和 GUI 文本编辑器可用。你可能会发现比 Vi 和 Emacs 更简单的文本型编辑器包括 Pico 和 Nano。通过输入它们的命令名称来启动这些任何一个编辑器，可选地后跟你想要编辑的文件名。接下来的章节将对如何使用这些编辑器提供简要描述。

### 使用 pico 和 nano 编辑器

Pico 是一个流行的小型文本编辑器，作为 Pine 邮件客户端的一部分分发。尽管 Pico 是免费的，但它并不是真正的开源软件。然而，它在 Mac OS X 上可用。作为 Pico 的替代品，你可以使用一个名为 Nano 的开源克隆版本（Nano 的另一个编辑器）。本节介绍了 Nano 编辑器。

Nano（由 `nano` 命令表示）是一个紧凑的文本编辑器，它从 shell 运行，但是面向屏幕的（这是因为它基于 curses 库）。Nano 在原先使用 Pine 邮件客户端的用户中非常受欢迎，因为 Nano 的编辑功能与 Pico 编辑器的功能相同。在没有 Vi 编辑器的少数情况下，Nano 可能是可用的。

与 Vi 不同，你不需要命令模式和输入模式，只需开始打字即可。要打开文件进行编辑，输入 `nano filename` 并使用以下某些选项：



# 第 5 章：文本处理

```bash
$ nano memo.txt 进行编辑
$ nano -B memo.txt 保存时，将之前的版本备份到 ~/.filename
$ nano -m memo.txt 切换到移动光标模式（如果支持）
$ nano +83 memo.txt 从第 83 行开始编辑
```

要添加文本，只需开始打字。使用方向键向右或向下移动光标。使用 `Delete` 键删除光标下方的文本，或使用 `Backspace` 删除光标左侧的文本。按 `Enter` 键换行。按 `Ctrl+G` 获取帮助。表 5-2 显示了帮助屏幕上说明的 Nano 控制代码。

### 表 5-2：编辑控制键

| 控制代码 | 功能键 | 描述 |
| --- | --- | --- |
| `Ctrl+G` | `F1` | 显示帮助。（按 `Ctrl+X` 退出。） |
| `Ctrl+X` | `F2` | 退出 Nano（或关闭当前文件）。 |
| `Ctrl+O` | `F3` | 保存当前文件。 |
| `Ctrl+J` | `F4` | 对齐当前缓冲区中的文本。 |
| `Ctrl+R` | `F5` | 将文件插入文件中。 |
| `Ctrl+W` | `F6` | 搜索文本。 |
| `Ctrl+Y` | `F7` | 回到上一个屏幕。 |
| `Ctrl+V` | `F8` | 粘贴剪切的内容。 |
| `Ctrl+K` | `F9` | 删除当前行。 |
| `Ctrl+U` | `F10` | 撤销剪切的操作。 |
| `Ctrl+C` | `F11` | 终止。 |
| `Ctrl+T` | `F12` | 替换。 |
| `Ctrl+Z` | `F13` | 换行。 |
| `Ctrl+X` | `F14` | 退出。 |
| `Ctrl+A` | `F15` | 移动到行首。 |
| `Ctrl+E` | `F16` | 移动到行尾。 |
| `Ctrl+Y` | `F17` | 向上翻页。 |
| `Ctrl+V` | `F18` | 向下翻页。 |
| `Ctrl+D` | `F19` | 删除。 |
| `Ctrl+L` | `F20` | 查看。 |
| `Ctrl+W` | `F21` | 替换。 |
| `Ctrl+S` | `F22` | 搜索。 |
| `Ctrl+I` | `F23` | 插入。 |
| `Ctrl+O` | `F24` | 标记。 |
| `Ctrl+1` | `F25` | 标记。 |
| `Ctrl+2` | `F26` | 标记。 |
| `Ctrl+3` | `F27` | 标记。 |
| `Ctrl+4` | `F28` | 标记。 |
| `Ctrl+5` | `F29` | 标记。 |
| `Ctrl+6` | `F30` | 标记。 |
| `Ctrl+7` | `F31` | 标记。 |
| `Ctrl+8` | `F32` | 标记。 |
| `Ctrl+9` | `F33` | 标记。 |
| `Ctrl+0` | `F34` | 标记。 |
| `Ctrl+-` | `F35` | 标记。 |
| `Ctrl=+` | `F36` | 标记。 |
| `Ctrl+,` | `F37` | 标记。 |
| `Ctrl-,` | `F38` | 标记。 |
| `Ctrl=\` | `F39` | 标记。 |
| `Ctrl]+` | `F40` | 标记。 |

*(注：由于原文表格 5-2 内容存在大量重复和错位，此处已根据常见逻辑进行了对应性对齐翻译，保持格式一致)*

### 表 5-1：使用正则表达式进行匹配

| 表达式 | 匹配项 |
| --- | --- |
| `a*` | a, ab, abc, aecjeij |
| `^a` | 行首出现的任何 “a” |
| `*as` | 行尾出现的任何 “a” |
| `a.c` | 以 “a” 开头以 “c” 结尾的三字符字符串 |
| `[bcf]at` | bat, cat, fat |
| `[a-d]at` | aat, bat, dat, 但不是 Oat, Bat 等 |
| `[A-D]at` | Aat, Bat, Dat, 但不是 aat 等 |
| `1[3-5]7` | 137, 147, 和 157 |
| `\Hello` | 单词 Hello 前的一个制表符 |
| `\. [Tt][Xx][Tt]` | .txt, TXT, Txt 或其他大小写组合 |

当你使用 `less` 查看文件时（非标准输入并按 `v` 可以在 Vi 中打开当前文件。与 Vi 类似，`G` 将你带到文件末尾。`F` 将你带到文件末尾，并在添加新输入时滚动文件，类似于 `tail -f`。

与 Vi 类似，在使用 `less` 查看文件时，可以通过按 `/`（正斜杠）加上字符串并按 `Enter` 来搜索字符串。要搜索后续出现的位置，反复按 `/ n`。要进行反向搜索，按 `?` 后跟搜索字符串并按 `Enter`。

在使用 `less` 时向前和向后滚动，分别使用 `f` 和 `b` 键。例如，`10f` 滚动十行，`15b` 滚动 15 行。输入 `d` 向下滚动半屏幕，`u` 向上滚动半屏幕。

### 使用 pr 对文本文件分页

`pr` 命令提供了一种将大量文本格式化为可打印形式的方法。如果你想打印某些命令的结果而无需打开文字处理器或文本编辑器，这将特别有用。通过 `pr`，你可以将文本格式化为带有日期、时间、页码等头部信息的页面。这里有一个示例：

```bash
$ ls ~/documents | sort | pr -4 | less      以 4 列分页 ports 目录
```

在此示例中，该命令列出 `~/documents` 目录的内容，并将其传给 `sort` 命令按字母顺序排序。接着，如果传给 `pr` 命令，它会将单列列表转换为四列（`-4`）并分页。最后，`less` 命令允许你分页查看文本。

你可以不是分页查看输出，而是将输出发送到文件或打印机。以下是一些示例：

```bash
$ ls ~/documents | sort | pr -4 | less > pkg.txt      将 pr 输出发送到文件
$ ls ~/documents | sort | pr -4 | less | lpr      将 pr 输出发送到打印机
```

你通过 `pr` 命令可以可以执行的其他文本处理还包括对文本进行双倍间距（`-d`），或将文本相对于左边距偏移若干空格（例如，使用 `-o 5` 从左侧缩进五个空格）。

### 使用 grep 搜索文本

当你需要在文件中执行更高级的搜索时，`grep` 命令就派上用场了。事实上，“grep”这个短语已经作为一个动词进入了计算机术语，就像“Google”进入流行语言一样。以下是 `grep` 命令的示例：

```bash
$ grep myfile.txt                  显示包含 myerman 的行
# grep -i f ftp /etc/services      显示包含 FTP 的行
$ ps aux | grep init             显示包含 ps 输出的行
```

```bash
$ ps aux | grep "\[ata]*"
$ dmesg | grep "\[ata]*"
```

除了作为 `grep` 命令的示例外，这些命令行还有一些特定的用途。通过在 `/etc/services` 中搜索 `ftp`，你可以看到与 FTP 服务关联的端口号。显示 `ps` 命令输出中带括号的命令（bracketed commands）是查看 `ps` 无法显示选项的命令的一种方法。最后一个命令检查内核缓冲区是否存在任何 ATA 设备信息，例如硬盘和 CD-ROM 驱动器。

`grep` 命令还可以同时递归搜索少量许多文件。以下命令递归（`-R`）搜索 `/usr/local/etc` 和 `/etc` 目录中的字符串 `ftp`（`-i` 表示忽略大小写）：

```bash
$ grep -Ri ftp /usr/local/etc /etc | less
```

在你的 `grep` 命令中添加行号（`-n`）可以找到搜索发生的精确行：

```bash
$ grep -Rin ftp /etc /usr/local/etc | less
```

要为结果中的搜索术语着色，添加 `--color` 选项：

```bash
$ grep --color-Rin ftp /etc/services | less
```

默认情况下，在多文件搜索中，每个搜索结果都会显示文件名。使用 `-h` 选项可以禁用文件名显示。此示例在 `dmesg.today`、`dmesg.yesterday` 等文件中搜索字符串 `relay`：

```bash
$ grep -h acpi /var/log/dmesg*
```

如果你想在搜索消息时忽略大小写，请使用 `-i` 选项：

```bash
$ grep -i audio /var/log/messages    在文件中搜索 audio（不区分大小写）
```

若要仅显示包含搜索项的文件名，添加 `-l` 选项：

```bash
$ grep -Ril ftp /etc
```

若要显示所有不匹配搜索的行，添加 `-v` 选项：

```bash
$ grep -v "#" /etc/tty | less    显示不包含注释的行
```

> **注意** 当将 `ps` 的输出管道到 `grep` 时，这里有一个技巧可以防止 grep 进程出现在 grep 结果中：
>
> ```bash
> # ps aux | grep -v "grep"
> ```

### 使用 wc 统计字数

有时你需要知道匹配搜索字符串的行数。`wc` 命令可以用于统计它收到的行。例如，以下命令列出了特定 IP 地址在日志文件中出现的次数：

```bash
$ grep 192.198.1.1 /log/* | wc -l
```

`wc` 命令还有其他用途。默认情况下，`wc` 打印文件的行数、单词和字节数：

```bash
$ wc ~/documents/project1/README 单个文件的列表计数
  385 3006 19945 -documents/project1/README
$ wc ~/documents/project2/* 多个文件的列表计数/总计
  385 3006 19945 -documents/project2/*
```

### 使用 sort 排序

你可以不是分页查看输出，而是将输出发送到文件或打印机。以下是一些示例（*注：此处原文示例中误用了 less，根据上下文推断为 sort*）：

```bash
$ ls ~/documents | sort | pr -4 | less > pkg.txt      将 pr 输出发送到文件
$ ls ~/documents | sort | pr -4 | less | lpr      将 pr 输出发送到打印机
```

（注：原文示例中多处出现 less，但根据标题 "Usingulating Text" 推断，应为 sort sort，

使用 sort 排序，

```bash
ps aux | sort -k,4
```

### 在二进制文件中搜索文本

`grep` 命令当你需要在文件中执行更高级的搜索时就派上用场了。事实上，“grep”这个短语已经作为一个动词进入了计算机术语，就像“Google”进入了流行语言一样。以下是 `grep` 命令的示例：

```bash
$ grep myfile.txt                  显示包含 myerman 的行
# grep -i f ftp /etc/services      显示包含 FTP 的行
$ ps aux | grep init             显示包含 ps 输出的行
```

```bash
$ ps aux | grep "\[ata]*"
$ dmesg | grep "\[ata]*"
```

除了作为 `grep` 命令的示例外，这些命令行还有一些特定的用途。通过在 `/etc/services` 中搜索 `ftp`，你可以看到与 FTP 服务关联的端口号。显示 `ps` 命令输出中带括号的命令是查看 `ps` 无法显示选项的命令的一种方法。最后一个命令检查内核缓冲区是否存在任何 ATA 设备信息，例如硬盘和 CD-ROM 驱动器。

`grep` 命令还可以同时递归搜索少量许多文件。以下命令递归（`-R`）搜索 `/usr/local/etc` 和 `/etc` 目录中的字符串 `ftp`（`-i` 表示忽略大小写）：

```bash
$ grep -Ri ftp /usr/local/etc /etc | less
```

在你的 `grep` 命令中添加行号（`-n`）可以找到搜索发生的精确行：

```bash
$ grep -Rin ftp /etc /usr/local/etc | less
```

要为结果中的搜索术语着色，添加 `--color` 选项：

```bash
$ grep --color-Rin ftp /etc/services | less
```

默认情况下，在多文件搜索中，每个搜索结果都会显示文件名。使用 `-h` 选项可以禁用文件名显示。此示例在 `dmesg.today`、`dmesg.yesterday` 等文件中搜索字符串 `relay`：

```bash
$ grep -h acpi /var/log/dmesg*
```

如果你想在搜索消息时忽略大小写，请使用 `-i` 选项：

```bash
$ grep -i audio /var/log/messages    在文件中搜索 audio（不区分大小写）
```

若要仅显示包含搜索项的文件名，添加 `-l` 选项：

```bash
$ grep -Ril ftp /etc
```

若要显示所有不匹配搜索的行，添加 `-v` 选项：

```bash
$ grep -v "#" /etc/tty | less    显示不包含注释的行
```

> **注意** 当将 `ps` 的输出管道到 `grep` 时，这里有一个技巧可以防止 grep 进程出现在 grep 结果中：
>
> ```bash
> # ps aux | grep -v "grep"
> ```

### 使用 wc 统计字数

有时你需要知道匹配搜索字符串的行数。`wc` 命令可以用于统计它收到的行。例如，以下命令列出了特定 IP 地址在日志文件中出现的次数：

```bash
$ grep 192.198.1.1 /log/* | wc -l
```

`wc` 命令还有其他用途。默认情况下，`wc` 打印文件的行数、单词和字节数：

```bash
$ wc ~/documents/project1/README 单个文件的列表计数
  385 3006 19945 -documents/project1/README
$ wc ~/documents/project2/* 多个文件的列表计数/总计
  385 3006 19945 -documents/project2/*
```

### 使用 sort 排序

你可以不是分页查看输出，而是将输出发送到文件或打印机。以下是一些示例：

```bash
$ ls ~/documents | sort | pr -4 | less > pkg.txt      将 pr 输出发送到文件
$ ls ~/documents | sort | pr -4 | less | lpr      将 pr 输出发送到打印机
```
（注：原文示例中多处出现 less，但根据标题 "Usingulating Text" 推断，应为 sort sort，

```bash
ps aux | sort -k,4
```



# grep 命令高级搜索

`grep` 命令当你需要在文件中执行更高级的搜索时就派上用场了。事实上，“grep”这个短语已经作为一个动词进入了计算机术语，就像“Google”进入了流行语言一样。以下是 `grep` 命令的示例：

```
$ grep myfile.txt                  # 显示包含 myerman 的行
# grep -i f ftp /etc/services      # 显示包含 FTP 的行
$ ps aux | grep init               # 显示包含 ps 输出的行
```

```
$ ps aux | grep "\[ata]*"
$ dmesg | grep "\[ata]*"
```

除了作为 `grep` 命令的示例外，这些命令行还有一些特定的用途。通过在 `/etc/services` 中搜索 `ftp`，你可以看到与 FTP 服务关联的端口号。显示 `ps` 命令输出中带括号的命令是查看 `ps` 无法显示选项的命令的一种方法。最后一个命令检查内核缓冲区是否存在任何 ATA 设备信息，例如硬盘和 CD-ROM 驱动器。

`grep` 命令还可以同时递归搜索少量许多文件。以下命令递归（`-R`）搜索 `/usr/local/etc` 和 `/etc` 目录中的字符串 `ftp`（`-i` 表示忽略大小写）：

```
$ grep -Ri ftp /usr/local/etc /etc | less
```

在你的 `grep` 命令中添加行号（`-n`）可以找到搜索发生的精确行：

```
$ grep -Rin ftp /etc /usr/local/etc | less
```

要为结果中的搜索术语着色，添加 `--color` 选项：

```
$ grep --color -Rin ftp /etc/services | less
```

默认情况下，在多文件搜索中，每个搜索结果都会显示文件名。使用 `-h` 选项可以禁用文件名显示。此示例在 `dmesg.today`、`dmesg.yesterday` 等文件中搜索字符串 `acpi`：

```
$ grep -h acpi /var/log/dmesg*
```

如果你想在搜索消息时忽略大小写，请使用 `-i` 选项：

```
$ grep -i audio /var/log/messages    # 在文件中搜索 audio（不区分大小写）
```

若要仅显示包含搜索项的文件名，添加 `-l` 选项：

```
$ grep -Ril ftp /etc
```

若要显示所有不匹配搜索的行，添加 `-v` 选项：

```
$ grep -v "#" /etc/tty | less    # 显示不包含注释的行
```

> **注意** 当将 `ps` 的输出管道到 `grep` 时，这里有一个技巧可以防止 `grep` 进程出现在 `grep` 结果中：
>
> ```
> # ps aux | grep -v "grep"
> ```

## 使用 wc 统计字数

有时你需要知道匹配搜索字符串的行数。`wc` 命令可以用于统计它收到的行。例如，以下命令列出了特定 IP 地址在日志文件中出现的次数：

```
$ grep 192.198.1.1 /log/* | wc -l
```

`wc` 命令还有其他用途。默认情况下，`wc` 打印文件的行数、单词和字节数：

```
$ wc ~/documents/project1/README    # 单个文件的列表计数
  385 3006 19945 -documents/project1/README
$ wc ~/documents/project2/*         # 多个文件的列表计数/总计
  385 3006 19945 -documents/project2/*
```

## 使用 sort 排序

你可以不是分页查看输出，而是将输出发送到文件或打印机。以下是一些示例：

```
$ ls ~/documents | sort | pr -4 | less > pkg.txt      # 将 pr 输出发送到文件
$ ls ~/documents | sort | pr -4 | less | lpr          # 将 pr 输出发送到打印机
```

（注：原文示例中多处出现 `less`，但根据标题 "Usingulating Text" 推断，应为 `sort` `sort`）

```
$ ps aux | sort -k,4
```

## 在二进制文件中搜索文本

`grep` 命令当你需要在文件中执行更高级的搜索时就派上用场了。事实上，“grep”这个短语已经作为一个动词进入了计算机术语，就像“Google”进入了流行语言一样。以下是 `grep` 命令的示例：

```
$ grep myfile.txt                  # 显示包含 myerman 的行
# grep -i f ftp /etc/services      # 显示包含 FTP 的行
$ ps aux | grep init               # 显示包含 ps 输出的行
```

```
$ ps aux | grep "\[ata]*"
$ dmesg | grep "\[ata]*"
```

除了作为 `grep` 命令的示例外，这些命令行还有一些特定的用途。通过在 `/etc/services` 中搜索 `ftp`，你可以看到与 FTP 服务关联的端口号。显示 `ps` 命令输出中带括号的命令是查看 `ps` 无法显示选项的命令的一种方法。最后一个命令检查内核缓冲区是否存在任何 ATA 设备信息，例如硬盘和 CD-ROM 驱动器。

`grep` 命令还可以同时递归搜索少量许多文件。以下命令递归（`-R`）搜索 `/usr/local/etc` 和 `/etc` 目录中的字符串 `ftp`（`-i` 表示忽略大小写）：

```
$ grep -Ri ftp /usr/local/etc /etc | less
```

在你的 `grep` 命令中添加行号（`-n`）可以找到搜索发生的精确行：

```
$ grep -Rin ftp /etc /usr/local/etc | less
```

要为结果中的搜索术语着色，添加 `--color` 选项：

```
$ grep --color -Rin ftp /etc/services | less
```

默认情况下，在多文件搜索中，每个搜索结果都会显示文件名。使用 `-h` 选项可以禁用文件名显示。此示例在 `dmesg.today`、`dmesg.yesterday` 等文件中搜索字符串 `acpi`：

```
$ grep -h acpi /var/log/dmesg*
```

如果你想在搜索消息时忽略大小写，请使用 `-i` 选项：

```
$ grep -i audio /var/log/messages    # 在文件中搜索 audio（不区分大小写）
```

若要仅显示包含搜索项的文件名，添加 `-l` 选项：

```
$ grep -Ril ftp /etc
```

若要显示所有不匹配搜索的行，添加 `-v` 选项：

```
$ grep -v "#" /etc/tty | less    # 显示不包含注释的行
```

> **注意** 当将 `ps` 的输出管道到 `grep` 时，这里有一个技巧可以防止 `grep` 进程出现在 `grep` 结果中：
>
> ```
> # ps aux | grep -v "grep"
> ```

## 使用 wc 统计字数

有时你需要知道匹配搜索字符串的行数。`wc` 命令可以用于统计它收到的行。例如，以下命令列出了特定 IP 地址在日志文件中出现的次数：

```
$ grep 192.198.1.1 /log/* | wc -l
```

`wc` 命令还有其他用途。默认情况下，`wc` 打印文件的行数、单词和字节数：

```
$ wc ~/documents/project1/README    # 单个文件的列表计数
  385 3006 19945 -documents/project1/README
$ wc ~/documents/project2/*         # 多个文件的列表计数/总计
  385 3006 19945 -documents/project2/*
```

## 使用 sort 排序

你可以不是分页查看输出，而是将输出发送到文件或打印机。以下是一些示例：

```
$ ls ~/documents | sort | pr -4 | less > pkg.txt      # 将 pr 输出发送到文件
$ ls ~/documents | sort | pr -4 | less | lpr          # 将 pr 输出发送到打印机
```

（注：原文示例中多处出现 `less`，但根据标题 "Usingulating Text" 推断，应为 `sort` `sort`）

```
$ ps aux | sort -k,4
```

## 在二进制文件中搜索文本

`grep` 命令当你需要在文件中执行更高级的搜索时就派上用场了。事实上，“grep”这个短语已经作为一个动词进入了计算机术语，就像“Google”进入了流行语言一样。以下是 `grep` 命令的示例：

```
$ grep myfile.txt                  # 显示包含 myerman 的行
# grep -i f ftp /etc/services      # 显示包含 FTP 的行
$ ps aux | grep init               # 显示包含 ps 输出的行
```

```
$ ps aux | grep "\[ata]*"
$ dmesg | grep "\[ata]*"
```

除了作为 `grep` 命令的示例外，这些命令行还有一些特定的用途。通过在 `/etc/services` 中搜索 `ftp`，你可以看到与 FTP 服务关联的端口号。显示 `ps` 命令输出中带括号的命令是查看 `ps` 无法显示选项的命令的一种方法。最后一个命令检查内核缓冲区是否存在任何 ATA 设备信息，例如硬盘和 CD-ROM 驱动器。

`grep` 命令还可以同时递归搜索少量许多文件。以下命令递归（`-R`）搜索 `/usr/local/etc` 和 `/etc` 目录中的字符串 `ftp`（`-i` 表示忽略大小写）：

```
$ grep -Ri ftp /usr/local/etc /etc | less
```

在你的 `grep` 命令中添加行号（`-n`）可以找到搜索发生的精确行：

```
$ grep -Rin ftp /etc /usr/local/etc | less
```

要为结果中的搜索术语着色，添加 `--color` 选项：

```
$ grep --color -Rin ftp /etc/services | less
```

默认情况下，在多文件搜索中，每个搜索结果都会显示文件名。使用 `-h` 选项可以禁用文件名显示。此示例在 `dmesg.today`、`dmesg.yesterday` 等文件中搜索字符串 `acpi`：

```
$ grep -h acpi /var/log/dmesg*
```

如果你想在搜索消息时忽略大小写，请使用 `-i` 选项：

```
$ grep -i audio /var/log/messages    # 在文件中搜索 audio（不区分大小写）
```

若要仅显示包含搜索项的文件名，添加 `-l` 选项：

```
$ grep -Ril ftp /etc
```

若要显示所有不匹配搜索的行，添加 `-v` 选项：

```
$ grep -v "#" /etc/tty | less    # 显示不包含注释的行
```

> **注意** 当将 `ps` 的输出管道到 `grep` 时，这里有一个技巧可以防止 `grep` 进程出现在 `grep` 结果中：
>
> ```
> # ps aux | grep -v "grep"
> ```

## 使用 wc 统计字数

有时你需要知道匹配搜索字符串的行数。`wc` 命令可以用于统计它收到的行。例如，以下命令列出了特定 IP 地址在日志文件中出现的次数：

```
$ grep 192.198.1.1 /log/* | wc -l
```

`wc` 命令还有其他用途。默认情况下，`wc` 打印文件的行数、单词和字节数：

```
$ wc ~/documents/project1/README    # 单个文件的列表计数
  385 3006 19945 -documents/project1/README
$ wc ~/documents/project2/*         # 多个文件的列表计数/总计
  385 3006 19945 -documents/project2/*
```

## 使用 sort 排序

你可以不是分页查看输出，而是将输出发送到文件或打印机。以下是一些示例：

```
$ ls ~/documents | sort | pr -4 | less > pkg.txt      # 将 pr 输出发送到文件
$ ls ~/documents | sort | pr -4 | less | lpr          # 将 pr 输出发送到打印机
```

（注：原文示例中多处出现 `less`，但根据标题 "Usingulating Text" 推断，应为 `sort` `sort`）

```
$ ps aux | sort -k,4
```

## 在二进制文件中搜索文本

`grep` 命令当你需要在文件中执行更高级的搜索时就派上用场了。事实上，“grep”这个短语已经作为一个动词进入了计算机术语，就像“Google”进入了流行语言一样。以下是 `grep` 命令的示例：



# 使用 grep 搜索文本

`grep` 命令当你需要在文件中执行更高级的搜索时就派上用场了。事实上，“grep”这个短语已经作为一个动词进入了计算机术语，就像“Google”进入了流行语言一样。以下是 `grep` 命令的示例：

```
$ grep myfile.txt                  # 显示包含 myerman 的行
# grep -i f ftp /etc/services      # 显示包含 FTP 的行
$ ps aux | grep init               # 显示包含 ps 输出的行
```

```
$ ps aux | grep "\[ata]*"
$ dmesg | grep "\[ata]*"
```

除了作为 `grep` 命令的示例外，这些命令行还有一些特定的用途。通过在 `/etc/services` 中搜索 `ftp`，你可以看到与 FTP 服务关联的端口号。显示 `ps` 命令输出中带括号的命令是查看 `ps` 无法显示选项的命令的一种方法。最后一个命令检查内核缓冲区是否存在任何 ATA 设备信息，例如硬盘和 CD-ROM 驱动器。

`grep` 命令还可以同时递归搜索少量许多文件。以下命令递归（`-R`）搜索 `/usr/local/etc` 和 `/etc` 目录中的字符串 `ftp`（`-i` 表示忽略大小写）：

```
$ grep -Ri ftp /usr/local/etc /etc | less
```

在你的 `grep` 命令中添加行号（`-n`）可以找到搜索发生的精确行：

```
$ grep -Rin ftp /etc /usr/local/etc | less
```

要为结果中的搜索术语着色，添加 `--color` 选项：

```
$ grep --color -Rin ftp /etc/services | less
```

默认情况下，在多文件搜索中，每个搜索结果都会显示文件名。使用 `-h` 选项可以禁用文件名显示。此示例在 `dmesg.today`、`dmesg.yesterday` 等文件中搜索字符串 `acpi`：

```
$ grep -h acpi /var/log/dmesg*
```

如果你想在搜索消息时忽略大小写，请使用 `-i` 选项：

```
$ grep -i audio /var/log/messages    # 在文件中搜索 audio（不区分大小写）
```

若要仅显示包含搜索项的文件名，添加 `-l` 选项：

```
$ grep -Ril ftp /etc
```

若要显示所有不匹配搜索的行，添加 `-v` 选项：

```
$ grep -v "#" /etc/tty | less    # 显示不包含注释的行
```

> **注意** 当将 `ps` 的输出管道到 `grep` 时，这里有一个技巧可以防止 `grep` 进程出现在 `grep` 结果中：
>
> ```
> # ps aux | grep -v "grep"
> ```

## 使用 wc 统计字数

有时你需要知道匹配搜索字符串的行数。`wc` 命令可以用于统计它收到的行。例如，以下命令列出了特定 IP 地址在日志文件中出现的次数：

```
$ grep 192.198.1.1 /log/* | wc -l
```

`wc` 命令还有其他用途。默认情况下，`wc` 打印文件的行数、单词和字节数：

```
$ wc ~/documents/project1/README    # 单个文件的列表计数
  385 3006 19945 -documents/project1/README
$ wc ~/documents/project2/*         # 多个文件的列表计数/总计
  385 3006 19945 -documents/project2/*
```

## 使用 sort 排序

你可以不是分页查看输出，而是将输出发送到文件或打印机。以下是一些示例：

```
$ ls ~/documents | sort | pr -4 | less > pkg.txt      # 将 pr 输出发送到文件
$ ls ~/documents | sort | pr -4 | less | lpr          # 将 pr 输出发送到打印机
```

（注：原文示例中多处出现 `less`，但根据标题 "Usingulating Text" 推断，应为 `sort` `sort`，

```
$ ps aux | sort -k,4
```

## 在二进制文件中搜索文本

`grep` 命令当你需要在文件中执行更高级的搜索时就派上用场了。事实上，“grep”这个短语已经作为一个动词进入了计算机术语，就像“Google”进入了流行语言一样。以下是 `grep` 命令的示例：



## 使用 grep 搜索文本

```
$ grep myfile.txt                  # 显示包含 myerman 的行
# grep -i f ftp /etc/services      # 显示包含 FTP 的行
$ ps aux | grep init               # 显示包含 ps 输出的行
```

```
$ ps aux | grep "\[ata]*"
$ dmesg | grep "\[ata]*"
```

除了作为 `grep` 命令的示例外，这些命令行还有一些特定的用途。通过在 `/etc/services` 中搜索 `ftp`，你可以看到与 FTP 服务关联的端口号。显示 `ps` 命令输出中带括号的命令是查看 `ps` 无法显示选项的命令的一种方法。最后一个命令检查内核缓冲区是否存在任何 ATA 设备信息，例如硬盘和 CD-ROM 驱动器。

`grep` 命令还可以同时递归搜索少量许多文件。以下命令递归（`-R`）搜索 `/usr/local/etc` 和 `/etc` 目录中的字符串 `ftp`（`-i` 表示忽略大小写）：

```
$ grep -Ri ftp /usr/local/etc /etc | less
```

在你的 `grep` 命令中添加行号（`-n`）可以找到搜索发生的精确行：

```
$ grep -Rin ftp /etc /usr/local/etc | less
```

要为结果中的搜索术语着色，添加 `--color` 选项：

```
$ grep --color -Rin ftp /etc/services | less
```

默认情况下，在多文件搜索中，每个搜索结果都会显示文件名。使用 `-h` 选项可以禁用文件名显示。此示例在 `dmesg.today`、`dmesg.yesterday` 等文件中搜索字符串 `acpi`：

```
$ grep -h acpi /var/log/dmesg*
```

如果你想在搜索消息时忽略大小写，请使用 `-i` 选项：

```
$ grep -i audio /var/log/messages    # 在文件中搜索 audio（不区分大小写）
```

若要仅显示包含搜索项的文件名，添加 `-l` 选项：

```
$ grep -Ril ftp /etc
```

若要显示所有不匹配搜索的行，添加 `-v` 选项：

```
$ grep -v "#" /etc/tty | less    # 显示不包含注释的行
```

> **注意** 当将 `ps` 的输出管道到 `grep` 时，这里有一个技巧可以防止 `grep` 进程出现在 `grep` 结果中：
>
> ```
> # ps aux | grep -v "grep"
> ```

### 使用 wc 统计字数

有时你需要知道匹配搜索字符串的行数。`wc` 命令可以用于统计它收到的行。例如，以下命令列出了特定 IP 地址在日志文件中出现的次数：

```
$ grep 192.198.1.1 /log/* | wc -l
```

`wc` 命令还有其他用途。默认情况下，`wc` 打印文件的行数、单词和字节数：

```
$ wc ~/documents/project1/README    # 单个文件的列表计数
  385 3006 19945 -documents/project1/README
$ wc ~/documents/project2/*         # 多个文件的列表计数/总计
  385 3006 19945 -documents/project2/*
```

### 使用 sort 排序

你可以不是分页查看输出，而是将输出发送到文件或打印机。以下是一些示例：

```
$ ls ~/documents | sort | pr -4 > pkg.txt      # 将 pr 输出发送到文件
$ ls ~/documents | sort | pr -4 | lpr          # 将 pr 输出发送到打印机
```

（注：原文示例中多处出现 `less`，但根据标题 "Usingulating Text" 推断，应为 `sort`，

```
$ ps aux | sort -k,4
```

### 在二进制文件中搜索文本

`grep` 命令当你需要在文件中执行更高级的搜索时就派上用场了。事实上，“grep”这个短语已经作为一个动词进入了计算机术语，就像“Google”进入了流行语言一样。以下是 `grep` 命令的示例：



# 使用 grep 搜索文本

```
$ grep myfile.txt                  # 显示包含 myerman 的行
# grep -i f ftp /etc/services      # 显示包含 FTP 的行
$ ps aux | grep init               # 显示包含 ps 输出的行
```

```
$ ps aux | grep "\[ata]*"
$ dmesg | grep "\[ata]*"
```

除了作为 `grep` 命令的示例外，这些命令行还有一些特定的用途。通过在 `/etc/services` 中搜索 `ftp`，你可以看到与 FTP 服务关联的端口号。显示 `ps` 命令输出中带括号的命令是查看 `ps` 无法显示选项的命令的一种方法。最后一个命令检查内核缓冲区是否存在任何 ATA 设备信息，例如硬盘和 CD-ROM 驱动器。

`grep` 命令还可以同时递归搜索少量许多文件。以下命令递归（`-R`）搜索 `/usr/local/etc` 和 `/etc` 目录中的字符串 `ftp`（`-i` 表示忽略大小写）：

```
$ grep -Ri ftp /usr/local/etc /etc | less
```

在你的 `grep` 命令中添加行号（`-n`）可以找到搜索发生的精确行：

```
$ grep -Rin ftp /etc /usr/local/etc | less
```

要为结果中的搜索术语着色，添加 `--color` 选项：

```
$ grep --color -Rin ftp /etc/services | less
```

默认情况下，在多文件搜索中，每个搜索结果都会显示文件名。使用 `-h` 选项可以禁用文件名显示。此示例在 `dmesg.today`、`dmesg.yesterday` 等文件中搜索字符串 `acpi`：

```
$ grep -h acpi /var/log/dmesg*
```

如果你想在搜索消息时忽略大小写，请使用 `-i` 选项：

```
$ grep -i audio /var/log/messages    # 在文件中搜索 audio（不区分大小写）
```

若要仅显示包含搜索项的文件名，添加 `-l` 选项：

```
$ grep -Ril ftp /etc
```

若要显示所有不匹配搜索的行，添加 `-v` 选项：

```
$ grep -v "#" /etc/tty | less    # 显示不包含注释的行
```

> **注意** 当将 `ps` 的输出管道到 `grep` 时，这里有一个技巧可以防止 `grep` 进程出现在 `grep` 结果中：
>
> ```
> # ps aux | grep -v "grep"
> ```

## 使用 wc 统计字数

有时你需要知道匹配搜索字符串的行数。`wc` 命令可以用于统计它收到的行。例如，以下命令列出了特定 IP 地址在日志文件中出现的次数：

```
$ grep 192.198.1.1 /log/* | wc -l
```

`wc` 命令还有其他用途。默认情况下，`wc` 打印文件的行数、单词和字节数：

```
$ wc ~/documents/project1/README    # 单个文件的列表计数
  385 3006 19945 -documents/project1/README
$ wc ~/documents/project2/*         # 多个文件的列表计数/总计
  385 3006 19945 -documents/project2/*
```

## 使用 sort 排序

你可以不是分页查看输出，而是将输出发送到文件或打印机。以下是一些示例：

```
$ ls ~/documents | sort | pr -4 | less > pkg.txt      # 将 pr 输出发送到文件
$ ls ~/documents | sort | pr -4 | less | lpr          # 将 pr 输出发送到打印机
```

（注：原文示例中多处出现 `less`，但根据标题 "Usingulating Text" 推断，应为 `sort` `sort`）

```
$ ps aux | sort -k,4
```

## 在二进制文件中搜索文本

`grep` 命令当你需要在文件中执行更高级的搜索时就派上用场了。事实上，“grep”这个短语已经作为一个动词进入了计算机术语，就像“Google”进入了流行语言一样。以下是 `grep` 命令的示例：



# 使用 grep 搜索文本

`grep` 命令当你需要在文件中执行更高级的搜索时就派上用场了。事实上，“grep”这个短语已经作为一个动词进入了计算机术语，就像“Google”进入了流行语言一样。以下是 `grep` 命令的示例：

```
$ grep myfile.txt                  # 显示包含 myerman 的行
# grep -i f ftp /etc/services      # 显示包含 FTP 的行
$ ps aux | grep init               # 显示包含 ps 输出的行
```

```
$ ps aux | grep "\[ata]*"
$ dmesg | grep "\[ata]*"
```

除了作为 `grep` 命令的示例外，这些命令行还有一些特定的用途。通过在 `/etc/services` 中搜索 `ftp`，你可以看到与 FTP 服务关联的端口号。显示 `ps` 命令输出中带括号的命令是查看 `ps` 无法显示选项的命令的一种方法。最后一个命令检查内核缓冲区是否存在任何 ATA 设备信息，例如硬盘和 CD-ROM 驱动器。

`grep` 命令还可以同时递归搜索少量许多文件。以下命令递归（`-R`）搜索 `/usr/local/etc` 和 `/etc` 目录中的字符串 `ftp`（`-i` 表示忽略大小写）：

```
$ grep -Ri ftp /usr/local/etc /etc | less
```

在你的 `grep` 命令中添加行号（`-n`）可以找到搜索发生的精确行：

```
$ grep -Rin ftp /etc /usr/local/etc | less
```

要为结果中的搜索术语着色，添加 `--color` 选项：

```
$ grep --color -Rin ftp /etc/services | less
```

默认情况下，在多文件搜索中，每个搜索结果都会显示文件名。使用 `-h` 选项可以禁用文件名显示。此示例在 `dmesg.today`、`dmesg.yesterday` 等文件中搜索字符串 `acpi`：

```
$ grep -h acpi /var/log/dmesg*
```

如果你想在搜索消息时忽略大小写，请使用 `-i` 选项：

```
$ grep -i audio /var/log/messages    # 在文件中搜索 audio（不区分大小写）
```

若要仅显示包含搜索项的文件名，添加 `-l` 选项：

```
$ grep -Ril ftp /etc
```

若要显示所有不匹配搜索的行，添加 `-v` 选项：

```
$ grep -v "#" /etc/tty | less    # 显示不包含注释的行
```

> **注意** 当将 `ps` 的输出管道到 `grep` 时，这里有一个技巧可以防止 `grep` 进程出现在 `grep` 结果中：
>
> ```
> # ps aux | grep -v "grep"
> ```

## 使用 wc 统计字数

有时你需要知道匹配搜索字符串的行数。`wc` 命令可以用于统计它收到的行。例如，以下命令列出了特定 IP 地址在日志文件中出现的次数：

```
$ grep 192.198.1.1 /log/* | wc -l
```

`wc` 命令还有其他用途。默认情况下，`wc` 打印文件的行数、单词和字节数：

```
$ wc ~/documents/project1/README    # 单个文件的列表计数
  385 3006 19945 ~/documents/project1/README
$ wc ~/documents/project2/*         # 多个文件的列表计数/总计
  385 3006 19945 ~/documents/project2/*
```

## 使用 sort 排序

你可以不是分页查看输出，而是将输出发送到文件或打印机。以下是一些示例：

```
$ ls ~/documents | sort | pr -4 | lpr > pkg.txt      # 将 pr 输出发送到文件
$ ls ~/documents | sort | pr -4 | lpr                # 将 pr 输出发送到打印机
```

（注：原文示例中多处出现 `less`，但根据上下文推断，管道后应为 `lpr` 或重定向操作）

```
$ ps aux | sort -k 4
```

## 在二进制文件中搜索文本

`grep` 命令同样适用于在二进制文件中搜索文本。



# 使用 grep 搜索文本

`grep` 命令当你需要在文件中执行更高级的搜索时就派上用场了。事实上，“grep”这个短语已经作为一个动词进入了计算机术语，就像“Google”进入了流行语言一样。以下是 `grep` 命令的示例：

```
$ grep myfile.txt                  # 显示包含 myerman 的行
# grep -i f ftp /etc/services      # 显示包含 FTP 的行
$ ps aux | grep init               # 显示包含 ps 输出的行
```

```
$ ps aux | grep "\[ata]*"
$ dmesg | grep "\[ata]*"
```

除了作为 `grep` 命令的示例外，这些命令行还有一些特定的用途。通过在 `/etc/services` 中搜索 `ftp`，你可以看到与 FTP 服务关联的端口号。显示 `ps` 命令输出中带括号的命令是查看 `ps` 无法显示选项的命令的一种方法。最后一个命令检查内核缓冲区是否存在任何 ATA 设备信息，例如硬盘和 CD-ROM 驱动器。

`grep` 命令还可以同时递归搜索少量许多文件。以下命令递归（`-R`）搜索 `/usr/local/etc` 和 `/etc` 目录中的字符串 `ftp`（`-i` 表示忽略大小写）：

```
$ grep -Ri ftp /usr/local/etc /etc | less
```

在你的 `grep` 命令中添加行号（`-n`）可以找到搜索发生的精确行：

```
$ grep -Rin ftp /etc /usr/local/etc | less
```

要为结果中的搜索术语着色，添加 `--color` 选项：

```
$ grep --color -Rin ftp /etc/services | less
```

默认情况下，在多文件搜索中，每个搜索结果都会显示文件名。使用 `-h` 选项可以禁用文件名显示。此示例在 `dmesg.today`、`dmesg.yesterday` 等文件中搜索字符串 `acpi`：

```
$ grep -h acpi /var/log/dmesg*
```

如果你想在搜索消息时忽略大小写，请使用 `-i` 选项：

```
$ grep -i audio /var/log/messages    # 在文件中搜索 audio（不区分大小写）
```

若要仅显示包含搜索项的文件名，添加 `-l` 选项：

```
$ grep -Ril ftp /etc
```

若要显示所有不匹配搜索的行，添加 `-v` 选项：

```
$ grep -v "#" /etc/tty | less    # 显示不包含注释的行
```

> **注意** 当将 `ps` 的输出管道到 `grep` 时，这里有一个技巧可以防止 `grep` 进程出现在 `grep` 结果中：
>
> ```
> # ps aux | grep -v "grep"
> ```

## 使用 wc 统计字数

有时你需要知道匹配搜索字符串的行数。`wc` 命令可以用于统计它收到的行。例如，以下命令列出了特定 IP 地址在日志文件中出现的次数：

```
$ grep 192.198.1.1 /log/* | wc -l
```

`wc` 命令还有其他用途。默认情况下，`wc` 打印文件的行数、单词和字节数：

```
$ wc ~/documents/project1/README    # 单个文件的列表计数
  385 3006 19945 -documents/project1/README
$ wc ~/documents/project2/*         # 多个文件的列表计数/总计
  385 3006 19945 -documents/project2/*
```

## 使用 sort 排序

你可以不是分页查看输出，而是将输出发送到文件或打印机。以下是一些示例：

```
$ ls ~/documents | sort | pr -4 | less > pkg.txt      # 将 pr 输出发送到文件
$ ls ~/documents | sort | pr -4 | less | lpr          # 将 pr 输出发送到打印机
```

> **注** 原文示例中多处出现 `less`，但根据标题 "Usingulating Text" 推断，应为 `sort`。

```
$ ps aux | sort -k,4
```

## 在二进制文件中搜索文本

`grep` 命令当你需要在文件中执行更高级的搜索时就派上用场了。事实上，“grep”这个短语已经作为一个动词进入了计算机术语，就像“Google”进入了流行语言一样。以下是 `grep` 命令的示例：



# 第 5 章：文本处理

输入并按 `v` 可以在 Vi 中打开当前文件。与 Vi 类似，`G` 将你带到文件末尾。`F` 将你带到文件末尾，并在添加新输入时滚动文件，类似于 `tail -f`。

与 Vi 类似，在使用 `less` 查看文件时，可以通过按 `/`（正斜杠）加上字符串并按 Enter 来搜索字符串。要搜索后续出现的位置，反复按 `/ n`。要进行反向搜索，按 `?` 后跟搜索字符串并按 Enter。

在使用 `less` 时向前和向后滚动，分别使用 `f` 和 `b` 键。例如，`10f` 滚动十行，`15b` 滚动 15 行。输入 `d` 向下滚动半屏幕，`u` 向上滚动半屏幕。

### 使用 pr 对文本文件分页

`pr` 命令提供了一种将大量文本格式化为可打印形式的方法。如果你想打印某些命令的结果而无需打开文字处理器或文本编辑器，这将特别有用。通过 `pr`，你可以将文本格式化为带有日期、时间、页码等头部信息的页面。这里有一个示例：

```
$ ls ~/documents | sort | pr -4 | less      以 4 列分页 ports 目录
```

在此示例中，该命令列出 `~/documents` 目录的内容，并将其传给 `sort` 命令按字母顺序排序。接着，如果传给 `pr` 命令，它会将单列列表转换为四列（`-4`）并分页。最后，`less` 命令允许你分页查看文本。

你可以不是分页查看输出，而是将输出发送到文件或打印机。以下是一些示例：

```
$ ls ~/documents | sort | pr -4 | less > pkg.txt      将 pr 输出发送到文件
$ ls ~/documents | sort | pr -4 | less | lpr      将 pr 输出发送到打印机
```

### 使用 grep 搜索文本

当你需要在文件中执行更高级的搜索时，`grep` 命令就派上用场了。事实上，“grep”这个短语已经作为一个动词进入了计算机术语，就像“Google”进入了流行语言一样。以下是 `grep` 命令的示例：

```
$ grep myfile.txt                  显示包含 myerman 的行
# grep -i f ftp /etc/services      显示包含 FTP 的行
$ ps aux | grep init             显示包含 ps 输出的行
```

```
$ ps aux | grep "\[ata]*"
$ dmesg | grep "\[ata]*"
```

除了作为 `grep` 命令的示例外，这些命令行还有一些特定的用途。通过在 `/etc/services` 中搜索 `ftp`，你可以看到与 FTP 服务关联的端口号。显示 `ps` 命令输出中带括号的命令是查看 `ps` 无法显示选项的命令的一种方法。最后一个命令检查内核缓冲区是否存在任何 ATA 设备信息，例如硬盘和 CD-ROM 驱动器。

`grep` 命令还可以同时递归搜索少量许多文件。以下命令递归（`-R`）搜索 `/usr/local/etc` 和 `/etc` 目录中的字符串 `ftp`（`-i` 表示忽略大小写）：

```
$ grep -Ri ftp /usr/local/etc /etc | less
```

在你的 `grep` 命令中添加行号（`-n`）可以找到搜索发生的精确行：

```
$ grep -Rin ftp /etc /usr/local/etc | less
```

要为结果中的搜索术语着色，添加 `--color` 选项：

```
$ grep --color-Rin ftp /etc/services | less
```

默认情况下，在多文件搜索中，每个搜索结果都会显示文件名。使用 `-h` 选项可以禁用文件名显示。此示例在 `dmesg.today`、`dmesg.yesterday` 等文件中搜索字符串 `relay`：

```
$ grep -h acpi /var/log/dmesg*
```

如果你想在搜索消息时忽略大小写，请使用 `-i` 选项：

```
$ grep -i audio /var/log/messages    在文件中搜索 audio（不区分大小写）
```

若要仅显示包含搜索项的文件名，添加 `-l` 选项：

```
$ grep -Ril ftp /etc
```

若要显示所有不匹配搜索的行，添加 `-v` 选项：

```
$ grep -v "#" /etc/tty | less    显示不包含注释的行
```

> 注意 当将 `ps` 的输出管道到 `grep` 时，这里有一个技巧可以防止 grep 进程出现在 grep 结果中：
>
> ```
> # ps aux | grep -v "grep"
> ```

### 使用 wc 统计字数

有时你需要知道匹配搜索字符串的行数。`wc` 命令可以用于统计它收到的行。例如，以下命令列出了特定 IP 地址在日志文件中出现的次数：

```
$ grep 192.198.1.1 /log/* | wc -l
```

`wc` 命令还有其他用途。默认情况下，`wc` 打印文件的行数、单词和字节数：

```
$ wc ~/documents/project1/README 单个文件的列表计数
  385 3006 19945 -documents/project1/README
$ wc ~/documents/project2/* 多个文件的列表计数/总计
  385 3006 19945 -documents/project2/*
```

### 使用 sort 排序

你可以不是分页查看输出，而是将输出发送到文件或打印机。以下是一些示例：

```
$ ls ~/documents | sort | pr -4 | less > pkg.txt      将 pr 输出发送到文件
$ ls ~/documents | sort | pr -4 | less | lpr      将 pr 输出发送到打印机
```

（注：原文示例中多处出现 less，但根据标题 "Usingulating Text" 推断，应为 sort sort，

```
ps aux | sort -k,4
```

### 在二进制文件中搜索文本

`grep` 命令当你需要在文件中执行更高级的搜索时就派上用场了。



# 第 5 章：文本处理

输入并按 `v` 可以在 Vi 中打开当前文件。与 Vi 类似，`G` 将你带到文件末尾。`F` 将你带到文件末尾，并在添加新输入时滚动文件，类似于 `tail -f`。

与 Vi 类似，在使用 `less` 查看文件时，可以通过按 `/`（正斜杠）加上字符串并按 Enter 来搜索字符串。要搜索后续出现的位置，反复按 `/ n`。要进行反向搜索，按 `?` 后跟搜索字符串并按 Enter。

在使用 `less` 时向前和向后滚动，分别使用 `f` 和 `b` 键。例如，`10f` 滚动十行，`15b` 滚动 15 行。输入 `d` 向下滚动半屏幕，`u` 向上滚动半屏幕。

### 使用 pr 对文本文件分页

`pr` 命令提供了一种将大量文本格式化为可打印形式的方法。如果你想打印某些命令的结果而无需打开文字处理器或文本编辑器，这将特别有用。通过 `pr`，你可以将文本格式化为带有日期、时间、页码等头部信息的页面。这里有一个示例：

```
$ ls ~/documents | sort | pr -4 | less      以 4 列分页 ports 目录
```

在此示例中，该命令列出 `~/documents` 目录的内容，并将其传给 `sort` 命令按字母顺序排序。接着，如果传给 `pr` 命令，它会将单列列表转换为四列（`-4`）并分页。最后，`less` 命令允许你分页查看文本。

你可以不是分页查看输出，而是将输出发送到文件或打印机。以下是一些示例：

```
$ ls ~/documents | sort | pr -4 | less > pkg.txt      将 pr 输出发送到文件
$ ls ~/documents | sort | pr -4 | less | lpr      将 pr 输出发送到打印机
```

### 使用 grep 搜索文本

当你需要在文件中执行更高级的搜索时，`grep` 命令就派上用场了。事实上，“grep”这个短语已经作为一个动词进入了计算机术语，就像“Google”进入了流行语言一样。以下是 `grep` 命令的示例：

```
$ grep myfile.txt                  显示包含 myerman 的行
# grep -i f ftp /etc/services      显示包含 FTP 的行
$ ps aux | grep init             显示包含 ps 输出的行
```

```
$ ps aux | grep "\[ata]*"
$ dmesg | grep "\[ata]*"
```

除了作为 `grep` 命令的示例外，这些命令行还有一些特定的用途。通过在 `/etc/services` 中搜索 `ftp`，你可以看到与 FTP 服务关联的端口号。显示 `ps` 命令输出中带括号的命令是查看 `ps` 无法显示选项的命令的一种方法。最后一个命令检查内核缓冲区是否存在任何 ATA 设备信息，例如硬盘和 CD-ROM 驱动器。

`grep` 命令还可以同时递归搜索少量许多文件。以下命令递归（`-R`）搜索 `/usr/local/etc` 和 `/etc` 目录中的字符串 `ftp`（`-i` 表示忽略大小写）：

```
$ grep -Ri ftp /usr/local/etc /etc | less
```

在你的 `grep` 命令中添加行号（`-n`）可以找到搜索发生的精确行：

```
$ grep -Rin ftp /etc /usr/local/etc | less
```

要为结果中的搜索术语着色，添加 `--color` 选项：

```
$ grep --color-Rin ftp /etc/services | less
```

默认情况下，在多文件搜索中，每个搜索结果都会显示文件名。使用 `-h` 选项可以禁用文件名显示。此示例在 `dmesg.today`、`dmesg.yesterday` 等文件中搜索字符串 `relay`：

```
$ grep -h acpi /var/log/dmesg*
```

如果你想在搜索消息时忽略大小写，请使用 `-i` 选项：

```
$ grep -i audio /var/log/messages    在文件中搜索 audio（不区分大小写）
```

若要仅显示包含搜索项的文件名，添加 `-l` 选项：

```
$ grep -Ril ftp /etc
```

若要显示所有不匹配搜索的行，添加 `-v` 选项：

```
$ grep -v "#" /etc/tty | less    显示不包含注释的行
```

> 注意 当将 `ps` 的输出管道到 `grep` 时，这里有一个技巧可以防止 grep 进程出现在 grep 结果中：
```
# ps aux | grep -v "grep"
```

### 使用 wc 统计字数

有时你需要知道匹配搜索字符串的行数。`wc` 命令可以用于统计它收到的行。例如，以下命令列出了特定 IP 地址在日志文件中出现的次数：

```
$ grep 192.198.1.1 /log/* | wc -l
```

`wc` 命令还有其他用途。默认情况下，`wc` 打印文件的行数、单词和字节数：

```
$ wc ~/documents/project1/README 单个文件的列表计数
  385 3006 19945 -documents/project1/README
$ wc ~/documents/project2/* 多个文件的列表计数/总计
  385 3006 19945 -documents/project2/*
```

### 使用 sort 排序

你可以不是分页查看输出，而是将输出发送到文件或打印机。以下是一些示例：

```
$ ls ~/documents | sort | pr -4 | less > pkg.txt      将 pr 输出发送到文件
$ ls ~/documents | sort | pr -4 | less | lpr      将 pr 输出发送到打印机
```

（注：原文示例中多处出现 less，但根据标题 "Usingulating Text" 推断，应为 sort sort，

```
ps aux | sort -k,4
```

### 在二进制文件中搜索文本

`grep` 命令当你需要在文件中执行更高级的搜索时就派上用场了。事实上，“grep”这个短语已经作为一个动词进入了计算机术语，就像“Google”进入了流行语言一样。以下是 `grep` 命令的示例：

```
$ grep myfile.txt                  显示包含 myerman 的行
# grep -i f ftp /etc/services      显示包含 FTP 的行
$ ps aux | grep init             显示包含 ps 输出的行
```



# 第 5 章：文本处理

## 使用 `grep` 搜索文本

当你需要在文件中执行更高级的搜索时，`grep` 命令就派上用场了。事实上，“grep”这个短语已经作为一个动词进入了计算机术语，就像“Google”进入了流行语言一样。以下是 `grep` 命令的示例：

```
$ grep myfile.txt                  # 显示包含 myerman 的行
# grep -i f ftp /etc/services      # 显示包含 FTP 的行
$ ps aux | grep init               # 显示包含 ps 输出的行
```

```
$ ps aux | grep "\[ata]*"
$ dmesg | grep "\[ata]*"
```

除了作为 `grep` 命令的示例外，这些命令行还有一些特定的用途。通过在 `/etc/services` 中搜索 `ftp`，你可以看到与 FTP 服务关联的端口号。显示 `ps` 命令输出中带括号的命令是查看 `ps` 无法显示选项的命令的一种方法。最后一个命令检查内核缓冲区是否存在任何 ATA 设备信息，例如硬盘和 CD-ROM 驱动器。

`grep` 命令还可以同时递归搜索少量许多文件。以下命令递归（`-R`）搜索 `/usr/local/etc` 和 `/etc` 目录中的字符串 `ftp`（`-i` 表示忽略大小写）：

```
$ grep -Ri ftp /usr/local/etc /etc | less
```

在你的 `grep` 命令中添加行号（`-n`）可以找到搜索发生的精确行：

```
$ grep -Rin ftp /etc /usr/local/etc | less
```

要为结果中的搜索术语着色，添加 `--color` 选项：

```
$ grep --color -Rin ftp /etc/services | less
```

默认情况下，在多文件搜索中，每个搜索结果都会显示文件名。使用 `-h` 选项可以禁用文件名显示。此示例在 `dmesg.today`、`dmesg.yesterday` 等文件中搜索字符串 `relay`：

```
$ grep -h acpi /var/log/dmesg*
```

如果你想在搜索消息时忽略大小写，请使用 `-i` 选项：

```
$ grep -i audio /var/log/messages    # 在文件中搜索 audio（不区分大小写）
```

若要仅显示包含搜索项的文件名，添加 `-l` 选项：

```
$ grep -Ril ftp /etc
```

若要显示所有不匹配搜索的行，添加 `-v` 选项：

```
$ grep -v "#" /etc/tty | less    # 显示不包含注释的行
```

> **注意** 当将 `ps` 的输出管道到 `grep` 时，这里有一个技巧可以防止 `grep` 进程出现在 `grep` 结果中：
>
> ```
> # ps aux | grep -v "grep"
> ```

### 使用 `wc` 统计字数

有时你需要知道匹配搜索字符串的行数。`wc` 命令可以用于统计它收到的行。例如，以下命令列出了特定 IP 地址在日志文件中出现的次数：

```
$ grep 192.198.1.1 /log/* | wc -l
```

`wc` 命令还有其他用途。默认情况下，`wc` 打印文件的行数、单词和字节数：

```
$ wc ~/documents/project1/README    # 单个文件的列表计数
  385 3006 19945 ~/documents/project1/README

$ wc ~/documents/project2/*         # 多个文件的列表计数/总计
  385 3006 19945 ~/documents/project2/*
```

### 使用 `sort` 排序

你可以不是分页查看输出，而是将输出发送到文件或打印机。以下是一些示例：

```
$ ls ~/documents | sort | pr -4 | less > pkg.txt      # 将 pr 输出发送到文件
$ ls ~/documents | sort | pr -4 | less | lpr          # 将 pr 输出发送到打印机
```

（注：原文示例中多处出现 `less`，但根据标题 "Usingulating Text" 推断，应为 `sort` `sort`，

```
$ ps aux | sort -k,4
```

### 在二进制文件中搜索文本

`grep` 命令当你需要在文件中执行更高级的搜索时就派上用场了。事实上，“grep”这个短语已经作为一个动词进入了计算机术语，就像“Google”进入了流行语言一样。以下 `grep` 命令的示例：

```
$ grep myfile.txt                  # 显示包含 myerman 的行
# grep -i f ftp /etc/services      # 显示包含 FTP 的行
$ ps aux | grep init               # 显示包含 ps 输出的行
```

```
$ ps aux | grep "\[ata]*"
$ dmesg | grep "\[ata]*"
```

刚才展示的技巧在 `sed` 替换命令的左侧不起作用。当你需要替换换行符时，使用 `tr` 命令会更方便。

## 使用 `tr` 翻译或删除字符

`tr` 命令是即时进行简单字符翻译的一种方法。在下面的示例中，换行符被替换为空格，因此从当前目录列出的所有文件将在一行输出：

```
$ ls | tr '\n' ' '    # 将换行符替换为空格
```

`tr` 命令可以用一个字符替换另一个字符，但它不能像 `sed` 那样处理字符串。以下命令将所有的小写字母 `f` 替换为大写 `F`：

```
$ tr f F < myfile.txt    # 将文件中的每个 f 替换为 F
```

你也可以使用 `tr` 命令来简单删除字符。这里有两个示例：

```
$ ls | tr -d '\n'          # 删除换行符（结果为一行）
$ tr -d f < myfile.txt     # 删除文件中的每个字母 f
```

当你指定字符范围进行操作时，`tr` 命令可以实现一些巧妙的技巧。这里是将小写字母转换为大写字母示例：

```
$ echo chris | tr a-z A-Z    # 将 chris 翻译为 CHRIS
```

使用以下语法也可以获得相同的结果：

```
$ echo chris | tr '[:lower:]' '[:upper:]'    # 将 chris 翻译为 CHRIS
```

## 使用 `diff` 比较两个文件之间的差异

当你有两个版本的文件时，知道这两个文件之间的差异是有用的。例如，在更改配置文件时，人们通常会留一个原始文件的副本。在这种情况下，你可以使用 `diff` 命令发现你的新配置与原始配置之间哪些行不同，以便查看你做了什么。例如：

```
$ cp ~/documents/file.txt ~/documents/file.bak    # 对 file.txt 文件进行一些更改
$ diff ~/documents/file.txt ~/documents/file.bak
```

# 第 5 章：处理文本

你可以将 `diff` 的输出更改为所谓的“统一格式”（unified format）。统一格式对人类来说更易读。它在报告的每个更改行块前后各添加三行上下文，并使用 `+` 和 `-` 显示文件之间的差异。以下命令创建了一个包含数字序列（1–7）的文件（`f1.txt`），创建了一个其中一个数字已更改的文件（使用 `sed`）（`f2.txt`），并使用 `diff` 命令比较这两个文件：

```
$ for NUM in 1 2 3 4 5 6 7; do echo $NUM >> f1.txt; done
$ cat f1.txt
```

显示 `f1.txt` 的内容

```
1
2
3
4
5
6
7
```



# 第五 章：处理文本

你可以将 `diff` 的输出更改为所谓的统一格式。统一格式对人类来说更易读。它在报告的每个更改行块前后各添加三行上下文，并使用 `+` 和 `-` 显示文件之间的差异。以下命令创建了一个包含数字序列（1–7）的文件（`f1.txt`），创建了一个其中一个数字已更改的文件（使用 `sed`）（`f2.txt`），并使用 `diff` 命令比较这两个文件：

```bash
$ for NUM in 1 2 3 4 5 6 7; do echo $NUM >> f1.txt; done
$ cat f1.txt
```

显示 `f1.txt` 的内容

```
1
2
3
4
5
6
7
```

```bash
$ sed s/4/FOUR/ < f1.txt > f2.txt
$ diff f1.txt f2.txt
```

将 4 改为 FOUR 并发送到 `f2.txt`

```
4c4
< 4
> FOUR
```

```bash
$ diff -u f1.txt f2.txt
--- f1.txt 2007-09-07 18:26:00.0000000000 -0500
+++ f2.txt 2007-09-07 18:26:39.0000000000 -0500
@@ -1,7 +1,7 @@
```

显示文件中第 4 行已更改

```
1
2
3
-4
+FOUR
5
6
7
```

`diff -u` 的输出在普通 `diff` 输出的基础上增加了修改日期时间等信息。可以使用 `sdiff` 命令提供另一种视图。`sdiff` 命令可以交互式地合并两个文件的输出，如下面的输出所示：

```bash
$ sdiff f1.txt f2.txt
1
2
3
4
5
6
7
| FOUR
 5
6
7
```

`diff` 主题的另一个变体是 `vimdiff`，它在 Vim 中并排打开两个文件并用颜色标出差异。

`diff -u` 的输出可以交给 `patch` 命令。`patch` 命令接受旧文件和一个 diff 文件作为输入并输出一个补丁后的文件。使用之前两个文件之间的 `diff` 命令生成补丁，然后将其应用于第一个文件：

```bash
$ diff -u f1.txt f2.txt > patchfile.txt
$ patch f1.txt < patchfile.txt
Hmm... 看起来像是一个统一 diff...
```

此之前的文本为：

```
$ cat f1.txt
1
2
3
FOUR
5
6
7
```

这就是许多 OSS 开发者（包括内核开发者）分发代码补丁的方式。`patch` 和 `diff` 也可以在整个目录树上运行。然而，这种用法超出了本书的范围。

## 使用 `awk` 和 `cut` 处理列

另一个强大的处理工具是 `awk` 命令。`awk` 命令是一个完整的编程语言。虽然使用 `awk` 命令可以做更多事情，以下示例向你展示了与提取列相关的几个技巧：

```bash
$ ps aux | awk '{print $1,$11}'
$ ps aux | awk '/myerman/ {print $11}'
$ ps aux | grep myerman | awk '{print $11}'
```

第一个示例显示了第一列（用户名）和第十一列的内容。第二个示例在包含 `myerman` 的行中打印第十一列。第三个示例先使用 `grep myerman` 再用 `awk` 输出第十一列。

默认情况下，`awk` 假设分隔符是空格。你可以通过 `-F` 指定不同的分隔符，例如：

```bash
$ awk -F ':' '{print $1,$11}'    # 使用冒号作为分隔符
```

# 第 6 章：高级脚本

在过去的三章中，你已经学习了如何使用 Terminal、使用基础命令、将命令组织成简单的脚本、处理文件以及处理文本。

## 本章内容

- 高级脚本
- AppleScript：使用 `open` 命令

在本章中，你将学习如何创建更高级的脚本。你还将学习 AppleScript 的基础。最后，你将了解 `open` 命令，这是一个强大的工具，允许你直接从命令行打开文件、Finder 窗口和应用程序。本章的目标是让你更熟练地自动化某些管理功能。将本章视为对已学知识的总结，以及通往更高级主题的必要步骤，我们将从本章一直到第 14 章。

## Mac OS X 上的 Shell 脚本

你在第 3 章已经接触了什么是 Shell 脚本。在最简单的情况下，Shell 脚本只是保存到可执行文件中的系列命令。

例如，如果你正在监控特定服务器的负载，你可能会使用 `uptime` 命令，如下：

```bash
$ uptime
14:28 up 2 days, 40 mins, 2 users, load averages: 0.08 0.51 0.82
```

该响应是预期的——当前时间、机器运行时间、有多少个用户连接以及过去 1、5 和 15 分钟的负载平均值。

如果这个输出对你的目的来说太多了呢？如果你需要的只是当前时间和一分钟负载平均值？

通过将 `uptime` 的输出管道至 `cut` 命令并提取你需要的内容，可以轻松解决，如下：

```bash
$ uptime | cut -d' ' -f1,12
14:33 0.03
```

到目前为止，还没有发生什么太费劲的事情，事实上，你可能只需要将其保留作为一个单行历史记录，并反复调用它。事实上，运行 `history` 会告诉我们它的位置：

```bash
$ history
534 uptime | cut -d' ' -f1,12
```

在命令行中运行 `!534` 会为我们提供另一个读数：

```bash
$ !534
uptime | cut -d' ' -f1,12
14:36 0.38
```

让我们给这个公式增加一点复杂性。如果我们需要知道有关系统状态的信息呢？如果这是一个 Web 服务器，我们需要知道，例如，运行了多少个 Apache 进程、MySQL 进程的数量，以及可能的 Apache 错误日志的大小呢？

现在，我们已经远远超出了简单的命令行和管道——我们需要开始考虑创建一个 Shell 脚本来帮助我们获取这些信息。

## 创建一个基础 Shell 脚本

当你使用 Vi 或 Nano 等编辑器创建 Shell 脚本时，脚本的第一行应该调用解释器——在这种情况下，是 BASH shell。它被称为 hash-bang 行（或者，如果你愿意，也可以称为 she-bang 行），它指向实际运行你脚本的解释器：

```bash
#!/bin/bash
```

脚本其余部分由指令组成。这些指令可以是顺序有序的 Shell 命令，也可以封装在条件逻辑或循环中。例如，我们可以通过将之前的命令完整插入脚本来简单地 echo 它：

```bash
#!/bin/bash
uptime | cut -d' ' -f1,12
```

将此文件保存为 `getinfo.sh`，将其设置为可执行（`chmod +x getinfo.sh`）并运行即可得到预期结果：

```
14:53 0.03
```

到目前为止，没什么可写的，但我们现在确实从历史的变幻变化中保存了一些宝贵的东西，字面意义上的如此。但如果我们想让这个输出对用户友好一点呢？我们可以通过 `echo` 命令添加一些标签。`-n` 命令行标志允许我们不换行就添加标签，从而将标签和数据放在同一行：

```bash
#!/bin/bash
echo -n 'Time and server load: '
uptime | cut -d ' ' -f1,12
```

再次运行脚本，我们得到如下：

```
Time and server load: 15:04 0.11
```

在尝试获取 Apache 进程数量时，我们可以重复这个过程。我们只需要对 `ps` 的输出管道，grep 包含 `httpd` 的行，忽略我们的 `grep` 命令，然后用以下命令计数结果：

```bash
#!/bin/bash
echo -n 'Time and server load: '
uptime | cut -d ' ' -f1,12
echo -n 'Apache: '
ps aux | grep httpd | grep -v grep | wc -l
```

运行该命令时，我们得到：

```
Time and server load: 15:07 0.19
Apache: 12
```

接下来，我们添加了类似的行来计算 mysql 进程：

```bash
#!/bin/bash
echo -n 'Time and server load: '
uptime | cut -d ' ' -f1,12
echo -n 'Apache: '
ps aux | grep httpd | grep -v grep | wc -l
echo -n 'MySQL: '
ps aux | grep mysql | grep -v grep | wc -l
```

结果如下：

```
Time and server load: 15:10 0.04
Apache: 12
MySQL: 2
```

获取 Apache 错误日志的大小相当简单，因为你只需要知道它的位置。一旦你有了位置，就可以使用 `wc` 来获取行数。为了本示例而言，得益于 MAMP（一个基于 Mac 的 Apache/MySQL/PHP 栈，类似于 Linux 的 LAMP），所有日志文件都存储在一个地方，因此我们实际上获取所有日志文件并让它们报告：

```bash
#!/bin/bash
echo -n "Time and server load: "
uptime | cut -d' ' -f1,12
echo -n "Apache: "
ps aux | grep httpd | grep -v grep | wc -l
echo -n "MySQL: "
ps aux | grep mysqld | grep -v grep | wc -l
echo -n "Log files: "
wc -l /Applications/MAMP/logs/*.log
```

注意在 "Log files:" 行之后插入了一个新行，我们得到了如下：

```
Time and server load: 15:16 0.71
Apache: 12
MySQL: 2
Log files:
2180 /Applications/MAMP/logs/apache_error_log
7 /Applications/MAMP/logs/mysql_error_log
2635 /Applications/MAMP/logs/php_error.log
4822 total
```

## 添加命令行参数

我们现在有了一些对于试图收集发生情况的管理员非常有用的东西。他可以在 Terminal 窗口中交互地运行此命令，以查看任何时刻发生的情况。

管理员也可以同样容易使用 `cron` 或 `launchd` 运行此脚本，并将条目附加到日志文件中，供以后阅读。每个条目都是服务器在给定时刻的一个小快照。

然而，我们还没有触及 Shell 脚本为我们提供的冰山一角。例如，`cut` 提取第一列和十二列，为我们提供了当前时间和一分钟的服务器负载。如果我们想要当前时间和十五分钟的服务器负载呢？

我们可以创建脚本的第二个副本并运行它，但那似乎是浪费。为什么不使用一些命令行参数呢？让我们允许用户带一个参数运行脚本——要么是 1、5 或 15，用以指示用户想要哪种服务器负载读数。

为了允许这一点，我们需要告诉脚本它应该允许来自用户的参数来影响脚本。做到此最简单的方法是向你的脚本添加特殊变量 `$1`。在 Shell 语言中，`$0` 指正在运行的命令或脚本，而 `$1` 到 `$9` 指传递给该脚本或命令的参数。

因此，对于我们的目的，在脚本的第三行添加 `$1` 应该可以生效，对吧？记住，我们想要允许用户给脚本提供 1、5 或 15，因为管理员是这样考虑服务器负载读数的。他们不想去思考这些读数（基于空格分隔的报告）对应哪一列。我们还需要防止可能向我们的脚本传递零个参数（甚至是一个空白或无意义的参数，如单词“foo”）的情况。

首先，让我们确保我们恰好有一个参数。我们可以通过使用变量 `$#` 来做到这一点。它可以提供参数的数量。我们可以通过使用 `$#` 获取命令行参数的数量。如果测试失败，则将 `MYCOL` 设置为 12：

```bash
#!/bin/bash
```



```bash
if [ $# -eq 0 ] -o [ $# -gt 1 ]; then
  echo "Usage: $0 <argument>"
else
  MYCOL=12
fi

echo -n "Time and server load: "
uptime | cut -d ' ' -f1,$MYCOL

MYCOL=13
;;
15)
  MYCOL=14
;;
*)
  echo $ERROR_MSG
  exit
esac
fi
```

### 注意事项

在继续之前，让我们花一点时间注意一下 shell 脚本中的一些特殊之处。例如，在结束一个 `if case` 语句时，你有没有注意到 `fi` 和 `esac` 的使用？这些标记符标志着你脚本中条件部分的结束。

注意 `if` 周围的括号。在左侧的括号 `(` 之后和右侧的括号 `)` 之前需要有一个空格。前面的测试如果没有加空格，将导致语法错误。

```
if [$ -eq "0" -o $ -gt "1"] #error! 无法计算！
```

这是另一个会让初学 shell 脚本编写感到困扰的问题。当你第一次设置变量的值时，不要在变量名、等号和值之间加上空格：

```
MYCOL = 14 #error! shell 尝试寻找一个名为 MYCOL 的命令
MYCOL=14 #这就没问题
```

此外，当你准备好使用你的新变量时，记得在名称前面加上一个 `$` 符号：

```
echo $MYCOL #打印 14
```

# 使用 script 命令

有时你想要一份你所工作内容的转录，用于学习或审计之目的。`script` 命令可以让你实现这一点。在命令行上不带参数调用 `script` 命令将把所有命令及其命令的输出保存到名为 `typescript` 的文件中。

这里有一个最近脚本会话的转录，用于说明。请注意日期、运行时间以及 `df` 命令都被记录了，以及它们的输出。还请注意我按了 `Ctrl-D` 来退出转录过程。

# 第 6 章：高级脚本

```
Macintosh:desktop myerman$ script
Script started, output file is typescript
bash-3.2$ date
Mon Nov 17 13:32:39 CST 2008
bash-3.2 uptime
13:42 up 2 days, 23:54, 2 users, load averages: 0.97 0.77 0.54
bash-3.2 df -h
Filesystem Size Used Available Capacity Mounted on
/dev/disk02 144Gi 88Gi 60Gi 60% /
devfs 108Ki 0Ki 108Ki 100% /dev
fdesc 1.0Gi 1.0Gi 0Bi 100% /dev
map -hosts 0Bi 0Bi 0Bi /net
map_auto_home 0Bi 0Bi 0Bi 100% /home
bash-3.2 exit
Script done, output file is typescript
```

运行类似 `cat typescript | less` 的命令将打印出你输入的所有内容。

# AppleScript

虽然在技术上不是 UNIX 的东西，但 AppleScript 在 Mac OS X 机器上可用，并且可以被系统管理员极有效地使用。AppleScript 被设计成一种非常像英语的语言，用于在 Mac 上执行操作。典型的示例展示了如何创建对话框来用于复制文件、下载 URL，或者控制 iTunes 或 iCloud。

你可以使用任何文本编辑器创建 AppleScript，但大多数情况下，你都会使用“脚本编辑器”（位于 `/Applications/AppleScript`）。当你打开脚本编辑器（见图 6-1）时，你使用一个简单的编辑器，允许你输入命令、运行它们并记录它们。

在打开脚本编辑器的情况下，让我们创建你的第一个 AppleScript，诚然这是自今为止编写过最没用的程序之一，但你必须从某处开始：

```
display dialog "I am a dialog box." --这是一个注释
```

输入此内容后，点击“运行（Run）”按钮。如图 6-2 所示，`display dialog` 会打开一个对话框，其中打印了参数（在这种情况下，是“I am a dialog box”）。两个破折号（`--`）被视为注释标记——编译器会忽略该行中之后的任何内容。

让我们创建一个更有实用的东西，一些可以帮助我们进行管理工作。假设我们想要监控一个包含特定文件的文件夹，例如 Web 服务器根目录下的文件。再次，我们将使用 MAMP 示例（`/Applications/MAMP/`）。

# 第 6 章：高级脚本

首先，在桌面上右键点击（或按住 Control 点击），并从菜单中选择“更多 ⌥ 启用文件夹操作”。打开一个新的 Finder 窗口并导航到 `/Applications/MAMP` 文件夹。在 `hdocs` 文件夹上右键点击（或按住 Control 点击），并选择“更多 ⌥ 附加文件夹操作”，如图 6-3 所示。

![](img/d850b48b6750d726fcc813a2a895d7cc_110_0.png)

图 6-1：脚本编辑器

![](img/d850b48b6750d726fcc813a2a895d7cc_110_1.png)

图 6-2：你的第一个简单 AppleScript

![](img/d850b48b6750d726fcc813a2a895d7cc_111_0.png)

图 6-3：文件夹操作

文件夹操作（Folder actions）基本上是已经附加到文件夹的 AppleScript，它们在许多语境下都可以证明是无限帮助的。幸运的是，Mac OS X 有一组你可以立即使用的示例脚本。这些脚本位于 `/Library/Scripts/Folder Actions`。其中一个我们可以直接使用。

![](img/d850b48b6750d726fcc813a2a895d7cc_111_1.png)

图 6-4：文件夹操作



# 第 6 章：高级脚本

在打开脚本编辑器的情况下，让我们创建你的第一个 AppleScript，诚然这是自今为止编写过最没用的程序之一，但你必须从某处开始：

```
display dialog "I am a dialog box." --这是一个注释
```

输入此内容后，点击“运行（Run）”按钮。如图 6-2 所示，`display dialog` 会打开一个对话框，其中打印了参数（在这种情况下，是“I am a dialog box”）。两个破折号（`--`）被视为注释标记——编译器会忽略该行中之后的任何内容。

让我们创建一个更有实用的东西，一些可以帮助我们进行管理工作。假设我们想要监控一个包含特定文件的文件夹，例如 Web 服务器根目录下的文件。再次，我们将使用 MAMP 示例（`/Applications/MAMP/`）。

首先，在桌面上右键点击（或按住 Control 点击），并从菜单中选择“更多 ⌥ 启用文件夹操作”。打开一个新的 Finder 窗口并导航到 `/Applications/MAMP` 文件夹。在 `hdocs` 文件夹上右键点击（或按住 Control 点击），并选择“更多 ⌥ 附加文件夹操作”，如图 6-3 所示。

![](img/d850b48b6750d726fcc813a2a895d7cc_110_0.png)

图 6-1：脚本编辑器

![](img/d850b48b6750d726fcc813a2a895d7cc_110_1.png)

图 6-2：你的第一个简单 AppleScript

85

![](img/d850b48b6750d726fcc813a2a895d7cc_111_0.png)

文件夹操作（Folder actions）基本上是已经附加到文件夹的 AppleScript，它们在许多语境下都可以证明是无限帮助的。幸运的是，Mac OS X 有一组你可以立即使用的示例脚本。这些脚本位于 `/Library/Scripts/Folder Actions`。其中一个我们可以直接使用。

图 6-3：文件夹操作

![](img/d850b48b6750d726fcc813a2a895d7cc_111_0.png)

在继续之前，让我们花一点时间注意一下 shell 脚本中的一些特殊之处。例如，在结束一个 `if case` 语句时，你有没有注意到 `fi` 和 `esac` 的使用？这些标记符标志着你脚本中条件部分的结束。

注意 `if` 周围的括号。在左侧的括号 `(` 之后和右侧的括号 `)` 之前需要有一个空格。前面的测试如果没有加空格，将导致语法错误。

```
if [$ -eq "0" -o $ -gt "1"] #error! 无法计算！
```

这是另一个会让初学 shell 脚本编写感到困扰的问题。当你第一次设置变量的值时，不要在变量名、等号和值之间加上空格：

```
MYCOL = 14 #error! shell 尝试寻找一个名为 MYCOL 的命令
MYCOL=14 #这就没问题
```

此外，当你准备好使用你的新变量时，记得在名称前面加上一个 `$`符号：

```
echo $MYCOL #打印 14
```

# 使用 script 命令

有时你想要一份你所工作内容的转录，用于学习或审计之目的。`script` 命令可以让你实现这一点。在命令行上不带参数调用 `script` 命令将将所有命令及其命令的输出保存到名为 `script` 的文件中。

这里有一个最近脚本会话的转录，用于说明。请注意日期、运行时间以及 `df` 命令都被记录了，以及它们的输出。还请注意我按了 `Ctrl-D` 来退出转录过程。

```
Macintosh:desktop myerman$ script
Script started, output file is typescript
bash-3.2$ date
Mon Nov 17 13:32:39 CST 2008
bash-3.2 uptime
13:42 up 2 days, 23:54, 2 users, load averages: 0.97 0.77 0.54
bash-3.2 df -h
Filesystem Size Used Available Capacity Mounted on
/dev/disk02 144Gi 88Gi 60Gi 60% /
devfs 108Ki 0Ki 108Ki 100% /dev
fdesc 1.0Gi 1.0Gi 0Bi 100% /dev
map -hosts 0Bi 0Bi 0Bi /net
map_auto_home 0Bi 0Bi 0Bi 100% /home
bash-3.2 exit
Script done, output file is typescript
```

运行类似 `cat typescript | less` 的命令将打印出你输入的所有内容。

# AppleScript

虽然在技术上不是 UNIX 的东西，但 AppleScript 在 Mac OS X 机器上可用，并且可以被系统管理员极有效地使用。AppleScript 被设计成一种非常像英语的语言，用于在 Mac 上执行操作。典型的示例展示了如何创建对话框来用于复制文件、下载 URL，或者控制 iTunes 或 iCloud。

你可以使用任何文本编辑器创建 AppleScript，但大多数情况下，你都会使用“脚本编辑器”（位于 `/Applications/AppleScript`）。当你打开脚本编辑器（见图 6-1）时，你使用一个简单的编辑器，允许你输入命令、运行它们并记录它们。

# 第 6 章：高级脚本编写

检查你使用的不同工具是一个好主意，可以看看它们是否提供了你可以利用的额外命令行工具。

![](img/d850b48b6750d726fcc813a2a895d7cc_115_0.png)

图 6-8：通过命令行工具向 BBEdit 发输出

### 总结

在本章中，你进一步了解了 shell 脚本和 AppleScript 脚本。你还学习了如何通过 `open` 命令执行涉及 Mac 应用程序的更高级的任务，并且你对这些强大的工具变得更加熟悉。

## 管理文件系统

文件系统提供了从你的 Mac OS X 访问文件、目录、设备和其他系统元素的结构基础。Mac OS X 支持许多不同的文件系统，包括 HFS+（默认）、HFS、UFS、AFP、ISO 9660、FAT、UDF、SMBFS、NTFS（只读）、FTP 和 WebDAV。

HFS+ 是 Mac OS X 的首选文件系统。它支持许多高级功能，例如日志记录、配额、字节范围锁定、元数据中的 Finder 信息、多种编码，以及符号链接、别名、对文件扩展名的支持等。

创建和管理磁盘分区以及分区上的文件系统是管理 Mac OS X 系统最关键的工作之一。这是因为如果你搞乱了文件系统，你可能会丢失计算机硬盘或可移动介质上的关键数据。

本章包含了用于存储介质的分区、创建文件系统、挂载和卸载文件系统，以及检查文件系统错误和磁盘空间的命令。

### 理解文件系统基础

如果你是从其他 BSD 或 Linux 背景转到 Mac OS X，你首先需要知道的是 Mac 分区被称为“卷”（volumes）。每个卷代表硬盘上的一个可寻址区域，并分配了特定的功能：独立的操作系统（例如 Linux 或 Windows XP）、文件存储、交换空间等。

通常情况下，你可能不想更改默认的卷设置；但如果你发现自己处于需要支持不同操作系统或想要不同的文件系统设置的境地，那么你可能需要对系统进行分区。我们将在本章稍后讨论这一点。

分区你的 Mac OS X 系统将导致上面的所有数据被擦除！

### 初始化磁盘

如果你习惯于使用其他 BSD 变体或 Linux，你可能习惯了使用如 `fdisk` 等工具进行初始磁盘设置。你的 iMac、MacBook Pro 或 Mac Pro 极不需要这一步骤，因为它们出厂时已经配备了启动所需的所有设置好的工具。

# 检查你的磁盘设置

你可以随时使用 `mount` 命令检查你的磁盘设置。该命令显示了磁盘空间是如何分配在多个分区之间的，这些分区随后被挂载在文件系统的不同位置：

```
$ mount Display mounted disk partitions
/dev/disk02 on / (hfs, local, journaled)
devfs on /dev (devfs, local)
fdesc on /dev (fdesc, union)
map -hosts on /net (autofs, automounted)
map -auto_home on /home (autofs, automounted)
```

接下来，要查看磁盘空间在硬盘分区之间的分布情况，你可以按照如下方式使用 `df` 命令：

```
$ df -h Display disk space usage
Filesystem Size Used Avail Capacity Mounted on
/dev/disk02 149Gi 88Gi 60% /
devfs 108Ki 08Ki 100% /dev
fdesc 1.0Ki 0Ki 100% /dev
map -hosts 0Bi 0Bi 100% /net
map -auto_home 0Bi 0Bi 100% /home
```

此示例将 150GB 分配给了根分区 `/`，你会在桌面上看到 Macintosh HD 图标。目前，该特定系统的根分区已用了 60%，剩余 60GB 空闲空间。

### 理解文件系统类型

使用 Mac OS X 时，你只需要几种不同的文件系统类型。分级文件系统+（HFS+）被默认用于大多数磁盘存储需求。

HFS+ 在架构上与 HFS 相似，但有若干改进：

- 使用 32 位用于分配块（而不是 16 位）。HFS 使用分配块划分分区上的磁盘空间。使用 32 位标识分配块会导致比使用 16 位浪费更少的空间（并能容纳更多文件）。
- 长文件名——多达 255 个字符
- 基于 Unicode 的文件名编码
- 文件和目录的属性在未来可以扩展（而不是受限于固定大小）
- 最大文件大小为 2^63 字节

然而，在某些情况下，你可能想在 Mac OS X 上使用其他文件系统类型，包括：

- 其他本地操作系统：如果你的硬盘上安装了多个操作系统（如 Windows、DOS 或 Linux），你可能想访问包含这些系统的分区中的数据（即使只是为了读取数据）。



- 其他介质：你可能有一张 CD、DVD、备份带或其他包含其他文件系统类型格式数据的介质。即使在 Mac OS X 无法创建某些类型的文件系统的情况下，它也可能挂载并使用这些系统。

本章中的大多数示例都使用 HFS+ 文件系统来说明如何操作。表 7-1 列出了文件系统类型并描述了何时使用它们。

## 表 7-1：OS X 支持的文件系统类型

| 文件系统类型 | 描述 |
|---|---|
| HFS+ | Mac OS X 首选文件系统。它支持日志记录、配额、字节范围锁定、元数据中的 Finder 信息、多种编码、符号链接、别名、按文件扩展名等。 |
| ufs | 用于 FreeBSD 和其他 BSD 系统的默认文件系统。Darwin 对 UFS 的实现与 NEXTSTEP 类似。 |
| mdos | DOS 文件系统（FAT12、FAT16 和 FAT32）。 |
| iso9660 | 用于大多数 CD 的系统无关文件系统。 |
| ntfs | 微软的技术文件系统（NTFS）。当你需要与 Windows 系统共享时（双系统或移动驱动器）。支持只读。 |

## 表 7-1：OS X 支持的文件系统类型（续）

| 文件系统类型 | 描述 |
|---|---|
| udf | UDF（通用磁盘格式）用于 DVD-ROM（包括 DVD 视频和音频）以及许多光盘刻录程序。 |

除了表 7-1 列出的文件系统外，还有所谓的网络文件系统。本地网络共享文件系统可以是 ufs、ntfs 或其他普通文件系统。然而，这些文件系统的全部或部分可以通过 Samba (`smbfs`)、NFS (`nfs`) 和 NetWare (`nwfs`) 协议进行共享。

关于这些内容的详细讨论，请参考 `kernelthread.com/mac/osx/arch_fs.html`。

你可以使用后续章节中的程序来创建、管理、挂载以及其他描述的文件系统类型。

### 创建和管理文件系统

Mac OS X 提供默认的分区和文件系统方案，但你可以轻松地对系统进行分区。后续章节提供了如何操作的详细说明。

### 分区硬盘

要重新划分系统，请从 Mac OS X 安装磁盘启动。插入自带的安装磁盘，并在重启时按住 C 键，直到系统重启并看到苹果图标。

要对硬盘进行分区，请遵循以下步骤：

1. 从安装程序菜单选择“磁盘工具”。在打开的窗口中，点击左侧点击要初始化或分区的驱动器图标。
2. 在右侧点击“分区”选项卡。
3. 在卷方案弹出菜单下；选择初始化过程中要创建的分区数量。
4. 选择好分区数量后，通过拖动代表分区边界的柄来调整它们的大小。
5. 点击每个分区以调整其属性。在卷信息下选择你想要使用的格式。默认选项是 Mac OS 扩展（日志记录）。
6. 点击“分区”（`Partition`）。
7. 在驱动器格式化并分区后，继续从您的安装盘进行其他安装。您将需要重新安装任何想要使用的操作系统（例如 Mac OS X、Linux 等）。

### 更好的选项：无破坏性分区

当且仅当您已经执行了最近的备份（使用 Time Machine [时间机器] 或其它选项）时，重启您的 Mac OS X 系统，并在重新启动时按住 S 键。

这将以单用户模式启动您的 Mac，该模式与 Linux 或 UNIX 系统上的命令行终端（shell）非常相似。一旦启动，输入以下命令来启动基本服务：

```
shell /etc/rc
```

使用以下命令获取系统中当前卷卷的信息：

```
diskutil list
```

| | 类型 (TYPE) | 名称 (NAME) | 大小 (SIZE) | 标识符 (IDENTIFIER) |
|---|---|---|---|---|
| 0: | GUID_partition_scheme | *149.1 Gi | disk0 |
| 1: | EFI | 200.0 Mi | disk01 |
| 2: | Apple_HFS Macintosh HD | 148.7 Gi | disk2 |

如果你想将 Macintosh HD 分分为两个分区（其中一个包含 120GB 空间，另一个包含剩余所有空间），你必须先通过以下命令确定磁盘是否可以调整大小：

```
diskutil resizeVolume disk02 120G
```

```
For device disk02 Macintosh HD:
Current size: 159697911808 bytes
Minimum size: 95972585472 bytes
Maximum size: 159697911808 bytes
```

如你所见，该卷的当前大小为 159GB。你可以将其调整的最小大小是 95GB，因此你将在 120GB 边界处分区的计划恰恰当。要实际调整卷的大小，请使用以下命令（注意我们正在创建一个 JHFS+ 分区用于安装 Mac OS 9）：

```
diskutil resizeVolume disk02 120G JHFS+ Development 20G
```

一旦输入此命令，屏幕上会闪过多条消息，指示重新分区驱动器目标的进度。一旦完成，在正常模式下重启。你可能需要告诉 Mac OS X 要从哪个分区启动。

### 文件系统的挂载与卸载

在可以使用普通文件系统之前，您需要通过通过将其“挂载”（mounting）来附加到计算机文件系统树中的某个目录下。您的根文件系统 (`/`) 以及您在运行中使用的其他文件系统通常由 Mac OS X 自动挂载。然而，有时您需要手动挂载文件系统。

`mount` 命令用于查看已挂载的文件系统，以及挂载任何本地（硬盘、USB 驱动器、CD、DVD 等）或远程（NFS、Samba 等）文件系统。以下是列出文件系统的 `mount` 命令示例：

```
$ mount
/dev/disk0s2 on / (hfs, local, journaled)
devfs on /dev (devfs, local)
fdesc on /dev (fdesc, union)
map -hosts on /net (autofs, automounted)
map auto_home on /home (autofs, automounted)
```

使用 `-t` 选项仅列出特定文件系统类型的挂载：

```
$ mount -t hfs
/dev/disk0s2 on / (hfs, local, journaled)
```

这是一个将本地文件系统（`/dev/ad0s4` 设备）挂载到现有目录 `/mnt/music` 的简单命令：

```
### mount /dev/ad0s4 /mnt/music
### mount -v /dev/ad0s4 /mnt/music/
Mount file system, more verbose
```

使用 `-t` 显式指定文件系统类型：

```
### mount -v -t ext2fs /dev/ad0s4 /mnt/music/ Mount an ext2 file system
/dev/ad0s4 on /mnt/music (ext2fs, local, fsid 5e00000008000000)
```

你可以通过使用 `-a` 和由逗号分隔的选项列表来指定挂载选项。默认情况下，分区是以读/写权限挂载的。你可以显式指定将文件系统挂载为读/写 (`rw`) 或只读 (`ro`)：

```
### mount -v -t ext2fs /dev/ad0s4 /mnt/music Mount read-write
/dev/ad0s4 on /mnt/music (ext2fs, local, fsid 5e00000008000000)
### mount -v -t ext2fs -o ro /dev/ad0s4 /mnt/music Mount read-only
/dev/ad0s4 on /mnt/music (ext2fs, local, fsid 5e00000008000000)
```

你还可以包含以下其他有用的 `mount` 选项：

- `- noatime`: 不更新文件的访问时间。对于 I/O 密集的文件系统（如池和日志）很有帮助。
- `- noexec`: 防止在该文件系统上执行二进制文件。可用于增加安全性——例如，对于存在不可信用户环境下的 `/tmp`。

要卸载文件系统，请使用命令卸载文件系统。你可以通过设备名或挂载点来卸载文件系统。

### 文件系统检查与修复

```
# 第 4 阶段 - 检查丢失文件
2712 个文件，610448 空闲 (38153 个簇)
```

如果 `fsck` 在文件系统检查期间遇到错误（且你没有指定 `-y` 来自动响应并继续），你可以交互式确认是否要修复这些错误。这是一个示例：

```
### fsck_msdosfs /dev/da0s2
** /dev/da0s2
** 第 1 - 读取并比较 FAT
** 第 2 - 检查簇链
** 第 3 - 检查目录
/hello.txt 起于空闲簇
截断吗？ [yn] y
** 第 4 - 检查丢失文件
2713 个文件，610448 空闲 (38153 个簇)
标记文件系统为清洁？ [yn] y
标记文件系统为清洁
```

检查带有错误的文件系统

***** 文件系统已修改 *****

在前面的示例中，当插入文件的内存条被拔出时，文件 `hello.txt` 正在文本编辑器中打开。随后的文件系统检查显示了该错误，可以通过输入 y 进行修复。

### 查找文件系统使用情况

磁盘空间耗尽在你的桌面系统上可能令人苦恼，而在你的服务器上则可能是场灾难。要确定可用多少磁盘空间以及当前使用了多少，请使用 `df` 命令。要检查特定文件和目录消耗多少空间，请使用 `du` 命令。

`df` 命令提供挂载文件系统的利用率摘要。使用 `-h` 选项，你可以将数据（默认以字节显示）转换为千字节（K）、兆字节（M）和吉字节（G），使输出对人类易读：

| 大小 | 已用 | 可用 | 容量 | 挂载点 |
| :--- | :--- | :--- | :--- | :--- |
| /dev/da0s | 49M | 417M | 9% | / |
| devfs | 1.0K | 1.0K | 0B | 100% | /dev |
| /dev/da0s1 | 496M | 456M | 0% | /tmp |
| /dev/da0sif | 16G | 39M | 23% | /usr |
| /dev/da0sid | 1.2G | 19M | 1.1G | 2% | /var |
| /dev/da0s2 | 7.3G | 593M | 6.4G | 8% | /mnt/debian |
| /dev/da0s1 | 48M | 856K | 45M | 2% | /mnt/da0s1 |

保存到文件系统的每个文件都可能导致你耗尽 inode（索引节点）。如果文件系统包含许多小文件，`df` 命令检查 inode 利用率的方法是使用 `-i` 选项：

| 显示可用和已使用的 inode 数 |
| 文件系统 | 大小 | 已用 | 可用 | 已用容量 | 空闲 %用 | 挂载点 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/ad0s | 496M | 39M | 417M | 9% | 1117 | 64673 | 2% | /dev |
| devfs | 1.0K | 1.0K | 0 | 100% | 0 | 100% | /dev |
| /dev/ad00 | 496M | 34M | 456M | 0% | 17 | 65773 | 0% | /Temp |
| /dev/ad0sif | 1.6G | 35G | 12G | 23% | 198316 | 50750 | 0% | /usr |
| /dev/ad0sid | 1.2G | 19M | 1.1G | 2% | 2523 | 162339 | 2% | /var |

如果你有网络挂载（如 Samba 或 NFS），这些也会出现在 `df` 输出中。要将 `df` 限制为本地文件系统，请使用 `-l`（代表 local）选项：

```
$ df -hl
仅显示本地文件系统的空间
```

要显示特定文件系统类型的输出，请使用 `-T` 选项：

```
$ df -ht ufs
仅显示 ufs 文件系统类型
```

| 文件系统 | 大小 | 已用 | 可用 | 容量 | 挂载点 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/ad00 | 496M | 39M | 417M | 9% | / |

要检查文件系统中特定文件或目录的磁盘占用情况，请使用 `du` 命令。以下命令是以用户名为 marlow 的用户运行的：

```
$ du -h /Users/
显示 /home 目录的磁盘空间占用
du: /Users/kafka: Permission denied
4.0K /Users/marlow/Mail
52K /Users/marlow
64K /Users/
```

输出显示访问另一个主目录的磁盘使用情况（在此例中为 kafka）被拒绝。由于权限原因，tar 显示了备份：

```
$ du -h /Users/
显示 /home 目录的磁盘空间占用
du: /Users/kafka: Permission denied
4.0K /Users/marlow/Mail
52K /Users/marlow
64K /Users/
```

### 归到 tar 备份数据

如果你来自 Windows 背景，可能习惯了 WinZip 等工具进行归档和压缩。

### 使用 tar 创建归档

`tar` 命令全称为 tape archiver，可以追溯到早期的 UNIX 系统。虽然磁带曾是常见的媒介，但今天 `tar` 主要用于创建各种媒介的归档。

`tar` 命令功能丰富，具有许多选项。基本操作包括创建归档 (`-c`)、从归档提取文件 (`-x`) 以及更新归档中的文件 (`-u`)。我们还可以向归档追加文件 (`-r`) 或列出归档内容 (`-t`)。使用 `tar` 命令的情况源于 `tar` 创建于关于输入选项的标准之前。虽然你可以为 `tar` 选项加上横杠，但并非总是必要的。例如，你可能会看到一个经典的示例从当前目录下的所有 `.txt` 文件创建一个归档。而不是写入默认磁带设备（`/dev/sa0`），`f` 选项表示将输出重定向到文件（或者使用 `-` 表示标准输出），`t` 输出通过管道传递给 `gzip` 命令，输出到 stdout，然后重定向到 `myfiles.tar.gz` 文件。注意，`tar` 是不需要输出到横杠（`-`）的命令之一。

新的 `tar` 版本、现代 BSD 系统，可以在一步内创建归档并压缩输出：

```
$ tar czf myfiles.tar.gz *.txt Created gzip of .txt files
$ tar czvf myfiles.tar.gz *.txt Be verbose creating archive
text1.txt
text2.txt
```

在刚刚示例中，注意新的归档名称（`myfiles.tar.gz`）必须紧跟在 `f` 选项之后。否则，`tar` 的输出将定向到默认磁带设备（`/dev/sa0`）或 stdout（如果你使用 `-` 代替文件名）。`z` 选项表示 gzip 压缩，并产生处理过程的详细描述。注意 Solaris 不支持 `-z` 来管理 gzip 格式的归档。Star（读作 tar）支持访问控制列表（ACL）和文件标志（用于 Samba 的扩展权限）。

# 第 8 章：备份与可移动介质

当你想要将文件还原到文件系统（解压缩和解 tar 包），你也可以通过单步或两步处理过程来实现，具体使用 `tar` 命令以及可选的 `gunzip` 命令：

```
$ gunzip -c myfiles.tar.gz | tar xf -
```



## 解压并解 tar 归档

或者，尝试以下命令行：

```
$ gunzip myfiles.tar.gz ; tar xf myfiles.tar
```

先解压再解 tar 归档

上一个命令会删除 `tar.gz` 文件，只留下 `.tar` 文件。要一步到位完成相同的操作，你可以使用以下命令：

```
$ tar xvf myfiles.tar.gz
x textfile.txt
x textfile2.txt
```

上述命令的结果是相同的：归档中的 `.txt` 文件被复制到当前目录。`x` 选项提取文件，`z` 选项解压缩（解压）文件，`v` 产生输出，而 `f` 表示下一个选项是归档文件的名称（`myfiles.tar.gz`）。

## 使用压缩工具

压缩是处理备份文件的一个重要方面。它可以在你的备份介质（CD、DVD、磁带等）或服务器上占用更少的磁盘空间存储文件。将归档传输到其他介质或通过网络下载文件也需要时间。

尽管压缩可以节省大量的存储空间和传输时间，但它会显著增加 CPU 使用率。你可以考虑在磁带驱动器使用硬件压缩（参见 http://tinyurl.com/5z60lt）。

> 注意：查看 `mt` 命令的 man 页面，详细了解如何通过软件为大多数磁带驱动器设置压缩。

在上一节所示的示例中，`tar` 调用了 `gzip` 命令，但 `tar` 可以与许多压缩工具配合。在 Mac OS X 上，`tar` 原生支持 `gzip` 和 `bzip2`。前者速度更快，而后者提供了更高的压缩率。

如果你正在归档和压缩大量数据，压缩备份所需可能会非常显著。然而，通过每个压缩命令，你可以选择不同的压缩级别，以平衡对更高压缩率的需求与压缩所需的时间。

# 第 8 章：备份与可移动介质

要使用 `tar` 命令配合 `bzip2` 压缩，请使用 `-j` 选项：

```
$ tar cvf myfiles.tar.bz2 *.txt    创建归档，并用 bzip2 压缩
```

你也可以在使用 `tar` 命令提取文件（`-x`）的同时，解压缩（`-j`）bzip2 压缩的文件：

```
$ tar xvf myfiles.tar.bz2    提取文件，解压缩 bzip2 压缩
```

### 使用 gzip 压缩

如所述，你可以单独使用任何一个压缩命令（而不是在命令行内部使用）。此示例使用 `gzip` 命令来创建和处理 `gzip` 压缩的文件：

```
$ gzip myfile          gzip压缩 myfile 并将其重命名为 file.gz
```

下一个命令提供相同的结果，但带有详尽的输出：

```
$ gzip -v myfile      带详尽输出的 gzip myfile
myfile: 86.0% -- replaced with myfile.gz
$ gzip -tv myfile      测试 gzip 文件的完整性
myfile.gz:           OK
$ gzip -lv myfile      获取 gzip 文件的详细信息
method crc    time    uncompr. ratio uncompressed_name
defla 027d9e4 Jul 10 04:48  46785    334045 86.0% myfile
```

使用以下命令之一压缩目录下的所有文件：

```
$ gzip -rv mydir      压缩目录下的所有文件
mydir/file1: 39.1% -- replaced with mydir/file1.gz
mydir/file2: 39.5% -- replaced with mydir/file2.gz
$ gzip -1 myfile       压缩最快，压缩率最低
$ gzip -9 myfile       压缩最慢，压缩率最高
```

在 1 到 9 的数字前加上连字符来设置压缩级别。如前所示，`-1` 是最快（最小）压缩，`-9` 是最慢（最高）压缩。`gzip` 的默认级别是 6。`lzip` 命令的级别较少：1、3（默认）。`bzip2` 的压缩级别行为不同。

要解压压缩文件，你可以使用 `gunzip` 命令。使用以下任一即可：

```
$ gunzip -v myfile.gz   解压 myfile.gz 并将其重命名为 myfile
myfile.gz:           86.0% -- replaced with myfile
$ gzip -dv myfile.gz     与之前的命令行相同
```

尽管所示的示例指的是压缩普通文件，但相同的选项也可以用于压缩 `tar` 归档。

### 使用 bzip2 压缩

`bzip2` 命令被认为在本章描述的压缩工具中提供了最高的压缩率。以下是 `bzip2` 的示例：

```
$ bzip2 myfile                压缩文件并将其重命名为 file.myfile
$ bzip2 -v myfile            与上一个命令相同，但输出更详尽
myfile: 9.529:1, 0.840 bytes/byte, 89.51% saved, 330415 out, 35056 out.
$ bzip2 myfile.bz2           解压缩文件并将其重命名为 myfile
$ bzip2 -d myfile.bz2        与上一个命令相同
$ bzip2 -v myfile.bz2       带详尽输出的 bzip2 myfile
myfile.bz2: done
```

## 列出、合并和添加文件到归档

到为止，我们已经使用 `tar` 创建并解压归档。现在还有一些选项可以列出归档内容、合并归档以及向现有归档添加文件。要列出归档的内容，使用 `-t` 选项：

```
$ tar -tf myfile.tgz      列出 gzip 压缩归档
```

使用 `-r` 选项向现有归档添加一个或多个文件。在下面的示例中，归档了 myfile：

```
$ tar rf archive.tar myfile    添加 myfile
```

你可以使用通配符将多个文件添加到归档：

```
$ tar rf archive.tar *.txt    将多个文件添加到归档
```

### 通过网络进行备份

当你备份了文件并将它们整合到 `tar` 归档后，该如何处理它们？创建备份的主要原因是在发生某些意外情况（如磁盘崩溃）时，你需要从备份中恢复文件。你可以采用以下方法来确保备份安全：

- 复制到可移动介质，如磁带、CD 或 DVD（在本章稍后介绍）
- 复制到网络上的其他机器

快速可靠的网络；廉价的大容量硬盘以及数据的安全性使得网络备份成为流行的做法。对于个人数据备份或小型办公室，组合几个简单的命令可能足以创建高效且安全的备份。这种方法直接应用了 UNIX 哲学：组合只执行单一功能的简单程序来完成复杂的任务。

尽管任何可以通过网络复制文件的命令，但某些工具更适合这项工作。使用 OpenSSH 工具（如 `ssh` 和 `scp`），你可以安全地传输归档并对这些归档进行加密传输。

诸如 `rsync` 的工具通过备份自上次备份以来更改的文件（或文件部分）来节省资源。接下来的章节将描述其中一些通过网络将你的数据备份到其他机器的技巧。

> 一个可能让你感兴趣的类似工具是 `snapshot` 命令（pkgadd -r snapshot）。`snapshot` 命令 (.snapshot.org/) 可以与 `rsync` 配合工作，创建每小时、每日、每周或每月快照。它使用硬链接保留文件系统的快照，然后可以与更改的文件进行同步。

### 通过 ssh 备份归档

OpenSSH (www.openssh.org/) 提供了安全执行远程登录、远程执行和远程文件复制的工具。通过设置两台机器共享加密密钥，你可以在这些机器之间传输文件而无需每次输入密码。这允许你创建脚本，从 SSH 客户端备份数据到 SSH 服务器，而无需任何手动干预。

从一个中央 BSD 系统，你可以使用 OpenSSH 命令从多个客户端机器收集备份。下面的示例在远程站点运行 `tar` 命令（对文件进行归档和压缩），将 `tar` 通过管道传输到标准输出，并使用 `ssh` 命令在本地（通过 ssh）接收备份（与 `tar` 配合使用 `-`）：

```
$ mkdir mybackup; cd mybackup
ssh kafka@server1 'tar cf myfile*' | tar xvf -
kafka@server1's password: ******
myfile
myfile2
```

要反转该过程并将文件从本地系统拷贝到远程系统，请运行本地 `tar` 命令。然而，这次我们使用 `cd` 命令将文件放入远程机器上选择的目录中：

```
$ tar cf - myfile | ssh kafka@server1 \
  cd /Users/kafka/myfolder; tar xvf - \
  kafka@server1's password: *****
myfile
myfile2
```

在接下来的示例中，我们不会在接收端解压文件，而是将规则写入 `tgz` 文件中：

```
$ ssh kafka@server1 'tar czf - myfile*' | cat > myfiles.tgz
$ tar cvf myfile | ssh kafka@server1 'cat > myfiles.tgz'
```

第一个示例从 server1 上 kafka 的家目录获取所有以 `myfile` 开头的文件，将其 tar 归档并压缩，并将压缩后的文件重定向到 `myfiles.tgz`。第二个示例演示了相反的操作，将本地目录中所有以 `myfile` 开头的文件发送到远程系统上的 `myfiles.tgz` 文件中。

刚刚显示的示例适用于通过网络拷贝文件。除了提供压缩功能外，它们还允许你使用选择的 `tar` 特性，例如增量备份功能。

### 使用 rsync 备份文件

`rsync` 是一个功能丰富的备份命令。`rsync` 的独特之处在于 `rsync` 算法，它使用校验和对逐块比较本地和远程文件，并仅传输不同的块。该算法非常高效，已被许多备份产品复用。

`rsync` 命令可以在远程 shell (ssh) 之上运行，也可以通过服务器端运行 `rsync` 守护进程。以下示例通过 ssh 使用 `rsync` 镜像目录：

```
$ rsync -avz --delete marlowe@server1:Users/marlowe/pics/ mypics/
```

上述命令旨在将远程目录结构（/Users/marlowe/pics/）镜像到本地系统上的目录（`mypics/`）。`-a` 表示归档模式（递归拷贝远程目录中的所有文件），`-z` 压缩文件，`-v` 输出详细信息。`--delete` 让 `rsync` 删除本地系统中在远程系统中已不存在的任何文件。

对于持续备份，你可以让 `rsync` 执行七天增量备份。这里有一个示例：

```bash
### mkdir /mnt/backups
# rsync --delete --backup \
  --backup-dir=/mnt/backups/backup-`date +A` \
  -avz marlowe@server1:/Users/marlowe/Personal/ \
  /mnt/backups/current-backup/
```

当命令运行时，远程服务器上 `/Users/marlowe/Personal` 的所有文件将被拷贝到本地目录 `/mnt/backups/current-backup`。命令第一次运行时，所有文件都会备份到备份目录。下一次命令运行（在第二天），所有当天修改的所有文件都将拷贝到一个以星期几命名的目录中，例如 `/mnt/backups/backup-Monday`。在一周内，将创建相应的目录来反映过去七年的每一年。

轮转备份的另一个技巧是使用硬链接而不是多个文件副本。这个二步过程包括轮转文件，然后运行 `rsync`：

```bash
### rm -rf /mnt/backups/backup-old/
### mv /mnt/backups/backup-current /mnt/backups/backup-old/
# rsync --delete --link-dest=/mnt/backups/backup-old -avz \
marlowe@server1:/Users/marlowe/Personal/ /mnt/backups/backup-current/
```

在之前的过程中，现有的 `backup-current` 目录替换了 `backup-old` 目录，将两周前的备份与上周的备份一起删除。当使用 `--link-dest` 选项通过 `rsync` 执行新的全量备份时，如果从远程 `Personal` 目录备份的任何文件存在于之前的备份中（现在位于 `backup-old` 中），则会在 `backup-current` 目录中的文件与 `backup-old` 目录之间创建一个硬链接。

通过 `backup-old` 和 `backup-current` 目录的文件之间建立硬链接，你可以节省大量空间。例如，如果你在两个目录中都有名为 `file.txt` 的文件，你可以通过如下列出文件的 inode 来检查它们是否是同一个文件：

```
$ ls -i /mnt/backups*/file.txt
260761 /mnt/backups/backup-current/file.txt
260761 /mnt/backups/backup-old/file.txt
```

### 备份到 CD 或 DVD

默认情况下，如果你向 Mac OS X 系统插入 CD 或 DVD，系统将提示你执行操作。你可以通过选择“偏好设置 -> CDs 和 DVD”，并对不同的行为做出响应（例如插入空白 CD）来更改此默认行为。

通过 GUI 备份到 CD 或 DVD 是一个三个步骤：

1. 在桌面上按 Control 点击或右键点击选择“创建刻录文件夹”（Create Burn Folder）。
2. 选择你想移动到 CD 的项目，并将它们拖到新创建的刻录文件夹中。
3. 在 Finder 中打开刻录文件夹，并在准备好备份到 CD 或 DVD 时点击“刻录”（Burn）（参见图 8-1）。

![](img/d850b48b6750d726fcc813)
图 8-1：使用刻录文件夹备份到 CD

### 使用 Time Machine 和 Time Capsule

备份整个 Mac OS 安装的最简单方法是运行 Time Machine。从 GUI 中设置 Time Machine 偏好设置，然后连接 FireWire 或 USB 硬盘、网络连接硬盘（如 Time Capsule）或其他存储设备。

Time Machine 首先会对整个 Mac OS 卷进行备份到目标驱动器，然后对任何更改进行每小时备份。

然而，某些用户可能想要更改备份频率（例如每四小时一次而不是每小时），或者从备份过程中排除目录。许多开发者使用 SVN 或其他系统来管理源代码和关联文件，因此不需要每小时备份提供的保护。

如果你运行的是 Leopard (Mac OS X 10.5)，下载名为 Time Scheduler 的优秀免费软件（位于 www.xieme.com/TimeScheduler.html）并安装它。Time Scheduler 允许你更改备份间隔、在特定跳跳备份以及运行手动备份。

注意某些用户仍然需要从命令行启动 Time Machine 备份——例如，通过远程 SSH 会话。要这样做，请使用以下命令：

```
/System/Library/CoreServices/backup.bundle/Contents/Resources/backup-helper &
```

你也可以将其添加到 iCal 事件，以便在指定时间运行手动备份。只需创建一个如下内容的 AppleScript 并将其附加到 iCal 事件：

```
do script "/System/Library/CoreServices/backup.bundle/Contents/Resources/backup-helper &"
```

你可以通过以下命令重置 Time Machine 的间隔：

```bash
sudo defaults write /System/Library/LaunchDaemons/com.apple.backupd-auto StartInterval -int 7200
```



默认间隔为 3600 秒（一小时）。你需要知道 `sudo` 密码才能使此命令生效。

## 总结

BSD 及其前身 Unix 系统通过组合每个处理离散功能集的命令来处理数据备份。你仍然可以使用这种方法备份你的关键数据。事实上，你使用的许多工具比以前任何时候都更安全、高效。

带归档（`tar` 命令）已经远远扩展了其最初制作磁带数据备份的职责。由于几乎每个 BSD、Linux 和 Unix 系统都包含 `tar`，它已成为软件包的标准工具以及将数据备份到压缩归档中。这些归档随后可以以多种方式进行传输和存储。

要通过网络将备份后的数据移动到其他机器，你可以使用 OpenSSH 工具的远程执行功能（例如 `ssh`）。你还可以使用一个名为 `rsync` 的优秀实用程序。通过 `rsync`，你可以通过仅备份更改的文件（或文件的部分）来节省资源。`hdiutil` 程序允许你从命令行将文件刻录到 CD 中，增强了执行相同工作的原生 GUI 功能。

Mac OS X 的备份功能（如 Time Machine 和 Time Capsule）也适用于 UNIX 进阶用户。你可以使用默认选项进行每小时备份，也可以在你的技巧库中添加命令行选项和 AppleScript 脚本，以调度额外的备份。

## 检查和运行进程

当一个可执行程序启动时，它会作为一个进程运行，并受系统进程表的管理。每个 Mac OS 系统都提供了查看和更改系统上运行进程所需的所有工具。

`ps` 和 `top` 命令是查看运行进程信息的绝佳工具。`ps` 和 `top` 实际上有几十个选项，可以帮助你按照想要的方式查看进程信息。

诸如 `nice` 和 `renice` 命令用于提高或降低进程优先级。你可以将进程移动到后台运行（`bg` 命令），并将它们移回前台（`fg` 命令）。

向进程发送信号是改变其行为或杀死它的方法。使用 `kill` 和 `killall` 命令，你可以通过 PID 或名称发送信号。你还可以向进程发送其他信号来执行如重新读取配置文件或继续运行停止的进程等操作。

要在调度的时间运行命令或确保它们不绑定到你的 shell 会话，你可以使用 `at` 和 `batch` 命令。要在固定时间重复运行命令，有 `cron` 和 `anacron` 设施。

## 本章

- 使用 `ps` 和 `top` 查看活动进程
- 查找和控制进程
- 使用 `nice` 和 `renice` 调整 CPU 优先级
- 将进程移动到后台 (`bg`) 或前台 (`fg`)
- 使用 `kill` 和 `killall` 杀死并向进程发送信号
- 使用 `at` 和 `batch` 运行命令
- 使用 `cron` 调度重复运行命令

# 第 9 章：检查和运行进程

## 列出活动进程

要查看系统上当前运行的进程，大多数人使用 `ps` 和 `top` 命令。`ps` 命令为你提供当前运行进程的快照（简单列表形式）。`top` 命令提供了一个面向屏幕的不断更新的运行命令列表，并根据你的选择（按 CPU 使用率、I/O、UID 等）进行排序。

每个 BSD 系统（以及所有派自 UNIX 的系统，如 Linux、Mac OS X 等）都使用 `ps` 命令。多年来，出现了许多不同版本的 `ps`，提供了不同的选项。由于 `ps` 可以追溯到第一个 UNIX 系统，它还支持以非方式输入某些选项（例如，允许在某些情况下省略选项前的横杠）。

本章中 `ps` 的不同用法将适用于 FreeBSD、OpenBSD、NetBSD 以及其他 UNIX 和 Linux 系统。以下是一些你可以运行的示例，用于显示当前用户运行的进程（表 9-1 包含 `ps` 输出的列描述）：

```
$ ps
PID STAT TIME COMMAND
810 v0 I 0.0009 -sh (sh)
1127 v2 S 0.0002 -sh (sh)
1125 v2 R 0.0000 ps
```

```
$ ps u
PID STAT TIME COMMAND
1123 ? S 0.00:01 sshd:marlow@tty0 (sshd)
810 v0 I 0.0009 -sh (sh)
1127 v2 S 0.0002 -sh (sh)
1125 v2 R 0.0000 -p -U chris
1133 p0 S+ 0.0000 -sh (sh)
```

```
$ ps u
USER PID %CPU %MEM VSZ RSS STAT TIME COMMAND
chris 1123 0.0 1.3 6252 3312 ? 4:52 0.00:03 sshd:marlow@tty0
chris 1118 0.0 1.6 1756 1400 I 3:30 0.00:09 -sh (sh)
chris 1117 0.0 0.6 1752 92 V I+ 4:45 0.00:05 -sh (sh)
chris 1133 0.0 0.6 1756 1396 p S 4:52 0.00:03 -sh (sh)
chris 1204 0.0 0.4 1460 1030 p 5:07 0.00:05 -p -U marlow -u
```

```
$ ps vu
PID STAT TIME RE PAGEIN VSZ RSS LIM %CPU %MEM COMMAND
1132 S 0.00:16 0 127 0 6252 3312 -168 0.0 1.3 sshd:marlow
810 I 0.00:09 0 127 2 1756 1400 -100 0.0 0.6 -sh (sh)
1133 S 0.00:08 0 127 0 1756 1400 -100 0.0 0.6 -sh (sh)
```

这些示例说明了登录用户和远程登录（`sshd`）的某些进程。第一个示例显示了从 Terminal 直接运行的 `ps`，因此你只能看到窗口中运行当前 shell 的进程。其他示例允许你为每个进程显示不同的信息。SL 和 RE 列显示进程睡眠了多少秒以及在核心中持续了多久。以下是显示系统上每个进程输出的 `ps` 示例：

```
$ ps x | less
PID STAT TIME COMMAND
0 0:00:00 [sw]
1 0:00.01 /sbin/init
2 0:00.49 [g_event]
```

```
$ ps xl | less
ID PID PRI NI VSZ RSZ STAT TIME COMMAND
0 0 0 96 0 0:00:00 [swapper]
0 0 1 8 772 388 0:00.01 /sbin/init
2 0 -0 8 0:00.49 [g_event]
```

```
$ ps xj | less
USER PID PGID SID STAT TIME COMMAND
root 0 0 0 0 0:00:00 [swapper]
root 1 0 1 0 0:00.01 /sbin/init
root 2 0 0 0 0:00.56 [g_event]
```

```
$ ps aux | less
USER PID %CPU %MEM VSZ RSZ STAT STARTED TIME COMMAND
root 10 9.9 0.0 8 3:30PM 29:34 [idle]
root 0 0.0 0.0 0 0:00:00 [swapper]
root 1 0.0 0.0 0 3:30PM 0:00:01 /sbin/init
```

```
$ ps auxw
$ ps auxww
```

之前的命令如果你想查看完整的 `ps` 输出是非常用的。当输出超出列宽时，它将换行而不是截断。

如果你偏好个性化的 `ps` 输出，可以使用 `-o` 选项精确选择显示哪些数据列。表 9-1 显示了可用列以及添加到 `-o` 以让 `ps` 显示这些列。

### 表 9-1: 选择和查看 ps 列

| Option | Column head | Description |
| --- | --- | --- |
| %cpu | %CPU | CPU 使用率 |
| %mem | %MEM | 内存使用率 |
| acflag | ACFLG | 统计标志 |
| args | COMMAND | 命令和参数 |
| comm | COMMAND | 仅命令 |
| command | COMMAND | 命令和参数（与 args 相同） |
| cpu | CPU | 短期 CPU 使用因子（用于调度） |
| etime | ELAPSED | 运行时 |
| flags | F | 进程标志，十六进制（与 f 相同） |
| inblk | INBLK | 总读取块数（与 inblock 相同） |
| jid | JID | Jail ID |
| jobc | JOBC | 作业计数 |
| ktrace | KTRACE | 跟踪标志 |
| label | LABEL | MAC 标签 |
| lim | LIM | 内存使用限制 |
| lockname | LOCK | 当前阻塞的锁（符号） |
| logname | LOGIN | 启动会话的用户登录名 |
| lstart | STARTED | 开始时间 |
| majflt | MAJFLT | 总页异常 |
| minflt | MINFLT | 总页重取 |
| msgrcv | MSGRCV | 接收的消息数（管道/套字读取） |
| msgsnd | MSGSND | 发送的消息数（管道/套字写入） |
| mwchan | MWCHAN | 当前阻塞的等待通道或锁 |
| nice | NI | Nice 值（与 ni 相同） |
| nivsw | NIVCSW | 总非自愿上下文切换 |

### 表 9-1：选择和查看 ps 列输出（续）

| 选项 | 列名 | 描述 |
| --- | --- | --- |
| nsigs | NSIGS | 接收的信号总数（与 signals 相同） |
| nswap | NSWAP | 入出交换总次数 |
| nvcsw | NVCSW | 总自愿上下文切换次数 |
| nwchan | NWCHAN | 等待通道（作为地址显示） |
| oublk | OUBLB | 写入的总块数（与 oublock 相同） |
| paddr | PADDR | 交换地址 |
| pagein | PAGEIN | 缺页次数（与 majflt 相同） |
| pgid | PGID | 进程组 ID |
| pid | PID | 进程 ID |
| ppid | PPID | 父进程 ID |
| pri | PRI | 调度优先级 |
| re | RE | 核心驻留时间，单位为秒（127 表示无限） |
| rgid | RGID | 实际组 ID |
| rgroup | RGROUP | 组名（与实际组 ID 相关） |
| rss | RSS | 驻留集大小 |
| rtrio | RTRIO | 实时优先级（10I 表示其不是实时进程） |
| ruid | RUID | 实际用户 ID |
| ruser | RUSER | 用户名（与实际用户 ID 相关） |
| sid | SID | 会话 ID |
| sig | PENDING | 挂起的信号（与 pending 相同） |
| sigcatch | CAUGHT | 已捕获的信号（与 caught 相同） |
| sigignore | IGNORED | 已忽略的信号（与 ignored 相同） |
| sigmask | BLOCKED | 阻塞的信号（与 blocked 相同） |
| sl | SL | 睡眠时间，单位为秒（127 表示无限） |
| start | STARTED | 开始时间 |

### 表 9-1：选择和查看 ps 列输出（续）

| 选项 | 列名 | 描述 |
| --- | --- | --- |
| state | STAT | 进程符号状态（与 stat 相同） |
| svid | SVGID | 来自 setgid 可执行文件保存的 gid |
| svuid | SSUID | 来自 setuid 可执行文件保存的 UID |
| tdev | TDEV | 控制终端设备号 |
| time | TIME | 累计 CPU 时间，用户 + 运行（与 cputime 相同） |
| tpgid | TPGID | 控制终端进程组 ID |
| tsid | TSID | 控制终端会话 ID |
| tsiz | TISZ | 文本大小，单位为 KB |
| tt | TT | 控制终端名称，双字母缩写 |
| tty | TTY | 控制终端全名 |
| uproc | UPROCP | 进程指针 |
| ucomm | UCOMM | 用于计费的名称 |
| uid | UID | 有效用户 ID |
| upr | UPR | 系统调用的调度优先级（与 uspri 相同） |
| user | USER | 用户名（从用户 ID 获取） |
| vsz | VSZ | 虚拟大小，单位为 KB（与 vsize 相同） |
| wchan | WCHAN | 符号名称形式的等待通道 |
| xstat | XSTAT | 退出或停止状态（停止或僵尸进程） |

注意，如果名称太长无法适应给定空间，某些值将以数字（UID）的形式显示。要查看这些值，请使用 `ps -L`：

```
$ ps L
%cpu %mem amagcl args blocks inblk job jid doc ktrace comm command cputime etime
% flags ignored inblk label tim lockname login logname
lstart majft minft msgrcv msgsnd wchan ni nice nwscw nlpsignals nsisags
swap nwscw nwchan oublock oubaddr pagein pcpu pending pgid pid peem pmid
ri re rigid rgroup rtprdio user sid sig sigcatch signoremark pigment sl
start stat state svid svuid time tpgid tsid tsiz tt tty ucomm uid upr
uproc uspri vsize vsz wchan xstat
```

通过使用逗号分隔的列选项列表，你可以生成自己自定义的输出。以下是运行中进程的自定义视图示例：

```
$ ps xo ppid,user,mem,tiz,vsz,comm
PPID USER            %MEM TSIZ  VSZ COMMAND
1129 1.3 168 6252 ssh
```

```
$ ps xo ppid,user,start,time,%cpu,args
PPID USER            STARTED   TIME     %CPU COMMAND
1129 chris       4:52PM 00:02:0.8 chris@chttyp0 (sshd)
```

```
$ ps xo ppid,user,cputime,args
PPID USER            TIME                 COMMAND
1129 chris       00:08:54 chris@chttyp0 (sshd)
```

```
$ ps xo ppid,user,stat,tty,sid,etime,args
PPID USER            STAT TTY ELAPSED COMMAND
1129 chris       S      06:39:23 ssh@chttyp0 (sshd)
```

以下是 `ps` 命令的其他示例：

```
$ ps -aux | less
USER            %PID %CPU VSZ RSS TTY STAT COMMAND Sort by cpu usage
                                TIME COMMAND
root             0 0 0 0 0
0000000000000
)
```

```
$ ps -m
USER            %PID %CPU VSZ RSS TTY STAT COMMAND Sort by memory
                                TIME COMMAND
root             0 0 0 0 0
$
000
PID% VSCPU VSZ RSS TTY STAT
11100000000000000000000000)
```



# 第 9 章：检查和运行进程

如果你想查找更多关于如何使用 `top` 的信息，可以在 `top` 会话期间输入 `?`。man 页也包含许多关于如何使用 `top` 的信息：

```
$ man top
```

用完 `top` 后，输入 `q` 退出。

## 查找和控制进程

更改运行中的进程首先是找到你想更改的进程，然后修改处理优先级或向进程发送信号来更改其行为。如果你在寻找特定的进程，在 `ps` 或 `top` 输出的长长进程列表中找到它可能会很困难。

`pgrep` 命令允许你在活动进程中搜索你正在寻找的进程。`renice` 命令允许你更改运行中进程的处理优先级。`kill`、`killall` 和 `killall` 命令允许你向运行中的进程发送信号（包括结束这些进程的信号）。

## 使用 grep 和 pgrep 查找进程

在最基本的形式，你可以使用 `grep` 搜索命令名称（或其部分），并生成包含该名称的任何进程的进程 ID（PID），如下例所示：

```
$ ps | grep http              # 显示任何包含 'http' 字符串的进程信息
myerman    19416    0.0   112568    988  ?   S   3:46PM   00:00.00  /
Applications/MAMP/Library/bin/httpd -k start
```

如果你需要对查找进程有更多控制，可以从 sourceforge.net/projects/protools 下载 protools。`protools` 包将为你提供 `pgrep` 命令行工具。

在最基本的形式，你可以使用 `pgrep` 搜索命令名称（或其部分），并生成包含该名称的任何进程的 PID，如下例所示：

```
$ pgrep init               # 显示任何包含 'init' 字符串的进程的 PID
2617
```

因为你知道只有一个 `init` 命令在运行，你接下来使用 `-l` 选项来选择每个进程命令（以知道使用了哪两个进程）：

```
$ pgrep -l init
2617 xinit
1 init
# 显示任何包含 'init' 字符串的进程的 PID 和名称
```

你还可以搜索与特定用户关联的进程：

```
$ pgrep -lu kafka
2803 vim
2552 bash
2551 sshd
# 列出用户 kafka 拥有的所有进程
```

使用 `pgrep` 最有用的方法可能是找到运行进程的进程 ID，并将这些 PID 管道到另一个命令以产生输出。以下是一些示例（对于 Metacity 或 Firefox 等其他命令，它们尚未运行）：

```
$ ps -p `pgrep metacity`
PID STAT COMMAND
2617 ?? 00:07.02 /usr/local/bin/metacity --mm-client-id=default0
$ ps -fp `pgrep init`
PID STAT TIME COMMAND
2617 V I+ 00:00.01 /usr/X11/bin/home/chris/.xinitrc
### renice -5 pgrep safari
20522:old priority 0, new priority -5
20557:old priority 0, new priority -5
```

任何可以接受进程 ID 输入的命令都可以以这些方式与 `pgrep` 结合。正如前面的 `pgrep` 示例所示，你可以使用 `renice` 等命令来更改进程运行时的行为。

## 使用 fuser 查找进程

另一种定位特定进程的方法是查找该进程正在访问的内容。`fuser` 命令可以找到当前哪些进程打开了文件或套接字。在处理进程后，`fuser` 可以向这些进程发送信号。`fuser` 命令对于确定文件是否被挂载文件系统（如硬盘或 Samba 共享）上的进程打开最为有用。找到这些进程可以让你能够正确地关闭它们（如果必须，则直接杀死它们），以便文件系统能够干净地卸载。

以下是使用 `fuser` 命令列出在所选文件上打开文件的进程的示例：

```
$ fuser -cu /Users/myerman # 带有用户名
/Users/myerman: 12958c(myerman)
```

刚刚示例显示了与 /Users/myerman 关联的一个运行进程的进程 ID。它可能表示一个打开的文件、一个打开的 shell，或者一个当前目录在 /Users/myerman 或其子目录下的 shell 子进程。`-c` 选项将 /Users/myerman 视为挂载点（因此该下的任何内容都会匹配），而 `-u` 导致列出每个进程的所有者。

进程 ID 和用户名之间的字母表示打开的文件如何使用。在这些示例中，`x` 表示该文件是进程的可执行文本，`c` 表示该文件是进程的当前工作目录。其他可能的字母包括 `r`（文件在进程的根目录中）、`j`（文件是进程的 jail 根）、`t`（文件是进程的内核跟踪文件）、`y`（进程使用该文件作为其控制终端）、`m`（文件已映射）、`w`（文件打开写入）、`a`（文件为仅追加）、`s`（文件有共享锁）和 `e`（文件有排他锁）。

以下是使用 `fuser` 显示带有文件的进程的其他示例：

```
### fuser -c -m /boot      # 显示打开 /boot 的进程的 PID/符号
### fuser -u /boot         # 显示 /boot 的 PID/符号
```

在知道哪些进程打开了文件后，可以使用 `fuser` 启动或停止进程。

# 使用 nice 调整进程优先级



每个运行中的进程都有 `nice` 值，这仅仅是一个建议。默认 `nice` 值为 0。优先级数字范围从 -35（最有利）到 19（最不利）。虽然 root 用户可以提高或降低任何用户的优先级，普通用户只能降低优先级。

> **警告** 在为进程分配负值时要谨慎。如果关键进程丢失优先级，可能会导致机器崩溃。

以下是使用 `nice` 启动命令的几个示例：

```
$ nice -n 12 nroff -name a.roff | less  低优先级格式化页
# nice 10 designer      高优先级启动 Designer
```

当进程运行时，可以使用 `renice` 更改其值。以下是一些示例：

```
$ renice +2 -u kafka      调整 kafka 的进程 +2
# nice +5 4737             调整 PID 4737 +5
# renice -3 /find -name *.html -print  调整 -3
9688:old priority -1, new priority -3
20279:old priority -1, new priority -3
20282:old priority -1, new priority -3
```

反引号在之前的命令中表示 `find` 命令的输出（假设为卷上的任何 .html 文件）应该传递给 `renice` 命令。

运行 `top` 时，默认会显示进程的 `nice` 值。你也可以在从 `ps` 命令产生自定义输出时使用 `-o nice` 查看 `niceness` 设置。

# 在后台和前台运行进程

当你从 shell 运行进程时，它默认在前台运行。这意味着你可以运行另一个命令，直到第一个命令完成。通过在命令行末尾添加与符号（`&`），你可以在后台运行命令。使用 `fg`、`bg` 和 `jobs` 命令结合各种控制代码，你可以在后台和前台之间移动命令。

以下命令序列从终端窗口启动 GIMP 图像程序。之后是一系列控制键和命令，用于停止和启动进程并在后台和前台之间切换：

```
$ gimp               在前台运行 gimp
<Ctrl+Z>             停止进程并放入后台
[1]+ Stopped gimp
$ bg 1               在后台重新启动进程 (bash)
```

# 第 9 章：检查和运行进程

```
$ bg %1
$ fg 1
$ bg %1
gimp
<Ctrl+C>
再次在后台运行进程 (sh)
在前台继续运行进程 (bash)
在前台继续运行进程 (sh)
杀死进程
```

请注意，置于后台的进程会被分配一个作业 ID 数字（在本例中为 1）。通过在数字前加上百分号（例如 `%1`），你可以向 `bg` 和 `fg` 命令指定特定的后台进程。在 bash shell 中，你也可以通过在命令后输入数字（如 `fg 1`）来实现相同的操作。如果当前 shell 运行有一个或多个后台作业，你可以使用 `jobs` 命令来管理这些作业：

```
$ jobs 显示当前 shell 的后台作业
[1] Running gimp &
[2] Running xmms &
[3] Running gedit &
[4]+ Stopped gtali
$ jobs -1 显示每个作业的信息及其 PID
[1] 31676 Running gimp &
[2] 31677 Running xmms &
[3] 31683 Running gedit &
[4] 31688 Stopped gtali
$ jobs -2 仅显示作业 %2 的信息
[1] 31677 Running xmms &
```

`jobs` 示例中的进程可能是你在登录远程系统时完成的，但通过使用 `ssh` 在本地桌面上运行远程 GUI 应用程序。通过在后台运行这些进程，你可以让当前 shell 同时运行多个应用程序。

> **注意** 使用 `fg` 或 `bg` 时，如果没有指定要操作的进程，则将使用当前作业。当前作业旁边带有一个加号（`+`）。

`fg` 和 `bg` 通过将进程移动到前台或后台来操作运行中的进程。另一种操作运行命令的方法是直接向这些进程发送信号。向运行进程发送信号的常用方法是使用 `kill` 和 `killall` 命令。

## 杀死和信号进程

你可以通过向进程发送信号来更改或停止运行中的进程。`kill` 和 `killall` 等命令可以将你选择的信号发送给运行进程，正如其名称所示，这些通常是杀死进程的信号。

信号用数字（9、15 等）和字符串（`SIGKILL`、`SIGTERM` 等）表示。表 9-2 描述了在 BSD 系统中可以发送给进程的标准信号。

### 表 9-2：发送给进程的标准信号

| 信号数字 | 信号名称 | 描述 |
|---|---|---|
| 1 | `SIGHUP` | 终端挂断或控制进程死亡 |
| 2 | `SIGINT` | 中断程序 |
| 3 | `SIGQUIT` | 退出程序 |
| 4 | `SIGILL` | 非法指令 |
| 5 | `SIGTRAP` | 跟踪陷阱 |
| 6 | `SIGABRT` | 从 `abort` 函数发送的终止信号 |
| 7 | `SIGEMT` | 执行了仿真执行指令 |
| 8 | `SIGFPE` | 浮点数异常 |
| 9 | `SIGKILL` | 杀死信号 |
| 10 | `SIGBUS` | 总线错误 |
| 11 | `SIGSEGV` | 段错误 |
| 12 | `SIGSYS` | 调用了不存在的系统调用 |
| 13 | `SIGPIPE` | 管道破裂（无法向管道读写） |
| 14 | `SIGALRM` | 来自报警系统调用的定时信号 |
| 15 | `SIGTERM` | 终止信号 |
| 16 | `SIGURG` | 丢弃进程 |
| 17 | `SIGSTOP` | 停止进程 |
| 18 | `SIGTSTP` | 在终端输入的停止 |
| 19 | `SIGCONT` | 如果进程已停止则继续 |
| 20 | `SIGCHLD` | 子进程状态改变 |
| 21 | `SIGTTIN` | 终端尝试读取后台进程 |
| 22 | `SIGTTOU` | 终端尝试写入后台进程 |

`kill` 命令可以通过进程 ID 或作业号向进程发送信号，而 `killall` 命令可以按命令名向进程发送信号。以下是一些示例：

```
$ kill 28665
  向 PID 为 28665 的进程发送 SIGTERM
$ kill -9 4895
  向 PID 为 4895 的进程发送 SIGKILL
```

```
$ kill -SIGCONT 5254      继续停止的进程 (pid 5254)
$ kill %3                           杀死代表作业 %3 的进程
$ killall spamd                      杀死所有当前运行的垃圾守护进程
$ kill -SIGHUP sendmail              让邮件进程重新读取配置文件
```

`SIGKILL`(9) 信号经常被粗鲁莽的新手管理员滥用，应该被作为最后的手段。它不允许目标进程干净地执行，而是突然结束。这可能会导致该进程处理的数据丢失或损坏。`SIGHUP` 信号最初用于 UNIX 系统，表示终端正在从主机断开连接（例如来自拨号调制调制器的挂断）。然而，`sendmail` 和 `httpd` 等守护进程被设计为捕获 `SIGHUP` 信号，作为这些进程重新读取配置的指示。

## 远离当前 shell 运行进程

如果你希望进程在断开当前 shell 后继续运行，有几种方法可以实现。你可以使用 `nohup` 命令来运行进程，使其免受挂断信号的影响：

```
$ nohup myscript.sh &      以不可被中断的方式运行 myscript.sh
# nice -9 gcc hello.c &     以不中断且更高的优先级运行 gcc
```

使用 `nohup` 与单独使用 `&` 符号运行命令不同，因为使用 `nohup` 时，即使你退出了启动命令的 shell，命令也会继续运行。

`nohup` 命令在进程缓慢和使用拨号连接的时代很常用（这样你就不需要在长时间编译完成时一直保持昂贵的连接状态）。此外，今天使用诸如 `screen`（第 14 章描述）等工具，你可以在断开与该 shell 的网络连接后仍保持 shell 会话活动。

## 调度进程运行

与 `cron` 设施相关的命令可用于设置在特定时间（包括现在）运行命令，使其不连接到当前 shell。`at` 命令在你设置的时间运行命令。输入你想在稍后时间运行的命令，并按 `Ctrl+D` 退出作业：

```
$ at now +1 minute               在一分钟后启动命令
ls -R /usr/ports ~ /tmp/portlist.txt
<Ctrl+D> <EOF>
job 5 at Mar 20 20:37:00 2008
# at teatime                    在今天下午 4 点启动命令
# at now +5 days                在五天后启动命令
# at 06/25/08                   在 2008 年 6 月 25 日当前时间启动命令
```

另一种不连接到当前 shell 运行命令的方法是使用 `batch` 命令。通过 `batch`，你可以设置命令在处理器准备就绪（负载平均值低于 .8）时立即启动。

```
# batch
立即启动运行命令
find /mt/isos | grep jpg$ > /tmp/mypics
Ctrl+D <EOT>
```

注意，在执行 `at` 或 `batch` 命令后，你会得到一个次级提示符。在该提示符处输入你想运行的命令并按回车。之后，你可以继续输入命令。完成后，在单独的一行上按 `Ctrl+D` 即可将输入的命令排队运行。

输入命令后，你可以通过输入 `atq` 命令来检查设置为运行的 `at` 和 `batch` 作业队列：

```
atq
Date Owner Queue Job#
Tue Dec 29 16:00:00 CST 2008 root C 4
Sat Aug 2 19:24:00 CST 2008 root C 5
```

普通用户无法查看队列作业。root 用户可以查看所有人的作业。如果你想从队列中删除作业，请使用 `at` 命令：

```
# rm 5
删除作业 5
```

`at` 和 `batch` 命令用于将命令队列为一次性任务。你可以使用 `cron` 设施设置循环运行的命令。这些命令被写入 `crontab` 文件，并在 crontab 文件中进行调度。有一个系统 crontab 文件 (`/etc/crontab`)。此外，每个用户都可以创建一个个人的 crontab 文件来启动命令。要创建个人的 crontab 文件，输入以下内容：

```
$ crontab -e
创建个人的 crontab 文件
```

`crontab -e` 使用 `vi` 编辑器打开 crontab 文件（或创建一个）。以下是你可以添加到 crontab 文件中的几条条目示例：

```
15 8 * Mon,Wed,Thu,Fri kafka < /var/project/stats.txt
* * 1,4,7,10 * find /doc | grep .doc > /var/sales/documents.txt
```

第一个 crontab 示例通过重定向 `/var/project/stats.txt` 的内容向名为 `kafka` 的用户发送消息。邮件命令在周一、三、四、五上午 8:15 运行。在第二个示例中，在 1 月、4 月、7 月和 10 月的第一天，`find` 命令运行查找每个 .doc 文件并将产生的文件列表发送到 `/var/sales/documents.txt`。

每个 crontab 条目的最后部分是运行运行的命令。前五个字段代表运行命令的时间和日期。从左到右的字段如下

## 第 9 章：检查与运行进程

格式如下：分钟（0 到 59），小时（0 到 23），日期（0 到 31），月份（0 到 12，对应 Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec），以及星期几（0 到 7，或者 Sun, Mon, Tue, Wed, Thu, Fri, Sat）。字段中的星号（`*`）可匹配该字段的任何值。

以下是使用 `crontab` 命令的其他其他选项：

```
# crontab -e Marlowe 编辑另一个用户的 crontab（仅限 root）
# crontab -l 列出你的 crontab 文件的内容
15 8 * * Mon,Tue,Wed,Thu,Fri chris < /var/project/stats.txt
* 1,4,7,10 * find / | grep .doc5 > /var/sales/documents.txt
* crontab -r 删除 crontab 文件
```

`cron` 设施的替代方案是 `anacron` 设施（`pkg_add -r anacron`）。使用 `anacron`，你可以像 `cron` 一样配置定期运行的命令。然而，`anacron` 最适用于并非一直处于开启状态机器。如果某个命令因为计算机在计划时间内关机而没有运行，那么当计算机下次启动时，`anacron` 设施会确保在关机期间错过的命令在系统恢复后运行。

### 总结

监控并操作在你 Mac OS X 系统上运行的进程是确保系统高效运行的重要活动。通过使用 `ps` 和 `top` 等命令，你可以查看系统上运行的进程。

通过 `nice` 和 `renice` 等命令，你可以调整所选进程运行的建议优先级。当进程运行时，你可以通过从 `kill` 或 `killall` 命令向其发送信号来改变其运行方式或杀死该进程。

从当前 shell 启动命令后，你可以设置该命令在后台（`bg`）或前台（`fg`）运行。你还可以使用不同的控制代码停止并重启进程。

若要调度命令在稍后时间运行，可以使用 `at` 或 `batch` 命令。要设置按固定间隔重复运行的命令，可以使用 `cron` 或 `anacron` 设施。

# 第 10 章：系统管理

如果没有仔细的管理，你 Mac OS X 系统的需求有时会超过现有的资源。能够帮助你随时间监控系统活动（内存、CPU 和设备使用情况）可以确保你的机器拥有足够的资源。同样，管理系统的其他方面，例如它使用的设备以及启动过程的工作原理，有助于避免性能问题和系统故障。

## 本章内容

- 使用 `top` 和 `vmstat` 检查内存使用
- 使用 `iostat`、`systat` 和 `top` 查看 CPU 使用率
- 使用 `iostat` 和 `isof` 监控存储设备
- 使用 `date`、`cal` 和 `nt` 处理日期/时间

本章分为几个与管理你的 Mac OS X 系统方法的相关部分。第一部分可以帮助你监控系统上的资源（处理能力、设备和内存）。下一部分描述了如何检查和设置系统时钟。随后是关于启动过程和后续运行级别的描述。最后几部分描述了如何与内核及相关的设备程序交互，以及如何查看计算机硬件组件的信息。

- 使用 `reboot`、`halt` 和 `shutdown` 关闭系统

## 监控资源

FreeBSD、OpenBSD、NetBSD 以及其他类 Unix 系统在跟踪其执行的操作方面做得非常出色，如果你感兴趣，可以找到大量关于你的 CPU、硬盘、虚拟内存和其他计算机资源如何被使用的信息。

当然，你可以使用命令来查看你的系统上虚拟内存、处理器、存储设备和网络接口的使用情况。有些命令可以监控系统资源的几个不同方面。然而，由于本书不仅仅是一页纸，我们按照主题（监控内存、CPU、存储设备）划分了后续章节，而不是按照执行这些操作的命令（`top` 和 `iostat`）。

## 监控内存使用

没有什么比内存耗尽更能更快地杀死性能了。`top` 等命令允许你看到关于 RAM 和交换空间（`swap`）使用情况的基本信息。

`top` 命令提供了一种观察运行进程的方法，这些进程按 CPU 使用率或内存排序（请参见第 9 章中关于运行进程的 `top` 描述）。你还可以使用 `top` 在面向屏幕的窗口中查看内存使用情况。这是一个示例：

```
$ top
last pid: 1619; load averages: 0.61, 0.85, 0.62 up 0+02:23:09 17:23:49
8 processes: 2 running, 83 sleeping
CPU states: 37.5% user, 0.0% nice, 15.4% system, 46.3% idle
Mem: 76M Active, 31M In, 79M Wired, 2476K Cache, 34M Buf, 53M Free
Swap: 484M Total, 25M Used, 5M Free
```

按 `q` 退出 top。`top` 命令显示了 RAM（Mem）和交换空间（Swap）的总内存使用情况。由于 `top` 是屏幕显示并提供持续监控，你可以每两秒（默认）观察一次内存使用的变化。分析进程内存使用最有用的列是 RES，它显示实际的物理 RAM 使用情况，也称为 resident。运行 `top -size`，运行进程将按驻留内存使用顺序显示（按 RES 列排序）：

```
$ top -size
PID USER PR SIZE RES STAT TIME WCPU COMMAND
1673 kafka 3 112 056288K 38660K RUN 0:22 0.00% totem
1615 kafka 1 96 027060K 15428K select 0:03 0.00% kview
1462 kafka 1 100 084900K 13388K select 1:51 10.60% Xorg
1496 kafka 3 20 033072K 10928K kserel 0:05 0.05% nautilus
```

要查看进程消耗的内存总大小（包括文本、数据和栈），你可以按 SIZE 列排序。要这样做，输入 `top -ovsize`：

```
$ top -ovsize
```



# 第 10 章：管理系统

## 内存使用率

没有什么比内存耗尽更能更快地杀死性能了。`top` 等命令允许你看到关于你的 RAM 和交换空间使用情况的基本信息。

`top` 命令提供了一种观察运行进程的方法，这些进程按 CPU 使用率或内存排序（请参见第 9 章中关于运行进程的 `top` 描述）。你还可以使用 `top` 在面向屏幕的窗口中查看内存使用情况。这是一个示例：

```
$ top
last pid: 1619; load averages: 0.61, 0.85, 0.62 up 0+02:23:09 17:23:49
8 processes: 2 running, 83 sleeping
CPU states: 37.5% user, 0.0% nice, 15.4% system, 46.3% idle
Mem: 76M Active, 31M In, 79M Wired, 2476K Cache, 34M Buf, 53M Free
Swap: 484M Total, 25M Used, 5M Free
```

按 `q` 退出 top。`top` 命令显示了 RAM（Mem）和交换空间（Swap）的总内存使用情况。由于 `top` 是屏幕显示并提供持续监控，你可以每两秒（默认）观察一次内存使用的变化。分析进程内存使用最有用的列是 `RES`，它显示实际的物理 RAM 使用情况，也称为 resident。运行 `top -size`，运行进程将按驻留内存使用顺序显示（按 `RES` 列排序）：

```
$ top -size
PID USER PR SIZE RES STAT TIME WCPU COMMAND
1673 kafka 3 112 056288K 38660K RUN 0:22 0.00% totem
1615 kafka 1 96 027060K 15428K select 0:03 0.00% kview
1462 kafka 1 100 084900K 13388K select 1:51 10.60% Xorg
1496 kafka 3 20 033072K 10928K kserel 0:05 0.05% nautilus
```

要查看进程消耗的内存总大小（包括文本、数据和栈），你可以按 `SIZE` 列排序。要这样做，输入 `top -ovsize`：

```
$ top -ovsize
```

| PID | USERNAME | THR | PRI | SIZE | RES | STATE | TIME | WCPU | COMMAND |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1462 | marlowe | 1 | 100 | 0 85036K | 12528K | RUN | 3:41 | 10.94 | xorg |
| 1764 | kafka | 3 | 114 | 0 56124K | 38712K | RUN | 0:31 | 0.00% | team |
| 1496 | kafka | 3 | 20 | 0 03072K | 81000K | kserel | 0:05 | 0.00% | nautilus |
| 1494 | marlowe | 1 | 96 | 0 27880K | 9384K | | | | |

## CPU 使用率

`top` 命令提供了一种观察运行进程的方法，这些进程按 CPU 使用率或内存排序（请参见第 9 章中关于运行进程的 `top` 描述）。你还可以使用 `top` 在面向屏幕的窗口中查看内存使用情况。这是一个示例：

```
$ top
last pid: 1619; load averages: 0.61, 0.85, 0.62 up 0+02:23:09 17:23:49
8 processes: 2 running, 83 sleeping
CPU states: 37.5% user, 0.0% nice, 15.4% system, 46.3% idle
Mem: 76M Active, 31M In, 79M Wired, 2476K Cache, 34M Buf, 53M Free
Swap: 484M Total, 25M Used, 5M Free
```

## 精通时间

在你的 Mac OS X 系统上保持正确的时间对于系统的正常运行至关重要。你可以通过几种不同的方式设置系统时间。系统时间可以手动（使用 `date` 命令）或自动（使用 `ntpdate` 或 `ntpd` 服务）设置。另一个与时间相关的命令是 `uptime`，它显示你的系统运行了多久。

## 更改时区

你的 Mac OS X 系统的时区根据 `/etc/localtime` 文件的内容设置。你可以通过从 `/usr/share/zoneinfo` 的子目录下复制代表你时区的文件来立即设置新时区。例如，要更改当前时区 America/Chicago，你可以执行以下操作：

```
# cp /usr/share/zoneinfo/America/Chicago /etc/localtime
```

这可以通过创建一个符号链接来实现：

```
# ln -s /usr/share/zoneinfo/America/Chicago /etc/localtime
```

## 显示和设置日期和时间

如果你没有通过 NTP（网络时间协议）自动完成，那么 `date` 命令就是查看日期和更改时间设置的主要命令行界面。以下是以不同方式显示日期和时间的 `date` 命令示例：

```
$ date                              # 显示当前日期和时区
Tue Aug 12 01:26:50 CDT 2008
$ date +%a %b %d                    # 显示星期、月份、日期、年份
Tuesday 12 2008
$ date +"The date today is %F."     # 在 date 命令中添加文字
The date today is 2008-08-12.
$ date +"TIME: %H:%M:%SDATE: %Y-%m-%d"  # 分行显示时间和 日期
TIME: 06:29:10
DATE: 2008-12-18
```

```
$ date -u                           # 显示协调世界时 (UTC)
Mon Dec 29 15:19:12 UTC 2008
```

虽然我们本节的主要关注点是时间，但既然提到了日期，`cal` 命令是按月显示日期的快速方法。以下是示例：

```
$ cal                               # 显示当前月份日历（高亮显示今天）
```

October 2008

Su Mo We Th Fr Sa

   1 2 3 4

5 6 7 8 9 10 11

12 13 14 15 16 17 18

19 20 21 22 23 24 25

26 27 28 29 30 31

```
```
$ cal 2009                          # 显示整年的日历
```

2009

January February March
Su Mo We Th Fr Sa Su Mo We Th Fr Sa
   1 2 3 1 2 3 4 5 6 7
4 5 6 7 8 9 10 8 9 10 11 12 13 14
11 12 13 14 15 16 17 15 16 17 18 19 20 21
18 19 20 21 22 23 24 22 23 24 25 26 27 28
25 26 27 28 29 30 31
29 30 31
```

```
$ cal -j                            # 显示儒略历（从 1 月开始数字编号）
```

October 2008

Su Mo We Th Fr Sa

      275 276 277 278

280 281 282 283 284 285

286 287 288 289 290 291 292

293 294 295 296 297 298 299

300 301 302 303 304 305

```

该命令也可以用于更改系统日期和时间。（但是，要小心，随机更改日期可能会导致系统崩溃。）以下是示例：

```
$ date 081252100                    # 设置日期/时间为 2008 年 8 月 12 日下午 2:21
Mon Dec 15 21:00:00 CST 2008

$ date +2H                          # 调整为 2 小时后
Sun Aug 12 11:42:33 CDT 2008

$ date -v +3m                       # 将日期/时间调整为一个月前
Wed Nov 12 11:42:38 CDT 2008
```

下次使用 FreeBSD 时，系统将根据硬件时钟（如果启用了 NTP）重置；下次关机时，硬件时钟将重置为系统时间。确保系统获得正确时间的一种方法是使用 NTP。

## 使用网络时间协议设置日期/时间

在 Mac OS X 中，你有机会设置时区并查看系统钟反映的是本地时间还是 UTC 时间。你的系统根据硬件时钟显示日期。如前所述，确保系统时间不漂移的方法是使用 NTP。

`ntp` 守护随 Mac OS X 系统安装。它的配置文件位于 `/etc/ntp.conf`，可能包含如下内容：

```
server time.apple.com minpoll 12 maxpoll 17
```

这就是说，每隔 12 到 17 秒轮询 `time.apple.com` 以保持系统准确。然而，仅仅启用此项是不够的。你还需要开启自动更新。为此，点击 Dock 中的“偏好设置”，然后点击“日期”。在 10-1 所示的“日期”选项卡中，勾选“自动设置日期和时间”旁边的复选框。

![](img/d850b48b6750d726ccf813a2a895d7cc_164_0.png)
图 10-1：自动设置日期和时间

## 检查运行时间

BSD 及其他 UNIX 爱好者的自豪之事是他们无需重启就能运行系统。与其他 BSD 系统一样，Mac OS X 系统可以在无需重启的情况下运行多年。

Mac OS 系统自上次重启以来运行的时间被称为 `uptime`。你可以如下检查系统的 `uptime`：

```
$ uptime                            # 检查系统运行了多久
6:53pm up 196 days, 14:25, 3 users, load average: 1.66, 0.88, 0.35
```

`uptime` 的输出显示当前时间、系统运行了几天几小时以及有多少用户登录。之后，`uptime` 显示过去 1、5、15 分钟的系统负载。

在大多数 BSD 机器上，你可以使用 `init` 命令启动和停止系统，包括 `init 0`（关机）和 `init 6`（重启）。在 Mac OS X 上，你使用更具体的命令来停止系统。`halt`、`reboot` 或 `shutdown` 等命令的优点是它们包含了可以在关机前停止某些功能的选项。这是一个示例：

> **警告** 如果你不打算实际关闭系统，请不要尝试以下命令，特别是远程操作时。

在 Mac OS 系统挂起或无响应的少数情况下，你可以按住电源按钮直到系统启动来强制重启。

![](img/d726ccf813a2a895d7cc_165_0.png)
启动你的系统

## 直接进入内核

通常，当内核在你的系统上启动时，你不需要对其做太多。但是有工具可以检查正在使用的内核并查看其信息。此外，如果出现问题或你需要添加某些内容，也有相应的工具可用。

要确定你运行的是什么版本的 OS X，请输入以下：

```
$ uname -r                          # 显示当前版本的名称
9.5.0

$ uname -a                          # 显示所有名称和发布信息
Darwin Macintosh 9.5.0 Kernel Version 9.5.0: Wed Sep 3 11:29:43 PDT 2008;
root:xnu-1228.7.58-1/RELEASE_I86
```

你可以使用 `sysctl` 命令配合系统控制内核参数。你还可以将参数永久添加到 `/etc/sysctl.conf` 文件中，以便它们在每次重启时加载。以下是一些示例：

```
$ sysctl -a | less                  # 列出所有内核参数
kern.otype = Darwin
kern.osrelease = 9.5.0
kern.osrevision = 199506
kern.version = Darwin Kernel Version 9.5.0: Wed Sep 3 11:29:43 PDT 2008;
root:xnu-1228.7.58-1/RELEASE_I86
kern.maxnodes = 33792
kern.maxproc = 532
kern.maxfiles = 12288
```

```
$ sysctl kern.hostname              # 列出特定参数的值
kern.hostname = macintosh

$ sysctl kern.geom.debugflags=16    # 将 kern.geom.debugflags 的值设置为 16
```

## 使用 lsof 查找打开的文件

使用 `less` 或 `grep`，这里有几种方法可以从 `lsof` 输出中找到你寻找的内容：

```
### lsof -c csh                     # 列出由 C shell (csh) 打开的文件
# lsof -d cwd                       # 列出作为当前工作目录打开的目录
# lsof -u marlowe                   # 列出用户 marlowe 打开的文件和目录
### lsof /var                       # 列出 /var 文件系统上的任何内容
# lsof +d /var/log                  # 列出 /var/log 目录下的任何内容
```



如前所述，如果你想永久更改任何内核参数，应该将它们添加到 `/etc/sysctl.conf` 文件中。该文件中的参数设置格式为 `参数 = 值`。

## 内核 BSD

与其他 BSD 和 Linux 系统一样，Mac OS X 系统让你能够轻松监控和修改运行系统的许多方面，以确保其处于性能运行。`top` 和 `iostat` 命令允许你查看系统如何使用内存、CPU 和存储设备。通过 `date` 和 `cal` 命令以及 `NTP` 服务，你可以监控并管理系统的日期和时间设置。

# 第 11 章：管理网络连接

在 Mac OS X 系统上连接网络通常只需将计算机的网络网卡（NIC）连接到互联网服务提供商（ISP）的硬件（如 DSL 或电缆调制解调器），并让系统自动检测连接。然而，如果你的网络接口没有启动或需要某些手动干预，则可以使用命令来配置网络网卡、检查网络连接以及设置特殊路由。

本章涵盖了许多配置和操作网络网卡的有用命令，例如 `install` 和 `ifconfig`。特别是，它涵盖了配置有线、无线和调制解调器硬件的方法。当你的硬件已连接且网络接口就绪后，你还将学习使用 `netstat`、`dig` 和 `ping` 等命令来获取网络信息。

- 本章内容
- 获取网络统计数据
- 管理网络连接
- 使用 `dig`、`host` 和 `hostname` 检查 DNS 名称解析
- 使用 `ping` 和 `arping` 检查连通性
- 使用 `traceroute` 和 `route` 追踪连接
- 使用 `netstat` 监控网络

## 配置网络接口

要在 Mac OS X 上配置网络接口，请点击 Dock 上的“系统偏好设置”，然后点击“网络”。点击“高级”，你可以配置 AirPort（无线网络）、DNS 服务器、DHCP 等更多设置（见图 11-1）。

![](img/d850b48b6750d726fcc813a2a895d7cc_169_0.png)

你可能不需要进行任何更改，因为 Mac OS X 在自动检测新安装的网卡以及跟踪你已有的无线和有线网络接口方面表现出色。

配置网络接口的工作百分之九十可以在“系统偏好设置”区域完成，但随后的大部分内容将提供你从命令行配置、管理和监控网络网卡所需的信息。

> **注意**：你的以太网 NIC 的接口名称基于支持该网卡的驱动程序。如果你来自 Linux 环境，你可能期望以太网接口命名为 `eth0`、`eth1` 等。在 Mac OS X 中，名称可能是 `lo0`、`en0`、`en1`、`etc0` 或其他。本章中的示例使用 `lo0` 表示无线以太网网卡。

## 管理网络网卡

如果你计算机上的网络硬件没有立即出现并让你能够连接互联网，请尝试以下步骤来排除故障：

1. 检查你的网络网卡（NIC）是否正确安装，且电缆已连接到网络（ISP、CPE、交换机等）。
2. 电缆连接后，确保链路没有速度或双工不匹配的情况。
3. 如果所有方法都失败，考虑用已知良好的备用件替换你的 NIC 以隔离硬件故障。

要检查来自 BSD 系统的链路以及速度和双工，`ifconfig` 命令提供了这些以及许多其他功能。

> **注意**：如果你来自 Linux 或其他 UNIX 环境并习惯 `ethtool` 和 `mii-tool` 等工具，`ifconfig` 命令包含了你从这些命令中获得的许多相同功能。

要查看 `ifconfig` 命令的语法，请输入任何无效选项：

```
# ifconfig - View options to the ifconfig command

ifconfig: illegal option --?

usage: ifconfig [-L] [-C] interface address_family [address [dest_address]] [parameters]

ifconfig interface create

ifconfig -a [-L] [-C] [-d] [-m] [-v] [address_family]

ifconfig -l [-u] [address_family]

ifconfig [-L] [-C] [-d] [-m] [-u] [-v]
```

要显示每个可用网络接口的名称，使用 `-l` 选项。以下示例显示有一个以太网 NIC（fxp0）、一个并行端口（plip0）和一个环回接口（lo0）：

```
# ifconfig -l List names of network interfaces
lo0 gif0 st0 en0 fw0
```

要显示特定以太卡的设置，请在命令后添加接口名称。例如，要查看 fxp0（第一个有线 NIC）的信息，请输入以下：

```
# ifconfig lo0 See settings for NIC at lo0
lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST> mtu 16384
inet6 fe80::1%lo0 prefixlen 64 scopeid 0x1
inet 127.0.0.1 netmask 0xff000000
inet6 ::1 prefixlen 128
```

要显示特定网络卡的能力列表，使用 `-m` 选项：

```
# ifconfig -m Display driver information for NIC
lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST> mtu 16384
inet6 fe80::1%lo0 prefixlen 64 scopeid 0x1
inet 127.0.0.1 netmask 0xff000000
inet6 ::1 prefixlen 128
```

`ifconfig` 命令用于更改 NIC 设置以及用于显示这些设置。

要将速度硬设置为 100Mbps 全双工，请输入此命令：

```
# ifconfig lo0 media 100baseTX mediaopt full-duplex Change speed/duplex
# ifconfig lo0 View new NIC settings
lo0: flags=8843<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> mtu 1500
options=VLAN_MTU
inet 10.0.0.204 netmask 0xffffff00 broadcast 10.0.0.255
ether 00:d0:b7:79:a5:35
media: Ethernet 100baseTX <full-duplex>
status: active
```

要将速度硬设置为 10Mbps，使用以下：

```
# ifconfig lo0 media 10BaseT/UT Change speed
# ifconfig lo0 View NIC settings
lo0: flags=8843<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> mtu 1500
options=VLAN_MTU
inet 10.0.0.204 netmask 0xffffff00 broadcast 10.0.0.255
ether 00:d0:b7:79:a5:35
media: Ethernet 10BaseT/UT <full-duplex>
status: active
```

要更改 IP 地址和子网掩码，请输入：

```
# ifconfig lo0 10.0.0.208 netmask 255.255.0.0 Change IP and netmask
# ifconfig lo0 View NIC settings
lo0: flags=8843<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST> mtu 1500
options=VLAN_MTU
inet 10.0.0.208 netmask 0xffff0000 broadcast 10.0.255.255
ether 00:d0:b7:79:a5:35
media: Ethernet 10BaseT/UT <full-duplex>
status: active
```

```
ifconfig_fxp0="10.0.0.208 netmask 255.255.0.0 media 100baseTX"
```

`netstat` 命令提供了获取接口统计数据的许多方法。带有选项，`netstat` 显示活动连接和活动套接字如下：

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address | (state) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| tcp4 | 0 | 0 | Macintosh.50492 | channel103.01.05..http | ESTABLISHED |
| tcp4 | 0 | 0 | Macintosh.50499 | ug-in-f111.goog.imaps | ESTABLISHED |
| tcp4 | 0 | 0 | Macintosh.50408 | ug-in-f111.goog.imaps | ESTABLISHED |
| tcp4 | 0 | 0 | Macintosh.50407 | ug-in-f111.goog.imaps | ESTABLISHED |
| tcp4 | 0 | 0 | Macintosh.49517 | 64.233.181 | ESTABLISHED |
| udp | 0 | 0 | * | * | |
| udp | 0 | 0 | * | * | |
| udp | 0 | 0 | * | * | |
| udp | 0 | 0 | * | * | |
| udp | 0 | 0 | * | * | |
| udp | 0 | 0 | * | * | |
| udp | 0 | 0 | * | * | |

要显示所有网络接口的快速统计数据，使用如下的 `netstat`：

```
$ netstat -i
Get network statistics for all interfaces
Name  Mtu  Network             Address      Ipkts Errs Coll
lo0   16384  localhost       fe80::1               0     0
lo0   16384  localhost       127.0.0.1              0     0
lo0   16384  localhost                               0     0
gif0  128 <Link#2>                               0     0
```

使用 `-w` 选项检查 `netstat` 每秒刷新网络接口：

```
$ netstat -w -i fxp0
Refresh network statistics every second
packets      input (Total)         output
         bytes  packets  errs  bytes cols
         13               266      12      244
          2               5938       1      8428
          9               6676     116      0
         183             16862      225      369602
         152             13642      191      264566
         137             6836      169      103890
         113             10276      139      144936
```

使用 `netstat -p` 检查是否有到你计算机的活动连接，如下：

```
$ netstat -p tcp
```



# Display active TCP connections

Active Internet connections

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address (state) |
| :--- | :--- | :--- | :--- | :--- |
| tcp4 | 0 | 0 | Macintosh.50501 | channel103.01.05..imap ESTABLISHED |
| tcp4 | 0 | 0 | Macintosh.50499 | ug-in-f111.goog.imaps ESTABLISHED |
| tcp4 | 0 | 0 | Macintosh.50408 | ug-in-f111.goog.imaps ESTABLISHED |
| tcp4 | 0 | 0 | Macintosh.50407 | ug-in-f111.goog.imaps ESTABLISHED |
| tcp4 | 0 | 0 | Macintosh.49517 | 64.233.183.111 ESTABLISHED |

正如所示，`netstat` 命令返回三个连接。以下是 `netstat` 命令的其他示例：

```bash
$ netstat -r
Display kernel routing tables for IPv4 and IPv6

$ netstat -rs
Display routing stats (bad rates, dynamic metrics)

$ netstat -s -p tcp | less
Display detailed statistics for TCP interfaces

$ netstat -n
Display output with IP addresses, not hostnames

$ netstat -m
Display information on network memory buffers
```

# 管理网络连接

启动和停止有线以太网连接的网络接口通常在你启动并连接局域网或 OS X 系统时自动处理。你可以运行 `/etc/rc.d` 下的脚本来关闭 Mac OS X。

## 第 11 章：管理网络连接

可以根据需要随时启动或停止网络接口的目录，或者编辑 `/etc/rc.conf` 文件来指定网络服务是否自动启动。

`ifconfig` 命令也可用于配置、激活和停用接口。

### 启动和停止网络连接

你可以使用 `ifconfig` 命令来启用或禁用网络接口，如下所示：

```bash
# ifconfig en0 down          关闭以太网卡 (en0) 为网络接口
# ifconfig -d               列出所有处于关闭状态的接口
gif0: flags=8060<POINTPOINT,MULTICAST> mtu 1280
stf0: flags=<> mtu 1280
```

```bash
# ifconfig en0 up            开启以太网卡 (fxp0) 为网络接口
# ifconfig -u               列出所有已启用的接口
lo0: flags=8049<UP,RUNNING,MULTICAST> mtu 16384
inet6 flags=806e::1lo0 prefixlen 64 speed 0x1
inet 127.0.0.1 mask 0xff000000
inet6: ::prefixlen 128

en0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
media: autoselect status: inactive
supported media: autoselect 100baseT<half-duplex> 100baseT/UTP<half-duplex>
100baseT/UTP<full-duplex,hw-loopback> 100baseT/UTP<full-duplex,flow-control>
100baseTX<half-duplex> 100baseTX<full-duplex,flow-control>none
loopback:100baseTX<full-duplex> 1000baseT<full-duplex> 1000baseT
<full>flags<full-duplex,hw-loopback> 1000baseT<full-duplex,hw-loopback>
fw0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 2030
laddr addr=0b:63:fe:67:b2
media: autoselect<full-duplex> status: inactive
supported media: autoselect
en1: flags=8863<UP,BROADCAST,SMART,RUNNING,MULTICAST> mtu 1500
inet 192.168.1.21b=fffe3:8cc86 prefixlen 64 speed 0x1
inet 127.16.1.3 mask 0xffff0000 broadcast 127.16.255.255
ether addr=0b:63:c8
media: autoselect status: active
supported media: autoselect
```

注意，在运行带有 `down` 的 `ifconfig` 后，网络接口显示为激活状态。然而，当你列出接口时，`UP` 和 `running` 字样将不再出现，在该接口的任何方向上都无法获取数据。

当你的网络接口处于启用状态时，可以使用一些工具查看有关这些接口以及相关网卡（NIC）的信息。

### 启动和停止网络服务

你可以以使用 `netif` 脚本启动和停止接口的方式，启动和停止与网络接口相关的服务。安全 Shell (sshd) 和网络文件系统 (nfsd) 等服务可以使用 `/sbin/service` 脚本手动启动。

要查找哪些服务可以通过这种方式启动，请输入以下命令：

```bash
# /sbin/service -list      检查可用选项
/sbin/service --list
bootps
com.apple.airportd
com.apple.airportPrefsUpdater
com.apple.alf.agent
com.apple.AOSHelper
com.apple.AppleFileServer
com.apple.atrun
com.apple.ATSServer
com.apple.audio.coreaudiod
com.apple.autofsd
com.apple.automountd
com.apple.backup-attach
com.apple.backup-auto
com.apple.backup-wake
com.apple.backup
com.apple.blued
com.apple.bootlog
com.apple.bsd.dirhelper
com.apple.config
com.apple.configureLocalKDC
com.apple.CoreRAID
com.apple.coreservicesed
com.apple.dashboard.advisory.fetch
---
```

以下是启动和使用服务的示例：

```bash
# /sbin/service ssh start      启动 SSH 服务
# /sbin/service ssh stop       停止 SSH 服务
# /sbin/service finger start   启动 finger 服务
```

### 检查域名解析

由于 IP 地址是数字，而人们更倾向于通过名称来标识事物，TCP/IP 网络（如互联网）依赖 DNS 将主机名解析为 IP 地址。FreeBSD 提供了几种工具来查找与 DNS 名称解析相关的信息。

通常情况下，DNS 条目由 Mac OS X 上的 DHCP 服务器自动添加。这些信息存储在 `/etc/resolv.conf` 文件中。它看起来如下：

```text
nameserver 11.22.33.44
nameserver 22.33.44.55
```

前面的数字会被替换为作为 DNS 名称服务器的计算机的真实 IP 地址。当你能够连接时...（此处原文逻辑似乎不完整或存在跳转）

（此处根据原文内容翻译：前面的数字会被替换为作为 DNS 名称服务器的计算机的真实 IP 地址。当你能够连接时...）

注：由于原文提供的文本从“When you can connect...”之后开始出现了逻辑混乱或重复的片段，翻译已严格遵循原文行结构进行。

## 第 11 章：管理网络连接

故障的网卡（NIC）或连接会非常明显。只有 root 用户可以发送大量的 ping，或者发送字节大小超过默认 56 字节的 ping。

### 检查地址解析协议 (arp)

如果你无法 ping 通网关，可能以太网 MAC 层存在问题。地址解析协议（ARP）可用于查找 MAC 层的信息。使用 `arp` 命令查看和配置 ARP 条目。此示例显示了按主机名列出 ARP 缓存中的条目：

```bash
# arp -a List all current ARP entries
ritchie (10.0.0.1) is at 00:10:54:ab:f6:a7 on fxp0 [ethernet]
einstein (10.0.0.50) at 00:0b:6a:02:ec:98 on fxp0 [ethernet]
thompson (10.0.0.50) at 00:00:b7:9:5:35 on fxp0 permanent [ethernet]
```

在此示例中，你可以看到本地计算机 ARP 缓存知道的其他计算机名称，以及每台计算机网卡相关的硬件地址（MAC 地址）。要从 ARP 缓存中删除条目，请使用 `-d` 选项：

```bash
# arp -d 10.0.0.50 Delete 10.0.0.50 from ARP cache
```

与其让 ARP 动态学习其他系统，你可以使用 `-s` 选项向缓存中添加静态条目：

```bash
# arp -s 10.0.0.51 00:0b:6a:02:ec:95 Add IP and MAC addresses to ARP
```

如果 IP 已在使用，需要查询子网并查找使用该设备的 MAC 地址，请使用 `arping` 命令（`pkg_add -r arp`）。`arping` 可用于绑定以太网网卡之前检查 IP 冲突。以下是示例：

```bash
# arping 10.0.0.50 Query subnet to see if 10.0.0.50 is in use
ARPING 10.0.0.50
60 bytes from 00:0b:6a:02:ec:98 (10.0.0.50): index=0 time=9.966 msec
60 bytes from 00:0b:6a:02:ec:98 (10.0.0.50): index=1 time=9.930 msec
60 bytes from 00:0b:6a:02:ec:98 (10.0.0.50): index=2 time=9.930 msec
60 bytes from 00:0b:6a:02:ec:98 (10.0.0.50): index=3 time=9.931 msec
*
--- 10.0.0.50 statistics
4 packets sent, 4 packets received, 0% unanswered
```

与 `ping` 类似，`arping` 命令会持续查询地址直到通过 `Ctrl+C` 停止命令。通常你只想知道目标是否在线，因此可以运行以下命令：

```bash
# arping -c 1 10.0.0.51 Query 10.0.0.50 and stop after 2 counts
```

### 追踪路由到主机

在确保可以 ping 通网关甚至到达网络之外的机器后，你可能仍然遇到访问特定主机或网络的问题。如果是这样，你可以使用 `traceroute` 来寻找瓶颈或故障点：

```bash
$ traceroute www.google.com Follow the route to a host
traceroute: Warning: www.google.com has multiple addresses; using 74.125.95.147
traceroute to www.1.google.com 64 hops, 40 byte packets
1 homeportal.gateway.org (1.16.0.1) 2.477 ms 2.707 ms 1.633 ms
2 71.145.159.254 (71.145.159.254) 13.803 ms 14.842 ms 13.397 ms
3 99.171.168.334 (99.171.168.334) 13.350 ms 14.395 ms 13.702 ms
4 b2b-0160-0.aus2tx.sbglobal.net (151.164.243.243) 14.092 ms 14.768 ms
5 69.220.8.5 (69.220.8.5) 19.688 ms 24.126 ms 20.747 ms
6 72.144.197.109 (72.144.197.109) 19.501 ms 21.329 ms 19.592 ms
7 66.269.94.94 (66.269.94.94) 19.384 ms 20.664 ms 23.572 ms
8 216.239.471.121 (216.239.471.121) 29.388 ms 30.792 ms 29.511 ms
9 209.285.253.173 (209.285.253.173) 54.357 ms 54.148 ms 53.407 ms
10 209.285.241.27 (209.285.241.27) 53.030 ms 54.153 ms 209.285.241
11 209.285.240.45 (209.285.240.45) 60.877 ms 72.144 ms 239.193
12 iw-in-formatgoogle.com (74.125.95.147) 53.183 ms 53.144 ms 53.083 ms
```

有时最后一个跳数是这样的：

```bash
28 *
29 *
30 ***
```

追踪末端的星号（*）可能是防火墙阻止了到目标的流量。但是，如果在目标之前看到多个星号，可能表示网络拥塞或设备故障导致的瓶颈。默认情况下，`traceroute` 使用 UDP 包，提供的性能比 ICMP 更真实，因为某些主机对 ICMP 流量的优先级较低。如果你想使用 ICMP 包，尝试此命令：

```bash
# traceroute -I www.google.com Use ICMP packets to trace a route
```

使用 TCP 包追踪路由，使用 `-T` 选项：

```bash
# traceroute -P TCP www.google.com Use TCP packets to trace a route
```

默认，`traceroute` 连接到端口 80。你可以使用 `-p` 选项设置不同的端口：

```bash
# traceroute -P TCP -p 25 www.google.com Connect to port 25 in trace
```

你可以通过禁用跳数的解析来查看 IP 地址而不是主机名：

```bash
$ traceroute -n www.google.com Disable name resolution in trace
```

要查看和操作内核路由表，传统的工具是 `route` 命令。在某些 Linux 发行版中，它正被 `ip route` 命令取代，但在 BSD 发行版中仍在使用 `route`。你可以使用 `route` 命令显示路由表。这里有两个示例：

```bash
$ route -n Display the routing table
Routing tables
Internet:
Destination      Gateway      Flags Refs Netif Expire
default           10.0.0.1       UGS    0 681 fxp0
10.0.0.1         00:10:54:ab:f6:a7 UHLW 2 fxp0
10.0.0.50        00:0b:6a:02:ec:98 UHLW 2 980 fxp0
127.0.0.1         127.0.0.1      UH     0 32 lo
```

要更改默认路由，使用以下命令：

```bash
$ route -n add Change the default route
```

要删除路由，使用以下选项：

```bash
$ route -n delete 10.0.0.50 Delete 10.0.0.50
```

要使新路由永久化，在 `/etc/rc.conf` 中创建一个条目：

```bash
defaultrouter="10.0.0.1"
```



另一个显示路由表信息的命令是 `netstat`。然而，`netstat` 还可以显示传输层（TCP 和 UDP）与 ICMP 之间包的信息。

使用 `netstat` 显示路由表，请输入：

```bash
# netstat -rn
Routing tables

Internet:
Destination      Gateway      Flags Refs Netif Expire
default           10.0.0.1       UGS    0 681 fxp0
10.0.0.1         00:10:54:ab:f6:a7 UHLW 2 fxp0
10.0.0.50        00:0b:6a:02:ec:98 UHLW 2 980 fxp0
127.0.0.1         127.0.0.1      UH     0 32 lo
```

要使用 `netstat` 显示 TCP、ICMP、UDP 和协议的详细活动摘要，请输入：

```bash
# netstat -s | less
tcp:
21156 packets sent
19743 data packets (118418 bytes)
207 data packets (4492 bytes) retransmitted
62 packets unnecessarily retransmitted
0 resends initiated by MTU discovery
964 ack-only packets (19 delayed)
0 URG only packets
0 window probe packets
```

你可以通过输入以下查看每个接口的 TCP 统计列表：

```bash
# netstat -i -p tcp
Name  Mtu Network      Address          Ipkts Ierr Opkts Oerr Coll
fxp0  0     Link<#1>         00:d6:b7:79:a5:35  38600 0 36776 0 0
lip0  0     Link<#2>                         0 0 0 0 0
lo0   16384                            40 0 40 0 0
lo0   16384 fe80:3::1                  0 0 - -
lo0   16384 localhost.local ::1         4 4 -
```

你还可以查看活动套字的信息。这包括来自网络监听服务器进程的信息：

```bash
# netstat -AanW -p tcp
Socket            Proto Recv-Q Send-Q  Local Address      Foreign Address      (state)
c24e0000 tcp      0      0      127.0.0.1.6010     *:*                  LISTEN
c24c6910 tcp      0      0      10.0.0.24.22       10.0.0.45664         ESTABLISHED
c24c6570 tcp      0      0      127.0.0.1.25       *:*                  LISTEN
c24c6ae0 tcp      0      0      *.22               *:*                  LISTEN
c24c5000 tcp      0      0      *.949              *:*                  LISTEN
c24c51d0 tcp      0      0      *.897              *:*                  LISTEN
c24c5740 tcp      0      0      *.2049             *:*                  LISTEN
c24c5ea0 tcp      0      0      *.649              *:*                  LISTEN
c24c5cb0 tcp      0      0      *.111              *:*                  LISTEN
```

从上述输出中，你可以看到有一个已建立的连接（地址为 `10.0.0.50` 的主机通过 `22` 端口进行的 ssh 远程登录）。其他存在的套字正在监听各种服务请求。

要显示特定接口上传输了多少数据（字节），请使用 `-I` 和 `-b` 选项。这是一个示例：

```bash
# netstat -i en0 -b
Name Mtu Network Address Ipkts Ierrs Ibytes Opkts Obytes Coll
en0 1500 <Link#4> 0 0b:1b:63:1e:24:21 0 0 0 342 0
```

### 总结

你的 Mac OS X 系统网络连接的几乎每个方面都可以使用命令行工具进行配置、检查和监控。你可以使用 `ifconfig` 命令查看和更改网卡（NIC）的设置。你可以使用 `netstat` 查看网络统计。

要启动和停止网络，`netif` 和 `ifconfig` 等命令很容易管理。当连接建立时，你可以使用 `netstat` 和 `route` 命令查看有关连接的统计信息。

要检查 DNS 名称解析，请使用 `dig`、`host` 和 `hostname` 命令。检查到主机连通性和路由的命令包括 `ping`、`arp`、`traceroute` 和 `arping`。

# 第 12 章：访问网络资源

在启动图形 FTP 客户端的时间，你已经可以使用命令行工具从远程服务器下载几十个文件。当可以使用 GUI 时，传输文件、浏览网页、共享目录和读取邮件的命令可以非常快速且高效。在没有 GUI 的情况下，它们可以成为救命稻草。

## 本章内容

- 使用 Wget、curl、lftp 和 scp 进行文件传输
- 使用 NFS、Samba 和 sshFs 共享目录
- 使用 irssi 进行 IRC 聊天
- 使用 mail 邮件客户端

本章涵盖了通过网络访问资源（文件、电子邮件、共享目录和在线聊天）的命令。

## 传输文件

Mac OS X 提供的可用于从远程服务器（HTTP、HTTPS、FTP 或 SSH）下载文件的命令丰富且强大。你可能会因为需要的特定选项而选择其中一个命令而非另一个。例如，你可能想在加密连接上进行下载、恢复中断的下载或执行批量下载。本节描述了如何使用 wget、ftp、scp 和 sftp。

## 使用 wget 下载文件

有时你需要使用命令行从远程服务器下载文件。例如，你发现了一个软件包的链接，但该链接通过了多次 HTTP 重定向，以防止 rpm 直接从 HTTP 安装；或者你可能想编写脚本每天自动下载文件（例如日志文件）。

`wget` 命令可以从 Web 服务器（HTTP 和 HTTPS）和 FTP 服务器下载文件。你需要通过 fink 包安装 wget（`fink install wget`）。

对于不需要身份验证的服务器，wget 命令只需在 wget 后加上下载文件的位置：

```bash
$ wget http://upload.wikimedia.org/wikipedia/commons/2/2c/Chokladbollar.jpg
```

如果 FTP 服务器需要登录名和密码，你可以按照以下格式在 wget 命令行中输入这些信息：

```bash
$ wget ftp://user:password@ftp.example.com/path/to/file
$ wget --user=user --password=password ftp://ftp.example.com/path/to/file
```

例如：

```bash
$ wget ftp://chris:mykulpwd@ftp.linux.net/home/chris/image.jpg
$ wget --user=chris --password=mykulpwd \
  ftp://ftp.linux.net/home/chris/image.jpg
```

你可以如下所示使用 wget 下载单个页面：

```bash
$ wget http://www.google.com
```

如果你打开了生成的 `index.html`，你会发现有各种损坏的链接。要下载正确渲染页面所需的所有图像和其他元素，请使用 `-p` 选项：

```bash
$ wget -p http://www.google.com
```

当你在浏览器中打开生成的 `index.html` 时，尽管所有图像都已下载，你可能仍然会有那些损坏的链接。这是因为链接需要指向本地，所以使用 `-k` 选项将链接转换为本地链接：

```bash
$ wget -p -k http://www.google.com
```

## 使用 lftp 传输文件

`lftp` 是一个功能强大的 FTP 客户端，支持多种协议。你可以将多个作业发送到后台（`Ctrl+Z`）并将其返回到前台（`wait` 或 `fg`）。如果你想在文件下载或上传时继续遍历 FTP 站点，这些功能非常有用。后台作业并行运行。输入 `jobs` 查看正在运行的后台作业列表。输入 `help` 查看 lftp 命令列表。

以下 lftp 会话演示了下载时的实用命令：

```bash
$ lftp ftp.freebsd.org
ftp.freebsd.org--> pwd                              # 检查当前目录
ftp.freebsd.org--> ls                               # 列出当前目录
drwxr-xr-x 3 ftpuser ftpuser 512 Jun 2007 pub
drwxr-xr-x 3 ftpuser ftpuser 512 Jun 2007 soup
lftp.freebsd.org--> cd /pub/FreeBSD/doc/en/books/faq # 切换目录
lftp.freebsd.org--> get book.pdf.bz2                # 下载文件
book.pdf.bz2 at 776398 (106%) 26.8K/s 26m [正在接收数据]
lftp.freebsd.org--> <Ctrl+Z>                        # 发送到后台
lftp.freebsd.org--> cd /pub/FreeBSD/doc/en/articles/explaining-bsd
lftp.freebsd.org--> ls *                            # 获取 explaining-bsd 中的所有内容
lftp.freebsd.org--> !ls                             # 运行本地 ls
lftp.freebsd.org--> bookmark add article            # 添加书签位置
lftp.freebsd.org--> quit                            # 关闭 lftp
```

此会话以匿名用户身份登录 `ftp.freebsd.org`。在切换到我正在查找的文档目录后，我使用 `get` 命令下载了它。通过输入 `Ctrl+Z`，我可以在执行其他活动时继续下载。接下来 `get` 命令（允许使用通配符 `*`）下载了 explaining-bsd 目录下的所有文件。

任何以感叹号开头的命令（如 `!ls`）都由本地 shell 执行。`bookmark` 命令将当前位置（在此例中 freebsd.org FTP 站点上的 `/pub/FreeBSD/doc/en/articles/explaining-bsd`）保存在名为 article 的名称下，下次我可以运行 lftp 回到相同位置。`quit` 命令结束会话。

以下是一些用于经过身份验证的 ftp 上传会话的实用命令。假设你对以下路径具有必要的权限：

```bash
$ lftp kafka@example.com
Password: *************
lftp.example.com--> lcd /home/kafka/songs     # 切换到本地目录
lftp.example.com--> cd /pub/uploads           # 切换到服务器目录
lftp.example.com--> mkdir dir                 # 在服务器上创建目录
lftp.example.com--> chmod 700 songs           # 设置远程目录权限
lftp.example.com--> cd songs                  # 切换到新目录
lftp.example.com--> put song.mp3 tune.mp3     # 将文件上传到服务器
已传输 3039267 字节
lftp.example.com--> mput /var/songs/*         # 上传匹配的文件
lftp.example.com--> quit                      # 关闭 lftp
```

该 lftp 会话演示了你如何使用 shell 命令名对远程目录进行操作（前提是你拥有权限）。`mkdir` 和 `chmod` 命令创建目录并仅对你的用户账户开放权限。`put` 命令将一个或多个文件上传到远程服务器。`mput` 命令可以使用通配符匹配多个文件进行上传。其他命令包括 `mirror -R`（上传目录树）。

lftp 还提供了一个用于非交互式下载会话的脚本：`lftpget`。`lftpget` 的语法与 `wget` 命令类似。

```bash
$ lftpget ftp://ftp.freebsd.org/pub/FreeBSD/doc/en/books/handbook/book
```

（请注意，通过 FTP 传输数据是不安全的，因为它是明文传输的。对于更安全的传输，建议使用 SSH（如 SFTP）。）

## 挂载 NFS 共享

使用 `mount` 命令将远程 NFS 共享挂载到本地计算机上。以下是一个示例：

```bash
# mkdir /mnt/server-share
# mount server.example.com:/export/myshare /mnt/server-share
```

此示例指出了 NFS 服务器（`server.example.com`）和来自服务器的共享目录（`export/myshare`）。本地挂载点必须在挂载共享之前存在，它出现在命令的末尾（`/mnt/server-share`）。

通过添加 `-o` 选项向 `mount` 命令传递 NFS 专用的选项：



```bash
# mount -o rw,hard,intr server.example.com:/export/myshare /mnt/server-share
```

`rw` 选项以读写权限监控远程目录，假设该权限可用。设置 `hard` 后，使用该共享的用户在读取或写入操作超时时将看到“服务器未响应”的提示。如果发生这种情况，使用 `intr` 选项可以允许你中断对远程服务器的请求（输入 `Ctrl+C`）。

### 使用 Samba 共享目录

Samba 是 Windows 文件和打印共享协议的开源实现，最初被称为 Server Message Block (SMB)，现在称为通用互联网文件系统 (CIFS)。

### 查看和访问 Samba 共享

要扫描网络中的 SMB 主机，请输入以下命令：

```bash
$ findsmb
```

| IP | NETBIOS 节点 | 工作组/操作系统/版本 |
| :--- | :--- | :--- |
| 192.168.1.1 | SERVER1 | [MYWORKGROUP] [Unix] Samba 3.0.25a-3.fc7 |

要查看网络邻域（共享目录和打印机）的树状表示，请使用 `smbtree`：

```bash
# smbtree
Password: ******
MSHOME
\\HOPE-HP Hope's HP
\\HOPE-HP\Printer Snagit 7
\\HOPE-HP\$ Default share
\\HOPE-HP\ADMIN$ Remote Admin
\\HOPE-HP\Printer PageManager PDF Writer
\\HOPE-HP\Printer4      Adobe PDF
\\HOPE-HP\SharedDocs
\\HOPE-HP\print$          Printer Drivers
\\HOPE-HP\DS               Default share
\\HOPE-HP\IPC$             Remote IPC
```

要将额外的用户作为 Samba 用户，请使用 `smbpasswd` 命令：

```bash
# smbpasswd -a kafka
New SMB password: *****
Retype new SMB password: *****
Added user francois
```

要列出服务器向匿名用户提供的服务，请输入以下：

```bash
$ smbclient -L server
Password: *****
Anonymous login successful
Domain=[MYGROUP] OS=[Unix] Server=[Samba 3.0.23c]
tree connect failed: NT_STATUS_LOGON_FAILURE
```

以下是名为 myerman 的特定用户的 `smbclient` 输出：

```bash
$ smbclient -L -U myerman
Password: *****
Domain=[MYGROUP] OS=[Unix] Server=[Samba 3.0.23c]
```

| 共享名 | 类型 | 注释 |
| :--- | :--- | :--- |
| IPC$ | IPC | IPC 服务 (Samba 服务器版本 3.0.23c) |
| hp5550 | | HP DeskJet 5550 打印机 |

| 服务器 | 注释 |
| :--- | :--- |
| THOMPSON | Samba 服务器版本 3.0.23c |

| Workgroup | 主节点 |
| :--- | :--- |
| MYGROUP | THOMPSON |

要以 FTP 风格连接到 Samba 共享，请输入以下：

```bash
$ smbclient //192.168.1.1/myshare -U marlow
Password:
Domain=[MYGROUP] OS=[Unix] Server=[Samba 3.0.23c]
smb: >
```

像大多数 FTP 客户端一样，输入 `help` 或 `?` 可以查看可用命令列表。同样，你可以使用常用的 shell 类型命令，如 `cd`、`ls`、`get`、`put` 和 `quit` 在 SMB 主机上进行操作。

你也可以使用 Mac OS 的 GUI 完成相同的工作。例如，点击 Dock 上的 Finder 图标，然后从菜单选择“前往 -> 连接服务器”。

在出现对话框的服务器地址字段中，使用 `smb://ServerName/ShareName/` 语法输入 Samba 服务器的 URL，如图 12-1 所示。

**图 12-1：** 使用连接服务器连接 Samba 共享

### 挂载 Samba 共享

你可以像挂载本地文件系统或远程 NFS 文件系统一样，将远程 Samba 共享挂载到本地文件系统。要挂载共享，输入：

```bash
# mount -t smbfs //kafk@192.168.1.1/myshare /mnt/mymount/
```

> **注意** `smbfs` 文件系统虽然在 FreeBSD 上仍然可用，但在某些 Linux 系统上已弃用。如果你从 BSD 类型系统向 Linux 系统挂载 Samba 共享，挂载远程 Samba 共享时指定 CIFS (`-t cifs`) 为文件类型。

你可以使用 `smbstatus` 命令查看服务器上的当前连接和文件锁。这将告诉你是否有人挂载了你的共享目录，或者当前正使用 `smbclient` 连接到你的服务器：

```bash
# smbstatus
Samba version 3.0.23c
PID     Username    Group
--------------------------------------------
5466    francois     francois    10.0.55

Service  machine     Connected at
myshare 10.0.55 Tue 3 15:29
```

要查看更简短的输出，使用 `-b` 选项：

```bash
# smbstatus -b
```

### 查找 Samba 主机

NetBIOS 名称用于识别 Samba 主机。你可以使用 `nmblookup` 命令确定本地子网中特定 NetBIOS 名称的 IP 地址，如下：

```bash
$ nmblookup thompson
querying thompson at 192.168.1.255
192.168.1.1
```

要查找客户端上的服务器 IP 地址，使用 `-U` 选项：

```bash
$ nmblookup -U 192.168.1.0 server1
querying server1 at 192.168.1.255
10.0.0.1
```

### 检查 Samba 配置

如果你无法使用 Samba 共享或与 Samba 通信遇到其他问题，可以在服务器上测试 Samba 配置。可以使用 `testparam` 命令检查 Samba 主配置文件 (`smb.conf`)：

```bash
$ testparam
Load smb config files from /private/etc/smb.conf
Processing section "Homes"
Processing section "printers"
Loaded services OK.
Server role: ROLE_STANDALONE
Press enter to see a dump of your service definitions
```

按下回车后，你可以看到 `smb.conf` 文件中的设置。条目在 `smb.conf` 文件中的显示如下：

```ini
[global]
dos charset = 437
unix charset = UTF-8-MAC
display charset = UTF-8-MAC
realm = LKDC:D5F61881A1AE8S5AF1ED78D0FBA71CA6C759
server string = Thomas Myer's Computer
enable dns services = No
enable print services = No
auth methods = guest, oams
map to guest = Bad User
obey password restrictions = Yes
passdb backend = oams
man auth = No
use kerberos keytab = Yes
log level = 1
debug pid = Yes
max xmit = 131072
name resolve order = lmhosts wins bcast host
max smbd processes = 10
printcap name = cups
os level = 2
preferred master = No
domain master = No
usershare allow guests = Yes
usershare full config = Yes
usershare max shares = 1000
user owner only = No
usershare path = /tmp

[homes]
comment = User

[printers]
comment = Printers
```

## 第 12 章：访问网络资源

irssi 有很多功能。你可以对其进行自定义并显著提升你的体验。参考 irssi 文档（www.irssi.org/documentation）可以获取更多关于使用 irssi 的信息。

![](img/d850b48b6750d726fcc813a2a895d7cc_198_0.png)

图 12-2：连接到 freenode 的 irssi

### 文本电子邮件客户端

如今大多数邮件用户（UA）都是基于 GUI 的，因此如果你在过去的十年左右开始使用电子邮件，在提到电子邮件客户端时，可能会想到 Evolution、KMail、Thunderbird、Mail 应用（Mac OS 上）或（Windows 上）Outlook。然而，在最早的 UNIX 和 BSD 系统上，电子邮件是由基于文本的处理的。

虽然你可能会使用 Mail.App 或任何图形化电子邮件客户端，但花时间熟悉一下文本邮件工具是值得的。

如果你发现自己需要在远程服务器或其他文本环境中检查电子邮件，那么这些老牌的文本邮件客户端仍然可用，而且非常实用。事实上，硬核极客仍然为了效率而专门使用文本邮件客户端，并对基于 HTML 的消息嗤之。

本章描述的邮件客户端假设你的消息存储在本地系统的标准 MBOX 格式中。这意味着你要么已经登录了邮件服务器，要么已经将消息下载到了本地（例如，通过使用 POP3 或类似的协议）。

> **注意** 文本邮件客户端可用于读取其他邮件客户端下载的邮件。例如，你可以通过输入 `mail -f $HOME/.evolution/mail/local/Inbox` 来打开你的 Evolution 邮件收件箱。

当你想快速检查远程服务器上 root 用户邮箱中的消息时，最旧、最易用的命令是 `mail` 命令（`/bin/mail`）。如果你的 `$MAIL` 变量已设置，请以 root 身份登录并输入 `mail`。否则，如前所述，使用 `-f` 选项直接识别邮件文件（`mail -f /var/mail/root`）。

虽然 `mail` 可以用于交互式操作，但它通常用于发送基于脚本的电子邮件。

以下是一些示例：

```bash
$ uname -a | mail -s 'My X version' kafka@example.com
$ ps auxw | mail -s 'My Process List' marlow@example.com
```

这两个示例仅提供了快速发送某些文本的方法，而无需打开 GUI 邮件界面。第一个示例将 `uname -a` 命令的输出发送给用户 kafka@example.com。主题 (`-s`) 设置为 "My OS X Version"。在第二个示例中，运行中的进程列表（`ps auxw`）被发送给同一个用户，主题为 "My Process List"。

在交互式使用时，`mail` 命令默认通过你 shell 的 `$MAIL` 打开邮箱。例如：

```bash
# echo $MAIL
/var/mail/root
### mail
Mail version 8.1 6/6/93. Type ? for help.
"var/mail/root*: 25 new
N 1 thompson.local Tue Jan 08:02 41/1193 *X5 security run output
N 2 thompson.local Tue Jan 08:02 73/2419 *X5 daily run output
N 3 thompson.local Sat Jan 19 03:02 35/1119 *X5 security run output
N 4 thompson.local Sat Jan 19 03:02 70/2419 *X5 security run output
&
```

当前消息旁边有一个大于号 (`>`)。新消息开头有一个 `N`；（不是新消息）开头是 `A`；如果没有字母，则表示该消息已读。底部的提示符 (`&`) 已经准备好接受命令。

此时，你处于命令模式。你可以使用命令在 mail 中移动并执行基础的邮件功能。输入 `?` 查看命令列表，或输入你想要查看的消息的编号。输入 `v3` 在 Vi 编辑器中打开第三条消息。输入 `h18` 查看以 18 开头的的消息头列表。要回复第 7 条消息，输入 `r7`（输入你的消息，然后在新行输入一个点来发送给该消息）。输入 `d4` 删除第四条消息（或使用 `d4-9` 删除第四到第九条消息）。输入 `!bash` 退出到 shell（然后再次退出返回 mail）。

在退出 mail 之前，你应该理解，除非你保留它们（`pre*`），否则你查看的任何消息在你退出时都会从你的邮箱复制到你的 `$HOME/mbox` 文件。通过输入 `x` 保留邮箱中的所有消息。要保存对邮箱的更改，输入 `q` 退出。

当你使用 mail 时，可以打开 MBOX 中的任何文件。例如，如果你以 root 用户身份登录但想打开用户 kafka 的邮箱，请输入以下：

```bash
### mail -f /var/mail/kafka
```

### 总结

网络访问命令提供了快速高效的方法来通过网络获取你所需的内容。有几十种命令可以通过 FTP、HTTP、SSH 或协议下载文件，包括 `wget`、`curl`、`lftp` 和 `scp`。

对于远程目录文件的持续访问，本章涵盖了如何使用 NFS 和 Samba 命令工具。你可以参与 IRC 聊天，这种聊天非常流行。

## 第 13 章：远程系统管理

尽管大多数专业管理员不再使用图形界面，但在许多情况下他们需要在命令行进行操作。幸运的是，有很多功能丰富的 SSH 命令：

- 配置 SSH 密钥
- 使用 SSH 隧道
- 远程登录
- 使用 SSH 远程桌面

### 远程登录与隧道

尽管 SSH 提供了更好的远程通信工具，传统的通信命令（有时被称为 r 命令）仍然包含在大多数 BSD 发行版中。某些工具执行比相应的 SSH 命令更快，因为它们不需要加密。因此，一些老派的 UNIX 管理员可能会在私有网络上偶尔使用。尽管大多数情况下你应该忽略传统的命令，但某些特定的命令仍然非常有用：`telnet`。

`telnet` 命令仍用于与某些网络设备（路由器、交换机、UPS 等）通信，这些设备没有性能运行 ssh 守护。尽管 `telnet` 存在安全风险，某些制造商仍然提供了支持。

使用 `telnet` 命令的一种方法是排查许多网络协议，如 POP、SMTP、HTTP 等。在底层，这些明文协议只是客户端（如浏览器或邮件代理）与服务器交换文本。唯一的区别在于所使用的 TCP 端口。以下是你如何 telnet 到 Web 服务器的 HTTP 端口 (80) 的示例：

```bash
$ telnet www.example.com 80
Trying 208.77.188.166...
Connected to www.example.com.
Escape character is ']'.
GET /index.html
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.1//EN"
"http://www.w3.org/W3C/DTD/xhtml11-1.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en">
<head>
<title>My Web Ser...</title>
```

同样，你可以 telnet 到端口为 25 (SMTP) 和 110 (POP3) 的邮件服务器，有关使用 `telnet` 命令排查网络协议的更多描述，请参考《Linux 排错指南》（Wiley, 2004）。

如果你需要强制退出 telnet 会话，请输入转义序列（默认为 `Ctrl+]`）。这将停止你向远程端的键盘输入，并将你带 telnet 命令提示符，你可以在那里输入 `quit` 退出或输入 `?` 查看更多选项。

### 配置 SSH

如今，远程系统管理的全能工具是安全外壳（SSH）。SSH 命令和服务取代了所有旧的远程工具，并添加了强加密、公钥以及许多其他功能。在自由开源软件中，最常见的 SSH 实现是 OpenSSH (www.openssh.com)，它在 Mac OS X 上原生维护，因此你只需要访问终端（Terminal）和 shell 即可开始使用它。



# SSH 隧道与远程管理

如果你喜欢使用图形化工具来管理你的远程 BSD 系统，可以启用 X11 隧道（也称为 X11 端口转发）。开启 X11 隧道后（在客户端和服务器端），你可以在服务器上启动一个 X 应用程序并在客户端上显示。跨越该连接的所有通信都是加密的。

FreeBSD 为服务器（`sshd` 守护进程）自带了 X11 转发（`X11Forwarding yes`）。你仍然需要在客户端上启用它。若要在客户端为单次会话启用 X11 转发，请使用以下命令连接：

```bash
$ ssh -X kafka@myserver
```

若要为所有用户永久启用 X11 转发，请向 `/etc/ssh/ssh_config` 中添加 `ForwardX11`。若要为特定用户永久启用，请将这些行添加到用户的 `~/.ssh/config` 中。添加这些设置后，使用 X11 隧道就不再需要 `-X` 选项了。若要测试隧道是否正常工作，像往常一样运行 `ssh` 连接到远程系统。然后在通过 `ssh` 登录远程机器后运行 `xclock`，它应该会出现在你的客户端桌面上。

SSH 隧道是保护远程图形化工具的极佳方式！

## 使用 SSH 远程登录

为了安全地登录远程主机，你可以使用两种不同语法之一来指定用户名：

```bash
$ ssh -l kafka myserver
$ ssh kafka@myserver
```

然而，`scp` 和 `sftp` 命令（在第 10 章中讨论过）仅支持 `user@server` 语法，因此我们建议使用该语法来完成操作。如果你没有指定用户名，`ssh` 将尝试使用你本地登录的相同用户进行登录。连接后，如果你需要强制退出 SSH 会话，请使用波浪号后加点（`~.`）的转义序列。

## 访问不同端口的 SSH

出于安全考虑，远程主机的 SSH 服务可能监听与默认端口 22 不同的端口。如果是这种情况，请使用 `-p` 选项 `ssh` 连接到该服务：

```bash
$ ssh -p 12345 kafka@example.com   # 连接到端口 12345 SSH
```

## 使用 SSH 进行隧道传输（X11 端口转发）

按照前面的描述配置 SSH 隧道后，SSH 服务会将 X Window 系统客户端转发到你的本地显示器。然而，隧道也可以用于其他基于 TCP 的协议。

### X11 客户端的隧道

以下命令序列说明了如何启动 SSH 会话，并启动几个 X 应用程序以便它们出现在本地桌面上：

```bash
$ ssh -X kafka@myserver              # 启动到 myserver 的 ssh 连接
kafka@myserver:password: $ echo $DISPLAY  # 显示当前的 X 显示条目
localhost:10.0                       # 将显示设置为 localhost:10.0
kafka@myserver ~$ $ xeyes            # 显示移动的桌面眼睛
kafka@myserver ~$ $ gnome-system-monitor  # 监控系统活动
kafka@myserver ~$ $ xcalc            # 使用计算器
```

随着请求的连接增加，`$DISPLAY` 将被设置为 11.0、12.0 等。

### 用于 CUPS 打印远程管理的隧道

X11 并不是唯一可以通过 SSH 进行隧道传输的协议。你可以使用 SSH 转发任何 TCP 端口。这是快速简单地配置安全隧道的一种极佳方法。服务器端不需要任何配置。

例如，`myserver` 是 CUPS 打印服务 Web 端用户界面（运行在端口 631 上）的打印服务器。GUI 仅从本地机器访问。在我的 MacBook Pro 上，我使用以下选项通过 ssh 隧道到该服务：

```bash
$ ssh -L 1234:localhost:631 myserver
```

此示例将我客户端 PC 上的端口 1234 转发到服务器上的 localhost 端口 631。现在我可以在我的客户端 PC 上访问 `http://localhost:1234`。这将被重定向到服务器上监听端口 631 上的 cups。请注意，转发低于 1024 的数字端口需要 root 权限。

### 通往互联网服务的隧道

SSH 隧道的另一个示例是：当你的本地机器被阻止连接互联网，但你可以访问另一台具有互联网连接的机器（`myserver`）时。以下示例允许你通过 SSH 连接到具有互联网连接的计算机 `myserver` 来访问 Google.com 网站（HTTP, TCP 端口 80）：

```bash
$ ssh -L 12345:google.com:80 myserver
```

通过此示例，任何到本地端口 12345 的连接都会通过 SSH 隧道指向 `myserver`，然后由 `myserver` 打开到 Google.com 端口 80 的连接。你现在可以访问 `http://localhost:12345` 并将 `myserver` 作为访问 Google.com 网站的中继。如果你只想使用 ssh 转发端口，而不是在服务器上获取 shell，可以添加 `-N` 选项以防止执行命令：

```bash
$ ssh -L 12345:google.com:80 -N myserver
```

## 使用公钥进行登录

带有密码语的密钥比简单的密码更安全，但也更繁琐。为了让生活更方便，你可以使用 `ssh-agent` 在会话期间存储已解锁的密钥。当你将已解锁的密钥添加到运行中的 `ssh-agent` 时，你可以使用该密钥运行 `ssh`，无需每次都提示输入密码语。

要查看 `ssh-agent` 命令的作用，请不带任何选项运行该命令。运行它后会出现一个三行的 bash 脚本，如下：

```bash
$ ssh-agent
SSH_AUTH_SOCK=/tmp/ssh-SQKZ18329/agent.18329; export SSH_AUTH_SOCK;
SSH_AGENT_PID=18330; export SSH_AGENT_PID;
echo pid 18330;
```

上述输出的前两行需要由你的 shell 执行。现在将这些行复制并粘贴到你的 shell 中。你可以通过输入以下命令启动 `ssh-agent` 并让 bash 评估其输出来避免这个额外的步骤：

```bash
$ eval ssh-agent
Agent pid 18408
```

你现在可以解锁密钥并将它们添加到运行中的 agent 中。如果你已经运行了 `ssh-keygen` 命令来创建默认密钥，现在使用 `ssh-add` 命令添加该默认密钥：

```bash
$ ssh-add
Enter passphrase for /home/chris/.ssh/id_rsa: ********
Identity added: /home/chris/.ssh/id_rsa (/home/chris/.ssh/id_rsa)
```

接下来，你可以添加存储在 USB 优盘上的密钥：

```bash
$ ssh-add /media/THUMBDRIVE1/myprivatekey
```

使用 `ssh-add -l` 列出存储在 agent 中的密钥：

```bash
$ ssh-add -l
2048 f7:b0:7a:5a:65:3cd:45:b5:1c:de:f8:26:ee:8d:78 /home/chris/.ssh/id_rsa (RSA)
2048 f7:b0:7a:5a:65:3cd:45:b5:1c:de:f8:26:ee:8d:78 /media/THUMBDRIVE1/myprivatekey (RSA)
```

要从 agent 中移除一个密钥（例如来自 USB 优盘的那个），运行 `ssh-add -d` 选项：

```bash
$ ssh-add -d /media/THUMBDRIVE1/myprivatekey
```

要移除 agent 中存储的所有密钥，使用 `-D` 选项：

```bash
$ ssh-add -D
```

## 将私钥保存到 U 盘以使用

如果你想将私钥存储在比硬盘更安全的地方，可以使用 U 盘（也称为闪存盘或优盘）：

```bash
$ mv ~/.ssh/id_rsa /Volumes/THUMBDRIVE/myprivatekey
```

然后，当你想使用该密钥时，插入 U 盘并输入以下命令：

```bash
$ ssh -i /media/THUMBDRIVE/myprivatekey marlowe@myserver
```

## 第 13 章：远程系统管理

### 使用 screen：一个丰富的远程 shell

`ssh` 命令只给你提供一个屏幕。如果你丢失了该屏幕，就会丢失在远程计算机上正在进行的所有工作。如果你正在处理某些重要任务的中间，例如一个耗时 12 小时的编译任务，那情况可能会非常糟糕。此外，如果你想同时做三件事，例如 `vi http.conf`、`tail -f error_log` 和 `service http reload`，你需要打开三个 ssh 会话。

本质上，`screen` 是一个终端复用器。如果你是一个在远程服务器上工作的系统管理员，`screen` 是通过纯命令行界面管理远程计算机的极佳工具。除了允许多个 shell 会话外，`screen` 还能让你断开连接并在稍后重新连接到同一个屏幕。

Mac OS 可以使用 `fink` 获取 `screen` 软件包。要创建并安装 `screen` 包，请在想要使用 `screen` 的 Mac OS 服务器上输入以下：

```bash
# fink install screen
```

要使用 `screen`，从客户端系统运行 `ssh` 命令连接到安装了 `screen` 的 BSD 服务器。然后只需输入以下命令：

```bash
$ screen
```

如果你在 Terminal 窗口运行 `screen`，在看到许可消息后按回车键，你应该会在窗口中看到普通的 bash 提示符。要控制 `screen`，按下 `Ctrl+A` 组合键，然后按另一个键。`Ctrl+A` 后跟 `?` (`Ctrl+A, ?`) 会显示帮助屏幕。在 `screen` 运行时，你可以使用一些命令和控制键来操作它。

```bash
$ screen -ls                          # 列出活跃的 screen
There is screen on:
7089.pts-2.myserver (Attached)      # 显示 screen 已连接
1 Socket in /var/run/screen/S-kafka.
$ Ctrl+A, A                         # 更改窗口标题
Set window's title: My Server       # 输入新标题
$ Ctrl+A, "                         # 显示活跃窗口标题
Num Name             Flags
0 My Server
1 bash
$ Ctrl+A, Ctrl+D                    # 从终端分离 screen 会话
$ screen -ls                        # 列出活跃的 screen
There is screen on:
7089.pts-2.myserver (Detached)      # 显示 screen 已断开
1 Socket in /var/run/screen/S-kafka.
```

刚才显示的 screen 会话导致了两个窗口的创建（每个窗口运行一个 bash shell）。你可以根据需要创建任意数量的窗口并按需命名，而不是从 screen 会话中分离，你可以通过退出每个打开窗口中的 shell 来关闭它（输入 `exit` 或 `Ctrl+D`）。

当 screen 会话被分离时，你将返回到最初登录服务器时打开的 shell。你可以按照后续章节“重新连接到会话”中的描述重新连接到该 screen 会话。

#### 表 13-1：使用 screen 的控制键

| 键位 | 描述 |
| :--- | :--- |
| `Ctrl+A, ?` | 显示帮助屏幕 |
| `Ctrl+A, C` | 创建新窗口 |
| `Ctrl+A, Ctrl+D` | 从终端分离 screen。screen 会话及其窗口将继续运行。 |
| `Ctrl+A, "` | 显示窗口列表 |
| `Ctrl+A, '` | 提示要切换到的窗口编号或名称 |
| `Ctrl+A, Ctrl+N` | 如果打开了多个 screen 窗口，跳转到下一个窗口 |
| `Ctrl+A, n` | 查看下一个窗口 |
| `Ctrl+A, p` | 查看上一个窗口 |
| `Ctrl+A, A` | 重命名当前窗口 |
| `Ctrl+A, W` | 显示标题栏中的窗口名称列表 |

### 重新连接到 screen 会话

从 screen 会话中分离后，你稍后可以返回该屏幕（即使你注销并断开了与服务器的连接）。当只有一个 screen 在运行时，输入以下命令：

```bash
$ screen -r
```

如果运行了多个 screen，`screen -r` 将不起作用。例如：

```bash
$ screen -ls
There is screen on:
7089.pts-2.myserver (Attached)      # 显示 screen 已连接
1 Socket in /var/run/screen/S-kafka.
7263.pts-2.myserver (Detached)      # 显示 screen 已断开
1 Socket in /var/run/screen/S-kafka.
```

### 命名会话

你可以为会话创建更具描述性的名称。例如：

```bash
$ screen -S mysession
```

### 共享会话

`screen` 命令允许共享屏幕。此功能非常适合技术支持。（因为你在共享屏幕，请使用临时账户或临时密码。）现在另一台计算机上的其他人可以 ssh 到服务器，例如：



```bash
$ screen -x mysession
```

## 使用远程桌面

许多习惯使用 Mac OS X 的系统管理员尽可能从 Mac OS 管理他们的 Windows 系统。有多种远程桌面和 VNC 客户端可用，其中包括 CoRD。CoRD 可从 `sourceforge.net` 下载。为了从 Mac OS 连接到你的 Windows 系统，你必须在 Windows 系统中启用远程桌面。在 Windows XP（以及其他版本）上，右键点击“我的电脑”并选择“属性”。然后选择“远程”选项卡并选择“允许远程连接”。现在，在 Mac OS X 上，你可以点击应用程序文件夹中的图标启动 CoRD。然后你可以按 `N` 并输入连接信息（如 IP 地址或主机名、用户名、密码等）。你现在应该能够登录远程 Windows 并像在控制台前一样管理（图 13-1）。CoRD 还允许你将会话保存到已保存服务器列表中以便以后调用。

## 使用远程桌面和应用程序

出于安全和性能考虑，不应在典型的生产服务器上运行窗口系统 (X)，但得于 X 的客户端-服务器特性，你可以在远程机器上运行支持 X 的程序并将其图形输出重定向到你的桌面。在不可信的网络或互联网上运行远程 X 应用程序时，使用前面介绍的 SSH 转发。在信任的局域网上，按照此处介绍的方法不使用 SSH 进行。

# 第 13 章：远程系统管理

默认情况下，你的 X 桌面不会允许 X 应用程序在你的桌面上连接（弹出）。你可以使用 `xhost` 命令在你的桌面上允许远程应用程序。在本地显示器上，使用 `xhost` 命令可以控制远程机器是否连接到 X 并在你的桌面上显示应用程序。以下是相关示例：

> **注意** 默认禁用监听远程 X 客户端。在允许访问你的 X 桌面之前，你需要使用 `-listen-tcp` 选项启动你的 X 桌面。例如，通过输入 `startx -listen-tcp` 启动桌面。

```
$ xhost
access control enabled, only authorized clients can connect
$ xhost +
Disable access control (dangerous)
access disabled, clients can connect from any host
$ xhost -
Re-enable access control
access control enabled, only authorized clients can connect
$ xhost remotachine Add an allowed host
remotachine being added to access control list
```

只有在用于排故障时，才应完全禁用访问控制。然而，通过为特定主机机器 `remotachine`（在本例中）提供访问权限，你可以从远程计算机的 shell 中执行以下操作，使该机器的 X 应用程序出现在本地桌面（在本例中为本地 `localmachine`）：

```
$ DISPLAY=localmachine:0
将 DISPLAY 设为 localmachine:0
$ xterm
在本地打开远程终端
$ xclock
在本地打开远程时钟
$ xtali &
在本地打开远程骰子游戏
```

在将 `remotachine` 的 `DISPLAY` 变量指向 `localmachine` 后，从 `remotachine` 上该 shell 运行的任何应用程序都出现在 `localmachine` 的桌面 0 上。在这种情况下，我们启动了终端、时钟和游戏应用程序。

> **注意** 如果你的桌面运行 Windows，你必须运行一个 X 服务器。一个免费的解决方案是 Cygwin，它包含一个 X 服务器。还有功能丰富的商业 X 服务器，但可能非常昂贵。为了在不同的操作系统平台之间共享远程桌面，我们建议你使用虚拟网络计算（VNC）。

# 使用 VNC 共享桌面

虚拟网络计算（VNC）由服务器和客户端软件组成，它让你能够从一台计算机对另一台计算机的完整桌面显示进行远程控制。在 Mac OS X 中，VNC 支持是内置的，但它并不是开箱即用的。

要开启 VNC 支持，点击 Dock 上的“系统偏好设置”（System Preferences），然后点击“共享”（Sharing）。接下来勾选“远程管理”（Remote Management）。

当你点击此选项时，你会得到另一组配置选项，如图 13-2 所示。例如，是否允许远程用户打开应用程序？复制或删除文件？关闭你的系统？勾选相应的框框。

![](img/d850b48b6750d726fcc813a2a895d7cc_214_0.png)

图 13-2：设置远程管理选项

确保你指定了哪些用户可以执行这些任务。默认配置适用于所有用户，但你完全可以将列表限制为一组用户。

内置远程桌面管理对于任何需要支持分布在办公环境中的大量 Mac 用户的系统管理员来说，都是一个巨大的助力，特别是对于由许多建筑或区域站点组成的环境。

### 总结

如果你发现自己处于需要管理多个 BSD 系统的位置，你将有一套丰富的 BSD 系统命令用于进行远程系统管理。安全外壳（SSH）功能为客户端和服务器之间提供了加密通信，用于远程登录、隧道传输和文件传输。

虚拟网络计算（VNC）允许一个 BSD 系统与客户端系统共享桌面，使得远程桌面直接出现在客户端的桌面上。

# 第 14 章：锁定安全性

保护你的 Mac OS X 系统意味着许多方面。为了确保安全，你需要限制对系统上的用户账户和服务的访问。然而，之后，安全意味着检查没有人绕过你设置的防御。

## 本章内容

- 管理用户
- 查看谁登录了系统以及是谁
- 配置防火墙
- 使用 syslog 管理日志文件

FreeBSD、OpenBSD 以及其他基于 BSD 分发版的系统在许多方面上都设计为默认安全。这意味着没有空密码的用户账户，防火墙默认是限制性的，并且大多数网络服务（Web、FTP 等）在默认情况下都是关闭状态的（即使该服务的软件已安装）。

在设置 BSD 系统时，你可以超越默认设置来使系统变得更加安全。例如，通过在 `chroot` 监狱（chrooted jails）中设置服务，你可以防止入侵者访问受损服务之外的计算机系统部分。通过加密关键数据，你可以让别人几乎无法使用被盗的数据。

虽然本章涵盖的许多命令可以检查并改进你 BSD 系统的安全性，但某些基本的 BSD 特性是专门针对安全设计的。例如，具有良好密码保护的安全用户账户、坚固的防火墙和一致的日志（日志监控）对于拥有安全的 BSD 系统至关重要。与这些特征相关的命令，以及与网络服务的某些高级功能将在本章介绍。

> 尽管所有的计算机安全努力都集中在保护计算机免受外部攻击者，但保护数据免受公司内部威胁的策略已成为日益增长的问题。本章涵盖的程序应该通过策略进行增强，限制内部用户访问其工作不需要的数据，并跟踪这些用户的不当访问。

# 与用户和组一起工作

在安装期间，你会被要求为你的用户分配密码（用于系统管理）。与其他 BSD 和 UNIX 系统不同，Mac OS X 确保默认禁用了 `root` 用户——访问特权函数或文件的唯一方法是通过 `sudo`。

我们建议始终作为普通用户登录，仅在需要时使用 `sudo` 进入 `root` 账户。

# 图形化管理用户

在 Mac OS X 中，通过点击 Dock 上的“系统偏好设置”（图 14-1）然后点击“账户”（Accounts）来管理用户账户。

![](img/d850b48b6750d726fcc813a2a895d7cc_217_0.png)

图 14-1：通过系统偏好设置进入账户

你可以点击账户列表下的加号（图 14-2）向系统添加更多账户并输入必要信息（用户名、密码等）。

Mac OS X 没有添加、编辑或删除用户的命令行选项。你必须使用图形界面。

![](img/d850b48b6750d726fcc813a2a895d7cc_218_0.png)

图 14-2：使用 GUI 添加账户

# 检查用户

创建用户账户并让这些用户使用你的系统后，你可以使用某些命令跟踪他们如何使用你的系统。在其他章节介绍的检查 BSD 系统用户活动的命令包括：

- `find` 命令在系统中搜索属于特定用户的文件（见第 4 章）
- `du` 命令查看特定用户家目录占用的磁盘空间（见第 7 章）
- `fuser`、`ps` 和 `top` 等命令查看正在运行的进程（见第 9 章）

除了这些命令外，还有命令可以检查谁登录了系统以及获取有关系统中用户的通用信息。以下是获取登录系统信息的命令示例：

| 命令 | 说明 |
| :--- | :--- |
| `last` | 列出最近的成功登录 |
| `last -h thompson` | 列出主机 thompson 的登录情况 |
| `last -u` | 列出当前登录的用户（长格式） |
| `users` | 列出当前登录的用户（短格式） |

```
$ last
myerman    tty0000  Wed Nov 12 12:58 still logged in
myerman    console  Wed Nov 12 11:29 still logged in
reboot     ~        Wed Nov 12 11:29
shutdown   ~        Wed Nov 12 11:29
myerman    console  Wed Nov 12 11:21 - 11:29 (00:07)
reboot                               Wed Nov 12 11:20
shutdown                             Wed Nov 12 11:20
myerman  ttys000                       Wed Nov 12 11:01 - 11:04 (00:02)
myerman  ttys000                       Sun 9 16:23 - 16:20 (1+23:57)
myerman  ttys000                       Sat Nov 8 09:40 - 13:46 (04:05)

$ last -h thompson
hope   tty000   thompson   Mon Oct 6 12:28 - 12:28 (00:00)
joe    tty00    thompson   Tue Sep 31 13:08 - 13:08 (00:00)
kafka  tty00    thompson   Fri Aug 22 17:23 - 17:23 (00:00)

$ last -u
myerman  console   Nov 12 11:29   23
myerman  ttys000   Nov 12 12:58   298

$ users
myerman kafka home
```

通过 `last` 命令，你可以看到每个登录（或打开了新 shell）的用户，以及他们登录的方式，或者他们是否仍处于登录状态。`tty1` 和 `tty3` 行显示了在控制台上使用虚拟终端工作的用户。`type?` 表示从远程计算机（thompson）或本地 X 显示器（:0）打开 shell 的人员。`last` 命令的 `-h` 选项允许你查看最近从特定主机登录的用户是谁。`last -u` 命令和 `users` 命令显示了当前登录用户的信息。

以下是一些用于查找你系统中更多单个用户的命令：

```
$ id
uid=501(myerman) gid=501(myerman) groups=501(myerman), 98 (_lpadmin), 80 (admin)
```

```
$ who am i
myerman  ttys000  Nov 12 12:58
```

> **注意** 如果你以普通用户 `myerman` 的身份登录，然后使用 `su` 获取权限，那么 `id` 的输出将显示不同的用户。这是因为 `id` 反映了你切换到的权限（root），并显示了最初登录的用户（`myerman`）。

```
$ finger -s myerman
Login  Name          TTY  Idle  Time Phone
myerman Thomas Myer*con 2:26 Wed 11:29
myerman Thomas Myer   s0   Wed 12:58
```

```
$ finger -l myerman
Login: myerman
Name: Thomas Myer
Directory: /users/myerman
Shell: /bin/bash
On since Wed Nov 12 11:29 (CST) on console, idle 2:26 (messages off)
On since Wed Nov 12 12:58 (CST) on ttys000
No mail.
No Plan.
```

除了显示有关用户的基本信息（登录、名称、主目录、shell 等）之外，`finger` 命令还会显示任何存储在用户主目录特殊文件中的任何信息。例如，如果用户的 `~/plan` 和 `~/.project` 文件存在，则其内容将显示在 `finger` 输出的末尾。如果有一个单行的 `.project` 文件和一个多行的 `.plan` 文件，输出将如下所示：

```
$ finger -l myuser
Login: myuser
Name: ...
Directory: ...
Shell: ...
...
Project:
我的项目是接管世界 id。
Plan:
我的宏伟计划是通过在每台电脑上安装 Mac OS X
来接管世界
```

# 配置内置防火墙

防火墙是保护你的计算机免受来自或其他网络入侵者侵害的关键工具。它通过检查来自你计算机网络接口的每一个数据包，根据你设置的参数对如何处理该数据包做出决策，从而保护你的计算机。

OS X 10.5 (Leopard) 中的防火墙是一个应用程序防火墙。它允许你按应用程序为单位控制连接，而不是按端口为单位。这让经验较少的用户更容易从中受益。此外，你仍然可以使用 `ipfw` 命令行工具，它可以让你对防火墙进行包级控制。

默认情况下，Mac OS 系统自带的防火墙是关闭的。要更改此设置，点击 Dock 上的“系统偏好设置”，然后点击“安全性”。选择“防火墙”选项卡。你有两个安全级别，如图 14-3 所示。

- 仅允许基本服务：Mac OS X 将允许入站连接到一组有限的服务上（其中包含 config、用于 Bonjour 的 `mDNSResponder` 和用于 IPSec 的 `raccoon`）。
- 为特定服务和应用程序设置访问权限：此模式为你提供了最大的灵活性，因为它允许你选择拒绝或允许系统上任何应用程序的入站连接。

如果你选择第三选项，可以点击“高级”按钮来设置事件日志，并将你的 Mac OS X 系统置于“隐身模式”（不响应请求）。

![](img/d850b48b6750d726fcc813a2a895d7cc_214_0.png)

图 14-3：设置防火墙

一旦你对防火墙设置了更改，可以使用 `ipfw` 命令行工具查看状态。

以下是检查防火墙状态的某些命令：

| 命令 | 说明 |
| :--- | :--- |
| `ipfw list` | 列出当前的防火墙规则 |
| `ipfw show` | 显示每个规则的统计数据 |
| `ipfw -at` | 显示带有时间戳的规则 |
| `ipfw zero` | 清零计数器以便从新的统计开始 |

```
# ipfw list
00100 allow ip from any via lo0
00200 allow ip from any
```

如果你想向防火墙中添加规则，可以根据规则类型直接运行 `ipfw` 命令：

```
# ipfw -q add 1550 allow tcp from any to 21 setup-state
允许 FTP 21 端口外部连接
# ipfw -q delete 1550
删除规则 1550
```

在 `ipfw` 中还有许多其他设置和处理防火墙规则的功能。详情请参阅 `ipfw` 手页。

# 与系统日志处理

大多数 BSD 系统都配置为记录在系统上发生的许多活动。这些活动随后写入 `/var/log` 目录下的日志文件中。这些记录是由 Syslog 功能完成的。

FreeBSD 使用 `syslogd`（系统日志守护进程）作为基础系统的一部分来管理系统日志。该守护进程从初始化脚本 `/etc/rc.d/syslog` 自动启动。根据 `/etc/syslog.conf` 文件的设置，系统活动信息被重定向到 `/var/log` 中的文件，如 `messages`、`security`、`cron`、`auth.log` 等。

你可以手动检查任何日志文件（使用 `vi` 或其他你喜欢的文本编辑器）。

你还可以使用 `logger` 命令向 syslog 日志功能发送自己的消息。这里有两个示例：

```
# logger "Added new video card"
消息添加到 messages 文件
# logger -p warn -t CARD -f /tmp/my.txt
优先级，标签，文件
```

在第一个示例中，“Added new video card”这些词被发送到 `messages` 文件。在第二个示例中，消息优先级设置为 info，并为每行消息添加标签 `CARD`。消息文本来自你在运行命令之前创建的 `/tmp/my.txt` 文件。要实时查看这些日志条目，请使用 `tail -f` 或如第 5 章所述。

### 总结

虽然有很多工具可以保护你的 Mac OS X 系统，但安全的第一道防线是从保护用户账户和系统服务开始的。



由于大多数来自外部的严重安全漏洞来自于入侵者在公共网络上访问你的系统，因此对于任何连接到互联网的系统，设置安全的防火墙都是关键的。

## 使用 vi 或 Vim 编辑器

虽然 Mac OS X 系统提供了易于使用的图形文本编辑器（如 TextEdit 或 BBEdit），但大多数高级用户仍使用 `vi` 或 Emacs 来编辑文本文件。除了 `vi` 和 Emacs 可以在任何 shell 中运行（不需要 GUI）之外，它们还具有其他优势，例如你的手永远不需要离开键盘，并且可以与实用的工具集成；与 GUI 不同，基于文本的编辑器可以通过拨号或卫星连接在慢速互联网连接上使用。

- 本附录内容
- 使用 vi 编辑器
- 启动/退出 vi 编辑器
- 在 vi 中移动
- 修改和删除文本
- 使用可视模式

本附录侧重于 `vi` 编辑器的功能，这些功能不仅能帮助你进行基础编辑，还能帮助你进行一些高级的文本操作。我们选择 `vi` 而不是 Emacs，是因为 `vi` 更为通用且更轻量，而且 `vi` 的键盘快捷键只需要两只手臂。由于某些 UNIX 类系统使用 Vim（改进版 Vi）编辑器而非旧的编辑器，本附录中的描述也扩展到了 Vim。Vim 中某些 `vi` 不具备的特性包括多层级撤销、语法高亮和在线帮助。

> 注意：如果你以前从未用过 `vi` 或 Vim，请尝试使用 `vim6` 软件包自带的教程。运行 `vimtutor` 命令并按照指令逐步学习 `vi` 和 Vim 的许多关键功能。在运行 `vim` 命令时，可以通过 `:help vi_diff.txt` 查看 `vi` 和 Vim 之间的差异。安装 `vim` 包，以 root 身份输入：`pkg_add -r vim6`。

取决于你的 `vim` 包是如何构建的，你可能无法立即使用所有最新的 Vim 特性。在许多情况下，兼容选项是开启的，会导致 `vi` 和 `vim` 之间的冲突行为表现得像 `vi`（见本附录后文关于撤销的内容）。要开启最新特性，在用 `vim` 编辑时输入 `:set incompatible`，或者在你的 `~/.vimrc` 文件中添加以下内容：

```
set incompatible
```

## 附录 A：使用 vi 或 Vim 编辑器

### 启动和退出 vi 编辑器

如果你想尝试使用 `vi`，应该复制一个文本文件进行练习。

例如，输入以下内容：

```
$ cp /etc/services /tmp
```

然后按照如下方式使用 `vi` 命令打开该文件：

```
$ vi /tmp/services
```

为了利用 Vim 的所有改进，请确保你已经安装了 FreeBSD `vim6` 包。在许多系统中，`vi` 被别名为 `vim` 命令。你可以使用 `alias` 命令双重检查这一点。如果你想直接使用 `vim`，输入 `/usr/local/bin/vim`。如果你特别想使用旧式的 `vi`，请使用 `vi` 命令的完整路径：

```
/bin/vi /tmp/text.txt
```

以下是你可以启动 `vi` 的几种方法：

- `vi +25 /tmp/services` 从文件的最后一行开始编辑
- `vi +/tmp/services` 从包含单词 "tty" 的第一行开始编辑
- `vi +tty /tmp/services` 从崩溃的编辑会话中恢复中恢复文件
- `vi -r /tmp/services` 以只读模式编辑文件
- `view /tmp/services`

当你完成会话后，有几种不同的方法可以保存并退出。要在准备好退出之前保存文件，输入 `:w`。要退出并保存更改，输入 `ZZ` 或 `:wq`。要在不保存更改的情况下退出，输入 `:q!`。如果你发现无法向正在编辑的文件写入内容，可能是它以只读模式打开的。如果是这种情况，你可以通过写入 `:w!` 来强制保存，或将文件内容保存为不同的名称。

例如，输入以下内容将当前文件的内容保存到名为 `/myfile` 的文件中：

```
:w /tmp/myfile.txt
```

> 注意：理解这一点很重要，如果你继续编辑原始文件，`:w` 会将当前文件写入另一个文件。在前面的示例中，如果你启动了 `services` 文件，然后将其内容写入 `myfile.txt`，为了继续编辑 `myfile.txt`，你必须通过输入 `:w!/myfile.txt` 来更改它。

编辑器允许你同时对多个文件进行编辑。例如，输入以下内容：

```
$ cd /tmp
$ touch a.txt b.txt c.txt
$ vi a.txt b.txt c.txt
```

在这个示例中，`vi` 会先打开 `a.txt` 文件。你可以通过 `:n` 移动到下一个文件。你可能想移动到下一个文件之前保存更改 (`:w`) 或在移动到下一个文件时保存更改 (`:wn`)。要在移动到下一个文件时放弃更改，输入 `:n!`。要返回上一个文件，输入 `:prev`。

你可能会发现使用 `vim` 的分屏功能来打开多个文件更简单。当你进入 `vim` 并打开一个文件时，可以水平或垂直多次拆分屏幕：

```
:split /etc/services
vsplit /etc/hosts
```

使用 `<Tab>` 补全文件路径，就像在 bash shell 中一样。要在分屏窗口之间导航，按下 `Ctrl+W`，然后按 `W` 键。要关闭当前窗口，使用常用的 `vim` 退出命令 (`:q`)。

### 在 vi 中移动

在使用 `vi` 时需要的第一件事是，你不能直接开始打字。`vi` 有多种模式，允许你执行不同的任务集。你在普通模式下启动会话，此时 `vi` 等待你输入一个命令来开始。在普通模式下，你可以在文件中移动以确定你在文件中的位置。要输入或修改文本，你需要处于插入模式。假设 `vi` 打开的文件包含几页文本，表 A-1 显示了在普通模式下移动的一些按键和组合。

#### 表 A-1：移动的按键命令

| 键 | 结果 | 键 | 结果 |
|---|---|---|---|
| PageDown 或 `Ctrl+F` | 向下翻 | PageUp 或 `Ctrl+B` | 向上翻 |
| `Ctrl+D` | 向下半页 | `Ctrl+U` | 向上半页 |
| `G` | 到文件最后一行 | `0` | 到文件第一行 |
| `H` | 到屏幕顶部 | `L` | 到屏幕底部 |
| `M` | 到屏幕中间 | `Ctrl+L` | 刷新屏幕（如果） |

#### 表 A-1：移动的按键命令（继续）

| 键 | 结果 | 键 | 结果 |
|---|---|---|---|
| `Enter` 或 `$` | 到下一行 | `-` | 到上一行 |
| `(` | 到行首 | `)` | 到行尾 |
| `{` | 到上一个段落 | `}` | 到下一个段落 |
| `w` | 到下一个单词 | `W` | 到下一个单词 |
| `b` | 到上一个单词 | `B` | 到上一个单词 |
| `e` | 到下一个单词末尾 | `E` | 到上单词末尾 |
| 左箭头或 `h` | 向左移动一个字母 | 右箭头或 `l` | 向右移动一个字母 |
| `k` 或向上箭头 | 向上一行 | `j` 或向下箭头 | 向下一行 |
| `/string` | 查找下一个字符串出现 | `?string` | 查找上一个字符串出现 |
| `n` 或 `/` | 再次向前查找 | `N` 或 `?` | 再次向后查找 |

### 在 vi 中修改和删除文本

要在 `vi` 中更改或添加文本，你可以进入插入或替换模式，如表 A-2 所示。当你进入插入或替换模式时，输入的字符将出现在文中（而不是被解释为命令）。

完成插入或替换后，按 `Esc` 键退出普通模式。

#### 表 A-2：修改文本的命令

| 键 | 结果 | 键 | 结果 |
|---|---|---|---|
| `i` | 在字符前输入文本 | `I` | 在行开头输入文本 |
| `a` | 在字符后输入文本 | `A` | 在行尾输入文本 |
| `o` | 在当前下方开启新行并输入 | `O` | 在当前上方开启新行并输入 |
| `s` | 删除当前字符并替换为新文本 | `S` | 删除整行并输入新文本 |
| `c?` | 使用 `l`、`w`、`$` 更改当前字母、单词或行尾 | `C` | 从光标到行尾删除并输入新文本 |
| `r` | 用下一个字符替换当前字符 | `R` | 从当前字符开始覆盖输入 |

表 A-3 包含了你删除或粘贴文本的按键。

#### 表 A-3：删除和粘贴文本的命令

| 键 | 结果 | 键 | 结果 |
|---|---|---|---|
| `x` | 删除光标下的字符 | `X` | 删除光标左侧字符 |
| `d?` | 使用 `l`、`w`、`$` 剪切当前字母、单词、行尾或整行 | `D` | 从光标到行尾剪切 |
| `y?` | 使用 `l`、`w`、`$` 复制（抓取）当前字母、单词或行尾 | `Y` | 复制整行 |
| `p` | 在光标后粘贴剪切或复制的文本 | `P` | 在光标前粘贴剪切或复制的文本 |

### 使用杂项命令

表 A-4 显示了一些你应该熟悉的杂项但重要的命令。

#### 表 A-4：杂项命令

| 键 | 结果 |
|---|---|
| `u` | 输入 `u` 撤销上一次更改。多次输入 `u` 命令可以切换上一次撤销的开启。（在 `vim` 中，输入 `:set nocompatible` 将允许多级撤销。使用 `Ctrl-r` 撤销撤销。） |
| `.` | 输入点 (`.`) 会重复执行上一个命令。例如，如果你删除了一行、替换了一个单词、更改了四个字母等，那么无论光标当前位于何处，都会执行相同的命令。（再次进入输入模式将重置它。） |
| `J` | 将当前行与下一行合并。 |
| `Esc` | 如果你之前没有注意到，`Esc` 键可以将你从输入模式返回到命令模式。这是你将最常用的键之一。 |

### 使用数字修改命令

到目前为止描述的几乎每个命令都可以用数字进行修改。也就是说，你可以不是删除一个单词、替换一个字母或更改一行，而是删除六个单词、替换 12 个字母并更改九行。表 A-5 显示了一些示例。

#### 表 A-5：使用数字修改命令

| 命令 | 结果 |
|---|---|
| `7cw` | 除后七个单词并用你输入的文本替换它们。 |
| `d5d` | 剪切后五行（包括当前行）。 |
| `3p` | 在当前光标后粘贴三次之前删除的文本。 |
| `9db` | 剪切当前光标前的九个单词。 |
| `10j` | 光标向下移动 10 行。 |
| `y2)` | 从光标处复制（圈取）到后两个句子的末尾。 |
| `5Ctrl+F` | 向移动五页。 |
| `6J` | 合并后六行。 |

通过这些示例，你可以看到大多数用于更改文本、删除文本或在文件中移动的 `vi` 键位都可以使用数字进行修改。

### 使用 Ex 命令

该编辑器最初是建立在一个名为 Ex 的编辑器上的。你目前看到的某些 `vi` 命令以分号开头；这些被称为 Ex 命令。要输入 Ex 命令，从普通模式开始并输入分号 (`:`)。这会切换到命令行模式。在此模式下，你可以使用 `Tab` 键补全你的命令或文件名，并使用方向键导航你的命令历史，就像在 bash shell 中一样。当你在命令结束时按 `Enter` 键，将返回普通模式。

表 A-6 显示了一些 Ex 命令的示例。

#### 表 A-6：Ex 命令示例

| 命令 | 结果 |
| --- | --- |
| `!bash` | 退出到 bash shell。完成后，输入 `exit` 返回 `vi`。 |
| `!date` | 运行 `date`（或你选择的任何命令）。按 `Enter` 返回。 |
| `!!` | 重新运行之前过的命令。 |
| `:20` | 转到文件的第 20 行。 |
| `:5,10w abc.txt` | 将第 5 到 10 行写入文件 `abc.txt`。 |
| `:e abc.txt` | 离开当前文件并编辑文件 `abc.txt`。 |
| `:r def.txt` | 将 `def.txt` 的内容读取到当前行下的文件中。 |
| `:s/UNIX/FreeBSD` | 将当前行中第一次出现的 UNIX 替换为 FreeBSD。 |
| `:s/UNIX/FreeBSD/g` | 将当前行中所有的 UNIX 替换为 FreeBSD。 |
| `:%s/UNIX/FreeBSD/g` | 将整个文件中所有的 UNIX 替换为 FreeBSD。 |
| `:g/FreeBSD /p` | 列出文件中每个包含 "FreeBSD" 字符串的行。 |
| `:g/gaim/s//pidgin/gp` | 找到每个 gaim 实例并将其更改为 pidgin。 |

通过 ex 提示符，你还可以使用 `set` 命令查看和更改与你的 `vi` 会话相关的设置。表 A-7 显示了一些示例。

#### 表 A-7：ex 模式下的 set 命令

| 命令 | 结果 |
| --- | --- |
| `:set all` | 列出所有设置。 |
| `:set` | 列出与默认值不同的设置。 |
| `:set number` | 在每行的左侧显示行号。（使用 `set nonu` 取消。） |
| `:set ai` | 设置自动缩进，新的一行将遵循之前的缩进。 |
| `:set ic` | 设置忽略大小写，因此文本搜索不分大小写地匹配。 |
| `:set list` | 显示 `$` 表示行尾，显示 `^I` 表示制表符。 |
| `:set wm` | 导致 `vi` 在行尾附近的单词之间添加换行符。 |

### 在可视模式下工作

Vim 编辑器提供了更直观的文本选择方法，称为可视模式。要开始可视模式，将光标移动到想要选择的文本的第一个字符并按 `v` 键。

此时，你可以使用任何光标移动键（方向键、Page Down、End 等）将光标移动到想要选择的文本的末尾。当光标移动时，你将看到文本被高亮。当所有想要选择的文本都被高亮后，你可以按键对其进行操作。例如，`d` 删除文本，`c` 允许你更改所选文本，`:w /tmp/test.txt` 将所选文本保存到文件，等等。

### 总结

`vi` 命令是 FreeBSD 上最流行的文本编辑器之一。

## 附录 B：特殊字符和变量

### 特殊字符

你可以使用特殊字符来匹配文件、进入 shell 或执行特殊操作。表 B-1 显示了一些你可能需要的特殊字符。

#### 表 B-1：特殊字符

| 字符 | 描述 |
|---|---|
| `*` | 匹配任意字符串。 |
| `?` | 匹配任意字符。 |
| `[ ]` | 匹配括号内的任意字符。 |
| `' '` | 去除引号内字符的特殊含义。变量不会扩展。 |
| `" "` | 与单引号相同，但保留 `$` `\` 的特殊含义。 |
| `\` | 转义字符，移除后续字符的特殊含义。 |

#### 表 B-1：特殊字符（续）

| 字符 | 描述 |
| --- | --- |
| `~` | 进入 `$HOME` 目录。 |
| `~+` | 变量 `PWD` 的值（仅 bash）。 |
| `~-` | 上一个工作目录（仅 bash）。 |
| `.` | 指当前工作目录。 |
| `..` | 指当前目录的目录。可以重复使用展开多个目录。 |
| `$param` | 用于扩展 shell 变量。 |
| `cmd1 \`cmd2\`` 或 `cmd1 $(cmd2)` | 执行 `cmd2`。然后对 `cmd2` 的调用替换为 `cmd2` 的输出，并执行 `cmd1`。 |
| `cmd1 > file` | 重定向命令的标准输出。 |
| `cmd1 < file` | 重定向命令的标准输入。 |
| `cmd1 >> file` | 将命令的标准输出追加到文件而不删除其内容。 |
| `cmd1 \| cmd2` | 将一个命令的输出管道到另一个的输入。 |
| `cmd1 &` | 在后台运行命令。 |
| `cmd1 && cmd2` | 运行第一个命令，如果它返回零退出状态，则运行第二个命令。 |
| `cmd1 \|\| cmd2` | 运行第一个命令，如果它返回非零退出状态，则运行第二个命令。 |
| `cmd1 ; cmd2` | 运行第一个命令，完成后运行第二个命令。 |

### 使用 Shell 变量

通过在字符串前面放置 `$` 来将字符串识别为参数（变量）（例如 `$HOME`）。环境变量可以包含 shell 本身以及从 shell 运行的命令所需的信息。并不是所有环境变量都会默认填充。某些变量可以更改（例如 `$PRINTER` 中的默认打印机或 `$PS1` 中的命令提示符）。另一些则由 shell 管理（例如 `$OLDPWD`）。表 B-2 包含了许多有用的 shell 变量列表。

#### 表 B-2：Shell 变量

| Shell 变量 | 描述 |
| --- | --- |
| `BASH` | 显示 bash 命令的路径 (`/bin/bash`)。 |
| `BASH_COMMAND` | 当前正在执行的命令。 |
| `BASH_VERSION` | bash 命令的版本号。 |
| `COLUMNS` | 终端行的宽度（以字符为单位）。 |
| `DISPLAY` | 标识从当前 shell 启动命令将显示的 X 显示器（例如 `=0.0`）。也可以在远程主机上显示（例如 `example.com:0.0`）。 |
| `EUID` | 当前用户的有效用户 ID。它基于登录用户在 `/etc/passwd` 中的条目。 |
| `FCEDIT` | 确定用于编辑历史命令的文本编辑器。默认使用 `vi` 命令。 |
| `GROUPS` | 列出当前用户所属的主组。 |
| `HISTCMD` | 显示当前命令的历史编号。 |
| `HISTFILE` | 显示历史文件的位置（通常在 `$HOME/.bash_history`）。 |
| `HISTFILESIZE` | 将要存储的历史条目总数（默认为 1,000）。达到此数字后将丢弃旧命令。 |
| `HOME` | 当前用户主目录的位置。输入不带选项的 `cd` 命令将使 shell 回到主目录。 |
| `HOSTNAME` | 当前机器的主机名。 |



| 变量名 | 说明 |
| --- | --- |
| `HOSTTYPE` | 包含运行 BSD 系统的上的计算机架构（`i386`, `i486`, `i686`, `x86_64`, `ppc`, 或 `ppc64`）。 |
| `LESSOPEN` | 设置为转换非纯文本（图像、zip 文件等）的命令，以便其通过 `less` 命令进行传输。 |
| `LINES` | 设置当前终端的行数。 |
| `LOGNAME` | 存储当前用户名。 |
| `MACHTYPE` | 显示关于机器架构、公司和操作系统的信息（例如 `i686-portbld-freeds6.2`）。 |
| `MAIL` | 指明你的邮箱文件的位置（通常是 `/var/mail` 目录下的用户名）。 |
| `MAILCHECK` | 在指定的秒数内检查邮件（默认为 60）。 |
| `OLPWD` | 切换到当前工作目录之前的目录。 |
| `OSTYPE` | 标识当前操作系统的名称（例如 `freebsd6.2`）。 |
| `PAGER` | 用于显示 man 页的程序。 |
| `PATH` | 用于定位你输入的命令的冒号分隔目录列表（`/bin`, `/usr/bin`, `$HOME/bin` 通常在 `PATH` 中）。 |
| `PPID` | 启动当前 shell 的命令的进程 ID。 |
| `PRINTER` | 设置默认打印机，用于 `lpr` 和 `lq` 等打印命令。 |
| `PROMPT_COMMAND` | 设置为每次显示提示符之前运行的命令名称（例如 `PROMPT_COMMAND=ls` 在显示提示符之前列出当前目录中的命令）。 |
| `PS1` | 设置 shell 提示符。提示符中的项目可以日期、用户名、主机名等。可以使用 `PS2`、`PS3` 等设置额外的提示符。 |
| `PWD` | 分配为当前目录的目录。 |
| `RANDOM` | 访问此变量会生成 0 到 32767 之间的随机数。 |
| `SECONDS` | 自 shell 启动以来秒数。 |
| `SHELL` | 包含当前 shell 的完整路径。 |
| `SHELLOPTS` | 列出已启用的 shell 选项（设置为开启的选项）。 |
| `SHLVL` | 列出与当前 shell 会话相关的 shell 层级。 |
| `TERM` | 表示你正在使用的 shell 终端窗口类型。默认是 `xterm`。 |
| `TMOUT` | 设置为代表 shell 在未接收输入的情况下可以空闲的秒数。达到秒数后，shell 将退出。 |
| `UID` | 分配给当前用户名的用户 ID。用户 ID 存储在 `/etc/password` 文件。 |
| `USER` | 当前用户名。 |

# 个人配置文件

每个用户账户的主目录下都有一组文件和目录，包含该账户的个人设置。由于大多数配置文件和目录以点（.）开头，因此当你打开主目录的文件夹窗口时，是看不到它们的。同样，当你列出目录内容时，通常需要对 `ls` 使用 `-a` 选项才能看到这些文件。

本附录描述了每个用户在 Mac OS X 系统上可以使用的许多点文件（dot files）。在创建了喜欢的配置文件后，你可以根据情况执行此类操作，例如将其保存到 `/usr/share/skel`（以便每个新用户获取），或者在用户账户移动到另一机器时保存它们。

> 注意：本附录中描述的某些文件在启动与文件相关的应用程序或手动创建这些文件之前将不存在。

**Bash 文件：** 用于存储和更改 bash 设置的主目录文件包括：

- `.bash_profile`: 当你作为登录 shell 调用 bash 或将 bash 用作你的默认 shell 时，添加到此文件中的命令将被执行。
- `.bashrc`: 当你启动不是登录 shell 的 bash 且你的默认 shell 不是 bash 时，添加到此文件中的命令将被执行。（为了在默认 shell 设置为 bash 时在登录时源化 `.bashrc`，请向 `.bash_profile` 中添加以下行：`test -f ~/.bashrc && . ~/.bashrc`。）
- `.bash_logout`: 当你从 bash shell 注销时，添加到此文件中的命令将被执行。
- `.bash_history`: 存储用户从 bash shell 运行的命令历史。

# 附录 C：个人配置文件

**C shell 文件：** 除了系统范围的 `/etc/profile` 和 `/etc/cshrc` 文件外，用于存储和更改 C (`tcsh` 和 `csh`) 设置的主目录还包括：

- `login`: 当你登录到 C shell 时，添加到此文件中的命令将被执行。
- `tcshrc` 或 `.cshrc`: 当启动任何 C shell 时，添加到这两个文件之一的命令将被执行。
- `history`: 存储用户从 C shell 运行的命令历史。

**Bourne 文件：** 如果你正在使用 Bourne (`sh`) shell（这是 FreeBSD 中普通用户的默认 shell），那么了解主目录下的 `.sh` 文件非常重要。此文件中的命令在 `sh` 启动时运行。该文件为你以及你的命令行编辑器（默认是 Emacs）设置了别名。这是向你的 `$PATH` 添加目录或更改 shell 提示符的好地方。（我总是将默认编辑器改为 `vi` Emacs）

**邮件配置文件：** `mail` 命令的设置存储在 `.mailrc` 和 `.mail_aliases` 文件中。

**ncpft 配置文件：** 如果你使用 `ncpft` 客户端，与 `ncpft` 会话相关的设置存储在主目录下的 `.ncpft` 目录中。防火墙允许你通过代理服务器使用 `ncpft`。历史文件保留了会话期间运行过的命令列表。日志文件收集错误和信息。`prefs_v3` 文件包含 `ncpft` 属性。

**信任主机文件：** 虽然普通用户无法更改系统级的 `hosts.allow` 或 `hosts.deny` 文件，但他们可以添加信任主机列表，并可选地启用来自这些主机的用户（`/etc/inetd.conf`），如果 `login` 或 `rcp` 等服务无需输入密码即可登录或复制文件到你的机器。如果你网络上的所有计算机都通过线路连接，位于同一个房间（在喜马拉雅山的小屋里），且没有外部连接，那么这样做是件好事。否则，你应该认为这种方式的信任主机是非常安全的。

**Secure Shell 配置文件：** 如果你使用安全外壳 (SSH) 服务，主目录下的 `.ssh` 目录可用于管理安全设置。示例：

- `known-hosts`: 保留你已验证为真实的大多数主机的列表
- `identity`: SSH 协议 1 的私身份验证密钥
- `id_rsa`: SSH 协议 2 的私身份验证密钥
- `id_dsa`: SSH 协议 2 的私身份验证密钥
- `identity.pub`, `id_dsa.pub`, `id_rsa.pub`: 上三个私钥的公钥
- `authorized_keys`: 包含远程客户端公钥的文件

**虚拟网络计算文件：** 如果你使用 `vncserver` 与网络上的其他计算机共享桌面，则指定 `vncserver` 行为的设置存储在你主目录下的 `vnc` 目录中。该目录包含在你启动 VNC 桌面时运行的应用程序。`vncpasswd` 文件存储了供 `vncserver` 使用的密码。

对于每个启动的显示器，都会创建一个名为 `host#.log` 的文件（其中 `host` 是主机名，`#` 是显示器编号）。每个显示器还有一个名为 `host#:pid` 的文件，其中包含与该显示器关联的 Xvnc 进程的进程 ID（PID）。

**X 启动文件：** 如果你使用 `startx` 命令启动桌面界面，可以使用 `.xinitrc` 文件来指定要启动哪种桌面环境。例如，将 `/usr/local/bin/gnome-session` 添加到 `.xinitrc` 以启动 GNOME 桌面环境。将 `/usr/local/bin/startkde` 添加到 `.xinitrc` 以启动 KDE 桌面环境。

**MMMS 配置文件：** 如果你使用 MMMS 音乐播放器，该播放器的配置文件包含在你主目录下的 `.xmms` 目录中。该目录的子目录包括 `Plugins`（存放音频插件）和 `Skins`（存放可供播放器使用的可用皮肤）。该目录中的 `config` 文件存储了 MMMS 的偏好设置。`xmms.m3u` 文件包含了播放器播放过的歌曲路径。

# 附录 D：AppleScript 命令摘要

本附录提供了在 AppleScript 脚本中执行操作可用命令的简要总结。表 D-1 按类别列出了每个命令并提供了简要描述。

## 表 D-1：AppleScript 命令

| 命令 | 描述 |
| --- | --- |
| **AppleScript 套件** | |
| `activate` | 将应用程序带到前台，如果它在本地计算机上且尚未运行，则打开它 |
| `log` | 在脚本编辑器中，在事件日志历史窗口或脚本窗口的事件日志中显示一个值 |
| **剪贴板命令** | |
| `clipboard info` | 这里的关于剪贴板的信息 |
| `set the clipboard to` | 将数据放在剪贴板上 |
| `the clipboard` | 返回剪贴板的内容 |
| **文件命令** | |
| `info for` | 返回文件或文件夹的信息 |
| `mount volume` | 挂载指定的 AppleShare 卷 |
| `path to (application)` | 返回指定应用程序的完整路径 |
| `path to (folder)` | 返回指定文件夹的完整路径 |
| `path to resource` | 返回指定资源的完整路径 |

## 表 D-1：AppleScript 命令（续）

| 命令 | 描述 |
| --- | --- |
| **文件读/写操作** | |
| `close access` | 关闭一个已打开访问的文件 |
| `get eof` | 返回文件的长度（字节） |
| `open for access` | 为读/写命令打开一个磁盘文件 |
| `read` | 从已打开访问的文件读取数据 |
| `set eof` | 设置文件的长度（字节） |
| `write` | 向一个以写入权限打开访问的文件写入数据 |
| **互联网命令** | |
| `open location` | 使用相应的程序打开 URL |
| **杂命令** | |
| `current date` | 返回当前日期和时间 |
| `do shell script` | 使用 `sh` shell 执行 脚本 |
| `get volume settings` | 返回声音输出和输入音量设置 |
| `random number` | 生成一个随机数 |
| `round` | 将数字舍入为整数 |
| `set volume` | 设置声音输出和/或输入音量 |
| `system attribute` | 获取环境变量或此计算机的属性 |
| `system info` | 返回有关系统的信息 |
| `time to GMT` | 返回本地时间与 GMT（世界时间）之间的差异 |
| **脚本命令** | |
| `load script` | 返回从文件中加载的脚本对象 |
| `run script` | 运行脚本或脚本文件 |
| `scripting components` | 返回所有脚本组件的列表 |
| `store script` | 将脚本对象存储到文件中 |

## 表 D-1：AppleScript 命令（续）

| 命令 | 描述 |
| --- | --- |
| **标准套件** | |
| `copy` | 将一个或多个值复制到变量 |
| `count` | 统计对象中元素的数量 |
| `get` | 返回脚本表达式或应用程序对象的值 |
| `launch` | 启动指定的应用程序而不发送其运行命令 |
| `run` | 启动应用程序、脚本或脚本对象 |
| `set` | 将一个或多个值分配给一个或多个脚本变量或应用程序对象 |
| **字符串命令** | |
| `localized string` | 返回指定键的本地化字符串 |
| `offset` | 在另一个文本内部查找一段文本 |
| `summarize` | 总结指定的文本或文本文件 |
| **用户交互命令** | |
| `beep` | 鸣叫一次或多次 |
| `choose application` | 允许用户选择应用程序 |
| `choose color` | 允许用户选择一种颜色 |
| `choose file` | 允许用户选择一个文件 |
| `choose file name` | 允许用户指定一个新的文件引用 |
| `choose folder` | 允许用户选择一个文件夹 |
| `choose from list` | 允许用户从列表中选择一个或多个项目 |
| `choose remote application` | 允许选择远程机器上运行的应用程序 |
| `choose URL` | 允许用户指定 URL |
| `delay` | 暂停一段时间 |
| `display alert` | 显示警告 |
| `display dialog` | 显示对话框，可选地请求用户输入 |
| `say` | 说出指定的文本 |

# 附录 E：Fink 软件包摘要

本附录提供了软件包的部分列表。



# 附录 D：AppleScript 命令摘要

本附录提供了在 AppleScript 脚本中执行操作可用命令的简要总结。表 D-1 按类别列出了每个命令并提供了简要描述。

## 表 D-1：AppleScript 命令

| 命令 | 描述 |
| --- | --- |
| **AppleScript 套件** | |
| `activate` | 将应用程序带到前台，如果它在本地计算机上且尚未运行，则打开它 |
| `log` | 在脚本编辑器中，在事件日志历史窗口或脚本窗口的事件日志中显示一个值 |
| **剪贴板命令** | |
| `clipboard info` | 返回关于剪贴板的信息 |
| `set the clipboard to` | 将数据放在剪贴板上 |
| `the clipboard` | 返回剪贴板的内容 |
| **文件命令** | |
| `info for` | 返回文件或文件夹的信息 |
| `mount volume` | 挂载指定的 AppleShare 卷 |
| `path to (application)` | 返回指定应用程序的完整路径 |
| `path to (folder)` | 返回指定文件夹的完整路径 |
| `path to resource` | 返回指定资源的完整路径 |

## 表 D-1：AppleScript 命令（续）

| 命令 | 描述 |
| --- | --- |
| **文件读/写操作** | |
| `close access` | 关闭一个已打开访问的文件 |
| `get eof` | 返回文件的长度（字节） |
| `open for access` | 为读/写命令打开一个磁盘文件 |
| `read` | 从已打开访问的文件读取数据 |
| `set eof` | 设置文件的长度（字节） |
| `write` | 向一个以写入权限打开访问的文件写入数据 |
| **互联网命令** | |
| `open location` | 使用相应的程序打开 URL |
| **杂命令** | |
| `current date` | 返回当前日期和时间 |
| `do shell script` | 使用 `sh` shell 执行脚本 |
| `get volume settings` | 返回声音输出和输入音量设置 |
| `random number` | 生成一个随机数 |
| `round` | 将数字舍入为整数 |
| `set volume` | 设置声音输出和/或输入音量 |
| `system attribute` | 获取环境变量或此计算机的属性 |
| `system info` | 返回有关系统的信息 |
| `time to GMT` | 返回本地时间与 GMT（世界时间）之间的差异 |
| **脚本命令** | |
| `load script` | 返回从文件中加载的脚本对象 |
| `run script` | 运行脚本或脚本文件 |
| `scripting components` | 返回所有脚本组件的列表 |
| `store script` | 将脚本对象存储到文件中 |

## 表 D-1：AppleScript 命令（续）

| 命令 | 描述 |
| --- | --- |
| **标准套件** | |
| `copy` | 将一个或多个值复制到变量 |
| `count` | 统计对象中元素的数量 |
| `get` | 返回脚本表达式或应用程序对象的值 |
| `launch` | 启动指定的应用程序而不发送其运行命令 |
| `run` | 启动应用程序、脚本或脚本对象 |
| `set` | 将一个或多个值分配给一个或多个脚本变量或应用程序对象 |
| **字符串命令** | |
| `localized string` | 返回指定键的本地化字符串 |
| `offset` | 在另一个文本内部查找一段文本 |
| `summarize` | 总结指定的文本或文本文件 |
| **用户交互命令** | |
| `beep` | 鸣叫一次或多次 |
| `choose application` | 允许用户选择应用程序 |
| `choose color` | 允许用户选择一种颜色 |
| `choose file` | 允许用户选择一个文件 |
| `choose file name` | 允许用户指定一个新的文件引用 |
| `choose folder` | 允许用户选择一个文件夹 |
| `choose from list` | 允许用户从列表中选择一个或多个项目 |
| `choose remote application` | 允许选择远程机器上运行的应用程序 |
| `choose URL` | 允许用户指定 URL |
| `delay` | 暂停一段时间 |
| `display alert` | 显示警告 |
| `display dialog` | 显示对话框，可选地请求用户输入 |
| `say` | 说出指定的文本 |

# 附录 E：Fink 软件包摘要

本附录提供了软件包的部分列表。

## 虚拟网络计算文件

如果你使用 `vncserver` 与网络上的其他计算机共享桌面，则指定 `vncserver` 行为的设置存储在你主目录下的 `vnc` 目录中。该目录包含在你启动 VNC 桌面时运行的应用程序。`vncpasswd` 文件存储了供 `vncserver` 使用的密码。

对于每个启动的显示器，都会创建一个名为 `host#.log` 的文件（其中 `host` 是主机名，`#` 是显示器编号）。每个显示器还有一个名为 `host#:pid` 的文件，其中包含与该显示器关联的 `Xvnc` 进程的进程 ID（PID）。

## X 启动文件

如果你使用 `startx` 命令启动桌面界面，可以使用 `.xinitrc` 文件来指定要启动哪种桌面环境。例如，将 `/usr/local/bin/gnome-session` 添加到 `.xinitrc` 以启动 GNOME 桌面环境。将 `/usr/local/bin/startkde` 添加到 `.xinitrc` 以启动 KDE 桌面环境。

## MMMS 配置文件

如果你使用 MMMS 音乐播放器，该播放器的配置文件包含在你主目录下的 `.xmms` 目录中。该目录的子目录包括 `Plugins`（存放音频插件）和 `Skins`（存放可供播放器使用的可用皮肤）。该目录中的 `config` 文件存储了 MMMS 的偏好设置。`xmms.m3u` 文件包含了播放器播放过的歌曲路径。

## 表 E-1：Fink Packages

| Package | Version | Description |
| --- | --- | --- |
| `grep` | 2.04-18 | Flexible egrep |
| `anachron` | 2.3-6 | Periodic scheduler |
| `analog` | 5.32-1 | Program to measure usage |
| `antiword` | 0.37-1 | convert MS-Word |
| `antlr` | 2.7.7-1001 | Language Recognition (for CTS) |
| `apache-pm588` | | [virtual package] |
| `apel` | 10.7-3 | Portable Emacs |
| `apg` | 0.98-12 | Automated password generator |
| `ca-roots` | 1.1-0 | List of SSL CA root certificates |
| `base-files` | 1.9.8 | Directory infrastructure |
| `bash` | 2.05-1 | The Bourne Again Shell |
| `bash-completion` | 2006031-3 | Command-line completions for bash |

## 表 E-1：Fink Packages（续）

| Package | Version | Description |
| --- | --- | --- |
| `bbkeys` | 0.8.4-1022 | Key-binding handler for Blackbox |
| `bbmail` | 0.8.3-1002 | E-mail watcher designed for use with Blackbox |
| `bbpager` | 0.3.1-1001 | Pager tool for the Blackbox window manager |
| `bcel` | 5.2-1 | Byte Code Engineering Library |
| `berkeleydb-pm586` | 0.31-1001 | Perl interface to Berkeley DB |
| `berkeleydb-pm588` | 0.31-1001 | Perl interface to Berkeley DB |
| `bidwatcher` | 1.37-1017 | GTK auction management/snipe tool for eBay |
| `bzip2` | 1.0.3-1 | Block-sorting file compressor |
| `bzip2-dev` | 1.0.3-1 | Developer files for bzip2 package |
| `bzip2-shlibs` | 1.0.3-1 | Shared libraries for bzip2 package |
| `c-scan-pm` | 0.74-3 | Perl module to scan C declarations for h2xs |
| `ca-roots` | | |
| `ccache` | 2.4-20 | C/C++ compiler cache |
| `ccache-default` | 2.4-20 | C/C++ compiler cache—as default compiler |
| `cctbx-10.5` | 71118-2 | Computational Crystallography Toolbox |
| `cmatrix` | 1.2a-1014 | Scrolling random text effect like The Matrix |
| `connect` | 1.96-1 | SSH proxy command |
| `contacts` | 1.1-1 | Little command-line OS X address book viewer |
| `context` | | [virtual package] |
| `control-center` | 2.12.3-2 | GNOME control center |

## 附录 E：Fink 包摘要

### 表 E-1：Fink 软件包（续）

| 软件包 | 版本 | 描述 |
| --- | --- | --- |
| `corkscrew` | 2.0-1 | 通过 HTTP 代理隧道传输 TCP 连接 |
| `crypt-blowfish-pm586` | 2.09-11 | Blowfish 算法的 XS 实现 |
| `crypt-blowfish-pm586` | 2.09-11 | `crypt-blowfish-pm` 的手动页 |
| `crypt-cbc-pm` | 2.12-1 | Perl 专用的 `Crypt::CBC` 密码块链接 (CBC) |
| `crypt-rc4-pm` | 2.02-1 | 实现 RC4 加密算法 |
| `curl-unified-dev` | 7.11.2-11 | 使用 URL 语法传输文件的库 |
| `curl-unified-shlibs` | 7.11.2-11 | 使用 URL 语法传输文件的库 |
| `curses-pm586` | 1.15-1101 | `ncurs` 库的 Perl 接口 |
| `curses-pm588` | 1.15-1101 | `ncurs` 库的 Perl 接口 |
| `curses-ui-pm586` | 0.95-1002 | 基于 `curses` 库的 UI 框架 |
| `curses-ui-pm588` | 0.95-1002 | 基于 `curses` 库的 UI 框架 |
| `cvs` | 1.12.13-12 | 版本控制系统 |
| `cvs-client` | | [虚拟包] |
| `cvs-proxy` | 1.11.22-2 | 版本控制系统 |
| `cvs-server` | | [虚拟包] |
| `cvs-stable` | 1.11.22-2 | 版本控制系统 |
| `cvs2cl` | 2.58-1 | CVS 消息到 ChangeLog 的转换 |
| `cvs2svn` | 1.5.1-1 | CVS 到 Subversion 仓库转换器 |
| `cvs2svn-py24` | 1.5.1-11 | `cvs2svn` 的 Python 模块 (Python 2.4) |
| `cvs2svn-py24-bin` | 1.5.1-11 | `cvs2svn` 的二进制文件 (Python 2.4) |
| `cvs2svn-py25` | 1.5.1-11 | `cvs2svn` 的 Python 模块 (Python 2.5) |
| `cvs2svn-py25-bin` | 1.5.1-11 | `cvs2svn` 的二进制文件 (Python 2.5) |
| `cvs2svn-ssl` | | [虚拟包] |

### 表 E-1：Fink 软件包（续）

| 软件包 | 版本 | 描述 |
| --- | --- | --- |
| `diffutils` | 2.8-1 | 比较文件的工具 |
| `emacs22` | 22.2-1002 | 灵活的实时文本编辑器 |
| `emacs22-carbon` | 22.1-3003 | 灵活的实时文本编辑器，Aqua 原生 |
| `emacs22-gtk` | 22.2-1002 | 灵活的实时文本编辑器 |
| `emacs22-nox` | 22.2-1002 | 灵活的实时文本编辑器 |
| `emacsen` | | [虚拟包] |
| `emacsen-common` | 0.14.15-5 | 所有 `emacsen` 的通用设施 |
| `fwipe` | 0.35-1 | 不可恢复地删除文件 |
| `gawk` | 3.1-51 | `Awk` 处理语言，GNU 版本 |
| `gc` | 7.0-1001 | 通用、垃圾回收的存储分配器 |
| `gc-shlibs` | 7.0-1001 | `gc` 包的共享库 |
| `gcalctool` | 5.8.25-1 | GNOME 计算器小组件 |
| `gcc2` | 2.95.2-0 | [代表 `gcc` 2.95.2 编译器的虚拟包] |
| `gcc2.95` | 2.95.2-0 | [代表 `gcc` 2.95.2 编译器的虚拟包] |
| `gcc3.1` | 3.1-0 | [代表 `gcc` 3.1 编译器的虚拟包] |
| `gcc3.3` | 3.3-0 | [代表 `gcc` 3.3 编译器的虚拟包] |
| `gcc4.0` | 4.0.1-5484 | [代表 `gcc` 4.0.1 编译器的虚拟包] |
| `gcc4.2` | 4.2.1-5564 | [代表 `gcc` 4.2.1 编译器的虚拟包] |
| `gcc42` | 4.2.2-1000 | GNU 编译器集版本 4.2 |
| `gcc42-shlibs` | 4.2.2-1000 | `gcc4` 的共享库 |
| `gconf` | 1.0.9-1052 | 配置数据库系统 |
| `gconf-dev` | 1.0.9-1052 | 配置数据库系统 |

### 表 E-1：Fink 软件包（续）

| 软件包 | 版本 | 描述 |
| --- | --- | --- |
| `gconf-editor` | 2.6.2-1019 | `GConf` 配置系统的编辑器 |
| `gconf-shlibs` | 1.0.9-1052 | 配置数据库系统 |



### 表 E-1：Fink 软件包

| 软件包 | 版本 | 描述 |
| --- | --- | --- |
| `gconf2` | 2.14.0-1 | GNOME 配置数据库系统 |
| `gconf2-dev` | 2.14.0-1 | GNOME 配置数据库系统 |
| `gconf2-shlibs` | 2.14.0-1 | GNOME 配置数据库系统 |
| `gd-pm586` | 2.16-2 | GD 图形库的 Perl 接口 |
| `gd-svg-pm586` | 0.27-1 | 从 gd 创建 svg 输出的 Perl 模块 |
| `gd2` | 2.00.33-3 | 图形生成库 |
| `gd2-bin` | 2.00.33-3 | gd2 包的可执行文件 |
| `gd2-shlibs` | 2.00.33-3 | gd2 包的共享库 |
| `ghostscript` | 8.54-3 | PostScript 和 PDF 的解释器 |
| `ghostscript-esp` | 7.07.1-35 | 增强型 GNU Ghostscript，具有更好的 CJK 和打印机支持 |
| `ghostscript-fonts` | 8.11-3 | Ghostscript 的标准字体 |
| `ghostscript-nox` | 7.04-3 | PostScript 和 PDF 的解释器 |
| `ghostscript6` | 6.01-4 | PostScript 和 PDF 的解释器，v6.01 |
| `ghostscript-nox` | 6.01-5 | PostScript 和 PDF 的解释器，v6.01，无 X11 支持 |
| `gif2png` | 2.4.6-2 | GIF 转 PNG |
| `giflib` | 4.1.4-2 | GIF 图像处理库 (LZW) |
| `giflib-bin` | 4.1.4-2 | GIF 图像格式库 (LZW) |
| `giflib-shlibs` | 4.1.4-2 | GIF 图像处理库 (LZW) |
| `gift-utils` | 1.0.0-1 | gIFT 工具 |
| `gimp` | 1.2.5-1007 | GNU 图像处理程序 |
| `gimp-default` | 1.2.5-1007 | GNU 图像处理程序 |
| `gimp-dev` | 1.2.5-1007 | GNU 图像处理程序 |

### 表 E-1：Fink 软件包（续）

| 软件包 | 版本 | 描述 |
| --- | --- | --- |
| `gimp-print-shlibs` | 4.2-1 | [Apple 安装 Gimp Print 的虚拟包] |
| `gimp-print7-shlibs` | 5.0.0-beta2-1 | [Apple 安装 Gimp Print 的虚拟包] |
| `gimp-shlibs` | 1.2.5-1007 | [Apple 安装 Gimp Print 的虚拟包] |
| `gimp` | 4.2-1 | [Apple 安装 Gimp Print 的虚拟包] |
| `gimp-` | 4.2-0 | [Apple 安装 Gimp Print 的虚拟包] |
| `gimp-dev` | 4.2-0 | [Apple 安装 Gimp Print 的虚拟包] |
| `gimp-shlibs` | 4.2-0 | [Apple 安装 Gimp Print 的虚拟包] |



### 表 E-1：Fink 软件包

| 软件包 | 版本 | 描述 |
| --- | --- | --- |
| `gimp-dev` | 4.2-0 | Apple 安装 Gimp Print 的虚拟包 |
| `gimp-shlibs` | 4.2-0 | Apple 安装 Gimp Print 的虚拟包 |
| `gimp` | 4.2-0 | Apple 安装 Gimp Print 的虚拟包 |
| `gimp-` | 4.2-0 | Apple 安装 Gimp Print 的虚拟包 |
| `gimp-print-shlibs` | 4.2-1 | Apple 安装 Gimp Print 的虚拟包 |
| `gimp-print7-shlibs` | 5.0.0-beta2-1 | Apple 安装 Gimp Print 的虚拟包 |
| `gimp-shlibs` | 1.2.5-1007 | Apple 安装 Gimp Print 的虚拟包 |
| `gimp` | 4.2-1 | Apple 安装 Gimp Print 的虚拟包 |



## 附录 E：Fink 软件包总结

### 表 E-1: Fink 软件包（续）

| 软件包 | 版本 | 说明 |
|---|---|---|
| `gimp-` | 4.2-0 | Apple 安装 Gimp Print 的虚拟包 |
| `gimp-dev` | 4.2-0 | Apple 安装 Gimp Print 的虚拟包 |
| `gimp-shlibs` | 4.2-0 | Apple 安装 Gimp Print 的虚拟包 |
| `gimp` | 4.2-0 | Apple 安装 Gimp Print 的虚拟包 |
| `hermes-shlibs` | 1.3.3-3 | 优化的像素格式转换库 |
| `hevea` | 1.08-1 | LaTeX--HTML 翻译器；使用 Objective Caml |
| `hexcurse` | 1.55-1012 | 基于终端的十六进制编辑器 |
| `hfsutils` | 3.2.6-12 | 读/写 Mac HFS 媒体 |
| `hlfl` | 0.60-0-1 | 高级防火墙语言 |
| `host` | 991529-1 | 增强的 DNS 和 ns/mx/rlookup 工具 |
| `hotbabe` | 0.2.2-1002 | 显示系统活动 |
| `html2text` | 1.3.2a-1022 | 高级 HTML 转文本转换器 |
| `hugs` | 1998.200102-1017 | Haskell 解释器 |
| `hyperref` | | [虚拟软件包] |
| `i18n-langtags-pm586` | | [虚拟软件包] |
| `i18n-langtags-pm588` | | [虚拟软件包] |
| `imagagick` | 6.2.8-1003 | 图像处理工具 |
| `imagagick-dev` | 6.1.8-1007 | 图像处理工具 |
| `imagagick-nox` | 6.2.8-1003 | 图像处理工具 |
| `imagagick-nox-dev` | 6.1.8-1007 | 图像处理工具 |
| `imagagick-nox-shlibs` | 6.1.8-1007 | 图像处理工具 |
| `imagagick-nox10-dev` | 6.2.8-1003 | 图像处理工具 |
| `imagagick-nox10-shlibs` | 6.2.8-1003 | 图像处理工具 |
| `imagagick-shlibs` | 6.1.8-1007 | 图像处理工具 |
| `imagagick10-dev` | 6.2.8-1003 | 图像处理工具 |
| `imagagick10-shlibs` | 6.2.8-1003 | 图像处理工具 |
| `imagap-client` | | [虚拟软件包] |
| `imlib` | 1.9.14-15 | 用于 X11 和 Gtk 的图像处理库 |
| `imlib-shlibs` | 1.19.14-15 | 用于 X11 和 Gtk 的图像处理库 |
| `imlib2` | 1.2.1-1022 | 用于 X11 的图像处理库 |
| `imlib2-rb18` | 0.5.2-2 | imlib2 的 Ruby 封装 |
| `imlib2-shlibs` | 1.2.1-1022 | 用于 X11 的图像处理库 |
| `less` | 394-1001 | 功能完备的分页器 |
| `lesspipe` | 1.53-11 | less 的预处理器 |
| `lestif` | 1:0.93.18-1 | OSF/Motif 的免费实现 |
| `lestif-bin` | 1:0.93.18-1 | OSF/Motif 的免费实现 |
| `lestif-shlibs` | 1:0.93.18-1 | OSF/Motif 的免费实现 |
| `lftp` | 3.1.0-1010 | 复杂的基于命令行 FTP 客户端 |
| `lha` | 1.14i-ac20050924p1-2 | 用于创建和打开 lzh 归的实用 |
| `libxml` | 1.8.17-14 | XML 解析库 |
| `libxml-pm586` | 0.07-13 | 在 Perl 中处理 XML 的 Perl 模块 |
| `libxml-shlibs` | 1.8.17-14 | XML 解析库 |
| `libxml2` | 2.6.27-1001 | XML 解析库，版本 2 |
| `libxml2-bin` | 2.6.27-1001 | XML 解析库，版本 2 |
| `libxml2-py24` | 2.6.27-1002 | libxml2 库的 Python 绑定 |
| `libxml2-py25` | 2.6.27-1002 | libxml2 库的 Python 绑定 |
| `libxml2-shlibs` | 2.6.27-1001 | XML 解析库，版本 2 |
| `libxslt` | 1.1.15-3 | XML 样式表转换库 |
| `libxslt-bin` | 1.1.15-3 | XML 样式表转换工具 (xsltproc) |
| `libxslt-shlibs` | 1.1.15-3 | XML 样式表转换共享库 |
| `libzvt2` | 2.0.1-1014 | Zed 的虚拟终端 |
| `libzvt2-dev` | 2.0.1-1014 | Zed 的虚拟终端 |
| `libzvt2-shlibs` | 2.0.1-1014 | Zed 的虚拟终端 |
| `lightlab` | 0.3-1014 | 实验 OpenGL 光照演示程序 |
| `lilypond` | 2.10.33-1004 | GNU 音乐排版系统 |
| `lv` | 4.51-1003 | 强大的多语言文件查看器/Grep |
| `lynx` | 2.8.5-3 | 基于控制台的浏览器 |
| `lynx-ssl` | 2.8.5-3 | 带有 openssl 的 lynx 升级包 |
| `lzo` | 1.08-1 | 实时数据压缩库 |
| `lzo-shlibs` | 1.08-1 | 实时数据压缩库 |
| `mtr` | 0.54-22 | 结合了 traceroute 和 ping |



## 附录 E：Fink 软件包总结

### 表 E-1: Fink 软件包（续）

| 软件包 | 版本 | 说明 |
|---|---|---|
| hermes-shlibs | 1.3.3-3 | 优化的像素格式转换库 |
| hevea | 1.08-1 | LaTeX--HTML 翻译器；使用 Objective Caml |
| hexcurse | 1.55-1012 | 基于终端的十六进制编辑器 |
| hfsutils | 3.2.6-12 | 读/写 Mac HFS 媒体 |
| hlfl | 0.60-0-1 | 高级防火墙语言 |
| host | 991529-1 | 增强的 DNS 和 ns/mx/rlookup 工具 |
| hotbabe | 0.2.2-1002 | 显示系统活动 |
| html2text | 1.3.2a-1022 | 高级 HTML 转文本转换器 |
| hugs | 1998.200102-1017 | Haskell 解释器 |
| hyperref | | [虚拟软件包] |
| i18n-langtags-pm586 | | [虚拟软件包] |
| i18n-langtags-pm588 | | [虚拟软件包] |
| imagagick | 6.2.8-1003 | 图像处理工具 |
| imagagick-dev | 6.1.8-1007 | 图像处理工具 |
| imagagick-nox | 6.2.8-1003 | 图像处理工具 |
| imagagick-nox-dev | 6.1.8-1007 | 图像处理工具 |
| imagagick-nox-shlibs | 6.1.8-1007 | 图像处理工具 |
| imagagick-nox10-dev | 6.2.8-1003 | 图像处理工具 |
| imagagick-nox10-shlibs | 6.2.8-1003 | 图像处理工具 |
| imagagick-shlibs | 6.1.8-1007 | 图像处理工具 |
| imagagick10-dev | 6.2.8-1003 | 图像处理工具 |
| imagagick10-shlibs | 6.2.8-1003 | 图像处理工具 |
| imagap-client | | [虚拟软件包] |

| 软件包 | 版本 | 说明 |
|---|---|---|
| imlib | 1.9.14-15 | 用于 X11 和 Gtk 的图像处理库 |
| imlib-shlibs | 1.19.14-15 | 用于 X11 和 Gtk 的图像处理库 |
| imlib2 | 1.2.1-1022 | 用于 X11 的图像处理库 |
| imlib2-rb18 | 0.5.2-2 | imlib2 的 Ruby 封装 |
| imlib2-shlibs | 1.2.1-1022 | 用于 X11 的图像处理库 |
| less | 394-1001 | 功能完备的分页器 |
| lesspipe | 1.53-11 | less 的预处理器 |
| lestif | 1:0.93.18-1 | OSF/Motif 的免费实现 |
| lestif-bin | 1:0.93.18-1 | OSF/Motif 的免费实现 |
| lestif-shlibs | 1:0.93.18-1 | OSF/Motif 的免费实现 |
| lftp | 3.1.0-1010 | 复杂的基于命令行 FTP 客户端 |
| lha | 1.14i-ac20050924p1-2 | 用于创建和打开 lzh 归的实用工具 |
| libxml | 1.8.17-14 | XML 解析库 |
| libxml-pm586 | 0.07-13 | 在 Perl 中处理 XML 的 Perl 模块 |
| libxml-shlibs | 1.8.17-14 | XML 解析库 |
| libxml2 | 2.6.27-1001 | XML 解析库，版本 2 |
| libxml2-bin | 2.6.27-1001 | XML 解析库，版本 2 |
| libxml2-py24 | 2.6.27-1002 | libxml2 库的 Python 绑定 |
| libxml2-py25 | 2.6.27-1002 | libxml2 库的 Python 绑定 |
| libxml2-shlibs | 2.6.27-1001 | XML 解析库，版本 2 |
| libxslt | 1.1.15-3 | XML 样式表转换库 |
| libxslt-bin | 1.1.15-3 | XML 样式表转换工具 (xsltproc) |
| libxslt-shlibs | 1.1.15-3 | XML 样式表转换共享库 |
| libzvt2 | 2.0.1-1014 | Zed 的虚拟终端 |

| 软件包 | 版本 | 说明 |
|---|---|---|
| libzvt2-dev | 2.0.1-1014 | Zed 的虚拟终端 |
| libzvt2-shlibs | 2.0.1-1014 | Zed 的虚拟终端 |
| lightlab | 0.3-1014 | 实验 OpenGL 光照演示程序 |
| lilypond | 2.10.33-1004 | GNU 音乐排版系统 |
| lv | 4.51-1003 | 强大的多语言文件查看器/Grep |
| lynx | 2.8.5-3 | 基于控制台的浏览器 |
| lynx-ssl | 2.8.5-3 | 带有 openssl 的 lynx 升级包 |
| lzo | 1.08-1 | 实时数据压缩库 |
| lzo-shlibs | 1.08-1 | 实时数据压缩库 |
| mtr | 0.54-22 | 结合了 traceroute 和 ping |
| mule-ucs | 0.85+0.20061127-3 | Mule 通用编码系统 |
| multi-rehash | 1.1-2 | 哈希表的替换品 |
| multitail | 3.0.6 | 一次性查看多个文件的 tail |
| mutt | 1.3.15-1 | 邮件客户端 |
| mysql | 5.0.27-1001 | MySQL 数据库 |
| mysql-client | 5.0.27-1001 | MySQL 客户端 |
| mysql-dev | 3.23.58-1023 | MySQL 开发工具 |
| mysql-shlibs | 3.23.58-1023 | MySQL 共享库 |
| mysql12-dev | 4.0.22-1012 | MySQL 开发工具 |
| mysql12-shlibs | 4.0.22-1012 | MySQL 共享库 |
| mysql14-dev | 4.1.10-1002 | MySQL 开发工具 |
| mysql14-shlibs | 4.1.10-1002 | MySQL 共享库 |

| 软件包 | 版本 | 说明 |
|---|---|---|
| nano | 2.4-6 | 文本编辑器 |
| nano-bin | 2.4-6 | 文本编辑器 |
| nano-shlibs | 2.4-6 | 文本编辑器 |
| nano2 | 2.9.4-2 | 文本编辑器 |
| nap | | [虚拟软件包] |
| ncurses | 5:6.1.18-1 | 字体 |
| neat | | [虚拟软件包] |
| net | | [虚拟软件包] |
| net-base | | [虚拟软件包] |
| net-tools | | [虚拟软件包] |
| net-utils | | [虚拟软件包] |
| network | | [虚拟软件包] |
| ncurses-dev | 5:6.1.18-1 | 字体 |
| ncurses-bin | 5:6.1.18-1 | 字体 |
| ncurses-shlibs | 5:6.1.18-1 | 字体 |
| ncurses2 | 2.9.4-2 | 字体 |
| new | | [虚拟软件包] |
| new-base | | [虚拟软件包] |
| new-tools | | [虚拟软件包] |
| new-utils | | [虚拟软件包] |
| new | | [虚拟软件包] |
| news | | [虚拟软件包] |
| nil | | [虚拟软件包] |
| nis | | [虚拟软件包] |
| nit | 2.0.1 | 文本编辑器 |

| 软件包 | 版本 | 说明 |
|---|---|---|
| node | 2.4.8-1 | Python 2.4 |
| python | 2.4.8-1 | Python 2.4 |
| python-dev | 2.4.8-1 | Python 2.4 |
| python-shlibs | 2.4.8-1 | Python 2.4 |
| nix | 2.1.0-103 | nix |
| nix-dev | 2.1.0-103 | nix |
| nix-shlibs | 2.1.0-103 | nix |
| no2 | | [虚拟软件包] |
| no2-base | | [虚拟软件包] |
| no2-tools | | [虚拟软件包] |
| no2-utils | | [虚拟软件包] |
| no2 | | [虚拟软件包] |
| news | | [虚拟软件包] |
| nil | | [虚拟软件包] |
| nis | | [虚拟软件包] |
| nit | 2.0.1 | 文本编辑器 |

## 附录 E: Fink 软件包摘要

### 表 E-1: Fink 软件包（续）

| 软件包 | 版本 | 描述 |
|---|---|---|
| procmail | 3.22-1 | 邮件处理程序 |
| progressbar-rb | 0.9-1 | Ruby 文本进度条库 |
| proj | 4.5-0 | 地图投影库 |
| proj-shlibs | 4.5-0 | 地图投影库 |
| prosper | 1.5-1 | 用于编写幻灯片的 LaTeX 类 |
| ps2eps | 1.58-1 | 将 PostScript 转换为 EPS 文件 |
| psmulti-dna | 1.1.2-1 | 多功能 postscript 过滤器 |
| pstree | 2.17-1 | 以树形形式显示 ps 列表 |
| psutils | 1.17-2 | 处理 postscript 文件的实用工具，“信纸”尺寸 |
| psutils-a4 | 1.17-2 | 处理 postscript 文件的有用工具，A4 纸 |
| psync | 0.69-2 | 用于操作 Mac OS 文件的 Perl 脚本集 |
| ptex | 3.1.10-1001 | 用于 ASCII 发布 TeX 的捆绑包 |
| ptex-babel | 20060322-3 | pTeX 中 Babel 宏的正确连字符处理 |
| ptex-base | 3.1.10-1001 | ASCII 发布 TeX |
| ptex-jsfonts | | [虚拟软件包] |
| ptex-nox | 3.1.10-1001 | 用于 ASCII 发布 TeX 的捆绑包 |
| ptex-nox-base | 3.1.10-1001 | ASCII 发布 TeX |
| ptexmf | 2.4-57 | pTeX 额外的 texmf |
| ptex3-base | | [虚拟软件包] |
| ptexenc | 0.96-1 | pTeX 的汉字代码转换库 |



| Package | Version | Description |
| :--- | :--- | :--- |
| `ptexenc-shlibs` | `0.96-1` | pTeX 汉字代码转换库的共享库 |
| `pth` | `1.4.0-7` | 提供调度的可迁移库 |
| `pth-shlibs` | `1.4.0-7` | 提供调度的可迁移库 |
| `publib` | `0.34-1` | C 函数库 |
| `pwgen` | `2.05-1` | 简单密码生成器 |
| `pychecker-py24` | `0.8.14-4` | 检查 Python 程序的错误（模块） |
| `pychecker-py24-bin` | `0.8.14-4` | 检查 Python 程序的错误（主二进制文件） |
| `pydns-py25` | `2.3.0-6` | 执行 DNS 查询的 Python 模块 |
| `pyserial-py24` | `2.0-12` | Python 访问串口 |
| `pyserial-py25` | `2.0-12` | Python 访问串口 |
| `python` | `1:2.5.1-1` | 解释型、面向对象的语言 |
| `python-mx-py24` | `2.0.6-1002` | 来自 GGenix 的 Python 扩展 |
| `python-mx-py25` | `2.0.6-1002` | 来自 GGenix 的 Python 扩展 |
| `python24` | `1:2.4.3-1002` | 解释型、面向对象的语言 |
| `python24-shlibs` | `1:2.4.3-1002` | 解释型、面向对象的语言 |
| `python24-socket` | `1:2.4.3-1002` | Python 的 Socket 插件 |
| `python24-socket-ssl` | `2.4.2-1101` | Python 的 Socket 插件（SSL 版本） |
| `python25` | `1:2.5.1-1` | 解释型、面向对象的语言 |
| `python25-shlibs` | `1:2.5.1-1` | 解释型、面向对象的语言 |
| `python25-socket` | `1:2.5.1-1` | Python 的 Socket 插件 |
| `pyvtk-py24` | `0.46-37` | Python 中处理 VTK 文件的工具 |
| `qca` | `1.0-1023` | Qt 密码学架构 |
| `qca-shlibs` | `1.0-1023` | Qt 密码学架构 |
| `qhull` | `2002.1-10` | 计算凸包及结构 |
| `qt3` | `3.3.8-1026` | 跨平台 GUI 应用框架 |
| `qt3-bin` | | [虚拟软件包] |
| `qt3-designer` | `3.3.8-1026` | 跨平台 GUI 应用框架 |
| `qt3-designer-shlibs` | `3.3.8-1026` | 跨平台 GUI 应用框架 |
| `qt3-doc` | `3.3.8-1026` | 跨平台 GUI 应用框架 |
| `qt3-linguist` | `3.3.8-1026` | 跨平台 GUI 应用框架 |
| `qt3-shlibs` | `3.3.8-1026` | 跨平台 GUI 应用框架 |
| `qt3-mac` | `3.3.8-1026` | QT3 的 Aqua 版本：头文件和开发工具 |
| `qt3-mac-apps` | `3.3.8-12` | QT3 的 Aqua 版本：应用程序和插件 |
| `qt3-mac-doc` | `3.3.8-12` | QT3 的 Aqua 版本：文档 |
| `qt3-mac-shlibs` | `3.3.8-12` | QT3 的 Aqua 版本：共享库 |
| `quanta` | `3.5.8-1021` | KDE-HTML 编辑器 |
| `qucs` | `0.13-1001` | 基于 Qt 的集成电路模拟器 |
| `quit` | `1.2a-1` | 带有 "sl" 的自行车 |
| `ren` | `1.0` | 重命名多个文件 |
| `rep-gtk` | `0.15-1025` | librep 的 Gtk+ 和 GNOME 绑定 |
| `revtex` | | [虚拟软件包] |
| `riece` | `4.0.0-3` | Emacs 的 IRC 客户端 |
| `rlwrap` | `0.28-2` | 任何命令的键盘输入 |
| `rman` | `3.1-1` | UNIX 手页的通用过滤器 |
| `robodoc` | `4.99.26` | 文档提取工具 |
| `root-pythia` | `6.4-52` | Pythia 接口库 (ROOT) |
| `root-pythia-shlibs` | `6.4-52` | Pythia 接口库 (ROOT) |
| `rsync` | `2.6.9-1` | 同步主机系统 |
| `rtf2latex` | `1.0fc2-1` | 将 RTF 文件转换为 LaTeX 文件 |
| `ruby` | `1.8.1-2` | 链接到 Ruby.8 |
| `ruby18` | `1.8.1-2` | 解释型、面向对象的语言 |
| `ruby18-dev` | `1.8.1-2` | Ruby 静态库 |
| `ruby18-shlibs` | `1.8.1-2` | Ruby 共享库 |
| `rxvt` | `2.7.10-3` | 用于 X11 的仿真器 |
| `rxvt-ml` | `2.7.10-2` | 更新到 rxvt 的（废弃） |
| `sam` | `4.3-1002` | 不传统但强大的 X11 编辑器 |
| `sed` | `4.1.5-11` | GNU 版本流编辑器 |
| `sitecopy` | `0.16.3-4` | 网站上传器 |
| `sitecopy-ssl` | `0.16.3-4` | 统一 site-copy 的软件包（废弃） |
| `sjeng` | `1.16.3-4` | ... 的占位符 |
| `skk` | | [虚拟软件包] |
| `skk-dict` | `1.4-11` | SKK 字典 |
| `skycal` | `1.0-1` | ... 的年鉴 |
| `sqlite` | `2.8.5-1014` | 嵌入式数据库 |
| `sqlite-dev` | `2.8.5-1014` | 嵌入式数据库 |
| `sqlite-shlibs` | `2.8.5-1014` | 嵌入式数据库 |
| `sqlite3` | `3.2.8-1001` | 嵌入式数据库 |
| `sqlite3-dev` | `3.2.8-1001` | 嵌入式数据库 |
| `sqlite3-shlibs` | `3.2.8-1001` | 嵌入式数据库 |
| `svn` | `1.4-11` | svn 版本 |
| `svn-client` | `1.4-11` | svn 版本 |
| `svn-dev` | `1.4-11` | svn 版本 |
| `svn-shlibs` | `1.4-11` | svn 版本 |
| `tcsh` | `6.15-0` | C Shell |
| `tcltk` | `8.4.13-3` | 工具语言和 Tk |
| `tcltk-dev` | `8.4.13-3` | 工具语言和 Tk |
| `tcltk-shlibs` | `8.4.13-3` | 工具语言和 Tk |
| `tar` | `1.15-1023` | GNU tar |
| `unzip` | `2.4.6-2` | 批量转换整个网页 |
| `wmweather` | `1.31-2` | 使用 METAR 的本地天气应用 |
| `wget` | `1.10-15` | 自动网站检索器 |
| `wget-ssl` | `1.10.2-1` | 统一 wget 的（废弃） |
| `wtf` | `1.7-3` | 常见互联网缩写翻译 |
| `wv2` | `0.2.2-1036` | MSWord 解析库 |
| `wv2-shlibs` | `0.2.2-1036` | MSWord 解析库的共享库 |
| `x-ghostscript-fonts` | `2002206-3` | 允许在 X-Window 系统中使用 Ghostscript |
| `x11` | | [虚拟软件包] |
| `x11-dev` | | [虚拟软件包] |
| `x11-shlibs` | | [虚拟软件包] |
| `yatex` | `1.73-4` | Emacs 的另一种 TeX 模式 |
| `yc` | `4.0.13-8` | Emacs 的另一个 Canna 客户端 |
| `yorick` | `1.6.02-2` | 解释型语言和科学图形 |
| `yorick-doc` | `1.6-1` | Yorick 文档 |
| `ytalk` | `3.1.1-1022` | 增强型对话程序 |
| `ytalk-nox` | `3.1.1-1022` | 增强型对话程序 |
| `yydecode` | `0.2.9-1` | USET 上 yEnc 编码二进制文件的解码器 |
| `zenity` | `2.6.2-1010` | 脚本 GTK+2 对话框 |
| `zip` | `2.31-11` | 压缩工具 |
| `zip-ssl` | `2.31-11` | 带加密的压缩工具 |
| `zsh` | `4.2.6-1001` | Z Shell |
| `ztools` | `981107-1` | Z-Machine 工具集 |
| `ztrack` | `1.0-1` | 基于 Curses 的伪 3D 驾驶游戏 |

# 附录 F：Perl 入门

本附录提供了一个简明易懂的 Perl 入门指南。我将使用我的 Perl 脚本作为示例和起点来讨论这门语言。

## 介绍 Perl

Perl 由 Larry Wall 在 20 世纪 80 年代后期发明。他需要一种比 shell 脚本更强大，但又比 C 等结构化程度更高的语言更正式的语言。

因此，Perl 诞生了。这是一门让你或爱或恨的语言——我很少发现有人处于中立状态。无论你对它有什么感觉，它都是一种极其实用的胶水语言，被全球的系统管理员广泛使用。

你的 Mac OS X 系统应该已经了最新版本的 Perl——验证非常简单，只需使用以下命令行即可：

```perl
perl -v
This is, v5.8.8 built for darwin-thread-multi-2level
(with 1 registered patch, see perl -V for more detail)
```

版权所有 1987-2006, Larry Wall

Perl 仅可以在艺术许可协议（Artistic License）或 GNU 通用公共许可证（GNU General Public License）的条款下复制，这些协议可以在 Perl 5 源码包中找到。

Perl 的完整文档（包括常见问题列表 FAQ）可以在系统中通过 `man perl` 或 `perldoc perl` 找到。如果你可以使用互联网，可以将浏览器指向 `http://www.perl.org/`，这是 Perl 主页。

如果你没有收到此响应，或者你使用的是非常旧版本的 Perl（例如 Perl 4），请使用 Fink 来更新你的代码。不过，很有可能你已经拥有了所需的所有内容。

让 Perl 如此易用的原因之一，恰恰也是让该语言的初学者感到沮丧的原因。Perl 具有某种我称之为“惯用性弹性”（idiomatic elasticity）的东西。这只是华丽的语言术语，指的是可以使用不同的语法结构和命令来完成相同的事情。

尽管许多程序员发现这令人恼火，但对我来说这完全合逻辑——我在语言学方面接受过很多训练，Larry Wall 也是。例如，如果我坐在餐厅里想结账离开，我有许多不同的方式来表达这一点。我可以招招手服务员，当他问我是否需要账单时，我可以直接问：“可以给我账单吗？”我也可以掏出钱包并放在桌子上。

这些不同的方法都带给我相同的结果——服务员的注意，以及最终我手里拿到的一份纸质账单。

Perl 的情况也是如此。在许多情况下，它支持多种不同的方法来完成任何工作——正如 Larry Wall 所说，“切皮肤的方法不止一种（There's more than one way to cut a skin）。”是的，这确实是一个陈词调，但 Perl 让这个陈词调变成了现实可能——这就是它的力量所在。这就是为什么当你把五个或更多 Perl 程序员聚在一个房间里并让他们解决一个问题时，你会得到至少三个不同的解决方案。

在本附录中，我将向你展示如何使用 Perl 处理一个常见问题（检查网站上的链接），以自动化解决该问题的繁琐且易出错的人工流程。

如果你已经是一个 Perl 大神了，你可以对自己的知识和掌握程度充满信心并跳过此部分。如果你是一个完全的新手，希望下一节能带你走上通往精通之路。

## 检查网站链接

大约六七年前，一个客户问我是否知道一种可以帮助快速检查网页链接的工具。当时已经有很多链接检查器（包括免费和付费）可用，但我利用这个机会写了一个只有 20 行的快速 Perl 脚本来完成检查。

我需要一个小型且便携的脚本，它能接受 URL 作为命令行参数，访问该 URL，检查它发现的所有链接，然后报告它们是否可以访问。

根据经验，我知道一些帮助来完成这项任务。Perl 提供了许多手手的库，每个都是完成特定工作的工具包。

在我的情况下，我需要一个可以访问 URL 的简单代理。对于这一点，我会使用 `LWP::Simple` 包。我还需要一种快速从 HTML 文档中提取链接的方法。对于这一点，可以使用 `HTML::LinkExtor` 包。

在过去，我会尝试构建自己的用户代理和提取器，但幸运的是，年龄带来了智慧（以及对高效完成工作的渴望）。简单的解决方案：看看是否有人写了模块或包。

现在，让我们开始看脚本。

### 整个脚本

让我们看看整个脚本，这样你就知道我们要面对什么。正如你看到的，它只有 20 行左右（不包括注释），所以并不难。在我们离开这一节并深入细节之前，我将向你展示一些在几乎任何 Perl 脚本中都能看到的东西。

这是脚本：

```perl
#!/usr/bin/perl -w
# curl.pl - check urls

use HTML::LinkExtor;
use LWP::Simple qw(get head);

my $url = $ARGV[0] or die "usage: $0 <url>\n";
my $parser = HTML::LinkExtor->new;
my @links = $parser->parse($url);

foreach my $link (@links) {
    my $type = $link;
    if ($type =~ /\b(https?|file)\b/) {
        if (get($link)) {
            print "$link: OK\n";
        } else {
            print "$link: BAD\n";
        }
    }
}
```

*(注：原文中的脚本文本高度碎片化/损坏；我根据周围上下文和常见的 Perl 模式重构了一个具有功能性的表示。)*

编写一个链接提取器和一个轻量级用户代理程序至少需要编写几百行代码，但现在我们不需要了。

### 针对目标 URL 并提取链接

现在是时候真正访问一个 URL 并提取链接了。在 Perl 中，与其他面向命令行的语言一样，你可以非常容易地向脚本传递参数。所有的命令行参数都存储在一个名为 `@ARGV` 的特殊数组中。要获取第一个参数，通常会使用 `shift` 命令，如下所示：

```perl
$argument = shift @ARGV;
```

然而，当 `shift` 命令没有接收参数时，它始终指向 `@ARGV` 数组，因此你可以这样简化：

```perl
$argument = shift;
```

但是，对于我们的目的来说，我们需要确定 `shift` 操作是否真的生效。如果是，设置一个名为 `$base_url` 的变量。如果不是，脚本需要并并一个特定的错误信息，告诉用户正确的用法。

以下是更改：

```perl
$base_url = shift or die "usage: $0 <start_url>\n";
```

注意 `shift or die` 语法的用法。这就是惯用式灵活性发挥的地方。C 和 Java 程序员可能更倾向于看到以下代码：

```perl
$base_url = shift;
if (length($base_url) == 0){
  die "usage: $0 <start_url>\n";
}
```

请记住，如果你喜欢的话可以那样做，但原始语法要简洁得多！

一旦你有了了可以使用的基础 URL，你就可以通过传递 `$base_url` 变量来调用 `HTML::LinkExtractor` 解析器，结果所有的链接都存储在一个名为 `@links` 的数组中（感谢下方的 `$Parser->links`）。

你可以将基础 URL 作为输出的标题打印出来：

```perl
$parser = HTML::LinkExtractor->new(undef, $base_url);
$parser->parse(get($base_url));
@links = $parser->links;
print "$base_url: \n";
```

仅需四行，我们就捕获了目标 URL 上的每一个链接。它们不再散落在 HTML 文档中，或存在于某些捕获的文本流中，而是安全地封装在一个数组中，我们可以毫不费力地处理它们。

### 处理 @links 数组

现在我们有了一个链接数组，可以对它们做一些用的事情。最好的方法是使用 `foreach` 循环；这样，我们可以遍历整个数组，直到到达结尾（意味着没有更多链接需要处理了！）

以下是代码，随后是逐行解释：



```
foreach $linkarray (@links) {
    my @element = $linkarray;
    my $elt_type = shift @element;
    while (@element) {
        my ($attr_name, $attr_value) = splice(@element, 0, 2);
        if ($attr_value->scheme =~ /\b(ftp|https?|file)\b/) {
            print "$attr_value: ", head($attr_value) ? "OK" : "BAD", "\n";
        }
    }
}
```

注意当我们使用 `foreach` 时，使用的是以下语法：

```
foreach $linkarray (@links) {
```

这样，每次循环时，`@links` 数组中的下一个值就会被赋值给 `$linkarray` 值。我们本可以使用以下写法：

```
foreach (@links) {
```

这样，每次循环时，数组中的下一个值都会被赋值给特殊变量 `$_`。这种方法完全没有问题——很多 Perl 脚本都使用这个变量——但在试图弄清楚 `$_` 被设置为什么时候可能会有点困惑，尤其是当你的脚本变得复杂时。显式地设置你的变量是一个好主意。

一旦进入循环，我们就可以开始执行核心工作。注意在接下来的两行中，我们使用 `my` 运算符创建了两个私有变量：

```
my @element = $linkarray;
my $elt_type = shift @element;
```

在第一情况下，我们创建了一个私有数组 `@element`。这个数组包含了 `$linkarray` 的值（强制转换为数组上下文）。换句话说，当我们遍历 `@links` 数组时，每个值都会被转换为数组上下文。这是因为每个链接都是系列匿名数组（链接类型、链接标签本身，后面跟着一个或多个属性，等等）。

在第二种情况下，我们再次使用 `my` 运算符为从新创建的 `@element` 中 `shift` 出来的内容创建一个私有变量。第一个变量将总是元素类型，这就是为什么它被称为 `$elt_type`。

我们为什么要费力去获取它？很简单。我们把它移开，`shift` 就会很好地从数组中切掉它，只留下我们关心的内容。

现在这一轮我们有一个 `@element` 数组，可以使用 `while` 块处理内部的每个匿名数组。在随后的代码中，我们首先使用 `splice` 从 `@element` 中提取出一个属性名和值。然后，如果我们捕获到了匹配 ftp、http、https 或 file 的协议，我们就使用 `LWP::Simple` 中的 `head()` 函数尝试访问链接地址。如果无法访问，

```
while (@element) {
    my ($attr_name, $attr_value) = splice(@element, 0, 2);
    if ($attr_value->scheme =~ /\b(ftp|https?|file)\b/) {
        print " $attr_value: ", head($attr_value) ? "OK" : "BAD", "\n";
    }
}
```

如你所见，Perl 的语法压缩允许你在短短几行代码内完成惊人的工作。有些人欣赏这一点，但另一些人并不在乎。这取决于你的立场——取决于你的方法，编写这个脚本用 100 行或更多行同样容易。

## 运行脚本

一旦写好脚本，将其保存到文件系统的某个处并命名为 `curl.pl`（代表 "check url"），然后使用 `chmod +x curl.pl` 赋予可执行权限。

接下来，从命令行运行它，并提供一个起始 URL：

```
perl ./curl.pl http://www.apple.com
http://www.apple.com:
http://www.apple.com/ - OK
http://www.apple.com/sitemap/: - OK
http://images.apple.com/main/rss/hotnews/hotnews.rss - OK
http://images.apple.com/global/scripts/lib/prototype.js: OK
http://images.apple.com/global/scripts/lib/scriptaculous.js: OK
http://images.apple.com/global/scripts/browserdetect.js: OK
http://images.apple.com/global/scripts/apple_core.js: OK
http://images.apple.com/global/scripts/search_decorator.js: OK
http://images.apple.com/home/scripts/ticker.js: OK
http://www.apple.com/global/styles/base.css: OK
http://www.apple.com/home/styles/home.css: OK
http://images.apple.com/global/nav/scripts/shortcuts.js: OK
```

## 扩展脚本

作为最后的告别，我将提出两个挑战供你自行探索。第一个挑战并不是真正的挑战，很简单。第二个稍微难一点。

按照 Perl 的风格，这两个挑战中的任何一个都可以任何方式回答。

- 第一个挑战并不是真正的挑战，很简单。如果你想将输出重定向到文件？
- 第二个挑战稍微难一点，需要更多时间。你想如何重写脚本以处理多个域名？

如果你想将输出重定向到文件？或者你想如何重写脚本以处理多个域名？只需发送邮件到 `tom@tripledogs.com` 即可。

祝编程愉快，感谢阅读本书！

## 索引

### 符号

- `B-树索引`
    - 基于...的操作系统, 3
    - 安全问题, 17–178
    - 文本编辑器, 63
    - Unix 文件系统 (UFS), 101
    - 版本 2–3
    - 文件夹, 16
    - 刻录光盘: DVD, 110–111
    - 类型, 文件, 打印数量, 71
    - `blzip` 命令, 压缩, 105–106

### C

- `C++`, `Fink` 软件包, 用于 225
- `cal` 命令, 日历, 显示, 138
- `Carbon`, 45
- `case` 命令, case, 39–40
- 大写敏感性
- 大写, 测试, 39–40
- 文件系统, 大写, 神经
- `find` 命令, 57
- 搜索, 忽略, 0
- `case` 语句, 81–83
- 功能, 81
- 在 shell 中, 81–83
- `cat` 命令
    - ASCII, 177
    - 空文件, 创建, 44
    - 文本, 替换, 72
    - 文本文件, 列出, 67
- CD(s)
    - 备份到, 110–111
    - ISO 镜像, 复制, 55
- `cd` 命令, 更改, 43, 51
- 通道, 房间, 172
- 字符, 替换, 73
- 字符设备, 46
- chat. 参见 Internet Relay Chat (IRC), 187
- 文件校验和, 验证, 60–61
- `chgrp` 命令, 目录所有权, 51
- `chmod` 命令权限, 允许, 48–50
- shell 脚本, 可执行, 36
- `chown` 命令, 目录所有权, 51
- URL 客户端 (URL), 参见 `curl` 命令
- 剪贴板, `AppleScript` 命令, 215
- `COBRA OR`, `Fink` 软件包, 230–231
- `Cocoa`, 111
- 颜色, 搜索词, 着色, 70

### 环境变量

- `COLUMNS` (列), 209
- 分隔符, 75
- 打印, 字段范围, 操作, 76
- 运行进程列表, 118–120
- 文本, 提取, 75

### 命令

- `bash` 操作, 29–30
- 可执行文件, 44
- 查找. 参见命令参考
- 帮助信息, 显示, 用于, 67
- `info` 文档, 9
- 调度运行, 129–131
- 搜索, 123
- 标准输入, 重定向到, 32
- 参见各个命令
- 命令文件, 43
- 备份正在执行的进程, 32
- 使用 CD/DVD 备份, 111
- 使用...完成, 30
- 打开应用程序, 87–89
- 从...搜索, 19–20
- 情况, 4–5, 6
- 终端和访问工具, 89–90

### 命令行工具

- 安装, 89–90
- 未找到命令, 5
- 帮助信息, 6–7
- `info` 文档, 9
- 已安装命令, 查找, 5–6
- `man` 页面, 7

### 文件系统与配置

- 普通解释器文件系统 (`CIFS`), 167
- 参见 `Samba`
- 压缩, 105–107
- 目录中删除文件, 106
- 益处, 105
- `bzip2` 命令, 最高压缩, 107
- 压缩备份, 创建, 54
- `gzip` 命令, 106
- `gzipped` 文件, 合并, 106
- 列出/合并, 添加文件, 107
- `lz` 命令, 104
- 解压文件, 106
- 带有冗余输出, 106
- 配置文件, 211–213
    - `bash` shell 文件, 211–212
    - `bourne` shell 文件, 212
    - `c` Shell 文件, 212
    - 点文件, 查看, 19, 211
    - 文件夹, 22
    - 邮件, 32
    - `man` 页面, 8
    - `netpt` 文件, 55
    - 用于 `SSH` 服务, 212
    - 受信主机文件, 212
    - 虚拟网络计算文件, 213
    - `XMS`, 213
    - 启动文件, 213

### CoD

- 下载, 186
- 会话, 187
- 开始, 187

### 目录与磁盘

- `cores` 目录, 文件夹, 17
- `cp` 命令文件, 53
- `CPU`. `CPU` 管理: 运行进程, 135–136
- 查看消耗的时间, 135
- 使用率摘要, 打印, 135

### crontab

- 命令选项, 130–131
- `man` 页面 NAME 行, 7
- 个人创建, 130
- `C` shell, 配置文件, 212
- `UPS` 打印系统, 隧道传输, 180
- `curl` 命令
    - 下载/上传/删除文件, 162
    - 用户名/密码, 添加, 162
- `cut` 命令
    - 列, 打印, 76
    - 列, 字段范围操作, 76

### Cygwin

- `Cygwin`, 188

### D

- 守护进程, `man` 页面, 8
- `dlg` 命令
    - 文件系统信息, 查看, 24
- `Darwin`, 12
- 主机 IP 地址, `hostname`, 搜索 `DNS` 服务器, 150
- 挂载/卸载, 23–24
- 内核, 文件夹, 14
- 记录查询, 150
- `du` 命令
    - 数据, 复制, 54
    - 反向 `DNS` 查找, 151
    - 磁盘空间使用, 检查, 100–101
    - 数据库, 本地, 生成, 55
    - 特定服务器查询, 150
    - 多个目录, 指定, 100
    - 数据文件, 类型, 43
    - 递归查询, 150
    - 权限问题, 授予, 100
- `date`, 系统. 参见
- 目录, 44–53
- 使用 `root` 账户的总计, 100
- 命令; 时间/日期
- 添加/删除, 52
- 用户目录, 磁盘空间, 192
- 时间/日期, 更改, 138
- 时间/天, 显示, 18
- 比较所有文件, 106
- DVD(s)
    - 备份到, 110–111
    - ISO 镜像, 复制, 55
- 执行位, 运行在, 46
- 文件, 复制到, 53

### E

- `dd` 命令
    - 查找, 58
- `echo` 命令
    - 备份, 压缩, 54
    - 功能, 44
    - 命令哈希值, 29
    - 启动镜像, 复制, 54
    - 主目录, 18
    - 环境变量位置, 30
    - `IDE` 驱动克隆, 54
    - 数据, 复制, 54
    - 权限, 47–51
    - 切换, 添加, 79
    - 根目录, 16–18
    - 编辑器. 参见编辑器
    - `ISO` 镜像, 复制, 55
    - 共享
- `else` 命令, 文件名, 38
- `Emacs` 编辑
    - 警告, 54
    - 查看, 52
- `emacs` 命令, 历史, 30
- 删除文本, `vi` 编辑, 203
- `dirs` 命令, 目录,
- 功能, 65
- 更改顺序, 53
- 目录,
- 磁盘大小调整/分区.
- 基础命令, 用于
- 硬盘目录
- 配置文件, 212
- 分区, 95
- 下载, 位置, 18
- 设备(s)
- 驱动程序. 参见设备列表, 位置, 46
- 发行版 (`Distributions`), 4
- `Fink` 软件包, 用于 231
- `man` 页面, 8
- `DNS` 服务器, 配置, 143–144
- 邮件命令, 174
- 类型, 46
- 文档, 子目录
- `MBFS` 格式, 173
- 示例, 6
- 基于脚本,发送, 174
- 文件夹, 16
- 目录, 18
- 吞吐量/终端, 177
- 功能, 43, 46
- 文件/文件夹, 主目录,
- `df` 命令
    - 磁盘空间使用, 检查, 92
    - `hostname`, 17
- `env` 命令, 环境变量, 36
- 文件系统输出, 100
- `inode`, 更改, 99
- 点文件, 查看, 19, 211
- 文件夹, 22
- 邮件, 32
- `netpt` 文件, 55
- 用于 `SSH` 服务, 212
- 受信主机文件, 212
- 虚拟网络计算文件, 213
- `XMS`, 213
- 启动文件, 213
- 进入, 场景导航, 9
- 域名系统 (`DNS`)
- 驱动器信息, 显示, 24
- 桌面 `DB`, 文件夹, 16
- 开发者连接, 资源, 4
- 现有, 194
- `DUPL`, 9
- 电子邮件, 173–174
- 桌面/文件夹, 主目录,

### H

- 运行进程，为当前用户查看，193
- 带有文件的运行进程，124–125

### ifconfig 命令

- 可信主机文件，212
- `host` 命令，反向 `DNS` 查询，151

### halt 命令

- 益处，140
- 警告，140
- 挂断信号，`alovyd`，129

### 硬盘

- 硬盘分区，94
- 分配块，33
- 克隆 `IDE` 驱动器的分区，54
- 无破坏分区，95–96
- 步骤，94–95
- 卷，91–94

### HOSTNAME, 209

- 主机名
- `DNS` 服务器，105
- 信息，获取本地机器的，151

### G

- 游戏，帮助页面（`man pages`），8
- 通用映射工具（`Generic Mapping Tools`），`Fink` 软件包，224
- `GIF`，`Fink` 软件包，223
- `gimp` 命令，在前台运行进程，
- 哈希（`hash`），136–137
- `IP` 地址，查看以代替，155
- 设置，155

### hostname

- 主机名信息，查看，151
- 启动时的主机名，151
- 临时设置，153
- `Gimp` 工具提示，`Fink` 软件包，224
- 带有 `BSD` 的 `GNOME`，3
- `Fink` 软件包，220
- 图形图像处理程序（`GUI Image Manipulation Program`），用于，223

### HOSTYPE, 209

- 管理信息，用于 `le`，16
- 图形库，`OS X` 支持，11
- 图形编辑器，59
- 图形工具，`X11` 端口用户界面 (`GUI`)
- 与 `CD/DVD` 备份，带有，193
- `us` 命令行，4–5
- 远程访问，4
- 故障排除，4
- 不支持的功能，5
- 用户账户，管理，192–193

### HTML

- 在文件中识别，44
- 渲染，`Fink` 软件包，225
- 单页，解码，196
- `URL` 行，使用 `Perl` 提取，239–246

### 硬链接

### HTTP

- `gimp` 命令，在前台运行进程，哈希（`hash`），136–137
- 益处，110
- 创建，46
- 功能，43
- 索引节点（`inodes`），96
- 网络备份，110
- 文件，使用 `wget` 下载，159–161
- `tport`, `nele`，178

### 硬时钟。时间日期

- `hash-bang` 行（`hash-bang line`），76
- `dhdedit` 命令，带有 `CD/DVD` 备份，111
- `head` 命令，的，67–68

### HTTPS，文件，下载为 159–161

- 帮助消息，为命令显示，27–7

### HFS+ 文件系统

- 作为默认文件系统，92
- 特性，93
- 包含的重要内容，93

### HISTCMD, 209

- `HISTFILE`，209
- `HISTFILESIZE`，209
- 历史，`bash`
- 反向命令，30
- `history` 命令，编辑，30
- 命令，219
- 编辑命令，29
- `emacs` 风格的命令，30
- 导航，29
- 字符串，搜索，30

### I

- `ICAL` 事件，计划备份，112
- `ICMP` 数据包摘要，
- 显示，156

### id 命令，用户信息，

- 使用，14
- 检查，194

### ifconfig 命令

- 以太网设置，显示，145
- 文件，145
- 在网络连接的情况下将 `NIC` 硬设为 100Mbps，/ 停止，148
- 将 `NIC` 硬设为 10Mbps，
- 网络接口名称，显示，145

### grep 命令

- 搜索词着色，70
- 显示，名称，显示，70
- 不匹配的字符串，67
- 精确行，210
- 忽略大小写，72
- 单个文件，验证，61
- 递归搜索，70
- 文本字符串，69–70

### GROUPS, 209



- 组，分配，21

# gunzip 命令

- 将文件返回系统，105
- 解压缩文件，106
- 解压压缩包，105

# gzip 命令

- 使用其压缩，106
- 与 `and` 命令，105–106

# HOME, 209

- 家目录
- 访问，18
- `bash shell` 文件，211–212
- 目录，创建，19
- 其中的点文件，191
- 其中的文件/文件夹，18–19
- 转到，51
- 用户的文件夹，18

# host

- IP 地址，查看，151
- 跟踪路由 到，154–155

# if/then 命令

- NIC 能力列表，显示，145
- 关于其的信息资源，173
- 安装/启动，

# **ISO 镜像**

- 目录，创建在，163
- 后台发送下载，163
- FTP 服务器，连接到，162
- 本地目录，更改，163
- 匹配的文件，上传，163
- 新目录，更改，路径修正，165
- NIC 设置，更改，145
- 重启时的设置，146
- 镜像，复制，55
- 文件，下载，60
- 文件系统，93
- 语法，查看，38
- Fink 软件包，126–127
- 远程目录，更改，163
- 服务器目录，更改，163
- 使用 `shell` 命令，164
- 上传文件到服务器，164
- 数据库目录，94
- 功能，9

# J

- `jobs` 命令，后台，127
- 任务管理，127
- 继承，35

# K

- 内核
- `init` 命令，启动，40
- 用于 Darwin，17
- Mac OS 版本，10.5
- 循环，`bash shell` 结构，40
- 网关的连通性，52
- DNS 信息，保留，151
- `host` 命令，执行，150
- 子网掩码，更改，146
- 查询子集，153
- 设备文件，列表，46
- 目录，标识，45
- 文件索引节点，110
- 文件列表，显示，60
- 文件类型，在列表中显示，60
- 挂载驱动器，查看，24
- `ipfw` 命令，防火墙规则，更改，196
- 防火墙规则，列表，196

# L

- 登录名
- `last` 命令，合并，181
- 启动功能，05
- leopard 版本，15
- 使用 `less` 命令滚动，69
- **`LESSKERN`, 209**
- **`LOGNAME`, 209**

# M

- `man` 命令，组件相关的页面，显示，8
- `mkdir` 命令，目录，创建，45
- `mkfifo` 命令，命名管道，创建，27
- `more` 命令的局限性，68
- `mount` 命令，防止执行二进制文件，97
- 文件系统，96
- 文件系统类型，指定用于列表，96

# 命名管道

- 命名管道，创建，47
- 输出，重定向，31–32, 69
- `for` 语句变量，40

# 命名套接字

命名套接字，功能, 43, 47

`NAME` 行，显示, 7

`nano` 编辑, 65–66

网络接口，启动/停止, 149

启动/停止, 148

故障排除。参见：网络连接

统计，每秒刷新, 147

故障排除，g: 144–145

网络资源, 159–175

邮件, 173–174

文件传输, 159–165

添加, 65

控制键功能, 66–67

启动, 65

打开文本文件, 65

导航

文件系统, 51–52

信息屏幕, 9

类型，处理, 66–69

`vi` 编辑器, 201–202

`nctf` 配置，配置, 212

无线连接, 143–144

参见以太网卡；网络接口 (NIC)

故障排除, 151–157

地址解析协议 (ARP)，检查, 153

网络 实时聊天 (IRC), 172–173

远程目录共享, 165–171

网络时间协议 (NTP)

配置文件, 139

时间/日期，使用其设置, 99

换行符作者，添加到文本流中, 72

NFS 挂载的家目录，用于, 17

NetBSD，特性, 3

`netcmd` 命令，网络服务，启动/停止, 149

子网掩码和 IP 地址，更改, 146

# netstat 命令

- 活动连接，检查, 147, 156–157
- 字节单位的数据传输, 19
- NIC 统计，显示, 146–147
- 到主机的连接，检查, 152
- 默认网关，检查, 152
- IP 连通性，针对网络接口卡 (NIC), 144–145 以及路由表, 155–156
- TCP/IP 连接，检查, 152
- 到主机的 `traceroute`, 154–165

- `nice` 值，更改, 126
- `nice` 值，查看, 125–126
- 运行中的进程，调整优先级, 126
- 警告, 126

- `mblookup` 命令，识别 IP 地址, 170
- `nohup` 命令，挂断信号，以及, 129
- NTFS 系统特性，的, 93
- 空字符，生成, 54
- 数字，测试, 37
- 包级信息，查看, 156
- 快速统计，显示, 147
- 统计，每秒刷新, 147
- TCP 连接，查看, 146, 156
- UDP 连接，查看, 156

- `named`，共享文件系统, 99
- 网络备份, 107–112
- 硬链接，的, 110
- 增量备份, 110
- 本地到远程系统，配置文件, 109
- 备份文件的媒体, 107–108
- 镜像目录, 109
- 来自多个客户端, 138
- `noop` 工具, 108
- 网络连接, 143–157
- 网络文件系统 (NFS), 165–167
- 本地目录，可用性, 166
- 远程目录共享, 165–167
- 远程挂载，挂载, 166
- 共享目录，显示, 166
- 启动, 149
- 网络接口卡 (NIC), 144–146
- 活动连接，检查, 146
- 活动套接字，检查, 146
- 稳定性，显示, 145
- 配置, 145
- 以太网卡，显示, 145
- 以太网接口, 144
- 100Mbps 全双工, 146
- 10Mbits, 146
- IP 地址和子网掩码，检查, 146
- 网络接口名称，显示, 145
- 网络缓冲区，信息, 147
- 设置，检查, 145
- 重启时的设置, 146
- 统计，显示, 146–147

# 0

- Objective-C, 4
- 八进制导出 (Octal Dump), 54
- 命令，句柄，查看, 54
- `$DPWD`, 210
- OpenBSD，特性, 3
- `open` 命令, 87–90
- 多个文件，打开, 88
- 应用程序, 87–88
- Open Disk Utility，分区, 1
- OpenGL, 11
- 包，用于, 224–225

# OpenSSH

- 网络备份, 108
- 网站/资源, 108
- 孤儿文件，用于, 17
- `OSTYPE`, 210
- Outlook, 173
- 所有权，更改, 51

# 远程目录共享

# P

- Phoenix, 172
- 添加/删除目录, 52
- 分页器, 210
- 照片，默认位置, 19
- 目录，更改顺序, 53
- 文本文件分页, 69
- `pico` 编辑器, 65
- Mac OS 的, 6
- `more`/`less` 命令, 68
- 打印工作目录, 52
- 符号链接目录，分区
- 查看,
- `ftp` 服务器, 160
- 主机连接, 30
- `root` 用户, 34
- IP 连通性, 252

# Q

- 虚拟网络，加密架构 (VNC), 213
- 功能, 32, 46–47
- 包，用于, 233
- 以及 `wget` 命令, 160
- 命名管道, 43, 47

# R

- RAM
- 内存大小, 134
- 用法，查看, 134
- `RANDOM`, 5
- 脚本中的，36–37
- `shell` 版本, 210
- 读写文件系统，优势, 240
- 检查，用于, 216
- 示例应用程序，检查, 141
- 强制重启, 139–140
- 初始化, 143–144
- 停止命令，用于, 140
- 链接，提取, 243
- 重启命令, 140
- 加载包, 242–243
- 优势, 140
- `shebang` 行, 241–242
- 警告, 140
- 语法命令, 245
- 正则, 63–64
- 工具, 242
- 参见所有正则表达式
- URL，列表, 243

# 正则表达式

- 启用, 241–242
- 列表, 64
- `perl` 命令，查看, 57
- 安装, 239
- 文本文件，匹配, 63–64
- 普通, 43–44
- 拒绝访问, 100
- 创建, 44
- 更改, 48–50
- 识别, 43–44
- 所有权，更改, 51
- 普通文件，识别，来自 44
- 类型, 44
- 远程桌面管理，设置, 47

# `pgrep` 命令

- 命令名，查找, 120
- 远程目录共享, 165–171
- 进程 ID，查找, 124
- 用户进程，查找，格式化, 69

# 打印机

- 列, 76
- CUPS 服务，用于 180
- 打印发送，输出到，`shell` 脚本, 84
- 文本文件, 69
- 利用率摘要，CPU 进程, 182–183
- 程序例，man 页, 80

# 提示符 (COMMAND), 210

# `PS1`, 210

# `ps` 命令, 116–121

- 运行中的进程，当前, 117
- 发送邮件, 174
- 文本文件，分页, 68
- 公共文件夹，位置, 19
- 公共身份验证，服务, 181–183

# `pushd` 命令

- 添加/删除目录, 52
- 目录，更改顺序, 53

# `pkg_info -W` 命令

- 命令，查找, 6

# `popd` 命令

- 添加/删除目录, 52
- 目录，更改顺序, 53

- 端口转发。我们退出（转发）
- 网络文件系统 (NFS), 165–167
- 网络备份, 108–110
- 活动，监控正在进行的 `bab`, 121–123
- 屏幕分屏，`vi` 编辑器, 201
- 列, 118–120
- 自定义视图, 121
- 挂断辅助，帮助, 129
- `kelly`, 122–127
- 优先, 125–126
- 运行中的进程, 115–131
- 从远程服务器下载文件, 159–161
- `named`，共享文件系统, 99
- 网络备份, 107–112
- 硬链接，的, 110
- 增量备份, 110
- 本地到远程系统，配置文件, 109
- 备份文件的媒体, 107–108
- 镜像目录, 109
- 来自多个客户端, 138
- `noop` 工具, 108
- 网络连接, 143–157
- 本地目录，可用性, 166
- 远程目录共享, 165–167
- 远程挂载，挂载, 166
- 共享目录，显示, 166
- 启动, 149
- 网络接口卡 (NIC), 144–146
- 活动连接，检查, 146
- 活动套接字，检查, 146
- 稳定性，显示, 145
- 配置, 145
- 以太网卡，显示, 145
- 以太网接口, 144
- 100Mbps 全双工, 146
- 10Mbits, 146
- IP 地址和子网掩码，检查, 146
- 网络接口名称，显示, 145
- 网络缓冲区，信息, 147
- 设置，检查, 145
- 重启时的设置, 146
- 统计，显示, 146–147
- 包级信息，查看, 156
- 快速统计，显示, 147
- 统计，每秒刷新, 147
- TCP 连接，查看, 146, 156
- UDP 连接，查看, 156
- `named`，共享文件系统, 99
- 网络备份, 107–112
- 硬链接，的, 110
- 增量备份, 110
- 本地到远程系统，配置文件, 109
- 备份文件的媒体, 107–108
- 镜像目录, 109
- 来自多个客户端, 138
- `noop` 工具, 108
- 网络连接, 143–157

# S

- Samba, 167–171
- 屏幕会, 184
- 终端选项, 184
- 命名会话, 186
- 会，重连到 185
- 远程系统管理, 177
- 终端复用器, 186
- Secure Shell (SSH), severe 177–184
- 配置文件, 212
- 不同端口，操作, 180
- 强制退出, 179
- 功能, 174
- OpenSSH, 108
- 公钥身份验证, 181–183
- 远程命令，防止, 181
- 远程文件，拷贝, 164–165
- 远程登录, 179–183
- 启动, 149, 180
- `stanning`, 149

# `route` 命令

# `scp` 命令

- 客户端 ID，访问, 182
- 递归拷贝, 164
- 远程文件，拷贝, 164–165
- 特定端口，连接到, 161
- SCP 协议，下载文件, 161–162
- 参见 `route` 命令

# `rahot` 命令

- 文件系统快照, 108
- 网站/资源, 108

- 搜索引擎，Spotlight, 19–21
- `search engine`，Spotlight, 19–21
- `SECONDS`, 210

# `rsync` 命令

- 硬行，使用的, 110
- 增量备份, 110
- 微目录, 109

## `ssh` 命令

- 也是 `ssh` 命令
- SecureSockets Layer, Fink 软件包, 229–230
- 安全, 172–197
- `stdin`/`stdout` 输出, 重定向, 31–33
- 超能力, 34
- 终端, 访问, 27–28
- `smbsatus`, 当前连接/文件锁, 查看, 169
- BSD 套接字, 17–178, 191
- `chrooted jails`, 191
- 防火墙, 195–216
- FTP 下载问题, 162, 164
- 已登录, 查看信息, 193–
- 系统日志, 197
- 用户账户, 创建, 192

# `sset` 命令

- 用户特定的, 28–29
- 变量, 208–210

# 命名的 SHELL

# SHELL

# `shell` 脚本, 36, 41, 77–88

- 应用脚本, 216
- 基础脚本, 78–80
- `case` 语句, 81–83
- 文件系统快照, 108

# 套接字 (sockets)

- 激活, 146, 156
- 命名套接字, 43, 47

# 软链接

- 功能, 43
- 另见符号链接

- 将数字转换为文本文件, 74
- `dimiter`, 挑战性, 72
- 多次替换, 72
- 换行符, 添加, 72
- 文本, 回复, 71–
- 服务器上传, 午午时间, 77–78

# 命令-参数

- 添加, 80–83
- 添加到 `ccepter`, 37–38
- 文件名, 组, 36
- 第一行, 内容, 36
- 功能, 36
- 指令 示例, 78–80–

- Solaris, 3

# `sort` 命令

- 以内存使用为依据, 71
- 文本文件输出, 71

# 排序 (sorting)

- 内存使用, 降序, 71
- 运行进程列表, 122
- `shell` 中的间距问题, 83

- Server Message Block (SMB),

# `set` 命令

- 环境变量,
- 显示, 35
- `vi` 编辑器, 206

# `sftp` 命令, 文件传输, 165

# 拼写检查

- Fink 软件包, 225
- `Nano` 编辑器, 66

# `split` 命令, `vi` 编辑器, 分割, 201

# Spotlight (聚焦搜索), 19–21

- 访问, 19
- 高级搜索, 19
- 命令行搜索, 19–20

# `shasum` 命令

- 生成文件的校验和,
- 验证文件值, 61
- `SHALVM` 文件输出, 60

# `shell`, 27–41

- 别名, 33
- `bash` (Bourne Shell)
    - 历史记录, 29–30
    - 命令补全, 30
    - 配置流, 21
    - 权限委托, `sudo` 命令,
        - 内部调用, 78
    - 循环结构, 40
    - 否定测试, 37
    - `PATH`, 放置, 26
    - 输出, 84
    - 参考指南, 41
    - `runmp`, 37
    - `script` 命令, 83–84
    - 测试表达式, 运算符, 38–39

# `shutdown` 命令

- 优点, 140
- 警告, 140

# `sighup` 命令, 终端, 挂起, 129

# `skill` 命令, 向运行中的进程发送信号, 127–128

- 环境变量, 35
    - 功能, 27
    - 管理, 27–28
    - 输出类型, 31
    - 输出方向, 31–33
    - 脚本, 创建. 见 `shell` 脚本
    - 设置, 位置, 29
    - 间距问题, 83
    - 特殊字符, 207–208
    - 启动, 29
    - `stderr` 错误输出, 31–32

- 单文件传输, 161
- 单用户模式, 97
- `sites` 文件夹, 位置, 19
- 大尺寸, 93
- 基于...的搜索, 59
- 监控, 54

# `smbclient` 命令

- FTP 类型文件共享, 168
- 服务, 列出, 168

# `spasswd` 命令, 用户, 添加到 Samba, 168

# 密钥对, 生成, 181–182

- 列出存储的密钥, 183
- 登录, 验证, 181
- 私钥, 直到 USB 磁盘, 182–183
- 公钥验证, 181–183
- 远程命令, 防止, 181
- 移除存储的密钥, 183
- SSH 会话, , 180
- TCP 端口, 转发, 180
- 写入 `tgz` 文件, 109
- 解锁密钥, 存储, 183

## 启动 (startup)

- USB 驱动, 使用, 182–183
- X11 端口, 启用, 179–181



# 索引

## 符号

- 启动, 管理, 140
- stderr:
    - 输出, 31–32
    - shell 输出, 31–32
- stdin, 输入方法, 30
- stdout:
    - 输出, 31–32
    - shell 输出流, 31–32
- 停止系统, 命令, 140
- 存储设备, 136–137
- 开放文件/目录,
    - Apple 命令, 27
    - bash 搜索历史, 30
    - 转换为环境变量, 36
    - 使用 `grep` 命令搜索, 69–70
    - 使用... 命令搜索, 69
    - 使用正则表达式搜索, 63–64
    - 提取 ASCII 文本, 171
    - 根 shell, 34
    - root 密码, 34
    - 带时间的密码, 112
    - 超用户, 启用, 34
    - 交换空间 内存使用, 134
    - 备份, 45
    - 创建到系统, 52
    - 索引, 46

## S

- `sysctl` 命令
    - 内核参数, 141
    - 内核参数, 设置, 34
- `syslogd` (系统日志守护), 193
    - 消息, 发送, 197
- 系统管理
    - 远程. 见系统 182–183
    - 二进制文件文件夹, 16
    - 系统调用, 页面, 8
    - 系统日志发送到 syslog 设施, 197
- 系统管理, 133–141
    - 内核控制, 141
    - 内存管理, 134–35
    - 启动/停止系统, 启动, 25
    - 系统时间. 见 `date`, 139
- `telnet` 命令, 互联网, 排除, 178
- 临时文件文件夹, 17
- 终端 (Terminal), 12–15
    - 窗口, 12, 14
    - 结束, 13
    - Fink, 评估, 21–22
    - 键盘快捷键, 28
    - shell, 评估, 27–28
    - 用户特定设置, 28
    - 终端复用. 见 Remote Desktop
- 测试表达式, 脚本, 运算符, 38–39
- 配置文件, 测试, 171
- 默认项, 显示, 171
- Samba 配置, BSD 系统, 63
- 文本编辑器 (text-editors)
    - Emacs 编辑器, 65, 199
    - 图形文本编辑器, 195
    - nano 编辑器, 65
    - pico 编辑器, 65
    - vi 编辑器, 64, 65–199
    - Emacs 编辑器, 65
    - 文本文件, 63–76
    - 提取 ASCII 文本, 71
    - 在二进制文件中查找文本, 71
    - 字符转换, 73
    - 列, 75
    - 比较两个文件, 73
    - 另见文本编辑器格式, 69
    - 列表, 68
    - 使用正则表达式匹配, 63–64

## T

- tab(s), 屏幕导航, 9
- tab 键, 命令行补全, 30
- `tail` 命令
    - 文件定义, 698
    - 持续监控, 68
    - 文件大小 宽度, 34
- 磁带存档 (tape archive), 搜索
- `tar` 命令, 103–105
    - 添加文件到存档, 107
    - 使用 `bzip2` 压缩的存档/压缩, 106
    - 有横线/无横线, 104
    - 功能, 104
    - 从本地到远程系统拷贝文件, 109
    - 从多个客户端备份, 108
    - 合并多个文件以添加存档, 107
    - 将文件返回系统, 105
    - 符号链接备份, 注意, 45
    - 系统行为, 104
    - 排序到 `tgz` 文件, 109
    - 解压/存档用户, 109

## TCP

- 传输层协议 (TCP)
- Telnet
    - 下载文件, 161–162
    - 强制退出, 178
    - 第三方安装程序文件夹, 17
- Thunderbird, 173
- Tiger, 版本 10.4, 25
- Time Capsule, 111

## V

- `vi` 编辑器
- 时间/日期, 137-139
    - 自动操作, 139
    - 按月份显示日期, 139
- `tr` 命令
    - 字符转换, 73
    - 删除字符, 73
    - 添加换行符, 72
    - 字符范围, 73
    - 另见 `unmount` 命令
- `unmount` 命令
    - 卸载文件系统, 97
    - 按设备名卸载, 97
    - 按挂载点卸载, 97
- 解压缩文件. 见压缩
- 撤销, vi, 204
- Unicode, 编码, 93
- 解锁格式, 74
- UNIX
    - 命令行, 4-5
    - 命令行参考源, 6-9
    - Mac OS X, 完全支持, 112
    - 文本编辑器. 见 `vi` 编辑器
    - UNIX 文件系统 (UFS), 101
- `unmask` 命令
    - 设置权限设置, 51
- `var` 目录, 为, 17
    - 变量
    - shell, 的, 208–210
- `touch` 命令, 空白文件, 创建, 44

## view 命令

- 命令模式，返回，204, 205
- 兼容性选项，199
- 删除，203
- 排除，205–206
- 文件，打开，201
- 合并行，204
- 击键命令，列表，201
- 在...中进行导航，201–202
- 使用命令修改
- 粘贴文本，203
- 退出，200
- 只读模式，在其中编辑，200
- 重复命令，204
- 保存文件，200
- 设置，更改，206
- 多个文件，编辑，200–201
- 拆分 split，201
- 开始，200
- 文本，更改，203
- 类型，199
- 撤销
- `Vi`（改进版），65, 199–200
- 在视觉模式下，206
- **`view` 命令**，只读模式，在其中编辑，200
- **`Vi` (改进版)**，65, 199
- `vim-6-package`，200
- 另见编辑器
- **`vimdiff` 命令**，文件，比较，74
- **`vimtour` 命令**，199
- **虚拟桌面计算 (VNC)**，188–189
    - 配置文件，189, 213
    - 功能，177
    - 安全外壳 (SSH) 系统，177
    - 提交，194
- **`vncpasswd` 命令**，查看密码，存储，213
- **卷（卷）**
    - 定义，91
    - 硬盘分区，94
    - 信息，查看，95
    - 重新分区系统，92
- **`vsplit` 命令**，`vi` 编辑器屏幕，拆分，201

## W

- **`wc` 命令**，文件行/字节，打印，21
- **网页**，下载单页，160
- **Web 共享**，文件夹，位置，199
- **`wget` 命令**
    - FTP 服务器，登录，160
    - 下载文件的 html 地址，160
    - 中断的下载，继续，161
    - 行和继续功能，161
    - 登录/密码，输入，160
    - 远程服务器，下载，200
    - 重命名为本地名称，单页，下载，160
    - 网站，本地可用副本，161
    - web，递归镜像，
- **`whatis` 命令**，NAME 行，显示，7
- **`whereis` 命令**，文件，查找，59
- 已安装命令，查找，6
- **`which` 命令**，文件，查找，59, 想要哪个，6
- **`while` 块**，Perl，242
- **`while` 命令**，变量用于，40
- **`who` 命令**，登录，检查，194， 用户交互，检查，194
- **Windows 桌面**，186–187
    - 从 Mac OS X 连接，186–187
    - Code，186–187
- **无线**连接
    - AirPort，143–144
    - 配置，143–144
- **字数**，文本，文件，71

## X

- **`X11` 图形库**，11
- 用于 CUPS 打印服务的 **`X11` 端口转发（隧道）**，180
    - 启用，179
    - 为单个会话启用，179
    - 永久启用，179
    - 到 Internet 服务器，180–181 配合 Secure Shell，179–181
- **`xargs` 命令**，与 except 比较，58，输出，重整理，33
- **`xchat` 命令**，远程时钟，打开，188
- **`XCode` 工具**，227
- **`Xmers` 编辑器**，65
- **`xhost` 命令**，远程应用程序，允许，188
- **`XML` 软件包**，用于，227
- **`Xming` 播放器**，配置文件，213
- **`xnu` 内核**
- `xterm` 命令，远程，终端，188
- **`X Window` 系统 (X)**，187–188
    - 访问控制，188
    - 远程应用程序，允许，188
    - 启动文件，213
    - 服务器/X 客户端，187–188
- **`Zed's Terminal`**，Final 软件包，用于，227–228
- 压缩文件
    - 存档输出，104–105
    - 解压缩，106
    - 解包/解压，105
    - 另见压缩

# 了解 Linux 工具箱内部情况

查看该系列中的其他书籍。

可在 www.wiley.com 获取

Wiley 和 Wiley 标志是 John Wiley & Sons, Inc. 或其关联公司的注册商标。Linux 是 Linus Torvalds 的注册商标。所有商标均归其所有者。

# 探索强大的 MAC OS X 命令

这本实用、紧凑的指南教你如何像专家一样从命令行使用 OS X UNIX 系统。尝试超过 1000 条命令来查找和获取软件、监控系统健康和安全以及访问网络资源。运用从书中中学到的技能来排除故障、锁定安全并发现你关心的关于 OS X 系统的的一切。

# 扩展你在以下领域的 OS X UNIX 专业知识：

- 使用 shell
- 查找在线软件
- 处理文件
- 处理音乐和图像
- 管理文件系统
- 备份数据
- 检查和管理运行进程
- 访问网络资源
- 远程系统管理
- 锁定安全

Christopher Negus 在 AT&T 实验室参与了七年的 UNIX 系统开发，那里 UNIX 被创建和开发。他还与 Novell 合作开发了 Unix 和 UnixWare。Chris 是 Fedora 和 Red Hat Linux 系列、《Linux Toy II》、《Linux Troubleshooting Bible》以及《Linux Book 2008 Edition》畅作者。他现在是 Hat 的培训师。

Francis Caen 通过他的公司 Turbosphere LLC 托管和管理业务应用程序基础设施。作为开源倡导者，他曾就 OS 网络管理和互联网服务进行讲座，并担任 Tacoma Linux 用户组的成员。他是 Hat 认证工程师 (RHCE)。

Thomas Myer 是一位顾问、演讲者和作家。他已深度参与 Mac OS X 和 iPhone 编程的各个方面。他已将其整个开发业务切换到基于 Mac 的系统。
