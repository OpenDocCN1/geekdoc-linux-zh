
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

- 7. 你的测试文章应该出现，带有你的博客标题和描述，以及你发布文章的日期时间。

有关操作博客的更多信息，请访问 http://www.blosom.com 网站。

## Movable Type 和 Typepad

`Movable Type` (`MT`) 被许多人认为是网络博客应用的黄金标准。它以安装有些困难而闻名，但它的功能如此丰富，这种中等的痛苦是值得的。许多技术倾向型博客运行 `MT`，许多企业和新闻组织也是如此。

`Typepad` 是由 `Movable Type` 开发者设立类似于 `Blogger` 的托管服务。`Typepad` 让你能够轻松制作高质量的 `MT` 类型博客，而无需管理安装。他们通过对基础用户收取极低费用（写为 4.95 美元）使其成为了一项长期业务。

`MT` 运行在几乎每一个平台上，并可以使用你喜欢的任何 Web 服务器或数据库应用程序。它有一个供个人使用的免费版本，但如果你想让你的博客有多个作者，就需要付费版本（少于 100 美）。

## 使用 WordPress 写博客

`WordPress` 是一个非常流行的系统，但运行起来有点复杂。它由 `MySQL` 数据库驱动，在开始之前必须运行该数据库。你的 Web 主机可能会支持数据库驱动的网站，但你应该提前检查。

同样，如果你想在本地系统上尝试 `WordPress`，你将必须安装并运行 `MySQL` 和 `PHP`。使用 `YaST` 安装 `PHP` 和 `MySQL` 软件包。

设置 `WordPress`：

- 1. 访问 http://www.wordpress.org/latest.tar.gz 下载当前版本。
- 2. 将 tar 包解压到任何目录（你的家目录即可，因为它会创建 `WordPress` 目录）。
- 3. 在 `YaST` 中创建一个 `WordPress` 用户。将其命名为 `wpress`。
- 4. 创建一个新的 `MySQL` 数据库。从 root shell 中，使用 `/usr/bin/mysqldadmin -p create wordpress`。
- 5. 登录 `WordPress` 数据库：`/usr/local/bin/mysql -p -u root GRANT ALL PRIVILEGES ON wordpress TO wpress@localhost IDENTIFIED BY password; GRANT ALL PRIVILEGES ON wordpress TO wordpress IDENTIFIED BY password;` 完成后，输入 `exit`。
- 6. 从 shell 或你的文件管理器，将你在第 2 步中创建的 `WordPress` 目录的内容复制到 `/public_html`。如果你已经在那里有内容（或想让你的博客成为大型网站的一部分），请复制整个目录。
- 7. 打开浏览器并访问你提取 `WordPress` 的目录 `http://localhost/wp-admin`。安装屏幕会检查一切是否正常，并偶尔向你提问。
- 8. `WordPress` 为管理员生成一个密码。登录并发布。你会看到一个非常直观的界面。`WordPress` 网站还提供插件和模板，以进一步定制你的体验。

## 热门博客服务

最大且最知名的博客服务通常为你的博客提供托管以及在其服务器上的免费存储空间。有些服务提供通过邮件发送文章的选项，这是一种方便的工具。以下是你通过这些服务可以做到的快速概述。

### Blogger (www.blogger.com)

博客圈中最知名且最容易入门的平台。基础账户是免费的，并且有许多模板可以选择。在许多方面，`Blogger` 是博客行业中最古老的；它是人们开始的地方。`Blogger` 涵盖了各种风格，但倾向于个人日记类。文章有三种发布方式：基于网页的。

*(注：由于您提供的文本在 Blogger 之后出现了大量逻辑重复和截断，以上翻译仅包含您提供的有效内容部分)*

## 第 14 章 创建基础网站

