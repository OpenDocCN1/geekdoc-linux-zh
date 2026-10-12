
## sendmail 信封与头部地址

Ben.” 当 Gonzo 和 Whizzer 的 Alphonse 同事收到这些信封时，他们会复印备忘录并发送给 Mary、Bill、Ted 和 Ben，而不去检查备忘录本身的地址。对于 Gonzo 和 Whizzer 的邮件管理员来说，备忘录本身甚至可能是写给教皇的。他们只关心信封上的地址。

SMTP 客户端和服务器的工作方式与此类似。假设 joe@gonzo.gov 向他的同事 betty@zippy.gov 和 fred@whizzer.com 发送邮件。信件头部中的收件人列表可能看起来像这样：

To: betty@zippy.gov, fred@whizzer.com

gonzo.gov 的 SMTP 客户端连接到 whizzer.com 的邮件传输代理以投递 Fred 的副本。当它准备列出收件人（信封地址）时，它应该说些什么？如果它像前述 To: 行（头部地址）中列出那样给出两个收件人，Betty 将会收到两封信，因为 whizzer.com 的邮件传输代理会将副本转发给 zippy.gov。如果 gonzo.gov 的 SMTP 客户端连接到 zippy.gov 并列出 Betty 和 Fred 作为收件人，也会出现同样的问题。zippy.gov 的邮件传输代理会将 Fred 的信的第二份副本转发。

解决方案是 Alphonse 和其他邮件管理员使用的那种。gonzo.gov 的 SMTP 客户端将信件放入一个信封中，该信封只包含每个主机上收件人的名字。完整的收件人列表仍然在信件头部中，但它们位于信封内部，而 gonzo.gov 和 whizzer.com 的 SMTP 服务器不查看它们。在这个例子中，给 whizzer.com 邮件传输代理的信封只列出了 fred，而给 zippy.gov 的信封只列出了 betty。

别名（Aliases）说明了头部地址和信封地址不同的另一个原因。假设你向别名 homeboys 发送邮件，其中包含 alphonse、joe 和 george 的名字。在你的信中，你写道 To: homeboys。然而，sendmail 展开别名并构建一个包含所有收件人的信封。取决于这些名字是否也是别名（也许在其他主机上），原始消息可能会被放入多达四个不同的信封并投递到四个不同的主机。在每种情况下，信封只包含收件人的名字，但原始消息包含别名 homeboys（扩展为 homeboys@your.host.domain 以便重新归档生效）。

最后一个例子展示了信封地址与头部地址可能不同的另一种方式。使用 sendmail 时，你可以在命令行上指定收件人。假设你有一个名为 letter 的文件，看起来像这样：

```
$ cat letter
To: null recipient <>
Subject: header and envelope addresses
```

测试

你使用以下命令发送这封信，用你自己的登录名替换 *yourLogin*：

$ /usr/sbin/sendmail *yourLogin* < letter

因为你的地址在信封上，即使你的登录名没有出现在信件头部，你也会收到这封信。除非被告知其他情况（使用 -t 标志），*sendmail* 根据你在命令行上指定的收件人构建信封地址，头部地址和信封地址之间不一定存在对应关系。

# sendmail 的任务

为了更好地理解如何设置 *sendmail*，你需要了解它执行什么任务以及这些任务如何融入 MUA、MTA、邮件路由、最终投递代理以及 SMTP 客户端和服务器的体系结构中。*sendmail* 可以充当邮件路由、SMTP 客户端和 SMTP 服务器。但是，它不进行邮件的最终投递。

## sendmail 作为邮件路由

*sendmail* 主要是一个邮件路由，意味着它接收信件，检查收件人地址，并决定发送的最佳方式。*sendmail* 如何执行此任务？

*sendmail* 自行确定它需要的一些信息，例如当前时间和它运行所在主机的名称，但它的大多数“大脑”由你（邮件管理员）通过配置文件 *sendmail.cf* 提供（将在后面详细描述）。这个略显晦涩的文件告诉 *sendmail* 你希望如何处理各种类型的邮件。*sendmail.cf* 极其灵活且强大，乍一看似乎不可理解。然而，V8 *sendmail* 的一个优点是其模块化配置文件构建块。大多数站点可以轻松地从这些模块构建它们的配置文件，并且包含了许多示例。从头编写配置文件是一项艰巨的任务，所以你应该尽量避免！

## sendmail 作为 MTA：客户端（发送方）和服务器（接收方）

SMTP

