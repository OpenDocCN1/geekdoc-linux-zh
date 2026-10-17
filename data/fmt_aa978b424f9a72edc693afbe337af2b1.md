
为了使 `trouble` 邮件被解析，它会被发送到代表“邮件读者”的别名 `tmr`。`tmr` 将消息归档到 `troubletrap` 并且：

- 16. 根据 RFC，只有 `postmaster` 和 `MAILER-DAEMON` 是真正强制要求的，但包含 `hostmaster`、`abuse` 和 `webmaster` 是惯例。

### 18.4 别名

发送到从主机上的文件获取的用户列表。将新手管理员添加到 `tm` 列表是让他们看到出现的问题、管理员的回复，以及与用户（即客户）交流时应使用的适当奉承语气的好方法。

`sa-class` 别名有两个级别，使得包含学生列表的文件只需要在单台机器（nag）上维护。第 546 页的 `sabook` 别名示例应该具有这种类型的方向，以便文件不需要复制。

`diary` 别名是一个方便的工具，对于那些反感记录自己工作的学生系统管理员来说，它是一种很好的文档提取技术。系统管理员可以通过将邮件发送到 `diary` 文件来轻松记录机器生命中的重要事件（操作系统升级、硬件更改、崩溃等）。不要将该文件放在包含日志文件的文件系统中；否则将允许黑客填满文件系统并防止 syslog 写入日志条目（掩盖踪迹）。

### 转发邮件

`aliases` 是一个由管理员维护的系统级配置文件。如果用户想要路由自己的邮件（且你的站点没有使用 POP 或 IMAP 访问邮件），他们可以通过在家目录中创建 `forward` 文件来实现。`sendmail` 始终会在用户的家目录中查找 `forward` 文件，除非设置了 `ForwardPath` 并覆盖了默认位置。当用户想要接收邮件时，使用 `forward` 文件是非常方便的。

`sendmail` 有一个 `notify` 功能 `FEATURE(redirect)`，有助于管理永久更改。如果别名指向 `user@newsite`，邮件将带有新地址通知返回给发送者，因此发送者必须更新其地址。

你可以配置 `sendmail` 支持 `.forward` 文件的中央目录，但用户并不期望这种配置。`.forward` 文件的位置由 `ForwardPath` 控制，它通常指向家目录以及第 572 页所示的 `generic.m4` 文件。

全局 `aliases` 中的项优于 `.forward` 文件中的项。由于这些文件由不同的人维护，用户必须小心不要创建邮件循环。如果网络上的用户有一个邮件（因此在全局 `aliases` 文件中有项），他们不能使用 `.forward` 文件重定向到共享相同别名的另一台机器。例如，在科罗拉多大学，我们使用站点级别名，如下：

`evi@boulder`

以及 `boulder` 机器上包含 `evi@anchor.cs` 的 `.forward` 文件将创建一个循环。发送给 `evi` 的邮件将被转发到 `boulder`，那里 `.forward` 文件将使其位于子域名。`anchor` 上的 `aliases` 文件将将其返回到 `boulder`，在 25 次跳数后，邮件将返回给发送者。

如果你的主要通信方式是电子邮件，通知用户邮件循环是挑战性的。邮件到 `\user` 将消息传递到本地机器，无论系统级别名文件或用户的 `.forward` 文件如何说。如果本地机器是用户期望读取邮件的地方，那就很好；否则，发送邮件给 `postmaster` 以报告循环或拨打电话。

- 17. 你可能需要使用两个或多个反斜杠才能让其中一个通过 shell 并进入 `sendmail`。

## 18.5 邮件列表与管理软件

### 哈希化的别名数据库

由于 `aliases` 文件中的条目没有特定顺序，让 sendmail 直接搜索该文件将是非常无效的。因此，使用 Berkeley 数据库系统构建了一个哈希版本。这种哈希处理显著加快了别名查找速度，特别是当文件很大时。

从 `/etc/mail/aliases` 派出的文件被称为 `aliases.db`。每当你更改 `aliases` 文件时，必须使用 `newaliases` 命令重建哈希数据库。`newaliases` 实际上是带有命令行标志 (`-bi`) 的 `sendmail`，它告诉程序重新构建数据库。如果你自动运行 `newaliases`，请保存错误输出——你可能引入了格式错误。

## 18.5 邮件列表列表与管理软件

邮件列表是一个巨大的别名，它会将发布到列表的每条消息复制发送给加入列表的每一个人。它就像是通过邮件投递的古代 Usenet 新闻组。有些邮件列表有数千个接收者。

邮件列表通常在 `aliases` 文件中指定，但在外部文件中维护。sendmail 和大多数邮件列表软件都能理解一些标准命名约定。经验丰富的的用户也开始依赖这些约定。最常见的是“request”后缀和“owner”前缀，用于联系列表的维护者。以下别名说明了其内容：

- `mylist`: `include=/etc/mail/include/mylist`
- `owner-mylist`: `mylist-request`
- `mylist-request`: `evi`
- `owner-owner`: `postmaster`

