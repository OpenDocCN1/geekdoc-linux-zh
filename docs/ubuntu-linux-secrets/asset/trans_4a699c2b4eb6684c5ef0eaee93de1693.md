

第一行显示 mailx 程序使用单个命令行选项执行，即邮件收件人的电子邮件地址。如果您向同一邮件服务器上的其他用户发送消息，可以省略电子邮件地址中的主机名部分；否则，请务必使用完整的电子邮件地址。

程序启动时，mailx 程序会自动进入撰写模式，提示您输入主题行，然后输入消息正文。要退出撰写模式，请在单独一行输入一个句点。这会生成一个提示，允许您输入抄送收件人的地址。如果没有要添加的地址，只需按 Enter 键即可；mailx 会将您返回到命令行，然后将消息发送给 MTA 进行处理。

要读取邮箱中的邮件消息，只需在命令行单独输入 `mail` 即可：

```
rich@testbox:~$ mail
Mail version 8.1 2/15/2001. Type ? for help.
"/var/mail/rich": 1 message 1 new
>N 1 rich@testbox.localdomain Mon Oct 27 06:46 14/494 Test message
&
Message 1:
From rich@testbox.localdomain Mon Oct 27 06:46:26 2008
X-Original-To: rich
To: rich@testbox.localdomain
Subject: Test message
Date: Mon, 27 Oct 2008 06:46:26 -0400 (EDT)
From: rich@testbox.localdomain (Rich Blum)

This is a test message.

&
```

在您输入 mail 命令后，会显示邮箱中所有消息的摘要。单个消息可以使用 mail 提示符中的简单单字母命令进行显示、复制或删除。

## Dovecot

*Dovecot* 服务器为远程用户提供了访问 Ubuntu 服务器上邮箱的方式。您最可能不希望用户通过 telnet 登录到 Ubuntu 服务器并使用 mailx 程序读取他们的消息。相反，您希望他们使用桌面上的花哨的图形邮件客户端程序，例如 Evolution，远程访问您的 Ubuntu 邮件服务器以读取邮件。

远程访问邮箱需要使用特殊的网络协议。大多数常见的邮件客户端程序使用邮局协议版本 3（POP3）或交互式邮件访问协议（IMAP）来访问远程邮件服务器并处理存储在用户邮箱中的邮件。

为了支持此功能，Ubuntu 邮件服务器软件包包含 Dovecot 服务器软件。连接 Dovecot 服务器后，用户可以读取邮件消息，还可以将它们存储在服务器上 Dovecot 邮箱文件夹下的子文件夹中。此功能允许用户从任何远程客户端连接以查看邮件消息。

以下是使用 POP3 连接检索邮件消息的示例：

```
rich@testbox:~$ telnet localhost 110
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
+OK Dovecot ready.
USER rich
+OK
PASS test
+OK Logged in.
LIST
+OK 1 messages:
1 449
.
RETR 1
+OK 449 octets
Return-Path: <rich@testbox.localdomain>
X-Original-To: rich
Delivered-To: rich@testbox.localdomain
Received: by testbox.localdomain (Postfix, from userid 1000)
id 641A2180E1; Mon, 27 Oct 2008 06:51:26 -0400 (EDT)
To: rich@testbox.localdomain
Subject: Test message
Message-Id: <20081027145126.641A2180E1@testbox.localdomain>
Date: Mon, 27 Oct 2008 06:51:26 -0400 (EDT)
From: rich@testbox.localdomain (Rich Blum)

This is a test message.
.
DELE 1
+OK Marked to be deleted.
QUIT
+OK Logging out, messages deleted.
Connection closed by foreign host.
rich@testbox:~$
```

POP3 连接使用简单的文本命令，允许您与 Dovecot 服务器交互并管理以及读取存储在 Ubuntu 服务器邮箱中的消息。大多数常见的邮件软件包，例如 Ubuntu 工作站发行版中的 Evolution 图形邮件软件包（参见第 9 章，“Evolution”）可以使用 POP3 或 IMAP 连接到在您的 Ubuntu 服务器上运行的 Dovecot 服务器。

## fetchmail

fetchmail 程序是一种略有不同的 MUA 程序。与作为用户 MUA 界面不同，它在幕后运行，允许一个邮件服务器联系另一个远程邮件服务器以从邮箱下载用户邮件。

较小的组织通常负担不起（或出于安全原因，不想）安装专用的 Internet 连接。这意味着他们无法运行专用于从 Internet 接收邮件的 Ubuntu 邮件服务器。作为替代方案，他们可以从远程 ISP 购买电子邮件服务，该服务将他们的公司消息存储在 ISP 服务器上的单个邮箱中。

