# The Book of Postfix ： 现代邮件传输




# 本书推荐语

> "虽然许多技术书籍不过是产品文档的翻版，但 Koetter 和 Hildebrandt 对 Postfix 的基础原理提供了精辟的见解。在为读者打下坚实的理解基础之后，他们进一步探讨了许多 Postfix 的高级特性。读完此书，我不禁感叹，如果其他邮件软件也能有这样一本书，相关技术将会被更好地理解和认识。"

——TOM THOMAS，《网络安全入门》（思科出版社）作者

> "随着 Postfix 的广泛普及和新功能的不断添加，管理员越来越需要一本全面的参考指南来部署和维护其 Postfix 系统。Patrick Koetter 和 Ralf Hildebrandt 自 Postfix 诞生之初就一直致力于这项事业，他们是该领域的专家，他们的书正好满足了这一关键需求。"

——LUTZ JÄNICKE，Postfix TLS 补丁的创建者和维护者

> "Ralf 和 Patrick 的书最令我印象深刻的是，它将困难、复杂的概念变得简单易懂。作者显然对主题了如指掌，并以易于理解的方式呈现出来。内容全面，毫无遗漏。"

——TOBIAS OETIKER，RRDTOOL（轮询数据库工具）和 MRTG（多路由器流量图形器）的发明者

> "本书包含大量实用示例和清晰的讲解，就像有一位 Postfix 专家在你身边指导一样。"

——DAVID SCHWEIKERT，POSTGREY（Postfix 灰名单策略服务器）作者

> "我向所有使用 Postfix 的人推荐本书，尤其是那些计划集成 AMaViS 病毒扫描的用户。"

——RAINER LINK，OPENANTIVIRUS.ORG 创始人

> "无论你是家庭用户还是当今最大规模邮件系统的管理员，只要你想使用和理解 Postfix，这本书都是不可或缺的参考资料。"

——DR. LIVIU DAIA，罗马尼亚科学院数学研究所高级研究员

献给那些热爱优秀软件的人

# 关于作者

Ralf Hildebrandt 和 Patrick Koetter 是 Postfix 社区中活跃且知名的人物。Hildebrandt 担任 T-Systems 的技术经理，T-Systems 是一家德国信息与通信技术（ICT）解决方案公司。Koetter 是一名信息架构师，经营自己的公司，为欧洲和非洲的客户提供企业通信咨询和开发服务。两人均在行业会议和黑客大会上就 Postfix 发表演讲，并定期为多个开源邮件列表贡献力量。

# 致谢

有很多人需要为本书表示感谢，因此我们将分别列出各自的致谢名单。

## Ralf Hildebrandt

在撰写本书的过程中，我注意到自己对 Postfix "底层"运作机制的了解是多么有限。我知道它的行为方式，但并不完全清楚背后的原因，至少在每一个组件和边界情况上并非如此。有些方面我知之甚少，有些方面我发现自己的认知（或缺乏认知）是错误的。我不得不阅读文档并在乐于助人的 postfix-users 邮件列表上大量提问，以获取详细信息。本书无法替代运行 Postfix 超过五年的经验，但它将引领你更接近掌握它。

坦率地说，当我在94年开始使用 Unix 时，互联网比现在安全得多。那时根本没有垃圾邮件！我认识 Postfix 是因为 Sendmail 不断崩溃。在短暂使用了一段 qmail 之后，我找到了 Postfix 并一直使用至今，从未回头。

当 Bill 找到我，问我是否想写一本关于 Postfix 的书时，我起初有些犹豫。我需要一位合著者，因为需要完成的工作量对一个人来说实在太大了。当时，Patrick 正在邮件列表上抱怨 SASL，并发誓如果有一天他搞定了 SASL，就要写一份 SASL-HOWTO。他确实搞定了，我读了那份 HOWTO，觉得很好，便邀请他合作。

事实证明，工作量对两个人来说也太多了，于是 Brian Ward 加入了我们担任技术编辑，在我们缺乏经验的领域提供了宝贵的帮助。

没有 Wietse Venema、Vi(cl)ktor Duchovni、Lutz Jänicke、Andreas Winkelmann 和 Peter Bieringer 的帮助，本书永远无法达到现在的水准，因此他们每人将获得一本免费赠书。虽然他们并不一定需要，但这确实是一份很棒的礼物。特别感谢我的妻子 Constanze，她忍受了我频繁的"但我现在还得写一章"的借口，才使这本书得以完成，而不是沦为"跳票"之作。对了，阅读 Patrick 的评价时，请记住我只是有点疯狂。

## Patrick Koetter

互联网要为我们提供所有期望的服务，还需要很长的时间。就像任何其他新媒体一样，服务提供者的首要冲动是推动增长，尤其是内容和服务的数量。服务质量和功能通常不得不退居其次——至少在服务开始盈利之前。与此同时，它暴露在那些喜欢滥用和破坏而非推广和扩展的人面前。

电子邮件就遭遇了这种情况，而这正是 Postfix 的用武之地，它真正提供了一个全新维度的质量。

当我着手搭建自己的 SMTP 服务器时，我发现 Sendmail 似乎需要某种文凭才能搞懂，尤其是那些宏。于是我开始寻找其他软件。长话短说：我爱上了 Postfix。

Postfix 让我看到了一种可能——复杂的软件可以用简单、清晰、结构化的语法来配置。如果你了解 SMTP，你就已经掌握了 Postfix 配置的大部分重要细节。当 Ralf 邀请我合著此书时，我其实并不真正了解 SMTP。这本书要求我学习的东西比预期的要多，也让我纠正了很多误解。

我非常自豪这本书让我有机会将我目前所掌握的关于计算机和电子邮件的知识传递给大家。希望本书能助你踏上创造性使用 Postfix 的征程。知识是创造力最好的土壤。

如果没有 Wietse Venema、Vi(c)ktor Duchovni、Liviu Daia、Lutz Jänicke、Florian Kirstein、Walter Steinsdorfer、Roland Rollinger、Tom Thomas、Alexey Melnikov、Andreas Winkelmann、Eric "cybertime hostmaster" 以及 Postfix 邮件列表用户的知识、好奇心和支持，这本书不可能问世；正是他们的问题和反馈，在我们以为已经面面俱到时，指出了我们的不足。

最重要的是，我要感谢 Ralf，他对 Postfix 的了解无人能及，更令人钦佩的是他驾驭计算机的潇洒自如——在这方面他如鱼得水。正是 Ralf 选择了我作为他的伙伴，共同踏上这段名为《Postfix 权威指南》的冒险之旅。我感激这个疯狂的家伙，在我们合著这本书的过程中，他已成为我亲密的朋友。

这本书对我来说是一个巨大的挑战，对我的妻子 Birgit 也是如此；她对我的信任支撑我完成了这本书的无数行文字。能够被委以做自己心之所向之事，是一种莫大的荣幸。当你终于付诸行动时，身边有 Birgit 这样的人，实乃天赐。




# 关于本书

![](img/852c79f689feb77c5fde686b993808b1_25_0.png)

> 用文字来描述魔法，就像用螺丝刀来切烤牛肉。
> —汤姆·罗宾斯

本书是学习Postfix的分步指南。你从初学者起步，当读到结尾时，希望你已成为专家。各个章节分为三种类型：教程、理论和Postfix实践。教程是入门读物，帮助你在尝试用Postfix实现解决方案之前理解主题。理论性章节告诉你Postfix如何处理该主题。实践章节则向你展示如何从理论过渡到一个可工作的安装。

我们将本书分为四个部分，分离了学习运行Postfix的主要步骤：

### 基础

本书第一部分向你展示Postfix的基础知识。你将学习如何为单个域名和拨号服务器配置Postfix。你还将从整体上看到Postfix的内部结构，并了解它提供了哪些工具。

### 内容控制

Postfix允许你显著控制你系统上的消息流。第二部分首先向你展示SMTP通信的工作原理，并解释电子邮件的格式。然后，你将看到Postfix如何控制消息处理的各个方面。

## 高级配置

Postfix经常与其他第三方应用程序交互，例如SQL服务器、Cyrus SASL、OpenSSL和OpenLDAP。第三部分的章节向你展示如何做到这一点。

## 性能调优

可配置的软件总有调优的空间。第四部分帮助你找到安装中的瓶颈，并提供提示，帮助你提高邮件系统的整体性能。

## 额外资源

除了*Postfix权威指南*和Postfix附带的文档外，还有另外两个资源可以在寻找信息或帮助时参考。

### Postfix文档、指南和常见问题解答

Postfix网站（http://www.postfix.org/docs.html）有一个页面，涵盖了由Postfix社区编写的Postfix文档、指南和常见问题解答。

### 邮件列表

Wietse Venema运行着几个服务于Postfix社区的邮件列表。你可以在Postfix邮件列表页面（http://www.postfix.org/lists.html）找到有关如何订阅以下列表的信息：

- **postfix-announce@postfix.org**：用于发布Postfix版本和更新公告的列表。
- **postfix-users@postfix.org**：关于Postfix邮件系统使用经验的通用讨论。帖子不受审核，仅限成员。
- **postfix-users-digest@postfix.org**：每日通过postfix-users邮件列表发送的文章摘要。
- **postfix-devel@postfix.org**：供对Postfix开发感兴趣的人使用的低流量列表。

Postfix社区在postfix-users@postfix.org列表上讨论概念、问题、错误、补丁和许多其他主题。当你遇到问题或想了解与Postfix相关的任何其他事情时，很可能通过浏览邮件列表存档找到答案。一些组织或个人托管postfix-users@postfix.org存档，可以通过Web浏览器访问。全面的存档列表可以在Postfix邮件列表页面（http://www.postfix.org/lists.html）找到。

## 本书中使用的约定

等宽字体用于

- 文件名和路径名
- 邮件列表名称和互联网地址，如域名、URL和电子邮件地址
- 守护进程、命令、参数名称和值、环境变量和命令行选项

*等宽斜体*用于

- 应替换为系统相应值的参数和占位符
- 示例命令行和代码示例中的注释

**等宽粗体**用于需要在shell窗口中输入的命令行和选项。

***等宽粗斜体***用于突出显示讨论中引用的特定行。

> **注意**：*$*字符代表命令行中的常规提示符；*#*字符是超级用户的shell提示符。

## 本书中使用的域名和名称

因为本书是关于邮件服务的，我们经常会谈到消息传递和传输，并且需要在示例中包含域名、发件人和收件人的名称。我们通常使用以下名称。

### 本地域名

在整本书中，我们将声称域名为example.com。邮件服务器大概会接受（或至少考虑）发往本地用户anyuser@example.com和anyuser@mail.example.com的消息。在按照示例构建自己的Postfix服务器时，你需要将example.com替换为你自己域名的名称。

> **注意**：当然，我们并不真正拥有example.com、example.org和example.net这些域名。互联网号码分配机构（IANA）已将它们保留用于文档。

### 我们的服务提供商

在整本书中，我们将使用example-isp.com域名作为我们ISP的域名。

### 脚本

你可以在http://www.postfix-book.com找到支持脚本和其他有用信息，如勘误表。

### 意见反馈

如果你发现错误或想发送其他反馈，请将你的意见发送至comments@postfix-book.com。

# 1. Postfix简介

![](img/852c79f689feb77c5fde686b993808b1_29_0.png)

Postfix是一种消息传输代理（MTA），它使用SMTP将消息从邮件用户代理（MUA，或邮件客户端）传输到远程邮件服务器。MTA也接受来自远程邮件服务器的消息，将其转发给其他MTA或投递到本地邮箱。在传输或投递消息后，Postfix的任务就结束了。其他服务器负责将消息送达最终用户。例如，MTA（如POP3或IMAP服务器）将消息交给像Mutt、Outlook或Apple Mail这样的MUA，用户可以在那里阅读它。

乍一看，MTA的工作似乎相当简单，但事实并非如此。消息传输代理是特殊的，因为它必须跨越网络边界通信——它们将内容传输到其他网络，并接受针对其自己网络的内容。常识告诉我们，任何运行网络的人都必须采取预防措施来保护他们的服务器和数据免受攻击，并且人们普遍认为，你需要做的就是安装一个防火墙来控制本地和远程网络之间的双向连接。这是一个误解：防火墙不是应用程序；它是一个概念。

常见防火墙实现中最受欢迎的部分是监控和限制连接的应用程序。不幸的是，防火墙通常无法评估两个主机之间交换的内容；它们控制用于数据通信的主机、端口和传输层协议，但它们不会根据通信内容进行限制。分析内容是一项困难得多的工作，必须由能够决定如何处理内容并确定其是否有害的专业应用程序来完成。MTA为电子邮件执行此任务。此外，现代MTA必须快速、可靠且安全，因为它们在地球上最大的网络上传输最受欢迎的数据：电子邮件。

有许多MTA可供选择，但它们大多在某些方面存在不足。例如，一个具有出色的安全模型，但其开发者基础不再是一个小型核心团队，这会导致失败并为安全问题敞开大门。第二个MTA之所以广泛使用，是因为它是一个流行的群件包的一部分，但开发团队似乎在群件功能上花费了太多时间，而忘记了跟上互联网标准和来自垃圾邮件及恶意攻击者的新挑战。最后，有一个MTA可以轻松应对标准，并且在同时服务许多用户方面没有问题，但它的安全记录非常糟糕，你需要一位专家在修复之间采取必要的反制措施才能安全运行。

运行Postfix不需要成为专家；它试图开箱即用，尽可能安全地运行。Postfix的安全性根植于其默认配置设置。如果应用程序的基本配置足够安全和完整，你无需更改任何内容，那么运行一个安全的MTA就很容易。更好的是，如果你需要更改某些内容，Postfix对于参数和选项具有如此清晰、结构化的语法，成功更改默认行为相当容易。此外，Postfix应用程序设计是模块化的，每个模块都以完成工作所需的最低权限级别运行。Postfix在设计时就考虑了安全性，其级别高于代码本身。

Postfix表现出色，因为它专注于邮件传输的核心任务；它不会用系统上其他应用程序已经提供的功能来重新发明轮子。Postfix为你提供了在相关任务超出消息传输范围时插入外部应用程序的方法。此外，Postfix利用Unix的全部功能来完成其工作。这种与操作系统的紧密集成不仅使得访问外部应用程序更容易，而且提高了性能。

审视现代邮件传输和处理的任务，可以看出Postfix是邮件传输套件的核心。在图1-1中，你可以看到Postfix被专门的应用程序和工具所包围，以帮助控制内容、连接和转发。



## 第一部分

### 基础

本书第一部分涵盖 Postfix 的基础知识，从操作系统先决条件开始，讲解如何为单个域设置邮件服务器。这些章节将帮助你熟悉 Postfix 配置文件语法以及 Postfix 的一些组件程序和实用工具。

以下是本部分四章内容的概述：

**准备主机和环境**
在安装 Postfix 之前，你应始终验证你的服务器主机能否处理 SMTP 服务器。第 2 章将向你展示如何配置操作系统，以便充分利用 Postfix。

**单域邮件服务器**
任何新的 Postfix 安装的第一步是创建一个能够接收单个域邮件的配置。在第 3 章中，你将看到如何验证系统是否正常工作，以及如何为更复杂的设置奠定基础。

**单域拨号邮件服务器**
你无需对单域设置进行重大修改即可获得一个可工作的拨号配置。第 4 章将向你展示这些虽小但重要的更改。

**Postfix 解剖**
Wietse Venema 说“Postfix 实际上是一个路由器”，一个路由消息而非 IP 数据包的路由器。在第 5 章中，你将从宏观上了解 Postfix 内部组件如何交互。

# 2 准备主机和环境

> 起初一无所有。上帝说：“要有光！”然后仍然一无所有，但你能看见它了。— Ignacio Schwartz

你可能非常兴奋，因为你刚拿到这本书，迫不及待地想开始使用 Postfix。然而，在你开始之前，有一件事你需要知道。

Postfix 由非常精通 Unix 的 Wietse Venema 构建，其设计并未包含 Unix 默认提供的功能。因此，Postfix 要求你的系统正确设置，并且其性能只能达到底层系统的水平。

不要因为本章看似基础就跳过它。花时间浏览以下章节，以确保你的系统一切就绪。Postfix 将以快速、可靠和安全的服务回报你的努力。

以下是 Postfix 的系统检查清单：

- ☐ 正确设置主机名
- ☐ 验证主机的连接性
- ☐ 保持可靠的系统时间
- ☐ 确保 syslog 服务可以记录 Postfix 诊断信息
- ☐ 为客户端配置名称解析
- ☐ 为邮件服务器配置域名服务（DNS）记录

## 主机名

邮件服务器必须拥有完全限定域名（FQDN；参见 RFC 821，ftp://ftp.rfc-editor.org/in-notes/rfc821.txt），例如 mail.example.com，才能与其他系统可靠地互操作。除非你手动配置其他名称，否则 Postfix 在向远程邮件客户端和服务器发出问候时会自动使用你分配给服务器的主机名。

完全限定域名也很重要，因为 Postfix 不仅从客户端接收邮件——当处于客户端模式时，Postfix 还会将消息传输到其他邮件服务器。许多邮件服务器会检查客户端公布的主机名，如果客户端未提供完全限定域名，则拒绝接收消息，有些服务器甚至会检查 FQDN 是否在 DNS 中解析。

你的操作系统在启动时设置系统主机名。要查看系统是否已有 FQDN，请登录并输入 hostname：

```
$ hostname -f
mail.example.com
```

如果此命令未返回完全限定域名，请查明系统如何设置主机名并进行修正。然而，如果你的系统已经有 FQDN 主机名，但希望 Postfix 使用不同的名称，请保持系统设置不变。你将通过 myhostname 参数来覆盖默认值。

> **注意** *hostname 的 -f 选项在 Solaris、使用 GNU hostname 命令时以及其他某些环境中不起作用。如果你的 hostname 命令如上所述不工作，请尝试省略 -f 选项。如果仍然不行，请查阅你的手册。*

## 连接性

验证你的机器能否到达其网络，以及网络上的主机能否与之通信。第一部分应该很容易——如果你的机器能上线并访问网页，它就在连接网络。传入连接更复杂一些。要测试它们，你需要一个客户端通常会连接的网络中的客户端。如果 Postfix 向整个互联网提供服务，你应该从一个完全独立于你的服务器的主机验证连接性。

### TCP 端口 25

确保没有任何东西阻止服务器的 TCP 端口 25。如果你有防火墙，请确保防火墙策略允许端口 25 上的传入和传出连接。请记住，一些互联网服务提供商（ISP）在其路由器上阻止到整个互联网的端口 25 的传出连接，除非你要求它们解除限制。一些 ISP 可能拒绝解除限制，而是希望你通过他们的邮件服务器进行中继，使用诸如 SMTP 身份验证之类的系统，该内容在第 16 章中描述。

TCP 端口 25 必须保持开放，因为 Postfix 和其他邮件服务器在此端口上监听连接。它是 SMTP 的官方 IANA 端口分配（完整列表请参见 http://www.iana.org/assignments/port-numbers）。IANA 是互联网协议中分配号码的中央注册机构，例如端口、协议、企业号、选项、代码和类型。

### 系统时间和时间戳

在调整功能和排除问题时，正确的系统时间很重要。当你需要超越系统边界与其他邮政管理员一起解决邮件问题时，正确的时间戳可能正是将你邮件服务器上的操作与你不控制的服务器上的操作联系起来所需要的。

Postfix 在邮件头中仔细记录其操作。例如，看看这个头部：

```
Received: from mail.example.net (mail.example.net [192.0.34.166])
	by mail.example.com (Postfix) with ESMTP id 6ED90E1C65
	for <recipient@example.com>; Sat,  7 Feb 2004 10:40:55 +0100 (CET)
Reply-To: sender@example.net
From: Sender <sender@example.net>
To: Recipient <recipient@example.com>
Subject: Keep correct system time
Date: Sat, 7 Feb 2004 10:42:01 +0100
```

Postfix 还会在邮件日志中做与日期相关的记录。以下是一些示例日志消息：

```
Feb 7 2004 10:40:55 mail postfix/pickup[32610]: 6ED90E1C65: uid=501 from=<sender>
Feb 7 2004 10:40:55 mail postfix/cleanup[398]: 6ED90E1C65: 
	message-id=<20040416020209.7D62343F30@mail.example.com>
```

因此，你应该确保获得尽可能准确的时间。不要信任系统内置的计时器；不仅 Unix 内核保持的时间会随时间漂移，而且主板制造商在电池供电时钟中使用的芯片也很廉价，也会偏离真实时间。你不能指望本地时间源与其他邮件服务器上的时间保持同步。

有两种获取精确时钟的方法。你可以使用 NTP（网络时间协议）通过网络获取时间，或使用 GPRS（全球）或 DCF-77（欧洲大部分地区）时间设备通过无线电获取时间。但是，如果你无法使用这些解决方案，可以尝试使用 clockspeed（http://cr.yp.to/clockspeed.html）作为最后手段。此应用程序使用硬件滴答计数器来补偿持续偏快或偏慢的系统时钟。给定来自可靠源的几次时间测量值，它会计算并补偿时钟偏差。

> **注意** 要使用 NTP 服务器，你必须在系统上运行 NTP 客户端（这样的客户端几乎每个操作系统都自带）。要使用 NTP，你必须允许防火墙端口 123 上的传入和传出用户数据报协议（UDP）数据包。如果你不知道如何配置 NTP 客户端，请访问 NTP 网站（http://www.ntp.org）获取更多信息。

### Syslog

查找诊断信息的最重要位置之一是邮件日志。Postfix 使用标准的 Unix 日志记录实用程序，称为 syslogd。你通常通过 /etc/syslog.conf 文件配置 syslogd。以下是一个示例配置：

```
# 记录除邮件外的所有 info 级别或更高级别的信息。
# 不要记录私有认证消息！
*.info;mail.none;authpriv.none;cron.none -/var/log/messages
# authpriv 文件有访问限制。
authpriv.* -/var/log/secure
# 在一个地方记录所有邮件消息。
mail.*    -/var/log/maillog
# 记录 cron 内容
cron.*    -/var/log/cron
# 每个人都获取紧急消息，并在另一台机器上记录它们。
*.emerg   *
# 将 err 级别或更高级别的邮件和新闻错误保存在特殊文件中。
uucp,news.crit  -/var/log/spooler
# 启动消息也保存到 boot.log
local7.*        /var/log/boot.log
```

首先，看第一个条目，它包含 mail.none 以将邮件消息排除在 /var/log/messages 之外。这很重要，因为你不想让邮件日志消息使你的通用系统消息变得杂乱。你可以看到邮件日志有自己的条目和文件（/var/log/maillog）。文件名前的连字符表示 syslogd 应异步将消息写入文件，而不是每次新日志消息到达时都强制写入磁盘。

不幸的是，syslogd 可能会出现几种问题。如果你似乎没有收到任何日志消息，你首先应该做的是确保 syslogd 确实在运行。以下示例展示了如何运行 ps 命令来查找守护进程。



# ps auxww | grep syslog
```
root     15540  0.0  0.0  1444   524 ?        S    May21 18:20 syslogd -m 0
root     22616  0.0  0.0  1444   452 pts/0    R    18:09   0:00 grep syslog
```

ℹ 此处输出的第一行表明 syslogd 自 5 月 21 日起就一直在运行。

此外，在指示 syslogd 写入日志文件之前，请确保这些日志文件存在且具有可写权限。某些 syslogd 的实现在文件不存在时不会自动创建文件，并且在日志文件出现问题时会静默失败。Solaris 的 syslogd 因此臭名昭著。

一个非常常见的错误是在 /etc/syslog.conf 文件中使用空格而非制表符来分隔日志类型和日志文件。你的 syslog.conf 应该这样编写：

```
mail.*<TAB>/var/log/maillog
```

另一个 syslogd.conf 的常见问题是将日志发送到另一台网络主机。请注意下面这样的条目：

```
mail.* @loghost
```

在这种情况下，syslogd 会将其所有日志发送到 loghost，因此你应该检查该主机上的日志，而不是邮件服务器上的日志。请确保你确实拥有这样一台主机。由于 syslogd.conf 文件中的错误条目，日志被发送到非预期的主机（或进入黑洞）的情况非常常见。

## 名称解析（DNS）

在 Postfix 等邮件服务器将邮件传输到远程目的地之前，它必须先定位该目的地。在互联网上，你需要通过域名服务（DNS）来查找远程资源。域名服务器返回主机名对应的 IP 地址，反之亦然，返回 IP 地址对应的主机名。

正常运行的 DNS 对 MTA 的性能至关重要。Postfix 越早解析出目标 IP 地址，就能越早开始与远程邮件服务器通信并传输邮件。

> **注意** *糟糕的主机名查询性能可能会成为大型邮件枢纽的主要瓶颈。如果你的服务器遇到问题，缓存域名服务器可以提供帮助。请为大型邮件系统设置缓存域名服务器。请注意，反垃圾邮件措施可能会使你的邮件服务器执行的 DNS 查询次数增加数倍。*

在尝试改进系统上的名称解析性能之前，请确保你的操作系统能够通过向域名服务器查询 postfix-book.com 的 MX 记录（参见本章后面的"MX 记录"部分）来正确解析远程主机名。尝试以下命令：

```
$ dig postfix-book.com MX
```

输出应如下所示：

```
;; <<>> DiG 9.2.2-P3 <<>> postfix-book.com MX
;; global options: printcmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 23929
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 2
;; QUESTION SECTION:
;postfix-book.com. IN MX

;; ANSWER SECTION:
postfix-book.com. 86400 IN MX 10 mail.postfix-book.com. ❶

;; AUTHORITY SECTION:
postfix-book.com. 86400 IN NS ns3.ray.net. ❷
postfix-book.com. 86400 IN NS ns.state-of-mind.de.

;; ADDITIONAL SECTION:
mail.postfix-book.com. 86400 IN A 212.14.92.89
ns.state-of-mind.de. 81566 IN A 212.14.92.88

;; Query time: 58 msec
;; SERVER: 212.18.0.5#53(212.18.0.5)
;; WHEN: Sat Apr 17 03:56:47 2004
;; MSG SIZE rcvd: 145
```

❶ 此行表示 mail.postfix-book.com 是接收 postfix-book.com 域内收件人邮件的邮件服务器。
❷ 这两行表示 ns3.ray.net 和 ns.state-of-mind.de 是 postfix-book.com 的权威域名服务器。

> **注意** *dig（Domain Information Groper，域名信息探查器）命令在某些过时的平台上不是标准命令。你可以从 ISC（http://www.isc.org）的 BIND 发行版中获取 dig。如果你无法安装 dig，你可能仍然可以使用 host 或 nslookup 来执行上述查询；后一条命令现已被弃用。*

如果查询成功，Postfix（理论上）可以正确解析主机名。如果请求不成功且无法解析任何主机名，你需要立即解决 DNS 问题。

名称解析的一个常见问题是当服务器尝试查询不可用的域名服务器时无法正常工作。检查你的 /etc/resolv.conf 文件。假设它看起来像这样：机器首先查询 localhost（127.0.0.1）上的域名服务器，失败后查询 134.169.9.107：

```
nameserver 127.0.0.1
nameserver 134.169.9.107
```

如果你正在运行缓存域名服务器，查询 localhost 是没问题的。但如果你没有运行缓存域名服务器，此请求将需要等待超时，耗时较长。如果你后来发现使用 dig 的域名服务器查询可以正常工作，但 Postfix 无法找到主机（例如，日志中出现"no route to host"），那么很可能是因为你以 chroot 方式运行 Postfix，因此它会查看不同的配置文件来确定名称解析的设置。例如，如果你的 chroot 监狱是 /var/spool/postfix，Postfix 将会查看 /var/spool/postfix/etc/resolv.conf。请通过运行 cp -p /etc/resolv.conf /var/spool/postfix/etc/resolv.conf 来确保文件一致，然后重启 Postfix。

### 邮件服务器的 DNS

你需要配置域名服务器，告知外界你的服务器是负责向你的域名投递邮件的服务器。请联系你的域名管理员（负责运行你域名的域名服务器的人）设置以下条目：

**A 记录**
你的邮件服务器必须拥有完全限定主机名，以便客户端能够找到你的服务器位置。A 记录将 FQDN 映射到 IP 地址。

**PTR 记录**
你的系统主机名应该可以被反向解析。通过 SMTP 通信获知你服务器主机名的邮件服务器应该能够验证你的服务器是否确实在与它们通信。

**MX 记录**
MX 记录让客户端知道你的服务器负责某个域名或特定主机的邮件投递。

#### A 记录

域名系统具有不同类型的记录来告知主机关于网络上的资源。其中最重要的是 A 记录，它将主机名映射到地址。向域名服务器发送主机名的客户端应获得该主机的 IP 地址作为响应。以下是一个示例会话，展示了 www.example.com 被映射到 192.0.34.166。

```
$ dig www.example.com A
; <<>> DiG 9.2.1 <<>> www.example.com
;; global options: printcmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 30122
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 0
;; QUESTION SECTION:
;www.example.com.               IN      A
```

```
;; ANSWER SECTION:
www.example.com.       172627  IN      A       192.0.34.166
;; AUTHORITY SECTION:
example.com.           21427   IN      NS      b.iana-servers.net.
example.com.           21427   IN      NS      a.iana-servers.net.
;; Query time: 1 msec
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Sat Apr 17 16:43:40 2004
;; MSG SIZE  rcvd: 97
```

#### PTR 记录

与 A 记录相对应的是 PTR 记录，它将地址映射到主机名。当客户端向域名服务器发送 IP 地址时，响应应为该地址对应的主机名，如下例所示：

```
$ dig -x 192.0.34.166
; <<>> DiG 9.2.1 <<>> -x 192.0.34.166
;; global options:  printcmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 37949
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 5, ADDITIONAL: 0
;; QUESTION SECTION:
;166.34.0.192.in-addr.arpa.    IN      PTR

;; ANSWER SECTION:
166.34.0.192.in-addr.arpa. 21374 IN    PTR     www.example.com.

;; AUTHORITY SECTION:
34.0.192.in-addr.arpa.     21374 IN    NS      ns.icann.org.
34.0.192.in-addr.arpa.     21374 IN    NS      svc00.apnic.net.
34.0.192.in-addr.arpa.     21374 IN    NS      a.iana-servers.net.
34.0.192.in-addr.arpa.     21374 IN    NS      b.iana-servers.org.
34.0.192.in-addr.arpa.     21374 IN    NS      c.iana-servers.net.

;; Query time: 1 msec
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Sat Apr 17 16:44:39 2004
;; MSG SIZE  rcvd: 201
```

**注意** 如今垃圾邮件泛滥互联网，使用 PTR 记录对 A 记录进行反向解析比以往任何时候都更加重要。许多邮件管理员配置其邮件服务器，仅在接受连接客户端的反向查询成功后才接收邮件。然而，仅仅因为其他邮件服务器基于反向查询来拒绝邮件，并不意味着你也应该这样做。这通常会导致问题，因为许多 ISP 不会将反向名称解析委派给其客户的域名服务器，也不会在其服务器上提供正确的信息。



## MX 记录

域名服务器不仅能解析资源记录；它还可以告知客户端有关域名中提供的服务。负责某个域名的邮件服务器就是其中一种服务。你可以配置一条 MX 记录，使其指向邮件服务器的 A 记录。

> **注意** *DNS 还有一种 CNAME 记录，即别名记录，它可以指向一条 A 记录。例如，你可以配置一条 CNAME 记录，将 www.example.com 指向 srv01.example.com。请求 www.example.com 的客户端将会收到 srv01.example.com 作为响应。*

*切勿让你的 MX 记录指向这些别名中的某一个。最常见的邮件传输协议（SMTP）要求电子邮件地址中的域名必须是 A 记录或 MX 记录。在前面的示例中，你无法将 MX 记录指向 www.example.com，但由于 srv01.example.com 有一条 A 记录，你可以将 MX 记录指向它。*

你可以指定多条 MX 记录，还可以对邮件服务器设置优先级，使客户端按照特定顺序尝试连接服务器。示例如下：

```
$ dig m-net.de MX
; <<>> DiG 9.2.1 <<>> m-net.de MX
;; global options: printcmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 3133
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 2, ADDITIONAL: 0
;; QUESTION SECTION:
;m-net.de.                     IN      MX

;; ANSWER SECTION:
m-net.de.              7200    IN      MX      50 mail-in.m-online.net. ①
m-net.de.              7200    IN      MX      100 mx01.m-online.net. ②
m-net.de.              7200    IN      MX      100 mx02.m-online.net.

;; AUTHORITY SECTION:
m-net.de.              7200    IN      NS      ns2.m-online.net.
m-net.de.              7200    IN      NS      ns1.m-online.net.

;; Query time: 27 msec
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Sat Apr 17 17:07:05 2004
;; MSG SIZE rcvd: 140
```

① mail-in.m-online.net 拥有最高的优先级，因为它的数值最低（50）。客户端将首先尝试将邮件投递到这台邮件服务器。
② mx01.m-online.net 和 mx02.m-online.net 的优先级并列第二（数值为 100）。如果最高优先级的邮件交换器不可用，客户端将尝试连接这两台中的任意一台。

### 单域名的邮件服务器

![img](img/852c79f689feb77c5fde686b993808b1_45_0.png)

为单个域名配置 Postfix 只需几分钟。无论你计划搭建何种配置，从以下单域名配置开始始终应该是你的第一个生产步骤；这将证明 Postfix 在最简单的设置下能够正常工作。

本章将向你介绍 Postfix 运行所需的最低配置参数，并展示如何在单域名设置中将较长的电子邮件地址映射为简短的用户名。

#### 最低配置

我们将配置 Postfix 使其接受某个单个域名的邮件，并且 Postfix 应将该域名内不同邮件地址的邮件投递到不同的邮箱。

Postfix 将仅处理这一个域名的邮件，我们将展示针对全新安装所需应用的最小配置更改集。最低配置的典型网络架构如图 3-1 所示。

![img](img/852c79f689feb77c5fde686b993808b1_46_0.png)

*图 3-1：单域名 Postfix 网络*

邮件服务器与互联网保持永久连接，并拥有一个静态 IP 地址。与该邮件服务器 IP 地址匹配的正向（A 记录）和反向 DNS 记录已配置完成。基础设置有基本要求。请确保你已按照第 2 章的说明正确配置了主机。

## 配置 Postfix

在本章中，我们将配置 Postfix 以接收单个域名的邮件。我们的主机名为 mail.example.com，域名为 example.com。我们将按照以下步骤操作：

- 1. 配置 Postfix 使其使用正确的主机名向邮件客户端打招呼。
- 2. 配置 Postfix 使其接受域名为 example.com 的邮件。
- 3. 配置 Postfix 使其在发送仅包含裸用户名的邮件时追加 example.com。
- 4. 配置 Postfix 使其将发送给 root 的邮件投递到另一个邮箱。
- 5. 配置 Postfix 使其将发送到电子邮件地址的邮件投递到相应的用户名。
- 6. 设置权限以使 Postfix 能够转发来自你的网络的邮件。

### 在 smtpd 横幅中设置主机名

当邮件客户端和服务器相遇时，它们会使用各自的 DNS 主机名互相打招呼。我们要做的第一件事是配置 Postfix 向邮件客户端自我介绍时使用的名称。如果你的主机名与你希望 Postfix 用于向邮件客户端打招呼的名称相同，那就太好了：无需做任何更改。另一方面，如果你的系统主机名设置为 www.example.com，并且你在同一台机器上运行 Postfix，而你希望它使用 mail.example.com 作为主机名向邮件客户端打招呼，这可以轻松实现。

> **注意** *当 Postfix 将消息传输到其他邮件服务器时，它充当邮件客户端。在向邮件服务器自我介绍时，它默认使用 myhostname 参数作为 HELO 名称。某些邮件服务器配置为：如果 HELO 名称与服务器的反向解析 FQDN 不匹配，则拒绝接收邮件。请确保你为 Postfix 设置的主机名与服务器 IP 的主机名匹配，或者设置 smtp_helo_name 使其与你 DNS 命名空间中的正式 FQDN 匹配。*

有两种方式可以实现不同的主机名：设置 myhostname 参数或设置 mydomain 参数。

#### 设置 myhostname

设置 myhostname 通过编辑 /etc/postfix/main.cf 完成。使用你喜欢的编辑器打开该文件，搜索 myhostname。然后将你预期的主机名作为 FQDN 主机名添加进去：

```
myhostname = mail.example.com
```

一旦设置好 myhostname，Postfix 就能自动推导出 mydomain。Postfix 只需去除第一个点及其之前的所有内容。由于我们将 myhostname 设置为 mail.example.com，Postfix 将推导出 mydomain 为 example.com——这正是我们需要的。

#### 设置 mydomain

你也可以不设置 myhostname，而只设置 mydomain。如果你的配置需要复制到多台机器上，这种方式会非常方便。

```
mydomain = example.com
```

一旦设置好 mydomain，Postfix 就能通过将该主机 `uname -n` 命令的输出与 mydomain 拼接来创建 myhostname。这意味着如果你的 main.cf 只显式设置了 mydomain，并且你将该文件复制到同一域名（本例中为 example.com）内的另一台主机，Postfix 会自行补全正确的主机名。

### 设置邮件被接受的域名

Postfix 将为主机的本地客户端充当转发中继，这意味着它会接受并非配置为最终目的地或转发目的地的域名的邮件。在单域名设置中，你只需设置 mydestination 参数即可。（关于将 Postfix 配置为转发多个域名邮件的步骤将在第 13 章和第 14 章讨论。）

> **注意** *当你设置 mydestination 时，可以硬编码目标值（例如 mydestination = mail.example.com），也可以使用已经通过 $parameter 记号在 Postfix 中设置的参数值。硬编码会使配置更改变得棘手，因为有许多参数需要编辑，而且考虑到拼写错误和其他潜在的人为错误，这种设置容易出错。我们不建议硬编码。*

本章的目标是让 Postfix 接收所有发往 example.com 的邮件。由于我们已经在 mydomain 中提供了该值，在 main.cf 中设置 mydestination 时只需引用它即可：

```
mydestination = $mydomain
```

如果你想更进一步，让 Postfix 也接受发往你在 myhostname 中设置的主机名的邮件，只需将该参数添加到 mydestination 中：

```
mydestination = $mydomain, $myhostname
```

如你所见，值以逗号分隔的列表形式添加，列表末尾不加逗号。如果要再进一步，你还可以通过将主机名与 $mydomain 组合来添加 www.example.com 和 ftp.example.com：

```
mydestination =
	$mydomain,
	$myhostname,
	www.$mydomain,
	ftp.$mydomain
```

本示例还介绍了另一种记法。如果需要向一个参数添加多个值，你可以将每个值放在单独的行上，但后续每一行必须以某些空白字符开头（否则 Postfix 将无法识别该值）。你可以在 shell 窗口中通过检查 `postconf mydestination` 的输出来验证这一点。

这种格式可用于 Postfix 中任何接受多个值的参数。

#### 设置附加到外发消息的域名

当本地服务（如 cron 或 at）或命令行邮件客户端发送邮件时，通常不会提供完整的发件人或收件人地址，而只提供裸用户名。虽然只要收件人是本地的就没问题，但当消息被发送到另一台主机时就会产生问题。追踪邮件来源主机需要花费相当长的时间，而且如果邮件收件人在目标主机上不存在，接收邮件服务器将无法将邮件退回。



Postfix 提供了一个参数，用于向以非完全限定形式指定的发件人或收件人追加值：myorigin。同样，我们可以复用已在 main.cf 中设置的参数：

```
myorigin = $mydomain
```

一旦启用了此设置，Postfix 就会向任何未完全限定的地址追加 mydomain 的值。例如，由 cron 作业产生并以 root 身份发送的邮件，其收件人将被设置为 root@$mydomain，在我们当前的配置中，这将变成 root@example.com。

如果你没有手动设置 myorigin，它将默认为 myhostname。当你运行多个主机，且希望所有 root 用户的邮件都投递到中央服务器上的一个特定账户时，这会非常方便。这样你总能知道邮件来自哪个主机名；例如，一个以 root 身份发送的 cron 作业，经过 Postfix 处理后，将以 root@$myhostname 的身份发出，在我们当前的配置中，这将是 root@mail.example.com。

### 将发送给 root 的邮件映射到另一个邮箱

Postfix 会将邮件直接投递给任何本地用户，包括 root。但 Postfix 在投递过程中不会授予 root 权限给外部程序。这意味着你无法使用本地投递代理（LDA），如 procmail 或 maildrop 来投递 root 的邮件，因为 Postfix 不会以 root 身份运行这些程序，而是以 default_privs（默认为 nobody 用户的权限）运行它们。这是一项安全预防措施，旨在通过不以 root 身份运行易受攻击的外部程序来保护超级用户账户。这并不意味着无法投递本应发给 root 的邮件。解决方案是在你的机器上创建一个具有普通、低权限的不同用户，并将本应投递给 root 的邮件转投递到这个账户。

在我们的示例中，我们使用 admin 作为启动主机管理工作的账户。¹ 为了使 Postfix 将发给 root 的邮件投递给 admin，只需打开默认安装中提供的 /etc/postfix/aliases 文件²，将 postfix 改为 admin，使其内容如下：

```
root:    admin
```

> 注意 如果你选择使用 admin 作为此用途，你还必须删除将 admin 邮件发送到 root 的别名文件条目。否则你将创建一个邮件循环。

¹ 最近，一种病毒/蠕虫利用发件人地址 admin@$mydomain 在互联网上传播自身。admin 这个名称可能不是一个好的用户账户选择。
² Postfix 附带的别名文件包含了各种 RFC 对邮件服务器要求的所有地址。别名文件本身会为你提供有关这些要求更多信息的查找提示。

一旦你编辑了 /etc/postfix/aliases³ 并添加了你偏好的用户名，你必须创建一个索引版本，通常是 /etc/postfix/aliases.db，以便加快 Postfix 的查找过程。这可以通过运行 postalias /etc/postfix/aliases 或不带参数运行 newaliases 来完成。为了熟悉 Postfix 附带的工具，请运行此命令：

```
# postalias hash:/etc/postfix/aliases
```

> **警告** 除非你已更新索引版本，否则 Postfix 不会使用 aliases 文件中的任何更改，因为它只从索引文件读取。

## 启动 Postfix 并测试向 root 投递邮件

现在是运行第一个测试的时候了。在前面的部分中，我们添加或更改了一些设置，如果我们继续操作而不验证到目前为止一切正常，那么一旦需要追踪错误，我们很可能会遇到麻烦。

### 启动 Postfix

在开始发送邮件之前，我们必须启动 Postfix。你只需输入 **postfix start**，Postfix 将回复以下消息：

```
# postfix start
postfix/postfix-script: starting the Postfix mail system
```

如果你收到以下消息，则说明 Postfix 已经启动并正在运行：

```
# postfix start
postfix/postfix-script: fatal: the Postfix mail system is already running
```

如果你在修改配置时 Postfix 正在运行，那么这些更改不会被 Postfix 注意到。你可以停止并启动 Postfix 使其重新读取配置，但有一个更优雅的方法。只需输入 **postfix reload**：

```
# postfix reload
postfix/postfix-script: refreshing the Postfix mail system
```

这样，Postfix 只会重新加载配置，这耗时更短，并且不会中断 Postfix 为客户端提供的服务。

### 发送测试邮件

既然 Postfix 已启动，我们可以进行第一个测试：将发送给 root 的邮件投递到其邮箱。有两种非常简单的方法可以做到这一点：从命令行发送邮件，或通过 telnet 会话发送邮件。两种方法都有排除其他应用程序（如复杂的 GUI 邮件客户端）影响的优势，让你在出现错误时能专注于 Postfix。

#### 使用 Postfix 的 sendmail 二进制文件发送邮件

最简单、最可靠的测试是使用 sendmail 测试基本功能，因为这不涉及 Postfix 之外的任何组件。这个命令行工具出于向后兼容性仍被称为 sendmail——许多 Unix 系统上发送电子邮件的应用程序都硬编码了 sendmail 二进制文件的路径，/usr/sbin/sendmail 或 /usr/lib/sendmail。Postfix 也把自己的 sendmail 二进制文件放在这里，以便从 Sendmail 到 Postfix 的平滑过渡转换。⁴

输入以下命令向 root 发送邮件：

```
# echo foo | /usr/sbin/sendmail -f root root && tail -f /var/log/maillog
```

这将向 root 发送文本 foo，信封发件人为 root，并打开你的邮件日志以检查其投递状态：

```
Aug 20 21:56:42 mail postfix/pickup[5160]: 848AD7247: uid=0 from=<root>
Aug 20 21:56:42 mail postfix/cleanup[5340]: 848AD7247: message-id=<20030820195642.848AD7247@mail.example.com>
Aug 20 21:56:42 mail postfix/nqmgr[5161]: 848AD7247: from=<root@mail.example.com>, size=306, nrcpt=1 (queue active)
Aug 20 21:56:42 mail postfix/local[5343]: 848AD7247: to=<admin@mail.example.com>, orig_to=<root>, relay=local, delay=0, status=sent (mailbox)
```

从邮件日志中可以看到，Postfix 能够将消息发送到邮箱。你可以通过运行 `less /var/mail/admin` 来验证：

```
From root@mail.example.com  Wed Aug 20 21:56:42 2003
Return-Path: <root@mail.example.com>
X-Original-To: root
Delivered-To: admin@mail.example.com
Received: by mail.example.com (Postfix, from userid 0)
    id 848AD7247; Wed, 20 Aug 2003 21:56:42 +0200 (CEST)
Message-Id: <20030820195642.848AD7247@mail.example.com>
Date: Wed, 20 Aug 2003 21:56:42 +0200 (CEST)
From: root@mail.example.com (root)
To: undisclosed-recipients:;

foo
```

⁴ 有一个需要注意的地方：如果你从 Sendmail 迁移到 Postfix，你最终可能会有两个 sendmail 二进制文件：一个是 Postfix 安装的，另一个是真正的 Sendmail 留下的。你必须只使用 Postfix 安装的那个。

注意 如果你不确定在哪里寻找邮箱，请输入 **postconf mail_spool_directory**。这会告诉你 Postfix 将邮件投递到哪里。

到目前为止一切顺利。Postfix 能够处理自己的应用程序。

*从命令行发送邮件*

接下来我们将验证是否能从 localhost 上的 MUA 向 root 发送邮件。这是第二个最简单的测试案例：

```
# mail admin
Subject: Test from command line
This is a test mail from command line.
.
```

提示 如果你不熟悉 mail 程序，以下是使用方法：

1. 在命令行输入 **mail**。
2. 输入你想发送邮件到的账户名，然后按回车键。
3. 在提示下，输入主题并按回车键。
4. 输入邮件正文。
5. 要发送消息，开始一个新的空行，输入一个句点 (.)，然后按回车键。

要验证邮件是否已发送，请再次运行 **less /var/mail/admin**：

```
# less /var/mail/admin
From root@mail.example.com  Wed Aug 20 20:55:11 2003
Return-Path: <root@mail.example.com>
X-Original-To: admin
Delivered-To: admin@mail.example.com
Received: by mail.example.com (Postfix, from userid 0)
        id 37DE07247; Wed, 20 Aug 2003 20:55:11 +0200 (CEST)
To: admin@mail.example.com
Subject: Test from command line
Message-Id: <20030820185511.37DE07247@mail.example.com>
Date: Wed, 20 Aug 2003 20:55:11 +0200 (CEST)
From: root@mail.example.com (root)

This is a test mail from command line.
```

邮件已成功投递，我们已经证明本地用户可以向其他本地用户发送邮件。现在是时候检查是否可以从远程用户向 admin 发送邮件了。

*通过 Telnet 会话发送邮件*

最简单的邮件客户端是一个连接到 SMTP 端口（端口 25）的 telnet 客户端。我们将采用更底层的方式来操作，因为我们希望排除其他更舒适（但也更容易出错）的邮件客户端可能引入的副作用。以下是使用 telnet 发送邮件的方法。



# telnet mail.example.com 25
尝试连接 172.16.0.1...
已连接到 mail.example.com.
转义字符为 '^]'.
220 mail.example.com ESMTP Postfix
HELO client.example.com
250 mail.example.com
MAIL FROM: <test@client.example.com>
250 Ok
RCPT TO: <root@example.com>
250 Ok
DATA
354 以 <CR><LF>.<CR><LF> 结束数据
来自 telnet 会话的测试邮件。
.
250 Ok: 已排队，编号为 69F1A7247
QUIT
221 再见

最后，使用 `less /var/mail/admin` 来检查邮件是否送达：

```
From test@client.example.com  Wed Aug 20 21:25:16 2003
Return-Path: <test@client.example.com>
X-Original-To: root@example.com
Delivered-To: admin@mail.example.com
Received: from client.example.com (mail.example.com [172.16.0.1])
        by mail.example.com (Postfix) with SMTP id 2D89A7251
        for <root@example.com>; Wed, 20 Aug 2003 21:24:59 +0200 (CEST)
Message-Id: <20030820192459.2D89A7251@mail.example.com>
Date: Wed, 20 Aug 2003 21:24:59 +0200 (CEST)
From: test@client.example.com
To: undisclosed-recipients:;

来自 telnet 会话的测试邮件。
```

这封邮件也已成功送达，我们已证实 Postfix 能够接受从远程用户发送到本地用户的消息，并且能够成功投递它们。

## 将电子邮件地址映射到用户名

既然我们已经成功设置了基础环境，现在是时候配置一些更复杂的电子邮件地址了。默认情况下，Postfix 只会将邮件投递到您邮件服务器上的用户名。然而，像 y0000247 这样的用户名（也常用于用户检索邮件时的身份验证）很少与人们日常交流中使用的名称（如 john.doe@example.com）相匹配。为了让 Postfix 能够接收和投递使用真实世界常见名称的邮件到现有账户，您需要创建别名，将这些别名指向 Postfix 要投递邮件的目标账户。

## 创建别名

假设您在 Example Inc. 有一位名叫 John Doe 的新同事，您的任务是为他提供一个电子邮件账户。John 在销售部工作，他需要接收发送到 john@example.com、john.doe@example.com 和 doe@example.com 的邮件到同一个邮箱，同时也要接收发送到 sales@example.com 的邮件，他与 Silvia 和 Karol 在该部门共事，他们两人都需要接收发送到 <sales@example.com> 的邮件。John 已经被分配了 john 这个账户名，他可以使用该账户访问自己的文件。

您现在必须做的是将这些别名（john@example.com、sales@example.com 等）映射到他的本地用户名。这通过在 /etc/postfix/aliases 文件中创建条目来完成。对于 John 的情况，您只需要创建三个条目，尽管实际上需要四个映射。您不需要创建的是 <john@example.com>，因为任何发送到该地址的邮件都会被投递到用户名 john，也就是 John 的账户。您需要在 /etc/postfix/aliases 中添加以下条目：

```
# 用户
john.doe:	john
doe:		john
# 组
sales:		silvia, karol, john
```

为了完成您的任务，您需要运行 **postalias hash:/etc/postfix/aliases** 或 **newaliases** 来更新您的 aliases.db 文件。

> **注意** 从上面的列表中，您可以看到必须*在冒号左侧指定本地部分，右侧是用户名*（电子邮件地址的本地部分是 @ 符号之前的所有内容）。每个别名条目可以由一个或多个用逗号分隔的值组成。您可以指定用户名或电子邮件地址。电子邮件地址可以指向不同主机上的其他用户，这意味着您可以为您的邮件服务器上的一个用户接收邮件，并将其投递到一个完全不同的地址。更多信息可以在 aliases 文件本身中找到，或者您可以运行 **man 5 aliases**。

一旦您添加了所有需要的别名，现在就可以像我们之前做的测试一样，对这些邮箱进行测试。

## 设置权限以允许 Postfix 从您的网络中继电子邮件

*开放中继*是邮件系统管理员的噩梦。默认情况下，任何 Postfix 安装都是中继安全的。在其默认配置中，Postfix 只会中继来自您网络内部 IP 地址的消息。Postfix 通过检查您为服务器配置的接口来了解您网络的 IP 地址。

> **注意** 在 Linux 服务器上，Postfix 将信任机器接口所在的*所有子网*。在 Linux 上运行 **ifconfig** 可以获取 Postfix 默认会信任的所有子网列表。

只要您的服务器及其上运行 Postfix 的主机位于同一网络范围内，默认设置就能正常工作。当您的网络增长或变得更复杂时，您可能需要更改这些设置。例如，您可以决定在 DMZ 中运行 Postfix，其 IP 范围与内部主机使用的范围不同。在这种情况下，Postfix 可能不会允许您的客户端向外部目的地中继邮件，您需要对其进行配置以建立正确的中继权限。

扩展或限制中继权限可以通过通用方式或单独方式完成：通用方式是通过选择适合您网络拓扑结构的 `mynetworks_style`；单独方式是通过手动指定 IP 地址列表或以无类别域间路由（CIDR）表示法（参见附录 C）指定的范围来设置 `mynetworks`。

两种方法都需要您手动更改 `main.cf` 中的配置。对于静态 IP 范围，管理开销是合理的，因为它们不经常更改。

> **注意** *如果您想为具有动态 IP 地址的主机（这些主机的 IP 地址会定期更改）允许中继，则手动管理开销是不合理的。手动应用更改很快就会变成一项繁琐的任务。第 16 章解释并展示了如何自动化此过程。*

### 通用网络中继权限

通用中继权限通过 `mynetworks_style` 设置，可选择 class、subnet 或 host 选项。

#### class

class 选项将使 Postfix 将中继权限扩展到服务器配置的整个 IP A/B/C 类网络。例如，如果您在 IP 地址为 192.0.34.166 的机器上运行 Postfix，并且启用了 `mynetworks_style = class`，Postfix 将信任整个 C 类网络 192.0.34.0/24，并允许该范围内的主机中继邮件。

#### subnet

subnet 选项将使 Postfix 将中继权限限制在您配置的服务器网络接口所在的精确子网。例如，如果您在 IP 地址为 192.0.34.166/30 的机器上运行 Postfix，并且启用了 `mynetworks_style = subnet`，Postfix 将信任正好在此范围内的所有主机。

#### host

host 选项将使 Postfix 将中继权限限制在运行 Postfix 的服务器本身。例如，如果您在 IP 地址为 192.0.34.166/30 和 127.0.0.1 的机器上运行 Postfix，并且启用了 `mynetworks_style = host`，Postfix 将仅信任这些主机（IP 地址 127.0.0.1 和 192.0.34.166）。

### 单独中继权限

单独的中继权限通过 **mynetworks** 设置，方法是创建一个以逗号分隔的列表，列出所有需要 Postfix 中继消息的主机和网络（以 CIDR 表示法）。

例如，如果您在一个连接两个位置（192.168.100.0/24 和 192.168.200.0/24）的网络中运行 Postfix，并且您希望它允许其所在的 DMZ 中的所有主机（10.0.0.0/30）以及其自身的任何本地接口（127.0.0.0/8）中继邮件，您可以指定如下列表：

```
mynetworks = 127.0.0.0/8, 192.168.100.0/24, 192.168.200.0/24, 10.0.0.0/30
```

> **注意** *如果您有许多 IP 地址和范围，这种列表在 main.cf 中可能会变得相当复杂。或者，您可以将 mynetworks 指向一个单独的文件（mynetworks = hash:/etc/postfix/mynetworks），并在该文件中创建复杂的列表。不过，此文件可能不能包含 CIDR 表示法的网络。如果您需要 CIDR 表示法，请使用 mynetworks = cidr:/etc/postfix/mynetworks。*



## 单域拨号邮件服务器

设置一个使用拨号连接的邮件服务器只需对基本 Postfix 配置进行少量修改。拨号连接互联网可能会产生费用（尤其在欧洲，因为有连接计费），因此您可能不想运行一个为每封发出的邮件都发起连接的邮件服务器。相反，您可以让服务器先收集一定数量的邮件再发送，以使拨号过程更具成本效益。

当拨号连接激活时，您会希望 Postfix 通过 ISP 的中继主机转发排队的消息。此外，您可能需要支持 SMTP 认证。您还应该自动检索在服务器离线时无法投递给本地用户的消息。

拨号服务器与基本 Postfix 配置之间的区别如下：

**连接**
由于邮件服务器只是临时连接到互联网，其 IP 地址很可能会随每次新连接而变化。

**DNS 解析**
服务器离线时无法解析主机名。此外，服务器自身的 DNS 信息会随每次新连接而变化，因此可能无法进行正确的反向解析。

**投递限制**
您的 ISP 要求您使用其中继主机，而且中继主机可能仅为已认证用户转发消息。

**邮件检索**
外部邮件服务器无法直接向您的服务器投递消息，因为您的服务器通常不在线。您的 ISP 应通过使用一台保存您邮件的邮件服务器来解决此问题。当有人向您发送消息时，ISP 的邮件服务器会接受并存储该消息，直到您通过 POP/IMAP 客户端或 fetchmail 检索邮件并将其传递给本地 MTA。

> **注意** 本书不涵盖使用 POP/IMAP 和 fetchmail (http://catb.org/~esr/fetchmail) 进行邮件检索的内容。

图 4-1 展示了一个典型的拨号网络。一台或多台机器位于专用网络中，任何需要访问互联网服务的机器都通过您的拨号网关，该网关同时运行您的 Postfix 服务器。

*图 4-1：典型的拨号网络*

要将 Postfix 配置为单域拨号邮件服务器，需要执行以下步骤。这些步骤在后续各节中描述。

1. 禁用 DNS 解析。
2. 调整中继权限。
3. 设置中继主机。
4. 延迟消息传输。
5. 触发消息投递。
6. 为中继主机配置中继权限。

> **注意** 此场景建立在第 3 章配置的基础上。您需要按照该章所述来配置和测试服务器。此外，您应该已经配置了服务器的拨号程序 (http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/PPP-HOWTO.html)。

## 禁用 DNS 解析

当 Postfix 收到要投递到远程域的消息时，它必须查找目标域的 MX 或 A 记录。DNS 服务器上的名称查找通常需要发送离开您网络的查询，这意味着服务器必须连接到互联网。

由于您希望尽可能减少拨号连接，因此应该指示 Postfix 在服务器上线之前不要查找 DNS 数据。实际上，Postfix 根本不应该查找远程域，因为您希望它通过 ISP 的中继主机发送消息，而中继主机本身可以确定消息的发送位置。

要防止 Postfix 查找 DNS 数据，请在 `main.cf` 文件中设置 `disable_dns_lookups` 参数：

```
disable_dns_lookups = yes
```

这将抑制 `smtp(8)` 客户端中的 DNS MX/A 查找以及 `lmtp(8)` 客户端中的 A 查找；在这两种情况下都使用 `gethostbyname()`。在本章后面设置中继主机时，您需要记住这一点。

设置 `disable_dns_lookups` 参数后，重新加载 Postfix 以激活更改。

> **注意** 此设置不会禁用 `smtpd` 服务器程序的 DNS。像 `reject_unknown_sender_domain` 和 `permit_mx_backup`（参见第 8 章）这样的参数仍然有效，无论 `disable_dns_lookups` 的值如何。

## 调整中继权限

拨号服务器通常具有动态 IP 地址，每次连接到互联网时都会更改。因此，除非您在每次服务器上线时手动设置中继权限，否则无法控制拨号服务器网络接口的中继权限。此外，互联网上谁会想要通过拨号主机中继呢——除了垃圾邮件发送者？

> **注意** 即使您的主机只是周期性地连接互联网，也绝不应该允许整个互联网的中继访问。作者的一台拨号邮件服务器在 30 天内收到了 56 次（失败的）中继尝试。这大约是每天两次，而且该机器甚至不是 24/7 在线！幸运的是什么都没发生，因为它是中继安全的。

除非您出于某种特殊原因希望互联网上的某些用户使用您的 Postfix 服务器作为中继（参见第 16 章），否则应该将 `main.cf` 中的中继权限限制为本地网络接口和回环接口。如果您的专用网络是 192.168.0.0/24，可以这样做：

```
mynetworks = 192.168.0.0/24, 127.0.0.1/8
```

> **注意** 不要使用 `mynetworks_style = class` 来控制拨号服务器的中继权限。此设置会为网络接口配置的所有 IP 地址范围授权，包括服务器拨入的网络。因此，ISP 网络中的每个客户端都可以使用您的邮件服务器中继消息！

与之前一样，使用 **postfix reload** 重新加载配置。

## 设置 ISP 中继主机

在执行此特定配置步骤之前，您需要确定您的 ISP 邮件中继主机。许多 ISP 会阻止拨号客户在 TCP 端口 25（SMTP 端口）上的出站连接，因为垃圾邮件发送者会滥用拨号服务试用优惠。

> **注意** 除了您的 ISP 自身的要求之外，还有很多充分的理由不应让 Postfix 直接将消息投递到最终目的地。例如，由于大量垃圾邮件来自拨号机器，黑名单已经开始将已知垃圾邮件发送者使用的整个拨号网络（模拟、ISDN 和 DSL）地址段列入其中。即使您的消息不是垃圾邮件，远程 MTA 也可能因为 DUL（拨号用户列表）而拒绝它，仅仅因为您的邮件来自属于拨号池的 IP 地址范围。

例如，如果中继主机是 `relay.example.com`，您将使用这一行：

```
relayhost = [relay.example.com]
```

将中继主机的名称或地址放在方括号中可以禁用对该主机的 MX 查找。
执行通常的 **postfix reload** 之后，您就可以继续了。

## 延迟消息传输

此时，Postfix 已具有这样的配置：可以在不进行 DNS 查找的情况下将邮件投递到中继主机，从而避免任何开放中继问题。然而，服务器仍然会在收到发往远程网络的出站邮件时拨号连接到 ISP。要停止此行为并让 Postfix 将出站消息排队，请编辑 `main.cf`，通过 `defer_transports` 参数告诉 Postfix 延迟 SMTP 传输方式，如以下示例所示。

```
defer_transports = smtp
```

> **注意** 如果您使用的是 UUCP 而不是 SMTP，可以用 `uucp` 替换 `smtp`。

与往常一样，在做出此更改后以 root 身份执行 **postfix reload**。重新加载后，Postfix 将不再通过 SMTP 投递消息，直到 `defer_transports` 参数被更改或移除。下一节将介绍如何在服务器拨号连接到 ISP 时利用此功能投递消息。

## 触发消息投递

剩下的唯一任务是指示 Postfix 在连接到互联网时通过 SMTP 投递所有排队的邮件。您所要做的就是在服务器上线时自动重新配置 Postfix，然后恢复原始配置。这可以通过在系统建立连接后运行的脚本来触发。在运行 PPP 的 Linux 系统上，这些脚本通常位于 `/etc/ppp/ip-up.d`。

在此目录中创建一个名为 `postfix` 的脚本，使其在设置 `resolv.conf` 的脚本**之后**运行。`postfix` 脚本如下所示：

```
## 启动或重新加载 Postfix（如果需要）
# 如果 Postfix 以 chroot 运行，请将 resolv.conf 复制到 Postfix 使用的 resolv.conf
cp -p /etc/resolv.conf `postconf -h queue_directory`/etc/resolv.conf ①
# 取消设置 defer_transports 并让 Postfix 注意到它
postconf -e "defer_transports ="
postfix reload
# 强制运行队列以投递任何待发邮件
postfix flush
```

> ① 涉及 `resolv.conf` 的行仅在 Postfix 以 chroot jail 方式运行时相关。它假定服务器在拨号连接时会更改其 `resolv.conf` 文件。Postfix 也需要知道当前的名称服务器，因此此命令将新版本复制到 chroot jail 中，以便 Postfix 能在那里找到它。

类似地，当机器离线时，您需要恢复之前的排队行为。在 `/etc/ppp/ip-down.d` 中创建一个名为 `postfix` 的脚本，在连接断开时运行（同样，涉及 `resolv.conf` 的行仅在 chroot jail 中是必要的）：

```
## 启动或重新加载 Postfix（如果需要）
# 将 resolv.conf 复制到 Postfix 使用的 resolv.conf（仅在 Postfix 被 chroot 时）
cp -p /etc/resolv.conf `postconf -h queue_directory`/etc/resolv.conf
# 设置 defer_transports 并让 Postfix 注意到它
postconf -e "defer_transports = smtp"
postfix reload
```



# 为中继主机配置中继权限

许多免费邮件提供商，特别是那些同时提供 SMTP 客户端访问和 Web 邮件界面的提供商，在允许客户端使用其中继主机之前，要求进行额外的验证。这是必要的，因为它们的大多数用户是从其他接入提供商（因此，从不同于其自身的 IP 范围）连接的，因此无法基于 IP 地址设置中继权限。如果邮件提供商将其邮件服务器开放给广泛的 IP 地址范围，它们实际上将成为开放中继，并且在几分钟内垃圾邮件发送者就会开始利用它们。因此，邮件提供商要求使用“发信前收信”或 SMTP 认证。

# 发信前收信

要求“发信前收信”的提供商（参见第 15 章）仅在你发送任何新消息之前检索传入邮件时，才接受传出的中继消息。换句话说，你的机器必须在发送任何内容之前向提供商的 POP3 或 IMAP4 服务器进行身份验证。当你的主机通过身份验证时，提供商会记录你当前的 IP 地址，并允许该 IP 地址在特定时间窗口内通过其转发器发送消息。

Postfix 是一个邮件传输代理；它*不*支持 POP3 和 IMAP4。因此，Postfix 无法自行执行“发信前收信”。这不是问题，因为你可以轻松配置 fetchmail (http://catb.org/~esr/fetchmail) 为你完成此操作。Fetchmail 是一个小型命令行实用程序，可以从 Internet 上几乎任何类型的邮件系统中检索邮件。要在“发信前收信”设置中使用它，请执行以下步骤：
1.  按照本章所述配置 Postfix。
2.  按照 fetchmail 文档中的说明创建一个有效的配置。
3.  在你的 /etc/ppp 拨号脚本中，在重新配置 Postfix *之前*，添加一个调用 fetchmail 的触发器。

这样，你的服务器在运行 Postfix（SMTP）出队阶段之前至少运行一次 fetchmail（一个 POP/IMAP 客户端），因此你的邮件提供商将接受你的传出消息。

# SMTP 认证

要求 SMTP 认证的提供商仅当你的客户端或服务器在 SMTP 对话期间通过身份验证后，才允许其通过其中继主机转发消息。要在 Postfix 中使用 SMTP 认证，你不需要任何额外的服务或程序，因此它比“发信前收信”更可取（特别是在你想发送消息但不检索任何内容的情况下）。

你可以在第 16 章中找到关于如何为 Postfix 配置客户端 SMTP 认证的详细信息。

# POSTFIX 的结构

本章描述了 Postfix 的工作原理、系统的每个组件的作用，以及这些组件如何相互关联。在了解这些材料之后，你应该能对 Postfix 有一个整体的理解，以便你可以专注于各个目标。

Postfix 由少数与用户进程交互的程序（`sendmail`、`postqueue`、`postsuper` 等）和更多在后台运行的程序组成。只有在后台运行的程序由 `master` 守护进程控制。`master` 守护进程的工作是确定有待完成的工作并分派适当的程序来完成工作。这种模块化设计允许更高水平的安全性，因为每个程序都以完成其任务所需的最低权限集运行。

你可以将整个 Postfix 系统想象成一个路由器。起初这可能听起来很奇怪，但请记住，路由器的工作是查看 IP 数据包，确定目标 IP 地址（以及可能的源地址），然后选择正确的接口将数据包路由到其目的地。Postfix 对邮件做同样的事情，查看消息的目标（信封收件人）和源（信封发件人），以确定哪个应用程序将消息移动到其最终目的地。

![](img/852c79f689feb77c5fde686b993808b1_63_0.png)

*图 5-1：Postfix 的工作原理类似于路由器*

![](img/852c79f689feb77c5fde686b993808b1_64_0.png)

*图 5-2：一个 Postfix "路由器"接受并建立各种类型的连接*

现在让我们更仔细地观察系统。真正的路由器通常从多个接口接收 IP 数据包，并通过这些接口将它们路由出去。Postfix 也是如此；它从多个来源接收消息，然后将邮件传递到多个目的地。消息的来源可以是本地 sendmail 二进制文件，或 SMTP 或 QMQP 连接。目的地可以是本地邮箱、传出 SMTP 或 LMTP、传入程序的管道等。图 5-2 展示了 Postfix 的这一视图。

消息的来源和目的地似乎很清楚，但 Postfix 如何根据目的地选择传递方法？路由器使用将 IP 地址与网络匹配的路由表来确定路径。Postfix 对电子邮件地址做同样的事情。

在 Postfix 中，查找表称为 *maps*。Postfix 不仅使用 maps 来查找邮件发送的位置，还用于对客户端、发件人和收件人施加限制，以及检查电子邮件内容中的某些模式。图 5-3 展示了 maps（仅举几例，如别名、虚拟和传输）的适用位置。

![](img/852c79f689feb77c5fde686b993808b1_64_1.png)

*图 5-3：Maps 是 Postfix "路由器"的查找表*

# Postfix 守护进程

图 5-4 展示了 Postfix 守护进程的概览以及它们如何协同工作。

> **注意** *Postfix 不断发展。以下守护进程列表基于 Postfix 2.1。*

**master**

master 守护进程是 Postfix 的主管，它监督所有其他 Postfix 守护进程。master 等待待处理的任务被分配给下属守护进程。如果有大量工作要做，master 可以调用守护进程的多个实例。你可以配置同时运行的守护进程实例数量、Postfix 可以重用它们的频率，以及在停止实例之前应经过的不活动时间段。

如果你曾经在 Unix 机器上使用过 inetd 服务器，你会发现它与 *master* 守护进程之间有许多相似之处。

**bounce 和 defer**

邮件传输代理必须通知发件人有关无法投递的邮件。在 Postfix 中，bounce 和 defer 守护进程处理此任务，该任务由队列管理器 (qmgr) 触发。具体来说，导致发件人通知的两种事件类型是不可恢复的错误和长时间无法到达的目的地。后者会导致延迟警告。

> 图 5-4：Postfix 守护进程之间的关系

![](img/852c79f689feb77c5fde686b993808b1_65_0.png)

# error

error 守护进程是一个邮件投递代理，就像 local 或 smtp 一样。它是一个始终导致邮件被退回的投递代理。通常你不会使用它，除非你将某个域配置为不可投递，方法是将邮件定向到 error 投递代理。如果邮件被发送到 error 守护进程，它将通知 bounce 守护进程记录收件人无法投递。

**trivial-rewrite**

trivial-rewrite 守护进程响应清理守护进程 (cleanup daemon) 的请求，将非标准地址重写为标准的 user@fqdn 形式。该守护进程还根据队列管理器 (qmgr) 的请求解析目的地。默认情况下，trivial-rewrite 仅区分本地和远程目的地。

**showq**

showq 守护进程列出 Postfix 邮件队列，它是 mailq (sendmail -bp) 命令背后的程序。这个守护进程是必要的，因为 Postfix 队列不是全局可读的；非 setuid 用户程序无法列出队列（而 Postfix 二进制文件不是 setuid 的）。

**flush**

flush 守护进程尝试清除待处理和延迟消息的邮件队列。通过使用按目的地组织的待发邮件列表，它提高了 SMTP Extended Turn (ETRN) 请求及其命令行等效项 sendmail -qR destination 的性能。你可以使用 main.cf 文件中的 fast_flush_domains 参数来维护目的地列表。

**qmgr**

qmgr 守护进程管理 Postfix 队列；它是 Postfix 邮件系统的核心。它将投递任务分配给 local、smtp、lmtp 和 pipe 守护进程。在委派任务后，它会将队列文件路径名信息、消息发件人地址、目标主机（如果目的地是远程的）以及一个或多个消息收件人地址提交给它委派投递任务的守护进程。qmgr 的设计是 Postfix 如何处理任务以避免资源耗尽并保持稳定性的一个好例子。有两点突出：
*   qmgr 维护一个较小的活动队列，其中只有几条待投递的消息。该队列有效地充当了潜在更大的传入队列和延迟队列的有限窗口，并防止 qmgr 在高负载下内存耗尽。
*   如果 Postfix 无法立即投递消息，qmgr 会将消息移动到延迟队列。将暂时无法投递的消息保存在单独的队列中，确保大量邮件积压不会减慢正常的队列访问速度。

qmgr 使用 bounce 和 error 守护进程来为 relocated 表中列出的收件人退回邮件，该表包含系统中不再存在的用户或域的联系信息。



## proxymap

Postfix 客户端进程可以通过 proxymap 守护进程以只读方式访问映射表。通过在许多 Postfix 守护进程之间共享单个打开的映射表，proxymap 规避了 chroot 限制，并减少了打开查找表的数量。

## spawn

spawn 进程按需创建非 Postfix 进程。它监听 TCP 端口、Unix 域套接字或 FIFO，这些连接到标准输入、输出和错误流。本书中讨论 spawn 的唯一用途是用于第 13 章中的 Postfix 外部内容过滤系统。

## local

顾名思义，local 守护进程负责本地邮箱投递。Postfix local 守护进程可以写入 mbox 和 Maildir 格式的邮箱。此外，local 可以访问 Sendmail 风格的别名数据库和用户 .forward 文件中的数据。

> **注意** *这些功能使 local 成为 Sendmail 邮件投递代理的对应物，而且它们两者都保持相同的用户界面。*

作为替代方案，local 可以将邮箱投递委托给提供高级功能（如过滤）的本地投递代理（LDA）。两个非常流行的 LDA 是 procmail (http://www.procmail.org) 和 maildrop (http://www.flounder.net/~mrsam/maildrop)。

Postfix 可以运行多个 local 实例。

## virtual

virtual 守护进程，有时称为 *虚拟投递代理*，是 local 的精简版本，专门投递到邮箱。它是 Postfix 中最安全的投递代理；它不会执行别名和 .forward 文件扩展。

该投递代理可以为多个域投递邮件，这使其特别适合在单台机器上托管多个小域（所谓的 POP toaster），而无需真实的系统或 shell 账户。

### smtp

smtp 客户端是将出站消息传输到远程目标的 Postfix 客户端程序。它查找目标邮件交换器，按优先级排序列表，并尝试每个地址，直到找到响应的服务器。繁忙的 Postfix 系统通常同时运行多个 smtp 守护进程。

### lmtp

lmtp 客户端使用 RFC 2033 (ftp://ftp.rfc-editor.org/in-notes/rfc2033.txt) 中定义的本地邮件投递协议（LMTP）与本地和远程邮箱服务器通信。它通常与 Cyrus IMAP 服务器 (http://asg.web.cmu.edu/cyrus/imapd) 一起使用。

使用 Postfix `lmtp` 客户端的设置优势在于，Postfix 处理所有队列管理，并且一台 Postfix 机器可以通过 LMTP 为多个邮箱服务器（需要具有 LMTP 守护进程）提供邮件。反之亦然：多台 Postfix 机器可以通过 `lmtp` 为一台邮箱服务器提供邮件。这些邮箱服务器可以例如运行 Cyrus IMAP。

### pipe

`pipe` 邮件客户端是其他邮件传输机制的出站接口。它使用参数调用程序，并将消息体通过管道传输到它们的标准输入。

## pickup

`pickup` 守护进程拾取由本地 `sendmail` 用户客户端程序放入 `maildrop` 队列的消息。在执行一些健全性检查后，`pickup` 将消息传递给 `cleanup` 守护进程。

## smmtpd

`smtpd` 守护进程处理与网络邮件客户端的通信，这些客户端通过 SMTP 将消息投递到 Postfix。`smtpd` 执行许多检查以保护 Postfix 系统的其余部分，并且可以配置为实施未经请求的商业电子邮件（UCE）控制（本地或基于网络的黑名单、DNS 查找、其他客户端请求等）。
接受消息后，`smtpd` 将其放入传入队列，由 `qmgr` 接管。

## cleanup

`cleanup` 守护进程是新消息的最终处理阶段。它添加任何必需的缺失头，安排地址重写，以及（可选）从消息头中提取收件人地址。`cleanup` 守护进程将结果插入传入队列，然后通知队列管理器新邮件已到达。

## sendmail

`sendmail` 是一个 Postfix 命令，用于替代和模拟 Eric Allman 的 MTA Sendmail。其目的是为那些只调用 `/usr/sbin/sendmail` 的应用程序提供与 Sendmail 兼容的接口。它与 `postdrop` 二进制文件交互，将邮件放入 `maildrop` 队列以供 pickup。

> **注意** *`sendmail` 是将邮件注入 Postfix 队列系统的最慢方式。如果您需要一次性发送大量邮件，请改用 SMTP。*

## qmqpd

Postfix QMQP 服务器实现了快速邮件排队协议（QMQP；参见 http://cr.yp.to/proto/qmqp.html），以使 Postfix 与 `qmail` 和 `ezmlm` 列表管理器兼容。

## anvil

Postfix `anvil` 是针对 SMTP 客户端和拒绝服务攻击的初步防御，这些攻击用太多同时或连续的连接尝试淹没 SMTP 服务器。它附带白名单功能，可以为授权客户端禁用限制。anvil 不包含在 Postfix 2.1 中，但在 Postfix 2.2 实验版本中可用。anvil 将保持实验状态，直到有足够的 Postfix 速率限制经验。

# Postfix 队列

Postfix 轮询 `main.cf` 文件中由 `queue_directory` 参数指定的目录中的所有队列。队列目录通常是 `/var/spool/postfix`。每个队列都有自己的子目录，名称标识该队列。Postfix 处理的所有消息都保留在这些目录中，直到 Postfix 投递它们。您可以通过消息的队列确定其状态：incoming、maildrop、deferred、active、hold 或 corrupt。

## incoming

所有进入 Postfix 队列系统的新消息都由 cleanup 服务发送到 incoming 队列。新队列文件以 `postfix` 用户作为所有者创建，访问模式为 `0600`。一旦队列文件准备好进行进一步处理，cleanup 服务将队列文件模式更改为 `0700`，并通知队列管理器新邮件已到达。队列管理器忽略模式为 `0600` 的不完整队列文件。

队列管理器在将新消息移入 active 队列时扫描 incoming 队列，并确保 active 队列的资源限制未被超过。默认情况下，active 队列最多有 20,000 条消息。

> **警告** *一旦达到 active 队列消息限制，队列管理器将停止扫描 incoming 和 deferred 队列。*

## maildrop

使用 `sendmail` 命令提交但尚未由 pickup 服务发送到主 Postfix 队列的消息在 maildrop 队列中等待处理。即使 Postfix 未运行，您也可以将消息添加到 maildrop 队列；Postfix 启动后会查看它们。

单线程的 pickup 服务定期扫描和排空 maildrop 队列，以及根据 `postdrop` 程序的通知。`postdrop` 程序是一个 setgid 辅助程序，允许无特权的 `sendmail` 程序将邮件注入 maildrop 队列，并通知 pickup 服务消息已到达。（所有进入主 Postfix 队列的消息都通过 cleanup 服务进入。）

## deferred

如果消息仍有因某些暂时性原因导致投递失败的收件人，并且消息已投递给所有可能的收件人，Postfix 将消息放入 deferred 队列。

队列管理器定期扫描 deferred 队列，将延迟的消息重新放回 active 队列。扫描间隔由 queue\_run\_delay 配置参数指定。如果 *deferred* 和 *incoming* 队列扫描碰巧同时进行，队列管理器在两个队列之间按消息交替进行。

## active

active 队列在某种程度上类似于操作系统的进程运行队列。active 队列中的消息已准备好发送，但不一定正在发送过程中。

队列管理器是一个投递代理调度程序，致力于确保在指定资源限制内快速公平地将邮件投递到所有目的地。

> **注意** *尽管大多数 Postfix 管理员认为 active 队列是磁盘上的目录，但真正的 active 队列是队列管理器进程内存中的一组数据结构。*

## hold

管理员可以定义 smtpd\_access(5) 策略和 cleanup 头部及正文检查（参见第 10 章），这些策略和检查会导致消息从正常处理中自动转移，并无限期地放入 hold 队列。放入 hold 队列的消息会一直保留在那里，直到管理员干预。hold 队列中的消息不会进行定期投递尝试。您可以运行 `postsuper` 命令手动将消息置于 hold 状态，或将消息从 hold 队列释放到 deferred 队列。

消息可能在 hold 队列中停留的时间超过 `maximal_queue_lifetime` 参数设置的队列文件生命周期（超过此时间后，未投递的消息将退回给发件人）。如果需要从 hold 队列中释放较旧的消息，您可以使用 `postsuper -r` 将它们移入 `maildrop` 队列，以便消息获得新的时间戳，并获得多次投递机会。

> **注意** *hold 队列在 Postfix 性能中不起太大作用；监控 hold 队列通常是为了跟踪垃圾邮件和恶意软件，而不是出于性能问题。*

## corrupt

corrupt 目录包含损坏的队列文件。Postfix 不是丢弃这些文件，而是将它们存储在这里，以便（人工）邮件管理员可以使用 `postcat` 检查它们。

Postfix 在启动时记录有关任何损坏文件的警告。

# 映射表

映射表是 Postfix 用于查找信息的文件和数据库。映射表有许多不同的用途，但它们都有一个共同点——左侧（LHS，或 *键*）和右侧（RHS，或 *值*）。

[content]
以下是几个键值对的示例：

| 键 | 值 |
|---|---|
| postmaster: | john |
| postmaster@example.com | john |
| 192.168.254.12 | REJECT |
| spammer@example.com | REJECT |
| /^Subject: your account {25}[a-z]{8}/ | REJECT Mail Virus Detected |

要使用映射，你需要指定一个键并获取相应的结果值。

> **注意** *此处的键和值来自各种文件，在单个文件中并不合理。前述列表仅作说明，展示所有映射条目都采用相同的基本形式。*

## 映射类型

Postfix 可以使用多种不同类型的映射。可用的格式取决于你的特定系统上编译 Postfix 的方式。要查明你的 Postfix 支持哪些格式，请在命令行运行 `postconf -m`。你应该会得到一个映射类型列表：

```
# postconf -m
btree
cdb
cidr
environ
hash
ldap
mysql
nis
pcre
proxy
regexp
sdbm
static
tcp
unix
```

## 索引映射（hash、btree、dbm 等）

索引映射是使用 `newaliases`、`postalias` 和 `postmap` 等命令从常规文本文件构建的二进制数据库。这些二进制映射具有索引格式，以便 Postfix 可以快速检索与键关联的值。作为进一步的性能改进，Postfix 守护进程在启动时会打开这些映射，并且除非注意到文件系统中的映射文件发生更改，否则不会重新读取它们。要重新加载映射，守护进程会退出，然后由主守护进程启动一个新的守护进程。

> **注意** 如果你有频繁更改的索引映射，使用这些映射的守护进程也会同样频繁地重启。在高负载下，这可能导致性能问题。

最常见的索引映射是从别名、虚拟、传输、重新定位和 sasl_passwd 文本文件构建的。你可以通过文件名识别映射文件，因为它是原始文件加上一个也告诉你索引格式的后缀。例如，使用 postalias 命令构建的别名映射文件名为 aliases.db。

> **注意** 当你创建文件以从中构建索引映射时，不必将键按特定顺序排列。使用索引映射的转换工具和程序不需要输入具有特定顺序。实际上，转换过程会移除顺序。

Postfix 按照 access(5) 手册页中指定的预定顺序查询条目。换句话说，每个映射查询实际上由一系列针对索引映射中单个键的单个查询（源自原始查询）组成。

## 线性映射（PCRE、regexp、CIDR 和平面文件）

线性映射是常规文本文件。Postfix 从上到下读取这些文件，这使其不同于索引映射。这种差异非常重要，因为文件中的第一个匹配项决定了 Postfix 将要执行的操作。Postfix 会忽略任何后续条目，无论它们是否匹配查询。

考虑以下正则表达式映射，其中查找 john.doe@example.com 返回 OK，因为第一行匹配。

```
/john\.doe@example\.com/  OK
/example\.com/           REJECT
```

但是，如果你交换正则表达式映射中的行，另一个条目会首先匹配，因此相同的 john.doe@example.com 查找将返回 REJECT：

```
/example\.com/           REJECT
/john\.doe@example\.com/ OK
```

你*不需要*将线性映射转换为二进制形式（事实上，你做不到）。Postfix 守护进程在启动时读取它们，并且在重新启动之前不会注意到映射的任何更改。典型的 Postfix 线性映射包括 header_checks、body_checks 和 mime_header_checks（参见第 9 章）。

> **警告** 随着你的线性映射增长，Postfix 守护进程处理它们所需的时间会更长。这对于正文或标题检查尤其如此，因为清理守护进程需要检查正文的每一行（最多 body_checks_size_limit）以及标题是否与映射的每一行匹配。

这可能导致明显的减速，特别是如果你有广泛的 *_checks 参数使用 regexp 或 PCRE（Perl 兼容的正则表达式）类型的映射来防止垃圾邮件进入系统。当这种情况发生时，通常是将复杂的垃圾邮件过滤交给外部应用程序处理的时候了。

要使 Postfix 守护进程注意到线性映射的更改，请运行 **postfix reload**。如果时间要求不严格，你可以设置 `max_use` 参数来定义守护进程的生存时间。一旦守护进程处理了该参数中指定数量的任务，它就会退出，并由 **master** 重启。重新启动后，它会重新读取所有需要的映射。

## 数据库（MySQL、PostgreSQL、LDAP）

Postfix 将数据库视为与索引映射相同。数据库查询的结果是**匹配**（连同查询返回的值）或**不匹配**。数据库映射和索引映射的主要区别在于，当数据库发生更改时，你不需要重启守护进程。Postfix 并不假设邮政局长是唯一可以更改数据库的人。

这种方法的缺点是数据库可能无法优雅地处理大量查询，因为 Postfix 需要对映射中的每次查找执行至少三个查询（参见后面的“Postfix 如何查询映射”部分）。在高负载下，数据库后端可能停止工作，你的邮件服务将容易受到自我引发的崩溃或拒绝服务攻击的影响。这种可能性不应阻止你使用数据库后端，但你应该意识到这种风险。

数据库查找对于高负载系统可能成为一个问题，但这不是唯一需要考虑的问题——延迟可能是另一个问题。数据库查询的延迟比索引映射更高，因为 Postfix 必须连接到数据库后端，发送查询，然后等待结果。使用索引映射时，Postfix 只需查询已经加载到内存中的数据。

如果数据库成为瓶颈，并且你没有过大的映射，你可以在数据库和 Postfix 之间插入一个映射。也就是说，你可以从完整的数据库查询创建一个索引映射，然后使用该映射运行 Postfix。你需要记住根据需要尽可能频繁地更新映射，但 **proxymap** 守护进程可用于显著减少并发连接数。

### 确定与数据库的并发连接数

Postfix 守护进程（`smtpd`、`smtp` 等）的进程限制（由 `default_process_limit` 设置）为 100 个并发进程。在峰值负载下运行，将会有 100 个并发的 `smtpd` 守护进程，每个守护进程都在为一次 access(5) 查找查询数据库后端（例如，因为我们使用映射来检查客户端是否在我们个人黑名单中，因此应拒绝其向我们发送邮件）。

请记住，一次查找至少会导致三次查询，因此对数据库的并发查询数至少为 `default_process_limit` * 3（在默认配置下，即 300 次查询），而并发连接数为 `default_process_limit`。这仅仅是 smtpd 守护进程的查询和连接数；其他守护进程（如 local 和 qmgr）可能正在处理其他作业，这会增加打开的连接数和并发查询数。

## Postfix 如何查询映射

映射可用于各种任务。Postfix 有使用映射的表驱动机制（参见 access(5)、aliases(5)、canonical(5) 和 transport(5)）。这些映射可以使用不同的查找机制（LDAP、NIS、SQL、btree、hash、regexp、cdb、cidr、pcre 等）。

1. `<localpart@domainpart>` 逐字匹配指定的邮件地址。
2. `<domainpart>` 将 *domainpart* 作为电子邮件地址的域名部分进行匹配。模式 *domainpart* 也匹配子域，但仅在字符串 `smtpd_access_maps` 列在 Postfix 的 `parent_domain_matches_subdomains` 配置设置中时才匹配。否则，请指定 *.domainpart*（注意开头的点）以匹配子域。
3. `<localpart@>` 匹配所有具有指定用户部分（*localpart*）的邮件地址，无论它们属于哪个域。
4. 失败 如果查找不匹配，Postfix 将返回未找到匹配项，查询以错误结束。

> **注意** *在某些查找表类型中无法查找空发件人地址。默认情况下，Postfix 使用 <> 作为空发件人地址的查找键。值在 `main.cf` 文件的 `smtpd_null_access_lookup_key` 参数中指定。*

这种查找顺序意味着 Postfix 为每个查询执行多次查找，除非你使用高延迟的映射（如 SQL 或 LDAP 映射），否则这实际上不是问题（当然，你应该预料到许多查找需要多次查询）。在你将所有映射放入 LDAP 然后在 postfix-users 邮件列表上抱怨“Postfix 很慢....”之前，这只是需要记住的一件事。

## 外部来源

Postfix 支持不构建在 Postfix 之上、甚至不由你直接控制的信息来源，例如黑名单（DNSBL 和 RHSBL 列表）、基于 DNS 的列表和其他外部来源。黑名单几乎专门用于 `smtpd_*_restrictions` 参数，以拒绝来自 DNSBL 或 RHSBL 风格列表中列出的客户端或发件人的邮件（参见第 7 章）。

与任何外部查询一样，这些查找可能由于连接问题、针对黑名单服务器的拒绝服务攻击和其他问题而失败。在超时或其他故障的情况下，Postfix 可能仍会接受邮件（绕过可能的限制），但它会在邮件日志中记录适当的警告。



## 命令行工具

Postfix 附带了一系列命令行工具，以协助您完成管理任务。尽管它们执行不同的功能（例如查询映射、检查队列文件、出队和重新排队消息以及更改配置），但它们都有一个共同点——它们的名称以“post”开头。

> **注意** *这些命令的功能远不止此处所述。我们重点关注您在日常操作中会遇到的选项。如果您在此处找不到所需信息，首先应查阅在线手册。*

### postfix

`postfix` 命令使用 `stop`、`start` 和 `reload` 选项来停止、启动和重新加载配置。

### postalias

`postalias` 命令从别名文件创建索引别名映射。它的工作原理与 `postmap` 命令（稍后描述）类似，但它特别注意别名文件中的表示法（其中冒号分隔键和值）。必须在别名文件上使用 `postalias`。

### postcat

`postcat` 命令显示邮件队列中消息的内容。
要读取邮件队列中的消息，您需要其队列 ID。运行 `mailq` 获取队列 ID 列表。例如，以下消息的队列 ID 是 F2B9715C0B3：

```
# mailq
F2B9715C0B3   2464 Mon Oct 13 15:29:39  markus.herrmann@example.com
                (connect to mail.example.com[217.6.113.151]: Connection timed out)
                           torsten.hecke@example.net
-- 2 Kbytes in 1 Requests.
```

获取队列 ID 后，将其用作 `postcat` 的选项以查看队列文件的内容：

```
# postcat -q F2B9715C0B3
```

### postmap

`postmap` 命令的主要目的是从平面文件构建索引映射。例如，要从 `/etc/postfix/virtual` 构建 `/etc/postfix/virtual.db`，请运行以下命令。

```
# postmap hash:/etc/postfix/virtual
```

`postmap` 命令可以做更多事情。其最有用的功能之一是能够测试您的 Postfix 安装支持的任何类型的映射。当调试配置时（其中对映射的查找似乎失败，并且您不确定键和值是否确实对 Postfix 可见），这非常有帮助。

### 调试查找表中的条目

要确定 Postfix 是否能在映射中找到条目，请使用 `postmap -q`。例如，以下命令返回映射 `/etc/postfix/sender_access`（类型为 `hash`）中分配给键 `<sender@example.com>` 的值：

```
# postmap -q sender@example.com hash:/etc/postfix/sender_access
OK
```

需要注意的是，`postmap` *不会*查找术语 `<sender@>`、`<example.com>` 和 `<com>`，即使这些术语出现在 `access(5)` 手册页中。您需要手动执行这些查找：

```
# postmap -q sender@ hash:/etc/postfix/sender_access
# postmap -q example.com hash:/etc/postfix/sender_access
# postmap -q com hash:/etc/postfix/sender_access
```

### postdrop

`postdrop` 命令从标准输入读取邮件，并将结果放入 `maildrop` 目录。此程序与 `sendmail` 实用程序配合使用。

### postkick

`postkick` 命令通过本地传输通道向 Postfix 守护进程发送请求，使 Shell 脚本和其他程序可以访问 Postfix 进程间通信。

> 注意 *postkick 命令向 Postfix 守护进程发送消息。这需要 Postfix 正在运行。*

### 重新排队消息

以下高级 `postkick` 示例展示了如何重新排队消息以立即重新投递：

```
# cat queueidlist | postsuper -r -
postkick public pickup W
```

此命令序列使用 postsuper -r - 命令将 queueidlist 中列出的所有选定消息移动到邮件投递队列，在那里 pickup 守护进程将像处理任何其他邮件一样处理它们。通过这样做，您将内容筛选器重置为适合本地提交的设置，并添加一个额外的 Received: 头。

postkick 命令请求立即扫描邮件投递队列。否则，消息将在邮件投递队列中最多停留 60 秒。pickup 守护进程将消息提交给清理守护进程，在那里它会获得一个新的队列 ID 并被存入传入队列。整个过程的要点是尽快将消息移至活动队列。

### postlock

postlock 命令让您获得 Postfix 写入的 mbox 文件的独占访问权限，然后在持有锁的情况下运行一个命令。您从 postlock 获得的锁与 Postfix 本地投递代理兼容。当您的命令执行时，Postfix 不会触碰该文件。以下是一个示例：

```
# postlock /var/mail/user from
```

> **警告** 尽量避免使用任何可能需要 CTRL-C 来终止的命令。中断 postlock 并不能保证锁会消失；您可能需要删除锁文件才能再次投递到邮箱。要查看是否有残留的锁文件，请运行不带命令的 **postlock**。如果它挂起并最终超时，您可能有一个遗留的锁。

### postlog

postlog 命令允许外部程序（例如 Shell 脚本）向邮件日志写入消息。这是一个与 Postfix 兼容的日志接口；默认情况下，它将命令行中的文本作为单条记录记录。以下是一个非常简单的示例：

```
# postlog This is a test
postlog: This is a test
# grep "This is a test" /var/log/mail.log
Feb 20 11:50:16 mail postlog: This is a test
```

### postqueue

postqueue 命令是 Postfix 队列的用户界面，为您提供传统上通过 sendmail 命令可用的功能。

-   `-f` 参数使 postqueue 请求队列管理器传递所有排队的邮件（刷新），无论目的地如何。这相当于 `postfix flush` 或 `sendmail -q`：

```
# postqueue -f
```

-   `-p` 参数使 postqueue 打印队列的内容。它等同于 `mailq`：

    ```
    # postqueue -p
    ```

-   `-s domain` 参数使 postqueue 尝试传递所有发往域的排队邮件。这相当于 `sendmail -q domain`：

    ```
    # postqueue -s example.com
    ```

> 注意 postqueue 命令向 Postfix 守护进程发送消息。这需要 Postfix 正在运行。

### postsuper

postsuper 命令维护 Postfix 队列内的作业。与 postqueue 不同，此命令仅限超级用户使用，并且可以在 Postfix 关闭时运行。在启动守护进程之前检查队列时需要一些 postsuper 功能。表 5-1 显示了 postsuper 命令的功能。

表 5-1：postsuper 命令的功能

| 选项 | 操作 |
| :--- | :--- |
| -d | 从指定的邮件队列中删除具有指定队列 ID 的消息 |
| -h | 将消息置于保留状态，使其不会被尝试投递 |
| -H | 释放当前保留的邮件 |
| -p | 清除崩溃后遗留的临时文件 |
| -r | 从指定的邮件队列重新排队具有指定队列 ID 的消息 |
| -s | 检查并修复队列结构 |

postsuper 最常用的用途之一是使用 `postsuper -d queueid` 从邮件队列中删除消息。手动执行此操作很繁琐，尤其是在删除许多文件时。以下 Perl 脚本（`delete_from_mailq`）使其更简单：

```perl
#!/usr/bin/perl
$REGEXP = shift || die "no email-address given (regexp-style, e.g. bl.*\n@yahoo.com)!";
@data = qx</usr/sbin/postqueue -p>;
for (@data) {
  if (/^\(\w+\)(\*|\!)?\s/) {
    $queue_id = $1;
  }
  if($queue_id) {
    if (/$REGEXP/i) {
      $Q{$queue_id} = 1;
      $queue_id = "";
    }
  }
open(POSTSUPER,"|cat") || die "couldn't open postsuper" ;
open(POSTSUPER,"|postsuper -d -") || die "couldn't open postsuper" ;
foreach (keys %Q) {
    print POSTSUPER "$_\n";
};
close(POSTSUPER);
```

以下是使用方法：

```
# mailq
C73A015C095   7509 Mon Oct 13 14:56:17  MAILER-DAEMON
        (connect to mx5.ancientaward.com[64.156.166.211]: Connection refused)
National_Nosepicking_Month@mx5.ancientaward.com
```

请注意，此处发件人被标识为 `<MAILER-DAEMON>`。要删除这些退回邮件，请以 root 身份运行 `delete-from-mailq`：

```
# delete-from-mailq MAILER-DAEMON
postsuper: C73A015C095: removed
postsuper: Deleted: 1 message
```



## 第二部分

### 内容控制

Postfix 提供了三个功能集，用于控制消息如何进入和离开邮件系统。利用这些功能，你可以基于 SMTP 对话和消息内容来管理消息流，也可以将内容管理委托给外部应用程序。这三类功能对应三组不同的配置参数：限制、检查和过滤器。

#### 邮件管理员的电子邮件入门
内容控制需要了解内容。要有效应用限制、检查和过滤器，你必须知道电子邮件中必须包含、应该包含以及可以包含哪些内容。请阅读第 6 章以深入了解电子邮件内容。

#### 消息传输限制如何工作
限制控制 SMTP 通信。第 7 章将解释限制如何工作。请花时间仔细阅读；这将使实施限制变得容易得多。

#### 使用消息传输限制
在第 8 章中，我们将向你展示如何实施限制。它们几乎都可以立即使用。

#### 内置内容过滤器如何工作
检查基于消息内容执行其工作。但它们是如何工作的呢？第 9 章向你介绍检查，并详细讲解检查的原理。

## 使用内置内容过滤器
第 10 章包含了一系列综合示例，帮助你立即上手。

#### 外部内容过滤器如何工作
外部内容过滤器将 SMTP 通信管理和内容控制委托给外部应用程序。要了解 Postfix 如何处理经过外部内容过滤器的消息，请阅读第 11 章。

## 使用外部内容过滤器
需要一些实施外部内容过滤器的示例吗？阅读第 12 章，找到你可以实际动手实践的示例。

# 6 邮件管理员的电子邮件入门

术语*信封*、*邮件头*、*正文*和*附件*都与 MTA 交换数据的某个部分相关。如果你知道它们的含义，你就能理解 Postfix 内容控制参数影响的消息的哪些部分。同样方便的是，Postfix 参数名称和语法源自 RFC。

本章是内容控制入门。请仔细阅读，并花一些时间理解术语和概念。在掌握基础知识后，你将能轻松实现高效的内容控制。

## 消息传输基础
消息传输涉及两个主要部分：处理传输的 SMTP 通信和被传输的数据（大多数人称之为“电子邮件”或“消息”）。用于描述消息传输的术语并非凭空发明；它们源自一个古老但知名且成熟的系统，在早期被称为“邮件”。

在处理常规邮政系统时，术语*信使*、*信封*、*邮件头*、*正文*和*附件*都有公认的含义。当指代电子邮件时，这些是技术术语。图 6-1 将常规信件与电子邮件进行比较，你可以识别出以下部分：

### 信使
在常规邮件中，信使被称为*邮递员*。在电子邮件中，信使是*客户端*。

### 信封
在电子邮件中，就像常规信件一样，信封作为一个包装，说明内容应如何投递。在信封上，你可以找到*发件人信封地址*和*收件人信封地址*。

### 邮件头
邮件头提供关于消息的元数据（信息）。就像在真实信件中一样，邮件头提供有关发件人（From: 头）、预期收件人（To:）、发送日期和时间（Date:）以及主题（Subject:）的信息。此外，电子邮件消息中的 Received: 邮件头告诉你消息的传输路径以及传输所花费的时间。

### 正文
电子邮件消息的正文包含实际内容，就像信件中一样。

### 附件
如果电子邮件消息中包含附件，这一事实将在正文中注明；就像在真实信件中一样。附件是可选的，可以有多种格式。

### 为什么你需要了解这些？
到目前为止，这可能听起来有点理论化；所有这些与运行 Postfix 有什么关系？首先，电子邮件消息中的信息通常比信件中的更多。你需要知道这些额外的部分是什么，以及这些部分出现在消息的哪个部分。此外，Postfix 有三组不同的内容控制参数组，直接与消息的不同部分相关：

## smtpd_*_restrictions
*smtpd_*_restrictions* 参数在消息传输过程中控制客户端连接和信封。

## *_checks
*_checks* 参数负责检查邮件头、正文和附件。

## 过滤器
Postfix 使用过滤器将任务委托给其他（外部）筛选应用程序。过滤器是通用的；它们可以控制消息的每个部分，从信封到附件。

## 邮件与电子邮件
| 邮件 | 电子邮件 |
| :--- | :--- |
| 邮递员 | 客户端 |
| “嗨，我有一封你的信。” | HELO client.example.com |
| **信封** | **信封** |
| 寄件人地址 | MAIL FROM:<sender@example.com> |
| | 250-OK |
| 收件人地址 | RCPT TO:<recipient@example.org> |
| | 250-OK |
| | DATA |
| | 354 End data with <CR><LF>.<CR><LF> |
| **信件** | **电子邮件** |
| 寄件人地址 | FROM: Sender <sender@example.com> |
| | TO: Recipient <recipient@example.org> |
| | Date: Sun, 11 Apr 2004 22:36:51 +0200 |
| | Subject: Mail and email |
| 收件人地址 | |
| | Date |
| 亲爱的收件人，随信附上您的新信用卡…… | 亲爱的收件人，随此邮件附上您的新证书。 |
| | |
| | --2o5SYaxWcQjTEyO |
| | Content-Type: application/zip |
| | Content-Description: Attachment |
| | Content-Disposition: attachment; filename="certificate.zip" |
| | Content-Transfer-Encoding: base64 |
| | |
| | UEsDBAoAAAAAAK61/S6eUZzNDAa3SY/VKgEAP0B9AFBcHRhy2htZW50I0pnQE5mMKWACutFoup1GczqWAAAFMAAADAgANAAAAABAAAAAAIETEAAAAAYXRvWmobVUdC50eHRVWAUJAA+fc3j9VeAAAEsFBgAAAAABAAEASQAAAoAA |
| | |
| | --2o5SYaxWcQjTEyO-- |

图 6-1：常规信件与电子邮件的比较

这些参数中的每一个都有大量的选项；如果你不知道消息的哪个部分触发了特定参数，你的内容控制将无法工作。

## 控制 SMTP 通信（信封）
SMTP 通信涉及两个组件：客户端（连接到提供 SMTP 服务的服务器的机器）和客户端传递的信封。使用你机器上的 telnet 程序连接到你的服务器，最容易看清这一点。

这是一个示例通信。首先通过命令行连接到邮件服务器的端口 25：

```
$ telnet mail.example.com 25
220 mail.example.com
```

服务器返回的 220 代码确认了服务器的主机名。现在，像这样向服务器介绍你自己：

```
HELO client.example.com
250 mail.example.com
```

你可以使用 HELO（用于 SMTP）或 EHLO（用于 ESMTP）命令执行握手，并将客户端主机名作为参数。如果命令成功，你应该会收到一个 250 返回码，后面跟着服务器的主机名。

现在发送一些邮件。MAIL 命令构建信封，从信封的发件人开始。如果服务器接受发件人，你会得到另一个 250 返回码：

```
MAIL FROM:<sender@example.com>
250 Ok
```

构建信封的下一步是使用 RCPT 命令指定信封收件人。你可以输入多个收件人：

```
RCPT TO:<recipient@example.com>
250 Ok
RCPT TO:<recipient_2@example.com>
250 Ok
```

> **注意** 请记住，信封发件人和信封收件人通常与邮件头中给出的发件人和收件人（你即将看到的 DATA 命令序列的一部分）不同。如果你混淆了各种发件人和收件人，你的内容控制可能会失败。

要发送实际的消息（包括所有额外的邮件头，如主题、收件人和日期），请使用 DATA 命令：

```
DATA
354 End data with <CR><LF>.<CR><LF>
Subject: message
...
This is the message
...
.
250 Ok: queued as 92933E1C66
QUIT
```

以下是您刚刚看到的内容概述，依据电子邮件 RFC 定义：

### 客户端

客户端是发送邮件的机器；Postfix 会记录主机名和 IP 地址，如果无法通过 DNS 查询确定主机名，则记录“unknown”。Postfix 从内核的 TCP/IP 协议栈获取客户端 IP 地址，并在 SMTP 通信发生前从 DNS 或 `/etc/hosts` 文件获取主机名。这使得 Postfix 能够在 SMTP 通信期间客户端 IP 地址与主机名不匹配时实施限制。

Postfix 始终在邮件日志中记录客户端 IP 地址和主机名（如果可用），并在最终邮件头中包含此信息。

### HELO/EHLO 语句

客户端必须向邮件服务器提供两类信息进行自我介绍：服务类型和主机名。

介绍语句的第一部分是客户端请求的服务类型。HELO 指定 RFC 821（ftp://ftp.rfc-editor.org/in-notes/rfc821.txt）定义的常规服务，而 EHLO 请求 RFC 2821（ftp://ftp.rfc-editor.org/in-notes/rfc2821.txt）定义的扩展服务。

服务类型之后是客户端身份。客户端应提交其完全限定主机名。

### 信封

信封必须包含至少两个不同的项目：恰好一个信封发件人和至少一个信封收件人。客户端通过先传输信封发件人，再传输信封收件人来发送信封。

如果存在多个信封收件人，客户端必须逐个提交，每个信封收件人另起一行，并在每次提交后等待服务器的响应。¹ 服务器负责允许向部分或所有收件人投递邮件。

#### 信封发件人

信封发件人是 Postfix 在出现错误（如延迟或退信通知）时回复的发送者。

#### 信封收件人

信封收件人指定邮件的预期收件人。一封邮件可以有多个信封收件人（例如，发送给邮件列表多个订阅者的邮件）。

邮件服务器至少需要一个信封收件人（否则它没有投递对象）。因此，客户端不能使用空的信封收件人（<>）。

> ¹ESMTP 命令流水线是此规则的例外。

> **注意** *当您想将邮件限制给特定收件人时，请勿查看“收件人”头中指定的收件人。邮件会发送到信封中定义的收件人，而不是邮件头中定义的收件人。*

前述列表中几乎所有数据都可能被伪造，因此 Postfix 通过 `smtpd_*_restrictions` 参数提供了限制伪造的方法，这些参数解决以下问题：

-   客户端来自哪里？
-   客户端伪装成谁？
-   客户端是否有特殊权限？
-   发件人是谁？
-   收件人是谁？

Postfix 还尝试回答以下更困难的问题：

-   客户端是否以适当的方式向 Postfix 提供信息？
-   客户端是否以适当的顺序提供信息？
-   客户端是否提供所有信息？
-   如果客户端未提供所有适当的信息，客户端是否会尝试发送邮件？
-   是否能够判断信息是否正确？
-   如果可能，客户端是否在说谎？

Postfix 可以通过检查邮件的信封和 SMTP 对话过程来获得这些问题的答案。当 Postfix 通过 SMTP 信封限制拒绝邮件时，它会在邮件接收之前拒绝。因此，Postfix 不会向发件人地址发送“无法投递”的通知。这仍然是客户端的责任。

> **注意** *如果 Postfix 基于 SMTP 信封限制拒绝邮件，由于 Postfix 已先于客户端采取行动，因此不必生成退信。这有助于节省系统资源，保持流量较低，并且在 Postfix 遭受大量垃圾邮件攻击时特别方便，因为如果这些邮件最初被接受进一步传输，可能需要生成数千封退信。*

您可以在第 7 章学习 Postfix 有哪些限制及其工作原理。第 8 章包含几个可在您自己的配置中使用的示例。

## 控制邮件内容

电子邮件邮件由头部和正文组成。正文还可以包含一个或多个附件，这些附件以文件形式或封装在主邮件中的另一个邮件形式存在。图 6-2 展示了带有附件的简单邮件的高层视图。

![](img/852c79f689feb77c5fde686b993808b1_89_0.png)

图 6-3 展示了以另一个邮件作为附件的邮件。

![](img/852c79f689feb77c5fde686b993808b1_89_1.png)

您可以通过使用纯文本查看器或编辑器查看邮件来识别这些部分。例如，这是一封带有文件附件的邮件：

```
Return-Path: <sender@example.com>
X-Original-To: recipient@example.com
Delivered-To: recipient@example.com
Received: by mail.example.com (Postfix)
        id 9F71443F50; Mon, 26 Apr 2004 01:32:59 +0200 (CEST)
Delivered-To: recipient@example.com
Received: by mail.example.com (Postfix, from userid 500)
        id 2F23043F4F; Mon, 26 Apr 2004 01:32:59 +0200 (CEST)
Date: Mon, 26 Apr 2004 01:32:58 +0200
From: Sender <sender@example.com>
To: Recipient <recipient@example.com>
Subject: Elements of email content
Message-ID: <20040425233258.GA22383@mail.example.com>
Mime-Version: 1.0
Content-Type: multipart/mixed; boundary="/9DWx/yDrRhgMJTb"
Content-Disposition: inline
User-Agent: Mutt/1.5.4i
```

```
--/9DWx/yDrRhgMJTb
Content-Type: text/plain; charset=us-ascii
Content-Disposition: inline
```

空行将邮件正文与头部隔开。MIME 编码的文本和 MIME 编码的附件可能出现在正文中。

您可以附加一个或多个文件，包括另一个电子邮件邮件。另一个邮件中的邮件包含其自己的头部和正文。因此，您可能会有嵌套的头部。

希望这有所帮助，

发件人

```
--/9DWx/yDrRhgMJTb
Content-Type: application/x-zip-compressed
Content-Disposition: attachment; filename="attachment.zip"
Content-Transfer-Encoding: base64

UEsDBAoAAAAAAIILmjBOMx1uCwAAAAsAAAAAAYXR0YW5obWVudC50ZXh0
C1BAQIUAoAAAAAAAILmjBOMx1uCwAAAAsAAAAAAAEIAC2gQAAABhdHRhY2ht
ZW50LnR4dFBLBQYAAAAAAQABAAwAAABwAAAAAAA=
```

--/9DWx/yDrRhgMJTb--

电子邮件的各个部分如下：

-   电子邮件头部
-   电子邮件正文开始
-   附件开始

Postfix 可以分别对每个部分（`header_checks`、`body_checks`、`mime_header_checks`）执行检查。为了有效检查它们，您需要知道邮件可能包含的必需、推荐和可选部分。

### 头部

头部携带关于邮件正文的元信息，例如字符编码和传输日期。RFC 2822（ftp://ftp.rfc-editor.org/in-notes/rfc2822.txt）将头部分为必需和推荐两类。

> **注意** *头部字段无需按任何特定顺序出现。不过，建议如果存在，按 Return-Path、Received、Date、From、Subject、Sender、To、Cc 等顺序发送头部。您可以在阅读电子邮件头部（http://www.stopspam.org/email/headers.html）中找到更多关于头部的信息。*

#### 必需头部

有两个必需的头部元素：

**Date**

日期字段通常指定邮件撰写和发送的日期和时间。如果发件人的客户端省略此头部，Postfix 会添加它。

**From**

此字段包含发送此邮件的人员的身份。如果发件人的客户端省略此头部，Postfix 会添加它。

#### 推荐头部

以下是推荐的头部元素：

**Message-Id**

此字段包含一个唯一标识符，指向当前邮件的当前版本。客户端生成消息 ID 并保证其唯一性。此外，消息 ID 旨在由机器阅读，对人类可能不一定有意义。因为消息 ID 对应于特定邮件的一个实例，任何后续修订的消息应获得新的消息 ID。

如果发件人的客户端省略此头部，Postfix 会添加它。



**收件人（To）**
此字段包含邮件主要收件人的标识。如果发件人的客户端省略了此头部，Postfix 会添加 `undisclosed_recipients_header` 配置参数的值。

**主题（Subject）**
此字段应包含对邮件的简要描述。

**抄送（Cc）**
此字段包含邮件所有次要收件人的标识。

**回复地址（Reply-To）**
此字段指示收件人的客户端应将回复发送至何处。

**内容类型（Content-type）**
此字段定义于 RFC 1049（ftp://ftp.rfc-editor.org/in-notes/rfc1049.txt），它指示邮件正文的结构。

**MIME 版本（MIME-Version）**
如果存在此头部字段，则表明邮件正文（据称）是按照 RFC 1521（ftp://ftp.rfc-editor.org/in-notes/rfc1521.txt）编写的。

**已接收（Received）**
每个处理消息的传输代理都会添加一行这样的头部，以指示消息到达的时间、地点和方式。这些字段中的信息对于追踪传输问题很有用。

**回退路径（Return-Path）**
此头部指示信封发件人，用于识别返回始发者的路径。邮件服务器在通过本地投递代理（如本地守护进程）投递时会插入此字段。

## **可选头部（X-Headers）**

*X-header* 是以大写字母 X 加连字符开头的扩展头部字段的通用术语。X-headers 被视为非标准的，仅用于提供信息；反之，任何非标准的信息性头部都应该是 X-header。

以下是一些示例 X-headers（当然还有数百万种）：

```
X-Mailer: Ximian Evolution 1.4.3
X-Priority: 3
X-Spam-Checker-Version: SpamAssassin 2.53 (1.174.2.15-2003-03-30-exp)
X-Original-To: recipient@example.com
```

## **正文（Body）**

正文承载消息内容，必须出现在头部部分之后。正文可以是纯文本或编码形式。正文还可以包含以某种编码形式的附件，使其在通过 Internet 传输时不会被损坏（在过去，许多 MTA 不支持八位清洁传输；去掉二进制文件的第八位会使其损坏）。

## **附件（Attachments）**

附件是转换为仅限文本表示（仅可打印字符）的文件，适合通过电子邮件发送。附件涉及多个环节，将在以下小节中进行说明。

## **MIME 编码**

MIME 代表多用途 Internet 邮件扩展，它是一个重新定义消息格式的系统，如 RFC 2045（http://www.rfc-editor.org/rfc/rfc2045.txt）中所述。二进制文件的两种常见 MIME 编码是 quoted-printable 和 base64：

### **quoted-printable**

quoted-printable 编码旨在表示主要由对应于 US-ASCII 字符集中可打印字符的八位字节组成的数据。它对数据进行编码，使生成的八位字节不太可能被邮件传输修改。

### **base64**

base64 是在 RFC 1421（ftp://ftp.rfc-editor.org/in-notes/rfc1421.txt）和 RFC 2045（ftp://ftp.rfc-editor.org/in-notes/rfc2045.txt）中定义的数据编码方案，用于将二进制编码的数据转换为可打印的 ASCII 字符。它本质上是一种用于 Internet 邮件的 MIME 内容传输编码，仅使用字母数字字符（A–Z、a–z、数字 0–9）以及"+"和"/"符号，以"="符号作为特殊后缀代码。用于手动编码和解码 base64 的命令行工具包括 mpack、munpack 和 uudeview。

所有较新的 MUA 都支持 MIME，附件通常只会以 base64 编码发送。

### **编码处理器**

MUA 负责执行编码二进制附件的任务，同时还会自动创建所需的 MIME 结构，以将邮件文本和编码后的附件嵌入到其他支持 MIME 的 MUA 可以理解的形式中。这种形式需要消息中包含以下头部：

#### **MIME-Version**

此头部的存在表明消息采用 MIME 格式。其值通常为 1.0，因此该头部通常如下所示：

```
MIME-Version: 1.0
```

#### **Content-type**

此头部指示消息内容的类型和子类型。以下是一个示例：

```
Content-type: text/plain
```

类型（本例中为 text）和子类型（plain）的组合通常称为 MIME 类型，因此本例中的 MIME 类型为 `text/plain`。

大量文件格式已注册了 MIME 类型。IANA 运营着一个存档，列出了已注册的类型（ftp://ftp.isi.edu/in-notes/iana/assignments/media-types）。此外，所有文本类型都有一个额外的可选 `charset` 参数，用于指示字符编码。大量字符编码已注册了 MIME charset 名称。

### **内容类型**

本节列出了一些你可能会遇到的 MIME 类型。此外，`multipart-mime-message` MIME 类型允许消息由排列为树状结构的多个不同部分组成，其中叶节点具有非多部分内容类型，而非叶节点可以是各种多部分类型之一。MIME 机制支持以下类型（以及其他类型）：

**text/plain**

简单文本消息使用 `text/plain`；它是 Content-type 头部的默认值。

**multipart/mixed**

此类型表示文本加附件（包含 `text/plain` 部分和其他非文本部分的 `multipart/mixed`）。带有附件的 MIME 消息通常通过 `Content-disposition` 头部指示文件的原始名称，因此文件类型既由 MIME 内容类型指示，也由（通常是操作系统特定的）文件扩展名指示。

病毒经常将自身作为文件发送，其中 `Content-type` 和 `Content-disposition` 头部指示不同的文件类型。

**message/rfc822**

这是带有原始消息附件的回复（包含 `text/plain` 部分和作为 `message/rfc822` 部分的原始消息的 `multipart/mixed`）。Postfix 以这种方式生成退信（`message/rfc822` 附件是被退回的原始消息）。

### **multipart/alternative**

此类型表示具有两种替代查看方式的内容，例如同时以纯文本和其他格式（如 HTML）发送的消息（以 `text/plain` 和 `text/html` 形式呈现的相同内容）。Outlook Express 默认使用此内容类型，因为它同时以 HTML 和纯文本形式发送邮件。

### **编码结构**

MIME 多部分消息包含一个边界字符串，在邮件的 Content-type 头部中标记为 `boundary`，此边界不应出现在任何部分中。相反，它应出现在各部分之间，以及消息正文的开头和结尾。以下示例说明了一个多部分消息的示例：

```
Return-Path: <sender@example.com>
X-Original-To: recipient@example.com
Delivered-To: recipient@example.com
Received: by mail.example.com (Postfix)
        id 9F71443F50; Mon, 26 Apr 2004 01:32:59 +0200 (CEST)
Delivered-To: root@example.com
Received: by mail.example.com (Postfix, from userid 500)
        id 2F23043F4F; Mon, 26 Apr 2004 01:32:59 +0200 (CEST)
Date: Mon, 26 Apr 2004 01:32:58 +0200
From: Sender <sender@example.com>
To: Recipient <recipient@example.com>
Subject: Elements of email content
Message-ID: <20040425233258.GA22383@mail.example.com>
Mime-Version: 1.0 ❶
Content-Type: multipart/mixed; boundary="/9DWx/yDrRhgMJTb" ❷
Content-Disposition: inline
User-Agent: Mutt/1.5.4i

--/9DWx/yDrRhgMJTb ❸
Content-Type: text/plain; charset=us-ascii ❹
Content-Disposition: inline
```

空行将消息正文与头部隔开。MIME 编码的文本和 MIME 编码的附件可以出现在正文中。

你可以附加一个或多个文件，包括另一封电子邮件消息。消息中的消息包含其自身的头部和正文。因此，你可能会有嵌套的头部。

此邮件仅供参考，

发件人

```
--/9DWx/yDrRhgmJTb ❸
Content-Type: application/x-zip-compressed ❺
Content-Disposition: attachment; filename="attachment.zip"
Content-Transfer-Encoding: base64 ❼

UEsDBAoAAAAAAILmjB0Mx1uCwAAAAsAAAAOAAAAYXR0YWNobWVudC50eHRhdHRhY2htZW50
C1BLAQIUAAoAAAAAAILmjB0Mx1uCwAAAAsAAAAAAAAAEAIAC2gAAAAAYXR0YWNobWVudC50eHRhdHRhY2ht
ZW50LnR4dFBLBQYAAAAAAQABAwAAAA03AAAAAAA=

--/9DWx/yDrRhgmJTb-- ❽
```

消息各部分说明如下：

- ❶ 这是 MIME 版本头部。
- ❷ 这是包含内容类型和用于分隔消息不同部分的边界字符串的头部。
- ❸ 边界字符串的首次出现。多部分消息的新部分从此处开始。
- ❹ 此部分是纯文本。
- ❺ 这是边界字符串的第二次出现，表示前一部分已完成，多部分消息的新部分从此处开始。
- ❻ 新部分是 Zip 格式的文件。
- ❼ Zip 文件以 base64 格式编码。
- ❽ 这是边界字符串的最终使用，表示部分和消息的结束。



# 7 消息传输限制的工作原理

> 要知道可以对什么进行限制，首先需要知道
> "什么"是什么，以及它应该是什么……
> ——Patrick，在试图理解 Ralf 解释限制时

本章解释限制的理论。限制允许你的邮件服务器通过检查客户端与服务器之间进行的 SMTP 通信来接受或拒绝传入消息。从该对话中获得的信息使 Postfix 能够对客户端、发件人和收件人施加或解除限制。

虽然"restrict"一词通常意味着你在限制某些东西，但在 Postfix 中，"restriction"一词也可以表示完全相反的意思；你可以配置限制来显式允许某些东西。

## 限制触发器

限制是强大的工具。要有效使用它们，你需要理解 SMTP 通信以及 Postfix 提供的分析此通信的功能。你已经在第 6 章中看到了 SMTP 通信是如何进行的。这里我们将从另一个角度来看待它；这次我们关注的是由客户端给出的命令所定义的 SMTP 通信阶段。图 7-1 概述了这些阶段。

*图 7-1：SMTP 通信阶段及典型的客户端输入*

图 7-1 中的每个新阶段都标志着 Postfix smtpd 守护进程了解到关于客户端及其想要传输的消息的另一条信息的时刻。Postfix 使用这些阶段来触发限制，每个阶段都有自己的限制参数，其命名遵循活动守护进程、阶段名称和用途。这就是限制触发器遵循此模板的原因：`smtpd_stagename_restrictions`。

以下是所有限制触发器及其默认行为的列表：

`smtpd_client_restrictions`
此触发器适用于客户端的 IP 地址或其主机名或两者。默认情况下，Postfix 允许任何客户端连接。

`smtpd_helo_restrictions`
此触发器适用于客户端的 HELO/EHLO 参数以及客户端的 IP 地址或主机名或两者。默认允许任何 HELO/EHLO 参数。

`smtpd_sender_restrictions`
这是第一个限制信封部分的触发器集。Postfix 将其应用于信封发件人、HELO/EHLO 参数和客户端。默认允许任何信封发件人发送消息。

`smtpd_recipient_restrictions`
此触发器适用于信封收件人、信封发件人、HELO/EHLO 参数以及客户端 IP 地址或主机名或两者。Postfix 中的默认设置是允许属于 mynetworks 配置参数的客户端的任何收件人，但否则仅允许 relay_domains 中的收件人域和 mydomains 中的收件人域。这可以防止 Postfix 成为开放中继。

`smtpd_data_restrictions`
此触发器检测在 Postfix 回复 DATA 命令之前发送邮件内容的客户端。Postfix 通过在客户端向服务器发送命令时跟踪 DATA 命令来实现这一点。默认没有限制。

`smtpd_etrn_restrictions`
此特殊触发器可以限制可能请求 Postfix 刷新邮件队列的客户端。默认允许任何客户端发出 ETRN 命令。

每个限制触发器对应一组限制；你可以将触发器视为空盒子。要从中获得任何用处，你需要在其中放入东西（限制）。

## 限制类型

Postfix 有几种可以归纳为四个不同组的限制：

-   通用限制
-   可切换限制
-   可自定义限制
-   额外的 UCE 控制参数

## 通用限制

第一组限制不检查 SMTP 对话中的任何内容；它们只是执行命令：

`permit`
允许请求。

`defer`
延迟请求。

`reject`
拒绝请求。

`warn_if_reject`
协助后续限制；如果 `warn_if_reject` 之后的限制决定拒绝请求，Postfix 实际上不会拒绝该消息，而是向日志打印 `reject_warning` 消息。

`reject_unauth_pipelining`
当客户端提前发送 SMTP 命令而不知道 Postfix 实际上支持 ESMTP 命令流水线时，拒绝该请求。这可以阻止不当使用 ESMTP 命令流水线来加速投递的批量邮件软件。

## 可切换限制

第二类限制的工作原理就像开关。你打开或关闭它们，一旦激活，它们就会检查是否满足某个条件。以下是一个不完整的列表：

`smtpd_helo_required`
此限制要求客户端在 SMTP 会话开始时发送 HELO（或 EHLO）命令。RFC 821 和 RFC 2821 都要求 HELO/EHLO。

`strict_rfc821_envelopes`
此限制调整 Postfix 对 MAIL FROM 或 RCPT TO 命令中给定地址错误的容忍度。不幸的是，广泛使用的 Sendmail 程序允许相当多的非标准行为，因此有很多软件期望能够侥幸通过。在此处严格可以阻止一些不需要的邮件，但也可能阻止来自编写不良客户端的合法邮件。

`disable_vrfy_command`
SMTP VRFY 命令允许客户端验证收件人是否存在。此限制允许你禁用 VRFY 命令。

`allow_percent_hack`
此限制控制将 user%domain 重写为 user@domain 的形式。

`swap_bangpath`
此限制控制将 site!user 重写为 user@site 的形式。如果你的机器连接到 UUCP 网络，这是必要的。

## 可自定义限制

可自定义限制是像过滤器一样工作的映射。在每个映射条目中，键是过滤器，值是过滤器匹配时采取的操作（有关有效操作的列表，请参阅"通用限制"部分）。以下是几种可自定义限制：

**HELO (EHLO) 主机名限制**
这些限制限制客户端可以使用 HELO 或 EHLO 命令发送的主机名。

**客户端主机名/地址限制**
这些限制限制可以建立与邮件服务器的 SMTP 连接的客户端。

**发件人地址限制**
这些限制限制 Postfix 接受用于 MAIL FROM 命令的发件人地址（信封发件人）。

**收件人地址限制**
这些限制限制 Postfix 接受用于 RCPT TO 命令的收件人地址（信封收件人）。

**ETRN 命令限制**
这些限制限制可以发出 ETRN 命令的客户端。

**头部过滤**
此过滤限制消息头部中允许的内容。模式应用于整个逻辑消息头部，即使逻辑头部跨越多行物理文本。

**正文过滤**
此过滤限制消息正文行中可能出现的文本。

**DNSBL 风格黑名单**
这些黑名单限制来自出现在 DNSBL 黑名单中的 IP 地址（客户端）的连接。

**RHSBL 风格黑名单**
这些黑名单禁止出现在 RHSBL 黑名单中的发件人域（作为信封发件人的一部分）。

## 额外的 UCE 控制参数

额外的 UCE 控制参数集支持其他不属于 Postfix 默认功能范围的限制或功能。以下是可用限制中的几个：

`default_rbl_reply`
创建默认回复模板，用于当 SMTP 客户端请求被 reject_rbl_client 或 reject_rhsbl_sender 限制阻止时使用。

`permit_mx_backup_networks`
将 permit_mx_backup 中继控制功能的使用限制为仅主 MX 主机匹配网络块列表的目的地。

`rbl_reply_maps`
指定按 DNSBL 域名索引的 DNSBL 回复模板的查找表。如果未找到模板，Postfix 将改用 default_rbl_reply 模板。

`relay_domains`
指示 Postfix 接受这些域的邮件，即使此服务器不是最终目的地。

`smtpd_sender_login_maps`
指定允许使用特定 MAIL FROM 地址（信封发件人）的用户。要使用此限制，Postfix 必须知道用户名，因此客户端必须使用 SMTP 认证来标识自己。



## 应用范围

正确使用限制的关键在于理解你可以在 SMTP 通信的哪个阶段应用它们。某些限制在特定阶段没有意义。表 7-1 按阶段列出了各项限制。

### 表 7-1：应用范围

| 阶段 | 限制 |
|---|---|
| 客户端（IP 地址和/或主机名） | check_client_access、reject_rbl_client、reject_rhsbl_client、reject_unknown_client |
| HELO/EHLO 主机名 | check_helo_access、permit_naked_ip_address、reject_invalid_hostname、reject_non_fqdn_hostname、reject_unknown_hostname |
| 信封发件人 | check_sender_access、reject_non_fqdn_sender、reject_rhsbl_sender、reject_unknown_sender_domain、reject_unverified_sender |
| 信封收件人 | check_recipient_access、permit_auth_destination、permit_mx_backup、reject_non_fqdn_recipient、reject_unauth_destination、reject_unknown_recipient_domain、reject_unverified_recipient |
| DATA | reject_unauth_pipelining |

## 构建限制

限制可能会变得相当复杂，如果不了解具体机制就随意调整，可能会以隐蔽（以及不那么隐蔽）的方式破坏你的邮件服务器。在构建限制时，请牢记以下规则：

- 笼统的写法会使你的限制失效。
- 评估的阶段会产生影响。
- 限制触发器中各条目的出现顺序很重要。先前的动作会影响后续限制的评估方式。

### 写法

如前所述，限制触发器就像空盒子。然而，填充它们并不意味着你只需把限制扔进去就万事大吉了。

```
restriction_trigger = conditional_restriction, customizable_restriction \
maptype:/path/to/the/map, general_restriction
```

由于单条限制很容易超出一行的合理宽度，你可以在续行的开头添加空白字符，这样 Postfix 就会将这些行识别为同一个参数设置。

此外，分隔各限制的逗号是可选的。因此，以下写法与上面的示例等效（而且更容易阅读）。

```
restriction_trigger =
    conditional_restriction
    customizable_restriction maptype:/path/to/the/map
    general_restriction
```

### 评估时机

一般来说，Postfix 不会在对应的 SMTP 通信步骤完成后立即评估和执行限制触发器中的限制。相反，Postfix 会等到客户端发送第一个信封收件人时才进行评估。之所以存在这种延迟，是因为某些邮件客户端在服务器拒绝其命令后，只要尚未发送完至少一个信封收件人，就会继续尝试提交邮件。

你可以通过将 smtpd_delay_reject 参数设置为 no 来覆盖此默认行为。

但是，即使可以追踪这些客户端并建立例外列表以确保它们不会被打断，最佳实践仍然是等待所有步骤完成后再使限制生效。这样不仅可以降低邮件系统的复杂性，还能收集更多关于邮件投递尝试的数据。

要了解 smtpd_delay_reject 如何影响限制的评估，请参阅图 7-2。

### 动作对限制评估的影响

正如"可自定义限制"一节中所描述的，可自定义限制使用映射表。当 Postfix 在限制映射表中查找某个键时，它会执行与该键对应的动作值。一个映射表可能如下所示：

| 键 | 动作 |
|---|---|
| 10.0.0.1 | PERMIT Private IP from VPN transfer tunnel |
| 172.16.0 | REJECT Private IP address cannot come from outside |
| 168.100.1.3 | DUNNO |
| 192.0.34.166 | OK |

![](img/852c79f689feb77c5fde686b993808b1_104_0.png)

*图 7-2：smtpd_delay_reject 对限制评估的影响*

上面的映射表包含四种可用于自定义限制的动作：PERMIT、REJECT、DUNNO 和 OK。这些值告诉 Postfix 如何处理客户端、发件人或收件人。虽然有多种动作（参见 access(5) 手册页），但以下是最常用的几种：

- **OK**
对客户端和邮件没有异议。Postfix 停止评估当前限制集中的限制，并转入下一组限制。

**PERMIT**
与 OK 等效。

**REJECT**
立即拒绝该邮件，忽略任何后续限制。该邮件最终被拒绝。

**DUNNO**
停止评估当前限制，但继续评估当前限制集中的下一个限制。

限制集中各条目的顺序很重要，因为第一个返回 OK 或 REJECT 的匹配项会立即终止当前限制集的评估（其中 REJECT 意味着客户端、发件人或收件人最终被拒绝）。Postfix 从上到下读取和应用限制，如果你写在一行中，则是从左到右。这就是为什么对于复杂的限制，使用多行写法更为方便。想象一下，如果这些限制全部写在一行中，阅读起来该有多费劲！

```
smtpd_recipient_restrictions =
    check_recipient_access hash:/etc/postfix/recipients_restrictions,
    permit_sasl_authenticated,
    permit_mynetworks,
    reject_unauth_destination,
    reject_unauth_pipelining,
    reject_rbl_client relays.ordb.org
    permit
```

图 7-3 展示了限制评估过程，并显示了每个动作值对应的行为。

## 拖慢不良客户端

任何在与 smtpd 通信时导致大量错误的客户端（例如，在限制中触发 REJECT 或导致参数语法错误），都会使 smtpd 在接受该会话中的后续命令前进行短暂暂停。这是一种防御失控客户端软件的手段。

你可以通过几个参数来调整这一行为。smtpd_error_sleep_time 参数指定每次错误后的暂停秒数（默认为一秒）。smtpd_soft_error_limit 参数起着一种"陷阱"机制的作用；当远程 SMTP 客户端犯了多个错误时，Postfix SMTP 服务器可以在响应之前插入额外的延迟。最后，你可以根据 smtpd_hard_error_limit 参数终止会话。

这三个参数的协同工作方式如下：

- 如果客户端导致错误，且当前 SMTP 会话中的错误总数低于 smtpd_soft_error_limit 的值，则每次错误会导致 smtpd_error_sleep_time 秒的延迟。
- 如果客户端导致错误，且 SMTP 会话中的错误总数超过 smtpd_soft_error_limit，则每次错误会导致超过 smtpd_soft_error_limit 部分的错误数（秒）的延迟。
- 如果客户端的错误数超过 smtpd_hard_error_limit，Postfix 将终止会话。

例如，假设你将参数配置如下：

```
smtpd_soft_error_limit = 5
smtpd_hard_error_limit = 10
smtpd_error_sleep_time = 1s
```

如果客户端在单次会话中导致 11 次错误，Postfix 将分别暂停 1、1、1、1、1、2、3、4、5 和 6 秒，在第 11 次错误时断开连接。

![](img/852c79f689feb77c5fde686b993808b1_106_0.png)

图 7-3：限制评估过程

## 限制类别

限制类别是一种特殊形式的限制触发器，它不是预定义的，也不绑定到 SMTP 通信的任何特定阶段。你可以根据需要自行定义，并通过在可自定义限制的映射表中引用它们来触发。

例如，假设你有一个用于检查信封发件人地址的可自定义限制映射表，当信封发件人匹配 example.com 时，你想触发另一组限制。在这种情况下，你需要将这组新限制放入一个名为 check_if_example.com_sender 的新类别中。首先，在 main.cf 文件中声明这个新类别。

```
smtpd_restriction_classes = 
    check_if_example.com_sender
```

现在，同样在 main.cf 中，为你的新类别添加一些限制：

```
check_if_example.com_sender = 
    check_sender_access hash:/etc/postfix/bounces
    check_sender_access hash:/etc/postfix/valid_example.com_senders
    check_sender_access regexp:/etc/postfix/nice_reject.regexp
```

如你所见，这些新限制检查的是信封发件人（尽管它们也可以是适合当前 SMTP 对话阶段的任何内容）。

不用担心这些限制中的映射表；你稍后会看到如何定义它们。不过我们还缺少一个重要的部分。如何激活 check_if_example.com_sender？

为此，你需要在 smtpd_*_restrictions 集中添加一个 check_sender_access 限制。假设你已经将该限制设置为以下映射表，该映射表接受来自 foo.com 的发件人并拒绝来自 bar.org 的发件人（有关有效动作，请参阅本章前面的"动作对限制评估的影响"一节）：

| 键 | 动作 |
|---|---|
| foo.com | OK |
| bar.org | REJECT |

要添加新的限制类别，请按如下方式扩展该映射表：

| 键 | 动作 |
|---|---|
| foo.com | OK |
| bar.org | REJECT |
| example.com | check_if_example.com_sender |

如你所见，使用限制类别的关键在于找到正确的插入位置，将其添加到可自定义限制的映射表中。



# 8 使用消息传递限制

> 垃圾邮件就是战争。RFC 不适用。
> —— 维特·维尼马

![](img/852c79f689feb77c5fde686b993808b1_109_0.png)

限制措施控制消息流，根据客户端在 SMTP 对话过程中传输的内容作出决策。限制措施可用的场景似乎不可胜数，因此本章不会列举所有限制措施及其可用选项，而是描述在 Postfix 邮件列表和日常使用中经常出现的场景。对于每个场景，我们将深入讨论相关的限制措施和选项，向你展示如何实施它们，并帮助你理解它们为何如此设计。

## 如何构建和测试限制措施

在开始修改默认限制之前，你应该清楚地知道要限制什么。当你只是开启或关闭布尔类型的限制时，这并不太难，但如果你想限制那些试图伪装来源的主机发送的邮件，事情可能会变得复杂一些。

Postfix 邮件列表上有一句常见的格言："日志是你的朋友。"把邮件日志想象成朋友似乎有些难以理解，但在收集限制邮件流所需的信息时，日志确实非常实用。简单来说，邮件日志包含了构建有效限制所需的大部分信息。来看看这条入站消息的一系列日志条目：

```
Apr 14 21:14:48 mail postfix/smtpd[31840]: 4F2A643F30: client=unknown[172.16.0.1]
Apr 14 21:14:48 mail postfix/cleanup[31842]: 4F2A643F30: message-id=<002101c42254$792c2530$010010ac@stateofmind.de>
Apr 14 21:14:48 mail postfix/nqmgr[31836]: 4F2A643F30: from=<test@example.com>, size=666, nrcpt=1 (queue active)
Apr 14 21:14:48 mail postfix/smtpd[31840]: disconnect from unknown[172.16.0.1]
Apr 14 21:14:48 mail postfix/smtpd[31844]: 4F2A643F30: to=<p@state-of-mind.de>, relay=mail.state-of-mind.de[212.14.92.89], delay=0, status=sent (250 Ok: queued as 97E70E1C65)
```

消息各部分的含义如下：

1. 投递消息的客户端（IP 地址和主机名）
2. Message-Id 头
3. 信封发件人（SMTP 对话中的 MAIL FROM 命令）
4. 收件人数量
5. 信封收件人（SMTP 对话中的 RCPT TO 命令）
6. 消息发送的目的地
7. 远端 Postfix 服务器为该消息分配的队列 ID

如果你的工作是限制消息的传输，并且需要更多信息来了解你面对的情况，日志就是了解你的"对手"的最佳途径。

## 模拟限制措施的影响

一套好的限制措施很少能一次就达到效果。为了获得你需要的结果，通常需要经过多次反复试验。要测试你的限制措施，你需要一些消息来运行测试，而你很可能没有专门的测试机器，只能在生产服务器上开发限制措施。不幸的是，这存在误报和丢失重要邮件的风险。

为了解决这个问题，Postfix 提供了一个用于测试限制措施的 `warn_if_reject` 参数，它类似于检查中的 WARN 操作。通过将此参数添加到你想测试的限制措施前面，Postfix 只会记录限制措施的效果，但不会拒绝邮件。以下是用它来测试 `reject_unknown_sender_domain` 的示例：

```
smtpd_recipient_restrictions =
    permit_mynetworks
    reject_unauth_destination
    warn_if_reject reject_unknown_sender_domain
    permit
```

一旦设置了这个参数，邮件日志就会这样报告"模拟"的拒绝：

```
Jun 25 16:10:52 mail postfix/smtpd[32511]: 8075015C02F: reject_warning: RCPT from sccrmhc11.comcast.net[204.127.202.55]: 550 <DickinsL@newfaces.gr>: Sender address rejected: Domain not found; from=<DickinsL@newfaces.gr> to=<example@charite.de> proto=ESMTP helo=<sccrmhc11.attbi.com>
```

确认限制措施正常工作后，你可以从限制中移除 `warn_if_reject` 参数。后续的日志条目将通过记录被拒绝的消息来通知你限制措施已生效：

```
Jun 25 16:11:23 mail postfix/smtpd[32511]: 8075015C02F: reject: RCPT from sccrmhc11.comcast.net[204.127.202.55]: 550 <DickinsL@newfaces.gr>: Sender address rejected: Domain not found; from=<DickinsL@newfaces.gr> to=<recipient@example.com> proto=ESMTP helo=<sccrmhc11.attbi.com>
```

## 使限制措施立即生效

Postfix 由多个不同的守护进程组成，它们在启动时加载配置数据。其中一些守护进程只运行很短的时间就会终止，以避免过多的资源占用。然而，其他守护进程*不会*自动重启，除非你要求 Postfix 这样做。

这些长期运行的守护进程——`qmgr` 和 `nqmgr`（`nqmgr` 只在旧版本中这样命名，新版本的 Postfix 默认使用新的队列管理器，但在这种情况下它被命名为 `qmgr`——旧的队列管理器则被命名为 `oqmgr`），在限制邮件流方面扮演着重要角色，在整个系统重启或你手动干预之前，它们*不会*注意到配置的更改。因此，你需要记住，每当更改 `main.cf` 或 `master.cf` 时，必须执行 **postfix reload** 命令来让队列管理器重新加载配置。

> **注意** *理论上，更改会随时间逐渐生效，因为守护进程在 `max_use` 次使用后会终止并重新启动。当然，`qmgr` 例外，它永远不会终止。`qmgr` 的选项更改始终需要执行 `postfix reload`。然而，让更改随时间逐渐生效可能导致一些守护进程使用旧配置，而另一些使用新配置，这可能并不理想。*

## 限制措施默认值

Postfix 附带了一套安全的默认限制措施，防止你的机器成为开放式中继（或第三方邮件中继）。你可以通过让 `postconf` 打印 `smtpd_recipient_restrictions` 的默认设置来查看默认限制：

```
# postconf -d smtpd_recipient_restrictions
smtpd_recipient_restrictions = permit_mynetworks, reject_unauth_destination
```

Postfix 按照列出的顺序评估限制措施。在这种情况下，如果客户端想要中继消息，Postfix 会检查连接是否来自 `mynetworks` 内的主机。如果是（即 `permit_mynetworks` 的评估结果返回 0OK），Postfix 接受该消息进行投递。

如果客户端不在 `mynetworks` 中，Postfix 会评估 `reject_unauth_destination`。此限制通过检查消息收件人是否在你为 Postfix 配置的最终目的地和中继域内来阻止中继尝试。如果收件人不在这些域内，`reject_unauth_destination` 返回 REJECT，Postfix 告诉客户端不允许中继。

如果 Postfix 认为该消息目的地由自己负责，`reject_unauth_destination` 返回 0K，Postfix 会评估下一条限制。然而，列表中没有更多限制，因此 Postfix 采用隐含的默认值 permit 并接受该消息。

这两条限制是保护你的服务器不成为开放式中继的基础，但它们并不能保护你的用户免受垃圾邮件的侵扰，也无法要求连接到你的服务器的客户端遵守规范。本章剩余部分将向你如何让限制措施更加严格。

## 要求符合 RFC 规范

要求本地和远程客户端遵守规范（符合 RFC）是严格管理的第一步。这不仅能确保你的邮件服务器向其他邮件服务器传递有效消息，还要求远程客户端规范行为。这对于防御垃圾邮件发送者非常有用，因为他们总是急匆匆的、绕过规则并伪装身份信息。

本节向你展示如何对主机名、信封发件人和信封收件人施加限制以实现 RFC 合规。

> **注意** *你在本节看到的限制措施在 main.cf 中不会按照它们被讲解的顺序使用。这是有意为之，你将在本章后面的"RFC 限制的处理顺序"一节中了解原因。目前，只需按照示例中的顺序添加限制措施即可。*



# 限制 HELO/EHLO 中的主机名

一个很好的起点是要求 Postfix 坚持让客户端在希望通过您的服务器发送或中继邮件时正确自我介绍。您可以对 SMTP 对话中的 HELO/EHLO 部分实施多种限制，从简单地要求客户端发送主机名，到要求他们发送有效的主机名。

### 要求主机名

Postfix 的 `smtpd_helo_required` 参数要求所有客户端在开始 SMTP 通信时必须发出 HELO 或 EHLO 语句。RFC 821 (ftp://ftp.rfc-editor.org/in-notes/rfc821.txt) 和 RFC 2821 (ftp://ftp.rfc-editor.org/in-notes/rfc2821.txt) 都强制要求此握手过程，但 Postfix 默认将此参数设置为否。您可以通过在 `main.cf` 文件中添加以下行来启用它：

```
smtpd_helo_required = yes
```

配置重新加载后，Postfix 将拒绝来自任何未正确自我介绍的客户端的消息。您可以通过连接到服务器并尝试在不发送 HELO 语句的情况下发起邮件传输来测试这一点。以下是 Postfix 在要求主机名时应有的交互过程：

```
$ telnet mail.example.com 25
220 mail.example.com ESMTP Postfix
MAIL FROM: <sender@example.com>
503 Error: send HELO/EHLO first
QUIT
221 Bye
```

### 要求完全限定域名 (FQDN)

HELO/EHLO 语句虽然不错，但也要求客户端在握手中提交其完整的主机名（例如，HELO client.example.com）。此外，RFC 要求主机名必须是完全限定域名（FQDN）。

> **注意** 一个 FQDN 不一定在域名服务 (DNS) 记录中实际存在。

如果您在 `smtpd_recipient_restrictions` 中设置 `reject_non_fqdn_hostname` 选项，Postfix 将拒绝来自任何未提交 FQDN 主机名的客户端的消息。

> **注意** 请小心使用此限制。一些邮件客户端，例如 Microsoft Outlook，默认只使用名称的本地部分（例如 `client`），除非您配置操作系统为其应用程序提供 FQDN 主机名。

当您将 `reject_non_fqdn_hostname` 添加到 `smtpd_recipient_restrictions` 列表中时，您的 `main.cf` 文件应如下所示：

```
smtpd_recipient_restrictions =
    permit_mynetworks
    reject_unauth_destination
    reject_non_fqdn_hostname
    permit
```

通过连接到邮件服务器并发出一个简单的主机名来测试此限制，例如：

```
$ telnet mail.example.com 25
220 mail.example.com ESMTP Postfix
HELO client
250 mail.example.com
MAIL FROM: <sender@example.com>
250 Ok
RCPT TO: <recipient@example.com>
504 <client>: Helo command rejected: need fully-qualified hostname
QUIT
221 Bye
```

# 拒绝主机名中的无效字符

RFC 规定，随 HELO/EHLO 语句发送的主机名不仅应是 FQDN，而且用于构建主机名的字符也必须遵守域名系统的要求。一个有效的域名必须至少包含以下元素：

- 一个顶级域 (TLD)，例如 “com”
- 一个域名，例如 “example”
- 一个分隔顶级域和域名的点 (.)

任何其他主机名都不太可能正确解析，这将使客户端与服务器之间的交互变得困难，甚至不可能。您可以通过在 `smtpd_recipient_restrictions` 中使用 `reject_invalid_hostname` 选项来告诉 Postfix 不与此类客户端通信。以下是您可能放置此选项位置的示例：

```
smtpd_recipient_restrictions =
    permit_mynetworks
    reject_unauth_destination
    reject_non_fqdn_hostname
    reject_invalid_hostname
    permit
```

像之前一样，通过从远程主机连接到邮件服务器并发出无效的主机名来测试此限制。在以下示例会话中，客户端自我介绍为 “.”

```
$ telnet mail.example.com 25
220 mail.example.com ESMTP Postfix
HELO .
250-mail.example.com
MAIL FROM:<sender@example.com>
250 Ok
RCPT TO:<recipient@example.com>
501 <.>: Helo command rejected: Invalid name
QUIT
221 Bye
```

# 限制信封发件人

信封发件人的域名部分也必须包含一个 FQDN，并且该域名必须存在。像 `sender` 和 `sender@example` 这样的信封发件人不包含 FQDN 域名部分。一个完整的信封发件人示例是 `sender@example.com`。无效的地址可能会造成很大混淆，因为邮件的发件人地址看起来像是源自该服务器。有两种情况可能会出错：

- 一个需要向不完整信封发件人退信的 MTA 会将退信发送给本地用户。退信将无法到达原始发件人。
- Postfix 可能会尝试“修复”无效地址，从而造成更糟糕的情况。因为 Postfix 知道信封发件人必须是 FQDN，它会运行 `trivial-rewrite` 守护进程，通过向 `sender` 添加 `$myorigin`（结果为 `sender@$myorigin`）以及向 `sender@example` 添加 `$mydomain`（结果为 `sender@example.$mydomain`）来规范化这些电子邮件地址。因此，来自远程服务器的消息的信封发件人将是完全错误的。

为了防止这种情况，将 `reject_non_fqdn_sender` 选项添加到 `smtpd_recipient_restrictions` 中，如下例所示：

```
smtpd_recipient_restrictions =
    reject_non_fqdn_sender
    permit_mynetworks
    reject_unauth_destination
    reject_non_fqdn_hostname
    reject_invalid_hostname
    permit
```

通过从远程机器连接到邮件服务器并发出不正确的信封发件人来测试此限制。此示例展示了该限制如何使 Postfix 拒绝来自此类发件人的消息：

```
$ telnet mail.example.com 25
220 mail.example.com ESMTP Postfix
HELO client.example.com
250 mail.example.com
MAIL FROM: <sender>
250 Ok
RCPT TO: <recipient@example.com>
504 <sender>: Sender address rejected: need fully-qualified address
```

# 接收来自不存在域的邮件

一个负责任的邮件服务器不会接受来自不存在发件人域的消息，因为如果投递失败，它无法联系到该不存在域中的发件人。其他配置会在 MTA 尝试通知发件人时立即导致双重退信，而带有不存在发件人域的消息最终会进入 postmaster 的邮箱。

> **注意** 邮件服务器必须处理不存在的域，因为用户在配置邮件客户端时有时会错误输入其邮件地址；垃圾邮件发送者也使用不存在的域来隐藏其来源。

为了保护收件人和管理员免受双重退信和格式错误的消息的影响，请将 `reject_unknown_sender_domain` 选项添加到您的 `smtpd_recipient_restrictions` 配置中。例如，您可以这样放置它：

```
smtpd_recipient_restrictions =
    reject_unknown_sender_domain
    permit_mynetworks
    reject_unauth_destination
    reject_non_fqdn_hostname
    reject_invalid_hostname
    permit
```

以下示例展示了如何测试此限制（您要寻找的是 Postfix 作为对 `MAIL FROM` 命令响应发送的 450 错误代码）：

```
$ telnet mail.example.com 25
220 mail.example.com ESMTP Postfix
HELO client.example.com
250 mail.example.com
MAIL FROM: <sender@domain.invalid>
250 Ok
RCPT TO: <recipient@example.com>
450 <sender@domain.invalid>: Sender address rejected: Domain not found
```

# 限制信封收件人

作为强制传入连接遵守 RFC 的最后一步，您可以拒绝任何在信封收件人中包含不存在域或用户的消息。

邮件服务器不应接受任何发送给不存在域的消息，因为无法投递此类消息。如果邮件服务器接受了消息然后将其退信，用户可能会认为邮件服务器有问题，因为它最初接受了该消息。

配置您的邮件服务器拒绝发送给不存在域的消息，可以将问题送回其起源——客户端或用户。要在 Postfix 中设置此功能，请在您的 `smtpd_recipient_restrictions` 集合中使用 `reject_unknown_recipient_domain` 选项，如下所示：

```
smtpd_recipient_restrictions =
    reject_unknown_recipient_domain
    permit_mynetworks
    reject_unauth_destination
    reject_non_fqdn_hostname
    reject_invalid_hostname
    permit
```

像往常一样，您可以通过在手动连接到服务器时发送一个不存在的收件人域来进行测试。以下是 Postfix 拒绝消息的示例，因为 `invalid.domain` 不是一个有效的域名：

```
$ telnet mail.example.com 25
220 mail.example.com ESMTP Postfix
HELO client.example.com
250 mail.example.com
MAIL FROM: <sender@example.com>
250 Ok
RCPT TO: <recipient@domain.invalid>
450 <recipient@domain.invalid>: Recipient address rejected: Domain not found
```

# 接收给未知收件人的邮件

您可以配置 Postfix 将您域中未知用户的消息投递给 postmaster。乍一看，这似乎是个好主意，因为 postmaster 可以检查并尽可能手动投递这些消息。

虽然理论上这构成了优秀的客户服务，但设置默认投递目标可能会导致您的邮件服务器成为垃圾邮件发送者或蠕虫的 *字典攻击* 目标后立即遭受拒绝服务 (DoS) 攻击。在此类攻击中，攻击者试图通过向使用所有可能字母组合的地址发送消息来向存在的收件人投递消息。例如，攻击者可以从 `aa@yourdomain.com` 开始，然后尝试 `ab@yourdomain.com`，并遍历所有两字母组合直到 `zz@yourdomain.com`。

不仅很难从这种攻击造成的混乱中筛选出有效的消息，而且服务器还面临着消耗过多带宽、CPU 时间、内存和磁盘空间的风险，直到您的服务器最终崩溃并停止处理消息传输请求。例如，Sobig.F 病毒在 2003 年 8 月使许多邮件服务器过载。



## 维护 Postfix 收件人验证

请记住，Postfix 会尽力提供最可靠的服务。可靠性意味着一致性，这就是为什么它默认会拒绝发送给未知用户的邮件，而无需任何手动干预。这对于独立的 Postfix 安装非常适用，对于运行在智能主机上保护其他邮件服务器的 Postfix 服务器也同样有用。

Postfix 通过查询映射表来确定收件人的有效性。有两个配置参数用于告知 Postfix 在何处查找这些信息：`local_recipient_maps` 和 `relay_recipient_maps`。这两个参数都期望一个或多个包含有效收件人的映射表。`local_recipient_maps` 参数定义有效的本地收件人，如以下示例所示，该示例在 Unix 密码文件和别名映射表中定义了收件人：

```
# postconf -d local_recipient_maps
local_recipient_maps = proxy:unix:passwd.byname $alias_maps
```

另一方面，`relay_recipient_maps` 定义了 Postfix 将消息中继到最终目标（如邮箱服务器）时的收件人：

```
# postconf -d relay_recipient_maps
relay_recipient_maps = hash:/etc/postfix/relay_recipients
```

使用 `relay_recipient_maps` 时，请特别注意确保 Postfix 知道其中继目标的所有有效收件人。如果目标恰好是 Microsoft Exchange 服务器，请参阅第 13 章了解如何提取用户映射表。

> **注意**
> 使用 `luser_relay` 会禁用 `local_recipient_maps` 参数，因为它使所有本地收件人都有效。同样，`virtual_alias_maps` 条目中的通配符捕获条目会禁用对不存在收件人的邮件拒绝，因为通配符使所有收件人都有效。例如，以下映射条目使 `example.com` 中的所有收件人都有效：
>
> @example.com		catchall@localhost

## 发送给不完整收件人名称的邮件

未完全限定的地址，例如 `recipient`，只包含电子邮件地址的本地部分。在接收单一域名邮件的机器上接受这些地址作为本地收件人是可以的，但一旦你的邮件服务器接收来自另一个域名的消息，这就会成为大问题。

这是因为本地部分单独存在时留下了过多的解释空间。

假设你同时为 `example.com` 和 `example.net` 这两个相互竞争的业务提供 ISP 服务。如果你收到一封发送给 `sales` 的消息，它应该发送到哪里？如果两者的电子邮件服务都托管在同一台机器上，应该发送给 `sales@example.com` 还是 `sales@example.net`？

这就是你应该拒绝未完全限定地址的原因。不要为与你无关的事情承担责任。发件人的职责是为消息的正确传输做好准备，这意味着要指定唯一的收件人。

> **注意** *只有一个例外：你必须接受以非 FQDN 形式发送给 postmaster 的邮件。*

当你将 `reject_non_fqdn_recipient` 选项添加到 `smtpd_recipient_restrictions` 参数后，Postfix 会立即拒绝发送给非 FQDN 收件人的消息，如以下示例所示：

```
smtpd_recipient_restrictions =
    reject_non_fqdn_recipient
    reject_unknown_recipient_domain
    permit_mynetworks
    reject_unauth_destination
    reject_non_fqdn_hostname
    reject_invalid_hostname
    permit
```

你可以从远程主机连接到你的邮件服务器并提供不完整的信封收件人来进行测试。以下会话应足以验证该限制是否生效：

```
$ telnet mail.example.com 25
220 mail.example.com ESMTP Postfix
HELO client.example.com
250 mail.example.com
MAIL FROM: <sender@example.com>
250 Ok
RCPT To: <recipient>
504 <recipient>: Recipient address rejected: need fully-qualified address
```

## 遵守 RFC 标准

你可能在本章中已经注意到，限制规则可能会变得相当复杂。限制规则的弊端在于，它们越复杂，你就越有可能指定一条导致邮件系统故障（甚至完全无法使用）的规则，因为它会拒绝那些在任何情况下都必须接受的内容。以下各节将向你展示如何避免无意中将部分或所有发件人拒之门外。这一点很重要，因为你可能会意外地排除那些能够告诉你配置存在问题的发件人。

### 空信封发件人

首先，永远不要屏蔽空信封发件人（<>）。这个地址属于 MAILER-DAEMON，邮件服务器在发送退信和状态通知时会使用它。如果你屏蔽了它，远程服务器就无法通知你的用户他们发送的消息是否出了问题。

> **注意** 黑名单（如 *dsn.rfc-ignorant.org*）会列出那些一概屏蔽空信封发件人的邮件服务器，因此使用这些黑名单的邮件服务器不会接受来自此类服务器的邮件。（这将在后面的"拒绝被列入黑名单的发件人域名"一节中讨论）。

你只需将空信封发件人视为任何其他有效收件人，并建立良好的（反垃圾邮件）限制规则来保护你的收件人。让限制规则发挥作用，如果收到带有空信封发件人的消息，就接受它。毕竟，任何发件人地址都可能是伪造的……

### 特殊角色账户

在邮件服务器上，你必须始终接受两个地址的消息；它们是运行符合 RFC 标准的邮件服务器所必需的：

#### postmaster

始终接受发送给 postmaster 的邮件；它是处理邮件相关问题的中心枢纽。用户在需要邮件帮助时必须能够联系 postmaster（参见 RFC 2821，网址为 http://www.rfc-editor.org/rfc/rfc2821.txt）。

#### abuse

接受发送给 abuse 的邮件可以确保用户能够告知你可能源自你的邮件服务器的邮件滥用行为（参见 RFC 2142，网址为 http://www.rfc-editor.org/rfc/rfc2142.txt）。

此外，如果你运行某些服务器，还应该接受发送给以下地址的消息（参见 RFC 2142；http://www.rfc-editor.org/rfc/rfc2142.txt）：

#### webmaster

如果你运行 Web 服务器，请接受发送给 webmaster 的邮件。

#### hostmaster

如果你运行域名服务器，请接受发送给 hostmaster 的邮件。

你可以通过使用 `check_recipient_access` 参数配合一个映射表（如 `/etc/postfix/roleaccount_exceptions`）来接受发送给这些收件人的消息，该映射表列出了应接受消息的收件人。该映射表可能如下所示（每个映射键的 OK 值告诉 Postfix，无论收件人限制规则如何，都可以接受该收件人的消息）：

```
# addresses that you must always accept
postmaster@	OK
abuse@		OK
# addresses that you should accept if you run DNS and WWW servers
hostmaster@     OK
webmaster@      OK
```

设置好此文件后，使用 `postmap hash:/etc/postfix/roleaccount_exceptions` 命令将其转换为映射表。然后，在 `main.cf` 的限制规则列表中，将该映射表指定为 `check_recipient_access` 设置的参数。以下是示例设置：

```
smtpd_recipient_restrictions =
    reject_non_fqdn_recipient
    reject_non_fqdn_sender
    reject_unknown_sender_domain
    reject_unknown_recipient_domain
    check_recipient_access hash:/etc/postfix/roleaccount_exceptions
    permit_mynetworks
    reject_unauth_destination
    permit
```

重新加载 Postfix 后，你就可以安全地继续构建更复杂的规则了。包含例外情况的映射表是在 Postfix 检查未授权中继之后被查询的；因此指定 `postmaster@` 是安全的。

## RFC 限制的处理顺序

你可能已经注意到，前面各节中添加到 `smtpd_recipient_restrictions` 的选项并非按照各节本身的顺序指定。这是因为如果限制选项的顺序不当，它们可能会相互干扰。请看以下列表：

```
smtpd_recipient_restrictions =
    reject_non_fqdn_recipient
    reject_non_fqdn_sender
    reject_unknown_sender_domain
    reject_unknown_recipient_domain
    permit_mynetworks
    reject_unauth_destination
    check_recipient_access hash:/etc/postfix/roleaccount_exceptions
    reject_multi_recipient_bounce
    reject_non_fqdn_hostname
    reject_invalid_hostname
    permit
```

`permit_mynetworks` 选项标志着内部网络客户端和外部客户端之间的重要分界线。出现在此选项之前（包括此选项）的选项适用于内部和外部客户端，而 `permit_mynetworks` 之后的选项仅适用于外部客户端。



在`permit_mynetworks`之前的选项要求所有客户端——无论其位于网络内部还是外部——都必须符合基本的 RFC 规范。

`reject_unauth_destination`选项可防止你的服务器成为开放中继。最好不要在指定`permit_mynetworks`之前指定任何允许消息通过的选项。之后，最好尽快跟进`reject_unauth_destination`，以确保未经授权的主机无法将你的服务器用作开放中继。

SMTP AUTH 检查应放在`reject_unauth_destination`和`permit_mynetworks`之间。然后，在指定更多拒绝选项之前，使用`check_recipient_access`来启用对系统上特殊角色邮箱的无条件投递。

最后，在拒绝了可能的多收件人垃圾邮件反弹尝试和伪造的信封收件人主机名之后，你可以使用`permit`选项接受消息。

## 反垃圾邮件措施

垃圾邮件发送者需要伪装其消息的来源，除非他们想被起诉。通常他们会伪造信封发件人，或者试图通过声称其客户端值得信赖——属于本地网络——来麻痹接收服务器。限制规则可以检查并拒绝此类消息。此外，还可以查询黑名单，其中列出了垃圾邮件发送者以及其他你不希望接收其消息的实体。以下部分将向你如何实施此类限制。

### 防止明显的伪造

一些垃圾邮件软件试图通过在 HELO/EHLO 问候中使用你的邮件服务器主机名作为其自身的主机名来伪装消息来源。对于 Postfix 来说，这似乎自相矛盾，因为唯一允许使用服务器主机名的主机就是服务器本身。然而，除非配置不当且邮件循环被创建，否则 Postfix 永远不会连接到其自身的`smtpd`守护进程来给自己发送邮件。

将这些限制添加在`permit_mynetworks`之后，将使它们仅适用于外部客户端，而不适用于代理过滤器或 SMTP 实现不完整的本地客户端。

因此，你可以安全地拒绝与任何以邮件服务器主机名作为 HELO 问候的客户端进行 SMTP 通信。为此，首先创建一个名为`/etc/postfix/helo_checks`的映射文件，其中包含你的主机名的变体。以下是一些示例，涵盖了主机名、主机的 IP 地址以及邮件服务器外部客户端不应使用的带方括号的 IP 地址：

```
/^mail\.example\.com$/       550 Don't use my hostname
/^192\.0\.34\.166$/           550 Don't use my IP address
/^\[192\.0\.34\.166\]$/      550 Don't use my IP address
```

根据 RFC 2821，单独的 IP 地址不是 HELO 握手请求的有效参数。IP 地址是被允许的，只要它被指定为 [ipv4address]（用方括号括起来）或 IPv6 地址 [ipv6:ipv6address]，同样用方括号括起来。为了严格执行并拒绝任何发送不带方括号的 IP 地址的客户端，添加以下行：

```
/^[0-9.]+$/                  550 Your client is not RFC 2821 compliant
```

要使该映射生效，请在`smtpd_recipient_restrictions`参数中将它（及其类型）指定为`check_helo_access`选项的参数。示例如下：

```
smtpd_recipient_restrictions =
    reject_non_fqdn_recipient
    reject_non_fqdn_sender
    reject_unknown_sender_domain
    reject_unknown_recipient_domain
    permit_mynetworks
    reject_unauth_destination
    reject_invalid_hostname
    check_recipient_access hash:/etc/postfix/roleaccount_exceptions
    reject_non_fqdn_hostname
    reject_invalid_hostname
    check_helo_access pcre:/etc/postfix/helo_checks
    permit
```

要测试此配置，请连接到你的邮件服务器并在 HELO 问候中发出你自己的名称。你应该会收到拒绝消息，如以下示例会话所示：

```
$ telnet mail.example.com 25
220 mail.example.com ESMTP Postfix
HELO mail.example.com
250 mail.example.com
MAIL FROM: <sender@example.com>
250 Ok
RCPT TO: <recipient@example.com>
550 <mail.example.com>: Helo command rejected: Don't use my hostname
QUIT
221 Bye
```

#### 伪造的名称服务器记录

如果有证据表明 HELO 域名、发件人域名和收件人域名的名称服务器记录是伪造的或不允许正确的消息传输，Postfix 可以拒绝消息。以下是你可能在 DNS 记录中看到的一些可疑情况：

##### 伪造的网络

一些邮件服务器声称来自 Postfix 无法到达的网络，包括你不使用的私有 IP 网络（参见 RFC 1918，ftp://ftp.rfc-editor.org/in-notes/rfc1918.txt）、回环网络、广播地址和多播网络。

##### 垃圾邮件巢穴

垃圾邮件巢穴是已知由垃圾邮件发送者拥有或为垃圾邮件发送者提供服务的网络。可以拒绝来自此类域名的所有消息。你可以在 ROKSO（已知垃圾邮件操作注册表，http://www.spamhaus.org/rokso/index.lasso）上查询垃圾邮件巢穴或垃圾邮件操作。

##### 通配符 MTA

通配符 MTA 声称负责任何域名，甚至是不存在的域名。通常，这不会是个问题，因为你可以拒绝涉及未知发件人和收件人域名的访问。不幸的是，一些域名注册机构想出了一个"好主意"，将未知域名重定向到他们自己的域名。这为未知域名提供了有效的 A 记录，从而使`reject_unknown_sender_domain`和`reject_unknown_recipient_domain`限制选项失效。

> 第一个重定向未知域名的域名注册机构是 VeriSign（http://www.verisign.com），时间是 2003 年。VeriSign 滥用了其对 .net 和 .com 命名空间的控制权，将所有不存在的 .com 和 .net 域名重定向到其自身站点（sitefinder.verisign.com）。此外，VeriSign 为未知域名建立了自己的邮件服务，这使得拒绝来自未知域名的消息变得不可能。这是对垃圾邮件发送者的公开邀请，你可以通过阻止通配符域名中的 MX 主机来拒绝来自通配符 MTA 的消息。

以上所有设置要么提供伪造的名称服务器记录，要么支持垃圾邮件发送者。要拒绝来自此类域名和网络的邮件，你可以创建一个名为`/etc/postfix/bogus_mx`的映射文件，其中包含名称服务器记录中的 IP 地址以及你希望给出的响应类型（完整响应列表请参见附录 C）。以下是映射文件示例：

```
# bogus networks
0.0.0.0/8        550 Mail server in broadcast network
10.0.0.0/8       550 No route to your RFC 1918 network
127.0.0.0/8      550 Mail server in loopback network
255.0.0.0/4      550 Mail server in class D multicast network
192.168.0.0/16   550 No route to your RFC 1918 network
# spam havens
69.6.0.0/18      550 REJECT Listed on Register Of Known Spam Operations
# wild-card MTA
64.94.110.11/32  550 REJECT VeriSign Domain wildcard
```

¹ 编写本书时，此网络在 spamhaus.org（http://www.spamhaus.org/sbl/sbl.lasso?query=SBL6636）上被列为已知发送垃圾邮件的网络。

² 编写本文时，此主机被已知充当通配符 MTA。

由于我们编辑的是 CIDR 类型的映射，这是一种顺序映射类型（参见第 5 章），因此你不需要也不能使用`postmap`进行转换。Postfix 将按原样使用该文件。只需将`check_sender_mx_access`选项及其映射作为参数添加到`smtpd_recipient_restrictions`参数中。示例如下：

```
smtpd_recipient_restrictions =
    reject_non_fqdn_recipient
    reject_non_fqdn_sender
    reject_unknown_sender_domain
    reject_unknown_recipient_domain
    permit_mynetworks
    reject_unauth_destination
    check_recipient_access hash:/etc/postfix/roleaccount_exceptions
    reject_non_fqdn_hostname
    reject_invalid_hostname
    check_helo_access pcre:/etc/postfix/helo_checks
    check_sender_mx_access cidr:/etc/postfix/bogus_mx
    permit
```

重新加载 Postfix 后，限制生效。你可以在邮件日志中看到限制的效果：

```
Sep 17 12:19:23 mail postfix/smtpd[3323]: A003D15C021: reject: RCPT from
unknown[61.238.134.162]:
  554 <recipient@example.com>: Sender address rejected: VeriSign Domain
wildcard;
  from=<alli.k_lacey_mq@joymail.com> to=<recipient@example.com> proto=ESMTP
  helo=<example.com>
```

你可以使用`host`命令检查该 IP 地址：

```
# host -t mx joymail.com
# host -t a joymail.com
joymail.com has address 64.94.110.11
```

> **注意** 此域名现在确实存在；看起来它是在 2003 年 10 月注册的。

## 向多收件人发送反弹邮件

在"空信封发件人"部分中，你了解到不应该阻止空信封发件人。此规则有一个例外——你应该阻止发送给多个收件人的空信封发件人邮件，因为目前没有已知的多收件人状态通知的合法用途，因此任何此类消息都可能是不合法的。

要拒绝来自空信封发件人发送给多个收件人的消息，请将`reject_multi_recipient_bounce`选项添加到`smtpd_recipient_restrictions`列表中。它几乎可以出现在限制列表中的任何位置，但以下是一个将其放在`permit_mynetworks`选项之后的示例。

如文档中所述，`reject_multi_recipient_bounce` 仅在 `smtpd_data_rejections` 中所有收件人都已知时才能可靠使用。

你可以通过手动连接来测试，就像之前测试其他限制选项一样。提交一个空信封发件人和多个收件人，应该会导致拒绝服务，如下列会话所示：

```
$ telnet localhost 25
220 mail.example.com ESMTP Postfix
EHLO client.example.com
250-mail.example.com
250-PIPELINING
250-SIZE 10240000
250-VRFY
250-ETRN
250 8BITMIME
MAIL FROM:<>
250 Ok
RCPT TO: <recipient1@example.com>
RCPT TO: <recipient2@example.com>
550 : Recipient address rejected: Multi-recipient bounce
QUIT
221 Bye
```

## 使用 DNS 黑名单

黑名单 DNS 服务器是一种可以告诉你哪些资源（如 IP 地址、信封发件人和域名）可能不可信的服务器。如果你选择了正确的黑名单，黑名单可以非常有效地阻止从客户端发送到你服务器的邮件。然而，选择错误的黑名单可能会导致你的服务器拒绝你认为合法的邮件。在使用黑名单之前，请务必查看其策略。任何运行黑名单的网站都应该列出其对资源进行黑名单处理时所采用的标准，并应公布一个简单明了的流程，用于移除不再需要黑名单处理的资源。

如果你正在寻找黑名单，一个可以参考的地方是 dmoz.org (http://dmoz.org/Computers/Internet/Abuse/Spam/Blacklists)。

> **注意** 所有黑名单都基于域名服务，这意味着 Postfix 必须执行 DNS 查询。未缓存的 DNS 查询可能需要长达一秒钟的时间，如果超时，服务器接受消息的速率将大幅下降。因此，黑名单检查在延迟方面代价相对较高。你应该始终将它们作为限制选项列表中的最后手段。

### 拒绝被列入黑名单的客户端

你可以使用 DNSBL（基于 DNS 的黑洞列表）黑名单来拒绝被列入黑名单的客户端。Postfix 有一个 `reject_rbl_client` 限制选项，它接受黑名单服务器的 FQDN 主机名作为参数。以下是该选项的使用示例：

```
smtpd_recipient_restrictions =
    reject_non_fqdn_recipient
    reject_non_fqdn_sender
    reject_unknown_sender_domain
    reject_unknown_recipient_domain
    permit_mynetworks
    reject_unauth_destination
    check_recipient_access hash:/etc/postfix/roleaccount_exceptions
    reject_non_fqdn_hostname
    reject_invalid_hostname
    check_helo_access pcre:/etc/postfix/helo_checks
    reject_rbl_client relays.ordb.org
    permit
```

重新加载 Postfix 后，新选项即生效。

> **注意** 要查看客户端是否在 DNSBL 列表中，请将客户端 IP 地址的四个八位组反转（即将 a.b.c.d 改为 d.c.b.a），附加 rbl.domain（如 relays.ordb.org），然后查询结果。如果该主机被列入黑名单，你将获得一个指向原始 IP 地址的响应，如下例所示：

```
$ host 2.0.0.127.relays.ordb.org
2.0.0.127.relays.ordb.org A 127.0.0.2
```

### 多值结果

Postfix 可以处理这些附加信息（主机不仅仅是被列入列表，返回的 IP 地址还可以区分其被列入的原因）。例如，以下配置拒绝来自任何在我们虚构的 domain.tld 黑名单中映射到 A 记录 127.0.0.2 的主机的消息：

```
reject_rbl_client domain.tld=127.0.0.2
```

### 拒绝被列入黑名单的发件人域名

除了限制来自 IP 地址的邮件外，你还可以阻止来自被列入黑名单的发件人域名的邮件。这种黑名单称为右侧黑名单（RHSBL）。为 Postfix 配置 RHSBL 的步骤是相同的。本节中的示例使用了 dsn.rfc-ignorant.org 上的一个特殊黑名单：

> **www.rfc-ignorant.org 使命宣言：**
>
> 我们维护着一些列表（目前包括 dsn、abuse、postmaster、bogusmx 和 whois），其中包含的域名管理员选择不遵守 RFC，即互联网的基石"规则"。
>
> 需要特别指出的是，没有任何规定要求任何人必须遵守 RFC（严格来说是"征求意见稿"），然而，互联网所享有的"协作互操作性"是基于每个人都拥有相同的"规则手册"并遵循它。在此列出仅仅意味着某个网站选择不实施特定 RFC 中描述的条件。当然，其他网站可以自行决定是否希望与那些选择不实施（例如）RFC2142、没有可用的 <abuse@domain> 地址的网站进行通信。
>
> —dredd, www.rfc-ignorant.org

有许多 MTA 不接受 RFC 所要求的邮件方式（例如，它们可能会拒绝空信封发件人），出于各种错误的原因，包括以下几点：

- 不允许来自匿名发件人的虚假邮件
- 禁止空发件人（以打击垃圾邮件问题）

对于这些非 RFC 兼容邮件服务器的错误消息，需要说明的是：任何人都可以伪造任何人的电子邮件地址。你完全可以用 president@whitehouse.gov 发送电子邮件，这和使用空信封发件人一样是匿名的。

垃圾邮件可以使用任意发件人发送，但退信*只能*使用空信封发件人发送。

任何阻止空信封发件人的邮件服务器，都在禁止其用户了解他们的邮件可能已被另一台邮件服务器拒绝，因为其服务器阻止了另一台 RFC 兼容服务器发送的退信——该退信使用空信封发件人，正如 RFC 中所述：

RFC 2821 明确规定，MTA *必须*接受带有空返回路径（信封发件人）的邮件，因为"在发送退信时使用空发件人可以防止不可投递的退信在两个系统之间循环。"

Postfix 有一个 `reject_rhsbl_sender` 限制选项，它会从任何电子邮件地址中剥离本地部分，并使用域名查询黑名单（如 dsn.rfc-ignorant.org）。如果客户端的信封发件人域名在黑名单中，Postfix 将拒绝该入站消息。与其他黑名单选项一样，你应该将此选项放在列表末尾，如下例所示：

```
smtpd_recipient_restrictions =
    reject_non_fqdn_recipient
    reject_non_fqdn_sender
    reject_unknown_sender_domain
    reject_unknown_recipient_domain
    permit_mynetworks
    reject_unauth_destination
    reject_multi_recipient_bounce
    reject_rbl_client relays.ordb.org
    check_recipient_access hash:/etc/postfix/roleaccount_exceptions
    reject_non_fqdn_hostname
    reject_invalid_hostname
    check_helo_access pcre:/etc/postfix/helo_checks
    reject_rhsbl_sender dsn.rfc-ignorant.org
    permit
```

重新加载后即生效，你可以通过连接到服务器并使用来自 dsn.rfc-ignorant.org 上列出域名的信封发件人来测试，如下例所示（sender@example.com 是官方测试地址）：

```
$ telnet localhost 25
220 mail.example.com ESMTP Postfix
EHLO client.example.com
250-mail.example.com
250-PIPELINING
250-SIZE 10240000
250-VRFY
250-ETRN
250 8BITMIME
MAIL FROM:<sender@example.com>
250 Ok
RCPT TO: <recipient@example.com>
554 Service unavailable; Sender address [sender@example.com] blocked \
    using dsn.rfc-ignorant.org; Not supporting null originator (DSN)
QUIT
221 Bye
```

### 手动黑名单检查

在 RHSBL 中检查域名与检查 IP 地址的过程类似，只是你不必反转任何元素的顺序。只需将黑名单服务器名称附加到你要检查的域名后面，然后进行 DNS 查询即可。

以下是一个不在黑名单中的域名的检查结果：

```
$ host postfix-book.com.dsn.rfc-ignorant.org
Host postfix-book.com.dsn.rfc-ignorant.org not found: 3(NXDOMAIN)
```

被列入黑名单的域名看起来像这样：

```
$ host example.com.dsn.rfc-ignorant.org
example.com.dsn.rfc-ignorant.org has address 127.0.0.2
```

### 被列入黑名单的发件人域名的例外情况

如果你想拒绝不遵守规则的邮件服务器发送的邮件，但又需要与某个原本会被你的限制规则拒绝的特定域名保持通信，你可以创建一个例外列表。使用 `check_sender_access` 选项配合映射表来实现例外。

首先，创建一个文件，例如 /etc/postfix/rhsbl_sender_exceptions，其中包含你想要接受其消息的用户和域名。例如，以下文件允许来自 example.com 的所有用户以及单个用户 sender@example.org 的邮件：

```
example.com	OK
sender@example.org	OK
```

文件就绪后，使用 `postmap hash:/etc/postfix/rhsbl_sender_exceptions` 构建映射表。然后将 `check_sender_access` 选项添加到 `reject_rhsbl_sender` 选项之前，如下例所示：

```
smtpd_recipient_restrictions =
  reject_non_fqdn_recipient
  reject_non_fqdn_sender
  reject_unknown_sender_domain
  reject_unknown_recipient_domain
  permit_mynetworks
  reject_unauth_destination
  reject_multi_recipient_bounce
  reject_rbl_client relays.ordb.org
  check_recipient_access hash:/etc/postfix/roleaccount_exceptions
  reject_non_fqdn_hostname
  reject_invalid_hostname
  check_helo_access pcre:/etc/postfix/helo_checks
  check_sender_access hash:/etc/postfix/rhsbl_sender_exceptions
  reject_rhsbl_sender dsn.rfc-ignorant.org
  permit
```

**注意** 本示例使用了`check_sender_access`，但以下是完整的异常选项列表：

- check_sender_access
- check_client_access
- check_helo_access
- check_recipient_access

你已在“防止明显伪造”一节中了解了`check_helo_access`。其余两项在 Postfix 文档中有说明。

## 验证发件人

Postfix 反垃圾邮件工具的核心是发件人地址验证，它验证信封发件人是否存在于发件人的域中：如果发件人不存在，Postfix 将不接受该邮件。

不幸的是，此功能开销较大，因为验证过程耗时并消耗额外的系统资源。涉及的步骤如下：

1. 客户端提交一个信封发件人。
2. Postfix 生成一个探测消息并排队发送给该信封发件人。
3. Postfix 查询信封发件人域的 MX 或 A 记录。
4. Postfix 尝试连接发件人的邮件服务器。如果无法连接到远程服务器，`smtpd` 会通过向客户端返回临时错误代码 450 来推迟是否接受邮件的决定。同时，Postfix 会继续尝试验证地址。
5. Postfix 与远程服务器建立 SMTP 会话。
6. Postfix 将之前的信封发件人作为信封收件人提交给远程邮件服务器。
7. 根据远程服务器的响应，Postfix 可以执行以下两种操作之一：
   - 如果远程邮件服务器接受了该收件人（原始的信封发件人），Postfix 会断开连接，销毁探测消息，并接受来自原始客户端的消息。
   - 如果远程邮件服务器拒绝了该收件人（原始的信封发件人），Postfix 会断开连接，销毁探测消息，并拒绝来自客户端的消息。

启用地址验证后，正常邮件在 Postfix *首次*检查地址时会经历长达九秒的短暂延迟。然而，Postfix 会缓存地址状态，因此后续邮件不会有延迟。

如果验证过程耗时超过九秒，`smtpd` 会以 450 回复拒绝来自客户端（发送机器）的邮件。正常的邮件客户端会在一段时间延迟后重新连接，但被劫持的代理不会，因为它们只是在转发 SMTP 命令，而控制代理的人不会想在这个地址上再浪费时间。

### 发件人地址验证配置

要启用发件人地址验证，请在 `smtpd_recipient_restrictions` 参数中添加 `reject_unverified_sender` 选项，如示例所示：

```
smtpd_recipient_restrictions =
    reject_non_fqdn_recipient
    reject_non_fqdn_sender
    reject_unknown_sender_domain
    reject_unknown_recipient_domain
    permit_mynetworks
    reject_unauth_destination
    reject_multi_recipient_bounce
    reject_rbl_client relays.ordb.org
    check_recipient_access hash:/etc/postfix/roleaccount_exceptions
    reject_non_fqdn_hostname
    reject_invalid_hostname
    check_helo_access pcre:/etc/postfix/helo_checks
    check_sender_access hash:/etc/postfix/rhsbl_sender_exceptions
    reject_rhsbl_sender dsn.rfc-ignorant.org
    reject_unverified_sender
    permit
```

除了 `reject_unverified_sender`，你还可以在限制条件中添加其他选项。然而，这些参数具有合理的默认值，它们用于调整发件人地址验证的行为，而不是进行配置。以下小节描述了对发件人地址验证行为最常见的更改。你可以在 Postfix 安装附带的 `ADDRESS_VERIFICATION_README` 文件中找到额外的调整参数。

### 探测消息的信封发件人

当 Postfix 生成探测消息以验证相关发件人时，它必须用自己的一个信封发件人向远程服务器进行自我介绍。你可以使用 `address_verify_sender` 参数配置此地址。默认值为 `postmaster@$myorigin`。

如果你想设置不同的探测信封发件人，请在 `main.cf` 中添加 `address_verify_sender` 参数，如示例所示：

```
address_verify_sender = sender@example.com
```

当然，此发件人必须存在，因为其他服务器可能会对你使用相同的发件人地址验证。

> 指定为 `address_verify_sender` 参数的收件人地址不受任何限制。

### 缓存

默认情况下，Postfix 将已验证的发件人保存在内存中。如果你重新加载或重新启动 Postfix，你将丢失它们，除非你指定一个可选的数据库来永久存储地址。要使用数据库，请将 `address_verify_map` 参数设置为一个数据库路径（确保你选择了一个有*充足*空间的文件系统）。以下是示例：

```
address_verify_map = btree:/var/spool/postfix/verified_senders
```

重新加载后，Postfix 会创建数据库，并继续添加正向和负向验证。如果你想要禁用收集负向验证，请在 `main.cf` 中设置 `address_verify_negative_cache` 参数，如下所示：

```
address_verify_negative_cache = no
```

### 选择性发件人地址验证

随着邮件服务器负载的增加，发件人地址验证更可能成为瓶颈。此时，你应该切换到选择性发件人地址验证。

选择性发件人地址验证的工作原理是创建一个常用信封发件人域的映射表，这些域是垃圾邮件发送者通常使用的。如果传入的信封发件人域在此映射表中，Postfix 会验证发件人，否则不会费心。创建一个映射文件，例如 `/etc/postfix/common_spam_senderdomains`，并设置 `reject_unverified_sender` 参数作为当信封发件人匹配该域时要执行的操作。以下是此类文件的示例：

```
hotmail.com   reject_unverified_sender
web.de         reject_unverified_sender
msn.com        reject_unverified_sender
mail.ru        reject_unverified_sender
```

access(5) 手册页说明，此映射的右侧是一个有效的限制条件或 `smtpd_restriction_class` 的名称。在此示例中，当客户端发起消息传输时，Postfix 执行以下两种操作之一：

- 如果发件人的域与 `common_spam_senderdomains` 中的条目匹配，映射查找返回 `reject_unverified_sender`，因此 Postfix 会验证信封发件人。如果地址有效，`reject_unverified_sender` 返回 `DUNNO`，Postfix 评估下一个限制条件。如果地址无效，Postfix 拒绝该消息。
- 如果发件人域与 `common_spam_senderdomains` 中的任何条目都不匹配，映射查找失败，选择性评估器返回 `DUNNO`，Postfix 评估下一个限制条件而不验证发件人地址。

创建映射后，使用 `postmap hash:/etc/postfix/common_spam_senderdomains` 命令将其转换为数据库。最后，将现有的 `reject_unverified_sender` 选项替换为 `check_sender_access` 选项和映射参数。以下是使用 `hash:/etc/postfix/common_spam_senderdomains` 映射的示例：

```
smtpd_recipient_restrictions =
  reject_non_fqdn_recipient
  reject_non_fqdn_sender
  reject_unknown_sender_domain
  reject_unknown_recipient_domain
  permit_mynetworks
  reject_unauth_destination
  reject_multi_recipient_bounce
  check_recipient_access hash:/etc/postfix/roleaccount_exceptions
  reject_non_fqdn_hostname
  reject_invalid_hostname
  check_helo_access pcre:/etc/postfix/helo_checks
  check_sender_access hash:/etc/postfix/rhsbl_sender_exceptions
  reject_rhsbl_sender dsn.rfc-ignorant.org
  check_sender_access hash:/etc/postfix/common_spam_senderdomains
  permit
```

你可以更进一步，引入除信封发件人之外的标准，例如内容。创建另一个名为 `common_spam_senderdomain_keywords` 的映射，其中包含触发发件人地址验证的域名关键字，如以下示例：

```
/sex/  reject_unverified_sender
/girl/  reject_unverified_sender
/sell/  reject_unverified_sender
/sale/  reject_unverified_sender
/offer/ reject_unverified_sender
/power/ reject_unverified_sender
```

然后添加另一个指向该映射的 `check_sender_access` 选项：

```
smtpd_recipient_restrictions =
  reject_non_fqdn_recipient
  reject_non_fqdn_sender
  reject_unknown_sender_domain
  reject_unknown_recipient_domain
  permit_mynetworks
  reject_unauth_destination
  reject_multi_recipient_bounce
  check_recipient_access hash:/etc/postfix/roleaccount_exceptions
  reject_non_fqdn_hostname
  reject_invalid_hostname
  check_helo_access pcre:/etc/postfix/helo_checks
```



## 限制顺序

从系统资源的角度来看，反垃圾邮件防护的开销很大。以下限制列表展示了如何排列反垃圾邮件选项。

```
smtpd_recipient_restrictions =
    reject_non_fqdn_recipient
    reject_non_fqdn_sender
    reject_unknown_sender_domain
    reject_unknown_recipient_domain
    permit_mynetworks ①
    (permit_sasl_authenticated)
    (pop-before-smtp)
    reject_unauth_destination
    check_recipient_access hash:/etc/postfix/roleaccount_exceptions
    reject_multi_recipient_bounce
    check_helo_access pcre:/etc/postfix/helo_checks ②
    reject_non_fqdn_hostname
    reject_invalid_hostname
    check_sender_mx_access /etc/postfix/verisign_mx_access ③
    check_sender_access hash:/etc/postfix/rhsbl_sender_exceptions ④
    reject_rhsbl_sender dsn.rfc-ignorant.org ⑤
    check_sender_access hash:/etc/postfix/common_spam_senderdomains ⑥
    check_sender_access regexp:/etc/postfix/common_spam_senderdomain_keywords
    permit
```

排列"低开销"限制先于"高开销"限制的一般规则：
① 将所有反垃圾邮件选项放在 permit_mynetworks *之后*，使其仅对外部客户端（未列在 mynetworks 中的客户端）生效。
② 对于使用你服务器主机名的客户端，无需进一步调查即可直接拒绝。无论其使用的是非完全限定域名主机名还是无效主机名，均不例外。
③ 此选项标志着高开销限制的开始。check_sender_mx_access 需要一到两次 DNS 查询。如果你运行的是缓存域名服务器，则可以在本地解析 DNS 查询。
④ 此映射表放在黑名单选项之前，因为它包含了可能被拒绝的用户和域名的例外情况。
⑤ 此选项开销较大，需要查询远程系统（dsn.rfc-ignorant.org 的 DNS 服务器），该系统可能负载较重或暂时不可用。因此它被放置在限制选项列表的末尾附近。
⑥ 两个开销最大的操作放在最后。如果被触发，Postfix 必须创建一个虚拟邮件、尝试投递并记录结果。开销非常大，因此仅作为最后手段使用。

## 限制类的用途

本节中的示例通过两种方式限制信封发件人。首先，它要求来自外部的邮件*不得*具有你域名内的发件人地址；其次，它要求来自内部客户端的邮件*必须*包含你域名内的发件人地址。

其思路是让 Postfix 首先检查传入的客户端连接是否来自你的网络：

1. 如果客户端在你的网络上，Postfix 将该客户端转到一个限制类。此类包含对信封发件人地址的检查。
   - 如果信封发件人匹配你的域名通配符，检查返回 OK。Postfix 停止评估限制并允许客户端继续。
   - 如果信封发件人未匹配域名通配符，下一个限制选项是 *reject*，因此 Postfix 拒绝为该客户端提供服务。
2. 如果客户端不属于你的网络，Postfix 不使用限制类，而是继续执行下一个限制选项，该选项检查信封发件人地址。
   - 如果客户端在信封发件人中使用了你的域名，Postfix 拒绝服务。
   - 如果客户端未在信封发件人中使用你的域名，则通过测试并继续执行下一个限制。

要实现上述功能，首先创建一个映射文件，包含你网络内的 IP 地址和网络列表。你可以将文件命名为 /etc/postfix/internal_networks；其内容如下：

```
192.0.34     has_our_domain_as_sender
192.168      has_our_domain_as_sender
192.168.1    has_our_domain_as_sender
```

然后，创建另一个映射文件 /etc/postfix/our_domain_as_sender，包含你的域名通配符和空信封发件人（记住你的服务器应该无条件接受此项）；这是内部客户端可以使用的信封发件人域名列表。映射文件内容如下：

```
example.com    OK
<>             OK
```

接下来，创建一个映射文件，包含外部客户端不得在其信封发件人中使用的域名。本例中使用文件名 /etc/postfix/not_our_domain_as_sender，仅包含一行内容：

```
example.com    554 Do not use my domain in your envelope sender
```

使用 postmap 命令为这两个映射文件创建映射后，在 main.cf 文件中设置限制类和所需的限制选项：

```
smtpd_restriction_classes =
    has_our_domain_as_sender
has_our_domain_as_sender =
    check_sender_access hash:/etc/postfix/our_domain_as_sender
    reject
smtpd_recipient_restrictions =
    check_client_access hash:/etc/postfix/internal_networks
    check_sender_access hash:/etc/postfix/not_our_domain_as_sender
    reject_unauth_destination
    ...
    permit
```

与往常一样，你需要重新加载 Postfix 配置以使更改生效。

# 第 9 章

## 内置内容过滤器的工作原理

![](img/852c79f689feb77c5fde686b993808b1_139_0.png)

检查会审查消息的内容，并根据内容执行预定义的操作。本章将向你介绍可用的检查类型，以及 Postfix 为实施内容控制提供了哪些操作。

检查是对限制的补充。*限制*监督 SMTP 对话，而*检查*控制消息的内容。不过，你最初可能会觉得检查与限制有很大不同。检查易于启用，但用于创建搜索模式的语法可能会变得相当复杂，因为检查使用正则表达式来定义搜索模式。

由于 Postfix 专注于作为 MTA 运行，其内置检查并非旨在替代功能全面的内容扫描器，而是为简单任务提供手段。以下是你可以使用检查完成的一些事情：

- 阻止由特定程序生成的消息，例如你的 SAP 邮件网关。
- 阻止具有特定主题行的消息。
- 过滤掉包含潜在有害附件的消息。
- 从消息头中删除特定信息。

> 注意：*如果你以前从未使用过正则表达式，可能需要花一些时间学习基础知识。Jeffrey E.F. Friedl 所著的《Mastering Regular Expressions, 2nd Edition》是一本关于该主题的优秀书籍。*

## 检查的工作原理是什么？

检查通过一组搜索模式扫描消息。如果某个模式与消息中的任何内容匹配，就会执行相应的操作。Postfix 可以对消息的不同部分应用单独的过滤器；Postfix 目前支持的部分如下：

- 消息头
- MIME 头
- 消息正文部分（包括附件）
- 附加消息的消息头

要创建一组检查，你需要使用单独的映射文件定义不同的搜索模式，然后将这些映射文件分配给适用于不同部分的不同检查参数。Postfix 使用这些映射文件配合内置的 MIME 解析器来检查消息内容。该解析器的工作方式类似于 egrep 命令；它只能每次逐行识别纯文本单词。以下是处理过程：

1. 解析器逐行遍历消息。
2. 解析器判断当前行属于消息的哪个部分。
3. 如果该部分存在对应的检查，Postfix 使用分配的映射文件在消息中搜索匹配的模式。
4. 如果搜索模式匹配成功，Postfix 触发一个操作，并停止执行其他检查。因此，第一个匹配的结果"生效"。

你可能已经猜到，检查是 CPU 密集型操作，而且映射文件中搜索模式的顺序可能至关重要，因为较早的匹配会使检查过程占用更少的 CPU 时间。

## 将检查应用于消息的不同部分

Postfix 为其识别的每个消息部分使用单独的配置参数。检查参数如下（注意它们在 main.cf 文件中默认未启用）。



**header_checks**
这些检查应用于消息头——即从消息的第一行到第一个空行之间的所有内容。这也包括跨越多个物理行的消息头。

**body_checks**
这些检查应用于消息正文；解析器将正文视为消息头之间的所有内容。

> **注意** *大量的 `body_checks` 命令可能非常耗费CPU资源，显著降低你的机器运行速度，因为正文检查会扫描正文段的每一行，并将该行与你在 `body_checks` 映射中定义的每个正则表达式进行比较。*

*为防止CPU过载，默认情况下，Postfix仅检查当前正文段的前51,200个字节。你可以通过 `body_checks_size_limit` 参数增加此限制。你也可以通过使用第11章描述的 `content_filter` 功能，将内容检查委托给另一台独立机器上的不同应用程序来处理增加的负载。*

**mime_header_checks**
这些检查应用于顶级消息头中的MIME头、MIME实体头，以及嵌套消息RFC 822消息头中的MIME头（参见图6-3）。

**nested_header_checks**
这些检查应用于附加电子邮件消息的头（MIME头除外）。这些检查仅作用于嵌套 `message/rfc822` 消息的头，不包括上面列出的 `mime_header_checks` 的MIME头。

## **这些参数有什么特别之处？**

Postfix 2.x 将消息正文处理为 *n* 个正文段，每个部分都用MIME头标记。默认情况下，此MIME处理是启用的，但你可以在 `main.cf` 文件中使用 `disable_mime_input_processing = yes` 来禁用它。

MIME解析器对其读取的每一行做出判断：该行属于头部还是正文段？Postfix基于此判断应用检查。如果一个消息段包含邮件头（即，如果它是 `message/rfc822` 类型的附加消息），则这些头由 `nested_header_checks` 评估。

在这些嵌套头之后，段内的任何内容都将由 `body_checks` 评估，直至达到 `body_checks_size_limit` 参数指定的限制。例如，如果你有一个包含五个100KB MIME段（或附件）的消息，Postfix会检查 *每个* 段的前 `body_checks_size_limit` 个字节。

Postfix使用 `mime_header_checks` 来评估每个MIME头（每个新段的开头）。如果在任何MIME头之后存在邮件头，则它们在每个段上由 `nested_header_checks` 评估。

图9-1显示了针对消息的每一行应用了哪些检查。

![](img/852c79f689feb77c5fde686b993808b1_142_0.png)

图9-1：Postfix为消息的每一行决定应用哪个检查

## Postfix何时应用检查？

客户端在成功完成初始SMTP对话后传输消息。因此，Postfix在 `smtpd_*_restrictions` 处理完毕后处理 `*_checks`。图9-2显示了Postfix清理守护进程何时处理检查。

```
$ telnet mail.example.com 25
220 mail.example.com ESMTP Postfix
HELO client.example.com
250-mail.example.com
MAIL FROM:<sender@example.com>
250 Ok
RCPT TO:<recipient@example.com>
250 Ok
DATA
354 End data with <CR><LF>.<CR><LF>
From: "Sender" <sender@example.com>
To: "Recipient" <recipient@example.com>
Date: Sat, 17 May 2003 15:24:43 +0200

Here comes the mail content. . . .
250 Ok: queued as oEAFFE1C6S
QUIT
221 Bye
```

图9-2：检查仅应用于消息内容，并且在限制条件之后执行

## 检查可以调用哪些操作？

每个搜索模式只能定义一个操作。Postfix当前支持以下操作：

- **REJECT** *[可选文本...]*
  拒绝接受消息。可选文本将被发送回尝试传递消息的客户端。Postfix还会将该文本记录在邮件日志中。
- **IGNORE**
  从消息中移除与检查中的搜索模式匹配的行。
- **WARN** *[可选文本...]*
  使Postfix向邮件日志写入一条通知。如果有可选文本，Postfix也会将其记录下来。Postfix将在不进行任何修改的情况下传递消息。
- **HOLD** *[可选文本...]*
  将消息放入保留队列，直到邮局管理员取走并决定如何处理。Postfix会将匹配的头/正文行与可选文本一起记录。
- **DISCARD** *[可选文本...]*
  告诉邮件客户端消息已成功传递，但静默删除该消息，而不是将其传输到最终目的地。如果有可选文本，Postfix会将其与匹配的文本一起记录在邮件日志中。
- **FILTER** transport:nexthop
  将消息发送到过滤器（在 `master.cf` 中定义的服务，将消息传输到另一个处理系统，如病毒扫描器）。你将在第11章了解更多关于定义过滤器的信息。
- **REDIRECT** user@domain
  将消息重新路由到指定的地址，而不是原始收件人，并且它会覆盖任何FILTER操作。

# 10
## 使用内置内容过滤器

![](img/852c79f689feb77c5fde686b993808b1_145_0.png)

如第9章所述，Postfix可以使用模式和操作表来检查消息内容。本章将向你展示如何实现这些模式和操作。请记住，检查是用于简单内容过滤的。对于更复杂的任务，请参考第11章。

检查在消息中查找字符，也可以修改消息。启用检查的配置参数名称以 `_checks` 结尾，无论你使用 `header_checks`、`body_checks`、`mime_header_checks` 还是 `nested_header_checks`，它们都遵循相同的方案：

1.  Postfix逐行检查消息，对照由正则表达式（regexp）或Perl正则表达式（PCRE）组成的模式映射。
2.  如果一行匹配正则表达式，则Postfix执行为该表达式定义的操作，并检查输入的下一行。

> **注意** 本章的示例大量使用了Postfix提供的行延续语法，以提高纸面文档的可读性。即，以空白字符开头的行是前一行的延续。

## 检查Postfix是否支持检查功能

Postfix默认支持头或正文过滤，但因为它可能使用regexp和/或PCRE映射，你应该弄清楚Postfix是支持两种类型还是仅支持regexp。要检查你的Postfix支持哪些映射，请运行 `postconf -m` 来报告你的系统支持的所有映射类型。以下示例中的Postfix软件包支持regexp和PCRE等多种映射：

```
$ postconf -m

btree
cidr
environ
hash
nis
pcre
proxy
regexp
static
tcp
unix
```

所有系统默认都应支持regexp表。如果你的系统在使用regexp样式的映射时遇到性能问题（或者更糟的是，如果你的系统使用了有缺陷的regexp实现），你可以安装PCRE库和头文件，并重新编译Postfix以支持PCRE。

## *使用PCRE映射支持编译Postfix*

要编译支持PCRE的Postfix，你需要PCRE库和头文件。你可以从你的发行版的开发包中获取它们，也可以从http://www.pcre.org 下载PCRE源代码并手动安装。

通过将 `-DHAS_PCRE` 和用于PCRE包含目录的 `-I` 预处理器标志添加到 `CCARGS`，并将PCRE库和路径标志添加到 `AUXLIBS`，来配置Postfix以支持PCRE。例如，假设 `pcre.h` 在 `/usr/local/include` 中，`pcre.a` 在 `/usr/local/lib` 中：

```
$ CCARGS="-DHAS_PCRE -I/usr/local/include" \
  AUXLIBS="-L/usr/local/lib -lpcre" \
  make makefiles
$ make
```

> **注意** *Solaris 也需要 `-R/usr/local/lib`。*

## 安全地实现头或正文过滤

正则表达式可能变得相当复杂，你最终可能会得到一个不工作、匹配范围超出预期，或者你不再理解的模式。

为了帮助你调试模式，Postfix提供了 `WARN` 操作。如果你在模式的右侧使用此操作，当表达式匹配时，Postfix会传递消息，并且还会在邮件日志中写入一条注释。在你确定模式工作正常后，可以安全地将 `WARN` 更改为所需的操作。

添加检查的安全流程如下：

1.  将你的模式添加到映射中，操作设置为 `WARN`。
2.  创建一个包含与你的过滤模式匹配的表达式的文件。
3.  验证映射中的模式与测试模式匹配。
4.  在Postfix主配置文件中设置该检查。
5.  使用真实邮件进行测试。

### 添加正则表达式并设置WARN操作

第一步是将要检查的模式添加到映射中，并为消息内容匹配测试模式时定义 `WARN` 操作。本节中我们将使用的示例测试 `Subject` 头中的过滤模式，但你可以将此处描述的过程用于其他头和其他 `*_checks` 参数。

将过滤模式添加到 `/etc/postfix/header_checks` 文件中。此文件保存 `header_checks` 的映射。示例如下：

```
/^Subject: FWD: Look at pack from Microsoft/
    WARN Unhelpful virus warning
```

### 创建测试模式

创建测试模式只需将匹配的消息放入文件，例如 `/tmp/testpattern`。以下内容可用于此示例：

```
From: dingdong@example.com
Subject: FWD: Look at pack from Microsoft
blah blah
```

### 正则表达式是否匹配测试模式？

通过将检查映射和测试模式提供给 `postmap` 来测试你的过滤模式。例如，运行此命令：

```
$ postmap -q - regexp:/etc/postfix/header_checks < /tmp/testpattern
```

如果匹配成功，命令会打印测试模式匹配的行，如下所示：

```
Subject: FWD: Look at pack from Microsoft                 WARN Unhelpful virus warning
```

如果模式不匹配，`postmap` 命令不会打印任何内容。

### 在主配置中设置检查

如果到目前为止一切正常，你可以编辑你的 `main.cf` 文件，使用包含你刚刚创建和测试的 `header_checks` 的文件：

```
header_checks = regexp:/etc/postfix/header_checks
```

重新加载 Postfix 并发送包含相同测试模式的测试邮件。

### 使用真实邮件进行测试

要使用真实邮件测试过滤器，请将你之前的测试模式提供给 Postfix。以下命令可以实现：

```
$ /usr/sbin/sendmail recipient@example.com < /tmp/testpattern
```

现在，检查你的邮件日志以验证 Postfix 是否为测试模式记录了警告。以下日志摘录中的第二行就是警告消息：

```
Mar 30 17:17:52 mail postfix/pickup[2455]: 53CAB633B3: uid=7945 from=<sender@example.com>
Mar 30 17:17:52 mail postfix/cleanup[2461]: 53CAB633B3: warning: header Subject: FWD: Look at pack from Microsoft from local; from=<sender@example.com> to=<recipient@example.com>: Unhelpful virus warning
Mar 30 17:17:52 mail postfix/cleanup[2461]: 53CAB633B3: message-id=<20040330151752.53CAB633B3@mail.example.com>
Mar 30 17:17:52 mail postfix/qmgr[2456]: 53CAB633B3: from=<sender@example.com>, size=346, nrcpt=1 (queue active)
```

在你确信过滤模式有效后，你可以安全地将操作从 WARN 更改为实际执行操作的动作，例如 REJECT 或 DISCARD。

## 检查信头

Postfix 可以使用 `header_checks` 执行多种操作，例如拒绝或保留邮件、移除信头、或丢弃、重定向或过滤邮件。本节讨论如何实现这些操作。

### 拒绝邮件

Postify 可以使用 REJECT 操作拒绝邮件。你可以使用此操作阻止匹配特定模式的邮件，例如包含特定主题头的邮件。

拒绝操作可以阻止邮件进入系统，从而使它们远离计算密集型的病毒检查器、垃圾邮件检测器或（可能更糟的）你的用户。我们将看几个例子。

此模式拒绝由 ScanMail 生成的无用病毒警告（即使病毒伪造发件人地址，它也总是警告发件人）：

```
/^Subject: ScanMail Message: To Sender, sensitive content found and action/
REJECT Unhelpful virus warning
```

如果你想阻止带有不正确的 Undisclosed-recipients 信头的邮件，可以使用以下模式。这匹配信头中出现 To: <Undisclosed Recipients> 的情况（无论是否有方括号，无论末尾是否有最终的 "s"）。（正确的 Undisclosed-recipients 信头应该是 To: undisclosed-recipients:;。）

```
/^To:.*<?Undisclosed Recipients>?>$/
REJECT Wrong undisclosed recipients header
```

此模式最好通过其注释和附带消息来描述：

```
#
# Spam that contains Subject: something   565876
#
/^Subject:.*[[:space:].]{5,}\(?#[[:digit:]]{2,}\)?$/
REJECT More than 5 whitespaces and a number follow the Subject:
```

我们从未在有效邮件的信头中见过 To:…<>：

```
/^To:.*<>/
REJECT To: <> in headers
```

最后，有些主题行简直是欺诈垃圾邮件的典型。你应该从这四个模式中得到想法。（为每个警告消息使用不同的数字有助于调试误报。）

```
#
# Certain Subject lines are indicative of fraud spam.
#
/^Subject:.*is NOT being SEEN/    REJECT fraud spam #1
/^Subject:.*URGENT BUSINESS RELATIONSHIP/   REJECT fraud spam #2
/^Subject:.*Confidential Proposal/  REJECT fraud spam #3
/^Subject: SEX-FLATRATE/    REJECT fraud spam #4
```

### 暂停投递

Postfix 可以使用 HOLD 操作暂停邮件的投递。你可以用它将可疑邮件“挂起”以进行进一步检查。要查看邮件，使用 postcat；要让邮件通过，使用 postsuper -H。如果你想从 Postfix 队列中删除邮件，请使用 postsuper -d。

这是一个匹配任何包含以 Subject: [listname] 开头的 Subject 信头的邮件的模式。一个用途是在工作时间后（系统未完全使用时）暂停内部邮件列表发送给所有用户的邮件，直到工作时间后：

```
/^Subject: \[listname\]/
    HOLD
```

这是一个暂停在 MIME 信头中使用单个回车符的消息的模式。这些消息大多是病毒和垃圾邮件，少数例外来自损坏的 Windows SquirrelMail 安装：

```
/\r/
    HOLD Lone CR in headers indicates virus or spam!
```

### 移除信头

如果你想从信头中移除行，请使用 IGNORE 操作。你可以用它来隐藏写入信头的信息，例如你使用的 MUA 类型，或者修剪内部邮件服务器、防火墙或病毒扫描器可能添加的 Received 信头。下面这个移除了 Postfix 通过 content_filter 指令委托电子邮件执行某项操作的程序（例如来自 amavisd-new）添加的 Received 信头：

```
/^Received: from localhost/
    IGNORE
```

下面这个移除了 Sender 信头——某些版本的 Outlook 在回复包含此信头的邮件时行为异常：

```
/^Sender:/
    IGNORE
```

### 丢弃邮件

Postfix 可以使用 DISCARD 操作静默丢弃邮件。例如，你可能希望某些主题行的邮件被移除而不被任何人注意到。这是一个愚蠢的例子。

```
/^Subject:.*deadbeef/
  DISCARD No dead meat!
```

当 Postfix 丢弃邮件时，它会像往常一样记录操作。例如，你可能会在邮件日志中看到如下内容：

```
Apr  9 23:14:28 mail postfix/cleanup[11580]: BB92B15C009: discard: header Subject: deadbeef
from client.example.com[10.0.0.1]; from=<sender@example.com> to=<recipient@example.com>
proto=ESMTP helo=<client.example.com>: No dead meat!
```

### 重定向邮件

如果信头和正文中的模式匹配，Postfix 可以使用 REDIRECT 操作将邮件重定向到另一个收件人。这是一个说明问题的例子（尽管我们真的不推荐这样做）：

```
/^Subject:.*deadbeef/
  REDIRECT bigbrotheriswatchingyou@example.com
```

在邮件日志中，重定向的邮件将如下所示：

```
Apr  9 23:20:38 mail postfix/smtpd[11873]: 9305215C009: client=client.example.com[10.0.0.1]
Apr  9 23:20:38 mail postfix/cleanup[11865]: 9305215C009: redirect: header Subject: deadbeef
from client.example.com[10.0.0.1]; from=<sender@example.com> to=<recipient@example.com>
proto=ESMTP helo=<client.example.com>: bigbrotheriswatchingyou@example.com
Apr  9 23:20:38 mail postfix/cleanup[11865]: 9305215C009:
message-id=<20040409212038.GK3406@example.com>
Apr  9 23:20:38 mail postfix/qmgr[11857]: 9305215C009: from=<sender@example.com>, size=1111,
nrcpt=1 (queue active)
Apr  9 23:21:08 mail postfix/smtp[11874]: 9305215C009:
to=<bigbrotheriswatchingyou@example.com>,
orig_to=<recipient@example.com>, relay=none, delay=30, status=deferred (connect to example.com
[192.0.34.166]: Connection timed out)
```

### 过滤邮件

Postfix 可以使用 FILTER 操作将邮件路由到 content_filter（参见第 11 章）。例如，你可以根据邮件信头将特定类型的邮件重定向到不同类型的传输服务。

此操作会覆盖你 main.cf 文件中的 content_filter 设置，并要求你配置不同的清理服务器——一个在过滤器之前，一个在过滤器之后。必须在第二个清理服务器中关闭 header_checks 和 body_checks，否则你将创建循环！有关处理此问题的更多信息，请参见第 12 章（查找 no_header_checks、body_checks 和 receive_override_options）。下面第一个模式不会将邮件发送到过滤器，而第二个会。



收件人:.*@example\.org FILTER nofilter:dummy
收件人:.*@example\.com FILTER virusfilter:dummy

> **注意** *请记住这只是一个示例。你不应在生产服务器上使用它！如果一条消息的收件人同时位于两个域中，它将匹配第一个正则表达式，因此永远不会被过滤（第一个匹配项生效）；第二个操作永远不会被执行。*

被过滤的消息会在邮件日志中产生如下记录：

```
Apr  9 23:34:12 mail postfix/cleanup[12543]: 2B97315C0D: filter: header To: nofilter@example.com from client.example.com[10.0.0.1]; from=<sender@example.com> to=<nofilter@example.com> proto=ESMTP helo=<client.example.com>: nofilter:dummy
Apr  9 23:38:00 mail postfix/cleanup[12543]: 2299815C00E: filter: header To: virusfilter@example.com from client.example.com[10.0.0.1]; from=<sender@example.com> to=<virusfilter@example.com> proto=ESMTP helo=<client.example.com>: virusfilter:dummy
```

## 检查 MIME 头

MIME 头适用于消息中附加的文件。默认情况下，系统会使用 `header_checks` 映射来扫描 MIME 头中的模式，除非你定义了一个单独的映射，并使用 `mime_header_checks` 参数告知 Postfix 使用它。

> **注意** *当你希望尽可能保持 `mime_header_checks` 映射简洁，仅在 Postfix 检测到消息中包含附件时才使用 MIME 头模式时，定义单独的映射是合理的。*

首先，你需要创建一个映射文件来保存你的 MIME 头模式。假设你选择了 `/etc/postfix/mime_header_checks`，其内容包含以下检查项：

```
# 按后缀名阻止的文件
/name="(.*)\.(386|bat|bin|chm|cmd|com|do|exe|hta|jse|lnk|msi|ole)"$/
    REJECT Unwanted type of attachment $1.$2
/name="(.*)\.(pif|reg|rm|scr|shb|shm|shs|sys|vbe|vbs|vxd|xl|xsl)"$/
    REJECT Unwanted type of attachment $1.$2
```

在此示例中，Postfix 查找包含 `name="` 的 MIME 头，后跟任意数量的字符，然后是一个字面点号（`.`）。接着是一个括在圆括号中的大型子匹配，其中包含几个由竖线（`|`）分隔的禁止扩展名。正则表达式以字面引号（`"`）结束，并且该引号也必须位于行尾（`$`）。右侧的操作使用了 `REJECT` 之后的可选文本。在此示例中，两个子匹配分别通过 `$1`（第一个子匹配——`(.* )`）和 `$2`（文件扩展名）来引用。

因此，如果有人发送了一个名为 `image.pif` 的附件，那么邮件中的 MIME 头行可能如下所示：

```
filename="image.pif"
```

由此生成的错误消息将是：

```
Unwanted type of attachment image.pif
```

因为 `$1` 等于 `image`，`$2` 等于 `pif`。

现在，将 `mime_header_checks` 参数添加到 `main.cf` 文件中，为其指定映射文件的路径：

```
mime_header_checks = pcre:/etc/postfix/mime_header_checks
```

重新加载 Postfix 后，`mime_header_checks` 参数即可生效。

## 检查附加消息中的头

Postfix 可以对附加在其他消息内部的消息中的头应用单独的操作。默认情况下，任何 `header_checks` 参数都会处理这些头，但如果你希望创建一个单独的映射（以节省 CPU 周期或创建例外），可以使用 `nested_header_checks` 参数来定义一个单独的映射。

与其他类型的检查一样，你应该创建一个单独的映射文件，例如 `/etc/postfix/nested_header_checks`，来保存你的检查项。以下是一个示例，用于记录嵌套头中的消息 ID：

```
/^Message-Id:/ WARN Nested Message-Id:
```

现在，将 `nested_header_checks` 参数添加到你的 `main.cf` 文件中：

```
nested_header_checks = pcre:/etc/postfix/nested_header_checks
```

重新加载 Postfix 后，你应该能够找到如下日志条目：

```
Apr 14 13:17:55 mail postfix/cleanup[32397]: 59C3115C02A: warning: header Message-ID: <DIDL27HL1L4H87CA@example.com> from mgate22.so-net.ne.jp[210.139.254.169]; from=<recipient@example.com> to=<recipient@example.com> proto=ESMTP helo=<mgate22.so-net.ne.jp>: Nested Message-Id:
```

> **注意** *本节中的示例并非非常实用，因为我们和邮件列表都无法想到一个真实的应用场景。如果你需要 `nested_header_checks`，你可能已经知道了。*

## 检查邮件正文

当你需要检测正文部分中的某个模式以触发操作时，扫描邮件正文部分非常有用。与其他检查一样，你可以使用 `body_checks` 参数结合一个包含模式和相应操作的映射来检查内容。

> **注意** *正文检查适用于所有消息，包括传入和传出的消息，以及所有发件人和收件人。因此，它们也适用于发送给 `abuse` 和 `postmaster` 的邮件。如果你实施了垃圾邮件检查，那么人们投诉声称从你的网络发送的垃圾邮件时，如果他们的投诉包含他们收到的原始垃圾邮件，他们将无法联系到 `abuse` 和 `postmaster`。在 Postfix 的当前版本中，你无法为某些用户覆盖检查。*

首先创建通常的映射文件，例如 `/etc/postfix/body_checks`。以下是一些模式和操作：

```
# 跳过 base 64 编码块。这可以节省大量 CPU 周期。
# 由 Liviu Daia 编写，Victor Duchovni 修改的表达式。
~^[[:alnum:]+/]{60,}\s*$~     OK
```

上述模式匹配 base64 编码块。请注意，这里使用波浪号（`~`）而不是通常的斜杠（`/`）来分隔正则表达式，这样就无需转义正则表达式内部的斜杠。以下是一些包含已知且独特的垃圾邮件消息模式的示例；Postfix 将拒绝它们：

```
# 垃圾邮件
/(AS SEEN ON NATIONAL TV|READ THIS E-MAIL TO THE END)/
    REJECT Spam #1
/We are shanghai longsun electrical alloy/
    REJECT Chinese spammer from hell
/Do you want EVERYONE to know your business/
    REJECT Spam #2
/(Zainab|San?ni) Abacha/
    REJECT Nigeria spam
/MILITARY HEAD OF STATE IN NIGERIA/
    REJECT Nigeria fraud spam
/antivirus\.5xx\.net/
    REJECT Virus hoax (0190-dialer)
/MOSE CHUKWU/
    REJECT Business fraud spam #1
/Ahmed Kabbah/
    REJECT Business fraud spam #2
/Godwin Igbunu/
    REJECT Business fraud spam #3
/I PRESUME THIS EMAIL WILL NOT BE A SURPRISE TO YOU/
    REJECT Business fraud spam #4
/http:\/\/www\.a1-opportunity4u\.com\/euro2/
    REJECT Business fraud spam #5
/http:\/\/66.151.240.30\//
    REJECT Spam of the worst kind
/http:\/\/members.tripod.com.br\/lev3irkd/
    REJECT Spam of the worst kind II
```

包含以下模式的消息将被拒绝；信封发件人将收到一条指向骗局数据库的退信消息。

```
# 骗局
/jdbgmgr\.exe/
    REJECT Virus hoax!
/ready to dictate a war/
    REJECT Hoax: http://www.tu-berlin.de/www/software/hoax/unicwash.shtml
/inquiries@un\.org/
    REJECT Hoax: http://www.tu-berlin.de/www/software/hoax/unicwash.shtml
/UNO is ready to receive signatures/
    REJECT Hoax: http://www.tu-berlin.de/www/software/hoax/unicwash.shtml
/Third World War/
    REJECT Hoax: http://www.tu-berlin.de/www/software/hoax/unicwash.shtml
```

有时，你可能希望在邮件病毒扫描程序尚未识别出病毒时，使用 `body_checks` 作为拒绝恶意消息的临时措施。请记住，一旦你的扫描程序能够处理该病毒，请立即移除该模式：

```
# 病毒
# Win32.Netsky.V
/The processing of this message can take a few minutes\.\.\./
    REJECT Win32.Netsky.V
/Converting message. Please wait\.\.\./
    REJECT Win32.Netsky.V
/Please wait while loading failed message\.\.\./
    REJECT Win32.Netsky.V
/Please wait while converting the message\.\.\./
    REJECT Win32.Netsky.V
```

将映射文件放置到位后，将 `body_checks` 参数添加到你的 `main.cf` 文件中：

```
body_checks = regexp:/etc/postfix/body_checks
```

与之前一样，你需要重新加载 Postfix 以激活正文检查。



# 11 外部内容过滤器的工作原理

> 接收时宜宽，发送时宜严。
> ——Jon Postel，互联网先驱（1943–1998）

![](img/852c79f689feb77c5fde686b993808b1_157_0.png)

前面章节描述的内置过滤器旨在解决简单的问题；更复杂的过滤必须委托给外部软件来完成。

你可以让 Postfix 在消息入队之前或之后运行内容检查应用程序。当邮件在入队前被过滤时，Postfix 可以将通知发件人的责任留给客户端。当邮件在入队后被过滤时，责任则由 Postfix 承担。

本章概述了委托处理的过程。你将了解如何配置 Postfix 守护进程架构，将消息发送给外部过滤机制，以及如何让消息在成功过滤后重新进入 Postfix 系统以完成最终投递。

外部内容过滤器接续了内置头部和正文过滤器的工作；它们不仅允许外部应用程序检查和拒绝消息，还允许应用程序修改消息内容。以下是过滤器的一些典型任务：

- 添加免责声明
- 扫描病毒和蠕虫
- 检测垃圾邮件
- 归档邮件

Postfix 有两种过滤机制，分别名为 `content_filter` 和 `smtpd_proxy_filter`，它们的设计思路相似，但在能力和内容处理方式上有所不同。表 11-1 列出了两种过滤器之间的差异。

**表 11-1：过滤器差异**

| 过滤器名称 | 传输方式 | 拒绝行为 |
|---|---|---|
| content_filter | smtp、lmtp、pipe | 入队后拒绝 |
| smtpd_proxy_filter | smtp | 入队前拒绝 |

本章将详细解释这些差异，帮助你决定哪种过滤器类型最适合你的场景。

## 过滤内容的最佳时机是什么时候？

RFC 互联网标准规定，邮件服务器*必须*在 SMTP 会话的 DATA 阶段结束之前决定接受还是拒绝消息。不幸的是，这留给邮件服务器检查消息内容的时间非常有限，因为邮件客户端实现了一个相对较短的超时机制，以防止与故障邮件服务器通信时陷入阻塞。例如，Postfix SMTP 客户端超时由 `smtp_data_done_timeout` 参数定义，该参数非常宽容，默认值为 600s。

如果邮件服务器在客户端超时*之前*完成了内容检查，一切正常运行，因为服务器可以通知客户端其关于是否接受消息的决定。然而，如果服务器太慢，客户端就会离开并在稍后重试，而下一次尝试很可能同样不会成功。

Postfix 的 `content_filter` 实现通过不同的方式处理内容检查，从而避免了此类问题：

1. 邮件客户端在 DATA 阶段发送内容。
2. Postfix 服务器接受消息并将其加入队列。客户端认为传输成功。
3. 队列管理器检查邮件，并根据 `content_filter` 条目安排投递。
4. Postfix 将消息交给外部应用程序。
5. 外部应用程序负责投递消息。外部应用程序可以对消息执行以下任一操作：
   - 接受消息并将其交回 Postfix 进行投递。
   - 接受消息并将其交给另一个应用程序或服务器。
   - 丢弃或退回消息。

第二种过滤器（`smtpd_proxy_filter`）以不同的方式处理邮件：

1. 邮件客户端在 `DATA` 阶段发送内容。
2. Postfix 的 `smtpd` 守护进程将 SMTP 命令和内容代理转发给外部应用程序。
3. 外部应用程序将 SMTP 响应发送回 Postfix 的 `smtpd` 守护进程，然后 `smtpd` 将其传递给邮件客户端。

此过滤器可能遇到邮件客户端超时问题，且无法扩展到大量并发邮件客户端连接。这是因为 `smtpd_proxy_filter` 没有队列机制来调度内容过滤。没有队列机制，外部应用程序需要立即处理 Postfix 接收到的每条消息。因此，如果外部应用程序无法像消息到达那样快速完成工作，就可能出现严重的性能下降。这在垃圾邮件检测或病毒扫描应用程序中很可能是问题，因为这些应用通常需要耗时地解包和解码附件。

两种方式都有缺点：

- `content_filter` 会产生额外的流量，因为 Postfix 在处理之前先接受了消息。如果过滤应用程序决定拒绝消息，后续可能会产生退回邮件。
- `smtpd_proxy_filter` 可以尽早拒绝不需要的内容，但它的扩展性不好，可能不够快以完成任务。

## 过滤器与地址重写

在重写邮件头部中的地址时，你需要考虑在哪里应用过滤器。特别是，你需要决定是在过滤之前还是之后让 Postfix 重写地址（例如，由于 `virtual_alias_maps`）。

如果你选择在过滤之前重写地址，就有可能在退回邮件和警告中使用内部地址。例如，发送给 `moe_helden@example.com` 的消息所引起的警告，可能会以 `mh123@mailbox.example.com` 这样的地址被退回。

因此，我们认为你应该让 Postfix（通过 `virtual_alias_maps` 或 `canonical_maps`）在邮件重新注入 Postfix 队列以进行最终投递*之后*再重写地址。这允许外部应用程序（如病毒扫描器）在 Postfix 重写地址之前看到原始收件人并生成适当的警告。

有两种方法可以在过滤前禁用地址映射（虚拟别名扩展、规范映射、地址伪装等）。一种方法是在 `main.cf` 中设置以下选项：

```
receive_override_options = no_address_mappings
```

你也可以在 `master.cf` 中仅为接受网络邮件的守护进程（通常是 `smtpd`）关闭地址重写：

```
smtp     inet  n       -       n       -       -      smtpd
  -o content_filter=foo:[127.0.0.1]:54321
  -o receive_override_options=no_address_mappings
  ...
```

过滤器处理完消息后，消息通常会被重新注入 Postfix 队列。这是执行地址操作的正确时机，为此你需要一个额外的 `smtpd` 来接受已过滤的邮件。这个额外的 `smtpd` 将使用 `receive_override_options=no_unknown_recipient_checks`，而不是 `receive_override_options=no_address_mappings` 设置。你将在以下章节中了解更多关于 `content_filter` 和 `smtpd_proxy_filter` 的详细信息。

## content_filter：先入队，后过滤

要配置使用 `content_filter` 机制的邮件服务，你通常需要两个 `smtpd` 实例（参见图 11-1）。第一个 `smtpd` 接受未过滤的消息，并使用 `content_filter` 将消息委托给外部过滤应用程序。第二个 `smtpd` 实例监听来自外部应用程序的连接，以便消息可以重新进入 Postfix 队列系统进行后续处理。

> 注意
> 不要将第二个实例配置为运行第一个实例所运行的 `content_filter` 应用程序。这会创建一个无限循环，Postfix 会将消息发送给过滤应用程序，而消息会回到与之前相同的 Postfix 队列位置。

![](img/852c79f689feb77c5fde686b993808b1_161_0.png)

*图 11-1：使用 `content_filter` 的投递过程*

其工作原理如下：

1. 配置了 `content_filter` 的 `smtpd` 将消息交给队列管理器。
2. 队列管理器将消息交给 `smtp`、`lmtp` 或 `pipe`，以将其投递到外部过滤应用程序。
3. 外部过滤应用程序接管消息并进行处理。
4. 如果过滤程序将消息重新注入 Postfix，它会连接到一个配置为不使用 `content_filter` 的 Postfix `smtpd`。
5. 第二个 `smtpd` 将消息交给队列管理器。
6. Postfix 在本地投递消息或将其传输到另一台邮件服务器。

除了消息本身，Postfix 还可以向外部过滤应用程序发送额外的信息以辅助处理。具体信息取决于 Postfix 用来向应用程序发送消息的守护进程（`lmtp`、`smtp` 或 `pipe`）。

## 过滤委托守护进程

使用 `content_filter` 时，你有三种基本的守护进程可供选择，用于将邮件委托给外部过滤应用程序。这些守护进程在功能和传输能力上有所不同。以下是概览：

### pipe

`pipe` 守护进程将消息发送给脚本和其他可执行程序。它们可以触发几乎任何可想象的操作，从归档消息到对消息内容执行其他类型的自动化工作，如病毒检测。

这些程序所执行的任务范围广泛，因此需要将多个参数和标志与消息一起传递给过滤程序。你可以在 `pipe(8)` 手册页中了解这些参数。

### smtp

你可以使用 Postfix 的 `smtp` 守护进程通过 SMTP 或 ESMTP 将消息传输给过滤应用程序（例如，发送给另一台 MTA）。随消息一起发送的信息受协议限制；`smtp(8)` 手册页中有更多详情。

### lmtp

Postfix 的 `lmtp` 守护进程也可用于通过 LMTP 协议向过滤程序发送消息。与 SMTP 客户端一样，LMTP 协议限制了可以随消息一起传输的额外信息量，你可以在 `lmtp(8)` 手册页中了解相关信息。



> **注意** *与当前未实现投递状态通知（DSN）以生成单独通知的 Postfix SMTP 客户端不同，LMTP 协议允许服务器为每条消息发送按收件人的状态报告（即，针对每个收件人报告消息是被拒绝还是被接受）。这使得在消息对某些收件人投递成功但对另一些投递失败时，可以避免产生令人困惑的多收件人状态通知。*

## 配置 content_filter 的基础知识

要使用 `content_filter` 将消息发送到外部过滤程序，你需要修改所有处理传入邮件的守护进程的行为。具体来说，你需要完成以下步骤：

1. 在 `main.cf` 文件中将一个传输定义为 `content_filter`。
2. 在 `master.cf` 文件中配置该传输。
3. 如果你希望在过滤后将消息送回 Postfix 队列，则需要在 `master.cf` 中配置额外的重注入路径。

#### 定义传输

要告诉 Postfix 必须将消息交给外部应用程序，请在 `main.cf` 文件中使用 `content_filter`。你必须指示 Postfix 将所有消息传输到一个（待创建的）Postfix 服务，该服务负责等待并将消息交给过滤应用程序。例如，以下代码行告诉 Postfix 将消息发送到名为 foo 的传输，通过 localhost（127.0.0.1）上的端口 54321。请注意，方括号可防止 Postfix 为 127.0.0.1 查询 MX 记录：

```
content_filter = foo:[127.0.0.1]:54321
```

### 配置传输

接下来，你需要在 `master.cf` 中配置刚刚在 `main.cf` 中创建的传输服务。传输服务的配置文件是 `master.cf`，因为主守护进程需要了解所有可用的服务。对于新的传输服务，你需要向主守护进程提供以下信息：

1. 服务的名称。
2. 将执行传输操作的 Postfix 守护进程程序的名称。
3. 程序执行任务所需的选项和其他信息。

以下是基于 foo 传输的示例：

```
# ==========================================================================
# service type  private unpriv chroot wakeup maxproc command
# (yes)  (yes)   (yes) (never) (100)
# ==========================================================================
...
foo     unix    -       -       n       -       2       smtp
        -o smtp_data_done_timeout=1200s
        -o disable_dns_lookups=yes
...
```

以 foo 开头的行是核心传输配置，包含八列。第一列必须与你在 `main.cf` 中定义的传输名称匹配。命令列包含将消息发送到过滤应用程序的命令（此处为 Postfix SMTP 客户端）。随后的两行是该命令的选项。

> **注意** *命令选项语法：* 在列出额外的命令参数时，每一行新参数的开头都要添加空白字符，因为空白字符开头的行会延续逻辑行。但是，你应该去掉参数和值之间的空白字符（例如 `smtp_data_done_timeout` 和 `1200s` 之间）；否则主守护进程将无法识别你的配置。

到目前为止一切正常——你已经可以将消息传输到外部应用程序了。但是，如果要让应用程序将消息交还给 Postfix，你需要配置一个重注入路径。

### 配置额外的重注入路径

重注入路径本质上是一种本地 Postfix 注入方式（如 SMTP、LMTP 或通过 sendmail 本地提交），它不使用 `content_filter`。它通常是另一个 `smtpd` 守护进程实例，使用特殊选项运行以覆盖 `main.cf` 文件中设置的全局参数。例如，如果你希望一个额外的 `smtpd` 重注入路径守护进程监听端口 10025，可以在 `master.cf` 文件中添加以下内容：

```
# ==========================================================================
# service type  private unpriv  chroot  wakeup  maxproc command
# (yes)   (yes)   (yes)   (never) (100)
# ==========================================================================
...
127.0.0.1:10025   inet    n       -       n       -       -       smtpd
        -o content_filter=
        -o receive_override_options=no_unknown_recipient_checks
        -o smtpd_recipient_restrictions=permit_mynetworks,reject
        -o mynetworks=127.0.0.0/8
...
```

请注意，这次传输类型是 `inet`，用于 Internet 传输（前面的示例是 Unix 域套接字传输类型）。

你可以将 Internet 服务指定为 host:port，而无需先在 main.cf 文件中定义传输（主机可以是主机名或 /etc/hosts 中定义的 IP 地址，而端口可以是数字或 /etc/services 文件中定义的服务名称）。
你可以省略 host:，但这会使服务在 inet_interfaces 定义的所有网络接口上可用。为了最大限度地降低重注入路径成为开放中继的风险，你应该将监听的网络接口限制为仅需要的接口，在此情况下只需 localhost/127.0.0.1。

以下是其他命令选项的说明：

- 显式设置为空的 content_filter 会禁用 main.cf 文件中的过滤传输，从而避免陷入无限过滤循环。
- receive_override_options 设置会禁用针对 local_recipient_maps 和 relay_recipient_maps 的收件人检查——因为这些检查已经由从 Internet 接收邮件的 smtpd 守护进程执行过了，无需再次执行。
- 最后两个参数协同工作，首先仅允许来自 mynetworks 参数的邮件，然后将 mynetworks 参数显式设置为 127.0.0.0/8。这是防止外部主机将你的重注入路径作为开放中继的额外安全措施。

## smtpd_proxy_filter：先过滤，后排队

要使用 `smtpd_proxy_filter` 机制，你需要修改现有的 `smtpd` 守护进程（过滤前的 `smtpd`），使其将来自邮件客户端的连接代理到外部过滤程序（参见图 11-2）。

> 注意：Postfix 的 `smtpd` 通过过滤掉管道传输、过长参数以及来自连接的异常字符等潜在有害内容，来保护外部应用程序。

根据你使用的过滤应用程序及其用途，你可能还需要创建第二个 `smtpd` 实例（过滤后的 `smtpd`），用于监听由外部过滤应用程序发回的消息。
其工作原理如下：

1. 过滤前的 `smtpd` 守护进程连接到外部应用程序。
2. `smtpd` 守护进程将传入的 SMTP 命令和数据代理到外部应用程序。
3. 外部过滤应用程序在处理消息内容时保持连接打开。
4. 如果过滤应用程序接受该消息，它可以将消息注入过滤后的 `smtpd` 守护进程或发送到另一个应用程序。
5. 在决定接受还是拒绝消息后，外部过滤应用程序向过滤前的 `smtpd` 发送 SMTP 响应（如 250 OK 或 554 Reject）。
6. 过滤前的 `smtpd` 守护进程将这些响应代理到原始邮件客户端。

![透传代理的投递过程](img/852c79f689feb77c5fde686b993808b1_166_0.png)

*图 11-2：透传代理的投递过程*

## 代理过滤的注意事项

使用 `smtpd_proxy_filter` 时，请注意以下几点：

### ESMTP 通信

当将消息发送到过滤器时，Postfix 使用 ESMTP 协议，但不使用命令管道传输。Postfix 的 `smtpd` 会生成自己的 EHLO、XFORWARD（用于记录远程客户端的 IP 地址而非 localhost[127.0.0.1]）、DATA 和 QUIT 命令。除此之外，Postfix 只是转发从过滤前的 `smtpd` 获取的、来自远程邮件客户端的未修改的 MAIL FROM 和 RCPT TO 命令副本。

### 外部应用程序要求

过滤器（*必须*使用 SMTP 协议）应接受与 Postfix `smtpd` 相同的 MAIL FROM 和 RCPT TO 命令语法。

### 内容重注入

过滤应用程序应将来自过滤前的 `smtpd` 的未修改 SMTP 命令传递给过滤后的 Postfix `smtpd`（后者通常监听非标准端口，在不受相同过滤器约束的路径上进行重注入；这与本章前面讨论的 `content_filter` 机制类似）。

### 拒绝内容

如果过滤器拒绝内容，它应向过滤前的 Postfix `smtpd` 发送否定 SMTP 响应（5xx 代码），然后中止与过滤后的 Postfix `smtpd` 的连接，而不完成与过滤后的 Postfix `smtpd` 的 SMTP 会话。否则，过滤后的 `smtpd` 可能会意外投递消息。

## 配置 `smtpd_proxy_filter` 的基础知识

要使用 `smtpd_proxy_filter` 将消息发送到外部过滤器，你需要修改 `smtpd` 守护进程的行为。以下两个步骤是必要的：

1. 修改现有的 `smtpd`。在本节中，我们将此守护进程称为过滤前的 `smtpd`。
2. 配置一个额外的 `smtpd` 实例，将邮件重新注入 Postfix 队列；即过滤后的 `smtpd`。

### 修改现有的 `smtpd`（过滤前的 `smtpd`）

要使现有的 `smtpd` 代理连接到过滤应用程序，请在 `master.cf` 文件中的 `smtpd` 服务中添加 `smtpd_proxy_filter` 参数。你必须提供代理的 IP 地址或 FQDN 以及端口。

以下是一个使用本地主机端口 10024 的示例：

```
#=================================================================
# service type        private unpriv chroot wakeup maxproc command
# (yes)   (yes)  (yes) (never) (100)
# =================================================================
...
smtp      inet  n       -       n       -       20      smtpd
    -o smtpd_proxy_filter=localhost:10024
```

### 配置额外的 smtpd 重新注入实例（过滤后 smtpd）

要在本地主机上创建另一个接收已过滤消息的 smtpd 实例，你需要在 `master.cf` 文件中添加另一行。它的配置与默认的 smtpd 类似，但会监听不同的端口，并且不应设置与过滤前 smtpd 相同的代理过滤选项。以下是监听端口 10025 的过滤后 smtpd 示例：

```
#=================================================================
# service type        private unpriv chroot wakeup maxproc command
# (yes)   (yes)  (yes) (never) (100)
# =================================================================
...
127.0.0.1:10025   inet n       -       n       -       -       smtpd
    -o smtpd_authorized_xforward_hosts=127.0.0.0/8
    -o smtpd_client_restrictions=
    -o smtpd_helo_restrictions=
    -o smtpd_sender_restrictions=
    -o smtpd_recipient_restrictions=permit_mynetworks,reject
    -o mynetworks=127.0.0.0/8
    -o receive_override_options=no_unknown_recipient_checks
    -o content_filter=
```

# 12

## 使用外部内容过滤器

> 我知道去哪里弄，如果你想要的话。
> ——蒙提·派森《布莱恩的一生》中的狱卒 #1

每个工具都有其用途。想象一下，你试图开发一把既能当锤子用又能用来抛光的工具。最终你很可能得到的是一把糟糕的锤子*和*一个糟糕的抛光器。这就是 Postfix 不做垃圾邮件过滤、邮件归档或邮件净化的原因。相反，它为你提供了将最好的外部过滤器接入最好的 MTA 的机会。在前面的章节中，你已经看到 Postfix 为过滤邮件提供了略有不同的方法，这些方法在处理传入消息的时间上有所不同。本章将介绍这些方法的实践应用。

你将具体了解如何通过将消息传送给脚本来为消息附加免责声明，以及如何使用 `content_filter` 或 `smtpd_proxy_filter` 将消息发送到 amavisd-new 进行病毒扫描。

## 使用脚本为消息附加免责声明

在 `content_filter` 脚本可以实现的众多功能中，其中之一就是为所有外发消息添加免责声明。以下示例使用 alterMIME（一个用于修改 MIME 编码邮件的小程序）在脚本中为从内部客户端发送的每条消息添加免责声明。图 12-1 展示了 alterMIME 如何集成到消息传输过程中。

要在不处理入站和本地消息的情况下为出站消息添加免责声明，你需要将不同方向的流量分开。假设你的邮件服务器为内部和外部网络分别配置了独立的网络接口。这意味着你需要创建三个独立的 smtpd 实例，并将它们分别绑定到本地主机、内部和外部网络接口。以下示例展示了如果你为不同的网络接口创建了独立的 smtpd 实例，从内部网络到远程目的地的消息传输将如何被处理。

1. 当消息离开你的网络时，邮件客户端连接到监听内部接口的 `smtpd` 实例。
2. 该内部 `smtpd` 接受消息并将其发送到 `qmgr`。
3. `qmgr` 将消息发送到 `content_filter` 服务。
4. `content_filter` 服务使用 pipe 守护进程将消息传递给脚本。
5. 脚本添加免责声明。
6. 脚本将消息重新注入到监听本地网络接口的 `smtpd` 实例。
7. 本地 `smtpd` 将重新注入的消息发送到 `qmgr`。
8. `qmgr` 将消息发送到 `smtp` 并传输到互联网。

然而，在配置传输之前，你必须先创建从 Postfix 中调用 alterMIME 的脚本。

### 安装 alterMIME 并创建过滤脚本

该脚本将运行 alterMIME（http://www.pldaniels.com/altermime）来修改外发消息。如果你没有安装 alterMIME（并且你的操作系统没有二进制安装包），请下载并解压它，切换到源代码目录，然后运行 `make` 和 `make install`。完成后，你将在 `/usr/local/bin/altermime` 中拥有 alterMIME 可执行文件。

#### 创建 alterMIME 环境

你应该以非特权系统用户身份运行 alterMIME。例如，如果你想在机器上使用 `filter` 用户名，可以运行以下命令来创建该用户：

```
# groupadd filter
# useradd -d /var/spool/altermime -G filter altermime
```

#### 创建脚本目录

将一堆脚本堆放在 `/etc/postfix` 目录中不是一个好主意。请以超级用户身份创建一个单独的子目录来存放脚本，并设置该子目录仅允许 `filter` 和 `root` 访问。

例如，以下命令序列会创建一个具有正确权限和所有权的目录：

```
# mkdir /etc/postfix/filter
# chown root /etc/postfix/filter
# chgrp filter /etc/postfix/filter
# chmod 770 /etc/postfix/filter
```

#### 创建脚本

以下脚本位于 `/etc/postfix/filter/add_disclaimer.sh`，对来自 Postfix 的传入消息（由 pipe 守护进程发送）调用 alterMIME。alterMIME 程序向消息添加免责声明，然后将其重新注入到 Postfix 队列中。alterMIME 需要一个写入临时文件的位置；它无法直接操作 stdin。

```
#!/bin/sh
# System dependent settings
ALTERMIME=/usr/local/bin/altermime
ALTERMIME_DIR=/var/spool/altermime
SENDMAIL=/usr/sbin/sendmail
# Exit codes of commands invoked by Postfix are expected
# to follow the conventions defined in <sysexits.h>.
TEMPFAIL=75
UNAVAILABLE=69
# Change in to alterMIME's working directory and
# notify Postfix if 'cd' fails.
cd $ALTERMIME_DIR || { echo $ALTERMIME_DIR does not exist; exit $TEMPFAIL; }
# Clean up when done or when aborting.
trap "rm -f in.$$" 0 1 2 3 15
# Write mail to a temporary file
# Notify Postfix if this fails
cat >in.$$ || { echo Cannot write to $ALTERMIME_DIR; exit $TEMPFAIL; }
# Call alterMIME, hand over the message and
# tell alterMIME what to do with it
$ALTERMIME  --input=in.$$ \
           --disclaimer=/etc/postfix/disclaimer.txt \
           --disclaimer-html=/etc/postfix/disclaimer.txt \
           --xheader="X-Copyrighted-Material: Please visit http:// \
           www.example.com/message_disclaimer.html" || \
           { echo Message content rejected; exit $UNAVAILABLE; }
# Call sendmail to reinject the message into Postfix
$SENDMAIL "$@" <in.$$
# Use sendmail's EXIT STATUS to tell Postfix
# how things went.
exit $?
```

创建脚本后，仅授予 root 写入权限，但授予 filter 用户执行权限：

```
# chown root add_disclaimer.sh
# chgrp filter add_disclaimer.sh
# chmod 750 add_disclaimer.sh
```

当然，现在你需要创建脚本中引用的免责声明。

#### 创建免责声明

如果你已经有免责声明文本，请将其放入 `/etc/postfilter/disclaimer/disclaimer.txt`。如果你还在寻找合适的免责声明，可以访问 emaildisclaimers.com（http://www.emaildisclaimers.com），这是一个专门提供免责声明和相关电子邮件法律信息的网站。本示例仅使用以下虚拟文本（来自 http://www.lipsum.com）：

> Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Nam commodo lobortis magna. Quisque neque. Etiam aliquam. Nulla tempor vestibulum.

文本准备好后，仅允许 filter 组读取你的免责声明：

```
# chgrp filter disclaimer.txt
# chmod 640 disclaimer.txt
```

过滤脚本到此就完成了。现在你需要配置 Postfix 来使用该脚本。

### 配置 Postfix 以使用免责声明脚本

配置 Postfix 调用该脚本是一个两步过程：

1. 在 `master.cf` 文件中为对应的 smtpd 定义 `content_filter` 参数。
2. 在 `master.cf` 文件中定义传输。

#### 定义 content_filter 参数

正如第 11 章所解释的，你现在需要在 `main.cf` 中添加 `content_filter` 参数并指定一个传输名称。然而，这将全局指定一个 `content_filter`，过滤器将应用于所有处理传入邮件的进程。在本例中你不希望这样，因为你只想将过滤器应用于来自内部网络接口的消息。

为了仅将过滤器分配给来自内部网络接口的消息，你只需在 `master.cf` 文件中为单个 smtpd 实例添加 `content_filter`。以下 `master.cf` 示例中内部接口的地址是 172.16.0.1：

```
127.0.0.1:smtp inet n - n - - smtpd ❶
172.16.0.1:smtp inet n - n - - smtpd ❷
 -o content_filter=disclaimer:
192.0.34.166:smtp inet n - n - - smtpd ❸
```

❶ 这是本地 smtpd 实例。
❷ 这是监听内部网络接口的 smtpd 实例。
❸ 这是监听外部网络的 smtpd 实例。

注意过滤传输的名称是 disclaimer；这不是脚本名称。你将在下一节中定义该传输。



#### 定义传输

现在你需要在 `master.cf` 文件中定义免责传输。创建一个 `pipe` 传输实例，运行 `add_disclaimer.sh` 脚本。以下是使用本章前面所示脚本的配置方法：

```
disclaimer  unix  -       n       n       -       -       pipe
  flags=Rq user=filter argv=/etc/postfix/filter/add_disclaimer.sh -f ${sender} -- ${recipient}
```

此定义以 `filter` 用户身份运行 `pipe` 守护进程，当收到消息时调用 `add_disclaimer.sh`。同时将信封发件人和信封收件人传递给脚本。`R` 标志会在邮件头部添加包含信封发件人地址的 Return-Path，`q` 标志会对命令行中 `$sender` 和 `$recipient` 参数的空白字符及其他特殊字符进行引用转义。

> 注意 *`pipe(8)` 手册页包含完整的标志和选项列表。*

### 测试过滤器

要测试过滤器，你需要执行以下步骤，各步骤将在后续小节中详细讨论：

- 1. 通过内部网络接口向远程用户发送邮件。
- 2. 检查邮件日志中的过滤器操作记录。
- 3. 检查已发送邮件中是否包含免责声明。

#### 向远程用户发送邮件

要生成一条由 Postfix 发送到过滤器的消息，请使用 telnet 连接到内部网络接口（该接口上的 smtpd 实例应使用过滤器）。以下是示例会话：

```
$ telnet 172.16.0.1 25
Trying 172.16.0.1...
Connected to 172.16.0.1.
Escape character is '^]'.
220 mail.example.com ESMTP Postfix
HELO client.example.com
250 mail.example.com
MAIL FROM: <sender@example.com>
250 Ok
RCPT TO: <recipient@remote-example.com>
250 Ok
DATA
354 End data with <CR><LF>.<CR><LF>
FROM: Sender <sender@example.com>
TO: Recipient <recipient@remote-example.com>
Subject: Testing disclaimer
This is a test. There should be text at the bottom of this message added by a disclaimer script.
.
250 Ok: queued as 3C4D043F2F
QUIT
221 Bye
```

#### 检查邮件日志

邮件日志中应包含过滤器操作的记录，如以下示例所示：

```
Mar 12 01:59:53 mail postfix/smtpd[30206]: connect from client.example.com[172.16.0.2]
Mar 12 02:00:21 mail postfix/smtpd[30206]: 3C4D043F2F: client=client.example.com[172.16.0.2]
Mar 12 02:01:53 mail postfix/cleanup[30209]: 3C4D043F2F: message-id=<20040312010021.3C4D043F2F@mail.example.com>
Mar 12 02:01:53 mail postfix/nqmgr[30193]: 3C4D043F2F: from=<sender@example.com>, size=444, nrcpt=1 (queue active)
Mar 12 02:01:53 mail postfix/pipe[30213]: 3C4D043F2F: to=<recipient@remote-example.com>, relay=disclaimer, delay=92, status=sent (mail.example.com) ①
Mar 12 02:01:53 mail postfix/pickup[30192]: 8421143F2F: uid=100 from=<sender@example.com> ②
Mar 12 02:01:53 mail postfix/cleanup[30209]: 8421143F2F: message-id=<20040312010021.3C4D043F2F@mail.example.com>
Mar 12 02:01:53 mail postfix/nqmgr[30193]: 8421143F2F: from=<sender@example.com>, size=977, nrcpt=1 (queue active)
Mar 12 02:01:55 mail postfix/smtpd[30206]: disconnect from client.example.com[172.16.0.2]
Mar 12 02:02:03 mail postfix/smtp[30220]: 8421143F2F: to=<recipient@remote-example.com>, relay=mail.remote-example.com[212.14.92.89], delay=10, status=sent (250 Ok: queued as 56851E1C65) ③
```

- ① `pipe` 守护进程使用 disclaimer 传输将消息发送到脚本。
- ② 脚本使用原始信封发件人重新注入消息。
- ③ `smtp` 守护进程成功将消息递送给信封收件人。

#### 检查邮件中是否包含免责声明

作为最后（也是相当直观的）一项测试，获取该消息并查看它是否包含 X 头和 alterMIME 应该添加到外发消息上的免责声明。在以下示例中可以看到两者：

```
Return-Path: <sender@example.com>
X-Original-To: recipient@remote-example.com
Delivered-To: recipient@remote-example.com
Received: from mail.example.com (mail.example.com [192.0.34.166])
	by mail.remote-example.com (Postfix) with ESMTP id 56851E1C65
	for <recipient@remote-example.com>; Fri, 12 Mar 2004 02:01:25 +0100 (CET)
Received: by mail.example.com (Postfix, from userid 100)
    id 8421143F2f; Fri, 12 Mar 2004 02:01:53 +0100 (CET)
Received: from client.example.com (client.example.com [172.16.0.2])by
    mail.example.com+(Postfix) with SMTP id 3C4D043F2for
    <recipient@remote-example.com>; Fri, 12 Mar 2004+02:00:21 +0100 (CET)
From: Sender <sender@example.com>
To: Recipient <recipient@remote-example.com>
Subject: Testing disclaimer
Message-Id: <20040312010021.3C4D043F2F@mail.example.com>
Date: Fri, 12 Mar 2004 02:00:21 +0100 (CET)
X-Copyrighted-Material: Please visit http://www.example.com/
    message_disclaimer.html

This is a test. There should be text at the bottom of this message
added by a disclaimer script.
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Nam commodo
lobortis magna. Quisque neque. Etiam aliquam. Nulla tempor vestibulum.
```

## 使用 content_filter 和 amavisd-new 扫描病毒

本节介绍第 11 章中描述的 `content_filter` 的高级用法——如何将流行的程序 amavisd-new 集成到 Postfix 中。amavisd-new 链接 MTA 和一个或多个病毒扫描器或垃圾邮件检测程序（如 SpamAssassin）。该项目正在积极开发中，并且在 Postfix 邮件列表上受到许多邮件管理员的推荐。

> **注意** 要获得病毒扫描功能，除了 amavisd-new 之外，你还需要至少安装一个受支持的病毒扫描器；请查阅文档以了解受支持产品的列表。

图 12-2 展示了 Postfix 和 amavisd-new 如何与其他应用程序（如垃圾邮件检测器和病毒扫描器）协同工作。以下是消息流：

- 1. 邮件客户端向 Postfix 发送消息。
- 2. `smtpd` 接受消息。
- 3. `smtpd` 将消息发送给 `qmgr`。
- 4. `qmgr` 将消息发送给 amavisd-new。
- 5. amavisd-new 将消息发送给其他应用程序（本例中为病毒扫描器）。
- 6. amavisd-new 将消息重新注入到本地 `smtpd`。
- 7. 本地 `smtpd` 将消息发送给 `qmgr`。
- 8. `qmgr` 退信或递送该消息。

![](img/852c79f689feb77c5fde686b993808b1_177_0.png)

图 12-2：使用 content_filter 将 amavisd-new 与 Postfix 集成

### 安装 amavisd-new

要获取 amavisd-new，请从 amavisd-new 网站 (http://www.ijs.si/software/amavisd) 上列出的镜像站点之一下载。解压归档文件后，按照 INSTALL 文件中的步骤为 Postfix 安装 amavisd-new。你还应阅读 README.postfix (http://www.ijs.si/software/amavisd/README.postfix) 文件，以获取针对 Postfix 的最新说明和注意事项。

> 提示 你只需构建 amavisd-new 的守护进程版本。辅助应用程序（如 `amavis(.c)` 和 `amavisd-milter(.c)`）在与 Postfix 配合使用时并非必需。

#### 从 CPAN 为 amavisd-new 安装 Perl 模块

amavisd-new 需要多个 Perl 模块才能正常工作，amavisd-new 的 SOURCE 目录中的 INSTALL 文档包含这些模块的完整列表。安装模块时，你通常可以选择使用发行版提供的软件包，或直接从 CPAN（Comprehensive Perl Archive Network，http://www.cpan.org）下载模块。

> **注意** CPAN 通常是获取最新模块的最佳来源，但为了保持一致性，你可能更愿意选择操作系统自带的软件包。

要从 CPAN 安装模块（如 `Compress::Zlib`），你需要使用 CPAN 模块运行 Perl，如下所示：

```
# perl -MCPAN -e shell;
cpan shell -- CPAN exploration and modules installation (v1.76)
ReadLine support enabled
cpan> install Compress::Zlib
Running install for module Compress::Zlib
Running make for P/PM/PMQS/Compress-Zlib-1.33.tar.gz
Fetching with LWP:
  ftp://ftp-stud.fht-esslingen.de/pub/Mirrors/CPAN/authors/id/P/PM/PMQS/
  Compress-Zlib-1.33.tar.gz
CPAN: Digest::MD5 loaded ok
Fetching with LWP:
  ftp://ftp-stud.fht-esslingen.de/pub/Mirrors/CPAN/authors/id/P/PM/PMQS/
  CHECKSUMS
Checksum for /root/.cpan/sources/authors/id/P/PM/PMQS/Compress-Zlib-
1.33.tar.gz ok
Scanning cache /root/.cpan/build for sizes
Compress-Zlib-1.33/
... lots of building output ...
All tests successful, 1 test skipped.
Files=6, Tests=287, 2 wallclock secs ( 0.73 cusr + 0.11 csys = 0.84 CPU)
  /usr/bin/make test -- OK
Running make install
Installing /usr/lib/perl5/site_perl/5.6.0/i386-linux/auto/Compress/Zlib/
Zlib.so
Files found in blib/arch: installing files in blib/lib into architecture
dependent library tree
Installing /usr/lib/perl5/site_perl/5.6.0/i386-linux/Compress/Zlib.pm
Installing /usr/man/man3/Compress::Zlib.3pm
Writing /usr/lib/perl5/site_perl/5.6.0/i386-linux/auto/Compress/Zlib/.packlist
Appending installation info to /usr/lib/perl5/site_perl/5.6.0/i386-linux/
perllocal.pod
  /usr/bin/make install -- OK
```

安装好所有模块并完成 amavisd-new 的安装后，你应该对其进行测试。

### 测试 amavisd-new

在尝试将 amavisd-new 与 Postfix 集成之前，请先单独对其进行测试，执行以下步骤：

- 1. 以调试模式启动 amavisd-new，查看其是否正常启动。
- 2. 进行网络测试，查看其是否监听网络端口。



# 以调试模式运行 amavisd-new

以调试模式调用 amavisd-new 可以一次性回答以下问题：

- 它能运行吗？amavisd-new 启动需要安装所有必需的 Perl 模块。如果缺少某个模块，你会收到一条错误消息，指示缺少的模块。
- 你能以非特权用户身份运行它吗？amavisd-new 需要一个新的组（默认为 `vscan`）和一个属于该组的用户账户（同样默认为 `vscan`）。
- 它能找到实现附加功能的可选 Perl 模块吗？例如 SpamAssassin、LDAP 和 SQL。
- 它是否使用了正确安装的 Perl？如果你安装了多个版本的 Perl，你可能没有为要使用的特定 Perl 版本安装所有模块。
- 它能找到辅助程序吗？例如病毒扫描器。
- 它使用哪个配置文件？通常是 `/etc/amavisd.conf`，但如果你完全清楚自己在做什么，可以覆盖此设置。
- 它能绑定到配置文件中指定的端口吗？

首次尝试时，最好以交互方式启动 amavisd-new，使其保持附加到终端。为此，切换到 `vscan` 用户并使用调试选项运行 `amavisd-new`。此示例会话显示了你期望看到的输出：

```
# su - vscan
$ /usr/local/sbin/amavisd debug
Jan 28 11:10:43 mail amavisd[29188]: starting. amavisd at mail amavisd-new-20030616-p6
Jan 28 11:10:43 mail amavisd[29188]: Perl version                5.006
Jan 28 11:10:43 mail amavisd[29188]: Module Amavis::Conf           1.15
Jan 28 11:10:43 mail amavisd[29188]: Module Archive::Tar           1.08
Jan 28 11:10:43 mail amavisd[29188]: Module Archive::Zip           1.09
Jan 28 11:10:43 mail amavisd[29188]: Module Compress::Zlib         1.33
Jan 28 11:10:43 mail amavisd[29188]: Module Convert::TNEF          0.17
Jan 28 11:10:43 mail amavisd[29188]: Module Convert::UUlib         1.0
Jan 28 11:10:43 mail amavisd[29188]: Module MIME::Entity            5.404
Jan 28 11:10:43 mail amavisd[29188]: Module MIME::Parser           5.406
Jan 28 11:10:43 mail amavisd[29188]: Module MIME::Tools            5.411
Jan 28 11:10:43 mail amavisd[29188]: Module Mail::Header           1.60
Jan 28 11:10:43 mail amavisd[29188]: Module Mail::Internet          1.60
Jan 28 11:10:43 mail amavisd[29188]: Module Mail::SpamAssassin     2.63
Jan 28 11:10:43 mail amavisd[29188]: Module Net::Cmd               2.24
Jan 28 11:10:43 mail amavisd[29188]: Module Net::DNS               0.40
Jan 28 11:10:43 mail amavisd[29188]: Module Net::SMTP              2.26
Jan 28 11:10:43 mail amavisd[29188]: Module Net::Server            0.86
Jan 28 11:10:43 mail amavisd[29188]: Module Time::HiRes            1.55
Jan 28 11:10:43 mail amavisd[29188]: Module Unix::Syslog           0.99
Jan 28 11:10:43 mail amavisd[29188]: Found myself: /usr/sbin/amavisd -c /etc/amavisd.conf
Jan 28 11:10:43 mail amavisd[29188]: Lookup::SQL code        NOT loaded
Jan 28 11:10:43 mail amavisd[29188]: Lookup::LDAP code       NOT loaded
Jan 28 11:10:43 mail amavisd[29188]: AMCL-in protocol code   loaded
Jan 28 11:10:43 mail amavisd[29188]: SMTP-in protocol code   loaded
Jan 28 11:10:43 mail amavisd[29188]: ANTI-VIRUS code         loaded
Jan 28 11:10:43 mail amavisd[29188]: ANTI-SPAM  code         loaded
Jan 28 11:10:43 mail amavisd[29188]: Net::Server: 2004/01/28-11:10:43 Amavis (type \
Net::Server::PreForkSimple) starting! pid(29188)
Jan 28 11:10:43 mail amavisd[29188]: Net::Server: Binding to UNIX socket file \
/var/amavis/amavisd.sock using SOCK_STREAM
Jan 28 11:10:43 mail amavisd[29188]: Net::Server: Binding to TCP port 10024 on host 127.0.0.1
Jan 28 11:10:43 mail amavisd[29188]: Net::Server: Setting gid to "54322 54322"
Jan 28 11:10:43 mail amavisd[29188]: Net::Server: Setting uid to "7509"
Jan 28 11:10:43 mail amavisd[29188]: Net::Server: Setting up serialization via flock
Jan 28 11:10:43 mail amavisd[29188]: Found $file          at /usr/bin/file
Jan 28 11:10:43 mail amavisd[29188]: Found $arc           at /usr/bin/arc
Jan 28 11:10:43 mail amavisd[29188]: Found $gzip          at /usr/bin/gzip
Jan 28 11:10:43 mail amavisd[29188]: Found $bzip2         at /usr/bin/bzip2
Jan 28 11:10:43 mail amavisd[29188]: Found $lzop          at /usr/local/bin/lzop
Jan 28 11:10:43 mail amavisd[29188]: Found $lha           at /usr/bin/lha
Jan 28 11:10:43 mail amavisd[29188]: Found $unarj         at /usr/bin/unarj
Jan 28 11:10:43 mail amavisd[29188]: Found $uncompress    at /usr/bin/uncompress
Jan 28 11:10:43 mail amavisd[29188]: Found $unfreeze      at /usr/local/bin/unfreeze
Jan 28 11:10:43 mail amavisd[29188]: Found $unrar         at /usr/bin/rar
Jan 28 11:10:43 mail amavisd[29188]: Found $zoo           at /usr/bin/zoo
Jan 28 11:10:43 mail amavisd[29188]: Found $cpio          at /bin/cpio
Jan 28 11:10:43 mail amavisd[29188]: No primary av scanner: KasperskyLab AntiViral Toolkit \
Pro (AVP)
Jan 28 11:10:43 mail amavisd[29188]: No primary av scanner: KasperskyLab AVPDaemonClient
Jan 28 11:10:43 mail amavisd[29188]: No primary av scanner: H+BEDV AntiVir or \
CentralCommand Vexira Antivirus
Jan 28 11:10:43 mail amavisd[29188]: No primary av scanner: Command AntiVirus for Linux
Jan 28 11:10:43 mail amavisd[29188]: No primary av scanner: Symantec CarrierScan via \
Symantec CommandLineScanner
Jan 28 11:10:43 mail amavisd[29188]: No primary av scanner: Symantec AntiVirus Scan Engine
Jan 28 11:10:43 mail amavisd[29188]: No primary av scanner: Dr.Web Antivirus for \
Linux/FreeBSD/Solaris
Jan 28 11:10:43 mail amavisd[29188]: No primary av scanner: F-Secure AntiVirus
Jan 28 11:10:43 mail amavisd[29188]: No primary av scanner: CAI InoculateIT
Jan 28 11:10:43 mail amavisd[29188]: No primary av scanner: MkS_Vir for Linux (beta)
Jan 28 11:10:43 mail amavisd[29188]: No primary av scanner: MkS_Vir daemon
Jan 28 11:10:43 mail amavisd[29188]: No primary av scanner: ESET Software NOD32
Jan 28 11:10:43 mail amavisd[29188]: No primary av scanner: ESET Software NOD32 - \
Client/Server Version
Jan 28 11:10:43 mail amavisd[29188]: No primary av scanner: Norman Virus Control v5 / Linux
Jan 28 11:10:43 mail amavisd[29188]: No primary av scanner: Panda Antivirus for Linux
Jan 28 11:10:43 mail amavisd[29188]: Found primary av scanner NAI McAfee AntiVirus (uvscan) \
    at /usr/local/bin/uvscan
Jan 28 11:10:43 mail amavisd[29188]: No primary av scanner: VirusBuster
Jan 28 11:10:43 mail amavisd[29188]: No primary av scanner: CyberSoft VFind
Jan 28 11:10:43 mail amavisd[29188]: No primary av scanner: Ikarus AntiVirus for Linux
Jan 28 11:10:43 mail amavisd[29188]: No primary av scanner: BitDefender
Jan 28 11:10:43 mail amavisd[29188]: No secondary av scanner: Clam Antivirus - clamscan
Jan 28 11:10:43 mail amavisd[29188]: No secondary av scanner: FRISK F-Prot Antivirus
Jan 28 11:10:43 mail amavisd[29188]: No secondary av scanner: Trend Micro FileScanner
Jan 28 11:10:43 mail amavisd[29188]: SpamControl: initializing Mail::SpamAssassin
```

1.  这一行指示了 Perl 版本。
2.  这一行及其后续行表明没有 SQL 或 LDAP 代码存在。
3.  这一行表明反垃圾邮件代码已加载；仅当 SpamAssassin 或 dspam 存在时才会成功。
4.  这一行及其前面的行表明已找到各种外部解包程序——从而使 amavisd-new 能够解压缩用这些打包程序压缩的附件。
5.  这一行表明 McAfee AntiVirus 已存在。
6.  此时，amavisd-new 已准备就绪。

#### 测试网络连接

在独立的 amavisd-new 仍在运行的情况下，你现在应该检查它是否接受连接。使用 telnet 会话来测试 ESMTP 和 LMTP 两种替代方案。

#### 测试 ESMTP 可用性

打开到本地端口 10024（amavisd-new 的默认端口）的 telnet 连接。你应该检查它是否正在监听该端口并响应 ESMTP 命令。amavisd-new 应该对 EHLO 命令做出响应，并返回一组可用的命令，如以下示例会话所示：

```
# telnet localhost 10024
220 [127.0.0.1] ESMTP amavisd-new service ready
EHLO mail.example.com
250-[127.0.0.1]
250-PIPELINING
250-SIZE
250-8BITMIME
250 ENHANCEDSTATUSCODES
QUIT
221 2.0.0 [127.0.0.1] (amavisd) closing transmission channel
```



#### 测试 LMTP 可用性

接下来，你需要检查 amavisd-new 是否正在监听本地端口 10024（amavisd-new 用于 LMTP 的默认端口）并能响应 LMTP 命令。你应该能够运行一个 LHLO 命令，如下会话所示：

```
# telnet localhost 10024
220 [127.0.0.1] ESMTP amavisd-new service ready
LHLO mail.example.com
250-[127.0.0.1]
250-PIPELINING
250-SIZE
250-8BITMIME
250 ENHANCEDSTATUSCODES
QUIT
221 2.0.0 [127.0.0.1] (amavisd) closing transmission channel
```

### 优化 amavisd-new 性能

如果你接收的邮件量很大，你可能希望调整 amavisd-new 的性能。由于 amavisd-new 大量使用文件系统来为消息的进一步检查做准备，其性能可能受限于磁盘 I/O 的速度和延迟。通过将此准备过程转移到 RAM 磁盘样式的文件系统，你可以显著优化读写操作速度。以下各节描述的过程使用的是 Linux 临时文件系统类型（tmpfs）。

#### 这样安全吗？

请放心，由于你将 amavisd-new 集成到 Postfix 中的方式，在过滤过程中你不会丢失任何邮件。来看看过滤过程中发生了什么：

1.  收到新消息后，Postfix 队列管理器会向一个 Postfix SMTP 或 LMTP 客户端发送邮件投递请求；该客户端将消息传输到 amavisd-new。
2.  amavisd-new 开始处理该消息（进行扫描、垃圾邮件检查等），但它不会立即确认已收到该消息。
3.  在等待 amavisd-new 的过程中，Postfix 将消息保留在其队列中，等待 amavisd-new 通知它消息已正确接收。
4.  amavisd-new 完成工作后，会将消息重新注入回 Postfix 队列。
5.  处理重新注入的 Postfix smtpd 从 amavisd-new 接受消息。
6.  在从重新注入的 smtpd 收到确认后，amavisd-new 向发起的 Postfix lmtp 或 smtp 客户端确认传输成功，后者继而向队列管理器报告消息已投递。

正如你所见，amavisd-new 只有在后过滤 smtpd 接受了已处理的消息后，才会告知前过滤的 Postfix 组件它已收到消息。这样，你就永远不会在 amavisd-new 中丢失邮件。

#### 计算 tmpfs 大小

要计算 tmpfs 的正确大小，请考虑以下情况：如果你运行 *n* 个 amavisd-new 实例，并且每个实例最多接受 `message_size_limit` 大小的消息，你需要以下空间：

```
n * (1 + maximum_expected_expansionfactor) * message_size_limit * 7/8
```

扩展因子比较复杂，但使用 2 的因子是相当合适的（压缩消息——例如 *.zip 或 *.rar 文件——可能会膨胀到原始大小的两倍）。

例如，如果你有五个 amavisd-new 实例和一个 10MB 的消息限制，你将得到以下 tmpfs 大小的计算结果：

```
5 * (1 + 2) * 10MB * 7/8 = 131.25MB
```

> **注意** *请确保你有足够的物理内存来容纳 tmpfs；否则，你的机器将开始将内存交换到磁盘，最终性能可能会比使用常规文件系统更差。*

#### 配置优化

设置 amavisd-new 使用 tmpfs 涉及以下几个步骤：

1.  找到 amavisd-new 的 `$TEMPBASE` 参数。
2.  创建一个 tmpfs 文件系统。
3.  停止 amavisd-new。
4.  挂载 tmpfs 文件系统。
5.  启动 amavisd-new。
6.  确保 amavisd-new 仍然正常工作。

首先，你需要找出 amavisd-new 的 `$TEMPBASE` 定义在哪里。这将是你即将创建的 tmpfs 的挂载点。默认的 `$TEMPBASE` 是 `$MYHOME`，其默认值为 `/var/amavis`。要确切找出，可以在你的配置文件上使用 grep。这个例子显示它被设置为 `$MYHOME`：

```
# grep TEMPBASE /etc/amavisd.conf
$TEMPBASE = $MYHOME;        # (must be set if other config vars use is)
$ENV{TMPDIR} = $TEMPBASE;    # wise, but usually not necessary
    "-f=$TEMPBASE {}", [0,8], [3,4,5,6], qr/infected: ([^\r\n]+)/ ],
# adjusting /var/amavis above to match your $TEMPBASE.
# directory $TEMPBASE specifies) in the 'Names=' section.
```

运行另一个 grep 来找出 `$MYHOME` 是什么。在下面的例子中，你可以看到 `$MYHOME` 的定义被注释掉了，所以它使用的是默认值：

```
# grep MYHOME /etc/amavisd.conf
# $MYHOME serves as a quick default for some other configuration settings.
# $MYHOME is not used directly by the program. No trailing slash!
#$MYHOME = '/var/lib/amavis';  # (default is '/var/amavis')
$TEMPBASE = $MYHOME;      # (must be set if other config vars use is)
#$TEMPBASE = "$MYHOME/tmp"; # prefer to keep home dir /var/amavis clean?
#$helpers_home = $MYHOME;    # (defaults to $MYHOME)
#$daemon_chroot_dir = $MYHOME; # (default is undef, meaning: do not chroot)
#$pid_file  = "$MYHOME/amavisd.pid"; # (default is "$MYHOME/amavisd.pid")
#$lock_file = "$MYHOME/amavisd.lock"; # (default is "$MYHOME/amavisd.lock")
#$forward_method = "bsmtp:$MYHOME/out-%i-%n.bs";
$unix_socketname = "$MYHOME/amavisd.sock"; # amavis helper protocol socket
                                          # (usual setting is $MYHOME/amavisd.sock)
$LOGFILE = "$MYHOME/amavisd.log";  # (defaults to empty, no log)
 "{}" -ss -i '*' -log=$MYHOME/vbuster.log", [0], [1],
```

现在你需要在 /etc/fstab 文件中创建一个 tmpfs 条目，使用上一节（“计算 tmpfs 大小”）中计算出的文件系统大小。以下示例使用了 150MB 的大小，并限制对特定用户和组的访问。在此例中，用户 ID 为 7509，组 ID 为 54322，它们与 /etc/passwd 和 /etc/group 文件中的用户和组 vscan 相匹配；请记住，你的系统几乎肯定有不同的数字，你需要自行查找：

```
/dev/shm    /var/amavis  tmpfs defaults,size=150m,mode=700,uid=7509,gid=54322 0 0
```

在你挂载 /var/amavis 之前，请确保使用如下命令停止 amavisd-new：

```
# /etc/init.d/amavisd-new stop
```

接下来，挂载 /var/amavis（记住这是你刚刚在 /etc/fstab 中定义的 tmpfs 文件系统）：

```
# mount /var/amavis
```

现在再次启动 amavisd-new：

```
# /etc/init.d/amavisd-new start
```

通过查看日志和检查 df -h 的输出来检查一切是否正常。在下面的例子中，/var/amavis 总共 100MB，目前只使用了 76KB：

```
# df -h /var/amavis
Filesystem      Size  Used Avail Use% Mounted on
/dev/shm        100M   76k   99M   1% /var/amavis
```

> **注意** 有时 amavisd-new 会在其 $TEMPBASE 目录中留下过期文件。为防止 $TEMPBASE 被这些文件填满，你可以每天停止 amavisd-new，删除过期文件，然后重启。如下的每日 cron 作业脚本可以完成这项工作：

```
#!/bin/bash
/etc/init.d/amavisd stop
rm -Rf /var/amavis/amavis-200*
/etc/init.d/amavisd start
```

### 配置 Postfix 使用 amavisd-new

此时，Postfix 和 amavisd-new 应该能够独立运行。因此，你需要配置 Postfix 将消息发送给 amavisd-new，并创建另一个 smtpd 实例用于消息重新注入。以下步骤（在后续章节中讨论）将把 amavisd-new 集成到 Postfix 中：

1.  创建一个传输（transport）。
2.  配置该传输。
3.  配置一个重新注入路径。

> **注意** 因为过滤后的邮件需要一种方式重新进入 Postfix 队列系统而无需再次被扫描，所以你需要一个专用的、不使用 content_filter 的 smtpd。这允许 amavisd-new 将邮件重新注入系统而不产生循环。端口 25 已被占用，因此你可以让 smtpd 的一个副本监听一个非标准端口。本例使用本地主机的端口 10025。amavisd-new 也需要一个监听端口。默认的本地主机端口 10024 是可以的。

#### 在 main.cf 中使用 content_filter 创建传输

将内容处理委托给外部程序的第一步是定义将消息发送给过滤程序的传输。Postfix 在 main.cf 文件中使用 `content_filter` 参数。该参数需要一个 `transportname:nexthop:port` 格式的表示法。

在我们处理的示例中，amavisd-new 与 Postfix 运行在同一台机器上，因此你可以通过 localhost (127.0.0.1) 的 10024 端口访问它。你需要在 main.cf 文件中定义以下 content_filter 参数，以使 Postfix 连接到 amavisd-new：

```
content_filter = amavisd-new:[127.0.0.1]:10024
```

#### 在不同的主机上运行 amavisd-new

如果你觉得单台机器的过滤负载过重，可以在一台或多台机器上运行 amavisd-new。transportname:nexthop:port 中的 nexthop 部分允许你轻松地为过滤器指定不同的主机。请看以下示例中的 `vscanners.example.com`：

```
content_filter = amavisd-new:vscanners.example.com:10024
```

名称 `vscanners.example.com` 可以是以下任一种情况：

- 一台机器（通过一个 A 记录）
- 多台机器（通过多个轮询 A 记录）
- 多台机器（一台或多台具有不同优先级 MX 记录的机器）

#### 在 master.cf 中定义传输

接下来，你需要定义将连接到 amavisd-new 的守护进程，并指定该守护进程的环境。记住，守护进程可以是 smtp、lmtp 或 pipe。你已经在本章前面看到了一个 pipe 的示例；现在来看看另外两种。

##### 定义 ESMTP 传输

如果你想使用 ESMTP 协议向 amavisd-new 发送消息，请在你的 master.cf 文件中添加以下条目：

```
# ==========================================================================
# service type  private unpriv  chroot  wakeup  maxproc  command
# (yes)   (yes)   (yes)   (never) (100)
# ==========================================================================
...
amavisd-new   unix  -       -       n       -       2       smtp
    -o smtp_data_done_timeout=1200s
    -o disable_dns_lookups=yes
```

在上面的条目中，有几点需要注意：

- 特殊的传输 `amavisd-new` 是常规 smtp 传输的一个副本。它的名称必须与你在 main.cf 中为 content_filter 参数定义的传输名称相匹配。
- amavisd-new 对资源的消耗很大。除非你有一台高速机器，否则你可能希望将同时运行的最大实例数保持为 2。
- `smtp_data_done_timeout` 参数是修改此守护进程行为的两个附加设置中的第一个。amavisd-new 处理传入消息可能需要相当长的时间，增加 smtp 发送消息后的超时时间可以保护 Postfix，避免在 amavisd-new 完成处理前就放弃连接。
- 因为此时你可能只处理本地机器名称，`disable_dns_lookups` 参数禁用了 smtp 客户端不必要的 DNS 查询。

> **注意** 你不一定需要专用的 SMTP 传输，因为默认的 smtp 就能很好地完成工作。然而，出于性能原因（以及由于 amavisd-new 相对较长的超时时间），专门为 amavisd-new 自定义一个传输是合理的。

##### 定义 LMTP 传输

如果你决定使用 LMTP 协议（而不是 SMTP）将消息传输到 amavisd-new，请在你的 master.cf 文件中添加以下条目：

```
#=========================================================
# service type    private unpriv  chroot  wakeup  maxproc  command
# (yes)   (yes)   (yes)   (never) (100)
#=========================================================
...
amavisd-new   unix  -       -       n       -       2       lmtp
    -o lmtp_data_done_timeout=1200s
    -o disable_dns_lookups=yes
```

##### 配置重新注入路径

最后，你需要创建一个重新注入路径，允许 amavisd-new 将消息回送至 Postfix 队列。重要的是，这个重新注入路径必须绕过 amavisd-new 传输。否则，消息会陷入一个循环：Postfix 将消息发送给 amavisd-new，邮件被重新注入 Postfix 队列，然后又再次被发送回 amavisd-new。

一个绕过任何先前定义的 content_filter 参数的重新注入路径在你的 master.cf 文件中看起来像这样：

```
#=========================================================
# service type    private unpriv  chroot  wakeup  maxproc  command
# (yes)   (yes)   (yes)   (never) (100)
# ====================================================================
...
127.0.0.1:10025  inet  n     -     n     -     -     smtpd
  -o content_filter=
  -o local_recipient_maps=
  -o relay_recipient_maps=
  -o smtpd_restriction_classes=
  -o smtpd_client_restrictions=
  -o smtpd_helo_restrictions=
  -o smtpd_sender_restrictions=
  -o smtpd_recipient_restrictions=permit_mynetworks,reject
  -o mynetworks=127.0.0.0/8
  -o strict_rfc821_envelopes=yes
```

在上述条目的所有选项中，*绝对*必不可少的是空的 `content_filter` 参数。这覆盖了 main.cf 文件中的 content_filter 参数。其余选项覆盖了其他 main.cf 参数，包括关闭那些对仅监听 localhost 网络接口的传输没有意义的限制选项。

设置完所有配置后，你就可以测试过滤器了。记住，对 master.cf 的更改需要你重新加载 Postfix。

### 测试 Postfix amavisd-new 过滤器

要测试 Postfix 和 amavisd-new 是否能协同工作，你必须验证 Postfix 能否将邮件发送给 amavisd-new，以及 amavisd-new 能否重新注入消息。测试包括以下步骤：

1. 查看 Postfix 是否在重新注入路径上监听。
2. 向 Postfix 发送一条消息，检查它是否将消息发送给 amavisd-new，以及消息是否回到了 Postfix 队列。
3. 查看病毒扫描器是否检测到测试模式。

#### 检查重新注入路径

更改 master.cf 文件后，运行 **postfix reload** 操作，使 Postfix 读取修改后的文件，然后检查日志文件是否有任何报错。接着，检查 smtpd 重新注入守护进程是否正在监听 localhost 的 10025 端口，如以下会话所示：

```
$ telnet 127.0.0.1 10025
220 mail.example.com ESMTP Postfix
EHLO 127.0.0.1
250-mail.example.com
250-PIPELINING
250-SIZE 10240000
250-VRFY
250-ETRN
250-STARTTLS
250-AUTH LOGIN PLAIN DIGEST-MD5 CRAM-MD5
250-XVERP
250 8BITMIME
QUIT
221 Bye
```

#### 向 Postfix 发送测试消息

Postfix 应该能够让未受感染的消息通过系统。从命令行发送一条消息，并使用 Postfix 和 amavisd-new 的日志文件来跟踪它。例如，你可以使用以下命令将你的 main.cf 文件邮寄给 `recipient@example.com`：

```
# sendmail -f sender@example.com recipient@example.com < /etc/postfix/main.cf
```

然后查看日志文件。文件底部应该有一个会话，开始部分如下所示，其中 Postfix 为消息分配了一个消息 ID，你可以用它来跟踪该消息：

```
Jan 31 10:45:08 mail postfix/pickup[10096]: 2788029AB29: uid=0 from=<sender@example.com>
Jan 31 10:45:08 mail postfix/cleanup[10652]: 2788029AB29:
message-id=<20040131094508.2788029AB29@mail.example.com>
```

下一条消息应该显示 Postfix 将消息交给 localhost 由 amavisd-new 处理（遗憾的是，Postfix 不会记录端口号或传输名称）：

```
Jan 31 10:45:08 mail postfix/qmgr[10097]: 2788029AB29: from=<sender@example.com>, size=1271,
nrcpt=1 (queue active)
Jan 31 10:45:08 mail postfix/smtp[10660]: 2788029AB29: to=<recipient@example.com>,
relay=localhost[127.0.0.1], delay=0, status=sent (250 2.6.0 Ok, id=25809-04, from MTA: 250
Ok: queued as 377D829AB2A)
```

现在 amavisd-new 扫描消息并记录该消息已通过：

```
Jan 31 10:45:08 mail amavis[25809]: (25809-04) Passed, <sender@example.com> ->
<recipient@example.com>, Message-ID: <20040131094508.2788029AB29@mail.example.com>, Hits: -
```

接下来，消息从 amavisd-new 返回 Postfix，以便重新注入队列。注意第二个 smtpd 也记录了消息 ID：

```
Jan 31 10:45:08 mail postfix/smtpd[10658]: connect from localhost[127.0.0.1]
Jan 31 10:45:08 mail postfix/smtpd[10658]: 377D829AB2A: client=localhost[127.0.0.1]
```



#### 检查测试病毒样本

你最后一次测试是模拟一条被病毒感染的消息。你可以通过获取 EICAR 测试病毒样本（http://www.eicar.org）并将其发送到 Postfix 来实现。任何未专门禁用该病毒特征的病毒扫描器都应该能够识别它。例如，以下命令应该会向 recipient@example.com 发送一个病毒：

```
# sendmail -f sender@example.com recipient@example.com < eicar.com
```

日志消息看起来和之前一样，直到 amavisd-new 扫描该消息为止：

```
Feb  6 15:48:54 mail postfix/pickup[30051]: 13B9E29AB29: uid=0 from=<sender@example.com>
Feb  6 15:48:54 mail postfix/cleanup[30741]: 13B9E29AB29: message-id=<20040206144854.13B9E29AB29@mail.example.com>
Feb  6 15:48:54 mail postfix/qmgr[19295]: 13B9E29AB29: from=<sender@example.com>, size=347, nrcpt=1 (queue active)
Feb  6 15:48:54 mail postfix/smtp[30744]: 13B9E29AB29: to=<recipient@example.com>, relay=localhost[127.0.0.1], delay=0, status=sent (250 2.5.0 Ok, id=10217-07, BOUNCE)
...
Feb  6 15:48:54 mail amavis[10217]: (10217-07) INFECTED (Eicar-Test-Signature), <sender@example.com> -> <recipient@example.com>, quarantine virus-20040206-154854-10217-07, Message-ID: <20040206144854.13B9E29AB29@mail.example.com>, Hits: -
```

发现消息包含病毒后，amavisd-new 向 virusalert@example.com 发出警报并将消息退回给发件人：

```
Feb  6 15:48:54 mail postfix/smtpd[30747]: connect from localhost[127.0.0.1]
Feb  6 15:48:54 mail postfix/smtpd[30747]: 639A729AB2A: client=localhost[127.0.0.1]
Feb  6 15:48:54 mail postfix/cleanup[30741]: 639A729AB2A: message-id=<VA10217-07@mail>
Feb  6 15:48:54 mail postfix/qmgr[19295]: 639A729AB2A: from=<>, size=1463, nrcpt=1 (queue active)
Feb  6 15:48:54 mail postfix/local[30749]: 639A729AB2A: to=<virusalert@example.com>, relay=local, delay=0, status=sent (forwarded as 8484829AB2C)
```

## 使用简化代理过滤器和 amavisd-new 进行病毒扫描

这是一种不同且更新的方法。最好将代理过滤器与 amavisd-new 结合使用。代理过滤器能在病毒扩散之前提供更好的检测效果。本图有助于更好地理解图 3 中的流程图。

(1) 代理过滤器（Proxy Filter）

(2) 病毒（Virus）

(3) 病毒（Virus）

(4) 病毒（Virus）

(5) 病毒（Virus）

(6) 病毒（Virus）

(7) 病毒（Virus）

(8) 病毒（Virus）

(9) 病毒（Virus）

(10) 病毒（Virus）

使用 smtpd_proxy_filter 时，消息的流转过程如下：

- 1. 邮件客户端将消息发送到 Postfix smtpd。
- 2. 启用了 smtpd_proxy_filter 的 smtpd 将消息移交给 amavisd-new。请注意，这与使用 content_filter 的情况不同——在 content_filter 方式中，队列管理器请求 Postfix lmtp 或 smtp 客户端将消息发送到 amavisd-new。
- 3. amavisd-new 将消息发送给其他应用程序（在本例中，发送给两个病毒扫描器）。
- 4. amavisd-new 告诉 smtpd 它是接受还是拒绝该消息。如果它接受消息，则会将消息重新注入到第二个 smtpd 实例中；如果它拒绝消息，则按照你的配置进行处理。
- 5. 原始 smtpd 监听 amavisd-new 的回放，接受或拒绝来自客户端的消息。

> **注意** *smtpd_proxy_filter 是将 smtpd 守护进程拆分为两部分：*
> * 一部分使用过滤器对传入邮件进行净化处理。
> * 另一部分负责队列处理。

本节说明如何按照第 11 章描述的通用步骤来配置 amavisd-new 与 smtpd_proxy_filter。你需要执行以下步骤将 amavisd-new 与 smtpd_proxy_filter 参数集成：

- 1. 安装 amavisd-new（本章前面的"安装 amavisd-new"部分已作描述）。
- 2. 测试 amavisd-new（前面的"测试 amavisd-new"部分已作描述）。
- 3. 配置 Postfix 以使用 amavisd-new。
- 4. 测试配置。

### 配置 Postfix 以使用 amavisd-new 配合 smtpd_proxy_filter

第一步是定义邮件进入过滤程序所使用的传输方式。你需要完成以下三项工作：

- 1. 修改现有的 smtpd 传输，使其作为 amavisd-new 的代理。
- 2. 创建一个额外的 smtpd 实例，用于将邮件重新注入 Postfix，从而绕过全局 smtpd_proxy_filter 参数。
- 3. 按照前面章节描述的方式测试配置。

### 修改现有 smtpd 以进行代理

要使 smtpd 将消息代理发送到 amavisd-new，请在 master.cf 文件中现有的 smtpd 服务配置后追加 smtpd_proxy_filter 参数。例如，以下配置使 smtpd 将消息发送到本地主机的 10024 端口（请记住，这些是 amavisd-new 的默认设置）：

```
#=============================================================
# service type  private unpriv  chroot wakeup maxproc command
# (yes)   (yes)  (yes)  (never) (100)
#=============================================================
...
smtp     inet  n       -       n       -       20      smtpd
  -o smtpd_proxy_filter=localhost:10024
  -o smtpd_client_connection_count_limit=10
```

请注意，-o smtpd_client_connection_count_limit=10 可以防止单个 SMTP 客户端占用 maxproc 列中定义的所有 20 个 SMTP 服务器进程。如果你的所有邮件都来自受信任的中继主机，则不需要此限制。

此外，与前面用于 content_filter 机制的流程不同，你并没有在 main.cf 文件中定义全局参数，因此不需要在重注入传输中显式覆盖它。

### 创建用于消息重注入的额外 smtpd 实例

要让消息在非代理的 smtpd 实例上重新进入 Postfix 队列，你需要在 master.cf 文件中添加一个特殊的 smtpd 实例。此示例在本地主机的 10025 端口上创建另一个实例：

```
#=============================================================
# service type  private unpriv  chroot wakeup maxproc command
# (yes)   (yes)  (yes)  (never) (100)
#=============================================================
...
127.0.0.1:10025 inet n  -       n       -       -       smtpd
  -o smtpd_authorized_xforward_hosts=127.0.0.0/8
  -o smtpd_client_restrictions=
  -o smtpd_helo_restrictions=
  -o smtpd_sender_restrictions=
  -o smtpd_recipient_restrictions=permit_mynetworks,reject
  -o mynetworks=127.0.0.0/8
  -o receive_override_options=no_unknown_recipient_checks
```

-o smtpd_authorized_xforward_hosts=127.0.0.0/8 参数允许过滤后的 smtpd 从过滤前的 smtpd 接收远程 SMTP 客户端信息。具体来说，过滤后的 smtpd 将接受来自 smtpd_authorized_xforward_hosts 中列出的主机发送的任何 XFORWARD 命令。这对于调试非常有用，因为 smtpd 将使用原始客户端 IP 地址而不是 localhost[127.0.0.1]。

其余参数减轻了过滤后 smtpd 的负担，因为过滤前的 smtpd 已经完成了这些工作。

## 第三部分

## 高级配置

在本书的这一部分中，你将看到 Postfix 与各种第三方应用程序交互的常见场景，例如 SQL 服务器、Cyrus SASL、OpenSSL 和 OpenLDAP。以下是本部分各章的概述：

- **邮件网关**
  邮件中继代表其他邮件服务器或客户端传输消息。在大多数情况下，邮件中继暴露在互联网上，而其他服务器则安全地位于防火墙之后。在第 13 章中，你将了解如何将简单的邮件中继打造为"智能"主机。

- **支持多域名的邮件服务器**
  第 14 章描述了 Postfix 处理多域名邮件的两种方式。此外，你将了解如何配置 Postfix 以查询 SQL 服务器，而不是使用静态映射。

- **理解 SMTP 认证**
  SMTP 认证是一种在邮件客户端中继消息之前对其进行身份验证的系统。由于 Postfix 中的 SMTP 认证依赖于 Cyrus SASL 软件，因此第 15 章将向你展示如何配置 Cyrus SASL，以便将其与 Postfix 配合使用。



# SMTP 认证

继续讨论 SMTP 认证，第 16 章将向你展示如何为服务器端、客户端或两者同时配置 Postfix 进行认证。

# 理解传输层安全

传输层安全（TLS）对 Postfix 与其他主机之间的通信层进行加密。Postfix 对 TLS 的实现依赖于 OpenSSL，因此第 17 章不仅会介绍 TLS 的工作原理，还会讲解如何准备所需的证书。

## 使用传输层安全

第 18 章将向你展示如何设置 Postfix 服务器以向其他主机提供加密通信，以及如何让 Postfix 客户端在其他服务器提供 TLS 时使用它。你还将了解基于证书的中继是如何工作的。

## 公司邮件服务器

第 19 章解释了如何配置 Postfix 来查询 LDAP 服务器。在此过程中，你将把本地投递的工作委托给一个 MDA（邮件投递代理），并配置一个基本的 Courier IMAP 服务器。最终，你将拥有一个从 OpenLDAP 服务器获取用户数据的完整邮件系统。

## 在 chroot 环境中运行 Postfix

第 20 章将向你展示如何配置 Postfix 以 chroot 方式运行。它解释了为什么某些守护进程不能在 chroot 环境下运行，并提供了如何将 Postfix 与 SASL 结合在 chroot 环境中运行的示例。

# 13 邮件网关

*邮件网关*（也称为“智能主机”）是连接逻辑上隔离网络的服务器。通常，邮件网关在 DNS 记录中作为互联网上其他邮件服务器的最终目的地出现，而这些服务器并不知道邮件网关后面还有其他邮件服务器。本章将向你展示如何设置邮件网关，并讨论*真正的*智能主机的特性。

公司和 ISP 使用邮件网关来控制进出其网络的 SMTP 流量。通常，网络设置只允许 25 端口的流量到达邮件网关，并强制网络内的客户端使用这台机器发送外部邮件。防火墙负责屏蔽端口，而 Postfix 则执行邮件网关的功能。

图 13-1 显示了一台将所有消息中继到邮件网关（反之亦然）的群件服务器。邮件网关保护群件服务器免受外部攻击——外部客户端和服务器无法直接连接到群件服务器。

![](img/852c79f689feb77c5fde686b993808b1_198_0.png)

图 13-1：Postfix 作为群件服务器的邮件中继

**提示：** 你可以通过集成病毒扫描和集中式垃圾邮件过滤等功能来扩展邮件网关的功能。这样，你不仅保护了群件免受恶意连接的侵害，还保护了它免受恶意内容的侵害。

如果你向客户提供中继服务，本章可以帮助你设置一个基本的邮件网关。你可以通过添加对 SMTP 认证（参见第 16 章）和传输层安全（参见第 18 章）的支持来扩展其服务。

## 基本设置

基本的邮件网关设置允许 Postfix 在外部邮件服务器上运行，并将发送到某些域名的邮件中继到另一个（内部）邮件服务器。要创建这样的邮件网关，你需要在中继服务器上执行以下步骤：

1.  允许内部服务器使用网关作为中继。
2.  设置邮件将被中继到的内部域（`relay_domains`）。
3.  设置邮件将被中继到的主机（`relayhost`）。
4.  定义邮件将被中继到的内部收件人（`relay_recipient_maps`）。

## 设置网关中继权限

你的第一步是允许邮件网关为你的“隐藏”邮件服务器进行中继。将内部邮件服务器的 IP 地址添加到 `mynetworks` 参数的服务器列表中。例如，如果内部服务器的地址是 172.16.1.1，你可以在邮件网关的 `main.cf` 文件中添加这一行：

```
mynetworks = 127.0.0.0/8 172.16.1.1/32
```

将中继访问限制在邮件网关的 localhost 地址（127.0.0.1）和内部邮件服务器（本例中为 172.16.1.1），这样你网络内的其他主机就无法使用该网关作为中继。

## 在网关上设置中继域

下一步是告诉 Postfix 接受来自外部网络的、发往内部网络主机的邮件。Postfix 使用 `relay_domains` 参数来定义它为其中继的域名列表，即使它不是这些域的最终目的地。例如，如果你想为 example.com 中继邮件，请使用此设置：

```
relay_domains = example.com
```

## 在网关上设置内部邮件主机

既然网关知道它应该接受某个域的邮件，你必须告诉它将发往该域的传入消息中继到哪里。你可以通过创建传输映射来实现，这是一个像 `/etc/postfix/transport` 这样的文件。例如，如果你想将 example.com 的消息中继到 `mail.office.example.com`，该文件可能如下所示：

```
example.com    smtp:[mail.office.example.com]
```

在此行中，`smtp` 表示 Postfix 应该使用在 `master.cf` 文件中定义的 smtp 传输类型。方括号很重要，因为它们会禁用对 `mail.office.example.com` 的 MX 查询。如果没有方括号，Postfix 将查找 `mail.office.example.com` 的 MX 记录。由于此记录可能属于服务器主机本身，它将尝试将邮件投递到自身，从而导致传入消息循环。

现在你需要使用此命令创建索引文件：

```
# postmap hash:/etc/postfix/transport
```

最后，在你的 `main.cf` 文件中按如下方式设置 `transport_maps` 参数（然后重新加载 Postfix）：

```
transport_maps = hash:/etc/postfix/transport
```

## 定义中继收件人

是什么让网关变得“智能”？普通网关接受发往中继域的*任何*收件人的*任何*消息，包括在最终投递消息的内部邮件服务器上不存在的无效收件人。

考虑到当今互联网上充斥着大量的垃圾邮件和恶意软件，并且可能存在不允许从外部接收消息的收件人（如共享文件夹、内部邮件列表，甚至可能是一些真实用户），普通网关可能会引发问题，因为它接受所有内容。特别是，它会将邮件、垃圾邮件和病毒中继到不存在和未授权的账户。

此外，通过接受发往不存在地址的邮件，网关就承担了在邮件无法投递时通知发件人的责任。这会用 MAILER-DAEMON 消息污染邮件队列，并导致互联网上从未发送过这些邮件的人收到散射邮件。

当 Postfix 不接受邮件时，该责任就留在了客户端。如果那个客户端是一台被植入后门的 Windows PC，那么根本就不会有散射邮件被发送。

智能主机懂得去伪存真，因为它拥有内部服务器上有效收件人的列表。使用 `relay_recipient_maps` 参数来定义和激活有效用户列表。例如，如果你的映射名称是 `/etc/postfix/relay_recipients`，你会在 `main.cf` 文件中使用这一行：

```
relay_recipient_maps = hash:/etc/postfix/relay_recipients
```

> **注意：** *如果你定义了此参数，映射必须提供有效中继收件人的列表。否则，你的网关将没有任何一致性。如果你无法提供列表，那么请通过设置 `relay_recipient_maps =` 来禁用该映射。*

当然，当你告诉 Postfix 在哪里可以找到映射时，你需要实际提供该列表。如果你按照前面的示例配置了映射，请创建一个名为 `/etc/postfix/relay_recipients` 的纯文本文件，其中包含有效的收件人。例如，以下文件启用了 `john@example.com` 和 `linda@example.com` 的中继：

```
john@example.com    OK
linda@example.com   OK
```

如果你想明确拒绝某个收件人的中继访问，请使用错误代码和消息，例如 `554 Delivery not permitted` 而不是 `OK`。

与任何映射一样，你需要将映射转换为你在 `relay_recipient_maps` 参数中定义的索引数据库类型。例如，运行 **`postmap hash:/etc/postfix/relay_recipients`** 来完成此操作。

> **注意：** *如果你远程邮件服务器上的用户很少且不常变化，手动设置有效用户列表很简单。不过，更有可能的情况是，你拥有许多持续变化的用户，甚至可能不知道用户列表。有关如何自动化此过程的讨论，请参阅本章后面的“从 Active Directory 导出有效收件人”部分。特别是，该部分描述了如何从 Microsoft Exchange 2003 服务器获取有效收件人列表。*

## 高级网关设置

高级网关不仅将邮件转发到其他服务器，还能防御本地邮件攻击，并自动更新中继域中的有效收件人列表。以下部分展示了多种技术，用于改进网关提供的一般邮件服务。



## 增强邮件网关的安全性

到目前为止，您的 Postfix 安装会将所有来自 example.com 地址的邮件转发到内部邮件服务器 mail.office.example.com。如果这是您的智能主机必须执行的唯一任务（即，您的智能主机不接收发送给其本地用户的邮件），那么您应该禁用本地投递，这样智能主机就不会因接收发送给本地用户的恶意消息而受到攻击。

请执行以下步骤以禁用本地投递：

+   1. 清空本地目的地。第一步是告诉 Postfix，通过将 `mydestination` 参数设置为空来使其不是最终目的地，如下所示：

```
mydestination =
```

+   2. 禁用本地收件人。将 `local_recipient_maps` 参数设置为空，这样 Postfix 将无法查找任何本地收件人：

```
local_recipient_maps =
```

+   3. 转发所需的本地收件人。当您设置了空的 `local_recipient_maps` 参数后，发送给所有本地收件人的邮件都将被禁用。但是，您仍然需要保持网关符合 RFC 规范，因此您必须为 postmaster 和 abuse 设置转发地址，指向您的内部邮件服务器。

创建一个映射文件用作 `virtual_alias_maps` 参数的目标（`/etc/postfix/virtual` 文件就可以），并为内部邮件服务器上的这两个收件人添加转发地址。例如，您的映射文件可能如下所示：

```
postmaster		postmaster@example.com
abuse		abuse@example.com
```

现在，使用 **postmap hash:/etc/postfix/virtual** 命令从该文件构建一个索引映射，并在您的 `main.cf` 文件中引用它，如下所示：

```
virtual_alias_maps = hash:/etc/postfix/virtual
```

+   4. 创建本地投递错误消息。当您禁用本地投递时，还应告知任何尝试向智能主机发送邮件的客户端，您已禁用向本地收件人的投递。为此，请使用 `local_transport` 参数定义一个特殊的本地传输，该传输会发送一条错误消息。例如，以下行将所有本地消息发送到错误守护进程，该守护进程将提供适当的错误消息：

```
local_transport = error:local mail delivery is disabled
```

+   5. 重定向对本地服务的回复。如果您已经按照前面章节中的步骤操作，Postfix 现在将不再接受除 postmaster 和 abuse 之外的本地用户邮件。但是，使用 Postfix 向管理员和用户发送状态报告的本地服务（如 cron）仍会使用与机器主机名关联的发件人地址发送邮件。这可能会造成混淆，因为您无法回复这些消息。

为了防止用户回复这些应用程序，可以更改 Postfix 作为电子邮件地址域名部分附加的 `myorigin` 参数的值。将 `myorigin` 设置为确实拥有邮件服务器并为这些发件人提供邮箱或别名的域名。例如，如果作为 example.com 最终目的地的内部邮件服务器可以提供此服务，您可以使用此设置：

```
myorigin = example.com
```

+   6. 禁用本地投递代理。最后，您可以防止 `master` 守护进程启动本地投递代理——这实际上关闭了本地投递代理，因为此机器上没有收件人。编辑您的 `master.cf` 文件，并通过在包含本地服务的行前添加井号（#）来注释掉该行，如下所示：

```
# ==================================================================
# service type  private unpriv  chroot  wakeup  maxproc command + args
# (yes)   (yes)   (yes)   (never)  (100)
# ==================================================================
smtp      inet  n       -       n       -       -       smtpd
# local   unix  -       n       n       -       -       local
virtual   unix  -       n       n       -       -       virtual
lmtp      unix  -       -       n       -       -       lmtp
anvil     unix  -       -       n       -       1       anvil
```

重新加载 Postfix 后，它将不再接受发送给本地收件人的消息。

## 与 Microsoft Exchange Server 配合使用 Postfix

Microsoft Exchange Server 无疑是一款功能强大的群件服务器，但其安全性记录和在遭受攻击时的稳定性并不理想。因此，许多邮件管理员使用 Postfix 网关来增强其群件功能。本节讨论如何为 Postfix 网关主机提供有效的收件人列表以及如何自动化此过程。

使 Postfix 和 Exchange Server 协同工作最简单、最常见的解决方案是让 Postfix 中继主机使用 LDAP（轻量级目录访问协议）查询 Exchange Server。中继主机将在每次消息到达时查询 Exchange Server，以确定收件人是否有效。然而，这种方法存在风险和局限性。另一种方法是让 Exchange Server 将收件人列表推送到 Postfix 服务器，这种方法在以下方面更好：

**安全性**

无论您在内部邮件服务器上运行什么软件包，您都希望它尽可能远离安全威胁。这就是为什么您一开始要将其置于防火墙之后。安全的基本规则之一是*只*允许应该允许的内容，并拒绝*所有*其他内容。

许多系统管理员的第一反应是让 Postfix 使用 LDAP 查询远程 Exchange Server 以获取有效的收件人。为此，您必须在 Exchange Server 上打开端口 389（TCP/UDP）以允许来自 Postfix 的连接。这相对容易，但它为您的内部局域网打开了一个端口。

改变方向更安全，即仅在收件人列表发生变化时，由 Exchange 为 Postfix 提供有效的收件人列表。通过使用 scp 或 rsync 由 Exchange Server 管理员将此列表推送到智能主机，您无需从 DMZ 向局域网打开端口。

**性能**

与 Postfix 使用的索引映射相比，LDAP 查询速度较慢。如果您为 Postfix 提供一个静态的有效收件人列表，智能主机可以非常快速地处理消息。

**稳定性**

智能主机的存在是为了保护内部邮件服务器，当受到攻击的智能主机导致内部服务器宕机时，这就适得其反了。这种情况可能会发生，因为垃圾邮件发送者使用字典攻击向大量收件人同时发送消息，这会导致使用 LDAP 的邮件中继向其本应保护的服务器发送大量查询，询问有效的收件人。这会减慢（甚至禁用）Active Directory，从而影响 Exchange Server，将字典攻击变成拒绝服务攻击。如果邮件服务器要宕机，您希望是外部的智能主机宕机，而不是内部的邮件服务器。

在本节中，您将按照以下步骤将 Exchange 2003 Server 中的有效收件人发送到 Postfix 邮件中继：

+   1. 导出所有有效收件人的列表。
+   2. 将列表复制到邮件中继。
+   3. 从列表中提取有效收件人。
+   4. 创建中继收件人映射。
+   5. 索引中继收件人映射。
+   6. 自动化此过程。

### 从 Active Directory 导出有效收件人

Microsoft 使用其 Active Directory 中的 `proxyAddresses` 属性来存储 Exchange 的有效收件人地址。从 Microsoft Active Directory 导出 `proxyAddresses` 的一个简便方法是使用 `csvde`，这是一个在每台 Exchange Server 上都可用的命令行工具——它不需要您使用自编写的脚本。例如，要将 `proxyAddresses` 的值导出到名为 `C:\export\example_com_recipients.txt` 的文件，您只需在命令提示符窗口中使用以下命令：

```
C:\> csvde -m -n -g -f "C:\export\example_com_recipients.txt" \
    -r "(|(&(objectClass=user)(objectCategory=person)) \
    (objectClass=groupOfNames) (objectClass=msExchDynamicDistributionList))" \
    -l proxyAddresses
```

> **提示** 组织和结构化 Active Directory 的方法有成千上万种，因此可能很难找到需要从 Active Directory 导出的对象名称。

Exchange 安装为您提供安装多个支持工具的选项，包括 ADSI Edit 模块。将其添加到您的 MMC（Microsoft 管理控制台）。设置好后，从命令行运行 `mmc.exe` 即可完全访问 Active Directory 中的对象名称。

前面命令的输出包含的信息远比 Postfix 所需的多。例如，您可能会在输出文件中看到如下内容：

```
DN,proxyAddresses
"CN=Administrator,CN=Users,DC=example,DC=com",smtp:abuse@example.com;SMTP:\
    Administrator@example.com; X400:c=DE\;a= \;p=Example Corporat\;o=Exchange\;s=Administrator\
    ;;smtp:postmaster@example.com
"CN=Gast,CN=Users,DC=example,DC=com",
"CN=SUPPORT_388945a0,CN=Users,DC=example,DC=com",
"CN=krbtgt,CN=Users,DC=example,DC=com",
"CN=IUSR_MAIL,CN=Users,DC=example,DC=com",
"CN=IWAM_MAIL,CN=Users,DC=example,DC=com",
"CN=Wilma Pebble,OU=purchasing,DC=example,DC=com",smtp:wilmapebble@example.com;smtp:\
    wilma@example.com;smtp:wilma.pebble@example.com;SMTP:w.pebble@example.com;smtp:\
    pebble@example.com; X400:c=DE\;a= \;p=Example Corporat\;o=Exchange\;s=Pebble\;g=Wilma\
    ;
"CN=Betty McBricker,OU=purchasing,DC=example,DC=com",smtp:mcbricker@example.com;smtp:\
    bettymcbricker@example.com;smtp:betty@example.com;smtp:betty.mcbricker@example.com;\
    SMTP:b.mcbricker@example.com;X400:c=DE\;a= \;p=Example Corporat\;o=Exchange\;\
    s=McBricker\;g=Betty\
"CN=Fred Flintstone,OU=sales,DC=example,DC=com",smtp:fredflintstone@example.com;\
    SMTP:fred.flintstone@example.com;smtp:f.flintstone@example.com;smtp:fred@example.com;\
    smtp:flintstone@example.com;X400:c=DE\;a= \;p=Example Corporat\;o=Exchange\;\
    s=Flintstone\;g=Fred\;
```



有效的收件人是标记为 smtp（别名）和 SMTP（主地址）的值。你需要提取与 smtp 和 SMTP 关联的值，以创建一个可供 Postfix smarthost 使用的列表。最终你将在 smarthost 上通过脚本完成此操作，但目前你需要先将该列表传输到 smarthost。

### 将收件人列表发送到邮件中继

有多种方式可以将文件从 Exchange Server 复制到 smarthost，但最佳方式之一是使用安全复制（scp），这是一种支持加密且可自动化的工具，Windows 和 Unix 均支持。
将文件自动传输到 smarthost 涉及以下步骤：

-   1. 为 Windows 获取安全复制（scp）客户端；例如 PuTTY。
-   2. 在 smarthost 上创建一个复制用户。
-   3. 创建认证密钥。
-   4. 将公钥添加到授权密钥列表。
-   5. 将私钥复制到 Windows 主机。
-   6. 将 SSH 密钥转换为 PuTTY 的密钥格式。
-   7. 将导出文件复制到 smarthost。

#### 为 Windows 获取安全复制客户端

PuTTY 是众多允许你使用 scp 从 Windows 主机复制文件的客户端之一，它是一款免费的 Telnet 和 SSH 客户端。你可以从 http://www.chiark.greenend.org.uk/~sgtatham/putty 下载。

你需要从此软件包中下载 pscp.exe 和 puttygen.exe 以执行本示例所需的操作。将这些可执行文件复制到 Windows 搜索路径中的目录，例如 C:\Windows。

#### 在 Smarthost 上创建复制用户

为满足文件传输需求，你需要在 smarthost 上创建一个用户。此账户仅用于接收导出的收件人列表。例如，你可以使用以下命令创建一个名为 e3k 的用户：

```
# useradd e3k
```

创建用户后，使用 passwd 命令设置密码。你将在设置过程中使用该密码，但当一切运行正常后你可以将其禁用。

#### 创建认证密钥

下一步是创建一组认证密钥，这样你就不需要密码即可将文件从 Windows 服务器传输到 smarthost。以 root 身份登录 smarthost，运行 **su - e3k** 切换到 e3k 用户，然后运行 **ssh-keygen** 创建密钥：例如，你可以以 e3k 身份运行以下命令：

```
$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/home/e3k/.ssh/id_rsa):
Created directory '/home/e3k/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/e3k/.ssh/id_rsa.
Your public key has been saved in /home/e3k/.ssh/id_rsa.pub.
The key fingerprint is:
17:7e:78:9e:39:0e:04:b7:ee:6d:39:28:c6:21:e4:84 e3k@mail.example.com
```

> ⚠ **如果你希望复制过程无需人工干预地运行，请不要设置密码短语。** 如果你输入了密码短语，则每次将导出文件复制到 smarthost 时都需要使用它。

前面的命令创建了两个文件：.ssh/id_rsa 和 .ssh/id_rsa.pub。前者是私钥；不要让它离开你的视线（除了你的 Windows 机器外，任何主机都不应拥有它）。

#### 将公钥添加到授权密钥列表

现在你已经拥有了密钥，你需要将刚创建的公钥告知 SSH 服务器。要将 id_rsa.pub 文件中的公钥追加到复制用户（e3k）的 $HOME/.ssh/authorized_keys 文件列表中，请运行以下命令。

```
$ cd .ssh
$ cat id_rsa.pub >> authorized_keys
```

创建 authorized_keys 文件后，确保其具有正确的权限，否则 SSH 服务器将拒绝使用该文件进行身份验证：

```
$ chmod 644 authorized_keys
$ ls -l authorized_keys
-rw-r--r--    1 e3k           e3k          230 May 13 10:38 authorized_keys
```

#### 将私钥复制到 Windows

接下来你需要将私钥从 smarthost 复制到 Windows 主机。最简单的方法是在 Windows 机器上使用 pscp.exe 命令。如果你的 smarthost 的 IP 地址是 172.16.1.1，你可以在命令提示符下运行以下命令：

```
> C:\export> pscp e3k@172.16.1.1:/home/e3k/.ssh/id_rsa .
e3k@172.16.1.1's password:
id_rsa                     |         0 kB |   0.9 kB/s | ETA: 00:00:00 | 100%
```

使用你在"在 Smarthost 上创建复制用户"一节中为该用户创建的密码。

#### 将 SSH 密钥转换为 PuTTY 密钥格式

PuTTY 用于存储公钥和私钥的格式与大多数 Unix SSH 软件包不同，因此你需要将私钥转换为 PuTTY 自身的格式才能使用。puttygen 工具可以进行密钥转换；在命令行中运行如下：

```
C:\export> puttygen id_rsa
```

此命令会启动一个加载私钥的 GUI 客户端。你现在应该会看到图 13-2 所示的对话框。

点击 **OK** 确认消息。将显示图 13-3 所示的 PuTTY 密钥生成器对话框。为转换后的密钥命名（例如 example_com.ppk），然后点击 **Save private key** 按钮。

如图 13-4 所示，密钥生成器会警告你密钥的密码短语为空。点击 **Yes** 以不设密码短语的方式保存密钥并存储私钥。现在你的 Windows 主机已准备好使用 scp 通过认证密钥将文件传输到 smarthost。

#### 将收件人列表复制到 Smarthost

保持命令提示符窗口打开，使用 `pscp.exe` 工具（属于 PuTTY 的 `scp`）将文件从 Windows 主机复制到 smarthost。运行 `pscp` 时，你必须指定私钥、要复制的文件以及执行复制的用户。在我们的示例中，私钥位于 `example_com.ppk` 文件中，要复制的文件是 `example_com_recipients.txt`，用户是 `e3k`。要将文件放入 `/home/e3k`，请使用以下命令：

```
C:\export> pscp -i example_com.ppk example_com_recipients.txt e3k@172.16.1.1:/home/e3k/
Authenticating with public key "rsa-key-20040512"
example_com_recients.txt |           2 kB |   2.4 kB/s | ETA: 00:00:00 | 100%
```

成功将文件复制到 smarthost 后，你可以将之前"从 Active Directory 导出有效收件人"一节中的 `csvde` 导出命令和前面的 `pscp` 命令存入名为 `export_valid_recipients.bat` 的批处理文件中。这样每当创建、更改或删除收件人时，你只需点击鼠标即可运行它。该文件内容大致如下：

```
csvde -m -n -g -f "C:\export\example_com_recipients.txt" \
    -r "(&(objectClass=user)(objectCategory=person)) \
    (objectClass=groupOfNames) (objectClass=msExchDynamicDistributionList))" \
    -l proxyAddresses
pscp -i example_com.ppk example_com_recients.txt e3k@172.16.1.1:/home/e3k/
```

验证此批处理文件可以正常工作后，你可以使用类似 `usermod -L e3k` 的命令在 smarthost 上禁用复制用户的密码，从而使 `e3k` 账户只能通过认证密钥进行远程访问。

### 构建收件人映射

现在你已经在 smarthost 上拥有了 Active Directory 导出文件，因此可以通过脚本从中提取收件人。操作时需要注意两点：

-   Microsoft 同时使用 `SMTP` 和 `smtp` 表示收件人地址，因此脚本必须捕获这两种变体。
-   你的脚本必须能够排除一些不应接收外部邮件的收件人。例如 Exchange 用于内部通信的 `SystemMailbox` 邮箱。

以下名为 `extract_valid_recipients` 的脚本提取所有有效收件人并将其写入文件，但不包含 `blacklist` 文件中列出的收件人。



## 构建收件人映射表

黑名单文件如下所示：

```
Administrator
SystemMailbox
```

运行 **extract_valid_recipients** 命令来执行脚本，它将在 `relay_recipients` 文件中生成有效收件人列表。

```
extract_valid_recipients /home/e3k/example_com_recipients.txt relay_recipients
```

输出应如下所示：

```
abuse@example.com	OK
postmaster@example.com	OK
wilma.pebble@example.com	OK
wilma@example.com	OK
wilma.pebble@example.com	OK
w.pebble@example.com	OK
pebble@example.com	OK
mcbricker@example.com	OK
bettymcbricker@example.com	OK
betty@example.com	OK
betty.mcbricker@example.com	OK
b.mcbricker@example.com	OK
fredflintstone@example.com	OK
fred.flintstone@example.com	OK
f.flintstone@example.com	OK
fred@example.com	OK
flintstone@example.com	OK
barney.rubble@example.com	OK
barneyrubble@example.com	OK
rubble@example.com	OK
barney@example.com	OK
b.rubble@example.com	OK
bammbamm@example.com	OK
bamm@example.com	OK
bamm.bamm@example.com	OK
b.bamm@example.com	OK
it-department@example.com	OK
purchasing-department@example.com	OK
sales-department@example.com	OK
```

如果此输出看起来正确，请使用 **postmap** 进行转换（例如，使用如下命令：**postmap hash:relay_recipients**），然后将其移动到 **relay_recipient_maps** 参数指向的路径（这在前文“定义中继收件人”部分已讨论）。例如，您可以使用如下命令：

```
# mv relay_recipients.db /etc/postfix/relay_recipients.db
```

> **注意** 不要将 **relay_recipient_maps** 直接指向您新创建的 **relay_recipients** 映射文件（例如 `hash:/home/e3k/relay_recipients`）！如果映射转换失败，Postfix 将停止服务。安全的方法是先进行映射转换，只有成功后才将其移动到 **relay_recipient_maps** 指向的位置。

### 构建发件人访问映射表

作为额外的好处，您的 Active Directory 导出文件还可以为 Postfix 提供一个允许向外部世界发送邮件的发件人列表。为此，您可以编写一个与“构建收件人映射表”部分类似的脚本，但只需做一个小改动：Microsoft 使用 **SMTP** 来标记有效的发件人地址，因此地址提取脚本应仅处理带有此标记的元素。

> **注意** 这对于防止病毒利用 Outlook 联系人文件夹构建虚假发件人地址，然后从您的网络发送邮件非常有用。

您可以将脚本命名为 **extract_valid_senders**，其内容应如下所示：

```
#!/bin/bash
# Extract all addresses that start with SMTP from an Active Directory
# export, but omit those that are listed in blacklist
cat $1 | tr -d " | tr , \\n| tr \; \\n | awk -F\: '/SMTP:/ {printf("%s\tOK\n",$2)}' | \
grep -v -f blacklist > $2
```

这次，当您运行以下命令时，应该会得到一个比之前更短的列表，因为这里没有别名：

```
# ./extract_valid_senders /home/e3k/example_com_recipients.txt example_com_senders
```

输出应如下所示，基于前面的示例：

```
w.pebble@example.com          OK
b.mcbricker@example.com         OK
fred.flintstone@example.com     OK
barney.rubble@example.com       OK
b.bamm@example.com              OK
it-department@example.com       OK
purchasing-department@example.com OK
sales-department@example.com    OK
```

在前面的命令行示例中，您将输出重定向到了名为 `example_com_senders` 的文件。现在，使用 `postmap hash:example_com_senders` 命令为其创建一个索引数据库。然后创建一个限制（参见第8章），用以下约束检查信封发件人：

- 如果邮件来自内部服务器，它必须携带一个有效的信封发件人地址。
- 如果邮件不是来自内部服务器，则此限制不适用。

要配置 Postfix 应用此条件限制，请定义一个限制类，当邮件来自内部邮件服务器时触发信封发件人限制。例如，您的 `main.cf` 文件可能包含以下内容：

```
smtpd_restriction_classes =
    must_be_valid_sender ①
must_be_valid_sender = ②
    check_sender_access hash:/etc/postfix/example_com_senders
    reject
smtpd_recipient_restrictions =
    check_client_access hash:/etc/postfix/example_com_ip ③
    reject_unauth_destination
    ...
```

① `must_be_valid_sender` 是一个限制的名称，其中包含当邮件来自内部邮件服务器时应用的限制子集；此行仅列出限制类。
② 此限制的定义包含处理来自内部服务器邮件的流程：首先检查有效信封发件人列表，拒绝任何其他信封发件人。
③ `check_client_access` 触发 `must_be_valid_sender` 限制类的执行。

最后，您需要将内部邮件服务器的 IP 地址添加到 `/etc/postfix/example_com_ip` 文件中，并附上要执行的限制操作。例如，以下行指定如果消息来自 `172.16.1.1`，Postfix 应应用 `must_be_valid_sender` 限制：

```
172.16.1.1   must_be_valid_sender
```

添加这些配置选项后，必须重新加载 Postfix 才能使更改生效。

#### 自动化映射构建过程

您可以在智能主机上自动化映射构建过程。以下示例使用了一个可以从《Postfix 书》网站（http://www.postfix-book.com）下载的 Makefile。

```
## 自动化映射构建过程的 Makefile
### 配置设置
# 我们从中提取数据的文件位置
ADS_DUMP=/home/e3k/example_com_recipients.txt
# .proto 文件的位置
PROTO_PATH=relay_recipients
PROTO_PATH2=valid_senders
# 成功构建的映射的目标路径
MAP_PATH=/etc/postfix/relay_recipients
MAP_PATH2=/etc/postfix/valid_senders
# 要构建的映射的类型和后缀
DB_TYPE=hash
DB_SUFFIX=db
### Makefile 选项
#
# 构建所有映射
all:            $(MAP_PATH).$(DB_SUFFIX) $(MAP_PATH2).$(DB_SUFFIX) blacklist
# 从 $(ADS_DUMP) 中提取有效收件人到 $(PROTO_PATH).proto
$(PROTO_PATH).proto:    $(ADS_DUMP)
	./extract_valid_recipients $(ADS_DUMP) $(PROTO_PATH).proto
# 从 $(ADS_DUMP) 中提取有效发件人到 $(PROTO_PATH2).proto
$(PROTO_PATH2).proto:   $(ADS_DUMP)
	./extract_valid_senders $(ADS_DUMP) $(PROTO_PATH2).proto
# 从 $(PROTO_PATH).proto 构建有效收件人映射
$(MAP_PATH).$(DB_SUFFIX):  $(PROTO_PATH).proto
	/usr/sbin/postmap -w $(DB_TYPE):$(PROTO_PATH).proto && \
	mv $(PROTO_PATH).proto.$(DB_SUFFIX) $(MAP_PATH).$(DB_SUFFIX)
# 从 $(PROTO_PATH2).proto 构建有效发件人映射
$(MAP_PATH2).$(DB_SUFFIX): $(PROTO_PATH2).proto
	/usr/sbin/postmap -w $(DB_TYPE):$(PROTO_PATH2).proto && \
	mv $(PROTO_PATH2).proto.$(DB_SUFFIX) $(MAP_PATH2).$(DB_SUFFIX)
# 移除所有 proto 映射
clean:
	rm -f $(PROTO_PATH).* $(PROTO_PATH2).* *~
```

一旦您成功运行 `make` 验证转换有效，您就可以创建一个 cron 作业来自动运行它。例如，您 crontab 中的以下作业将每15分钟运行一次：

```
0,15,30,45 * * * * cd /root/relay_recipients && /usr/bin/make
```

## 配置 Exchange 与 Postfix 的通信

本节介绍如何配置 Microsoft Exchange 通过您的 Postfix 网关中继所有邮件，以及如何配置 Exchange 以使其不会意外地淹没您的 Postfix 服务器。

默认情况下，Exchange 不会将出站消息中继到网关。要启动中继配置，请执行以下步骤。

1. 从“程序”菜单启动 Exchange 系统管理器。
2. 从左侧的树形菜单中选择“服务器”。
3. 从子树中选择您的邮件主机。
4. 从“主机”菜单中选择“协议”。
5. 从“协议”菜单中选择“SMTP”。
6. 右键单击“SMTP”菜单，然后从“默认 SMTP 虚拟服务器”菜单项中选择“属性”。
7. 在“默认 SMTP 虚拟服务器属性”窗口中选择“传递”选项卡。

您现在可以完成配置了。步骤将在以下各节中描述。

### 将 Postfix 服务器设置为智能主机

首先要做的是配置 Exchange 将所有出站消息发送到您的 Postfix 网关。从“传递”选项卡中选择“高级传递”，然后输入您的 Postfix 智能主机的完全限定域名（FQDN）（例如 `postfix.example.com`），如图13-5所示。

![](img/852c79f689feb77c5fde686b993808b1_214_0.png)

> **注意** Exchange 不接受 IP 地址作为“智能主机”字段的值。要么将智能主机添加到 Exchange 服务器查询的（内部）DNS 中，要么在 Exchange 服务器的 hosts 文件中静态设置。



在设置智能主机（smarthost）的FQDN后，你需要停止并重新启动Exchange Server的默认SMTP虚拟服务器，以使更改生效。

### 限制出站连接

到目前为止，你已经投入了大量精力来保护内部邮件服务器免受智能主机的不当行为影响。下一步是保护Postfix免受来自Exchange Server的消息过载。你需要做的就是限制同时出站的连接数量。

> **注意** Exchange中的默认设置是1000个同时连接。如果出站邮件队列中积累了如此多的消息（在较大的网络中，Exchange SMTP服务重启后很可能发生），它将在几分钟内将大量负载转移到智能主机上，这可能会占用智能主机过多资源，尤其是当智能主机并非只为单个内部邮件服务器提供服务时。

在这种情况下，最好让Exchange Server以较慢的速度处理其出站邮件队列。如果你无法访问该服务器，也可以使用第21章中描述的Postfix速率限制机制，来强制主机建立有限数量的连接。

在默认SMTP虚拟服务器窗口的“传递”选项卡中，选择“出站连接”，并将限制设置为50个同时连接，如图13-6所示。在常规情况下，这已被证明是一个良好的设置。

![](img/852c79f689feb77c5fde686b993808b1_215_0.png)

图13-6：在Exchange中限制出站连接数

### NAT 设置

位于NAT网关后面的Postfix邮件服务器会遇到问题，因为NAT网关在将IP数据包传输到Postfix之前会修改它们（替换目标地址）。这意味着smtpd只会监听网关的私有IP地址，而NAT网关接受的是对“官方”IP地址的连接。

这之所以成为问题，是因为电子邮件RFC要求邮件服务器接受发送到 *postmaster@[address]* 的邮件，其中 *[address]* 是一个IP地址。某些黑名单仅向该地址发送解封信息。

你可以通过使用 *proxy_interfaces* 参数配置Postfix以接受发送到 *postmaster@[address]* 的邮件。即使Postfix只监听一个内部IP地址，它也会接受发送到 *user@[address]* 的邮件。如果你的NAT网关地址是192.0.34.166，你应该使用此设置：

```
proxy_interfaces = 192.0.34.166
```

# 14

## 多域名邮件服务器

![](img/852c79f689feb77c5fde686b993808b_1_0.png)

Postfix可以通过两种不同的方法之一，为多个域名发送、接收和存储消息。第一种方法使用 *虚拟别名域* ，这简单地扩展了服务器作为最终目的地的域名数量。第二种方法涉及 *虚拟邮箱域* ，它更进一步，因为虚拟邮箱域不需要本地账户。本章将向你展示如何为多个域名提供SMTP服务实现这两种方法。

### 虚拟别名域

通常，Postfix仅将自己识别为 `mydestination` 参数中指定的域名的最终目的地。¹ 在 `mydestination` 中列出的域被称为规范域，因为它们通常列出了本地机器（及其父域名）的所有名称。

> ¹ Postfix也将自己识别为地址形式为 user@[ipaddress] 且列出Postfix之一IP地址的最终目的地。

在本章中，我们描述了几种使Postfix成为额外域名的最终目的地的方法。这些额外的域被称为虚拟域，因为它们与机器自身的名称无关。要为虚拟别名域配置基本服务，你必须执行以下步骤：

1. 设置虚拟别名域名。
2. 创建收件人地址映射。
3. 配置Postfix以接收虚拟别名域的邮件。
4. 测试新配置。
5. 创建高级映射。

这些步骤将在以下各节中描述。

#### 设置虚拟别名域名

你的第一步是告诉Postfix，除了系统默认域之外，它还是另一个域的最终目的地。Postfix使用 `virtual_alias_domains` 参数来定义虚拟域的映射。要使用此参数，请创建一个映射文件，例如 `/etc/postfix/virtual_alias_domains`，其中包含如下格式的虚拟域：

```
# virtual alias domains
postfix-book.com       20021125
```

在上面的示例中，右侧的数字是域的创建日期，但你可以将其设置为任何你喜欢的值。当查找 `virtual_alias_domains` 参数的映射时，Postfix不使用右侧部分，但Postfix映射总是要求同时有右侧和左侧部分。创建文件后，使用以下命令将其转换为索引映射：

```
# postmap hash:/etc/postfix/virtual_alias_domains
```

> **注意**
如果你将一个域列为虚拟域，请不要将其用作 `mydestination` 参数的值，否则可能会发生意外情况。Postfix将不知道它应该在本地投递邮件，还是将其发送到虚拟重写。这就是为什么Postfix会在日志中对此类配置提出强烈警告。

#### 创建收件人地址映射

配置虚拟别名域的下一步是创建 `/etc/postfix/virtual_alias_maps` 文件，将虚拟别名域收件人地址映射到本地收件人地址。以下示例包含单个和多个收件人。

```
# postfix-book.com
postmaster@postfix-book.com	ralf@example.com
abuse@postfix-book.com		abuse@example.com, patrick@example.com
ralf@postfix-book.com		ralf@example.com
patrick@postfix-book.com	patrick@example.com
```

确保包含 postmaster 和 abuse 的目标地址，因为RFC要求所有域都必须有这些地址的收件人。

> **警告** 始终在你的 virtual_alias_maps 文件右侧的收件人地址中使用完全限定域名。否则，你留下的解释空间太大。如果你只指定本地部分（例如，ralf），Postfix的trivial-rewrite守护进程将添加由myorigin指定的域部分。本地用户 ralf@myorigin 可能不正确，具体取决于myorigin和mydestination的值。

有了这个文件后，使用以下命令创建索引映射：

```
# postmap hash:/etc/postfix/virtual_alias_maps
```

### 配置Postfix以接收虚拟别名域的邮件

现在你已经将两个映射都准备就绪，必须根据收件人映射中的规则配置Postfix以接收虚拟别名域的邮件。你需要在main.cf中设置的参数是 `virtual_alias_domains` 和 `virtual_alias_maps`。使用前面各节中的文件名，参数应如下所示：

```
virtual_alias_domains = hash:/etc/postfix/virtual_alias_domains
virtual_alias_maps = hash:/etc/postfix/virtual_alias_maps
```

重新加载Postfix，并按照下一节所述测试虚拟别名域。

### 测试虚拟别名域设置

你可以通过向两个域名中的现有和未知收件人发送消息来测试你的虚拟别名域设置。

#### 向虚拟别名域中的有效地址发送邮件

以下是如何向有效收件人（postmaster）发送消息的示例：

```
$ echo test | /usr/sbin/sendmail postmaster@postfix-book.com
```

通过查看日志文件来验证消息是否成功发送。你应该看到类似以下的日志消息。

```
Apr 19 11:20:50 mail postfix/pickup[17850]: B8C4629AB38: uid=0 from=<root>
Apr 19 11:20:50 mail postfix/cleanup[17863]: B8C4629AB38:
    message-id=<20040419092050.B8C4629AB38@mail.example.com>
Apr 19 11:20:50 mail postfix/qmgr[17851]: B8C4629AB38:
    from=<root@mail.example.com>, size=282, nrcpt=1 (queue active)
Apr 19 11:20:50 mail postfix/local[17866]: B8C4629AB38: to=<ralf@example.com>,
    orig_to=<postmaster@postfix-book.com>, relay=local, delay=0, status=sent
    (mailbox)
```

测试消息首先发送到 postmaster@postfix-book.com；由于 virtual_alias_maps 中的条目，发送到 postmaster@postfix-book.com 的邮件被转到 ralf@example.com。然后它被本地投递给用户 ralf，因为 example.com 是“真实”域。

#### 向虚拟别名域中的无效地址发送邮件

以下是如何向无效收件人（nouser）发送消息的示例：

```
$ echo test | /usr/sbin/sendmail nouser@postfix-book.com
$ tail -f /var/log/mail.log
Apr 19 11:21:23 mail postfix/pickup[17850]: 9B61F29AB38: uid=0 from=<root>
Apr 19 11:21:23 mail postfix/cleanup[17863]: 9B61F29AB38:
    message-id=<20040419092123.9B61F29AB38@mail.example.com>
Apr 19 11:21:23 mail postfix/qmgr[17851]: 9B61F29AB38:
    from=<root@mail.example.com>, size=282, nrcpt=1 (queue active)
Apr 19 11:21:23 mail postfix/error[17887]: 9B61F29AB38:
    to=<nouser@postfix-book.com>, relay=none, delay=0, status=bounced
    (user unknown in virtual alias table)
```

这封邮件是发送给 nouser@postfix-book.com 的。由于在 virtual_alias_maps 中没有对应条目，发送到 nouser@postfix-book.com 的邮件会退回，并显示错误消息“虚拟别名表中用户未知”。

### 高级映射

你添加的虚拟别名域越多，就越有可能需要一遍又一遍地添加相同的映射条目。这时，通配符地址——正则表达式条目和隐式映射——就派上用场了。它们将在以下小节中描述。

#### 通配符地址

在某些情况下，你可能希望虚拟别名域中未知用户的邮件发送到一个通配符地址。virtual(5)手册页列出了多种方法，可以在 virtual_alias_maps 映射条目中实现这一点。优先级最低的一种方法如下：

```
@postfix-book.com   catchall@example.com
```



对于前一个条目，如果你的 Postfix 服务器在 `postfix-book.com` 的虚拟别名域别名映射中找不到 `unknownuser@postfix-book.com` 的匹配项，Postfix 会将该地址映射到 `catchall@example.com`。

## 正则表达式条目

你可以在 `virtual_alias_maps` 中使用正则表达式，将发送到虚拟别名域中一组未知用户的邮件映射到一个通配符账户。此外，你还可以将左侧（LHS）的匹配内容替换到右侧（RHS）的目标地址中——下文示例将展示这一点。如果你将匹配的地址发送到在 `alias_maps` 条目中指定的程序，这会非常方便。

为了了解其工作原理，请看以下 `virtual_alias_maps` 条目：

```
/^(.*)@postfix-book\.com$/   catchall+$1@example.com
```

当一封邮件发送给未知用户时，会发生以下情况：

1. 发送给 `unknownuser@postfix-book.com` 的邮件被映射到 `catchall+unknownuser@example.com`。
2. Postfix 将邮件递送给本地的现有收件人 `catchall@example.com`，但在递交给程序的过程中，它会按照 `local(8)` 手册页的描述，将 `$EXTENSION` 环境变量设置为 `unknownuser`。（`recipient_delimiter` 参数设置了扩展分隔符；默认值为 `+`。）
3. 如果一个程序处理该通配符地址的邮件，它可以使用 `$EXTENSION` 环境变量来找到预期的收件人，并构建一条信息性消息发送回原始发件人。你可以在 http://www.stahl.bau.tu-bs.de/~hildeb/postfix 找到一个名为 `fuzzy` 的此类程序示例。

在你的 `virtual_alias_maps` 映射中使用正则表达式还有许多其他方式。一个特别有用的做法是将匹配特定模式的地址映射到单个收件人。假设你有几个 `admin-name@example.com` 地址应该都发送到同一个邮箱。你可以尝试这样的条目：

```
/^admin-.*@postfix-book\.com$/   mailbox@example.com
```

这比像下面这样手动指定每个映射要好得多：

```
admin-firewall@postfix-book.com    mailbox@example.com
admin-mail@postfix-book.com        mailbox@example.com
admin-web@postfix-book.com         mailbox@example.com
...
```

## 多域的隐式映射

有时，创建一个适用于多个域的通用映射会很有用。例如，你的目标可能是创建一个始终匹配的通用 `postmaster` 收件人，无论你托管了多少个虚拟别名域。你可以通过在虚拟别名映射中添加以下条目来实现：

```
postmaster   postmaster@example.com
```

这样设置后，所有发送给本地部分为 `postmaster` 的收件人的邮件都会发送到 `postmaster@example.com`。由于前面的条目，Postfix 将接受发送给这些地址的邮件并将其递送到 `postmaster@example.com`：

- `postmaster@$myorigin`
- `postmaster@[$inet_interfaces]`
- `postmaster@$mydestination`

请注意，并非所有这些都是虚拟别名域，并且这三个域不一定涵盖你所有的虚拟别名域。请查看 `virtual(5)` 手册页，其中详细描述了搜索顺序。如果你希望你所有的虚拟别名域都具有相同的 `postmaster` 地址，请编写一个脚本将它们添加到 `virtual_alias_maps` 中。

> **注意** 你不能在映射中使用配置变量（例如 `$myorigin`）。Postfix 不会展开这些变量。我们的符号仅作为说明。

### 虚拟邮箱域

虚拟邮箱域是为没有本地账户（即不在 `/etc/passwd` 中）的用户设计的域。该功能最初作为包含单独投递代理守护进程的补丁引入，现在已成为 Postfix 的标准组件。

Postfix 中的虚拟投递代理基于本地投递代理。与本地代理不同，虚拟投递代理无法访问你系统的本地用户信息（例如在 `/etc/passwd` 中）来查找收件人名称。相反，虚拟投递代理完全依赖与你的系统无关的映射类型。

阻止虚拟投递代理了解系统账户有两个原因：

**可扩展性**

在 Linux 上，使用在 `/etc/passwd` 中定义的本地账户会将邮件服务器限制为大约 65,536 个收件人。Solaris 和 *BSD 不受此限制，它们拥有更长的 UID。虚拟投递代理不受这些限制。

**安全性**

如果为了简单地收发邮件而不需要用户名和密码，系统被入侵的可能性会大大降低。此外，虚拟投递代理不会执行用户指定的 shell 命令，也不会将邮件附加到用户指定的本地文件。

因为虚拟投递代理对你的系统一无所知，所以它无法处理诸如 `$HOME/.forward` 这样的文件，也无法使用诸如 `procmail` 和 `vacation` 等应用程序。虚拟投递代理的功能已简化为仅将邮件递送到邮箱。

#### 检查 Postfix 对虚拟投递代理的支持

要使用虚拟邮箱域，`master` 守护进程必须能够运行虚拟守护进程。检查你的 `master.cf` 文件；默认情况下该守护进程是启用的，如以下示例所示：

```
# ============================================================================
# service type  private unpriv  chroot  wakeup  maxproc  command + args
# (yes)   (yes)   (yes)   (never) (100)
# ============================================================================
smtp      inet  n       -       n       -       -       smtpd
...
local     unix  -       n       n       -       -       local
virtual   unix  -       n       n       -       -       virtual
...
```

> **注意** *确保虚拟守护进程没有在 chroot 环境中运行（请参阅上例中的第五列）。*

## 基本配置

要配置一个基本的虚拟邮箱域，你必须让虚拟投递代理在扁平化层次结构中使用相同的 UID 和 GID 存储所有消息。你需要执行以下步骤：

1. 设置虚拟邮箱域的名称。
2. 设置虚拟投递代理的文件所有权。
3. 设置域邮箱的基本目录。
4. 创建收件人映射。
5. 创建别名映射。

#### 设置虚拟邮箱域名称

首先，你需要通过在 `main.cf` 文件中设置 `virtual_mailbox_domains` 参数为一个域列表，来告诉 Postfix 它是一个或多个虚拟邮箱域的最终目的地。例如，如果你想为 `example.com` 创建一个虚拟邮箱域 `mailbox`，你会使用此设置：

```
virtual_mailbox_domains = example.com
```

#### 设置文件所有权

虽然虚拟邮箱域不要求每个邮箱都有唯一的用户，但你仍然需要至少一个用户 ID（UID）和组 ID（GID）来让虚拟投递代理访问邮箱。为此，你必须使用 `virtual_uid_maps` 和 `virtual_gid_maps` 参数定义所有权映射。

#### 设置用户

要设置邮箱所有者，你需要为邮箱创建一个本地用户（如果尚未创建）。要创建一个名为 `vbox`、用户 ID 为 1000 的邮箱用户，请运行以下命令：

```
# useradd vuser -u 1000
```

> **注意** 默认情况下，邮箱所有者的 UID 不得低于 100。这是由 `virtual_minimum_uid` 参数设置的安全措施，用于防止虚拟用户覆盖系统账户拥有的敏感文件。你可以通过在 `main.cf` 文件中设置 `virtual_minimum_uid` 来设置不同的边界。

设置好邮箱所有者用户后，你必须告诉虚拟投递代理在向文件系统写入消息时使用此 UID。在你的 `main.cf` 文件中使用 `virtual_uid_maps` 参数设置 UID，如以下示例中 UID 为 1000：

```
virtual_uid_maps = static:1000
```

> **注意** 对于 UID，使用 `static` 选项可以使命令虚拟守护进程专门使用此 UID。你也可以动态应用 UID，如稍后在“高级配置”部分所述。

#### 设置组

除了刚刚设置的用户外，你还需要一个本地组。对于基本设置，创建一个 GID，其编号与上一节中的 UID 相同。你的 `useradd` 命令可能已经为你完成了此操作（检查你的 `/etc/group` 文件），但如果尚未执行，请使用如下命令：

```
# groupadd vuser -g 1000
```

现在，在你的 `main.cf` 文件中设置 `virtual_gid_maps` 参数，方法与之前设置虚拟邮箱用户时相同：

```
virtual_gid_maps = static:1000
```

#### 设置虚拟邮箱域基础目录

虚拟投递代理需要知道在其收件人的位置查找邮箱。通常，由操作系统提供环境变量和配置文件，向应用程序传达默认系统设置。由于虚拟投递代理不识别环境变量，你必须明确说明应将要投递给用户的消息存放于何处。

在你的 `main.cf` 文件中设置 `virtual_mailbox_base` 参数，以指定传入消息的存储位置。示例如下：

```
virtual_mailbox_base = /var/spool/virtual_mailboxes
```

> **注意** 单个虚拟邮箱的完整路径由 `virtual_mailbox_base` 的值和查找映射中的一个值（下一节描述）组成。换句话说，它是 `$virtual_mailbox_base/$mailboxname`。

设置 `virtual_mailbox_base` 参数后，最好实际创建该目录，并使其对在前几节中定义的用户可访问：

```
# mkdir /var/spool/virtual_mailboxes
# chown vuser:vuser /var/spool/virtual_mailboxes
# chmod 700 /var/spool/virtual_mailboxes
```

#### 创建收件人映射

你必须在映射中定义虚拟邮箱域收件人。例如，你可以创建一个名为 `/etc/postfix/virtual_mailbox_recipients` 的文件，左侧是完全限定的收件人地址，右侧是邮箱名。以下是可能的样子：

```
wilma.pebble@example.com        wilmapebble
betty.mcbricker@example.com     bettymcbricker
fred.flintstone@example.com     fredflintstone
barney.rubble@example.com       barneyrubble
bamm.bamm@example.com           bammbamm/
```

虚拟守护进程会将 `virtual_mailbox_base` 参数的值添加到邮箱名前面，以形成完整的邮箱文件路径名。邮箱的默认格式是 mbox 格式，但你可以通过在邮箱名后附加一个斜杠 (`/`) 来指定 Maildir 格式，如前面对 `bamm.bamm@example.com` 的条目所示。

一旦你对这个文件感到满意，就必须通过输入以下命令来构建索引版本：

```
# postmap hash:/etc/postfix/virtual_mailbox_recipients
```

然后，你可以通过在 `main.cf` 中设置 `virtual_mailbox_maps` 参数来告诉 Postfix 在哪里可以找到该映射，如下所示：

```
virtual_mailbox_maps = hash:/etc/postfix/virtual_mailbox_recipients
```

#### 收件人映射限制

出于安全原因，收件人映射有一些限制：

- 虚拟邮箱域收件人不能使用地址扩展，例如 `user+extension@domain.tld`。
- 虚拟守护进程不能像 `local` 那样调用外部程序。
- 允许使用正则表达式映射，但不能使用表达式替换（这意味着你不能在 RHS 中放入 `$1`）。
- 你不能使用 `proxymap` 守护进程执行表查找。

#### 创建别名映射

你可以为虚拟邮箱域设置别名，但必须将它们放在单独的映射中，例如 `/etc/postfix/virtual_mailbox_aliases`。格式要求左侧是完全限定的别名，右侧是完全限定的目标，如下例所示：

```
wilma@example.com        wilma.pebble@example.com
pebble@example.com       wilma.pebble@example.com
...
postmaster@example.com   bamm.bamm@example.com
abuse@example.com        bamm.bamm@example.com
```

与其他映射一样，你必须使用以下命令创建索引版本：

```
# postmap hash:/etc/postfix/virtual_mailbox_aliases
```

最后，通过在你的 `main.cf` 文件中设置 `virtual_alias_maps` 参数来告诉 Postfix 将此映射用于别名，如下所示：

```
virtual_alias_maps = hash:/etc/postfix/virtual_mailbox_aliases
```

重新加载 Postfix 后，你的邮件服务器将接受发送给你虚拟邮箱域收件人的消息。

## 高级配置

如果你需要为多个虚拟邮箱域提供邮件服务，将所有消息存储在单个目录层次结构中可能会引起麻烦，因为可能存在同名用户。此外，单独备份数据会变得非常复杂。为了解决这些问题，你可以配置虚拟邮箱域，将不同域的消息存储在不同的目录中。你还可以选择使用不同的用户 ID (UID) 和组 ID (GID)。

要设置这种高级配置，你必须执行以下操作：

1. 设置虚拟邮箱域的名称。
2. 为虚拟投递代理设置文件所有权。
3. 设置邮箱的基础目录。
4. 创建收件人映射。
5. 创建别名映射。
6. 设置存储和访问权限。

#### 设置虚拟域名

如前面“设置虚拟邮箱域名”一节所述，你使用 `virtual_mailbox_domains` 参数设置虚拟邮箱域名。以下是包含两个域的示例：

```
virtual_mailbox_domains = example.com, postfix-book.com
```

#### 设置文件所有权

对于高级配置，你需要为每个虚拟收件人域创建一组 UID 和 GID。假设你想为 `example.com` 使用用户和组名 `example`，为 `postfix-book.com` 使用 `pfxbook`。请返回“设置文件所有权”一节了解详情；要创建这些用户，你可能会使用以下命令：

```
# useradd example -u 1001
# useradd pfxbook -u 1002
# groupadd example -g 1001
# groupadd pfxbook -g 1002
```

记下这些 UID 和 GID；当你在“设置存储和访问权限”一节中创建查找映射时，很快就会再次用到它们。

#### 设置虚拟邮箱域的基础目录

你需要设置 `virtual_mailbox_base` 参数来告诉虚拟代理应将消息存储在何处，就像在前面“设置虚拟邮箱域基础目录”一节中一样。

让我们使用与该节相同的设置：

```
virtual_mailbox_base = /var/spool/virtual_mailboxes
```

然而，我们在此处执行的操作与之前设置的基本配置之间的区别在于，你必须更改 `virtual_mailbox_base` 的目录权限。否则，虚拟守护进程——在为每个用户和域存储消息时使用不同的 UID 和 GID——将不被允许写入子目录：

```
# mkdir /var/spool/virtual_mailboxes
# chown vuser:vuser /var/spool/virtual_mailboxes
# chmod 775 /var/spool/virtual_mailboxes
```

现在你将需要创建子目录（例如，`example.com` 和 `postfix-book.com`），因为虚拟代理只会创建收件人的 mbox 或 Maildir，而不是其域的父目录。

```
# mkdir example.com
# chown example example.com/
# chgrp example example.com/
# chmod 700 example.com/
```

> **注意** Postfix 2.0 及更早版本不会在全局可写的父目录中创建 Maildir 样式的邮箱；你需要预先创建 Maildir。

如果由于某些权限问题导致邮件投递失败，你将在邮件日志中看到如下消息：

```
May 26 12:04:33 mail postfix/virtual[14196]: warning: maildir access problem
for UID/GID=1002/1002: create /var/spool/mailboxes/postfix-book.com/
patrik/tmp/1085565873.P14196.mail.example.com: Permission denied
May 26 12:04:33 mail postfix/virtual[14196]: warning: perhaps you need to
create the maildirs in advance
```

#### 创建收件人映射

现在你需要为虚拟邮箱域中的有效收件人创建一个映射。此过程与前面“创建收件人映射”一节相同，不同之处在于你需要在邮箱名前加上目录路径。这样，发往不同域的消息将进入不同的目录，因此你无需担心名称冲突。

例如，你可以像这样创建一个 `/etc/postfix/virtual_mailbox_recipients` 文件：

```
wilma.pebble@example.com          example.com/wilmpebble/
betty.mcbricker@example.com       example.com/bettymcbricker/
```



fred.flintstone@example.com       example.com/fredflintstone/
barney.rubble@example.com       example.com/barneyrubble/
bamm.bamm@example.com          example.com/bamm/
ralf@postfix-book.com          postfix-book.com/ralf/
patrick@postfix-book.com        postfix-book.com/patrick/

请记住，在创建映射后，你需要使用以下命令构建索引版本：

```
# postmap hash:/etc/postfix/virtual_mailbox_recipients
```

与之前一样，在你的 `main.cf` 文件中将 `virtual_mailbox_maps` 参数设置为该映射。

```
virtual_mailbox_maps = hash:/etc/postfix/virtual_mailbox_recipients
```

这会处理除别名映射之外的所有收件人，而别名映射的创建方式与前面"创建别名映射"一节所述相同。

#### 设置存储和访问权限

你*无法*像之前"设置文件所有权"一节所描述的那样，为不同的虚拟邮箱域定义单独的存储和访问权限。相反，你必须创建将邮箱与用户 ID 和组 ID 关联起来的映射。

现在你需要用到"设置文件所有权"一节中创建的 UID 和 GID。你必须在 `virtual_uid_maps` 参数指定的映射中为每个邮箱分配一个 UID。例如，你可以通过在 `main.cf` 文件中加入以下行，将映射名称设置为 `hash:/etc/postfix/virtual_uid_map`：

```
virtual_uid_maps = hash:/etc/postfix/virtual_uid_map
```

现在，通过在左侧输入完整的收件人地址，右侧输入 UID，将收件人放入映射中，如本例所示：

```
wilma.pebble@example.com        1001
betty.mcbricker@example.com     1001
fred.flintstone@example.com     1001
barney.rubble@example.com       1001
bamm.bamm@example.com           1001
ralf@postfix-book.com           1002
patrick@postfix-book.com        1002
```

> 注意：别忘了使用 postmap 命令创建映射的索引版本。一个更简短的版本可以是：

```
@example.com 1001
@postfix-book.com 1002
```

GID 映射的工作方式与 UID 映射相同。这里有一个示例映射，你可以将此示例用于 `/etc/postfix/virtual_gid_map` 文件：

```
wilma.pebble@example.com           1001
betty.mcbricker@example.com        1001
fred.flintstone@example.com        1001
barney.rubble@example.com          1001
bamm.bamm@example.com              1001
ralf@postfix-book.com              1002
patrick@postfix-book.com           1002
```

如下所示，在你的 `virtual_gid_maps` 参数中指定此文件：

```
virtual_gid_maps = hash:/etc/postfix/virtual_gid_map
```

> **提示**：*因为在此示例中 `virtual_gid_map` 的条目与 `virtual_uid_map` 的条目完全相同，你可以跳过创建 GID 映射文件的工作，只需在你的 main.cf 中按如下方式引用 UID 映射即可：*

```
virtual_gid_maps = $virtual_uid_maps
```

设置好映射和配置文件后，重新加载 Postfix，以便虚拟守护进程将消息投递到以收件人域命名的子目录中。

#### 使用脚本生成映射

你可能已经注意到，虚拟邮箱至少需要三个映射来查找收件人、邮箱以及所有者和组权限。通过让脚本从一个包含所有必需信息的单一源文件（例如 `/etc/postfix/virtual_build_map_source`）构建所有映射，可以大大简化你的工作。例如，假设源文件包含以下行：

```
wilma.pebble@example.com           example.com/wilmapebble/      1001     1001
betty.mcbricker@example.com        example.com/bettymcbricker/   1001     1001
fred.flintstone@example.com        example.com/fredflintstone/   1001     1001
barney.rubble@example.com          example.com/barneyrubble/     1001     1001
bamm.bamm@example.com              example.com/bammbamm/         1001     1001
ralf@postfix-book.com              postfix-book.com/ralf/        1002     1002
patrick@postfix-book.com           postfix-book.com/patrick/     1002     1002
```

以下脚本（我们称之为 `/etc/postfix/build_virtual_maps`）从映射源读取数据并创建三个目标映射：

```
#!/bin/bash
#
# 从单一源构建所有虚拟邮箱映射
#
# 部分：路径
SOURCE=/etc/postfix/virtual_build_map_source
VMAP=/etc/postfix/virtual_mailbox_recipients
VUID=/etc/postfix/virtual_uid_map
VGID=/etc/postfix/virtual_gid_map
AWK=/usr/bin/awk
POSTMAP=/usr/sbin/postmap
# 部分：构建
# 构建 $virtual_mailbox_maps
$AWK '{printf("%s %s\n",$1,$2)}' $SOURCE > $VMAP
$POSTMAP hash:$VMAP
# 构建 $virtual_uid_maps
$AWK '{printf("%s %s\n",$1,$3)}' $SOURCE > $VUID
$POSTMAP hash:$VUID
# 构建 $virtual_gid_maps
$AWK '{printf("%s %s\n",$1,$4)}' $SOURCE > $VGID
$POSTMAP hash:$VGID
```

**注意**：你可以从《Postfix 之书》网站 http://www.postfix-book.com 下载此脚本。（当然，你可能需要更改开头的路径。）

运行脚本后，除源文件和虚拟别名映射外，所有映射的日期和时间应相同：

```
-rw-r--r-- 1 root root   532 May 26 12:12 virtual_build_map_source
-rw-r--r-- 1 root root   251 May 26 13:21 virtual_gid_map
-rw-r--r-- 1 root root 12288 May 26 13:21 virtual_gid_map.db
-rw-r--r-- 1 root root   394 May 26 13:21 virtual_mailbox_recipients
-rw-r--r-- 1 root root 12288 May 26 13:21 virtual_mailbox_recipients.db
-rw-r--r-- 1 root root   251 May 26 13:21 virtual_uid_map
-rw-r--r-- 1 root root 12288 May 26 13:21 virtual_uid_map.db
```

### 数据库驱动的虚拟邮箱域

如果你对企业或 ISP MTA 感兴趣，可以让 Postfix 访问数据库以获取虚拟邮箱域信息。这种安排特别灵活，因为你可以将用户管理委托给其他人，而无需授予他们服务器的 root 权限。如果你提供一个强大的 Web 界面，你的客户就可以管理自己的数据（添加别名、更改其 SMTP AUTH、POP3 和 IMAP 密码等）。此外，数据库中的数据更改会立即生效，因此你无需在每次更改数据时重新加载 Postfix。

另一方面，索引映射的访问速度更快，并且映射查找不会像 SQL 查询那样消耗大量系统资源，因为你无需运行数据库服务器。此外，数据库驱动的解决方案可能更为复杂。

如果遇到数据库查找的性能问题，你可以设置一个专用的数据库服务器，该服务器可以供网络上的多个 Postfix 服务器（和其他服务）使用。结合轮询等负载均衡机制和专用硬件，你可以构建基于数据库的高性能邮件服务。

本节向你展示如何使用 MySQL 作为数据库来实现数据库驱动的虚拟邮箱域。你需要做的是：

- 1. 检查 Postfix 是否支持 MySQL 映射。
- 2. 构建支持 MySQL 映射的 Postfix。
- 3. 配置数据库。
- 4. 测试数据库驱动的虚拟邮箱域。

> **注意**：数据库驱动的映射不限于在虚拟邮箱域中使用。你可以在许多其他场景中使用它们。Postfix 还支持 PostgreSQL 和 LDAP 查询（PostgreSQL 的配置与 MySQL 几乎相同；LDAP 在第 19 章讨论）。

#### 检查 Postfix 是否支持 MySQL 映射

在配置 Postfix 查询 MySQL 之前，你可能应该验证你的安装是否确实支持此类型的映射。使用 `postconf -m` 命令打印支持的映射类型。如果你有 MySQL 支持，你应该在输出中看到 `mysql`，如本例所示：

```
# postconf -m
btree
cidr
environ
hash
ldap
mysql
nis
pcre
proxy
regexp
sdbm
static
unix
```

如果你的安装中没有 MySQL 支持，你可以安装一个来自操作系统发行版的、支持 MySQL 的 Postfix 包，或者你可以手动构建它，然后安装你的新版本（如下一节所述）。

#### 构建支持 MySQL 映射的 Postfix

要构建具有 MySQL 表支持的 Postfix，首先需要定位 Postfix 构建所需的头文件和库。要查找头文件目录，请使用以下命令：

```
# find /usr -name 'mysql.h'
/usr/include/mysql/mysql.h
```

前面的输出显示，在此特定系统上，头文件位于 /usr/include/mysql。要查找 MySQL 客户端库，请运行以下命令：

```
# find /usr -name 'libmysqlclient.*'
/usr/lib/mysql/libmysqlclient.so.10
/usr/lib/mysql/libmysqlclient.so.10.0.0
/usr/lib/mysql/libmysqlclient.so
/usr/lib/mysql/libmysqlclient.a
```

此处的输出显示库位于 /usr/lib/mysql。

现在你已知道正确的路径，可以为 Postfix Makefile 构建配置过程设置变量。对于本示例中的路径，你将使用以下命令来配置和构建 Postfix：

```
$ make tidy
$ make makefiles CCARGS='-DHAS_MYSQL -I/usr/include/mysql' \
    AUXLIBS='-L/usr/lib/mysql -lmysqlclient -lz -lm'
$ make
```

构建完成并安装 Postfix 后，请按照上一节的描述验证你是否拥有 MySQL 支持。

#### 配置数据库

准备好设置 MySQL 数据库以存储你的虚拟域信息时，请以 root 身份连接到 MySQL 并创建一个数据库。以下命令创建一个名为 `mail` 的数据库：

```
mysql> CREATE DATABASE `mail`;
```

> **提示**：你可以从《Postfix 之书》网站 http://www.postfix-book.com 下载本节的完整 SQL 语句集。如果你需要先了解一些 SQL 语句知识，可以在 http://sqlzoo.net 找到《SQL 简明教程》。



##### 创建收件人域表

创建一个名为 `virtual_mailbox_domains` 的表，用于存储 Postfix 将视为最终目的地的域。你可以使用以下命令：

```sql
CREATE TABLE `virtual_mailbox_domains` (
  `Id` int(10) unsigned NOT NULL auto_increment,
  `domain` varchar(255) default NULL,
  PRIMARY KEY  (`Id`),
  FULLTEXT KEY `domains` (`domain`)
) TYPE=MyISAM COMMENT='Postfix virtual aliases';
```

如果该命令执行成功，你就可以将虚拟域添加到表中。例如，要将 example.com 添加到表中，请输入以下 SQL 命令插入一行：

```sql
INSERT INTO virtual_mailbox_domains VALUES (1,'example.com');
```

##### 添加用户

现在需要创建一个表，其中每一行包含收件人、邮箱名称、UID 和 GID。你可以将其命名为 `virtual_users`；其结构与前面"使用脚本生成映射"一节中使用的 `/etc/postfix/virtual_build_map_source` 文件的列非常相似。

> **注意** _下表基于第 18 章描述的 MySQL SMTP AUTH 表构建。它包含密码和其他信息，因此你可以将其用作 SMTP 认证和虚拟邮箱域的认证后端数据源。_

运行以下命令创建 `virtual_users` 表：

```sql
CREATE TABLE `virtual_users` (
  `id` int(11) unsigned NOT NULL auto_increment,
  `username` varchar(255) NOT NULL default '0',
  `userrealm` varchar(255) NOT NULL default 'mail.example.com',
  `userpassword` varchar(255) NOT NULL default '1stP@ss',
  `auth` tinyint(1) default '1',
  `active` tinyint(1) default '1',
  `email` varchar(255) NOT NULL default '',
  `virtual_uid` smallint(5) default '1000',
  `virtual_gid` smallint(5) default '1000',
  `virtual_mailbox` varchar(255) default NULL,
  PRIMARY KEY  (`id`),
  UNIQUE KEY `id` (`id`),
  FULLTEXT KEY `recipient` (`email`)
) TYPE=MyISAM COMMENT='SMTP AUTH and virtual users';
```

active 字段是可选的；你可以用它来启用或禁用收件人的邮箱（当客户未付款且你需要暂停服务，但又不想丢失账户配置时，这会很有用）。

表创建完成后，你需要添加测试数据。以下是添加示例数据的命令：

```sql
INSERT INTO virtual_users VALUES (5,'bamm.bamm','mail.example.com','1stP@ss',1,1,
'bamm.bamm@example.com',1001,1001,'example.com/bammbamm/');
```

##### 创建虚拟别名表

你需要创建的最后一张表是虚拟别名表。与其他别名映射一样，表的行包含别名名称和真实收件人地址。按如下方式创建一个表（命名为 virtual_aliases）：

```sql
CREATE TABLE `virtual_aliases` (
  `Id` int(10) unsigned NOT NULL auto_increment,
  `alias` varchar(255) default NULL,
  `virtual_user_email` text,
  PRIMARY KEY (`Id`),
  FULLTEXT KEY `aliases` (`alias`,`virtual_user_email`)
) TYPE=MyISAM COMMENT='Postfix virtual recipients';
```

与其他表一样，你应该为其填充一些数据。首先添加 RFC 要求的别名：

```sql
INSERT INTO virtual_aliases VALUES (1,'postmaster@example.com','bamm.bamm@example.com');
INSERT INTO virtual_aliases VALUES (2,'abuse@example.com','bamm.bamm@example.com');
```

##### 为 Postfix 创建 MySQL 用户

配置数据库的最后一步是创建一个用于查询表的 MySQL 用户。你应该限制该用户的权限，使 Postfix 无法修改数据。以下命令添加一个名为 postfix 的新用户，该用户只能从 localhost 连接：

```sql
CONNECT mysql;
INSERT INTO user VALUES
  ('localhost','postfix','','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y');
UPDATE mysql.user SET password=PASSWORD("Yanggt!") WHERE user='postfix' AND
    host='localhost';
FLUSH PRIVILEGES;
```

你需要将该账户限制为只读（SELECT）访问。Postfix 不应能修改或创建表。使用 GRANT 命令来实现：

```sql
GRANT USAGE ON *.* TO 'postfix'@'localhost' IDENTIFIED BY PASSWORD '2fc879714f7d3e72';
GRANT SELECT ON mail.virtual_aliases TO 'postfix'@'localhost';
GRANT SELECT ON mail.virtual_users TO 'postfix'@'localhost';
GRANT SELECT ON mail.virtual_mailbox_domains TO 'postfix'@'localhost';
```

#### 配置 Postfix 使用数据库

为 Postfix 配置 SQL 查询系统时，必须在一个特殊文件中设置以下参数。Postfix 会将这些参数代入一系列 SQL 语句中，最终以一条 SELECT 语句结束：

- **user**：连接数据库的用户名。
- **password**：数据库用户的密码。必须以明文形式提供。
- **hosts**：一个或多个 SQL 服务器的 FQDN 主机名或 IP 地址的列表。如果 Postfix 尝试连接列表中的第一台主机失败，它将按随机顺序尝试其他主机。如果没有可用的服务器，Postfix 会将任务延迟到服务器上线。

    当你使用 localhost 作为服务器时，Postfix 会自动使用 Unix 域套接字而非 TCP/UDP 连接。

- **dbname**：要连接的数据库。
- **table**：包含虚拟域数据的表名。
- **select_field**：包含查询结果的字段（例如用户的电子邮件地址）。
- **where_field**：查询数据库时用于匹配的字段（例如电子邮件别名）。
- **additional_conditions**：查询的附加条件；例如，你可能只想查询当前处于活跃状态的用户账户。此参数是可选的。

表 14-1 展示了索引映射的字段如何对应数据库参数。如果你不确定需要指定哪些表字段，可以参考此表来创建 SELECT 语句。

##### 表 14-1：索引映射字段与数据库参数的对应关系

| 映射类型 | 左侧（LHS） | 右侧（RHS） | 条件 |
| :--- | :--- | :--- | :--- |
| 索引映射 | 左列 | 右列 | - |
| SQL 数据库表 | where_field | select_field | additional_conditions |

#### 保护 Postfix 的 SQL 配置

Postfix 目前支持两种配置 MySQL（和 PostgreSQL）SELECT 语句的方式。

第一种方式要求你在 `main.cf` 文件中写入 Postfix 的 SQL 服务器用户名和密码。由于这种方式安全性较差，本书将不作介绍（`main.cf` 通常对所有用户可读，因此系统上的每个用户都能获取这些凭据）。如果你坚持使用此方法，请参阅 Postfix readme 目录中的 `MYSQL_README` 了解更多信息，但请注意 Postfix 的未来版本将不再支持这种方式。

第二种方式更可取，因为它在安全性方面表现更好。`SELECT` 语句（包括用户名和密码）放在 `main.cf` 之外的独立文件中。此外，你将它们放入一个只有 Postfix 和 `root` 可访问的子目录中（你将在 `main.cf` 中指定文件的位置）。

要设置文件结构，首先创建一个目录，例如 `/etc/postfix/sql`，并设置适当的权限：

```bash
mkdir /etc/postfix/sql
chown postfix /etc/postfix/sql
chgrp root /etc/postfix/sql
chmod 500 /etc/postfix/sql
```

现在你可以在此处添加文件，它们可以免受（大多数）窥探。

#### 构造收件人域查询

你需要添加的第一个文件将定义查询参数，用于检索 Postfix 视为最终目的地的域。将以下配置添加到 `/etc/postfix/sql/virtual_mailbox_domains.cf` 等文件中：

```
user = postfix
password = Yanggt!
dbname = mail
table = virtual_mailbox_domains
select_field = domain
where_field = domain
hosts = localhost
```

如前所述，这些参数对应于 SQL SELECT 语句中的值。上述文件对应的语句如下，其中 *domainpart* 是传入收件人电子邮件地址的域部分：

```sql
SELECT domain FROM virtual_mailbox_domains WHERE domain = '*domainpart*'
```

虽然你已经知道域名，再从表中读取它看起来可能有点奇怪，但这个查询的重点是查看数据库中是否确实存在与域名部分匹配的行。如果不存在，查询就会失败，Postfix 便知道它不是该域名的最终目的地。

> **注意** *你不需要手动输入任何这些 SELECT 语句（Postfix 在访问数据库时会自动构建它们），但当需要在 MySQL 命令行中排查数据库问题时，了解它们会很有帮助。*

现在你需要告诉 Postfix（在 main.cf 中）使用 MySQL，以及在哪里找到 `virtual_mailbox_domains` 的参数。其规范看起来很像常规的索引映射，只是将 `hash` 关键字替换为 `mysql`：

```
virtual_mailbox_domains = mysql:/etc/postfix/sql/virtual_mailbox_domains.cf
```

#### 创建用户 ID 和组 ID 查询

接下来，你需要添加 UID 和 GID 查询的参数（请记住，这些参数定义了虚拟邮箱文件的所有者）。在名为 `/etc/postfix/sql/virtual_uid_maps.cf` 的文件中添加以下行：

```
user = postfix
password = Yanggt!
dbname = mail
table = virtual_users
select_field = virtual_uid
where_field = email
hosts = localhost
```

与该文件对应的 SELECT 语句如下所示（其中 *recipient* 是传入消息的收件人地址）：

```
mysql> SELECT virtual_uid FROM virtual_users WHERE email = 'recipient'
```

在 main.cf 中使用 `virtual_uid_maps` 参数，告诉 Postfix 在哪里可以找到用于查询 UID 的 SQL：

```
virtual_uid_maps = mysql:/etc/postfix/sql/virtual_uid_maps.cf
```

为 GID 创建 SQL 查询的过程与 UID 类似。使用一个文件名（如 `/etc/postfix/sql/virtual_gid_maps.cf`）来创建 SQL SELECT 语句：

```
user = postfix
password = Yanggt!
dbname = mail
table = virtual_users
select_field = virtual_gid
where_field = email
hosts = localhost
```

该文件对应的 SQL SELECT 语句如下：

```
mysql> SELECT virtual_gid FROM virtual_users WHERE email = 'recipient'
```

然后告诉 Postfix 在哪里查找 GID。在 main.cf 中将 `virtual_gid_maps` 参数指向 SQL 查询文件：

```
virtual_gid_maps = mysql:/etc/postfix/sql/virtual_gid_maps.cf
```

#### 创建收件人查询

也许最重要的查询是根据给定的收件人地址检索收件人邮箱名称的查询。将以下查询参数添加到 `/etc/postfix/sql/virtual_mailbox_recipients.cf` 文件中：

```
user = postfix
password = Yanggt!
dbname = mail
table = virtual_users
select_field = virtual_mailbox
where_field = email
additional_conditions = and active = '1'
hosts = localhost
```

注意这里的 `additional_conditions` 参数。此文件中的参数对应以下 SELECT 语句：

```
mysql> SELECT virtual_mailbox FROM virtual_users WHERE email = 'recipient' AND active = '1'
```

`virtual_mailbox_maps` 参数告诉 Postfix 在哪里查找虚拟邮箱收件人及其邮箱。在 main.cf 中，添加以下行：

```
virtual_mailbox_maps = mysql:/etc/postfix/sql/virtual_mailbox_recipients.cf
```

#### 创建别名查询

最后，是时候指定虚拟别名查询的参数了。将以下行放入一个文件中，例如 `/etc/postfix/sql/virtual_alias_maps.cf`：

```
user = postfix
password = Yanggt!
dbname = mail
table = virtual_aliases
select_field = virtual_user_email
where_field = alias
hosts = localhost
```

这是与上述文件对应的 SELECT 语句：

```
mysql> SELECT virtual_user_email FROM virtual_aliases WHERE alias = 'recipient'
```

作为收尾，通过 main.cf 中的 `virtual_alias_maps` 参数告诉 Postfix 在哪里可以找到别名查询配置文件：

```
virtual_alias_maps = mysql:/etc/postfix/sql/virtual_alias_maps.cf
```

重新加载 Postfix，使 main.cf 中的所有更改生效，然后开始测试。

#### 测试数据库驱动的虚拟邮箱域名

如果你无法判断问题出在 Postfix 还是 MySQL 上，排查问题可能会变得相当繁琐。这就是为什么你应该分别测试 MySQL 和 Postfix。如果 MySQL 测试通过，那么你就知道问题出在 Postfix 的配置上。

##### 测试 MySQL

你首先应该测试的是，在查询配置文件中提供的用户名和密码是否被允许访问 MySQL 并执行查询。

然后尝试连接到存储虚拟邮箱域名数据的数据库。两个测试都将在此示例中展示：

```
# mysql -u postfix -p -h localhost -A
```

成功登录后，你将看到以下输出：

```
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 144 to server version: 3.23.58
Type 'help;' or '\h' for help. Type '\c' to clear the buffer.
mysql>
```

使用 `CONNECT` 语句访问 mail 数据库，你应该会看到类似以下的确认信息：

```
mysql> CONNECT mail;
Connection id:    145
Current database: mail
mysql>
```

如果你无法连接到服务器，请检查你在前面"为 Postfix 创建 MySQL 用户"部分中指定给 MySQL 的用户名和密码。另一方面，如果你在连接 mail 数据库时遇到问题，请检查 GRANT 语句（在同一部分中）。

##### 查询收件人域名

现在是时候运行一条 SELECT 语句来验证你的 Postfix MySQL 用户是否能在 `virtual_mailbox_domains` 表中查找虚拟邮箱域名了。输入如下命令：

```
mysql> SELECT domain FROM virtual_mailbox_domains WHERE domain = 'example.com';
```

如果成功，你应该看到一行输出，其中包含查询输入（回顾"构建收件人域名查询"部分，这是正确的行为）：

```
+--------------+
| domain       |
+--------------+
| example.com  |
+--------------+
1 row in set (0.00 sec)
```

如果没有匹配结果，请检查该域名是否存在于你的表中。一个简单的检查方法是省略 WHERE 子句来检索表中的所有行：

```
mysql> SELECT domain FROM virtual_mailbox_domains;
```

##### 查询虚拟邮箱 UID 和 GID

接下来，验证你的 MySQL 用户是否能够检索已知的收件人地址。尝试从 `virtual_users` 表中已知的收件人地址检索 `virtual_uid` 字段，如下所示的成功示例，它展示了 bamm.bamm@example.com 到虚拟邮箱 UID 1001 的映射：

```
mysql> SELECT virtual_uid FROM virtual_users WHERE email =
    'bamm.bamm@example.com';
+-------------+
| virtual_uid |
+-------------+
|        1001 |
+-------------+
1 row in set (0.00 sec)
```

对 GID 执行同样的操作：

```
mysql> SELECT virtual_gid FROM virtual_users WHERE email =
    'bamm.bamm@example.com';
+------------+
| virtual_gid |
+------------+
|        1001 |
+------------+
1 row in set (0.00 sec)
```

##### 查询收件人邮箱

测试 Postfix MySQL 用户是否能为给定的收件人查找邮箱。请记住，这就是 `virtual_users` 表中的 `virtual_mailbox`。以下示例将 bamm.bamm@example.com 映射到 Maildir 风格的邮箱 example.com/bammbamm/：

```
mysql> SELECT virtual_mailbox FROM virtual_users WHERE email = 'bamm.bamm@example.com';
+----------------------+
| virtual_mailbox      |
+----------------------+
| example.com/bammbamm/ |
+----------------------+
1 row in set (0.00 sec)
```

###### 查询别名

你最后的数据库检查是针对别名的。对于一个已知的别名，检索收件人地址（`virtual_aliases` 表中的 `virtual_user_email` 字段）。以下是示例：

```
mysql> SELECT virtual_user_email FROM virtual_aliases WHERE alias = 'postmaster@example.com';
+---------------------+
| virtual_user_email  |
+---------------------+
| bamm.bamm@example.com |
+---------------------+
1 row in set (0.00 sec)
```

##### 测试 Postfix

你无需发送任何测试邮件即可测试 Postfix 的 MySQL 查询。`postmap` 命令可以执行任何类型的查询，包括 MySQL 表中的查询。以下是执行 MySQL 查询的 `postmap` 命令的通用格式：

```
# postmap -q "value" mysql:path-to-parameter-file
```



例如，以下是如何指示 Postfix 查询 MySQL 以获取已知的虚拟邮箱域：

```
# postmap -q "example.com" mysql:/etc/postfix/sql/virtual_mailbox_domains.cf
```

如果操作成功，与查询匹配的数据应显示在命令行上：

```
example.com
```

如果没有返回结果，请检查该虚拟域名是否存在于你的表中（请参阅前面的“查询收件人域”部分）。如果该测试成功，请核实你的 `virtual_mailbox_domains.cf` 文件中的用户名和密码信息。

###### 查询 UID 和 GID

为了继续测试，请指示 Postfix 查询 MySQL 以获取已知虚拟邮箱收件人的 UID 和 GID：

```
# postmap -q "bamm.bamm@example.com" mysql:/etc/postfix/sql/virtual_uid_maps.cf
1001
# postmap -q "bamm.bamm@example.com" mysql:/etc/postfix/sql/virtual_gid_maps.cf
1001
```

###### 查询收件人

接下来，验证 Postfix 能否查询已知收件人。对应于前面“查询收件人邮箱”部分中 `SELECT` 语句的 `postmap` 命令如下所示：

```
# postmap -q "bamm.bamm@example.com" mysql:/etc/postfix/sql/virtual_mailbox_recipients.cf
example.com/bammbamm/
```

###### 查询别名

你的最终测试是指示 Postfix 查询 MySQL 以获取已知别名的虚拟用户电子邮件地址。成功的查询如下所示：

```
# postmap -q "postmaster@example.com" mysql:/etc/postfix/sql/virtual_alias_maps.cf
bamm.bamm@example.com
```

# 15

# 理解 SMTP 认证

SMTP 认证是一种独立于客户端 IP 地址来识别邮件客户端的方法，这使得服务器可以为那些 IP 地址不被服务器信任的邮件客户端中继消息。本章是 SMTP 认证（SMTP AUTH）的入门指南。你不仅将了解 SMTP 认证及其相对于其他方法的优势，还将看到如何安装和配置 Cyrus SASL——这是在 Postfix 中支持 SMTP 认证所需的一个软件包。

## Cyrus SASL 的架构和配置

在早期，SMTP 服务器会将来自任何客户端的邮件转发到任何目的地。当垃圾邮件成为问题时，MTA 必须扩展功能，以仅接受来自特定客户端的邮件转发请求。MTA 实现者决定通过 IP 地址来识别这些特定客户端，然后管理员必须配置他们的系统以拒绝不受信任的客户端（参见图 15-1）。

如今，邮件中继滥用尝试仍然是日常的烦扰，管理员花费大量时间通过进一步的限制来加固他们的服务器（参见第 8 章）。然而，在当今使用的超大规模分布式网络中，基于 IP 地址来控制中继访问是困难的，并且对于移动用户来说完全不可行。

移动用户（在 RFC 2977 中定义）需要在互联网上的任何位置访问其自身域的资源。不幸的是，移动用户几乎从不使用相同的 IP 地址，而且，移动用户和管理员永远无法提前知道他们的 IP 地址，这使得基于静态 IP 地址的规则变得无效。

有几种允许移动用户中继访问的方法：

-   SMTP-after-POP 和 SMTP-after-IMAP
-   SMTP 认证
-   基于证书的中继
-   虚拟专用网络（VPN）

SMTP-after-POP 或 SMTP-after-IMAP 方法（参见图 15-2）将识别问题委托给 POP 或 IMAP 服务器。

以下是 SMTP-after-POP 或 SMTP-after-IMAP 方法的基本步骤：

1.  邮件客户端向 POP 或 IMAP 服务器进行身份验证。
2.  验证成功后，POP 或 IMAP 服务器将邮件客户端的 IP 地址写入与邮件服务器共享的数据库。该 IP 地址在数据库中保留有限的时间。
3.  邮件客户端尝试通过 SMTP 服务器中继消息。
4.  SMTP 服务器在数据库中查找邮件客户端的 IP 地址。如果该 IP 地址在数据库中，服务器允许中继。

SMTP 认证从根源上解决了问题（参见图 15-3）。以下是 SMTP AUTH 方法的基本步骤：

1.  SMTP 服务器向邮件客户端提供 SMTP AUTH。
2.  客户端将其凭据传递给服务器。
3.  服务器验证凭据，如果凭据有效，则允许中继。

基于证书的中继（在第 18 章中介绍）基于 TLS 客户端证书的交换和验证（参见图 15-4）。以下是基于证书的中继的基本步骤：

1.  SMTP 服务器向邮件客户端提供 TLS 连接。
2.  客户端将其证书发送给服务器。
3.  服务器验证证书，如果该证书是服务器认可的证书之一，则允许客户端中继。

虚拟专用网络（VPN）通过建立在常规互联网之上的安全虚拟网络，使客户端能够访问邮件服务器。在 VPN 中，管理员可以控制 IP 地址，因此你可以使用基于 IP 地址的中继。由于 VPN 配置与 SMTP 服务器配置无关，因此本书不涉及此内容。使用 VPN 的基本步骤如下：

1.  邮件客户端的计算机连接到 VPN。
2.  SMTP 服务器根据客户端在虚拟网络中的 IP 地址允许其进行中继。

## 哪种方法最好？

使用 TLS 的基于证书的中继非常棒，因为它提供了高级别的安全性，但许多邮件客户端还不支持它。此外，在客户端和服务器上管理证书的开销也不容小觑。这两个因素构成了在公司范围或 ISP 范围内推广的重大障碍。如果你还不能使用证书进行中继，你的选择就简化为 SMTP-after-POP、SMTP AUTH 和 VPN。

从系统架构师的角度来看，SMTP-after-POP 远非理想方案，因为该解决方案甚至不在问题所在的服务器和协议内部。相反，由另一台服务器（至少与 SMTP 服务器一样复杂的 POP 或 IMAP 服务器）提供了一个权宜之计。这使事情变得复杂，因为两台服务器必须相互通信，而且由于这些服务器几乎肯定是由不同的人员开发的，因此存在很高的不兼容风险，尤其是在新版本出现时。

SMTP-after-POP 的设计并非其唯一的缺点。由于其基于 IP 地址的决策机制，它实际上并没有提供非常好的安全性。伪造 IP 地址并不困难——攻击者可以发现一个刚刚被授予某个时间段中继权限的邮件客户端的 IP 地址，并在该时间段过去之前伪造该 IP 地址。当客户端必须为其想要发送的每条新消息进行身份验证时，这种滥用就无法发生。

如果你已经拥有 VPN，那么基于 VPN 的系统非常容易设置，但仅为邮件服务器设置 VPN 需要付出巨大的努力。此外，VPN 需要持续维护，因为每个新的移动用户都需要 VPN 软件。

如果你想要简单、独立且安全的解决方案，SMTP AUTH 可能适合你。

## SASL：简单认证和安全层

Postfix 在 SASL（简单认证和安全层）的帮助下实现了 SMTP 认证。SASL 是在 RFC 2222 中描述的一个认证框架，理解其工作原理对于整体理解 SMTP 认证至关重要。有多种 SASL 实现，Postfix 使用源自 Project Cyrus 中原始 SASL 实现的 Cyrus-SASL 库。

> 注意：*Project Cyrus 是卡内基梅隆大学构建新校园邮件系统的项目的名称。更多信息请参见 http://asg.web.cmu.edu/cyrus。*

SASL 由三个需要配置的层组成。图 15-5 展示了这三层：认证接口、机制和方法。

在使用 Cyrus SASL 框架的应用程序中，认证过程需要以下步骤：

1.  支持 SASL 的应用程序（如 Postfix 的 `smtpd` 守护进程）监听网络连接。
2.  客户端连接并启动认证，包含以下四个子步骤：
    a. 客户端选择一个 SMTP AUTH 机制。
    b. 客户端根据机制的要求准备传输其凭据。
    c. 客户端告诉服务器它选择了哪个机制。
    d. 客户端传输凭据。
3.  应用程序存储关于所选机制和凭据的信息。
4.  应用程序将信息移交给机制驱动程序，后者将其传递给密码验证服务。
5.  密码验证服务访问一个认证后端，例如 `/etc/shadow`。后端尝试将其条目之一与客户端的凭据进行匹配。



![](img/852c79f689feb77c5fde686b993808b1_250_0.png)

图 15-5：SASL 层

-   6. 密码验证服务将后端返回的结果传递给 smtpd。
-   7. smtpd 根据结果采取相应操作。例如，它可以让通过认证的用户转发邮件。

以下各节将更详细地介绍 Cyrus SASL。你将全面了解 SASL 认证接口、方法、机制和认证后端，以及如何准备 Cyrus SASL 和 Postfix 以提供服务器端 SMTP AUTH。

### 认证接口

认证接口的作用是告知客户端认证可用以及可以使用哪些认证机制。许多服务（仅举几例，如 LDAP 或 SMTP）可能需要认证，但它们的客户端-服务器协议各不相同。因此，SASL 没有自己的认证接口，而是将认证能力如何引起客户端注意的问题留给具体的服务及其协议来整合。

对于电子邮件而言，客户端和服务器交汇的地方就是 SMTP 对话。ESMTP 协议通过将认证添加到邮件服务器的功能列表中，将其集成到对话中。你可以通过连接到服务器并使用 EHLO 问候语来查看邮件服务器是否提供 SMTP AUTH 功能，如下所示：

```
$ telnet mail.example.com 25
220 mail.example.com ESMTP Postfix
EHLO client.example.com
250-mail.example.com
250-PIPELINING
250-SIZE 20480000
250-VRFY
250-ETRN
250-AUTH PLAIN LOGIN
250-AUTH=PLAIN LOGIN
250-XVERP
250 8BITMIME
QUIT
221 Bye
```

上述输出中的粗斜体行表示支持 PLAIN 和 LOGIN 认证机制的 SMTP 认证。第二行（带等号的那行）是为那些不遵循最终 SASL 规范的有缺陷的邮件客户端而存在的。

> **注意** *认证接口是在提供 SMTP AUTH 的应用程序中配置的。在 Postfix 中，这个应用程序就是 smtpd 守护进程；你将在第 16 章中看到如何配置该接口。*

### SMTP AUTH 机制

SMTP AUTH 机制（如 PLAIN 和 LOGIN）定义了认证过程中使用的验证策略。服务器提供的机制会显示在应用接口中；在本例中就是 SMTP 对话。发起认证时，客户端选择一种机制，将其选择发送给服务器，然后传输其凭据。

Cyrus SASL 提供了多种 SASL 机制，它们在凭据传输方式和安全级别上各不相同。其中一些是非标准的，专为特定客户端设计。你不必使用所有可用的机制；你可以配置 Postfix 只提供有限范围的 Cyrus SASL 机制。

> **提示** *在实践中，最好在需要支持 Windows、Mac OS 和 Unix 客户端的环境中使用 PLAIN、LOGIN 和 CRAM-MD5。*

以下是各机制：

#### ANONYMOUS

ANONYMOUS 机制（在 RFC 2245 中定义）是为了允许对邮件服务的匿名访问而创建的。使用此机制时，邮件客户端只需向服务器发送任意字符串，服务器就会允许该客户端进行中继。

> **注意** *除非你希望邮件服务器成为开放中继，否则不要在 Postfix 中使用 ANONYMOUS 机制。垃圾邮件发送者知道如何滥用此机制。*

#### CRAM-MD5、DIGEST-MD5

Cyrus SASL 库支持两种"共享密钥"机制：CRAM-MD5 及其后续者 DIGEST-MD5。这些方法依赖于客户端和服务器共享一个密钥，通常是密码。服务器根据该密钥生成质询，客户端做出响应，从而证明它知道共享密钥。这比简单地在网络上发送未加密的密码安全得多，但服务器仍然需要存储密钥。

#### EXTERNAL

EXTERNAL 机制允许你将 TLS/SSL 凭据绑定到 SASL。具体而言，EXTERNAL 机制允许你从 TLS/SSL 协商期间使用的证书中提取某种形式的用户名。

#### GSSAPI、KERBEROS_V4

Cyrus SASL 库附带了两种利用 Kerberos 认证系统的机制：KERBEROS_V4（应该能够使用任何 Kerberos v4 实现）和 GSSAPI（针对 MIT Kerberos v5 和 Heimdal Kerberos v5 进行了测试）。由于这些机制利用了 Kerberos 基础设施，它们不需要密码数据库。

> **注意** *遗憾的是，KERBEROS_V4 存在一些安全问题。请改用 GSSAPI。*

#### NTLM

NTLM 机制是一种由 Microsoft 开发的非标准、未文档化的机制。SASL 发行版中包含此机制，以便需要与 Microsoft 客户端（如 Outlook）和服务器（如 Exchange）互操作的站点使用。

#### OTP

一次性密码（OTP）机制与 CRAM-MD5 和 DIGEST-MD5 类似，使用共享密钥和质询/响应交换。然而，OTP 被认为比其他共享密钥机制更安全，因为该密钥用于生成和存储一系列一次性（单次使用）密码，以防止重放攻击，因此你不需要在服务器上存储密钥。

#### PLAIN、LOGIN

使用 PLAIN 作为机制发送的凭据以 base64 编码的明文形式传输。此机制简单，大多数邮件客户端都实现了它，但 base64 编码的字符串可以轻松解码。LOGIN 与 PLAIN 相同，但它用于不遵循 RFC 的邮件客户端（如 Outlook Express）。

> **注意** *凭据以明文形式通过网络发送这一事实会带来安全风险。任何运行嗅探器（如 snort 或 tcpdump）的人都可以读取这些密钥。你可以通过将 TLS 与明文 SMTP 认证结合使用来解决此问题。具体而言，你可以告诉 Postfix 仅在建立 TLS 会话后才提供明文机制（参见第 18 章）。*

#### SRP

SRP 将共享密钥认证的安全性与 OTP 的一次性使用特性相结合。它基于公钥密码学，并在认证过程中依赖密码（而非证书）。

### 认证方法（密码验证服务）

认证方法（也称为密码验证服务）处理各种机制，负责提供 SMTP 认证的应用程序与存储凭据的后端之间的通信。

Cyrus SASL 提供两种密码验证服务：saslauthd 和 auxprop。这两种服务在可提供的机制和可连接的后端方面有所不同。通过其接口提供认证的应用程序必须选择使用哪种密码验证服务。（你将在后面的"Cyrus SASL 的安装和配置"部分看到相关配置。）以下是这些服务的概述：

-   **saslauthd**
    saslauthd 是一个独立的守护进程，可以以超级用户权限运行。它可以连接到多种类型的认证后端，尤其是那些需要超级用户权限的后端，如 `/etc/shadow`。saslauthd 仅限于明文机制（PLAIN 和 LOGIN）。

-   **auxprop**
    auxprop 是针对多种辅助插件的通用密码验证服务。每个插件专门针对一种特定类型的认证后端，如 sasldb2 和 SQL 服务器。

> **注意** *auxprop 插件以提供认证的应用程序的权限连接到认证后端。在 Postfix 中，该应用程序是 smtpd，它以所需的最少权限运行。*

*2.x 之前的 Cyrus SASL 版本允许使用 auxprop 访问 `/etc/shadow`。这需要增加提供 SMTP AUTH 的守护进程的权限，从而破坏了 Postfix 的安全架构。强烈建议你不要使用迫使你增加应用程序权限的后端。*

### 认证后端

作为最后一步，Cyrus SASL 需要一个或多个认证后端来验证客户端提供的凭据。密码验证服务检查凭据是否与认证后端中存储的内容匹配。Cyrus SASL 支持的官方认证后端列表包括以下内容：

-   **imap**
    IMAP 服务器可以验证凭据。

-   **kerberos**
    Cyrus SASL 可以检查 Kerberos 票据。

-   **ldap**
    Cyrus SASL 可以从 OpenLDAP 服务器读取凭据。

-   **pam**
    Cyrus SASL 可以从你通过 PAM（可插拔认证模块）提供的任何模块读取凭据。



## 规划服务器端 SMTP 身份验证

如果你想在邮件服务器上支持 SMTP 身份验证，只需执行两个步骤：

1.  确定将使用 SMTP AUTH 的客户端以及这些客户端支持的机制。
2.  定义你希望使用的身份验证后端，并推导出相应的密码验证服务。

### 查找客户端及其支持的机制

计算机安全的一个原则是，你无法攻击一个不存在的服务。因此，你应考虑仅为用户所需的机制配置 Postfix。在一个你能良好控制所使用邮件客户端的小型网络中，你可以非常有效地限制机制。表 15-1 是 Alexey Melnikov 的 SASL 客户端参考手册 (http://www.melnikov.ca/mel/devel/SASL_ClientRef.html) 的简化版本，它列出了各种邮件客户端支持的机制。它相当全面地概述了邮件客户端的 POP、IMAP、ACAP 和 LDAP AUTH 功能。

然而，如果你需要支持尽可能多的客户端，请至少提供 PLAIN、LOGIN 和 CRAM-MD5 机制。大多数邮件客户端都支持这些。

> **注意** *你可能会注意到表 15-1 中列出的机制比 SASL 客户端参考手册中少。机制实在太多，因此有必要对 SASL 客户端参考手册进行删减，但表 15-1 中列出的机制将在异构 IT 环境中为你提供最大的收益。*

确定你需要支持邮件客户端的机制后，你需要选择合适的身份验证后端。

**passwd/shadow**
Cyrus SASL 可以从系统用户数据库（/etc/passwd 以及可能的 /etc/shadow）中读取数据。

**sasldb2**
Cyrus SASL 有一个名为 sasldb2 的自身用户数据库。Cyrus IMAP 服务器需要此数据库，但你无需 IMAP 服务器即可将其与 SMTP 身份验证一起使用。

**sql**
Cyrus SASL 可以访问 SQL 服务器上的用户数据。当前支持的服务器是 MySQL 和 PostgreSQL。

### 表 15-1：支持 SMTP AUTH 的客户端的机制

| 客户端 | ANONYMOUS | CRAM-MD5 | DIGEST-MD5 | EXTERNAL | GSSAPI | Kerberos 4 | LOGIN | NTLM | PLAIN | SCRAM-MD5 | SKEY |
|---|---|---|---|---|---|---|---|---|---|---|---|
| AKmail | 否 | 是 | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 |
| Bat! (SecureBat!) | 否 | 是 | 是 | 否 | 否 | 否 | 是 | 否 | 是 | 否 | 否 |
| Control Data’s IMAPSP | 否 | 是 | 否 | 否 | 否 | 否 | 否 | 否 | 是 | 否 | 是 |
| Eudora Pro 4.3 及更高版本 | 否 | 是 | 否 | 否 | 否 | 否 | 是 | 否 | 是 | 否 | 否 |
| fetchmail 5.0.3 | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 |
| Forte Agent | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 |
| Gnus | 否 | 是 | 否 | 否 | 否 | 否 | 是 | 否 | 否 | 否 | 否 |
| JavaMail | 否 | 否 | 否 | 否 | 否 | 否 | 是 | 否 | 是 | 否 | 否 |
| MH UCI 6.8.3 | ? | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 |
| Mozilla 1.0 | 否 | 是 | 否 | 是 | 否 | 否 | 否 | 否 | 是 | 否 | 否 |
| Mulberry v3 | 否 | 是 | 是 | 否 | 是 | 否 | 是 | 是 | 是 | 否 | 否 |
| mutt 1.2.5i | 不适用¹ | 不适用 | 不适用 | 不适用 | 不适用 | 不适用 | 不适用 | 不适用 | 不适用 | 不适用 | 不适用 |
| Netscape Messenger 4.51+ | 否 | 否 | 否 | 是 | 否 | 否 | 否 | 否 | 是 | 否 | 否 |
| nmh 1.0.4 | —² | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 |
| Novell Evolution | 否 | 是 | 是 | 否 | 否 | 是 | 否 | 是 | 是 | 否 | 否 |
| Orangsoft Winbiff > 2.30 | 否 | 是 | 否 | 否 | 否 | 否 | 是 | 否 | 是 | 否 | 否 |
| Outlook Express > 4.0³ | 否 | 否 | 否 | 否 | 否 | 否 | 是 | 是 | 否 | 否 | 否 |
| Outlook > 98³ | 否 | 否 | 否 | 否 | 否 | 否 | 是 | 是 | 否 | 否 | 否 |
| Paladin | 否 | 是 | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 |
| PalmOS Eudora | 否 | 是 | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 |
| Pegasus Mail 3.12 | 否 | 是 | 否 | 否 | 否 | 否 | 是 | 否 | 否 | 否 | 否 |
| Pine 4.33 及更高版本 | 否 | 是 | 否 | 否 | 是 | 是 | 是 | 否 | 是 | 否 | 否 |
| PMMail | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 | 否 |
| Sylpheed | 否 | 是 | 是 | 否 | 否 | 否 | 是 | 否 | 否 | 否 | 否 |
| Wanderlust | 是 | 是 | 是 | 否 | 否 | 是 | 是 | 否 | 否 | 是 | 否 |

¹ 不直接支持 SMTP；依赖于本地 MTA。
² 参见 CMU SASL 库。
³ 支持 SMTP AUTH 规范的草案 10（即支持 "AUTH=" 但不支持 "AUTH "）。

### 定义身份验证后端和密码验证服务

一个容易但不是特别安全的获取用户凭证的地方是你系统的本地用户数据库 /etc/passwd。此身份验证后端已经存在，除非你是 ISP，否则你可能已经为所有邮件用户创建了帐户。

不幸的是，太多管理员创建了允许 shell 访问的用户帐户。任何获得 SMTP AUTH 会话中使用的用户名和密码的人，都可以轻松获得对你服务器的 shell 访问（结果是，他们很可能也能获得超级用户访问权限，因为当你已经拥有一个 shell 帐户时，这要容易得多）。仅此一点就足以成为选择一个与系统用户无关的身份验证后端的理由。

理论上，理想的身份验证后端与系统用户无关，特别是如果你使用明文机制，因为凭证被泄露仅用于邮件中继的后果与系统入侵相比并不严重。你可以使用独立的数据库，例如 sasldb、SQL 服务器，甚至是 LDAP 服务器。表 15-2 和 15-3 确定了你可以为每种类型的身份验证后端使用的机制。请注意，你选择的后端也决定了你必须使用的密码验证服务。

### 表 15-2：与 sasldauthd 密码验证服务兼容的身份验证后端和机制

| 身份验证后端 | PLAIN | LOGIN | CRAM-MD5 | DIGEST-MD5 | OTP | NTLM |
| --- | --- | --- | --- | --- | --- | --- |
| getpwent（常规系统用户） | 是 | 是 | 否 | 否 | 否 | 否 |
| kerberos | 是 | 是 | 否 | 否 | 否 | 否 |
| pam | 是 | 是 | 否 | 否 | 否 | 否 |
| rimap（远程 IMAP 服务器） | 是 | 是 | 否 | 否 | 否 | 否 |
| shadow | 是 | 是 | 否 | 否 | 否 | 否 |
| ldap | 是 | 是 | 否 | 否 | 否 | 否 |

### 表 15-3：与 auxprop 密码验证服务兼容的身份验证后端和机制

| 身份验证后端 | PLAIN | LOGIN | CRAM-MD5 | DIGEST-MD5 | OTP | NTLM |
| --- | --- | --- | --- | --- | --- | --- |
| sasldb2 | 是 | 是 | 是 | 是 | 是 | 是 |
| sql | 是 | 是 | 是 | 是 | 是 | 是 |

决定身份验证后端后，你就可以为 smtpd 配置 Cyrus SASL 了。

## 安装和配置 Cyrus SASL

Postfix 需要 Cyrus SASL 来向邮件客户端提供 SMTP AUTH 功能，或者当远程邮件服务器提供 SMTP AUTH 时，自身使用它。

如果你只需要配置 Postfix smtp 客户端以向远程服务器进行身份验证，你需要做的就是安装 Cyrus SASL 并继续阅读第 16 章。

但是，如果你想让作为 MTA 的 Postfix 向远程邮件客户端提供 SMTP AUTH，你需要安装并配置 Cyrus SASL。此外，当你想使用服务器端 SMTP AUTH 时，需要告诉 Postfix 如何与 Cyrus SASL 交互。总的来说，你需要执行以下操作：

1.  安装 Cyrus SASL。
2.  创建 Postfix 应用程序配置文件。
3.  配置日志记录和日志级别。
4.  设置密码验证服务。
5.  选择 SMTP AUTH 机制。
6.  配置 saslauthd 或 auxprop。
7.  测试身份验证。

### 安装 Cyrus SASL

如果你的系统没有预装 Cyrus SASL 或没有将其作为软件包提供，你需要从下载 Cyrus 软件网页 http://asg.web.cmu.edu/cyrus/download 下载 Cyrus SASL 库。

> 以下部分假设你使用的至少是 Cyrus SASL 2.1.17，但当你阅读本文时，使用更新版本也是自然的。如果你想获取 2.1.17 版本，可以从 CVS 存储库 http://asg.web.cmu.edu/cyrus/download/anoncvs.html 获取。

解压软件后，进入 Cyrus SASL 源代码目录。如果你使用的是从 CVS 获取的 SASL 版本，你需要运行 `sh ./SMakefile` 来构建 configure 脚本。

运行以下命令为本章其余部分描述的所有后端配置 Cyrus SASL：

```
# ./configure \
    --with-plugindir=/usr/lib/sasl2 \
    --disable-java \
    --disable-krb4 \
    --with-dblib=berkeley \
    --with-saslauthd=/var/state/saslauthd \
    --without-pwcheck \
    --with-devrandom=/dev/urandom \
    --enable-cram \
    --enable-digest \
    --enable-plain \
```



### 创建 Postfix 应用配置文件

每个提供 SASL 服务的应用程序都必须指定如何使用 SASL 库。Cyrus SASL 为每个应用程序提供一个配置文件，而不是一个大型的全局配置文件。这使得为不同的应用程序定义不同的配置成为可能。Postfix 的应用程序配置文件名为 `smtpd.conf`，因为默认情况下提供 SASL 服务的 Postfix 应用程序是 `smtpd` 守护进程。该文件默认位于 `/usr/lib/sasl2` 目录下。

> **注意** *Debian 用户必须将 `smtpd.conf` 放在 `/etc/postfix/sasl` 目录下才能使 SMTP AUTH 正常工作。*

某些操作系统自带一个包含若干默认设置的 `smtpd.conf` 文件；请事先检查该文件是否存在。如果文件不存在，请以 root 身份执行以下命令创建它：

```
# touch /usr/lib/sasl2/smtpd.conf
# chmod 644 /usr/lib/sasl2/smtpd.conf
```

上述命令不会损坏已有的配置文件。创建配置文件后，就可以开始配置 Postfix 如何使用 SASL 库了。

Cyrus 配置文件的语法与 Postfix 不同。参数及其值必须在同一行中。在 Cyrus 中，每个参数以冒号结尾，参数与其值之间用空格分隔。

### 配置日志和日志级别

你应该在 `/usr/lib/sasl2/smtpd.conf` 文件中配置的第一个参数是 `log_level` 参数。其可选值列于表 15-4 中。

#### 表 15-4：Cyrus SASL 日志级别值

| log_level 值 | 描述 |
|---|---|
| 0 | 不记录日志 |
| 1 | 记录异常错误；这是默认值 |
| 2 | 记录所有认证失败 |
| 3 | 记录非致命警告 |
| 4 | 比 3 更详细 |
| 5 | 比 4 更详细 |
| 6 | 记录内部协议跟踪信息 |
| 7 | 记录内部协议跟踪信息，包括密码 |

在配置和测试 Cyrus SASL 时，你应该将日志级别至少设置为 3。以下是在 `smtpd.conf` 文件中设置的方法：

```
# Global parameters
log_level: 3
```

随着后续各节内容的深入，该文件会逐步扩展。

### 设置密码验证服务

下一步是告诉 Postfix 使用哪个密码验证服务来认证用户。此时，你应该在 `saslauthd` 和 `auxprop` 之间做出明确的选择，因为后续步骤会因密码验证服务的不同而有很大差异。Cyrus SASL 通过 `pwcheck_method` 参数来确定密码验证服务。如果你计划使用 `saslauthd`，请按如下方式配置 `smtpd.conf`：

```
# Global parameters
log_level: 3
pwcheck_method: saslauthd
```

如果你计划使用辅助插件，请在 `smtpd.conf` 中使用以下配置：

```
# Global parameters
log_level: 3
pwcheck_method: auxprop
```

### 选择 SMTP AUTH 机制

Cyrus SASL 由客户端来选择用于认证的机制。这在以下情况下可能导致认证失败：

- 如果你提供了需要配置但尚未完成的配置的机制。例如，如果你没有使用 Kerberos，但服务器提供了 KERBEROS 机制且客户端选择了它，认证将会失败。
- 如果你选择了 saslauthd 作为密码验证服务，但未将机制限制为明文机制。在这种情况下，如果选择了非明文机制，认证将会失败，因为 saslauthd 无法处理 PLAIN 和 LOGIN 以外的机制。

你可以通过 `mech_list` 参数确保服务器只提供特定的机制列表。例如，如果你使用的是 saslauthd，你的 smtpd.conf 文件*必须*如下所示：

```
# Global parameters
log_level: 3
pwcheck_method: saslauthd
mech_list: PLAIN LOGIN
```

使用辅助插件时，你可以选择不同的列表，例如：

```
# Global parameters
log_level: 3
pwcheck_method: auxprop
mech_list: PLAIN LOGIN CRAM-MD5 DIGEST-MD5
```

机制选择完成后，你现在需要配置 saslauthd 或辅助插件。如果你想配置 saslauthd，请继续阅读下一节；如果要配置 auxprop，请跳转到"配置辅助插件（auxprop）"部分。

### 配置 saslauthd

saslauthd 是一个独立的守护进程，负责与认证后端通信。你通过命令行选项来配置 saslauthd。在启动守护进程之前，请执行以下步骤。

1. 检查你的 saslauthd 支持的认证后端。
2. 准备 saslauthd 运行环境。
3. 为 saslauthd 配置一个认证后端。

#### 检查支持的认证后端

如果 saslauthd 不支持你想使用的认证后端，后续工作将无法顺利进行。运行 `saslauthd -v` 可以获取你的 saslauthd 二进制文件支持的认证后端列表。示例如下：

```
# saslauthd -v
saslauthd 2.1.17
authentication mechanisms: getpwent pam rimap shadow ldap
```

请注意，saslauthd 将其后端标记为"authentication mechanisms"（认证机制）。不要将此与 SMTP AUTH 机制（如 PLAIN 和 CRAM-MD5）混淆。

如果所需的机制不在列表中，你需要重新编译 Cyrus SASL。在 Cyrus SASL 源代码目录中运行 `./configure --help` 可以获取启用各种后端的选项列表。

#### 准备 saslauthd 运行环境

saslauthd 需要一个状态目录来存储套接字和 PID 文件。Cyrus SASL 安装脚本不会为你创建状态目录，但如果你通过二进制包（如 RPM）安装 Cyrus SASL，包安装程序可能会创建该目录。默认状态目录为 /var/state/saslauthd，/var/run/saslauthd 也很常见。

你可以在构建时通过 `--with-saslauthd=DIR` 选项设置 configure 脚本的状态目录位置。你可以通过以调试模式启动 saslauthd 来检查状态目录：

```
# saslauthd -a shadow -d
saslauthd[31076] :main         : num_procs    : 5
saslauthd[31076] :main         : mech_option: NULL
saslauthd[31076] :main         : run_path     : /var/run/saslauthd
saslauthd[31076] :main         : auth_mech    : shadow
saslauthd[31076] :main         : could not chdir to: /var/run/saslauthd
saslauthd[31076] :main         : chdir: No such file or directory
saslauthd[31076] :main         : Check to make sure the directory exists and is
saslauthd[31076] :main         : writable by the user this process runs as.
```

在上述输出中，`run_path` 表示 saslauthd 将创建套接字的状态目录。请注意，saslauthd 的调试输出显示该目录不存在。

如果目录不存在，请创建它并将其访问权限设置为仅 root 用户和 root 组成员可访问。以下示例展示了操作方法。

---

配置脚本创建 Makefile 后，你可以运行 `make` 来编译 Cyrus SASL，然后以 root 身份运行 `make install` 来安装它。

接下来你需要创建一个符号链接。安装过程默认将 SASL 库放在 `/usr/local/lib/sasl2` 目录下，但 configure 脚本中设置的配置参数会使 Cyrus SASL 在 `/usr/lib/sasl2` 中查找库文件。按如下方式创建链接：

```
# ln -s /usr/local/lib/sasl2 /usr/lib/sasl2
```

最后，检查 syslogd 守护进程是否已设置为记录 Cyrus SASL 消息。Cyrus SASL 向 syslog 的 `auth` 设施记录日志，因此如果你还没有捕获该设施的日志配置，你应该在 `syslog.conf` 文件中添加以下行并重启 syslogd：

```
auth.*					/var/log/auth
```

> **注意** *Cyrus SASL 还有更多配置选项。在源代码目录中运行 `./configure --help` 可以了解 Cyrus SASL 支持的所有功能。不过，如果你认为不需要所有后端，可以更改相关选项。*



```
# mkdir /var/state/saslauthd
# chown root:root /var/state/saslauthd
# chmod 750 /var/state/saslauthd
```

#### 使用不同的状态目录

如果你想使用默认目录以外的状态目录（例如，如果你在系统上找到了 saslauthd 的状态目录），可以使用 -m dir 命令行选项来覆盖默认设置。例如，如果你想使用 /var/run/saslauthd 目录，可以按如下方式运行守护进程：

```
# saslauthd -m /var/run/saslauthd -a shadow
```

这里，路径是目录名称，不包含套接字（mux）的名称。-a 选项用于指定认证后端；你将在下一节中看到相关内容。

不过，你还需要通过在 smtpd.conf 文件中设置 saslauthd_path 参数来告知 Postfix 新的状态目录。这次，你必须包含套接字的文件名，如以下示例中*粗斜体*所示：

```
# Global parameters
log_level: 3
pwcheck_method: saslauthd
# saslauthd parameters
saslauthd_path: /var/run/saslauthd/mux
```

状态目录就绪后，就可以将 saslauthd 连接到认证后端了。

#### 为 saslauthd 配置认证后端

saslauthd 使用 -a backend_name 选项来选择认证后端。名称应为运行 saslauthd -v 时列出的后端之一，如表 15-2 所述。以下示例使用 shadow 后端从 shadow 密码文件中读取：

```
# saslauthd -a shadow
```

以下各节列出了与 saslauthd 配合使用的最常见认证后端。有关 saslauthd 的完整认证后端列表，请参阅 saslauthd(8) 手册页。

##### 从本地用户账户进行认证

saslauthd 可以访问本地密码文件，这在大多数 Unix 系统上都适用，也可以在支持 shadow 密码的系统上访问本地 shadow 密码文件。要从常规密码文件（/etc/passwd）读取，请使用 -a getpwent 参数。

```
# saslauthd -a getpwent
```

在使用 shadow 密码的系统上，你可以使用 -a shadow 选项启动 saslauthd，使其访问 /etc/shadow；你必须以 root 身份运行 saslauthd 才能访问 /etc/shadow：

```
# saslauthd -a shadow
```

##### 通过 PAM 进行认证

saslauthd 支持 PAM（可插拔认证模块）来认证 SMTP 用户。要使用 PAM 支持的后端，请创建 /etc/pam.d/smtp 并添加适合你需求和系统的配置参数，或者在 /etc/pam.conf 中添加相应的设置。

以下是在 Red Hat Fedora Core 1 系统上可能放在 /etc/pam.d/smtp 中的示例：

```
#%PAM-1.0
auth       required     /lib/security/pam_stack.so service=system-auth
account    required     /lib/security/pam_stack.so service=system-auth
```

> 配置文件名必须是 smtp，因为 RFC 2554 规定 SASL over SMTP 的服务名称为 smtp。Postfix 将值 smtp 作为服务名称传递给 sasl_server_new() 函数。然后该服务名称被传递给 saslauthd，最终传递给 PAM，PAM 进而会在 smtp 中查找认证指令。

配置完 PAM 后，你可以按如下方式启动 saslauthd：

```
# saslauthd -a pam
```

##### 通过 IMAP 服务器进行认证

saslauthd 支持一种特殊的认证后端，可以连接到 IMAP 服务器。这种后端的不同之处在于，检查用户名和密码的是 IMAP 服务器，而非 SASL 库。

你可以通过两个参数将 IMAP 配置为 saslauthd 的认证后端。第一个是通常的 -a 选项来选择后端，然后使用 -O 指定 IMAP 服务器，如下例所示：

```
# saslauthd -a rimap -O imap.example.com
```

##### 从 LDAP 进行认证

saslauthd 可以从 OpenLDAP 服务器读取凭据。LDAP 查询和连接 LDAP 服务器的其他参数可能非常复杂，因此你不会通过命令行将这些参数传递给 saslauthd。相反，它会从一个单独的文件中读取配置。默认文件名为 /usr/local/etc/saslauthd.conf，但你可以使用 -O file 参数指定不同的文件。

以下是 saslauthd.conf 文件示例：

```
ldap_servers: ldap://127.0.0.1/ ldap://172.16.10.7/
ldap_bind_dn: cn=saslauthd,dc=example,dc=com
ldap_bind_pw: Yanggt!
ldap_timeout: 10
ldap_time_limit: 10
ldap_scope: sub
ldap_search_base: dc=people,dc=example,dc=com
ldap_auth_method: bind
ldap_filter: (|(&(cn=%u)(&uid=%u@%r)(smtpAuth=Y)))
ldap_debug: 0
ldap_verbose: off
ldap_ssl: no
ldap_start_tls: no
ldap_referrals: yes
```

显然，查询（在此由 ldap_search_base 和 ldap_filter 参数定义）取决于你自己的 LDAP 配置。

> 注意 这里列出的 LDAP 参数远非全部。有关完整列表，请参阅 saslauthd 的 auth_ldap 模块。

假设你将配置放在 /etc/saslauthd.conf 中。你可以按如下方式启动 saslauthd：

```
# saslauthd -a ldap -O /etc/saslauthd.conf
```

### 配置辅助插件（auxprop）

与基于 saslauthd 的后端不同，使用 auxprop 系统的辅助插件的应用程序直接运行插件，并从应用程序自身的 SASL 配置文件中读取配置。如前所述，Postfix 的应用程序配置文件是 smtpd.conf。以下各节将向你展示如何配置 SASL 源代码中附带的辅助插件。

> 注意 SASL 的辅助插件不止本节所列出的这些，例如 ldapdb，你可以在 OpenLDAP 源文件的 /contrib 部分中找到它。ldapdb 插件非常出色，但安装较为困难，因为它不附带 Makefile 或其他构建工具。本章的讨论侧重于中级用户的配置。

#### 使用 sasldb2 插件

Cyrus SASL 附带一个名为 sasldb2 的标准插件，主要用于 Cyrus IMAP，但也可以单独使用。sasldb2 插件附带两个工具：saslpasswd2 用于用户管理，sasldblistusers2 用于列出 sasldb2 中的所有用户。

**注意** 数据库和工具名称以 "2" 结尾，因为它们属于 Cyrus SASL 2.x。它们必须重命名以避免与 Cyrus SASL 1.x 冲突，因为两个版本之间的 Cyrus SASL API 发生了变化。如果你找到的工具末尾没有数字，它们可能是用于 Cyrus SASL 1.x 的，无法与版本 2 配合使用。

要使用 sasldb2 配置 Cyrus SASL，你需要做两件事：

1. 创建 sasldb2 数据库。
2. 配置 SASL 从数据库中读取。

##### 创建 sasldb2 数据库

你可以通过以 root 身份运行 saslpasswd2 命令来创建 sasldb2 数据库。选项 -c 会在 /etc/sasldb2 文件中创建一个 sasldb2 数据库。以下是创建数据库、添加用户以及指定 Postfix myhostname 作为 realm 的示例（如果不添加用户就无法创建数据库）：

```
# saslpasswd2 -c -u `postconf -h myhostname` test
Password:
Again (for verification):
```

**注意** sasldb2 插件除了凭据外还需要一个 realm。Postfix 使用 smtpd_sasl_local_domain 参数的值作为 realm（默认为空）。Postfix 每个 smtpd 实例只能有一个 realm，这实际上将认证限制为单个 realm。

创建数据库后，将访问权限限制为 root 用户和 postfix 组：

```
# chmod 640 /etc/sasldb2
# chgrp postfix /etc/sasldb2
# ls -l /etc/sasldb2
-rw-r----- 1 root postfix 12288 Feb 4 16:23 /etc/sasldb2
```

如果你提供 OTP 机制，还必须使数据库文件对 Postfix 可写，以便它能标记过期的密码。如果其他组需要访问数据库文件，你可能需要修改所有权和权限。

##### 配置 SASL 从 sasldb2 数据库读取

要将 sasldb2 数据库告知 Postfix，请编辑 smtpd.conf 文件，将 auxprop 指定为密码验证服务，将 sasldb 指定为 auxprop 插件类型：

```
# Global parameters
log_level: 3
pwcheck_method: auxprop
```



mech_list: PLAIN LOGIN CRAM-MD5 DIGEST-MD5
# 辅助插件参数
auxprop_plugin: sasldb

#### 使用 sql 插件

Cyrus SASL 2 提供了对两种流行关系数据库的访问：MySQL 和 PostgreSQL。两者都可通过 sql 辅助插件访问，并使用相同的配置参数：

**sql_engine**

`sql_engine` 参数指定数据库类型。从 Cyrus SASL 2.1.17 开始，你可以选择 `mysql` 或 `pgsql`。

**sql_hostnames**

`sql_hostnames` 参数指定数据库服务器名称。你可以指定一个或多个以逗号分隔的全限定域名 (FQDN) 或 IP 地址。如果选择 `localhost`，SQL 引擎会尝试通过套接字进行通信。

**sql_database**

`sql_database` 参数定义要连接的数据库名称。

**sql_user**

`sql_user` 参数定义数据库用户名。

**sql_passwd**

`sql_passwd` 参数定义数据库用户（明文）的密码。

**sql_select**

`sql_select` 参数定义用于查找给定用户名和域的密码的 SELECT 语句。

**sql_insert**

`sql_insert` 参数定义允许 SASL 库在 SQL 数据库中创建用户的 INSERT 语句（使其可被 `saslpasswd2` 等程序访问）。

**sql_update**

`sql_update` 参数定义允许 SASL 库或插件为 OTP 等机制更新 SQL 数据库中用户的 UPDATE 语句。`sql_update` 参数必须与 `sql_insert` 结合使用。

**sql_usessl**

`sql_usessl` 参数允许你使用加密连接连接到数据库。默认情况下，它处于关闭状态 (`sql_usessl: no`)；使用 `yes`、`1`、`on` 或 `true` 设置来启用 SSL。

Cyrus SASL 提供了以下宏，你可以在参数设置中使用它们来构建数据库查询：

| 宏 | 描述 |
| --- | --- |
| %u | 此宏在身份验证过程中会被提供的用户名替换。 |
| %p | 这是密码的占位符；这是明文密码的默认列名。 |
| %r | 此宏在身份验证过程中会被提供的域替换。 |
| %v | 这指定了在 SQL UPDATE 或 INSERT 操作期间应替换现有值的提交值。 |

> **注意** 在 `smtpd.conf` 中定义查询时，宏必须用单引号 (') 分别括起来。

##### 为 SASL 配置 MySQL

在 Postfix 中为 SASL 配置 MySQL 时，第一步是创建数据库和表。此示例 SQL 语句创建一个包含 Cyrus SASL 期望的默认字段以及一个额外字段的表，该字段允许你禁用特定用户的中继访问：

```
mysql> CREATE TABLE `users` (
    `id` int(11) unsigned NOT NULL auto_increment,
    `username` varchar(255) NOT NULL default '0',
    `userrealm` varchar(255) NOT NULL default 'mail.example.com',
    `userpassword` varchar(255) NOT NULL default '1stP@ss',
    `auth` tinyint(1) default '1',
    PRIMARY KEY  (`id`),
    UNIQUE KEY `id` (`id`)
) TYPE=MyISAM COMMENT='SMTP AUTH relay users';
```

如你所见，所有字段（`id`、`username`、`userrealm`、`userpassword` 和 `auth`）都有默认值。特别重要的是要有默认密码，这样攻击者就无法尝试空密码。

接下来，你需要创建一个可以读写 SASL 授权数据库的 MySQL 用户。例如，以下命令序列创建了一个名为 `postfix` 的用户：

```
mysql> CONNECT mysql;
mysql> INSERT INTO user VALUES
    ('localhost','postfix','','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y','Y',
    'Y','Y','Y','Y','Y','Y');
mysql> UPDATE mysql.user SET password=PASSWORD("Yanggt!") WHERE user='postfix'
    AND host='localhost';
mysql> GRANT SELECT, UPDATE ON mail.users TO 'postfix'@'localhost';
mysql> FLUSH PRIVILEGES;
```

使用如下命令在 `users` 表中添加一个测试条目：

```
mysql> INSERT INTO `users` VALUES (1,'test','mail.example.com','testpass',0);
```

最后，在设置好 MySQL 数据库之后，在你的 `smtpd.conf` 文件中配置辅助插件认证后端，如下所示：

```
# 全局参数
log_level: 3
pwcheck_method: auxprop
mech_list: PLAIN LOGIN CRAM-MD5 DIGEST-MD5
# 辅助插件参数
auxprop_plugin: sql
sql_engine: mysql
sql_hostnames: localhost
sql_database: mail
sql_user: postfix
sql_passwd: Yanggt!
sql_select: SELECT %p FROM users WHERE username = '%u' AND userrealm = '%r' AND auth = '1'
sql_usessl: no
```

请注意 `auxprop` 密码验证服务和 `sql` 插件。其他参数和宏的含义请参阅前面的“使用 sql 插件”部分。

> **注意** *有关符号和参数的更详细信息，请阅读 Cyrus SASL 文档目录中的 `options.html`。*

##### *为 SASL 配置 PostgreSQL*

将 PostgreSQL 与 SASL 一起使用的过程与使用 MySQL 非常相似。以下是在 PostgreSQL 中创建邮件数据库的方法：

```
# createdb mail
CREATE DATABASE
```

现在，连接到数据库并为 SASL 用户创建一个表，如下所示：

```
# psql -d mail
Welcome to psql 7.3.4, the PostgreSQL interactive terminal.
Type: \copyright for distribution terms
       \h for help with SQL commands
       \? for help on internal slash commands
       \g or terminate with semicolon to execute query
       \q to quit
mail=# CREATE TABLE public.users
mail-# (
mail(#  id int4 NOT NULL,
mail(#  "username" varchar(255),
mail(#  "userrealm" varchar(255),
mail(#  "userpassword" varchar(255),
mail(#  auth int2 DEFAULT 0,
mail(#  CONSTRAINT id PRIMARY KEY (id)
mail(#) ) WITHOUT OIDS;
NOTICE:  CREATE TABLE / PRIMARY KEY will create implicit index 'id' for table 'users'
CREATE TABLE
mail=# COMMENT ON TABLE public.users IS 'mail users';
COMMENT
mail=#
```

接下来，创建一个可以读写数据库的用户：

```
mail=# CREATE USER postfix PASSWORD 'Yanggt!' NOCREATEDB NOCREATEUSER;
CREATE USER
```

授予此用户对表的 `SELECT` 和 `UPDATE` 访问权限：

```
mail=# GRANT UPDATE,SELECT ON users TO postfix;
GRANT
```

下一步是在 `mail` 表中创建一个测试帐户条目：

```
mail=# INSERT INTO users VALUES ('1','test','mail.example.com','testpass','1');
```

最后，在 PostgreSQL 数据库就位后，你可以在 `smtpd.conf` 中如下配置辅助插件：

```
# 全局参数
log_level: 3
pwcheck_method: auxprop
mech_list: PLAIN LOGIN CRAM-MD5 DIGEST-MD5
# 辅助插件参数
auxprop_plugin: sql
sql_engine: pgsql
sql_hostnames: localhost
sql_database: mail
sql_user: postfix
sql_passwd: Yanggt!
sql_select: SELECT %p FROM users WHERE username = '%u' AND realm = '%r' AND auth = '1'
sql_usessl: no
```

配置好认证后端后，你就可以开始测试认证了。

### 测试认证

在配置 Cyrus SASL（使用 `saslauthd` 或一个辅助插件及后端）后，你应该在按照第 16 章所述在 Postfix 中配置 SMTP AUTH *之前*对其进行测试。经验表明，大多数 SMTP AUTH 问题都源于 Cyrus SASL 安装问题，而非 Postfix 本身。

测试的第一步是找到测试工具。除非你是从源代码安装 Cyrus SASL，否则这可能不是一项容易的任务（默认情况下，工具位于源代码分发目录的 *sample/* 子目录中）。如果你使用的是随操作系统分发包附带的 Cyrus SASL 安装，则需要仔细查找名为 `client` 和 `server` 的程序。

> **注意** *二进制文件的名称在不同操作系统包中远非一致，而且某些包甚至不安装所有二进制文件。请检查 `cyrus-*-devel` 包，并查看这些包中程序的名称。它们不一定命名为 `client` 和 `server`。*

*例如，Red Hat Linux 提供混合的 Cyrus SASL 1.x 和 2.x，将二进制文件重命名为 Cyrus SASL 1.x 的 `sasl-sample-client` 和 `sasl-sample-server`，以及 2.x 的 `sasl2-sample-client` 和 `sasl2-sample-server`。*

找到 `client` 和 `server` 程序后，请按照以下步骤测试认证：

- 1. 如果你使用的后端需要 `saslauthd` 作为密码验证服务，请启动 `saslauthd`。
- 2. 创建服务器配置文件。
- 3. 启动服务器程序。
- 4. 使用客户端程序测试认证。

#### 启动 saslauthd

如果你选择了一个使用 `saslauthd` 作为密码验证服务的后端（即，它不使用 `sasldb` 等辅助插件或 SQL 数据库），你应该从命令行使用调试参数启动 `saslauthd`。不要使用 init 脚本；你需要能够使用 `-d` 选项，该选项告诉主 `saslauthd` 不要进入守护进程模式，而是保持附加到当前终端并打印调试输出。

以下是为 shadow 密码认证启动 `saslauthd` 的示例：

```
# saslauthd -m /var/state/saslauthd -a shadow -d
saslauthd[4401] :main          : num_procs  : 5
saslauthd[4401] :main          : mech_option: NULL
saslauthd[4401] :main          : run_path   : /var/run/saslauthd
saslauthd[4401] :main          : auth_mech  : shadow
```



saslauthd[4401] :ipc_init            : 使用的接受锁文件：/var/run/saslauthd/mux.accept
saslauthd[4401] :detach_tty          : 主进程 PID 为：0
saslauthd[4401] :ipc_init            : 监听套接字：/var/run/saslauthd/mux
saslauthd[4401] :main                : 使用进程模型
saslauthd[4402] :get_accept_lock     : 已获取接受锁
saslauthd[4401] :have_baby           : 已派生子进程：4402
saslauthd[4401] :have_baby           : 已派生子进程：4403
saslauthd[4401] :have_baby           : 已派生子进程：4404
saslauthd[4401] :have_baby           : 已派生子进程：4405

#### 创建服务器配置文件

现在你需要为服务器程序创建配置文件。请记住，每个 SASL 应用程序都需要自己的配置文件；测试程序 server 需要一个 `sample.conf` 文件。但是，测试配置应该与你用于 Postfix 的配置相同。最简单的方法是创建一个指向 `smtpd.conf` 文件的符号链接，如下所示：

```
# cd /usr/lib/sasl2/
# ln -s smtpd.conf sample.conf
```

#### 启动服务器程序

打开一个新的 shell，使用 `-s` 和 `-p` 选项运行服务器程序，以指定服务器的服务和端口：

```
# server -s rcmd -p 8000
trying 10, 1, 6
socket: Address family not supported by protocol
trying 2, 1, 6
```

> 请确保使用你的机器上尚未使用的端口。

注意：`rcmd` 的含义文档说明不够完善。

#### 使用客户端程序进行测试

最后，启动客户端程序，并让它连接到服务器。连接成功后，客户端程序会要求你输入认证 ID、授权 ID 和密码。使用 `-m` 命令行选项来选择认证机制。以下示例在 `localhost`（127.0.0.1）上使用 `test` 作为认证和授权 ID，`testpass` 作为密码：

```
# client -s rcmd -p 8000 -m PLAIN 127.0.0.1
receiving capability list... recv: {11}
PLAIN LOGIN
PLAIN LOGIN
please enter an authentication id: test
please enter an authorization id: test
Password:
send: {5}
PLAIN
send: {1}
Y
send: {18}
test[0]test[0]testpass
successful authentication
closing connection
```

你需要关注的是 `successful authentication`（认证成功）消息。你也可以在服务器程序端监控通信过程。以下示例展示了连接建立、凭据传入并被验证的过程：

```
# server -s rcmd -p 8000
trying 10, 1, 6
socket: Address family not supported by protocol
trying 2, 1, 6
accepted new connection
send: {11}
PLAIN LOGIN
recv: {5}
PLAIN
recv: {1}
Y
recv: {18}
test[0]test[0]testpass
successful authentication 'test'
closing connection
```

最后，如果你使用的是需要 saslauthd 的后端，你可以看到 saslauthd 验证凭据时发生的情况。输出应该类似于：

```
# saslauthd -m /var/run/saslauthd -a shadow -d
saslauthd[4547] :main : num_procs : 5
saslauthd[4547] :main : mech_option: NULL
saslauthd[4547] :main : run_path : /var/run/saslauthd
saslauthd[4547] :main : auth_mech : shadow
saslauthd[4547] :ipc_init : using accept lock file: /var/run/saslauthd/mux.accept
saslauthd[4547] :detach_tty : master pid is: 0
saslauthd[4547] :ipc_init : listening on socket: /var/run/saslauthd/mux
saslauthd[4547] :main : using process model
saslauthd[4548] :get_accept_lock : acquired accept lock
saslauthd[4547] :have_baby : forked child: 4548
saslauthd[4547] :have_baby : forked child: 4549
saslauthd[4547] :have_baby : forked child: 4550
saslauthd[4547] :have_baby : forked child: 4551
saslauthd[4548] :rel_accept_lock : released accept lock
saslauthd[4548] :do_auth : auth success: [user=test] [service=rcmd] [realm=]
                                          [mech=shadow]
saslauthd[4548] :do_request : response: OK
saslauthd[4548] :get_accept_lock : acquired accept lock
```

如果出现问题，你应该可以通过以下步骤来定位问题：

- 1. 如果你将 saslauthd 用作密码验证服务，请在调试输出中查找 `[reason=…]`。
- 2. 验证你的认证后端中用户名和密码是否正确。
- 3. 确保 saslauthd 有权访问你的认证后端。
- 4. 验证你提交的用户名和密码字符串是否正确。

认证成功后，请继续阅读第 16 章，配置 Postfix smtpd 守护进程以向邮件客户端提供 SMTP AUTH。

## SMTP AUTH 的未来

当前的 SMTP AUTH 实现远非最终版本。未来的 Postfix 版本将在 SASL 方面发生重大变化。目前，访问认证后端的 SASL 库是被链接并在 smtpd 守护进程（即处理与邮件客户端通信的同一个守护进程）内部使用的。图 15-6 展示了当前连接链的结构。

![当前 SASL 与 Postfix 的集成方式](img/852c79f689feb77c5fde686b993808b1_273_0.png)

图 15-6：当前 SASL 与 Postfix 的集成方式

访问认证后端通常需要特权用户，因此任何能够劫持负责 SMTP AUTH 的守护进程的人，都几乎可以访问系统中的用户数据库。
Postfix 尽可能避免使用特权进程，尤其是当认证守护进程直接暴露在（始终充满敌意的）网络上时。此外，复杂性是安全的大敌，而 Cyrus SASL 毫无疑问是复杂的。

在未来某个时候，Postfix 将拥有一个新的守护进程（可能命名为 `sasld`），它唯一的工作就是连接 Postfix 和 Cyrus SASL 库。Postfix 与这个新守护进程之间的通信应该尽可能简单。图 15-7 展示了新的连接链可能的样子。

![未来 SASL 与 Postfix 的集成方式](img/852c79f689feb77c5fde686b993808b1_274_0.png)

图 15-7：未来 SASL 与 Postfix 的集成方式

新的设计将使需要暴露在网络上的守护进程更不容易受到攻击，这将使 Postfix 更接近其主要目标之一——安全的服务。

# 16

## SMTP 身份认证

![SMTP 身份认证](img/852c79f689feb77c5fde686b993808b1_275_0.png)

SMTP 身份认证（SMTP AUTH）允许拥有动态 IP 地址的授权邮件客户端通过你的服务器转发邮件，而无需创建开放中继。本章将向你展示如何在服务器中启用 SMTP AUTH，以及如何在 Postfix 中配置客户端侧的 SMTP AUTH。

### 检查 Postfix 是否支持 SMTP AUTH

虽然 Postfix 源代码包含对 SMTP 身份认证的支持，但默认情况下并未启用，因为 Postfix 并未附带处理实际工作的 SMTP AUTH 库。在构建 Postfix 时，你需要将此库的信息告知构建过程。
许多发行版提供的 Postfix 软件包已经包含 SMTP AUTH 支持。你可以很容易地验证你的 Postfix 版本是否已经启用了 SMTP AUTH 支持。以 root 身份运行 `ldd \`postconf -h daemon_directory\`/smtpd`，并在输出中搜索 `libsas2.so`。

```
# ldd `postconf -h daemon_directory`/smtpd
    libldap.so.2 => /usr/lib/libldap.so.2 (0x00117000)
    liblber.so.2 => /usr/lib/liblber.so.2 (0x008a9000)
    libpcre.so.0 => /lib/libpcre.so.0 (0x00b86000)
    libsasl2.so.2 => /usr/lib/libsasl2.so.2 (0x00101000) ①
    libssl.so.4 => /lib/libssl.so.4 (0x00b11000)
    libcrypto.so.4 => /lib/libcrypto.so.4 (0x00977000)
    libgssapi_krb5.so.2 => /usr/lib/libgssapi_krb5.so.2 (0x00afc000)
    libkrb5.so.3 => /usr/lib/libkrb5.so.3 (0x00a6f000)
    libcom_err.so.2 => /lib/libcom_err.so.2 (0x00a6a000)
    libk5crypto.so.3 => /usr/lib/libk5crypto.so.3 (0x00ad8000)
    libresolv.so.2 => /lib/libresolv.so.2 (0x00965000)
    libdl.so.2 => /lib/libdl.so.2 (0x008b8000)
    libz.so.1 => /usr/lib/libz.so.1 (0x008bd000)
    libdb-4.1.so => /lib/libdb-4.1.so (0x00c18000)
    libnsl.so.1 => /lib/libnsl.so.1 (0x008fe000)
    libc.so.6 => /lib/libc.so.6 (0x0076e000)
    libcrypt.so.1 => /lib/libcrypt.so.1 (0x008d0000)
    /lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x00759000)
    libpthread.so.0 => /lib/libpthread.so.0 (0x00912000)
```

① `libsasl2.so.2` 的输出表明 SASL 支持已经编译到 Postfix 中，你可以开始配置 SMTP 身份认证了。`libsasl2.so.2` 是当前主要的 Cyrus SASL 版本。

> **注意** *Postfix 也支持较旧的 Cyrus SASL 版本 1.5。如果你在 `ldd` 命令的输出中找到 `libsasl.so.7`，说明你的 Postfix 版本是使用 Cyrus SASL 1.5 构建的。如果你只找到 `libsasl2.so.7`，建议升级到 Cyrus SASL 2；该版本的认证后端支持相比 1.5 版本有了实质性的改进。*

### 为 Postfix 添加 SMTP AUTH 支持

如果你的 Postfix 安装中没有 SASL 支持，但想使用 SMTP AUTH，你需要重新构建 Postfix。首先需要做的是在你的系统上找到 Cyrus SASL 库和头文件。使用 `find` 命令搜索库文件，如下所示：

```
# find /usr -name 'libsasl*.*'
/usr/lib/sasl2/libsasldb.la
/usr/lib/sasl2/libsasldb.a
/usr/lib/sasl2/libsasldb.so.2.0.15
/usr/lib/sasl2/libsasldb.so
/usr/lib/sasl2/libsasldb.so.2
/usr/lib/libsasl2.so.2.0.15
/usr/lib/libsasl2.so.2
```



### 服务器端 SMTP 认证

本章的这一节将解释如何配置 Postfix smtpd 服务器，以便向邮件客户端提供 SMTP AUTH 服务。一旦完成认证，即使客户端的 IP 地址不在 `mynetworks` 配置参数定义的 IP 地址范围内，它们也可以通过 Postfix 服务器转发邮件。

> **注意** 要在服务器上正确配置 SMTP AUTH，你不仅需要配置 Postfix 库并将其与 Cyrus SASL 库链接，还必须配置 Cyrus SASL 以与认证后端进行通信。详见第 15 章。

在前面的示例中，你可以看到 Cyrus SASL 2 库位于 `/usr/lib`。记下这个位置，然后使用以下命令搜索对应的头文件：

```
# find /usr -name '*sasl*.h'
/usr/include/sasl/sasl.h
/usr/include/sasl/saslplug.h
/usr/include/sasl/saslutil.h
```

> **注意** 各 Linux 发行版将头文件和库文件分别放在不同的软件包中，这种做法是为了节省磁盘空间，但有时会给用户带来不便。如果你在系统上找不到 Cyrus SASL 的头文件，但库文件确实存在，请查找并安装以 `-dev` 或 `-devel` 结尾的 SASL 软件包。

如果你的系统中没有 Cyrus SASL 库，请阅读第 15 章以进行配置和安装。一旦你知道了头文件和包含文件目录的位置，你就可以像下面这样构建支持 SASL 的 Postfix：

```
$ CCARGS="-DUSE_SASL_AUTH -I/usr/include/sasl AUXLIBS="-L/usr/lib -lsasl2"
   make makefiles
$ make
```

1.  以普通用户身份解压 Postfix 源码。
2.  切换到 Postfix 源码目录。
3.  设置构建选项并运行 `make makefiles` 和 `make`，如下所示：
4.  切换到超级用户（root）。
5.  如果这是你第一次安装 Postfix，请运行 `make install`。但是，如果你是升级或替换现有安装，请运行 `make upgrade`。
6.  如本章开头所述，验证你是否拥有 SASL 支持。

请记住，这些只是 SASL 相关的选项；你可能希望根据 Postfix 源码树中 `README_FILES` 目录下的 `*_README` 文件的描述，添加更多选项。

图 16-1 展示了一个邮件客户端，在向远程目的地发送待转发的消息之前，先向邮件服务器进行身份验证。服务器将邮件客户端提供的凭据与存储在认证后端中的凭据进行比较。只有当提供的凭据与存储的凭据匹配时，服务器才会为该客户端转发消息。

### 启用和配置服务器

在 SASL 中配置好认证后端（如第 15 章所述）后，你必须按照以下方式配置服务器：

1.  启用服务器端 SMTP AUTH。
2.  配置将提供给客户端的 SASL 机制。
3.  为非标准邮件客户端配置 SMTP AUTH 支持。
4.  配置 Postfix 传递给 SASL 库的领域（realm）。
5.  在 Postfix 中配置中继权限。

> 以 chroot 方式运行 Postfix 并提供 SMTP AUTH 并不复杂。请按照本章的说明设置服务器端认证。一旦你验证了非 chroot 环境下的 SMTP 认证工作正常，就可以继续学习第 20 章；在 chroot 环境中运行 SMTP AUTH 将作为描述 chroot 设置的示例。

#### 启用服务器端 SMTP AUTH

你需要做的第一件事是为 Postfix smtpd 服务器启用服务器端 SMTP 认证，因为此功能默认是禁用的。在 `main.cf` 中设置 `smtpd_sasl_auth_enable` 参数以启用它：

```
smtpd_sasl_auth_enable = yes
```

#### 配置 SASL 机制

现在你必须定义 Postfix 应提供给邮件客户端的认证机制。Cyrus SASL 提供了多种机制，从匿名“认证”到非常强大的系统（如 Kerberos）。
你可以使用 `smtpd_sasl_security_options` 参数来控制提供的机制。将其设置为以下选项中一个或多个的逗号分隔列表：

-   **noanonymous**: 此设置确保服务器实际验证客户端的凭据。这是默认设置，你绝对应该保留它，因为一些垃圾邮件发送者知道匿名 SMTP 认证。请确保你的 `smtpd_sasl_security_options` 参数始终列出 `noanonymous`；否则，你的邮件服务器几乎肯定会被滥用为开放中继。
-   **noplaintext**: 在 SASL 安全选项列表中添加 `noplaintext` 会排除所有明文认证机制，例如 PLAIN 和 LOGIN。这是推荐的做法，因为明文凭据很容易在网络中被窃听。
-   **noactive**: 此设置排除容易受到主动（非字典）攻击的 SASL 机制。例如，相互认证就不易受到主动攻击。
-   **nodictionary**: 此关键字排除所有可能被字典攻击破解的机制。字典攻击者试图通过暴力破解密码，尝试许多不同的密码直到有一个成功。
-   **mutual_auth**: 使用 `mutual_auth` 仅允许提供相互认证的机制。这种认证形式要求服务器也向客户端进行身份验证，反之亦然。

在测试配置时，你不需要更改此参数；默认值 `smtpd_sasl_security_options = noanonymous` 可以保护你免受垃圾邮件发送者的侵扰，同时仍允许明文机制，这样调试会稍微容易一些。稍后，当你验证 SMTP AUTH 可以正常工作后，你应该禁用明文认证，至少将 `main.cf` 中的 `smtpd_sasl_security_options` 参数扩展为如下设置：

```
smtpd_sasl_security_options = noanonymous, noplaintext
```

> **警告** 使用明文机制的邮件客户端会将用户名和密码作为 base64 编码的字符串发送。解码它非常简单，因此任何监听 SMTP 对话的人都可以利用这些数据滥用你的邮件服务器。不幸的是，这是 Outlook Express 唯一支持的机制。如果你想提供明文机制，请仅在加密的通信层上提供，如第 18 章所述。

#### 为非标准邮件客户端配置 SMTP AUTH 支持

接下来你应该做的是告诉 Postfix 在 SMTP 对话中提供另一种表示方式，以便有问题的邮件客户端仍然可以使用 SMTP AUTH。

有问题的邮件客户端无法识别 RFC 2222 中描述的 SMTP AUTH 提供方式；相反，它们识别的是标准文档草案中使用的一种表示方式，其中 AUTH 语句和机制之间使用等号（=）而不是空格。

已知有问题的客户端包括旧版本的 Microsoft Outlook、Microsoft Outlook Express 和 Netscape Mail。

要支持有问题的邮件客户端，请在 `main.cf` 中设置 `broken_sasl_auth_clients` 如下：

```
broken_sasl_auth_clients = yes
```

重新加载 Postfix 后，你将在 SMTP 对话中注意到另一行包含等号的 AUTH 行。例如：

```
# telnet mail.example.com 25
220 mail.example.com ESMTP Postfix
EHLO client.example.com
250-mail.example.com
250-PIPELINING
250-SIZE 51200000
250-VRFY
250-ETRN
250-AUTH LOGIN PLAIN
250-AUTH=LOGIN PLAIN
250 8BITMIME
QUIT
```

#### 配置 SASL 领域

根据 Cyrus SASL 的版本和具体服务，你可能需要在 `main.cf` 中设置一个领域（realm），该领域将被传递给你使用的 Cyrus SASL 密码验证服务。当客户端想要进行身份验证时，Postfix 会将领域连同客户端的凭据一起发送给 Cyrus SASL。你可以在 Postfix 的 `main.cf` 文件中使用 `smtpd_sasl_local_domain` 参数定义领域；此参数默认为空，除非你使用确实需要领域的辅助插件，否则应留空：

```
smtpd_sasl_local_domain =
```

你应该根据使用的密码验证服务来更改此设置：

**auxprop**

使用辅助属性的服务需要一个领域。将 `smtpd_sasl_local_domain` 设置为你的 SMTP AUTH 用户在认证后端中的领域。例如，如果你的 `/etc/sasldb2` 中 SMTP AUTH 用户的领域是 `example.com`，请使用以下设置：

```
smtpd_sasl_local_domain = example.com
```

**Cyrus SASL 2.1.17 之前的 saslauthd**

Cyrus SASL 2.1.17 之前的 saslauthd 无法处理领域；你不应该使用它。按如下方式移除 `smtpd_sasl_local_domain` 的值：

```
smtpd_sasl_local_domain =
```

**Cyrus SASL 2.1.17 的 saslauthd**

Cyrus SASL 2.1.17 的 saslauthd 不知道如何处理领域，因此它会忽略此信息。你发送什么领域都没有关系，因此你不必修改 `smtpd_sasl_local_domain` 参数。

**Cyrus SASL 2.1.19 的 saslauthd**

Cyrus SASL 2.1.19 及更高版本的 saslauthd 使领域发送变得可配置。启动 saslauthd 时使用 `-r` 选项，领域将被传递给你的密码验证后端。

#### 配置中继权限

最后一步是告诉 Postfix 允许经过 SASL 认证的客户端进行中继。为此，请将 `permit_sasl_authenticated` 添加到你的配置中的 `smtpd_recipient_restrictions` 列表中。例如：

```
smtpd_recipient_restrictions =
    [...]
    permit_sasl_authenticated,
```

### 测试服务器端SMTP认证

测试服务器端SMTP认证涉及以下步骤：

1.  检查邮件日志，以查找Postfix自身能检测到的错误。
2.  检查SMTP对话，确保`smtpd`提供了SMTP AUTH。
3.  对用户进行身份验证，以确保Postfix能与Cyrus SASL通信。
4.  向远程用户发送测试消息，以验证经过认证的用户能否通过您的服务器将消息中继到非本地目的地。

#### 检查邮件日志

使用以下命令打印出`/var/log/maillog`中包含单词`reject`、`error`、`warning`、`fatal`或`panic`后跟冒号（`:`）的所有行，来检查日志文件：

```
# egrep '(reject|error|warning|fatal|panic):' /var/log/maillog
```

您不应看到任何与SMTP AUTH相关的错误，但如果出现了，请检查您的配置是否有排印错误或与Cyrus SASL相关的问题。

现在，为`smtpd`守护进程启用详细日志记录，并在测试SMTP AUTH期间保持此日志级别。通过在`master.cf`中的`smtpd`命令添加`-v`来进行此更改：

```
# ============================================================================
# service type  private unpriv  chroot  wakeup  maxproc command + args
# (yes)   (yes)  (yes)  (never)  (100)
# ============================================================================
smtp      inet  n       -       n       -       -       smtpd -v
#smtps    inet  n       -       n       -       -       smtpd
```

重新加载Postfix后，更改将生效。

#### 检查SMTP对话

下一个测试是确保Postfix向邮件客户端提供了SMTP AUTH，以便客户端知道何时可以发起SMTP认证。连接到您的服务器，并向服务器发送EHLO介绍（SMTP AUTH仅在扩展SMTP通信中有效）。这是一个示例：

```
$ telnet mail.example.com 25
220 mail.example.com ESMTP Postfix
EHLO client.example.com
250-mail.example.com
250-PIPELINING
250-SIZE 10240000
250-VRFY
250-ETRN
250-STARTTLS
250-AUTH NTLM LOGIN PLAIN DIGEST-MD5 CRAM-MD5
250-AUTH=NTLM LOGIN PLAIN DIGEST-MD5 CRAM-MD5
250-XVERP
250 8BITMIME
QUIT
221 Bye
```

您可以轻松看到，AUTH参数不仅告诉您SMTP AUTH已启用，还提供了可用的身份验证机制列表。此外，还有一行几乎相同的行用于兼容性不好的客户端。

如果服务器没有提供AUTH参数，请检查您是否完成了以下操作：

*   编译Postfix时启用了Cyrus SASL支持
*   正确配置了基本参数，并且main.cf中没有任何拼写错误；使用`postconf -n`验证参数
*   连接到正确的服务器，并且使用的是EHLO而不是HELO

#### 对用户进行身份验证

要对用户进行身份验证，您需要一个base64编码的字符串，其中包含来自您的身份验证后端的有效用户名和密码。例如，如果您的用户名是`test`，密码是`testpass`，请使用此命令：

```
$ perl -MMIME::Base64 -e 'print encode_base64("test\0test\0testpass");'
```

输出将如下所示：

```
dGVzdAB0ZXN0AB0testpass
```

现在，连接到您的服务器，使用EHLO开始扩展SMTP通信，然后使用`AUTH PLAIN`告诉Postfix您想使用base64编码的字符串通过明文机制进行身份验证。这是一个成功测试的示例：

```
$ telnet mail.example.com 25
220 mail.example.com ESMTP Postfix
EHLO client.example.com
250-mail.example.com
250-PIPELINING
250-SIZE 10240000
250-VRFY
250-ETRN
250-STARTTLS
250-AUTH NTLM LOGIN PLAIN DIGEST-MD5 CRAM-MD5
250-AUTH=NTLM LOGIN PLAIN DIGEST-MD5 CRAM-MD5
250-XVERP
250 8BITMIME
AUTH PLAIN dGVzdABvZXNAMHAHRlc3RwYXNz
235 Authentication successful
QUIT
221 Bye
```

您可以轻松看到`235 Authentication successful`确认信息。如果遇到问题，服务器响应`535 Error: authentication failed`，请尝试以下操作：

-   检查您的日志文件是否有错误。
-   验证身份验证后端中的用户名和密码。
-   如第15章所述，检查您在`/usr/lib/sasl2/smtpd.conf`中的Cyrus SASL配置。
-   如果更改了`/usr/lib/sasl2/smtpd.conf`，请重新加载Postfix。
-   解码您的base64字符串，并将输出与您的原始输入进行比较。（如果您想测试空字节，请将输出重定向到文件并使用文本编辑器打开该文件。）这是一个示例：

```
$ perl -MMIME::Base64 -e 'print decode_base64("dGVzdABvZXNAMHAHRlc3RwYXNz");'
testtesttestpass
```

> **注意** 如果您将日志发布到邮件列表，您可能应该修改它们以删除详细日志级别中附带的用户名和密码信息。或者，您可以创建一个测试用户，并在完成后立即删除。

#### 中继测试消息

您终于准备好查看Postfix服务器是否允许经过认证的用户中继消息了。不过，首先您需要确保其他中继权限不会干扰您新的基于身份验证的规则。为确保这一点，请从*未被允许在不使用*SMTP认证情况下进行中继的主机或网络连接。仔细检查是值得的，因此首先尝试在不使用SMTP AUTH的情况下发送消息。

如果您无法从mynetworks定义的网络范围之外访问客户端，请在测试时禁用`mynetworks`参数并设置`mynetworks_style = host`。这将中继权限限制为仅服务器，因此您可以使用局域网上的任何主机来测试服务器。

按照上一节所述连接到服务器，但在成功认证后*不要*退出。相反，继续进行一个常规的SMTP通信会话，向非本地用户发送邮件。这是一个从`john.doe@example.com`向`echo@postfix-book.com`发送消息的示例：

```
$ telnet mail.example.com 25
220 mail.example.com ESMTP Postfix
EHLO client.example.com
250-mail.example.com
250-PIPELINING
250-SIZE 10240000
250-VRFY
250-ETRN
250-AUTH DIGEST-MD5 CRAM-MD5 GSSAPI PLAIN LOGIN
250-AUTH=DIGEST-MD5 CRAM-MD5 GSSAPI PLAIN LOGIN
250-XVERP
250 8BITMIME
AUTH PLAIN dGVzdABvZXNoYWRlc3RwYXNz
235 Authentication successful
MAIL FROM: <john.doe@example.com>
250 Ok
RCPT TO: <echo@postfix-book.com>
250 Ok
DATA
354 End data with <CR><LF>.<CR><LF>
This is a server side SMTP AUTH test. If the mail is accepted, relaying works.
.
250 Ok: queued as 3FF15E1C65
QUIT
221 Bye
Connection closed by foreign host.
```

注意服务器响应`RCPT TO:`命令时发送的`250 Ok`消息；这通常是个好兆头，但您仍然需要确认消息确实发送成功。如果此测试不成功，请尝试以下操作：

-   检查您的日志文件是否有错误。
-   确保您已正确设置`permit_sasl_authenticated`，如前面的“配置中继权限”部分所述。
-   仔细检查您的base64字符串。
-   检查您的SMTP对话是否有拼写错误。

### 高级服务器设置

自从SMTP AUTH功能在Postfix中出现以来，添加了一些参数，以便您能更好地控制应如何处理SMTP AUTH。以下小节将告诉您Postfix目前能做什么。

#### 选择性提供SMTP AUTH

您可以排除某些网络，使Postfix不会向它们提供SMTP AUTH。当您有Netscape邮件客户端（Netscape 4.x）只要SMTP AUTH可用就坚持使用它时，这非常有用；无论您是否配置了它们使用它。

在`main.cf`中设置`smtpd_sasl_exceptions_networks`参数，并使用Postfix从其自身配置中知道的变量，例如`mynetworks`，或者使用IP地址/CIDR表示法（例如172.16.0.117/32）定义一个列表：

```
smtpd_sasl_exceptions_networks = $mynetworks, 172.16.0.117/32
```

#### 强制SMTP AUTH用户匹配特定的信封发件人

一旦邮件客户端通过身份验证，它就可以使用任何它选择的信封发件人进行发送。但是，您可以使用`smtpd_sender_login_maps`参数限制邮件客户端只能使用特定的信封发件人地址；它定义了一个映射的路径，该映射将信封发件人地址与SASL登录名进行匹配。该映射（例如`/etc/postfix/smtpd_sender_login_map`）如下所示：

```
flintstone@example.com    flintstone
rubble@example.com        rubble
sales@example.com         flintstone, rubble
```

映射的左侧是信封发件人，右侧是单个登录名或逗号分隔的登录名列表。使用`postmap`转换映射，例如`postmap hash:/etc/postfix/smtpd_sender_login_map`，并在`main.cf`中告诉Postfix读取该映射。



smtpd_sender_login_maps = hash:/etc/postfix/smtpd_sender_login_map

你也可以使用 NIS、LDAP 或 SQL 查询来代替哈希映射类型。一旦 Postfix 了解该映射，你必须选择以下两种限制之一，以指定当客户端的信封发件人与其登录名不匹配时应采取的操作。

**reject_sender_login_mismatch**

这将限制所有客户端，无论其是否经过 SMTP 认证。

**reject_unauthenticated_sender_login_mismatch**

这将仅限制尚未进行 SMTP 认证的客户端。

其中一个参数需要放入 `main.cf` 的 `smtpd_recipient_restrictions` 列表中：

```
smtpd_recipient_restrictions =
    ...
    reject_unauthenticated_sender_login_mismatch
    ...
```

### 客户端 SMTP 认证

在客户端 SMTP 认证中，Postfix 的 smtp 和 lmtp 守护进程使用 Cyrus SASL 向远程服务器进行认证。在客户端配置中，你需要配置 Postfix，但*无需*担心配置 Cyrus SASL。smtp 和 lmtp 这两个守护进程都可以使用 Cyrus SASL 库支持的任何机制。

![](img/852c79f689feb77c5fde686b993808b1_287_0.png)

*图 16-2：客户端 SMTP AUTH 架构*

图 16-2 显示了 Postfix smtp 守护进程与远程邮件服务器进行 SMTP AUTH 会话的情况。客户端（smtp）将 SASL 密码文件中存储的凭据发送到远程服务器，以获取中继权限。

#### 为 Postfix SMTP 客户端配置 AUTH

为 Postfix 客户端配置 SMTP 认证比为服务器配置要*容易得多*。虽然你仍然需要 Cyrus SASL 库，但无需配置 SASL。以下是你需要做的步骤：

1. 向远程服务器询问其提供的机制。
2. 启用客户端 SMTP AUTH。
3. 提供一个包含 SMTP AUTH 凭据的文件。
4. 配置 Postfix 以使用该凭据文件。
5. 禁用不安全的认证机制。

##### 检查有效的认证机制

你的第一步是找出远程服务器提供了哪些机制，并确保你的 Cyrus SASL 安装提供了支持这些机制的库。连接到你的邮件服务器，并发送 EHLO 问候语以列出可用机制。示例如下：

```
$ telnet mail.remote-example.com 25
220 mail.remote-example.com ESMTP
EHLO mail.example.com
250-mail.remote-example.com
250-PIPELINING
250-SIZE 10240000
250-VRFY
250-ETRN
250-STARTTLS
250-AUTH LOGIN PLAIN DIGEST-MD5 CRAM-MD5
250-AUTH=LOGIN PLAIN DIGEST-MD5 CRAM-MD5
250-XVERP
250 8BITMIME
QUIT
221 Bye
```

你可以看到，服务器不仅支持 LOGIN、PLAIN、DIGEST-MD5 和 CRAM-MD5 机制，还会与之前在“为非标准邮件客户端配置 SMTP AUTH 支持”部分中描述的那些有问题的客户端通信。现在，列出你的 Cyrus SASL 库目录中的库。例如，如果你的 Cyrus 安装前缀是 `/usr/local`，你可以运行以下命令。

```
# ls -1 /usr/local/lib/sasl2/lib*.so
```

输出应类似如下：

```
/usr/local/lib/sasl2/libanonymous.so
/usr/local/lib/sasl2/libcrammd5.so
/usr/local/lib/sasl2/libdigestmd5.so
/usr/local/lib/sasl2/liblogin.so
/usr/local/lib/sasl2/libplain.so
/usr/local/lib/sasl2/libsasldb.so
```

很容易看出，这个安装支持 ANONYMOUS、CRAM-MD5、DIGEST-MD5、LOGIN 和 PLAIN 机制。（注意 `libsasldb.so` 不是一个认证机制库。）

一旦你获得了所有这些信息，将远程服务器提供的机制与你自己服务器的 Cyrus SASL 库列表进行比较，你就会知道你的 Postfix 客户端将能够使用哪些机制连接到该服务器。

#### 启用客户端 SMTP AUTH

默认情况下，客户端 SMTP 认证是禁用的。要启用它，请将 `main.cf` 中的 `smtp_sasl_auth_enable` 参数设置为 `yes`：

```
smtp_sasl_auth_enable = yes
```

这启用了客户端 SMTP AUTH；你仍然需要告诉 Postfix 在哪里可以找到认证所需的密钥，以及 Postfix 可以使用远程服务器提供的哪些机制。

##### 存储 SMTP AUTH 凭据

你的下一步是准备 Postfix 客户端在需要与一个或多个远程服务器认证时将使用的数据。以 root 身份，如果 `/etc/postfix/sasl_passwd` 映射文件不存在，则创建它：

```
# touch /etc/postfix/sasl_passwd
```

**提示** Postfix 总是在 chroot 之前打开映射，因此该表可以安全地保存在 chroot 监狱之外。

编辑此文件，在左侧放置需要认证的邮件服务器的完全限定域名，在右侧放置冒号分隔的用户名和密码对。以下是为 `mail.example.com` 和 `relay.another.example.com` 设置用户名和密码的示例：

```
mail.example.com		test:testpass
relay.another.example.com	username:password
```

编辑 `sasl_passwd` 后，更改权限，以便只有 root 可以读取它；请记住，它包含本地用户不应能够读取的机密信息。使用 `chown` 和 `chmod` 命令执行此操作：

```
# chown root:root /etc/postfix/sasl_passwd && chmod 600 /etc/postfix/sasl_passwd
```

> **注意** 无需担心 Postfix 的权限问题；它在切换到权限较低的用户之前以及进入 chroot 监狱之前读取 `sasl_passwd`。

设置好适当的权限后，将映射文件转换为 Postfix 可以快速访问的索引映射（每次更改 `sasl_passwd` 时都需要执行此操作）：

```
# postmap hash:/etc/postfix/sasl_passwd
```

##### 配置 Postfix 以使用 SMTP AUTH 凭据

接下来，你需要告诉 Postfix 客户端在哪里可以找到你刚刚设置的认证凭据映射。将 `main.cf` 中的 `smtp_sasl_password_maps` 参数设置为你的 `sasl_passwd` 文件的完整路径，但指定映射值存储在带有 `hash:` 限定符的哈希文件中。示例如下：

```
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
```

##### 限制认证机制

作为客户端配置的最后一步，你应该禁用不安全的机制。将 `smtp_sasl_security_options` 参数设置为客户端可能不使用的机制类型的逗号分隔列表（有关有效类型的列表，请参阅前面的“配置 SASL 机制”部分）。默认情况下，`smtp_sasl_security_options` 设置为 `noanonymous`，但你应该尽可能禁用明文机制（即，如果你的服务器支持加密机制，如 DIGEST-MD5 或 CRAM-MD5）。为此，在 `main.cf` 中添加以下行：

```
smtp_sasl_security_options = noanonymous, noplaintext
```

> **提示** 如果远程服务器仅提供明文机制，但你不想在未加密的通信层上使用它们，你可以查看服务器是否提供 STARTTLS。如果提供，你可以强制 Postfix 使用 TLS，如第 18 章所述，这样客户端仅在建立加密通信层之后才发送明文凭据。

##### 测试客户端 SMTP AUTH

测试客户端的认证涉及本地和远程测试：

1. 与远程服务器验证凭据，确保你拥有的凭据是有效的，并且被远程服务器所知。
2. 检查日志文件。
3. 使用 Postfix 向远程用户发送测试消息，证明你可以通过服务器中继消息。

###### 与远程服务器验证凭据

你的第一步是验证你拥有的用户名和密码是否确实有效。按照前面“认证用户”部分中的描述连接到远程服务器，并使用给定的用户名和密码进行认证。

> **注意** 如果远程服务器不在未加密的通信层上提供明文机制，你可以尝试使用 OpenSSL 的 `s_client` 建立 TLS 会话，查看其是否提供明文机制，然后尝试进行 AUTH。有关如何操作的详细信息，请参阅第 18 章。
你也可以尝试将凭据配置到支持各种认证机制的 GUI 邮件客户端中。使用客户端发送一封邮件，看看服务器是否接受凭据。

在你确定服务器接受你的用户名和密码后，你可以专注于你的 Postfix 配置。

##### 检查日志文件

下一步是使用我们熟悉的 `egrep` 命令在 Postfix 日志文件中查找明显的错误：

```
# egrep '(reject|error|warning|fatal|panic):' /var/log/maillog
```

###### 使用 Postfix 客户端向远程用户发送测试消息

最终测试是使用你的 Postfix 邮件客户端守护进程（smtp）向远程目的地发送消息。执行以下步骤：

1. 增加 smtp 守护进程的日志级别。
2. 向远程目的地发送消息。
3. 检查日志文件以确认认证成功。



##### 增加 smtp 守护进程的日志级别

要增加 smtp 客户端守护进程的日志输出量，请编辑您的 `master.cf` 文件，并为 `smtp` 程序添加 `-v` 参数，如下所示（确保不要将 `smtpd` 行与 `smtp` 混淆）：

```
# ==========================================================================
# service type  private unpriv  chroot  wakeup  maxproc command + args
# (yes)   (yes)  (yes)  (never)  (100)
# ==========================================================================
smtp      inet  n       -       n       -       -       smtpd
#smtps     inet  n       -       n       -       -       smtpd
...
smtp      unix  -       -       n       -       -       smtp
...
```

重新加载 Postfix 配置后，`smtp` 守护进程将记录 SMTP AUTH 通信*以及*凭证信息的计算过程，例如 base64 字符串的编码或解码。

> **注意** 您可能需要谨慎地将 Postfix 日志发送到邮件列表，因为 `smtp` 会以明文形式记录您的凭证。发布日志前，请务必替换您的用户名和密码（例如用 `XXX` 替代）。

##### 向远程目的地发送测试消息

您可以使用 GUI 邮件客户端将消息传输到 Postfix 客户端守护进程，以此检查客户端认证是否正常工作。或者，您可以使用以下命令行向 `echo@postfix-book.com` 发送一条消息，该地址会将消息回复给信封发件人，其中包含原始消息的完整标题和正文：

```
$ mail -s 'Testing client side authentication' echo@postfix-book.com
Testing...
.
Cc:
$
```

##### 检查日志文件以确认认证成功

最后，使用 `grep` 命令检查 Postfix 日志文件，确认认证成功：

```
# grep '235 Authentication successful' /var/log/maillog
```

如果一切顺利，您应该会看到一行或多行如下所示的内容，表明与 `relay.example.com` 的认证成功：

```
Jan 20 12:40:39 mail postfix/smtp[21740]: < relay.example.com[172.16.0.100]:
  235 Authentication successful
```

**注意** 您的目标邮箱中也应该有一条新消息；请检查此消息的标题。

### lmtp 客户端

配置 Postfix 的 `lmtp` 客户端以使用 SMTP AUTH，与配置 `smtp` 客户端非常相似（请参阅前面的“Postfix SMTP 客户端的 AUTH”部分）。您需要执行以下步骤：

- 1. 通过在 `main.cf` 文件中设置 `lmtp_sasl_auth_enable = yes` 来启用客户端 SMTP AUTH。
- 2. 创建一个保存 SMTP AUTH 凭证的文件。为此，请参考前面的“存储 SMTP AUTH 凭证”部分，但使用 `lmtp_passwd` 作为文件名，而不是 `smtp_passwd`（当然，您也可以与 `smtp` 客户端共享凭证文件）。
- 3. 配置 Postfix 以使用包含 SASL 凭证的文件；在 `main.cf` 文件中设置 `lmtp_sasl_password_maps = /etc/postfix/lmtp_passwd`。
- 4. 将客户端限制为安全的认证机制（如下一节所述）。

#### 将 lmtp 限制为特定机制组

禁止 `lmtp` 客户端守护进程使用不安全机制的过程，与“限制认证机制”部分描述的 `smtp` 客户端守护进程的过程非常相似。例如，如果您想确保客户端不使用明文机制，请如下设置 `lmtp_sasl_security_options` 参数：

```
lmtp_sasl_security_options = noplaintext, noanonymous
```

但是，与 `smtp` 守护进程设置有一点轻微不同：如果您的 `lmtp` 客户端守护进程恰好与 Postfix 服务器位于同一台机器上，并且它们通过套接字通信，那么您不妨稍微放宽设置，允许明文机制：

```
lmtp_sasl_security_options = noanonymous
```

##### 测试 lmtp 客户端的 SMTP AUTH

要测试 `lmtp` 客户端，请执行与前面“测试客户端 SMTP AUTH”部分描述的相同步骤。此外，您可能还想使用 `imtest`，这是 Cyrus IMAP 软件包中的一个实用工具。当您的目标是让 Postfix `lmtp` 客户端将邮件投递到 Cyrus IMAP 服务器附带的 LMTP 服务器时，这特别有用。

# 17

# 理解传输层安全

![](img/852c79f689feb77c5fde686b993808b1_295_0.png)

到目前为止，您已经了解到，从系统的角度来看，Postfix 是相当安全的——也就是说，Postfix 努力消除可能导致入侵的常见安全漏洞。然而，尽管这些努力很高尚，但仍有一些缺失。问题在于，SMTP 在设计上并不能保护您免受可能窃听网络数据包的入侵者的侵害。这听起来可能是个严峻的情况，尽管您可能认为关于危险的描述有些夸张，但在某些真实情况下，确实有必要保护 SMTP 对话免受窃听者的侵害。

例如，一家通过邮件服务器在互联网上交换内容的公司可能需要考虑对这些内容进行加密，任何运行支持允许明文认证的 SMTP AUTH 的 SMTP 服务器的人都有理由感到担忧。敏感的消息内容和密码将以明文 TCP 数据包传输，任何可能访问该数据流路径的人都可以将 TCP 数据包转储到他们自己的计算机上并重建数据流。

您可以使用传输层安全来解决这个问题，TLS 是一种在任何敏感数据通过线路发出*之前*加密两台主机之间通信的系统。在 Postfix 中，您甚至可以使用 TLS 来允许基于证书系统的中继。本章解释了 TLS 在 Postfix 中的理论，无论是作为邮件客户端、邮件服务器，还是基于客户端证书允许中继的邮件服务器。学完本章后，您还将知道何时使用 TLS 是合理的及其前提条件。

## TLS 基础

默认的 SMTP 客户端-服务器通信未加密。客户端只是建立一个 TCP 连接并开始传输数据（参见图 17-1）。除非内容本身已被另一个系统加密，否则它以明文传输，任何能够监听数据流的人都可以读取它。一个不受欢迎的监听者可以轻松地看到内容，如果他们控制了路由器，还可能修改它。

![](img/852c79f689feb77c5fde686b993808b1_296_0.png)

*图 17-1：未加密通信——对所有人可读*

当客户端和服务器使用 TLS 时，这些攻击就不可能发生（参见图 17-2），因为该系统提供了三样东西：

### 隐私性

客户端和服务器之间的通信封装在一个加密会话中。无法访问客户端和服务器的第三方无法解密交换的数据。

### 完整性

尽管中间人攻击是可能的，但双方都可以立即检测到内容的任何更改。

### 真实性证明

客户端和服务器可以交换由受信任的证书颁发机构验证的证书，这些证书证明了相关主机的真实性。证书包含诸如主机的 FQDN 等信息。仅举一例，DNS 欺骗会在发送数据之前被检测到。

![](img/852c79f689feb77c5fde686b993808b_297_0.png)

*图 17-2：加密通信——仅发送者和接收者可读*

关于 TLS 有三个常见的误解：

- TLS 不保护内容从客户端到服务器之后的安全。一旦服务器接收并存储了消息，它就再次变为明文。
- TLS 仅保证从邮件客户端到邮件服务器的加密。请记住，邮件服务器可能需要将消息传递给另一个服务器。消息在到达最终目的地的路径上的其他邮件服务器可能不支持 TLS。因此，尽管您可以在自己的邮件枢纽上强制执行加密，但一旦消息离开您的组织，您可能就无法控制传输。只要路径上的某个服务器不支持 TLS，它就会回到明文。
- TLS 不一定保护接受后又作为无法投递返回的邮件。无法保证退信会遵循相同的路径。

如果其中任何一个问题令人担忧，您必须在发送前加密消息内容。流行的邮件加密工具包括 S/MIME、PGP 和 GnuPG。

## TLS 的工作原理

传输层安全仅加密两台主机之间的通信。启用 TLS 的会话按如下流程进行：

- 1. 客户端连接到服务器。
- 2. 主机启动 SMTP 通信。
- 3. 服务器在 SMTP 通信中使用 `STARTTLS` 关键字提供 TLS。
- 4. 如果客户端能够使用 TLS，它会通过向服务器发送 `STARTTLS` 来响应。
- 5. 公共服务器证书使用私钥签名并发送给客户端。
- 6. 客户端通过检查其 CA 签名与客户端自身根存储中的公共 CA 签名是否匹配来验证服务器的证书。



7. 客户端通过比对证书的通用名称字符串与服务器的 DNS 主机名来验证服务器证书。
8. 客户端和服务器切换到加密通信。
9. 主机之间交换数据。
10. 会话结束。

从上述流程可以看出，证书在 TLS 中扮演着重要角色。

## 了解证书

加密技术并不依赖于证书，但证书是确保只有预期的通信双方才能实际进行通信的必要条件。如果每个主机都能验证对方的证书，它们就同意对会话进行加密。否则，它们将中止整个加密流程并发出警告，因为缺少信任（真实性）基础。

### 如何建立信任

创建证书时，系统会向磁盘写入两个文件：一个包含公钥，另一个包含私钥。发送主机使用其私钥对某些数据进行加密，接收主机则使用公钥进行解密并验证发送方的真实性。可以通过 CA 签名来验证公钥——CA 充当发送主机有效性的担保人。

接收主机每次验证证书时并不会直接查询 CA。这不仅会产生大量流量，而且在验证数据通过网络传输时还会留下过多被外部篡改的空间。相反，接收方会在本地将 CA 公钥的签名与相关证书的校验和进行比对。CA 在签名过程中会计算并将其添加到发送方的证书中。任何对已签名证书的更改都会改变校验和，使其失效，因为 TLS 机制会立即检测到篡改行为。

要在客户端和服务器之间建立信任，必须满足不同的要求：

**客户端**

验证服务器证书真实性的邮件客户端必须能够访问 CA 的公钥。必须有人将此密钥导入客户端操作系统的证书存储中，以便邮件客户端和其他应用程序可以读取。

**服务器**

颁发证书的邮件服务器必须拥有有效的私钥和公钥。公钥必须由 CA 签名。

### 哪个认证机构适合你的需求？

目前有多家认证机构愿意为你的证书签名。选择哪个 CA 最适合你的需求，取决于 CA 的服务和价格，以及你使用证书的原因：

**私人用途**

如果你只是打算将证书用于私人用途，即你或少数用户需要签名证书（例如，公司同事或分布在不同地点但均受你控制的较大网络中的服务器），那么你可以考虑自己充当证书颁发机构。自行签名服务器证书，然后将你的 CA 根证书和服务器证书提供给你的客户端和服务器。这种方式花费的精力和金钱较少，但你组织外部的邮件客户端和服务器不会信任你的证书。

**官方用途**

如果你需要与你无法控制的外部用户和邮件服务器进行官方联系，你应该使用官方 CA 的服务。你可以在 PKI 页面（http://www.pki-page.org）开始搜索适合你特定需求的 CA，那里有全球 CA 的综合列表。

## 创建证书

无论你是打算自己搭建 CA 还是让官方认证机构为你的证书签名，你都需要创建证书签名请求。

创建新证书很简单——你只需运行一个脚本和几条命令，它们会帮你完成大部分工作。运行脚本时，你需要手头准备一些信息。

### 所需信息

以下大部分参数不言自明，你应该不会有任何理解困难。但是，有一个条目需要特别注意：`Common Name`。你在服务器证书中提供的值必须与主机的 DNS 名称匹配。如果不匹配，TLS 会怀疑存在中间人攻击（即有人窃取了证书），并中止验证。对于客户端证书，通常指定个人名称代替。

以下是需要准备的信息：

- 国家
- 州或省
- 城市或其他市政区域
- 组织
- 组织单位
- 通用名称
- 电子邮件地址

### 创建 CA 证书

如果你决定自行签名证书，首先需要创建自己的 CA 证书。（如果你使用官方 CA，请跳至"分发和安装 CA 证书"部分。）在你的 OpenSSL 发行版中运行 `misc/CA.pl -newca`：

```
# ./CA.pl -newca
CA certificate filename (or enter to create)
Making CA certificate ...
Generating a 1024 bit RSA private key
.....++++++
.....++++++
writing new private key to './demoCA/private/cakey.pem'
Enter PEM pass phrase: (1)
Verifying - Enter PEM pass phrase:
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:EX
State or Province Name (full name) [Some-State]:Examplia
Locality Name (eg, city) []:Exampleton
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Example Inc.
Organizational Unit Name (eg, section) []:Certification Authority
Common Name (eg, YOUR name) []:mail.example.com
Email Address []:postmaster@example.com
```

> ⚠️ 生成 CA 证书时，你需要输入密码短语。此后每次以 CA 身份签署和撤销证书时都需要使用该密码。

`misc/CA.pl` 程序会创建子目录，用于存放运行 CA 所需的文件和目录。运行程序后，你应有一个新的 `misc/demoCA` 子目录，其结构如下：

```
# tree demoCA/
demoCA/
|-- cacert.pem (1)
|-- certs
|-- crl
|-- index.txt
|-- newcerts
|-- private
|   `-- cakey.pem ②
`-- serial
```

① cacert.pem 是 CA 的公钥。你的主机需要将其放入证书根存储中，以验证 Postfix 公共证书中的签名。
② cakey.pem 是 CA 的私钥。必须加以保护，只有运行 CA 的用户才应拥有读/写权限。

### 分发和安装 CA 证书

下一步是将 CA 证书分发给所有将使用 TLS 的客户端。如果你运行自己的 CA，可以在 misc/demoCA 中找到 CA 证书。默认情况下，openssl 会将其保存为 cacert.pem。如果你选择了官方认证机构，则需要找到并下载它们的 CA 证书。

如何分发 CA 证书主要取决于使用证书的应用程序及其运行环境。GUI 应用程序通常使用操作系统提供的证书根存储，可对所有证书进行集中管理。

对于仅提供命令行界面并使用 OpenSSL 的服务器，不存在单一的集中式根存储。命令行应用程序可以使用自己的存储，且存储位置必须在每个应用程序内配置。由于 Postfix 是一个命令行应用程序，你需要配置 smtp 守护进程或 smtpd 守护进程（或两者）以访问包含 CA 证书的存储。这部分配置将在第 18 章中介绍。

> NOTE 单独的存储为设计专用解决方案提供了灵活性，但也增加了维护各证书存储中证书最新状态的复杂性。

#### Windows 安装

Windows 要求使用不同格式的证书——OpenSSL 可以为你转换 CA 证书。你不必使用 CA.pl；可以直接运行 openssl。在以下示例中，SSL 安装目录为 /usr/local/ssl：

```
# cd /usr/local/ssl/misc/demoCA
# openssl x509 -in cacert.pem -out cacert.der -outform DER
```

完成后，你会在 /usr/local/ssl/misc/demoCA 中找到一个名为 cacert.der 的新文件。

在 Windows 上安装 CA 证书非常简单：

1. 将 cacert.der 复制到你的 Windows 机器上。
2. 双击 cacert.der 以启动安装过程（参见图 17-3）。
3. 点击**安装证书**，然后按照证书导入向导操作。



#### Linux (KDE-3.1.x) 安装

在 Linux/KDE 上安装 CA 证书与在 Windows 上一样简单：

1. 将 cacert.der 复制到您的 Linux 机器。
2. 在 Konqueror 中双击 cacert.der 以启动安装过程。
3. KDE 启动 KDE 安全证书导入工具。
4. 选择导入。
5. 会出现一个对话框，确认导入成功。
6. 启动 KDE 控制中心，并在左侧窗格中选择安全与隐私。
7. 在左侧窗格中选择加密。
8. 在右侧窗格中单击 SSL 签发者选项卡。
9. 验证新证书是否在此（参见图 17-4）。

#### Mac OS X 安装

在 Mac OS X 上安装证书取决于您运行的版本。以下是适用于所有版本（10.3 之前的 OS X 以及之后版本）的命令行和图形界面步骤的混合。

要手动安装证书，请按照以下步骤操作：

1. 将 cacert.pem 复制到您的主目录。
2. 打开终端窗口。
3. 将 cacert.pem 导入钥匙串：

```
$ sudo certtool i cacert.pem k=/System/Library/Keychains/X509Anchors
...certificate successfully imported
```

要验证证书是否成功导入，请按照以下步骤操作：

1. 在图形界面中打开位于 /Applications/Utilities/ 的钥匙串访问。您将只看到您的本地钥匙串。
2. 从文件菜单中选择添加钥匙串，并将 /System/Library/Keychains/X509Anchors 添加到您的钥匙串。
3. 通过滚动 X509Anchors 钥匙串来搜索您的 CA 证书。名称列应通过您使用的通用名称来引用它（参见图 17-5）。

### 创建服务器的证书

安装 CA 证书后，就该创建 Postfix 服务器证书了。在 `/usr/local/ssl/misc` 的命令行中，运行以下命令。它将生成证书请求，您将在接下来的“签署服务器的证书”部分让 CA 签署该请求：

```
# openssl req -new -nodes -keyout postfix_private_key.pem -out postfix_private_key.pem -days 365
Generating a 1024 bit RSA private key
.....................+++++
..............+++++
writing new private key to 'postfix_private_key.pem'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:EX
State or Province Name (full name) [Some-State]:Exemplia
Locality Name (eg, city) []:Exampleton
Organization Name (eg, company) [Internet Widgits Pty Ltd]:Example Inc.
Organizational Unit Name (eg, section) []:MX Services
Common Name (eg, YOUR name) []:mail.example.com
Email Address []:postmaster@example.com
Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
#
```

> **注意** *除非您编辑它使其不要求在密钥中包含私有密码短语，否则不要使用 misc/CA.pl 来创建私钥文件。添加密码短语意味着每当 Postfix 想要使用证书时，就必须有人输入密码短语！Postfix 在每次启动或重新启动其 smtp 和 smtpd 守护进程时都会加载证书，如果有密码，用户就必须输入它。不用说，像 Postfix 这样的服务器无法自行重启是极其不切实际的。*

### 签署服务器的证书

构建服务器证书的最后一步是让 CA 签署它。如果您使用的是官方 CA，请遵循他们的说明。否则，从命令行运行 **openssl** 从 postfix_private_key.pem 创建 postfix_public_cert.pem。

```
# openssl ca -policy policy_anything -out postfix_public_cert.pem -infiles postfix_private_key.pem
Using configuration from /usr/local/ssl/openssl.cnf
Enter pass phrase for ./demoCA/private/cakey.pem:
Check that the request matches the signature
Signature ok
Certificate Details:
        Serial Number: 1 (0x1)
        Validity
            Not Before: Nov  9 21:25:13 2003 GMT
            Not After : Nov  8 21:25:13 2004 GMT
        Subject:
            countryName               = EX
            stateOrProvinceName       = Examplia
            localityName              = Exampleton
            organizationName          = Example Inc.
            organizationalUnitName    = MX Services
            commonName                = mail.example.com
            emailAddress              = postmaster@example.com
        X509v3 extensions:
            X509v3 Basic Constraints: 
                CA:FALSE
            Netscape Comment: 
                OpenSSL Generated Certificate
            X509v3 Subject Key Identifier: 
                9E:36:9D:9B:ED:4E:32:73:0E:86:55:2A:FF:1B:49:F9:1C:47:17:75
X509v3 Authority Key Identifier:
keyid:00:52:AD:B7:FA:C2:EF:01:1A:9E:7B:0F:57:DB:DC:E4:82:59:8D:0B
DirName:/C=EX/ST=Examplia/L=Exampleton/O=Certification Authority
Example Inc./CN=mail.example.com/emailAddress=postmaster@example.com
serial:00
Certificate is to be certified until Nov  8 21:25:13 2004 GMT (365 days)
Sign the certificate? [y/n]:y
1 out of 1 certificate requests certified, commit? [y/n]y
Write out database with 1 new entries
Data Base Updated
```

postfix_public_cert.pem 是将在初始 TLS 协商期间发送给客户端的证书。除了此证书外，Postfix 还会发送来自 postfix_private_key.pem 的签名。为了验证 postfix_public_cert.pem，接收主机随后将基于 Postfix 的私钥签名和 CA 证书签名进行一些计算。结果必须与 postfix_public_cert.pem 的签名匹配。否则，公钥将被视为伪造，通信将立即终止。

### 准备在 Postfix 中使用的证书

无论您计划将证书用于 smtp（邮件客户端）还是 smtpd（邮件服务器），您都应将所有证书复制到 /etc/postfix/certs：

```
# mkdir /etc/postfix/certs
# cp cacert.pem /etc/postfix/certs
# cp ../*.pem /etc/postfix/certs
```

然后，您必须保护服务器的私钥 postfix_private_key.pem，防止机器上的其他用户访问：

```
# cd /etc/postfix/certs
# chmod 600 postfix_private_key.pem
```

完成后，权限应如下所示：

```
# ls -all certs/
total 20
drwxr-xr-x  2 root  root  4096 Nov  9 23:03 .
drwxr-xr-x  3 root  root  4096 Oct 28 00:13 ..
-rw-r--r--  1 root  root  1379 Nov  9 23:02 cacert.pem
-rw-------  1 root  root  1620 Nov  9 23:02 postfix_private_key.pem
-rw-r--r--  1 root  root  3806 Nov  9 23:02 postfix_public_cert.pem
```

现在您已准备好使用下一章中描述的 Postfix TLS 功能。

## 使用传输层安全

Postfix 的传输层安全有两种形式：客户端 TLS 和服务器端 TLS。除了基本的 TLS 之外，这两种形式还提供用于性能调优和细粒度 TLS 强制实施的功能，以及启用用于安全明文 SMTP AUTH 的封装，并能够基于客户端证书允许中继。

本章向您展示如何为客户端和服务器端 TLS 配置 Postfix。您将看到部署 TLS 的不同方法，以及补充默认 Postfix 守护进程集的 TLS 守护进程。

### 检查 Postfix 对 TLS 的支持

在您可以设置用于 TLS（如 RFC 2487 中所述）的 Postfix 配置文件之前，您必须检查您的 Postfix 版本是否支持它。这很重要，因为标准 Postfix 源代码不包含 TLS

完全不支持——你必须修补 Postfix 源代码才能获得 TLS 和 STARTTLS 支持。不过，如果你使用的是预编译的二进制文件，可能已经包含了 TLS 支持，因为许多 Linux 发行版在其 Postfix 软件包中已包含该功能。Postfix 2.2 将 TLS 作为编译时选项内置。

> **注意** *Postfix 的 TLS 补丁由 Lutz Jänicke 博士开发，他是 OpenSSL 开发团队的成员，专业从事加密技术开发。正如 OpenSSL 网站所述："OpenSSL 项目是一项协作性工作，旨在开发一个健壮的、商业级的、功能齐全的开源工具包，实现安全套接层（SSL v2/v3）和传输层安全（TLS v1）协议，以及一个功能完备的通用密码学库。"有关 OpenSSL 项目的更多信息，请访问 http://www.openssl.org。*

虽然 TLS 支持以补丁形式提供，但你的 Postfix 中可能已经具备了 TLS 支持，因为许多发行版在其 Postfix 软件包中已包含该功能。

要检查你的 Postfix 安装是否支持 TLS，请在 `postconf -d` 的输出中查找 `tls` 相关内容。通过管道连接到 `grep` 命令，应该能返回 TLS 参数及其默认值。以下是示例：

```
# postconf -d | grep tls
smtp_enforce_tls = no
smtp_starttls_timeout = 300s
smtp_tls_CAfile =
smtp_tls_CApath =
smtp_tls_cert_file =
smtp_tls_cipherlist =
smtp_tls_dcert_file =
smtp_tls_dkey_file = $smtp_tls_dcert_file
smtp_tls_enforce_peername = yes
smtp_tls_key_file = $smtp_tls_cert_file
smtp_tls_loglevel = 0
smtp_tls_note_starttls_offer = no
smtp_tls_per_site =
smtp_tls_session_cache_database =
smtp_tls_session_cache_timeout = 3600s
smtp_use_tls = no
smtpd_enforce_tls = no
smtpd_tls_CAfile =
smtpd_tls_CApath =
smtpd_tls_ask_ccert = no
smtpd_tls_auth_only = no
smtpd_tls_ccert_verifydepth = 5
smtpd_tls_cert_file =
smtpd_tls_cipherlist =
smtpd_tls_dcert_file =
smtpd_tls_dh1024_param_file =
smtpd_tls_dh512_param_file =
smtpd_tls_dkey_file = $smtpd_tls_dcert_file
smtpd_tls_key_file = $smtpd_tls_cert_file
smtpd_tls_loglevel = 0
smtpd_tls_received_header = no
smtpd_tls_req_ccert = no
smtpd_tls_session_cache_database =
smtpd_tls_session_cache_timeout = 3600s
smtpd_tls_wrappermode = no
smtpd_use_tls = no
tls_daemon_random_bytes = 32
tls_daemon_random_source =
tls_random_bytes = 32
tls_random_exchange_name = ${config_directory}/prng_exch
tls_random_prng_update_period = 60s
tls_random_reseed_period = 3600s
tls_random_source =
```

所有这些 TLS 相关参数的存在表明系统支持 TLS。

### 使用 TLS 支持构建 Postfix

如果你的二进制文件没有 TLS 支持，你必须构建一个新的 Postfix 安装。首先，检查你的系统中是否有 OpenSSL 库和头文件（即 .h 包含文件）。使用 `find` 命令搜索 SSL 库和包含文件，如下所示：

```
# find /usr -name 'ssl.*'
```

此命令可能需要一些时间才能完成。如果成功，你应该会看到类似以下的输出：

```
/usr/include/openssl/ssl.h
/usr/lib/libssl.so
/usr/lib/libssl.a
```

在此示例中，`ssl.h` 是包含文件，`libssl.so` 是 OpenSSL 库的共享版本，`libssl.a` 是库的静态版本。

如果你在机器上找不到 OpenSSL，可以尝试从你的发行版中找到二进制软件包。请务必安装 OpenSSL 开发包（通常名为 `openssl-dev` 或 `openssl-devel`）；否则你可能无法获取包含文件。

如果你想使用比你的发行版附带版本更新的 OpenSSL，或者找不到二进制软件包，你可以自行编译 OpenSSL。接下来将介绍具体方法。

### 从源代码构建和安装 OpenSSL

OpenSSL、Postfix 和 TLS 补丁套件都在持续开发中。因为 TLS 补丁套件同时依赖 Postfix 和 OpenSSL，所以在下载源代码和补丁套件时，你必须确保所有组件相互兼容。

> **警告** 某些 Linux 发行版附带的 OpenSSL 库可能会在你覆盖系统现有 OpenSSL 安装时导致系统部分功能损坏。如果你的机器上已有 OpenSSL 0.9.6 或更高版本，你应该继续使用该版本，除非你知道如何配置新版本使其不与现有安装冲突。

OpenSSL 0.9.6 或更高版本与 Postfix TLS 兼容良好。作为替代方案，你可以将新库安装到不同的位置，从而避免覆盖关键库的问题。

获取合适源代码的最简单方法是访问 Lutz Jänicke 的网站 http://www.aet.tu-cottbus.de/personen/jaenicke/postfix_tls，在那里你可以找到一个 TLS 兼容性表格。你只需从该表格的同一行中选择 Postfix、TLS 补丁套件和 OpenSSL 源代码，就可以开始构建和安装了。

要安装 OpenSSL，请执行以下步骤：

- 1. 以普通用户身份，使用 `tar xzf openssl-version.tar.gz` 命令解压 OpenSSL 源代码，其中 *version* 是 OpenSSL 版本号。
- 2. 切换到包含 OpenSSL 源代码的新建目录。
- 3. 阅读 INSTALL 文件，确定是否需要任何特殊选项。
- 4. 如果你想构建共享库，请在运行 `configure` 时添加 `--shared` 参数；共享库默认不会构建。如果你将 Postfix 静态链接到 `libopenssl.a`，那么由于安全问题需要更新 OpenSSL 时，你将需要重新编译整个 Postfix。
- 5. 运行 configure 脚本生成 Makefile 后，运行 `make && make test`。
- 6. 切换到超级用户（root），运行 `make install`。如果你没有构建共享库，到此就完成了。
- 7. 验证共享库路径；安装过程会在结束前打印此目录。默认路径为 `/usr/local/ssl/lib`。
- 8. 将共享库路径添加到动态链接器的运行时搜索路径中。在 Linux 上，这意味着你需要将该目录添加到 `/etc/ld.so.conf` 文件中，然后运行 `ldconfig`。在 Solaris 上，你需要运行 `crle`。

### 使用 TLS 构建 Postfix

获取 OpenSSL 库和包含文件后，你就可以构建一个新的支持 TLS 的 Postfix。你需要 Postfix 源代码和 TLS 补丁套件。

> **警告** 请务必在操作前阅读 README 和 INSTALL 文件；安装 TLS 支持的步骤可能在出版日期之后已有所变更。

要构建 Postfix，请按照以下步骤操作：

- 1. 以普通用户身份，将 Postfix 源代码和 TLS 补丁套件分别解压到不同的目录中。
- 2. 切换到 Postfix 源代码目录。
- 3. 运行 `patch -p1 < ../tls_dir/pfixtls.diff` 应用补丁，其中 `tls_dir` 是包含名为 `pfixtls.diff` 的 TLS 补丁文件的目录。
- 4. 设置构建选项，然后运行 `make makefiles` 和 `make`，如下所示，其中 `ssl_prefix` 是你的 SSL 基础目录，`sasl2_prefix` 是你的 SASL2 基础目录。

```
$ CFLAGS="-DUSE_SSL -DUSE_SASL_AUTH -I$sasl2_prefix/include -I$ssl_prefix/includes" AUXLIBS="-L$ssl_prefix/lib -lssl -lcrypto -L$sasl2_prefix/lib -lsasl2"
$ make makefiles
$ make
```

> 这些选项指定了一个支持 TLS 和 SASL2 的 Postfix 构建。要添加更多选项，请阅读 Postfix 源代码树中 readme 目录下的相关文件。

- 5. 切换到超级用户（root）。
- 6. 如果这是首次从源代码安装，运行 `make install`；如果你已有可运行的 Postfix 安装，运行 `make upgrade`。
- 7. 如果你构建的是共享库，请运行 `ldd \`postconf -h daemon_directory\`/smtpd` 以验证动态运行时链接器能否找到你编译 Postfix 时使用的所有库。

完成这些步骤后，你应该拥有一个支持传输层安全的 Postfix 安装。

## 服务端 TLS

在服务端 TLS 中，Postfix 作为邮件服务器（MTA）运行，向邮件客户端提供 TLS 服务（参见图 18-1）。你可以将 Postfix 配置为加密传输层，隐藏整个 SMTP 通信会话；或者安全地接收明文 SMTP AUTH 凭据；或者根据客户端提供的证书来为客户端中继邮件。

> **注意** Postfix 不会向 `sendmail` 命令行工具提供 STARTTLS。这是一项安全特性；支持 TLS 的 `sendmail` 需要访问服务器的私钥。然而，该密钥由 root 拥有且只有 root 可读，而 Postfix 的 `sendmail` 并非以 root 身份运行。



### 基本服务器配置

要设置服务器端 TLS，你需要修改 Postfix 配置文件中的五个参数。此外还应设置两个额外的参数以方便调试（这不仅能帮助你发现问题，还在调整 TLS 会话时非常实用，因为 Postfix 能够识别哪些邮件客户端支持 TLS、哪些不支持）。

配置步骤如下：

1. 在 Postfix 主配置文件中启用 TLS。
2. 告诉 Postfix 在哪里找到 TLS 所需的证书。
3. 将 Postfix 连接到随机数源生成器。
4. 提高日志级别，以便在学习运行 TLS 的过程中获取有用信息。
5. 在邮件头中添加信息，以便进一步追踪 TLS。

#### 启用服务器端 TLS

默认情况下，支持 TLS 的 Postfix 服务器并未启用服务器端 TLS，因此即使客户端请求 TLS，Postfix 也不会提供。要启用服务器端 TLS，请在 `main.cf` 中将 `smtpd_use_tls` 参数设置为 `yes`：

```
smtpd_use_tls = yes
```

重新加载配置后，Postfix 会在 SMTP 对话中向邮件客户端提供 STARTTLS，告知它们可以协商 TLS 会话。然而，仅启用服务器端 TLS 还不足以使其正常工作，因为你尚未告诉 Postfix 在哪里找到 TLS 会话所必需的服务器证书。你将在邮件日志中看到类似如下消息：

```
Dec  1 03:07:13 mail postfix/smtpd[741]: TLS engine: do need at least RSA _or_ DSA cert/key data
```

#### 设置证书路径

下一步是添加保存服务器证书的文件或目录路径。你至少需要提供由认证机构签名的服务器密钥和证书，以及创建证书请求时使用的相应私钥。两项声明均在 main.cf 中。以下是一个示例，证书位于 /etc/postfix/certs：

```
smtpd_tls_key_file = /etc/postfix/certs/postfix_private_key.pem ❶
smtpd_tls_cert_file = /etc/postfix/certs/postfix_public_cert.pem ❷

❶ smtpd_tls_key_file 是私钥的路径。
❷ smtpd_tls_cert_file 是服务器证书的路径。
```

> NOTE *以上设置假设你的服务器证书和私钥位于单独的文件中。如果你决定将两个证书放在同一个文件中，可以通过类似 `smtpd_tls_cert_file = $smtpd_tls_key_file` 的配置行将一个参数指向另一个。*

设置完这些证书参数后，你就可以在服务器端 TLS 模式下运行 Postfix 了，但日志文件中仍会有一些错误和警告。这是因为 Postfix 无法传输 CA 的证书，也无法验证邮件客户端发送的证书。你还需要配置 CA 证书的来源。

#### 配置 Postfix 证书根存储

如第 17 章前面所述，OpenSSL 没有默认的集中根存储，因此你需要创建专为邮件系统设计的根存储，或使用系统上已有的根存储。你即将看到的配置使用的是 Apache mod_ssl 模块附带的 ca-bundle.crt 文件，其中包含多个 CA 证书和 Apache 的服务器证书。

> NOTE *你可能需要自行收集 CA 证书，以确保它们确实来自相应的认证机构，而不是在打包过程中被某些第三方篡改。这是最安全的做法，因为如果该机制所依赖的证书是伪造的，那么所有 TLS 安全措施都将付诸东流。*

*在准备为服务器收集 CA 证书时，请做好花费大量时间的心理准备。我们在研究本章时发现，收集证书是一项非常耗时的任务。几乎所有认证机构似乎都把相关信息藏在了他们网站的深处。*

要在系统上找到 Apache mod_ssl 的 ca-bundle.crt，请在命令行运行 `locate ca-bundle.crt`：

```
$ locate ca-bundle.crt
/usr/share/ssl/certs/ca-bundle.crt
```

如果你没有 `locate` 命令，就需要使用较慢的 `find` 命令：

```
$ find / -name ca-bundle.crt
```

找到或安装根存储后，你必须在 `main.cf` 中通过 `smtpd_tls_CAfile` 参数配置 Postfix 使用它。示例如下：

```
smtpd_tls_CAfile = /usr/share/ssl/certs/ca-bundle.crt
```

如果你自己充当认证机构，则需要将你的 CA 证书添加到该根存储中。你只需使用 `cat` 命令将你的证书追加到现有根文件的末尾，示例如下：

```
$ cat /usr/local/ssl/misc/demoCA/cacert.pem >> /usr/share/ssl/certs/ca-bundle.crt
```

> **NOTE** *如果你的 CA 证书是证书链中的一环，请将从你的 CA 证书向下直到根 CA 证书的所有 CA 证书全部添加。*

`smtpd_tls_CAfile` 参数要求所有证书位于单个文件中。作为替代方案，Postfix 提供了 `smtpd_tls_CApath` 参数，你可以将其设置为一个目录，其中的证书以单独文件的形式存储。

> **NOTE** *存储方式并非 `smtpd_tls_CAfile` 和 `smtpd_tls_CApath` 之间的唯一区别。`smtpd_tls_CApath` 中的文件仅在 Postfix 需要验证证书时才会被查询。而 Postfix 在启动时、进入 chroot jail 之前就会读取 `smtpd_tls_CAfile` 参数指定的文件。因此，如果你决定在 chroot 环境中运行 Postfix，`smtpd_tls_CAfile` 是更好的选择，因为你可以将证书文件放在 chroot jail 之外。*

你最好同时设置这两个参数，将部分 CA 证书从单个文件的主批次中分离为单独文件。Postfix 会先读取 `smtpd_tls_CAfile` 指定的文件，然后将 `smtpd_tls_CApath` 作为后备。

#### 将 Postfix 连接到随机数源生成器

TLS 是一种安全的邮件发送方式，不仅因为它对通信层进行加密，还因为它不会为任何两组密码使用相同的数字组合。TLS 实现通过为所有新的 TLS 会话选择（伪）随机数来做到这一点。

OpenSSL 不会自行生成随机数，因为大多数 Linux 和 BSD 衍生系统在 `/dev` 中作为系统设备内置了随机数源。

> **NOTE** *如果你的系统没有内置随机数生成功能，你可以使用伪随机数生成器守护进程（同样由 Lutz Jänicke 开发）。要配置 Postfix 使用该守护进程，请在 `main.cf` 中设置 `tls_random_exchange_name` 参数。更多详情请查看 Postfix 发行版中的 `samples/sample-tls.cf`。*

你的系统上通常可用的两个随机数源是 `dev:/dev/random` 和 `dev:/dev/urandom`。

**/dev/random**

/dev/random 生成器提供高质量的随机数据，但你不应在大量使用 TLS 的系统上使用它。原因是 /dev/random 在 TLS 快速请求随机数据时可能会阻塞，耗尽随机源。如果发生这种情况，Postfix 会停止工作，直到系统积累足够的熵才能再次提供数字。

**/dev/urandom**

/dev/urandom 生成器永远不会阻塞，因为它使用内部伪随机数生成器来创建熵数据。对于自动启动 Postfix 的系统，请使用 /dev/urandom。

要将 Postfix 连接到随机数源生成器，请在 main.cf 中设置 tls_random_source 参数并重新加载配置：

```
tls_random_source = dev:/dev/urandom
```

> **NOTE** OpenSSL 版本高于 0.9.6 会自动检测 /dev/urandom。如果你使用的是这些版本之一，则无需设置 tls_random_source。OpenSSL 0.9.7 更进一步，可以检测其他随机数源生成器。如果你使用的是 OpenSSL 0.9.7，请参阅其文档了解更多详情。

#### 提高 TLS 日志级别

TLS 子系统提供 smtpd_tls_loglevel 参数来控制写入邮件日志的 TLS 相关信息量。表 18-1 描述的五个级别控制日志的详细程度。

**表 18-1：smtpd 的 smtpd_tls_loglevel 级别**

| 日志级别 | 描述 |
|---|---|
| 0 | 不记录 TLS 日志；这是默认值 |
| 1 | 启动和证书信息 |
| 2 | 级别 1 的全部内容，加上 TLS 协商各阶段的信息 |
| 3 | 级别 2 的全部内容，加上协商过程的十六进制和 ASCII 转储 |
| 4 | 级别 3 的全部内容，加上邮件客户端发送 STARTTLS 后完整传输的十六进制和 ASCII 转储 |

首次启用服务器端 TLS 时，请将日志级别设置为 2，这将为你提供足够的信息以便在出现问题时开始调试：

```
smtpd_tls_loglevel = 2
```

#### 在邮件头中添加信息

你还可能希望邮件服务器在每条使用 TLS 发送的消息的 Received 头中添加 TLS 信息。请在 main.cf 中按如下方式设置 smtpd_tls_received_header 参数。



### 测试服务器端 TLS

配置好 TLS 基础设置后，需要进行三项测试：

- 1. 检查日志文件，查看 Postfix 是否遇到任何错误。
- 2. 检查 SMTP 对话中的 STARTTLS，确认 Postfix 已提供 TLS。
- 3. 使用 openssl 程序测试 TLS，证明 Postfix 能够使用您在基础配置中提供的证书启动 TLS 会话。

smtpd_tls_received_header = yes

重新加载配置后，您应该在邮件头中看到类似这样的信息：

> Received: from client.example.com (client.example.com [172.16.0.3])
> (使用 TLSv1，密码为 EDH-RSA-DES-CBC3-SHA (168/168 位))
> (未请求客户端证书)
> by mail.example.com (Postfix) with ESMTP id B637A7247
> for <tls-bounce@mail.examples.com>; Wed, 10 Dec 2003 23:37:02 +0100 (CET)

##### 检查日志文件

第一项测试是使用正则表达式扫描日志文件以查找 TLS 支持：

```
$ egrep '(reject|error|warning|fatal|panic):' /var/log/maillog
```

此命令会打印出 /var/log/maillog 中所有包含单词 reject、error、warning、fatal 或 panic 后跟冒号 (:) 的行。
如果您操作正确，就不应该有任何与 TLS 相关的错误。如果出现问题，请检查配置文件是否有拼写错误，并检查证书的读取权限。

#### 在 SMTP 通信中查找 STARTTLS

您应该进行的下一个测试是运行一个 telnet 会话连接到 Postfix 服务器，以验证它是否向邮件客户端提供 TLS。请仔细查看以下输出中的 STARTTLS 关键字：

```
$ telnet localhost 25
220 mail.example.com ESMTP Postfix
EHLO client.example.com
250-mail.example.com
250-PIPELINING
250-SIZE 10240000
250-VRFY
250-ETRN
250-STARTTLS
250-AUTH NTLM LOGIN PLAIN OTP DIGEST-MD5 CRAM-MD5
250-XVERP
250 8BITMIME
QUIT
221 Bye
```

#### 使用 OpenSSL 模拟 TLS 邮件客户端-服务器会话

最后一项测试是使用 openssl 的 s_client 选项模拟邮件客户端到服务器的会话。OpenSSL 客户端可以使用 TLS/SSL 连接到远程主机，并在此过程中打印出大量诊断信息。如果成功，您的 TLS 服务器配置就正常工作，现在可以使用邮件客户端进行测试了。如果此测试失败，您将获得丰富的有用调试信息来追踪错误。以下是一个成功会话的示例，其中您的 CA 路径为 /etc/postfix/certs：

```
# openssl s_client -starttls smtp -CApath /etc/postfix/certs/ -connect localhost:25
CONNECTED(00000003)
depth=1 /C=DE/ST=Bavaria/L=Munich/O=Postfix Book/OU=#Authoring/CN=mail.example.com/emailAddress=postmaster@example.com
verify return:1
depth=0 /C=DE/ST=Bavaria/L=Munich/O=Postfix Book/OU=Mailserver/CN=mail.example.com/emailAddress=postmaster@example.com
verify return:1
---
Certificate chain
 0 s:/C=DE/ST=Bavaria/L=Munich/O=Postfix Book/OU=Mailserver/CN=mail.example.com/emailAddress=postmaster@example.com
   i:/C=DE/ST=Bavaria/L=Munich/O=Postfix Book/OU=#Authoring/CN=mail.example.com/emailAddress=postmaster@example.com
 1 s:/C=DE/ST=Bavaria/L=Munich/O=Postfix Book/OU=#Authoring/CN=mail.example.com/emailAddress=postmaster@example.com
   i:/C=DE/ST=Bavaria/L=Munich/O=Postfix Book/OU=#Authoring/CN=mail.example.com/emailAddress=postmaster@example.com
---
Server certificate
-----BEGIN CERTIFICATE-----
MIID4DCCAoMgAwIBAgIBATANBgkqhkiG9w0BAQQFADCBnjELMAkGA1UEBhMCREUx
EDAOBgNVBAgTB0JhdGFyaWExDzANBgNVBAcTBk11bmNoMQ0wCwYDVQQREwQxMTIx
MDZpeCBCb29rMRMwEQYDVQQLEw0vQXV0aG9yaW5nMQ0wCwYDVQQREwQxMTIxMDZpe
Yw1gbGUuY29tMSUwIwYJKoZIhvcNAQkBFhZwb3N0bWFzdGVyQGV4YW1wbGUuY29t
MB4XDTEzMTAyMzIwMtkyOVoXDTAyMjAxMDAyMTkwMtkyOWowZzxCzAJBgNVBAYTAkRF
MRAwDgYDVQQIEwdCYXZhcmlhMQ8wDQYDVQQHEwZNdW5jaDELMAkGA1UECREwMTIx
c3RmaXggQm9vazETMBEGA1UECXMKTWZpbHNlcnZpY2VZMBcGA1UEAxMQbWFpbHBv
Y3N0ZQ==
-----END CERTIFICATE-----
subject=/C=DE/ST=Bavaria/L=Munich/O=Postfix Book/OU=Mailserver/CN=mail.example.com/emailAddress=postmaster@example.com
issuer=/C=DE/ST=Bavaria/L=Munich/O=Postfix Book/OU=#Authoring/CN=mail.example.com/emailAddress=postmaster@example.com
---
No client certificate CA names sent
---
SSL handshake has read 2592 bytes and written 356 bytes
---
New, TLSv1/SSLv3, Cipher is DHE-RSA-AES256-SHA
Server public key is 1024 bit
SSL-Session:
    Protocol  : TLSv1
    Cipher    : DHE-RSA-AES256-SHA
    Session-ID: D341BF543EB5690DA873EFD0B04CB2EF210930812C14F3DBB85BD1AE92C6CB3
    Session-ID-ctx: 
    Master-Key: D4E3B4617214EDA8E1D2EFAF54482FC65D1BD7BF5474F2FB2E2C0312BE098D8AF29ABC6603C4A89B7B413ED24D79375CD
    Key-Arg   : None
    Start Time: 1068108666
    Timeout   : 300 (sec)
    Verify return code: 0 (ok)
---
220 mail.example.com ESMTP Postfix (2.0.16-20030921)
QUIT
DONE
```

使用传输层安全 289

### 服务器性能调优

加密操作会给您的处理器带来负载。在每个 TLS 会话开始时，客户端和服务器会执行多个私钥操作来签名握手消息——这是一个计算成本高昂的过程。大量同时进行的 TLS 会话可能会严重拖慢邮件服务器的速度。

默认情况下，Postfix 的 smtpd 会为其连接记住会话密钥。但是，Postfix 也允许 smtpd 进程在一段时间不活动后终止，以节省服务器资源并加载可能的新配置信息。不幸的是，这意味着 Postfix 在 smtpd 终止后会丢失会话密钥，因此当邮件客户端返回传输另一条消息时，它必须重新计算密钥。

为避免当 smtpd 实例终止时会话密钥的丢失，Postfix 可以维护一个进程外会话密钥缓存，如下一节所述。

#### 配置 TLS 会话密钥缓存

为避免 TLS 加密可能产生的计算负载问题，您需要配置 smtpd 进程将会话密钥存储在数据库中。一旦一个 smtpd 存储了密钥，所有 smtpd 进程都可以访问该密钥，无论它们是刚刚启动还是已经运行了很长时间。会话密钥缓存可显著降低 CPU 负载。

要启用会话密钥缓存，请设置 `smtpd_tls_session_cache_database` 参数，并启用 `tlsmgr` 守护进程。`main.cf` 中的参数如下所示：

```
smtpd_tls_session_cache_database = sdbm:/etc/postfix/smtpd_scache
smtpd_tls_session_cache_timeout = 3600s
```

注意：会话密钥缓存需要对密钥数据库进行并发写入访问。在 Postfix 中，只有 SDBM 数据库类型支持此功能。所有启用了 TLS 的 Postfix 安装都识别此密钥类型。

默认情况下，数据库中的所有会话密钥在一小时（3,600 秒）后过期。RFC 2246 建议最大超时时间为 24 小时。您可以通过为 `smtpd_tls_session_cache_timeout` 设置不同的值（以秒为单位）来更改默认行为。

##### 使用 tlsmgr 维护 TLS 会话密钥缓存

Postfix 需要主动维护其 TLS 会话密钥缓存数据库。出于安全原因，您必须在密钥过期时将其删除，同时还需要防止数据库无限制地增长。仅存在于支持 TLS 的 Postfix 安装中的 `tlsmgr` 守护进程执行这些任务。以下是 `tlsmgr` 所做工作的具体说明：

- 在没有内置随机支持的系统上，协助生成随机数
- 根据 `smtpd_tls_session_cache_timeout` 的定义，从会话缓存数据库中清除过期的密钥
- 在您重新启动 Postfix 时，从头开始重建由 `smtpd_tls_session_cache_database` 指定的数据库

要运行 `tlsmgr`，您必须验证它在 `master.cf` 中是否已启用。对于从源代码构建的安装，您应该不需要更改任何内容，但某些发行版在其 Postfix 软件包中禁用了该守护进程，因此确保它在您的 `master.cf` 中未被注释掉总是有益的，如下所示：

```
# ===================================================================
# service type  private unpriv  chroot  wakeup  maxproc  command + args
# (yes)   (yes)  (yes)  (never)   (100)
# ===================================================================
...
tlsmgr      fifo  -       -       n       300       1  tlsmgr
...
```

> **警告** 切勿将 TLS 会话缓存数据库放在 chroot 监狱中。被破坏的会话缓存数据库可能被用来欺骗邮件客户端，使其相信正在与安全的邮件服务器通信，从而允许客户端传输敏感信息。

您可以以 chroot 方式运行 `tlsmgr` 守护进程，因为它在更改其根目录之前就会打开会话密钥数据库，因此能够在 chroot 环境下读写数据库。

在 `master.cf` 中进行相应更改后，您必须重新加载 Postfix 才能启动 `tlsmgr`。

#### 服务器端保护 SMTP AUTH 握手的措施

SMTP AUTH 可能提供明文安全机制，例如 PLAIN 和 LOGIN。某些邮件客户端，特别是 Microsoft Outlook 和 Outlook Express，目前只能使用这些机制。尽管用户通常对安全机制不敏感，但使用明文进行 SMTP AUTH 往往会让管理员感到紧张，因为任何能够在网络上读取原始数据包的人都可以轻松提取用户名和密码。

您可以通过仅在 TLS 连接建立后才提供 SMTP AUTH 来防止明文用户名和密码的提交。

##### 仅通过 TLS 提供 SMTP AUTH

Postfix 提供了 `smtpd_tls_auth_only` 参数，以便仅在建立加密的 SMTP 连接后才提供 SMTP AUTH。此参数默认未启用；要将其打开，请将此行添加到 `main.cf` 并重新加载您的配置：

```
smtpd_tls_auth_only = yes
```

请记住，将 SMTP AUTH 限制为 TLS 会话是从非加密 SMTP 会话中禁止明文机制的一种非常严格的方法，它禁止某些其他（更安全的机制）用于常规 SMTP 通信。



##### 验证 TLS 强制执行

要验证你的 TLS 强制执行，请确保 Postfix 服务器不会为未加密的会话提供 SMTP AUTH。通过端口 25 连接到你的服务器，并使用 EHLO yourFQDN 开始握手，如下所示：

```
$ telnet mail.example.com 25
220 mail.example.com ESMTP Postfix
EHLO client.example.com
250-mail.example.com
250-PIPELINING
250-SIZE 10240000
250-VRFY
250-ETRN
250-STARTTLS
250 8BITMIME
QUIT
221 Bye
```

请注意，此 SMTP 会话中未出现 SMTP AUTH 及其机制，因此此配置的第一步是有效的。

###### 使用加密传输层进行测试

现在你应该检查在 TLS 会话中是否提供了 SMTP AUTH。如之前测试 TLS 时一样，运行 openssl s_client 连接到你的服务器，然后像之前的 telnet 会话一样发出 EHLO yourFQDN。虽然这次输出的内容多得多，但你应该能够从末尾找出 SMTP AUTH 信息：

```
# openssl s_client -starttls smtp -CApath /etc/postfix/certs/ -connect localhost:25
CONNECTED(00000003)
depth=1 /C=EX/ST=Exemplia/L=Exampleton/O=Certification Authority Example Inc./
CN=mail.example.com/emailAddress=postmaster@example.com
verify return:1
depth=0 /C=EX/ST=Exemplia/L=Exampleton/O=Example Inc./OU=MX Services/CN=mail.example.com/
emailAddress=postmaster@example.com
verify return:1
---
Certificate chain
 0 s:/C=EX/ST=Exemplia/L=Exampleton/O=Example Inc./OU=MX Services/CN=mail.example.com/
emailAddress=postmaster@example.com
   i:/C=EX/ST=Exemplia/L=Exampleton/O=Certification Authority Example Inc./CN=mail.example.com/
emailAddress=postmaster@example.com
 1 s:/C=EX/ST=Exemplia/L=Exampleton/O=Certification Authority Example Inc./CN=mail.example.com/
emailAddress=postmaster@example.com
   i:/C=EX/ST=Exemplia/L=Exampleton/O=Certification Authority Example Inc./CN=mail.example.com/
emailAddress=postmaster@example.com
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIDjCCAh+gAwIBAgIBATANBgkqhkiG9w0BAQFADCBpjELMAkGA1UEBhMCRVgx
ETAPBgNVBAgTCEV4YW1wbGlhMRMwEQYDVQQHEwpFeGFtcGxlG9uZTAxMCowKgYD
VQQKEyJDZXJ0aWZpY2F0aW9uIEF1dGhvcml0eSBFeGFtcGxlIEluYy4xGDAWBgNV
BAsTD01YIFNlcnZpY2VzMR0wGwYDVQQDExRtYWlsLmV4YW1wbGUuY29tMB4XDTEy
MDkwMTAwMDAwMFoXDTIyMDkwMTAwMDAwMFowgbkxCzAJBgNVBAYTAkVYMQ0wCwYD
VQQIEwRFeGFtcDEdMBsGA1UEBxMURXhhbXBsZXRvbjEaMBgGA1UEChMRRXhhbXBs
ZSBJbmMuLkwuMS4xHDAaBgNVBAsTE01YIFNlcnZpY2VzMR0wGwYDVQQDExRtYWls
LmV4YW1wbGUuY29tMR0wGwYDVQQDEytwb3N0bWFzdGVyQGV4YW1wbGUuY29tMIIB
IjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAuFhAwbGlmVJ1bGhMRYWkEQYD
VQQHEwpFeGFtcGxlT24xMDAuMCogJkNVBAoTQ2VydGlmaWNhdGlvbiBBdXRob3Jp
dHkgRXhhbXBsZSBJbmMuLjAYMBYGA1UEBxMPTVggU2VydmljZXMxHTAbBgNVBAMT
FHVzZXIzQGV4YW1wbGUuY29tMB4XDTEwMDEwMTAwMDAwMFoXDTE5MTIzMTIzNTk1
OVowRTELMAkGA1UEBhMCQVUxDTALBgNVBAgTBE5TV0ExEjAQBgNVBAoTCUV4YW1w
bGUgQ28uMRIwEAYDVQQDEwlsb2NhbGhvc3QwggEiMA0GCSqGSIb3DQEBAQUAA4IB
DwAwggEKAoIBAQC5WEDBsaWZUnVsaExFhaQRBgdUQ05FZXdvZkVVbHBoTVZFUzZs
bGhNUnVXREYDVQQHEwpFeGFtcGxlT24xMDAuMCogJkNVBAoTQ2VydGlmaWNhdGlv
biBBdXRob3JpdHkgRXhhbXBsZSBJbmMuLjAYMBYGA1UEBxMPTVggU2VydmljZXMx
HTAbBgNVBAMTHXVzZXIzQGV4YW1wbGUuY29tMIGfMA0GCSqGSIb3DQEBAQUAA4GN
ADCBiQKBgQDNQKqGgSsUOZ+2J5k6cLhP1h9XVfE8B2fXHjyvUqJ9XJZbRQ3nE7k
6vGzYwIDAQABo2MwYTAPBgNVHRMBAf8EBTADAQH/MA8GA1UdDwEB/wQEAwIFoDAr
BgNVHRMBAf8ECDAwHgYDVR0lBBcwFQYIKwYBBQUHAwEGCSsGAQQBgb5JegIDA0EA
xJl9aJ7Vh2vUeI8T8R9nRk5n8O6wH4xj1K3nE7m6vFyYwIDAQABMA0GCSqGSIb3
DQEBCwUAA4IBAQBR9o7N8e8S9Xk8TQ1r8S9mNz0wK3nE7m6vf2Yw-----END CERTIFICATE-----

subject=/C=EX/ST=Exemplia/L=Exampleton/O=Example Inc./OU=MX Services/CN=mail.example.com/emailAddress=postmaster@example.com

issuer=/C=EX/ST=Exemplia/L=Exampleton/O=Certification Authority Example Inc./CN=mail.example.com/emailAddress=postmaster@example.com

---

Acceptable client certificate CA names
/C=EX/ST=Exemplia/L=Exampleton/O=Certification Authority Example Inc./CN=mail.example.com/emailAddress=postmaster@example.com

---

SSL handshake has read 2822 bytes and written 368 bytes

---

New, TLSv1/SSLv3, Cipher is DHE-RSA-AES256-SHA
Server public key is 1024 bit
SSL-Session:
    Protocol  : TLSv1
    Cipher    : DHE-RSA-AES256-SHA
    Session-ID: 01DFC00E443BBA8E4E9FE65C7F398702D7BB95367E62D9CBD12F217A97A9B8FC
    Session-ID-ctx:
    Master-Key: E0F1C5F47787E3D9CE236E38407555DE544C97BB9F81ACE3343C897DF8E50691AB432D03E2D79509F452DA7BB363CB8
    Key-Arg   : None
    Start Time: 1071223541
    Timeout   : 300 (sec)
    Verify return code: 0 (ok)
---
220 mail.example.com ESMTP Postfix
EHLO client.example.com
250-mail.example.com
250-PIPELINING
250-SIZE 10240000
250-VRFY
250-ETRN
250-AUTH NTLM LOGIN PLAIN OTP DIGEST-MD5 CRAM-MD5
250-AUTH=NTLM LOGIN PLAIN OTP DIGEST-MD5 CRAM-MD5
250-XVERP
250 8BITMIME
QUIT
DONE
```

通过上述以***粗斜体***显示的 AUTH 输出，你可以看到 Postfix 确实在加密连接时提供了 SMTP AUTH。现在你可以将邮件客户端配置为在 SMTP AUTH 中使用明文机制配合 TLS。

###### 在 TLS 中控制 SASL 机制

在常规 SMTP 通信中禁止明文机制的一种更精细的方式是使用 `smtpd_sasl_tls_security_options` 参数。与上一节类似，此参数指定明文机制必须在 TLS 会话中受到保护，但也允许在未加密通信中使用非明文机制。将 SASL 的 `smtpd_sasl_security_options` 参数与 `smtpd_sasl_tls_security_options` 参数巧妙组合，即可实现这一点：

```
smtpd_sasl_security_options = noanonymous, noplaintext
smtpd_sasl_tls_security_options = noanonymous
```

第一行表示不允许匿名和明文认证，但第二行覆盖了这一设置，表示在 TLS 会话中可以使用明文。

###### 使用 TLS 测试 SASL

与禁止所有 SMTP AUTH 机制时一样，测试 SASL 配置的第一步是确保 Postfix 不会在未加密的会话中提供明文机制。通过端口 25 连接到你的服务器，发出 EHLO yourFQDN，并观察结果：

```
$ telnet mail.example.com 25
220 mail.example.com ESMTP Postfix
EHLO client.example.com
250-mail.example.com
250-PIPELINING
250-SIZE 10240000
250-VRFY
250-ETRN
250-STARTTLS
250-AUTH NTLM OTP DIGEST-MD5 CRAM-MD5
250-AUTH=NTLM OTP DIGEST-MD5 CRAM-MD5
250 8BITMIME
QUIT
221 Bye
```

请注意，SMTP AUTH 行中缺少明文的 LOGIN 和 PLAIN 机制，这证明 `smtpd_sasl_security_options = noanonymous, noplaintext` 设置生效了。

###### 测试加密传输层

在验证了 `smtpd_sasl_security_options` 设置生效后，检查你的 `smtpd_sasl_tls_security_options = noanonymous` 设置是否按预期工作。使用 openssl s_client 连接到你的服务器，并像之前一样发出 EHLO yourFQDN。结果应如下所示：

```
# openssl s_client -starttls smtp -CApath /etc/postfix/certs/ -connect localhost:25
CONNECTED(00000003)
depth=1 /C=EX/ST=Examplia/L=Exampleton/O=Certification Authority Example Inc./
CN=mail.example.com/emailAddress=postmaster@example.com
verify return:1
depth=0 /C=EX/ST=Examplia/L=Exampleton/O=Example Inc./OU=MX Services/CN=mail.example.com/
emailAddress=postmaster@example.com
verify return:1
---
Certificate chain
 0 s:/C=EX/ST=Examplia/L=Exampleton/O=Example Inc./OU=MX Services/CN=mail.example.com/
emailAddress=postmaster@example.com
   i:/C=EX/ST=Examplia/L=Exampleton/O=Certification Authority Example Inc./CN=mail.example.com/
emailAddress=postmaster@example.com
 1 s:/C=EX/ST=Examplia/L=Exampleton/O=Certification Authority Example Inc./CN=mail.example.com/
emailAddress=postmaster@example.com
   i:/C=EX/ST=Examplia/L=Exampleton/O=Certification Authority Example Inc./CN=mail.example.com/
emailAddress=postmaster@example.com
---
Server certificate
-----BEGIN CERTIFICATE-----
MIID9jCCA1+gAwIBAgIBATANBgkqhkiG9w0BAQQFADCBpjELMAkGA1UEBhMCRVgx
ETAPBgNVBAgTCEV4YW1wbGlhMRMwEQYDVQQHEwpFeGFtcGxldG9uMSowKAYDVQQK
EyRDZXJ0aWZpY2F0aW9uIEF1dGhvcml0eSBFeGFtcGxlIEluYy4xGTAXBgNVBAMT
EG1haWwuZXhhbXBsZS5jb20xJTAjBgkqhkiG9w0BCQEWFnBvc3RtYXN0ZXJAZXhh
bXBsZS5jb20wHhcNMDQxMTA5MjEyNTEzWhcNMDQxMTA5MjEyNTEzWjCBpDELMAkG
A1UEBhMCRVgxETAPBgNVBAgTCEV4YW1wbGlhMRMwEQYDVQQHEwpFeGFtcGxldG9u
```

### 基于证书的服务器端中继

可以看到，在 TLS 会话中，Postfix 提供了明文的 LOGIN 和 PLAIN 机制，这证明了 `smtpd_sasl_tls_security_options = noanonymous` 设置生效。你现在可以继续配置邮件客户端，使其在 SMTP AUTH 中与 TLS 一起使用明文机制。

Postfix 允许基于客户端证书进行中继的能力（参见图 18-2）是基于 SMTP AUTH 中继的一种替代方案。这在无法（或不想）使用 SMTP AUTH 的网络中很有用，或者当您希望通过将中继和传输层加密合并为一个步骤来简化流程时。

这种方法的唯一缺点是，已知支持此类功能的唯一邮件 GUI 是 Netscape/Mozilla 邮件客户端。尽管存在此限制，但在大型网络中，当多个不同位置安装了 Postfix，并且这些位置仅通过拨号方式访问互联网且受限于动态 IP 地址时，此方法仍然很有用。在这种情况下，让拨号的 Postfix 服务器将其外发消息中继到具有静态 IP 地址的 Postfix 服务器是有意义的，使用基于证书的中继可确保消息来自拨号服务器之一，而不是某个随机的第三方。这种方法还简化了服务器设置，通过排除 SMTP AUTH 使 Postfix 更安全，并保护内部消息的传输。

> **注意** *随着时间的推移，越来越少的邮件服务器接受来自拨号和 DSL 线路的邮件，因为大量垃圾邮件源自这些系统的 IP 地址。称为拨号用户列表 (DUL) 的特殊 DNS 黑洞列表 (DNSBL) 现在禁止已知由拨号机器使用的所有子网。*

您需要执行以下步骤来配置服务器：

- 1. 配置 Postfix 以请求客户端证书。
- 2. 配置 Postfix 以允许基于客户端证书的中继。

> **注意** *基于证书的中继要求您同时配置服务器端和客户端的 TLS。本节解释服务器端配置；您将在本章后面看到客户端配置。*

#### 配置 Postfix 以请求客户端证书

启用基于证书中继的第一步是指示 Postfix 明确请求客户端证书。这是必要的，因为邮件客户端通常不会自动提供其证书。`smtpd_tls_ask_ccert` 参数处理此问题（默认情况下未启用）：

```
smtpd_tls_ask_ccert = yes
```

此参数对于调试也很有用，并且您可以始终保持其开启状态，因为添加到通过 TLS 发送的每条消息头部的信息不会造成任何安全风险。

> **注意** *如果没有可用证书，Netscape 的邮件客户端会抱怨或提供多个客户端证书供选择。这种行为很烦人，因此默认情况下此选项是关闭的。但是，如果您想使用基于证书的中继，您的 SMTP 服务器需要该证书。*

#### 配置 Postfix 以允许基于客户端证书的中继

Postfix TLS 补丁包含两个额外的限制，可以使用 `smtpd_recipient_restrictions` 参数来控制中继。限制的设置方式取决于您的 CA 证书：

**基于客户端证书的中继**
您可以构建一个客户端证书映射，允许这些证书通过 Postfix 中继邮件。如果您的客户端证书来自多个（官方）CA，这是一种安全的方法。

**基于认证机构的中继**
如果您运行自己的 CA 并完全控制证书，您可以选择允许所有拥有由您自己的 CA 签名的证书的邮件客户端进行中继。

这两个选项将在以下两个部分中描述。

### 基于客户端证书的中继

如果您的设置要求邮件客户端使用由一个或多个官方 CA 签名的证书进行中继，则需要执行以下步骤：

- 1. 创建客户端证书指纹列表。
- 2. 将列表转换为数据库。
- 3. 允许这些客户端中继。

您需要做的第一件事是从允许中继的邮件客户端收集公共证书。对于每个证书，您需要提取 MD5 指纹。

> **注意** *如果您不想手动执行此操作，请下载并运行 `add_ccerts_to_relay_clientcerts.sh`。此脚本计算 MD5 指纹，将其复制到 `/etc/postfix/relay_clientcerts`，并根据此文件的内容构建适当的映射。*

假设您有一个名为 `client_public_cert.pem` 的客户端证书。您可以使用以下命令提取 MD5 指纹：

```
# openssl x509 -noout -fingerprint -in client_public_cert.pem
```

输出应如下所示：

```
MD5 Fingerprint=00:8B:02:30:9D:18:F4:81:5D:2F:48:E4:5B:17:82:A7
```

指纹是十六进制数字和冒号的字符串。将指纹与客户端主机名一起添加到 `/etc/postfix/relay_clientcerts` 文件中，如下所示：

```
00:8B:02:30:9D:18:F4:81:5D:2F:48:E4:5B:17:82:A7 client_1.example.com
18:F4:81:5D:2F:82:A7:48:E4:5B:17:00:8B:02:30:9D client_2.example.org
...
```

尽管 Postfix 的 TLS 实现只需要指纹，但 `/etc/postfix/relay_clientcerts` 是一个典型的 Postfix 映射，因此每行需要两项。您可以选择任何想要的字符串作为右侧；在此示例中，它是客户端的完全限定域名。使用 FQDN 使得在映射中查找和识别指纹更容易。

> **提示** *您还可以在右侧添加客户端证书的过期日期，以加快或自动化查找过期证书的过程。*

添加指纹后，使用 `postmap` 将 `relay_clientcerts` 文件转换为 Postfix 映射：

```
# postmap hash:/etc/postfix/relay_clientcerts
```

此命令创建 `/etc/postfix/relay_clientcerts.db`，列表创建完成。



现在，您需要在 main.cf 中添加一个参数，告诉 Postfix 在哪里查找客户端映射：

```
relay_clientcerts = hash:/etc/postfix/relay_clientcerts
```

最后，通过向 smtpd_recipient_restrictions 添加 permit_tls_clientcerts 参数来扩展中继权限：

```
smtpd_recipient_restrictions =
 ...
  permit_tls_clientcerts
 ...
```

请确保 smtpd_recipient_restrictions 中各项的顺序很重要。请确保 permit_tls_clientcerts 出现在限制列表的靠前位置。配置基于证书的中继仅需完成这些操作。重新加载 Postfix 以使更改生效。

### 基于证书授权机构的中继

如果您只想基于有效证书进行中继，则必须完全控制客户端证书。您必须运行自己的证书授权机构 (CA) 并自行对客户端证书进行签名，而且您的 CA 必须是 Postfix 唯一认知的 CA。这在技术上是绝对必要的，因为在此功能下，Postfix 使用的唯一标准是证书验证是否成功。

> 如果您使用的是官方 CA 证书，甚至是官方 CA 证书列表，则互联网上的任何客户端都可能获得由这些证书授权机构之一签名的证书，因此将被允许中继——您的服务器将变成开放中继。

之前讨论的中继方法需要您构建并维护一份允许中继的客户端证书列表；这里的优势在于，您只需一个 CA 证书即可做出决定。

为了使 Postfix 为通过您私有 CA 签名的客户端进行中继，首先将 CA 列表缩小为一个，即您自己的公开 CA 证书。如前文所述，smtpd_tls_CAfile 参数控制 CA 文件，因此您的参数行在 main.cf 中将大致如下所示：

```
smtpd_tls_CAfile = /usr/share/ssl/certs/cacert.pem
```

在确认 Postfix 仅识别您自己的证书后，向 smtpd_recipient_restrictions 添加 permit_tls_all_clientcerts 参数：

```
smtpd_recipient_restrictions =
 ...
  permit_tls_all_clientcerts
 ...
```

最后，重新加载 Postfix 以使更改生效。

## 收紧 TLS 服务器

到目前为止，您已经了解了如何配置 Postfix 以提供和处理传输层安全性 (TLS)。本节展示了如何对客户不提交证书时强制执行并拒绝 TLS。

> **注意** 在使用以下功能时需谨慎，因为它们在不适当的环境中可能破坏您的邮件系统。

### 强制执行 TLS

您可以强制所有客户端使用 TLS。此功能在私有网络中非常有用，该网络需要确保所有消息流量均经过加密（例如，拥有分布式地点的大公司）。为此，请将 `main.cf` 文件中的 `smtpd_enforce_tls` 参数设置为 `yes`（默认为 `no`），然后重新加载 Postfix：

```
smtpd_enforce_tls = yes
```

> **注意** *RFC 2487 规定：“公开引用的 SMTP 服务器不得要求使用 STARTTLS 扩展以在本地交付邮件。此规则可防止 STARTTLS 扩展损害互联网 SMTP 基础设施的互操作性。”*
*在公共邮件服务器上要求每个客户端都使用 TLS 通常不是一个好主意，因为它会将无法使用 TLS 或未配置使用 TLS 的客户端拒之门外。如果在公共邮件服务器上要求 TLS，则预计有大量电子邮件无法传送到您的网络。*

### 要求客户端证书

您可以进一步执行 TLS 强制执行，仅允许提交证书的客户端。使用此选项时，如果客户端未发送证书，Postfix 将拒绝使用 TLS。要使该选项生效，请按照如下方式向 `main.cf` 添加 `smtpd_tls_req_ccert` 参数，并重新加载 Postfix：

```
smtpd_tls_req_ccert = yes
```

> **注意** *此设置本身并不能阻止客户端使用未加密的 SMTP 通信，除非您使用前面描述的 `smtpd_enforce_tls` 参数强制执行 TLS。如欲实施非常严格的策略，请使用这两个参数。*

## 客户端 TLS

客户端侧的 TLS 在 Postfix 作为邮件客户端运行并连接至支持 TLS 的邮件服务器时使用（见图 18-3）。根据配置，Postfix 可通过使用 TLS 发送明文 SMTP 认证凭据以获取中继权限，或通过出示自己的客户端证书以获准中继访问，从而（选择性）使用 TLS。

![图 18-3：Postfix 邮件客户端的 TLS](img/852c79f689feb77c7c5fde686b993808b1_331_0.png)

### 基本客户端配置

需要在 main.cf 中设置三个参数，以启用 Postfix 邮件客户端的基本 TLS 支持。您还可以调整一个额外参数以协助调试 TLS 会话。以下是您需要执行的步骤：

- 启用客户端 TLS。
- 配置 Postfix 以验证服务器证书。
- 将 Postfix 连接到随机源生成器。
- 记录客户端 TLS 活动。

#### 启用客户端 TLS

所有支持 TLS 的 Postfix 安装都具备客户端侧 TLS，但默认并未启用。在您向客户端 main.cf 添加以下参数设置之前，Postfix 不会在与任何服务器（即使服务器强制执行 TLS）使用 STARTTLS。

```
smtp_use_tls = yes
```

有了该参数，Postfix SMTP 守护进程将在连接另一端的邮件服务器提供 STARTTLS 时，在 SMTP 对话框中启动 STARTTLS。但是，启用客户端 TLS 不足以使整个流程生效。Postfix 客户端尚不知道在哪里查找用于验证服务器证书所需的 CA 证书。

#### 验证服务器证书

当 Postfix SMTP 客户端与邮件服务器启动 TLS 时，它尝试验证服务器在会话中展示的证书。Postfix 使用 CA 证书的公钥，检查 CA 添加在服务器证书上的密码签名。因此，您的 Postfix 安装必须拥有一个 CA 证书存储库，供其查找密码签名并进行比较。

**注意** 正如第 17 章所述，OpenSSL 没有用于 CA 证书的中央根存储。因此，您需要创建一个新的根存储。下面描述的配置使用了 ca-bundle.crt，该证书在“配置 Postfix 证书根存储”部分中进行了说明。您可能还希望在此部分创建自己的根存储文件。

像 Postfix 服务器一样，客户端可以使用两种不同类型的 CA 证书存储：包含所有 CA 证书的单文件，或包含多个文件的目录，每个文件包含一个 CA 证书。

对于 chrooted 邮件客户端，您应该将所有 CA 证书保存在单个文件中，因为 Postfix 会在 chroot 操作运行之前于启动时读取这些文件。

如果您不使用 chroot，则可以将 CA 证书保存在目录中，因为这样更容易维护。如果经常添加 CA 证书，这尤其有用，因为您不必在每次添加新 CA 证书时重新启动 Postfix。但是，对于 chrooted 设置，不要使用目录方法，因为您需要将证书保存在 chroot jail 中，这违背了 chroot 的初衷（将敏感信息从 jail 中隔离）。

**注意** 与 TLS 服务器配置一样，您可以同时使用这两种方法。请在下面的部分中设置这两个参数，并将一些 CA 证书与其他证书分开。当 Postfix 搜索 CA 证书时，它将首先读取文件，然后如果文件中未找到证书，则转向目录。

##### 将所有 CA 证书合并到单个文件中

最简单的方法（也是可能最行之有效的方法）是将所有 CA 证书存储在一个文件中。正如前面提到的，如果您偶然运行带有 mod_ssl 的 Apache，则您已经拥有这样一个文件，名为 ca-bundle.crt。请在命令行中执行 locate ca-bundle.crt 以查找该文件：

```
$ locate ca-bundle.crt
/usr/share/ssl/certs/ca-bundle.crt
```

现在，通过将 main.cf 中的 smtp_tls_CAfile 参数设置为 ca-bundle.crt 路径来告诉 Postfix 客户端使用该文件，然后重新加载 Postfix：

```
smtp_tls_CAfile = /usr/share/ssl/certs/ca-bundle.crt
```



#### 将所有 CA 证书存储在一个目录中

对于基于目录的 CA 证书访问方式，请将 `smtp_tls_CApath` 参数设置为包含证书文件的目录。对于新的 Postfix 安装，您可能需要做的第一件事是为证书文件创建一个目录：

```
# mkdir /etc/postfix/certs
```

现在，将您设置所需的所有 CA 证书放入此目录，并构建一个索引表以实现快速的证书查找。使用 OpenSSL 附带的程序 `c_rehash` 创建索引。运行此命令会构建索引并创建指向 CA 证书的符号链接：

```
# c_rehash /etc/postfix/certs/
Doing /etc/postfix/certs/
cacert.pem => e0dc2d06.0
WARNING: postfix_private_key.pem does not contain a certificate or CRL: skipping
postfix_public_cert.pem => 6df723a3.0
```

注意：每次添加新的 CA 证书后，都不要忘记运行 `c_rehash`。
完成这些步骤后，告诉 Postfix 使用此目录作为其 CA 根存储，然后重新加载您的配置：

```
smtp_tls_CApath = /etc/postfix/certs
```

注意：如果您运行自己的证书颁发机构，请使用类似以下的命令将您的 CA 证书添加到此根存储中：

```
# cat /usr/local/ssl/misc/demoCA/cacert.pem >> /usr/share/ssl/certs/ca-bundle.crt
```

如果您的 CA 证书是证书链中的一个链接，请添加从您的 CA 证书到证书链中根 CA 证书的所有 CA 证书。

#### 将 Postfix 客户端连接到随机源生成器

为了正确初始化加密，您需要将 Postfix 连接到随机数源。请参阅之前“将 Postfix 连接到随机源生成器”部分中关于 `tls_random_source` 参数的讨论。客户端和服务器的过程相同。

#### 记录客户端 TLS 活动

在启动 Postfix 测试您的 TLS 客户端之前，将 `smtp_tls_loglevel` 参数设置增加到 2，以便您可以看到重要的 TLS 事件（默认值为 0）：

```
smtp_tls_loglevel = 2
```

有关各种日志级别的含义，请参阅之前“提高 TLS 日志级别”部分中关于 `smtpd_tls_loglevel` 参数的讨论。

### 测试基本客户端功能

要测试基本的客户端 TLS，您只需执行两个步骤：

1.  检查日志文件，查看 Postfix 客户端是否检测到任何错误。
2.  向启用 TLS 的服务器发送邮件。

#### 检查日志文件中的错误

运行 `egrep` 命令，从 Postfix 日志文件中筛选出 TLS 问题：

```
$ egrep '(reject|error|warning|fatal|panic):' /var/log/maillog
```

如果存在任何 Postfix 可以检测到的 TLS 相关故障，此命令应该能捕获它们。不应该有任何指向 TLS 相关问题的错误，但如果存在问题，请检查您的配置，看看是否有输入错误，并确保 Postfix 对证书有读取权限。

#### 向 TLS 服务器发送邮件

现在尝试向启用 TLS 的邮件服务器发送消息，以查看 Postfix 客户端是否使用 TLS。

如果您不知道任何 TLS 服务器，TLS 补丁的开发者 Lutz Jänicke 有一个公共邮件服务器可供测试使用。向 `postfix_tls-bounce@serv01.aet.tu-cottbus.de` 发送一条消息，该服务器应将邮件发送回给您，包括添加到您原始邮件中的头部，该头部指示邮件是否通过 TLS 传输。头部应如下所示：

```
Received: from mail.state-of-mail.de (mail.state-of-mail.de [212.14.92.89])
	(using TLSv1 with cipher EDH-RSA-DES-CBC3-SHA (168/168 bits))
	(Client did not present a certificate)
	by serv01.aet.tu-cottbus.de (Postfix) with ESMTP id 74C6B2330
	for <postfix_tls-bounce@serv01.aet.tu-cottbus.de>; Wed, 10 Dec 2003
	23:50:45 +0100 (MET)
```

### 选择性 TLS 使用

通过选择性 TLS 客户端配置，您可以对某些服务器强制执行安全策略，同时，如果提供 STARTTLS 的邮件服务器配置不当，也能避免消息进入黑洞。

> **注意：**这种情况在 Lotus Notes 服务器上经常发生。

您将执行三个步骤：

1.  在您的 Postfix 配置中启用选择性 TLS。
2.  构建一个策略映射，告诉 smtp 客户端何时使用 TLS。
3.  配置 Postfix 以记录服务器何时提供 TLS。

#### 启用选择性 TLS

通过将 `smtp_tls_per_site` 参数设置为策略映射，在 `main.cf` 中启用客户端选择性 TLS。在此示例中，映射为 `/etc/postfix/tls_per_site`：

```
smtp_tls_per_site = hash:/etc/postfix/tls_per_site
```

#### 构建 TLS 策略映射

TLS 策略映射与其他任何 Postfix 映射具有相同的样式；每一行代表一个包含键值对的条目。将主机或域放在左侧（键），将 TLS 策略放在右侧（值）。Postfix SMTP 客户端的可能策略如下：

- **NONE**
  禁用客户端 TLS。

- **MAY**
  如果远程服务器提供 STARTTLS，则允许客户端尝试 TLS，但如果它不想尝试，也可以不尝试。

- **MUST**
  当此服务器通过 STARTTLS 提供 TLS 时，强制 Postfix 客户端使用 TLS。此外，Postfix 会检查服务器证书的 CommonName 参数与服务器的完全限定域名是否匹配。

- **MUST_NOPEERMATCH**
  是 MUST 策略的简化版本。Postfix 客户端响应 STARTTLS 并验证服务器的证书，但它忽略 CommonName 和 FQDN 之间的任何差异。

注意：如果您配置 Postfix 使用 TLS 策略映射，映射中的设置将始终覆盖您的 `main.cf` 设置。如果您关闭了 TLS，它将对在映射中找到的主机使用 TLS。反之，如果您在 `main.cf` 中开启了 TLS 且在策略映射中找不到该主机，它仍将使用 TLS。

创建一个名为 `/etc/postfix/tls_per_site` 的文件来启动映射，内容如下：

```
dom.ain                NONE
host.dom.ain           MAY
important.host         MUST
some.host.dom.ain      MUST_NOPEERMATCH
```

编写此 ASCII 映射后，使用 `postmap` 命令构建哈希映射，使其可供 Postfix 使用：

```
# postmap hash:/etc/postfix/tls_per_site
```

#### 识别 TLS 服务器

查找提供 TLS 的服务器不仅在调试 TLS 会话时有用，而且在您配置 Postfix 的选择性 TLS 功能时也很有用。在您的 `main.cf` 文件中将 `smtp_tls_note_starttls_offer` 参数设置为 `yes`：

```
smtp_tls_note_starttls_offer = yes
```

现在，只要您的 Postfix 客户端连接到提供 STARTTLS 的邮件服务器，客户端就会按如下方式将服务器名称记录到邮件日志中：

```
client postfix/smtp[1504]: Host offered STARTTLS: [mail.example.com]
```

通过这最后的配置设置，您的 TLS 客户端已准备就绪。

### 客户端性能调优

在“服务器性能调优”部分中描述的适用于 Postfix TLS 服务器的相同性能考量也适用于 TLS 客户端。客户端使用该部分中描述的相同 `tlsmgr` 守护进程来缓存客户端的会话密钥。但是，由于这是客户端，配置参数名称略有不同；将 `smtpd` 改为 `smtp`。

因此，要启用缓存，请按照“服务器性能调优”中描述的所有步骤操作，但在您的 `main.cf` 中使用 `smtp_tls_session_cache_database` 和 `smtp_tls_session_cache_timeout` 替换：

```
smtp_tls_session_cache_database = sdbm:/etc/postfix/smtp_scache
smtp_tls_session_cache_timeout = 3600s
```

#### 保护客户端 SMTP AUTH

在“保护 SMTP AUTH 握手的服务器端措施”部分，您了解了如何在服务器端使用 TLS 保护 SMTP AUTH 通信。本节向您展示如何在客户端执行此操作。简而言之，您不希望您的客户端通过未加密的连接使用 SMTP AUTH 明文机制发送您的用户名和密码。如果必须使用明文机制，客户端应首先启动 TLS 会话。

通过组合用于未加密连接的 `smtp_sasl_security_options` 参数和用于 TLS 会话的 `smtp_sasl_tls_security_options` 参数，您可以锁定 SMTP AUTH：

```
smtp_sasl_security_options = noanonymous, noplaintext
smtp_sasl_tls_security_options = noanonymous
```

第一条规则禁止在未加密的传输层上使用匿名和明文认证机制，第二条规则允许在与服务器使用 TLS 通信时使用明文机制。

### 基于客户端证书的中继

基于证书的中继是一种安全的方式，允许服务器为客户端中继消息，即使客户端不在服务器已知的网络上。您在“基于服务器端证书的中继”部分看到了服务器配置。然而，客户端配置不像服务器的中继功能；它更像是设置服务器本身，因为您必须提供客户端向内核出示的证书路径和客户端用于启动连接的密钥路径。

#### 配置 Postfix 客户端证书和密钥的路径

要使 Postfix 客户端在 TLS 会话开始时向服务器出示证书，您需要在 `main.cf` 中将 `smtp_tls_cert_file` 参数设置为客户端证书，并将 `smtp_tls_key_file` 参数设置为客户端密钥。示例如下：

```
smtp_tls_cert_file = /etc/postfix/certs/postfix_public_cert.pem
smtp_tls_key_file = /etc/postfix/certs/postfix_private_key.pem
```

注意：如果您也在 Postfix 安装中配置了服务器端 TLS，除非您希望您的 Postfix 服务器和客户端具有不同的“数字身份”，否则请重用服务器的证书和密钥。

现在，重新加载您的 Postfix 配置并开始测试。



##### 测试基于客户端证书的中继

测试涉及三个步骤：

1.  检查日志文件是否有明显错误。
2.  验证客户端是否发送了其证书。
3.  验证客户端能否基于其证书进行中继。

##### 检查日志文件

检查日志文件就是运行本章前面介绍过的 `egrep` 命令：

```
$ egrep '(reject|error|warning|fatal|panic):' /var/log/maillog
```

如果收到任何错误，常规建议适用：检查您的配置文件是否有拼写错误，并确保客户端对证书具有读取权限。

##### 验证客户端证书是否被发送

要获得客户端发送其证书的证明，您必须向一个启用了 TLS 的服务器发送邮件，并查看其是否接受客户端证书。如果您向一个设置了 `smtpd_tls_received_header = yes` 的 Postfix 邮件服务器发送客户端证书，则在您的邮件头中会出现类似以下内容的文本：

```
Received: from client.example.com (client.example.com [172.16.0.3])
    (using TLSv1 with cipher EDH-RSA-DES-CBC3-SHA (168/168 bits))
    (Client CN "client.example.com", Issuer "mail.example.com" (verified OK))
    by mail.example.com (Postfix) with ESMTP id 63AC77247
    for <tls-bounce@mail.example.com>; Thu, 11 Dec 2003 19:48:38 +0100 (CET)
```

第三行指出，邮件客户端 Client 向邮件服务器发送了证书。该证书由 `mail.example.com` CA 签名，并且服务器已成功验证。

> 注意：如果事情未按预期进行，且您不确定是客户端还是服务器导致了问题，请向 postfix_tls-bounce@serv01.aet.tu-cottbus.de 发送一条消息。如前所述，此服务会启用 TLS 调试将消息回送给您。

##### 验证客户端能否使用其证书进行中继

现在通过 TLS 服务器发送消息，测试您客户端的基于证书的中继功能。确保服务器根据以下标准使用您的证书中继消息。

1.  确保您的客户端不属于服务器的网络，或不属于服务器通过其他标准（如 `mynetworks`）授予中继访问权限的任何网络。
2.  确保您的客户端不使用任何功能，如 SMTP AUTH。
3.  确保收件人不在最终目的地的 `relayhosts` 列表中。

##### 加固客户端 TLS

您可以强制客户端使用 TLS，或者采取更严格的立场，仅在客户端能验证服务器对等名称时才与服务器通信。在客户端强制使用 TLS 通信仅在您可以控制客户端与之通信的服务器时才有用。

> 警告：错误配置这些功能可能会破坏您的出站邮件系统。

必须满足以下先决条件才能强制 TLS 通信：

1.  服务器必须提供 TLS。
2.  证书中的 `CommonName` 值必须与服务器的全限定域名匹配。
3.  客户端必须能够通过 CA 的签名验证服务器的证书。

如果这些条件中有一个不满足，客户端就不会将消息发送给服务器。相反，客户端会将消息保留在其队列中，并向邮件日志发送 4xx 错误通知。

> 注意：在专用网络中，或者当您知道客户端通过一台服务器中继所有消息时，强制 SMTP 客户端使用 TLS 是有用的。

要强制客户端 TLS，请在您的 `main.cf` 中设置 `smtp_enforce_tls` 参数，如下所示：

```
smtp_enforce_tls = yes
```

如果此模式对于日常使用来说过于严格，您可以允许在服务器证书中的 `CommonName` 与其全限定域名不匹配时进行传输。通过将 `smtp_tls_enforce_peername` 设置为 `no` 来实现此操作（当您设置 `smtp_enforce_tls` 时，此选项通常已启用）：

```
smtp_tls_enforce_peername = no
```

> 警告：此选项存在中间人攻击的风险。

# 19

## 公司邮件服务器

![img](img/852c79f689feb77c5fde686b993808b1_341_0.png)

本章将向您展示如何构建一个基于 Postfix、Cyrus SASL、Courier maildrop 和 Courier IMAP 的完整邮件系统。这些组件将从提供目录服务的 OpenLDAP 服务器获取配置和身份验证数据。

我们将从基本设置开始，过渡到高级设置。基本设置将把所有应用程序连接到中央 LDAP 服务器。一旦完成，我们将使系统更复杂。高级设置将在尽可能的地方添加传输层安全，并向您展示如何提供基于 LDAP 查询的 SMTP 身份验证。

在开始实施本章描述的公司邮件服务器之前，您应该对 LDAP 模式和 OpenLDAP 有深入的理解。如果您之前没有处理过 OpenLDAP，*OpenLDAP 管理员指南*，http://www.openldap.org/doc/admin22，是很好的入门读物。

# 概念概览

图 19-1 向您概述了本章将要处理的应用程序以及它们将如何相互连接。您可以看到 OpenLDAP 位于所有服务的中心。应用服务器的工作原理如下：

-   当邮件客户端尝试使用 SMTP AUTH 进行中继时，Postfix 将身份验证数据交给 LDAP 服务器。此外，当传入邮件到达时，Postfix 向 LDAP 服务器查询本地用户和别名信息。接受消息后，Postfix 将其交给 Courier maildrop。
-   Courier maildrop 负责本地投递。它向 LDAP 服务器询问邮箱位置，同时还会查找过滤规则（例如，将标记为垃圾邮件的消息放入名为 .spam 的子文件夹）。
-   用户连接到 Courier IMAP 服务器以获取邮件。此服务器向 LDAP 服务器查询用户的凭证。LDAP 还会告诉 Courier 在哪里可以找到邮箱，以及在访问时使用哪个 UID 和 GID。

![img](img/852c79f689feb77c5fde686b993808b1_342_0.png)

# LDAP 目录结构

构建邮件系统的第一步是设计您的 LDAP 目录树。这可能是一项艰巨的任务；LDAP 没有更广泛普及的原因之一是，从头开始设计目录令人望而生畏。在绘制结构、模式使用和属性时，需要考虑三个关键因素：

-   目录的目的
-   您的组织结构
-   使用 LDAP 目录的服务器的要求

本章中目录的主要目的是向您展示 Postfix 和其他服务器如何查询 LDAP 服务器。我们将保持结构尽可能简单，以便您可以专注于应用程序配置，而不是迷失在目录的泥潭中。

我们将在本章中为名为 Example Inc. 的组织构建邮件系统。该公司最初销售岩石，现已发展壮大，拥有多个部门。其中包括一个 IT 部门（由一位有些孩子气的管理员 Bamm Bamm 运营）、一个销售部门和一个采购部门。为简单起见，我们将只使用这三个部门。

目录服务将为 Postfix、Cyrus SASL、Courier maildrop 和 Courier IMAP 提供用户和配置数据。本示例将基于 Courier IMAP 附带的 authldap.schema，因为其他服务器可以毫无问题地使用它。

> 注意：如果您不想构建自己的目录，可以从 Postfix 手册网站 http://www.postfix-book.com 下载 Example Inc. 的 LDIF（LDAP 数据交换格式）转储。

图 19-2 显示了目录树，它从名为 dc=example,dc=com 的节点开始，扩展为两个主要分支。

左侧分支包含服务器的身份验证帐户；我们稍后将在“高级配置”部分查看这些内容，以保护 LDAP 数据和连接。

右侧分支称为 ou=people,dc=example,dc=com。它有子节点，例如 ou=it,ou=people,dc=example,dc=com，代表组织结构。当您进一步深入时，会遇到更多子节点，这些子节点保存着填充了属性和值的用户对象，这些属性和值包含为完整邮件系统提供所有用户相关数据所需的全部信息。

> 注意：您可以使用目录服务做更多事情。例如，您可以为 mydestination、relayhost、virtual_domain 等添加 Postfix 服务器配置值。



## 在 Postfix 架构中选择属性

如果你是 LDAP 新手，并期望一个简单的解决方案，那么很抱歉，我们有个坏消息。并没有一个现成的 Postfix LDAP 架构可以直接插入、填充数据然后运行。你可能更受打击地听说这是有意为之，但这是有充分理由的。Postfix 为此解决方案所需的几乎所有东西都存在于其他架构中，例如 OpenLDAP 中的 core.schema，或像 Courier IMAP 这样的应用程序，它自带了 authldap.schema。

要为你的服务器选择正确的架构和属性，你需要检查服务器的要求。例如，如果 Postfix 使用 LDAP 用于映射，你可以设置以下实体。

### 目标、网络和主机

目标、网络和主机由主机名和 IP 地址表示。Postfix 查找这些以确定它应该接受哪些域名的邮件并允许中继访问，它也可能在应用主机和网络限制时使用它们。

你的目录必须包含描述主机和网络的属性，并可能允许在单个 LDAP 对象中进行多值添加。你可以在网络相关的架构中找到合适的属性，例如 CORE 或 NIS 架构示例。

### 收件人和发件人

当 Postfix 查找收件人和发件人时，它默认查找 *username@hostname*。有许多可用的架构包含这样的属性。例如，你可以查看 core.schema 和其他邮件相关的架构，如 Sendmail 或 qmail 的架构。然而，不要忘记邮件系统的投递端。许多 POP 和 IMAP 服务器自带其自己的架构，都包含用于定义发件人和收件人地址的属性。

### 别名

用户可能有多个别名。你选择的属性必须允许向对象添加多个别名。大多数邮件相关的架构都有一个别名属性。你打算用于发件人和收件人地址的架构可能就适用。

### 列表

列表由单个别名条目和多个收件人地址组成。如果你的架构同时包含这两个属性，你就拥有了列表所需的一切。

在你着手编写自己的 Postfix 架构之前，你更应该将其他服务器的架构适配到 Postfix。这种方法减少了 LDAP 服务的负载和复杂性，并在扩展目录或使用它的服务器时为你提供了更大的灵活性。

如前所述，本章的示例主要基于 Courier IMAP 附带的 authldap.schema，因为它几乎包含了完整目录所需的所有内容。

### 分支设计

我们将目录分为两个主要分支（见图 19-2）。左分支将包含应用程序账户，我们稍后将在“高级配置”部分使用这些账户来实现对查询目录的应用程序的访问控制。

右分支将包含与用户相关的信息。它将根据部门结构分为更小的子单元。我们将使用 organizationalUnit 对象来创建这些子单元，稍后我们将配置 organizationalUnit 对象以保存简单邮件列表的信息。

有了分支，我们就可以转向创建实际的用户对象了。

## 构建用户对象

你可以从三个对象类构建用户对象：inetOrgPerson、CourierMailAlias 和 CourierMailAccount，你可以在 inetorgperson.schema、authldap.schema（Courier IMAP）和 nis.schema 中找到它们。使用 nis.schema 是必要的，因为 authldap.schema 依赖于它的一些属性。

使用来自所有三个架构的属性，我们将描述一个单独的用户对象。本章中我们使用的 IT 部门中 Bamm Bamm 的完整对象如下所示：

```
dn: uid=bammbamm,ou=it,ou=people,dc=example,dc=com
uid: bammbamm
givenName: Bamm
sn: Bamm
cn: Bamm Bamm
userPassword: bamm_secret
homeDirectory: /var/spool/mail/bammbamm
mailbox: /var/spool/mail/bammbamm/Maildir
quota: 51200000S
mail: bamm@example.com
maildrop: postmaster@example.com
maildrop: bamm.bamm@example.com
maildrop: abuse@example.com
objectClass: CourierMailAlias
objectClass: CourierMailAccount
objectClass: inetOrgPerson
uidNumber: 1003
gidNumber: 1003
```

你可能想知道所有这些属性从何而来。以下部分将解释它们的来源。

## 创建发件人和收件人

你需要创建一个对象来承载所有用户相关的属性和值。我们将使用 inetorgperson.schema，因为它提供了额外的属性，允许创建公司范围内的地址簿。

你可以使用 uid 属性创建一个唯一的用户对象。inetorgperson.schema 还提供了 mail 属性的访问权限，你可以将其用于本地收件人地址和有效的发件人地址。这两个属性在 inetorgperson.schema 中如下所示：

```
attributetype ( 0.9.2342.19200300.100.1.1
    NAME ( 'uid' 'userid' )
    DESC 'RFC1274: user identifier'
    EQUALITY caseIgnoreMatch
    SUBSTR caseIgnoreSubstringsMatch
    SYNTAX 1.3.6.1.4.1.1466.115.121.1.15{256} )
```

```
attributetype ( 0.9.2342.19200300.100.1.3
    NAME ( 'mail' 'rfc822Mailbox' )
    DESC 'RFC1274: RFC822 Mailbox'
    EQUALITY caseIgnoreIA5Match
    SUBSTR caseIgnoreIA5SubstringsMatch
    SYNTAX 1.3.6.1.4.1.1466.115.121.1.26{256} )
```

> **注意** _你可以多次将 mail 属性添加到一个对象。稍后你会看到这在创建邮件列表成员时很方便。_

假设我们想创建一个对象。在本章中，我们将使用用户名和姓氏的连接作为 uid 属性。

## 定义别名

你可以在 Courier IMAP 的 authldap.schema 中找到一个用于定义别名的好属性。那里有一个名为 CourierMailAlias 的辅助类，其中包含一个 maildrop 属性，该属性为邮件别名定义了一个 RFC 822 邮箱：

```
attributetype ( 1.3.6.1.4.1.10018.1.1.4 NAME 'maildrop'
    DESC 'RFC822 Mailbox - mail alias'
    EQUALITY caseIgnoreIA5Match
    SUBSTR caseIgnoreIA5SubstringsMatch
    SYNTAX 1.3.6.1.4.1.1466.115.121.1.26{256} )
```

> **注意** _CourierMailAlias 对象类是一个辅助类，这意味着你不能单独将其添加到目录中。你需要将其与一个结构类一起添加。这没问题，因为我们要使用的 inetOrgPerson 类是一个结构类。_

## 创建列表对象

Postfix 无需列表管理器（如 Mailman）支持的最简单的列表只是映射到收件人列表的别名。此时，我们已经拥有了所有需要的属性，所以我们只需要提出一个合适的列表对象——任何没有 userPassword 属性的对象都应该可以。

事实上，你不需要为列表创建额外的对象。只需将 CourierMailAlias 对象类添加到用于创建原始分支的 organizationalUnit 类中。

CourierMailAlias 对象为我们提供了对 maildrop 和 mail 属性的访问。现在你可以将一个别名名称（例如 all@example.com）分配给 ou=people,dc=example,dc=com 的 maildrop 属性，并为组织中的每个成员添加 mail 条目。一个完整的列表对象可能如下所示：

```
dn: ou=people,dc=example,dc=com
ou: people
description: All employees
objectClass: CourierMailAlias
objectClass: organizationalUnit
```

- maildrop: all@example.com
- mail: bamm@example.com
- mail: pebble@example.com
- mail: mcbricker@example.com
- mail: flintstone@example.com
- mail: rubble@example.com

此时，LDAP 服务器拥有了 Postfix 所需的收件人和别名，因此你可以将注意力转向其他服务器。

## 为剩余服务器添加属性

当 Postfix 完成处理电子邮件后，它会将其发送到本地投递代理（LDA），例如 Courier maildrop。LDA 需要知道邮箱的位置以及它应该使用的用户和权限。像 Courier IMAP 这样的邮件传输代理也需要知道邮箱的位置。

我们将使用 Courier 的 authldap.schema 中的 mailbox 属性来指定邮箱位置：

```
attributetype ( 1.3.6.1.4.1.10018.1.1.1 NAME 'mailbox'
  DESC 'The absolute path to the mailbox for a mail account in a non-default location'
    EQUALITY caseExactIA5Match
    SYNTAX 1.3.6.1.4.1.1466.115.121.1.26 SINGLE-VALUE )
```

此架构还定义了一个 quota 属性，可用于定义邮箱的最大大小：

```
attributetype ( 1.3.6.1.4.1.10018.1.1.2 NAME 'quota'
  DESC 'A string that represents the quota on a mailbox'
    EQUALITY caseExactIA5Match
    SYNTAX 1.3.6.1.4.1.1466.115.121.1.26 SINGLE-VALUE )
```

然而，authldap.schema 引用了 nis.schema 中 Courier 访问邮箱时所需的以下属性：

```
attributetype ( 1.3.6.1.1.1.1.0 NAME 'uidNumber'
  DESC 'An integer uniquely identifying a user in an administrative domain'
  EQUALITY integerMatch
  SYNTAX 1.3.6.1.4.1.1466.115.121.1.27 SINGLE-VALUE )
attributetype ( 1.3.6.1.1.1.1.1 NAME 'gidNumber'
  DESC 'An integer uniquely identifying a group in an administrative domain'
  EQUALITY integerMatch
  SYNTAX 1.3.6.1.4.1.1466.115.121.1.27 SINGLE-VALUE )
attributetype ( 1.3.6.1.1.1.1.3 NAME 'homeDirectory'
  DESC 'The absolute path to the home directory'
  EQUALITY caseExactIA5Match
  SYNTAX 1.3.6.1.4.1.1466.115.121.1.26 SINGLE-VALUE )
```



`uidNumber` 和 `gidNumber` 属性分别包含邮箱用户ID和组ID的编号。Courier maildrop 需要这些属性来获取写入邮箱消息时的正确权限，而 Courier IMAP 在读取和删除消息时也需要它们。此外，Courier maildrop 需要 `homeDirectory` 属性来读取过滤规则。

## 基本配置

本节向你展示如何将 LDAP 支持集成到 Postfix 和其他服务器中。我们在此只探讨基本功能。本章后面的“高级配置”部分将说明如何保护你的数据安全。

### 配置 Cyrus SASL

公司邮件服务器安装的软件中，一个有些奇特的情况是：Cyrus SASL 的 ldapdb 插件需要 OpenLDAP 开发库。然而，要能与 Cyrus SASL 通信，OpenLDAP 又需要 Cyrus SASL 开发库。如果你想从源代码构建两者，这种相互依赖关系可能会很棘手。

> **注意** ldapdb 插件需要 OpenLDAP 版本高于 2.1.27 或高于 2.2.6。如果你已经安装了支持 SASL 的合适 OpenLDAP，那么在构建 SASL 时启用 ldapdb 支持，你可能只需要安装 OpenLDAP 开发库。

要解决这个问题，你必须构建并安装 Cyrus SASL 两次。第一次，你将在不启用 ldapdb 的情况下进行构建，以便 OpenLDAP 可以链接 SASL 库。本章后面，你需要用新安装的 OpenLDAP 库重新构建 Cyrus SASL，以获得 ldapdb 插件。如果你的服务器上其他应用不需要 Cyrus SASL，你可以使用以下配置命令来获取构建 OpenLDAP 所需的最小 SASL：

```
# ./configure \
    --with-plugindir=/usr/lib/sasl2 \
    --disable-java \
    --disable-krb4 \
    --with-dblib=berkeley \
    --with-saslauthd=/var/state/saslauthd \
    --without-pwcheck \
    --with-devrandom=/dev/urandom \
    --enable-cram \
    --enable-digest \
    --enable-plain \
    --enable-login \
    --disable-otp
```

现在，你可以将注意力转向构建 OpenLDAP。

### 配置 OpenLDAP

如果你的系统上没有 OpenLDAP，请获取一个比 2.1.27 或 2.2.6 更新的版本（此版本使用不同的 BerkeleyDB），可以从软件包获取，或者从 http://www.openldap.org/software/download 下载源代码。如果你是从源代码构建，请阅读下面的“从源代码安装 OpenLDAP”部分。

#### 从源代码安装 OpenLDAP

以普通用户身份，解压归档文件并进入新创建的目录。运行 `configure` 时，至少需要包含以下选项：

```
$ ./configure  --prefix=/usr --exec-prefix=/usr --bindir=/usr/bin \
    --sbindir=/usr/sbin --sysconfdir=/etc --datadir=/usr/share \
    --includedir=/usr/include --libdir=/usr/lib --libexecdir=/usr/libexec \
    --localstatedir=/var --sharedstatedir=/usr/com --mandir=/usr/share/man \
    --infodir=/usr/share/info --with-slapd --with-slurpd --without-ldapd \
    --with-threads=posix --enable-static --enable-dynamic --enable-local \
    --enable-cldap --enable-rlookups --with-tls --with-cyrus-sasl \
    --enable-wrappers --enable-passwd --enable-cleartext --enable-crypt \
    --enable-spasswd --enable-modules --disable-sql --libexecdir=/usr/sbin \
    --localstatedir=/var/run --enable-ldbm --with-ldbm-api=berkeley \
    --enable-bdb --enable-ldap --enable-meta --enable-monitor \
    --enable-null --enable-rewrite --disable-shared --with-kerberos=k5only
```

配置脚本运行完成后，依次执行 `make depend`、`make` 和 `make test`，然后切换到 root 用户，执行 `make install`。现在，你已准备好配置 OpenLDAP。

#### 配置 LDAP 服务器

要配置 OpenLDAP 服务器 slapd，请切换到配置目录（例如 `/etc/openldap`）并编辑 `slapd.conf` 文件。你需要添加以下配置：

```
# SCHEMATA
include         /etc/openldap/schema/core.schema
include         /etc/openldap/schema/cosine.schema
include         /etc/openldap/schema/inetorgperson.schema
include         /etc/openldap/schema/misc.schema
include         /etc/openldap/schema/nis.schema
include         /etc/openldap/schema/authldap.schema
# RUNTIME
pidfile         /usr/var/slapd.pid
argsfile        /usr/var/slapd.args
# DATABASE DEFINITIONS
database        ldbm
suffix          "dc=example,dc=com"
rootdn          "cn=Manager,dc=example,dc=com"
rootpw          {CRYPT}SHXa4LHVH8y3A
directory       /usr/var/openldap-data
# INDICES
index objectClass eq
index cn eq
index mail,maildrop pres
index mailbox,quota,uidNumber,gidNumber eq
```

`slapd.conf` 的 SCHEMATA 部分指定了启动时要加载的模式。DATABASE DEFINITIONS 部分将 "dc=example,dc=com" 设置为定义目录树顶层分支的后缀。它指定了一个 `rootdn` 属性值集（"cn=Manager,dc=example,dc=com"）和一个 `rootpw` 值，为由 `rootdn` 定义的用户提供对目录的读写访问权限。使用 `slappasswd(8)` 命令来创建加密密码。INDICES 部分定义了应该建立索引的属性。当你为某个属性建立索引后，查找速度会快得多。

#### 控制 OpenLDAP 中的 SASL 认证

因为 OpenLDAP 具有 SASL 支持，所以在认证时可能会使用 SASL 将用户绑定到服务器。虽然它不会使用明文机制来处理认证，但在剩余机制中可能会提供 GSSAPI。由于我们不会为了使用这个机制而配置一个完整的 Kerberos 服务器，所以最好现在就禁用它，以免客户端尝试使用。为此，只需在 OpenLDAP 的一个特殊 SASL 配置文件中列出你想要的机制。创建一个 `/usr/lib/sasl2/slapd.conf` 文件，包含以下设置：

```
mech_list: DIGEST-MD5
```

有关 SMTP 认证的更多信息，请参阅第 15 章。

#### 导入目录

现在是时候用数据填充 LDAP 数据库了。有多种方法可以实现，但在我们的场景中，slapd 可能还未运行。这意味着你可以使用 `slapadd` 工具对 LDIF 文件执行操作，如下所示：

```
# slapadd -v -b "dc=example,dc=com" -l example.com.ldif
```

> **警告** 请勿在 slapd 运行时执行 slapadd。该工具直接写入数据库，可能导致 slapd 崩溃并损坏你的数据库。

成功导入 LDIF 文件后，启动 slapd。如果导入过程中遇到问题，请阅读 `slapadd(8)` 文档，看看是否需要其他参数（或者，如果问题真的很严重，启用调试）。

#### 配置 LDAP 客户端

要测试你的 slapd 配置并使其与 Courier IMAP 协同工作，你需要配置 OpenLDAP 客户端。通常，你需要在 `/etc/openldap/ldap.conf` 文件中调整一些设置。对于基础配置，启用以下参数：

```
URI ldap://mail.example.com
BASE dc=example,dc=com
```

`URI` 和 `BASE` 参数指定了要访问的 LDAP 服务器以及在目录树中开始查询的位置。一旦正确设置了这些参数，你就可以测试目录了。

### 测试 LDAP

测试 LDAP 服务器最简单的方法是使用 OpenLDAP 自带的客户端工具。从命令行运行 **ldapsearch**，将 LDAP 客户端连接到服务器并对目录进行查询。以下是一个成功的示例：

```
# ldapsearch -x -LLL -b "uid=bammbamm,ou=it,ou=people,dc=example,dc=com" "(objectclass=*)"
dn: uid=bammbamm,ou=it,ou=people,dc=example,dc=com
uid: bammbamm
givenName: Bamm
sn: Bamm
cn: Bamm Bamm
homeDirectory: /var/spool/mail/bammbamm
maildrop: postmaster@example.com
maildrop: bamm.bamm@example.com
maildrop: abuse@example.com
objectClass: CourierMailAlias
objectClass: CourierMailAccount
objectClass: inetOrgPerson
mailbox: /var/spool/mail/bammbamm/Maildir
quota: 5120000S
userPassword:: YmFtbV9zZWNyZXQ=
uidNumber: 1003
gidNumber: 1003
mail: bamm@example.com
```

如果你看到此输出，说明你可以访问目录，并且数据已按预期存储。如果没有输出，请按照 `slapd.conf(5)` 中的描述配置 `loglevel` 参数，并查看更详细的调试信息能告诉你什么。



### 配置 Postfix 和 LDAP

要检查您的 Postfix 是否已启用 LDAP 和 SASL 支持，请尝试此命令：

```
$ ldd /usr/sbin/postconf -h daemon_directory/smtpd
linux-gate.so.1 =>  (0x00bad000)
libldap.so.2 => /usr/lib/libldap.so.2 (0x00882000)
liblber.so.2 => /usr/lib/liblber.so.2 (0x00646000)
libsasl2.so.2 => /usr/lib/libsasl2.so.2 (0x0098a000)
libdb-4.2.so => /lib/tls/libdb-4.2.so (0x00a73000)
libnsl.so.1 => /lib/libnsl.so.1 (0x00835000)
libresolv.so.2 => /lib/libresolv.so.2 (0x00655000)
libc.so.6 => /lib/tls/libc.so.6 (0x004e6000)
libdl.so.2 => /lib/libdl.so.2 (0x00603000)
libssl.so.4 => /lib/libssl.so.4 (0x0084c000)
libcrypto.so.4 => /lib/libcrypto.so.4 (0x04377000)
libpthread.so.0 => /lib/tls/libpthread.so.0 (0x0061c000)
/lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x004cd000)
libgssapi_krb5.so.2 => /usr/lib/libgssapi_krb5.so.2 (0x00d09000)
libkrb5.so.3 => /usr/lib/libkrb5.so.3 (0x006da000)
libcom_err.so.2 => /lib/libcom_err.so.2 (0x058fd000)
libk5crypto.so.3 => /usr/lib/libk5crypto.so.3 (0x05902000)
libz.so.1 => /usr/lib/libz.so.1 (0x00609000)
```

包含 ldap 和 sasl2 库的行表明 LDAP 和 SASL 支持已被编译进 Postfix。您已在第 15 章学习了如何配置 SASL 支持。现在您需要在 SASL 之外再获得 LDAP 支持。您可以通过以合理的方式组合构建过程中使用的环境变量 CCARGS 和 AUXLIBS 来获得此支持。首先，回顾一下您是这样构建 SASL 支持的：

```
$ CCARGS="-DUSE_SASL_AUTH -I/usr/local/include AUXLIBS="-L/usr/local/lib -lsasl2" make makefiles
```

要构建支持 LDAP 的 Cyrus SASL 库，您需要在系统上找到 LDAP 库和头文件。如果您不知道它们的位置，可以像这样搜索库：

```
# find /usr -name 'libldap*.*'
/usr/local/lib/libldap.so.2
/usr/local/lib/libldap.so.2.0.122
/usr/local/lib/libldap_r.so.2
/usr/local/lib/libldap_r.so.2.0.122
/usr/local/lib/libldap.so
/usr/local/lib/libldap.a
/usr/local/lib/libldap_r.so
/usr/local/lib/libldap_r.a
# find /usr -name 'liblber*.*'
/usr/local/lib/liblber.so.2.0.122
/usr/local/lib/liblber.so.2
/usr/local/lib/liblber.so
/usr/local/lib/liblber.a
```

此输出显示 LDAP 库位于 `/usr/local/lib`；编译器、预处理器和链接器会自动搜索 `/usr/lib` 和 `/usr/include` 路径。记下此位置，然后使用以下命令搜索对应的 include 文件：

```
# find /usr -name '*ldap*.h'
/usr/local/include/ldap.h
/usr/local/include/ldap_cdefs.h
/usr/local/include/ldap_schema.h
/usr/local/include/ldap_utf8.h
/usr/local/include/ldap_features.h
```

> **注意** *如果您在系统上找不到 LDAP 的 include 文件，但库确实存在，您可能需要从操作系统安装 LDAP 开发包。您需要查找名称以 -dev 或 -devel 结尾的包。*

现在您知道了在哪里寻找 LDAP 和 SASL 支持，请以普通用户身份解压 Postfix 源代码，并进入 Postfix 源代码目录。使用同时包含 SASL (`-DUSE_SASL_AUTH`) 和 LDAP (`-DHAS_LDAP`) 的选项配置并构建 Postfix，如下所示：

```
$ CCARGS="-DHAS_LDAP -DUSE_SASL_AUTH -I/usr/local/include" AUXLIBS="-lldap -llber -L/usr/local/lib -lsasl2"
$ make makefiles
$ make
```

构建完成后，切换为超级用户（root）并根据需要运行 `make install` 或 `make upgrade`。最后，按照本章开头所述验证您是否拥有 SASL 和 LDAP 支持。

## LDAP 查询

Postfix 邮件列表中关于 LDAP 的问题不多，特别是与询问数据库后端的问题数量相比。许多人认为使用 LDAP 运行 Postfix（或任何其他程序）类似于巫术，并试图不惜一切代价避免它。然而，事实并非如此。LDAP 查询的配置步骤始终如下：

1.  为 LDAP 配置文件创建一个目录。
2.  为 LDAP 创建一个 Postfix 配置文件。
3.  测试一个 LDAP 查询。
4.  配置 Postfix 以使用 LDAP 查询配置。

您将在下面的小节中对这些步骤进行两次迭代。首先，您将配置一个用于本地收件人的查询，然后作为第二步，配置一个用于邮件别名的查询。

### 创建 LDAP 配置目录

一个配置良好的 LDAP 服务器会出于安全原因拒绝查询目录数据。它要求想要检索此类数据的用户首先对 LDAP 服务器进行身份验证（“绑定”）。您将在本章后面的“高级配置”部分学习如何为 Postfix 创建绑定用户，但您现在需要迈出第一步，创建额外的配置目录。这是因为 Postfix 绑定凭据必须存储在 Postfix 特定的配置文件中，但您不想将它们放入 `main.cf` 文件中，因为这将使它们可被所有用户读取。

> **警告** *在外部文件中创建 LDAP 配置需要 Postfix 2.x。您可以在 `main.cf` 中完全配置 LDAP 查询参数，但由于这要求将 LDAP 用户的密码放在 `main.cf` 中，因此不太安全——Postfix 运行所在的 Unix 系统上的任何用户都可以读取它们。*

*如果您确实想使用 `main.cf` 文件存储凭据，请阅读 `ldap_table(5)` 手册页中的“向后兼容性”部分。*

要创建配置目录，请创建一个仅 root 和 postfix 可访问的 `/etc/postfix/ldap` 目录。您将在那里存储所有 LDAP map 配置文件，并在 `main.cf` 中引用它们。

```
# mkdir /etc/postfix/ldap
# chgrp postfix /etc/postfix/ldap
# chmod 750 /etc/postfix/ldap
```

### 为本地收件人添加 LDAP 查询

现在让我们看看用于查询 LDAP 服务器的基本 Postfix 参数。我们将首先禁用 LDAP 绑定操作。然后我们将创建一组参数，这些参数将为我们提供用于验证本地收件人的信息。

#### 禁用 LDAP 绑定

默认情况下，Postfix 在运行查询之前尝试通过 LDAP 绑定对服务器进行身份验证。当您刚开始时，最好禁用此身份验证，以使事情尽可能简单。创建一个名为 `/etc/postfix/ldap/local_recipients.cf` 的 LDAP 查询配置文件，并包含以下配置参数，该参数将关闭绑定：

```
bind = no
```

#### 配置 LDAP 主机

您可以使用 `server_host` 和 `server_port` 配置参数告诉 Postfix 在哪里找到目录服务。`server_host` 参数定义了一个或多个 LDAP 服务器 URL 中的连接类型（`ldap://`、`ldaps://` 或 `ldapi://`），这些 URL 可能包含服务器端口。此参数默认为 `server_host = ldap://localhost:389`。

您可以选择设置 `server_port`（默认端口为 389）来定义 LDAP 服务器端口，但这仅在所有 LDAP 服务器都监听同一端口时才有意义。否则，您可以按 URL 附加端口，如下所示：

```
server_host = ldap://mail.example.com:389, ldaps://auth.example.com:636
```

在本章中，LDAP 服务器运行在与其他服务器相同的主机上，并监听默认 LDAP 端口（389）。在这种情况下，您可以这样设置 `server_host`：

```
server_host = ldap://mail.example.com
```

#### 指定基础节点

接下来要做的事情是使用 `search_base` 参数设置 Postfix 搜索的起始分支。没有默认值，因此您必须始终设置它。添加用户对象分支的 `dn` 部分，如下所示：

```
search_base = ou=people,dc=example,dc=com
```

#### 定义 LDAP 结果属性

要完成 LDAP map 配置，您需要定义存储 Postfix 在查找时访问的键的属性。逻辑与您之前看到的任何其他 map 完全相同。与索引 map 相比，键和值的参数名称如表 19-1 所示。

##### 表 19-1：索引 map 的字段如何对应 LDAP 查询参数

| Map 类型 | LHS | RHS | 条件 |
|---|---|---|---|
| 索引 map | key | value | - |
| LDAP 查询 | query_filter | result_attribute, result_filter | special_result_attribute |

如您所见，您使用 `query_filter` 参数定义查询键属性。按照 Example Inc. 目录的示例，指定用于本地收件人邮件地址的属性（`mail` 属性），并定义 Postfix 应提交给 LDAP 服务器的完整邮件地址部分。替换内容如下。



%s 完整的邮件地址（例如，bamm@example.com）
- %u 不带`@`和域名的本地部分（例如，bamm）
- %d 不带本地部分和`@`的域名部分（例如，example.com）

因为本章中的目录条目仅包含完整的邮件地址，例如 bamm@example.com，我们将使用 `%s`。按照以下方式配置 Postfix，以便基于完整域名进行查询：

```
query_filter = (mail=%s)
```

> **注意** *LDAP 查询和结果的标准语法在 RFC 2254 (http://www.rfc-editor.org/rfc/rfc2254.txt) 中定义。你可以按任何你喜欢的方式指定查询。例如，如果你的模式中有一个名为 `mailboxActive` 的属性，表示一个活跃（未禁用）的邮箱，你可以如下形式构建查询参数：*

```
query_filter = (&(mail=%s)(mailboxActive=1))
```

现在你需要定义 Postfix 将用于查询结果的属性。你有两个可用参数：`result_attribute` 用于配置实际的属性，以及 `result_filter` 用于过滤掉你可能不需要的 LDAP 查询结果的部分。

在本章中，你只需要验证本地邮件地址的存在性，因为本章中的投递代理是 Courier maildrop，而不是 Postfix。Postfix 只需要知道本地收件人地址是否有效，因此你可以使用任何返回的属性。

> **注意** *这意味着 Postfix 接受 LDAP 服务器返回的任何值，作为传入消息存在本地收件人的证明。如果 LDAP 服务器没有返回任何值，Postfix 将拒绝该消息。*

选择一个在测试查询时易于识别的简单属性。在我们的案例中，`uid` 符合要求，因此以下是如何在 Postfix 的 `local_recipients.cf` 配置文件中将其配置为结果属性：

```
result_attribute = uid
```

#### 激活查询映射

当你对 `/etc/postfix/ldap/local_recipients.cf` 文件感到满意时，你需要在主 Postfix 配置中激活此映射。在你的 `main.cf` 文件中，将 `local_recipient_maps` 参数设置为一个映射列表，Postfix 在查找本地收件人时将咨询这些映射。使用 `proxymap`（在第 5 章中描述）来提高 LDAP 查询性能，如下所示：

```
local_recipient_maps = proxy:ldap:/etc/postfix/ldap/local_recipients.cf
```

每个 proxymap 进程代表多个客户端进行查询，可以（但不必）缓存查找结果。映射设置好后，重新加载你的 Postfix 配置并开始测试。

### 测试 LDAP 收件人

此时，你能执行的唯一测试是检查 Postfix 是否能查找有效的本地收件人。你将无法发送测试消息，因为本地投递尚未配置。使用 `postmap` 命令查询 LDAP 服务器，查找已知的本地收件人，例如 `bamm@example.com`。但是，在执行此操作之前，你需要切换到系统上的 `postfix` 用户，因为你必须确保此用户有权读取 LDAP 配置文件并运行查询。成功的测试如下所示：

```
# su - postfix
$ /usr/sbin/postmap -q "bamm@example.com" ldap:/etc/postfix/ldap/local_recipients.cf
bammbamm
```

这里的查询返回了 `bamm@example.com` 的 `uid` 值；在本例中，该属性的值是 `bammbamm`，因此配置有效。如果无效，请在 `postmap` 命令中添加 `-v` 参数以获取详细输出。此外，你可以在 LDAP 查询配置文件中添加 `debuglevel` 参数：

```
debuglevel = 1
```

> 你可以将调试级别增加到 3，这应该能为你提供修复问题所需的所有信息。

### 查询 LDAP 邮件别名

要配置 Postfix 查询 LDAP 服务器以获取邮件别名，你将遵循前面“为本地收件人添加 LDAP 查询”一节中所示的相同基本配置步骤，只是这次你必须为查询结果指定不同的 `result_attribute` 参数，并且必须使用 `query_filter` 参数从结果中提取特定属性。示例目录服务器中的别名名称被分配给条目的 `maildrop` 属性。因此，别名的配置文件（例如 `/etc/postfix/ldap/virtual_aliases.cf`）应如下所示。

```
bind = no
server_host = ldap://mail.example.com
search_base = ou=people,dc=example,dc=com
query_filter = (maildrop=%s)
result_attribute = mail
```

#### 配置 Postfix 的 LDAP 别名查询映射

有了 LDAP 别名查询配置文件后，你需要通过在 `main.cf` 中设置 `virtual_alias_maps` 参数，将其连接到你的 Postfix 配置。语法与前面“激活查询映射”一节中描述的收件人映射相同：

```
virtual_alias_maps = proxy:ldap:/etc/postfix/ldap/virtual_aliases.cf
```

重新加载你的配置并开始测试。

#### 测试 LDAP 别名查询映射

与之前一样，你无法发送消息来测试 LDAP 查询配置，但你可以使用 `postmap` 命令。回想一下，在目录中 `postmaster@example.com` 是 `bamm@example.com` 的别名。切换到 `postfix` 用户，看看别名映射是否像这样工作：

```
# su - postfix
$ /usr/sbin/postmap -q "postmaster@example.com" ldap:/etc/postfix/ldap/virtual_aliases.cf
bamm@example.com
```

如果此命令没有任何输出，请在 `postmap` 命令中添加 `-v` 参数以获取详细输出。你也可以在 LDAP 查询配置文件中添加 `debuglevel` 参数（并且可以根据你需要的信息量将调试级别增加到 3）：

```
debuglevel = 1
```

### 测试列表

你可能还记得，本章前面“创建列表对象”一节中描述的简单列表设计使用了别名。因此，你应该能够通过对列表名称运行 `postmap` 查询来检索别名的多个收件人：

```
# su - postfix
$ /usr/sbin/postmap -q "all@example.com" ldap:/etc/postfix/ldap/virtual_aliases.cf
bamm@example.com,pebble@example.com,mcbricker@example.com,flintstone@example.com,rubble@example.com
```

当 LDAP 服务器返回多个结果时，Postfix 会收集所有结果并将它们转换为逗号分隔的列表，如上例所示。

## 将传输委托给 Courier maildrop

本章中的配置不使用任何 Postfix 投递代理（`local`、`maildrop` 和 `virtual` 守护进程）。原因之一是第三方投递代理提供了过滤规则和配额等功能。例如，用户 `bambbamm` 可以将 `postmaster@example.com` 的所有消息放入子文件夹。本节将向你展示如何配置 Postfix，将本地消息投递任务委托给 Courier maildrop。

### 创建本地传输

首先在你的 `master.cf` 文件中定义一个新的传输服务。不用担心会破坏你当前的 LDA（如果你甚至有一个可用的），因为直到你在 `main.cf` 文件中进行相应的更改，Postfix 才会使用新服务。新的传输将是一个名为 `maildrop` 的管道传输。将以下配置行添加到你的 `master.cf` 文件：

```
maildrop    unix  -       n       n       -       -       pipe
  flags=DRhu user=vmail argv=/usr/local/bin/maildrop -d ${recipient} -w 75
```

此 `pipe(8)` 传输的标志作用如下：

- **D**：在信封收件人地址前添加 Delivered-To 收件人消息头。这模仿了 Postfix `local` 守护进程，作为防止邮件循环的预防措施。
- **R**：在信封发件人地址前添加 Return-Path 消息头。RFC 2821 要求 Postfix `local` 守护进程执行此操作。
- **h**：将命令行 `$recipient` 地址的域名和 `$nexthop` 主机名转换为小写。
- **u**：将命令行 `$recipient` 地址的本地部分转换为小写。
- **user**：`user=vmail` 指定 `/usr/local/bin/maildrop -d ${recipient}` 应以 `vmail` 用户身份运行，这个用户你将在稍后设置 Courier maildrop 时看到。
- **-w**：将 `deliverquota(8)` 的警告级别设置为邮件目录配额的 75%。如果你不想强制执行配额，请省略此项。

添加服务后，编辑你的 `main.cf` 文件，告诉 Postfix 将其用作本地传输：

```
local_transport = maildrop
```

> **注意**：使用 `maildrop` 而不是本地投递代理有两个副作用。首先 `local` 会查看别名映射，但 Courier maildrop 无法做到这一点。然而，你已经在前面的“配置 Postfix 的 LDAP 别名查询映射”一节中解决了这个问题。



### 限制并发消息

在测试新的传输机制之前，你需要确保其被配置为一次只投递给一个用户。无需担心这会带来性能损失，因为对于大多数邮件服务器而言这是正常的。即使是 Postfix 的本地传输，也通过 `local_destination_recipient_limit` 参数限制为一次处理一条消息。

为其他 LDA 创建限制的参数语法为 `servicename_destination_recipient_limit`，其中 `servicename` 等于 `master.cf` 中的第一个字段。为你刚刚定义的 Courier maildrop 服务在 `main.cf` 中添加以下行：

```
maildrop_destination_recipient_limit = 1
```

现在重新加载 Postfix 并开始测试。

### 测试 LDA

要测试 LDA，只需向你的收件人映射中的某个地址发送一条消息，并观察邮件日志。你应该能看到 Postfix 使用了新的 maildrop 传输，如下所示：

```
# echo foo | /usr/sbin/sendmail -f "" postmaster@example.com
# tail -f /var/log/maillog
Jun 29 14:39:13 mail postfix/pickup[5122]: AC7B94400C: uid=0 from=<>
Jun 29 14:39:13 mail postfix/cleanup[5127]: AC7B94400C:
  message-id=<20040629123913.AC7B94400C@mail.example.com>
Jun 29 14:39:13 mail postfix/qmgr[5123]: AC7B94400C:
  from=<>, size=285, nrcpt=1 (queue active)
Jun 29 14:39:13 mail postfix/pipe[5130]: AC7B94400C:
  to=<bamm@example.com>, orig_to=<postmaster@example.com>,
  relay=maildrop, delay=0, status=sent (example.com)
Jun 29 14:39:13 mail postfix/qmgr[5123]: AC7B94400C: removed
```

如果你在日志中没有看到 maildrop 传输，请在 `master.cf` 中为 `smtpd` 开启详细日志记录，重新加载配置，然后再次发送消息。

#### 配置 Courier Maildrop

Courier maildrop 是一个 LDA，它从传输代理（如 Postfix）接收消息，并将其以 Maildir 格式存储在收件人的邮箱中。Maildrop 还可以对消息应用过滤器。另一个有趣的功能是强制执行目录配额（Maildir 格式的消息作为独立文件存储在目录中）。

#### 准备你的系统

Courier maildrop 禁止未授权用户写入邮箱。在构建二进制文件之前，你需要选择受信任的用户和组。创建至少一个新用户，其用户 ID 和组 ID 数字与你在 LDAP 目录中为 `uidNumber` 和 `gidNumber` 属性设置的值匹配。Courier maildrop 和 IMAP 在访问邮箱时会从目录中检索这些属性。

本章中的示例配置使用以下用户 ID 和组 ID：

```
uidNumber: 1003
gidNumber: 1003
```

如果你还没有这样做，请创建一个用户和组来匹配这些值。例如，以下命令在 Linux 系统上添加名为 `vmail` 的用户和组：

```
# useradd -u 1003 vmail
# groupadd -g 1003 vmail
```

#### 安装 Courier Maildrop

在编写本文时，Courier maildrop 的 LDAP 支持正处于测试阶段。正确配置时运行良好，但如果遇到错误，它不会告诉你出了什么问题。考虑到 Courier maildrop 的发展速度，当你读到本书时，这可能已经得到修复。要获得 LDAP 支持，请从 http://www.courier-mta.org/download.php#maildrop 下载 maildrop 的开发快照。

以普通用户身份解压归档文件，并切换到新创建的目录。Courier maildrop 使用 GNU Autoconf，因此构建选项指定如下：

```
$ ./configure --enable-restrict-trusted=1 --enable-trusted-users='root vmail' \
--enable-trusted-groups='root vmail' --enable-maildirquota --with-trashquota \
--enable-maildropldap
```

确保指定 `--enable-maildropldap` 以获取 LDAP 支持。如果你想获得配额支持，请包含 `--enable-maildirquota` 和 `--with-trashquota`，但请先查看“准备 Maildir 配额”一节。配置脚本运行完成后，执行 `make`。如果一切顺利，切换到 root 用户并运行 `make install-strip install-man` 以安装剥离符号的二进制文件和手册页。

现在你已经安装了 maildrop，你需要处理 Postfix 的 `pipe` 守护进程，它拒绝以 root 权限运行任何进程。为了解决这个问题，将 maildrop 二进制文件更改为 setuid root。

```
# chmod 750 /usr/local/bin/maildrop
# chmod u+s /usr/local/bin/maildrop
# chown root:vmail /usr/local/bin/maildrop
# ls -l /usr/local/bin/maildrop
-rwsr-x---  1 root vmail 165552 Jun 25 12:48 /usr/local/bin/maildrop
```

不用担心会绕过正常的 Postfix 安全策略。`pipe` 守护进程运行 maildrop，后者立即以 root 身份开始运行，但在从 LDAP 获得正确的用户 ID 和组 ID 后，maildrop 会切换到该用户和组。

#### 配置 Courier Maildrop

为 LDAP 设置 maildrop 配置最简单的方法是将示例文件 `maildropldap.config` 从 maildrop 源目录复制到 `/etc/maildropldap.config`（这是 Courier maildrop 默认查找 LDAP 配置文件的位置）。编辑该文件以匹配你的配置。

以下是本章示例的配置：

| 键 | 值 |
|---|---|
| hostname | mail.example.com |
| basedn | dc=example,dc=com |
| filter | &(objectclass=inetorgperson) |
| timeout | 5 |
| search_method | mail |
| mail_attr | mail |
| uid_attr | uid |
| uidnumber_attr | uidNumber |
| gidnumber_attr | gidNumber |
| maildir_attr | mailbox |
| homedirectory_attr | homeDirectory |
| quota_attr | quota |

##### 创建 Maildir 邮箱

此公司邮件服务器中的所有用户都是虚拟用户。他们与本地用户账户无关，当你在 LDAP 目录中创建用户时，没有脚本自动创建主目录或邮箱。

在测试 maildrop 程序之前，你需要创建用户邮箱。目前你必须手动执行此操作（当然，以后可以使用脚本自动化）。Courier maildrop 附带一个名为 `maildirmake` 的实用程序，用于创建 Maildir 邮箱和一些默认子文件夹。

maildrop 查看 LDAP 服务器上的 `homeDirectories` 属性以定位邮箱。然而，由于你切换到了虚拟用户，你可以在 `/home/mailskel` 这样的位置创建一个骨架目录，你可以简单地将其复制到用户主目录中，而无需担心特定的用户权限。

以下是创建外部邮件骨架目录的方法：

```
# mkdir /home/mailskel
# chgrp vmail /home/mailskel
# chmod 770 /home/mailskel
# ls -dall /home/mailskel
drwxrwx---  6 root   vmail      4096 Jun 28 17:52 /home/mailskel
```

现在你可以创建另一个名为 `/home/mailskel/.templateDir` 的目录，并将所有权赋予 `vmail`：

```
# mkdir /home/mailskel/.templateDir
# chown vmail /home/mailskel/.templateDir/
# chgrp vmail /home/mailskel/.templateDir/
# chmod 700 /home/mailskel/.templateDir/
# ls -dall /home/mailskel/.templateDir
drwx------  2 vmail   vmail      4096 Jun 29 22:27 /home/mailskel/.templateDir
```

现在你可以构建实际的邮件目录了。然而，在运行 `maildirmake` 创建基本的 Maildir 目录结构之前，你需要切换到 `vmail` 用户，以便 maildrop 以后能够访问其精确副本：

```
# su - vmail
$ maildirmake /home/mailskel/.templateDir/Maildir
```

验证 `maildirmake` 是否按如下方式创建了目录：

```
$ ls -la /home/mailskel/.templateDir/Maildir
total 20
drwx------  5 vmail   vmail      4096 Jun 29 22:31 .
drwx------  3 vmail   vmail      4096 Jun 29 22:31 ..
drwx------  2 vmail   vmail      4096 Jun 29 22:31 cur
drwx------  2 vmail   vmail      4096 Jun 29 22:31 new
drwx------  2 vmail   vmail      4096 Jun 29 22:31 tmp
```

如你所见，你现在拥有一个名为 `Maildir` 的目录，其中包含三个子目录 `cur`、`new` 和 `tmp`，收件箱消息根据其状态驻留在这些目录中。再运行几次 `maildirmake` 以创建名为 `Drafts`、`Trash` 和 `Spam` 的子文件夹：

```
$ maildirmake -f Drafts /home/mailskel/.templateDir/Maildir
$ maildirmake -f Trash /home/mailskel/.templateDir/Maildir
$ maildirmake -f Spam /home/mailskel/.templateDir/Maildir
$ ls -la /home/mailskel/.templateDir/Maildir
```



```
total 32
drwx------  8 vmail vmail  4096 Jun 29 22:39 .
drwx------  3 vmail vmail  4096 Jun 29 22:31 ..
drwx------  2 vmail vmail  4096 Jun 29 22:31 cur
drwx------  5 vmail vmail  4096 Jun 29 22:39 .Drafts
drwx------  2 vmail vmail  4096 Jun 29 22:31 new
drwx------  5 vmail vmail  4096 Jun 29 22:39 .Spam
drwx------  2 vmail vmail  4096 Jun 29 22:31 tmp
drwx------  5 vmail vmail  4096 Jun 29 22:39 .Trash
```
请注意，每个子目录下都包含 `cur`、`new` 和 `tmp` 子目录。

现在，您的邮件目录模板已准备好，可在为其他用户创建虚拟 Maildir 邮箱时作为骨架使用。请以超级用户身份使用 `cp -pR` 命令，在复制模板时保留所有权和权限。例如，您可以按照以下方式为用户 bammbamm 创建邮箱：
```
# cp -pR /home/mailskel/.templateDir/ /var/spool/mail/bammbamm
# ls -all /var/spool/mail/bammbamm
total 12
drwx------  3 vmail vmail  4096 Jun 29 22:31 .
drwxrwx---  9 root  vmail  4096 Jun 29 22:55 ..
drwx------  8 vmail vmail  4096 Jun 29 22:39 Maildir
# ls -all /var/spool/mail/bammbamm/Maildir/
total 32
drwx------  8 vmail vmail  4096 Jun 29 22:39 .
drwx------  3 vmail vmail  4096 Jun 29 22:31 ..
drwx------  2 vmail vmail  4096 Jun 29 22:31 cur
drwx------  5 vmail vmail  4096 Jun 29 22:39 .Drafts
drwx------  2 vmail vmail  4096 Jun 29 22:31 new
drwx------  5 vmail vmail  4096 Jun 29 22:39 .Spam
drwx------  2 vmail vmail  4096 Jun 29 22:31 tmp
drwx------  5 vmail vmail  4096 Jun 29 22:39 .Trash
```
现在请不要为其余用户创建目录；请先阅读下一节。

##### 创建邮件过滤器

创建 Maildir 模板目录后，您可以为 Courier maildrop 创建一组默认的投递过滤器。首先，在 `/etc/maildroprc` 中配置一套适用于服务器上每个邮件接收者的全局规则。出于调试目的，您可能发现通过此规则将日志文件放入每个用户的主目录会很方便：
```
logfile "$HOME/maildrop.log"
```
现在，您可以开始关注过滤规则了。以下示例中的第一条规则将防止“创建本地传输”一节中提到的 `Delivered-To` 循环。它应始终位于您的 `maildroprc` 文件开头，以便在执行任何其他操作之前捕获问题。第二条规则告诉 maildrop 将任何在邮件头中包含 `X-Spam-Status: Yes` 的邮件放入收件人邮箱（`$DEFAULT`）的 `.spam` 子文件夹：
```
logfile "$HOME/maildrop.log"
if ( /^Delivered-To: $LOGNAME@mail.example.com/:h )
{
  echo "This message is looping, it already has my Delivered-To: Header!"
  EXITCODE = 1
  exit
}
if (/^X-Spam-Status: Yes/)
{
  to $DEFAULT/.spam/
}
```
您可以按用户添加包含额外规则的 `.mailfilter` 文件到收件人的主目录，以进行按用户过滤。您必须使用严格的权限设置，否则 maildrop 将拒绝使用来自 `.mailfilter` 的指令。以下是如何为 bammbamm 创建该文件：
```
# su - vmail
$ cd /var/spool/mail/bammbamm
$ touch .mailfilter
$ chmod 600 .mailfilter
```
回想一下，前面的用户也是 postmaster。因此，以下 `.mailfilter` 过滤规则将邮件头中收件人为 `postmaster@example.com` 的邮件筛选到 `.postmaster` 目录：
```
if (/^To.*postmaster@example\.com/)
{
  to "$DEFAULT/.postmaster/"
}
```
> **注意**
> *全局过滤规则优先于按用户规则。*
当然，您尚未创建 `.postmaster` 文件夹，因此在使用此规则之前，您必须创建它。切换到 `vmail` 用户并运行 `maildirmake`，如下所示：
```
# su - vmail
$ cd /var/spool/mail/bammbamm
$ maildirmake -f postmaster Maildir
```
Maildrop 过滤规则可以大大简化用户的生活，因为他们不必依赖邮件客户端。要了解更多关于 maildrop 过滤功能的信息，请参阅 `maildropfilter(5)` 手册页，并特别注意“其他”部分列出的 http://www.dotfiles.com 示例。

##### 准备 Maildir 配额

配额似乎是一个不错的功能，但在决定启用它们之前，您应该意识到 maildrop 配额系统存在一些争议，因为 Maildir 配额并非始终可靠。Victor Duchovni 的以下陈述总结了一位 Postfix 开发者的观点：
> 真正的症结在于，“maildir++”的用户不想要保证始终可靠的健壮配额代码！他们愿意牺牲健壮性（配额状态文件永远不需要重建，用户始终在配额限制内，……）以换取易用性（无需担心文件系统配额接口，配额可以是软性的，允许在超过配额时具有可配置的有限功能）。
当然，配额的这个方面是已知的（参见 http://www.inter7.com/courierimap/README.maildirquota.html），但许多管理员仍然更愿意接受 Courier maildrop 的优点以及一些轻微的缺点。每种情况都不同，因此您需要自己决定配额事宜。
如果您决定采用，首先在前面“创建本地传输”一节的 maildrop 服务行中添加 `-w 75`，以便在邮件目录容量达到 75%（“软”限制）时生成警告消息。您需要自己设计警告消息模板。创建一个名为 `/usr/local/etc/quotawarnmsg` 的纯文本文件作为模板，包含类似以下内容的消息：
```
From: MAILER-DAEMON <>
To: Valued Customer:;
Subject: Mail quota warning
Mime-Version: 1.0
Content-Type: text/plain; charset=iso-8859-1
Content-Transfer-Encoding: 7bit

Your mailbox on the server is now more than 75% full. So that you can continue to receive mail you need to remove some messages from your mailbox.
```
Maildrop 在将配额警告存储到收件人邮箱时，会添加 `Message-ID` 和 `Date` 头。

#### 测试 Courier Maildrop

现在是时候测试您的 Courier maildrop 安装了。测试包含四个步骤：
1. 测试 Courier maildrop 在没有 Postfix 的情况下是否工作。
2. 使用 Postfix 附带的 `sendmail` 程序向 Courier maildrop 投递一条消息。
3. 测试过滤器是否工作。
4. 测试配额是否工作（如果您选择使用它们）。

##### 测试独立的 Courier Maildrop

切换到 `vmail` 用户，并执行 maildrop 命令（就像 Postfix 执行那样）：
```
# su - vmail
$ /usr/local/bin/maildrop -d bammbamm@example.com
this is a test message
```
在单独的行上输入 `CTRL-D` 来发送消息。通过查看退出码检查 maildrop 是否正常终止，如下所示：
```
$ echo $?
0
```
退出码为零表示成功执行和投递。当然，您也可以验证 maildrop 是否在 bammbamm 的邮件目录中创建了一个新文件：
```
$ ls -l /var/spool/mail/bammbamm/Maildir/new
total 4
-rw-------  1 vmail vmail  23 Jun 30 12:12 1088590342.M975018P6589V000000000000302I0001840E_0.mail.example.com,S=4
```
如果您启用了 Courier maildrop 日志记录，您将在日志中找到此投递证明：
```
Date: Mon Aug  9 09:05:56 2004
From:
Subj:
File: /var/spool/mail/bammbamm/Maildir                (12)
```

##### 结合 Postfix 测试 Courier Maildrop

要结合 maildrop 测试 Postfix，请使用 Postfix 的 `sendmail` 二进制文件并检查您的邮件日志，如下所示：
```
# echo foo | /usr/sbin/sendmail -f rubble@example.com bammbamm@example.com
# tail -f /var/log/maillog
Jul 26 23:20:58 mail postfix/pickup[27883]: 608DD229EF5: uid=0 from=<rubble@example.com>
Jul 26 23:20:58 mail postfix/cleanup[28429]: 608DD229EF5: message-id=<20040726212058.608DD229EF5@mail.example.com>
Jul 26 23:20:58 mail postfix/qmgr[27882]: 608DD229EF5: from=<rubble@example.com>, size=288, nrcpt=1 (queue active)
Jul 26 23:20:58 mail postfix/pipe[28432]: 608DD229EF5: to=<bamm@example.com>, relay=maildrop, delay=0, status=sent (example.com)
Jul 26 23:20:58 mail postfix/qmgr[27882]: 608DD229EF5: removed
```
此处的邮件日志表明 Postfix 将消息中继给了 maildrop。如果您在 `/etc/maildroprc` 中启用了日志记录，您应该在 Bamm Bamm 的 `maildrop.log` 文件中找到类似以下的日志条目：
```
Date: Mon Jul 26 23:24:42 2004
From: rubble@example.com (root)
Subj: 
File: /var/spool/mail/bammbamm/Maildir (345)
```
此条目说明来自 `rubble@example.com`（被 Postfix 标识为 root）的消息被投递到了 `/var/spool/mail/bammbamm/Maildir`，这恰好是 Bamm Bamm 的收件箱。

##### 测试 Courier Maildrop 过滤器

要测试过滤功能，请创建并发送一个名为 `testmessage` 的文件，其中包含一些可以触发 `/etc/maildroprc` 中过滤规则的内容。以下消息应适用于“创建邮件过滤器”一节中的垃圾邮件过滤规则：
```
From: Barney <rubble@example.com>
To: Bamm Bamm <bamm@example.com>
Subject: Test message tagged as SPAM
X-Spam-Status: Yes
foo bar
```
使用 `sendmail` 发送消息，如下所示：
```
# /usr/sbin/sendmail -f rubble@example.com bamm@example.com < testmessage
```
除了检查垃圾邮件子文件夹以验证其是否工作外，还需检查 `maildrop.log` 文件。它应该如下所示：
```
Date: Mon Jul 26 22:29:24 2004
From: Barney <rubble@example.com>
Subj: Test message tagged as SPAM
File: /var/spool/mail/bammbamm/Maildir/.spam/ (412)
```
消息被投递到了子文件夹 `.spam`，因此全局过滤器有效。现在，按照以下方式修改您的测试消息，看看本地过滤器是否工作：
```
From: Barney <rubble@example.com>
To: Postmaster <postmaster@example.com>
Subject: Test message for Postmaster
```



##### 测试 Courier Maildrop 配额

最后，如果你已将 maildrop 配置为使用 Maildir 配额，则需要测试软限制和硬限制是否生效。创建一个 5MB 大小的测试消息，如下所示：

```
# dd if=/dev/zero of=/root/testmessage bs=5M count=1
1+0 records in
1+0 records out
# ls -all testmessage
-rw-r--r-- 1 root root 5242880 Jul 27 09:25 testmessage
```

接下来，使用 `ldapmodify` 为 Bamm Bamm 设置一个较低的配额。它应该在收到第一条测试消息后达到软限制，在收到第二条后达到硬限制。创建一个文件，例如 `modify_bammbamm_quota.ldif`，其中包含你的更改：

```
dn: uid=bammbamm,ou=it,ou=people,dc=example,dc=com
changetype: modify
replace: quota
quota: 6990507S
```

然后运行 `ldapmodify`，并从 `modify_bammbamm_quota.ldif` 导入更改：

```
# ldapmodify -x -D "cn=Manager,dc=example,dc=com" -w secret -f modify_bammbamm_quota.ldif
```

设置完毕后，你可以向 `bamm@example.com` 发送两条测试消息中的第一条：

```
# /usr/sbin/sendmail -f rubble@example.com bamm@example.com < /root/testmessage
```

检查消息是否已投递到 Bamm Bamm 的邮箱：

```
# ls -la
-rw------- 1 vmail vmail 5243221 Jul 27 09:38 1090913892.\ M24019P29629V00000000000000302I00229EF6_0.mail.example.com,S=5243221
-rw-r----- 1 vmail vmail     447 Jul 27 09:38 1090913893.\ M932062P29629V00000000000000302I00229F00_warn.mail.example.com,S=447
```

你可以看到一条额外的、文件名中包含字符串 `warn` 的消息。使用 `cat` 查看其内容：

```
# cat 1090913893.M932062P29629V00000000000000302I00229F00_warn.mail.example.com\,S\=447
From: MAILER-DAEMON <>
To: Valued Customer:;
Subject: Mail quota warning
Mime-Version: 1.0
Content-Type: text/plain; charset=iso-8859-1
Content-Transfer-Encoding: 7bit

Your mailbox on the server is now more than 75% full. So that you can
continue to receive mail you need to remove some messages from your mailbox.
```

Maildrop 已经投递了消息，并在收件人的邮箱中创建了一条邮件配额警告消息。由于邮箱已被认为是 75% 满，你的下一条消息将达到硬限制；Maildrop 将不得不将消息退信回 `rubble@example.com`：

```
# /usr/sbin/sendmail -f rubble@example.com bamm@example.com < /root/testmessage
```

在邮件日志中，你应该会看到该消息被退回给发件人：

```
# tail -f /var/log/maillog
Jul 27 09:59:18 mail postfix/pickup[29788]: 4C083229F09: uid=0
  from=<rubble@example.com>
Jul 27 09:59:18 mail postfix/cleanup[29793]: 4C083229F09:
  message-id=<20040727075918.4C083229F09@mail.example.com>
Jul 27 09:59:18 mail postfix/qmgr[29789]: 4C083229F09:
  from=<rubble@example.com>, size=5250843, nrcpt=1 (queue active)
Jul 27 09:59:19 mail postfix/pipe[29795]: 4C083229F09: to=<bamm@example.com>,
  relay=maildrop, delay=1, status=bounced (permission denied. Command output:
  maildrop: maildir over quota. )
```

退信通知发件人 `rubble@example.com`，由于以下原因无法投递：`<bamm@example.com>: permission denied. Command output: maildrop: maildir over quota.`

### 配置 Courier IMAP

你需要配置的最后一个服务器是 Courier IMAP。如果你还不熟悉它，Courier 支持 Maildir 格式，并为客户端提供 POP、POP-SSL、IMAP 和 IMAP-SSL 服务。

#### 安装 Courier IMAP

要安装 Courier IMAP 服务器，请从 `http://www.courier-mta.org/download.php#imap` 下载源代码。以普通用户身份，解压存档，切换到新目录，并按如下所示运行 **configure**。

```
$ ./configure --enable-workarounds-for-imap-client-bugs --enable-unicode --without-authpgsql --without-socks
$ make
```

配置过程会自动检测你机器上的 LDAP 库。

> **注意** *如果你运行的是 Red Hat，请在配置选项中添加 `--with-redhat` 以启用 Red Hat 特定的解决方法。*

配置完成后，切换到 root 用户并运行 `make install install-configure` 来安装软件和文档。

#### 将 Courier IMAP 配置为使用其 LDAP 认证守护进程

Courier 使用模块化认证后端（如果你使用默认选项编译 Courier IMAP，模块位于 `/usr/lib/courier-imap/libexec/authlib`）。要将 Courier 认证守护进程（authdaemon）配置为仅使用 LDAP 认证，请更改 `/usr/lib/courier-imap/etc/authdaemonrc` 中 `authmodulelist` 参数的值，使其如下所示：

```
authmodulelist="authldap"
```

为保持一致性，你应该从 `authmodulelist` 中删除所有其他模块名称。
在编辑 `authdaemonrc` 文件时，转到文件末尾，更改或添加 `version` 参数，使其仅包含 `authdaemond.ldap`（否则，authdaemon 会选择它找到的第一个 `authdaemond.*` 模块）：

```
version="authdaemond.ldap"
```

#### 配置认证后端

现在你需要告诉认证后端你的 LDAP 服务器和目录信息。要配置 `authdaemond.ldap` 模块，请更改 `/usr/lib/courier-imap/etc/authldaprc` 中的默认条目以匹配你的服务器和目录。要使其与本章中的示例一起工作，请指定以下参数：

| 参数 | 值 |
| :--- | :--- |
| LDAP_SERVER | mail.example.com |
| LDAP_BASEDN | dc=example,dc=com |
| LDAP_MAIL | mail |
| LDAP_FILTER | (objectClass=inetorgperson) |
| LDAP_HOMEDIR | homeDirectory |
| LDAP_MAILDIR | mailbox |
| LDAP_MAILDIRQUOTA | quota |
| LDAP_CLEARPW | userPassword |
| LDAP_UID | uidNumber |
| LDAP_GID | gidNumber |

> `authldaprc` 中的注释对于解释这些参数非常有帮助。

##### 创建 IMAP 证书

剩下唯一要做的事情是为 Courier IMAP 创建一个安全证书。虽然 Courier 在启动 `imapd-ssl` 时会自动创建一个（并且它自带 `mkimapdcert` 工具），但我们实际上无法使用它，因为它不是由我们的证书颁发机构签名的。
按照以下步骤创建证书：

1.  假设你已经按照第 17 章的描述建立了自己的 CA，你可以按如下方式创建 `imapd` 证书：

```
# openssl req -new -nodes -keyout imapd_private_key.pem -out imapd_private_key.pem -days 365
```

2.  使用你的 CA 签署密钥，创建公共证书：

```
# openssl ca -policy policy_anything -out imapd_public_cert.pem -infiles imapd_private_key.pem
```

3.  为 Courier IMAP 创建证书文件与为 Postfix TLS 和 OpenLDAP 创建略有不同。连接两个密钥文件以创建 `imapd.pem` 文件：

```
# cat imapd_private_key.pem imapd_public_cert.pem > imapd.pem
```

4.  将证书复制到 Courier 可以找到的位置，并设置正确的权限以保护文件内的私钥：

```
# cp imapd.pem /usr/lib/courier-imap/share/imapd.pem
# chmod 600 /usr/lib/courier-imap/share/imapd.pem
# chown root /usr/lib/courier-imap/share/imapd.pem
```

5.  启动 `imapd` 的 SSL 实例：

```
# /usr/lib/courier-imap/libexec/imapd-ssl.rc start
```

6.  使用 `ps` 确保它已启动：

```
# ps auxwww | grep imapd-ssl
root 1676 0.0 0.3 1940 500 ? S 16:08 0:00 /usr/lib/courier-imap/libexec/couriertcpd -address=0 -stderrlogger=/usr/lib/courier-imap/sbin/courierlogger -stderrloggername=imapd-ssl -maxprocs=40 -maxperip=4 -pid=/var/run/imapd-ssl.pid -nodnslookup -noidentlookup 993 /usr/lib/courier-imap/bin/couriertls
root  1680  0.0  0.2  1952  340 ?   S  16:08  0:00 /usr/lib/courier-imap/sbin/courierlogger imapd-ssl
root  1810  0.0  0.4  4600  564 pts/0  S  17:24  0:00 grep imapd-ssl
```

**注意** 你可以使用 `/usr/lib/courier-imap/libexec` 中的脚本，并将它们复制到你的 `init.d` 目录中，以便在更改运行级别时自动启动和停止 Courier。

#### 测试 IMAP 服务器

要验证你的 IMAP 服务器可访问且用户可以登录，请连接到服务器的 143 端口并执行一个会话。按如下方式连接到服务器：

```
# telnet mail.example.com 143
* OK [CAPABILITY IMAP4rev1 UIDPLUS CHILDREN NAMESPACE \
      THREAD=ORDEREDSUBJECT THREAD=REFERENCES SORT QUOTA \
      IDLE ACL ACL2=UNION STARTTLS] Courier-IMAP ready. \
      Copyright 1998-2004 Double Precision, Inc.  \
      See COPYING for distribution information.
```

看到上述问候消息后，登录：

```
. login bamm bamm bamm_password
. OK LOGIN Ok.
```

现在选择收件箱以查看文件夹是否正常工作：

```
. select INBOX
* FLAGS (\Draft \Answered \Flagged \Deleted \Seen \Recent)
* OK [PERMANENTFLAGS (\* \Draft \Answered \Flagged \Deleted \Seen)] Limited
* 5 EXISTS
* 0 RECENT
* OK [UIDVALIDITY 1089237749] Ok
* OK [MYRIGHTS "acdilrsw"] ACL
. OK [READ-WRITE] Ok
```

最后，注销：

```
. logout
* BYE Courier-IMAP server shutting down
. OK LOGOUT completed
```



##### 通过 TLS 测试 IMAP

要通过 TLS 测试 IMAP，请使用 OpenSSL 的 `s_client` 工具，而不是 telnet。让它连接到端口 993（即 imaps 端口）。该客户端会显示相当多的证书检查输出，但连接建立后，你可以像使用前面的未加密会话一样使用它。以下是其输出的示例：

```
# openssl s_client -CAfile /usr/share/ssl/certs/cacert.pem -connect localhost:993
CONNECTED(00000003)
depth=1 /C=EX/ST=Examplia/L=Exampleton/O=Example Inc./OU=Certification
    Authority/CN=mail.example.com/emailAddress=certmaster@example.com
verify return:1
depth=0 /C=EX/ST=Examplia/L=Exampleton/O=Example Inc./OU=IMAP \
    services/CN=mail.example.com/emailAddress=postmaster@example.com
verify return:1
---
Certificate chain
  0 s:/C=EX/ST=Examplia/L=Exampleton/O=Example Inc./OU=IMAP services/\
        CN=mail.example.com/emailAddress=postmaster@example.com
    i:/C=EX/ST=Examplia/L=Exampleton/O=Example Inc./OU=Certification
        Authority/ CN=mail.example.com/emailAddress=certmaster@example.com
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIE DDCCA3MgAwIBAgIBANBgkqhkiG9w0BAQQFADCBS DELMAKGA1UEBhMCRVgx
ETAPBgNVBAgTCEV4YW1wbGlhMRMwEQYDVQQHEwpFcGFtcGxldG9uMRUwEwYDVQQK
EwxsFeGFtcGxldGlEuVy4xIDAEcBgNVBAsTF0NlcnRpZmljYXRpb24gQXV0aG9y
MRkwFwYDVQQDExBtYXRpbG50a2xhbG1hLMSUwIYJKoZIhvcNAQkBFgNtYXRl
bWZzdGV2QYy1wbGUuY29tMB4XDTE0MDcxMzE4NTMwMloxDzANBgNVHRwEBwE=
MlowgaYxc2ABgNVBAgTMEV4YW1wbGlhMRMwEQYDVQQHEwpFcGFtcGxldG9uMRUw
RXhhbXBsZSIncjVvb0VMVWdwbmxhLXhSbWJkMUJyYW1FYUZkVVQQLeUJ1TUFP
IHn1cNzPY2ZzMRkwFwYDVQQDExBtYXRpbG50a2xhbG1hLMSUwIYJKoZIhvcNAQkE
FAoBFhZwb3NBdWZzdGV2QYy1wbGUuY29tMIGfMAoGCCqGSIb3DQEBAQUAAGN
ADCBiQKBgQClw1tVdVghNLPEmY3Bw/iMKkXtNhX11lAUVEshZEIDGGJBIq9w8
QC4mLB0sWTYTLXtUbvoJHmBCmf6tzVo01932r4KTDzanLP7EDc4tvg8ohFuXEka
1VA+1g3l5oY8v1LIOYwS8fpmRQENYHWncoShmXRPjg4wO6/2pZaawIDAQABo4IB
PdCCATgCQYDVR0TBAIwADAsBglghkgBhvhCAQ0EhYd0Td3B11bNTTCBHw51cmFO
ZW0gQ2VyVWd1maWdhdGh0UQDVR0BBDYwNMAoEYYE61+FMCqcC3M/Em3X2I8Cn8JM1Hd
BgNVHSMEdgdKdKFMNGZ7/NorS6WpJQJZ21hDno97iXoYG2pIgZVMIgwMQswCQYD
VQQGEwJFWDhERMA8GA1UEBMIRXhhbXBsaWd0ZzVwNExwBsaWTcKv4YW1wb00b24x
FTATBgNVBAoTDEV4YW1wbGlhMRMwEQYDVQQHEwpFcGFtcGxldG9uMRUwEwYDVQQK
dXR0b3dJpdHkXa0ZVY1h0aWd0Z0VXamxhaWdhdGh0dGR0b3dJpdHkX
CQEWFMn1cnRtYXNoZ1pAZXhhbXBlb20tY2Vjb20gQXODJqoZIhvcNAQkEFgEA
iqd/nOvhip1EWF+K7hgbpt1v13tzyuE3TMSI3oXtGnQtYNLTvx3eaYDBecUQA1I
q1ocQBsVz17+no29JwD69UlBWANwxDuobPHmrr7CeePVnv6fAyZ4Jg9x8vApzDD
Nu/Tu88MokEVQ2XT35oPM+gDy3Mw44NnYB2xhky8Ptg=
-----END CERTIFICATE-----
subject=/C=EX/ST=Exemplia/L=Exampleton/O=Example Inc./OU=IMAP services/CN=mail.example.com/emailAddress=postmaster@example.com
issuer=/C=EX/ST=Exemplia/L=Exampleton/O=Example Inc./OU=Certification Authority/CN=mail.example.com/emailAddress=certmaster@example.com
---
No client certificate CA names sent
---
SSL handshake has read 1202 bytes and written 340 bytes
---
New, TLSv1/SSLv3, Cipher is AES256-SHA
Server public key is 1024 bit
SSL-Session:
    Protocol  : TLSv1
    Cipher    : AES256-SHA
    Session-ID: 7AA6E031976D8B3846F1B2C8FCBEBEB777C89BAD16E548C0D8FE0B170BF1D49B
    Session-ID-ctx:
    Master-Key: E41CE39B98EFF3395936404F7142D2804FA7BBE63ADB6A57F3FB513A756E6D55F548A5765AC27F99F862F46664131C72
    Key-Arg   : None
    Krb5 Principal: None
    Start Time: 1089732738
    Timeout   : 300 (sec)
    Verify return code: 0 (ok)
---
* OK [CAPABILITY IMAP4rev1 UIDPLUS CHILDREN NAMESPACE THREAD=ORDEREDSUBJECT THREAD=REFERENCES SORT QUOTA IDLE AUTH=PLAIN ACL ACL2=UNION] Courier-IMAP ready. \
Copyright 1998-2004 Double Precision, Inc.  See COPYING for distribution information.
. login bamm@example.com bamm_secret
. OK LOGIN Ok.
. logout
* BYE Courier-IMAP server shutting down
. OK LOGOUT completed
closed
```

恭喜！你现在拥有一个可正常工作的基于 LDAP 的邮件服务器。但还有一些工作要做。

## 高级配置

你的邮件服务器已经可以运行，但你还有更多的工作要做。目前，任何能够连接到 LDAP 服务器的人都可以检索与安全相关的数据，例如 userPassword 属性。此外，各个服务器（包括 Postfix）检索的所有数据都是通过明文 LDAP 会话进行的。

你的首要任务应该是通过加强安全措施来解决这些问题。本节将向你展示如何在 LDAP 服务器中使用绑定用户，以便限制 LDAP 服务器可以发送给客户端的内容。此外，你还将了解如何加密 LDAP 会话本身。作为额外的好处，你将配置基于 ldapdb 的 SMTP 身份验证，并利用它来执行公司策略，以防止发送者地址被潜在滥用。

### 扩展目录

控制对 LDAP 目录的访问和执行 SMTP 身份验证需要你为所有依赖该目录的服务器设置账户。为此，你需要扩展目录树，添加另一个顶级分支，将服务器与邮件用户分隔开。图 19-3 展示了名为 ou=auth,dc=example,dc=com 的新分支，其中包含 account 类的对象。

![](img/852c79f689feb77c5fde686b993808b1_377_0.png)

在明文目录中，你将使用以下属性和模式：

```
dn: ou=auth,dc=example,dc=com
ou: auth
objectClass: organizationalUnit
dn: uid=postfix,ou=auth,dc=example,dc=com
uid: postfix
objectClass: account
objectClass: simpleSecurityObject
description: Postfix Bind user
userPassword: {CRYPT}9lGRsJNHN5DrI
dn: uid=couriermaildrop,ou=auth,dc=example,dc=com
uid: couriermaildrop
objectClass: account
objectClass: simpleSecurityObject
description: Courier Maildrop Bind user
userPassword: {CRYPT}lA8iQdmwZRC86
dn: uid=courierimap,ou=auth,dc=example,dc=com
uid: courierimap
objectClass: account
objectClass: simpleSecurityObject
description: Courier IMAP Bind user
userPassword: {CRYPT}S1t1/3ENmjk1s
dn: uid=ldapdb,ou=auth,dc=example,dc=com
uid: ldapdb
objectClass: inetOrgPerson
givenName: ldapdb
sn: ldapdb
cn: ldapdb
userPassword: AvaAg07i
mail: ldapdb
saslAuthzTo: ldap:///ou=people,dc=example,dc=com??sub?(objectclass=inetOrgPerson)
```

每个通过 ldapdb 模块访问 LDAP 目录的服务器（Postfix、Courier maildrop、Courier IMAP 和 Cyrus SASL）都将拥有自己的账户。uid=ldapdb,ou=auth,dc=example,dc=com 对象中的属性与其他对象有以下不同：

-   密码以明文格式存储，以启用 DIGEST-MD5 共享密钥身份验证机制（该机制无法访问加密的密码）。
-   新的 mail 属性将替代 uid 用于验证用户身份。
-   saslAuthzTo 属性定义了 ldapdb 可以代表哪个用户的身份。

### 为服务器添加身份验证

我们要实现的第一个功能是通过 SMTP 身份验证进行邮件中继，以便 IP 地址在本地可信网络之外的移动和远程用户能够发送邮件。你已经了解了在没有 LDAP 的情况下如何实现这一点（参见"理解 SMTP 身份验证"一节），但这次我们将使用 ldapdb 插件来构建和配置 Cyrus SASL。你始终可以使用 saslauthd 独立守护进程来完成此操作，但遗憾的是，该守护进程仅限于明文学机制。完成本节内容后，你的 Postfix 服务器应该能够向邮件客户端提供明文机制（PLAIN、LOGIN）和共享密钥机制（CRAM-MD5、DIGEST-MD5）。

身份验证过程与第 16 章（讨论 Postfix 和 Cyrus SASL 交互）中描述的略有不同，因为它使用授权 ID 来验证身份。此标识符源自 Cyrus IMAP 项目，在该项目中允许一组用户代表某个用户进行操作。例如，你可以设置 Cyrus IMAP 允许其他人在不交换任何密码的情况下读取休假用户的邮件。

ldapdb 身份验证过程如下：

1.  使用 SMTP 身份验证的邮件客户端连接到 Postfix 服务器并传输用户名（如果使用明文机制，还包括密码）。此用户名在 SASL 上下文中是身份验证 ID。
2.  Postfix smtpd 要求 SASL 库验证凭据。SASL 库将此任务委托给 ldapdb 插件，由它与 LDAP 服务器进行通信。
3.  Postfix smtpd 守护进程的 ldapdb 配置包含另一个用户名和密码（ldapdb 仅在客户端使用明文机制时才传输密码）。此用户名在 SASL 上下文中称为授权 ID，因为它有权从邮件用户（身份验证 ID）那里检索密码。
4.  如果 ldapdb 成功从 LDAP 服务器检索到密码，它会将该字符串与邮件客户端提供的密码进行比较。具体的验证方法取决于邮件客户端使用的机制。明文机制意味着执行简单的字符串比较，而共享密钥机制则使 ldapdb 使用密码计算字符串并进行比较。

如果任一方法成功，即身份验证成功，ldapdb 将信息传回 SASL，然后 SASL 告知 Postfix 可以授予中继访问权限。

#### 应用 ldapdb 补丁

ldapdb 插件由 OpenLDAP 架构师 Howard Chu 贡献给 Cyrus SASL，旨在使 SASL 身份验证支持共享密钥机制。虽然 ldapdb 已计划纳入未来的 Cyrus SASL 版本，但截至目前（Cyrus SASL 2.1.19），它尚未包含在当前发行版中。为了方便你为 Cyrus SASL 添加 ldapdb 支持，我们创建了一个补丁，你可以从 http://www.postfix-book.com 网站下载。

要将补丁应用到 Cyrus SASL 源文件，请解压一份全新的 SASL 发行包并切换到新目录。按照以下示例应用补丁。



# patch -p1 < ../cyrus-sasl-2.1.19-ldapdb.patch
patching file config/openldap.m4
patching file configure.in
patching file doc/install.html
patching file doc/options.html
patching file doc/readme.html
patching file doc/sysadmin.html
patching file lib/staticopen.h
patching file plugins/ldapdb.c
patching file plugins/Makefile.am
patching file plugins/makeinit.sh

如果补丁顺利应用，按如下方式构建 Cyrus SASL（注意 `--with-ldap*` 选项）：

```
# ./configure \
    --with-plugindir=/usr/lib/sasl2 \
    --disable-java \
    --disable-krb4 \
    --with-dblib=berkeley \
    --with-saslauthd=/var/state/saslauthd \
    --without-pwcheck \
    --with-devrandom=/dev/urandom \
    --enable-cram \
    --enable-digest \
    --enable-plain \
    --enable-login \
    --disable-otp \
    --with-ldap=/usr \
    --with-ldapdb
```

配置过程完成后，你可以通过运行 `make install` 来安装或升级当前版本的 SASL。如果尚未创建，请从 `/usr/local/lib/sasl2` 到 `/usr/lib/sasl2` 创建一个符号链接，因为 SASL 在使用这些特定配置选项时会期望在该目录中找到库文件。

完成后，你应该能在 `/usr/lib/sasl2` 中看到这些新的 ldapdb 库：

```
# ls -la libldapdb.*
-rwxr-xr-x  1 root root  702 Jul 16 20:43 libldapdb.la
lrwxrwxrwx  1 root root   19 Jul 16 20:43 libldapdb.so -> libldapdb.so.2.0.19
lrwxrwxrwx  1 root root   19 Jul 16 20:43 libldapdb.so.2 -> libldapdb.so.2.0.19
-rwxr-xr-x  1 root root 94948 Jul 16 20:43 libldapdb.so.2.0.19
```

#### 配置 ldapdb

正如前面"为服务器添加认证"一节所述，你必须在 `/usr/lib/sasl2/smtpd.conf` 中为 Postfix `smtpd` 守护进程创建 SASL 配置，才能使 Postfix 使用 SASL。

示例如下：

```
pwcheck_method: auxprop
auxprop_plugin: ldapdb
mech_list: PLAIN LOGIN DIGEST-MD5 CRAM-MD5
ldapdb_uri: ldap://mail.example.com
ldapdb_id: proxyuser
ldapdb_pw: proxy_secret
ldapdb_mech: DIGEST-MD5
log_level: 7
```

额外的 LDAP 相关配置参数是 ldapdb_id 和 ldapdb_pw。此处的用户名是授权 ID。（请记住，ldapdb 插件要求 smtpd 使用授权 ID，然后才能成为邮件用户的身份并重新进行认证。）

#### 配置 OpenLDAP 授权策略

现在你已经设置好了 Postfix 绑定到 OpenLDAP 服务器，但你仍需配置 OpenLDAP slapd 来认证用户并授权其成为另一个用户。首先，选择一个策略来定义 slapd 应如何处理已认证的用户。将 slapd.conf 文件中的 sasl-authz-policy 参数设置为以下选项之一：

- **none** 禁用授权。这是默认设置。
- **from** 要求每个 LDAP 用户明确允许一个或多个用户充当授权 ID。要允许授权，他们需要将自己的用户对象添加 saslAuthzFrom 属性。此属性包含可以使用其身份的用户的 dn（可分辨名称）。
- **to** 默认允许所有用户充当授权 ID。使用此策略时，用户将自己的用户对象添加 saslAuthzTo 属性，该属性定义了在哪些情况下可以使用其他用户的身份。LDAP 目录管理员必须创建规则，仅允许有限数量的用户使用其他身份（以防止滥用）。
- **both** 同时激活 from 和 to 策略。

> **注意** 你可以在《OpenLDAP 管理员指南》第 10 章（http://www.openldap.org/doc/admin22/sasl.html#SASL%20Proxy%20Authorization）中找到更详细的信息。

在本书中我们将使用 `to` 作为策略，因为我们认为管理员限制谁可以使用其他身份比为每个用户对象添加新属性更容易。要配置本章示例的策略，请在 slapd.conf 中添加以下行：

```
sasl-authz-policy to
```

#### 配置 SASL OpenLDAP 绑定

要完成启用基于 SASL 的绑定到 OpenLDAP 服务器的最后一步，你需要配置 slapd 的凭据存储目录分支。你还需要为给定的认证 ID 指定查询属性。这通过一个名为 `sasl-regexp` 的搜索过滤器来处理，该过滤器定义了 smtpd 绑定（授权 ID）应在何处搜索需要认证的用户。

将过滤器按如下方式放入你的 slapd.conf 配置文件：

```
sasl-regexp
    uid=(.*),cn=.*,cn=auth
    ldap:///dc=example,dc=com??sub?(&(objectclass=inetOrgPerson)(mail=$1))
```

**注意** 前面的正则表达式查找的不是 uid（登录名），而是邮件地址。这是有意为之的；许多 ISP 和邮件服务提供商使用电子邮件地址作为登录名。使用电子邮件地址作为登录名有很多原因，但主要的两个原因是：用户需要少记一个值，以及更容易与其他系统（如 Radius 服务器）共享认证数据。

过滤器配置完成后，重启你的 OpenLDAP 服务器，检查日志是否有问题，然后开始测试。

### 测试 ldapdb 插件

你需要在 ldapdb 配置中检查三个要点：

- 机制限制
- 直接基于 SASL 的绑定
- 基于 ldapdb 的认证

#### 测试机制限制

确保 `/usr/lib/sasl2/slapd.conf` 配置中的 mech_list 参数生效。按如下方式运行 ldapsearch 来列出 slapd 提供给客户端的机制：

```
# ldapsearch -LLL -x -s base -b "" "(objectClass=*)" supportedSASLMechanisms
dn:
supportedSASLMechanisms: DIGEST-MD5
```

如果你的输出与此类似，说明一切正常。否则请检查你的 slapd.conf 文件是否有拼写错误。

#### 测试直接 SASL 绑定

验证你目录中的用户可以使用 SASL（不通过 ldapdb 插件）直接绑定到 slapd，方法是使用 ldapwhoami 命令。

```
# ldapwhoami -U bamm@example.com
SASL/DIGEST-MD5 authentication started
Please enter your password:
SASL username: bamm@example.com
SASL SSF: 128
SASL installing layers
dn:uid=bammbamm,ou=it,ou=people,dc=example,dc=com
```

此测试验证你确实可以以用户身份进行认证。如果测试失败，你将无法继续进行后续步骤。请回顾"配置 SASL OpenLDAP 绑定"一节，查看是否有错误。

#### 测试 ldapdb 认证

Cyrus SASL 附带了名为 `server` 和 `client` 的实用程序，允许你在独立于其他服务器的情况下测试认证。使用它们可以消除 Postfix 等软件包可能引入的副作用，使你能够专注于基于 SASL 的问题，包括涉及 ldapdb 的问题。

要测试认证，首先为 server 创建从 smtpd.conf 到 sample.conf 的符号链接：

```
# cd /usr/lib/sasl2/
# ln -s smtpd.conf sample.conf
```

现在，打开一个终端窗口并启动 server：

```
# ./server -s rcmd -p 23
trying 10, 1, 6
socket: Address family not supported by protocol
trying 2, 1, 6
```

打开第二个终端窗口，使用 LDAP 服务器中用户的 LDAP uid 启动 client。该程序会要求你输入认证 ID 和授权 ID。以下是为 bammbamm（dn: uid=bammbamm,ou=it,ou=people,dc=example,dc=com）执行的操作：

```
# ./client -s rcmd -p 23 -m PLAIN mail.example.com
receiving capability list... recv: {31}
LOGIN PLAIN DIGEST-MD5 CRAM-MD5
LOGIN PLAIN DIGEST-MD5 CRAM-MD5
please enter an authentication id: bammbamm
please enter an authorization id: bammbamm
Password:
send: {5}
PLAIN
send: {1}
Y
send: {29}
bammbamm[0]bammbamm[0]bamm_secret
successful authentication
closing connection
```

注意
授权 ID 将被替换为你 sample.conf 文件中 ldapdb_id 参数指定的值，但你仍然需要在提示符处输入内容。

如果你看到"successful authentication"（如上述输出所示），则基于 ldapdb 的认证正常工作。否则，请查看你的认证日志和 Cyrus SASL 日志，以找出问题所在。

## 保护目录数据

出于安全考虑，你不希望 LDAP 服务器上的所有数据都能被任何查询服务器的人读取。你可以通过对绑定到 LDAP 服务器的用户设置访问控制列表（ACL）来限制服务器上的读取访问。这是一个两步过程：

1. 配置 LDAP 服务器以限制读取访问。
2. 配置依赖 LDAP 的软件包以绑定到 LDAP 服务器。

### 限制目录读取访问

在前面的"扩展目录"一节中，你已向目录中添加了绑定用户。现在你必须告诉 slapd 绑定用户可以访问目录的哪些部分，以及其他用户（如匿名用户）可以做什么。

将以下规则添加到你的 `/etc/openldap/slapd.conf` 文件：

```
# saslAuthzTo 的访问规则
access to dn.subtree="dc=example,dc=com" attr=saslAuthzTo
    by dn.base="cn=Manager,dc=example,dc=com"    write
    by *                                            read
# userPassword 的访问规则
# 已认证用户（self）和目录 Manager 可以
# 更改其（自身的）密码。
# 其他任何人在认证过程中可以访问密码。
access to dn.subtree="dc=example,dc=com"
    attr=userPassword
    by self                                            write
    by dn.base="cn=Manager,dc=example,dc=com"         write
    by dn.base="uid=courierimap,ou=auth,dc=example,dc=com"  read
    by *                                                auth
# uidNumber、gidNumber、mailbox、homeDirectory、quota 的访问规则
# 只有 Manager 可以更改它们的值。
# 需要这些值的应用程序可以读取它们。
# 已认证用户可以读取自己的数据。
# 其他任何人不能访问这些数据。
```



### 在 LDAP 客户端中配置绑定用户

配置好 OpenLDAP ACL 后，你需要为每个访问 LDAP 服务器的应用程序配置一个绑定用户。

### 将 Postfix 配置为绑定用户

要使 Postfix 以绑定用户身份连接到 LDAP 服务器，你必须修改 `/etc/postfix/ldap` 目录下配置文件中的三个参数。这些参数是 `bind`、`bind_dn` 和 `bind_pw`：

-   `bind` 参数必须设置为 yes 以启用绑定用户。
-   `bind_dn` 参数设置绑定用户的可分辨名称。在本章示例中，你可以设置 `bind_dn = uid=postfix,ou=auth,dc=example,dc=com`。
-   `bind_pw` 参数设置密码（明文形式）。

> **注意**
> 你可以看到，你需要保护这些数据的安全，因为它包含密码。这就是我们在本章开头为 LDAP 查询配置文件创建单独目录的原因。

完成后，`/etc/postfix/ldap` 中的所有配置文件应包含如下行：

```
bind = yes
bind_dn = uid=postfix,ou=auth,dc=example,dc=com
bind_pw = Yanggt!
```

### 将 Courier Maildrop 配置为绑定用户

Courier maildrop 的参数与 Postfix 的几乎相同，只是没有用于切换绑定系统的参数（如果你不指定绑定可分辨名称，Courier 不会尝试绑定）。你将在 `/etc/maildropldap` 文件中使用的参数是 `binddn` 和 `bindpw`；配置应类似于以下内容：

```
binddn          uid=couriermaildrop,ou=auth,dc=example,dc=com
bindpw          Yrj6h16r
```

> **警告**
> 现在你有了明文密码，请确保 `/etc/maildropldap` 只能由 root 访问。

### 将 Courier IMAP 配置为绑定用户

你需要配置为绑定用户的最后一个客户端是 Courier IMAP。与 Courier maildrop 一样，你只需要在 `/usr/lib/courier-imap/etc/authldaprc` 文件中设置两个参数——`LDAP_BINDDN` 和 `LDAP_BINDPW`：

```
LDAP_BINDDN      uid=courierimap,ou=auth,dc=example,dc=com
LDAP_BINDPW      X5mYp16p
```

> **警告**
> 同样，请确保你的 IMAP LDAP 配置文件（`/usr/lib/courier-imap/etc/authldaprc`）只能由 root 访问。

### 测试服务器限制

要测试服务器，请回顾“测试 LDAP 收件人”一节；你只需确保每个组件都能从 LDAP 服务器检索数据。如果遇到问题，请检查日志文件。特别要仔细查看 slapd 日志文件。如果需要调整 slapd 日志级别，请按照 slapd.conf(5) 手册页中描述的方法调整 `loglevel` 参数。

### 加密 LDAP 查询

虽然你现在保护了 LDAP 服务器上的数据免受未授权用户访问，但在数据通过不安全的网络传输时，你还没有采取任何措施来保证其安全。本节向你展示如何使用 TLS 来保护通信层。

#### 为 OpenLDAP 配置 TLS

在尝试为你的 LDAP 安装配置 TLS 之前，请验证 slapd 是否支持 TLS。如果支持 TLS，对 slapd 运行 `ldd` 命令通常会显示对 SSL 库的依赖：

```
# ldd /usr/sbin/slapd
	libslapd_db-4.1.so => /usr/lib/libslapd_db-4.1.so (0x00116000)
	libsasl2.so.2 => /usr/lib/libsasl2.so.2 (0x00101000)
	libkrb5.so.3 => /usr/lib/libkrb5.so.3 (0x00a6f000)
	libk5crypto.so.3 => /usr/lib/libk5crypto.so.3 (0x00ad8000)
	libcom_err.so.2 => /lib/libcom_err.so.2 (0x00a6a000)
	libssl.so.4 => /lib/libssl.so.4 (0x00b11000)
	libcrypto.so.4 => /lib/libcrypto.so.4 (0x00977000)
	libcrypt.so.1 => /lib/libcrypt.so.1 (0x008d0000)
	libresolv.so.2 => /lib/libresolv.so.2 (0x00965000)
	libdl.so.2 => /lib/libdl.so.2 (0x008b8000)
	libwrap.so.0 => /usr/lib/libwrap.so.0 (0x00bfe000)
	libpthread.so.0 => /lib/libpthread.so.0 (0x00912000)
	libc.so.6 => /lib/libc.so.6 (0x0076e000)
	libgssapi_krb5.so.2 => /usr/lib/libgssapi_krb5.so.2 (0x00afc000)
	libz.so.1 => /usr/lib/libz.so.1 (0x008bd000)
	/lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x00759000)
	libnsl.so.1 => /lib/libnsl.so.1 (0x008fe000)
```

你需要执行以下步骤来为 slapd 配置 TLS：

1.  为 slapd 创建 X509 证书。
2.  配置 slapd 以提供 TLS。
3.  配置 LDAP 客户端以使用 TLS。

##### 为 slapd 创建 X509 证书

与任何提供基于 SSL 加密的服务器一样，你必须为 slapd 创建包含公钥和私钥的证书。第 17 章解释了如何创建证书。
假设你运行自己的 CA，你可以按如下方式为 slapd 创建一个名为 `slapd_private_key.pem` 的私钥文件：

```
# openssl req -new -nodes -keyout slapd_private_key.pem -out \
  slapd_private_key.pem -days 365
```

创建名为 `slapd_public_cert.pem` 的公钥的相应命令如下：

```
# openssl ca -policy policy_anything -out slapd_public_cert.pem -infiles \
  slapd_private_key.pem
```

现在在 `/etc/openldap` 中创建一个名为 `certs` 的子目录来存放你的密钥。
将 `.pem` 文件复制到子目录后，目录内容应如下所示：

```
# ls -la /etc/openldap/certs/
total 24
drwx------ 2 ldap ldap 4096 Jun 21 22:31 .
drwxr-xr-x 4 root root 4096 Jun 21 23:12 ..
-rw------- 1 ldap ldap 1624 Jun 21 22:31 slapd_private_key.pem
-rw------- 1 ldap ldap 3807 Jun 21 22:31 slapd_public_cert.pem
```

> **警告**
> 确保更改文件的所有权和权限，使其只能由运行 slapd 的用户访问。

##### 配置 slapd 以提供 TLS

要告知 slapd 你的新证书文件，你需要在 `slapd.conf` 文件中添加四个参数：

```
TLSCACertificateFile /usr/share/ssl/certs/cacert.pem
TLSCACertificateFile /etc/openldap/certs/slapd_public_cert.pem
TLSCACertificateKeyFile /etc/openldap/certs/slapd_private_key.pem
TLSVerifyClient demand
```

`TLSCACertificateFile` 参数指定了 CA 证书的位置。在本例中，slapd 查找单个文件来获取此证书，但你可能需要多个文件。如果是这种情况，你可以省略文件名，让 slapd 搜索整个目录。你还需要使用 OpenSSL 工具中的 `c_rehash` 来建立目录索引，如第 18 章所述。

> **注意**
> 你的 CA 证书应位于其他 LDAP 客户端可以访问的位置。

你可以将 `TLSVerifyClient` 参数设置为 `never`、`allow`、`try` 或 `demand` 之一，以限制某些类型身份验证的访问。你需要确保 TLS 设置在客户端侧有效，因此将此参数设置为 `demand` 以强制客户端使用 TLS。这样可以轻松判断客户端是否支持它。

##### 为 LDAP 客户端配置 TLS

本节向你展示如何在 Postfix 和 Courier IMAP 中启用客户端 LDAP 支持。目前，Courier maildrop 无法使用 TLS，但这实际上不是问题，因为 LDA 不需要知道任何用户密码。

#### 启用 Postfix LDAP 支持

Postfix 需要自己的公钥和私钥才能通过 TLS 访问 LDAP 服务器。你应该已经在第 17 章创建了密钥文件，因此可以重复使用它们。



要启用 LDAP 上的 TLS，必须在 `/etc/postfix/ldap` 中的所有 LDAP 查询配置文件里添加以下参数：

```
version = 3
tls_ca_cert_file = /usr/share/ssl/certs/cacert.pem
tls_cert = /etc/postfix/certs/postfix_public_cert.pem
tls_key = /etc/postfix/certs/postfix_private_key.pem
start_tls = yes
```

各参数的作用如下：

**version**
设置 LDAP 协议的版本。默认情况下，Postfix 使用版本 2，但 TLS 需要版本 3。

**tls_ca_cert_file**
指定 CA 证书。

**tls_cert**
指定 Postfix 的公钥证书。

**tls_key**
指定 Postfix 的私钥。

**start_tls**
启用 TLS。

#### 为 Courier IMAP 启用 LDAP 查询

要为 Courier IMAP 启用 LDAP over TLS，你需要遵循与 Postfix 不同的配置策略，因为 Courier 没有自己的 LDAP 客户端，而是使用 OpenLDAP 自带的客户端。你需要配置 OpenLDAP 客户端以使用 TLS，然后告诉 Courier IMAP 从 OpenLDAP 客户端请求 LDAP over TLS。
OpenLDAP 客户端配置文件通常是 `/etc/openldap/ldap.conf`。你需要添加以下 `TLS_*` 参数以启用 TLS 支持：

```
URI ldap://mail.example.com
BASE dc=example,dc=com
TLS_CACERT /usr/share/ssl/certs/cacert.pem
TLS_CERT /etc/openldap/certs/slapd_public_cert.pem
TLS_KEY /etc/openldap/certs/slapd_private_key.pem
TLS_REQCERT demand
```

这些参数与 Postfix 的类似：

**TLS_CACERT**
指定本章其余部分使用的 CA 证书。

**TLS_CERT**
指定客户端的公钥证书。

**TLS_KEY**
指定客户端的私钥。如果愿意，你可以重复使用 slapd 的证书和密钥。

**TLS_REQCERT**
指定请求服务器证书的策略。将其设置为 `demand` 以强制 TLS 或断开连接。

既然你已经向 OpenLDAP 客户端提供了证书和密钥信息，你只需告诉 Courier IMAP 在 `/usr/lib/courier-imap/etc/authldaprc` 文件中请求 LDAP over TLS：

```
LDAP_TLS	1
```

有了这最后一步，你就可以重启 Courier IMAP 并进行测试了。

#### 测试 TLS

你刚刚添加到配置中的 TLS 参数大大增加了复杂性，因此仔细测试非常重要。

- 1. 测试所有应用都依赖的核心——LDAP 服务器。测试 LDAP 服务器自身的客户端。
- 2. 如果测试成功，再测试 Postfix 看它能否连接。验证 Courier IMAP 是否能够使用 LDAP 客户端获取 SSL。

##### 测试 OpenLDAP 服务器

第一个测试是确保 OpenLDAP 服务器提供了 TLS 证书。实际上，没有简单的命令可以在端口 389（通常用于 LDAP over TLS）上检查这一点。我们将尝试访问端口 636（OpenLDAP 提供 SSL 的端口），看看 slapd 是否接受这些证书。

使用 `s_client` 工具按如下方式连接到服务器：

```
# openssl s_client -CAfile /usr/share/ssl/certs/cacert.pem -connect localhost:636
CONNECTED(00000003)
depth=1 /C=EX/ST=Examplia/L=Exampleton/O=Example Inc./OU=Certification Authority/\
	CN=mail.example.com/emailAddress=certmaster@example.com
verify return:1
depth=0 /C=EX/ST=Examplia/L=Exampleton/O=Example Inc./OU=LDAP services/\
	CN=mail.example.com/emailAddress=ldapmaster@example.com
verify return:1
---
Certificate chain
 0 s:/C=EX/ST=Examplia/L=Exampleton/O=Example Inc./OU=LDAP services/\
	CN=mail.example.com/emailAddress=ldapmaster@example.com
	i:/C=EX/ST=Examplia/L=Exampleton/O=Example Inc./OU=Certification Authority/\
	CN=mail.example.com/emailAddress=certmaster@example.com
 1 s:/C=EX/ST=Examplia/L=Exampleton/O=Example Inc./OU=Certification Authority/\
	CN=mail.example.com/emailAddress=certmaster@example.com
i:/C=EX/ST=Examplia/L=Exampleton/O=Example Inc./OU=Certification Authority/\
	CN=mail.example.com/emailAddress=certmaster@example.com
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIE DDCC A3wgAwIBAgIBANBgkqhkkiG9wBAQ FADCBsDELMAkGA1UEBhMC RVgx
ETAPBgNvBaAgTCEV4Y1wbGh1M RMwE QYDVQOQ HEwp FeGFtcGxldG9uMRUwE wYDVQQx
EwxFcGFt cGx1E 1Uy4xIDAEAgNVBasTFOnlcnRpZmljYXRpb24gQXV0aG9yaxR5
MRkwFwYDVQQDExBtY WLsmV4Y1wbGUuy29tMSUwIwYJKoZIhvcNAQkBFhZjXJO
bwFzdGVyQGV4Y1wbGUuy29tMB4XDTAO0MDcxMzEzNTAwN1wXDTAxMDcxMzEzNTQw
NlowgaYxCzAJBgNVBAYTAkVYMRQwEgYDVQQIEwtFeGFtcGxhbjEUMBIGA1UEBxQL
RXhhbXBsZS XRvb jEVMNBMGA1UEChMMRXhhbXBsZS ZSBbmMuMRwFAYDVQQLEw1MREFQ
IHNLcnZpY2VzMZwKfwYDVQQDExBtY WLsmV4Y1wbGUuy29tMSUwIwYJKoZIhvcN
AQkBFhZsZGFwWGFzdGVyQGV4Y1wbGUuy29tMIGfMA0GCSqGSIb3DQEBAQUAA4GN
ADCBiQKBgQDcPqYpn4qhI6ssAdPgu+Et2vzWsyHT/IT39mZ6Qqrh150a/eOAlZz
GmUKR/t/Wol28ygn/udpkHZiTUDjUC5ENF7kqk4vnx/4DpwmDmOjNg07JERoFL
cOJ1/KqZzAlTh2xKt1V8BQcdlFzd0xEq07MkxRipu7LyLo5q0kwIDAQABo4IB
PDCCATgwQVYDVR0OBI4EAEHxYdTT3BlblNTCBHZW5lmFo
ZWQgQ2VydGlmaWNhdGUvHQYDVROOBBYE FCKdRZg1sm4/1io2sltDiriyCE+KMIHd
BgNVHSMEGdUwgdKAFMNZ7/NorS6WpJQJZ2IhDno97iXoYG2pIGzMiGwMQswCQYD
VQQGEwJFDERMA8GA1UECBMlXhheXBsZS BsaWxEzARBGNVBacTCkV4Y1wbGV0b24x
FTATBgNVBAoTDVEV4Y1wbGUuY1wIGUgSW5jLjEGA1UECAwAQ4oVydGlmawNhZdIvB
dXRob3JpdHkxGTAxBGNVBAMTEGIhaWwuZXhhbXBsZS ZS5jb20xojAjBgkqhkiG9w0B
CQEWFNm1cnRtYXN0ZXJAZXhhbXBsZS ZS5jb22CAQwDQYJKoZIhvcNAQEEBQADgEA
AZCH5A23WdId0gNKd23Bz3HF+MyOf8fUxiCaQbLwoS72mjgB/03H7K969bU/te2
BeLOjifMo/vexXPMeajwzDnIKm/yJO7eNt85eeKciG6MZJvhuPvtp/RcSvArcas
HNqpmn70DAEFIRclHsfhsyAHwsTTr18UGndfL3Hetkw=
-----END CERTIFICATE-----
subject=/C=EX/ST=Examplia/L=Exampleton/O=Example Inc./OU=LDAP services/\
	CN=mail.example.com/emailAddress=ldapmaster@example.com
issuer=/C=EX/ST=Examplia/L=Exampleton/O=Example Inc./OU=Certification Authority/\
	CN=mail.example.com/emailAddress=certmaster@example.com
---
Acceptable client certificate CA names
/C=EX/ST=Examplia/L=Exampleton/O=Example Inc./OU=Certification Authority/\
	CN=mail.example.com/emailAddress=certmaster@example.com
---
SSL handshake has read 2402 bytes and written 352 bytes
---
New, TLSv1/SSLv3, Cipher is AES256-SHA
Server public key is 1024 bit
SSL-Session:
    Protocol  : TLSv1
    Cipher    : AES256-SHA
    Session-ID:
    21430E35213A797176B28B16BF24D20EC9019902B5B09FCEDDA0333682FD6F7D
    Session-ID-ctx:
    Master-Key:
    45636217FD3136A536CE62618DBC1CA92E6E0B1E773F75120632F761C289943BB\
    85F78369C622A0D78DB60726147465F
    Key-Arg   : None
    Krb5 Principal: None
    Start Time: 1089733870
    Timeout     : 300 (sec)
    Verify return code: 0 (ok)
---
QUIT
DONE
```

如果你得到返回码 0 (ok)，则证书检查通过。现在你可以测试是否能使用 LDAP 客户端通过 TLS 查询服务器。

##### 测试 OpenLDAP 客户端

要查看 OpenLDAP 客户端是否工作，尝试使用 `ldapsearch` 命令检索数据，如下所示：

```
# ldapsearch -ZZ -x -LLL "(mail=bamm@example.com)" userPassword
dn: ou=people,dc=example,dc=com
dn: ou=it,ou=people,dc=example,dc=com
dn: uid=bammbamm,ou=it,ou=people,dc=example,dc=com
userPassword:: YmFtbV9zZWNyZXQ=
```

这个 `ldapsearch` 命令特别有用，因为它读取了 `ldap.conf` 中的默认设置；请记住，Courier IMAP 的 TLS/LDAP 配置依赖于此。此外，此查询模拟了 Courier IMAP 的查询。`-ZZ` 选项强制 `ldapsearch` 使用 TLS。
如果此命令无法工作，请仔细检查你的 `ldap.conf` 文件和日志。

##### 测试 Postfix

要测试 Postfix 的 LDAP over TLS 支持，运行 `postmap` 命令查询目录中的已知收件人。以下是本章中的一个示例：

```
# postmap -q "bamm@example.com" ldap:/etc/postfix/ldap/local_recipients.cf
bammbamm
```

如果这不成功，看看在没有 TLS 支持的情况下是否工作。成功后，重新启用 TLS 设置，并在你的 Postfix LDAP 配置文件（例如 `/etc/postfix/ldap/local_recipients.cf`）中将 `debuglevel` 至少设置为 1，以便你可以仔细研究一些描述性的日志信息。

##### 测试 Courier IMAP

你刚刚在“测试 OpenLDAP 客户端”部分测试了 Courier IMAP 配置的一些基础部分。要验证一切是否正常，请连接到 IMAP 端口并像“测试 IMAP 服务器”部分那样登录。成功的登录如下所示：

```
# telnet mail.example.com 143
* OK [CAPABILITY IMAP4rev1 UIDPLUS CHILDREN NAMESPACE \
     THREAD=ORDEREDSUBJECT THREAD=REFERENCES SORT QUOTA \
```



# 强制验证发件人地址

一旦用户通过 SMTP 身份验证成功连接到 Postfix 服务器，他们就可以使用任何想要的发件人地址通过你的服务器转发邮件。如果你对用户的信任程度有限，可以使用 Postfix 2.1 中引入的 `reject_authenticated_sender_login_mismatch` 限制来强制验证发件人地址。其工作原理如下：

1. 用户使用用户名通过 SMTP 身份验证进行连接。
2. 当用户尝试发送邮件时，Postfix 提取信封发件人地址。
3. Postfix 在 `smtpd_sender_login_maps` 配置的映射中查找信封发件人。理想情况下，这是一个基于 LDAP 的映射。
4. 如果查找结果返回的用户名与 SMTP 身份验证时使用的用户名一致，Postfix 就接受该邮件。否则 Postfix 会拒绝该邮件。

# 创建 LDAP 映射

你已经在目录中拥有了 `smtpd_sender_login_maps` 映射所需的全部数据，因此复用它是合理的——不仅因为不需要额外的数据，还因为无需额外的维护工作。要设置该映射，请在 /etc/postfix/ldap 中创建一个新文件，并配置查询所需的参数。

当你要指定从 LDAP 服务器检索的属性作为用户名时，可以选择仅允许使用 *mail* 属性中的邮件地址，或者也允许发件人使用其别名（存储在 *maildrop* 属性中）。

假设你想创建一个同时允许两者的配置，查询文件名为 /etc/postfix/ldap/mail_from_login.cf。假设你已启用 TLS，完整的文件内容应如下所示：

```
version = 3
debuglevel = 0
server_host = ldap://mail.example.com
tls_ca_cert_file = /usr/share/ssl/certs/cacert.pem
tls_cert = /etc/postfix/certs/postfix_public_cert.pem
tls_key = /etc/postfix/certs/postfix_private_key.pem
tls_random_file = /dev/urandom
start_tls = yes
bind = yes
bind_dn = uid=postfix,ou=auth,dc=example,dc=com
bind_pw = Yanggt!
search_base = ou=people,dc=example,dc=com
query_filter = (|(mail=%s)(maildrop=%s))
result_attribute = mail
```

这里只有两个参数需要与 /etc/postfix/ldap 中的其他文件不同，即 query_filter 和 result_attribute。配置好查询映射文件后，在你的 main.cf 文件中设置 smtpd_sender_login_maps 参数，如下所示：

```
smtpd_sender_login_maps = ldap:/etc/postfix/ldap/mail_from_login.cf
```

# 配置 smtpd 限制

最后，通过在 main.cf 文件的限制列表中添加 reject_authenticated_sender_login_mismatch 参数，完成将发件人限制为使用其自身邮件地址的所有配置：

```
smtpd_recipient_restrictions =
    permit_mynetworks
    reject_authenticated_sender_login_mismatch
    permit_sasl_authenticated
    reject_unauth_destination
```

**注意** *此限制仅适用于已进行身份验证的用户，而不适用于其他人。因此，你信任网络中的用户可以使用任意身份发送邮件。此外，来自互联网其他地方的邮件仍然可以正常接收。*

# 测试 smtpd 限制

要测试你的新配置，首先检查映射是否正常工作。使用 postmap 匹配一个普通收件人，如下所示：

```
# postmap -q "bamm@example.com" ldap:/etc/postfix/ldap/mail_from_login.cf
bambamm
```

如果你允许将别名作为发件人地址，请使用 postmap 查询别名：

```
# postmap -q "postmaster@example.com" ldap:/etc/postfix/ldap/mail_from_login.cf
bambamm
```

如果以上步骤都正常，最后需要测试的是一个实际的 SMTP 会话。首先，为连接的第一阶段准备一个 base64 编码的身份验证字符串：

```
# perl -MMIME::Base64 -e \
'print encode_base64("bamm\@example.com\0bamm\t@example.com\0bamm_secret");'
YmFtbUBIeGFtcGxlLmNvbQBiYW1tQGV4YW1wbGUuY29tAGJhbW1fc2VjcmV0
```

现在，从远程主机连接到你的 Postfix 服务器，并使用此字符串进行身份验证：

```
# telnet mail.example.com 25
220 mail.example.com ESMTP Postfix
EHLO client.example.com
250-mail.example.com
250-PIPELINING
250-SIZE 10240000
250-VRFY
250-ETRN
250-AUTH PLAIN LOGIN CRAM-MD5 DIGEST-MD5
250-AUTH=PLAIN LOGIN CRAM-MD5 DIGEST-MD5
250 8BITMIME
AUTH PLAIN YmFtbUBIeGFtcGxlLmNvbQBiYW1tQGV4YW1wbGUuY29tAGJhbW1fc2VjcmV0
235 Authentication successful
```

现在，尝试以另一个用户身份发送邮件（请注意，你使用的是 Bamm Bamm 的身份进行验证）：

```
MAIL FROM: <rubble@example.com>
250 Ok
RCPT TO: <wietse@porcupine.org>
553 <rubble@example.com>: Sender address rejected: not owned by user
bamm@example.com
```

Postfix 在 RCPT TO 阶段检测到了不匹配，因为这正是 smtpd_recipient_restrictions 参数生效的地方。你还应该尝试以真实用户身份发送邮件。如果测试通过，就不需要做其他操作了。配置完成，尽情使用吧！

# 20

# 在 CHROOT 环境中运行 POSTFIX

> > chroot 功能只是增加了抵御入侵的又一道屏障；这道屏障只有在主机已经以强化配置运行时才有意义。——Wietse Venema

在 chroot 监狱中运行 Postfix 可以将其与操作系统的整个目录结构隔离开来。其目的是保护系统免受入侵者突破 Postfix 防线后的进一步危害。为了使用此功能，你必须将最少数量的文件、应用程序和其他资源锁定到 chroot 监狱目录中。

设置 chroot 监狱不需要外部程序。发行版中包含用于设置适当 chroot 环境的辅助脚本。本章既描述了 chroot 环境的理论，也提供了一个 SASL/TLS 示例，展示 chroot 与 Postfix 实际如何协同工作。

Postfix 附带的 chroot 脚本可以在源代码树的 examples/chroot-setup 目录中找到。如果你使用预打包的 Postfix 二进制文件，打包者可能已添加了一些脚本来保持 chroot 监狱目录的内容与外部文件系统同步。设置 chroot 监狱的可靠步骤如下：

1. 在不使用 chroot 的情况下让服务正常运行。
2. 逐一将 Postfix 守护进程转换为 chroot 设置。

如果你按照此步骤操作，可以轻松识别在 chroot 环境中出问题的守护进程，并相应地调整监狱目录的内容。

## CHROOT 监狱如何工作？

想象一个窃贼破窗进入你的房子，但这扇窗户属于一个高安全性房间。这个房间不仅没有任何有价值的物品，而且房间内的物品也无法帮助窃贼进一步进入房子内部。窃贼别无选择，只能放弃。为了使这一设计奏效，建筑师必须确保只有绝对必要的物品才放置在这个高安全性房间内。此外，这些物品必须妥善固定，以免被用于对付高安全性房间本身。Unix 系统下的 chroot 监狱与这个高安全性房间非常相似。

## CHROOT 设置的基本原则

以下是 chroot 设置的基本原则：

**使用运行应用程序所需的最低权限**
用户的权限越大，对系统造成的危害就越大。特别是 root 用户以及以 root 身份运行的程序可以相当容易地突破 chroot 监狱。因此，在 chroot 监狱中运行的程序不应使用超级用户权限，而应使用完成任务所需的最低权限级别。

**正确地降级权限**
在低编号端口（如端口 25）上提供服务的应用程序可能需要以 root 身份启动以获取端口访问权限。但是，在应用程序获取所需资源后，应该正确地放弃特殊的访问权限。

**保持监狱小而精简**
在 chroot 监狱中只保留最基本的文件。文件越少，为入侵者提供可利用资源的可能性就越小。

**确保监狱中的文件由 root 拥有且仅 root 可写**
在 chroot 监狱中运行的应用程序不应能够修改监狱内的文件。将所有权和写入权限更改为仅 root 所有。



### 从外部链接配置文件

从 jail 内部指向外部文件的符号链接，对于在 jail 内运行的系统将无法工作。某些系统会在被 jail 的守护进程和从用户模式运行的其他实用程序之间共享配置文件。这要求所有守护进程（无论是在 jail 内还是 jail 外）都能访问该配置文件。与其重新构建这些实用程序以使用特殊路径（如 /chroot/named/etc/named.conf），你可以创建一个*从 jail 外部指向内部*的符号链接，如下例所示：

```
# ln -s /chroot/named/etc/named.conf /etc/named.conf
```

这允许大多数工具正常运行，但在编辑如 /etc/named.conf 这样的文件时，你需要更加小心，因为当你这样做时，你是在影响一个被 jail 的系统。

### 技术实现

守护进程会自行进行 chroot 并放弃特权。这使它们能够在进入 jail 之前访问 /etc/postfix 文件（和打开的映射）。

`chroot()` 系统调用会改变进程（在进入 chroot jail 后）对文件系统的感知方式。以下是其工作原理：

1.  `master` 守护进程调用 `chdir(queue_directory)`。
2.  `master` 守护进程启动其他 Postfix 守护进程，并告诉每个进程是否应该更改文件系统根目录或放弃其特权。

除非在非常有限的情况下，否则不可能逃脱这个 jail。

## chroot 如何影响 Postfix？

当你在 chroot jail 中运行 Postfix 时，它会影响 Postfix 查看文件系统的方式。假设你 chroot 到了 /var/spool/postfix。虽然任何其他应用程序可能可以看到 /var/spool/postfix（队列目录）以及系统上的其他所有内容，但一旦 Postfix 守护进程启动并 chroot，它们就认为 /var/spool/postfix 是 /。它们无法访问 /var/spool/postfix 之外的任何其他内容。

这可能要求你将几个 chroot 守护进程无法访问的文件复制到 Postfix jail 中：

### 二进制文件（守护进程）

你不需要将守护进程复制到 chroot jail 中，因为它们是由未被 chroot 的 `master` 守护进程启动的。

### 二进制文件所需的库

程序在进入 jail 之前会加载库，因此你不需要将它们复制到 jail 中。

### 映射

程序在进入 jail 之前会打开静态映射。但是，你可能需要在 chroot jail 中创建一个套接字以用于数据库驱动的映射（请参见此列表中的套接字点）。

### 配置文件

守护进程在进入 jail 之前会读取配置文件。无需将它们复制到 jail 中。

#### 套接字

套接字文件，例如 mysql 套接字或 SASL 套接字，需要可以被 jail 内的守护进程访问。请记住，MySQL 客户端库可能会在诸如 /var/run/mysql.socket 的位置查找套接字，因此你需要将其放在诸如 queue_directory/var/run/mysql.socket 的位置。

### 库所需的文件

C 库需要查看诸如 /etc/resolv.conf 和 /etc/localtime 等文件才能正常工作。你需要在 /var/spool/postfix 中安装这些文件的副本。

### chroot 的辅助脚本

Postfix 在源代码树的 examples/chroot-setup 目录中附带了几个辅助脚本。这些脚本可协助你为特定的操作系统设置 chroot jail。

当你以 chroot 方式运行 Postfix 时，它会检查基本所需文件（如 /var/spool/postfix/etc/resolv.conf）是否存在于 chroot jail 中并且是最新的。如果 jail 内外的文件不同步，Postfix 会将警告写入日志文件。你务必重视这些警告并采取行动修复不一致之处。

### chrooted 守护进程

由于 master 守护进程启动其余的 Postfix 守护进程，因此由它来告诉守护进程是否以 chroot 方式运行。你在 /etc/postfix/master.cf 中控制 chroot 调用。

### 启用 chroot

要以 chroot 方式运行守护进程，你需要在 master.cf 文件中识别调用它的服务。检查 master.cf 中的 chroot 列以查找守护进程的当前 chroot 状态。Postfix SOURCE 源代码中所有守护进程的默认设置为 `n`，但某些发行版在其 Postfix 软件包中会更改此设置。也就是说，在标准安装中，没有任何守护进程以 chroot 方式运行。要更改它，请将 chroot 选项从 `n` 或 `-` 更改为 `y`。

例如，如果你希望以 chroot 方式运行 smtpd 守护进程，你的配置文件可能如下所示：

```
# ===============================================
# service type private unpriv chroot wakeup maxproc command + args
# (yes)   (yes)  (yes)  (never) (100)
# ===============================================
smtp      inet  n       -       y       -       -       smtpd
#smtps    inet  n       -       n       -       -       smtpd
# -o smtpd_tls_wrappermode=yes -o smtpd_sasl_auth_enable=yes
...
pickup    fifo  n       -       n       60      1       pickup
cleanup   unix  n       -       n       -       0       cleanup
...
```

请注意，smtp 服务的 chroot 列条目已更改为 `y`。在你重新加载 Postfix 后，master 守护进程将以此 chroot 方式运行此服务。

### chroot 的限制和任务委派

master.cf 中的文档指出，你可以以 chroot 方式运行几乎任何守护进程，“除了 pipe、virtual 和 local 守护进程”：

-   **pipe**
    pipe 守护进程生成外部程序，这些程序通常位于 Postfix 队列目录之外，因此通常需要访问队列目录之外的文件。

-   **local**
    local 守护进程负责本地投递，需要能够访问用户主目录。以 chroot 方式运行 local 守护进程没有太大意义，因为这意味着主目录位于 /var/spool/postfix 下（在 chroot jail 内部），入侵者可能访问它们。

-   **virtual**
    virtual 守护进程负责本地投递，就像 local 守护进程一样。反对以 chroot 方式运行 local 守护进程的理由同样适用于此守护进程。

当使用 chroot 环境时，其他守护进程可能需要使用 proxymap 守护进程来访问配置数据。例如，如果一个被 chroot 的 SMTP 服务器需要访问系统 passwd 文件以拒绝不存在的本地地址的邮件，在 chroot jail 中维护 passwd 文件的副本是不切实际的，因为这将破坏以 chroot 方式运行 Postfix 的整个初衷。

为了将安全相关的映射保持在 jail 之外，你可以使用此配置参数将查找委派给 proxymap 守护进程（同样，不以 chroot 方式运行）：

```
local_recipient_maps = proxy:unix:passwd.byname $alias_maps
```

请记住，因为 proxymap 穿过了 jail 的屏障，所以 proxymap 不能代理在安全相关上下文中使用的映射。

### chroot 的库、配置文件和其他文件

许多程序需要外部文件才能正确运行。这些文件包括：

-   库和其他共享对象
-   配置文件
-   其他文件，如套接字设备

有几种方法可以找出程序需要哪些文件。要查找共享库依赖项，你可以使用大多数 Unix 变体上的 ldd 或 chatr。然而，对于标准的 Postfix 安装，这不会成为一个问题，因为所有守护进程都是在进入 chroot jail 之前启动并加载其库的。

要找出需要哪些配置文件，请使用诸如 strace（在 Linux 上）、truss（在 Solaris 上）或 ktrace（在其他 Unix 变体上）之类的程序。使用 strace 的一种方法是像这样启动程序：

```
# strace -o ouputfile program
```

然后检查输出文件中的 open() 调用：

```
# grep open outputfile | grep ENOENT
open("/etc/ld.so.preload", O_RDONLY)    = -1 ENOENT (No such file or directory)
open("/usr/share/locale/C/libdst.cat", O_RDONLY) = -1 ENOENT (No such file or directory)
open("/usr/share/locale/C/LC_MESSAGES/libdst.cat", O_RDONLY) = -1 ENOENT (No such file or directory)
open("/usr/share/locale/C/libdst.cat", O_RDONLY) = -1 ENOENT (No such file or directory)
open("/usr/share/locale/C/LC_MESSAGES/libdst.cat", O_RDONLY) = -1 ENOENT (No such file or directory)
open("/usr/share/locale/C/libisc.cat", O_RDONLY) = -1 ENOENT (No such file or directory)
open("/usr/share/locale/C/LC_MESSAGES/libisc.cat", O_RDONLY) = -1 ENOENT (No such file or directory)
open("/usr/share/locale/C/libisc.cat", O_RDONLY) = -1 ENOENT (No such file or directory)
open("/usr/share/locale/C/LC_MESSAGES/libisc.cat", O_RDONLY) = -1 ENOENT (No such file or directory)
open("/usr/share/locale/C/libdns.cat", O_RDONLY) = -1 ENOENT (No such file or directory)
open("/usr/share/locale/C/LC_MESSAGES/libdns.cat", O_RDONLY) = -1 ENOENT (No such file or directory)
open("/usr/share/locale/C/libdns.cat", O_RDONLY) = -1 ENOENT (No such file or directory)
open("/usr/share/locale/C/LC_MESSAGES/libdns.cat", O_RDONLY) = -1 ENOENT (No such file or directory)
```



**注意** 请记住，一个程序在找到正确的配置文件之前，可能会尝试打开多个版本的配置文件。

或者，你也可以将 `strace` 附加到正在运行的进程上，以查看它正在尝试做什么。例如，如果你想查看主守护进程正在做什么，可以尝试类似这样的命令：

```
# ps auxwww|grep master
root    9004  0.0  0.3 3452  940 ? S 07:49 0:00 /usr/lib/postfix/master
# strace -p 9004
Process 9004 attached - interrupt to quit
select(76, [10 11 12 15 17 18 21 23 24 26 27 29 30 32 33 35 36 38 39 41 42 44 45 47 48 50 51 53 54 56 57 59 60 62 63 65 66 68 69 71 72 74 75], [], [10 11 12 15 17 18 21 23 24 26 27 29 30 32 33 35 36 38 39 41 42 44 45 47 48 50 51 53 54 56 57 59 60 62 63 65 66 68 69 71 72 74 75], {22, 790000} <unfinished ...>
Process 9004 detached
```

### 克服 chroot 限制

Postfix 源代码发行版中（位于 `examples/chroot-scripts`）用于帮助你在 chroot 监狱中设置环境的脚本，也可以告诉你哪些系统文件可能需要复制到 chroot 监狱中，例如 C 库所需的时区文件。以下是所需文件的概览。

#### DNS

C 库需要某些文件来正确实现名称解析；例如，在 Linux 系统上，你需要 `/etc/resolv.conf`、`/etc/nsswitch.conf` 和 `/etc/hosts`。这些文件需要位于 chroot 监狱内，辅助脚本可以为你复制它们。

#### 时间设置

如果你发现 Postfix 守护进程产生的日志时间偏差了几个小时，你需要将时区信息（`/etc/localtime`）复制到 chroot 监狱中。

#### 套接字

你可以轻松配置 Postfix 和 `saslauthd` 在 Postfix chroot 环境中工作。你只需为 `saslauthd` 的套接字配置不同的路径。

在 Postfix chroot 监狱中（通常是 `/var/spool/postfix`），首先创建所有必需的 `run_path` 子目录：

```
# mkdir /var/spool/postfix/var
# mkdir /var/spool/postfix/var/run
# mkdir /var/spool/postfix/var/run/saslauthd
# chmod 750 /var/spool/postfix/var/run/saslauthd
# chgrp postfix /var/spool/postfix/var/run/saslauthd
```

现在，在 `/usr/lib/sasl/smtpd.conf` 中添加 `saslauthd_path` 参数，该参数告知被 chroot 的 `smtpd` 在何处查找套接字。去掉通往监狱的路径（即，省略 `/var/spool/postfix`），并提供 `run_path` 的路径，包括套接字名称（`mux`）作为其值：

```
saslauthd_path: /var/run/saslauthd/mux
```

最后，使用 `-m` 选项启动 `saslauthd`，该选项定义了创建套接字的位置。提供它在监狱外看到的完整路径：

```
# /usr/sbin/saslauthd -m /var/spool/postfix/var/run/saslauthd/mux -a shadow
```

这样，即使 Postfix 在 chroot 环境中运行，两个应用程序也能使用同一个套接字进行通信。

## 调优 POSTFIX

本书的这一部分提供了关于如何提高服务器性能的提示。从常见问题（如 DNS 缓存和成为开放中继）开始，我们逐步深入到高级概念，包括如何避免无法投递的邮件弹回以及设置专用传输。你可以使用黑名单来减少邮件流入，Postfix 2.1 的实验性速率限制功能也值得关注。

**远程客户端并发与请求速率限制**

第 21 章向你展示了一项限制客户端连接速率的新功能。这是一项用于保护 Postfix 免受 SMTP 客户端同时淹没 `smtpd` 守护进程的过多连接的对策。

**性能调优**

Postfix 很快，但有时你可以调整它使其变得更快。如果你的 Postfix 性能没有达到预期，你应该阅读第 22 章。

### 远程客户端并发与请求速率限制

![](img/852c79f689feb77c5fde686b993808b1_407_0.png)

Postfix 2.1 和 2.2 实现了远程客户端并发和速率限制。速率限制是一种用于保护 Postfix 免受 SMTP 客户端同时淹没 `smtpd` 守护进程的过多连接的对策。本章说明了速率限制有用的几个实例，并向你展示如何配置它。

#### 速率限制的基础知识

即使是一个精心调优的 Postfix 安装，一次也只能处理有限数量的电子邮件流量。服务器的容量取决于磁盘 I/O 吞吐量、CPU 速度以及连接到 Postfix 的任何病毒扫描器的速度等参数。在 Postfix 2.1 之前，单个客户端可能使用所有可用的 `smtpd` Postfix 服务器进程，从而阻止所有其他尝试投递邮件的客户端。

硬件限制、客户端耗尽连接以及复杂的配置，足以证明限制传入邮件量是合理的。然而，在其他情况下，速率限制可以防止邮件延迟或以其他方式减轻对 Postfix 的不利影响：

**病毒和蠕虫爆发**

在网络上蔓延的新病毒和蠕虫通常会尽快地尝试传播自身。速率限制通过节流传播速度来减慢恶意软件的传播。

**邮件炸弹**

邮件炸弹是大量、连续的邮件突发，通常从单个系统发送到你的系统。通常这是恶意行为，但也可能是意外发生的。（例如，我们见过一个防病毒产品为每个受感染的文件发送一条消息——当这种情况发生在一个彻底受感染的系统上时，你的邮件服务器可能会每分钟收到超过 100 条消息而被淹没。）

**失控的客户端**

“失控的客户端”这个术语是一个概括，包括病毒或蠕虫爆发以及邮件炸弹；它指的是任何失控的、向你的系统发送连续邮件流的客户端。客户端不一定是恶意的——问题可能是由编程或配置错误引起的。

**来自开放代理的垃圾邮件**

开放代理是垃圾邮件发送者用来掩盖其邮件来源的流行工具。当速率限制限制来自开放代理的消息时，Postfix 会以临时错误代码拒绝来自开放代理的传入消息。由于代理本身没有排队机制，它不会重试投递，因此来自开放代理的大量垃圾邮件不会进入你的系统。

要使用速率限制，你必须收集统计数据并调整几个参数，以影响客户端可以向 `smtpd` 守护进程进行连续和同时连接的数量。你将在以下部分中看到如何操作。

#### 收集速率统计信息

在开始限制客户端连接之前，你必须知道哪些客户端连接以及它们在正常操作期间发起多少连续和同时连接。`anvil` 守护进程为你跟踪客户端，维护连接统计数据并记录最大连接数和速率。

> **注意** *记录客户端连接统计信息的用途超出了速率限制的实施范围。例如，你可以将此信息读取到日志监视程序中，该程序随后更新防火墙规则以阻止这些失控的客户端。速率限制对 Postfix 来说相对较新，因此在撰写本文时，还没有流行的程序能做到这一点。*

##### 运行 anvil 守护进程

与其他 Postfix 守护进程一样，`anvil` 由 `master` 守护进程控制。
虽然 `anvil` 默认启用，但你应该检查你的 `master.cf` 文件，
以确保配置 `anvil` 的行没有被注释掉：

```
# ==================================================================
# service type  private unpriv  chroot  wakeup  maxproc command + args
# (yes)   (yes)   (yes)   (never)  (100)
# ==================================================================
anvil       unix  -       -       n       -        1       anvil
```

`anvil` 守护进程按需启动，它会以固定的时间间隔将收集到的所有数据写入邮件日志。这些日志消息如下所示：

```
Dec 20 01:19:16 mail postfix/anvil[8991]: statistics: max connection count 4
for (10.0.0.1:smtp:216.129.165.190) at Dec 20 01:18:35
Dec 20 01:29:16 mail postfix/anvil[8991]: statistics: max connection rate 9/
60s for (10.0.0.1:smtp:62.243.72.19) at Dec 20 01:22:11
Dec 20 01:29:16 mail postfix/anvil[8991]: statistics: max connection count 2
for (10.0.0.1:smtp:62.243.72.19) at Dec 20 01:22:09
Dec 20 01:39:16 mail postfix/anvil[8991]: statistics: max connection rate 3/
60s for (10.0.0.1:smtp:146.82.138.6) at Dec 20 01:37:04
Dec 20 01:49:16 mail postfix/anvil[8991]: statistics: max connection rate 2/
60s for (10.0.0.1:smtp:218.18.32.248) at Dec 20 01:46:35
Dec 20 01:49:16 mail postfix/anvil[8991]: statistics: max connection count 2
for (10.0.0.1:smtp:218.18.32.248) at Dec 20 01:46:35
Dec 20 01:59:16 mail postfix/anvil[8991]: statistics: max connection rate 3/
60s for (10.0.0.1:smtp:146.82.138.6) at Dec 20 01:50:58
Dec 20 01:59:16 mail postfix/anvil[8991]: statistics: max connection count 2
for (10.0.0.1:smtp:171.67.16.117) at Dec 20 01:55:33
Dec 20 02:09:16 mail postfix/anvil[8991]: statistics: max connection rate 2/
60s for (10.0.0.1:smtp:216.136.204.119) at Dec 20 02:03:38
Dec 20 02:19:16 mail postfix/anvil[8991]: statistics: max connection rate 2/
60s for (10.0.0.1:smtp:63.161.42.51) at Dec 20 02:09:29
Dec 20 02:19:16 mail postfix/anvil[8991]: statistics: max connection count 2
for (10.0.0.1:smtp:130.149.17.13) at Dec 20 02:11:52
```

#### 更改 anvil 日志间隔

默认情况下，`anvil` 每十分钟将统计报告写入邮件日志，
或者在守护进程终止时（例如，如果你重新加载 Postfix，或者守护进程在 `max_idle` 秒后自行终止）。如果你需要增加或
减少此间隔，请在 `main.cf` 中设置 `client_connection_status_update_time` 参数：

```
client_connection_status_update_time = 10m
```

你的更改在重新加载 Postfix 后立即生效。



> 注意 此日志间隔是一个独立于 anvil 守护进程内部运行的诊断工具。缩短间隔并不会导致 anvil 更频繁地收集统计数据；Postfix 程序通过进程间通信访问所有当前的 anvil 数据。它们不会查看日志文件。

### 限制客户端连接频率

默认情况下，Postfix 不对客户端可以连续连接的次数施加限制。因此，如果你不更改任何设置，客户端可以随心所欲地连接和断开，这会导致 smtpd 浪费宝贵资源来执行 DNS 查询、TLS 握手等操作。

要实施客户端连接频率限制，Postfix 必须在特定时间段内计算连接数。此间隔称为速率时间单位，你可以使用 `client_connection_rate_time_unit` 参数来定义它。默认值为一分钟（60 秒）：

```
client_connection_rate_time_unit = 60s
```

现在，你可以使用 `smtpd_client_connection_rate_limit` 参数来设置在此速率时间单位内允许单个客户端进行的连接次数上限。例如，以下设置结合前面的默认速率时间单位，允许一个客户端在 60 秒内最多连接 30 次：

```
smtpd_client_connection_rate_limit = 30
```

### 测试客户端连接频率限制

测试速率限制最简单的方法是应用设置，然后观察几天的日志。错误的设置不会导致你丢失邮件或损害你的系统，因为 Postfix 会使用临时错误代码拒绝被限速的客户端。一个配置正确的客户端会重试投递；例如，Postfix 默认会重试五天（参见 `maximal_queue_lifetime` 参数）。

如果你想立即测试，请尝试以下步骤：

1.  使用 smtp-source 等程序生成大量邮件流量。
2.  从一个未被豁免速率限制的 IP 地址发送邮件。

> 注意 在测试期间，你也可以将 `client_connection_status_update_time` 参数减少到一分钟，以便更频繁地收集连接统计数据。

要执行测试，请在你的 `master.cf` 文件中使用以下设置，然后重新加载服务器配置：

```
smtpd_client_event_limit_exceptions=
client_connection_rate_time_unit = 60s
smtpd_client_connection_rate_limit = 1 ②
client_connection_status_update_time = 1m ③
```

1.  将此参数设置为空指定所有客户端都受速率限制；仅将此设置用于测试。
2.  此限制被人为地设置得很低，仅用于测试目的。你肯定不希望邮件服务器只允许客户端每分钟连接一次。
3.  此设置每分钟生成一次统计日志，这样你就不用等待十分钟才能看到状态报告。同样，仅将此用于测试。

现在你需要生成足够的流量来触发速率限制器。在你的 Postfix 服务器上像这样使用 smtp-source 命令：

```
$ smtp-source -m 10 -f sender@example.com -t recipient@example.com 127.0.0.1:25
```

> **注意**
> *如果 smtp-source 不是你的发行版的一部分，请从 Postfix 源文件中获取它。*

前面的命令通过 127.0.0.1（本地主机）上的 SMTP 服务器，从 sender@example.com 向 recipient@example.com 发送十封测试邮件。因为你将每个客户端的限制设置为每 60 秒一次连接，这个命令很容易超过该限制。

你将看到 smtp-source 输出以下错误：

```
smtp-source: fatal: bad startup: 450 Too many connections from 127.0.0.1
```

此外，你的日志将显示如下内容：

```
Jan  9 09:04:16 mail postfix/smtpd[26530]: connect from localhost[127.0.0.1]
Jan  9 09:04:16 mail postfix/smtpd[26530]: 12AA515C06F: client=localhost[127.0.0.1]
Jan  9 09:04:16 mail postfix/smtpd[26530]: disconnect from localhost[127.0.0.1]
Jan  9 09:04:16 mail postfix/smtpd[26530]: connect from localhost[127.0.0.1]
Jan  9 09:04:17 mail postfix/smtpd[26530]: warning: Too frequent connections: 2 from 127.0.0.1 for service localhost:smtp
Jan  9 09:04:17 mail postfix/smtpd[26530]: disconnect from localhost[127.0.0.1]
```

这里是另一个示例，其中 `smtpd_client_connection_rate_limit` 参数被设置为 30。Postfix 以 450 状态码拒绝所有超过该最大允许频率的客户端，断开连接，并生成一条包含客户端名称和地址以及守护进程名称的警告：

```
Dec 20 02:39:03 mail postfix/smtpd[18431]: warning: Too frequent connections: 31 from 81.199.6.44 for service 10.0.0.1:smtp ①
Dec 20 02:39:04 mail postfix/smtpd[17840]: warning: Too frequent connections: 32 from 81.199.6.44 for service 10.0.0.1:smtp
Dec 20 02:39:04 mail postfix/smtpd[17878]: warning: Too frequent connections: 33 from 81.199.6.44 for service 10.0.0.1:smtp
...
Dec 20 02:39:15 mail postfix/smtpd[18440]: warning: Too frequent connections: 65 from 81.199.6.44 for service 10.0.0.1:smtp
Dec 20 02:39:15 mail postfix/smtpd[18432]: warning: Too frequent connections: 66 from 81.199.6.44 for service 10.0.0.1:smtp
Dec 20 02:39:16 mail postfix/anvil[8991]: statistics: max connection rate 72/60s for (10.0.0.1:smtp:81.199.6.44) at Dec 20 02:39:15
```

1.  在 81.199.6.44 上运行的客户端超过了每分钟 30 次连接的限制，导致日志中出现 "Too frequent connections" 警告。
2.  这个特定客户端（81.199.6.44）在 60 秒内建立了 72 次连接，从而创造了连接速率记录，正如 anvil 在此处报告的那样。

### 限制同时客户端连接数

默认情况下，每个客户端的同时连接数限制为默认进程限制的一半。因此，两个客户端就可以占据 Postfix 允许运行的所有 smtpd 进程。`smtpd_client_connection_count_limit` 参数控制每个客户端的同时连接数。例如，`main.cf` 中的以下配置设置将一个客户端限制为 25 个并发连接：

```
smtpd_client_connection_count_limit = 25
```

> **注意**
> *smtpd 的进程限制或 `default_process_limit` 参数应远大于 `smtpd_client_connection_count_limit`；否则，一个客户端可能会占用所有可用的 smtpd 进程。*

#### 测试同时客户端连接限制

与连接频率限制的情况一样，测试并发会话限制最简单的方法是应用设置并观察几天的日志。但是，如果你想立即测试，请使用 `smtp-source` 命令从一个未被豁免速率限制的 IP 地址生成大量同时连接。

在测试期间，你可能需要将 `client_connection_status_update_time` 减少到一分钟。

要执行测试，请在你的 `master.cf` 文件中按如下方式设置速率限制参数，然后重新加载配置：

```
smtpd_client_connection_limit_exceptions = ①
client_connection_rate_time_unit = 60s
smtpd_client_connection_count_limit = 1 ②
client_connection_status_update_time = 1m ③
```

1.  所有客户端都受到速率限制；仅将此用于测试。
2.  此限制设置得极低；仅将此用于测试。你不想使用一个只允许一个客户端每 60 秒连接一次的邮件服务器。
3.  每分钟生成一次日志报告，这样你就不用等待十分钟才能看到状态报告；仅将此用于测试。

你可以使用 smtp-source 命令打开几个同时连接。尝试在你的 Postfix 服务器上运行此命令：

```
$ smtp-source -s 10 -m 10 -f sender@example.com -t recipient@example.com 127.0.0.1:25
```

`-m 10` 选项表示发送十封测试邮件，`-s 10` 选项指定十个同时 SMTP 会话。在每个客户端限制为一次连接的情况下，你应该很容易触发限制，并从 smtp-source 生成以下错误消息：

```
smtp-source: fatal: bad startup: 450 Too many connections from 127.0.0.1
```

日志应显示类似以下内容：

```
Jan  9 09:14:15 mail postfix/smtpd[28438]: warning: Too many connections:
 2 from 127.0.0.1 for service localhost:smtp
Jan  9 09:14:15 mail postfix/smtpd[28438]: disconnect from localhost[127.0.0.1]
Jan  9 09:14:15 mail postfix/smtpd[28437]: warning: Too many connections:
 2 from 127.0.0.1 for service localhost:smtp
Jan  9 09:14:15 mail postfix/smtpd[28437]: disconnect from localhost[127.0.0.1]
Jan  9 09:14:15 mail postfix/smtpd[28439]: warning: Too many connections:
 3 from 127.0.0.1 for service localhost:smtp
Jan  9 09:14:15 mail postfix/smtpd[28439]: disconnect from localhost[127.0.0.1]
Jan  9 09:14:15 mail postfix/smtpd[28440]: warning: Too many connections:
 4 from 127.0.0.1 for service localhost:smtp
Jan  9 09:14:15 mail postfix/smtpd[28440]: disconnect from localhost[127.0.0.1]
```

对于接下来的日志消息，`smtpd_client_connection_count_limit` 被设置为 25。与频率限制的情况类似，Postfix 会向同时连接过多的客户端发送 450 状态码，断开连接，并记录一条包含客户端名称和地址的警告：

```
Dec  3 09:12:53 mail postfix/smtpd[19883]: warning: Too many connections:
 26 from 213.165.64.165 for service 10.0.0.1:smtp ❶
Dec  3 09:12:53 mail postfix/smtpd[19884]: warning: Too many connections:
 27 from 213.165.64.165 for service 10.0.0.1:smtp
…
Dec  3 09:13:15 mail postfix/smtpd[19894]: warning: Too many connections:
 35 from 213.165.64.165 for service 10.0.0.1:smtp
…
Dec  3 09:16:47 mail postfix/anvil[7958]: statistics: max connection count
 37 for (10.0.0.1:smtp:213.165.64.165) at Dec  3 09:12:3 ❷
```

1. 213.165.64.165 超过了 25 次连接的限制，导致日志中出现 "Too many connections" 警告。
2. 213.165.64.165 针对 smtpd 建立了 37 次连接，从而创造了记录。



### 客户端限制豁免

你可以使用 `smtpd_client_connection_limit_exceptions` 参数，将授权的主机和网络从本章介绍的客户端限制中排除。该参数的表示法包括网络/网络掩码表达式、主机名和域名。

默认情况下，Postfix 会为 `mynetworks` 中的所有主机提供客户端限制豁免。如果你希望使用更严格的设置，可以查阅 `sample-smtpd.cf`、`smtpd(8)` 和 `anvil(8)`。

以下示例允许 `$mynetworks` 中的主机、子网 `10.45.207.0/24` 以及域名 `example.com` 无限制地进行连接：

```
smtpd_client_connection_limit_exceptions =
    $mynetworks,
    10.45.207.0/24,
    .example.com
```

## 性能调优

Postfix 开箱即用的速度就很快，但和其他软件包一样，你通常可以通过调优让它运行得更快。此外，在某些情况下，Postfix 的性能可能不如预期，这可能是由于服务器系统的硬件或软件限制，或者其他不利条件，例如大量垃圾邮件或无法投递的邮件涌入。

本章将向你展示如何发现和分析最常见的性能问题。

### 基础增强

我们将首先介绍一些基础的调整，这些调整可能仍然不那么明显。将此处的建议视为解决或避免简单问题的检查清单。最重要的是，请记住许多性能问题实际上是由有缺陷的设置引起的，例如不良的 `/etc/resolv.conf` 文件。以下各点没有特定顺序；它们同等重要。

#### 加快 DNS 查询速度

Postfix 会进行大量 DNS 查询，因为 SMTP 需要查找 MX 和 A 记录。此外，Postfix 的许多限制功能也使用 DNS 查询来验证客户端主机名或执行黑名单查询。因此，你的服务器能够快速查询 DNS 记录至关重要，特别是如果你有大量的流量。

##### 测试 DNS 查询

DNS 名称解析最常见的问题是查询耗时过长。你可以使用 dig 命令执行 DNS 查询，并显示有关查询执行情况的详细信息：

```
$ dig www.example.com
; <<>> DiG 9.2.3rc4 <<>> www.example.com
;; global options:  printcmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 48136
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0
;; QUESTION SECTION:
;www.example.com.                IN      A
;; ANSWER SECTION:
www.example.com.        172800  IN      A       192.0.34.166
;; Query time: 174 msec
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Mon Oct  6 09:40:52 2003
;; MSG SIZE  rcvd: 49
```

在此示例中，查询耗时 174 毫秒。现在，让我们再次运行该查询：

```
$ dig www.example.com
; <<>> DiG 9.2.3rc4 <<>> www.example.com
;; global options:  printcmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 6398
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0
;; QUESTION SECTION:
;www.example.com.                IN      A
;; ANSWER SECTION:
www.example.com.        172765  IN      A       192.0.34.166
;; Query time: 18 msec
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Mon Oct  6 09:41:27 2003
;; MSG SIZE  rcvd: 49
```

对同一主机的后续查询仅耗时 18 毫秒，大约快了十倍。第二次查询如此之快的原因是该特定机器正在访问一个缓存 DNS 服务器。

如果查询耗时显著更长（或者更糟，超时），那么你就遇到了 DNS 问题。有几种可能的原因：

##### resolv.conf 设置

如果你在 chroot 监狱中运行 Postfix，你可能修改了 /etc/resolv.conf，但忘记将更新后的文件复制到 chroot 监狱（通常是 /var/spool/postfix/etc/resolv.conf）。

/etc/resolv.conf 中列出的 nameserver 可能响应缓慢，或者根本不处理请求。使用 dig 命令验证 /etc/resolv.conf 中每个 server 行指定的服务器是否能及时响应你的 DNS 查询。

##### 网络问题

你的互联网上行链路可能没有按预期工作，或者可能已经饱和。如果是这种情况，你应该考虑增加带宽或使用流量整形来优先处理 nameserver 查询。

##### 防火墙设置

防火墙可能会阻止进出你的邮件服务器的 nameserver 数据包。

##### 缓存 nameserver 故障

如果你在本地运行缓存 nameserver，请确保它确实在正常工作。

##### 提高 DNS 查询性能

如果你的 /etc/resolv.conf 设置、网络和防火墙看起来都正常，但你仍然需要加快 DNS 查询速度，你应该考虑运行一个本地缓存服务器，例如 djbdns dnscache 或在你的服务器或网络上运行一个 BIND 实例。缓存可以显著加快查询过程，同时减少网络利用，因为重复的查询不会导致出站数据包。

#### 确认你的服务器未被列为开放中继

如果你运行的是开放中继，可以预期许多邮件服务器会拒绝来自你的服务器的任何邮件。此外，垃圾邮件发送者会利用你的系统发送他们的邮件，从而增加你系统的负载，因为你的系统需要同时处理你的用户和滥用者。

通常，在开放中继被确认后，你的系统会出现在黑名单上。从黑名单中移除可能非常麻烦，可能需要几天甚至几周时间。因此，你必须确保你的系统不是开放中继或开放代理。在 http://openrbl.org 上查询你的 IP 地址。如果你被列入，请立即关闭开放中继。只允许用户在以下情况之一中进行中继：

- 用户的客户端列在 mynetworks 参数中。
- 用户的客户端成功执行了 SMTP 身份验证。
- 用户的客户端使用 TLS 客户端证书成功进行了身份验证。

#### 拒绝发送给不存在用户的消息

拒绝发送给系统中不存在的收件人的消息是一个好主意。如果 Postfix 接受此类邮件，它将不得不向发件人地址发送未送达通知。对于垃圾邮件或病毒邮件，该发件人地址几乎肯定不是邮件的真正来源。由此产生的 MAILER-DAEMON 通知会使队列堵塞几天。

这本身可能不会造成太大问题，但如果你接受发送给系统中不存在用户的邮件，你的系统可能会将消息存储在最终可能被填满的地方，或者如果你运行的是中继系统（参见第 13 章），消息的最终目标最终将不得不向消息的信封发件人（消息头中的 Return-Path）发送退信。此外，该退信本身可能无法投递，因为用作发件人域的域可能不会接受任何邮件。

无论如何，这些退信会使你的队列杂乱无章，或者进入 double_bounce_recipient 指定的邮箱（可能是你的 postmaster 帐户）。如果你在邮件队列中看到类似这样的内容，你可能正遇到这个问题：

```
$ mailq
-Queue ID- --Size-- ----Arrival Time---- -Sender/Recipients-------
63BE9CF331  10658 Mon Jan 12 14:38:30  MAILER-DAEMON
          (connect to mail3.quickspress.com[63.89.113.198]: Connection timed out)
                                    platinum@quickspress.com
1C932CF30E   3753 Sat Jan 10 16:16:38  MAILER-DAEMON
          (connect to mx.unrealdeals.biz[69.5.69.110]: Connection refused)
                                    EntrepreneurCareers@unrealdeals.biz
98EC3CF3F9   5505 Sat Jan 10 20:25:06  MAILER-DAEMON
          (connect to fhweb8.ifollowup.com[216.171.193.38]: Connection refused)
                                    root@fhweb8.ifollowup.com
50B14CF31E   5196 Mon Jan 12 11:35:11  MAILER-DAEMON
          (connect to mail.refilladvice.net[218.15.192.166]: Connection timed out)
                                    clintoncopeland@refilladvice.net
F4009CF39D   5452 Sun Jan 11 01:58:27  MAILER-DAEMON
          (connect to fhweb9.ifollowup.com[216.171.193.39]: Connection refused)
                                    root@fhweb9.ifollowup.com
-- 30 Kbytes in 5 Requests.
```

在这里你可以看到五条消息被退回到原始发件人（注意发件人是 MAILER-DAEMON），但在每种情况下，收件人的邮件服务器都无法访问。



要拒绝对系统中不存在的收件人的消息，请将 `local_recipient_maps` 和 `relay_recipient_maps` 参数（如果你运行的是一个仅将邮件中继到内部邮件服务器的网关，则设置后者）设置为包含有效收件人的映射。

如果退信问题真的失控了，你还可以采用 RHSBL 风格的黑名单（参见第 8 章）来拒绝来自根本不接受退信的服务器的邮件（因为所有需要发回这些服务器的退信会在你的邮件队列中停留数天）。RFC-Ignorant.Org (http://rfc-ignorant.org) 上有一个 RHSBL 风格的黑名单，你可以像这样使用：

```
check_rhsbl_sender dsn.rfc-ignorant.org
```

#### **阻止来自黑名单网络的消息**

有许多不同类型的阻止列表和 DNS 黑名单可供使用，这些列表基于各种原因列出了单个 IP 地址、整个 IP 范围甚至发件人域名。对于每种被认为的不当行为，至少有一个对应的列表。

其中最有用的列表是那些列出开放中继和开放代理的列表，因为它们可以以客观的方式自动进行测试。以下是一些黑名单：

- relays.ordb.org
- list.dsbl.org
- cbl.abuseat.org
- dul.dnsbl.sorbs.net

> **注意** *没有什么东西比黑名单变化得更快了。今天热门的黑名单明天可能就停止服务了。*

这些黑名单的误报率很低，因为它们提供了明确的地址列入标准。运行开放代理或开放中继通常被认为是错误的，因此使用这些列表会对配置错误的系统的管理员施加社会压力。（当然，他们可能毫无头绪或根本不在乎。）

#### **拒绝来自未知发件人域名的消息**

如果可能，不要接受包含无效域名的信封发件人的消息。如果在投递过程中出现问题，错误报告总是会返回给信封发件人，如果这个地址包含一个不存在的域名，那么错误报告就无处可发。

Postfix 会尝试发送错误报告，发现它无法投递，然后（因为它无法退信，因为信封发件人为空）将其发送到 `2bounce_notice_recipient`。你可以通过将 `reject_unknown_sender_domain` 添加到 `smtpd_sender_restrictions` 或 `smtpd_recipient_restrictions` 来避免这种情况，正如第 8 章详细讨论的那样。

#### **降低重传尝试频率**

如果你有很多邮件在最初的几次尝试中无法投递，可以考虑使用备用中继（使用 `fallback_relay` 参数）或增加退避时间（`maximal_backoff_time`），以减少延迟邮件重新进入活动队列的频率。

没有备用中继，Postfix 会花费宝贵的时间尝试向宕机或不可达的站点投递邮件。每一次这样的投递尝试都会占用一个 `smtp` 进程，该进程必须等待直到超时。备用中继可以为你完成那些无法一次投递成功的邮件的脏活，即重试传输。这意味着你的常规邮件服务器可以使用默认超时值，甚至使用更短的超时值运行，从而加快投递速度。

另一方面，增加 `maximal_backoff_time` 参数会提高服务器在发生投递问题后忽略特定目标的最大时间。因此，Postfix 对问题服务器的联系尝试就会减少。

#### **发现瓶颈**

本节介绍如何识别系统中的瓶颈。在阅读本节之前，你可能需要复习第 5 章，以了解哪些守护进程负责什么工作。

因为所有 Postfix 守护进程都必须访问一个或多个队列才能完成工作，所以了解队列状态会非常有用。以下是你需要关注的一些队列：

- incoming（传入队列）
- deferred（延迟队列）
- active（活动队列）
- maildrop（邮件投放队列）

当一条消息进入系统时，它会成为一个队列文件，Postfix 会在队列之间移动它。如果其中一个队列中有很多消息，你可能遇到了底层的性能问题。为了深入了解不同的队列，Victor Duchovni 编写了一个名为 `qshape` 的巧妙工具，用于显示消息在上述队列中的分布情况。该程序直接读取队列文件，绕过了 `mailq` 命令，因此只有 root 和 postfix 用户可以运行它。你可以从 http://sberv.stahl.bau.tu-bs.de/~hildeb/postfix/scripts 下载它。最近的 Postfix 版本已将此脚本包含在源代码 tarball 中。

`qshape` 以表格形式显示 Postfix 队列内容。表格的行显示发送到特定目的地的消息数量以及总数。列显示消息的年龄。例如，查看以下 `hold` 队列（参数 `hold`）的输出，你可以看到捕获的垃圾邮件的（主要是伪造的）发件人域名分布（参数 `-s`）的前十大行：

```
# qshape -s hold
```

|     | T | 5 | 10 | 20 | 40 | 80 | 160 | 320 | 320+ |
|:----|:---|:---|:---|:---|:---|:---|:---|:---|:---|
| TOTAL | 12 | 0 | 0 | 0 | 0 | 2 | 2 | 0 | 6 |
| hotmail.de | 2 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 2 |
| alb-24-194-161-132.nycap.rr.com | 1 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 |
| freenet.de | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 |
| x4u2.desy.de | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 |
| csi.com | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 |
| da.ru | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 |
| freeuk.com | 1 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 |
| mx5.outrageouscourtiers.com | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 |
| online.de | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| molgen.mpg.de | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 |
| charite.de | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

`T` 列包含每个域名的消息总数。其他列显示大于某个年龄（以分钟为单位）但不大于右侧列中年龄的消息计数。在这种情况下，有两条消息声称来自 hotmail.de。两条消息都超过了 320 分钟。

默认情况下，`qshape` 显示传入和活动队列的统计信息，因为它们与整体性能直接相关。你可以在命令行上指定不同的队列集，如下例所示：

```
$ qshape deferred
$ qshape incoming active deferred
```

既然你可以追踪到繁忙的队列，你就可以对它们采取一些措施。以下部分解释了如何解决每种类型队列中的瓶颈问题。我们还将介绍可用于计算你的系统能否处理给定邮件量的公式，以及如何以及何时使用备用中继。

##### **传入队列瓶颈**

如前一节“发现瓶颈”中所述，Postfix 的 cleanup 服务将所有新邮件存储在传入队列中。新文件在完成并准备好进行进一步处理之前，权限模式为 0600，处理完成后变为 0700 的访问模式。在正常情况下，传入队列几乎是空的，只包含模式为 0600 的文件，因为队列管理器应该能够在 cleanup 服务完成后立即将新消息导入活动队列。

然而，当消息输入速率飙升超过队列管理器将消息移入活动队列的速率时，传入队列将会增长。在那个阶段，唯一减慢队列管理器速度的是 trivial-rewrite 服务。如果队列管理器难以跟上，你可能使用了缓慢的查找服务——例如 MySQL 和 LDAP——进行传输查找，或者你可能需要加快提供查找服务的服务器的速度。

> **注意** *如果你使用的是高延迟或可变延迟的 IPC（进程间通信）映射，例如 LDAP 和 SQL，Postfix 需要更多时间来接收邮件。因此，Postfix 将运行更多的 smtpd（和 cleanup）进程，并且会更快地达到 smtpd 进程限制。使用这些缓慢的表查找，投递代理（local、pipe、virtual、lmtp）的完成时间可能比 smtpd 接收邮件所需的时间短，因此 Postfix 将运行比预期更少的投递代理。*

> *LDAP 的一个可能的补救措施是尝试避免绑定到你的 LDAP 服务器。在你的 LDAP 查询配置文件中设置 bind = no。这使得 Postfix 以匿名方式绑定到 LDAP 服务器，从而减少了身份验证和密码验证的开销。*

> *与基于文件的映射（如 hash、btree、dbm 和 cdb）相比，IPC 映射查找信息确实需要更长时间，因此 Postfix 守护进程在等待查找完成时无所事事。如果查找更快，Postfix 就会更快。*

> *正如其他地方讨论的那样，这些映射确实有其优点，而且可能大于缺点。其中一个最显著的优点是，当内容发生变化时，Postfix 无需终止和重新启动进程即可重新打开映射。你可能想尝试一些数据库调优。*

如果瓶颈位于传入队列中，那么消息的涌入优先于发送消息出去。防止邮件流入导致输出中断的一种方法是调整 `in_flow_delay` 参数，以便在队列管理器开始落后时限制输入速率。如果 cleanup 服务无法从队列管理器获得令牌，它会在创建新的队列文件之前暂停 `in_flow_delay` 指定的秒数。

这样做的原因是，cleanup 进程的数量通常受 SMTP 服务器 (`smtpd`) 并发数的限制。输入速率最多可以超过输出速率，即 SMTP 连接数除以 `in_flow_delay` 每秒的消息数。要找出当前传入 SMTP 连接的数量，请按如下方式使用 `ps` 和 `grep`：

```
# ps auxww| grep smtpd | grep -v grep | wc --lines
```



此系统上正在运行22个smtpd进程。此命令统计所有smtpd进程，因此如果您有多个smtpd配置（例如，您正在使用一个通过SMTP将邮件重新注入队列的内容过滤器），那么您需要使用更具体的grep模式来查找从外部网络接收邮件的smtpd守护进程数量：

```
# ps auxww| grep smtpd | grep -v grep | grep -v localhost | wc --lines
9
```

默认进程限制为100，`in_flow_delay`设置为一秒，这种耦合足以将单个失控的注入器限制为每秒一条消息。然而，它不足以同时抵消来自多个来源的过多输入速率。

如果您的服务器正受到多个来源的攻击，最好的选择是将SMTP会话尽可能缩短（设置`smtpd_error_sleep_time`为零，以及一个较低的`smtpd_hard_error_limit`，这将使Postfix挂断超过此限制的连接）。仅当传入队列在活动队列未满且`trivial-rewrite`服务使用快速传输查找机制时仍在增长时，才执行此操作。

如果您尝试了这些补救措施，但传入队列拥塞而活动队列不拥塞的问题仍然存在，那么问题很可能出在您的I/O子系统：邮件进入并写入磁盘，但`smtpd`和`qmgr`进程需要访问相同的资源（磁盘上的队列），您受限于I/O子系统的速度。

在这种情况下，您需要向邮件服务器添加大量内存（以便为操作系统增加磁盘缓存池），或者将队列目录移动到以下之一：

- 一个条带化RAID系统
- 一个带电池备份的RAM磁盘（这适合那些敢于冒险的人，因为系统崩溃时您会丢失邮件）

##### Maildrop队列瓶颈

通过Postfix `sendmail`命令提交但尚未由`pickup`服务发送到主Postfix队列的消息会停留在maildrop队列中——您可以使用`sendmail`命令发送消息，即使Postfix系统未运行，它们也会被添加到maildrop队列。单线程的`pickup`服务会定期扫描maildrop队列目录，或者在收到`postdrop`的新消息到达通知时扫描。

`pickup`服务将消息注入主队列的速度在很大程度上取决于磁盘访问时间，因为它必须在完成之前将消息提交到稳定存储。写入maildrop目录的`postdrop`程序也是如此。

由于`pickup`服务是单线程的，它一次只能传递一条消息，整体速率不超过`cleanup`服务引起的磁盘I/O延迟（以及适用的CPU使用率），因为`pickup`处理的每封邮件都需要经过`cleanup`。您记得，`cleanup`执行`header_checks`、`body_checks`等，这些可能非常耗费CPU。然后`cleanup`将消息写入队列文件——这受限于磁盘I/O延迟。如果您的maildrop队列出现拥塞，您可能遇到以下两个问题之一：

- 本地消息提交速率过高
- 由于过多的正文检查，`cleanup`服务CPU消耗过高

然而，请记住，当活动队列已满时，`cleanup`服务会根据`in_flow_delay`参数尝试通过每条消息暂停来减慢消息注入速度。在这种情况下，maildrop队列中的拥塞可能是更下游拥塞的结果。

不要尝试通过`pickup`服务传递大量邮件。如果您的站点流量很大，您需要避免使用通过`sendmail`和`postdrop`重新注入扫描邮件的内容过滤器。相反，使用SMTP连接进行注入。有很多程序可以为您完成此操作，包括mini_sendmail (http://www.acme.com/software/mini_sendmail)。

如果您有很多本地提交的邮件，您可能存在转发循环或失控的通知程序。此外，`postsuper -r`命令可以将选定的消息放入maildrop队列进行重新处理。虽然这对于重置陈旧的`content_filter`设置很有用，但使用`postsuper -r`重新排队大量消息可能会导致maildrop队列大小激增。

##### Deferred队列瓶颈

当Postfix由于临时故障无法将消息传递给某些收件人时，它会将消息放入deferred队列，希望稍后传递。队列管理器按照`queue_run_delay`参数指定的时间间隔定期扫描deferred队列。如第5章所述，队列管理器以轮询方式从传入队列和deferred队列中选择消息，以防止延迟邮件主导活动队列。

每次deferred队列扫描会将一小部分deferred队列重新注入活动队列进行重试，因为deferred队列中的每条消息在延迟时都会被分配一个冷却时间。Postfix通过将队列文件的修改时间时间扭曲到未来来实现这一点。如果队列文件的修改时间未到，则不符合重试条件。

冷却时间至少为`minimal_backoff_time`的值，最多为`maximal_backoff_time`。Postfix通过将消息在队列中的存在时间加倍并调整结果以确保时间介于这些限制之间来设置下一次重试时间。最终结果是Postfix更频繁地重试年轻的消息。

如果您的大型站点有一个大型deferred队列，您可能需要调整`queue_run_delay`、`minimal_backoff_time`和`maximal_backoff_time`参数，以便在第一次失败时提供短延迟，并在多次失败后可能导致较长的延迟。这将减少旧消息的重传速率，减少活动队列中先前延迟邮件的数量。

> **注意** 大型deferred队列的一个常见原因是在SMTP输入阶段未能验证收件人。有关为什么必须执行收件人验证的原因，请参见第8章中的“发送给未知收件人”部分。

如果一个有大量延迟邮件的服务器停机一段时间，当服务器恢复运行时，整个deferred队列可能同时达到重试时间。这可能导致活动队列非常繁忙。更复杂的是，如果大多数消息再次被延迟，该现象大约每隔`maximal_backoff_time`秒就会重复一次。

理想情况下，为了解决此问题，Postfix将在标准重试时间之外包含一个随机偏移量，以减少整个deferred队列同时被重复刷新的机会。

##### 活动队列瓶颈

如第5章所述，队列管理器是一个传递代理调度程序，试图在指定的资源限制内确保向所有目的地快速、公平地传递消息。当一个或多个目的地接受消息的速度慢于相应的消息输入速率时，活动队列就会发生拥塞。

如果目的地宕机一段时间，队列管理器会将其标记为死亡，并立即延迟该目的地的所有邮件，甚至不会费心将其分配给传递代理。因此，这些消息会很快离开活动队列，但最终进入deferred队列。如果目的地只是速度慢，或者存在问题导致输入速率过高，活动队列就会增长，并被发往慢速目的地的消息饱和。只有两种方法可以减少拥塞：

- 降低输入速率。
- 增加吞吐量。

增加吞吐量需要增加并发性（您运行的同时Postfix smtp进程数量）或降低传递延迟（通过使用更好的网络、更改映射类型、修复DNS延迟等）。要增加并发性，您可以在`main.cf`文件中增加`default_process_limit`参数的值。但是，如果您想按目的地执行此操作，请找到主导活动队列的慢速传输（例如用于`content_filter`的传输）或目的地（例如某些大型免费邮件站点）（`qshape`非常适合此目的）。找到罪魁祸首后，定义一个专用的传输名称并设置`name_destination_concurrency_limit`。有关如何操作的更详细信息，请参见本章中的“配置替代传输”。

最重要的是，请记住，任何服务使用的最大进程数在`master.cf`和`main.cf`中受到限制。

**注意** *请记住，您的操作系统必须能够处理增加的进程数和打开的文件数。请参阅Postfix常见问题解答中的“运行数百个进程”部分，网址为http://www.postfix.org/faq.html。*

有时可以通过加速DNS（参见本章中的“提高DNS查找性能”部分）和第5章“数据库（MySQL，PostgreSQL，LDAP）”部分中提到的映射查找来降低延迟。此外，对于拥有大量MX主机的繁忙站点，减少超时时间会有所帮助。但是，如果接收系统无法跟上（例如，当您向某些免费邮件网站等慢速站点发送时），这些都不会有帮助。

活动队列拥塞的另一个原因是无根据地刷新整个deferred队列。deferred队列包含可能无法传递的消息，至少在任何随机尝试中都不会传递。此外，导致延迟的故障可能需要很长时间，因为Postfix必须等待超时。

**注意** *某些管理员对于大型deferred队列的“刷新队列”本能可能适得其反，使问题变得更糟。除非您期望其中的大多数消息在下一次尝试中真正到达目的地，否则不要刷新deferred队列！因此，先分析，修复问题，然后刷新队列！*

最后，尽量避免重新加载或重启Postfix。当队列管理器重启时，活动队列目录中可能有消息，但真正的活动队列（在内存中）是空的。为了恢复内存中的状态，队列管理器将活动队列中的所有消息移回传入队列，并依靠正常的传入队列扫描来重新填充活动队列。将所有消息来回移动、重新执行传输表查找以及将消息重新导入内存的过程开销很大。



##### 异步弹跳队列拥塞不等式

**注意** postfix reload 命令会重启队列管理器，因此应避免在繁忙的生产服务器上随意修改需要执行 `postfix reload` 才能使更改生效的配置文件。

如果延迟队列中堆满了无法投递的弹跳邮件，Postfix 不应对队列拥塞负责。这种拥塞是在存在大量无法投递邮件积压时，因高平均延迟而导致的后果，因为尝试发送邮件的 smtp 守护进程会超时。Victor Duchovni 推导出了这个拥塞不等式，可以告诉你是否遇到了此类问题。

在一个包含大量永久无法投递的弹跳邮件的队列中，每次队列运行带入活动队列的垃圾邮件数量由以下公式决定：

```
队列大小 × 队列运行延迟 / 最大回退时间
```

每次队列运行处理的消息数量最多为：

```
队列运行延迟 × 默认进程限制 / smtp连接超时 × M
```

当进程限制耗尽时，你可以假设队列中的弹跳邮件数量远大于进程限制。（这里假设 `default_process_limit` 适用于 smtp 守护进程。如果你在 `master.cf` 的 maxproc 列中提高了该值，请在此方程中使用该值代替。）

将这些方程组合起来，你得到以下结果：

```
队列大小 × 队列运行延迟 / 最大回退时间 ≥ 队列运行延迟 × 默认进程限制 / smtp连接超时 × M
```

当你将不等式两边乘以 `最大回退时间 / 队列运行延迟` 时，就得到了拥塞不等式：

```
P × B ≥ Q × T × M
```

参数如下：

- **P** smtp 传输进程限制，通过运行以下命令获得：

```
# postconf default_process_limit
default_process_limit = 100
```

**注意** 检查 `master.cf` 中 smtp 行的 maxproc 值，看看是否有显式的 smtp 传输进程限制。

- **B** 最大回退时间，通过以下命令获得：

```
# postconf maximal_backoff_time
maximal_backoff_time = 4000s
```

- **Q** 队列中的弹跳邮件数量（这些弹跳邮件大概会发送到至少 P / destination\_concurrency\_limit 个不同的目标）。

- **T** smtp 连接超时，通过以下命令获得：

```
# postconf smtp_connect_timeout
smtp_connect_timeout = 30s
```

- **M** 平均 MX IP 地址数量。当一个域名有多个 MX 记录时，Postfix 必须尝试每一个。你不需要精确的数字；只需估算一下，并使用 qshape 来估算主要目标的 MX 数量。

**注意** 默认情况下，每个目标最多可以使用 20 个投递代理（default\_destination\_concurrency\_limit = 20），因此不断添加目标直到达到进程限制。实际上，只需估算 M 的范围，也许可以通过设置 `smtp_mx_address_limit`（Postfix 尝试的 MX 地址数量上限）来加以限制。

如果无法满足此不等式，你就会遇到严重的问题。尽一切努力降低不等式右侧的值并提高左侧的值。尝试降低右侧的值时，请记住以下几点：

- 除了删除弹跳邮件，你无法减少 Q。
- 你可以通过为弹跳邮件的目标域创建专用的 smtp 传输并降低其 SMTP 连接超时来减少 T。
- 你无法减少 M，因为你并不运行目标服务器和 DNS 服务。

以下是一些提高左侧值的建议：

- 增加 P 很容易。更改默认进程限制或编辑 master.cf 以允许更多 smtp 进程。
- 要增加 B，请增加最大回退时间。

让我们看几个例子。第一个是 Solaris 上安装的 Postfix 1.x，队列中有 2,000 条垃圾邮件。在 Postfix 1.x 中，`smtp_connection_timeout` 设置是操作系统的 TCP 连接超时。在 Solaris 上默认约为 180 秒，在 Linux 上则更长。如果你使用默认的 `default_process_limit` 值 50，你会得到以下结果：

```
P * B >= Q * T
50 * 4000 >= 2000 * 180
200000 >= 360000
```

这里，不等式不成立，因为 4,000 秒的 `maximal_backoff_time` 太小了，特别是当垃圾目标有多个 MX 记录时。

现在让我们考虑使用 Postfix 1.1.11（或更高版本）且队列中有 2,000 条垃圾邮件的情况。对于较新版本的 Postfix（至少 1.1.11-20020717），所有平台上的连接超时都是 30 秒，并且版本 1.1.12-20021212 将默认进程限制提高到 100。这得出以下结果：

```
P * B >= Q * T
100 * 4000 >= 2000 * 30
400000 >= 60000
```

这一次，不等式成立。此外，因为默认回退时间是 4,000 秒，即使典型的垃圾目标 MX 主机数量为 4，这也远低于临界水平。较新版本的 Postfix 可以处理大得多的垃圾邮件队列。

`default_process_limit` 设置为 100 时的临界队列大小大约如下：

```
100 * 4000 / 30 = 13000
```

如果 MX 数量大于一，这个值可能会更低。如果进程限制为 500，超时为 10 秒，`maximal_backoff_time` 为 4 小时，临界队列大小就是这个惊人的数字：

```
500 * 14400 / 10 = 720000
```

然而，这个荒谬的限制将使 500 个进程忙于每 10 秒尝试新消息——换句话说，每秒将有 50 条消息离开并重新进入延迟队列。

#### 使用故障转移中继

如果主队列在负载下不堪重负，值得费心设置第二台服务器（或 Postfix 实例；多实例支持计划在 2.2 版本中实现）来处理重试。因此，你可以正常调整主队列，或许设置非常短的超时时间，而任何首次投递失败的消息都可以在故障转移队列或使用本章前面描述的特殊调整的故障转移中继上进行重试。

要进行设置，请在你的主 Postfix 服务器的 `main.cf` 文件中设置以下参数：

```
smtp_connect_timeout = 5s
smtp_mx_address_limit = 3
#fallback_relay = [127.0.0.1]:20025
# for multiple instances of Postfix on the same machine
fallback_relay = fallback.example.com
# for another instance on another host
```

然后，在 `fallback_relay` 指定的服务器上，设置一个较高的临界队列大小。例如，使用以下参数设置限制为 720000：

```
smtp_connect_timeout = 10s
smtp_mx_address_limit = 5
default_process_limit = 500
bounce_queue_lifetime = 2d
maximal_backoff_time = 4h
```

**注意** 你可能想稍微增加一下 `smtp_connect_timeout`。有些主机和网络确实很慢。

### 针对更高吞吐量的调整

如果你的机器中转大量的入站邮件，你可以安排一个单独的传输将邮件转发到入站域。在本节中，我们称该传输为 "relay"。在 Postfix 2.x 中，你可以这样调整：

1. 将 `relay_destination_concurrency_limit` 设置为一个较高的数字（例如 50）。
2. 在 master.cf 中为 relay 设置条目，使其包含 `-o smtp_connect_timeout=$relay_connect_timeout`（等号两边没有空格）。
3. 在 main.cf 中将 `relay_connect_timeout` 设置为 5 或 1。

如果你使用基于 SMTP 的 `content_filter` 进行病毒内容过滤（请参见第 12 章），请确保发送传输配置了 `-o disable_dns_lookups=yes`。当你将所有邮件发送到固定目标且不必查找 MX 记录时（例如，使用 relayhost 功能时），这也有帮助。

### 配置备用传输

如果你经常向具有大量邮件交换器（例如 Hotmail 就是一个显著例子）的站点发送大量邮件，使用默认超时没有多大意义。如果 Postfix 不在每个故障邮件交换器上花费那么多时间，它可能可以更快地投递发往这些域的邮件。本节将向你展示如何操作。

首先，在你的 `master.cf` 文件中定义一个名为 `deadbeats` 的新 `smtp` 传输。为此，复制 `smtp` 传输行，将其重命名为 `deadbeats`，并进行一点微调——设置一个更低的 `smtp_connect_timeout` 值：

```
deadbeats unix  -       -       -       -       -       smtp
    -o smtp_connect_timeout=$deadbeats_connect_timeout
```

默认超时是 30 秒，因此在你的 `main.cf` 文件中将 `deadbeats_connect_timeout` 设置为 5 秒：

```
deadbeats_connect_timeout = 5
```

现在，仍然在你的 `main.cf` 文件中，通过设置 `transport_maps` 参数指示 Postfix 在向某些目标域发送邮件时使用这个特殊传输：

```
transport_maps = hash:/etc/postfix/transport
```

按如下方式创建 `/etc/postfix/transport` 映射：

| 目标 | 传输 | 备注 |
|---|---|---|
| yahoo.com | deadbeats: | yahoo.com 有 3 个 MX 主机，总共 9 个 A 记录 |
| compuserve.com | deadbeats: | compuserve.com 有 3 个 MX 主机，每个 4 个 A 记录 |
| aol.com | deadbeats: | aol.com 有 4 个 MX 主机，总共 18 个 A 记录 |
| hotmail.com | deadbeats: | hotmail.com 有 4 个 MX 主机，总共 10 个 A 记录 |
| hotmail.de | deadbeats: | hotmail.de 没有 MX 主机，但有 6 个 A 记录 |

要使其生效，运行 `postmap hash:/etc/postfix/transport`，并重新加载你的配置。



# 附录

*Postfix 权威指南*的最后部分是附录。这些附录旨在帮助您入门、在遇到问题时进行故障排除，并在配置服务器过程中为您提供一些参考资料：

**安装 Postfix**

附录 A 包含了从源代码安装 Postfix 的说明，以及适用于 Debian 和 Red Hat Linux 发行版的说明。

**Postfix 故障排除**

尝试修改配置时遇到麻烦？附录 B 提供了针对最常见问题的建议，并给出了一些排查问题的通用技巧。

**CIDR 和 SMTP 标准参考**

并非每个人都能记住 CIDR 表示法中的子网或 SMTP 服务器响应代码。我们已将它们整理在附录 C 中。

### A

## 安装 POSTFIX

本附录描述了如何从源代码构建 Postfix，以及如何为 Debian Linux 和 Red Hat Linux 安装、准备和构建软件包。

### Postfix 源代码

您可以在 http://www.postfix.org/download.html 找到指向 Postfix 源代码的链接。有多个镜像站点；您应选择离您最近的一个以获得最快速度。

在下载源代码之前，您应该了解实验性（快照）版本和正式发布版本之间的区别。正式发布版本不会更改，除非有错误修复和可移植性补丁。另一方面，快照版本包含新的、未经测试的功能。快照版本中有效（且停止更改）的代码最终会成为正式发布版本的一部分。

正式的 Postfix 发布版本命名为 `postfix-a.b.c.tgz`，其中 *a*、*b* 和 *c* 如下：

- a 主版本号（重大软件包重组）
- b 次版本号（新功能）
- c 补丁级别（错误修复）

快照版本的名称类似于 `postfix-a.b-yyyymmdd.tgz`，其中 *yyyymmdd* 是发布日期。`mail_release_date` 配置参数包含正式发布和快照发布的发布日期。

当您应用正式补丁时，补丁级别和发布日期会发生更改。但是，新的快照只有不同的发布日期，除非快照包含与补丁版本相同的错误修复。

### 应用补丁

通过应用第三方补丁，您可以获得一些特殊功能。您可以在 http://www.postfix.org/addon.html 找到 Postfix 补丁列表。（如果您不知道如何应用补丁，您可能不应该这样做。）

补丁有其自己的文档，并且由于它们可能显著改变 Postfix 的功能和行为，您应仔细阅读说明。

### 从源代码构建和安装

使用 `tar xfz postfix-a.b.c.tgz` 解压源代码包后，您可能会根据所需功能自定义构建过程。`README_FILES` 目录包含有关 BerkeleyDB、PCRE、MySQL 和 SASL (SMTP-AUTH) 支持等功能的文档。该目录中的每个文件都提供了有关如何设置环境变量以更改构建过程的说明。

如果您正在寻找本书中描述的、但不在默认配置中的功能，您很可能会在描述该功能的章节开头找到如何构建带有该功能的 Postfix 的说明。您可以在 Postfix 附带的 `INSTALL` 文件中找到可用选项的完整列表。构建过程始终相同：

1. 将 `AUXLIBS` 环境变量设置为一组链接器选项。
2. 将 `CCARGS` 环境变量设置为一组编译器和预处理器选项。
3. 运行 `make makefiles` 来创建 Makefile。

例如，在一台古老的 HP-UX 10.20 机器上，以下命令包含 BerkeleyDB 支持，其中库路径为 `/users2/local/BerkeleyDB-4.0.14/lib`，包含路径为 `/users2/local/BerkeleyDB-4.0.14/include`。

```
$ AUXLIBS='-L/users2/local/BerkeleyDB-4.0.14/lib -ldb' \
CCARGS='-DHAS_DB -I/users2/local/BerkeleyDB-4.0.14/include' \
make makefiles
```

如果您想改用 CDB，请应用补丁、安装 CDB 库，然后运行此命令：

```
$ AUXLIBS='-L/usr/local/lib -lcdb' \
CCARGS='-DHAS_CDB -I/usr/local/include' \
make makefiles
```

然后，作为普通用户，运行 `make`：

```
$ make
```

编译软件包后，您需要确定是首次安装 Postfix 还是仅安装升级。对于首次安装，请以 root 身份运行此命令：

```
# make install
```

此命令会询问有关安装路径的几个问题。但是，如果您正在升级现有安装，请改为以 root 身份运行以下命令：

```
# postfix stop
# make upgrade
# postfix start
```

对于升级，安装程序会从 `main.cf` 文件中提取现有 Postfix 安装的路径，并重用这些路径和配置文件。

### 启动和停止 Postfix

您可能已经注意到，您可以使用 `postfix` 程序控制 Postfix。它理解以下参数：

**start** 启动 Postfix 邮件系统。这也会运行下面描述的配置检查。

**stop** 执行邮件系统的有序关闭。正在运行的进程将在最早方便时终止。

**check** 验证 Postfix 配置是否有效。此命令会警告您有关错误的目录或文件所有权和权限的问题，并会创建缺失的目录。

## 在 Debian Linux 上安装 Postfix

使用 apt-get 命令在 Debian Linux 发行版上安装 Postfix 很容易。尽管 Postfix 版本可能随时间变化，但您在 Debian Linux 上执行安装和集成的步骤可能在一段时间内保持不变。

### 安装 Postfix

使用 Debian 初始安装系统时，您可以选择 Postfix 作为软件包。但是，如果您不手动覆盖邮件系统的默认选择，exim 将在初始启动后作为默认 MTA 启用。您可以使用 dpkg 命令查看系统上是否安装了 Postfix，如果已安装，它将打印出已安装的版本。使用方法如下：

```
$ dpkg -l 'postfix*'
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Installed/Config-files/Unpacked/Failed-config/Half-installed
|/ Err?=(none)/Hold/Reinst-required/X=both-problems (Status,Err:
uppercase=bad)
||/ Name           Version        Description
+++-==============-==============-=================================
ii  postfix        1.1.11.0-3     A high-performance mail transport agent
un  postfix-dev    <none>         (no description available)
un  postfix-doc    <none>         (no description available)
ii  postfix-ldap   1.1.11.0-3     LDAP map support for Postfix
ii  postfix-mysql  1.1.11.0-3     MYSQL map support for Postfix
ii  postfix-pcre   1.1.11.0-3     PCRE map support for Postfix
un  postfix-snap   <none>         (no description available)
un  postfix-snap-dev <none>       (no description available)
un  postfix-snap-doc <none>       (no description available)
un  postfix-snap-ldap <none>      (no description available)
un  postfix-snap-mysql <none>     (no description available)
un  postfix-snap-pcre <none>      (no description available)
un  postfix-snap-tls <none>       (no description available)
un  postfix-tls    <none>         (no description available)
```

如您所见，已安装 Postfix 1.1.11.0-3。此系统还支持 ldap、mysql 和 pcre 映射。不存在的是 postfix-tls 软件包（支持 TLS 和 SASL 的软件包）或某个更实验性的快照版本（postfix-snap）。

如果您想尝试 Postfix 快照，请运行此命令：

```
# apt-get install postfix-snap
Reading Package Lists... Done
Building Dependency Tree... Done
```



以下软件包将被 **移除**：
  postfix postfix-ldap postfix-mysql postfix-pcre
以下 **新** 软包包将被安装：
  postfix-snap
0 个软件包被升级，1 个新安装，4 个待移除，0 个未升级。
需要下载 567kB 的归档。解包后将释放 47.1kB 的空间。
您是否希望继续？[Y/n]

Debian 的软件包管理系统会在安装 postfix-snap 软件包之前移除任何冲突的软件包，例如 exim 和 Sendmail。

### 启动和停止 Postfix

Debian 的策略规定，系统守护进程必须配备启动和关闭脚本，并将其置于 `/etc/init.d` 目录中。你可以使用 `/etc/init.d/postfix start` 手动启动 Postfix，并使用 `/etc/init.d/postfix stop` 停止它。

### 安装更新

在 Debian 上安装更新和升级也通过 `apt-get` 命令进行。以下是执行更新的示例：

```
# apt-get update
Hit http://marillat.free.fr unstable/main Packages
Hit http://marillat.free.fr unstable/main Release
Hit http://smarden.org woody/unofficial Packages
Ign http://smarden.org woody/unofficial Release
Hit http://smarden.org woody/pape Packages
...
Reading Package Lists... Done
Building Dependency Tree... Done
# apt-get upgrade
Reading Package Lists... Done
Building Dependency Tree... Done
0 packages upgraded, 0 newly installed, 0 to remove and 0  not upgraded.
```

除非有绝对必要的变更，例如对 `master.cf` 文件的添加或更改以及对队列目录的更改，否则升级过程会保留当前配置不变。

### 从 Debian 源代码包构建

如果你想从 Debian 源代码包构建 Postfix，首先获取源代码包：

```
# apt-get source postfix
Reading Package Lists... Done
Building Dependency Tree... Done
```

```
Need to get 2382kB of source archives.
Get:1 http://http.us.debian.org unstable/main postfix 2.1.3-1 (dsc) [832B]
Get:2 http://http.us.debian.org unstable/main postfix 2.1.3-1 (tar) [1972kB]
Get:3 http://http.us.debian.org unstable/main postfix 2.1.3-1 (diff) [409kB]
Fetched 1977kB in 9s (216kB/s)
dpkg-source: extracting postfix in postfix-2.1.3
```

获取系统上的源代码后，你可以修改 `debian/rules` 或 `debian` 目录中的其他文件，以任何你想要的方式更改构建过程。当你对配置感到满意时，可以尝试使用以下命令构建 Postfix：

```
# cd postfix-2.1.3
# dpkg-buildpackage
```

假设你尝试了这个操作，但遇到了一些错误信息，例如：

```
dpkg-buildpackage: source package is postfix
dpkg-buildpackage: source version is 2.1.3-1
dpkg-buildpackage: source maintainer is LaMont Jones <lamont@debian.org>
dpkg-buildpackage: host architecture is i386
dpkg-checkbuilddeps: Unmet build dependencies: libdb4.2-dev libgdbm-dev libldap2-dev (>= 2.1) libmysqlclient10-dev libsasl2-dev postgresql-dev
dpkg-buildpackage: Build dependencies/conflicts unsatisfied; aborting.
dpkg-buildpackage: (Use -d flag to override.)
```

这意味着你缺少构建这个特定的 Postfix 源代码包所需的一些软件包。像这样安装这些软件包：

```
# apt-get install libdb4.2-dev libgdbm-dev libldap2-dev libmysqlclient10-dev libsasl2-dev postgresql-dev
...
```

现在，再次尝试。构建过程应该如下所示：

```
# dpkg-buildpackage
dpkg-buildpackage: source package is postfix
dpkg-buildpackage: source version is 2.1.3-1
dpkg-buildpackage: source maintainer is LaMont Jones <lamont@debian.org>
dpkg-buildpackage: host architecture is i386
 debian/rules clean
test -f debian/rules
dh_clean build
...
dpkg-deb: building package `postfix-doc' in `../postfix-doc_2.1.3-1_all.deb'.
 dpkg-genchanges
dpkg-genchanges: including full source code in upload
dpkg-buildpackage: full upload (original source is included)
```

到目前为止一切顺利，但你可能想确认一下软件包是否已生成：

```
# cd ..
# ls -l *.deb
-rw-r--r-- 1 root src  97592 Jul  5 13:11 postfix-dev_2.1.3-1_all.deb
-rw-r--r-- 1 root src 662758 Jul  5 13:11 postfix-doc_2.1.3-1_all.deb
-rw-r--r-- 1 root src  33644 Jul  5 13:11 postfix-ldap_2.1.3-1_i386.deb
-rw-r--r-- 1 root src  29646 Jul  5 13:11 postfix-mysql_2.1.3-1_i386.deb
-rw-r--r-- 1 root src  29430 Jul  5 13:11 postfix-pcre_2.1.3-1_i386.deb
-rw-r--r-- 1 root src  29920 Jul  5 13:11 postfix-pgsql_2.1.3-1_i386.deb
-rw-r--r-- 1 root src 140110 Jul  5 13:11 postfix-tls_2.1.3-1_i386.deb
-rw-r--r-- 1 root src 763570 Jul  5 13:11 postfix_2.1.3-1_i386.deb
```

如果一切正常，使用 `dpkg -i` 安装软件包：

```
# dpkg -i postfix_2.1.3-1_i386.deb
```

## 在 Red Hat Linux 上安装 Postfix

你可以使用 RPM（Red Hat 软件包管理器）系统在 Red Hat Linux 发行版上安装 Postfix。从 Red Hat Linux 7.3 版本开始，你甚至可以将 Postfix 与 Sendmail 并行安装。你可以通过使用 alternatives 系统在它们之间切换来选择运行哪个 MTA。

与 Debian 软件包一样，尽管 Postfix 版本会随时间变化，但在 Red Hat Linux 系统上安装 Postfix 所需的步骤在很长一段时间内不太可能改变。

### 获取适用于 Red Hat Linux 的 Postfix

Red Hat 安装程序在安装 Red Hat Linux 时默认不包含 Postfix，但你可以在安装时添加它。要检查 Postfix 是否已在你的系统上，请查询软件包管理器：

```
# rpm -q postfix
postfix-2.1.1-3.fc1
```

这里，软件包管理器打印出了当前安装的版本。如果你的系统上没有安装 Postfix，你会得到类似这样的输出：

```
# rpm -q postfix
package postfix is not installed
```

> **注意** RPM 仅列出使用 RPM 安装的软件。它不会列出从源代码编译和安装的应用程序。

### 从 CD 获取 Postfix

将 Postfix 放到你的机器上最方便的方法是从 Red Hat CD 复制到你的硬盘并安装 RPM。将光盘插入你的 CD 驱动器，并使用如下命令将其挂载到你的系统：

```
# mount /dev/cdrom /mnt/cdrom/
```

使用如下命令将 Postfix RPM 复制到你的硬盘：

```
# rpm -ivh /mnt/cdrom/RedHat/RPMS/postfix-XX-xx.rpm
```

### 从 Red Hat 站点下载 Postfix

你也可以从 Red Hat FTP 站点或其镜像站之一下载 Postfix 软件包。你可以在 http://www.redhat.com/download/mirror.html 找到镜像站列表。下载软件包后，让软件包管理器获取并安装文件：

```
# rpm -ivh ftp://USER:PASSWORD@HOST:PORT/path/to/postfix-XX-xx.rpm
```

请记住，Red Hat 不会以 Postfix 开发的速度来更新这些软件包。如果你想运行具有最新功能的 Postfix 软件包但又不想从源代码构建它，可以查看 Simon J. Mudd 维护的 RPM。

### 下载 Simon J. Mudd 的 Postfix RPM

Simon 的 RPM 通常比 Red Hat 发行版附带的 RPM 更新。你可以下载适用于多个平台的预编译二进制文件，包括 Alpha、Sparc 和 IBM S390（大型机）上的 Linux，或者你可以获取 SRPM（RPM 源代码包）。SRPM 支持使用网站上列出的多个选项来构建二进制软件包。

你可以在 http://postfix.wl0.org/en/mirrors/ 找到 Simon 的 RPM 和 SRPM 的镜像站点。

### 从 rpmfind.net 下载 Postfix

最后，你会发现 rpmfind.net 提供了许多发行版的 RPM。将你的浏览器指向 http://www.rpmfind.net，搜索 *postfix*，并下载适合你需要的 RPM。

### 从 SRPM 构建 RPM

出于安全考虑，你不应该以 root 用户身份从 SRPM 构建 RPM。然而，以非 root 用户身份构建它们需要一些准备工作。具体来说，RPM 需要特定的目录结构才能从源代码或 SRPM 构建 RPM。默认情况下，这些目录位于 `/usr/src/redhat` 下。

#### 设置目录结构和环境变量

当你以普通用户身份构建 RPM 时，不能使用默认位置，因为只有 root 才被允许写入默认目录。使用以下脚本在你的主目录中创建所需的目录结构，并为 RPM 设置适当的环境变量：

```
#!/bin/sh
# rpmuser Build user rpmbuild environment
# Author: Tuomo Soini <http://tis.foobar.fi>
#
# create directories
for i in SOURCES SPECS BUILD SRPMS RPMS/i386 RPMS/i486 RPMS/i586 RPMS/i686 \
RPMS/athlon RPMS/noarch
do
    mkdir -p $HOME/rpm/$i
done
unset i
# set environment variables
echo "%_topdir $HOME/rpm" >> $HOME/.rpmmacros
# EOF
```

假设你创建了一个名为 `rpmuser` 的用户来构建 RPM。运行 `rpm_prepare.sh` 后，该用户的主目录应包含以下目录和子目录：

```
$ tree
.
|-- rpm
|   |-- BUILD
|   |-- RPMS
|   |   |-- athlon
|   |   |-- i386
|   |   |-- i486
|   |   |-- i586
|   |   |-- i686
|   |   `-- noarch
|   |-- SOURCES
|   |-- SPECS
|   `-- SRPMS
`-- rpm_prepare.sh
12 directories, 1 file
```

该脚本还在 `.rpmmacros` 文件中设置了正确的变量。每次以构建 RPM 的用户身份登录和注销时，你都需要设置环境。使用 `echo "%_topdir $HOME/rpm" >> $HOME/.rpmmacros` 命令执行此操作。

> **注意** *如果你想了解更多关于构建 RPM 的详细信息，请查看 http://rpm.org 上的 RPM HOWTO。*



#### 构建和安装 RPM

你无法查询源代码包的选项来构建二进制文件。解决方法是使用 `rpm -ivh postfix-XX-xx.src.rpm` 将源代码包安装到新的 rpm 构建目录；然后查看用于构建 spec 文件的脚本：

```
$ less rpm/SOURCES/make-postfix.spec
...
# The following external variables if set to 1 affect the behaviour
#
# POSTFIX_MYSQL        include support for MySQL's MySQL packages
# POSTFIX_MYSQL_REDHAT include support for RedHat's mysql packages
# POSTFIX_MYSQL_PATHS  include support for locally installed mysql binary,
# providing the colon separated include and
# library paths ( /usr/include/mysql:/usr/lib/mysql )
# POSTFIX_MYSQL_QUERY  include support for writing full select statements
# in mysql maps
# POSTFIX_LDAP         include support for openldap packages
# POSTFIX_PCRE         include support for pcre maps
# POSTFIX_PGSQL        include support for PostGres database
# POSTFIX_SASL         include support for SASL (1, 2 or 0 to disable)
# POSTFIX_TLS          include support for TLS
# POSTFIX_IPV6         include support for IPv6
# POSTFIX_VDA          include support for Virtual Delivery Agent
...
# To rebuild the spec file, set the appropriate environment
# variables and do the following:
#
# cd `rpm --eval '%{_sourcedir}'`
# export POSTFIX_MYSQL=1      # for example
# sh make-postfix.spec
# cd `rpm --eval '%{_specdir}'`
# rpmbuild -ba postfix.spec
```

按照脚本中的说明设置相应的环境变量并创建你的 spec 文件。对 spec 文件满意后，使用以下命令构建你的 RPM：

```
$ rpmbuild -ba rpm/SPECS/postfix.spec
```

成功完成后，以 root 身份安装 Postfix：

```
# rpm -ivh /path/to/postfix-XX-xx.rpm
```

现在你需要做的就是告诉你的 Red Hat 服务器使用 Postfix 作为其 MTA。

### 切换到 Postfix

Red Hat 服务器的默认 MTA 是 Sendmail。你可以使用 alternatives 命令将其切换为 Postfix。

> **注意** 从 Red Hat 7.3 开始，该发行版包含一个名为 *alternatives* 的 Debian 移植版。这个命令使得多个执行相同或类似功能的程序可以同时安装在单个系统上。

以 root 身份，调用 `alternatives --config mta`，然后将 Postfix 指定为默认 MTA：

```
# alternatives --config mta
There are 2 programs which provide 'mta'.

  Selection    Command
-----------------------------------------------
*+ 1           /usr/sbin/sendmail.sendmail
   2           /usr/sbin/sendmail.postfix

Enter to keep the default[*], or type selection number: 2
```

作为默认 MTA，Red Hat 会在启动时自动启动 Postfix。你可以通过运行 `chkconfig` 来检查运行级别：

```
# chkconfig --list postfix
postfix          0:off  1:off  2:on  3:on  4:on  5:on  6:off
```

### 卸载 Sendmail MTA

安装 Postfix 后，没有理由再保留 Sendmail，所以像这样卸载它：

```
# rpm -e sendmail
```

### 在 Red Hat Linux 中启动和停止 Postfix

Red Hat Linux 的 RPM 通常包含位于 `/etc/init.d` 的启动和关闭脚本。你可以使用 `/etc/init.d/postfix start` 启动 Postfix，使用 `/etc/init.d/postfix stop` 停止它。

### B

## POSTFIX 故障排除

本章包含针对几个不同 Postfix 故障领域的技巧，包括系统日志记录器、配置问题、网络异常和一般系统问题。与任何类型的故障排除一样，当 Postfix 出现问题时，你需要在修复之前对问题所在有一个大致的了解。对于拥有多个独立子系统的 Postfix 来说，这一点尤其重要。

## Postfix 启动和查看日志问题

Postfix 无法处理你的邮件最“明显”的原因可能是 Postfix 甚至没有在运行。即使你只是使用 sendmail 命令提交邮件，Postfix 也必须在运行。检查 Postfix 是否在运行的最简单方法是运行 **postfix start**：

```
# postfix start
postfix/postfix-script: starting the Postfix mail system
```

如果你看到此消息，表示 Postfix 未在运行，因此该命令尝试启动它。但是，如果 Postfix 已经在运行，你将看到此消息：

```
# postfix start
postfix/postfix-script: fatal: the Postfix mail system is already running
```

运行此命令时，你应该在邮件日志中看到类似的消息，例如：

```
Jul  5 22:49:29 mail postfix/postfix-script: starting the Postfix mail system
Jul  5 22:49:29 mail postfix/master[14835]: daemon started -- version 2.1.3
```

如果没有看到这些消息，请立即检查你的 syslog 配置。你需要确保它记录了 *mail.*；完整的日志对于任何全面的故障排除都至关重要。

我们建议将邮件设施（或 Postfix 配置的任何设施）的所有 syslog 条目合并到一个日志文件中。某些安装（例如 Debian GNU/Linux 中的那个）将日志拆分为多个文件，但这会使阅读日志变得非常繁琐。为了便于查看，请确保你的 /etc/syslog.conf 有如下条目：

```
# (- Log all the mail messages to one place.)
mail.*							-/var/log/maillog
```

假设你在命令行和日志中看到了消息，但仍然怀疑 Postfix 是否真的在运行。有时保持偏执是值得的，因为如果存在严重问题，Postfix 可能会启动后立即崩溃。使用 ps 和 grep 查看 Postfix 组件守护进程是否真的在运行。如果它们在运行，命令执行应如下所示：

```
# ps aux|grep postfix
root     5035  0.0  0.4  2476 1100 ?        S   09:29   0:00 /usr/lib/postfix/master
postfix  5036  0.0  0.3  2404  936 ?        S   09:29   0:00 pickup -l -t fifo -u -c
postfix  5037  0.0  0.3  2440  964 ?        S   09:29   0:00 qmgr -l -n qmgr -t fifo -u -c
```

在上面的输出中，你可以看到 Postfix master 守护进程以 root 身份运行，而队列管理器 (*qmgr*) 和 pickup 服务以 postfix 用户身份运行，因此系统正在运行。

Postfix 启动失败有多个原因，但最常见的是 Postfix 守护进程找不到共享库。要处理此问题，首先使用以下命令找到 Postfix 使用的目录：

```
# postconf | grep directory
command_directory = /usr/sbin
config_directory = /etc/postfix
daemon_directory = /usr/lib/postfix
mail_spool_directory = /var/mail
manpage_directory = /usr/local/man
process_id_directory = pid
program_directory = /usr/sbin
queue_directory = /var/spool/postfix
readme_directory = no
require_home_directory = no
sample_directory = /etc/postfix
tls_random_exchange_name = ${config_directory}/prng_exch
```

你要寻找的是 daemon_directory 的路径。找到它并切换到该目录。查看内容：

```
# cd /usr/lib/postfix
# ls -l
total 384
-rwxr-xr-x 1 root root 16588 Sep 12 18:50 bounce
-rwxr-xr-x 1 root root 22684 Sep 12 18:50 cleanup
-rwxr-xr-x 1 root root  4248 Sep 12 18:50 error
-rwxr-xr-x 1 root root 10344 Sep 12 18:50 flush
-rwxr-xr-x 1 root root 20508 Sep 12 18:50 lmtp
-rwxr-xr-x 1 root root 31956 Sep 12 18:50 local
-rwxr-xr-x 1 root root 22388 Sep 12 18:50 master
-rwxr-xr-x 1 root root 33084 Sep 12 18:50 nqmgr
-rwxr-xr-x 1 root root  7248 Sep 12 18:50 pickup
-rwxr-xr-x 1 root root 10496 Sep 12 18:50 pipe
-rwxr-xr-x 1 root root 27424 Sep 12 18:50 qmgr
-rwxr-xr-x 1 root root 12160 Sep 12 18:50 qmqpd
-rwxr-xr-x 1 root root  7456 Sep 12 18:50 showq
-rwxr-xr-x 1 root root 25000 Sep 12 18:50 smtp
-rwxr-xr-x 1 root root 44712 Sep 12 18:50 smtpd
-rwxr-xr-x 1 root root  5612 Sep 12 18:50 spawn
-rwxr-xr-x 1 root root 10284 Sep 12 18:50 trivial-rewrite
-rwxr-xr-x 1 root root 10400 Sep 12 18:50 virtual
```

/etc/postfix/master.cf 文件中命令列的 Postfix 守护进程应在此目录中。你可以使用 ldd 命令检查单个程序的共享库依赖关系（这适用于 Linux、Solaris 和其他常见的 Unix 变体；在其他系统上可能是不同的命令）：

```
# ldd `postconf -h daemon_directory`/smtpd
	libpostfix-master.so.1 => /usr/lib/libpostfix-master.so.1 (0x4001d000)
	libpostfix-global.so.1 => /usr/lib/libpostfix-global.so.1 (0x40023000)
	libpostfix-dns.so.1 => /usr/lib/libpostfix-dns.so.1 (0x4003c000)
	libpostfix-util.so.1 => /usr/lib/libpostfix-util.so.1 (0x40040000)
	libdb3.so.3 => /usr/lib/libdb3.so.3 (0x4005d000)
	libnsl.so.1 => /lib/libnsl.so.1 (0x40105000)
```



```
    libresolv.so.2 => /lib/libresolv.so.2 (0x40119000)
    libgdbm.so.1 => /usr/lib/libgdbm.so.1 (0x4012a000)
    libc.so.6 => /lib/libc.so.6 (0x40130000)
    libdl.so.2 => /lib/libdl.so.2 (0x4024b000)
    /lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
```

上面的输出似乎表明 smtpd 守护进程一切正常，因为每个库依赖项都解析到了实际文件。但是，你可能运气不好，反而会看到这样的情况：

```
    # ldd `postconf -h daemon_directory`/smtpd
    libpostfix-master.so.1 => /usr/lib/libpostfix-master.so.1 (0x4001d000)
    libpostfix-global.so.1 => /usr/lib/libpostfix-global.so.1 (0x40023000)
    libpostfix-dns.so.1 => /usr/lib/libpostfix-dns.so.1 (0x4003c000)
    libpostfix-util.so.1 => /usr/lib/libpostfix-util.so.1 (0x40040000)
    libdb3.so.3 => not found
    libnsl.so.1 => /lib/libnsl.so.1 (0x4005d000)
    libresolv.so.2 => /lib/libresolv.so.2 (0x40071000)
    libgdbm.so.1 => /usr/lib/libgdbm.so.1 (0x40082000)
    libc.so.6 => /lib/libc.so.6 (0x40088000)
    libdl.so.2 => /lib/libdl.so.2 (0x401a3000)
    /lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
```

在这种情况下，`libdb3.so.3` 缺失。一个找不到所有共享库的程序将无法运行。如果你使用的是 Linux，并且安装了为其他发行版（甚至是你的发行版的其他版本）设计的 Postfix 软件包，那么你可能在运行时才会发现这类问题。如果情况如此，你需要做出决定。

最佳解决方案是找到适合你发行版的 Postfix 软件包，或者从源代码编译 Postfix（参见附录 A）。但是，如果你坚持尝试使用现有资源，你可以尝试这样查找 `libdb3.so.3`：

```
    # find / -name libdb3.so.3
    /usr/lib/libdb3.so.3
```

这个命令可能需要永远才能完成（因为它会搜索你的整个文件系统），但如果你足够幸运找到了这个库，你可以将其目录路径添加到 `/etc/ld.so.conf` 文件中，然后运行 `ldconfig`。当然，这可能会引发库和符号冲突。除非你真的知道自己在做什么，否则摆弄共享库几乎从来都不是个好主意。

`find` 命令甚至可能帮不上忙，因为该库可能根本不在你的系统上。如果是这种情况，你或许能找到包含该库的软件包。但是，如果你实在无法解决这个问题，你需要做出艰难的决定。如果找到一个可用的 Postfix 软件包似乎不可能，从源代码编译又显得令人生畏，你可能需要考虑更换操作系统或发行版。

## 连接到 Postfix

如果 Postfix 启动正常但行为不符合预期，请查看你的服务器是否确实在 25 端口上接受连接。连接到 SMTP 端口以确认。以下是一个成功连接的示例：

```
    # telnet localhost 25
    220 mail.example.com ESMTP Postfix
    QUIT
    221 Bye
```

你可能能够连接到回环接口，但这并不意味着整个互联网都可以。假设你的机器 IP 是 10.1.2.233。再次尝试，这次连接到该地址：

```
    # telnet 10.1.2.233 25
    220 mail.example.com ESMTP Postfix
    QUIT
    221 Bye
```

如果这不起作用，首先要检查你的 `main.cf` 文件，看看 `inet_interfaces` 是否被设置但排除了你尝试连接的 IP 地址。默认情况下会监听所有接口。

## 检查网络

如果 Postfix 配置看起来正常，并且 Postfix 已经重启，但你仍然无法建立连接，请检查网络的防火墙或 IP 过滤配置。你的系统可能默认阻止了该端口。有几个地方需要查看，因为 IP 过滤可能通过操作系统防火墙脚本（例如，调用 `iptables` 或 `ipf` 的脚本）进行，也可能在机器外部通过防火墙设备和路由器执行。

你必须到处检查。

如果到目前为止你的配置似乎正确，你需要检查本地网络之外的情况。你的互联网服务提供商可能会阻止传入到你 25 端口的流量（顺便说一句，也会阻止到其他机器 25 端口的出站流量）。如果你发现你的互联网服务提供商拒绝传入流量并且拒绝打开该端口，你唯一的办法就是更换互联网服务提供商。

要查看外部用户是否能连接到你，请运行此命令：

```
    # telnet relay-test.mail-abuse.org
```

当你建立此连接时，`relay-test.mail-abuse.org` 会执行针对发起连接机器的在线中继测试。如果你的互联网服务提供商（或你自己的防火墙）没有阻止到你机器 25 端口的传入连接，那么你应该在日志文件中看到相当多的消息。

如果你无法连接到上述主机，你可能遇到了名称解析问题。用以下命令测试它：

```
# host relay-test.mail-abuse.org
relay-test.mail-abuse.org is an alias for cygnus.mail-abuse.org.
cygnus.mail-abuse.org has address 168.61.4.13
```

你应该看到一个 IP 地址，如上面的输出所示。如果你没有看到，说明你无法解析主机名。你的 `/etc/resolv.conf` 或 `/etc/nsswitch.conf` 文件（或两者）可能不正确。情况可能更糟；你的机器甚至可能无法连接到互联网。尝试 ping 一些地址。成功的测试如下所示（使用 CTRL-C 停止测试）：

```
# ping 134.169.9.107
PING 134.169.9.107 (134.169.9.107): 56 data bytes
64 bytes from 134.169.9.107: icmp_seq=0 ttl=54 time=12.1 ms
64 bytes from 134.169.9.107: icmp_seq=1 ttl=54 time=12.1 ms
64 bytes from 134.169.9.107: icmp_seq=2 ttl=54 time=12.1 ms
--- 134.169.9.107 ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 12.1/12.1/12.1 ms
```

## 验证监听进程

如果 Postfix 正在运行且你的网络检查正常，但你的测试连接仍然不成功，请使用 `netstat` 命令查看 Postfix 是否确实在 25 端口上监听：

```
# netstat -t -a | grep LISTEN
tcp        0      0 *:printer              *:*                    LISTEN
tcp        0      0 localhost:domain       *:*                    LISTEN
tcp        0      0 *:ssh                  *:*                    LISTEN
tcp        0      0 *:smtp                 *:*                    LISTEN
```

上面的输出显示有服务器在 printer、domain、SSH 和 SMTP 端口上监听（查看 `/etc/services` 了解这些名称对应的数字端口）。你可以看到有东西在 25 端口（smtp）上监听。但是，这是 Postfix 还是其他东西？`lsof` 命令可以告诉你。尝试下面的命令。如果输出包括 `sendmail` 在 25 端口上监听，那么你旧的 `sendmail` 二进制文件仍然在运行：

```
# lsof -i tcp:25
COMMAND    PID USER   FD   TYPE DEVICE SIZE NODE NAME
sendmail 25976 root    4u  IPv4 228618       TCP mail.example.com:smtp (LISTEN)
```

终止此进程，并编辑你的系统启动文件，使其在重启后不会再次启动（如果可能，完全从你的系统中移除 Sendmail，因为记住，你应该运行的是 Postfix）。

> **注意** _lsof_ 是一个功能极其强大的工具，可以显示所有打开的文件（以及使用这些文件的进程），但它非常依赖于你的内核。确保你的 _lsof_ 是最新版本，并且与你当前的内核匹配。过时的 _lsof_ 对于网络连接根本不返回任何输出。如果不确定它是否工作，请运行 **lsof -i**。

如果你使用的是 Postfix，_lsof_ 的输出应该包括 Postfix 的 _master_ 守护进程在 25 端口上监听：

```
# lsof -i tcp:25
COMMAND  PID USER    FD   TYPE DEVICE SIZE NODE NAME
master  26079 root   11u  IPv4 228828     TCP *:smtp (LISTEN)
```

## 使 Postfix 使用你的配置设置

_main.cf_ 文件很长，可能难以阅读。一个配置选项可能出现两次，或者一个拼写错误可能隐藏在一堆注释中。使用 _postconf_ 命令来显示 Postfix 实际使用的配置。仅从行数就能看出差异：

```
# cd /etc/postfix
# wc -l main.cf
# postconf -n | wc -l
```

_postconf -n_ 的输出列出了 _main.cf_ 中所有参数设置，包括那些与默认值相同的参数。更改 _main.cf_ 时，你应该用 _postconf_ 验证你的更改，看看 Postfix 是否能识别它们。

你可能更喜欢使用命令 _postconf -e parameter=value_ 以编程方式将 _main.cf_ 中的参数编辑为 _value_。这个小技巧允许你使用 shell 脚本或 cron 任务来修改 Postfix 配置。

如果你正在处理一个配置问题，_postconf(5)_ 手册页值得一读。

## 报告 Postfix 问题

当你刚开始使用 Postfix 时，可能很难判断应该向 postfix-users@postfix.org 报告哪些信息。_postfinger_ 程序（由 Simon J. Mudd 开发）可以提取大多数相关信息。要了解它的作用，可以像这样将 _postfinger_ 的输出连同你自己的问题一起发送给自己：

```
# postfinger | /usr/sbin/sendmail youraddress@your.domain
```



当然，这假设你的系统上出站邮件能正常工作。当所有方法都失败时，你可以将输出转移到另一个系统。

如果你的问题与SMTP-AUTH及其使用的SASL相关，请使用Patrick的脚本saslfinger！saslfinger是一个bash工具脚本，旨在帮助你调试SMTP AUTH设置。该程序会收集关于Cyrus SASL和Postfix的各种系统信息并将其发送到标准输出。要查看其功能，可以像下面这样将saslfinger的输出连同你自己的问题一起通过邮件发送给自己：

```
# saslfinger -s | /usr/sbin/sendmail youraddress@your.domain
```

**注意** Postfinger自2.1版本起已成为Postfix源码发行版的一部分。你也可以从ftp://ftp.wl0.org/sources/postfinger获取它。
saslfinger并非Postfix源码发行版的一部分。你可以从http://postfix.state-of-mind.de/patrick.koetter/saslfinger获取它。

## 获取更多日志信息

如果你难以聚焦于Postfix特定组件的问题，可以按守护进程为单位增加日志信息量。通过在`/etc/postfix/master.cf`中守护进程配置条目后添加`-v`参数来实现，例如smtpd的配置示例：

```
# ===================================================================
# service type  private unpriv  chroot  wakeup  maxproc command + args
# (yes)   (yes)   (yes)   (never) (50)
# ==================================================================
smtp      inet  n       -       -       -       -       smtpd -v
```

要使更改生效，请重新加载Postfix。此时守护进程在工作时应该会输出非常详细的信息。如果这还不够，你甚至可以在条目中再添加一个`-v`，将获得更详细的输出。请确保在调试完成后恢复为正常设置，因为详细日志会在日志文件中生成大量记录，影响整体系统性能。

### 针对特定客户端的日志记录

如果你有一个繁忙的邮件服务器，提高所有客户端的日志级别会产生过多输出，你也可以使用`debug_peer_list`参数为特定客户端选择性增加日志。以下示例展示了如何仅为10.0.0.1和10.0.0.4客户端的smtpd日志设置更详细的输出：

```
debug_peer_list = 10.0.0.1, 10.0.0.4
```

你可以为该参数指定一个或多个主机、域名、地址和网络。要使更改立即生效，需要运行`postfix reload`命令。

### 日志与qmgr

一个常见问题是缺少qmgr进程的日志输出。队列管理器应该发出类似这样的日志条目：

```
Aug  5 17:05:26 hostname postfix/qmgr[308]: A44F828C71: from=<bamm@example.com>, size=153136, nrcpt=1 (queue active)
```

如果你缺少这些日志信息，可能有两个原因：

**libc问题**
libc实现存在缺陷（syslog客户端在syslogd服务器重启时不会重新连接）。如果是这种情况，你应该升级你的libc。

**qmgr在chroot环境下运行**
Postfix的qmgr进程在chroot环境下运行（参见master.cf），但chroot监狱内没有syslog套接字。请参阅syslog(8)手册页了解如何指定额外的套接字以及为Postfix chroot监狱指定套接字。

## 其他配置错误

有三种错误似乎经常发生：

**文件打开问题**
如果你在打开一个看似存在的文件时遇到问题，请检查它是否在配置文件中被指定为映射（例如，如果它以`hash:`前缀开头）。如果是这种情况，请对包含映射数据的纯文本文件运行`postmap`来创建索引版本。

此外，验证权限和所有权是否正确。不要忘记目录及其上级所有目录的可执行权限。

**权限问题**
如果你遇到权限问题，可以查看Postfix是否能通过post-install命令自动修复：

```
# /etc/postfix/post-install set-permissions upgrade-configuration
```

此命令除了修复权限问题外，还会相应地编辑`main.cf`和`master.cf`，因此在执行前最好备份你的配置。

**注释**
任何第一个非空格字符为井号（#）的行都是注释。Postfix不接受任何其他注释语法。如果`postconf`显示一个看起来陌生的参数，你可能在配置文件的某处错误地放置了#。

## chroot监狱的复杂性

太常见的是，能够以chroot方式运行会导致奇怪的问题。Postfix安装**永远不会**默认以chroot方式运行。可能出错的事情太多了，因此Wietse明智地选择*不*默认启用chroot。不幸的是，其他软件包维护者有时在安全特性上有点过于热衷。

Postfix守护进程在进入监狱前会打开所有它们的映射。但是，用于DNS查找、其他主机相关查找、网络服务查找、时区查找以及链接到Postfix的库中发生的其他事情所需的系统文件必须位于chroot监狱内。软件包维护者需要提供脚本，将必要的文件从文件系统的原始位置复制到监狱中。你通常需要`/etc/resolv.conf`和`/etc/nsswitch.conf`。Postfix源码发行版包含一个`examples/chroot-setup`子目录，其中包含在不同操作系统下设置chroot监狱的脚本。Matthias Andree编写了一个LINUX2脚本，用于在Linux上正确设置。

理论上，软件包维护者应该包含在你特定的操作系统或发行版上正确构建chroot监狱的机制。然而，如果你刚刚开始使用，可能会感到不知所措。与其纠正你根本不知道存在的chroot监狱，你可能应该取消Postfix守护进程的chroot设置，直到Postfix完全正常运行。编辑`/etc/postfix/master.cf`，查看每个条目：

```
# =============================================================================
# service type  private unpriv  chroot  wakeup  maxproc command + args
# (yes)   (yes)   (yes)   (never) (50)
# =============================================================================
smtp      inet  n       -       -       -       -       smtpd
```

chroot列中的连字符表示smtpd在chroot环境下运行。将其设置为`n`，然后重新加载Postfix。此外，请记住并非每个Postfix守护进程都能在chroot环境下运行。大多数可以，但如果你尝试以chroot方式运行pipe、local或virtual守护进程，你很可能会遇到奇怪的问题。

你将在第20章中找到更多关于chroot过程的信息。

## 解决文件系统问题

大多数现代Unix系统都提供日志文件系统，但这可能无法保护你免受偶尔的文件系统损坏，尤其是如果你有硬件问题或使用尚未完全调试的新奇文件系统。如果发生非常奇怪的事情，比如目录变成文件，请考虑立即重启并使用一系列命令对所有磁盘进行强制fsck：

```
# touch /forcefsck
# sync
# reboot
```

是的，你将没有漂亮的运行时间数字，用户也会抱怨，但不强制fsck你就无法修复文件系统问题。我们已经通过这种方式成功地让Red Hat和Debian上的许多用户感到烦恼。

## 库地狱

Postfix大量使用共享库，例如BerkeleyDB库。这个特定的库导致了很多问题，因为有太多不同的版本具有不同的磁盘数据格式。所有邮件服务组件，如Postfix、POP-before-SMTP、dracd、postgrey以及其他访问和修改`hash:`或`btree:`类型映射的工具，都需要使用兼容的BerkeleyDB库。

情况变得更糟：不同版本的BerkeleyDB的磁盘格式不兼容，这意味着一个应用程序可能无法读取由使用不同版本BerkeleyDB的另一个应用程序写入的映射。

要检查Postfix使用的库，请使用`ldd`命令，如“启动Postfix和查看日志的问题”一节所述：

```
# ldd `postconf -h daemon_directory`/smtpd
    libpcre.so.0 => /usr/local/lib/libpcre.so.0 (0x4001d000)
    **libdb-3.1.so => /lib/libdb-3.1.so (0x40028000)**
    libnsl.so.1 => /lib/libnsl.so.1 (0x400a1000)
    libresolv.so.2 => /lib/libresolv.so.2 (0x400b8000)
    libc.so.6 => /lib/libc.so.6 (0x400ca000)
    /lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
```

在前面的输出中，smtpd是针对BerkeleyDB-3.1.x链接的，因此所有其他需要共享Postfix `hash:`和`btree:`映射的程序必须使用相同版本的BerkeleyDB（或至少具有相同磁盘格式的版本）。

## 守护进程不一致

如果Postfix升级失败，或者你以非标准方式执行（例如直接从源码覆盖RPM安装而不是先删除旧版本），可能会发生奇怪的事情。你可能混合了来自不同版本Postfix的守护进程。



要查明守护进程属于哪个版本的 Postfix，可以对所有守护进程二进制文件使用 `strings` 命令，如下所示：

```
# strings /usr/libexec/postfix/smtpd | grep 2003
2.0.13-20030706
20030706
# strings /usr/libexec/postfix/cleanup | grep 2003
2.0.13-20030706
20030706
```

在这个例子中，版本（以日期表示）实际上是匹配的。我们在本例中使用 2003 作为年份，但如果你使用的版本来自其他年份，则应改为 grep 该年份。

## Fork 地狱

混合使用来自不兼容 Postfix 版本的守护进程会导致一个常见问题，这与 `tlsmgr` 守护进程有关。负载看起来会异常高，进程 ID 持续增加，但实际上并没有太多邮件流量或排队的邮件。

你可能升级了 Postfix，但保留了旧的 `tlsmgr` 和运行它的 `master.cf` 文件。

问题在于，新的 Postfix 会生成旧的 `tlsmgr`，但该守护进程会立即以状态 0 退出，因为它无法与新版本的 Postfix 协同工作。Postfix 不会记录任何内容，因为退出代码 0 是正常的。然而，Postfix 会立即重新生成 `tlsmgr`，这个过程会不断重复。

如果情况确实如此，首先注释掉 `master.cf` 中的 `tlsmgr` 行，然后重新加载 Postfix 以恢复正常服务。之后，你就可以使用兼容版本的 `tlsmgr` 完成升级。

## 压力测试 Postfix

要了解你的安装能处理多少邮件流量，你需要进行某种压力测试。为了给服务器施加足够的负载，你需要一个快速的邮件生成器。Postfix 自带了两个测试程序 `smtp-source` 和 `smtp-sink`，正是为此目的而设计。以下是它们的工作方式：

- **smtp-source** — 此程序连接到指定主机上的 TCP 端口（默认为 25），并发送一个或多个消息，可以是顺序或并行发送。该程序支持 SMTP（默认）或 LMTP 协议，旨在帮助测量服务器性能。

- **smtp-sink** — 此测试服务器监听指定的主机（或地址）和端口。它从网络接收消息并丢弃它们。你可以使用此程序测量客户端和网络性能。

让我们从 `smtp-source` 开始，对你的 Postfix 安装进行压力测试。以下示例向运行在 localhost 端口 25 上的 Postfix 服务器注入总共 100 条消息，每条 5KB，分 20 个并行会话发送。由于你还想知道这花了多长时间，所以使用 `time` 命令：

```
$ time ./smtp-source -s 20 -l 5120 -m 100 -c \
  -f sender@example.com -t recipient@example.com localhost:25
100
real    0m4.294s
user    0m0.060s
sys     0m0.030s
```

- `-s 20` — 20 个并行会话
- `-l 5120` — 5KB 消息大小
- `-m 100` — 共 100 条消息
- `-c` — 显示计数器
- `-f` — 信封发件人
- `-t` — 信封收件人
- 目标 SMTP 服务器

在这个例子中，注入花了 4.294 秒。你还想知道实际投递花了多长时间。请检查你的日志以确认，并验证为 `recipient@example.com` 到达的每一条消息都已接收。

现在，让我们将注意力转向 `smtp-sink`，以了解你的服务器每秒能处理来自你那糟糕的群发邮件软件的多少消息。Postfix 必须处理每条出站消息，即使另一端的服务器将其丢弃（因此你不能用它来测试你的邮件发送器的原始性能，除非你将邮件发送器直接连接到 `smtp-sink`）。

以下示例在 localhost 的 25 端口上设置了一个 SMTP 监听器：

```
$ ./smtp-sink -c localhost:25 1000
```

现在你可以运行你的客户端测试了。

如果你想了解网络带来了多少开销，并且想运行一个受控实验来查看邮件服务器的理论最大吞吐量，你可以让 `smtp-source` 和 `smtp-sink` 相互通信。打开两个窗口，在第一个窗口中，像这样启动虚拟服务器：

```
# ./smtp-sink -c localhost:25 1000
100
```

设置好之后，在另一个窗口中使用 `smtp-source` 向此服务器发送消息：

```
$ time ./smtp-source -s 20 -l 5120 -m 100 \
-f sender@example.com -t recipient@example.com localhost:25
100
real    0m0.239s
user    0m0.000s
sys     0m0.040s
```

此输出显示 `smtp-sink` 接受消息的速度比 Postfix 快得多。它只用了 0.239 秒就接受了消息，这比 Postfix 的注入过程快 18 倍。现在，如果你能像这样丢弃所有传入邮件，岂不美哉？

## 磁盘 I/O

当你运行压力测试时，你可能会在机器上遇到似乎不合常理的巨大平均负载。假设你没有设置任何内容过滤，那么 Postfix 受 I/O 限制，因此你的 I/O 子系统可能已饱和。

如果 `top` 的输出显示高负载，例如 10.7，但没有任何进程实际使用 CPU，那么你的负载可能来自内核使用大部分 CPU 进行 I/O 而不让进程运行。此外，内核进行如此多 I/O 的原因是，有更多进程请求了 I/O 操作（并且现在正在等待它们）。

Linux 2.6 内核支持在 `top` 命令中显示 iowait 状态。要在 2.4.x 内核（没有单独的方法显示 iowait 状态）上查看是否是这种情况，你可以添加一个内核模块。Oliver Wellnitz 编写了这样一个内核模块，你可以从 ftp://ftp.ibr.cs.tu-bs.de/os/linux/people/wellnitz/programming 下载。这个模块以不同的方式计算负载，并在 `/proc` 文件系统中提供一个你可以查看的接口，如下所示：

```
# cat /proc/loadavg-io
rq 0.30 0.23 0.14
io 0.08 0.31 0.27
```

在这个例子中，`rq` 是处于 TASK_RUNNING 状态的进程数，而 `io` 是处于 TASK_UNINTERRUPTIBLE（等待 I/O）状态的进程数。这两者之和就是内核通常所说的负载。

如果你遇到此类问题，你需要更快的磁盘，或者甚至使用诸如 SSD（固态磁盘——本质上是一个带电池备份的 RAM 磁盘）之类的解决方案，或者为队列目录使用镜像或条带化 RAID。有关更多信息，请参见第 22 章中的“入站队列瓶颈”部分。

另一个可能有效也可能无效的解决方案是移除队列目录的同步更新。如果你使用的是 ext2 或 ext3 文件系统，请尝试此命令：

```
# chattr -R -S /var/spool/postfix/
```

此设置实际上在新版本的 Postfix 安装中是默认的。

## 连接数过多

在设置邮件服务器时，你可能试图同时解决太多问题。如果你想拥有一个稳定的 Postfix 系统，请一次只修改一项。如果你要使用 LDAP 或 SQL，这一点尤其重要。尝试按以下步骤进行：

1. 构建你的系统*不使用* LDAP 映射（即使用 hash、btree 或 dbm 映射）。
2. 使用适当的 `ldapsearch` 命令从你的 LDAP 服务器提取所有必要的数据。使用脚本语言，如 Perl 或 Python，将数据重新格式化为 Postfix 映射文件输入。
3. 当你的 Postfix 在没有 LDAP 的情况下正常工作后，一次将一个映射替换为相应的 LDAP 映射。以 `postfix` 用户身份测试每个 LDAP 映射，如下所示：

```
$ postmap -q - ldap:mapname < keyfile
```

`keyfile` 包含要查询的地址（键）列表。如果映射返回有意义的数据，则更改相应的 `_maps` 配置参数以让 Postfix 使用该 LDAP 映射。

4. 为了整合打开的查找表数量，可以使用 `proxymap` 守护进程在多个 Postfix 进程之间共享一个打开的表，如第 5 章标题为“Postfix 守护进程”的部分所述。

## CIDR 和 SMTP 标准参考

本章的这一节首先解释了 Postfix 可在 `cidr:` 类型映射和 `mynetworks` 参数中使用的无类域间路由（CIDR）表示法。第二节引用了 RFC 2821 中可能的 SMTP 服务器响应代码。

### CIDR 表示法中的子网

在 CIDR 表示法中，IP 地址表示为 `A.B.C.D/`*n*，其中 *n* 称为 IP 前缀或网络前缀。IP 前缀标识用于识别网络的位数。例如，`192.9.205.22 /18` 表示前 18 位用于表示网络，其余 14 位用于标识主机。常见前缀有 8、16、24 和 32。



即使你声称自己从10岁起就开始玩电脑，并且是最早上网的人之一（在ARPANET这个词还有实际意义的那个年代），你可能仍然难以记住CIDR表示法中的子网掩码。表C-1列出了子网掩码及其等价表示。

## 表C-1：CIDR表示法中的子网

| CIDR前缀 | 子网掩码 | 二进制值 | 网络数量 |
| :--- | :--- | :--- | :--- |
| /1 | 128.0.0.0 | 10000000000000000000000000000000 | 128个A类域 |
| /2 | 192.0.0.0 | 11000000000000000000000000000000 | 64个A类域 |
| /3 | 224.0.0.0 | 11100000000000000000000000000000 | 32个A类域 |
| /4 | 240.0.0.0 | 11110000000000000000000000000000 | 16个A类域 |
| /5 | 248.0.0.0 | 11111000000000000000000000000000 | 8个A类域 |
| /6 | 252.0.0.0 | 11111100000000000000000000000000 | 4个A类域 |
| /7 | 254.0.0.0 | 11111110000000000000000000000000 | 2个A类域 |
| /8 | 255.0.0.0 | 11111111000000000000000000000000 | 1个A类域 |
| /9 | 255.128.0.0 | 11111111100000000000000000000000 | 128个B类域 |
| /10 | 255.192.0.0 | 11111111110000000000000000000000 | 64个B类域 |
| /11 | 255.224.0.0 | 11111111111000000000000000000000 | 32个B类域 |
| /12 | 255.240.0.0 | 11111111111100000000000000000000 | 16个B类域 |
| /13 | 255.248.0.0 | 11111111111110000000000000000000 | 8个B类域 |
| /14 | 255.252.0.0 | 11111111111111000000000000000000 | 4个B类域 |
| /15 | 255.254.0.0 | 11111111111111100000000000000000 | 2个B类域 |
| /16 | 255.255.0.0 | 11111111111111110000000000000000 | 1个B类域 |
| /17 | 255.255.128.0 | 11111111111111111000000000000000 | 128个C类域 |
| /18 | 255.255.192.0 | 11111111111111111100000000000000 | 64个C类域 |
| /19 | 255.255.224.0 | 11111111111111111110000000000000 | 32个C类域 |
| /20 | 255.255.240.0 | 11111111111111111111000000000000 | 16个C类域 |
| /21 | 255.255.248.0 | 11111111111111111111100000000000 | 8个C类域 |
| /22 | 255.255.252.0 | 11111111111111111111110000000000 | 4个C类域 |
| /23 | 255.255.254.0 | 11111111111111111111111000000000 | 2个C类域 |
| /24 | 255.255.255.0 | 11111111111111111111111100000000 | 1个C类域 |
| /25 | 255.255.255.128 | 11111111111111111111111110000000 | 128台主机 |
| /26 | 255.255.255.192 | 11111111111111111111111111000000 | 64台主机 |
| /27 | 255.255.255.224 | 11111111111111111111111111100000 | 32台主机 |
| /28 | 255.255.255.240 | 11111111111111111111111111110000 | 16台主机 |
| /29 | 255.255.255.248 | 11111111111111111111111111111000 | 8台主机 |
| /30 | 255.255.255.252 | 11111111111111111111111111111100 | 4台主机 |
| /31 | 255.255.255.254 | 11111111111111111111111111111110 | 2台主机 |
| /32 | 255.255.255.255 | 11111111111111111111111111111111 | 1台主机 |

## 服务器响应代码

以下服务器响应代码可以帮助你理解日志消息，或设置与Postfix默认设置不同的响应代码。这些代码摘自RFC 2821第4.2节。

### 4.2.1 响应代码的严重级别与原理

回复的三个数字各有特殊含义。第一个数字表示响应是好的、坏的还是不完整的。一个简单的SMTP客户端，或收到意外代码的客户端，可以通过检查这个第一个数字来确定下一步操作（按计划继续、重试、撤回等）。想要了解大致发生了什么类型错误（例如，邮件系统错误、命令语法错误）的SMTP客户端可以检查第二个数字。第三个数字及可能存在的补充信息用于最细粒度的信息表示。

响应代码的第一个数字有五个取值：

#### 1yz 正面初步回复

命令已被接受，但请求的操作被暂时搁置，等待对此回复中信息的确认。SMTP客户端应发送另一个命令来指定是继续还是中止该操作。

**注意** *未扩展的SMTP没有任何允许此类回复的命令，因此也没有继续或中止的命令。*

#### 2yz 正面完成回复

请求的操作已成功完成。可以发起新的请求。

#### 3yz 正面中间回复

命令已被接受，但请求的操作被暂时搁置，等待接收更多信息。SMTP客户端应发送另一个命令来指定此信息。此回复用于命令序列组中（即在DATA命令中）。

#### 4yz 瞬态负向完成回复

命令未被接受，请求的操作未执行。但是，错误状态是暂时的，可以再次请求该操作。发送方应返回到命令序列的开头（如果有的话）。当两个不同的站点（接收方和发送方的SMTP代理）必须就解释达成一致时，很难确定"瞬态"的含义。此类别中的每个回复可能有不同的时间值，但建议SMTP客户端重试。判断一个回复属于4yz还是5yz类别（见下文）的经验法则是：如果在命令形式或发送方/接收方属性没有任何改变的情况下重复该回复可以成功，则该回复为4yz（即命令被完全相同地重复，且接收方没有部署新的实现）。

#### 5yz 永久负向完成回复

命令未被接受，请求的操作未执行。不建议SMTP客户端重复完全相同的请求（在同一序列中）。即使某些"永久性"错误状态也可以被纠正，因此用户可能希望在未来的某个时刻直接指示SMTP客户端重新发起命令序列（例如，在拼写更正后，或用户更改了账户状态之后）。

[ . . . ]

### 4.2.3 响应代码按数字顺序排列

- 211  系统状态，或系统帮助回复
- 214  帮助信息
  （关于如何使用接收方或某个特定非标准命令含义的信息；此回复仅对人类用户有用）
- 220  \<domain\> 服务就绪
- 221  \<domain\> 服务关闭传输通道
- 250  请求的邮件操作正常，已完成
- 251  用户非本地；将转发至\<forward-path\>
  （参见第3.4节）
- 252  无法验证用户，但将接受消息并尝试投递
  （参见第3.5.3节）
- 354  开始邮件输入；以\<CRLF\>.\<CRLF\>结束
- 421  \<domain\> 服务不可用，关闭传输通道
  （如果服务知道必须关闭，可以作为对任何命令的回复）
- 450  请求的邮件操作未执行：邮箱不可用
  （例如，邮箱忙）
- 451  请求的操作中止：处理中出现本地错误
- 452  请求的操作未执行：系统存储空间不足
- 500  语法错误，命令无法识别
  （可能包括命令行过长等错误）
- 501  参数或参数中存在语法错误
- 502  命令未实现（参见第4.2.4节）
- 503  命令顺序错误
- 504  命令参数未实现
- 550  请求的操作未执行：邮箱不可用
  （例如，邮箱未找到、无访问权限，或因策略原因拒绝命令）
- 551  用户非本地；请尝试\<forward-path\>
  （参见第3.4节）
- 552  请求的邮件操作中止：超出存储配额
- 553  请求的操作未执行：邮箱名称不被允许（例如，邮箱语法不正确）
- 554  事务失败（或者，在连接建立响应的情况下，"此处无SMTP服务"）

版权所有 (C) 互联网协会 (2001)

本文档及其译本可以被复制并提供给他人，对本文档进行评论或以其他方式解释或协助其实现的衍生作品可以被准备、复制、发布和分发，全部或部分，不受任何限制，前提是上述版权声明和本段落包含在所有此类副本和衍生作品中。但是，本文档本身不得以任何方式修改，例如删除版权声明或对互联网协会或其他互联网组织的引用，除非出于制定互联网标准的目的，在这种情况下必须遵循互联网标准过程中定义的版权程序，或需要将其翻译成英语以外的其他语言。



## 术语表

### A

**A 记录** 在 DNS 中，将主机名映射到 IP 地址的记录。

**Active Directory** 微软的目录服务。它是一个集中式系统，用于分发与用户、网络和安全设置相关的数据。可以将其视为带有 Kerberos 的 LDAP，但具有增值性的、不符合标准的特性。

**Active Directory 服务接口 (ADSI)** 一种 API，使脚本或 C/C++ 程序的程序员能够轻松查询和操作 Active Directory 中的对象。

**附件** 电子邮件中的文件。

### B

**base64 编码** 一种数据编码方案，将二进制编码数据转换为可打印的 ASCII 字符。它是互联网电子邮件中使用的 MIME 内容传输编码之一。

**密件抄送** 一种电子邮件头，标记为 bcc:，列出应发送消息的地址，收件人看不到这些地址。*另请参阅* 抄送。

**布尔值** 一种保存真值的变量，要么为真，要么为假。

### C

**抄送** 一种电子邮件头，标记为 cc:，列出应发送消息的次要地址，所有收件人都可见。

**证书** 一个包含用于证明人或机器身份信息的文件。

**认证机构 (CA)** 一个颁发和管理数字身份的权威机构。

**chroot** chroot() 系统调用为进程指定一个新的根目录。

**CNAME 记录** 在 DNS 中，CNAME 记录，也称为规范名称，是一种扩展别名的记录。根据涉及的 DNS 树（正向或 in-addr.arpa），CNAME 可以指向 A 记录或 PTR 记录。*另请参阅 A 记录和 PTR 记录。*

**注释** 配置文件或源代码中的说明，提供有关配置或代码片段的有用信息。

### D

**守护进程** 在计算机后台运行并提供服务的进程。

**DCF-77** 在长波频率 77.5 kHz 上发送的编码时间信号。德国物理技术研究所 (http://www.ptb.de) 是该信号的官方来源，为德国分发正确的时间。任何人都可以使用此信号将设备同步到官方时间。

**非军事区** 私有网络和公共网络之间的中立区域，允许来自公共网络的用户受控地访问私有网络提供的数据。*另请参阅防火墙。*

**拨号用户列表 (DUL)** 一种 RBL 风格的黑名单，包含已知拨号池的 IP 地址。

**字典攻击** 指通过遍历可能的列表（通常是字典中的单词列表）来获取收件人的地址。

**发行版** 一个操作系统集合，包含内核、操作系统、各种免费软件，有时还包含专有软件。该术语最常用于 Linux。

**域** 一组计算机，其主机名共享一个公共后缀，即域名。*另请参阅顶级域名、域名服务 (DNS)。*

**域名服务 (DNS)** 一种通用、分布式且复制的数据查询服务，主要用于互联网上将主机名转换为互联网地址。

**动态 IP 地址** 在连接到网络时，从 IP 地址池分配给计算机网络接口的 IP 地址。

**动态链接** 一种程序执行系统，操作系统在可执行文件运行时加载并链接库代码。*另请参阅库。*

### E

**扩展简单邮件传输协议 (ESMTP)** 对原始 SMTP 协议的一组扩展，使邮件客户端能够询问邮件服务器其功能。

**外部应用程序** Postfix 之外的应用程序，例如病毒扫描器或脚本。

### F

**误报** 当测试错误地将条件报告为真时发生。

**防火墙** 控制私有网络和公共网络之间入站和出站连接的网关服务器。它还可以提供从外部对非军事区的受控访问。*另请参阅* 非军事区。

**先进先出 (FIFO)** 处理请求或数据的系统。队列是 FIFO；先进入的首先被处理。其思想始终是首先处理最旧的请求。

**完全限定域名 (FQDN)** 系统的完整名称，由其本地主机名和域名组成，包括顶级域名。例如，mail 是主机名，mail.example.com 是 FQDN。FQDN 应足以确定互联网上任何主机的唯一互联网地址。这个过程（称为*名称解析*）使用域名服务 (DNS)。

### G

**群件** 一个高度集成的应用程序，由几个程序组成，提供各种服务，如电子邮件、时间规划、地址数据库和新闻服务。

### H

**十六进制** 一种以 16 为基数的数字系统，通常使用符号 0–9 和 A–F 或 a–f 编写。

### I

**包含文件** 包含（头）文件包含编译软件所需的功能原型、常量定义和宏。大多数包含文件对应于一个库。*另请参阅* 库。

**互联网号码分配机构 (IANA)** 互联网协议中各种分配号码的中央注册机构，例如端口、协议、企业编号、选项、代码和类型。

**互联网消息访问协议 (IMAP)** 一种允许客户端访问和操作服务器上电子邮件消息的协议。它允许以与本地邮箱功能等效的方式操作远程消息文件夹（邮箱）。IMAP 包括创建、删除和重命名邮箱；检查新消息；永久删除消息；搜索；以及选择性获取消息属性、文本及其部分内容的操作。它没有指定发送邮件的方式；此功能由邮件传输协议（如 SMTP）处理。

**进程间通信 (IPC)** 一种应用程序编程接口 (API) 和底层支持，允许多个正在运行的进程相互通信。

### K

**内核** 操作系统的基础。内核负责为各种计算机程序提供对机器硬件的安全访问。

### L

**左侧 (LHS)** 在具有两列的映射中，左侧是左列。在 Postfix 中，条目的左侧称为键。

**库** 一个预编译机器代码的集合，可以在编译程序时链接。库作为其他程序的辅助代码。*另请参阅* 包含文件。

**轻量级目录访问协议 (LDAP)** 一种用于访问在线目录服务的协议。它定义了一个相对简单的协议，用于在 TCP/IP 上运行的目录的更新和搜索。

**本地邮件传输协议 (LMTP)** SMTP（简单邮件传输协议）的衍生协议。*另请参阅简单邮件传输协议 (SMTP)。*

### M

**宏** 一个简短的指令，可展开为一组更大的指令。

**邮件交换记录 (MX 记录)** 一种 DNS 资源记录，指示为主机名处理电子邮件的主机。

**邮件用户代理 (MUA)** 一个允许用户撰写和阅读电子邮件的程序。MUA 提供用户和消息传输代理 (MTA) 之间的接口。传出邮件最终传输到 MTA 进行投递，传入消息从邮件投递代理 (MDA) 留下的位置获取。

**恶意软件 (malware)** 对计算机有害的程序或文件。

**中间人攻击** 描述攻击者位于双方通信之间的攻击。攻击者能够在双方不知情的情况下读取和修改双方之间发送的消息，从而知道他们之间的链接已被破坏。

**映射** Postfix 中的映射是一个两列的表，其中每一行代表一个条目，将键与值相关联。键和值有时被称为左侧和右侧。*另请参阅* 左侧 (LHS)、右侧 (RHS)。



### N

**名称解析** 将主机名解析为 IP 地址的过程。

**网络地址转换（NAT）** 有时也称为网络伪装或 IP 伪装，网络地址转换是计算机网络中使用的一种技术，允许私有网络通过单一点访问公共网络。它依赖于对经过路由器或防火墙的网络数据包的 IP 地址进行重写。

**网络时间协议（NTP）** 一种用于将计算机时钟与某个时间参考同步的互联网协议。NTP 是一个互联网标准协议，最初由特拉华大学的大卫·L·米尔斯教授开发。

### O

**开放代理** 一个配置错误的代理服务器，它处理来自第三方的连接请求。开放代理可用于通过该开放代理向服务器提交邮件。

**开放中继** 一种在第三方之间转发邮件的 SMTP 服务器。当邮件服务器处理的邮件消息中，发送方和接收方均非本地用户时，即发生了第三方消息中继。

### P

**补丁** 对一段代码的（临时）添加，通常用于修复现有错误或提供新功能。

**端口** （网络）端口是通过网络与计算机程序进行通信的接口。网络端口通常有编号，网络实现（如 TCP 或 UDP）会在其发送的数据上附加一个端口号；接收方的实现则使用附加的端口号来确定将数据发送给哪个计算机程序。

**邮局协议（POP）** 一种从服务器检索电子邮件的协议。消息会立即从服务器下载。另请参阅互联网消息访问协议（IMAP）、简单邮件传输协议（SMTP）。

**良好隐私加密（PGP）** 一种提供加密隐私和身份验证的计算机程序。

**代理** 代表另一台服务器行事的服务器，通常以透明方式运行。

**PTR 记录** 在 DNS 中，将 IP 地址映射到主机名的记录。

### Q

**快速邮件队列协议（QMQP）** QMQP 在主机集群内提供集中式邮件队列。一台中央服务器运行消息传输代理。其他主机没有自己的邮件队列；它们通过 QMQP 将每条新消息交给中央服务器。QMQP 由 D.J. Bernstein 发明，他也是 qmail 的发明者。

### R

**独立磁盘冗余阵列（RAID）** 一种在多个磁盘上存储数据的方法。RAID 系统中的所有磁盘对操作系统来说都表现为单个磁盘。RAID 系统可以平衡 I/O 操作，从而提高性能。

**正则表达式** 正则表达式（缩写为 regexp、regex 或 regxp）是一种高级模式匹配系统，它实际上是一个接受特定语言的非确定性有限状态自动机的结果。

**征求意见稿（RFC）** 来自互联网工程任务组（IETF）的正式文件。RFC 可以是信息性的，也可以旨在成为互联网标准，并提供网络和应用程序之间的互操作性。虽然不能修改 RFC，但可以编写新的 RFC 来取代现有的 RFC。

**右侧（RHS）** 在一个包含两列的映射中，右侧是最后一列。在 Postfix 中，条目的右侧称为值。

**root** 参见超级用户。

**路由器** 一种计算机网络设备，它确定数据包在通往目的地的路径上应该转发到的下一个网络节点。

### S

**安全多用途互联网邮件扩展（S/MIME）** 一种用于安全发送电子邮件的互联网标准。它描述了如何将加密信息和数字证书作为邮件正文的一部分包含在内。

**安全套接层（SSL）** 参见传输层安全（TLS）。

**Sendmail** 互联网上最古老且使用最广泛的 MTA 之一。

**简单认证和安全层（SASL）** 在 RFC 2222（ftp://ftp.rfc-editor.org/in-notes/rfc2222.txt）中定义的一种认证框架，适用于使用基于 IMAP、LDAP 或 SMTP 等协议连接的应用程序。它为这些应用程序提供认证服务，并可在众多数据后端中查找用户数据。

**简单邮件传输协议（SMTP）** 在 STD 10、RFC 821 中定义的一种协议，用于在计算机之间传输电子邮件。参见 http://www.faqs.org/rfcs/std/std-index.html。

**结构化查询语言（SQL）** 一种用于与数据库交互的编程语言。

**超级用户** 又称 root，超级用户是在 Unix 风格操作系统中拥有所有模式（单用户或多用户）下所有权限和权限的用户。

### T

**tarpit** 计算机系统（通常是服务器）上的一种服务，它尽可能地延迟传入连接。tarpit 使网络滥用（如垃圾邮件或字典攻击）的效果降低，因为攻击者处理攻击所需的时间太长。这个名称类比于焦油坑，动物在其中会陷入困境并缓慢沉入表面以下。也以德语名称*teergrube*而闻名。

**telnet** 互联网上使用的一种网络协议。它也是一个程序的名称，用于调用到远程主机的 telnet 会话。

**顶级域名** 互联网完全限定域名的最后一个也是最重要的组件，即最后一个点之后的部分。例如，主机 mail.example.com 位于 com 顶级域名中（用于商业机构）。

**传输层安全（TLS）** TLS（前身为 SSL）是一种用于加密客户端和服务器之间通信层的协议。不应将其与 S/MIME 和 PGP 等电子邮件加密技术混淆，后者加密的是内容而非通信。

### U

**Unix** 1969 年起源于贝尔实验室的一种操作系统。

**Unix 域套接字** Unix 域套接字（正确的标准 POSIX 术语为 POSIX 本地 IPC 套接字）主要作为进程间通信的手段，因此也称为 IPC 套接字。这些连接是从本地计算机到其自身的；它们不是实际通过物理网络传输的连接。

**Unix 到 Unix 复制协议（UUCP）** 一种 Unix 实用程序和协议，允许一个 Unix 系统通过串行线路向另一个系统发送文件，该线路可以是从一台机器的串行端口直接连接到另一台的电缆，也可以是在电话线两端各使用一个调制解调器。

也有软件可以允许 UUCP 通过以太网工作，但有更好的替代方案，例如用于文件传输的 scp、用于电子邮件的 SMTP 和用于新闻的 NNTP。

**未经请求的商业电子邮件（UCE）** UCE 是垃圾邮件的一种更精确的表达方式。UCE 不应与收件人自愿订阅的商业电子邮件混淆。

### W

**空白字符** 空白字符是任何占据空间但不在屏幕上显示的字符。
