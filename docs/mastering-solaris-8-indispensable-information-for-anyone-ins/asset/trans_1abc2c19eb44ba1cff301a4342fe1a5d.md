
# 相关资源

起步的一个最佳去处是 Sun 的网站本身，具体位于 docs.sun.com 部分（网址为 http://docs.sun.com）。docs.sun.com 的首页如图 1.6 所示，列出了 Sun 发布的各种硬件和软件的多套文档。许多资料既是操作指南也是参考手册，更棒的是，它们支持跨版本搜索。涵盖的类别包括：

- Solaris 8
- 可信 Solaris 8
- 所有 Solaris 版本
- 手册页（Man pages）
- 编译器和编程工具
- 企业级服务器
- 工作站
- 存储

![](img/256e02a6afce528d264a8d911fa0ff20_34_0.png)

docs.sun.com 上的许多书籍可以下载为 Adobe 便携式文档格式（PDF），并使用 Adobe 在其网站 www.acrobat.com 提供的免费阅读软件进行阅读。你也可以从 Fatbrain.com（www.fatbrain.com）购买 Sun 文档集的打印副本。从 docs.sun.com 的首页，你还可以找到指向许多 Sun 站点的链接，这些站点提供了本书中详细描述的附加软件：

- iPlanet
- Java 平台
- Sun Microsystems 出版社
- Sun 微电子文档
- BigAdmin 主页
- SunSolve 在线
- 在线支持工具

你还可以找到指向 Java 技术站点以及产品、开发人员和研究站点的链接。如果你经常使用 Solaris，你很可能希望在浏览器中书签 docs.sun.com 的首页。

### AnswerBook2

如果你的工作环境足够大，能够支持相关工具，你可能会发现系统管理员已经在工作站或服务器上安装了 Sun Solaris AnswerBook2。如果没有，你可以使用浏览器通过网络在 AnswerBook 服务器上访问此在线帮助系统，利用公司的内部网络即可。你还会发现 AnswerBook2 也在 docs.sun.com 的 Sun 网站上。AnswerBook 是一个可选的安装包，作为每个 Solaris 发行版的一部分，它单独位于一张光盘上。它是一系列 PDF 文件，包括以下内容：

- 64 位开发人员指南
- 二进制兼容性指南
- CDE 过渡指南
- CDE 用户指南
- 设备驱动程序开发人员指南
- 国际化开发人员指南
- Jumpstart 指南
- 邮件服务器指南
- 命名服务指南
- NFS 管理指南
- NIS+ 指南
- OpenWindows 用户指南
- 电源管理用户指南
- 源兼容性开发人员指南
- SPARC 汇编语言开发人员指南
- STREAMS 开发人员指南
- SunShield 安全指南
- WebNFS 开发人员指南

要在本地系统中访问 AnswerBook2，请单击面板中的“帮助”子面板，并选择 AnswerBook2 命令，如图 1.7 所示。或者，你可以打开一个终端窗口并输入以下命令：

`/usr/dt/bin/answerbook2`

在这种情况下，AnswerBook 将在你的浏览器中打开，对于 Solaris 8，默认浏览器为 Netscape Navigator 4.7。如果你的浏览器不起作用，或者当你在 StarOffice 内工作时，请注意你也可以使用 StarOffice 的浏览功能访问 AnswerBook。

![](img/256e02a6afce528d264a8d911fa0ff20_36_0.png)

