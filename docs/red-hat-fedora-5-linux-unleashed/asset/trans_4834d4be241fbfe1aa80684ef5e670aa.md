
除了基本程序之外，还有丰富的插件和扩展，它们可以将 Firefox 的功能提升至超越简单网页浏览的层面。诸如 Shockwave Flash 和 Java 等插件可即时提供，用于观看视频内容的多媒体编解码器也可随时使用，而扩展则为浏览体验提供了实用且有时趣味的附加功能。例如，ForecastFox 是一个扩展，可提供当地天气状况，而 Bandwidth Tester 则是一个计算当前带宽的工具。随着 Firefox 的发展，你将可以使用越来越多的扩展和插件来提升浏览乐趣。

## 摩祖拉套件（Mozilla Suite）

摩祖拉套件是微软 Internet Explorer 面临的首个重大竞争对手。在 20 世纪 90 年代末的浏览器大战中，Netscape 几乎被微软碾碎后，Netscape 的一群员工决定将他们现有的浏览器及相关应用程序开源。由此产生的是摩祖拉套件，它构成了后续 Netscape 版本的基础。Firefox 诞生于摩祖拉（Mozilla），并得益于摩祖拉基金会（Mozilla Foundation）的开创性工作而得以存在。

摩祖拉套件不仅仅是一个互联网浏览器；它包含电子邮件和新闻阅读器组件、一个简单的网页设计组件、一个 IRC 客户端以及一个地址簿。目前我们只关注浏览器组件，其他组件将在后文介绍。请记住，如果你安装摩祖拉，也会获得套件中的其他组件：邮件和新闻组阅读器、地址簿以及 IRC 客户端。如果你不需要所有这些，使用 Firefox 可能是更好的选择。

![](img/2045828cf45e5632bf056f9ca99d6755_248_0.png)

**图 8.2** 摩祖拉套件，Firefox 的先驱，Netscape 的继承者。

Fedora 默认包含摩祖拉套件，尽管它并未列在“互联网”菜单中。如果你在桌面上右键点击并选择**新建终端**（New Terminal）以切换到终端，可以通过输入 `mozilla` 来启动摩祖拉。摩祖拉的默认主题相当复古，让人回想起早期版本的 Netscape，但你可以轻松更改：点击**查看**（View）菜单，然后点击**应用主题**（Apply Theme）条目，最后选择**现代**（Modern）。你需要重启摩祖拉才能使新主题生效。

## Epiphany

Epiphany 是随原生 GNOME 桌面环境提供的浏览器（参见图 8.3）。它非常基础，构建在与 Firefox 和此前的摩祖拉相同的 Gecko 渲染引擎之上，当前版本已在多个领域取得进步。有些人喜欢 Epiphany 的简洁，而另一些人使用它仅仅是因为它就在那里。如果你想要真正的 GNOME 体验，应该选择 Epiphany。

![](img/2045828cf45e5632bf056f9ca99d6755_249_0.png)

**图 8.3** Epiphany，标准的 GNOME 网络浏览器。

## Konqueror

KDE 用户可以选择使用 Konqueror，这是 KDE 的默认浏览器（参见图 8.4）。除了处理文件系统导航外，Konqueror 还可用于浏览网页。它同样基于 Firefox、摩祖拉和 Epiphany 中所使用的 Gecko 渲染引擎。

![](img/2045828cf45e5632bf056f9ca99d6755_250_0.png)

**图 8.4** Konqueror，标准的 KDE 网络及文件浏览器。

## 选择电子邮件客户端

在 UNIX 时代，有各种基于文本的电子邮件客户端，如 elm 和 pine（Pine Is Not Elm）。尽管它们界面简陋，但允许普通用户互动处理邮件，无论是撰写还是阅读通信。随着主流计算的出现以及人们意识到需要友好的 GUI 界面才能提高生产力，涌现了海量的电子邮件客户端，其中一些是跨平台的，兼容 Linux、Windows 和 Mac OS X，甚至包括 UNIX。

### 电子邮件术语简介

电子邮件世界充满了缩写和技术术语。此处介绍的第一类术语描述了电子邮件系统的组成部分。一些应用程序融合了这三类功能。

邮件用户代理（MUA）、邮件客户端或邮件阅读器允许用户阅读和撰写邮件。这是大多数用户最熟悉的应用程序；它向用户提供文本或图形界面。示例包括 Evolution、Balsa、mutt、Mozilla Mail 和 KMail。Fedora Core 均提供这些客户端。

