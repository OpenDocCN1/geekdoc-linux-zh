
## 摘要

本章试图消除内核构建过程中的一些神秘感。虽然你必须对硬件有相当多的了解才能自定义内核，但它不是黑魔法或高雅艺术，只是知道在哪里查找适当信息的问题。构建 Linux 内核与构建任何其他复杂软件包没有更困难，不应引起恐惧。通过采取一些简单的预防措施，你可以安全地修改内核以获得特定需求的最佳性能。

## 36 章节
### Centennial学区，波特兰，俄勒冈州
### 本章内容
- 关于Centennial的背景 1136
- Red Hat 6.0 与互联网 1144
- Web服务器 1147
- 使用Samba进行网络身份验证、访问和用户管理 1148
- 在Linux环境中联网Macintosh计算机 1152
- 对网络的有限管理控制和访问 1153
- 使用IP伪装 1155
- 电子邮件 1156
- 系统管理 1158
- 管理用户和组 1159
- 使用TCP Wrappers进行内容管理 1161

本案例研究涉及Centennial学区从Novell 4.11域迁移到Linux Enterprise。该学区的计算机资源涵盖了各种Macintosh计算机、Microsoft Windows 95/98计算机和Novell NetWare的异构平台环境。该学区在Michael Richards加入IT部门并说服David Pierce访问波特兰大学的生产Linux部署后决定迁移到Linux。

在大学里，高级系统管理员Kent Thompson提供了充足的证据证明Linux是一个稳定、多功能且易于管理的网络解决方案。他首先演示了他部署的拓扑结构以及Solaris、Windows、Macintosh和DOS平台之间的互操作性。接下来，他向Centennial工程师展示了Centennial网络所缺乏的强大功能、可靠性、安全、远程访问和远程管理。当Kent通过用备用Linux机器替换宕机的工作站来演示快速业务连续性时，David和Michael能够在他们的企业中可视化Linux。

David和Michael将他们所学的信息带回给网络系统经理Mike Caron和媒体与技术主管Connie Freeman。在这次初步会议中，Michael和David提出了将Linux作为迁移路径的有力商业案例。

在继续通过额外的研究和分析报告验证Linux商业案例的发现的同时，David和Michael访问了Riverdale学区的Paul Nelson。Paul向他们展示了所有Riverdale服务都运行在两台Linux服务器上。他还讨论了他与NetWare和NT服务器遇到的问题，同时展示了他的Linux机器的性能。他向他们展示了他的Linux服务器已连续运行18个月而无需重新启动。David和Michael离开时已确信无疑。

Connie Freeman将部门的商业案例提交给助理学监，后者批准了该举措。Centennial的IT部门获得了迁移到Linux的许可。现在，他们需要的是 know-how。

## 关于Centennial的背景
Centennial学区成立于1976年，由旧的Lynch学区和Centennial高中合并而成，后者此前是邻近Gresham学区的一部分。1993年，该学区增设了Centennial学习中心，一所替代高中。

该学区计算机数量从几台Apple II增长到1998年的约1,600台Mac和PC。1995年，该学区使用通用服务器建立了Novell域。Mike Caron告诉我们，自那以后，所有旧服务器都已更换为Compaq。

技术部门源于几位志愿教师在20世纪80年代初开始使用Apple和IBM个人计算机的努力。随着学区的发展并开始购买额外设备，出现了共享资源的需要。

## Bynari如何参与
在七月，Mike首次联系我们之前，该学区派出了三名技术人员前往犹他州参加为期一周的Linux集训。参加者包括Mike Caron、David Pierce和Michael Richards。在为期一周的时间里，员工们尝到了Linux的味道，但他们并不觉得自己有足够的经验从Novell切换到Linux。

前一个夏天，担任高级技术主管和CNE的David Pierce领导了一个项目，将学区所有服务器从Novell 3.11升级到4.11版，以便学区能够利用新服务器上使用的多个功能。他知道迁移平台所涉及的工作量，他想要帮助。

在接下来的几年里，技术中心因需要管理新服务和与以往不同的一系列问题而变得紧张和压力重重。在访问波特兰大学和Riverdale后得到说服，Mike Caron决定是时候迁移了。

