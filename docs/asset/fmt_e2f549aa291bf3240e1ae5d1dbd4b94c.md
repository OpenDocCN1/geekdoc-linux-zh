
当你考虑 IT 基础设施时，你可能不会将电信需求包含在同一组中。然而，随着 IP IP（VOIP）的日益普及，语音流量正与数据流量并行传输。这种语音与数据的融合赋予了你许多自由，这些自由在过去仅限于模拟电话系统。`Asterisk` 是一个开源软件包，提供了一个中央交换核心，并带有四个 API 用于将电话系统模块化加载到单一交换网络中。

![](img/72e1c6125676a623b5032cfdab8d797c_273_0.png)

仅仅因为 `Asterisk` 服务器是一个开源项目，并不意味着它没有地方获得支持。`Asterisk` 项目的大量支持来自一家名为 `Digium` 的公司，该公司围绕 `Asterisk` 相关的服务和硬件销售开发了其业务。他们还是该软件的主要开发者，并将工作成果回馈项目。`Digium` 模式允许其他开发者为代码库做出贡献。`Digium` 为企业在通用 `x86` 服务器上利用开源软件提供了一个有力的理由。这降低了终端用户的成本，而这些用户可能会可能会使用

## 256 Linux 业务桌面迁移

来自 Nortel、Siemens 或 Lucent 等公司的单源软件和支持。软路交换机（soft PBX）还具有语音数据的迁移性，可以通过存档语音邮件或使用基于软件的电话来与 PC 交互。这为更多服务打开了大门，例如语音邮件存储和备份，或与个人信息管理器集成的增值软件包。

## 总结

Windows 和其他操作系统可以并已经提供了足够的后台服务来支持当今流行的桌面配置，但它们的功能并不仅于此。它们可能拥有你已经熟悉的熟悉的快速开发工具或管理界面。从逻辑上讲，你应该权衡培训和部署新系统的成本，但从长远来看，你可能会发现这些成本微乎其微。你还需要考虑席位许可以及你为 Windows Server 以及其他和服务工具支付的费用。没有适用于所有人的最佳方案，这正是开源的意义所在——通过权衡每个选项的优缺点来做出选择。

软件许可和获取成本是 Linux 的两个最大优势之一。操作系统是免费的，因此从软件许可的角度来看，初始所有成本比商业解决方案低一些。此外，开源模型允许组织根据需要评估和更改他们拥有的底层代码。与商业操作系统的另一个优势是，开源解决方案可以从满足特定需求的碎片组合而成，而不是要求用户接受用于解决各种问题的缩封装解决方案。相反，如果用户觉得从商业供应商那里获得了价值，他们可以从像 Red Hat、MySQL 或其他 这样的供应商处获取解决方案。

开放架构和基于标准的协议对于开源解决方案是有意义的。Windows 对开源解决方案的支持正在增长，但仍然落后于微软。随着开源进入企业领域，情况发生了转转。由于 Java 是一个例子。微软在 Java 上的诉讼导致了断裂。在建立新系统时可以减少旧系统的维护成本。

与专有系统的兼容性是开源解决方案的另一个问题。微软可能会向其产品中添加功能，使其难以交互。

## 其他资源

- Red Hat
- Novell
- Debian
- SELinux
- NFS
- Samba
- Postfix
- Exim
- Dovecot
- Cyrus
- Qpopper
- FreeSwan
- Squid
- SquidGuard
- SUSE
- Open-Xchange

## 258 Linux 迁移

- SquirrelMail
- eGroupWare
- Hula
- SpamAssassin
- IPCHAINS
- Netfilter
- Astar
- Coyote
- Fedora
- Linksys
- Apache
- Mono
- MySQL
- PHP Admin
- PPPSSH

## 参考文献

