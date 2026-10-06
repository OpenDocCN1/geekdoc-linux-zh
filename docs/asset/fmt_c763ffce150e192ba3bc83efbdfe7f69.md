
iBCS2 可从 `ftp://linux.mit.edu/pub/ADSM` 获取。你必须使用 `SCO` 二进制文件并安装 `iBCS2` 模拟器来运行 `ADSM`。此描述针对 `ADSM v2rl`。在本文编写期间，我只知道一个适用于 `i386 Linux` 的版本。例如，`f` 窗口管理器将管理虚拟桌面，你可以随心所欲地自定义颜色、字体、窗口大小和位置等。

iBCS2 可从 `ftp://linux.mit.edu/pub/ADSM` 获取。你必须使用 `SCO` 二进制文件并安装 `iBCS2` 模拟器来运行 `ADSM`。此描述针对 `ADSM v2rl`。在本文编写期间，我只知道一个适用于 `i386 Linux` 的版本。

iBCS2 可从 `ftp://linux.mit.edu/pub/ADSM` 获取。你必须使用 `SCO` 二进制文件并安装 `iBCS2` 模拟器来运行 `ADSM`。此描述针对 `ADSM v2rl`。在本文编写期间，我只知道一个适用于 `i386 Linux` 的版本。

你必须在你的 `XF86Config` 文件中插入一个新的适当的模型，以定义具有较低刷新率的分辨率。例如，将旧值：

```
Modeline "1024x768" 75 1024 1048 1184 1328 768 771 777 806 -hsync -vsync
```

替换为：

```
Modeline "1024x768" 65 1024 1032 1176 1344 768 771 777 806 -hsync -vsync.
```

魔法数字 `75` 和 `65` 是你通过 `X` 在 `X.err` 文件中找到的相应时钟频率。请查阅 `XF86` 文档中的 `monitors` 文件，获取适用于显卡在 `16` 位色彩深度下能提供的最大时钟频率的 `Modelines`。

# 3 安装 ADSM 客户端

`ADSM` 是一种基于网络的备份系统，由 `IBM` 销售，被许多机构使用。适用于多种系统（不同的 `UNIX` 品牌、`Windows`、`Novell`、`Mac`、`Windows NT`）。遗憾的是，在本文编写期间，还没有原生 `Linux` 版本。

你必须使用 `SCO` 二进制文件并安装 `iBCS2` 模拟器来运行 `ADSM`。此描述针对 `ADSM v2rl`。在本文编写期间，我只知道一个适用于 `i386 Linux` 的版本。

iBCS2 可从 `ftp://linux.mit.edu/pub/ADSM` 获取。你必须使用 `SCO` 二进制文件并安装 `iBCS2` 模拟器来运行 `ADSM`。此描述针对 `ADSM v2rl`。在本文编写期间，我只知道一个适用于 `i386 Linux` 的版本。

iBCS2 可从 `ftp://linux.mit.edu/pub/ADSM` 获取。你必须使用 `SCO` 二进制文件并安装 `iBCS2` 模拟器来运行 `ADSM`。此描述针对 `ADSM v2rl`。在本文编写期间，我只知道一个适用于 `i386 Linux` 的版本。

你必须在你的 `XF86Config` 文件中插入一个新的适当的模型，以定义具有较低刷新率的分辨率。例如，将旧值：

```
Modeline "1024x768" 75 1024 1048 1184 1328 768 771 777 806 -hsync -vsync
```

替换为：

```
Modeline "1024x768" 65 1024 1032 1176 1344 768 771 777 806 -hsync -vsync.
```

魔法数字 `75` 和 `65` 是你通过 `X` 在 `X.err` 文件中找到的相应时钟频率。请查阅 `XF86` 文档中的 `monitors` 文件，获取适用于显卡在 `16` 位色彩深度下能提供的最大时钟频率的 `Modelines`。

# 4 运行客户端

`ADSM` 是一种基于网络的备份系统，由 `IBM` 销售，被许多机构使用。适用于多种系统（不同的 `UNIX` 品牌、`Windows`、`Novell`、`Mac`、`Windows NT`）。遗憾的是，在本文编写期间，还没有原生 `Linux` 版本。

你必须使用 `SCO` 二进制文件并安装 `iBCS2` 模拟器来运行 `ADSM`。此描述针对 `ADSM v2rl`。在本文编写期间，我只知道一个适用于 `i386 Linux` 的版本。

有两个客户端：一个是 `X11` 接口 `dsm`，另一个是命令行接口 `dsmc`。你的计算机中心会告诉你如何运行它。可能需要在启动机时运行某个启动脚本，例如

```dsm schedule -quiet 2>&1 >/dev/null \
```

# 5 已知问题

遗憾的是，`SCO` 只能处理超过八个字符的主机名。如果你的主机名更长或全限定，你可能需要在 `/usr/adsm/dsm.sys` 的 `NODename` 行中指定你的主机名。如果你使用 `DISPLAY` 变量，将提供全限定的主机名（例如使用 `DISPLAY=host.full.do.main:0` 而不是 `DISPLAY=host:0`）。

