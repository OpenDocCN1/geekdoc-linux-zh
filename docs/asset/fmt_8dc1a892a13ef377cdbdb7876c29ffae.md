
![](img/a3cb513bfd7a0b21f70c67fcaede10f6_23_0.png)

注意：我们尽力确保书中呈现的信息（内容或示例）的准确性。然而，我们预计书中可能存在无意的错误。如果您发现任何需要的错误（无论是示例缺陷还是拼写错误），我们希望听到您的反馈。请访问 SunWebServer.com 网站，点击 Errata 链接，并按照说明在线提交错误。

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

### 1.1 Sun Web Server 的早期版本
