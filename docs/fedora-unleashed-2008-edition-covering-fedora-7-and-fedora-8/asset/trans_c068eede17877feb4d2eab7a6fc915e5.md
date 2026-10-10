
## 配置用户账户

.fetchmailrc 文件的第三部分也是最后一部分，包含关于服务器（在上一部分中指定）上用户账户的信息。以下是一个示例：

```
user foobar
pass secretword
fetchall
flush
```

当然，第一行是用于登录邮件服务器的用户名，第二行指定该用户的密码。许多注重安全的人一想到在配置文件中明文存储密码就会感到不舒服，如果该文件对其他用户或所有人可读，他们确实应该感到不安。保护此信息的唯一方法是确保该文件仅可由所有者读取；也就是说，文件权限应为 600。

第三行告诉 Fetchmail 应从服务器获取所有邮件，即使它们已经被读取。

第四行告诉 Fetchmail 在完全下载邮件后，应将其从邮件服务器中删除。这是默认行为，因此您实际上无需指定此选项。如果您希望在下载后保留服务器上的邮件，请使用 `no flush` 选项。

您刚才插入的配置选项将整个 .fetchmailrc 文件配置为如下所示：

```
set daemon 600
set postmaster foobar
set logfile ./.fetchmail.log

poll mail.sompenet.org
proto pop3
no dns

user foobar
pass secretword
fetchall
flush
```

此文件指示 Fetchmail 执行以下操作：

- 每 600 秒检查一次 POP3 服务器 `mail.samplingnet.org` 上的新邮件。
- 使用用户名 `foobar` 和密码 `secretword` 登录。
- 下载服务器上的所有邮件。
- 在 Fetchmail 完成下载后，从服务器中删除这些邮件。
- 将 Fetchmail 接收到的任何无法投递给本地用户的邮件发送给账户 `foobar`。

如前所述，`.fetchmailrc` 文件可以包含比此处列出的更多选项。然而，这些选项足以让您开始使用基本配置。

为了获得更大的灵活性，您可以定义多个 `.fetchmailrc` 文件，以便使用同一个 Linux 用户账户从不同的远程邮件服务器检索邮件。例如，您可以为您最常用账户定义设置，并将其保存在默认的 `.fetchmailrc` 文件中。然后就可以像这样快速检索邮件：

```
$ fetchmail -a
1 message for ahudson at mail.myserver.com (1108 octets).
reading message 1 of 1 (1108 octets). flushed
```

通过使用 Fetchmail 的 `-f` 选项，您可以指定替代资源文件，然后轻松地从此另一服务器检索邮件，如下所示：

```
$ fetchmail -f .myothermailrc
2 messages for bball at othermail.otherverser.org (5407 octets).
reading message 1 of 2 (3440 octets). flushed
reading message 2 of 2 (1967 octets). flushed
You have new mail in /var/spool/mail/bball
```

通过使用 `-d` 选项并指定时间间隔（以秒为单位），您可以将 Fetchmail 用于守护程序——或后台——模式。该命令作为后台进程启动，并以指定间隔从指定的远程服务器检索邮件。有关更多高级选项，请参阅 Fetchmail 手册页，该手册页编写得非常详尽，详细记录了所有选项。

> **注意**  
> 由于 `.fetchmailrc` 文件包含您的邮件服务器密码，它应仅对您可读。这意味着它应由您拥有，且权限不得超过 600。如果 `.fetchmailrc` 文件的权限大于此值，Fetchmail 会发出抱怨并拒绝启动。

## 选择邮件传输代理

由于邮件处理具有模块化特性，因此可以使用多个应用程序来处理邮件，而不仅仅是投递邮件。从存储区域获取邮件并将其显示给用户是邮件传输代理（MDA）的目的。MDA 功能可以在某些邮件客户端（MUA）中找到，这可能会让那些对 UNIX 邮件概念尚不熟悉的人感到困惑。例如，Procmail MDA 提供基于规则集的过滤功能；KMail 和 Evolution（两者都是 MUA）也提供过滤功能，但 MUA pine、mutt 和 Balsa 不提供。一些 MDA 执行简单的排序，而其他 MDA 则旨在消除不需要的电子邮件，例如垃圾邮件和病毒。

您应根据希望如何处理邮件来选择 MDA。以下部分将介绍五个 MDA，它们提供的功能在您的特定情况下可能有用。如果您的需求很简单（只需按规则组织邮件），那么提供过滤功能的 MUA 可能更适合您的需求。Fedora 默认提供 Evolution MUA（如上所述，它包含一些 MDA 功能），因此请首先尝试该 MUA，看看它是否满足您的需求。如果不能满足，请研究 Fedora 提供的以下 MDA 之一。

除非另有说明，所有 MDA 软件均随 Fedora 光盘提供。第 34 章详细介绍了任何软件的一般安装方法。

