
通过使用 `-d` 选项并配合时间间隔（秒），你可以让 Fetchmail 以守护进程或后台模式运行。该命令将启动一个后台进程，并按照指定的间隔从指定的远程服务器检索邮件。有关更多高级选项，请参阅 Fetchmail 的 man 页面，该页面编写得非常出色，并详细说明了所有选项。

### 注意

由于 `.fetchmailrc` 包含了你的邮件服务器密码，因此它应该仅供你读取。这意味着它的所有者应该是你，且权限不应大于 `600`。如果 `.fetchmailrc` 文件的权限大于此值，Fetchmail 将报错并拒绝启动。

# 选择邮件投递代理 (MDA)

由于邮件处理的模块化性质，可以使用多个应用程序来处理邮件并完成比简单投递更多的任务。从存储区域获取邮件并将其显示给用户是 MDA 的目的。MDA 功能可以在某些邮件客户端（MUA）中也找到，这可能会让那些不熟悉 UNIX 邮件客户端的用户感到困惑。例如，Procmail MDA 提供了规则集过滤功能；KMail 和 Evolution 均为 MUA，都提供过滤功能，但 MUA pine、mutt 和 Basa 则不提供。某些 MDA 执行简单的排序，而其他 MDA 则设计用于消除不需要的邮件，如垃圾邮件和病毒。

你会根据想对邮件进行什么操作来选择 MDA。我们将查看五种在你的特定情况下可能认为有用的 MDA。如果你有简单的需求（仅根据规则组织邮件），那么提供过滤功能的 MUA 之一可能更符合你的需求。Ubuntu 默认提供 Evolution，并可以满足你的需求。如果不是，请研究 Ubuntu 提供的以下 MDA 之一。

如前所述，所有 MDA 软件都通过 `synaptic` 和 `apt-get` 提供。第 31 章“管理软件”详细介绍了任何软件的通用安装方法。

# Procmail

作为一种面向进阶用户的工具，Procmail 应用程序在邮件从邮件服务器检索时充当邮件过滤器。它在读取每条邮件信息时会使用规则集（称为 recipes）。它不提供默认配置；你必须为每个用户手动创建一个 `~/.procmail` 文件，或者每个用户可以创建自己的文件。

没有系统范围的默认配置文件。规则集的创建并非易事，需要对正则表达式的使用有理解，这超出了本章的范围。Ubuntu 在 `/usr/share/doc/procmail/` 目录下提供了三个文件示例，并在 `/usr/share/doc/procmail` 目录下提供了一个全注释的示例，该目录还包含 README 和 FAQ。规则集的细节可以在 Procmail 的 man 页面以及 `procmairc`、`procmailsc` 和 `procmaile` 的 man 页面中找到，这些页面包含了 Procmail recipes 的示例。

# Spamassassin

如果你使用电子邮件已经有一段时间了，你很可能遭受过垃圾邮件——即同时发送给数千人的不受需要的邮件。Ubuntu 提供了一个名为 Spassassin 的 MDA 来帮助你减少和消除不需要的邮件。它可以轻松地与 Procmail 和 Sendmail 集成，并配置为系统级或个人使用。它使用了规则集和黑名单（已知发送垃圾邮件的互联网域名）的组合。

启用 Spassassin 非常简单。你必须先安装并配置 Procmail。`/usr/share/doc/spamassassin` 中的 README 文件提供了关于如何配置 `.procmail` 文件以通过 Spassassin 处理邮件的详细信息。它会为垃圾邮件打上唯一的头部标记；然后你可以让 Procmail 以你选择的任何方式过滤邮件。Spamassassin 的一个有趣用途是使用它来标记专门为吸引垃圾邮件而建立的特殊账户收到的邮件。这些信息会与 Spassassin 网站共享，那里的“垃圾陷阱”产生的命中可以帮助作者精调规则集。

# Squirrelmail

