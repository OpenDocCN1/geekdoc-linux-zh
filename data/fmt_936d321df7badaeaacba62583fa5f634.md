
PPP 支持由 Michael Callahan <callahan@maths.ox.ac.uk> 和 Al Longyear <longyear@nec.com> 添加。这对于增加主动使用 Linux 进行网络的人数也至关重要。

Jonathan Naylor <jsn@cs.nott.ac.uk> 通过显著增强 Alan 的 AX.25 代码，添加 NetRom 和 Rose 协议做出了贡献

支持。AX/25/NetRom/Rose 支持本身意义重大，因为没有其他操作系统（除 Linux 外）可以宣称对这些协议提供标准的原生支持。

当然，还有数百位其他人为 Linux 网络软件的开发做出了重大贡献。其中一些人在后文的技术特定章节中会被提及；其他人则贡献了模块、驱动程序、错误修复、建议、测试报告以及精神支持。在所有情况下，每个人都可以声称自己发挥了作用并提供了力所能及的贡献。Linux 内核网络代码是 Linux 无政府主义开发风格所能取得的成果的绝佳范例；如果它尚未让你惊讶，那么很快你就会感到惊奇。开发工作并未停止。

## 在哪里获取有关 Linux 网络的更多信息

有许多地方可以找到有关 Linux 网络的良好信息。

Alan Cox，Linux 内核网络代码的当前维护者，维护一个万维网页面，该页面包含 Linux 网络当前和新发展的亮点，位于 `www.uk.linux.org`。

另一个好去处是一本由 Olaf Kirch 撰写的书，题为*《网络管理员指南》*。它是 Linux 文档项目（见 `http://MetaLab.unc.edu/LDP/`）的一部作品，你可以交互式阅读其 HTML 版本（见 `http://MetaLab.unc.edu/LDP/nag/nag.html`），或者通过 ftp 从 MetaLab.unc.edu 的 LDP ftp 存档获取各种格式（见 `ftp://MetaLab.unc.edu/pub/linux/docs/LDP/network-guide/`）。Olaf 的书非常全面，提供了 Linux 下网络配置的良好高层概述。

在 Linux 新闻组层次结构中，有一个专门用于网络和有关事项的新闻组（见 `news:comp.os.linux.networking`）。

还有一个邮件列表可供订阅，你可以提出与 Linux 网络相关的问题。要订阅，你应该发送一条电子邮件：

致：`major-domo@vger.rutgers.edu`

主题：任意内容

正文：

`subscribe linux-net`

在各种 IRC 网络上，通常有 `#linux` 频道，在那里人们可以回答关于 Linux 网络的问题。

在报告任何问题之前，请记住包含尽可能多的关于问题的相关细节。具体而言，你应该指定你正在使用的软件版本，特别是内核版本，`ppp` 或 `dip` 等工具的版本，以及你正在经历的问题的确切性质。这意味着要注意你收到的任何错误消息的确切语法以及你发出的任何命令。

## 在哪里获取一些非 Linux 特定的网络信息

如果你寻求有关 TCP/IP 网络的一般基础教程信息，我建议你查看以下文档：

- **TCP/IP 简介** 此文档既有文本版本（见 `ftp://athos.rutgers.edu/runet/tcp-ip-intro.doc`），也有 PostScript 版本（见 `ftp://athos.rutgers.edu/runet/tcp-ip-intro.ps`）。

- **TCP/IP 管理** 此文档既有文本版本（见 `ftp://athos.rutgers.edu/runet/tcp-ip-admin.doc`），也有 PostScript 版本（见 `ftp://athos.rutgers.edu/runet/tcp-ip-admin.ps`）。

如果你寻求有关 TCP/IP 网络的更详细信息，我强烈推荐：

*《利用 TCP/IP 进行互连，第 1 卷：原理、协议和体系结构》*，Douglas E. Comer 著，ISBN 0-13-227836-7，Prentice Hall，第三版，1995 年。

如果你想了解如何在 Unix 兼容环境中编写网络应用程序，我也强烈推荐：

*《Unix 网络编程》*，W. Richard Stevens 著，ISBN 0-13-949876-1，Prentice Hall，1990 年。

该书的第二版即将出现在书架上；新书由三卷组成：请访问 Prentice-Hall 的网站（`http://www.phptr.com/`）进行进一步探究。

