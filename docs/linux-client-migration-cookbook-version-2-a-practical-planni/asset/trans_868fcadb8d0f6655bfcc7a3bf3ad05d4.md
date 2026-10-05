
这为桌面级 Linux 软件栈的灵活性如何促进创新的部署模型以整合计算系统提供了一个极佳的示例。

- 最后，一旦你确定了基于 Linux 的操作系统镜像的设计和配置，并且设计并测试了一个能够优化预期管理成本的成本效益部署模型，你仍然需要将用户迁移到新系统。最大限度减少对用户干扰的关键挑战之一是：如何高效地从现有 Windows 客户端获取并将重要的桌面个性化数据集迁移到目标 Linux 客户端？现在，多家供应商已提供用于此类数据自动化迁移的工具。我们强调了在中大型企业中使用这些工具的重要性，并在第 277 页的附录 C“使用 Versora Desktop Description 自动化桌面迁移”中深入介绍了如何使用其中一种工具。

## 编写本红皮书的团队

本 IBM 红皮书的第 2 版本是由来自全球、位于奥斯汀中心的国际技术支持组织（International Technical Support Organization, Austin Center）的专家团队编写。

Chris Amend 是驻在德克萨斯州奥斯汀 ITSO 中心的项目负责人和 IT 架构师。他拥有共 15 年的 IT 行业经验，其中最后五年是在 IBM 就职。他的经验包括 UNIX/Linux 系统工程、网络工程、基于 Lotus®Domino® 的内容管理解决方案以及基于 WebSphere Portal 的解决方案设计。

Jeroen van Hof 是荷兰 IBM 全球服务的高级 IT 专家。他在 UNIX 操作系统方面拥有超过15 年的经验，在 Linux 方面拥有超过10 年的经验。在通过 PwC 加入 IBM 之前，他曾在荷兰国家超级计算中心（Dutch National Supercomputing Centre）作为并行专家从事高性能计算。他的专业领域包括 UNIX/Linux、Windows、虚拟化、TCP/IP 网络（路由、交换）、并行化（MPI, PVM）、防火墙安全、编程（Fortran, C, Pascal, Perl）、SAP Basis 咨询以及 Web 技术（HTTP, HTML, CGI）。他是红帽认证工程师、VMware 认证专业人士以及 SAP 认证技术顾问。他拥有内梅根大学的理论物理学博士学位。

Nick Lassonde 是 Versora 的首席软件架构师，在那里领导 Progression Desktop 的开发工作，这是一个在 Windows 和 Linux 桌面环境之间迁移个性化数据的领先自动化工具。在加入 Versora 之前，Nick 曾担任 Miramar Systems 的高级架构师，主要负责用于移动关键数据和自动化测试程序配置的工具开发。在 Miramar 之前，Nick 担任 Cadence Design Systems 的软件架构师，专注于 Microsoft 与 Linux/UNIX® 工作站之间的互操作性问题。

Ben Li 是 Useful Corporation 的创新与拓展副总裁，在那里负责监督多站 Linux 系统的集成软硬件解决方案的开发。他的技术经验包括在学术环境中 Linux、Windows 和 OS X 操作系统上的安全和系统管理角色、开发和完善内容管理系统及工作流，以及在线和跨媒体出版。Ben 还是创新研究中心（The Center for Innovation Studies）的研究员，这是一个总部位于卡加利的创新和研究商业化社区的研究与倡导团体，他拥有卡加大学的两个学位。在加入 Useful 之前，Ben 曾为一家跨国业务服务公司开发过帮助台通知系统，还为一家领先的加拿大能源公司开发了基于数据库的公共关系跟踪和报告系统。

Kurt Taylor 是位于德克萨斯州奥斯汀的 IBM Linux 技术中心的高级软件工程师。Kurt 目前是 Linux 系统管理团队的技术领袖。他在 IBM 工作了 10 年，在架构、设计和开发分布式网络及系统管理产品方面拥有超过17 年的行业经验。他目前正在与 OpenPegasus 项目和 OSDL Desktop Linux 工作组合作。Kurt 毕业于北德克萨斯大学，获得计算机科学学士学位。

