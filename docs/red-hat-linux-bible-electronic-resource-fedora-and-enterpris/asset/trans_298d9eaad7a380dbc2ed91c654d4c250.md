
> **提示：** 有时，你可能想在一台不是你常用电脑的电脑上检查电子邮件，但仍希望以后能保存这些邮件。在这种情况下，大多数邮件阅读器允许你选择一个设置，将电子邮件复制下来而不从 POP 服务器中删除它们。这样，当你回到常用电脑时，就能再次下载这些邮件。

## 配置 POP

通过配置 POP 服务器监听网络请求，你的邮件服务器的用户可以从网络上的另一台电脑下载他们的电子邮件。以下过程描述如何启用你的 POP 服务。

- 1. Turn on the POP service by typing the following (as root user):

```bash
# chkconfig ipop3 on
```

- 2. Start the POP service immediately by restarting the xinetd super-server as follows:

```bash
# /etc/init.d/xinetd restart
```

> **注意：** 大多数电子邮件客户端支持 POP3。然而，如果你使用的是较旧的邮件阅读器，你可以改用 `ipop2` 而不是前面所示的 `ipop3`。如果你的用户使用具有 SSL 支持的邮件阅读器，你可以使用 `pop3s` 服务，这样下载的邮件将被加密（以获得更好的安全性）。

所有在你的邮件服务器上拥有用户账户的用户，默认情况下都被配置为接收电子邮件。例如，如果电子邮件发送到 mail.handsonhistory.com 服务器的用户 jsmith，邮件将被复制到服务器上的 /var/spool/mail/jsmith 文件中。继续这个例子，从 jsmith 的电脑上，他可以按如下方式设置他的邮件阅读器：

- **邮件服务器：** mail.handsonhistory.com
- **用户名：** jsmith
- **密码：** theuserspassword
- **协议：** POP3

配置好邮件阅读器后，当 jsmith 从他的邮件阅读器中点击发送和接收时，/var/spool/mail/jsmith 文件中的所有电子邮件都会下载到他的本地邮件阅读器中。然后这些邮件将被从服务器中删除。

> **注意：** 如果你的任何用户都无法从邮件服务器下载邮件，请检查你的防火墙（iptables 或 ipchains）是否配置为允许访问 POP 服务。默认情况下，`pop3` 监听 110 端口，`pop2` 监听 109 端口，而具有 ssl 支持的 `pop3` 监听 995 端口。

## 管理邮件列表

即使 sendmail 提供了几种灵活的地址别名方法，许多情况仍需要额外的功能。邮件列表管理器（或更常见的列表服务器）提供处理大型分发列表的能力，并结合高级功能，如版主、带文件传输的归档、摘要、自动订阅和自动过滤不良地址。

列表服务器通常为每个列表的配置提供多种选项（回复发送给作者、回复发送给列表、任何人都可以向列表发帖、发帖仅限订阅者、订阅向任何人开放、订阅必须确认等等）。它们还提供消息如何呈现给收件人的选项（带自定义页眉和页脚、主题前缀、标题或正文中的过滤文本等等）。

本节简要描述 majordomo 邮件列表管理器。Majordomo 是一个用 Perl 编写的免费列表服务器，例外的是一个包装程序（不是用 Perl 编写的），它允许切换到 majordomo 用户。配置文件（列表服务器以及每个单独列表的）都是纯文本，易于编辑。其他可用的邮件列表管理器列在随附的侧边栏中。

### 其他邮件列表管理器

尽管列表服务器的基本概念对所有邮件列表管理器都是共通的，但某些软件包提供截然不同的功能并以不同方式处理任务。以下是在 Linux 上可用的一些其他列表服务器：

- **Mailman GNU 列表管理器** — Mailman 列表管理器包含一个用于使用和管理邮件列表的 Web 界面。每个邮件列表的主页都可以自定义，用户可以使用 Web 浏览器轻松订阅和取消订阅。你可以从 www.list.org 下载并获取有关 Mailman 的更多信息。
- **CREN ListProc 9.0** — 该邮件列表管理器具有基于 Web 的管理、广泛的日志记录功能和自动删除不良地址的功能。它最近成为一个 sourceforge 项目（*sourceforge.net/projects/listproc*）。
- **L-Soft LISTSERV** — 已使用十多年（最初在 IBM 大型机上），该软件包具有通过电子邮件进行文件传输、索引、摘要和订阅标志等功能。详细信息、定价信息和受限的免费试用版可以从 www.lsoft.com/list-serv.stm 下载。