也许你不想在 MUA 中读取和发送邮件。如果你经常使用网络浏览器，那么通过 Web 界面（如 Yahoo 或 Hot! 使用界面）读取和发送邮件可能有意义。Ubuntu 提供了 Squirrelmail 用于这一目的。Squirrelmail 使用 PHP 语言编写，支持 IMAP 和 SMTP，且在不使用 Java 的情况下渲染 HTML 4.0。它支持 MIME 附件，以及地址簿和用于分类邮件的文件夹。

你必须配置你的 Web 服务器以配合 PHP 4。详细的安装说明可以在 `/usr/share/doc/squirrelmail/INSTALL` 中找到。配置完成后，通过浏览器访问 `http://www.yourdomain.com/squirrelmail/` 读取并发送邮件。

# 病毒扫描器

尽管目前的观点是 Linux 对针对 Microsoft Outlook 用户的邮件病毒具有免疫，但让 UNIX 邮件服务器允许病毒通过它们传输毫无意义。尽管 Ubuntu 不提供病毒扫描器，但在许多此类扫描器中流行的之一是 MailScanner，可以从 `http://www.sng.ecs.soton.ac.uk/mailscanner/` 获取；它提供了 Ubuntu DEB 包以及源码。它支持 Sendmail 和 Exim，但不支持 Postfix 或 Qmail。通过 `synaptic` 使用“virus”和“scanner”术语搜索应该为你提供其他可以尝试的选项。

# Microsoft Exchange Server 的替代方案

# 邮件守护进程

- Biff 是一个监控你的邮件文件夹的小型守护进程，并在邮件放入那里时通知你。通常会将 biff 包含在 `.login` 或 `.profile` 文件中，以便在用户登录时自动启动。
- 自动回复器（Autoreponders）自动对收到的邮件生成回复；它们通常用于通知收件人不在办公室。谢天谢地，Ubuntu 提供了这些功能。

# phpgroupware

`phpgroupware` 是一个用 PHP 编写的开源应用程序（配合 MySQL 或 postgresql 加上 Web 服务器和 IMAP 服务器使用）。`phpgroupware` 是一个基于 Web 的日历、任务列表、通讯录、电子邮件、新闻标题和文件管理器。它的模块化特性允许你根据需要插入各种组件（目前大约 50 个）。主页为 `http://www.phpgroupware.org/`。

# PHProjekt

PHProjekt 是一个用 PHP 编写的开源软件（配合 MySQL、postgresql、Oracle、Informix 和 MS-sql 使用）。PHProjekt 提供了日历、联系人管理器、工时系统、项目管理、在线聊天、线程式讨论论坛、工单系统、电子邮件、公共文件、笔记、投票系统、任务列表、提醒、站点搜索以及与 PostLuke 站点应用的集成。它完全不提供 Exchange/Outlook 兼容性。主页为 `http://www.PHProjekt.com/`

# Horde

Horde 是一个基于 PHP 的应用程序框架。当与 HTTP 服务器（Apache、Microsoft IIS、Netscape）和 MySQL 数据库结合时，IMP/Horde 提供的模块包含 Webmail、联系人管理器、日历、CVS 查看器、文件管理器、时间跟踪、邮件过滤规则管理器、笔记、任务、聊天、新闻组、表单、错误跟踪、FAQ 库，主页为 `http://www.horde.org/`

# Ubuntu 和 Linux 命令

你将使用以下命令在 Ubuntu 中管理电子邮件：

- `balsa`—一个用于 X 的 GNOME 邮件代理
- `biff`—一个基于控制台的邮件通知工具
- `evolution`—一个用于 X 的功能强大的 GNOME 邮件 PIM
- `fetchmail`—一个用于 Linux 的基于控制台和守护模式的邮件检索命令
- `fetchmailconf`—一个用于 X 的图形 fetchmail 配置客户端
- `kmail`—一个用于 KDE 和 X 的图形邮件客户端
- `karn`—一个用于 KDE 和 X 的 biff 应用
- `mut`—一个基于控制台的邮件用户代理
- `sendmail`—一个用于 UNIX 和 Linux 的全面邮件传输代理
- `xbiff`—邮件通知客户端

