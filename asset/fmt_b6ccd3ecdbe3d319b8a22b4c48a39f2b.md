
> 中继邮件需要正当理由；否则，请勿这样做。允许所有域名通过你进行中继将让你成为垃圾邮件发送者的磁铁，他们将使用你的邮件服务器发送垃圾邮件。这可能导致你的网站被许多其他网站列入黑名单，从而不再接受来自你或网站用户的任何邮件——即使这些邮件是合法的！

# 使用别名 (Aliases) 转发邮件

别名允许你在系统中拥有无限数量的有效收件人地址，你无需为每个地址创建帐户或其他支持文件。例如，大多数系统都将“postmaster”定义为有效收件者，但并没有一个名为 postmaster 的实际登录账户。别名在 `/etc/aliases` 文件中配置。以下是别名条目的示例：

```
postmaster: root
```

此条目将任何收到的 postmaster 的邮件转发给 root 用户。默认情况下，`/etc/aliases` 文件列出的所有别名都转发到 root。

> 以 root 身份读取邮件存在安全风险；恶意邮件可能会利用邮件客户端并导致其以运行客户端的用户身份执行任意代码。为了避免这种危险，你可以将所有 root 的邮件转发到另一个账户，并在那里读取。你可以选择两种方法中的一种。

# 使用 Fetchmail 获取邮件

另一种方法是在 root 的家目录下创建一个名为 `.forward` 的文件，其中包含邮件应该转发到的地址。

每当你对 `/etc/aliases` 文件进行任何更改时，必须重新构建别名数据库，更改才能生效。使用以下命令执行此操作：

```
mathew@seymour:~ sudo newaliases
```

SMTP 设计用于与具有全天候互联网连接的系统配合。如果你使用的是拨号账户怎么办？如果你有另一个服务器为你存储邮件，而你稍后登录去取邮件又怎么办？（大多数不设置服务器的用户都会处于这种情况。）在这种情况下，你无法轻松使用 SMTP 接收邮件，你需要使用某种协议，如 POP3 或 IMAP。

> 注意：记住我们提到过邮件客户端包含某些功能。接下来的章节将介绍如何安装、配置和使用 Fetchmail。

## 安装 Fetchmail

与其它软件包类似，你可以使用 synaptic 或 `apt-get` 安装 Fetchmail。你可以在 `www.debian.org` 获取最新版本的 Fetchmail。

## 配置 Fetchmail

安装 Fetchmail 后，你必须在家目录下创建一个名为 `fetchmailrc` 的文件为 Fetchmail 提供配置。

你可以使用任何文本编辑器编辑 `fetchmailrc`。配置文件直观且易于创建；以下章节将介绍最常用的选项。

### 注意

`.fetchmailrc` 文件分为三个部分：全局选项、邮件服务器选项和用户选项。这些部分按列出的顺序出现很重要。不要将选项添加到错误的部分。将选项放在错误的位置是新用户配置 Fetchmail 时常见的问题之一。

### 配置全局选项

`fetchmailrc` 的第一部分包含全局选项。这些选项影响你在文件中列出的所有邮件服务器和用户账户。稍后在本节中可以使用本地配置选项来覆盖某些全局选项。以下是 `fetchmailrc` 全局部分可能出现的选项示例：

```
set daemon 600
set postmaster foobar
set logfile ./fetchmail.log
```

示例中的第一行告诉 Fetchmail 以守护模式启动，并每 600 秒（即 10 分钟）检查一次邮件服务器。守护模式意味着 Fetchmail 启动后会移动到后台并持续运行。如果没有此行，Fetchmail 只会在启动时检查一次，之后不再检查。

第二个选项告诉 Fetchmail 使用本地账户 `foobar` 作为最后的地址。也就是说，任何它接收但无法投送到指定账户的邮件将发送到 `foobar`。

第三行告诉 Fetchmail 将其活动记录到文件 `./fetchmail.log`。或者，你可以使用 `set syslog`——在这种情况下，Fetchmail 将记录到 `syslogset`。

### 配置邮件服务器选项

`.fetchmailrc` 文件的第二部分包含每个应检查新邮件的邮件服务器的信息。以下是邮件部分可能所示的示例：

```
poll mail.samplenet.org
proto pop3
no dns
```

### 使用 Fetchmail 获取邮件

