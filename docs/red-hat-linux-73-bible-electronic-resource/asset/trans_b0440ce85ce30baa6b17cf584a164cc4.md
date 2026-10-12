

## 别名文件

处理邮件投递（而非针对某个特定用户，而是针对整个系统）的更灵活方法涉及 `/etc/aliases` 文件，该文件同样是一个纯文本文件。别名文件（在 sendmail.cf 章节中已有描述）包含一个名称，后跟一个冒号，接着是用户名、另一个别名、收件人列表、文件，或者邮件将被投递到的程序。冒号左侧的名称（可以是有效的用户名，也可以只是一个别名）随后可以在本地机器上用作电子邮件收件人。使用别名文件进行邮件别名化允许对常规邮件处理行为进行若干扩展：

- 一个账户可以在几个不同的名称下接收邮件：
  - `patterson: jkpat`
    这表示任何发给 patterson@mybox.com（仅是一个别名）的邮件都会到达 jkpat（一个实际的用户账户）的邮箱。

- 邮件可以在一个不是有效（或合理）的用户名下被接收：
  - `Charlie.Jackson.II@mybox.com: jackson`
    他实际上并不希望输入 Charlie.Jackson.II 作为用户名，但这并不意味着他不能以此方式接收邮件。

- 原本发给一个用户的消息可以被重定向到另一个账户（或几个账户）：
  ```
  oldemployee: bradford
  consultant: bradford, jackson, patterson
  users: :include: /root/mail/lists/users
  ```
  在此处，任何发给 oldemployee@mybox.com 的消息都会被投递到用户 bradford 的邮箱。此外，用户 bradford、jackson 和 patterson 将会接收到所有发给 consultant 的邮件。第三行表示“users”别名的收件人在文件 /root/mail/lists/users 中指定。

- 邮件可以直接发送到本地机器上的一个文件：
  ```
  acsp-bugs: /dev/null
  trouble-ticket: /var/spool/trouble/incoming
  ```
  在第一行中，由于虚构的 ACSP 程序不再在该机器上使用，因此没有必要跟踪其错误，所以邮件实际上被忽略。第二行将传入的故障工单存储在 /var/spool/trouble/incoming 文件中。请记住，如果你启用此功能，任何地方的任何人都可以向你发送足够大的消息以填满该目录所在分区的空间。这是一个安全风险，实施前应仔细评估。

- 传入的消息可以直接通过管道传入可执行程序：
  - `majordomo: "| /usr/lib/majordomo/wrapper majordomo"`

**提示：** 在解析地址时，sendmail 实际上并不使用 `/etc/aliases` 文本文件。为了更快的访问速度，文本文件会被转换为 Berkeley 数据库格式文件，即 `/etc/aliases.db`，用于解析别名地址。因此，每次修改 `/etc/aliases` 文本文件时，都必须运行 `newaliases` 命令（等效于 `sendmail -bi`）来重建数据库文件。

## 介绍 Postfix

Postfix 是一个邮件传输代理（MTA），你可以用它替代 Sendmail 来处理 Red Hat Linux 系统上的邮件服务。Postfix 旨在提供更容易的管理和更高的安全性。

虽然许多配置文件和其他组件与 Sendmail 的不同，但有些组件旨在替代 Sendmail 的组件。为了帮助你从 Postfix 过渡到 Sendmail，Red Hat Linux 已配置这两个包使用 alternatives 系统。第 10 章描述了如何使用邮件传输代理切换器（Mail Transport Agent Switcher）在两种传输方式之间切换。

当你按照第 10 章的描述切换到 Postfix 并启动 Postfix 守护进程时，Postfix 将接管 MTA 角色，用 Postfix 组件替换 Sendmail 组件，并使用一些相同的位置存放邮箱和日志文件。Postfix 基于 `/etc/postfix` 目录中设置的配置文件接管邮件传输。以下是 Postfix 服务默认使用的位置概览：

- **邮件配置**（`/etc/postfix/main.cf`） — Postfix 的主要配置文件。标识 Postfix 队列、命令和别名的位置，以及定义 Postfix 所服务的主机名和域名。如果你不在此文件中添加完全限定域名，Postfix 将使用你的本地主机名作为它代表的邮件服务的名称。

- **邮箱**（`/var/spool/mail`） — 包含传入邮件文件的目录，每个用户的邮箱由一个以该用户名称命名的文件表示。（这与 Sendmail 使用的默认 spool 目录相同。）

- **邮件队列**（`/var/spool/postfix`） — 邮件消息排队等待投递的目录位置。

- **邮件日志**（`/var/log/maillog`） — 邮件日志文件的位置。

