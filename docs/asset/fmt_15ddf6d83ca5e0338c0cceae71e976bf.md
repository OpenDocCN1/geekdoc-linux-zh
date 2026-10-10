
使用别名允许你创建邮件列表。这里有一个例子：

- `info-list`: `chris`, `tweaks`, `francois@mailak.com`
- 在示例中，任何发送到 `info-list` 的消息都会发送给 `chris`、`tweaks` 和 `francois@mailak.com`。注意用户列表可以是本地用户和外部邮箱地址的组合。

针对某个用户的消息可以重定向到另一个账户（多个账户）：

- `oldemployee`: `bradford`
- `consultant`: `bradford`, `jackson`, `patterson`
- `users:include:/root/mail/lists`

在这里，任何发往 `oldemployee` 的消息将投递到用户 `bradford` 的邮箱。此外，`bradford`、`jackson` 和 `patterson` 将接收任何发往 `consultant` 的邮件。第三行表示“`users`”别名的接收者在文件 `/root/mail/lists` 中。

邮件可以直接发送到机器上的文件：

- `acsp-bugs`: `/dev/null`
- `trouble-ticket`: `/var/spool/trouble/incoming`

在第一行中，由于虚构的 ACSP 程序不再被机器使用，因此无需跟踪其，所以错误实际上被忽略了。第二行将输入的工单存储在 `/var/spool/trouble/incoming` 文件中。记住，如果你启用了此项，任何人都可以发送足够大的消息来填满该目录所在的分区。这是一个安全风险，在实施前应仔细评估。

## 第 19 章：设置邮件服务器 815

### newaliases

> 提示：在解析地址时，`sendmail` 实际上并不使用 `/etc/aliases` 文件。为了更快的访问，该文本文件会被转换为 Berkeley 数据库文件 `/etc/aliases.db`，它用于解析别名地址。因此，每当修改 `/etc/aliases` 文本文件时，都必须运行 `newaliases` 命令（等于 `sendmail -bi`）来重建数据库文件。这在每次 `sendmail` 重启时都会自动发生。

### 介绍 Postfix

`Postfix` 是一个邮件传输代理（MTA），你可以用替代 `sendmail` 在你的 Fedora 或 Red Hat Linux 系统上处理邮件服务。`Postfix` 的支持者倾向于使用 `Postfix` 而不是 `sendmail` 来提供邮件服务，出于几个原因：

- `Postfix` 设计得更易于管理。`Postfix` 没有在 `sendmail.mc` 文件中使用 `m4` 语法，而是使用了与 Apache Web 服务器中相同类型的指令。
- `Postfix` 内置了多层安全机制，包括在 `chroot` 监狱中运行的能力。它还会在将信息导出到 `Postfix` 环境之前过滤掉任何发送者提供的信息。

尽管某些配置文件和其他组件与 `sendmail` 中的不同，但许多组件是为了替换 `sendmail` 组件的（例如别名、访问和转发文件，以及 `/var/mail` 目录）。为了帮助你从 `sendmail` 迁移，`Postfix` 和 RHEL 已配置这两个软件包以使用替代方案（alternatives）系统。第 10 章描述了如何使用邮件传输代理切换器在两者之间切换。

当你选择 `Postfix` 并启动 `Postfix` 守护进程（如第 10 章所述）时，`Postfix` 将接管 MTA，用 `Postfix` 组件替换 `sendmail` 组件，并使用某些一些相同的邮件邮箱和日志文件位置。`Postfix` 根据 `/etc/postfix` 目录下的配置文件来接管邮件传输。以下是 `Postfix` 服务使用的默认位置概述：

- 邮件配置 (`/etc/postfix/main.cf`) —— `Postfix` 的主配置文件。它标识了队列、命令和别名的位置，并定义了 `Postfix` 服务的主机名和域名。如果你在此处没有添加限定域名，`Postfix` 将使用你的本地主机名作为它代表的邮件服务的名称。
- 邮件邮箱 (`/var/spool/mail`) —— 包含入站邮件文件的目录，每个用户的邮箱由一个以用户名命名的文件表示。（这与 `sendmail` 使用的默认池目录相同）。
- 邮件队列 (`/var/spool/postfix`) —— 邮件消息排队等待的目录位置。

## 第四部分：Fedora 和 RHEL 网络与服务器设置

- 邮件日志 (`/var/log/maillog`) —— 邮件日志文件的位置。

