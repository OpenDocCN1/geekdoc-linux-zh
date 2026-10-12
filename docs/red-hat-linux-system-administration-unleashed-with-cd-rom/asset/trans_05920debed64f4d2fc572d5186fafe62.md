
## 总结 Centennial 的资源

在一封发送给 Bynari 的电子邮件中，Mike Caron 提供了以下信息：

> > Centennial 学区由 1 所高中、1 所初中、6 所小学、1 所另类学校、1 栋行政楼、1 栋维护/运输/餐饮服务楼以及一个技术中心（容纳 Mike Caron 及相关人员）组成。

> > 每栋建筑都拥有一个局域网，由内部光纤主干、CAT 5 以及至少 2 个集线器机架支持（高中有 7 个）。

> > 高中和初中各有一台建筑文件服务器和一台图书馆服务器。小学在其建筑文件服务器上运行图书馆系统。维护楼和技术中心各有自己的服务器。

> > 学区还拥有一个邮件服务器（Novell Groupwise）和一台运行 Novell 网络服务器软件的 Web 服务器。

> > 所有服务器（通常为带 RAID 的 Compaq）均运行 Novell 4.11，唯一例外是 2 台专用图书馆服务器（配备多台 CD 驱动器的 IBM），它们仍使用 3.12。

> > 工作站为办公和行政用途的 Pentium 级 PC，以及供教师、教室和学生实验室使用的各种 Mac。小学实验室通过 Localtalk 连接到实验室 AppleShare 服务器，该服务器运行着通往建筑局域网的以太网网关。

> > Microsoft Office 97 是办公标准套件。

> > 每栋建筑都有一台 Bay Networks 多协议路由器、Kentrox CSU 以及一条通往我们教育服务区的 T1 链路。服务区提供所有 Internet、会计、学生记录和 WAN 服务，包括防火墙。

> > 我们的目标是降低 Novell 产品的高成本和高维护费用。

> > 我们希望用 Linux 替换所有 Novell OS，用 POP3 替换 GroupWise，用 Apache 替换 Novell 的 Web 服务器。用户访问共享应用程序和数据时变化最小。

> > 我们计划从技术中心服务器开始，然后扩展到最近的建筑物及更远的地方。系统地一次改造一栋建筑。

> > Centennial 还计划与 US West 实施 PVC，以建立我们自己的帧云，以便更好地管理 WAN 上的流量。

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