在这个示例中，`mylist` 是邮件列表的。成员从文件 `/etc/mail/include/mylist` 中读取。发送到列表的退信（Bounces）会发送给其所有者 `evi`，加入列表的请求也是如此。从“owner”到“request”的间接跳转变为发送到列表的每条消息的 `Return-Path` 地址。对于这个字段，`mylist-request` 比实际的维护者稍微好一点。发送到 `owner-mylist` 别名的消息中的错误实际上会被发送到 `owner-owner`。

消息不可接受的情况被称为“退回”（bounce）。关于退回的错误信息无法投递的情况被称为“双重退回”（double bounce）。在我们的示例中，双重退回被发送到 `owner-owner` 或 `postmaster`。

如果你使用全站的 `aliases` 文件，你需要添加一个额外的间接层 `pointlist` 指向 `myrealalias@master`，这样包含成员列表的数据文件只需要存在于一个。

### 用于维护邮件列表的软件包

有几个软件包可以实现邮件列表的自动化维护。它们通常允许用户从列表中添加或移除自己，获取有关列表的信息，并通过电子邮件获取文件。一些流行的邮件列表管理器（及其下载来源）如下：

- Majordo，来自 `www.greatcircle.com`（包含在 SUSE 中）
- Mailman，GNU 邮件列表处理器，来自 `www.list.org`
- ListProc，来自 `www.cren.net`
- SmartList，源自 procmail
- listmanager，来自 `www.listmanager.org`
- LISTERV Lite，来自 `www.lsoft.com`（商业版 LISTERV 的免费版本）

总来说，SmartList 较小而简单，ListProc 庞大且复杂，而其他的则介于两者之间。它们在列表维护的哲学上有所不同，有些倾向于让系统管理员作为管理员（ListProc），另一些则倾向于让维护者（Majordo, Mailman, SmartList, LISTERV Lite）负责。

Mailman、listmanager 和 LISTERV Lite 支持远程管理；列表维护者甚至不需要在列表所在的机器上登录，因为所有事务都通过电子邮件完成。大多数软件包允许将发布到列表的信息汇成摘要（digests），有些是自动（SmartList 和 Majordo），有些则通过手动配置（ListProc, Mailman）。

Mailman 是我们最喜欢的管理器。管理它是一种享受，并让列表维护者可以使用他们自己列表的所有功能。ListProc 和 LISTERV Lite 是专有的且昂贵的，其他的仅限二进制且功能受限。我们还没有尝试过 SmartList，但我们喜欢它依赖的 procmail。

我们将简要描述这些软件包。要了解更多细节，请查看每个软件包的文档或 Alan Schwartz 和 Paula Ferguson 编写的 O'Reilly 书籍《Managing Mailing Lists》。

### Majordo

Majordo 是来自 `www.greatcircle.com` 的 Perl/C 软件包。它最初由 Brent Chapman 编写。Majordo 的开发已经停止；Majordo 2 是重写版本，但似乎在 2004 年陷入了沉寂，因此我们只描述常用的原始版本。在我们示例发行版中，只有 thing 自带了 Majordo。尽管页面上说是这样的（`/usr/lib/mail/majordo`），但它隐藏在目录中（`/usr/lib/majordo`）。

Majordo 以无权限用户身份运行，通常名为 `majordo` 或 `mdom`，默认组为 `daemon`。由于 Linux 支持用户名（超过 8 个字符），你也可以使用 majordo 作为登录名。该用户必须被 sendmail 识别为“信任”，因此必须出现在你的 sendmail 配置中，通常在 `confTRUSTED_USERS` 声明中。

Majordo 通过 `majordomo.cf` 文件进行配置。Majordomo 要求 `/etc/mail/aliases` 中存在特殊的别名。集成这些最干净的方法是创建一个独立的别名文件 `majordomo.aliases`。

关于邮件列表最常见的用户问题是“如何取消订阅？”对于 Majordomo 管理的列表，fieldname@host 的答案是向 `majordomo@host` 地址发送邮件，并在正文中包含“unsubscribe listname”。

使用第一种方法，你需要从你订阅时使用的同一个主机发送取消订阅的消息；在第二种形式中，host 是电子邮件地址的一部分。参见 535 了解如何从邮件头中获取此信息，以便在你忘记了加入列表时使用的机器也能正确取消订阅。有些邮件列表也接受向 `listname-request@host` 的邮件，正文包含“unsubscribe”。

永远、不要向列表本身发送取消订阅邮件。如果你这样做，就向列表的所有接收者宣布了你不知道在做什么。

### Mailman

Mailman 是邮件列表软件中一个较新的成员（2.1.8 版本于 2006 年 4 月发布），从 `www.list.org` 或 GNU 存档获取。它最初由 John Vega 编写，目前与 Ken Manheimer 和 Barry Warsaw 合作开发。与 Majordo 一样，Mailman 主要用脚本语言配合 C 封装编写，但这种情况下语言是 Python（可在 `www.python.org` 获取）。

Mailman 的灵感源于 Majordomo 的作者以及他们对退回错误、高级功能（如摘要和现代列表）的复杂配置以及批量邮件性能问题的沮丧。一个 Mailman 脚本导入 Majordomo 列表。

