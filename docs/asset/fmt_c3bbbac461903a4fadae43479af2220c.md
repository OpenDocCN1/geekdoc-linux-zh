
# Web 服务器工具

首先是 Web 服务器程序——让你的计算机能够向浏览器发送 Web 页面的软件。下一章将介绍 `Linux` 提供的许多 Web 服务器，包括免费的和提供商业支持的。Web 服务器既稳健又快速。许多服务器还使用 `First Virtual`、`Verisign` 或类似技术确保交易安全。以下列表仅列出了 `Linux` 提供的几种 Web 服务器：

- 来自美国在线的 `AOLServer`（位于 `http://www.aolserver.com/server/index.html`）
- 来自 Apache 项目的 `Apache`（位于 `http://www.apache.org`）
- 来自 `UKWeb` 的基于 `Apache` 的 `Stronghold SSL Web Server`（位于 `http://stronghold.ukweb.com`）
- 来自 `Caldera, Inc.` 的、与 `Netscape` 拥有独家许可的针对 `OpenLinux` 的 `Netscape 快速通道 (Netscape FastTrack) for OpenLinux`（位于 `http://www.caldera.com`）
- 来自国家超级计算机应用中心的 `Zeus httpd server`（位于 `http://hohooo.ncsa.uiuc.edu`）

## 防火墙

大多数 Web 服务器还需要你的计算机系统与互联网之间提供安全保护。防火墙是提供这种保护的最常见方法。

`Linux` 有可用的商业防火墙软件。这些软件包允许你配置哪些网络数据包到达你的 Web 服务器或网络中的其他计算机，并封堵许多潜在的安全漏洞。`Linux` 带有强大的 `IP` 过滤功能可能对你已经足够了，但附加防火墙软件的主要优势之一是它让安全性的设置和维护变得简单得多。以下列表给出了 `Linux` 提供的几种防火墙工具：

- 来自 `TIS` 的 `Firewall Toolkit`（位于 `http://www.tis.com/docs/products/fwtk/index.html`）
- 来自荷兰 `X/OS` 的 `ipfwadm` 实用，一种 `IP` 防火墙管理工具（位于 `http://www.qos.nl/linux/ipfwadm`）
- 来自 `WatchGuard Technologies` 的 `WatchGuard` 防火墙（位于 `http://www.watchguard.com`）
- `CERN` Web 服务器的一部分的 `WebFilter`（位于 `http://www.w3.org/pub/WWW/Daemon`）

## 硬件支持

你可能需要的用于设置 Web 服务器或完整互联网服务器的所有特殊硬件，`Linux` 均提供支持。这包括终端服务器、`ISDN` 板、帧中继继板、路由器板、高速网卡、`256` 端口串行卡等。

在第二部分中，当你决定如何将 Web 服务器连接到互联网时，将读到更多关于使用这些外围设备的内容。关于一些最热门硬件选项的具体信息将在第 `4` 章中提供。

## HTML 转换工具

有许多转换过滤器帮助你从现有材料创建 `HTML` 文档。如果你有 `WordPerfect`、`Word`、`RTF`、`FrameMaker`、`LaTeX`、文本文件或许多其他格式的文档，`Linux` 都提供了免费的过滤器。还有几种商业过滤器。以下列表显示了流行的 `HTML` 工具（参阅第 `1` 章获取更全面的跨平台转换工具列表）：

- 来自 `Empress Software, Inc.` 的 `Empress DataWEB`（位于 `http://www.empress.com`）
- `LaTeX2HTML`，一个免费软件项目（位于 `http://cbl.leeds.ac.uk/nikos/latex2html/html/latex2html.html`）
- 来自 `Talentoft` 的 `Web+`，一种 Web 到数据库的集成工具（位于 `http://www.talentoft.com`）
- `WebTuk`，一个免费的图形 `HTML` 编辑工具（位于 `http://www.sunscript.sun.com`）

## HTML 验证工具

文档从原始格式转换为 `HTML` 或从零创建 `HTML` 页面之后，通常会使用 `HTML` 验证工具来检查 Web 页面的质量。

`Linux` 支持多种 `HTML` 验证工具，可以在你的客户指出页面上的错误之前，检查你的 `HTML` 页面的一致性、编码错误以及拼写错误。支持多种语言的几种标准拼写检查器也支持创建无错误的 Web 文，并包含在包括 `OpenLinux Lite` 在内的标准 `Linux` 发行版中。