- *kdewebdev.org*—KDE WebDev 站点，用于 Quanta 及其辅助工具。
- *bluefish.openoffice.nl*—Bluefish，基于 GTK 的网页编写工具。
- *bfwiki.telfelsen.net*—Bluefish Wiki，开发团队在此向我们发布最新进展。
- *www.screem*—用于 HTML 和 XML 文件的 GNOME/GTK 编辑器。
- *www.ndepak.info/stuff/vtu/ginf*—“Ginf 不是 FrontPage”，另一个简化网页编写的尝试。
- *webmoney.wired/webmoney*—全能在线网页设计学校。提供各种技能水平的各种网络技术教程，从基础 HTML 到 Apache 以及 ColdFusion。像《Wired》杂志一样，这些页面偶尔会涉及非正规内容。
- *webdesign.about.com*—关于网站设计的实用建议。提供 HTML 和 CSS 样式工具的免费在线课程。
- *radio.weblogs.com/0120449*—来自元宇宙的笔记，作者的技术博客。包含许多与开源软件和 SUSE Linux 相关的链接和新闻。
- *www.planetsuse.org*—Planet SUSE，SUSE Linux 开发者的小组博客。
- *directory.google.com/Top/Computers/Internet/On_the_Web/Blogs*—博客工具和服务的当前目录。你可以在这里找到一些资源。
- *www.blosxm*—下载并学习 Blosxm，一种基于 CGI 的博客工具。
- *www.billclair.com/blogmax*—Eccles 的博客编辑器。
- *wordpress.org*—WordPress 博客和内容管理工具。拥有活跃且实用的支持论坛。
- *www.blogger.com*—仍然是开始博客最简单最便宜的方法。现在由 Google 管理。
- *www.sixapart.com*—Movable Type 和 Typepad 背后的公司。可以通过公司页面博客访问其任一产品。
- *www.livejournal.com*—LiveJournal 是一个用于更多个人博客和建立同类博主社区的地方。
- *radio.weblogs.com/0120385/2003/04/24.html#a329*—关于如何在 Wine 下运行 Windows 博客程序 Radio Userland 的描述。
- *http://akregator.sourceforge.net/index.php*—用于 KDE 的 Akregator 阅读器。

## 第 15 章

## 本章内容

- 电子邮件的工作原理
- MTA 配置
- 对抗垃圾邮件和病毒
- Postfix 的替代方案

## 管理邮件服务器

是否还有哪种应用程序比电子邮件更让人们产生上网的愿望呢？向同事、朋友和家人快速发送短便信息，而无需购买信封、寻找邮票和寻找邮箱——并且让信息在几秒钟内（而不是几天）送到收件人手中——这简直像魔法一样，不是吗？

对我们许多人来说，这种魔力已经消失了一点。我们必须穿过成堆的垃圾邮件、转发的笑话和半无意义的邮件列表帖子，才能找到真正重要的内容。更不用说每周与网络上出现的最新病毒作斗争了。电子邮件是一份礼物，尽管它伴随着许多波折。

电子邮件的魔力发生在一个网络感知操作系统的帮助的一系列标准和协议之上。在本章中，你将学习了解电子邮件从你的信箱发送到收件人信箱的机制。

你还将学习如何在 `YaST` 中设置你的电子邮件账户，以及可以使用哪些用于读取、发送电子邮件以及处理其他信息相关任务的不同程序。如果你在多平台业务环境中使用 SUSE Linux，你也会发现连接 Microsoft Exchange（及其替代方案）的章节非常有帮助。

## 电子邮件的工作原理

当你去掉所有的邮政比喻后，电子邮件（email）只是在网络内部或网络之间传输的纯文本。这些文本使用简单邮件传输协议（SMTP）从服务器发送到服务器。

## 第 15 章 管理邮件服务器

该协议的扩展允许身份验证和发布错误信息。邮件传输代理（MTAs）在用户感知不到的情况下运行，负责邮件的发送和接收。

接收邮件有两套规则。如果你从互联网服务提供商（ISP）获取邮件，你可能使用的是邮局协议第 3 版（POP3）。该协议设置了从中央服务器（你的 ISP）下载邮件到本地客户端（你的硬盘）的规则。POP3 服务器随后会删除已下载的邮件。

接收邮件的另一种方法是邮件访问协议第 4 版（IMAP），通常在企业环境中看到，用户需要访问数据或通过多台机器访问。使用 IMAP，邮件永久存储在中央服务器上，用户在登录网络时查看他们的邮件。

简单来说，当你向 occupant@email.net 写一封电子邮件时，在你点击发送按钮后的几秒内会发生以下情况：

1. 客户端将你的消息发送到 SMTP 服务器。
2. 服务器的 MTA 查询 DNS 服务器以定位 email.net 的 IP 地址，并将其与同时到达的其他消息一起队列。
3. 你的 SMTP 服务器通过 25 端口连接 email.net 的 MTA。当服务器确认连接时，你的 SMTP 服务器发送你的消息以及其他发往 email.net 的消息。