### Procmail

作为高级用户的工具，Procmail 应用程序在从邮件服务器获取邮件时起过滤器作用。它使用规则集（称为配方）来读取每封电子邮件。不提供默认配置；您必须为每个用户手动创建 `.procmailrc` 文件，或者每个用户可以创建自己的文件。

没有系统范围的默认配置文件。创建规则集并非易事，需要对正则表达式的使用有深刻理解，这超出了本章的范围。Fedora 确实在 `/usr/share/doc/procmail/examples` 中提供了这三个文件的示例，并且在 `/usr/share/doc/procmail` 目录中提供了带有完整注释的示例，该目录还包含 Read Me 和 FAQ。有关规则集的详细信息可在 Procmail 的手册页中找到，以及 `procmailrc`、`procmailrc` 和 `procmaillex` 的手册页（包含 Procmail 配方的示例）中也有记载。

### Spamassassin

如果您使用电子邮件有一段时间了，您可能已经遭受过垃圾邮件的困扰——即垃圾邮件是同时发送给成千上万人的 unwanted 电子邮件。Fedora 提供了一个名为 Spamassassin 的 MDA，以帮助您减少和消除不需要的电子邮件。它可以轻松与 Procmail 和 Sendmail 集成，并可以配置为系统范围和个人使用。它采用规则集和黑名单（已知发送垃圾邮件的互联网域名）的组合。

启用 Spamassassin 很简单。您必须先安装并配置 Procmail。位于 `/usr/share/doc/spamassassin` 中的 *Read Me* 文件提供了有关配置 `.procmail` 文件以便通过 Spamassassin 处理邮件的详细信息。它会为可能的垃圾邮件添加独特的标头；然后您可以让 Procmail 以任何您选择的方式过滤邮件。Spamassassin 的一个有趣用途是将其用于标记专门用于吸引垃圾邮件的特殊电子邮件账户收到的邮件。此信息随后与 Spamassassin 网站共享，其中由这些“垃圾邮件陷阱”生成的命中次数有助于作者微调规则集。

### Squirrelmail

也许您不想在 MUA 中阅读邮件。如果您经常使用 web 浏览器，通过 web 界面阅读和发送邮件可能是有意义的，例如 Hotmail 或 Yahoo! Mail 使用的那种界面。Fedora 提供 Squirrelmail 正是用于此目的。Squirrelmail 使用 PHP 4 语言编写，支持 IMAP 和 SMTP，所有页面均以 HTML 4.0 渲染而不使用 Java。它支持 MIME 附件，以及用于隔离电子邮件的地址簿和文件夹。

您必须配置 web 服务器以支持 PHP 4。详细安装说明可在 `/usr/share/doc/squirrelmail/INSTALL` 中找到。配置完成后，将您的 web 浏览器指向 `http://www.yourdomain.com/squirrelmail/` 即可阅读和发送电子邮件。

### 病毒扫描器

尽管目前的普遍看法是，Linux 对针对 Microsoft Outlook 用户的电子邮件病毒具有免疫力，但显然 UNIX 邮件服务器允许受感染的电子邮件通过它们发送是没有道理的。虽然 Fedora 不提供病毒扫描器，但许多此类扫描器中较受欢迎的是 MailScanner，可从 `http://www.eng.scs.mot.com/mailscanner/` 获取；也有 Fedora RPM 包以及源代码可用。它支持 Sendmail 和 Exim，但不支持 Postfix 或 Qmail。在 Freshmeat.net 上搜索“*病毒*”和“*电子邮件*”这两个术语，将发现一份令人惊讶的、可能满足您需求的带有 GPL 许可证的病毒扫描器列表。

### 特殊邮件传输代理

如果您已经使用 Hotmail 或其他基于 web 的电子邮件账户，当前可用的 MUA 对您没有用：无法免费获得 Hotmail 账户的正式 POP3 访问。但是，Microsoft Outlook Express 可以使用称为 `HTTPMail` 的特殊协议免费访问 Hotmail。其实现方式在 RFC 2518 中作为“HTTP/1.1 的 WebDAV 扩展”进行了介绍。Fedora 没有提供特定的解决方案，但它提供的基本工具辅以一些巧妙的 Perl 编程就足够了。

Hotwayd 可从 `http://sourceforge.net/projects/hotwayd/` 获取并实现此功能，允许您使用您喜爱的邮件客户端阅读来自 Hotmail 的邮件。

较新的 Hotmail 访问工具是 Gotmail，来自 `http://sourceforge.net/projects/gotmail/`。这是一个易于配置的 Perl 脚本。在 `http://www.madpenguin.org/cms/?m=show&id=437` 上有关于配置其与 KMail 和 Evolution 一起使用的简短教程。
