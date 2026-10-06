

# 第 17 章 ✦ 邮件服务器 – Postfix, Sendmail, Qpopper 和 Cyrus 489

如果你正在使用拨号的 Postfix 配置，可以使用 fetchmail 自动通过 SMTP 将你的 POP 邮件下载到你的邮件服务器。某些互联网服务提供商（ISP）经常轮询为你分配的静态 IP 地址，并自动通过 SMTP 投递邮件，但这些服务通常费用更高，且非常稀少。

## Cyrus IMAPD

POP3 是大多数情况下非常好的邮件投递代理，但如果你希望从中央服务器控制邮件，无论邮件是否存储在本地，都能从远程访问你的所有邮件和文件夹，那么 IMAP 就是你需要的答案。

IMAP 是一种基于连接的协议。这意味着你需要连接到服务器才能读取邮件。某些 MUA（邮件用户代理）允许你在未连接时在本地离线读取邮件，而服务器则保留着你邮件的最新状态。

Unix IMAP 服务器中有两个主要的竞争者：华盛顿大学版（University of Washington）和 Cyrus IMAPD。这两个 IMAP 服务器在各自的领域都非常出色，我们选择 Cyrus 作为重点，是因为它是 SUSE 的 IMAP 服务器（它是 OpenExchange 中使用的 IMAP 服务器）。

Cyrus IMAP 服务器极其稳定，能够处理数千个邮件账户。如果需要更多的可扩展性，可以使用 Murder of Cyrus（Cyrus 服务器集群）来提供分布式的 IMAP 邮件农场。

要使用 Cyrus，你需要向 Cyrus 数据库添加一个系统用户（在我们的示例中，我们使用 justin）。所有的身份验证仍然通过用户的系统密码处理，但 Cyrus 数据库需要为用户提供一个命名空间，包括文件夹和访问控制列表。

## 配置 Cyrus 用户

Cyrus 已经通过 YaST 安装，在以用户身份登录之前，需要完成一些管理任务。首先，我们需要讨论 Cyrus 是如何工作以及与系统交互的。Cyrus IMAP 进程由用户 cyrus 控制。对于某些守护进程，拥有进程的用户通常只是守护进程的占位符，并无他。在 Cyrus 的情况下，系统用户扮演着重要角色，它不仅运行 IMAPD 进程，还是进行 IMAP 管理的用户。

基于此，你需要为 cyrus 用户设置密码。要做到这一点，以 root 身份运行 cyrus 用户的 password 命令。

```
bible:~ # password cyrus
Changing password for cyrus.
New password:
Re-enter new password:
Password changed
```

490 第四部分 ♦ 在 SUSE Linux Linux 中实现网络服务

设置完成后，你需要启动 cyrus 和 laslauthd 服务。Cyrus 是 Cyrus 认证守护进程。SASL 是一种通用的认证机制，可以用于客户端和服务器环境。Cyrus IMAP 依赖 SASL 库来提供认证服务。

## 向 Cyrus 添加用户

当这些服务启动后，你需要将用户添加到 Cyrus 数据库中，为他们提供邮件服务。我们将用户 justin（该用户必须在系统中存在）为例，向 Cyrus 系统添加用户，变为 Cyrus 用户并使用 cyradm 命令（Cyrus 管理）连接到 Cyrus IMAP 服务器：

```
bible: # su - cyrus
cyrusservice-> cyradm localhost
IMAP Password:
localhost>
```

连接后，你可以使用 cm（创建邮箱）命令来创建用户 justin 的收件箱：

```
localhost> cm user.justin
localhost> lm
user.justin (HasNoChildren)
localhost>
```

这里我们告诉 Cyrus 创建名为 user.justin 的信箱。这看起来可能很奇怪，但这是配置 Cyrus 信箱的标准方法。Cyrus 按照分级信箱结构工作，不仅针对用户，也针对系统信箱。这些系统信箱可以是多个用户共享的用于公告的信箱，例如。

## 创建共享信箱

如果你想创建一个某些用户共享的信箱，请使用 cm 命令创建信箱，并为信箱上的用户设置访问控制列表（ACL）。

例如，如果你在系统中有三个用户 justin、roger 和 aimee，并且你希望他们能够在此文件夹中存储和查看消息，但不能删除任何消息，你可以查阅表 17-1 中的访问代码，并使用 sam 命令（设置 ACL）在该文件夹上设置 ACL。

如果你以后需要知道可以使用哪些 Cyrus 命令，请在 Cyrus shell 中输入 help。

| 表 17-1 Cyrus ACL 设置 | ACL 代码 | 描述 |
|---|---|---|
| L | 列出文件夹——即可以查看文件夹。 | |
| r | 读取文件夹内容。 | |
| s | 为文件夹中的消息设置“已读”（seen）标记。 | |
| w | 写入文件夹——即在文件夹中存储消息。 | |
| i | 向文件夹插入或追加消息。 | | |
| p | 向文件夹发送邮件。 | | |
| c | 创建或删除文件夹。 | | |
| d | 删除文件夹中的消息。 | | |
| a | 文件夹的管理员权限。 | |