## 致谢

这是本 IBM 红皮书的第二个版本。IBM 红皮书团队想要感谢编写此书第一版本的作者团队：Chris Almond, Art Cannon, Jeroen van Hof, Christian Patsch, Sekkar Vaddadi, Oliver Mark 和 Thomas Schaller。他们在第一版本中所做的努力帮助创建了这本书的原始概念，并奠定了许多仍出现在第二个版本中的大量内容。

此外，团队还感谢以下为该项目提供过重大支持的人员：

- Greg Kelleher，全球 Linux 桌面策略和市场开发高级计划经理：感谢他赞助项目并帮助指导书籍大纲和范围的开发。

- Stephen Hochstettler，ITSO 项目和 Linux 团队负责人：感谢他的远见和支持。

- John Bergland，ITSO 项目负责人，Lotus 和 WebSphere Portal 负责人：感谢他的贡献。

- Bernard Golden，感谢他的贡献。

- Gerry Anderson, Jim Zemlin, 和 Dirk Hohndel，来自 Intel Inc.

- Mike Sheffey, Jon Walker, 来自 Versora Inc., 以及 Timothy Griffin, 来自 Useful Inc.

- Gerry Rivers, Jonathan Blandford, Chris Blizzard, Dan Walsh, Nickell, 和 Máirin Duffy，来自 Red Hat, Inc.

- IBM ITSO 专业人员：Erica Wazewski（法律支持）以及 Leslie Parham 为书籍准备出版所提供的支持。

## 成为出版作者

加入我们为期二至六周的驻留计划！帮助编写涉及特定产品或解决方案的 IBM 红皮书，同时获得前端技术的实践经验。你将与 IBM 技术人员、合作伙伴和客户组成团队。

你的努力将有助于提高产品的接受度和客户满意度。作为奖励，你将在 IBM 开发实验室建立人脉网络，并提高你的生产力和竞争力。

了解更多关于驻留计划的信息，浏览驻留索引并在线申请：

http://ibm.com/redbooks/residencies.html

## 欢迎意见

您的意见对我们非常重要！

我们希望我们的红皮书能够尽可能提供帮助。请通过以下方式向我们提交关于本或其他红皮书的意见：

- 使用下处的红皮书反馈表单：

http://www.redbooks.ibm.com/

- 通过电子邮件发送您的意见至：
redbook@us.ibm.com

- 邮寄意见至：
IBM Corporation, International Technical Support Organization
Bldg 905, 3D-004
11400 Burnet Road
Austin, Texas 78758-3493

## 第一部分

## 选择 Linux

本书的第一部分包括：

- 第1章“引言”，位于第1页
- 第2章“迁移的理由”，位于第25页

## 引言

多年来，许多从事计算和互联网的人们一直希望 Linux 能够成为更广泛通用用户的可用操作系统选择。与此同时，人们对微软目前主导的商业桌面操作系统的问题和局限性感到日益挫败。反之，这种挫败感推动了市场对替代桌面操作系统选择的需求。同时，由于开源开发运动的包容性和开放动态，基于 Linux 的桌面型发行版已经有了巨大的改进。

本书的目标是为考虑迁移到 Linux 个人电脑的 组织提供技术规划参考。对于 Linux，目前存在大量的“如何做”信息，可以解决特定的且非常技术的操作系统配置问题、特定平台的安装方法、用户界面定制等。本电子书包含了一些技术性的“如何做”内容，但本书内容的整体重点是引导读者了解在迁移项目过程中可能遇到的重要考虑因素和规划问题。在现有 Microsoft Windows 环境的基础上，我们试图为完成向 Linux 客户端成功迁移所需的挑战和方法提供一个更全面的端到端视角。