**邮件传输代理（MTA）**在幕后工作，用于在计算机之间发送和接收邮件。示例包括 Sendmail、Postfix、Fetchmail、Exim 和 Qmail。除最后两者外，**Fedora Core** 均提供。**邮件投递代理（MDA）**类似于 MTA，但不处理系统之间的投递，也不像 MUA 那样为用户提供界面。示例可以是 **Procmail** 或 **Spamassassin**，它们都为 MTA 提供过滤服务，其中后者由 **Fedora Core** 提供。

电子邮件使用的协议是缩写的温床；这些将在下文介绍。

- **RFC**—**请求评论**（Request For Comments）是接近互联网规则手册的文件。请参见本章末尾的“参考”部分以获取特定 RFC 的链接。通过更改链接中的数字，你可以查看任何特定的 RFC。如果你安装了 Fetchmail，作者 Eric S. Raymond 包含了一个相关 RFC（带描述）的列表，该列表位于文件 `/usr/share/doc/fetchmail/NOTES` 中。
- **POP**—由 RFC-1939 定义，**邮局协议**（Post Office Protocol）是一种向客户端投递邮件的邮件服务器。（它不用于向服务器发送邮件；那是 SMTP，稍后介绍。）当你在一台计算机上只有一个邮件客户端时，POP3 非常有用，例如典型的家庭用户。POP3 设计用于本地访问邮件；它将所有邮件从中央服务器下载到本地客户端，然后删除服务器上的文件。大多数 ISP 提供 POP3 邮件访问。
- **IMAP**—它是互联网**邮件访问协议**（Mail Access Protocol），允许用户访问存储在远程服务器上的邮件，而不是本地磁盘。这意味着如果用户使用支持 IMAP 的邮件客户端，可以从任何地方访问电子邮件。IMAP 是向局域网（LAN）提供邮件服务的良好解决方案。Fedora Core 提供的版本是华盛顿大学 IMAP 服务器，位于 http://www.washington.edu/imap/。
- **SMTP**—由 RFC-821 定义，它是用于从一个网络向另一个网络发送邮件的**简单邮件传输协议**（Simple Mail Transport Protocol）。这是一种服务器到服务器的协议，因此必须使用其他方法将消息投递到客户端应用程序以供用户阅读。该协议的扩展功能为基本协议添加了认证和错误消息。
- **MIME**—由 RFC-1341、1521、1522、1523、1820 以及许多其他定义，**多用途互联网邮件扩展**（Multipurpose Internet Mail Extensions）解决了电子邮件消息的格式问题，以包含非 ASCII 文本、编码的二进制图像和多媒体内容。

当然，这并非详尽的列表，也未打算做到。你可能会发现 jargoogle 搜索页面有助于 decipher 其他你遇到的陌生术语。它位于 http://www.tuxedo.org/~esr/jargon/jargoogle.html。

> **注意**
>
> 海量垃圾邮件和利用伪造标头的互联网骗局激起了对“更好捕鼠器”的兴趣。其中一个项目是位于 http://amtp.org 的 AIMP，它是 SMTP 的一种增强。该规范要求邮件服务器需要签署安全证书并使用 TLS（传输层安全，RFC2246）。AMTP 邮件服务器不会中继来自“不可信来源”的邮件——换句话说，即缺乏适当认证的邮件服务器。虽然 AMTP 不能根除垃圾邮件，但它确实提供了一种识别来源的机制。

Evolution 是 Ximian/Novell 的产品，是随 Fedora 提供的标准电子邮件客户端（参见图 8.5）。如果你使用过 Microsoft Outlook，Evolution 的界面不会让你感到意外。它实际上是 Outlook 的直接替代品，涵盖了 Outlook 的许多功能和优点，包括电子邮件、日历、联系人管理和任务管理。在此我们研究如何配置 Evolution 以访问电子邮件。

![](img/2045828cf45e5632bf056f9ca99d6755_252_0.png)

**图 8.5** Ximian Evolution，Fedora 的默认且功能极其强大的电子邮件客户端。

要成功配置 Evolution，你需要拥有以下信息：

- 你的电子邮件地址
- 你的入站邮件服务器名称和类型（即 pop.email.com，POP 和 IMAP）
- 你的入站服务器用户名和密码
- 你的出站邮件服务器名称（即 smtp.email.com）

收集齐所有信息后，你可以启动 Evolution。首先呈现给你的屏幕是账户设置辅助（参见图 8.6）。

下一个屏幕允许你配置 Evolution 使用你的 MTA。你可以选择 POP、IMAP、位于 `/var/mail` 的本地邮箱（采用 mbox 或 maildir 格式）、本地 MTA，或者如果你想仅使用 Evolution 的其他功能，可以选择“无”（None）。如 图 8.7 所示，你还可以设置密码。