尽管 Postfix 所需的大多数选项都描述在 `/etc/postfix/main.cf` 文件中，你可以在同一目录下的 `main.cf.default` 文件中看到许多其他可用选项。基于 `main.cf` 文件中的默认配置，Postfix 将按如下方式处理出站和传入邮件：

- **出站邮件** — 本地主机名会被添加为从该计算机发布的邮件的发送主机。你可能希望将其更改为本地域名（设置 `myorigin = $mydomain`）。

- **传入邮件** — 默认情况下，只有发往本地主机名的邮件会被保留在本地服务器上。其他邮件会被转发。若要将你域名的所有邮件保留在本地服务器上，请在 mydestination 行中添加 $mydomain。

## 其他邮件列表管理器

尽管所有邮件列表管理器的基本列表服务器概念是通用的，但一些包提供了截然不同的功能，并以不同的方式处理任务。以下是可用于 Linux 的一些其他列表服务器：

- **CREN ListProc 9.0** — 向 CREN（研究与教育网络公司）捐赠 2,000 美元即可获得。此邮件列表管理器功能包括基于 Web 的管理、广泛的日志记录能力以及自动删除无效地址。有关进一步信息和免费试用版，请访问 www.cren.net/listproc。

- **listar** — 此免费的邮件列表管理器（最初为 Linux 创建）具有非特权执行、通过电子邮件的安全远程管理功能，以及通过动态加载模块实现的可扩展性。更多详细信息和源代码可从 www.listar.org 获取。

- **L-Soft LISTSERV** — 已使用十多年（最初在 IBM 大型机计算机上），此包具有通过电子邮件进行文件传输、索引、摘要以及订阅标记等功能。详细信息、价格信息和受限免费试用版可从 www.lsoft.com/listserv.stm 下载。

如需了解配置 Postfix 的更完整信息，请参阅随 postfix 包附带的文档（HTML 格式）。若要开始使用该文档，你可以从终端窗口输入以下内容在 Netscape Navigator 中打开它：

```bash
$ netscape /usr/share/doc/postfix*/html/index.html
```

## 管理邮件列表

尽管 sendmail 提供了几种灵活的地址别名方法，但许多情况需要额外的功能。邮件列表管理器（或更常见的列表服务器）提供了处理大型分发列表的能力，并结合了诸如版主、带文件传输的存档、摘要、自动订阅以及自动过滤无效地址等高级功能。

列表服务器通常提供多种配置每个列表的选项（回复发给作者、回复发给列表、任何人可以向列表发布帖子、帖子仅限于订阅者、订阅对任何人开放、订阅必须经过确认等）。它们还提供选项来确定消息如何呈现给收件人（使用自定义页眉和页脚、主题前缀、在页眉或正文中过滤文本等）。

本节简要介绍了 majordomo 邮件列表管理器。Majordomo 是用 Perl 编写的免费列表服务器，除了一个包装器程序（非 Perl 编写）允许切换到 majordomo 用户外，没有其他例外。配置文件（针对列表服务器以及每个单独的列表）均为纯文本，且易于编辑。其他可用的邮件列表管理器列在附带的边栏中。

### 安装 majordomo

Majordomo 以 RPM 格式可从任何 Red Hat 镜像站点获取，源代码发行版可从 www.greatcircle.com/majordomo 获得。如果包位于当前目录中，可以使用以下命令安装：

```bash
# rpm -ivv majordomo*
```

### 配置 majordomo

应该在 `/etc/aliases` 文件中添加几个别名。这些别名允许将邮件相关账户列在不同名称下：

```text
#
#  Majordomo Aliases
#
listserv: listserv
listserver: listserv
majordomo: listserv
listserv: "| /usr/lib/majordomo/wrapper majordomo"
majordomo-owner: owner-majordomo
owner-majordomo: owner-listserv
listserv-owner: owner-listserv
owner-listserv: mailserverguy@mybox.com
#
# List Aliases
#
# The BioChemistry List
#
biochem-request: "| /usr/lib/majordomo/wrapper request-answer biochem"
biochem-approval: biochem-owner
biochem-owner: owner-biochem
owner-biochem: emailguy@mybox.com
biochem: "| /usr/lib/majordomo/wrapper resend -l biochem -h mail.mybox.com -R biochem-out"
biochem-out: :include:/var/lib/majordomo/lists/biochem,biochem-archival
biochem-archival: "| /usr/lib/majordomo/wrapper archive2.pl -a -M -f /var/lib/majordomo/archives/biochem/biochem"
```

第一组别名确立了“拥有”列表服务器的个人（或者至少是接收其错误消息的人）以及 majordomo 已知的名称。它最主要的...