- Evans Data, “超过 90% 的 Linux 系统从未被病毒感染，”新的 Evans Data 调查。在线获取：http://www.evansdata.com/n2/pr/releases/Linux04_02.shtml，2005年4月27日。
- Fersht, Phillip，“异构 Linux、Windows 网络增加了集成挑战，”Yankee Group。在线：http://www.yankegroup.com/public/products/decision_note.jspID=13113，2005年5月20日。
- Hall, Mark，《计算机世界》（2003年10月13日）。在线获取：http://www.computerworld.com/datathetics/data/software/0/10810,85900.00.html，2005年5月24日。
- Howorth, Roger，《IT 周刊一个Samba 3 赢得 2003 年，”（2003年10月14日）。在线获取：http://www.itweek.com/news/1144312。
- Microsoft，Windows Small Business Server 2003 定价和许可。在线：http://www.microsoft.com/windowserver2003/sbs/howtobuy/pricing.mspx，2005年11月4日。
Netcraft, “April 2005 Web Server Survey.” 在线获取：http://news.net-craft.com/archives/2005/04/01/april_2005_Web_server_survey.html, 2005年4月27日。
Netcraft, “September 2001 Web Server Survey.” 在线获取：http://www.neteraft.com/Survey/index-200109.html#computers, 2005年4月27日。
Novell, SUSE LINUX Enterprise Server: 价格表（美元）。在线获取：http://www.novell.com/products/linuxenterpriseserver/pricing.html, 2005年4月27日。
Quandt, Stacy, “A Comparative Analysis of Linux vs. Windows Capabilities.” Quandt Analytics (2004年5月6日)。

## 数据迁移与备份

本章内容

- 格式转换
- 将数据从 Windows 桌面迁移
- 备份
- 总结
- 其他资源

将数据从一个平台迁移到另一个平台并不是一项愉快的任务，无论数据是从 Windows 移动到 Linux 桌面，还是从一台 Windows PC 移动到另一台。在两台 PC 之间移动数据不仅需要考虑各种因素，在迁移之前选择互补的文件格式也具有重要意义，以避免互操作性问题。数据迁移的步骤始于你对应用程序的选择；例如，如果你已经决定使用 `OpenOffice` 代替 `Microsoft Office`，那么在迁移到 Linux 桌面之前，你已经克服了一个相当大的障碍。从一个桌面移动到另一个平台的物理步骤并非易事，但可以结合你的备份方案来解决。这一策略有两个优点：第一，它能确保你在 Linux 迁移过程中遇到的任何小故障都不会导致数据丢失；第二，当你想要将旧 PC 重用为运行 Linux 的胖客户端，或者重用为数据会被迁移到服务器的瘦客户端时，它为你提供了一种迁移数据的方法。在从 Linux 迁移数据时，你应该考虑以下因素：

**格式转换：** 你需要首先调查如何将设置和文件转换为 Linux 可用的格式。例如，`Internet Explorer` 需要转换为 `Firefox` 或其他浏览器的书签；文字处理和其他文档现在需要用与 Microsoft 程序类似的原生 Linux 应用程序打开。在某些情况下，你可以继续使用相同的格式，因为大多数 Linux 办公套件可以以很高的可靠性打开 Microsoft 文档。然而，你应该考虑能够利用文档中所有格式的格式，即 `XML` 文档格式，如 `OpenOffice.org` 倡导的 `XML OpenDocument` 格式。你还可以采用归档策略，将文档转换为便携文档格式 (`PDF`) 以保留格式。

**数据迁移：** 物理移动应用程序数据将是你最具挑战性且最耗时的过程之一，特别是当从一个平台迁移到另一个平台的用户将大部分数据存储在本地而非文件服务器时。你可以分批将数据从一个平台移动到另一个平台，这将非常耗时。有一群 Linux 软件厂商开发了工具使这一过程变得更容易且不耗时。

**备份：** 同时探索数据迁移和备份是因为这两项任务的性质相似：从 PC 以外的位置或介质复制并恢复数据。在此时考虑备份的原因是，你希望在停止使用某台 PC 之前尽可能保留用户特定的数据和设置。
