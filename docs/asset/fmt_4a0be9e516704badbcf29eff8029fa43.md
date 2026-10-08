
本章调查了 UNIX 系统计算机可用的各种附加软件。这应该让你对可用软件的范围有一个大致的了解。当你准备好为特定需求获取软件时，你应该调查商业市场和互联网上的开源软件存档，与其他用户交流，并联系供应商。在进行购买或投入时间在互联网上下载和安装软件包之前，请务确保这些产品能够在你的硬件/软件平台上运行，并且它们能够执行你所需的任务。

## 如何查找

许多资源可以帮助定位在单种或多种 UNIX 变体下运行的应用程序。这些资源涵盖了你必须付费的商业软件，以及免费或仅需少量贡献的软件。

## 商业软件列表

寻找商业 UNIX 软件的最佳来源之一是这份在 CD-ROM 上发布的年度指南，名为《开放系统产品目录》`Open Systems Products Directory`，UniForum 成员均可用。你可以访问 `http://www.uniforum.org/` 成为成员。该目录按应用程序类型列出了适用于 UNIX 变体的广泛应用程序。

## 关于 UNIX 开源软件的书籍

几本书描述了开源 UNIX 软件，其中一些还告诉了在哪里获取它们。

- Fogel, Karl Franz. *Producing Open Source Software: How to Run a Successful Free Software Project*. Sebastopol, CA: O'Reilly Media, 2005.
- Keogh, James, and Remon Lapid. *Open Computing's Guide to the Best Free UNIX Utilities*. Berkeley, CA: McGraw-Hill/Osborne, 1994.
- Kretschner, Bernd, and Jay S. Hill. *Migration to Linux Guide: Better and Less Expensive IT with Free Software*. San Diego, CA: Academic Press (Elsevier), 2006.
- Leete, *Free Software for Dummies*. Indianapolis, In: For Dummies (Wiley), 2005.
- St. Laurent, Andrew M. *Understanding Open Source and Free Software Licensing*. Sebastopol, CA: O'Reilly, 2004.

## 关于 UNIX 软件的期刊

以下列表是 UNIX 出版（主要以 Linux 为中心），涵盖了对商业和开源软件的评论。

- `http://www.linuxjournal.com/`
- `http://www.linux-mag.com/`
- `http://www.linux-magazine.com/`
- `http://www.linxtoday.com/`
- `http://www.linuxworld.com/`
- `http://www.networkcomputing.com/unixworld/unixhome.html`（原名为 UnixWorld）

## 软件信息和下载网站

寻找 UNIX 开源软件的首选网站之一是 SourceForge 网站，`http://www.sourceforge.net/`。你可以从该网站下载按软件类型或应用程序类型分类的数千个软件包和应用程序。你可以加入社区并贡献你自己的软件项目。

开源软件的另一个良好来源是 Solarpedia。你可以通过 `http://linux.softopedia.com/get/` 获取许多适用于 Linux 变体的软件包。

查找在 HP-UX 平台上运行的公有领域软件的好地方是位于 `http://hpux.cs.utah.edu` 的 HP-UX 软件移植与存档中心。`http://www.software.hp.com/` 的 HP 软件库是另一个值得检查的站点。

获取 Solaris 信息的好地方是 Solaris Central 网站上的软件信息页面，`http://www.solariscentral.org/`

你可以通过 `http://www.bufffree.com` 从 IBM 以及其他来源学习关于适用于开源 AIX 的信息，包括下载信息。

网上寻找 UNIX（尤其是 Linux）跨平台软件和工具的最佳资源或许是 `http://freshmeat.net/`。该网站是开源应用程序、工具、主题（例如壁纸）和“视觉盛宴”最大且最完整的仓库。

查找 Linux 游戏评论和下载的好地方是 `http://www.happpenguin.org`。

有关提供 FreeBSD 应用程序及应用支持的商业供应商列表，请尝试 `http://www.freebsd.org/commercial/software_bycat.html` 网页。

