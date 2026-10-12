
set daemon 600
set postmaster foobar
set logfile ../fetchmail.log

此示例的第一行告诉 fetchmail 它应以守护进程模式启动，并每隔 600 秒（即 10 分钟）检查一次邮件服务器上的新邮件。守护进程模式意味着在 fetchmail 启动后，它会将自己移至后台并继续运行。如果没有这一行，fetchmail 将在启动时检查一次邮件，然后终止运行，之后不再进行检查。

第二个选项告诉 fetchmail 使用本地账户 foobar 作为最后手段地址。换句话说，它接收到的任何无法交付到指定账户的电子邮件都应发送给 foobar。

第三行告诉 fetchmail 将其活动日志记录到文件 `../fetchmail.log` 中。或者，你可以使用 `set syslog` 这一行，在这种情况下，fetchmail 将通过 syslog 设施记录日志。

## 配置邮件服务器选项

`.fetchmailrc` 文件的第二部分包含关于应检查新邮件的各个邮件服务器的信息。以下是邮件部分可能看起来的样子：

poll mail.samplet.org
proto pop3
no dns

第一行告诉 fetchmail 它应在每个全局选项部分设置的轮询间隔（在我们的示例中为 600 秒）检查邮件服务器 `mail.samplet.org`。或者，第一行可以以 `skip` 开头。如果邮件服务器行以 `skip,` 开头，则不会在轮询间隔时轮询，而仅在 fetchmail 命令行中明确指定时才进行轮询。

第二行指定在联系邮件服务器时应使用的协议。在这种情况下，我们使用 POP3 协议。其他合法选项包括 IMAP、APOP 和 KPOP。你也可以在这里使用 AUTO——在这种情况下，fetchmail 将尝试自动确定与邮件服务器配合使用的正确协议。

第三行告诉 fetchmail 不要尝试进行 DNS 查找。如果你正在通过拨号连接运行，可能希望包含此选项。

## 配置用户账户

`.fetchmailrc` 的第三部分也是最后一部分，包含关于前一节中指定的服务器上用户账户的信息。以下是一个示例：

user foobar
pass secretword
fetchall
flush

当然，第一行仅指定用于登录电子邮件服务器的用户名，第二行指定该用户的密码。许多注重安全的人一想到在配置文件中放置明文密码就会感到不安，如果该文件可被组或其他用户读取，他们应该会感到不安。保护此信息的唯一方法是确保文件只能由所有者读取；即文件权限为 `600`。

第三行告诉 Fetchmail 应从服务器获取所有消息，即使它们已经被阅读过。

第四行告诉 Fetchmail 在完成下载后，应删除邮件服务器上的消息。这是默认设置，因此我们实际上不需要指定此选项。如果你希望下载后将消息保留在服务器上，请使用 `no flush` 选项。

你刚刚插入的配置选项使整个 `.fetchmailrc` 文件看起来像这样：

set daemon 600
set postmaster foobar
set logfile ../fetchmail.log

poll mail.siplenel.org
proto pop3
no dns

user foobar
pass secretword
fetchall
flush

此文件告诉 Fetchmail 执行以下操作：

- 每 600 秒检查一次 POP3 服务器 `mail.siplenel.org` 的新邮件
- 使用用户名 `foobar` 和密码 `secretword` 登录
- 从服务器下载所有消息
- 在下载完成后从服务器删除这些消息
- 将其接收到的任何无法交付给本地用户的邮件发送给账户 `foobar`

如前所述，`.fetchmailrc` 文件可以包含比此处列出的更多选项。但是，这些选项可以帮助你使用基本配置开始工作。

为了增加灵活性，你可以定义多个 `.fetchmailrc` 文件，以便在使用同一个 Linux 用户账户的同时从不同的远程邮件服务器获取邮件。例如，你可以为你最常用的账户定义设置，并将其保存在默认的 `.fetchmailrc` 文件中。然后可以快速获取邮件，如下所示：

$ fetchmail -a
1 message for dball at mail.myserver.com (1108 octets).
reading message 1 of 1 (1108 octets). flushed

通过使用 fetchmail 的 -f 选项，你可以指定一个替代资源文件，然后轻松地从另一个服务器获取邮件，如下所示：

$ fetchmail -f .myothermailrc
2 messages for dball at othermail.othserver.org (5407 octets).
reading message 1 of 2 (3440 octets) ... flushed
reading message 2 of 2 (1967 octets) . flushed
You have new mail in /var/spool/mail/dball