如前所述，*sendmail* 可以充当 MTA，因为它理解 SMTP 协议（V8.8 *sendmail* 也理解 ESMTP）。SMTP 是一个面向连接的协议，因此客户端和服务器（也称为发送方和接收方）始终存在。SMTP 客户端将信件投递到 SMTP 服务器，该服务器在其计算机的 SMTP 端口上持续监听。*sendmail* 可以是 SMTP 客户端或 SMTP 服务器。当被 MUA 运行时，它成为 SMTP 客户端并与 SMTP 服务器（不一定是另一个 *sendmail* 程序）进行客户端端 SMTP 通信。当你的 *sendmail* 以守护进程模式启动时，它作为服务器运行。在这种服务器模式下，它执行两个主要任务。第一个是持续监听 SMTP 端口上的传入邮件。第二个是管理尚未投递的邮件队列，并定期重试投递，直到消息最终成功投递或超过重试限制。

# sendmail 不是最终投递代理

sendmail 不做的一件事是最终投递。sendmail 的作者明智地将此任务留给其他程序。sendmail 是一个庞大且复杂的程序，以超级用户权限运行。这几乎是安全问题的保证配方，在 sendmail 的历史中确实发生过不少。额外的最终邮件投递复杂性是 sendmail 最不需要的。在 Red Hat 系统的默认情况下，procmail 被用作本地投递代理。

# sendmail 的辅助文件

sendmail 依赖许多辅助文件来完成其工作。最重要的是别名文件和配置文件 sendmail.cf。统计文件 sendmail.st 可以创建或不创建，取决于你是否想要关于发送到你的主机和从你的主机接收的消息数量的统计信息。这还包括电子邮件流量的总千字节量。SMTP 帮助文件 sendmail.hf 如果你打算将 sendmail 作为 SMTP 服务器运行（大多数站点都这样），应该安装。

你的主机上可能需要的另一个文件是 sendmail.cw，它包含你的邮件服务器的所有替代主机名。例如，如果你的主要邮件服务器是 mail.whizzer.com，它被指定为 whizzer.com 的 MX，你需要在这个文件中放入 whizzer.com 以告诉 sendmail 在 mail.whizzer.com 上投递 whizzer.com 的电子邮件。

这就是关于 sendmail.st、sendmail.hf 和 sendmail.cw 的所有内容。其他辅助文件在《Sendmail 安装和操作指南》（简称 SIOG）中有涵盖。SIOG 通常位于 /usr/share/doc/sendmail/doc/op/ops.ps，它来自 sendmail-doc RPM 或 sendmail 的源代码分发版。另一方面，别名和 sendmail.cf 文件重要到足以在它们自己的章节中涵盖。

# 别名文件

sendmail 始终检查收件人地址的别名，这些别名是收件人的替代名称。例如，每个互联网站点都必须有一个有效的地址 postmaster，邮件问题可以报告给这个人。大多数站点没有实际具有该名称的账户，而是将 postmaster 的邮件转给负责电子邮件

管理的人。例如，在虚构站点 **gonzo.gov**，用户 **joe** 和 **betty** 共同负责电子邮件管理，别名文件中有以下条目：

```
postmaster: joe, betty
```

这一行告诉 **sendmail** 给 **postmaster** 的邮件应该转而投递到登录名 **joe** 和 **betty**。事实上，这些名字也可以是别名：

```
postmaster: firstshiftoffops, secondshiftoffops, thirdshiftoffops
firstshiftoffops: joe, betty
secondshiftoffops: lou, emma
thirdshiftoffops: ben, mark, clara
```

在所有这些例子中，别名名称在冒号的左侧，这些名称的别名在右侧。**sendmail** 反复评估别名，直到它们解析为真实用户或远程地址。要解析前述例子中的别名 **postmaster**，**sendmail** 首先将其扩展为收件人列表——**firstshiftoffops**、**secondshiftoffops** 和 **thirdshiftoffops**——然后将这些别名中的每一个扩展为最终列表——**joe**、**betty**、**lou**、**emma**、**ben**、**mark** 和 **clara**。

虽然别名的右侧可以指代远程主机，但左侧不能。别名 **joe**: **joewhizzcr.com** 是合法的，但 **goeongono.gov**: **joewhizzcr.com** 不是。每次修改别名文件时，都必须运行命令 **newaliases**。否则，**sendmail** 将不知道这些更改。

## 从文件读取别名：`:include:` 指令

别名可用于创建邮件列表。（在前一节所示的例子中，别名 **postmaster** 实际上是本地邮件管理员的邮件列表。）对于大型或经常变动的列表，你可以使用 **:include:** 别名形式来指导 **sendmail** 从文件中读取列表成员。假设别名文件包含这一行：

```
homeboys: :include:/home/alphonse/homeboys.aliases
```

还假设文件 **/home/alphonse/homeboys.aliases** 包含这些：

```
alphonse
joe
betty
george
```

其效果等同于这个别名：

```
homeboys: alphonse, joe, betty, george
```

此指令对于自动生成的、经常变动的或由邮件管理员以外的用户管理的邮件列表非常有用。如果你发现某个用户要求频繁更改邮件别名，你可能希望将其置于她的控制之下。你必须小心；最新版本的 **sendmail** 对文件权限非常挑剔