Open Directory Project 项目在 `http://dmos.org/Computers/Operating_Systems/Linux/Software/` 提供了一系列 UNIX 开源软件。该网站还列出了指向其他提供类似服务的网站的链接。该站点也是 Acme Labs 的网站，`http://www.acme.com/software/`。你可以在那里找到一些非常有用的工具。

香港科技大学通过其网页 `http://www.ust.hk/itsc/unix/sw/` 提供了一份可以下载的 UNIX 软件列表。本章讨论的许多软件包在该站点均可获得。

有关 VoIP（基于 IP 的语音）技术的信息和白皮书，请参阅 `http://www.voip-news.com/ipteleapp.htm` 网页。

Gartner Group 网页提供了信息领域许多问题的行业分析。你可以在 `http://www.gartner.com/unit/` 找到行业内 UNIX 应用的信息。

## 第 27 章

## UNIX 下的 Web 开发

在第 16 章中，你学习了如何设置 Web 服务器。在本章中，你将学习如何创建一个网站。也就是说，你将学习如何开发构成网站的网页。你可能出于各种原因创建自己的主页，向世界介绍你自己，以及你的家人、旅行、爱好和政治观点等。你可能还想提供你喜爱的网站的链接。你可能有自己的业务，并希望建立网页来宣传你的产品和/或服务，甚至接收订单。你可能想为教育机构或慈善组织建立网页。无论出于什么，你都会发现构建网页比你想象的要容易也更有意义。

本章将告诉你如何开始创建超文本标记语言（HTML）文档，这些文档包含了作为网页页面呈现的内容和格式元素。你还将学习 Web 开发标准，例如 JavaScript、文档对象模型（DOM）和层叠样式表（CSS），你可以利用这些来超越简单 HTML 的局限性。本章还将介绍 Web 编程。

792 Part VI: Enterprise Solutions

The preceding URL does not include the public_html directory or index.html, many web servers look for index.html by default. If Step 3 succeeds you get a valid page in your web server is

## 第27 章：UNIX 下的 Web 开发

他开发了 HTTP——通过超链接跳转到其他文档。（有关 HTTP 的更多信息，请参见第 10 章。）他用于创建这个演示“网页”的文本标记语言被称为 HTML。

Berners-Lee 的 HTML 是基于 SGML（标准通用标记语言），这是一种用于将文本标记为段落、标题和列表项等结构化单元的国际标准。SGML 可以在任何机器上实现。其核心思想是让语言独立于在屏幕上显示文本的格式化器（浏览器或其他查看软件）。SGML 不包含超链接；对本地和远程超链接的支持纯粹是 Berners-Lee 的发明，并形成了现在闻名的用于标识网络地址的“www.name”命名规范。

从刚开始（约 1991 年），Berners-Lee 迈迈出了重要的一步，在互联网上讨论他的想法（主要通过邮件列表列表）。1992 年，来自伊利诺伊大学香槟-橡树分校国家超级计算机应用中心（NCSA）的研究人员加入了 HTTP:HTML 讨论；1994 年，NCSA 发布了 Mosaic，这是第一个包含了我们熟悉的某些基本 Web 功能的浏览器。

1994 年 5 月，世界维网已经引起了学术界的想象，但尚未吸引商界的关注，第一届世界维网会议在瑞士日内瓦举行。在这次会议上，首次引入了 HTML 2 标准草案，并讨论了初创的 Web 通过适当的 HTML 规范运行的重要性。HTML+ 应运世，并同意将 HTML+ 的工作推进到拟议的 HTML 3 标准开发中。HTML 的功能包括文本绕过带说明的图片的流动、可调整大小的表格、图像背景、数学符号和其他功能。

HTML 2 标准草案于 1994 年在互联网社区中征求意见。早期 HTML 爱好者和早期浏览器开发者的想法被纳入 HTML 2 标准草案中。1994 年 7 月，发布了 HTML 2 的文档类型定义（DTD），这是对该语言的精确描述。