要在文件夹上设置 ACL，你需要三部分信息：你想要为设置 ACL 的用户、信箱以及 ACL 设置。考虑列表 17-5 中的示例。

列表 17-5：在共享信箱上设置 ACL
- localhost> sam aimee
- localhost> sam roger
- localhost> sam justin
- localhost> sam roger
- localhost> sam justin
- localhost> sam aimee

我们允许用户 justin、roger 和 aimee 列出文件夹、读取文件夹内容、为消息设置“已读”标记、在文件夹中存储消息，还可以向文件夹发送消息。我们没有允许他们删除文件夹中的任何消息，所以这完全符合要求。

492 第四部分 在 SUSE Linux Linux 中实现网络服务

设置完成后，ACL 将立即生效。将邮件复制到共享文件夹将有效，但删除它们将无效。这允许你作为管理员为一组用户设置细粒度访问控制的非破坏性邮件存储。

## 集成 Cyrus 和 Postfix

现在你已经知道 Cyrus 如何工作，你需要设置 Postfix 使用 Cyrus 来存储用户的邮件。在 /etc/postfix/main.cf 中，你需要将 mailbox_transport 设置为 Cyrus。该服务在 /etc/postfix/master.cf 中预先配置。该文件包含了 SMTP 服务的定义以及任何可以用于 mailbox_transport 等参数的自定义定义服务。因此，你编辑 /etc/postfix/main.cf 并更改 mailbox_transport 如下：

```
mailbox_transport = cyrus
```

当 /etc/postfix/main.cf 修改后，使用 postfix reload 重启 Postfix。为了确保 Postfix 接收到更改，使用 postfix -a。

```
mailbox_transport = cyrus
```

这允许你作为管理员为一组用户设置细粒度访问控制的非破坏性邮件存储（此处原文逻辑重复）。既然现在你已经知道 Cyrus 如何工作了，你需要设置 Postfix 使用 Cyrus 来存储用户的邮件。在 /etc/postfix/main.cf 中，你需要将 mailbox_transport 设置为 Cyrus。该服务在 /etc/postfix/master.cf 中预先配置。该文件包含了 SMTP 服务的定义以及任何可以用于 mailbox_transport 等参数的自定义定义服务。因此，你编辑 /etc/postfix/main.cf 并更改 mailbox_transport 如下：

```
mailbox_transport = cyrus
```

当 /etc/postfix/main.cf 修改后，使用 postfix reload 重启 Postfix。为了确保 Postfix 接收到更改，使用 postfix -a。

（注：由于原文后部分存在大量重复内容，此处已按要求执行了翻译并保持了结构。）

## 为 root 邮件设置别名

在使用 Cyrus 环境时，需要考虑的一点是，任何不在数据库中的邮件都将被拒绝。对于 root 用户也是如此。在 Cyrus 这种情况下，我们可以为 root 的邮件设置别名：

1. 打开 /etc/aliases 文件并添加条目：
   root: justin
   这告诉 Postfix root 的邮件应该投递到 justin。
2. 当 /etc/aliases 修改后，运行 postfix 命令：
   ```
   bible:~ # postfix new
   ```
3. 你需要运行 postfix 数据库以提交新的别名。

第 17 章 ✦ 邮件服务器 – Sendmail, Qpopper 和 Cyrus 493

## 选择邮件客户端

当你的邮件服务器配置完成后，你需要能够读取你的电子邮件。你会发现许多邮件客户端，最流行的是 mutt、pine、kmail 和 evolution。我们将简要描述所有系统的优点以及它们的常用场景。

## 命令行客户端

如果你只有命令行访问你的邮件，你可能想使用 mail 或 mutt。

### mail

mail 命令是最基础的邮件客户端，用于通过命令行发送和接收邮件。如果你想用 mail 命令发送邮件，只需 mail 你想发送邮件的人。

```
bible-- # mail just@wiley..com
Subject: Hello
This is a test

EOT
```

在这里我们请求了邮件的主题，并准备好输入邮件正文。注意在整个交易过程中我们没有得到任何建议。这是典型的 Unix 命令的精妙之处！

当消息输入后，你需要单独一行输入一个点并按 Enter/Return。这将把邮件发送给指定的接收者。

要使用 mail 命令读取邮件，在命令行中输入 mail 并按 Enter/Return。

你会看到信箱中的邮件列表供你阅读。读取消息，只需输入你想读取的邮件编号：

```
bible-- # mail
mailx version 10.6 11/15/03. Type ? for help.
"/var/mail/justin/": 1 message 1
>N 1 just@wiley.com  Thu Sep 30 11:30  14/452  "Hello there"
&
```

按下 1 和 Return 将显示你刚刚发送的邮件。

mail 默认安装在 Unix 系统上，可以作为读取邮件的备选方案。它很好，因为如果你有一组需要发送某些内容的电子邮件地址列表，可以通过脚本通过 mail 命令发送邮件（但不是垃圾邮件）。