## MTA 配置

当你在 `YaST` 中运行传输代理组件时，你正在配置 `Postfix` 和 `Fetchmail`。自 8.1 版本以来，`Postfix` 一直是 SUSE 的标准 MTA。早期的 SUSE 版本使用了仍广泛使用的 `Sendmail`。`Sendmail` 以难以配置而闻名，而 `Postfix` 则不然。`Postfix` 处理流量也比 `Sendmail` 多。不难看出 SUSE 开发者为什么要进行切换。

然而，对于用户来说，区别不大，因为是由 `YaST` 控制配置。手动创建配置是可能的，但可能会被 `YaST` 在安装新包后的每次运行所覆盖。

在本节中，我们将处理 `YaST` MTA 向导提供的额外界面。基础用户应坚持这些设置的默认值，但如果你想微调邮件操作，请阅读后文。

## 身份验证

假设你有一个不同电子邮件账户的用户，且所有的邮件都应该来自该账户。使用本地用户对话框指定用户以及应显示在邮件“发件人”行中的地址。

某些 ISP 要求在使用其 SMTP 服务器发送邮件时提供密码。如果属于此类，请使用此对话框识别用户、用户名和密码。如果你没有这些信息，可能需要向你的 ISP 技术支持索要。

## 远程 SMTP 连接

如果此系统是邮件服务器，请勾选接受远程连接。这将允许你的用户通过此系统发送邮件。

## 入站邮件协议

如前所述，有两种接收邮件的主要方式：POP3 和 IMAP。其他协议可用于接收/下载邮件，它们列在下拉菜单中。默认情况下，Postfix 会联系服务器并自动确定其使用的协议。其他协议列如下：

- POP2—可能仍存在于某些邮件服务器上，这个版本的邮局协议非常老旧。
- APOP, KPOP—比普通 POP 更安全的身份验证。

> 注意
尽管它是网络上最常用的服务之一且已经持续了很久，但电子邮件仍然是最不安全的服务之一。你为该服务添加任何安全功能（包括更安全的客户端）都能在问题发生之前将其解决。

## 第 15 章 管理邮件服务器

- SDPS——英国互联网服务供应商（ISP）Demon Internet 使用的特殊 POP3 兼容协议。
- ETRN——扩展传输（Extended Turn）的缩写，是 SMTP 邮件投递协议的扩展，允许 SMTP 服务器向另一个 SMTP 服务器请求其针对特定域的任何邮件消息。ETRN 通常用于从没有专用互联网连接的邮件服务器中检索邮件消息（来自 webopedia.com）。
- ODMR——按需邮件中继（On Demand Mail Relay）。

如果你的 ISP 使用了这些协议中的任何一种，他们应该告知你。否则，Fetchmail 的自动检测应该可以正常工作。

## 投递模式

默认为“直接”（Directly）。要使用 SUSE Linux 自带的 Cyrus IMAP 服务器，请从下拉菜单中选择此选项。要使用 Procmail 对邮件投递进行更多控制，请选择此选项。更多信息请参见本章的“对抗垃圾邮件和病毒”章节。

## 别名

别名（Aliases）允许为你本地账户（但接收来自 ISP 的邮件）指定无限数量的电子邮件地址，而无需创建具有登录功能的真实用户。发往 `<alias>@<yourdomain>`（或 IP 地址）的邮件将转发给一个真实用户账户。

打开别名对话框会显示几十个默认别名，这些别名对应邮件转发后到达的真实账户。通过选择你想要操作的别名并点击相应的按钮，可以向列表添加或删除现有别名。

## 虚拟域名

允许你更改电子邮件地址的用户名部分。虚拟域名（也称为虚拟主机）允许你更改地址的域名部分。

关于此点的更多信息请阅读第 26 章“管理 Apache Web 服务器”。

## 对抗垃圾邮件和病毒

电子邮件极其易用，而且几乎是免费的。这就是为什么它很受欢迎。不幸的是，正是这些相同的因素导致我们的邮箱每天都被数十封甚至上百封匿名邮件充斥，这些邮件恳求我们装修家居、购买各种药物以及增强你选择的身体部位。

电子邮件也是通过蠕虫、木洛马、病毒和其他恶意软件对我们的计算机和网络传播攻击的最爱机制。

