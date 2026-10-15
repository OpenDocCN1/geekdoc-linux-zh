

## 侧边栏可能是金矿

仅仅因为它在侧边栏中并不意味着你在这里找不到新东西。请务必注意这些元素，它们会带来与正文讨论内容相关的旁支内容。你将阅读到关于其他技术、基于 Linux 的硬件，以及使你的系统更稳健高效的特殊流程。

为提高可读性而使用的其他格式技术包括在计算机命令语法中使用斜体表示占位符。计算机术语或概念在正文中首次出现时也会使用斜体。

最后，你应该知道，《Ubuntu Unleashed》中的所有文本、示例代码和屏幕截图都是使用 Ubuntu 和开源工具开发的。

继续阅读，开始学习并使用最新版本的 Ubuntu。经验丰富的用户在计划或考虑升级时应关注本版中的新信息。存在许多来自不同厂商的 Linux 发行版，但其中许多源自 Debian 发行版，或与其非常相似。

## PART I
## 安装和配置

### IN THIS PART

- CHAPTER 1 Introducing Ubuntu 13
- CHAPTER 2 Preparing to Install Ubuntu 25
- CHAPTER 3 Installing Ubuntu 47
- CHAPTER 4 Post-Installation Configuration 61
- CHAPTER 5 First Steps with Ubuntu 87
- CHAPTER 6 The X Window System 127
- CHAPTER 7 Managing Software 145
- CHAPTER 8 On the Internet: Surfing the Web, Writing Email, and Reading the News 157
- CHAPTER 9 Productivity Applications 179
- CHAPTER 10 Multimedia Applications 201
- CHAPTER 11 Graphics Manipulation 227
- CHAPTER 12 Printing with Ubuntu 241
- CHAPTER 13 Games 253

## CHAPTER 1
## Introducing Ubuntu

欢迎阅读《Ubuntu Unleashed》！Ubuntu 是当今世界上增长最快的 Linux 发行版，由 Ubuntu 基金会开发和维护，得到了百万富翁 Mark Shuttleworth 和 Canonical Software 的支持。Ubuntu 是一个非洲词汇，涵盖了许多不同的含义，但可以解释为“通过一人，我们是许多人”，反映了将 Ubuntu 这样的 Linux 发行版带入开发和发布的协作过程。

Ubuntu 极受欢迎，曾在 Distrowatch.com 上占据榜首数月，但它也是建立在最稳定和最安全的发行版之一 Debian 之上。被描述为 Ubuntu 所建立的基石，Debian 提供了 Ubuntu 发行版可以利用的许多关键优势。然而，正如你将在本书中发现的那样，Ubuntu 与 Debian 也大不相同。

Ubuntu 是一个免费的发行版，主要由活跃且乐于助人的社区支持，该社区活跃于论坛和邮件列表中。然而，一些商业合作伙伴可以为 Ubuntu 提供商业支持，甚至一些 OEM 厂商在电脑上预装 Ubuntu。尽管 Ubuntu 是 Linux 发行版世界中的相对新来者，其第一个版本于 2004 年 10 月发布，但它在 Linux 社区中掀起了巨大波澜。Ubuntu 因其易用性和“开箱即用”的方式而备受赞誉，已在世界各地赢得了众多奖项。

最初仅单独发布，Ubuntu 现在拥有许多隶属于 Ubuntu 旗下的稳定伙伴。Ubuntu 本身默认随 GNOME 窗口管理器一起提供，但还有 Kubuntu，使用 KDE 窗口管理器，Xubuntu，使用 Xfce 窗口管理器，

### IN THIS CHAPTER

- What Is Ubuntu?
- Ubuntu for Business
- Ubuntu in Your Home
- 64-Bit Ubuntu
- Ubuntu on the PPC Platform
- Ubuntu on Multi-Core Machines
- Getting the Most from Ubuntu and Linux Documentation
- Ubuntu Developers and Documentation
- Reference

甚至还有 Edubuntu，这是一个专门为教育和学术机构设计的 Ubuntu 版本。它们都共享一个共同的代码库，每个版本都附带一张安装光盘，使其易于重新分发 Ubuntu 副本。事实上，如果你想要额外的副本，Ubuntu 实际上会免费寄送光盘。目前，你只能收到 Ubuntu 发行版，但你可以申请 x86 或 PPC 版本，每个包装都包含一张安装光盘和一张 Live CD。正在努力通过相同的光盘分发计划提供 Kubuntu 发行版。

### About Debian

如前所述，Ubuntu 建立在 Debian Linux 之上并借鉴了许多功能。Debian 本身是 Linux 发行版中最古老的之一，其开发可追溯到 1993 年。Ian Murdock 建立了 Debian 宣言，呼吁对 Linux 发行版进行开放和协作式开发，并使用自己的名字和他当时女友、现任妻子 Debra 的名字来命名。

Debian 发行版通常被认为是最稳定和最安全的发行版之一。它也是完全非商业化的，有严格的指导方针以确保只有真正的自由软件（在言论意义上）才能通过 Debian 获取。

拥有如此坚实的基础，其他发行版以 Debian 为基础也就不足为奇了；截至撰写本文时，约有 52 个发行版可以追溯到 Debian 的血统。流行的发行版如 Linspire、Xandros，以及非常有用的 Knoppix Live CD 都以 Debian 为核心。

Linux 成功的理由有很多。也许最重要的一点是它满足了真正的需要。人们不仅可以按原样部署软件，而且如果需要以特定方式工作，他们可以与源代码，即软件的构建基块一起工作，以操纵程序本身并改变其工作方式。这种开放性在软件世界中是闻所未闻的，但它是 Linux 的关键优势。Linux 在服务器机房的早期进展中运行了诸如 Web、电子邮件和文件服务器等应用程序。随着各种发行版以及应用程序和窗口管理器的持续开发，Linux 在桌面上变得越来越常见。

UNIX 在 20 世纪 70 年代问世时也非常流行。然而，限制性的许可和后来被称为 UNIX 战争的东西扼杀了重大的开发和标准化，导致微软通过后门进入并以远逊于 Windows NT 的产品进入。如今，微软正面临真正的挑战，以阻止 Linux 主导服务器市场。

归根结底就是这样：你手中的软件如果商业开发的话估计价值 19 亿美元。Linux 中存在超过 5500 万行源代码，来自世界各地的数千名开源开发者的集体开发工作直接贡献于 Linux。

如今，看到公司转向 Linux 的报道已相当常见。事实上，更可能是政府机构寻求摆脱

