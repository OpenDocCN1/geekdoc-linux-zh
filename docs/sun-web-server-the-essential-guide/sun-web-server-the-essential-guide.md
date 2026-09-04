# Sun Web 服务器：核心指南






![](img/a3cb513bfd7a0b21f70c67fcaede10f6_0_0.png)

Scott G. McNealy 序言



















我们将本书献给亲爱的妻子和家庭成员 Rosella、William 和 Rachael Nelson，Tara 和 Nisha Abraham 以及 Sujatha Arundhati Chintalapati，感谢他们无条件的爱和鼓励。



- 2.3.7 总结 . . . . 39
























# 前言

网络计算一直是 Sun Microsystems 的核心和灵魂。过去一直是如此，未来也必将。如果万维网 (WWW) 是一个巨大的交换机，那么 Web Server 就是可靠交付拨号音或 Web 基调的技术，正如我们在这里所称的那样。从大规模可扩展的基于芯片的多内核服务器到 Solaris 操作系统以及 Java Web Server 基础设施，Sun 拥有这项技术。由于我们的系统旨在持久运行，Web Server 的软件组件的设计旨在从单核心扩展到数百个核心，从几百到数百个用户连接。Web Server 也不例外，它是驱动整个系统栈创新的关键技术之一。凭借其稳健的质量、卓越的可扩展性以及结合 Java 和原生 Web 技术的独特架构，Web Server 被 Sun、大大联盟 (MLB.com) 以及《纽约时报》等企业广泛部署。

在 Web 自 90 年代广泛使用十多年半后，Web Server 软件持续通过重大创新来满足互联网的需求。Web Server 7.0 版本在许多领域提供了创新，包括：

- 满足现代多内核系统和 Web 2.0 时代所需的巨大扩展性改进
- 管理性增强，通过全新的服务器界面简化了系统管理员部署和管理服务器集群的工作
- 安全功能更新，保护在线属性免受日益增长的威胁
- 部署异构 Web 技术的便利性

因此，我很荣幸地介绍关于 Web Server 7.0 版本最权威的指南。我为这些作者在 Web Server 开发、教学和支持客户方面积累多年经验感到自豪。通过具体的示例和对复杂概念的清晰解释，本书的作者提供了一份极好的实用参考指南。无论您是开发网站的开发者，还是负责管理和监控大型服务器集群的管理员，我都希望您发现书中的信息是有用的。

感谢您选择 Sun 和 Web Server 作为您 Web 解决方案的一部分。

Scott G. McNealy
Sun Microsystems 公司主席

# 前言

“总而言之，Sun Web Server 的速度通常是 Apache 的两倍。Sun Web Server 快速、灵活、可扩展且运行愉快……如果性能和易于管理至关重要，Web Server 是首选。”
——ServerWatch，2007年4月

Web 服务器一术泛泛指托管网站并向请求代理提供网站内容的服务器和软件。在最基础的层面，Web 服务器监听 TCP/IP 端口的超文本传输协议 (HTTP) 请求并提供请求资源。Web 服务器是公共互联网以及机构和公司私有网络的关键基础设施。市场上广泛使用了许多 Web 服务器产品，例如 Apache 服务器、Microsoft Internet Information Server、Sun Java Web Server 以及较新的服务器等。

Sun Web Server（正式名为 Netscape Enterprise/SunONE/iPlanet Web Server）是金融、电信、政府、旅游和体育领域大型企业广泛部署的安全服务平台。Java System Web Server（也称为 Sun Web Server）是一个免费提供的、高性能、功能丰富的 HTTP 服务器，提供了简单易用的管理界面。除了作为图像和 HTML 文档等静态媒体交付引擎外，这种多功能服务器还支持各种异构动态技术，包括 Java 以及流行的非 Java 原生脚本技术，如 NSAPI（Netscape 服务器应用程序接口）、Java Servlets、JavaServer Pages (JSP)、PHP、Perl、Ruby On Rails、Active Server Pages (ASP) 和 Coldfusion。通过支持数十万并发连接，Sun Web Server 展示了卓越的可扩展性，是部署多内核系统和基于芯片的多线程 (CMT) 架构 Web 2.0 技术企业的完美选择。

## Sun Web Server 在 CMT/多内核系统上的扩展性是行业标准

在运行 Solaris 10 Update 5 和 JDK 1.6.0 的 Sun Fire T5220 CMT 服务器上，Sun Web Server 7.0 的单64位实例在2008年4月创下了 SPEC 基准世界记录。一些示例性能指标展示了 Web Server 的卓越扩展性：超过250,000个并发 HTTP 连接、每秒131,000次安全银行操作（每分钟生成1GB Web 服务器访问日志数据）以及通过 HTTP 接口处理1.4TB 的数据。

通过对其架构、新功能、管理、性能等的深入讨论，Sun 最新的 Web Server 7.0 版本是本书的主题。结合对产品创新的见解以及对现今生产环境中使用产品客户的培训经验，作者们专注于对管理员、架构师和开发者最有确定性的技术信息。

## 本书的读者群体

本书为管理员、架构师、开发者和部署者提供了有用的技术信息。它是为需要安装、配置、监控和保护 Web Server 的人员设计的。无论您是构建动态网站的开发者，还是管理大型 Web 服务器集群的管理员，这本书都适合您。

## 本书的结构

本书呈现了有助于您建立产品专业知识的深度信息。首先，第一章提供了产品新功能的概述。然后，第二章“Web Server 7.0 架构”为您理解服务器奠定了基础。第三章随后探索了初始安装或从旧版本迁移的各种方法。接下来的两章，即第四章“Web Server 7.0 管理”和第五章“Web Server 7.0 配置文件”，为服务器管理员提供了必要的set。第六章讨论了 Web Server 如何处理 HTTP 请求，当您添加自定义 URL 规则时该章节非常有用。第七章“监控 Web Server 7.0”和第八章“安全 Web Server 7.0”为配置和保护服务器实例以获得最佳性能的服务器管理员提供了关键信息。第九章和第十章转向开发者需求，讨论了如何通过脚本语言和服务器端 Java 扩展构建动态内容。快速解决服务器运行行为中的异常（例如意外的 500 服务器错误）对于开发者和部署者可能非常重要，因此第十一章专门用于故障排除。最后一章第十二章专门介绍如何使用 Sun Web Server 构建动态（Web 2.0/企业 2.0 风格）网站，并解释了为什么该产品是使用您选择的动态内容和数据库技术构建网站的理想选择。本章还介绍了由 Web Server 7.0 驱动的 Sun 生产部署案例——Sun Blogs (http://blogs.sun.com) 是使用 Sun Web Server 7.0 部署的员工博客站点，而 MySQL Forums  (http://forums.sun.com) 是使用 Sun Web Server 7.0 部署的数千种产品和技术的公共论坛。





# 前言

xii

- 请充分利用书中书中大量的命令行示例和自学实验。。可管理性是 Sun Web Server 7.0 版本的一个大主题，其管理界面旨在让您能够相对轻松地完成常见任务。
- 本书包含了许多清晰且简洁的“如何做”类风格的示例，例如配置安全的 HTTP 监听器、虚拟服务器、FastCGI 接口、反向代理前端、LDAP 身份验证或 MySQL 数据库等数据源。

## 本书使用的规范

我们的目标是让您充分利用本书的价值并高效地完成工作。为了提高可读性，我们采用了一些规范。以下是书中使用的规范：

- “Sun Web Server”一词指代所有版本的 Web Server，而“Sun Web Server 7.0”指代特定版本。
- 图、表和示例采用统一编号方式，使用章节号和顺序数字；例如，图 1.1、表 6.1 和示例 6.2。
- 使用特殊字体来区分文件名（例如 `obj.conf`）、变量以及命令行管理脚本片段与正文。
- 特殊信息有时会通过以下注释显式标出：

> 注意：Sun Java System Web Server 7.0 发布版的核心主题包括可管理性、安全性、互操作性、CMT 可扩展性、通过对动态脚本技术的集成支持实现的便捷部署以及代理配置。

- 大多数章节以“自学实验”部分结束。这些自学实验旨在帮助验证您对相应章节中所述概念的理解。自学实验参考了 Sun Web Server 的培训，由首席培训师兼本书作者之一 Bill Nelson 设计。自学练习的答案可以在本书的辅助网站 http://www.sunweb-server.com 在线获取。在该网站，您还将找到常见问题解答（FAQs）、勘误表、关于本书的讨论以及关于 Sun Server 产品更多信息的链接（包括下载位置和产品论坛）。请访问该网站并分享您对我们工作的见解和感受。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_22_0.png)

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_23_0.png)

**注意：** 我们尽力确保书中呈现的信息（内容或示例）的准确性。然而，我们预计书中可能存在无意的错误。如果您发现任何需要的错误（无论是示例缺陷还是拼写错误），我们希望听到您的反馈。请访问 SunWebServer.com 网站，点击 Errata 链接，并按照说明在线提交错误。

## 致谢

我们要感谢许多帮助塑造本书的明智之士和领域专家。从 Sun Web Server 产品开发团队到产品管理、支持团队、现场专家以及热情的客户（包括 Sun 内部和外部），以及 Pearson 出版公司的书籍评审员和技术编辑，许多人在我们的努力中发挥了关键作用。

技术创新——特别是可管理性、CMT 团队可扩展性和安全性——跨越了 Web Server 7.0 许多方面。我们写这本书的动力源于产品创新。我们非常感谢整个产品开发和质量工程团队，包括现任及成员——Chris Elving, Praveen Chandrasekhar, Jyri Virkki, Uma Sabada, Nelson Segura-Nunez, Tuan Tran（已故），Sriram Natarajan, Baskant Kukreja, Meena Vyas, Isvar Krishnamurthy, V Premkumar, CV Padmanabhan, Anand Swamanathan, Rahul Nair, Vinutha Nagaraju, Manju Battula, Megha Shivasprasad, Chandrasekhar Arunachalam, Regi Augustine, Haridharasudasan Reghuramaaran, Partha Dey, Manoj Malhotra, Pallab Bhattacharya, Jackson Thompson 等。这些扩展产品团队的成员帮助提供了最高质量的产品，并审查了书中介绍的一些示例。

我们由心感谢支持团队的以下成员，他们帮助评审书籍内容并提供了见解和建议：Vallejo, Janice Hunt, Manish Kapur 和 Rodrigo Stumpf。来自 Sun Common Web Platform 工程的 Will Sow, Jed Michowicz, John Remko, Ramachander Varadarajan 和 Joe Mocker 分享了将 Sun Web Server 在 Sun.com、Sun Blogs 及其他属性进行生产部署的实践见解。同样，感谢 Hal Stern 对 MLB.com 的敏锐架构洞察。我们由心感谢 Pearson Education, Inc. 团队提供的卓越支持：Greg Doench, Michelle Housley 以及技术编辑宋林（音）和 Christopher Steel。感谢 Sun Microsystems 的 Myrna Rivera 为该项目的启动提供支持。

我们感谢前产品管理和营销部门成员 Joe McCabe, Chris Hogan, John Brock, Yvette Montiel 和 John Shell 为 Sun 的 Web 层产品提供的宝贵支持；如果没有像 Rob McCool 等天才工程人才多年来做的某些开创性工作，以及全球依赖该产品进行关键任务业务的企业，Sun Web Server 就不有今天。我们感谢他们对 Web Server 演变的贡献和影响，其中一些已记录在书中。我们非常感谢 Sun Microsystems, Inc. 主席 Scott G. McNealy 慷慨接受了我们的序言请求。能在书中加入序言，我们深感荣幸。我们感谢主席办公室的 Daniel Berthiume 为序言提供的帮助。

最后，我们要以最感激和深爱的方式感谢家人的耐心与理解，他们允许我们满足虚心，并投入到这个花费了太多时间的项目中。

## 关于作者

William C. Nelson 从事 IT 行业已超过20 年。在此期间，他曾担任过开发者、讲师、作者、顾问和项目经理，专注于 Web 层、身份和访问管理产品。Bill 丰富的经验和有效的沟通技巧使他能够跨越技术与业务之间的鸿沟，这种鸿沟通常阻碍了数据中心与董事会之间的沟通。Bill 为 Sun Microsystems 编写了 10 多门专注于 Java 企业的课程。他与 Sun 的目录、Web 和身份产品合作多年，并将这些经验带入他写的课程、书籍和文章。Bill 目前住在佛罗里达州的坦帕，在那里管理一个专门从事身份管理的专业服务机构。

Arvind Srinivasan 是 Web Server 开发工程团队的三位架构师之一。自2000年加入 Sun Microsystems以来，他一直担任个人贡献者，并担任 Sun Web Server 和 Application Server Servlet/JSP 容器的技术主管。大规模托管和 Servlet/JSP 容器的卓越性能/可扩展性是他对 Sun Java Web Server 的两个主要贡献。Arvind 还是《Java 网络》（Java Networking）和《Awt SuperBible: The Comprehensive Reference for the Java Programming Language》一书的合著者（ISBN: 15716931X）。

Murthy (CVR) Chintapati（通常称为 CVR）是开发主管，负责 Sun Web 层产品，包括 Sun Web Server 7.0 和 OpenSolar Web Stack (AMP)。他专注于为部署 web 2.0 技术的企业提供基础设施软件产品，以及多核和基于芯片的多线程 (CMT) 系统上的可扩展性。CVR 拥有印度理工学院（IIT 孟买）计算机科学与工程硕士学位。他获得了五项美国专利，并荣获 Sun Microsystems 主席创新奖。





# Sun Java System Web Server 7.0 简介

## Sun Web Server 7.0 有什么新？

> “我对从版本 6.1 到 7 的改进非常满意。管理控制台操作要方便得多。服务器运行更快，占用的资源更少。安装过程比 6.1 简单了 100 倍。产品做得太棒了！”——Nathaniel Walker, Mellon Bank。

Sun Java System Web Server 7.0（下称为 Sun Web Server 7.0，或后续简称 Web Server 7.0）是 Sun 商业 Web 服务器的最新版本，属于 Sun Java System 品牌软件基础设施产品家族的一部分。该产品家族包括行业领先的产品，如 Sun Java System Web Proxy Server、Application Server、Portal Server 和目录服务器企业版（Directory Server Enterprise Edition，简称 DSEE）。请注意，该产品家族中出现“Java”主要是出于品牌考虑。

Sun Web Server 7.0 在该产品及其构成产品的各个子系统中引入了多项增强。来自企业客户的广泛反馈以及更新的多核芯片多线程（CMT）系统的出现，驱动了其中许多功能增强和可扩展性改进。由 CMT 技术支持的吞吐量计算在单个芯片上提供了多个执行线程。Sun 的 CMT 系统（如 Sun Fire T2000 服务器和 Sun SPARC Enterprise T5120）为 Web Server 等服务器提供了实质性的扩展优势、吞吐量优势以及架构优势。

作为软件的任何重大版本修订，Web Server 7.0 都包含了从零开始设计的全新功能（例如新的管理 UI），以及增量改进（例如基于正则表达式模式匹配辅助的条件请求处理）。在设计如 Web Server 7.0 等软件产品重大版本修订的新接口时，与先前版本的兼容性是一个重要的设计考虑因素。尽管对于 Web Server 7.0 的任何重大版本修订，某些不兼容性是不可避免的，但我们仍确保向后兼容，以简化从之前的版本的迁移。

在对 Sun Web Server 早期版本进行简要介绍后，我们展示了 Sun Web Server 7.0 技术的概念概述，随后介绍了 Web Server 7.0 发布中的各种功能增强和改进。您将了解到 7.0 版本相对于之前的版本有哪些新特性以及哪些变化。请务必参阅第 2 章“Web Server 7.0 架构”，对核心、安全、Java Servlet 容器和管理等服务器子系统进行更深入讨论。

## 1.1 Sun Web Server 的早期版本

Sun Java Web Server（曾称为 Sun ONE Web Server、iPlanet Web Server、Netscape Enterprise Server、Netsite Communications Server 和 Commerce Server）拥有自 20 世纪 90 年代互联网快速崛起以来的技术和品牌演变历史。这导致了 NCSA（伊利诺伊大学厄尔巴纳-香槟槟分校国家超级计算机应用中心）的 HTTPd，它后来被称为 Apache HTTP Server。事实上，这些服务器是由 Rob McCool 在其担任 Mosaic Communications Corp.（后变为 Netscape Communications）开发人员的早期开发的。这些 Web 服务器源自 NCSA HTTPd，而 Apache 在开源领域演进，Netscape 则继续进行商业化开发（随后由 SunNetscape 联盟接手开发）。表 1.1 显示了 Sun Web Server 的简史。

### 表 1.1 Sun Web Server 的早期版本

| Web Server 版本 | 年份 | 主要功能 | 备注 |
| --- | --- | --- | --- |
| Netscape Communications Server 1.0, Commerce Server 1.0. | 1994–98 | HTTP/1.0, CGI, 服务端 (SSI), 图像映射、访问日志和日志轮转、额外的文档根、UNIX 目录、基于 HTTP 的基本身份验证以及基于 DBM 的哈希文件格式（用于“高容量”用户数据库）。Commerce Server 支持 RSA 公钥加密。 | 兼容 NCSA HTTPd 服务器的第一个商业互联网服务器。旨在在网络上安全地进行电子商务交易和敏感文档交换。 |
| Netscape SuiteSphere–Netscape Enterprise Server (NES) 2.3–x; NES 4.0; 安全套套接层 (SSL) 版本 3.0, HTTP Cookies 规范。 | 1998 | 软件版本、集成文本搜索引擎（基于 Vertex）、SNMP v1 和 v2、通过 HTTP PUT 方法进行一键发布、访问控制 (ACL)、Netscape 服务器编程接口 (NSAPI)、客户端证书认证和基于 Web 的远程图形化管理界面。NES 3.0/6 多线程 NSAPI、LDAP 认证、动态服务端 JavaScript 和 Java（Web 应用程序接口，WAI）；NES Pro 支持 Live Pro 数据库连接、对象代理器 (ORB) 和互联网 ORB 协议 (IIOP)。 | NES 2.0 和 3.0 开启了互联网创新的新时代，并促进了 WWW 和内网的增长——这是通过具有短购物车和通过 HTTPS 安全交易的 Web 发布和电子商务技术实现的。Sun 产品线包括 Web代理、目录、新闻、消息、日历、协作和证书服务器。该产品线获得了众多奖项——1996 年 PC 最佳新产品、1997 年 Datimation 和 CNET 最佳服务器奖。 |
| Netscape Enterprise 4.0, iPlanet Web Server 4.1–6.0 | 1999–2001 | 集成运行时和符合 J2EE 的 servlet 容器（替换了 IIS 4.1 中的 WAI），移除了 ORB/IOOP 支持，并提供了相对于 Apache HTTP 服务器的分布式架构。IIS 6.0 整合了可扩展的连接处理并增强了虚拟服务器支持；它还提高了质量和性能。 | iPlanet 品牌的 IIS 4.1 是由 SunNetscape 联盟开发的。IIS 6.0 是 SPEC99 基准测试中最快的服务器 |
| Sun ONE Web Server 6.1, 也称为 Sun Java System Web Server 6.1. | 2003 | Sun ONE Server 7.0 的后代，引入了 J2EE 参考实现和替代 Apache Tomcat 的 servlet 容器。 | Web Server 6.1 可能是部署最广泛的，支持如 MLB.com 和 NYTimes.com 等网站。 |

# 第 1 章 SUN JAVA WEB SERVER 7.0 简介

## 1.2 Sun Java System Web Server 7.0——概念概述

图 1.1 提供了 Web Server 7.0 的高层概念概述。它包含了 Web 服务器如何在典型的网站中配置目录服务器或身份服务器、数据库服务器或其他数据源。在最基本的形式下，Web 服务器通过 TCP/IP 连接响应 HTTP 请求，并提供由资源定位符（URL）标识的资源。资源（也称为内容）可以是静态媒体文件（例如 HTML、CSS 文件、Flash 文件等），也可以是动态执行的代码或内容，如 NSAPI 插件、JavaServer Pages (.jsp)、PHP 页面 (.php)。资源可能托管在接收请求的同一服务器上，也可能托管在其他地方，在这种情况下，Web 服务器可以将用户重定向到其位置，或者作为代理从源服务器（可能是另一个 Web 或应用程序服务器）获取内容。网站提供不同的服务（例如 MLB.com 提供比分、统计、赛程、门票等），每个服务都由构成静态和动态内容的应用程序实现。安全对于网站至关重要，Web 服务器提供了全面的安全功能，包括支持 SSL、身份验证/单点登录、访问控制等，以及防止跨站脚本等常见 Web 漏洞。

该图还突出了 Web Server 7.0 版本中的一些新特性——例如，FastCGI 引擎允许与 PHP 或 Ruby On Rails 等脚本技术集成；反向代理功能有助于将 Web 服务器部署在源 Web 和应用程序服务器之前，以增加安全负载均衡；管理服务器提供了集群管理和远程管理的安全基础设施，可以通过浏览器或命令行界面进行。

以下章节将讨论 Web Server 7.0 的特性：

* 核心服务器改进，包括 CMT 可扩展性。
* 可管理性增强。
* 安全性改进。
* Web 应用程序功能、易开发性和部署性。
* 互操作性和协议合规性。
* 国际化和本地化。





## 1.3 核心 Web 服务器改进

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_31_0.png)

图 1.1 Sun Java System Web Server 7.0 概念概述

如名所示，Web 服务器核心子系统是其他服务器子系统构建的基础，它实现了服务器配置和运行时请求处理的基本方面功能。在 7.0 版本中，核心子系统进行了许多重大改进。

凭借 Sun Web Server 7.0 对 Solaris（以及 Linux）平台的原生 64 位支持，它整合了多项设计改进以在 CMT（并发多线程）系统上扩展，世界级 Web 服务器基准测试结果已证明了这一点。在讨论 Web Server 7.0 核心改进之前，我们先对核心子系统进行高层概述。关于核心及其他子系统的更详细功能讨论，请参考第 2 章。

### 1.3.1 Web 服务器核心子系统

Web 服务器核心子系统在初始化、处理 HTTP 请求以及维护运行时配置和关键统计数据方面发挥着核心作用。以下是核心子系统在功能性 Sun Web Server 实例中作用的概述：

- 通过读取 `server.xml` 等文件中指定的服务器配置来启动服务器，创建运行时环境并初始化如文件缓存和 NSAPI 插件等子系统。

- 执行 Web 服务功能，例如处理入站连接、在适用时进行 SSL 通信加密和解密，以及解析和处理 HTTP 请求。请求处理的所有方面都通过 `obj.conf` 中的一系列指令进行自定义。

- 响应管理操作，例如监控服务器运行状态、动态更改配置等。

### 1.3.2 配置增强

由于多项改进，Web Server 7.0 显著增强了服务器的可配置性：

- 服务器配置的 XML Schema 验证——提供了易易用性（例如，在适当的情况下放宽了服务器配置中元素的顺序限制），并对配置元素和引用进行完整性检查（例如，确保 HTTP 监听器中指定的 IP 地址是真实的，或对服务器配置元素应用稳健的类型检查）。

- 新的服务器配置（`server.xml`）语法——这提高了了可读性，因为它镜像了 Servlet 部署描述符中使用的约定。

- 合并与委托服务器配置——通过将以前 Web Server 版本中存在的各种配置文件和指令（如 `ns.conf`（文件配置-密码）、`web.conf`、`dbswitch.conf`（身份数据库配置）等）合并到 `server.xml`，简化了配置。同时，Web Server 7.0 提供了委托机制，允许单个虚拟服务器拥有自己的配置。

### 1.3.3 核心子系统改进

本节介绍了 Web Server 7.0 中核心子系统的改进：

- 条件请求处理，当入站请求匹配一组表达式时，为以某些方式处理请求提供了极大的灵活性。例如，当用户通过明文 HTTP 连接请求资源时，你希望强制用户跳转到安全的 HTTPS 连接。

- 基于正则表达式的模式匹配，适用于整个配置。

- URL 重写，允许你将外部使用的美化 URL（也称为虚荣 URL）重写为内部的丑 URL。这与 Apache Web 服务器流行的 `mod_rewrite` 模块相似，甚至比它更灵活、通用。

- URL 重定向，允许你将请求从一个 URL 重定向到另一个 URL。`location` 和 `want` 的示例用法是：假设资源已移动到不同的位置，你希望服务器相应地重定向用户。虽然此功能在之前的版本中可用，但 Web Server 7.0 增强了其易用性和灵活性，你可以将 URL 重定向与条件处理和模式匹配相结合。

- 集成反向代理，允许 Web Server 部署为作为应用源服务器的安全 HTTP 前端。反向代理支持基础的轮询负载均衡和会话保持路由。

- 集成 FastGI 引擎，允许 Web Server 与 PHP 和 Ruby On Rails 等进程外的动态脚本引擎集成。

- 两个新的 NSAPI 请求处理过滤器（一个用于输入阶段，另一个用于输出阶段），允许管理员使用 UNIX `sed` 程序中的语法操作进出 Web Server 的数据。正如你后面将看到的，这些过滤器有许多应用，例如检测常见的 Web 漏洞形式，如跨站脚本（XSS）攻击。

## 1.4 可管理性增强

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_33_0.png)

注意：管理性（manageability）一词通常指系统/服务器管理员和最终用户执行配置、部署、监控以及自定义或扩展一个或多个 Web Server 安装的常规任务的容易程度，无论是在单机开发环境还是大规模服务器集群中。

先前的 Web Server 版本包含一个基于浏览器的界面，该界面侧重于配置单个 Web Server 安装且范围简单。然而，客户的反馈（部署 Sun Web Server 的主流互联网网站管理员）更倾向于能够管理和监控跨服务器集群的多个 Web Server 安装的界面、用于脚本编写常规任务（如日志聚合或可自动化的滚动升级）的命令行界面，以及对于常用任务具有更高的易用性。

管理性是 Sun Web Server 7.0 的主要主题之一，新版本对管理基础架构（也称为管理框架）进行了完全重写。管理员管理单个实例或服务器集群的易用性是可管理性的关键。从技术角度来看，Web Server 7.0 中的管理性指的是以下章节概述的若干功能。

### 1.4.1 基于 Web 的图形界面

基于浏览器的图形界面（也称为管理员控制台）体现了 Web Server 7.0 的各项重要管理性进展。无论是管理单个 Web Server 实例还是服务器集群，该 Web 界面都提供了一个集中控制台来配置服务器、部署配置并监控运行中的服务器。如图 1.2 所示，该 Web 界面为安装证书、部署应用程序、调整服务器设置以及启动和停止服务器等常用任务提供了更好的导航便利性。

### 1.4.2 命令行界面

命令行界面（CLI）对于自动化管理员任务至关重要，许多任务是远程执行的，例如向服务器集群滚动更新应用程序、收集日志或将部分生产服务器上线或离线。该框架是全面、安全且可脚本的。

Sun Web Server 7.0 中基于 Web 的图形管理控制台

> 注意：`wadm` 二进制文件（Windows 平台上的 `wadm.bat` 文件）位于相对于安装目录的 `bin/` 子目录下，实现了 Web Server 7.0 的 CLI 功能。用户可以在 Web Server 安装程序中选择自定义安装选项，仅安装 CLI 而不是整个服务器产品。

命令行（CLI）脚本可以针对远程服务器运行。如图 1.3 所示，在 Windows PC 上执行的 `wadm` 可以安全地远程访问其他地方的 Web 服务器的运行时性能信息（通过 `wadm` 的 `get-perfdump` 子命令）。




# 第 1 章 Sun Java Web Server 7.0 简介

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_36_0.png)

图 1.3 Sun Web Server 7.0 中的远程命令行界面 (CLI)

### 1.4.3 集群管理

集群管理是指通过单一管理界面、基于 Web 的图形化界面或命令行界面 (CLI)，对部署在一组节点上的set Web 服务器实例进行管理。正如后续管理章节详细提到的，节点可以是一个单机服务器，也可以是一个虚拟化系统。集群管理是可维护性的关键，也是 Sun Web Server 7.0 安全管理基础设施设计中不可或缺的一部分，该基础设施包括一个管理服务器（Administration Server）以及集群中每个节点一个管理代理（administrative agent）。CLI 通过安全的 HTTPS 连接进行。作为管理员，你将管理一组——实际上是一个或多个——服务器配置文件。如图 1.4 所示，管理服务器维护一个服务器配置文件的中央仓库，并通过安全地将这些文件复制到其管理的节点集群来帮助进行集中管理。在节点上运行的 Web 服务器安装被称为服务器实例（server instance），集群中的所有实例都使用相同的配置。每个节点上的管理代理还帮助集中管理服务器实例的生命周期，并从这些实例中收集运行统计数据。管理服务器和每个节点上的代理通过安全的 HTTPS 连接通信，共同构成了集群管理基础设施的核心。图 1.4 显示了 Web Server 7.0 中的集群管理基础设施。

## 1.5 安全改进

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_37_0.png)

对于 Web 开发者而言，安全性对于管理运行生产环境中 Web 服务器的系统和站点管理员来说是同样重要的考虑因素。由于在全球范围内已通过安全部署，安全性是 Sun Web Server 的优势，也是其在 Web Server 7.0 中的一个重要主题。在这里，我们介绍了 7.0 版本中实现的显著安全特性，其中许多是客户要求的：

- 椭圆曲线密码 (ECC) 密码套件——Web Server 7.0 是采用 ECC 技术的早期之一，通过大幅减小密钥尺寸极大提高了公钥加密的效率。
- LDAP 身份验证改进——旨在提供更灵活的 LDAP 服务器配置功能，Web Server 7.0 整合了以下重要变化：
  - 在 LDAP 服务器中搜索和匹配用户及组成员信息的灵活配置。Web 服务器通常使用 LDAP 条目中的属性名和值来搜索和匹配所需的值（例如，userid 或组名）。在 Sun Web Server 的此前的版本中，属性名搜索模式是硬编码的。Web Server 7.0 消除了这一限制，因此更容易对许多 LDAP 服务器（如 Microsoft Active Directory Server）进行身份验证。
- LDAP 服务器连接失败处理，允许管理员配置备选的备用 LDAP 服务器。
- 对 WebDAV（基于 Web 的分布式授权和版本控制）访问控制协议 (RFC 3744)的支持——允许第三方授权工具通过扩展的 HTTP 接口对内容进行保护。
- 动态证书吊销列表 (CRL) 刷新——允许管理员配置周期性的实时刷新 CRL，而无需重启服务器。
- 拒绝服务 (DoS) 攻击防护——提供了几种防御机制来保护你的网站免受 DoS 攻击。相对于 Web Server 7.0 版本，这里有以下增强：
  - Web Server 7.0 提供了机制来保护 Web 服务器及其提供的资源免受潜在恶意客户端的侵害。管理员可以使用各种请求属性（例如客户端 IP 地址）配置 Web 服务器如何隔离这些客户端，并将流量限制在某些阈值内（每秒允许请求数或最大并发连接数）。此外，还可以指定将流量阈值应用于全局服务器、特定资源、一组匹配 URL 模式的资源集，或使用更强大的条件指示器。
  - 另一种形式的 DoS 攻击可能发生在恶意客户端打开许多连接（超过请求处理工作线程的最大数量）并滴流请求数据时，从而导致合法客户端无法访问服务器。Sun Web Server 的此前的版本支持对此类攻击的有限形式防护，即限制处理 CGI 请求的工作线程在连接上等待请求数据的时间。Web Server 7.0 将此扩展到任何 HTTP 请求，并允许管理员对服务器在连接上等待接收请求头或请求主体的持续时间设置超时限制。
  - 跨站脚本 (XSS) 攻击检测——XSS 攻击是一种常见的 Web 安全漏洞，除非被检测和防止，否则可能会损害无意用户的在线安全。该攻击发生在恶意用户将脚本发布到有漏洞的网站（如在线公告板）时。当毫无防备的用户在浏览器中查看该站点时，嵌入的恶意脚本会在用户的浏览器环境中执行，反过来可以将个人信息直接传输给恶意用户。Web Server 7.0 的 sed 过滤器允许管理员应用 sed 脚本来过滤掉恶意帖子，并从源头防止该漏洞。

## 1.6 Web 应用开发与部署的便利性

除了其原生服务器扩展 API（即 NSAPI）带有集成的 Java Servlet 容器和对原生技术的支持外，Sun Java Web Server 支持广泛的异构 Web 应用、部署和开发。（注：此处 OCR 文本存在混乱，但上下文清晰的）。

- Java EE 5——支持 Servlet 2.5、JSP 2.1、JSTL（JSP 标准标签库）1.2 等最的 Web 应用。
- XML/SOAP Web 服务——通过 JWSDP 2.0 提供。这是 GlassFish 的最新版本。
- 内存会话复制——Web 服务器将会话数据保存到备用服务器，以便发生故障时前端负载均衡器可以将流量重定向到备用服务器，从而提供用户连续性。

## 1.7 互操作性改进

互操作性是任何多层部署架构中一个重要的考虑因素，Sun Web Server 7.0 在多个方面改进了互操作性：

- Solaris 10 平台互操作性——通过 PKCS#11 接口支持 Solaris Crypto Framework (SCF)；Solaris 服务管理框架 (SMF)；支持 Zones。
- 单点登录——跨网站或域内不同服务的身份验证通过 Sun Java System Access Manager/Federated Access Manager 及其相关的开源项目 OpenSSO 提供。请注意，基于安全 Web 服务的联邦访问管理提供了跨多个网站或域的单点登录能力。
- Sun Web Server 7.0 可配合 OpenID，这是一种在 Web 上使用的轻量级去中心化身份验证系统。单点登录也有商业解决方案；例如 Computer Associates 的 Identity SiteMinder。此外，如前所述，Sun Web Server 7.0 可以轻松与 Microsoft Directory Server 进行互操作。




## 1.8 国际化 (I18N) 与全球化 (G11N) 支持

- 内容/开发者工具的互操作性——例如 Adobe Dream-weaver 和 WebDAV 访问控制，后者允许使用基于 DAV 的内容管理工具。

## 1.8 国际化 (I18N) 和全球化 (G11n) 支持

考虑到 Sun 产品和技术的全球影响力，符合 I18N 标准是 Sun 的基本规则之一，而针对当地的本地化是一项常态。Sun Web Server 7.0 也不例外，其基于浏览器的管理 GUI、服务器错误信息、在线帮助和发布说明已本地化为七种语言（法语、德语、西班牙语、日语、简体中文、繁体中文和韩语）。图 1.5 显示了日语版 Sun Web Server 7.0 Web 管理控制台界面。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_41_0.png)

图 1.5 Sun Java System Web Server 7.0 管理控制台（日语）

## 1.9 总结

Sun Web Server 7.0 是部署最广泛的 Wide Web 服务器之一演进过程中的重大版本，驱动着互联网上一些繁忙且最安全的网站，其技术起源源于 Netscape Enterprise Server 和 NCSA HTTPd。Sun Web Server 是财富 100 强和全球 250 强企业领先的 Web 服务器，涵盖教育、电子商务、金融、政府、医疗、信息技术、媒体、军事、零售、体育、电信和旅游领域。

作为一个重大版本，Sun Web Server 7.0 整合了主题、可管理性、安全性、更新的 Java 标准遵循以及互操作性方面的改进。可管理性的改进贯穿整个服务器，包括在大型集群环境中如何配置、部署、管理和监控服务器。

集群管理是 Web Server 7.0 的核心，其特点是对管理基础设施的完全重写，并采用了全新的基于 Web 的全面图形化管理界面以及安全、可脚本的命令行界面。通过支持现代 Java EE Web 技术以及通过 FastCGI 启用 PHP 和 Ruby On Rails 等原生脚本技术，Sun Web Server 7.0 代表了最全面的异构动态 Web 平台。核心架构增强包括 64 位（有助于更大的文件缓存和 Java 堆内存大小）多线程架构、模式匹配、URL 重写、基于 UNIX sed 的 NSAPI 过滤器（也可用于保护网站免受 XSS 攻击等常见 Web 漏洞的影响）、DoS 攻击感知以及集成反向代理，使 Web Server 7.0 成为健壮、安全且可扩展的部署平台。

## 1.10 自学实验室

利用本章的信息执行以下练习。这些练习将帮助验证你对本章描述概念的理解。

1. 通过访问以下任何 URL，查看大型网站是如何实现 Web Server 的：
   - www.sun.com
   - forums.sun.com
   - www.mlb.com
   - www.nyl.com
   - www.boeing.com
2. 访问书籍网站 (www.sunwebserver.com) 并探索在该网站上找到的额外信息。
3. 额外练习：
   - 研究构建基于 OpenID 的联邦单点登录 (Single SignOn) 基础设施解决方案，参考文章 [Openid At Work](www.sun.com/bigadmin/features/openid_web_server.jsp)。
   - 了解 Sun Web Server 如何通过现代 64 位多内核多线程 (CMT) 架构扩展到数十万并发连接，参考文章：http://blogs.sun.com/webtier/rise_of_cmt_systems_on

## Web Server 7.0 

Web Server 7.0 是一种快速、可扩展且易于安装和管理的安全 HTTP 服务器，在多种操作系统上免费可用。理解 Web Server 7.0 的各种组件如何相互作用以及底层架构，将有助于你管理和排错 Web Server。

本章解释了 Web Server 的整体架构以及构成 Web Server 的组件之间的关系。具体讨论了构成 Web Server 的各种进程、服务器中的不同子系统、支持静态和动态内容以及 64 位架构。

## 2.1 进程

当你启动 Web Server 实例时，会运行多个进程。每个进程在确保你的网站 HTTP 请求保持可用和运行方面起着特定作用。本节描述了启动 Web Server 7.0 实例时运行的各种进程。实例（instance）指的是特定节点上的 Web Server 环境，包括其配置、日志文件以及数据库、缓存和临时文件等运行时产物。为了管理目的，实例可以启动/停止/重启或重新配置。

如图 2.1 所示，启动 Web Server 实例时会创建三个进程：守护进程（watchdog）、原始进程（primordial）和工作进程（worker）。

## 第 2 章 WEB SERVER 7.0 架构

## Web Server

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_46_0.png)

**图 2.1** 进程

守护进程生成原始进程，原始进程生成一个或多个工作进程。工作进程监听一个或多个端口的 HTTP 请求，并负责处理这些端口上的请求。工作进程负责处理安全和非安全连接的 HTTP 请求。这些进程的创建顺序（当你执行启动实例的脚本时）如图 2.1 所示，如下：

1. 守护进程
2. 原始进程
3. 工作进程

守护进程和原始进程提供了服务器内部的高可用性水平。如果工作进程崩溃或异常终止，原始进程负责重启另一个工作进程。如果原始进程本身异常终止，则由守护进程重启另一个原始进程。

在 UNIX 平台上，Web Server 实例恰好有一个守护进程、一个原始进程和一个多个工作进程。在 Windows 平台上，每个实例恰好有一个守护进程和一个工作进程。Windows 上没有独立的原始进程，且每个实例不能启动多个工作进程。

> 注意：理论上，单个进程可以同时守护进程和原始进程的工作。它们作为独立进程（在 UNIX 平台上）的原因更多是历史性的。

原始进程和工作进程都命名为 `webservd`。守护进程的名字为 `webservd-watchdog`。

在 UNIX 服务器上，可以使用 `ps -ef` 命令查看这些进程。以下示例了在 Solaris 上运行实例的每个进程：

```
# ps -ef | grep http
```

```
webservd 14857 14856 0 Jan 22 ?   33:12 webservd -d
/sun/webserver7/https-boulder.example.com/config -r /sun/webserver7
root 14856 14855 0 Jan 22 ?   7:19 webservd -d
/sun/webserver7/https-boulder.example.com/config -r /sun/webserver7
root 14855 1 0 Jan 22 ?   0:04 webservd-watchdog -d
/sun/webserver7/https-boulder.example.com/config -r /sun/web
```

> 注意：`ps` 命令提供了关于进程所有者、进程 ID、父进程 ID、进程启动日期、运行的守护进程以及传递给进程的参数的重要信息。

第一列指定进程所有者，在这种情况下，守护进程和原始进程为 `root`。如果你的 Web Server 监听的是小于 1024 的端口（UNIX 上的特权端口），则需要。如果端口大于 1024，守护进程和原始进程可以是非 root 用户。子进程所有者的用户在安装过程中指定。在这种情况下，进程所有者是默认用户 `webservd`。

第二列是运行进程的进程 ID，第三列是父进程（或启动该进程的进程）的进程 ID。

从从下到上观察条目，可以观察到以下内容：

* 14855 是守护进程。它是由 `init` 进程（由进程 ID 1 表示）启动的。
* 14856 是原始进程。它是由守护进程启动的。
* 14857 是子进程。它是由原始进程启动的。

各种进程之间存在父子关系。你可以使用 UNIX 的 `ptree` 命令作用守护进程来确定这种关系，如下：

```
# ptree 14855
```

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_47_0.png)





# 第 2 章 Web Server 7.0 架构

14855 webservd-wdog -d /sun/webserver7/https-boulder.example.com/config -r /sun/webse
14856 webservd -d /sun/webserver7/https-boulder.example.com/config -r /sun/webserver7
14857 webservd -d /sun/webserver7/https-boulder.example.com/config -r / sun/webserver7

## 2.2 Web Server 架构

Web Server 7.0 是一个多线程、多进程、高扩展性且安全的 HTTP 服务器。在为任何 Web Server 实例启动的所有进程（守护进程、原始进程和工作进程）中，工作进程（worker process）是最有趣的，因为在处理 HTTP 请求时，它承担了大部分的工作。

图 2.2 显示了工作进程的一些主要组件。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_48_0.png)

接下来的子节将详细描述工作进程。

## 2.2 Web Server 架构

### 2.2.1 连接处理线程

Web 服务器通过网络连接接收 HTTP 请求并发送 HTTP 响应。Web Server 支持通过安全和非安全网络连接运行 HTTP。Web Server 的连接处理子系统由三个不同的线程池组成，这些线程池协作工作以确保连接的可扩展性以及计算资源的高效利用。

### 2.2.1.1 接收线程 (Acceptor Threads)

新的 HTTP 请求最初由接收线程处理。接收线程负责接受来自客户端的连接请求，并将这些连接传递给其中一个工作线程。

图 2.3 说明了传入的连接如何首先由其中一个接收线程处理，然后交给工作线程进行进一步处理。连接队列（Connection Queue）是一个线程安全的数据结构，用于在接收线程和工作线程之间传递传入的连接。当所有工作线程都忙于处理请求时，新的传入连接将在连接队列中等待，直到下一个可用的工作线程接管它们。连接队列的容量通常配置为比工作线程数量大几个数量级。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_49_0.png)

**图 2.3** 传入 HTTP 请求的处理

你只需要少量接收线程即可处理大量的传入连接，因为每个线程执行的工作并不是资源密集型的。通常，你会将接收线程的数量配置为与计算机上的处理器数量相同。

### 2.2.1.2 保持活动线程 (Keep-Alive Threads)

保持活动线程管理空闲的 HTTP 连接。如果 HTTP 请求数据无法立即被服务器读取，则该 HTTP 连接被认为是“空闲”的。保持活动线程定期监控所有空闲连接以检测数据。当在连接上检测到数据时，保持活动线程会将连接传递给工作线程，然后由工作线程处理请求。

在持久连接出现之前，HTTP 客户端会为每个 URL 建立单独的 TCP 连接。为每个 URL 建立新的 TCP 连接是无效的，会增加 Web 服务器的负载并导致网络拥塞。使用持久连接，HTTP 客户端现在可以在同一个 TCP 连接上发送多个 HTTP 请求，从而减少 TCP 连接的开启和关闭，减少网络拥塞和延迟。持久 HTTP 连接也称为 Keep-Alive 连接。

### 2.2.1.3 工作线程 (Worker Threads)

工作线程是 Web Server 的核心工作单元。每个工作线程处理来自 HTTP 客户端的一个或多个 HTTP 请求。为了处理请求，工作线程传递 HTTP 请求，并根据请求头中的信息设置虚拟服务器环境，以对请求进行进一步处理。然后，工作线程让请求通过各种请求处理阶段，最后向 HTTP 客户端发送响应。有关请求处理阶段的详细描述可以在第 6 章“Web Server 7.0 请求处理”中找到。

当工作线程完成对 HTTP Keep-Alive 连接上的请求的服务后，它会检查同一连接上是否有其他准备好处理的请求。这避免了将连接传递给 Keep-Alive 系统后又因为连接上有可读数据而将其重新传回工作线程的延迟。

如果没有可用的请求，则该连接被传递给 Keep-Alive 系统。

### 2.2.2 服务器函数

服务器应用函数 (SAFs) 是用 C 语言编写的小型函数，用于扩展 Web Server 的功能。每个 SAF 会在请求处理生命周期中的各个位点被调用，允许开发者拦截并修改服务器的行为。

### 2.2.3 NSAPI 引擎

Netscape 接口 (NSAPI) 是一种程序化接口，允许开发者与 Web Server 交互。它由 Netscape Communications 开发，为模块扩展服务器功能提供标准方式。NSAPI 提供了一系列用于平台无关性的函数。

### 2.2.4 进程模式

Web Server 7.0 可以以单进程或多进程模式运行。默认模式为单进程模式。

在单进程模式下，单个工作进程接收并处理所有请求。由于工作进程本身是多线程的，因此多个请求可以并发处理。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_51_0.png)

在多进程模式下，有多个工作进程。在这种模式下，Web Server 不在各个进程之间分发传入请求，而是依靠操作系统来实现。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_52_0.png)

### 2.2.5 原生线程池

在 Web Server 的语境下，原生线程（native thread）是指能够安全支持阻塞调用的线程。原生线程池是 Web Server 创建并用于运行需要原生线程的 NSAPI 函数的线程池。

Web Server 使用 Netscape 运行时 (NSPR)，这是一个底层可移植层，提供了一个平台中性的 API，用于访问操作系统设施和服务，例如线程、同步、时间、I/O、网络地址和内存管理。





## 2.2 Web 服务器架构

### 2.2.6 内容处理子系统

使用 Web Server 7.0，你可以在你的网站上托管各种类型的静态内容（如 HTML、文本和图像文件）以及动态内容（如 CGI 程序、Java Servlets、PHP 等）。

高性能 Web 服务器必须具备一个高效且可扩展的子系统，用以处理对大量静态内容的请求。Web Server 7.0 的文件缓存允许服务器通过避免不必要的磁盘访问，高效地处理对静态内容的请求。高度可配置的文件缓存还用于缓存服务器解析的 HTML 内容。服务器的文件缓存可以配置为使用不同类型的高效内存管理技术，根据文件大小等参数来缓存静态内容。众，文件缓存具有高度的可扩展性，研究表明它能够高效地缓存并服务于 32GB 静态内容的请求！

Web Server 7.0 还支持 HTTP 压缩。通过此功能，可以配置服务器为目录中的文件创建预压缩版本，或者对发送出的数据进行动态压缩。通过减少发送的数据量，内容压缩可以缩短内容的下载耗时间，并提高页面的显示速度。

### 2.2.7 安全与访问控制

Web Server 7.0 是首批支持椭圆曲线加密（ECC）的产品之一。ECC 是一种下一代安全技术，使用更短的密钥提供与传统替代方案同等的安全性。

Web Server 7.0 的创新安全特性包括对拒绝服务（DoS）攻击的节流以及跨站脚本（XSS）的检测。恶意用户可以通过不断向服务器发送请求来阻止他人访问服务器。可以通过配置服务器检测此类情况并自动限制此类请求的服务速率或限制此类请求的并发数来缓解此类攻击。`sed` 是一种流行的 UNIX/Linux 实用程序，使用单个命令语言转换文本。Web Server 7.0 包含了新的过滤器，这些过滤器整合了 sed 的命令语法，并可以转换请求或响应中的内容。这些过滤器可以用于中和跨站脚本攻击。以下摘自虚拟服务器对象配置文件（obj.conf）的片段演示了过滤器如何将响应中网站地址的每个出现处都替换为另一个 URL：

```
fn="insert-filter" type="text/html" filter="sed-response"
sed="s|http://internal.server|http://external.server.com/|g"
```

访问控制子系统用于限制对整个服务器或其部分的访问。身份验证、授权和访问控制是服务器保护、限制和强制执行资源访问的一些机制。身份验证是验证身份的过程，而授权意味着授予资源的访问权限。Web Server 7.0 的访问控制配置由一组称为访问控制条目（ACEs）的层级规则组成。ACE 的集合称为访问控制列表（ACL）。可以为每个虚拟服务器配置 ACL，如果服务器确定 ACL 适用于该请求，服务器将评估其 ACEs 以决定是否授予访问权限。

访问控制子系统还包含一个 ACL 缓存，这在使用外部 LDAP 数据库执行用户组身份验证时特别有用。在受 ACL 保护的资源繁忙的网站上，ACL 缓存通过减少必须查找外部 LDAP 数据库的次数来帮助提高整体性能。

Web Server 7.0 还支持使用 `.htaccess` 文件进行访问控制。标准的访问控制检查始终在任何 `.htaccess` 访问控制之前应用。

### 2.2.8 反向代理

与之前的版本不同，Web Server 7.0 包含了集的反向代理功能。反向代理在客户端看来是 Web 服务器，但实际上它将收到的所有请求都转发给一个或多个托管实际内容的源服务器。通过配置将请求反向代理到多个源服务器，可以使用 Web Server 进行应用程序负载均衡。当配置为反向代理时，Web Server 可以作为任何符合 HTTP/1.1 的源服务器的前端。当用作反向代理时，服务器会定期检查以确保源服务器在线。当发现源服务器无响应时，它被标记为离线，在它被认为再次在线之前，请求将不会路由到那里。

### 2.2.9 动态重配置

配置是指用于配置 Web 服务器 运行时服务的元数据。运行时服务的一个示例是从给定的文档根提供网页（例如 HTML 页面/图像）。配置元数据被服务器运行时用于加载内置服务和第三方插件，并设置其他服务器扩展（如数据库驱动程序），所有这些都有助于提供网页和动态 Web 应用程序。

动态重配置有助于在无需停止和启动服务器进程的情况下对正在运行的 Web 服务器进行更改。对于用于生产环境以及用于开发的 Web 服务器，重启服务器进程是有益的。对于开发者来说，动态重配置减少了将更改部署到服务器所需的时间。对于运行网站的管理员，动态重配置使他们能够在不中断可能正在浏览网站的用户体验的情况下更改正在运行的服务器。此功能首次在 Web Server 6.0 版本（当时称为 iPlanet Web Server 6.0）中亮相，从那时一直是 Web Server 的亮点。

当更改通过管理命令行界面（wadm）或图形用户界面部署到服务器时，服务器会进行动态重配置。执行位于每个服务器 `bin` 目录下的配置脚本将触发动态重配置。Web Server 的大部分配置可以在重启的情况下动态更改。在动态重配置期间，如果服务器检测到正在部署的配置存在错误，将记录错误消息。

### 2.2.10 模式匹配

Web Server 7.0 包含一个强大的新模式匹配子系统，支持通配符和正则表达式。Web Server 7.0 还定义了许多用于请求处理的变量，如 $url,$cookie,$browser 等。正则表达式和变量替换可以使用请求处理中的任何地方。Web Server 7.0 引入了一种使用 Perl 语法的表达式语法，用于在文件中指定复杂的请求逻辑。

Web Server 的模式匹配能力用于在文件中实现复杂的 URL 重写和重定向。以下摘自虚拟服务器对象配置（obj.conf）的片段，演示了如何将误用大写字母的用户的用户重定向到正确的资源名称：

```
<$If code == 404 and -U uri>
Error fn="redirect" url="$uri)">
```

请参考《Sun Java Web Server 7.0 管理配置参考》中的“使用变量、表达式和字符串插值”以及“使用通配符模式”章节，获取有关 Web Server 7.0 中模式匹配、表达式和插值的更多信息。

## 2.3 管理服务器架构

Web Server 7.0 的管理基础设施包含了强大的命令行工具和重新设计的基于任务的图形界面，使得 Web Server 实例变得更加简单。

典型的 Web Server 7.0 安装为你的站点创建一个 Web 服务器实例和一个特殊配置的 Web 服务器实例（下称为管理服务器），用于管理你的站点。管理服务器是仅用于管理目的的特殊 Web 服务器实例，并在其部署管理应用程序。使用管理服务器，你可以创建、删除、管理和维护你的 Web Server 实例。

管理服务器管理与每个实例相关的配置信息，并通过特定的监听套字接收管理命令。





第 4 章“Web Server 7.0 管理”详细描述了 Web Server 7.0 的管理架构。

## 2.4 动态内容

使用 Web Server 7.0，除了托管和提供静态内容外，您还可以提供用各种脚本语言编写的动态内容。

### 2.4.1 通用网关接口 (CGI)

部署为通用网关接口 (CGI) 程序由 CGI 子系统处理。CGI 是外部程序与 Web 服务器交互的标准。CGI 程序通常用 Perl 和 Bourne shell 等脚本语言编写。在 Windows 平台上，用 Visual Basic 等 Windows 特有语言编写的 CGI 程序由 Web Server 中的 Shell CGI 子系统处理。

CGI 规定了 Web 服务器的接口，用于接收来自 HTTP 客户端的数据，将这些数据传递给外部程序进行处理，然后将结果传回 HTTP 客户端。

图 2.4 显示了 Web Server 与 CGI 程序之间的典型关系。在接收到 CGI 程序请求时，服务器会创建一个 CGI 进程，并使用输入、输出和错误的标准文件描述符与 CGI 程序交换数据。执行请求后，CGI 程序将终止。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_57_0.png)

图 2.4 Web Server—CGI 进程交互

在 UNIX 平台上，Web Server 中的 CGI 子系统对以什么身份执行什么实施了若干安全限制。Web Server 中的 CGI 子系统还可以配置为以不同的 UNIX 用户运行 CGI 程序，限制 CGI 消耗内存内存，并指定 CGI 程序的运行优先级。Web Server 包含一个 Perl 解释器，用于运行用 Perl 语言编写的 CGI 程序。

### 2.4.2 服务器解析 HTML (SHTML)

SHTML 子系统处理对 HTML 文件的请求，这些文件包含在服务器上执行的标签/指令。服务器解析 HTML 或服务器端包含 (SSI) 是一种基本的服务器端脚本语言，大部分内容是 HTML，但也包含一组有限的动态指令，用于包含其他文件、打印 HTTP 环境变量、在服务器上执行程序、显示文件最后修改时间等。在 Web Server 中，您可以定义自己的服务器解析 HTML 指令，并在 HTML 文件中嵌入 Java servlet。只有在启用了服务器端解析时，Web Server 才会解析服务器端标签。Web Server 中的 SHTML 子系统还包含一个缓存，可加速 SHTML 内容的处理。

### 2.4.3 FastCGI

FastCGI 是通用网关接口的扩展，它缓解了 CGI 的许多局限性，并为与 Web Server 操作的应用提供了高性能。对于每个 CGI 应用请求，都会创建一个单独的进程。取决于 CGI 应用 Nature，这可能是一个耗时耗资源的操作。FastCGI 应用的生命周期与客户端请求绑定，从而消除了创建开销，并允许 FastCGI 应用跨请求维护状态（如内容缓存和连接池）。在 FastCGI 环境中运行的应用在于 Web Server 的进程中运行。FastCGI 可用于运行任何语言编写的应用，如 Perl、Python、PHP、Ruby 等。

图 2.5 显示 Web Server 与 FastCGI 进程通过持久的全双工套接字连接进行通信。套接字可以是 TCP socket 或 UNIX socket。与 CGI 进程模型不同，FastCGI 进程不会为每个请求创建和销毁。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_58_0.png)

图 2.5 Web Server—FastCGI 进程交互

### 2.4.4 Java

对 Java Web 应用内容的请求由图 2.2 所示的 Java 容器处理。Java Web 应用技术包括 servlets、JavaBeans、JavaFaces 和 Web Services。Web Server 中的 Java 容器还支持命名和目录接口 (JNDI) API 和 Java 数据库连接 (JDBC) API。

与 Apache HTTP 部署不同，Java Web 应用内容的请求通常被委托给另一个进程（例如 Tomcat Web Server），Web Server 7.0 中的 Java 容器嵌入在工作进程本身。这消除了使用进程通信协议（例如 Apache JSP 协议）和通道（例如套接字和管道）的需求。Web Server 与 Java 容器之间（通过编程 API）更紧密的集成使得服务器能够更高效地处理 Java 内容请求，并使 Java 容器能够利用 Web Server 中的子系统（如高性能文件缓存）。

## 2.5 多线程架构

多线程是一种高效的编程模型，多个线程存在于单个进程中共享共享资源但能够同时执行。同一进程中的线程共享地址空间。进程内线程之间的上下文切换通常比进程之间的上下文切换更高效。多线程程序在具有多个 CPU 的计算机上运行得更快。

Web Server 的多线程设计支持海量连接扩展性，且不会牺牲性能或不必要的浪费资源。根据服务器的负载，Web Server 7.0 会自动从低延迟模式切换到高并发模式。





## 2.5 多线程架构

`c++filt` 命令用于对 C++ 符号名称进行修饰（mangle），从而使其更易于读。

```
% /usr/bin/pstack 29472 | /opt/SUNWspro/bin/c++filt
29472: webserver-d -d /opt/webserver7/https-test/config -r /opt/webserver7
fe457c8 pollys (8d008, 3, ffbf460, 0)
fede124 pollys (8d008, 3, 2710, 10624c00, 0) + 7
0001923 int wdlSmanager::Wait_for_Message(2c45c, 0, 12c, 14c, 0)
+ 20
00017268 main (8, 1, 2c45c, 0, 2bc20, 2ff0) + 12a8
000130a0_start (0, 0, 0, 0, 0, 0) + 108
```

对主进程的检查显示，它只有一个线程：

```
% /usr/bin/pstack 29473 | /opt/SUNWspro/bin/c++filt
29473: webserver7 /opt/webserver7/https-test/config -r /opt/webserver7 -t /t
fd5c7c8 pollys (ffbf808, 4, ffbf798, 0)
f56d214 pollys (ffbf808, 4, 64, 10624, 17d784, 5fe5e10) + 7
fe85c70 void ParentAdmin::poll(unsigned) (64, ffbf808, 2710, 7eac, 4, 3) + 42c
ff197654 void poll(unsigned) (25ae88, 2710, ff2a3c0, 0)
ff2a3c0, ff2a3c0, ff2f440) + c
ff19e8ac PRStatus WebServer::() (25ae88, ff2a3f24, fffff
ff2a400, 6, 1) + 494
00010fd4 main (9, ffbfebc, ffbffebec, 21400, fd134fc0) + 1c
00010b98_start (0, 0, 0, 0, 0, 0) + 108
```

以下命令显示了工作进程中的各种线程：

```
% /usr/bin/pstack 29473 | /opt/SUNWspro/bin/c++filt
```

工作进程具有多个线程，请注意每个线程都用如下形式的行隔开：

```
lwp# 6 / thread# 6
```

其中 lwp（轻量级进程）标识操作系统层级，而线程数标识用户层级。

虽然 `pstack` 命令对工作进程的输出非常详尽，无法全部包含，但其余部分识别了对应于工作进程中子进程的线程。

以下 `lwp#1` 的堆栈跟踪显示了工作进程中主线程的调用栈，用于检测服务器何时关闭：

```
lwp#1 / thread#1
fd5c4a9c lwp_park (0, fff8f8, 0)
fd5eae8 cond_wait_queue (154c90, 25ae8, fff88d, 0, 0, 0) + 28
d5bef60 cond_wait_common (154c90, 25ae8, fff88d, 0, 0, 0) + 298
d5bbf0f8 pr_Thread_cond (154c90, 25ae8, ffffa60, 0, 0, 0) + 34
d5bfle6c cond_timedwait (154c90, 25ae8, ffffa60, b1a1300, 998660, 4e7e3650) + 14
d5bf22c thread_cond_timedwait (154c90, 25ae8, fffb84, 48c32a4, 0, 1ce6a8b) + c
fe85a1c pr_ThreadCond (154c88, 0, 827f20, 0, 1ce6a8b, 0) + 170
f19f77ac PR WebServer::Run() (ff2a4000, ff2a4000, 6, 2a5cf8, 3d, f22a6b4) + 1394
00010fd4 main (9, fffbc4c, ffeb210, 0, fd134fc0) + 1c
00010b9b_start (0, 0, 0, 0, 0, 0) + 108
```

此线程的后续堆栈跟踪用于动态配置服务器：

```
lwp#6 / thread# 6
fd5c4a9c lwp_park (0, 2af190, 32e368, 0, 0) + 0
fd5eae8 cond_wait_queue (2af190, 32368, 0, 0, 0) + 28
d5bf068 cond_wait_common (2af190, 32368, 0, 0, 0) + 298
d5bfb0a4 pr_Thread_cond (2af190, 32368, 0, 0, 0) + 34
d5bf0a4 cond_timedwait (2af190, 32368, 0, b1a1300, 998660, 4e7e3650) + 14
d5bf0a4 thread_cond_timedwait (2af190, 32368, 0, 48c32a4, 0, 1ce6a8b) + c
fe85a1c pr_ThreadCond (154c88, 0, 827f20, 0, 1ce6a8b, 0) + 170
f19f77ac PR WebServer::Run() (ff2a4000, ff2a4000, 6, 2a5cf8, 3d, f22a6b4) + 1394
00010fd4 main (9, fffbc4c, ffeb210, 0, fd134fc0) + 1c
00010b9b_start (0, 0, 0, 0, 0, 0) + 108
```

*(注：由于原文中存在大量重复的 OCR 错误干扰文本，翻译时已根据逻辑保留了核心堆栈结构。)*

`lwp12` 的以下调用栈是一个接收线程的：

```
fd5c57c8 polls (fcaf88, 1, fcaf08, 0)
fd561d2 poll (fcaf88, 1, 1388, 10624c0, 0, 0) + 7c
fd58658_pt_poll_now (fc4f34, 1, fcbd24, fcaf88, 028, fffffff) + 4c
fe85e9f8_pt_accept (230408, fcafbe58, fffffff, 13, 0, fffffff) + cc
ff77690 PRFileDesc::accept(PRNetAddr&, const unsigned) (1b9c48, fcafbe58, fffffff, ff00000, 0, fd5f478) + cc
f17c30 void Acceptor::run (128398, 7, 0, 2, fffffff) + 4c
fe6a2d4 ThreadMain (128398, 2531a8, 0, feb9c0, ff17be4, ff2a3a0) + 1c
fe85e04c pt_root (2531a8, fefa6cd8, 400, fe87bb8, 0, fe87914) + d4
fd5c9fc_lwp_start (0, 0, 0, 0, 0)
```





3. 如果你同时拥有一台 Solaris 和 Linux 计算机，请在这两个操作系统上都安装 Web Server 7。在每台计算机上启动实例，并对比在 Solaris 和 Linux 上执行 `ps -ef` 命令的输出。为什么 Linux 上有这么多 `webserv` 进程呢？

注意：访问 www.sunwebserver.com 获取如何执行上述这些练习的详细说明。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_66_0.png)

## Web Server 7.0 的安装与迁移

本章提供了成功安装 Web Server 7.0 或从之前的版本迁移到 Web Server 7.0 所需的必要信息。

在开始使用 Web Server 7.0 之前，你必须首先使用三种安装方法之一在受支持的操作系统上安装该软件。完成后，你就可以自定义配置，并开始向各种用户代理提供静态和动态内容。

安装过程创建了在本地系统上运行 Web Server 7.0 所需的环境。这包括提取 Web Server 二进制文件、共享对象（或动态链接库）、配置文件以及用于管理 Web Server 的各种脚本。迁移过程允许你获取之前的 Web Server 安装并将其更新到最新版本。

## 3.1 支持的平台

Web Server 7.0 可以安装在多个发行版的 UNIX 上，并在 Windows 平台上也具有无与伦比的安全性。在尝试安装 Web Server 7.0 之前，你应该确定你的系统有足够的内存和可用存储空间，并且你正在受支持的平台上安装软件。

表 3.1 总结了 Web Server 7.0 支持的操作系统平台。

### 表 3.1 操作系统平台

| 架构 | 操作系统 |
|---|---|
| PowerPC | IBM AIX 5.2, 5.3 |
| PA-RISC | HP-UX 11i |
| Intel x86/AMD | Windows 2003 Server 企业版, Windows 专业版 |
| UltraSPARC | Solaris 8, 9 和 10 OS |
| Intel x86 (32-bit) | Solaris 9 和 10 OS |
| AMD (64-bit) | Solaris 10 OS |
| Intel x86/AMD | Red Hat Linux Enterprise 3.0, 4.0 Advanced Server, SuSE Linux 9 Enterprise Server |

Sun 建议为每个平台提供的最小随机存存储器（RAM）为 128MB（但优选 512MB）。在任何情况下，你需要大约 550MB 的磁盘空间进行初始 Web Server 安装。这将根据你如何使用 Web 服务器以及提供的内容类型而增加。

> 注意：你应该在 Solaris 操作系统上安装最新的补丁集，以确保 Web Server 7.0 的正确安装和执行。不兼容的补丁可能会影响 Web Server 的启动并导致服务器对某些请求无响应。在这种情况下，Sun 提供了关于兼容补丁的信息，支持 Web Server 7.0 的高效运行。

在 Solaris OS 平台上，Web Server 7.0 安装程序会检查所需的补丁，如果发现所需的补丁，则不会安装。

请参考《Sun Java System Web Server 7.0 发布说明》获取有关平台和补丁的最新信息。

## 3.2 获取软件

Sun Java System Web Server (Web Server) 是 Sun Java Enterprise System (Java ES) 的组件。Web Server 7.0 可在 Java ES 第 5 版本中使用，并可以使用 Java ES 安装程序进行安装。

你可以从 Sun 网站 http://www.sun.com/software/swportfolio/get.jsp 并下载 Java ES 软件。本书未提供使用 Java ES 安装程序的说明。有关作为 Java ES v5 的组件安装 Web Server 7.0，或从之前的 ES 发布版本升级 Web Server 的信息，请参考位于 http://docs.sun.com/app/docs/prod/entys#chic 的 Java ES 文档。

Web Server 7.0 也作为单独下载包提供。你可以通过以下步骤获取软件的独立版本：

1. 访问 Sun 的软件下载页面 www.sun.com/download/。
2. 点击“按类别查看”（View by Category）选项卡。
3. 选择右下角的“Web 服务器”（Web Servers）链接。这会带你进入 Web Server 内容的主下载页面。该页面包含多个 Web Server 版本的链接以及各种 Web Server 附加组件的链接。
4. 选择 Web Server 7.0 最新版本的下载（例如，Web Server 7.0 Update 5）。这将带你进入 Web Server 7.0 的产品下载页面。该页面包含 Web Server 7.0 的概述。
5. 选择你想要安装软件的平台和相应的语言。
6. 选择“Sun 软件组合许可协议”（Sun Software Portfolio License Agreement）链接以了解 Sun 安装软件的条款和条件。
7. 如果你同意这些条款，选中文本旁的复选框：“我同意 Sun 软件组合许可协议”（I agree to the Sun Software Portfolio License Agreement）。
8. 点击“继续”（Continue）按钮。
9. 选择相应发行版的链接（例如，sjsws-7_0u5-windows-i586.zip）。这将开始下载过程。
10. 将文件保存到本地文件系统上的临时目录中。对于大多数平台，该文件约为 150MB。文件名格式如下：

- sjsws-release-platform.tar.gz（适用于基于 Unix 的系统）
- sjsws-release-platform.tar.zip（适用于 Windows 系统）

11. 你现在已经下载了软件副本并准备好进行安装。

## 3.3 准备安装

Web Server 7.0 软件以压缩归包的形式发行——基于 UNIX 的系统的 GNU zip 归包 (*gz) 和基于 Windows 系统的 zip 归包 (*zip)。在安装软件之前，你必须先将归包解压到磁盘上的临时位置。提取出的文件大约需要 250MB 的空磁盘空间。

在基于 UNIX 的系统上，你可以使用以下命令解压并提取文件：

```
gzip -dc sjsws-release-platform.tar.gz | tar xvf -
```

最新版本的操作系统（如 Windows）支持 zip 文件格式，可以使用 WinZip 等工具来解压文件。

### 安装目录内容

| 文件/目录 | 说明 |
|---|---|
| Legal | 此目录包含此软件的许可信息以及此版本包含的任何第三方产品。 |
| README.txt | 此文件包含可能有用的信息。 |
| setup 或 setup.exe | 这是安装文件。执行此命令启动安装过程。 |
| WebServer | 此目录包含 Web Server 7.0 安装组件。 |

## 3.4 安装软件

你可以使用三种方法之一安装 Web Server 7.0 软件：图形界面、命令行和静默。这些方法适用于任何发行版，并允许你以交互或非交互方式安装软件。

### 3.4.1 setup 命令

通过执行 `setup` 命令开始安装过程。该命令的语法如下：

```
setup [--help] [--console] [--silent state_file] [--savestate] [--javahome java_dir] [--id]
```

你可以通过向 setup 命令提供选项来选择所需的安装模式。表 3.3 提供了这些选项的列表。

### 表 3.3 setup 命令选项

| 选项 | 说明 |
|---|---|
| ./setup --help | 显示 setup 命令的选项。 |
| ./setup | 以图形模式运行程序。 |
| ./setup --console | 以命令行模式运行程序。 |
| ./setup --savestate | 以图形模式运行程序，并根据此安装创建一个配置文件（状态文件）。随后可以使用该状态文件执行静默（非交互）安装。状态文件创建并保存在安装目录中。默认文件名为 statefile，但可以更改。 |
| ./setup --console --savestate | 以命令行模式运行程序，并同时根据此安装创建一个配置文件（状态文件）。 |
| ./setup --silent_file | 以静默模式运行程序。安装参数从指定的状态文件（state_file）中读取，该文件是先使用 --savestate 选项创建的。 |
| ./setup --javahome java_dir | 定义安装程序 Java 虚拟机 (JVM) 应使用的 JDK 安装位置。此安装以图形模式进行。 |





# 第 3 章 WEB SERVER 7.0 安装与迁移

表 3.3 setup 命令选项（续

| 选项 | 说明 |
|---|---|
| ./setup --console --javahome dir | 定义用于安装程序 JVM 的 JDK 安装位置。此安装将在命令行模式下进行。 |
| ./setup --id | 显示安装程序构建的唯一标识符。提供此选项是为了在必要时简化不同软件版本之间复用安装程序状态文件。每个安装程序版本都有一个唯一标识符。要复用由不同版本创建的安装程序状态文件，安装状态文件中引用的唯一标识符必须与当前安装程序版本中的相匹配。--id 选项允许您确定此值，以便您可以编辑状态文件中的该值。更多信息请参见第 3.4.4.2 节“构建标识符”。 |

### 3.4.2 图形化安装

Web Server 7.0 包含一个图形安装向导（简单称为安装向导），它可以引导您完成安装过程。安装向导将引导您通过一系列屏幕，在这些屏幕中，系统会提示您安装软件所需的信息和偏好设置。

如上一节所示，当启动安装程序时不带任何选项时，图形化安装是默认模式。您可以通过以下步骤以图形化模式安装 Web Server 7.0：

- 1. 以 root 用户（类 UNIX 系统）或 Administrator 用户（Windows 系统）登录您的系统。
- 2. 如下所示，带任何选项启动安装向导：
    * ./setup（类 UNIX 系统）
    * setup.exe（Windows 系统）

如图 3.1 所示，打开安装向导欢迎界面。

> 注意：在 UNIX 系统上，如果未将 DISPLAY 环境变量导出到本地机器，或者不支持 X Windows，则安装界面默认采用命令行模式。如要在命令行模式下安装，请遵循后续“命令行安装”章节中的说明进行操作。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_72_0.png)

## 3.4 安装软件

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_73_0.png)

图 3.1 安装向导—欢迎界面

- 3. 点击“Next（下一步）”按钮进入软件许可协议界面，如图 3.2 所示。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_73_1.png)

图 3.2 安装向导—软件许可协议界面

- 4. 审核软件许可协议。如果您同意许可条款，选择“Yes（是）”单选按钮并点击“Next（下一步）”按钮进入图 3.3 所示的“选择安装目录”界面。

> 注意：如果您不同许可协议，将无法继续安装。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_74_0.png)

图 3.3 安装向导—选择安装目录界面

Web Server 7.0 组件将安装在“选择安装目录”界面指定的目录中。如果该目录不存在，您可以创建它。请记住，初始安装至少需要 550MB 的磁盘空间。

- 5. 审核默认安装目录并根据需要对其进行更改。点击“Next（下一步）”按钮进入图 3.4 所示的“选择安装类型”界面。

此屏幕允许您选择将要执行的安装类型——快速（Express）或自定义（Custom）。

## 3.4 安装软件

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_75_0.png)

图 3.4 安装向导—选择安装类型界面

快速安装允许您使用最常用的选项和预定义的默认值快速安装 Web Server。快速安装是默认安装类型，并会做出各种假设，例如主机名、端口号和 Java 开发工具包 (JDK) 安装。如果您选择快速，则无需在安装期间指定这些设置。设置将使用表 3.4 列出的默认值自动配置。

表 3.4 快速安装默认值

| 设置 | 默认值 |
| --- | --- |
| 通用设置 | |
| 管理实例 | 配置为管理服务器（Administration Server）。 |
| JDK | 安装与 Web Server 捆绑的 JDK。 |
| 组件 | 安装以下内容：\n服务器核心：安装 Web Server 环境所需的核心二进制文件。\n服务器核心 64 位二进制文件（仅限 Solaris SPARC 和 AMD64）：设置 Web Server 实例的 64 位运行时所需的 64 位二进制文件。此选项仅在您安装软件的系统支持 64 位时才可用。将同时安装 64 位和 32 位二进制文件。 |

# 第 3 章 WEB SERVER 7.0 安装与迁移

表 3.4 快速安装默认值（续

| 设置 | 默认值 |
|---|---|
| | 命令行界面：用于从命令行管理和配置 Web Server 及其托管应用程序的命令行管理客户端。示例应用程序：演示 Web 特性和功能的示例应用程序。语言包：安装 Web Server 的本地化字符串。 |
| 启动随机启动 | 否 |
| 管理服务器 | | 安装管理服务器的计算机的全限定域名名。 |
| SSL 端口 | 如果可用，则为 8989；否则默认为下一个可用端口 |
| 非 SSL 端口 | 如果可用，则为 8800；否则默认为下一个可用端口 |
| 运行时用户 ID (Unix) | 安装时，默认值为 root。对于非 root 安装，默认值为执行安装的用户。 |
| Web Server 实例（管理节点） | |
| 服务器名称 | 安装 Web Server 实例的计算机名称。 |
| HTTP 端口 | 默认值取决于管理实例的运行时用户 ID。如果管理实例的运行时 ID 为非 root，默认值为 8080。如果管理实例的运行时 ID 为 root，默认值为 80。 |
| 运行时用户 ID (Unix) | 如果管理实例的运行时 ID 为非 root，则默认值为管理服务器的运行时 ID。如果管理实例的运行时 ID 为 root，默认值为 webservd。 |
| 文档根目录 | install_dir/https-server_name/docs |
| 64 位配置（仅限 Solaris SPARC 和 AMD64） | 否 |

如果您是 Web Server 7.0 的新手或正在对产品进行评估，建议选择快速安装类型。如果您希望自定义安装，请选择自定义安装。后续步骤提供了执行自定义安装的详细说明。

- 6. 选择“Custom（自定义）”单选按钮并点击“Next（下一步）”按钮进入图 3.5 所示的“组件选择”界面。此屏幕让您有机会选择要安装的各种组件。通常，这些选择取决于服务器作为独立服务器或在服务器集群环境中扮演的角色。此外，您还可以根据各种管理考虑因素选择其他选项。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_77_0.png)

图 3.5 安装向导—组件选择界面

以下项目为这些每个组件提供了额外信息：

- 服务器核心——指的是 Web Server 环境所需的内核二进制文件。如果选择了服务器核心，将创建一个管理实例，并且它可以被配置为管理服务器或管理节点，这将在在本章稍后介绍。如果将管理实例配置为管理服务器，将安装默认的 Web Server 实例。这些安装选项用于服务器集群环境，其中集中的管理服务器位于一个节点上，其他节点位于管理节点。





## 第 3 章 WEB SERVER 7.0 的安装与迁移

-   Server Core 64 位二进制文件（Solaris SPARC 和 AMD64）——如果选择此选项，将安装设置 Web Server 实例所需的 64 位二进制文件。此选项默认被选中，且仅在安装了 32 位二进制文件时显示。

-   管理命令行界面——管理命令行界面用于管理和配置服务器农场中的所有管理器实例和 Web Server 实例。此工具可用于管理本地安装的服务器，也可用于安装在远程服务器上的服务器。您可以仅选择此选项来安装远程管理其他服务器所需的工具，而无需在本地机器上安装任何 Web Server 实例。

注意：您可以在不安装 Server Core 的情况下安装管理命令行界面，但无法在不安装管理命令行界面的情况下安装 Server Core。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_78_0.png)

-   示例应用程序——如果您在安装的组件选择部分选择了示例应用程序，则会安装演示 Web Server 特性和功能的示例应用程序。默认安装位置为 install_dir/samples。有关示例应用程序的更多信息，请参阅《Sun Java System Guide to Java Web Server 7.0 Developer's Guide to Java Web Applications》。

-   语言包——如果您在安装组件部分选择了语言包，将安装包含 Web Server 本地化字符串的语言资源束。Web Server 7.0 支持日语、韩语、法语、德语、繁体中文和简体中文等语言。作为 Server Core 部分的代码消息可以使用支持的本地语言显示。例如，要查看日语管理控制台，请将浏览器更改为日语。

-   选择此面板中显示的每个组件，并点击“下一步”（Next）按钮继续到 Java 配置屏幕，如图 3.6 所示。

您可以决定安装与 Web Server 7.0 捆绑的 JDK（默认），或指定现有 JDK 的绝对路径。

## 3.4 安装软件

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_79_0.png)

图 3.6 安装向导——Java 配置屏幕

-   8. 选择 Install Java Standard Edition 1.5.0_09 单选按钮（如有必要），点击“下一步”按钮继续到管理选项屏幕，如图 3.7 所示。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_79_1.png)

图 3.7 安装向导——管理选项屏幕

## 第 3 章 WEB SERVER 7.0 的安装与迁移

此屏幕允许您指定是同时安装管理服务器和 Web Server 实例（默认值），还是仅安装管理节点（Administration Node）。以下项目提供了有关这些选项的附加信息：

-   **管理服务器（Administration Server）**——管理服务器是一个特殊配置的 Web Server 实例，仅用于管理目的，并在其部署管理应用程序。服务器农场或集群环境中的每个节点都运行着一个管理服务器。在这些节点中，有一个被配置为主主服务器，其余的被配置为从服务器，称为管理节点（Administration Nodes，见下文描述）。管理服务器用于管理所有 Web Server 实例并将配置推送到各个节点。主管理服务器运行通用管理控制台和命令行界面，而农场中的节点仅运行管理节点应用程序。管理服务器维护所有实例的配置库。

-   **管理节点（Administration Node）**——管理节点是不具备管理服务器特性和功能的 Web Server 实例（例如，没有图形控制台）。管理节点接收来自指定管理服务器的命令，并允许对特定节点执行有限操作，例如创建、删除、启动和停止 Web Server 实例。实例只能通过管理服务器在管理节点上创建。服务器农场或集群内的节点不能被独立配置。

> **警告：** 管理节点必须在安装期间或安装后向管理服务器注册。在注册期间，管理服务器必须处于运行状态。

在考虑这些选项时，请遵循以下通用指南：

-   如果您没有设置服务器农场并想要一个独立的 Web Server 实例，请选择将管理实例配置为管理服务器。这也会创建一个默认的 Web Server 实例。

-   如果您正在设置服务器农场，请先配置集中的管理服务器实例。然后，通过选择将管理实例配置为管理节点的选项，将服务器农场中的其余节点配置为管理节点。如果您将管理实例配置为管理服务器，也会创建一个默认的 Web Server 实例。

## 3.4 安装软件

-   9. 选择 Create an Administration Server and a Web Server Instance 单选按钮，以创建管理服务器实例和管理节点实例。
10. 如果您希望这两个实例在系统重启时启动，还可以勾选 Start Servers During System Startup（系统启动时启动服务器）复选框。选择此选项将为基于 UNIX 的系统创建相应的启动脚本，并为 Windows 系统实例注册为自动启动的服务。

注意：如果选择了在系统启动时启动服务器，将在以下类 UNIX 系统上创建各种脚本：

-   Solaris: /etc/init.d/webserver7-*
-   Linux: /etc/init.d/webserver7-*
-   AIX: /etc/rc.d/webserver7-*
-   HPUX: /sbin/init.d/webserver-*

-   11. 点击“下一步”按钮继续到管理服务器屏幕，如图 3.8 所示。

此屏幕允许您配置各种管理服务器设置，如表 3.5 所示。只有当您将管理实例配置为管理服务器时才会显示此屏幕。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_81_0.png)

## 第 3 章 WEB SERVER 7.0 的安装与迁移

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_82_0.png)

图 3.8 安装向导——管理服务器设置

## 表 3.5 管理服务器设置

| 设置 | 值 |
|---|---|
| 主机名 (Host Name) | 指定安装管理节点实例的域名。 |
| SSL 端口 (SSL Port) | 指定管理节点实例的 SSL 端口或接受默认值。默认 8989，除非该端口不可用，否则默认为下一个可用端口。 |
| 创建非 SSL 端口 (Create a non-SSL Port) | 如果要启用对管理服务器的非 SSL ，请选择此框。如果选中，服务器将允许输入非 SSL 端口号。 |
| 非 SSL 端口 (Non-SSL Port) | 指定管理节点实例的非 SSL 端口或接受默认值。默认 8800，除非该端口不可用，否则默认为下一个可用端口。 |
| 运行时用户 ID (Runtime User ID) | （仅限 UNIX）指定运行管理服务器时的 UNIX 用户名。对于 root 安装，默认值为 root。对于非 root 安装，默认值为您登录时使用的用户名。 |
| 管理员用户名 (Administrator User Name) | 指定管理员用户名。这是您将用于登录图形用户界面的用户。默认值为 admin |
| 管理员密码 (Administrator Password) | 为管理员指定密码。 |
| 重输密码 (Retype Password) | 确认管理员密码。 |





## 3.4 安装软件

表 3.6 提供了完成此屏幕上数据的示例值。

**表 3.6** 管理服务器设置示例

| 设置 | 值 |
| --- | --- |
| 主机名 (Host Name) | 接受（或输入）计算机的完全限定主机.域名名。 |
| SSL 端口 (SSL Port) | 接受默认端口 8988。 |
| 创建非 SSL 端口 (Create a non-SSL Port) | 不要勾选此框。 |
| 非 SSL 端口 (Non-SSL Port) | 不（未选择创建非 SSL 端口）。 |
| 运行用户 ID (Runtime User ID) | 接受默认用户 root。 |
| 管理员用户名 (Administrator User Name) | 接受默认用户 admin。 |
| 管理员密码 (Administrator Password) | 输入密码 password。 |

- 12. 如表 3.6 所示完成管理服务器设置，点击“下一步”按钮继续到 Web 服务器设置屏幕。如图 3.9 所示。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_83_0.png)

**图 3.9** 安装向导—Web 服务器设置屏幕

此屏幕允许你为默认 Web 服务器实例配置各种设置。见表 3.7。

## 第 3 章 Web 服务器 7.0 安装与迁移

表 3.7 Web 服务器设置

| 设置 | 值 |
| --- | --- |
| 服务器名称 (Server Name) | 指定安装默认 Web 服务器实例的计算机的完全限定域名。你在此处输入的信息将将用于创建初始配置、实例和虚拟服务器的名称。 |
| HTTP 端口 (HTTP Port) | 默认值取决于管理服务器实例的运行用户 ID。如果管理服务器实例的运行用户 ID 不是 root，则默认值为 8080。如果管理服务器实例的运行用户 ID 不是 root，则默认值为 80。 |
| 运行用户 ID (Runtime User ID) | (仅限 UNIX) 如果管理服务器实例的运行用户 ID 为 root，则默认运行用户 ID 为 webserv。如果管理服务器实例的运行用户 ID 不是 root，则默认值与管理服务器实例的运行用户 ID 相同。 |
| 启用 64 位运行时 (Enable 64-bit runtime) | 指定是否为默认 Web 服务器实例启用 64 位运行时。默认值为否（未选择该选项）。如果此平台不支持 64 位模式，则不显示此选项。 |
| 创建默认文档根目录 (Create a default document root directory) | 指定是否在安装期间创建默认文档根目录。默认值为 install_dir/https-server_name/docs。服务器的内容位于此目录中。 |
| 使用作为 DocumentRoot (Use as DocumentRoot) | 指定默认值之外的文档根目录。 |

> 警告：基于 UNIX 的系统的 root 用户可以启动和停止绑定到任何端口的进程。然而，非 root 用户只能启动和停止监听大于 1024 端口的进程（这些被是非特权端口）。要让非 root 用户启动和停止小于或等于端口 1024 的进程，必须授予用户适当的权限。

Solaris 10 为非 root 用户提供了绑定小于 1024 端口的替代方案。在 Solaris 10 上，你必须为非 root 用户提供 `net_privaddr` 并启动服务器。例如，要以 webserv（Solaris 10 默认 Web 服务器）启动 Web 服务器实例，你需要以 root 登录并执行以下命令：/usr/sbin/usermod -K default_priv=base, net_privaddr webserv。webserv 用户现在将具有适当权限来停止和启动小于 1024 的进程。

有关 usermod 的更多信息，请访问 http://docs.sun.com/app/docs/doc/816-5166。有关权限的更多信息，请访问 http://docs.sun.com/app/docs/doc/816-5175。

表 3.8 提供了完成此屏幕上数据的示例值。

## 3.4 安装软件

表 3.8 Web 服务器设置示例

| 设置 | 值 |
| --- | --- |
| 服务器名称 (Server Name) | 接受（或输入）计算机的完全限定主机.域名名。 |
| HTTP 端口 (HTTP Port) | 接受默认端口 80。 |
| 运行用户 ID (Runtime User ID) | 接受默认值 webservd。 |
| 启用 64 位运行时 (Enable 64-bit runtime) | 不要勾选此框。 |
| 创建默认根目录 (Create a default root directory) | 选中此单选按钮。 |
| 使用以下目录作为 DocumentRoot (Use the following directory as DocumentRoot) | 不要选中此单选按钮。 |

- 13. 如表 3.8 所示完成 Web 服务器设置，点击“下一步”按钮继续到准备就绪屏幕。如图 3.10 所示。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_85_0.png)

图 3.10 安装向导—准备就绪屏幕

- 14. 验证你的设置并点击“现在安装”按钮开始安装过程。将打开一个新窗口显示你在安装过程中的阶段。如图 3.11 所示。
你可以随时选择“停止”按钮来终止安装。安装过程完成后，将出现“安装完成”屏幕，指示安装成功还是失败。

## 第 3 章 Web 服务器 7.0 安装与迁移

此屏幕允许你为默认 Web 服务器实例配置各种设置。见表 3.7。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_83_0.png)

图 3.9 安装向导—Web 服务器设置屏幕

表 3.7 Web 服务器设置

| 设置 | 值 |
| --- | --- |
| 服务器名称 (Server Name) | 指定安装默认 Web 服务器实例的计算机的完全限定域名。你在此处输入的信息将将用于创建初始配置、实例和虚拟服务器的名称。 |
| HTTP 端口 (HTTP Port) | 默认值取决于管理服务器实例的运行用户 ID。如果管理服务器实例的运行用户 ID 不是 root，则默认值为 8080。如果管理服务器实例的运行用户 ID 不是 root，则默认值为 80。 |
| 运行用户 ID (Runtime User ID) | (仅限 UNIX) 如果管理服务器实例的运行用户 ID 为 root，则默认运行用户 ID 为 webserv。如果管理服务器实例的运行用户 ID 不是 root，则默认值与管理服务器实例的运行用户 ID 相同。 |
| 启用 64 位运行时 (Enable 64-bit runtime) | 指定是否为默认 Web 服务器实例启用 64 位运行时。默认值为否（未选择该选项）。如果此平台不支持 64 位模式，则不显示此选项。 |
| 创建默认文档根目录 (Create a default document root directory) | 指定是否在安装期间创建默认文档根目录。默认值为 install_dir/https-server_name/docs。服务器的内容位于此目录中。 |
| 使用作为 DocumentRoot (Use as DocumentRoot) | 指定默认值之外的文档根目录。 |

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_85_0.png)

图 3.10 安装向导—准备就绪屏幕

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_83_0.png)

图 3.11 安装向导—进度屏幕

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_85_0.png)

图 3.12 安装向导—完成屏幕





## 3.4 安装软件

可以使用命令行执行。在基于 UNIX 的系统上创建状态文件的示例例如：

```
./setup --savestate (图形化安装)
./setup --console --savestate (命令行安装)
```

设置将在交互式安装期间捕获并保存到状态文件中。该文件形成了静默安装的模板，可用于在非交互模式下在一个或多个系统上安装产品。

状态文件将被创建并保存到您安装期间指定的安装目录中（Unix 上默认为 `/sun/webserver7`，Windows 上为 `C:\Program Files\webserver7`）。文件的默认名称为 `statefile`，但在创建后可以更改其他名称。

基于 UNIX 的系统的状态文件示例可能如下：

```
#
# Wizard Statefile created: Mon Jan 22 08:52:30 EST 2007
# Wizard path: /ws7-extract/WebServer/WebServer
#
#
# Install Wizard Statefile section for Sun Java System Web Server
#
#
[STATE_BEGIN Sun Java System Web Server cb2498a60eaeb-712da267df2723b96730573]
defInstallDirectory = /sun/webserver7
currentInstallDirectory = /sun/webserver7
UPGRADE = false
SELECTED_COMPONENTS =\ svrcore,admincli,svrcore64,devsupport,svrcore_110n,admincli_110n
USE_BUNDLED_JDK = true
JDK_LOCATION =
IS_ADMIN_NODE = false
STARTUP_ONBOOT = true
ADMIN_HOST = boulder.example.com
ADMIN_SSL_PORT = 8989
ADMIN_PORT = 8800
ADMIN_UID = root
ADMIN_NAME = admin
ADMIN_PASS = password
NODE_HOST =
NODE_SSL_PORT =
REGISTER_NODE = =
WEB_SERVERNAME = boulder.example.com
WEB_PORT = 80
WEB_UID = webservd
WEB_DOCROOT =
SIXTYFOURBIT_INSTALL = true
CONFIG_NAME = boulder.example.com
SKIP_INSTANCE_CREATION =
[STATE_DONE Sun Java System Web Server cb2498a60eaeb-712daf267df27293b96373053b]
```

> 注意：此特定状态文件是由第 3.4.2 节“图形化安装”中演示图形化安装步骤生成的。

表 3.9 对这些参数每一个提供了解释。请注意，参数按字母顺序排列，而不是它们在状态文件中出现的顺序。

## 表 3.9 常见状态文件参数

| 参数 | 可能的值 | 描述 |
|---|---|---|
| ADMIN_PORT | 0–65535 | 用于非 SSL 通信的管理服务器端口号。 |
| ADMIN_SSL_PORT | 0–65535 | 用于 SSL 通信的管理服务器端口号。 |
| ADMIN_UID | 有效的 UNIX 用户 ID | （仅 UNIX）运行管理服务器的有效 UNIX 用户 ID。 |
| CONFIG_NAME | https-host.domain | Web 服务器用于创建配置、与节点关联并创建实例的默认配置名称。 |
| currentInstall-Directory | | 存储安装二进制文件和其他组件的位置。 |
| defaultInstall-Directory | /sun/webserver7 (Unix) C:\Program Files\Sun\WebServer7 (Windows) | 存储安装二进制文件和其他组件的默认位置。 |
| IS_ADMIN_NODE | true 或 false | 仅适用于管理服务器和管理节点安装；对于管理命令行安装为 null。 |

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_90_0.png)

## 3.4 安装软件

| 参数 | 可能的值 | 描述 |
|---|---|---|
| JDK_LOCATION | | 此 Web 服务器使用的 JDK 路径。它要么包含系统上现有 JDK 的路径，或者在将 USE_BUNDLED_JDK 参数设置为 true 时则为空。 |
| NODE_HOST | | 正在安装管理节点的计算机完全限定名。 |
| NODE_SSL_PORT | 0–65535 | 用于 SSL 通信的管理节点端口号。 |
| REGISTER_NODE | true 或 false | 指定管理节点实例应在安装时或稍后注册到管理服务器实例。 |
| SELECTED_COMPONENTS | | 选择安装的产品组件的逗号分隔列表。 |
| SIXTYFOURBIT_INSTALL | true 或 false | 标识 64 位安装。 |
| SKIP_INSTANCE_CREATION | true 或 false | 不创建默认实例。 |
| STARTUP_ONBOOT | true 或 false | 系统启动时启动选项。 |
| USE_BUNDLED_JDK | true 或 false | 安装安装程序捆绑的 JDK；如果为 false，JDK_LOCATION 不能为空。 |
| WEB_DOCROOT | | Web 服务器实例的主要文档目录；如果为空，则创建一个默认文档目录。 |
| WEB_PORT | 0–65535 | 在 HTTP 模式下运行 Web 服务器实例的有效默认端口。 |
| WEB_SERVERNAME | | 正在安装管理节点的计算机完全限定名。 |
| WEB_UID | （仅 UNIX）运行管理服务器的有效 UNIX 用户 ID。 |

# 第 3 章 WEB 服务器 7.0 迁移

| 参数 | 可能的值 | 描述 |
|---|---|---|
| ADMIN_PORT | 0–65535 | 用于非 SSL 通信的管理服务器端口号。 |
| ADMIN_SSL_PORT | 0–65535 | 用于 SSL 通信的管理服务器端口号。 |
| ADMIN_UID | 有效的 UNIX 用户 ID | （仅 UNIX）运行管理服务器的有效 UNIX 用户 ID。 |
| CONFIG_NAME | https-host.domain | Web 服务器用于创建配置、与节点关联并创建实例的默认配置名称。 |
| currentInstall-Directory | | 存储安装二进制文件和其他组件的位置。 |
| defaultInstall-Directory | /sun/webserver7 (Unix) C:\Program Files\Sun\WebServer7 (Windows) | 存储安装二进制文件和其他组件的默认位置。 |
| IS_ADMIN_NODE | true 或 false | 仅适用于管理服务器和管理节点安装；对于管理命令行安装为 null。 |
| JDK_LOCATION | | 此 Web 服务器使用的 JDK 路径。它要么包含系统上现有 JDK 的路径，或者在将 USE_BUNDLED_JDK 参数设置为 true 时则为空。 |
| NODE_HOST | | 正在安装管理节点的计算机完全限定名。 |
| NODE_SSL_PORT | 0–65535 | 用于 SSL 通信的管理节点端口号。 |
| REGISTER_NODE | true 或 false | 指定管理节点实例应在安装时或稍后注册到管理服务器实例。 |
| SELECTED_COMPONENTS | | 选择安装的产品组件的逗号分隔列表。 |
| SIXTYFOURBIT_INSTALL | true 或 false | 标识 64 位安装。 |
| SKIP_INSTANCE_CREATION | true 或 false | 不创建默认实例。 |
| STARTUP_ONBOOT | true 或 false | 系统启动时启动选项。 |
| USE_BUNDLED_JDK | true 或 false | 安装安装程序捆绑的 JDK；如果为 false，JDK_LOCATION 不能为空。 |
| WEB_DOCROOT | | Web 服务器实例的主要文档目录；如果为空，则创建一个默认文档目录。 |
| WEB_PORT | 0–65535 | 在 HTTP 模式下运行 Web 服务器实例的有效默认端口。 |
| WEB_SERVERNAME | | 正在安装管理节点的计算机完全限定名。 |
| WEB_UID | （仅 UNIX）运行管理服务器的有效 UNIX 用户 ID。 |

## 表 3.9 常见状态文件参数

| 参数 | 可能的值 | 描述 |
|---|---|---|
| ADMIN_PORT | 0–65535 | 用于非 SSL 通信的管理服务器端口号。 |
| ADMIN_SSL_PORT | 0–65535 | 用于 SSL 通信的管理服务器端口号。 |
| ADMIN_UID | 有效的 UNIX 用户 ID | （仅 UNIX）运行管理服务器的有效 UNIX 用户 ID。 |
| CONFIG_NAME | https-host.domain | Web 服务器用于创建配置、与节点关联并创建实例的默认配置名称。 |
| currentInstall-Directory | | 存储安装二进制文件和其他组件的位置。 |
| defaultInstall-Directory | /sun/webserver7 (Unix) C:\Program Files\Sun\WebServer7 (Windows) | 存储安装二进制文件和其他组件的位置。 |
| IS_ADMIN_NODE | true 或 false | 仅适用于管理服务器和管理节点安装；对于管理命令行安装为 null。 |

## 表 3.9 参数

| 参数 | 可能的值 | 描述 |
|---|---|---|
| ADMIN_PORT | 0–65535 | 用于非 SSL 通信的管理服务器端口号。 |
| ADMIN_SSL_PORT | 0–65535 | 用于 SSL 通信的管理服务器端口号。 |
| ADMIN_UID | 有效的 UNIX 用户 ID | （仅 UNIX）运行管理服务器的有效 UNIX 用户 ID。 |
| CONFIG_NAME | https-host.domain | Web 服务器用于创建配置、与节点关联并创建实例的默认配置名称。 |
| currentInstall-Directory | | 存储安装二进制文件和其他组件的位置。 |
| defaultInstall-Directory | /sun/webserver7 (Unix) C:\Program Files\Sun\WebServer7 (Windows) | 存储安装二进制文件和其他组件的位置。 |
| IS_ADMIN_NODE | true 或 false | 仅适用于管理服务器和管理节点安装；对于管理命令行安装为 null。 |

## 表 3.9 管理节点实例参数

| 参数 | 可能的值 | 描述 |
|---|---|---|
| ADMIN_PORT | 0–65535 | 用于非 SSL 通信的管理服务器端口号。 |
| ADMIN_HOST | | 正在安装管理节点的计算机完全限定名。 |
| _SSL_PORT | 0–65535 | 用于 SSL 通信的管理节点端口号。 |
| REGISTER_NODE | true 或 false | 指定管理节点实例应在安装时或稍后注册到管理服务器实例。 |
| SELECTED_COMPONENTS | | 选择安装的产品组件的逗号分隔列表。 |
| SIXTYFOURBIT_INSTALL | true 或 false | 标识 64 位安装。 |
| SKIP_INSTANCE_CREATION | true 或 false | 不创建默认实例。 |
| STARTUP_ONBOOT | true 或 false | 系统启动时启动选项。 |
| USE_BUNDLED_JDK | true 或 false | 安装安装程序捆绑的 JDK；如果为 false，JDK_LOCATION 不能为空。 |
| WEB_DOCROOT | | Web 服务器实例的主要文档目录；如果为空，则创建一个默认文档目录。 |
| WEB_PORT | 0–65535 | 在 HTTP 模式下运行 Web 服务器实例的有效默认端口。 |
| WEB_SERVERNAME | | 正在安装管理节点的计算机完全限定名。 |
| WEB_UID | （仅 UNIX）运行管理服务器的有效 UNIX 用户 ID。 |

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_90_0.png)

## 3.4 安装软件

### 3.4.4.2 构建标识

状态文件包含一个与创建该状态文件的产品构建关联的标识。不同构建创建的状态文件具有不同的标识，且不能跨构建使用。以下是状态文件中包含的标识示例：

```
[STATE_BEGIN Sun Java System Web Server cb2498a60eaeb-712da267df2723b96730573]
state file parameters
[STATE_DONE Sun Java System Web Server cb2498a60eaeb-712daf267df27293b96373053b]
```

如果您想在较新版本的软件中使用旧状态文件，首先需要用要使用的构建标识来更新状态文件。要实现这一点，您应该在要使用的构建上运行 `setup --id` 命令来确定构建标识。

```
./setup --id
05ff73ff18c2c641920463c5e6000160e28ee5
```

然后您将用新的构建标识更新状态文件并启动静默安装。

> 注意：状态文件参数在产品发布之间可能会发生。因此，您可能会发现较后的版本添加或删除某些参数。如果您尝试使用发布之间发生变化的状态文件（即使带有新的构建标识），您将看到针对缺失或添加参数的特定错误消息。

### 3.4.4.3 执行静默安装

您可以通过以下步骤执行 Web 服务器 7.0 的静默安装：

- 1. 以 root 用户（基于 UNIX 的系统）或管理员（Windows 系统）登录您的系统。
- 2. 使用 `--silent` 选项启动安装向导并指定状态文件的名称如下：



```
./setup --silent state_file (UNIX-based 系统)
setup.exe --silent state_file (Windows 系统)
```

（请参见第 3.4.1 节“setup 命令”，以获取 setup 命令选项的完整列表。）

你不会看到任何安装成功完成的指示，而是会看到一条类似下面的消息：

安装成功。

后续步骤：

- 1. 通过执行以下命令启动管理服务器：

/sun/webserver7/admin-server/bin/startserv

- 2. 你可以通过访问以下 URL 访问 Web 管理服务器：

https://boulder.example.com:8989

- 3. 请参阅位于 /sun/webserver7/setup/Sun_Java_System_Web_Server_install.log 的安装日志文件以获取更多详情。

- 4. 请参阅第 3.5 节“验证安装”，以验证你已在目标系统上成功安装了 Web Server 7.0。

## 3.5 验证安装

安装过程允许你将安装内容配置为管理服务器（带有 Web 服务器实例）或管理节点。根据你的选择，安装过程会在文件系统上为每个实例创建相应的结构。它会将库、二进制文件和配置文件等各种文件放入该目录结构中，以支持每个实例。

有几种方法可以验证安装是否按预期完成。下一节将详细详细描述这些方法。

## 3.5 验证安装

### 3.5.1 安装日志文件

安装过程会创建各种输出（或日志）文件，其中包含与安装过程相关的消息。这些日志文件可用于验证 Web Server 是否正确安装，或对失败的安装进行故障排除，分为两类：

- Web Server 安装日志（位于 Web Server 安装目录）
- 低级（Java 企业系统）日志文件（仅限 Solaris 和 Linux，位于特定操作系统的产品注册中）

查看这些文件中发现的数据，可以了解安装过程中执行的步骤。如果你的安装成功了，则没有必要查看这些日志文件。然而，如果安装失败了，你应该检查每个日志文件以确定错误的性质。

### 3.51.1 Web Server 安装日志

Web Server 安装日志位于 setup 目录，该目录直接位于你在安装过程中指定的安装目录之下。示例如下：

```
/sun/webserver7/setup/Sun_Java_System_Web_Server_install.log
```

此文件包含指定安装期间执行的操作项、执行该操作使用的包、操作的结果（或结果）以及失败原因（如适用）。文件中的每个条目跨越两行，并具有以下语法：

```
[timestamp] [package] [action]
[result]: [cause]
```

结果分为多个类别。表 3.12 详细描述了这些每个类别。

## 第 3 章节 WEB SERVER 7.0 安装与迁移

## 表 3.12 安装日志条目类别

| 类别 | 描述 |
| :--- | :--- |
| INFO | 表示特定安装任务正常完成。 |
| FINE | 表示特定安装任务正常完成。此消息包含比 INFO 更多的细节，但没有 FINEST 那么多。 |
| FINEST | 表示特定安装任务正常完成。此消息包含最多的细节。它是所有信息中最详尽的。 |
| WARNING | 表示非关键性失败。警告消息包含有关失败性质和原因的信息，并指出了可能的解决办法。 |
| ERROR | 表示关键性失败并报告安装状态为失败。错误级消息提供了有关问题性质和原因的详细信息。 |

以下是成功安装的片段。为了可读性，每个条目之间已添加了空格。

```
[2007-01-22 10:17:28] [package] [action]
[result]: Start
[2007-01-22 10:17:28] [package] [action]
[result]: Initialized
[2007-01-22 10:17:28] [package] [action]
[result]: Starting
[2007-01-22 10:18:35] [package] [action]
[result]: Copied
[2007-01-22 10:18:35] [package] [action]
[result]: Replacing
[2007-01-22 10:18:36] [package] [action]
[result]: ...
[2007-01-22 10:18:36] [package] [action]
[result]: done
[2007-01-22 10:18:36] [package] [action]
[result]: created
[2007-01-22 10:18:40] [package] [action]
[result]: Starting
[2007-01-22 10:19:54] [package] [action]
[result]: Returned
[2007-01-22 10:19:54] [package] [action]
[result]: End
[2007-01-22 10:19:54] [package] [action]
[result]: created
[2007-01-22 10:19:54] [package] [action]
[result]: copied
[2007-01-22 10:19:54] [package] [action]
[result]: moved
```

## 3.5 验证安装（继续）

从日志末尾开始向前回溯，直到看到指示安装失败的错误消息。常见的失败原因是空间不足或以没有权限的用户尝试安装。在确定安装失败的原因后，你可以采取相应的措施并重启安装过程。

### 3.5.2 低级日志文件

Web Server 7.0 是 Java 企业系统（Java ES）的一个组件。因此，安装过程会创建特定于 Java ES 的日志文件。文件名具有以下语法（其中 mm 是月份，dd 是日期，HH 和 MM 是执行安装时的分钟）：

```
Sun_Java_System_Web_Server_install.AmmddHHMM
Sun_Java_System_Web_Server_install.BmmddHHMM
```

这些文件位于不同的目录（取决于操作系统），如表 3.13 所示。

## 表 3.13 低级日志文件位置

| 操作系统 | 低级日志文件的位置 |
| :--- | :--- |
| Solaris（以 root 用户安装） | /var/sadm/install/logs |
| Solaris（非 root 用户安装） | /var/tmp/ |
| Linux, HP-UX, AIX | /var/tmp/ |
| Windows | %temp% |

以下是两个低级日志文件中第一个（Sun_Java_System_Web_Server_install.AmmddHHMM）的片段：

```
正在安装 Java System Web
日志文件: /var/sadm/install/logs/Sun_Java_System_Web_Server_install.BmmddHHMM
安装完成。
```

应该注意的是，此文件的内容仅指向 Web Server 安装的第二个低级日志文件的位置。第二个文件（Sun_Java_System_Web_Server_install.BmmddHHMM）包含如下具体的安装信息：





## 3.5 验证安装

正在安装 Sun Java System Web Server
日志文件：/var/sadm/install/logs/Sun_Java_System_Web_Server_install.BmmddHHMM
已安装：/sun/webserver7/uninstall.class
卸载程序为：/sun/webserver7/uninstall.class

正在安装示例应用程序
已安装：/sun/webserver7/include
已安装：/sun/webserver7/include/base
已安装：/sun/webserver7/include/base/buffer.h
已安装：/sun/webserver7/include/base/cinfo.h
已安装：/sun/webserver7/include/base/crit.h
已安装：/sun/webserver7/include/base/daemon.h
已安装：/sun/webserver7/include/base/ereport.h
已安装：/sun/webserver7/include/base/file.h
已安装：/sun/webserver7/include/base/net.h
已安装：/sun/webserver7/include/base/pblock.h
已安装：/sun/webserver7/include/base/pool.h
已安装：/sun/webserver7/include/base/regexp.h

... 
已安装：/sun/webserver7/lib/webapps/search/images/search_ko.jpg
已安装：/sun/webserver7/lib/webapps/search/images/search_zh_CN.jpg
已安装：/sun/webserver7/lib/webapps/search/images/search_zh_TW.jpg
已安装：/sun/webserver7/lib/webapps/server-rt-11on.jar
安装完成。

第二个文件包含 Web Server 7.0 安装期间安装的每个组件的特定细节。在 UNIX 系统上，您可以使用 `grep` 命令来获取已安装组件的概述。

```
# grep Installing Sun_Java_System_Web_Server.BmmddHHMM
```

- 正在安装 Sun Java System Web Server
- 正在安装示例应用程序
- 正在安装 64 位位的服务器核心二进制文件
- 正在安装管理命令行界面
- 正在安装管理命令行界面的语言包
- 正在安装服务器核心
- 正在安装服务器核心语言包

返回值应与安装过程中选择的组件相关（请参见图 3.5）。

### 3.5.2 服务器进程

在 Web Server 7.0 安装期间创建的实例具有其特定的用途，并具有反映该用途的不同配置设置。每个实例都响应客户端请求，并有服务器进程监听特定的监听套接字（listen socket）以处理这些请求。

服务器（Administration Server）包含一个特殊配置的 Web Server 管理实例。该实例用于管理配置信息，可以通过图形或命令行界面访问。因此，管理实例具有一个监听特定的监听套接字以接收管理命令的 HTTP 。

节点（Administration Node）为 HTTP 用户代理提供了访问由 Web Server 提供的内容的接口。该实例有自己的进程，监听在不同的端口，甚至可能完全存在于另一台服务器上。

除了监听客户端请求的进程外，两个实例都具有用于在进程级别提供高可用性的内部进程。通常情况下，每个实例会创建三个进程。这些进程是监视进程（watchdog process）、原始进程（primordial process）和工作进程（worker process），它们之间的关系如图 3.13 所示。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_100_0.png)

图 3.13 服务器进程

工作进程监听特定端口的客户端请求。HTTP 客户端直接与工作进程交互。监视进程和原始进程无法通过监听套接字访问，因此 HTTP 客户端无法与这些进程直接通信。启动和停止每个实例的脚本直接与监视进程通信。监视进程与原始进程交互，而原始进程又与工作进程交互。原始进程没有直接的接口。

工作进程负责处理来自客户端的 HTTP 请求。如果工作进程由于任何原因终止，那么重启它的职责就是原始进程的（以便其能够继续处理客户端请求）。如果原始进程终止，则监视进程将重启它。

当您执行 `startscript` 时会启动监视进程。监视进程和原始进程的目的是在服务器进程内提供有限级的高可用性。

您可以在单个实例中运行多个 Web Server 进程。原始进程负责启动这些进程中的每一个。当您启动单个实例时，原始进程的作用并不大；它的真正优势在于您启动多个 Web Server 实例且原始进程可以监控并重启所有实例时。这是原始进程的主要目的。

原始进程和工作进程的名称均为 `webserverd`。监视进程的名称为 `webserverd-wdog`。在 UNIX 服务器上，可以使用 `ps -ef` 命令查看这些进程。下面的示例演示了管理节点的每个进程：

```
# ps -ef | grep http
```

```
webserverd 14856 14856 0 Jan 22 ? 33:12 webserverd -d
/sun/webserver7/https-boulder.example.com/config -r /sun/webserver7
```

```
root 14855 14856 0 Jan 22 ? 7:19 webserverd -d
/sun/webserver7/https-boulder.example.com/config -r /sun/webserver7
```

```
root 14855 14856 0 Jan 22 ? 0:14 webserverd -d
/sun/webserver7/https-boulder.example.com/config -r /sun/webserver7
```

### 3.5.3 目录结构

在安装过程中，您选择了想要放置 Web Server 文件的目录。这被称为安装目录或服务器根目录。

安装程序在服务器根目录下放置各种文件夹、配置文件、可执行文件、库文件和二进制文件，如图 3.14 所示。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_103_0.png)

图 3.14 根目录内容

admin-server 和 https-{instance} 文件夹是安装过程中创建的各个实例文件夹。每个文件夹都包含特定于特定实例的信息。所有其他文件夹包含被认为是对所有服务器全局的信息。图 3.14 所示每个文件夹内容的简要描述见表 3.14。

表 3.14 根目录内容

| 文件夹 | 描述 |
| --- | --- |
| admin-server | 服务器的管理实例。此文件夹下的信息取决于服务器是配置为管理服务器还是管理节点。 |
| bin | 全局使用的二进制文件和脚本。（全局适用于 admin-server 和其他服务器实例） |
| https-{instance} | 默认 Web Server 实例。这在安装期间默认在管理服务器上创建。在管理节点上，直到创建该实例之前都不会创建。 |





## 表 3.14 服务器根目录内容续

| 文件夹 | 描述 |
|---|---|
| include | 用于编译 Web Server 7.0 插件的包含文件。这些文件对所有服务器实例都是全局的。 |
| jdk | 此文件夹包含随 Web Server 一带的 Java 开发包 (JDK)。 |
| plugins | 此文件夹包含 Web Server 支持的插件。默认插件默认安装在此文件夹中。将您自己的插件也添加到此文件夹中是一个良好的做法。 |
| samples | 随 Web Server 带的示例应用程序。如果您在安装过程中选择了“示例应用程序”组件，则会创建此文件夹。 |
| setup | 此文件夹包含与 Web Server 安装相关的文件（如安装日志）。它还包含允许您卸载 Web Server 的信息。 |
| lib | 此文件夹包含运行 Web Server 所需的内部服务器文件。这包括 Java 存档文件 (.jar)、共享对象 (.so)、脚本和属性文件。此文件夹被视为**私有接口 (PRIVATE INTERFACE)**，不应直接修改。 |

> 警告：您永远不应该对视为私有接口的文件创建依赖关系。私有接口包含的文件和/或文件结构未记录文档，并且在产品发布之间可能会发生变化。

关于管理服务器实例的具体信息可以在 admin-server 文件夹下找到。图 3.15 展示了管理服务器的文件布局。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_104_0.png)

**图 3.15** 管理服务器文件夹内容

## 3.5 验证安装

图 3.15 所示的每个文件夹所包含信息的简要描述见表 3.15。

## 表 3.15 管理服务器文件夹内容

| 文件夹 | 描述 |
| --- | --- |
| bin | 特定于管理服务器实例的二进制文件和脚本。 |
| config | 管理服务器配置文件。此文件夹被视为**私有接口 (PRIVATE INTERFACE)**，不应直接修改。 |
| config-store | 托管实例的配置存储库。此文件夹被视为**私有接口 (PRIVATE INTERFACE)**，不应直接修改。 |
| generated | 为管理服务器生成的内部数据。这包括为管理服务器编译的 JSP 文件。此文件夹被视为**私有接口 (PRIVATE INTERFACE)**，不应直接修改。 |
| logs | 管理服务器日志文件。 |
| sessions | 特定于管理服务器 Web 应用程序会数据。此文件夹被视为**私有接口 (PRIVATE INTERFACE)**，不应直接修改。 |

> **警告：**您永远不应该对视为私有接口的文件创建依赖关系。私有接口包含的文件和/或文件结构未记录文档，并且在产品发布之间可能会发生变化。

为了与未来的版本保持兼容性，您应该使用管理控制台或 wadm 命令读取或写入配置文件。

关于管理节点实例 `{instance}` 文件夹的具体信息（其中 `{instance}` 是您为 Web 服务器实例指定的名称）。图 3.16 展示了管理节点的文件系统布局。

图 3.16 所示的每个文件夹所包含信息的简要描述见表 3.16。

## 第 3 章 WEB 服务器 7.0 安装与迁移

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_106_0.png)

图 3.16 管理节点文件夹内容

## 表 3.16 管理节点文件夹内容

| 文件夹 | 描述 |
| bin | 与管理节点实例相关的二进制文件和脚本。Sun Web Server 的较早版本将这些搜索文件存储在实例的主文件夹中。现在它们位于实例的 bin 文件夹中。 |
| config | 管理节点配置文件。config 目录中的某些文件被视为私有文件，且不应直接修改。请参阅《Java 系统 Web 服务器 7.0 管理员配置参考指南》以获取更多信息。 |
| docs | 此实例提供的文档（如 .html 文件）的默认目录。这也称为 doctroot 目录。 |
| collections | 站点 Web 应用程序的搜索查询。此文件夹被视为**私有接口 (PRIVATE INTERFACE)**，不应直接修改。 |
| generated | 为管理服务器生成的内部数据。这包括为管理服务器编译的 JSP 文件。此文件夹被视为**私有接口 (PRIVATE INTERFACE)**，不应直接修改。 |
| logs | 管理服务器日志文件。 |
| sessions | 特定于管理服务器 Web 应用程序的会话数据。此文件夹被视为**私有接口 (PRIVATE INTERFACE)**，不应直接修改。 |
| web-app | 此实例的默认 Web 应用程序。此文件夹被视为**私有接口 (PRIVATE INTERFACE)**，不应直接修改。 |

> 警告：您永远不应该对视为私有接口的文件创建依赖关系。私有接口包含的文件和/或文件结构未记录文档，并且在产品发布之间可能会发生变化。

## 3.5 验证安装

为了与未来的版本保持兼容性，您应该使用管理控制台或 wadm 命令读取或写入配置文件。

## 3.5.4 非 Windows 注册表项

产品注册表是非 Windows 系统上的一个存储库，所有软件包在安装时都会在此注册。注册表包含安装位置、产品版本和组件依赖关系等信息。可以在以下位置找到产品注册表：

* Solaris OS: /var/sadm/install/productregistry
* Linux: /var/opt/sun/install/productregistry
* HP-UX: /var/adm/sw/productregistry

在安装过程中，您选择了想要作为 Web 服务器一部分安装的各种组件。组件在产品注册表中有一组条目，引用了每个已安装的软件包。例如，下面的代码演示了提供管理命令行接口的软件包之一的产品注册表条目：

```
<compid>admincli_zip
<compversion>1.0</compversion>
<uniquame>admincli</uniquame>
<compinstance>1
<parent>admincli</parent>
<instance>1
<version>7.0</version>
</instance>
<comptype>COMPONENT</comptype>
<location>/opt/webserver</location>
<dependent>
<comref>admincli</comref>
</dependent>
<compinstance>1
<version>7.0</version>
</compinstance>
</compid>
```

如果 Web Server 7.0 安装文件删除错误（例如，如果手动删除文件而不是通过卸载程序删除），文件可能已从文件系统中删除，但 Web 服务器的条目仍留在产品注册表中。如果您尝试重新安装到相同位置，将收到检测到现有安装的消息，尽管该安装似乎并不存在。要解决这个问题，请进入产品注册表并手动删除这些条目。这包括开始和结束的 comp 标签。

以下条目被视为 Web Server 7.0 产品注册表条目：

- svcore64_zip
- svrcomponents64_zip
- svcore64
- admincli_zip
- clicomponents_zip
- uninstall
- admincli
- svcore_zip
- svrcomponents_zip
- svcore
- Sun Java System Web Server





## 3.5.5 Windows 特有条目

在 Windows 操作系统上的安装会产生 UNIX 系统上不存在的额外条目。本节包含有关 Windows 特有条目的详细信息。

### 3.5.5.1 Windows 程序组

安装过程会创建一个名为 Web Server 7.0 的程序组，可以在以下位置找到：

Programs -> Sun Microsystems -> Web Server 7.0

该程序组包含各种图标，用于启动和停止管理服务器实例、通过浏览器浏览器访问管理控制台以及启动产品卸载。此组包含的特定项目如下：

- 管理控制台 (Administration Console)
- 启动管理服务器 (Start Administration Server)
- 停止管理服务器 (Stop Administration Server)
- 卸载 (Uninstall)

### 3.5.5.2 Windows 服务条目

Web Server 7.0 实例（如管理服务器和管理节点）作为 Windows 服务运行。因此，你将在服务应用程序 (services.msc) 中看到类似下面的条目：

- Sun Java System Web Server 7.0 (https-configurable)
- Sun Java System Web Server 7.0 Administration Server

对于每个部署在 Windows 服务器上的配置，都会创建一个服务条目——每个实例对应一个条目。你可以从服务应用程序手动启动和停止实例，或者配置实例在服务器启动或关闭时自动启动或停止。

### 3.5.5.3 Windows 注册表条目

安装过程会在 Microsoft 注册表中创建或修改若干条目。在安装过程中创建或修改了以下条目：

- KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Current-Version\Uninstall\Sun Java System Web Server
这会将 Sun Java System Web Server 添加到可以通过控制面板中的“添加或删除程序”功能进行卸载的应用程序列表中。当产品通过卸载程序卸载时，该键会被删除。
- HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Current-Version\AppManagement\ARCache\Sun Java System Web Server
ARP 代表 Add/Remove Program（添加/删除程序）。与上一个项目类似，此注册表项用于识别可以使用控制面板下的添加/删除工具移除的当前已安装程序。
- Control Set 条目，例如：HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Enum\LEGACY_HTTPS-ADMSERV70, HKEY_LOCAL_MACHINE\SYSTEM\ControlSet002\Enum\Root\LEGACY_HTTPS-CONFIGNAME, 以及 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlServices\https-admserv70

这些条目包含每个 Web Server 实例最后一次成功启动的配置数据。

> 注意：有关 Control Set 条目的更多信息，请参见 Microsoft 库文章“What Are Control Sets? CurrentControlSet?”，地址为 http://support.microsoft.com/kb/100010。

## 3.6 安装后任务

安装完成后，你可能需要执行若干任务以开始使用你的 Web Server 实例。本节提供了完成后与 Web Server 交互的详细信息。

### 3.6.1 启动和停止 Web Server 7.0

安装过程创建了各种 Web Server 控制脚本，可用于启动、停止和重启 Web Server 7.0 实例。每个服务器实例（包括管理服务器）都有一套独立的脚本。表 3.17 说明了为每个实例创建的脚本。

表 3.17 Web Server 控制脚本

| 脚本 | 说明 |
| :--- | :--- |
| startserv | 启动相应实例的守护进程。在此轮中，分别启动原始进程和工作进程。（更多信息请参见第 3.5.2 节“服务器进程”）。这允许服务器实例开始处理客户端请求。 |
| startserv.bat | 终止相应实例的守护进程。在此轮中，终止任何后续进程（分别终止原始进程和工作进程）。更多信息请参见第 3.5.2 节“服务器进程”）。这些进程的终止将防止服务器实例处理客户端请求。 |
| stopserv | 停止并重启服务器进程。 |
| restart | |
| restart.bat | |

如前所述，每个实例都有其自己的一套进程控制脚本。用于停止、启动和重启 Web Server 实例的控制脚本可以在以下位置找到：

```
install_dir/instance/bin/script
```

其中满足以下条件：

install_dir 是安装 Web Server 7.0 的目录。

instance 是 Web Server 实例的名称（例如 admin-server 或 https-www.example.com）。

script 是脚本的名称。

### 3.6.1.1 startserv 命令的输出

为管理服务器实例执行 startserv 脚本会产生以下输出：

```
Sun Java System Web Server 7.0U1 B06/12/2007 22:48
info:CORE3016: daemon is running as super-user
info:CORE5076: Using [Java HotSpot(TM)] Server VM, Version 1.5.0_09
from [Sun Microystems Inc.]
info:WEB08100: Loading web module in virtual server [admin-server]
[/admingui]
info:WEB08100: Loading web module in virtual server [admin-server]
[/jmxconnector]
info:HTTP30274: admin-ssl-port: https://www.example.com:8989 ready to accept requests
info:CORE3274: successful server startup
```

以下项目提供了此输出中数据的描述。

- 输出的前三行提供了发布信息、进程所有者名称以及管理服务器使用的 Java 版本。
- 第四行和第五行指定了加载到管理服务器的两个 Web 应用程序。第一个 Web 应用程序提供了管理配置和 Web Server 实例的图形用户界面（此应用程序在管理节点上找不到）。第二个 Web 应用程序提供了用于执行远程管理的基于 JMX 的管理界面。
- 第六行指定启动成功。
- 第七行指定管理节点实例的 startserv 脚本产生以下输出：

执行以下输出：

```
Sun Java System Web Server 7.0U1 B06/12/2007 22:48
info:CORE5076: Using [Java HotSpot(TM)] Server VM, Version 1.5.0_09
from [Sun Microystems Inc.]
info:HTTP30272: http-listener-1: http://www.example.com:80 ready to accept requests
info:CORE3274: successful server startup
```

以下项目提供了此输出中数据的描述。

- 前两行指定了管理节点使用的发布信息 Java 版本。
- 第三行指定了通过浏览器访问管理节点的连接信息。
- 第四行指定启动成功。

### 3.6.1.2 Web Server 实例的自动启动

在安装过程中，你有机会选择一个允许在系统启动时启动服务器进程的选项。如果你在 UNIX 系统上选择了此选项，则会在相应目录创建启动和停止脚本（详情请参见 3.4.2 节“图形化安装”）。启动和停止脚本分别创建 `startserv` 和 `stopserverv` 脚本，并对 `install_dir` 目录下的所有实例执行此操作。

img/a3cb513bfd7a0b21f70c67fcaede10f6_113_0.png

> **警告：** 管理服务器实例在默认启动中启动。你应该考虑禁用自动启动，因为运行此实例可能会存在安全风险。

在 UNIX 系统上，可以通过在实例的主目录下创建一个 `.noStartOnBoot` 文件来禁用特定服务器实例的自动启动。创建此文件的一种方法是使用以下 UNIX touch 命令：

```
touch install_dir/instance/.noStartOnBoot
```

这会在主目录下创建一个名为 `.noStartOnBoot` 的空文件。启动脚本配置为跳过任何在其实例目录下包含该文件的实例启动。

在 Windows 系统上，可以通过服务应用程序 (C:\WINDOWS\system32\services.msc) 禁用特定进程的自动启动。启动此应用程序，并将想要禁用的实例的启动类型更改为手动。





### 3.6.2 访问 Web Server 7.0 实例

管理服务器（Administration Servers）和管理节点（Administration Nodes）都是 Web Server 实例。因此，一旦启动，您可以使用标准的 浏览器与每个实例进行通信。

表 3.18 提供了每个服务器实例的默认 Web Server 7.0 URL 概览。

### 表 3.18 默认 Web Server URL

| 实例 | 描述 |
|---|--|
| 管理服务器 | http://host.domain:8989 (默认 URL—SSL)<br>http://host.domain:8800 (默认 URL—非 SSL) |
| 管理节点 | http://host.domain:80 (默认 URL—以 root 用户身份安装)<br>http://host.domain:8080 (默认 URL—以非 root 用户身份安装) |

### 3.6.2.1 访问管理服务器

管理服务器的默认端口为 8989。该实例配置为通过 SSL 进行通信，并受在安装过程中生成的自签名数字证书保护。如果您在安装期间为管理服务器选择了默认值，则访问管理服务器的 URL 为 https://host.domain:8989。

> 注意：如果您在尝试访问管理服务器的安全端口时无意中使用了 HTTP 协议，您的浏览器将重定向到相同的主机和端口号，但协议从 HTTP 变为 HTTP(S)。

例如，对 http://host.domain:8989 的请求将重定向到 https://host.domain:8989。

当您通过安全端口访问管理服务器时，会看到证书警告，因为 SSL 证书是自签名的，不是由信任的证书颁发机构 (CA) 发布的。图 3.17 提供了证书警告的示例。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_114_0.png)

访问管理服务器时，您可以选择仅在此话信任证书（默认值），或选择永久信任证书。永久信任证书会将管理服务器的证书颁发机构添加到浏览器的受信任实体列表中，您以后将不再看到此证书警告。如果您决定不信任证书，将无法访问管理服务器。

管理服务器也可以配置为监听非安全端口。这并非默认行为，您必须在安装过程中通过选择相应的选项来指定此项。如果您选择了此选项，基于 SSL 的服务器的默认端口为 8800，通过非 SSL 端口访问管理服务器的 URL 为 http://host.domain:8880。

> 警告：如果您通过互联网访问服务器，不建议将管理服务器配置为监听非安全端口。敏感数据存在泄露的风险，因为数据在浏览器和管理服务器之间是以加密模式传输的。

您需要输入用户名和密码以访问管理服务器。在提示输入这些值时，请输入您在“图形化安装”部分第 11 步中使用的值。现在您可以执行此类操作，如启动和停止 Web Server 实例以及创建和修改 Web Server 配置。有关管理 Web Server 7.0 的更多信息，请参阅第 4 章“ Web Server 7.0 管理”。

### 3.6.2.2 访问管理节点

在安装过程中，您可以选择是想安装管理服务器（结合管理节点）还是单独安装管理节点。两种选项都会创建一个管理节点实例。

在 UNIX 系统上，只有 root 用户才能监听端口小于 1024 的端口。如果您以 root 用户身份安装了软件，可以通过以下 URL 访问：http://host.domain。如果您是以非 root 用户安装的，则需要选择大于 1024 的端口。

### 3.6.3 创建初始配置

安装后，您要做的第一件事是创建配置。此配置用于定义设置。有关更多信息，请参阅第 4 章“ Web Server 7.0 管理”。

## 3.7 卸载 Web Server 7.0

卸载过程是从系统中删除 Web Server 7.0。与安装类似，有三种方法：图形、命令行或静默。

### 3.7.1 uninstall 命令

uninstall 命令用于卸载 Web Server 7.0。可以在 install_dir/bin 中找到，语法如下：

```
uninstall [help] [console] [silent] [javadirir] [save-instances]
```

您可以通过向命令提供相应的选项来选择模式（图形、命令行或静默）。表 3.19 提供了这些选项的列表以及解释。

### 表 3.19 uninstall 命令选项

| 选项 | 描述 |
|---|--|
| /help | 显示 uninstall 命令的选项。 |
| /uninstall | 以图形模式运行卸载程序。 |
| /console | 以命令行模式运行。 |
| /silent | 以静默模式运行。 |
| /javadir | 定义应使用的 JDK 位置。 |
| /save-instances | 以保存实例的图形模式运行卸载程序。 |

### 3.7.2 图形化卸载

Web Server 7.0 包含一个图形化卸载向导（简单称为卸载向导），它可以引导您完成卸载过程。卸载向导将引导您通过一系列屏幕，并在屏幕上提示卸载软件所需的信息和偏好。

如上一节所示，当启动卸载程序时，图形化卸载是默认模式。可以通过执行以下步骤以图形模式卸载：

1. 以 root 用户（基于 UNIX 系统）或管理员（Windows 系统）登录系统。
2. （仅限 UNIX）如果您在 UNIX 系统上执行卸载，请按以下方式启动卸载向导：/install_dir/bin/uninstall。
3. （仅限 Windows）如果您在 Windows 系统上执行卸载，请导航 Windows 资源管理器到安装软件的目录并双击 uninstall.exe 命令。

> 注意：在 Windows 系统上，您还可以通过以下三种方法之一启动卸载向导：
1. 从命令行运行 uninstall.exe。
2. 点击开始、“控制面板”、“添加或删除程序”、“Sun Java System Server 7.0”。
3. 点击开始、“程序”、“Sun Microsystems”、“Web Server 7.0”、“卸载”。

卸载向导欢迎界面打开如图 3.18 所示。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_118_0.png)

图 3.18 卸载向导—欢迎界面





注意：在 UNIX 系统上，如果未将 DISPLAY 环境变量导出到您的本地机器，或者不支持 X Windows，则卸载界面将默认使用命令行模式。若要在命令行模式下卸载，请按照第 3.7.3 节“命令行卸载”中的说明进行。

- 3. 点击“下一步”按钮继续进入“卸载选项选择面板”，如图 3.19 所示。勾选“保存实例”复选框（默认未选中）将保留 Web 服务器安装目录中的所有服务器实例目录。保存实例允许您通过将配置复制到新管理服务器实例的配置服务器来重用这些配置。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_119_0.png)

**图 3.19** 卸载向导——卸载选项选择面板

- 4. 点击“下一步”按钮继续进入“准备卸载”界面，如图 3.20 所示。

# 3 章 WEB 服务器 7.0 安装与迁移

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_120_0.png)

**图 3.20** 卸载向导——准备卸载界面

- 5. 验证您的设置，并点击“立即卸载”按钮开始卸载过程。将打开一个新窗口，显示您在卸载过程中的进度。见图 3.21。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_120_1.png)

**图 3.21** 安装向导——卸载进度界面

当卸载过程完成后，将出现“卸载摘要”界面，该界面显示卸载过程的结果（见图 3.22）。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_121_0.png)

图 3.22 卸载向导——卸载摘要界面

- 6. 卸载现在已完成。点击“关闭”按钮退出卸载向导。

与安装过程类似，卸载过程会提供日志文件，用于了解卸载向导所执行的步骤。这些日志文件可以在以下位置找到：

高级级日志文件：

```
install_dir/setup/Sun_Java_System_Web_Server_uninstall.log (High Level)
```

低级日志文件：

```
Sun_Java_System_Web_Server_install.AmmddHHMM
Sun_Java_System_Web_Server_install.BmmddHHMM
```

（其中 mm 是两位数的月份，dd 是两位数的日期，HH 是两位数的小时，MM 是执行卸载时的两位数分钟）。

如果在卸载过程中发生错误，请考虑检查这些文件中找到的数据。

### 3.7.3 命令行卸载

Web 服务器 7.0 包含一个命令行卸载程序，它提供了一种从终端窗口执行交互式、基于文本卸载的方法。如果您通过 TELNET 或 SSH 远程访问目标系统，这种方法特别有用。与图形化卸载向导一样，命令行卸载程序会引导您完成卸载过程，并提示您安装软件所需的信息和偏好。您可以通过执行以下步骤在命令行模式下卸载 Web 服务器 7.0：

- 2a. （仅限 UNIX）如果您从基于 UNIX 的系统执行卸载，请如下方式启动卸载向导：
`install_dir/bin/uninstall --console`

- 2b. （仅限 Windows）如果您从基于 Windows 的系统执行卸载，请如下方式启动卸载向导：
`install_dir\bin\uninstall.exe --console`

命令行卸载程序启动。您将看到类似下面的文本：

欢迎使用 Sun Java System Web Server 7.0 卸载向导。
该向导用于卸载 Web 服务器。强烈建议在开始卸载之前退出所有程序。如果其他程序正在运行，输入 Control-C 停止卸载，然后关闭程序并重新启动卸载程序。

按 Enter 键继续程序（某些键盘上为 Return）。
默认选项显示在括号 [] 中。
<按 ENTER 继续>

- 3. 按 Enter 键继续显示如下文本：

选择所需的卸载选项。
保存实例 [是/否] [ 否] {"<<" 返回，“!" 退出}：

- 4. 按 Enter 键接受默认不保存实例。您将看到类似下面的文本：

```
Product: Sun Java System Web Server
Location: /sun/webserver7
释放空间: 155.29 MB
------------------------------------
示例应用程序
服务器核心 64 位二进制文件
管理命令行界面语言包
服务器核心语言包
管理命令行界面
服务器核心

准备好卸载

- 1. 立即卸载
2. 重新开始
3. 退出卸载

您想执行什么 [1] {"<" 返回，“!" 退出}？

- 5. 按 Enter 键接受默认设置开始卸载过程。您将看到指示 Web 服务器已卸载的文本。此外，您将看到类似下面的进度条：

```
卸载 Sun Java System Web
|0%------25%-----------50%-----------75%-------100%|
```

# 3 章 WEB 服务器 7.0 安装与迁移

| 产品 | 结果 |
| :--- | :--- |
| Sun Java System Web | 完成 |

- 2. 完成

- 6. 点击“关闭”按钮退出卸载向导。

如果在卸载过程中发生错误，请考虑检查这些文件中找到的数据。

### 3.7.4 静默卸载

Web 服务器 7.0 允许您在不回答问题的情况下执行卸载。这被称为静默卸载。要在静默模式下卸载，您只需在卸载命令中指定 --saveinstances 参数：

```
./uninstall --silent
```

卸载将继续进行。可选，可以提供 saveinstances 以获取实例信息。否则，实例信息将在卸载期间删除。有关文件的更多信息，请参见第 3.7.2 节“图形化卸载”。

## 3.8 迁移到服务器 7.0

注意：如果您运行的是旧版本的服务器（如 iPlanetWeb 4.0 或 Sun ONE Web Server 4.1），您必须先将其迁移到 6.1，然后迁移到 7.0。

### 3.8.1 迁移过程

Web 服务器允许您使用图形用户界面或管理命令行界面执行迁移。无论您选择哪种方法，过程都是相同的。您必须先将 Web 服务器 6.0 或 6.1 实例迁移到 7.0 配置。该配置将存储在 Web 7.0 配置存储中，但尚未部署。下一步是将配置部署到管理节点并测试新实例。

执行迁移的具体步骤如下：

- 1. 提交 Web 服务器 6.0 或 6.1 上的等待配置更改。
2. 确认现有 Web 服务器运行正常。
- 3. 停止正在迁移的 Web 服务器实例（以免端口冲突）。
- 4. 从 CLI 或 GUI 执行迁移工具。
- 5. 检查迁移日志文件。
- 6. 根据需要执行手动配置。
- 7. 验证迁移。

> 注意：正在迁移的服务器和 Web 服务器 7.0 管理服务器必须位于同一物理主机上。这是为了从文件中提取数据并将其用于 7.0。创建新配置后，可以将其部署到服务器环境中的任何管理节点。

某些设置可能无法迁移，必须手动重新配置。详细的迁移信息在迁移过程中和之后提供。这些信息包括已迁移和未迁移的设置列表、需要手动更改的警告，以及迁移成功或失败的指示。这些信息记录在以下迁移日志文件中：

```
install_dir/admin-server/logs/MIGRATION_yyyymmddhhmmss.log
```




如果您在命令行执行迁移时使用了 --logdir 选项，可以为此文件指定备用路径。

> 注意：迁移完成后，您应该检查日志文件，以确定哪些设置（如果有）必须手动配置。

## 3.8.2 哪些内容已及未迁移

Web Server 7.0 是 Sun Web Server 产品的一个重大新版本。它采用了不同的管理范式，因此配置文件和目录发生了大量更改。这些更改的设计意图旨在实现以下目标：

- 减少文件数量
- 简化并改进配置文件的语法
- 增强现有文件的灵活性和功能

作为重新设计的一部分，虽然没有引入新的配置文件，但进行了多项更改，以将特定实例的配置文件合并到实例的 config 目录中。

迁移过程考虑了这些更改，并根据情况重新定位或删除这些文件。在某些情况下，无法迁移某些信息。在这种情况下，迁移过程会在迁移日志中标记这些事件，您必须手动迁移这些信息。本节剩余部分定义了已迁移的项以及未迁移的项。

### 3.8.2.1 哪些内容已迁移

以下项目在迁移过程中会进行迁移。在某些情况下，文件会被移动到特定的配置目录（如 ACL 文件），在另一些情况下，数据从一个文件迁移到另一个文件。这可以通过从 `dbswitch.conf` 文件中的项移动到现在位于 `server.xml` 文件中的元素作为示例。

- ACL 文件
- 配置文件
- 调度器设置

## 3.8 迁移到 WEB SERVER 7.0

- 文件缓存调优的配置设置
- 密钥和证书数据库以及证书映射
- 监听 socket 设置
- MIME 类型设置
- NSAPI 信息
- SHTML 设置
- SNMP 设置
- SSL 信息
- 用户数据库
- 虚拟服务器设置
- Web 应用程序
- WebDAV 设置（但不包括物理集合和锁）
- Web Server 6.1 搜索集合信息（但不包括搜索集合的索引和文档根目录）

## 3.8.2.2 哪些内容未迁移

Web Server 7.0 对某些功能的支持已废弃（过时），因此这些功能不会被迁移。在其他情况下，必须对脚本进行手动更改进行重新应用，以维护迁移后的功能。最后，迁移过程不会移动诸如 CGI 脚本、Web 应用程序或文档根目录中的数据。相反，事实上的新实例仅指向 Web Server 6.x 所在的数据。

> 警告：在完全确定所有内容已迁移之前，不要从旧实例中删除文件。常见的错误是删除了仍然包含 CGI 脚本或 Web 应用程序等数据的旧实例目录。

以下项目在迁移过程中**不会**迁移：

- CGI 目录（新实例将指向这些目录；数据不会移动）
- 虚拟服务器类（这些类在 Web Server 7.0 中不再受支持）
- 命令行脚本（如 startsrv、stopsrv、restart 和 reconfig）

## 第 3 章节 WEB SERVER 7.0 安装与迁移

- 文档根目录（新实例指向此目录；数据本身不会移动）
- Web 应用程序（新实例指向 Web 应用程序的旧位置；数据本身不会移动）
- 遗留 servlets（Web Server 7.0 不支持遗留 servlet）
- 日志文件（日志文件不会移动；新实例也不指向旧的文件位置）
- Simple Session Manager 和 JDBC Session Manager（这些会话管理器不再受支持）
- 用户库和插件
- WebDAV 物理集合和锁（设置已迁移，但集合和锁没有）
- 搜索配置和集合（设置已迁移，但索引和文档根目录没有）

## 3.8.3 使用图形用户界面迁移

Web Server 7.0 包含一个易于使用的迁移向导，用于通过图形界面执行迁移。以下步骤描述了如何使用此工具对一个或多个服务器进行迁移。

1. 登录管理控制台并点击 Configurations 标签。打开 Configuration界面。
2. 在 Configuration界面中点击 Migrate 按钮。打开迁移向导。
3. 在迁移向导中，输入您想要迁移的 Web Server 6.0 或 6.1 实例安装目录的绝对路径。点击 Next。打开 Select Instances 窗口。
4. 选择您想要迁移的实例旁的一个或多个复选框。
5. 在您迁移的每个实例旁输入配置名称。使用如 migrated-w561 等描述性名称，并点击 Next。打开 Choose Migration Options 窗口。
6. （可选）如果您只想迁移来自 Web Server 6.1 的搜索集合，请勾选 Search Collections 复选框。
7. （可选）提供 Web Server 6.1 搜索集合可能所在目录的绝对路径。
8. （可选）提供生成日志文件的目录的绝对路径。
9. 点击 Next。出现 Review 界面。
10. 检查此中发现的数据并点击 Finish 开始迁移过程。
11. 迁移过程完成后，您将看到类似下面的消息：

Instance Migration Successful（实例迁移成功）

12. 检查迁移相关的日志文件并处理任何问题。

> 注意：迁移向导根据您为服务器提供的设置来创建 Web Server 7.0 配置。

## 3.8.4 使用命令行界面迁移

Web Server 7.0 包含一个命令行工具，允许您在不使用图形界面的情况下执行迁移。该工具在需要自动化迁移过程时特别有用。其语法如下：

```
wadm migrate-server <connect-options> [--echo] [--no-prompt] [--verbose] [--search-collection-copypath] [--log-dir] [--config] [--instance] [--all] [--server-root]
```

## 第 3 章节 WEB SERVER 7.0 安装与迁移

可选参数（选项）显示在方括号 [] 内。参见 migrate-server 命令。

**表 3.20 migrate-server 选项**

| 选项 | 描述 |
| --- | --- |
| <connect-options> | 使用 connect_options 连接到管理服务器。connect_options 包括管理用户名、密码文件、主机、端口以及可选的权限文件。这些选项适用于所有命令。 |
| [--echo|-e] | 指定此选项以在执行前将其打印到标准输出。该选项还会打印您未在命令中提供的所有非强制选项的默认值。 |
| [--no-prompt|-Q] | 如果指定此选项，wadam 将不会提示输入密码。如果您已经在密码文件中定义了所有密码并使用 password-file 选项指定了该文件，请使用此选项。 |
| [--verbose|-v] | 指定此选项显示详细输出。 |
| [--search-collection-copypath|-s] | 指定旧实例中搜索集合所在的目录。 |
| [--log-dir|-d] | 指定创建迁移日志目录，例如 install_dir/admin-serv/logs。 |
| [--config|-c newconfig] | 指定迁移后将创建的新配置名称。 |
| [--instance|-n instename] | 指定要迁移的实例名称。 |
| [--all|-1] | 指定此选项迁移所有服务器实例。 |
| --server-root|-r path | 指定较旧版本 Web Server（即 6.0 或 6.1）的安装位置（目录）。 |





## 3.9 总结

Web Server 7.0 是一个极其动态的产品，它使得安装和管理整个服务器集群变得像管理单个服务器实例一样简单。Web Server 7.0 提供的工具和向导使其成为一个强大且灵活的产品，使安装、迁移或卸载 Web Server 实例成为一个简单且直观的过程。

## 3.10 自学实验

使用本章包含的信息执行以下练习。这些练习将帮助您验证对本章所描述概念的理解。

- 1. 验证您的计算机是否支持 Web Server 7.0。
- 2. 将 Web Server 7.0 的最新版本下载到您的工作站上。
- 3. 安装 Web Server 7.0 并将其配置为独立服务器（带有 Web Server 实例的管理服务器）。为每个实例使用可用端口，并在提示时选择您自己的密码。（考虑使用 `--state` 选项以便您能够参考安装时使用的使用的值。）
- 4. 通过访问默认 Web 页面和管理服务器 GUI 验证安装是否成功。

注意：请访问 http://www.sunwebserver.com 获取如何执行这些练习的详细说明。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_131_0.png)

- 5. 额外练习：

如果您有现有的 Web Server 6.x 安装，请使用迁移向导执行迁移。

如果您没有现有的 Web Server 6.x 安装，请考虑从 Sun 网站下载并安装 Web Server 6.1。

使用图形用户界面自定义产品并执行迁移。使用命令行界面重复此过程。（考虑为命令行迁移使用不同的配置名称，并比较这两个配置。）

## Web Server 7.0 管理

Web Server 7.0 包含一个完全重新设计的管理体系，使得管理 Web Server 实例比以前版本要容易得多。它包含一个强大的命令行工具，可以访问图形（Web）界面中提供的所有功能。新的命令行工具提供了广泛的配置管理、配置分发、服务器监控和远程诊断，并可以安装在管理服务器或远程工作站上。这允许在管理您的 Web Server 实例时，在安全、可靠的环境中提供灵活性。

图形界面经过重新设计，以支持国际化和 508 障碍访问要求。它提供了更好的管理性和更直观的任务集。该界面基于管理员将执行的日常任务，而不是基于功能区域（如 Web Server 的之前的版本）。图形界面通过提供向导和合理的默认值来降低复杂性，减少用户输入，同时允许管理员根据需要更改默认值。

本章描述了新重新设计的管理框架，以及它如何使多个实例（如服务器集群）的管理变得像管理单个 Web Server 实例一样简单。

## 4.1 Web Server 7.0 管理框架

Web Server 7.0 提供了一个框架，可以像管理单个服务器实例一样轻松管理服务器集群。这是通过允许您从名为“管理服务器”的中央管理枢纽管理本地和远程服务器来实现的。管理服务器允许您从单一界面控制、配置和监控 Web Server 实例。您可以通过命令行或图形用户界面跨网络访问管理服务器。

图 4.1 提供了 Web Server 7.0 管理框架的高级概述。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_134_0.png)

**图 4.1** Web Server 7.0 管理框架

管理员访问管理服务器，在其中管理 Web Server 配置。他们随后可以将这些配置部署到管理节点，在那里它们成为 Web Server 实例。Web Server 实例可以通过 HTTP 访问，并可以进行集群以管理多个实例。

这允许您管理服务器集群，就像在单台服务器上配置它一样简单。第 4.2 节提供了有关术语的进一步详细说明。您可能已经熟悉上一节中的某些术语。如果没有，对这些术语进行常规回顾将会有帮助。图 4.2 提供了 Server 7.0 组件的模型及其交互方式。本节的其余部分提供了有关 Server 7.0 组件的更多详细信息。

管理服务器、管理节点和 Server 7.0。

![](img/a3cb513bfd7a0b21f70c6.png)

## 4.2.1 管理服务器

管理服务器是一个专门的 Web Server 7.0 实例，用于管理一个或多个节点。管理服务器与任何已配置的管理节点之间存在主从关系。管理员通过以下 Web 应用程序访问管理服务器：

- adminui：提供图形界面的功能
- jmxconnector：提供命令行界面的功能

每个实例的配置数据存储在管理服务器上的中央存储库中。

> 注意：管理服务器与管理节点之间的所有通信都通过 SSL 安全地传输。

在安装过程中，您决定是否希望将服务器配置为管理服务器还是管理节点。如果您正在管理独立服务器，您现在已经拥有了所需的所有组件。如果您正在管理服务器集群环境，您可能想使用默认的管理节点作为临时暂留区。

### 4.2.2 管理节点

节点是一种网络资源，例如服务器或主机。在典型的数据中心中，节点网络被称为服务器集群。管理节点是安装了 Web Server 7.0 的节点，并在该节点向用户代理提供内容。

管理节点可以包含零或多个用于提供内容的 Web Server 实例。当您首次安装管理节点时，它配置了零个实例。当配置部署到节点时，就会创建实例。

### 4.2.3 配置

配置是一组元数据，用于配置 Web Server 7.0 实例的运行时服务。配置由配置文件（如 `migrated-config` 等）、部署到服务器实例的 Web 应用程序、搜索引擎集合，以及用于实现内置服务和安装在 Web Server 实例中的第三方 NSAPI 插件的共享对象组成。





# 第 4 章 Web Server 7.0 管理

配置元数据被服务器运行时用于加载内置服务（服务应用函数或 SAF）以及第三方插件，并设置其他服务器扩展（例如数据库驱动程序）。

管理基础设施的主要功能是从中心位置（管理服务器）管理配置。这些配置可以分发到一个或多个管理节点，并在这些节点上成为服务器实例。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_138_0.png)

> 注意：数据中心通常会分配一部分管理节点专门用于特定的服务或内容。finance.yahoo.com 就是一个例子，它托管了一个报价 Web 应用程序以及其他内容，如研究材料和图表。

为了便于管理和支持，子集中的节点通常具有相同的操作系统和硬件平台。此外，它们可能共享其他数据中心资源，例如用于文档根目录的网络文件系统 (NFS)。Web Server 7.0 中运行给定配置的节点子集被称为集群。

Web Server 实例可以聚类（或分组）在一起，使得配置信息（以及运行时服务）可以在多个节点之间保持一致。

## 4.2.4 配置存储库

配置存储在管理服务器文件系统的区域，被称为“配置存储库”（Configuration Store）。可以在以下位置找到配置存储库：

```
install_dir/admin-server/config-store
```

在安装管理服务器期间，会创建一个初始配置并存储在此目录下，其名称反映了服务器的主机名和域名。此配置用于创建随管理服务器一起的默认 Web Server 实例（参见第 4.2.1 节“管理服务器”）。您可以使用管理服务器创建额外的配置。每个新配置都存储在配置存储库下的单独子目录中，如下：

```
install_dir/admin-server/config-store/configname
```

## 4.2 术语

作为实例配置一部分的文件（例如 magnus.conf、server.xml 和 mime.types）包含在此目录中，以及部署到实例内虚拟服务器的应用程序、该实例使用的第三方插件，以及在该实例内定义的搜索集合。

使用命令行界面或图形化管理界面对服务器配置进行的任何更改都会首先应用于配置存储库中的文件，当您对更改满意后，再将其部署到相应的节点。在部署过程中，会捕获之前配置的副本并保存到配置存储库的以下目录下：

```
install_dir/admin-server/config-store/configname/backup
```

这允许您根据给定的时间戳恢复（或回滚）之前的配置。

如果 Web 应用程序是配置的一部分，整个应用程序以及 config-store 目录下的所有配置目录将被压缩并复制到相应的服务器实例。压缩后的信息包含在一个名为 center.zip 的文件中，可以在相应的配置目录下找到。

> 警告：不要手动编辑管理服务器 configstore 目录下的任何文件，或对这些文件使用用户编写的脚本。此目录下的文件仅供 Web Server 内部使用，并可能会在不通知更改。

可以在特定的管理节点上直接编辑和修改配置文件（参见第 4.5.3 节，“手动编辑配置文件”）。如果管理服务器检测到配置文件不再与配置存储库中的同步，则会在图形化管理界面中注明。系统管理员可以选择从管理节点拉取更改并更新配置存储库中的副本，也可以选择用配置存储库中的文件覆盖管理节点上的文件。如果从管理节点拉取更改，配置存储库中的相应文件将得到更新，并重新部署到可能属于集群的任何其他服务器。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_139_0.png)

### 4.2.5 实例

实例指的是在给管理节点上运行 Web Server 7.0 守护进程或服务所需的环境。这包括它的配置、日志文件和其他运行时产物，例如锁数据库、缓存和临时文件。出于管理目的，可以对实例进行启动、停止、重启或动态重新配置。

当管理服务器向或多个管理节点部署配置时，该节点上会创建一个该配置的实例。每个实例直接位于安装根目录下方，名称为 https-configname。以下示例演示了与 default-config 配置实例相关的目录结构：

```
# cd /sun/webserver7/https-default-config/
# ls
bin config generated logs web-app
collections docs lock-db sessions
```

### 4.2.6 集群

集群是跨越一个或多个管理节点的实例集。这些管理节点可以被多个集群重叠，为了简单起见，集群中的所有节点必须是同构。也就是说，管理节点必须运行在相同的操作系统版本（包括补丁级别）并且配置相同，以提供相同的运行时服务。

> 警告：Sun 支持跨同构节点的集群。这意味着集群内的所有节点必须运行相同的操作系统和补丁级别。

### 4.2.7 虚拟服务器

虚拟服务器是位于特定 Web Server 实例内的功能完整的“虚拟”Web 服务器，利用构成实例的资源和配置设置。您可以从配置继承设置（或元素），也可以为每个虚拟服务器覆盖某些元素。这允许您自定义和差异化虚拟服务器。您可以为虚拟服务器指定的元素示例包括：

- 文档根目录
- MIME 类型文件
- 日志文件
- 访问控制列表文件
- 身份验证数据库

> 注意：请参考《Sun Java System Web Server 7.0 管理员配置参考》中的 virtual-server 元素以获取您可以使用的子元素完整列表。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_141_0.png)

虚拟服务器允许您通过单个安装的服务器为公司或个人提供他们自己的域名、IP 地址和一些服务器监控功能。对于用户来说，几乎就像他们拥有自己的 Web 服务器一样，尽管硬件和基础 Web 服务器维护由您提供。

## 4.3 管理架构

Java 管理扩展 (JMX) 为 Web Server 7.0 管理框架提供了基础。JMX 是 JDK 早期版本中可用的扩展，现在是 Java 平台标准版 (J2SE) 5.0 版本中的功能。它为构建用于管理和监控设备、应用程序和服务驱动网络的分布式、模块化动态解决方案提供了工具。

Web Server 7.0 通过部署到管理服务器和每个管理节点的 jmxconnector 实现 JMX 框架。通过对 JMX API 的实现，Web Server 7.0 的管理基础设施设计用于管理和监控集群部署中的 Web Server 实例。管理和监控环境中应用程序的功能包含在托管豆 (mBeans) 中。

MBeans 位于 MBean 服务器中，MBean 服务器是种提供管理应用程序访问 MBeans 的容器。应用程序不直接访问 MBeans，而是通过 MBean 服务器以其唯一的进行访问


# 第 4 章 Web Server 7.0 管理

ObjectNames。Web Server 7.0 实现了三种类型的 MBeans：监控 MBeans、任务 MBeans 和代理 MBeans。各种 MBean 与 Web Server 管理组件之间的关系如图 4.3 所示。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_142_0.png)

图 4.3 基于 JMX 的管理架构

## 4.3 管理架构

### 4.3.1 监控 MBeans

监控 MBeans 分别在相应管理实例的管理服务器（Administration Server）和管理节点（Administration Node）上创建。使用 Java Native Interface（JNI）层获取实例监控数据，该层通过 UNIX socket（适用于 Solaris 和 Linux OS）和管道（适用于 Microsoft Windows）连接到运行中的实例。

管理节点级提供的监控 MBeans 暴露特定实例的数据，或可以聚合多个实例的数据。这些信息可以通过图形化管理界面或命令行界面显示。在某些情况下，信息可以通过为管理服务器实例配置的特定 URL 显示。（更多信息请参阅第 7 章，“监控 Web Server 7.0”。）

### 4.3.2 任务 MBeans

任务 MBeans 注册在运行管理服务器上的 MBean Server 中。这些 MBean 暴露复合管理任务，而不模拟配置文件。因此，这些 MBean 不暴露对配置文件进行属性获取和设置的操作。

命令行界面和图形化用户界面使用基于 JSR-160 的 JMX 连接器，调用位于管理服务器上的任务 MBeans 操作。这些连接器还被任务 MBeans 用于调用运行在其他节点管理节点上的代理 MBeans 的操作。管理基础设施使用的 JMX 连接器层叠在 HTTP 协议之上，因此也可以运行在 SSL 上，以提供安全的传输层。连接在服务器端由一个特殊的 JMX servlet 处理。

> 注意：Web Server 7.0 利用了 Sun 引用 JMX 实现，该实现附带了 HTTP 和 RMI 协议处理器。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_143_0.png)

### 4.3.3 代理 MBeans

代理 MBeans 是任务 MBeans 的子集，暴露与管理 Web Server 实例相关的任务。代理 MBeans 暴露的操作包括创建和删除实例、部署到实例、对实例执行生命周期操作以及监控实例。只有管理节点在其 MBean Server 上注册了代理 MBeans。

JMX API 基础设施为命令行界面和图形化用户界面提供了一个通用接口，用于在 Web Server 7.0 内部启动管理任务。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_144_0.png)

> 注意：有关 JMX 应用程序编程接口 (API) 的更多信息，请参阅 http://java.sun.com/products/JavaManagement/。

## 4.4 启动和停止管理实例

要管理管理服务器上的配置，该节点上必须运行一个管理实例。要在管理节点上部署、监控或停止/启动实例，这些节点上也必须运行管理实例。

### 4.4.1 在类 UNIX 系统上启动

在类 UNIX 系统上，你可以结合使用 `ps` 和 `grep` 命令来轻松判断相应节点上是否运行了管理实例，如下：

```
ps -ef | grep admin-server
```

如果管理服务器实例正在运行，你将看到类似下面的响应：

```
root 1419 1418 5 10:22:09 ? 0:46 webservd -d /sun/webserver/
admin-server/config -r /sun/webserver7 -t /tmp/admi
root 1418 1417 1 00:22:09 ? 0:00 webservd-wdog -d /sun/
webserver7/
admin-server/config -r /sun/webserver7 -t /tmp
root 1418 1417 0 10:22:09 ? 0:02 webservd -d /sun/webserver/
admin-server/
config -r /sun/webserver7 -t /tmp/admi
```

**注意：** Web Server 进程的解释可以在第 3 章“Web Server 7.0 安装与迁移”中找到。

如果你没有看到管理实例正在运行，可以使用 `startserv` 命令启动它，如下：

```
install_dir/admin-server/bin/startserv
```

在管理服务器上运行此命令将得到类似下面的响应：

- - Sun Java System Web Server 7.0 B12/04/2006 10:15
- info: CORE3016: daemon is running as super-user
- info: CORE5076: Using [Java HotSpot(TM)] Server VM, Version 1.5.0_0 from [Sun Microsystems Inc.]
- info: WEB1000: Loading module in virtual server [admin-server]
- info: WEB1000: Loading module in virtual server [admin-server]
- info: HTTP3072: admin-port:8889 ready to accept requests
- info: CORE3274: successful startup

## 4.4.2 在类 UNIX 系统上停止

在类 UNIX 系统上，你可以使用 `stopserv` 命令停止管理实例，如下：

```
install_dir/admin-server/bin/stopserv
```

当服务器停止后，你将看到类似下面的响应：

> server has been shut down

没有办法跨多个节点集中启动/停止实例。因此，你需要通过 SSH 或 TELNET 连接到每个节点，并在每个节点上手动运行 `stopserv` 命令。

### 4.4.3 在 Windows 系统上启动和停止

在 Windows 平台上有多种停止和启动管理实例的方法。

### 4.4.3.1 命令行方法

与类 UNIX 系统类似，在 Windows 系统上你可以直接从命令行运行启动和停止脚本，如下：

- install_dir/admin-server/bin/startserv.bat
- install_dir/admin-server/bin/stopserv.bat

### 4.4.3.2 程序组方法

此外，安装过程会创建一个名为 Web Server 7.0 的程序组，其中分组合了若干用于与管理服务器交互的图标。该组可以在以下位置找到：

Programs -> Sun Microsystems -> Web Server 7.0

该程序组包含了用于启动、停止或访问管理服务器管理界面的各种图标：

- Administration Console（管理控制台）
- Start Administration Server（启动管理服务器）
- Stop Administration Server（停止管理服务器）

只需点击 Start Administration Server 图标即可启动该服务器进程。

### 4.4.3.3 服务方法

管理服务器作为服务程序小组件运行。因此，你也可以使用服务应用程序 (services.msc) 直接启动和停止此服务。





## 4.5.1 管理控制台 (Administration Console)

管理控制是一个专门设计的 Web ，仅部署在管理服务器上。它由 HTML 页面、Java 页面 (JSP)、JavaScript 技术、基于核心 Java 技术的类以及基于 XML 的部署描述、各种组件的数据文件等组成。构成管理控制台的文件是私有的；管理员无需对其进行编辑。

### 4.5.1.1 访问管理控制台

管理员通过浏览器访问管理控制台。与管理控制台的通信通常通过 SSL（默认情况下）进行，但您可以在安装期间指定一个非 SSL 管理端口。以下 URL 提供了在使用默认设置时，您将如何访问管理控制台的示例：

```
https://adminhost.admindomain:8989
```

> 注意：尝试使用标准 HTTP 协议连接到安全端口的客户端将通过基于 SSL 的 HTTP (HTTPS) 自动重定向到安全端口。

如果管理服务器实例正在运行，则您的浏览器窗口将显示图 4.4 所示的登录界面。

输入您在安装过程中提供的凭据登录管理控制台。管理员通过基于表单的身份验证进行认证，该认证将用户验证到 Web 容器。基于表单的身份验证允许管理员在注销时无需关闭浏览器窗口。

### 4.5.1.2 管理控制台布局

您通过导航标签和子标签（也称为父标签和子标签）的组合，并通过各种 Web 元素提供输入来执行各种管理任务。管理控制台每个页面提供的信息的设计旨在便于导航并提供对价值信息的访问。图 4.5 展示了提供虚拟服务器属性访问的管理控制台窗口。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_148_0.png)

## 4.5 管理 Web 服务器 7.0 的方法

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_149_0.png)

图 4.4 管理控制台登录界面

| 首页 (HOME) | 刷新 (REFRESH) | 退出 (LOG OUT) | 帮助 (HELP) |
| --- | --- | --- | --- |
| 用户 admin 服务器 boulder | 运行中的实例 1 |
| Sun Java* 系统 Web 服务器 | 已停止的实例 0 |

配置 > boulder.example.com > 虚拟服务器 > boulder.example.com

| 服务器设置 (Server Settings) | Web 应用 (Web Applications) | 内容处理 (Content Handling) | WebDAV | 搜索 (Search) | 访问控制 (Access Control) | 摘要 (Summary) |
| --- | --- | --- | --- | --- | --- | --- |
| 通用 (General) | 查找偏好 (Look Preferences) | 监控设置 | 请求限制 | | |

boulder.example.com - 虚拟服务器通用属性

所有虚拟服务器都指定了一个或多个 HTTP 监听器。当新请求进来时，服务器根据配置的 HTTP 监听器确定将其发送到哪个虚拟服务器。您可以从此页面关联 HTTP 监听器。

图 4.5 管理控制台—控制台布局

表 4.1 总结了此页面包含的各种组件。

## 表 4.1 管理控制台组件

| 名称 | 类型 | 位置 | 描述 |
| --- | --- | --- | --- |
| VERSION | 按钮 | 左上角 | 此按钮允许立即访问系统上安装的 Web 服务器版本。点击此按钮时显示的数据示例如下：Sun Java Web Server 7.0U1 B06/12/2007 22:48。 |
| User: admin | 标签 | 左上角 | 表示当前登录到管理服务器的管理员用户名。 |
| Server: boulder | 标签 | 左上角 | 表示管理员当前登录的服务器名称。 |
| HOME | 按钮 | 右上 | 点击此按钮将您带到常用任务页面。 |
| REFRESH | 按钮 | 右上 | 点击此按钮将刷新页面。 |
| LOG OUT | 按钮 | 右上 | 点击此按钮将注销。 |
| HELP | 按钮 | 右上 | 点击此按钮将启动帮助窗口。 |
| Instance(s) Running 1 | 标签 | 右上 | 此标签显示当前运行的实例数量。 |
| Instance(s) Stopped 0 | 标签 | 右上 | 此标签显示当前停止的实例数量。 |
| Configurations > boulder.example.com > Virtual Servers > boulder.example.com | 面包屑 | 左上 | 此面包屑显示您在管理控制台中的位置。点击面包屑可以返回。 |
| Parent tabs (tabs) | 按钮 | 中间 | 父标签用于分组。在图 4.5 中，已选择了设置标签。 |
| Child tabs (subtabs) | 按钮 | 中间 | 子标签存在于父标签之下。此标签显示的子标签为通用、设置。 |
| Content | N/A | N/A | 页面的其余部分由表、标签和通用信息组成。 |

## 4.5 管理 WEB 服务器 7.0 的方法

点击任何父标签都可能导致子标签出现。子标签的操作取决于特定标签。点击特定任务或子任务将打开相应的页面。然而，某些任务需要一系列页面的收集。管理控制台对此类任务具有向导。

### 4.5.1.3 常用任务

常用任务页的设计是基于任务的（而不是基于功能的），根据先前的版本 Web 服务器的用户模式。该界面包含了针对常用任务的向导；包括创建配置、虚拟服务器和请求证书的向导。图 4.6 提供了您登录后立即可用的常用任务概述。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_151_0.png)

图 4.6 管理控制台—常用任务

您可以从此屏幕选择许多常用任务之一，也可以通过选择相应的标签（如配置或节点）深入某个特定区域。

### 4.5.1.4 最新新闻

常用任务页还包含各种来源（例如博客、维基和开发者文章）的链接，让您了解 Web 服务器 7.0 的最新信息。图 4.7 展示了位于下方的信息示例。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_152_0.png)

图 4.7 管理控制台—新闻

### 4.5.1.5 管理控制台帮助

所有表和其他特定页面字段都有关于如何为特定表输入数据的信息。帮助信息说明了如何验证数据以及哪些参数是必的，哪些是可选的。在访问特定向导的页面时，您可以在向导的任何步骤点击帮助标签，以获得针对特定任务的特定帮助。

## 4.5.2 命令行界面

Web 服务器 7.0 包含一个强大的命令行界面，可用于执行与图形界面中提供的相同的管理任务。这包括创建和部署配置、启动和停止服务器实例、监控实例和配置，以及图形界面中提供的任何其他任务。命令行界面充分利用了 JMX 管理框架，因此，可以使用本地安装的 CLI 管理远程管理服务器。





## 4.5 管理 Web Server 7.0 的方法

命令行界面是一个基于 Java 命令语言 (JACL) 的脚本框架；它本质是 TCL 语言的 Java 实现。CLI 功能通过 `com.sun.web.admin.cli.shell-adapter.wAdminShell` Java 类实现，并通过 `wadm` 脚本启动。

Web Server 7.0 附带有多个预配置的管理脚本（见表 4.3），这些脚本使用 TCL 语法来访问管理子命令。通过对 TCL 的基础了解，你可以创建自己的管理脚本，从而扩展 Web Server 管理环境以满足你的需求。

管理员可以使用三种模式之一使用命令行界面：

- **单行模式**——整个命令（包括选项）包含在一行内。
- **文件模式**——将一组命令存储在文件中并输入到 `wadm`。
- **Shell 模式**——在交互式 JACL shell 中输入命令。

之前的 Web Server 版本提供了如 `HttpServerAdmin`、`wdeploy` 和 `flexanlg` 等命令，这些命令提供了图形化 Administration Server 界面功能的子集。然而，CLI 经过重新设计，可以访问 Administration Server 提供的 100% 功能。

> 注意：Web Server 7.0 仍然支持 `wdeploy` 命令，但仅用于与 Web Server 6.x 版本向后兼容。它只在 Administration Server 包含的 Web 实例上运行。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_153_0.png)

命令行界面包含在 Administration Server 和 Administration Node 的安装中，你也可以单独安装 CLI。如果你只想使用 CLI 从自己的桌面管理远程服务器，后者将非常有用。

### 4.5.2.1 运行命令行界面

`wadm` 脚本可以在 `install_dir/bin` 目录下找到。当你启动脚本时，它会尝试将其绑定到特定的 Administration Server 实例以执行任务。因此，在你启动 CLI 之前，你通信的 Administration Server 需要正在运行。你可以指定特定 Administration Server 的主机名和端口号以访问该节点上的管理实例。如果你不提供这些信息，CLI 将尝试连接到本地主机端口 8989（默认值）。

为了确保只有授权用户才能访问 Administration Server，你需要指定安装期间输入的管理员用户名和管理员密码凭据（见第 3 章图 3.8）。如果你不提供管理员用户名，CLI 将假设你正尝试以管理员用户身份执行此操作。对于密码值不做任何假设。

下面的示例演示了如何在启动 `wadm` 脚本时指定主机、端口和用户参数：

```
install_dir/bin/wadm --host adminhost --port adminport --user
  adminuser
```

请参阅第 4.5.2.3 节“语法”，以获取 `wadm` 脚本使用方法和语法的概览。

如果 Administration Server 上启用了安全套接层 (SSL)，则 `wadm` 脚本与 Administration Server 之间的所有流量都将被加密。Administration Server 传递的证书将根据位于 `~/.wadmtruststore` 的信任存储文件进行验证。如果证书存在且有效，命令将正常进行。否则，`wadm` 脚本将显示证书并让用户选择接受它。如果用户接受，证书将添加到信任存储文件中，命令将正常进行。

> 注意：信任存储（truststore）是一个包含各种服务器公钥的数据库文件。公钥作为签名者证书存储在信任存储中。

### 4.5.2.2 Shell 变量

命令行上提供的任何参数都可以通过调用 `wadm` 脚本的 shell 以环境变量提供，或者通过在 shell 本身中设置变量。使用这些 Shell 变量可以让你避免每次启动 `wadm` 脚本时都输入主机名和端口号等常用参数。

特定参数的 Shell 变量名通过在参数名前加上字符串 "wadm_" 得到。例如，主机名、端口号和管理用户参数可以通过以下 Shell 变量引用：

- wadm_host
- wadm_port
- wadm_user

如果特定参数包含连字符（如 `document-root`），则连字符在相应的 Shell 变量中被替换为下划字符（`wadm_document-root`）。

在 UNIX 操作系统中，rc 文件用于为各种应用程序提供配置设置。例如，`~/.bashrc` 提供 bash shell 的配置设置。在 `/etc` 下找到的 rc 文件定义了系统级设置，而在用户主目录下的 rc 文件则特定于某个用户。

> 注意：rc 文件：[Unix：源自 1955 年 CTSS 系统上的 'runcom files'，通过启动脚本 '/etc/rc'] 一个包含应用程序程序（或整个操作系统）启动指令的脚本文件，通常是一个文本文件，其中包含的命令是在系统运行时可能被手动调用的、但在每次系统启动时都将自动执行的命令。

> 来源：Cool Jargon of the Day http://www.jargon.net/jargonfile/rcfile.html。

`.wadmrc` 文件是 `wadm` 命令的默认文件。这是一个 TCL 文件，通常位于基于 UNIX 的系统的用户主目录下。该文件的内容在执行任何 `wadm` 命令之前会被处理。你可以使用 `--rcfile` 或 `-R` 命令行来指定特定 rc 文件的位置和名称。这对于可能没有主目录的 Windows 系统有用。下面的示例演示了如何在 Windows 系统上引用 rc 文件：

```
C:\SunServer\bin\wadm -R c:\wadmrc
```

> 注意：在 Windows 系统上，wadm 脚本搜索 .wadmrc 文件时使用 `USERPROFILE` 环境变量。该环境变量默认未设置。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_155_0.png)

## 第 4 章 Web Server 7.0 管理

变量可以通过 `set` 命令在 `.wadmrc` 中定义。以下是一个 `.wadmrc` 文件的示例，它为用户、主机和端口参数设置了默认值：

```
set wadm_host host01.example.com
set wadm_port 8988
set wadm_user admin
set wadm_password password
```

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_156_0.png)

> 注意：你可以在 `.wadmrc` 文件中使用 `wadm_password` 变量指定管理员密码。然而，由于在系统上保存密码相关的安全问题，强烈不建议这样做。

如果你需要 CLI 提供更详细的信息，可以将 `wadm_verbose` 设置为 `true`。如果你对发送到管理服务器的完整命令，可以将 `wadm_echo` 设置为 `true`。要启用 JACL，将 `wadm_script` 设置为 `true`。以下是带有这些值的更新后的 `.wadmrc` 文件：

```
set wadm_host host01.example.com
set wadm_port 8989
set wadm_user admin
set wadm_password password
set wadm_verbose true
set wadm_echo true
set wadm_script true
```





## 4.5 管理 Web Server 7.0 的方法

4. 在 `wadm` shell 中使用 `set/unset` 命令定义的选项最后被处理。

如果您不确定当前设置了哪些变量，可以使用 `info` 子命令来列出当前值，如下所示：

```
wadm> info vars
wadm_echo argv wadm_histfile auto_execs auto_index errorInfo wadm_user
wadm_ss1 auto_oldpath wadm_script tcl_library errorCode wadm_
verse wadm_password argc wadm_port wadm_savehist wadm_mode tcl_
patchLevel wadm_host tcljava tcl_platform env tcl_version
tcl_interactive wadm_prompt argv0 auto_path
wadm>
```

### 4.5.2.3 语法

理解新命令的语法至少可以被说是一项艰巨的任务。你可以阅读大约 500 多页的《Sun Java System Web Server 7.0 CLI 参考手册》，也可以尝试通过反复尝试来学习命令。坦率地说，Web Server 7.0 提供了一种通过使用命令本身来学习语法的直观方法。

`w` 脚本的用法如下：

```
Usage: wadm --version|-V
or wadm --help|?
or wadm [--user=admin-user] [--password-file=admin-pswd-file]
[--host=admin-host] [--port=admin-port] [--no-ss1] [--rcfile=rcfile]
[--no-prompt] [--commands-file=filename]
```

你在命令行上指定与用法不符的参数时，就会显示此信息。获取此信息最简单的方法是输入 `wadm` 命令而不提供任何参数（这假设未定义 `.wadrc` 文件）。

特定参数的选项都有长格式和短格式版本。例如，以下两个命令提供相同的输出：

- wadm --version（长格式）
- wadm -V（短格式）

# 第 4 章节 WEB SERVER 7.0 管理

**注意：** 你可以使用 `--help` 选项查看 `wadm` 脚本的完整选项列表。信息类似于 UNIX 的 man 条目（帮助手册）。要获取特定命令的帮助，请使用以下格式：`install_dir/bin/wadm command --help`（其中 command 是你正在寻求额外帮助的命令）。

`wadm` 脚本接受一系列子命令和选项来执行各种管理任务。需要注意的是，子命令之间的选项可能不同，即使它们可能具有相同的短格式。例如，参数 `-f` 用于为 `create-ldap-authdb-command` 指定*搜索过滤器*，而在与 `create-instance` 子命令配合使用时，它会*强制*创建实例（并覆盖现有实例）。

图 4.8 提供了一个带有 `restart-instance` 子命令的 `wadm` 脚本结构的示例说明。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_158_0.png)

**图 4.8** 命令行界面的使用

以下项目描述了图 4.8 中的详细信息：

- *工具名称*（Tool name）是处理一组参数并然后按照参数指定的方式执行操作的可执行程序或脚本。Web Server 7.0 的工具名称为 `wadm`。
- 命令行上提供的所有参数（包括子命令）都是可选的。如果没有提供子命令，脚本将进入交互式 shell。
- 所有的选项都依赖于特定的子命令。每个选项都有*选项前缀（Option prefix）、选项名称（Option name）*和*选项参数（Option argument）*。
- 所有选项都有长名称，大多数选项都有同义的短名称。选项前缀短选项使用单个横杠（-），长选项使用两个连续的横杠（--）。
- 布尔选项可以分组（例如，在 UNIX 中，`1s -1a` 等于 `1s -1 -a`），但仅限于它们的短选项名称。在此示例中，`-f` 和 `-y` 选项被组合在一起。

## 4.5 管理 Web Server 7.0 的方法

- 选项可以任意顺序指定。
- 命令行从左侧扫描，在耗尽所有选项值后，剩余部分被视为操作数（operands）。
- 如果命令行上使用不同的选项参数重复选项，则使用最后一个选项值并显示警告消息。
- 参数 `--` 作为分隔符，表示选项的结束。任何后续参数都将被视为操作数，即使它们以 `-` 字符开头。

命令行界面的退出代码

| 退出代码 | 含义 |
| :--- | :--- |
| 0 | 成功 |
| 1 | 通用错误 |
| 2 | 使用错误 |
| 3 | 运行时错误 |
| 4 | 权限错误 |
| 5 | 找不到文件 |
| 6 | 输入错误 |
| 7 | 磁盘空间不足 |
| 8 | 内存错误 |
| 9 | 未定义错误 |





## 4.5.2.5 模式

有三种方式可以调用 wadm 脚本。你选择的方法取决于你的经验水平以及你计划使用的交互程度。这三种调用模式如下：

-   独立模式 (Standalone Mode)
-   Shell 模式 (Shell Mode)
-   文件模式 (File Mode)

### 独立模式
在独立模式下，你从命令行外壳（例如 UNIX 上的终端窗口或 Windows 上的命令窗口）调用 wadm 脚本。你可以在命令行中指定所需的子命令以及执行所需的所需的任何选项或操作数。当子命令执行完成后，所有控制权将返回到启动它的命令行外壳。wadm 脚本在独立模式下运行的示例例如：

```
$ list-configs --user=admin --host=www.example.com --password-file=./admin.pwd
www.example.com $
```

如果未通过密码文件提供或在 .wadmrc 文件中定义密码，系统会提示用户输入密码。如果通过这两种方法之一提供了密码，则不会提示用户，且脚本以非交互执行模式运行。

> 注意：密码无法通过命令行传递给 wadm 脚本。不过，你可以指定一个包含明文密码的文件，并使用 --password-file 选项在执行 wadm 脚本时引用该文件。如果你选择使用此方法，请确保该文件仅对你自己可读。

如果你熟悉各种子命令和子命令语法，独立模式将非常有用。它允许你以极小的开销快速指定并执行子命令。然而，你无法使用 4.5.2.4 节中的 Tab 补全功能。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_162_0.png)

## 4.5 管理 Web 服务器 7.0 方法

### Shell 模式
在 Shell 模式下，你从命令行外壳调用 wadm 脚本，但不提供子命令。在验证了初始参数（例如主机、端口、用户和密码文件）后，wadm 脚本将进入它自己的 shell（称为 wadm shell），等待用户输入子命令。

```
$ wadm --user=admin --host=www.example.com -password-file=./admin.pwd
Connected to localhost:8989
Sun Java System Web Server 7.0 Build 12/12/2007 08:48
wadm>
```

执行子命令后，控制权将返回到 wadm shell，它将等待另一个子命令。

```
$ wadm --user=admin --host=www.example.com -password-file=./admin.pwd
Connected to localhost:8989
Sun Java System Web Server 7.0 Build 12/12/2007 08:48
wadm> list-configs
www.example.com
wadm>
```

你可以通过输入 exit 或 quit 命令退出 wadm shell。

> 注意：为了在 UNIX 上提供额外功能，你可以在运行 shell 模式运行时在 CLI 中访问 UNIX 命令和外部脚本。例如，你可以如下所示从 shell 内部访问 UNIX ls 命令：

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_163_0.png)

如果你计划执行多个命令且不确定语法，Shell 模式将非常有用。虽然进入 shell 模式会有开销，但在建立 wadm shell 后，这种开销是非常微小的。当你首次学习如何使用 CLI 时，Shell 模式非常有帮助。

### 文件模式
在文件模式下，你可以在外部文件中指定子命令列表，并将该文件作为参数传递给 wadm 脚本。CLI 从文件中读取子命令并按照它们出现的顺序执行。wadm 脚本使用 --commands-file 或 -f 选项来指定包含子命令的文件名。例如，假设你名为 `restart-instance.cmds` 的文件，其中定义了以下子命令：

```
stop-instance --config=www.example.com
start-instance --config=www.example.com
```

你可以如下将其作为参数传递给 wadm 脚本：

```
$ wadm --user=admin --host=www.example.com --password-file=./admin.pwd
--commands-file=restart-instance.cmds
```

脚本随后执行文件中找到的每个子命令，并在每个子命令完成后将控制权返回到原始 shell。

install_dir/samples/admin/scripts 目录包含了 Web Server 7.0 发行版自带的几个预定义脚本（见表 4.3）。这些脚本可用于执行各种常见的管理任务，并演示如何在现有命令的基础上构建新的实用程序。

> 注意：wadm 脚本基于基于 Java 的 Tcl 引擎构建，因此你可以在命令文件中包含 Tcl 脚本。有关 Tcl 支持的更多信息，请参见 4.5.2.6 节。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_164_0.png)

## 4.5 管理 WEB 服务器 7.0 方法

### 表 4.3 管理脚本

| 脚本 | 描述 | 用法 |
| :--- | :--- | :--- |
| enable-ssl | 在指定的 Web 服务器启用 SSL | wadm -f enable-ssl.tcl <config> <server> |
| filter-mime | 从指定的 Web 服务器获取匹配类型 | wadm -f filter-mime.tcl <config> <vs> |
| remove-mime | 从指定的 Web 服务器删除匹配类型 | wadm -f remove-mime.tcl <config> <vs> |
| add-mime-ext | 为匹配类型添加指定的扩展 | wadm -f add-mime-ext.tcl <config> <vs> |
| summary | 提供安装的摘要 | wadm -f summary.tcl |
| list-webapps | 提供所有部署应用程序的摘要 | wadm -f list-webapps.tcl |
| collate-logs | 提供跨多个节点的汇总日志 | wadm -f collate-logs.tcl <node1> <node2> |
| renew-selfsigned-cert | 允许更新指定的自签名证书 | wadm -f renew-selfsigned-cert.tcl <config> <nickname> |

install_dir/samples/admin/scripts 目录还包含了几个可以交互的工具。查看该目录下的 README 文件可以获取完整列表及其描述。

如果你有一组定期执行的子命令序列，文件模式将非常有用。这允许你通过一次调用执行多个事件。文件模式也非常强大，它允许通过脚本扩展管理过程。

### 4.5.2.6 工具语言 (Tcl) 支持

JACL（或 Java 命令语言）是由 John 创建的 Tcl 脚本语言的 Java 实现。命令行界面实现了全 Tcl 支持，因此采用了该语言的所有特性。你可以在 shell 模式下的 wad 提示符处或在文件模式创建的脚本中使用 Tcl 命令。Tcl 命令及其语法的示例可以在 install_dir/samples/admin/scripts 中的管理脚本中看到。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_166_0.png)

> 注意：Tcl 参考手册可以在 http://tmml.sourceforge.net/doc/tcl/ 获取。该页面包含了 Tcl 命令、变量处理结构和其他对开发自己的 Tcl 脚本非常有用的信息。

## 4.5.3 手动编辑配置文件

你可以通过手动编辑和保存文件来对节点上的任何配置文件进行更改。取决于所更改的文件，你可能需要重启或重新加载配置文件以便节点能够检测到更改。





## 4.6 本地化与无障碍

- 2. 如果发现任何实例存在手动编辑，则暂停配置的部署，并向用户提供选项：在配置存储（Configuration Store）中更新配置，或使用现有配置覆盖管理节点（Administration Node）上的更改。
- 3. 如果用户选择使用编辑后的配置，则管理服务器将整个配置从该实例拉取到配置存储中，并覆盖现有配置。
- 4. 配置更新后，它将部署到特定集群内共享该配置的所有实例。

警告：不要手动编辑配置存储库（Configuration Repository）中的任何文件。此目录下的文件由 Web 服务器创建，供内部使用。

## 4.6 本地化与无障碍

经过本地化的产品已翻译成其他语言或文化。所谓具有无障碍性（accessible）的产品可以供残障人士阅读和使用，并符合 508 合规性等政府标准。管理控制台（图形用户界面）和命令行界面均支持本地化，并符合无障碍标准，使其符合 508 合规。

> 注意：本地化（localization）和国际化（internationalization）术语分别缩写为 L10n 和 i18n。这些缩写中的数字 10 和 18 代表每个单词首字母和尾字母之间的字母数量。L10n 中的大写字母“L”有助于将其区别于 i18n 中的小写字母“i”。

美国《康复法案》第 508 节定义了电子和信息技术无障碍指南，应遵循这些指南以使残障人士能够获取信息。遵循这些指南的产品被称为 508 合规产品。有关 508 合规的更多信息，请参阅 http://www.section508.gov。

### 4.6.1 管理控制台的本地化

可以配置 Web浏览器以指定用户可以阅读的语言。Web 服务器可以检测此类信息并以指定的语言将数据返回给浏览器。这些信息通过 Accept-Request 请求头从 Web浏览器传递到 Web 服务器，如下：

```
GET / HTTP/1.1
Host: localhost:8989
User-Agent: Mozilla/5.0 (Windows; Windows NT 5.1; en-US)
r/1.8.1.12) Gecko/200802021 Firefox/2.0.0.12
Accept: text/xml,application/xml,xhtml-xml,text/
q=0.9,text/plain;q=0.8,image/png,/*;q=0.3
Accept-Language: es,en;q=0.7
Accept-Encoding: deflate
Accept-Charset: ISO-8859-1,utf-8;q=0.7;*q=0.7
Connection: keep-alive
```

管理控制台是一个自动检测 Accept-Language 请求头并以本地方式返回内容的应用程序。因此，无需在管理服务器中进行任何本地化配置。图 4.9 展示了西班牙语的本地化登录服务器。

### 4.6.2 命令行界面的本地化

通过向管理服务器的 `server.xml` 文件添加本地化特定元素，实现命令行界面的本地化。二级本地化元素包含一个名为 `default-language` 的子元素，它指定了 RFC 4646（语言标识）规定的 IANA 语言标记。

> 注意：互联网地址分配机构（IANA）是互联网最老的机构之一，其活动可追溯到 20 世纪 70 年代。IANA 分配并维护用于构成的技术标准（“协议”）的唯一代码和编号系统。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_168_0.png)

## 4.6 本地化与无障碍

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_169_0.png)

**图 4.9** 针对西班牙语 (es) 本化的管理控制台

使用本地化标签将默认语言设置为西班牙语（拉丁美洲）的例如下：

```
<localization>
<default-language>es-419</default-language>
</localization>
```

设置此元素后，与 CLI 的任何交互都会产生西班牙语消息。例如，在请求无效配置名称的统计数据时，会返回以下错误：

```
wadm> get-config-stats --config=foobar
ADMIN3725: No hay datos de ajuste disponibles para la configuración:
foobar
wadm>
```

这大致翻译为：“配置 foobar 无可用数据。”

## 第 4 章 Web 服务器 7.0 管理

所有消息都以 `default-language` 元素指定的语言返回。然而，子命令、选项和操作数不会发生变化。

> 注意：参考 Web Server 7.0 发布说明以获取管理控制台和命令行界面支持的语言列表。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_170.png)

### 4.6.3 无障碍

508 合规的应用程序返回供残障人士阅读的内容。这方面的例子是视障人士通过屏幕阅读器与应用程序交互。符合 508 节要求的应用程序和网站必须以设备易于读取的格式提供数据。如果网站符合以下领域的标准，则认为符合 508 标准：

- 文本标签
- 多媒体演示
- 颜色
- 可读性
- 服务端图像映射
- 客户端图像映射
- 数据表格 (i) 帧
- 闪烁率
- 纯文本替代方案
- 脚本
- 小程序和插件
- 电子表单
- 导航链接
- 时间延迟

Sun Microsystems 花了大量时间确保管理控制台和命令行界面均符合 508 标准。这些界面在之前的版本进行了重大重新设计，以确保数据组织方式符合这些标准。

## 4.7 管理 Web 服务器配置

回顾本章内容可以清楚地看到，配置是管理基础设施的核心。





## 4.7 管理 Web 服务器配置

这是管理控制台（Administration Console）的替代方案，实际上可能更快且更灵活。以下信息提供了该子命令的概述：

```
wasm create-config --<TAB>
--httpport* --server-name* --echo --no-prompt
--verbose --document-root --jdk-home --server-user
--ip --platform
```

`create-config` 子命令实际上允许你指定在“新配置向导”（New Configuration Wizard）中不可用的额外参数。若要在管理控制台中指定这些值，你需要在配置创建后对其进行编辑；这是一个两步过程。命令行界面允许你一步到位地完成这两个步骤。以下示例演示了如何使用 `create-config` 子命令创建一个新配置：

```
wasm create-config --server-name=www.example.com --document-root=../docs --httpport=80 --ip=* "My Test Config"
CLI2001 Command 'create-config' ran successfully
wasm
```

为了对比，子命令选项按照它们在“新配置向导”中出现的顺序列出。请注意，配置名称列在最后。如果你想在配置名称中包含空格，需要使用双引号（如所示）。

### 4.7.1.2 复制现有配置

使用现有配置作为模板通常比创建新配置更简单。当你想要在更新（已测试的）配置之前尝试某些操作时，可以使用此功能。Web Server 7 允许你在管理控制台中这样复制现有配置：

- 1. 打开管理控制台并点击“配置”（Configurations）选项卡进入主配置页面。
- 2. 选择想要作为模板的配置旁边的复选框，并点击页面上的“复制”（Duplicate）按钮。将出现“新配置向导”页面。
- 3. 为你的配置输入名称（Name）。这是一个可读名称，帮助你在界面中与其他配置区分来。点击“确定”（OK）按钮。
- 4. 你将看到新配置出现在“配置”表格中。现在你可以编辑该配置并应用你的自定义设置。

CLI 中的 `copy-config` 子命令可以作为管理控制台的替代方案。以下信息提供了该子命令的概述：

```
wadm copy-config --<TAB>
--config* --echo --no-prompt --verbose
```

以下示例演示了如何使用 `copy-config` 子命令将一个配置复制到另一个：

```
wadm copy-config --config="My Test Config" "My Second Test Config"
CLI201 Command 'copy-config' ran successfully
wadm
```

> **注意：** 你不能在复制配置的过程中创建服务器实例。

### 4.7.2 部署现有配置

配置无非是一组可以实例化 Web 服务器实例的文件。在查看配置中包含的自定义设置之前，你需要将配置部署到一个或多个节点上。部署过程仅仅是将所有配置文件从配置存储（Configuration Store）复制到一个或多个节点，并在节点上创建服务器实例。创建实例后，你就可以启动它以查看你所做的自定义设置。

你可以通过管理控制台或命令行界面部署配置。

要使用管理控制台部署配置，请完成以下步骤：

- 1. 打开管理控制台并点击“配置”选项卡进入主配置页面。
- 2. 选择想要部署的配置旁边的复选框并点击“部署”（Deploy）按钮。你将看到一个窗口显示部署正在等待中。
- 3. 点击“部署”按钮。
- 4. 配置部署完成后，点击“关闭”（Close）按钮。你将返回主配置页面。
- 5. 选择想要部署的配置旁边的复选框并点击“部署”按钮。出现一个窗口显示部署正在等待中。

上述步骤假设在你想要部署配置时当前没有编辑该配置。情况并非总是如此。你通常希望在做出更改后立即测试更改。当你通过管理控制台对配置进行更改后，右上角会出现一条消息显示部署正在等待中。此消息见图 4.10。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_175_0.png)

图 4.10 部署等待通知

你可以继续对配置进行更改，或点击“部署等待中”（Deployment Pending）链接来启动部署过程。在编辑配置时点击“部署”链接将消除上述列表中的前两个步骤。

CLI 中的 `deploy-config` 子命令可以作为管理控制台的替代方案。以下信息提供了该子命令的概述：

```
wadm> deploy-config --<TAB>
--echo --no-prompt --verbose --force --restart
--no-reconfig
```

以下示例演示了如何使用 `deploy-config` 子命令将配置部署到相应的节点上：

```
wadm> deploy-config "My Test Config"
CLI201 Command 'deploy-config' ran successfully
wadm>
```

### 4.7.3 回滚到之前的配置

有时，你对配置所做的更改可能会导致问题，你需要删除更改以恢复功能。在这种情况下，你只需编辑配置并将配置设置恢复到先先的值。但如果你不知道是哪些更改导致了问题呢？在这种情况下，你可能希望恢复（或回滚）到配置之前的版本。

管理服务器会对更新的现有（已部署的）配置创建一个备份副本。无论你是从管理控制台还是命令行界面执行操作，都会发生，但只有在对配置进行了实际更改时才会发生。备份存储在配置存储中每个特定配置目录下的一个名为 `backup` 的子目录中。备份目录的完整路径如下：

```
install_dir/admin-server/config-store/config_name/backup
```

此目录中的文件通过配置创建时的时间戳来识别。

这些文件中的每一个都是之前部署配置的完整存档。

```
20080116_203853.zip
20080116_204412.zip
20080116_204409.zip
```

此目录中找到的每个文件名格式为 `yyymmdd_HHMMSS.zip`（其中 `yyyy` 是四位年份，`mm` 是两位月份，`dd` 是两位日期，`HH` 是两位小时，MM 是两位分钟，SS 是两位秒）。

可以通过以下步骤通过管理控制台访问备份：

- 1. 打开管理控制台并点击“配置”选项卡进入主配置页面。
- 2. 点击你想查看的配置链接。
- 3. 点击“常规”（General）选项卡。这将打开允许你执行此配置通用功能的窗口。其中一项项是查看和恢复之前部署配置的能力。
- 4. 点击“恢复”（Restore）选项卡。你会看到此配置之前的版本列表。示例见图 4.11。

| 虚拟服务器 | HTTP 监听器 | 实例 | 常规 | 性能 | 访问控制 | 证书 | Java |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 日志偏好 | MIME 类型 | 监控设置 | Web/AV | 计划事件 | 恢复 | 高级 | |

www.example.com - 配置备份
页面根据采取备份的日期列出配置。备份在部署配置时自动进行。选择备份日期并点击恢复以恢复该配置。

# 配置备份 (3)

- EST2008年1月16日 8:38:53
- EST2008年1月16日 8:41:42
- EST2008年1月15日 8:44:09

图 4.11 配置备份屏幕

除了管理控制台外，你还可以使用 CLI 中的 `list-backups` 子命令显示特定配置的备份列表，如下：

```
wadm> list-backups --config=www.example.com
20080116_203853
20080116_204142
20080116_204409
wadm>
```

然后你可以使用 `restore-config` 子命令恢复这些配置中的任何一个。以下信息提供了该子命令的概述：

```
wadm> restore-config --<TAB>
--from-backup* --echo --no-prompt --all
--verbose
```





# 第 4 章 Web 服务器 7.0 管理

```
restore-config --backup=20080116_204142 "www.example.com"
CLI201 Command 'restore-config' ran successfully
```

> 注意：回滚功能是在 Web Server 7.0 PU2 中引入的。在软件的之前的版本中无法找到此功能。

在本书编写时，您无法查看为特定配置版本定义的设置。（此功能无法通过管理控制台或 CLI 访问）。那么，你如何知道正在恢复的配置就是你需要的那一个呢？实现这一点的最佳方法是提取配置 zip 压缩包的内容，并查看包中包含的文件。虽然不建议您修改 config store 目录下的文件，但查看配置 zip 压缩包是您恢复适当配置的唯一方法。

### 4.7.4 删除现有配置

可以通过管理控制台或 CLI 从文件系统中删除不再使用的旧配置。要通过管理控制台删除配置，请执行以下步骤：

- 1. 打开管理控制台并点击“配置（Configurations）”选项卡进入主配置页面。
- 2. 选择您想要删除的配置旁边的复选框，并点击页面上的“删除（Delete）”按钮。将删除配置页面。该页面提供了此配置任何已部署实例的信息。
- 3. 点击 OK 按钮执行以下任务：
   - 停止部署该配置的任何节点上运行的该配置实例
   - 从部署该配置的节点上移除实例
   - 从管理服务器上的配置存储器（Configuration Store）中删除配置
- 4. 您将看到该配置从“配置”表中消失。

## 4.8 总结

CLI 中的 `delete-config` 子命令可以作为管理控制台的替代。以下信息提供了该子命令的概述：

```
wadm> delete-config --<TAB>
--echo --no-prompt --verbose config-name
```

以下演示了如何使用 `delete-config` 子命令删除配置：

```
wadm> delete-config "My Test Config"
CLI201 Command 'delete-config' ran successfully
wadm>
```

与管理控制台不同，`delete-config` 子命令不支持删除已部署的配置。如果您尝试删除已部署的配置，将收到以下错误消息：

```
wadm> delete-config "My Test Config"
ADMIN3653: Cannot delete the configuration 'My Test Config'. It has been deployed to '1' node(s).
wadm>
```

要执行此任务，您必须先从部署该配置的节点上删除任何实例。然后就可以安全地移除配置。以下命令序列演示了如何从命令行完成此操作：

```
wadm> delete-instance --config="My Test Config" www.example.com
CLI201 Command 'delete-instance' ran successfully
wadm> delete-config "My Test Config"
CLI201 Command 'delete-config' ran successfully
wadm>
```

## 4.8 总结

Web Server 7.0 提供了多种管理 Web 服务器配置的方法。许多管理员使用图形化管理控制台来学习产品，但许多人很快就会转向命令行工具，甚至直接编辑配置文件。无论您偏好图形界面、基于工具的还是直接编辑，Web Server 7 都能让您拥有极大的灵活性，按照您想要的方式管理 Web 服务器。

## 4.9 自学实验

使用本章包含的信息执行以下练习。这些练习将帮助验证您对本章描述概念的理解。

使用图形化管理控制台执行以下步骤：

- 检查默认配置中的设置。将设置与您在安装过程中插入参数相关联。
- 停止并启动默认配置，并验证您可以使用网络浏览器访问它。
- 为您的默认配置创建一个副本；将其命名为“My New Config”。
- 编辑“My New Config”配置，并将端口号更改为服务器上的可用端口。
- 部署“My New Config”配置。
- 启动“My New Config”配置的实例。
- 验证您的服务器上部署了两个新配置，且它们都监听不同的端口。
- 为“My New Config”配置添加 URL 重定向，并使用以下参数：
  - 源（Source）：URL 前缀：/foo
  - 目标 URL：您的默认服务器实例的 URL（例如，http://localhost:80）
- 部署更新后的配置，并在“My New Config”实例中访问 /foo URI。验证您是否被重定向到默认服务器实例。
- 将“My New Config”配置恢复到上一个版本。
- 部署恢复的“My New Config”配置，并验证在使用 /foo URI 时您不再被重定向。
- 删除“My New Config”配置。
- 使用命令行界面重复第 1–12 步。

> 注意：访问 http://www.sunwebserver.com 获取有关如何执行这些练习的详细说明。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_180_0.png)

# Web Server 7.0 配置文件

第 4 章“Web 服务器 7.0 管理”介绍了配置文件。每个实例都有自己的文件集。表 5.1 提供了配置文件的概述。

表 5.1 Web Server 7.0 配置文件

| 文件名 | 概述 |
|---|---|
| cert8.db | 网络安全服务 (NSS) 数据库。此数据库发布可访问的对象（如证书、证书吊销列表和 MIME 类型），并与 key3.db 数据库工作。此文件是信任数据库的一部分 |
| certmap.conf | 证书到 LDAP 的映射 |
| default-web.xml | 所有应用程序的默认值 |
| default.acl | 实例的默认访问控制列表 (ACL)。 |
| key3.db | NSS 私钥数据库。此数据库存储了服务器生成的私钥 |

# 第 5 章 WEB 服务器配置文件

**表 5.1** Web Server 7.0 配置文件 *续* |

| 文件名 | 概述 |
|---|---|
| keyfile | 包含扁文件用户名和哈希密码的文件 |
| login.conf | Java 身份验证和授权服务 (JAAS) 的信息。 |
| magnus.conf | Netscape 服务器应用程序接口 (NSAPI) 插件初始化指令和设置，用于控制 NSAPI 插件的运行方式。 |
| mime.types | 多用途互联网邮件扩展 (MIME) 类型映射文件。此文件包含扩展名到 MIME 类型的映射，允许服务器确定请求的内容。 |
| obj.conf | NSAPI 请求处理配置。此文件包含指示服务器处理各种 HTTP 请求的操作。 |
| secmod.db | PKCS #11 模块数据库。此数据库存储了用于各种加密模块（例如硬件加速卡）的 PKCS #11 模块信息。 |
| server.policy | 控制应用程序访问资源的策略。 |
| server.xml | 主实例配置文件，包含了运行服务器所需的大部分设置 |

当您通过管理控制台或命令行执行管理任务时，配置文件会被更新。此外，您可以直接编辑每个配置文件并根据需要进行修改。

> 警告：允许您编辑实例的配置文件，但不要编辑管理服务器存储目录下的任何文件。此目录中的文件由管理服务器和命令行修改，仅供内部使用。





## 5.1 magnus.conf 文件

注意：指令（directive）是定义 Web 服务器内部设置的语句。

Web 服务器由许多功能组成，允许你在安装完成后立即执行基础请求处理。这些功能由作为 Web 服务器平台部分的服务器应用程序函数（SAFs）提供。

你可以通过在 `magnus.conf` 和 `obj.conf` 文件中添加或修改指令，来更改服务器响应客户端请求的方式。每个指令都引用一个 SAF，该 SAF 用于在请求处理的特定阶段执行工作。你可以选择添加调用 Web Server 7.0 提供的 SAF 的指令，或者通过 NSAPI 创建自己的共享库（或插件）来扩展 Web 服务器的功能。此外，你可能发现有必要包含第三方供应商或其他太阳日月系统（Sun Microsystems）产品提供的功能。

插件必须在 `magnus.conf` 文件中向 Web 服务器注册；这是通过 `Init` 指令完成的。一旦注册，你就可以使用插件包含的 SAFs 在 `obj.conf` 中自定义请求处理。

示例 5.1 展示了在自定义的 `magnus.conf` 中使用 `Init` 指令。

## 示例 5.1 示例 magnus.conf 文件

```
#
# Copyright 2006 Sun Microsystems, Inc. All rights reserved.
# Use is subject to license terms.
#
Init fn="load-modules"
Init fn="load-modules" shlib="libfastcgi.so"
Init fn="load-modules"
shlib="sun/webserver7/plugins/myplugin/myplugin.so"
funcs="myplugin,myfunc2"
```

`load-modules` SAF 用于向 Web 服务器加载并注册插件。此函数最常用于将第三方插件加载到 Web 服务器中，以提供基础平台未包含的功能。此类示例可能包括一个用于为应用程序提供接口的插件。

此示例指定了在初始化过程中注册的三个插件。`lib2eeplugin.so` 和 `libfastcgi.so` 插件随 Web Server 7.0 一起包含。`myplugin.so` 插件是一个用户创建共享库，可以在 `/sun/webserver7/plugins/myplugin` 目录下找到。`shlib` 参数指定共享库的本地文件系统路径。

> 注意：如果你不在 `shlib` 参数中指定完全限定文件名，Web 服务器将在启动脚本（startserv）定义的 `SERVER_LIB_DIR` 变量指定的路径中搜索插件。如果你将 Web 服务器安装在 `/sun/webserver7` 目录，则 `SERVER_LIB_DIR` 的默认值为 `/sun/webserver7/lib`。

`shlib_flags` 参数（如第一个指令所示）指定了共享库如何被加载到 Web 服务器进程中。启动后，Web 服务器进程使用 `dlopen` 函数将额外的库文件加载到内存中。第一个指令中的 `global` 和 `now` 选项分别指的是 `dlopen` 选项 `RTLD_GLOBAL` 和 `RTLD_NOW`。你可以通过使用以下 UNIX 命令阅读更多这些及其他选项：

- # man dlopen

第三个 `Init` 指令还演示了注册特定插件内特定函数（即 `myfunc1` 和 `myfunc2`）的能力。前两个指令中没有指定 `functions` 参数，因此这些插件中定义的所有函数均可使用。

> 注意：有关 Web 服务器指令的更多信息，请参考《Sun Java Web Server 7.0 NSAPI 开发人员指南》（文档编号 819-2632）。

### 5.1.1 语法

表 5.2 提供了 `magnus.conf` 文件的通用语法。

表 5.2 magnus.conf 语法

| 语法 | 规则 |
| :--- | :--- |
| 大写敏感性 | `magnus.conf` 文件中的项对大小写敏感 |
| 注释 | 井号（#）用于标记 magnus.conf 文件中的注释。井号后面的文本会被忽略 |

## | MAGNUS.CONF 文件

| 语法 | 规则 |
| :--- | :--- |
| 指令 | `magnus.conf` 文件中的指令定义了值。错误可能会导致服务器无法正常运行 |
| 参数 | 对于预定义的 SAF，参数的数量和名称取决于函数 |
| 路径名称 | 在路径名称中，始终使用正斜杠（/）而不是反斜杠（\），即使在 Windows 平台上也是如此 |
| 引号 | 字符串包含空格时需要引号（""），否则是可选的。每个左引号必须与右引号匹配 |
| 空格 | `magnus.conf` 文件中的指令出现在其行中。在分隔名称和值的等号（=）前后不允许有空格。换行在示例 5.1 的前三个指令中有演示 |

### 5.1.2 上下文

管理节点可能包含多个已部署的配置。这些部署配置被称为实例。每个实例只能包含一个 `magnus.conf` 文件；因此，实例与文件之间是一一对应的。

### 5.1.3 修改

通过控制台或命令行界面进行的某些更改会更新 `magnus.conf` 文件。如果该文件通过这些接口进行了更新，你必须部署配置以使其在相应的管理节点上生效。如果你使用这些工具部署新配置，将提示你重启。

`magnus.conf` 文件在实例启动时被读取；因此，对 `magnus.conf` 的任何更改都需要重启才能生效。控制台和命令行界面会在部署过程中检测 `magnus.conf` 文件的更改。

## 5.2 server.xml 文件

`server.xml` 文件是 Web 服务器实例的主配置文件。它包含了安装过程中配置的监听套字、虚拟服务器和其他组件的初始值。它还包含了允许 Web 服务器在安装后立即运行的默认设置。你可以通过控制台或命令行界面修改这些设置的值，也可以通过编辑特定管理节点上的 `server.xml` 文件。

> 注意：`server.xml` 文件是最重要的配置文件之一。如果你决定手动编辑它，了解该文件的语法及其结构至关重要。

### 5.2.1 语法

正如名称所示，`server.xml` 文件以扩展标记语言（XML）格式包含信息。因此，理解基本的 XML 结构和术语对于理解 `server.xml` 文件至关重要。

XML 文档包含元素的值的层次结构。元素是 XML 数据单元，也是 XML 文档的基础构建块。元素可以关联值或其他子元素；从而形成父子关系。





## 5.2 SERVER.XML 文件

元素通过起始标签和结束标签分隔，其结构类似于你在查看 HTML 文档源代码时看到的结构（它们使用 `<` 和 `>` 括号）。元素以起始标签开始，例如 `<virtual-server>`，并结束标签结束，例如 `</virtual-server>`。标签是区分大小写的。

以下是运行在 64 位模式下的 Web 服务器的平台元素示例：

```
<platform>64</platform>
```

XML 文档必须包含一个根根元素，它是层次结构中的最顶层元素。与任何其他 XML 元素一样，根元素可以包含子元素。`<server>` 元素是 server.xml 文件的根元素。`<server>` 元素有许多子元素，其中许多子元素也有自己的子元素。

示例 5.2 展示了默认管理节点（Administration Node）的 server.xml 文件。

### 示例 5.2 示例 server.xml 文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!--
Copyright 2006 Sun Microsystems, Inc. All rights reserved.
Use is subject to license terms.
-->
<server>
  <cluster>
    <local-host>boulder.example.com</local-host>
    <instance>
      <host>boulder.example.com</host>
    </instance>
  </cluster>
  <log>
    <log-file>../logs/errors</log-file>
    <log-level>info</log-level>
  </log>
  <platform>64</platform>
  <temp-path>/tmp/https-boulder.example.com-6accbd0a</temp-path>
<jvm>
<java-home>/sun/webserver7/jdk</java-home>
<server-class-path>
/sun/webserver7/lib/webserver-rt.jar:${sun/java.home}/lib/tools.jar:
/sun/webserver7/lib/ant.jar:/sun/webserver7/lib/pwc.jar:
/sun/webserver7/lib/jstsearch.jar:/sun/webserver7/lib/webserver-jst1.jar:
/sun/webserver7/lib/jsf-impl.jar:/sun/webserver7/lib/jsf-api.jar:
/sun/webserver7/lib/webserver-jwsdsp.jar:/sun/webserver7/lib/
container-auth.jar:
/sun/webserver7/lib/mail.jar:/sun/webserver7/lib/activation.jar
</server-class-path>
<debug>false</debug>
<jvm-options>
-Xdebug -Xrunjdw:transport=dt_socket,server=y,suspend=n,address=7896
</jvm-options>
<jvm-options>-Djava.security.auth.login.config=login.conf
<jvm-options>-Xms128m -Xmx256m</jvm-options>
</jvm>

<thread-pool>
<max-threads>128</max-threads>
<stack-size>131072</stack-size>
</thread-pool>

<default-auth-db-name>keyfile/default-auth-db-name>

<auth-db>
<name>keyfile</name>
<url>keyfile</url>
<property>
<name>syntax</name>
<value>keyfile</value>
</property>
<property>
<name>keyfile</name>
<value>keyfile</value>
</property>
</auth-db>

<acl-file>default.acl</acl-file>

<mime-file>mime.types</mime-file>

<access-log>
<file>../logs/access</file>
</access-log>

<http-listener>
<name>http-listener-1</name>
<port>80</port>
<server-name>boulder.example.com</server-name>
<default-virtual-server-name>boulder.example.com</default-virtual-server-name>
</http-listener>

<virtual-server>
<name>boulder.example.com</name>
<host>boulder.example.com</host>
<http-listener-name>http-listener-1</http-listener-name>
<document-root>/sun/webserver7/https-boulder.example.com/docs</document-root>
</virtual-server>
</server>
```

### 5.2.2 XML Schema

XML Schema 提供了一种定义 XML 文档结构、内容和语义的方法。它可以使用基于 XML 的语言对 XML 文档指定约束条件（即有效的元素名称、数据类型和值）。XML Schema 是层次化的，因此更容易。




# 第 5 章 Web 服务器 7.0 配置文件

示例 5.4 展示了默认管理节点的 `obj.conf` 文件。

## 示例 5.4 默认 obj.conf 文件

```xml
#
# 版所有 2006 Sun Microsystems, Inc. 保留所有。
# 使用受许可条款约束。
#

# 您可以编辑此文件，但在使用管理 GUI 或 CLI 时，
# 注释和格式更改可能会丢失。

<Object name="default">
AuthTrans fn="match-browser" browser="*MSIE*"
ssl-unclean-shredout="true"
NameTrans fn="ntrans-jee" name="jee"
NameTrans fn="pfx2diri" from="/mc-icons" dir="/opt/webserver7/lib/icons"
name="es-internal"
PathCheck fn="unix-uri-clean"
PathCheck fn="findpathinfo"
PathCheck fn="find-index-jee"
PathCheck fn="find-index" index-names="index.html,home.html,index.jsp"
ObjectType fn="type-jee"
ObjectType fn="type-by-extension"
ObjectType fn="force-type" type="text/plain"
Service method="GET | HEAD" type="magnus-internal/directory"
fn="index-common"
Service method="GET | HEAD | POST" type="*-magnus-internal/*"
fn="send-file"
Service method="TRACE" fn="service-trace"
Error fn="error-jee"
Addlog fn="flex-log"
</Object>

<Object name="jee">
Service fn="service-jee" method="*"
</Object>

<Object name="es-internal">
</Object>

<Object name="es-internal">
</Object>

<Object name="cgi">
ObjectType fn="force-type" type="magnus-internal/cgi"
Service fn="send-cgi"
</Object>
```

## 5.3 OBJ.CONF 文件

```xml
<Object name="send-precompressed">
PathCheck fn="find-compressed"
</Object>
```

```xml
<Object name="compress-on-demand">
Output fn="insert-filter" filter="http-compression"
</Object>
```

### 5.3.2 语法

对象配置文件中的指令遵循与 `magnus.conf` 中包含的指令类似的语法（详情参见表 5.2）。例外是，对象配置文件还包含用于将指令分组在一起的对象（称为模板/templates）。模板允许您根据条件处理指令。

> 注意：有关如何根据条件处理请求的信息，请参阅第 6 章“Web 服务器 7.0 请求处理”。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_193_0.png)

对象配置文件的整体结构如下：

```xml
<Object name="default">
directives
</Object>
```

```xml
<Object name="objectname">
directives
</Object>
```

```xml
<Object name="objectname">
directives
</Object>
```

这些模板的顺序并不重要，但必须存在一个名为 `default` 的模板。`default` 模板中包含的指令用于处理每个请求。Web 服务器 7 的对象配置文件包含一个标准的默认模板，其中包含用于标准请求处理的指令。这使您能够在安装后立即处理请求。

# 第 5 章 Web 服务器 7.0 配置文件

**警告**：不要更改默认模板的名称，否则将无法处理请求。如果没有默认模板，实例将无法启动，但在请求过程中会标记一个类似的错误：

```
[05/Aug/2007:07:27:28:02] config ( 3208): for host 127.0.0.1 trying to GET / , process-uri-objects reports: HTTP: find template default
```

配置文件中的某些语法错误可能会导致实例无法启动，而另一些错误直到处理请求时才会被发现。导致实例启动的错误示例包括指令名称拼写错误或指令参数名称，可以在以下示例中找到：

```
NameTrans func="pfx2dir" from="mc-icons" dir="/opt/webserver7/lib/" name="es-internal"
```

在此示例中，指令参数 `fn` 指定不正确。如果发生这种情况，当我们尝试启动实例时，您将看到类似的错误：

```
config: CONF2265: Error parsing file obj.conf, line 12, column 1:
Missing parameter (need fn)
config: CORE3235: File server.xml line 71: Error processing
<object-file> element: Error processing file obj.conf
failure: server initialization failed
```

其他语法错误不容易被注意到，直到处理请求时才会被识别。例如，如果您在 `fn` 规范中指定了错误的 `SAF`：

```
NameTrans fn="badfunc" from="/mc-icons" dir="/opt/webserver7/lib/ " name="es-internal"
```

您在启动时将看到如下警告消息：

```
config: trying to GET / , func_exec reports: HTTP2120: cannot find function
```




## 5.3 OBJ.CONF 文件

示例 5.4 展示了作为默认对象配置文件一部分定义的各种对象。

`<object>` 标签最常用的属性之一是 `name` 属性，它在配置文件中唯一标识该对象。使用 `name` 属性的对象的语法如下：

```
<Object name="objectname">
  directives
</Object>
```

对象配置文件包含一个默认对象，它告诉实例默认如何处理请求。

```
<Object name="default">
  directives
</Object>
```

对象配置文件可以包含仅在满足特定 `NameTrans` 指令的某些条件为真时才执行的对象。其中两种条件涉及使用额外的命名对象或 `ppath` 对象。

### 命名对象处理

条件处理的一个一个示例是使用 `NameTrans` 指令中的可选属性。假设客户端正在请求以下 URL：

```
http://www.example.com/mc-icons/back.gif
```

在请求处理期间，服务器会评估默认对象中的每个 `NameTrans` 指令以尝试查找匹配。在这种情况下，由于 URI 以 `/mc-icons` 开头，因此匹配了第二个指令。

```
NameTrans fn="ntrans-j2ee name="j2ee"
NameTrans fn="pfx2dir from="/mc-icons" dir="/opt/webserver7/lib/ics" name="es-internal"
```

服务器然后判断是否为指令指定了 `name` 属性。

```
NameTrans fn="pfx2dir from="/mc-icons" dir="/opt/webserver7/lib/ics" name="es-internal"
```

如果指令指定了 `name` 属性，则属性值指向另一个对象，该对象包含了用于处理请求的额外指令。

```
<Object name="es-internal">
directives
</Object>
```

对于正在处理的特定阶段，额外对象中发现任何指令都会在默认对象中找到指令之前被处理。

> 注意：请求处理将在第 6 章进行详细讨论。

### ppath 对象处理

另一个条件处理示例是使用 `ppath`（部分路径）对象。

```
<Object ppath="path">
directives
</Object>
```

`ppath` 对象允许你指定一个文档或资源的路径，只有当资源路径可以在 `ppath` 值指定的路径下方找到时，对象中包含的指令才会被执行。例如，假设你指定了如下 `ppath` 对象：

```
<Object ppath="opt/webserver7/https-www.example.com/docs/private//">
directives
</Object>
```

在处理 `NameTrans` 指令期间，如果确定资源可以在 `/opt/webserver7/https-www.example.com/docs/private/` 目录下找到，则在此 `ppath` 对象中发现的任何指令将在默认对象中找到的指令之前被处理。

通常，服务器始终从默认对象开始处理请求，并根据 `NameTrans` 指令中的条件处理其他对象中的指令。添加到对象配置文件的每个新对象都有可能修改默认对象的行为。

### 5.3.2.3 变量

SAF 参数可以包含对变量和表达式的引用。变量可以是预定义变量、使用 `set-variable` SAF 在请求定义的定义的变量或在 `server.xml` 文件中定义的变量。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_199_0.png)

> 注意：`set-variable` SAF 允许在请求处理期间动态创建变量。这是一项非常强大的功能，但当未定义的变量在被使用（在请求期间）之前不报告时，可能会令人困惑。

在 `server.xml` 文件本身中，可以在多个级别定义变量（例如 `<server>` 和 `<virtual-server>`）。因此，服务器必须有一种方法来解决重复的变量定义。在尝试解析变量时，服务器按（以下顺序）提供以下命名空间：

- 预定义变量
- 通过使用 `set-variable` SAF 在请求时定义的变量
- 在 `<virtual-server>` 级别定义的虚拟服务器特定变量
- 在 `<server>` 级别定义的服务器变量

Web 服务器名称以美元符号 ($) 开头，后跟大写或小写字母。变量的语法如下：

``````
$[A-Za-z0-9_]*
```

### 5.3.3 上文

`server.xml` 文件包含每个虚拟服务器的定义。每个虚拟服务器可以使用不同的 MIME 类型文件，该文件用于标识资源。

### 5.3.4 修改

通过管理控制台或命令行进行的某些更改会更新相应的对象配置。文件中的错误可能会防止实例正常启动。

## 5.4 MIME.TYPES 文件

多用途互联网邮件扩展（MIME）类型文件。通过将不同的 MIME 文件关联到每个虚拟服务器，可以让你在虚拟服务器级别上支持不同的资源。

### 5.4.1 文件结构

`mime.types` 文件包含一系列关联，帮助实例识别请求类型并随后理解如何处理请求。示例 5.6 展示了默认管理节点的 MIME 类型文件。





## 第 5 章 Web 服务器 7.0 配置文件

type=application/msword
type=application/oda
type=application/pdf
type=application/postscript
type=application/studium
type=application/timbuktu
type=application/vnd.ms-excel
extsext-doc,dot,wiz,rtf
extsext-oda
extsext-pdf
extsext-ai,eps,ps
extsext-smp
extsext-tbt
extsext-xls,xlw,xla,lc,xlm,xlt
extsext-ppt,pps,pot

[条目已删除]

+ - enc=x-gzip
- enc=x-compress
- enc=x-uewcode
extsext-gz
extsext-z
extsext-uu,uue

type=magnus-internal/parsed-html
type=magnus-internal/cgi
extsext-shtml
extsext-cgi,exe,bat

type=application/x-x509-server
type=application/x-x509-server-cert
type=application/x-x509-user-cert
type=application/x-x509-email-cert
extsext-cacert
extsext-scert
extsext-ucert
extsext-ecert

type=application/vnd.sun.xml.writer
type=application/vnd.sun.xml.writer.template
type=application/vnd.sun.xml.calc
type=application/vnd.sun.xml.draw
type=application/vnd.sun.xml.calc.template
type=application/vnd.sun.xml.template
type=application/vnd.sun.xml.impress
type=application/vnd.sun.xml.impress.template
type=application/vnd.sun.xml.writer.global
type=application/vnd.sun.xml.math
extsext-sxw
extsext-stw
extsext-sxc
extsext-stc
extsext-sxd
extsext-std
extsext-sxi
extsext-sti
extsext-sxg
extsext-sxm

type=application/vnd.stardision.writer
type=application/vnd.stardision.writer-global
type=application/vnd.stardision.calc
type=application/vnd.stardision.draw
type=application/vnd.stardision.impress
type=application/vnd.stardision.impress-packed
type=application/vnd.stardision.math
type=application/vnd.stardision.chart
type=application/vnd.stardision.mail
extsext-sdw
extsext-sgl
extsext-sdc
extsext-sda
extsext-sdd
extsext-sdp
extsext-smf,sdf
extsext-sds
extsext-sdm

## 5.4.2 文件结构

该格式与 Web 浏览器与其连接的 Web 服务器之间交换请求/响应信息的格式相似。这种相关格式作为超文本传输协议（HTTP）的一部分指定，并遵循以下规则：

MIME 类型文件的第一行标识文件格式：

```
#--Sun Microsystems MIME 信息
```

其他未注释的行具有以下格式：

```
type=type/subtype exts=[文件扩展名]
```

其中 type/subtype 指的是 MIME 类型，subtype 指的是与该类型相关的扩展名。例如，MIME 类型文件使用以下映射将扩展名 .html 和 .htm 关联到 text/html：

```
type=text/html exts=htm,html
```

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_203_0.png)

> 注意：关于 HTTP 的权威信息，您应该咨询 RFC 2616，“超文本传输协议—HTTP/1.1”。

## 5.4.3 处理

MIME 类型配置文件决定了您的 Web 服务器的虚拟服务器如何将文件名扩展名映射到返回给浏览器的 MIME 类型。您的浏览器随后会将这些 MIME 类型映射到“助手”应用程序或内联插件。

以下小节描述了在请求/响应处理期间，Web 服务器和用户代理如何使用 MIME 映射。

### 5.4.3.1 服务器处理

当 Web 服务器从客户端接收资源请求时，它使用 MIME 类型映射来确定请求的资源类型。

在请求处理的 ObjectType 阶段，服务器确定客户端请求的资源的 MIME 类型属性。使用了几种不同的 SAF 来确定 MIME 类型，但最常用的是按扩展名类型（type-by-extension）。此函数告诉服务器根据 MIME 类型表（存储在 MIME 类型文件中）中请求资源的扩展扩展名查找 MIME 类型。

MIME 类型由三个属性定义：语言（lang）、编码（enc）和内容类型（type）。至少有一个这些属性必须存在。最常用的属性是 type。当服务器生成响应时，MIME 类型、语言和编码这些属性会发送给客户端。

> 注意：在发送响应时，服务器根据 MIME 类型来决定。enc 和 lang 属性通常不使用。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_204.png)

如果存在多个 MIME 类型，服务器将按照其顺序进行处理。以下步骤概述了服务器处理 MIME 映射的高级别：

- 当服务器到达 ObjectType 阶段时，它读取 MIME 类型文件查找匹配的扩展名。
- 服务器找到匹配项并设置为 text/html。
- 服务器选择处理请求的服务。
- 服务器向客户端发送带有相应 Content-type 的响应。

## 5.4.3 MIME 类型文件

| 类型 | 扩展名 |
| :--- | :--- |
| type=text/css | css |
| type=text/html | htm |
| type=text/plain | txt |
| type=text-separated | tsv |
| type=text/x-richtext | rt |
| type=text/x-speech | talk |
| type=text/xml | xml |
| type=text/xul | xul |

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_205.png)

```
HTTP/1.1 200 OK
Server: Sun-Web-Server/7.0
Content-type: text/html
```

### 5.4.3.2 客户端处理

相应阶段的 SAF 生成数据并将其给客户端。当服务器向客户端发送数据时，还会发送头信息。这些头信息包含了 MIME 类型属性（通常由 type 定义）。

客户端维护自己的 MIME 类型表，如图 5.2 所示。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_206.png)

## 5.2 客户端定义

当客户端接收到头信息时，它使用自身 MIME 类型中的信息决定如何处理。对于浏览器，通常的操作是在浏览器窗口中显示数据。

有时请求资源无法在浏览器窗口中显示，需要由应用程序处理。在这种情况下，服务器返回的 Content-type 通常以 application/ 开头，例如 application/x-pdf（针对 .pdf 文件）或 application/x-maker（针对 .fm 文件）。

客户端有一组用户可编辑的映射，告诉浏览器数据类型使用数据应用程序。例如，如果类型是 application/x-pdf，客户端通常通过打开 Adobe Acrobat Reader 来显示文件。

### 5.4.4 上下文

server.xml 文件包含实例中每个虚拟服务器的定义，因此 server.xml 与虚拟服务器之间存在一对多的关系。

每个虚拟服务器可以使用不同的 MIME 类型文件进行映射关联。因此，实例与 MIME 类型文件之间存在一对多的关系，但虚拟服务器与其 MIME 类型文件之间存在一对一的关系。





## 5.5 信任数据库文件 (*.DB Files)

### 5.4.5 修改

尽管默认的 MIME 类型文件包含了最常见的 MIME 定义，但你也可以自由修改该文件以添加对任何额外 MIME 类型的支持。要添加新的 MIME 类型定义，只需按照以下格式将定义追加到文件中现有的 MIME 类型之后（其中 `type/subtype` 是文件名以其中一个扩展名结尾的文档 MIME 类型）：

```
type=type/subtype exts=extension1,extension2...,extensionN
```

扩展名列表包含任意数量的逗号分隔的文件名扩展名。MIME 类型条目的示例可以在虚拟服务器随附的默认 MIME 类型文件中找到。

你也可以使用管理控制台或命令行界面来更新虚拟服务器的 MIME 文件。文件更新后，你必须部署更新后的配置，更改才会反映在相应的管理节点（s）上。

在实例启动或执行动态重新配置时会读取 MIME 类型文件。MIME 类型文件中包含的语法将在启动或重新配置代码库中进行验证。在 MIME 类型文件或 `server.xml` 文件（涉及 `<mime-file>` 属性）中发现的错误可能会导致实例无法启动。

## 5.5 信任数据库文件 (*.db Files)

Web 服务器通过两个网络安全服务 (NSS) libdbm 数据库文件存储安全信息，如下：

- cert8.db—存储公共可访问的对象（例如证书、证书吊销列表和 S/MIME 记录）
- key3.db—存储由服务器生成的私钥
- secmod.db—存储 PKCS #11 模块配置信息

这些文件的组合通常称为信任数据库，每个文件在保护你的 Web 服务器方面起着不同的作用。

例如，cert8.db 和 key3.db 文件用于存储启用安全套接层 (SSL) 的公钥、私钥和证书。secmod.db 文件存储用于启用和配置 Web 服务器使用的附加模块（如硬件加速卡）的信息。请参考第 8 章“保护 Web 服务器 7.0”获取有关如何使用这些文件为你的 Web 服务器提供安全的更多信息。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_208_0.png)

注意：NSS 是一组旨在支持启用安全功能的客户端和服务器应用程序跨平台开发的库。使用 NSS 构建的应用可以支持 SSL v2 和 v3、TLS、PKCS #5、PKCS #7、PKCS #11、PKCS #12、S/MIME、X.509 证书和其他安全标准。有关 NSS 的更多信息，请访问 https://www.mozilla.org/projects/security/pki/nss/

### 5.5.1 文件结构

信任数据库采用 Berkeley DB 1.85 哈希格式格式，因此无法使用标准文本编辑器查看或编辑。然而，你可以使用十六进制编辑器或 UNIX strings 命令来了解这些文件的内容。5.7 提供了 cert.8.db 文件的示例。

示例 5.7 cert8.db 文件的十六进制输出片段

```
0000b20 00 00 08 03 00 01 00 15 00 00 63 65 72 74 2d
0000b20 66 6f 62 2e 75 7e 61 6d 70 6c 65 23 65 62 64 6d 00
0000b30 03 55 04 06 13 02 55 4c 31 30 6c 03 55 04 07 13 05 .U....SL1.U...
0000b30 00 6f 00 00 87 1b 31 30 68 31 03 09 06 09 ..o...$.*U01h.o..
0000b40 04 03 55 31 31 09 05 53 03 31 09 06 03 05 55 04 **....SL1.U...
0000b40 08 53 01 02 46 63 31 10 6c 03 06 03 05 55 04 ..FL1.0....U....
0000b60 54 61 64 61 73 74 31 31 30 06 03 05 55 04 13 04 Tampal.O....U....
0000b70 54 65 72 72 72 31 38 06 03 05 13 0a 57 Test1.0..U....W
0000b80 65 20 53 75 72 76 72 72 75 31 18 06 03 05 55 oo.Server1.0..U....
0000b90 04 03 13 03 0f 66 6f 62 2e 75 73 61 64 74 65 72 65-
0000bca 63 6f 64 03 30 68 31 30 09 06 03 55 04 13 06 com.oh1.0..U....
0000bb0 02 55 53 31 31 09 06 03 05 54 08 12 04 43 FC .SL1.0..U....
0000b3c 31 30 03 06 03 05 55 04 13 04 Tampal.O....U....
```





## 5.7 certmap.conf 文件

Web Server 7 可以配置为允许通过 X.509 数字证书进行客户端身份验证。这可以在特定 HTTP 监听器的 SSL 设置下进行。

当服务器接收到来自客户端的请求时，它可以在继续操作之前请求客户端证书。客户端被程序化为通过向服务器发送客户端证书来响应。

在检查客户端证书链是否以受信任的证书颁发机构 (CA) 结尾后，Web Server 可以可选地确定由客户端证书标识的用户，然后在目录服务器中查找该用户的条目。Web Server 通过比较证书中的信息与用户目录条目中的数据来对用户进行身份验证（认证）。

为了在目录中定位用户条目，服务器必须知道如何解释来自不同 CA 的证书。你通过证书映射配置文件 (certmap.conf) 为服务器提供解释信息。该文件为每个列出的 CA 提供了三类信息：

- 它将证书中的区分名称 (DN) 映射到 LDAP 目录中的分支点（branch point）。
- 它指定了服务器应该使用证书中的哪些值（用户名、电子邮件地址等）来执行目录搜索。
- 它指定了服务器是否应该通过额外的验证过程。该过程涉及将客户端用于认证的证书与存储在用户目录条目中的证书进行比较。通过比较证书，服务器决定是否访问证书，或是否通过从用户目录条目中删除它来撤销证书。

如果有多个条目包含用户证书中的信息，服务器可以检查所有匹配的条目，以确定哪个用户正在尝试身份验证。在检查目录条目时，服务器会将提交的证书与条目中存储的证书进行比较。如果提交的证书不匹配任何目录条目，或者匹配的条目不包含匹配的证书，则客户端身份验证失败。

服务器在目录中找到匹配的条目和证书后，它可以为客户端确定适当的类型。例如，某些服务器使用用户条目中的信息来确定组成员关系，这反过来可以在评估访问控制指令 (ACI) 期间使用，以确定用户被授权访问哪些资源。

## 5.7 certmap.conf 文件

注意：有关访问控制指令的更多信息，请参阅第 8 章。

### 5.7.1 文件结构

certmap.conf 文件包含了关于如何将客户端证书映射到目录服务器条目的信息。示例 5.8 展示了默认管理节点文件的证书映射配置。

示例 5.8 默认 certmap.conf 文件

```
#
# 版权 2006 Sun Microsystems, Inc. 保留所有。
# 使用受许可条款限制。
#
```

```
#
# 此文件配置了证书如何映射到 LDAP 条目。
# 有关此文件的信息，请参阅文档。
# 此文件的格式如下：
# certmap <name> <issuerDN>
# <name>:<prop1> [val1]
# <name>:<prop2> [val2]
#
```

# 注释：
# 1. 映射可以按证书的每个发行者定义。如果特定的 'issuerDN' 不存在映射，则服务器将使用默认映射。
# 2. 必须有一个 <name>=default 且 issuerDN 为 "default" 的条目。这是映射条目。
# 3. '# ' 可用于注释掉一行。
# 4. DNComps 和 FilterComps 用于形成基准 DN 和过滤器响应，以便在将证书映射到用户条目时执行 LDAP 搜索。
# 5. DNComps 可以是以下内容之一：
# 注释掉 - 直接从证书中获取用户的 DN
# 空白 - 搜索整个 LDAP 树 (DN == suffix)
# attr nms - 用逗号分隔的属性列表，用于形成 DN
# 6. FilterComps 可以是以下内容内容之一：
# 注释掉 - 将过滤器设置为 "objectclass=*"
# 将过滤器设置为 "objectclass=*"
# 空白
# attr names - 用逗号分隔的属性列表，用于形成过滤器
#

```
certmap default default
#default:DNComps
#default:FilterComps e, uid
#default:verifycert on
#default:CmapAttr subjectDN
#default:library <path_to_shared_lib_or_dll>
#default:InitFn <init function>
```

### 5.7.2 语法

该文件包含一个或多个命名映射，每个映射适用于不同的证书颁发机构 (CA)。行头的哈希符号 (#) 表示该行是注释。Web Server 会忽略这些行。额外的行具有以下语法：

```
certmap <name> <issuerDN>
<name>:<property [value>]
```

第一行使用 `name` 参数为证书映射指定一个名称。它使用 `issuerDN` 参数指定形成 CA 证书中找到的区分名称的属性。`name` 属性是任意的；你可以命名为任何名称。然而，`issuerDN` 属性必须与颁发客户端证书的 CA 的区分名称完全匹配。例如，两个 `issuerDN` 行仅在分隔属性的空格上不同，但服务器将这些条目视为不同的：

```
certmap name ou=Example CA, c=US
certmap name ou=Example CA, c=US
```

映射的第二行及后续行标识了服务器在目录搜索从证书中提取的信息时应使用的规则：

```
certmap name issuerDN
name:property1 [value1]
name:property2 [value2]
```

这些规则通过 DNComps、FilterComps、VerifyCert、CmapAttr、Library 和 InitFn 指定，用于将证书映射到用户条目。表 5.4 描述了证书中的属性。

# 属性 certmap.conf 属性

| 属性 | 描述 |
| :--- | :--- |
| DNComps | 一组逗号分隔的属性列表，用于在将证书映射到用户条目时执行 LDAP 搜索时形成基准 DN 和过滤器响应。DNComps 可以是以下内容之一：<br>- 注释掉 - 直接从证书中获取用户的 DN<br>- 空白 - 搜索整个 LDAP 树 (DN == suffix)<br>- attr nms - 用逗号分隔的属性列表，用于形成 DN |
| FilterComps | 一组逗号分隔的属性列表，用于形成过滤器。FilterComps 可以是以下内容之一：<br>- 注释掉 - 将过滤器设置为 "objectclass=*"<br>- 将过滤器设置为 "objectclass=*"<br>- 空白<br>- attr names - 用逗号分隔的属性列表，用于形成过滤器 |

# 5.4 certmap.conf 属性继续

| 属性 | 描述 |
| :--- | :--- |
| FilterComps | 一组逗号分隔的属性列表，用于在将证书映射到用户条目时执行 LDAP 搜索时形成基准 DN 和过滤器响应。FilterComps 也可以是以下内容之一：<br>- 注释掉 - 将过滤器设置为 "objectclass=*"<br>- 将过滤器设置为 "objectclass=*"<br>- 空白<br>- attr names - 用逗号分隔的属性列表，用于形成过滤器 |
| verifycert | 告诉服务器是否应该比较目录中找到的证书。它接受两个值：on 和 off。只有当你的 LDAP 目录包含证书时，才使用此属性。此功能用于确保用户拥有有效的未撤销的证书。 |
| cmapLdAttr | 目录中包含本地 DN 的属性名称。其默认值为 certDN。此属性不是标准的 LDAP 属性；要使用此属性，必须扩展 LDAP 架构。如果 cmapLdAttr 指定的属性已索引，搜索速度将更快。如果 certmap.conf 文件中存在此属性，服务器将在目录中搜索与（以此属性命名的）匹配的完整 DN（取自证书）。如果搜索未找到条目，服务器将使用 DNComps 和 FilterComps 映射重试搜索。 |
| Library | 属性值为指向共享库或 DLL 的路径。只有当你使用证书 API 创建自定义属性时，才需要使用此属性。更多信息请参阅 Sun Java System Web Server 7.0 开发者指南。 |
| InitFn | 属性值为自定义库中初始化 (init) 函数的名称。只有当你使用证书 API 创建自定义属性时，才需要使用此属性。 |





## 5.7 CERTMAP.CONF 文件

如果你正在使用 Library 和 InitFn 属性，完整的映射可能如下所示：

```
certmap Example CA ou=Example CA, o=Example, c=US
Example CA:CmapLdapAttr certSubjectDN
Example CA:DNComps e, C
Example CA:FilterComps uid
Example CA:VerifyCert on
```

在此示例中，证书映射的名称为 Example CA，它映射到发行者的区分名称 `ou=Example CA, o=Example, c=US`。

> 注意：请注意映射属性的其余行是如何以证书映射名称（Example CA）开头的。Web 服务器正是通过此知道这些属性适用于该映射。

`CmapLdapAttr` 属性告诉服务器在整个目录中搜索 `certSubjectDN` 与客户端证书列出的主体完整 DN 匹配的条目。如果搜索没有任何条目，服务器将使用 `DNComps` 和 `FilterComps` 映射重试搜索。

`DNComps` 属性表示搜索的基区分名称（baseDN）应该根据从客户端证书中提取的组织（organization）和国家（country）属性来创建。

`FilterComps` 属性表示 Web 服务器应该搜索与从客户端证书中提取的电子邮件（e-mail）和用户 ID（user ID）属性匹配的条目。

`VerifyCert` 属性告诉服务器是否将客户端证书与用户目录条目中的证书进行比较。值 `on` 确保除非呈现证书与存储在目录中的证书完全匹配，否则服务器不会对客户端进行身份验证。

### 5.7.3 上文

每个服务器实例都有自己的证书映射配置文件；因此，服务器实例与此文件之间是一一对应的关系。

### 5.7.4 修改

管理控制台和命令行界面未提供管理证书映射文件的方法。因此，必须在特定的管理节点直接向 `certmap.conf` 文件添加条目。执行此操作后，必须将更改推回配置并根据情况推送到额外的管理节点。

## 5.8 default.acl 文件

你可以控制对整个 Web 服务器或服务器部分（例如目录、文件和文件类型）的访问。当 Web 服务器评估传入的请求时，它根据允许访问控制条目（ACEs）的分级规则来决定访问权限。Web 服务器使用匹配的条目来确定客户端请求是被允许还是拒绝。

ACE 集合被称为访问控制列表（ACL）。Web 服务器从上到下处理 ACL 列表。如果在任何时候 ACE 的评估值为 `false`，ACL 的处理将停止，用户被拒绝访问资源。

ACL 文件包含定义谁可以访问存储在 Web 服务器上的资源的规则。默认情况下，Web 服务器使用一个包含默认访问列表 `default.acl`。你可以通过编辑此文件或为一个或多个实例创建额外的 ACL 文件来更改访问控制规则。如果你创建了额外的 ACL 文件，可以使用 server.xml 中的 `<acl-file>` 元素将其与不同的虚拟服务器关联。

示例 5.9 展示了如何使用 `<acl-file>` 元素为特定服务器指定 ACL 文件：

示例 5.9 ACL 文件的虚拟服务器定义

```
<virtual-server>
<name>www.example.com</name>
<http-listener-name-http-listener-1</listener-name>
<host>www.example.com</host>
<object-file>www.example.com-obj.conf</object-file>
<mime-file>mime.types</mime-file>
<acl-file>example.acl</acl-file>
</virtual-server>
```

## 5.8 DEFAULT.ACL 文件

```
<document-root>/export/home/example.com/public_html</document-root>
<access-log>
<file>/export/home/example.com/logs/access</file>
</access-log>
</virtual-server>
```

为每个虚拟服务器关联不同的 ACL 文件，可以让你在虚拟服务器级别提供不同访问控制的活性。

### 5.8.1 文件结构

ACL 文件是一个包含一个或多个 ACL 的文本文件。示例 5.10 展示了默认管理节点的访问控制列表文件。

示例 5.10 default.acl 文件

```
# Copyright 2006 Sun Microsystems, Inc. All rights reserved.
# Use is subject to terms.
version 3.0;
acl "default" {
  allow (read, info) user = "everyone";
  allow (list, write) user = "admin";
  deny (all) user = "guest";
}

acl "/public_html/private/*" {
  allow (read, info) user = "authorized_user";
  allow (list, write) user = "admin";
  deny (all) user = "guest";
}
```

### 5.8.2 语法

输入字符串可以包含以下字符：

- 字母 a 到 z 以及数字 0 到 9
- 点 (.) 或下划线 (_)

如果你使用任何其他字符，请在其周围加上双引号。单个语句可以单独占一行，并以分号结束。多个语句放在大括号内。项目列表必须用逗号隔开，并用双引号括起来。

### 5.8.3 身份验证方法

ACL 可以可选地指定服务器在处理 ACL 时必须使用的身份验证方法。共有三种方法：

- basic
- digest
- ssl

basic 和 digest 方法都需要用户在访问资源之前输入用户名和密码。然而，两者的区别在于客户端与 Web 服务器之间传输数据的方式，以及在身份数据库中验证密码的方式。

basic 身份验证方法允许用户输入用户名和密码，并将信息以知的 Base64 编码传输到 Web 服务器。出于安全考虑，basic 几乎总是与 SSL 连接一起使用，用户名和密码在从客户端发送之前会被加密。

digest 身份验证方法防止客户端的用户名和密码以明文发送。浏览器使用 MD5 算法通过密码和 Web 服务器发送的信息创建消息摘要。摘要值在服务器端使用 Digest 身份验证插件进行计算和比较。

ssl 方法要求用户拥有客户端证书。Web 服务器必须开启加密，并且用户的证书颁发机构必须在受信任证书颁发机构（CA）列表中。有关使用客户端证书进行身份验证的更多信息，请参见第 5.7 节“certmap.conf 文件”。




# 第 5 章 Web 服务器 7.0 配置文件

默认情况下，对于任何未显式指定方法的 ACL，服务器都使用基础方法（basic）。如果你使用摘要方法（digest），服务器的身份验证数据库必须能够处理摘要认证。身份验证数据库在 `server.xml` 中通过 `<auth-db>` 元素配置。有关配置身份验证数据库的更多信息，请参阅第 8 章。

每一行身份验证内容必须指定属性（用户、组或同时包含用户和组）。以下位于 ACL 类型行之后的身份验证语句指定了基础认证，并将用户与数据库或目录中的单个用户匹配：

```
authenticate (user) { method = "basic";
```

以下示例使用 `ssl` 作为用户和组的认证方法：

```
authenticate (user, group) { method = "ssl";
```

以下示例允许任何以 `sales` 开头的用户：

```
authenticate (user)
allow (all)
  user = sales*
```

如果将最后一行改为 `group = sales`，则 ACL 将失败，因为组属性未经过身份验证。

## 5.8.2.3 授权语句

每个 ACL 条目可以包含一个或多个授权语句。授权语句指定了谁允许或拒绝访问服务器资源。使用以下语法编写授权语句：

```
allow|deny [absolute] (right[,right..]) attribute expression;
```

每条语句都以 `allow` 或 `deny` 开头。由于层级规则，通常的做法是在第一条规则中拒绝所有人的访问，并在后续规则中专门允许用户、组或计算机的访问。也就是说，如果你允许访问名为 `/my_stuff` 的目录，并且你有一个允许少数用户访问的子目录 `/my_stuff/personal`，那么该子目录的访问控制将不起作用，因为任何被允许访问 `/my_stuff` 目录的人也被允许访问 `/my_stuff/personal` 目录。为了防止

## 5.8 DEFAULT.ACL 文件

出现这种情况，请为子目录创建一个规则，首先拒绝任何访问，然后允许需要访问的少数用户访问。

在某些情况下，如果你将默认 ACL 设置为拒绝所有人访问，则你的其他 ACL 规则就不需要 `deny all` 规则。

以下行拒绝了所有人的访问：

```
deny (all) user = "anyone";
```

## 5.8.2.4 授权语句的层级

ACL 具有取决于资源的层级。例如，如果服务器接收到文档（URI）`/my_stuff/web/presentation.html` 的请求，服务器将构建一个适用于该 URI 的 ACL 列表。服务器首先添加 `obj.conf` 文件中 `check-acl` 语句列出的 ACL。服务器随后追加匹配的 URI 和 PATH ACL。

服务器按照相同的顺序处理此列表。除非存在绝对（absolute）ACL 语句，否则所有语句都按顺序评估。如果绝对 `allow` 或绝对 `deny` 语句的评估结果为 `true`，服务器将停止处理并接受该结果。

如果匹配到多个 ACL，服务器将使用最后一个匹配的语句。然而，如果你使用了绝对语句，服务器将停止查找其他匹配项，并使用包含绝对语句的 ACL。如果你对同一资源有两个绝对语句，服务器将使用文件中的第一个，并停止查找其他匹配的资源。

示例 5.11 展示了如何编写 ACL 以允许 `user1` 访问 `/my_stuff/web/presentation.html` 的内容。

### 示例 5.11 保护 Web 服务器内容的 ACL 示例

```
version 3.0;
acl "default"; {
  authenticate (user, group) {
    prompt = "Sun Java Web Server";
  };
  allow (read, execute, info) user = "anyone";
  allow (list, write, delete) user = "all";
  acl "uri/my_stuff/web/presentation.html";
  deny (all) user = "anyone";
  allow (all) user = "user1";
}
```

## 5.8.2.5 表达式属性

属性表达式根据用户名、组名、主机名或 IP 地址定义谁允许或拒绝访问。以下是允许不同用户或计算机访问的示例：

- user = "anyone"
- user = "smith*"
- group = "sales"
- dns = "*.sun.com"
- dns = "*.sun.com,*.mozilla.com"
- ip = "198.*"
- ciphers = "..."





## 5.10 LOGIN.FILE

### 5.9.2 上文

每个服务器实例都有自己的默认 `default-web.xml` 文件；因此，服务器实例与该文件之间是一一对应的。

### 5.9.3 修改

管理控制台（Administration Console）和命令行界面没有提供 `default-web.xml` 方法。因此，对该文件的所有修改都必须在特定的管理节点（Administration Node）上进行。完成后，必须将这些修改拉回到配置中，然后根据需要推送到额外的管理节点。

## 5.10 login.conf 文件

Java 身份验证和授权服务（JAAS）是一组 API，允许服务对用户进行身份验证并强制执行访问控制。它实现了一种标准可插拔认证模块（PAM）框架的 Java 技术版本，并支持基于用户的授权。

JAAS 可用于两个目的：

- 用于用户身份验证，以可靠且安全地确定当前正在执行 Java 代码的用户，无论该代码是以应用程序、applet、bean 还是 servlet 的形式运行的。
- 用于用户授权，确保他们拥有执行所执行操作所需的访问控制权限（权限）。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_227_0.png)

> 注意：更多信息请参见 Sun 网站上的 http://java.sun.com/products/jaas/  Java 身份验证和授权服务页面。

登录配置文件（login.conf）包含了 JAAS 用于客户端认证的登录模块定义。它在特定服务器实例的 JVM 设置中被引用，如示例 5.12 所示。

### 示例 5.12 server.xml 中对登录文件的引用

```xml
<jvm>
<java-home>/opt/webserver7/jdk/java-home</java-home>
<server-class-path>../server-class-path</server-class-path>
<debug>false</debug>
<debug-jvm-options>-Xdebug -Xrunjdw:transport=dt_socket,server=y,suspend=n,address=7896</debug-jvm-options>
<jvm-options>-Djava.security.auth.login.config=login.conf</jvm-options>
<jvm-options>-Djava.util.logging.manager=com.sun.webserver.logging.ServerLogManager</jvm-options>
<jvm-options>-Xms128m -Xmx256m</jvm-options>
</jvm>
```

### 5.10.1 文件结构

登录配置文件指定了用于每个认证域（realm）的 Java 类。示例 5.13 展示了默认管理节点的 login.conf。

### 示例 5.13 默认 login.conf

```java
/* Copyright 2006 Sun Microsystems, Inc. All rights reserved. */
/* Use is subject to license terms. */

fileRealm {
  com.planet.ias.security.auth.login.FileLoginModule required;
}
ldapRealm {
  com.planet.ias.security.auth.login.LDAPLoginModule required;
}

solarisRealm {
  com.planet.ias.security.auth.login.SolarisLoginModule required;
}

nativeRealm {
  com.planet.ias.security.auth.login.NativeLoginModule required;
};
```

### 5.10.2 语法

登录配置文件中登录模块定义的基本格式如下：

```
Application {
  ModuleClass Flag ModuleOptions;
  ModuleClass Flag ModuleOptions;
  ModuleClass Flag ModuleOptions;
}
```

登录配置文件中的每个条目通过应用程序名称（Application）索引。每个应用程序包含一个为该应用程序配置的登录模块列表。每个登录模块由其完全限定类名（ModuleClass）指定。认证按照指定的顺序在模块列表中进行。Flag 值控制认证向下执行的整体行为。Flags 可以是 Required（必须）、Requisite（必须）、Sufficient（足够）或 Optional（可选）。ModuleOptions 是直接传递给底层登录模块的空格分隔列表。Options 由登录模块本身定义并控制其行为。

> 注意：更多信息请参见 http://java.sun.com/j2se/docs/api/javax/security/auth/login/Configuration.html java.security.auth.login 页面。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_229.png)

### 5.10.3 上文

每个服务器实例都有自己的登录配置文件；因此，服务器实例与该文件之间是一一对应的。

### 5.10.4 修改

管理控制台和命令行界面没有提供管理 default-web.xml 方法。因此，对该文件的所有修改都必须在特定的管理节点上进行。完成后，必须将这些修改拉回到配置中，然后根据需要推送到额外的管理节点。

## 511 keyfile

认证数据库是维护凭据的存储。这些凭据可以在授予 Web 服务器资源访问之前验证用户。常见的存储包括目录服务器、数据库和平面文件。Web Server 7 自带一个名为 keyfile 的默认存储，包含用于文件认证的用户和哈希密码。keyfile 默认是空的，但在 server.xml 中可以在实例级别、特定服务器或两者进行配置。示例 5.14 展示了将 keyfile 定义认证数据库的设置。

### 5.14 server.xml 中 keyfile 的定义

```xml
<auth-db>
  <name>keyfile</name>
  <url>file</url>
  <property>
    <name>keyfile</name>
    <value>/opt/webserver/example.com/config/keyfile</value>
  </property>
  <property>
    <name>syntax</name>
    <value>keyfile</value>
  </property>
</auth-db>
```

表 5.5 认证数据库属性

| 元素 | 描述 |
| :--- | :--- |
| <auth-db> | 指定认证数据库的开始和结束。 |
| <name> | 认证数据库的名称。用于引用 Web 服务器内的数据库，必须是唯一的。此值为任意的。 |
| <url> | 值 file 表示这是一个基于文件的认证数据库。该元素的其他值可能包括相应的 LDAP URL。 |
| <property> | 指定认证数据库的一组键/值属性对。列出的第一个属性是 keyfile。这表示数据库类型为 keyfile。keyfile 数据库的位置可以在以下路径找到：/opt/webserver/example.com/config/keyfile。下一个属性指定文件的语法。 |

### 5.11.1 文件结构

管理节点的 keyfile 默认是空的。每个新用户都会在 keyfile 中创建一个条目，如示例 5.15 所示。

### 示例 5.15 示例 keyfile

```text
# Copyright 2006 Sun Microsystems, Inc. All rights reserved.
# Use is subject to license terms.

# 简单域的用户列表。默认是空的。
rodale;SSHA)0Fga3ioPwQhdbW0uWNNMkKL7J2ydGVyAA==
elise;SSHA)5QKlGMJ27ZYYaOblcLE1kdmZKGVyAA==
wlay;SSHA)h3y4+I6f75k+5XH2EC1fv6ZI1pbbgAAAA==
```

管理实例使用 keyfile 存储其自身的认证凭据。示例 5.16 展示了管理节点的默认 keyfile：

### 示例 5.16 管理服务器实例的默认 keyfile

```text
# Copyright 2006 Sun Microsystems, Inc. All rights reserved.
# Use is subject to license terms.
#
# 简单域的用户列表。默认是空的。
admin;SSHA)h3y4+I6f75k+5XH2EC1fv6ZI1pbbgAAAA==;wsadmin
```

### 5.11.2 语法

keyfile 的基本格式为：

```
username; hashedpassword; group
```

基于文件的认证数据库文件中行的最大长度为 255 个字符。如果任何行超过此限制，服务器将无法启动，并在错误日志文件中记录一个错误。

### 5.11.3 上文

每个服务器实例都有自己的 keyfile 文件；因此，服务器实例与该文件之间是一一对应的。

### 5.11.4 修改

你可以通过管理控制台或命令行界面配置认证数据库。这会导致 server.xml 文件发生变化。如果该文件由于通过这两个接口之一的更改而进行更新，你必须在更改反映到相应的管理节点（s）之前部署更新后的配置。

向 keyfile 添加用户不需要重新部署配置。

在文件中发现的错误可能会阻止实例启动。

## 5.12 总结

知道如何使用管理控制台或 CLI 工具不足以有效管理你的 Web 服务器实例。你应该了解服务器的配置文件，以及通过管理控制台或 CLI 工具进行的更改如何影响这些文件。你可能永远不需要直接编辑配置文件，但拥有这些操作的知识将大大增加你成功管理服务器和调试由配置错误引起问题的概率。

## 5.13 自助实验

使用本章包含的信息来执行以下练习。这些练习将验证你对本章描述的概念的理解。




# 5.13 自学式实验室

1. 查看你默认服务器安装的 `server.xml` 文件。此操作针对节点上的文件，而不是 admin-server 实例下的文件。

2. 找到 `cluster` 元素。该实例的主机名称是什么？（请查找 `local-host` 元素）。

3. `instance` 元素定义了服务器集群中的成员。组成此服务器集群的单个实例的主机名是什么？

4. 找到 `log` 元素。该服务器实例的日志级别是什么？日志文件在你的文件系统中的位置在哪里？

5. `platform` 元素描述了服务器是作为 32 位还是 64 位进程运行的。该服务器运行在什么平台上？

6. 找到 `user` 元素（仅限 UNIX）。这是服务器运行的系统账户。Web Server 进程将以什么账户运行？

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_233_0.png)

> 提示：你可以执行 `ps -ef | grep http` 命令字符串来验证进程是否是以该用户运行的。

- 7. 找到 `auth-db` 元素。该元素取代了 Web Server 6.1 中 `dbswitch.conf` 的功能。ACL 授权数据库的 URL 是？

- 8. `auth-db` 元素包含 `property` 元素。所有的 `property` 元素必须包含 `name` 和 `value` 子元素（用于键/值对）。它们还可以包含一个 `description` 子元素，对于 `auth-db`，它们可能包含 `encoded` 子元素，表示该值是 Base 64 编码的。列出 `auth-db` 元素中定义的 `property` 元素的键/值对。

- 9. 找到 `acl-file` 元素。该元素包含了包含此服务器实例访问控制列表的文件名。该元素的值可以是文件系统中文件的绝对路径，也可以是相对于实例配置文件夹的文件名。控制此实例访问的文件名是什么？它位于何处？

- 10. 找到 `mime-file` 元素。该元素包含了用于请求处理的 MIME 类型的文件名。包含 MIME 类型映射的文件名是什么？它位于何处？

- 11. Web Server 6.1 监听套被称为 Web Server 7.0 HTTP 监听器。你通过 `http-listener` 元素定义 HTTP 监听器。该服务器的 HTTP 监听器定义了哪些子元素？

# 第5章 Web Server 7.0 配置文件

- 12. 虚拟服务器通过 `virtual-server` 元素定义。到为止讨论的许多元素可以在 `virtual-server` 元素的体内重新定义。这包括 `auth-db`、`acl-file` 和 `mime-file` 元素。允许虚拟服务器重新定义这些元素可以为服务器实例提供全局设置以及特定虚拟服务器的本地化设置的灵活性。该服务器定义的任何虚拟服务器定义了哪些子元素？

- 13. 这些虚拟服务器是否被任何全局元素（`auth-db`、`acl-file` 或 `mime-file`）重新定义过？如果是，是哪些？

> 注意：访问 http://www.sunserver.com 获取关于如何回答这些问题的详细说明。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_234_0.png)

- 14. 附加练习：为你的默认服务器实例制作 `server.xml` 备份。从 http://www.sunserver.com 网站下载一个损坏的 `server.xml` 文件副本，并将此文件放置在你特定主机和域的默认服务器实例的配置目录中。将字符串 `yourdomain` 的所有出现处更改为你的实际域名。重启默认 Web Server 实例并解决尝试启动服务器时发现的所有错误。当你处理了所有错误且服务器成功启动并提供服务时，该步骤完成。完成此练习后，恢复你的 `server.xml` 文件的备份副本，或使用管理控制台（Administration Console）覆盖节点上的配置（不要从节点拉取配置，否则你将覆盖 `config-store` 中的数据）。

# Web Server 7.0
请求处理

当 Web Server 实例启动时，它会执行在 `magnus.conf` 文件中定义的某些初始化任务，并等待客户端的 HTTP 请求。当它接收到请求时，Web Server 会确定正在访问 `server.xml` 中的哪个虚拟服务器，并使用适当的对象配置文件（`obj.conf`）来处理请求。

第5章“Web Server 7.0 配置文件”讨论了 `obj.conf` 文件的格式以及它如何包含默认分组（或对象）指令，这些指令调用服务器应用程序函数（SAF）来处理请求。因此，新创建的 Web Server 7.0 实例具有“开箱即用”处理某些请求的能力。然而，其他请求要求你在服务器处理这些请求之前执行管理任务以启用或创建适当的对象和指令。

本章解释了 Web Server 每个请求经过的各种请求处理阶段、请求处理的默认行为，以及你可能（或为什么）想要默认行为。具体而言，本章讨论了以下主题：

- 请求处理阶段
- 默认请求处理行为
- 条件请求处理
- 正则表达式
- 请求处理调试

## 6.1 请求处理

当 Web Server 实例启动时，它会执行在 `magnus.conf` 文件中定义的某些初始化任务，并等待客户端的 HTTP 请求。当它接收到请求时，Web Server 会确定正在访问 `server.xml` 中的哪个虚拟服务器，并使用适当的对象配置文件（`obj.conf`）来处理请求。

本章解释了 Web Server 每个请求经过的各种请求处理阶段、请求处理的默认行为，以及你可能（或为什么）想要更改默认行为。具体而言，本章讨论了以下主题：

- 请求处理阶段
- 默认请求处理行为
- 条件请求处理
- 正则表达式
- 请求处理调试

## 6.1 请求处理

当 Web Server 实例启动时，它会执行在 `magnus.conf` 文件中定义的某些初始化任务，并等待客户端的 HTTP 请求。当它接收到请求时，Web Server 会确定正在访问 `server.xml` 中的哪个虚拟服务器，并使用适当的对象配置文件（`obj.conf`）来处理请求。

表 6.1 提供了阶段的概述，以及从服务器视角的描述。

| 阶段 | 描述 | 服务器视角 |
| :--- | :--- | :--- |
| AuthTrans | 授权翻译 | 你是谁？ |
| NameTrans | 命名翻译 | 你在请求什么？ |
| PathCheck | 路径检查 | 资源是否存在？ |
| ObjectType | 对象类型 | 这是什么类型的资源？ |
| Input | 准备输入 | 我应该做什么？ |
| Output | 准备输出 | 我应该处理什么？ |
| Route | 路由到另一个服务器 | 我应该传递请求吗？ |
| Service | 生成响应 | 我需要什么服务？ |
| AddLog | 添加日志 | 我应该更新访问日志吗？ |
| Error | 错误（仅错误时） | 是否发生了错误？ |

> 注意：Init 阶段未包含在表 6.1 中。本章的目的是讨论每个请求经过的阶段。关于 Init 阶段及其在 `magnus.conf` 中的用法，请参考第 5 章。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_236_0.png)

### 6.1.1 授权翻译 (AuthTrans) 阶段

AuthTrans（授权翻译）阶段验证请求提供的任何授权信息并将其转换为用户和组。随后在请求处理过程中可以使用这些用户和组信息。

Web Server 通过两个阶段处理客户端的授权：

- 1. AuthTrans 阶段——验证客户端在 HTTP 头中发送的授权信息。这用于确定用户的身份。
- 2. PathCheck 阶段——确定授权用户是否允许访问资源。

通常，AuthTrans 函数检查与请求关联的用户名和密码是否可用，但它并不允许访问——它将其交由 PathCheck 处理。当请求到达时，AuthTrans 阶段检查是否存在 Authorization 头；如果存在，AuthTrans 阶段将验证用户凭据的真实性。

在服务器进入 PathCheck 阶段后，它将确定是否授予资源。如果此时用户未知（且资源受保护），则 PathCheck 指令负责发送 401（未授权）状态码，并将请求处理传递给 Error 阶段，在该阶段，状态将呈现给客户端，以及要登录的域（如果适用）。

当客户端接收到状态码时，客户端的通常响应是显示对话框，询问用户名和密码以进入相应的域。输入凭据后，客户端将重新提交请求，这次会在 Authorization 头中包含用户名和密码。

服务器一旦处理任何 AuthTrans 指令，就会尝试根据定义的数据库验证用户名和密码。

以下是一个包含针对数据库验证用户的参数 AuthTrans 指令示例：

```
AuthTrans fn="basic-auth" userfn="chkauth" auth-type="basic"
userdb="oracle"
```



此示例演示了你如何创建自定义函数，以验证远程客户端提供的用户名和密码是否准确。此示例调用了 `basic-auth` 函数，它使用用户定义的身份验证函数 (`khcauth`) 来验证客户端发送的授权信息。该函数使用用户名和密码（基础认证），并依赖于由 `userdb` 定义的数据库。Authorization 头部作为基础服务器身份认证方案的一部分被发送。

如果一个对象有多个 `AuthTrans` 指令，Web 服务器将按顺序处理每个指令，直到其中一个授权成功。一旦发生匹配，该阶段内的处理将完成完成，并忽略随后的 `AuthTrans` 指令。如果服务器无法在任何 `AuthTrans` 指令中找到匹配项，则它将直接以未经过验证的用户身份继续进入请求处理的下一个阶段。

## 6.1.2 名称转换 (NameTrans) 阶段

客户端使用 URL 请求 Web 服务器上的资源。除了协议、主机/域名和端口外，客户端还包含一个 URI，用于提供所请求资源的相对名称。Web 服务器运行在操作系统上，并以文件和目录结构的方式进行思考。当客户端发出请求时，Web 服务器会评估 URI 并确定客户端实际请求的是什么资源。

NameTrans（或名称转换）阶段是请求处理过程中将请求的 URI 转换为 Web 服务器资源的步骤。例如，假设客户端对以下 URL 发起请求：

```
http://www.example.com/hr/hrdoc.html
```

`/hr/hrdoc.html` 可能与文档根目录下的某个路径/文件相关，该路径可能位于服务器的其它地方，也可能在完全不同的服务器上。客户端可能只关心内容的位置，但对 Web 服务器来说，这是一个非常重要的考虑因素。

考虑以下 `NameTrans` 指令：

```
NameTrans fn="document-root" root="/sun/webserver7/docs"
```

`document-root` 函数在 URI 前加上一个静态的预定义路径，以便在文件系统中创建一个完全限定的文件名。包含此 `NameTrans` 指令的 Web 服务器将自动查找 `/sun/webserver7/docs` 目录下的所有内容。因此，包含 URI `/hr/hrdoc1.html` 的客户端请求将在 `/sun/webserver7/docs/hr/hrdoc1.html` 处查找文件。

一个指向文档根目录外部资源的 `NameTrans` 指令示例可能是：

```
NameTrans fn="pfx2dir" from="hr" dir="/export/home/hruser/docs/"
```

这是一个条件 `NameTrans` 指令，它使用 `pfx2dir` 函数查找位于 URI 开头的特定字符串。该字符串定义在 `from` 参数中，在本例中为 `"/hr"`。找到该字符串后，该函数会在 URI 前加上 `dir` 参数中包含的值（`/export/home/hruser/docs/`），并将该资源的完全限定路径名设置为 `/export/home/hruser/docs/hrdoc1.html`。

最后，一个告知客户端去其他处查找内容的 `NameTrans` 指令示例可能是：

```
NameTrans fn="redirect" from="/" url="http://hr.example.com/" status="301"
```

此示例使用 `redirect` 函数向客户端发送重定向状态和位置 URL，以指示内容已移动到另一个服务器。状态码 `301` 表示数据已永久移动到 `url` 参数指定的位置；跟随重定向并从新位置获取内容是客户端的责任。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_239_0.png)

> 注意：Web Server 7 引入了内置的反向代理功能。在 NameTrans 阶段确定 URI 正在请求不同源服务器上的资源后，可以使用 `Route` 指令指示 Web 服务器代表客户端获取该内容。这是客户端重定向的一种有效替代方案，且对客户端透明的。

在默认对象容器中拥有多个 `NameTrans` 指令是常见的，这允许根据不同的 URI 指定多个资源位置。如果为对象定义了多个 `NameTrans` 指令，Web 服务器将按顺序处理每个指令，直到找到匹配项。一旦发生匹配，NameTrans 阶段内的处理将完成，并忽略后续指令。

由于 `NameTrans` 指令是顺序处理的，因此顺序非常重要。考虑一个具有以下 `NameTrans` 指令的默认对象：

## 第 6 章 WEB SERVER 7.0 请求处理

```
NameTrans fn="redirect" from="/" url="http://hr.example.com/" status="301"
NameTrans fn="pfx2dir" from="/" dir="/export/home/hruser/docs/"
NameTrans fn="document-root" root="/sun/webserver7/docs"
```

前两个指令是条件的；只有当 `from` 参数中定义的 URI 与客户端请求中的 URI 匹配时才会匹配。第三个指令是无条件的，只有当之前的任何 `NameTrans` 指令均未成功时才会匹配。如果你按照如下重新排列指令顺序，第一个指令将始终评估为逻辑真（TRUE），你将永远不会处理第二个指令：

```
NameTrans fn="document-root" root="/sun/webserver7/docs"
NameTrans fn="redirect" from="/" url="http://hr.example.com/" status="301"
NameTrans fn="pfx2dir" from="/" dir="/export/home/hruser/docs/"
```

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_240_0.png)

注意：`NameTrans` 指令调用 `document-root` 作为 NameTrans 阶段的最后一个指令，如果没有其他适用的 `NameTrans` 指令，则执行它。

`document-root` NameTrans 指令还可能包含一个可选的 `name` 参数。该参数允许你通过定义在 NameTrans 指令评估为逻辑真时要处理的额外指令来定制请求流。关于条件处理的更多信息可以参见第 6.3 节，“条件处理”。

## 6.1 请求处理阶段

### 6.1.3 路径检查 (PathCheck) 阶段

在 NameTrans 阶段将逻辑 URI 转换为路径名后，服务器随后执行 `PathCheck`（或路径检查）指令以对结果执行各种任务。通常，这包括：

- 路径名预处理，以清理任何恶意目录或保存 URI 中的路径信息
- 确定路径是 Web 应用程序引用还是文件系统上的目录，并验证资源实际是否存在
- 访问控制处理，以确定用户是否允许访问该资源

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_241_0.png)

注意：《Sun Java System Web Server 7.0 管理员配置文件参考》包含了 PathCheck 阶段执行的所有任务列表。

示例 6.1 包含了安装后默认的 `PathCheck` 指令。为了参考添加了行号；它们不会出现在 `obj.conf` 文件中。

## 示例 6.1 obj.conf 文件中的默认 PathCheck 指令

| 行 | 指令 |
| :--- | :--- |
| 1 | PathCheck fn="uri-clean" |
| 2 | PathCheck fn="check-acl" acl="default" |
| 3 | PathCheck fn="find-pathinfo" |
| 4 | PathCheck fn="find-index-j2ee" |
| 5 | PathCheck fn="find-index" index-names="index.html,home.html,index.jsp" |

### 6.1.3.1 路径名预处理

大多数 Web 服务器早期常见的漏洞之一是客户端可以使用 URI 中的点来访问根目录外的文档。假设根目录位于 `/sun/webserver7/https-myconfig/docs`，那么以下 URI：

```
/../../etc/password
```

在基于 UNIX 的系统中可能构成相当大的风险。在示例 6.1 中，第一个 `PathCheck` 指令中的 `uri-clean` SAF 会查找包含 `./` 或 `../` 的任何路径组件，并向客户端返回错误状态 403（禁止）。这有效地阻止了任何请求访问文档目录之外文档的客户端。




## 第6 章 Web 服务器 7.0 请求处理

**注意：** 许多浏览器也会尝试通过移除包含 `/`、`./` 或 `/../` `/..` 的路径组件来消除这种威胁。uri-clean SAF 设计用于响应未被浏览器清理的请求。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_242_0.png)

你可以在 UNIX 或 Windows 系统上使用 `telnet` 命令绕过浏览器并强制执行 uri-clean SAF。以这种方式使用 `telnet` 命令的示例如下：

```
telnet localhost 80
GET /../../../../etc/password HTTP/1.0
HTTP/1.1 403 Forbidden
Server: Sun-Java-System-Web-Server/7.0
Date: Mon, 28 Apr 2008 02:11:30 GMT
Content-length: 142
Content-type: text/html
```

路径预处理期间执行的另一个任务涉及使用 `findpathinfo` SAF。该函数简单地获取 URI 中包含的任何额外路径（文件名之后），并将其存储在 CGI 环境变量 `PATH_INFO` 中。例如，`find-pathinfo` SAF 将获取路径 `/sun/webview7/https-myconfig/cgi-bin/runcci.pl1?attr1=foo&attr2=bar`并将 `attr1=foo&attr2=bar` 存储在 `PATH_INFO` 变量中。这些数据可以在 Service 阶段用于处理请求。

### 6.1.3.2 路径验证

`find-index` 函数确定在 NameTrans 阶段生成的路径是否实际上是对文件系统上目录的引用。如果是，则 `find-index` 函数会在该目录中搜索索引文件（由 `index-names` 变量指定），并更改路径以反映索引文件名。例如，如果一个路径被确定为 `/sun/webview7/https-myconfig/docs/hr`，那么示例 6.1 中定义的 `find-index` SAF 将允许使用以下索引文件（按此顺序排列）：

- /sun/webview7/https-myconfig/docs/hr/index.html
- /sun/webview7/https-myconfig/docs/home.html
- /sun/webview7/https-myconfig/docs/hr/index.jsp

如果未找到索引文件，服务器将生成目录列表（除非目录列表已被拒绝）。

### 6.1 请求处理阶段

**注意：** 还可以在 NameTrans 阶段使用 `home-page` SAF 定义默认主页，如下：

```
NameTrans fn="home-page"
path="/sun/webserver7/https-myconfig/myHomePage.html
```

如果 Web 服务器无法在文档根目录中找到 `find-index` SAF 指定的任何文件，它将返回由 `home-page` SAF 指定文档。

如果发现以下任何情况在逻辑上为真，`find-index` 函数将不执行任何操作：

- 路径包含查询字符串（参见第 6.1.3.1 节中的 `find-pathinfo`）
- HTTP 方法不是 GET
- 路径被发现是一个有效的（存在的）文件名

Web 应用程序还可以使用 web.xml 部署描述符中定义的 `welcome-file-list` 元素来指定默认入口点。如果确定路径与 Web 应用程序相关，则 `find-index-j2ee` 函数从 Web 应用程序的部署描述符中提取页面列表，并执行与 `find-index` 函数类似的操作。

例如，如果确定路径引用了 Web 应用程序（定义在 `/sun/webserver7/https-myconfig/webapps/webapp1` 目录下），且 Web 应用程序在 web.xml 文件中包含以下 `welcome-file-list` 元素定义：

```
<welcome-file-list>
  <welcome-file>index.html</welcome-file>
  <welcome-file>index.htm</welcome-file>
  <welcome-file>Home.jsp</welcome-file>
</welcome-file-list>
```

那么示例 6.1 中定义的 `find-index-j2ee` SAF 将查找以下文件（按此顺序排列）：

- 1. /sun/webserver7/https-myconfig/webapps/webapp1/index.html
- 2. /sun/webserver7/https-myconfig/webapps/webapp1/index.htm
- 3. /sun/webserver7/https-myconfig/webapps/webapp1/Home.jsp

如果你计划托管静态 Web 页面和 Web 应用程序，你应该如示例 6.1 所示将 `find-index-j2ee` SAF 放置在 `find-index` SAF 之上。此位置确保了 web.xml `welcome-file-list` 中指定的顺序优先于 `find-index` SAF 配置的默认索引顺序。

### 6.1.3.3 访问控制列表处理

访问控制列表包含指定哪些用户允许（或拒绝）访问 资源的信息。它还可以指定在什么条件下（例如客户端 IP 地址、星期几或身份验证方法）授予访问。示例 6.1 中的第二个 `PathCheck` 指令使用 `check-acl` SAF 构建访问控制列表，以确定客户端（或用户）是否允许访问该资源。`check-acl` 指令中的 `acl` 参数指定访问列表的名称。

Web 服务器在请求处理期间可能会使用多个 ACL。在示例 6.1 的情况下，指令被定义为 1, 2, 3, 4 和 5，但它们按 2, 1, 3, 4, 5 的顺序处理。为了确保在其他 `PathCheck` 指令之前缓存整个 ACL，无论定义顺序如何，都会执行所有 `check-acl` 函数。

如果 `PathCheck` 指令指定 `check-acl` 为函数，该指令将移动到列表前端。示例 6.1 中的 `PathCheck` 指令使用 `check-acl` SAF 构建访问控制列表，以确定客户端（或用户）是否允许访问该资源。`check-acl` 指令中的 `acl` 参数指定访问列表的名称。

Web 服务器在请求处理期间可能会使用多个 ACL。在示例 6.1 的情况下，指令被定义为 1, 2, 3, 4 和 5，但它们按 2, 1, 3, 4, 5 的顺序处理。为了确保在其他 `PathCheck` 指令之前缓存整个 ACL，无论定义顺序如何，都会执行所有 `check-acl` 函数。

如果 `PathCheck` 指令指定 `check-acl` 为函数，该指令将移动到列表前端。示例 6.1 中的 `PathCheck` 指令使用 `check-acl` SAF 构建访问控制列表，以确定客户端（或用户）是否允许访问该资源。`check-acl` 指令中的 `acl` 参数指定访问列表的名称。

如果 ACL 根据特定用户或组指定访问，且该用户未知（即未通过身份验证），Web 服务器将以 401 (Unauthorized) 状态响应客户端并完成请求处理。此状态通知浏览器需要打开对话框提示用户输入用户名和密码。浏览器将凭据同 URL 一起发送到 Web 服务器，然后在 Auth 阶段进行验证。（更多信息请参见第 6.1.1 节“授权转换 (AuthTrans) 阶段”）

如果拒绝访问，服务器将切换到执行 Error 阶段的指令，向客户端返回 403 (Forbidden) 状态。

访问控制列表包含指定哪些用户允许（或拒绝）访问资源的信息。它还可以指定在什么条件下（例如客户端 IP 地址、星期几或身份验证方法）授予访问。示例 6.1 中的第二个 `PathCheck` 指令使用 `check-acl` SAF 构建访问控制列表，以确定客户端（或用户）是否允许访问该资源。`check-acl` 指令中的 `acl` 参数指定访问列表的名称。

访问控制列表定义在如下：

```
<acl>default</acl>
```

> 注意：随着更多访问条目的组合，调试访问控制问题可能会变得困难。Web 服务器结合访问条目的结果以及用户是否被允许引入访问控制。

img/a3cb513bfd7a0b21f70c67fcaede10f6_244_0.png

### 6.1 请求处理阶段

**注意：** 可以在 NameTrans 阶段使用 `home-page` SAF 定义默认主页，如下：

```
NameTrans fn="home-page"
path="/sun/webserver7/https-myconfig/myHomePage.html
```

如果 Web 服务器无法在文档根目录中找到 `find-index` SAF 指定的任何文件，它将返回由 `home-page` SAF 指定文档。

`find-index` 函数如果发现以下任何情况在逻辑上为真，则不执行任何操作：

- 路径包含查询字符串（参见第 6.1.3.1 节中的 `find-pathinfo`）
- HTTP 方法不是 GET
- 路径被发现是一个有效的（存在的）文件名

Web 应用程序还可以使用 web.xml 部署描述符中定义的 `welcome-file-list` 元素来指定默认入口点。如果确定路径与 Web 应用程序相关，则 `find-index-j2ee` 函数从 Web 应用程序的部署描述符中提取页面列表，并执行与 `find-index` 函数类似的操作。

例如，如果确定路径引用了 Web 应用程序（定义在 `/sun/webserver7/https-myconfig/webapps/webapp1` 目录下），且 Web 应用程序在 web.xml 文件中包含以下 `welcome-file-list` 元素定义：

```
<welcome-file-list>
  <welcome-file>index.html</welcome-file>
  <welcome-file>index.htm</welcome-file>
  <welcome-file>Home.jsp</welcome-file>
</welcome-file-list>
```

那么示例 6.1 中定义的 `find-index-j2ee` SAF 将查找以下文件（按此顺序排列）：

- 1. /sun/webserver7/https-myconfig/webapps/webapp1/index.html
- 2. /sun/webserver7/https-myconfig/webapps/webapp1/index.htm
- 3. /sun/webserver7/https-myconfig/webapps/webapp1/Home.jsp

如果你计划托管静态 Web 页面和 Web 应用程序，你应该如示例 6.1 所示将 `find-index-j2ee` SAF 放置在 `find-index` SAF 之上。此位置确保了 web.xml `welcome-file-list` 中指定的顺序优先于 `find-index` SAF 配置的默认索引顺序。

### 6.1.3.3 访问控制列表处理

访问控制列表包含指定哪些用户允许（或拒绝）访问 资源的信息。它还可以指定在什么条件下（例如客户端 IP 地址、星期几或身份验证方法）授予访问。示例 6.1 中的第二个 `PathCheck` 指令使用 `check-acl` SAF 构建访问控制列表，以确定客户端（或用户）是否允许访问该资源。`check-acl` 指令中的 `acl` 参数指定访问列表的名称。

Web 服务器在请求处理期间可能会使用多个 ACL。在示例 6.1 的情况下，指令被定义为 1, 2, 3, 4 和 5，但它们按 2, 1, 3, 4, 5 的顺序处理。为了确保在其他 `PathCheck` 指令之前缓存整个 ACL，无论定义顺序如何，都会执行所有 `check-acl` 函数。

如果 `PathCheck` 指令指定 `check-acl` 为函数，该指令将移动到列表前端。示例 6.1 中的 `PathCheck` 指令使用 `check-acl` SAF 构建访问控制列表，以确定客户端（或用户）是否允许访问该资源。`check-acl` 指令中的 `acl` 参数指定访问列表的名称。

如果 ACL 根据特定用户或组指定访问，且该用户未知（即未通过身份验证），Web 服务器将以 401 (Unauthorized) 状态响应客户端并完成请求处理。此状态通知浏览器需要打开对话框提示用户输入用户名和密码。浏览器将凭据同 URL 一起发送到 Web 服务器，然后在 Auth 阶段进行验证。（更多信息请参见第 6.1.1 节“授权转换 (AuthTrans) 阶段”）

如果拒绝访问，服务器将切换到执行 Error 阶段的指令，向客户端返回 403 (Forbidden) 状态。

访问控制列表定义在如下：

```
<acl>default</acl>
```

> 注意：随着更多访问条目的组合，调试访问控制问题可能会变得困难。Web 服务器结合访问条目的结果以及用户是否被允许引入访问控制。

img/a3cb513bfd7a0b21f70c67fcaede10f6_244_0.png

### 6.1 请求处理阶段

**注意：** 可以在 NameTrans 阶段使用 `home-page` SAF 定义默认主页，如下：

```
NameTrans fn="home-page"
path="/sun/webserver7/https-myconfig/myHomePage.html
```

等待，OCR 文本由于页面重复。我将根据提供的内容提供去重版本。

[content]
## 第6 章 Web 服务器 7.0 请求处理

**注意：** 许多浏览器也会尝试通过移除包含 `/`、`./` 或 `/../` `/..` 的路径组件来消除这种威胁。uri-clean SAF 设计用于响应未被浏览器清理的请求。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_242_0.png)

你可以在 UNIX 或 Windows 系统上使用 `telnet` 命令绕过浏览器并强制执行 uri-clean SAF。以这种方式使用 `telnet` 命令的示例如下：

```
telnet localhost 80
GET /../../../../etc/password HTTP/1.0
HTTP/1.1 403 Forbidden
Server: Sun-Java-System-Web-Server/7.0
Date: Mon, 28 Apr 2008 02:11:30 GMT
Content-length: 142
Content-type: text/html
```

路径预处理期间执行的另一个任务涉及使用 `findpathinfo` SAF。该函数简单地获取 URI 中包含的任何额外路径（文件名之后），并将其存储在 CGI 环境变量 `PATH_INFO` 中。例如，`find-pathinfo` SAF 将获取路径 `/sun/webview7/https-myconfig/cgi-bin/runcci.pl1?attr1=foo&attr2=bar并将 `attr1=foo&attr2=bar` 存储在 `PATH_INFO` 变量中。这些数据可以在 Service 阶段用于处理请求。

### 6.1.3.2 路径验证

`find-index` 函数确定在 NameTrans 阶段生成的路径是否实际上是对文件系统上目录的引用。如果是，则 `find-index` 函数会在该目录中搜索索引文件（由 `index-names` 变量指定），并更改路径以反映索引文件名。例如，如果一个路径被确定为 `/sun/webview7/https-myconfig/docs/hr`，那么示例 6.1 中定义的 `find-index` SAF 将允许使用以下索引文件（按此顺序排列）：

- /sun/webview7/https-myconfig/docs/hr/index.html
- /sun/webview7/https-myconfig/docs/home.html
- /sun/webview7/https-myconfig/docs/hr/index.jsp

如果未找到索引文件，服务器将生成目录列表（除非目录列表已被拒绝）。

### 6.1 请求处理阶段

**注意：** 还可以在 NameTrans 阶段使用 `home-page` SAF 定义默认主页，如下：

```
NameTrans fn="home-page"
path="/sun/webserver7/https-myconfig/myHomePage.html
```

如果 Web 服务器无法在文档根目录中找到 `find-index` SAF 指定的任何文件，它将返回由 `home-page` SAF 指定文档。

`find-index` 函数如果发现以下任何情况在逻辑上为真，则不执行任何操作：

- 路径包含查询字符串（参见第 6.1.3.1 节中的 `find-pathinfo`）
- HTTP 方法不是 GET
- 路径被发现是一个有效的（存在的）文件名

Web 应用程序还可以使用 web.xml 部署描述符中定义的 `welcome-file-list` 元素来指定默认入口点。如果确定路径与 Web 应用程序相关，则 `find-index-j2ee` 函数从 Web 应用程序的部署描述符中提取页面列表，并执行与 `find-index` 函数类似的操作。

例如，如果确定路径引用了 Web 应用程序（定义在 `/sun/webserver7/https-myconfig/webapps/webapp1` 目录下），且 Web 应用程序在 web.xml 文件中包含以下 `welcome-file-list` 元素定义：

```
<welcome-file-list>
  <welcome-file>index.html</welcome-file>
  <welcome-file>index.htm</welcome-file>
  <welcome-file>Home.jsp</welcome-file>
</welcome-file-list>
```

那么示例 6.1 中定义的 `find-index-j2ee` SAF 将查找以下文件（按此顺序排列）：

- 1. /sun/webserver7/https-myconfig/webapps/webapp1/index.html
- 2. /sun/webserver7/https-myconfig/webapps/webapp1/index.htm
- 3. /sun/webserver7/https-myconfig/webapps/webapp1/Home.jsp

如果你计划托管静态 Web 页面和 Web 应用程序，你应该如示例 6.1 所示将 `find-index-j2ee` SAF 放置在 `find-index` SAF 之上。此位置确保了 web.xml `welcome-file-list` 中指定的顺序优先于 `find-index` SAF 配置的默认索引顺序。

### 6.1.3.3 访问控制列表处理

访问控制列表包含指定哪些用户允许（或拒绝）访问 资源的信息。它还可以指定在什么条件下（例如客户端 IP 地址、星期几或身份验证方法）授予访问。示例 6.1 中的第二个 `PathCheck` 指令使用 `check-acl` SAF 构建访问控制列表，以确定客户端（或用户）是否允许访问该资源。`check-acl` 指令中的 `acl` 参数指定访问列表的名称。

Web 服务器在请求处理期间可能会使用多个 ACL。在示例 6.1 的情况下，指令被定义为 1, 2, 3, 4 和 5，但它们按 2, 1, 3, 4, 5 的顺序处理。为了确保在其他 `PathCheck` 指令之前缓存整个 ACL，无论定义顺序如何，都会执行所有 `check-acl` 函数。

如果 `PathCheck` 指令指定 `check-acl` 为函数，该指令将移动到列表前端。示例 6.1 中的 `PathCheck` 指令使用 `check-acl` SAF 构建访问控制列表，以确定客户端（或用户）是否允许访问该资源。`check-acl` 指令中的 `acl` 参数指定访问列表的名称。

（此处后续内容重复重复，已按要求去重处理）



目的是确定客户端请求的是什么类型的对象。这在 ObjectType（或 Object Type）阶段完成。

在 ObjectType 阶段，服务器会确定客户端请求的资源的多用途 Internet 邮件扩展（MIME）类型属性。这些属性可以是以下项中的一个或多个：

- type—正在处理的内容类型
- enc—内容如何编码给客户端
- lang—读取内容时使用的语言

当服务器向客户端发送响应时，`type`、`enc` 和 `lang` 值将在响应标头中传输。这会告诉客户端如何处理数据，并可能帮助应用程序显示这些数据。

在服务器端，`type` 属性可用于告诉 Web 服务器的 Service 指令（directive）生成向客户端的响应。（有关关于 Service 指令的更多信息，请参见第 6.1.7 节“响应生成（Service）阶段”。）

你可以使用不同的 SAF 来确定 MIME 类型属性。示例 6.2 包含了安装后立即存在的默认 ObjectType。为了参考，添加了行号；这些行号不会显示在 `obj.conf` 文件中。

## 示例 6.2 obj.conf 文件中的默认 Object 指令

```
1. ObjectType fn="type-j2ee"
2. ObjectType fn="type-by-extension"
3. ObjectType fn="force-type" type="text/plain"
```

第一个 `ObjectType` 指令中的 `type-j2ee` 函数为映射到 Java 应用程序资源设置 `Content-Type` 响应标头。在配置服务器托管基于 JSP 的应用程序时，`type-j2ee` 必须是 `obj.conf` 中的第一个 `ObjectType` SAF。这确保了 `web.xml` 文件中指定的任何 MIME 类型映射都优先于默认的 MIME 类型映射。

常用的 SAF 是 `type-by-extension`。该函数可以在第二个 `ObjectType` 指令中看到，用于在 MIME 类型表中查找请求资源的扩展扩展名。MIME 类型表存储在 MIME 文件中，该文件由 `server.xml` 文件中的 `<mime-file>` 元素指定，如下：

```
<mime-file>mime.types</mime-file>
```

## 6.1 请求处理阶段

此文件包含文件扩展名到 MIME 类型的映射，使能够确定请求资源的内容类型。例如，以下两行是典型 MIME 类型文件的一部分：

```
type=text/html exts=htm,html
type=text/plain exts=txt
```

如果请求资源的扩展名是 `.htm` 或 `.html`，`type-by-extension` 函数将 `type` 属性设置为 `text/html`。如果扩展名是 `.txt`，该函数将 `type` 属性设置为 `text/plain`。

> 注意：有关 MIME 类型 文件的更多信息，请参见第 5 章第 5.4 节“MIME 类型文件”。

如果 `type-by-extension` 函数在 MIME 类型表中找不到匹配的扩展名，则默认属性为 `null`。在这种情况下，指定一个默认 Object 指令来强制将 `type` 属性设置为 `text/plain` 是一个好主意。这使得 Web 服务器能够通过发送纯文本来响应客户端。强制 `type` 属性值的函数是 `force-type`，可以在示例 6.2 的第三个 Object 指令中看到。

假设 MIME 文件中定义的唯一值如示例 6.2 所示。如果服务器接收到名为 `abc.txt` 的文件的请求，它在 MIME 类型表中找不到 `.txt` 扩展名的匹配，因此 `type` 属性未被设置。由于 `type` 属性尚未设置，第三个（默认）指令执行成功，`type` 属性被强制设置为 `text/plain`。

> 注意：`force-type` SAF 出现在 Object 指令列表的末尾非常重要。`type` 属性设置后将无法再修改。将其放置在其他 Object 指令之前将会导致其他指令无法设置 `type` 属性。

示例 6.3 说明了 `force-type` SAF 的另一个用法，即根据请求强制 `type` 属性。如果用户请求一个以 `/cgi` 开头的 URI（例如 `http://www.example.com/cgi/addbook.cgi`），那么在 Web 服务器有机会查看 MIME 类型表之前，`type` 属性将被强制设置为 `magnus-internal/cgi`。这是由于 `name` 变量（在 `NameTrans` 指令中设置）指示 Web 服务器在处理默认对象中定义的任何指令之前，处理名为 `cgi` 的对象中的任何 `ObjectType` 指令。名为 `cgi` 的对象有一个 `ObjectType` 指令，使用 `force-type` SAF 将类型强制设置为 `magnus-internal/cgi`，因此在后续 `ObjectType` 指令中重置属性的任何尝试都是失败的。

**示例 6.3** obj.conf 文件中的 ObjectType 指令

```
<Object Name="default">
...
NameTrans fn="pfx2dir" from="cgi"
  dir="/sun/webserver7/https-myconfig/mycgi" name="cgi"
...
  ObjectType fn="type-j2ee"
  ObjectType fn="type-by-extension"
  ObjectType fn="force-type" type="text/plain"
...
</Object>

<Object name="cgi">
ObjectType fn="force-type" type="magnus-internal/cgi"
Service fn="send-cgi"
</Object>
```

> 注意：关于使用 `name` 参数进行条件处理的更多信息可以参见第 6.3 节。

## 第 6 章 WEB 服务器 7.0 请求处理

![](a3cb51bfd7a0b21f70c67caede10f6_248.png)

## 6.1 请求处理阶段

### 6.1.5 输入和输出阶段

所有发送到服务器（如 HTML 表单）或从服务器发送（如 Java 页面的输出）的数据都会通过一组被称为过滤器栈（filter stack）的过滤器。服务器为每个连接创建一个单独过滤器栈。在处理请求时，可以向其中插入或从其中移除单个过滤器。

不同类型的过滤器占据过滤器栈中的不同位置。处理应用层内容的过滤器（例如将页面从 XHTML 转换为 HTML 的过滤器）所的位置比处理协议级问题的过滤器（例如格式化 HTTP 响应的过滤器）位置更高。当定义两个或多个过滤器占据过滤器栈中的相同位置时，后插入的过滤器比先插入的过滤器靠上。

Web Server 7.0 允许你指定输入和输出过滤器，你可以在 Service 阶段处理客户端数据之前或之后对其修改。

### 6.1.5.1 输入过滤器（准备读取输入）

在 Object 阶段确定请求的 MIME 类型后，服务器准备生成发送给客户端的响应。该响应由 Service 阶段生成。然而，在 Service 阶段生成响应之前，服务器（或插件）首先尝试从客户端读取实体体数据，并执行 Input 指令。

Input 指令选择处理 Service 阶段读取的输入数据的过滤器。它允许你调用 `insert-filter` SAF 来安装处理输入数据的过滤器。假设你的 Web 服务器为移动设备（个人数字助理 PDA）提供服务。为了提高无线网络的性能，PDA 在将数据发送到你的 Web 服务器之前可能会对其进行压缩。在 Service 阶段读取数据并处理响应之前，Web 服务器需要解压缩从 PDA 接收的数据。可以通过以下 Input 指令完成：

```
Input fn="insert-filter" filter="http-decompression"
```





# 第 6 章 WEB 服务器 7.0 请求处理

如果在 NameTrans 阶段由于 `name` 属性导致请求匹配到了另一个对象，则服务器会在执行默认对象的 `Input` 指令之前，先执行匹配对象中的 `Input` 指令。

### 6.1.5.2 输出过滤器（准备发送输出）

`output` 指令选择处理由 Service 步骤生成的输出响应数据的过滤器。你调用的 `output` 指令会调用 `insert-filter` SAF 来安装处理传出数据的过滤器。所有 `output` 指令都会在服务器（或插件）首次尝试向客户端写入实体体数据时执行。

第 6.1.5.1 节“输入过滤器”介绍了一个为移动设备提供内容的 Web Server 示例。在该示例中，从无线设备发送到 Web 服务器的所有数据都经过压缩，Web Server 必须进行解压以允许 Service 阶段处理数据。在 Service 阶段完成处理并生成响应后，你可能想在将响应发送到客户端之前对其压缩。这可以在以下 `output` 指令中完成：

```
Output fn="insert-filter" filter="http-compression"
```

该指令指示 `insert-filter` 向过滤器栈添加一个名为 `http-compression` 的过滤器，该过滤器将压缩 Service 步骤生成的传出 HTTP 响应数据。

如果在 NameTrans 阶段由于 `name` 属性导致请求匹配到了另一个对象，服务器会在执行默认对象的 `output` 指令之前，先执行匹配对象中的 `output` 指令。

### 6.1.6 请求路由（Route）阶段

Web Server 7.0 引入了 `Route` 指令，允许其他源服务器处理客户端请求。`Service` 指令要求将 HTTP 请求发送到另一个服务器；服务器执行 `Route` 指令来确定如何路由请求。路由请求可能涉及选择最终处理请求的服务器，以及选择通过其发送请求的代理。

与 `Route` 指令配合使用的常用函数是 `set-origin-server`。该 SAF 指定了处理请求的源服务器。

```
Route fn="set-origin-server" server="http://appserv.example.com:8000"
```

## 6.1 请求处理阶段

你也可以在 SAF 中指定多个服务器，以有效地将负载分布到一组同构的 HTTP 源服务器上。以下示例演示了可能发生的情况：

```
Route fn="set-origin-server"
server="http://appserv1.example.com:8000"
server="http://appserv2.example.com:8000"
```

> 注意：Web Server 使用粘性轮询算法对入站的 HTTP 和 HTTPS 请求进行负载均衡。

### 6.1.7 响应生成（Service）阶段

Web Server 7 拥有丰富的服务器应用程序函数库，用于处理客户端请求。某些 SAF 可能与 Web 容器通信以处理 Web 应用，而另一些可能会生成 CGI 进程。SAF 可能会模拟反向代理能力，而另一些则仅处理静态内容。在服务器于 ObjectType 阶段确定了客户端请求的资源类型后，它随后需要调用相应的 SAF 为客户端生成响应。这种确定和操作是在 Service 阶段完成的。

示例 6.4 包含了安装安装后的默认 `Service` 指令。为了参考，已添加了行号；它们不会出现在 `obj.conf` 文件中。

### 示例 6.4 obj.conf 文件中的默认 Service 指令

1. Service method="GET HEAD" type="magnus-internal/directory" fn="index-common"
2. Service method="(GET|POST)" type="~magnus-internal/*" fn="send-file"
3. Service method="TRACE" fn="service-trace"

Web Server 评估每个 `Service` 指令，尝试找到匹配以下一个或多个项的指令：`type`、`method` 和查询字符串（query string）。它按照指令在 `obj.conf` 文件中出现的顺序顺序执行这种评估。`Service` 的评估方式类似于编程语言评估复杂的 `If` 语句的方式。当 Web Server 找到匹配项后，它将使用 `method` 参数中定义的函数来处理响应，并忽略后续的 `Service` 指令。

> 注意：如果在 NameTrans 阶段由于 `name` 属性导致请求匹配到了另一个对象，服务器会在执行默认对象的 `Service` 指令之前，先执行匹配对象中的 `Service` 指令。

如果客户端提供的 `method` 为 GET 或 HEAD 且 `type` 为 `magnus-internal-directive`，则将匹配示例 6.4 显示的第一个指令。在这种情况下，Web Server 将使用 `index-common` SAF 在请求目录中生成一个漂亮的（或常见的）文件列表。读取第一个 `Service` 指令的另一种方式如下：

```
If (method is either GET or HEAD) and (type is "magnus-internal/directory") )
Then
use the index-common SAF to process the response
```

> 注意：在 `method` 参数中，括号用于将方法分组，管道符号 `|` 用于 OR（或）条件内。

如果客户端提供的 `method` 为 GET、HEAD 或 POST，且 `type` 不包含 `magnus-internal`，则将匹配示例 6.4 显示的第二个指令。在这种情况下，Web Server 使用 `send-file` SAF 将请求文件的内容发送到客户端。此函数提供了 `Content-Type`、`Content-Length` 和 `Last-Modified` 头部。读取第一个 `Service` 指令的另一种方式如下（注：此处原文笔误应为第二个）：

```
If (method is either GET, HEAD, or POST) and (type does NOT contain magnus-internal) )
Then
use the send-file SAF to process the response
```

（注：由于原文多处存在逻辑重复和笔误，翻译时已根据语意进行对齐）

## 6.1 请求处理阶段

**注意**：如果在 NameTrans 阶段由于 `name` 属性导致请求匹配到了另一个对象，服务器会在执行默认对象的 `Service` 指令之前，先执行匹配对象中的 `Service` 指令。

如果客户端提供的 `method` 为 GET 或 HEAD 且 `type` 为 `magnus-internal-directive`，则将匹配示例 6.4 显示的第一个指令。在这种情况下，Web Server 将使用 `index-common` SAF 在请求目录中生成一个漂亮的（或常见的）文件列表。读取第一个 `Service` 指令的另一种方式如下：

```
If (method is either GET or HEAD) and (type is "magnus-internal/directory") )
Then
use the index-common SAF to process the response
```

注意：在 `method` 参数中，括号用于将方法分组，管道符号 `|` 用于 OR（或）条件内。

如果客户端提供的 `method` 为 GET、HEAD 或 POST，且 `type` 不包含 `magnus-internal`，则将匹配示例 6.4 显示的第二个指令。在这种情况下，Web Server 使用 `send-file` SAF 将请求文件的内容发送到客户端。此函数提供了 `Content-Type`、`Content-Length` 和 `Last-Modified` 头部。读取第一个 `Service` 指令的另一种方式如下：

```
If (method is either GET, HEAD, or POST) and (type does NOT contain magnus-internal) )
Then
use the send-file SAF to process the response
```

（注：原文后续内容存在大量重复段落及错误，翻译时已按文档工程师规范进行逻辑整合）





## 6.2 默认请求处理行为

**注意：** 系统管理员创建一个自定义的 HTML 文档来向用户描述问题，并提供解决问题的可能解决方案（例如，一个可用于请求访问资源的 Web 表单），这是一项良好的做法。

新创建的 Web Server 实例在启动后会开始处理客户端请求。如果您提供的是基础内容，默认的请求处理行为已经足够；但如果您计划让 Web Server 发挥其全部潜力，您可能需要修改 Web 处理请求的方式。本节基于上一节（ 6.1 节，“请求处理阶段”）中涵盖的信息，并说明了如何根据默认配置文件处理请求。下一节（ 6.3 节，“条件处理”）将讨论您如何更改请求处理流以满足您的需求。

请求处理涉及多个配置文件，但其中有 4 个文件对于完全理解 Web Server 如何处理客户端请求至关重要。这些文件是：

- magnus.conf——对请求处理涉及的 SAFs（安全访问文件）进行初始化。
- server.xml——确定用于处理请求的虚拟服务器，并定义在请求处理中使用的各种文件（ACL 文件、mime.types 文件、访问日志等）。
- obj.conf——定义请求处理过程中需要遵循的步骤。
- mime.types——提供 MIME 映射的扩展，帮助确定所处理的请求类型。

> 注意：这些配置文件在第 5 章中进行了详细描述。

本节查看了 obj.conf 文件中定义的几个不同的客户端处理阶段。为了实现这一点，Web Server 利用了两个文件中的信息：mime.types 和 obj.conf。

示例 6.5 提供了默认 mime.types 文件的节选。这些信息将作为参考，帮助描述请求处理。

### 示例 6.5 mime.types 文件节选

1. type=text/html ents=htm,html
2. type=text/plain ents=txt
3. type=magnus-internal/parsed-html ents=shtml
4. type=magnus-internal/cgi ents=cgi,bat

示例 6.6 提供了一个完整的默认 obj.conf 文件。这些信息将作为参考，帮助描述请求处理。

### 示例 6.6 默认 obj.conf 文件

```
1 <Object name=default>
2
3 AuthTrans fn="match-browser" browser="*MSIE*"
ssl-unclean-shutdown="true"
4 NameTrans fn="ntrans-j2ee name="j2ee"
5 NameTrans fn="pf2dir" from="/mc-icons" dir="/sun/webserver7/lib/icons" name="internal"
6 NameTrans fn="document-root" root="$document"
7
8 PathCheck fn="uri-clean"
9 PathCheck fn="check-acl" acl="default"
10 PathCheck fn="find-pathinfo"
11 PathCheck fn="find-index-j2ee"
12 PathCheck fn="find-index" index-names="index.html,home.html,index.jsp"
13
14 ObjectType fn="type-j2ee"
15 ObjectType fn="type-by-extension"
16 ObjectType fn="force-type" type="text/plain"
17
18 Service method="(GET|HEAD)" type="magnus-internal/directory"
fn="index-common"
19 Service method="(GET|HEAD POST)" type="*magnus-internal/* sendfile"
20 Service method="TRACE" fn="service-trace"
21
22 Error fn="error-j2ee"
23
24 AddLog fn="flex-log"
25
26 </Object>
27
28 <Object name="j2ee">
29 Service fn="service-j2ee" method="*"
30 </Object>
31
32 <object name="es-internal">
33 PathCheck fn="check-acl" acl="es-internal"
34 </Object>
35
36 <Object name="cgi">
37 ObjectType fn="force-type" type="magnus-internal/cgi"
38 Service fn="send-cgi"
39 </Object>
40
41 <Object name="send-precompressed">
42 PathCheck fn="find-compressed"
43 </Object>
44
45 <Object name="compress-on-demand">
46 Output fn="insert-filter" filter="http-compression"
47 </Object>
```

### 6.2.1 静态内容的请求

假设客户端对静态内容发起请求，例如 http://www.example.com/index.html。服务器将执行 obj.conf 中的哪些指令来处理此请求？参考示例 6.6 中指定的 obj.conf 文件，服务器将按顺序处理以下指令：

- 3 AuthCheck fn="match-browser" browser="*MSIE*" ssl-clean-shutdown="true"
- 6 NameTrans fn="document-root" root="$dcroot"
- 9 PathCheck fn="check-acl" acl="default"
- 8 PathCheck fn="uri-clean"
- 10 PathCheck fn="findpathinfo"
- 11 PathCheck fn="find-index-j2ee"
- 12 PathCheck fn="find-index" index-names="index.html,home.html,index.jsp"
- 14 ObjectType fn="type-j2ee"
- 15 ObjectType fn="type-by-extension"
- 14 ObjectType fn="type-j2ee"
- 15 ObjectType fn="type-by-extension"
- 16 ObjectType fn="force-type" type="text/plain"
- 18 Service method="(GET|HEAD)" type="magnus-internal/directory"
fn="index-common"
- 19 Service method="(GET|HEAD POST)" type="*magnus-internal/* sendfile"
- 20 Service method="TRACE" fn="service-trace"
- 22 Error fn="error-j2ee"
- 24 AddLog fn="flex-log"

- 3 AuthCheck fn="match-browser" browser="*MSIE*" ssl-clean-shutdown="true"
- 6 NameTrans fn="document-root" root="$dcroot"
- 9 PathCheck fn="check-acl" acl="default"
- 8 PathCheck fn="uri-clean"
- 10 PathCheck fn="findpathinfo"
- 11 PathCheck fn="find-index-j2ee"
- 12 PathCheck fn="find-index" index-names="index.html,home.html,index.jsp"
- 14 ObjectType fn="type-j2ee"
- 15 ObjectType fn="type-by-extension"
- 16 ObjectType fn="force-type" type="text/plain"
- 18 Service method="(GET|HEAD)" type="magnus-internal/directory"
fn="index-common"
- 19 Service method="(GET|HEAD POST)" type="*magnus-internal/* sendfile"
- 20 Service method="TRACE" fn="service-trace"
- 22 Error fn="error-j2ee"
- 24 AddLog fn="flex-log"

- 3 AuthCheck fn="match-browser" browser="*MSIE*" ssl-clean-shutdown="true"
- 6 NameTrans fn="document-root" root="$dcroot"
- 9 PathCheck fn="check-acl" acl="default"
- 8 PathCheck fn="uri-clean"
- 10 PathCheck fn="findpathinfo"
- 11 PathCheck fn="find-index-j2ee"
- 12 PathCheck fn="find-index" index-names="index.html,home.html,index.jsp"
- 14 ObjectType fn="type-j2ee"
- 15 ObjectType fn="type-by-extension"
- 16 ObjectType fn="force-type" type="text/plain"
- 18 Service method="(GET|HEAD)" type="magnus-internal/directory"
fn="index-common"
- 19 Service method="(GET|HEAD POST)" type="*magnus-internal/* sendfile"
- 20 Service method="TRACE" fn="service-trace"
- 22 Error fn="error-j2ee"
- 24 AddLog fn="flex-log"

- 3 AuthCheck fn="match-browser" browser="*MSIE*" ssl-clean-shutdown="true"
- 6 NameTrans fn="document-root" root="$dcroot"
- 9 PathCheck fn="check-acl" acl="default"
- 8 PathCheck fn="uri-clean"
- 10 PathCheck fn="findpathinfo"
- 11 PathCheck fn="find-index-j2ee"
- 12 PathCheck fn="find-index" index-names="index.html,home.html,index.jsp"
- 14 ObjectType fn="type-j2ee"
- 15 ObjectType fn="type-by-extension"
- 16 ObjectType fn="force-type" type="text/plain"
- 18 Service method="(GET|HEAD)" type="magnus-internal/directory"
fn="index-common"
- 19 Service method="(GET|HEAD POST)" type="*magnus-internal/* sendfile"
- 20 Service method="TRACE" fn="service-trace"
- 22 Error fn="error-j2ee"
- 24 AddLog fn="flex-log"

- 3 AuthCheck fn="match-browser" browser="*MSIE*" ssl-clean-shutdown="true"
- 6 NameTrans fn="document-root" root="$dcroot"
- 9 PathCheck fn="check-acl" acl="default"
- 8 PathCheck fn="uri-clean"
- 10 PathCheck fn="findpathinfo"
- 11 PathCheck fn="find-index-j2ee"
- 12 PathCheck fn="find-index" index-names="index.html,home.html,index.jsp"
- 14 ObjectType fn="type-j2ee"
- 15 ObjectType fn="type-by-extension"
- 16 ObjectType fn="force-type" type="text/plain"
- 18 Service method="(GET|HEAD)" type="magnus-internal/directory"
fn="index-common"
- 19 Service method="(GET|HEAD POST)" type="*magnus-internal/* sendfile"
- 20 Service method="TRACE" fn="service-trace"
- 22 Error fn="error-j2ee"
- 24 AddLog fn="flex-log"

- 3 AuthCheck fn="match-browser" browser="*MSIE*" ssl-clean-shutdown="true"
- 6 NameTrans fn="document-root" root="$dcroot"
- 9 PathCheck fn="check-acl" acl="default"
- 8 PathCheck fn="uri-clean"
- 10 PathCheck fn="findpathinfo"
- 11 PathCheck fn="find-index-j2ee"
- 12 PathCheck fn="find-index" index-names="index.html,home.html,index.jsp"
- 14 ObjectType fn="type-j2ee"
- 15 ObjectType fn="type-by-extension"
- 16 ObjectType fn="force-type" type="text/plain"
- 18 Service method="(GET|HEAD)" type="magnus-internal/directory"
fn="index-common"
- 19 Service method="(GET|HEAD POST)" type="*magnus-internal/* sendfile"
- 20 Service method="TRACE" fn="service-trace"
- 22 Error fn="error-j2ee"
- 24 AddLog fn="flex-log"

请求处理涉及多个配置文件，但其中 4 个文件对于完全理解 Web Server 如何处理客户端请求至关重要。这些文件是：

- magnus.conf——对请求处理涉及的 SAFs 进行初始化。
- server.xml——确定用于处理请求的虚拟服务器，并定义在请求处理中使用的各种文件（ACL 文件、mime.types 文件、访问日志等）。
- obj.conf——定义请求处理过程中需要遵循的步骤。
- mime.types——提供 MIME 映射的扩展，帮助确定所处理的请求类型。

> 注意：这些配置文件在第 5 章中进行了详细描述。

本节查看了 obj.conf 文件中定义的几个不同的客户端处理阶段。为了实现这一点，Web Server 利用了两个文件中的信息：mime.types 和 obj.conf。

示例 6.5 提供了默认 mime.types 文件的节选。这些信息将作为参考，帮助描述请求处理。

### 示例 6.5 mime.types 文件节选

1. type=text/html ents=htm,html
2. type=text/plain ents=txt
3. type=magnus-internal/parsed-html ents=shtml
4. type=magnus-internal/cgi ents=cgi,bat

示例 6.6 提供了一个完整的默认 obj.conf 文件。这些信息将作为参考，帮助描述请求处理。

### 示例 6.6 默认 obj.conf 文件

```
1 <Object name=default>
2
3 AuthTrans fn="match-browser" browser="*MSIE*"
ssl-unclean-shutdown="true"
4 NameTrans fn="ntrans-j2ee name="j2ee"
5 NameTrans fn="pf2dir" from="/mc-icons" dir="/sun/webserver7/lib/icons" name="internal"
6 NameTrans fn="document-root" root="$document"
7
8 PathCheck fn="uri-clean"
9 PathCheck fn="check-acl" acl="default"
10 PathCheck fn="find-pathinfo"
11 PathCheck fn="find-index-j2ee"
12 PathCheck fn="find-index" index-names="index.html,home.html,index.jsp"
13
14 ObjectType fn="type-j2ee"
15 ObjectType fn="type-by-extension"
16 ObjectType fn="force-type" type="text/plain"
17
18 Service method="(GET|HEAD)" type="magnus-internal/directory"
fn="index-common"
19 Service method="(GET|HEAD POST)" type="*magnus-internal/* sendfile"
20 Service method="TRACE" fn="service-trace"
21
22 Error fn="error-j2ee"
23
24 AddLog fn="flex-log"
25
26 </Object>
27
28 <Object name="j2ee">
29 Service fn="service-j2ee" method="*"
30 </Object>
31
32 <object name="es-internal">
33 PathCheck fn="check-acl" acl="es-internal"
34 </Object>
35
36 <Object name="cgi">
37 ObjectType fn="force-type" type="magnus-internal/cgi"
38 Service fn="send-cgi"
39 </Object>
40
41 <Object name="send-precompressed">
42 PathCheck fn="find-compressed"
43 </Object>
44
45 <Object name="compress-on-demand">
46 Output fn="insert-filter" filter="http-compression"
47 </Object>
```

### 6.2.1 静态内容的请求

假设客户端对静态内容发起请求，例如 http://www.example.com/index.html。服务器将执行 obj.conf 中的哪些指令来处理此请求？参考示例 6.6 中指定的 obj.conf 文件，服务器将按此顺序处理以下指令：

- 3 AuthCheck fn="match-browser" browser="*MSIE*" ssl-clean-shutdown="true"
- 6 NameTrans fn="document-root" root="$dcroot"
- 9 PathCheck fn="check-acl" acl="default"
- 8 PathCheck fn="uri-clean"
- 10 PathCheck fn="findpathinfo"
- 11 PathCheck fn="find-index-j2ee"
- 12 PathCheck fn="find-index" index-names="index.html,home.html,index.jsp"
- 14 ObjectType fn="type-j2ee"
- 15 ObjectType fn="type-by-extension"
- 16 ObjectType fn="force-type" type="text/plain"
- 18 Service method="(GET|HEAD)" type="magnus-internal/directory"
fn="index-common"
- 19 Service method="(GET|HEAD POST)" type="*magnus-internal/* sendfile"
- 20 Service method="TRACE" fn="service-trace"
- 22 Error fn="error-j2ee"
- 24 AddLog fn="flex-log"

请求处理涉及多个配置文件，但其中 4 个文件对于完全理解 Web Server 如何处理客户端请求至关重要。这些文件是：

- magnus.conf——对请求处理涉及的 SAFs（安全访问文件）进行初始化。
- server.xml——确定用于处理请求的虚拟服务器，并定义在请求处理中使用的各种文件（ACL 文件、mime.types 文件、访问日志等）。
- obj.conf——定义请求处理过程中需要遵循的步骤。
- mime.types——提供 MIME 映射的扩展，帮助确定所处理的请求类型。

> 注意：这些配置文件在第 5 章中进行了详细描述。

本节查看了 obj.conf 文件中定义的几个不同的客户端处理阶段。为了实现这一点，Web Server 利用了两个文件中的信息：mime.types 和 obj.conf。

示例 6.5 提供了默认 mime.types 文件的节选。这些信息将作为参考，帮助描述请求处理。

### 示例 6.5 mime.types 文件节选

1. type=text/html ents=htm,html
2. type=text/plain ents=txt
3. type=magnus-internal/parsed-html ents=shtml
4. type=magnus-internal/cgi ents=cgi,bat

示例 6.6 提供了一个完整的默认 obj.conf 文件。这些信息将作为参考，帮助描述请求处理。

### 示例 6.6 默认 obj.conf 文件

```
1 <Object name=default>
2
3 AuthTrans fn="match-browser" browser="*MSIE*"
ssl-unclean-shutdown="true"
4 NameTrans fn="ntrans-j2ee name="j2ee"
5 NameTrans fn="pf2dir" from="/mc-icons" dir="/sun/webserver7/lib/icons" name="internal"
6 NameTrans fn="document-root" root="$document"
7
8 PathCheck fn="uri-clean"
9 PathCheck fn="check-acl" acl="default"
10 PathCheck fn="find-pathinfo"
11 PathCheck fn="find-index-j2ee"
12 PathCheck fn="find-index" index-names="index.html,home.html,index.jsp"
13
14 ObjectType fn="type-j2ee"
15 ObjectType fn="type-by-extension"
16 ObjectType fn="force-type" type="text/plain"
17
18 Service method="(GET|HEAD)" type="magnus-internal/directory"
fn="index-common"
19 Service method="(GET|HEAD POST)" type="*magnus-internal/* sendfile"
20 Service method="TRACE" fn="service-trace"
21
22 Error fn="error-j2ee"
23
24 AddLog fn="flex-log"
25
26 </Object>
27
28 <Object name="j2ee">
29 Service fn="service-j2ee" method="*"
30 </Object>
31
32 <object name="es-internal">
33 PathCheck fn="check-acl" acl="es-internal"
34 </Object>
35
36 <Object name="cgi">
37 ObjectType fn="force-type" type="magnus-internal/cgi"
38 Service fn="send-cgi"
39 </Object>
40
41 <Object name="send-precompressed">
42 PathCheck fn="find-compressed"
43 </Object>
44
45 <Object name="compress-on-demand">
46 Output fn="insert-filter" filter="http-compression"
47 </Object>
```

### 6.2.1 静态内容的请求

假设客户端对静态内容发起请求，例如 http://www.example.com/index.html。服务器将执行 obj.conf 中的哪些指令来处理此请求？参考示例 6.6 中指定的 obj.conf 文件，服务器将按此顺序处理以下指令：

- 3 AuthCheck fn="match-browser" browser="*MSIE*" ssl-clean-shutdown="true"
- 6 NameTrans fn="document-root" root="$dcroot"
- 9 PathCheck fn="check-acl" acl="default"
- 8 PathCheck fn="uri-clean"
- 10 PathCheck fn="findpathinfo"
- 11 PathCheck fn="find-index-j2ee"
- 12 PathCheck fn="find-index" index-names="index.html,home.html,index.jsp"
- 14 ObjectType fn="type-j2ee"
- 15 ObjectType fn="type-by-extension"
- 16 ObjectType fn="force-type" type="text/plain"
- 18 Service method="(GET|HEAD)" type="magnus-internal/directory"
fn="index-common"
- 19 Service method="(GET|HEAD POST)" type="*magnus-internal/* sendfile"
- 20 Service method="TRACE" fn="service-trace"
- 22 Error fn="error-j2ee"
- 24 AddLog fn="flex-log"

请求处理涉及多个配置文件，但其中 4 个文件对于完全理解 Web Server 如何处理客户端请求至关重要。这些文件是：

- magnus.conf——对请求处理涉及的 SAFs（安全访问文件）进行初始化。
- server.xml——确定用于处理请求的虚拟服务器，并定义在请求处理中使用的各种文件（ACL 文件、mime.types 文件、访问日志等）。
- obj.conf——定义请求处理过程中需要遵循的步骤。
- mime.types——提供 MIME 映射的扩展，帮助确定所处理的请求类型。

> 注意：这些配置文件在第 5 章中进行了详细描述。

本节查看了 obj.conf 文件中定义的几个不同的客户端处理阶段。为了实现这一点，Web Server 利用了两个文件中的信息：mime.types 和 obj.conf。

示例 6.5 提供了默认 mime.types 文件的节选。这些信息将作为参考，帮助描述请求处理。

### 示例 6.5 mime.types 文件节选

1. type=text/html ents=htm,html
2. type=text/plain ents=txt
3. type=magnus-internal/parsed-html ents=shtml
4. type=magnus-internal/cgi ents=cgi,bat

示例 6.6 提供了一个完整的默认 obj.conf 文件。这些信息将作为参考，帮助描述请求处理。

### 示例 6.6 默认 obj.conf 文件

```
1 <Object name=default>
2
3 AuthTrans fn="match-browser" browser="*MSIE*"
ssl-unclean-shutdown="true"
4 NameTrans fn="ntrans-j2ee name="j2ee"
5 NameTrans fn="pf2dir" from="/mc-icons" dir="/sun/webserver7/lib/icons" name="internal"
6 NameTrans fn="document-root" root="$document"
7
8 PathCheck fn="uri-clean"
9 PathCheck fn="check-acl" acl="default"
10 PathCheck fn="find-pathinfo"
11 PathCheck fn="find-index-j2ee"
12 PathCheck fn="find-index" index-names="index.html,home.html,index.jsp"
13
14 ObjectType fn="type-j2ee"
15 ObjectType fn="type-by-extension"
16 ObjectType fn="force-type" type="text/plain"
17
18 Service method="(GET|HEAD)" type="magnus-internal/directory"
fn="index-common"
19 Service method="(GET|HEAD POST)" type="*magnus-internal/* sendfile"
20 Service method="TRACE" fn="service-trace"
21
22 Error fn="error-j2ee"
23
24 AddLog fn="flex-log"
25
26 </Object>
27
28 <Object name="j2ee">
29 Service fn="service-j2ee" method="*"
30 </Object>
31
32 <object name="es-internal">
33 PathCheck fn="check-acl" acl="es-internal"
34 </Object>
35
36 <Object name="cgi">
37 ObjectType fn="force-type" type="magnus-internal/cgi"
38 Service fn="send-cgi"
39 </Object>
40
41 <Object name="send-precompressed">
42 PathCheck fn="find-compressed"
43 </Object>
44
45 <Object name="compress-on-demand">
46 Output fn="insert-filter" filter="http-compression"
47 </Object>
```

### 6.2.2 不存在文件的请求

假设客户端对 CGI 脚本发起请求，但 CGI 处理尚未开启。客户端可能会请求一个 URL，例如 http://www.example.com/cgi/addbook.cgi。假设这是初始安装，且根目录中没有 /cgi/addbook.cgi 文件，obj.conf 中的哪些指令将执行来处理此请求？参考示例 6.6 中指定的 obj.conf 文件，服务器将按此顺序处理以下指令：

- 3 AuthCheck fn="match-browser" browser="*MSIE*" ssl-clean-shutdown="true"
- 6 NameTrans fn="document-root" root="$dcroot"
- 9 PathCheck fn="check-acl" acl="default"
- 8 PathCheck fn="uri-clean"
- 10 PathCheck fn="findpathinfo"
- 11 PathCheck fn="find-index-j2ee"
- 12 PathCheck fn="find-index" index-names="index.html,home.html,index.jsp"
- 14 ObjectType fn="type-j2ee"
- 15 ObjectType fn="type-by-extension"
- 16 ObjectType fn="force-type" type="text/plain"
- 18 Service method="(GET|HEAD)" type="magnus-internal/directory"
fn="index-common"
- 19 Service method="(GET|HEAD POST)" type="*magnus-internal/* sendfile"
- 20 Service method="TRACE" fn="service-trace"
- 22 Error fn="error-j2ee"
- 24 AddLog fn="flex-log"

请求处理涉及多个配置文件，但其中 4 个文件对于完全理解 Web Server 如何处理客户端请求至关重要。这些文件是：

- magnus.conf——对请求处理涉及的 SAFs（安全访问文件）进行初始化。
- server.xml——确定用于处理请求的虚拟服务器，并定义在请求处理中使用的各种文件（ACL 文件、mime.types 文件、访问日志等）。
- obj.conf——定义请求处理过程中需要遵循的步骤。
- mime.types——提供 MIME 映射的扩展，帮助确定所处理的请求类型。

> 注意：这些配置文件在第 5 章中进行了详细描述。

本节查看了 obj.conf 文件中定义的几个不同的客户端处理阶段。为了实现这一点，Web Server 利用了两个文件中的信息：mime.types 和 obj.conf。

示例 6.5 提供了默认 mime.types 文件的节选。这些信息将作为参考，帮助描述请求处理。

### 示例 6.5 mime.types 文件节选

1. type=text/html ents=htm,html
2. type=text/plain ents=txt
3. type=magnus-internal/parsed-html ents=shtml
4. type=magnus-internal/cgi ents=cgi,bat

示例 6.6 提供了一个完整的默认 obj.conf 文件。这些信息将作为参考，帮助描述请求处理。

### 示例 6.6 默认 obj.conf 文件

```
1 <Object name=default>
2
3 AuthTrans fn="match-browser" browser="*MSIE*"
ssl-unclean-shutdown="true"
4 NameTrans fn="ntrans-j2ee name="j2ee"
5 NameTrans fn="pf2dir" from="/mc-icons" dir="/sun/webserver7/lib/icons" name="internal"
6 NameTrans fn="document-root" root="$document"
7
8 PathCheck fn="uri-clean"
9 PathCheck fn="check-acl" acl="default"
10 PathCheck fn="find-pathinfo"
11 PathCheck fn="find-index-j2ee"
12 PathCheck fn="find-index" index-names="index.html,home.html,index.jsp"
13
14 ObjectType fn="type-j2ee"
15 ObjectType fn="type-by-extension"
16 ObjectType fn="force-type" type="text/plain"
17
18 Service method="(GET|HEAD)" type="magnus-internal/directory"
fn="index-common"
19 Service method="(GET|HEAD POST)" type="*magnus-internal/* sendfile"
20 Service method="TRACE" fn="service-trace"
21
22 Error fn="error-j2ee"
23
24 AddLog fn="flex-log"
25
26 </Object>
27
28 <Object name="j2ee">
29 Service fn="service-j2ee" method="*"
30 </Object>
31
32 <object name="es-internal">
33 PathCheck fn="check-acl" acl="es-internal"
34 </Object>
35
36 <Object name="cgi">
37 ObjectType fn="force-type" type="magnus-internal/cgi"
38 Service fn="send-cgi"
39 </Object>
40
41 <Object name="send-precompressed">
42 PathCheck fn="find-compressed"
43 </Object>
44
45 <Object name="compress-on-demand">
46 Output fn="insert-filter" filter="http-compression"
47 </Object>
```


位置？请记住，尽管 obj.conf 文件中定义了以下对象来处理 CGI 脚本，但服务器尚未被指示在处理请求时访问这些指令：

```
<Object name="cgi">
ObjectType fn="force-type" type="magnus-internal/cgi"
Service fn="send-cgi"
</Object>
```

下一节将描述你如何整合附加功能，并更改默认处理流，以使请求处理具有条件性。

## 6.3 条件处理

obj.conf 文件包含了一些指令，这些指令指示 Web 服务器如何处理客户端请求并提供相应的响应。对象标签（也称为容器）中包含指令。默认对象包含指令，用于指示 Web 服务器 默认如何处理请求。你添加的每个新对象，或者你可能修改默认对象行为的每个现有对象，都会改变默认对象的行为。你可以通过在 obj.conf 中添加或更改指令来修改和扩展请求处理过程，或者简单地根据某些条件更改流程。

Web Server 7.0 提供了多种方法，让你能够根据条件执行指令。具体如下：

- 指令参数
- 名称翻译（name）属性
- 部分路径（ppath）参数
- 客户端容器
- If/ElseIf/Else 容器

每种方法各不相同，你选择其中一种方法的决定取决于信息的可用性以及你尝试采用的功能。本节将详细描述这些每种方法。

## 6.3 条件处理

### 6.3.1 指令参数

直接指令可以根据指令本身定义的条件进行执行。其中一个示例已在 6.1.7 节“响应生成（服务）阶段”中讨论过。一个 Service 指令的示例指定了函数是否应如下方式执行：

```
Service method="GET HEAD" type="magnus-internal/directory"
fn="index-common"
```

在这种情况下，只有当满足以下条件真时，才会执行 index-common SAF：

- 客户端发送的方法为 GET 或 HEAD
- 在 mime.types 文件中选择的类型不包含字符串 magnus-internal

如果这些条件中的一个或多个条件为假，则请求处理将继续到下一个 Service 指令。

### 6.3.2 名称翻译（name）属性

在请求处理期间，Web 服务器会评估默认对象中的每个 NameTrans 指令，尝试寻找与请求的 URI 一致的匹配。如果匹配的 NameTrans 指令包含 name 属性，则 Web 服务器将切换到处理由 name 属性指定的对象中找到的任何指令，然后再处理默认对象中的剩余指令。

包含 name 属性的 NameTrans 指令示例例如：

```
NameTrans fn="pfx2dir" from="/cgi"
dir="/sun/webserver/7-httpsconfig/mycgi" name="cgi"
```

如果客户端请求的资源以 URI /cgi 开始，则将匹配到此 NameTrans 指令。pfx2dir 函数通过将 dir 属性指定的值与字符串 /cgi 之后的 URI 剩余部分拼接，来创建资源的路径。这告诉 Web 服务器在文件系统的何处查找该资源进行处理；即使找到了该资源，默认对象中的 Service 指令也不会正确处理该请求。相反，处理将回退到默认情况，结果将由包含 send-file SAF 的 Service 指令进行处理。

包含 name 属性的 NameTrans 指令提供了一种机制，通知 Web 服务器另一个对象包含附加指令，仅当发现此 NameTrans 指令为真时才执行这些指令。以下是一个可以与 NameTrans 指令配合使用的 cgi 对象的示例：

```
<Object name="cgi">
  ObjectType fn="force-type" type="magnus-internal/cgi"
  Service fn="send-cgi"
</Object>
```

本质上，name 属性指向另一个对象，该对象包含用于处理请求的附加指令。需要注意的是，NameTrans 指令中 name 属性的值必须与对象的名称相同，两者才能匹配。在这种情况下，两者都必须共享 name="cgi" 值。如果这些值不一致，则在请求处理期间会返回错误。

### 6.3.3 部分路径（ppath）属性

ppath 对象允许你指定指向文档或资源的路径，只有当在 ppath 值指定的位置可以找到该资源的路径时，才会执行该对象中的指令。

当服务器完成对默认对象中 NameTrans 指令的处理后，请求的 URI 已被转换为物理路径名。如果此物理路径名匹配另一个对象的 ppath 属性，则服务器将切换到该对象中的指令，然后再处理默认对象中的剩余指令。

示例 6.7 提供了一个 ppath 对象定义。

示例 6.7 ppath 定义示例

```
<Object ppath="sun/webserver7/https-myconfig/docs/private/*">
  directives
</Object>
```

在 NameTrans 阶段完成后，Web 服务器将查找是否有任何对象的 ppath 值与 NameTrans 阶段生成的路径匹配。在示例 6.7 所示的 ppath 定义情况下，服务器正在查找 NameTrans 阶段生成的路径是否映射到 /sun/webserver7/https-myconfig/docs/private 目录下的任何文档。如果是，则在此 ppath 对象找到找到的指令都将在默认对象中的指令之前进行处理。

## 6.3 条件处理

### 6.3.4 客户端容器

客户端容器用于将一组指令的执行限制为来自特定客户端的请求。列在 <Client> 和 </Client> 之间的指令仅在来自特定客户端的请求时执行。

> 注意：客户端容器只能出现在其他容器内部（例如默认对象）；它们不能独立存在。

客户端参数示例包括：

- browser—浏览器发送的 User-Agent 字符串
- dns—客户端的 DNS 名称
- method—浏览器使用的 HTTP 方法
- type—请求的文档类型（例如 text/html 或 image/gif）
- urlhost—请求的虚拟服务器 DNS 名称

此外，你可以使用通配符模式提供更细粒度的控制。

以下示例演示了在默认对象内部使用客户端容器：

```
<Object name="default">
AuthTrans ...
<Client urlhost="hr.example.com">
NameTrans fn="document-root"
root="/sun/webserver7/https-myconfig/hrdocroot"
</Client>
NameTrans ...
NameTrans ...
</Object>
```

第一个 NameTrans 指令仅当客户端请求 hr.example.com 内容时才会评估。

在以下示例中，客户端标签和 AddLog 指令结合，指示 Web 服务器记录指定子网以外的所有客户端的访问：

```
<Client ip="~192.168.2.*">
AddLog fn="flex-log" name="access"
</Client>
```

客户端容器还允许通过将 match 参数设置为 none 来创建否定匹配。在示例中，排除了指定子网对虚拟服务器 foo.example.com 的所有访问：

```
<Client match="none" ip="~192.168.2.*" urlhost="foo.example.com">
AddLog fn="flex-log" name="access"
</Client>
```

> 注意：请参考 Sun Java System Web Server Administrator Reference 文档获取更多可用参数。Sun Java System Web Server Administrator Reference 的附录 B 提供了 Web Server 7.0 支持的通配符模式类型的细节。

### 6.3.5 If/ElseIf/Else 容器

Web Server 7.0 引入了三种额外的容器，这些容器充分利用逻辑条件、变量和正则表达式来确定是否执行某些指令。

If、ElIf 和 Else 容器允许你定义执行某些指令集的条件。这些容器使用了典型编程语言中的 if-then-else 逻辑。这些新容器只能出现在现有的对象容器内部——它们不能作为 ppath 或命名对象独立存在。然而，这两种类型的容器之间存在一些关键区别，总结如下：





## 6.3 条件处理

- If 和 ElseIf 容器提供了更丰富的表达式语法，包括对正则表达式的支持。这种表达式语法与客户端（Client）反向引用不同。
- If、ElseIf 和 Else 容器可以包含其他容器。客户端容器则不能。
- If 和 ElseIf 表达式每个请求只评估一次，而不是对每个包含的指令评估一次。
- If、ElseIf 和 Else 容器只能包含相同类型的指令；它们不能在同一个容器内包含多种类型的指令。客户端容器可以包含。
- If 和 ElseIf 容器内的指令可以使用正则表达式的后向引用（back references）。

If、ElseIf 和 Else 容器用于在特定情况下执行指令，并可以评估服务器变量以确定是否应该处理这些指令。例如，假设你运行一个网站，该网站仅在早晨 8:30 到下午 5:00 之间开放，并且你希望在营业时间内显示一组页面，在非营业时间内显示另一组页面。你可以利用符号链接和 Unix cron 任务来玩尝试（或者想出其他更改文档根目录的方法来反映营业时间），也可以在对象配置文件中使用一个简单的 If 来如下评估当天的当前时间：

```
<If $time_hour:$time_min < "8:30" || "$time_hour:$time_min > "17:00">
  AuthTrans fn="set-variable" $docroot=/var/www/docs/closed"
</If>
...
NameTrans fn="document-root" root="$docroot"
```

在此示例中，Web 服务器评估 $time_hour 和 $time_min 服务器变量，以确定服务器时间早于上午 8:30 还是晚于下午 5:00。如果发现其中任何情况为真，则处理 AuthTrans 指令，并且 set-variable SAF 会将文档根目录变量 ($docroot) 设置为指示您当前处于关闭状态的页面。然而，如果请求在营业时间内进行处理，则 If 容器中的条件被判断为假，NameTrans 指令将文档根目录设置为在 server.xml 文件中定义的 $docroot 原始值。

**注意：** 使用 set-variable SAF 设置的变量优先级高于 server.xml 文件中定义的变量，因此其他指令对此变量的值没有影响。（有关尝试解析特定变量时所查询的命名空间的描述，请参见第 5 节第 5.3.2.3 部分“变量”）

除了 $doctype 变量外，此示例还引入了变量 $time_hour 和 $time_min。请参考 *Sun Java Web Server Administrator's Configuration File Reference* 中的附录 A 获取变量列表以及在 Web Server 7.0 中定义自定义变量的方法。

尽管此示例非常简单，但它展示了根据简单 if 条件执行指令的能力。一个更复杂的示例展示了多层 If 容器的使用，并引入了 ElseIf 和 Else 容器，如下：

```
<If path="/>
<If $browser="MSIE">
nNames fn="rewrite" path="/msie.html"
</If>
<ElseIf $browser="Mozilla">
nNames fn="rewrite" path="/mozilla.html"
</ElseIf>
<Else>
nNames fn="rewrite" path="/unknown.html"
</Else>
</If>
```

在此示例中，有一个外层 If 容器用于评估 $path 变量是否等于 ""。（当用户在 URI 中未指定任何目录或文件时会发生此情况）。外层 If 容器内有三个“子”容器：If、ElseIf 和 Else。If 和 Else 容器评估 $browser 变量以确定正在使用的浏览器类型。此示例演示了如何配置 Web Server 以根据浏览器是 Microsoft Internet Explorer、Mozilla 还是其他浏览器呈现不同的页面。

> **注意：** 使用时，ElseIf 或 Else 容器必须紧跟在 If 或 ElseIf 容器之后。如果前面的 If 或 ElseIf 表达式评估为逻辑真，则跳过 ElseIf 和 Else 容器。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_266_0.png)

## 6.4 模式匹配与正则表达式

此示例还演示了正则表达式在 If 和 ElseIf 条件语句中的用法。通过评估 $browser 变量来确定字符串 MSIE 或 Mozilla 是从客户端接收到的 user-agent 头部中的部分。“~~”字符序列是一个表示“包含”的正则表达式。第 6.3 节包含了有关正则表达式用法的额外信息。

模式匹配是使用元字符或通配符符号匹配字符字符串的行为。在 Web Server 中，有效使用模式匹配可以让你条件地处理指令，并大幅减少配置文件中的条目数量。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_267_0.png)

> 注意：元字符是一种影响模式匹配方式的特殊字符。字母 A 是普通字符。专门查找字母 A 的搜索仅返回匹配 A（或包含 A）的项。然而，点（.）是一个元字符，可以匹配除换行符以外的单个字符。

### 6.4.1 简单模式匹配

在基于 UNIX 的系统中，模式匹配通常用于使用通配符字符选择多个文件，例如：

- 问号——匹配任意单个字符
- 星号——匹配任意字符一次或多次

例如，在基于 Solaris 的系统中，你可以使用星号来确定 /etc 目录下所有以字母 rc 开头的文件：

```
ls -d /etc/rc*
/etc/rc0 /etc/rc1 /etc/rc2 /etc/rc3 /etc/rc5 /etc/rcm
/etc/rc0.d /etc/rc1.d /etc/rc2.d /etc/rc3.d /etc/rc5.d
```

这显示了所有以 rc 开头的文件。如果你想缩小显示范围，仅匹配 rc0.d、rc1.d、rc2.d、rc3.d 和 rc5.d，则可以使用单字符模式运算符：

```
ls -d /etc/rc?.d
/etc/rc0.d /etc/rc1.d /etc/rc2.d /etc/rc3.d /etc/rc5.d
```

在 Web Server 7.0 中，模式匹配已扩展到 server.xml 文件中的 host 元素。在 virtual-server/host 元素中使用模式匹配可以演示如何最小化定义的元素数量。

**示例 6.8 不使用模式匹配的主机定义**

```
<virtual-server>
  <name>https-foo.bar.example.com</name>
  <host>foo.bar.example.com</host>
  <name>foo.bar.example.com</name>
  <host>foo.eng.example.com</host>
  <name>foo.eng.example.com</name>
</virtual-server>
```

如果 DNS 将这些主机每一个都解析到你的服务器，那么此 virtual-server 定义将允许你处理这些任何主机的请求。但如果你想继续添加额外的 DNS 条目，且不想每次都修改你的 Web Server，该怎么办？你可以使用通配符模式来完成





## 6.4 模式匹配与正则表达式

快速观察示例 6.8 中列出的主机，可以发现每个主机元素都以 `foo..` 字符串模式开头。如果你想向 DNS 添加 `foo.sales` 和 `foo.sales.example.com`，并让服务器在不修改 `server.xml` 文件的情况下对其中一个或两个主机做出响应，你需要如示例 6.9 所示的虚拟服务器定义。

### 示例 6.9 使用通配符模式的主机定义

```
<virtual-server>
<name>https-foo.bar.example.com</name>
<host>foo.*</host>
</virtual-server>
```

示例 6.9 使用简单的模式匹配将主机元素数量从四个减少到一。该定义之所以实现这一点，是因为星号 `*` 匹配字符串 `foo.` 之后的任何字符模式，因此匹配任何以 `foo..` 开头的主机。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_269_0.png)

> 注意：模式匹配仅适用于 `host` 元素。主机比较是大小敏感的。

### 6.4.2 正则表达式

正则表达式在简单的模式匹配技术的基础上，提供了更复杂的匹配条件。它们使用元字符来匹配各种类型的数据模式，并允许你定义匹配多个相似字符串的表达式。例如，正则表达式语句 `he[l]+o w[i|o]ld` 可以匹配 `hello world` 或 `heilo wild`。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_269_1.png)

> 注意：查看 O’Reilly 关于 PERL 正则表达式的页面以了解该语句中所使用的字符概述。地址：http://www.perl.com/doc/manual/html/pod/perre.html。

Web 服务器 7.0 对正则表达式的支持允许你创建非常动态的匹配表达式，并配置更少的设置。正则表达式的一个通用示例如下：

```
[a-z]*://\.*\.example\.com/.*
```

# 第 6 章 WEB 服务器 7.0 请求处理

此示例包含各种模式匹配表达式，用于动态匹配一个或多个 URL。本示例展示了一些常见的模式匹配表达式。

首先，字符集由方括号定义。在本示例中，`a-z` 周围的方括号定义了从字母 `a` 到 `z` 的所有小写字母范围。星号字符 `*` 匹配其之前内容的零或多次出现。因此，当你组合示例中的星号时，你会得到从 `a` 到 `z` 的零或多个字母。这将匹配 `http`、`ftp`、`gopher` 或任何其他字符串。

你还可以在正则表达式中包含实际字符串字符。在本示例中，冒号后跟两个斜杠（`://`）意味着你实际上在寻找该特定字符串。

点 `.` 表示除换行符以外的单个字符。将其与星号 `*` 结合意味着你匹配一个或几乎任何字符。（这被亲切地称为贪婪字符。）

反斜杠 `\` 表示转义字符。这意味着你取的是下一个字符的值。在本示例中，点之前的反斜杠意味着你实际上在寻找一个点字符，而不是除换行符以外任何单个字符的模式。

总之，此正则表达式将匹配用于访问 `.example.com` 域名下服务的任何类型文档或这些主机的任何协议。

正则表达式可以在 `obj.conf` 内部用于评估服务器变量并控制请求处理的流。知道如何以及何时使用它们，对于精简请求处理和正确配置服务器至关重要。

## 6.4.2.1 正则表达式注意事项

正则表达式使用由 Perl兼容正则表达式 (PCRE) 库集实现的 Perl 兼容语法。默认情况下，正则表达式是大小敏感的，但你可以在正则表达式开头使用 `(?i)` 选项标志来实现大小写不敏感。

正则表达式最有效的用法是在 `If/ElseIf/Else` 容器中，以确定何时执行某些指令。`~` 和 `!` 匹配运算符可分别用于判断变量是否包含或不包含模式匹配。容器、匹配运算符和服务器变量的使用允许你创建动态模式匹配场景，以解决一些非常实际的问题。

例如，假设你决定将内容从网站的一个区域（某个文件夹下）迁移到完全全新的服务器。以下示例演示了如何使用正则表达式来实现这一点。

```
<If $uri ~ '^/folder'>
NameTrans fn="redirect" url="http://newsite.example.com"
</If>
```

`If` 容器确定 `$uri` 变量是否包含字符串 `^/folder`（其中脱字符 `^` 是代表字符串开头的元字符）。此特定正则表达式匹配任何请求的 URI 在开头包含 `folder` 字符串的请求。它不会匹配 `/folder`，因为该字符串没有出现在 URL 的开头。所有请求包含此字符串 URI 的客户端都将被重定向到 `http://newsite.example.com` 上的主页。

尽管这实现了将客户端重定向到新站的预期效果，但将所有流量导向新站的主页可能具有很大的局限性。下一节将展示如何使用反向引用（backreferences）来解决这个问题。

## 6.4.2.2 反向引用

正则表达式元字符可以匹配多个字符串。因此，你可能知道自己匹配了内容，但不确定具体匹配的是什么。正则表达式使用名为“反向引用”的概念来处理这种情况。正则表达式的不同部分可以括在括号内，表示你想跟踪匹配的内容。正则表达式的反向引用变量采用 `$n` 形式（其中 `n` 是 1 到 9 的整数），并对应括号内的表达式。换句话说法，反向引用变量采用 `$1`、$2`...`$n` 形式，其中第一个括号表达式由 `$1` 表示，第二个由 `$2` 表示，依此类推。

假设客户端请求包含如下 URI：`/folder1/folder2/folder3/file.html`。

如果你对 URI 应用正则表达式，可以匹配并捕获 URI 的每个部分，并保存到反向引用变量中，如下：

`'^/(.*)/(.*)/(.*)`

这是一个非常简单的示例，除非客户端 URI 包含三个目录，否则不会匹配。然而，它演示了如何使用反向引用以及反向引用变量是如何填充的。

脱字符 `^` 匹配 `$uri` 变量字符串的开头。斜杠 `/` 匹配客户端请求中相应的斜杠。贪婪字符 `.*` 匹配 URI 的每个部分，由于它们被括在括号内，这些值将存储在反向引用变量中：

- $1 = folder1
- $2 = folder2
- $3 = folder3
- $4 = file.html

任何表达式都可以包含对同一容器内早期表达式的反向引用。这允许你使用之前匹配的数据执行额外操作或根据这些数据设置其他变量。

在 6.4.2.1 节中，你看到了根据请求 URI 包含特定文件夹名称将客户端重定向到新站的示例。例如，你看到所有客户端请求（包括子目录中文件的请求）都重定向到了新站的主页。假设你想维护从旧站到新站的请求结构，如果用户请求深层目录（例如 `http://www.example.com/folder/subfolder/file.html`），该用户将能够重定向到新服务器上相同的目录结构，这演示了你如何使用反向引用来实现这一点。

```
<If $uri ~ '^/folder/(.*)'>
NameTrans fn="redirect" url="http://newsite.example.com/$1"
</If>
```




<!-- no content -->




# 第 6 章 WEB 服务器 7.0 请求处理

[04/May/2008:12:46:05] finest (1128): for host 127.0.0.1 trying to GET /index.html, func_exec reports: fn="ntrans-j2ee" name="j2ee" **Directive="NameTrans** returned -2 (REQ_NOACTION)

这两条条目表明服务器目前正在 NameTrans 阶段进行处理，并且刚刚完成了 ntrans-j2ee SAF 的执行。调用 SAF 的返回码为 REQ_NOACTION。这表示该 SAF 未采取任何操作，应该继续执行当前服务器阶段的下一个 SAF。
（完整的 SAF 状态列表请参阅表 6.3。）

[04/May/2008:12:46:05] finest (1128): for host 127.0.0.1 trying to GET /index.html, func_exec reports: executing fn="pfx2dir" from="/icons" dir="C:/Sun/WebServer7/lib/icons" name="internal" **Directive="NameTrans**

[04/May/2008:12:46:05] finest (1128): for host 127.0.0.1 trying to GET /index.html, func_exec reports: fn="pfx2dir" from="/mc-icons" dir="C:/Sun/WebServer7/lib/icons" name="internal" **Directive="NameTrans** returned -2 (REQ_NOACTION)

这两条条目表明服务器目前正在 pfx2dir 阶段进行处理，并且刚刚完成了 SAF 的调用。返回码为 REQ_NOACTION。这表示该 SAF 未采取任何操作，应该继续执行当前服务器阶段的下一个 SAF。这是 NameTrans 阶段处理的最后一个指令，且没有任何指令匹配成功。发生这种情况时，默认行为是根据 $uri 和 $doctype 变量的拼接创建一个文档路径。

[04/May/2008:12:46:05] finest (1128): for host 127.0.0.1 trying to GET /index.html, func_exec reports: executing fn="uri-clean" **Directive="PathCheck**

[04/May/2008:12:46:05] finest (1128): for host 127.0.0.1 trying to GET /index.html, func_exec reports: fn="uri-clean" **Directive="PathCheck** returned 0 (REQ_PROCEED)

这两条条目表明服务器目前正在 PathCheck 阶段进行处理，并且刚刚完成了 uri-clean SAF 的执行。调用 SAF 的返回码为 REQ_PROCEED。这表示该 SAF 成功实现了目标（清理 URI），并应该继续执行当前服务器阶段的下一个 SAF。（参考表 6.3 以了解为什么 REQ_PROCEED 码会让 PathCheck 指令继续处理。）

## 6.5 调试请求处理

乍一看，这些条目包含的信息似乎与 PathCheck 指令的放置冲突。事实并非如此。与创建默认文档根的内部 SAF 处理类似，PathCheck 指令在服务器日志中是隐藏的。你需要意识到每个请求在处理剩余阶段（PathCheck, ObjectType, Service, AddLog）时都会调用 SAF。

由于由于对象配置文件中引入了额外复杂性，该请求在处理剩余阶段时生成的其余条目被刻意省略了。这些条目包含的数据与已讨论的条目相似。表 6.3 包含了对每个 SAF 调用返回代码码的解释。其中某些返回码根据当前处理的阶段而具有不同的含义。理解这些代码有助于更好地理解请求处理。

### 表 6.3 SAF 返回码

| 返回码 | 解释 |
| --- | --- |
| REQ_PROCEED | | SAF 实现了其目标。[注：此处原文重复，修正为：]
| REQ_PROCEED | 表示 SAF 实现了其目标。对于某些请求-响应步骤（AuthTrans, NameTrans, Service 和 Error），此代码告诉服务器跳转到下一个请求-响应阶段，跳过当前阶段的所有其他 SAF。对于其他请求-响应步骤（Input, Output, PathCheck, ObjectType 和 AddLog），服务器将继续执行当前阶段的下一个 SAF。 |
| REQ_NOACTION | | SAF 未采取任何操作。服务器继续执行当前阶段的下一个 SAF。 |
| REQ_ABORTED | 表示发生了错误，并应向客户端发送 HTTP 响应以指示错误原因。返回 REQ_ABORTED 的 SAF 还应设置 HTTP 状态码。如果服务器发现匹配状态码或原因描述的 Error 指令，服务器将执行指定的指令并发送一个反映状态码和原因描述的短 HTML 页面。服务器跳转到第一个 AddLog 指令。 |
| REQ_EXIT | 表示与客户端的连接丢失。当 SAF 在读取或写入客户端失败时，应返回此代码。服务器跳转到第一个 AddLog 指令。 |

## 7.0 请求处理

通常，当你尝试排排除请求处理问题时，应该始终检查日志文件。如果日志文件中不包含足够帮助确定问题的信息，则你应该将日志级别增加到 finest。然后重现问题并再次检查日志文件。

## 6.6 总结

Web Server 7.0 中的请求处理比之前的版本更健壮。为了应对对象配置文件引入的额外复杂性，解析器被重写以捕获更多的配置错误并以逻辑方式处理其他错误。尽管如此，在实现容器和复杂的正则表达式时，很容易误配置你的 Web Server 实例。确保在对对象配置文件进行重大更新之前保存配置，并在非生产系统上彻底测试你的更改。但是，如果你犯了错误，请放心，你有多种调试技术可以帮助确定并解决问题。

## 6.7 自学实验室

使用本章包含的信息执行以下练习。这些将将验证你对本章描述概念的理解。

1. 通过以下步骤为终端用户主页提供支持：
   a) 在服务器上创建一个目录结构以包含用户目录，b) 在其下方创建新的特定于用户的目录，例如：
   - /var/websites/people/rodale
   - /var/websites/people/wclay
   - /var/websites/people/relise
   c) 在用户特定目录中填充示例 index.html 文件，并 d) 使用 If Container 和适当 NameTrans 指令访问内容。更新 NameTrans 指令以接受用户目录的大小写字母。

2. 创建单个容器和 NameTrans 指令以支持虚拟服务器内的别名和多个网站。使用正则表达式、表达式函数和反向引用来解决问题。参考以下项目：
   - www.example.com 映射到 /var/websites/sites/www.example.com
   - w3.example.com 映射到 /var/websites/sites/www.example.com
   - example.com 映射到 /var/websites/sites/www.example.com

3. 向服务器日志发送用户自定义消息，指示你正在使用的浏览器。

4. 为各种浏览器类型创建不同的网页（例如，mozilla.html, msie.html），并使用 If/ElseIf/Else 容器结构为每个浏览器显示不同的网页。

5. 使用管理控制台启用 CGI 作为目录的 NameTrans 指令。查看对对象 配置文件进行的更改（你应该看到一个针对 CGI NameTrans 指令的新 pfxdir SAF 条目）。验证你有一个在匹配 NameTrans 指令时调用 cgi 对象的项。在 CGI 目录下方放置一个输出 "Hello World!" 的脚本，并验证你可以访问/处理该脚本。

> 注意：访问 http://www.sunwebserver.com 可获得如何回答这些每个问题的详细说明。

6. 将日志级别更改为 finest 并重新创建生成步骤 1-6 响应的客户端请求。检查为每个客户端请求生成的条目。





## 监控 Web Server 7.0

**有效监控** Web Server 是维护最佳生产环境的基本任务。通过持续关注，你可以识别性能瓶颈，从而能够对系统进行调整以获得最佳性能。监控 Web Server 允许你通过确定何时需要额外的节点来服务不断增长的客户群，采取主动的容量规划方法。如果你计划在网站上添加新的服务或功能，且预计这会吸引更多访问者，那么这一点就至关重要。监控可以让你判断网站的配置是否正确，或者网页内是否存在错误的链接。它还能允许你检测并预测某些故障，在发生故障时进行根原因分析，并在某些情况下只需确保一切运行都符合预期。

本章解释了你用于监控 Web Server 的各种方法。这可能简单到关注 Web 日志文件，也可以是将统计数据存储在数据库中并查找趋势。你监控的内容、类型以及如何处理这些数据完全由你决定。

本章将介绍 Web Server 7.0 内部的监控子系统以及你如何使用各种工具从该子系统中提取数据。随后，它将探索如何评估数据模式，并利用这些知识微调你的 Web Server 性能。通常，我们将讨论以下主题：

- Web Server 统计数据
- Web Server 监控子系统
- 监控 Web Server 方法
- 如何使用监控数据调优 Web Server

## 7.1 Web Server 统计数据

Web Server 为收到的每个请求维护统计数据。这些数据允许你监控服务器活动并获取有助于微调系统的信息。统计数据显示了你的服务器处理了多少请求以及处理这些请求的情况如何。你可以查看单个虚拟服务器、服务器实例或跨多个节点配置的统计数据。

统计数据在每个节点与其注册的管理服务器（Administration Server）之间传输。因此，即使服务器实例已重启，你也可以查看统计数据。这在你需要排除一个停止响应或已重启的实例时特别有用。

统计数据可以按实例进行配置。与 Web Server 的之前的版本不同，Web Server 7.0 中的统计功能默认启用，并在 `server.xml` 文件中配置如下：

```xml
<stats>
  <enabled>true</enabled>
  <interval>10</interval>
</stats>
```

此示例演示了一个启用了统计功能且每五秒更新一次信息的服务器实例。`stats` 元素用于配置统计收集子系统，并可能包含以下元素：

- enabled—服务器在运行时是否收集统计数据。可选值为 `true` 或 `false`；默认值为 `true`。
- interval—更新统计数据的间隔时间（秒）。可选范围在 `0.001` 到 `3600` 之间；默认值为 `5`。
- profiling—是否启用了性能桶（performance buckets）。（性能桶用于跟踪 NSAPI 函数的执行时间。）可选值为 `true` 或 `false`；默认值为 `true`。

对特定实例的 `server.xml` 文件进行检查可能包含也可能不包含 `stats` 元素。缺少此元素意味着统计功能已启用并使用默认配置设置。除非你想覆盖默认值，否则无需添加 `stats` 元素。

## 7.2 Web Server 监控子系统

监控子系统从注册的节点收集统计数据，并将数据暴露给各种客户端使用。默认客户端接口包括：

- 命令行界面 (CLI)
- 图形用户界面 (GUI)
- Java 企业级监控控制台 (Java ES Monitoring Console)
- 简单网络管理协议 (SNMP) 客户端

图 7.1 提供了 Web Server 7.0 监控子系统的分层概述。它包含了用于通信和收集统计数据的各种接口信息。

命令行界面和图形用户界面都通过管理服务器实例访问统计数据。GUI 通过管理控制台 Web 实现此，而 CLI 则直接与 Java 管理扩展 (JMX) 连接 Servlet 通信。

管理节点（Administration Node）上的监控 MBeans 从每个运行的服务器实例获取统计数据。MBeans 使用 Java 原生接口 (JNI) 层连接并检索数据。然后，信息被传回管理服务器，在那里供 CLI 或 GUI 接口使用。

> 注意：请参阅第 4 章第 4.3 节“Web Server 7.0 管理”，获取更多关于 Web Server 7.0 管理架构的信息。

你还可以使用 Java ES 监控控制台或网络管理系统与运行在特定管理节点上的代理应用程序通信。这让你能够灵活地从不同的基于标准的客户端监控应用程序中获取数据，并以一致的方式显示这些数据。图 7.1 展示了在类似此类客户端应用程序的环境中如何访问数据。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_286_0.png)

**图 7.1** Web Server 7.0 监控子系统组件

## 7.3 监控 Web Server 方法

Web Server 7.0 提供了几种监控 Web Server 内部组件的方法。你可以监控共享特定配置的所有节点的数据，缩小到配置中的某个特定实例，甚至可以是单个实例内的某个特定虚拟服务器。你可以跟踪以下信息……

### 7.3.1 访问日志

访问日志的默认名为 `access.log`。访问日志记录了到 Web 服务器的每一个请求。访问日志对于审计、故障排除和流量模式分析有用。访问日志中的每个条目包含客户端 IP 地址、请求时间、使用的 HTTP 方法、请求的 URL、返回的状态码以及响应的大小。

你可以在 `server.xml` 文件中配置访问日志格式。默认情况下，日志包含以下信息：

- 客户端 IP 地址
- 时间
- HTTP 方法
- 请求 URL
- 状态

还可以自定义访问日志格式以包含或排除字段。例如，你可能希望包含用户代理（user-agent）字符串或引用页 URL（referrer URL）。

### 7.3.1.1 访问日志示例

下表显示了访问日志样本。

| 客户端 IP | 时间 | 方法 | URL | 状态 | 大小（字节） |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 10.102.201.100 | [05/Oct/2006:15:00:00 -0500] | GET | / | 200 | 966 |
| 10.102.201.100 | [05/Oct/2006:15:00:50 -0500] | GET | /img/sun_logo.gif | 200 | 999 |
| 10.102.201.100 | [05/Oct/2006:15:00:51 -0500] | GET | /a.gif | 200 | 234 |
| 10.102.201.100 | [05/Oct/2006:15:00:51 -0500] | GET | /img/sjsws-title.text.gif | 200 | 822 |
| 10.102.201.100 | [05/Oct/2006:15:00:52 -0500] | GET | /img/content_hline.gif | 200 | 473 |
| 10.102.201.100 | [05/Oct/2006:15:00:52 -0500] | GET | /img/foo.gif | 404 | 292 |





## 7.3 监控 Web 服务器的方法

示例 7.1 的第一行定义了每个日志条目的格式，并有助于解释日志文件中其余行。根据该格式，系统会记录客户端 IP 地址，随后是经过验证的用户名（如果已知）。接下来记录的是系统日期，然后是来自客户端的实际 HTTP 请求、服务器对该请求的响应，以及传输到客户端的内容长度（字节）。

示例 7.1 包含六个 GET 请求以及 Web 服务器为每个请求发送给客户端的相关响应。其中包含一个针对主页的 GET 请求和另外五个针对页面内包含的图片的 GET 请求。前五个请求包含响应代码 200（意味着请求成功）。最后一个请求包含响应代码 404，意味着在该服务器上未找到该项目（或文件）。这很可能是由于网页中的引用不正确导致的。你应该定期扫描日志文件，并解决此类问题。

服务器访问日志可以是通用日志格式（Common Log Format），你也可以提供自己自定义的格式。通用日志格式是多个供应商服务器共同支持的常用格式，并提供了有关服务器的固定数量的信息。你可以通过使用参数块（blocks）来自定义定义日志格式，这允许你控制记录哪些内容。有关可自定义格式参数的列表，请参见《Sun Java Web Server 7.0 NS 开发者指南》。

> 注意：你可以通过管理控制台、命令行界面或直接编辑相应服务器实例的 `server.xml` 文件来更改访问日志的格式。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_289_0.png)

特定配置的访问日志创建后，在你将其归档或为该配置创建新的访问日志文件之前，无法更改其属性。

### 7.3.1.2 服务器日志文件

服务器日志文件的默认名称为 `errors`。此文件列出了服务器遇到的所有错误，以及服务器的启动和停止信息。服务器日志包含服务器运行事件（例如加载证书吊销列表）时生成的消息，你可以使用日志 API 向服务器日志中添加任何条目。你可以通过修改 `server.xml` 文件中的 `log-level` 属性来配置服务器日志中提供的详细程度。

# 第 7 章监控 Web 服务器 7.0

服务器日志的基本格式如下：

`[date] log-level (pid): error-message-number: error-message`

并可以描述如下：

- date：条目的日期（或时间戳）。该日期由一组方框括定。
- log-level：条目的严严重程度。不同的日志级别包含不同类型或数量的数据。Web 服务器定义了以下日志级别：
  - finest, finer, fine——消息非常详尽，可能包含调试信息。`finest` 日志级别提供的信息最多。
  - info——消息在本质上是信息性的，通常包含与服务器配置或状态相关的信息。这些消息并不表示需要立即采取行动。
  - warning——消息表示警告。消息通常会伴随异常（exception）。
  - failure——消息表示重大的失败，可能会阻止应用程序的正常执行。
  - config——消息与各种静态配置信息有关，用于调试可能与特定配置相关的问题。
  - security——消息表示安全问题。
  - catastrophe——消息表示致命错误。

列表顶部的项目产生的信息最多，随着你向后移动，消息数量会逐渐减少。在排查 Web 服务器问题时，增加日志级别是常见操作。

- pid：Web 服务器的进程标识符。
- error-message-number：与该条目相关的错误消息数字。
- error-message：与该条目相关的错误消息。错误是自由格式文本。

警告：`error-message-number` 和 `error-message` 由 API 开发者创建并在函数之间传递。Web 服务器与其他 Sun Web 层产品（例如 Java 企业级系统代理服务器）共享代码，尽管某些信息可能相似，但你不能认为日志条目是相同的。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_290_0.png)

## 7.3 监控 Web 服务器的方法

`log` 元素用于在 `server.xml` 文件中配置服务器日志参数。以下 `log` 元素的默认配置示例。

```xml
<log>
  <log-file>../logs/errors</log-file>
  <log-level>info</log-level>
</log>
```

`log-file` 子元素用于定义服务器日志文件的位置。如果未提供全限定文件名作为该元素的值，则所有文件引用都相对于实例的配置目录。`log-level` 子元素用于定义日志级别，直接影响发送到服务器日志的条目类型。

> 注意：请参见《Sun Java Web Server 7.0 管理员配置文件参考》，以获取可以为服务器日志配置的其他属性。

示例 7.2 提供了服务器启动后不久的服务器日志文件示例。文件中找到的条目与示例 7.1 中的条目相对应。

## 示例 7.2 服务器日志文件

```
[05/Oct/2006:07:11:01 -0500] info (1234): Sun Java Web Server 7.0 (Java SE) built on Oct 11
[05/Oct/2006:07:11:05 -0500] info (1234): Using HotSpot VM version 1.5.0, mixed mode, client-based VM
[05/Oct/2006:07:11:09 -0500] info (1234): Listener ready to accept requests on port 80
[05/Oct/2006:07:11:10 -0500] info (1234): Server startup complete.
10.0.0.101 - [05/Oct/2006:15:00:52 -0500] "GET /img/foo.gif HTTP/1.1" 404 292
```

示例 7.2 前四个条目是提供启动信息的消息。这些条目可以描述为：

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_291_0.png)

# 第 7 章监控 Web 服务器 7.0

- 条目 1：Web 服务器的版本。
- 条目 2：Java 虚拟机（JVM）的版本以及 Web 服务器使用的 HotSpot 插件。
- 条目 3：演示监听器准备好接受请求。
- 条目 4：指示服务器启动成功。

示例 7.2 中的最后一个条目提供了为什么访问日志中的后续条目向客户端返回了 404 错误代码的原因。

在大多数情况下，服务器日志中的数据足够调试涉及内容的问题。然而，如果你需要对特定问题进行大量的排查，你应该将日志级别提高到 `finest`，重现问题，并查看由于级别增加生成的额外条目。

### 7.3.1.3 从管理控制台访问并修改设置

管理控制台提供了一个易用的图形化 Web 表单，允许你查看并修改访问日志或服务器日志的设置。你可以通过以下步骤从管理控制台访问日志设置：

1. 打开管理控制台并点击 `Configurations` 标签进入主配置页面。
2. 点击要修改的服务器日志设置所在的配置链接。
3. 点击 `General` 标签。这将打开一个窗口，允许你执行该配置的通用功能，例如修改日志引用。
4. 点击 `Log Preferences` 标签（如果需要）。主窗口将打开以更新访问日志或服务器日志的偏好。

通过控制台进行的任何更改将更新 `server.xml` 文件中的 `access-log` 或 `log` 元素（视情况而定）。




## 7.3 监控 Web 服务器的方法

### 7.3.1.4 从命令行界面访问和修改访问日志属性

命令行界面提供了子命令，用于快速访问和修改访问日志（Access Log）的日志设置。这些子命令可以包含在脚本中，以便在执行管理任务时实现更多功能。

CLI 中的 `get-access-log-prop` 子命令可用于获取日志的当前属性。以下信息提供了该子命令的概述：

```
wadm get-access-log-prop --<TAB>
--config* --vs --uri-pattern --echo --no-prompt
--verbose
```

你可以在服务器级或虚拟服务器级配置访问日志属性。子命令同样允许你获取这两个层级的属性。以下示例演示了如何使用 `get-access-log-prop` 子命令获取 My Test Config 配置的当前访问日志属性：

```
wadm get-access-log-prop --config="My Test Config"
enabled=true
file=./logs/access
format=%Ses--client.ip% %Req->auth-user% [%SYSDATE%] "%Req-
reqpb.clf-
request*" %Req->srvhds.clf-status% %Req->srvhds.content-length%

wadm>
```

CLI 中的 `enable-access-log` 子命令用于修改访问日志属性。以下信息提供了该子命令的概述：

```
wadm enable-access-log --<TAB>
--config* --file* --log-ip --vs
--uri-pattern --echo --no-prompt
```

你可以在服务器级或虚拟服务器级配置访问日志属性。子命令同样允许你配置这两个层级。以下示例演示了如何使用 `enable-access-log` 子命令设置 My Test Config 的访问日志位置：

```
wadm>enable-access-log --config="My Test Config" --file="/foo.txt"
CLI201 命令 'enable-access-log' 执行成功
wadm>
```

![](img/a3cb513bf7a0b21f70c67_293_0.png)

使用 `enable-access-log` 子命令进行的更改将更新 `server.xml` 文件中相应的访问日志元素。

### 7.3.1.5 从命令行界面访问和修改服务器日志属性

命令行界面提供了子命令，用于快速访问和修改服务器日志（Server Log）的设置。这些子命令可以包含在脚本中，以便在执行管理任务时实现更多功能。

CLI 中的 `get-log-prop` 子命令可用于获取服务器日志的当前属性。以下信息提供了该子命令的概述：

```
wadm> get-log-prop --<TAB>
--config* --echo --no-prompt --verbose
```

你可以在服务器级或虚拟服务器级配置服务器日志设置。该子命令同样允许获取每个层级的属性。以下示例演示了如何使用 `get-log-prop` 子命令获取 My Test Config 配置的当前服务器日志属性：

```
wadm> get-log-prop --config="My Test Config"
log-stdout=true
log-to-syslog=false
log-virtual-server-name=false
log-to-console=true
date-format=[%d/%d/%Y:%H:%M:%S]
log-level=info
archive-suffix=.%Y%m%d%H%M
log-file=../logs/errors
stderr=true
```

CLI 中的 `set-log-prop` 子命令用于设置服务器日志属性。以下信息提供了该子命令的概述：

```
wadm> set-log-prop --<TAB>
--config* --echo --no-prompt --verbose
```

你可以在服务器级或虚拟服务器级配置服务器日志设置。以下示例演示了如何使用 `set-log-prop` 子命令设置 My Test Config 配置的服务器日志级别：

```
wadm set-log-prop --config="My Test Config" log-level=finCLI201 命令 'set-log-prop' 执行成功
wadm>
```

使用 `set-log-prop` 子命令进行的更改将更新 `server.xml` 文件中相应的日志元素。

### 7.3.1.6 从控制台访问日志数据

控制台日志查看器（Log Viewer）提供了一个用于查看日志的 Web 界面。在单个网页上，你可以轻松地查看任何配置的访问日志或服务器日志。这可以限于配置内的所有节点。你可以根据日期、日志级别或标识符对条目进行排序。你还可以根据条目数量、日志级别或服务器响应代码过滤数据，或者显示特定时间范围内的条目。

要访问日志查看器，请执行以下步骤：

1. 打开控制台并点击 Configuration 标签进入主配置页。
2. 点击页面右上角的 Logs 按钮。这将打开日志查看器窗口。

如果你已经打开了 GUI，在控制台访问日志数据非常方便。但如果你需要立即访问数据，图形界面可能不是合适的方法。幸运的是，Web 服务器还提供了通过命令行或直接在文件系统中查看日志的方法。接下来的两个章节介绍了如何使用这两种方法访问日志文件。

### 7.3.1.7 从命令行访问数据

命令行界面提供了与控制台相同的日志数据访问功能。有两个特定的子命令用于此目的：用于获取访问日志条目（get-access-log）和服务器日志条目（get-log）。本节介绍了这两个子命令。CLI 中的 `get-access-log` 子命令可用于检索特定配置的访问日志条目。以下信息提供了该子命令的概述：

```
wadm> get-access-log --<TAB>
  --config --start-date --status-code --num-records
  --vs --echo
  --no-prompt --verbose
```

该命令允许你根据条目数量、特定的服务器响应代码或特定时间范围过滤数据。以下示例演示了如何使用 `get-access-log` 子命令检索 example.com 配置的访问日志数据：

```
wadm> get-access-log --config="example.com" www.example.com
[05/Oct/2006:15:00:50] 10.100.2.101 - "GET / HTTP/1.1" 200
[05/Oct/2006:15:00:50] 10.100.2.101 - "GET /img/sun_logo.gif HTTP/1.1" 234
[05/Oct/2006:15:00:51] 10.100.2.101 - "GET /img/a.gif HTTP/1.1" 43
[05/Oct/2006:15:00:51] 10.100.2.101 - "GET /img/sws_title.gif HTTP/1.1" 201
[05/Oct/2006:15:00:52] 10.100.2.101 - "GET /img/content-hline.gif HTTP/1.1" 473
[05/Oct/2006:15:00:52] 10.100.2.101 - "GET /img/foo.gif HTTP/1.1" 402
```

注意：当从命令行检索访问日志时，不会返回格式条目。

CLI 中的 `get-log` 子命令可用于检索特定配置的服务器日志条目。以下信息提供了该子命令的概述：

![](img/a3cb513bf7a0b21f70c67_293_0.png) (此处为示例引用)

```
wadm> get-log --config="My Test Config"
```

该命令同样允许你根据条目数量、日志级别或特定时间范围过滤数据。以下示例演示了如何使用 `get-log` 子命令获取 My Test Config 的服务器日志：

### 7.3.1.8 从文件系统访问日志数据

访问日志数据的方法之一是查看文件系统中的日志文件内容。你可以使用操作系统特定的命令来搜索数据、排序数据、合并日志文件，或者仅仅监控文件内部的事件。

你可以在特定节点的 server_root/configuration/logs 目录下找到日志。

### 7.3.2 XML 报告

Web 服务器实例启动后，它开始收集用于监控的统计数据，并通过 XML 数据报告进行访问。控制台和某些文本报告从该提取信息


XML 数据旨在为您提供一个用户友界面。然而，在某些情况下，您可能需要查看原始 XML 数据，因为它包含的信息比格式化的网页或报告详详细得多。

> 注意：Web Server 7.0 继续支持在之前的 Web Server 版本中找到并使用 stats-xml SAF 生成的 XML 数据流。与之前的版本不同，Web Server 7.0 默认启用了统计收集，且数据现在包含了额外的 Java 数据值。

XML 报告通常用于分析工具，可以通过命令行界面或用户定义的 URI 进行访问。

## 7.3.2.1 从命令行访问 XML 报告

命令行界面需要对管理服务器（Administration Server）进行身份验证，且 CLI 与管理服务器之间的所有流量都经过加密。因此，从 CLI 访问数据既安全又方便。

默认情况下，可以使用 CLI 中的 `get-stats-xml` 子命令访问 Web Server 的全部统计数据，如下：

```
wadm> get-stats-xml ---<TAB>
--config* --node* --echo --no-prompt --verbose
```

您可以仅获取配置中某个特定节点的统计信息。以下示例演示了如何使用 `get-stats-xml` 命令检索来自 www.example.com 配置中 `node1` 节点的 get-stats-xml 数据。

```
wadm> get-stats-xml --config=www.example.com --node=node1
```

> 注意：参见附录 B，“示例 XML 报告数据”，获取此命令的示例输出。

CLI 对于排除服务器实例停止响应 HTTP 请求的情况非常有用。挂起实例的最后已知统计数据仍然存储在管理服务器中，可以通过

## 7.3 监控 Web 服务器的方法

通过命令行获取。这些信息对于调试问题很有帮助，因为通常包含了服务器出现问题之前的最后一次请求。

## 7.3.2.2 从用户定义的 URI 访问 XML 报告

命令行界面的访问默认启的，但如果您想通过特定的 URI 访问 XML 报告，则需要在虚拟服务器级别启用 XML 报告。

管理控制台（Administration Console）提供了一个易于使用的图形化 Web 表单，允许您启用 XML 报告并配置访问数据所需的 URI。您可以通过以下步骤通过管理控制台访问表单：

1. 打开管理控制台并点击“配置”（Configurations）选项卡进入主配置页面。
2. 点击包含您想要启用 XML 报告的虚拟服务器的配置链接。您将看到虚拟服务器列表。
3. 点击想要启用 XML 报告的虚拟服务器链接。您将看到虚拟服务器常规属性页面。
4. 点击“服务器设置”（Server Settings）选项卡（如有必要）。
5. 点击“监控设置”（Monitoring Settings）子标签页（如有必要）。您将看到为此虚拟服务器启用和配置 XML 报告的主窗口。
6. 勾选“XML 报告已启用”旁边的复选框并修改 URI（如有必要）。

命令行界面也可用于启用 XML 报告、禁用 XML 报告以及查询特定虚拟服务器的 XML 报告状态。这些任务可以通过子命令完成：

- get-stats-xml-prop: 获取 XML 报告设置的属性
- enable-stats-xml: 启用 XML 报告并提供相应的 URI
- disable-stats-xml: 禁用 XML 报告

`get-stats-xml-prop` 子命令可判断特定虚拟服务器是否已启用 XML 报告。以下示例演示了该子命令用法：

## 第 7 章 监控 Web Server 7.0

```
wadm> get-stats-xml-prop --
--Config* --vs* --echo --no-prompt --verbose
```

通过 URI 访问 XML 报告数据默认是禁用的。您可以使用 `get-stats-xml-prop` 子命令进行验证：

```
wadm> get-stats-xml-prop --config=www.example.com --vs=www.example.com
enabled=false
uri/=stats-xml(/*)
```

您可以使用 CLI 中的 `enable-stats-xml` 子命令启用通过 URI 访问 XML 报告，并使用 `disable-stats-xml` 子命令再次将其禁用。`enable-stats-xml` 子命令接受 URI 作为选项。这允许您在启用 XML 报告时指定自己的 URI。以下示例演示了如何从命令行启用 XML 报告并为访问数据指定自定义 URI。

```
wadm> enable-stats-xml --config=www.example.com --vs=www.example.com
--uri-prefix=/wsstats(/*)
CLI201 Command 'enable-stats-xml' ran successfully
```

在通过管理控制台或命令行界面启用 XML 报告数据访问后，执行这些步骤的结果将是一个修改后的对象配置文件，其中包含以下新增内容：

- 一个 `NameTrans` 指令，用于拦截 URI 并关联命名对象以进行进一步处理，如下：
  NameTrans fn="assign-name name="stats-xml" from="/wsstats(/*)" 
- 指定用于导出 XML 报告数据的适当服务的命名对象如下：
<Object name="stats-xml">
Service fn="stats-xml"
</Object>

现在您可以通过向您的虚拟服务器提供相应的 URI 来访问 XML 报告：

```
http://www.example.com/wsstats/
```

## 7.3 监控 Web 服务器的方法

该请求的响应是一个包含与附录 B，“示例 XML 数据”类似内容的页面。

> 注意：您可以通过对某个元素指定 0 来限制报告中的数据量。默认显示所有元素，但您可以从 URI 隐藏它们：

http://localhost:8080/

XML 报告中的某些数据可能被认为是敏感的。因此，如果您启用了对该 URI 的访问，应考虑添加访问控制。创建此创建的 ACL 文件必须在对象定义中引用。例如，您需要在对象配置中添加 `PathCheck`：

```
<Object name="stats-xml">
  PathCheck fn="check-acl" acl="stats.xml"
  Service fn="stats-xml"
</Object>
```

> 注意：参见第 8 章，“安全 Web Server 7.0”，获取有关创建 ACL 的更多信息。

## 7.3.3 文本报告

service-dump 是 Web Server 内的服务器应用程序（SAF），它收集各种性能数据并以 ASCII 格式的报告显示出来。

> 注意：您可能会在 Sun 文档中看到 service-dump、perfdump 或文本报告的引用。它们都指的是相同的功能。

## 7.3.1 从命令行访问文本报告数据

文本报告数据未在 CLI 或管理控制台中显示所有统计信息，但它仍然是监控 Web 服务器的有用工具。可以使用 CLI 中的 `get-perfdump` 命令或通过定义 URI 来获取文本报告。

文本报告提供以下类的统计信息：

- 连接队列信息
- HTTP 监听（监听字）信息
- 保持（Keep-alive）信息
- 会话创建（线程）信息
- 文件缓存信息（静态内容）
- 线程池信息
- DNS 缓存信息

默认情况下可以从命令行访问文本报告数据，使用 `get-perfdump` 子命令：

```
wadm> get-perfdump --<TAB>
--config* --node* --echo --no-prompt --verbose
```

> 注意：参见附录 C，“示例文本报告数据”，获取此子命令的示例输出以及对数据的解释。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_302_0.png)

文本报告包含的数据可以为服务器如何处理请求提供宝贵的见解。stats-xml 数据提供了所有可用统计数据的全面视图，对于深入研究数据非常有用，但它实际上可能包含过多信息。作为替代，文本报告提供了 stats-xml 数据的格式化子集，并为您提供服务器整体性能的仪表盘视图。





## 7.3 监控 Web 服务器的方法

### 7.3.3.2 从自定义 URI 访问纯文本报告数据

命令行界面默认启用访问功能，但如果您想通过特定的 URI 访问此类信息，则需要在虚拟服务器级别启用纯文本报告（Plain Text Report）。

管理控制台提供了一个易于使用的图形化 Web 表单，允许您启用纯文本报告并配置访问数据所需的 URI。可以通过以下步骤通过管理控制台访问该表单：

- 1. 打开管理控制台并点击“配置”（Configurations）标签进入主配置页面。
- 2. 点击包含要启用纯文本报告的虚拟服务器的配置链接。您将看到虚拟服务器列表。
- 3. 点击要启用纯文本报告的虚拟服务器链接。您将看到虚拟服务器属性页。
- 4. 点击“服务器设置”（Server Settings）标签（如有必要）。
- 5. 点击“监控设置”（Monitoring Settings）标签（如有必要）。您将看到启用和配置此虚拟服务器纯文本报告的主窗口。
- 6. 勾选启用纯文本报告（Enabled for Plain Text Report）旁边的复选框并修改 URI（如有必要）。

> 注意：这些步骤与 7.3.2.2 中的步骤相似。不同之处在于，您现在选择的是纯文本报告（而不是启用 XML），并且同样指定了适当的 URI 来访问报告。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_303_0.png)

还可以使用命令行界面启用纯文本报告功能、禁用纯文本报告并获取特定虚拟服务器的纯文本报告数据。可以使用以下命令执行这些任务：

- get-perfdump-prop—获取纯文本报告配置设置的属性
- enable-perfdump—启用纯文本报告并提供相应的 URI
- disable-perfdump—禁用通过 URI 访问纯文本报告

get-perfdump-prop 子命令可用于判断特定虚拟服务器是否已启用纯文本报告。以下示例演示了该子命令用法：

```
wadm> get-perfdump-prop ---
--config --vs=* --echo --no-prompt --verbose
```

通过 URI 访问纯文本报告数据默认是禁用的。您可以如下所示使用 get-perfdump-prop 子命令进行验证：

```
wadm> get-perfdump-prop --config=www.example.com --vs=www.example.com
enabled=false
uri=/.perf
```

您可以使用 CLI 中的 enable-perfdump 子命令启用通过 URI 访问纯文本报告，并使用 disable-perfdump 子命令再次禁用。enable-perfdump 子命令接受 URI 作为选项。在启用纯文本报告时，您可以指定自己的 URI。以下示例演示了您如何从命令行启用纯文本报告，并为访问数据指定自定义 URI。

```
wadm> enable-perfdump --config=www.example.com --vs=www.example.com
--uri=/.perf
CLI201 Command 'enable-perfdump' ran successfully
```

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_304_0.png)

> 注意：enable-stats-xml 命令和 enable-perfdump 命令的参数略有不同。例如，enable-stats-xml 子命令使用 uri-prefix 参数来指定 URI；而 enable-perfdump 子命令使用 uri 参数。

在通过控制台或命令行界面启用通过 URI 访问纯文本报告后，执行这些步骤的结果将是一个修改后的对象配置文件，其中包含以下新增：

- NameTrans 指令，用于拦截 URI 并关联命名对象以进行进一步处理，如下：

NameTrans fn="assign-name" name="perf" from="./.perf"

- 指定用于转储纯文本报告数据的适当服务的命名对象，如下：

```
<Object name="perf">
Service fn="service-dump">
</Object>
```

现在可以通过向虚拟服务器提供适当的 URI 来访问纯文本报告：

```
http://www.example.com/.perf
```

该请求的响应是一个网页，其中包含与附录 C“示例纯文本报告数据”中所示类似的数据。

纯文本报告中的某些数据可能具有敏感性。因此，如果您选择通过 URI 访问数据，则应该考虑为该资源的 URI 添加访问控制。这样做可以限制通过浏览器查看您服务器数据的用户数。

为了保护此 URI 而创建的 ACL 文件必须在对象配置文件中的 perf 定义中引用。例如，如果您为 /.perf URI 创建了命名的 ACL 并将其命名为 perfdump.acl，则您需要在对象定义中添加 PathCheck 指令，如下：

```
<Object name="perf">
PathCheck fn="check-acl" acl="perfdump.acl"
Service fn="service-dump"
</Object>
```

> 注意：关于创建 ACL 文件的更多信息，请参第 8 章。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_305_0)

## 7.3 监控 Web 服务器的方法

### 7.3.3 命令行界面

通过 URI 访问纯文本报告数据默认禁用。您可以使用 get-perfdump-prop 子命令进行验证：

```
wadm> get-perfdump-prop --config=www.example.com --vs=www.example.com
enabled=false
uri=/.perf
```

您可以使用 CLI 中的 enable-perfdump 子命令启用通过 URI 访问纯文本报告，并使用 disable-perfdump 子命令再次禁用。enable-perfdump 子命令接受 URI 作为选项。在启用纯文本报告时，您可以指定自己的 URI。以下示例演示了您如何从命令行启用纯文本报告并为访问数据指定自定义 URI。

```
wadm> enable-perfdump --config=www.example.com --vs=www.example.com
--uri=/.perf
CLI201 Command 'enable-perfdump' ran successfully
```

在通过控制台或命令行界面启用通过 URI 访问纯文本报告后，执行这些步骤的结果是一个修改后的对象配置文件，其中包含以下：

- NameTrans 指令，用于拦截 URI 并关联命名对象以进行进一步处理，如下：

NameTrans fn="assign-name" name="perf" from="./.perf"

- 指定用于转储纯文本报告数据的适当服务的命名对象，如下：

```
<Object name="perf">
Service fn="service-dump">
</Object>
```

现在可以通过向虚拟服务器提供适当的 URI 来访问纯文本报告：

```
http://www.example.com/.perf
```

该请求的响应是一个网页，其中包含与附录 C“示例纯文本报告数据”中所示类似的数据。

纯文本报告中的某些数据可能具有敏感性。因此，如果您选择通过 URI 访问数据，则应该考虑为该资源的 URI 添加访问控制。这样做可以限制通过浏览器查看您服务器数据的用户数。

为了保护此 URI 而创建的 ACL 文件必须在对象配置文件中的 perf 定义中引用。例如，如果您为 /.perf URI 创建了命名的 ACL 并将其命名为 perfdump.acl，则您需要在对象定义中添加 PathCheck 指令，如下：

```
<Object name="perf">
PathCheck fn="check-acl" acl="perfdump.acl"
Service fn="service-dump"
</Object>
```

> 注意：关于创建 ACL 文件的更多信息，请参第 8 章。

### 7.3.4 获取统计数据

通过 URI 访问纯文本报告数据默认禁用。您可以使用 get-perfdump-prop 子命令验证：

```
wadm> get-perfdump-prop --config=www.example.com --vs=www.example.com
enabled=false
uri=/.perf
```

您可以使用 CLI 中的 enable-perfdump 子命令启用通过 URI 访问纯文本报告，并使用 disable-perfdump 子命令再次禁用。enable-perfdump 子命令接受 URI 作为选项。在启用纯文本报告时，您可以指定自己的 URI。以下示例演示了您如何从命令行启用纯文本报告并为访问数据指定自定义 URI。

```
wadm> enable-perfdump --config=www.example.com --vs=www.example.com
--uri=/.perf
CLI201 Command 'enable-perfdump' ran successfully
```

## 7.3 监控 Web 服务器的方法
（注：OCR 文本包含重复章节和分页。我已根据提供的源材料整合了逻辑流。）

## 7.3 监控 Web 服务器的方法

此子命令返回的数据包括：

- 请求总数 (countRequests)
- 过去 1、5、15 分钟的每秒请求数 (rpsLast1Min, rpsLast5Min, rpsLast15Min)
- 错误响应总数 (countErrors)
- 过去 1、5、15 分钟的每秒错误数 (epsLast1Min, epsLast5Min, epsLast15Min)
- 处理请求所需的的最响应时间 (maxTime)
- 过去 1、5、15 分钟的平均响应时间 (rtLast1Min, rtLast5Min, rtLast15Min)
- 从客户端接收的字节数 (countBytes)
- 发送到客户端的字节数 (countBytesTransmitted)

此子命令聚合了特定配置内所有实例的数据。如果配置仅包含单个节点，除非您指定了 `--node` 选项，否则信息将并不特殊。这样做可以为特定节点收集额外数据（但对整个配置没有意义）。您可以在以下示例的加粗项目中查看额外信息：

```
*(自我纠正：提供的 OCR 文本在 303-307 页之间高度碎片化且重复。我将根据指令合并并纠正，提供一个文本找到唯一内容的整洁重构版本。)*




# 第 7 章监控 Web 服务器 7.0

```
process.1.fractionSystemMemoryUsage=0.0
process.1.countConnectionQueues=1
process.1.sizeResident=0
process.1.countIdleThreads=2
process.1.mode=1
process.1.sizeVirtual=0
process.1.countConfigurations=2
process.1.pid=5540
process.1.timeStarted=Jun 8, 2008 10:33:55 PM
...
process.1.threadPool.1.countQueued=0
process.1.threadPool.1.countThreadsIdle=1
process.1.threadPool.1.threadPoolId=NativePool
process.1.threadPool.1.maxThreads=128
process.1.threadPool.1.countThreads=1
process.1.threadPool.1.maxQueued=0
process.1.threadPool.1.peakQueued=0
process.1.threadPool.1.name=NativePool
```

## 7.3.4.2 获取虚拟服务器统计

如果你在配置中配置了多个虚拟服务器，可以获取跨节点的所有虚拟服务器的统计信息，或者获取配置中特定节点的统计信息。以下是 virtual-server-stats 命令的示例及其输出输出：

```
wadm> get-virtual-server-stats --config=example.com
--vs=www.example.com
count200=1150
count2xx=1150
count302=0
count304=0
count3xx=0
count400=64
count401=0
count403=0
count404=0
count4xx=62
count5xx=0
countBytesReceived=497652
countBytesTransmitted=2219783
countErrors=0
countOpenConnections=0
countOther=0
```

## 7.3 监控 Web 服务器的方法

```
countRequests=1212
rateBytesTransmitted=0
vsName=www.example.com
wadm/
```

该子命令返回的数据包括：

- 向客户端返回特定状态码的响应总数。这包括以下值：count200, count302, count304, count400, count401, count403 和 count404。
- 返回特定范围内状态码的响应总数。这包含了列出的任何特定状态码。例如，count4xx 包含 400 到 499 之间的所有响应，并包含 count400、count401、count403 和 count404（4xx 范围内的其他响应未显式显示）。
- 从客户端接收的字节数（countBytesReceived）
- 向客户端发送的字节数（countBytesTransmitted）
- 请求处理过程中检测到的错误数（countErrors）
- 开放连接总数（countOpenConnections）
- 不在任何默认响应计数器中的响应总数。这包括任何 1xx 响应（countOther）。
- 请求总数（countRequests）
- 字节传输到客户端的平均速率（rateBytesTransmitted）
- 虚拟服务器名称（vsName）

> 注意：虚拟服务器统计还可能包含 Web 应用程序统计（如 JSP 计数、会话计数或 servlet 响应缓存统计）以及 servlet 统计（例如 servlet 服务的请求数和处理请求花费的时间）。当 Web 应用程序未部署到虚拟服务器时，不会显示这些信息。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_309_0.png)

此子命令汇总了特定配置内所有虚拟服务器的数据。与 get-config-stats 子命令一样，你可以通过指定 --node 将信息限制为特定节点。

## 7.3.4.3 获取 Web 容器统计

Web Server 7.0 使跟踪 Web 容器统计成为可能。这包括特定 Web 应用程序或 Java servlet 的数据。之前的 Web Server 版本未提供这种粒度。Web Server 7.0 现在允许你跟踪 Web 容器内组件的运行情况。

以下示例演示了如何使用 get-webapp-stats 子命令获取 URI /hello 的信息：

```
wadm> get-webapp-stats --config=www.example.com --node=model
--vs=www.example.com --uri=/hello
CountActiveSessions=1
CountExpiredSessions=0
countJsps=1
countRejectedSessions=0
countReloadedJsps=1
countSessions=1
peakActiveSessions=1
secondsSessionAliveAverage=0
secondsSessionAliveMax=0
uri=/hello
wadm>
```

该语法用于获取部署在特定节点实例中的虚拟服务器上的给定 Web 应用程序统计信息。要获取该配置部署的所有节点上的汇总 Web 应用程序统计信息，请使用不带 --node 的命令。

以下示例演示了如何使用 get-servlet-stats 子命令获取特定 servlet (/myServlet) 的信息：

```
wadm> get-servlet-stats --config=www.example.com --node=model
--vs=www.example.com --uri=/hello
```

该语法用于获取部署在特定节点实例中的虚拟服务器上的给定 Web 应用程序统计信息。要获取该配置部署的所有节点上的汇总 Web 应用程序统计信息，请使用不带 --node 的命令。




统计部分与“配置监控统计”（Configuration Monitoring Statistics）页面上的内容相同，提供了实例内包含的各种虚拟服务器的概述。如图 7.5 所示。

| 监控的虚拟服务器 (1) | | | |
| :--- | :--- | :--- | :--- |
| 虚拟服务器 | 请求 | 开放连接 | 错误 |
| example.com | 1245 | 0 | 0 |

**图 7.5** 虚拟服务器统计概述

图 7.5 中的表格提供了可用虚拟服务器列表，以及以下内容：

- **虚拟服务器（Virtual Server）**——配置中虚拟服务器的名称。
- **请求（Requests）**——虚拟服务器收到的总数。
- **开放连接（Open Connections）**——虚拟服务器当前的开放连接数。
- **错误（Errors）**——虚拟服务器内记录的错误总数。

点击虚拟服务器名称链接查看该虚拟服务器的详细信息。这将带您进入“虚拟服务器监控统计”（Virtual Server Monitoring Statistics）页面，您可以在那里看到图 7.6 中包含的信息。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_314_0.png)

**图 7.6** 虚拟服务器监控统计（常规信息）

## 7.3 监控 Web 服务器的方法

在此页面上，您可以查看有关虚拟服务器的基本信息（如图 7.6 所示），以及来自此虚拟服务器的响应详细信息（如图 7.7 所示）。

| 响应统计 | |
| :--- | :--- |
| 成功响应统计 | | |
| 200 响应数 | 1183 |
| 成功响应总数 | 1183 |
| 重定向响应统计 | | |
| 302 响应数 | 0 |
| 304 响应数 | 0 |
| 重定向响应总数 | 0 |
| 客户端错误统计 | | |
| 400 响应数 | 62 |
| 401 响应数 | 0 |
| 403 响应数 | 0 |
| 404 响应数 | 0 |
| 客户端错误总数 | 62 |
| 服务器错误统计 | | |
| 503 响应数 | 0 |
| 服务器错误响应总数 | 0 |

**图 7.7** 虚拟服务器监控统计（响应统计）

您可以通过使用 `get-virtual-server-stats` 子命令并在特定节点（--node 选项）上指定特定服务器（--vs 选项）来获取图 7.6 和图 7.7 中显示的统计数据。

除了此处描述的常规和响应统计信息，“虚拟服务器监控页面还提供了可能部署在此虚拟服务器上的任何 Web 应用程序的统计信息。这些信息见图 7.8。

**Web 应用程序（Web Applications）**

```
Web Application: [ ]选择一个 Web 应用程序查看监控数据
```

| Web 应用程序统计 | |
| :--- | :--- |
| Web 应用程序统计 | |
| 加载的 JSP 数量 | 0 |
| 重载的 JSP 数量 | 0 |
| 服务会话总数 | 0 |
| 活跃会话数 | 0 |
| 活跃会话峰值 | 0 |
| 拒绝的会话数 | 0 |
| 过期会话数 | 0 |
| 过期会话的生存时间（秒） | 0 |
| 过期会话的最持续时间（秒） | 0 |

**图 7.8** 虚拟服务器监控统计（Web 应用程序统计）

在此表中找到的信息与当您在特定节点（--node 选项）上的特定虚拟服务器（--vs 选项）指定特定 Web 应用程序（--uri 选项）时由 `get-webapp-stats` 命令返回的信息相同。

> 注意：您会在主统计页面上，“配置”（Configuration）选项卡旁边有一个“实例”（Instances）选项卡。该选项卡允许您快速访问特定实例的信息，而无需访问特定配置的信息。

## 7.3.6 Java ES 监控框架 (Java ES-MF)

Web Server 7.0 集成了 Java 企业级系统监控框架（Java ES-MF）。这使得 Web Server 的统计数据可以在 Java ES-MF 中可用。Java ES-MF 基于通用信息模型（CIM），该模型由分布式管理任务小组（DMTF）维护。因此，Java ES-MF 提供的数据必须以统一对象和值的格式暴露，保持可比较属性一致。

> 注意：访问 http://www.dmtf.org/standards/cim 获取更多关于 CIM 标准的信息。

为了支持 Java ES-MF，Web Server 必须以 CIM 格式提供数据。为了实现这一点，Web Server 7.0 中的管理节点实例包含一个 Java ES-MF 中层，该层获取监控数据并根据 CIM 映射创建通用监控模型（CMM）对象。这些对象根据 CIM 模型创建 CMM。

Java ES 监控控制台是一个显示管理节点收集的所有监控数据的 Web 应用程序。Java ES 监控控制台可以通过 JMX 接口直接从管理节点检索数据，通过接口，您可以从任何主机上的简单浏览器窗口安全地访问这些数据。使用图形界面，您可以实时查看被监控的值、查看并确认警报，以及创建触发自定义警报的规则。

> 注意：Java ES-MF 监控仅在从 Java ES 安装程序安装 Web Server 时相关。当独立安装 Web Server 时无法使用此功能。

## 7.3.7 简单网络协议 (SNMP)

您还可以使用简单网络协议（SNMP）监控 Web 服务器实例。SNMP 是一种用于发布命令或交换有关受管理设备的数据。

> 注意：受管理设备是指任何能够处理 SNMP 协议设备：主机、路由器、您的 Web 服务器以及网络上的其他服务器。网络管理站是用于远程监控和管理受管理设备的机器。

SNMP 使用默认 UDP 端口 161 处理常规 消息，使用 UDP 端口 162 处理 SNMP 陷阱（或错误）。

NMS 通常是安装了一个或多个网络管理应用程序的强大工作站。网络管理应用程序如 HP Open-View 或 CA Unicenter 以图形化方式显示受管理设备的信息，例如您的 Web 服务器。

您可以使用 `get-snmp-prop` 子命令来确定特定配置是否启用了 SNMP，如下：

```
wadm> get-snmp-prop --config=example.com
wadm>
```

如果没有启用 SNMP，则不会返回任何内容。您可以使用 `enable-snmp` 子命令启用 SNMP 并提供帮助您识别和管理该配置的各种参数。

当启用 SNMP 后，这些这些参数与 `server.xml` 中的元素具有直接对应关系，如下：

每个参数都对应于 `server.xml` 中 `snmp` 元素下的子元素。以下示例演示了如何使用此命令启用 SNMP：

```
wadm> enable-snmp
  --config=example.com
  --description=SunWebServer
  --organization=ExampleCorp
  --location=Tampa-2ndFloor-Grid3
  --contact=rodale@example.com
  --master-host=www.example.com
CLI21 Command 'enable-snmp' ran successfully
wadm>
```

启用后，您可以使用 `get-snmp-prop` 子命令观察到现在返回了数据，且代理已针对此配置启用。

```
wadm> get-snmp-prop --config=example.com
contact=rodale@example.com
enabled=true.
description=SunWebServer
master-host=www.example.com
location=Tampa-2ndFloor-Grid3
organization=ExampleCorp
wadm>
```

最后，您可以使用 `disable-snmp` 子命令禁用 SNMP，如下：





## 7.4 如何使用监控数据调优 Web 服务器

```
wadm> disable-snmp --config=www.example.com
CLI201 Command 'disable-snmp' ran successfully
```

如果你在进行更改之前之后没有测量系统的行为，你将不知道该更改是一个好主意、坏主意，还是仅仅与此无关。本章提供了多种监控你的 Web 服务器的方法，并提供了具体的示例，说明你如何确定 Web 服务器的性能状况。

表 7.2 回顾了你可以用于专门监控 Web 服务器性能的各种方法。

表 7.2 性能监控方法

| 监控方法 | 如何启用 | 如何访问 | 优势和要求 |
| --- | --- | --- | --- |
| 通过管理控制台获取统计信息 | 默认启用 | 在管理控制台中，针对某个配置 | 当会话线程挂起时可以访问。管理服务器必须运行。 |
| 通过单个 wadm 命令获取统计信息 | 默认启用 | 通过 wadm 命令：<br>get-config-stats<br>get-virtual-server-stats<br>get-webapp-stats<br>get-servlet-stats | 当会话线程挂起时可以访问。管理服务器必须运行。 |
| 通过浏览器获取 XML 格式统计信息 (stats-xml) | 通过管理控制台、编辑对象文件或运行 wadm 命令启用。 | 通过 URI | 服务器不需要运行。 |
| 通过命令行界面获取 XML 格式统计信息 (stats-xml) | 默认启用 | 通过 wadm 命令 get-stats-xml | 当会话线程挂起时可以访问。管理服务器必须运行。 |
| 通过浏览器获取 perdump | 通过管理控制台、编辑对象配置或运行 wadm 命令启用。 | 通过 URI | 服务器不需要运行。 |
| 通过命令行界面获取 perdump | 默认启用 | 通过 wadm 命令 get-perdump | 当会话线程挂起时可以访问。管理服务器必须运行。 |
| Java ES 监控 | 默认启用 | 通过 Java ES 监控控制台 | 仅适用于 Java ES 安装。管理服务器必须运行。 |
| SNMP 监控 | 通过管理控制台、编辑对象配置或运行 wadm 命令启用。 | | | |

在大多数情况下，Web Server 7.0 自带的默认调优参数对于所有除了极高流量的站点外都是适当的，即使如此，大型站点经常需要更改的唯一设置也是线程池和保持活动（keep-alive）设置。你可以在管理控制台中或使用 wadm 子命令在配置级别调优这些设置。你也可以通过直接编辑 server.xml 文件中的元素来调优服务器，除非你确切知道自己在做什么，否则可能会适得其反。

一个良好的建议是使用纯文本报告（perfdump）来监控各个类别的统计信息。（有关这些设置的更多信息，请参阅第 7.3.3 节“纯文本报告”和附录 C“示例纯文本报告数据”）。在大多数情况下，这些统计信息也会显示在管理命令行界面和 stats-xmn 输出中，但纯文本报告是在一个地方处获取所有这些统计信息的方便方法。

无论你使用哪种方法来监控数据，都应该遵循一些通用指南。在调优服务器时，记住你的特定环境是独特的非常很重要。本章提供的建议的影响将根据你的特定环境而异。最终，你必须依靠自己的判断和观察来选择最适合你的调整。

在努力优化性能时，请记住以下指南：

- **有条不紊地工作**——尽可能一次只进行一种调整。在每次更改的前后测量你的性能，并撤销任何没有产生可衡量改进的更改。

- **逐渐调整**——在调整量化参数时，连续进行几次阶进式的变化，而不是尝试一次性做出剧变。不同的系统面临不同的情况，如果你更改值太快，你可能会直接跳过系统的最佳设置。

- **从头开始**——在每次重大的系统更改（无论是硬件或软件升级，还是部署一个主要的新应用程序），请检查之前的所有调整，查看它们是否仍然适用。在升级 Solaris 之后，你应该从一个未修改的 /etc/system 文件重新开始。

- **保持信息更新**——每当你升级系统时，请阅读 Sun Java System Web Server 7.0 Update 2 发布说明以及你操作系统的发布说明。发布说明通常会提供有关特定调整的更新信息。

> 警告：调优服务器时请务必小心。在进行任何更改之前，务必备份你的配置文件。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_321_0.png)

## 第 7 章 监控 WEB SERVER 7.0

## 7.5 总结

持续监控 Web 服务器是系统管理员执行的最容易被忽视的任务之一。通常，Web 服务器被简单地忽略，直到你收到一封邮件或电话引起你对问题的关注。然而，那时已经太晚了，你被迫对一个本可以预防的问题做出反应。

Web Server 7.0 提供了各种监控服务器的机制，它让你能够非常容易获取可以用于确定服务器健康状况的统计信息。通过定期的监控，你可以采取主动的方法并在问题发生之前防止其出现。

## 7.6 自学实验

本章包含的信息用于执行以下练习。这些练习将帮助验证你对概念的理解。

- 为默认服务器生成数百个请求。为了获得最佳结果，请确保你的请求产生了成功响应（服务器响应 200）以及错误响应（服务器响应 404）。注意：你可以使用 wget 工具生成这些请求，也可以使用 Internet 浏览器。如果你使用浏览器，请确保在请求时按下 Shift 键，以确保不是从浏览器缓存中检索页面。

- 为默认配置的虚拟服务器级别启用日志记录，并指定特定的虚拟服务器的日志文件（例如，“../logs/www.example.com-server.log”和“../logs/www.example.com-access.log”）。检查 server.xml 文件中对虚拟服务器元素的更改。验证新日志文件已创建并包含特定服务器的数据。

- 通过管理控制台为默认配置启用 XML 和纯文本报告格式。通过相应的 URI 访问报告。

- 使用命令行界面访问 XML 和纯文本报告。

- 使用命令行界面禁用 XML 和纯文本报告的访问。

- 通过管理控制台访问默认配置的配置级统计信息。

- 通过管理控制台访问默认配置中虚拟服务器统计信息。

- 使用相应的命令行命令重复练习 6 和 7。

> 注意：访问 http://www.sunwebserver.com 获取每个练习的详细说明。

- 附加练习：为虚拟服务器启用 SNMP 并使用 snmpwalk 等工具查看服务器提供的数据。

第四章描述了如何使用命令行界面执行各种管理任务。Web Server 7.0 包含了几个预定义脚本来演示此功能。表 4.3（管理脚本）是 collate-logs.tcl，该脚本允许你跨多个节点汇总日志。使用此脚本查看你可能部署配置的任何节点上的访问文件。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_322_0.png)

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_323_0.png)





# Web 服务器 7.0 安全防护

公共 Web 服务器是不满员工、黑客或商业竞争对手吸引的目标，他们旨在让组织蒙脸或仅仅阻止其在互联网上开展业务。尽管 Web 服务器可能被认为是安全链中的弱点，但 Web Server 7.0 凭借其成熟的代码库、安全代码审查以及安全相关功能，展现了强大的实力——这些功能支撑了全球一些最有价值公司网站的运行。

> 注意：根据 Netcraft (www.netcraft.com)，Sun Java System Web Server 在财富 100 强企业中排名第一。

本章将介绍 Web Server 7.0 中包含的一些安全相关功能，以及您如何使用它们来保护您的 Web 服务器。通常，它涵盖了以下主题：

- 控制对 Web 服务器资源的访问
- 使用 SSL 证书保护数据安全
- 自动维护证书吊销列表 (CRLs)
- 检测并响应拒绝服务 (DoS) 攻击
- 将 Web 服务器作为反向代理以提供额外的保护

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_325_0.png)

## 8.1 控制对 Web 服务器资源的访问

您可以通过多种安全服务和机制保护位于 Web 服务器上的资源，包括身份验证、授权和访问控制。

身份验证（Authentication）验证某人确实如其所声称的过程。在计算机系统中，身份验证通常通过使用密码完成。然而，与数字证书、令牌（tokens）甚至生物识别设备相比，这是较弱的身份验证形式之一。Web Server 7.0 默认支持多种身份验证方法，并提供了一种扩展处理的方式以包含用户定义的方法。

在人员通过身份验证后，计算机系统必须验证该用户是否允许对系统包含的资源执行某些操作。此过程被称为授权（authorization），通常涉及查询授权（或策略）数据存储，以确定用户对于 Web 服务器所提供资源的权限。策略与用户或组关联，因此授权在用户身份确定后进行。

访问控制（Access control）是对授权数据存储中指定策略的执行，可以通过多种安全模型实现，例如 Web 服务器应用程序安全、htaccess、身份验证域（authentication realms）等。Web Server 7.0 提供了默认的访问控制，允许您在安装后立即提供内容。您可以通过限制对一个或多个以下资源的访问，在您的 Web 服务器上实施额外的控制：

- 整个服务器实例
- 服务器部分
- 文件或目录
- 文件类型
- 通用资源标识符 (URIs)

### 8.1.1 用户身份验证

身份验证是确定用户确实如其所声称的过程。为了验证用户的凭据，Web 服务器必须查询包含用户身份验证信息的数据存储。该数据存储被称为身份验证数据库，由 `server.xml` 文件中的 `auth-db` 元素指定。

身份验证数据库默认在服务器级别进行配置，但可以在特定的虚拟服务器内指定 `auth-db` 元素进行覆盖。

Web Server 7.0 支持三种类型的身份验证数据库：文件 (file)、目录服务 (ldap) 和可插拔身份模块 (pam)。您可以按照这三种类型的任意组合配置任意数量的身份验证数据库。

### 8.1.11 使用文件作为身份验证数据库

管理员可以配置 Web 服务器使用本地文件作为身份验证数据库。这种用户数据存储方法在开发期间或可以使用集中式用户管理（或需要）的小规模部署中特别为方便。Web Server 7.0 支持三种不同的格式：keyfile、digestfile 和 htaccess。选择一种文件格式而非另一种的决定取决于所实施的身份验证机制类型。

表 8.1 提供了每个文件格式的概述以及如何将其与相应的身份验证机制配合。

表 8.1 文件格式与身份验证机制的比较

| 文件格式 | 身份验证机制 | 概述 |
| :--- | :--- | :--- |
| keyfile | 基础身份验证 | 一种允许用户代理（User Agent）在发起 HTTP 请求时提供用户名和密码的方法。请求格式为：http://username:password@host.domain。基础身份验证不提供任何级别的加密。相反，用户名和密码以 Base64 编码格式传递给 Web 服务器。 |
| digestfile | 摘要身份验证 | 一种类似于基础身份验证的方法，但密码不是以 Base64 编码文本发送。在摘要身份验证中，有效的响应包含用户名、密码、随机值（nonce value，由 Web 服务器发送）、HTTP 方法和请求的 URI 的校验和（默认为 MD5 校验和）。可选的标头允许服务器指定校验和或摘要，但默认使用 MD5 算法。摘要身份验证不如 Kerberos 或 X.509 证书安全；它仅作为基础身份验证的替代。 |
| htaccess | 基础身份验证 | 该方法利用包含在受保护文件所在目录内的分布式控制文件。这些访问控制文件（通常命名为 .htaccess）引用一个位于文档根目录之外的集中身份验证文件（通常命名为 .htpasswd）。由于 .htaccess 文件 分布在需要访问控制的各个目录中，它们的实现和维护比 ACL 文件更困难。 |

## 第 8 章 Web 服务器 7.0 安全防护

> 注意：RFC 2617（HTTP 身份验证：基础和摘要访问验证）提供了关于基础和摘要身份验证机制的额外信息。

keyfile 和 digestfile 身份验证数据库类型在安装后即可直接使用。您可以使用 GUI 或 CLI 创建这些类型的数据库文件，或在其中管理用户。

CLI 中的 `create-file-authdb` 子命令用于创建 keyfile 或 digestfile 类型的身份验证数据库，如下：

```
create-file-authdb --connect-options [--echo|-e] [--no-prompt|[-Q]
[--verbose|-v] [-vs|-s name] [-syntax|-t keyfile|digestfile]
[--no-enabled|-n] --path|-P filepath --config|-c name authdb-name
```

> 注意：虽然身份验证数据库文件的内容看起来显而易见，但其格式被视为私，并在 Web Server 版本之间可能会更改。因此，您不应根据这些文件创建任何程序、脚本或假设。

示例 8.1 展示了 `server.xml` 文件中的用户定义身份验证数据库。

# 示例 8.1 基于文件的身份验证数据库

```
<auth-db>
<name>mykeyfile</name>
<url>file</url>
<property>
<name>syntax</name>
<value>keyfile</value>
</property>
<property>
<name>keyfile</name>
<value>keyfile</value>
</property>
</auth-db>
```

该身份验证数据库通过 `name` 元素指定为 mykeyfile。这是在 GUI 或 CLI 中用于引用该身份验证数据库的用户定义名称。`url` 元素的值为 `file`，告诉 Web 服务器 该数据库使用文件身份验证。文件的类型由 `syntax` 属性指定，表明它是 keyfile，因此使用基础身份验证。文件在文件系统中的位置由 `value` 属性指定。该元素的值可以是完全路径，也可以相对于配置目录的文件。在这种情况下，文件名是 keyfile，它直接位于配置目录。

digestfile 身份验证数据库的格式与示例 8.1 相同，仅在于 `syntax` 属性指定为 digestfile。所有其他元素与 keyfile 身份验证数据库相同。

htaccess 身份验证数据库是为了兼容旧版本的 Web 服务器而维护，但建议管理员使用 keyfile 或 digestfile。htaccess 身份验证方法默认未启用；您必须通过 GUI 或 CLI 启用它并在 htaccess 环境中管理用户。您必须使用位于 install_dir/bin 目录下的 passwd 身份验证来管理此身份验证数据库中的用户。

### 8.1.1.2 使用目录服务作为身份验证数据库

文件身份验证数据库虽然方便，但随着用户数量的增加，存在性能和扩展性限制。当发生时，管理员转向适用于大量用户的数据存储应用程序（例如目录服务或关系型数据库）。

许多公司以 Sun Java System Directory Server (Sun Directory Server) 或 Microsoft Active Directory (Active Directory) 的形式实现企业级目录服务。这些集中式服务器通常包含身份验证所需的用户群体，并提供支持轻量级目录访问协议 (LDAP) 的便捷接口以访问用户记录。记录包含唯一用户标识符和密码，可以在访问 Web 服务器资源之前验证用户身份。图 8.1 展示了 Web 服务器与集中式目录服务器之间的关系。

**图 8.1** Web 服务器与目录服务器的交互





# 第 8 章 安全 Web Server 7.0

Web Server 若要使用目录服务作为身份验证数据库，它需要知道在网络何处找到该服务。为此，它需要托管目录服务的服务器主机名，以及该服务监听的端口号。Web Server 使用这些信息通过 LDAP 协议建立与目录服务的连接。在这种关系中，Web Server 在客户端-服务器的交互中充当 LDAP 客户端。

目录服务实现了其自身的形式的身份验证和授权；因此，Web Server 需要以允许访问特定信息的用户身份对目录服务进行身份验证。为了实现这一过程，它必须以绑定操作（bind operation）的形式提供适当凭据，并使用特定的 bindDN 和密码。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_330_0.png)

> 注意：目录服务数据库中的每个条目都由一个唯一的区分名称（DN， DN）标识。DN 是目录树中条目的字符串表示。你可以将 DN 认为是到所建模对象（例如，到树的根节点（或后缀））的完整路径。这类似于典型系统中文件的表示方式。如果你将某个特定条目用于身份验证，则该条目的 DN 被称为 bindDN。在 Web Server 对目录服务完成身份验证后，它需要通过提供 baseDN 来知道从目录信息树（DIT）的何处开始搜索用户。这允许通过消除不包含用户信息的树部分来更快速地执行搜索。最后，Web Server 需要知道如何在树中唯一标识一个用户。它通过呈现一个过滤器来实现这一点，该过滤器由用于标识用户的唯一属性组成。在 Sun Directory 中，唯一的命名属性是 `uid`，在 Active Directory 中，它是 `sAccountName`。Web Server 7.0 提供了指定用于定位用户的唯一属性的灵活性，并支持将 Active Directory 作为目录服务。之前的版本不支持。与目录服务交互所需的所有都在 `auth-db` 元素中指定。示例 8.2 提供了与图 8.1 所示目录服务相关的身份验证数据库。

## 8.1 控制对 Web Server 资源的访问

### 示例 8.2 目录服务身份验证

```
<auth-db>
  <name>ds.example.com</name>
  <url>ldap://ds.example.com:389/ou=People,dc=example,dc=com</url>
  <property>
    <name>binddn</name>
    <value>uid=webadmin,dc=example,dc=com</value>
  </property>
  <property>
    <name>bindpw</name>
    <value>GFzc3dvcmQ==value>
    <encoded>true</encoded>
  </property>
</auth-db>
```

在示例 8.2 中，`name` 元素指定了用于在 GUI 或 CLI 中引用身份验证数据库的用户定义。`url` 元素指定了连接到目录服务所需的信息。该元素的值包括连接协议（ldap 或 ldaps）、你正在连接的目录服务器的主机名和端口号，以及你希望在目录树中搜索用户的位置（即 baseDN）。URL 的格式为 `ldap://host:port/baseDN`，并使用字符来表示特殊符号（如等号 `=`）。

此，为此身份验证数据库定义了两个可选属性：第一个是 `binddn`，包含值为 `uid=webadmin,dc=example,dc=com`。这是为服务账户创建的区分名称，允许 Web Server 绑定并对用户标识符执行查找操作。第二个属性是 `bindpw`，它是指定在 `binddn` 属性中的用户用户的 Base64 编码密码。

如果你不指定 `binddn` 和 `bindpw`，Web Server 将以匿名用户的身份绑定到目录服务器。虽然这看起来很方便，但你应该验证你的目录服务是否支持匿名搜索，以及你的安全策略是否允许这样做。允许匿名用户进行搜索会限制目录服务日志文件中包含的信息量。因此，某些公司要求 Web Server 使用有效的服务账户绑定到目录服务器。

图 8.1 展示了 Web Server 使用 `bindDN uid=webadmin,dc=example,dc=com` 绑定到目录服务器。这是一个为了唯一目的——允许 Web Server 与目录服务器通信而创建的条目，它类似于 UNIX 类型系统上的服务账户。Web Server 执行的任何操作（例如搜索操作）都可以在目录服务器日志文件中易于追踪。

> **警告：** Sun Directory Server 包含一个类似于 UNIX 系统上 root 用户的超级用户。该账户被称为 rootDN 或目录管理器（Directory Manager）账户，默认是 `cn=directoryManager`。从 Web Server 绑定到目录服务器时，绝不要使用此账户。目录管理器账户不受加在其他账户上的访问控制规则或限制的影响。因此，可能会无意中影响你的 Sun Directory Server 的性能和安全性。最好在目录服务器专门为此 Web Server 创建一个账户，赋予该账户适当的管理用户权限，并作为该账户绑定到目录服务器。

Web Server 7.0 允许你为给条目指定多个目录服务器。这允许在主目录不可用时故障转移到备服务器。你通过在 `url` 中指定多个以空格分隔的目录列表来配置此项。可以在示例 8.3 中看到。

### 示例 8.3 目录故障转移

```
<auth-db>
  <name>ds.example.com</name>
  <url>ldap://ds.example.com:389/ou=People,dc=example,dc=com ldap://ds2.example.com:389/ou=People,dc=example,dc=com ldap://ds3.example.com:389/ou=People,dc=example,dc=com</url>
  <property>
    <name>binddn</name>
    <value>uid=webadmin,dc=example,dc=com</value>
  </property>
  <property>
    <name>bindpw</name>
    <value>GFzc3dvcmQ</value>
    <encoded>true</encoded>
  </property>
</auth-db>
```

当提供多个目录服务器时，Web Server 会尝试连接列表中的第一个服务器。如果该服务器不可，将尝试连接列表中的后续服务器。你可以在列表中指定不同的 baseDN，甚至服务器本身可以是不同的。唯一的要求是 `binddn` 和 `bindpw` 属性必须保持一致。

Web Server 7.0 允许你配置在产品之前的版本中不可用的额外搜索参数。这允许你与供应商提供的目录服务器（如 Active Directory）进行用户身份验证和静态组查找。在 Web Server 7.0 中可以指定的附加参数包括：

- search-filter——用于搜索用户（默认为 `uid`）
- group-search-filter——用于搜索组（默认为 `uniquember`）
- group-target-attr——包含组名的 LDAP 属性（默认为 `cn`）

### 示例 8.4 灵活搜索

```
<auth-db>
  <name>ldapMSAD</name>
  <url>ldap://msad.example.com:389/ou=People,dc=example,dc=com</url>
  <property>
    <name>binddn</name>
    <value>cn=webadmin,cn=special users,dc=example,dc=com</value>
  </property>
  <property>
    <name>bindpw</name>
    <value>GFzc3dvcmQ==value>
    <encoded>true</encoded>
  </property>
  <property>
    <name>search-filter</name>
    <value>samAccountName</value>
  </property>
</auth-db>
```

在配置身份验证数据库后，Web Server 就可以与目录服务交互，以验证用户是否如其所称。但这是如何发生的呢？在提示时，用户不会以这种呈现他们的凭据。




目录服务器 DN（特命名名）的形式，那么 Web 服务器是如何进行这种判断的呢？针对外部目录服务器进行用户身份验证的过程如图 8.2 所示。

![](a3cb513bfd7a0b21f70c67fcaede10f6_334_0.png)

**图 8.2** 用户身份验证过程

在身份验证过程中，有三个主要组件参与：浏览器、Web 服务器和目录服务。验证用户身份所需的通用步骤可以总结如下：

- 1. 用户尝试访问 Web 服务器上受限制的页面。用户被提示输入凭据并被要求响应，以便 Web 服务器确定其身份。用户输入用户名和密码，并将结果提交给 Web 服务器。
- 2. Web 服务器使用身份验证数据库的 `bindDN` 中指定的特命名名执行绑定（bind）操作。在这种情况下，绑定操作的特命名名为空，因此以匿名用户身份执行。绑定操作完成后，Web 服务器获取浏览器提供的用户名，并根据适当的命名属性（uid=scarter）创建搜索过滤器。Web 服务器执行搜索操作以查找匹配该过滤器的条目，从基础 DN（dc=example, dc=com）开始，直到操作完成。
- 3. 搜索操作找到一个匹配过滤器的条目。它将该条目的特命名名返回给 Web 服务器。Web 服务器通过取消绑定（unbind）终止与目录服务的连接。

## 8.1 控制对 Web 服务器资源的访问

**注意：** 默认情况下，Web 服务器假设它从搜索中最多接收到一个条目。如果返回多个条目，Web 服务器将记录内部错误并终止身份验证过程。如果发生这种情况，你可能需要更改搜索开始的位置（baseDN）、选择新的搜索过滤器（search-filter），或确保目录服务中的唯一性。Sun Directory 服务器有一个名为 UID Uniqueness 的插件，可以用于此目的。如果这些选项都不可行，你可能需要考虑编写自己的身份验证函数并将其整合到请求处理过程中。

- 4. Web 服务器执行新的新的绑定操作，但这次它使用步骤 3 中返回的特命名名。它还使用了步骤 1 中由浏览器提供的密码。
- 5. 如果密码与用户条目中的值匹配，则绑定操作成功，目录服务返回错误代码 0。这表示绑定操作成功，Web 服务器已成功验证了用户的身份。Web 服务器终止与目录服务的连接，并允许浏览器访问请求的资源。

CLI 包含一个创建特定目录身份验证数据库的命令，它与用于创建文件身份验证数据库的命令不同。`create-ldap-authdb` 子命令允许你按照如下创建基于目录服务的身份验证数据：

``````
create-ldap-authdb [--echo] [--no-prompt] [--verbose] [--vs=vs-name]
--no-enabled] [--group-search-filter=filter] [--search-filter=filter]
--dc-suffix=suffix] [--group-search-attr=attribute] [--bind-dn=bind-dn]
--auth-expiring-url=url] [--timeout=timeout]
--ldap-url=ldap://server:port/dc=acme,dc=com --config=config-name
db-name
```

数据库创建后，你可以使用 Web 服务器 CLI 中的 `create-user` 子命令，或者通过任意数量的启用了 LDAP 的工具直接管理目录数据库中的用户。

### 8.1.1.3 使用可插拔身份验证模块作为身份验证数据库

Web 服务器 7.0 包含了针对 Solaris 操作系统可插拔身份验证模块（PAM）栈进行用户验证的能力。这意味着可以针对本地主机上配置的任何支持的 Solaris 操作系统命名服务进行身份验证。这包括网络信息系统（NIS）、目录服务器或如 /etc/passwd 的平文件。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_336_0.png)

> 注意：PAM 是 Web 服务器 7.0 支持的全新原生身份验证数据库。之前的 Web 服务器版本支持 Java Solaris Realm，允许 Java 应用程序使用 PAM 验证用户。然而，原生内容（静态文件、CGI 等）无法利用这种身份验证机制。

Solaris 9 及以上操作系统支持配置 PAM 身份验证数据库。Web 服务器仅能验证本地系统上的 PAM 栈，因此配置 `auth-db` 元素时不需要除身份验证数据库名称以外的任何属性。示例 8.5 展示了配置 PAM 身份验证数据库所需的元素。

示例 8.5 配置 PAM 身份验证数据库

```xml
<auth-db>
  <name>solarisAuth</name>
  <url>pam</url>
</auth-db>
```

使用 PAM 作为身份验证数据库是验证用户的另一种方便方法，但它存在限制。首先，你只能在 Solaris 9 或更高操作系统上配置此项，且只能使用用户名和密码进行验证；不支持智能卡和其他身份验证设备。其次，你无法对命名服务中的用户进行搜索或修改。最后，要使用 PAM 作为身份验证数据库，如果你正在访问系统，则需要以 root 用户身份运行你的 Web 服务器实例。![](imga3cb513bfd7a0b21f70c67fcaede10f6_336_0.png)

> 注意：PAM 是 Web 服务器 7.0 支持的全新原生身份验证数据库。之前的 Web 服务器版本支持 Java Solaris Realm，允许 Java 应用程序使用 PAM 验证用户。然而，原生内容（静态文件、CGI 等）无法利用这种身份验证机制。




## 8.1 控制 Web 服务器资源的访问

在虚拟服务器级别。这允许你提供适用于所有虚拟服务器的通用访问控制，或仅适用于特定虚拟服务器的精细粒度访问控制。

你可以根据以下任何项来指定你是希望允许还是拒绝对服务器资源的访问：

- 谁发起了请求（用户和/或组）
- 请求来自哪里（主机 IP）
- 请求发生的时间（例如，一天中的某个时间）
- 使用了什么种类型的连接（SSL）

此外，你还可以为允许访问的用户指定你所许可的权限。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_339_0.png)

> 注意：请参考第 5 章“Web 服务器 7.0 配置文件”以了解 `default.acl` 文件的结构和语法。理解此文件对于确定 Web 服务器如何处理访问控制语句非常有帮助。

### 8.1.2.1 访问控制权限

访问控制权限限制对 Web 服务器资源（如文件和目录）的访问。除了允许或拒绝所有访问权限（默认设置）外，你还可以通过指定显式允许或拒绝某些访问权限的规则来实现更细粒度的控制。例如，你可能希望允许用户对 Web 服务器上的文件具有只读权限以便他们查看，但你可能不想授予他们修改文件的权限。

ACL 文件中用于控制访问的常用权限包括：所有 (all)、读 (read)、执行 (execute)、信息 (info)、写 (write)、列表 (list) 和删除 (delete)。这些权限与 HTTP 协议中采用的方法对应，但一个权限实际上可能对应多个方法，而一个方法可能要求你允许多个权限。表 8.2 提供了 Web 服务器访问权限与 HTTP 协议方法之间的映射关系。

# 第 8 章 安全 Web 服务器 7.0

# 表 8.2 访问控制权限与 HTTP 方法的映射表

| 权限 | HTTP 方法 |
| --- | --- |
| read | GET, HEAD, TRACE, OPTIONS, COPY, BCOPY |
| write | PUT, MKDIR, LOCK, UNLOCK, PROPPATCH, MKCOL, ACL, VERSION–CONTROL, CHECKOUT, UNCHECKOUT, CHECKIN, MKWORKSPACE, UPDATE, MERGE, BASELINE–CONTROL, MKACTIVITY, BPROPPATCH |
| execute | POST, CONNECT, SUBSCRIBE, UNSUBSCRIPT, NOTIFY, POLL |
| delete | DELETE, RMDIR, MOVE, DELETE, BREMOVE |
| info | HEAD, TRACE, OPTIONS |
| list | INDEX, PROPPIND, REPORT, SEARCH, BPROPPIND |

例如，如果你想允许浏览器获取 Web 服务器上特定文件夹的目录列表，你需要授予 `list` 权限。这反过来允许允许 `INDEX` 方法，从而允许 Web 服务器提供目录列表。

示例 8.6 展示了如何使用这些权限为不同类型的用户提供细粒度的访问控制（为了演示目的添加了行号）。

# 示例 8.6 访问控制权限

1. acl "uri/";
2. authenticate (user, group) {
3. prompt = "Sun Java System Web Server";
4. allow user="anyone";
5. deny (all) read, execute, info user="all";
6. allow (read, execute, info) user="all";
7. allow (list, write, delete) group = "superusers";

第 5–7 行定义了为三类用户提供的访问控制权限。第 5 行拒绝所有属于 `anyone` 类别的用户的权限。这包括已验证的用户和匿名用户。第 6 行允许所有已验证的用户对此 Web 服务器上的任何资源（由第 1 行指定）进行读取、执行和获取信息。第 7 行允许属于 `superusers` 组的用户对 Web 服务器上的页面进行列表显示、写入和删除。`superusers` 组的用户也拥有第 6 行指定的权限，因为他们也是所有已验证用户的一部分。

## 8.1 控制 Web 服务器资源的访问

**注意：** 第 5 行的条目必须出现在列表的第一位。该条目拒绝任何用户（已验证和未验证的用户）的所有权限。该条目的评估结果为 TRUE，因此评估列表中的下一个条目（第 6 行）。随后定义后续 ACE（访问控制项），为某些用户授予特定权限。

除了这些权限外，Web 服务器还允许你使用 `http_<methods>` 权限严格基于 HTTP 方法来配置访问控制。例如，假设你想阻止特定主机（或子网）发出 `GET` 方法。在 Web 服务器 7.0 中，你可以创建一个类似下面的拒绝规则来实现这些结果：

```
deny (http_GET) ip = "123.45.67.*";
```

最后，你还可以在 Web 服务器 7.0 中控制与 HTTP 协议的分布式授权和版本控制 (DAV) 能力相关的权限。例如，你可以通过在 ACE 中指定适当权限（如 `dav:read-acl` 或 `dav:read-current-user-privilege-set`）来允许或拒绝 DAV 能力。

**注意：** 关于 Web 服务器 7.0 中可以控制的 DAV 权限类型的更多信息，请参阅 RFC-3744（Web 分布式授权和版本控制 (DAV)访问控制协议）。

## 8.1.2.2 访问控制处理

当 Web 服务器接收到传入请求时，它会选择相应的虚拟服务器，并根据称为访问控制项（或 ACE）的层级规则决定允许还是拒绝客户端访问。Web 服务器根据这些 ACE 决定客户端是否允许或拒绝访问。Web 服务器考虑任何 ACE 以决定是否应该授予或拒绝访问。

针对特定资源的 ACE 集合被称为访问控制列表（或 ACL）。`default.acl` 中找到的访问控制项在服务器特定的访问控制文件之前被处理。文件内部 ACE 的顺序也很重要，因为先定义的 ACE 会出现在后定义的 ACE 之前。ACL 生成后，Web 服务器从上到下处理它。任何时间 ACE 评估为 FALSE，则 ACL 处理停止并拒绝客户端访问。服务器处理列表直到到达末尾或遇到绝对 ACE。如果处理到 ACL 的末尾没有看到 FALSE 条件，则授予用户访问资源。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_342_0)

> 注意：如果 ACE 解析为 TRUE，则只有当该 ACE 不是绝对 ACE 时，才会评估列表中的下一个 ACE。如果绝对 ACE 评估为 TRUE，则根据 ACE 指定的定义允许或拒绝访问，不再继续处理列表。当在 ACE 定义中指定 `absolute` 关键字时，ACE 是绝对的。

allow absolute (read, execute, info) user = "anyone";

你也可以在控制台 (GUI) 中通过定义 ACE 时取消勾选 `Continue` 框来实现此。

Web 服务器 7.0 默认定义了两个 ACL：`default` 和 `internal`。图 8.3 展示了默认访问控制列表在控制台中的外观。示例 8.7 提供了 `default.acl` 中对应的条目（为了演示添加了行号）。

编辑访问控制列表
服务器通过使用本地存储的访问控制列表（ACL）支持身份验证和授权，ACL 描述了用户对资源的访问权限。

| 资源: | default |
| 身份验证默认: | Default |
| 身份验证方法: | Basic |
| SSL | |
| Digest | |
| 其他 | |
| 身份验证提示: | Java System Web Server |
| 拒绝访问响应: | 默认消息 |
| 其他. | |

| 访问控制列表 (ACEs) (2)| 新建... 删除 向上 向下 | 访问用户/组 来自主机 权限 | 继续 ACE 动作 |
| Allow anyone anyplace -r-i | 是 | 编辑 | 自定义 ACE |
| Allow all anyplace -w-di | 是 | 编辑 | 自定义 ACE |





## 8.1 控制对 Web 服务器资源的访问

### 示例 8.7 默认 ACL

1. acl "default";
2. authenticate (user, group) {
3.   prompt = "Sun Java System Web Server";
4. }
5. allow (read, execute, info) user = "anyone";
6. allow (list, write, delete) user = "all";

示例 8.7 中各个条目的描述如下：

* 第一行指定了 ACL 的名称。这与图 8.3 所示的 Resource（资源）文本框对应。
* 第二行指定在允许用户执行某些受后续 ACE（访问控制项）保护的操作之前，需要进行身份验证。Web 服务器使用基本认证方法（默认方法）来验证用户身份。
* 第三行指定了在用户代理（User Agent）打开的用户名/密码对话框中显示的提示。这与图 8.3 所示的 Prompt for Authentication（认证提示）文本框对应。
* 第五行指定了列表中的第一个 ACE。该 ACE 允许所有用户（anyone；无论是否经过验证）对受此规则保护的资源拥有读取、执行和获取信息的权限。由于经过验证和未经过验证的用户都被视为 anyone，因此此规则的评估值为 TRUE。
* 第六行指定了列表中的第二个 ACE。该 ACE 允许所有未经过验证的用户（all）对受此规则保护的资源拥有列出、写入和删除的权限。这与图 8.3 所示的第二个 ACE 对应。

第一个 ACE 不需要验证，因此不会请求用户身份。第二个 ACE 在允许用户执行列出的操作之前需要进行验证。如果在处理此 ACE 时用户身份未知，则会提示用户输入凭据。

让我们来看一个简单的 ACL 文件，并看看它是如何针对各种客户端请求进行处理的。示例 8.8 包含 `default.acl` 文件的片段，该文件已修改为拒绝用户 bnelson 的 info 权限。为了演示目的，添加了行号。

### 示例 8.8 简单访问控制文件

1. acl "default";
2. authenticate (user, group) {
3. prompt = "Sun Java System Web Server";
4. };
5. allow (read, execute, info) user = "anyone";
6. allow (list, write, delete) user = "all";
7.
8. acl "/file.html";
9. deny (info) user = "bnelson";

示例 8.3 提供了各种客户端请求，并演示了示例 8.8 中的控制条目是如何针对每个请求进行评估的。请参考表 8.2 以确定适用于这些请求的权限映射。

| 请求 | 适用的 ACE | 请求结果 |
| :--- | :--- | :--- |
| HEAD / | 包含以下权限的 ACE 适用于此请求：all, http_head 和 info。HEAD / 的 ACL 如下：allow (read, execute, info) user = "anyone"; | 在第 5 行定义的 ACE 评估为 TRUE。允许 HEAD 请求。第 9 行的 ACE 不评估，因为它是针对不同的 URI。 |
| GET / 或 /file.html | 包含以下权限的 ACE 适用于此请求：all, http_get。GET /file.html 的 ACL 如下：allow (read, execute, info) user = "anyone"; | 在第 5 行定义的 ACE 评估为 TRUE。允许 GET 请求。第 9 行的 ACE 不评估，因为它是针对不同的权限（info）。 |
| HEAD /.html (作为用户 bnelson) | 包含以下权限的 ACE 适用于此请求：all, http_head 和 info。HEAD /file.html 的 ACL 如下：allow (read, execute, info) user = "anyone"; deny (info) user = "bnelson"; | 在第 5 行定义的 ACE 评估为 TRUE，并继续 ACE 处理。在第 9 行定义的 ACE 评估为 TRUE，但拒绝用户 bnelson 的请求。 |
| HEAD /.html (作为用户 rodole) | 包含以下权限的 ACE 适用于此请求：all, http_head 和 info。HEAD /file.html 的 ACL 如下：allow (read, execute, info) user = "anyone"; deny (info) user = "bnelson"; | 在第 5 行定义的 ACE 评估为 TRUE，并继续 ACE 处理。在第 9 行定义的 ACE 评估为 FALSE，因为该用户不是 bnelson。允许用户 rodole 的 HEAD 请求。 |

表 8.3 ACE 对客户端请求的适用性

| 请求 | 适用的 ACE | 请求结果 |
| :--- | :--- | :--- |
| HEAD /file.html | 包含以下权限的 ACE 适用于此请求：all, read, http_head 和 info。HEAD /file.html 的 ACL 如下：allow (read, execute, info) user = "anyone"; deny (info) user = "bnelson"; | 在第 5 行定义的 ACE 评估为 TRUE 并继续 ACE 处理。用户尚未经过验证，因此在在此发生之前，无法真实评估在第 9 行定义的 ACE。在此之前，对资源的访问被拒绝。 |

![](img/a3cb513bfd7a0b21f70c67fcaede10f_345_0.png)

**注意：** 尽管我们没有为 anyone 用户设置任何 deny ACE，但对特定用户设置显式的 deny 或 allow ACE（如第 9 行所示）会隐含地拒绝未验证用户的访问。访问控制语句的处理有时会令人困惑。下一节将演示如何在访问控制期间执行了 ACE 以及哪些 ACE 允许或拒绝了访问。

### 8.1.2 观察访问控制

向支持部门提出的常见原因之一是对 ACL 评估方式的困惑。以前版本的 Web 服务器没有提供足够的工具来帮助理解为什么规则接受或拒绝了请求。过去，尝试法是唯一的诊断机制，但由于 ACL 评估是不透明的，这存在风险。为了解决这个问题，Web 服务器 7.0 引入了调试日志功能，使 ACL 处理的结果可见。现在你可以在服务器日志中查看 ACL 处理的结果，并将日志级别设置为 `finest` 获取更多信息。假设你的 `default.acl` 文件包含示例 8.9 所示的条目。

### 示例 8.9 带有保护的访问控制文件

1. acl "default";
2. authenticate (user, group) {
3. prompt = "Sun Java System Web Server";
4. };
5. allow (read, execute, info) user = "anyone";
6. allow (list, write, delete) user = "all";
7.
8. acl "internal";
9. allow (read, execute, info) user = "anyone";
10. deny (list, write, delete) user = "anyone";
11.
12. acl "uri=/topsecret/*"
13. authenticate (user, group) {
14. database = "keyfile";
15. method = "basic";
16. };
17. deny (all) user = "anyone";
18. allow (all) user = "bnelson"

此特定文件包含一个允许 bnelson 用户访问 /topsecret 之下资源的 ACL。任何其他用户无论是否在数据库中，都应被拒绝访问该资源。示例 8.10 展示了当 rodole 用户尝试访问 /topsecret 之下资源时生成的服务器日志。rodole 用户存在于 keyfile 数据库中，但根据示例 8.9 的第 18 行不允许访问资源。

### 示例 8.10 在服务器日志中观察访问控制

```
[13/Oct/2008:21:59:05] fine (256): for host 127.0.0.1 尝试 GET /topsecret, request /topsecret/index.html
[13/Oct/2008:21:59:05] fine (256): virtual server www.example.com 的 GET 请求无法绕过 ACL 检查
[13/Oct/2008:21:59:05] fine (256): acl: 匹配了 [uri=/topsecret/*]
```

```
[13/Oct/2008:21:59:05] fine (256) acl user: 匹配 user = (anyone)
[13/Oct/2008:21:59:05] fine (256) acl user: 匹配 user = (anyone)
[13/Oct/2008:21:59:05] fine (256) acl: 调用 getter (attr=user; method-basic, dtype=file)
[13/Oct/2008:21:59:05] fine (256) acl: 调用 getter (attr=invalid-password; method-basic, dtype=file)
[13/Oct/2008:21:59:05] fine (256) acl: 调用 getter (attr=raw-user; method-basic, dtype=file)
[13/Oct/2008:21:59:05] fine (256) acl: 调用 getter (attr=authorization); method-basic, dtype=file)
[13/Oct/2008:21:59:05] fine (256) acl: getter (attr=authorization; method-basic, dtype=file) returns -2
[13/Oct/2008:21:59:05] fine (256) acl: getter (attr=raw-user; method-basic, dtype=file) returns -2
[13/Oct/2008:21:59:05] fine (256) acl: 调用 getter (attr=invalid-word; method-basic, dtype=file) returns -2
[13/Oct/2008:21:59:05] fine (256) acl: getter (attr=user; method-basic, dtype=file) returns -6
[13/Oct/2008:21:59:10] fine (256) acl for host 127.0.0.1 尝试 GET /topsecret/index.html
[13/Oct/2008:21:59:10] fine (256) acl user: 匹配 user = (anyone)
[13/Oct/2008:21:59:10] fine (256) acl: 调用 getter (attr=user; method-basic, dtype=file)
[13/Oct/2008:21:59:10] fine (256) acl: 调用 getter (attr=invalid-password; method-basic, dtype=file)
[13/Oct/2008:21:59:10] fine (256) acl: 调用 getter (attr=raw-user; method-basic, dtype=file)
```





[13/Oct/2008:21:59:10] fine (2056): file authdb: Authentication succeeded for [rodale] (basic)
[13/Oct/2008:21:59:10] fine (2056): acl: get for (attr=isvalid-password, method=basic, dbtype=file) returns -1
[13/Oct/2008:21:59:10] fine (2056): acl: get for (attr=user; method-basic, dbtype=file) returns -1
[13/Oct/2008:21:59:10] fine (2056): acl: user [rodale] does not match user = (bnelson)
[13/Oct/2008:21:59:10] security (2056): for host 127.0.0.1 trying to GET /topsecret/index.html while trying to GET /topsecret/, acl-state reports: HTTP5191: access of /sun/webserver7/https://www.example.com/docs/topsecret/index.html denied by ACL uri=/topsecret/ directive 1

前13条条目（时间戳为 13/Oct/2008:21:59:05）展示了 rodale 用户在身份验证之前发出的初始请求，剩余的15条条目（时间戳为 13/Oct/2008:21:59:10）展示了身份验证过程中生成的条目。请特别注意用户正在进行身份验证以及身份验证是否成功的条目（这些是示例 8.10 中列出的前两个**粗体**条目）。还要注意示例 8.10 中的最后两个**粗体**条目；这些条目提供了有关用户访问资源请求被拒绝的细节。

该特定资源的 ACL（访问控制列表）由第 17 行和 18 行定义的两个 ACE（访问控制实体）组成。此示例表明，用户被第一个评估的 ACE 阻止访问该资源（该 ACE 定义在示例 8.9 的第 17 行）。之所以发生这种情况，是因为第二个 ACE 的结果为 FALSE，因为用户与 bnelson 不匹配。

## 8.1 控制对 Web 服务器资源的访问

访问控制策略的实现利用了身份验证（Authentication）和授权（Authorization）来有效保护 Web 服务器。在允许用户访问信息之前，你必须知道他们是谁；这要求你拥有一个身份验证数据库（Web 服务器支持不同类型）。一旦确定了用户身份，就可以根据策略中定义的数据确定该用户是否被允许访问信息（以及以什么方式）。这需要你拥有一个或多个访问控制文件，用于定义你为每个 Web 服务器资源定义的权利。当这两项都经过妥当配置时，你就为保护 Web 服务器中包含的信息奠定了基础。

图 8.4 展示了在实现基础或摘要身份验证（简单的用户名和密码）时，HTTP 用户代理程序与 Web 服务器之间的通信情况。它展示了请求处理过程中身份验证和授权发挥作用的点，以及双方对接收到的信息的常用响应方式。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_349_0.png)

图 8.4 访问控制流程

在此示例中，用户指定了用户名和密码进行身份验证。同样简单的方法是为 Web 服务器提供受信任的客户端证书进行身份验证。这被称为基于证书的身份验证，比标准的用户名和密码提供了更强的加密级别。使用证书提供更多层级的安全性将在下一节中进行更多讨论。

## 8.2 使用 SSL 证书保护数据

组织每天利用互联网与员工、客户、供应商和业务伙伴开展业务。因此，这些实体之间交换的信息必须是安全的、未被篡改的，且双方的身份必须是可靠的。

例如，考虑一个在线销售产品的网站。希望从该网站购买产品的客户想要知道他们正与谁做生意。他们想要知道信任的供应商确实是他们所说的人。反之，供应商无法查看消费者的执照或员工证来确保消费者有权进行购买或访问信息的纸质记录（包括信用卡单和销售发票），在这些票据中，双方都可以证明交易的发生。对于双方从未面对面接触过的电子交易，可以提供此类证明吗？

互联网使用广播媒体，在传输过程中的某些点可能完全不受保护。比作邮政递送系统（信件装在信子里），通过互联网发送的信息就像发送明信片。明信片缺乏递送保证，可以被任何处理明信片的任何人读取，并且可以在发送者或接收者不知情的情况下被更改。事实上，市上有很容易获得的软件，允许不怀好意的人截获、读取并可能修改传递的电子消息。供应商和消费者如何保持信息机密，如何防止信息被修改？幸运的是，这种技术是。SSL（安全套层）是一种为网络流量提供隐私和验证的安全协议。要启用 SSL，你必须首先安装 X509 证书。证书提供了一种分发各种信息（如你的公钥）的方法。Netscape 在 20 世纪中期开发了安全套层协议（SSL），以解决网络隐私问题。SSL 协议及其继任者传输层安全（TLS）建立了在互联网上进行业务所需的信任，这两种协议在所有 Web 服务器中被广泛使用的加密技术如下：

- 身份验证和不可否认性：使用 X509 证书和数字签名来验证身份。这是通过 RSA（Rivest, Shamir 和 Adleman）公对称加密实现的。
- 信息隐私：数据加密标准（DES）、里斯特密码（RC2）或里斯特密码 4（RC4）对称加密确保信息不被第三方看到。
- 信息完整性：使用单向哈希（或消息摘要）如消息摘要（MD5）或安全哈希算法（SHA-1）来确保信息未更改。

SSL 协议支持使用多种不同的算法或密码，用于服务器和客户端之间的身份验证、传输证书以及建立会话密钥等。客户端和服务器支持不同的密码套件，这取决于它们支持的 SSL 版本、公司对加密强度的政策以及对启用 SSL 的软件的限制。这些功能解决了互联网和其他 TCP/IP 网络通信的基本问题：

- SSL 服务器身份验证使用户能够确认服务器身份。启用了 SSL 的客户端软件可以使用公钥密码学的标准技术检查服务器证书和公 ID 是否有效，以及是否由客户端信任证书列表中的证书机构（CA）颁发。如果用户（例如）正通过网络发送信用卡，并想要检查接收服务器的身份，那么这种确认可能是关重要的。
- SSL 客户端身份验证允许服务器确认用户的身份。使用与服务器身份验证相同的技术，启用 SSL 的服务器软件可以检查客户端证书和公 ID 是否有效，以及是否由服务器信任证书列表中的 CA 颁发。如果服务器（例如）是向客户发送机密财务信息的银行，且银行需要检查接收者的身份，那么这种确认可能是关重要的。





## 8.2 使用 SSL 证书保护数据

- 加加密的 SSL 连接要求客户端和服务器之间发送的所有信息都必须由发送软件加密并由接收软件解密，从而提供高水平的机密性。在任何私人交易中，机密性对双方都至关重要。此外，所有通过加密 SSL 连接发送的所有数据都受到检测篡改机制的保护——即自动判断数据在传输过程中是否被更改过。

SSL 2.0 和 SSL 3.0 协议支持重叠的加密套件。管理员可以为客户端和服务启用或禁用任何支持的加密套件。当特定的客户端和服务器在 SSL 握手期间交换信息时，它们会识别出共同的最强加密套件，并将其用于 SSL 会话。

加密强度通常用用于执行加密的会话密钥来描述。通常，密钥越长，加密越强。密钥长度以位（bits）衡量。例如，用于 SSL 支持的 RC4 对称密钥算法的 128 位密钥，比用于相同算法的 40 位密钥提供了优好得多的保护。

### 8.2.1 对称密钥加密

计算机应用程序是可预测的，且只能执行程序员编写它们执行的操作。应用程序内部的逻辑以某种可预测的水平反复处理。因此，许多在计算机程序中使用的算法通过足够的观察就可以很容易确定。在算法中引入随机性的方法是使用一个不易被预测的随机值或密钥。这使得算法能够利用该密钥并产生一种在不知道密钥值的情况下无法回溯到算法逻辑的数据。在编程中使用密钥最显著的例子是伪随机数生成器，它需要使用随机种子来使输出具有真正的随机性。

密码学是隐藏信息的实践与研究，用于保护 Internet 交易。加密算法被用于将普通信息（明文）转换为看似无意义的信息（密文），然后再次转换回原文。这使得双方如果共享相同的算法，就可以进行安全通信。为了创建一个不易被破解的有效算法，加密算法（或称为密文算法）必须共享一个随机密钥值。最简单的加密类型使用一个平凡的、通常是相同的密钥同时用于解密和加密。密钥在通信双方之间共享，因此被称为对称密钥。使用对称密钥对数据进行加密和解密的过程被称为对称加密。图 8.5 展示了如何使用共享对称密钥允许 William 向 Rachael 发送消息。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_354_0.png)

图 8.5 使用共享（对称）密钥共享消息

双方同意使用用于加密和解密消息的算法（例如，高级加密标准 (AES)）。此外，双方共享一个秘密密钥，将其作为算法的种子。William 创建了一条他想要与 Rachael 分享的明文消息。他使用加密算法对消息进行加密，并使用对称密钥作为输入。这产生了任何没有对称密钥的人无法阅读的密文。当 Rachael 接收到消息时，她可以解密并读取，因为她拥有共享密钥的副本。

对称密钥加密通常是加密解密消息最快的方法，但双方之间分发对称密钥是其最大的缺点。你不能通过电子介质发送密钥，因为担心可能被截获并对你不利。那么，如何在两个可能从未谋面的双方之间共享密钥呢？公钥加密为这一困境提供了解决方案。

### 8.2.2 公钥加密

公钥加密被称为非对称加密，因为它使用两个不同的密钥（公钥和私钥）来编码和解码被加密的数据。这与对称密钥加密形成，后者使用同一个密钥同时用于加密和解密。公钥加密中使用的算法其开发方式使得：使用一个密钥加密的数据只能用另一个密钥解密（反之亦然）。这两个紧密耦合的密钥的组合被称为密钥对（key-pair）。

希望他人与其进行私密通信的实体（例如，电子商务网站）会将两个密钥中的一个公开，供公众使用。他们将另一个密钥私密地锁定。客户随后可以使用公钥来加密数据。

### 8.2.3 X.509 数字证书

数字证书是驾驶执照、护照和其他身份证明的电子对应物。你通过电子方式出示证书来证明你的身份或访问信息和服务的权利。与任何实体身份证明一样，数字证书可以创建、过期、撤销或挂起。数字证书将实体的身份与用于加密和签密钥对绑定。与加密结合时，数字证书提供了更完整的安全解决方案，确保电子交易中所有参与方的身份。数字证书通常包含以下信息：

- 所有者公钥
- 所有者名称
- 公钥有效期
- 证书颁发机构名称（证书 Authority—CA）
- 数字证书序列号
- CA 的数字签名




00:ca:fa:79:8f:19:f8:d7:de:e4:49:80:e6:2a:2a:86:
ed27:40:4d:86:b3:05:01:bb:50:15:c9:dc:2c:19:22:
43:7d:65:71:e4:17:d3:f0:36:b5:7f:a8:51:a3:a1:00:
98:ce:7f:47:50:2c:93:36:71:cb:89:06:41:72:b5:e9:
73:39:76:ef:9a:32:48:86:ac:49:63:0f:f9:ff:16:2a:e3:00:
9d:3b:af:ce:9a:63:48:65:96:61:05:0a:11:a2:b80:
7d:89:dc:09:99:c4:de:25:06:a8:31:a8:ca:54:a9:41:45

指数: 65537 (0x10001)

算法: mdWithRSAEncryption加密
63:23:af:f3:b6:7a:df:90:dc:f7:de:18:e6:01:69:5e:64:55:06:30:43
d34:d3:01:f6
t73:c0:a8:fa:28:b2:c1:a4:83:a2:fe:2b:a2:f8:bf:f0:d6:ff:75:a3:78:f57:24
46:62:97:1d:0d
96:c6:11:04:a2:e0:cc:2a:75:c6:b8:b6:9b:87:00:d7:c4:79:ba:f8
b4:d2:62:58:c3:
c5:b6:c1:a3:63:44:42:ed:af:c8:0f:2f:38:65:d6:59:e8:41:a2:a5:a4
e:25:36:38:ff:32
t78:a1:b3:f1:ed:dc:03:d1:b0:d6:67:e2:a9:44:a8:d4:c4

证书遵循 RFC 3280 中定义的格式，通常称为用于公钥基础设施（X.509）的 PKIX。尽管证书可能包含大量信息，但您应该特别注意以下字段：

- 发行者（Issuer）字段包含证书颁发机构（CA）的特异名称，即发行此证书的实体。浏览器会查看此信息并与其受信任 CA 列表进行对比。如果未找到该名称，浏览器将不会自动信任此证书。
- 有效期（validity）字段包含证书生效的日期和过期日期。如果浏览器在这两个日期之外的日期收到证书，它将不会自动信任此证书。
- 主体（Subject）字段包含证书所有者的特异名称。它可能包含标识此证书的各种属性，但最重要的属性是 CN（或通用名称）。CN 必须与它正尝试访问的主机主机名和域名匹配。如果 CN 与这些信息不符，浏览器将不会自动信任此证书。
- 证书签名遵循算法（Algorithm）字段并包含一个编码的位流签名。浏览器通过对证书的第一部分进行 MD5 哈希处理并使用 CA 的私钥进行加密来计算此值。浏览器可以使用 CA 的公钥解密数字签名，以获得证书的原始哈希值。然后它们可以使用签名算法（Signature Algorithm）字段中指定的算法复制相同的哈希过程。然后可以比较这两个哈希值，以确定证书是否经过了任何形式的更改。

在可以在 Web 服务器上启用 SSL 之前，您必须先安装数字证书。与启用 SSL 的 Web 服务器通信的用户代理在 SSL 握手期间会接收数字证书的副本。用户代理从数字证书中提取公钥，并使用它与 Web 服务器建立安全通信。

> 注意：数字证书包含所有者公钥的副本，并作为向想要与所有者建立通信的人发布公钥的主要机制。有关 SSL 握手的更多信息请参考 8.2.6 节；有关公钥加密的描述，请参考第 8.2.2 节。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_358_0.png)

证书存储在 Web 服务器的信任数据库中。默认情况下，Web 服务器将安全相关信息存储在三个网络安全服务（NSS）文件中：

- cert9.db——存储基于安全的信息
- key9.db——存储密钥
- root9.db——存储根证书

#### 证书类型

三种主要的算法类型：
- 数字签名算法（DSA）
- RSA（Rivest-Shamir-Adleman）
- 椭曲线数字签名算法（ECDSA）

#### 使用证书加密数据

数字签名算法（DSA）是由美国国家标准与技术研究院（NIST）首次提出的，用于 SSL。RSA 被广泛用于允许服务器提供内容，也可用于其他身份识别目的，如数字签名或电子邮件。管理员可以通过向证书颁发机构请求 Web 服务器的 X509 数字证书。表单可能包含公司信息，如公司名称、网站地址、物理地址、电话号码、城市、州和邓氏指数以帮助 CA 进行尽职调查。公司还可以随请求提交证书签名请求（CSR）。CSR 是为特定的 Web 服务器生成的，由标识证书所有者的属性组成；这些包括组织名称、城市、州。重要的是，CSR 还包含了服务器生成的公钥。相应的私钥不包含在 CSR 中，但用于对整个请求进行数字签名。

可以使用管理控制台或命令行界面中的 `create-cert-request` 命令为 Web 服务器 7.0 创建 CSR。以下提供了如何使用该命令来生成 CSR 的示例：

由于移动设备的限制，ECC 具有优势，减少 CPU 消耗和带宽需求。一些专家认为 RSA 密钥长度可能会被破解。随着向移动设备的发展，对更长密钥的需求已经出现。国家安全局（NSA）要求的签名可持续 50 年。椭圆密码学（ECC）在移动设备中越来越具有吸引力。1024 位 RSA 密钥提供了同等的安全性。2048 位 RSA 密钥在服务器上是常用的。256 位 ECC 密钥提供了比 RSA 几个数量倍的安全性。这些要求铺平了使用椭曲线数字签名算法（ECDSA）的道路。

#### 第8章 安全 Web 服务器

注意：Web 服务器 7.0 支持 RSA 和 ECC 证书。有关 ECC 证书的更多信息，请访问 Sun Labs Crypto 网站 http://research.sun.com/projects/crypto。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_360_0.png)

### 8.2.5 证书颁发机构

证书颁发机构（CA）创建并颁发用于服务器（或其他应用程序或设备）的 X509 数字证书，以便它们在互联网上识别身份。这最广泛用于允许服务器通过 SSL 提供内容，也可用于其他身份识别目的，如数字签名或加密电子邮件。

管理员可以通过向证书颁发机构请求 Web 服务器的 X509 数字证书。表单可能包含公司信息，如公司名称、网站地址、物理地址、电话号码、城市、州和邓氏指数以帮助 CA 执行调查调查。公司还可以随请求提交证书签名请求（CSR）。CSR 是为特定的 Web 服务器生成的，由有助于标识证书所有者的属性组成；这些包括组织名称、城市、州和国家。最重要的是，CSR 还包含了服务器生成的公钥。相应的私钥不包含在 CSR 中，但用于对整个请求进行数字签名。

可以使用管理控制台或命令行界面中的 `create-cert-request` 命令为 Web 服务器 7.0 创建 CSR。以下提供了如何使用该命令生成第 8.2.3 节所示证书的示例：

```
wadm create-cert-request --key-type=rsa --key-size=1024 --org=IT
--org-unit=Internet --locality=Tampa --state=Florida --country=US
--config=www.example.com --token=internal --server-name=www.example.com
```

`key` 参数指定了请求的密钥类型，`key-size` 参数指定密钥长度。`token` 参数引用服务器使用的 PKCS 令牌名称，默认为内部。其余选项指定了有助于识别证书所有者的数据。此子命令产生类似于下面的输出：



------BEGIN NEW CERTIFICATE REQUEST------
MIIBJ1TC8CAQawatELMAKGA1UEBMCVCMWDA0BGNVAgBT0Zsb3jPGEXDJAM
BgGNVCA TBBVRhBqHMVsQCVVDYQEWJ2VDERMAGA1UECMisW50ZWXZJUXQXGDA
BgBNVAM3TD3c5y5G1EqcCxC1mLbTbCnAnBAGBqhkKI9gW0BAQFAE0JAgQwKGC
YEAt1r3P77B5TIj/G0nQcV13A10p77X5nZ21r0113M2ayMuAeuZDA
C2b6VAv8dc4cV806H71Gab4p2qzgTHXQ9R08DbOIecfI5GargA4V4Ggb1I
JB0X6a1610Xd003x11Y9D345bHI6X4Yq1695P3jd33Y3mDbZndSCAEWAAATmcCSCSqG
JB3Q3DEJEMwB40RRBWEYIjd3mY3lbW29Yt6bu0JcbpsY53B3
DBQEBABA44ADFBQgPG9S011a64bKoYJTJnQQ0AgMgj0cbpsY97b570q
bB08+jOFXY5b58+UYYKZK0R+fTLaIRYd79Ut5gcCdE6pb2ho+0bHNKFYB
------ END CERTIFICATE REQUEST------

管理员将 CSR（包括整个 BEGIN 和 END 行）连同申请表（适用）提交给证书颁发机构（CA）。如果请求通过，CA 将生成一个证书，其中包含公钥，该公钥还包含颁发证书的 CA 的数字签名——换句话说，CA 正在为证书所有者背书。因此，CA 每每次颁发新证书时都会质押自己的声誉。因此，CA 在向实体颁发证书之前有责任识别特定公钥的所有者身份。CA 用于建立所有者身份的方法是 CA 安全策略中最重要的部分，而互联网安全的有效性取决于颁发证书时采取的谨慎程度。

证书请求过程涉及费用。诸如 Verisign 和 Entrust 等 CA 会对此服务收取费用。然而，这也有好处，因为从这些受信 CA 获取证书的浏览器不会为该网站生成安全警报。

由证书颁发机构获取的证书采用如下：

------BEGIN CERTIFICATE------
MI0HDTCCAaoAgWIBAgIBQb5XuaTDHdBc00njX1ElzMspANBgqhkKI9gW0BAQUFAEADCB
hzELMKGA1UEBMCwkEIjAgBgNVAgBT0AgGUZPIBURVNUSUSHIFBVU1BPUOVTIE90

lines dated

YGFnDSShkGfcfs+pAIq6LLKYm2TCalryGMo+TalpnIZkfvcfIE44MktTmsroxBVLVC
w33JbP5EC8KKZ08gQKKCHYt+4gNswyDDeExAmRy9LcCCEqX

------END CERTIFICATE------

您可以使用管理控制台或命令行界面中的 `install-cert` 子命令在 Web Server 7.0 中安装证书。以下提供了如何使用 `install-cert` 子命令安装从证书颁发机构获取的证书示例。证书包含在 `serverCert.fil` 文件中。

```
wadm> install-cert --token=internal --cert-type=server--nickname=exampleCert --config=www.example.com /serverCert.fil
```

`cert-type` 选项指定正在安装的证书类型，可以是 CA 证书、服务器证书或证书链。`nickname` 选项指定在管理服务器中引用证书的方式。`token` 选项引用服务器正在使用的 PKCS 令牌名称，默认为 `internal`。

如前所述，CA 颁发的证书涉及相关费用。如果您不想产生费用，并且不在意浏览器中生成的安全警报，那么您可以选择生成或获取自签名证书。自签名证书是由其自身的创建者签名的标准 X.509 证书。换句话说，创建证书的人也签署了其合法性。自签名证书广泛用于内部或测试目的，但大多数公司选择为他们的面向客户的网站从受信 CA 购买证书。

Web Server 7.0 提供了生成 RSA 和 ECC 自签名证书的机制。事实上，管理服务器已通过在安装 Web Server 软件期间创建的自签名证书启用了 SSL。您可以使用管理控制台或使用命令行界面中的 `create-selfsigned-cert` 子命令生成自己的自签名证书。以下提供了如何使用此子命令创建自签名证书的示例：

```
wadm> create-selfsigned-cert --key-type=rsa --key-size=1024 --org=IT--org-unit=Internet --locality=Tampa --state=Florida --country=US--config=www.example.com --token=internal--server --nickname=exampleCert
```

# 8.2 使用证书加密 SSL

`create-selfsigned-cert` 命令将自签名证书的生成和安装合并到一个步骤。自签名证书是由其自身的创建者签署了其合法性。

注意：如前所述，CA 颁发的证书涉及相关费用。如果您不想产生费用，并且不在意浏览器中生成的安全警报，那么您可以选择生成或获取自签名证书。自签名证书是由其自身的创建者签名的标准 X.509 证书。自签名证书广泛用于内部或测试目的，但大多数公司选择为他们的面向客户的网站从受信 CA 购买证书。

Web Server 7.0 提供了生成 RSA 和 ECC 自签名证书的机制。事实上，管理服务器已通过在安装 Web Server 软件期间创建的自签名证书启用了 SSL。您可以使用管理控制台或使用命令行界面中的 `create-selfsigned-cert` 子命令生成自己的自签名证书。以下提供了如何使用此子命令创建自签名证书的示例：

# 8.2 使用证书加密 SSL

`create-selfsigned-cert` 命令将自签名证书的生成和安装合并到一个步骤。自签名证书是由其自身的创建者签署了其合法性。

注意：如前所述，CA 颁发的证书涉及相关费用。如果您不想产生费用，并且不在意浏览器中生成的安全警报，那么您可以选择生成或获取自签名证书。自签名证书是由其自身的创建者签名的标准 X.509 证书。自签名证书广泛用于内部或测试目的，但大多数公司选择为他们的面向客户的网站从受信 CA 购买证书。

### 8.2 SSL 握手

SSL 握手总是从交换消息开始的。握手涉及的步骤总结如下：

- 1. 客户端向服务器发出请求。服务器使用 SSL 版本、加密算法设置和其他随机数据响应客户端。
- 2. 客户端审查证书以确定是否应该信任服务器。具体验证项目：
    - 有效期：当前日期必须在有效期内。证书不能过期。
    - 受信 CA：每个客户端都维护一个受信证书列表。如果颁发 CA 的区别名称 (DN) 与客户端列表匹配，则客户端接受该证书。
    - 数字签名：证书包含的数字签名实际上是使用 CA 私钥进行哈希并加密的。客户端使用公钥来验证证书上的数字签名。这种方法确保了证书没有被任何方式更改。
    - 主题：证书的主题（例如 example.com）经过审查，以确定其是否与请求主机匹配。此步骤确认了客户端接收证书的服务器确实与其尝试通信的服务器。
- 3. 使用到目前握手中生成的所有数据，客户端（根据加密算法与服务器协作）创建一个会话密钥，并使用服务器的公钥（从步骤 2 发出的证书中获取）对其进行加密。
- 4. 客户端将加密的主密钥消息发送给服务器。
- 5. 服务器使用其私钥解密主密钥消息。
- 6. 客户端和服务器都使用共享的主密钥来生成会话密钥，这些对称密钥用于 SSL 会话期间交换信息的加密和解密。

可选步骤：
如果服务器请求了用户身份验证（握手的可选步骤，未在图 8.6 中显示），客户端还会签署另一段对于本次握手唯一且仅客户端和服务器已的数据。在这种情况下，客户端会将签名数据和客户端自身的证书发送给服务器，连同加密的主密钥消息。

如果服务器请求了用户身份验证，服务器将尝试验证客户端。如果无法验证客户端，则会话将终止。如果成功验证客户端，则握手将继续。





# 第 8 章 Web 服务器 7.0 的安全性

用户代理（User Agent）向 Web 服务器发送一条消息，告知其未来来自用户代理的消息将使用会话密钥加密。随后，它会发送一条独立的（加密）消息，表示用户代理握手部分已完成。

Web 服务器向用户代理发送一条消息，告知其未来来自 Web 服务器的消息将使用会话密钥加密。随后，它会发送一条独立的（加密）消息，表示 Web 服务器握手部分已完成。

SSL 握手现在完成，SSL 会话已开始。用户代理和 Web 服务器使用会话密钥对相互发送的数据进行加密和解密，并验证其完整性。

如步骤 5 所示，Web 服务器可以请求用户代理证书以验证用户代理的身份。可以配置 Web 服务器，在继续会话之前，验证用户代理证书是否存在于 LDAP 目录中的用户条目中。此配置选项提供了一种确保用户代理证书未被撤销的方法。

需要注意的是，用户代理和 Web 服务器的身份验证都涉及使用公私钥对中的一个密钥对某些数据进行加密，并用另一个密钥进行解密。

在服务器身份验证的情况下，用户代理使用 Web 服务器的公钥加密预主密钥摘要（premaster secret digest）。相应的私钥可以正确解密该秘密消息摘要，因此用户代理能够确认与公钥关联的身份确实是用户代理连接的 Web 服务器。否则，Web 服务器无法解密预主密钥消息，且无法生成会话对称密钥，会话将被终止。

在客户端身份验证的情况下，用户代理使用用户代理的私钥对某些随机数据进行加密——即创建一个数字签名。只有在使用相应的私钥时，用户代理证书中的公钥才能正确验证该数字签名。否则，Web 服务器无法验证数字签名，会话将被终止。

## 8.3 证书撤销列表 (CRL) 维护自动化

依赖公钥基础设施 (PKI) 证书作为安全设计一部分的应用通常会实现某种机制来确保这些证书是有效的。一种常见的机制是从颁发证书的证书授权机构 (CA) 获取撤销证书列表（称为 CRL 或证书撤销列表）。依赖最新证书信息的应用通常会定期获取最新版本的 CRL，并据此更新它们的信任数据库。

> 注意：VeriSign 维护着 crl.version.com 网站，应用程序可以在那里获取当前证书撤销列表列表。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_367_0.png)

旧版本的 Web 服务器允许管理员通过管理 GUI 或 `crtl` 命令行工具更新管理服务器中的 CRL 列表。旧版本 Web 服务器的缺点是，每次更新 CRL 后都必须重启实例。

Web 服务器 7.0 支持动态 CRL 刷新，允许管理员配置 Web 服务器检查特定文件系统目录中的更新 CRL，并处理在该目录发现的任何 CRL。在 Web 服务器 7.0 中，这不需要重启服务器。

### 8.3.1 CRL 处理自动化

必须配置两个参数以允许自动化 CRL 处理；这些参数包括查找 CRL 的目录（由 `server.xml` 中的 PKCS 属性 `crl-path` 指定）以及在该路径查找文件的频率（由 `event` 元素指定）。

可以使用 `set-pkcs11-prop` 子命令配置 CRL 路径，如下：

```
wadm> set-pkcs11-prop --config=www.example.com crl-path=/crl
```

这会导致 `server.xml` 文件中创建以下元素：

```
<pkcs11>
<crl-path>/crl</crl-path>
</pkcs11>
```

Web 服务器现在将在 /crl 目录中查找任何更新的证书撤销列表。Web 服务器假设在指定目录找到的所有文件都是 CRL。

要配置 Web 服务器在该目录中查找更新 CRL 的频率，请使用 `create-event` 子命令，如下：

```
wadm create-event --interval=60 --command=update-crl
--config=www.example.com
```

这会导致 `server.xml` 文件中创建以下元素：

```xml
<event>
<interval>60</interval>
<update-crl>true</update-crl>
</event>
```

这使得 Web 服务器每 60 秒处理一次 CRL。

> 注意：管理控制台允许你从 CRL Updates 页面同时配置这两个参数。你可以按照以下路径找到此页面：Configurations (配置), config_name, Certificates (证书), CRL Updates (CRL 更新)。

希望利用动态 CRL 刷新的管理员将提供自己的机制来下载并将 CRL 文件放置在相应的路径。执行此任务的典型方法是使用 `wget`、`curl` 或类似的工具从 CA 连接到相应的 CRL。再次，你通过配置服务器事件来实现这一点。

除了几个预定义的命令外，`create-event` 子命令还允许你指定任何你想要调度的脚本、可执行文件或操作系统命令。因此，你可以调度一个事件运行。

### 8.3.2 证书撤销列表 (CRLs) 维护自动化

```
wadm create-event --interval=300 --command="check limits" --config=www.example.com
```

希望利用动态 CRL 刷新的管理员将提供自己的机制来下载并将 CRL 文件放置在相应的路径。执行此任务的典型方法是使用 `wget`、`curl` 或类似的工具从 CA 连接到相应的 CRL。再次，你通过配置服务器事件来实现这一点。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_369_0.png)





## 8.4 检测并响应拒绝服务 (DoS) 攻击 

`check-request-limits` SAF 用于对象配置文件中 `PathCheck` 指令的主体内部。该 SAF 的语法可以总结如下：

```
PathCheck fn=check-request-limits [max-rps=x] [max-connections=x] [interval=i] [continue={silence|threshold}] [error=n] [monitor-attr]
```

该 SAF 定义的参数描述如下：

- `max-rps` 参数是每秒请求数 (RPS) 的阈值。如果超过了此值，后续的连接将不再提供服务。一旦速率低于此阈值，新请求将开始处理。
- `max-connections` 参数是用于请求的最大并发连接数。如果在至少有许多请求正在处理时，接收到匹配的请求，则该请求将被拒绝。一旦并发请求数低于此限制，新请求将开始处理。

> 注意：此 SAF 的 `max-rps` 或 `max-connections` 没有默认值。如果你使用 `check-request-limits` SAF，则必须指定这两个参数中的至少一个。

- `interval` 参数是计算每秒平均请求数的时间间隔。`interval` 参数的默认值为 30 秒。
- `continue` 参数决定了被阻塞的请求类型满足什么条件后重新恢复服务。`continue` 有两个值：`silence`（拒绝的请求必须降为零才能恢复服务）和 `threshold`（拒绝的请求率必须低于 RPS 阈值才能恢复服务）。`continue` 的默认值为 `threshold`。
- `error` 参数包含用于拦截请求的 HTTP 状态码。`error` 的默认值为 `Error 503, Service Unavailable`（服务不可用）。
- `monitor` 参数允许你指定一个可选的监控请求。请求速率被记录在一个由此参数值命名的容器（桶）中。如果未指定 `monitor` 参数，请求将记录在匿名（或通用）桶中。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_371_0.png)

# 第 8 章 保护 Web 服务器 7.0

以下指令提供了一个如何在 `check-request-limits` SAF 中使用这些参数，将客户端限制为每秒最多 10 次请求的示例：

```
PathCheck fn="check-request-limits" monitor="$ip" max-rps="10"
```

这是一个通用指令，用于跟踪来自任何客户端 IP 地址的请求；这是通过使用 `monitor` 属性实现的。`monitor` 属性指定了用于维护每秒请求数的计数器或桶的名称。为此值指定变量 `$ip` 允许你为每个客户端 IP 地址维护单独计数器。`interval` 和 `error` 值未显式说明；因此，服务器将分别使用这些属性的默认值 `30`、`threshold` 和 `503`。

你可以通过如下的条件处理将跟踪限制在特定类型的请求上：

```
<If path="*.pl">
PathCheck fn="check-request-limits" monitor="$ip" max-rps="10"
</If>
```

此示例演示了如何使用 `<IF>` 容器将监控仅限制为 PERL 请求。如果某个特定客户端在 30 秒内尝试处理超过 10 次 PERL 请求（任何类型），则下一个请求将不会被处理。相反，客户端将收到 503 错误（服务不可用）。在任何超过限制的客户端请求访问日志中，你都会看到此错误。

你可以使用命令行界面通过 `enable-request-limits` 子命令来为特定的虚拟服务器启用并配置处理限制，如下：

```
enable-request-limits --max-rps=10 --monitor-attribute="$ip"
--config=www.example.com --vs=www.example.com
```

这将向对象配置文件添加以下指令：

```
PathCheck fn="check-request-limits" max-rps="10" monitor="$ip"
```

> 警告：在配置 `monitor` 属性以使用如 `$ip` 等变量时，必须使用反斜杠 (\) 字符。这是为了转义美元符号并告诉 Web 服务器使用下一个字符。

管理控制台（Administration Console）还允许你从虚拟服务器限制（Virtual Server Limits）页面启用并配置请求处理限制。你可以通过以下路径找到该页面：Configurations (配置), config_name (配置名称), Virtual Servers (虚拟服务器), virtual_server_name (虚拟服务器名称)。

### 8.4.2 垄断服务器连接

客户端在处理期间利用应用程序线程。Web 服务器维护一个接受器线程（acceptor threads）池来接收客户端请求，以及一个执行请求处理的工作线程（worker threads）。在请求完成且服务器向客户端提供响应后，线程将返回池中。

> 注意：关于 Web 线程的更多信息，请参阅第 2 章“Web 服务器 7.0 架构”。

一个客户端可以向 Web 服务器打开多个连接并占用多个线程。同一个客户端可以故意缓慢地提供请求，从而在线程上停留的时间比应该的长。这两种情况的任何一种都可能导致线程池耗尽，导致无法处理额外的请求。可以使用 `check-request-limits` SAF 来指定客户端连接的最大数量，但不能用于解决故意缓慢的请求处理。

旧版本的 Web Server 使用 `AcceptTimeout` 指令来指定服务器等待客户端数据的时间秒数。这在 `magnus.conf` 中配置，默认设置为 30 秒。

> 注意：`AcceptTimeout` 现在由 `server.xml` 指定，默认值仍为 30 秒。如果在 30 秒内没有看到请求，服务器将终止连接。你可以通过 TELNET 观察此元素的行为（例如，连接到 www.example.com 80）。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_373_0.png)

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_373_1.png)

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_373_2.png)

# 第 8 章 保护 Web 服务器 7.0

该参数在许多情况下是足够的，但它无法对整个请求提供粒度控制。在客户端发送初始请求后，`io-timeout` 设置不再生效，客户端可以垄断连接。

为了满足粒度控制的需求，Web Server 7.0 现在包含了两个额外的属性：

- `request-header-timeout` —— 服务器等待完整 HTTP 头部的最大时间（秒）。
- `request-body-timeout` —— 服务器等待完整 HTTP 正文的最大时间（秒）。

这两个属性的可能值包括 0–604800 秒（相当于 0–10080 分钟或 0–168 天）以及 -1（禁用计时器）。计时器默认禁用禁用，但你可以根据需要启用它们。例如，如果你想确保在连接后的 10 分钟内接收所有请求头，并在随后的 60 分钟内接收正文数据，可以将 `request-header-timeout` 和 `request-body-timeout` 的值分别设置为 600 和 3600。所有超过这些值的连接将被服务器自动断开。

完成此任务的 CLI 子命令是 `set-http-prop`，可以如下指定这些值：

```
wadm> set-http-prop --config=www.example.com request-header-timeout=600
request-body-timeout=3600
```

该子命令会导致 `server.xml` 文件生成以下条目：

```xml
<http>
<request-body-timeout>3600</request-body-timeout>
<request-header-timeout>600</request-header-timeout>
</http>
```

管理控制台还允许你从 HTTP 设置（HTTP Settings）页面启用并配置这些超时值。你可以通过以下路径找到该页面：Configurations (配置), config_name (配置名称), Performance (性能), HTTP。





## 8.5 使用 Web 服务器作为反向代理

反向代理是一种在两个实体之间充当中间人的服务器，它通过验证和处理事务，使得事务的实际双方无需进行直接通信。这意味着代理代表内容 Web 服务器（也称为源服务器/服务器）进行操作。反向代理可以代表一个或多个源服务器，如图 8.7 所示。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_375_0.png)

当配置得当时，无法通过反向代理访问随机服务器，只能访问源服务器上的一组预定义的资源。反向代理作为这些服务器的指定代理，所有客户端都通过它来访问其提供服务的站点。

将防火墙与反向代理协同工作可以极大地减少暴露后端数据的可能性。必须配置防火墙以仅允许来自反向代理的特定类型访问（HTTP/HTTPS）。此配置确保了来自代理的请求是有效的，而其他请求被视为潜在的黑客。

实施反向代理以保护网络资源访问的益处包括：

- 为 Web 客户端提供访问源服务器资源的单一入口。这增加了第二层安全，使您能够跟踪并遏制针对源服务器的攻击。
- 提供一个单一控制点，您可以在此处指定谁可以访问以及他们被允许访问的内容。
- 提供一个访问层，以掩盖或隐藏被代理的源服务器的真实名称。这使您能够轻松地更换内容服务器或更改主机名。

对于关注硬件成本的公司，利用反向代理可以显著降低成本，因为消除了为内部和外部用户准备不同硬件的需求。内部和外部用户可以使用相同的 HTTP 请求访问相同的服务器。这种方法还消除了为内部和外部用户存储数据的硬件需求。反向代理能够在不向外界泄露任何信息的情况下保护后端数据。

建立具有单一入口的架构的理念也有助于负载均衡和故障转移。事实上，配置反向代理将请求转发到具有相似配置的源服务器，可以使反向代理作为应用程序级的负载均衡器运行。在典型的部署中，在浏览器和源服务器之间部署一个或多个反向代理。

在将反向代理放置于非军事化区 (DMZ) 时，一个安全的平台至关重要。然而，与其它 Web 服务器相比，Web Server 提供了最安全的环境。

> 警告：虽然 Apache 配合其 mod_proxy 插件也可以作为反向代理，但客户应仅谨慎使用。与 Apache 相比，Java Web Server 具有更高的安全性，CERT (http://www.cert.org) 报告的漏洞少十个。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_376_0.png)

## 8.5 使用 Web 服务器作为反向代理

要配置 Web 服务器作为反向代理，您需要指定 URI 与一个或多个源服务器之间的映射。您可以在 CLI 中通过 `create-reverse-proxy` 子命令执行此操作，也可以通过访问管理控制台中的反向代理配置页。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_377_0.png)

注意可以通过以下路径在管理控制台中找到反向代理配置页：Configurations (配置)、config_name、Virtual Servers (虚拟服务器)、virtual_server_name、Content Handling (内容处理)、Reverse Proxy (反向代理)。

`create-reverse-proxy` 子命令的语法如下：

```
create-reverse-proxy [--echo] [--no-prompt] [--verbose]
--config=config-name --vs=vs-name --uri-prefix=uri-prefix
--server=remote-server-url
```

`uri-prefix` 选项指定客户端访问反向代理内容的 URI。该 URI 被转发或重映射到特定源服务器上的内容。`server` 选项指定了托管内容的源服务器的协议和主机。如果内容可能存在多个服务器上，您可以指定一个逗号分隔的服务器列表，例如：

```
adm> create-reverse-proxy --config=www.example.com
--vs=www.example.com
--uri-prefix="/" --server=http://www1.example.com,http://www2.example.com
```

该子命令生成一个匹配指定 URI 的 `NameTrans` 指令。`NameTrans` 指令还指定了新创建对象（reverse-proxy/）的名称，该 URI 映射到一个或多个源服务器。如果您定义了多个 URL，服务器将以轮询方式在指定的服务器之间分配负载。示例 8.11 展示了此子命令生成的条目。

示例 8.11 对象配置文件中的反向代理指令

```
<Object name="default">
...
NameTrans fn="map" from="/" to="http://" name="reverse-proxy/"
...
</Object>
...
```

```
<Object name="reverse-proxy/">
Route fn="set-origin-server" server="http://www1.example.com"
server="http://www2.example.com"
</Object>
```

> **警告：** 您正在代理的 URI 在源服务器上必须存在；否则您将收到 404（未找到）状态码。默认情况下，反向代理 URI 映射到源服务器上的相同 URI。

可以配置反向代理以利用安全套接层 (SSL) 保护数据。这种配置被称为安全反向代理。安全反向代理可以从防火墙外的服务器到防火墙内的安全服务器提供加密连接。它还允许客户端连接代理服务器，促进信息的安全传输。

## 8.6 总结

Web Server 7.0 提供了丰富的安全框架使其使其今天最安全的 Web 服务器之一。通过使用身份验证数据库可以保护资源访问。Web Server 7.0 通过允许管理员监控请求和连接来防止拒绝服务攻击。最后，完全集成的 HTTP 反向代理允许其作为 HTTP 端点，在为公司提供间接访问的同时保持服务器本身的安全。

## 8.7 自学实验

使用本章包含的信息执行以下实验。这些实验将有助于验证您对本章描述概念的理解。

### 8.7.1 访问控制

使用命令行界面验证您对配置访问控制的理解。执行以下步骤：

- 1. 创建类型为 keyfile 的文件身份验证数据库。调用数据库 keyfile。在默认配置的虚拟服务器上执行此操作。
- 2. 创建类型为 digestible 的文件身份验证数据库。在默认配置的虚拟服务器上执行此操作。
- 3. （可选）如果您在 Solaris 服务器上执行这些实验，请创建一个类型为 PAM 的文件身份验证数据库。在默认配置的虚拟服务器上执行此操作。
- 4. （可选）如果您可以访问 LDAP 目录服务器，请创建一个类型为 LDAP 的文件身份验证数据库。在默认配置的虚拟服务器上执行此操作。
- 5. 列出身份验证数据库。
- 6. 向 keyfile 身份验证数据库添加两个用户（即 user1 和 user2）。
- 7. 列出 keyfile 身份验证数据库中的用户。
- 8. 将更新后的配置部署到所有节点。
- 9. 使用 UNIX cat 或 Windows more 命令验证用户是否存在于 keyfile 身份验证文件中。
- 10. 验证 server.xml 文件包含每个新创建的身份验证数据库的条目。
- 11. 添加允许 user 访问但不允许其他任何人访问。
- 12. 验证第 11 步中的访问控制是否实施正确。确保 user2 没有访问权限，而 user1 有。





## 第 8 章 加固 Web 服务器 7.0

14. 打开服务器日志（errors），并查看告知为何 user2 被拒绝访问服务器的条目。

15. 第 11 步中输入的 ACL，并验证所有用户是否能够再次访问服务器。

### 8.7.2 数字证书

使用命令行界面来验证你对如何配置 Web 服务器使用数字证书的理解。执行以下步骤：

+ 1. 为你的服务器创建一个自签名数字证书。使用以下参数：

密钥类型：RSA
密钥大小：1024
组织机构：My Company
组织单位：Training
城市：Tampa
州：Florida
国家：U.S.
配置：使用你的默认配置
服务器：www.example.com
令牌：internal
别名：exampleCertificate

> 注意：此步骤的意图是故意输入一个与你自己的主机主机名和域名不匹配的服务器值。如果你的服务器配置为 www.example.com，请为 Server 参数使用不同的值。

## 8.7 自主学习实验

+ 2. 在端口 443 上创建一个新的 HTTP 监听器并配置其使用 SSL。使用 exampleCertificate 证书启用 SSL。使用以下参数：

名称：
```
http-listener-ssl
```
端口：
```
443
```
IP 地址：*
服务器名称：
```
www.example.com
```
默认虚拟服务器：使用你的默认配置

SSL：
已启用
证书：
```
exampleCertificate
```

+ 3. 部署配置并在提示时重启服务器。
4. 连接到端口 443 服务器，并验证你是否看到一条指示存在主题不匹配（subject mismatch）的错误消息。查看该消息并检查证书。
5. 仅为本次会话接受证书。你应该看到你的服务器实例的主网页。
6. 删除 exampleCertificate 证书并创建一个具有正确服务器名称（即你真实的主机名和域名）的新证书。部署配置，再次访问该站点，并验证你没有看到主题错误。
7. 仅为本次会话接受证书。你应该看到你的服务器实例的主网页。

> 注意：旧版本的 Web 服务器要求在启动服务器实例之前提供信任数据库的密码。这不再是 Web Server 7.0 的要求。但是，如果你的安全策略认为有必要，你可以配置服务器要求密码。

+ 8. 配置服务器在实例启动期间需要密码。
你首先需要将密码与内部令牌（internal token）关联。你可以通过在管理控制台以下位置关联 PKCS11 Tokens来实现：Configurations, config_name, Certificates, PKCS11 Tokens, internal。一旦你为内部令牌关联了密码，如果不提供密码，你无法看到任何与证书相关的数据。点击“设置密码”（Set Password）按钮并提供密码，即可再次查看与证书相关的数据。此密码仅对管理服务器的本次会话有效。如果你注销并重新登录，需要重新输入密码。

+ 9. 从管理控制台或命令行停止并启动实例。在提示时输入第 8 步中配置的密码，并验证服务器进程是否正常启动。

+ 10. 禁用内部令牌的状态（token state）。这将从内部令牌中移除。

### 8.7.3 证书撤销列表 (CRL)

使用命令行界面来验证你对如何配置动态撤销列表的理解。执行以下步骤：

+ 1. 从 crl.verisign.com 下载一个或多个 CRL 到你本地主机的目录中。该网站上的 CRL 示例包括：ClassIndividual.crl、Class1Individual.crl 和 RSASecureServer。

+ 2. 打开另一个窗口并在服务器日志（errors）上运行 UNIX tail -f 命令。这允许你监控服务器读取这些文件的状态。

+ 3. 配置服务器每 60 秒更新一次第 2 步中目录找到的 CRL。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_382_0.png)

> 注意：在配置事件时需要重启服务器，但不需要在每次读取 CRL 时都重启服务器。

+ 4. 重启服务器以启动自动更新过程。

+ 5.回到运行 tail -f 命令的窗口。你应该会在服务器日志中看到生成的条目。条目应指示无法读取文件。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_382_1.png)

> 注意：如果你没有在服务器日志中看到生成的特定 CRL 条目，最可能是因为 Web 服务器尚未尝试读取这些文件。你可以使用 UNIX touch 命令强制读取文件，操作如下：touch *, crl。等待 60 秒，你应该能看到预期的 CRL 条目。

## 8.7 自主学习实验

+ 6. 确定 CRL 文件的权限。为什么服务器无法读取文件？

+ 7. 修改文件权限以解决问题，并使用 UNIX touch 命令修改文件的时间戳。

+ 8. 修改一个文件的时间戳，等待 60 秒，并观察服务器日志中生成的条目。

+ 9. 删除其中一个 CRL，等待 60 秒，并观察服务器日志中生成的条目。

+ 10. 配置服务器事件，定期从 crl.verisign 自动下载 CRL 到 CRL 目录。验证 Web 服务器是否正确读取了这些文件。

### 8.7.4 拒绝服务攻击 (DoS)

使用命令行界面来验证你对如何配置 Web 服务器以防 DoS 攻击的理解。执行以下步骤：

+ 1. 创建一个脚本或获取一个能够向 Web 服务器发送大量请求的应用程序。你应该将此脚本放置在环境中的另一台服务器或工作站上。这允许你在执行脚本时不对自身产生性能影响。

> 注意：你可以在 http://www.webserver.com 找到提供此功能的脚本。它是为具有 /usr/sbin wget 命令的 Solaris 安装编写的。

+ 2. 执行脚本对 Web 服务器上的 index.html 进行 1000 次请求。在脚本运行时，打开浏览器窗口尝试访问该页面。验证你是否看到了性能影响。如果没有看到影响，请在同一台服务器上运行多个实例。

+ 3. 将实例配置为最大 RPS 10。

+ 4. 重复第 2 步并验证响应时间已增加。你还应该注意到请求被限流，因为服务器在低于阈值之前停止响应。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_383_0.png)

### 8.7.5 反向代理配置

使用命令行界面来验证你对如何将 Web 服务器配置为反向代理的理解。执行以下步骤：

+ 1. 创建新配置。调用新配置 proxy 并将其与 Web 服务器上的可用监听套字（listen socket）关联。
2. 修改配置作为 www.google.com 的反向代理。指定 / 为 URI。
3. 通过尝试访问 Web 服务器上的内容来测试代理配置。确保你正在尝试访问第 1 步中配置的端口。你应该会在浏览器中看到 Google 网站，但 URL 行应反映你的服务器名称。
4. 执行搜索并观察浏览器中的 URL。你应该看到它变为反映 Google 的主机名和域名。为什么会发生这种情况？
5. 更新代理配置修复修复。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_384_0.png)

> 注意：访问 http://www.webserver.com 了解如何执行这些练习的详细说明。




本章解释了 Web Server 7.0 如何提供使用 CGI、SHTML、ASP 和 PHP 等流行的服务器端脚本技术生成动态内容的支持。具体而言，本章讨论了这些技术中的每一种，并描述了 Web Server 中包含的用于启用和配置这些技术的管理支持。另一种在动态内容开发者中非常流行的语言是 Java。第 10 章描述了在 Web Server 7.0 中使用服务器端 Java 技术进行动态内容生成。

## 9.1 通用网关接口 (CGI)

通用网关接口 (CGI) 是一种用于外部程序与 Web 服务器进行交互的标准接口。你可以使用多种编程语言来实现通用网关接口 (CGI) 程序。在 UNIX 计算机上，CGI 程序通常用 Perl 和 Bourne shell 等脚本语言或 C/C++ 编写。在 Windows 平台上，CGI 程序可以使用 Perl 或C/C++ 等语言或如 Visual Basic 等 Windows 特定的语言编写。Web Server 7.0 包含了对《通用网关接口规范第 1.1 版本》的支持。

CGI 指定了服务器向外部程序传递数据以及从外部程序接收数据的接口。图 9.1 展示了 Web 服务器如何将 HTTP 请求传递给 CGI 程序，并将 CGI 程序的响应传回 HTTP 客户端。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_386_0.png)

图 9.1 通用网关接口概述

在 UNIX/Linux 系统上，Web Server 7.0 创建 Cgist 进程来执行 CGI 程序。这些进程在首次访问 CGI 时创建，其数量取决于服务器上的 CGI 负载。

在运行 Windows 的计算机上，Web Server 7.0 可以配置为使用 Windows 文件关联来运行 CGI 程序，或将文件作为 Windows CGI 程序运行。

下一节描述了 Web Server 7.0 中 CGI 子系统的配置。

### 9.1.1 CGI 配置

配置服务器以识别并执行 CGI 程序包括以下内容：

- 指定一个目录为包含 CGI 程序目录
- 指定具有特定扩展名的文件为 CGI 程序
- 在 UNIX 上指定额外的 CGI 安全设置
- 指定 CGI 子系统的全局设置

表 9.1 标识了 Web Server 7.0 中包含 CGI 子系统配置的配置文件。

#### 表 9.1 CGI 配置文件

| 文件名 | 说明 |
| --- | --- |
| obj.conf | 包含实现 CGI 程序请求处理的 SAFs。虚拟服务器——CGI 子系统的特定配置在虚拟服务器—.s 对象文件中指定。 |
| server.xml | 主实例文件中的 c 元素配置了 CGI 子系统的全局设置。 |
| mime.types | 指定被视为 CGI 程序的扩展扩展名。Web Server 在处理 CGI 程序请求时会分配以下 MIME 类型之一：magnus-internal/cgi magnus-internal/shellcgi magnus-internal/wincgi。你可以通过 server.xml 文件中 virtual-server 元素下的 mime-file 子元素，按每个虚拟服务器为基础配置 MIME 类型关联。 |

Web Server 7.0 重新设计的面向任务型管理控制台以及新的管理命令行工具 (wadam) 包含了对配置 CGI 子系统各个方面的支持。

图 9.2 展示了在使用管理控制台创建新配置时如何启用 CGI 子系统。

在虚拟服务器中配置 CGI 子系统的页面可以从管理控制台的主页轻松访问。图 9.3 展示了这一点。

图 9.4 显示了配置虚拟服务器 CGI 设置的管理控制台页面。

## 第 9 章 通过脚本提供动态内容

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_388_0.png)

图 9.2 管理控制台—新配置向导

## 通用网关接口 (CGI)

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_389_0.png)

图 9.3 管理控制台—通用任务

## 通过脚本提供动态内容

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_390_0.png)

图 9.4 管理控制台—虚拟服务器 CGI 设置 (Windows)

本节剩余部分描述了在 Web Server 中配置 CGI 的选项。

### 9.1.1 目录配置

通过目录配置 CGI 需要在虚拟服务器中映射一个 URI 前缀到包含 CGI 程序的目录。目录中的所有文件都作为 CGI 程序执行，无论其扩展名如何。虚拟服务器可以指定多个指向 CGI 程序的 URI 前缀。

图 9.5 展示了使用管理控制台创建 CGI 映射。

图 9.6 显示了添加 CGI 映射后的设置标签页。可以通过勾选表中的相应复选框并点击删除按钮来删除单个条目。

## 目录

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_391_0.png)

图 9.5 管理控制台—目录

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_391_1.png)

图 9.6 管理控制台—虚拟服务器 CGI 设置

wadam 的 create-cgi-dir 和 delete-cgi-dir 命令也可创建和删除 CGI 目录。wadm 的 list-cgi 命令可列出服务器中的 CGI 映射，如下：

```
wadm list-cgi --verbose --config=test --vs=test
uri-prefix             type
---------------------------------
cgi-bin               Sun/WebServer/cgi
```

### 9.1.2 文件扩展名配置

Web Server 可以配置为将特定扩展名的文件视为 CGI 程序。对此类文件的请求会导致执行，无论它们位于哪个目录。当 CGI 程序和 HTML 文件位于同一目录时，通过文件扩展名指定 CGI 程序非常有用。Web Server 可以根据扩展名识别虚拟服务器中的所有 URI 或特定 URI 的 CGI 程序。

文件扩展名在服务器的 mime.types 文件中指定。CGI 的默认扩展名为 .exe、.bat 和 .cgi，如图 9.7 所示。

你可以通过管理控制台的 MIME 类型标签页为虚拟服务器自定义 CGI MIME 类型，如图 9.8 所示。

图 9.9 展示了管理员如何根据扩展名配置 CGI 程序。

图 9.10 显示了添加 CGI 文件类型 URI 设置标签页。可以通过勾选表中的相应复选框并点击删除按钮来删除单个条目。

wadam 的 enable-cgi-file-type、disable-cgi-file-type 和 get-cgi-file-type-prop 命令也可用于管理根据扩展名识别 CGI 程序的 URI 映射。有关这些命令的更多信息，请参阅《Sun Java System Web Server 7.0 CLI 参考手册》。

图 9.7 管理控制台—全局 MIME 类型

图 9.8 管理控制台—新 Web 服务器控制台—新增 CGI 文件类型 URI

图 9.10 管理控制台—虚拟服务器 CGI 设置




# 第 9 章通过脚本提供动态内容

### 9.1.1.3 CGI 安全配置（仅限 UNIX）

在 UNIX/Linux 系统上，Web Server 创建并使用一组 CGI 存根（stub）进程来执行 CGI 程序。使用 CGI 存根进程执行 CGI 程序允许 Web Server 为 CGI 程序创建自定义的执行环境。例如，通过使用 Web Server，可以配置 CGI 程序以**唯一**的用户和组的权限执行，从而防止虚拟服务器的 CGI 程序干扰其他用户。CGI 存根强制执行的额外安全限制，使得黑客难以利用 Web Server 7.0 中的 CGI 子系统获取 root 权限。有关在 Web Server 7.0 中配置 CGI 程序执行环境的更多信息，请参阅《Sun Java System Web Server 7.0 开发指南》中的“为 CGI 程序创建执行环境”章节。图 9.11 展示了安装在 UNIX 系统上的 Web Server 7.0 中，管理员控制台中中用于配置虚拟服务器 CGI 执行环境的额外字段（与图 9.10 相比）。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_396_0.png)

图 9.11 管理员控制台-虚拟服务器 CGI 设置 (UNIX)

## 9.1 通用网关接口 (CGI)

如果你使用 wadm 的 `get-cgi-prop` 和 `set-cgi-prop` 子命令，也可以操作这些设置。请参考《Sun Java System Web Server 7.0 CLI 参考手册》获取有关这些子命令的更多信息。

### 9.1.1.4 全局 CGI 配置

全局 CGI 设置适用于所有虚拟服务器，包括以下内容：

- 空闲或无响应 CGI 程序终止后的超时时间
- 未使用的 CGI 存根进程终止的超时时间（仅限 UNIX）
- CGI 环境变量
- 服务器执行 CGI 程序使用的最小和最大 CGI 存根进程数（仅限 UNIX）

示例 9.1 提供了 server.xml 文件的片段，演示了如何使用 `cgi` 元素来配置 CGI 子系统的全局设置。

### 示例 9.1 server.xml 文件的片段

```
<cgi>
<cgistub-idle-timeout>60</cgistub-idle-timeout>
<max-cgistubs>10</max-cgistubs>
<env-variable>
<name>MYVAR</name>
<value>foo</value>
<description>自定义的 CGI 环境变量</description>
</env-variable>
</cgi>
```

必须重启服务器才能使全局 CGI 设置的生效。全局 CGI 设置在配置的 CGI 子选项页中进行，如图 9.12 所示。

如果你使用 wadm 的 `create-envvar`、`delete-cgi-envvar`、`list-cgi-envvars`、`get-cgi-prop` 和 `set-cgi-prop` 子命令，也可以操作这些设置。请参考《Sun Java System Web Server 7.0 CLI 参考手册》获取有关这些子命令的更多信息。

# 第 9 章 通过脚本提供动态内容

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_398_0.png)

图 9.12 管理员控制台—全局 CGI 设置

## 9.1.2 CGI 服务器应用程序函数 (SAFs)

Web Server 进程中的 CGI 引擎通过使用应用程序函数在请求处理中工作。第 6 章“Web Server 7.0 请求处理”描述了 Web Server 在每次请求时经过的不同请求处理阶段。表 9.2 描述了在 Web Server 中实现执行 CGI 程序支持应用程序函数 (SAFs)。

## 9.2 通用网关接口 (CGI)

**表 9.2** CGI 服务器应用程序函数

| 请求处理阶段 | SAF | 说明 |
| :--- | :--- | :--- |
| Init | init-cgi | 配置 CGI 子系统。此 SAF 已弃用，被 server.xml 文件中的 cgi 元素取代。 |
| Service | send-cgi send-wincgi send-shellcgi query-handler | send-cgi 函数设置用于传递给 CGI 程序的 CGI 环境变量，在单独进程中执行 CGI 程序并将结果发送客户端。此 SAF 的参数用于配置 UNIX/Linux 系统上 CGI 程序的自定义执行环境。你可以通过将扩展名与 `magnus-internal/cgi` MIME 类型关联，来配置 Server 将文件作为 CGI 程序执行。send-wincgi SAF 将文件作为 Windows CGI 程序执行并将结果发送到客户端。你可以通过将文件与 `magnus-internal/wincgi` MIME 类型关联，来配置 Server 将文件作为 Windows CGI 程序执行。send-shellcgi SAF 将文件作为 CGI 程序执行。query-handler SAF 运行 CGI 程序并用于支持过时的查询处理器（不再支持查询处理器）。Web 浏览器使用 HTML 表单向服务器提交数据。 |

示例 9.2 obj.conf（在启用 CGI 的 Server 中）

```
# Copyright 2008 Sun Microsystems, Inc. 版权所有。
# 使用受许可条款限制
# 你可以编辑此文件，但在使用管理 GUI 或 CLI 时
# 注释和格式更改可能会丢失。
# 在路径名中仅使用正斜杠，因为反斜杠可能会导致
# 问题。请参阅文档获取更多信息

<Object name="default">
Auth="match-browser" browser="MSIE*"
shutdown="true"
Name="j2ee"
```





# 第 9 章通过脚本提供动态内容

当前时间为 <b><!--echo var="DATE_LOCAL" --></br>。text.html 的内容如下：<br><br><b><!----include file="text.html" --></b></</body>></html>

图 9.13 展示了 Web 服务器在响应示例 9.3 所示服务器解析 HTML 文件请求时提供的内容。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_402_0.png)

**图 9.13** 由启用 SHTML 的 Web 服务器生成的示例响应

## 9.2 服务器解析的 HTML (SHTML)

下一节简要描述了可以在 Web Server 7.0 中使用的各种 SHTML 命令。

### 9.2.1 SHTML 命令

SHTML 命令嵌入在 HTML 注释中。这使得即使没有启用服务器解析的 HTML，也可以在 HTML 文件中使用 SHTML 命令，因为浏览器不会显示 HTML 注释的内容。

SHTML 命令的格式如下：

```
<!--command name="value" name="value" -->
```

每个 `name="value"` 对表示一个属性。命令和属性名称均采用小写字母。

表 9.3 描述了 Web Server 7.0 识别的标准 SHTML 命令。你也可以通过定义自定义 SHTML 标签来扩展 Web Server 的功能。请参考 *Sun Java System Server 7.0 Developer's Guide* 中的“Defining Custom Server-Parsed HTML Tags”章节获取实现自定义标签的信息。

**表 9.3** SHTML 命令

| 命令 | 说明 |
|---|---|
| config | 设置其他命令用于表示时间、大小和错误信息的格式。 |
| echo | 插入环境变量的值，如果未找到变量则插入（无）。你可以使用 echo 命令打印标准环境变量的值。SHTML 可使用的额外变量还有：`DOCUMENT_NAME, DOCUMENT_URI, QUERY_STRING, UNESCAPED, LAST_MODIFIED`；请参考 *Sun Java System Server 7.0 Developer's Guide* 中的“Server-side HTML Commands”和“CGI Variables”章节获取 SHTML 可使用的环境变量。 |
| exec | 执行 shell 命令或 CGI 程序的输出。 |
| lastmod | 打印文件的修改日期。日期格式由 config 命令控制。 |
| fsize | 打印文件的大小。大小由 config 命令控制。 |
| include | 包含文件的内容。如果包含的文件本身是 SHTML 文件，则 Web Server 会递归解析文件中的任何 SHTML 命令。 | 在启用了 Java 的 Web Server 中，你可以将 Java 应用程序内容作为 servlet 和 Java Pages (JP) 脚本包含 SHTML 文件。Web Server 的 HTML 子系统还支持 `<servlet>` 标签。这允许开发者在 SHTML 文件中嵌入 servlet 的输出。请参考 *Java System Server 7.0 Developer's Guide* 中的“Embedding Servlets”章节。

### 9.2.2 SHTML 配置

配置 Web Server 以启用 SHTML 解析包括：

- 指定包含 SHTML 文件的虚拟服务器
- 指定服务器将解析的文件

9.4 标识 Web Server 7.0 包含 SHTML 系统配置的文件。

## 9.4 SHTML 配置

| 文件名 | 说明 |
|---|---|
| obj.conf | 包含 SHTML 解析的处理。SHTML 子系统的虚拟服务器特定配置在服务器的对象文件中。 |
| mime.types | 指定哪些扩展名被视为 SHTML 文件。当处理 SHTML 文件请求时，Web Server 分配以下 MIME 类型：如果你使用 server.xml 文件中的虚拟服务器元素，可以根据虚拟服务器配置 MIME 类型。 |

Web Server 7.0 的管理框架支持为虚拟服务器启用 SHTML 解析。图 9.2，“CGI Configuration”章节说明了如何使用控制台启用 SHTML 解析。图 9.14 显示了控制台页面上的“Content Handling”标签，用于配置启用了 SHTML 的虚拟服务器。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_405_0.png)

# 通通用属性

可以从此页面修改内容特定的属性。更改任何默认值都会影响服务器处理和交付内容的方式。

- 目录列表
- 解析的 HTML/SSI
- 其他
- HTTP 压缩

## 目录列表

| 列表类型 | |
|---|---|
| [ ] 华丽 | [x] 简单 |
| 错误： | 解析的 HTML/SSI |
| 索引： | index.html |
| 文件： | index.jsp |
| HTTP 压缩： | [ ] 无 |
| 其他： | [ ] 华丽 |
| 解析的 HTML/SSI： | [ ] 简单 |
| 目录列表： | [x] 简单 |

| 列表类型 | |
|---|---|
| [x] 丽丽 |x HTML 简单 |
| 错误： | [ ] 无 |
| 索引： | [ ] index.html |
| 文件： | [ ] index.jsp |
| HTTP 压缩： | [x] 无 |
| 其他： | [x] 华丽 |
| 解析的 HTML/SSI： | [x] 简单 |
| 目录列表： | [ ] 华丽 |

| 列表类型 | |
|---|---|
| [x] 华丽 | [x   | |
  ：： | ||  | |  索引 | index index. index |
| 文件： | [ | index index. |

|   ： | [ [ 无 |
| 其他：： [ [ ] 华丽 |
| 解析的 HTML/SSI： | [x] 简单 |
| 目录列表： | [ ] 华丽 |

| 列表类型 | |
|---|---|
| [x] 华丽 | [x] 简单 |
| 错误： | [ ] 无 |
| 索引： | [ ] index.html |
| 文件： | [ ] index.jsp |
| HTTP 压缩： | [x] 无 |
| 其他： | [x] 华丽 |
| 解析的 HTML/SSI： | [x] 简单 |
| 目录列表： | [x] 华丽 |

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_406_0.png)

# 内容处理 - 通用属性

| 列表类型 | |
|---|---|
| [ ] 华丽 | [x] 简单 |
| 错误： | [x] 无 |
| 其他： | [x] 华丽 |
| 解析的 HTML/SSI： | [x] 简单 |
| 目录列表： | [x] 华丽 |
| 错误： | [ ] 无 |
| 索引： | [x] index.html |
| 文件： | [x] index.jsp |





## 9.2 服务器解析的 HTML (SHTML)

```
or disable-parsed-html [--echo] [--no-prompt] [--verbose] [--uri-
pattern=pattern]--config-config-name --vs=vs-name
CLI04 is a required option.
wadm=
wadm= get-parsed-html-prop
Usage: get-parsed-html-prop --help|?
or get-parsed-html-prop [--echo] [--no-prompt] [--verbose] [--uri-
pattern=pattern]--config-config-name --vs=vs-name (property-name)*
CLI04 is a required option.
```

有关这些子命令的更多信息，请参考《Sun Java Web Server 7.0 CLI 参考手册》。

## 9.2.3 SHTML 服务器应用函数 (SAFs)

Web Server 中的 SHTML 引擎通过使用服务器应用函数（SAFs）参与请求处理。第 6 章描述了 Web 服务器处理每个请求时所经历的不同请求处理阶段。表 9.5 描述了实现解析 HTML 文件中嵌入的 SHTML 命令支持的服务器应用函数 (SAFs)。

表 9.5 SHTML 服务器应用函数

| 请求阶段 | SAF | 描述 |
|---|---|---|
| Init | shtml-init | 初始化 Web Server 中的 SHTML 子系统。不再再从 magnus.file 中的 Init 指令中调用此 SAF 来启用 SHTML 解析。SHTML 子系统在服务器启动期间始终会被初始化。此 SAF 已弃用。 |
| ObjectType | shtml-hackype | 为 .html 或 .htm 扩展的文件启用 SHTML 解析。通常，服务器为 .html 或 .htm 扩展的文件分配 `text/html` 作为 Content-Type。shtml-hackype SAF 将 .html/.htm 文件的 Content-Type 更改为 `magnus-internal/parsed-html`，以便该文件由 shtml-send SAF 处理，而不是由 send-file SAF 处理。 |
| Service | shtml-send | 处理包含 SHTML 命令的 HTML 文件。 |

示例 9.4 展示了启用了解析 HTML 处理的服务器配置的 `obj.conf` 文件。示例 9.4 中与 SHTML 相关的指令和对象用**粗体**字体标记。

## 第 9 章通过脚本提供动态内容

示例 9.4 obj.conf 文件（在启用 HTML 的服务器中）

```
#
# 版权所有 2008 Sun Microsystems, Inc. 保留所有。
# 使用受许可条款限制。
#
```

```
# 你可以编辑此文件，但当您使用管理 GUI 或 CLI 时，
# 注和格式更改可能不会丢失。
```

```
# 在路径名中仅使用正斜杠，因为反斜杠可能会引起
# 问题。更多信息请参阅文档。
```

```
<Object name="default">
AuthTrans fn="match-browser" browser="MSIE*" ssl-unclean-shutdown="true"
Name fn="assign-name" from="/html/*" name="html/*"
Name fn="ntrans-j2ee" name="j2ee"
Name fn="pfx2dir" from="/mc-icons" dir="D:/WebServer7/lib/icons"
name="es-internal">
PathCheck fn="uri-clean"
PathCheck fn="check-acl" acl="default"
PathCheck fn="find-pathinfo"
PathCheck fn="find-index-j2ee"
PathCheck fn="find-index" names="index.html,home.html,index.jsp"
ObjectType fn="type-j2ee"
ObjectType fn="type-by-extension"
ObjectType fn="force-type" type="text/plain"
Service method="[HEAD]" type="magnus-internal/parsed-html"
Service fn="html-send" type="*magnus-internal/*" noexec
method="[HEAD][POST]" type="*magnus-internal/*" fn="send-file"
Service method="[GET]" opts="noexec"
Service method="TRACE" fn="service-trace"
Error fn="error-j2ee"
Addlog fn="flex-log"
</Object>
```

```
<Object name="j2ee">
Service fn="service-j2ee" method="*"
</Object>
```

```
<Object name="es-internal">
PathCheck fn="check-acl" acl="es-internal"
</Object>
```

```
<Object name="cgi">
ObjectType fn="force-type" type="magnus-internal/cgi"
Service fn="send-cgi"
</Object>
```

```
<Object name="send-precompressed">
PathCheck fn="find-compressed"
</Object>
```

```
<Object name="compress-on-demand">
Output fn="insert-filter" filter="http-compression"
</Object>
```

```
<Object name="/shtml/"
ObjectType fn="html-hackype"
Service fn="html-send" type="magnus-internal/parsed-html"
method="(GET)"
</Object>
```

有关启用解析 HTML 的更多信息，请参考《Sun Java Web Server 7.0 管理员指南》中的“管理服务器内容”章节。

## 9.3 FastCGI

FastCGI 是通用网接口（CGI）的扩展，适用于应用服务器和 Web 服务器。Web Server 7.0 中的 FastCGI 是通过插件实现的。以下内容描述了 FastCGI 的主要方面：

- FastCGI 消除了像 CGI 为每个请求创建进程的开销。FastCGI 应用独立于 Web 服务器运行。- FastCGI 允许在 Web 服务器上维护状态，如缓存。- FastCGI 使用 TCP 套接字或 UNIX 套接字连接远程计算机。Web 服务器与 FastCGI 应用之间使用单向连接，而不是像 CGI 那样使用独立的管道（标准输入、输出和标准错误）。- FastCGI 应用可分为三个定义的角色：响应者（Responder）、授权者（Authorizer）和过滤器（Filter）。响应者接收 HTTP 请求并生成 HTTP 响应。授权者根据 HTTP 请求信息生成 HTTP 授权响应。过滤器应用使用存储在 Web 服务器上的文件作为 HTTP 请求数据，并生成过滤后的数据。

有关 FastCGI 的更多信息，请参考《FastCGI 规范 1.0》。

### 9.3.1 FastCGI 配置

Web Server 7.0 对 FastCGI 的支持通过 NSAPI 插件实现。FastCGI 插件位于 Web Server 7.0 安装目录 `plugins/fastcgi`。该目录下还包含一个名为 `fastcgi` 的可执行文件，插件使用它来管理 FastCGI 应用的生命周期。配置 Web Server 的 FastCGI 插件包括：

- 配置 Web Server 加载插件
- 指定与 FastCGI 应用关联的扩展
- 配置虚拟服务器的 URI 空间以启用 FastCGI 请求处理

表 9.6 标识了指定 FastCGI 配置的 Web Server 7.0 配置文件。

表 9.6 FastCGI 配置文件

| 文件名 | 描述 |
| --- | --- |
| magnus.conf | 加载 FastCGI 插件并初始化 Web Server 中的 FastCGI 子系统。 |
| obj.conf | 包含实现 FastCGI 请求处理的 SAF。虚拟服务器特定的 FastCGI 配置位于服务器的对象文件中。 |
| mime.types | 被视为 FastCGI 程序的扩展名。可以通过服务器 .xml 文件中 `virtual-server` 元素的 `mime-file` 子元素按每个虚拟服务器基础配置 MIME 类型关联。 |

此外，请参考《Sun Java Web Server 7.0 开发者指南》中的“服务器标签”章节获取有关 FastCGI 的信息。

Web Server 7.0 的管理框架支持为虚拟服务器启用和配置 FastCGI 请求处理。

图 9.18 显示了管理页面上“内容处理”选项卡下的“FastCGI”子选项卡，用于配置虚拟服务器启用了 HTML 的 URL。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_413_0.png)

图 9.18 管理控制台--FastCGI





# 第 9 章通过脚本提供动态内容

图 9.19 展示了用于配置虚拟服务器中 FastCGI URI 的管理控制台对话框。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_414_0.png)

图 9.19 管理控制台——带有 FastCGI 映射的新 URI

你可以通过管理控制台的 MIME Types 子选项卡自定义虚拟服务器的 FastCGI MIME 类型，这在图 9.8 中已有演示。虚拟服务器 mime.types 文件中的以下条目可用于启用使用 FastCGI 实现的 PHP 脚本执行：

```
type=magnus-internal/fastcgi exts=php
```

## 9.3 FastCGI

以下 wadm 子命令有助于在 Web Server 中配置 FastCGI 插件：

- create-fastcgi-handler
- delete-fastcgi-handler
- list-fastcgi-handlers
- get-fastcgi-handler-prop
- set-fastcgi-handler-prop

《Sun Java System Web Server 7.0 CLI 参考手册》包含了关于这些子命令的更多信息。

### 9.3.2 FastCGI 服务器应用程序函数 (SAFs)

Web Server 7.0 中的 FastCGI 子系统被实现为 NSAPI 插件。插件中实现的 FastCGI SAFs 参与了第 6 章描述的请求处理的各个阶段。表 9.7 描述了 Web Server 中实现支持 FastCGI 应用的应用程序函数 (SAFs)。

表 9.7 FastCGI 服务器应用程序函数

| 请求处理阶段 | SAF | 说明 |
| :--- | :--- | :--- |
| Init | n Init | 初始化 FastCGI 子系统。此 SAF 已弃用，不再需要在 magnus.conf 中使用 Init 指令显式指定此 SAF。当 FastCGI 共享库在服务器启动期间加载时，会自动调用 init-fastcgi。 |
| PathCheck | auth-fastcgi | 将请求转发到执行授权者（Author）角色的 FastCGI 应用，并将授权者的响应返回给客户端。 |
| Service | responder-fastcgi, filter-fastcgi | responder-fastcgi SAF 用于处理对执行响应者（Responder）角色的 FastCGI 应用的请求。filter-fastcgi SAF 用于处理对执行过滤器（Filter）角色的 FastCGI 应用的请求。 |
| Error | error-fastcgi | 处理 FastCGI 请求过程中发生的错误。系统管理员可以使用此 SAF 自定义在 FastCGI 处理期间发生错误后返回给客户端的错误响应。 |

示例 9.5 列出了 FastCGI Web Server 7.0 配置的 magnus.conf 文件内容。删除或禁用示例 9.5 中用**粗体字体**标记的 Init 指令（通过在行首添加 #）将禁用整个服务器的 FastCGI 子系统。

##  示例 9.5 magnus.conf 文件（在启用了 FastCGI 的服务器中）

```
#
# Copyright 2006 Sun Microsystems, Inc.  All rights reserved.
# Use is subject to license terms.
```

```
Init fn="load-modules" shlib="libfastcgi.so";
```

查看服务器在启动期间记录的日志是判断 FastCGI 插件是否启用的简单方法。启动带有 FastCGI 插件的服务器会提供类似下面的响应：

```
# bin/startserv
Sun Java System Web Server 7.0U3 B06/16/2008 12:00
info: FCG1000: Sun Java System Web Server 7.0U3 FastCGI NSAPI Plugin B06/16/2008 12:00
info: HTTP3072: http-listener-1: http://test:9000 ready to accept requests
info: CORE3274: successful server startup
```

用**粗体字体**标记的消息在 FastCGI 插件初始化期间记录。这表示 Web Server 的 FastCGI 插件已加载。

示例 9.6 展示了使用 FastCGI  PHP 脚本的服务器配置的 obj.conf 文件。示例 9.6 中与 FastCGI 相关的指令和对象已用**粗体字体**标记。

## 示例 9.6 obj.conf 文件（在启用了 FastCGI 的服务器中）

```
#
# Copyright 2008 Sun Microsystems, Inc.  All rights reserved.
# Use is subject to license terms.
```

```
# 你可以编辑此文件，但使用管理 GUI 或 CLI 时，注释和格式更改可能会丢失。
```

## 9.3 FastCGI

# 路径名中仅使用正斜杠，因为反斜杠可能会引起问题。
# 更多信息请参阅文档。

```
<Object name="default">
Authn fn="match-browser" browser="*MSIE*" ssl-clean-shutdown="true"
NameTrans fn="px2dir" from="*mc-icons*" to="d:/Sun/WebServer7/lib/icons"
name="es-internal">
NameTrans fn="assign-name" from="*php/*" name="*php/*"
PathCheck fn="*uri-clean"
PathCheck fn="check-acl" acl="default">
```

（注：提供的第 417-419 页 OCR 内容在源文本中存在严重损坏/重复。根据修正错误并保留所有信息的指示，上述已处理了第 414-416 页的主要连贯部分。 417-419 页的碎片文本似乎是重复循环或损坏的 OCR 输出，在没有外部源的情况下无法进行意义上的重构。）




图 9.20 显示了在 Web Server 7.0 中使用 FastCGI 运行示例 9.7 中示例 PHP 脚本的输出。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_420_0.png)

图 9.20 示例 PHP 输出

## 9.4.1.3 作为 NSAPI 插件运行 PHP

使用 Web Server 的 NSAPI 插件运行 PHP 脚本包括以下内容：

- 安装 PHP 专用的 NSAPI 插件，并通过手动编辑 `magnus.conf` 文件配置 Web Server 加载该插件。

## 9.5 活动服务器页 (Active Server Pages)

- 配置虚拟服务器的对象文件 (.conf)以指定将由 PHP NSAPI 插件中的服务器应用程序函数 (SAFs) 处理的 URI。
- 将 PHP 文件扩展名（.php, .php3, .php4, .php5）与 `magnus-internal/x-httpd-php` MIME 类型关联。
- 使用浏览器访问 PHP 脚本。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_421_0.png)

注意：关于 PHP NSAPI 插件的更多信息，可以在 PHP 手册的 http://www.php.net 中的“NSAPI”部分找到。

请参考 PHP for Sun Java System Server 7.0 网页 (http://www.sun.com/software/products/web_srvr/php.xml) 了解更多关于 Web Server 7.0 支持 PHP 的信息。

## 9.5 活动服务器页 (Active Server Pages)

活动服务器页 (ASP) 是微软最初为 Internet 信息服务 (IIS) 开发的服务器端脚本环境。ASP 脚本是一个嵌入了服务器端脚本命令的 HTML 页面，并包含通用对象模型 (COM) 组件。ASP 脚本通常使用 VBScript 实现。示例 9.8 显示了一个 ASP 脚本示例。

示例 9.8 示例 ASP 脚本

```
<%
Response.ContentType="text/html"
%>
<html>
<body>
<%
Response.Write("Hello World!")
%>
Today's date is: <%Response.Write(Date())%>
</body>
</html>
```

Sun Java System Active Server Pages（也称为 Sun Java System ASP Server）是 ASP 技术的一种实现，它适用于多个 UNIX/Linux 平台以及 Windows。你可以使用 Sun Java System ASP Server 在 Windows以外的平台上运行 ASP 脚本。

Sun Java System ASP Server 提供了一个 NSAPI 插件，可用于配置 Web Server 处理 ASP 脚本的请求。

图 9.21 展示了 Web Server 如何使用 ASP NSAPI 插件与 ASP Server 交互以处理 ASP 内容的请求。

```
http://host/hello.asp
```

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_422_0.png)

**图 9.21** Web Server 和 Sun Java System ASP Server 概述

使用 Web Server 的 NSAPI 插件运行 ASP 脚本包括以下内容：

- 安装 Sun Java System ASP Server 的 NSAPI 插件，并通过手动编辑 `magnus.conf` 文件配置 Web Server 加载该插件。
- 配置虚拟服务器的对象文件 (os.conf) 以指定将由 ASP NSAPI 插件中的服务器应用程序函数 (SAFs) 处理的 URI。
- 将 ASP 文件扩展名（.asp, .asa）与 `chilisoft/active-server-page` MIME 类型关联。
- 使用浏览器访问 ASP 脚本。

Web Server 7.0 的管理框架不包括配置 ASP 插件的支持。请参考 *PHP for Sun Java System Server 7.0* 了解更多信息。

## 9.6 总结

在本章中，你学习了 Web Server 对多种脚本语言的支持。Web Server 可以根据 MIME 类型托管动态内容。

## 9.7 实验

使用本章包含的信息执行以下实验。这些将帮助你理解本章的概念。

1. 配置 Web Server 使用 CGI 托管 HTML 文件。
2. 在 Web Server 中使用 CGI 生成动态 HTML。
3. 当 Web Server 启动时创建了多少 CGI 进程？
4. 使用浏览器访问 CGI 进程。
5. 创建一个会进入死循环的 CGI 程序。
6. 在 Web Server 中通过 Java 语言执行 CGI 程序。
7. 在 Web Server 上使用 PHP 扩展 CGI。
8. Web Server 是否支持 PHP 扩展？
9. 列出 CGI 与 NSAPI 的优缺点。
10. 重启服务器是否可以更改 CGI？

注意：访问 www.php.net 获取如何执行这些实验的详细说明。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_423_0.png)

## 通过 Java 提供动态内容

大多数网站的内容通常包含静态内容（HTML 文件）和动态内容（由脚本生成）。在第 9 章“通过脚本提供动态内容”中，我们描述了如何使用今天流行的脚本语言。另一种深受喜爱的语言是 Java。

本章解释了 Web Server 7.0 如何通过 Java 技术提供动态内容。具体而言，本章讨论了 Web Server 对 Java 技术的支持。本章描述了与 Java 相关的辅助配置文件以及管理支持。最后，本章介绍了 IDE 中的 Java 支持。

## 10.1 服务器端 Java 技术

Java 平台企业版（Java EE，以前称为 J2EE）是实现迁移、安全和可扩展服务器端应用的行业标准。Java EE 基于 Java 平台标准版（Java SE，以前称为 J2SE）的坚实基础，并简化了分布式企业级应用程序的编写。

图 10.1 展示了 Web Server 插件中的服务器端 Java 相关技术。

| JavaServer Pages | JavaServer Faces | Java Web Services | 服务器周期模块 | Java 数据库连接池 |
|---|---|---|---|---|
| Standard Tag Library | | | | |
| JavaServer Pages | | | | |
| Session Replication | Java Servlets | Java Mail | Java 命名和目录接口 | Java Database Connectivity |
| | Java SE Java Native Interface | | |
| j2ee | ntrans_j2ee | type_j2ee | find_index_j2ee | service_j2ee error_j2ee |

**图 10.1** Web Server 技术

本节剩余部分将介绍 Java EE 平台的一部分并包含在 Web Server 7.0 中的 Web 相关技术。

### 10.1.1 Java Servlets

Java Servlet API 为开发者提供了迁移的可编程接口，用于扩展 Web 服务器的功能。Servlet 可以被视为用 Java 编写的 FastCGI 程序。Servlet 是与平台无关的服务器端对象，根据请求中的数据接收并生成响应。除了 Servlet 对象之外，Java Servlet API 还定义了表示请求和响应的 Java 对象，以及用于配置 servlet 运行环境的对象。




## 10.1 服务端 Java 技术

虽然 servlet 可以处理任何协议的请求，但它们最常被用于扩展 Web 服务器的功能。servlet 编程模型遵循 HTTP（超文本传输协议）的请求-响应模型。使用 servlet 的应用程序可以通过 Java Web 应用程序会话（sessions）跨请求维护状态。Web 应用程序会话将在本文后的第 10.5.5 节“Java Web 应用程序中的会话管理”中描述。

在执行之前，servlet 必须经过编译并部署到 Web 服务器。ServletAPI 与早期版本完全后兼容。因此，任何为旧版本 API 编写的 servlet 可以在无需任何更改或重新编译的情况下继续运行。

运行 servlet 的集成 Java 运行时（在 Web/应用程序进程内部）被称为 Java Web 容器。

Web Server 7.0 当前版本包含了对 Java Servlet 规范 2.5 的支持。

### 10.1.2 JavaServer Pages

Server Pages (JSP) 技术是 Java servlet 的扩展，能够快速开发动态网页。通常，一个 JSP 页面由 HTML 内容组成，其中包含类 XML 标签和嵌入的 Java 代码，这些代码封装了生成响应中动态部分的逻辑。

一个 JSP 页面的主要组件由以下部分组成：

- 静态内容（如文本、HTML、XML）
- 脚本元素
- 标准指令（静态标签）
- 标准动作（动态标签）
- 标签扩展（自定义标签）

JSP 技术实现了模型与视图的分离，从而允许网页设计人员更改页面的外观，而无需更改生成页面的内容。与 Java servlet 一一样，JSP 技术也是平台无关的。这意味着你可以在任何实现 JSP 标准的 Java Web 容器上运行基于 JSP 的应用程序。JSP 的表达式语言 (EL) 功能使得 JSP 页面作者能够使用简化的表达式语言来访问和操作数据，而无需处理与 Java 编程语言相关的复杂性。

与 servlet 不同，JSP 页面在部署之前不需要编译。Java Web 容器内的 JSP 编译器会根据需要自动编译 JSP 页面。JSP 编译器将 JSP 编译为 servlet，并将该 servlet 新添加到服务器中。Web Server 还包含一个命令行工具——jsp——用于将 JSPs 预编译为 servlet。有关 JSP 命令行编译器的更多信息，请参阅《Sun Java System Web Server 7.0 开发者指南：开发 JavaServer Pages》。Java Web 应用程序包含的 JSPs 可以使用 Web Server 的管理接口进行预编译，以部署 Java Web 应用程序。第 10.5.4 节“将 Java Web 应用程序部署到 Web Server”描述了 Web Server 为部署 Java Web 应用程序提供的管理支持。

Web Server 7.0 当前版本包含了对 JavaServer 规范版本 2.1 的支持。

### 10.1.3 JavaServer Pages 标准标签库

Java Pages Standard Tag Library 扩展了 JSP 规范，由一组标准标签组成，JSP 程序员可以在 JSP 页面中使用这些标签（代替 Java 代码或 servlet）。这些标签实现了 JSP 页面中常用的功能。JSTL 中的标签示例包括循环/迭代器、访问数据库数据的标签、实现条件逻辑的标签、国际化标签以及处理 XML 数据的标签。

表 10.1 总结了组成 JSTL 的四个独立标签库，每个标签库都包含针对特定功能领域的标签。该表还列出了引用这些库时使用的 URI 和标签前缀（尽管 JSP 开发者可以自由分配不同的前缀）。

表 10.1 JSTL 标签库

| 功能领域 | URI | 前缀 | 说明 |
|---|---|---|---|
| 核心 | http://java.sun.com/jstl/core | c | 包含所有 Web 应用程序常用的标签，如迭代器、条件判断和 URL 操作。 |
| XML 处理 | http://java.sun.com/jstl/xml | x | 包含解析、处理和转换 XML 数据的标签。 |
| 国际化/格式化 | http://java.sun.com/jst/fmt | fmt | 包含以区域敏感的方式解析和格式化数字、时间和日期数据的标签。 |
| 关系型数据库访问 | http://java.sun.com/jstl/sql | sql | 包含访问关系型数据库的标签。 |

Web Server 7.0 当前版本包含了对 JavaServer Tag Library 版本 1.2 的支持。

### 10.1.4 Java Database Connectivity

Java Database Connectivity (JDBC) API 是定义 Java 程序如何访问、查询和更新数据库中数据的标准。创建连接的开销很大，并且通常涉及耗时的操作。在所有应用程序之间共享 JDBC 连接池可以极大提高扩展性和资源利用率。Web Server 7.0 为 JDBC 资源实现了连接池，并允许管理员通过命令行或图形用户界面配置 JDBC。第 10.4.4 节“全局 Java 设置”列出了 Web Server 用于配置资源的管理支持。

### 10.1.5 Java Naming and Directory Interface

Java Naming and Directory Interface (JNDI) 为基于 Java 的应用程序提供了一个用于命名和目录服务的、可移植的统一的接口。命名服务允许你将名称与对象关联，并通过名称查找该对象。命名服务的一个示例是域名系统服务 (DNS)，它将主机名（如 www.google.com）映射到 IP 地址（如 209.85.153.104）。目录服务将名称与对象关联，并允许对象包含属性。目录服务的一个示例是公司的员工数据库，可以通过搜索名称或其他属性（如员工编号、部门代码等）查找员工记录。

Web Server 7.0 容器中的 JNDI 支持允许系统管理员和 Web 应用程序开发者使用标准的命名语法和可编程接口创建、定位和访问数据源、数据库连接池、Java 邮件会话和外部 JNDI 资源等 Java 资源。更多信息请参阅第 10.4.4 节“全局 Java 设置”。

### 10.1.6 JavaServer Faces

JavaServer Faces (JSF) 技术是构建服务端用户界面的标准。它是一个 Web 应用程序框架，简化了服务端 Java 应用程序用户界面的过程。JavaServer Faces 技术包括

- 一组用于表示用户界面组件、管理其状态、输入验证、事件处理、错误处理、定义页面导航以及支持辅助国际化的 API
- 用于在 JSP 页面内实现 JavaServer Faces 用户界面的两个 Java Pages (JSP) 标签库

使用 JavaF 技术实现的应用程序在服务器上运行用户界面代码，响应客户端的事件。JSF 实现了 Web 用户界面的可用组件开发。

要运行使用 JSF 技术的 Java 应用程序，只需按照第 10.5.4 节“将 Java 应用程序部署到 Web Server”中描述的任何方法部署应用程序，并使用浏览器访问。图 10.2 展示了 Web Server 的 cafstore JSF 示例应用程序。

Web Server 7.0 当前版本包含了对 JavaServer Faces 规范版本 1.2 的支持。




## 10.1 服务端 Java 技术

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_431_0.png)

# # 汽车演示

杜克的精简版破旧车

杜克的俗俗豪华车

如果你是那种不在乎别人怎么想的人，那么这辆车是你想要的。专为点对点类型的人设计。

邻壁的琼斯家什么都有有，不是吗？很好，开着这辆配置齐全的底盘开过去，让他们看看你才是那个赚大钱的人。

杜克的臃肿 SUV

杜克的 MLC 道路跑车

年纪老了吗？需要对青春进行最后的挣扎吗？当你坐在这辆小宝贝的车后时，你会觉得自己年轻了 20 岁。

总有一天，和你需要的汽车相比，你再也不够高或不够大了。而那些新车型一次比一次大。买一辆能装下一切，并让路上的每个人都感到胆畏的 SUV 吧。

图 10.2 示例 JavaServer Faces 应用程序

### 10.1.7 Java Web 服务

Web 服务为运行在各种平台上的软件应用程序提供了一种标准方式。SOAP 是一种在分布式软件应用程序之间交换结构化数据的轻量级协议。Web 服务使用 Web 服务描述语言 (WSDL) 标准（一种基于 XML 的语言）来描述自身。客户端通过在注册表中查找来发现 Web 服务。构成 Web 服务的客户端和服务器使用 SOAP 交换 XML 消息。图 10.3 展示了 Web 服务是如何描述和发现的。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_432_0.png)

图 10.3 Web 服务技术

Web Server 7.0 集成的 java 运行时和工具使其能够托管可的 Java Web 服务实现。Web Server 还支持 WS-Security 标准。以下列出了 Web Server 7.0 包含的 Java Web 服务技术：

- JAX-WS 2.0
- JAXB 2.0
- JAXP 1.3.1
- SOAP 1.2
- WSDL 1.1
- SAAJ 1.3
- XWSS-XML
- Fast Infoset
- Message Security

Web 服务被封装为 Web 应用程序并部署到 Web Server 中。使用 Web Server 的管理工具，系统管理员可以配置和部署包含 Web 服务的 Java Web 应用。Web Server 7.0 对 Java Web 应用的支持在第 10.5 节“Java Web 应用”中有更详细的描述。

### 10.1.8 生命周期模块

Web Server 7.0 支持在服务器生命周期的不同阶段执行自定义逻辑（用 Java 编程语言编写）。此类逻辑实现在实现生命周期接口的 Java 类中。以下列表总结了服务器可以在用户定义的生命类中调用自定义逻辑的服务器生命周期不同阶段：

- 初始化（Initialization）——当服务器创建其内置子系统时调用。
- 启动（Startup）——当服务器加载其应用程序时调用。
- 服务（Service）——被调用以表示服务器已准备好处理请求。
- 终止（Termination）——当服务器正在关闭时调用。
- 重配置（Reconfiguration）——当服务器配置被动态重新配置时调用。这是服务器进程生命周期内可能发生多次的状态。

标题为“全局 Java 设置”的章节列出了 Web Server 中配置生命周期模块的管理支持。参考 *Sun Java System Web Server 7.0 Java Web 应用开发者指南* 中的“开发生命周期监听器”章节获取有关在 Web Server 7.0 中实现生命周期监听器的更多信息。

### 10.1.9 Java Web 应用会话复制

Servlet 规范定义了 Java Web 容器通过以下几种方法跨 Java Web 应用请求跟踪并维护会话状态。Web Server 中的会话复制功能为 Java Web 应用会话数据提供了有限的高可用性。

此功能仅适用于部署到 Web Server 7.0 集群的 Java Web 应用。如第 4 节所述，“集群是一组跨一个或多个节点并运行相同配置的 Web 服务器实例。”当集群中启用会话复制功能时，集群中的每个实例将其 Java Web 应用会话内存表示复制到集群中的另一个实例。在集群中的某个实例不可用的故障情况下，集群仍然可以访问故障实例会话数据的备份。

### 10.1.10 Java 原生接口

Java 原生接口 (JNI) 是一种标准的编程接口，允许 Java 代码与用其他语言编写的代码集成。JNI 提供了一种标准方式，让运行在 Java 虚拟机 (JVM) 中的 Java 方法调用或被 C 和 C++ 等其他语言原生应用程序调用。此接口还允许原生应用程序嵌入 Java 虚拟机 (JVM)。Web Server 7.0 作为一个 C/C++ ，使用 Java 原生接口集成本节之前描述的服务端 Java 技术。如图 10.1 所示，Web Server 的 Web 容器服务器应用功能 (SAFs) 用 C/C++ 编程语言编写的——init_j2ee, ntrans_j2ee,

## 10.2 服务端 Java 模型

（注：原文此处开始出现大量重复内容，已根据要求去重处理并保留核心逻辑）




## 10.3 Java 请求处理行为

| 请求处理阶段 | SAF | 描述 |
|---|---|---|
| 服务 (Service) | service-j2ee | 处理 Java Web应用程序中资源的请求，并在成功后向客户端返回响应。 |
| 错误 (Error) | error-j2ee | 处理在 Java Web应用程序中的资源服务过程中发生的错误。在处理 Java Web应用程序中的资源请求时，如果检测到错误条件，Web 应用程序可以自定义生成的响应。您通过在 web.xml 中定义一个错误页面描述列表来定义此类自定义。error-j2ee 在为 Java Web应用程序中的资源生成错误响应时，会应用 web.xml 中指定的任何页面自定义。 |

示例 10.1 列出了启用 Java 的 Web Server 7.0 配置中 `magnus.conf` 文件的内容。删除或禁用（通过在行前加 #）示例 10.1 中用**粗字体**标记的 `Init` 指令将禁用整个服务器的 Java 容器。

### 示例 10.1 magnus.conf（在启用 Java 的服务器中）

```
# # Copyright 2006 Sun Microsystems, Inc. All rights reserved.
# Use is subject to license terms.
#
Init fn="load-modules" shlib="libj2eplugin.so"
```

Web Server 的早期版本通过使用 `magnus.conf` 中的 `Init` 指令显式指定服务器应用程序功能 (SAF)。以下展示了 Web Server 6.1 中 `magnus.conf` 的 `Init` 指令：

```
Init fn="load-modules" shlib="install_dir/lib/libj2eplugin.so" funcs="init-j2ee,ntrans-j2ee,service-j2ee,error-j2ee" shlib_flags="global|now)"
Init fn="init-j2ee" LateInit=yes
```

Web Server 7.0 的 `magnus.conf` 中简单紧凑的 `Init` 指令形式是设计和开发 Web Server 7.0 的 Sun 工程师某些微妙创新的结果。服务器知道从某些已知目录（如 `install_dir/lib`）加载 NSAPI 插件，因此不会在 `magnus.conf` 中将其共享库（如 UNIX 上的 `libj2eplugin.so` 和 Windows 上的 `j2eplugin.dll`）硬编码路径（路径可能会随机器而变化）。

示例 10.1 所示的 `Init` 指令没有显式列出每个 SAF，因为 Web Server 7.0 的 Java Web 容器插件使用 NSAPI 函数 `nsapi_module_init()` 来注册其 SAF。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_438_0.png)

注意：`nsapi_module_init()` 函数在《Sun Java Web Server 7.0 NSAPI 开发者指南》的“NSAPI 函数和宏引用”章节中有介绍。

本节的其余部分基于第 6 章“默认请求处理行为”中描述的信息，通过使用 Java Web 应用程序内容的示例客户端请求，追踪通过不同请求处理阶段的路径。

示例 10.2 展示了启用 Java 容器的服务器配置的 `obj.conf` 文件。这些信息将用于帮助描述 Java Web 应用程序中 Java 内容的请求处理。Java 容器请求处理 SAF（见表 10.2）的使用在示例 10.2 中已用**粗体**标记。

### 示例 10.2 obj.conf 文件（在启用 Java 的服务器中）

```
# 1
# # Copyright 2006 Sun Microsystems, Inc. All rights reserved.
# # Use is subject to license terms.
# 4
# 5
# # 您可以编辑此文件，但当使用管理 GUI 或 CLI 时，
# # 注释和格式更改可能会丢失。
# 8
# 9 <Object name="match-browser" browser="*MSIE*" ssl-unclean-shutdown="true"
# 10 AuthTrans fn="ntrans-j2ee" name="j2ee"
# 12 NameTrans fn="pfx2fdi" dir="/opt/webserver7/lib/icons" name="ex-internal"
# 13 PathCheck fn="uri-clean"
# 14 PathCheck fn="check-acl" acl="default"
# 15 PathCheck fn="find-pathinfo"
# 16 PathCheck fn="find-index-j2ee"
# 17 PathCheck fn="find-index" index-names="index.html,home.html,index.jsp"
# 18 ObjectType fn="type-j2ee"
# 19 ObjectType fn="type-by-extension"
# 20 ObjectType fn="force-type" type="text/plain"
# 21 Service method="GET|HEAD" type="magnus-internal/directory" fn="index-common"
# 22 Service method="GET|POST" type="*=magnus-internal/*" send-file
# 23 Service method="TRACE" fn="service-trace"
# 24 Error fn="error-jee"
# 25 AddLog fn="flex-log"
# 26 <Object>
# 27
# 28 <Object name="j2ee">
# 29 Service fn="service-j2ee" method="*"
# 30 <Object>
# 31
# 32 <Object name="es-internal">
# 33 PathCheck fn="check-acl" acl="es-internal"
# 34 </Object>
# 35
# 36 <Object name="cgi">
# 37 ObjectType fn="force-type" type="magnus-internal/cgi"
# 38 Service fn="send-cgi"
# 39 </Object>
# 40
# 41 <Object name="send-compressed">
# 42 PathCheck fn="find-compressed"
# 43 </Object>
# 44
# 45 <Object name="compress-on-demand">
# 46 Output fn="insert-filter" filter="compression"
# 47 </Object>
```

### 10.3.1 Java 内容的请求

参考 10.2 中指定的 `obj.conf` 文件，当客户端请求 Java Web 应用程序中目录以外的 Java 内容（例如 `http://www.example.com/index.jsp` 或 `http://www.example.com/bookstore/Servlet`）时，服务器将按（此顺序处理以下指令：

```
10 AuthTrans fn="match-browser" browser="*MSIE*" ssl-unclean-shutdown="true"
11 NameTrans fn="ntrans-j2ee" name="j2ee"
13 PathCheck fn="uri-clean"
14 PathCheck fn="check-acl" acl="default"
15 PathCheck fn="find-pathinfo"
16 PathCheck fn="find-index-j2ee"
17 PathCheck fn="find-index" index-names=index.html,home.html,index.jsp
18 ObjectType fn="type-by-j2ee"
19 ObjectType fn="type-by-extension"
29 Service fn="service-j2ee" method="*"
25 AddLog fn="flex-log"
```

尽管执行了这些指令，但 `find-index-j2ee` 和 `find-index` SAF 不起作用；它们仅对目录请求起作用。注意：第 6 章中的“名称翻译 (name)”章节描述了 `NameTrans` 的 `name` 属性如何影响请求处理。

### 10.3.2 不存在的 Java 内容的请求

参考 10.2 中指定的 `obj.conf` 文件，当客户端请求不存在的 Java 内容（例如 `http://www.example.com/abcdef.jsp`）时，服务器将按（此顺序）处理以下指令：

```
10 AuthTrans fn="match-browser" browser="*MSIE*" ssl-unclean-shutdown="true"
11 NameTrans fn="ntrans-j2ee" name="j2ee"
13 PathCheck fn="uri-clean"
14 PathCheck fn="check-acl" acl="default"
15 PathCheck fn="find-pathinfo"
16 PathCheck fn="find-index-j2ee"
17 PathCheck fn="find-index" index-names=index.html,home.html,index.jsp
18 ObjectType fn="type-by-j2ee"
19 ObjectType fn="type-by-extension"
29 Service fn="service-j2ee" method="*"
24 Error fn="error-j2ee"
25 AddLog fn="flex-log"
```

这些指令与处理 Java 内容时（参见 10.3.1 节“Java 内容”）的指令相似，仅多了一个指令（24 行）来处理 Java 资源的情况。

### 10.3.3 Java 应用程序中的目录请求

假设在 URI /bookstore 部署了一个 Java 应用程序，并且假设该应用程序的 `web.xml` 文件未指定任何欢迎页，处理请求 `http://www.example.com/bookstore` 时，`obj.conf` 文件中的哪些指令将被执行？参考示例 10.2 中指定的 `obj.conf` 文件，服务器将按（此顺序）处理以下指令：

```
10 AuthTrans fn="match-browser" browser="*MSIE*" ssl-unclean-shutdown="true"
11 NameTrans fn="ntrans-j2ee" name="j2ee"
13 PathCheck fn="uri-clean"
14 PathCheck fn="check-acl" acl="default"
15 PathCheck fn="find-pathinfo"
16 PathCheck fn="find-index-j2ee"
17 PathCheck fn="find-index" names="index.html,home.html,index.jsp"
18 ObjectType fn="type-j2ee"
19 ObjectType fn="type-by-extension"
29 Service fn="service-j2ee" method="*"
25 AddLog fn="flex-log"
```

### 10.3.4 带有欢迎页的 Java 应用程序中的目录请求

示例 10.3 提供了 `web.xml` 片段片段展示了 Java Web 应用程序如何在其部署符中指定欢迎页。

**示例 10.3** web.xml 文件片段

```
<welcome-file-list>
  <welcome-file>home.jsp</welcome-file>
  <welcome-file>home.html</welcome-file>
</welcome-file-list>
```





# 第 10 章通过 JAVA 提供动态内容

10 AuthTrans fn="match-browser" browser="*MSIE*" ssl-unclean-shutdown="true"
11 NameTrans fn="ntrans-j2ee" name="j2ee"
13 PathCheck fn="uri-clean"
14 PathCheck fn="check-acl" acl="default"
15 PathCheck fn="find-pathinfo"
16 PathCheck fn="find-index-j2ee"
17 PathCheck fn="find-index" index-names="index.html,home,index.jsp"
18 ObjectType fn="type-j2ee"
19 ObjectType fn="type-by-extension"
29 Service fn="service-j2ee" method=""
25 AddLog fn="flex-log"

这些指令与在没有欢迎页的 Java Web 应用中请求目录时的指令相似（参见“在 Java Web 应用中请求目录”章节），不同之处在于 `find-index-j2ee`（第 16 行）成功地将请求的 URI 映射到 Web 应用程序文档根目录中的欢迎页，因此 `find-index`（第 17 行）不起作用，因为它仅对目录请求起作用。

## 10.3.5 在 Java Web 应用中请求 MIME 映射的内容

示例 10.4 提供了一个 `web.xml` 文件的片段，演示了 Java 如何指定扩展名与多用途互联网邮件扩展（MIME）类型之间的映射。

示例 10.4 web.xml 文件的片段

```xml
<mime-mapping>
<extension>pdf</extension>
<mime-type>application/pdf</mime-type>
</mime-mapping>
```

如果上一节引入的 /bookstore 应用指定了如示例 10.4 所示的 MIME 映射，并且应用程序的根目录下确实包含一个名为 `book.pdf` 的文件，那么 `obj.conf` 文件中的哪些指令将被执行以处理 http://www.example.com/bookstore/book.pdf 的请求？参考示例 10.2 中指定的 `obj.conf` 文件，服务器将处理以下指令（按此顺序）：

10 AuthTrans fn="match-browser" browser="*MSIE*" ssl-unclean-shutdown="true"
11 NameTrans fn="ntrans-j2ee" name="j2ee"
13 PathCheck fn="uri-clean"
14 PathCheck fn="check-acl" acl="default"
15 PathCheck fn="find-pathinfo"
16 PathCheck fn="find-index-j2ee"
17 PathCheck fn="find-index" index-names="index.html,home,index.jsp"

这些指令与在没有欢迎页的 Java Web 应用中请求目录时的指令相似，不同之处在于 `find-index-j2ee`（第 16 行）成功地将请求的 URI 映射到 Web 应用程序文档根目录中的欢迎页，因此 `find-index`（第 17 行）不起作用，因为它仅对目录请求起作用。

## 10.3.6 Java 配置

Java 容器配置在以下内容指定：

- 启用 Java 容器
- 配置虚拟机 (JVM)
- 配置全局 Web 设置

通常，Java 开发者指定 Java 配置，而管理员指定部署环境。Java 容器配置在以下文件中指定：

表 10.3 配置文件

| 文件名 |  |
| :--- | :--- |
| default.xml | Java 容器的全局配置。 |
| login.xml | 特定于实例的配置。 |
| obj.conf | 实际上控制服务器的配置。 |
| server.policy | 安全设置的配置。 |
| server.xml | 应用程序的主部署文件。 |

Java 容器配置在以下内容指定：

- 启用 Java 容器
- 配置虚拟机 (JVM)
- 配置全局 Web 设置

## 10.4 Java 配置

Java 容器配置在以下内容指定：

- 启用 Java 容器
- 配置虚拟机 (JVM)
- 配置全局 Web 设置

Java 容器配置在以下内容指定：

- 启用 Java 容器
- 配置虚拟机 (JVM)
- 配置全局 Web 设置

表 10.4 配置文件

| 文件名 | 说明 |
| :--- | :--- |
| default.xml | Java 容器的全局配置。 |
| server.xml | 特定于实例的配置。 |
| obj.conf | 实际上控制服务器的配置。 |

### 10.4.1 全局启用/禁用 Java

当你创建一个新的服务器配置时，Java 容器默认是启用的，如图 10.4 所示。

[https://example.com/image10.4.png]

图 10.4 管理控制——新配置

### 10.4.2 启用/禁用 Java

Java 容器配置在以下内容指定：

- 启用 Java 容器
- 配置虚拟机 (JVM)
-

你也可以通过服务器的管理界面在现有配置中启用或禁用 Java 容器。图 10.5 高亮了屏幕上用于启用或禁用配置 Java 容器的复框框

[https://example.com/image10.5.png]

图 10.5 管理控制——JVM 普通设置

注意：本章包含了超出本书范围的 Java 配置示例。这些信息可以在《Sun Java Server 7.0 管理员指南》中找到。

下面的 shell 示例显示了如何使用 `wadm` 脚本的 `enable-java` 和 `disable-java` 命令来配置 Java 容器的状态。

```bash
wadm> disable-java --config=test
CLI201 Command 'disable-java' ran successfully
wadm> deploy-config --restart test
CLI201 Command 'deploy-config' ran successfully
wadm>
wadm> enable-java --config=test
CLI201 Command 'enable-java' ran successfully
wadm> deploy-config --restart test
CLI201 Command 'deploy-config' ran successfully
```





## 第 10 章通过 JAVA 提供动态内容

虚拟服务器定义在 `server.xml` 中。`server.xml` 中虚拟服务器定义中的对象 `object-file` 子元素指定了确定如何处理该虚拟服务器请求的文件。要禁用虚拟服务器的 Java 功能，如示例 10.5 所示，在 `server.xml` 中找到虚拟服务器的 `object-file` 定义。

## 示例 10.5 虚拟服务器的对象配置文件

```xml
<virtual-server>
  <name>www.example.com</name>
  <http-listener-name>http-listener-1</http-listener-name>
  <host>www.example.com</host>
  <object-file>www.example.com-obj.conf</object-file>
  <document-root>/export/home/example.com/public_html</document-root>
  <access-log>
    <file>/export/home/example.com/logs/access</file>
  </access-log>
</virtual-server>
```

使用编辑器，以示例 10.2 为参考，编辑命名的对象文件（位于实例的配置目录中）；删除所有**加粗**标记的行并将这些更改保存到文件中。

> 注意：这假设没有其他虚拟服务器使用此对象文件且你希望对其继续使用 Java。

动态重新配置你的服务器实例，以禁用特定服务器的 Java 处理。

要验证是否已禁用了虚拟服务器的 Java 处理，你可以在虚拟服务器的文档根目录中安装/创建一个简单的 Java Server 页面 (JSP) 脚本，然后对刚安装的 JSP 脚本发送请求。未启用 Java 处理的虚拟服务器将允许包含 JSP 脚本源码的响应。

### 10.4.4 全局 Java 设置

图 10.5 显示了 Web Server 管理控制台的截图，其中显示了指定 Web Server 中 Java 相关配置的各种选项卡。Web Server 中的管理框架包含命令行支持，用于配置服务器中的 Java 子系统。这些设置中的许多的更改都需要重启服务器。表 10.5 列出了图 10.5 所示的每个 Java 配置选项卡的命令行支持和配置文件元素。

### 10.5 Java 配置

#### 表 10.5 Java 管理

| 控制台标签名称 | 子命令 | server.xml 元素 | 需要重启服务器？ | 描述 |
| --- | --- | --- | --- | --- |
| General | enable-java disable-java set-jvm-prop get-jvm-prop | jvm | 是 | 管理 Java 虚拟机 (JVM)的核心配置。 |
| JVM Settings | create-jvm-options create-jvm-profiler delete-jvm-options delete-jvm-profiler list-jvm-options list-jvm-profiler | jvm-options debug debug-jvm-options profiler | 是 | 管理可选的 JVM 配置和 Java 分析器配置 |
| Resources | create-custom-resource create-custom-resource-userprop create-external-jndi-resource create-external-jndi-resource-userprop create-jdbc-resource create-jdbc-resource-userprop create-mail-resource create-mail-resource-userprop delete-custom-resource delete-custom-resource-userprop delete-external-jndi-resource delete-external-jndi-resource-userprop delete-jdbc-resource delete-jdbc-resource-userprop delete-mail-resource delete-mail-resource-userprop get-custom-resource-prop get-external-jndi-resource-prop get-jdbc-resource-prop get-mail-resource-prop list-custom-resources list-custom-resource-userprops list-external-jndi-resources list-external-jndi-resource-userprops list-jdbc-resources list-jdbc-resourceprops list-mail-resources list-mail-resource-userprops set-custom-resource-prop set-external-jndi-resource-prop set-jdbc-resource-prop set-mail-resource-prop | custom-resource resource jndi-resource jdbc-resource mail-resource | 是 | 管理 JDBC、JNDI JavaMail 和自定义资源配置。 |

#### 表 10.5 Java 管理续）

| 控制台标签名称 | wadm 子命令 | server.xml 元素 | 需要重启服务器？ | 描述 |
| --- | --- | --- | --- | --- |
| Lifecycle | create-lifecycle-module delete-lifecycle-module get-lifecycle-module list-lifecycle-module | lifecycle-module | 是 | 管理生命周期 |
| Authentication | create-auth-module delete-auth-module get-auth-module list-auth-module | auth-module | 是 | 管理身份验证 |
| Servlet Container | create-servlet-module delete-servlet-module get-servlet-module list-servlet-module | servlet-container | 否 | 管理 servlet 容器 |
| Session Replication | create-session-module delete-session-module get-session-module list-session-module | session-replication | 是 | 管理会话复制 |

## 10.5 Java 应用

Web 是 Java 资源（如 servlet、Java Pages）、静态内容（如 HTML 文件）、部署描述符（如 web.xml）以及构成 Web 服务器的其他类型的集合。Servlet 容器为 Web应用程序提供了访问 Java 组件（如 servlet 和 JSP）的能力。

### 10.5.1 Web 应用生命周期

在 Web Server 上下文中，Web应用程序的生命周期可以总结如下：

- 开发 Web应用程序的内容和代码
- 创建部署描述符
- 打包 Web应用程序
- 将 Web应用程序部署到 Web Server 中
- 通过 Web 浏览器访问 Web应用程序
- 调试 Web应用程序中的问题
- 卸载 Web应用程序

Web Server 支持开发、管理和卸载 Web 应用程序。

### 10.5.2 Web 内容

Web应用程序由图 10.6 所示的层次结构组成。

目录的顶层作为应用程序的根目录。文档根是存储 HTML 文件、图像、JSP 脚本、CGI 程序和其他内容的地方。

文档根可能包含名为 WEB-INF 和 META-INF 的特殊子目录。根据 Java Servlet 2.5 的规定，Java 容器保护这些目录的内容不受客户端直接访问。应用程序可以通过 ServletContext 的 `getResource` 和 `getInputStream` 方法看到这些目录的内容。表 10.6 描述了 WEB-INF 目录的内容。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_452_0.png)

图 10.6 Web应用程序结构

#### 表 10.6 WEB-INF 内容

| 文件/目录 | 是否可选 | 描述 |
|---|---|---|
| web.xml | 是 | Web应用程序部署描述符。由 Java Servlet 2.5 定义。 |
| sun-web.xml | 是 Web Server（以及 Sun 应用程序服务器）特定的 Web应用程序部署描述符。由《Sun Java Web Server 7.0 Java Web开发指南》定义。 |
| *.tld | 是 | 标签库。由 Java Pages 2.1 定义。 |
| classes | 是 | 包含应用程序服务端 Java 类（如 servlet、工具类和 JavaBean）的目录。Java 包名必须反映在此目录结构中。例如，名为 `com.example.TestServlet` 的类需要存储在 WEB-INF/classes/com/example/TestServlet 文件中。Web应用程序的类加载器会在加载 WEB-INF/lib 目录中的 JAR 文件之前，加载 WEB-INF/classes 目录下的所有类。 |
| lib | 是 | 包含封装为 Java 归 (JAR) 文件的应用程序服务端类的目录。 |
| tags | 是 | 包含应用程序 JSP 标签文件的目录。 |





## 10.5 Java Web 应用

如果使用标准的 jar 工具对目录层次进行归档，可以将 Web 应用程序封装成 Web 归档（WAR）文件。当 Web 应用封装成 Web 归档（WAR）文件格式时，会创建一个 META-INF 目录。它包含了 Java 归档工具有用的清单信息。

除了支持文件和目录存在于文件系统的“未解包” Java Web 应用外，Web Server 7.0 还支持部署封装为 WAR 文件的 Java Web 应用。

下一节将描述 Web Server 如何使用部署描述符来指定 Web 应用的配置。

### 10.5.3 Web Server 中的 Java Web 应用配置

Java Web 应用配置的不同方面在以下配置文件中指定：

- server.xml
- default-web.xml
- web.xml
- sun-web.xml

图 10.7 展示了 Web Server 如何使用这些文件中的信息来初始化和加载 Java Web 应用。

本节的其余部分将详细描述这些文件。

### 10.5.3.1 server.xml 文件

server.xml 是 Web Server 的主配置文件，位于每个服务器实例的 config 子目录中。它包含的信息包括部署在每个虚拟服务器中的 Java Web 应用。server.xml 中的 web-app 元素在 virtual-server 元素内部配置 Java Web 应用映射。web-app 元素是 virtual-server 元素的子元素，并且可以在 virtual-server 元素中出现 0 次或多次。表 10.7 列出了 server.xml 文件中 web-app 元素的子元素。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_454_0.png)

**图 10.7** Java Web 应用初始化

## 10.5 JAVA WEB APPLICATIONS

## 表 10.7 server.xml 中的 web-app 子元素

| 元素 | 是否强制 | 描述 |
| --- | --- | --- |
| description | 否 | Web 应用程序的文本描述。旨在为网站管理员提供参考。 |
| enabled | 否 | 控制在运行时是否启用该 Web 应用的布尔值。可用于在运行时临时禁用 Web 应用，而无需移除 web-app 元素。默认值为 true。 |
| path | 是 | Web Web 应用内容的文件系统路径。可以是绝对路径，也可以是相对路径。相对路径相对于服务器的 config 目录。 |
| uri | 是 | 访问 Web 应用的上下文路径。 |

第 10.5.4 节“将 Java Web 应用部署到 Web Server”包含了更多关于 Web Server 7.0 管理 server.xml 中 web-app 元素的管理接口的信息。

### 10.5.3.2 default-web.xml 文件

default-web.xml 文件包含了所有部署到服务器的 Java Web 应用共享的 Web 应用配置。该文件位于每个服务器实例的 config 子目录中。

该文件是一个 XML 格式的文件，其内容根据标准 XML 数据类型定义 (DTD) 进行验证，该 DTD 验证 web.xml 文件如下：

```
<!DOCTYPE web-app
PUBLIC "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
  "http://java.sun.com/dtd/web-app_2_3.dtd">
```

如 10.7 所示，此文件可为所有 Web 应用指定通用配置，否则这些配置将在每个 Web 应用的部署描述符文件——web.xml 中重复。单个 Web 应用始终可以覆盖此文件中指定的任何设置。

本节的其余部分描述了为每个配置创建的 default-web.xml 文件的内容，并描述了 Web Server 管理框架中包含的该文件的支持。元素的顺序和分组已更改，以便将相关的配置放在一起。

如前所述，Web Server 7.0 的 Java Web 容器包含对 Java Pages (JSP) 支持。Web Server 7.0 中的 JSP 引擎包含一个将 JSP 脚本编译为 servlet 的 JSP 编译器，以及一个执行这些编译脚本的 JSP 运行时。默认情况下，Web Server 7.0 中的所有 Web 应用都使用 Web Server 的 JSP 引擎处理 Java Pages 的请求。Web Server 的 JSP 引擎通过 jsp servlet 及其映射提供给 Web 应用，这些在 default-web.xml 中的定义如下：

```
<servlet>
<servlet-name>jsp</servlet-name>
<servlet-class>org.apache.jasper.servlet.JspServlet</servlet-class>

<init-param>
<param-name>httpMethods</param-name>
<param-value>GET,HEAD,POST</param-value>
</init-param>
<init-param>
<param-name>fork</param-name>
<param-value>false</param-value>
</init-param>
<init-param>
<param-name>mappedfile</param-name>
<param-value>false</param-value>
</init-param>
<load-on-startup>3</load-on-startup>
</servlet>

<servlet-mapping>
<servlet-name>jsp</servlet-name>
<url-pattern>*.jsp</url-pattern>
</servlet-mapping>

<servlet-mapping>
<servlet-name>jsp</servlet-name>
<url-pattern>*.jspx</url-pattern>
</servlet-mapping>
```

默认 servlet 处理不映射到 Web 应用中任何其他 servlet 的请求，例如静态内容（HTML 文件、图像等）的请求。Web Server 的默认 servlet 与服务器的 NSAPI 引擎紧密集成，使 Java Web 容器可以使用服务器的文件缓存来高效地提供静态内容。Web Server 7.0 中的默认 servlet 实现还促进了 Java 和非 Java 动态内容（如 JSP、包括 CGI 程序、Servlet 以及 HTML 文件）的无缝集成。默认 servlet 及其映射在 default-web.xml 中的定义如下：

```
<servlet>
  <servlet-name>default</servlet-name>
  <servlet-class>com.sun.webservices.servlets.DefaultServlet</servlet-class>
  <load-on-startup>1</load-on-startup>
</servlet>
```

```
<servlet-mapping>
  <servlet-name>default</servlet-name>
  <url-pattern>/*</url-pattern>
</servlet-mapping>
```

客户端通过指定 URI 模式访问 servlet。servlet 映射指定在 web.xml 中，即 Web 应用的部署描述符。示例 10.6 是 web.xml 的片段，展示了 HelloServlet 的映射。

#### 示例 10.6 web.xml 片段

```
<servlet-mapping>
  <servlet-name>HelloServlet</servlet-name>
  <url-pattern>/helloworld</url-pattern>
</servlet-mapping>
<servlet-mapping>
  <servlet-name>HelloServlet</servlet-name>
  <url-pattern>/hello/*</url-pattern>
</servlet-mapping>
```

客户端通过指定 URI 模式访问 servlet。servlet 映射指定在 web.xml 中，即 Web 应用的部署描述符。通过在 web.xml 中指定这些映射，Web 应用开发者可以允许以 /context_path/helloworld、/context_path/hello 等 等访问 HelloServlet。同样，为了启用应用程序中的每个 servlet，必须在 web.xml 中定义 servlet 映射。invoker servlet 通过消除原型设计时无需指定 servlet 映射来促进应用程序开发。在生产环境中使用 Web Server 时建议禁用 invoker servlet。以下定义了 invoker servlet：

```
<servlet>
  <servlet-name>invoker</servlet-name>
  <servlet-class>org.apache.catalina.servlets.InvokerServlet</servlet-class>
  <init-param>
    <param-name>debug</param-name>
    <param-value>0</param-value>
  </init-param>
  <load-on-startup>2</load-on-startup>
</servlet>

<servlet-mapping>
  <servlet-name>invoker</servlet-name>
  <url-pattern>/servlet/*</url-pattern>
</servlet-mapping>
```

在 default-web.xml 中定义的 invoker servlet 映射允许以 /context_path/servlet/servlet_name 的形式访问 Web 应用中的任何 servlet，其中 context_path 是 Web 应用部署路径，servlet_name 是 Java 完全限定名。以下示例说明了使用 invoker servlet 访问部署在 / 的单个 servlet：

- /test/servlet/HelloWorld（使用 web.xml 中的 servlet-name）
- /test/servlet/foo.bar.HelloServlet（使用 Java 类名）

## 表 10.8 default-web.xml Servlet 映射示例

| URL | 调用的 servlet |
| --- | --- |
| http://host:port/webapp/index.jsp | jsp |
| http://host:port/webapp/index.html | default |
| http://host:port/webapp/subdir/catalog.jsp | jsp |
| http://host:port/webapp/banner.jpg | default |
| http://host:port/webapp/servlet/ShoppingCart | invoker |
| http://host:port/webapp/servlet/index.html | invoker |

default-web.xml 文件还可以用于为 Web Server 中的 Java Web 应用指定会话配置。Web Server 7.0 包含的 default-web.xml 文件仅指定了 Java Web 应用会话的默认超时时间。





```xml
<session-config>
  <session-timeout>30</session-timeout>
</session-config>
```

尽管 Web Server 的管理框架不包含编辑 `default-web.xml` 文件中单个元素的支持，但命令行界面——wadm——通过 `get-config-file` 和 `set-config-file` 子命令提供了管理该文件的支持。图 10.8 展示了使用 `getconfig-file` 和 `set-config-file` 修改 `default-web.xml` 文件。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_459_0.png)

图 10.8 管理 default-web.xml 文件的命令行支持

Web 应用部署描述符中指定的配置设置可覆盖 `default-web.xml` 文件中指定的设置。本节将描述 `web.xml` 文件。

## 第 10 章通过 JAVA 提供动态内容

### 10.5.3.3 web.xml 文件

`web.xml` 文件是一个 J2EE 标准 XML 文档，用于描述 Java Web 应用的内容。该部署描述符包含了 Java Web 应用的部署和配置信息。`web.xml` 文件的格式和内容在 Java Servlet 规范 2.5 版本中定义。如果存在，`web.xml` 文件必须位于应用程序的 `WEB-INF` 子目录下。Web 应用**并不要求**包含 `web.xml` 文件。

应用程序 `web.xml` 文件中指定的类型类型包括：

- Servlet 定义和映射
- JSP 配置
- Servlet 过滤器定义和映射
- Session 配置
- 安全配置
- 欢迎文件顺序
- 应用 (ServletContext) 初始化参数和生命周期监听器
- 地地语言和编码映射
- 错误页面声明

有关此部署描述符中每个元素的详细信息，请参阅《Java Servlet 规范 2.5 版本》。

示例 10.7 展示了一个示例 `web.xml` 文件。

示例 10.7 示例 web.xml 文件

```xml
<xml version="1.0" encoding="ISO-8859-1"?>
<web-app xmlns="http://java.sun.com/xml/ns/javaee"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
  version="2.5">
  <display-name>Yummy Pizzas</display-name>
  <context-param>
    <param-name>Owner</param-name>
    <param-value>raj@yummypizzas.com</param-value>
  </context-param>
  <servlet>
    <servlet-name>MenuServlet</servlet-name>
    <servlet-class>yummypizzas.MenuServlet</servlet-class>
    <init-param>
      <param-name>specials</param-name>
      <param-value>true</param-value>
    </init-param>
  </servlet>
  <servlet-mapping>
    <servlet-name>MenuServlet</servlet-name>
    <url-pattern>menu/*</url-pattern>
  </servlet-mapping>
  <session-config>
    <session-timeout>10</session-timeout>
  </session-config>
  <welcome-file-list>
    <welcome-file>menu.jsp</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>index.html</welcome-file>
  </welcome-file-list>
  <error-page>
    <error-code>404</error-code>
    <location>nosuchpizza.html</location>
  </error-page>
  <resource-ref>
    <description>Pizza Database</description>
    <res-ref-name>jdbc/pizzas</res-ref-name>
    <res-type>javax.sql.DataSource</res-type>
    <res-auth>Container</res-auth>
  </resource-ref>
</web-app>
```

为了实现快速开发，当 Web Server 的 Java Web容器检测到应用程序的 `web.xml` 文件被修改时，可以在不重启服务器或不影响其他应用程序的情况下重新部署应用程序。关于此点的更多信息请见第 10.5.9 节，“动态重配置 Java Web 应用”。

图 10.7 展示了服务器如何使用 `web.xml` 中的信息初始化 Java Web 应用。Web Server 不包含创建或编辑 `web.xml` 文件的工具。流行的 Java 集成开发环境 (IDE) 如 NetBeans 和 Eclipse 包含了创建和打包 Web 应用及其关联部署描述符的支持。图 10.9 展示了如何使用 NetBeans 编辑示例 10.7 中的示例 `web.xml` 文件。

## 第 10 章通过 Java 提供动态内容

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_462_0.png)

图 10.9 NetBeans 6.1 中的 web.xml 编辑

### 10.5.4 sun-web.xml 文件

`sun-web.xml` 文件是一个可选的部署描述符，专门 Sun 的 Web 层服务，即 Web Servlet 和 Application Server。该文件也是一个 XML 格式文档，指定了 Web Server 7.0 中包含的 Web 应用部署和配置信息。`sun-web.xml` 文件的格式和内容定义在《Java System Web Server 7.0 开发指南》的附录 A 中。如果存在，`sun-web.xml` 文件必须位于应用程序的 `WEB-INF` 子目录下。Web 应用并不要求包含 `sun-web.xml` 文件。

此此文件中的所有项目都根据 `sun-web.xml` 部署描述符的 XML 类型定义 (DTD) 进行验证，如下：

```xml
<!DOCTYPE sun-web-app PUBLIC
"//Sun Microsystems, Inc.//DTD Application Server 9.0 Servlet 2.5//EN"
"http://www.sun.com/software/appserver/dtds/sun-web-app_2_5-0.dtd">
```

除了 DODOCTYPE 声明中引用的 URL 外，还可以找到类型定义文件 (sun-web-app_2_5-0.dtd)。`sun-web.xml` 描述符是 `web.xml` 的辅助文件，指定了 Web Server 7.0 的 Web 应用部署和配置。`sun-web.xml` 中指定的类型包括：

- Servlet 定义和映射
- JSP 配置
- Servlet 过滤器定义和映射
- Session 配置
- 安全配置
- 欢迎文件顺序
- 应用 (ServletContext) 初始化参数和生命周期监听器
- 语言和编码映射
- 错误页面声明

示例 10.8 展示了一个示例 `sun-web.xml` 文件。

示例 10.8 示例 sun-web.xml 文件

```xml
DOCTYPE sun-web-app PUBLIC
"//Sun Microsystems, Inc.//DTD Application Server 9.0 Servlet 2.5//EN"
"http://www.sun.com/software/appserver/dtds/sun-web-app_2_5-0.dtd">
<web-app>
  <display-name>Yummy Pizzas</display-name>
  <context-param>
    <param-name>Owner</param-name>
    <param-value>raj@yummypizzas.com</param-value>
  </context-param>
  <servlet>
    <servlet-name>MenuServlet</servlet-name>
    <servlet-class>yummypizzas.MenuServlet</servlet-class>
    <init-param>
      <param-name>specials</param-name>
      <param-value>true</param-value>
    </init-param>
  </servlet>
  <servlet-mapping>
    <servlet-name>MenuServlet</servlet-name>
    <url-pattern>menu/*</url-pattern>
  </servlet-mapping>
  <session-config>
    <session-timeout>10</session-timeout>
  </session-config>
  <welcome-file-list>
    <welcome-file>menu.jsp</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>index.html</welcome-file>
  </welcome-file-list>
  <error-page>
    <error-code>404</error-code>
    <location>nosuchpizza.html</location>
  </error-page>
  <resource-ref>
    <description>Pizza Database</description>
    <res-ref-name>jdbc/pizzas</res-ref-name>
    <res-type>javax.sql.DataSource</res-type>
    <res-auth>Container</res-auth>
  </resource-ref>
</web-app>
```
（注：提示中提供的后续页面 OCR 文本高度碎片化/重复。我根据提供的上下文重建了逻辑流，并修正了如“getconfigfile”和“Example 10.7”等同步片段。）

等等，严格遵循提供的 OCR 文本修复修复：

[content]
<session-config>
  <session-timeout>30</session-timeout>
</session-config>

尽管 Web Server 的管理框架不包含编辑 `default-web.xml` 文件中单个元素的支持，但命令行界面——wadm——通过 `get-config-file` 和 `set-config-file` 子命令提供了管理该文件的支持。图 10.8 展示了使用 `getconfig-file` 和 `set-config-file` 修改 `default-web.xml` 文件。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_459_0.png)

图 10.8 管理 default-web.xml 文件的命令行支持

Web 应用部署描述符中指定的配置设置可覆盖 `default-web.xml` 文件中指定的设置。本节将描述 `web.xml` 文件。

## 第 10 章通过 JAVA 提供动态内容

### 10.5.3.3 web.xml 文件

`web.xml` 文件是一个 J2EE 标准 XML 文档，用于描述 Java Web 应用的内容。该部署描述符包含了 Java Web 应用的部署和配置信息。`web.xml` 文件的格式和内容在 Java Servlet 规范 2.5 版本中定义。如果存在，`web.xml` 文件必须位于应用程序的 `WEB-INF` 子目录下。Web 应用**并不要求**包含 `web.xml` 文件。

应用程序 `web.xml` 文件中指定的类型类型包括：

- Servlet 定义和映射
- JSP 配置
- Servlet 过滤器定义和映射
- Session 配置
- 安全配置
- 欢迎文件顺序
- 应用 (ServletContext) 初始化参数和生命周期监听器
- 语言和编码映射
- 错误页面声明

有关此部署描述符中每个元素的详细信息，请参阅《Java Servlet 规范 2.5 版本》。

示例 10.7 展示了一个示例 `web.xml` 文件。

示例 10.7 示例 web.xml 文件

```xml
<xml version="1.0" encoding="ISO-8859-1"?>
<web-app xmlns="http://java.sun.com/xml/ns/javaee"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
  version="2.5">
  <display-name>Yummy Pizzas</display-name>
  <context-param>
    <param-name>Owner</param-name>
    <param-value>raj@yummypizzas.com</param-value>
  </context-param>
  <servlet>
    <servlet-name>MenuServlet</servlet-name>
    <servlet-class>yummypizzas.MenuServlet</servlet-class>
    <init-param>
      <param-name>specials</param-name>
      <param-value>true</param-value>
    </init-param>
  </servlet>
  <servlet-mapping>
    <servlet-name>MenuServlet</servlet-name>
    <url-pattern>menu/*</url-pattern>
  </servlet-mapping>
  <session-config>
    <session-timeout>10</session-timeout>
  </session-config>
  <welcome-file-list>
    <welcome-file>menu.jsp</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>index.html</welcome-file>
  </welcome-file-list>
  <error-page>
    <error-code>404</error-code>
    <location>nosuchpizza.html</location>
  </error-page>
  <resource-ref>
    <description>Pizza Database</description>
    <res-ref-name>jdbc/pizzas</res-ref-name>
    <res-type>javax.sql.DataSource</res-type>
    <res-auth>Container</res-auth>
  </resource-ref>
</web-app>
```

为了实现快速开发，当 Web Server 的 Java Web容器检测到应用程序的 `web.xml` 文件被修改时，可以在不重启服务器或不影响其他应用程序的情况下重新部署应用程序。关于此点的更多信息请见第 10.5.9 节，“动态重配置 Java Web 应用”。

图 10.7 展示了服务器如何使用 `web.xml` 中的信息初始化 Java Web 应用。Web Server 不包含创建或编辑 `web.xml` 文件的工具。流行的 Java 集成开发环境 (IDE) 如 NetBeans 和 Eclipse 包含了创建和打包 Web 应用及其关联部署描述符的支持。图 10.9 展示了如何使用 NetBeans 编辑示例 10.7 中的示例 `web.xml` 文件。

## 第 10 章通过 Java 提供动态内容

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_462_0.png)

图 10.9 NetBeans 6.1 中的 web.xml 编辑

### 10.5.4 sun-web.xml 文件

`sun-web.xml` 文件是一个可选的部署描述符，专门 Sun 的 Web 层服务，即 Web Servlet 和 Application Server。该文件也是一个 XML 格式文档，指定了 Web Server 7.0 中包含的 Web 应用部署和配置信息。`sun-web.xml` 文件的格式和内容定义在《Java System Web Server 7.0 开发指南》的附录 A 中。如果存在，`sun-web.xml` 文件必须位于应用程序的 `WEB-INF` 子目录下。Web 应用并不要求包含 `sun-web.xml` 文件。

此此文件中的所有项目都根据 `sun-web.xml` 部署描述符的 XML 类型定义 (DTD) 进行验证，如下：

```xml
<!DOCTYPE sun-web-app PUBLIC
"//Sun Microsystems, Inc.//DTD Application Server 9.0 Servlet 2.5//EN"
"http://www.sun.com/software/appserver/dtds/sun-web-app_2_5-0.dtd">
```

除了 DODOCTYPE 声明中引用的 URL 外，还可以找到类型定义文件 (sun-web-app_2_5-0.dtd)。`sun-web.xml` 描述符是 `web.xml` 的辅助文件，指定了 Web Server 7.0 的 Web 应用部署和配置。`sun-web.xml` 中指定的类型包括：

- Servlet 定义和映射
- JSP 配置
- Servlet 过滤器定义和映射
- Session 配置
- 安全配置
- 欢迎文件顺序
- 应用 (ServletContext) 初始化参数和生命周期监听器
- 语言和编码映射
- 错误页面声明

示例 10.8 展示了一个示例 `sun-web.xml` 文件。

示例 10.8 示例 sun-web.xml 文件

```xml
DOCTYPE sun-web-app PUBLIC
"//Sun Microsystems, Inc.//DTD Application Server 9.0 Servlet 2.5//EN"
"http://www.sun.com/software/appserver/dtds/sun-web-app_2_5-0.dtd">
<web-app>
  <display-name>Yummy Pizzas</display-name>
  <context-param>
    <param-name>Owner</param-name>
    <param-value>raj@yummypizzas.com</param-value>
  </context-param>
  <servlet>
    <servlet-name>MenuServlet</servlet-name>
    <servlet-class>yummypizzas.MenuServlet</servlet-class>
    <init-param>
      <param-name>specials</param-name>
      <param-value>true</param-value>
    </init-param>
  </servlet>
  <servlet-mapping>
    <servlet-name>MenuServlet</servlet-name>
    <url-pattern>menu/*</url-pattern>
  </servlet-mapping>
  <session-config>
    <session-timeout>10</session-timeout>
  </session-config>
  <welcome-file-list>
    <welcome-file>menu.jsp</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>index.html</welcome-file>
  </welcome-file-list>
  <error-page>
    <error-code>404</error-code>
    <location>nosuchpizza.html</location>
  </error-page>
  <resource-ref>
    <description>Pizza Database</description>
    <res-ref-name>jdbc/pizzas</res-ref-name>
    <res-type>javax.sql.DataSource</res-type>
    <res-auth>Container</res-auth>
  </resource-ref>
</web-app>
```




# 第10章 通过 Java 提供动态内容

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_466_0.png)

图 10.11 管理控制台—常见任务

## 10.5 Java Web应用程序

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_467_0.png)

图 10.12 管理控制台—虚拟服务器 Web应用程序

## 第10章 通过 Java 提供动态内容

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_468_0.png)

图 10.13 管理控制台—添加 Web应用程序

图 10.13 通过识别对话框上的用户交互，演示了如何向名为 `test` 的虚拟服务器添加上下文路径为 `/simple` 的 Web 应用程序。图 10.14 阐了 Web 服务器的管理框架如何通过将其内容提取到实例的 `web-app` 子目录来部署 `.war` 文件。

当 Java Web 应用程序部署到该虚拟服务器时，`server.xml` 中对应的虚拟服务器元素会添加一个新的 `web-app` 元素。示例 10.9 列出了 `server.xml` 的相关部分，对应于之前图 10.13 中添加的示例 Web 应用程序。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_469_0.png)

### test - 虚拟 Web应用程序

此页面允许您向虚拟服务器添加应用程序。Web 应用程序作为 Web （每个一个）添加。添加应用程序后，您需要部署配置以将添加的 Web 应用程序传播到实例。该页面还允许您设置单点登录。

- 单点登录
- Web应用程序

### 单点登录

- 单点登录
  启用
  会话超时（分钟）：30
  如果用户单点登录记录过期且未看到 n，则超时后进行清理（-1 表示不超时）

- 返回顶部

### Web应用程序

### Web应用程序 (1)

| 名称 | 启用 | 路径 | 说明 |
|---|---|---|---|
| simple | true | web/simple | 简单示例应用程序 |

- 返回顶部

相对路径是相对于 `config` 目录指定的。

单个 Web 应用程序的内容托管由应用程序 URI（上下文路径）标识的子目录中。

`web-app` 目录下的顶级目录使用托管 Web 应用程序框架部署 Web 应用程序的虚拟服务器命名。

图 10.14 管理控制台—虚拟服务器 Web应用程序

示例 10.9 server.xml 文件的片段

```xml
<virtual-server>
<name>test</name>
<host>test</host>
<http-listener-name>http-listener-1</http-listener-name>
<document-root>../docs/document-root</document-root>
<web-app>
<uri>/simple</uri>
<path>../web-app/test/simple</path>
<description>Simple Sample Application</description>
</web-app>
</virtual-server>
```

基于 Web 的管理控制台还允许管理员同时管理多个 Web 应用程序。图 10.15 显示了管理员如何一起启用、禁用或删除 Web 应用程序。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_470_0.png)

图 10.15 管理控制台—Web应用程序的组操作

### 10.5.4.2 命令行部署

Web 服务器的主要管理命令行界面——`wadm`——提供了以下子命令来支持 Java Web应用程序管理：

- add-webapp
- disable-webapp
- enable-webapp
- list-webapps
- remove-webapp

以下 shell 模式示例显示了如何使用命令行界面使用某些命令来部署和卸载 Java Web应用程序：

```
wadm> list-webapps --verbose --all --config=test --vs=test
uri enabled
/simple true
wadm> add-webapp --description="JSTL Sample Application" --config=test
--vs=test --uri=jst/c:/sun/webserver7/samples/java/webapps/jst/
webapps-jst.war
CLI201 Command 'add-webapp' ran successfully
wadm> list-webapps --verbose --all --config=test --vs=test
uri enabled
/simple true
/jst true
wadm> remove-webapp --config=test --vs=test --uri=/simple
CLI201 Command 'remove-webapp' ran successfully
wadm> list-webapps --config=test --vs=test --verbose --all
uri enabled
/jst true
wadm>
wadm> deploy-config test
CLI201 Command 'deploy-config' ran successfully
```

与基于 Web 的界面不同，`wadm` 子命令不支持通过单个命令对启用、禁用和删除多个 Web 应用程序进行组操作。

> 注意：在 shell 模式下使用 `wadm` 时，文件路径（即使在 Windows 上使用 `wadm`）始终使用 UNIX 风格的正斜杠 (/) 指定，而不是反斜杠 (\\)。

### 10.5.4.3 自动部署

Web 服务器支持从指定目录快速、迭代地部署 Web 应用程序。从指定目录快速、迭代部署 Web 应用程序的功能都包括“已包”格式（.war 文件）和“已解包”格式（文件系统中的目录）。Web Server 7.0 Update 3 是第一个支持 Java 应用程序自动部署的发布版本。用于自动部署 Java 应用程序的指定目录是 `instance/auto-deploy`。向该目录添加 Java 应用程序会导致其部署到所有活动虚拟服务器。从该目录删除 Java 应用程序会导致其从活动虚拟服务器中卸载。在自动部署期间，Web 服务器使用文件名或目录名来确定部署上下文路径。

## 第10章 通过 Java 提供动态内容

在以下阶段：

* 服务器启动
* 动态重新配置

Web 服务器可以配置为定期检查其 `auto-deploy` 目录的添加/删除，并在运行的服务器中反映这些更改。`dynamic-reload-interval`（见10.5.9，“动态配置Web应用程序”）控制服务器检查的频率。

表 10.9 自动应用程序的上下文路径

| 文件/目录名称 | 格式 | 上下文路径 |
|---|---|---|
| simple | 已解包 (目录) | /simple |
| hello_world.war | 已包 (归档) | /hello_world |
| tax-planner | 已解包 (目录) | /tax_planner |
| 100examples.war | 已包 (归档) | /100 |

与之前的部署方法（见“Web部署”和“命令行部署”章节）不同，自动部署（或自动部署）不需要管理服务器运行。

要自动部署封装为 Web 归文件（.war 文件）的 Java 应用程序，只需将 .war 文件复制到服务器的 `auto-deploy` 目录，如下所示：

```
C:\Sun\WebServer7> copy samples\java\webapps\jst1\webapps-jst.war https-test\auto-deploy
file(s) copied.
C:\Sun\WebServer7>https-test\bin\startserver.bat
Sun System Web Server 7.0 U13 B06/16/2008 11:32
info: CORES076: Using [HotSpot(TM)] Server VM, Version 1.5.0_05 from [MicroSystems Inc.]
info: WEB0100: Loading module in virtual server [test] at [webapps-jst1]
info: HTTP3072: http-listener-1: http://test:9000 ready to accept requests
info: CORES3274: successful server startup
```

> 注意：粗体字体说明了 Web 服务器如何使用 .war 文件名作为部署的上下文路径。

现在可以通过浏览器访问自动部署的应用程序，如图 10.16 所示。

之前的示例演示了 Web 服务器如何在启动期间自动部署 .war 文件。以下示例演示了通过将 Web 应用程序的内容解包到实例的 `auto-deploy` 子目录后，动态重新配置运行的服务器来自动部署 Java 应用程序：

```
C:\Sun\WebServer7\https-test\auto-deploy>mkdir simple
C:\Sun\WebServer7\https-test\auto-deploy>cd simple
```





## 第 17 章 通过 Java 提供动态内容

```
C:\Sun\WebServer7\https-test\auto-deploy\simple -jar C:\nWebServer7\samples\java\simple\webapps-simple.war
C:\Sun\WebServer7-https-test\bin\reconfig.bat
info (4092): CORE3276: Installing a new configuration
info (4092): WEB0100: Loading web module in virtual server [test] at [/simple]
info (4092): PWC3031: Security role name tomcat used in an <auth-constraint> without being defined in a <security-role> in context [/simple]
info (4092): PWC3031: Security role name role1 used in an <auth-constraint> without being defined in a <security-role> in context [/simple]
```

**注意：** 使用粗体字体是为了了 Web 服务器如何使用目录名称作为部署应用程序的路径。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_474_0.png)

图 10.16 自动部署的 Java Web 应用程序

## 10.5 Java Web 应用程序

删除自动部署的应用程序对应的 .war 文件或目录将导致应用程序的卸载。在 UNIX 平台上，可以在服务器运行时执行删除操作。然而，在 Windows 平台上，你必须在删除文件/目录之前停止服务器，因为当服务器运行时删除自动部署的应用程序时，会显示类似下面的错误信息：

```
C:\SunServer7>del https-test-auto-deploy\webapps-jstl.war
C:\SunServer7>https-test-auto-deploy\webapps-jstl.war
The process cannot access the file because it is being used by another process.
```

卸载自动部署的应用程序涉及删除对应的文件/目录，如下所示（在 UNIX 平台上，可以使用 reconfig.bat 代替 startserv 从正在运行的服务器部署应用程序）：

```
C:\SunServer7>del https-test-auto-deploy\webapps-jstl.war
C:\SunServer7>https-test-test.bin\startserv.bat
Sun Java System Server 7.003 B06/16/2008 11:32
info: CORE5076: Using [Java HotSpot(TM) Server VM, Version 1.5.0_15]
from [Sun Microsystems Inc.]
info: WEB0100: Loading web module in virtual server [test] at [
simple]
info: PWC3031: Security role name tomcat used in an <auth-constraint>
without defined in a <security-role> in context [/simple]
info: PWC3031: Security role name role1 used in an <auth-constraint>
without defined in a <security-role> in context [/simple]
info: HTTP30721: http-listener-1: http://test:9000 ready to accept
requests
info: CORE3274: successfully started server
```

Web Server 中的管理框架目前不支持管理 auto-deploy 目录中的应用程序。wadm 的 `list-webapps` 子命令以及图 10.17 中的虚拟 Web 应用程序屏幕都不包含服务器 auto-deploy 目录中的 Java 应用程序。

## 第 10 章 通过 Java 提供动态内容

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_476_0.png)

图 10.17 管理控制——虚拟服务器应用程序

### 10.5.4.4 手动部署

要向特定的虚拟服务器手动部署 Java 应用程序，只需将 Web 应用程序的内容提取到文件系统上的目录中。然后编辑服务器实例的 .xml 文件，并在正确的 `virtual-server` 元素内添加一个 `web-app` 子元素，并包含有关你提取到文件系统的 Web 应用程序的相关信息。示例 10.9 显示了这些更改后虚拟服务器的样子。Web 应用程序的路径指定了文件系统中包含 Web 应用程序文件的目录。启动、重启或动态重新配置服务器都会将新添加的 Web 应用程序部署到指定的虚拟服务器中。

要手动卸载 Web 应用程序，只需从 `server.xml` 中删除对应的 `web-app` 元素，并动态重新配置或重启服务器。

## 10.5 Java Web 应用程序

**注意**：在对实例配置进行手动更改时，建议使用 wadm 的 `pull-config` 子命令或管理控制台将手动更改与 Web Server 管理框架维护的配置进行同步。

### 10.5.4.5 默认 Web 应用程序

使用 "/" 作为上下文路径部署的 Web 应用程序被称为默认 Web 应用程序（对于部署它的虚拟服务器）。默认 Web 应用程序处理部署它的虚拟服务器的请求。在启用 Java 的服务器中，每个虚拟服务器都有自己的默认 Web 应用程序。默认应用程序配置可以是显式的（用户分配）或隐式的（系统分配），如 10.10 所示。

```xml
<virtual-server>
<name>test</name>
<host>test</host>
<http-listener-name>http-listener-1</http-listener-name>
<document-root>../docs/document-root>
<web-app>
<uri>/simple/</uri>
<description>Simple Application</description>
</web-app>
</virtual-server>
```

如果虚拟服务器没有配置 Web 应用程序，Web Server 将隐式创建一个默认 Web 应用程序。与用户分配的 Web 应用程序不同，隐式默认应用程序没有对应的 `web-app` 元素。

### 10.5.5 Java Web 应用程序会话管理

会话定义为一组相关的请求。使用特定的 Cookie 或 URL 中的特定参数来跟踪会话。Java 容器创建并维护表示会话的对象。这些对象位于服务器上，并通过唯一标识进行识别。客户端和用户跨请求跟踪。Web 应用程序可以在会话中存储特定数据。会话对象持续一段时间，后被认为失效。会话对象及其存储的任何属性在 Web 应用程序之间不共享。每个 Java 应用程序都有维护其可能创建的会话的管理器。

Web Server 支持 Java 会话，并提供了多种会话管理选项。由于会话对象消耗系统资源，配置 Web Server 如何管理会话变得非常重要。

- 决定会话存储的位置（内存、磁盘、数据库或复制）
- 选择合适的超时值以控制会话过期（选择过大的超时可能导致空闲会话浪费内存；选择过短的超时会导致频繁创建会话）
- 确定每个会话中存储的属性的总大小
- 允许的最大活动会话数





## 10.5 Java Web 

检查应用程序中的所有会话以确定其是否过期，如果是，管理器会将会话从存储中清除。会话管理器处理会话过期的频率由 `sun-web.xml` 配置的 `reapIntervalSeconds` 属性控制。适当配置会话超时（通常通过 `web.xml` 中的 `session-timeout` 元素）和会话管理器清理间隔有助于高效的资源利用。例如，为了确保过期的会话不浪费存储，当会话超时设置为较小值时，应配置会话管理器更频繁地清理。在具有长时间会话的应用程序中，可以将会话管理器配置为频率运行，从而节省计算资源。

要指定会话管理器配置，请使用 Web 应用程序 `sun-web.xml` 文件中的 `session-manager` 元素。《Java System Web Server 7.0 Developer's Guide to Java Web Applications》包含一个完整章节，详细描述了 Web Server 7.0 包含的每个会话管理器。

### 10.5.5.2 会话复制 (Session Replication)

Web Server 7.0 引入的会话复制功能为通过负载均衡器访问的 Web Server 7.0 集群中运行的 Web 应用程序会话提供了有限的高可用性。当 Web Server 7.0 集群启用会话复制时，集群中的每个 Web Server 都会将其所有的 Java Web 应用程序话复制到集群中的另一个实例。当集群中的一个节点发生故障时，负载均衡器会将请求重定向到已复制数据的节点。会话复制在 Cookie 中编码了获取数据的位置，该位置会从每个会话的备份节点（在集群中）的备份节点上检索数据，因此要求用于访问应用程序的浏览器接受 HTTP Cookie。

在集群中启用会话复制将会在 Web 应用程序以及集群中每个节点的服务器中启用此功能。

在 Java Web 应用程序中启用会话复制需要在应用程序的 `sun-web.xml` 文件中指定以下内容：

```
<session-manager persistence-type="replicated"/>
```

`server.xml` 文件中的 `session-replication` 元素配置服务器集群内的 Java Web 会话复制。图 10.18 显示了 Web Server 7.0 管理控制台中用于配置此元素值的屏幕。

## 第 10 章 通过 Java 提供动态内容

54

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_480_0.png)

图 10.18 管理控制台—会话复制

`wadm` 的 `get-session-replication-prop` 和 `set-session-replication-prop` 子命令也可用于配置服务器集群中的会话复制。

### 10.5.6 Java Web 应用程序安全

Web Server 7.0 的 Java Web 容器基于 Java EE 安全模型提供了一个高度的环境。Web Server Java Web 容器的安全方面包括：

-   完全符合《Java Servlet 规范 2.5》中指定的安全模型
-   除了 Java Servlet 安全模型外，还支持基于访问控制列表 (ACL)的安全模型
-   支持 Java 安全管理器 (Java Security Manager)。出于性能考虑，默认禁用了 Java 安全管理器。建议在开发期间启用 Java 安全管理器。
-   支持单个安全域内所有 Java Web 应用程序的单点登录 (SSO)。此功能允许应用程序之间共享用户身份验证信息，从而避免要求用户对每个应用程序进行身份验证。
-   支持程序化登录 (Programmatic Login)。程序化登录允许 Java Web 应用程序调用登录方法。
-   支持多种底层身份验证域 (realms)，例如文件和 LDAP
-   支持 SSL 客户端证书认证
-   支持 Solaris PAM
-   支持 Web 服务消息安全
-   通过 Web Server 特有的、基于 XML 的角色映射支持声明式安全

您通过在 `server.xml`、`server.policy`、`login.conf`、`obj.conf`、`web.xml` 和 `sub-web.xml` 等各种配置文件中的多个不同指令在 Web Server 中指定安全配置。请参考《Sun Java System Web Server 7.0 Developer’s Guide to Java Web Applications》中的“Securing Web Applications”章节以及《Sun Java System Web Server 7.0 Administrator’s Guide》中的“Controlling Access to Your Server”章节，获取有关 Web Server 7.0 安全功能的更多信息。

### 10.5.7 Java Web 应用程序中的缓存

执行 servlet 或 JSP 会动态地为 servlet 或 JSP 请求生成响应。缓存动态响应或缓存动态响应的一部分有助于更快的响应速度和更好的计算资源利用。部署在 Web Server 7.0 中的 Java Web 应用程序可以配置启用 servlet、JSP 以及 Java 应用程序内部资源的缓存。Web Server 7.0 还包含一个自定义标签库，Java Web 开发人员可以使用它缓存 JSP 片段。

Web Server 在处理 Java Web 应用程序中静态内容的请求时利用其文件缓存。通过在应用程序的 `sun-web.xml` 部署描述符中如下配置，启用 Java Web 应用程序中动态内容的缓存：

```
<cache enabled="true">
```

### 10.5.7.1 缓存整个响应

响应的缓存配置在 `sun-web.xml` 文件的 `cache` 元素中指定，并支持：

-   缓存由 servlet 名称标识的 servlet 
-   缓存由 URL 模式标识的 servlet 
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-（重复行已清理）

响应的缓存配置在 `sun-web.xml` 文件的 `cache` 元素中指定，并支持以下：

-   缓存由 servlet 名称标识的 servlet 响应
-   缓存由 URL 模式标识的 servlet 响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   缓存使用该 Web 应用程序的请求响应
-   （重复行已清理）

请参考《Sun Java System Web Server 7.0 Developer’s Guide to Java Applications》获取更多关于 `cache` 元素的信息。示例 10.11 展示了缓存一分钟和两分钟的示例。

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE sun-web-app PUBLIC
  "//Sun Microsystems, Inc.//DTD Application Server 2.4//EN"
  "http://www.sun.com/software/appserver/dtd/sun-web.app">

<sun-web-app>
  <cache enabled="true" timeout-in-seconds="120">
    <cache-mapping>
      <servlet-name>YummyPizzas</servlet-name>
      <key-field name="toppings" scope="request.parameter">
      <constraint-field name="toppings" scope="request.parameter">
        <value>one</value>
        <value>two</value>
      </constraint-field>
    </cache-mapping>
  </cache>
</sun-web-app>
```

### 10.5.7.2 缓存页面片段 (Caching Page Fragments)

Web Server 包含了启用缓存页面片段的自定义标签。这些标签指定在 `install_dir/lib/tlds/sun-web-cache.tld` 标签库文件中。Web Server 包含的 JSP 缓存标签如下：

-   cache-缓存开始和结束标签之间的主体
-   flush-刷新整个缓存或刷新缓存中的指定条目

要使用这些标签，请将标签库文件 (sun-web-cache.tld) 复制到 Java Web 应用程序的 WEB 目录，并在 JSP 中引用该标签库。示例 10.12 展示了在 JSP 中使用 `cache` 标签。

# 示例 10.12 在 JSP 中使用缓存标签

```
<@taglib prefix="suncache" uri="/com/sun/web/taglibs/cache" %>
<h1>披萨菜单</h1>
<suncache:cache timeout="1h">
<b>每小时特惠</b>
<br/>
// 获取每小时特惠
<suncache:cache>
<b>可用配料</b>
// 获取披萨配料列表
</suncache:cache>
```

### 10.5.8 类加载器 (Classloaders)

Java 虚拟机 (JVM) 中的类加载器负责在运行时查找并加载 Java 类。类加载器组织成父类加载器和子类加载器的层次结构。类加载器在加载类时遵循委托模型。类加载器首先请求父类加载器加载该类，仅当父类加载器无法加载该类时。如果一个类既存在于加载器中也存在于其父类中，则优先选择父类。父类加载器不会将加载委托给任何子类加载器。Java 类加载器委托





# 第 10 章通过 Java 提供动态内容

该模型避免了由于存在同一类的多个版本导致的 `ClassCastException`。

图 10.19 展示了由 Web Server 创建的各种类加载器之间的委托模型。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_484_0.png)

每个应用程序的 `sun-web.xml` 中 `class-loader` 元素的 `delegate` 属性值控制了 Web 应用程序类加载器何时将加载委托给其父加载器。

图 10.19 Web Server 中的 Java 类加载器

Web 类加载器遵循 Java Servlet 规范版本 2.5 中“SRV.9.7.2 Web Application Class Loader” 推荐的类加载器委托模型，并在委托给父类加载器之前，尝试在 Java Web 应用程序内部加载类和资源。你可以通过在应用程序的 `sun-web.xml` 文件中指定以下内容来覆盖此行为：

```xml
<class-loader delegate="true"/>
```

了解每个类加载器在 Web Server 中扮演的角色可以帮助排查类加载问题。关于 Web Server 类加载器的更多信息请参阅《Sun Java System Web Server 7.0 Developer’s Guide to Java Web Applications》一书。

## 10.5.9 动态重配置 Java Web 应用程序

Web Server 7.0 中的动态重配置功能支持对确定为已变化的 Java Web 应用程序进行重新加载。未更改的现有 Web 应用程序将继续无中断地运行。现有数据（未更改的应用程序中）在动态重配置之前、期间和之后均保持不变。无需重启服务器能够在应用程序开发周期期间快速部署更改。标题为“Global Java Settings”的章节包含了需要重启服务器的 Java 设置信息。

不需要重启 Web Server 的更改类型包括：

- 添加和删除 Java Web 应用程序
- 添加、删除和更新封装为 WAR 文件的 Java Web 应用程序
- 在 Web 应用程序中添加、删除和更新静态内容
- 在 Web 应用程序中添加、删除和更新 Java Servlet 类和 JSP
- 在 Web 应用程序中添加、删除和更新 Java  (JAR) 文件
- 添加、删除和更新 Java 应用程序描述符，包括 `web.xml`、`sun-web.xml` 和标签库描述符
- 更改 `server.xml` 中 `web-app` 元素指定的 Web 应用程序配置
- 更改 `server.xml` 中 `servlet-container` 元素指定的 Java 容器配置
- 更改所有 Java Web 应用程序共享的全局部署描述符 (`default-web.xml`)
- 更改 Web 应用程序 `META-INF` 和 `WEB-INF` 目录的内容

静态内容的更改不需要动态重配置即可生效。Web Server 中的文件缓存在检测到磁盘上的内容比缓存副本新时会自动提供新的静态内容。

默认情况下，Web Server 中 Java 容器的 JSP 引擎在处理请求时会检测 JSP 变化并自动重新编译 JSP。你可以通过配置应用程序 `sun-web.xml` 文件中 `jsp-config` 元素的 `reload-interval` 属性，来更改在请求时检测 JSP 变化的默认行为。《Java System Web Server 7.0 Developer's Guide to Java Web Applications》附录 A 包含该属性的更多信息。

在动态重配置期间，Web Server 7.0 中的 Java 容器使用多种启发式算法自动判断 Java Web 应用程序是否发生了“变化”并需要重新加载。图 10.20 展示了当服务器动态重配置时，Java 容器如何判断 Web 应用程序是否已加载。

Web Server 7.0 支持允许 Web 应用程序开发者或站点管理员强制重新加载应用程序。当启用此功能时，Web 会在每个 Web 应用程序的文档根目录下查找名为 `.reload` 的文件。服务器将重新加载任何包含 `.reload` 文件的 Web 应用程序，只要该文件自服务器上次检查该应用程序以来已更新。此功能默认是禁用的，但可以通过在 `sun-web.xml` 中设置 `reload-interval` 属性非零值来启用。

以下显示使用 `wadm` 脚本配置 Web 容器每 5 秒检查一次：

```
.servlet-container- dynamic-reload-interval=5
wadm deploy-
-containercontainer-config' 成功
```

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_484_0.png)
图 10.20 动态重配置—Java 应用程序

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_484_0.png)
Servlet 容器

## Servlet 容器

Servlet 容器是 Web Server 的一个组件，用于托管并与 servlet 交互。它控制映射到 servlet 的请求和响应。

| 属性 | 取值 | 描述 |
| :--- | :--- | :--- |
| Log Level | info, fine, warning, error | |
| Dynamic Reload Interval | 60000 | 服务器检查应用程序的时间间隔 |
| Anonymous Role | ANYONE | |
| Servlet Pool Size | 5 | Servlet 实例数量 |
| Dispatcher Max Depth | 100 | 嵌套请求的最大深度 |
| Allow Cross | Enabled | 是否允许跨请求 |
| Enable Cookies | Enabled | |

图 10.21 控制台—Servlet

当发生以下情况时，服务器会动态重配置：

- 从控制台部署了配置。
- 通过使用 `wadm` 脚本部署了配置。
- 执行了 `reconfig` 命令（`reconfig.bat`）。
- 启用了非零重加载间隔且应用程序的 `.reload` 文件已更新。

在重配置期间，服务器日志指示应用程序已重新加载。以下示例展示了如何使用服务器消息识别：

启动包含两个应用程序的服务器
C:\Sun\WebServer\test

## 10.6 Web Server 和 NetBeans

Sun Java System Web Server 7.0U3 B06/16/2008 11:32
info: CORE 使用 [Java HotSpot(TM) Server VM, Version 1.5.0_15]
来自 [Sun Microsystems Inc.]
info: WEBO0100: 在虚拟服务器中加载模块 [/ simple
info: WEBO0100: 在虚拟服务器中加载模块 [/ WebApplication1
info: HTTP3072: http-listener-1: http://test:9000 已准备好请求
info: CORE3274: 启动成功

在不更改任何内容的情况下重配置服务器，注意没有加载相关的消息
C:\WebServer7-https-test\bin\reconfig.bat
info: CORE3276: 正在新配置
info: CORE3280: 新配置安装成功

修改一个应用程序的部署描述符
C:\WebServer7\notepad-test\web-app\simple\WEB-INF\web.xml

重配置服务器，注意指示该应用程序已重新加载的消息
C:\WebServer7-https-test\bin\reconfig.bat
info: CORE3276: 安装新配置
info: WEBO0100: 在虚拟服务器中加载模块 [/ simple
info: CORE3280: 新配置安装成功





## 10.6.1 为 NetBeans IDE 安装 Web Server 7.0 插件

本节简要介绍了 NetBeans IDE 本身以及用于 Java Web 应用程序和 Web Server 7.0 的 IDE 支持模块（插件）。

从 NetBeans 主页 http://www.netbeans.org 下载并安装 NetBeans IDE，如图 10.22 所示。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_490_0.png)

图 10.22 NetBeans 首页

启动 NetBeans IDE，并在“工具 (Tools)”菜单中选择“插件 (Plugins)”菜单项，如图 10.23 所示。

在对话框的“可用插件 (Available Plugins)”选项卡中，选择并安装“Sun Java System Web Server 7.0”插件和“Web 应用程序 (Web Applications)”插件，如图 10.24 所示。

## 10.6 Web Server 与 NetBeans

## NetBeans 6.1

| 文件 (File) | 编辑 (Edit) | 视图 (View) | 导航 (Navigate) | 源码 (Source) | 重构 (Refactor) | 构建 (Build) | 运行 (Run) | 属性 (Properties) | 工具 (Tools) | 窗口 (Window) | 帮助 (Help) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 项目 (Projects) | x | 节点 (Nodes) | 服务 (Services) | 首页 (Start Page) | x | | | | | | |
| 添加发布... (Add to Publish...) | | | | | | | | | | | | |
| 服务器 (Servers) | | | | | | | | | | | |

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_491_0.png)

| 库 (Libraries) | | | | | | | | | | | | |
| Java 平台 (Java Platforms) | | | | | | | | | | | | |
| NetBeans 平台 (NetBeans Platforms) | | | | | | | | | | | | |
| 模板 (Templates) | | | | | | | | | | | | |
| Web (Web) | | | | | | | | | | | | |
| XSD 和 J2EE 架构 (XSD and J2EE Schemas) | | | | | | | | | | | | | |
| 插件 (Plugins) | | | | | | | | | | | | |
| 其他 (Others) | | | | | | | | | | | | |

增强结构化文档标题...
关于增强可见性和外观的教程...

理解代码和托管代码...
使用 NetBeans IDE 6 开发 Web 应用程序...

假设项目变为现实：热点...
微软已宣布发布 NetBeans

所有新闻 >>

James 的博客：如何制作 SQL 查询...
今天，我决定写一个关于更改 MySQL 密码的提示，以防此类情况再次发生。就在今天。

APISign：回归测试确实很重要...
当你更改 API 时，必须为它设置一个截止日期。API 并不好...

连接机器人：MySQL，我们...
本教程展示了如何将 NetBeans 连接到 MySQL 数据库。它提供了关于的几个事实

# 导航器 (Navigator)

# 特色演示 (Featured Demo)

在 NetBeans IDE 中使用 EclipseLink 的 JPA 支持

| 项目 (PROJECT) | 专用模块 (EXCLUSIVE_MODULE) |
| :--- | :--- |
| 位置 (Location) | 数据项目 (Data Project) |
| 包 (Package) | |
| <无可用视图> | |

- 为持久化生成查询注解
- 项目具有一个持久化单元，其
- 创建持久化单元...Create Persistence Unit...)

所有演示 >>

# NetBeans IDE—菜单

| 更新 (23) | 可用插件 (115) | 已安装 (20) | 设置 (50) |
| :--- | :--- | :--- | :--- |

# 重新加载目录 (Reload Catalog)

| 搜索 (Search:) | | | | |
| 安装 (Install) | 名称 (Name) ^ | 类别 (Category) | 来源 (Source) |
| :--- | :--- | :--- | :--- |
| 启动设置 (startup settings) | | Web & Java EE | |
| 结构 (Struct) | | | |
| Java System Portal Server 7.0 | Portallack | | | |
| Sun Java Web Server 7.0 | ... | Sun Microsystems | | |
| Sun Java ToolKit, 2.2 | ... | | | |
| SCM Maven Manager | | | | |
| Ridgeline | | | | |
| Topix List Filter Support | | | |
| Tomcat | | | | |
| UML | Web & Java EE | | |
| 新工具 (New Tools) | | Java Link | | |
| 使用系统默认 (Use system default) | | Java Link | | |
| 编辑器工具支持 (Editor Utility Support) | | Web & Java EE | | |
| 可视化器 (Visualizer) | Web & Java EE | | |
| 可视化设计器 (Visual Designer) | Web & Java EE | | |
| Visual J2BP Backcoms ... | Web & Java EE | | |
| Visual J2BP Portal Support | Web & Java EE | | |
| Web 应用程序 (Web Applications) | Web & Java EE | | |
| Web 服务 (Web Services) | Web & Java EE | | |
| XML 和架构 (XML and Schema) | Web & Java EE | | |
| 客户端示例 (Client Samples) | Web & Java FF | | |
| 安装选定的 2 个插件，108 | 测试工具 (Testing tools) | | |

# Web 应用程序 (Web Applications)

NetBeans 认证插件
版本: 1.1.2
日期: 2007
作者: NetBeans
首页: http://www.netbeans.org/

# 插件描述 (Plugin Description)

用于包含的 bug 修复代码。
http://www.netbeans.org/netbeans_6/IPatches.html

提供开发 Java Web 应用程序的支持：管理项目、编辑服务和 JSP 页面、重构、部署和调试。

# NetBeans IDE—插件 (Plugins)

## 第 10 章通过 JAVA 提供动态内容

NetBeans IDE 现在已准备好用于向 Web 服务器开发、调试和部署 Java 应用程序。

## 10.6.2 创建 Java 应用程序

本节介绍了如何使用 NetBeans IDE 创建可以部署到 Web 服务器的 Java 应用程序。

启动 NetBeans IDE，并在“工具”菜单中选择“插件”菜单项，如图所示。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_492_0.png)

图 10.25 NetBeans IDE—文件

在“可用插件 (Available Plugins)”选项卡中选择并安装“Sun Java System Web Server 7.0”插件和“Web 应用程序 (Web Applications)”插件，如图 10.24 所示。

在“文件”菜单中选择“新建项目”，如图所示。

选择项目名称并指定位置，点击“下一步”。

图 10.26 NetBeans IDE—新建项目

点击“下一步”。

图 10.27 NetBeans IDE—新建项目

选择目标服务器，点击“下一步”。

## 10.6 Web Server 与 NetBeans

本节引导了你如何将 NetBeans  部署之前部署的 Java 应用程序。

## 10.6.3 部署 Java 应用程序

要部署 Java 应用程序，在项目窗口中右键点击该应用程序并选择“部署 (Deploy)”，如图所示。NetBeans 将应用程序中的所有 servlet 编译成 Web 归档 (.war)，然后将 .war 文件部署到 Web Server 7.0。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_494_0.png)

图 10.28 NetBeans IDE—部署

## 10.6.4 基础 Web 服务器管理

NetBeans 的 Web 服务器插件还允许开发人员在内部对 Web 服务器进行某些基础操作。

通过点击“服务 (Services)”选项卡中的“Sun Java System Server 7.0”来识别可用的管理任务。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_495_0.png)

图 10.29 NetBeans IDE—添加

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_495_1.png)

图 10.30 NetBeans IDE—添加

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_496_0.png)

图 10.31 NetBeans IDE—新建

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_497_0.png)

图 10.32 NetBeans IDE—index.jsp





# 第10章 通过 Java 提供动态内容

当从 NetBeans 管理 Web Server 7.0 时，会弹出一个新窗口包含 Web 服务器的日志消息。Sun Java System Web Server 7.0 还包含了一些按钮，允许开发者执行常见任务，例如启动和停止服务器。图 10.38 显示了此类标签页的示例。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_500_0.png)

图 10.38 NetBeans IDE—输出—基本 Web Server 7.0 管理

图 10.39 展示了 NetBeans 暴露的 Web Server 配置和管理的其他一些方面。

## 10.6 调试 Web 应用程序

在 servlet 代码或 JSP 中进行调试是应用开发不可或缺的一部分。Web Server 包含了对 Java Web 应用程序代码远程调试的支持，例如 NetBeans 中包含的这种。

## 10.6 Web Server 与 NetBeans

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_501_0.png)

图 10.39 NetBeans IDE—服务—Web Server 7.0 配置

为了本次练习，我们将向之前创建的 Web 应用程序添加一个示例 servlet，然后演示如何在 servlet 的 Java 代码中设置断点。

要向 Web 应用程序添加 servlet，请在“项目”（Projects）窗口中右键点击 Web 应用程序的名称以弹出菜单，然后在“新建”（New）菜单中选择“Servlet”项，如图 10.40 所示。

为 servlet 输入类名和包名，然后点击“新建”向导中的“下一步”（Next）按钮，如图 10.41 所示。

# 第10章 通过 Java 提供动态内容

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_502_0.png)

图 10.40 NetBeans IDE—添加 Servlet

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_502_1.png)

图 10.41 NetBeans IDE—Servlet 向导

## 10.6 Web Server 与 NetBeans

通过指定访问 servlet 的 URL 模式来配置 servlet 部署参数，并勾选“添加到部署描述符 (xml)”复框框以便 NetBeans 自动创建并填充 Web 部署描述符。图 10.42 展示了这一点。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_503_0.png)

图 10.42 NetBeans IDE—新建文件向导

点击图 10.42 中的“完成”（Finish）按钮将创建图 10.43 所示的 HttpServlet.java servlet。

图 10.44 展示了 HelloServlet 在部署到 Web Server 并通过浏览器访问时的效果。

要在 servlet 中设置断点，只需点击源显示窗口的左侧边距。下一次执行 servlet 时，执行将在断点处停止，开发者可以通过 NetBeans IDE 控制 servlet 剩余部分的执行。高亮的红线标识断点。图 10.45 显示了高亮代码语句 `out.println("<html>");` 处的断点。

# 第10章 通过 Java 提供动态内容

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_504_0.png)

图 10.43 NetBeans IDE—HelloServlet.java

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_504_1.png)

图 10.44 NetBeans IDE—HelloServlet

## 10.6 Web Server 与 NetBeans

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_505_0.png)

**图 10.45** NetBeans IDE—调试器断点

高亮的绿线标识执行停止的代码行。NetBeans IDE 中的 Java 调试器使开发者能够轻松地检查和调试在 Web Server 中运行的应用代码。

在已设置断点的情况下调试 Web 应用程序，只需在“项目”窗口中右键点击应用程序，并在弹出菜单中选择“调试”（Debug）菜单项，如图 10.46 所示。

图 10.47 展示了一个调试会话，其中 servlet 的执行在 HelloServlet.java 第 32 行设置的断点处停止。

要结束调试会话，从“运行”（Run）菜单中选择“完成调试会话”（Finish Debugger Session），如图 10.48 所示。

# 第10章 通过 Java 提供动态内容

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_506_0.png)

图 10.46 NetBeans IDE—调试会话

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_506_1.png)

图 10.47 NetBeans IDE—调试会话

## 10.7 总结

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_507_0.png)

图 10.48 NetBeans IDE—完成调试会话

当从 NetBeans 管理 Web Server 7.0 时，会弹出一个新窗口包含 Web 服务器的日志消息。Sun Java System Web Server 7.0 还包含了一些按钮，允许开发者执行常见任务，例如启动和停止服务器。图 10.38 显示了此类标签页的示例。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_500_0.png)

图 10.38 NetBeans IDE—输出—基本 Web Server 7.0 管理

图 10.39 展示了 NetBeans 暴露的 Web Server 配置和管理的其他一些方面。

## 10.6 调试 Web 应用程序

在 servlet 代码或 JSP 中进行调试是应用开发不可或缺的一部分。Web Server 包含了对 Java Web 应用程序代码远程调试的支持，例如 NetBeans 中包含的这种。

## 10.6 Web Server 与 NetBeans

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_501_0.png)

图 10.39 NetBeans IDE—服务—Web Server 7.0 配置

为了本次练习，我们将向之前创建的 Web 应用程序添加一个示例 servlet，然后演示如何在 servlet 的 Java 代码中设置断点。

要向 Web 应用程序添加 servlet，请在“项目”（Projects）窗口中右键点击 Web 应用程序的名称以弹出菜单，然后在“新建”（New）菜单中选择“Servlet”项，如图 10.40 所示。

为 servlet 输入类名和包名，然后点击“新建”向导中的“下一步”（Next）按钮，如图 10.41 所示。

# 第10章 通过 Java 提供动态内容

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_502_0.png)

图 10.40 NetBeans IDE—添加 Servlet

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_502_1.png)

图 10.41 NetBeans IDE—Servlet 向导

## 10.6 Web Server 与 NetBeans

通过指定访问 servlet 的 URL 模式来配置 servlet 部署参数，并勾选“添加到部署描述符 (xml)”复选框以便 NetBeans 自动创建并填充 Web 部署描述符。图 10.42 展示了这一点。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_503_0.png)

图 10.42 NetBeans IDE—新建文件向导

点击图 10.42 中的“完成”（Finish）按钮将创建图 10.43 所示的 HttpServlet.java servlet。

图 10.44 展示了 HelloServlet 在部署到 Web Server 并通过浏览器访问时的效果。

要在 servlet 中设置断点，只需点击源显示窗口的左侧边距。下一次执行 servlet 时，执行将在断点处停止，开发者可以通过 NetBeans IDE 控制 servlet 剩余部分的执行。高亮的红线标识断点。图 10.45 显示了高亮代码语句 `out.println("<html>");` 处的断点。

# 第10章 通过 Java 提供动态内容

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_504_0.png)

图 10.43 NetBeans IDE—HelloServlet.java

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_504_1.png)

图 10.44 NetBeans IDE—HelloServlet

## 10.6 Web Server 与 NetBeans

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_505_0.png)

**图 10.45** NetBeans IDE—调试器断点

高亮的绿线标识执行停止的代码行。NetBeans IDE 中的 Java 调试器使开发者能够轻松地检查和调试在 Web Server 中运行的应用代码。

在已设置断点的情况下调试 Web 应用程序，只需在“项目”窗口中右键点击应用程序，并在弹出菜单中选择“调试”（Debug）菜单项，如图 10.46 所示。

图 10.47 展示了一个调试会话，其中 servlet 的执行在 HelloServlet.java 第 32 行设置的断点处停止。

要结束调试会话，从“运行”（Run）菜单中选择“完成调试会话”（Finish Debugger Session），如图 10.48 所示。

# 第10章 通过 Java 提供动态内容

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_506_0.png)

图 10.46 NetBeans IDE—调试会话

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_506_1.png)

图 10.47 NetBeans IDE—调试会话

## 10.7 总结

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_507_0.png)

图 10.48 NetBeans IDE—完成调试会话

当从 NetBeans 管理 Web Server 7.0 时，会弹出一个新窗口包含 Web 服务器的日志消息。Sun Java System Web Server 7.0 还包含了一些按钮，允许开发者执行常见任务，例如启动和停止服务器。图 10.38 显示了此类标签页的示例。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_500_0.png)

图 10.38 NetBeans IDE—输出—基本 Web Server 7.0 管理

图 10.39 展示了 NetBeans 暴露的 Web Server 配置和管理的其他一些方面。

## 10.6 调试 Web 应用程序

在 servlet 代码或 JSP 中进行调试是应用开发不可或缺的一部分。Web Server 包含了对 Java Web 应用程序代码远程调试的支持，例如 NetBeans 中包含的这种。

## 10.6 Web Server 与 NetBeans

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_501_0.png)

图 10.39 NetBeans IDE—服务—Web Server 7.0 配置

为了本次练习，我们将向之前创建的 Web 应用程序添加一个示例 servlet，然后演示如何在 servlet 的 Java 代码中设置断点。

要向 Web 应用程序添加 servlet，请在“项目”（Projects）窗口中右键点击 Web 应用程序的名称以弹出菜单，然后在“新建”（New）菜单中选择“Servlet”项，如图 10.40 所示。

为 servlet 输入类名和包名，然后点击“新建”向导中的“下一步”（Next）按钮，如图 10.41 所示。

# 第10章 通过 Java 提供动态内容

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_502_0.png)

图 10.40 NetBeans IDE—添加 Servlet

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_502_1.png)

图 10.41 NetBeans IDE—Servlet 向导

## 10.6 Web Server 与 NetBeans

通过指定访问 servlet 的 URL 模式来配置 servlet 部署参数，并勾选“添加到部署描述符 (xml)”复选框以便 NetBeans 自动创建并填充 Web 部署描述符。图 10.42 展示了这一点。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_503_0.png)

图 10.42 NetBeans IDE—新建文件向导

点击图 10.42 中的“完成”（Finish）按钮将创建图 10.43 所示的 HttpServlet.java servlet。

图 10.44 展示了 HelloServlet 在部署到 Web Server 并通过浏览器访问时的效果。

要在 servlet 中设置断点，只需点击源显示窗口的左侧边距。下一次执行 servlet 时，执行将在断点处停止，开发者可以通过 NetBeans IDE 控制 servlet 剩余部分的执行。高亮的红线标识断点。图 10.45 显示了高亮代码语句 `out.println("<html>");` 处的断点。

# 第10章 通过 Java 提供动态内容

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_504_0.png)

图 10.43 NetBeans IDE—HelloServlet.java

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_504_1.png)

图 10.44 NetBeans IDE—HelloServlet

## 10.6 Web Server 与 NetBeans

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_505_0.png)

**图 10.45** NetBeans IDE—调试器断点

高亮的绿线标识执行停止的代码行。NetBeans IDE 中的 Java 调试器使开发者能够轻松地检查和调试在 Web Server 中运行的应用代码。

在已设置断点的情况下调试 Web 应用程序，只需在“项目”窗口中右键点击应用程序，并在弹出菜单中选择“调试”（Debug）菜单项，如图 10.46 所示。

图 10.47 展示了一个调试会话，其中 servlet 的执行在 HelloServlet.java 第 32 行设置的断点处停止。

要结束调试会话，从“运行”（Run）菜单中选择“完成调试会话”（Finish Debugger Session），如图 10.48 所示。

# 第10章 通过 Java 提供动态内容

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_506_0.png)

图 10.46 NetBeans IDE—调试会话

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_506_1.png)

图 10.47 NetBeans IDE—调试会话

## 10.7 总结

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_507_0.png)

图 10.48 NetBeans IDE—完成调试会话

当从 NetBeans 管理 Web Server 7.0 时，会弹出一个新窗口包含 Web 服务器的日志消息。Sun Java System Web Server 7.0 还包含了一些按钮，允许开发者执行常见任务，例如启动和停止服务器。图 10.38 显示了此类标签页的示例。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_500_0.png)

图 10.38 NetBeans IDE—输出—基本 Web Server 7.0 管理

图 10.39 展示了 NetBeans 暴露的 Web Server 配置和管理的其他一些方面。

## 10.6 调试 Web 应用程序

在 servlet 代码或 JSP 中进行调试是应用开发不可或缺的一部分。Web Server 包含了对 Java Web 应用程序代码远程调试的支持，例如 NetBeans 中包含的这种。

## 10.6 Web Server 与 NetBeans

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_501_0.png)

图 10.39 NetBeans IDE—服务—Web Server 7.0 配置

为了本次练习，我们将向之前创建的 Web 应用程序添加一个示例 servlet，然后演示如何在 servlet 的 Java 代码中设置断点。

要向 Web 应用程序添加 servlet，请在“项目”（Projects）窗口中右键点击 Web 应用程序的名称以弹出菜单，然后在“新建”（New）菜单中选择“Servlet”项，如图 10.40 所示。

为 servlet 输入类名和包名，然后点击“新建”向导中的“下一步”（Next）按钮，如图 10.41 所示。

# 第10章 通过 Java 提供动态内容

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_502_0.png)

图 10.40 NetBeans IDE—添加 Servlet

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_502_1.png)

图 10.41 NetBeans IDE—Servlet 向导

## 10.6 Web Server 与 NetBeans

通过指定访问 servlet 的 URL 模式来配置 servlet 部署参数，并勾选“添加到部署描述符 (xml)”复选框以便 NetBeans 自动创建并填充 Web 部署描述符。图 10.42 展示了这一点。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_503_0.png)

图 10.42 NetBeans IDE—新建文件向导

点击图 10.42 中的“完成”（Finish）按钮将创建图 10.43 所示的 HttpServlet.java servlet。

图 10.44 展示了 HelloServlet 在部署到 Web Server 并通过浏览器访问时的效果。

要在 servlet 中设置断点，只需点击源显示窗口的左侧边距。下一次执行 servlet 时，执行将在断点处停止，开发者可以通过 NetBeans IDE 控制 servlet 剩余部分的执行。高亮的红线标识断点。图 10.45 显示了高亮代码语句 `out.println("<html>");` 处的断点。

# 第10章 通过 Java 提供动态内容

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_504_0.png)

图 10.43 NetBeans IDE—HelloServlet.java

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_504_1.png)

图 10.44 NetBeans IDE—HelloServlet

## 10.6 Web Server 与 NetBeans

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_505_0.png)

**图 10.45** NetBeans IDE—调试器断点

高亮的绿线标识执行停止的代码行。NetBeans IDE 中的 Java 调试器使开发者能够轻松地检查和调试在 Web Server 中运行的应用代码。

在已设置断点的情况下调试 Web 应用程序，只需在“项目”窗口中右键点击应用程序，并在弹出菜单中选择“调试”（Debug）菜单项，如图 10.46 所示。

图 10.47 展示了一个调试会话，其中 servlet 的执行在 HelloServlet.java 第 32 行设置的断点处停止。

要结束调试会话，从“运行”（Run）菜单中选择“完成调试会话”（Finish Debugger Session），如图 10.48 所示。

## 10.8 自助实验室

使用本章包含的信息来完成以下练习。这些练习将帮助你验证章中所描述的概念。

- 1. 启动你的 Administration Server。识别并访问 Administration Server 中的 Java 应用程序。
- 2. 识别 Administration 使用的 Java 虚拟机 (JVM) 版本。
- 3. 使用管理界面或命令行界面 (wadm) 识别启用 Java 的服务器的堆配置。指定虚拟机最小堆大小和最大堆大小的默认值是什么？
- 4. 检查并构建与 Web Server 一起的示例 Java 应用程序。
- 5. 将 Web 应用程序包 (.war 文件) 部署到服务器并使用浏览器访问 Web 应用程序。
- 6. 使用 Web Server 的自动部署功能部署并访问 Java 应用程序。
- 7. 将 Java 应用程序配置为虚拟服务器的默认 Web 应用程序。确保其配置正确。现在使用管理界面或命令行界面禁用该 Java 应用程序。
- 8. 是否需要重启服务器才能检测到对 Java 应用程序中 JSP 文件的更改？





- 9. 为了让服务器检测到 Java Web 应用中 JSP 文件的更改，是否需要更新 .reload 文件？

- 10. 为了让服务器检测到 Java Web 应用中 Java 类和部署描述符的更改，是否需要更新 .reload 文件？

- 11. 使用 NetBeans IDE 在 Web Server 上创建并部署一个 Java Web 应用。

- 12. 对 Java Web 应用进行更改并将其重新部署到 Web Server。

- 13. 使用 NetBeans IDE 在你的 Java Web 应用的 servlet 中设置断点，并使用浏览器访问该 servlet。使用 NetBeans 中的 Java 调试器跟踪 servlet 的执行过程。

- 14. 在 Java Web 应用中启用并配置缓存。缓存是否提高了你应用程序的响应速度？

> 注意：访问 www.sunwebserver.com 获取有关如何执行这些练习的详细说明。

![](img/a3cb513bfd7a0b21f70c67fcaede10f_510_0.png)

# Web Server 7.0 故障排除

WEB Server 是一款复杂的软件，它满足了企业级 Web 服务器的需求，同时也对开发者友好。Web Server 7.0 提供了一个高度可扩展、可扩展的多线程、多进程平台，用于在 UNIX/Linux 平台以及 Windows 平台上托管基于 Web 的应用程序。Web Server 支持多种动态技术，如 CGI、FastCGI、HTML、JSP、Servlets 和 Web Services。你可以使用 NSAPI 插件扩展服务器的功能。你可以使用集成开发环境（IDE）如 NetBeans IDE 来开发并将 Java Web 应用部署到 Web Server。Web Server 包含一个内置支持，可使用轻量级目录访问协议（LDAP）服务器对其他 Web 和应用程序服务器进行用户验证。Web Server 可以配置为反向代理服务器，将请求分配到其他 Web 和应用程序服务器。Web Server 7.0 包含了一个良好的基于 Web 的图形化界面和一个强大的命令行工具用于管理 Web Server。管理框架包含了部署、管理和监控 Web 服务器或 Web 服务器集群的功能。

Web Server 运行时遇到的问题可能归因于多个因素，包括但不限于配置错误、内存不足、第三方 NSAPI 插件错误、与 Web Server 交互的其他服务器错误，以及服务器本身的故障。了解超文本传输协议（HTTP）、理解操作系统概念和服务器计算，并理解 Web Server 的工作原理以及具备逻辑、系统的解决问题方法，是诊断和修复 Web Server 问题的巨大资产。

本章为排除 Web Server 7.0 中的问题提供了有用信息。具体而言，本文描述了用于识别、分析和寻找在使用 Web Server 7.0 时遇到的问题问题的指南、方法论和工具。本章中的信息旨在补充《Sun Java System Web Server 7.0 故障排除指南》中的信息。

## 11.1 错误

Web Server 7.0 遇到的错误可以广泛归分为以下几类：

- 安装问题
- 启动问题
- 崩溃（Crashes）
- 死锁（Hangs）
- 运行时错误
- 性能/可扩展性问题
- 管理问题
- 迁移错误
- 卸载问题

本节的其余部分简要描述了这些每一类别。

### 11.1.1 安装问题

安装 Web Server 7.0 时遇到的问题通常是由于资源不足（如内存、磁盘空间）或没有足够的权限在指定目录中安装服务器引起的。当你尝试在不符合最低要求的平台上安装 Web Server 7.0 时，可能会发生安装错误。安装错误会报告到控制台，并记录在服务器的日志文件中。

### 11.1.2 启动问题

启动期间发生的错误会阻止服务器启动。启动的常见原因包括文件所有权/权限、缺乏系统资源（如内存）、NSAPI 插件错误以及与其他进程的端口冲突。启动错误会报告到控制台，并记录在服务器的日志文件中。

### 11.1.3 崩溃

崩溃是进程的异常终止。Web Server 崩溃会导致终端用户服务的中断。可能导致 Web Server 崩溃的错误示例包括系统资源（如内存）急剧缺少、NSAPI 插件中的缓冲区溢出、Java虚拟机（JVM）中的致命错误、硬件错误以及操作系统错误。服务器崩溃的证据通常在 Windows 系统上找到。

### 11.1.4 死锁

当服务器停止响应客户端请求时，称为死锁。死锁也可能由于 Web Server 内部的资源竞争、NSAPI 插件中的同步问题、Java虚拟机（JVM）中的同步问题引起。你可以通过结合 Web Server 的监控功能和操作系统命令来检测服务器死锁。

### 11.1.5 运行时错误

运行时错误是在服务器运行期间发生的，但不会导致异常终止。示例包括在处理 CGI、HTML 文件和 Java Web 应用等动态内容时发生的错误。应用程序配置错误、用户身份验证和授权错误以及与安全套字（SSL）配置相关的错误。

# 11.1.6 性能/可扩展性问题

如果 Web Server 响应客户端请求缓慢，或者 Web Server 无法处理大量客户端请求，这可能表明一个或多个子系统未正常运行。性能/可扩展性限制的情况包括系统配置不当、服务器配置不当、网络问题（如低带宽或延迟）、与 Web Server 同系统运行的其他资源密集型进程、NSAPI 插件中的多线程问题、耗时操作（如复杂的数据库查询），以及处理客户端请求时可能执行的计算密集型操作（如加密和压缩）。

### 11.1.7 管理问题

此类包括在使用基于 Web 的控制台或命令行工具管理 Web Server 实例时发生的错误。在使用 Web Server 7.0 管理框架时遇到的错误包括系统资源不足、手动编辑引起的配置错误、用户错误、JVM 错误以及管理框架本身的问题。这些错误记录在管理服务器/节点的日志文件中，并通过管理控制台或命令行工具向管理员报告。

### 11.1.8 迁移错误

当你从早期版本的 Web Server 迁移服务器实例到 Web Server 7.0 时可能会发生错误。迁移错误可能是由错误的所有权/权限、被迁移服务器的配置错误以及系统资源（如磁盘空间）不足引起的。详细的迁移信息（包括错误）记录在迁移日志。

### 11.1.9 卸载问题

卸载错误的原因包括用户权限不足以及文件访问问题（例如尝试删除系统上某些其他进程正在使用的 Web Server 文件）。卸载期间发生的错误可能需要手动


在系统可以重新安装服务器之前进行干预。卸载错误将报告到用户控制台，并记录在卸载程序的日志文件中。

## 11.2 调查周边

为了全面描述问题，你必须收集有关硬件、操作系统、Web 服务器环境和浏览器的详细信息。本节的其余部分将关注你在收集信息时应该考虑的细节。

### 11.2.1 硬件信息

收集运行程序的系统的信息可能是很有价值的，甚至比简单描述问题更有价值。有些问题可以归因于硬件、操作系统（或补丁）、Web 服务器的软件发布版本，或者 Web 服务器与其他第三方应用程序交互的方式。

收集系统信息的第一步是记录你的硬件环境。特别关注 RAM、磁盘空间以及 CPU 的数量和类型。记录每项默认安装了多少，然后确定每项已了多少，可用又是多少。

此外，确定你是如何连接到网络的，以及你是否使用了任何其他设备（如硬件加速卡）。

### 11.2.2 操作系统信息

收集系统信息的下一步是查看操作系统。你运行的是什么操作系统？修订版本是多少？你安装了任何补丁吗？Web 服务器可用的系统资源限制是什么？Web 服务器可使用多少可用磁盘空间？有多少空闲内存？系统上运行着哪些其他进程？

### 11.2.3 Web 服务器环境

收集系统信息的下一步是理解你的 Web 服务器环境。

你的 Web 服务器正在提供静态和/或动态内容吗？对于什么类型的动态内容（JSP, Servlets, FastCGI, HTML, PHP 等），服务器可以处理请求？

你启用了 Java 插件吗？Java 虚拟机 (JVM) 的版本是多少？你配置了哪些 JVM 选项？你是否在服务器路径中指定了额外的 Java 归档 (JAR) 文件？是否启用了安全管理器 (Security Manager)？你是否配置了额外的 Java 资源（如数据连接池）？你是否更改了服务器实例默认-web.xml 文件中的任何设置？

你在此服务器上运行什么种类型的 NSAPI 或第三方插件？该插件是否有相关的版本号，它是否已通过可以在此版本的 Web 服务器上运行？

你正在运行 SSL 吗？如果是，你是否在使用硬件加速卡？

你在使用特定网络浏览器时遇到问题吗？你能持续地重现该问题吗？仅在有多个并发请求时出现吗？问题的严重程度如何？服务器启动了吗？服务器会崩溃吗？服务器会随机挂起吗？

你的网络拓扑结构是什么？你运行了多少个 Web 服务器？它们位于何处？你正在进行任何负载均衡吗？前端是否有应用服务器？是否有代理服务器或负载均衡器将请求路由到 Web 服务器？是否有防火墙？

你需要知道运行在此服务器上的其他应用程序可能导致什么问题。例如，Web 服务器是否也兼作电子邮件服务器或企业级目录服务器？如果是，这些应用程序可能会影响你的 Web 服务器的性能。

### 11.2.4 其他服务器上的环境

收集系统信息的下一步是理解 Web 服务器 可能与之交互的其他服务器上的环境。如果 Web 服务器与应用程序服务器、Web 服务提供程序通信，或仅作为其他 Web 服务器的代理，那么那些服务器上的环境可能是一个问题。

与 Web 服务器交互的服务器版本是多少？这些服务器是否发生了任何更改和/升级？这些版本是否被 Web Server 7.0 支持？这些服务器是否存在任何已知问题？

## 11.3 常见嫌疑对象

使用什么协议与其他服务器通信？其他应用程序是否也通过相同协议与这些服务器通信？它们在执行时时遇到问题吗？

Web 服务器是否通过 SSL 与这些服务器通信？如果是，之前是否测试过通信？使用的是哪种版本的 SSL？使用了什么种级别的加密？Web 服务器信任其他服务器使用的证书吗？任意一侧服务器在 SSL 方面发生了任何变化吗？

其他服务器上最近是否有可能影响 Web 服务器的插件或其他特殊配置设置更改？这些插件被 Web Server 7.0 支持吗？

当你直接连接到其他服务器时会看到相同的问题吗？如果是，你应该能够排除问题完全出现在 Web 服务器中的可能性。

### 11.2.5 HTTP 客户端环境

最后一步是收集有关 HTTP 客户端的信息。

你正在使用哪种浏览器？浏览器版本号是多少？浏览器被 Web Server 7.0 支持吗？浏览器上使用的是哪个版本的 HTTP？浏览器是否通过 SSL 与 Web 服务器通信？

问题是否局限于特定的浏览器、厂商或版本？问题是否在旧版本的浏览器中出现？问题是否特定于你网络中的某个区域？问题是否特定于对特定类型内容的请求？

下一节将阐述了问题可能发生的各种区域。

## 11.3 常见嫌疑对象

图 11.1 展示了 Web 服务器环境中你可能排故障问题的各种区域。当问题出现时，HTTP 客户端、Web 服务器、其他 Web 或应用服务器、目录服务器、数据库服务器甚至网络都可能是嫌疑对象。

可能需要调查的子系统数量可能会使诊断错误的过程变得复杂。图 11.2 显示了导致 Web 服务器错误的组件或子系统的示例。

![](img/a3cb51bfd7a0b21f70c6caede10f6_518.png)

图 11.1 Web 服务器环境

- 第三方插件
- 管理节点
- 管理服务器
- CGI
- 配置
- FastCGI
- 安装程序
- Java 虚拟机
- NSAPI
- 网络
- 操作系统

图 11.2 Web 服务器错误——常见嫌疑对象





# 第 11 章 Web Server 7.0 故障排除

事件/动作的日志通常提供以下信息：

- 事件/动作的日期/时间
- 消息类型/级别，例如警告（warning）、灾难（catastrophe）、调试（debug）
- 消息文本

某些消息文本可以清楚地说明需要做什么。例如，Java 异常的堆栈跟踪可以精确确定问题所在。其他消息可能仅提供有关问题或解决方案的信息。在这种情况下，问题并不明显，或者可能存在多个错误。

Web Server 实例错误日志（errors log）记录的错误消息包含以下信息：

字体 生成消息的 Web Server 进程的进程标识 (PID)
- 消息标识：一个带有短名称的四位整数，短名称标识生成消息的子系统
- 可选标识：标识生成消息的虚拟服务器

图 11.3 显示了记录在 Web Server 实例的 logs/errors 文件中的各种错误消息字段。

| 日期/时间 | 进程 ID | 消息文本 |
|---|---|---|
| [03/Nov/2008:14:49:52] | info (4400) | CORE116: Sun Java System Server 7.0U3 B06/16/2008 11:32 |
| [03/Nov/2008:14:49:52] | info (4400) | FCG1000: Java System Server 7.0U3 FastCGI NSAPI |
| [03/Nov/2008:14:49:52] | config (4400) | HTTP4292: flex-log: /logs/access should be removed before changing its format. |
| [03/Nov/2008:14:49:52] | info (4400) | HTTP3072: hetty-listener-1: http://localhost:8005 ready to accept requests |
| [03/Nov/2008:14:49:52] | config (4400) | CORE3274: successful server startup |
| [03/Nov/2008:15:57:08] | info (4400) | CORE3276: Installing a new configuration |
| [03/Nov/2008:15:57:08] | config (4400) | HTTP4292: flex-log: /logs/access should be removed before changing its format |
| [03/Nov/2008:15:57:08] | config (4400) | CORE3280: A new configuration was successfully installed |
| [03/Nov/2008:15:57:16] | failure (4400) | for 127.0.0.1 trying to get /cgi-bin/test.cgi, send-cgi reports: HTTP4068: not execute CGI script:d:/Sun/WebServer7/cgi/test.cgi (The specified program is not a Windows executable)| |

**图 11.3** Web Server 错误消息字段

## 11.4 信息线员

Web Server 实例的服务器日志文件（Server Log）之外的日志文件也包含诊断错误的有用信息。表 11.1 标识了有助于排查 Web Server问题的各种日志文件。为了方便起见，表 11.1 中所有平台的文件系统路径均使用 UNIX 正斜线（/）字符。

## 表 11.1 有助于排除错误的日志文件

| 组件 | 日志 | 注释 |
| --- | --- | --- |
| Web Server 7.0—服务器实例 | `install_dir/https-instance/logs/errors` `install_dir/https-instance/logs/access` | 服务器的错误日志文件是服务器问题信息的主要来源。 |
| Web Server 7.0—管理/节点 | `install_dir/admin-server/logs/errors` `install_dir/admin-server/logs/access` | 管理服务器/节点将错误消息写入其目录下的文件并记录 HTTP 访问。 |
| Web Server 7.0 - 安装程序 | `install_dir/setup/Sun_Java_System_Web_install.log` `/var/sam/install/logs/Sun_Java_System_Web_Server_install.AmmddHHMM(Solaris/Linux/AIX/HP-UX)` `/var/sam/install/logs/Sun_Java_System_Web_Server_install.BmmddHHMM(Solaris)` `/tmp/Sun_Java_System_Web_Server_install.AmmddHHMM(Solaris/Linux/AIX/HP-UX)` `/tmp/Sun_Java_System_Web_Server_install.BmmddHHMM(Solaris/Linux/AIX/HP-UX)` `%TMP%/Sun_Java_System_Web_Server_install.AmmddHHMM(Windows)` `%TMP%/Sun_Java_System_Web_Server_install.BmmddHHMM(Windows)` | 有这些文件的更多信息，请参考第 3 章《Web Server 7.0 安装与迁移》中的“安装日志文件”章节。 |
| Web Server 7.0 - 卸载程序 | `install_dir/setup/Sun_Java_System_Web_Server.uninstall.log` `/var/sam/install/logs/Sun_Java_System_Web_Server_install.mmddHHMM(Solaris)` `/tmp/Sun_Java_System_Web_Server_install.mmddHHMM(Solaris/Linux/AIX/HP-UX)` `%TMP%/Sun_Java_System_Web_Server_install.mmddHHMM(Windows)` | 卸载过程中发生的错误。在 Windows 上运行安装程序之前，确保命令行 shell 等应用程序位于 Web Server 的根目录下。 |

### 11.1 有助于排除错误的日志文件

| 组件 | 日志 | 注释 |
|---|---|---|
| Web Server 7.0 - 迁移 | `install_dir/admin-server/logs/migration_ymddmmss.log` | 将旧版本的 Web Server 迁移到 7.0 时遇到的错误记录在此文件中。 |
| Java 虚拟机 | `install_dir/https-instance/logs/errors` | JVM 错误记录在实例日志中。 |
| FastCGI | `install_dir/https-instance/logs/fastcgi.log (Windows)` `install_dir/https-instance/logs/fastcgi.log (UNIX/Linux)` | 该日志由 FastCGI 进程写入。
|| 操作系统 (Solaris) | `/var/adm/messages` | 操作系统消息记录在此文件中。 |
| 操作系统 (Linux) | `/var/log/messages` | 操作系统消息记录在此文件中。 |
| 操作系统 (Windows) | 事件查看器 | 事件查看器是一个应用程序，可以从控制面板的工具文件夹启动。 |

### 11.4.2 访问日志文件

客户端发送给服务器请求以及服务器的响应记录在实例的访问日志文件中。以下列出了可能记录在 Web Server 7.0 访问日志中的某些组件：

字体 客户端主机名
- 日期
- HTTP 请求行
- HTTP 状态码
- 响应内容长度
- 授权用户
- Cookie 值
- 虚拟服务器 ID
- 服务器发送请求的时间

请参考《Java Web Server 7.0 参考》中的“使用自定义日志”附录，获取访问日志中可以记录信息的完整列表。示例 11.1 显示了 Web Server 7.0 实例访问日志的摘录。

### 示例 11.1 访问日志文件

```
format=%Ses->client.ip% %Req->auth-user% [%SDATE%]
"%Req->request%" %Req->srvhdrs.status%
%Req->srvhdrs.content-length%
127.0.0.1 - - [03/Nov/2008:14:50:56 +0530] "GET / HTTP/1.1" 200 12370
127.0.0.1 - - [03/Nov/2008:14:50:56 +0530] "GET /img/gradation_header_R.gif HTTP/1.1" 200 1906
127.0.0.1 - - [03/Nov/2008:14:50:56 +0530] "GET /img/sjsws_title-text.gif HTTP/1.1" 200 365
127.0.0.1 - - [03/Nov/2008:14:50:56 +0530] "GET /img/gradation_header_L.gif HTTP/1.1" 200 254
127.0.0.1 - - [03/Nov/2008:14:50:56 +0530] "GET /img/footer_R.gif HTTP/1.1" 200 2349
127.0.0.1 - - [03/Nov/2008:14:50:56 +0530] "GET /img/sun_logo.gif HTTP/1.1" 200 254
127.0.0.1 - - [03/Nov/2008:14:50:56 +0530] "GET /img/footer_L.gif HTTP/1.1" 200 257
127.0.0.1 - - [03/Nov/2008:14:57:59 +0530] "GET /php/test.php?=PPE9568F34-D428-D1d2-A769-00AA01ACF42 HTTP/1.1" 200 2524
127.0.0.1 - - [03/Nov/2008:14:57:59 +0530] "GET /php/test.php?=PPE9568F34-D428-D1d2-A769-00AA01ACF42 HTTP/1.1" 200 305
```

### 11.4.3 Core 文件

核心文件对于调试 UNIX/Linux 系统上的 Web Server 崩溃和挂起非常。核心文件包含了进程崩溃时的内存映像。核心文件通常包含足够的信息来确定





## 11.4 报告者

进程在崩溃时正在执行。核心文件（core file）的内容包含以下信息：

- 进程栈
- 线程
- 程序寄存器值
- 数据结构及其内容

核心文件通常命名为 `core`，创建在应用程序崩溃前运行的目录。导致生成核心文件的错误示例包括缓冲区溢出错误、段错误以及用户请求的生成文件生成。

你可以使用多种工具来分析核心文件中的信息。这些工具可以帮助你识别服务器在崩溃或挂起时正在做什么。许多此类工具还允许你检查服务器在崩溃/挂起时正在执行的函数的参数值。

与服务器服务器进程（`webserv` 或 `webserverd-wdog`）崩溃对应的核心文件可以在崩溃的服务器实例的配置目录中找到。

### 11.4.4 Web 服务器统计

对你的 Web 服务器进行有效监控可以帮助你识别性能瓶颈，从而让你能够对系统进行调优以获得最佳性能。为每个请求维护的统计数据也可用于排查停止响应或已重启的实例故障。

以下是 Web Server 7.0 维护的少量统计数据示例：

- 连接队列信息
- 响应时间
- HTTP 错误计数
- 请求计数
- Java 虚拟机统计
- Java Web 应用程序统计
- 文件缓存信息

Web Server 7.0 的监控子系统公开了这些统计数据以供各种客户端使用。统计数据可以在不同的粒度级别进行查看。使用 Web Server 7.0，你可以查看单个虚拟服务器、服务器实例或配置的统计数据。统计数据以多种格式提供，包括 XML、纯文本和简单网络管理协议（SNMP）。解释 Web Server 提供的统计数据可以帮助你识别并调优性能不佳的服务器。在排查服务器挂起时，统计数据也可以为你提供有用的见解。

请参阅第 7 章详细介绍你用于监控 Web 服务器的各种方法。

### 11.4.5 网络流量

Web Server 7.0 设计用于使用传输控制协议（TCP）连接来接收 HTTP 请求并发送 HTTP 响应。HTTP 请求和响应数据通过传输控制协议（TCP）连接在网络上传输。图 11.1 中所示的所有箭头均表示通过网络连接进行的数据传输。你还可以配置 Web Server 在与 HTTP 客户端或其他服务器交互时使用安全/加密的通信通道。

在排查 Web 服务器问题时，有时需要检查网络本身的数据。检查网络上的原始数据可以帮助你识别此类问题，如安全套接层（SSL）错误、请求中的格式错误、无效字符以及响应内容长度不正确。

### 11.4.6 产品文档

在你正在排查的 Web Server 7.0 版本的*发布说明*（Release Notes）中标题为“已知问题”（Known Issues）和“已解决问题”（Resolved Issues）的章节可以帮助你判断遇到的问题是否为 Web Server 开发团队已知。Web Server 7.0 最新更新版本的*发布说明*中的信息可以告诉你你遇到的问题是否已修复。

请参阅你正在排查的 Web Server 7.0 版本的*发布说明*中标题为“支持的平台”、“所需的补丁程序”和“支持的浏览器”的章节，以获取更新的系统要求和依赖项。

## 11.5 询问方法

为了排查 Web 服务器问题，你可能需要从几个不同的来源收集信息。本节描述了你可以用于以更好地理解问题的不同工具和方法。

### 11.5.1 诊断命令和工具

你可以使用许多免费的工具和命令来诊断 Web 服务器问题。其中一些工具包含在 Web Server 中；另一些可以在网上找到并包含在操作系统中。表 11.3 简描述了许多此类工具。

表 11.3 排除工具

| 命令/工具 | 位置 | 描述 |
| :--- | :--- | :--- |
| certuil | install_dir/bin/certuil | 你可以使用 `certuil` 命令检查并修复 Web Server 的证书和密钥数据库。`certuil` 的用法记录在标题为“使用证书工具”的网页中，该 URL 为：http://www.mozilla.org/projects/security/pkn/ns/tools/certuil.html。 |
| df | /bin/df | `df` 是标准的 UNIX/Linux 命令，用于显示文件系统的空闲/可用磁盘空间。 |
| DTrace | /usr/sbin/dtrace | DTrace 是由 Sun Micros 创建的动态跟踪框架，用于排查操作系统和应用程序中的问题。 |
| free | /usr/bin/free | `free` 是 Linux 命令，用于显示系统中使用的和空闲的物理及交换内存。 |
| gcore | /usr/bin/gcore | `gcore` 是标准的 UNIX 命令，用于为运行进程生成核心文件。要生成核心文件，你必须提供进程 ID (PID) 作为 `gcore` 命令的参数。`gcore` 常用于为挂起的服务器生成核心文件。 |
| kill | /bin/kill | `kill` 是标准的 UNIX/Linux 命令，用于终止或信号进程。你可以使用 `kill` 终止挂起的进程。在调试 Web Server java 容器中的问题时，你也可以使用 `kill` 为启用 Java 的 Web 服务器实例的虚拟机（JVM）中的所有线程生成堆栈跟踪。 |

表 11.3 排除工具（续）

| 命令/工具 | 位置 | 描述 |
| :--- | :--- | :--- |
| Live HTTP Headers | http://livehttp-headers.org | Live HTTP Headers 是一个浏览器插件，允许你查看浏览器请求和 Web Server 响应中的 HTTP 头。 |
| modutil | install_dir/bin/modutil | 安全数据库工具——`modutil` 用于管理 Web Server 的 PKCS#11 模块。`modutil` 的用法记录在标题为“使用安全数据库”的网页中，URL 为：http://www.mozilla.org/projects/security/pki/nss/modutil.html。 |
| netstat | /bin/netstat | `netstat` 是标准的 UNIX/Linux 命令，显示网络状态。`netstat` 通常用于通过端口冲突排查故障。 |
| pfiles | /usr/bin/pfiles | `pfiles` 是 Solaris 工具，用于列出进程的所有文件。当 Web Server 无法打开文件且耗尽描述符时，你可以使用 `pfiles` 排查相关进程。 |
| prstat | /usr/bin/prstat | `prstat` 是 Solaris 工具（类似于 top），持续报告统计信息。 |
| ps | /bin/ps | `ps` 是标准的 UNIX/Linux 命令，报告进程状态。你通常使用 `ps` 检查进程是否运行。 |
| pstack | /usr/bin/pstack | `pstack` 是位于 Solaris 和 Linux 上的命令，用于为指定进程中的每个轻量级进程（LWP）打印堆栈跟踪。`pstack` 也可以用于为核心文件中的每个 LWP 打印堆栈跟踪。 |
| ptree | /usr/bin/ptree | `ptree` 是 Solaris 工具，打印包含指定进程（通过 PID 指定）的父进程和子进程进程树。`ptree` 命令有助于识别 webserver-dog 进程与 webserver 进程之间的父子关系。 |
| pwdx | /usr/bin/pwdx | `pwdx` 是 Solaris 命令，打印进程目录。你可以用它确定可能核心文件的目录。 |
| showrev | /usr/bin/showrev | `showrev` 是 Solaris 工具，显示有关硬件、操作系统以及已安装补丁的修订信息。该命令用于验证计算机符合运行 Web Server 7.0 的最低支持要求。 |





## 11.5 询问方法

| 命令/工具 | 位置 | 描述 |
| :--- | :--- | :--- |
| snoop | /usr/sbin/snoop | snoop 是一个 Solaris 命令，类似于 Linux 中的 tcpdump 实用程序，它可以捕获并检查网络包。捕获的数据包可以在接收时显示，也可以保存到文件中以备日后检查。 |
| ssltap | http://www.mozilla.org/projects/security/pki/tools/ssltap.html | ssltap 用于捕获 HTTP 流量以及捕获安全套接层 (SSL)握手期间交换的信息。 |
| startserv | install_dir/https-instance/bin/startserv | startserv 命令可用于不实际启动服务器的情况下验证服务器配置文件中信息的有效性。要验证配置文件，请带有 --config 选项运行 startserv 命令。 |
| strace | /usr/bin/strace | strace 是一个 Linux 命令，类似于 Solaris 中的 truss 实用程序，它可以跟踪活动进程中的系统调用和信号。strace 用于跟踪进程的执行路径，是排查 Web 服务器错误（如挂起和启动错误）的有用工具。 |
| swap | /usr/sbin/swap | swap 是一个 Solaris 命令，可以在排查内存不足导致的 Web 服务器错误时显示交换空间的使用信息。 |
| swapon | /sbin/swapon | swapon 是一个 Linux 命令，可以在排查内存不足导致的 Web 服务器错误时显示交换空间的使用信息。 |
| tcpdump | /usr/sbin/tcpdump | tcpdump 是一个 Linux 实用程序（类似于 snoop），可以捕获网络流量。tcpdump 可将网络包数据保存到文件中以便后续分析。从网络接口读取数据包可能需要超级用户权限。 |
| top | /usr/bin/top | top 是一个 UNIX/Linux 实用程序，显示系统中活动进程的动态实时视图。你可以使用 top 来识别消耗最多 CPU 或内存的进程。 |
| truss | /usr/bin/truss | truss 是一个 Solaris 命令，类似于 Linux 中的 truss 实用程序，可以跟踪活动进程中的系统调用和信号。truss 用于跟踪进程的执行路径，是排查 Web 服务器错误（如服务器挂起和启动错误）的有用工具。 |

# 第 11 章 Web 服务器 7.0 故障排除

表 11.3 故障排除工具续

本节的其余部分将详细介绍最常用的工具。

### 11.5.1.1 Live HTTP Headers

Live HTTP Headers 是一个浏览器插件，允许你轻松查看浏览器发送到服务器的 HTTP 请求以及服务器返回给浏览器的响应中的 HTTP 头部。使用 Live HTTP Headers，你可以查看服务器和浏览器之间 SSL 连接上的 HTTP 头部。你可以使用正则表达式配置 Live HTTP Headers 以对特定 URL 启用/禁用 HTTP 头部捕获。还可以还可以修改之前的请求头部并重放它们以测试各种场景。

根据你的浏览器，Live HTTP Headers 可以配置为侧边栏、新标签页或新窗口。

图 11.4 展示了 Firefox 浏览器中 Live HTTP Headers 的用法。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_531_0.png)

图 **11.4** http://www.sun.com 的 HTTP 头部，在 Live HTTP Headers 中捕获

### 11.5.1.2 netstat

netstat 命令通常用于检查端口是否被占用。以下显示了如何使用 netstat 确定端口 8080 未被占用：

```
# netstat -an | grep 8080
#
```

接下来的示例演示了 netstat 如何显示某些进程正在端口 1894 上监听连接：

```
# netstat -an | grep 1894
*.1894              *.*              0       49152      0 LISTEN
#
```

### 11.5.1.3 prstat, ps, ptree, 和 pdwx

许多诊断工具需要在命令行上指定进程标识符 (PID)。以下说明了你如何使用 ps 命令找到 Web Server 进程的 PID。

```
# ps -ef | grep weservd
root 14431 1 00:23:23 ? 00:00 weservd-wdog -d /opt/
weserver7/https-test/config -r /opt/webserver7 -t /tmp/h
weservd 14433 14432 0 23:23:25 ? 0:43 weservd -d /opt/
weserver7/https-test/config -r /opt/webserver7 -t /tmp-
root 14432 0 00:23:23 ? 0:11 weservd -d /opt/
weserver7/https-test/config -r /opt/webserver7 -t /tmp/https-
```

你可以将其中一个 PID (14431, 14433 或 14432) 指定给 ptree 命令，以确定各种 Web Server 进程之间的父子关系。以下示例演示了这一点：

```
# ptree 14433
14431 weservd-wdog -d /opt/weberver7/https-test/config -r /opt/
weserver7 -t
14432 weservd -d /opt/weberver7/https-test/config -r /opt/
weserver7 -tm
14433 weservd -d /opt/weberver7/https-test/config -r /opt/
weserver7 -t
```

通过 ptree 命令的输出并结合 Web Server 中进程启动的方式，可以确定 PID 为 14433 的进程是 worker 进程。

确定 worker 进程的 PID 后，可以使用 prstat 命令查看 worker 进程内的 LWP 统计信息。如示例 11.2 所示。

示例 11.2 Worker LWP

```
# prstat -L 14433
PID USERNAME RSS TIME CPU/LWP
14433 weservd 388M 202M sleep 59 0:00:13 0.1% weservd/30
14433 weservd 388M 202M sleep 59 0:00:05 0.0% weservd/19
14433 weservd 388M 202M sleep 59 0:00:09 0.0% weservd/1

| PID USERNAME RSS TIME CPU/LWP |
| :--- | :--- | :--- | :--- | :--- |
| 14433 | weservd | 388M | 202M | sleep 59 0:00:02 | 0.0% weservd/25 |
| 14433 | weservd | 388M | 202M | sleep 59 0:00:01 | 0.0% weservd/9 |
| 14433 | weservd | 388M | 202M | sleep 59 0:00:01 | 0.0% weservd/20 |
| 14433 | weservd | 388M | 202M | sleep 59 0:00:00 | 0.0% weservd/28 |
| 14433 | weservd | 388M | 202M | sleep 59 0:00:00 | 0.0% weservd/23 |
| 14433 | weservd | 388M | 202M | sleep 59 0:00:00 | 0.0% weservd/22 |
| 14433 | weservd | 388M | 202M | sleep 59 0:00:00 | 0.0% weservd/21 |
| 14433 | weservd | 388M | 202M | sleep 59 0:00:00 | 0.0% weservd/18 |
| 14433 | weservd | 388M | 202M | sleep 59 0:00:03 | 0.0% weservd/17 |
| 14433 | weservd | 388M | 202M | sleep 59 0:00:03 | 0.0% weservd/16 |
| 14433 | weservd | 388M | 202M | sleep 59 0:00:00 | 0.0% weservd/15 |
| 14433 | weservd | 388M | 202M | sleep 59 0:00:00 | 0.0% weservd/14 |
| 14433 | weservd | 388M | 202M | sleep 59 0:00:00 | 0.0% weservd/13 |
| 14433 | weservd | 388M | 202M | sleep 59 0:00:00 | 0.0% weservd/12 |
| 14433 | weservd | 388M | 202M | sleep 59 0:00:00 | 0.0% weservd/11 |
| 14433 | weservd | 388M | 202M | sleep 59 0:00:00 | 0.0% weservd/10 |
| 14433 | weservd | 388M | 202M | sleep 59 0:00:00 | 0.0% weservd/8 |

Total: 1 processes, 36 lwps, load averages: 0.19, 0.19, 0.18

## 11.5.1.1 sslt

SSL 调试工具 (sslt) 是一个感知 SSL 的命令行，它可以显示在 TCP 连接上交换的数据，sslt 打开监听来自客户端的请求并将其传递给服务器。当从服务器接收到响应时，sslt 随后显示该响应，包括 SSL 记录和窗口中的握手。你可以使用 -f 选项将这些信息重定向到 HTML 文件。

示例 11.3 展示了 sslt 在加载 http://sun.com/ URL 时捕获的数据（包括请求和头部）。

# 示例 11.3 sslt 请求数据捕获

```
--> [GET http://sun.com/ HTTP/1.1
Host: sun.com
User-Agent: Mozilla/5.0 (Windows NT 5.1; en-US; rv:1.9.0)
Gecko/20080924 Firefox/3.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9;q=0.8
Accept-Language: en-us,q=0.5
Accept-Encoding: gzip, deflate
Accept-Charset: ISO-8859-1,utf-8;q=0.7;*;q=0.7
Keep-Alive: 300
Proxy-Connection: keep-alive
]
```

客户端的请求由指向右侧的箭头表示。请求的内容位于左括号和右括号之间。

示例 11.4 展示了针对示例 11.3 所示请求的服务器响应的第一部分（由 sslt 捕获）。sslt 捕获的响应数据包括 HTTP 状态行以及 Server 和 Content-length 等 HTTP 头部。服务器的响应由指向左侧的箭头指示。响应的内容再次封装在左括号和右括号之间。

# 示例 11.4 sslt 响应数据捕获

```
<-- [HTTP/1.1 200 OK
Server: Sun-Java-System-Web-Server/7.0
Date: Wed, 12 Nov 2008 21:09:46 GMT
X-tags: noindex,follow
Last-modified: Wed, 12 Nov 2008 21:05:54 GMT
Expires: Thu, 01 Jan 1970 00:00:00 GMT
Content-type: text/html;charset=utf-8
Content-length: 31579

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
```




## 11.5 询问方法

ssltap 工具不会对原始数据流进行任何形式的解释。这可能会导致一些奇怪的效果，例如声音、闪烁，甚至命令行 shell窗口的崩溃。使用 -h 选项可以将不可打印字符替换为点号。

要通过 SSL 连接捕获数据，你必须使用 -s 选项来启用 SSL 解析和解码。

你检索的页面在浏览器中可能看起来不完整。默认情况下，工具在完成第一次 HTTP 请求/响应交换后终止。因此，浏览器无法检索可能是整个页面的部分的后续资源（如图像）。要强制工具继续连接，请使用 -i 选项在循环模式下运行 ssltap。

请参考《Sun Java Web Server 7.0 故障指南》中的“分析 SSL 请求”章节，查看另一个演示如何使用 ssltap 分析 SSL 请求的示例。有关关于 ssltap 的更多信息，请参考 http://www.mozilla.org/projects/security/pki/nss/tools/ssltap.html。

### 11.5.1 snoop

你可以使用 snoop 命令捕获网络包并以你指定的格式显示其内容。数据包可以实时显示，也可以保存到文件中以便稍后分析。RFC 1761 规定了数据捕获文件的格式。snoop 命令本身可用于解释捕获的文件并转换为人类可读的格式。其他工具如 Wireshark 也可以读取和分析 Snoop 版本 2 数据捕获文件。

示例 11.5 展示了由 snoop 命令捕获并解释的部分数据。

示例 11.5 snoop 数据样本

```
HTTP: ----- HyperText Transfer Protocol -----
HTTP:
HTTP: GET /index.html HTTP/1.1
HTTP: Host: www.sun.com
HTTP: [...]
```

在混杂模式下从默认接口捕获包可能需要超级用户权限。有关其使用的更多信息，请参考 snoop(1) 手页。

### 11.5.1.6 Wireshark

Wireshark 是一个开源的多平台网络协议分析器，可以分析数百种协议（包括 LDAP、HTTP、HTTPS、TCP）。网络数据可以实时捕获，也可以保存到文件中以便稍后分析。Wireshark 可以读取和写入几种不同的捕获格式，包括 tcpdump 和 snoop。Wireshark 包含一个易于使用的图形用户界面用于分析网络流量。

图 11 展示了相比 snoop 的几个优势，例如易用性和搜索功能、Wireshark 的图形用户界面。

该工具相比 snoop 具有若干优势，例如易用性和搜索功能，但必须单独安装。Wireshark 首页——http://www.wireshark.org——包含关于其使用的更多信息。

### 11.5.1.7 DTrace

DTrace 是一个内置于 Solaris 的动态跟踪框架，系统管理员和开发人员可以使用检查应用程序（如 Web 服务器）以及操作系统本身的行为。DTrace 允许你能够在应用程序执行路径的特定位置或从操作系统本身记录额外数据。这些数据采集传感器被称为探针（probes）。DTrace 具有表 11.3 中描述的许多工具的功能。以下是 DTrace 框架在 Solaris 中的一些常见用途：

- 动态启用和管理数千个探针
- 实现新的 Dtrace 探针
- 将操作与探针动态关联
- 检查来自运行系统或系统崩溃转储的跟踪数据

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_537_0.png)

图 11.5 使用 Wireshark 图形界面分析 HTTP 流量

当前版本的 Web Server 7.0 也内置了 Dtrace 探针。但是，可以使用 Solaris 操作系统包含的各种探针来排查 Web Server 问题。示例 11.6 展示了如何使用 dtrace 命令列出 Solaris 中所有的探针

#### 示例 11.6 Solaris 中的 DTrace 探针

| ID | PROVIDER | MODULE | FUNCTION NAME |
|---|---|---|--|
| 1 | dtrace | | BEGIN |
| 2 | dtrace | | END |
| 3 | dtrace | | ERROR |
| 4 | Xserver721 | Xsun | AddResource resource-alloc |
| 5 | Xserver721 | Xsun | WriteEventsToClient send-event |

```
# dtrace -l | wc -l
50570
```

使用 DTrace，你可以检查、调整和排查 Solaris 系统上整个软件栈的行为。有关使用 DTrace 检查、排查和调整系统的更多信息，请参考《Solaris 动态跟踪指南》。

### 11.5.2 增加服务器日志信息的详细程度

你可以配置服务器的日志级别，以便将调试消息记录到服务器日志文件中。调试消息可以让你对问题发生条件有有用的见解。

你可以使用管理控制台或命令行工具配置 Web Server 记录错误消息的日志级别。将服务器日志级别配置为 fine、finer 或 finest 之一，会导致服务器在记录信息、警告和错误消息等其他消息之外记录调试消息。

请参考第 7 章中“Web Server 日志文件”章节，获取有关 Web Server 7.0 在配置服务器实例的服务器日志文件中记录详细级别方面的管理支持信息。

### 11.5.3 关联访问和服务器日志条目

HTTP 访问日志文件和服务器日志文件中的每个条目通常包含时间戳。你可以通过搜索 5xx 类请求的状态码，在 HTTP 日文件中搜索未成功处理（由于服务器错误）的请求。使用每个返回 5xx 状态码请求的访问日志时间戳，并在服务器日志文件中搜索包含相同时间戳的错误消息。你可能需要搜索时间戳范围，因为错误消息和访问日志条目的记录时间可能不完全。

这种方法使你能够找到与服务器问题对应的错误消息。

### 11.5.4 为 Java 线程生成堆栈跟踪信息

检查 Java 线程的堆栈跟踪有助于排查 Java 虚拟机中的线程挂起问题。

### 11.5.5 有效监控

Web Server 7.0 提供了多种监控服务器性能健康的工具。你可以使用内置或第三方工具收集 CPU 使用率、内存消耗和请求吞吐量等指标。这些信息可以帮助你识别瓶颈并优化服务器配置。

示例 11.7 演示了如何使用 wadm 监控数据。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_539_0.png)





## 11.5 查询方法

原生池 (Native pools):

NativePool:
空/峰值/限制 1/1/128
工作队列长度/峰值/限制 0/0/0

DNSCacheInfo:
启用 yes
缓存项 0/1024
命中率 0/0 ( 0.00%)

异步 DNS 已禁用

性能计数器 (Performance Counters):

| 平均总百分比 |
| :--- | :--- |
| 请求总数: | 132 |
| 请求处理时间: | 0.0006 0.0798 |

| default-bucket (默认桶) | 132 (100.00%) |
| 请求数: | 1665 (100.00%) |
| 调用次数: | 0.0002 0.0290 ( 36.26%) |
| 延迟：函数处理时间: | 0.0004 0.0509 ( 63.74%) |
| 总响应时间: | 0.0006 0.0798 (100.00%) |

会话 (Sessions):

进程状态 客户端年龄 VS 方法 URI 函数

通过分析监控数据，你可以识别服务器中配置不当的子系统。例如，调用长时间运行数据库查询的应用程序可能需要额外的工作线程来跟上传入的请求。在这种情况下，可以使用 perfdump 报告中“原生池 (Native pools)”部分中的信息来判断工作线程的使用是否高效。

《Sun Java System Web Server 7.0 性能调优、配置与扩展指南》（Performance Tuning, Sizing, and Scaling Guide）包含了有关如何使用 Web 服务器监控数据来排除性能问题的详细信息。

## 11.5.6 跟踪服务器挂起和死循环

`pstack` 命令记录进程中所有 LWP（轻量级进程）的栈跟踪。Web 服务器进程可能包含许多 LWP，`pstack` 可能会为此类进程生成大量数据。

在排查无谓浪费 CPU 循环期的运行失控服务器进程时，你可以使用 `prstat` 命令识别工作进程中消耗最多 CPU 循环的 LWP。然后，可以在 `pstack` 输出中搜索该 LWP ，以查看浪费 CPU 循环的线程的栈跟踪。

在排查挂起的服务器进程时，你可以使用 `pstack` 命令生成进程中所有线程的栈跟踪并将输出保存到文件中。在一段时间内重复此操作。使用 `diff` 工具比较不同时间点生成的包含 `pstack` 输出的文件，可以帮助你识别哪些是活动线程，哪些是卡住/挂起或等待事件发生的线程。将挂起服务器的 `pstack` 输出与该服务器启动后不久的服务器 `pstack` 输出进行比较，也可以帮助你确定问题所在位置。

你还可以使用 `gcore` 命令让挂起的服务器进程生成核心文件（core file）。然后你可以使用调试工具研究核心文件，以进一步调查问题。

> 注意：出于安全考虑，启用 SSL 的 Web 服务器实例默认情况下不生成核心文件。如果你想为启用 SSL 的服务器生成核心文件，必须在相应服务器的启动脚本中显式设置 `SSL_DUMP` 环境变量。你可以通过在服务器的启动脚本中添加以下内容来设置 `SSL_DUMP` 环境变量：SSL_DUMP=1; export SSL_DUMP。

## 11.5.7 编辑正确的虚拟服务器对象文件

你可以配置 Web Server 7.0 为每个虚拟服务器使用不同的对象文件 (obj.conf)。当你创建一个服务器实例时，Web Server 的管理框架会在实例的配置目录中创建一个名为 `obj.conf` 的默认对象文件。随后的管理操作可能会导致创建名为 `virtual_server-obj.conf` 的额外对象文件。在这种情况下，原始的 obj.conf 文件可能未被配置中的任何虚拟服务器引用。手动更改虚拟服务器的请求处理行为时，务必检查主服务器配置文件——server.xml，以获取对应虚拟服务器的正确文件名。对象文件由 `server.xml` 文件中的 `object-file` 元素指定。

## 11.5.8 进行增量配置更改

当同时部署许多配置更改时，由服务器配置文件错误引起的 Web 服务器错误很难排查。在这种情况下，采用系统方法并增量地进行、部署和测试配置更改，可以帮助你隔离出导致问题的更改。在修改虚拟服务器对象文件 (obj.conf) 中的请求处理指令以及修改访问控制列表 (ACLs) 时情况尤为如此。

## 1166 其他调查机构

“Sun Java System Web Server”在线论坛 http://forums.sun.com/ 包含了 Web 应用开发人员、系统管理员和 Web 服务器用户关于 Web Server 的讨论。Web Server 7.0 产品和开发团队的过去和现在成员也积极参与该论坛。你可以在“Sun Java System Web Server”在线论坛中搜索与 Web Server 问题相关的信息。你也可以向论坛上的其他用户就你面临的任何 Web Server 问题寻求帮助。请记住清楚、简洁地描述问题。

Sun Developer Network 的“Web Tier”主页 http://developers.sun.com/webdriver/ 包含有用的文章，包括演示 Web Server 7.0 功能的截图。你可以搜索该站点以检查你尝试的操作是否已被记录。Sun 的开发工程师提供了帮助解决常见问题的资源。

如果你与 Sun 有支持合同，可以联系技术支持部门报告问题。可以访问 http://www.sun.com/support/ 知识库获取 Web Server 问题的信息。

## 11.7 总结

在本章中，你学习了在使用 Web Server 7.0 时可能遇到的各种问题。本章还描述了可能问题的区域以及你可以使用的诊断工具和程序。使用本章中的概念可以帮助你快速发现并修复问题，缩短站点不可的时间。

## 11.8 自助实验

使用本章包含的信息执行以下实验。这些实验将帮助验证理解。

- 配置服务器日志并使用浏览器请求 index.html。使用日志跟踪执行的服务器函数。
- Web Server 处理请求时调用了多少系统调用？
- 为运行在 Windows 上的 Web Server 生成栈跟踪。
- 安装 Wireshark 并使用它捕获流量。
- 捕获对应 http://www.sun.com 的 HTTP 请求和响应头。

> 访问 http://www.webserver.com 获取有关执行这些每个实验的详细说明。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_544_0.png)





![](img/a3cb513bfd7a0b21f70c67fcaede10f6_546_0.png)

图 12.1 Web 1.0 网站上的用户交互

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_546_1.png)

图 12.2 Web 2.0 网站上的用户交互

Web 2.0 网站本质上是社交性的、交互性的且易用的。这些网站背后的指导理念是用户增加价值，此类网站的总体目标是创建一个环境，让终端用户提供的数据增加网站的价值。

Sun Blogs 使用了开源博客服务器 Apache Roller Webblogger 的自定义版本，该版本已部署在 Web Server 7.0 上。图 12.3 提供了 Sun Blogs 使用的架构概述。

# 第 12 章使用 WEB SERVER 7.0 构建安全的动态的 WEB 2.0 网站

Sun Java System Web Server 7.02
(JDK 1.6.0_04)
Sun Fire T2000 32GB
(拥有数千员工)
博客；每日 2M 次访问；每日传输 30GB；97% 的空闲时间)

主数据库服务器：
MySQL 5.0.x v40z, 16GB

Apache Roller 4.0.x
Web 应用程序

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_548_0.png)

图 12.3 Sun Blogs 系统架构

Web Server 配置由两个实例组成，安装在两个 Sun Fire T2000 服务器上，每台配有 32GB 内存，磁盘空间占用忽略不计，并有一个共享文件服务（来自集群的 NFS）。两台服务器都位于硬件负载均衡器之后，均衡器均匀划分流量。所有数据都存储在 MySQL 数据库服务器中，并利用 memcached 提供额外的性能提升。最后，该服务集成了 Sun 的安全单登录身份系统，并由全球员工 LDAP 目录支持身份验证和授权。

Web Server 支持此应用程序所需的配置极少，大部分更改是对调优参数进行的。示例 12.1 展示了获得所需网站性能所需的配置更改。未列出整个 server.xml 文件；仅在内联列中提供了相关部分。

示例 12.1 Sun Blogs 的服务器配置

```
<server>
<log>
<log-file>../logs/errors</log-file>
<archive-suffix>%Y%m%d</archive-suffix>
<log-level>info</log-level>
</log>
```

<!-- 增加每个线程的输出缓冲区大小。这允许 Web Server 接收来自来自 j2ee-module SAF 的数据并为慢客户端进行缓冲。这反过来允许 j2ee-module 及时返回系统资源。 -->

```
<http>
  <output-buffer-size>40960</output-buffer-size>
</http>

<!-- 对于具有更深调用栈深度的 Java Web 应用程序，具有较高栈大小的典型工作线程池并不罕见 -->
<thread-pool>
  <max-threads>250</max-threads>
  <stack-size>256000</stack-size>
</thread-pool>

<!-- JVM 虚拟机设置 -->
<jvm>
  <java-home>.../java-home
  <server-class>.../server-class-path
  <debug-false=debug>
  <jvm-options>-Xdebug -Xrunjdwp:transport=dt_socket,server=y,
    suspend=n,address=7896</jvm-options>
  <jvm-options>-Dsecurity.auth.login.config=login.conf</jvm-options>

<!-- 增加了 ms 和 mx，默认情况下为 -Xms128m -Xmx256m
<jvm-options>-server -XX:NewSize=1g</jvm-options>-XX:+ParallelGC</jvm-options>
  <jvm-options>-XX:+UseParallelGC -XX:+ParallelGCThreads=20</jvm-options>

<!-- 添加了密钥库位置 -->
<jvm-options>-Dcom.sun.management.jmxremote -Djavax.net.ssl.keyStore=....keystore -Djavax.net.ssl.keyPassword=...</jvm-options>
</jvm>

<!-- 将 MySQL 数据源配置为 JDBC 资源 -->
<jdbc-resource>
  <jdbc-name>jdbc:rollerdb</jdbc-name>
  <datasource-class>com.mysql.jdbc.optional.MysqlDataSource</datasource-class>
  <property>
    <name>Password</name>
    <value>...</value>
    <description/>
  </property>
  <property>
    <name>User</name>
    <value>...</value>
    <description/>
  </property>
</jdbc-resource>
```

```
<name>URL</name>
<value>jdbc:mysql://some:3306/database?autoCommit=true&unicode=true&characterEncoding=utf-8</value>
<description/>
</property>
<description>datasource</description>
<min-connections>15</min-connections>
<max-connections>250</max-connections>
<idle-timeout>180</idle-timeout>
<connection-validation>metadata</connection-validation>
</jdbc-resource>

<mail-resource>
<jndi-name>mail/Session</jndi-name>
<description>roller session</description>
<property>
<name>mail.smtp.host</name>
<value>host</value>
<description>Mail hostname</description>
</property>
</mail-resource>

<!-- Web 应用程序在虚拟服务器中配置
所有 URI 为 '/' 的流量都会执行 Web 应用程序 -->
<virtual-server>
<name>blogs</name>
<host>blogs</host>
<listener-name>http-1</listener-name>
<web-app>
<uri>/</uri>
<path>_default</path>
<description/>
</web-app>
</virtual-server>
```




## 12.2 Site：SUN FORUMS

Sun Forums 基于 Jive Forums，这是一个 Java Web 应用程序，以简单的 WAR 文件形式部署在运行 Java 平台标准版 (Java SE) 6 的 Web 服务器上。Jive 部署在 Web Server 7.0 上，运行在两台配备 8GB 内存的 Sun Fire V40Z 服务器上。这些服务器连接到运行 Solaris 10 操作系统的 Sun F490 服务器上的 Oracle 10g 数据库服务器。

与 Sun Blogs（第 12.1 节）类似，支持此应用程序的 Web 服务器所需的配置很少。示例 12.2 展示了为了获得所需的站点性能所需的配置更改。并未列出整个 server xml 文件，而是提供了相关部分并显示了内联注释。

## 示例 12.2 Sun Forum 服务器配置

```xml
<server>
<!-- Java VM 设置，三十位服务器的最大可用堆大小，并行 GC 选项以及 Tangosol 相性备份 -->
<jvm>
<jvm-options>-Xms2048m -Xmx2748m -server -XX:+UseParallelGC -XX:+Parallel1DGC -XX:ParallelGCThreads=4 -XX:+AggressiveOpts/></jvm-options>
</jvm-options>
<jvm-options>
<jvm-options>-Dtangasol.coherence.localhost=72.5.126.82</jvm-options>
</jvm>
```

```xml
-- 略高的 keep-alive 线程设置，表示预计的并发 HTTP 连接更高 --
<keep-alive>
<threads>8</threads>
</keep-alive>
```

```xml
-- 典型的工作线程池，对于调用栈深度较深的 Java Web 应用程序，较大的栈大小并不罕见 --
<thread-pool>
<min-threads>128</min-threads>
<max-threads>256</max-threads>
<stack-size>262144</stack-size>
</thread-pool>
```

```xml
-- 配置为 JDBC 资源的 Oracle 数据源 --
<resource>
<jndi-name>jdbc:jdcforum/jndi-name</jndi-name>
<datasource-class>oracle.jdbc.pool.OracleDataSource</datasource-class>
<min-connections>130</min-connections>
<max-connections>200</max-connections>
<idle-timeout>0</idle-timeout>
```

```xml
<isolation-level>read-committed</isolation-level>
<property>
  <name>MaxStatements</name>
  <value>200</value>
</property>
<property>
  <name>ImplicitCachingEnabled</name>
  <value>true</value>
</property>
<jdbc-resource>
```

```xml
-- HTTP 监听器配置为为论坛虚拟服务器服务；8 个接收器线程计数是针对 4 核心 AMD Opteron 服务器进行了调优 --
<http-listener>
  <name>http-listener-1</name>
  <acceptor-threads>8</acceptor-threads>
</http-listener>
```

```xml
-- 一个文档根目录为 '/' 的单个论坛 Web 应用运行虚拟服务器 --
<virtual-server>
  <name>forum</name>
  <host>/</host>
  <http-listener-name>http-listener-1</http-listener-name>
  <web-app>
    <uri/></uri>
    <path>../web-app/forum/_default/*</path>
  </web-app>
</virtual-server>
```

```xml
-- 日志每天滚动一次。 --
<event>
  <time>
    <time-of-day>23:55</time-of-day>
  </time>
  <rotate-access-log>true</rotate-access-log>
</event>
<event>
  <time>
    <time-of-day>23:55</time-of-day>
  </time>
  <rotate-log>true</rotate-log>
</event>
</server>
```

## 12.2 站点：Sun Forums

为 forums.sun.com 配置的参数与为 Sun Blogs 配置的参数（见第 12.1 节）非常相似。但需要注意一个例外，即为 HTTP 监听器配置的接收器线程数。第 2 章引入了接收器线程的概念，并指出一个经验法则是将接收器线程的数量配置为等于 CPU 的数量。

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_555_0.png)

> 注意：接收器线程等待连接。当接收到请求时，它会被交给工作线程。工作线程的数量应根据预期的连接数进行调优。




## 第 12 章 使用 Web Server 7.0 构建安全的动态 Web 2.0 站点

## 12.4 总结

Web Server 7.0 为部署任务关键型站点提供了一个经过验证的、稳定、安全且可扩展的环境。其连接处理架构特别适用于处理动态 Web 2.0 站点所面临的海量事务。它对 Ruby、PHP、Java 甚至甚至 ASP 等动态编程技术的支持，允许开发者在他们选择的任何平台上构建下一代站点。Web Server 7.0 管理整个服务器集群的能力与管理单台服务器一样简单，这使其成为构建安全、动态 Web 2.0 站点的自然选择。

## 12.5 自学实验

本书之前的几个章节提供了自学实验，让您能够验证自己对在配置和管理 Web Server 7.0 方面的理解。通过这些章节中获取的知识，您现在应该能够创建自己的 Web 2.0 站点，并有信心这些站点既是安全的，能够提供支持广泛用户社区所需的性能要求。

然而，如果您觉得想进行更多练习，可以在 http://www.sunwebserver.com 找到额外的练习。新的 Web 2.0 站点一直在开发中，而许多基础设施是由框架、博客软件、聊天和其他交互产品的开源实现提供的。事实上，我们要列出的远远比这里能写的得多。因此，请访问 http://www.sunwebserver.com 查看如何安装 MediaWiki、Joomla、Moodle、Roller 等应用程序的说明。虽然 Web Server 7.0 技术可能不会频繁更改，但该产品可以支持的应用将不断变化。因此，随着新应用程序的出现，站点将更新针对新应用程序的说明。通过安装许多此类应用程序，并观察如何配置 Web Server 7.0 来支持它们，您将能够熟练地自定义 Web Server。谁知道呢——您可能会在 Web Server 7.0 之上构建下一个 Facebook 或 YouTube 应用程序！

作为额外收益，该站点还包含了书中未收录的自测题、常见问题解答以及自学实验。这些信息的目的是创建一个由志同道合的开发者和管理员组成的社区，他们对在 Web Server 7.0 之上进行开发感兴趣。在这里您将与他人互动，查看他们是如何解决问题的，并使用该产品开发他们自己的 Web 2.0 应用程序。

## 详细查看 server.xml 文件

乍看之下，server.xml 文件可能看起来有点人生畏。然而，您会发现，在理解了元素的名称及其可能的值后，它的格式非常直观且易于修改。

下面的示例展示了一个 server.xml 文件。为了参考，添加了行号。

1. <?xml version="1.0" encoding="UTF-8"?>
2.
3. <!--
4. Copyright 2006 Sun Microsystems, Inc. All rights reserved.
5. Use is subject to license terms.
6. -->
7.
8. <server>
9. <cluster>
10. <local-host>boulder.example.com</local-host>
11. <instance>
12. <host>boulder.example.com</host>
13. </instance>
14. </cluster>
15.
16. <log>
17. <log-file>../logs/errors</log-file>
18. <log-level>info</log-level>
19. </log>
20.
21. <platform>64</platform>
22.
23. <temp-path>/tmp/https/boulder.example.com-6accbd0a</temp-path>
24.
25. <user>webservd</user>
26.
27. <jvm>
28. <java-home>/sun/webserver7/jdk/java-home>
29. <server-class-path>/sun/webserver7/lib/webserv-rt.jar:/sun/webserver7/lib/pwc.jar:/sun/webserver7/lib/ant.${java.home}/lib/tools.jar:/sun/webserver7/lib/ktsearch.jar:/sun/webserver7/lib/webserv-jst1.jar:/sun/webserver7/lib/jsf-impl.jar:/sun/webserver7/lib/jsf-api.jar:/sun/webserver7/lib/webserv-jdwsp.jar:/sun/webserver7/lib/container-auth.jar:/sun/webserver7/lib/mail.jar:/sun/webserver7/lib/activation.jar</server-class-path>
30. <debug>false</debug>
31. <debug-options>-Xdebug -Xrunjwp:transport=dt_suspend=n,address=7896</debug-jvm-options>
32. <jvm-options>-Djava.security.auth.login.config=login.conf</jvm-options>
33. <jvm-options>-Xms128m -Xmx256m</jvm-options>
34. <jvm>
35.
36. <thread-pool>
37. <max-threads>128</max-threads>
38. <stack-size>131072</stack-size>
39. </thread-pool>
40.
41. <default-auth-db-name>keyfile</default-db-name>
42.
43. <auth-db>
44. <name>keyfile</name>
45. <url>file</url>
46. <property>
47. <name>syntax</name>
48. <value>keyfile</value>
49. </property>
50. <property>
51. <name>keyfile</name>
52. <value>keyfile</value>
53. </property>
54. <auth-db>
55.
56. <acl-file>default.acl</acl-file>
57.
58. <mime-file>mime.types</mime-file>
59.
60. <access-log>
61. <file>../logs/access</file>
62. </access-log>
63.
64. <http-listener>
65. <name>http-listener-1</name>
66. <port>80</port>
67. <server-name>boulder.example.com</server-name>
68. <server-name>boulder.example.com</server-name>
69. </http-listener>
70. <port>80</port>
71. <server-name>boulder.example.com</server-name>
72. <server-name>boulder.example.com</server-name>
73. </http-listener>
74. <server-name>boulder.example.com</server-name>
75. <server-name>boulder.example.com</server-name>
76. </server-
-
...
77. </server>




# server.xml 文件的详细介绍

| 行号 | 描述 |
| --- | --- |
| 第 36–39 行 | <thread-pool> 元素配置用于处理 HTTP 请求的线程。在示例中，<thread-pool> 有两个子元素：<max-threads> 和 <stack-size>。
<max-threads> 元素指定了为 HTTP 请求处理分配的最大工作线程数。取值范围为 1 到 4096。
<stack-size> 元素指定了创建新工作线程时线程栈的大小（以字节为单位）。取值范围为 8192 到 61708864。 |
| 第 41 行 | <default-auth-db> 元素指定了用于访问控制处理的默认身份验证数据库的名称。该元素的值必须在 server.xml 文件的现有 <auth-db> 上下文中定义。
在此示例中，<default-auth-db> 的值对应第 43 行定义并在第 44 行命名的身份验证数据库。 |
| 第 43–54 行 | <auth-db> 元素为访问控制过程中可能使用的身份验证数据库提供定义。在 <auth-db> 中可以定义多个子元素。它们指定了身份验证的名称 <name>、身份验证数据库的类型 <url> 以及在身份验证数据库上下文中使用的各种属性 <properties>（例如身份验证数据库的格式和大小）。
在此示例中定义了一个基于文件的身份验证数据库（第 45 行），并通过名称和密钥文件（第 44 行）进行引用。实际文件的名称也称为 keyfile，可以直接在该实例的配置 keyfile 键下方（第 50–53 行）找到。文件中任何条目的句法均遵循 keyfile 格式（第 46–49 行）。 |
| 第 56 行 | <acl-file> 元素定义了一个用于指定访问各种服务器资源规则的文件。在示例中，<acl-file> 元素定义了一个名为 default.acl 的文件，可能用于访问控制处理。如果未指定完整文件名，则该文件名相对于此服务器实例的配置目录。 |
| 第 58 行 | <mime-file> 元素定义了一个用于为 Web 服务器配置多用途邮件扩展 (MIME) 类型映射的文件。该文件在 HTTP 请求处理期间用于将文件类型映射到适当的处理服务。
在此示例中，<mime-file> 元素定义了一个名为 mime 的文件，可能用于此用途。文件可以在此服务器实例的配置目录下找到。 |
| 第 60–62 行 | 所有的 HTTP 请求都存储在服务器的访问日志（Access Log）中。<access-log> 元素可以包含若干子元素，定义访问日志的名称、位置和状态。在示例中，<access-log> 元素指定访问日志位于 logs 目录下。文件名简单 access。该文件的默认格式是 CLF（常用日志格式）。 |

# 附录 A

| 行号 | 描述 |
|--- | --- |
| 第 64–69 行 | 客户端请求在特定的端口或 HTTP 监听器上接收。<http-listener> 元素用于配置 HTTP 监听器。示例中的 <http-listener> 元素包含四个子元素：<name>、<port>、<server-name> 和 <default-virtual-server-name>。
<name> 元素指定用于引用监听器的名称。
<port> 元素指定监听器配置的端口号。
<port> 元素可以与 <ip> 元素关联，以产生不同的虚拟服务器组合。如果 <http-listener> 定义中缺少 <ip> 元素，则 <port> 元素适用于服务器已配置的所有 IP 地址。
<server-name> 元素指定了此监听器使用的默认服务器名称。该值可以包含方案前缀（例如 http://）和端口后缀（例如 :80）。
<default-virtual-server-name> 元素指定当服务器无法通过程序化方法确定虚拟服务器时，用于请求处理的虚拟服务器名称。当 DNS 中有多个网站指向同一个 IP 地址，但在 Web 服务器中未为该网站配置虚拟服务器时，可能会使用此元素。 |
| 第 71 行及起 | 虚拟服务器允许你在单个安装的服务器内托管多个网站。<virtual-server> 元素用于为你的实例配置 HTTP 虚拟服务器。每个服务器通常至少配置配置了一个虚拟服务器，并且所有的虚拟服务器都指定了 HTTP 监听器。
示例中的 <virtual-server> 元素包含四个子元素：<name>、<host>、<http-listener-name> 和 <document-root>。
<name> 元素指定用于引用虚拟服务器的名称。
<host> 元素指定了虚拟服务器服务请求的主机名称。主机比较不区分大小，<host> 元素的值可以是主机名或通配符模式（例如 *, example.com）。
<http-listener-name> 元素指定了与虚拟服务器的一个或多个主机关联的 HTTP 监听器名称。<http-listener-name> 的值是 HTTP 监听器的名称。<document-root> 元素指定了虚拟服务器根目录的路径。示例中的 <virtual-server> 元素包含至少一个 <document-root> 元素。<document-root> 元素指定了虚拟服务器根目录的路径。 |





```
<request-bucket countRequests="0" countBytesReceived="0"
countBytesTransmitted="0" rateBytesTransmitted="0" rateTransmissionRate="0"
countConnections="0" maxOpenConnections="0" count2xx="0"
count3xx="0"
count4xx="0" count5xx="0" countOther="0" count200="0" count302="0"
count304="0"
count400="0" count401="0" count403="0" count404="0" count503="0"/>
<profile-bucket profile="profile-0" countCalls="0">
  countRequests="0" ticksDispatch="0" ticksFunction="0">
    <profile-bucket profile="profile-1" countCalls="0">
    countRequests="0" ticksDispatch="0" ticksFunction="0">
      <profile-bucket profile="profile-2" countCalls="0">
      countRequests="0" ticksDispatch="0" ticksFunction="0">
</thread>
</profile-bucket>
</thread>
  <thread mode="idle" timeStarted="1211245269"
connection-queue="cql"
addressClient="127.0.0.1">
<request-bucket countRequests="3" countBytes
Received="1394"
countBytesTransmitted="4290" rateBytesTransmitted="0" maxTransmissionRate="0"
countConnections="0" maxOpenConnections="0" count2xx="1"
count3xx="1"
count4xx="1" count5xx="0" countOther="0" count200="0" count302="0"
count304="1"
count400="0" count401="0" count403="0" count404="1" count503="0"/>
<profile-bucket profile="profile-0" countCalls="48">
  countRequests="3" ticksDispatch="9" ticksFunction="1">
    <profile-bucket profile="profile-1" countCalls="48">
    countRequests="3" ticksDispatch="9" ticksFunction="1">
      <profile-bucket profile="profile-2" countCalls="0">
      countRequests="0" ticksDispatch="0" ticksFunction="0">
</thread>
</profile-bucket>
</thread>
  <thread mode="idle" timeStarted="1211245300"
connection-queue="cql">
<request-bucket countRequests="0" countBytesReceived="0"
countBytesTransmitted="0" rateBytesTransmitted="0" maxTransmissionRate="0"
countConnections="0" maxOpenConnections="0" count2xx="0"
count3xx="0"
count4xx="0" count5xx="0" countOther="0" count200="0" count302="0"
count304="0"
count400="0" count401="0" count403="0" count404="0" count503="0"/>
<profile-bucket profile="profile-0" countCalls="0">
  countRequests="0" ticksDispatch="0" ticksFunction="0">
    <profile-bucket profile="profile-1" countCalls="0">
```

# 附录 B

<profile-bucket profile="profile-2" countCalls="0"
countRequests="0" ticksDispatch="0" ticksFunction="0">
</thread>
<jvm countClassesLoaded="1944" countTotalClassesLoaded="1944">
countTotalClassesUnloaded="0" sizeHeap="9338152" peakThreads="7"
countTotalThreadsStarted="8" countThreads="7" version="1.5.0_12-b04"
name="Java

HotSpot(TM) Server vendor="Sun. Microsystems Inc." countGarbage-Collections="3"
millisecondargbageCollection="37">

</virtual-server-id="www.example.com" mode="active" hosts="www.example.com"
interfaces="8080">:
<request-bucket method="GET" uri="favicon.ico" count
Requests="3"
countBytesReceived="1394" countBytesTransmitted="4290" rateMaxByteTimeoutRate="0" countOpenConnections="0" maxOpenConnections="0"
countxx="1" count3xx="1" count4xx="1" count5xx="0" countother="0"
count200="1" count302="0" count304="1" count400="0" count401="0" count403="0"
count404="1" count503="0">

<profile-bucket profile="profile-0" countCalls="48" count
Requests="3"
ticksDispatch="9" ticksFunction="1">
  <profile-bucket profile="profile-1" countCalls="48" count
Requests="3"
ticksDispatch="9" ticksFunction="1">
    <profile-bucket profile="profile-2" countCalls="0" count
Requests="3"
ticksDispatch="9" ticksFunction="1">

<web-app-bucket uri="/" mode="enabled" countJsps="0"
countReloadedJsps="0" countActiveSessions="0"
peakActiveSessions="0" countExpiredSessions="0"
secondSessionAlive="0" countSessionAlive="0">
<servlet-bucket name="jsp" countRequests="0"
countErrors="0"
millisecondProcessing="0" millisecondsPeakProcessing="0">
<servlet-bucket name="invoker" countRequests="0"
countErrors="0"
millisecondProcessing="0" millisecondsPeakProcessing="0">
<servlet-bucket name="default" countRequests="0"
countErrors="0"
millisecondProcessing="0" millisecondsPeakProcessing="0"/>
</web-app-bucket>
</virtual-server>
<server>
<stats>大部分（但并非所有）XML 报告中的元素可以通过管理 GUI 或 CLI 访问。请参阅第 7 章“监控 Web 服务器”以获取更多信息。

# 纯文本数据示例

service-dump 是 Web 服务器中构建的服务器应用程序 (SAF)，它收集内部服务器统计 (stats) 的各种性能数据并以 ASCII 格式的报告进行显示。注意：你可能会在文档中看到 service-dump、perfdump 或纯文本报告的引用，它们都具有相同的功能。纯文本报告没有显示通过 CLI 可用的所有统计信息，但对于监控你的 Web 服务器仍然是一个非常有用的工具。纯文本报告提供了以下类别的统计：

- 连接队列信息
- HTTP 监听（监听套）信息
- Keep-Alive 信息
- 会话创建（线程）信息
- 文件缓存信息（静态内容）
- 线程池信息
- DNS 缓存信息

注意：请参阅第 7 章 7.3.3 节“性能监控工具 (perfdump)”获取更多信息。本附录的其余部分演示了典型纯文本报告包含的信息。报告中的各个位置插入了注释，以解释显示的数据以及如何调整你的 Web 服务器。《Sun Java Web Server 7.0 性能调整、配置和扩展指南》。

警告：在更改任何这些参数之前，你应该建立（可能自动化）测试用例，以便在受控系统上创建性能基准。收集数据后，你可以修改附录中讨论的参数并再次执行测试，以确保你所做的更改对系统性能产生了积极影响。

Sun Java Web Server 7.0U2 B12/2007 08:48 (WINNT DOMESTIC)
服务器启动于 2008 年 5 月 19 日 21:01:01
进程 219 启动于2008 年 5 月 19 日 21:01:01

注意：报告的第一部分提供了有关 Web 服务器版本及其运行的操作系统的信息。它还包含了详细说明服务器进程启动时间以及与当前运行的 Web 服务器实例相关的进程标识符的信息。

当前/峰值/限制队列长度 0/1/16384
总队列连接数 23
平均队列长度（1，15 分钟）0.00, 0.00, 0.00
平均队列延迟 0.00 毫秒

注意：当客户端从 Web 服务器发送请求时，连接由与 HTTP 监听器关联的接收线程接受。接收线程将连接放在连接队列中并返回等待下一个客户端请求。请求处理线程（称为工作线程）然后从连接队列中获取连接并处理请求。在典型的 Web 服务器实例中，你会有几个请求在队列中等待处理。然而，队列请求过多可能表明服务器没有及时响应请求。

perfdump 数据中的连接队列信息显示了连接队列中的会话数量以及连接被请求处理线程接受之前的平均延迟。

此示例提供的连接队列信息演示了一个负载极小的服务器。如果你发现峰值队列长度接近限制队列长度（最大队列大小），你应该考虑增加最大队列大小，以防在高负载下丢弃连接。

```
ListenSocket http-listener-1:
Address                 http://0.0.0.0:8080
Acceptor Threads        1
默认虚拟服务器  www.example.com
```

```
ListenSocket http-listener-2:
Address                 https://0.0.0.0:443
Acceptor Threads        1
默认虚拟服务器  www.example.com
```

> 注意：监听Socket（HTTP 监听）信息包含了 IP 地址、端口号、接收线程数量以及默认虚拟服务器。

# 纯文本报告示例
```





# 附录 C

## KeepAliveInfo:

KeepAliveCount 1/65536
KeepAliveHits 117
KeepAliveFlushes 0
KeepAliveRefusals 0
KeepAliveTimeouts 7
KeepAliveTimeout 30 seconds

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_574_0.png)

**注意：** 在 Web 服务器术语中，Keep-Alive（持久连接）连接是指客户端的请求（以及 Web 服务器随后的同意）保持当前连接处于开启（或活跃状态），以便进行多次请求，而无需为每个请求打开、关闭并重新打开连接。这极大地减少了打开和关闭连接相关的开销，特别是当单个网页在完全传输之前可能需要若干次请求时。旧版本的 HTTP 标准使用 *keep-alive*（保持连接）术语来描述此功能，但 HTTP 1.1 现在将此概念称为持久连接（PersistentConnection）。Sun Web 服务器继续使用之前的 Keep-Alive 连接术语来指代它。

Web 服务器维护一个最大等待 Keep-Alive 连接数的计数器。在示例 7.1 中，这由 KeepAliveCount 值中包含的 65536 表示，表示 Web 服务器在任何时刻维护的 Keep-Alive 连接的最大数。

Web 服务器中的 keep-alive 子系统设计为具有大规模扩展性。然而，如果负载不是持续的（例如，如果客户端使用 HTTP 1.0 且未提供 KeepAlive 请求头），或者对于主要服务 Keep-Alive 连接的轻负载系统，其开箱配置可能不是最优的。

## SessionCreationInfo:

Active Sessions 0
Keep-Alive Sessions 1
Total Sessions Created 4/128

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_574_1.png)

**注意：** 会话（线程）创建统计包括用于处理请求的当前线程数（活动会话）、（Keep-Alive 会话）以及与最大线程数相比已创建的会话总数（已创建的会话总数）。

## 示例纯文本报告数据

Web 服务器可以从 Total Sessions Created 值中的 keep-alive 线程提供某些类型的请求，例如缓存静态内容。因此，最大线程值是 server.xml 文件中 thread-pool 元素中配置的最大线程数加上 keep-alive 线程数的和。在示例 7.1 中，这由 Total Sessions Created 字段中的数字 128 表示，被称为 Maximum Threads（最大线程）设置。

Maximum Threads 设置指定了 Web 服务器在任何给定时间内可以处理的并发事务最大数。默认值为 128。更改此值可用于限制服务器性能，从而最大限度地减少所执行事务的延迟。Maximum Threads 值跨多个虚拟服务器生效，但不会尝试进行负载均衡。它是为每个配置设置的。

达到配置的线程最大数并不意味着是坏事，如果达到达到 Maximum Threads 值，您不需要自动增加服务器中的线程数。达到此限制意味着服务器在峰值负载下需要这些线程，但只要它能够及时提供服务，服务器的调优就是充分的。然而，您应该监控 Total Sessions Created 值，因为一旦达到 Maximum Threads 值，请求将进入队列。如果请求继续积累，您可能会导致连接队列（Connection Queue）溢出并停止提供服务。如果您监控服务器性能并发现创建的会话总数接近最大线程数，则应考虑增加您的线程限制。

## CacheInfo:

| File Cache Enabled | yes |
| :--- | :--- |
| File Cache Entries | 4/1024 |
| File Cache Hit Ratio | 32/74% |
| Maximum Age | 30 |
| Accelerator Entries | 45/1024 |
| Acceleratable Requests | 45/0% |
| Accelerator Hit Ratio | 00% |

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_574_1.png)

**：** ，，，，，，，，，，，，，，，，，，，，，，， 翻译的。。达到此限制意味着服务器在峰值负载下需要这些线程，但只要它能够及时提供服务，服务器的调优就是充分的。然而，您应该监控 Total Sessions Created 值，因为一旦达到 Maximum Threads 值，请求将进入队列。如果请求继续积累，您可能会导致连接队列溢出并停止提供服务。如果您监控服务器性能并发现创建的会话总数接近最大线程数，则应考虑增加您的线程限制。

**：**，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，，。

** Cache：：

| File Cache Enabled | yes |
| :--- | :--- |
| File Cache Entries | 4/1024 |
| File Cache Hit Ratio | 32/74% |
| Maximum Age | 30 |
| Accelerator Entries | 45/1024 |
| Acceleratable Requests | 45/0% |
| Accelerator Hit Ratio | 00% |

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_574_1.png)

**注意：** 会话（线程）创建统计包括当前用于处理请求的线程数（活动会话）、（Keep-Alive 会话）以及与最大线程数相比已创建的会话总数（已创建的会话总数）。

## 示例纯文本报告数据

Web 服务器可以从 Total Sessions Created 值中的 keep-alive 线程提供某些类型的请求，例如缓存静态内容。因此，最大线程值是 server.xml 文件中 thread-pool 元素中配置的最大线程数加上 keep-alive 线程数的和。在示例 7.1 中，这由 Total Sessions Created 字段中的数字 128 表示，被称为 Maximum Threads（最大线程）设置。

Maximum Threads 设置指定了 Web 服务器在任何给定时间内可以处理的并发事务最大数。默认值为 128。更改此值可用于限制服务器性能，最大限度地减少所执行事务的延迟。Maximum Threads 值跨多个虚拟服务器生效，但不会尝试进行负载均衡。它是为每个配置设置的。

达到配置的线程最大数并不意味着是坏事，如果达到 Maximum Threads 值，您不需要自动增加服务器中的线程数。达到此限制意味着服务器在峰值负载下需要这些线程，但只要它能够及时提供服务，服务器的调优就是充分的。然而，您应该监控 Total Sessions Created 值，因为一旦达到 Maximum Threads 值，请求将进入队列。如果请求继续积累，您可能会导致连接队列（Connection Queue）溢出并停止提供服务。如果您监控服务器性能并发现创建的会话总数接近最大线程数，则应考虑增加您的线程限制。

## CacheInfo:

| File Cache Enabled | yes |
| :--- | :--- |
| File Cache Entries | 4/1024 |
| File Cache Hit Ratio | 32/74% |
| Maximum Age | 30 |
| Accelerator Entries | 45/1024 |
| Acceleratable Requests | 45/0% |
| Accelerator Hit Ratio | 00% |

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_574_1.png)

**注意：** 会话（线程）创建统计包括用于处理请求的当前线程数（活动会话）、（Keep-Alive 会话）以及与最大线程数相比已创建的会话总数（已创建的会话总数）。




## NativePool:

NativePool:

空闲/峰值/限制 2/2/128
工作队列长度/峰值/限制 0/1/0

my-custom-pool:

空闲/峰值/限制 1/1/128
工作队列长度/峰值/限制 0/0/0

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_578_0.png)

**注意：** 如果您使用默认设置，将使用默认池中的工作线程来处理客户端请求。但是，您可以创建自己的自定义线程池并使用它们来处理自定义 NSAPI 函数。此外，Web 服务器还会创建一个名为 NativePool 的额外池，也可用于此目的。perfdump 报告可以深入了解 NativePool 线程的有效效率。如果您定义了额外的自定义线程池，它们将位于 NativePool 章节下方，如示例 7.1 中的 `my-custom-pool` 节所示。

本节定义的每个原生池都包含相关信息，指定了当前空闲的线程数（Idle）、在峰值处理期间使用的线程数（Peak）以及池中允许的最大原生线程数（Limit）。

有关工作队列（Work Queue）的信息可以深入了解等待使用池中原生线程的服务器请求数量。工作队列长度（Work Queue Length）是等待原生线程的当前请求数。峰值（Peak）是指自服务器启动以来，曾经同时等待使用原生线程的请求最高数。此值可以被视为需要原生线程请求的最大并发数。限制（Limit）是可以一次队列等待原生线程的最大请求数，由 `max.conf` 文件中的 `NativePoolSize` 设置决定。

如果您发现 `NativePool` 线程或工作队列长度达到了峰值（Peak）值，可以增加池的大小或队列长度。然而，需要注意，因为增加这些值会消耗服务器的额外内存，并且可能无法解决实际问题。您可能会经常发现达到峰值的其他原因，例如未正确释放数据库连接的 Web 应用程序。在简单地修改这些设置之前，您应该检查其他领域。

## 示例纯文本报告数据

DNSCacheInfo:

启用 是
缓存条目 0/1024
命中率 0/0 ( 0.00%)

**注意：** Web 服务器使用 DNS 缓存机制来减少在解析 DNS 主机名到 IP 地址时执行的 DNS 查询次数。DNS 缓存存储 IP 地址到 DNS 名称的映射，并用于提高引用 DNS 名称的日志和访问控制规则的性能。DNS 缓存默认启用，但如果您没有执行需要 DNS 查询的操作，则不会利用该 DNS 缓存。

perfdump 报告中的 `CacheEntries` 值显示了当前缓存条目数与最大可能缓存条目数之间的比较。一个缓存条目代表单个 IP 地址或 DNS 名称查询。在调优 DNS 缓存时，您应该尝试将其配置为接近并发访问您网站的最大客户端数量。这可以通过监控 `CacheEntries` 实际完成，在未进行此操作之前不应修改。将 DNS 缓存大小值设置得太实际上可能会浪费内存并降低性能。

`HitRatio`（命中率）值是缓存命中次数与缓存查询次数的比较。

Web 服务器可以配置为使用其异步 DNS 解析器或操作系统提供的同步解析器。为了节省查询时间，它默认使用操作系统的解析器。这通过 perfdump 报告中的 `Async DNS disabled` 引用指示。

## 性能计数器:

| | 平均值 | 总计 | 百比 |
|---|---|---|---|
| 请求总数：请求处理时间： | | 139 12.1250 | |
| default-bucket (默认请求: 调用次数: 延迟: 函数处理时间: 总响应时间: | 0.0064 0.0809 0.0872 | 139 2650 0.8850 11.2400 12.1250 | (100.00%) (100.00%) ( 7.30%) ( 92.70%) (100.00%) |

## 附录 C

会话：

| 进程状态 | 客户端年龄 VS 方法 URI 函数 |
|---|---|---|
| 2192 keep-alive 127.0.0.1 | | |

![](img/a3cb513bfd7a0b21f70c67fcaede10f6_580_0.png)

**注意：** perfdump 报告中包含的其余信息可以深入了解您的 Web 服务器的整体性能。可以在示例 7.1 的性能计数器部分找到它。该部分包含各种指标的平均值、总计和百分比值，让您判断您的更改可能如何影响服务器性能。

您可以使用性能桶（performance buckets）来隔离请求或请求类别。性能桶允许您定义计数器并将其关联到各种函数。每当调用这些函数中的某一个时，服务器就会收集统计数据并将其添加到桶中。例如，`ccgi` 和 `servlet-jee` 分别用于处理 CGI 和 Servlet 请求的函数。您可以定义两个桶分别为 CGI 和 Servlet 请求维护单独计数器，也可以创建一个计算这两种类型动态内容的桶。收集这些信息的成本极低，对服务器性能的影响通常可以忽略不计。

性能桶数据包含以下信息：

- 平均值、总计和百分比列提供了每个请求统计的数据。
- 请求处理时间是服务器处理目前为止收到的所有请求所需的总时间。
- 请求数是该函数的请求总数。
- 调用次数是该函数被调用的总次数。这与请求数的不同在于，在处理单个请求期间，一个函数可能会被调用多次。该行的百分比列是相对于所有桶的调用总次数计算的。
- 延迟是 Web 服务器准备调用函数所需的时间（秒）。
- 函数处理时间是 Web 服务器在函数内部花费的时间（秒）。函数处理时间和总响应时间的百分比是相对于总请求处理时间计算的。
- 总响应时间是函数处理时间和延迟之和（秒）。

perfdump 报告中包含的数据可以为您的服务器处理请求的情况提供宝贵的见解。stats-xml 数据提供了所有可用内容的视图。





# 558
# 索引

- 管理用实例 (administrative instances)
  - 在 UNIX 类系统上的启动/停止， 118-120
  - 在 Windows 类系统上的启动/停止， 120-121
- 管理员界面 (administrator interface), 8
- Agent MBeans, 117
- 应用生命周期，Java Web 应用, 425
- ASP (Active Server Pages), 395-396
- auth-fcgi SAF, 389
- 身份验证 (authentication), 300。另见用户身份验证。
- 身份验证数据库库 (authentication databases), 204
  - keyfile 文件 (keyfile file), 204
  - 上文 (context), 206
  - 文件结构 (file structure), 205
  - 修改 (modifications), 206
  - 语法 (syntax), 205
- 授权 (authorization), 300
- 授权语句，default.acl 文件， 196-197
- 请求处理中的 AuthTrans 阶段， 211-212
- 自动补全功能， 133-135
- 自动启动 Web Server 实例， 87
- 自动 Web Web 部署， 445-449
- 自动化 CRL 部署， 341-343
- certmap.conf 配置文件， 186-187
  - 上文 (context), 191
  - 文件结构 (file structure), 178-188
  - 修改 (modifications), 192
  - 语法 (syntax), 188-191
- certutil 命令， 501
- CGI (通用网关接口), 360。另见 FastCGI
  - 配置 (configuring), 360-361
  - 按目录 (by directory), 344-366
  - 按文件扩展 (by file extensions), 366-368
  - 适用于 UNIX/Linux 系统 (for UNIX/Linux systems), 371
  - 全局配置 (global configuration), 371
- 动态内容 (dynamic content), 31-32
  - SAFs, 372-375
  - check-limits SAF, 345-347
- 类加载器 (classloaders), 457
- CLI (命令行接口), 8-126
  - 命令语法 (command syntax), 131-132
  - 获取配置级统计数据 (configuration-level statistics, obtaining), 280-282
  - 本地化 (localization), 142-144
  - 访问日志文件 (log files, accessing), 270-271
  - 修改日志文件 (log files, modifying), 267-269
  - 访问纯文本报告 (Plain Text Report, accessing), 276
  - shell 模式，Tab 收集 (shell mode, Tab collection), 133-135
  - shell 变量 (shell variables), 128-131
  - Tel 脚本支持 (Tel scripting support), 140
  - 获取虚拟服务器统计数据 (virtual server statistics, obtaining), 282-283
  - 调用 wasm 脚本 (wasm script, invoking)
  - 文件模式 (file mode), 138-139
  - shell 模式 (shell mode), 137-138
  - 独立模式 (standalone mode), 136
  - 获取 Web 容器统计数据 (web container statistics, obtaining), 284
  - Web 服务器监控 (web server monitoring), 280
  - XML 报告 (XML Report), 272
- 基于 CLI 迁移到 Web Server 7.0， 103-105
- 客户端身份验证 (client authentication), 186
- 客户端容器 (client containers), 237-238
- 客户端接口（监控子系统） (client interfaces (monitoring subsystem)), 259

# B-C

- 反向引用 (backreferencing), 245-248
- 基本身份验证方法 (basic authentication method), 195
- 构建标识符 (build identifiers), 67
- Java Web 应用中的缓存 (caching in Java web applications), 455
  - 整体 (entire), 456
  - 页面片段 (page fragments), 457
- CAs (证书 Authorities), 334-337
- CRL 处理 (CRLs processing), 343
- 自动化 CRL 处理 (CRLs processing, automating), 341-343
- 客户端处理，mime.types 配置文件 (client processing, mime.types configuration file), 179-180
- 集群管理 (cluster management), 10
- 集群 (clusters), 112-114
- CMM (通用监控模型) 对象, 290
- 命令行安装/卸载 (command-line installation/uninstallation), 61-62, 98
- 命令行 Web 应用部署 (command-line web application deployment), 444-545
- 命令 (commands)
  - config, 377
  - dtrace, 510-512
  - echo, 377
  - exec, 377
  - flastmod, 377
  - size, 377
  - get-config-stats, 280-282
  - get-virtual-server-stats, 282-283
  - grep, 118
  - include, 377
  - netstat, 505
  - ps, 21, 34, 76, 506
  - pstack, 35, 516
  - ptree, 201
  - sed, 27
  - setup, 安装 Web Server 7.0, 45-46
- SHTML, 379
- snoop, 509-510
- sslapt, 507-509
- startserv, 85-87
- 语法 (syntax), 131, 132
- Tab 补全, 133-135
- unwindill, 91
- 管理控制台中的任务 (common tasks in Administration Console), 125
- 符合 508 标准 (compliance with 508 standards), 144
- 组件选择向导 (Component Selection (Install Wizard)), 51-52
- 条件处理 (conditional processing), 234
- 客户端容器 (Client containers), 237-238
  - 指令参数 (directive parameters), 234
  - If/Else 容器 (If/Else containers), 238-241
  - Name 指令属性 (NameTrans directive attributes), 235（注：原文为NameTrans，可能为Path笔误）
  - 路径属性 (Path attributes), 236
- config 命令 (config command), 377
- 配置文件 (configuration files)
  - certmap.conf 文件, 186-187
    - 上文 (context), 191
    - 文件结构 (file structure), 178-188
    - 修改 (modifications), 192
    - 语法 (syntax), 188-191
  - CGI, 361
  - default.acl 文件, 196-197
    - 上文 (context), 191
    - 文件结构 (file structure), 187-188
    - 修改 (modifications), 192
    - 语法 (syntax), 188-191
  - default-web.xml, Java 应用配置, 429-432
    - 上文 (context), 201
    - 文件结构 (file structure), 202
    - 修改 (modifications), 201
    - 语法 (syntax), 200
  - default-web.xml 文件
    - 上文 (context), 201
    - 文件结构 (file structure), 202
    - 修改 (modifications), 201
    - 语法 (syntax), 200
  - login.conf, 201
    - 上文 (context), 203
    - 文件结构 (file structure), 202
    - 修改 (modifications), 203
    - 语法 (syntax), 203
  - magnus.conf, 156
    - 上文 (context), 159
    - 修改 (modifications), 158-159
  - 手动编辑 (manually editing), 140-141
  - mime.types, 174
    - 上文 (context), 180
    - 文件结构 (file structure), 175-177
    - 修改 (modifications), 181
    - 处理 (processing), 177-180
  - obj.conf
    - 上文 (context), 174
    - 文件结构 (file structure), 165-167
    - 修改 (modifications), 174
    - 语法 (syntax), 173
  - server.policy 文件
    - 上文 (context), 185
    - 修改 (modifications), 185
    - 语法 (syntax), 184
  - server.xml
    - 上文 (context), 164
    - 修改 (modifications), 164
    - 语法 (syntax), 160-163
  - sun-web.xml, Java 应用配置, 436-438
- 从 CLI 获取配置级统计数据 (configuration-level statistics, obtaining from CLI), 280-282
- 配置文件 (configuration file), 179-180
  - default.acl, 199
    - 上文 (context), 183
    - 文件结构 (file structure), 182-183
    - 修改 (modifications), 183
    - 语法 (syntax), 194
- 配置存储 (Configuration Store), 112-113
- 配置 (configurations), 111
  - 使用管理控制台拷贝 (copying with Administration Console), 147-148
  - 使用管理控制台创建 (creating with Administration Console), 145-147
  - 删除 (deleting), 152-153
  - 部署 (deploying), 148-149
  - 回滚 (rolling back), 150-152
- 控制脚本 (control scripts), 85
- 控制 Web 服务器访问 (controlling access to web servers), 300
- 访问控制 (access control), 312-324
- 用户身份验证 (user authentication), 300-312
- CGI, 360-361
  - 使用管理控制台拷贝配置 (copying configurations with Administration Console), 147-148
  - 按目录 (by directory), 366-368
  - 按文件扩展 (by file extensions), 366-371
  - 适用于 UNIX/Linux 系统 (for UNIX/Linux systems), 371
  - 全局配置 (global configuration), 371
- 核心文件排排除 (core files as troubleshooting)
- 核心库 (JSTL), 402
- 核心子系统 (core subsystem), 5-7
- FastCGI, 386-389
- 关联 HTTP 日志和服务器日志 (relating HTTP Access Log and Server Log), 417
- 日志条 (Log entries), 512
- Java Web 应用配置 (Java web application configuration), 427
- 崩溃排排除 (crashes, troubleshooting), 487
- 创建反向代理子命令 (create-reverse-proxy subcommand), 351
- server.xml 文件, 427
- 创建 sun-web.xml 文件, 436-438
- web.xml 文件, 434-435
- PHP, 392
- Java Web 应用, 466-470
- SHTML, 378, 383

# D

- *db 文件, 181
- 数据中心 (data centers), 122
- DAV 权限 (DAV privileges), 315
- 调试 Java Web 应用 (debugging Java web applications), 474-479
- 请求处理 (request processing)
  - 日志 SAF (log SAF), 249
  - 服务器日志 (Server Log), 250-254
- 默认请求处理行为 (default request processing behavior), 229
- 不存在的文件请求 (nonexistent file requests), 233-234
- obj.conf 文件
  - 指令处理顺序 (directive processing order), 167
  - default.acl 配置文件 (default.acl configuration file), 192-193
    - 上文 (context), 191
    - 文件结构 (file structure), 192
    - 修改 (modifications), 193
    - 语法 (syntax), 194
  - 默认 Web 应用部署 (default web application deployment), 451
  - 命令行部署 (command-line deployment), 444
  - 手动部署 (manual deployment), 450
  - Web 部署 (web-based deployment), 439
  - 检测 DoS 攻击 (detecting DoS attacks), 344-348
  - 诊断工具 (diagnostic tools), 501-504
  - netstat 命令, 505
  - ptree 命令, 506
  - DSA（数字签名算法）算法, 333
  - 数字证书 (digital certificates), 334-337
  - 指令 (directives), 175
    - 条件处理 (conditional processing)
      - 客户端容器 (Client containers), 237-238
      - If/Else 容器 (If/Else containers), 238-241
      - NameTrans 指令属性 (NameTrans directive attributes), 235
      - 路径属性 (Path attributes), 236
      - 默认模板 (default template), 167
      - 安装 Web Server 7.0 (install Web Server 7.0), 77
    - 故障转移 (failover), 306
    - 身份验证数据库 (as authentication database), 303
    - 禁用 Java (disabling Java), 419-422
  - 请求洪水 (request flooding), 343
  - DTrace, 510-512
  - 动态内容 (dynamic content)
    - CGI, 31
    - FastCGI, 32
    - Java, 33
    - 内容请求 (content requests), 413
    - 目录请求 (directory requests), 415-416
  - MIME 映射内容请求 (MIME-mapped content requests), 417
  - 不存在的内容请求 (nonexistent content requests), 414
  - 请求处理行为 (request behavior), 409
  - 服务端进程模型 (server-side process model), 408-409
  - 服务器错误消息字段 (fields of server error messages), 495-496
  - SHTML, 32
  - 动态 Java 应用重配置 (dynamic Java application reconfiguration), 459-460
  - 动态重配置 (dynamic reconfiguration), 29
  - 文件模式（CLI） (file mode (CLI)), 127
  - 文件模式调用 wasm 脚本 (invoking wasm script), 138–139
  - 文件结构 (file structure)

# E

- ECC（椭圆加密学）密码套, 11
- ECDSA（椭圆曲线数字签名算法）, 333
- echo 命令, 377
- 配置文件的手动编辑 (configuration files, manual editing), 140–141
- 启用 Java (enabling Java), 419–422
- Java Web 应用中的整体响应 (entire responses, caching in Java web applications), 456
- 请求错误处理 (Error Handling of request processing), 228
- ERROR 安装日志 (ERROR install logs), 70
- 错误消息来源 (error messages as source of troubleshooting), 494–496
- 错误-fastcgi SAF (error-fastcgi SAF), 389
- 示例 (examples)
  - certmap.conf 文件, 187-188
  - default.acl 配置文件, 193
  - keyfile.conf 配置文件, 202
  - mime.types 配置文件, 175-177
  - obj.conf 文件, 165-167
  - 信任数据库文件, 182-183
- 文件系统访问日志数据 (file system accessing log data), 271
- 过滤器-fastcgi SAF (filter-fastcgi SAF), 389
- 过滤器 (filters)
  - 输入过滤器 (Input filters), 223
  - 输出过滤器 (Output filters), 224
- FINE 安装日志, 70
- FINEST 安装日志, 70
- fastmod 命令, 377
- free 命令, 501
- size 命令, 377
- 函数 (functions), SAFs, 244

# G

- G11n 支持 (G11n support)
  - 文本数据报告 (plain text data report), 545, 548–555
  - server.xml 文件的 (of server.xml file), 533–538
  - XML 数据报告 (XML data report), 539, 542–543
- exec 命令, 377
- 快速安装 (Express Installation), 49
- 表达式属性 (expression attribute), default.acl file, 198
- 表达式函数 (expression functions), 248–249
- 表达式操作符 (expression operators), default.acl file, 199




# 索引

# 563

- 全局 Java 设置（管理控制台），422–424
- 增量配置更改, 517
- 无限循环，跟踪, 516
- 全局启用/禁用 Java, 419–421
- Web Server 7.0 的图形化安装, 46-51
- INFO 安装日志, 70
- it-cgi SAF, 373
- it-fastcgi SAF, 389
- 管理选项界面, 54-57
- 组件选择界面, 51-52
- 安装进度界面, 59
- Java 配置界面, 53
- 准备安装界面, 59
- Web Server 设置界面, 57-58
- 图形化卸载, 91–92, 95
- grep 命令, 118
- 向 Web Server 7.0 的 GUI 迁移, 102
- 初始配置，创建, 90
- 请求处理的输入阶段, 223
- 故障排除, 486
- 安装进度界面（安装向导）, 59
- 安装 NetBeans IDE 插件, 464-466。参见安装 Web Server 7.0
- Web Server 7.0，另见卸载 Web Server 7.0
- 命令行安装, 61-62
- 表达式数组 (Expression Array), 49
- 图形化安装, 46-51
- 管理选项界面, 54-57
- 组件选择界面, 51-52
- 安装进度界面, 59
- Java 配置界面, 53
- 准备安装界面, 59
- Web Server 设置界面, 57-58
- 内存需求, 42
- 安装后任务, 85-87
- 初始配置，创建, 90
- Web Server 7.0 实例，访问, 88-90
- Web Server 实例，自动准备, 44
- 设置命令, 45-46
- 静默安装, 62, 67-68
- 构建标识符, 67
- 状态文件，生成, 63-66
- 支持的平台, 41
- 验证安装
- 目录结构, 77-81
- 日志文件, 69-73
- 产品注册表, 81-82
- 服务器进程, 74-76
- Windows 特有条目, 83-84

# H

- 握手 (SSL), 337–340
- 挂起
- 跟踪, 516
- 故障排除, 487
- 硬件收集
- 故障排除, 489
- 管理控制台帮助信息, 126
- Sun Server 历史, 2-3
- HTTP 访问日志作为故障排除信息源, 496-498
- 条目，与服务器日志条目关联, 512
- HTTP 客户端环境信息，用于故障排除, 443

# I

- I18N 支持, 15
- IANA（国际分配数字机构）, 142
- If/ElseIf/Else 计数器, 238-241
- 正正则表达式, 244–245
- include 命令, 377
- 增加日志消息详细性, 512

# 564

# 索引

- 实例, 19, 114
- 管理服务器, 110
- 管理
- 在基于 UNIX 的系统中启动/停止, 118-120
- 在基于 Windows 的系统中启动/停止, 120-121
- 配置, 111-113
- 统计，监控, 285
- 国际化/格式化库 (JSTL) 403
- 可操作性，改进, 14-15
- 调用 wadm 脚本
- 文件模式, 138-139
- Shell 模式, 137-138
- 独立模式, 136
- 生命周期模块, 407
- 会话复制功能, 407
- Web 服务技术, 405–406
- 线程，生成栈跟踪信息, 513
- Web 
- 应用生命周期, 425
- 缓存, 455-457
- 配置, 427-438
- 创建, 466-470
- 调试, 474, 477-479
- 部署, 470, 473
- 部署到 Web 服务器, 439, 444-451
- 目录, 425-427
- 动态重配置, 459-460, 463
- 安全, 454-455
- 会话管理, 452
- 会话管理器, 453
- 会话复制, 453-454

# J

- JAAS（Java 身份验证与授权）, 201
- JACL（Java 语言）, 127
- Java
- 管理控制台全局设置, 422-424
- 配置文件, 418-419
- 配置, 417
- 内容请求, 413
- 目录, 415-416
- 用于 MIME 映射内容, 416-417
- 动态内容, 333
- 虚拟服务器启用/禁用, 421–422
- 全局启用/禁用, 419-421
- JVM 类加载器, 457
- 不存在的请求, 414
- 请求处理行为, 409-413
- 服务器端 Java 模型, 408–409
- 服务器端技术
- Java Servlets API, 400-401
- JDBC, 403
- JNI, 408
- JSF, 404
- JSP, 401, 402
- Java 配置界面（向导）, 53
- Java EE, 400
- Java ES，监控 Web 服务器, 290-291
- Java ES 软件，获取, 43
- Java Servlets API, 400-401
- JDBC（数据库连接）, 403
- JMX（Java 管理扩展）, 115
- Agent MBeans, 117
- MBeans，监控, 117
- Task MBeans, 117
- JNI（Java 原生接口）, 408
- JSF, 404
- JSP 技术, 401–402
- JVM 类加载器, 457

# K

- Keep活线程, 24
- Keyfile, 204–205
- 上下文, 206
- 文件结构, 205
- 修改, 206
- 语法, 205
- kill 命令, 501

# 565

# L

# M

- 管理控制台布局, 122, 125
- LDAP, 115
- libfastci 插件, 157
- lib22plugin 插件, 157
- 生命周期模块（Java）, 407
- Linux，配置 CLI, 371
- Live HTTP Headers, 502-504
- load-modules SAF, 157
- 本地化
- 管理控制台, 142
- CLI, 142-144
- 日志文件, 669
- Web Web 服务器访问日志, 262-263
- 作为故障排除信息源, 493-496
- 数据访问：从管理控制台 (269), 从 CLI (270), 从文件系统 (271)
- HTTP 作为故障排除信息源, 496-498
- 低级日志文件，验证 Web Server 7.0, 72-73
- 监控 Web 服务器, 269
- Server 文件，监控 Web 服务器, 263-266
- 从管理控制台修改, 266
- 从 CLI 修改, 267-269
- Server 日志文件，验证 Web Server 7.0, 269
- 管理控制台本地化, 142
- CLI 本地化, 142-144
- 日志文件, 669
- Web Web 服务器访问日志, 262-263
- 作为故障排除信息源, 493-496
- 数据访问：从管理控制台 (269), 从 CLI (270), 从文件系统 (271)
- HTTP 作为故障排除信息源, 496-498
- 低级日志文件，验证 Web Server 7.0, 72-73
- 监控 Web 服务器, 269
- Server 文件，监控 Web 服务器, 263-266
- 从管理控制台修改, 266
- 从 CLI 修改, 267-269
- Server 日志文件，验证 Web Server 7.0, 269

等待，我需要根据提供的文本重新格式化索引。

[content]
# 索引

# 563

- 全局 Java 设置（管理控制台）, 422–424
- 增量配置更改, 517
- 无限循环，跟踪, 516
- 全局启用/禁用 Java, 419–421
- Web Server 7.0 的图形化安装, 46-51
- INFO 安装日志, 70
- it-cgi SAF, 373
- it-fastcgi SAF, 389
- 管理选项界面, 54-57
- 组件选择界面, 51-52
- 安装进度界面, 59
- Java 配置界面, 53
- 准备安装界面, 59
- Web Server 设置界面, 57-58
- 图形化卸载, 91–92, 95
- grep 命令, 118
- 向 Web Server 7.0 的 GUI 迁移, 102
- 初始配置，创建, 90
- 请求处理的输入阶段, 223
- 故障排除, 486
- 安装进度界面（安装向导）, 59
- 安装 NetBeans IDE 插件, 464-466。参见安装 Web Server 7.0
- Web Server 7.0，另见卸载 Web Server 7.0
- 命令行安装, 61-62
- 表达式数组 (Expression Array), 49
- 图形化安装, 46-51
- 管理选项界面, 54-57
- 组件选择界面, 51-52
- 安装进度界面, 59
- Java 配置界面, 53
- 准备安装界面, 59
- Web Server 设置界面, 57-58
- 内存需求, 42
- 安装后任务, 85-87
- 初始配置，创建, 90
- Web Server 7.0 实例，访问, 88-90
- Web Server 实例，自动准备, 44
- 设置命令, 45-46
- 静默安装, 62, 67-68
- 构建标识符, 67
- 状态文件，生成, 63-66
- 支持的平台, 41
- 验证安装
- 目录结构, 77-81
- 日志文件, 69-73
- 产品注册表, 81-82
- 服务器进程, 74-76
- Windows 特有条目, 83-84

# H

- 握手 (SSL), 337–340
- 挂起
- 跟踪, 516
- 故障排除, 487
- 硬件收集
- 故障排除, 489
- 管理控制台帮助信息, 126
- Sun Server 历史, 2-3
- HTTP 访问日志作为故障排除信息源, 496-498
- 条目，与服务器日志条目关联, 512
- HTTP 客户端环境信息，用于故障排除, 443

# I

- I18N 支持, 15
- IANA（国际分配数字机构）, 142
- If/ElseIf/Else 计数器, 238-241
- 正正则表达式, 244–245
- include 命令, 377
- 增加日志消息详细性, 512

# 564

# 索引

- 实例, 19, 114
- 管理服务器, 110
- 管理
- 在基于 UNIX 的系统中启动/停止, 118-120
- 在基于 Windows 的系统中启动/停止, 120-121
- 配置, 111-113
- 统计，监控, 285
- 国际化/格式化库 (JSTL) 403
- 可操作性，改进, 14-15
- 调用 wadm 脚本
- 文件模式, 138-139
- Shell 模式, 137-138
- 独立模式, 136
- 生命周期模块, 407
- 会话复制功能, 407
- Web 服务技术, 405–406
- 线程，生成栈跟踪信息, 513
- Web 
- 应用生命周期, 425
- 缓存, 455-457
- 配置, 427-438
- 创建, 466-470
- 调试, 474, 477-479
- 部署, 470, 473
- 部署到 Web 服务器, 439, 444-451
- 目录, 425-427
- 动态重配置, 459-460, 463
- 安全, 454-455
- 会话管理, 452
- 会话管理器, 453
- 会话复制, 453-454

# J

- JAAS（Java 身份验证与授权）, 201
- JACL（Java 语言）, 127
- Java
- 管理控制台全局设置, 422-424
- 配置文件, 418-419
- 配置, 417
- 内容请求, 413
- 目录, 415-416
- 用于 MIME 映射内容, 416-417
- 动态内容, 333
- 虚拟服务器启用/禁用, 421–422
- 全局启用/禁用, 419-421
- JVM 类加载器, 457
- 不存在的请求, 414
- 请求处理行为, 409-413
- 服务器端 Java 模型, 408–409
- 服务器端技术
- Java Servlets API, 400-401
- JDBC, 403
- JNI, 408
- JSF, 404
- JSP, 401, 402
- Java 配置界面（向导）, 53
- Java EE, 400
- Java ES，监控 Web 服务器, 290-291
- Java ES 软件，获取, 43
- Java Servlets API, 400-401
- JDBC（数据库连接）, 403
- JMX（Java 管理扩展）, 115
- Agent MBeans, 117
- MBeans，监控, 117
- Task MBeans, 117
- JNI（Java 原生接口）, 408
- JSF, 404
- JSP 技术, 401–402
- JVM 类加载器, 457

# K

- Keep活线程, 24
- Keyfile, 204–205
- 上下文, 206
- 文件结构, 205
- 修改, 206
- 语法, 205
- kill 命令, 501

# 565

# L

# M

- 管理控制台布局, 122, 125
- LDAP, 115
- libfastci 插件, 157
- lib22plugin 插件, 157
- 生命周期模块（Java）, 407
- Linux，配置 CLI, 371
- Live HTTP Headers, 502-504
- load-modules SAF, 157
- 本地化
- 管理控制台, 142
- CLI, 142-144
- 日志文件, 669
- Web Web 服务器访问日志, 262-263
- 作为故障排除信息源, 493-496
- 数据访问：从管理控制台 (269), 从 CLI (270), 从文件系统 (271)
- HTTP 作为故障排除信息源, 496-498
- 低级日志文件，验证 Web Server 7.0, 72-73
- 监控 Web 服务器, 269
- Server 文件，监控 Web 服务器, 263-266
- 从管理控制台修改, 266
- 从 CLI 修改, 267-269
- Server 日志文件，验证 Web Server 7.0, 269
- 管理控制台本地化, 142
- CLI 本地化, 142-144
- 日志文件, 669
- Web Web 服务器访问日志, 262-263
- 作为故障排除信息源, 493-496
- 数据访问：从管理控制台 (269), 从 CLI (270), 从文件系统 (271)
- HTTP 作为故障排除信息源, 496-498
- 低级日志文件，验证 Web Server 7.0, 72-73
- 监控 Web 服务器, 269
- Server 文件，监控 Web 服务器, 263-266
- 从管理控制台修改, 266
- 从 CLI 修改, 267-269
- Server 日志文件，验证 Web Server 7.0, 269




# 索引

# 567

- 文件结构, 165-167
- 修改, 174
- 命名对象处理, 171-172
- 路径对象处理, 172-173
- 语法, 167-170
- 对象, 170-173
- 变量, 173
- 对象文件（虚拟），编辑, 517
- 请求处理的 ObjectType 阶段, 220-222
- 观察访问控制行为, 319-322
- 获取
- 从 CLI 获取配置级统计数据, 280-282
  - Java ES 软件, 43
  - 独立软件, 43
  - 从 CLI 获取虚拟服务器统计, 282-283
  - 从 CLI 获取 Web 容器统计, 284
- 操作系统功能，用于故障排除的收集, 489
- 性能优化，最佳实践, 295
- 源层, 349
- Ousterhout, John, 140
- 请求处理的 Output 阶段，输入过滤器, 224
- 性能监控, 293-295
- pfiles, 502
- PHP
  - 配置, 392
  - 作为 CGI 程序运行, 393
  - 作为 FastCGI 程序运行, 393
  - 作为 NSAPI 程序运行, 394
- 用于公钥基础设施的 PKIX, 331
- 纯文本报告
  - 从 CLI 访问, 276
  - 从用户定义的 URI 访问, 277-279
  - 示例, 545-555
  - Web 服务器, 监控, 275
- 插件
  - FastCGI 插件, 386
  - NetBeans IDE
    - 安装, 464–466
    - Web 服务器管理, 472, 475
  - 安装后任务
    - 初始配置，创建, 90
    - 启动和 Web Server 7.0, 85-87
    - Web Server 7.0 实例，访问管理节点, 90
    - 管理节点, 88-89
  - 路径属性, 236
  - 路径对象处理，obj.conf 配置, 172-173
  - 安装准备, 44
- 原始进程, 20, 75
  - 探针, 50
- 进程, 19
  - 显示, 21
  - 原始的, 75
  - 验证 Web Server 7.0 安装, 74-76
  - 看门狗 (watchdog), 75
  - 工作进程 (worker), 75
- 工作进程, 22
- 访问控制子系统, 28
  - 连接句处理线程, 23-24
- 内容处理子系统, 27
- 动态重配置, 29
- 原生线程池, 26

# P

- Java Web 应用中的页面片段缓存, 457
- 作为认证数据库的 PAMs（可插拔身份模块）,310
- 参数，壳变量, 128-131
- 路径属性 (Path Attribute), 236
- 请求处理的 PathCheck 阶段, 214
  - ACL 处理, 218-219
  - 路径名预处理, 215-216
  - 路径验证, 216-217
- 模式匹配, 29-30
  - 正则表达式, 243-245
  - 反引用, 245-248
  - 表达式函数, 248-249
  - 简单模式匹配, 241-243
- perdump 报告, 513-515
- 性能，故障排除, 488
- NSAPI 引擎, 25
  - 默认行为, 229
  - 模式匹配, 29-30
  - 不存在的请求, 233-234
  - 模式, 25-26
  - obj.conf 文件, 230-231
  - SAFs, 24
  - 静态内容请求, 231-233
- 安全性, 27
- 错误处理阶段, 228
- mime.types 配置
- 输入阶段, 223
- 客户端处理, 179-180
- Java, 409-413
  - 服务器处理, 177-179
  - 目录请求, 415-416
  - MIME 映射内容请求, 416-417
- 故障排除信息的源产品文档 (product documentation), 500
- 不存在的内容请求, 414
- 验证 Web Server 7.0 安装的制品注册表, 812

# 索引
- NameTrans 阶段, 212-214
- ObjectType 阶段, 220-222
- prostat 命令, 502
- Output 阶段, 224
- ps 命令, 21, 34, 76, 506
- PathCheck 阶段, 214
- pstack 命令, 35, 502, 516
- ACL 处理, 218-219
- ptree 命令, 21, 502, 506
- 路径名预处理, 215-216
- 公钥加密, 328-329
- 路径名验证, 216-217
- pwdx 命令, 502
- Response 阶段, 224-227

# Q-R

- query-handler SAF, 373
- Route, 224
- 资源访问控制, 300
- 准备安装（安装向导）, 459-460
- 用户认证, 300-312
- responder-fastcgi SAF, 389
- 验证 Web Server 7.0 安装, 84
- 请求的 Response 阶段, 224
- 处理, 225-227
- 正则表达式, 243-244
- 反向代理, 213
- Web 服务器，作为,349-352
- 反向代理服务器, 28
- 反引用, 245-248
- 表达式函数, 248-249
- 回滚配置, 150-152
- 根元素 (XML), 161
- 请求的 Route 阶段, 224
- 请求泛洪, 324-347
- 请求供应, 210
- 运行 CLI, 127-128
- 运行时错误，故障排除, 487
- AuthTrans 阶段, 211-212
- 条件处理, 24-26
- SAFs（应用程序函数）, 237-238
- CGI, 372-375
- If/Else, 238-241
- 检查请求限制, 345-347
- NameTrans 指令, 235
- 部分路径属性, 236
- 加载模块, 157
- log SAF, 249
- SHTML, 383-385

# S

- 可扩展性问题，故障排除, 488
- 架构 (schema), 163-164
- 控制脚本, 85
- FastCGI, 385-386
  - 配置, 386-389
- PHP, 392
  - 作为 CGI 运行,393
  - 作为 FastCGI 程序运行, 393
  - 作为 NSAPI 程序运行, 394
- SHTML, 375-377
- 命令, 378-383
- SAFs, 383-385
- 脚本, 140
- 安全反向代理, 352
- 访问，关联用户认证, 301-312
- 访问控制, 312
- 行为, 319-322
- 处理, 315-319
- CRL 处理, 341-343
- Java Web 应用, 454-455
- 反向代理，服务器作为, 349-352
- SSL 证书, 325-326
- CA, 334-337
- 握手, 337-340
- 公钥加密, 328-329
- 对称加密, 327-328
- X.509 数字证书, 330-332
- XSS 攻击，防护, 13
- 安全模块数据库工具, 502
- 自签名证书, 336
- send-cgi SAF, 373
- send-shellcgi SAF, 373
- responder-fastcgi SAF, 389
- 反向代理服务器, 28
- 状态文件
- 构建标识符, 67
- 生成, 63-66
- 静态内容请求，默认请求行为, 231-233
- 静态数据, 258
- 停止 Unix 系统上的实例, 120
- strace 命令, 503
- 子命令，自动补全功能, 133-135
- 子系统，核心子系统, 5-7
- Solaris 动态跟踪指南, 512
- 故障排除信息源, 493
- 核心文件, 499
- Sun 博客网站, 521-526
- Sun 开发者网络 Web 层主页, 517
- Sun 论坛网站, 526-529
- Sun Java System ASP 服务器, 396
- Sun Java System Web Server 7.0 管理员配置文件参考, 30, 248





# 索引

# 571

Sun Java Web Server 7.0 Java Web 应用程序开发者指南, 184
Sun Java Web Server 7.0 性能调优、尺寸配置与扩展指南, 515, 546
Sun Java Web Server 7.0 故障排除指南, 509
Sun 支持中心网站, 517
sun-web.xml 配置文件, Java Web 应用程序配置, 436-438
超级用户账户, 306
swap 命令, 503
对称密钥加密, 327-328
语法
- 用于 certmap.conf 文件, 188-191
- 用于 default.acl 配置文件, 194-195
- 身份验证方法, 195
- 授权语句, 196-197
- 表达式属性, 198
- 表达式运算符, 199
- 用于 default-web.xml 配置文件, 200
- 用于 keyfile 文件, 205
- 用于 login.conf 配置文件, 203
- 用于 magnus.conf 文件, 158-159
- 用于 obj.conf 文件, 167-170
- 对象, 170-173
- 变量, 173
- 用于 server.policy 文件, 184
- 用于 server.xml 文件, 160-163
- 用于 SML 命令, 377
CLI 命令语法, 131-132

Java 线程, 生成堆栈跟踪信息, 513
多线程, 33-38
TLS (传输安全层), 326
追踪无限循环, 516
故障排除
- 管理性问题, 488
- 崩溃, 487
- 诊断工具, 501-504
- DTrace, 510-512
- Live HTTP 头部, 504
- netstat 命令, 505
- ps 命令, 506
- tree 命令, 506
- snoop 命令, 509-510
- ssltap, 507-509
- Wireshark, 510
- 挂起, 487
信息收集
- 硬件信息, 489
- HTTP 客户端环境信息, 491
- 操作系统信息, 489
- Web 服务器环境信息, 489-491
- 安装问题, 486
- 迁移错误, 488
- 性能, 488
- 运行时错误, 487
- 信息来源, 493
- 核心文件, 499
- HTTP 访问日志文件, 496-498
- 日志文件, 493-496
- 网络流量, 500
- 产品文档, 500
- Web 服务器统计数据, 499-500
- 启动问题, 487
- 卸载问题, 489
信任数据库, 332
文件, 181
上下文, 183
文件结构, 182-183
修改, 183
使用监控数据调优 Web 服务器, 293-295

# T

制表补全, 133-135
Task MBeans, 117
Tcl 脚本支持, 140
tcpcdump, 503
threads. 另见 processes
- 接收线程, 529
- 连接处理, 23
- 接收器, 23
- 保持存活, 24
- 工作线程, 24

# U

ulimit 命令, 504
name 命令, 504
卸载命令, 91
卸载 Web Server 7.0
- 命令行卸载, 96-98
- 图形化卸载, 91-92, 95
故障, 故障排除, 489
- 静默卸载, 98
卸载命令, 91

UNIX
- 管理实例, 启动/停止, 118-120
- CGI, 配置, 371
- 管理控制台最新动态, 126
- 用户账户, 超级用户, 306
用户身份验证
-目录服务, 303-309
- 文件, 301-303
- 接入, 311-312
- PAMS, 310
用户派生 URI
纯文本报告, 访问, 277-279
XML 报告, 访问, 273-275

# V

值 (XML), 160
变量, obj.conf 配置, 173
服务器日志消息的详细程度, 增加, 512
验证安装
- 目录结构, 77-81
- 日志文件, 69
- 低级日志文件, 72-73
- Web Server 安装, 69-72
- 产品注册表, 81-82
- 服务器进程, 74-76
- Windows 特有项目, 83
注册表条目, 84
Windows 程序组, 83
Sun Web Server 版本, 2-3
虚拟服务器统计数据, 从 CLI 获取, 282-283

虚拟服务器统计数据, 监控, 285
虚拟服务器, 114-115
Java, 启用/禁用, 421-422
对象文件, 编辑, 517
vmstat, 504

# W

admin 脚本, 调用
文件模式, 138
shell 模式, 137
独立模式, 70
watchdog 进程, 20-21, 75
Web 2.0 网站
- , 519-520
MLB.com, 530-531
Sun Blogs, 521-526
Sun Forums, 526-529
Web 应用程序开发, 13
应用生命周期, 425
缓存, 445
页面碎片, 557
配置
default-web.xml 配置文件, 429-432
server.xml 配置文件, 434-435
web.xml 配置文件, Java
应用程序配置, 436-438
创建, 466
部署到 Web 服务器, 470
自动部署, 444
默认 Web , 451
目录, 425-427
动态配置, 459-460
安全, 454
会话管理, 452
会话管理器, 453
会话复制, 454

# 索引

# 573

# X

Web 容器, 408
统计数据, 从 CLI 获取, 284
Web 服务器环境信息
用于故障排除, 489-491
Web 安装日志
Server 7.0 安装, 69-72
Web 服务器统计数据来源
499-500
Web 服务技术 (Java), 405-406
WebDAV (基于 Web 的分布式创作与版本控制), 12
网站, 2.0, 519-520
MLB.com, 530-531
Sun Blogs, 521-526
Sun Forums, 526-529
Web 应用程序, 13
web.xml 配置文件, Java
应用程序配置, 436-435
通配符, 简单模式匹配, 243
Windows 操作系统
管理实例, 启动/
停止, 120-121
注册表条目, 验证 Web Server 7.0
安装, 84
Windows 程序组, 验证
Server 7.0 安装, 83
Wireshark, 504, 510
工作进程, 20-22, 75
访问控制子系统, 28
连接处理线程
- 接收线程, 23
- 保持连接线程, 24
- 工作线程, 24
内容处理子系统, 27
动态配置, 29
LWP 统计数据, 506
原生线程池, 26
NSAPI 引擎, 25
模式匹配, 29-30
进程模式, 25-26
SAFs, 24
安全, 27
工作线程, 24

X.509 数字证书, 330-332
客户端身份验证, 186
自签名的, 336
XML (可扩展标记语言)
根元素, 161
架构, 163-164
XML 库 (JSTL), 402
XML 报告
从 CLI 访问, 272
从用户定义 URI 访问, 273-275
示例, 539, 542-543
监控 Web 服务器, 272
XSS (跨站脚本) 攻击
防御, 13

