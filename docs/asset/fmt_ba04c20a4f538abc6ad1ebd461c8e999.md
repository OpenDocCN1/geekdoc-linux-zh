
# Linux 数据库 DBA 指南 [包含 Oracle & MySQL]

> “表述清晰且见解独到——是任何在 Linux 上处理关系型数据库的人士必读的参考资料。”

—Marc Connolly，

Oracle 公司大型系统组，

高级技术顾问

David Egan, RHCE, MCT

Paul Zikopoulos

技术编辑：

Chris Rogers

![](img/4dc2950553fde871c28ea3e04a065356_1_0.png)

# solutions@syngress.com

![](img/4dc2950553fde871c28ea3e04a065356_2_0.png)

文字编辑：Adrienne Rebello

技术编辑：Chris Rogers

索引：Jennifer R. Coker

项目编辑：Mark A. Listewnik

校对：Lynette Crane

排版及制作：Craig Enslin 和 Katherine Glennon

合出版者：Richard Kristof

发行商：Publishers Group West

# 致谢

我们要感谢以下人员为本书出版提供的支持与支持。

感谢 Global Knowledge 的 Richard Kristof, Duncan Anderson, Jennifer Gould, Robert Woodruff, Kevin Murray, Dale Leatherwood, Shelley Everett, Laurie Hedrick, Rhonda Harmon, Lisa Lavallee 和 Robert Sanregret，感谢他们慷慨提供 IT 行业顶级课程、导师和培训设施。

感谢 Ralph Troupe 和 Rt. 1 Solutions 团队，他们对设计、部署和支持世界级企业网络的挑战提供了宝贵的见解。

感谢 Publishers Group West 的 Karen Cross, Kim Wylie, Harry Kirchner, John Hays, Bill Richter, Kevin Votel, Brittin Clark, Sarah Schaffer, Luke Kreinberg, Ellen Lafferty 和 Sarah MacLachlan，他们分享了极其丰富的营销经验和专业知识。

感谢 Harcourt International 的 Peter Hoenigsberg, Mary Ging, Caroline Hird, Simon Beale, Julia Oldknow, Kelly Burrows, Jonathan Bunkell, Catherine Anderson, Peet Kruger, Pia Rasmussen, Denelise L'Ecluse, Rosanna Ramacciotti, Marek Lewinson, Marc Appels, Paul Chrystal, Femi Otesanya 和 Tracey Alcock，确保我们的愿景在全球范围内。

特别感谢 Osborne 的专业人士，我们很幸能出版畅销的 Global Knowledge Certification Press 系列。

# 来自 Global Knowledge

在 Global Knowledge，我们致力于支持学生成为技术专业人士所需的多种学习风格。作为全球最大的 IT 培训公司，Global Knowledge 在提供这些书籍方面具有独特优势。通过向全球数十万学生提供导师指导的培训所积累的专业知识已以书籍形式呈现，以增强您的学习体验。我们希望这些书籍的质量体现了我们对您终身学习成功的承诺。无论您选择通过文字、计算机培训、Web 交付还是导师指导的培训来学习，Global Knowledge 都致力于在每个类别中为您提供最好的服务。对于那些了解 Global Knowledge 的人或刚发现我们的人，我们的目标是成为您终身的能力伙伴。

感谢您让我们有机会为您服务。我们期待未来再次为您服务。

最诚挚的问候，

![](img/4dc2950553fde871c28ea3e04a065356_7_0.png)

Duncan Anderson

Global Knowledge 总裁兼首席执行官

# 贡献

Tom Bascom 是 EDS 的企业架构师，负责为 EDS 客户企业提供业务和信息技术咨询。他的职责包括制定企业战略并提供产品解决方案建议。Tom 从 1986 年开始接触 Progress 产品，从 1994 年开始接触 Linux，是公共论坛和 comp.databases 新组的频繁贡献者。Tom 还是行业文章的作者。

Jamieson Becker 是一名 Linux/UNIX 和 Windows 工程师，Ring0.com 的所有人。自 1980 年开始编程以来，Jamieson 已成为一名经验丰富的顾问，完成了 IBM、Compaq、Carrier、Brown & Williamson、VoiceStream、Cill 和 Citizens 等项目。Jamieson 专门从事使用 Linux 的大型 Web 应用。他与妻子 Jennifer 以及猫 Angie 住在乔治亚州亚特兰。可以通过 jamiebecker@ring0.com 联系他。

Geoff Crawford 领导位于新泽西的咨询公司 Innov8 Computer Software, LLC。(www.innov8cs.com)。自从 15 年前发布以来，他一直在使用 Progress。Geoff 是 Progress E-mail Group 的频繁贡献者，Progress ODBC FAQ 的作者，也是 Progress 用户大会的定期演讲者。在空闲时间，Geoff 喜欢研究他的宾夕法尼亚语根源并听 Pantera 乐队。

Marc Connolly 自 1987 年以来一直从事关系型数据库。他在 DB2、Informix 和 Oracle 方面拥有丰富经验，并在 DBA、产品开发人员、产品经理和营销专家等各种身份担任过这些产品。

Brad Dietrich（计算机科学与电气工程学士）自互联网早期起便在专业和学术领域从事互联网相关工作。他目前是位于加利福尼亚州金山的 ChannelDot Networks 的创始软件工程师之一。在加入 ChannelDot 之前，他创立并经营了 DefTech Contracting (with)，这是一家成功的互联网和 Web 应用开发业务，他为包括美泰（Mattel）和 Spyglass 在内的许多客户开发了世界顶的 Web 应用。他参与过的项目涵盖了从电子商务解决方案到遗留系统集成以及 TB 级数据库。他曾为 Linux 环境下的开源社区应用开发提供支持，范围涵盖从可行中间件到闭源驱动程序中的 Bug 规避方案。在开始互联网应用开发业务之前，他曾在 FORE Systems 开发过基于 Web 的网络管理应用，并在卡内基·梅隆大学开发过基于 Web 的远程学习系统。

David Egan（注册工程师；多伦多大学工程学学士；MCT；RHCE）曾居住在多个国家，并自苹果和 IBM 时代 PC 早期起就开始与计算机打交道。David 的第一份“爱好转工作”是为期五年的 Z80 汇编语言和 C 语言程序员。在过去的 15 年里，David 转型转型，成为一名 VMS/Unix/NT/PC 系统集成顾问和技术讲师。David 仍在从事咨询工作并偶尔编写书籍，但主要为位于北卡罗莱纳州凯里的 Global Knowledge Inc. 担任基于 Unix、NT 和 Linux 的课程总监和课程编写员，网址为：http://www.globalknowledge.com。在不在走台上宣扬 Linux 和 NT 的优点时，他居住在列属颠比亚省温哥华郊，与他可爱的女儿 Vanessa 和儿子 Callen 生活在一起。可以通过 egand@istar.ca 或 egand@wwdb.org 或通过 http://home.istar.ca/~egand 与他联系。

Brent Gilmore（Sun 认证 Solaris 管理员和 Sun 认证网络管理员）是圣地亚哥州立大学的 Oracle DBA 和程序员/分析师。他自 1989 年以来一直从事 IT 行业，拥有信息系统学士学位和工商管理管理硕士学位。Brent 从 1996 年开始使用 Linux，并从 1997 年开始使用 Oracle。他目前正致力于使用 Oracle8/8i、Linux、Perl、PL/SQL、OAS 和 Apache 进行互联网应用开发和数据库设计。