第一行告诉 Fetchmail 它应该按照全局选项部分设置的 `poll` 间隔检查邮件服务器 `mail.samplenet.org`（在我们的示例中设置为 600 秒）。或者，第一行也可以以 `skip` 开始。如果邮件服务器以 `skip` 开始，则不会按 `poll` 间隔轮询，只有在 Fetchmail 命令行明确指定时才会进行轮询。

第二行指定连接邮件服务器时应使用的协议。在这种情况下，我们使用的是 POP3。其他合法选项包括 IMAP、认证邮局协议 `APOP` 和密钥化邮局协议 `KPOP`。你也可以使用 `AUTO`，在这种情况下 Fetchmail 会尝试自动确定与邮件服务器使用的正确的协议。

第三行告诉 Fetchmail 它不应尝试进行域名服务器 `DNS` 查找。如果你通过拨号连接运行，可能需要包含此选项。

### 配置用户账户

`.fetchmailrc` 的第三部分也是最后部分包含了上一部分中指定的用户账户信息。这是一个示例：

```
user foobar
pass secretword
fetchall
no flush
```

第一行简单地指定用于登录邮件服务器的用户名，第二行指定该用户的密码。许多具有安全意识的人对在文件中放置明文密码的想法感到反感，因此保护此信息的唯一方法是确保该文件对所有者不可读；也就是说，文件权限为 600。

第三行告诉 Fetchmail 它应该从服务器抓取所有邮件，即使它们已经被读取过。

第四行告诉 Fetchmail 在完成下载后应从邮件服务器删除邮件。这是默认设置，所以我们实际上不需要指定此选项。如果你想在下载后从邮件服务器删除邮件，请使用 `flush` 选项。

插入的配置选项使得整个 `.fetchmailrc` 文件看起来如下：

```
set daemon 600
set postmaster foobar
set logfile ./fetchmail.log
poll mail.samplenet.org
proto pop3
no dns

user foobar
pass secretword
fetchall
```

此文件告诉 Fetchmail 执行以下操作：

- 每 600 秒检查一次 POP3 服务器 `mail.samplenet.org` 的新邮件。
- 使用用户名 `foobar` 和密码 `secretword` 登录。
- 从服务器下载所有邮件。
- 在下载完成后从服务器删除邮件。
- 将任何无法交付的邮件发送到本地用户 `foobar`。

正如前面提到的，`.fetchmailrc` 文件中包含的选项比这里列出的更多。然而，本节提供的选项将让你完成基础配置。

为了额外的灵活性，你可以定义多个 `.fetchmailrc` 文件，使用同一个账户从不同的远程服务器获取邮件。例如，你可以为你最常用的账户定义设置并保存在默认的 `.fetchmailrc` 文件中。可以这样快速检索：

```
matt@seymour:- fetchmail -a 1 message for mail at matt.helmke.com (reading message 1 of 1)
flushed
```

通过使用 Fetchmail 的 `-f` 选项，你可以指定替代资源并从另一个服务器获取邮件，如下：

```
matt@seymour:- fetchmail -f .othermailrc 2 messages forget at matt.helmke.com (reading message 1 of 2)
flushed
reading message 2 of 
```

在 `/var/spool/matt` 有新邮件。通过 `-d` 选项配合时间间隔（秒），你可以让 Fetchmail 以守护进程（后台模式）运行。该命令作为后台进程启动，并在指定的间隔从远程服务器获取邮件。更多高级选项，请参 Fetchmail 页面，该页面详细说明了所有选项。

## 选择邮件代理

### 注意

由于 `.fetchmailrc` 文件包含了你的邮件服务器信息，它应该只对你可见。这意味着它应该由你拥有且权限不大于 600。如果 `.fetchmailrc` 文件的权限大于此，Fetchmail 会报错并拒绝启动。

由于邮件处理的模块化性质，可以使用多个应用程序来处理邮件而不仅仅是投递。MDA 从存储区域获取邮件并显示给用户的目的是。MDA 功能可以在某些邮件客户端 `MUA` 中找到，但对于不熟悉 UNIX 邮件概念的人可能会引起困惑。例如，Procmail MDA 根据规则提供过滤；Kmail 和 Evolution 均提供过滤，但 Basta 不。某些 MDA 执行简单的排序，而其他 MDA 设计用于消除不良邮件，如垃圾邮件和病毒。

