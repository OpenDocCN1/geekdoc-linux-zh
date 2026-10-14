
# Damn Small Linux 官方书：可在任何设备上运行的微型可适配 Linux（Negus Live Linux 系列）

美国企业和政府销售<br>
(800) 382-3419<br>
corpsales@pearsontechgroup.com

美国以外销售请联系：

国际销售<br>
international@pearsoned.com

## 本书已启用 Safari

您喜爱的科技图书封面上的 Safari® Enabled 图标意味着该书可通过 Safari Bookshelf 获取。购买本书后，您可免费获得 45 天的在线版访问权限。

Safari Bookshelf 是一个电子参考图书馆，让您轻松搜索数千本技术书籍、查找代码示例、下载章节，并在您需要时随时随地访问技术信息。

获取 45 天 Safari Enabled 访问权限：

- 前往 http://www.prenhallprofessional.com/safarienabled
- 完成简短的注册表格
- 输入优惠券代码 MZM-WP3L-2RXB-HYLV-GTM1

如果您在 Safari Bookshelf 注册或访问在线版时遇到困难，请发送电子邮件至 customer-service@safaribooksonline.com。

访问我们的网站：www.prenhallprofessional.com

**John Andrews’ dedication:**

我谨将本书中由我撰写的部分献给 Jennifer、Marja、Kelsey 和 Maddie，她们在我撰写章节时，忍受了忙碌的丈夫和爸爸。

**Robert Shingledecker’s dedication:**

谨以此纪念我的父母，Winston 和 Stella。

**Christopher Negus’ dedication:**

一如既往，我将对本书的贡献献给我妻子 Sheree。

## 致谢

我想感谢 Prentice Hall 所有优秀的朋友们给我这个机会。特别感谢 Chris Negus 在写作过程中给予我的指导。站在 Richard Stallman、Linus Torvalds、Klaus Knopper 以及其他许多已经并继续为自由开源软件做出贡献的巨人的肩膀上，我深表感谢。因为没有他们，这个项目就不会存在。

感谢 John Andrews 创立并分享他的作品。非常感谢 DSL 用户社区。感谢你们提出的建议、提交的 bug 报告、与他人分享知识，以及构建了被称为 MyDSL 仓库的众多应用程序扩展。感谢社区成员 milkshaw、thehatsrule、cabbagar01 以及许多其他多年来持续帮助这个项目取得成功的人。

我还要感谢 Joe Rabinsy 阅读我的初稿并提出改进建议。

—Robert Shingledecker

我非常感激我的妻子 Jennifer Lew-Andrews，她就像一位无偿编辑，为我在这本书中写的所有内容付出了努力。Robert Shingledecker 主要负责将先进的功能整合到 DSL 中，使其如今如此受欢迎。

DSL 社区同样值得感谢。DSL 中的许多改革和改进都是我们知识渊博的用户在 DSL 论坛上发布反馈和技巧的直接成果。我要感谢 Melodie 和 Antonina，她们在幕后做了大量工作，在我们投入时间和金钱的同时，让 DSL 得以维持。最后，非常感谢 Chris Negus，他非常努力地促成了这本书的出版。

—John Andrews

特别感谢 Prentice Hall 的 Debra Williams Cauley 和 Mark Taub，他们相信一本关于小型免费操作系统的书能找到大量读者。感谢 Songlin Qiu、Jovana San Nicolas-Shirley 和 San Dee Phillips 在出版阶段的支持，以及 Kelli Brooks 细致的文字编辑。感谢 Joe Brockmeier 和 Bryan Helvey 深思熟虑的技术编辑。

最后，我想感谢 John Andrews 和 Robert Shingledecker 花时间分享他们对当今最优秀的紧凑型桌面操作系统的见解。

—Christopher Negus

## 关于作者

Robert Shingledecker 的 IT 职业生涯长达 35 年，始于为 Burroughs 公司小型机手工编写机器语言程序。后来，他喜欢使用汇编语言，然后是 COBOL。他对计算机始终充满热情，曾是 COMAL 的倡导者，也是 MINIX 和 Coherent OS 的早期黑客。