# 第 XLVII 部分

## 由 Paul L. Rogers 编写“Linux 推广 mini-HOWTO”

努力

# 目录

- 1 关于本文档 ........................................................................................ 1573
- 2 简介介绍 ........................................................................................................ 1573
- 3 相关信息 ............................................................................................ 1574
- 4 推广 Linux ................................................................................................... 1574
- 5 行为准则 ............................................................................................ 1575
- 6 用户组 ..................................................................................................... 1575
- 7 厂商关系 ................................................................................................ 1575
- 8 媒体关系 ................................................................................................... 1576
- 9 致谢 ............................................................................................... 1576

![](img/e0ed64e774a11b944fd2651b5a09cd8c_1574_0.png)

# 摘要

v0.4, 1997年2月6日

本文档为 Linux 社区如何有效推广 Linux 的提供了建议。

# 1 关于本文档

本 Linux 推广 mini-HOWTO 旨在提供指南和建议以协助您的 Linux 推广工作。

本 mini-HOWTO 的灵感源于 Jon “maddog” Hall，他在回复关于推广 Linux NetDay96 (http://www.netday96.com) 活动指南的反馈请求时。他对这些指南给出了积极回应，并指出这些指南是一项有益于 Linux 社区的“行为准则”列表的基础。

本文的 HTML 格式可在 http://www.datsync.com/rogers/Advocacy-HOWTO.html 处获取。

Nat Karemvich <nat@nataka.fr.eu.org> 正在将本文档翻译成法语。

中谷千惠 <janie@mbox.kyoto-inetor.or.jp> 已将本文档翻译成日语。

日语版（http://jf.ge.kyoto-u.ac.jp/JF/JF-ftp/euc/Advocacy.euc）。

Linux 推广 mini-HOWTO 的作者和维护者是 Paul. Rogers <Paul.L.Rogers@li.org>。

欢迎提出意见和建议。

如果您需要更多关于 Linux 文档项目（Linux Documentation Project）或 HOWTO 的信息，请随时联系主管 Greg Hanks <hregh@sumsite.unc.edu> 或每月关注几个国家和国际新闻组。

# 2 简介

Linux 社区一直很清楚，许多应用程序都是稳定、可靠、健壮（尽管并非完美）的产品。遗憾的是，仍然有很多人（包括关键决策者）并不知道 Linux 的存在及其能力。

如果 Linux 以及构成 Linux 发行版的许多其他组件要发挥其全部潜力，我们接触潜在的“客户”并推广（注意不要过度承诺）使用合适的 Linux 应用是至关重要的。我的公司的产品之所以在市场上表现良好，很大程度上不是因为产品技术上的优越性，而是因为公司的营销能力。

如果您使用 Linux 并希望为 Linux 社区做出贡献，请考虑采取本 mini-HOWTO 中的一个或多个想法，帮助他人通过 Linux 推广了解 Linux。

Linux 国际组织 (http://www.li.org/) 的目标是促进 Linux 的开发和使用。

Linux 文档项目 (http://sunsite.unc.edu/mdw/linux.html) 是 Linux 推广者的宝贵资源。

Linux 业务应用网站 (http://www.m-tech.ab.ca/linux-biz) 为那些依赖 Linux 进行日常业务运营的机构提供了一个分享经验的论坛。

Linux 推广项目 (http://1mb.com/linux/) 的目标是鼓励商业应用开发者为其软件提供原生的 Linux 版本。

Linux CD 支持赠送活动 (http://email.math.ucsb.edu:8000/giveaway.html) 正通过鼓励使用 Linux CD-ROM 让 Linux 更加普及可用。

Specialized Systems Consultants, Inc. (SSC) 出版了《Linux 杂志》(http://www.ssc.com/lj/) 以及在线时事通讯《Linux Gazette》(http://www.lg/)。

# 3 相关信息

comp.os.linux 新闻组公告员 Lars Wienius 也有一些想法 (http://www.iki.fi/liw/texts/advocating-linux.html)—advocating-linux.html。

# 4 推广 Linux

- 分享你关于 Linux 的个人经验（好的坏的）。每个人都知道软件有 Bug 和局限性，如果我们对 Linux 只有赞美之词，我们就不够诚实。我喜欢告诉人们我在三年内不得不重启四次的事情。
- 如果有人遇到了 Linux 可能解决的问题，提议提供相关信息的提示（网页、文章、书籍、顾问……）。如果你没有实际使用过建议的解决方案，请直说。
- 提议帮助他人开始使用 Linux。
- 尝试回答“网络帖子”卡住的情况。寻找那些棘手的问题，你可能是唯一回答的人，并且在这个过程中学到了东西。然而，如果你不确定自己能否给出正确答案，请找到可以的人。
- 寻找软件开发公司并提议进行演示。
- 参加如 NetDay96 (http://www.netday96.com) 等活动。虽然 Linux 是一个平台，但接触潜在的“客户”并推广（注意不要过度承诺）合适的 Linux 应用是至关重要的。我的公司的产品之所以在市场上表现良好，很大程度上不是因为产品技术上的优越性，而是因为公司的营销能力。
- 如果您使用 Linux 并希望为 Linux 社区做出贡献，请考虑采取本 mini-HOWTO 中的一个或多个想法，帮助他人通过 Linux 推广了解 Linux。

Linux 国际组织 (http://www.li.org/) 的目标是促进 Linux 的开发和使用。

Linux 文档项目 (http://sunsite.unc.edu/mdw/linux.html) 是 Linux 推广者的宝贵资源。

Linux 业务应用网站 (http://www.m-tech.ab.ca/linux-biz) 为那些依赖 Linux 进行日常业务运营的机构提供了一个分享经验的论坛。

Linux 推广项目 (http://1mb.com/linux/) 的目标是鼓励商业应用开发者为其软件提供原生的 Linux 版本。

Linux CD 支持赠送活动 (http://email.math.ucsb.edu:8000/giveaway.html) 正通过鼓励使用 Linux CD-ROM 让 Linux 更加普及可用。

Specialized Systems Consultants, Inc. (SSC) 出版了《Linux 杂志》(http://www.ssc.com/lj/) 以及在线时事通讯《Linux Gazette》(http://www.lg/)。

# 5 行为准则

- 作为 Linux 社区的代表，要表现专业。
- 克制人身攻击和使用粗俗语言。
- 始终考虑他人的观点。
- 避免毫无根据的指控。
- 不要理会挑衅（flame-bait）。
- 如果有人遇到了 Linux 可能解决的问题，提议提供相关信息的提示（网页、文章、书籍、顾问……）。如果你没有实际使用过建议的解决方案，请直说。
- 如果您使用 Linux 并希望为 Linux 社区做出贡献，请考虑采取本 mini-HOWTO 中的一个或多个想法，帮助他人通过 Linux 推广了解 Linux。

Linux 推广 mini-HOWTO 的作者是 Paul. Rogers <Paul.L.Rogers@li.org>。
- 欢迎提出意见和建议。
- 如果你需要更多关于 Linux 文档项目或 HOWTO 的信息，请随时联系主管 Greg Hanks <hregh@sumsite.unc.edu> 或每月关注几个国家和国际新闻组。

# 6 用户组

- 参与本地用户组。如果你所在的地区没有，请创建一个。Linux 用户组信息页 (http://www.ssc.com/glue/) 允许你搜索本地用户组，并包含了关于如何建立用户组的建议。
- 为对 Linux 感兴趣的机构提供演讲者。
- 向当地媒体发布关于你们活动的新闻稿。
- 自愿配置 Linux 系统以满足本地社区组织的需求。当然，安装过程必须包括对社区使用该系统的培训，以及用于持续维护的足够文档。

# 7 厂商关系

- 在考虑购买硬件时，询问厂商关于 Linux 的支持以及其他用户在 Linux 环境下的经验。
- 考虑支持销售 Linux 产品和服务的厂商。
- 支持那些将其部分收入捐赠给诸如以下机构的厂商。

# 1576 XLVII. PAUL L. ROGERS 编写的“LINUX 倡导迷你指南”

自由软件基金 (http://www.gnu.ai.mit.edu/)、Linux 开发补助基金 (http://www.li.org/About/Fund/Welcome.html)、XFree86 项目 (http://www.xfree86.org/donations.html) 或公共利益软件组织 (mailto:bruce@pixar.com)。

如果可能，请向这些或其他支持免费可用软件的组织进行个人捐赠。
- 如果你需要一个 Linux 不支持的应用程序，请联系供应商并请求原生 Linux 版本。

## 8 媒体关系

- Linux International 正在收集提到 Linux、GNU 或可自由分发软件的媒体剪报 (http://www.li.org/Products/Articles/Welcome.html)。当您看到相关文章时，请将以下信息发送至 clippings@li.org：
  - 出版名称
  - 出版者联系地址
  - 作者姓名
  - 作者联系地址
  - 文章标题
  - 文章开始的页码
  - 如果可以在网上找到，请提供 URL
  - 文章摘要，包括您的观点
- 如果您认为某篇文章、评论或新闻报道没有对 Linux 给予公平对待，请将细节及上述信息发送至 li@li.org，以便向出版者发送适当的回应。如果您直接联系出版者，请保持专业并确保事实属实。

## 9 致谢

诚心感谢所有贡献者，包括：
- Jon <maddog@zk3.digital.com>
- Greg Hanks <gegh@cc.gatech.edu>
- Eric Ladner <elandner@goldinc.com>
- Chie Nakatani <jeanne@mbox.kyoto-inet.or.jp>
- Nat Makarevitch <nat@nataa.fr.eu.org>
- Martin Michmayr <tbm@cyrius.com>
- Idan Shoham <idan@m-tech.ab.ca>
- Adam Spiers <adam.spiers@new.ox.ac.uk>
- C. J. Suisse <suire@datasync.com>
- Lars Wirzenius <liw@iki.fi>

# John A. Eikenberry 编写的“Linux & AI-Alife 迷你指南”

# 目录

- 1 引言 ................................................................................................ 1577
