
- **邮件队列** (`/var/spool/postfix`) — 邮件消息排队等待投递的目录位置。
- **邮件日志** (`/var/log/maillog`) — 邮件日志文件的位置。

虽然 Postfix 所需的大多数选项都描述在 `/etc/postfix/main.cf` 文件中，但你可以在同一目录的 `main.cf.default` 文件中看到更多可用的选项。根据 `main.cf` 文件中的默认配置，Postfix 将如下处理发出的邮件和收到的邮件：

- **发出邮件** — 本地主机名将被添加为从这台计算机发出的邮件的发送主机。你可能希望将其更改为本地域名（设置 `myorigin = $mydomain`）。
- **接收邮件** — 默认情况下，只有发往本地主机名的邮件才保留在本地服务器上。其他邮件将被转发。若要使域名的所有邮件都保留在本地服务器上，请将 `$mydomain` 添加到 `mydestination` 行。

有关配置 Postfix 的完整信息，请参阅 www.postfix.org/docs.html。

## 使用 SpamAssassin 阻止垃圾邮件

尽管这很无礼且令人讨厌，但仍有人发送数千条未经请求的电子邮件（称为垃圾邮件），希望得到一些回复。使用名为 SpamAssassin 的工具，你可以配置你的收件邮件服务，对其认为的垃圾邮件进行标记，以便你和你的用户自行处理这些邮件。

SpamAssassin 用于识别垃圾邮件的几种方法如下：

- **检查邮件头** — 检查你的来信邮件的头部，查找用于使电子邮件看起来有效的已知技巧。
- **检查邮件正文** — 查找邮件正文中常用的文本样式、内容和免责声明，这些在垃圾邮件中常见。
- **检查黑名单** — 检查 `mail-abuse.org`、`ordb.org` 以及其他黑名单，以查找来自已知曾发送垃圾邮件的网站的电子邮件。
- **检查垃圾邮件签名** — 比较电子邮件签名。由于垃圾邮件通常由数千次发送的完全相同的消息组成，对垃圾邮件进行签名可让 SpamAssassin 将你的邮件与已知垃圾邮件数据库进行比较。SpamAssassin 使用 Vipul's Razor（参见 `http://razor.sourceforge.net`）。

尽管处理垃圾邮件（或更确切地说是 *可能* 是垃圾邮件的电子邮件）的方法有很多，但我咨询的大多数专家都喜欢配置 SpamAssassin 仅对看起来像垃圾邮件的来信进行标记。然后他们鼓励每位邮件服务器用户创建自己的垃圾邮件过滤规则。

## 在你的邮件服务器上设置 SpamAssassin

以下是启用 SpamAssassin 并让用户自行决定如何处理遇到的垃圾邮件的快速流程：

- 1. 配置你的邮件传输代理（sendmail 或 postfix）使用 procmail 命令作为其邮件处理器。对于 sendmail，它已基于 /etc/mail/sendmail.mc 文件中的以下行配置为默认邮件处理器：
```
FEATURE(`local_procmail',` `procmail -t -Y -a $h -d $\')dnl
```
- 2. 确保 SpamAssassin spamd 守护进程正在运行（它应在运行级别 2-5 下已开启），如果没有，请以 root 用户身份输入以下命令启动它：
```
# chkconfig --list spamassassin
spamassassin        0:off     1:off     2:on      3:on      4:on      5:on      6:off
# chkconfig spamassassin on
```
- 3. 创建一个 /etc/procmailrc 文件（使用任何文本编辑器，以 root 用户身份）。此 procmailrc 文件示例将 procmail 接收到的所有邮件消息通过 spamc 管道传输（spamc 是上一步中启动的 spamd 守护进程的客户端）：
```
:0fw
| /usr/bin/spamc
```
如果愿意，你可以在 procmailrc 文件中做更多操作来在系统范围内处理垃圾邮件。例如，你可以创建 procmail 配方，将报告的垃圾邮件消息分类到系统范围的垃圾邮件文件夹中或完全删除它们。同样，每个用户也可以创建单独的 $HOME/.procmailrc 文件来创建个人 procmail 配方。（输入 man procmailex 可查看 procmailrc 文件中规则的示例。）
- 4. 检查 /etc/mail/spamassassin/local.cf 文件。该文件包含 SpamAssassin 在系统范围内使用的规则，除非被用户个人的 $HOME/.spamassassin/user_prefs 文件覆盖。以下是 local.cf 文件的内容：
```
required_hits 5
rewrite_subject 1
subject_tag [SPAM]
report_safe 0
```
required_hits 行表示需要 5 分才能将邮件标记为垃圾邮件。对于公共邮件服务器，你应将其设置得更高（例如 8 或 10）。将 rewrite_subject 设置为 1 可允许 SpamAssassin 修改邮件的主题行。subject_tag [SPAM] 行会让 SpamAssassin 在找到的垃圾邮件的主题行中添加文本 "[SPAM]"。report_safe 0 行可确保仅更改邮件头，而内容保持完整。（输入 **man Mail::SpamAssassin::Conf** 可查看可在 `local.cf` 文件中使用的其他设置。）

由于几乎肯定会出现一些误报，如果进行系统范围的过滤，你可能会阻止用户看到他们需要的电子邮件。为避免此问题，此处所示的方法让用户自行决定如何处理被标记为垃圾邮件的电子邮件。

接下来，你应让该邮件服务器的用户在其主目录中设置自己的用户首选项。每个用户 `$HOME/.spamassassin/user_prefs` 文件中设置的首选项有助于告诉 SpamAssassin 如何处理该用户的电子邮件。以下是用户可能希望在该文件中包含的行示例：
```
required_hits               3
whitelist_from    jsmith@example.com  bjones@example.net
blacklist_from    *.example.org
```
The `required_hits` line (which is on by default) sets the number of hits needed to consider the message to be spam. Hits are based on scores for matching or not matching criteria in the tests SpamAssassin performs. (See `http://spamassassin.org/tests.html`.)