通过使用 -d 选项和时间间隔（以秒为单位），你可以以守护进程或后台模式使用 fetchmail。该命令作为后台进程启动，并以指定间隔从指定的远程服务器获取邮件。要了解更高级的选项，请参阅 fetchmail 手册页，其编写非常详尽，并详细记录了所有选项。

![](img/2045828cf45e5632bf056f9ca99d6755_719_0.png)

## 选择邮件传递代理

由于邮件处理的模块化特性，可以使用多个应用程序来处理邮件并实现不仅仅是传递邮件的功能。从存储区域获取邮件并将其显示给用户是邮件传递代理（MDA）的目的。一些邮件客户端（MUA）具有 MDA 功能，这可能会让那些对 UNIX 邮件概念尚不熟悉的人感到困惑。例如，Procmail MDA 基于规则集提供过滤；KMail 和 Evolution 都是 MUA，提供过滤功能，但 MUA pine、mutt 和 Balsa 不提供。一些 MDA 执行简单的排序，而其他 MDA 则旨在消除不需要的电子邮件，例如垃圾邮件和病毒。

你应根据想要对邮件做什么来选择 MDA。我们将查看五个 MDA，它们提供你在特定情况下可能觉得有用的功能。如果你的需求很简单（只是按规则整理邮件），提供过滤功能的其中一个 MUA 可能更适合你的需求。Fedora 提供 Evolution MUA 作为默认选择（并且如前所述，它包含一些 MDA 功能），因此先尝试它，看看是否满足你的需求。如果不满足，请调查 Fedora 提供的以下 MDA 之一。

除非另有说明，所有 MDA 软件均随 Fedora 光盘提供。第 7 章详细介绍了任何软件的一般安装方法。

### Procmail

作为面向高级用户的工具，Procmail 应用程序在从邮件服务器获取电子邮件时充当过滤器。它在读取每个电子邮件消息时使用*规则集*（称为*配方*）。不提供默认配置；你必须为每个用户手动创建一个 `~/.procmail` 文件，或者每个用户可以创建自己的文件。

没有系统范围的默认配置文件。创建规则集并非易事，需要理解正则表达式的使用，这超出了本章的范围。Fedora 确实提供了 `/usr/share/doc/procmail/examples` 中的三个文件示例，以及在 `/usr/share/doc/procmail` 目录中完全注释的示例，该目录还包含 `README` 和 `FAQ`。规则集的详细信息可以在 Procmail 手册页以及 `procmailrc`（从 OCR 错误 `procmaile` 更正而来）、`procmailrc` 和 `procmailex` 的手册页中找到，其中包含 Procmail 配方的示例。

### Spamassassin

如果你使用电子邮件已有一段时间，你很可能会遭受*垃圾邮件*（spam）的侵扰——即同时发送给数千人的 unwanted 电子邮件。Fedora 提供了一个名为 Spamassassin 的 MDA，帮助你减少和消除 unwanted 电子邮件。它易于与 Procmail 和 Sendmail 集成，可以配置用于系统范围和个体使用。它结合使用了规则集和*黑名单*（已知发送垃圾邮件的互联网域名）。

启用 Spamassassin 很简单。你首先必须安装并配置好 Procmail。位于 `/usr/share/doc/spamassassin` 中的 `README` 文件提供了有关配置 `.procmail` 文件以通过 Spamassassin 处理邮件的详细信息。它会通过唯一的标头标记可能的垃圾邮件；然后你可以让 Procmail 按你选择的方式过滤邮件。Spamassassin 的一个有趣用途是使用它来标记仅在旨在吸引垃圾邮件的特殊电子邮件账户上接收的电子邮件。然后，此信息与 Spamassassin 网站共享，这些“垃圾邮件陷阱”产生的命中数据有助于作者微调规则集。

### Squirrelmail

也许你不想在 MUA 中阅读邮件。如果你经常使用 Web 浏览器，通过 Web 界面（例如 Hotmail 或 Yahoo! mail 使用的那种）阅读和发送邮件可能更合理。Fedora 为此目的提供了 Squirrelmail。Squirrelmail 是用 PHP 4 语言编写的，支持 IMAP 和 SMTP，所有页面均以 HTML 4.0 渲染，不使用 Java。它支持 MIME 附件，以及用于隔离电子邮件的地址簿和文件夹。