你也可以尝试 `comp.protocols.tcp-ip` 新闻组（见 `news:comp.protocols.tcp-ip`）。

有关互联网和 TCP/IP 协议套件的具体技术信息的一个重要来源是 RFC。RFC 是“Request for Comment”（请求评论）的首字母缩略词，是提交和记录互联网协议标准的标准方式。有许多 RFC 存储库。这些站点中的许多是 ftp 站点，其他提供万维网访问和相关的搜索引擎，允许你搜索 RFC 数据库中的特定关键字。

获取 RFC 的一个可能来源是 Nexor RFC 数据库（见 `http://pubweb.nexor.co.uk/public/rfcs/index/rfcl.html`）。

### 通用网络配置信息

在你实际尝试配置网络之前，你基本上需要了解并理解以下小节。它们是基本原则，无论你想部署的网络的确切性质如何，都适用。

### 开始需要哪些？

在你开始构建或配置网络之前，你需要一些东西。其中最重要的是：

#### 当前内核源代码

由于你当前运行的内核可能尚未支持你希望使用的网络类型或网卡，你可能需要内核源代码，以便使用适当的选项重新编译内核。

你总是可以从 `ftp.kernel.org`（见 `ftp://ftp.kernel.org/pub/linux/kernel`）获取最新内核源代码。请记住 `ftp.kernel.org` 严重超载：获取当前源代码的首选方式是下载补丁而不是完整的 tar 文件；此外，你应该首先尝试访问主要 ftp 站点的镜像，如 `ftp.funet.fi`（见 `ftp://ftp.funet.fi/mirrors/ftp.kernel.org/pub/linux/kernel`）；还要记住每个 Linux 站点通常都携带更新的内核源代码。

通常，内核源代码会解压缩到 `/usr/src/linux` 目录。关于如何应用补丁和构建内核的信息，你应该阅读《内核 HOWTO》（见 `Kernel-HOWTO.html`）。关于如何配置内核模块的信息，你应该阅读“模块 mini-HOWTO”。此外，内核源代码中的 README 文件和 Documentation 目录对勇敢的读者来说非常有信息量。

除非另有明确说明，我建议你坚持使用标准内核版本（版本号中第二位数字为偶数的那个版本）。开发版本内核（第二位数字为奇数的版本）可能包含结构或其他变更，这可能会导致与你系统上其他软件的问题。如果你不确定自己能否解决这些问题，就不要使用它们。

另一方面，此处描述的一些功能是在 2.1 内核开发期间引入的，因此你必须做出选择：你可以坚持使用 2.0 版本，等待 2.2 版本和带有每个新工具的更新发行版，或者你可以获取 2.1 版本并寻找利用新功能所需的各个支持程序。在我写这一段时，1998 年 8 月，2.1.115 是当前版本，2.2 预计很快会出现。

#### 当前网络工具

网络工具是你用来配置 Linux 网络设备的程序。这些工具允许你为设备分配地址并配置路由，例如。

大多数现代 Linux 发行版都附带网络工具，因此如果你是从发行版安装的，并且尚未安装网络工具，那么你应该安装它们。

如果你不是从发行版安装的，那么你需要自己获取源代码并编译工具。这并不困难。

网络工具现在由 Bernd Eckenfels 维护，可在以下位置获取：`ftp.inka.de`（见 `http://ftp.inka.de/pub/comp/Linux/networking/NetTools/`），并在以下位置有镜像：`ftp.uk.linux.org`（见 `http://ftp.uk.linux.org/pub/linux/Networking/base/`）。

务必选择最适合你希望使用的内核的版本，并按照包中的说明进行安装。要安装和配置本文写作时的当前版本，你需要执行以下操作：

```
user% tar xvzf net-tools-1.33.tar.gz
user% cd net-tools-1.33
```

此外，如果你计划配置防火墙或使用 IP 伪装（IP masquerade）功能，你将需要 `ipfwadm` 命令。可以从以下地址获取最新版本：`ftp.xos.nl`（参见 `ftp://ftp.xos.nl/pub/linux/ipfwadm`）。同样，有多个版本可供选择。务必选择与你内核版本最接近的版本。请注意，Linux 的防火墙功能在 2.1 版本开发期间发生了变化。这仅适用于 2.0 版本的内核。

要安装并配置本文撰写时的最新版本，你需要执行以下操作：