列表列出了 `Linux` 可用的几种免费 `HTML` 验证工具（第 `19` 章详细介绍了 `HTML` 验证工具）：

- 来自 `Electronic Publishing Corporation` 的 `Linkscan`（位于 `http://www.elsop.com/linkscan/index.html`）
- `VWbot`，一个共享软件网站爬虫（位于 `http://vancouver-webpages.com/VWbot`）
- 来自 `Webethreads, LLC` 的 `webthreads`（位于 `http://www.webthreads.com`）

## 统计工具

通过跟踪你的网站的使用情况，你可以深入了解客户对什么感兴趣，以及你的网站满足他们需求的程度如何。统计工具允许你跟踪网站活动的许多方面，包括访问者如何使用你的网站查找信息。你可以跟踪诸如最热门页面、一天中最忙的时段以及你页面的全球吸引力。第 `13` 章将详细介绍 Web 统计。

`Linux` 有许多基于脚本和 `C` 语言的统计工具，可以分析日志文件、创建动态图表。以下列表显示了 `Linux` 提供的许多统计工具：

- 位于 `http://www.lily.net` 的 `Lilypad`
- 位于 `http://www.uci.edu/` 的 `wwstat`
- 位于 `http://www.umass.edu/` 的 `gwstat`

## 结论

除非你想开发新的应用程序，否则如今这些并不真的有必要。像 `Caldera` 这样的系统是完全自动化的。即使你需要向内核添加模块或重制系统，一切都是通过自动化脚本完成的，这些脚本会向你提问并为你完成所有工作。（将在第 `21` 章中带你实际重制 `Linux` 内核。）与其他系统相比，正如一家大银行的信息系统高管所说：“`Windows NT` 在许多互联网服务中确实不那么稳定。”

# 强力的 Web 工具

本书的其余部分将介绍你使用 `Linux` 可以进行的所有与 Web 相关的操作，但这里有一个快速的预览。此列表包含了一些可用工具，几乎全部都是免费的，以帮助你创建和维护基于 `Linux` 的网站。

## 涂鸦 (doodles)

- `AppGen`（位于 `http://www.man.ac.uk/~whaley/ag/appgen.html`）
- `Gifmap`（位于 `http://www.cyberram.net/~bfriesen/gifmap`）
- `heintl`（位于 `http://www.heintl.com/`）
- `Mapedit`（位于 `http://www.boutell.com/map`）

## Linux Web 服务器工具包

`Linux` 的销售数据无法以精确的形式呈现，因为销售 `Linux` 的公司都是私有企业，而且许多用户在一年内会多次购买，这使得收集准确的统计数据变得困难。然而，最新信息似乎表明全球每月购买的 `Linux` 数量超过 `10,000` 份。这个数字还没有加上通过书籍、杂志发行以及从 `FTP` 站点下载的数万份。

# Linux 应用程序

在过去的 `18` 个月中，`Linux` 可用的应用程序数量急剧增加。`Linux` 商业 `HOWTO` 和 `Caldera` 网站上的合作伙伴信息是跟踪 `Linux` 商业应用开发进展的两个良好途径。表 `2-1` 列出了几个 `URL`。

# 表 2-1 跟踪可用 Linux 应用程序列表的网站

| 网站 | URL |
|---|---|
| Linux 应用程序与实用程序页 | http://www.chariott.com/linapps.html |
| Linux 商业 HOWTO | http://www.caldera.com/LDP/HOWTO/Commercial-HOWTO.html (或其他 LDP 站点) |
| Caldera OpenSolutions 目录 | http://www.caldera.com/ |
| Linux 科学应用 | http://SAL.kachinatech.com |

在过去的 `18` 个月中，美国和德国的顶级供应商在各个类别中增加了应用程序，如数据库、办公套件、`POS` 和会计等垂直应用、开发者工具，甚至是游戏。图 `2-3` 显示了 `Caldera` 在线应用程序目录的一页。

`SunSoft` 产品 `Wabi` 的可用使得 `Linux` 能够运行 `16` 位 `Windows` 应用程序，这为 `Linux` 作为桌面或家庭计算系统的使用开辟了新领域。但那是另一个故事了。