Mike Caron开始寻找顾问来帮助学区迁移。他向Bynari的支持中心放置了一级服务呼叫并询问了额外的服务。

Bynari的技术总监发现Mike Caron是一个令人愉快的人，但他并不觉得自己能够缓解Mike对转向新系统，尤其是与他习惯的Novell世界截然不同的系统的挫败感和焦虑。因此，双方花费了大量时间和多次通话来回答有关迁移到Linux以及如何管理项目的问题。

大约讨论了五个小时后，Mike问Bynari是否有人可以前往波特兰帮助建立Linux测试域并培训他的员工。Bynari的技术经理在知道客户需要专业项目管理帮助的情况下，对派遣培训师前往波特兰感到不安。

## 从达拉斯到波特兰
援助请求在八月下旬到来，当时Mike处于沮丧状态。他两个月前提出了关于Linux的商业案例，他的上级已向上级指挥链获得批准，现在他需要展示成果。

Bynari的技术经理自愿亲自监督该项目，并要求Bynari的资深合伙人之一Nicholas Donovan与他同行。没有时间似乎是合适的。Nick的承诺延伸到遥远的未来。尽管如此，他知道如果不在他的日程中腾出时间，他永远不会腾出时间，而Mike需要他的帮助。

Connie Freeman安排了Bynari顾问的旅行和住宿。她还安排行程在周末进行，这对Bynari的顾问有所帮助。几名Bynari的同事在团队从波特兰返回前承担了额外的责任。

## Connie提供的书面需求
Connie Freeman列出了一份需求清单。她写道：

> 我们希望解决的问题包括：
> - 配置文件类型、用途、位置
> - 安装Red Hat 6.0；应用更新和补丁
> - 讨论与Compaq RAID配置相关的概念
> - 构建两台Compaq服务器（到访前已完成一台）
> - 在两台服务器之间配置离线WAN；讨论路由问题
> - 配置两台Win95客户端
> - 配置DHCP并讨论相关问题
> - 配置IP伪装服务及相关问题
> - 讨论电子邮件管理；安全选项—FTP等。
> - 讨论Macintosh问题

## 项目团队的顾虑
Centennial学区实施团队由网络服务经理Mike Caron、技术经理Dave Pierce、助理系统管理员Michael Richards以及担任管理联络的Connie Freeman组成。Bynari团队由Tom Adelstein和Nicholas Donovan组成。

Centennial独立学区展现了我们在任何大型企业中都能找到的大多数元素。首席技术官在面对企业每天看到的部署障碍的同时建立了出色的企业网络设施。David Pierce在上个夏天升级Novell的经历后，对更换操作系统感到担忧。

Michael Richards担心员工在新平台上需要多少培训。他表达了对支持呼叫和增加工作量的担忧。

Bynari团队到达后，Centennial团队与他们举行了“棕色纸”会议。Bynari的项目经理使用贴在会议室墙上的牛皮纸向每个人讲解项目计划。 within an hour，团队有了方向、时间线、任务、可交付成果和迁移路径。表36.1描绘了“棕色纸”会议的笔记。

## 表36.1 工作分解结构

| 步骤 | 现状 | 目标 | 需求 | 范围 |
|---|---|---|---|---|
| 需求 | Novell 4.11 (NDS) | Linux | 身份验证 | 生产系统 |
| 约束 | 本地服务器 |  | 主目录 | 用户配置文件 (skel) |
| 规格 | 路由器 | 邮件 | 邮件组和用户 | 客户端访问，Windows，Mac，Linux |
| 范围 | T-1接入/帧中继 | 消息传递 | POP3 IMAP SMTP LDAP | 邮件 |
| 文档 | 帧中继 |  |  |  |
| 项目计划 | 10 mbps 集线器 | 调度 |  | 备份 |
| 任务清单 | Groupwise | 网络打印 |  | 用户管理 |
| 里程碑 | Compaq Proliants | 备份 |  | Kick starting |
| 时间线 | 管理工具 | DHCP | Web服务 | 防火墙 |

## 总结 Centennial 的资源

在一封发送给 Bynari 的电子邮件中，Mike Caron 提供了以下信息：