技术专栏作家、政治家和普通用户在面对这种攻击时宣布了电子邮件的死亡。我们能做什么？继续努力战斗。

SUSE Linux 9.2 引入了一个新的反垃圾向导，它可以与你的邮件客户端协作，在垃圾邮件填满你的邮箱之前将其移除。

几个旨在对抗垃圾邮件的开源项目应运而出，每个项目都有自己的粉丝：SpamAssassin、Bogofilter、SpamBayes、Assistance-Filter 和 GMX 是最为人知的。

KMail 和 Mozilla Thunderbird 都包含了反垃圾工具。Thunderbird 是内置的，而 KMail 则利用上述反垃圾工具创建过滤器。

最后，还有老派的方法，使用 Procmail。

## 反垃圾邮件工具

现代反垃圾工具使用贝叶斯过滤来识别垃圾邮件中典型的单词和模式。它们与 MTA 协作扫描入站邮件并根据其规则进行过滤。

过滤器最大的问题是它们会产生误报，将好邮件（也称为 Ham）当作垃圾邮件丢弃。作为代价，它们也会漏掉大量的垃圾邮件。它们可以通过不同的方式进行训练，以便在你纠正它们的错误时提高它们的检测能力。

在训练过滤器时，确保检测到的垃圾邮件被发送到你自己的文件夹而不是立即删除。否则，无法知道会丢失多少误报。

要训练过滤器，请在你的邮件客户端中创建两个新文件夹：用于误报的“非垃圾邮件”（Not Spam）和用于漏报的“垃圾邮件”（Missed Spam）。当垃圾邮件进入时，手动移动到“漏垃圾邮件”文件夹。尽可能经常（最好每周）检查垃圾邮件文件夹并将好邮件移动到“非垃圾邮件”文件夹。运行训练工具，这取决于你使用的具体工具。

你可能想要访问的是 Apache SpamAssassin 项目，地址为 http://spamassassin.apache.com。这是一个开源软件（一套 Perl 脚本），运行在服务器上并在垃圾邮件进入你的网络之前将其拦截。它通过使用多种不同的技术完成这项艰巨的任务，包括使用 DNS 阻塞列表、分析报头和文本以及一些统计学方法。

由于使用多种技术来识别垃圾邮件，该工具能够过滤掉目前流浮的大多数垃圾邮件。强烈建议你下载最新版本并安装在你的服务器上。

> 可能发生的最噩梦之一是发现你的服务器已变成垃圾邮件网关——字面上的以极快速度传递垃圾邮件。许多公司目前提供作为反垃圾邮件网关的软件产品，这些产品可以防止垃圾邮件、钓鱼尝试和许多病毒越过服务器。

这些产品提供的主要优势是它们预先配置好了，管理员除了在安装期间微调几处设置外无需做其他。除了这种简化外，它们提供的几乎没有 SpamAssassin 中不具备的功能，强烈建议你在购买类似产品之前，调查这个开源解决方案及其可能性。

## 客户端垃圾邮件过滤器

Mozilla Thunderbird 团队对其产生的垃圾过滤器（Junk filters）感到自豪。它很容易训练，而且几乎不会产生误报。可能由于这种心态，它在你的邮箱中留下了许多漏报。幸运的是，选择消息并按 J 键可以迅速将消息标记为垃圾邮件。

垃圾过滤功能默认关闭。转到工具 > 邮件控制（垃圾 Mail Controls）来开启并配置它们。你将看到图 15.1。

![](img/a5bd665678bc)  **图 15.1 在 Thunderbird 中设置垃圾过滤**

使用此对话框自动将地址录中的所有人加入白名单。当你确认没有误报时，将邮件移动到“垃圾”文件夹。

## Procmail

Procmail 在邮件从服务器获取时处理每个邮件。详细信息请参见 `/usr/share/doc/procmail` 中的 README 和示例文件。

## 病毒防护工具

传统观念认为 Linux 几乎是免疫的。这在很大程度上是正确的，但可能并非永远。病毒编写者，从脚本小子到更专业的人士，都喜欢利用 Outlook 作为传播媒介。随着越来越多的人使用 Linux 完成日常工作，恶意的程序会尝试挑战。

SUSE Linux 默认不安装病毒工具。你可以配置 fetch 与病毒工具协作，反之适用于大多数病毒工具。