**docs.sun.com/ab2/** 上也可以在线查看 AnswerBook，并且在该位置你可以选择语言并指定所需的特定 AnswerBook 主题。你还可以查看旧版操作系统的 AnswerBook。当你点击 Solaris 8 链接时，你会被带到如图 1.8 所示的屏幕。Sun 的网站具有搜索功能，这特别有价值，而你在本地网络上访问的版本则不具备此功能。

对于有关 SPARC 或 Intel 上的 Solaris 但并非官方 Sun 文档的信息，你可能希望从这两个平台的主页开始：**www.sun.com/solaris**（用于 SPARC）和 **www.sun.com/intel**（用于 Intel）。

这些页面上的链接将带你进入概述、深入视图、资源、常见问题解答（FAQ）、解决方案以及各种旨在与这些平台配合使用的软件包的下载页面。位于 **http://solaris.java.sun.com** 的 Solaris 开发者连接是另一个资源，提供深入的专业技术资料以及对开发者计划的访问权限，程序员会对这些内容感兴趣。加入开发者计划的用户还可以获得许多软件包的特别访问权限，并根据其开发者状态获得折扣价格或免费下载。

### 图 1.8

![](img/256e02a6afce528d264a8d911fa0ff20_37_0.png)

![](img/256e02a6afce528d264a8d911fa0ff20_37_1.png)

# 第三方网站

你可以在第三方网站上找到许多针对 Solaris 用户和管理员的资源。以下列表列出了其中一些较知名的网站：

- 位于 www.sunfreeware.com 的 Sun Freeware 网站。该网站提供针对各种版本的 SPARC Solaris（包括版本 8）的免费预编译软件，你可以直接下载并安装到系统中。
- 位于 ftp://x86.cs.duke.edu/pub/solaris-x86/bins/ 的 Solaris 8 for Intel 网站。该网站包含 Intel Solaris 程序的预编译版本，你可以直接下载并安装到系统中。
- 许多版本的 Solaris 的预编译软件包可以在 www.ibiblio.org/pub/solaris/sparc 找到，通过一个易于跟随的图表即可找到。该网站由北卡罗来纳大学维护。
- 位于 www.sunhelp.org 的 SunHELP 网站。该网站包含 Solaris 8 的常见问题解答（FAQ）以及指向 Sun 网站各个主题的链接。

对于硬件，请考虑以下内容：

- 位于 www.sunsunsun.net 的 SunSunSun 硬件网站，它是一个二手和翻新 Sun 电脑的集散中心。另一个良好且可靠的二手设备来源是位于 www.mce.com 的 MinitComputer Exchange。
- 对于新的 Sun 硬件，你可以从 www.sun.com 的 Sun 网站访问 Sun 商店。
- 通常你会发现在 eBay（www.ebay.com）等拍卖网站上，Sun 正在出售其最新和新款的工作站和服务器。此外，eBay 和其他拍卖网站还出售二手的 Sun 工作站和服务器。

### 新闻组、邮件列表和常见问题解答

有许多专门针对 Solaris 操作系统的新闻组论坛和邮件列表。一个被广泛引用的 Usenet 组是 comp.unix.solaris 新闻组，它维护了关于与 Solaris 8 相关问题的深入讨论。通常，该新闻组中的讨论围绕基于 SPARC 的硬件展开。对于专注于 Intel 问题的新闻组，你应该考虑常去 alt.solaris.x86 新闻组。两个 Solaris 平台的管理问题在 comp.sys.sun.admin 论坛中讨论。

许多关于 Solaris 的具体问题在常见问题解答（FAQ，即 Frequently Asked Questions 列表）中都有涵盖，这些列表发布在互联网上。阅读 FAQ 而不是在新闻组论坛中提问的好处是，你可以匿名地自学。一个同时涵盖 SPARC 和 Intel 平台的 FAQ 可以在 www.cs.uu.nl/wais/html/na-dir/comp-sys-sun-faq.html 找到；它由 comp.sys.sun.admin 组维护。另一个专注于 Intel 平台的 FAQ 可以在 www.sun-drydog.com/faq/ 找到。一个常被引用的 Solaris 8 FAQ 是由 Casper Dik 发布在 www.wins.uva.nl/pub/solaris/solaris2/7 的。表 1.1 列出了常见的 Solaris 网站、资源和 FAQ。

| 主题 | URL |
| :--- | :--- |
| Access1 Sun 软件支持 | http://access1.sun.com/ |
| CDE FAQ | www.laxmi.net/cde.htm |
| CD-ROM FAQ | http://Saturn.tlug.org/suncd/faq/ |
| Celeste 关于 Solaris/SunOS 调制解调器和终端的教程 | www.stokely.com/unix.serial.port.resources/tutorials.html |
| CERT 协调中心 | www.cert.org |
| 颜色映射 FAQ | http://bul.eecs.umich.edu/~crowej/sunfaq/ColormapFAQ.html |
| 计算机事件预警能力（CIAC）安全 | http://ciac.llnl.gov/ciac/ |
| 帧缓冲区 FAQ | http://bul.eecs.umich.edu/~crowej/sunfaq/FrameBuffer.html |
| Solaris 内部机制 | www.zdjournals.com/sun/ |
| Intel 硬件兼容性列表 | http://soldc.sun.com/support/drivers/hcl/ |
| Intel x86 FAQ | http://sun-drydog.com/faq/ |
| IP 过滤（防火墙/NAT 软件） | http://playground.sun.com/pub/ipng/html/ipng-main.html |
| IPfilter/NAT 配置 | www.riddleware.com/solx86/nat-config.html |
| ISP 连接 | www.kempston.net/solaris/connectedanyisp.html |
| NIS+ FAQ | www.eng.auburn.edu/users/rayh/solaris/NIS+_FAQ.html |
| NVRAM/hostid FAQ | www.squirl.com/squirl/sun-nvram-hostid.faq.html |
| Open Look FAQ | www.faqx.org/faqs/open-look/03-xview/ |
| Passwd+ 安全 | ftp://ftp.Dartmouth.edu/pub/security/ |