> Centennial 学区由 1 所高中、1 所初中、6 所小学、1 所另类学校、1 栋行政楼、1 栋维护/运输/餐饮服务楼以及一个技术中心（容纳 Mike Caron 及相关人员）组成。

> 每栋建筑都拥有一个局域网，由内部光纤主干、CAT 5 以及至少 2 个集线器机架支持（高中有 7 个）。

> 高中和初中各有一台建筑文件服务器和一台图书馆服务器。小学在其建筑文件服务器上运行图书馆系统。维护楼和技术中心各有自己的服务器。

> 学区还拥有一个邮件服务器（Novell Groupwise）和一台运行 Novell 网络服务器软件的 Web 服务器。

> 所有服务器（通常为带 RAID 的 Compaq）均运行 Novell 4.11，唯一例外是 2 台专用图书馆服务器（配备多台 CD 驱动器的 IBM），它们仍使用 3.12。

> 工作站为办公和行政用途的 Pentium 级 PC，以及供教师、教室和学生实验室使用的各种 Mac。小学实验室通过 Localtalk 连接到实验室 AppleShare 服务器，该服务器运行着通往建筑局域网的以太网网关。

> Microsoft Office 97 是办公标准套件。

> 每栋建筑都有一台 Bay Networks 多协议路由器、Kentrox CSU 以及一条通往我们教育服务区的 T1 链路。服务区提供所有 Internet、会计、学生记录和 WAN 服务，包括防火墙。

> 我们的目标是降低 Novell 产品的高成本和高维护费用。

> 我们希望用 Linux 替换所有 Novell OS，用 POP3 替换 GroupWise，用 Apache 替换 Novell 的 Web 服务器。用户访问共享应用程序和数据时变化最小。

> 我们计划从技术中心服务器开始，然后扩展到最近的建筑物及更远的地方。系统地一次改造一栋建筑。

> Centennial 还计划与 US West 实施 PVC，以建立我们自己的帧云，以便更好地管理 WAN 上的流量。

> "我们有以下服务器清单[见表 36.2]："

### 表 36.2 现有设备

| 数量 | 类型 |
|---|---|
| 2 | ProLiant 800—128MB RAM, Smart 2 SL 控制器, (3) 4GB 硬盘, 4/8GB HP DAT 磁带。 |
| 3 | ProLiant 1200—256MB RAM, Smart 2 SL RAID 控制器, (3) 4GB 硬盘, 12/24GB Compaq DAT 磁带 |
| 8 | ProLiant 1600—256MB RAM, Smart 2 SL RAID 控制器, (3) 4GB 硬盘, 12/24GB Compaq DAT 磁带 |
| 2 | ProLiant 2500—256MB RAM, Smart 2 SL RAID 控制器, (3) 9GB 硬盘, 12/24GB HP DAT 磁带 |
|  | 除少数磁带驱动器外，所有组件均为“纯 Compaq”。 |
|  | LAN/WAN 备份：Seagate Backup Exec，单机和企业版许可证。 |

## 组织倡议

在与 Connie Freeman 的一次访谈中，Bynari 的顾问了解到“The Centennial Independent School District’s primary initiative focuses on improved learning and real world experience which involves communication, research and tapping real world resources. The ability to find real professionals and real world challenges interests us.

> "当技术能够促进该倡议的实现时，学区会为教职员工和学生使用技术。今天，学区认为部署互操作性和通信是最有效和最高效的方式来促进其倡议。"

## Centennial 选择 Red Hat

经过对各种发行版的多次测试后，技术团队将选择范围缩小到 Red Hat 6.0 和 Mandrake 6.0。他们认为 Red Hat 是实施其网络的最佳方式。虽然 Mandrake 与 Red Hat 6.0 兼容，但 David 选择在其 Compaq 服务器上安装 Red Hat。

Red Hat 轻松安装在 Compaq 服务器上，在其 Smart 2 RAID 上创建了可引导分区，并以很少的问题进行条带化。Michael 选择使用 Mandrake，因为它与 Red Hat 类似，并且为他提供了 KDE 办公桌面。

## 挑战

