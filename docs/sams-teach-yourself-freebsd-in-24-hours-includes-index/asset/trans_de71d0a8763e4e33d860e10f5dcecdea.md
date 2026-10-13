
## 练习

- 1. Apache 是无限可扩展的。浏览一下可用的各种模块（/usr/ports/www 中所有名称以 mod_ 开头的 ports），看看哪些可能对你有用。mod_perl 让你可以将 Perl 解释器嵌入到 Apache 中，加快经常使用的 Perl 脚本的执行速度；mod_frontpage 让你可以支持想要使用 Microsoft FrontPage 来创建网站的用户；mod_dav 则让你可以创建一个 WebDAV 服务器（如 Apple 的 iCal 软件所使用）。你可以安装任意多个这些模块。不断尝试，直到拥有符合你需求的模块配置。
- 2. 启用服务器端包含，使用 Apache 网站上找到的文档。学习如何创建一个简单的 if/then 语句，根据某些条件的结果（例如，访客使用的浏览器）输出不同的 HTML 内容。
- 3. 学习如何使用 .htaccess 文件在整个系统的不同位置控制配置选项。这与在 httpd.conf 中全局进行更改相比有什么好处？
- 4. 同样适用于 /usr/local/etc/apache/mime.types。与在 httpd.conf 中指定相比，在此文件中指定新的文件类型有什么好处？

![](img/ba0161b65b37e94cffc801ecbacaba5e_387_0.png)

## 第 23 小时

### 基础电子邮件服务

任何在互联网上的多用户操作系统都必须让其用户能够向其他系统的用户发送电子邮件。这是最早的互联网用途之一，而且最近它无疑已成为任何计算机用户生活不可或缺的一部分。然而，以其当前形式，电子邮件与过去相比有些不同。

FreeBSD 开箱即用时已配置为为系统的本地用户提供电子邮件服务；如果你对默认配置做某些更改，它也可以充当中继，让拨号机器上的人使用你的服务器将消息传递到其目标服务器。然而，这也意味着大规模邮件发送者（“垃圾邮件发送者”）也可以在未经你许可的情况下将你的服务器用作广播站。

在本小时的课程中，我们将介绍 Sendmail，这款 venerable *邮件传输代理 (MTA)*，它仍然传输着世界上大部分的电子邮件，并且是 FreeBSD 的一部分。你将学习

- 使用构成 Sendmail 配置的各种文件
- 自定义主配置文件并重新生成 Sendmail 的运行时配置文件
- 向系统添加别名
- 启动和停止 Sendmail
- 查看消息队列并查看正在等待投递的消息
- 通过控制邮件中继来对抗垃圾邮件发送者

### SMTP 与 Sendmail

*简单邮件传输协议 (SMTP)* 负责将电子邮件从一个服务器传输到下一个服务器。顾名思义，它是一个简单的协议，仅用于建立发件人和收件人的身份，并传输消息的内容。发件人和收件人各自由电子邮件地址指定，电子邮件地址由用户名和主机名组成，以 at 符号 @ 分隔；如果接收消息的 SMTP 服务器具有与电子邮件地址中相同的主机名，它就知道消息 intended 到达那里的收件人。如果不是，它就知道必须将消息 *中继* 到另一台主机。

在最简单的情况下，这就是电子邮件从一个用户到另一个用户的方式；在过去，每个人都在服务器上拥有 shell 账户时，一个服务器上的用户只需在本地机器上打开一个邮件程序（*邮件用户代理*，例如 Pine、Elm 或 Mutt），写一封消息并告诉程序发送即可给另一台服务器上的用户发送电子邮件。然后 MUA 会在端口 25 上打开到远程用户邮件服务器（通常是该用户拥有 shell 账户的同一台机器）的 SMTP 连接。远程服务器会读取电子邮件地址，意识到消息 intended 给本地用户，然后将消息转储到用户的邮箱中。然后用户可以打开自己的 MUA 并阅读消息。

如今，通常会复杂一些，如图 23.1 所示。完整的电子邮件投递路径通常在到达目的地之前需要经过两个或多个网络跳数。

今天最常见的情况是，电子邮件的发送者并不是邮件服务器机器上的本地 shell 用户，而是一个通过 *互联网服务提供商 (ISP)* 通讯的拨号用户。该用户的 MUA 可能是 Microsoft Outlook、Apple Mail、Eudora 或其任何流行的同类产品。当 MUA 发送消息时，它会打开到用户 ISP 提供的 SMTP 服务器的 SMTP 连接——*不是*直接连接到远程用户的邮件服务器。

### 图 23.1

电子邮件消息从一个用户到另一个用户的路径图，显示了 MUAs 和 MTAs 的作用。

![](img/ba0161b65b37e94cffc801ecbacaba5e_389_0.png)