### 安装 majordomo

Majordomo 以 RPM 格式提供，可从 rpmfind.net 获取，源代码分发包可从 www.greatcircle.com/majordomo 获取。可以使用以下命令安装软件包（软件包位于当前目录）：

```bash
# rpm -Uhv majordomo*
```

### 配置 majordomo

应向 /etc/aliases 文件添加几个别名。这些别名允许邮件相关账户在不同名称下列出：

```
#  Majordomo Aliases
#
listserve: listserv
listserver: listserv
majordomo: listserv
listserv: "| /usr/lib/majordomo/wrapper majordomo"
majordomo-owner: owner-majordomo
owner-majordomo: owner-listserv
listserv-owner: owner-listserv
owner-listserv: mailserverguy@mybox.com
#
#  List Aliases
#  The BioChemistry List
#
biochem-request: "| /usr/lib/majordomo/wrapper request-answer biochem"
biochem-approval: biochem-owner
biochem-owner: owner-biochem
owner-biochem: emailguy@mybox.com
biochem: "| /usr/lib/majordomo/wrapper resend -l biochem -h mail.mybox.com -R biochem-out"
biochem-out: :include:/var/lib/majordomo/lists/biochem,biochem-archival
biochem-archival: "| /usr/lib/majordomo/wrapper archive2.pl -a -M -f /var/lib/majordomo/archives/biochem/biochem"
```

第一组别名确定了“拥有” listserv 的个人（或至少接收其错误消息的人）以及 majordomo 将被识别的名称。最常见的是向“listserv”地址发送请求，这有时会被混淆并翻译成“listserve”或“listserver”，因此这些也是可以接受的。

下一个块是用于生物化学列表的。与 listserv 本身一样，每个列表都有一个所有者来控制其配置并在出现错误时收到通知。发送到 biochem@mail.mybox.com 的邮件会发送到 /var/lib/majordomo/lists/biochem 文件中的收件人。邮件也会发送到 archive2.pl Perl 脚本。归档的邮件存储在诸如 /var/lib/majordomo/archives/biochem/biochem.200305（2003 年 5 月归档）的文件中。

### 运行 majordomo

不幸的是，这些精彩的功能目前还不能正常工作。首先，需要使用 newaliases 命令或 sendmail -bi 重建别名数据库。接下来，由于所有直接传递给程序的邮件都由 smrsh 程序处理，因此需要配置 smrsh 程序以允许 majordomo 的包装程序接收邮件。为此，只需使用以下命令创建适当的符号链接：

```bash
# ln -s /usr/lib/majordomo/wrapper /etc/smrsh/wrapper
```

我还建议你将名称 *majordomo* 添加到 */etc/mail/trusted-users* 文件中，以避免任何多余的 X-Authentication-Warning 标头行。

现在可以测试列表服务器了。运行以下命令：

```bash
# echo "help" | mail majordomo@mail.mybox.com
```

你应该很快在你的邮箱中收到 majordomo 的帮助文档。majordomo 分发包中包含的程序在表 19-5 中进行了总结。

### 表 19-5：随 majordomo 包含的程序

| 程序 | 描述 |
| :--- | :--- |
| **approve** | 批准 majordomo 请求并处理退信消息。 |
| **archive2.pl** | 归档消息以便以后检索。 |
| **bounce** | 自动从列表中删除一个地址（通常是因为重复投递失败）并将该地址订阅到“bounce”列表（如果存在）。 |
| **bounce-remind** | 向“bounce”列表的订阅者发送通知，告知他们已被从他们曾经订阅的列表中移除。 |
| **config-test** | 验证 majordomo 安装并指出当前和潜在问题。 |
| **digest** | 将消息打包成摘要，在达到特定时间限制或消息大小时发送。 |
| **majordomo** | 执行管理分发列表涉及的大多数任务。 |
| **medit** | 锁定一个 majordomo 文件以进行编辑，并在编辑会话完成后解锁文件。 |
| **resend** | 重新传输传出消息到分发列表。 |
| **request-answer** | 回答订阅请求并将其转发给列表所有者。 |
| **wrapper** | 允许程序以 majordomo 用户身份运行并简化在 smrsh 下运行（只需在 */etc/smrsh* 中放置一个链接）。 |

## 摘要

在 Red Hat Linux 中安装邮件服务器是容易的部分；真正需要耐心、决心和一些实验的是配置。一旦你的邮件服务器运行起来，设置邮局协议服务以允许用户将电子邮件下载到自己的工作站就很容易了。

