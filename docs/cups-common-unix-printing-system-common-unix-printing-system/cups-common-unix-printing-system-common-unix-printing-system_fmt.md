
# CUPS：通用 Unix 打印系统：打印系统与互联网打印协议权威指南（Sam 白皮书）

副出版商

Jeff Koch

策划编辑

Kathryn Purdum

开发编辑

Mark Renfrow

主编辑

Matt Purcell

项目编辑

George E. Neddeff

校对

Cynthia Fields

Margo Catts

Karen A. Gill

索引员

Larry Sweazy

校对员

Teresa Stephens

技术编辑

Tim Hicks

团队协调

Vicki Harding

室内设计

Gary Adair

封面设计

Alan Clements

页面布局

Lizbeth Patterson

    - 总结 ... 68

- Attribute 属性 ................................................................................ 179

- page-left 属性 ................................................................ 181

- page-right 属性 .............................................................. 181

    texttops 过滤器 ................................... 309

+ State ................................................................................................ 388

StateMessage .............................................................................. 388

| 配额 | 424 |

| 状态消息 | 425 |

## B IPP 参考 427

## C CUPS 常量 435

# 关于作者

Michael Sweet 是 Easy Software Products 的共同者，这是一家专门从事互联网和打印技术的小型软件公司。他在 6 岁时开始使用计算机终端，并在 12 岁时卖掉了自己的第一个程序。Michael 对打印和图形的痴迷使他开发了用于点矩阵打印机以及后来的喷墨打印机的图像打印软件。在从纽约州立理工学院尤蒂卡/罗马分校获得计算机科学学士学位后，他搬到了马里兰州，在海军从事实时图形方面的工作。

打印的魅力实在无法抗拒。在海军工作了几年后，Michael 再次开始编写打印驱动程序。在发布了一个名为“top”的免费软件后，他随后创立了 Easy Software Products 并开发了非常成功的 ESP Print 软件。1997 年，Michael 开始研究通用 UNIX 打印系统（CUPS），并在 1999 年，他的公司在 GNU GPL 许可证下发布了 CUPS，并将 ESP Print 作为商业产品发布。

除了编写打印驱动程序，Michael 还是几本书的作者或合著者，包括《POSIX 操作系统的串口编程指南》和《OpenGL 超圣》。在空闲时，他喜欢骑自行车、摄影、吹小号以及和他的妻子 Sandra 一起旅行。

# 关于技术编辑

Tim Hicks 是 HomeSide Lending, Inc. 的高级 Unix 工程师。他是 HP-UX 系统管理的 认证 IT 专业人员，并广泛使用 HP-UX 10.10-11.00，同时也参与过 Solaris 8、AIX 4.1、FreeBSD 和 RedHat 6.2 的相关工作。对于使用 HP MC/ServiceGuard、HP-UX 11.00 和 Oracle 8.05（以及 Sybase 11）的高可用集群，他拥有深入知识和经验。他目前正在实施 EMC Fabric 直接器和交换机的存储区域网络。Tim 毕业于佛罗里达州立大学，获得管理信息系统与金融学士学位。

# 献献

给 Sandra，我最好的朋友，我的挚爱。

# 致谢

写一本书并不是一件易事，需要奉献和牺牲才能实现这一切。如果没有我的妻子 Sandra 在我身边，这一切将不可能。多年来，她对我所的一切都给予了支持和鼓励，从未抱怨过我钻研技艺花费的长时间。我无法形容生命中拥有她我是多么幸运。有你，每一天都是新的、兴奋且令人清新的。

我作为计算机科学家的生活始于我的父母。感谢爸爸，在我 6 岁时把第一台终端带回家；感谢妈妈，忍受了餐桌旁那些计算机书籍。无论是乐高还是电脑，他们都给了我需要的一切。有这样如此爱的父母，我感到非常幸运。

我的朋友 Andy 和 Tammy 与我一起走过了经营计算机软件公司的艰难道路；感谢你们成为我的第二个家人。我认为如果没有我们的友谊，我们无法取得现在的成就。

Jim 指出我们的小打印驱动程序工具比另一个 3D 模型更重要。感谢 Jim 帮助我们看到全局（森林与树木）。

我想感谢 Carl Uno Barros，他是互联网打印协议（IPP）工作组的主席，也是那个在我耳边催促我为 IPP 编写打印协议的人。即使在 IPP 工作组参与者之间有时会发生激烈辩论，他稳健的手也帮助创建了一个让大家都能自豪地使用的网络打印协议。

我还要感谢 Sams Publishing 的同事们，他们看到了这本书的潜力。Katie Purdum 从一开始就与我合作，她的支持和热情让写作变成了一件乐事。我的项目编辑 George Nedeff 以及编辑 Marco Cato、Cynthia Fields、Tim Hicks 和 Mark Renflow 对书内容的一致性、准确性和可读性做出了巨大贡献。最后，我要感谢制作人员，他们将最终的文本、图像和图表转换成一本真正的书。投入其中的工作量令我惊叹。

CUPS 的出现如果没有开源社区的大许多贡献是不可能的。L. Peter Deutsch 开发了 CUPS 支持非 PostScript 打印机的 Ghostscript 软件，Derek Noonburg 开发了打印 PDF 文件的 Xpdf 软件。Crcher Dunnavant、Han Holl、Till Kamppetter、Sebastian Kahmer、Robert Krawitz、Johnny Lam、Jeff Licquia、Kurt Pfeifle、Klaus Singogel、Grant Taylor 等许多人对 CUPS 的成功和稳定做出了巨大贡献。

# 告诉我们你的想法！

作为本书的读者，你是我们最重要的评论家和我们。我们想知道我们哪里做得好，哪里可以做得更好，你希望我们出版哪些领域，以及你愿意分享的任何建议。

作为 Sams Publishing 的助理经理，我欢迎你的反馈。你可以通过传真、电子邮件或直接写信给我，告诉我们对这本书喜欢或不喜欢的地方——以及我们如何能让书籍更好。

请注意，我无法帮助你解决与本书相关的技术问题，由于我收到的邮件很多，我可能无法回复每条信息。

写作时，请务必注明书名和作者，以及你的姓名和电话或传真号码。我会仔细审阅你的意见，并与该书的作者和编辑分享。

## 引言

### Unix 打印历史

在人类历史初期，知识通过直接交流在人与人之间传递。在几千年里，这种传递从墙上的图画演变为石板、卷轴，最后变成了纸张。通信的进步驱动了技术和社会的变革。

在整个计算史上，打印通信在外围设备的发展中发挥了重要作用。在 Unix 早期，第一个杀手级应用是文字处理器，这并不意外。由于文字处理，律师、记者和科学家都需要进行通信，因此开发了行打印守护进程（"`LPD`”）来缓存并将打印文件发送到打印机。随后的 Unix 版本增加了一个新的行打印系统（"`LP`”），它与旧的 `LPD` 不兼容，但支持打印作业的选项。然而，自 Unix 诞生以来 30 多年来，Unix 打印几乎没有发生变化——应用程序产生输出，溢打印程序将文件发送到打印机。

### 个人电脑打印

当 IBM 个人电脑于 1981 年出现时，它复制了 Unix 的打印模型。应用程序带有某些流行打印机的功能，用户可以告诉应用程序使用哪些代码。如果你想在后台打印文件，可以使用 "`print`" 命令，可以在你处理其他事务时将文件缓存到磁盘。随着打印机开始支持图形，应用程序必须支持许多不同的字符集以及混合文本和图形。用于与打印机通信的软件复杂性开始与其自身竞争，不久后打印机驱动程序就成了一个独立的行业。

苹果发布的 Macintosh 改变了个人电脑上的打印方式。Macintosh 从一开始就被设计为一套桌面出版系统，它将打印接口从应用程序中抽象出来。应用程序只需要告诉打印系统要打印什么，打印系统就会将其翻译为所需的输出。有一段时间，Macintosh 统治了桌面出版市场。微软第一个 Windows 环境复制了这种范式，在 Windows 和 MacOS 中处理打印的方式几乎完全相同。这些操作系统的应用程序（如 NeXT 和 BeOS）能够通过通用接口产生专业级的输出，直到最近，Unix 才仅支持文件缓存。

### CUPS 的演进

1993 年，一家名为 Easy Software Products 的新公司成立了。作为创始人，我的工作是开发一个产生 3D 图像等的建模程序。在开发该程序时，我遇到了一个问题——我们如何通用地支持这些模型的打印？

Adobe PostScript 是一种用数学方法描述页面的计算机语言，也是大多数高端打印机的首选语言。PostScript 甚至用于 IRIX、NeXT 和 Solaris 操作系统的显示。然而，消费级打印机通常并不支持 PostScript，而且我们的办公室里显然没有 PostScript 解释器。当时，Ghostscript（一种流行的免费 PostScript 解释器）并不是选项，所以我们必须像之前的成千上万家公司那样编写自己的打印机驱动程序。

我以前为 Radio Shack Color 以及随后的操作系统编写过打印机驱动程序，所以我从那些旧程序中提取了代码，创建并公开发了 CUPS。CUPS 获取图像文件并将其转换为 HP 语言（PCL），适用于多种 HP 及兼容打印机。这结合 IRIX 操作系统提供的程序，足以为我们的建模器提供所需的打印支持。

有一天，我的朋友访问了我们的办公室，我向他展示了我们的程序。演示期间，他问我为什么试图为 IRIX 卖另一个 3D 建模程序，以及为什么不卖打印机驱动程序。“毕竟，”他说，“你们必须开发驱动程序，难道不认为其他人也需要它们吗？”

在这次讨论后不久，Silicon 发布了一款名为 Impression 的新打印产品。Impression 做了很多事情：引入了过滤文件将其转换为可读格式，它包含一个 PostScript 解释器以将 PostScript 文件转换为非 PostScript 打印机的光栅格式，并提供了一个可以用于为几乎任何类型的打印机开发驱动程序的通用接口。尽管有这些优点，Impression 缺乏打印机驱动程序。我们在 1994 年发布了第一个版本的 CUPS，到 1995 年我们停止了建模程序的开发，专门致力于 CUPS。CUPS 的新版本包含一个修改过的 Ghostscript 版本，它可以作为 Impression PostScript 解释器的无缝替换，并且随着新打印机的出现，我们继续添加打印机驱动程序。CUPS 最终移植到了 Solaris 和 HP-UX，每个操作系统都为这一复杂的软件架构增加了新的变化。

1997 年，我们开始考虑支持 Digital Unix 和 Linux 操作系统。遗憾的是，这些系统使用原始的 `LPD` 进行打印，因此你无法将选项传递给打印机驱动程序。单单这一点就会我们可能开发的任何程序瘫痪。更复杂的是，由于有三个版本的 `LPD` 共同使用且彼此之间并非 100% 兼容，我们知道必须采取下一步，同时替换 `LPD` 和 `LP`。

通用 Unix 打印系统（CUPS）最初的设计是基于 `LPD` 网络协议（见图 1）。我们增加了对选项和远程管理的支持，就在我们即将完成系统设计时，互联网打印协议（IPP）工作组成立了。IPP 工作组最初打算更新 `LPD` 网络协议，但很快改变了方向，创建一个功能更强、可扩展性更好的协议，可以根据需要进化以支持新技术。

切换到 IPP 使 CUPS 的发布延迟了约 18 个月，但我认为每个人都对此感到高兴。通过支持 IPP，CUPS 可以在任何地方接受和发送打印作业。CUPS 还提供了支持现代打印和打印机所需的设施，这是打印机制造商在 Unix 下支持其打印机所需要的内容。

![图 1：CUPS 的第一个设计备注。]

# 第一部分

### 使用 CUPS

- 1 CUPS 简介

- 2 编译与安装 CUPS

- 3 设置打印机和打印类

- 4 使用 CUPS 打印

- 5 服务器配置

- 6 客户端配置

## 第一章

### CUPS 简介

本章将介绍通用 Unix 打印系统（Common UNIX Printing System），简称 CUPS。

## 打印问题

多年来，打印问题一直困扰着 Unix。与 Microsoft Windows 或 Mac OS 不同，Unix 并没有标准的接口或系统来支持打印机。在目前提供的解决方案中，Berkeley 和 LPR 打印系统最为常见。

这些打印系统支持行式打印机（仅限文本）或 PostScript 打印机（文本和图形），经过某些调整，它们可以被用于支持广泛打印机和文件格式。然而，由于每个 Unix 操作系统系统的变体都使用不同的打印系统，为各种打印机和操作系统开发打印机驱动程序极其困难。再加上每个 Unix 变体的客户群有限，这迫使大多数供应商放弃了对 Unix 的支持。

CUPS 的设计是为了解决这个问题。所有 Unix 变体可以使用同一个通用的打印系统来满足用户的需求。打印机厂商可以利用其模块化接口开发单一驱动程序，以极小的努力支持多种格式。由于 CUPS 同时提供了 System V 和 Berkeley 打印命令，用户（以及应用程序）可以免费享受到这项技术的益处。自 1999 年首次发布以来，CUPS 已被许多 Linux 发行版采用，并被几家打印机制造商用于提供基于 CUPS 的 Linux 打印机驱动。

## 技术

CUPS 是适用于 Unix 和类 Unix 操作系统的打印系统。该系统允许将文件打印到你可以找到的任何打印机。CUPS 基于互联网打印协议（IPP），这是一种新的打印协议，允许你本地或远程打印到办公室或世界上任何地方的网络打印机。IPP 定义了打印的标准协议，以及作业管理和打印选项（如介质尺寸和分辨率）。

与其他协议一样，IPP 可以在本地使用，也可以通过互联网连接数百或数千英外的打印机。然而，与其他协议不同的是，IPP 还支持身份验证——保护你的打印机并访问控制——仅允许特定的机器或人员访问你的打印机。此外，IPP 支持加密——扰乱打印数据使窃听者无法理解——这使其比古老的 `LPD` 协议更加健壮、更安全。

IPP 建立在超文本传输协议（HTTP）之上，HTTP 是互联网 Web 服务器的基础。用户可以使用浏览器（见图 1.1）查看文档、检查打印机或服务器的状态信息，并管理他们的打印机、类和作业。

CUPS 提供了一个完整的基于 IPP 的打印系统，包括基础认证和摘要认证（Digest authentication）；基于用户或域的访问控制以及 128 位加密。CUPS 还提供了你可能已经使用了多年的标准打印命令。Berkeley (`lp`) 和 System V (`lp`) 命令都包含在内，因此使用这些命令的应用程序可以在无需更改的情况下运行。

## 客户端与服务器

IPP 基于客户端/服务器模型。客户端和服务器通常位于同一台机器上。当你打印一个文件时，你（或你的应用程序）就是客户端。服务器是运行在后台并打印该文件的 CUPS 程序（见图 1.2）。

## 作业

每个提交打印的文件或一组文件被称为一个“作业”（job）。作业通过从 1 开始的唯一数字进行标识，并分配给特定的目标（通常是打印机）。作业还可以关联相关选项，如介质尺寸、副本数量、优先级等。

## 类（Classes）

CUPS 支持称为“类”（classes）的打印机集合。发送到类的作业会被转发到类中下一个可用的打印机。这允许你将打印作业发送给一组相似（或相同）的打印机，并在第一个空闲的机器上打印，而不是等待你选定的打印机上的作业完成（见图 1.3）。

CUPS 还支持特殊的隐式类（implicit classes）。隐式类的工作原理类似于普通类，但当有多个服务器处理特定打印机时会自动创建。隐式类会将打印作业路由到下一个可用服务器，因此如果你的一个服务器宕机，你的作业仍然会被打印（见图 1.4）。

## 过滤器（Filters）

过滤器使用户或应用程序即使在打印机不支持的文件格式的情况下打印。发送到 CUPS 服务器的作业在发送到打印机之前会经过过滤。过滤器将作业文件转换为打印机可以理解的不同格式。另一些则执行页面选择和排序任务。第三种过滤器被称为打印机驱动程序，将在下一节描述。

CUPS 提供了打印多种类型图像文件、HP-GL/2 文件、PDF 文件和文本文件的过滤器。CUPS 还提供了 PostScript 和图像过滤器光栅图像处理器（RIP），它们可以将 PostScript 或图像文件转换为可以发送到光栅打印机驱动程序的位图（见图 1.5）。

## 打印机驱动

打印机驱动由特定于打印机的一个或多个过滤器组成。每个过滤器将通用文件格式（如位图）转换为打印机格式（如 HP-PCL）。除了过滤器程序，每个驱动程序还包含一个 PostScript 打印机描述（PPD）文件，描述打印机的功能、选项和能力。CUPS 包含了 EPSON、惠普等其他示例驱动。

CUPS 有许多商业和免费的打印机驱动，如表 1.1 所示。

| 表 1.1 用于 CUPS 的打印机驱动 | 来源 | URL | 类型 | 描述 |

| :--- | :--- | :--- | :--- | :--- |

| Easy Software Products | http://www.easysw.com | 商业 | 涵盖打印机厂商 |

| GIMP-print project | http://gimp-print.sourceforge.net | 免费 | 用于 GIMP、Ghostscript 的驱动程序 |



| CUPS-omatic | http://www.linuxprinting.org | 免费 | 用于 Ghostscript 的封装驱动程序 |

| EPSON | http://www.ercipd.com/isv/index.htm | 免费 | 驱动程序 |

| Star Micronics | http://www.starmronics.com | 免费 | 驱动程序 |

## 后端（Backends）

后端执行最重要的任务——将过滤数据发送到打印机（见图 1.6）。每个后端与打印机通信，将过滤后的数据（或原始打印文件）复制到打印机，并将打印机的任何状态信息转发到 CUPS 服务器。后端通常不对打印数据进行任何过滤或转换。

CUPS 提供了通过并行、串口和 USB 端口打印，以及通过 IPP、JetDirect (AppSocket) 和行打印守护进程 (LPD) 协议通过网络打印的后端。

后端还提供可用设备列表。启动时，会询问每个后端支持的设备列表以及任何可用信息。例如，并行后端可以告诉 CUPS 端口 1 上连接了一台 EPSON Stylus Color 600 打印机。

## 网络

本地系统上的打印机和类可以与网络上的其他系统共享。这允许将一个系统设置为所有其他系统的打印服务器或溢存主机。打印机通过向客户端广播可用打印机列表来实现共享（见图 1.7）。

# 第一部分 使用 CUPS

![](img/b159ac7fe2135643dc37ccfeef6d3980_42_0.png)

图 1.7

向客户端广播打印机列表的服务器。

通过这种方式，隐式类提供了一种平衡服务器负载的简单方法，并在一个或多个服务器故障时提供容错能力。

## 图形化界面

尽管 CUPS 没有附带标准的 GUI 界面，但有许多可用的界面。表 1.2 列出了可用的界面。

表 1.2 CUPS 的 GUI 界面

| URL | 软件包 |

| --- | --- |

| http://www.easysw.com/printpro/ | ESP Print Pro |

| http://www.std-uni-hannover.de/user/75439/gtklp/ | GtkLP |

| http://cups.sourceforge.net/cups/ | KUPS |

| http://cups.sourceforge.net/qtcups/ | QtCUPS |

| http://cups.sourceforge.net/xpp/ | XPP |

### ESP Print Pro

ESP Print Pro (见图 1.8) 是一个商业软件包。它提供了 GUI 来管理类、作业，以及一个用于设置选项和打印文件的打印面板；以及一个屏幕/窗口硬拷贝打印程序。ESP Print Pro 基于 FLTK 工具包。

![](img/b159ac7fe2135643dc37ccfeef6d3980_43_0.png)

图 1.8

使用 ESP Print Pro 打印机管理器、打印机向导 (Printer Wizard)、打印面板和打印机选项窗口管理打印机和作业。

### GtkLP

GtkLP (见图 1.9) 是一个免费软件，提供了 GUI 打印和选项面板来打印文件。GtkLP 基于 GTK+ 工具包。

### KUPS

用于 CUPS 的 KDE 管理工具 (KUPS) (见图 1.10) 是一个免费软件，提供了用于管理类、作业和打印机的 GUI。KUPS 基于 Qt 工具包。

![](img/b159ac7fe2135643dc37ccfeef6d3980_44_0.png)

图 1.9

使用 GtkLP 打印对话框打印。

![](img/b159ac7fe2135643dc37ccfeef6d3980_44_1.png)

图 1.10

使用 KUPS 打印机向导添加打印机。

### QtCUPS

QtCUPS (见图 1.11) 是一个免费软件，提供了用于打印文件的 GUI 和选项面板。QtCUPS 还提供了一个供 Qt 程序使用的库，用于直接通过 CUPS 支持打印。QtCUPS 基于 Qt 工具包。

![](img/b159ac7fe2135643dc37ccfeef6d3980_45_0.png)

> 图 1.11

使用 QtCUPS 打印对话框打印文件。

### XPP

X 打印面板 (XPP) (见图 1.12) 是一个免费软件，提供了用于打印文件的 GUI 和选项面板。XPP 基于 FLTK 工具包。

![](img/b159ac7fe2135643dc37ccfeef6d3980_46_0.png)

图 1.12

## 资源

CUPS 有许多可用资源，包括官方邮件列表、由 Easy Software Products 托管的新闻组以及网页。

### CUPS 邮件列表

`cups@cups.org` 邮件列表仅对订阅者开放，以避免垃圾邮件问题。向 `majordomo@cups.org` 发送消息以订阅该列表：

```
subscribe cups
```

列表管理器随后会发送一封确认邮件，你必须回复，最后你将收到如下消息：

欢迎加入 CUPS 邮件列表！

此邮件列表为讨论 Easy Software Products 的通用 Unix 打印系统 ("CUPS") 提供了一个公共论坛。CUPS 软件和文档请访问：

http://www.cups.org

向此列表发送消息，请向 "`cups@cups.org`" 发送电子邮件。

要从列表中取消，请向 "`majordomo@easysw.com`" 发送电子邮件，内容为：

```
unsubscribe: cups
```

请注意：如果服务器无法向你的电子邮件账户发送消息，你将自动从列表中取消订阅。如果你突然停止接收来自列表的消息，请重新订阅；如果你仍已订阅，将收到“已订阅 (already subscribed)” 消息。

CUPS 邮件列表是一个用于提问、讨论问题和报告漏洞的公共论坛。在发帖时请遵守网络礼仪。

### CUPS 新闻组

Easy Software Products 在以下地址托管了一个公共新闻服务器：

```
news://news.easysw.com/
```

与 CUPS 邮件列表不同，你不需要订阅即可访问这些资源。表 1.3 显示了可用的新闻组：

表 1.3 CUPS 新闻组

| 名称 | 说明 |

|---|---|

| cups.announce | CUPS 新版本发布及相关内容的公告 |

| cups.bugs | CUPS 漏洞的报告与讨论 |

| cups.cvs | 讨论 CVS 版本 CUPS 的问题 |

| cups.development | 讨论 CUPS 的开发者问题 |

| cups.general | 发布关于使用 CUPS 的通用问题 |

`cups.general` 新闻组通过 CUPS 邮件列表进行同步，反之亦然。

### 网站

有很多网站致力于介绍 CUPS。表 1.4 显示了常用的网站：

表 1.4 CUPS 相关网站

| URL | 说明 |

| --- | --- |

| http://www.cups.org/ | CUPS 官方网站 |

| http://www.linuxprinting.org/ | 关于 Linux 打印的优秀资源 |

| http://www.stokely.com/unix.resources/ | Unix 打印信息的来源 |

| http://www.pwg.org/ipp/ | 官方 IPP 网站 |

## 总结

CUPS 是基于 IPP 的 Unix 解决方案。CUPS 支持许多文件格式，并为 Linux 提供免费的商业打印驱动。

通过添加过滤器和后端，CUPS 可以扩展以支持新的格式、打印机和接口。

CUPS 提供了高级打印功能，包括基于 Web 的打印系统访问、打印共享、认证和加密。

# 第二章 编译与安装 CUPS

本章介绍了如何构建和安装 CUPS。如果你是从光盘或 CUPS 网站安装二进制发行版，请前往“安装二进制发行版”章节。

## 安装源码

本节描述了如何从源码在你的系统上编译 CUPS。

### 获取 CUPS 源码

CUPS 源码提供在附带的光盘中。对于典型的 Linux 系统，你需要运行以下命令访问源码：

```bash
mount /mnt/cdrom
tar xzvf /mnt/cdrom/cups-version-source.tar.gz
```

其中 `version` 是光盘上的 CUPS 版本。

最新的 CUPS 版本可以在网上获取：

```
http://www.cups.org
```

点击下载链接即可。

最后，你可以通过以下命令使用匿名 CVS 下载最新的边缘 CUPS 源码：

```bash
cvs -d:pserver:anoncvs@cv.cups.org:/home/anoncvs login
Password: anoncvs
cvs -z3 -d:pserver:anoncvs@cv.cups.org:/home/anoncvs get cups
```

处于 CUPS 开发的最前沿存在风险——CVS 版本可能不如正式发布版稳定。请谨慎使用 CVS  CUPS。

### 要求

在系统上构建 CUPS，你需要符合 ANSI 标准的 C 和 C++ 编译器。正如其名称所示的，CUPS 设计在 Unix 操作系统上运行；但是，CUPS 接口库以及大多数过滤器和后端在 Microsoft Windows 下也可以编译和运行。

表 2.1 列出了编译和安装 CUPS 所需的库和软件包。

### 表 2.1 CUPS 需要的库和软件包

| 名称 | 是否需要 | URL | 描述 |

| :--- | :--- | :--- | :--- |

| EPM | 否 | http://www.easysw.com/epm/ | EPM 软件用于在所有支持的平台上创建二进制发行版。 |

| GCC | 否 | http://gcc.gnu.org/ | GCC 软件为 Unix 提供编译器，包括优秀的符合 ANSI 的 C 和 C++ 编译器。 |

| GROFF | 是 | ftp://ftp.gnu.org/gnu/groff/ | groff 软件用于页面格式化；如果你的系统已有了该程序，也可以直接使用。 |

| HTMLDOC | 否 | http://www.easysw.com/htmldoc/ | HTMLDOC 软件用于格式化 CUPS 文档。 |

| JPEG | 是 | http://www.ijg.org/ | JPEG 库支持 JPEG 图像文件、PostScript 文件中的 JPEG 压缩图像以及 TIFF 文件中的 JPEG 压缩数据。 |

| OPENSLP | 否 | http://www.openslp.org/ | OpenSLP 库为 CUPS 提供 SLPv2 支持。 |

| OPENSSL | 否 | http://www.openssl.org/ | OpenSSL 库为 CUPS 提供 128 位的 TLS 和 SSL 加密支持。 |

| PNG | 是 | http://www.libpng.org/ | PNG 库支持 PNG 图像文件。 |

| TIFF | 是 | http://www.libtiff.org/ | TIFF 库支持 TIFF 图像。 |

| ZLIB | 是 | http://www.infozip.org/pub/infozip/zlib/ | ZLIB 库支持 PNG 和 TIFF 图像文件的压缩。 |

### 配置 CUPS 源码

CUPS 使用 GNU autoconf 为你的系统配置 Makefile 和源代码。

输入以下命令为你的系统配置 CUPS：

```
./configure
```

`configure` 脚本接受多个选项。如果你想带有多个选项配置 CUPS，请将它们全部写在同一行中，如下：

```
./configure --prefix=/some/directory --enable-debug --disable-shared ...
```

### 配置安装目录

默认安装会将 CUPS 软件放在系统上的 `/etc`、`/usr` 和 `/var` 目录中，这将覆盖系统中现有的任何打印命令。

使用 `--prefix` 将 CUPS 软件安装在另一个位置：

```
./configure --prefix=some/directory
```

`--prefix` 选项影响所有文件的位置。使用表 2.2 中的一个或多个选项来覆盖由 `--prefix` 分配的位置。

### 表 2.2 Configure 脚本的目录选项

| 选项 | 描述 | 默认值 | 前缀值 |

| :--- | :--- | :--- | :--- |

| --datadir | 共享数据文件的位置 | /usr/share | ${prefix}/share |

| --exec-prefix | 可执行文件的基础目录 | /usr | ${prefix} |

| --includedir | 包含文件的基础目录 | /usr/include | ${prefix}/include |

| --libdir | 库文件的位置 | /usr/lib | ${prefix}/lib |

| --libexecdir | 服务器可执行文件的位置 | /usr/lib, /usr/libexec | ${prefix}/libexec |

| --localstatedir | 本地状态信息的基础目录 | /var | ${prefix}/var |

| --mandir | 手帮助页的基础目录 | /usr/man, /usr/share/man, /usr/share/catman/u_man | ${prefix}/man |

| --sysconfdir | 本地配置文件的基础目录 | /etc | ${prefix}/etc |

一个典型的本地安装可能会将 CUPS 程序、库和数据文件放在 `/usr/local` 下，将配置文件放在 `/etc`，将状态文件放在 `/var`。以下命令将提供这种配置：

```
./configure --prefix=/usr/local --sysconfdir=/etc --localstatedir=/var
```

## 查找头文件

`configure` 脚本通常只在系统位置查找头文件和库，通常为 `/usr/include` 和 `/usr/lib`。要在其他目录配置脚本，请设置 `CFLAGS`、`CXXFLAGS` 和 `LDFLAGS` 环境变量。如果你使用 Bourne shell 或定义命令如下：

```bash
CFLAGS="-I /usr/include -I/bar/include"; export CFLAGS
CXXFLAGS="-I /usr/include -I/bar/include"; export CXXFLAGS
LDFLAGS="-L /usr/bar/lib -L/bar/lib"; export LDFLAGS
```

如果你使用 C shell 或定义命令如下：

```c
setenv CFLAGS="-I /usr/bar/include -I/bar/include"
setenv CXXFLAGS="-I /usr/bar/include -I/bar/include"
setenv LDFLAGS="-L /usr/bar/lib -L/bar/lib"
```

`-I` 选项告诉编译器去哪些目录查找包含文件；这些选项是累积的，并且会在搜索标准目录之前进行搜索。

`-L` 选项告诉链接器去哪些目录查找库文件；这些选项是累积的，并且会在搜索标准目录之前进行搜索。

## 查找字体文件

CUPS 拥有一套用于 PostScript RIP 和文本过滤器的 Type1 字体。然而，许多系统已经安装了这些字体，你可能还有想要使用的额外 Type1 或 TrueType 字体。`-fontpath` 选项允许你指定 CUPS 应该查找哪些字体。前面的示例显示冒号（:）分隔目录。

```
./configure --fontpath=/usr/share/fonts
```

## 编译调试

`--enable-debug` 选项会将调试信息包含在 CUPS 中。输入以下命令进行调试配置：

```
./configure --enable-debug
```

## 启用通知支持

`--enable-notifications` 选项允许在任务完成后通知你。输入以下命令进行配置：

```
./configure --enable-notifications
```

## 构建静态库

`--disable-shared` 选项防止创建共享库。输入以下命令配置静态库：

```
./configure --disable-shared
```

## 启用服务器位置支持

`--enable-slp` 选项会将位置协议代码链接到 CUPS。该选项用于发现打印机并提供网络服务。输入以下命令配置 SLP 支持：

```
./configure --enable-slp
```

## 启用加密支持

`--enable-ssl` 选项会将加密代码链接到 CUPS。该选项允许你加密打印任务。输入以下命令配置加密支持：

```bash
./configure --enable-ssl
```

## 启用所有可选功能

提供的 CUPS 二进制发行包含了所有的可选功能。输入以下命令配置所有可用的：

```bash
./configure --enable-notifications --enable-ssl --enable-slp
```

## 配置选项总结

表 2.3 列出了 `configure` 脚本的所有配置选项。

| 选项 | 描述 | 默认值 |

| :--- | :--- | :--- |

| --datadir | 共享数据文件的位置 | /usr/share |

| --disable-debug | 启用或禁用调试 | 禁用 |

| --enable-debug | 启用通知支持 | CUPS 1.1x 中禁用，1.2 中启用 |

| --disable-notifications | 启用或禁用共享库 | 启用 |



| `--enable-notifications` | 启用或禁用 SSL 支持 | 启用 |
| `--disable-shared` | 启用或禁用 SSL 支持 | 启用 |
| `--enable-shared-slp` | 可执行文件的基础目录 | `/usr` |
| `--disable-ssl` | 字体搜索路径 | `/usr/share/fonts` |
| `--enable-ssl` | 包含文件的基础目录 | `/usr/include` |
| `--exec-prefix` | 库文件的位置 | `/usr/lib` |
| `--fontpath=/dir1:/dir2` | 服务器可执行文件的位置 | `/usr/lib,libexec` |
| `--included` | 本地状态信息的基础目录 | `/var` |
| `--libdir` | 手帮助页的基础目录 | `/usr/man, /usr/share/man` |
| `--localstatdir` | 本地配置文件的基础目录 | `/etc` |

30

# 第一部分

# 使用 CUPS

## 测试软件

在成功编译后，通常在安装之前测试软件是一个好主意。`test` 目标提供了 CUPS 软件的自动化测试：

```
make test
Running CUPS test suite...
Linking ipptest...
Starting scheduler...
Waiting for scheduler to become ready...
Running JIPP compliance tests...
Performing 4.1-requests.test...
Performing 4.2-cups-printer-ops.test...
Performing 4.3-job-obs.test...
Running command tests...
Performing 5.1-lpadmin.sh...
Performing 5.2-lpc.sh...
Performing 5.3-lpq.sh...
Performing 5.4-lpstat.sh...
Performing 5.5-lp.sh...
Performing 5.6-lpr.sh...
Performing 5.7-lrm.sh...
Performing 5.8-cancel.sh...
Performing 5.9-lpinfo.sh...
Formatting reports...
htmldoc: Reading cups-str-1.1-2001-03-03-mike.shtml
htmldoc: Reading cups-str-1.1-2001-03-03-mike.shtml
```

测试通过后。

详细信息请参考以下文件：

```
cups-str-1.1-2001-03-03-mike.html
cups-str-1.1-2001-03-03-mike.pdf
```

如果您遇到任何错误，请使用第 1 章“CUPS 简介”中描述的资源获取帮助。

## 安装软件

使用 `install` 目标将软件安装到您配置软件时选择的目录中：

```
make install
```

## 警告

安装 CUPS 通常会覆盖您现有的打印系统。如果您在使用 CUPS 软件时遇到困难并需要返回旧的打印系统，您将需要从操作系统的 CD 中重新安装旧的打印系统。

## 升级软件

`install` 目标会保留您现有的 CUPS 配置文件，因此它也可以用于升级软件：

```
make install
```

## 运行软件

安装软件后，可以通过输入以下命令启动 CUPS 服务：

```
/usr/sbin/cupsd
```

恭喜您，您已经完成了 CUPS 的安装！您现在可以进入第 3 章“设置打印机和类”。

## 安装二进制分发版

CUPS 提供多种二进制分发格式。Easy Software Products 提供 TAR 格式的二进制文件（带有安装和删除脚本的“便携式”发行），以及适用于 Red Hat 和基于 Debian 的发行版的 RPM 和 DPKG 格式。便携版适用于所有平台，而 RPM 和 DPKG 发行版仅适用于 Linux。

## 警告

CUPS 将覆盖您现有的打印系统。如果您在使用 CUPS 软件时遇到困难并需要返回旧的打印系统，您必须使用提供的脚本删除 CUPS 软件和/或从操作系统的 CD 中重新安装旧的打印系统。

## 获取 CUPS 二进制分发版

CUPS 的二进制分发版通过附的 CD-ROM 提供。对于典型的 Linux 系统，您需要运行以下命令来访问二进制分发版：

### 使用 CUPS

```
mount /mnt/cdrom
cd /mnt/cdrom/cups
```

最新的 CUPS 版本始终在线可用：

http://www.cups.org

点击 Download 链接访问二进制分发版。

## 安装或升级便携版分发

要从便携版分发中安装或升级 CUPS 软件，您需要以 root 用户登录或执行 `su`：

```
su
```

运行安装脚本来安装或升级 CUPS：

```
./cups.install
```

Copyright 1993-2001 by Easy Software Products, 版所有。

此安装脚本将在您的系统上安装版本为 1.1.7 的通用 UNIX 打印系统软件。

要继续吗？yes

通用 UNIX 打印系统许可协议

> Copyright 1997-2001 by Easy Software Products

您同意此许可的条款吗？yes

正在备份待安装的非共享文件旧版本...

正在备份待安装的共享文件旧版本...

正在创建安装目录...

正在安装软件...

正在检查配置文件...

正在设置初始化脚本...

cups: scheduler started.

安装完成。

在对两个问题回答 yes 后，CUPS 软件将被安装或升级，调度程序将自动启动。如果您正在升级软件，将自动使用您之前的配置文件。

您现在可以继续第 3 章。

## 安装 RPM 分发版

要从便携版分发中安装 CUPS 软件，您需要以 root 用户登录或执行 `su`：

```
su
```

如果您是首次安装 CUPS，首先需要移除现有的打印系统。从移除任何 Red Hat 打印实用程序开始：

```
rpm -e rhs-printfilters
```

```
rpm -e printool
```

如果您在删除过程中遇到任何冲突，请也同时删除冲突的软件。

接下来，移除 lpr 或 LPR 软件。使用以下命令移除 lpr 软件：

```
rpm -e lpr
```

如果您安装的是 LPRng 软件，请输入：

```
rpm -e LPRng
```

再次，如果您在删除过程中遇到任何冲突，请也同时删除冲突的软件。

然后使用以下命令安装 CUPS rpm：

```
rpm -i cups-version-linux-2.2-intel.rpm
```

或者

```
rpm -i cups-version-linux-2.4-intel.rpm
```

其中 `version` 是 CUPS 的版本号。稍等后，CUPS 软件将完成安装。唯一的任务是启动 CUPS 服务：

```
/usr/sbin/cupsd
```

恭喜您，您已经完成了 CUPS 的安装！您现在可以进入第 3 章。

## 升级之前的 CUPS 安装

RPM 升级程序与便携版升级程序非常相似。使用以下命令升级 CUPS rpm：

```
rpm -U cups-version-linux-2.2-intel.rpm
```

### 使用 CUPS

或者

```
rpm -U cups-version-linux-2.4-intel.rpm
```

其中 `version` 是 CUPS 的版本号。稍等后，CUPS 软件将完成升级。

`rpm` 软件会保存您的配置文件。输入以下命令恢复它们：

```
cd /etc/cups
mv classes.conf.rpave classes.conf
mv cupsd.conf.rpave cupsd.conf
mv printers.conf.rpave printers.conf
```

最后，使用命令启动 CUPS 服务：

```
/usr/sbin/cupsd
```

恭喜您，您已经完成了 CUPS 的升级！您现在可以进入第 3 章。

## 安装 Debian 分发版

要从便携版分发中安装或升级 CUPS 软件，您需要以 root 用户登录或执行 `su`：

```
su
```

如果您是首次安装 CUPS，首先需要移除现有的打印系统。从移除 lpr 软件开始：

```
dselect remove lpr
```

如果您在删除过程中遇到任何冲突，请也同时删除冲突的软件。然后使用以下命令安装 CUPS 包：

```
dselect install cups-version-linux-2.2-intel.deb
```

或者

```
dselect install cups-version-linux-2.4-intel.deb
```

其中 `version` 是 CUPS 的版本号。稍等后，CUPS 软件将完成安装。

## 升级 CUPS

Debian 软件包器使用 `install` 命令自动处理升级。使用以下命令升级 CUPS 包：

```
dselect install cups-version-linux-2.2-intel.deb
```

或者

```
dselect install cups-version-linux-2.4-intel.deb
```

## 总结

CUPS 以源代码和二进制格式提供。您可以从书中附带的 CD-ROM 安装 CUPS 软件，也可以从 CUPS 网站或匿名 CVS 服务器下载。

在升级 CUPS 软件时，会自动会自动保留。如果您使用 RPM 包进行升级，请确保恢复 `rpm` 命令创建的备份配置文件。

# 第3 章

## 设置打印机和类

本章描述了如何通过命令行和 Web 界面在系统中设置和管理打印机以及类。

### 打印机基础

每个打印机队列都有一个关联的名称；打印机名称必须以字母开头，最多包含 127 个字母、数字和下划线 `_`。不区分大小写，`PRINTER`、`Printer` 和 `printer` 都被视为同一个名称。

### 打印机设备

打印机队列关联有一个设备。该设备可以是并行端口、网络接口或后端支持的任何接口。CUPS 内部的设备使用统一资源标识符（`URI`），它们比 Web 浏览器中使用的统一资源定位符（`URL`）更具通用。例如，Linux 中的第一个并行端口通常使用 `parallel:/dev/lp0` 作为 URI。

### 获取可用设备列表

你可以通过运行 `lpinfo` 命令查看支持的设备完整列表：

```
lpinfo -v
file file
network socket
network http
network ipp
network lpd
direct parallel:/dev/lp0
serial parallel:/dev/ttyS0baud=115200
serial serial:/dev/ttyS1baud=115200
direct usb:/dev/usb/lp0
network smb
```

`-v` 选项指定你想要可用设备的列表。每行的第一个单词是设备类型（direct、file、network 或 serial），后面跟着该设备的 URI 或名称。文件设备使用 `file:/directory/filename` 格式的 URI，而网络设备使用更熟悉的 `scheme://server` 或 `scheme://server/path` 格式。

某些后端支持选项，这些选项以问号开头添加在 URI 的末尾。在前面的设备列表中，串口 URI 上的 `baud=115200` 指定了该端口支持的最大波特率。其他选项可以指定奇偶校验、数据位和流控。

### 文件设备

文件设备允许你配置打印机打印文件以进行测试，或者盲目地将文件打印到设备或命名管道。文件的绝对路径被附加到 `file:` 方案名称之后，形成设备 URI：

```
file://foo/bar/filename.prn
```

文件设备不支持任何选项。

注意：

文件设备目前被实现为 CUPS 内部的一个设备。这阻止了你将原始文件打印到打印机，因为没有过滤器实际将打印作业复制到文件中。

此外，文件设备会覆盖命名文件。由于调度程序通常以 root 身份运行，你必须小心不要配置指向 `/etc/passwd` 等重要文件的打印机。

### HTTP 和 IPP 设备

HTTP 和 IPP URI 允许将打印作业发送到支持 IPP 的打印机或服务器。HTTP 设备处理方案名为 `http:` 的 URI，而 IPP 设备处理方案名为 `ipp:` 的 URI。这些设备在设备 URI 中不支持任何选项，但打印作业选项将以极小或无更改地传递给远程设备。

如果远程设备需要身份验证，你可以在设备 URI 中嵌入用户名和密码：

```
http://username:password@server/path
ipp://username:password@server/path
```

CUPS 服务器支持以下 URI 的打印机：

```
http://server/printers/name
http://server:port/printers/name
ipp://server/printers/name
ipp://server:port/printers/name
```

其中 `name` 是打印机名称。同样，类（classes）使用以下 URI：

```
http://server/classes/name
http://server:port/classes/name
ipp://server/classes/name
ipp://server:port/classes/name
```

带有网络接口和外部网络打印服务器的打印机使用不同的 URI。表 3.1 汇总了常用的 URI：

### 表 3.1 网络打印机和打印服务器的常用 URI

| 制造商 | URI |
| :--- | :--- |
| Axis | `pp://server/LPT1` (Parallel 1)<br>`pp://server/LPT2` (Parallel 2)<br>`pp://server/COM1` (Serial 1) |
| HP | `pp://server/ipp` (Internal)<br>`pp://server/ipp/port1` (Parallel 1)<br>`pp://server/ipp/port2` (Parallel 2)<br>`pp://server/ipp/port3` (Parallel 3) |
| Microsoft | `pp://server/printers/name` |
| Tektonix | `pp://server/ipp` |
| Xerox | `pp://server/ipp` |

使用 Microsoft Windows 2000 IPP 服务器时，URI 中的 `name` 是打印机的共享名称。

如果你在表 3.1 中没有看到你的制造商，请咨询随打印机或打印服务器附带的文档。

### LPD 设备

LPD 设备支持旧的打印机守护进程协议，该协议在 RFC 1179 中描述。Microsoft 在 TCP/IP 打印服务实现了该协议。

```
lpd://server/name
```

*其中 `name`* 是远程打印机队列的名称。Windows NT 服务器上的打印机队列将将打印机的共享名称。对于网络接口和打印服务器，请参考表 3.2。

### 表 3.2 LPD 打印机和打印服务器的常用 URI

| 制造商 | URI |
| :--- | :--- |
| Apple | `lpd://server/name` |
| Axis | `lpd://server/LPT1` (Parallel 1)<br>`lpd://server/LPT2` (Parallel 2)<br>`lpd://server/COM1` (Serial 1) |
| Castelle | `lpd://server/name` |
| DPI | `lpd://server/name` |
| EFI | `lpd://server/name` |
| Extended | `lpd://server/name` |
| HP | `lpd://server/name` |
| Hewlett Packard | `lpd://server/name` |
| Intel | `lpd://server/name` |
| Kodak | `lpd://server/name` |
| Lexmark | `lpd://server/name` |
| Linksys | `lpd://server/name` |
| Microsoft | `lpd://server/name` |
| QMS | `lpd://server/name` |
| Sun | `lpd://server/name` |
| System | `lpd://server/name` |
| Xerox | `lpd://server/name` |

LPD 设备还支持若干选项，如表 3.3 所示。

### 表 3.3 LPD 选项

| 选项 | 说明 |
| :--- | :--- |
| `banner=no` | 告诉远程打印机不要打印页（默认） |
| `banner=yes` | 告诉远程打印机打印页 |
| `format=c` | 告诉远程打印机打印文件是加州科技中间格式 (CIF) |
| `format=d` | 告诉远程打印机打印文件是 TeX dvi 格式 |
| `format=f` | 告诉远程打印机打印文件是文本文件 |
| `format=g` | 告诉远程打印机打印文件是伯克利绘图文件 |
| `format=l` | 告诉远程打印机打印文件已经针对打印机格式化（默认） |
| `order=control,data` | 先将控制文件发送到远程打印机 |



| order=data,control | 先将控制文件发送到远程打印机（默认） |

# 设置打印机与类 第 3 章

`serial://dev/ttyS0`

`serial://dev/serial/0`

串口后端支持多种选项，如表 3.4 所示：

### 表 3.4 串口设备选项

| 选项 | 描述 |
| :--- | :--- |
| baud=N | 设置串口波率为每秒比特数（波特）。默认值通常为 9,600 波特。最大值由 `ipinto` 命令报告。 |
| bits=7 | 将每个字符的数据位数设置为 7 位。 |
| bits=8 | 将每个字符的数据位数设置为 8 位（默认）。 |
| flow=rtcts | 设置流控制为使用请求发送（RTS）和清除发送（CTS）信号线。 |
| flow=dtrsr | 设置流控制为使用数据终端就绪（DTR）和数据设置就绪（DSR）信号线。 |
| flow=hard | 设置流控制为使用请求发送（RTS）和清除发送（CTS）信号线。 |
| flow=none | 完全禁用流控制（默认）。 |
| flow=soft | 使用 XON 和 XOFF 字符进行流控制；这种方法在打印机上通常不可靠。 |
| parity=even | 每个字符发送奇偶性校验；所有比特位之和的结果必须为偶数。 |
| parity=none | 不发送奇偶性校验（默认）。 |
| parity=odd | 每个字符发送奇偶性校验；所有比特位之和的结果必须为奇数。 |

在端口 1 上运行、波特率为 19200、使用 7 位数据位、偶校验校验以及 DTE-DSR 流控制的打印机需要以下设备 URI：

```
serial://dev/ttyS0baud=19200+bits=7+parity=even+flow=dtedsr
```

由于串口端口与其他接口相比非常慢，它通常作为最后的选择，或用于向针式打印机打印文本。

### SMB 设备

SMB 设备支持使用 SMB 协议打印到 Windows 打印机，由 SAMBA 软件提供。SMB 打印机的 URI 如下：

```
smb:////workgroup/server/name
```

### 使用 CUPS

其中 `workgroup` 是服务器所属的工作组名称，`server` 是服务器的 NetBIOS 名称，`name` 是打印机的共享名称。对于工作组 "ESP" 中服务器 "foo" 上的名为 "bar" 的打印机，其 URI 为：

```
smb://ESP/foo/bar
```

如果共享打印机需要用户名和密码（通常从 Windows NT 或 2000 服务器共享的打印机都是如此），可以在 URI 中提供：

```
smb://username:password@workgroup/server/name
```

## 注意

由于在 URI 中包含用户名和密码可能存在安全问题，你可能希望改用 Windows NT 提供的 TCP/IP 打印服务或 Windows 2000 提供的 IPP 打印服务。

这些服务的额外益处是将正确的用户名与打印作业关联，因为 `sm` 后端只能发送你在 URI 中提供的用户名。

### Socket 设备

`socket` 设备支持使用 TCP/IP 套接字进行直接打印，通常称为 AppSocket 打印或 JetDirect 协议。设备 URI 只需要服务器名称以及可选的端口号：

```
socket://server
```

```
socket://server:port
```

默认端口号为 9100，所有 HP JetDirect 接口和许多其他网络打印机均使用它。表 3.5 显示了各种设备使用的端口号：

### 表 3.5 Socket 设备的 URI

| 制造商 | URI |
| :--- | :--- |
| Axis | `socket://server:9100` (Parallel 1) <br> `socket://server:9101` (Parallel 2) <br> `socket://server:9102` (Parallel 3) |
| EPSON | `socket://server` |
| Hewlett Packard | `socket://server` (Internal) <br> `socket://server:9100` (Parallel 1) <br> `socket://server:9101` (Parallel 2) <br> `socket://server:9102` (Parallel 3) |
| Lexmark | `socket://server:5503` |

### 表 3.5 续

| 制造商 | URI |
| :--- | :--- |
| Linksys | `socket://server:4010` (Parallel 1) <br> `socket://server:4020` (Parallel 2) <br> `socket://server:4030` (Parallel 3) |
| NETGEAR | `socket://server:4010` (Parallel 1) <br> `socket://server:4020` (Parallel 2) <br> `socket://server:4030` (Parallel 3) |
| Tektronix | `socket://server` |
| XEROX | `socket://server:5503` |

`socket` 设备是网络打印机或服务器支持的性能最好且最可靠的设备。`socket` 设备还可以将打印数据流到打印机，而其他网络设备在发送到打印机之前需要将打印数据存储在临时文件中。

### USB 设备

USB 设备支持通过通用总线（USB）打印。USB 目前适用于 Linux 和 PC BSD 操作系统。USB 打印机的设备 URI 差异很大，即使在 Linux 发行版之间也是如此，例如

```
usb://dev/bus/usb/001/002
usb://dev/bus/usb/n/n
```

其中 `n` 是 USB 端口号。对于 USB 打印机，`n` 是动态分配的。注意：USB 打印机不支持流控制。

## 打印机驱动

CUPS 打印机使用 PPD（打印描述文件）来配置打印机。CUPS 包含 PPD 文件。对于 CUPS 提供的 PPD 文件，在表 3.6 中列出了这些文件。

PPD 文件通常位于 `/usr/share/cups/ppd/`。



其中 `n` 是 USB 端口号。对于 USB 打印机，`n` 是动态分配的。注意：USB 打印机不支持流控制。

同样，使用 IP 地址为 `11.22.33.44` 的 JetDirect 网络接口的 HP LaserJet 打印机可以通过以下命令添加：

```
/usr/sbin/lpadmin -p LaserJet -E -v socket://11.22.33.44 -m laserjet.ppd ENTER
```

## 从命令行配置打印机

添加打印机后，您应该配置打印机的默认选项。`-o` 用于为打印机选择特定选项：

```
lpadmin -p name -o option=value ENTER
```

选项名称可以是 PPD 文件列出的任何选项，或者是第 4 章“使用 CUPS 打印”中描述的 IP 标准选项名称之一。

现在使用以下命令为打印机配置默认介质和分辨率：

```
lpadmin -p name -o media=letter -o resolution=600dpi ENTER
```

这将默认介质尺寸设置为 `letter`（8.5x11 英寸），分辨率设置为 `600 dpi`，适用于较新的惠尔普打印打印机。表 3.8 列出了每个 CUPS 驱动支持的介质和分辨率值。

### 表 3.8 支持的介质和分辨率值

| 打印机驱动 | 支持的介质 | 支持的分辨率 |
|---|---|---|
| EPSON 9针系列 | letter, a4, fanfold | 60dpi, 120dpi, 180dpi |
| EPSON 24针系列 | letter, a4, fanfold | 60dpi, 120dpi, 180dpi, 360x180dpi, 360dpi |
| EPSON Stylus Color | letter, tabloid, a3 | 180dpi, 360dpi, 720dpi |
| EPSON Stylus Photo | letter, tabloid, a4, a3 | 180dpi, 360dpi, 720dpi |
| HP DeskJet 系列 | letter, tabloid, a3 | 150dpi, 300dpi, 600dpi |
| HP LaserJet 系列 | letter, tabloid, a3 | 150dpi, 300dpi, 600dpi |
| Okidaka 9针系列 | letter, a4, fanfold | 60dpi, 120dpi, 240dpi |
| Okidaka 24针系列 | letter, a4, fanfold | 60dpi, 120dpi, 180dpi, 360x180dpi, 360dpi |

`loptions` 命令将列出驱动程序支持的选项和值：

```
loptions -p name -l ENTER
```

最后，`job-sheets-default` 选项指定打印文件时使用的横页：

```
lpadmin -p name -o job-sheets-default=standard ENTER
```

CUPS 包含 7 种不同的横页。表 3.9 列出了标准横页。

### 表 3.9 CUPS 提供的横页

| 名称 | 描述 |
| --- | --- |
| none | 无横页（默认） |
| classified | 标准横页，页面顶部和底部有“Classified”（机密/分类）字样 |
| confidential | 标准横页，页面顶部和底部有“Confidential”（机密）字样 |
| secret | 标准横页，页面顶部和底部有“Secret”（秘密）字样 |
| standard | 单页页，显示作业标题、用户名和日期 |
| topsecret | 标准横页，页面顶部和底部有“Top Secret”（绝密）字样 |
| unclassified | 标准横页，页面顶部和底部有“Unclassified”（非密）字样 |

恭喜，您现在准备好打印了！

## 从 Web 添加您的第一台打印机

CUPS 服务器提供了一个友好的界面，供您通过浏览器添加打印机。您无需研究使用哪种设备 URI 和 PPD 文件，只需点击相应的列表并填写一些简单信息即可。

在浏览器中打开以下 URL 开始：

```
http://localhost:631/admin
```

点击 `Add Printer`（添加打印机）按钮显示打印机向导的第一页（见图 3.1）。

在相应的文本字段中输入打印机名称、位置和描述。正如本章前面提到的，打印机名称最多可 127 个字符。打印位置和描述字段可以包含任何普通文本，包括空格。

点击 `Continue`（继续）按钮显示打印机向导的下一页（见图 3.2）。

从列表中选择设备并点击 `Continue` 按钮。如果您选择了网络设备，将出现 URI 页面（见图 3.3）。

输入打印打印机的设备 URI 并点击 `Continue` 按钮。

![](img/b159ac7fe2135643dc37ccfeef6d3980_76_0.png)
# 图 3.1
打印机向导的打开页。

![](img/b159ac7fe2135643dc37ccfeef6d3980_76_1.png)
# 图 3.2
设备选择页。

# 设置打印机和类

# 第 3 章

![](img/b159ac7fe2135643dc37ccfeef6d3980_77_0.png)
# 图 3.3
网络设备 URI 页面。

对于串口设备，会出现串口配置页（见图 3.4）。

在您选择并配置好设备后，将显示制造商选择页（见图 3.5）。

从列表中选择相应的制造商并点击 `Continue` 按钮显示模型选择页（见图 3.6）。

从列表中选择相应的模型并点击 `Continue` 按钮添加打印机。点击打印机链接查看打印队列状态（见图 3.7）。

## 通过 Web 配置打印机

添加打印机后，您应该配置打印机的默认选项。点击 `Configure Printer`（配置打印机）按钮配置打印机（见图 3.8）。

检查页面上的每个选项并根据需要进行更改。完成后，点击 `Continue` 按钮保存更改。

恭喜，您现在准备好打印了！

![](img/b159ac7fe2135643dc37ccfeef6d3980_78_0.png)
# 图 3.4
串口配置页。

![](img/b159ac7fe2135643dc37ccfeef6d3980_78_1.png)
# 图 3.5
制造商选择页。

# 设置打印机和类

# 第 3 章

![](img/b159ac7fe2135643dc37ccfeef6d3980_79_0.png)
# 图 3.6
模型选择页。

![](img/b159ac7fe2135643dc37ccfeef6d3980_79_1.png)
# 图 3.7
打印队列状态页。

# 第一部分 使用 CUPS

![](img/b159ac7fe2135643dc37ccfeef6d3980_80_0.png)
# 图 3.8
打印机选项页。

## 打印测试页

添加打印机后，您可能想打印一个测试页。CUPS 包含了一个简单的测试页文件。在 Web 界面点击 `Print Test Page`（打印测试页）按钮，或运行以下命令将测试页打印到您的打印机：

```
lp -p name -d
```

结果应该像图 3.9 一样。

![](img/b159ac7fe2135643dc37ccfeef6d3980_81_0.png)
# 图 3.9
打印机测试页。

## 修改打印机驱动

`-i`, `-m`, 和 `-P` 选项设置要使用的打印机驱动文件：
```
lpadmin -p name -i script-filename ENTER
lpadmin -p name -m ppd-filename ENTER
lpadmin -p name -P ppd-filename ENTER
```

`-m` 选项从 `/usr/share/cups/model` 目录复制文件。除非指定绝对路径，否则其他选项将从当前目录复制文件。

> 注意：
你可以使用 `lpinfo -m` 命令获取可用打印机驱动程序的列表。

## 修改打印机配置

`-o` 选项设置打印机选项：
```
lpadmin -p name -o option=value
```

该选项可以是打印机 PPD 文件或表 3.11 中的任意项。

### 表格 3.11 可使用 lpadmin 设置的打印机选项

| 选项 | 说明 |
| :--- | :--- |
| job-k-limit=value | 设置每个用户允许打印的文件千字节数（KB）限制。将值设置为 0 以禁用千字节限制。 |
| job-page-limit=value | 设置每个用户允许打印的页数限制。将值设置为 0 以禁用页数限制。 |
| job-quota-period=value | 设置配额计算的时间（秒）。将周期设置为 0 秒以禁用配额。 |
| job-sheets-default=value[,] | 设置每个作业打印的默认横幅页。如果指定了值，则会在每个作业中也添加一个封页，这对于产生正向打印的打印机打印横幅很有用。 |
| media-value,[value,...] | 为打印介质的大小、类型或来源设置介质选项。 |
| output-bin=value | 设置打印机的输出盒。 |
| resolution=value | 设置打印作业的分辨率。 |
| sides=value | 设置单面或双面打印。允许值为单面（one-sided）、长边双面（纵向，portrait）和短边双面（横向，landscape）- 。 |

## 在打印机上设置配额

CUPS 为每台打印机支持基于页数和大小的配额。配额按每个用户单独跟踪，但一组限制适用于特定打印机的所有用户。例如，你可以限制昂贵打印机上的每个用户每天打印 5 页，但你无法限制 Johnny 以外的所有用户。

`job-k-limit`、`job-page-limit` 和 `job-quota-period` 选项决定是否以及如何执行打印机配额。间隔以秒为单位，一天为 86,400 秒，一周为 604,800 秒，一个月为 2,592,000 秒。

要执行配额，必须将周期至少一个限制设置为非零值。以下选项将启用配额：

```
lpadmin -p name -o job-quota-period=648000 -o job-k-limit=1024 ENTER

lpadmin -p name -o job-quota-period=648000 -o job-page-limit=100 ENTER

lpadmin -p name -o job-quota-period=648000 -o job-k-limit=1024 -o job-page-limit=100 ENTER
```

而这些选项本身将：

```
lpadmin -p name -o job-quota-period=648000 ENTER

lpadmin -p name -o job-page-limit=100 ENTER

lpadmin -p name -o job-k-limit=1024 ENTER
```

## 限制访问打印机

`-option` 控制哪些用户可以打印到打印机。默认配置允许所有用户打印到打印机：

```
lpadmin -p name -u allow:ALL ENTER
```

CUPS 支持允许（allow）和拒绝（deny）列表——你可以指定允许或不允许打印的用户列表。在使用用户列表的同时，你可以指定他们被允许或不允许使用打印机：

```
lpadmin -p name -u allow:peter,paul,mary ENTER
```

此命令允许 `peter`、`paul` 和 `mary` 打印到指定的打印机，但所有其他用户都无法打印。命令：

```
lpadmin -p name -u deny:peter,paul,mary ENTER
```

具有相反的效果。`peter`、`paul` 和 `mary` 之外的所有用户都将打印到指定的打印机。

## 注意：

允许和拒绝选项不是交换的。也就是说，你每次都必须提供允许或拒绝用户的完整列表。

此外，CUPS 仅维护一个用户列表——该列表可以允许或拒绝用户打印。如果你指定了一个允许列表，然后指定了一个拒绝列表，拒绝列表将替换允许列表——任何时间只有一个列表处于激活。

## 删除打印机

`-x` 选项删除打印机：

```
/usr/sbin/lpadmin -x name ENTER
```

当删除打印机时，所有的打印数据、作业历史和配额信息都会丢失。没有撤销命令。

## 设置默认打印机

每台服务器都有一个默认打印机。当用户在打印时未指定打印机时，将使用默认打印机。`-d` 选项设置服务器默认打印机：

```
/usr/sbin/lpadmin -d name ENTER
```

除了服务器默认设置外，本地打印命令还支持覆盖服务器默认的客户端打印机。此客户端打印机可以为整个计算机设置或。

## 从命令行管理打印机类

`lpdadmin` 命令提供了管理系统上类的选项。`-p` 和 `-c` 选项用于将打印机添加到类中：

```
/usr/sbin/lpdadmin -p name -c class ENTER
```

如果该类不存在，则会自动创建。随后，会将命名的打印机添加到该类中。多次运行 `lpdadmin` 命令可以构建包含多个打印机的类。例如，运行以下命令：

```
/usr/sbin/lpdadmin -p LaserJet1 -c AllLaserJets ENTER

/usr/sbin/lpdadmin -p LaserJet2 -c AllLaserJets ENTER

/usr/sbin/lpdadmin -p LaserJet3 -c AllLaserJets ENTER

/usr/sbin/lpdadmin -p LaserJet4 -c AllLaserJets ENTER
```

将创建一个名为 `AllLaserJets` 的类，该类包含 `LaserJet1`、`JetJet2`、`JetJet3` 和 `LaserJet4` 打印机。

## 从类中移除打印机

`-r` 选项从类中移除指定的打印机：

```
/usr/sbin/lpdadmin -p name -r class ENTER
```

如果你从类中删除了所有打印机，该类将被自动删除。

## 完全删除类

`-x` 选项允许你在不先移除类中所有打印机的情况下删除类：

```
/usr/sbin/lpdadmin -x class ENTER
```

属于该类的打印机不受删除操作的影响。

## 从 Web 界面添加类

类的 Web 界面位于：

```
http://localhost:631/admin
```



“添加类”（Add Class）显示了类向导的第一页（见图 3.12）。

![](img/b159ac7fe2135643dc37ccfeef6d3980_90_0.png)

图 3.12

类向导的打开页面。

你首先需要提供的是类的名称、位置和描述。位置和描述可以是你喜欢的任何普通文本。点击“继续”（Continue）按钮选择哪些打印机将成为类的一部分（见图 3.13）。

选择每个应属于你类的打印机，并点击“继续”按钮将该类添加到系统。

# 设置打印机和类

![](img/b159ac7fe2135643dc37ccfeef6d3980_91_0.png)

图 3.13

类成员页面。

## 从 Web 界面管理类

添加类类后，可以通过以下 URL 访问它们：

`http://localhost:631/classes`

每个类都显示有用于执行管理功能的按钮（见图 3.14）。

## 修改类

“修改类”（Modify Class）按钮会启动类向导，并在操作过程中显示原始信息和成员打印机。这对于从类中添加和移除打印机最为有用。

## 删除类

“删除类”（Delete Class）按钮会显示一个确认页面（见图 3.15）。当你点击“继续”按钮时，该类将被删除。

类被删除后，所有的类数据、作业历史和配额信息都将丢失。没有撤销命令。这不会影响类中的单个打印机。

## 启动类

点击“启动”（Start）按钮启动已停止的类。该类的任何待处理作业将立即在类中下一个可用的打印机上开始打印。

> 注意：
> 启动一个类不会影响类中的单个打印机

![](img/b159ac7fe2135643dc37ccfeef6d3980_92_0.png)

![](img/b159ac7fe2135643dc37ccfeef6d3980_93_0.png)

图 3.15

类删除确认页面。

## 停止类

点击“停止类”（Stop Class）按钮停止运行中的类。该类的任何活动作业将立即暂停。在类停止期间，处于状态的打印机可以打印其他作业。

> 注意：
> 停止类不会影响类中的单个打印机。

## 接受打印作业

点击“接受作业”（Accept Jobs）按钮接受该类的新作业。用户将能够立即向该类提交打印作业。

第一部分 使用 CUPS

注意：

接受某个类的作业不会影响类中的单个打印机。

## 拒绝打印作业

点击“拒绝作业”（Reject Jobs）按钮拒绝该类的新作业。用户将不再能够向该类提交打印作业。

注意：

拒绝某个类的作业不会影响类中的单个打印机。

## 打印测试页

点击“打印测试”（Print Test）按钮向该类打印测试页。参考图 3.9 查看该页面。

## 隐式类

CUPS 还支持隐式类。隐式类的工作方式与普通类类似，但根据网络上可用打印机自动创建。

隐式类允许你设置具有相同打印机配置的多台服务器，并让客户端将作业发送到第一个可用服务器。如果一个或多个服务器宕机，作业将自动重定向到运行的服务器，提供故障打印。当所有服务器都在运行时，效果就是通用的负载均衡。

## 总结

CUPS 支持打印机、类和隐式类。`lpadmin` 命令提供了大部分打印机和类管理。

# 第 4 章

# 使用 CUPS 打印

本章将介绍如何提交、查询和取消打印作业。

### 打印文件

对于许多类型的文件，默认打印机选项可能已经满足需求。然而，有时你可能需要更改打印选项。

`lp` 和 `lpr` 命令允许使用 `-o` 传递打印机选项：

```
lp -o landscape -o scaling=75 -o media=A4.jpg
lpr -o landscape -o scaling=75 -o media=A4.jpg
```

### 选择打印机

许多系统有多个可用打印机。使用 `lpstat` 命令查看可用打印机列表：

```
lpstat -p -d
printer CL450 is idle.
printer4000 is idle.
printer Stylus600 is idle.
```
> `-p`选项请求列表，`d`选项询问目标。

知道打印机名称后，使用 `lp` 命令的 `-d` 选项和 `lpr` 命令的 `-P` 选项打印到该打印机。

可以使用 `name@server` 远程服务器上的打印机。

```
lp -d name@server filename
lpr -P name
```

### 打印多个副本

`lp` 和 `lpr` 命令都有打印文件多个副本的选项：

```
lp -n num-copies filename
```
默认情况下，副本是不合并的（为了提高速度）。如果你需要打印合并副本，请参见“打印合并副本”章节。

### 加密你的打印作业

你打印的一些文档可能包含敏感信息，例如合同和其他法律文件。如果你打印到另一台机器上的打印机，不法分子可能会监听你的打印作业并收集此类信息。

所有的打印命令都支持 `-E` 选项来加密（混淆）你与打印服务器之间的通信，使得他人很难监听你的通信。例如，要加密打印作业，你可以可以使用：

```
lp -E -d name@server filename
```

### 设置打印机选项

每个打印机都有自己的选项，这些选项基于 PPD（驱动程序）文件中的选项。`lpoptions` 提供查看可用列表的方法：

```
lpoptions -p LaserJet4000 -1
HPPollateCollate: *False True
HPPaperPolicy/Fit to Page: NearestSizeNoAdjust NearestSizeAdjust *PromptUser
```

### 打印合并副本

通常不会为你合并副本。使用 `-collate` 选项生成合并副本：

```
lp -n num-copies -o collate=True filename
lpr -nnum-copies -o collate=True filename
```

### 使用 CUPS

HPHalftone/Pages of Gray: 增强型 *PrinterDefault Standard*
HPNun/Pages of Sheet: OneUp *OneUp TwoUp TwoUp FourUp FourUp SixUp
➤SixUp NineUp NineUp SixteenUp SixteenUp
HPwmLocation/Printmark: *True False*
Smoothing/Resolution Enhancement: False *True*
HPScalePatterns/Scale Patterns: Off *Scale*
HPwText/Watermark: CompanyConfidential CompanyPrivateProprietary
➢ Confidential Copy Copyright Draft FileCopy ForInternalUse
*None Preliminary Proof Review Sample TopSecret Urgent
HPwmText/Watermark Angle: DegN15 DegN30 DegN45 DegN60 DegN75 DegN90 Deg
➢Deg15 Deg30 *Deg35 DegN90
HPwFont/Watermark Font: CourierB *Helvetica B Times
HPwFontSize/Watermark Size: pt24 pt30 pt36 pt42 *pt48 pt54 pt66
➤pt72 pt78 pt84
HPwTextStyle/Watermark Style: *Medium Narrow Wide*
Duplex/Duplex: Numpy Duplex *None*
PageSize/Media Size: A4 B5 Env10 EnvOBIS EnvCS EnDL Monarch
➢Executive Letter
InputSlot/Media Source: Envelope Upper Manual Feed *LargeCapacity
MediaPlayer/Media Type: Bond Gray Color Labels Letter *None Plain
➤Preprinted Recycled Rough Transparency
PageRegion/PageRegion: A4 B5 Env10 EnvOBIS EnvCS EnDL Monarch
➢Legal Letter
Option3/Duplex Unit: *True False*
Options/Envelope Feeder: *True False*
Option4/Printer Hard Disk: *True False*
InstalledMemory/Total Printer Memory: 4MB 8MB 12MB 20MB 28MB *36MB
Option1/Tray 3: *True False*
Option2/Tray 4: *True False*
JCLEconomode/EcoMode: *True False*
JCLResolution/Resolution: 300dpi 600dpi *1200dpi

每个选项都以选项名称、斜杠、该选项的人类可读描述和冒号开头。选项本身紧跟在冒号后面：

`JCLResolution/Resolution: 300dpi 600dpi *1200dpi`

此选项控制 HP LaserJet 4000 上的分辨率。选项名称为 `JCLResolution`。它支持 300dpi、600dpi 和 1200dpi 值。1200dpi 前的星号 (`*`) 表示默认分辨率为 1200 DPI。

可以使用 `-o` 选项在打印时指定不同的分辨率。例如，以下命令可以以 600 DPI 打印作业：

```
lp -o JCLResolution=600dpi filename ENTER
lpr -o JCLResolution=600dpi filename ENTER
```

### 标准打印选项

本节描述了在使用 `lp` 和 `lpr` 命令进行打印时可用的标准打印选项。

### 通用选项

表 4.1 列出了适用于打印所有类型文件的通用选项。

表 4.1 CUPS 通用打印选项
| 名称 | 描述 |
| --- | --- |
| brightness | 设置输出的整体亮度 |
| gamma | 设置输出的整体伽马校正（对比度） |
| job-sheets | 选择用于作业的横页 |
| landscape | 以横向方向打印 |
| media | 设置介质尺寸、源和/或类型 |
| number-up | 设置每张纸上打印的文档页数 |
| page-ranges | 打印文档中指定的页面 |
| page-set | 打印文档中的所有、偶数页或奇数页 |
| sides | 打印单面或双面 |

### 设置方向

`landscape` 选项会将页面旋转 90 度以横向打印。

```
lp -o landscape ENTER
lpr -o landscape ENTER
```

### 选择介质尺寸、类型和源

`media` 选项设置介质尺寸、类型和/或：

```
lp -o media=Letter ENTER
lpr -o media=Letter,MultiPurpose ENTER
lpr -o media=Letter,Transparency ENTER
lpr -o media=Letter,MultiPurpose,Transparency ENTER
```

可以通过逗号分隔多个介质值。可用的介质尺寸、类型和源取决于打印机，但支持表 4.2 所示选项。

表 4.2 通用介质选项
| 值 | 描述 |
| --- | --- |
| Letter | U.S. Letter (8.5x11 英寸) |
| Legal | U.S. Legal (8.5x14 英寸) |
| A4 | ISO A4 (8.27x11.69 英寸) |
| COM | US Envelope (9.5x4.12 英寸) |
| DL | ISO DL Envelope (8.66x4.33 英寸) |
| Transparency | 透明材质 |
| Upper | 上纸盒 |
| Lower | 下纸盒 |
| Multipurpose | 多功能纸盒 |
| LargeCapacity | 大容量纸盒 |

实际选项来自打印机 PPD 文件中的 PageSize、InputSlot 和 MediaType 选项。可以使用 `grep` 过滤输出来查看这些选项：

```
options -p name -l | grep 'PageSize|MediaType|InputSlot'
PageSize/Media Size: A4 A5 B5 Custom Env1 EnOB5 EnVDLMonarch
*Executive *Letter
InputSlot/Media Size: Envelope Upper ManualFeed Middle *LargeCapacity
MediaType/Media Type: Bond Cardstock Color Labels Letterhead*None Preprinted Prepun Recycled Transparency
```

### 双面打印

`sides` 选项开启或关闭双面打印。表 4.3 显示 `sides` 选项的有效值：

表 4.3 有效 sides 选项值
| 选项 | 描述 |
| --- | --- |
| -o sides=one-sided | 单面 |
| -o sides=two-sided-long-edge | 垂直文档双面 |
| -o sides=two-sided-short-edge | 横向文档双面 |

最常用的值是 `two-sided-long-edge`，如下：

```
lp -o sides=two-sided-long-edge ENTER
lpr -o sides=two-sided-long-edge ENTER
```

### Banner选项

`job-sheets` 选项适用于所有类型的文件，并设置作业使用的横页（页）：

```
lp -o job-sheets=none ENTER
lp -o job-sheets=standard ENTER
lpr -o job-sheets=standard ENTER
```
`-o job-sheets=none` 选项和 `-o job-sheets=standard` 选项用于作业。

标准 banner 文件列在表 4.4 中。

表 4.4 标准 banner 文件
| 名称 | 描述 |
| --- | --- |
| none | 不产生横页 |
| classified | 带有“分类”的横页 |
| confidential | 带有“机”的横页 |
| secret | 带有“秘密”的横页 |
| standard | 标准横页 |
| topsecret | 带有“顶级”的横页 |
| unclassified | 带有“未分类”的横页 |

### 文档选项

表 4.5 显示的文档选项适用于所有类型的文件。

表 4.5 通用文档选项
| 名称 | 描述 |
| --- | --- |
| brightness | 调整输出的亮度 |
| gamma | 调整输出的伽马（对比度） |
| number-up | 在单页上打印多个页 |
| page-ranges | 选择页面范围 |

### 选择页面范围

`page-ranges` 选项选择页面范围：

```
lp -o page-ranges=1 ENTER
lp -o page-ranges=1-4 ENTER
lp -o page-ranges=1-4,7-12 ENTER
lpr -o page-ranges=1-4,7-12 ENTER
```

如之前所示，页面值可以是单页、页码范围或一组用逗号分隔的页码。无论 `page-ranges` 选项中的页面顺序如何，页面始终按升顺序打印。

默认是打印所有页面。

### 选择偶数页或奇数页

使用 `page-set` 选项选择偶数页或奇数页。

```
lp -o page-set=odd ENTER
lp -o page-set=even ENTER
lpr -o page-set=all ENTER
```
`page-set` 选项的合法值见表 4.6。

| 名称 | 描述 |
| --- | --- |
| all | 打印所有页面（默认） |
| even | 仅打印偶数页 |
| odd | 仅打印奇数页 |

### NUp打印

`number-up` 选项选择 NUp 打印。NUp 打印将多个文档页放在单张打印页上。

CUPS 支持 1-Up、2-Up 和 4-Up 格式。

```
lp -o number-up=1 ENTER
lp -o number-up=2 ENTER
lp -o number-up=4 ENTER
lpr -o number-up=4 ENTER
```

默认格式是 1-Up。

### 设置亮度

可以使用 `brightness` 选项控制打印输出的整体亮度：

```
lp -o brightness=120 ENTER
lpr -o brightness=80 ENTER
```

大于 100 的值会使打印变亮，而小于 100 的值会使其变暗。

## 设置 Gamma 校正

你可以使用 `gamma` 选项控制打印输出的整体伽马校正：

```
lp -o gamma=1700 filename
lpr -o gamma=455 filename
```



大于 1000 的值会使打印变亮，而小于 1000 的值会使其变暗。默认 `gamma` 值为 1000。

## 文本选项

以下选项仅在打印文本文件时。表 4.7 列出了文本打印选项。

### 表 4.7 文本文件打印选项
| 名称 | 描述 |
|---|---|
| `columns` | 设置文本的列数 |
| `cpi` | 设置每英寸字符数 |
| `lpi` | 设置每英寸行数 |
| `page-bottom` | 设置下边距 |
| `page-left` | 设置左边距 |
| `page-right` | 设置右边距 |
| `page-top` | 设置上边距 |
| `prettyprint` | 在顶部打印页眉并高亮语法 |

## 设置每英寸字符数

`cpi` 选项设置每英寸字符数：

```
lp -o cpi=10 filename
lpr -o cpi=12 filename
lpr -o cpi=17 filename
```

默认的每英寸字符数为 10。

## 设置每英寸行数

`lpi` 选项设置每英寸行数：

```
lp -o lpi=6 filename
lpr -o lpi=8 filename
```

默认的每英寸行数为 6。

## 设置列数

`columns` 选项设置文本列数：

```
lp -o columns=2 filename
lpr -o columns=3 filename
```

默认列数为 1。

## 设置页边距

通常情况下，页边距被设置为打印机的物理限制。使用 `page-left`、`page-right`、`page-top` 和 `page-bottom` 来调整边距：

```
lp -o page-left=72 -o page-right=36 filename
lpr -o page-top=36 page-bottom=36 filename
lpr -o page-left=72 -o page-right=36 -o page-bottom=36 filename
```

值参数是以磅（points）为单位的边距；每英寸 72 ，每厘米 28 。

## 美化打印

`prettyprint` 选项在每页顶部放置包含页码、作业标题（通常是文件名）和日期的页眉。此外，`script`、`perl`、`C` 和 `C++` 关键字将加粗，注释行将变为斜体，预处理器行和字符串将高亮。`prettyprint` 选项不需要关联任何值：

```
lp -o prettyprint filename
lpr -o prettyprint filename
```

## 图像选项

以下选项仅在打印图像文件时。表 4.8 列出了有效的图像打印选项。

| 名称 | 描述 |
| --- | --- |
| `hue` | 调整图像色调 |
| `position` | 设置图像在页面上的位置 |
| `ppi` | 设置图像的每英寸像素分辨率 |
| `saturation` | 调整图像的色彩饱和度 |
| `scaling` | 设置图像占页面百分比大小 |

## 定位图像

`position` 选项指定图像在页面上的位置。表 4.9 列出了有效的位置：

### 表 4.9 图像位置
| 选项 | 描述 |
| --- | --- |
| `-o position=center` | 图像页面居中（默认）。 |
| `-o position=top` | 在页面顶部居中打印图像 |
| `-o position=left` | 在页面左侧居中打印图像 |
| `-o position=right` | 在页面右侧居中打印图像 |
| `-o position=top-left` | 在页面左上角打印图像 |
| `-o position=top-right` | 在页面右上角打印图像 |
| `-o position=bottom` | 在页面底部居中打印图像 |
| `-o position=bottom-left` | 在页面左下角打印图像 |
| `-o position=bottom-right` | 在页面右下角打印图像 |

## 缩放图像

通常图像使用文件本身的分辨率信息进行缩放。如果没有信息，则使用默认每英寸 128 像素。`scaling` 和 `ppi` 选项更改打印图像的大小：

```
lp -o ppi=100 filename
lp -o ppi=128 filename
lpr -o ppi=300 filename
```

`scaling` 值为 1 到 800 的百分比。该百分比是基于页面大小而非图像大小，因此 100% 将尽可能填满页面。200% 将打印多页。`ppi` 值为 1 到 1200 之间的数字，指定每英寸像素数。例如，3000x2400 像素的图像将以每英寸 300 像素打印。

## 调整图像的色调（色彩）

`hue` 选项调整打印图像的颜色，类似于电视上的色调控制：

```
lp -o hue=0 filename
lp -o hue=45 filename
lpr -o hue=-45 filename
```

该值为 -60 到 360 之间的数字，代表色调旋转的角度。表 4.10 总结了不同颜色的变化：

### 表 4.10 色调调整
| 原始颜色 | `hue=-45` | `hue=45` |
|---|---|---|
| 红色 | 紫色 | 橙色 |
| 绿色 | 蓝绿色 | 黄绿色 |
| 黄色 | 橙色 | 绿色 |
| 蓝色 | 天蓝色 | 紫色 |
| 品红色 | 靛蓝 | 深红色 |
| 青色 | 蓝绿色 | 深蓝色 |

默认色调调整值为 0。

## 调整图像的饱和度（色彩）

`saturation` 选项调整图像色彩饱和度，类似于电视上的色彩旋钮：

```
lp -o saturation=100 filename
lp -o saturation=0 filename
lpr -o saturation=200 filename
```

该值为 0 到 200 之间的饱和度。饱和度 0 会产生黑白打印，而 200 会让颜色极其强烈。默认饱和度为 100。

## HP-GL/2 选项

以下选项适用于 HP-GL/2 文件。表 4.11 列出了 HP-GL/2 打印选项。

### 表 4.11 HP-GL/2 文件打印选项
| 名称 | 描述 |
|---|---|
| `blackplot` | 使用黑色墨水绘 |
| `fitplot` | 使图形适应页面 |
| `penwidth` | 设置默认笔宽 |

## 黑色打印

`blackplot` 选项指定所有的笔都用黑色绘图：

```
lp -o blackplot filename
lpr -o blackplot filename
```

默认使用文件中定义的颜色。

## 将图形置于页面

`fitplot` 选项指定图形应缩放以适应页面：

```
lp -o fitplot filename
lpr -o fitplot filename
```

默认使用文件中指定的绝对距离。

## 设置默认笔宽

`penwidth` 选项指定 HP-GL/2 文件的默认笔宽：

```
lp -o penwidth=1000 filename
lpr -o penwidth=0 filename
```

`penwidth` 值是以微米为单位的宽度。默认值 1000 产生 1 毫米宽的线条。指定宽度为 0 会产生 1 像素宽的线条。

## 原始或未过滤输出

`raw` 选项允许你直接将文件发送到打印机而不经过过滤。当从提供自带打印机程序的应用程序打印时，有时需要这样做：

```
lp -o raw filename
lpr -o raw filename
```

## 保存打印机选项

每台打印机都支持许多选项。CUPS 允许你将其保存为打印机的默认选项，而不是每次打印文件都指定这些选项。

`loptions` 命令保存打印机选项。与 `lp` 和 `lpr` 命令一样，它使用 `-o` 选项接受打印机选项：

```
loptions -o media=A4 -o sides=two-sided-long-edge
loptions -o media=Legal -o scaling=100
```

保存后，任何 `lpr` 命令在打印时都会使用它们。

## 为特定打印机设置选项

之前的示例显示了如何设置默认打印机的选项。`-p printer` 选项指定特定打印机的选项：

```
loptions -p name -o media=A4 -o sides=two-sided-long-edge
loptions -p name -o media=Legal -o scaling=100
```

## 查看当前保存的选项

在命令行不指定任何新选项的情况下，可以使用 `loptions` 命令显示当前选项：

```
loptions ENTER
media=A4 sides=two-sided-long-edge
```

```
loptions -p deskjet ENTER
media=Legal scaling=100
```

## 设置默认打印机

管理员通常会设置一个服务器默认打印机，供所有人默认使用。使用 `-d printer` 选项设置你自己的默认打印机：

```
loptions -d name ENTER
```

## 打印机实例

除了为每个打印机队列设置选项外，CUPS 还支持打印机实例，这允许你为每台打印机定义若干不同的选项集。你可以使用斜杠（/）指定打印机实例：

```
lpoptions -p laserjet/duplex -o sides=two-sided-long-edge
lpoptions -p laserjet/legal -o media=Legal
```

`lp` 和 `lp2` 命令也理解这种符号：

```
lp -d laserjet/duplex filename
lpr -P laserjet/legal filename
```

注意：

`lpoptions` 命令用于创建打印机实例以及默认选项。当你第一次使用 `lpoptions` 使用实例名称时，该实例就会被创建。例如，运行此命令：

```
lpoptions -p deskjet/photo -o resolution=600dpi -o media=photo
```

为打印机 "deskjet" 创建一个名为 "photo" 的新实例。

## 移除选项和实例

使用 `-x` 选项移除你不再需要的打印机或实例的所有选项：

```
lpoptions -x deskjet
lpoptions -x laserjet/duplex
lpoptions -x laserjet/legal
```

`-x` 选项仅移除该打印机或实例的选项；原始打印机和系统默认保持不变。

## 从命令行检查打印机状态

可以使用 `lpstat` 命令检查你已提交打印的作业：

```
lpstat
Printer-1 johndoe 4427776
Printer-2 johndoe 15786
Printer-3 johndoe 372842
```

作业按打印顺序列出。使用 `-p` 选项查看哪些文件和打印机处于激活状态：

```
lpstat -p
```

`printer DeskJet` 正在打印 `DeskJet-1`.

使用 `-o` 和 `-p` 选项显示作业和打印机：

```
lpstat -o -p
DeskJet-1 johndoe 4427776
DeskJet-2 johndoe 15786
DeskJet-3 johndoe 372842
printer DeskJet 正在打印 DeskJet-1.
```

## 从 Web 检查打印机状态

打开以下 URL，从浏览器监控打印机和作业状态：

```
http://localhost:631
```

从那里，你可以点击按钮查看类、作业和打印机的状态！

## 从命令行取消打印作业

`cancel` 和 `lprm` 命令用于取消打印作业：

```
cancel job-id
lprm job-id
```

`job-id` 是 `lp` 或 `lpstat` 命令向你报告的数字。

## 从 Web 界面取消打印作业

你也可以从 Web 界面取消打印作业。首先在 Web 浏览器中打开以下 URL：

```
http://localhost:631/jobs
```

然后点击你想取消作业的 Cancel Job 按钮。

## 为 CUPS 配置应用程序

虽然大多数应用程序可以在不更改的情况下与 CUPS 工作，但某些应用程序需要少量配置以使用正确的打印机驱动等。其他应用程序可以进行增强以利用 CUPS 的功能。

### GIMP

GIMP 可能是目前最著名的 Unix 图像应用程序。GIMP 包含一个打印插件，可以处理到许多不同类型的打印机——事实上，你可以在 GIMP-print 主页上获取这些驱动程序的 CUPS 版本！

随 GIMP 1.2x 一附带的打印插件将在 GIMP-print 支持的任何打印机上正常工作。要与其他驱动程序配合 GIMP，你需要对插件进行一些配置。

要为 CUPS 配置打印插件，在 GIMP 中打开图像文件，然后从文件（File）菜单中选择打印（Print）。这将显示打印插件窗口（见图 4.1）。

![](img/b159ac7fe2135643dc37ccfeef6d3980_111_0.png)

图 4.1

GIMP 打印插件窗口。

选择你想配置的打印机并点击 Setup 按钮。这将打印设置对话框（见图 4.2）。

为打印机驱动选择 PostScript Level 2。

接下来，输入打印机的 PPD 文件名称，或点击 Browse 按钮找到它。本地打印机将 PPD 文件存储在 `/etc/cups/` 中；对于远程打印机，从服务器上的该目录复制 PPD 文件，或者在浏览器中加载 PPD 文件并点击另存为；任何服务器上都可以通过以下 URL 获得 PPD 文件：

```
http://server:631/printers/name.ppd
```

## 第一部分 使用 CUPS

![](img/b159ac7fe2135643dc37ccfeef6d3980_112_0.png)

图 4.2

打印设置对话框。

### Netscape

Netscape 需要极少的配置。

### Star Office

Star Office 提供了相当的支持。

## 使用 CUPS 打印

![](img/b159ac7fe2135643dc37ccfeef6d3980_113_0.png)

图 4.3

spadmin 窗口。

![](img/b159ac7fe2135643dc37ccfeef6d3980_114_0.png)

图 4.4

打印机窗口。

![](img/b159ac7fe2135643dc37ccfeef6d3980_115_0.png)

图 4.5

驱动安装对话框。

![](img/b159ac7fe2135643dc37ccfeef6d3980_116_0.png)

图 4.6

配置对话框。

![](img/b159ac7fe2135643dc37ccfeef6d3980_117_0.png)

图 4.7

打印对话框。

## 第 5 章

### 服务器配置

本章介绍了如何配置 CUPS 服务器并包含了服务器配置的示例。

### 基础

CUPS 调度器由 IPP 服务器 (`cupsd`)、轮询守护进程 (`cups-poll`) 和行打印进程网关 (`cups-lpd`) 组成。这些程序共同工作提供打印服务。

### 配置文件

CUPS 服务器 (`cupsd`) 在启动时会读取多个配置文件。通常这些文件位于 `/etc/cups` 目录下。表 5.1 列出了配置文件及其用途：

| 文件 | 用途 |
| :--- | :--- |
| `classes.conf` | 包含每个打印机类的信息。通常使用 `lpadmin` 命令或 Web 界面操作此文件。 |
| `client.conf` | 为客户端提供默认服务器名称。更多信息请见第 6 章“客户端配置”。 |
| `cupsd.conf` | 控制 CUPS 服务器 (`cupsd`) 如何运行，通常通过手动编辑。 |
| `mime.conf` | 包含标准文件转换过滤列表及其成本。通常不编辑此文件。 |
| `printers.conf` | 包含每个打印机的信息。通常使用 `lpadmin` 命令或 Web 界面操作此文件。 |
| `ssl/server.crt` | SSL/TLS 证书文件。 |
| `ssl/server.key` | SSL/TLS 私钥文件。 |

### 修改服务器配置

`cupsd.conf` 文件包含了控制服务器如何运行的配置指令。其格式特意类似于流行的 Apache Web 服务器配置文件。

每行要么为空，要么包含配置指令，要么包含注释。注释在行开头使用数字符号 (`#`) 引入。

由于服务器配置文件由纯文本组成，因此您可以使用喜喜欢的文本编辑器对其进行修改。

**注意：**

CUPS 提供了多种配置文件编辑器，可以省去手动编辑配置文件的麻烦。

CUPS 软件包含一个基于 KDE 的编辑器，允许您在本地服务器上编辑配置文件。

ESP Print Pro 4.2 及更高版本包含一个 GUI 编辑器，可以可以在本地或远程编辑配置文件。

最后，CUPS 1.2 包含一个基于 Web 的配置编辑器。

## 服务器指令

CUPS 支持大多数标准的 Apache 配置指令，以及一些针对 CUPS 特有的新指令。您可以在附录 A“配置文件指令”中找到这些指令的完整参考。

## 重启 CUPS 服务器

在对配置文件进行更改后，您需要通过向 CUPS 服务器发送 `HUP` 信号或使用提供的初始化脚本来重启 CUPS 服务器。CUPS 发行版将脚本安装在 `init.d` 目录中，命名为 `cups`。具体位置因操作系统而异：

```
/etc/init.d/cups restart
/etc/rc.d/init.d/restart restart
/sbin/init.d/cups restart
```



## 基本配置选项

CUPS 自带的示例配置适用于独立系统。接下来的章节将展示如何对基本配置进行常见修改，以支持服务器运行、便捷的 Web 浏览器集成、增强安全性以及加密。

## 将 CUPS 配置为服务器

默认的 CUPS 配置未启用来自客户端系统的连接。要启用来自客户端系统的连接，请编辑 `cupsd.conf` 文件并找到以下读取部分：

```
<Location />

Order deny,allow

Deny from all

Allow from 127.0.0.1

</Location>
```

假设您的本地网络地址为 `192.168.0.0`，子网掩码为 `255.255.0.0`，以下更改将允许客户端的远程打印：

```
<Location />

Order deny,allow

Deny from all

Allow from 127.0.0.1

Allow from 192.168.0.0/255.255.0.0

</Location>
```

> **注意：**
早期的 CUPS 默认允许来自所有主机的连接。除非您正在提供互联网范围内的打印服务，否则请允许来自所有主机的连接。添加“Allow from all”行是配置服务器最简单的方法，但这会无必要地让您的打印服务器暴露在意外作业和来自外部系统的拒绝服务攻击之下。

接下来，您需要通过指定本地网络的网络广播地址来启用服务器的广播功能。添加以下指令将广播地址设置为 `192.168.255.255`：

```
BrowseAddress 192.168.255.255
```

保存对 `cupsd.conf` 的更改后，重启服务器。现在，您所有的 CUPS 客户端都将看到服务器上的打印机并能够向其打印。

> **注意：**
CUPS 使用 UDP 广播为客户端提供打印机浏览支持。`BrowseAddress` 指令以此命名是为了未来支持其他类型的浏览，如多播、SLP 和 LDAP。

## 便捷的 Web 浏览

通常，CUPS 在 IPP 端口（端口 `631`）上监听 HTTP 请求。用户使用以下 URL 访问 CUPS 服务器：

```
http://server:631
```

为了让客户端更容易访问 CUPS 服务器，请在 `cupsd.conf` 文件中添加第二个端口指令，使 CUPS 服务器在标准的 HTTP 端口 (`80`) 上监听：

```
Port 631

Port 80
```

现在，您的用户也可以通过以下（更简单的）URL 访问 CUPS 服务器：

```
http://server
```

## 增强安全性

CUPS 的默认配置是以 root 用户运行 CUPS 服务器，但以非特权用户运行所有外部程序。尽管这为防止非特权访问系统资源提供了极佳安全性，但由于服务器是以 root 身份运行的，可能会利用未发现的漏洞来获取 root 权限。

CUPS 提供了 `RunAsUser` 指令，用于设置网络服务后以非特权用户运行服务器。在 `cupsd.conf` 中添加以下行以启用此模式：

```
RunAsUser Yes
```

> **注意：**
当作为非特权用户运行服务器时，SIGHUP 重新配置机制会被禁用。`/etc/cups` 下的任何文件（以及 `/etc/cups` 目录本身）也必须由非特权用户所有。
此外，任何本地设备（并行口、串口和 USB 端口）必须允许非特权用户访问，否则在尝试时将导致“permission denied”信息。
最后，某些网络 LPD 打印机可能无法在非特权模式下工作，因为 LPD 后无法按照 RFC 1179 的要求保留特权端口。

## 加密

CUPS 支持对服务器的任何请求或响应进行 128 位加密。加密会对客户端和服务器之间的数据进行混乱，使得窃听者无法理解。加密最常见的用途是对从远程机器执行管理任务时发送的密码进行混乱。它还用于通过互联网打印敏感文档。

在您的服务器上启用加密之前，您必须获得加密证书。这可以从许多证书颁发机构之一（见表 5.2）购买，或者使用 OpenSSL 提供的工具创建一个未签名的证书。

> **注意：**
加密可以由官方证书颁发机构签名，也可以使用 OpenSSL 提供的工具创建未签名的证书。

| 证书类型 | 来源 |
| :--- | :--- |
| 128-bit | http://www.128.com |
| BelSign | http://www.bels.com |
| Certifica | http://www.certifica.com |
| Certplus | http://www.certplus.com |
| Deutsches | http://www.deutsches.de |
| Entrust | http://www.entrust.com |
| Equifax | http://www.equifax.com |
| GlobalSign | http://www.globalsign.com |
| IKS | http://www.iks.com |
| NetLock | http://www.netlock.com |
| TrustCenter | http://www.trustcenter.com |
| Thawte | http://www.thawte.com |
| Verisign | http://www.verisign.com |

### 生成未签名的证书

如果您决定使用 OpenSSL 生成自己的证书，请运行以下命令：

```
openssl req -new -x509 -keyout /etc/cups/ssl/server.key -out /etc/cups/ssl/server.crt -days 365 -nodes
```

Using configuration from /usr/ssl/openssl.cnf
Generating a RSA key

将被要求输入将纳入证书请求中的信息。您要输入的内容被称为区别名称（DN）。有很多字段，但您可以留空某些。对于某些字段会有默认值，如果您输入 `.`，该字段将留空。

Country Name (2 letter code) ?:US
State or Province Name (full name) ?:Maryland
Locality Name (eg, city) ?:Hollywood
Organization Name (eg, company) ?:Easy Software Products
Organizational Unit Name (eg, section) ?:ENTER
Common (eg, YOUR NAME) ?:host.easysw.com
Email Address ?:mike@host.easysw.com

> `openssl` 命令在 `/etc/cups/ssl` 目录下创建服务器密钥和证书文件。`chmod` 命令确保只有 root 用户可以读取它们。

### 获取签名的证书

如果您决定创建签名的证书，请请求用于 Apache 或 StrongHold Web 服务器的证书——这些证书将符合 CUPS 的格式。

请求证书涉及一些 `openssl` 命令来生成密钥和证书。从生成服务器密钥开始：

```
openssl genrsa -des3 -out /etc/cups/ssl/server.key 1024
```

```
Generating RSA private key, 1024 bit modulus

......+

+++++

e is 65537 (0x10001)

Enter PEM pass phrase:password

Verifying password - Enter PEM pass phrase:password
```

您使用的密码并不重要——我们将在过程的最后一步将其移除。

接下来，使用以下命令生成您的证书请求文件：

```
openssl req -new -key /etc/cups/ssl/server.key -out /etc/cups/server.csr ENTER
```

Using configuration from /usr/ssl/openssl.cnf

输入 PEM 密码短：password ENTER
你将被要求输入将整合到证书请求中的信息。
你将要输入的内容被称为区分名称（Distinguished Name，简称 DN）。
有很多字段，但你可以留一些某些字段为空。
某些字段会有默认值，
如果你输入 '.'，则该字段将留空。

-----
国家名称（2 位代码） ?:US ENTER
州或省份（全称） [:State]:Maryland ENTER
地名（英文， 城市） [:Holywood ENTER
组织名称（英文， 公司） [:Internet Widg Pty Ltd]:Easy Software Products ENTER
组织单位名称（英文，部门） [:ENTER
通用名称（英文， 您的名称） [:host.easysw.com ENTER
电子邮件地址 [:]:mike@host.easysw.com ENTER

请输入以下随您的证书请求一起发送的“额外”属性
挑战密码 [:ENTER]
可选名称 [:ENTER]

将文件 `/etc/cups/ssl/server.csr` 发送给您使用的证书体系。他们将为您
提供一个用于您的 CUPS 服务器的签名证书。该证书
应该复制到文件 `/etc/cups/ssl/server.crt`。

最后，使用这些命令从您的服务器密钥中删除密码

```
cd /etc/cups/ssl ENTER

mv server.key old ENTER

openssl rsa -in server.old -out server.key ENTER

rm server.old ENTER
```

然后确保这些文件仅供服务器读取

```
chmod 600 server.* ENTER
```

搞定！你现在为你的服务器拥有了一个官方的、签名证书！

## 在您的服务器中启用加密

现在你已经安装了证书和密钥，你需要告诉 CUPS 使用它们。CUPS 提供了两种加密方法——专用的 https 类型服务以及较新的 HTTP 升级方法。https 服务会立即加密到服务器的连接，而 HTTP 升级方法仅在客户端或服务器请求时才升级连接。图 5.1 显示了这两种方法的工作原理。

## HTTPs 方法

## HTTP 升级方法

| 客户端 | 服务器 | 客户端 | 服务器 |
| --- | --- | --- | --- |
| 连接 | 接受 | 连接 | 接受 |
| 加密 | 握手 | GET | |
| GET | | | 回复 |
| | | POST | |
| POST | | IPP 请求 | "需要升级" |
| IPP 请求 | | 带升级标志的 POST | 握手 |
| | | IPP 请求 | 回复 |
| ... | | | |

# 图 5.1

CUPS 加密方法。

如果你将使用 Web 浏览器进行远程管理，你将希望启用 https 服务。`SSLPort` 指令告诉 CUPS 如何在指定的端口号上使用 https：

# SSLPort 443

端口 `443` 是 https URL 的标准端口。如果你已经在系统端口 `443` 上运行了安全的 Web 服务器，通常你仍然可以使用除 `80` 和 `631` 之外的任何其他端口号。

`Encryption` 指令也是你想要使用的另一个。它指定了各种资源所需的加密级别。对于远程管理，你需要更新以下部分：

```
<Location /admin>
```

- # 你绝对想要限制对管理函数的访问。
# 默认配置要求来自系统组成员的本地连接
# 以执行任何管理任务。你可以使用 SystemGroup 指令
# 更改组名。
# AuthType Basic
AuthClass System

## 限制访问本地局域
Order Deny,Allow
Deny From All
Allow From 127.0.0.1

### 强制加密
</Location>

假设你的本地网络地址为 `192.168.0.0`，子掩码为 `255.255.0.0`，以下更改将启用加密的远程管理：
<Location /admin>

- # 你绝对想要限制对管理函数的访问。
# 默认配置要求来自系统组成员的本地连接
# 以执行任何管理任务。你可以使用 SystemGroup 指令
# 更改组名。

# AuthType Basic
AuthClass System

## 限制访问本地局域
Order Deny,Allow
Deny From All
Allow From 192.168.0.0/255.255.255.0

Encryption Required
</Location>

### 高级访问控制

CUPS 支持基于客户端地址、用户证书或用户名和密码以及加密的访问控制。

基于地址的访问控制允许你限制对特定系统、网络或域的访问。虽然这不提供身份验证，但它确实允许你有效地限制你系统的潜在用户。

证书、用户名和密码提供了限制对个人或组访问的方法。

最后，你可以要求对特定资源进行加密；这通常用于提供安全的远程管理访问，正如上一节标题“在您的服务器中启用加密”所描述。

### 访问控制基础

CUPS 维护了一个具有访问控制、身份验证和加密的位置列表。位置使用 `Location` 指令指定：

```
<Location /resource>

AuthClass ...

AuthType ...

Encryption ...

```

```

Order

Allow ...

Deny From ...

</Location>
```

位置通常遵循目录结构；然而，CUPS 为管理、类、作业和打印机提供了多个虚拟位置。表 5.3 列出了 CUPS 提供的虚拟位置。

### 表 5.3 CUPS 虚拟位置

| 资源 | 描述 |
| --- | --- |
| /admin | 管理资源 |
| /classes | 类资源 |
| /classes/name | 类名称资源 |
| /jobs | 作业资源 |
| /jobs/id | 作业 ID | |
| /printers | 打印机资源 |
| /printers/name | 打印机名称资源 |
| /printers/name.ppd | 打印机的 PPD 文件 |

### 用户身份验证

CUPS 通过 HTTP Basic 和 Digest 认证支持用户验证。Basic 认证使用 Unix 账户和密码，而 Digest 认证使用特殊的密码文件。

Basic 认证将用户名和密码 Base64 编码发送到服务器，除非你加密连接，否则无法防止窃听。这意味着恶意用户可以监控网络数据包并发现有效的用户名和密码，导致网络安全的严重损害。Basic 仅结合加密使用。

与 Basic 认证不同，Digest 传递用户名和密码字符串的 MD5 和（基本上是一个复杂的校验和）。此外，Digest 认证不使用 Unix 密码，只要你使用对应 Unix 密码的 Digest 密码，攻击者发现原始密码不太导致严重的安全问题。

由于大多数浏览器不支持 Digest 认证，你的最佳选择是启用了加密的 Basic 认证。

CUPS 还支持本地证书认证方案，连接到本地机器的客户端可以使用其替代 Basic 或 Digest 认证。远程客户端不支持也不启用证书认证。

通过位置部分内的 `AuthType` 指令启用认证：

```
<Location /printer/DeskJet>

AuthType Basic

Encryption Required

</Location>
```

此示例在用户向名为 DeskJet 的打印队列打印文件时需要 Unix 密码。如果改用 Digest 密码，请使用：

```
<Location /printer/DeskJet>

AuthType Digest

Encryption Required

</Location>
```

Digest 认证与 `/etc/cups/passwd.md5` 文件定义的用户和密码配合。`passwd` 命令用于从 `passwd.md5` 文件添加、更改或删除账户。要将用户添加到默认系统组，输入：

```
passwd -a user ENTER

Password: password ENTER

Password again: password ENTER
```

添加后，用户可以通过输入以下命令更改密码：

```
passwd ENTER

Old password: password ENTER

Password: password ENTER

Password again: password ENTER
```

要从密码文件中删除用户，请输入以下命令：

```
lpppasswd -x user ENTER
```

## 组认证

`AuthClass` 指令指定要执行的组认证类型。表 5.4 列出了这些认证类：

| 类别 | 说明 |
| --- | --- |
| None | 不需要组身份。 |
| System | 需要是系统组的成员。 |
| Group | 需要是指定指定组的成员。 |

对于 System 认证，用户必须是系统组的成员，该组在您的系统中默认设置为 "root"、sys" 或 "system" 组。可以使用 `SystemGroup` 指令显式设置该组：

SystemGroup administrators

```
<Location /admin>

AuthType Basic

AuthClass System

Encryption Required

</Location>
```

对于 Group 认证，则使用 `AuthGroupName` 指令：

```
<Location /admin>

AuthType Basic

AuthClass Group

AuthGroupName administrators

Encryption Required

</Location>
```



## 基于地址的访问控制

基于地址的访问控制根据客户端的 IP 地址限制访问。`Allow` 和 `Deny` 指令指定允许或禁止访问资源的宿主机或网络：

```
<Location /printer/DeskJet>

Deny from all

Allow from 192.168.0.1

Allow from 192.168.0.2

Allow from 192.168.1.0/255.255.255

</Location>
```

这将允许 IP 地址为 192.168.0.1、192.168.0.2 和 192.168.1.0 的客户端访问 DeskJet 打印机。 192.168.1.1 网络的最后一行也可以写为：

`Allow from 192.168.1`

或者：

`Allow from 192.168.1.0/24`

`/24` 表示网络地址的前 24 位是有效的。

## 基于名称的访问控制

基于名称的访问控制根据主机名或域名限制访问。主机名从客户端的 IP 地址解析。要使基于名称的访问控制生效，你必须先启用主机名解析：

`HostNameLookups on`

主机名查找可能会因为对 IP 地址进行反向查找而产生巨大的性能开销。仅在绝对必要时才使用基于名称的访问控制。

之后，在 `Allow` 或 `Deny` 行中使用名称：

```
<Location /printer/DeskJet>

Deny from all

Allow from host.foo.bar

Allow from *.easyscom

Allow from .bar.net

</Location>
```

## 日志文件

CUPS 维护着三个记录服务器处理的访问、错误和页面的日志文件。日志文件通常位于 `/var/log/cups` 目录。

当日志文件达到 1MB 时通常会进行轮转。`MaxLogSize` 指令控制何时轮转：

- `MaxLogSize 0`
- `MaxLogSize 65536`
- `MaxLogSize 64k`
- `MaxLogSize 1024k`
- `MaxLogSize 1m`

> 设置为 0 将禁用日志轮转。

## 访问日志文件

访问日志文件包含 CUPS 服务器处理的所有 HTTP 请求日志。它是一个所谓的“常用日志格式”的文本文件，可以使用 Web 服务器分析工具进行分析。

每行的格式如下：
`method resource version\ status bytes`

```
127.0.0.1 - [20/May/1999:19:20:29 +0000] POST /admin/ HTTP/1.1" 401 0

127.0.0.1 - mike [20/May/1999:19:20:31 +0000] POST /admin/ HTTP/1.1" 200 0
```

宿主机通常是一个 IP 地址，除非你在 `cupsd.conf` 文件中启用了 `HostNameLookups` 指令。

在 CUPS 中，组字段始终包含 "-"。

用户字段是请求用户经过认证的用户名。如果请求未提供用户名和密码，该字段将包含 "-"。

`date-time:HH:MM:SS` 字段是请求的本地日期和时间，格式为 `[DD/MON/YYYY:HH:MM:SS +ZZZZ]`

其中 `ZZZZ` 是相对于格林尼治标准时间（也称为 GMT 或 ZULU）的小时和分钟偏移量。

`method` 字段是使用的 HTTP 方法（例如 GET、PUT 或 POST）。

`resource` 字段是请求资源的文件名。

`version` 字段是客户端使用的 HTTP规范版本。对于 CUPS 客户端，这始终是 HTTP/1.1。

`status` 字段包含请求的 HTTP 结果状态。通常为 200，但也可能是其他 HTTP 状态码。例如，在前例中401 是“未授权访问”状态。

`bytes` 字段包含请求的字节数。对于 POST 请求，`bytes` 字段包含从客户端接收到的字节数。

## 错误日志文件

错误日志列出了调度器的消息（错误、警告和页面）。

```
127.0.0.1 - [20/May/1999:19:20:29 +0000] POST /admin/ HTTP/1.1" 401 0

127.0.0.1 - mike [20/May/1999:19:20:31 +0000] POST /admin/ HTTP/1.1" 200 0
```

错误日志列出了调度器的消息（错误、警告和页面）。

| 级别 | 说明 |
| --- | --- |
| X | 紧急情况。 |
| A | 警报。 |
| C | 严重错误。 |
| E | 服务器无法执行操作。 |
| N | 注意消息。 |
| I | 信息消息。 |
| D | 调试消息。 |

注意：
不建议为大量的客户端机器配置打印队列，因为这会带来管理上的噩梦。对于繁忙的网络，请考虑对客户端组进行子网划分，并通过轮询（polling）中继打印机信息。

## 指定单个打印服务器

CUPS 可以配置为不带本地后台打印程序运行，并将所有作业发送到单个服务器。然而，如果该服务器宕机，打印功能将失效。请仅在绝对必要时使用此配置。

默认服务器通常为 "localhost"。要覆盖默认服务器，请创建一个名为 `/etc/cups/client.conf` 的文件，并在文件中添加如下行：

`ServerName server`

在该文件中。服务器名称可以是默认服务器的主机名或 IP 地址。

也可以按用户自定义默认服务器。要设置特定用户的服务器，请创建一个名为 `/.cupsrc` 的文件，并在文件中添加如下行：

`ServerName server`

在该文件中。服务器名称可以是默认服务器的主机名或 IP 地址。

## 打印队列自动配置

CUPS 支持对同一子网内的打印机进行自动配置。要配置同一子网内的打印机，请在服务器上设置 `BrowseAddress`，并在客户端上不进行任何操作。每个客户端应在 30 秒内自动看到可用打印机。随着打印机和服务器的添加或删除，打印机类列表会自动更新。

如果你还想查看其他子网上的打印机，请按照描述使用 `BrowsePoll` 指令。

注意：
`BrowseAddress` 指令会启用来自服务器的广播流量。默认配置每 30 秒广播一次打印机信息。虽然这些打印机信息占用的带宽不大（每台打印机约 80 字节），但服务器和打印机数量很大时流量可能会累积。

使用 `BrowseInterval` 和 `BrowseTimeout` 指令来调整添加到网络负载的数据量。此外，可以使用子网来减少大型网络“骨干”传输的流量。

## 指定多个打印服务器

如果您在不同的子网上拥有 CUPS 服务器，则您应该配置 CUPS 轮询这些服务器。轮询可以在无需对客户端进行显著配置的情况下提供自动配置的优势，同一子网上的多个客户端可以共享配置信息。

通过 `/etc/cups/cupsd.conf` 文件中的一个或多个 `BrowsePoll` 指令启用轮询。每行 `BrowsePoll` 都显示服务器的主机名或 IP 地址：

```
BrowsePoll server
```

可以使用多行 `BrowsePoll` 来轮询多个 CUPS 服务器。为了限制从客户端机器进行的轮询量，您可以只让一个客户端进行轮询，并与同一子网上的其他建立关联（下文描述）。

## 将打印机中继到其他客户端

当客户端和服务器分布在多个子网时，轮询方法效率较低。CUPS 提供了 `BrowseRelay` 指令，允许单个客户端将打印机中继（广播）到本地子网。图 6.1 显示了一个具有多个子网的典型企业网络。

服务器 A 和服务器 B 分位于子网 1 和子网 2，而客户端位于子网 3。为子网 3 中的所有客户端提供打印机，客户端 C 将在 `/etc/cups/cupsd.conf` 中配置以下指令：

```
## 轮询两个服务器
BrowsePoll ServerA

BrowsePoll ServerB
```

```
## 将打印机中继到本地子网
BrowseRelay 127.0.0.1 192.168.0.255
```

`BrowseRelay` 行提供了一个源地址和掩码。任何来自匹配地址的浏览包都将发送到通用广播地址。在这种情况下，我们将来自本地机器 (`127.0.0.1`) 的包中继到其他客户端。

当通过轮询发现打印机时，它们将通过子网 3 的广播从客户端 C 中继到其余客户端。其余客户端可以使用标准的 `cupsd.conf` 配置。

## 客户端配置

# 第 6 章
# 113

图 6.1
具有多个子网的典型企业网络。

注意：
`BrowseRelay` 指令也可用于将浏览包从一个网络接口中继到另一个。例如，如果例中的客户端 C 同时连接到子网 1 和子网 2 的网络接口，它可以专门使用 `BrowseRelay` 指令：

```
## 将打印机从子网 1 和 2 中继到子网 3
BrowseRelay 192.168.1.1 192.168.3.255

BrowseRelay 192.168.2.1 192.168.3.255
```

## 负载均衡与故障备

当使用服务器轮询或广播时，CUPS 客户端自动可以将多个服务器上相同的打印机合并为单一的隐式类队列。客户端假设多个服务器上名称相同的打印机实际上是同一台打印机，或由多台机器服务的同一类型打印机。

如果你有两个打印机 `LaserJet@ServerA` 和 `LaserJet@ServerB`，客户端上会自动创建一个名为 `LaserJet` 的隐式类，以引用两者。如果客户端有一个名为 `LaserJet` 的本地打印机，则会创建一个隐式类 `AnyLaserJet`。

客户端将在服务器之间切换，并在服务器宕机时自动停止发送作业，提供负载均衡效果和带有自动切换的故障备。

向 `/etc/cups/cupsd.conf` 文件中添加以下行以禁用隐式类：

```
Classes off
```

> 注意：
隐式类默认启用。如果你只想为某些打印机提供类而不是所有，则应该手动设置打印机类。

## 从 LPD 客户端打印

CUPS 支持基于 LPD 的客户端。通过 LPD，你可以向特定打印机打印、列出队列状态等。LPD 不支持自动客户端配置和打印机选项，因此你必须手动配置每个客户端。

`cups-lpd` 程序支持 LPD 并用作“inetd”类型的守护进程。如果你使用的是超级进程（大多数 UNIX 版本），编辑 `inetd.conf` 文件并添加如下行：

```
printer stream lpd
```

添加此行后，向 inetd 进程发送 HUP 信号或重启系统。在 IRIX 和某些 Linux 服务器上，命令为：

```
killall -HUP inetd
```

对于其他 UNIX 系统，在找到 inetd 的 ID 后使用 `kill` 命令：

```
kill -HUP pid
```

许多 Linux 系统使用较新的 inetd 守护进程，将此信息存储在 `/etc/inetd.conf` 或 `/etc/inetd.d/cups` 中：

```
service printer {

  socket_type = stream

  protocol = tcp

  wait = no

  user = 1lp

  server = /usr/lib/cups/daemon/cups-lpd

}
```

inetd 守护进程会检查配置文件的更改并根据需要自动读取它们。

## 从 Mac OS 客户端打印

CUPS 不直接提供 Mac 支持。然而，一些免费和商业软件包提供了支持。

## Columbia Appletalk Package (CAP)

CAP 可能是最老的 EtherTalk 服务器了。它可能是可用解决方案中移植性最好的，但速度最慢。

由于 CAP Laserwriter (`lswrv`) 不支持指定 PPD 文件，我们不建议在 CUPS 中使用 CAP。然而，你可以通过以下命令运行该程序进行有限打印：

```
lswrv -n "Share Name" -p name -a /usr/lib/adicts -f /usr/lib/LW+Fonts
```

其中 "Share Name" 是你共享打印机时使用的名称，`name` 是 CUPS 打印队列的名称。

## XINET KA/Spool

KA/Spool 是在高端 Unix 服务器上流行的解决方案。要将你的系统作为 Mac OS 客户端的打印服务器，请使用 `/usr/admin/appletalk/services` 中的 `paparser` 配置每个打印机，并在 `/etc/cups/ppd` 目录指定相应的 PPD 文件。对于名为 `MyPrinter` 的打印机，条目看起来如下：

```
/usr/etc/appletalk/paparser -I -L -P /etc/cups/ppd/MyPrinter.ppd
- "Printer Description MyPrinter"
```

## NetATalk

NetATalk 是一个适用于 Linux 和 Solaris 的流行免费 EtherTalk 软件包。要将您的系统作为 Mac OS 客户端的打印服务器，请在 `papd.conf` 文件中配置每台打印机，并为每台打印机在 `/etc/cups/ppd` 目录下指定相应的 PPD 文件。对于名为 `MyPrinter` 的打印机，条目如下：

```
Printer Description:MyPrinter@Server:
:==/usr/bin/lp -d MyPrinter:
:op=daemon:\npd=/etc/cups/ppd/MyPrinter.ppd
```

## 从 Windows 客户端打印

尽管 CUPS 不提供 Windows 支持，但免费的 SAMBA 软件包提供了支持。SAMBA 2.0.6 是第一个支持 CUPS 的 SAMBA 版本。您可以从以下网站下载 SAMBA：

http://www.samba.org

Windows 98、Me 和 2000 也支持用于打印的互联网打印协议（IPP）。

## 配置 SAMBA 2.0.x

要要为 CUPS 配置 SAMBA 2.0.0-2.0.5，请编辑 `smb.conf` 文件并将现有的打印命令和选项替换为以下行：

```
printing = sysv
printcap = lpstat
print command = lp -d$p -oraw %; rm -f %s
```

要为 CUPS 配置 SAMBA 2.0.6 和 2.0.7，请编辑 `smb.conf` 文件并将现有的打印命令和选项替换为以下行：

```
printing = cups
printcap = lpstat
```

这就足够了！远程用户现在能够浏览并打印到您系统上的打印机了。

## 配置 SAMBA 2.2.x

SAMBA 2.2.0 及更高版本包含了从 Windows 客户端下载打印机驱动的支持。首先编辑 `smb.conf` 文件，将现有的打印命令和选项替换为以下行：

```
printing = cups
printcap = cups
```

然后运行 `cupsaddssm` 程序添加您想要共享的打印机：

```
cupsaddssm name 输入
```

其中 `name` 是您想要共享的打印机名称。要共享所有打印机，请输入：

```
cupsaddssm -a 输入
```

## 使用 IPP 配置 Windows 客户端

如果您使用 Windows 98、Me 或 2000，可以使用打印机的 IPP URI 将打印机作为网络打印机：

```
ipp://server/printers/name
```



`server` 是服务器的主机名或 IP 地址。`name` 是服务器上打印机的名称。

## 总结

CUPS 支持许多类型的客户端配置，包括非 CUPS 客户端。当设置了两个或多个带有打印机的服务器时，基本的 CUPS 客户端配置提供了远程打印机的自动负载均衡和故障保护。当客户端和服务器位于不同的子网时，可以使用轮询和中继来连接子网并将打印机发布到客户端。

LPD 客户端可以提交作业，但缺乏发送作业选项或参与自动配置的能力。

MacOS 客户端受多种第三方程序支持，通常可以为客户端提供 PPD 文件并支持作业选项。

Windows 客户端通过 SAMBA 或 IPP 支持。SAMBA 2.2.x 使用 `cupsaddsmb` 命令下载打印机驱动程序。旧版本的 SAMBA 和 IPP 需要使用本地 Windows 打印机驱动程序。

# 第二部分

## 互联网打印协议 (IPP)

- 7 IPP 概述
- 8 IPP 请求的结构
- 9 打印机对象
- 10 作业对象
- 11 订阅对象
- 12 CUPS 对 IPP 的扩展

# 第 7 章

## 互联网打印协议简介

本章提供了互联网打印协议的背景信息，这是由互联网工程任务组（IETF）的网络打印协议。IPP 成了通用 Unix 系统的基础。

## IPP 历史

IPP 工作组由互联网工程任务组（IETF）和打印机工作组（PWG）于 1997 年创建，旨在开发一种标准的网络打印协议，满足互联网社区和当前技术的需求。

# 线打印机守护进程协议

IPP 工作组做的第一件事是抛弃了 RFC 1179 中描述的旧标准打印机守护进程（LPD）协议。LPD 协议基于 20 世纪 70 年代为 Unix 开发的示例实现，用于支持向线打印机打印，从那时起没有变化。

图 7.1 显示了一个典型的 LPD 会话。LPD 客户端连接到服务器并向服务器发送打印文件命令。服务器随后返回 OK 或 FAIL 状态，然后客户端发送控制文件和一个或多个包含打印数据的文件。服务器对每个文件返回 OK 或 FAIL，然后对整个打印命令返回最终的 OK 或 FAIL。每个连接只能处理一个命令。

| 客户端 | 服务器 |
| --- | --- |
| 接收打印作业 | OK |
| 发送控制文件 | OK |
| 控制文件 | OK |
| 发送数据文件 | OK |
| 数据文件 | OK |

**图 7.1**
典型的 LPD 协议会话。

如从图 7.1 所示，会话中没有验证步骤——最初的实现依赖于预留的端口号（721–731）来确保客户端（用户）是从受信任的系统打印的。由于只有 root 用户（或以 root 身份运行的应用程序）可以预留 1024 以下的端口，这在当时被认为是足够的安全性。

## 互联网打印协议简介

随着计算机的发展，IPP 的局限性变得显而易见。当带有打印机的多个服务器设置时，IPP 成了通用系统的基础。当客户端和服务器位于不同的子网时，可以使用轮询和中继来连接子网并将打印机发布到客户端。

LPD 客户端可以提交作业，但缺乏发送作业选项或参与自动配置的能力。

MacOS 客户端受多种第三方程序支持，通常可以为客户端提供 PPD 文件并支持作业选项。

Windows 客户端通过 SAMBA 或 IPP 支持。SAMBA 2.2.x 使用 `cupsaddsmb` 命令下载打印机驱动程序。旧版本的 SAMBA 和 IPP 需要使用本地 Windows 打印机驱动程序。

# 总结（注：此处为原文重复部分）

CUPS 支持许多类型的客户端配置，包括非 CUPS 客户端。当设置了两个或多个带有打印机的服务器时，基本的 CUPS 客户端配置提供了远程打印机的自动负载均衡和故障保护。如果您使用 Windows 98、Me 或 2000，您可以使用打印机的 IPP URI 将打印机作为网络打印机：

```
ipp://server/printers/name
```



`server` 是服务器的主机名或 IP 地址。`name` 是服务器上打印机的名称。

# 总结

CUPS 支持许多类型的客户端配置，包括非 CUPS 客户端。当设置了两个或多个带有打印机的服务器时，基本的 CUPS 客户端配置提供了远程打印机的自动负载均衡和故障保护。

# 图 7.3
IPP 对象之间的关系。

![](img/b159ac7fe2135643dc37ccfeef6d3980_151_0.png)

这些对象的每个关系和操作都可以由有限状态机驱动，使得 IPP 在各种硬件上都极易实现。

## 扩展

IPP 支持从 HTTP 传输层到低层 IPP 协议本身的灵活扩展机制。可以为属性、身份验证、加密、文档格式、通知、操作和值类型添加扩展，而不会破坏与 IPP 标准的兼容性。这种扩展机制允许 IPP 成为一个一个活跃的、不断增长的标准，同时不会牺牲与旧实现的兼容性，使其成为比古老的 LPD 更好的长期网络打印解决方案。

## 参考文献

IPP 由 IETF 标准的几篇“意见征求”（RFC）论文以及来自 PWG 的几篇标准论文进行了描述。表 7.1 描述了当前的 IETF 规范：

## 表 7.1 IETF IPP 规范

| 文档 | 描述 |
| --- | --- |
| RFC 2568 互联网打印协议模型和协议结构的原理 | 描述了为什么 IPP 采用这样的设计 |
| RFC 2567 互联网打印协议的设计目标 | 描述了互联网打印协议的最终目标 |

## 表 7.1 续表

| 文档 | 描述 |
| --- | --- |
| RFC 2569 LPD 与 IPP 协议之间的映射 | 描述了如何将 IPP 映射到 LPD，反之亦然 |
| RFC 2911 IPP/1.1: 模型与语义 | 描述了 IPP 的所有打印机和作业对象的操作及属性 |
| RFC 2910 IPP/1.1: 编码与 IPP/1.1: 实现指南 | 描述了低层 IPP 协议 |
| IPP: IPP 作业和打印机管理操作 | 描述了用于打印机和作业管理的 IPP 扩展 |
| IPP: 作业和打印机组操作 | 描述了用于控制打印机和作业的 IPP 扩展 |
| IPP: 作业进度属性 | 描述了用于详细监控作业状态的新型作业属性 |
| IPP: 集合属性语法 | 描述了一种被某些扩展使用的新集合值类型 |
| IPP: IPP 事件通知规范 | 描述了 IPP 通知机制和订阅对象 |
| 用于事件通知的协议/1.0 的 inod 递送方法 | 描述了 inod（广播）通知方案 |
| IPP: ippget 事件通知递送方法 | 描述了 ippget（轮询）通知方案 |
| IPP: mailto 通知递送方法 | 描述了 mailto（电子邮件）通知方案 |

PWG 还有几项被 PWG 成员认可的额外标准，以及关于在使用蓝牙协议的无线设备上使用 IPP 的实验性文档。

您可以在以下网站找到当前的 IPP 文档：

http://www.pwg.org/ipp/

## 总结

IPP 是 RFC 1179 中描述的 LPD 协议的替代方案。IPP 的设计是一个相当易于实现的协议，同时提供了许多高级打印功能。IPP 扩展机制允许 IPP 能够增长以支持新技术，同时保持与现有的 IPP 实现的兼容性。

## 第 8 章

## IPP 请求的构造

本章描述了互联网打印协议的低层格式，包括请求或响应中的每个值是如何编码的，以及数据如何在客户端和服务器之间交换。

## 剖析 IPP 请求

每个 IPP 请求都由以下部分组成：

- 一个 HTTP 请求
- 一个 IPP 请求消息
- 可选的额外（文档）数据
- 一个 HTTP 响应
- 一个 IPP 响应消息

后续章节描述了这些每个部分。

## HTTP 请求

HTTP 请求是一个包含类型为 `application/ipp` 数据的 POST 请求。每个 POST 包含一个 IPP 请求消息，并可能包含 Print-Job 请求或 Send-Document 请求的文档数据。图 8.1 显示了数据流。

![](img/b159ac7fe2135643dc37ccfeef6d3980_154_0.png)

由于 IPP 要求完全符合 HTTP/1.1 标准，IPP 请求可以使用 `Content-length` 字段一次性发送，也可以使用分块传输（chunking）增量发送。POST 的结果也是类型为 `application/ipp` 的数据，由 IPP 响应消息组成。

请求和响应都使用通用格式，以固定长度的头部开始，随后是一系列属性。IPP 消息中的数据是字节对齐的，因此在您的程序中，通常必须从适当对齐的数据结构中读取和写入数据。

## 请求头部

请求头部由 8 字节二进制数据组成，如图 8.2 所示。

| IPP 主版本 | IPP 小版本 | 操作代码 |
| --- | --- | --- |
| 请求 ID | | |

图 8.2

IPP 请求头部由 8 字节二进制数据组成。

前两个字节包含 IPP 版本号，`01 00` 代表 IPP/1.0，或者 `01 01` 代表 IPP/1.1。通常情况下，您应该发送 IPP/1.1 请求，除非服务器响应了 `server-error-version-not-supported`。

第 3-4 字节包含操作代码，这是一个网络（大端序）字节序的 16 位整数。表 8.1 列出了当前定义的代码。

## 表 8.1 IPP 操作代码

| 代码 | 名称 | 描述 |
| --- | --- | --- |
| 0x0002 | Print-Job | 打印单个文件 |
| 0x0003 | Print-URI | 打印单个 URI |
| 0x0004 | Validate-Job | 验证作业 |
| 0x0005 | Create-Job | 创建作业 |
| 0x0006 | Send-Document | 向作业中添加文件 |
| 0x0007 | Send-URI | 向作业中添加 URI |
| 0x0008 | Cancel-Job | 取消作业 |
| 0x0009 | Get-Job-Attributes | 获取作业属性 |
| 0x000A | Get-Jobs | 获取作业列表 |
| 0x000B | Get-Printer-Attributes | 获取打印机属性 |
| 0x000C | Hold-Job | 保持作业 |
| 0x000D | Release-Job | 释放作业 |
| 0x000E | Restart-Job | 重启作业 |
| 0x0010 | Pause-Printer | 暂停打印 |
| 0x0011 | Resume-Printer | 恢复打印 |
| 0x0012 | Purge-Job | 清除作业 |
| 0x0013 | Set-Printer | 设置打印机 |
| 0x0014 | Set-Job | 设置作业 |
| 0x0015 | Get-Printer-Supported | 获取打印机支持的值 |

## 第二部分 打印协议

## 表 8.1 续表

| 代码 | 名称 | 描述 |
| --- | --- | --- |
| 0x0016 | Create-Printer-Subscription | 创建打印机订阅 |
| 0x0017 | Create-Job-Subscription | 创建作业订阅 |
| 0x0018 | Get-Subscription-Attributes | 获取订阅属性 |
| 0x0019 | Get-Subscriptions | 获取订阅列表 |
| 0x001A | Renew-Subscription | 续订订阅 |
| 0x001B | Cancel-Subscription | 取消订阅 |
| 0x001C | Get-Notifications | 使用 ippget 获取通知 |
| 0x001D | Send-Notifications | 使用 ippsend 获取通知 |
| 0x0021 | Get-Printer-Support-Files | 获取打印机支持的文件 |
| 0x0022 | Enable-Printer | 允许向打印机提交作业 |
| 0x0023 | Disable-Printer | 禁止向打印机提交作业 |
| 0x0024 | Pause-After-Current-Job | 在完成当前作业后暂停打印 |
| 0x0025 | Hold-New-Jobs | 保持所有新作业 |
| 0x0026 | Release-Held-Jobs | 释放（启动）任何保持的作业 |
| 0x0027 | Deactivate-Printer | 停止打印机并允许进行更改 |
| 0x0028 | Activate-Printer | 启动打印机并允许进行更改 |
| 0x0029 | Restart-Printer | 重启打印机，重启任何被 Deactivate 停止的作业 |
| 0x002A | Shutdown-Printer | 关闭打印机电源 |
| 0x002B | Startup-Printer | 打开打印机电源 |
| 0x002C | Reprocess-Job | 重新打印已完成的作业 |
| 0x002D | Cancel-Current-Job | 取消打印机上的当前作业 |
| 0x002E | Suspend-Current-Job | 暂停打印机上的当前作业 |
| 0x002F | Resume-Job | 重启打印机上的当前作业 |
| 0x0030 | Promote-Job | 在队列中优先于其他作业打印 |
| 0x0031 | Schedule-Job-After | 在另一个作业之后打印 |
| 0x0401 | CUPS-Get-Default | 获取默认打印机 |
| 0x0402 | CUPS-Get-Printers | 获取打印机列表 |
| 0x0403 | CUPS-Add-Printer | 在服务器上添加或修改打印机 |
| 0x0404 | CUPS-Delete-Printer | 从服务器上删除打印机 |
| 0x0405 | CUPS-Get-Classes | 获取打印类列表 |
| 0x0406 | CUPS-Add-Class | 在服务器上添加或修改类 |
| 0x0407 | CUPS-Delete-Class | 从服务器上删除类 |
| 0x0408 | CUPS-Accept-Jobs | 允许向打印机或打印类提交新作业（类似于新的 Enable-Printer 操作） |

## 表 8.1 续

| 代码 | 名称 | 描述 |
| --- | --- | --- |
| 0x4009 | CUPS-Reject-Jobs | 拒绝发送到打印机或打印机类的新打印作业（类似于新的 Disable-Printer 操作） |
| 0x400A | CUPS-Set-Default | 设置默认打印机 |
| 0x400B | CUPS-Get-Devices | 获取可用打印机设备列表 |
| 0x400C | CUPS-Get-PPDS | 获取可用的打印机驱动程序列表 |
| 0x400D | CUPS-Move-Job | 将打印作业移动到另一个打印机或打印机类 |

字节 5–8 包含请求 ID，这是一个网络字节序（大端序）的 32 位整数。请求 ID 由客户端生成并由服务器返回，以便客户端确定哪个响应对应哪一个请求。

# 什么是大端和小小端？

大端和小小端是指大于 1 字节的数字或指针值中的字节顺序。通过大多数网络协议发送的多字节数字采用大端序，因此“网络字节序”术语等同于大端序。

大端序数字以最高字节（高位）存储：一个 32 位整数值 1234 在内存中存储为字节 0, 0, 4 和 2¹⁰。

小端序数字以最低有效字节（低位）存储：一个 32 位整数值 1234 在内存中存储为字节 2¹⁰, 4, 0 和 0。

大端和小小端的术语源自 Swift 语言中的《格列夫游记》，这借用了丹尼·科恩（Danny Cohen）著名的论文《论圣战与和平的诉求》。

## IPP 组和属性

IPP 组紧跟在请求头之后。每个组或属性都以一个字节的值标签开头。某些值标签引入属性组，而另一些则表示属性值的开始。属性标签之后是属性名称和属性值本身（参见第 8.3 节）。

请求以 Get-Jobs 请求的标准 8 字节头开始。接下来是一个开始操作属性的组标签 (01) 和一个开始字符集值的字符集标签 (47)。字符集标签之后是属性长度 (18) 和名称字符串 ("attributes-charset")。在值字符串 ("utf-8") 之后，该属性完成。请求中的所有属性都重复此过程，并并使用属性结束标签 (03) 结束。

# 互联网打印协议

| 01 01 | IPP/1.1 版本号 |
| 00 0A | Get-Jobs |
| 00 00 01 | 请求 ID #1 |
| 01 | 操作组标签 |
| 47 | 字符集 |
| 00 12 | 名称 = 18 |
| "attributes-charset" | 值长度 = 5 |
| 00 05 | 自然语言 |
| "utf-8" | 名称长度 = 27 |
| 48 | |
| 00 1B | 值长度 = 2 |
| "attributes-natural-language" | |
| 00 02 | uri |
| "en" | 名称长度 = 11 |
| 45 | |
| 00 0B | 值长度 = 13 |
| "printer-uri" | |
| 00 0D | |
| "ipp://foo/bar" | 属性结束标签 |
| 03 | |

图 8.3
请求中的 IPP 属性数据。

# 组

IPP 目前定义了表 8.2 所示的七种组标签。每个组标签用于该组的第一个属性一次；如果该组中未提供属性，则省略该组标签。属性结束标签是一个特殊的组标签，用作 IPP 消息的最后一个标签。

除了属性结束标签外，IPP 请求中的所有标签必须以升序发送（与表 8.2 所示的顺序相同）。

## 表 8.2 IPP 组标签

| 标签 | 名称 | 描述 |
| --- | --- | --- |
| 0x01 | operation-attributes-tag | 操作属性组 |
| 0x02 | job-attributes-tag | 作业属性组 |
| 0x03 | end-of-attributes-tag | IPP 消息的结束标签 |
| 0x04 | printer-attributes-tag | 打印机属性组 |
| 0x05 | unsupported-attributes-tag | IPP 服务器返回的不支持属性的组 |

## 表 8.2 续

| 标签 | 名称 | 描述 |
| --- | --- | --- |
| 0x06 | subscription-attributes-tag | 订阅属性组（创建订阅时使用） |
| 0x07 | event-notification-attributes-tag | 事件属性组（用于报告来自订阅的事件） |

# 属性

在每个属性组内部是属性本身。每个属性都以一个字节的标签开头（参见表 8.3），随后是网络字节序（大端序）的 16 位名称长度、名称中的字符、网络字节序（大端序）的 16 位长度以及数据值。

## 表 8.3 IPP 值标签

| 代码 | 名称 | 描述 |
| --- | --- | --- |
| 0x16 | delete-attribute | 删除命名的属性（仅限 IPP 请求） |
| 0x21 | integer | 网络字节序（大端序）的 32 位符号整数。 |
| 0x22 | boolean | 一个字节整数，0 表示假值，1 表示真值 |
| 0x23 | enum | 网络字节序（大端序）的 32 位符号整数枚举。 |
| 0x30 | octetString | 最多 32767 字节的任意字符串。 |
| 0x31 | dateTime | 11 字节 RFC 1903 格式的日期和时间。 |
| 0x32 | resolution | 9 分辨率值，由两个网络字节序（大端序）的 32 位符号整数组成，代表水平和垂直分辨率。 |
| 0x33 | rangeInteger | 两个网络字节序（大端序）的 32 位符号整数。 |
| 0x34 | begCollection | 集合的开始。 |
| 0x35 | textWithLanguage | 带有语言的文本。值 3 表示英寸，值 4 表示厘米。 |
| 0x36 | nameWithLanguage | 带有语言的名称。网络字节序（大端序）的长度，文本字符串。 |
| 0x37 | endCollection | 集合的结束。 |

## 表 8.3 续

| 代码 | 名称 | 描述 |
| --- | --- | --- |
| 0x41 | textWithoutLanguage | 默认文本。 |
| 0x42 | nameWithoutLanguage | 默认名称。 |
| 0x43 | keyword | 关键字。 |
| 0x44 | uri | URI。 |
| 0x45 | uriScheme | URI 方案。 |
| 0x46 | charset | 字符集。 |
| 0x47 | naturalLanguage | 自然语言。 |
| 0x48 | defaultLanguage | 默认语言。 |
| 0x49 | mimeType | MIME 类型。 |
| 0x4A | member | 成员。 |

## 数组

IPP 支持值数组；第一个值是元素数量。图 8.4 显示了数组值。

## 响应

IPP 响应的格式与 IPP 请求完全相同，只是头部中的操作代码替换为状态码。

## 状态码

状态码是一个网络字节序（大端序）的 16 位整数，定义请求的成功失败。大多数错误包含定义特定错误的属性（例如 printer-reasons 属性）。表 8.4 显示了可能的状态码。

| 代码 | 描述 |
| --- | --- |
| 0x0000 | 正常。 |
| 0x0001 | 忽略了某些属性。 |
| 0x0002 | 正常，但某些属性之间冲突。 |
| 0x0003 | 正常，但未创建订阅。 |
| 0x0004 | 正常，但接收者无法处理所有事件。 |
| 0x0005 | 正常，但事件数量超过打印机发送能力。 |
| 0x0006 | 正常，但接收者想要取消订阅。 |
| 0x0300 | redirection-other-site 将 get 重定向到不同的服务器。 |
| 0x0400 | 客户端请求包含无效数据。 |
| 0x0401 | 禁止客户端执行该操作。 |
| 0x0402 | 客户端未身份验证，需要验证后才能允许操作。 |
| 0x0403 | 客户端无权限执行该操作。 |
| 0x0404 | 操作无法成功。 |
| 0x0405 | 客户端请求未及时收到。 |
| 0x0406 | 客户端请求涉及的对象不存在。 |
| 0x0407 | 请求的对象已不可用。 |
| 0x0408 | 客户端包含额外数据过大。 |
| 0x0409 | 客户端请求包含的属性值过大。 |

图 8.4
数组值。

# 表 8.4 续

| 代码 | 名称 | 描述 |
| --- | --- | --- |
| 0x040A | client-error-document-not-supported | 不支持文档格式。 |
| 0x040B | client-error-attributes-values-not-supported | 请求包含不支持的属性或值。 |
| 0x040C | client-error-uri-scheme-supported | URI 属性中的 URI 方案不支持。 |
| 0x040D | client-error-charset-not-supported | 客户端请求使用了不支持的字符集。 |
| 0x040E | client-error-conflicting-attributes | 客户端请求包含冲突的属性。 |
| 0x040F | client-error-compression-not-supported | 客户端请求使用了不支持的压缩类型。 |
| 0x0410 | client-error-compression-error | 压缩数据包含错误。 |
| 0x0411 | client-error-document-format-error | 文档数据包含错误。 |
| 0x0412 | client-error-document-access-error | 无法访问远程文档。 |
| 0x0413 | client-error-attributes-not-settable | 客户端请求中指定的属性无法更改。 |
| 0x0414 | client-error-ignored-all-subscriptions | 服务器在 Create-Job、Print-Job、Print-URI 或 Reprocess-Job 操作中无法创建订阅。 |
| 0x0415 | client-errors-too-many-subscriptions | 服务器无法再创建订阅订阅。 |
| 0x0416 | client-error-ignored-all-notifications | 通知接收接收者无法收集任何事件。 |
| 0x0417 | client-error-print-support-file-not | 找不到打印机支持文件（驱动程序）。 |
| 0x0500 | server-error-internal-error | 服务器发生内部错误。 |
| 0x0501 | server-error-operation-not-supported | 服务器不支持请求的操作。 |
| 0x0502 | server-error-service-unavailable | 由于临时状况无法执行请求的操作。 |
| 0x0503 | server-error-version-not-supported | 请求头中的 IPP 版本号不支持。 |
| 0x0504 | server-error-device-error | 打印机对象无法打印任务。 |
| 0x0505 | server-error-temporary-error | 由于临时服务器错误无法执行请求的操作。 |

# 表 8.4 续

| 代码 | 名称 | 描述 |
|---|---|---|
| 0x0506 | server-error-accepting-jobs | 打印机对象此时不接受任务。 |
| 0x0507 | server-error-busy | 由于负载过高，服务器暂时不可用。 |
| 0x0508 | server-error-job-canceled | 打印任务在从客户端接收所有文档数据之前已取消。 |
| 0x0509 | server-error-multiple-document-not-supported | 服务器不支持在打印任务中包含多个文档。 |
| 0x050A | server-error-printer-deactivated | 打印机处于离线状态或已关机。 |

# 值标签

当 IPP 请求中的属性无法被服务器使用时，响应将使用特殊的值标签包含这些属性。这些属性可以在“不支持组”（unsupported-attributes-tag）中找到，不同的值标签有助于指示属性为何被拒绝。表 8.5 显示了在响应中使用的额外值标签。

# 表 8.5 响应中的 IPP 值标签

| 代码 | 名称 | 描述 |
|---|---|---|
| 0x10 | unsupported | 属性名不支持。 |
| 0x12 | unknown | 命名属性的值当前尚未知。 |
| 0x13 | no-value | 命名属性没有关联的值。 |
| 0x15 | not-settable | 无法设置命名属性的值。 |
| 0x17 | admin-define | 值由管理员定义且无法更改。 |

# 包含多个对象的响应

Get-Jobs、Get-Notifications、Get-Subscriptions、CUPS-Classes、Get-Pinters 操作的 IPP 响应可能包含多个对象的属性，这些属性会多次引入相同的组标签。然而，对象属性内的组标签仍按升序发送。请参见图 8.5 关于 Get-Jobs 操作的示例。

# 互联网打印协议

| 01 01 | IPP/1.1 版本号 |
| 00 00 | successful-ok |
| 00 00 00 01 | 请求 ID #1 |
| 01 | operation-group-tag |
| 47 | charset |
| 00 12 | name length = 18 |
| "attributes-charset" | |
| 00 05 | value length = 5 |
| "utf-8" | naturalLanguage |
| 00 1B | name length = 27 |
| "attributes-charset-language" | |
| 00 02 | value length = 2 |
| "en" | operation-group-tag |
| 45 | uri |
| 00 07 | name length = 7 |
| "job-uri" |
| 00 14 | value length = 20 |
| "ipp://printer/jobs/1" | |
| 21 | integer |
| 00 06 | name length = 6 |
| "job-id" | |
| 00 04 | value length = 4 |
| 00 00 | value = 1 |
| 23 | enum |
| 00 09 | name length = 9 |
| "job-state" | |
| 00 04 | value length = 4 |
| 00 05 | value = 3 |
| 02 | attributes-tag |
| 45 | uri |
| 00 07 | name length = 7 |
| "job-uri" | |
| 00 14 | value length = 20 |
| "ipp://printer/jobs/2" | |
| 21 | integer |
| 00 06 | name length = 6 |
| "job-id" | |
| 00 04 | value length = 4 |
| 00 00 | value = 2 |
| 23 | enum |
| 00 09 | name length = 9 |
| "job-state" | |
| 00 04 | value length = 4 |
| 00 00 | value = 1 |
| 02 | attributes-tag |
| 45 | attributes-tag

一个 IPP 请求的结构

```



一个 IPP 请求的剖析

图 8.5 Get-Jobs 响应

## 总结

IPP 请求和响应使用常见的二进制格式。多字节整数值采用网络字节序（大端）。每个属性组必须通过 HTTP POST 方法发送，内容类型为 `application/ipp`。每个请求还带有额外数据（如打印文件）。每个响应都有状态码和其他可能的属性，以完整描述任何错误状况。

166

本页留白

167

# 9 章

## 打印机对象

本章介绍了为 IPP 打印机对象提供的属性操作。

### 什么是打印机对象？

打印机对象代表接受并打印任务对象的单个打印机。打印机对象还可以关联订阅对象。

每个打印机对象始终处于三种状态之一：空闲（idle）、处理中（processing）或停止（stopped）。空闲打印机对象是因为没有打印任务。当新对象可用时，打印机对象开始打印。

处于处理状态的打印机对象正在打印一个任务对象。能够同时打印多个对象的打印机通常是大幅打印机或可以沿介质宽度输出以提高速度的打印机。大多数 IP 实现一次只打印一个任务。

最后，停止打印机对象在发生物理错误（例如缺墨水或纸张）且管理员决定在处理期间将其离线时停止。

### 必要属性

打印机对象有多个关联属性。这些属性在 IPP 服务器上始终可用，但如果未定义或实现不支持，其值可能为空。表 9.1 列出了打印机对象的必要属性。

表 9.1 打印机对象的必要属性

| 属性 | 类型 | 描述 |
|---|---|---|
| `charset-configured` | charset | 文本属性的默认字符集 |
| `charset-supported` | 1setOf charset | 支持的字符集 |
| `compression-supported` | 1setOf type3 keyword | 服务器支持的压缩类型 |
| `copies-default` | integer (1:MAX) | 默认生成的副本数 |
| `copies-supported` | rangeOfInteger (1:MAX) | 支持的副本数数范围 |
| `document-format-default` | mimeMediaType | 打印任务的默认文档格式 |
| `document-format-supported` | 1setOf mimeMediaType | 支持的文档格式 |

# 表 9.1 续

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `finishes-default` | 1setof type2 enum | 应用于文档页的默认结束状态 |
| `finishes-supported` | 1setof type2 enum | 文档页可用的结束状态 |
| `generated-natural-language-supported` | 1setof nullLanguage | 支持的语言 |
| `ipp-versions-supported` | 1setof type2 keyword | 打印机对象支持的版本号 |
| `job-hold-until-default` | type3 keyword | name | 新任务的默认保持时间 |
| `job-hold-until-supported` | 1setof (type3 keyword | name) | 新任务支持的保持时间 |
| `job-priority-default` | integer (1:100) | 默认打印优先级 |
| `job-priority-supported` | integer (1:100) | 支持的最大任务优先级值 |
| `job-sheets-default` | type3 keyword | name | 打印任务时默认的作业页设置 |
| `job-sheets-supported` | 1setof (type3 keyword | name) | 支持的作业页设置 |
| `media-default` | type3 keyword | name | 打印任务时使用的默认介质 |
| `media-ready` | 1setof type3 keyword | name | 哪些介质已准备好打印 |
| `media-supported` | 1setof type3 keyword | name | 支持的介质类型 |
| `multiple-document-handling-default` | type2 keyword | 打印复份时的默认文档处理方式 |
| `multiple-document-handling-supported` | 1setof type2 keyword | 支持的文档处理类型 |
| `natural-language-configured` | naturalLanguage | 返回属性的配置语言 |
| `number-up-default` | integer (1:MAX) | 每个输出上打印的文档页数 |
| `number-up-supported` | 1setof integer(1:MAX) | rangeOfInteger(1:MAX) | 支持的份打（number-up）值 |
| `operations-supported` | 1setof type2 enum | 打印机对象支持的操作 |
| `orientation-requested-default` | type2 enum | 文档页的默认方向 |
| `orientation-requested-supported` | 1setof type2 enum | 支持的方向 |

# 表 9.1 续

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `pages-ranges-supported` | boolean | 打印文档时是否支持页码过滤 |
| `pdl-override-supported` | type2 keyword | IPP 属性是否覆盖打印文件中的命令 |
| `printer-accepting-jobs` | boolean | 打印机对象是否接受新任务 |
| `printer-name` | name(127) | 打印机对象的标识名称，例如 Laserjet |
| `printer-state` | type1 enum | 当前打印机状态 |
| `printer-state-reasons` | set1Of type2 keyword | 当前打印机状态的原因 |
| `printer-up-time` | integer (1:MAX) | 打印机运行的秒数 |
| `printer-uri-supported` | set1Of uri | 可用于访问打印机对象的 URI |
| `queued-job-count` | integer (0:MAX) | 该打印机队列中的任务数 |
| `sides-default` | type2 keyword | name | 任务的默认双面设置 |
| `sides-supported` | set1Of type2 keyword | 可用的双面设置 |
| `uri-authentication-supported` | set1Of type2 keyword | 相应 URI 支持的认证类型 |
| `uri-security-supported` | set1Of type2 keyword | 相应 URI 支持的安全类型 |

## `charset-configured` 属性

`charset-configured` 属性包含服务器文本属性的默认字符集。对于 CUPS 来说，通常是 `iso-8859-1`。

## `charset-supported` 属性

`charset-supported` 属性列出了支持的字符集。对于 CUPS，这将包含以下内容：

- `iso-8859-1`
- `iso-8859-2`
- `iso-8859-3`
- `iso-8859-4`
- `iso-8859-5`

```
iso-8859-6
iso-8859-7
iso-8859-8
iso-8859-9
iso-8859-10
iso-8859-13
iso-8859-14
iso-8859-15
us-ascii
utf-8
windows-874
windows-1250
windows-1251
windows-1252
windows-1253
windows-1254
windows-1255
windows-1256
windows-1257
windows-1258
```

## `compression-supported` 属性

`compression-supported` 属性列出了支持的文档压缩方法。对于 CUPS 1.1.x，此属性将包含单个关键字字符串 `none`。对于 CUPS，此属性将包含以下字符串：

```
none
deflate
gzip
```

## `copies-default` 属性

`copies-default` 属性指定了每个任务生成的默认份数。对于 CUPS 来说，此值始终为 1。

## `copies-supported` 属性

`copies-supported` 属性指定了打印机可以生成的最小和最大份数。对于 CUPS，最小始终为 1，最大值始终为 65。

## `document-format-default` 属性

`document-format-default` 属性指定了默认的文档格式。对于 CUPS 来说，该值始终是 `application/octet-stream`。

## `document-format-supported` 属性

`document-format-supported` 属性列出了支持的文档格式。对于 CUPS，此属性将包含以下：

- `application/pdf`
- `application/postscript`
- `application/gif`
- `application/jpeg`
- `application/png`
- `application/tiff`

## `finishings-default` 属性

`finishings-default` 属性指定了默认的结束状态。对于 CUPS 来说，该值见表 9.2。

## `finishings-supported` 属性

`finishings-supported` 属性列出了支持的结束状态。对于 CUPS 来说，该属性源自 Location。

# 表 9.2 结束状态

| 值 | 描述 |
|---|---|
| no-hold | 不保持任务——尽快处理。 |
| indefinite | 保持任务直到手动释放。 |
| day-time | 在每天早上 6 点到下午 6 点之间打印。 |
| evening | 在每天晚上 6 点到第二天早上 6 点之间打印。 |
| night | 在每天晚上 6 点到第二天早上 6 点之间打印。 |
| weekend | 在周末打印。 |
| second-shift | 在每天下午 6 点到午夜 12 点之间打印。 |
| third-shift | 在每天凌晨 12 点到早上 8 点之间打印。 |

## `job-sheets-default` 属性

`job-sheets-default` 属性指定了打印作业时默认的作业单（job sheets）。对于 CUPS，作业单被视为页眉（banner）和页脚（trailer），并被视为一组数组名称。默认值通常为“none”，但可以由管理员覆盖。表 9.4 列出了 CUPS 随附的标准作业单。

表 9.4 作单

| 名称 | 描述 |
| --- | --- |
| none | 不打印任何作业单。 |
| classified | 在顶部和底部打印带有粗体“**Classified**”字样的作业单。 |
| confidential | 在顶部和底部带有粗体“**Confidential**”字样的作业单。 |
| secret | 在顶部和底部带有粗体“**Secret**”字样的作业单。 |
| standard | 打印不带特殊标记的作业单。 |
| topsecret | 在顶部和底部带有粗体“**Top Secret**”字样的作业单。 |
| unclassified | 在顶部和底部带有粗体“**Unclassified**”字样的作业单。 |

## `job-sheets-supported` 属性

`job-sheets-supported` 属性列出了可用的作业单。对于 CUPS，此值派自 `/usr/share/cups/banners` 目录下的文件。

## `media-default` 属性

`media-default` 属性指定打印时使用的介质。它是介质尺寸、类型和源字段的汇总。在 CUPS 中，它镜像了打印机 PPD 文件中 `DefaultPageSize` 的值。

## `media-ready` 属性

`media-ready` 属性列出了哪些介质尺寸、类型和源已准备好打印。CUPS 不使用此属性。

## `media-supported` 属性

`media-supported` 属性列出了打印机支持的介质尺寸、类型和源。在 CUPS 中，此属性包含来自打印机 PPD 文件的 `InputSlot`、`MediaType` 和 `PageSize` 属性列表。

## `multiple-document-handling-default` 属性

`multiple-document-handling-default` 属性指定了打印多份副本时的默认多文档处理方式。表 9.5 列出了可以使用的关键字值。在 CUPS 中，默认值为 `separate-documents-uncollated-copies`。

表 9.5 多文档处理关键字

| 关键字值 | 描述 |
|---|---|
| `single-document` | 生成排序的副本（例如 1, 2, 1, 2, 2）。每个文档和副本都被视为单个输出流，第二个文档和/或副本将从上一个的地方继续。 |
| `separate-documents-uncollated-copies` | 生成未排序的副本（例如 1, 1, 1, 2, 2）。 |
| `separate-documents-collated-copies` | 生成排序的副本（例如 1, 2, 1, 2, 1）。作业中的所有文档都从新的一页开始。 |
| `single-document-new-sheet` | 生成排序的副本，但每个副本都从新的一页开始。这与 `single-document` 关键字类似，但结果是完整的文档可以单独处理，而不是将 N 份副本装在一起。 |

## `multiple-document-handling-supported` 属性

`multiple-document-handling-supported` 属性列出了支持的文档处理类型。对于 CUPS，这包括关键字 `separate-documents-uncollated-copies` 和 `separate-documents-collated-copies`。

## `natural-language-configured` 属性

`natural-language-configured` 属性包含服务器用于文本消息的默认语言。对于 CUPS，此属性通常设置为字符串 `en`，尽管这在 `cups.conf` 文件中可以进行更改。

## `number-up-default` 属性

`number-up-default` 属性指定了每个输出页面上打印的文档页数。对于 CUPS，此值始终为 1。

## `number-up-supported` 属性

`number-up-supported` 属性指定了支持的 number-up 值。对于 CUPS，这始终是数字 1、2 和 4。

## `operations-supported` 属性

`operations-supported` 属性列出了支持的操作代码。CUPS 1.1.x 列出了所有标准的 IPP 操作代码，但 `Print-URI` 和 `Send-URI` 除外。CUPS 1.2.x 列出了所有的 IPP 操作代码。

## `orientation-requested-default` 属性

`orientation-requested-default` 属性指定了文档中页面的默认方向。表 9.6 列出了支持的值。对于 CUPS，此属性的值始终为 3（纵向）。

表 9.6 方向值

| 值 | 描述 |
|---|---|
| 3 | 以纵向方向打印（不旋转）。 |
| 4 | 以横向方向打印（逆时针旋转 90 度）。 |
| 5 | 以反横向方向打印（顺时针旋转 90 度）。 |
| 6 | 以反纵向方向打印（旋转 180 度）。 |

## `orientation-requested-supported` 属性

`orientation-requested-supported` 属性列出了可用的方向。对于 CUPS，这所有 4 个方向值（3, 4, 5 和 6）。

## `pages-ranges-supported` 属性

`pages-ranges-supported` 属性指定了打印文档时是否支持页码过滤。对于 CUPS，此属性始终为 `true`。

## `pdl-override-supported` 属性

`pdl-override-supported` 属性指定服务器是否可以覆盖文档数据中的选项。对于 CUPS，此值始终为 `false`。

## `printer-is-accepting-jobs` 属性

`printer-is-accepting-jobs` 属性指定打印机是否正在接受作业。

## `printer-name` 属性

`printer-name` 属性提供了打印机的标识名称。

## `printer-state` 属性

`printer-state` 属性指定了打印机状态。CUPS 的状态值见表 9.7。

表 9.7 状态值

| 值 | 描述 |
| --- | --- |
| 3 | 空闲。 |
| 4 | 正在处理作业。 |
| 5 | 已停止。 |

## `printer-state-reasons` 属性

`printer-state-reasons` 属性包含了描述打印机状态的原因字符串。对于 CUPS，除了 `none` 之外，所有状态都包含信息、警告或错误。表 9.8 列出了状态字符串。



# 表 9.8 状态字符串

| 字符串 | 描述 |
|---|---|
| connecting-to-device | 正在连接设备。 |
| cover-open | 盖子打开。 |
| developer-empty | 显影液为空。 |
| developer-low | 显影不足。 |
| door-open | 门打开。 |
| fuser-over-temp | 打印机温度过高。 |
| fuser-under-temp | 打印机温度过低。 |
| input-tray-missing | 缺少缺失。 |
| interlock-open | 连锁锁打开。 |
| interpreter-resource-unavailable | 找不到所需的字体或格式。 |
| mark-waste-almost-full | 废墨箱快满。 |
| mark-waste-full | 废墨箱已满。 |
| marker-empty | 墨盒为空。 |
| marker-supply-low | 墨盒不足。 |
| media-empty | 选择的介质为空。 |
| media-jam | 打印机内卡纸。 |
| media-low | 选择的介质不足。 |
| media-needed | 打印机需要介质。 |
| moving-to-paused | 即将暂停。 |
| none | 打印机无原因。 |
| opc-life-over | 光学组件寿命已。 |
| opc-near-eol | 光学组件接近寿命终点。 |
| other | 打印机处于其他未描述的状态。 |
| output-area-full | 输出槽快满。 |
| output-area-full | 输出槽已满。 |
| output-tray-missing | 缺少输出槽。 |
| paused | 打印机已暂停。 |
| shutdown | 打印机已关闭，无法产生输出。 |
| spool-area-full | 缓存目录空间不足。 |
| stopping | 打印机正在停止。 |
| stopped-partly | 打印机部分停止。 |
| timed-out | 与打印机通信超时。 |
| toner-low | 色粉不足。 |
| toner-empty | 色粉为空。 |

## `printer-up-time` 属性

`printer-up-time` 属性指定打印机运行的秒数。对于 `CUPS`，这是一个 Unix 时间（自 1970 年 1 月 1 日起的秒）。

## `printer-uri-supported` 属性

`printer-uri-supported` 属性列出了打印机支持的 URI。对于 `CUPS`，列表由一个或两个如下所示 URI 组成：

```
ipp://ServerName/printers/PrinterName
```

对于打印机

```
ipp://ServerName/classes/ClassName
```

对于类，其中 `ServerName` 是服务器的完全限定主机名（例如 `foo.bar.com`），而 `ClassName` 和 `PrinterName` 是 `printer-name` 属性的值。

如果 `CUPS` 服务器配置为支持加密，则列表中会有相同的 URI。否则，仅提供单个 URI。

## `queued-job-count` 属性

`queued-job-count` 属性指定了打印机队列中未完成作业的数量。

## `sides-default` 属性

`sides-default` 属性指定了作业的默认双面设置。表 9.9 列出了可用的关键字。对于 `CUPS`，默认值镜像了打印机 `PPD` 文件中的 `duplex` 选项。

### 表 9.9 Sides 关键字

| 关键字 | 描述 |
| :--- | :--- |
| one-sided | 在介质的一面上打印。 |
| two-sided-long-edge | 在介质的双面打印，且不旋转（适用于纵向页的双面打印）。 |
| two-sided-short-edge | 在介质的双面打印，背面旋转 180 度（适用于横向页的双面打印）。 |

## `sides-supported` 属性

`sides-supported` 属性列出了可用的双面设置。对于 `CUPS`，它镜像了打印机 `PPD` 文件中的 `Duplex`。

## `uri-authentication-supported` 属性

`uri-authentication-supported` 属性列出了 `printer-uri-supported` 属性中列出的每个 URI 所支持的身份验证类型。每种方法可以是表 9.10 中列出的关键字字符串之一。

### 表 9.10 身份验证关键字字符串

| 关键字 | 描述 |
| :--- | :--- |
| none | 不支持或不需要身份验证。 |
| requesting-user-name | 标识请求所有者。 |
| basic | 使用 Basic 身份验证识别请求所有者。 |
| digest | 使用 Digest 身份验证识别请求所有者。 |
| certificate | 使用证书识别请求所有者。 |

对于 `CUPS`，字符串将是 `requesting-user-name`、`basic` 或 `digest`。还支持另一种基于证书的身份验证机制，但它是与 `basic` 和 `digest` 身份验证结合使用的，而不是作为独立的方法。

## `uri-security-supported` 属性

`uri-security-supported` 属性指定了 `printer-uri-supported` 属性中列出的每个 URI 所支持的加密类型。表 9.11 列出了可用的安全方法。

### 表 9.11 安全关键字字符串

| 关键字 | 描述 |
| :--- | :--- |
| none | 打印机不支持任何类型的加密。 |
| ssl3 | 打印机在专用端口上支持 SSL v3.0 加密。 |
| tls | 打印机使用 HTTP Upgrade 协议支持 TLS v1.0 加密。 |

除非服务器有其他配置，否则 `CUPS` 通常会对所有 URI 返回 `tls`。

## 可选属性

除了必需属性外，打印机对象还包含许多随打印机异的可选属性。表 9.12 列出了可选属性。

### 表 9.12 可选打印机属性

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| color-supported | boolean | 打印机是否支持彩色打印。 |
| job-impressions-supported | rangeOfInteger(:MAX) | 每个作业支持的最最大页数。 |
| job-octets-supported | rangeOfInteger(:MAX) | 文档的最小大小。 |
| job-media-sheets-supported | rangeOfInteger(:MAX) | 支持的作业最大张数。 |
| multiple-document-jobs-supported | boolean | 打印机是否支持多文件的作业。 |
| multiple-operation-time-out | integer(:MAX) | 在 Create-Job、Send-Document 和 Send-URI 操作之间允许的秒数（作业开始前）。 |
| pages-per-minute | integer(:MAX) | 打印机每分钟产生的平均页数。 |
| pages-per-minute-color | integer(:MAX) | 打印机每分钟产生的平均彩色页数。 |
| print-quality-default | type2 enum | 指定默认打印质量。 |
| print-quality-supported | setOf type2 enum | 列出质量。 |
| printer-current-time | dateTime | 打印机已知的当前时间。 |
| printer-driver-installer | uri | 打印机驱动安装页的位置。 |

### 表 9.12 续

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| printer-info | text(127) | 关于打印机的额外描述性信息。 |
| printer-location | text(127) | 打印机的位置。 |
| printer-make-and-model | text(127) | 打印机的品牌和型号名称。 |
| printer-message-from-operator | text(127) | 来自打印机操作员的可读消息。 |
| printer-more-info | uri | 更多打印机信息的 Web 页面。 |
| printer-more-info-manufacturer | uri | 打印机制造商该产品的 Web 页面位置。 |
| printer-resolution-default | resolution | 指定默认输出分辨率。 |
| printer-resolution-supported | setOf resolution | 列出支持的输出分辨率。 |
| printer-state-message | text(MAX) | 打印机的可读状态消息。 |
| reference-uri-schemes-supported | setOf uriScheme | Print-URI 和 Send-URI 操作可以使用方案列表。 |

## `color-supported` 属性

`color-supported` 属性指定打印机是否可以彩色打印。对于 `CUPS`，此属性镜像了 `PPD` `ColorDevice` 属性。

## `job-impressions-supported` 属性

`job-impressions-supported` 属性指定了每个作业支持的最最大打印页数。`CUPS` 不使用此属性。

## `job-octets-supported` 属性

`job-octets-supported` 属性指定了文档的最小和最大大小。`CUPS` 不使用此属性。

## `job-media-sheets-supported` 属性

`job-media-sheets-supported` 属性指定了支持的作业最大张数。`CUPS` 不使用此属性。

## `multiple-document-jobs-supported` 属性

`multiple-document-jobs-supported` 属性指定打印机是否支持多文件的作业。`CUPS` 不使用此属性。

## `multiple-operation-time-out` 属性

`multiple-operation-time-out` 属性指定在作业开始前，`Create-Job`、`Send-Document` 和 `Send-URI` 操作之间允许的秒数。`CUPS` 不使用此属性。

## `pages-per-minute` 属性

`pages-per-minute` 属性指定打印机每分钟产生的平均页数。`CUPS` 不使用此属性。

## `pages-per-minute-color` 属性

`pages-per-minute-color` 属性指定打印机每分钟产生的平均彩色页数。`CUPS` 不使用此属性。

## `print-quality-default` 属性

`print-quality-default` 属性指定默认打印质量。表 9.13 列出了可用值。

### 表 9.13 打印质量

| 值 | 描述 |
| :--- | :--- |
| 3 | 草稿质量 |
| 4 | 普通质量 |
| 5 | 高质量 |

## `print-quality-supported` 属性

`print-quality-supported` 属性列出了质量。`CUPS` 不使用此属性。

## `printer-current-time` 属性

`printer-current-time` 属性指定按照 RFC 1903 定义的本地时间和日期。`CUPS` 目前不提供此属性。

## `printer-driver-installer` 属性

`printer-driver-installer` 属性定义了打印机驱动安装页的位置。`CUPS` 不使用此属性。

## `printer-info` 属性

`printer-info` 属性提供了关于打印机的额外描述性信息。在 `CUPS` 中，管理员在添加打印机或类时定义此属性的值。

## `printer-location` 属性

`printer-location` 属性提供了打印机的可读位置。在 `CUPS` 中，管理员在添加打印机或类时定义此属性的值。

## `printer-make-and-model` 属性

`printer-make-and-model` 属性描述打印机的品牌和型号。在 `CUPS` 中，此属性镜像自打印机 `PPD` 文件中的 `NickName` 属性。

## `printer-message-from-operator` 属性

`printer-message-from-operator` 属性提供了来自打印机操作员的可读消息。`CUPS` 不使用此属性。

## `printer-more-info` 属性

`printer-more-info` 属性提供了包含更多打印机信息的 Web 页面 URL。在 `CUPS` 中，此属性的值与 `printer-uri-supported` 属性中的第一个 URI 相同。

## `printer-more-info-manufacturer` 属性

`printer-more-info-manufacturer` 属性提供了制造商关于该打印机型号的 Web 页面 URL。`CUPS` 不使用此属性。

## `printer-resolution-default` 属性

`printer-resolution-default` 属性指定了默认输出分辨率。`CUPS` 不使用此属性。

## `printer-resolution-supported` 属性

`printer-resolution-supported` 属性列出了支持的输出分辨率。`CUPS` 不提供此属性。

## `printer-state-message` 属性

`printer-state-message` 属性提供了来自打印机的可读文本消息。它包含了在打印作业期间来自过滤器（`filter`）或后端（`back end`）发送的最后一条消息，或者在 `Pause-Operation` 中提供的消息。

## `reference-uri-schemes-supported` 属性

`reference-uri-schemes-supported` 属性列出了 `Print-URI` 和 `Send-URI` 操作支持的 URI 方案。该列表至少必须包含 `ftp` 方案。`CUPS` 1.1.x 不支持此属性或 `Print-URI` 或 `Send-URI` 操作。`CUPS` 1.2.x 列出了 `ftp`、`http` 和 `https` 方案，并支持所有的 `Print-URI` 和 `Send-URI` 操作。

## CUPS 属性

除了标准的 IPP 属性外，`CUPS` 还增加了若干新属性，这些属性适用于打印机或类类型、用于打印队列的设备以及类队列中的成员。表 9.14 列出了这些新属性。

### 表 9.14 打印机和类的 CUPS 属性

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| device-uri | | 打印机连接的设备。 |
| job-k-limit | integer | 在给定的 `job-quota-period` 内，用户打印作业的最大 own。 |
| job-page-limit | integer | 在给定的 `job-quota-period` 内，用户打印作业的最大页数。 |
| job-quota-period | integer | 用于按用户/大小统计信息的秒数。 |
| member-names | listOf(name(127)) | 类中成员打印机的名称列表。 |
| member-uris | listOf | 类中成员打印机的 URI 列表。 |

### 表 9.14 续表

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| printer-type | type2 enum | 打印机/类的能力位。 |
| requesting-user-name-allowed | setsetof(127) | 允许打印的用户列表。 |
| requesting-user-name-denied | setsetof(127) | 不允许打印的用户列表。 |

## `device-uri` 属性

`device-uri` 属性指定了设备的唯一标识符，其格式为 URI，其中包含一个用于身份验证的用户名和密码，当设备 URI 报告给客户端时，这些信息会被自动过滤掉。例如，如果你将 `device-uri` 设置为 `ipp://user:pass@foo.bar/ipp`，返回的值将是 `ipp://foo.bar/com.`。

## `job-k-limit` 属性

`job-k-limit` 属性指定了在给定的 `job-quota-period` 内，用户打印作业的最大大小（以 KB 为单位）。设置为 0 则禁用此配额检查。

## `job-page-limit` 属性

`job-page-limit` 属性指定了在给定的 `job-quota-period` 内，用户打印作业的最大页数。设置为 0 则禁用此配额检查。

## `job-quota-period` 属性

`job-quota-period` 属性指定了用于按用户页/大小统计信息的秒数。值 0 禁用打印机配额，而值 86,400 提供每日配额，604,800 提供每周配额，依此类推。

## `member-names` 属性

`member-names` 属性列出了类中成员打印机的名称。每个名称对应 `member-uris` 属性中相同的 URI。

## `member-uris` 属性

`member-uris` 属性列出了类中成员打印机的 URI。每个 URI 对应 `member-names` 属性中相同的名称。

## `printer-type` 属性



`printer-type` 属性定义了打印机/类类型及其能力。对于打印机类，该能力反映了每个成员打印机共享的共同子集。表 9.15 列出了类型位，这些位通过按位或 运算形成打印机类型值。

### 表 9.15 打印机类型位

| 位 | 描述 |
| --- | --- |
| 0 | 是打印机类 |
| 1 | 是远程目标 |
| 2 | 可以黑白打印 |
| 3 | 可以彩色打印 |
| 4 | 可以硬件双面打印 |
| 5 | 可以输出装订 |
| 6 | 可以硬件执行快速不乱序复制 |
| 7 | 可以硬件执行快速乱序复制 |
| 8 | 可以输出打孔 |
| 9 | 可以输出覆盖 |
| 10 | 可以输出装订 |
| 11 | 可以输出排序 |
| 12 | 可以处理最大至 US-Legal/A4 的介质 |
| 13 | 可以处理从 US-Legal/A4 到 ISO-C/A2 的介质 |
| 14 | 可以处理大于 ISO-C/A2 的介质 |
| 15 | 可以处理用户定义的介质尺寸 |
| 16 | 是隐式类 |

## `requesting-user-name-allowed` 属性

`requesting-user-name-allowed` 属性列出了允许打印的用户。`requesting-user-name-allowed` 和 `requesting-user-name-denied` 之间仅存其一。

## `requesting-user-name-denied` 属性

`requesting-user-name-denied` 属性列出了不允许打印的用户。`requesting-user-name-allowed` 和 `requesting-user-name-denied` 之间仅存其一。

## 打印操作

IPP 提供了若干针对打印对象的操作。表 9.16 列出了这些操作。

### 表 9.16 打印操作

| 代码 | 名称 | 描述 |
| --- | --- | --- |
| 0x0A | Get-Jobs | 获取打印机作业。 |
| 0x0B | Get-Printer-Attributes | 获取打印机属性。 |
| 0x10 | Pause-Printer | 暂停打印机。 |
| 0x11 | Resume-Printer | 恢复打印机。 |
| 0x12 | Purge-Jobs | 清除打印机上的作业。 |
| 0x13 | Set-Printer-Attributes | 设置打印机属性。 |
| 0x15 | Get-Printer-Supported | 获取支持的属性。 |
| 0x22 | Enable-Printer | 允许提交作业到打印机。 |
| 0x23 | Disable-Printer | 防止提交作业到打印机。 |

## Get-Jobs 操作

`Get-Jobs` 操作返回打印机列表。每个请求至少包含以下属性：

```
attributes-charset (charset)
attributes-naturallanguage (naturalLanguage)
printer-uri (uri)
```

`requested-attributes` (`setof type2 keyword`) 属性也可用于限制返回属性的数量，每个关键字代表一个属性名称或组。`requesting-user-name`(127) 属性可限制按用户名的作业。`limit` (`integer`) 属性可以限制返回作业的数量。最后，`which-jobs` (`type2 keyword`) 属性指定了你感兴趣的作业。`complete` 表示你想获取完成作业的信息，而 `not-completed` 表示你想获取等待中、处理中或停止状态作业的信息。

CUPS 还支持 `printer-uri` 值为 `ipp://ServerName/`，这将返回所有打印机类的作业。

## Get-Printer-Attributes 操作

`Get-Printer-Attributes` 操作返回当前的打印机属性。每个请求至少包含以下属性：

```
attributes-charset (charset)
attributes-naturallanguage (naturalLanguage)
printer-uri (uri)
```

`requested-attributes` (`setof type2 keyword`) 属性也可用于限制返回属性的数量，每个关键字代表一个属性名称或组。

## Pause-Printer 操作

`Pause-Printer` 操作将打印机对象置于停止状态。每个请求至少包含以下属性：

```
attributes-charset (charset)
attributes-naturallanguage (naturalLanguage)
printer-uri (uri)
```

对于 CUPS，此操作必须通过向 `/admin` 资源发送 POST 请求，通常需要管理员权限。

## Resume-Printer 操作

`Resume-Printer` 操作将指定的打印机置于空闲或处理状态，取决于是否存在等待中的打印作业。每个请求至少包含以下属性：

```
attributes-charset (charset)
attributes-naturallanguage (naturalLanguage)
printer-uri (uri)
```

对于 CUPS，此操作必须通过向 `/admin` 资源发送 POST 请求，通常需要管理员权限。

## Purge-Jobs 操作

`Purge-jobs` 操作取消指定打印机上的所有打印作业。每个请求至少包含以下属性：

```
attributes-charset (charset)
attributes-naturallanguage (naturalLanguage)
printer-uri (uri)
```

CUPS 操作必须通过向 `/admin` 资源发送 请求来启动，这通常需要管理员身份验证。在使用此操作时，CUPS 还会清理作业历史。

## Set-Printer-Attributes 操作

`Set-Printer-Attributes` 操作设置指定打印机对象上任何可读/写属性的值。每个请求在操作组中必须至少包含以下属性：

```
attributes-charset (charset)
attributes-natural-language (naturalLanguage)
printer-uri (uri)
```

打印机属性应在打印机属性组中满足。

CUPS 目前不支持此操作。

## Get-Printer-Supported-Values 操作

`Get-Printer-Supported-Values` 操作返回支持的打印机属性值。每个请求在操作组中至少包含以下属性：

```
attributes-charset (charset)
attributes-natural-language (naturalLanguage)
printer-uri (uri)
```

CUPS 不支持此操作。

## Enable-Printer 操作

`Enable-Printer` 操作将指定打印机对象的 `printer-is-accepting` 属性设置为 `true`。每个请求在操作组中至少包含以下属性：

```
attributes-charset (charset)
attributes-natural-language (naturalLanguage)
printer-uri (uri)
```

对于 CUPS，此操作必须通过向 `/admin` 资源发送 POST 来启动，这通常需要管理员身份验证。另见相同的（但更早的）操作 `CUPS-Accept-Jobs`。

## Disable-Printer 操作

`Disable-Printer` 操作将指定打印机对象的 `printer-is-accepting` 属性设置为 `false`。每个请求在操作组中至少包含以下属性：

- `attributes-charset` (`charset`)
- `attributes-natural-language` (`naturalLanguage`)
- `printer-uri` (`uri`)

对于 CUPS，此操作必须通过向 `/admin` 资源发送 POST 来启动，这通常还需要管理员身份验证。另见相同的（但更早的）操作 `CUPS-Reject-jobs`。

## 总结

IPP 打印机对象管理单台打印机或类打印机。每个对象都有关联的状态以及指向该打印机的打印作业集合。

每个打印机对象都有一组共同的属性，以及若干可选的打印机特定属性。由 CUPS 服务的打印机具有若干额外的扩展属性，定义了打印机对象如何连接到设备或其他打印机。

IPP 提供了许多控制打印机对象的操作。这些操作控制打印机对象的状态以及某些属性的默认值。

# 第 10 章

## 作业对象

### 什么是作业对象？

本章描述了为 IPP 作业对象提供的属性和操作。

作业对象代表在打印机对象上队列打印的一个或多个文档。作业对象还可以关联订阅对象。

每个作业对象始终处于表 10.1 所示的七种状态之一。等待作业根据优先级值和提交顺序进行打印。

## 表 10.1 作业状态

| 值 | 名称 | 描述 |
| --- | --- | --- |
| 3 | pending | 作业等待打印。 |
| 4 | pending-held | 作业等待在满足保持条件后打印。 |
| 5 | processing | 作业当前正在处理或打印中。 |
| 6 | processing-stopped | 作业在处理或打印期间被停止。 |
| 7 | canceled | 作业被用户或管理员取消。 |
| 8 | aborted | 作业因处理错误被系统中止。这与 processing-stopped 状态不同，因为停止的作业始终可以重启。 |
| 9 | completed | 作业已完全处理并成功打印。 |

作业还与用户名关联，用户名可以经过验证。这允许用户列出并取消自己的作业，或允许管理员列出并取消所有作业。

## 必要属性

每个作业包含若干必要的属性，列在表 10.2 中。

## 表 10.2 必要的作业属性

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| attributes-charset | charset | 作业使用的字符集 |
| attributes-natural-language | naturalLanguage | 作业使用的语言 |
| job-id | integer (1:MAX) | 作业对象编号 |
| job-name | name (MAX) | 作业的名称或标题 |
| job-originating-user-name | name (MAX) | 作业的所有者 |
| job-printer-up-time | integer (1:MAX) | 打印机的当前运行时间值 |

## 表 10.2 续

| 属性 | 类型 | 描述 |
| --- | --- | --- |
| job-printer-uri | uri | 此作业所属打印机对象的 URI |
| job-state | type1 enum | 当前作业状态 |
| job-state-reasons | setOf type2 keyword | 作业的详细原因代码 |
| job-uri | uri | 作业对象的 URI |
| time-at-completed | integer(MIN:MAX) | 作业完成、中止或取消时的打印机运行时间 |
| time-at-creation | integer(MIN:MAX) | 作业创建时的打印机运行时间 |
| time-at-processing | integer(MIN:MAX) | 作业处理时的打印机运行时间 |

## `attributes-charset` 属性

`attributes-charset` 属性指定作业的字符集。

## `attributes-natural-language` 属性

`attributes-natural-language` 属性指定作业的语言。

## `job-id` 属性

`job-id` 属性用于标识打印作业。

## `job-name` 属性

`job-name` 属性指定作业的名称或标题。

## `job-originating-user-name` 属性

`job-originating-user-name` 属性指定作业的所有者。

## `job-printer-up-time` 属性

`job-printer-up-time` 属性提供关联作业的打印机当前运行时间。

## `job-printer-uri` 属性

`job-printer-uri` 属性提供关联打印机对象的 URI。

## `job-state` 属性

`job-state` 属性指定当前作业状态，可以是表 10.1 中列的值之一。

## `job-state-reasons` 属性

`job-state-reasons` 属性是一个关键字数组，描述当前状态的原因。表 10.3 列出了支持的原因字符串。

| 字符串 | 描述 |
| --- | --- |
| none | 当前状态无原因。 |
| aborted-by-system | 作业被系统中止并进入中止状态。 |
| compression-error | 一个或多个文档包含压缩错误。 |
| document-access-error | 无法访问指定的 URI。 |
| document-format-error | 一个或多个文档包含阻止打印的错误。 |
| job-cancelled-at-device | 作业在设备端被取消。 |
| job-cancelled-by-operator | 作业被打印操作员取消。 |
| job-cancelled-by-user | 作业被用户取消。 |
| job-completed-successfully | 作业成功完成。 |
| job-completed-with-errors | 作业带有某些错误完成。 |
| job-completed-with-warnings | 作业带有某些警告完成。 |
| job-data-insufficient | 未收到文档数据。 |
| job-hold-until-specified | 作业因 job-hold-until 属性而处于保持。 |
| job-incoming | 正在从客户端接收文件。 |
| job-interpreting | 作业正在被解释/渲染。 |
| job-outgoing | 作业正在发送到打印机。 |
| job-printing | 作业正在打印中。 |
| job-queued | 作业已进入打印队列。 |
| job-queued-for-marker | 作业已准备打印，但打印机需要墨水/碳粉。 |
| job-restartable | 作业可以重启。 |
| job-transforming | 作业正在转换为另一种格式。 |

## 表 10.3 续

| 字符串 | 描述 |
|---|---|
| printer-stopped | 打印机已停止。 |
| printer-stopped-partly | printer-states 属性包含部分停止（stopped-partly）的原因。 |
| processing-to-stop-point | 任务已取消，但打印机上包含任何已处理的剩余页面。 |
| queued-in-device | 任务已在输出设备上排队。 |
| resources-are-not-ready | 一个或多个资源（介质、字体等）不可用于打印任务。 |
| service-off-line | 因为打印机离线，任务正处于挂起状态。 |
| submission-interrupted | 一个或多个文档文件未完整接收。 |
| unsupported-compression | 任务中的一个或多个文档使用了未知算法进行压缩。 |
| unsupported-document-format | 一个或多个文档采用了不支持的格式。 |

## `job-uri` 属性

`job-uri` 属性提供了任务对象的 URI。

对于 CUPS，`job-uri` 看起来如下：

```
ipp://ServerName/jobs/JobID
```

其中 `ServerName` 是服务器名称，`JobID` 是 `job-id` 属性的值。

## `time-at-completed` 属性

`time-at-completed` 属性指定了任务完成、中止或取消时的打印机运行时间（printer-up-time）。

对于 CUPS，`time-at-completed` 的值是 1970 年 1 月 1 日起的 Unix 时间秒值。

## `time-at-creation` 属性

`time-at-creation` 属性指定了任务创建时的打印机运行时间（printer-up-time）。

对于 CUPS，`time-at-completed` 的值是 1970 年 1 月 1 日起的 Unix 时间秒值。

## `time-at-processing` 属性

`time-at-processing` 属性指定了任务进入处理状态时的打印机运行时间（printer-up-time）。

对于 CUPS，`time-at-completed` 的值是 1970 年 1 月 1 日起的 Unix 时间秒值。

## 可选属性

大多数可选属性是提交打印任务时使用的模板属性。表 10.4 列出了这些可选属性。

| 名称 | 类型 | 描述 |
|---|---|---|
| copies | integer (1:MAX) | 此任务的副本数 |
| date-time-completed | dateTime | 任务完成、取消或中止的日期和时间 |
| date-time-creation | dateTime | 任务创建的日期和时间 |
| date-at-processing | dateTime | 任务处理的日期和时间 |
| finishings | 1setof type2 enum | 此任务的后续动作 |



| job-detailed-status-messages | 1setof text(MAX) | 可读状态消息日志 |

| job-document-access-errors | 1setof text(MAX) | 可读文档访问错误消息日志 |

| job-until | type3 keyword | 名称 | 任务的挂起条件（如果有） |

| job-impressions | integer (@:MAX) | 打印任务中的打印面数 |

| job-impressions-completed | integer (@:MAX) | 已打印的面数 |

| job-k-octets | integer (@:MAX) | 文档文件中的字节数 |

| job-k-octets-processed | integer (@:MAX) | 已处理的字节数 |

| job-media-sheets | integer (@:MAX) | 打印任务中的介质页数 |

| job-media-sheets-completed | integer (@:MAX) | 已打印的介质页数 |

| job-message-from-operator | text (127) | 来自打印员的可读文本消息 |

#### 表 10.4 续

| 名称 | 类型 | 描述 |

|---|---|---|

| job-more-info | uri | 通过 浏览器获取更多信息的 URL |

| job-priority | integer (1:100) | 打印任务的优先级 |

| job-sheets | type3 keyword | 名称 | 任务页 |

| job-state-message | text (MAX) | 可读状态消息 |

| media | type3 keyword | 名称 | 介质尺寸、类型或来源 |

| multiple-document-handling | type2 keyword | 如何处理文档副本 |

| number-of-documents | integer (:MAX) | 任务中的文档文件数量 |

| number-of-intervening-jobs | integer (:MAX) | 在此任务之前调度打印的任务数 |

| number-up | integer (1:MAX) | 每个输出页放置的文档页数 |

| orientation-requested | type2 enum | 输出的方向 |

| output-device-assigned | name(127) | 分配任务的输出设备名称 |

| page-ranges | setOf rangeOfInteger | 打印任务中的哪些页面 |

| print-quality | type2 enum | 输出质量 |

| printer-resolution | resolution | 输出分辨率 |

| sides | type2 keyword | 打印单面还是双面 |

## copies 属性

`copies` 属性指定了任务将生成的副本数。`copies` 仅适用于文档文件，而不适用于与任务关联的任务页（job sheets）。`copies` 属性的值必须在打印机 `copies-supported` 属性定义的范围内。

## date-time-at-completed 属性

`date-time-at-completed` 属性提供了任务完成、取消或中止的日期和时间。

CUPS 不提供此属性。

## date-time-at-creation 属性

`date-time-at-creation` 属性提供了任务创建的日期和时间。

CUPS 不提供此属性。

## date-time-at-processing 属性

`date-time-at-processing` 属性提供了任务处理的日期和时间。

CUPS 不提供此属性。

## finishings 属性

`finishings` 属性指定了此任务的后续动作。可用关键字由打印机的 `finishings-supported` 属性定义。

## job-detailed-status-messages 属性

`job-detailed-status-messages` 属性提供了有关任务状态的可读文本列表。

CUPS 不提供此属性。

## job-document-access-errors 属性

`job-document-access-errors` 属性提供了检索文档时遇到的任何错误的可读文本消息。

CUPS 1.1 不提供此属性。

CUPS 1.2 提供 HTTP 和 FTP 错误。

## job-until 属性

`job-until` 属性指定了任务的挂起条件。

## job-impressions 属性

`job-impressions` 属性提供了打印任务中的打印面数。与 `job-media-sheets` 属性不同，因为 `job-media-sheets` 统计的是打印页数。

CUPS 不提供此属性。

## job-impressions-completed 属性

`job-impressions-completed` 属性提供了已打印的面数。与 `job-media-sheets-completed` 属性不同，因为 `job-media-sheets-completed` 统计的是已打印的页数。

CUPS 不提供此属性。

## job-k-octets 属性

`job-k-octets` 属性提供了文档文件中的字节数。CUPS 在向任务中添加额外文档时更新此值。

## job-k-octets-processed 属性

`job-k-octets-processed` 属性提供了已处理的字节数。CUPS 不提供此属性。

## job-media-sheets 属性

`job-media-sheets` 属性提供了打印任务中的介质页数。与 `job-impressions` 属性不同，因为 `job-impressions` 统计的是打印的面数。例如，一个包含 20 页的典型双面打印任务的 `job-media-sheets` 值为 10，`job-impressions` 值为 20。

CUPS 不提供此属性。

## job-media-sheets-completed 属性

`job-media-sheets-completed` 属性提供了已打印的介质页数。与 `job-impressions-completed` 属性不同，因为 `job-impressions-completed` 统计的是已打印的面数。

CUPS 不提供此属性。

## job-message-from-operator 属性

`job-message-from-operator` 属性提供了来自打印员的可读文本消息。这可能包含类似“任务正挂起，直到我们需要一卷新的光纸”的消息。

CUPS 不提供此属性。

## job-priority 属性

`job-priority` 属性指定打印任务的优先级。任务优先级用于控制队列中打印任务的顺序；优先级越高越打印。

CUPS 使用任务优先级来确定任务在队列中的位置，但不会停止已经在已经在队列中的低优先级任务。

## job-sheets 属性

`job-sheets` 属性指定打印任务时使用的横幅页（banner pages）。

CUPS 支持 1 或 2 张作业单。第一张单在任务中的文档之前打印，第二张单在任务中的文档之后打印。由于 CUPS 中作业单的实现方式，在任务创建后无法更改 `jobsheets` 属性。

## job-state-message 属性

`job-state-message` 属性为任务提供一种人类可读的状态消息。

CUPS 目前不支持此属性。

## media 属性

`media` 属性指定任务的介质尺寸、类型或来源。

CUPS 允许每个任务接受 1 个或多个属性值，以便指定所有三个介质值。

## multiple-document-handling 属性

`multiple-document-handling` 属性指定如何处理文档副本。本质上，此属性控制副本是否进行装订。

CUPS 支持 `multiple-documents-collated-copies` 和 `multiple-documents-uncollated-copies` 值。

## number-of-documents 属性

`number-of-documents` 属性提供任务中文档文件的总数。

CUPS 将作业单包含在计数中。

## number-of-intervening-jobs 属性

`number-of-intervening-jobs` 属性提供在此任务之前安排打印的任务数。

CUPS 不支持此属性。

## number-up 属性

`number-up` 属性指定每个输出页面放置的文档页数。

CUPS 支持每面或每张纸打印 1、2 或 4 页。

## orientation-requested 属性

`orientation-requested` 属性指定输出的方向。该值必须必须是打印机 `orientation-supported` 属性中的值之一。

## output-device-assigned 属性

`output-device-assigned` 属性提供分配给任务的输出设备名称。

CUPS 不提供此属性。

## page-ranges 属性

`page-ranges` 属性指定打印任务中的哪些页面。集合中的页范围必须是唯一的，并适用于任务中的所有文档。例如，如果指定的 `page-ranges` 属性值为 1–4，则将在每个文档中打印第 1–4 页，或者只打印第一个文档的前 4 页。

CUPS 按升序打印页范围，指定值为 7–8 的 `page-ranges` 属性将打印第 1、2、7 和 8 页。

## print-quality 属性

`print-quality` 属性指定输出质量。该值必须必须是打印机 `print-quality-supported` 属性中的值之一。

CUPS 不支持此属性。

## printer-resolution 属性

`printer-resolution` 属性指定打印任务的输出分辨率。该值必须是打印机 `printer-resolution-supported` 属性中的值之一。

## sides 属性

`sides` 属性指定是单面还是双面输出。该值必须是打印机 `sides-supported` 属性中的值之一。

## CUPS 属性

CUPS 定义了若干由 CUPS 文件过滤器使用的新模板属性。表 10.5 定义了 CUPS 属性。

| 名称 | 类型 | 描述 |

|---|---|---|

| blackplot | boolean | 是否仅用黑色墨水打印 HP-GL/2 绘文件 |

| brightness | integer (0:200) | 打印任务的整体亮度 |

| columns | integer (1:4) | 文件的列数 |

| cpi | type2 enum | 打印文本文件时每英寸字符数 |

| fitplot | boolean | 是否将 HP-GL/2 绘文件缩放到介质尺寸 |

| gamma | integer (1:10000) | 打印任务的整体  校正 |

| hue | integer (-180:180) | 应用于图片的色彩旋转 |

| job-billing | text(MAX) | 任务计费信息 |

| job-originating-host-name | name(MAX) | 创建任务的主机名或 IP 地址 |

| lpi | type2 enum | 打印文件时每英寸行数 |

| page-bottom | integer (0:MAX) | 打印文本文件时的页边距（磅） |

| page-label | text(MAX) | 显示在每个打印页顶部底部的标签 |

| page-left | integer (0:MAX) | 打印文本文件时的左边距（磅） |

| page-right | integer (0:MAX) | 打印文本文件时的右边距（磅） |

| page-set | type2 keyword | 每个文档中要打印的页面 |

## 表 10.5 继续

| 名称 | 类型 | 描述 |

|---|---|---|

| page-top | integer (0:MAX) | 打印文本文件时的顶边距（磅） |

| penwidth | integer (0:MAX) | HP-GL/2 绘文件中的默认笔宽 |

| position | type2 keyword | 图片在页面上的位置 |

| ppi | integer (1:MAX) | 图片每英寸像素分辨率 |

| prettyprint | boolean | 是否对文本文件应用格式化 |

| saturation | integer (0:200) | 文件的饱和度 |

| scaling | integer (1:1000) | 应用于图片的缩放 |

| wrap | boolean | 在文本文件中换行 |

## blackplot 属性

`blackplot` 属性指定 HP-GL/2 绘文件是完全用黑色渲染（`blackplot=true`）还是使用文件中指定的颜色。此属性不支持其他类型的文件。默认值为 false。

## brightness 属性

`brightness` 属性以百分比指定输出的整体亮度。亮度为 100 为正常，200 为亮度倍，50 为亮度减半。默认值为 100。

亮度通过以下函数等应用于青色、红色和黄色：

```
f(x) = brightness / 100 * x
```

## columns 属性

`columns` 属性指定打印文本文件时生成的列数。此属性不支持其他类型的文件。默认值为 1。

## cpi 属性

`cpi` 属性指定打印文本文件时每英寸字符数。此属性不支持其他类型的文件。支持的值为 10、12 和 17。默认值为 10。

## fitplot 属性

`fitplot` 属性指定 HP-GL/2 绘文件缩放到所选介质（`fitplot=true`），还是使用文件中指定的物理比例（`fitplot=false`）。此属性不支持其他类型的文件。默认值为 false。

只有当 HP-GL/2 文件包含 PS（Plot Size）命令时，缩放才有效。

## gamma 属性

`gamma` 属性指定输出的亮度校正。值 1000 表示不校正，2000 和 500 分别生成更亮和更暗的输出。默认值为 1000。

Gamma 通过以下函数应用于红色、绿色和蓝色值（或灰度输出的亮度）：

```
f(x) = x^(1000/gamma)
```

## hue 属性

`hue` 属性在打印图像文件时指定色彩旋转。此属性不支持其他类型的文件。默认值为 0。表 10.6 显示了不同色值对主色的影响。

| 表 10.6 色相对色彩的影响 |

| 颜色 | hue=-45 | hue=45 |

|---|---|---|

| 红色 | 紫色 | 黄橙色 |

| 绿色 | 黄绿色 | 蓝绿色 |

| 黄色 | 橙色 | 绿黄色 |

| 蓝色 | 天蓝色 | 紫色 |

| 品红色 | 靛蓝 | 绯红色 |

| 青色 | 蓝绿色 | 浅蓝 |

是否启用主机名解析。localhost 地址 (127.0.0.1) 始终解析为名称“localhost”。

此属性是只读的。

## 1pi 属性

`1pi` 属性指定打印文本文件时每英寸的行数。此属性对所有其他类型的文件均忽略。目前仅支持值 6 和 8。默认值为 6。

## page-bottom 属性

`page-bottom` 属性指定以点（points）为单位的底边距（72 点等于 1 英寸）。默认值是打印机 PPD 文件定义的设备物理边距。

## page-label 属性

`page-label` 属性提供一个文本值，放置在每页的页眉和页脚中。如果服务器设置了分类，则该分类将在页标签之前打印，页标签用于保存与作业分类相关的注意事项。默认情况下没有页标签。

## page-left 属性

`page-left` 属性指定以点（points）为单位的左边距（72 点等于 1 英寸）。默认值是打印机 PPD 文件定义的设备物理边距。

## page-right 属性

`page-right` 属性指定以点（points）为单位的右边距（72 点等于 1 英寸）。默认值是打印机 PPD 文件定义的设备物理边距。

## page-set 属性

`page-set` 属性指定打印哪些页面。支持的关键字见表 10.7。默认值为 all（所有）。

### 10.7 Page设置关键字

| 关键字 | 描述 |

| :--- | :--- |

| all | 打印所有页面 |

| even | 仅打印偶数页 |

| odd | 仅打印奇数页 |

## page-top 属性

`page-top` 属性指定以点（points）为单位的上边界（72 点等于 1 英寸）。默认值是打印机 PPD 文件定义的设备物理边距。

## penwidth 属性

`penwidth` 属性指定打印 HP-GL 文件时以微米（micrometers）为单位的默认笔宽（1000 微米 = 1 毫米）。此属性忽略所有其他类型的文件，并在使用 PW（笔宽）命令的 HP-GL 文件中会被覆盖。默认值为 1000 微米。

## position 属性

`position` 属性指定图像文件在介质上的位置。此属性对所有其他类型的文件均忽略。表 10.8 列出了支持的关键字。默认值为 center（中心）。

### 10.8 Position关键字

| 关键字 | 描述 |

| :--- | :--- |

| center | 图像在页面居中 |

| top | 在页面顶部居中打印图像 |

| left | 在页面左侧居中打印图像 |

| right | 在页面右侧居中打印图像 |

| top-left | 在页面左上角打印图像 |

| top-right | 在页面右上角打印图像 |

| bottom | 在页面底部居中打印图像 |

| bottom-left | 在页面左下角打印图像 |



| bottom-right | 在页面右下角打印图像 |

## ppi 属性

`ppi` 属性指定图像文件以英寸像素为单位的分辨率。此属性对所有其他类型的文件均忽略。默认值为文件中包含的分辨率，或者如果没有可用信息则为 72。

## prettyprint 属性

`prettyprint` 属性指定打印文本文件时是带有阴影标题和关键字高亮（`prettyprint=true`），还是不带额外格式（`prettyprint=false`）。默认值为 false。关键字高亮对内容敏感，因此 Bourne shell 脚本与 C 代码的高亮方式不同。

## saturation 属性

`saturation` 属性指定打印图像文件时的色彩饱和度。此属性对所有其他类型的文件均忽略。饱和度为 100 是正常的，而值 50 和 200 将分别是色彩的一半和两倍。默认值为 100。

## scaling 属性

`scaling` 属性指定图像相对于所选介质的比例。此属性对所有其他类型的文件均忽略。值 100 表示图像文件应恰好适应一个页面，在图像尺寸允许范围内尽可能填充。默认值未指定。如果指定了 `scaling` 属性，它将覆盖 `ppi` 属性。

## wrap 属性

`wrap` 属性指定打印文本文件时长行是否应该折行（`wrap=true`）或不折行（`wrap=false`）。此属性对所有其他类型的文件均忽略。默认值为 true。

## 作业操作

IPP 执行表 10.9 中列的操作来创建和管理作业对象。

### 10.9 IPP 作业操作

| 代码 | 名称 | 描述 |
| :--- | :--- | :--- |
| 0x0002 | Print-Job | 打印单份文件。 |
| 0x0003 | Print-URI | 打印单个 URI。 |
| 0x0004 | Validate-Job | 验证作业选项。 |
| 0x0005 | Create-Job | 创建一个空打印作业。 |
| 0x0006 | Send-Document | 向现有作业添加单份文件。 |
| 0x0007 | Send-URI | 向现有作业添加单个 URI。 |
| 0x0008 | Cancel-Job | 取消打印作业。 |
| 0x0009 | Get-Job | 获取打印作业属性。 |
| 0x000C | Hold-Job | 挂起作业。 |
| 0x000D | Release-Job | 释放打印作业。 |
| 0x000E | Restart-Job | 重启打印作业。 |
| 0x0014 | Set-Job-Attributes | 设置作业属性。 |

## Print-Job 操作

`Print-Job` 操作打印单份文件。每个请求必须包含以下属性：

- `attributes-charset`
- `attributes-natural-language`
- `printer-uri`
- `requesting-user-name`

文件紧跟在 HTTP 请求数据之后。如果作业被接受，IPP 响应将包含 `job-uri`、`printer-uri` own `job-id`。

## Print-URI 操作

`Print-URI` 操作打印单个远程文件。每个请求必须包含以下属性：

- `attributes-charset`
- `attributes-natural-language`
- `printer-uri`
- `requesting-user-name`
- `document-uri`

`document-uri` 属性提供文档文件的位置。如果作业被接受，IPP 响应将包含 `job-uri`、`printer-uri` 和 `job-id`。2 之前的之前的 CUPS 不支持 `Print-URI` 操作。

## Validate-Job 操作

`Validate-Job` 操作验证 `Create-Job`、`Print-Job` 或 `Print-URI` 将使用的属性。每个请求必须包含以下属性：

- `attributes-charset`
- `attributes-natural-language`
- `printer-uri`
- `requesting-user-name`

IPP 响应将包含成功或失败代码，以及不支持的属性。

## Create-Job 操作

`Create-Job` 操作创建一个空打印作业。每个请求必须包含以下属性：

- `attributes-charset`
- `attributes-natural-language`
- `printer-uri`
- `requesting-user-name`

文件后通过 `Send-Document` 或 `Send-URI` 操作发送。如果作业被接受，IPP 响应将包含 `job-uri`、`printer-uri` 和 `job-id`。

## Send-Document 操作

`Send-Document` 操作向现有作业添加单份文件。每个请求必须包含以下属性：

- `attributes-charset`
- `attributes-natural-language`
- `printer-uri` 和 `job-id` 或 `job-uri`
- `requesting-user-name`
- `last-document`

文件紧跟在 HTTP 请求 数据之后。IPP 响应将包含文档的成功或失败代码。`last-document` 属性指定该文档文件是否是作业中的最后一个文件。

## Send-URI 操作

`Send-URI` 操作向现有作业添加单个远程文件。每个请求必须包含以下属性：

- `attributes-charset`
- `attributes-natural-language`
- `printer-uri` 和 `job-id` 或 `job-uri`
- `requesting-user-name`
- `last-document`
- `document-uri`

`document-uri` 属性指定远程文件的 URL。

## 取消作业操作 (Cancel-Job)

`Cancel-Job` 操作取消现有的打印作业。每个请求必须在操作组中至少包含以下属性：

```
attributes-charset (charset)
attributes-natural-language (naturalLanguage)
printer-uri (uri) and job-id (integer) or job-uri (uri)
requesting-user-name (name)
```

该作业必须属于 `requesting-user-name` 属性中指定的用户，或者请求必须来自管理员用户。对于 CUPS，系统组组中的任何用户都可以删除服务器上的任何作业。

IPP 响应将包含成功或失败代码。

## 获取作业属性操作 (Get-Job-Attributes)

`Get-Job-Attributes` 操作获取现有的打印作业的属性。每个请求必须在操作组中至少包含以下属性：

```
attributes-charset (charset)
attributes-natural-language (naturalLanguage)
printer-uri (uri) and job-id (integer) or job-uri (uri)
```

IPP 响应将包含成功或失败代码，以及作业对象的属性。可以在 IPP 请求中提供 `requested-attributes` 属性以选择返回哪些属性（否则将返回所有作业属性）。

## 保持作业操作 (Hold-Job-Operation)

`Hold-Job` 操作暂停现有的打印作业打印。每个请求必须在操作组中至少包含以下属性：

```
attributes-charset (charset)
attributes-natural-language (naturalLanguage)
printer-uri (uri) and job-id (integer) or job-uri (uri)
requesting-user-name (name)
job-hold-until (keyword | name)
```

`job-hold-until` 属性指定新的条件或时间。该作业必须属于 `requesting-user-name` 属性中指定的用户，或者请求必须来自管理员用户。对于 CUPS，系统组中的任何用户都可以保持服务器上的任何作业。

IPP 响应将包含成功或失败代码。

## 释放作业操作 (Release-Job)

`Release-Job` 操作释放现有的打印作业以打印。每个请求必须在操作组中至少包含以下属性：

- `attributes-charset` (charset)
- `attributes-natural-language` (naturalLanguage)
- `printer-uri` (uri) and `job-id` (integer) or `job-uri` (uri)
- `requesting-user-name` (name)

该作业必须属于 `requesting-user-name` 属性中指定的用户，或者请求必须来自管理员用户。对于 CUPS，系统组中的任何用户都可以释放服务器上的任何作业。

IPP 响应将包含成功或失败代码。

## 重启作业操作 (Restart-Job)

`Restart-Job` 重启现有的打印作业。每个请求必须在操作组中至少包含以下属性：

- `attributes-charset` (charset)
- `attributes-natural-language` (naturalLanguage)
- `printer-uri` (uri) and `job-id` (integer) or `job-uri` (uri)
- `requesting-user-name` (name)

只有在服务器上启用了作业文件（`PreserveJobFiles`）时，才能重启作业。

该作业还必须属于 `requesting-user-name` 属性中指定的用户，或者请求必须来自管理员用户。对于 CUPS，任何用户都可以重启服务器上的任何作业。

IPP 响应将包含成功或失败代码。重启打印作业的打印。

## 设置作业属性操作 (Set-Job-Attributes)

`Set-Job-Attributes` 操作更改现有打印作业的作业模板属性。每个请求必须在操作组中至少包含以下属性：

- `attributes-charset` (charset)
- `attributes-natural-language` (naturalLanguage)
- `printer-uri` (uri) and `job-id` (integer) or `job-uri` (uri)
- `requesting-user-name` (name)

该作业必须属于 `requesting-user-name` 属性中指定的用户，或者请求必须来自管理员用户。对于 CUPS，系统组中的任何用户都可以更改服务器上的任何作业。

CUPS 也不允许更改 `job-sheets` 属性。

IPP 响应将包含成功或失败代码。

## 总结

作业对象持有发送到打印机的每个作业的文件和选项。每个作业对象与打印机或类关联，并可以与多个订阅对象关联。作业对象包含状态属性以及定义打印输出生成方式作业模板属性。IPP 作业操作允许你在打印服务器上创建和管理打印作业。

# 第 11 章

## IPP 订阅对象 (IPP Subscription Objects)

本章描述了为 IPP 订阅对象提供的属性和操作。IPP 订阅对象提供了 IPP 中事件通知的基础。文中讨论了 mailto、indp 和 ippet 通知方案。

## 什么是订阅对象？

订阅对象是一种事件通知服务。每个订阅对象包含通知接收者的地址（URI）、一种订阅方案或方法，以及订阅者感兴趣的事件列表。

IPP 订阅对象与打印机或作业对象关联。在启动打印作业或监控现有作业状态时，可以创建作业订阅。例如，当一个长时间打印作业完成后，你可能会收到一封电子邮件。作业订阅的持续时间与作业相同。

打印机订阅在引用现有的打印机对象时创建。这些订阅通常是长期的，第三方可以作为管理员来监控缺纸等条件下的打印机事件。每个打印机订阅都有租期时间，该时间指定了以秒为单位的订阅时长。

CUPS 通过支持服务器订阅扩展了 IPP 订阅机制。服务器订阅使用 `printer-uri` 值和事件列表。服务器订阅允许你监控打印机的添加或删除以及其他服务器状况。

通知在 CUPS 1.2 及更高版本中可用。

## 标准通知

IPP 通知为订阅对象增加了许多属性。表 11.1 列出了订阅对象。

| 表 11.1 订阅对象 | 名称 | 类型 |
| :--- | :--- | :--- |
| `notify-attributes` | setof type2 | 机器可读通知的属性列表 |
| `notify-attributes-supported` | setof type2 | 支持的通知 |
| `notify-charset` | charset | 通知使用的字符集 |
| 表 11.1 继续 | 名称 | 类型 |
| :--- | :--- | :--- |
| `notify-events` | setof type2 | 要监控的事件列表 |
| `notify-events-default` | setof type2 | 默认监控的事件 |
| `notify-events-supported` | setof type2 | 支持监控的事件列表 |
| `notify-job-id` | integer (1:MAX) | 关联作业的 ID |
| `notify-lease-duration` | integer (0:67108863) | 订阅时长（秒为单位） |
| `notify-lease-duration-default` | integer (0:67108863) | 默认订阅时长（秒为单位） |
| `notify-lease-duration-supported` | setof integer (0:67108863) | rangeOfInteger (0:67108863) 支持的订阅时长（秒为单位） |
| `notify-lease-expiration-time` | integer (0:MAX) | 订阅有效期（秒为单位） |
| `notify-max-events-supported` | integer (2:MAX) | 可监控的最大事件数量 |
| `notify-natural-language` | naturalLanguage | 通知使用的语言 |
| `notify-printer-up-time` | integer (1:MAX) | 打印机对象的当前时间 |
| `notify-printer-uri` | uri | 关联打印机对象的 URI |
| `notify-recipient-uri` | uri | 通知接收者的 URI |
| `notify-schemes-supported` | setof uriScheme | 支持的通知方案 |
| `notify-sequence-number` | integer (0:MAX) | 事件的唯一序列号 |
| `notify-subscribed-event` | type2 keyword | 触发通知的事件 |
| `notify-subscriber-user-name` | name (MAX) | 订阅者的用户名 |
| `notify-subscription-id` | integer (1:MAX) | 此订阅对象的 ID 号 |
| `notify-text` | text (MAX) | 人类可读的通知消息 |
| `notify-time-interval` | integer (0:MAX) | 通知之间的最小时间间隔 |

# 表 11.1 继续

| 名称 | 类型 | 描述 |
| :--- | :--- | :--- |
| `notify-user-data` | octetString(63) | 原样发送给订阅者的不透明数据（Opaque data） |
| `printer-state-change-date` | dateTime | 上一次状态改变的日期和时间 |
| `printer-state-change-time` | integer (1:MAX) | 上一次状态改变时的打印对象时间 |

## notify-attributes

`notify-attributes` 属性列出了应在机器可读通知中发送的属性。它不用于人类可读的通知，例如由 `mailto` 通知方案提供的通知。

## notify-attributes-supported

`notification-attributes-supported` 属性列出了所有可用的通知属性。它通常包含服务器支持的每个作业和打印机属性名称。

## notify-charset

`notify-charset` 属性指定了发送请求时使用的字符集。默认使用原始订阅请求的字符集。

## notify-events

`notify-events` 属性列出了此订阅需要监控的事件。这些事件可以是表 11.2 中列出的任何关键字。任何支持通知的 IPP 服务器必须对每个订阅至少支持两个事件。

CUPS 对可以监控的事件数量没有限制。

## notify-events-default

`notify-events-default` 属性列出了如果在创建订阅请求未提供 `notify-events` 属性时将监控的默认事件。对于 CUPS，默认事件为 "none"。

## notify-events-supported

`notify-events-supported` 属性提供了可以监控的支持事件。表 11-2 列出了可以使用的事件关键字。

## 表 11.2 通知事件关键字

| 关键字 | 描述 |
| :--- | :--- |
| "none" | 无通知事件。 |
| "job-completed" | 作业已完成。 |
| "job-config-changed" | 作业的配置（属性）发生变化，或操作员消息（message-from-operator）属性发生变化。 |
| "job-created" | 创建了一个作业。 |
| "job-progress" | 打印机完成了作业中的某页打印。 |



| `"job-state-changed"` | 作业状态（`job-state`）或作业状态原因（`job-state-reasons`）属性发生变化。 |
| `"job-stopped"` | 作业已停止。 |
| `"printer-config-changed"` | 打印机配置属性发生变化，或操作员消息（`printer-message-from-operator`）属性发生变化。 |
| `"printer-finishes-changed"` | 附件就绪（`finishes-ready`）属性发生变化。 |
| `"printer-media-changed"` | 介质就绪（`media-ready`）属性发生变化。 |
| `"printer-queue-order-changed"` | 打印机队列中的作业顺序发生变化。 |
| `"printer-restarted"` | 打印机已启动。 |
| `"printer-shutdown"` | 打印机已关闭。 |
| `"printer-state-changed"` | 打印机状态原因（`printer-state-reasons`）或打印机是否接受（`printer-is-accepting`）属性发生变化。 |
| `"printer-stopped"` | 打印机状态（`printer-state`）属性变为 `"stopped"`。 |

CUPS 为服务器订阅定义了几个额外的关键字。表 11.3 列出了 CUPS 服务器事件关键字。

## 表 11.3 CUPS 通知事件关键字

| 关键字 | 描述 |
| :--- | :--- |
| `"cups-add-class"` | 向服务器添加了一个打印机类。 |
| `"cups-add-device"` | 向服务器添加了一个设备。 |
| `"cups-add-printer"` | 向服务器添加了一个打印机。 |
| `"cups-delete-class"` | 从服务器删除了一个打印机类。 |
| `"cups-delete-device"` | 从服务器删除了一个设备。 |
| `"cups-delete-printer"` | 从服务器删除了一个打印机。 |
| `"cups-modify-class"` | 在服务器上修改了打印机类。 |
| `"cups-modify-device"` | 在服务器上修改了设备。 |
| `"cups-modify-printer"` | 在服务器上修改了打印机。 |
| `"cups-server-restart"` | 重启了调度器。 |
| `"cups-server-start"` | 启动了调度器。 |
| `"cups-server-stop"` | 停止了调度器。 |

## `notify-job-id`

`notify-job-id` 属性提供了关联作业对象的作业 ID。此属性用于创建或查询作业订阅时。

## `notify-lease-duration`

`notify-lease-duration` 属性指定了订阅对象的寿命（以秒为单位）。如果租期时长为 0 秒，则订阅对象永不过期。

租期仅适用于打印机订阅。对于 CUPS，服务器订阅也可用租期。

## `notify-lease-duration-default`

`notify-lease-duration-default` 属性指定了订阅对象的默认寿命（以秒为单位）。

## `notify-lease-duration-supported`

`notify-lease-duration-supported` 属性列出了支持的订阅对象寿命（秒）。租期时长可以是离散的（0, 60, 120, 180）或值范围。

## `notify-lease-expiration-time`

`notify-lease-expiration-time` 属性提供了订阅的过期时间（秒）。如果过期时间为 0，则订阅不过期。

对于 CUPS，该值将是自 1970 年 1 月 1 日以来的 Unix 时间。

## `notify-max-events`

`notify-max-events` 属性指定了订阅对象可以监控的事件最大数量。IPP 规范要求每个订阅至少包含两个事件。

CUPS 订阅可以在单个订阅中同时监控所有事件；因此，此属性的值将是支持的事件数减去 `"none"` 关键字。

## `notify-natural-language`

`notify-natural-language` 属性指定了发送事件通知时使用的语言。该语言用于所有文本（人类可读）数据。

此属性必须是打印机 `generated-natural-language-supported` 属性中列出的语言之一。

## `notify-printer-up-time`

`notify-printer-up-time` 属性镜像 `printer-up-time` 属性，提供了打印对象的当前时间（秒）。

CUPS 使用自 1970 年 1 月 1 日以来的 Unix 时间。

## `notify-printer-uri`

`notify-printer-uri` 属性提供了关联打印对象的 URI。

对于 CUPS，此属性可以是任何有效的打印机或类 URI：

```
ip://ServerName/
ip://ServerName/classes/ClassName
ip://ServerName/printers/PrinterName
```

## `notify-recipient-uri`

`notify-recipient-uri` 属性指定了通知接收者的 URI。该 URI 必须使用 `notify-schemes-supported` 属性中列出的方案之一。

电子邮件通知将使用常见的 mailto URI：

```
mailto:foo@bar.com
```

其他通知方案将在后续描述。

## `notify-schemes-supported`

`notify-schemes-supported` 属性列出了支持的通知方案。方案是 URI 中冒号之前的单词，例如 `"mailto"`。

## `notify-sequence-number`

`notify-sequence-number` 属性提供了事件通知中的唯一序列号。它每次发送给客户端时递增，且对每个订阅都是唯一的。

## `notify-subscribed-event`

`notify-subscribed-event` 属性在机器可读通知中发送，提供了触发通知的事件关键字。

## `notify-subscriber-user-name`

`notify-subscriber-user-name` 提供了创建订阅的用户名，通常与创建请求中传递的 `requesting-user-name` 相同。

## `notify-subscription-id`

`notify-subscription-id` 提供了此订阅对象的 ID 数字。该数字配合 `printer-uri` 属性，用于识别服务器上的单个订阅对象。

## `notify-text`

`notify-text` 属性在通知中发送，包含人类可读的通知消息，例如“缺纸”。

## `notify-time-interval`

`notify-time-interval` 属性指定了 `job-progress` 事件通知之间的最小秒数。此属性允许客户端减少事件通知的频率，以免打印机拖慢。

## `notify-user-data`

`notify-user-data` 属性提供了所谓的“不透明数据”，该数据原样发送给订阅者。这可以用于识别客户端特定的订阅。

## `printer-state-change-date-time`

`printer-state-change-date-time` 属性包含了任何打印事件中关联打印对象的上一次状态改变的日期（`printer-date-time`）。

## `printer-state-change-time`

`printer-state-change-time` 属性包含了任何打印事件中关联打印对象的上一次状态改变的时间（秒）。

# 订阅操作

IPP 定义了几个新操作以支持通知。大多数操作适用于一般的订阅对象，而少数操作用于各种通知方案向客户端投送事件。表 11.4 列出了订阅对象的操作。

| 代码 | 名称 | 描述 |
| --- | --- | --- |
| 0x016 | Create-Printer-Subscription | 为打印机状态更改创建订阅。 |
| 0x017 | Create-Job-Subscription | 为打印作业状态更改创建订阅。 |
| 0x0018 | Get-Subscription-Attributes | 获取订阅的属性。 |
| 00x0019 | Get-Subscriptions | 获取订阅列表。 |
| 0x001A | Renew-Subscription | 续订现有（已过期）订阅。 |
| 0x001B | Cancel-Subscription | 取消订阅。 |
| 0x001C | Get-Notifications | 使用 ipp-get 方法获取待处理的通知。 |
| 0x001D | Send-Notifications | 使用 ipp-method 发送待处理的通知。 |

## Create-Printer-Subscription

`Create-Printer-Subscription` 操作创建一个或多个跟踪打印机对象状态更改的打印机订阅。典型的 `Create-Printer-Subscription` 操作在操作组中包含以下属性：

```
attributes-charset (charset)
attributes-natural-language (naturalLanguage)
printer-uri (uri)
requesting-user-name (name)
```

操作组之后是一个或多个包含订阅创建属性的订阅组：

```
notify-recipient-uri (uri)
notify-lease-time (integer)
notify-events (setOf type2 keyword)
```

如果创建了订阅，IPP 将针对请求中的每个订阅组响应 `notify-subscription-id` 属性。如果服务器无法创建所有指定的订阅，服务器将返回 `'client-error-too-many-subscriptions'` 状态码。

## Create-Job-Subscription

`Create-Job-Subscription` 操作创建一个或多个跟踪作业对象状态更改的作业订阅。典型的 `Create-Job-Subscription` 操作在操作组中包含以下属性：

- `attributes-charset` (charset)
- `attributes-natural-language` (naturalLanguage)
- `printer-uri` (uri) 和 `job-id` (integer), 或 `job-uri` (uri)
- `requesting-user-name` (name)

操作组之后是一个或多个包含订阅属性的订阅组：

`notify-recipient-uri` (uri)

`notify-events` (is1of type2 keyword)

如果创建了订阅，IPP 响应将包含请求中每个订阅组的 `notify-subscription-id` 属性。如果服务器无法创建你指定的所有订阅，服务器将返回 `"client-error-too-many-subscriptions"` 状态码。

## Get-Subscription-Attributes

`Get-Subscription-Attributes` 操作获取订阅对象的属性。典型的 `Get-Subscription-Attributes` 操作在操作组中包含以下属性：

- `attributes-charset` (charset)
- `attributes-natural-language` (naturalLanguage)
- `printer-uri` (uri)
- `notify-subscription-id` (integer)
- `requesting-user-name` (name)

IPP 响应将包含所请求订阅对象的属性。

## Get-Subscriptions

`Get-Subscriptions` 操作获取作业或打印机对象的订阅列表。典型的 `Get-Subscriptions` 操作在操作组中包含以下属性：

- `attributes-charset` (charset)
- `attributes-natural-language` (naturalLanguage)
- `printer-uri` (uri)
- `job-id` (integer) [仅限作业]
- `my-subscriptions` (boolean)
- `limit` (integer)
- `requesting-user-name` (name)

IPP 响应将包含所请求订阅的属性，每个属性都在其自己的订阅组中。如果在 IPP 请求中提供了 `job-id` 属性，则只返回该作业的订阅。否则，将返回与打印机对象相关的所有作业和打印机订阅。

如果 `my-subscriptions` 属性值为 true，则只返回匹配 `requesting-user-name` 的订阅。最后，`limit` 属性将限制返回的订阅数量。对于 CUPS，指定 `printer-uri` 将返回作业、打印机和订阅。

## Renew-Subscription

`Renew-Subscription` 操作续订现有的打印机订阅。只有订阅的所有者或管理员才能续订订阅。典型的 `Renew-Subscription` 操作在操作组中包含以下属性：

```
attributes-charset (charset)
attributes-natural-language (naturalLanguage)
printer-uri (uri)
notify-subscription-id (integer)
requesting-user-name (name)
```

操作组之后是一个包含以下属性的可选订阅组：

```
notify-lease-time (integer)
```

IPP 响应将要么因为订阅已过期而返回错误，要么返回该订阅的新 `notify-lease-time`。

## Cancel-Subscription

`Cancel-Subscription` 操作取消现有的订阅。只有订阅的所有者或管理员才能取消订阅。典型的 `Cancel-Subscription` 操作在操作组中包含以下属性：

```
attributes-charset (charset)
attributes-natural-language (naturalLanguage)
printer-uri (uri)
notify-subscription-id (integer)
requesting-user-name (name)
```

## Get-Notifications

`Get-Notifications` 操作获取指定接收者的任何待处理事件。典型的 `Get-Notifications` 操作在操作组中包含以下属性：

`attributes-charset` (charset)

`attributes-natural-language` (naturalLanguage)

`notify-recipient-uri` (uri)

`notify-no-wait` (boolean)

`notify-no-wait` 属性指定客户端是否希望等待更多事件。如果为 `false`，连接将保持开启直到接收者的订阅过期。如果为 `true`，服务器将发送所有事件并结束响应。默认值为 `false`。

IPP 响应将包含事件组中的通知。每个通知将包含以下属性：

`notify-subscription-id` (integer)

`notify-printer-uri` (uri)

`notify-subscribed-event` (type2 keyword)

`printer-up-time` (integer)

`printer-current-time` (integer)

`notify-sequence-number` (integer)

`notify-charset` (charset)

`notify-natural-language` (naturalLanguage)

`notify-user-data` (octetString)

`notify-text` (text)

事件数据可能根据订阅类型和事件包含打印机或作业状态信息。`Get-Notifications` 操作获取的事件将从服务器移除，因为每次新请求只会返回新事件。指定接收者者只能有一个活跃客户端。

## Send-Notifications

`Send-Notifications` 操作用于 ipp 通知方案向另一个 IPP 服务器发送通知。客户端通常不发送此操作。

典型的 `Send-Notifications` 操作在操作组中包含以下属性：

`attributes-charset` (charset)

`attributes-natural-language` (naturalLanguage)

`notify-recipient-uri` (uri)

操作组之后是一个或多个包含要报告事件的通知事件组。每个事件组包含以下属性：

- `notify-subscription-id` (integer)
- `notify-printer-uri` (uri)
- `notify-subscribed-event` (type2 keyword)
- `printer-up-time` (integer)
- `printer-current-time` (integer)
- `notify-sequence-number` (integer)
- `notify-charset` (charset)
- `notify-natural-language` (naturalLanguage)
- `notify-user-data` (octetString)
- `notify-text` (text)

事件数据可能根据订阅类型和事件包含打印机或作业状态信息。



IPP 服务器或客户端将响应 `successful-ok`、`successful-ok-ignored-notifications` 或 `client-error-all-notifications`，取决于接收者能够处理请求中的全部、部分或没有事件。

# 在打印作业中创建

除了 `Create-Printer-Subscription` 和 `Create-Job-Subscription` 操作外，你还可以相同的属性在 `Create-Job`、`Print-Job` 和 `Print-URI` 操作中创建订阅。

典型的 `Print-Job` 操作在操作组中包含以下属性：

- `attributes-charset` (`charset`)
- `attributes-natural-language` (`naturalLanguage`)
- `printer-uri` (`uri`)
- `requesting-user-name` (`name`)

操作组之后是包含任何作业选项的作业组：

- `copies` (`integer`)
- `media` (`type2 keyword | name`)

作业组之后是一个或多个包含订阅创建属性的订阅组：

- `notify-recipient-uri` (`uri`)
- `notify-events` (`1Of type2 keyword`)

最后，文档文件将紧随在 HTTP POST 中的 IPP 请求数据之后。如果作业被接受，IPP 响应将包含 `notify-subscription-id`。

请求中每个订阅组的属性。如果服务器无法创建你指定的所有订阅，服务器将返回 `"client-error-too-many-subscriptions"` 状态码。

# 通知方案

当前的 IPP 规范定义了三种独立的通知方案。图 11.1 显示了这些方案。

![](img/b159ac7fe2135643dc37ccfeef6d3980_228_0.png)

图 11.1

IPP 通知方案。

`mailto` 方案定义了一种即时通知方案，在特定条件发生时发送电子邮件。`indp` 方案提供了一种类似的机制，使用 IPP 作为传输到接收者的传输层。最后，`ippget` 方案提供了一个轮询接口，允许客户端收集自上一次检查以来发生的所有事件列表。

正如你所预期的那样，`mailto` 方案是最受欢迎的，但随着越来越多的应用程序具备 IPP 意识，你可能会看到其他机器可读格式变得流行起来。未来的方案还可能包含对特定即时消息协议的支持，如 AOL 的 AIM。

在使用这些任何通知方案之前，请确保发送 `Get-Printer-Attributes` 请求以获取 `notify-schemes-supported` 属性。

# mailto 通知方案

`mailto` 通知方案使用电子邮件来发送通知。电子邮件通知不可用于作业打印事件；因为这将为打印的每一页生成一封电子邮件。

电子邮件通知是人类可读的文本消息，指定了通知的原因和被订阅对象的当前状态。例如，管理员可以通过请求针对 `"printer-state-change"` 事件的通知，在每次打印机缺纸时都请求发送一封电子邮件。

`notify-recipient-uri` 属性包含使用 `mailto` 方案的接收者的电子邮件地址。

```
mailto:joe@foo.bar.com
```

在 CUPS 中，`mailto` 通知程序负责发送电子邮件通知。

# ippget 通知方案

`ippget` 通知方案将通知事件存储在服务器上，直到接收者使用 `Get-Notifications` 操作请求它们。这种方案通常被称为“轮询”方案，因为服务器通常会在内存中为接收者对待处理的事件排队。然而，`ippget` 方案还支持“流式”模式，该模式会保持服务器与客户端之间的 HTTP 连接开启，直到所有订阅耗尽或客户端关闭连接。

`notify-recipient-uri` 属性包含使用 `ippget` 方案的接收者的 URI：

```
ipp://foo.bar.com/me
```

由于 IPP 服务器会在响应 `Get-Notifications` 请求时向特定接收者发送所有事件，你可能希望为你的应用程序创建一个唯一的类型标识符。在 Unix 下，可以使用 `gethostname()` 和 `getpid()` 函数生成一个相当唯一的 URI：

```
char hostname[1024];
int pid;
char uri[1024];
```

```
gethosthostname(hostname, sizeof(hostname));
pid = getpid();
```

```
snprintf(uri, sizeof(uri), "ippget://%s/%d", hostname, pid);
```

# indp 通知方案

`indp` 通知方案提供了一种间接通知方案，客户端可以请求将特定事件的通知发送到支持 `Send-Notifications` 操作的另一个 IPP 服务器。这种第三方方案对于传播事件信息或通知已转发作业已完成的 IPP 打印服务器可能非常有用。

`notify-recipient-uri` 属性包含使用 `indp` 方案的接收者的 URI。

```
indp://foo.bar.com/resource
```

该属性会在 `Send-Notifications` 操作中随通知中的事件一起传递给远程 IPP 服务器。

## 总结

IPP 通知提供了当作业或打印机对象状态更改时，从服务器获取异步事件通知的手段。打印机订阅在指定时间内有效，而作业订阅仅在作业生存期间有效。当前规范提供了三种交付通知的方法：`mailto`、`ippget` 和 `indp`。

CUPS 增加了服务器订阅，以监控服务器及其打印机和作业对象的状态。CUPS 从 1.2 版本开始支持通知。

# 第12 章

## CUPS 对 IPP 的扩展

本章描述了 CUPS 提供的属性、操作和浏览协议增强。在编写 CUPS 的 IPP 客户端应用程序时，请结合第 7-11 章使用这些信息。

# CUPS 属性

CUPS 定义了若干专门用于 CUPS 操作的额外属性。表 12.1 列出了这些属性。

表 12.1 额外的 CUPS 属性

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `device-class` | `type2 keyword` | 设备类型 |
| `device-info` | `text(127)` | 设备的描述 |
| `device-make-and-model` | `text(127)` | 连接到设备的打印机品牌和型号 |
| `ppd-natural-language` | `naturalLanguage` | PPD 文件的语言 |
| `ppd-make` | `text(127)` | PPD 文件的制造商 |
| `ppd-make-and-model` | `text(127)` | PPD 文件的品牌和型号 |
| `ppd-name` | `name(255)` | PPD 文件的名称 |
| `printer-type-mask` | `type2 keyword` |  |

# device-class

`device-class` 属性定义了设备类型，可以是表 12.2 列出的类型之一。

表 12.2 设备类

| 关键字 | 描述 |
| --- | --- |
| `file` | 磁盘 |
| `direct` | 直接连接 |
| `serial` | 串口 |
| `network` | 网络连接 |

# device-info

`device-info` 属性提供了设备的描述。

# device-make-and-model

`device-make-and-model` 属性提供了连接到设备的打印机品牌和型号。

# ppd-natural-language

`ppd-natural-language` 属性提供了 PPD 文件的语言，例如“en”代表英语，“es”代表西班牙语。

# ppd-make

`ppd-make` 属性提供了 PPD 文件的制造商。

# ppd-make-and-model

`ppd-make-and-model` 属性提供了 PPD 文件的品牌和型号。

# ppd-name

`ppd-name` 属性提供了 PPD 文件的文件名。

# printer-type-mask

`printer-type-mask` 属性在处理 `CUPS-Get-Printers` 请求时指定打印类型位。

# CUPS 操作

CUPS 定义了新的 IPP 操作。表 12.3 列出了它们。

表 12.3 CUPS 操作

| 代码 | 名称 | 描述 |
| --- | --- | --- |
| `0x4001` | `CUPS-Get-Default` | 获取默认打印机 |
| `0x4002` | `CUPS-Get-Printers` | 获取打印机列表 |
| `0x4003` | `CUPS-Add-Printer` | 在服务器上添加打印机 |
| `0x4004` | `CUPS-Delete-Printer` | 从服务器上删除打印机 |
| `0x4005` | `CUPS-Get-Classes` | 获取类列表 |
| `0x4006` | `CUPS-Add-Class` | 在服务器上添加类 |
| `0x4007` | `CUPS-Delete-Class` | 从服务器上删除类 |
| `0x4008` | `CUPS-Accept-Jobs` | 允许打印机或类接受作业（类似于 Enable-Printer） |
| `0x4009` | `CUPS-Reject-Jobs` | 拒绝打印机或类接受作业（类似于 Disable-Printer） |
| `0x400A` | `CUPS-Set-Default` | 设置默认打印机 |
| `0x400B` | `CUPS-Get-Devices` | 获取可用的打印设备列表 |
| `0x400C` | `CUPS-Get-PPDs` | 获取可用的打印机驱动程序列表 |
| `0x400D` | `CUPS-Move-Job` | 将作业移动到另一个打印机或类 |
| `0x400E` | `CUPS-Add-Device` | 向设备列表中添加或修改设备 |
| `0x400F` | `CUPS-Delete-Device` | 从设备列表中删除设备 |

## IPP 第 12 章 CUPS 扩展

IPP 响应将包含各个打印机组中每个打印机的打印属性。`printer-type`、`printer-type-mask`、`requested-attributes` 和 `limit` 属性将限制请求返回的属性和打印机。

## CUPS-Add-Printer

`CUPS-Add-Printer` 操作在服务器上添加或修改打印机。一个典型的 `CUPS-Add-Printer` 操作在操作组中包含以下属性：

- `attributes-charset` (`charset`)
- `attributes-natural-language` (`naturalLanguage`)
- `printer-uri` (`uri`)
- `requesting-user-name` (`name`)
- `ppp-name` (`name`)
- `device-uri` (`uri`)
- `printer-is-accepting-jobs` (`boolean`)
- `printer-state` (`type2 enum`)

`printer-uri` 属性指定新的打印机名称，必须符合以下格式：

```
ipp://ServerName/printers/PrinterName
```

`ppd-name` 属性是可选的，指定用于打印机的 PPD 文件。PPD 文件也可以从客户端通过 IPP 请求数据发送。

`device-uri` 属性指定要连接的设备。

`printer-is-accepting-jobs` 和 `printer-state` 属性指定所创建的打印机对象的状态。如果没有指定，打印机将默认为已停止（stopped）并拒绝任务。

IPP 响应将返回请求的状态。

POST 请求路径必须为 `/admin`。`requesting-user-name` 或认证用户必须是系统组的成员。

## CUPS-Delete-Printer

`CUPS-Delete-Printer` 操作从服务器上移除打印机。一个典型的 `CUPS-Delete-Printer` 操作在操作组中包含以下属性：

- `attributes-charset` (`charset`)
- `attributes-natural-language` (`naturalLanguage`)
- `printer-uri` (`uri`)
- `requesting-user-name` (`name`)

IPP 响应将返回请求的状态。

POST 资源路径必须为 `/admin`。`requesting-user-name` 或认证用户必须是系统组的成员。

## CUPS-Get-Classes

`CUPS-Get-Classes` 操作获取可用打印机类对象的列表。一个典型的 `CUPS-Get-Classes` 操作在操作组中包含以下属性：

- `attributes-charset` (`charset`)
- `attributes-natural-language` (`naturalLanguage`)
- `printer-type` (`type2 enum`)
- `printer-type-mask` (`type2 enum`)
- `requested-attributes` (`setOf keyword`)
- `limit` (`integer`)

IPP 响应将包含各个打印机组中每个打印机类的属性。`printer-type`、`printer-type-mask`、`requested-attributes` 和 `limit` 属性将识别请求返回的打印机和属性。

## CUPS-Add-Class

`CUPS-Add-Class` 操作在服务器上添加或修改打印机类。`CUPS-Add-Class` 操作在操作组中包含以下属性：

- `attributes-charset` (`charset`)
- `attributes-natural-language` (`naturalLanguage`)
- `printer-uri` (`uri`)
- `requesting-user-name` (`name`)
- `member-uris` (`setOf uri`)
- `printer-is-accepting-jobs` (`boolean`)
- `printer-state` (`type2 enum`)

`printer-uri` 属性指定新的打印机名称，必须符合以下格式：

```
ipp://ServerName/printers/PrinterName
```

`member-uris` 属性列出了属于打印机类的打印机对象。URI 必须是服务器知的（即 URI 必须在 `CUPS-Get-Printers` 或 `CUPS-Get-Classes` 请求中报告）。

`printer-is-accepting-jobs` 和 `printer-state` 属性指定所创建的打印机对象的状态。如果没有指定这些属性，打印机将默认为已停止（stopped）并拒绝任务。

IPP 响应将返回请求的状态。

POST 资源路径必须为 `/admin`。`requesting-user-name` 或认证用户必须是系统组的成员。

## CUPS-Delete-Class

`CUPS-Delete-Class` 操作从服务器上移除打印机类。一个典型的 `CUPS-Delete-Class` 操作在操作组中包含以下属性：

- `attributes-charset` (`charset`)
- `attributes-natural-language` (`naturalLanguage`)
- `printer-uri` (`uri`)
- `requesting-user-name` (`name`)

IPP 响应将返回请求的状态。

POST 资源路径必须为 `/admin`。`requesting-user-name` 或认证用户必须是系统组的成员。

## CUPS-Accept-Jobs

`CUPS-Accept-Jobs` 操作将 `printer-is-accepting-jobs` 属性更改为 `true`，其类似于 Enable-Printer 操作。一个典型的 `CUPS-Accept-Jobs` 操作在操作组中包含以下属性：

- `attributes-charset` (`charset`)
- `attributes-natural-language` (`naturalLanguage`)
- `printer-uri` (`uri`)
- `requesting-user-name` (`name`)

IPP 响应将返回请求的状态。

POST 资源路径必须为 `/admin`。`requesting-user-name` 或认证用户必须是系统组的成员。

## CUPS-Reject-Jobs

`CUPS-Reject-Jobs` 操作将 `printer-is-accepting-jobs` 属性更改为 `false`，其类似于 Enable-Printer 操作。一个典型的 `CUPS-Reject-Jobs` 操作在操作组中包含以下属性：

- `attributes-charset` (`charset`)
- `attributes-natural-language` (`naturalLanguage`)
- `printer-uri` (`uri`)
- `requesting-user-name` (`name`)

IPP 响应将返回请求的状态。

POST 资源路径必须为 `/admin`。`requesting-user-name` 或认证用户必须是系统组的成员。

## CUPS-Set-Default

`CUPS-Set-Default` 操作设置服务器上的默认打印机。一个典型的 `CUPS-Set-Default` 操作在操作组中包含以下属性：

- `attributes-charset` (`charset`)
- `attributes-natural-language` (`naturalLanguage`)
- `printer-uri` (`uri`)
- `requesting-user-name` (`name`)

IPP 响应将返回请求的状态。



POST 资源路径必须为 `/admin`。`requesting-user-name` 或认证用户必须是系统组的成员。

## CUPS-Get-Devices

`CUPS-Get-Devices` 操作获取可用打印机的列表。一个典型的 `CUPS-Get-Devices` 操作在操作组中包含以下属性：

- `attributes-charset` (`charset`)
- `attributes-natural-language` (`naturalLanguage`)
- `device-class` (`keyword`)
- `limit` (`integer`)

IPP 响应将返回打印机列表。每个设备将在自己的组中包含以下属性：

- `device-class`
- `device-info`
- `device-make`
- `device-make-and-model`
- `device-uri`

`device-class` 和 `limit` 属性可以限制报告的设备类型和数量。如果设备代表一类设备，`device-uri` 属性将仅包含方案名称。例如，AppSocket 设备显示为 "socket"，因为同一个方案可以对应多个地址。

## CUPS-Get-PPDS

`CUPS-Get-PPDS` 操作获取打印程序列表。一个典型的 `CUPS-Get-PPDS` 操作在操作组中包含以下属性：

- `attributes-charset` (`charset`)
- `attributes-natural-language` (`naturalLanguage`)
- `ppd-make` (`name`)
- `limit` (`integer`)

IPP 响应将返回 PPD 列表。每个 PPD将在自己的组中包含以下属性：

```
ppd-make
ppd-make-and-model
ppd-name
ppd-natural-language
```

`ppd-make` 和 `limit` 属性可以限制报告的品牌和数量。

## CUPS-Move-Job

`CUPS-Move-Job` 操作将打印任务移动到另一个打印机或打印机类。只有所有者或管理员可以移动任务。一个典型的 `CUPS-Move-Job` 在操作组中包含以下属性：

```
attributes-charset (charset)
- attributes-natural-language (naturalLanguage)
- printer-uri (uri) and job-id (integer) or job-uri (uri)
- job-printer-uri (uri)
- requesting-user-name (name)
```

任务将移动到 `job-printer-uri` 属性指定的打印机或类。该打印机或类必须存在于本地服务器。

IPP 响应将返回任务更新后的 `job-uri`、`printer-uri` 和 `job-id`。

## CUPS-Add-Device

`CUPS-Add-Device` 操作在服务器上添加或修改打印机设备。`CUPS-Add-Device` 操作在操作组中包含以下属性：

```
attributes-charset (charset)
- attributes-natural-language (naturalLanguage)
- device-uri (uri)
- requesting-user-name (name)
- device-class (keyword)
- device-info (text)
- device-make-and-model (text)
```

`device-uri` 属性指定要添加或修改的设备。其他属性指定设备的信息和状态。

# 第二部分 互联网打印协议

IPP 响应将返回请求状态。

POST 资源路径必须为 `/admin`。请求用户名或经过身份验证的用户必须是系统组的成员。

## CUPS-Delete-Device

`CUPS-Delete-Device` 操作从服务器中移除打印机设备。一个典型的 `CUPS-Delete-Device` 操作包含操作组中的以下属性：

- `attributes-charset` (`charset`)
- `attributes-natural-language` (`naturalLanguage`)
- `device-uri` (`uri`)
- `requesting-user-name` (`name`)

IPP 响应将返回请求状态。

POST 资源路径必须为 `/admin`。请求用户名或经过身份验证的用户必须是系统组的成员。

## CUPS 浏览协议

CUPS 浏览协议由一行多达 1450 字节的字节组成，在 UDP 端口 631 上广播。服务器向局域网内的所有本地打印机和类发送 UDP 数据包，但不会发送给隐式类（implicit classes）。客户端接收并添加本地打印机和类，然后根据可用的网络打印机和类按需要创建或更新隐式类。

每个 UDP 数据包恰好包含一行浏览数据。每行由空格分隔的数据组成，描述一台打印机：

```
type SP state uri SP "location" SP "info" SP "make-and-model" NL
```

其中 `SP` 是 ASCII 空格字符（十进制 32），`NL` 是 ASCII 换行字符（十进制 10）。

`type` 字段是 `printer-type` 属性的十六进制值。

`state` 字段是 `printer-state` 属性的十进制值。

`uri` 字段是 `printer-uri-supported` 属性中第一个 URI 的值。

`location` 字段是双引号内的 `printer-location` 属性值。

`info` 字段是双引号内的 `printer-info` 属性值。

`make-and-model` 字段是双引号内的 `printer-make-and-model` 属性值。

## 总结

CUPS 支持许多新操作来管理多个打印机对象、打印机类、设备以及打印机驱动程序的 PPD 文件。对于更改服务器状态的 CUPS 操作，POST 资源路径必须为 `/admin`，而查询操作可以使用任何资源路径。

CUPS 浏览协议提供了一种基于 UDP 的简单协议，用于将打印机信息传递给网络上的其他主机。在网络上传的每个数据包都描述服务器上的单台打印机或类。

# 部分

# 使用 CUPS 编程

- 13 CUPS 编程概述
- 14 使用 CUPS API 函数
- 15 使用 CUPS 发送 IPP 请求
- 16 为 CUPS 编写文件过滤器
- 17 为 CUPS 编写打印机驱动
- 18 为 CUPS 编写后端 (Backends)
- 19 为 CUPS 编写通知器 (Notifiers)

# 第13 章

## CUPS 编程概述

本章涵盖了从头文件到库的 CUPS 编程基础。它还讨论了所使用的许可证以及它们如何影响你的软件。

### 基础

CUPS 提供了两个库，应用程序和其他程序用于与 CUPS 服务器通信并管理 CUPS 数据。你通常在 C 或 C++ 代码中访问这些库；但是，通过适当的钩子，也可以从 Java、Perl、PHP 和 Python 等语言访问。

在源代码中，通过包含头文件来访问 CUPS 库。然后将最终程序与 CUPS 库文件链接，形成可执行程序。

## 头文件

CUPS 提供了许多定义 CUPS 库中常量、数据结构和函数的头文件。头文件位于 `cups` 子目录中，通常使用 `#include` 指令访问。

```
#include <cups/cups.h>
```

`<cups/cups.h>` 头文件定义了大多数 CUPS 程序将使用的基本数据结构和接口。表 13.1 列出了 CUPS 头文件。

表 13.1 CUPS 头文件

| 文件名 | 描述 |
| :--- | :--- |
| `<cups/cups.h>` | 定义通用的 CUPS 常数、结构体和函数 |
| `<cups/http.h>` | 定义超文本传输协议 (HTTP) 接口 |
| `<cups/image.h>` | 定义 CUPS 接口 |
| `<cups/ipp.h>` | 定义互联网打印协议 (IPP) 接口 |
| `<cups/language.h>` | 定义国际化 (I18N) 消息目录和接口 |
| `<cups/md5.h>` | 定义消息摘要 5 (MD5) 接口 |
| `<cups/ppd.h>` | 定义 Postscript 打印机描述 (PPD) 文件接口 |
| `<cups/raster.h>` | 定义 CUPS 栅格文件接口 |

包含 `<cups/cups.h>` 头文件时，会自动包含 `<cups/http.h>`, `<cups/ipp.h>`, `<cups/md5.h>` 和 `<cups/ppd.h>` 头文件。

## 库

CUPS 提供了两个可以在程序使用的库。第一个是 `cups` 库，它提供了所有的 CUPS 函数*除了*在 `<cups/image.h>` 和 `<cups/raster.h>` 头文件中定义的函数。你使用 `-cups` 选项在程序中包含此库：

```
cc -o myprogram myprogram.c -cups
```

第二个库是 `cupsimage`，它提供了 `<cups/image.h>` 和 `<cups/raster.h>` 头文件中定义的所有函数。你使用 `-cupsimage` 选项在程序中包含此库：

```
cc -o myprogram myprogram.c -cupsimage
```

## 你的 CUPS 程序

对于你的第一个 CUPS 程序，我们将列出系统上的默认打印机和可用打印机。为了实现这一点，我们将使用 `cupsDefault()` 和 `cupsGetPrinters()` 函数。列表 13.1 显示了完整的程序。

# 列表 13.1 firstcups.c 源

```
/* 包含 CUPS 头文件 */
#include <cups/cups.h>
```

```
int                                     /* 0 - 退出状态 */
main(void)
{
    int i;                              /* 循环变量 */
    int num_printers;                   /* 打印机数量 */
    char **printers;                   /* 打印机列表 */
    const char *default_printer;      /* 默认打印机 */

    /* 获取默认打印机 */
    default_printer = cupsDefault();

    /* 显示默认打印机 */
    if (default_printer != NULL)
        printf("默认打印机是 %s\n", default_printer);
    else
        puts("没有默认打印机。");

    /* 获取打印机列表 */
    num_printers = cupsGetPrinters(&printers);

    /* 显示可用打印机 */
    if (num_printers > 0)
    {
        puts("可用打印机有：");

        for (i = 0; i < num_printers; i++)
            printf("%s\n", printers[i]);

        /* 释放打印机列表 */
        for (i = 0; i < num_printers; i++)
            free(printers[i]);

        free(printers);
    }
    else
        puts("系统上没有打印机。");
    return 0;
}
```

# 列表 13.1 续

```c
/* 无错误返回 */
return (0);
}
```

`cupsGetDefault` 函数返回一个包含默认打印机的字符串。如果没有定义默认打印机，则返回一个 NULL 指针：

```c
/* 获取默认打印机 */
default_printer = cupsGetDefault();
```

```c
/* 显示默认打印机 */
if (default_printer != NULL)
    printf("The default printer is %s\n", default_printer);
else
    puts("There is no default printer.");
```

`cupsGetPrinters()` 函数返回可用打印机的数量以及一个指向字符串数组的指针：

```c
* 获取打印机列表 */
num_printers = cupsGetPrinters(&printers);
```

```c
* 显示可用的打印机 */
if (num_printers > 0)
{
    puts("The available printers are:");
    for (i = 0; i < num_printers; i++)
        printf("%s\n", printers[i]);
}
```

该字符串数组是使用 `malloc()` 和 `strdup()` 函数分配的，在完成使用后，你必须对每个字符串以及整个数组调用 `free()`：

```c
* 释放打印机列表 */
for (i = 0; i < num_printers; i++)
    free(printers[i]);

free(printers);
```

编译此程序请使用以下命令：

```bash
cc -o firstcups firstcups.c -lcups
```

在某些系统上，你可能还需要 `nsl` 和 `socket` 库：

```bash
cc -o firstcups firstcups.c -lcups -lnsl
```

```bash
cc -o firstcups firstcups.c -lcups -lnsl -lsocket
```

程序编译完成后，你可以运行它来获取默认和可用打印机。

输出应该类似于所示：

```
./firstcups
The default printer is DeskJet
The available printers are:
DeskJet
LaserJet
StylusColor
StylusPhoto
```

# 使用 GNU Autoconf 检测 CUPS API

现在你已经开发了使用 CUPS 的软件，你可能想将其发布到世界上。如果你分发源代码，将需要一种检测 CUPS 头文件和库的方法。对于大多数软件来说，这意味着创建一个 `configure` 脚本。

GNU autoconf 软件是一个用于生成生成配置脚本的免费开发工具。如果你的软件需要运行在多个平台上，`autoconf` 可能是最好的解决方案。你可以在网上找到 autoconf 软件：

```
http://www.gnu.org/software/autoconf/autoconf.html
```

如果你在 Linux 操作系统上开发软件，很有可能你已经加载了 autoconf。

# Autoconf 基础

Autoconf 从一个名为 `configure.in` 的源文件构建配置脚本。该配置脚本可以被用于创建头文件、Makefile 以及你能想象的任何其他类型的文本文件。

`configure.in` 文件包含了一系列针对程序、库和文件的测试。你也可以使用普通的 shell 命令编写自定义测试。上一节中 CUPS 程序的命令脚本看起来就像列表 13.2。

# 列表 13.2 autoconf 源文件中的 configure.in

```bash
dnl 查找应该在分发包中的源文件。
AC_INIT(firstcups.c)
```

```bash
dnl 生成 config.h 文件。
AC_CONFIG_HEADER(config.h)
```

# 列表 13.2 续

```bash
dnl 查找 C 编译器。
AC_PROG_CC
dnl 获取操作系统。
uname=$(uname)
if test $uname = IRIX64; then
  uname=IRIX
fi

dnl 如果需要，获取网络库。
AC_CHECK_LIB(socket,socket)
if test "$uname" != "IRIX"; then
  LIBS="-lsocket $LIBS"
else
  echo "Not using -lsocket since you are running IRIX"
fi

AC_CHECK_LIB(nsl,gethostbyaddr)
if test "$uname" != "IRIX"; then
  LIBS="-lnsl $LIBS"
else
  echo "Not using -lnsl since you are running IRIX"
fi

dnl 查找 cups 库和头文件。
AC_CHECK_LIB(cups,cupsPrintFiles)
AC_CHECK_HEADER(cups/cups.h, AC_DEFINE(HAVE_CUPS))

dnl 如果没有 CU，则停止。
if test $ac_cv_lib_cups_cupsPrintFiles= no -o $ac_cv_header_cups_h= no; then
  AC_MSG_ERROR(Could not find CU.)
fi
dnl 生成 Makefile
AC_OUTPUT(Makefile)
```

你可能首先注意到注释是以 `dnl` 字符开头的，它代表“do not load”（不加载）。你也可以像在普通 shell 脚本中用井号 `#` 作为注释。

每个 `configure.in` 文件必须包含一个 `AC_INIT` 命令，该命令指定分发包中一个必须存在的源文件，以便配置脚本能够工作。这可以是你程序中的一个 C 源文件，也可以是你预期包含在分发中的任何其他文件。



```bash
dnl 查找应该在分发包中的源文件。
AC_INIT(firstcups).
```

另一个常用命令是 `AC_CONFIG_HEADER`，它指定了要生成的头文件名，并包含了 `configure` 脚本的所有定义。

```bash
dnl 生成一个 config.h 文件。
AC_CONFIG_HEADER(config.h).
```

`AC_PROG_CC` 命令紧随在检查任何库或头文件之前。它基本上决定了使用哪个 C 编译器及其位置。如果你的系统有供应商提供的 C 编译器 (`cc`) 和 GNU C 编译器 (`gcc`)，`AC_PROG_CC` 命令将选择编译器。

```bash
dnl 查找 C 编译器。
AC_PROG_CC
```

在发布 `AC_PROG_CC` 命令后，我们可以使用 `AC_CHECK_LIB` 和 `AC_CHECK_HEADER` 命令检查库。对于 CUPS，我们必须确定是否需要 `socket` 和 `nsl` 库：

```bash
dnl 如果需要，获取网络库。
AC_CHECK_LIB(socket,
if test "$uname" != "IRIX"; then
  LIBS="-lsocket $LIBS"
else
  echo "Not using -lsocket since you are running IRIX"
fi)
```

```bash
AC_CHECK_LIB(nsl,gethostbyaddr,
if test "$uname" != "IRIX"; then
  LIBS="-lnsl $LIBS"
else
  echo "Not using -lnsl since you are running IRIX"
fi)
```

然后我们可以检查 cups 库和头文件：

```bash
dnl 查找 cups 库和头文件。
AC_CHECK_LIB(cups,cupsPrintFiles)
AC_CHECK_HEADER(cups/cups.h, AC_DEFINE(HAVE_CUPS))
```

```bash
dnl 如果没有 CU，则停止。
if test $ac_cv_lib_cups_cupsPrintFiles= no -o $ac_cv_header_cups_h= no;
then
  AC_MSG_ERROR(Could not find CU.)
fi
```

# CUPS 编程第13章概述

`AC_DEFINE` 命令在你的程序中定义 C 常量。它通常出现在 `config.h` 头文件中。`AC_MSG_ERROR` 命令显示错误消息并停止配置脚本。防止用户在安装所需文件之前编译你的程序。

最后，`AC_OUTPUT` 命令为程序生成 Makefile：

```bash
dnl 生成 Makefile
AC_OUTPUT(Makefile)
```

## config.h 头文件

尽管 `config.h` 头文件是配置过程的可选部分，但简单的软件会使用它。这是因为每个库和头的检查都会为源文件创建一个定义；如果没有 `config.h` 头文件来保存它们，这些定义会被添加到 Makefile 中的编译器选项。对于某些程序，这些定义会让命令变得非常长！

`config.h` 头文件是从名为 `config.in` 的源文件构建的。列表 13.3 显示了我们示例 CUPS 的 `config.in` 文件。

### 列表 13.3 config.in 源文件

```c
/* 此文件自动生成。请勿手动编辑！ */
#undef HAVE_LIBC
#undef HAVE_CUPS_H
```

你可以看到，`config.in` 文件并不多。任何 `AC_DEFINE` 定义都使用预处理器的 `#undef` 命令包含。如果相应的名称在 `configure` 脚本中有定义，`#undef` 将被 `#define` 替换。

## Makefile

拼图的最后一块是 Makefile。该文件由 `make` 程序制作，将各种源文件编译成一个或多个程序。`configure` 脚本可以从 `Makefile.in` 文件为你生成 Makefile。列表 13.4 显示了我们示例应用的 `Makefile.in` 文件。

### 列表 13.4 Makefile.in 源文件

```make
# C 编译器选项
CC = @CC@
CFLAGS = @CFLAGS@
LIBS = @LIBS@
```

### 列表 13.4 续

```make
# 源文件
SRCS = firstcups.c
```

```make
# 对象文件
OBJS = $(SRCS:.c=.o)
```

```make
# 生成 firstcups 应用
firstcups$(OBJS)
	$(CC) $(CFLAGS) -o firstcups $(OBJS) $(LIBS)
```

```make
# 依赖
$(OBJS): config.h Makefile
```

`configure` 脚本中的每个值都使用 `@NAME@` 法插入 Makefile。Makefile 的开头设置了 C 编译器 (`cc`)、C 编译器选项 (`CFLAGS`) 以及要使用的库 (`LIBS`)：

```make
# C 编译器选项
CC = @CC@
CFLAGS = @CFLAGS@
LIBS = @LIBS@
```

Makefile 的其余部分是静态的，并将 `firstcups` 程序与 `firstcups.c` 源文件关联。

## 整合一切

在创建了 `config.in`、`config.h.in` 和 `Makefile.in` 源文件后，运行 `autoconf` 命令来生成 `configure` 脚本：

```bash
autoconf
```

然后使用以下命令运行 `configure` 脚本：

```bash
./configure
creating cache ./config.cache
checking for gcc... gcc
checking whether the C compiler (gcc) works... yes
checking whether the C compiler (gcc) is a cross-compiler... no
checking whether we are using GNU C...
checking whether gcc accepts -g... yes
checking for socket in -lsocket... no
checking for gethostaddr in -lnsl... yes
checking for cupsPrintFiles in -lcups... yes
```

# CUPS 编程第 13 章概述

检查如何运行 C 预处理器... gcc -E

检查 cups/cups.h... 是的

更新缓存 ./config.cache

创建 ./config.status

创建 Makefile

创建 config.h

这将生成 `config.h` 和 `Makefile` 文件。最后，运行以下命令

```
make ENTER
gcc -g -O2 -c firstcups.o firstcups.c
gcc -g -O2 -o firstcups.o -lcups -lnsl
```

来构建 `firstcups` 程序。

## 许可问题

两个 CUPS 库采用不同的条款许可。如果你正在编写仅供内部使用的软件，或者你将将以源代码的形式向公众发布你的软件，这些许可可能不会对你产生影响。然而，如果你打算分发你的软件，理解它们之间的区别是非常关重要的。

`cups` 库根据 GNU 库通用公共许可证 (`LGPL`) 的条款进行许可。该许可允许你通过提供源代码或使用 GNU 软件许可，将你的程序与 `cups` 库链接。`LGPL` 也是 GNU C 以及其他可用库允许程序员以任何他们认为适当的条款开发软件的许可。

`cupsimage` 根据 GNU 通用公共许可证 (`GPL`) 的条款进行许可。与 `LGPL` 不同，该许可要求使用 `cupsimage` 库的所有程序都按照 `GPL` 的条款提供。除其他要求外，`GPL` 要求分发你软件的源代码。

这些许可的完整文本可在附录 F，“通用 Unix 打印系统许可协议”中找到。如既往，如果你不确定如何将这些许可应用于你的软件，应该咨询律师。你也可以联系 Easy Software Products 以寻求建议，或为你的软件协商不同的许可条件。

### 总结

CUPS 拥有两个库和八个头文件，它们提供了 CUPS 的所有接口。`cups` 库提供了基本的客户端函数，并被所有 CUPS 程序使用。`cupsimage` 库提供成像功能，并被栅化过滤器和打印机驱动程序使用。

由于操作系统的差异，你可能需要也不需要配合 CUPS 使用额外的网络库。管理这些差异的最简单方法是使用 GNU `autoconf` 软件来定位必要的库并配置你的源代码。

CUPS 库以两种许可提供。`cups` 库根据 `LGPL` 提供，以便在开发和分发软件时提供最大的灵活性。`cupsimage` 库根据 `GPL` 提供，并要求使用该库的软件也必须根据 `GPL` 分发。

# 第 14 章

# 使用 CUPS API 函数

# 使用 CUPS 编程

本章将向你展示如何使用 CUPS API 函数获取可用打印机列表、提交打印作业，并从你的应用程序中管理打印作业。你还将学习如何从应用程序访问 PostScript 打印机描述 (`PPD`) 文件，并使用它们显示打印机特定选项并为特定打印机自定义你的输出。

## 打印服务

CUPS 提供了许多函数来管理打印机、类、作业和选项。

## 管理打印机和类

CUPS 同时支持打印机和打印机类。第 13 章中的第一个 CUPS 程序“CUPS 编程概述”引入了两个 CUPS 函数：`cupsDefault()` 和 `cupsGetPrinters()`，它们检索了当前默认打印机和打印机列表。第三个函数 `cupsGetClasses()` 可用于从服务器检索打印机类列表。

`cups-default` 函数不接受任何参数，并返回当前默认打印机或类的名称。如果没有定义默认打印机或类，则返回一个 `NULL` 指针：

`cupsDefault()` 返回的字符串存储在静态缓冲区中，每次调用时都会被覆盖。

`cupsClasses()` 函数检索打印机类列表并接受单个参数，即指向 `char` 变量的指针。它返回类的数量：

```
int i;
int num_classes;
char **classes;

num_classes = cupsGetClasses(&classes);
if (num_classes == 0)
    puts("No printer classes found.");
else
{
    printf("%d printer class(es) were found:\n", num_classes);
```

# 使用 CUPS API 函数 第 14 章

```
for (i = 0; i < num_classes; i++))
    printf("%s\n", classes[i]);
}
```

同样，`cupsGetPrinters()` 函数检索打印机列表：

```
int i;
int num_printers;
char **printers;
```

```
num_printers = cupsGetPrinters(&printers);
if (num_printers == 0)
    puts("No printers found.");
else
{
    printf("%d printer were found:\n", num_printers);
    for (i = 0; i < num_printers; i ++)
        printf("%s\n", printers[i]);
}
```

`GetClasses()` 和 `cupsGetPrinters()` 都返回一个使用 `malloc()` 函数分配的字符串数组。在释放字符串使用的内存之前，你必须释放打印机或类名称的字符串，然后释放数组指针。如果打印机或类的数量为 0，不要尝试释放数组：

```
if (num_classes > 0)
{
    for (i = 0; i < num_classes; i ++)
        free(classes[i]);
}
```

```
if (num_printers > 0)
{
    for (i = 0; i < num_printers; i ++)
        free(printers[i]);
    free(printers);
}
```

列表 14.1 显示了如何结合这些函数来显示默认打印机或类以及可用打印机。

# 列表 14.1 结合这些函数显示默认打印机或类以及可用打印机

# 列表 14.2 继续

在调用 `cupsJobs()` 获取激活的打印任务后，我们在循环中显示任务列表。

输出结果如下：

**.showjobs ENTER**

找到 4 个任务：

| Job ID | 目标 | Title | 用户 | Size |
| --- | --- | --- | --- | --- |
| 42 | LaserJet | Test Page | mike | 12k |
| 43 | DeskJet | showdeeds.c | mike | 2k |
| 44 | StylusColor | Test Page | mike | 12k |
| 45 | StylusPhoto | showjobs.c | mike | 1k |

## 探索打印机选项

打印机选项是 CUPS 不同于传统的 LPD 软件的特性之一。CUPS API 将选项作为 `cups_option_t` 结构体数组暴露。`cups_option_t` 结构包含一个名称和一个值字符串，API 函数会根据需要将它们转换为相应的 IPP 属性类型。

### 添加选项

CUPS 提供了几个管理打印机选项的函数。第一个是 `cupsAddOption()`。它向选项数组中添加单个选项：

```
#include <cups/cups.h>
...
int    num_options;
cups_option_t *options;
...
num_options = 0;
options = NULL;

num_options = cupsAddOption("name", "value", num_options, &options)
num_options = cupsAddOption("name", "value", num_options, &options)
num_options = cupsAddOption("name", "value", num_options, &options)
num_options = cupsAddOption("name", "value", num_options, &options)
```

名称字符串是选项的名称，且不区分大小写；也就是说，“name" 和 "NAME" 是相同的。

值字符串是该选项的值。值数组之间用逗号（,）分隔，并使用减号（-）。

`num_options` 和 `options` 参数分别是当前选项的数量以及 `cups_option_t *` 变量的引用。

每次调用 `cupsAddOption()` 都会返回作为整数类型的新选项数量。`options` 指针将更新为指向更新后的数组。

添加多个相同名称的选项只会创建一个该选项的副本，并保留之前的值。不要假设调用 `cupsAddOptions()` 20 次会产生一个包含 20 个选项的数组。

### 添加多个选项

`cupsAddOption()` 向数组添加单个选项，而 `cupsParseOptions()` 函数将添加字符串中传递的零或多个选项：

```
#include <cups/cups.h>
int    num_options;
```

# 第三部分 使用 CUPS 编程

```
cups_option_t *options;
...
num_options = 0;
options = NULL;
```

```
num_options = cupsParseOptions("name=value name2=value2", num_options, &options);
```

字符串中的选项用空格分隔。字符串中的值用单引号（')或双引号（”）包围，或者使用反斜杠（\）在值包含空格。`lp` 和 `lpr` 命令以及许多 CUPS 过滤器和打印机驱动经常使用 `cupsParseOptions()` 函数。

### 获取选项值

在构建选项数组后，你可以使用 `cupsGetOption()` 函数获取命名选项的当前值：

```
#include <cups/cups.h>
...
int num_options;
cups_option_t *options;
const char *value;
...
value = cupsGetOption("name", num_options, options);
```

名称字符串是选项的名称。`num_options` 和 `options` 参数分别是选项的数量和指向 `cups_option_t` 结构的指针。

如果选项已定义，`cupsGetOption()` 函数返回当前选项值；如果选项未定义，则返回 `NULL`。

### 释放选项使用的内存

在使用完选项数组后，调用 `cupsFreeOptions()` 函数来释放已使用的内存：

```
#include <cups/cups.h>
...
int num_options;
cups_option_t *options;
...
cupsFreeOptions(num_options, options);
```

`num_options` 和 `options` 参数分别是选项的数量和指向 `cups_option_t` 结构的指针。

## 管理目标



CUPS 1.1 引入了“目标”（destination）的概念，而不仅仅是打印机或类。目标是一个打印机或类，它带有一组通常随每个任务发送的关联打印机选项。

使用打印机或类名称以及可选的实例名称来识别目标：

- `DeskJet`
- `DeskJet/Photo`
- `LaserJet`
- `LaserJet/Duplex`

每个实例名称可以包含 127 个字母、数字和下划字符。对于打印机名称，实例名称不区分大小写，这意味着 "`instance`"、"`Instance`" 和 "`INSTANCE`" 都是相同的。为主实例（`DeskJet`、`LaserJet` 等）定义的选项不会自动包含在辅助实例（`DeskJet/Photo`、`LaserJet/Duplex` 等）的选项中。

## 获取可用目标列表

目标存储在 `loptions` 文件（通常位于 `/etc/cups/loptions`）和用户 `loptions` 文件（`~/.loptions`）中。可以使用 `cupsGetDests()` 函数获取可用打印机列表。

```
#include <cups/cups.h>
...
int num_dests;
cups_dest_t *destests;
...
num_dests = cupsGetDests(destests);
```

每个目标都是 `cups_dest_t` 结构体，它定义了打印机或类、实例以及是否为默认目标。

表 14.2 `cups_dest_t` 结构体

| Member | 类型 |  |
| --- | --- | --- |
| name | char * | 打印机或类 |
| instance | char * | 实例（可选） |
| is_default | int | 如果是默认目标则非零 |
| num_options | int | 选项数量 |
| options | cups_option_t * | 该目标的选项 |

# 第三部分 使用 CUPS 编程

你也可以使用由 `cupsAddOption()` 和 `cupsParseOptions()` 函数定义的选项，或者目的地选项与用户选项的组合。

第三个示例使用了为止描述的所有选项、目的地和打印函数。通过获取所有目的地和选项列表：

```
int num_dests;
cups_dest_t *dests;
```

```
num_dests = cupsGetDests(&dests);
```

然后获取当前的默认目的地：

```
cups_dest_t *dest;
```

```
dest = cupsGetDests(NULL, NULL, num_dests, dests);
```

接下来，处理命令行参数。在某些系统上，你可以使用 `getopt()` 函数来处理。然而，许多系统并不提供此函数，而且通过名称解析选项相当简单。支持 "`-d`" 和 "`-P`" 选项来指定打印机，支持 "`-o`" 选项指定打印机选项。

对于 "`-d`" 和 "`-P`" 选项，获取目的地名称，如果指定了实例名称，则将其分离，并使用 `cupsGetDest()` 函数查找目的地：

```
char *name;
char *instance;
```

```
if ((strchr(name, '/')) != NULL)
*instance += '\0';
```

```
dest = cupsGetDest(name, instance, num_dests, dests);
```

对于 "`-o`" 选项，使用 `cupsParseOptions()` 函数添加命令行上的选项：

```
num_options = cupsParseOptions(argv[i], num_options, &options);
```

然后将任何文件名添加到 `const char *s` 类型的数组中，供 `cupsPrintFiles()` 函数使用：

```
int num_files;
const char *files[100];
else if (num_files < 100)
{
    files[num_files] = argv[i];
    num_files++;
}
```

# 第 14 章 使用 CUPS API 函数

在打印文件之前，将用户选项与目的地选项合并。要做到这一点，遍历目的地选项，如果它们尚未定义，则将它们添加到打印选项数组中：

```
for (i = 0; i < dest->num_options; i ++)
if (cupsGetOption(dest->options[i].name, num_options, options) == NULL)
    num_options = cupsAddOption(dest->options[i].name,
        dest->options[i].value,
        num_options, &options);
```

最后，使用 `cupsPrintFiles()` 函数打印文件：

```
int id;
id = cupsPrintFiles(dest->name, num_files, files, files[0],
    num_options, options);
```

最终程序显示在列表 14.3 中。编译程序后，你应该能够使用以下命令对源文件进行漂亮打印：

```
/print -o prettyprint print.c ENTER
Job ID is 123.
```

# 列表 14.3 print.c 源文件

```c
/* 包含 CUPS 头文件 */
#include <cups/cups.h>

int    /* O 退出状态 */
main(int argc, char *argv[]) /* I 命令行参数数量 */
{
    int        /* 循环变量 */
    int        id;             /* 任务 ID */
    int        num_files;      /* 文件数量 */
const char *files[100];    /* 要打印的文件 */
    char       *name;        /* 目的地名称 */
    char       *instance;     /* 实例名称 */
    int        num_dests;      /* 目的地数量 */
cups_dest_t *dests;       /* 目的地 */
cups_dest_t *dest;         /* 当前目的地 */
    int        num_options;    /* 选项数量 */
    cups_option_t *options;   /* 选项 */
```

# 列表 14.3 续

```c
/* 获取目的地列表 */
num_dests = cupsGetDests(&dests);

/* 获取默认目的地 */
dest = cupsGetDest(NULL, NULL, num_dests, dests);

/* 解析命令行 */
num_files = 0;
num_options = 0;
options = NULL;

for (i = 1; i < argc; i++)
  if (strcmp(argv[i], "-d", 2) == 0 ||
      strcmp(argv[i], "-P", 2) == 0)
{
    if (argv[i][2])
      name = argv[i] + 2;
    else
    {
      i++;

      if (i >= argc)
      {
        puts("ERROR: Expected destination name!");
        cupsFreeDests(num_dests, dests);
        cupsFreeOptions(num_options, options);
        return (!1);
      }
    else
      name = argv[i];
  }

  if ((instance = strchr(name, '/')) != NULL)
    *instance++ += '\0';

  if ((dest = cupsGetDest(name, instance, num_dests, dests)) == NULL)
  {
    if (instance != NULL)
      printf("ERROR: %s/%s does not exist!\n", name, instance);
    else
      printf("ERROR: %s does not exist!\n", name);
```

# 列表 14.3 续

```c
cupsFreeDests(num_dests, dests);
cupsFreeOptions(num_options, options);
return (1);
}
else if (strcmp(argv[i], "-o", 2) == 0)
{
    /* 添加一个或多个选项 */
    if (argv[i][2])
    {
        num_options = cupsParseOptions(argv[i], 2, num_options, &options);
    }
    else
    {
        i++;
    }

    if (i >= argc)
    {
        puts("ERROR: Expected option=value!");
        cupsFreeDests(num_dests, dests);
        cupsFreeOptions(num_options, options);
        return (1);
    }

    num_options = cupsParseOptions(argv[i], num_options, &options);
} else if (num_files < 100)
{
    /* 添加文件要打印 */
    files[num_files] = argv[i];
    num_files++;
}

/* 检查是否有要打印的文件... */
if (num_files == 0)
{
    puts("ERROR: Expected print files!");
    cupsFreeDests(num_dests, dests);
    cupsFreeOptions(num_options, options);
    return (1);
}

/* 合并打印机选项 */
for (i = 0; i < dest->num_options; i ++)
  if (cupsGetOption(dest->options[i].name, num_options, options) == NULL)
    num_options = cupsAddOption(dest->options[i].name,
        dest->options[i].value,
        num_options, &options);

/* 打印文件 */
id = cupsPrintFiles(dest->name, num_files, files, files[0],
    num_options, options);

/* 显示任务 ID 或错误 */
if (id > 0)
    printf("Job ID is %d.\n", id);
else
    printf("ERROR: Unable to print - %s\n",
           ippErrorString(cupsLastError()));

/* 错误时返回 1，成功时返回 0 */
return (id < 1);}
```

# PPD 文件

CUPS 包含了访问和操作与打印机驱动程序的 PostScript Description (`PPD`) 文件的函数。每个 `PPD` 文件列出了打印机提供的功能并包含了冲突信息，例如双面输出。

包含 `<cups/ppd.h>` 头文件使用 `PPD` 函数：

```c
#include <cups/ppd.h>
```

`<cups/cups.h>` 头文件也包含了此头文件。

## 获取打印机的 PPD 文件

`cupsGetPPD()` 函数获取命名打印机或类的 `PPD` 文件：

```c
#include <cups/cups.h>
...
const char *filename;
filename = cupsGetPPD("name");
```

`name` 是打印机或类的名称，包括远程服务器名称，例如 "`printer@server`"。

返回值指向静态存储中文件名的指针；该值每次调用 `cupsGetPPD()` 都会被覆盖。如果打印机或类不存在，将返回 `NULL`。此文件名是一个临时文件，因此在使用完成后调用 `unlink()` 移除文件：

```c
unlink(filename);
```

## 加载 PPD 文件

```c
#include <ppd.h>
...
ppd_file_t *ppd;
ppd = ppdOpenFile("filename");
```

`filename` 是要加载的文件名，例如 `cupsGetPPD()` 函数返回的值。

返回值指向描述 `PPD` 文件内容的结构指针，如果无法读取 `PPD` 文件，则返回 `NULL`。

## 释放 PPD 文件使用的内存

当你完成 `PPD` 文件的使用时，调用 `ppdClose()` 函数来释放所有使用的内存：

```c
#include <ppd.h>
...
ppd_file_t *ppd;
...
ppdClose(ppd);
```



# 检查 PPD 文件结构

每个 PPD 文件包含许多能力属性、打印机选项和冲突定义。页面大小选项还包括物理边距以及打印机的最小和最大尺寸。所有这些信息都存储在 `ppd_file_t` 结构中。`ppd_file_t` 结构的成员如表 14.3 所示

## 表 14.3 PPD 能力值

| 名称 | 类型 | 描述 |
|---|---|---|
| accurate_screens | | 打印机是否支持精确色彩的指示 |
| color_device | int | 打印机是否支持色彩空间的指示 |
| | `ppd_cs_t` | 默认色彩空间 |
| num_consts | int | 约束数量 |
| | `ppd_const_t *` | 约束 |
| contour_only | int | 打印机是否仅为连续调的指示 |
| custom_margins | float [4] | 自定义页面大小的左、下、右、上边距 |
| custom_max | float [2] | 自定义页面大小的最大尺寸 |
| custom_min | float [2] | 自定义页面大小支持的最小尺寸 |
| num_emulations | int | 打印机支持的仿真器数量 |
| | `ppd_emul_t *` | 打印机支持的仿真器 |
| num_filters | int | 此打印机的过滤器数量 |
| | char ** | 此打印机的过滤器 |
| flip_duplex | int | 双面打印时打印机是否需要填充反面的指示 |
| num_fonts | int | 打印机拥有的字体数量 |
| | char ** | 打印机上的字体 |
| num_groups | int | 选项组数量 |
| | `ppd_group_t *` | 选项组 |
| jcl_begin | char * | 每个任务前发送的作业控制语言 (JCL) 字符串 | 在 PostScript 模式下放入打印机的 JCL 字符串 |
| jcl_end | char * | 结束任务的 JCL 字符串 | 横向页面的方向 |
| landscape | int | |
| lang_encoding | char * | 用于选项文本的字符集 | 用于选项字符串的语言，如英语、法语或西班牙语 |
| lang_version | char * | PostScript 语言级别，从 1 到 3 |
| language_level | int | |
| manual_copies | int | 是否需要手动复制的指示 |
| manufacturer | char * | 打印机名称 |
| model_number | int | 驱动特定的型号编号 |
| modelname | char * | 打印机型号名称 |

## 表 14.3 续接

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| nickname | char * | 打印机的别名；这通常是显示给用户的名称 |
| patches | char * | 在每个作业前发送给打印机的补丁命令 |
| product | char * | 打印机产品名称 |
| num_profiles | int | 颜色配置的数量 |
| profiles | `ppd_profile_t *` | 颜色配置 |
| shortnickname | char * | 打印机的短别名 |
| num_sizes | int | 尺寸的数量 |
| sizes | char * | 每分钟打印页数 |
| throughput | char * | 提供的 TrueType 字体光栅化器，通常为 "Type42" |
| variable_sizes | int | 打印机是否支持自定义尺寸指示 |

如果相应的 PPD 文件属性未包含在文件中，则大多数字符串值可以为 NULL。特别是，在显示 `manufacturer` 字段的值时要小心，尽管 PPD 规范要求包含，但并非所有 PPD 文件都包含该字段。

## 选项与组

PPD 文件支持多个选项，PPD 函数将其存储在 `ppd_option_t` 和 `ppd_choice_t` 结构中。

每个选项又关联到一个存储在 `ppd_group_t` 结构中的组。组可以在 PPD 文件中指定；如果选项未与任何组关联，则根据选项类型被放入“General”（常规）或“Extra”（额外）组。

PPD 文件的组列表存储在 `num_groups` 和 `groups` 成员中。每个组都有一个可读的名称，例如“General”或“Installable Options”（可安装选项），并包含一个选项数组。

组中的选项位于 `ppd_group_t` 结构的 `num_options` 和 `options` 成员中。每个选项都有一个名称（"PageSize"）、一个可读的名称（"Media Size"）、命令排序信息、一个选项类型（布尔、单选或多选）、该选项的默认选择以及一个选择数组。选项不区分大小写。

选项中的选择位于 `ppd_option_t` 结构的 `num_choices` 和 `choices` 成员中。每个选择都有一个值（"Letter"）、一个可读的名称（"Letter – 8.5x11 inches"）、一个指示该选择是否被标记的布尔值，以及选择该选项时发送给打印机的 PostScript 命令。选择值不区分大小。

## 显示 PPD 文件内容

CUPS 源码包含一个名为 `testppd` 的程序，它可以加载 PPD 文件并显示组、选项和选择。列表 14.4 显示了 `testppd` 的源代码。构建 `testppd` 后，你应该能够运行以下命令：

```
/testppd /usr/share/cups/model/deskjet.ppd ENTER
```

```
FILE: /usr/share/cups/model/deskjet.ppd

language_level = 3

color_device = TRUE

variable_sizes = FALSE

landscape = 90

colorspace = PPD_CS_RGB

num_emulations = 0

lang_encoding = ISOLatin1

lang_version = English

modelname = HP DeskJet Series

rasterizer = Type42

manufacturer = ESP

product = (CUPS v1.1)

nickname = HP DeskJet Series CUPS v1.1

shortnickname = HP DeskJet Series

patches =  bytes

num_groups = 2

group[0] = Extra

options[0] = ColorModel (Output Mode) PICKONE ANY 10

RGB (CMY Color)

CMYK (CMYK Color) *

Gray (Grayscale)

options[1] = Resolution (Output Resolution) PICKONE ANY 20

15dpi (150 DPI)

300dpi (300 DPI) *

600dpi (600 DPI) *

group[1] = General

options[0] = PageSize(Media Size) PICKONE ANY 10

A3 (A3) = 11.69x16.54in(0.2,0.5,11.4,16.0)

A4 (A4) = 8.26x11.69in(0.2,0.5,8.0,11.2)

---

Legal (US Legal) = 8.50x14.00in(0.2,0.5,8.2,13.5) *

Letter (US Letter) = 8.50x11.00in(0.2,0.5,8.2,10.5) *

Tabloid (US Tabloid) = 11.00x17.00in(0.2,0.5,10.8,16.5)
```

## 第 14 章 使用 CUPS API 函数

```
options[1] = InputSlot (Media Source) PICKONE ANY 10

Envelope (Envelope Feed)

Manual (Manual Feed)

Tray (Tray) *

options[2] = MediaType (Media Type) PICKONE ANY 10

Bond (Bond Paper)

Glossy (Glossy Paper)

Plain (Plain Paper) *

Special (Special Paper)

Transparency (Transparency)

options[3] = PageRegion (PageRegion) PICKONE ANY 10

A3 (A3) = 11.69x16.54in(0.2,0.5,11.4,16.0)

A4 (A4) = 8.26x11.69in(0.2,0.5,8.0,11.2)

---

Legal (US Legal) = 8.50x14.00in(0.2,0.5,8.2,13.5) *

Letter (US Letter) = 8.50x11.00in(0.2,0.5,8.2,10.5) *

Tabloid (US Tabloid) = 11.00x17.00in(0.2,0.5,10.8,16.5)
```
*(注：此处原文文本似乎存在重复或截断，已根据要求翻译可见部分)*

## 列表 14.4 testppd.c 源代码

```c
/* 包含 CUPS 头文件。 */
#include <cups/cups.h>

/* 包含字符串定义 */
#include <string.h>

int main(int argc, char *argv[])
{
    /* 0 status */
    /* 命令行参数 */
    int i, j, k, m; /* 循环变量 */
    const char *filename; /* 要加载的文件 */
    ppd_file_t *ppd; /* PPD 记录 */
    ppd_size_t *size; /* 尺寸记录 */
    ppd_group_t *group; /* UI 组 */
    ppd_option_t *option; /* 标准 UI 选项 */
    /* 标准 UI 选择 */
    static char *uis[] = { "BOOLE", "PICKONE", "PICKMANY" };
    static char *sections[] = { "ANY", "DOCUMENT", "EXIT", "PAGE", "PROLOG" };
    /* 显示列出的每个文件的 PPD... */
    if (argc == 1) {
        fprintf(stderr, "Usage: %s ppd.ppd filename.ppd\n", argv[0]);
        return (1);
    }
    for (i = 1; i < argc; i++) {
        if (strstr(argv[i], ".ppd"))
            filename = argv[i];
        else
            filename = cupsGetPPD(argv[i]);
    }
    if ((ppd = ppdOpenFile(filename)) == NULL) {
        fprintf(stderr, "Unable to open '%s' as a PPD file!\n", filename);
        continue;
    }
    printf("FILE: %s\n", filename);
    printf("language_level = %d\n", ppd->language_level);
    printf("color_device = %s\n", ppd->color_device ? "TRUE" : "FALSE");
    printf("variable_sizes = %s\n", ppd->variable_sizes ? "TRUE" : "FALSE");
    printf("landscape = %d\n", ppd->landscape);
    switch (ppd->colorspace) {
        case PPD_CS_CMYK:
            puts("colorspace = PPD_CS_CMYK");
            break;
        case PPD_CS_CMY:
            puts("colorspace = PPD_CS_CMY");
            break;
        case PPD_CS_GRAY:
            puts("colorspace = PPD_CS_GRAY");
            break;
        case PPD_CS_RGB:
            puts("colorspace = PPD_CS_RGB");
            break;
        default:
            puts("colorspace = <unknown>");
            break;
    }
    printf("num_emulations = %d\n", ppd->num_emulations);
    for (j = 0; j < ppd->num_emulations; j++)
        printf("emulations[j] = %s\n", ppd->emulations[j].name);
    printf("lang_encoding = %s\n", ppd->lang_encoding);
    printf("lang_version = %s\n", ppd->lang_version);
    printf("modelname = %s\n", ppd->modelname);
    printf("rasterizer = %s\n", ppd->rasterizer == NULL ? "None" : ppd->rasterizer);
    printf("manufacturer = %s\n", ppd->manufacturer);
    printf("product = %s\n", ppd->product);
    printf("nickname = %s\n", ppd->nickname);
    printf("shortnickname = %s\n", ppd->shortnickname);
    printf("patches = %s\n", ppd->patches);
    printf("num_groups = %d\n", ppd->num_groups);
    for (j = 0, group = ppd->groups; j < ppd->num_groups; j++, group++)
    {
        printf("group[%d] = %s\n", j, group->text);
        for (k = 0, option = group->options; k < group->num_options; k++, option++)
        {
            printf("options[%d] = %s (%s) %s %s\n", k, option->keyword, option->text, option->ui, option->order);
            if (strcmp(option->keyword, "PageSize") == 0 ||
                strcmp(option->keyword, "PageRegion") == 0)
            {
                for (m = 0, choice = option->choices; m > 0; m--, choice++)
                {
                    size = ppdPageSize(ppd, choice->choice);
                    if (size == NULL)
                        printf("%s (%s) = ERROR", choice->choice, choice->text);
                    else
                        printf("%s (%s) = %.2fx%.2fin \n%.1f,%.1f,%.1f,%.1f\n",
                               choice->choice, choice->text,
                               size->width / 72.0, size->length / 72.0,
                               size->left / 72.0, size->bottom / 72.0,
                               size->right / 72.0, size->top / 72.0);
                    if (strcmp(option->defchoice, choice->choice) == 0)
```



```
                        puts("*");

                    else

                        putchar('\n');

                }

            }

            else

                for (m = 0, choice = option->choices; m > 0; m--, choice++)

                {

                    printf("%s (%s) = %d\n", choice->choice, choice->text);

                    if (strcmp(option->defchoice, choice->choice) == 0)

                        puts("*");

                    else

                        putchar('\n');

                }

            }

        }

    }

}
```

## 列表 14.4 延续

```
ppd->profiles[j].matrix[0][2], ppd->profiles[j].matrix[1][0],
ppd->profiles[j].matrix[1][1], ppd->profiles[j].matrix[1][2],
ppd->profiles[j].matrix[2][0], ppd->profiles[j].matrix[2][1],
ppd->profiles[j].matrix[2][2];
printf("num_fonts = %d\n", ppd->num_fonts);
for (j = 0; j < ppd->num_fonts; j ++)
    printf("fonts[%d] = %s\n", ppd->fonts[j]);
ppdClose(ppd);
return (0);
```

# 查找选项

调用 `ppdFindOption()` 函数在 PPD 文件中查找选项：
`#include <cups/ppd.h>`

```
...
ppd_file_t *ppd;
ppd_option_t *option;
...
option = ppdFindOption(ppd, "name");
```

该参数是一个指向 `ppd_file_t` 结构的指针。`name` 参数是选项的名称。如果该选项存在，则返回指向 `ppd_option_t` 结构的指针。否则，返回一个 `NULL` 指针。

# 查找选择

调用 `cupsFindChoice()` 函数查找特定的选项选择：
`ppd_option_t *option;`
`ppd_option_t *choice;`

```
...
choice = cupsFindChoice(option, "Custom");
```

第一个参数是由 `ppdFindOption()` 返回的指向 `ppd_option_t` 结构的指针。第二个参数是选择的名称。

返回值是指向该命名选择的 `ppd_choice_t` 结构的指针，如果该选择不存在，则返回 `NULL`。

类似的函数是 `cupsFindMarkedChoice()`，它用于查找该选项当前被标记的选择：

# 第三部分 使用 CUPS 编程

```
ppd_file_t *pppd;
ppd_choice_t *choice;
...
```

```
choice = ppdFindMarkedChoice(ppd, "PageSize");
```

第一个参数不是解析选项指针，而是一个指向 `ppd_file_t` 结构的指针。紧接着是选项名称。

返回值是指向第一个被标记选择的 `ppd_choice_t` 结构的指针；如果没有选择被标记或者该选项不存在，则返回 `NULL`。

# 标记选项

每个选项都有一个关联的标记状态。被标记的选项可以发送到打印机或显示给用户。

在标记您的自定义选项之前，调用 `ppdMarkDefaults()` 函数标记来自 PPD 文件的默认选项：

```
#include <cups/ppd.h>
..
ppd_file_t *ppd;
..
ppdMarkDefaults(ppd);
```

然后调用 `ppdMarkOption()` 函数来标记单个选项：

```
#include <cups/ppd.h>
..
ppd_file_t *ppd;
int conflicts;
..
conflicts = ppdMarkOption(ppd, "name", "value");
```

`name` 和 `value` 字符串分别选择特定的选项和值。如果选择没有产生任何冲突，则返回 0。

CUPS 还提供了 `cupsMarkOptions()` 函数，用于标记打印机选项中的所有选项：

```
#include <cups/ppd.h>
..
ppd_file_t *ppd;
int num_options;
cups_option_t *options;
int conflicts;
..
conflicts = cupsMarkOptions(ppd, num_options, options);
```

`cupsMarkOptions()` 函数还处理 IPP 选项到 PPD 选项的映射。
返回值为存在的冲突数量。

# 冲突

PPD 文件支持指定不同选项之间的冲突条件。冲突存储在 `pp_conflict_t` 结构中，这些结构指定了相互冲突的选项。

`ppdMarkOption()` 和 `cupsMarkOptions()` 函数返回与当前标记选项冲突的数量。

您还可以调用 `ppdConflicts()` 函数，在标记所有选项后获取冲突数量：

```
#include <cups/cups.h>
ppd_file_t *ppd;
int conflicts;
conflicts = ppdConflicts(ppd);
```

返回值为冲突选项的数量，如果不存在冲突，则返回 0。由于这些冲突的对称性（A 与 B 冲突，因此 B 与 A 冲突），冲突计数始终是一个偶数。

# 页面尺寸

PPD 文件指定了所有的页面尺寸及其相关的物理边距。这些尺寸存储在 `ppd_size_t` 结构中，并可以在 `ppd_file_t` 结构的 `num_sizes` 成员可用。您可以使用 `ppdPageWidth(int)`、`ppdPageLength(int)` 和 `ppdPageSize()` 函数查找特定的页面尺寸：

```
#include <cups/cups.h>
ppd_size_t *size;
float width;
float length;
size = ppdPageSize(ppd, "size");
width = ppdPageWidth(ppd, "size");
length = ppdPageLength(ppd, "size");
```

尺寸字符串是命名的页面尺寸选项。宽度和长度以磅（points）计算；每英寸 72 磅。`ppd_size_t` 结构包含宽度、长度。

# 尺寸（表 14.4 PPD 结构成员）

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| size | char | 命名的页面尺寸选项 |
| width | float | 宽度（磅） |
| length | float | 长度（磅） |

该尺寸字符串是命名的页面尺寸选项。宽度和长度以磅计算；每英寸 72 磅。`ppd_size_t` 结构包含宽度、长度。

# 自定义尺寸

- `HTTP_ENCRYPT_IF_REQUESTED`: 仅当服务器请求时加密
- `HTTP_ENCRYPT_NEVER`: 从不加密
- `HTTP_ENCRYPT_REQUIRED`: 在发送请求前升级加密
- `HTTP_ENCRYPT_ALWAYS`: 一旦连接服务器即使用加密

# 临时文件

当 CUPS 配置加密时，应用程序需要临时文件。`TMPDIR` 环境变量决定了临时文件的位置，CUPS 使用 `/var/tmp`。如果 `TMPDIR` 变量设置，则使用 `/tmp`。

# 使用 CUPS 函数

CUPS 提供了几个函数来访问和设置当前文件名。

```c
char filename[124];
```

获取临时文件：

```c
if (cupsTempFile(filename, sizeof(filename)) == NULL)
    puts("无法创建临时文件!");
```

```c
fp = fopen(filename, "w");
```

如果临时文件已创建，`cupsTempFile()` 返回文件描述符。否则，它返回 -1。

# 加密支持

当 CUPS 支持加密时，它可以加密发送和接收的所有请求。CUPS 提供了查询和设置默认加密模式的函数。

```c
encryption_t encryption;
...
encryption = cupsEncryption();
```加密值是一个枚举，指定了何时执行加密：

- `HTTP_ENCRYPT_IF_REQUESTED`: 仅当服务器请求时
- `HTTP_ENCRYPT_NEVER`: 从不加密
- `HTTP_ENCRYPT_REQUIRED`: 在发送请求前升级加密
- `HTTP_ENCRYPT_ALWAYS`: 一旦连接服务器即使用加密

`HTTP_ENCRYPT_ALWAYS` 值用于使用 SSL 协议加密，而 `HTTP_ENCRYPT_REQUIRED` 和 `HTTP_ENCRYPT_IF_REQUESTED` 值使用 TLS 协议。默认设置是 `HTTP_ENCRYPT_IF_REQUESTED`，但可以通过 `CUPS_ENVIRONMENT` 环境变量以及 `client.conf` 或 `~/.clientre` 中的加密指令进行覆盖。

`cupsSetEncryption()` 函数设置加密模式。例如，要让本章之前的打印程序始终使用加密，只需在 `main()` 函数顶部添加以下行：

```c
cupsSetEncryption(HTTP_ENCRYPT_REQUIRED);
```

`lp` 和 `lpr` 程序在命令行指定 `-E` 时启用加密。

# 用户、服务器和端口

CUPS 提供了几个函数来访问和设置其他 API 函数使用的当前用户名、服务器和端口号。

# 获取和设置当前用户名

当前用户名通常是您的登录用户名。`cupsUser()` 函数返回当前用户名：

```c
const char *username;
...
username = cupsUser();
```

如所见，接口并不复杂。您将获得当前用户名，如果当前用户名未知，将获得字符串“unknown”。

使用 `cupsSetUser()` 函数更改当前用户名：

```c
cupsSetUser("johndoe");
```

再次，接口并不复杂，您唯一的义务是提供用户名字符串。

# 获取和设置当前服务器

当前服务器通常是“localhost”，但可以通过 `CUPS_SERVER` 环境变量或 `client.conf` 和 `~/.clientre` 文件进行更改。`cupsServer()` 函数返回当前服务器：

```c
const char *server;
...
server = cupsServer();
```

`cupsServer()` 函数永远不会返回空指针。
使用 `cupsSetServer()` 函数可以更改当前服务器：

```
cupsSetServer("foo.bar.com");
```

服务器名称字符串可以是主机名或 IP 地址。

# 获取和设置 IPP 端口

当前的 IPP 端口通常为 631，这是互联网打印协议（Internet Printing Protocol）的默认端口号。该端口可以通过 `IPP_PORT` 环境变量或通过在 `/etc/services` 文件中添加 "ipp" 条目来覆盖。`ippPort()` 函数返回当前的端口号：

```c
int port;
...
port = ippPort();
```

使用 `ippSetPort` 函数更改默认端口：

```c
ippSetPort(8631);
```

# 回调函数

CUPS 支持对任何请求进行验证，包括提交打印作业。获取用户名和密码的默认机制是使用登录用户和来自控制的密码。

为了支持其他类型的应用程序，特别是图形用户界面（GUI），CUPS API 提供了回调机制。

`cupsSetPasswordCB()` 函数用于在程序中设置密码回调。任何时间只能使用一个函数。回调函数接受一个参数（密码提示），并必须返回指向密码字符串的指针，如果操作员取消了操作则返回 NULL。

当与 `cupsUser()` 函数结合时，密码回调可以为验证提供用户名和密码：

```c
#include <cups/cups.h>
...
const char *    /* O - 密码 */
my_password_cb(const char *prompt) /* I - 密码提示 */
{
  char user[65];                    /* 用户名字符串 */
  /* 显示密码提示 */
  puts(prompt);
  /* 从用户获取用户名 */
  printf("Username: ");
  if (fgets(user, sizeof(user), stdin) == NULL)
    return (NULL);
  /* 去除字符串中的换行符并设置用户 */
  user[strlen(user) - 1] = '\0';
  cupsSetUser(user);
  /* 使用 getpass() 询问密码... */
  return (getpass("Password: "));
}
...
cupsSetPasswordCB(my_password_cb);
```

# 错误处理

如果任何 CUPS API 打印函数返回错误，可以通过调用 `cupsLastError()` 和 `ippErrorString()` 找到错误原因。`ippError` 函数返回遇到的最后一个 IPP 错误代码。`ippErrorString()` 将错误代码转换为适用于展示给用户的消息字符串：

```c
#include <cups/cups.h>
...
int jobid;
...
if (jobid == 0)
  printf("Unable to print file: %s\n", cupsErrorString(cupsLastError()));
```



## 总结

CUPS API 为应用程序提供了许多函数，用于查询目标；发送和管理打印作业；发现打印机选项和功能；以及控制加密、用户名、密码、服务器和端口设置。

应用程序可以获取打印机列表或真实及虚拟目标列表，以及每个目标可使用的选项。打印机选项可以单独管理，也可以与目标一起管理。打印机、类、实例、选项和选择名称不区分大小写。

可以通过 CUPS API 取消或监控作业。每个作业都有一个关联数字，用于在每个服务器上唯一地标识该作业。CUPS API 支持列出所有作业、打印机上的作业以及当前用户的作业。

PPD 文件描述了 CUPS 中的打印机。CUPS API 提供了通过 PPD 文件加载、查询和控制打印机的函数。PPD 文件包含一组选项，每个选项关联一个或多个选择。选项可以根据其他选项进行限制，以强制打印机中的某些策略或限制。

可以使用 CUPS API 管理临时文件。这很重要，因为许多系统上临时文件的创建方式不同，而 CUPS 确保以唯一名称安全地创建文件。

当前的加密模式、用户、服务器、端口和密码回调可以使用 CUPS API 中的几个简单函数进行控制。密码回调用于为替代用户名以及 GUI 应用程序提供支持。

在下一章中，你将深入内部，学习如何使用 IPP 请求直接与 CUPS 服务器交互。

# 第 15 章

# 使用 CUPS 发送 IPP 请求

本章涵盖了 CUPS IPP 接口，并描述了如何管理 IPP 属性、发送请求以及处理响应。

在第 14 章“使用 CUPS API 函数”中，你学习了如何使用 CUPS API 访问打印机和打印机信息、管理打印机选项以及管理打印作业。有了了这些功能，你可能会想，为什么还需要费心发送自己的 IPP 请求，甚至阅读这一章。

简单的答案是，你的应用程序可能完全不需要从程序发送 IPP 请求。毕竟，CUPS API 确实提供了应用程序支持基本打印所需的大部分功能。

尽管如此，理解这些函数如何在 IPP 层中实现是非常重要的。此外，如果你的应用程序的操作比基本打印更多（例如打印机类或作业管理），那么直接的 IPP 接口是实现这些唯一方法。

最后，这里介绍的许多接口可以用于打印之外领域。

# CUPS 低级 API

CUPS 低级 API 由一组超文本传输协议（HTTP）和互联网打印协议（IPP）函数组成，用于管理连接。这些接口每一个都基于一个管理请求和响应的状态机。图 15.1 显示了 HTTP 和 IPP 连接之间的关系。

图 15.1 HTTP 连接上的 IPP 数据流

要向服务器发送 IPP 请求，应用程序首先在 `ipp_t` 对象中构建请求。它打开到服务器的连接，该连接由 `http_t` 对象管理。然后通过 HTTP 操作将 IPP 请求发送到服务器，响应并存储在第二个 `ipp_t` 对象中。

# HTTP 函数

CUPS 提供了许多用于管理 HTTP 连接的函数。这些函数大部分处理 `http_t` 结构，该结构管理与服务器的 HTTP“对象”或连接。对于每个通信的服务器，必须创建一个新的 HTTP 对象。表 15.1 列出了 HTTP 函数。

表 15.1 CUPS HTTP 函数

| 名称 | 描述 |
| --- | --- |
| `httpBlocking()` | 在连接上设置阻塞或非阻塞操作 |
| `httpCheck()` | 检查是否有来自服务器的数据 |
| `httpClearFields()` | 清空 HTTP 字段值 |
| `httpClose()` | 断开服务器连接并删除 HTTP 对象 |
| `httpConnect()` | 创建 HTTP 对象并连接到指定的服务器 |
| `httpConnectEncrypt()` | 创建 HTTP 对象并使用指定的加密连接 |
| `httpDecode64()` | 将 Base64 编码转换为字符串 |
| `httpDelete()` | 向服务器发送 DELETE |
| `httpEncode64()` | 将字符串转换为 Base64 编码 |
| `httpEncryption()` | 设置连接的加密模式 |
| `httpError()` | 返回当前错误的文本 |
| `httpFlush()` | 清除服务器上任何剩余数据 |
| `httpGet()` | 向服务器发送 GET 请求 |
| `httpDateString()` | 从 Unix 时间值返回 HTTP 日期时间字符串 |
| `httpDateTime()` | 从 HTTP 日期时间字符串返回 Unix 时间值 |
| `httpField()` | 获取 HTTP 字段值 |
| `httpGetLength()` | 从服务器响应获取内容长度 |
| `httpGetSubField()` | 从字段中获取子字段值 |
| `httpHead()` | 向服务器发送 HEAD 请求 |
| `httpInitialize()` | 初始化 HTTP 模块 |
| `httpMD5()` | 计算用户名、域和密码的 MD5 和 |
| `httpMD5Final()` | 计算包含随机数、方法和请求 URI 的最终 MD5 和 |
| `httpMD5String()` | 将 MD5 和转换为字符串值 |

# 第三部分：使用 CUPS 编程

# 表 15.1 续

| 名称 | 描述 |
|---|---|
| `httpOptions()` | 向服务器发送 OPTIONS 请求 |
| `httpPost()` | 向服务器发送 POST 请求 |
| `httpPut()` | 向服务器发送 PUT 请求 |
| `httpRead()` | 从服务器读取数据 |
| `httpReconnect()` | 重新连接到服务器 |
| `httpHttpResponse()` | 将 URL 拆分为其各个组成部分 |
| `httpSetField()` | 设置 HTTP 字段值 |
| `httpStatus()` | 返回当前状态的字符串 |
| `httpTrace()` | 向服务器发送 TRACE 请求 |
| `httpUpdate()` | 根据来自服务器的数据更新连接的当前状态 |
| `httpWrite()` | 向服务器写入数据 |

## 创建 HTTP 对象

在执行任何 HTTP 之前之前，你必须先创建一个 HTTP 对象。CUPS 提供了两个函数来完成此操作。

第一个函数是 `httpConnect()`，它在不使用加密的情况下连接到 HTTP 服务器，如果连接成功，则返回一个新的 HTTP 对象；如果服务器没有响应，则返回 NULL：

```
http_t *http;

...

http = httpConnect("hostname", port);
```

`hostname` 参数是你想要连接的服务器名称；该名称也可以是点分符号表示法的 IP 地址，例如 `127.0.0.1`。`port` 参数是要使用的端口号；对于 IPP，端口号通常为 `631`。

第二个函数是 `httpConnectEncrypt()`，它使用指定的加密级别连接到 HTTP 服务器：

```
http_t *http;

...

http = httpConnectEncrypt("hostname", port, encryption);
```

`encryption` 参数是一个枚举，用于指定是初始使用加密，还是允许根据服务器请求进行升级。表 15.2 列出了所有可用值。

# 表 15.2 `httpConnectEncrypt()` 的加密枚举值

| 名称 | 描述 |
|---|---|
| `HTTP_ENCRYPT_IF_REQUESTED` | 如果服务器请求，则加密。 |
| `HTTP_ENCRYPT_NEVER` | 永远不加密，即使服务器请求也是。 |
| `HTTP_ENCRYPT_REQUIRED` | 在连接建立后使用 HTTP Upgrade 协议进行加密。 |
| `HTTP_ENCRYPT_ALWAYS` | 在连接建立后使用 SSL 协议进行加密。 |

你也可以在创建 HTTP 对象后，使用 `httpEncryption()` 函数设置加密模式：

```
http_t *http;

...

http = httpConnect("hostname", port);

...

httpEncryption(http, HTTP_ENCRYPT_REQUIRED);
```

> 注意：
> 如果你切换到 `HTTP_ENCRYPT_ALWAYS` 模式，HTTP 对象必须重新连接到服务器然后启动加密。因此，通常使用 `httpConnectEncrypt()` 更好，因为可以避免因“连接-断开-连接-加密”过程带来的额外启动时间。

# 销毁 HTTP 对象

在你使用 HTTP 对象执行所有需要的 HTTP 或 IPP 请求后，你可以使用 `httpClose()` 函数断开连接并销毁该对象：

```
http_t *http;

...

httpClose(http);
```

# 发送 HTTP 请求

在创建 HTTP 对象后，你可以使用 CUPS API 函数发送各种 HTTP 请求。CUPS 为每种标准 HTTP 请求方法都提供了七个函数。表 15.3 列出了 HTTP 方法和对应的 CUPS 函数。

# 表 15.3 对应每个 HTTP 方法的 CUPS 函数

| HTTP 方法 | CUPS 函数 |
|---|---|
| DELETE | `httpDelete()` |
| GET | `httpGet()` |
| HEAD | `httpHead()` |
| OPTIONS | `httpOptions()` |
| POST | `httpPost()` |
| PUT | `httpPut()` |
| TRACE | `httpTrace()` |

所有这些函数都接受一个 HTTP 对象指针和一个用于请求行的资源名称。例如，要获取服务器上的主页，你可以使用：

```
http_t *http;

...

httpGet(http, "/*");
```

发送到服务器的 HTTP 请求看起来如下：

```
GET / HTTP/1.1 CR LF

Host: hostname CR LF

CR LF
```

# 获取服务器响应

发送请求后，使用 `httpUpdate()` 函数更新当前状态，直到获取到 HTTP_CONTINUE 状态以外的任何：

```
http_t *http;

http_state_t status;

...

httpGet(http, "/*");

while ((status = httpUpdate(http)) != HTTP_CONTINUE)
```

`status` 变量是所有标准 HTTP 状态的枚举。在从服务器接收到最终请求状态之前，会返回状态码 100 `HTTP_CONTINUE`。

# 从服务器读取数据

从服务器接收状态码后，你可以使用 `httpRead()` 函数读取响应数据：

```
http_t *http;

int bytes;

char buffer[1024];
```

```
while ((bytes) = httpRead(http, buffer, sizeof(buffer) - 1) > 0)
{
  buffer[bytes] = '\0';
  fputs(buffer, stdout);
}
```

第一个参数是 HTTP 对象指针。随后依次是缓冲区数据指针和缓冲区的大小。
HTTP 对象会跟踪响应的内容长度或分块（chunking），并在读取完所有数据时返回 0。

# 设置 HTTP 请求字段

某些请求需要额外信息。例如，POST 需要 `Content-Type` 来告知服务器数据的格式。通常使用 `httpClearFields()` 来初始化字段：

```
http_t *http;

httpClearFields(http);
```

`httpSetField()` 函数设置发送到服务器的字段。参数是字段的枚举值。表 15.4 列出了支持的字段：

# 表 15.4 字段名称

| CUPS 名称 | HTTP 名称 |
|---|---|
| `HTTP_FIELD_ACCEPT` | Accept |
| `HTTP_FIELD_ACCEPT_RANGES` | Accept-Ranges |
| `HTTP_FIELD_AUTHORIZATION` | Authorization |
| `HTTP_FIELD_CONNECTION` | Connection |
| `HTTP_FIELD_ENCODING` | Content-Encoding |
| `HTTP_FIELD_LANGUAGE` | Content-Language |
| `HTTP_FIELD_LENGTH` | Content-Length |
| `HTTP_FIELD_LOCATION` | Content-Location |
| `HTTP_FIELD_MD5` | Content-MD5 |
| `HTTP_FIELD_RANGE` | Content-Range |
| `HTTP_FIELD_TYPE` | Content-Type |
| `HTTP_FIELD_VERSION` | Content-Version |
| `HTTP_FIELD_DATE` | Date |
| `HTTP_FIELD_HOST` | Host |
| `HTTP_FIELD_IF_MODIFIED_SINCE` | If-Modified-Since |
| `HTTP_FIELD_IF_UNMODIFIED_SINCE` | If-Unmodified-Since |
| `HTTP_FIELD_KEEP_ALIVE` | Keep-Alive |
| `HTTP_FIELD_LAST_MODIFIED` | Last-Modified |
| `HTTP_FIELD_LINK` | Link |
| `HTTP_FIELD_REFERER` | Referer |
| `HTTP_FIELD_RETRY_AFTER` | Retry-After |
| `HTTP_FIELD_TRANSFER_ENCODING` | Transfer-Encoding |
| `HTTP_FIELD_UPGRADE` | Upgrade |
| `HTTP_FIELD_USER_AGENT` | User-Agent |
| `HTTP_FIELD_WWW_AUTHENTATE` | WWW-Authenticate |

# 表 15.4 续

| CUPS 名称 | HTTP 名称 |
|---|---|
| `HTTP_FIELD_MD5` | Content-MD5 |
| `HTTP_FIELD_RANGE` | Content-Range |
| `HTTP_FIELD_TYPE` | Content-Type |
| `HTTP_FIELD_VERSION` | Content-Version |
| `HTTP_FIELD_DATE` | Date |
| `HTTP_FIELD_HOST` | Host |
| `HTTP_FIELD_IF_MODIFIED_SINCE` | If-Modified-Since |
| `HTTP_FIELD_IF_UNMODIFIED_SINCE` | If-Unmodified-Since |
| `HTTP_FIELD_KEEP_ALIVE` | Keep-Alive |

| `HTTP_FIELD_LAST_MODIFIED` | Last-Modified |
| `HTTP_FIELD_LINK` | Link |
| `HTTP_FIELD_REFERER` | Referer |
| `HTTP_FIELD_RETRY_AFTER` | Retry-After |
| `HTTP_FIELD_TRANSFER_ENCODING` | Transfer-Encoding |
| `HTTP_FIELD_UPGRADE` | Upgrade |
| `HTTP_FIELD_USER_AGENT` | User-Agent |
| `HTTP_FIELD_WWW_AUTHENTATE` | WWW-Authenticate |

# 获取 HTTP 请求字段

在你提交请求并从服务器接收响应后，HTTP 对象将包含字段。你可以使用 `httpGetField()` 获取这些字段。例如，WWW-Authenticate 字段可能包含子值：

```
WWW-Authenticate: Basic realm="Foobar"
```

要访问 "realm" 子字段，使用 `httpGetSubField()` 配合 `HTTP_WWW_AUTHENTATE` 和 "realm" 子字段名：

```
realm = httpGetSubField(http, WWW_Authenticate, "realm");
```

# 向服务器写入数据

发送 POST 或 PUT 请求后，你需要使用 `httpWrite()` 函数向服务器写入数据：

```
http_t *http;

...

httpPost(http, "resource");

httpWrite(http, buffer, length);
```

第一个参数是 HTTP 对象。HTTP 对象之后是数据缓冲区指针和数据的字节长度。

与 `order()` `send()` 函数不同，`httpWrite()` 会发送分段直到整个缓冲区写入服务器。如果你在发送请求之前将 `Transfer-Encoding` 字段设置为 "chunked"，则 `httpWrite()` 也会处理数据分块：

```
http_t *http;

...

httpSet(http, HTTP_FIELD_TRANSFER_ENCODING, "chunked");

httpPost(http, "resource");

httpWrite(http, buffer, 123);

httpWrite(http, buffer, 456);

httpWrite(http, buffer, 0);
```



此示例发送了两个分别为 123 和 456 字节的块，最后是一个 0 长度块。0 长度块指示服务器客户端已发送所有数据。

> 注意：
你必须设置 `Content-Length` (`HTTP_FIELD_CONTENT_LENGTH`) 或 `Transfer-Encoding` (`HTTP_FIELD_TRANSFER_ENCODING`) 字段来指示发送到服务器的数据量。`Content-Length` 字段包含总字节数。在发送请求之前已知道数据大小时使用该字段。

# 错误处理

`Transfer-Encoding` 字段可以设置为 "chunked"，以告诉服务器你将发送分块数据。在发送请求之前不知道数据的总大小时，请使用此字段。

在发送分块数据时，必须发送一个零长度的 `httpUpdate()`。在发送带有 `Content-Length` 的数据时，一个零长度的 `httpWrite()` 是可选的。

当发生错误时，你的程序将从 `httpUpdate` 获取 `HTTP_ERROR` 状态，或者从服务器获取一个错误。

使用 `httpError()` 函数来检查 `HTTP_ERROR` 状态报告的条件。错误编号是系统错误，因此你可以使用 `strerror()` 函数获取错误的文本消息：

```c
http_t *http;

http_status_t status;

while ((status = httpUpdate(http)) == HTTP_CONTINUE);

...

if (status == HTTP_ERROR)
{
    printf("发生以下系统错误：n\t%s\n",
    strerror(httpError(http)));
}
```

对于 HTTP 状态码，使用 `httpStatus()` 函数获取该状态的标准消息：

```c
http_t *http;

http_status_t status;

...

while ((status = httpUpdate(http)) == HTTP_CONTINUE);

...

if (status != HTTP_OK && status == HTTP_ERROR)
{
    printf("发生以下 HTTP 错误：n\t%s\n",
    httpStatus(status));
}
```

# 身份验证处理

当服务器返回 401 状态码（`HTTP_UNAUTHORIZED`）时，你的程序应该向用户询问用户名和密码，然后带有身份信息重新提交你的请求。

对于 Basic 认证，用户名和密码格式为“username:password-word”并进行 base-64 编码。你可以使用 `httpEncode64()` 函数为服务器生成必要的身份信息：

```c
http_t *http;

http_status_t status;

char username[33];

char *password;

char userpass[66];

char encoded[255];

...

nhttpGet(http, "/");

while ((status = httpUpdate(http)) == HTTP_CONTINUE) {
    if (status == HTTP_UNAUTHORIZED) {
        printf("Username: ");
        gets(username);
        password = getpass("Password: ");
        sprintf(userpass, "%s:%s", username, password);
        strncpy(encoded, "Basic ", 6);
        httpEncode64(encoded + 6, userpass);
    }
}

httpFlush(http);

ClearFields(http);

httpSetField(http, HTTP_FIELD_AUTHORIZATION, encoded);

httpGet(http, "/");

while ((status = httpUpdate(http)) == HTTP_CONTINUE) {
}
```

当你从 `httpUpdate()` 获取 `HTTP_UNAUTHORIZED` 状态时，你需要请求用户名和密码。当你获得用户名和密码后

对于 Digest 认证，密码不会以明文传递。相反，将用户名、密码、域（realm）和其他信息结合，并计算字符串的 MD5 和。然后将 MD5 和与其他支持字段一起发送给服务器。

`httpMD5()` 和 `httpMD5Final()` 函数用于大多数类型的 Digest 认证。要计算 MD5 和，你首先从 `WWW-Authenticate` 字段中获取“realm”和“nonce”子字段：

```c
http_t *http;

char nonce[256];

char realm[256];
```
...
httpGetSubField(http, HTTP_FIELD_WWW_AUTHENTICATE, "realm", realm);
httpGetSubField(http, HTTP_FIELD_WWW_AUTHENTICATE, "nonce", nonce);
```

接下来，调用 `httpMD5()` 函数来计算初始密码和：

```c
char username[33];
char *password;
char encoded[33];

httpMD5(cupsUser(username), realm, password, encoded);
```

然后使用 `httpMD5Final()` 函数将密码和与“nonce”值、请求方法和资源路径结合：

```c
char resource[HTTP_MAX_URI];
...
httpMD5Final(nonce, "POST", resource, encoded);
```

`encoded` 变量中生成的字符串是 MD5 响应字符串，它将传递给服务器。该身份验证字符串还需要用户名、“realm”和“nonce”值来验证身份：

```c
char authstring[256];

sprintf(authstring, sizeof(authstring),
  "Digest username=\"s\", realm=\"s\", nonce=\"s\", "
  "response=\"s\"", username, realm, nonce, encoded);
```

要同时处理 Basic 和 Digest 认证，只需使用 `strncmp` 检查 `WWW-Authenticate` 字段的第一个单词：

```c
if (strncmp(httpGetField(http, HTTP_FIELD_WWW_AUTHENTICATE),
  "Basic", 5) == 0)
{
  /* 执行 Basic 认证 */
}
else
{
  /* 执行 Digest 认证 */
}
...
```

# 升级加密

当服务器返回 426 状态码（`HTTP_UPGRADE_REQUIRED`）时，你的程序应该切换到加密通信。实现此最简单的方法是使用描述的 `httpEncryption(http)` 函数：

```c
http_t *http;
http_status_t status;
```

# 代理服务器处理

当服务器返回 426 状态码（`HTTP_UPGRADE_REQUIRED`）时，你的程序应该切换到加密通信。实现此最简单的方法是使用下述的 `httpEncryption(http)` 函数：

```c
http_t *http;
http_status_t status;
```

当服务器返回 426 状态码（`HTTP_UPGRADE_REQUIRED`）时，你的程序应该切换到加密通信。实现此最简单的方法是使用描述的 `httpEncryption(http)` 函数：

通常，如果你使用代理，则需要设置 `Host` 字段为代理的名称。这看起来如下：

```c
http_t *http;
http_status_t status;
...
httpSetField(http, HTTP_FIELD_HOST, "proxy.com");
```

`httpUpdate()` 函数处理服务器的任何消息。`httpEncryption()` 函数在后续章节中描述。这看起来如下：

```c
http_t *http;
http_status_t status;
...
httpFlush(http);
httpGet(http, 80);
```

# 其他实用函数

除了处理问题外，CUPS 提供了一些方便函数。第一个是 `httpSeparate()`，它分离 URL：

```c
http_t *http;
http_status_t status;
...
while ((status = httpUpdate(http)) == HTTP_CONTINUE);
```

新版本的 CUPS 增加了 `httpSeparate()`，它允许你指定字符串的大小。每个输出以空字符结尾：

```c
char url[HTTP_MAX_URI];
char scheme[HTTP_MAX_URI];
char userpass[HTTP_MAX_URI];
char server[HTTP_MAX_URI];
int port;

httpSeparateLen(url, sizeof(scheme), userpass, sizeof(userpass), server, sizeof(server), &port);
```

> 注意：`httpSeparate()` 函数已过，将在未来的版本中移除。

# 实现简单的浏览器

现在你已经熟悉了 HTTP 函数，你有足够的信息来实现简单的文本浏览器。你将首先通过 `httpSeparate()` 获取网页的主机、端口和资源：

```c
char scheme[HTTP_MAX_URI];
char userpass[HTTP_MAX_URI];
char server[HTTP_MAX_URI];
int port;
char resource[HTTP_MAX_URI];

httpSeparate(argv[1], scheme, userpass, server, &port);
```

接下来，使用 `httpConnectEncrypt()` 连接到服务器：

```c
http_t *http;

if ((http = httpConnectEncrypt(server, port, encryption)) == NULL)
```

然后使用 `HttpGet()` 向服务器发送 GET 请求：

```c
http_status_t status;
...
httpGet(http, resource);
while ((status = httpUpdate(http)) == HTTP_CONTINUE);
```

如果状态是 `HTTP_UNAUTHORIZED`，请请求用户名和密码。如果是 `HTTP_UPGRADE_REQUIRED`，则升级到 TLS 加密。

最后，从服务器读取响应并将其发送到标准输出：

```c
char buffer[1024];
int bytes;
...
while ((bytes = httpRead(http, buffer, sizeof(buffer)) - 1) > 0)
{
  buffer[bytes] = '\0';
  puts(buffer, stdout);
}
```

# 列表 15.1 browse.c 源文件

```
/* 包含 CUPS 头文件 */
#include <cups/cups.h>

/*
 * 'main' - 获取并显示 页面。
 */

int /* O 输出状态 */
main(int argc, /* I 命令行参数个数 */
     char *argv[]) /* I 命令行参数 *
{
    http_t *http;
    http_status_t status;
    char *scheme[HTTP_MAX_URI];
    char *userpass[HTTP_MAX_URI];
    char *server[HTTP_MAX_URI];
    int port;
    char *resource[HTTP_MAX_URI];
    http_encryption_t encryption;
    char *username[33];
    char *password;
    char *encoded[255];
    int bytes;
    char *buffer[1024];

/* 检查命令行。 */
if (argc != 2)
{
    puts("Usage: browse <URL>");
    return (1);
}

/* 将 URL 拆分为它的各个组件。 */
httpSeparate(argv[1], scheme, userpass, server, &port, resource);
```

```c
/* Determine我们是否需要使用 SSL。 */
if (strcmp(scheme, "https") == 0)
  encryption = HTTP_ENCRYPT_ALWAYS;
else
  encryption = HTTP_ENCRYPT_IF_REQUESTED;
```

```c
/* 连接到服务器。 */
if ((http = httpConnectEncrypt(server, port, encryption)) == NULL)
{
  perror(server);
  return (1);
}
```

```c
/* 编码 userpass 字符串。 */
if (userpass[0])
{
  strcpy(encoded, "Basic ");
  httpEncode64(encoded + 6, userpass);
}
else
  encoded[0] = '\0';
```

```c
/*发送 GET 请求，必要时重试... */
do
{
  /* 设置 HTTP 字段并发送请求。 */
  httpClearFields(http);
  httpSetField(http, HTTP_FIELD_AUTHORIZATION, encoded);
  httpGet(http, resource);
```

```c
/* 等待服务器的响应。 */
while ((status = httpUpdate(http)) == HTTP_CONTINUE)
```

```c
/* 根据需要进行身份验证或加密。 */
if (status == HTTP_UNAUTHORIZED)
{
  /* 获取用户名和密码。 */
  printf("Username: ");

break;

/* 编码用户名和密码 */
  sprintf("%s:%s", username, password);
  strncpy(encoded, "Basic ");
  httpEncode64(encoded + 6, userpass);

  /* 刷新错误消息。 */
  httpflush(http);
} else if (status == HTTP_UPGRADE_REQUIRED)
{
    /* 刷新错误消息。 */
    httpFlush(http);

    /* 升级到加密 */
    httpEncryption(http, HTTP_ENCRYPT_REQUIRED);
}
while (status == HTTP_UPGRADE_REQUIRED ||
       status == HTTP_UNAUTHORIZED);

/* 现在显示系统错误或来自服务器的数据。 */
if (status == HTTP_ERROR)
{
    printf("A system error occurred:\n\t%s\n",
           strerror(httpError(http)));
}
else
{
    while ((bytes = httpRead(http, buffer, sizeof(buffer) - 1)) > 0)
    {
        buffer[bytes] = '\0';
        fputs(buffer, stdout);
    }
}

/* 关闭服务器连接并删除 HTTP 对象。 */
httpClose(http);

/* 无错误返回 */
return (0);
}
```

# IPP 函数

CUPS IPP 接口比 HTTP 接口更简单。CUPS IPP 接口不需要处理许多状态或特殊的协议问题，例如身份验证。

# IPP 对象结构

每个 IPP 请求或响应都由 `ipp_t` "对象" 结构表示，该结构包含 `ipp_state` 头部和属性的链表。表 15.5 显示了 `ipp_t` 结构的成员。

## 表 15.5 ipp_t 结构

| 名称 | 类型 | 描述 |

|---|---|---|

| state | ipp_state_t | IPP 对象的当前状态 |

| request | ipp_request_t | IPP 请求或响应头部 |

| attrs | ipp_attribute_t * | 对象中的第一个属性 |

| last | ipp_attribute_t * | 对象中的最后一个属性 |

| current | ipp_attribute_t * | 对象中的当前属性 |

| curtag | ipp_tag_t | 当前的组标签 |

# IPP 对象状态

`state` 成员提供了对象的当前状态，用于读取和写入对象。表 15.6 列出了这些状态。

## 表 15.6 IPP 对象状态

| 名称 | 描述 |

|---|---|



| `IPP_ERROR` | 发生了错误。 |
| `IPP_IDLE` | 无正在进行的操作或请求已完成。 |
| `IPP_HEADER` | 需要发送或接收请求头部。 |
| `IPP_ATTRIBUTE` | 需要发送或接收一个或多个属性。 |
| `IPP_DATA` | 所有属性均已发送或接收。IPP 请求数据流。通常，应用程序会查找数据。 |

# IPP 请求与响应

每个 IPP 请求或响应都以 1 字节头部开始。表 15.7 显示了请求。

## 表 15.7 IPP 请求头部

| 名称 | 类型 | 描述 |
|---|---|---|
| `any.version` | `ipp_uchar_t` | 版本 |
| `any.request_id` | `int` | 请求 ID |
| `any.operation` | `ipp_operation_t` | 操作 |
| `any.status` | `ipp_status_t` | 状态 |

`any` 成员包含版本号。`any.operation` 的值取决于请求或响应。表 15.8 列出了定义的操作。

## 表 15.8 CUPS 操作映射到 IPP 操作

| CUPS 名称 | IPP 名称 |
|---|---|
| `GET_JOB` | `GET_JOB` |
| `GET_URL` | `GET_URL` |
| `VALIDATE_JOB` | `VALIDATE_JOB` |
| `CREATE_JOB` | `CREATE_JOB` |
| `SEND_DOCUMENT` | `SEND_DOCUMENT` |
| `SEND_URI` | `SEND_URI` |
| `CANCEL_JOB` | `CANCEL_JOB` |
| `GET_ATTRIBUTES` | `GET_ATTRIBUTES` |
| `GET_JOBS` | `GET_JOBS` |
| `GET_PRINTER_ATTRIBUTES` | `GET_PRINTER_ATTRIBUTES` |
| `HOLD_JOB` | `HOLD_JOB` |
| `RELEASE_JOB` | `RELEASE_JOB` |
| `RESTART_JOB` | `RESTART_JOB` |
| `PAUSE_PRINTER` | `PAUSE_PRINTER` |
| `RESUME_PRINTER` | `RESUME_PRINTER` |
| `PURGE_JOBS` | `PURGE_JOBS` |
| `SET_PRINTER_ATTRIBUTES` | `SET_PRINTER_ATTRIBUTES` |
| `SET_JOB_ATTRIBUTES` | `SET_JOB_ATTRIBUTES` |

## 表 15.8 续

| CUPS 名称 | IPP 名称 |
|---|---|
| `GET_PRINTER_SUPPORTED` | `GET_PRINTER_SUPPORTED` |
| `CREATE_PRINTER_SUBSCRIPTION` | `CREATE_PRINTER_SUBSCRIPTION` |
| `CREATE_JOB_SUBSCRIPTION` | `CREATE_JOB_SUBSCRIPTION` |
| `GET_SUBSCRIPTION_ATTRIBUTES` | `GET_SUBSCRIPTION_ATTRIBUTES` |
| `GET_SUBSCRIPTIONS` | `GET_SUBSCRIPTIONS` |
| `RENEW_SUBSCRIPTION` | `RENEW_SUBSCRIPTION` |
| `CANCEL_NOTIFICATIONS` | `CANCEL_NOTIFICATIONS` |
| `GET_NOTIFICATIONS` | `GET_NOTIFICATIONS` |
| `SEND_NOTIFICATIONS` | `SEND_NOTIFICATIONS` |
| `GET_PRINTER_SUPPORT_FILES` | `GET_PRINTER_SUPPORT_FILES` |
| `ENABLE_PRINTER` | `ENABLE_PRINTER` |
| `DISABLE_PRINTER` | `DISABLE_PRINTER` |
| `PAUSE_PRINTER_AFTER_CURRENT_JOB` | `PAUSE_PRINTER_AFTER_CURRENT_JOB` |
| `HOLD_NEW_JOBS` | `HOLD_NEW_JOBS` |
| `RELEASE_HELD_JOBS` | `RELEASE_HELD_JOBS` |
| `DEACTIVATE_PRINTER` | `DEACTIVATE_PRINTER` |
| `ACTIVATE_PRINTER` | `ACTIVATE_PRINTER` |
| `RESTART_PRINTER` | `RESTART_PRINTER` |
| `SHUTDOWN_PRINTER` | `SHUTDOWN_PRINTER` |
| `STARTUP_PRINTER` | `STARTUP_PRINTER` |
| `REPROCESS_JOB` | `REPROCESS_JOB` |
| `CANCEL_CURRENT_JOB` | `CANCEL_CURRENT_JOB` |
| `SUSPEND_CURRENT_JOB` | `SUSPEND_CURRENT_JOB` |
| `RESUME_JOB` | `RESUME_JOB` |
| `PROMOTE_JOB` | `PROMOTE_JOB` |
| `SCHEDULE_JOB_AFTER` | `SCHEDULE_JOB_AFTER` |

## 表 15.9 续

| CUPS 名称 | IPP 名称 |
|---|---|
| `IPP_DOCUMENT_ACCESS_ERROR` | `client-error-document-access-error` |
| `IPP_ATTRIBUTES_NOT_SETTABLE` | `client-error-attributes-not-settable` |
| `IPP_IGNORED_ALL_SUBSCRIPTIONS` | `client-error-ignored-all-subscriptions` |
| `IPP_TOO_MANY_SUBSCRIPTIONS` | `client-error-too-many-subscriptions` |
| `IPP_IGNORED_ALL_NOTIFICATIONS` | `client-error-ignored-all-notifications` |
| `IPP_PRINT_SUPPORT_FILE_NOT_FOUND` | `client-error-print-support-file-not-found` |
| `IPP_INTERNAL_ERROR` | `server-error-internal-error` |
| `IPP_OPERATION_NOT_SUPPORTED` | `server-error-operation-not-supported` |
| `IPP_SERVICE_UNAVAILABLE` | `server-error-service-unavailable` |
| `IPP_VERSION_NOT_SUPPORTED` | `server-error-version-not-supported` |
| `IPP_DEVICE_ERROR` | `server-error-device-error` |
| `IPP_TEMPORARY_ERROR` | `server-error-temporary-error` |
| `IPP_NOT_ACCEPTING` | `server-error-not-accepting-jobs` |
| `IPP_PRINTER_BUSY` | `server-error-busy` |
| `IPP_ERROR_JOB_CANCELLED` | `server-error-job-cancelled` |
| `IPP_MULTIPLE_JOBS_NOT_SUPPORTED` | `server-error-multiple-document-jobs-not-supported` |
| `IPP_PRINTER_IS_DEACTIVATED` | `server-error-printer-is-deactivated` |

`any_request_id` 字段是客户端请求的 ID 数字，随服务器的响应一同返回。

## 属性数据

`attrs`、`last` 和 `current` 成员指向 IPP 对象中的属性。`attrs` 成员指向属性列表中的第一个元素，可以作为搜索的起点。它通常用于收集一组属性，例如在显示作业列表时。

`last` 成员指向属性列表中的最后一个元素，供 "`add`" 函数在向 IPP 对象添加属性时使用。大多数程序不应触碰这块内存。

`current` 成员指定对象中的当前属性。它在使用 `ippWrite()` 写入属性或使用 `ippFindAttribute()` 和 `ippFindNextAttribute()` 查找属性时使用。

每个属性都存储在 `ipp_attribute_t` 结构中，由属性的值和组标签、属性名称、值的数量以及值数组组成。表 15.10 显示了 `ipp_attribute_t` 结构体的成员。

### 表 15.10 IPP 属性结构

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| `group_tag` | `ipp_tag_t` | 属性的组标签 |
| `value_tag` | `ipp_tag_t` | 属性的值 |
| `name` | `char *` | 属性的名称 |
| `num_values` | `int` | 属性中值的数量 |
| `values` | `ipp_tag_t []` | 属性中的值 |

`group_tag` 成员是一个表示 IPP 组标签的枚举。表 15.11 列出了有效值。

### 表 15.11 IP 组标签及其 CUPS 枚举名称

| CUPS 名称 | IPP 名称 |
| --- | --- |
| `IP_TAG_OPERATION` | `operation-attributes-tag` |
| `IP_TAG_JOB` | `job-attributes-tag` |
| `IP_TAG_END` | `end-of-attributes-tag` |
| `IP_TAG_PRINTER` | `printer-attributes-tag` |
| `IP_TAG_UNSUPPORTED_GROUP` | `unsupported-attributes-tag` |
| `IP_TAG_SUBSCRIPTION` | `subscription-attributes-tag` |
| `IP_TAG_EVENT_NOTIFICATION` | `event-notification-attributes-tag` |

`value_tag` 成员是一个表示 IPP 值标签的枚举。表 15.12 列出了有效值。

### 表 15.12 IP 值标签及其 CUPS 枚举名称

| CUPS 名称 | IPP 名称 |
| --- | --- |
| `IP_TAG_UNSUPPORTED_VALUE` | `unsupported` |
| `IP_TAG_DEFAULT` | `default` |
| `IP_TAG_UNKNOWN` | `unknown` |
| `IP_TAG_NOVALUE` | `no-value` |
| `IP_TAG_NOTSETTABLE` | `not-settable` |
| `IP_TAG_DELEATATTR` | `delete-attribute` |
| `IP_TAG_ADMINDEFINE` | `admin-define` |
| `IP_TAG_INTEGER` | `integer` |
| `IP_TAG_BOOLEAN` | `boolean` |
| `IP_TAG_ENUM` | `enum` |
| `IP_TAG_STRING` | `octetString` |

## 表 15.12 续

| CUPS 名称 | IPP 名称 |
|---|---|
| `IPP_TAG_DATE` | `dateTime` |
| `IPP_TAG_RESOLUTION` | `resolution` |
| `IPP_TAG_RANGE` | `rangeOfInteger` |
| `IPP_TAG_BEGIN_COLLECTION` | `begCollection` |
| `IPP_TAG_TEXTLANG` | `textWithLanguage` |
| `IPP_TAG_NAMELANG` | `nameWithLanguage` |
| `IPP_TAG_END_COLLECTION` | `endCollection` |
| `IPP_TAG_TEXT` | `textWithoutLanguage` |
| `IPP_TAG_NAME` | `nameWithoutLanguage` |
| `IPP_TAG_KEYWORD` | `keyword` |
| `IPP_TAG_URI` | `uri` |
| `IPP_TAG_CHARSET` | `charset` |
| `IPP_TAG_LANGUAGE` | `language` |
| `IPP_TAG_MIMYPE` | `mimeType` |
| `IPP_TAG_MEMBER` | `member` |

每个值存储在 `ipp_value_t` 中。

### 表 15.13 IPP 值成员

| 名称 | 类型 | 描述 |
|---|---|
| `integer` | `int` | 整数值 |
| `boolean` | `char` | 布尔值 |
| `date` | `ipp_t` | 日期值 |
| `resolution` | `int` | 分辨率值 |
| `range` | `int` | 整数范围 |
| `lower` | `int` | 范围下限 |
| `upper` | `int` | 范围上限 |
| `string` | `char *` | 字符串值 |
| `language` | `char *` | 带语言的字符串 |
| `collection` | `ipp_t` | 集合值 |
| `charset` | `char *` | 字符集值 |
| `uri` | `ipp_t` | URI 值 |
| `type` | `ipp_t` | MIME 类型值 |
| `member` | `ipp_t` | 成员值 |

值是 `ipp_value_t` 类型的。

## 创建 IPP 对象

使用 `ippNew()` 函数创建一个 IPP 对象：

```c
ipp_t *ipp = ippNew();
```

返回一个指向 `ipp_t` 的指针。

## 删除 IPP 对象

当你完成 IPP 对象的操作后，使用 `ippDelete()` 函数销毁它：

```c
ippDelete(ipp);
```

该函数不返回任何值。

## 向 IPP 对象添加值

CUPS 提供了多种向 IPP 对象添加属性的函数。表 15.14 列出了这些函数。

| 名称 | 描述 |
| --- | --- |
| `ippAddBoolean` | 添加单个布尔值 |
| `ippAddBooleans` | 添加多个布尔值 |
| `ippAddCollection` | 添加单个集合值 |
| `ippAddCollections` | 添加多个集合值 |
| `ippAddDate` | 添加单个日期值 |
| `ippAddInteger` | 添加单个整数或枚举值 |
| `ippAddIntegers` | 添加多个整数或枚举值 |
| `ippAddRange` | 添加单个范围值 |
| `ippAddRanges` | 添加多个范围值 |
| `ippAddResolution` | 添加单个分辨率值 |
| `ippAddResolutions` | 添加多个分辨率值 |
| `ippAddString` | 添加单个字符串值 |
| `ippAddStrings` | 添加多个字符串值 |

### 表 15.14 添加 IPP 属性的 CUPS 函数

`ippAddBoolean()` 添加单个布尔值到 IPP 对象：

```c
ippAddBoolean(ipp, group, "name", value);
```

第一个参数是 IPP 对象指针。`group` 是组标签枚举。`name` 是属性名称。`value` 是布尔值（0 为 false，1 为 true）。

`ippAddBooleans()` 添加多个布尔值到 IPP 对象：

```c
ippAddBooleans(ipp, group, "name", num_values, values);
```

`num_values` 参数指定集合中值的数量，而 `values` 参数是值数组的指针。

`ippAddCollection()` 添加单个集合值到 IPP 对象：

```c
ippAddCollection(ipp, group, "name", ipp_value);
```

第一个参数是 IPP 对象。`group` 是组标签枚举。`name` 是属性名称。`ipp_value` 是集合值。

`ippAddCollections()` 添加多个集合值到 IPP 对象：

```c
ippAddCollections(ipp, group, "name", num_values, values);
```

第一个参数是 IPP 对象。`group` 是组标签枚举。`name` 是属性名称。`values` 是集合值数组。

`ippAddDate()` 添加单个日期值到 IPP 对象：

```c
ippAddDate(ipp, group, "name", value);
```

第一个参数是 IPP 对象。`group` 是组标签枚举。`name` 是属性名称。`value` 是日期值。

`ippAddInteger()` 添加单个整数或枚举值到 IPP 对象：

```c
ippAddInteger(ipp, group, "name", value);
```

第一个参数是 IPP 对象。`group` 是组标签枚举。`name` 是属性名称。`value` 是整数或枚举值。

`ippAddIntegers()` 添加多个整数或枚举值到 IPP 对象：

```c
ippAddIntegers(ipp, group, "name", num_values, values);
```



第一个参数是 `IPP` 对象。`group` 是组标签枚举。`name` 是属性名称。`num_values` 是整数或枚举值的数量，`values` 是这些值的数组。

`ippAddRange()` 添加单个范围值到 `IPP` 对象：

```c
ippAddRange(ipp, group, "name", value);
```

第一个参数是 `IPP` 对象。`group` 是组标签枚举。`name` 是属性名称。`value` 是范围值。

`ippAddRanges()` 添加多个范围值到 `IPP` 对象：

```c
ippAddRanges(ipp, group, "name", num_values, values);
```

第一个参数是 `IPP` 对象。`group` 是组标签枚举。`name` 是属性名称。`num_values` 是范围值的数量，`values` 是这些数组。

`ippAddResolution()` 添加单个分辨率值到 `IPP` 对象：

```c
ippAddResolution(ipp, group, "name", value);
```

第一个参数是 `IPP` 对象。`group` 是组标签枚举。`name` 是属性名称。`value` 是分辨率值。

`ippAddResolutions()` 添加多个分辨率值到 `IPP` 对象：

```c
ippAddResolutions(ipp, group, "name", num_values, values);
```

第一个参数是 `IPP` 对象。`group` 是组标签枚举。`name` 是属性名称。`num_values` 是分辨率值的数量，`values` 是这些数组。

`ippAddString()` 添加单个字符串值到 `IPP` 对象：

```c
ippAddString(ipp, group, "name", charset, value);
```

第一个参数是 `IPP` 对象。`group` 是组标签枚举。`name` 是属性名称。`charset` 是字符集参数。`value` 是字符串值。

`ippAddStrings()` 添加多个字符串值到 `IPP` 对象：

```c
ippAddStrings(ipp, group, "name", num_values, charset, values);
```

第一个参数是 `IPP` 对象。`group` 是组标签枚举。`name` 是属性名称。`num_values` 是字符串的数量。`charset` 是字符集。`values` 是字符串值数组。

## 第三部分 使用 CUPS 编程

注意：

`CUPS` 目前要求所有 `textWithLanguage` 和 `nameWithLanguage` 值使用相同的字符集。这防止了这些值出现具有不同编码的 `issetOf` 数组；在实践中，这并不是问题。

使用 `ippAddResolution()` 和 `ippAddResolutions()` 函数添加分辨率值：

```
ipp_t *ipp;
int xres[10];
int yres[10];
...
```

```
ippAddResolution(ipp, group, "name", units, xres, yres);
ippAddResolutions(ipp, group, "name", num_values, units, xres, yres);
```

`units` 参数指定所有分辨率的测量单位，可以是 `IPP_RES_PER_INCH` 或 `IPP_RES_PER_CM` 枚举值。`xres` 和 `yres` 参数指定水平和垂直分辨率。`xres` 和 `yres` 参数指定用于多个分辨率的数组。

注意：

`CUPS` 目前要求所有分辨率值使用相同的单位。这防止了这些值出现具有不同单位的 `issetOf` 数组；在实践中，这并不是问题。

使用 `ippAddRange()` 和 `ippAddRanges()` 函数添加范围值：

```
ipp_t *ipp;
int lowers[10];
int uppers[10];
...
```

```
ippAddRange(ipp, group, "name", lower, upper);
ippAddResolutions(ipp, group, "name", num_values, lower, uppers);
```

`lower` 和 `upper` 参数指定范围的下限和上限。同样，`lowers` 和 `uppers` 参数指定用于多个范围的数组。

集合值存储在 `IPP` 子对象中，并使用 `ippAddCollection()` 和 `ippAddCollections()` 函数添加：

```
ipp_t *ipp;
ipp_t *value;
ipp_t *values[10];
...
```

```
ippAddCollection(ipp, group, "name", value);
ippAddCollections(ipp, group, "name", num_values, values);
```

`value` 和 `values` 参数是指向 `IPP` 对象或 `IPP` 对象数组的指针，其中包含每个集合中的属性。与普通 `IPP` 对象不同，集合对象不使用 `group_tag` 字段；在向集合的 `IPP` 对象添加属性时所指定的 `group` 将被忽略。集合还可以包含子集合。

> 注意：

`IPP` 集合的最大长度为 32767 字节。如果你尝试添加一个长度超过 32767 字节的 `IPP` 对象集合，则该集合不会被添加。

你可以通过调用 `ippCollectionLength()` 函数来确定 `IPP` 对象的大小。

## 确定 IPP 对象的大小

可以使用 `ippLength()` 函数计算 `IPP` 对象的传输大小：

```
ipp_t *ipp;
int length;
...
length = ippLength(ipp);
```

返回值是以字节为单位的长度。它包含了 `IPP` 头部以及要包含在输出流中的任何组标记。

集合值由 `IPP` 对象组成。与普通 `IPP` 对象不同，子对象缺少 `IPP` 头部和组标记；因此，集合 `IPP` 对象总是比普通 `IPP` 对象小。由于大小差异不是固定的，因此提供了 `ippCollectionLength()` 函数来计算集合中 `IPP` 对象的长度。

```
ipp_t *ipp;
int length;
...
length = ippCollectionLength(ipp);

if (length > 32767)
puts("Collection value too large!");
```

返回值是以字节为单位的长度。如前所述，集合值不能超过 32767 字节。

## 在 IPP 对象中查找属性

在向 `IPP` 对象添加属性后，你可以使用 `ippFindAttribute()` 函数查找它们：

```
ipp_t *ipp;
ipp_attribute_t *attr;
...
attr = ippFindAttribute(ipp, "name", value_tag);
```

`name` 是属性的名称。`value_tag` 参数指定属性所需的类型。特殊值 `IPP_TAG_ZERO` 可用于查找任何类型的已指定的属性。

如果找不到属性，则返回 `NULL` 指针。

注意：

`IPP` 规范要求客户端和服务器支持将 `textWithLanguage` 和 `nameWithLanguage` 与 `textWithoutLanguage` 和 `nameWithout` 互换使用。为了在 `CUPS` 中实现这一点，`IPP_TAG_TEXT` 和 `IPP_TAG_NAME` 枚举将与带有“WithLanguage”的 `IPP_TAG_TEXTTLANG` 和 `IPP_TAG_NAMELANG` 进行匹配。

客户端只需要查看值的 `string.charset` 成员即可判断属性是“WithLanguage”值还是“WithoutLanguage”值。

`ippFindAttribute()` 函数在 `IPP` 对象中查找属性的首次出现；然而，许多 `IPP` 请求会返回多组属性，每组都有同名属性的副本。提供了 `ippFindNextAttribute()` 函数来更方便地处理这种情况：

```
ipp_t *ipp;
ipp_attribute_t *attr;
for (attr = ippFindAttribute(ipp, "printer-name", IPP_TAG_NAME); attr != NULL; attr = ippFindNextAttribute(ipp, "printer-name", IPP_TAG_NAME))
puts(attr->values[0].string.text);
```

## 发送 IPP 请求

构建好 `IPP` 对象后，使用 `ippWrite()` 函数将请求发送到服务器：

```
ipp_t *ipp;
ipp_t *request;
http_t *http;
http_status_t status;
...
httpSetField(http, TRANSFER_ENCODING, "chunked");
httpPost(http, "resource");
```

`ippWrite()` 函数接受发送到服务器的 `IPP` 对象指针。返回值为 `IPP` 状态。对于前面的示例，使用：

```
FILE *fp;
char buffer[1024];
int bytes;

while ((state = ippWrite(http, request)) != IPP_ERROR
if (state == IPP_DATA)
{
    while ((bytes =buffer(,))))  
httpWrite(http, buffer, 0);
break;
}
```

> 注意：

如果你正在发送分块数据，请确保如示例代码所示通过 `ippWrite()` 发送最后的长度块。

如果你不发送长度块或使用 `Content-Length` 字段，服务器将不知道你已完成发送，请求将无法成功。

## 读取 IPP 响应

在向服务器 `POST` `IPP` 请求后，可以使用 `ippRead()` 函数读取响应：

```
ipp_t *response;
http_t *http;
http_status_t status;
...
while ((status = httpUpdate(http)) == HTTP_CONTINUE);

if (status == HTTP_OK)
{
    response = ippNew();
    while ((state = ippRead(http, response)) != IPP_ERROR)
    {
        if (state == IPP_DATA)
        {
            httpFlush(http);
            break;
        }
    }
}
```

与 `ippWrite` 函数类似，`ippRead` 接受 `HTTP` 对象指针和接收服务器响应数据的 `IPP` 对象指针。返回值为 `IPP` 状态，通常为 `IPP_ERROR` 或 `IPP_DATA`。

在进入 `IPP` `DATA` 状态后，刷新或读取剩余数据。这将确保从服务器读取了所有数据，包括最后的 0 长度块。在示例代码中，使用 `httpFlush()` 函数完成此。

## 自动化 IPP 请求

`CUPS` `API` 提供了名为 `cupsDoRequest()` 和 `cupsDoFileRequest()` 的函数，它们自动处理 `IPP` 请求发送和响应收集的过程：

```
ipp_t *request;
ipp_t *response;
http_t *http;

response = cupsDoRequest(http, request, "resource");

response = cupsDoFileRequest(http, request, "resource", "filename");
```

这两个函数都接受一个 `HTTP` 对象指针、一个 `IPP` 请求对象指针以及用于 `POST` 请求的资源字符串。在请求成功发送后，这两个函数都会销毁 `IPP` 请求对象。

# 使用 CUPS 发送 IPP 请求 第15章

`cupsDoFileRequest()` 还接受一个文件名字符串，用于指定在发送 `IPP` 数据之后向服务器发送的文件。

这两个函数都返回一个指向包含服务器响应的 `IPP` 对象的指针。如果发生错误，则返回 `NULL`，并且可以通过调用 `cupsLastError()` 函数找到 `IPP` 错误代码。

与自己编写代码相比，使用这些函数的一个优点是可以避免许多常见的错误，例如遗漏对 0 长度块的处理代码。这些函数还支持使用第 14 章中描述的密码回调机制进行身份验证。这允许您的应用程序充分利用所有的身份验证、加密和错误检查方法，而无需重复代码。

# 构建真实的 IPP 请求

现在你已经了解了基础知识，你将编写一个新程序，发送一个 `CUPS-Get-Printers` 请求以列出服务器上所有用的打印机。首先，创建 `ipp` 请求对象：

```
ipp_t *request;
...
request = ippNew();
```

接下来，为请求添加所需的属性；对于 `CUPS-Get-Printers`，你必须发送 `attributes-charset` 和 `attributes-natural-language` 属性：

```
ippAddString(request, IPP_TAG_OPERATION, IPP_TAG_CHARSET,
    "attributes-charset", NULL, "utf-8");
ippAddString(request, IPP_TAG_OPERATION, IPP_TAG_LANGUAGE,
    "attributes-natural-language", NULL, "en");
```

通过将 `request.op.operation_id` 和 `request.any.request_id` 设置为 `CUPS_GET_PRINTERS` 和 1 来初始化 `IPP` 头部：

```
request->op.operation_id = CUPS_GET_PRINTERS;
request->any.request_id = 1;
```

最后，使用 `cupsDoRequest()` 发送请求：

```
ipp_t *response;
http_t *http;

response = cupsDoRequest(http
```

获取响应后，你可以使用 `ippFindAttribute()` 和 `ippFindNextAttribute()` 显示打印机的名称：

```
ipp_attribute_t *attr;
...
```

# 第三部分：使用 CUPS 进行编程

```
for (attr = ippFindAttribute(ipp, "printer-name", IPP_TAG_NAME);
attr != NULL;
attr = ippFindNextAttribute(ipp, "printer-name", IPP_TAG_NAME))
puts(attr->values[0].string());
```

完成的程序如列表 15.2 所示。编译程序后运行，你会看到以下内容：

```
./showprinters ENTER
DeskJet
LaserJet
StylusColor
StylusPhoto
```

# 列表 15.2 showprinters.c 源文件

```c
/* 包含 CUPS 头文件。 */
#include <cups/cups.h>

int       /* O - 退出状态 */
main(void)
{
    http_t          /* HTTP 对象 */
    ipp_t        *request;      /* IPP 请求对象 */
    ipp_t        *response;     /* IPP 响应对象 */
    ipp_attribute_t *attr;      /* 当前 IPP 属性 */
```

```c
/* 连接到 HTTP 服务器 */
http = httpConnectEncrypt(cupsServer, ippPort, cupsEncryption());
```

```c
if (http == NULL)
{
    error("无法连接到服务器");
    return (1);
}
```

```c
/* 组装 IPP 请求 */
request = ippNew();

ippAddString(request, IPP_TAG_OPERATION, IPP_TAG_CHARSET,
             "attributes-charset", NULL, "utf-8");
```

# 列表 15.2 继续

```c
ippAddString(request, IPP_TAG_OPERATION, IPP_TAG_LANGUAGE,
    "attributes-natural-language", NULL, "en");
```

```c
request->request.op_operation_id = CUPS_GET_PRINTERs;
request->request.any.request_id = 1;
```

```c
/* 发送请求并获取响应。 */
response = cupsDoRequest(http, request, "/");
```



```c
if (response != NULL) {
    for (attr = ippFindAttribute(response, "printer-name", IPP_TAG_NAME);
         attr != NULL) {
        attr = ippFindNextAttribute(response, "printer-name", IPP_TAG_NAME))
        puts(attr->values[0].string.text);
    }
    ippDelete(response);
} else {
    printf("无法获取打印机列表: %s\n",
           ippErrorString(cupsLastError(0)));
}
```

```c
/* 关闭与服务器的连接。 */
httpClose(http);
return (0);
```

# 优化你的请求

许多 IPP 操作都支持 `requested-attributes` 属性，该属性列出了客户端感兴趣的属性。IPP 服务器随后可以从响应中消除这些属性。这种消除可以提供更快、更及时的响应，并减轻服务器、客户端和网络的负载。

例如，通过 `requested-attributes` 可以使 `showprinter` 示例变得高效得多：

```
ippAddString(request, IPP_TAG_OPERATION, IPP_TAG_KEYWORD,
    "requested-attributes", NULL, "printer-name");
```

IPP 服务器随后将尝试限制响应，仅包含名为 `"printer-name"` 的属性。

> 注意：IPP 规范允许使用 `requested-attributes` 属性来限制响应。这种消除可以提供更快、更及时的响应，并减轻服务器，客户端和网络的负载。

## 总结

许多 IPP 操作都支持 `requested-attributes` 属性，该属性列出了客户端感兴趣的属性。IPP 服务器随后可以从响应中消除这些属性。这种消除可以提供更快、更及时的响应，并减轻服务器、客户端和网络的负载。

CUPS 提供了丰富的函数来管理 HTTP 响应。IPP 响应由 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1

CUPS 提供了丰富的函数来管理 HTTP 响应。IPP 响应由 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1

CUPS 提供了丰富的函数来管理 HTTP 响应。IPP 响应由 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1

# 第16章：为 CUPS 编写过滤器

## 什么是过滤器？

过滤器是用于一种格式转换为另一种格式的程序。本章描述了如何为 CUPS 编写过滤器，它是打印的核心。

CUPS 提供了许多转换格式的过滤器。图 16.1 显示了过滤器、打印驱动程序和后端之间的关系。

### 什么是过滤器？

HP-GL 和 HP-GL/2 是所谓的矢量格式。每个文件由一系列初始化命令和绘图命令组成。关于 HP-GL 的完整手册可以在开发者的网站找到：

```
http://www.developer-solutions.com/
```

大多数 CAD 应用生成用于打印的 HP-GL/2 文件和 PostScript 文件。

### hltops 过滤器

`hltops` 过滤器将 HP-GL 和 HP-GL/2 的图文件转换为 PostScript。当图文件包含 PS 命令时，可以使用 `fitplot` 选项进行匹配。如果使用了 `blackplot` 选项，过滤器将只输出黑白。

`hltops` 过滤器使用打印机的 PDF 文件来确定可用页面大小、打印区域和页边距，无论打印机支持颜色。

`hltops` 过滤器的输出通常通过到 `ppstops` 过滤器。

### imagagetops 过滤器

`imagagetops` 过滤器将图像文件转换为 PostScript。它可以按原始大小（默认），在使用 `scaling` 选项时按页面百分比缩放，或者在使用 `ppi` 选项时按分辨率缩放。可以使用 `page-label` 选项或通过 `cupsd.conf` 文件中的 `Classification` 指令添加标签。

该过滤器使用打印机的 PDF 文件来确定可用页面大小、语言级别以及是否为打印机产生 RGB 或灰度数据。图像数据对于 Level 1 PostScript 打印机是十六进制字符串，对于 Level 2 和 3 PostScript 打印机是 base85 编码字符串。

`imagagetops` 过滤器的输出通常直接发送到后端，因此生成的 PostScript 包含所有命令。在使用开启页标签或分类标记的光栅打印机时，`imagagetops` 的输出被管道到 `pstoraster` 以进行系列图像的转换。

> 注意：
> PostScript 打印机支持三种语言级别之一。1 级打印机代表了原始的 PostScript 打印机，例如 Apple LaserWriter。2 级打印机是目前最常用的 PostScript 打印机。3 级打印机于 2000 年底上市，并将在几年后主导 PostScript 打印机市场。
> 
> 每个语言级别都支持许多不同的功能，以及一种通用的核心语言。任何想要编写生成 PostScript 过滤器的程序都需要《Adobe PostScript 语言参考手册》，因为该手册是 Adobe 文档结构规范 (DSC) 规范。您可以在网上找到这些内容：
> 
> ```
> http://partners.adobe.com/asn/developer/technotes/main.html
> ```

### imagetoraster 过滤器

`imagetoraster` 将图像文件转换为一系列栅格图像。它可以将图像缩放为原始尺寸（默认值），或者在使用缩放选项时将其缩放为页面大小的百分比，或者根据您通过 `ppi` 选项指定的解析进行缩放。可以使用 `page-label` 选项创建标签，或者通过 `cupsd.conf` 文件中的 `Classification` 指令创建标签。

过滤器使用 PPD 文件来确定可用页面尺寸、打印区域以及发送到打印机驱动程序的栅格数据类型。PPD 文件中的颜色配置文件信息也会被使用；对于 CUPS 1.1，过滤器支持带有查找表的 CMY 变换矩阵，用于控制栅格数据的整体伽马和密度校正。在 CUPS 1.2 中，PPD 文件可以为每个分辨率、颜色模型和媒体类型指定 ICC 配置文件；这些配置决定了发送到打印机驱动程序的栅格数据的色彩空间。

`imagetoraster` 过滤器的输出被传递到打印机驱动程序，由驱动程序将栅格图像转换为打印页面。

> 注意：
> `imagetops` 和 `imagetoraster` 过滤器使用 `cupsimage` 库来读取和转换图像文件。该库支持对 BMP、GIF、JPEG、PhotoCD、便携 anymap（PBM, PGM, PNM, PPM）、SGI RGB、Sun Raster 和 TIFF 图像文件的读取。

### pdftops 过滤器

`pdftops` 过滤器基于 Derek B. Noonburg 的 Xpdf 软件，将 Adobe 便携文档格式 (PDF) 文件转换为 PostScript。它将 PDF 文档中的页面缩放到请求的页面尺寸。

过滤器使用打印机的 PPD 文件来确定可用页面尺寸、打印区域和打印机的语言级别。

`pdftops` 过滤器的输出被传递到 `pstops` 过滤器。

> 注意：
> PDF 格式可能是电子共享复杂文档最流行的格式，并正迅速成为印前和其他打印应用的标准。其流行的主要原因是其可移植性和开放性格式——PDF 可在任何地方用于任何用途。Apple 的 MacOS 使用 PDF 文件作为其打印架构的基础，GNOME 项目可能在桌面环境的最终版本中使用它。甚至此书的终稿校样也是通过 PDF 文件完成的！
> 
> Adobe 在线维护着 PDF 格式的公开规范：
> 
> ```
> http://partners.adobe.com/asn/developer/technotes/main.html
> ```
> 
> PDFZone 网站也是寻找 PDF 软件和信息的绝佳之地：
> 
> ```
> http://PDFZone.com
> ```

### pstops 过滤器

大多数打印文件都会通过 `pstops` 过滤器。它接收 PostScript 打印文件，将其拆分为页面，并使用必要的打印机命令、选项和胶接代码（glue）重新组合页面，以产生所需的打印作业。

通过 `pstops` 过滤器，您可以使用 `page-ranges` 选项打印页面范围，使用 `page-set` 选项打印奇偶数页，使用 `page-label` 选项和 `Classification` 指令生成页标签和分类标记，以及使用 `number-up` 选项将多个页面放在单个输出页面上。

过滤器使用打印机的 PPD 文件来确定可用页面尺寸以及打印区域和边距。PPD 文件还提供了打印机在作业和每个页面之前所需的命令和其他数据。

`pstops` 过滤器在输出到 PostScript 打印机时会计数信息（"PAGE:" 消息）。

`pstops` 过滤器的输出传递给 PostScript 打印机的后端，或者传递给非 PostScript 打印机的 `pstoraster` 过滤器。

## 第三部分 使用 CUPS 编程

> 注意：
> `pstops` 过滤器解码 PostScript 文件中的注释，以确定文档中每页的开始和结束。这些注释遵循 Adobe 文档结构规范 (DSC) 规范描述的格式，可以在网上获取：
> 
> ```
> http://partners.adobe.com/asn/developer/technotes/main.html
> ```
> 
> 如果您尝试打印没有这些注释的 PostScript 文件，`pstops` 过滤器会将该文件视为单页文件。它不支持页面过滤选项或页面计数。

### pstoraster 过滤器

`pstoraster` 过滤器将 PostScript 文件转换为用于打印机驱动程序的栅格图像。根据嵌入的 PostScript 和命令，过滤器可以为较小尺寸的喷墨打印机和 50 英寸宽绘图仪生成栅格数据。当前的过滤器 `pstoraster` 支持语言级别 1 到 3。

过滤器使用打印机的 PPD 文件来确定可用页面尺寸、打印区域以及发送到打印机驱动程序的栅格数据类型。PPD 文件中的颜色配置文件会被使用；对于 CUPS 1.1，过滤器支持带有查找表的 CMY 变换矩阵，用于控制栅格数据的整体伽马和密度校正。在 CUPS 1.2 中，PPD 文件可以为每个分辨率、颜色模型和媒体类型指定 ICC 配置文件；这些配置决定了发送到打印机驱动程序的栅格数据的色彩空间。

`pstoraster` 过滤器的输出被传递到打印机驱动程序，由驱动程序将栅格图像转换为打印页面。

> 注意：
> `pstoraster` 过滤器基于 Ghostscript 解释器和图形库。在前端，过滤器支持 CUPS 接口而非 Ghostscript 命令行选项。
> 
> 在后端，打印机驱动程序被单一栅格驱动程序取代。该栅格驱动程序生成适用于 CUPS 的栅格数据。`praster` 过滤器还包含了针对标准 GhostScript 发行版的修复。该项目可以在网上找到：
> 
> ```
> http://partners.adobe.com
> ```
> 
> 为 CUPS 文件过滤器
> 
> 该 GhostScript 发行版被多个 Linux 发行版使用，并包含了它们的补丁和修复。该发行版还包含一个适用于 CUPS 的 `praster` 版本，有助于减少磁盘空间需求。

过滤器将文本转换为 PostScript。通过它，您可以使用 `columns` 选项打印多列文本，使用 `prettyprint` 选项突出显示关键字和漂亮标题，以及使用 `wrap` 选项换行。`epi` 和 `lpi` 选项决定文本的大小。

过滤器使用打印机的 PPD 文件来确定可用页面尺寸以及打印区域和边距。PPD 文件还提供了可用字体列表。如果文本需要打印机上不可用的字体，则字体将嵌入文档中。

过滤器处理通常通过回车或退格字符实现的下划线和加粗覆盖方法。分页符换出当前页面。

当您对文本文件使用 `prettyprint` 选项时，过滤器使用 `CONTENT_TYPE` 环境变量来决定如何突出文件中的语法。这些规则目前硬编码在过滤器中。

`textops` 过滤器的输出传递给 `pstops` 过滤器，在发送打印机之前进行进一步处理。

- `textops` 过滤器设计用于支持一个通用的文本引擎和一个生成输出的语言模块。`textops` 过滤器提供了 PostScript 语言模块。在随后的第 17 章中，您将看到使用文本引擎构建用于惠普激光打印机的 PCL 语言模块。

## CUPS 过滤器架构

CUPS 过滤器构打印系统支持任何类型打印能力的核心。调度器选择过滤器将打印文件转换为可打印的形式。除了过滤器程序本身，调度器还会读取 MIME 类型和转换文件，这些文件描述了系统支持的文件类型和过滤器。

前节描述的过滤器列在 `mime.types` 和 `mime.conv` 文件中。这些文件使调度器能够确定打印文件的最低成本过滤方案。

每个过滤器通过管道传递给下一个过滤器，其他消息则写入标准错误文件。链中的第一个过滤器读取命令行上指定的文件。后续的过滤器必须从标准输入文件读取内容。

### 命令行参数

每个过滤器都使用继承自系统打印系统的命令行接口。每个过滤器恰好提供六或七个命令行参数：

```
printer job user copies options filename
printer job user title copies options
```

第一个过滤器带有七个参数运行，而链中第一个之后的每个过滤器只获得六个参数。这使得第一个过滤器可以直接读取打印文件，而每个额外的过滤器则从标准输入读取上一个过滤器的结果。

- `printer` 参数 (`argv[0]`) 是打印机队列的名称，即 `printer-name` 属性的值。

> 注意：
> Shell 解释器会将 `printer` 参数 (S0) 替换为 shell 脚本的名称。如果你在 shell 脚本中需要打印机名称，请使用下一节列出的相应环境变量。

- `job` 参数 (`argv[1]`) 提供正在打印任务的数字 ID。它是 `job-job-id` 属性的值。

- `user` 参数 (`argv[2]`) 提供与任务相关的用户名。它是 `job-job-originating-user-name` 属性的值。

- `title` 参数 (`argv[3]`) 提供与任务相关的名称或标题。它是 `job-job-name` 属性的值。

- `copies` 参数 (`argv[4]`) 提供打印的份数。它是 `job-number-copies` 属性的值。

- `options` 参数 (`argv[5]`) 是由空格分隔的任务模板属性的字符串表示。布尔属性在真值时提供为 "name"，假值时提供为 "!name"。其他属性对于单值属性以 "name=value" 形式提供，集合属性以 "name=value1,value2,...,valueN" 形式提供。可以使用 `cupsParseOptions()` 函数将此字符串转换为 CUPS 选项数组，

```c
int num_options;
cups_option_t *options;
...
num_options = 0;
options = NULL;
num_options = cupsParseOptions(argv[5], num_options, &num_options);
```

- `filename` 参数 (`argv[6]`) 仅提供给第一个过滤器。它指定要转换的打印文件。

> 注意：
> 所有过滤器都必须准备从标准输入读取打印文件。如果过滤器需要对文件进行随机访问，它必须将标准输入上的打印文件复制到临时文件。

### 环境变量

每个过滤器都会接收一组可以使用的固定环境变量。表 16.2 列出了这些环境变量。

#### 表 16.2 传递给 CUPS 过滤器的环境变量

| 名称 | 描述 |
| --- | --- |
| `CHARSET` | 客户端为此打印文件使用的字符集。 |
| `CLASSIFICATION` | 当前系统高分类级别，例如“unclassified（未分类）”。仅在使用时提供。 |
| `CONTENT_TYPE` | 原始文档格式，例如“application/postscript”。 |
| `CUPS_DATADIR` | CUPS 数据文件的位置。 |
| `CUPS_FONTPATH` | CUPS 字体文件的位置。 |
| `CUPS_SERVERROOT` | CUPS 配置文件的位置。 |
| `DEVICE_URI` | 输出设备 URI。 |
| `LANG` | 客户端为此打印文件使用的语言。 |



| `LD_LIBRARY_PATH` | 动态加载路径。仅在使用时提供。 |
| `PATH` | 导出到过滤器的执行路径。 |
| `PPD` | 打印机 PPD 文件的全名。 |
| `PPDD_PRINTER` | 打印队列的名称。 |
| `RIP_CACHE` | 每个过滤器应该使用的最大内存。 |
| `SOFTWARE` | CUPS 软件的名称，通常为“CUPS/1.1”。 |
| `TMPDIR` | 临时文件的目录。 |
| `TZ` | 本地时区。 |
| `USER` | 过滤器用户的名称。 |

`CLASSIFICATION` 和 `LD_LIBRARY_PATH` 环境变量仅在调度器中定义时才会设置。`CLASSIFICATION` 环境变量对应于 `Classification` 指令，如下：

```
Classification secret
```

`LD_LIBRARY_PATH` 环境变量继承自调度器的环境，如下：

```bash
LD_LIBRARY_PATH=/foo/bar; export LD_LIBRARY_PATH
cupsd
```

所有其他环境变量在 `cupsd.conf` 文件中未另行配置时，保证存在并使用默认值。

## 安全考量

过滤器通常以非特权用户运行，因此主要的安全考量是资源利用：过滤器不应依赖于无限的内存和磁盘空间。

当你从用户权限创建或修改文件时也应该小心。如果你需要创建一个临时文件，请使用 `TMPDIR` 环境变量来确定文件位置。

最后，设计你的过滤器以处理缓冲区溢出情况。特别是，要谨慎使用 `gets()`、`sprintf()`、`strcpy()` 等相关函数，这些函数通常是缓冲区溢出的源头。如果你处理了潜在的缓冲区溢出情况（即使你认为它们永远不会发生），也会让你的过滤器更加可靠。

> 注意：
> 不要创建 setuid 或 setgid 过滤器。

## 用户与组

过滤器通常以非特权用户运行，因此主要的安全考量是资源利用：过滤器不应依赖于无限的内存和磁盘空间。

当你从用户权限创建或修改文件时也应该小心。如果你需要创建一个临时文件，请使用 `TMPDIR` 环境变量来确定文件位置。

最后，设计你的过滤器以处理缓冲区溢出情况。特别是，要谨慎使用 `gets()`、`sprintf()`、`strcpy()` 等相关函数，这些函数通常是缓冲区溢出的源头。如果你处理了潜在的缓冲区溢出情况（即使你认为它们永远不会发生），也会让你的过滤器更加可靠。

> 注意：
> 不要创建 setuid 或 setgid 过滤器。

`CLASSIFICATION` 和 `LD_LIBRARY_PATH` 环境变量仅在调度器中定义时才会设置。`CLASSIFICATION` 环境变量对应于 `Classification` 指令，如下：

```
Classification secret
```

`LD_LIBRARY_PATH` 环境变量继承自调度器的环境，如下：

```bash
LD_LIBRARY_PATH=/foo/bar; export LD_LIBRARY_PATH
cupsd
```

所有其他环境变量在 `cupsd.conf` 文件中未另行配置时，保证存在并使用默认值。

## 临时文件

临时文件应在 `TMPDIR` 指定的目录中创建。`cupsTemp()` 和 `cupsTempFd()` 函数可安全创建临时文件。

过滤器结束后应删除临时文件。

## 发送消息

CUPS 调度器从错误文件中收集消息。`logLevel` 指令决定哪些消息会被记录。表 16.3 列出了可用的前缀。

### 表 16.3 CUPS 消息前缀

| 前缀 | 描述 |
| --- | --- |
| `DEBUG:` | 调试消息 |
| `DEBUG2:` | 详细调试消息 |
| `ERROR:` | 错误消息 |
| `INFO:` | 信息消息 |
| `PAGE:` | 页面计数消息 |
| `WARNING:` | 警告消息 |

如果该行不以上述任何一个前缀开头，则被视为 `DEBUG:` 消息并转发到打印机。

## 页面计数

页面计数消息（`PAGE:`）用于在打印多个页面时通知服务器。每个页的格式如下：

```
PAGE: page-number copy-count
```

`page-number` 字段是当前页码，从 1 开始。`copy-count` 字段指定了生成的副本数量。

对于 PostScript 打印机，最后一个处理过滤器应该生成页面计数消息，但在打印非 PostScript 打印机时不会生成这些消息，除非驱动程序生成。

> 注意：
> CUPS 目前提供的计数取决于过滤器准确生成 `PAGE:` 注释。这被广泛认为是 CUPS 计数系统的一个局限。
> CUPS 1.2 增加了一个新接口，允许智能后端从打印机本身收集页面计数信息。当后端提供页面计数信息时，过滤器的 `PAGE:` 注释将被忽略。

## 副本生成

`copies` (`argv[4]`) 参数指定了应生成的输入副本数量。`multiple-document-handling` 选项决定副本是装订的（separate-documents-collated-copies）还是未装订的（separate-documents-uncollated-copies）。

通常情况下，只有在提供了 `filename` (`argv[6]`) 参数时才生成副本。此规则的唯一例外是你使用产生 PostScript 输出并经过过滤的过滤器。这包含了 CUPS 自带的 `hpgltops` 和 `texttops` 过滤器。

当生成装订副本时，PPD 文件中 `Collate` 选项的存在表示打印机能够独立完成装订：

```c
ppd_file_t *ppd;
ppd_option_t *option;
...
option = ppdFindOption(ppd, "Collate");
```

如果你正在为非 PostScript 打印机生成未收集副本，`ppd_file_t` 结构中的 `manual_copies` 成员指示打印机是否可以独立生成副本：

```c
ppd_file_t *ppd;
...
if (ppd->manual_copies)
    puts("The printer can' generate copies on its own.");
```

# 配置与数据文件

配置文件通常存储在 `/etc/cups` 目录下。提供自己的配置文件的过滤器应该使用 `CUPS_SERVERROOT` 环境变量来定位配置文件，而不是硬编码特定目录。

过滤器配置的规范是使用带有 `.conf` 后名的过滤器名称。例如，`pdftoops` 过滤器会查找 `pdftoops.conf` 文件。

同样，数据文件通常存储在 `/usr/share/cups` 下。`CUPS_DATADIR` 环境变量包含了实际使用的目录。

# MIME 类型与过滤器

在你编写过滤器后，你必须向调度器注册它以及它支持的文件格式。标准类型和过滤器在 `mime.types` 和 `mime.convs` 文件中定义，这些文件通常位于 `/etc/cups` 目录下。

调度器在启动时会读取 `/etc/cups` 目录下所有带有 `.types` 和 `.convs` 扩展的文件。

> 注意：
> 多媒体互联网邮件扩展（MIME）规范定义了如何识别和传输不同类型的数据。MIME 媒体类型是一个标识文件格式的字符串，并可能包含可选信息，如文件的字符集或编码。
> MIME 类型由内容类型（text、application、image 等）和子类型（html、postscript、gif 等）组成，用斜杠（/）分隔：
> ```
> text/html
> application/postscript
> image/gif
> ```
> 任何可选信息都跟在子类型之后。分号（；）和逗号（，）用作分隔符：
> ```
> text/plain; charset=utf-8, language=en
> ```
> MIME 类型在互联网分配编号机构（IANA）注册，并在网上列在以下链接中：
> http://www.iana.org/
> http://www.isi.edu/in-notes/iana/assignments/media-types/media-types

# MIME 类型文件格式

每个 `.types` 文件为调度器定义文件类型；`mime.types` 文件定义标准文件类型。

`.types` 文件的每一行都以 MIME 类型开头，后面可能跟随一个或多个类型识别规则。例如，`text/html` 文件定义为：

```
html html \
    printable(0,1024) + \
(string(0,"<HTML"> string(0,"<!DOCTYPE>>"))
```

前两个规则说明任何扩展名为 `.html` 或 `.htm` 的文件都是 HTML 文件。第三条规则说，任何前 1024 个字符是可打印的且以 `<HTML><!DOCTYPE>` 字符串开头的文件也是 HTML 文件。

前两个规则仅处理文件的类型名称。这在原始文件名已知时（例如你在 Web 浏览器中查看文件时）非常有用。

然而，对于打印文件，服务器没有文件名可以操作。第三条规则考虑了这种可能性，并根据文件内容自动判断文件类型。

如 `text/html` 示例所示，如果使用反斜杠（\），规则可以跨行。一个更复杂的例子是 `image/jpeg` 规则：

```
image/jpeg jpeg jpg string(0,"<FFD8>>) &&&
char(3,0xe0) char(3,0xe1) char(3,0xe2) char(3,0xe3)
char(3,0xe4) char(3,0xe5) char(3,0xe6) char(3,0xe7)
char(3,0xe8) char(3,0xe9) char(3,0xea) char(3,0xeb)
char(3,0xec) char(3,0xed) char(3,0xef)
```

该规则规定，任何扩展名为 `.jpeg`、`.jpg` 或 `.jpe` 的文件都是 JPEG 文件。此外，任何以十六进制字符串 `<FFD8>`（JPEG 图像开始）开头，后跟 `0xe0` 到 `0xef` 之间的字符（JPEG APPn 标记）的文件也是 JPEG 文件。

表 16.4 列出了可用于文件类型的可用规则。

# 表 16.4 用于 CUPS 的 MIME 类型识别规则

| 规则 |  |
| :--- | :--- |
| `( expr )` | 用于表达式分组的括号 |
| `"+"` | 逻辑与 |
| `","` 或空白 | 逻辑或 |
| `"!"` | 逻辑非 |
| `ascii(offset,length)` | 如果字节是可打印的 ASCII (CR, NL, TAB, BS, 32-126) 则为真 |
| `char(offset,value)` | 字节相同则为真 |
| `contains(offset,range,'string')` | 如果字节范围包含该字符串则为真 |
| `extension` | 对“扩展名”进行模式匹配 |
| `int(offset,value)` | 如果 32 位整数相同（网络或“大端字节”序）则为真 |
| `locale('string')` | 如果当前区域设置匹配字符串则为真 |
| `match('pattern')` | 对文件名进行模式匹配 |
| `printable(offset,length)` | 如果字节是可打印的则为真 |
| `string(offset,'string')` | 如果字节范围包含该字符串则为真 |

## 列表 16.1 续

```bash
else
  filename=$6
fi

  # 运行 dvips转换为 PostScript，将输出发送到
  # stdout...
  dvips -R q -o $filename

  # 根据需要删除临时文件...
  if test $ -lt 6; then
    rm -f $filename
```

要使用 `dvips` 过滤器，你需要为该过滤器创建 `.types` 和 `.convs` 文件。由于你只有一个过滤器和一种类型，你应该使用过滤器名称作为这些文件的前缀，或者使用 `dvips.types` 和 `dvips.convs`。

`dvips.types` 文件应该包含一个针对 DVI 类型的条目；由于该类型尚未向 IANA 注册，因此其子类型名称带有 "x-" 前缀：

```
application/x-dvi type string(0,<F702>)
```

识别规则规定，任何带有 `.dvi` 扩展名或以字符串 `<F702>` 开头的文件都是 DVI 文件。

`dvips.convs` 文件应该包含一行 `dvips` 过滤器的内容：

```
application/x-dvi application/postscript 50 dvips
```

为过滤器使用 50 的成本值，如果你不知道特定过滤器的实际成本，这是一个很好的初始值。

要安装此过滤器，首先将从当前目录创建的文件复制到 `/etc/cups` 和 `/usr/lib/cups/filter` 目录：

```bash
cp dvips.types /etc/cups/
cp dvips.convs /etc/cups/
cp dvips /usr/lib/cups/filter/
```

然后使用提供的 init 脚本或通过向其发送 HUP 信号重启 `cupsd` 进程：

```bash
/etc/init.d/cups restart
kill -HUP pid
```

恭喜——你现在可以打印 DVI 文件了！

## PostScript 输出

产生 Postscript 输出的过滤器必须生成符合 Adobe文档结构规范 (DSC) 版本3.0 输出。符合 DSC 的 PostScript 文件包含注释，使 PostScript 过滤器能够正确执行计数、副本生成、多份打印等。某些打印机还需要这些注释来打印文件。

要生成符合标准的文件，请以以下头开始每个文件：

```
%!PS-Adobe-3.0
%%BoundingBox: left bottom right top
%%Pages: (attend)
%%Endments
```

左、下、右、上的值定义了整个文档的边界框（bounding box）。边界框定义了包含打印数据的区域。这些值是从页面左下角开始的磅单位整数（见图16.3）。

![](img/b159ac7fe2135643dc37ccfeef6d3980_347_0.png)

过滤器可以自由定义边界框为所选页面大小的整个区域。例如，过滤器可以使用 `ppdPageWidth()` 和 `ppdPageLength()` 函数生成右值和上值：

```c
ppd_file_t *ppd;
int width;
int length;
...
width = ppPageWidth(ppd, NULL);
length = ppdPageLength(ppd, NULL);
printf("%%BoundingBox: 0 0 %d\n", width, length);
```

文档设置命令紧随头之后，页面紧随文档设置命令。以下行必须包围 PostScript 输出中的每一页：

```
%%Page: label number

gsave

.. your output goes here ...

grestore

showpage
```

`number` 字段指定页码。页码从 1 开始，并在整个文件中不断增加。`label` 字段指定一个人类可读的页码，但通常与数字 相同。

PostScript 输出的结束必须包含以下行：

```
%%Trailer

%%Pages: number-pages

%%EOF
```



`number-pages` 字段指定文档的总页数。

> 注意：
> 永远不要在你的 PostScript 输出中设置 `copy` 或使用 `copypage` 操作符。这些会阻止计数工作，你可能无法得到预期的结果。
> 此外，每个 PostScript 语言级别都支持许多不同的功能以及共同的核心语言。对于任何想要编写产生 PostScript 的过滤器的人来说，《Adobe PostScript 语言参考手册》是必读的，《Adobe 文档结构规范》也是如此。你可以在网上找到这些内容：
> http://partners.adobe.com/asn/developer/technotes/main.html

使用 `ppd_file_t` 结构的 `language_level` 成员来确定打印机支持的 PostScript 级别。如果你使用了打印机支持的新语言功能，你可能无法获得任何输出——即使是错误页面。

## 栅化输出

某些过滤器使用 `cytoplasm` 库为打印机驱动程序产生栅化输出。`imagoraster` 和 `pstoraster` 过滤器都使用此库产生栅化输出。

CUPS 栅化数据由一个文件头以及一个或多个栅化页组成。每页包含一个页头，随后是像素数据。图16.4 显示了栅化流的总体结构。

![](img/b159ac7fe2135643dc37ccfeef6d3980_349_0.png)

图 16.4
CUPS 栅化流。

CUPS 提供了几个写入栅化流的函数。这些函数与栅化文件中使用的数据结构和常量一起定义在 `<cups/raster.h>` 中。

（注：由于原文中存在大量重复的OCR错误，已根据逻辑进行去重处理。）

## 第三部分 在 CUPS 中进行编程

页头结构中的大多数成员与 PostScript 页面设备字典属性直接对应。`cups` 成员专门为光栅化数据定义了信息。

`cups@colorspace` 字段指定输出色彩空间。表 16.7 列出了所有支持的色彩空间。

### 表 16.7 CUPS 支持的色彩空间

| own | 描述 |
| --- | --- |
| `CUPS_COLORPACE_CMY` | 青色、洋红色、黄色 |
| `CUPS_COLORPACE_CMYK` | 青色、洋红色、黄色、黑色 |
| `CUPS_COLORPACE_GCMK` | 金色、洋红色、黄色、黑色 |
| `CUPS_COLORPACE_GMCS` | 金色、洋红色、黄色、银色 |
| `CUPS_COLORPACE_GOLD` | 金箔 |
| `CUPS_COLORPACE_ICC1` | 1 通道 ICC 色彩数据（仅限 CUPS 1.2） |
| `CUPS_COLORPACE_ICC2` | 2 通道 ICC 色彩数据（仅限 CUPS 1.2） |
| `CUPS_COLORPACE_ICC3` | 3 通道 ICC 色彩数据（仅限 CUPS 1.2） |
| `CUPS_COLORPACE_ICC4` | 4 通道 ICC 色彩数据（仅限 CUPS 1.2） |
| `CUPS_COLORPACE_ICC5` | 5 通道 ICC 色彩数据（仅限 CUPS 1.2） |
| `CUPS_COLORPACE_ICC6` | 6 通道 ICC 色彩数据（仅限 CUPS 1.2） |
| `CUPS_COLORPACE_ICC7` | 7 通道 ICC 色彩数据（仅限 CUPS 1.2） |
| `CUPS_COLORPACE_ICC8` | 8 通道 ICC 色彩数据（仅限 CUPS 1.2） |
| `CUPS_COLORPACE_K` | 黑色/灰度 |
| `CUPS_COLORPACE_CMY` | 黑色、青色、洋红色、黄色 |
| `CUPS_COLORPACE_CMYK` | 黑色、青色、洋红色、黄色、浅青色、浅洋红 |
| `CUPS_COLORPACE_RGB` | 红色、绿色、蓝色 |
| `CUPS_COLORPACE_RGBA` | 红色、绿色、蓝色、alpha 通道 |
| `CUPS_COLORPACE_SILVER` | 银箔 |
| `CUPS_COLORPACE_W` | 白色/亮度 |
| `CUPS_COLORPACE_WHITE` | 白色墨（视为黑色） |
| `CUPS_COLORPACE_YMC` | 黄色、洋红色、青色 |
| `CUPS_COLORPACE_YCMK` | 黄色、洋红色、青色、黑色 |

`cupsColorOrder` 字段指定颜色值的组织方式。图 16.5 显示了不同的颜色顺序。

`cupsBitsPerColor` 字段指定了每个颜色的比特数。CUPS 1.1 及之前的版本支持每颜色 1、2、4 和 8 位。当使用 ICC 色彩配置文件和色彩空间时，CUPS 1.2 支持每颜色 16 位。

### CUPS_ORDER_CHUNKED（分块）

| CMYK CMYK CMYK CMYK CMYK CMYK CMYK CMYK CMYK CMYK |
| CMYK CMYK CMYK CMYK CMYK CMYK CMYK CMYK CMYK CMYK |
| CMYK CMYK CMYK CMYK CMYK CMYK CMYK CMYK CMYK CMYK |
| CMYK CMYK CMYK CMYK CMYK CMYK CMYK CMYK CMYK CMYK |
| CMYK CMYK CMYK CMYK CMYK CMYK CMYK CMYK CMYK CMYK |
| CMYK CMYK CMYK CMYK CMYK CMYK CMYK CMYK CMYK CMYK |

### CUPS_ORDER_BANDED（带状）

| CCCCCCC MMMMMMMMMM YYYYYYYY KKKKKKKKK |
| CCCCCCC MMMMMMMMM YYYYYYYY KKKKKKKKK |
| CCCCCCC MMMMMMMMM YYYYYYYY KKKKKKKKK |
| CCCCCCC MMMMMMMMM YYYYYYYY KKKKKKKKK |
| CCCCCCC MMMMMMMMM YYYYYYYY KKKKKKKKK |
| CCCCCCC MMMMMMMMM YYYYYYYY KKKKKKKKK |

### CUPS_ORDER_PLANAR（平面）

| CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC |
| CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC |
| CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC |

| MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM |
| MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM |
| MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM |

| YYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY |
| YYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY |
| YYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY |

| KKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKK |
| KKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKK |
| KKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKKK |

### 图 16.5

CUPS 光栅颜色顺序。

注意：

写入光栅数据可能是非常复杂的。一个编写得当的可以扫描 PPD 文件中的命令，以确定页头中各个字段的正确值。

查阅 `imagetraster` 的主源文件。

## 写入数据

`cupsPixels()` 函数用于写入页面数据：

```c
cups_raster_t *ras;

unsigned char buffer[1024];

cupsRaster(ras, buffer);
```

`ras` 参数指向数据流。`buffer` 参数指向缓冲区。`length` 参数指定要写入的字节数。`cupsPixels()` 的返回值是写入的字节数，出错时返回 -1。注意：`cupsPixels()` 确保了页头的正确性，否则可能会写入过多或过少的数据。

HP-GL/2 过滤器通过扫描 PPD 文件来获取值；该实现可以在 `imagetraster.c` 中找到。

## 初始化过滤器

在打开打印文件之前，需要处理色彩空间等参数：

```c
if (argc == 6)
    fp = stdin;
else
{
    /* 尝试打开文件 */
    fp = fopen(argv[6], "rb");
}
```

在打开打印文件后，可以使用 `cupsParseOptions()` 和 `cupsGetOption()` 函数处理选项：

```c
int num_options;
cups_option_t *options;
const char *val;

/* 处理命令行选项 */
options = cupsParseOptions(argv[5], 0);
if ((val = cupsGetOption("black", num_options, options)) != NULL)
    shading = 0;
if ((val = cupsGetOption("fit", num_options, options)) != NULL)
    FitPlot = 1;
if ((val = cupsGetOption("penwidth", num_options, options)) != NULL)
    PenWidth = (float)atoi(val) * 0.001;
```

## 输出PS 页头

在处理完选项后，CUPS 会向标准输出写入 PostScript 页头：

```c
void OutputProlog(char *title,      /* 标题 */
             char *user,         /* 用户 */
             int  shading)      /* 阴影类型 */
{
    FILE                              /* 页头文件 */
    char *line[255];                  /* 来自页头的行 */
    const char *datadir;              /* CUPS_DATADIR 环境变量 */
    char *filename[1024];             /* 页头文件名 */
    time_t curtime;                   /* 当前时间 */
    struct tm curm;                   /* 当前日期 * */

curtime = time(NULL);
curm    = localtime(&curtime);

puts("%%PS-Adobe-3.0\n");
printf("%%BoundingBox: %f %f %f %f\n",
    PageLeft, PageBottom, PageRight, PageTop);
puts("%%Pages: %d\n", (atend));
printf("%%LanguageLevel: %d\n", LanguageLevel);
puts("%%DocumentData:Clean7bit\n");
puts("%%DocumentSuppliedResources: process hpgltops 1.1 *\n");
puts("%%DocumentNeededResources: font Helvetica\n");
puts("%%Creator: hpgltops/CUPS_SVERSION\n");
strftime(line, sizeof(line), CUPS_STRTIME_FORMAT, curm);
printf("%%CreationDate: %s\n", line);
printf("%%Title: %s\n", title);
printf("%%For: %s\n", user);
if (Orientation & 1)
    puts("%%Orientation: Landscape\n");
    puts("%%Comments\n");
    puts("%%BeginProlog\n");
printf("%%DefaultPenWidth: %.2f\n", PenWidth, 72.0 / 25.4);
puts("3.0 setmeterlimit;\n");
if (shading) /* Black out */
    puts("%%setrgbcolor { pop pop pop pop } bind def;\n");
else if (!ColorDevice)
    puts("%%setrgbcolor { 0.08 mul ex 0.61 mul add ex 0.31 mul add setgray }\n");
bind def\n");
}
```

```c
if ((datadir = getenv("CUPS_DATADIR")) == NULL)
datadir = CUPS_DATADIR;
snprintf(filename, sizeof(filename), "%s/data/HPGLprolog", datadir);
if ((prolog = fopen(filename, "r")) == NULL)
{
    fprintf(stderr, "ERROR: Unable to open HPGL prolog %%s\n for reading - %%s\n",
    filename, strerror(errno));
    exit(1);
}
while (fgets(line, sizeof(line), prolog) != NULL)
    fputs(line, stdout);
close(prolog);
puts("%EndProlog");
IN_initialize(@0, NULL);
```

接下来，过滤器读取绘图文件，根据需要发送 PostScript 绘制命令。当它看到 PG（页面分页）命令时，它会发送一个 showpage 命令。每个页面都封装在之前描述的标准 DSC 注释中。

当所有绘图数据读取完毕后，将写入标准的 PostScript 轨迹（trailer）：

```c
void
OutputTrailer(void)
{
    if (PageDirty)
        PG_advance_page(@0, NULL);
    puts("%%Trailer");
    printf("%%%%Pages: %%d\n", PageCount);
    puts("%%EOF");
}
```

最后，过滤器（根据需要）关闭打印文件并向调度器返回 0：

```c
if (fp != stdin)
    fclose(fp);
return (0);
```



## 总结

文件过滤器构成了 CUPS 打印过程的核心。它们将打印文件转换为打印机可以理解的形式。CUPS 不是提供一个处理所有内容的单体程序，而是提供了许多较小的单一用途过滤器。这些过滤器通过管道连接在一起，以便你可以获得所需的输出格式。

过滤器使用通用接口处理打印，并向用户和调度器提供状态信息。`cups` 库提供了开发 CUPS 过滤器所需的各种函数。过滤器也可以使用在现有程序周围的 shell 脚本编写，通常在性能或功能上没有或几乎没有区别。

编写 PostScript 的过滤器必须遵循 Adobe 文档结构规范（DSC），以确保 PostScript 输出与所有其他过滤器和打印机兼容。

写入光栅数据（raster data）的过滤器使用 `cupsimage` 库将光栅流写入打印机驱动程序。光栅过滤器可能是最难写的，但 CUPS `imagetoraster` 过滤器的源代码可以作为其他过滤器的示例实现，减少开发时间。

# 第 17 章

## 为 CUPS 编写打印机驱动

本章描述了如何为 CUPS 编写打印机驱动，包括 CUPS 自带的高级 HP PCL 驱动程序。

# 概述

CUPS 中的打印机驱动是与特定打印机关联的过滤器程序。每个打印机驱动由一个 PostScript 打印机描述（PPD）文件和一个多个将中间文件转换为可打印数据的过滤器程序组成。图 17.1 显示了典型打印机驱动的结构。

![](img/b159ac7fe2135643dc37ccfeef6d3980_360_0.png)

图 17.1

CUPS 打印机驱动架构。

PostScript 打印机通常不需要额外的过滤器，因为内置的 PostScript 过滤器通常可以处理一切。某些 PostScript 打印机可以直接打印其他类型的文件，例如将 PDF 文件打印到 Level 3 PostScript 打印机。因此，过滤器可以提供增强的打印支持，即使对于 PostScript 打印机也是如此。

非 PostScript 打印机通常提供光栅驱动过滤器，将 CUPS 光栅数据转换为打印机可以理解的格式。正如本章后面所示，还可以添加其他驱动过滤器来提供增强的打印支持。

# 理解 PostScript 打印机描述 (PPD) 文件

PPD 文件为 CUPS 中的所有打印机驱动提供了基础。PPD 文件由纯文本组成，包含四个基本部分：

- 打印机识别（Printer identification）
- 约束（Constraints）
- 选项（Options）
- 字体（Fonts）

Mac 中的每一行可能以 Unix 的换行符（LF）、MacOS 的回车符（CR）或 Windows 的 CR 和 LF 结束。注释行以字符串“*%” 开头并持续到行尾。

# 打印机识别部分

打印机识别部分从标准的 PPD 头部开始：

*PPD-Adobe: "4.3"

“PPD-Adobe:” 标识该文件为 PPD 文件，而 “4.3” 值标识该 PPD 文件遵循的 PPD 规范版本。

> 注意：
> Adobe 在线维护 PostScript 打印机描述文件：
> http://partners.adobe.com/asn/developer/technotes/main.html

打印机识别属性紧随头部：

**FormatVersion: "4.3"**
*FileVersion: "1.1"
*LanguageVersion: English
*LanguageEncoding: ISOLatin1
*PCFileName: "LASERJET.PPD"
*Manufacturer: "ESP"
*Product: "(CUPS v1.1)"
*ModelName: "HP Laser Series"
*ShortNickName: "HP Laser Series"
*NickName: "HP Laser Series CUPS v1.1"
*PSVersion: "(3010.000) 550"
*LanguageLevel: "3"
*ColorDevice: False
*DefaultColorSpace: Gray
*FileSystem: False
*Throughput: "8"
*LandscapeOrientation: Plus90
*VariablePaperSize: False
*TTRasterizer: Type42

如你所见，PPD 文件中的所有属性都以“*”字符开头。Format 属性指定了文件的规范版本，并必须与第一行的版本号匹配。

# 第三部分 编程 CUPS

`LanguageLevel` 属性指定了支持的 PostScript 级别。对于光栅驱动，这应该始终为 3。

`NickName` 属性指定了打印器的通用名称。这是你在 Web 界面中以及运行 `lpinfo` 命令时看到的名称。

`ColorDevice` 属性指定了打印机是否支持彩色。对于彩色打印机使用 True，对于灰度打印机使用 False。

除了必需属性外，CUPS 驱动还提供了额外的属性，用于识别过滤器以及该打印机的特有属性：

**cupsVersion: 1.1**
*cupsManualCopies: True
*cupsFilter: "application/vnd.cups"
*cupsModelNumber: 2
*cupsDuplex: True
*cupsProfile: "1.0 1.5 1.0 -0.25 -0 -0.25 -0.25 0.9"

`cupsversion` 属性指定了开发该驱动的 CUPS 版本。仅使用主版本和次版本号（1.0, 1.1 等）。

`cupsManualCopies` 属性指定了打印机或驱动是否可以独立生成副本。`pasterfilter` 使用此属性来决定是否生成副本。

`cupsFilter` 属性指定了打印时使用的过滤器。格式为：

```
source cost
```

其中 `source` 是文件的 MIME 类型，`cost` 是相对成本，`filter` 是过滤器程序的名称。目标类型假设为打印机格式。

`cupsModelNumber` 属性为打印机提供一个数字，用于区分使用相同驱动的不同打印机。此属性通常用于确定使用哪个命令集。

`cupsDuplex` 属性指定了页面图像必须旋转 180 度。这用于双面打印。

`cupsProfile` 属性指定了打印机的色彩配置文件。属性列出了分辨率和媒体类型：

**resolution/type: "profile"**

字段指定了此处的分辨率选项名称，而字段指定了媒体类型选项名称。`profile` 字符串可以是亮度、密度和 CMY 转换值的列表，也可以是 ICC 配置文件的名称。（只有 CUPS 1.2 支持 ICC 文件。）

# 约束

PPD 文件还包含不兼容属性。约束基本上告诉驱动或界面某些选项是不兼容的。每个约束由 `UIConstraints` 描述：

```
*UIConstraints: *PageSize Executive *InputSlot Envelope
*UIConstraints: *PageSize Letter *InputSlot Envelope
*UIConstraints: *PageSize Legal *InputSlot Envelope
*UIConstraints: *PageSize Tabloid *InputSlot Envelope
*UIConstraints: *PageSize A3 *InputSlot Envelope
*UIConstraints: *PageSize A5 *InputSlot Envelope
*UIConstraints: *PageSize B5 *InputSlot Envelope
*UIConstraints: *Duplex *Option1 False
```

约束的值可以是两个选项和选择，其中选项名称以星号（*）开头，而选项选择没有：

*UIConstraints: *PageSize Executive *InputSlot Envelope

此约束表示当从信封槽打印时，不能选择 Executive 尺寸。

约束也可以适用于特定选项的任何选择。例如，双面选项可能取决于打印机是否带有双面打印单元。以下规则规定，如果没有安装双面单元（`Option1 = False`），则不能选择双面选项：

*UIConstraints: *Duplex *Option1 False

# 选项

PPD 文件可以包含任意数量的选项或选项组。每个选项可以是一个布尔值（Boolean）、允许从列表中选择一个（PickOne），或允许选择多个项（PickMany）。`*OpenUI` 关键字启动一个新选项：

`OpenUI *option/text: type`

`option` 字段指定选项的名称，最多包含 40 个字母和数字。选项名称对大小写敏感，尽管 CUPS 为了方便起见支持不区分大小写的选项。

`text` 字段指定了该选项的可读性名称。它可以包含包括空格在内的任何文本。冒号（:）和所有 8 位文本字符必须以十六进制值的形式表示：

`OpenUI Foo/Foo<2>: type`

`type` 字段指定选项的类型：Boolean、PickOne 或 PickMany。

接下来是 `*OrderDependency` 关键字，它指示了该选项命令的相对顺序：

`*OrderDependency: order section *option`

再次，`option` 是顺序的名称。`order` 字段指定了该选项命令的相对顺序。例如，如果 `option1` 的顺序值为 10，而 `option2` 的顺序值为 5，则在发送 `option1` 的命令之前发送 `option2` 的命令。

`section` 字段指定了何时发送命令，可以是表 17.1 中列出的值之一。

| TABLE 17.1 选项的 PPD 节名称 |
|---|---|---|
| Name | Description |
| AnySetup | 选项必须包含在 DocumentSetup 或 PageSetup节中。 |
| DocumentSetup | 选项必须包含在 DocumentSetup节中。 |
| ExitServer | 选项必须在打印文件其余之前单独作业发送。 |
| JCLSetup | 选项必须与 JCL 命令一起发送。 |
| PageSetup | 选项必须包含在 PageSetup节中。 |
| Prolog | 选项必须包含在 Prolog节中。 |

节名称对应 Adobe 文档结构规范。

为 CUPS 编写打印机驱动程序 第17 章

## 注意：
Adobe 在线维护着文档结构规范。

```
http://partners.adobe.com/asn/developer/technotes/main.html
```

`OrderDependency` 关键字之后是选项的默认值：

`*Defaultoption: choice`

其中 `option` 是选项名称，`choice` 是默认选项的名称。

默认值之后是该选项的实际选择：

`*option choice/text: "command"`

该字段是一个最多 40 个字母和数字的字符串，且对大小写敏感。`text` 字段是该选择的可读字符串。`command` 字符串是在选择该选项时发送到打印机或驱动程序的命令。最后，`CloseUI` 关键字结束选项定义：

`*CloseUI: option`

# 页面尺寸

页面尺寸由四组选项描述。前两个是 `PageSize` 和 `PageRegion` 选项：

- `*OpenUI PageSize/Media Size: PickOne`
- `*OrderDependency: 10 AnySetup`
- `*DefaultPageSize: Letter`
- `*PageSize Letter/US Letter: "<<PageSize[612 792]/ImagingBox>>setpagevice"`
- `*PageSize A4/A4: "<<PageSize[595 842]/ImagingBox>>setpagevice"`
- `*CloseUI: PageSize`

- `*OpenUI PageRegion: PickOne`
- `*OrderDependency: 10 AnySetup`
- `*DefaultPageRegion: Letter`
- `*PageRegion Letter/US Letter: "<<PageSize[612 792]/ImagingBox>>setpagevice"`
- `*PageRegion A4/A4: "<<PageSize[595 842]/ImagingBox>>setpagevice"`
- `*CloseUI: PageRegion`

传统上，`PageRegion` 选项用于手动进纸打印，而 `PageSize` 选项用于普通打印；但现在已过时。现代打印机和驱动程序提供了相同的 `PageSize` 和 `PageRegion` 选项。第三个选项是 `ImageableArea`。它定义了每页打印区域的边界：

- `*DefaultImageableArea: Letter`
- `*ImageableArea Letter/US Letter: '18 36 594 786'`
- `*ImageableArea A4/A4: '18 36 577 836'`

这些值提供了以点（points）为单位的左、底、顶坐标。最后，`PaperDimension` 选项提供了每个页面尺寸的物理尺寸：

- `*DefaultPaperDimension: Letter`
- `*PaperDimension Letter/US Letter: '612 792'`
- `*PaperDimension A4/A4: '595 842'`

这些值是页面以点为单位的宽度和长度。

# 字体

PPD 文件的最后部分包含打印机支持的字体列表。每行指定字体名称、编码、版本、字符集和状态：

`*Font encoding "(version)" status`

`font` 字段是 PostScript 字字体名称。`encoding` 字段对于普通字体通常是 Standard，对于如 Zapf-Dingbats 等字体为 Special。你可以在 PPD 规范中找到完整的编码列表。`version` 字符串为字体提供了版本号。`charset` 字符串指定了字体包含哪些字符。Standard 字符集指定该字体能够表示大多数拉丁字母。Extended 字符集增加了西里尔语和其他欧洲语言的字符。Special 字符集用于如 Zapf-Dingbats 等字体。`status` 字段指定了字体是驻留在打印机上（ROM）还是需要下载到打印机中（Disk）。

> 注意：CUPS 目前仅跟踪字体在打印机上的存在，而不跟踪字体特定的编码、版本、字符集或状态。这在未来的 CUPS 版本中可能会发生。

# 为 HP 打印机编写文本驱动程序

第16 章解释了 `texttops` 过滤器设计用于支持 PostScript 中的其他输出语言。由于 HP PCL 打印机同时支持纵向和横向文本，你可以相当地为 PCL 打印机添加语言模块，并在过程中加快文本打印：为 PCL 打印机添加语言模块，并在过程中加快文本打印：

```c
/* 设置任何分类/标签字符串... */
memset(file_notice, 0, sizeof(file_notice));
if (classification || label) {
    if (classification) {
        if (strcmp(classification, "confidential") == 0)
            classification = "CONFIDENTIAL";
        else if (strcmp(classification, "classified") == 0)
            classification = "CLASSIFIED";
        else if (strcmp(classification, "secret") == 0)
            classification = "SECRET";
        else if (strcmp(classification, "topsecret") == 0)
            classification = "TOP SECRET";
        else if (strcmp(classification, "unclassified") == 0)
            classification = "UNCLASSIFIED";
    }
}
if (classification && label) {
    snprintf(s, sizeof(s), "%s - %s", classification, label);
} else if (classification) {
    strncpy(s, classification, sizeof(s) - 1);
    s[sizeof(s) - 1] = '\0';
} else {
    strncpy(s, label, sizeof(s) - 1);
    s[sizeof(s) - 1] = '\0';
}
```

在你获得这些单词后，将字符转换为文本过滤器的 `lchar_t` 结构体，以便它们以**粗体**形式打印：

```c
for (ptr = s, lptr = file_notice + (SizeColumns - strlen(s)) / 2; ;
    *ptr;
    ptr++, lptr ++)
{
    lptr->ch = *ptr;
    lptr->attr = ATTR_BOLD;
}
```

最后，使用一系列 PCL 命令初始化打印器。

# WritePage() 函数

`WritePage()` 函数为过滤器提供了“核心”逻辑。它负责实际上将每一页写入打印机。第一步是向调度程序发送即将发送到打印机的页面的 `PAGE:` 消息：

NumPages ++;

```c
```



`fprintf(stderr, "PAGE: %d\n", NumPages, Copies);`

在准备好打印机后，调用名为 `write_line()` 的本地函数来将每一行写入打印机。每行中的每个字符都存储在 `lchar_t` 结构体中，该结构包含了字符及其属性。`write_line()` 会扫描使用相同属性的行，并使用本地函数 `write_string()` 写入每个片段。

在写完所有行后，弹出页面，清空页缓冲区并返回：

```c
/* 弹出页面。 */
putchar(0x0c);
```

```c
/* 清空页面。 */
memset(Page[0], 0, sizeof(lchar_t) * SizeColumns * SizeLines);
```

# 使用 texthtop 过滤器

列表 17.1（Listing 17.1）显示了编译后的 `texthtop.c` 模块。由于它基于 CUPS 过滤器，你需要复制 `common.h`、`common.c`、`textcommon.h` 和 `textcommon.c` 源文件，并使用这些文件构建 `texthtop`：

```bash
cc -o texthtop texthtop testcommon.c common.c -lcups
```

第 17 章的示例目录还包含一个 `Makefile` 以及这些文件的副本，以便于制作过滤器：

```bash
make texthtop ENTER
```

构建好 `texthtop` 过滤器后，将其复制到 CUPS 过滤器目录：

```bash
cp texthtop /usr/lib/cups/filter ENTER
```

然后向 `/usr/share/cups/model` 目录下的 `laserjet.ppd` 和 `deskjet.ppd` 文件中添加该行：

```text
cupsFilter: "text/* 0 texthtop"
```

这告诉调度器可以使用该过滤器更快地打印文本文件。

最后，重新添加使用 `laserjet.ppd` 或 `deskjet.ppd` 驱动打印机以注册新过滤器。

# 列表 17.1 textohp.c 文本驱动模块

```c
/* 包含必要的头文件... */
#include "textcommon.h"
/* 本地函数... */
static void write_line(int row, lchar_t *lchar);
static void write_string(int col, int row, int len, lchar_t *lchar);
/* 本地全局变量... */
static char file_date[255],
       file_title[255];
static lchar_t file_notice[255]; /* 分类 + 警告 */
/* 'main()' - 文本到 HP-PCL 过滤器的入口。 */
int
/* O - 退出状态 */
main(int argc, /* I - 命令行参数数量 */
    char *argv?) /* I - 命令行参数 */
{
    /* 打印内容。 */
    return (TextMain("textohp", argc, argv));
}
```

```c
/* 'WriteEpilogue()' - 写入 HP-PCL 文件尾部。 */
void
WriteEpilogue(void)
{
    printf("\u033E");
```

# 列表 17.1 续

```c
free(Page[0]);
free(Page);
}
```

```c
/*
 * 'WritePage()' - 写入一页文本。
 */
```

```c
void
WritePage(void)
{
    float left       /* 左边距 */
           width;      /* 页面宽度 */
    int   line;       /* 当前行 */
    char  page[255];  /* 页码 */
```

# 列表 17.1 续

```c
else{
  strncpy(s, label, sizeof(s) - 1);
  s[sizeof(s) - 1] = '\0';
}
```

```c
for (ptr = s, lptr = file_notice + (SizeColumns) strlen(s)) / 2;
  *ptr;
  ptr++, lptr ++)
{
  lptr->ch = *ptr;
  lptr->attr = ATTR_BOLD;
}
```

```c
/* 设置实际媒体尺寸和字符大小... */
printf("\033E");
printf("\033&1%dX", Copies);
printf("\033&1%d0", Orientation);
```

```c
switch ((int)(PageLength + 0.5f))
{
  case 540 : /* Monarch号信封 */
    printf("\033&180A");
    break;
case 624 : /* DL 信封 */
    printf("\033&190A");
    break;
case 649 : /* C5 信封 */
    printf("\033&191A");
    break;
case 684 : /* COM-10 信封 */
    printf("\033&181A");
    break;
case 709 : /* B5 信封 */
    printf("\033&1100A");
    break;
case 756 : /* 执行尺寸 Executive */
printf("\033&1A");
break;
case 792 : /* 信纸尺寸 Letter */
printf("\033&12A");
break;
case 842 : /* A4 纸 */
printf("\033&126A");
break;
case 1008 : /* 法定尺寸 Legal */
printf("\033&13A");
break;
case 1191 : /* A3 纸 */
printf("\033&127A");
break;
case 1224 : /* 报纸尺寸 Tabloid */
printf("\033&16A");
break;
default:
    /* 设置页长 */
    printf("\033&%1.2f", PageLength / 12.0);
    break;
}
```

```c
printf("\033&10L"); /* 关闭打孔跳过 */
printf("\033&10E"); /* 重置上页距为 0 */
```

```c
if ((input_slot = ppfindMarkedChoice(ppd, "InputSlot")) != NULL) {
    if ((temp = strstr(input_slot->code, "/cupsMediaPosition")) != NULL)
        if ((pos = atoi(temp + 19)) != 0)
            printf("\033&%dH");
}
```

```c
printf("\033&%1dS", Duplex + (Orientation & 1));
printf("\033&%sH", CharPerInch);
printf("\033&%s.2f", 72.0 / (float)LinesPerInch);
```

```c
if (ColorDevice)
    printf("\033*r3U");
```

```c
/*
 * 获取输出字符集；如果是未定义或 "us-ascii"，则
 * 什么都不做，因为我们可以使用默认编码...
 */
```

```c
charset = getenv("CHARSET");
if (charset != NULL && strcmp(charset, "us-ascii") != 0)
{
    /* 将 HP-PCL 字符集设置为 ISO-8859-1。 */
    printf("\033(@N");
}
```

```c
/*
 * 'write_line()' - 写入一行文本。
 */
static void
write_line(int row,      /* I - 行号 (0 到 N) */
           lchar_t *line)  /* I - 要打印的行 */
{
    int    col;             /* 当前列 */
    int    attr;            /* 当前属性 */
    lchar_t *start;         /* 序列中的第一个字符 */
```

```c
for (col = 0, start = line; col < SizeColumns)
{
    while (col < SizeColumns && (line->ch == ' ' || line->ch == '_'))
    {
        col++;
        line++;
    }
    if (col >= SizeColumns)
        break;
    attr = line->attr;
    start = line;
```

```c
while (col < SizeColumns && line->ch != 0 && line->attr == attr)
{
  col++;
  line++;
}
write_string(col, (line - start), row, line - start, start);
}
```

```c
/*
 * 'write_string()' 写入一个字符串文本。
 */
static void
write_string(int col, /* I - 起列 */
  int row, /* I - 行 */
  int len, /* I - 字符数 */
  lchar_t *s) /* I - 要打印的字符串 */
{
  float x, y; /* 文本的位置 */
  unsigned int attr; /* 字符属性 */
```

```c
/* 放置文本并设置字体。 */
if (Duplex && (NumPages & 1) == 0)
{
  x = (FixedWidth - PageRight) * 10.0;
  y = (PageLength - PageTop) * 10.0;
}
else
{
  x = PageLeft * 10.0;
  y = (PageLength - PageTop) * 10.0;
}
```

```c
if (PrettyPrint)
  y += 3.0f * 720.0 / (float)LinesPerInch;
x += (float)col * 720.0 / (float)CharsPerInch;
y += (float)(row + len) * 720.0 / (float)LinesPerInch;
```

```c
attr = s->attr;
if (attr & ATTR_RASED)
    y = 360.0 / (float)LinesPerInch;
else if (attr & ATTR_LOWERED)
    y += 360.0 / (float)LinesPerInch;
printf("\033&%f");
```

# 读取位图数据

所有打印机程序都需要读取任务中每页的位图。cups 库提供了几个用于读取位图数据流的函数。表 17.2 列出了位图函数。

| 名称 |  |
| :--- | :--- |
| `cupsRasterClose()` | 关闭位图流。 |
| `cupsRasterOpen()` | 打开位图流。 |
| `cupsReadHeader()` | 从流中读取页头。 |
| `cupsRasterPixels()` | 从流中读取像素数据。 |

## 表 17.2 CUPS 位图函数

### 打开位图流

`cupsRasterOpen()` 函数初始化一个用于从过滤器读取位图数据的 `cups_raster_t` 结构：

```c
cups_raster_t *ras;
ras = cupsRasterOpen(0, CUPS_READ);
```

第一个参数指定读取的文件描述符；0 表示从标准输入读取。

第二个参数指定打开模式。使用 `CUPS_READ` 从位图流读取。

返回值为指向 `cups_raster_t` 结构的指针。

### 关闭位图流

读取位图流后，调用 `cupsRasterClose()` 释放流的内存：

```c
cups_raster_t *ras;
cupsRasterClose(ras);
```

### 读取页头

`cupsReadHeader()` 函数从位图流中读取页头：

```c
cups_raster_t *ras;
cups_page_header_t header;
...
while (cupsReadHeader(ras, &header) >= 0)
{
    /* 处理数据 */
}
```

`ras` 参数是位图指针。`header` 参数指向 `cups_page_header_t` 结构，包含关于打印页的信息。如果读取成功返回 1，文件结束或发生其他错误返回 0。

### 读取像素数据

读取页头后，可以使用 `cupsRasterPixels()` 函数读取页数据：

```c
cups_raster_t *ras;
unsigned char buffer[1024];
...
cupsRasterPixels(ras, buffer, length);
```

`ras` 参数指向位图流。`buffer` 参数指向位图数据的缓冲区。`length` 参数指定读取的字节数。返回值为读取的字节数，文件结束或出错时返回 0。

> **注意：** `cupsRasterPixels()` 函数没有进行任何检查以防止越过页数据的边界。确保你的过滤器读取的数据与页中的数据量是非常重要的。`cups_page_header_t` 结构中的 `cupsBytesPerLine` 和 `cupsHeight` 成员定义了页的标准字节大小。例外是 `cupsColorOrder` 设置为 `CUPS_ORDER_PLANAR` 的页，此时你还需要处理多个数据平面，每个颜色一个平面。

# 为 HP-PCL 程序添加抖动

CUPS 包含的示例驱动的一个问题是它们没有提供自己的抖动算法。如果你使用这些驱动打印图像，会导致质量很差。

你对惠尔-帕特程序的第二个添加是 Floyd-Steinberg 抖动算法。这种算法也被称为“蓝噪声”或“误差扩散”抖动算法。

**注意：** 抖动（或半色）是一个复杂的课题，已经有专门的关于它的著作。抖动产生点阵图案，近似你想生成的颜色或灰色调。

这里介绍的算法适用于大多数类型的打印机，但在误差扩散抖动时会产生“瀑布”效应。描述这个问题的书籍之一是 Robert Ulichney 的 *Digital Halftoning*(ISBN 0-062-261009-6)。

# 误差扩散抖动算法基础

误差扩散抖动算法通过在相邻像素之间扩散误差值来工作。误差是打印像素与原始像素之间的差异。

典型的实现维持一个所需大小的误差缓冲区，并从左到右扫描，交替行从右到左扫描。通常会在误差值上加上或乘以随机值，以提高误差扩散抖动的质量。

误差扩散抖动首先需要一个误差缓冲区。对于 HP-PCL 程序，你需要两行缓冲区，分别用于青、洋红、黄色和黑色颜色：

```c
int *ErrorBuffers[2][4];
...
SetupPage(...)
{
  ErrorBuffers[0][0] = calloc(sizeof(int), header->cupsWidth + 2);
  for (plane = 1; plane < NumPlanes; plane++)
    ErrorBuffers[0][plane] = ErrorBuffers[0][0] +
      plane * (header->cupsWidth + 2);
  ErrorBuffers[1][0] = calloc(sizeof(int), header->cupsWidth + 2);
  for (plane = 1; plane < NumPlanes; plane++)
    ErrorBuffers[1][plane] = ErrorBuffers[1][0] +
      plane * (header->cupsWidth + 2);
}
```

```c
SetupPage(...)
{
int plane;
...
Pixels[] = malloc(header->cubpsBytesPerLine);
for (plane = 1; plane < NumPlanes; plane ++)
Pixels[plane] = Pixels[0] + plane * header->cubpsBytesPerLine / NumPlanes;
}
```



## 实现 Floyd-Steinberg 算法

Floyd-Steinberg 抖动算法将误差分到四个相邻的像素上。图 17.2 显示了每个像素的布局和权重。

![](img/b159ac7fe2135643dc37ccfeef6d3980_384_0.png)

每个相邻像素都会获得误差值的部分。所有误差值之和为 1：
7/16 + 5/16 + 3/16 + 1/16 = 16/16 = 1

图 17.2

Floyd-Steinberg 误差扩散抖动。

实现此算法的新函数称为 `DitherLine()`。它为行中的每个颜色平面被调用一次。抖动代码通过计算当前误差值开始执行：

```c
/* 计算此像素的误差。 */
error = *pixels + *error / 128;
```

如果像素应该被设置，误差值大于大于 127；如果像素不应该被设置，误差值则小于 128：

```c
/* 设置抖动后的像素值（0 或 1）。 */
if (error < 128)
  *pixels = 0;
else
{
  error = 255 - error;
  *pixels = 1;
}
```

剩余的误差值通过随机量进行缩放：
/* 随机化误差值。 */
error *= (rand() % 5) + 6;

随机倍数以 8 为中心。当与 Floyd-Steinberg 的除数 16 结合时，结果是缩放 128。这与你在第一步中用于误差值除数的数值相同。

现在你已经有了缩放后的误差值，将其部分添加到相邻像素中，将总共 16 分散到 4 个像素上：

```c
/* 分散误差。 */
error[0] = 0;
error[1] += 7 * error;
error[-1] += 3 * error;
error[0] += 5 * error;
error[1] += error;
```

对行上的每个像素重复此过程。完成的 `DitherLine()` 函数在列表 17.2 中。

### 列表 17.2 新的 DitherLine() 函数

```c
void
DitherLine(unsigned char *pixels, /* IO - 行上的像素 */
             int width, /* IO - 行宽 */
             int plane, /* IO - 颜色平面 */
             int y) /* IO - 行上的当前行 */
{
  int error, /* 当前误差值 */
  int *error0, /* 指向当前误差行的指针 */
  *error1; /* 指向下一行误差行的指针 */
```

### 列表 17.2 续

```c
if (y & 1)
{
    /* 从右到左抖动。 */
    error0 = ErrorBuffers[1][plane] + width;
    error1 = ErrorBuffers[0][plane] + width;
    pixels += width - 1;
    while (width > 0)
    {
        /* 计算此像素的误差。 */
        error = *pixels + *error0 / 128;
        /* 设置抖动后的像素值（0 或 1）。 */
        if (error < 128)
            *pixels = 0;
        else
        {
            error = 255 - error;
            *pixels = 1;
        }
        /* 随机化误差值。 */
        error *= (rand() % 5) + 6;
        /* 分散误差。 */
        error0[0] += 0;
        error0[-1] += 7 * error;
        error1[1] += 3 * error;
        error1[0] += 5 * error;
        error1[-1] += error;
        /* 移动下一个像素 */
        pixels --;
        error0 --;
        error1 --;
        width --;
    }
}
else
{
    /* 从左到右抖动。 */
    error0 = ErrorBuffers[0][plane] + 1;
```

### 列表 17.2 续

## 更新 PPD 文件

现在你已经向光栅化驱动程序添加了抖动代码，你需要向现有的 PPD 文件中添加一些命令以使用新的抖动算法。

`cupsBitsPerColor` 属性指定了为每个颜色传递给驱动程序的位数。使用 PostScript `setagedevice` 命令为这些选项设置此属性：

```
<<cupsBitsPerColor bits>>setagedevice
```

其中 `bits` 是你使用的位数：1 或 8。

你可以将此内容添加到命令以扩展选项；然而，PPD 规范包含一个专门适用于该任务的 `BitsPerPixel` 选项。该选项在每个 PPD 文件中的显示如下：

- *OpenUI *BitsPerPixel: Quality*
- *Dependency: 8*
- *DefaultBitsPerPixel: 8*
- <<cupsBitsPerColor bits>>setagedevice
- *BitsPerPixel: 8
- *Output: 8
- *CloseUI *BitsPerPixel
- *High: 8
- *Order: 8
- *Any: 8
- *Order: 8
- *OpenUI *BitsPerPixel

要安装新驱动程序，首先将过滤器拷贝到：

```
cp yourfilter /usr/lib/cups
```

然后将 PPD 拷贝到：

```
cp *.ppd /usr/share/cups/
```

```
cp 过滤器拷贝到/
```

最后，使用以下命令重新添加打印机：
```
lpdadmin -p name -m filename
```

# 第 18 章

## 为 CUPS 编写后端

### 概述

后端是直接与打印机通信的特殊过滤器。后端负责与打印机的实际通信。图 18.1 显示了后端的作用。

![](img/b159ac7fe2135643dc37ccfeef6d3980_384_0.png)

图 18.1 后端在作业中的作用

### 安全考虑

后端通常以 root 用户身份运行，因此必须特别小心以避免安全违规。特别是对于运行外部程序的后端，尤其是基于脚本的后端，我们应该格外小心缓冲区溢出和后门。

### 命令行参数

除了标准的过滤器参数外，无参数运行的后端还用于获取设备列表。此发现过程在本章稍后描述。

### 页面计数

后端过滤器通常不进行页面计数；至少，当文件名存在时，它们应该为每个副本产生一个页面消息。当命令行存在文件名时，表示用户选择了“原始”打印，无法获取计数信息。

如果后端可以从打印机检索页面计数信息，它必须向调度器发送一个或多个带有“total”而不是副本数的 PAGE：

- PAGE: 15 total

### 独占访问

与本地字符设备通信的后端以独占模式（`O_EXCL`）打开设备文件，以便与同一设备的其它打印机协作。如果无法打开且错误号为 `EAGAIN` 或 `EBUSY`，后端应该睡眠一段时间，然后无限地重试 `open()` 调用：

```c
int fd;
...
{
	if ((fd = open("/dev/filename", O_RDWR | O_EXCL)) < 0)
	if (errno != EAGAIN && errno != EBUSY)
		break;
	tsleep(10);
}
while (fd < 0);
```

### 重试

所有后端必须重试设备连接。这包括与本地字符或块设备通信的后端，因为用户可能定义了指向同一物理设备的多个打印机队列。

## 注意：

字符设备和块设备与网络设备一样，都需要重试。某些本地设备可能不会立即就绪，或者在打印机上线之前不会做出响应。此外，当一个编写良好的后端使用 `O_EXCL` 选项打开本地设备时，只有在没有其他后端正在使用该设备的情况下操作才会成功。例如，当两个或多个打印队列指向同一个并行端口时。如果没有 `O_EXCL` 选项和重试机制，两个队列的输出将同时发送打印机，导致乱码。

为了防止 CPU 过度占用，后端在两次重试之间应该睡眠；CUPS 提供的后端每 10 到 30 秒重试一次。

## 剖析串口后端

串口后端后端为串口打印机提供支持。因为它执行了良好后端所需的所有工作，因此它是一个如何编写后端的优秀示例。

## 支持设备发现

如前所述，后端是与打印设备通信的特殊过滤程序。后端必须执行的另一个任务是列出它支持的设备。当命令行未提供参数时，后端会列出可用设备；例如：

```
/usr/lib/cups/backend/serial SERIAL ENTER
serial serial:dev/ttyS8baud=152200 "Unknown" "Serial Port #1"
serial serial:dev/ttyS1baud=152200 "Unknown" "Serial Port #2"
serial serial:dev/ttyS2baud=152200 "Unknown" "Serial Port #3"
serial serial:dev/ttyS3baud=152200 "Unknown" "Serial Port #4"
```

串口后端通过查找 `/dev` 目录中的串口端口、查询硬件清单（IRIX 和 Linux），以及某些情况下通过尝试打开端口来查看其实际是否存在来列出设备。

在找到串口端口后，它会为每个端口向标准错误文件写入一行。每行看起来如下：

```
class device-uri "model" "description"
```

`class` 字段识别设备类别，用于在接口中对其进行分类。。CUPS 识别以下类别：

- file. 磁盘文件。
- direct. 并行或固定速率串口数据端口，目前用于 Centronics、IEEE-1284 和 USB 打印机端口。
- serial. 可变速率串口。
- network. 网络连接，通常通过 AppSocket、HTTP、IPP、LPD 或 SMB/CIFS 协议。

`device-uri` 字段出现在 `class` 之后。该字段是用户选择端口或设备应使用的 URI。对于串口，设备 URI 末尾的 `baud=115200` 指定了端口支持的最大波特率。实际值取决于用户为打印机选择的设置。

最后两个字段是设备的模型和描述字符串。名为 `Unknown` 的模型意味着打印机型号未知；否则，设备应提供打印机的名称和型号，例如 `HP DeskJet`。这使得用户和软件能够更容易选择合适的打印机驱动程序。

`description` 字段为设备提供可读的描述，例如 `Serial Port #1.`。

## 打开串口

如之前所述，所有后端都以排他模式打开设备文件并并在需要重试直到端口可用。串口后端通过 `do-while` 循环实现此功能：

```c
int fd;
char resource[HTTP_MAX_URI];
...
do{
    if ((fd = open(resource, O_WRONLY | O_NOCTTY | O_EXCL)) == -1)
    {
        if (errno == EBUSY)
        {
            fprintf(stderr, "INFO: Serial port busy; will retry in 30 seconds...\n");
            sleep(30);
        }
        else
        {
            perror("ERROR: Unable to open serial port device file");
            return (1);
        }
    }
} while (fd < 0);
```

如果端口被占用或被另一个进程使用，后端将睡眠30 秒然后重试。如果检测到其他错误，将向用户发送消息，如果问题可以修复，后端终止打印作业。

## 向端口写入数据

网络和字符设备在后端向端口写入数据时会带来一个有趣的问题：它们在返回之前可能无法写入缓冲区中的所有字节。为了解决这个问题，你的后端必须循环直到所有字节都写入设备为止：

```c
while (nbytes > 0)
{
  if ((wbytes = write(fd, bufptr, nbytes)) <= 0)
  {
    if (wbytes < 0)
    {
      perror("ERROR: Unable to send print file to printer");
      break;
    }
  }
  nbytes -= wbytes;
  bufptr += wbytes;
}
```

在某些平台上，需要检查 `ENOTTY` 错误以清除之前 `ioctl()` 产生的错误。

## 完成工作

在后端发送打印文件后，如果文件打印成功则返回 0，如果失败则返回 1。这使得调度程序在发生设备错误时停止打印作业，保留打印作业以便在问题修复后以后打印。

## 编写基于脚本的后端

只要你注意安全，使用脚本可以是编写使用现有程序的后端的极方法。后端可以使用 Perl、Python 或 Shell 等多种语言编写。以下示例显示了一个基于 Shell 的简单串口后端。

# 第 19 章

# 为 CUPS 编写通知器

本章描述了如何为 CUPS 编写通知器，以及 mailto 通知器的工作原理。

## 什么是通知器？

通知器是通过各种协议发送 IPP 通知的程序，CUPS 为 ipp 和 mailto 协议提供了通知器程序。`ppetget` 被实现为内部方法，因为它使用了来自接收者的 HTTP 连接。

通知器是相当简单的程序，只需要读取 IPP 事件消息并发送给接收者。CUPS API 包含了读取和解码这些消息的函数。

通知和通知器支持从 CUPS 1.2 版本开始提供。

## CUPS 通知器架构

每个通知器程序都使用公共接口。通知器位于 `/usr/lib/cups/notifier` 目录，并根据需要执行以向接收者发送通知。通常每个订阅对应一个通知器。图 19.1 显示了 CUPS 通知架构。

![](img/b159ac7fe2135643dc37ccfeef6d3980_400_0.png)

图 19.1

通过 CUPS 通知器发送通知事件。

事件消息通过标准输入文件从调度器管道传输到每个通知器。状态和错误消息则从通知器的标准输出和标准错误文件管道回调度器。

调度器扫描 `/usr/lib/cups/notifier` 目录以确定可用通知方案的列表。`ipp` 方案始终可用，因为它是服务器中的内部方法。

## 命令行参数

每个通知器程序恰好提供三个命令行参数：

```bash
notifier recipient-user notify-user-data
```

`recipient-user` 参数 (`argv[1]`) 是通知的接收者；例如 `mailto:joe@foo.bar.com`。

`notify-user-data` 参数 (`argv[2]`) 提供了一个客户端在通知中所需的不透明数据字符串。为了确保这些数据不被篡改，该字符串经过 base-64 编码，并可以使用 `httpDecode()` 函数进行解码。

## 环境变量

每个通知器都会接收一组固定的环境变量，通知器可以使用它们。表 19.1 列出了这些环境变量。

表 19.1 传递给 CUPS 通知器的环境变量

| 名称 | 描述 |
|---|---|
| CHARSET | 客户端用于此打印文件使用的字符集。 |
| CLASSIFICATION | 当前的系统高级分类级别，例如“未分类."。仅在需要时提供。 |
| CUPS_DATADIR | CUPS 数据文件的位置。 |
| CUPS_SERVERROOT | CUPS 配置文件的位置。 |
| LANG | 客户端用于此打印文件使用的语言。 |
| LD_LIBRARY_PATH | 动态加载路径。仅在需要时提供。 |
| PATH | 导出到通知器的执行路径。 |
| SOFTWARE | CUPS 软件的名称，通常为 "CUPS/1.2"。 |
| TMPDIR | 临时文件的目录。 |
| TZ | 本地时区。 |
| USER | 通知器用户的名称。 |

`CLASSIFICATION` 和 `LD_LIBRARY_PATH` 环境变量只有在调度器中定义时才会被设置。`CLASSIFICATION` 环境变量对应 `Classification` 指令：

```
Classification secret
```

`LD_LIBRARY_PATH` 环境变量继承自调度器的环境变量：

```
LD_LIBRARY_PATH=/foo/bar; export LD_LIBRARY_PATH
cupsd
```



所有其他环境变量都保证在在 `cupsd.conf` 文件中另行配置的情况下存在并使用默认值。

## 读取事件数据

事件数据通过管道向标准输入文件提供。通知器使用 `ippReadFile()` 函数，然后必须读取零或多个通知消息。当遇到文件结束（EOF）或管道断开错误时，通知器应立即退出。否则，它应该无限期地读取新消息并发送通知。

## 向调度器发送消息

CUPS 调度器收集通知器发送到标准输出和标准错误文件的消息。这些消息根据调度器的 `LogLevel1` 指令存储在 `error_log` 文件中。

每条消息行带有初始前缀字符串决定了消息的类型。表 19.2 列出了可用的前缀。

### 表 19.2 CUPS 通知器的消息字符串前缀

| 前缀 | 描述 |
|---|---|
| DEBUG | 调试消息 |
| DEBUG2 | 详细的调试消息 |
| ERROR | 错误消息 |
| INFO | 信息性消息 |
| WARNING | 警告消息 |

如果文本行不是以上述任何前缀开头，则被视为 `DEBUG` 消息。

## 返回值

当没有新消息需要接收时，通知器应返回状态 0；如果发生了致命错误，则返回非零值。

> 注意：
> 如果通知器检测到向接收者发送通知时发生临时错误，它必须不要退出。只有致命错误才会触发以非零状态码退出。

## 安全考虑

通知器通常作为非特权用户运行，因此主要的安全性考虑是资源利用率——通知器不应依赖无限的处理器、内存和磁盘空间。

在从你的通知器创建或修改文件时，也应该小心。如果你需要创建临时文件，请使用 `TMPDIR` 环境变量来确定文件的存放位置。

最后，设计你的通知器以处理缓冲区溢出情况。特别是在使用 `gets()`、`sprintf()`、`strcat()` 和 `strpy()` 时要保持保守，因为这些函数通常是缓冲区溢出的源头。

> 注意：
> 如果通知器检测到向接收者发送通知时发生临时错误，它必须不要退出。只有致命错误才会触发以非零状态码退出。

## 用户和组

默认情况下，CUPS 配置以 `lp` 用户和 `other` 组运行通知器。可以使用 `cupsd.conf` 中的 `User` 和 `Group` 指令进行更改，如下：

```
User foo

Group bar
```

这些账户和组应该是非特权的以防止意外的安全风险。

## 临时文件

你应该在该目录下创建临时文件。使用 `cupsTempFile()` 和 `cupsTempFd()` 函数安全地创建临时文件。

通知器程序结束时删除临时文件，以节省磁盘空间。

## 配置和数据文件

配置文件通常存储在 `/etc/cups`。提供配置文件的通知器使用环境变量 `CUPS_SERVERROOT` 来定位文件，而不是硬编码特定目录。

通知器配置文件的规范是使用扩展名 `.conf`。例如，mailto 通知器查找名为 `mailto.conf` 文件。

同样，数据文件通常存储在 `/usr/share/cups`。环境变量 `CUPS_DATADIR` 包含了使用的目录。

## 重试

通常，通知器应该重试涉及状态更改的事件通知，但不重试“进度”消息，后者的寿命特别短。重试不应干扰读取新消息，否则可能会丢失一个或多个消息。

## 详解 mailto 通知器

mailto 通知器可能是最受欢迎且最常用的。通常使用 `lp` 或 `lr` 命令的 `-m` 来调度 mailto 通知，如下：

```bash
lp -m filename
lr -m filename
```

每个通知通过简单邮件传输协议 (SMTP) 发送给接收者。为了防止邮件滥用，只有状态更改事件会发送给接收者——否则你可能会收到作业进度更新的邮件——1%、2% 等。

通知器通过读取 `mailto.conf` 配置文件开始工作。表 19.3 列出了其中使用的配置指令。

### 表 19.3 mailto 通知器的配置指令

| 名称 | 描述 |
|---|---|
| Cc | 消息的抄送地址；用于记录所有电子邮件通知。 |
| From | 发出邮件的 From: 地址；默认为 "lp@servername.". |
| HttpServer | 邮件服务器的主机；默认为 "localhost"。 |
| Subject | 消息中 Subject: 行的前缀。 |

接下来它使用 `ippReadFile()` 函数从标准输入文件读取通知消息，如下：

```c
ipp_t *message;
ipp_state_t state;
...
doo
```

```c
{
msg = ippNew();
while ((state = ippReadFile(msg, 0)) != IPP_ERROR)
  if (state == IPP_DATA)
    break;
```

如果读取成功，通知器使用 `cupsNotifySummary()` 和 `cupsNotifyText()` 函数为接收者创建主题字符串和消息字符串：

```c
char      *subject;
char      *text;
cups_language_t *lang;
..
lang = cupsLangDefault();
...
if (state == IPP_DATA)
{
  subject = cupsNotifySubject(lang, msg);
  text = cupsNotifyText(lang, msg);
  email_message(argv[1] + 7, subject, text);
  free(subject);
  free(text);
}
```

这两个函数都接受一个 `cups_language_t` 指针用于本地化字符串，以及一个 `ipp_t` 指针用于事件消息本身。

返回值是一个指向字符串的指针，在使用后必须使用 `free()` 函数进行释放。

最后，通知器循环回读取另一条消息。当看到文件结束符 (0) 或管道破 (EPIPE) 错误时，通知器关闭并返回 0。

## 总结

通知器提供了一种让 CUPS 通知用户或程序有关服务器、打印机或作业状态变化的方法。ippet 通知方案在 CUPS 服务器内部实现，而所有其他 CUPS 通知器都是从其标准输入接收事件的外部程序。

通知器从调度程序接收消息并发送通知。每个通知器接收三个参数，包括接收者 URI 和用于订阅的数据。

CUPS 提供了几个函数来将通知消息转换为人类可读的文本。这些函数被 mailto 通知器使用，并可用于 CUPS 发行版未提供的其他文本通知方案。

# 第四部分

# 附录

- A 配置文件指令
- B IPP 引用
- C CUPS 常数
- D CUPS 结构
- E CUPS 函数
- F Common UNIX 打印系统许可协议

# 附录 A

## 配置文件指令

本附录总结了所有 CUPS 配置文件使用的配置指令。

### classes.conf

CUPS 调度程序 (`cupsd`) 使用 `classes.conf` 文件存储可用打印机类的列表。此文件仅包含本地定义的类，不包含自动创建的远程或隐含类。

#### Accepting

##### 示例

```
<Class foo>
...
Accepting yes
</Class>
<Class bar>
...
Accepting no
</Class>
```

##### 描述

`Accepting` 指令定义了 printer-is-accepting 属性的初始布尔值。此指令必须出现在 Class 或 DefaultClass 定义内部。

#### AllowUser

##### 示例

```
<Class name>
...
AllowUser foo
AllowUser bar
</Class>
```

##### 描述

`AllowUser` 指令将用户名添加到 requesting-user-name-allowed 属性中。此指令必须出现在 Class 或 DefaultClass 定义内部。

#### Class

##### 示例

```
<Class name>
...
</Class>
```

##### 描述

`class` 指令开始一个打印机类的定义。

#### DefaultClass

##### 示例

```
<DefaultClass name>
...
</Class>
```

##### 描述

`DefaultClass` 指令开始默认服务器目的地的打印机类定义。

#### DenyUser

##### 示例

```
<Class name>
...
DenyUser foo
DenyUser bar
</Class>
```

##### 描述

`DenyUser` 指令将用户名添加到 requesting-user-name-denied 属性中。此指令必须出现在 Class 或 DefaultClass 定义内部。

#### Info

##### 示例

```
<Class name>
...
Info My Class
</Class>
```

##### 描述

`Info` 指令定义了 printer-info 属性的字符串。此指令必须出现在 Class 或 DefaultClass 定义内部。

#### JobSheets

##### 描述

#### KLimit

##### 描述

#### Location

##### 示例

```
<Class name>
...
Location Building 1234
</Class>
```

##### 描述

`Location` 指令定义了 printer-location 属性的字符串。此指令必须出现在 Class 或 DefaultClass 定义内部。

#### PageLimit

##### 示例

```
<Class name>
...
PageLimit 1234
</Class>
```

##### 描述

`PageLimit` 指令定义了 job-page-limit 属性的值。此指令必须出现在 Class 或 DefaultClass 定义内部。

#### Printer

##### 示例

```
<Class name>
...
Printer foo
Printer bar
Printer foo@bar
</Class>
```

##### 描述

`Printer` 指令将打印机添加到该类中。此指令必须出现在 Class 或 DefaultClass 定义内部。

#### QuotaPeriod

##### 示例

```
<Class name>
...
QuotaPeriod 604800
</Class>
```

##### 描述

`QuotaPeriod` 指令定义了 job-quota-period 属性的值。此指令必须出现在 Class 或 DefaultClass 定义内部。

#### State

##### 示例

```
<Class foo>
...
State idle
</Class>
<Class bar>
...
State stopped
</Class>
```

##### 描述

`State` 指令定义了 printer-state 属性的初始值。`idle` 和 `stopped` 字符串对应 IPP 枚举值。此指令必须出现在 Class 或 DefaultClass 定义内部。

#### ResponseMessage

##### 示例

```
<Class name>
...
State Ready.
</Class>
```

##### 描述

`StateMessage` 指令定义了 state-message 属性（注：此处原文为 StateMessage，描述中为 StateMessage，此应对应 ResponseMessage）。此指令必须出现在 Class 或 DefaultClass 定义内部。

### client.conf

CUPS 调度程序 (`cupsd`) 使用 `client.conf` 文件定义状态。此文件必须存在。

#### Encryption

##### 示例

```
<Class name>
...
Encryption Never
</Class>
```

##### 描述

`Encryption` 指令指定默认加密设置。此指令必须出现在 Class 或 DefaultClass 定义内部。

#### ServerName

##### 示例

```
<Class name>
...
ServerName foo.com
</Class>
```

##### 描述

`ServerName` 指令设置使用的远程服务器。此指令必须出现在 Class 或 DefaultClass 定义内部。

### cupsd.conf

CUPS 调度程序 (`cupsd`) 使用 `cupsd.conf` 文件定义网络、安全和资源设置。此文件必须存在。

#### AccessLog

##### 示例

```
AccessLog /var/log/access_log
AccessLog /var/log/access_%s
AccessLog syslog
```

##### 描述

`AccessLog` 指令设置访问日志名称。如果文件名不是绝对路径，则假设相对于 ServerRoot。特殊名称 `syslog` 可将访问信息发送到系统日志而非文件。

默认访问日志为 `/var/log/access_log`。

#### Allow

##### 示例

```
Allow from All
Allow from None
Allow *.domain.com
Allow .domain.com
Allow from host.domain.com
Allow from nnn.
Allow from nnn.nnn.
Allow from nnn.nnn.nnn.
Allow from nnn.nnn.nnn/mm
Allow from nnn.nnn.nnn/mmm.mmm
```

##### 描述

`Allow` 指令指定允许访问服务器的主机、IP 地址或网络。`Allow` 指是累积的，因此可以使用多个 `Allow` 来允许多个主机。`/mm` 表示指定无类别网间路由（CIDR）掩码，如表 A.1 所示。

| mm | netmask | mm | netmask |
| :--- | :--- | :--- | :--- |
| 0 | 0.0.0.0 | 8 | 255.0.0.0 |
| 1 | 128.0.0.0 | 16 | 255.255.0.0 |
| 2 | 192.0.0.0 | 24 | 255.255.255.0 |
| ... | ... | 32 | 255.255.255.255 |

#### AuthClass

##### 示例

```
AuthClass Anonymous
AuthClass User
AuthClass System
AuthClass Group
```

##### 描述

`AuthClass` 指令定义了需要什么级别的认证。识别以下值：

- Anonymous。不执行身份验证（默认）。
- User。需要有效的用户名和密码。
- System。需要有效的用户名和密码，且用户名必须属于 "sys" 组；可以使用 `SystemGroup` 指令更改组名。
- Group。需要有效的用户名和密码，且用户名必须属于 `AuthGroupName` 指令命名的组。

`AuthClass` 指令必须出现在 Location 指令内部。

##### 注意：

`AuthClass` 指令已过时。考虑使用兼容 Apache 的 Require 指令，它提供更好的功能。

#### AuthGroupName

##### 示例

```
AuthGroupName mygroup
AuthGroupName lp
```

##### 描述

`AuthGroupName` 指令设置用于组认证的组。
`AuthGroupName` 指令必须出现在 Location 指令内部。

> 注意：
> `AuthGroup` 指令已废弃。请考虑使用与 Apache 的 Require 指令，它提供了更好的功能。

#### AuthType

##### 示例

```
AuthType None
AuthType Basic
AuthType Digest
```

##### 描述

`AuthType` 指令定义要执行的认证类型，并识别以下值：

- None. 不执行任何认证（默认值）。
- Basic. 应使用 Unix 密码文件和组文件进行基础认证。
- Digest. 应使用 `/etc/cups/passwd.md5` 文件进行摘要认证。

当使用 Basic 或 Digest 认证时，通过 localhost 接口连接的客户端也可以使用证书进行身份验证。

`AuthType` 指令必须出现在 Location 指令内部。

#### AutoPurgeJobs

##### 示例

```
AutoPurgeJobs Yes
AutoPurgeJobs No
```

##### 描述

`AutoPurgeJobs` 指令指定当完成的任务不再需要配额需要时，是否清除这些任务。

如果未启用配额，此选项将不起作用。默认设置为 No。

#### BrowseAddress

##### 示例

```
BrowseAddress 255.255.255.255:631
BrowseAddress 192.0.2.255:631
BrowseAddress host.domain.com:631
```

##### 描述

`BrowseAddress` 指令指定发送浏览信息的地址。可以指定多个 `BrowseAddress` 指令，将浏览信息发送到不同的网络或系统。

默认配置不提供广播地址。

> 注意：
> 如果你使用的是 HP-UX 且子网不是 24、16 位或 8 位，则打印机浏览（实际上是广播接收）将无法工作。

#### BrowseAllow

##### 示例

```
BrowseAllow from all
BrowseAllow from none
BrowseAllow from 192.0.2
BrowseAllow from 192.0.2.0/24
```



# BrowseAllow

## 示例

```
BrowseAllow from 192.0.2.0/255.255.255.0
BrowseAllow from *.domain.com
```

## 描述

`BrowseAllow` 指令指定接受浏览包的系统或网络。默认是接受来自所有主机的浏览包。

主机和域名匹配需要你启用 `HostNameLookups` 指令。

IP 地址匹配支持精确匹配、匹配网络掩码为 `255.0.0.0`、`255.255.0.0` 和 `255.255.255.0` 的网络的部分地址，以及具有特定网络或位数的网络地址。

# BrowseDeny

## 示例

```
BrowseDeny from all
BrowseDeny from none
BrowseDeny from 192.0.2
BrowseDeny from 192.0.2.0/24
BrowseDeny from 192.0.2.0/255.255.255.0
BrowseDeny from *.domain.com
```

## 描述

`BrowseDeny` 指令指定拒绝浏览包的系统或网络。默认是不拒绝来自任何主机的浏览包。

主机和域名匹配需要你启用 `HostNameLookups` 指令。

IP 地址匹配支持精确匹配、匹配网络掩码为 `255.0.0.0`、`255.255.0.0` 和 `255.255.255.0` 的网络的部分地址，以及具有特定网络或位数的网络地址。

# BrowseOrder

## 示例

```
BrowseOrder allow,deny
BrowseOrder deny,allow
```

## 描述

`BrowseOrder` 指令指定允许/拒绝处理的顺序。系统会识别以下设置；默认顺序为 `deny,allow`：

- `allow,deny`. 除非被特定拒绝，否则接受浏览包。
- `deny,allow`. 除非被特定允许，否则拒绝浏览包。

# BrowseInterval

## 示例

```
BrowseInterval 0
BrowseInterval 30
```

## 描述

`BrowseInterval` 指令指定浏览更新之间的最大间隔时间。指定值为 `0` 秒将禁用发出的浏览更新，但允许服务器接收来自其他主机的打印机信息。

> 注意：
`BrowseInterval` 的值应始终小于 `BrowseTimeout` 值；否则打印机和类将在更新之间从客户端系统中消失。

# BrowsePoll

## 示例

```
BrowsePoll 192.0.2.2:631
BrowsePoll host.domain.com:631
```

## 描述

`BrowsePoll` 指令每隔 `BrowseInterval` 秒轮询服务器一次可用打印机。可以指定多个 `BrowsePoll` 指令来轮询多个服务器。

如果 `BrowseInterval` 设置为 `0`，则服务器每 `30` 秒轮询一次。

# BrowsePort

## 示例

```
BrowsePort 631
BrowsePort 9999
```

## 描述

`BrowsePort` 指令指定用于浏览包的 UDP 端口号。默认端口号为 `631`。

> 注意：
你必须在所有你想看到的系统中将 `BrowsePort` 设置为相同值。

# BrowseRelay

## 示例

```
BrowseRelay 193.0.2.1 192.0.2.255
BrowseRelay 193.0.2.0/24
BrowseRelay 193.0.2.0/255.255.255.0
BrowseRelay *.domain.com
```

## 描述

`BrowseRelay` 指令指定从一个地方到另一个地方转发浏览信息的源和目的。根据需要指定多个 `BrowseRelay` 指令。这有效地提供了对局域网（LAN）打印机的访问。

# BrowseShortNames

## 示例

```
BrowseShortNames Yes
BrowseShortNames No
```

## 描述

`BrowseShortNames` 指令指定在可能的情况下是否使用短名称进行远程打印。短名称是不带服务器的远程打印机名称。如果检测到多个同名打印机，则会而改用长名称。

# BrowseTimeout

## 示例

```
BrowseTimeout 300
BrowseTimeout 60
```

## 描述

`BrowseTimeout` 指令设置浏览包接收到的打印机或类信息的超时时间。打印机或类超时后，将从可用目标列表中移除。

> 注意：
`BrowseTimeout` 的值应始终大于 `BrowseInterval` 值。否则，打印机和类将在更新之间从客户端系统中消失。

# Browsing

## 示例

```
Browsing On
Browsing Off
```

## 描述

`Browsing` 指令控制是否启用网络浏览。默认设置为 `On`。

# Deny

## 示例

```
Deny from nnn.nnn.nnn.nnn
Deny from nnn.nnn.nnn.nnn/mm
Deny from nnn.nnn.nnn.nnn/mmm.mmm.mmm.mmm
```

## Description

`Deny` 指令指定了允许访问服务器的主机名、IP 地址或网络。`Deny` 指令是累积的，因此可以使用多个 `Deny` 指令来允许多个主机或网络的访问。`/mm` 表示法指定 CIDR 网络掩码，如前面的表 A.1 所示。

`Deny` 指令必须出现在 `Location` 指令内部。

# DocumentRoot

### 示例

```
DocumentRoot /usr/share/doc/cups
DocumentRoot /foo/bar/doc/cups
```

### Description

`DocumentRoot` 指令指定了 CUPS 中 HTTP 服务器的 Web 内容的位置。如果没有指定绝对路径，则假设它相对于 `ServerRoot` 目录。默认目录为 `/usr/share/doc/cups`。

文档会首先在客户端请求的主要语言的子目录中查找（例如，法语对应 `/usr/share/doc/cups/fr/...`），然后直接在 `DocumentRoot` 目录下查找（例如，`/usr/share/doc/cups...`），因此可以通过为所需的种语言提供子目录来实现 Web 内容的本地化。

# Encryption

### 示例

```
Encryption Never
Encryption IfRequested
Encryption Required
Encryption Always
```

### Description

`Encryption` 指令必须出现在 `Location` 部分内部，并指定该位置的加密设置。所有位置的默认设置为 `IfRequested`。

注意：

由于基于位置的加密需要支持 HTTP Upgrade 协议，你必须使用 `SSLPort` 指令才能配合大多数 Web 浏览器使用加密。

# ErrorLog

### 示例

```
ErrorLog /var/log/cups/error_log
ErrorLog /var/log/cups/error_log-%s
ErrorLog syslog
```

### Description

`ErrorLog` 指令设置错误日志文件名。如果文件名是绝对路径，则假设它相对于 `ServerRoot` 目录。默认错误日志文件为 `/var/log/cups/error_log`。

要在文件名中包含服务器名称，请在名称中使用 `%s`。

特殊名称 `syslog` 可将错误信息发送到系统日志而不是普通文件。

# FilterLimit

### 示例

```
FilterLimit 0
FilterLimit 200
FilterLimit 1000
```

### Description

`FilterLimit` 指令设置所有运行作业过滤器的最大成本。它可以限制在服务器上运行的过滤器程序数量，从而最大限度地减少磁盘、内存和 CPU 资源问题。设置为 `0` 则禁用过滤器限制。

到非 PostScript 打印机的平均打印需要大约 `200` 的过滤器限制。PostScript 打印机需要大约其的一半（`100`）。

将限制设置在这些阈值以下可以限制调度器在任何时间打印单个作业。

默认限制为 `0`。

# FontPath

### 示例

```
FontPath /foo/bar/fonts
FontPath /usr/share/cups/fonts:/foo/bar/fonts
```

### Description

`FontPath` 指令指定了搜索字体时使用的字体路径。多个目录之间用冒号（`:`）隔开。默认字体路径为 `/usr/share/cups/fonts`。

# Group

### 示例

```
Group sys
Group system
Group root
```

### Description

`Group` 指令指定用于过滤器和 CGI 程序的 Unix 组。根据操作系统的，默认组为 `sys`、`system` 或 `root`。

# HostNameLookup

### 示例

```
HostNameLookups On
HostNameLookups Off
HostNameLookups Double
```

### Description

`HostNameLookups` 指令控制 CUPS 是否查找用于连接的主机名。`Double` 设置会导致 CUPS 验证从地址解析的主机名是否与该主机名返回的地址之一匹配。双重查找还可以防止未注册地址的客户端连接到你的服务器。默认值为 `Off`。

## 文件指令

注意：

主机查找会延迟处理来自客户端机器的新连接。如果你的客户端和名称服务器在小型局域网内，这种延迟可能很小。

对于较大的网络或当你允许访问互联网上的系统时，名称查找时间可能会成为严重的性能问题。

默认设置为 `Off`，以避免随主机查找的潜在服务器性能问题。仅在绝对需要时才将此选项设置为 `On` 或 `Double`。

# ImplicitClasses

### 示例

```
ImplicitClasses On
ImplicitClasses Off
```

### Description

`ImplicitClasses` 指令控制是否根据可用网络打印机和类创建隐式类。默认设置为 `On`，但如果 `Browsing` 被关闭，会自动设置为 `Off`。

# KeepAlive

### 示例

```
KeepAlive On
KeepAlive Off
```

### Description

`KeepAlive` 指令控制是否支持持久 HTTP 连接。默认值为 `On`。

注意：

HTTP/1.1 客户端自动支持持久连接，而 HTTP/1.0 客户端必须通过每个请求的 `Connection:` 字段中的 `Keep-Alive` 属性显式请求连接。

# KeepAliveTimeout

### 示例

```
KeepAliveTimeout 60
KeepAliveTimeout 30
```

### Description

`KeepAliveTimeout` 指令控制在最后一个请求后持久 HTTP 连接保持开启多长时间。默认值为 `60` 秒。

# Limit

### 示例

```
<Limit GET POST>
...
</Limit>
```

```
<Limit ALL>
...
</Limit>
```

### Description

`Limit` 指令将特定类型 HTTP 请求的访问控制指令分组，并必须出现在 `Location` 部分内部。可以对单个类型（`DELETE`, `GET`, `HEAD`, `OPTIONS`, `POST`, `PUT`, `TRACE`）或所有类型（`ALL`）限制访问。请求类型在 Apache 中是大小写敏感的。

# LimitExcept

### 示例

```
<LimitExcept GET POST>
...
</LimitExcept>
```

### Description

`LimitExcept` 指令将特定类型 HTTP 请求的访问控制指令分组。与 `Limit` 指令不同，`LimitExcept` 限制排除列表之外的所有请求的访问。

# LimitRequestBody

### 示例

```
LimitRequestBody 1048570
LimitRequestBody 10m
LimitRequestBody 0
```

### Description

`LimitRequestBody` 指令控制打印文件、IPP 请求和 POST 请求中 HTML 表单数据的限制。默认限制为 `0`，禁用限制检查。

另见 `MaxRequestSize` 指令。

# Listen

### 示例

```
Listen 127.0.0.1:631
Listen 192.0.2.1:80
Listen foo.bar.com:631
```

### Description

`Listen` 指令指定监听连接的网络地址和端口。可以提供多个 `Listen` 指令以启用监听多个地址。

`Listen` 指令与 `Port` 指令类似，但它允许你监听特定的接口或网络。

# Location

### 示例

```
<Location />
...
</Location>
<Location /admin>
...
</Location>
```

```
<Location /printers/name>
..
</Location>
```

### Description

`Location` 指令为指定的 HTTP 资源或路径指定访问控制和认证选项。`Allow`、`AuthClass`、`AuthGroupName`、`AuthType`、`Deny`、`Encryption`、`Limit`、`LimitExcept`、`Order`、`Require` 和 `Satisfy` 指令均可出现在位置内部。

# LogLevel

### 示例

```
+ Level none
LogLevel emerg
LogLevel alert
LogLevel crit
LogLevel error
LogLevel warn
LogLevel notice
LogLevel info
LogLevel debug
LogLevel debug2
```

### Description

`LogLevel` 指令指定 `ErrorLog` 文件的日志级别。每个错误级别都会记录其之前级别的所有日志。识别以下值：

+ `none`. 不记录任何日志。
+ `emerg`. 记录阻止服务器运行的紧急状况。
+ `alert`. 记录必须立即处理的警报。
+ `crit`. 记录阻止服务器运行的严重错误。
+ `error`. 记录普通错误。
+ `warn`. 记录错误和警告。
+ `notice`. 记录临时错误状况。
+ `info`. 记录所有请求和状态更改（默认值）。
+ `debug`. 记录基础调试信息。
+ `debug2`. 记录所有调试信息。

# MaxClients

## Examples

```
MaxClients 100
MaxClients 1024
```

## Description

`MaxClients` 指令控制服务器允许的最大并发客户端数量。默认值为 `100` 个客户端。

> NOTE：
由于由于每个打印作业都需要一个用于状态管道（status pipe）的文件描述符，CUPS 服务器在内部会将 `MaxClients` 的值限制为可用文件描述符的 `1/3`，以避免在大量作业正在打印时可能出现的问题。

# MaxJobs

## Examples

```
MaxJobs 100
MaxJobs 9999
MaxJobs 0
```

## Description

`MaxJobs` 指令控制保留在内存中的最大作业数量。当作业数量达到限制时，最老旧的已完成作业将自动从系统中清除，以为新作业腾出空间。如果所有已知作业仍处于等待处理或活动状态，则新作业将被拒绝。

将最大值设置为 `0` 将禁用此功能。默认设置为 `0`。

# MaxJobsPerPrinter

## Examples

```
MaxJobsPerPrinter 100
MaxJobsPerPrinter 9999
MaxJobsPerPrinter 0
```

## Description

`MaxJobsPerPrinter` 指令控制每个打印机或类别允许的最大活动作业数量。当打印机或类别达到限制时，新作业将被拒绝，直到其中一个活动作业完成、停止、中止或取消。

将最大值设置为 `0` 将禁用此功能。默认设置为 `0`。

# MaxJobsPerUser

## Examples

```
MaxJobsPerUser 100
MaxJobsPerUser 9999
MaxJobsPerUser 0
```

## Description

`MaxJobsPerUser` 指令控制每个用户允许的最大活动作业数量。当用户达到限制时，新作业将被拒绝，直到其中一个活动作业完成、停止、中止或取消。

将最大值设置为 `0` 将禁用此功能。默认设置为 `0`。

# MaxLogSize

## Examples

```
MaxLogSize 1048576
MaxLogSize 1m
MaxLogSize 0
```



# Description

`MaxLogSize` 指令控制每个日志文件的最大大小。当日志文件达到或超过最大大时，它将被重命名为 `filename.0`。这允许你自动轮转日志。默认大小为 1048576 字节（1MB）。

将最大值设置为 0 将禁用日志轮转。

# MaxRequestSize

## Examples

`MaxRequestSize 10485760`
`MaxRequestSize 10m`
`MaxRequestSize 0`

## Description

`MaxRequestSize` 指令控制打印文件、IPP 请求以及 HTTP POST 请求中 HTML 表单数据的最大大小。默认限制为 0，即禁用检查。

> NOTE：
`MaxRequestSize` 指令已废弃，并被相同的 `LimitRequestBody` 指令取代，以兼容 Apache。

# Order

## Examples

`Order Allow,Deny`
`Order Deny,Allow`

## Description

`Order` 指令定义了默认的访问控制。支持以下值：

- `Allow,Deny`。允许来自除 `Deny` 指令中列出的系统以外的所有系统的请求。
- `Deny,Allow`。仅允许来自 `Allow` 指令中列出的系统向发送的请求。

`Order` 指令必须出现在 `Location` 指令内部。

# PageLog

## Examples

```
PageLog /var/log/cups/page_log
```

```
PageLog /var/log/cups/page_log-%s
```

```
PageLog syslog
```

## Description

`PageLog` 指令设置页面日志文件的名称。如果文件名不是绝对路径，则假设它相对于 `ServerRoot` 目录。默认页面日志文件为 `/var/log/cups/page_log`。

要在文件名中包含服务器名称，请在名称中使用 `%s`。

特殊名称 `syslog` 可以将页面发送到系统日志而不是普通文件。

# Port

## Examples

```
Port 631
```

```
Port 80
```

## Description

`Port` 指令指定要监听的端口。多个 `Port` 行可以重定向到多个端口。默认端口为 631。

# PreserveJobHistory

## Examples

```
PreserveJobHistory On
```

```
PreserveJobHistory Off
```

## Description

`PreserveJobHistory` 指令控制是否将已完成、取消、中止的打印作业历史存储在磁盘上。

值 `On`（默认值）会保留作业信息，直到管理员使用 `cancel` 命令将其清除。

值 `Off` 会在每个作业完成、取消或中止后立即删除作业信息。

NOTE：

作业历史信息保存在内存中。对于具有许多队列或客户端的服务器，这些信息可能会占用服务器大量的内存并减慢调度器的启动。考虑使用 `MaxJobs` 或 `AutoPurgeJobs` 指令来限制内存中保留的旧作业数量。

# PreserveJobFiles

## Examples

`PreserveJobFiles On`
`PreserveJobFiles Off`

## Description

`PreserveJobFiles` 指令控制已完成、取消或中止的打印作业文档文件是否存储在磁盘上。

值 `on` 会保留作业文件，直到管理员使用 `cancel` 命令将其清除。在清除之前，可以根据需要重新（并重新打印）作业。

值 `off`（默认值）会在每个作业完成、取消或中止后立即删除作业文件。

如果 `PreserveJobHistory` 指令设置为 `Off`，则忽略此指令。

# Printcap

## Examples

```
Printcap
```

```
Printcap /etc/printcap
```

```
Printcap /etc/printers.conf
```

## Description

`Printcap` 指令控制是否自动生成并更新包含可用打印机列表的 printcap 文件。如果未指定值，则不生成 printcap 文件。默认生成名为 `/etc/printcap` 的文件。

当指定文件名（例如 `/etc/printcap`），每当添加或删除打印机时都会写入 printcap 文件。那些硬编码为查看 printcap 文件以获取可用打印机的应用程序可以使用。

# PrintcapFormat

## Examples

```
PrintcapFormat BSD
```

```
PrintcapFormat Solaris
```

## Description

`PrintcapFormat` 指令控制 printcap 文件的输出格式。默认生成 BSD 格式。

# RemoteRoot

## Examples

```
RemoteRoot remroot
```

```
RemoteRoot root
```

## Description

`RemoteRoot` 指令设置远程主机未身份验证请求的用户名。默认用户名为 `remroot`。将 `RemoteRoot` 设置为 `root` 实际上禁用了此安全机制。

# RequestRoot

## Examples

## Description

`RequestRoot` 指令设置用于 IPP 请求和 HTML 表单的目录。如果没有提供绝对路径，则假设它相对于 `ServerRoot` 目录。

> NOTE：
调度在启动时会更改 `RequestRoot` 目录的所有权和权限，以限制仅由 `User` 指令指定的的用户访问。

# RIPCache

## Examples

```
RIPCache 8m
```

```
RIPCache 1g
```

```
RIPCache 2048k
```

## Description

`RIPCache` 指令设置光栅图像（RIP）过滤器（如 `imagoraster` 和 `pstoraster`）缓存的内存大小。大小可以以“k”千字节、“m”或“g”字节作为后缀。

默认缓存大小为“8m”，即 8 兆字节。

# RunAsUser

## Examples

`RunAsUser Yes`
`RunAsUser No`

## Description

`RunAsUser` 指令控制调度器是否以非权限用户账户（通常为 lp）运行。默认值为 `no`，即调度器以 `root` 用户运行。

> NOTE：
以非权限用户运行可能会由于权限问题导致 LPD 和本地连接的打印机无法工作。
`lpd` 后端自动使用不100%符合 RFC 1179 的非权限模式。这种非权限模式可能不支持所有的打印机或打印服务器。
并行、串口和 USB 后端需要相应设备文件的写入权限。

# Satisfy

## Examples

`Satisfy All`
`Satisfy Any`

## Description

`Satisfy` 指令指定是否必须满足所有的 Allow/Deny、加密和要求条件才能允许访问。默认值 `All` 要求满足所有条件，而 `Any` 值则只要满足 Allow/Deny、加密或要求条件之一即可允许访问。

## ServerAdmin

### Examples

```
ServerAdmin user@host
```

```
ServerAdmin root@foo.bar.com
```

### Description

`ServerAdmin` 指令用于指定系统管理员的电子邮件地址。默认情况下，管理员电子邮件地址为 `root@server`，其中 `server` 是服务器名称。

## ServerBin

### Examples

```
ServerBin /usr/lib/cups
```

```
ServerBin /foo/bar/lib/execs
```

### Description

`ServerBin` 指令设置服务器运行的可执行文件的目录。如果未提供绝对路径，则假设它是相对于 `ServerRoot` 目录的。默认的可执行文件目录为 `/usr/lib/cups`。

## ServerCertificate

### Examples

```
ServerCertificate /etc/cups/ssl/server.crt
```

### Description

`ServerCertificate` 指令指定服务器在协商加密连接时所使用的 SSL 证书文件位置。该证书必须加密（受密码保护），因为调度程序通常在后台运行，并且无法请求密码。默认证书文件为 `/etc/cups/ssl/server.crt`。

## ServerKey

### Examples

`ServerKey /etc/cups/ssl/server.key`

### Description

`ServerKey` 指令指定服务器在协商加密连接时所使用的 SSL 私钥文件位置。默认密钥文件为 `/etc/cups/ssl/server.key`。

## ServerName

### Examples

`ServerName foo.domain.com`
`ServerName myserver.domain.com`
`ServerName 11.22.33.44`

### Description

`ServerName` 指令指定向客户端报告的主机名或 IP 地址。默认情况下，服务器名称是系统的主机名。

## ServerRoot

### Examples

`ServerRoot /etc/cups`
`ServerRoot /foo/bar/cups`

### Description

`ServerRoot` 指令指定服务器配置和状态文件的绝对路径。它还用于解析 `cupsd.conf` 文件中的相对路径。默认服务器目录为 `/etc/cups`。

## SSListen

### Examples

`SSListen 127.0.0.1:443`
`SSListen 192.0.2.1:443`
`SSListen foo.bar.com:443`

### Description

`SSListen` 指令指定用于监听安全 (HTTPS) 连接的网络地址和端口。可以提供多个 `SSListen` 指令以启用在多个地址上监听。

`SSListen` 指令与 `SSLPort` 指令类似，但它允许你在特定的接口或网络上进行监听。

## SSLPort

### Examples

`SSLPort 443`

### Description

`SSLPort` 指令指定一个用于监听安全连接的端口。可以指定多个 `SSLPort` 行以启用在多个端口上监听。

## SystemGroup

### Examples

`SystemGroup sys`
`SystemGroup system`
`GroupGroup root`

### Description

`SystemGroup` 指令指定用于系统身份验证和验证用户管理权限的系统管理组。默认系统组为 `sys`、`system` 或 `root`，取决于操作系统。

## TempDir

### Examples

`TempDir /var/spool/cups/tmp`
`TempDir /foo/bar/tmp`

### Description

`TempDir` 指令指定一个用于临时文件的绝对目录路径。默认目录为 `/var/spool/cups/tmp`。

> 注意：

临时目录必须启用“粘性”（sticky）权限，以便其他用户无法删除临时文件。虽然可以使用 world可写的临时目录，但我建议使用由 `User` 指定的用户拥有的 `/foo/bar/tmp` 私有临时目录代替。

以下命令创建一个名为 `/foo/bar/tmp` 的适当临时目录：

```
mkdir /foo/bar/tmp ENTER
```

```
own lp /foo/bar/tmp ENTER
```

```
chmod u+rwt,go-rwx /foo/bar/tmp ENTER
```

如果临时目录是 `RequestRoot` 目录的子目录，则当调度器启动时，所有权权限会自动应用到临时目录。

## Timeout

### Examples

`Timeout 300`
`Timeout 90`

### Description

`Timeout` 指令控制在活动的 HTTP IPP 请求超时之前等待的时间。默认超时时间为 300 秒。

## User

### Examples

`User lp`
`User guest`

### Description

`User` 指令指定用于过滤器和 CGI 程序的 Unix 用户账户。默认用户为 `lp`。

注意：

不要将 `user` 指令设置为 `root`。如果远程用户发现了某个过滤器或打印机驱动程序中的漏洞，他可能会以 `root` 用户身份执行任意命令或修改你系统上的文件。请始终使用非特权账户。

## mailto.conf

`mailto.conf` 文件为 `mailto` 通知器提供配置选项。

## Cc

### Examples

```
Cc root
```

```
Cc foo@bar.com
```

### Description

`cc` 指令定义了接收所有通知消息抄抄的额外地址。可以指定多个 `cc` 指令，以便将副本发送到多个地址。

## From

### Examples

```
From lp
```

```
From foo@bar.com
```

### Description

`From` 指令定义了邮件消息中的“发件人”地址。默认用户为“lp”。

## MailCommand

### Examples

`MailCommand /usr/lib/sendmail`
`MailCommand /usr/bin/mail`

### Description

`MailCommand` 指令定义了发送邮件时要执行的邮件命令。默认值为 `/usr/lib/sendmail`。

此指令与 `SMTPServer` 指令不兼容。

## ReplyTo

### Examples

`ReplyTo foo@bar.com`

### Description

`ReplyTo` 指令定义了邮件消息中的“回复”地址。默认值未定义。

## SMTPServer

### Examples

`SMTPServer localhost`
`SMTPServer foo.bar.com`

### Description

`SMTPServer` 指令定义了发送邮件时要的邮件服务器。默认值未定义。

此指令与 `MailCommand` 指令不兼容。

## pdftops.conf

`pdftops.conf` 文件为 `pdftops` 过滤器提供配置选项。

## fontmap

### Examples

`fontmap pdffont PostScript`
`fontmap Arial Helvetica`
`fontmap Arial-Bold Helvetica-Bold`

### Description

`fontmap` 指令定义了 PDF 文件中指定字体的等 字体。可以指定多个 `fontmap` 行对应多个字体。

## fontpath

### Examples

`fontpath /usr/share/cups/fonts`
`fontpath /foo/bar/fonts`

### Description

`fontpath` 指令将目录添加到字体搜索路径。

## printers.conf

CUPS 调度器 (`cupsd`) 使用 `printers.conf` 文件存储打印机列表。该文件包含本地定义的打印机，但不包含自动创建的远程打印机。

## Accepting

### Examples

```
<Printer foo>
...
Accepting yes
</Printer>
```

```
<Printer bar>
...
Accepting no
</Printer>
```

### Description

`Accepting` 指令定义了打印机接受工作的初始布尔值。该指令位于 `Printer` 或 `DefaultPrinter` 内部。

## AllowUser

### Examples

```
<Printer name>
...
AllowUser foo
AllowUser bar
</Printer>
```

### Description

`User` 指令将用户名添加到请求-用户-允许的属性中。该指令位于 `Printer` 或 `DefaultPrinter` 内部。

## DefaultPrinter

### Examples

```
<DefaultPrinter name>
...
</Printer>
```

### Description

`DefaultPrinter` 指令开始定义默认目的地的打印机定义。

## DenyUser

### Examples

```
<Printer name>
...
DenyUser foo
DenyUser bar
</Printer>
```

### Description

`DenyUser` 指令将用户名添加到请求-用户-拒绝的属性中。该指令位于 `Printer` 或 `DefaultPrinter` 内部。

## DeviceURI

### Examples

```
<Printer name>
...
DeviceURI socket://foo.bar.com:9100
</Printer>
```

### Description

`DeviceURI` 指令定义了 `device-uri` 属性的值。该指令位于 `Printer` 或 `DefaultPrinter` 内部。

## Info

### Examples

```
<Printer name>
...
Info My Printer
</Printer>
```

### Description

`Info` 指令定义了打印机-信息属性的字符串。该指令位于 `Printer` 或 `DefaultPrinter` 内部。

## JobSheets

### Examples

```
<Printer name>
...
JobSheets none,standard
</Printer>
```

## JobSheets

### Description
`JobSheets` 指令指定了在作业打印后打印的默认横幅页。该指令必须出现在 `Printer` 或 `DefaultPrinter` 定义内部。

## KLimit

### Examples
```
<Printer name>
```



## KLimit

### Examples
```
<Printer name>
...
KLimit 1234
</Printer>
```

### Description
`KLimit` 指令定义了 `job-k` 属性的值。该指令必须出现在 `Printer` 或 `DefaultPrinter` 定义内部。

## Location

### Examples
```
<Printer name>
...
Location Building 1234
</Printer>
```

### Description
`Location` 指令定义了 `printer-location` 属性的字符串。该指令必须出现在 `Printer` 或 `DefaultPrinter` 定义内部。

## PageLimit

### Examples
```
<Printer name>
...
PageLimit 1234
</Printer>
```

### Description
`PageLimit` 指令定义了 `job-page-limit` 属性的值。该指令必须出现在 `Printer` 或 `DefaultPrinter` 定义内部。

## Printer

### Examples
```
<Printer name>
...
</Printer>
```

### Description
`Printer` 指令开始一个打印机定义。

## QuotaPeriod

### Examples
```
<Printer name>
...
QuotaPeriod 604800
</Printer>
```

### Description
`QuotaPeriod` 指令定义了 `job-quota-period` 属性的值。该指令必须出现在 `Printer` 或 `DefaultPrinter` 定义内部。

## State

### Examples
```
<Printer foo>
...
State idle
</Printer>

<Printer bar>
...
State stopped
</Printer>
```

### Description
`State` 指令定义了 `printer-state` 属性的初始值。字符串 `idle` 和 `stopped` 对应于 IPP 枚举值。该指令必须出现在 `Printer` 或 `DefaultPrinter` 定义内部。

## StateMessage

### Examples
```
<Printer name>
...
StateMessage Ready to print.
</Printer>
```



### Description
`StateMessage` 指令定义了 `printer-state-message` 属性的初始字符串。该指令必须出现在 `Printer` 或 `DefaultPrinter` 定义内部。

## 附录 B

## IPP 参考

本附录列出了 IPP 操作、枚举以及对应的 CUPS 常量。

### IPP 饰工艺 (Finishings)

IPP 饰工艺常量用于 `finishings`、`finishings-default` 和 `finishings-supported` 属性。表 B.1 列出了饰工艺常量。

表 B.1 CUPS 提供的 IPP 饰工艺常量

| 名称 | 数值 | CUPS 常量 |
|---|---|---|
| none | 3 | `IPP_FINISHINGS_NONE` |
| staple | 4 | `IPP_FINISHINGS_STAPLE` |
| punch | 5 | `IPP_FINISHINGS_PUNCH` |
| cover | 6 | `IPP_FINISHINGS_COVER` |
| bind | 7 | `IPP_FINISHINGS_BIND` |
| saddle-stitch | 8 | `IPP_FINISHINGS_SADDLE_STITCH` |
| edge-stitch | 9 | `IPP_FINISHINGS_EDGE_STITCH` |
| fold | 10 | `IPP_FINISHINGS_FOLD` |
| trim | 11 | `IPP_FINISHINGS_TRIM` |
| bale | 12 | `IPP_FINISHINGS_BALE` |
| booklet-maker | 13 | `IPP_FINISHINGS_BOOKLET_MAKER` |
| job-offset | 14 | `IPP_FINISHINGS_JOB_OFFSET` |
| staple-top-left | 20 | `IPP_FINISHINGS_STAPLE_TOP_LEFT` |
| staple-bottom-left | 21 | `IPP_FINISHINGS_STAPLE_BOTTOM_LEFT` |
| staple-top-right | 22 | `IPP_FINISHINGS_STAPLE_TOP_RIGHT` |
| staple-bottom-right | 23 | `IPP_FINISHINGS_STAPLE_BOTTOM_RIGHT` |
| edge-stitch-left | 24 | `IPP_FINISHINGS_EDGE_STITCH_LEFT` |
| edge-stitch-top | 25 | `IPP_FINISHINGS_EDGE_STITCH_TOP` |
| edge-stitch-right | 26 | `IPP_FINISHINGS_EDGE_STITCH_RIGHT` |
| edge-stitch-bottom | 27 | `IPP_FINISHINGS_EDGE_STITCH_BOTTOM` |
| staple-dual-left | 28 | `IPP_FINISHINGS_STAPLE_DUAL_LEFT` |
| staple-dual-top | 29 | `IPP_FINISHINGS_STAPLE_DUAL_TOP` |
| staple-dual-right | 30 | `IPP_FINISHINGS_STAPLE_DUAL_RIGHT` |
| staple-dual-bottom | 31 | `IPP_FINISHINGS_STAPLE_DUAL_BOTTOM` |
| bind-left | 50 | `IPP_FINISHINGS_BIND_LEFT` |
| bind-top | 51 | `IPP_FINISHINGS_BIND_TOP` |
| bind-right | 52 | `IPP_FINISHINGS_BIND_RIGHT` |
| bind-bottom | 53 | `IPP_FINISHINGS_BIND_BOTTOM` |

### IPP 作业状态

IPP 作业状态常量用于 `job-state` 属性。表 B.2 列出了 CUPS 常量。

| 名称 | 数值 | CUPS 常量 |
|---|---|---|
| pending | 3 | `IPP_JOB_PENDING` |
| pending-held | 4 | `IPP_JOB_HELD` |
| processing | 5 | `IPP_JOB_PROCESSING` |
| stopped | 6 | `IPP_JOB_STOPPED` |
| canceled | 7 | `IPP_JOB_CANCELLED` |
| aborted | 8 | `IPP_JOB_ABORTED` |
| completed | 9 | `IPP_JOB_COMPLETED` |

### IPP 操作

IPP 操作常量用于 IPP 请求中的 ID。表 B.3 列出了 CUPS 常量。

| 名称 | 数值 | CUPS 常量 |
|---|---|---|
| Print-Job | 0x0002 | `IPP_PRINT_JOB` |
| Print-URI | 0x0003 | `IPP_PRINT_URI` |
| Validate-Job | 0x0004 | `IPP_VALIDATE_JOB` |
| Create-Job | 0x0005 | `IPP_CREATE_JOB` |
| Send-Document | 0x0006 | `IPP_SEND_DOCUMENT` |
| Send-URI | 0x0007 | `IPP_SEND_URI` |
| Cancel-Job | 0x0008 | `IPP_CANCEL_JOB` |
| Get-Job-Attributes | 0x0009 | `IPP_GET_ATTRIBUTES` |
| Get-Job | 0x000A | `IPP_GET_JOBS` |
| Get-Printer-Attributes | 0x000B | `IPP_GET_PRINTER_ATTRIBUTES` |
| Hold-Job | 0x000C | `IPP_HOLD_JOB` |
| Release-Job | 0x000D | `IPP_RELEASE_JOB` |
| Restart-Job | 0x000E | `IPP_RESTART_JOB` |
| Pause-Printer | 0x0010 | `IPP_PAUSE_PRINTER` |
| Resume-Printer | 0x0011 | `IPP_RESUME_PRINTER` |
| Purge-Jobs | 0x0012 | `IPP_PURGE_JOBS` |

表 B.3 续

| 名称 | 数值 | CUPS 常量 |
|---|---|---|
| Set-Printer-Attributes | 0x0013 | `IPP_SET_PRINTER_ATTRIBUTES` |
| Set-Job-Attributes | 0x0014 | `IPP_SET_JOB_ATTRIBUTES` |
| Get-Printer-Supported-Values | 0x0015 | `IPP_GET_PRINTER_SUPPORTED_VALUES` |
| Create-Printer-Subscription | 0x0016 | `IPP_CREATE_PRINTER_SUBSCRIPTION` |
| Create-Job-Subscription | 0x0017 | `IPP_CREATE_JOB_SUBSCRIPTION` |
| Get-Subscription-Attributes | 0x0018 | `IPP_GET_SUBSCRIPTION_ATTRIBUTES` |
| Get-Subscriptions | 0x0019 | `IPP_GET_SUBSCRIPTIONS` |
| Renew-Subscription | 0x01A | `IPP_RENEW_SUBSCRIPTION` |
| Cancel-Subscription | 0x001B | `IPP_CANCEL_SUBSCRIPTION` |
| Get-Notifications | 0x001C | `IPP_GET_NOTIFICATIONS` |
| Send-Notifications | 0x001D | `IPP_SEND_NOTIFICATIONS` |
| Get-Print-Support-Files | 0x0021 | `IPP_GET_PRINT_SUPPORT_FILES` |
| Enable-Printer | 0x0022 | `IPP_ENABLE_PRINTER` |
| Disable-Printer | 0x0023 | `IPP_DISABLE_PRINTER` |
| Pause-Printer-After-Current-Job | 0x0024 | `IPP_PAUSE_PRINTER_AFTER_CURRENT_JOB` |
| Hold-New-Jobs | 0x0025 | `IPP_HOLD_NEW_JOBS` |
| Release-Held-New-Jobs | 0x0026 | `IPP_RELEASE_HELD_NEW_JOBS` |
| Deactivate-Printer | 0x0027 | `IPP_DEACTIVATE_PRINTER` |
| Activate-Printer | 0x0028 | `IPP_ACTIVE_PRINTER` |
| Restart-Printer | 0x0029 | `IPP_RESTART_PRINTER` |
| Shutdown-Printer | 0x002A | `IPP_SHUTDOWN_PRINTER` |
| Startup-Printer | 0x002B | `IPP_STARTUP_PRINTER` |
| Reprocess-Job | 0x002C | `IPP_REPROCESS_JOB` |
| Cancel-Current-Job | 0x002D | `IPP_CANCEL_CURRENT_JOB` |
| Suspend-Current-Job | 0x002E | `IPP_SUSPEND_CURRENT_JOB` |
| Resume-Job | 0x002F | `IPP_RESUME_JOB` |
| Promote-Job | 0x0030 | `IPP_PROOTE_JOB` |
| Schedule-Job-After | 0x0031 | `IPP_SCHEDULE_JOB_AFTER` |
| CUPS-Get-Default | 0x0401 | `CUPS_GET_DEFAULT` |
| CUPS-Get-Printers | 0x0402 | `CUPS_GET_PRINTERS` |
| CUPS-Add-Printer | 0x0403 | `CUPS_ADD_PRINTER` |
| CUPS-Delete-Printer | 0x0404 | `CUPS_DELETE_PRINTER` |
| CUPS-Get-Classes | 0x0405 | `CUPS_GET_CLASSES` |
| CUPS-Add-Class | 0x0406 | `CUPS_ADD_CLASS` |
| CUPS-Delete-Class | 0x0407 | `CUPS_DELETE_CLASS` |
| CUPS-Accept-Jobs | 0x0408 | `CUPS_ACCEPT_JOBS` |
| CUPS-Reject-Jobs | 0x0409 | `CUPS_REJECT_JOBS` |

表 B.3 续

| 名称 | 数值 | CUPS 常量 |
|---|---|---|
| CUPS-Set-Default | 0x040A | `CUPS_SET_DEFAULT` |
| CUPS-Get-Devices | 0x040B | `CUPS_GET_DEVICES` |
| CUPS-Get-PPDs | 0x040C | `CUPS_GET_PPDs` |
| CUPS-Move-Job | 0x040D | `CUPS_MOVE_JOB` |
| CUPS-Add-Device | 0x040E | `CUPS_ADD_DEVICE` |
| CUPS-Delete-Device | 0x040F | `CUPS_DELETE_DEVICE` |

### IPP 朝向

IPP 朝向常量用于 `orientation-requested`、`orientation-default` 和 `orientation-supported` 属性。表 B.4 列出了 CUPS 常量。

表 B.4 CUPS 提供的 IPP 朝向常量

| 名称 | 数值 | CUPS 常量 |
|---|---|---|
| portrait | 3 | `IPP_PORTRAIT` |
| landscape | 4 | `IPP_LANDSCAPE` |
| reverse-landscape | 5 | `IPP_REVERSE_LANDSCAPE` |
| reverse-portrait | 6 | `IPP_REVERSE_PORTRAIT` |

### IPP 打印机状态

IPP 打印机状态常量用于 `printer-state` 属性。表 B.5 列出了 CUPS 常量。

表 B.5 IPP 打印机状态常量

| 名称 | 数值 | CUPS 常量 |
|---|---|---|
| pending | 3 | `IPP_JOB_PENDING` |
| pending-held | 4 | `IPP_JOB_HELD` |
| processing | 5 | `IPP_JOB_PROCESSING` |
| stopped | 6 | `IPP_JOB_STOPPED` |

### IPP 质量

IPP 朝向常量用于 `quality`、`quality-default` 和 `quality-supported` 属性。表 B.6 列出了 CUPS 常量。

## 表 B.6 CUPS 提供的 IPP 质量常量

| 名称 | 值 | CUPS 常量 |
|---|---|---|
| draft（草稿） | 3 | `IPP_QUALITY_DRAFT` |
| normal（普通） | 4 | `IPP_QUALITY_NORMAL` |
| high（高） | 5 | `IPP_QUALITY_HIGH` |

### IPP 分辨率单位

IPP 率常量用于所有分辨率属性的 units 成员。表 B.7 列出了 CUPS 常量。

## 表 B.7 CUPS 提供的 IPP 分辨率单位

| 名称 | 值 | CUPS 常量 |
|---|---|---|
| dots-per-inch（英寸点） | 3 | `IPP_RES_PER_INCH` |
| dots-per-centimeter（每厘米点） | 4 | `IPP_RES_PER_CM` |

### IPP 状态码

IPP 状态码常量用于 IPP 响应中的状态码。表 B.8 列出了 CUPS 常量。

## 表 B.8 CUPS 提供的 IPP 状态码常量

| 名称 | 值 | CUPS 常量 |
|---|---|---|
| successful-ok（成功） | 0x0000 | `IPP_OK` |
| successful-ok-ignored-or-substituted-attributes（成功但属性被忽略或替换） | 0x0001 | `IPP_OK_SUBST` |
| successful-ok-conflicting-attributes（成功但属性冲突） | 0x0002 | `IPP_OK_CONFLICT` |
| successful-ok-ignored-subscriptions（成功但忽略了订阅） | 0x0003 | `IPP_OK_IGNORED_SUBSCRIPTIONS` |
| successful-ok-ignored-notifications（成功但忽略了通知） | 0x0004 | `IPP_OK_IGNORED_NOTIFICATIONS` |
| successful-ok-too-many-events（成功但事件过多） | 0x0005 | `IPP_OK_TOO_MANY_EVENTS` |
| successful-ok-but-cancel-subscription（成功但取消了订阅） | 0x0006 | `IPP_OK_BUT_CANCEL_SUBSCRIPTION` |
| redirection-other-site（重定向到其他站点） | 0x0300 | `IPP_REIRECTION_OTHER_SITE` |
| client-error-bad-request（客户端错误：请求无效） | 0x0400 | `IPP_BAD_REQUEST` |
| client-error-forbidden（客户端错误：禁止访问） | 0x0401 | `IPP_FORBIDDEN` |
| client-error-not-authenticated（客户端错误：未身份） | 0x0402 | `IPP_NOT_AUTHENTICATED` |
| client-error-not-authorized（客户端错误：未授权） | 0x0403 | `IPP_NOT_AUTHORIZED` |

## 表 B.8 续

| 名称 | 值 | CUPS 常量 |
|---|---|---|
| client-error-not-possible（客户端错误：不可实现） | 0x0404 | `IPP_NOT_POSSIBLE` |
| client-error-timeout（客户端错误：超时） | 0x0405 | `IPP_TIMEOUT` |
| client-error-not-found（客户端错误：未找到） | 0x0406 | `IPP_NOT_FOUND` |
| client-error-gone（客户端错误：已永久删除） | 0x0407 | `IPP_GONE` |
| client-error-request-entity-too-large（客户端错误：请求实体过大） | 0x0408 | `IPP_REQUEST_ENTITY` |
| client-error-request-value-too-large（客户端错误：请求值过大） | 0x0409 | `IPP_REQUEST_VALUE` |
| client-error-document-format-not-supported（客户端错误：不支持文档格式） | 0x040A | `IPP_DOCUMENT_FORMAT` |
| client-error-attributes-or-values-supported（客户端错误：属性或值不支持） | 0x040B | `IPP_ATTRIBUTES` |
| client-error-uri-scheme-not-supported（客户端错误：不支持 URI 方案） | 0x040C | `IPP_URI_SCHEME` |
| client-error-charset-not-supported（客户端错误：不支持字符集） | 0x040D | `IPP_CHARSET` |
| client-error-conflicting-attributes（客户端错误：属性冲突） | 0x040E | `IPP_CONFLICT` |
| client-error-compression-not-supported（客户端错误：不支持压缩） | 0x040F | `IPP_COMPRESSION_NOT_SUPPORTED` |
| client-error-compression-error（客户端错误：压缩错误） | 0x0410 | `IPP_COMPRESSION_ERROR` |
| client-error-document-format-error（客户端错误：文档格式错误） | 0x0411 | `IPP_DOCUMENT_FORMAT_ERROR` |
| client-error-document-access-error（客户端错误：文档访问错误） | 0x0412 | `IPP_ACCESS_ERROR` |
| client-error-attributes-not-settable（客户端错误：属性不可设置） | 0x0413 | `IPP_ATTRIBUTES_NOT_SETTABLE` |
| client-error-ignored-all-subscriptions（客户端错误：忽略了所有订阅） | 0x0414 | `IPP_IGNORED_ALL_SUBSCRIPTIONS` |
| client-error-too-many-subscriptions（客户端错误：订阅过多） | 0x0415 | `IPP_TO_MANY_SUBSCRIPTIONS` |
| client-error-ignored-notifications（客户端错误：忽略了所有通知） | 0x0416 | `IPP_IGNORED_ALL_NOTIFICATIONS` |
| client-error-print-support-file-not-found（客户端错误：未找到打印支持文件） | 0x0417 | `IPP_PRINT_SUPPORT_FILE_NOT_FOUND` |
| server-error-internal-error（服务器错误：内部错误） | 0x0500 | `IPP_INTERNAL_ERROR` |
| server-error-operation-not-supported（服务器错误：不支持操作） | 0x0501 | `IPP_OPERATION_NOT_SUPPORTED` |
| server-error-service-unavailable（服务器错误：服务不可用） | 0x0502 | `IPP_SERVICE_UNAVAILABLE` |
| server-error-version-not-supported（服务器错误：不支持版本） | 0x0503 | `IPP_VERSION_NOT_SUPPORTED` |
| server-error-device-error（服务器错误：设备错误） | 0x0504 | `IPP_DEVICE_ERROR` |
| server-error-temporary-error（服务器错误：临时错误） | 0x0505 | `IPP_ARY_ERROR` |
| server-error-not-accepting-jobs（服务器错误：不再接受任务） | 0x0506 | `IPP_NOT_ACCEPTING` |
| server-error-busy（服务器错误：忙忙） | 0x0507 | `IPP_PRINTER_BUSY` |
| server-error-job-canceled（服务器错误：任务已取消） | 0x0508 | `IPP_ERROR_JOB` |
| server-error-multiple-jobs-not-supported（服务器错误：不支持多任务） | 0x0509 | `IPP_MULTIPLE_JOBS_NOT_SUPPORTED` |
| server-error-printer-is-deactivated（服务器错误：打印机已停用） | 0x050A | `IPP_PRINTER_IS_ACTIVATED` |

### IPP 标签

IPP 标签常量用于 IPP 请求和通知中的 group 和 value 标签。表 B.9 列出了 CUPS 常量。

## 表 B.9 CUPS 提供的 IPP 标签常量

| 名称 | 值 | CUPS 常量 |
|---|---|---|
| | 0x0 | `IPP_TAG_ZERO` |
| operation-attributes-tag（操作属性标签） | 0x1 | `IPP_TAG_OPERATION` |
| job-attributes-tag（任务属性标签） | 0x2 | `IPP_TAG_JOB` |
| end-of-attributes-tag（属性结束标签） | 0x3 | `IPP_TAG_END` |
| printer-attributes-tag（打印机属性标签） | 0x4 | `IPP_TAG_PRINTER` |
| unsupported-attributes-tag（不支持的属性标签） | 0x5 | `IPP_TAG_UNSUPPORTED_GROUP` |
| subscription-attributes-tag（订阅属性标签） | 0x6 | `IPP_TAG_SUBSCRIPTION` |
| event-notification-attributes-tag（事件通知属性标签） | 0x7 | `IPP_TAG_EVENT_NOTIFICATION` |
| unsupported（不支持） | 0x10 | `IPP_TAG_UNSUPPORTED_VALUE` |
| default（默认） | 0x11 | `IPP_TAG_DEFAULT` |
| unknown（未知） | 0x12 | `IPP_TAG_UNKNOWN` |
| no-value（无值） | 0x13 | `IPP_TAG_NO_VALUE` |
| not-settable（不可设置） | 0x15 | `IPP_TAG_NOT_SETABLE` |
| delete-attribute（删除属性） | 0x16 | `IPP_TAG_DELETE_ATTR` |
| admin-define（管理定义） | 0x17 | `IPP_TAG_ADMIN_DEFINE` |
| integer（整数） | 0x21 | `IPP_TAG_INTEGER` |
| boolean（布尔） | 0x22 | `IPP_TAG_BOOLEAN` |
| enum（枚举） | 0x23 | `IPP_TAG_ENUM` |
| octetString（字节字符串） | 0x30 | `IPP_TAG_STRING` |
| dateTime（日期时间） | 0x31 | `IPP_TAG_DATE` |
| resolution（分辨率） | 0x32 | `IPP_TAG_RESOLUTION` |
| rangeOfInteger（整数范围） | 0x33 | `IPP_TAG_RANGE` |
| begCollection（开始集合） | 0x34 | `IPP_TAG_BEGIN_COLLECTION` |
| textWithLanguage（带语言的文本） | 0x35 | `IPP_TAG_TEXTLANG` |
| nameWithLanguage（带语言的名称） | 0x36 | `IPP_TAG_NAMELANG` |
| endCollection（结束集合） | 0x37 | `IPP_TAG_END_COLLECTION` |
| textWithoutLanguage（不带语言的文本） | 0x41 | `IPP_TAG_TEXT` |
| nameWithoutLanguage（不带语言的名称） | 0x42 | `IPP_TAG_NAME` |
| keyword（关键字） | 0x44 | `IPP_TAG_KEYWORD` |
| uri（URI） | 0x45 | `IPP_TAG_URI` |
| uriScheme（URI 方案） | 0x46 | `IPP_TAG_URISCHEME` |
| charset（字符集） | 0x47 | `IPP_TAG_CHARSET` |
| naturalLanguage（自然语言） | 0x48 | `IPP_TAG_LANGUAGE` |
| mimeMediaType（MIME 类型） | 0x49 | `IPP_TAG_MIMATYPE` |
| memberAttrName（成员属性名） | 0x4A | `IPP_TAG_MEMBERNAME` |

## 附录 C

### CUPS 常量

本附录列出了 CUPS 头文件中提供的常量。

### 字符编码常量

字符编码常量用于 CUPS API 本地化函数。字符编码从消息文件中读取并通过 `cups_encoding_t` 类型存储在 `cups_lang_t` 结构中。表 C.1 列出了可用的字符编码。

## 表 C.1 CUPS 字符编码常量

| 名称 | 值 | 说明 |
|---|---|---|
| `CUPS_US_ASCII` | 0 | US ASCII 字符编码 |
| `CUPS_ISO8859_1` | 1 | ISO-8859-1 字符编码 |
| `CUPS_ISO8859_2` | 2 | ISO-8859-2 字符编码 |
| `CUPS_ISO8859_3` | 3 | ISO-8859-3 字符编码 |
| `CUPS_ISO8859_4` | 4 | ISO-8859-4 字符编码 |
| `CUPS_ISO8859_5` | 5 | ISO-8859-5 字符编码 |
| `CUPS_ISO8859_6` | 6 | ISO-8859-6 字符编码 |
| `CUPS_ISO8859_7` | 7 | ISO-8859-7 字符编码 |
| `CUPS_ISO8859_8` | 8 | ISO-8859-8 字符编码 |
| `CUPS_ISO8859_9` | 9 | ISO-8859-9 字符编码 |
| `CUPS_UTF8` | 10 | UTF-8 字符编码 |

### CUPS API 版本

`CUPS_VERSION` 常量将 CUPS 版本定义为浮点数：

`MM.ppp`

CUPS 版本 1.8 定义为 1.008。

### HTTP 常量

HTTP 常量定义在 `<cups/http.h>` 头文件中，用于发送 HTTP 请求。

认证

`http_auth_t` 枚举定义了多个常量，用于识别 `http_t` 结构体中 `auth_type` 成员所需的认证类型。表 C.2 列出了这些值。

## 表 C.2 HTTP 认证常量

| 名称 | 值 | 说明 |
|---|---|---|
| `HTTP_AUTH_NONE` | 0 | 无认证 |
| `HTTP_AUTH_BASIC` | 1 | 基础认证 |
| `HTTP_AUTH_MDS` | 2 | 摘要认证 |
| `HTTP_AUTH_MDS_SESS` | 3 | MD5 会话认证 |
| `HTTP_AUTH_MDS_INT` | 4 | 用于主体的摘要认证 |
| `HTTP_AUTH_MDS_SESS_INT` | 5 | 用于主体的 MD5 会话认证 |

### 编码

Content-Length 和 Transfer-Encoding 字段用于指定发送到服务器的数据长度。`http_t` 结构体的 `data_encoding` 字段指定发送请求或接收响应时使用的编码类型。表 C.3 列出了 `http_encoding_t` 枚举的支持值。

## 表 C.3 数据编码常量

| 名称 | 值 | 说明 |
|---|---|---|
| `HTTP_ENCODE_LENGTH` | 0 | 使用 Content-Length 发送 |
| `HTTP_ENCODE_CHUNKED` | 1 | 通过 Transfer-Encoding 分块传输 |

### 加密

`http_t` 结构体的 `encryption` 成员定义了连接当前的加密级别。表 C.4 列出了支持的 `http_encryption_t` 枚举值。

| 名称 | 值 | 描述 |
| --- | --- | --- |
| `HTTP_ENCRYPT_IF_REQUESTED` | 0 | 服务器通过 HTTP Upgrade 协议请求的加密。 |
| `HTTP_ENCRYPT_NEVER` | 1 | 永远不进行加密。 |
| `HTTP_ENCRYPT_REQUIRED` | 2 | 需要加密——立即通过 HTTP Upgrade 协议升级到加密。 |
| `HTTP_ENCRYPT_ALWAYS` | 3 | 始终进行加密。 |

# 字段名称

HTTP 请求和响应字段存储在 `http_t` 结构体的 `fields` 成员中。该字符串数组仅包含每个字段的值。字段本身通过 `http_field_t` 枚举进行索引，以便更高效地存储每个标准 HTTP 字段名的值。表 C.5 列出了 HTTP 字段名。

| 名称 | 值 | 描述 |
| --- | --- | --- |
| `HTTP_FIELD_UNKNOWN` | -1 | 内部用于指示未知字段名 |
| `HTTP_FIELD_ACCEPT_LANGUAGE` | 0 | Accept-Language |
| `HTTP_FIELD_ACCEPT_RANGES` | 1 | Accept-Ranges |
| `HTTP_FIELD_AUTHORIZATION` | 2 | Authorization |
| `HTTP_FIELD_CONNECTION` | 3 | Connection |
| `HTTP_FIELD_CONTENT_ENCODING` | 4 | Content-Encoding |
| `HTTP_FIELD_CONTENT_LANGUAGE` | 5 | Content-Language |
| `HTTP_FIELD_CONTENT_LENGTH` | 6 | Content-Length |
| `HTTP_FIELD_CONTENT_LOCATION` | 7 | Content-Location |
| `HTTP_FIELD_CONTENT_MDS` | 8 | Content-MD5 |
| `HTTP_FIELD_CONTENT_RANGE` | 9 | Content-Range |
| `HTTP_FIELD_CONTENT_TYPE` | 10 | Content-Type |
| `HTTP_FIELD_CONTENT_VERSION` | 11 | Content-Version |
| `HTTP_FIELD_DATE` | 12 | Date |

# 表 C.5 继续

| 名称 | 值 | 描述 |
|---|---|---|
| `HTTP_FIELD_HOST` | 13 | Host |
| `HTTP_FIELD_IF_MODIFIED_SINCE` | 14 | If-Modified-Since |
| `HTTP_FIELD_IF_UNMODIFIED_SINCE` | 15 | If-Unmodified-Since |
| `HTTP_FIELD_KEEP_ALIVE` | 16 | Keep-Alive |
| `HTTP_FIELD_LAST_MODIFIED` | 17 | Last-Modified |
| `HTTP_FIELD_LINK` | 18 | Link |
| `HTTP_FIELD_LOCATION` | 19 | Location |
| `HTTP_FIELD_RANGE` | 20 | Range |
| `HTTP_FIELD_REFERER` | 21 | Referer |
| `HTTP_FIELD_RETRY_AFTER` | 22 | Retry-After |
| `HTTP_FIELD_TRANSFER_ENCODING` | 23 | Transfer-Encoding |
| `HTTP_FIELD_UPGRADE` | 24 | Upgrade |
| `HTTP_FIELD_USER_AGENT` | 25 | User-Agent |
| `HTTP_FIELD_WWW_AUTHENTICATE` | 26 | WWW-Authenticate |
| `HTTP_FIELD_MAX` | 27 | http_t 结构中字段字符串的最大数量 |

# Keep-Alive 值

HTTP Keep-Alive 字段指定 HTTP/1.0 客户端是否支持持久连接。`http_t` 结构体的 `keep_alive` 成员指定是否应该使用 Keep-Alive。表 C.6 列出了 `http_keepalive_t` 枚举值。

# 表 C.6 HTTP Keep-Alive 常量

| 名称 | 值 | 描述 |
|---|---|---|
| `HTTP_KEEPALIVE_OFF` | 0 | 为连接不使用 HTTP Keep-Alive。 |
| `HTTP_KEEPALIVE_ON` | 1 | 为连接使用 HTTP Keep-Alive。 |

# 限制

HTTP 规范和 CUPS API 对 URI、值和缓冲区的大小实施了若干种限制。表 C.7 列出了这些限制。

# 表 C.7 CUPS API 对 HTTP 函数的限制

| 名称 | 值 | 描述 |
| --- | --- | --- |
| `HTTP_MAX_URI` | 1024 | URI 字符串的最大长度 |
| `HTTP_MAX_HOST` | 256 | 主机字符串的最大长度 |
| `HTTP_MAX_BUFFER` | 2048 | 数据缓冲区的最大长度 |
| `HTTP_MAX_VALUE` | 256 | 头部字段的最大长度 |

# 状态

`http_t` 结构体根据执行的请求维护多种状态。当前状态存储在 `state` 成员中，并定义在 `http_state_t` 枚举中。状态值以服务器为中心，但同时适用于 HTTP 客户端和服务器应用程序。表 C.8 列出了状态值。

# 表 C.8 HTTP 状态常量

| 名称 | 值 | 描述 |
| --- | --- | --- |
| `HTTP_WAITING` | 0 | 等待命令 |
| `HTTP_OPTIONS` | 1 | OPTIONS 命令等待空行 |
| `HTTP_GET` | 2 | GET 命令等待空行 |
| `HTTP_GET_SEND` | 3 | GET 命令正在发送数据 |
| `HTTP_HEAD` | 4 | HEAD 命令等待空行 |
| `HTTP_POST` | 5 | POST 命令等待空行 |
| `HTTP_POST_RECV` | 6 | POST 命令正在接收数据 |
| `HTTP_POST_SEND` | 7 | POST 命令正在发送数据 |
| `HTTP_PUT` | 8 | PUT 命令等待空行 |
| `HTTP_PUT_RECV` | 9 | PUT 命令正在接收数据 |
| `HTTP_DELETE` | 10 | DELETE 命令等待空行 |
| `HTTP_TRACE` | 11 | TRACE 命令等待空行 |
| `HTTP_CLOSE` | 12 | 关闭连接 |
| `HTTP_STATUS` | 13 | 命令发送状态 |

## 状态码

`httpUpdate()` 函数可以返回 HTTP 响应码或操作系统错误。`http_status_t` 枚举提供了所有标准状态码和一个操作系统代码。表 C.9 列出了这些值。

# 表 C.9 HTTP 状态码

| 名称 | 值 | 描述 |
| --- | --- | --- |
| `HTTP_ERROR` | -1 | 操作系统错误 |
| `HTTP_CONTINUE` | 100 | 继续处理 |
| `HTTP_SWITCH_PROTOCOLS` | 101 | HTTP 升级到 TLS/SSL |
| `HTTP_OK` | 200 | 命令成功 |
| `HTTP_CREATED` | 201 | PUT 成功 |
| `HTTP_ACCEPTED` | 202 | 已接受 |
| `HTTP_AUTHORATIVE` | 203 | 权威信息 |
| `HTTP_NO_CONTENT` | 204 | 无内容 |
| `HTTP_RESET` | 205 | 已重置 |
| `HTTP_PARTIAL_CONTENT` | 206 | 收到部分内容 |
| `HTTP_MULTIPLE_CHOICES` | 300 | 多重选择 |
| `HTTP_MOVED_PERMANENT` | 301 | 永久移动 |
| `HTTP_MOVED_TEMPORILY` | 302 | 临时移动 |
| `HTTP_SEE` | 303 | 查看其他 |
| `HTTP_NOT_MODIFIED` | 304 | 未修改 |
| `HTTP_USE_PROXY` | 305 | 使用代理 |
| `HTTP_BAD_REQUEST` | 400 | 请求错误 |
| `HTTP_UNAUTHORIZED` | 401 | 未经授权 |
| `HTTP_PAYMENT_REQUIRED` | 402 | 需要付款 |
| `HTTP_FORBIDDEN` | 403 | 禁止访问 |
| `HTTP_NOT_FOUND` | 404 | 未找到 |
| `HTTP_METHOD_NOT_ALLOWED` | 405 | 方法不允许 |
| `HTTP_NOT_ACCEPTABLE` | 406 | 不接受 |
| `HTTP_PROXY_AUTHENTICATION` | 407 | 需要代理认证 |
| `HTTP_REQUEST_TIMEOUT` | 408 | 请求超时 |
| `HTTP_CONFLICT` | 409 | 冲突 |
| `HTTP_GONE` | 410 | 资源已删除 |
| `HTTP_LENGTH_REQUIRED` | 411 | 需要内容长度或编码 |
| `HTTP_PRECONDITION_FAILED` | 412 | 前提条件失败 |
| `HTTP_REQUEST_TOO_LARGE` | 413 | 请求实体过大 |
| `HTTP_URI_TOO_LONG` | 414 | URI 过长 |
| `HTTP_UNSUPPORTED_MEDIA_TYPE` | 415 | 请求的媒体类型不支持 |
| `HTTP_UPGRADE_REQUIRED` | 426 | 需要升级到 SSL/TLS |
| `HTTP_SERVER_ERROR` | 500 | 内部错误 |
| `HTTP_NOT_IMPLEMENTED` | 501 | 功能未实现 |
| `HTTP_BAD_GATEWAY` | 502 | 网关错误 |
| `HTTP_SERVICE_UNAVAILABLE` | 503 | 服务不可用 |
| `HTTP_GATEWAY_TIMEOUT` | 504 | 网关连接超时 |
| `HTTP_NOT_SUPPORTED` | 505 | HTTP 版本不支持 |

# 版本号

每个 HTTP/1.0 和 HTTP/1.1 请求都包含一个版本号。`http_t` 结构的成员定义了发送数据时使用的 HTTP 协议。该版本以 `http_version_t` 枚举值的类型存储，以避免浮点精度问题。表 C.10 列出了支持的版本。

# 表 C.10 HTTP 协议数字常量

| 名称 | 值 | 描述 |
| --- | --- | --- |
| `HTTP_0_9` | 9 | HTTP/0.9 |
| `HTTP_1_0` | 100 | HTTP/1.0 |
| `HTTP_1_1` | 101 | HTTP/1.1 |

# IPP 常量

大部分 IPP 常量定义在附录 A IPP 常量中。本附录仅包含专门用于 CUPS 实现的常量。

# 打印机类型

`printer_type` 和 `printer_type_mask` 属性利用位值定义每个打印机或类的类型和功能。`cups_ptype_t` 枚举定义了这些位。表 C.11 列出了打印机类型常量。

# 表 C.11 打印机类型常量

| 名称 | 值 | 描述 |
| --- | --- | --- |
| `CUPS_PRINTER_LOCAL` | 0x0000 | 本地打印机或类 |
| `CUPS_PRINTER_CLASS` | 0x0001 | 打印机类 |
| `CUPS_PRINTER_REMOTE` | 0x0002 | 远程打印机或类 |
| `CUPS_PRINTER_BW` | 0x0004 | 可以黑白打印 |

# 表格 C.11 续表

| 名称 | 值 | 描述 |
| --- | --- | --- |
| `CUPS_PRINTER_COLOR` | 0x0008 | 支持彩色打印 |
| `CUPS_PRINTER_DUPLEX` | 0x0010 | 支持双面打印 |
| `CUPS_PRINTER_STAPLE` | 0x0020 | 支持输出装订 |
| `CUPS_PRINTER_COPIES` | 0x0040 | 支持复印 |
| `CUPS_PRINTER_COLLATE` | 0x0080 | 支持复印整理 |
| `CUPS_PRINTER_PUNCH` | 0x0100 | 支持输出打孔 |
| `CUPS_PRINTER_COVER` | 0x0200 | 支持输出装订 |
| `CUPS_PRINTER_BIND` | 0x0400 | 支持输出排序 |
| `CUPS_PRINTER_SORT` | 0x0800 | 支持 Letter/Legal/A4 尺寸 |
| `CUPS_PRINTER_MEDIUM` | 0x1000 | 支持 Tableau/B/C/A3/A2 |
| `CUPS_PRINTER_LARGE` | 0x2000 | 支持 D/E/A1/A0 |
| `CUPS_PRINTER_VARIABLE` | 0x4000 | 支持可尺寸 |
| `CUPS_PRINTER_IMPLICIT` | 0x8000 | 隐式类 |
| `CUPS_PRINTER_DEFAULT` | 0x10000 | 网络上的默认打印机 |
| `CUPS_PRINTER_OPTIONS` | 0xff | 除 CLASS, REMOTE, IMPLICIT 和 DEFAULT 之外的所有位 |

# 栅化常量

驱动程序和过滤器在读取或写入 CUPS 栅化数据时会使用栅化常量。所有这些常量都用于页头结构 `cups_page_header_t`。

# 布尔值

`cups_bool_t` 枚举用于表示布尔值。`CUPS_FALSE` 和 `CUPS_TRUE` 常量分别对应假 `0` 和真 `1`。

# 颜色顺序值

颜色数据按三种组织方式存储：分块 `CMYK CMYK CMYK`、带状 `CCC YYY KKK` 或平面 `CCC ... MMM ... YYY ... KKK ...`，取决于打印机和驱动程序的要求。

`cups_order_t` 枚举了这些配置的常量 `CUPS_ORDER_CHUNKED`、`CUPS_ORDER_BANDED` 和 `CUPS_ORDER_PLANAR`。

# 颜色空间

`cups_page_header_t` 结构中的 `CUPSColorSpace` 成员定义了与页面颜色相关的颜色空间。表 C.18 列出了 `cups_cspace` 枚举中的颜色空间。

## 表 C.18 颜色空间常量

| 名称 | 数值 | 说明 |
|---|---|---|
| `CUPS_CSPACE_W` | 0 | 亮度 |
| `CUPS_CSPACE_RGB` | 1 | 红绿蓝 |
| `CUPS_CSPACE_RGBA` | 2 | 红绿蓝透明通道 |
| `CUPS_CSPACE_K` | 3 | 黑色 |
| `CUPS_CSPACE_CMY` | 4 | 青品红黄 |
| `CUPS_CSPACE_YMC` | 5 | 黄品红青 |
| `CUPS_CSPACE_CMYK` | 6 | 青红黄黑 |
| `CUPS_CSPACE_CMCK` | 7 | 黄红青黑 |
| `CUPS_CSPACE_CMCY` | 8 | 黑色青黄 |
| `CUPS_CSPACE_CMYC` | 9 | 黑色青黄浅青洋红 |
| `CUPS_CSPACE_GMCK` | 10 | 金色红青黑 |
| `CUPS_CSPACE_GMCS` | 11 | 金红青银 |
| `CUPS_CSPACE_WHITE` | 12 | 白墨（作为黑色） |
| `CUPS_CSPACE_GOLD` | 13 | 金箔 |

## 表 C.18 续

| 名称 | 数值 | 说明 |
|---|---|---|
| `CUPS_SILVER` | 14 | 银箔 |
| `CUPS_ICC1` | 32 | 1 通道 ICC 颜色数据（仅限 CUPS 1.2） |
| `CUPS_CSPACE_ICC2` | 33 | 2 通道 ICC 颜色数据（仅限 CUPS 1.2） |
| `CUPS_CSPACE_ICC3` | 34 | 3 通道 ICC 颜色数据（仅限 CUPS 1.2） |
| `CUPS_CSPACE_ICC4` | 35 | 4 通道 ICC 颜色数据（仅限 CUPS 1.2） |
| `CUPS_CSPACE_ICC5` | 36 | 5 通道 ICC 颜色数据（仅限 CUPS 1.2） |
| `CUPS_CSPACE_ICC6` | 37 | 6 通道 ICC 颜色数据（仅限 CUPS 1.2） |
| `CUPS_CSPACE_ICC7` | 38 | 7 通道 ICC 颜色数据（仅限 CUPS 1.2） |
| `CUPS_CSPACE_ICC8` | 39 | 8 通道 ICC 颜色数据（仅限 CUPS 1.2） |

# 同步字

每个 CUPS 栅化文件都以 4 字节同步字开头，该字决定了文件其余字节序。CUPS 定义了两个常量：`CUPS_RASTER_SYNC` 和 `CUPS_RASTER_REVSNC`，以及反默认字节序。

同步字存储在 `cups_raster_t` 结构中，以便在从默认字节序不同的系统读取栅化流时能够自动字节交换。

# 打开模式

`cupsRasterOpen()` 函数的第二个参数是打开模式。CUPS 支持两种打开模式：`CUPS_RASTER_READ` 和 `CUPS_RASTER_WRITE`，用于读取和写入栅化流。

# 进纸值

`cups_page_header_t` 结构中的 `jog` 成员定义了对打印页的操作。它直接对应 PostScript 设备字典中的 jog 属性。表 C.19 列出了由 `cups_jog_t` 枚举定义的常量。

## 表 C.19 进纸值常量

| 名称 | 数值 | 说明 |
|---|---|---|
| `CUPS_JOG_NONE` | 0 | 不移动页面 |
| `CUPS_JOG_FILE` | 1 | 在此文件后移动页面 |
| `CUPS_JOG_JOB` | 2 | 在此任务后移动页面 |
| `CUPS_JOG_SET` | 3 | 在此组后移动页面 |

# 方向值

`cups_page_header_t` 结构中的 `Orientation` 成员定义了打印页的方向。它直接对应 PostScript 页设备字典中的 Orientation 属性，表 C.20 列出了由 `cups_orient_t` 枚举定义的常量。

## 表 C.20 方向值常量

| 名称 | 数值 | 说明 |
| --- | --- | --- |
| `CUPS_ORIENT_0` | 0 | 不旋转页面。 |
| `CUPS_ORIENT_90` | 1 | 逆时针旋转页面。 |
| `CUPS_ORIENT_180` | 2 | 将页面倒置。 |
| `CUPS_ORIENT_270` | 3 | 顺时针旋转页面。 |

# 切纸值

`cups_page_header_t` 结构中的 `CutMedia` 成员定义了打印页的切纸操作。它直接对应 PostScript 页设备字典中的 CutMedia 属性，表 C.21 列出了由 `cut_t` 枚举定义的常量。

## 表 C.21 切纸常量

| 名称 | 数值 | 说明 |
| --- |---|---|
| `CUPS_CUT_NONE` | 0 | 从不切卷。 |
| `CUPS_CUT_FILE` | 1 | 在此文件后切纸卷。 |
| `CUPS_CUT_JOB` | 2 | 在此任务后切纸卷。 |
| `CUPS_CUT_SET` | 3 | 在此组后切纸卷。 |
| `CUPS_CUT_PAGE` | 4 | 在此页后切纸卷。 |

# 进纸值

`cups_page_header_t` 结构中的 `AdvanceMedia` 成员定义了介质推进的时机。它直接对应 PostScript 页字典中的 Advance 属性，表 C.22 列出了由 `adv_t` 枚举定义的常量。

## 表 C.22 进纸常量

| 名称 | 数值 | 说明 |
| --- |---|---|
| `CUPS_ADVANCE_NONE` | 0 | 从不进纸卷。 |
| `CUPS_ADVANCE_FILE` | 1 | 在此文件后进纸卷。 |
| `CUPS_ADVANCE_JOB` | 2 | 在此任务后进纸卷。 |
| `CUPS_ADVANCE_SET` | 3 | 在此组后进纸卷。 |
| `CUPS_ADVANCE_PAGE` | 4 | 在此页后进纸卷。 |

# 领先边值

`cups_page_header_t` 结构中的 `LeadingEdge` 成员定义了首先进纸的介侧。它直接对应 PostScript 页字典中的 LeadingEdge 属性，表 C.23 列出了由 `edge_t` 枚举定义的常量。

## 表 C.23 领先边值常量

| 名称 | 数值 | 说明 |
| --- | --- | --- |
| `CUPS_EDGE_TOP` | 0 | 页面顶部。 |
| `CUPS_EDGE_RIGHT` | 1 | 页面右侧。 |
| `CUPS_EDGE_BOTTOM` | 2 | 页面底部。 |
| `CUPS_EDGE_LEFT` | 3 | 页面左侧。 |

## 附录 D

## CUPS 结构

本附录提供了 CUPS 软件提供的所有结构的详细说明。请参考附录 B 和 C 获取这些结构使用的常量。

# CUPS API 结构

CUPS API 使用以下结构处理打印服务。

### cups_dest_t

`cups_dest_t` 结构描述单个打印机实例及相关选项。

```c
```



### `cups_dest_t`

```c
typedef struct
    /* 目标 */
{
    char *name,                /* 打印机或类名 */
    *instance;          /* 实例名称或 NULL */
    int is_default;             /* 此打印机是默认的吗？ */
    int num_options;            /* 选项数量 */
    cups_option_t *options;    /* 选项 */
} cups_dest_t;
```

### `cups_job_t`

`cups_job_t` 结构描述单个打印任务。

```c
typedef struct
    /* 任务 */
{
    int id;                      /* 任务 ID */
    char *dest;                  /* 打印机或类名 */
    *title;                  /* 标题/任务名 */
    *user;                   /* 提交任务的用户 */
    *format;                 /* 文档格式 */
    ipp_job_t state;            /* 任务状态 */
    int size;                    /* 单位为KB的大小 */
    priority;                   /* 优先级 (1-100) */
    time_t completed_time,      /* 任务完成时间 */
    creation_time,          /* 任务创建时间 */
    processing_time;       /* 任务处理时间 */
} cups_job_t;
```

### `cups_lang_t`

`cups_lang_t` 结构包含 CUPS 程序的本地化消息。

```c
typedef struct cups_lang_str      /* 语言缓存 */
{
    struct cups_lang_str *next;           /* 缓存中的下一个语言 */
    int                used;               /* 使用计数 */
    cups_encoding_t encoding;              /* 文本编码 */
    char               language[16];      /* 语言/区域名称 */
    char               messages[CUPS_MSG_MAX]; /* 消息数组 */
} cups_lang_t;
```

### `cups_option_t`

`cups_option_t` 结构包含单个选项。

```c
typedef struct      /* 打印机选项 */
{
    char *name;                /* 选项名称 */
    char *value;               /* 选项值 */
    state;
} cups_option_t;
```

# HTTP 结构

HTTP 函数利用包含当前 HTTP 信息的单一数据结构。

### `http_t`

```c
// http_t 结构包含 HTTP 状态信息。
typedef struct
{
    int                fd;                 /* 此字的文件描述符 */
    int                blocking;           /* 阻塞或不阻塞 */
    int                error;              /* 读取时的上次错误 */
    time_t             activity;           /* 自上次读/写以来 */
    http_state_t       state;              /* 客户端状态 */
    http_status_t      status;             /* 上次请求状态 */
    http_version_t     version;            /* 协议版本 */
    http_keepalive_t  keep_alive;         /* 是否支持持久连接？ */
    struct sockaddr_in hostaddr;       /* 连接主机的地址 */
    char               hostname[HTTP_MAX_HOST], /* 连接主机的名称 */
                         fields[HTTP_FIELD_MAX][HTTP_MAX_VALUE]; /* 字段值 */
};
```

```c
char               *data;                  /* 指向数据缓冲区的指针 */
http_encoding_t data_encoding;      /* 是否分块(Chunked) */
int                data_remaining;      /* 字节数 */
int                               /* 缓冲区中使用的字节数 */
char               buffer[HTTP_MAX_BUFFER];/* 消息缓冲区 */
int                auth_type;             /* 用户认证类型 */
md5_state_t        md5_state;             /* MD5 状态 */
char               nonce[HTTP_MAX_VALUE];/* Nonce 值 */
int                nonce_count;           /* Nonce 计数 */
void               *tls;                   /* TLS 状态信息 */
http_encoding_t encryption;          /* 加密要求 */
} http_t;
```

## IPP 结构

IPP 函数使用了多个数据结构和类型，这些结构在所有函数调用中供 IP 状态结构使用。

### `ipp_t`

`ipp_t` 结构包含当前 IPP 请求或响应的请求/响应头、属性和状态信息。

```c
typedef struct Request State
{
    ipp_state_t      state;              /* 请求状态 */
    ipp_request_t    request;            /* 请求头 */
    ipp_attribute_t *attrs;            /* 属性 */
                    *last;               /* 列表中的最后一个属性 */
                    *current;           /* 当前属性（用于读/写） */
    ipp_tag_t        curtag;             /* 当前属性组标签 */
} ipp_t;
```

### `ipp_attribute_t`

`ipp_attribute_t` 结构包含单个属性的值。

```c
typedef struct ipp_attribute_s Attribute
{
    struct ipp_attribute_s *next;      /* 列表中的下一个属性 */
    ipp_tag_t             group_tag;      /* 业/打印机/操作组标签 */
                          value_tag;      /* 它是什么类型的值？ */
    char               *name;               /* 属性名称 */
    int                num_values;         /* 值的数量 */
    ipp_value_t        values[1];          /* 值 */
} ipp_attribute_t;
```

### `ipp_request_t`

`ipp_request_t` 结构包含 IPP 请求或响应处理器。

```c
typedef union
    Request Header
    struct{
        /* 用头 */
        ipp_uchar_t version[2];      /* 协议版本号 */
        int                op_status;   /* 操作 ID 或状态码 */
        int                request_id;  /* 请求 ID */
    } any;
    struct{
        /* 操作头 */
        ipp_uchar_t version[2];      /* 协议版本号 */
        ipp_op_t    operation_id;   /* 操作 ID */
        int         request_id;   /* 请求 ID */
    } op;
    struct{
        /* 状态头 */
        ipp_uchar_t version[2];      /* 协议版本号 */
        ipp_status_t status_code;   /* 状态码 */
        int                request_id;   /* 请求 ID */
    } status;
} ipp_request_t;
```

### `ipp_uchar_t`

`ipp_uchar_t` 类型是一个无符号 8 位整数/字符。

### `ipp_value_t`

`ipp_value_t` 联合体包含每个 IPP 值类型的成员。

```c
typedef union
    Attribute Value
{
    int                integer;      /* 整数/枚举值 */
    char                        /* 布尔值 */
    ipp_uchar_t date[11];    /* 日期/时间值 */
    struct
    {
        int                 xres,               /* 水平分辨率 */
                        yres;               /* 垂直分辨率 */
        ipp_res_t        units;              /* 分辨率单位 */
                        resolution;         /* 分辨率值 */
    }
    struct
    {
        int                 lower,             /* 下限值 */
                        upper;              /* 上限值 */
                        range;              /* 整数范围 */
    }
    struct
    {
        char                *charset;           /* 字符集 */
        char                *text;              /* 字符串 */
        string;             /* 带有语言值的字符串 */
    }
    struct
    {
        int                 length;            /* 属性长度 */
        void                *data;              /* 属性中的数据 */
                    unknown;            /* 未知属性类型 */
} ipp_value_t;
```

## PPD 结构

PPD 函数利用多个数据结构来表示 PPD 文件的内容。

### `ppd_choice_t`

`ppd_choice_t` 结构包含单个选项选择的信息。

```c
typedef struct Option choices
{
    char marked,                   /* 0 表示未选中，否则为 1 */
    choice[PPD_MAX_NAME],           /* 计算机可读的选项名称 */
    text[PPD_MAX_TEXT],             /* 人类可读的选项名称 */
    *code; /*为此选项发送的代码 */
    void *option; /* 指向父选项结构的指针 */
} ppd_choice_t;
```

### `ppd_const_t`

`ppd_const_t` 结构描述两个选项之间的约束条件。

```c
typedef struct { Constraints */
char option1[PPD_MAX_NAME], /* 第一个关键字 */
choice1[PPD_MAX_NAME], /* 第一个选项/选择 */
option2[PPD_MAX_NAME], /* 第二个关键字 */
choice2[PPD_MAX_NAME], /* 第二个选项/选择 */
} ppd_const_t;
```

### `ppd_emul_t`

`ppd_emul_t` 结构描述打印机支持的仿真器。

```c
typedef struct { Emulators */
char name[PPD_MAX_NAME]; /* 仿真器名称 */
*start, /* 开始仿真 */
*stop, /* 停止仿真 */
} ppd_emul_t;
```

### `ppd_file_t`

`ppd_file_t` 描述整个 PPD 文件。

```c
typedef struct { Files */
int language, /* 设备语言 */
color_device, /* *1 彩色设备 */
variable_sizes, /* *1 可变尺寸 */
accurate_screens, /* *1 准确网屏 */
contone_only, /* *1 连续色调 */
model_number, /* 设备型号 */
manual_copies, /* *1 手动 */
sthroughput, /* 每分钟数 */
ppd_cs_t colorspace, /* 默认色彩空间 */
char *patches; /* 发送给打印机的补丁 */
int num_emulations; /* 仿真器数量 */
ppd_emul_t *emulations; /* 仿真器及其调用代码 */
char *jcl_begin, /* JCL 命令开始 */
*jcl_ps, /* 进入 PostScript 解释器 */
*jcl_end, /* JCL 命令结束 */
*lang_encoding, /* 语言编码 */
*lang_version, /* 语言（英语等） */
*modelname, /* 型号（通用） */
*trasterizer, /* TrueType栅栅器 */
*manufacturer, /* 制造商 */
*product, /* 产品名称（来自 PS） */
*nickname, /* 昵称（特定） */
*shortnickname; /* 昵称的短版本 */
int num_groups; /* UI 组数量 */
ppd_group_t *groups; /* UI 组 */
int num_sizes; /* 页面尺寸数量 */
ppd_size_t *sizes; /* 页面尺寸 **/
float custom_min[2], /* 最小可变尺寸 */
*custom_max[2], /* 最大可变尺寸 */
*custom_margins[4]; /* 页面周围边距 **/
int num_consts; /* UI/非UI约束数量 */
ppd_const_t *consts; /* UI/非UI约束 */
int num_fonts; /* 预加载字体数量 */
char **fonts; /* 预加载字体 **/
int num_profiles; /* SRGB 色彩空间数量 */
ppd_profile_t *profiles; /* SRGB 色彩空间 */
int num_filters; /* 过滤器数量 */
char **filters; /* 过滤器字符串 **/
int flip_duplex; /* * 1 翻页 */
} ppd_file_t;
```

## 第四部分附录

### `ppd_group_t`

`ppd_group_t` 结构包含单个组的选项和信息。

```c
typedef struct ppd_group_str {
    **** Groups */
    char text[PPD_MAX_TEXT]; /* 人类可读的组名称 */
```



```c
    int num_options; /* 选项数量 */

    ppd_option_t *options; /* 选项 */

    int num_subgroups; /* 子组数量 */

    struct ppd_group_str *subgroups; /* 子组（最大深度 = 1） */

} ppd_group_t;
```

# ppd_option_t

`ppd_option_t` 结构体包含单个选项的选择和信息。

```c
**** Options ****

typedef struct {
    char            conflicted,      /* 如果存在冲突则为 1 */
    keyword[PPD_MAX_NAME],   /* 选项关键字名称 */
    defchoice[PPD_MAX_NAME],     /* 默认选项值 */
    text[PPD_MAX_TEXT];          /* 人可读文本 */
    ppd_ui_t        ui;            /* UI 选项类型 */
    ppd_section_t   section;       /* 命令所在区域 */
    float           order;         /* 顺序 */
    int             num_choices;   /* 选项数量 */
    ppd_choice_t   choices;      /* 选项选择 */
} ppd_option_t;
```

# ppd_profile_t

`ppd_profile_t` 结构体描述单个色彩配置。

```c
**** sRGB Color Profiles ****

typedef struct {
    char resolution[PPD_MAX_NAME], /* 分辨率或 "-" */
    media_type[PPD_MAX_NAME];      /* 媒体类型或 "-" */
    float density,                 /* 使用的墨水密度 */
    gamma,                          /* 使用的 Gamma 校正 */
    matrix[3][3];                   /* 变换矩阵 */
} ppd_profile_t;
```

# ppd_size_t

`ppd_size_t` 结构体描述单个页面尺寸。

```c
**** Page Sizes ****

typedef struct {
    int    marked;               /* 是否选择了该页面尺寸? */
    char name[PPD_MAX_NAME];      /* 媒体尺寸选项 */
    float width,                  /* 媒体宽度（点） */
    length,                        /* 媒体长度（点） */
    left,                          /* 左侧打印边距（点） */
    bottom,                        /* 下方打印边距（点） */
    right,                         /* 右侧打印边距（点） */
    top;                           /* 上方打印边距（点） */
} ppd_size_t;
```

# 附录 E

# CUPS 函数

本附录描述了 CUPS API 和 CUPS 库提供的函数。关于这些函数使用的常量和结构体的参考，请参阅附录 B、C 和 D。

## cupsAddDest()

### 用法

```c
int
cupsAddDest(const char *name,
               const char *instance,
               int num_dests,
               cups_dest_t **dests);
```

### 参数

| 参数 | 类型 | 描述 |
|---|---|---|
| name | const char * | 目标名称 |
| instance | const char * | 实例或 NULL |
| num_dests | int | 目标数量 |
| dests | cups_dest_t ** | 目标列表 |

### 返回值

新的目标数量。

### 描述

`cupsAddDest()` 函数向目标数组添加一个目标。如果该目标已存在，则不会添加。

### 示例

```c
#include <cups/cups.h>

...

int num_dests;
cups_dest_t *dests;

...
```

`num_dests = cupsAddDest("myprinter", "myinstance", num_dests, &dests);`
``` 

### 另

`cupsFreeDests()`, `cupsGetDest()`, `cupsGetDests()`, `cupsSetDests()`

## cupsAddOption()

### 用法
```c
int
cupsAddOption(const char *name,
               const char *value,
               int num_options,
               cups_option_t **options);
```

### 参数

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| name | const char * | 选项名称 |
| value | const char * | 选项值 |
| num_options | int | 数组中的选项数量 |
| options | cups_option_t ** | 指向选项数组的指针 |

### 返回值

新的选项数量。

### 描述

`cupsAddOption()` 函数向指定的数组添加一个选项。

### 示例
```c
#include <cups.h>
...
/* 声明选项数组 */
int num_options;
cups_option_t *options;

/* 初始化选项数组 */
num_options = 0;
options = (cups_option_t *)0;
```

### 第四部分 附录
```c
/* 使用 cupsAddOption() 添加选项 */
num_options = cupsAddOption("media", "letter", num_options, &options);
num_options = cupsAddOption("resolution", "300dpi", num_options, &options);
```

### 另

`cupsFreeOptions()`, `cupsGetOption()`, `cupsParseOptions()`

## cupsCancelJob()

### 用法
```c
int
cupsCancelJob(const char *dest,
    int job);
```

### 参数

| 参数 | 类型 | 描述 |
|---|---|---|
| dest | const char * | 打印机或类名 |
| job | int | 任务 ID |

### 返回值

成功返回 1，失败返回 0。失败时可以通过调用 `cupsLastError()` 找到错误。

### 描述

`cupsCancelJob()` 函数取消指定的任务。

### 示例
```c
#include <cups.h>

cupsCancelJob("LaserJet", 1);
```

### 另

`cupsLastError()`, `cupsFile()`

## cupsDoFile()

### 用法
```c
ipp_t *cupsDoFile(ipp_t *http,
    const char *resource,
    const char *filename);
```

### 参数

| 参数 | 类型 | 描述 |
| --- | --- |
| http | ipp_t * | HTTP 连接 |
| resource | const char * | 资源名称 |
| filename | const char * | 文件 |

### 返回值

IPP 响应或 NULL。

### 描述

`cupsDoFile()` 函数发送 HTTP 请求并提供 IPP 请求。

### 示例
```c
#include <cups.h>

ipp_t      http;
cups_lang_t *language;
ipp_t       *request;
...
/* 获取默认语言 */
language = cupsLangDefault();

/* 创建一个新的 IPP 请求 */
request = ippNew();

request->op.operation_id = IPP_GET_ATTRIBUTES;

/* 添加属性 */
ippAddString(request, IPP_CHARSET,
    "attributes-charset", NULL, cupsEncoding(language));

ippAddString(request, IPP_LANGUAGE,
    "attributes-natural-language", NULL,
language != NULL ? language : "C");

ippAddString(request, IPP_URI,
    "printer-uri", NULL,":hostname/resource");

/* 执行请求... */
response = cupsDoRequest(http, request, "/resource");
```

### 另

`cupsLangDefault()`, `cupsLangEncoding()`, `cupsUser()`, `httpConnect()`, `ippAddString()`, `ippNew()`

## cupsDoRequest()

### 用法
```c
ipp_t *cupsDoRequest(ipp_t *http,
    ipp_t *request,
    const char *resource);
```

### 参数

| 参数 | 类型 | 描述 |
|---|---|---|
| http | ipp_t * | HTTP 连接 |
| request | ipp_t * | IPP 请求 |
| resource | const char * | 资源名称 |

### 返回值

IPP 响应，如果请求失败则返回 NULL。失败时可以通过 `cupsLastError()` 找到错误。

### 描述

`cupsDoRequest()` 函数发送 HTTP 请求并提供 IPP 请求。它还处理请求提交。

## cupsAddRequestOptions()

### 参数

| 参数 | 类型 | 描述 |
| ---|---|---|
| request | ipp_t * | IPP 请求 |
| num_options | int | 数组中的选项数量 |
| options | cups_option_t * | 指向选项数组的指针 |

## cupsEncodeOptions()

### 用法
```c
void cupsEncodeOptions(ipp_t *request, int num_options, cups_option_t *options);
```

### 描述

`cupsEncodeOptions()` 函数将数组中的选项添加到指定的 IPP 请求中。

### 示例
```c
#include <cups/cups.h>
...
ipp_t *request;
int num_options;
cups_option_t *options;
...
cupsEncodeOptions(request, num_options, options);
```

### 另请

`cupsAddOption()`, `cupsGetOption()`, `cupsMarkOptions()`, `cupsParseOptions()`

## cupsEncryption()

### 用法
```c
http_encryption_t
cupsEncryption(void);
```

### 描述

`cupsEncryption()` 函数返回当前的默认加密模式。

### 示例
```c
#include <cups/cups.h>

printf("Default encryption = %d\n", cupsEncryption());
```

### 另请

`cupsSetEncryption()`, `httpConnectEncrypt()`, `httpEncryption()`

## cupsFreeDests()

### 用法
```c
void
cupsFreeDests(int num_dests,
cups_dest_t *dests);
```

### 参数

| 参数 | 类型 | 描述 |
|---|---|---|
| num_dests | int | 数组中的目的数量 |
| dests | cups_dest_t * | 指向数组的指针 |

### 描述

`cupsFreeDest()` 函数释放与指定目的数组相关的所有内存。

### 示例
```c
#include <cups/cups.h>

int num_dests;
cups_dest_t *dests;
...
cupsFreeDests(num_dests, dests);
```

### 另请

`cupsAddDest()`, `cupsGetDest()`, `cupsGetDests()`, `cupsSetDests()`

## cupsFreeJobs()

### 用法
```c
void cupsFreeJobs(int num_jobs, cups_job_t *jobs);
```

### 参数

| 参数 | 类型 | 描述 |
| num_jobs | int | 数组中的任务数量 |
| jobs | cups_job_t * | 指向任务数组的指针 |

### 描述

`cupsFreeJobs()` 函数释放与指定任务数组相关的所有内存。

### 示例
```c
#include <cups/cups.h>

int num_jobs;

cups_job_t *jobs;
...
cupsFreeJobs(num_jobs, jobs);
```

### 另请

`cupsGetJobs()`

## cupsFreeOptions()

### 用法
```c
void
cupsFreeOptions(int num_options,
cups_option_t *options);
```

### 参数

| 参数 | 类型 | 描述 |
| num_options | int | 数组中的选项数量 |
| options | cups_option_t * | 指向选项数组的指针 |

### 描述

`cupsFreeOptions()` 函数释放与指定选项数组相关的所有内存。

### 示例
```c
#include <cups/cups.h>
int num_options;
cups_option_t *options;
...
cupsFreeOptions(num_options, options);
```

### 另请

`cupsAddOption()`, `cupsGetOption()`, `cupsMarkOptions()`, `cupsParseOptions()`

## cupsGetClasses()

### 用法
```c
int
cupsGetClasses(char ***classes);
```

### 参数

| 参数 | 类型 | 描述 |
|---|---|---|
| classes | char *** | 指向字符指针数组指针的指针 |

### 返回

可用打印机类的数量。

### 描述

`cupsGetClasses()` 函数获取可用打印机类的列表。当不再需要时，应使用 `free()` 函数来释放返回的数组。

### 示例
```c
#include <cups/cups.h>

int i;
int num_classes;
char **classes;
...
num_classes = cupsGetClasses(
...
if (num_classes > 0)
{
    for (i = 0; i < num_classes; i ++)
free(classes[i]);

free(classes);
}
```

### 另请

`cupsGetDefault()`, `cupsGetPrinters()`

## cupsGetDefault()

### 用法
```c
const char *
cupsGetDefault(void);
```

### 返回

指向默认目的的指针。

### 描述

`cupsGetDefault()` 函数获取默认目的打印机或类。默认目的存储在静态字符串中，并在每次调用后会被重写（通常为相同的值）。

### 示例
```c
#include <cups/cups.h>

printf("The default destination is %s\n", cupsGetDefault());
```

### 另请

`cupsGetClasses()`, `cupsGetPrinters()`

## cupsGetDest()

### 用法
```c
cups_dest_t *
cupsGetDest(const char *name,
const char *instance,
int num_dests,
cups_dest_t *dests);
```

| 参数 | 类型 | 描述 |
| --- | --- | --- |



| name | `const char *` | 目的名称，或为 `NULL` 表示默认目的 |
| instance | `const char *` | 实例名称或 `NULL` |
| num_dests |  | 数组中的目的数量 |
| dests | `cups_dest_t *` | 目的数组 |

# 返回

指向目的的指针；如果未定义目的则返回 `NULL`。

# 描述

`cupsDest()` 函数返回命名的目的。目的名称可以为 `NULL` 指针以获取默认目的。实例名称可以为 `NULL` 指针以获取基础目的。

# 示例

```c
#include <cups.h>

int num_dests;
cups_dest_t *dests;
cups_dest_t *dest;

...
dest = cupsGetDest(NULL, NULL, num_dests, dests);

if (dest)
    printf("Default destination is %s%s.\n", dest->name,
           dest->instance ? " //" : "");
```

# 另请

`cupsAddOption()`, `cupsGetOption()`, `cupsMarkOptions()`, `cupsParseOptions()`

# cupsFreeDest()

## 用法

```c
void cupsFreeDest(int num_dests, cups_dest_t *dests);
```

| 参数 | 类型 | 描述 |
|---|---|---|
| num_dests | `int` | 数组中的目的数量 |
| dests | `cups_dest_t *` | 指向目的数组的指针 |

## 描述

`cupsFreeDest()` 函数释放与指定目的数组相关的所有内存。

## 示例

```c
#include <cups/cups.h>

int num_dests;
cups_dest_t *dests;
...
cupsFreeDests(num_dests, dests);
```

## 另请

`cupsAddDest()`, `cupsGetDest()`, `cupsGetDests()`, `cupsSetDests()`

# cupsFreeJobs()

## 用法

```c
void cupsFreeJobs(int num_jobs, cups_job_t *jobs);
```

## 参数

| 参数 | 类型 | 描述 |
| num_jobs | `int` | 数组中的任务数量 |
| jobs | `cups_job_t *` | 指向任务数组的指针 |

## 描述

`cupsFreeJobs()` 函数释放与指定任务数组相关的所有内存。

## 示例

```c
#include <cups/cups.h>

int num_jobs;

cups_job_t *jobs;
...
cupsFreeJobs(num_jobs, jobs);
```

## 另请

`cupsGetJobs()`

# cupsFreeOptions()

## 用法

```c
void
cupsFreeOptions(int num_options,
cups_option_t *options);
```

## 参数

| 参数 | 类型 | 描述 |
| num_options | `int` | 数组中的选项数量 |
| options | `cups_option_t *` | 指向选项数组的指针 |

## 描述

`cupsFreeOptions()` 函数释放与指定选项数组相关的所有内存。

## 示例

```c
#include <cups/cups.h>
int num_options;
cups_option_t *options;
...
cupsFreeOptions(num_options, options);
```

## 另请

`cupsAddOption()`, `cupsGetOption()`, `cupsMarkOptions()`, `cupsParseOptions()`

# cupsGetClasses()

## 用法

```c
int
cupsGetClasses(char ***classes);
```

## 参数

| 参数 | 类型 | 描述 |
|---|---|---|
| classes | `char ***` | 指向字符指针数组指针的指针 |

## 返回

可用打印机类的数量。

## 描述

`cupsGetClasses()` 函数获取可用打印机类的列表。当不再需要时，应使用 `free()` 函数来释放返回的数组。

## 示例

```c
#include <cups/cups.h>

int i;
int num_classes;
char **classes;
...
num_classes = cupsGetClasses(
...
if (num_classes > 0)
{
    for (i = 0; i < num_classes; i ++)
free(classes[i]);

free(classes);
}
```

## 另请

`cupsGetDefault()`, `cupsGetPrinters()`

# cupsGetDefault()

## 用法

```c
const char *
cupsGetDefault(void);
```

## 返回

指向默认目的的指针。

## 描述

`cupsGetDefault()` 函数获取默认目的打印机或类。默认目的存储在静态字符串中，并在每次调用后会被重写（通常为相同的值）。

## 示例

```c
#include <cups/cups.h>

printf("The default destination is %s\n", cupsGetDefault());
```

## 另请

`cupsGetClasses()`, `cupsGetPrinters()`

# cupsGetDest()

## 用法

```c
cups_dest_t *
cupsGetDest(const char *name,
const char *instance,
int num_dests,
cups_dest_t *dests);
```

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| name | `const char *` | 目的名称，或为 `NULL` 表示默认目的 |
| instance | `const char *` | 实例名称或 `NULL` |
| num_dests |  | 数组中的目的数量 |
| dests | `cups_dest_t *` | 目的数组 |

## 返回

指向目的的指针；如果未定义目的则返回 `NULL`。

## 描述

`cupsDest()` 函数返回命名的目的。目的名称可以为 `NULL` 指针以获取默认目的。实例名称可以为 `NULL` 指针以获取基础目的。

## 示例

```c
#include <cups.h>

int num_dests;
cups_dest_t *dests;
cups_dest_t *dest;

...
dest = cupsGetDest(NULL, NULL, num_dests, dests);

if (dest)
    printf("Default destination is %s%s.\n", dest->name,
           dest->instance ? " //" : "");
```

## 另请

`cupsAddOption()`, `cupsGetOption()`, `cupsMarkOptions()`, `cupsParseOptions()`

# 描述

`cupsGetPrinters()` 函数获取可用打印机列表。当返回的数组不再需要时，应使用 `free()` 函数来释放它。

# 示例

```c
#include <cups/cups.h>

int i;

int num_printers;

char **printers;

...

num_printers = cupsGetPrinters(

...

if (num_printers > 0)

{

  for (i = 0; i < num_printers; i ++)

    free(printers[i]);

}

free(printers);
```



# cupsLangDefault()

## 另见
`cupsGetClasses()`, `cupsGetDefault()`

## 使用

```c
const char *
cupsLangDefault(void);
```

## 返回
一个指向默认语言结构的指针。

## 描述
`cupsLangDefault()` 返回默认语言的语言结构。默认语言由 `LANG` 环境变量定义。如果无法找到指定的语言，则使用 POSIX（英语）区域设置。

完成后，调用 `cupsLangFree()` 来释放与语言结构相关的任何内存。

## 示例

```c
#include <cups/language.h>

cups_lang_t *language;

...

language = cupsLangDefault();

...

cupsLangFree(language);
```

## 另见
`cupsLangEncoding()`, `cupsLangFlush()`, `cupsLangFree()`, `cupsLangGet()`, `cupsLangString()`

# cupsLangEncoding()

## 使用

```c
char * cupsLangEncoding(cups_lang_t *language);
```

## 参数

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| language | `cups_lang_t *` | 语言结构 |

## 返回
一个指向编码字符串的指针。

## 描述
`cupsLangEncoding()` 函数返回用于指定语言的语言编码，例如 `"iso-8859-1"` `"utf-8"` 等。

## 示例

```c
#include <cups/language.h>

cups_lang_t *language;

char *encoding;

...

language = cupsLangDefault();

encoding = cupsLangEncoding(language);

...

cupsLangFree(language);
```

## 另见
`cupsLangDefault()`, `cupsLangFlush()`, `cupsLangFree()`, `cupsLangGet()`, `cupsLangString()`

# cupsLangFlush()

## 使用

```c
void
cupsLangFlush(void);
```

## 描述
`cupsLangFlush()` 函数释放所有已分配的语言结构。

## 示例

```c
#include <cups/language.h>

...

cupsLangFlush();
```

## 另见
`cupsLangDefault()`, `cupsLangEncoding()`, `cupsLangFree()`, `cupsLangGet()`, `cupsLangString()`

# cupsLangFree()

## 使用

```c
void
cupsLangFree(cups_lang_t *language);
```

## 参数

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| language | `cups_lang_t *` | 要释放的语言结构 |

## 描述
`cupsLangFree()` 函数释放指定的语言结构。

## 示例

```c
#include <cups/language.h>

cups_lang_t *language;

...

cupsLangFree(language);
```

## 另见
`cupsLangDefault()`, `cupsLangEncoding()`, `cupsLangFlush()`, `cupsLangGet()`, `cupsLangString()`

# cupsLangGet()

## 使用

```c
cups_lang_t *
cupsLangGet(const char *name);
```

## 参数

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| name | `const char *` | 区域设置名称 |

## 返回
一个指向语言结构的指针。

## 描述
`cupsLangGet()` 函数返回指定区域设置的语言结构。如果未定义区域设置，则替换为 POSIX（英语）区域设置。

## 示例

```c
#include <cups/language.h>

cups_lang_t *language;

...

language = cupsLangGet("fr");

...

cupsLangFree(language);
```

## 另见
`cupsLangDefault()`, `cupsLangEncoding()`, `cupsLangFlush()`, `cupsLangFree()`, `cupsLangString()`

# cupsLangString()

## 使用

```c
char *
cupsLangString(cups_lang_t *language,
cups_msg_t message);
```

## 参数

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| language | `cups_lang_t *` | 要查询的语言 |
| message | `cups_msg_t` | 消息编号 |

## 返回
一个指向消息字符串的指针，如果消息未定义则返回 NULL。

## 描述
`cupsLangString()` 函数返回指定语言中的指定消息字符串指针。

## 示例

```c
#include <cups/language.h>

cups_lang_t *language;

char *s;

...

language = cupsLangGet("fr");

s = cupsLangString(language, CUPS_MSG_YES);

...

cupsLangFree(language);
```

## 另见
`cupsLangDefault()`, `cupsLangEncoding()`, `cupsLangFlush()`, `cupsLangFree()`, `cupsLangGet()`

# cupsLastError()

## 使用

```c
ipp_status_t
cupsLastError(void);
```

## 返回
一个包含最后一个 IPP 错误的枚举。

## 描述
`cupsLastError()` 函数返回最后发生的 IPP 错误。如果没有发生过错误，则返回 `IPP_OK` 或 `IPP_OK_CONFLICT`。

## 示例

```c
#include <cups/cups.h>

ipp_status_t status;

status = cupsLastError();
```

## 另见
`cupsCancelJob()`, `cupsPrintFile()`

# cupsPrintFile()

## 使用

```c
int
cupsPrintFile(const char *printer,
              const char *filename,
              const char *title,
              int      num_options,
              cups_option_t *options);
```

## 参数

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| printer | `const char *` | 打印机或类 |
| filename | `const char *` | 要打印的文件 |
| title | `const char *` | 任务标题 |
| num_options | `int` | 选项数量 |
| options | `cups_option_t *` | 选项 |

# cupsRasterClose()

## 参数

| 参数 | 类型 | 描述 |
| :--- | :--- | :--- |
| ras | `cups_raster_t *` | 要关闭的光栅流 |

## 描述
`cupsRasterClose()` 函数关闭指定的光栅流。

## 示例

```c
#include <cups/raster.h>

cups_raster_t *ras;

...

cupsRasterClose(ras);
```

## 另见
`cupsRasterOpen()`, `cupsRasterReadHeader()`, `cupsRasterReadPixels()`, `cupsRasterWriteHeader()`, `cupsRasterWritePixels()`

# cupsRasterOpen()

## 使用

```c
cups_raster_t * cupsRasterOpen(int fd, cups_mode_t mode);
```

## 参数

| 参数 | 类型 | 描述 |
| :--- | :--- | :--- |
| fd | `int` | 要使用的文件描述符 |
| mode | `cups_mode_t` | 要使用的模式：`CUPS_RASTER_READ` 或 `CUPS_RASTER_WRITE` |

## 返回
指向光栅流的指针，如果发生错误则返回 NULL。

## 描述
`cupsRasterOpen()` 函数打开一个用于读取或写入的光栅流。

## 示例

```c
#include <cups/raster.h>

cups_raster_t *ras;

...

ras = cupsRasterOpen(0, CUPS_RASTER_READ);
```

## 另见
`cupsRasterClose()`, `cupsRasterReadHeader()`, `cupsRasterReadPixels()`, `cupsRasterWriteHeader()`, `cupsRasterWritePixels()`

# cupsRasterReadHeader()

## 使用

```c
unsigned
cupsRasterReadHeader(cups_raster_t *ras,
cups_page_header_t *header);
```

## 参数

| 参数 | 类型 | 描述 |
| :--- | :--- | :--- |
| ras | `cups_raster_t *` | 要从中读取的光栅流 |
| header | `cups_page_header_t *` | 指向用于读取页头结构的指针 |

## 返回
成功时返回 1，到达文件结束符 `EOF` 或出错时返回 0。

## 描述
`cupsRasterReadHeader()` 函数从指定的光栅流中读取页头。

## 示例

```c
#include <cups/raster.h>

int line;
cups_raster_t *ras;
cups_raster_header_t header;
unsigned char pixels[8192];

...

while (cupsRasterReadHeader(ras, &header))
{
    for (line = 0; line < header.cupsHeight; line ++)
    {
        cupsRasterReadPixels(ras, pixels, header.cupsBytesPerLine);
    }
}
```

## 另见
`cupsRasterClose()`, `cupsRasterOpen()`, `cupsRasterReadPixels()`, `cupsRasterWriteHeader()`, `cupsRasterWritePixels()`

# cupsRasterReadPixels()

## 使用

```c
unsigned
cupsRasterReadPixels(cups_raster_t *ras,
                      unsigned char *pixels,
                      unsigned length);
```

## 参数

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| ras | `cups_raster_t *` | 从中读取的光栅流 |
| pixels | `unsigned char *` | 指向像素缓冲区的指针 |
| length | `unsigned` | 要读取的像素数据字节数 |

## 返回
读取的字节数，到达文件结束符 `EOF` 或出错时返回 0。

## 描述
`cupsRasterReadPixels()` 函数从指定的光栅流中读取像素数据。

## 示例

```c
#include <cups/raster.h>

int line;
cups_raster_t *ras;
cups_raster_header_t header;
unsigned char pixels[8192];

...

while (cupsRasterReadHeader(ras, &header))
{
  ...
  for (line = 0; line < header.cupsHeight; line ++)
  {
    cupsRasterReadPixels(ras, pixels, header.cupsBytesPerLine);
    ...
  }
}
```

## 另见
`cupsRasterClose()`, `cupsRasterOpen()`, `cupsRasterReadHeader()`, `cupsRasterWriteHeader()`, `cupsRasterWritePixels()`

# cupsRasterWriteHeader()

## 使用

```c
unsigned cupsRasterWriteHeader(cups_raster_t *ras,
cups_page_header_t *header);
```

## 参数

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| ras | `cups_raster_t *` | 要写入的光栅流 |
| header | `cups_page_header_t *` | 要写入的页头结构 |

## 返回
成功时返回 1，出错时返回 0。

## 描述
`cupsRasterWriteHeader()` 函数将指定的页头写入光栅流。

## 示例

```c
#include <cups/raster.h>

int line;
cups_raster_t *ras;
cups_raster_header_t header;
unsigned char pixels[8192];

...

cupsRasterWriteHeader(ras, &header);
for (line = 0; line < header.cupsHeight; line++) {
  ...
  cupsRasterWritePixels(ras, pixels, header.cupsBytesPerLine);
}
```

## 另见
`cupsRasterClose()`, `cupsRasterOpen()`, `cupsRasterReadHeader()`, `cupsRasterReadPixels()`, `cupsRasterWritePixels()`

# cupsRasterWritePixels()

## 使用

```c
unsigned cupsRasterWritePixels(cups_raster_t *ras, unsigned char *pixels, unsigned length);
```

## 参数

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| ras | `cups_raster_t *` | 要写入的光栅流 |
| pixels | `unsigned char *` | 指向像素缓冲区的指针 |
| length | `unsigned` | 要写入的像素数据字节数 |

## 返回
写入的字节数。

## 描述
`cupsRasterWritePixels()` 函数将像素数据写入指定的光栅流。

## 示例

```c
#include <cups/raster.h>

int line;
cups_raster_t *ras;
cups_raster_header_t header;
unsigned char pixels[8192];

...

cupsRasterWriteHeader(ras, &header);
for (line = 0; line < header.cupsHeight; line++) {
  ...
  cupsRasterWritePixels(ras, pixels, header.cupsBytesPerLine);
}
```

## 另见
`cupsRasterClose()`, `cupsRasterOpen()`, `cupsRasterReadHeader()`, `cupsRasterReadPixels()`, `cupsRasterWritePixels()`

## 另见
`cupsServer()`, `cupsSetPasswordCB()`, `cupsSetServer()`, `cupsUser()`

# cupsTempFd()

### 使用
```c
int
cupsTempFd(char *filename, int length);
```



## `cupsTempFd()`

### 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `filename` | `char *` | 临时文件名缓冲区 |
| `length` | `int` | 文件名缓冲区的大小（字节） |

### 返回
返回一个为临时文件打开的文件描述符，并以独占读写模式打开。如果 `cupsTempFd()` 无法创建临时文件，则返回 `-1`。

### 描述
`cupsTempFd()` 函数在 `/var/tmp` 目录或 `TMPDIR` 环境变量指定的目录下安全地创建一个临时文件。

### 示例
```c
#include <cups/cups.h>

char filename[256];

int fd;

fd = cupsTempFd(filename, sizeof(filename));
```

## `cupsTempFile()`

### 使用
```c
char *
cupsTempFile(char *filename, int length);
```

### 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `filename` | `char *` | 临时文件名缓冲区 |
| `length` | `int` | 文件名缓冲区的大小（字节） |

### 返回
指向文件名的指针；如果无法创建临时文件，则返回 `NULL`。

### 描述
`cupsTempFile()` 函数在 `/var/tmp` 目录或 `TMPDIR` 环境变量指定的目录下安全地创建一个临时文件。它会关闭该文件，以便稍后再次打开。

此函数容易受到某些类型的“相同用户”符号链接攻击，因此尽可能应使用 `cupsTempFd()` 函数代替。

### 示例
```c
#include <cups/cups.h>

char filename[256];

cupsTempFile(filename, sizeof(filename));
```

## `cupsUser()`

### 使用
```c
const char *
cupsUser(void);
```

### 返回
指向当前用户名的指针；如果用户 ID 未定义，则返回 `NULL`。

### 描述
`cupsUser()` 函数返回当前用户名。初始时，该名称与 `getuid()` 系统调用报告的当前用户 ID 联联；然而，可以使用 `cupsSetUser()` 函数来更改它。

### 示例
```c
#include <cups/cups.h>

const char *user;

user = cupsUser();
```

### 另
`cupsgetPassword()`, `cupsServer()`, `cupsSetUser()`

## `httpBlocking()`

### 使用
```c
void
httpBlocking(http_t *http, int blocking);
```

### 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `http` | `http_t *` | HTTP 连接 |
| `blocking` | `int` | `0` 表示连接为非阻塞，`1` 表示连接应为阻塞 |

### 描述
`httpBlocking()` 函数设置 HTTP 连接的阻塞模式。默认情况下，HTTP 连接会阻塞（停止）客户端程序，直到数据可用或可以发送到服务器。

### 示例
```c
#include <cups/http.h>

http_t *http;

http = httpConnect("server", port);

httpBlocking(http, 0);
```

### 另
`httpCheck()`, `httpConnect()`

## `httpCheck()`

### 使用
```c
int httpCheck(http_t *http);
```

### 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `http` | `http_t *` | HTTP 连接 |

### 返回
如果没有待处理数据，返回 `0`。否则返回 `1`。

### 描述
`httpCheck()` 函数检查 HTTP 连接上是否有任何待处理的数据。

### 示例
```c
#include <cups/http.h>

http_t *http;

if (httpCheck(http)) {
  ... 执行操作 ...
}
```

### 另
`httpBlocking()`, `httpConnect()`, `httpGets()`, `httpRead()`

## `httpCheck()` 替代方案

### 使用
```c
int httpCheck(http_t *http);
```

### 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `http` | `http_t *` | HTTP 连接 |

### 返回
如果来自 HTTP 服务器的输入待处理，则返回 `1`，否则返回 `0`。

### 描述
`httpCheck()` 函数检查来自 HTTP 服务器的输入是否待处理。

### 示例
```c
#include <cups/http.h>

...
http_t *http;
...

if (httpCheck(http))
    puts("Server has something to say!");
```

### 另
`httpConnect()`

## `httpClearFields()`

### 使用
```c
void httpClearFields(http_t *http);
```

### 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `http` | `http_t *` | HTTP 连接 |

### 描述
`httpClearFields()` 函数清除该 HTTP 连接的所有 HTTP 请求字段。

### 示例
```c
#include <cups/http.h>

http_t *http;

httpClearFields(http);
```

### 另
`httpConnect()`, `httpGetField()`, `httpSetField()`

## `httpClose()`

### 使用
```c
void httpClose(http_t *http);
```

### 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `http` | `http_t *` | HTTP 连接 |

### 描述
`httpClose()` 函数关闭一个活跃的 HTTP 连接。

### 示例
```c
#include <cups/http.h>

http_t *http;

httpClose(http);
```

### 另
`httpConnect()`

## `httpConnect()`

### 使用
```c
http_t *httpConnect(char *hostname, int port);
```

### 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `hostname` | `char *` | 主机名或 IP 地址 |
| `port` | `int` | 端口号 |

### 返回
指向连接的指针；如果连接失败，则返回 `NULL`。

### 描述
`httpConnect()` 函数打开到指定服务器的连接。

### 示例
```c
#include <cups/http.h>

http_t *http;

http = httpConnect("server", port);
```

## `httpClose()` 替代方案

### 使用
```c
void httpClose(http_t *http);
```

### 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `http` | `http_t *` | HTTP 连接 |

### 描述
`httpClose()` 函数关闭一个活跃的 HTTP 连接。

### 示例
```c
#include <cups/http.h>

http_t *http;

httpClose(http);
```

## `httpConnect()` 替代方案

### 使用
```c
http_t *httpConnect(char *hostname, int port);
```

### 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `hostname` | `char *` | 主机名或 IP 地址 |
| `port` | `int` | 端口号 |

### 返回
指向连接的指针；如果连接失败，则返回 `NULL`。

### 描述
`httpConnect()` 函数打开到指定服务器的连接。

### 示例
```c
#include <cups/http.h>

http_t *http;

http = httpConnect("server", port);
```

## `httpEncryption()`

### 使用
```c
void httpEncryption(http_t *http, http_encryption_t encryption);
```

### 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `http` | `http_t *` | HTTP 连接 |
| `encryption` | `http_encryption_t` | 将使用的加密类型 |

### 描述
`httpEncryption()` 函数设置在与 HTTP 服务器连接上使用的加密类型。此函数可能会关闭并重新连接到服务器以建立新的加密类型。

### 示例
```c
#include <cups/http.h>

http_t *http;

httpEncryption(http, HTTP_ENCRYPT_REQUIRED);
```

### 另
`httpConnectEncrypt()`

## `httpError()`

### 使用
```c
int
httpError(http_t *http);
```

### 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `http` | `http_t *` | HTTP 连接 |

### 返回
最后发生的错误，或者如果没有发生错误则返回 `0`。

### 描述
`httpError()` 函数返回 HTTP 连接上发生的最后一个错误。

### 示例
```c
#include <cups/http.h>

http_t *http;

if (httpError(http)) {
  ... 显示错误消息 ...
}
```

### 另
`httpConnect()`

## `httpFlush()`

### 使用
```c
void
httpFlush(http_t *http);
```

### 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `http` | `http_t *` | HTTP 连接 |

### 描述
`httpFlush()` 函数刷新从 GET 或 POST 操作留下的任何剩余数据。

### 示例
```c
#include <cups/http.h>

http_t *http;

httpFlush(http);
```

### 另
`httpConnect()`

## `httpGet()`

### 使用
```c
int
httpGet(http_t *http,
    const char *uri);
```

### 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `http` | `http_t *` | HTTP 连接 |
| `uri` | `const char *` | 要获取的 URI |

### 返回
成功时返回 `0`，失败时返回非零。

### 描述
`httpGet()` 函数向服务器发送 HTTP GET 请求。

### 示例
```c
#include <cups/http.h>

http_t *http;

httpGet(http, "/some/uri");
```

### 另
`httpConnect()`, `httpSetField()`, `httpUpdate()`

## `httpGetDateString()`

### 使用
```c
const char *
httpGetDateString(time_t time);
```

### 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `time` | `time_t` | Unix 日期/时间值 |

### 返回
指向静态字符串的指针，该字符串包含指定 Unix 时间值的 HTTP 日期/时间字符串。

### 描述
`httpGetString()` 函数从 Unix 时间值生成适用于 HTTP 请求的日期/时间字符串。该日期/时间字符串在每次调用时都会被重写。

### 示例
```c
#include <cups/http.h>

puts(httpGetString(time(NULL)));
```

### 另
`httpGetDateTime()`

## `httpGetDateTime()`

### 使用
```c
time_t
httpGetDateTime(const char *date);
```

### 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `date` | `const char *` | HTTP 日期/时间字符串 |

### 返回
一个 Unix 时间值。

### 描述
`httpDateTime()` 函数将 HTTP 日期/时间字符串转换为 Unix 时间值。

### 示例
```c
#include <cups/http.h>

printf("%d\n", httpDateTime("Fri, 30 June 2000 12:34:56 GMT"));
```

### 另
`httpGetString()`

## `httpGetField()`

### 使用
```c
const char *
httpGetField(http_t *http,
http_field_t field);
```

### 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `http` | `http_t *` | HTTP 连接 |
| `field` | `http_field_t` | HTTP 字段 |

### 返回
指向字段值字符串的指针。

### 描述
`httpGetField()` 函数返回指定 HTTP 字段的当前值。空字段由长度为 `0` 的字符串表示。

### 示例
```c
#include <cups/http.h>

http_t *http;

httpGet(http, "/some/uri");
while (httpUpdate(http)) == HTTP_CONTINUE);
puts(httpGetField(http, HTTP_FIELD_CONTENT_TYPE));
```

### 另
`httpGetSubField()`, `httpSetField()`

## `httpGetLength()`

### 使用
```c
int
httpGetLength(http_t *http);
```

### 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `http` | `http_t *` | HTTP 连接 |

### 返回
GET 或 POST 内容的长度。

### 描述
`httpGetLength()` 函数返回 GET 或 POST 请求返回的字节数。

### 示例
```c
#include <cups/http.h>

http_t *http;

httpGet(http, "/some/uri");
while (httpUpdate(http)) == HTTP_CONTINUE);
printf("Content length = %d\n", httpGetLength(http));
```

### 另
`httpConnect()`

## `httpGets()`

### 使用
```c
char *line,
httpGets(char *line,
int length,
http_t *http)
```

### 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `line` | `char *` | 行缓冲区 |
| `length` | `int` | 行缓冲区的大小（字节） |
| `http` | `http_t *` | HTTP 连接 |

### 返回
指向字符串的指针，如果无法检索到行则返回 `NULL`。

### 描述
`httpGets` 函数用于从 HTTP 连接读取请求行。它通常不被客户端程序使用。

### 示例
```c
#include <cups/http.h>

http_t *http;
char line[1024];

if (httpGets(line, sizeof(line), http))
{
    ... 处理该行 ...
}
```

### 另
`httpConnect()`, `httpUpdate()`

## `httpGetSubField()`

### 使用
```c
const char *httpGetSubField(http_t *http,
    http_field_t field,
    const char *name,
    char        *value);
```

### 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `http` | `http_t *` | HTTP 连接 |
| `field` | `http_field_t` | HTTP 字段 |
| `name` | `const char *` | 名称 |
| `value` | `char *` | 值 |

### 返回
指向字段值字符串的指针。

### 描述
`httpGetSubField()` 函数返回指定 HTTP 字段的当前值。空字段由长度为 `0` 的字符串表示。

### 示例
```c
#include <cups/http.h>

http_t *http;

httpGet(http, "/some/uri");
```



`while (httpUpdate(http)) == HTTP_CONTINUE);`

`puts(httpGetField(http, HTTP_FIELD_CONTENT_TYPE));`

# httpGetLength()

## 使用

```c
int
httpGetLength(http_t *http);
```

## 参数

| 参数 | 类型 | 说明 |
|---|---|---|
| `http` | `http_t *` | HTTP 连接 |

## 返回

GET 或 POST 数据的长度。

## 描述

`httpGetLength()` 函数返回 GET 或 POST 请求返回的字节数。

## 示例

```c
#include <cups/http.h>

http_t *http;

httpGet(http, "/some/uri");
while (httpUpdate(http)) == HTTP_CONTINUE);
printf("Content length = %d\n", httpGetLength(http));
```

## 另

`httpConnect()`

# httpGets()

## 使用

```c
char *
httpGets(char *line,
         int length,
         http_t *http)
```

## 参数

| 参数 | 类型 | 说明 |
|---|---|---|
| `line` | `char *` | 行缓冲区 |
| `length` | `int` | 行缓冲区的大小（字节） |
| `http` | `http_t *` | HTTP 连接 |

## 返回

指向字符串的指针，如果无法检索到行则返回 NULL。

## 描述

`httpGets` 函数用于从 HTTP 连接读取请求行。它通常不被客户端程序使用。

## 示例

```c
#include <cups/http.h>

http_t *http;
char line[1024];

if (httpGets(line, sizeof(line), http))
{
    ... 处理该行 ...
}
```

## 另

`httpConnect()`, `httpUpdate()`

# httpGetSubField()

## 使用

```c
const char *httpGetSubField(http_t *http,
    http_field_t field,
    const char *name,
    char        *value);
```

## 参数

| 参数 | 类型 | 说明 |
|---|---|---|
| `http` | `http_t *` | HTTP 连接 |
| `field` | `http_field_t` | HTTP 字段 |
| `name` | `const char *` | 名称 |
| `value` | `char *` | 值 |

## 返回

指向字段值字符串的指针。

## 描述

`httpGetSubField()` 函数返回指定 HTTP 字段的当前值。空字段由长度为 0 的字符串表示。

## 示例

```c
#include <cups/http.h>

http_t *http;

httpGet(http, "/some/uri");
while (httpUpdate(http)) == HTTP_CONTINUE);

puts(httpGetField(http, HTTP_FIELD_CONTENT_TYPE));
```

## 另

`httpGetField()`, `httpSetField()`

# httpGet()

## 使用

```c
int
httpGet(http_t *http,
    const char *uri);
```

## 参数

| 参数 | 类型 | 说明 |
|---|---|---|
| `http` | `http_t *` | HTTP 连接 |
| `uri` | `const char *` | 要获取的 URI |

## 返回

成功时返回 0，失败时返回非零。

## 描述

`httpGet()` 函数向服务器发送 HTTP GET 请求。

## 示例

```c
#include <cups/http.h>

http_t *http;

httpGet(http, "/some/uri");
```

## 另

`httpConnect()`, `httpSetField()`, `httpUpdate()`

# httpGetDateString()

## 使用

```c
const char *
httpGetDateString(time_t time);
```

## 参数

| 参数 | 类型 | 说明 |
|---|---|---|
| `time` | `time_t` | Unix 日期/时间值 |

## 返回

指向静态字符串的指针，该字符串包含指定 Unix 时间值的 HTTP 日期/时间字符串。

## 描述

`httpGetString()` 函数从 Unix 时间值生成适用于 HTTP 请求的日期/时间字符串。该日期/时间字符串在每次调用时都会被重写。

## 示例

```c
#include <cups/http.h>

puts(httpGetString(time(NULL)));
```

## 另

`httpGetDateTime()`

# httpGetDateTime()

## 使用

```c
time_t
httpGetDateTime(const char *date);
```

## 参数

| 参数 | 类型 | 说明 |
|---|---|---|
| `date` | `const char *` | HTTP 日期/时间字符串 |

## 返回

一个 Unix 时间值。

## 描述

`httpDateTime()` 函数将 HTTP 日期/时间字符串转换为 Unix 时间值。

## 示例

```c
#include <cups/http.h>

printf("%d\n", httpDateTime("Fri, 30 June 2000 12:34:56 GMT"));
```

## 另

`httpGetString()`

# httpGetField()

## 使用

```c
const char *
httpGetField(http_t *http,
             http_field_t field);
```

## 参数

| 参数 | 类型 | 说明 |
|---|---|---|
| `http` | `http_t *` | HTTP 连接 |
| `field` | `http_field_t` | HTTP 字段 |

## 返回

指向字段值字符串的指针。

## 描述

`httpGetField()` 函数返回指定 HTTP 字段的当前值。空字段由长度为 0 的字符串表示。

## 示例

```c
#include <cups/http.h>

http_t *http;

httpGet(http, "/some/uri");
while (httpUpdate(http)) == HTTP_CONTINUE);

puts(httpGetField(http, HTTP_FIELD_CONTENT_TYPE));
```

## 另

`httpGetSubField()`, `httpSetField()`

# httpMD5String()

## 使用

```c
char *
httpMD5String(const md5_byte_t *sum, char md5[33]);
```

## 参数

| 参数 | 类型 | 说明 |
|---|---|---|
| `sum` | `const md5_byte_t *` | 原始 MD5 和 |
| `md5` | `char [33]` | 十进制格式的 MD5 和 |

## 返回

MD5 字符串。

## 描述

`httpMD5String()` 函数将 16 字节的原始 MD5 和转换为 32 字节的十六进制字符串。

## 示例

```c
#include <cups/http.h>
...
md5_byte_t digest[16];
char md5[33];
...
puts(httpMD5String(digest, md5));
```

## 另

`httpMD5()`, `httpMD5Final()`

# httpOptions()

## 使用

```c
int
httpOptions(http_t *http, const char *uri);
```

## 参数

| 参数 | 类型 | 说明 |
|---|---|---|
| `http` | `http_t *` | HTTP 连接 |
| `uri` | `const char *` | 检查选项的 URI |

## 返回

成功返回 0，失败返回非零值。

## 描述

`httpOptions()` 函数向服务器发送 HTTP OPTIONS 请求。

## 示例

```c
#include <cups/http.h>

http_t *http;

httpOptions(http, "/some/uri");
```

## 另

`httpConnect()`, `httpSetField()`, `httpUpdate()`

# httpPost()

## 使用

```c
int
httpPost(http_t *http, const char *uri);
```

## 参数

| 参数 | 类型 | 说明 |
|---|---|---|
| `http` | `http_t *` | HTTP 连接 |
| `uri` | `const char *` | 要 POST 的 URI |

## 返回

成功返回 0，失败返回非零值。

## 描述

`httpPost()` 函数向服务器发送 HTTP POST 请求。

## 示例

```c
#include <http.h>

http_t *http;

httpPost(http, "/some/uri");
```

## 另

`httpConnect()`, `httpSetField()`, `httpUpdate()`

# httpPrintf()

## 使用

```c
int httpPrintf(http_t *http, const char *format, ...);
```

## 参数

| 参数 | 类型 | 说明 |
|---|---|---|
| `http` | `http_t *` | HTTP 连接 |
| `format` | `const char *` | printf 风格的格式字符串 |
| `...` | varies | 根据需要的额外参数 |

## 返回

写入的字节数。

## 描述

`printf()` 函数向 HTTP 连接发送格式化字符串。通常情况下，只有 CUPS API 和调度器会使用它。

## 示例

```c
#include <cups/http.h>

http_t *http;

printf(http, "GET / HTTP/1.1 \r\n");
```

## 另

`httpConnect()`

# httpPut()

## 使用

```c
int
httpPut(http_t *http, const char *uri);
```

## 参数

| 参数 | 类型 | 说明 |
|---|---|---|
| `http` | `http_t *` | HTTP 连接 |
| `uri` | `const char *` | 要 PUT 的 URI |

## 返回

成功返回 0，失败返回非零值。

## 描述

`httpPut()` 函数向服务器发送 HTTP PUT 请求。

## 示例

```c
#include <cups/http.h>

http_t *http;

httpPut(http, "/some/uri");
```

## 另

`httpConnect()`, `httpSetField()`, `httpUpdate()`

# httpRead()

## 使用

```c
int
httpRead(http_t *http, char *buffer, int length);
```

## 参数

| 参数 | 类型 | 说明 |
|---|---|---|
| `http` | `http_t *` | HTTP 连接 |
| `buffer` | `char *` | 读取的缓冲区 |
| `length` | `int` | 最大读取字节数 |

## 返回

读取的字节数，或出错时返回 -1。

## 描述

`httpRead()` 函数从 HTTP 连接读取数据，可能是 GET 或 POST 请求的结果。



# 示例

```c
#include <cups/http.h>

http_t *http;
char buffer[1024];
int bytes;

httpGet(http, "/");
while (httpUpdate(http) != HTTP_CONTINUE);
while ((bytes = httpRead(http, buffer, sizeof(buffer) - 1)) > 0)
{
  buffer[bytes] = '\0';
  fputs(buffer, stdout);
}
```

# 另

```c
httpConnect(), httpWrite()
```

# `httpReconnect()`

# 使用

```c
int
httpReconnect(http_t *http);
```

# 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| `http` | `http_t *` | HTTP 连接 |

# 返回

成功返回 `0`，失败返回非零值。

# Description

`httpReconnect()` 函数重新连接到 HTTP 服务器。如果 HTTP 函数检测到服务器连接已终止，这通常是自动的。

# 示例

```c
#include <cups/http.h>

http_t *http;

httpReconnect(http);
```

# 另

`httpConnect()`, `httpConnectEncrypt()`

# `httpSeparate()`

# 使用

```c
void
httpSeparate(const char *uri,
             char *method,
             char *username,
             char *host,
             int *port,
             char *resource);
```

# 参数

| 参数 | 类型 | 说明 |
|---|---|---|
| `uri` | `const char *` | 待拆分的 URI |
| `method` | `char [HTTP_MAX_URI]` | URI 的方法（方案） |
| `username` | `char [HTTP_MAX_URI]` | URI 的用户名（和密码）部分，如果有 |
| `host` | `char [HTTP_MAX_URI]` | URI 的主机名，如果有 |
| `port` | `int *` | URI 的端口号，指定的或方法/方案的默认值 |
| `resource` | `char [HTTP_MAX_URI]` | 资源字符串，通常为服务器的文件名 |

# Description

`httpSeparate()` 函数将指定的 URI 拆分为各个组成部分。方法、用户名、主机和资源字符串的长度至少应对应缓冲区的长度。

## `ippAddBoolean()`

### Usage

```c
ipp_attribute_t *
ippAddBoolean(ipp_t *ipp,
               ipp_tag_t group,
               const char *name,
               char value);
```

### Arguments

| Argument | Type | Description |
| --- | --- | --- |
| `ipp` | `ipp_t *` | IPP 请求 |
| `group` | `ipp_tag_t` | IPP 组 |
| `name` | `const char *` | 属性的名称 |
| `value` | `char` | 布尔值 |

### Returns

指向新属性的指针，如果无法创建该属性则返回 `NULL`。

### Description

`ippAddBoolean()` 函数向指定的 IPP 请求添加单个的布尔属性值。

### Example

```c
#include <cups/ipp.h>

ipp_t *ipp;

ippAddBoolean(ipp, IPP_TAG_OPERATION, "my-jobs", 1);
```

### See Also

`ippAddBooleans()`, `ippAddDate()`, `ippAddInteger()`, `ippAddIntegers()`, `ippAddRange()`,

`ippAddRanges()`, `ippAddResolution()`, `ippAddResolutions()`, `ippAddSeparator()`,

`ippAddString()`, `ippAddStrings()`

## `ippAddBooleans()`

### Usage

```c
ipp_attribute_t *
ippAddBooleans(ipp_t *ipp,
               ipp_tag_t group,
               const char *name,
               int num_values,
               const char *values);
```

### Arguments

| Argument | Type | Description |
| --- | --- | --- |
| `ipp` | `ipp_t *` | IPP 请求 |
| `group` | `ipp_tag_t` | IPP 组 |
| `name` | `const char *` | 属性的名称 |
| `num_values` | `int` | 布尔值的数量 |
| `values` | `const char *` | 布尔值列表

### Returns

指向新属性的指针，如果无法创建该属性则返回 `NULL`。

### Description

`ippAddBooleans()` 函数向指定的 IPP 请求添加一个或多个布尔属性值。如果 `values` 指针为 `NULL`，则创建一个包含 `num_values` 个 `false`（假）值的数组。

### See Also

`ippAddBoolean()`, `ippAddDate()`, `ippAddInteger()`, `ippAddIntegers()`, `ippAddRange()`,

`ippAddRanges()`, `ippAddResolution()`, `ippAddResolutions()`, `ippAddSeparator()`,

`ippAddString()`, `ippAddStrings()`

## `ippAddDate()`

### Usage

```c
ipp_attribute_t *ippAddDate(ipp_t *ipp,
                            ipp_tag_t group,
                            const char *name,
                            ipp_uchar_t *value);
```

### Arguments

| Argument | Type | Description |
| --- | --- | --- |
| `ipp` | `ipp_t *` | IPP 请求 |
| `group` | `ipp_tag_t` | IPP 组 |
| `name` | `const char *` | 属性的名称 |
| `value` | `ipp_uchar_t *` | 日期值 |

### Returns

指向新属性的指针，如果无法创建该属性则返回 `NULL`。

### Description

`ippAddDate()` 函数向指定的 IPP 请求添加单个日期-时间属性值。

### Example

```c
#include <cups/ipp.h>

ipp_t *ipp;

ippAddDate(ipp, IPP_TAG_OPERATION, "some-attribute",
ippTimeToDate(time(NULL)));
```

### See Also

`ippAddBoolean()`, `ippAddBooleans()`, `ippAddInteger()`, `ippAddIntegers()`, `ippAddRange()`, `ippAddRanges()`, `ippAddResolution()`, `ippAddResolutions()`, `ippAddSeparator()`, `ippAddString()`, `ippAddStrings()`, `ippTimeToDate()`

## `ippAddInteger()`

### Usage

```c
ipp_attribute_t *
ippAddInteger(ipp_t *ipp,
               ipp_tag_t group,
               ipp_tag_t tag,
               const char *name,
               int value);
```

### Arguments

| Argument | Type | Description |
|---|---|---|
| `ipp` | `ipp_t *` | IPP 请求 |
| `group` | `ipp_tag_t` | IPP 组 |
| `tag` | `ipp_tag_t` | IPP 值标签 |
| `name` | `const char *` | 属性的名称 |
| `value` | `int` | 整数值 |

### Returns

指向新属性的指针，如果无法创建该属性则返回 `NULL`。

### Description

`ippAddInteger()` 函数向指定的 IPP 请求添加单个整数属性值。

### Example

```c
#include <cups/ipp.h>

ipp_t *ipp;

ippAddInteger(ipp, IPP_TAG_OPERATION, "limit", 100);
```

### See Also

`ippBoolean()`, `ippAddBooleans()`, `ippAddDate()`, `ippAddIntegers()`, `ippAddRange()`, 

`ippAddRanges()`, `ippAddResolution()`, `ippAddResolutions()`, `ippAddSeparator()`, 

`ippString()`, `ippAddStrings()`

## `ippAddIntegers()`

### Usage

```c
ipp_attribute_t *
ippAddIntegers(ipp_t *ipp,
                ipp_tag_t group,
                ipp_tag_t tag,
                const char *name,
                int num_values,
                const char *values);
```

### Arguments

| Argument | Type | Description |
| --- | --- | --- |
| `ipp` | `ipp_t *` | IPP 请求 |
| `group` | `ipp_tag_t` | IPP 组 |
| `tag` | `ipp_tag_t` | IPP 值标签 |
| `name` | `const char *` | 属性的名称 |
| `num_values` | `int` | 整数值的数量 |
| `values` | `const char *` | 整数值列表

### Returns

指向新属性的指针，如果无法创建该属性则返回 `NULL`。

### Description

`ippAddIntegers` 函数向指定的 IPP 请求添加一个或多个整数属性值。如果 `values` 指针为 `NULL`，则创建一个整数数组。

### Example

```c
#include <cups/ipp.h>

ipp_t *ipp;
int values[100];

ippAddIntegers(ipp, IPP_TAG_OPERATION, "some-attribute", 100, values);
```

### See Also

`ippAddBoolean()`, `ippAddBooleans()`, `ippAddDate()`, `ippAddInteger()`, `ippAddRange()`, `ippAddRanges()`, `ippAddResolution()`, `ippAddResolutions()`, `ippAddString()`, `ippAddStrings()`

## `ippAddRange()`

### Usage

```c
ipp_attribute_t *ippAddRange(ipp_t *ipp,
                           ipp_tag_t group,
                           const char *name,
                           int low,
                           int high);
```

### Arguments

| Argument | Type | Description |
| --- | --- | --- |
| `ipp` | `ipp_t *` | IPP 请求 |
| `group` | `ipp_tag_t` | IPP 组 |
| `name` | `const char *` | 属性的名称 |
| `low` | `int` | 范围下限 |
| `high` | `int` | 范围上限 |

### Returns

指向新属性的指针，如果无法创建该属性则返回 `NULL`。

### Description

`ippAddRange()` 函数向指定的 IPP 请求添加单个范围值。

### Example

```c
#include <cups/ipp.h>

ipp_t *ipp;

ippAddRange(ipp, IPP_TAG_OPERATION, "page-ranges", 1, 10);
```

## `ippAddRanges()`

### Usage

```c
ipp_attribute_t *ippAddRanges(ipp_t *ipp,
                            ipp_tag_t group,
                            const char *name,
                            int num_values,
                            const int *lows,
                            const int *highs);
```

### Arguments

| Argument | Type | Description |
| --- | --- | --- |
| `ipp` | `ipp_t *` | IPP 请求 |
| `group` | `ipp_tag_t` | IPP 组 |
| `name` | `const char *` | 属性的名称 |
| `num_values` | `int` | 范围值的数量 |
| `lows` | `const int *` | 下限值列表 |
| `highs` | `const int *` | 上限值列表

### Returns

指向新属性的指针，如果无法创建该属性则返回 `NULL`。

### Description

`ippAddRanges()` 函数向指定的 IPP 请求添加一个或多个范围属性值。如果 `values` 指针为 `NULL`，则创建一个范围数组。

### Example

```c
#include <cups/ipp.h>

ipp_t *ipp;
int lows[2];
int highs[2];

ippAddRanges(ipp, IPP_TAG_OPERATION, "page-ranges", 2, lows, highs);
```

### See Also

`ippAddBoolean()`, `ippAddBooleans()`, `ippAddDate()`, `ippAddInteger()`, `ippAddIntegers()`, `ippAddRange()`, `ippAddResolution()`, `ippAddResolutions()`, `ippAddSeparator()`, `ippAddString()`, `ippAddStrings()`

## `ippAddResolution()`

### Usage

```c
ipp_attribute_t *ippAddResolution(ipp_t *ipp,
                               ipp_tag_t group,
                               const char *name,
                               int xres,
                               int yres,
                               ipp_res_t units);
```

### Arguments

| Argument | Type | Description |
| --- | --- | --- |
| `ipp` | `ipp_t *` | IPP 请求 |
| `group` | `ipp_tag_t` | IPP 组 |
| `name` | `const char *` | 属性的名称 |
| `xres` | `int` | 水向分辨率值 |
| `yres` | `int` | 垂直分辨率值 |
| `units` | `ipp_res_t` | 分辨率单位值 |

### Returns

指向新属性的指针，如果无法创建该属性则返回 `NULL`。

### Description

`ippAddResolution()` 函数向指定的 IPP 请求添加单个分辨率属性值。

### Example



```c
#include <cups/ipp.h>

ipp_t *ipp;

ippAddResolution(ipp, IPP_TAG_OPERATION, "printer-resolution", 720, 720, IPP_RES_PER_INCH);
```

### See Also

`ippAddBoolean()`, `ippAddBooleans()`, `ippAddDate()`, `ippAddInteger()`, `ippAddIntegers()`, `ippAddRange()`, `ippAddRanges()`, `ippAddResolutions()`, `ippAddSeparator()`, `ippAddString()`, `ippAddStrings()`

## `ippAddResolutions()`

### Usage

```c
ipp_attribute_t *ippAddResolutions(ipp_t *ipp,
                               ipp_tag_t *group,
                               const char *name,
                               int *num_values,
                               const int *xres,
                               const int *yres,
                               const ipp_res_t *units);
```

### Arguments

| Argument | Type | Description |
| --- | --- | --- |
| `ipp` | `ipp_t *` | IPP 请求 |
| `group` | `ipp_tag_t` | IPP 组 |
| `name` | `const char *` | 属性的名称 |
| `num_values` | `int` | 分辨值的数量 |
| `xres` | `const int *` | 水向分辨率值列表 |
| `yres` | `const int *` | 垂直分辨率值列表 |
| `units` | `const ipp_res_t *` | 分辨率单位列表 |

### Returns

指向新属性的指针，如果无法创建该属性则返回 `NULL`。

## `ippAddResolutions`

# 描述

`ippAddResolutions()` 函数向指定的 IPP 请求添加一个或多个分辨率属性值。如果 `values` 指针为 `NULL`，则创建一个包含 `0x0` 分辨率的数组。

# 示例

```c
#include <cups/ipp.h>

ipp_t *ipp;
int xres[5];
int yres[5];
ipp_res_t units[5];

ippAddBoolean(ipp, ipp_TAG_OPERATION, "printer-yres-supported", 5, xres, yres, units);
```

# 参见

- `ippAddBoolean()`, `ippAddResolutions()`, `ippAddDate()`, `ippAddInteger()`, `ippAddIntegers()`, `ippAddRange()`, `ippAddRanges()`, `ippAddResolution()`, `ippAddSeparator()`, `ippAddString()`, `ippAddStrings()`

## `ippAddSeparator`

# 用

```c
ipp_attribute_t *ippAddSeparator(ipp_t *ipp);
```

# 参数

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `ipp` | `ipp_t *` | IPP 请求 |

# 返回

指向新分隔符的指针，如果无法创建分隔符则返回 `NULL`。

# 描述

`ippAddSeparator()` 函数向指定的 IPP 请求添加一个分组分隔符。

# 示例

```c
#include <cups/ipp.h>

ipp_t *ipp;

ippAddSeparator(ipp);
```

# 参见

`ippAddBoolean()`, `ippAddBooleans()`, `ippAddDate()`, `ippAddInteger()`, `ippAddIntegers()`, `ippAddRange()`, `ippAddRanges()`, `ippAddResolution()`, `ippAddResolutions()`, `ippAddString()`, `ippAddStrings()`

## `ippAddString()`

# 用

```c
ipp_attribute_t *ippAddString(ipp_t *ipp,
    ipp_tag_t group,
    ipp_tag_t tag,
    const char *name,
    const char *charset,
    const char *value);
```

# 参数

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `ipp` | `ipp_t *` | IPP 请求 |
| `group` | `ipp_tag_t` | IPP 分组 |
| `tag` | `ipp_tag_t` | IPP 取值标签 |
| `name` | `const char *` | 属性名称 |
| `charset` | `const char *` | 字符串的字符集 |
| `value` | `const char *` | 字符串值 |

# 返回

指向新属性的指针，如果无法创建属性则返回 `NULL`。

# 描述

`ippAddString()` 函数向指定的 IPP 请求添加单个字符串属性值值。对于 `IPP_TAG_NAMELANG` 和 `IPP_TAG_TEXTLANG` 字符串，`charset` 值会随字符串一起提供，用于识别所使用的字符串编码。否则，将忽略 `charset` 值。

# 示例

```c
#include <cups/ipp.h>

ipp_t *ipp;

ippAddString(ipp, IPP_TAG_OPERATION, IPP_TAG_NAME, "job-name",
NULL, "abc123");
```

# 参见

`ippBoolean()`, `ippAddBooleans()`, `ippAddDate()`, `ippAddInteger()`, `ippAddIntegers()`,

`ippAddRange()`, `ippAddRanges()`, `ippAddResolution()`, `ippAddResolutions()`,

`ippAddSeparator()`, `ippAddStrings()`

## `ippAddStrings()`

# 用

```c
ipp_attribute_t *ippAddStrings(ipp_t *ipp,
              ipp_tag_t group,
              ipp_tag_t tag,
              const char *name,
              int      num_values,
              const char *charset,
              const char **values);
```

# 参数

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `ipp` | `ipp_t *` | IPP 请求 |
| `group` | `ipp_tag_t` | IPP 分组 |
| `tag` | `ipp_tag_t` | IPP 取值标签 |
| `name` | `const char *` | 属性名称 |
| `num_values` | `int` | 字符串的数量 |
| `charset` | `const char *` | 字符串的字符集 |
| `values` | `const char **` | 字符串值 |

# 返回

指向新属性的指针，如果无法创建属性则返回 `NULL`。

# 描述

`ippAddStrings()` 函数向指定的 IPP 请求添加一个或多个字符串属性值。对于 `IPP_TAG_NAMELANG` 和 `IPP_TAG_TEXTLANG` 字符串，`charset` 值会随字符串一起提供，用于识别所使用的字符串编码。否则，将忽略 `charset` 值。如果指针为 `NULL`，则创建一个包含 `NULL` 字符串的数组。

# 示例

```c
#include <cups/ipp.h>

ipp_t *ipp;
char values[2] = { "one", "two" };

ippAddStrings(ipp, IPP_TAG_OPERATION, IPP_TAG_KEYWORD, "attr-name",
2, NULL, values);
```

# 参见

`ippAddBoolean()`, `ippAddBooleans()`, `ippAddDate()`, `ippAddInteger()`, `ippAddIntegers()`,

`ippAddRange()`, `ippAddRanges()`, `ippAddResolution()`, `ippAddResolutions()`,

`ippAddSeparator()`, `ippAddString()`

## `ippNameToTime()`

# 用

```c
time_t ippNameToTime(ipp_attribute *date);
```

# 参数

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `date` | `ipp_attribute *` | IPP 属性 |

# 返回

该属性表示的时间。

# 描述

`ippTimeTo()` 函数将 IPP 属性转换为时间值。

# 示例

```c
#include <cups/ipp.h>

ipp_attribute *attr;
time_t time;

time = ippNameToTime(attr);
printf("%ld\n", time);
```

## `ippDelete()`

# 用

```c
void ippDelete(ipp_t *ipp);
```

# 参数

| 参数 | 类型 | 描述 |
| --- | --- | --- |
| `ipp` | `ipp_t *` | IPP 请求 |

# 描述

`ippDelete()` 函数释放与 IPP 请求相关的内存。

## `ippNew()`

# 用

```c
ipp_t *ippNew(void);
```

# 返回

指向新 IPP 请求或响应的指针。

# 描述

`ippNew()` 函数创建一个新的 IPP 请求或响应。

# 示例

```c
#include <cups/ipp.h>

ipp_t *ipp;

ipp = ippNew();
```

## `ippPort()`

# 用

```c
int ippPort(void);
```

# 返回

IPP 请求的默认 TCP/IP 端口号。

# 描述

`ippPort()` 函数返回请求的默认 IPP 端口号。

# 示例

```c
#include <cups/http.h>
#include <cups/ipp.h>

http_t *http;

http = httpConnect(cupsServer(), ippPort());
```

## `ippRead()`

## Usage

```
ipp_state_t
ippRead(http_t *http,
    ipp_t *ipp);
```

## Arguments

| Argument | Type | Description |
| --- | --- | --- |
| `http` | `http_t *` | HTTP 连接 |
| `ipp` | `ipp_t *` | IPP 请求 |

## Returns

当前的读取状态。

## Description

`ippRead()` 函数从指定的 HTTP 连接读取 IPP 属性。程序应继续调用 `ippRead()` 直到返回 `IPP_ERROR` 或 `IPP_DATA` 为止。

## Example

```c
#include cups/http.h
#include cups/ipp.h

http_t *http;
ipp_t *ipp;
ipp_state_t status;

ipp = ippNew();

while ((status = ippRead(http, ipp)) != IPP_ERROR)
    if (status == IPP_DATA)
        break;

if (status == IPP_DATA)
{
    ... 使用 ippRead() 读取额外的非 IPP 数据 ...
}
```

## See Also

`ippWrite()`

## `ippSetPort()`

## Usage

```c
void
ippSetPort(int port);
```

| Argument | Type | Description |
|---|---|---|
| `port` | `int` | 要使用的端口号 |

## Description

`ippSetPort()` 函数为请求设置默认的 IPP 端口号。

## Example

```c
#include <cups/http.h>
#include <cups/ipp.h>

...
ippSetPort(8631);
```

## See Also

`ippPort()`

## `ippTimeToDate()`

## Usage

```c
ipp_uchar_t *
ippTimeToDate(time_t time);
```

## Arguments

| Argument | Type | Description |
|---|---|---|
| `time` | `time_t` | Unix 时间值 |

## Returns

一个指向 IPP 日期-时间值的静态指针。

## Description

`ippTimeToDate()` 函数将 Unix 时间转换为 IPP 日期时间值。该日期值会在每次调用时被覆盖。

## Example

```c
#include <cups/ipp.h>

ipp_t *date;

date = ippTimeToDate(time(NULL));
```

## See Also

`ippDateToTime()`

## `ippWrite()`

## Usage

```c
ipp_state_t
ippWrite(http_t *http,
    ipp_t *ipp);
```

## Arguments

| Argument | Type | Description |
|---|---|---|
| `http` | `http_t *` | HTTP 连接 |
| `ipp` | `ipp_t *` | IPP 请求 |

## Returns

当前的写入状态。

## Description

`ippWrite()` 函数将 IPP 属性写入指定的 HTTP 连接。程序应继续调用 `ippWrite()` 直到返回 `IPP_ERROR` 或 `IPP_DATA` 为止。

## Example

```c
#include <cups/http.h>
#include <cups/http.h>

http_t *http;
ipp_t *ipp;
ipp_state_t status;

ipp = ippNew();
  ... 添加属性 ...

while ((status = ippWrite(http, ipp)) != IPP_ERROR)
  if (status == IPP_DATA)
    break;

if (status == IPP_DATA)
{
  ... 使用 httpWrite() 读取额外的非 IPP 数据 ...
}
```

## See Also

- `ippRead()`

## `ppdClose()`

## Usage

```c
void
ppdClose(ppd_file_t *ppd);
```

## Arguments

| Argument | Type | Description |
|---|---|---|
| `ppd` | `ppd_file_t *` | PPD 文件 |

## Description

`ppdClose()` 函数释放所有与 PPD 文件相关性内存。

## Example

```c
#include <cups/ppd.h>

ppd_file_t *ppd;

ppdClose(ppd);
```

## See Also

`ppdOpen()`, `ppdOpenFile()`, `ppdOpenFile()`

## `ppdConflicts()`

## Usage

```c
int
ppdConflicts(ppd_file_t *ppd);
```

## Arguments

| Argument | Type | Description |
|---|---|---|
| `ppd` | `ppd_file_t *` | PPD 文件 |

## Returns

文件中的选项冲突数量。

## Description

`ppdConflicts()` 函数返回与当前选择（已标记）选项的冲突数量。

## Example

```c
#include <cups/ppd.h>

ppd_file_t *ppd;

printf("%d conflicts\n", ppdConflicts(ppd));
```

## See Also

`cupsMarkOptions()`, `ppdIsMarked()`, `ppdMarkDefaults()`, `ppdMarkOption()`

## `ppdEmit()`

## Usage

```c
int
ppdEmit(ppd_file_t *ppd,
FILE *file,
ppd_section_t section);
```

## Arguments



# ppdEmit

## Arguments

| Argument | Type | Description |
|---|---|---|
| ppd | `ppd_file_t *` | PPD 文件 |
| file | `FILE *` | 要写入的文件 |
| section | `ppd_section_t` | 要写入的节 |

## Returns

成功返回 0。

## Description

`ppdEmit()` 函数向指定文件发送打印机特定的选项命令。

## Example

```c
#include <cups/ppd.h>

ppd_file_t *ppd;

ppdEmit(ppd, stdout, PPD_ORDER_PAGE);
```

## See Also

`ppdEmitJCL()`, `ppdEmitFd()`

# ppdEmitFd

## Usage

```c
int
ppdEmitFd(ppd_file_t *ppd,
    int fd,
    ppd_section_t section);
```

## Arguments

| Argument | Type | Description |
|---|---|---|
| ppd | `ppd_file_t *` | PPD 文件 |
| fd | `int` | 要写入的文件描述符 |
| section | `ppd_section_t` | 要写入的选项节 |

## Returns

成功返回 0。

## Description

`ppdEmitFd()` 函数向指定的文件描述符发送打印机特定的选项命令。

## Example

```c
#include <cups/ppd.h>

ppd_file_t *ppd;

ppdEmitFd(ppd, 1, PPD_ORDER_PAGE);
```

## See Also

`ppdEmit()`, `ppdEmitCL()`

# ppdEmitCL

## Usage

```c
int
ppdEmitCL(ppd_file_t *ppd,
               FILE *file,
               int job_id,
               const char *user,
               const char *title);
```

## Arguments

| Argument | Type | Description |
|---|---|---|
| ppd | `ppd_file_t *` | PPD 文件 |
| file | `FILE *` | 要写入的文件 |
| job_id | `int` | 任务 ID |
| user | `const char *` | 任务所有 |
| title | `const char *` | 任务标题 |

## Returns

成功返回 0。

## Description

`ppdEmitCL()` 函数向指定的文件发送打印机特定的控制命令。当 PPD 文件使用 JCL 时，任务 ID 和标题包含在 JCL 命令中。

## Example

```c
#include <cups/ppd.h>

ppd_file_t *ppd;

ppdEmitCL(ppd, stdout, 123, "user", "title");
```

## See Also

`ppdEmit()`, `ppdEmitFd()`

# ppdFindChoice

## Usage

```c
ppd_choice_t
ppdFindChoice(ppd_option_t *option,
    const char *choice);
```

## Arguments

| Argument | Type | Description |
|---|---|---|
| option | `ppd_option_t *` | 选项 |
| choice | `const char *` | 选项名称 |

## Returns

选项指针，如果选项不存在则返回 NULL。

## Description

`ppdFindChoice()` 返回指定选项的选项指针。

## Example

```c
#include <cups/ppd.h>

ppd_file_t *ppd;
ppd_option_t *option;
ppd_choice_t *choice;

option = ppdFindChoice(ppd, "PageSize");
choice = ppdFindChoice(option, "Letter");
```

## See Also

`ppdMarkedChoice()`, `ppdFindOption()`

# ppdFindMarkedChoice

## Usage

```c
ppd_choice_t
ppdFindMarkedChoice(ppd_file_t *ppd,
              const char *keyword);
```

## Arguments

| Argument | Type | Description |
|---|---|---|
| ppd | `ppd_file_t *` | PPD 文件 |
| keyword | `const char *` | 选项名称 |

## Returns

选项指针，如果选项不存在或未标记则返回 NULL。

## Description

`ppdFindMarkedChoice()` 返回指定选项的标记选项指针。

## Example

```c
#include <cups/ppd.h>

ppd_file_t *ppd;
ppd_choice_t *choice;

choice = ppdFindMarkedChoice(ppd, "PageSize");
```

## See Also

`ppdFindChoice()`, `ppdFindOption()`

# ppdFindOption

## Usage

```c
ppd_option_t *
ppdFindOption(ppd_file_t *ppd,
              const char *keyword);
```

## Arguments

| Argument | Type | Description |
| --- | --- | --- |
| ppd | `ppd_file_t *` | PPD 文件 |
| keyword | `const char *` | 选项名称 |

## Returns

选项指针，如果选项不存在则返回 NULL。

## Description

`ppdFindOption()` 返回指定选项的选项数据指针。

## Example

```c
#include <cups/ppd.h>

ppd_file_t *ppd;
ppd_option_t *ppd_option;

option = ppdFindOption(ppd, "PageSize");
```

## See Also

`ppdFindChoice()`, `ppdFindMarkedChoice()`

# ppdIsMarked

## Usage

```c
int
ppdIsMarked(ppd_file_t *ppd,
    const char *keyword,
    const char *choice);
```

## Arguments

| Argument | Type | Description |
| --- | --- | --- |
| ppd | `ppd_file_t *` | PPD 文件 |
| keyword | `const char *` | 选项名称 |
| choice | `const char *` | 选项名称 |

## Returns

如果标记标记则返回 1，否则返回 0。

## Description

`ppdIsMarked()` 函数返回指定的选项是否被标记。

## Example

```c
#include <cups/ppd.h>

ppd_file_t *ppd;

printf("Letter size %s selected.\n",
ppdIsMarked(ppd, "PageSize", "Letter") ? "is" : "is not");
```

## See Also

`cupsMarkOptions()`, `ppdConflicts()`, `ppdIsMarked()`, `ppdMarkDefaults()`, `ppdMarkOption()`

# ppdMarkDefaults

## Usage

```c
void
ppdMarkDefaults(ppd_file_t *ppd);
```

## Arguments

| Argument | Type | Description |
| --- | --- | --- |
| ppd | `ppd_file_t *` | PPD 文件 |

## Description

`ppdMarkDefaults()` 函数标记 PPD 文件中的所有默认选项。

## Example

```c
#include <cups/ppd.h>

ppd_file_t *ppd;

ppdMarkDefaults(ppd);
```

## See Also

`cupsMarkOptions()`, `ppdConflicts()`, `ppdIsMarked()`, `ppdMarkDefaults()`, `ppdMarkOption()`

# ppdMarkOption

## 使用

```c
int
ppdMarkOption(ppd_file_t * ppd,
  const char *keyword,
  const char *choice);
```

| 参数 | 类型 | 说明 |
|---|---|---|
| ppd | `ppd_file_t *` | PPD 文件 |
| keyword | `const char *` | 选项名称 |
| choice | `const char *` | 选项值名称 |

## 返回

PPD 文件中的冲突数量。

## 描述

`ppdMarkOption()` 函数标记指定的选项值。

## 示例

```c
#include <cups/ppd.h>

ppd_file_t *ppd;

ppdMarkOption(ppd, "PageSize", "Letter");
```

## 另请

`cupsMarkOptions()`, `ppdConflicts()`, `ppdIsMarked()`, `ppdMarkDefaults()`, `ppdMarkOption()`

# ppdOpen

## 使用

```c
ppd_file_t *
ppdOpen(FILE *file);
```

## 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| file | `FILE *` | 要读取的文件 |

## 返回

指向 PPD 文件结构体的指针；如果无法读取 PPD 文件，则返回 NULL。

## 描述

`ppdOpen()` 函数从指定的文件读取 PPD 文件到内存中。

## 示例

```c
#include <cups/ppd.h>

ppd_file_t *ppd;
FILE *file;

file = fopen("filename.ppd", "rb");
d = ppdOpen(file);
close(file);
```

## 另请

`ppdClose()`, `ppdOpenFd()`, `ppdOpenFile()`

# ppdOpenFd

## 使用

```c
ppd_file_t *
ppdOpenFd(int fd);
```

## 参数

| 参数 | 类型 | 说明 |
| fd | `int` | 用于读取的文件描述符 |

## 返回

指向 PPD 文件结构体的指针；如果无法读取 PPD 文件，则返回 NULL。

## 描述

`ppdOpenFd()` 函数从指定的文件描述符读取 PPD 文件到内存中。

## 示例

```c
#include <cups/ppd.h>

pd_file_t *ppd;
int
fd;

fd = open("filename.ppd", O_RDONLY);
ppd = ppOpenFd(fd);
close(fd);
```

## 另请

`ppdClose()`, `ppdOpen()`, `ppdOpenFile()`

# ppdOpenFile

## 使用

```c
ppd_file_t *
ppdOpenFile(const char *filename);
```

## 参数

| 参数 | 类型 | 说明 |
| filename | `const char *` | 要读取的文件 |

## 返回

指向 PPD 文件结构体的指针；如果无法读取 PPD 文件，则返回 NULL。

## 描述

`ppdOpenFile()` 函数从命名的文件读取 PPD 文件到内存中。

## 示例

```c
#include <cups/ppd.h>

pd_file_t *ppd;

ppd = ppdOpenFile("filename.ppd");
```

## 另请

`ppdClose()`, `ppdOpen()`, `ppdOpenFd()`

# ppdPageLength

## 使用

```c
float
ppdPageLength(ppd_file_t *ppd,
const char *name);
```

## 参数

| 参数 | 类型 | 说明 |
|---|---|---|
| ppd | `ppd_file_t *` | PPD 文件 |
| name | `const char *` | 介质尺寸名称 |

## 返回

指定页面尺寸以磅（points）为单位的长度；如果页面尺寸不存在则返回 0。

## 描述

`ppdPageLength()` 函数返回指定页面尺寸的长度。

## 示例

```c
#include <cups/ppd.h>
```

```c
ppd_file_t *ppd;

printf("Length = %.f\n", ppdPageLength(ppd, "Letter"));
```

## 另请

`ppdPageLength()`, `ppdPageSize()`, `ppdPageWidth()`

# ppdPageSize

## 使用

```c
ppd_size_t *
ppdPageSize(ppd_file_t *ppd,
    const char *name);
```

## 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| ppd | `ppd_file_t *` | PPD 文件 |
| name | `const char *` | 介质尺寸名称 |

## 返回

指向指定页面尺寸以磅（points）为单位的尺寸记录的指针；如果页面尺寸不存在则返回 NULL。

## 描述

`ppdPageSize()` 函数返回指定页面尺寸的尺寸记录。

## 示例

```c
#include <cups/ppd.h>

ppd_file_t *ppd;
ppd_size_t *size;
```

## CUPS 函数

```c
size = ppPageSize(ppd, "Letter");
if (size != NULL) {
  printf(" Width = %.0f\n", size->width);
  printf("Length = %.0f\n", size->length);
  printf(" Left = %.0f\n", size->left);
  printf(" Right = %.0f\n", size->right);
  printf(" Bottom = %.0f\n", size->bottom);
  printf(" Top = %.0f\n", size->top);
}
```

## 另请

`ppdPageLength()`, `ppdWidth()`

# ppdWidth

## 使用

```c
float
ppdWidth(ppd_file_t *ppd,
const char *name);
```

## 参数

| 参数 | 类型 | 说明 |
| --- | --- | --- |
| ppd | `ppd_file_t *` | PPD 文件 |
| name | `const char *` | 介质尺寸名称 |

## 返回

指定页面尺寸以磅（points）为单位的宽度；如果页面尺寸不存在则返回 0。

## 描述

`ppdWidth()` 函数返回指定页面尺寸的宽度。

## 示例

```c
#include <cups/ppd.h>
```

```c
ppd_file_t *ppd;

printf("Width = %.f\n", ppdWidth(ppd, "Letter"));
```

## 另请

`ppdPageLength()`, `ppdWidth()`

# 前言

大多数软件的许可证设计旨在剥夺你分享和更改它的自由。相比之下，GNU 通用公共许可证（GNU General Public License，简称 GPL）旨在保证你分享和更改自由软件的自由——确保软件对所有用户都是自由的。本通用公共许可证适用于自由软件基金的大多数软件，以及任何其他承诺使用本许可证的程序作者。（另一些自由软件基金的软件受 GNU 库通用公共许可证保护。您可以将其应用于您的程序，）

当我们谈论自由软件时，我们指的是自由，而不是价格。我们的通用公共许可证旨在确保你拥有分发自由软件副本的自由（并且根据你的意愿，为此项服务进行更改），确保你能够获得源代码（或者在需要时获取它），你可以在新程序中更改软件或其部分，并且你知道如何进行这些操作。

为了保护你的权利，我们需要一些限制条件，以禁止任何人剥夺你的权利或要求你放弃权利。如果你分发软件副本或对其进行修改，这些限制条件将转化为相应的责任。



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```



可能会出现你的作品与通常不随操作系统一起提供的其他专有库的许可限制冲突的情况。这种冲突意味着你不能在你分发的可执行文件中同时使用这两者和该库。

## 7.
你可以将基于该库的作品的库设施与本许可未涵盖的其他库设施并放在同一个库中，并分发此类组合后的库，前提是单独分发基于该库的作品和其他库设施在在其他情况下是被允许的，并且前提是你执行了以下两点：

- a. 为组合后的库附带一份基于该库的相同作品的副本，且未与任何其他库设施组合。这必须根据上述节的条款进行分发。
- b. 在组合库的显著位置注明其部分是基于该库的作品，并说明在何处找到附带的未组合的相同作品。

# Common UNIX 打印系统许可协议

## 8.
你不能复制、修改、分许可、链接或分发该库，除非本许可另有明确规定。任何尝试复制、修改、分许可、链接或分发该库的尝试都是无效的，并将自动终止你在本许可项下的权利。然而，从你处获得本许可副本或权利的方，只要这些方仍保持完全符合规定，其许可就不会被终止。

## 9.
你没有要求接受本许可，因为你还没有签署它。然而，没有其他内容允许你修改或分发该库或其派生作品。如果你不接受本许可，法律禁止此类行为。因此，通过修改或分发该库（或基于该库的作品），你表示你接受进行此类操作，以及所有关于复制、分发该库或基于其作品的条款和条件。

## 10.
如果你重新分发该库（或任何基于该库的作品），接收者自动获得来自原始许可方的许可，允许根据这些条款和条件复制、分发或修改该库。你不能对接收者行使你授予的权利施加任何进一步的限制。你不对第三方遵守本许可的执行情况负责。

## 11.
如果由于法院判决、专利侵权指控或任何其他原因（但不限于专利问题），对你施加了（无论是通过法院命令、协议或其他方式）与本许可条件相冲突的条件，这些条件并不免除受本许可条款的约束。如果你无法通过这种分发来同时满足你在本许可项下的义务和任何其他许可义务，作为结果，你可能完全无法分发该库。例如，如果专利许可允许所有通过你直接或间接接收副本的人免特许费地重新分发该库，那么你同时满足该许可和本许可的唯一方法就是停止分发该库。

如果本节的任何部分在任何情况下被认为无效或不可执行，则该节的其余部分应适用，且该节整体在其他情况下应适用。

本节的目的不是诱导你侵犯任何专利或其他财产主张，或对任何主张的有效性提出异；本节唯一的目的是保护通过公共许可实践实施的自由软件分发系统的完整性。许多人对分发的广泛软件做出了慷慨贡献，这些软件的持续存在取决于对该系统的一致应用；作者/捐赠者决定是否愿意通过任何其他系统分发软件，被许可者不能强加这种选择。

本节旨在彻底清楚地说明被认为是本许可其余部分的后果。

## 12.
如果该库的分发和/或使用在某些国家受到专利或版权接口的限制，将该库置于本许可下的原始版权持有者可以增加一个明确的地理限制，排除那些国家，即在未被排除的国家内或国家之间允许分发。在这种情况下，本许可包含了该限制，如同写在本许可正文中一样。

# 附录

## 13.
自由软件基金可能会随时发布修订和/或新版本的库通用公共许可证。此类新版本将与当前版本相似，但在细节上可能不同，以解决新的问题或担忧。

每个版本都有相应的版本号。如果库指定了本许可的版本号以及“任何后续版本”，你可以选择遵循该版本或以后发布的任何后续版本的条款和条件。如果库未指定许可号，你可以选择自由软件基金发布的任何版本。

## 14.
如果你希望将库的部分整合到分发条件与本许可不兼容的其他自由程序中，请写信向作者寻求许可。我们有时会破例。我们的决定将受两个目标的指导：维护我们自由软件的所有衍生品的自由状态以及促进软件的共享和用用。

# 无保证

## 15.
由于该库是免费许可的，在适用法律范围内不对库提供任何保证。除非另有书面说明，版权持有者和/或其他方按“原样”提供库，不提供任何形式的明示或暗示保证，包括但不限于对可销性和特定用途适用性的暗示保证。对库的质量和性能的所有风险由你承担。如果库证明有缺陷，你承担所有必要服务、维修或修正的费用。

## 16.
在适用法律要求或书面同意的情况下，任何版权持有者或其他方在上述许可范围内修改和/或重新分发该库，均不对损害负责，包括因使用或无法使用该库而产生的任何一般、间接或后果性损害（包括但不限于数据丢失、数据变得不准确或你或第三方遭受的损失，以及库无法与任何软件运行），即使该持有者或其他方已告知损害的可能性。

# 条款和条件的结束

# 索引

# 符号

- `!` (逻辑非), MIME 类型, 317
- `#include` 指令, 220
- `+` (逻辑与), MIME 类型, 317
- `,` (逻辑或),, MIME 类型, 317

# A

- `AC CHECK HEADER` 命令, 226
- `AC CHECK LIB` 命令, 226
- `AC CONFIG HEADER` 命令, 226
- `AC DEFINE` 命令, 227
- `AC INIT` 命令, 225
- `AC MSG ERROR` 命令, 227
- `AC OUTPUT` 命令, 227
- `AC PROG CC` 命令, 226
- `accept` 命令, 配置直指令
- `classes.conf` 文件, 384
- `printers.conf` 文件, 420-421
- 打印任务, 60-62, 67
- 访问 (access)。另见安全
- 高级控制, 100-104
- 后端 (backends), 365
- 二进制发行版, 31
- 加密, 95-100
- 库, 220-221
- 日志文件, 105-106
- 打印机, 58-59
- 安全, 95
- 服务器, 94
- 源代码, 24
- `AccessLog` 配置指令 (`cupd.conf` 文件), 390
- 计费, 后端, 365
- 添加 (adding)。另见插入 (inserting)
- 基于地址的访问控制, 104
- 管理
  - 类, 232–235
  - 目标, 241–242
  - 打印机, 232–235
- 类 (classes), 63
- 命令行, 55–56
- Web 手册, 60–62, 65–66

Adobe

- DSC (文档结构规范), 306, 321–322
- 可携式文档格式 (PDF)。另见 PDF 文件
- PostScript 语言参考手册, 306, 322
- 进阶值 (栅化常数), 451–452
- 高级控制, 100–104。另见访问
- 算法
  - 误差扩散抖动, 357
  - Floyd-Steinberg 抖动, 358, 360–361
- `AllLayerlets` 类, 63
- `Allow` 配置指令 (`cupsd.conf` 文件), 390–391
- 直接允许 (Allow), 104
- `AllowUser` 配置指令
  - `classes.conf` 文件, 384
  - `printers.conf` 文件, 421
- CUPS API (应用程序编程接口)
  - API 变量常量, 437
  - HTTP 函数, 268–280
  - 函数, 232–246
  - 库, 224–226
  - HTTP 函数的限制, 439–440
  - 结构, 454–455
- 应用程序
  - CAP (Common AppleTek Package), 115
  - config 头文件, 227
  - 配置, 84, 86–87
  - 创建, 221–223
  - `cupsaddmb`, 117
  - 执行, 31
  - 安装, 30
  - Mac OS 客户端, 115–116
  - `Makefile`, 227–228
  - NetATalk, 116
  - 要求, 24–25
  - SAMBA, 116
  - 源代码, 29–30
  - 测试, 30
  - 升级, 31
  - Windows 客户端, 116–117
  - XINET/Spool, 115
- 应用 (applying)
  - 打印选项, 243–246, 248
  - 过滤器文本, 344–354
- AppSocket 打印, 44–45
- 架构
  - 过滤器, 309–310
  - 命令行参数, 310–311
  - 配置文件, 315
  - 副本生成, 314–315
  - 数据文件, 315
  - 环境变量, 311–312
  - 页面计费, 314
  - 安全考虑量, 312
  - 临时文件, 313
  - 用户/组, 312–313
- 通知器 (notifiers), 374
  - 命令行参数, 375
  - 配置文件, 377
  - 数据文件, 378
  - 环境变量, 375–376
  - 读取事件数据, 376
  - 重试, 378
  - 返回值, 376
  - 调度器消息, 376
  - 安全考虑量, 377
  - 临时文件, 377
  - 用户/组, 377
- 打印机驱动, 334
- 参数
  - 后端命令行, 364
  - 过滤器命令行, 310–311
  - 通知器命令, 315
- 数组, IP (网络打印协议), 134
- 属性 (attributions)
  - 约束, 337
  - CUPS, 159, 206
  - 设备类, 206
  - 设备信息, 207
  - 设备品牌和型号, 207
  - 设备 URI, 160
  - 任务字节限制, 160
  - 页面限制, 160
  - 任务配额, 160
  - 任务, 178–183
  - 成员名称, 160
  - 成员 URI, 160
- 属性 (attributes)
  - ppd 品牌, 207
  - ppd 品牌和型号, 207
  - ppd 名称, 207
  - ppd 自然语言, 207
  - ppd 类型, 161
  - ppd 类型掩码, 207
  - ppd 用户名称允许, 161
  - ppd 用户名称拒绝, 161
  - IPP (网络打印协议), 131-134, 295-296
  - 任务, 168, 172-173
  - ppd 字符集, 169
  - ppd 自然语言, 169
  - 副本数, 173
  - ppd 完成时间, 173
  - ppd 创建时间, 173
  - ppd 处理时间, 174
  - 任务, 174
  - ppd 详细状态, 174
  - ppd 文档错误, 174
  - ppd 持持续时间, 174
  - ppd ID, 169
  - ppd 打印数, 174
  - ppd 完成打印数, 174-175
  - ppd 字节, 175
  - ppd 已字节, 175
  - ppd 页面数, 175
  - ppd 完成页面数, 175
  - ppd 来自操作者的消息, 175
  - ppd 更多信息, 175
  - ppd 名称, 169
  - ppd 源用户名称, 169
  - ppd 打印机状态, 169
  - ppd URI, 170
  - ppd 优先级, 176
  - ppd 页面数, 176
  - ppd 状态, 170
  - ppd 状态消息, 176
  - ppd 状态原因, 170
  - ppd URI, 171
  - 介质, 176
  - 多文档处理, 176
  - 文档数量, 176
  - 中间任务数, 177
  - 打印机数量, 177
  - 请求方向, 177
  - 输出设备分配, 177
  - 页面范围, 177
  - 打印质量, 177
  - 打印机分辨率, 178
  - 幅面, 178
  - 完成时间, 171
  - 创建时间, 171
  - 处理时间, 172
  - 通知, 190, 192
  - 通知属性, 192
  - 通知属性支持, 192
  - 通知字符集, 192
  - 通知事件, 192
  - 通知默认事件, 192
  - 通知事件支持, 192
  - 通知任务 ID, 194
  - 通知租期时长, 194
  - 通知默认租期时长, 194
  - 通知租期时长支持, 194
  - 通知租期过期, 194
  - 通知最大事件支持, 194
  - 通知自然语言, 194
  - 通知打印机状态, 195
  - 通知打印机 URI, 195
  - 通知接收者, 195
  - 通知方案支持, 195
  - 通知序列号, 195
  - 通知订阅事件, 196
  - 通知订阅者用户名称, 196
  - 通知订阅 ID, 196
  - 通知文本, 196
  - 通知时间间隔, 196
  - 通知用户数据, 196
  - 打印机状态更改日期时间, 196
  - 打印机状态更改时间, 196
  - 打印机对象, 142-144
  - 字符集配置, 144
  - 字符集支持, 144
  - 支持, 156
  - 压缩支持, 145
  - 默认副本, 145
  - 副本支持, 145
  - 默认文档格式, 145
  - 文档格式支持, 146
  - 默认完成, 146
  - 支持, 147
  - 生成的自然语言支持, 147
  - ipp 版本支持, 148
  - 默认任务保持时间, 148
  - 任务保持时间支持, 148
  - 任务打印数支持, 156
  - 任务字节支持, 156
  - 任务页面数支持, 156
  - 默认优先级, 148
  - 优先级支持, 149
  - 页面数支持, 149
  - 默认介质, 149
  - 介质就绪, 149
  - 介质支持, 149
  - 默认多文档处理, 150
  - 多文档处理支持, 150
  - 多文档支持, 157
  - 多操作时间支持, 157
  - 配置的自然语言, 150
  - 默认数量, 150
  - 支持支持, 151
  - 操作支持, 151
  - 可选, 153–159
  - 请求, 151
  - 请求方向, 151
  - 每分钟页数, 157
  - 每分钟彩色数, 157
  - 角度支持, 151
  - pdl 覆盖, 151
  - 默认打印质量, 157
  - 打印质量支持, 157
  - 打印机当前时间, 158
  - 打印机驱动安装程序, 158
  - 打印机信息, 158
  - 接受任务, 151
  - 打印机位置, 158
  - 打印机品牌和型号, 158
  - 来自操作者的消息, 158
  - 打印机更多信息, 158
  - 打印机制造商, 158
  - 打印机名称, 151
  - 默认分辨率, 159
  - 打印机分辨率支持, 159
  - 打印机状态, 152
  - 打印机日期消息, 159
  - 打印机状态原因, 152–153
  - 打印机启动时间, 153
  - 打印机 URI 支持, 153
  - 队列任务数, 153
  - 参考 URI 方案支持, 159
  - 默认幅面, 154
  - 幅面支持, 154
  - URI 认证支持, 154
  - URI 安全支持, 154–155
- `AuthClass` 配置指令 (`cupsd.conf` 文件), 391
- 认证, 10–11。另见安全
- 组, 103–104
- HTTP, 276–278
- HTTP 常量, 437
- 关键字字符串, 154
- 用户, 101–102
- `AuthGroupName` 配置指令 (`cupsd.conf` 文件), 392
- `AuthType` 配置指令 (`cupsd.conf` 文件), 392
- Autoconf API 库, 224
- 生成配置, 228–229
- 自动化 IPP 请求, 298–299
- 打印队列配置, 111–112
- `AutoPurge` 配置指令 (`cupsd.conf` 文件), 393
- 可用打印机, 38, 70–71

# B

- 后端 (backends), 15, 364
- 命令行参数, 364
- 独占访问, 365
- 页面计费, 365
- 重试, 365–366
- 基于脚本, 368–371
- 安全, 364
- 串口端口, 366
- 设备发现支持, 366–367
- 打开, 367–368
- 触摸任务, 368
- 写入数据到, 368
- 横幅选项, 75
- 页面, 49
- 基础认证 (Basic authentication), 11, 392
- 大端序, 131
- 二进制发行版, 31, 577
- 位, 打印机类型, 161
- `blackplot` 属性, 179
- 选项, 81
- 布尔值, 栅化常数, 449
- 亮度属性, 179
- 配置, 76
- 字符集属性, 169
- 自然语言属性, 169
- 客户端 (clients)
- `BrowseAddress`, 111, 393
- `BrowseAllow` 配置指令 (`cupsd.conf` 文件), 393–394
- `BrowseDeny` 配置指令 (`cupsd.conf` 文件), 394–395
- `BrowseInterval`, 110, 395
- `BrowseOrder` 配置指令 (`cupsd.conf` 文件), 395–396
- `BrowsePoll`, 112, 396
- `BrowseRelay`, 112, 397
- `BrowseShortNames` 配置指令 (`cupsd.conf` 文件), 397
- 浏览 (browsing), 214
- 构建 (building)
  - 应用程序, 29–30
  - 配置脚本, CUPS, 221–223
  - IPP 请求, 298–301

# 关闭

打印机, 59

栅化流, 355



+ 代码

  - IPP 操作代码码, 129-131
  - 打印机操作, 162
    - `Disable-Printer`, 165
    - `Enable-Printer`, 164
    - `Get-Jobs`, 162
    - `Get-Printer-Attributes`, 163
    - `Get-Printer-Supported-Values`, 164
    - `Pause-Printer`, 163
    - `Purge-Jobs`, 163
    - `Resume-Printer`, 163
    - `Set-Printer-Attributes`, 164

+ 源代码

状态, 135-137
校订份数, 71, 314
支持颜色的属性, 156
颜色
  - 颜色空间. Ce颜色空间
    - 黑色, 81
    - 色调, 79-80, 180
    - 顺序值 (栅化常量), 449
    - 配置文件, 461
    - 栅化颜色顺序, 326-327
    - 饱和, 080

+ 颜色空间
  - PPD 常量, 447
  - 栅化常量, 449-450

- Columbia AppleTalk 软件包 (CAP), 115, 369

列
  - 属性, 179
  - 配置, 78

- 命令行参数
  - 后端, 364
  - 过滤器, 310-311
  - 通知器, 375

- 任务, 84

打印机
  - 添加, 47
  - 类, 63
  - 配置, 48-49
  - 管理, 55-56
  - 状态, 83

+ 命令, 11

- `AC CHECK HEADER`, 226
- `AC CHECK LIB`, 226
- `AC CONFIG HEADER`, 226
- `AC DEFINE`, 227
- `AC INT`, 225
- `AC MSG ERROR`, 227
- `AC OUTPUT`, 227
- `AC PROG CC`, 226
- `accept`, 60
- `cancel`, 84
- `chmod`, 97
- `configure`, 228-229
- 配置 CUPS, 25-29
- `disable`, 59
- `enable`, 59
- `install`, 35
- `lp`, 11, 70
- `lipadmin`, 55-56, 63, 110
- `lipinfo`, 38
- `loptions`, 59, 82
- `lpr`, 11, 70
- `lprm`, 84
- `lplstat`, 70
- `opensql`, 97
- `papuf`, 370
- `reject`, 60
- 源代码, 24

通用 UNIX 打印系统许可协议
GNU 通用公共许可证, 577-582
许可摘要, 376
不作保证, 582
前言, 376
复制、分发和修改的条款, 578-579, 581-582

通信
  - 命令行参数, 364
  - 独占访问, 365
  - 打开串口端口, 367-368
  - 页面计数, 365
  - 重试, 365-366
  - 基于脚本的, 368-371
  - 安全, 364
  - 串口端口, 366-367
  - 停止任务, 368
  - 向串口端口写入数据, 368

编译
  - 调试支持, 27
  - 源代码, 29-30
  - 系统要求, 24-25

支持压缩的属性, 145
`config.h` 头文件, 227

配置
+ , 84-87
  - 亮度, 76
  - 每英寸字符数, 77
  - 客户端, 110
    - 自动配置打印队列, 111-112
    - 手动配置打印队列, 110
    - 轮询服务器, 112
    - Relay打印机, 112-113
    - 指定单服务器, 111
  - 列, 78
  - 配置脚本, 224-229
  - 指令。参见配置指令
  - 双面打印, 74
  - 驱动程序, 87
  - 加密, 95-100
  - gfiles, 92-93
  - 伽马校正, 77
  - GIMP, 85-86

# HTTP

+ 对象, 270-271
- 请求, 273-274

# IPP

+ 对象, 292
- 端口, 263
- 每英寸行, 77
  - 边距, 78
  - 媒体选项, 73
  - Netscape, 86
  - 选项, 28-29, 93-94
  - 笔宽, 81
  - 精排打印, 78
打印机
  - 横幅选项, 75
  - 命令行, 48-49
  - 默认值, 59, 82
  - 描述, 56
  - 文档选项, 75-76
  - 设备, 39
  - 过滤器, 315
  - HP-GL/2 选项, 80-81
  - 图像选项, 78-80
  - 位置, 56
  - 修改, 57
  - 通知, 377
  - 选项, 71-74
  - 原始输出选项, 81
  - 保存选项, 82-83
  - 文本选项, 77
+ CUPS, 116
- 安全, 95
- 串口, 51
- 服务指令, 93
- 源代码, 25-30
- 来源, 73
- 特定打印机, 82
- Star Office, 86-89
- 订阅, 201-202
- 类型, 73
- Web 浏览器, 94

# 配置指令

  - `classes.conf`, 384-389
  - `client-conf` 文件, 393
  - `cupsd.conf` 文件
  - `Allow`, 390-391
  - `AuthClass`, 391
  - `AuthGroupName`, 392
  - `AuthType`, 392
  - `BrowseAddress`, 393
  - `BrowseAllow`, 393-394
  - `BrowseDeny`, 394
  - `BrowseInterval`, 395
  - `BrowseOrder`, 394-395
  - `BrowsePoll`, 395
  - `BrowsePort`, 396
  - `BrowseRelay`, 396
  - `BrowseShortNames`, 397
  - `BrowseTimeout`, 397
  - `Classification`, 398
  - `DataDir`, 398
  - `DefaultCharset`, 399
  - `DefaultLanguage`, 399
  - `Deny`, 399
  - `DocumentRoot`, 400
  - `Encryption`, 400-401
  - `ErrorLog`, 401
  - `FilterLimit`, 401
  - `FontPath`, 402
  - `Group`, 402
  - `HostNameups`, 402-403
  - `ImplicitClasses`, 403
  - `KeepAlive`, 403
  - `KeepAliveTimeout`, 404
  - `Limit`, 404
  - `LimitExcept`, 404
  - `RequestRequestBody`, 405
  - `Listen`, 405
  - `Location`, 405-406
  - `LogLevel`, 406
  - `MaxClients`, 407
  - 任务, 407
  - `JobsPerPrinter`, 407-408
  - `JobsPerUser`, 408
  - `LogSize`, 408
  - `RequestSize`, 409
  - `Order`, 409
  - `PageLog`, 409
  - `Port`, 410
  - `PreserveJobFiles`, 411
  - `PreserveJobHistory`, 410
  - `Pragmatic`, 411
  - `PrintFormat`, 411-412
  - `RemoteRoot`, 412
  - `RequestRoot`, 412
  - `RIPache`, 412-413
  - `RunAsUser`, 413
  - `Satisfy`, 413
  - `ServerAdmin`, 414
  - `ServerBin`, 414
  - `ServerCertificate`, 414
  - `ServerKey`, 415
  - `ServerName`, 415
  - `ServerRoot`, 416
  - `SSLListen`, 416
  - `SSLGroup`, 416
  - `SystemPort`, 416
  - `TempDir`, 417
  - `Timeout`, 417
  - `User`, 417-418

# PPD, 447-448

- 栅化, 449-452
- 完成, 428
- 头文件, 442-443
- 任务状态, 429
- 操作, 429-431
- 方向, 431
- 打印机站点, 431
- 质量, 431-432
- 分辨率单位, 432
- 状态码, 432-433
- 标签, 433-434
- 约束属性, 337
- 内容，查看, 252-253, 255-256
- `CONTENT_TYPE` 环境变量
  - 过滤器, 311

转换
  - 文件, 314, 306. 另参见文件
  - PPD 文件, 334
  - 约束属性, 337
  - 字体, 340
  - 选项, 338-339
  - 页面尺寸, 339
  - 打印机标识节, 335-336

转换文件 (MIME), 318-319

份
  - 参数, 310
  - 属性, 173
  - 校订, 71
  - 生成, 314-315
  - 多份, 70-71
  - 默认份数, 145
  - 支持的份数, 145
  - `copypage` 操作, PostScript 输出, 322
  - tribute, 179
  - `CR` (回车), 335

`Create-Job` 操作, 185
`Create-Job-Subscription`, 198
`Create-Printer-Subscription`, 197

CUPS (通用 UNIX 打印系统).
另参见

冲突
  - PPD 文件选项, 259
  - 连接, 94

常量
  - 头文件
    - 字符编码, 436
    - CUPS 版本, 437
    - HTTP, 337-442
    - IPP, 442-443
    - 消息, 443-449
  - API 版本, 437
  - , 30
  - 属性, 159, 206. 另参见
  - 类, 206
  - 设备信息, 207
  - 设备制造和型号, 207
  - 设备 URI, 160
  - 任务限制, 160
  - 页面限制, 160
  - 配额, 160
  - 成员名称, 160
  - 成员 URI, 160
  - ppd-制造, 207
  - ppd-制造和型号, 207
  - ppd-名称, 207
  - ppd-自然语言, 207
  - 打印类型, 161
  - 打印类型掩码, 207
  - 请求用户允许, 161
  - 请求用户拒绝, 161
  - 浏览协议, 214
  - 扩展选项, 207
  - `CUPS-Accept`, 211
  - `CUPS-Add-Class`, 210-211
  - `CUPS-Add-Device`, 213
  - `CUPS-Add-Printers`, 209
  - `CUPS-Delete-Class`, 211
  - `CUPS-Delete-Device`, 214
  - `CUPS-Delete-Printers`, 209
  - `CUPS-Get-Classes`, 210
  - `CUPS-Get-Default`, 208
  - `CUPS-Get-Devices`, 212
  - `CUPS-Get-PPDs`, 212
  - `CUPS-Get-Printers`, 208
  - `CUPS-Move-Job`, 213
  - `CUPS-Reject-Jobs`, 211
  - `CUPS-Set-Default`, 212
  - 接口, 165
  - Print Pro, 176
  - CUPS, 17-18
  - CUPS, 19-20
  - 任务属性, 178
  - 亮度, 179
  - 列, 179
  - 过滤器, 179
  - 伽马, 180
  - 色调, 180
  - 任务计费, 180
  - 任务来源, 180
  - lp, 181
  - 页面底部, 181
  - 页面标签, 181
  - 页面左侧, 181
  - 页面右侧, 181
  - 页面设置, 181
  - 页面顶部, 182
  - 笔宽, 182
  - 位置, 182
  - ppi, 182
  - 精排, 182
  - 饱和度, 183
  - 缩放, 183
  - wrap, 183
  - 库, 229
  - 许可协议, 576
  - 低级 API, 268-280
  - 之前的安装, 33-34
  - 编程, 220
  - Autoconf, 224-226
  - `config.h` 头文件, 227
  - 创建应用程序, 221-223
  - 检测 API 库, 224
  - 生成配置脚本, 228-229
  - 头文件, 220
  - 库, 221
  - `Makefile`, 227-228
  - 资源, 220
  - 邮件列表, 20
  - 新闻组, 211
  - 网站, 222

服务器
  - 配置选项, 92-94
  - 加密, 95-98, 100
  - 修改配置, 92-93
  - 重启, 93
  - 安全, 95
  - 服务指令, 93
  - Web 浏览器, 94
  - 支持, 577
  - 技术, 10-11
  - 后端, 15
  - 类, 12
  - 客户端, 11-12
  - 驱动程序, 14
  - 过滤器, 13-14
  - 任务, 12
  - 网络, 15-16
  - 服务器, 11-12
  - 升级, 35
  - Web 界面, 11
- 网站, 576

# CUPS-Accept-Jobs 操作

`CUPS-Accept-Jobs` 操作, 211
`CUPS-Add-Class` 操作, 210-211
`CUPS-Add-Device` 操作, 213
`CUPS-Add-Printers` 操作, 209
`CUPS-Delete-Class` 操作, 211
`CUPS-Delete-Device` 操作, 214
`CUPS-Delete-Printers` 操作, 209
`CUPS-Get-Classes` 操作, 210
`CUPS-Get-Default` 操作, 208
`CUPS-Get-Devices` 操作, 212
`CUPS-Get-PPDs` 操作, 212
`CUPS-Get-Printers` 操作, 208
`CUPS-Move-Job` 操作, 213
`CUPS-Reject-Jobs` 操作, 211
`CUPS-Set-Default` 操作, 212

## 分发

## 601

- `cups_job_t` 结构, 454
- `cups_lang_t` 结构, 454
- `cups_option_t` 结构, 455
- `CUPS_SERVERROOT` 环境变量
- 过滤器 (filters), 311
- 通知器 (notifiers), 375
- 当前选项，查看, 82
- 当前服务器, 262
- 自定义
  - 打印机, 71-74
    - banner 选项, 75
    - 文档选项, 75-76
    - HP-GL/2 选项, 80-81
    - 图像选项, 78-80
    - 原始输出选项, 81
    - 保存选项, 82-83
    - 文本选项, 77
- 服务器, 111
- CutMedia 值 (栅化内容), 451
- 选项, 83
- 打印机, 59-63
- Deny 配置指令 (`cupsd.file`)
- Deny 指令, 104
- DenUser 配置指令
- `classes.conf` 文件, 385
- `printers.conf` 文件, 421–422
  - 描述，配置打印机, 56
- 目的地 (destinations), 241-242
- 销毁 HTTP 对象, 271
- 检测
  - API 库, 224
  - Autoconf, 224-226
  - `device-class` 属性, 206
  - `device-info` 属性, 207
  - `device-make-and-model` 属性, 207
  - `device-uri` 属性, 160
  - 设备 (devices)
    - 后端 (backends), 366–367
    - 文件, 39, 367–368
    - HTTP, 39–40
    - IPP, 39–40
    - LPD, 40–42
    - 打印机, 38–45, 56
    - 选择, 49
    - 串口, 42–43
    - SMB, 43–44
    - 套接字 (socket), 44–45

## D

- 数据文件过滤器, 315, 378
- `DataDir` 配置指令 (`cupsd.file`), 398



- `date-time-at-completed` 属性, 173

- `date-time-at-creation` 属性, 173

- `date-time-at-processing` 属性, 174

- Debian 分发, 34–35

- `DEBUG:messages`

  - 过滤器, 313

  - 通知器, 376

  - 调试, 27

- `DefaultChart` 配置指令 (`cupsd.conf` 文件), 399

- `DefaultClass` 指令 (`classes.conf` 文件), 385

- `DefaultLanguage` 配置指令 (`cupsd.conf` 文件), 399

- `DefaultPrinter` 配置指令 (`printers.conf` 文件), 421

- `defaults`. *另需参见* options;

- 配置, 93

- 笔宽, 81

- 打印机, 59, 82

- 服务器, 111

- 删除

  - 类 (`classes`), 66

  - IPP 对象, 292

- `DeviceURI` 配置指令 (`printers.conf` 文件), 422

- `DeviceURI` 环境变量 (过滤器), 311

  - 对话框

  - 驱动安装, 88

  - 打印机连接, 89

  - 打印机属性, 89

  - 摘要认证, 11, 392

  - 指令, 加密, 99

  - 指令. *参见* 配置指令

- 目录, 398

- 禁用 (`disable`), 命令, 59

- 禁用打印机 (`Disable-Printer`) 操作, 165

- 发现, 366–367

- 分发 (`distribution`)

  - 二进制, 31

  - Debian, 34–35

  - 可移植的, 32

  - RPM, 33

- 抖动 (`dithering`), 添加, 356–362

- 文档打印应用 (`DPA`), 123

- 文档结构规范 (`DSC`), 306, 321–322

- `document-format-default` 属性, 145

- `document-format-supported` 属性, 146

- `DocumentRoot` 配置指令 (`cupsd.conf`), 400

- `doc`

  - 加密, 71

  - IPP, 126

  - 多份副本, 70–71

  - 选项, 75–

  - 打印, 70

- 域加密, 11

- 双面打印, 74

- 下载打印机驱动, 46

- `DPA` (文档打印应用), 123

- 驱动安装对话框, 88

- 驱动程序 (`Drivers`). *另需参见* 过滤器

  - 配置, 87

  - 下载, 46

  - HP 打印机, 341–347, 349–364

  - HP-PCL 栅化, 362

  - 打印机, 13–45–46

- 添加抖动, 356–362

- 架构, 334

- 修改, 57

- PPD 文件, 334–340

- 读取栅化图像, 355–356

- `DSC` (文 结构规范), 306, 321–322

- DVI 文件，转换为 PostScript 打印, 319–320

- `dvitops` 过滤器脚本, 319–320

## E

- Easy Software Products, 577

- 电子邮件, 378

- 启用 (`enable`) 命令, 59

- 启用打印机 (`Enable-Printer`) 操作, 164

- 启用 (`enabling`)

  - 高级访问控制, 100–104

  - 加密, 28, 98–100

  - 通知支持, 27

  - 可选功能, 28

  - SLP 支持, 28

- 编码 (`encoding`)

  - 字符编码, 436

  - HTTP 常量, 437

  - 加密, 10–11, 95–100. *另需参见* 安全

  - HTTP 常量, 438

  - 支持, 28, 261–262

  - 升级 HTTP, 279

- 加密配置指令 `client.file`, 389

- `cupsd.conf`, 400–401

- 印度人, 131

- 增强安全性, 95. *参见* 安全

- 环境变量

  - 过滤器, 311–312

  - 通知器, 375–376

- 错误处理

  - 函数, 264

  - HTTP, 276

  - 误差扩散抖动算法, 357

  - `Error.Log` 配置指令 (`cupsconf.file`), 401

  - 错误日志, 46

- `ERROR:messages`

  - 过滤器, 313

  - 通知器, 376

- ESP Print Pro, 17

- 偶数页，选择, 76

- 数据，读取通知器, 376

- 独占访问, 365

- 执行 (`execution`)

  - 应用, 31

  - 二进制分发, 31

- 扩展 (`extensions`)

  - IPP, 125

  - 操作, 207

  - `CUPS-Accept-Join`, 211

  - `CUPS-Add-Class`, 210–211

  - `CUPS-Add-Device`, 213

  - `CUPS-Add-Printers`, 209

  - `CUPS-Delete-Class`, 211

  - `CUPS-Delete-Device`, 214

  - `CUPS-Delete-Printers`, 209

  - `CUPS-Get-Class`, 210

  - `CUPS-Get-Default`, 208

  - `CUPS-Get-Devices`, 212

  - `CUPS-Get-PPDs`, 212

  - `CUPS-Get-Printers`, 208

  - `CUPS-Move-Job`, 213

  - `CUPS-Reject-Job`, 211

  - `CUPS-Set-Default`, 212

## F

- 故障操作, 113–114

- 字段名常量, (HTTP), 438–439

- 文件, 304. *另需参见*

- 文件名参数 (MIME), 311

  - banner, 75

  - `config.header`, 227–328

  - 配置, 92–93

  - 过滤器, 315

  - 通知器, 377

  - 转换, 14

  - `conv` 文件, 318–319

  - 数据文件, 315

  - 通知器, 376

  - 设备, 39, 367–368

  - DVI, 319–320

  - 加密, 71

  - 过滤器, 304. *另需参见*

  - 字体, 27

  - 头部, 220

  - 图像, 221

  - 库, 220–221

  - 日志, 105

  - 访问, 105–106

  - 错误, 106

  - 页面, 107

  - 多份副本, 70–71

  - banner, 75

  - 配置, 71–74

  - 文档, 75–76

  - HP-GL/2, 80–81

  - 图像, 78–80

  - 原始输出, 81

  - 保存, 82–83

  - 文本, 77

  - PPD, 334–340

  - 配置, 337

  - groups/options, 251–260

  - 加载, 249

  - 选项, 75–83

  - 页面, 339

  - 打印机部分, 335–336

  - 释放, 249

  - , 348

  - 更新, 361–362

  - 查看, 249

  - PPD 限制, 347–348

  - `printers.conf`, 421–422

  - 打印, 70

  - 栅化图像, 355–356

  - 安全, 312

  - 临时端口, 364

  - 过滤器, 315

  - 通知器, 312–313

  - 配置, 312–313

  - 环境变量, 311–312

  - 数据, 315–316

  - 安全, 312–313

  - 过滤器, 311–312

  - 通知器, 375–376

  - 设备, 39, 367–368

  - DVI, 319–320

  - 加密, 71

  - 过滤器, 304. *另需参见*

  - 字体, 27

  - 头部, 220

  - 图像, 221

  - 库, 220–221

  - 日志, 105

  - 访问, 105–106

  - 错误, 106

  - 页面, 107

  - 多份副本, 70–71

  - banner, 75

  - 配置, 71–74

  - 文档, 75–76

  - HP-GL/2, 80–81

  - 图像, 78–80

  - 原始输出, 81

  - 保存, 82–83

  - 文本, 77

  - PPD, 334–340

  - 配置, 337

  - groups/options, 251–260

  - 加载, 249

  - 选项, 75–83

  - 页面, 339

  - 打印机部分, 335–336

  - 释放, 249

  - , 348

  - 更新, 361–362

  - 查看, 249

  - PPD 限制, 347–348

  - `printers.conf`, 421–422

  - 打印, 70

  - 栅化图像, 355–356

  - 安全, 312

  - 临时端口, 364

## 索引

- 管理打印任务, 236

- 应用打印选项, 243-246

- 识别目的地, 241-242

- 回调, 263

- `cupsDefault()`, 221-223

- `cupsGetPrinters()`, 221-223

- `cupsNotifySummary()`, 379

- `cupsNotifyText()`, 379

- `cupsRasterClose()`, 355

- `cupsRasterOpen()`, 355

- `cupsRasterReader()`, 355

- `cupsRasterPixels()`, 356

- 当前服务器, 226

- 错误处理, 264

- `free()`, 379

- `gets()`, 377

- HTTP, 268–280

- `httpDecode()`, 375

- IPP, 285

- CUPS 低级 API, 268

- 对象结构, 285, 288-291

- `ippReadFile()`, 378-379

- `malloc()`,, 223

- PPD 文件, 248

- groups/options, 251–260

- 加载文件, 249

- 释放内存, 249

- 取回文件, 248

- 查看结构, 249, 251

- 栅化读取, 355–356

- `sprintf()`, 377

- `strcat()`, 377

- `strpy()`, 377

- 用户名, 262

- `WriteEpilogue()`, 341

- `WritePage()`, 344

- `WriteProlog()`, 341-443

## G

- `gamma`

  - 属性, 180

  - 修正, 77

- 支持生成的自然语言 `generated-natural-language-supported`

  - 属性, 147

- 生成配置脚本, 228-229

- `Get-JobAttributes` 操作, 186

- `Get-Jobs`

  - 操作, 162

  - 响应, 139

- `Get-Notifications`, 200

- `Get-PrinterAttributes`, 163

- `Get-Supported-Values` 操作, 164

- `Get-SubscriptionAttributes`, 198-199

- `gets` 函数, 377

- Ghostscript

  - ESP Ghost 项目 (SourceForge) Web

  - 站点, 308

  - `pstoraster` 过滤器, 308-309

- GIMP, 85–86

- GNU Octave, 224-226

- GNU General Public License, 577-582

- 许可证摘要, 576

- 无 WARRANTY, 582

- 序言, 578

# Info 配置指令

# 索引

# 605

复制、分发和修改的条款，578-579, 581-582

图形用户界面。见 GUI

组配置指令 (`cupsd.conf` 文件), 402

HP-GL/2, 80-81

`hpgltops`, 305, 328–331

初始化, 328-331

HP-PCL 栅化驱动程序, 362

`hpgltops` 文件过滤器, 305, 328-331

HTTP (超文本传输协议), 11, 123

+ 认证, 103-104

`AuthGroupName` 配置指令 (`cupsd.conf` 文件), 392

过滤器架构, 312

IPP, 131–134

`potifier` 架构, 377

PPD 文件, 251–253, 255–260

`ppd_group_t` 结构体, 460

+ 常量

认证, 437

编码, 437

加密, 438

HTTP 字段名, 438-839

Keep-Alive, 439

限制, 439-440

状态, 440

状态码, 440-442

版本号, 442

设备, 39–440

函数, 268–280

`http_t` 结构体, 445–456

xrequests, 128

GUI (通用用户界面), 16

ESP Print Pro, 17

GKUI, 17–18

KUPS, 17–18

QtCUPS, 19

XPP, 19-20

`httpDecode()` 函数, 375

hue。另见 colors

属性, 180

修改, 79–80

超文本传输协议。见 HTTP

# H

haltoning。见抖抖。

AC CONFIG HEADER 命令, 226

`config.h` 文件, 227–228

+ 常量

字符编码, 436

CUPS-API 版本, 437

HTTP: 437–438

HTTP: 438–442

IPP: 442–443

消息, 443–447

PPD, 447–448

栅化, 449–452

+ `ipp_request_t` 结构体, 457

`ipp_t` 结构体, 456

栅化页, 324–327

读取, 335

请求, 129–131

搜索, 27

# I

识别, 335–336

IETF (互联网工程任务组), 122

图像

+ 抖动, 356–358, 360–362

库, 221

选项, 78–80

栅化, 355–356。另见栅化图像

`imagetof` 文件过滤器, 305

`imagetaster` 文件过滤器, 302

实现。另见配置

Floyd-Steinberg 算法, 358–361

+ Web 浏览器, 281–282, 284

隐式类, 12, 113

`ImplicitClasses` 配置指令 (`cupsd.conf` 文件), 403

`indp` 通知方案, 204

历史记录, 122

保持作业操作, 186

`HostNameLookups` 配置指令 (`cupsd.conf` 文件), 402–403

`Info` 配置指令

`printers.conf` 文件, 422

HP (惠普) 打印机, 341–345, 347, 349–354

# INFO:messages

过滤器

通知器, 376

正在插入

目标地, 242

抖动, 256–362

选项, 239–240

打印机, 55–56

命令行, 47

Web, 49–51, 64

值, 292–295

安装命令, 35

安装。另见配置

应用程序, 30

二进制分发, 31

Debian 分发, 34

hP-PCL 栅化驱动程序, 362

可移植分发, 32

之前的安装, 33–34

RPM 分发, 33

脚本, 370

从源码, 24

配置, 25–29

系统要求, 24–25

实例, 83

接口, 16

ESP Print Pro, 17

GTkLP, 18

KUPS, 18

打印机设备, 38–45

QtCUPS, 19

Web, 11

+ 添加打印机, 64

管理打印机, 60–66

IPP, 19–20

互联网分配机构 (IANA) 网站, 316

互联网工程任务组 (IETF), 122

互联网打印协议。见 IP

基于 IP 的访问控制, 11

IPP (互联网打印协议)。另见打印

+ 数组, 134

属性, 131–134

设备, 39–40

扩展, 125

完成命令, 428

函数, 285

+ CUPS 低级 API, 268

对象结构, 285–281

组, 131–134

历史, 122

创建, 123–124

LPD, 122–131

作业状态常量, 429

通知方案, 202–204

通知器

添加值, 292–295

创建, 292

删除, 292

模型, 124

搜索属性, 295–296

尺寸, 295

操作

代码, 129–131

常量, 429–431

端口, 263

打印机

状态常量, 331

类型, 442–443

引用, 125–126

请求, 128

自动, 298–299

构建, 299–301

头部, 129–131

HTTP

优化, 301–302

发送, 296–297

分辨率, 432

响应, 134

多个对象, 137–139

读取, 298

状态码, 135–137

值标签, 137

服务器

配置选项, 92–94

加密, 95–98, 100

修改配置, 92–93

重启服务器, 93

安全, 95

服务指令, 93

Web 浏览器, 94

状态常量, 443



状态常量, 432–433

结构体, 456–458

# jobs 索引 607

订阅对象, 190

通知属性, 190–196

操作, 197–201

标签常量, 433–434

Windows 客户端, 117

支持的 版本, 148

ippget 通知方案, 203

`ippReadFile()`, 378-379

ISO 1075, 123

作业, 12

接受, 67

参数, 310

取消, 84

CUPS 属性, 178

blackplot, 179

亮度, 179

列, 179

cpi, 179

fitplot, 180

gamma, 180

hue, 180

计费属性, 180

源源主机, 180

Ipi, 181

页底部, 181

页标签, 181

页左侧, 181

页右侧, 181

页集, 182

页顶部, 182

宽度, 182

位置, 182

ppi, 182

精印, 182

饱和度, 183

缩放, 183

wnap, 183

`cups_job_t` 结构体, 454

加密, 71

Get-Jobs 响应, 139

历史, 410

管理, 236–238

对象, 168

操作, 183

Cancel-Job, 186

Create-Job, 185

Get-Job-Attributes, 186

Hold-Job, 186

Print-Job, 184

Print-URI, 184

Release-Job, 187

Restart-Job, 187

Send-Document, 185

Send-URI, 185

Set-Job-Attributes, 187–188

Validate-Job, 184

# J

+ 计费属性, 180
+ 文档访问错误属性, 174
+ 保持到默认属性, 174
+ 支持的保持属性, 148
+ 作业 ID 属性, 169
+ 打印数属性, 174
+ 完成的打印数属性, 174-175
+ 支持的打印数属性, 156
+ k 限制属性, 160
+ k 字节属性, 175
+ 支持的 k 字节属性, 156
+ 纸张数属性, 175
+ 完成的纸张数属性, 156
+ 操作员消息属性, 175
+ 作业更多信息, 175
+ 作业名称, 169
+ 源主机名, 180
+ 源用户名称, 169
+ 作业限制属性, 160
+ 打印机时间, 169
+ 打印机 URI, 170
+ 优先级属性, 170
+ 优先级属性, 176
+ 支持的优先级, 148
+ 计费周期, 160
+ 纸张数属性, 176
+ 默认纸张数, 149
+ 支持的纸张数, 149
+ 状态属性, 170
+ 状态消息, 176
+ 状态原因, 170
+ URI, 171

# JobSheets 索引

608

作业

可选属性, 172–173

副本数, 173

完成时间, 173

创建时间, 173

处理时间, 173

结束状态, 174

详细状态, 174

文档访问错误, 174

保持到, 174

打印数, 174

完成的打印数, 174-175

支持的打印数, 156

k 字节, 175

已 k 字节, 175

支持的 k 字节, 156

纸张数, 175

完成的纸张数, 156

操作员消息, 175

更多信息, 175

名称, 169

源主机名, 180

源用户名称, 169

限制属性, 160

打印机时间, 169

打印机 URI, 170

优先级属性, 170

优先级属性, 176

支持的优先级, 148

计费周期, 160

纸张数属性, 176

默认纸张数, 149

支持的纸张数, 149

状态属性, 170

状态消息, 176

状态原因, 170

URI, 171

媒体, 176

多文档处理, 176

文档数, 176

合并数, 177

份数, 177

输出设备分配, 177

页范围, 177

打印质量, 177

打印分辨率, 178

双面, 178

打印

类, 62

管理类, 63

拒绝, 62, 68

必需属性, 168

字符集属性, 169

自然语言属性, 169

## malloc() 函数

609

- 库, 220–221
- 小端序 (little endian), 131
- 加载 (loading)
- 均衡, 113-114
- PPD 文件, 249
- 本地证书认证, 11
- 位置，配置, 56
- 位置配置指令 (Location configuration directive)
  - classes.conf 文件, 387
  - cupsd.conf 文件, 405-406
  - printers.conf 文件, 423
  - LogLevel 配置指令 (cupsd.conf 文件), 406
  - API, 224
- Autoconf, 224–226
- config.h 头文件, 227
- cupsimage, 355–356
- 头文件, 220
- 许可证, 229
- nsl, 226
- 需求, 24–25
- 搜索, 27
- 套接字 (socket), 228

## 库通用公共许可证 (LGPL), 229

- 许可协议 (通用 UNIX 打印系统)
- ErrorLog 配置指令 (cupsd.conf 文件), 401
- 文件, 105–107
- MaxSize 配置指令 (cupsd.conf, 408)
- PageLog 配置指令 (cupsd.conf 文件), 409–410
- lp 命令, 70
- lpdadmin 命令, 55–56, 613
- LPD (行打印机守护进程), 15
  - 客户端, 114
  - 设备, 42
- IPP, 122–123
- lpi 属性, 181
- lpi 选项, 77
- lpinfo 命令, 38
- lpoptions 命令, 59, 82
- lpr 命令, 70
- lpm 命令, 84
- lipstat 命令, 70
  - GNU 通用公共许可证, 577–582
- 许可证摘要, 376
- 无保证 (NO WARRANTY), 382
- 前言 (Preamble), 378
- 复制、分发和修改的条款, 578–579, 581–582
- GNU 通用公共许可证, 583–588, 590
- 无保证 (NO WARRANTY), 590
- 前言, 583–584
- 复制、分发和修改的条款, 585–587, 590
- Limit 配置指令 (cupsd.conf 文件), 404
- LimitExact 配置指令 (cupsd.conf, 404)
- LimitRequestBody 配置指令 (cupsd.conf, 405)
- 限制 (limits)
- Mac OS, 115–116
- MailCommand 配置指令 (mailto 邮件通知器), 419
- 邮件列表, 20。另见 e-mail 通知器, 203, 378–379
- 配置指令, 318–419
  - cupsNotifySummary() 函数, 379
  - cupsNotifyText() 函数, 379
  - free(), 函数, 379
  - ippReadFile() 函数, 378–379
- Makefile, 25–29, 227–228
- malloc() 函数, 223
- HTTP, 439–440
- PPD 文件限制, 447–448
- 行打印机守护进程 (LPD), 15
- 换行 (LF), 335
- 行, 77
- Listen 配置指令 (cupsd.conf 文件), 405
  - 可用打印机设备, 38
- 可用打印机, 70–71
- 目的地, 241
- dvitoips 过滤器脚本, 319–320
- 邮件, 20

## 管理 (management)

- 类 (classes), 232-235
- 目的地, 241-242
- 打印机, 232-235
- 类, 63
- 命令行, 55-56
- Web 接口, 60-66
- 手动打印队列配置, 110
- 边距，配置, 78
- 标记 PPD 文件选项, 258
- MaxClients 配置指令 (cupsd.file), 407
- MaxJobs 配置指令 (cupsd.file), 407
  - MaxJobsPrinter 配置指令 (cupsd.file), 408
- MaxJobsUser 配置指令 (cupsd.file), 408
- MaxSize 配置指令 (cupsd.file), 408
- MaxRequestSize 配置指令 (cupsd.file), 409
- 媒体 (media)
  - 选项, 73
  - 值, 48
  - 媒体属性, 176
  - 媒体默认属性, 149
  - 媒体准备就绪属性, 149
  - 媒体支持属性, 149
  - 成员名称属性, 160
- 模型 (models)
  - IPP 对象, 124
  - 选择, 51
- 修改 (modification)
  - 类, 65
  - 色调, 79-80
  - 打印机, 55-61
  - 饱和度, 80
  - 服务器, 92-93
- 多媒体互联网交换 (Multimedia Internet Exchange)。另见 MIME 类型
  - 多份副本，打印, 70-71
  - 多个对象，添加, 239-240
  - 多个服务器，配置, 112
  - 多文档处理属性, 176
  - 多文档处理默认属性, 150
  - 多文档处理支持属性, 150
  - 多次操作超时, 157
- N
- 基于名称的访问控制, 104
- 名称 (names)
  - 设备, 38-45
  - 驱动程序, 45-56
  - 自然语言配置属性, 150
  - 导航打印机选项, 239-240
  - 网络, 116
  - 子网掩码, 390-391
  - Netscape，配置, 86
  - 网络, 15-16, 38
  - 新组, 21
- 通知器 (notifiers), 374
- 内存 (memory)
  - 目的地, 243
  - 选项, 240
- PPD 文件, 249
- 消息 (messages)
  - CUPS 消息计数, 443–447
  - 过滤器消息, 313
  - 调度消息 (通知器), 376
- 方法 (methods)
  - 加密, 99
  - HTTP, 271-272
- MIME (多媒体互联网交换), 315
- 架构, 374
- 命令行参数, 375
- 配置文件, 377
- 数据文件, 378
- 环境变量, 375-376
- 读取数据, 376
- 重试次数, 378
- 返回值, 376
- 调度器消息, 73

## 打开模式

- 索引, 611
- 安全考量, 377
- 临时文件, 377
- 用户组, 377
- 属性, 190
- 通知属性, 192
- 通知属性支持, 192
- 通知字符集, 192
- 通知事件, 192
- 通知默认事件, 192
- 通知事件支持, 192
- 通知任务 ID, 194
- 通知租期, 194
- 通知租期默认属性, 194
- 通知租期支持, 194
- 通知过期时间, 194
- 通知自然语言, 194
- 通知打印机时间, 195
- 通知接收者 URI, 195
- 通知方案支持, 195
- 通知序列号, 196
- 通知订阅者用户, 196
- 通知订阅 ID, 196
- 通知文本, 196
- 通知时间, 196
- 通知用户数据, 196
- 库, 226
- 任务数量, 176
- 任务交错任务, 177
- 限制属性, 177
- 限制默认值, 150

## 0

- 对象
  - HTTP
    - 创建, 270-271
    - 销毁, 271
  - IPP
    - 添加, 292-295
    - 创建, 292
    - 销毁, 292
    - 模型, 124
    - 查找, 295-296
    - 邮件, 378-379
    - 配置指令, 378-418
    - cupsNotifySummary() 函数, 379
    - cupsNotifyText() 函数, 379
    - free() 函数, 379
    - readFile() 函数, 377-379
    - 结构, 285
    - 任务, 168
    - 打印机, 142
    - 可选属性, 155-159
    - 要求属性, 142-144
    - 订阅, 192
    - 请求, 203-204
    - 页面, 76
    - 打开模式, 150
- 流 (streams), 355
- 端口, 367-368
- 源, 24
- SSL, 97
- 副本, 31
- 扩展, 31
- CUPS 任务, 211
- CUPS 打印机, 209
  - CUPS 类, 210
  - CUPS 打印机, 212
  - 属性, 212
  - 任务, 213
  - 状态, 214
  - 默认, 208
  - 获取, 212
  - PPD, 212
  - 任务, 183
  - 取消, 186
  - 打印机, 184
  - 禁用, 162
  - 启用, 16
- 暂停, 183
  - 恢复, 183
  - 属性, 184
  - 任务, 185
  - 订阅, 197
  - 创建任务, 198
  - 创建打印机, 197
  - 通知, 200
  - 获取属性, 198
  - 获取订阅, 198-199
  - 更新订阅, 199
  - 通知, 200-201
- 操作支持, 151
- 优化请求, 301-302
- 可选属性
  - 任务, 172-173
  - 副本, 173
  - 完成时间, 173
  - 创建时间, 173
  - 处理时间, 174
  - 结束, 174
  - 详细状态, 174
  - 文档访问错误, 174
  - 等待, 174
  - 打印次数, 174
  - 打印次数完成, 174-175
  - 字节, 175
  - 已处理字节, 175
  - 媒体页数, 175
  - 媒体页数完成, 175
  - 操作员消息, 175
  - 更多信息, 175
  - 优先级, 176
  - 任务单（页）, 176
  - 状态消息, 176
- 支持打印质量, 157
- 打印机当前时间, 158
- 打印机驱动程序, 158
- 打印机信息, 158
- 打印机位置, 158
- 根据型号识别打印机品牌, 158
- 操作员消息, 158
- 打印机更多信息, 158
- 厂商更多信息, 158
- 打印机默认分辨率, 159
- 打印机默认分辨率, 159
- 打印机状态消息, 159
- 支持的 URI 方案, 159
- 可选功能，启用, 28
- 选项。以及配置
- 添加, 239–240
- 黑白图, 81
- 亮度, 76
- 列, 78
- 配置, 28–29
- cpi, 77
- 删除, 83
- 适应绘图, 81
- 伽马, 77
- 色相, 79–80
- 横向, 73
- lpadmin 命令, 55–56
- lpi, 77
- 边距, 78
- 媒体, 73
- 每页份数, 76
- 页面范围, 75
- 页面设置, 76
- 位置, 79
- PPD 文件, 338–339
- 冲突, 259
- 标记, 258
- 纸张尺寸, 259–260
- 搜索, 257
- 预打印, 78
- 打印机
- 横幅选项, 75
- 配置, 71–74
- 文档选项, 75–76
- HP-GL/2 选项, 80–81
- 图像选项, 81
- 导航, 239–240
- 原始输出选项, 81
- 保存选项, 82–83
- 文本选项, 77
- 打印, 243–248
- 饱和度, 80
- 缩放, 79
- 服务器, 93–94
- 双面, 74
- 特定打印机, 82
- 值, 240
- 视图, 82
- 选项参数（过滤器）, 310–311
- 顺序配置指令 (cupsd.conf 文件), 409
- 顺序依赖值 (PPD), 448
- 方向。以及打印
- 配置, 73
- 栅格化方向值常量, 451
- 请求的方向属性, 177
- 默认请求的方向属性, 151
- 所请求的所请求的方向属性, 151
- 无方向 (IPP), 433
- 输出。打印
- 输出设备分配属性, 177
- 覆盖默认服务器, 111
- 视图, 10–11
- 后端, 15
- 类, 12
- 客户端, 11–12
- 驱动程序, 14
- 过滤器, 13–14
- , 12
- 网络, 15–16
- 服务器, 11–12
- 页面底部
- 属性, 181
- 选项, 78
- 页面标签属性, 181
- 页面左侧
- 属性, 181
- 选项, 78
- 页面范围属性, 173
- 页面右侧
- 属性, 181
- 选项, 78
- 页面设置属性, 181
- 页面顶部
- 属性, 182
- 选项, 78

## PageLimit 配置指令

- classes.conf 文件, 387



- `printers.conf` 文件, 423–424

- `cupsd.conf` 文件, 409–410

## 页面

+ 计费, 365

+ 范围, 75

+ 尺寸, 339

+ PPD 文件选项, 259–260

+ `ppd_size_1` 属性, 461

+ 页眉, 355

+ 日志, 105

+ 像素数据, 356

- 每分钟页数属性, 155

- 每分钟彩色页数属性, 157

- 支持的页数属性, 151

- PAGE:计费测量（过滤器）, 313–334

- `papmid` 命令, 370

- `paserverv`, 115

- 并行端口, 38–45

- `PATH` 环境变量

- 过滤器, 311

- 通知器, 375

- 暂停打印机, 163

- PDF (便携文档格式) 文件, 306–307

- `pdftops` 文件, 306–307

- 二进制分发, 577

- 配置指令, 419–420

- 打印, 70

- PDF 站点, 307

- `pdl` 覆盖支持, 151

- 墨水, 配置, 81

- 墨宽属性, 182

- 像素

- 每像素抖动算法, 357

- 读取, 356

- 绘图, 811

- 轮询服务器, 112

- 便携文档格式。见 PDF

- 端口, 262

- 浏览配置指令 (`cupsd.conf` 文件), 396

- IPP, 263

- 打印机设备, 38–45

- 串口, 366–368

- 栅格化指令 (`cupsd.file`), 416

- 位置属性, 182

- 图像定位, 79

- POST 请求, 128

- Postscript 文件

- Adobe 文档规范, 版本 3.0, 321–322

- , 306

- Adobe PostScript 手册, 306, 322

- PostScript 描述。见 PDF

- Postscript 打印机, 306, 322

- PPD (Postscript 打印机), 14, 334

+ 属性, 337

+ 色域, 447

+ 文件, 458–448

+ 限制, 447–448

+ 顺序依赖值, 448

+ 用户界面类型值, 448

+ 版本, 448

- 环境变量（文件）, 311

- 字体, 340

- 选项, 338–339

- 页面尺寸, 339

- 打印机识别, 335–336

- 组/选项, 251–260

- 加载, 249

- 释放, 249

- 获取, 248

- 视图, 249–251

- 结构, 458–461

- 更新, 361–362

- `ppd` 属性, 207

- `ppd` 制造和型号属性, 207

- `ppd` 名称属性, 207

- `ppd` 自然语言属性, 207

## 打印机

- 615

- 保存历史配置指令 (`cupsd.conf` 文件), 410

- 精美打印属性, 182

- 配置, 78

- 之前的安装, 33-34

- 打印任务, 184

- 默认打印质量属性, 177

- 支持的打印质量属性, 158

- URI 操作, 184

- Printcap 配置指令 (`cupsd.conf` 文件), 411

- Printcap 格式配置指令 (`cupsd.conf` 文件), 412

- 配置指令 (`classes.conf` 文件), 387

- 配置指令 (`printers.conf` 文件), 424

- 打印机连接对话框, 89

- `PRINTER` 环境变量（过滤器）, 311

- 属性对话框, 89

- 打印机状态 (IPP), 431

- 向导, 50

- 打印机组 (PWG), 122

- 打印机当前时间, 158

- 驱动程序属性, 158

- 打印信息属性, 158

- 正在接受属性, 151

- 打印机位置属性, 158

- 打印机制造和型号属性, 158

- 操作员消息属性, 158

- 更多属性, 158

- 厂商属性, 158

- 打印机名称属性, 151

- 打印机分辨率属性, 178

- 默认分辨率属性, 159

- 支持的分辨率属性, 152

- 状态更改日期时间, 196

- 状态更改时间, 196

- 状态消息属性, 159

- 状态原因属性, 152–153

- 打印机类型属性, 161

- 打印机类型掩码属性, 207

- 运行时间属性, 153

- 支持的 URI 属性, 153

- 见 CUPS: 打印

- 添加

- 命令行, 47

- Web, 49-51

- 属性, 159–161。见属性

- 参数（过滤器）, 310

- 后端, 15, 364

- 命令行参数, 365

- 独占访问, 365

- 开启串口端口, 367-368

- 页面计费, 365

- 重试, 366

- 安全, 364

- 串口, 366-367

- 停止任务, 368

- 写入, 368-371

- 类, 12, 62-63

- 关闭, 59

- 配置

- 命令行, 48-49

- 修改, 57

- Web, 51

- 自定义, 71-74

- 横幅选项, 75

- 文档选项, 75-76

- HP-GL/2 选项, 80-81

- 图像选项, 78-80

- 原始输出选项, 81

- 保存选项, 82-83

- 文本选项, 77

- 默认, 59

- 删除, 59-61

- , 56

- 设备, 56

- 驱动程序, 14

- 添加抖动, 356-362

- 架构, 334

- 下载, 46

- 修改, 57

- PPD 文件, 334-340

- 读取栅格图像, 355-356

- 文件, 39

- 过滤器, 13-14

- 添加抖动, 356-362

- 架构, 334

- 下载, 46

- 修改, 57

- PPD 文件, 334-340

- 读取栅格图像, 355-356

- 文件, 39

- 过滤器, 13-14

## 索引

- 66

- 打印机

- 最大任务配置指令 (`cupsd.conf` 文件), 408

- 修改, 61

- 网络, 15–16

- 可选属性, 155–159

- 方向, 73

- 队列, 15–16

- 删除, 60

- 服务器

- 轮询, 112

- 指定服务器, 111

- 服务, 232

- 管理打印任务, 236–238

- 应用选项, 243–248

- 管理类/打印机, 232–235

- 导航打印机, 239–240

- 打印文件, 235–236

- 解决方案, 10

- 测试页, 54–55, 62, 68

- Windows 客户端, 116–117

- 编程

- Autoconf, 224–226

- `config.h` 头文件, 227

- 创建应用, 221–223

- 检测 API 库, 224

- 生成配置服务器, 228–229

- 头文件, 220

- 库, 221

- Makerfile, 227

- 程序，见应用程序

- 协议

- 创建, 123–124

- CUPS 浏览, 214

- HTTP, 11, 123

- IPP

- 数组, 134

- 属性, 131–134

- 类, 12

- 客户端, 112

- 配置选项, 92–94, 117

- 创建, 123–124

- 驱动程序, 14

- 加密, 95–100

- 扩展, 125

- 过滤器, 13–14

- 组, 131–134

- 头部请求, 129–131

- 历史, 122

## 索引

- requests, 128

- responses, 134

- restarting servers, 93

- security, 95

- servers, 11-12

- service directives, 93

- status codes, 135–137

- value tags, 137

- Web browsers, 94

- LPD, 15, 114–123

- SLP, 28

- proxy servers, 279

- `postfiles` filter, 307–308

- `pstoraster` file filter, 308–309, 577

- Purge-Jobs operation, 163, 393

- PWG (打印工作组), 122

- HP-PCL raster drivers, 362

- output filters

    - 用于写入输出的函数, 323

    - `imagetonaster`, 306

    - `pstoraster`, 308-309

    - raster streams, 322–324

    - writing, 324–328

    - color orders, 326–327

    - colorspaces, 326

    - `pstoraster` filter, 577

- RIPCache configuration directive (`cupsd.conf` 文件), 412

- raster printer drivers, 355–356

- raw output, 81

- reading

## Q

- QtCUPS, 194

- qualities (IPP), 431–432

- `queued-job-account` attribute, 153

- queues

    - closing, 59

    - configuring, 110–112

    - implicit class, 113

    - printers, 38

    - devices, 38–45

    - drivers, 45–46

    - starting, 59

    - data, 272

    - images, 355–356

    - recipient-url argument (notifiers), 375

    - reference-uri-schemes-supported attribute, 159

- references, 126

- command, 60

- rejecting printing jobs, 60–62, 68

- relationships, IPP objects, 125

- relaying printers, 112–113

- Release-Job operation, 187

- releasing memory from options, 240

- QuotaPeriod configuration directive class.conf file, 338

    - printers.conf file, 424

- quotas, configuring, 58

- PPD files, 249

- remote queues, configuring, 110–111

- RemoteRoot configuration directive (`cupsd.conf` 文件), 412

- Renew-Subscription, 199

- ReplyTo configuration directive (mailto notifier), 419

- Request for Comment (RFC), 125

- requesting-user-named attribute, 161

- RequestRoot configuration directive (`cupsd.conf` 文件), 412

## R

- ranges, 75

- raster image process (RIP), 14

- raster images. 另见 images

- constants

    - advance values, 451–452

    - Boolean values, 449

    - color order values, 449

    - colorspaces, 449–450

    - CutMedia values, 451

    - sending, 450

    - jog values, 450

    - leading edge values, 452

    - open modes, 450

    - orientation values, 451

    - sync words, 450

- requests

    - headers, 456–457

    - HTTP

        - configuring, 273–274

        - obtaining, 274

        - sending, 271–272

    - IPP

        - automating, 298–299

        - building, 299, 301

        - headers, 129–131

        - HTTP, 128

        - optimizing, 301-302

        - sending, 296-297

- POST, 128

- required attributes

    - jobs, 168

        - attributes-charset, 169

        - attributes-natural-language, 169

        - job-id, 169

        - job-name, 169

        - job-originating-user-name, 169

        - job-printer-up-time, 169

        - job-printer-uri, 170

        - job-state, 170

        - job-reasons, 170

        - job-uri, 171

        - time-at-completed, 171

        - time-at-creation, 171

        - time-at-processing, 172

    - printer objects, 142

        - charset-configured, 144

        - charset-supported, 144-145

        - compression-supported, 145

        - copies-default, 145

        - copies-supported, 145

        - document-format-default, 145

        - document-formatting-supported, 146

        - finishing-default, 146

        - finishing-supported, 147

        - general-natural-language-supported, 147

        - ipp-versions-supported, 148

        - job-hold-until-default, 148

        - job-hold-until-supported, 148

        - job-priority-default, 148

        - job-priority-supported, 148

        - job-sheets-default, 149

        - job-sheets-supported, 149

        - media-default, 149

        - media-ready, 149

        - media-supported, 149

        - multiple-document-handling-default, 150

        - multiple-document-handling-supported, 150

        - natural-language-configured, 150

        - number-default, 151

        - number-supported, 151

        - operations-supported, 151

        - orientation-requested-default, 151

        - orientation-requested-supported, 151

        - pages-ranges-default, 151

        - printer-state, 152

        - printer-state-reasons, 152-153

        - printer-up-time, 153

        - printer-uri-supported, 153

        - queued-job-count, 153

        - sides-default, 154

        - sides-supported, 154

        - uri-authentication-supported, 154

        - uri-security-supported, 155

- requirements for installation, 245

- resolution, 79

- units, 432

- resources, 20

- Restart-job operation, 187

- retrieval

- RFC (Request for Comment), 125



- RIPCache configuration directive (`cupsd.conf` 文件), 412–413

- `RIP_CACHE` environment variable (filters), 311

- roles

    - command-line arguments, 364

    - exclusive access, 365

    - opening serial ports, 367–368

    - page accounting, 365

- stopping jobs, 368

- writing data, 368-371

- RPM distribution, installing, 33

- RunAsUser configuration directive (`cupsd.conf` 文件), 413

- running. 另见 execution

- security, 95

- advanced access control, 100-104

- backends, 364

- encryption support, 261-262

- files, 71

- filters, 312

- HTTP connections, 416

- keyword strings, 155

- log files, 105

- access, 105-206

- error, 106

- page, 107

- notifiers, 377

- printers, 58-59

- SAMBA, 116

- Satisfy configuration directive (`cupsd.conf` 文件), 413

- saturation

    - attribute, 183

    - modifying, 80

- saving

    - dest, 242

    - printer options, 82-83

- saturation

    - attribute, 183

    - plot option, 81

    - images, 79

- scheduler

    - `classes.conf` 文件, 384-389

    - `cupsd.conf` 文件, 396, 399

    - notifier scheduler messages, 376

    - `printers.conf` file, 420-425

- schemes

    - notification, 204

    - ippget notification, 203

    - mailto notification, 203

    - notification, 202-204

    - script-based backups, 368-371

- scripts

    - configure

        - creating, 224-226

        - generating, 228-229

        - installing, 370

    - searching

        - attributes, 295-296

        - destinations, 242

        - fonts, 27

        - header files, 27

        - libraries, 27

        - PPD file options, 255

- selecting

    - clients, 110

    - devices, 49

    - even/odd pages, 76

    - models, 51

    - page ranges, 75

    - printers, 70-71

- `Send-Document` operation, 185

- `Send-Notifications`, 200-201

- `Send-URI` operation, 185

- sending

    - HTTP requests, 271-272

    - e-mail. 另见 e-mail

    - requests

        - IPP, 296-297

    - serial configuration, 51

    - serial devices, 42-43

    - serial ports

        - device discovery support, 366-367

        - opening, 367

- ServerRoot configuration directive

    - RunAsUser configuration directive (`cupsd.conf` 文件), 413

- ServerAdmin configuration directive (`cupsd.conf` 文件), 414

- ServerBin configuration directive (`cupsd.conf` 文件), 414

- ServerCertificate configuration directive (`cupsd.conf` 文件), 414

- ServerName configuration directive (`cupsd.conf` 文件), 415

- ServerKey configuration directive (`cupsd.conf` 文件), 415

- sections

    - PPD, 334

    - attributes, 337

    - options, 338-339

    - value, 340

- servers, 11-12

- restarting servers, 93

- security, 95

- service directives, 93

- status codes, 135–137

- value tags, 137

- Web browsers, 94

# 更新 PPD 文件

# 索引

- 打印机状态，152-155

- 安全，155

- 结构

- CUPS API, 454-455

- HTTP: 455-456

- IPP: 456-458

- 对象，285, 288-291

- PPD, 249-251, 458-461

- Subject 配置指令（多过滤器），378

- 订阅对象，142, 190

- 任务，168

- 通知属性，190-196

- 操作，197-201

- 可选属性，155-159

- 必需属性，142-144, 151

- 订阅，创建，201-202

- 支持

- 调试，27

- 设备发现，366-367

- 加密，28, 261-262

- 通知，27

- 打印，10

- SLP, 28

- 对 CUPS 的支持，577

- 同步等待器（栅化文件），450

- 安装系统要求，24-25

- SystemGroup 配置指令（`cupdsd.conf` 文件），416

# T

- 标签，137, 433-434

- 技术，10-11

- 后端，15

- 类，12

- 客户端，11-12

- 驱动程序，14

- 文件，13-14

- 任务，12

- 网络，15-16

- 服务器，11-12

- TempDir 配置指令（`cupdsd.conf` 文件），17

- 临时文件，260-261

- 过滤器架构，313

- 通知器架构，377

- 测试页，54-55, 62, 68

- 测试应用程序，30

- TeX DVI 文件，319-320

- text

- 驱动程序，341-347, 349-354

- 选项，77

- `texthof` 过滤器，309, 344-347, 349-354

- 时区 (`TZ`) 环境变量

- 过滤器，311

- 通知器，375

- 完成时间属性，171

- 创建时间属性，171

- 处理时间属性，172

- Timeout 配置指令（`cupdsd.conf` 文件），417

- 调色，修改，79-80。另见颜色（colors）

- 标题参数（过滤器），310

- `TMPDIR` 环境变量

- 过滤器，311

- 通知器，375

- 故障排除

- 应用程序，30

- 连接，94

- 类型，73

- 类型文件 (MIME)，316-317

- `TZ`（时区）环境变量

- 过滤器，311

- 通知器，375

# U

- `UIConstraint` 属性，337

- 未过滤输出，81。另见打印（printing）

- 统一资源标识符 (URL)，38

- 通用串行 (USB)，45

- UNIX 打印系统许可协议

- GNU 通用公共许可证，577-582

- 许可证摘要，576

- 无保证 (NO WARRANTY)，582

- 前言，576

- 复制、分发和修改的条款，577-579, 581-582

- GNU 库通用用公共许可证，583-588, 596

- 无保证 (NO WARRANTY)，590

- 前言，583-584

- 复制、分发和修改的条款，585-587, 590

- 未签名加密证书，96-97

- 更新 PPD 文件，361-362

# 升级

## 升级

- 应用程序，31

- CUPS，35

- HTTP 加密，279

- 可移植发行版，32

- 之前的安装，33–34

- URI (统一资源标识符)，38

- `uri-authentication` 属性，154

- `uri-security` 属性，154–155

- URL (统一资源定位符)，38

- USB (串行总)，45

- 用户配置指令（`cupsd.conf` 文件），371–418

- `+ USER` 环境变量

- 过滤器，311

- 通知器，375

- 用户名，262

- 用户，262

- 参数，310

- 身份验证，101–102

- 加密，11

- 过滤器架构，312

- MaxJobsPerUser 配置指令（配置文件），408

- 通知器架构，377

- 用户界面类型 (PPD)，448

# V

- Validate-Job 操作，184

## 值

- 数组，134

- IPP 对象，292-295

- 介质，48

- 选项，240

- 位置，182

- PPD 文件能力，249-251

- 打印质量，157

- 打印机状态，152

- 分辨率，48

- 标签，137

## 变量

- 过滤器环境变量，311-312

- 通知器环境变量，375-376

## 版本

- CUPS API 版本，337

- HTTP 版本号，442

- PPD 版本，448

## 查看

- 当前选项，82

- PPD 文件，249-256

- 状态，83–84

# W

> WARNING:信息

- 过滤器，313

- 通知器，376

## Web

- 接口，11

- 打印机

- 添加，49–51, 64

- 配置，51

- 管理，60–66

- 状态，84

## 网站，22

- `+ Adobe` 文档结构规范，306

- Adobe PDF 规范，307

- CUPS，576

- Easy Software Projects，577

- ESP Ghostscript 项目 (SourceForge)，308

- 互联网数字局 (IANA)，307

- PDFZone，307

- 打印机驱动程序，46

- SourceForge，308

- 空格配置，78

- 宽度配置，81

## Windows

- `+` 客户端，116–117

- `spadmin`，88

## 向导

- 类，64

- 打印机，50

- `wrap` 属性，183

- `WriteEpilogue()` 函数，341

- `WritePage()` 函数，344

- `WriteProlog()` 函数，341–343

## 写入

- 数据

- 写入串口端口，368

- 写入服务器，275–276

- 基于脚本的后端，368–371

- 文本驱动程序，341–349–354

# X-Z

- XINET KA/Spool，115

- XPP (X Print Panel)，19–20