Mailman 的成名之处在于其 Web 界面，这使得版主或邮局管理员管理列表变得更容易，用户订阅、取消订阅和配置选项也更加方便。Mailman 还能某种程度上检测并控制垃圾邮件。

### ListProc

ListProc 是邮件列表管理软件中的老兵了。它由 Anastasios Kitsikonas 于 1991 年编写，并维护到 1994 年。它闲置了几年，但在 1999 年发布新的新的测试版后重新复活。它以前可以从波士顿大学计算机系免费获取，但带有奇怪的许可规则。现在可以通过 `www.cren.net` 获取，但需要支付昂贵的许可费用（每份 2000 美元，即使是大学也是如此）。忘记 ListProc 吧，选择一个免费的开源软件包。

### SmartList

SmartList 最初由 Stephen R. van den Berg 编写，他是 procmail 的原始作者。它可以在 `www.procmail.org` 获取。SmartList 使用 procmail，因此你需要下载 `procmail.tar.gz` 和 `SmartList.tar.gz`。最简单的方法可能是获取适用于你系统的 Linux 软件包。

SmartList 既小又简单。它是 C 代码、procmail 规则和 shell 脚本的结合。邮件列表维护中的头疼问题退信（Bounces）会被软件自动删除。当某个地址发生一定次数的退信后，该用户会自动从列表中移除。SmartList 要求在 `passwd` 文件中有一个登录项（“smart”或可能是“list”），该项必须是 sendmail 配置文件中的受信任用户。

安装程序包含一个用于编辑的锁封装（lock wrapper），它尝试在留下不连贯、部分编辑的配置文件后保护 SmartList。

### listmanager

listmanager 由 Murray Kuchery 用 C 语言编写，与构建在 Perl 或 Python 等脚本语言之上的软件包大有径庭。listmanager 还通过使用 sleepcat.com 的 DB 数据库包而不是平面文件和文件系统得到了改进。它的功能列表大约有一页长，并包含 Web 界面、界面、数字以及若干安全增强。

listmanager 看起来确实是一个杀手级的列表管理器——唯一的缺点是源代码尚未发布。根据 listmanager.org 网页，代码被保留着，直到作者完成清理以避免可能的尴尬。目前提供 Linux 二进制文件。

### LISTERV Lite

LISTERV Lite 由 Eric Thomas 开发，是 L-Soft International, Inc. 商业产品 LISTERV 的删减版。真实版本的一些功能缺失，且软件限制管理 10 个邮件列表，每个列表最多 500 人。LISTERV Lite 需要以伪用户 listerv 运行，该用户必须拥有其文件。它还希望有一个 listgroup 组。LISTERV Lite 提供了一个用于订阅列表和维护列表的 Web 界面。

该发行版可以在 `www.loft.com` 获取。不分发源代码，但提供了许多 UNIX 和 Linux 版本的预编译二进制文件和存根。如果你已经熟悉 LISTERV 并有在使用它的列表，你可能会认为运行一个只有二进制文件的删减列表管理器是合理的。如果你是从零开始，选择上述的开源无限制替代品。

## 18.5 邮件列表和列表管理软件

### LDAP：轻量级目录访问协议

LDAP 是一种提供通用管理目录服务的协议。它已经存在几年，但刚刚开始流行。管理员们发现 LDAP 在某些方面很有用：

- sendmail 配置：别名、虚拟域名、邮件主页、访问数据库和表
- 用户管理：登录名、密码、主机（例如斯坦福大学）
- 管理配置文件（例如 SUSE）
- NIS 的替代品
- 日历服务器
- 使用可插认证模块 (PAM)

人们设想 LDAP 最终将成为用于许多用途的全球目录系统。遗憾的是，仍然缺乏使用 LDAP 自动化管理员任务的工具。

LDAP 源于 ISO 协议和 X.500 目录服务。它的背景立刻让人想到复杂、臃肿、冗长、糟糕等，但 LDAP 中的 L 似乎可以处理这一切。幸运的是，所有版本向下兼容。LDAP 协议版本 3 支持分级服务器；查询一个服务器获取某条数据可能会导致对另一个服务器的引用。版本 2 支持分级数据，但分级服务器仅在版本 3 中。

邮件别名是 LDAP 的一个极佳匹配，特别是现在 sendmail 内部已支持 LDAP。sendmail 可以查询 LDAP 服务器进行别名查找，而不是直接进行查找。LDAP 还可以管理邮件路由和虚拟域名。LDAP 支持必须编译到 sendmail 的二进制文件中。

如果你正在寻找 LDAP 的实现，我们推荐使用由 OpenLDAP 小组在 `www.openldap.org` 的服务器。该小组接管并增强了在密歇根大学开发的早期服务器代码。有关 LDAP 相关软件的更多信息，请参阅第 520 页。

LDAP 数据库条目类似于变量名更长的 termcap 条目。LDAP 数据库中的属性（变量名）尚未完全标准化，这可能导致不同实现之间的不兼容。

数据库条目第一行的属性由 LDAP 配置文件定义。本节中的示例假设 LDAP 服务器守护进程（在 OpenLDAP 中为 slapd）配置了根区分名称 (rootdn)：
