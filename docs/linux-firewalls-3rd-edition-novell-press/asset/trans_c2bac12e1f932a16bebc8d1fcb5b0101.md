
# 附录 B：防火墙示例和支持脚本

- 第 4 章独立系统的 iptables 防火墙 427
- 第 5 章优化后的 iptables 防火墙 446
- 第 6 章用于阻塞防火墙的 iptables 防火墙 463

# 附录 C：VPN

- 虚拟专用网络概述 475
- VPN 协议 475
  - PPTP 476
  - IPsec 476
- Linux 与 VPN 产品 480
  - Openswan 480
  - FreeS/WAN 481
  - 虚拟专用网络守护进程 481
  - PPTP Linux 解决方案 481
  - 虚拟隧道 482
- VPN 配置 482
  - 漫游用户 482
  - 网络连接 483
  - VPN 与防火墙 483
- 总结 485

# 附录 D：术语表

- 索引 499

# 关于作者

**Steve Suehring** 是一位技术架构师，拥有多元化的技能。他广泛运用多种技术，从大型机 OS/390 到 Microsoft Windows，再到多个 Linux 发行版。他撰写了一本关于 MySQL 的书，并发表了众多杂志文章。在担任 *LinuxWorld Magazine* 编辑期间，他致力于推广 Linux 和开源软件，同时也关注计算机安全。他为 *LinuxWorld Magazine* 撰写了一篇封面故事，介绍了 WilliamsF1 车队如何使用 Linux 设计其一级方程式赛车。Suehring 还是思科认证网络专业人士（CCNP），据他称，他为一些开源项目贡献了“极少量的代码”，并且潜伏在许多邮件列表中，在力所能及的范围内提供帮助和解答问题。

**Robert Zigler** 是一位著名的防火墙架构师和顾问，曾为包括 Nokia 路由器和接入组在内的各类组织工作。他因担任前两大版本《Linux Firewalls》一书的作者而闻名，并运营着一个备受尊敬的防火墙资源网站，用于分享他的设计技能及对工具的评估。

# 献词

*致我的妻子，Rebecca*

# 致谢

首先感谢我的家人，在我几乎每天都要写作的时候给予我支持。我还要感谢我的经纪人、Studio B 的 Laura Lewin，感谢她辛勤的工作和不断的帮助。也要感谢 A.J. Prowant 负责本项目的技术编辑。

Chris 和 Nikie Tuescher 值得被提及，因为他们是极好的朋友，并且理解为什么我们最近没来明尼阿波利斯——写这些书需要时间！感谢 Aaron 和 Jodi Deering 招待我们，也感谢 Aaron 在打篮球时对我手下留情。感谢 Duff Damos 多年来持续的友谊。Pat Dunn，谢谢你总是改变密码然后又忘记它。感谢 meet 的耐心和不断的帮助。

以下是名单，没有特定顺序：尽管你们中有些人如何帮助的确切方式可能并不显而易见，但你们在某种程度上都为这本书做出了贡献（无论是好是坏）。Andy Hale（等你想开始修地板时通知我），Dan Noah, Jim & Amy Leu, Kent & Amy Laabs, Michael Mittelstadt, Denise Sandell, The Pilgers, AWRC, Jake Buchholz, Richard Dean Anderson, Aaron Schrunk, Beaz, RySch, HFB & The #JBS, The Guthries, The Heinis, Tim McKeown, Pearl & Moff, Roo Konkol, Erin Thomas, Paul, Darrick, Jeff Sanner, Edward Van Haken, Peter DeLuise, The DBAs and the Data Architect team, Sarah Hagerman, Jay & Deb Schrunk, Brian Page, Is Anyone Still Reading This, Mark Little, Nightmare Squad, Jim Oliva, John Eckendorff, 90fm, Scott & Karla Kluck, Amanda Tapping, The Steffens, Eliot Irons, Keith Imlach & the Data Security team, No, seriously, is anyone reading this, Sue Crawford, Eric Hartman, Commas are my best friend, Ron Mackay, The Chaasteens, Darin Davission, If you haven’t seen your name yet wait until my next book, Justin Hoerter, John Hein, Andy Berkman, The Internets, Mike Wrzinski, , That was an extra comma because I love them so much, Chris Judge, Tony Failardo, Steve Hannan (I just thanked a Project Manager), Greg Ruby, Ryan Anderson, Suzi Limberg, Kevin Blake, Dave Duhle, I get paid based on how many people I thank, Michael Shanks, Tom Lindley, This Space For Rent, Kevin Bedell, James Turner, Dee-Ann LeBlanc, Neil Peart, Norm & Crew @ Music Quest。

这名单很长，我确定我漏掉了一些人，就像上次一样。随着截止日期临近，我需要将这份最终交付物发送给出版社。如果这里没有明确感谢到你，请知道我是感激你的……即使我在写这段时忘记了你。

# 我们想听听你的声音！

作为本书的读者，你是我们最重要的评论家和批评者。我们珍视你的意见，希望知道我们做对了什么，什么可以做得更好，你希望我们涵盖哪些主题，以及你愿意传达给我们的其他任何智慧之言。

你可以通过电子邮件或直接写信告诉我，你喜欢或不喜欢这本书的哪些内容——以及我们可以做些什么来使我们的书变得更好。

> *请注意，我无法帮助你解决与本书主题相关的技术问题，并且由于收到的邮件数量庞大，我可能无法回复每一封信。*

当你写信时，请务必备注本书的书名和作者，以及你的姓名和电子邮件地址或电话号码。我会仔细审阅你的评论，并与参与本书工作的作者和编辑分享。

电子邮件：feedback@novellpress.com

邮寄地址：
Mark Taber
Associate Publisher
Novell Press/Pearson Education
800 East 96th Street
Indianapolis, IN 46240 USA

# 读者服务

欲了解有关本书或 Novell Press 其他书籍的更多信息，请访问我们的网站 www.novellpress.com。*在搜索栏中输入 ISBN 或书名即可找到您正在查找的页面。*

# 前言

本书主要介绍如何在 Linux 操作系统中使用 Netfilter 和 iptables 创建软件防火墙。除了防火墙的基础知识外，本书还在网络化计算环境的背景下探讨了防火墙。为此，入侵检测和系统安全等主题也在涵盖之列。

计算机安全是一个广阔的领域。已经有很多卷书就此撰写，未来还将继续有卷书问世。计算机安全的核心在于使用三项原则保护数据资产：机密性、完整性和可用性。机密性意味着数据只能被授权访问的人访问，其他人无法访问。完整性确保数据是可信的且未被篡改。可用性意味着在需要时可以访问数据。这三项原则指导着计算机安全的讨论，并构成了本书的框架。

除了机密性、完整性和可用性这三项原则外，我还信奉一种深入且基于风险评估的计算机安全方法。这意味着在保护数据方面，我不认为任何单一选项是终点，而是认为防火墙或杀毒软件等每一项都扮演着保护数据的角色。然而，每种安全措施都涉及成本。因此，必须对每个额外的安全措施或安全层进行评估，以确保该层的成本不超过免受该风险保护所带来的收益。

考虑这个例子：我使用两个防火墙，一个阻塞防火墙和一个网关防火墙（参见第 6 章“数据报转发”），用于我的家庭网络。我认为双防火墙方法的收益超过了运营和维护这些防火墙的成本。其他人使用单个防火墙甚至不使用防火墙。他们认为数据或系统不可用或遭受攻击的风险，比运行双防火墙甚至对某些人来说比运行单个防火墙的成本更低。这种成本/收益评估还有更多例子