根据你想如何处理邮件来选择 MDA。我们查看了五个在特定情况下可能有用的 MDA。如果你有简单的需求（按规则组织邮件），一个提供过滤的 MUA 可能更适合你的需求。Ubuntu 提供 Evolution 作为默认（它包含前面提到的某些 MDA 功能），所以先尝试看看它是否满足你的需求。如果没有，请调查 Ubuntu 提供的以下 MDA。

与其他不同，所有 MDA 软件都在 Ubuntu 仓库中。第 8 章“管理软件”详细介绍了任何软件的通用安装方法。

### Procmail

作为一个面向高级用户的工具，Procmail 应用程序在从邮件服务器获取邮件时充当过滤器。它在读取每封邮件时使用规则集（配方）。没有提供默认配置；你必须为每个用户手动创建 `~/.procmail` 文件，或者用户可以创建自己的。

没有系统级的默认配置文件。规则集的创建并非易事，需要理解正则表达式的使用，这是本章的范围。Ubuntu 在 `/usr/share/doc/procmail/examples/` 三个文件示例，在 `/usr/share/doc/procmail` 目录下还有一个带注释的示例，该目录还包含 README 和 FAQ。你可以在 Procmail 的 man 页中找到规则集的详情，并在 `procmailrc`、`procmailsc` 和 `procmailex` 的 man 页中找到，它们包含了 Procmail 配方的示例。

### Spamassassin

如果你使用电子邮件已经有一段时间，那么在同时发送给数千人时，很可能遭受垃圾邮件的影响。Ubuntu 提供了一个名为 Spamassassin 的 MDA 来帮助你减少和消除不良邮件。

# 第 25 章处理电子邮件

与 Procmail 和 Sendmail 集成，它可以配置为系统级和个人使用。它使用了规则集和黑名单（已知发送垃圾邮件的互联网域名）。

启用 Spamassassin 非常简单。你必须先安装并配置 Procmail。`/usr/share/doc/spam/` 中的 README 文件提供了关于配置 `.procmail` 文件以通过 Spamassassin 处理邮件的详情。Spamassassin 为垃圾邮件标记一个唯一的标头；然后你可以使用 Fetchmail 以你选择的方式发送邮件。Spamassassin 的一个有趣用途是用它来标记为了吸引垃圾邮件而建立的电子邮件账户。这些信息会与 Spamassassin 网站共享，这些由“垃圾邮件陷阱”生成的提示有助于作者精调规则集。

# Squirrelmail

可能你不想在 MUA 中读取邮件。如果你使用 Web 浏览器，通过 Web 界面读取和发送邮件可能有意义，例如 Hotmail 或 Yahoo! Mail 使用的那种。Ubuntu 提供 Squirrelmail 正是为了该目的。Squirrelmail 使用 PHP 编写并支持 IMAP 和 SMTP。它支持 MIME 附件以及用于分类邮件的地址簿和文件夹。

你必须为你的 Web 服务器配置 PHP 4。你可以在 `/usr/share/doc/squirrelmail/INSTALL` 中找到详细的安装说明。配置 Squirrelmail 后，将浏览器指向默认安装位置 `www.yourdomain.com/squirrelmail/` 来读取和发送邮件。

## Microsoft Exchange Server 的替代方案

Outlook 和 Microsoft Exchange Server 用于访问电子邮件，并提供日历、备注、文件共享以及其他协作功能。行业内对 Exchange Server 的通用投诉集中在可扩展性、管理（特别是备份和恢复）以及许可费用上。

“即插用（drop-in）”替代方案需要与 Microsoft Outlook 兼容，因为它的设计目标是在已存在使用 Outlook 的 Microsoft 桌面系统的环境中替换 Exchange Server。“工作相似型（work-alike）”替代方案则提供与 Exchange Server 类似的功能，但并不提供与 Microsoft Outlook 客户端本身的兼容性；后者是许多开源替代方案的典型特征。

目前存在多种“即插用”替代方案，但没有一个是完全开源的，因为需要某些属性连接器来为 Microsoft Outlook 客户端提供服务（或为 Linux Evolution 客户端提供服务）。对于 Outlook 兼容性，关键似乎在于对 MAPI（微软消息传递程序接口）的完整实现。这一目标很难实现，因为 MAPI 是一个文档记录较少的协议。对于仅限 Linux 的解决方案，许多替代方案缺失的元素是 Exchange Server/Outlook 提供的群组日历/调度系统。