MUAs 不直接向收件人的 SMTP 服务器发送消息，因为 MUAs 的邮件发送能力非常有限。它们没有诸如消息队列或保持重试连接的能力等功能。大多数 MUAs 通过真正的 SMTP 服务器运行，后者能更高效地处理所有邮件发送任务。

发送 MTA，即 ISP 的 SMTP 服务器，接收消息并将其放入消息队列。意识到收件人不是其作为邮件服务器的网络上的用户，它会立即尝试将消息传输到收件人的 SMTP 服务器。如果 MTA 无法立即发送，消息将保留在消息队列中长达五天，不断重试，然后 MTA 才删除它。成功传输后，接收 MTA 会将消息附加到收件人用户的邮箱——如果是 FreeBSD 机器，则为 /var/mail/<user>。

今天的电子邮件收件人通常也不是接收 MTA 上的本地 shell 用户。他们也是拨号用户，必须通过 POP3（Post Office Protocol version 3）或 IMAP（Internet Message Access Protocol）获取邮件，这两种方法都是将消息下载到我们之前讨论过的本地 MUA 的方法。

![](img/ba0161b65b37e94cffc801ecbacaba5e_390_0.png)

你完全可以仅从命令行执行一个完全有效的 SMTP 事务；SMTP 是一个纯文本交互协议，使用简单的四字母、类似英语的命令，你甚至无需访问 MTA 或电子邮件程序即可向某人发送简单消息：

```
# telnet destination.com 25
Trying 64.41.134.166...
Connected to destination.com.
Escape character is '^]'.
220 destination.com ESMTP Sendmail 8.11.1/8.11.1; Wed, 16 May 2001 22:55:37
- >0000 (PDT)
HELO stripes.sender.com
250 destination.com Hello w012.z064002043.sjc-ca.dsl.cnc.net
[64.2.43.12],
- pleased to meet you
MAIL FROM: frank@sender.com
250 2.1.0 frank@sender.com... Sender ok
RCPT TO: bob@destination.com
250 2.1.5 bob@destination.com... Recipient ok
DATA
354 Enter mail, end with "." on a line by itself
From: frank@sender.com
To: bob@destination.com
Subject: Testing, 123...

This is a test message.
.
250 2.0.0 f4H5uCu35501 Message accepted for delivery
QUIT
221 2.0.0 destination.com closing connection
Connection closed by foreign host.
```

这当然不太用户友好。如果没有 MTAs 和 MUAs，我们就是这样处理所有电子邮件的——而且不会那么有用或有趣。

### 基础 Sendmail 配置

FreeBSD 自带 Sendmail，已安装并开箱即用配置为满足基本的电子邮件需求。要启用 Sendmail（使其在启动时启动），只需在 /etc/rc.conf 中添加以下行：

```
sendmail_enable="YES"
```

系统启动并运行后，只要你正确设置了几件事，你就可以向互联网上的任何人发送消息，他们也可以向你发送消息。大多数情况下，这些不是 Sendmail 本身的配置项，而是系统的一般配置——Sendmail 依赖于系统在无缝运行前具备一些保证。

### Sendmail 文件布局

系统中与 Sendmail 相关的有三个位置：

- `/etc/mail`—Sendmail 配置文件
- `/var/mail`—用户邮箱
- `/var/spool/mqueue`—消息队列文件

Sendmail 本身位于 `/usr/sbin/sendmail`，其日志文件写入 `/var/log/maillog`（该日志会自动按日轮换和归档，因此旧日志文件可作为 maillog.0.gz、maillog.1.gz 等使用）。

`/var/mail` 中的邮箱文件（邮件 spool）是纯文本文件——每个文件以其所有者的用户名命名，权限设置为 600（仅所有者可读可写）。新消息会被附加到收件人邮件 spool 文件的末尾。还有临时 POP 锁文件，其长度为零，名称形式为 `.username.pop`。在 POP3 连接打开时，它们会接收对应邮件 spool 文件的内容，任何未传输的残余随后会被复制回邮箱。

### 使用 Sendmail 配置文件

Sendmail 通过多个不同的配置文件控制——全部位于 `/etc/mail` 中。每个文件都有其自己的用途，允许你控制特定的一组 Sendmail 功能。

### 进行通用配置更改

主要的 Sendmail 配置文件——启动时读取的包含所有操作选项和过滤规则的文件——是 `/etc/mail/sendmail.cf`。然而，与几乎所有其他程序的几乎所有其他配置文件不同，你并不打算编辑此文件来更改 Sendmail 的行为。相反，你应该在 Master Config（`.mc`）文件中以更高的“宏”级别进行更改，然后从中编译一个 `sendmail.cf` 文件。除非绝对必要，否则最好不要修改 sendmail.cf。

你的实际配置更改应在此处进行 `/etc/mail/freebsd.mc`，即主配置文件。把它想成是配置文件的配置文件。它包含一个列表

![](img/ba0161b65b37e94cffc801ecbacaba5e_391_0.png)