## 参考

以下参考文献是电子邮件配置的推荐阅读材料。当然，并不是所有的参考文献都适用于你。请选择适用于你正在使用的电子邮件服务器的内容。

# 网络资源

- `http://www.sendmail.org/`—这是 Sendmail 的主页。在这里你可以找到关于 Sendmail MTA 的配置信息和常见问题解答。
- `http://www.postfix.org/`—这是 Postfix 的主页。如果你使用 Postfix MTA，可以在此站点找到文档和示例配置。
- `http://www.qmail.org/`—这是 Qmail MTA 的主页。它包含了关于 Qmail 的文档以及指向其他资源的链接。
- `http://www.linuxgazette.com/issue35/jao.html`—Linux 上的 IMAP：实用指南。电子邮件访问协议允许用户访问存储在远程服务器而非本地磁盘上的电子邮件。
- `http://www.imap.org/about/whatisimap.html`—此页面描述了 IMAP。
- `http://www.rfc-editor.org/`—RFC（意见征稿）库，定义了现代计算机使用的技术“规则”。
- `http://www.procmail.org/`—Procmail 主页。
- `http://www.moongroup.com/docs/procmail/`—Procmail 常见问题解答，包含了故障问题的建议。该页面还引用了一个链接页面，反过来引用了其他集合以及 Procmail 邮件列表的存档。
- `http://www.ibilio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Qmail-VMailMgr-Courier-imap-HOWTO.html`—如果你需要帮助配置基于较常用应用程序的邮件系统，这个 HOWTO 将会有帮助。

# 书籍

- Sendmail (O'Reilly Publishing)—这是所有 Sendmail 相关内容的实际标准。它有超过 1000 页，让你了解到 Sendmail 仍然是多么复杂。
- Postfix (Sams Publishing)—来自 Sams 出版的一本优秀书籍，涵盖了 Postfix MTA。
- Running Qmail (Sams Publishing)—这与 Sams 出版的 Postfix 书籍类似，不同在于它涵盖了 Qmail MTA。

# 第 20 章

## 本章内容

# 代理与反向代理

- 什么是代理服务器？
- 安装 Squid
- 配置客户端
- 访问控制列表
- 指定客户端 IP 地址
- 示例配置
- 参考

在这个世界上，两样东西你永远都不嫌：时间和带宽。Ubuntu 自带了一个代理服务器——Squid，它允许你缓存 Web 流量，以便网站加载更快，用户消耗更少的带宽。

# 什么是代理服务器？

代理服务器位于客户端机器（你公司的台电脑）和互联网之间。当客户端请求网站时，它们不会直接连接到 Web 并发送 HTTP 请求。相反，它们连接到本地代理服务器。代理服务器将请求转发到 Web，获取结果，并将其返回给客户端。简单来说，代理服务器实际上只是客户端和服务器之间的额外层，那么为什么要费此精力呢？

部署代理服务器的主要理由如下：

- 内容控制——你希望阻止人们在工作时间阅读新闻或下载 MP3 来消磨时间。
- 速度——你希望缓存常用网站以最大限地利用你的带宽。
- 安全——你希望缓存常用网站以最大限地利用你的带宽。

# 安装 Squid

这些规则是不言自明的。第一条写着：“允许本地计算机的 HTTP 访问，但拒绝其他人”。如前提到的，这是默认规则。目前保持其不变，并运行 `squid` 以使用默认设置启动服务器。如果你尚未配置本地网络浏览器使用你的 Squid 服务器，请对其进行配置，这样你就可以测试默认规则了。

在你的网络浏览器中（从这里开始 Firefox 将被冻结，但区别不大），访问 URL `http://www.linux.org`。你应该能看到它在浏览器中正常显示，但在日志窗口中，你应该能看到大量信息滚动，因为 Squid 正在为你下载该站点并将其存储在缓存中。这些都是被允许的，因为默认配置允许对 localhost（本地主机）的访问。

回到配置编辑器窗口，在最后两行 `http_access` 之前添加以下内容：

```
```