Bynari Systems 于 1999 年 7 月介入该学区，当时 Mike Caron 调查了支持和专业服务的市场。为了测试 Linux 行业的各家公司，他进行了支持电话并要求有人联系他。

Mike 对支持行业中的几种做法表示反对：首先，他无法为长期捆绑的支持事件提出案例。其次，他在使用电话支持时需要立即响应。最后，他希望在做出任何承诺之前亲身体验与支持技术人员的合作。

在许多方面，Bynari 的结构适合他的情况。Bynari 立即开始帮助他进行支持电话。Bynari 按事件收费并保证其工作。换句话说，除非在几分钟内通过电话解决问题，否则他无需付款。

其次，Bynari 接受开放式发票，这意味着它仅在客户使用服务时才向客户开具账单。最后，Bynari 的支持团队不需要超出当前支持电话的承诺。

## 引入 Linux 和 Red Hat 6.0

Centennial 的不成文主题在每项已完成的工作中持续回响。

技术存在是为了教师及其学生的利益。如果技术能够促进能力的提升，那么它就受欢迎。Dave 和 Mike 表示，当他们提供一流服务时，在学生、教职员工和管理员中遇到的阻力很少，支持很大。

Centennial 在 1999-2000 学年的技术预算目标集中于及时分发更可靠的支持物流。在这种情况下，网络通过改进的通信、Intranet 工具和打印共享，Internet 访问只有在促进更好教育时才有价值。

从教育背景来看 Centennial 的项目时，需求变得清晰。如果一个流程没有增加价值，它就不属于这里。

团队问道，“媒体和技术部门需要做什么才能实现学区的目标？”

首先，技术部门必须获得一套生产力套件来取代 Novell 的 Groupwise。替换应用程序需要覆盖每位教职员工和行政人员。每位教师都必须使用其生产力套件有效地帮助推动学生实现更好的教育结构。

一旦教师确定了其班级的需求，他或她就必须找到并使用适当的教学材料。然后每位教师都可以制定自己的课程计划。

## 课程的互联网

教师发现 Internet 提供了满足其需求的高效有效媒介。Centennial 确定他们可以使用高速 Internet 访问来帮助实现其主要倡议。

Centennial 的技术管理员看到了过滤内容并为学生用户提供安全措施的需要。教学界反对限制。

技术部门发现企业级防火墙和过滤软件成本高昂，尤其是当学校教学管理要求免费访问 Internet 时。Linux 防火墙在成本可能成为障碍的情况下提供了真正的替代方案。

## Red Hat 6.0 帮助 Centennial 满足需求

Dave 喜欢 Red Hat 6.0，因为它功能强大且易于安装。学区购买的 Compaq 服务器以及最便宜的计算机都具有与 Red Hat 兼容的硬件。Red Hat 提供了视频驱动程序，使最新的计算机采购能够与 Linux 配合使用。

一旦安装了 Red Hat，性能较慢的计算机的表现超出了每个人的预期。这为原本无法获得计算机课程的学生提供了潜在系统。

在学术上，学习使用 Linux 这种类 UNIX 操作系统对毕业生来说比学习由 Microsoft 和 Novell 专有域网络基础提供的文字处理和电子表格程序更有价值。

## Red Hat 6.0 与 Internet

Linux 的一个关键特性提供了通过防火墙以低成本管理内容和网络访问的解决方案。术语“防火墙”源自汽车上使用的防火墙。防火墙可保护车厢内的乘员免受发动机舱火灾的影响。

网络上的防火墙可保护其后本地网络上的用户和数据免受未经授权的入侵。它还可以用于阻止本地网络用户连接到禁止访问的站点。

Linux 中存在两种防火墙。每种类型都有两个子类型。两种基本类型包括“数据包过滤器”和“代理”防火墙。

数据包过滤防火墙可以是以下类型之一：

- **转发** — 对于这种数据包过滤器，防火墙的决策关系到是否将数据包转发到 Internet。
- **伪装** — 这些防火墙可以重写数据包头中的源地址和目标地址，以防止外部人员获知内部网络的地址和拓扑结构。

代理防火墙可以是以下类型之一：

