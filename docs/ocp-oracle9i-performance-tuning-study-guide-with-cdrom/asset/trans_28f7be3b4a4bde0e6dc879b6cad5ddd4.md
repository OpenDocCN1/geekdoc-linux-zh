

# 致谢

我谨此感谢众多对塑造我的职业经历，从而促成本书写作之人。其中包括我在格林布里尔·罗素公司（Greenbrier & Russel, Inc.）的甲骨文（Oracle）同事，他们的 Oracle 挑战也帮助塑造了我自己的职业路径：Christopher Guillaume、John Golden、Jesus Quinones、Jim Whitte 和 Jane Yang。

此外，我还要感谢在过去几年中为我提供许多有趣 Oracle 经验的客户和同行数据库管理员（DBA），包括：美国输电公司（American Transmission Company）的 Jonathan Jackson、Tim Eleyt、Linda Ramme、Bob Budden、Greg Van Haren 和 John Aaholm；高地社区学院（Highland Community College）的 Tony Gastel 和 Audrey Smith；迪恩健康计划（Dean Health Plan）的 George Carpenter 和 Lorin Weiler；密尔沃基地区技术学院（Milwaukee Area Technical College）的 Mike Gavin、Jerri Wang、Dan Hartsman、Thomas Baas 和 Ted Drankus；以及 Snap-On Tools 的 Jim Schwarz 和 Reginald Bron。

我要感谢 Matt Weishan，他撰写或修订了 9i 书籍及 CD 中的所有问题。我很高兴我们能在这个项目中再次合作。

还要感谢 Bob Bryla 和 Ashok Hanumantth 在技术审查期间的付出，以及 Sybex 公司所有让这个�目顺利进行的人：Christine McGeever、Jeff Kellum、Dan Schiff、Linda Stephenson 和 Leslie Light。

最后，我要感谢我的妻子 Brenda，她总能在截止日期临近时，腾出时间为我校对章节或修复屏幕截图。

# 引言

信息技术（IT）行业对专业人才的需求很高，而 Oracle 认证是数据库领域最炙手可热的资历凭证。你做出追求认证的决定是正确的，因为获得 Oracle 认证将为你在这个竞争激烈的市场中带来明显的优势。

许多读者可能已经熟悉 Oracle，不需要介绍 Oracle 数据库世界。对于那些不熟悉该公司的读者，Oracle 成立于 1977 年，销售了第一个商用关系数据库，如今是全球领先的数据库公司，也是第二大独立软件公司，营收超过 100 亿美元，服务于 145 多个国家。

Oracle 数据库是大型互联网网站的事实标准。当 Oracle 的广告商宣称“互联网运行在 Oracle 之上”时，他们虽然自夸，但说的是事实。几乎所有大型互联网网站都运行 Oracle 数据库。Oracle 在数据库市场的渗透很深，并不仅限于互联网公司的应用。许多公司的企业资源规划（ERP）应用程序套件、数据仓库和定制应用程序都依赖 Oracle。在经济低迷时期，对 DBA 资源的需求仍然高于其他领域。

本书旨在帮助你踏上成为 Oracle 认证专业人员（OCP）和 Oracle 认证大师（OCM）的激动人心之旅。具备 Oracle SQL 的基础知识在阅读本书时是一个优势，但并非必要条件。使用本书和一个练习数据库，你可以开始学习 Oracle 并通过 1Z0-033 考试：Oracle9i 数据库：性能调整。

## 为什么要成为 Oracle 认证专业人员？

成为 OCP 的首要原因是获得更高的知名度，并更大程度地进入该行业最具挑战性的机会。Oracle 认证是展示你在 Oracle 数据库系统方面知识和技能的最佳方式。认证考试是基于场景的，这是评估你动手能力和关键问题解决技能的最有效方式。

认证是你知识的证明，表明你具备支持 Oracle 核心产品所需的技能。Oracle 认证计划可以帮助公司识别那些经过验证的表现优异者，他们已展示了自己的技能，并能支持公司对 Oracle 技术的投资。它表明你对自己的职位角色及该角色中使用的 Oracle 产品有扎实的理解。

OCP 是 IT 行业中薪酬最高的群体之一。薪资调查一致表明，OCP 认证带来的薪资高于其他认证，包括 Microsoft、Novell 和 Cisco。

因此，无论你正在开始职业生涯、转换职业、稳固现有职位，还是希望完善和提升你的职位，这本书都适合你！

## Oracle 认证

Oracle 认证遵循面向职位角色的路径。有数据库管理、数据库操作员和开发者等路径。在每个路径中，Oracle 都有一个三级认证计划：

- 第一级是 Oracle 认证助理（OCA）。OCA 认证通常要求你完成两项考试，第一项通过互联网进行，第二项在监考环境中进行。
- 下一等级是 Oracle 认证专业人员（OCP），它建立在 OCA 认证之上，并要求持有 OCA 认证。获得 OCP 认证的额外要求是通过额外的监考考试。
- 第三级也是最高级别是 Oracle 认证大师（OCM）。OCM 认证建立在 OCP 认证之上，并要求持有 OCP 认证。要获得 OCM 认证，你必须参加两门高级 Oracle 教育课堂课程（来自特定合格课程列表）并完成一项实践考试。

以下内容仅讨论数据库管理路径，因为截至本书写作时，它是 Oracle 提供的唯一 9i 路径。其他路径拥有 8 和 8i 认证，并且无疑将推出 9i 认证。请访问 Oracle 网站 http://www.oracle.com/education/certification/ 获取最新信息。

## Oracle9i 认证数据库助理

数据库管理员（DBA）的角色已成为当今高度复杂的数据库系统中成功的关键。最优秀的 DBA 在幕后工作，但当关键问题出现时，他们会成为焦点。他们进行规划、创建、维护数据库，并确保数据库对业务可用。他们始终关注数据库的性能问题，并防止计划外的停机。DBA 的工作要求对 Oracle 数据库的架构有广泛的理解，以及解决问题的专业知识。

Oracle9i 认证数据库助理是数据库管理路径的入门级认证，是向更高级别认证等级晋级所必需的。该认证要求你通过两项考试，以展示你对 Oracle 基础知识的掌握：

- **1Z0-007**：Oracle9i 介绍：SQL
- **1Z0-031**：Oracle9i 数据库：基础 I

1Z0-007 考试，Oracle9i 介绍：SQL，在互联网上提供。1Z0-031 考试，Oracle9i 数据库：基础 I，在 Sylvan Prometric 考场提供。

## Oracle9i 认证数据库管理员（OCP）

数据库管理路径的 OCP 级别要求你展示你对 Oracle 技术的持续经验和知识。Oracle9i 认证数据库管理员认证要求达成认证数据库助理级别，并在 Sylvan Prometric 考场通过以下两项考试：

- **1Z0-032**：Oracle9i 数据库：基础 II
- **1Z0-033**：Oracle9i 数据库：性能调整

## Oracle9i 认证大师

Oracle9i 认证大师是 Oracle 提供的最高级别认证。要成为认证大师，你必须首先获得 OCP 状态，然后在 Oracle 教育设施完成两门高级讲师引导课程，最后在 Oracle 教育通过一项动手考试。这些课程和实践考试仅在 Oracle 教育设施提供，可能需要差旅。计入 OCM 要求的高级课程包括以下课程：

- Oracle9i：使用 PL/SQL 编程
- Oracle9i：高级 PL/SQL
- Oracle9i：SQL 调整研讨班
- Oracle9i：互联网环境中的高可用性