当然，这些独立应用在开源世界中层出不穷，但“协同软件”的一个特点是集中管理；另一个特点是所有组件都可以共享信息。

以下章节将介绍几个现有的服务器，从 Microsoft Exchange Server 本身开始，逐渐转向与其兼容性日益降低的应用。这些服务器均未由 Ubuntu 提供。

### Microsoft Exchange Server/Outlook 客户端

Exchange Server 和 Outlook 由于其广泛部署，似乎是行业基准。它们提供了一个专有服务器，提供电子邮件、联系人、调度、公共文件夹、列表、日志和备注，并使用 Microsoft Outlook 作为客户端并将 MAPI 作为 API。如果你将 Microsoft Exchange 提供的内容视为“全套”功能，那么没有其他替代品能提供与 Microsoft Exchange Server 完全相同的 100% 功能——即使是那些即插用替换方案也是。Microsoft Exchange 服务器的主页为 `www.microsoft.com/exchange/`

### CommuniGate Pro

CommuniGate Pro 是 Microsoft Exchange Server 的专有“即插用”替代方案，提供电子邮件、网页邮件、轻量级目录访问协议 `LDAP` 目录、Web 服务器、文件服务器、联系人、日历（第三方）、IP 电话 `VoIP` 和列表服务器。CommuniGate Pro MAPI 连接器允许从 Microsoft Outlook 和其他启用 MAPI 的客户端访问服务器。该服务器的主页为 `www.stalker.com`。

### Oracle Beehive

Oracle Beehive 可能是你所获得的最接近 Exchange 的替代品。它允许你通过即时消息、电子邮件、文件共享（工作空间）、日历和其他工具进行协作。Beehive 可用于 Linux 平台，其主页为 `www.oracle.com/us/products/middleware/beehive/index.html`。

### Bynari

Bynari 提供了一组专有服务器，作为 Microsoft Exchange Server 的即插用替换方案，用于电子邮件、日历、公共文件夹、调度、地址簿、网页邮件和联系人。尽管它运行在 Linux 上，但它没有提供 Linux 客户端；你可以配合 Evolution 和 Thunderbird 使用它，且该连接器为 Microsoft Outlook 提供服务。主页为 `www.bynari.net`。

### Open-Xchange

Open-Xchange 具有很高的地位，曾由 Novell/SUSE 拥有并开发，直到被拆分为独立公司。它基于开放标准工作，提供了多种协作方案，并深根于 Linux。它可以与多种协议配合，使其成为连接性最强的套件之一。你可以在 `www.open-xchange.com` 获取开源版本。

### phpgroupware

`phpgroupware` 是一个用 PHP 编写（配合 MySQL 或 postgresql 使用）的开源应用，外加 Web 服务器和一个 IMAP 邮件服务器。`phpgroupware` 提供基于日历的的任务列表、地址簿、电子邮件、新闻头条和文件管理器。其模块化功能允许你根据需要插入各种组件（约 50 个）。主页为 `www.phpgroupware.org`。

### PHProjekt

PHProjekt 是一个用 PHP 编写的开源软件（配合 MySQL、PostgreSQL）。PHProjekt 提供日历、联系人管理、时间卡系统、项目管理、在线聊天、线程论坛、工单系统、电子邮件、公共文件、备注、投票系统、任务列表等。

### Horde

Horde 是一个基于 PHP 的应用程序框架。结合 HTTP 服务器 `Apache`、`Microsoft IIS`、`Netscape` 和 MySQL 数据库时，Horde 模块提供了网页邮件、联系人管理、日历、CVS 查看器、文件管理器、时间跟踪、邮件过滤器管理器、备注、任务、聊天、新闻组、错误跟踪、FAQ 库和演示。其主页为 `www.horde.org`。

# 参考文献

- `www.sendmail.org/`——Sendmail 主页。你可以在这里找到关于 Sendmail MTA 的配置信息和 FAQ。
- `www.postfix.org/`——Postfix 主页。如果你使用 Postfix MTA，可以在此地找到文档和示例配置。