在 Linux 项目方面，Robert 领导了加利福尼亚州 Garden Grove 市首次大规模 Linux 部署，并于 1994 年在 DG/UX 系统上部署了 Samba。他还设计了一个大规模可扩展的 Linux/AOLserver/Sybase 电子商务系统。随后，Robert 成为几家基于 Linux 的互联网公司的首席技术官。

在构建基于 Linux 的免安装 live CD-ROM 设备（包括防火墙、VPN、Web、电子邮件和数据库设备）的过程中，他对 Damn Small Linux 产生了兴趣。不久，Robert 加入了 John Andrews，共同领导 Damn Small Linux 的开发。

如今 Robert 已退休，他把时间花在编写代码和开发 Damn Small Linux 上。他也喜欢旅行。

John Andrews 是 Damn Small Linux (DSL) 的创建者。1996 年，作为一家串珠和珠宝店的老板，John 学习了 HTML 和 Perl 来开发自己的网站。这最终扩展到在 Linux 服务器上为他人运营网站。他对 Linux 的兴趣促使他全职改用 Linux 桌面。

快速高效应用程序的吸引力促使 John 开发了 Damn Small Linux。在尝试了几个主要用于诊断和系统恢复的迷你发行版之后，John 想要构建一个本质上拥有什么的低于 50MB 的发行版
他需要完成一天的工作；结果是 Damn Small Linux 发行版。John 的专长包括 Perl、shell 脚本、Lua、awk、SQL、php，以及一些 C 编程语言。

**Christopher Negus** 几乎十年以来一直是世界上领先的 Linux 书籍作者之一。他的 *Red Hat Linux Bible* 系列在全球销量超过四分之一百万册。Chris 还为 Wiley Publishing 撰写或合著了书籍 *Linux Bible*（2005 年至 2007 年版）、*Linux Toys*、*Linux Toys II* 和 *Linux Troubleshooting Bible*。对于 Prentice Hall，Chris 是 *Negus Live Linux Series* 的编辑，并撰写了该系列的旗舰书籍 *Live Linux CDs*。

在成为全职作者之前，Chris Negus 在 1980 年代和 1990 年代在 AT&T Bell Labs、UNIX System Labs 和 Novell 的 UNIX 操作系统开发团队工作。特别是，Chris 在 UNIX 系统管理和网络领域工作。

当不从事计算机书籍工作时，Chris 喜欢与家人共度时光：Sheree、Seth 和 Caleb。Chris 还喜欢踢足球、唱歌剧（当没人能听到他时），以及用旧电脑制作东西。

## 引言

Damn Small Linux（DSL）始于 John Andrews 的一个练习，即将一个完整的桌面计算机系统压缩到 50MB 的映像中。在几年之内，DSL 发展成为世界上最受欢迎的 Linux 系统之一（据一些说法排名前十），而没有超出 50MB 的目标。

在一个桌面系统充斥着花哨的视觉效果和许多很少使用的功能的世界里，你可能会想知道这个小小的操作系统为何如此受欢迎？可能是因为人们不想因为最新的 Windows 系统无法运行而丢弃一台可用的电脑。也可能是因为人们厌倦了等待常见的计算机操作完成，而后台却不知发生了什么。或者也许只是对简洁和优雅的热爱。

DSL 致力于包含现代桌面计算机系统所需的所有基本功能——然后使这些功能具有功能性、快速和高效。因此，DSL 可以在比大多数当今桌面系统要求更小、更旧或更弱的硬件上良好运行。

DSL 开发的一些精彩分支是，你可以用 DSL 做以下事情：

- **随身携带。** 它可以放在一张实时 CD、USB 闪存驱动器（也称为笔式驱动器或拇指驱动器）、Zip 驱动器，或一张可随身携带的启动式名片 CD 上。
- **随处运行。** 你只需要一台标准 PC（具有最小的处理器、少量 RAM，且无需磁盘空间）即可重新启动。或者，你可以运行一个特别为从 Windows 桌面运行而设置的 DSL 版本。如果你愿意，甚至可以对 DSL 进行传统的硬盘安装。
- **添加软件。** 如果你只需要再安装几个应用程序，只需几次点击即可下载、安装并保存你需要的应用程序。