The `whitelist_from` and `blacklist_from` lines let you set addresses for people, individual hosts, or entire domains that should not be considered as spam (`whitelist_from`) or should always be considered as spam (`blacklist_from`). For other ways to modify SpamAssassin behavior, type the following command: **man Mail::SpamAssassin::Conf**.

At this point, SpamAssassin should be running and identifying spam based on input from you and the people using your e-mail server. Next, each user needs to decide what to do with the messages that are marked as spam, as described in the following section.

> **提示：** 你可以与 SpamAssassin 一起使用的技术包括 RealTime Blackhole Lists (RBL) 和 SpamCop 等服务。使用 RBL (`http://mail-abuse.org/rbl`)，你可以在垃圾邮件到达服务器之前就将其阻止。SpamCop (`www.spamcop.net`) 提供一项服务，允许你将收到的垃圾邮件输入到数据库中，帮助他人阻止相同的垃圾邮件。

## 设置邮件阅读器以过滤垃圾邮件

每个用户都可以在其邮件阅读器中启用过滤，以决定如何处理 SpamAssassin 标记为垃圾邮件的每条消息。常见做法是将标记为垃圾邮件的邮件定向到单独的文件夹。由于真正的邮件偶尔会被错误标记为垃圾邮件，你可以每隔一两周检查一次垃圾邮件文件夹，以确保没有遗漏任何内容。

以下是从 Evolution Email 添加过滤规则的示例：

- 1. 在你的收件箱下创建一个标记为 SPAM 的文件夹。
- 2. 点击 工具 → 过滤器。
- 3. 在过滤器窗口中，点击 添加。会出现一个添加规则窗口。
- 4. 指定一个规则名称（例如 Spam），该规则添加一个条件，查找包含特定文本（YES）的特定头部（X-Spam-Flag）。然后在 添加操作 下，选择一个操作（移动到文件夹）并指定包含垃圾邮件的文件夹（SPAM）。

当你请求从邮件服务器接收邮件时，所有 X-Spam-Flag 设置为 yes 的邮件都将被分类到你的 SPAM 文件夹中。或者，你也可以将主题行中出现文本 [SPAM] 作为分类垃圾邮件的依据。

其他邮件阅读器（Mozilla mail、pine、Netscape mail 等）也包含根据你输入的标准过滤和排序电子邮件的功能。

## 从服务器获取邮件（POP）

一旦你设置了邮件服务器，你将希望让用户从该服务器访问其电子邮件。这意味着要么让每个用户登录邮件服务器阅读电子邮件，要么更可能的是配置邮局协议（POP）或 IMAP，让他们将邮件下载到工作站。

本节介绍如何使用 POP 允许你的邮件服务器用户通过网络从服务器下载邮件消息。POP 是访问网络上邮箱的两种协议中更常见、更简单的协议。

## 在 Linux 中访问邮箱

当电子邮件消息在你的 sendmail 或 postfix 邮件服务器上接收时，它们会被分类到单独的文件中，每个文件代表一个用户的邮箱。邮箱文件的默认位置是 `/var/spool/mail` 目录。因此，登录账户 jsmith 将拥有一个邮箱：
```
/var/spool/mail/jsmith
```
在登录邮件服务器时，jsmith 可以简单地从终端窗口输入 mail 来阅读他的电子邮件（使用简单的基于文本的 mail 命令）。然而，由于大多数人更喜欢从自己桌面电脑的舒适环境中获取电子邮件，你可以设置邮局协议（POP）或互联网消息访问协议（IMAP）。

POP 和 IMAP 服务器在网络上监听用户电子邮件的请求，然后要么将邮箱的全部内容下载到用户的邮件阅读器（像 POP 那样），要么让用户在邮件保留在服务器上的同时管理邮件（像 IMAP 那样）。

通常，你的邮件服务器将被配置为使用 POP 或 IMAP 向用户提供电子邮件（尽管可以在同一台机器上同时运行两者）。

下一节介绍如何设置 POP 服务以允许访问电子邮件账户。此服务要求你在服务器上安装了 imap RPM 包。