最著名的开源病毒工具是 ClamAV，适用于几个商业工具包括 F-Prot 和 Sophos。

## Postfix 的替代方案

微软尚未被开源产品超越的最后领域之一是企业治理和邮件。许多企业使用 Microsoft Outlook 和/或 Microsoft Exchange Server 获取电子邮件，提供日历、笔记和其他协作功能。行业对 Exchange Server 的普遍投诉集中在可扩展性、管理（特别是备份和恢复，那里有一个活跃的第三方市场）以及许可费用上。

“直接式”替代方案需要兼容 Outlook，因为它旨在在使用微软桌面的环境中替换 Exchange Server。“工作类似”替代方案提供与 Exchange Server 类似的功能，但不提供对 Outlook 客户端的支持；后者是许多开源替代方案的典型。

有几种直接式替代方案，但没有一个是完全开源的，因为需要某些专有连接器来为 Outlook 提供服务（或为 Linux Evolution 客户端提供 Exchange 服务）。对于 Outlook 兼容性，关键似乎在于 MAPI（微软的消息应用程序接口）的完整实现。该目标可能很难实现，因为对于 Linux 解决方案，许多替代方案的成分是一个文档记录良好的协议。

当然，这些功能的独立应用程序在开源世界随处可见，但协作软件的一个特征是集中管理；另一个是所有组件都可以共享信息。开源对微软在该领域统治地位的关键转向邮件、日历和调度的开放标准。日历分布式写作和版本控制（CalDAV）标准基于更早的工作

## 第15章 管理电子邮件服务器

Web上的分布式协作与版本控制 (WebDAV)。随着一种更有序、基于标准方法的出现，Exchange 的统治地位可能走向终结。

接下来的章节将检查几款可用服务器，从 Exchange Server 本身开始，转向与其兼容性日益增加的应用程序。

## Microsoft Exchange Server

由于广泛部署，Exchange Server 和 Outlook 似乎是电子邮件行业的行业基准。它们提供了一个专有的服务器，使用 Outlook 作为客户端并将 MAPI 作为 API，提供电子邮件、联系人、日程、公共文件夹、任务列表、日志和备注。如果你认为 Exchange 提供了“全套”功能，那么没有其他替代方案可以提供 Exchange 100% 的功能。

## CommuniGate Pro

CommuniGate Pro 是一种专有的 Exchange 直接替代方案，提供电子邮件、网页邮件、LDAP 目录、Web 服务器、文件服务器、联系人和列表服务器。CommuniGate Pro MAPI 连接器允许通过 Outlook 和启用 MAPI 的客户端访问该服务器。

## Novell GroupWise

GroupWise 是 Novell 的专有消息和日历解决方案。除了电子邮件外，它还处理即时消息以及任务和文档管理。SUSE Linux 10 首次包含了 GroupWise 客户端。

## Samsung Connect

这是一种专有的 Exchange 直接替代方案。Samsung Connect 服务器提供了几乎是 Exchange 的完全替代品，并将支持任何出现的、支持 Linux 的日历标准。

## OPEN-XCHANGE

OPEN-XCHANGE 是 SUSE 在被 Novell 收购之前进入协作市场的尝试。OPEN-XCHANGE 主要围绕面向 Java 的组件构建，提供了一个可以处理联系人、日程、电子邮件和任务管理的 Web 界面。它基于 Cyrus IMAP 和 Postfix。通过与 SUSE Linux Enterprise Server (SLES)get，OPEN-XCHANGE 还可以进行项目管理、论坛和书签管理。

## Kolab/Krowuate

Kolab 计划始于德国州政府向 KDE 开发人员小组提供资金用于协作软件解决方案。Kolab2 使用 Postfix、Cyrus-imap、OpenLDAP 和 ProFTPd 作为其内核，与 Contact 客户端配合效果最佳。

## OpenGroupware (Ogo)

以前称为 SKYRiX，OpenGroupWare 为任何现有的电子邮件配置提供协作软件和协作组件。它提供日程、联系人、网页邮件、任务管理、资源、项目和文档管理。它运行在 SOPE 应用上。

## phpGroupWare

这可能是几个基于 PHP 的项目中的最好的，你将在第 31 章“创建动态网站”中学习更多相关内容。其他的包括 PHPProject、eGroupWare 和 more.groupWare。它与 MySQL 或 PostgreSQL 等数据库管理系统，以及 Web 服务器和 IMAP 邮件服务器一起使用。它提供基于 Web 的日程、任务列表、地址簿、电子邮件，并附带了新闻标题和文件管理器。问题是 phpGroupWare 在浏览器之外并不能正常运行，将该领域留给了更健壮的客户端。