- **标准** — 对于这种代理防火墙，私有网络上的工作站连接到服务器。工作站的数据包通过一个特殊端口或开口，然后通过另一个端口被重定向出去。
- **透明** — 对于这种防火墙，工作站不使用特殊端口。防火墙软件代理或代表工作站，通过连接透明地发送和返回数据包。

Red Hat 6.0 随附的 Linux 内核已预编译，包含学区利用数据包过滤所需的一切功能。网络管理员通过现代 Linux 内核的功能实现防火墙。Centennial 选择启用 IP Chains 将其私有网络伪装在防火墙之后。他们还选择使用代理服务器来限制对私有网络的访问以及从私有网络的访问。

## 定义其他需求

Centennial 深刻意识到对集中管理、可扩展性、本地网络分离以及业务连续性的需求。

概括而言，技术部门的需求包括

- 1. 部署分布式应用程序
- 2. Internet 连接
- 3. 增强的安全性和内容管理
- 4. 集中管理

## 约束条件

Centennial 在诸多约束条件下工作，并非全部是预算方面的。一些约束与设施有关，以及学生和教职员工以及其他学校员工的计算机素养。Centennial 如同所有学区一样，因资金问题和财政管理而面临预算约束。Internet 内容访问问题尚未解决，阻碍了技术管理部门就内容管理做出决策。

## 技术专长与知情管理

Centennial 面临教职员工、行政人员和学生群体中缺乏计算机人才的问题。技术部门主要由 Dave Pierce、Mike Caron 和 Michael Richards 组成。

该团队必须提供规划、网络管理、应用支持和应用开发。学区管理部门还期望他们提供桌面支持、识别需求、寻找外部资源、提交需要充分论证的采购请求，并维护物理设施。

## 项目规范

将 Centennial 的技术需求与其约束条件结合起来，Mike 可以开始制定规范文档。例如，需求 #1 指出 Centennial 必须部署分布式应用程序。当 Mike 加入稳定可靠、低维护和资源稀缺的约束条件后，规范变为

- 1. 通过网络部署稳定可靠、低维护的应用程序，使用分布式用户界面。
- 2. 使用局域网提供稳定可靠、低维护的 Internet 连接。
- 3. 提供稳定可靠、低维护的内容管理和安全。
- 4. 提供易于使用的集中网络管理。

此时，Centennial 只能从宏观角度看待该计划。完整的规范文档要求有人识别可用的平台，如硬件和操作系统、应用程序、资源和用户界面。

当企业计划的规范被定义后，项目计划可以形象地“从文档中落出”成为任务清单。就 Centennial 而言，技术部门需要处理的领域太多，以至于一份已开始的不完整项目清单就充当了任务清单。

## 短期和长期目标

在尝试了许多操作系统后，Dave 将 Linux 定义为他首选的操作系统。他希望迈出下一步，激活他的网络。

学区的长期目标包括将高级计算机科学引入课堂。俄勒冈州的许多学区已教授计算机科学课程数年。Centennial 教授的第一批课程是文字处理和电子表格。

学区希望在课程中加入系统管理、网络和编程。然而，技术部门担心向可能破坏安全和资源的学生开放其资源。

学术界与网络管理员之间利益冲突的解决，将通过在课堂上引入更高层次的课程，同时允许技术部门管理企业资源来实现。

## 项目计划

学区将本学年的项目定义为部署可管理的网络平台。Dave 简称其为 Linux 项目。

为了完成 Dave 的生产力应用程序并将其分发给教职员工，他需要一个平台中立的图形界面。拥有一个可用的 Web 启用应用程序后，Centennial 需要通过 Web 服务器为每位教职员工提供安全访问。

使用 Internet 技术在内部向用户群交付应用程序意味着 Dave 需要一个内部网。

## Web 服务器

Red Hat 随 Red Hat 6.0 分发 Apache Web 服务器。该服务器默认已安装并配置好。此 Web 服务器用于在 Red Hat 6.0 桌面级别处理在线帮助请求和在线文档。用户还可以部署其 Apache 服务器与本地网络用户共享文档或 Web 应用程序。

本地用户可以从 Apache Web 服务器访问 HTML 文档。他们在 Web 浏览器中指定主机计算机的 IP 地址或本地网站的 URL 以访问文档。