虽然你需要的 `Postfix` 大部分选项都在 `/etc/postfix/main.cf` 文件中描述，但你可以在同一目录下的 `main.cf.default` 文件中看到更多可用选项。基于 `main.cf` 文件中的默认配置，以下是 `Postfix` 处理出站和入站邮件的方式：

- 出站邮件 —— 添加为从此计算机发布邮件的发送主机名。你可能希望将其更改为本地域名（设置 `myorigin=$mydomain`）。
- 入站邮件 —— 默认情况下只有本地主机的邮件保留在本地服务器上。其他邮件会被转发。要将你域名的所有邮件保留在本地服务器上，请在 `mydestination` 行中添加 `$mydomain`。有关配置 `Postfix` 的完整信息，请参阅 `http://www.postfix.org/docs.html`。

### 使用 SpamAssassin 阻止垃圾邮件

尽管这非常无礼且反社会，但仍有人发送成千上万封未经请求的电子邮件（称为垃圾邮件），希望获得一些回复。由于互联网经济学，垃圾邮件发送者可以发送数百万条信息。极少数回复者就足以让垃圾邮件发送者盈利。此外，现代垃圾邮件可能是危险的，包括旨在欺骗用户输入用户名和密码的消息（网络钓鱼），或试图利用漏洞系统的消息（特别是 Windows 系统）。

由于 Linux 系统经常被用邮件服务器，多年来扫描邮件中的垃圾邮件和病毒的工具已变得非常复杂。在本章中，我描述了如何使用 ClamAV 工具处理邮件服务器上的垃圾邮件。如果这不能满足你的需求，你可以添加 ClamAV 病毒扫描器来测试邮件是否存在真实的恶意软件附件。以下是一些你可以通过它们了解 ClamAV 以及它如何与不同软件配合使用的链接：

- ClamAV (`www.clamav.net`) —— 具有数据库功能的命令行病毒扫描器。`clam` 包在 Fedora 仓库中（`yum install clamav`）。
- ClamAV (`http://clamav.sourceforge.net/clamavwiki/index.php`) —— KDE 版本的 ClamAV（`yum install clamav`）。
- 第三方应用 (`www.clamav.net/party.html`) —— 与 ClamAV 配合的第三方软件链接。

### 使用 SpamAssassin

通过 `SpamAssassin`，你可以配置你的入站邮件服务，标记它认为可能是垃圾邮件的消息，以便你的用户处理这些消息。`SpamAssassin` 使用了多种方法来识别垃圾邮件：

- **检查邮件标头** —— 检查入站邮件的标头，寻找用于使电子邮件看起来有效的常用技巧。
- **检查邮件正文** —— 在邮件正文中寻找垃圾邮件中常用的样式、内容和免责声明。
- **检查黑名单** —— 检查黑名单以查找从已知转发垃圾邮件站点发送的邮件。`mail-abuse.com` 网站提供了一个搜索工具来检查特定 IP 地址是否被列黑。（要使用该工具，请访问 `mail-abuse.com/cgi-bin/lookup`。）
- **检查垃圾签名** —— 比较电子邮件签名。由于垃圾邮件通常由数千条完全相同的消息组成，对垃圾邮件提取签名可以让 `SpamAssassin` 将你的消息与已知垃圾邮件数据库进行比较。`SpamAssassin` 使用 `Razor`（参见 `http://razor.sourceforge.net`）。

尽管有许多处理垃圾邮件的不同方法，我咨询的大多数专家都配置 `SpamAssassin` 来统计看起来像垃圾邮件的入站邮件。他们鼓励服务器的每个用户创建自己的过滤规则。注意：虽然该程序描述了如何使用与最新版本 Fedora 自带的 `SpamAssassin` RPM 包，但许多人直接从 `SpamAssassin` 官网获取 `SpamAssassin` 版本。因为反垃圾邮件软件进化非常快（为了走在垃圾邮件发送者前面），一些人希望确保他们拥有最新版本。从源码安装 `spamassassin` 的指令可以在 `SpamAssassin` 下载页面获取：`http://spamassassin.apache.org/downloads.cgi`。通常，你可以对 tar 包运行 `rpmbuild -bb` 命令来创建一个新的 RPM。

### 为你的邮件服务器设置 SpamAssassin

以下是启用 `SpamAssassin` 并让用户选择处理垃圾邮件的快速步骤：

1. 配置你的邮件传输代理（`sendmail` 或 `Postfix`）使用 `procmail` 作为其邮件器。对于 `sendmail`，根据 `/sendmail.mc` 中的以下行：

```
FEATURE(local, 'procmail -t -Y')
```