## Hula

另一个 Novell 开源倡议，Hula 起始于一个专有的 NetMail 服务器。NetMail 在 2005 年春季开源，其初始开发团队公开讨论重新思考人们协作的方式，并使 Hula 成为支持人们真实工作方式的应用程序。它的目标是“既有趣又易用，同时能够从容地从小小组扩展到拥有数千成员的大型组织”。然而，在本文写作时，1.0 版本仍然遥不可及。

## 结论

如前所述，在开发出替代标准之前，企业电子邮件不太可能发生巨大变化。这可能出现在未来几年互联网工程任务组 (IETF) 的讨论中。在此之前，企业可以并应该尝试现有的开源产品，并知道当标准到来时，他们的业务已经准备就绪。

## 参考文献

- http://www.gnome.org/projects/evolution—Evolution 首页。
- http://www.mozilla.org/products/thunderbird—Thunderbird 页面。链接 MozillaZine 知识库和帮助论坛。
- http://pim.kde.org—KDE 个人信息管理套件首页：Contact、KMail、Korganizer 以及所有辅助工具。
- http://sylphed.good-day.net—Sylphed，另一个基于 GTK 的邮件客户端。
- http://www.mutt.org—基于文本的电子邮件客户端中的大杂烩。
- http://www.fpx.de/Software/UDEView—UDEView 多格式附件解码器。支持所有编码格式（BinHex, yEnc, MIME, UUEncode）。享受《编码简介》文档并获取一些实用的历史。
- http://www.yenc.org/linux.htm—用于 yEnc 编码格式的 Linux 读写器。
- http://email.about.com/cs/standards/a/base64_encoding.htm—对 Base64 编码的优秀描述。
- http://www.postfix.org/start.html—Postfix 首页。务必点击菜单上的 Web Sites 以找到适合你的镜像站点。
- http://www.sendmail.org—Sendmail 首页。
- http://catb.org/esr/fetchmail—Fetchmail 首页。
- http://www.paulgraham.com/spam.html—Paul Graham 的原文《垃圾邮件计划》概述了贝叶斯过滤理论。
- http://spamassassin.apache.org—SpamAssassin 首页。查看 wiki 页面以获取可下载的自定义内容。

# 今日 Usenet 新闻 273

对于某些人来说，这导致了替代（alt）层级的兴起，在该层任何人都可以创建一个组，而且许多人都这样做了（见证 alt.swedishchef.bork.bork.bork 的存在）。

随着硬件和软件公司提供 Usenet 支持通道，其他层级也发展出来；学院和大学为学生和教职工使用新闻组；面向社区的企业极客则为他们的本地社区使用新闻组。其中一些在今天仍在运行。

垃圾邮件首次在 Usenet 上显露头角，是一对移民律师在当时活跃的所有新闻组中发布了他们的服务广告。在千年到来之前，垃圾邮件几乎完全消灭了许多小组的真实帖子。但其他小组仍然非常有用。

你的 ISP 很可能提供某种形式的 Usenet 访问。联系他们以获取其 Usenet 服务器的地址以及他们提供的新闻组（也称为他们的新闻源）。许多 ISP 对其馈源内容具有选择性，特别是涉及到 alt 分组时。这些通常被视为种子用户的虚拟社区，其中充斥着盗版软件、恶意软件以及不适合家庭的文本和图像。如果你正在寻找某个特定的组而它没有被包含在内，通常可以请求添加。

有几个可用的新闻服务器，你可以在 http://freenews.maxbaud.net 找到它们的列表。遗憾的是，垃圾邮件发送者经常利用这个机会推销他们的商品，因此在使用时请务必小心。

# 使用 GOOGLE GROUPS

曾经，有一个 DejaNews，它是 Usenet 的存档，而且它非常好用。几乎所有追溯到 1980 年代的每条 Usenet 帖子都包含在这个免费的网络资源中。随后 .com 时代崩溃了，DejaNews 陷入了危险。但谁能来营救呢？那家努力让 Web 对人类更有用的公司：Google。