Red Hat 6.0 中最基本但也很重要的服务之一是 Web 服务器。Apache 具有许多可配置的不同功能。对基本 Web 服务器进行的众多修改和扩展提供了一种出人意料的灵活机制。

## 保护应用程序访问

Centennial 在 Apache 上可用的配置修改选项包括

- **授权**—确定客户端是否被允许访问特定网站的过程。
- **访问控制**—基于客户端或用户的授权，允许或阻止访问特定网站对象 的过程。
- **基于主机的授权**—根据客户端的主机名或 IP 地址控制对网站或其部分的访问。
- **基于用户的授权**—根据用户身份控制对 Web 应用程序的访问。
- **身份验证**—确定远程用户身份的过程。在 Red Hat 6.0 中，这涉及让用户提供姓名和密码，只有授权用户才知道。

基于主机的授权提供了一个有吸引力的方面。用户和管理员认为它简单且不具侵入性。使用基于主机的授权，授权客户端的过程对用户完全没有影响。

基于用户的授权要求用户输入姓名和密码以访问网站或目录。基于用户的授权提供最安全可靠的安全性。不幸的是，它需要系统管理员付出额外的工作。

Centennial之所以做出这种权衡，是因为生产力套件所涉及的数据具有敏感性。生产力套件设施的应用程序完整性要求尽可能高的安全性。这确保了数据不会被泄露。

Centennial通过定义用户组以及用户本身来减少管理职责。通过管理用户集合，系统管理员为 Apache 使用定义了一个组文件。这通过将用户放入组定义中消除了定义个人访问权限的需求。

## 使用 Samba 进行网络身份验证、访问和用户管理

为了身份验证服务和网络管理，Centennial 需要使用 smb 协议。Samba 是一个适用于 Linux 的开源软件包，提供对 Windows 95/98 和 Windows NT 使用的协议的支持。

Samba 允许 Windows 客户端以与访问 Windows NT 服务器类似的方式访问 Linux 系统的文件和打印功能。

选择随 Red Hat 6.0 包含的 Samba 包使 Centennial 节省了资金。该学区无需按用户或席位支付许可费即可提供基本的 NT 服务。使用 Samba 的优点包括

- 稳定可靠的解决方案。Linux 上的 Samba 为该学区提供了本应使用 Windows NT 部署的默认服务。同样，Linux 解决方案不需要用户许可费。
- 管理时间更少。

在 Centennial 的主身份验证服务器上，技术部门从 Red Hat 6.0 安装了 Samba 和 sambas rpms。在 2.05 版本下，Samba 可以充当域控制器。在之前的版本中，Samba 不能作为域控制器对用户进行身份验证。Red Hat 通过将此应用程序添加到 Red Hat 6.0 提高了 Red Hat 6.0 的功能。

## Samba 在 Centennial 的异构环境中

Samba 的开发人员创建了一套程序，允许类 UNIX 操作系统如 Linux 与 Microsoft 主机通信。Microsoft 使用一种称为 NetBEUI 的协议，该协议实现了网络通信的服务器消息块。由于 Centennial 的许多工作站运行 Windows 95/98，因此为了使用 Linux，实现 Samba 变得必要。

## 培训 Centennial 团队

为了举例说明 Bynari 如何指导 Centennial 团队，我们将使用 Samba 配置来演示 Bynari 的方法。Mike Caron 解释道：

> 我们最初在未将服务器设为 NT 域服务器的情况下开始 samba 安装。我们学习了如何创建 Linux 用户，以及如何从现有的 Linux 用户创建 samba 用户。然后我们编辑了 `/etc/hosts` 文件以包含我们的 samba 客户端的 ip 地址。这是因为我们尚未准备好在测试局域网中实施 DNS 服务。然后编辑 `smb.conf` 以设置磁盘共享。

> 以下步骤是我们用于在 Linux 服务器上安装 Samba 并创建 NT 域的一般指南。