在写本文时，Google Groups 在技术上仍处于 Beta 阶段，它既可以通过所有标准的 Google 工具搜索 Usenet 存档的方法，也可以免费访问当今的 Usenet。Google 确实在页面上投放了广告。

只需访问 Google Groups (//groups-beta.google.com) 并进行关键词，或通过链接浏览组。通过免费注册，你可以订阅喜爱的组并创建自己的公共或私有组。图 1.6 显示了由 Konqueror 创建的 alt.linux.use.group。

在阅读 Usenet 帖子时，你的客户端可以让你轻松地回复，通过电子邮件或作为公共帖子进行回复。某些客户端支持用于发布和发送电子邮件的多个“身份”，因此你可以选择不同的签名或回信地址。

# 注意

垃圾邮件发送者使用软件“机器人”来收集他们在 Usenet 上找到的每一个电子邮件地址，他们从不发布真实的电子邮件地址。他们使用人类可以读懂但机器人会遇到困难的地址，例如 myNameNOSPAMmyISP.com。

# 第 16 章 与他人协作

![](img/a5bd665678bc55d634220eefc7819145_299_0.png)

**图 16.1** Google Groups 在 Web 上为你提供了可搜索和下载的 Usenet 馈源。这是 alt.os.linux.suse 组。标准的 Google 广告出现在页面底部。

# 选择 Usenet 新闻器

基于在 SUSE Linux 中阅读 Usenet 的选择。许多客户端也可以传递新闻。周围还有几个独立的客户端（Knode/Kontakt、Pan 以及各种基于文本的客户端）。有些要求你会在访问新闻时在线，而另一些则允许离线阅读。当然，还有针对 Emacs 的版本。

# 邮件/新闻客户端

阅读和处理新闻是非常相似的任务：阅读并回复，也许保存以备后用。出于这个原因，跟进的最简单方法是使用支持 Usenet 的邮件客户端。

许多客户端都支持这一点，包括一些最出名的：Mozilla Mail/Thunderbird、Evolution、Sylpeed、mut 和 pine。将它们配置为读取 Usenet 通常只需要识别 Usenet 服务器（通常为 <ISPName.com>）并在需要身份验证时包含登录信息即可。

在邮件客户端中阅读新闻通常是一种非常纯净的体验，没有独立新闻阅读器使用的某些高级过滤器，但通常支持线程（如果邮件支持支持的话），并且回复帖子的操作方式与电子邮件相同。

# 选择 Usenet 新闻器 275

通过 Usenet 进行二进制传输（包括图像、多媒体文件和程序）的支持参差不齐。yEnc 编码格式在 Usenet 中要广泛得多（见第 15 章“管理电子邮件服务器”更多关于 yEnc 信息），如果你的邮件客户端不支持它，你将会错过很多内容。许多内容通过 Usenet 二进制文件传播，这可能是件好事。

# 独立 GUI 新闻器

也许你的邮件客户端不支持某些功能（例如 KMail），或者你想要一些更适应 Usenet 氛围的东西（二进制传输、bozo 过滤器以及清除垃圾邮件的方法）。独立新闻器可能是一个不错的选择。

与许多其他 GUI 软件包一样，针对 KDE (KNode) 和 gnome (Pan) 都有独立的新闻器。如果你需要，可以将 KNode 包含在 Kontakt 内部。

# Pan

Pan 的运行类似于 Windows 新闻器 Forté Agent，但它更先进。你可以从多个服务器读取馈源，包括 Novell Linux 支持组（图 16.2）。

![](img/a5bd665678bc55d634220eefc7819145_300_0.png)

**图 16.2** Pan 是一个易于使用的新闻器。

（注：原文后续存在大量重复段落已省略，仅保留核心翻译内容）

# 第 16 章 与他人协作

5. 现在转到“视图”、“过滤”（或点击像漏斗一样的过滤器工具栏图标），并选择“有新回复”（Has New_Followups）以激活当前群组的过滤器。

## 基于文本的新闻器

由于在图形用户界面（GUI）出现之前 Usenet 就已经存在了，许多基于文本的新闻器仍在在使用。有些甚至仍在活跃开发中。SUSE Linux 带有 NetNews (nn)、InterNews (inn)、tin、slrn 和 suck。

在开始使用任何这些程序之前，您需要将您的新闻服务器设置为环境变量。请以该用户身份操作，不要以 root 身份。在 shell 中，输入以下命令：

```bash