- 第一步是下载 Samba 最新稳定的 RPM 然后安装它。`rpm -Uvh <rpm name>`（“U”代表“upgrade”升级）
- 接下来创建一个公共目录，并使用 chmod 使所有用户拥有完全访问权限。
- 我们执行 `mkdir /home/pub` 然后 `chmod /home/pub 777`。
- 我们编辑了 `/etc/hosts` 并为 `/home/pub` 目录创建了一个公共共享。
- 我们将模板 `smb.conf` 文件复制到 `/etc` 目录并根据特定服务器、域名以及任何其他特定设置进行编辑。
- 现在运行 `linuxconf` 编辑服务器的一些特定网络设置。
- 选择 Browse Master=yes，Local Master=yes，os level=65（稍后 Domain Master=yes，os level=255）
- 选择 Synchronize Linux from SMB passwords（是）
- 创建 Linux 用户，必要时使用 `adduser`，然后为任何想要访问此 samba 服务器的用户创建 Samba 用户 `smbadduser`。

> "现在配置 Windows 工作站。将网络邻居属性更改为以下内容："

- Identification 选项卡更改为新的工作组（csd28）
- Access Control 更改为 Share 级访问控制
- Client for Microsoft Networks 属性更改为新工作组（csd28）
- TCP/IP 属性
  - IP Number: 192.168.3.10（最初，任何静态号码）
  - DNS Configuration:
    - Domain: mtc.net
    - Host:
    - DNS Search Order: 最初禁用 稍后添加 192.168.3.15（MTC 代理服务器，它是 ESD 服务器）
    - Gateway: 198.236.3.1
- 打开 File & print sharing
- 在 `c:/Windows/LM Hosts` 文件末尾添加 192.168.3.15 CSD28（ip & 工作组）
- Reboot

Bynari 的方法使用渐进式来教管理员如何配置任何服务。在 samba 过程开始时，Centennial 团队只执行了一个功能。他们创建了一个名为 "guest" 的用户，并将该用户添加到 Linux 密码文件和 smbpasswd 文件中。他们还配置了一台 Windows 98 系统以登录到 Samba 服务器。他们将 Windows 信息添加到 Linux "hosts" 文件并对 `smb.conf` 进行了条目。

一旦团队在简单的 guest 共享上取得成功，他们就增加了功能，直到测试 LAN 具有域身份验证、动态主机配置协议（DHCP）、邮件以及通过 Linux 防火墙浏览互联网的能力。

## 回到 Samba

Samba 2.0 引入了一个程序，可通过 Web 浏览器协助设置和管理 Samba。人们将该程序称为 SWAT，即 Samba Web Administration Tool。有鉴于 Centennial 资源有限，技术部门需要一种简单的方法来为 Microsoft 工作站提供管理。Red Hat 6.0 在其发行版中提供了 SWAT。

为了在 Red Hat 6.0 中启用 SWAT，技术部门使用了“inetd”方法，该方法不需要 Web 服务器。在此方法下，Samba 的各个组件可通过 Web 浏览器进行配置和维护。尽管 Red Hat 6.0 提供了 Samba 和 SWAT，但系统管理员必须对其进行配置。

Samba Web Administration Tool 对相对较新的 Linux 网络管理员提出了相当大的挑战。在安装 Samba 2.05 时，安装程序会自动在系统的 `inetd.conf` 文件中放置一个条目。

在配置 Samba 时，管理员必须打开配置文件并删除该文件中 SWAT 条目前面的注释符号（#）。删除注释允许在系统启动过程中调用 Samba。

接下来，管理员必须在系统服务文件中将 swat 作为服务输入。该文件的名称 simply 为 services，它位于 `/etc` 目录中。使用文本编辑器，管理员打开文件并找到端口号允许“900”系列条目的部分。SWAT 在此配置文件中需要的条目是 `swat 901/tcp #swat`。

一旦条目完成，管理员必须重新启动服务以使更改生效。通过使用命令 `/etc/rc.d/inet.d/inetd restart` 系统启用 SWAT 以供使用。在 root 用户的命令行提示符下执行此命令时，他或她会看到一系列与启动计算机时看到的类似的条目。然后管理员可以打开他的 Web 浏览器并访问 SWAT 界面。

管理员输入 `http://localhost:901`，SWAT 界面在浏览器中打开。通常在第一次看到 SWAT 界面时会伴随着惊讶感，在 Centennial 的情况下也是如此。

突然间，在比喻的隧道尽头看到了光明。由 Dave 及其团队组成的小组在前往另一房间的工作站并从远程浏览器访问 SWAT 时，对远程管理可能性产生了更大的兴趣。

一旦管理员在 Centennial 的 Compaq 服务器上配置了 Samba，他们就为其 Windows 工作站启用了打印服务。

## 使用 Samba 的全局打印服务

Linux 管理员在 Samba 服务器上配置了一个 Public 目录。管理员创建了一个公共共享和按用户为基础的私有共享，并使所有用户都能访问由 Samba 服务器控制的共享打印机。这使得一台运行 Linux 操作系统的计算机能够提供共享 Samba 打印以及其他服务，例如安全 Web 服务和用户身份验证以访问网络。

## 使用 Samba 从 Windows PC 访问 Red Hat 6.0 系统

管理员必须为每台 Windows 工作站提供桌面支持。每台 PC 的网络属性都必须手动配置。通过验证 Windows 网络和 TCP/IP 已安装并运行，他们可以开始与 Linux 服务器连接的过程。

管理员使用在 Samba 配置期间使用 Samba 用户名授予访问权限的相同用户名登录 Windows PC。然后他们在 Windows 桌面上打开了网络邻居。

Linux 系统出现在列表中，对 Windows 用户而言看起来像网络上的另一台 Windows 计算机。在 Windows 95/98 网络邻居中右键单击 Linux Samba 服务器图标并选择属性后，标题显示为 Windows Print and File Services。

然后管理员双击 Linux 系统，并在提示时输入 Linux 用户密码。管理员和用户可以根据需要浏览 Linux 文件系统。

现在，用户可以将驱动器映射到特定的 Linux 目录，右键单击该项目并从弹出菜单中进行选择。通过从 Windows 95/98 系统映射网络驱动器，Windows 用户名将与 Red Hat 6.0 机器上的用户名相同。如果目录所有者授予权限，用户可以查看这些文件。

## 在 Linux 环境中联网 Macintosh 计算机

Centennial 使用 AppleTalk 互连协议栈，它允许点对点网络模型，用于其 Macintosh 计算机的文件和打印机共享等功能。每台机器可以同时充当客户端和服务器，并且必要的软件和硬件都包含在每台 Apple 计算机中。

Centennial 使用了所有 Apple Macintosh 计算机和各种打印机上可用的 AppleTalk 网络系统和 TCP/IP。AppleTalk 协议套件包括使用 AppleShare 的高级文件共享、LaserWriter 打印服务和打印后台处理程序，以及低级数据流和简单数据报传输。

尽管 AppleTalk 一词最初既指协议也指连接电缆，但它已在不同介质上可用，因此 LocalTalk 用于描述用于将 Mac 连接到其他 Mac 或打印机的简单屏蔽双绞线电缆。

Centennial 使用以太网上的 EtherTalk，以便 AppleTalk 数据可以在不同的协议中传输，SNAP 和 TCP/IP 都用于封装。

Linux 提供完整的 AppleTalk 网络。Netatalk 是最初为 BSD 衍生系统开发的 AppleTalk 协议套件的内核级实现，包含对 AppleTalk 路由的支持，通过 AFP（AppleShare）提供 UNIX 和 AFS 文件系统服务，提供 UNIX 打印机服务，以及通过 PAP 访问 AppleTalk 打印机。

学区系统管理员希望访问网络上带有 EtherTalk 适配器的 LaserWriter 等 Mac 打印机。Mac 用户希望访问 Linux 可访问的任何打印机。为了在 Linux 下设置此类服务，管理员在两种情况下都使用了相同的程序。

在编译并安装 AppleTalk 软件 netatalk 之后，Dave 使用 `/etc` 目录中的 `rc.atalk` 启动了所有守护进程。在尝试配置打印机之前，我们确保 AppleTalk 服务正在工作。

使用命令 `/usr/local/atalk/bin/getzones` 使管理员能够查看所有 AppleTalk 区域是否对主 Linux 服务器可见。

> 使用命令行选项我们查明了我们所在的区域：

```
