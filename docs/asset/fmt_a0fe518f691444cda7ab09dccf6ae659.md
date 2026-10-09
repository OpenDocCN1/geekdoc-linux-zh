
FreeBSD 集成的邮件服务器`sendmail(8)`很好地支持垃圾邮件黑名单和灰名单。

# Sendmail

多年来，Unix 类操作系统一直包含了传统的`Sendmail`邮件传输代理（MTA），或称邮件服务器。这个程序庞大、晦涩，并且令新管理员感到非常畏惧。许多经验丰富的系统管理员也发现它庞大、晦涩且令人畏惧。`Sendmail`甚至违反了 Unix 类系统的一条基本准则：它不是由许多良好完成单项任务的小工具组成，而是一个执行许多项任务的巨型程序。在编写`Sendmail`时，这种可以通过文件进行配置而无需重新编译程序的程序想法在当时是革命性的。`Sendmail`的配置看起来像是一个兴奋的哥布林敲在键盘上产生的结果，这一事实并不重要。查看`/etc/mail/sendmail.cf`可以看到一个非常基本的`sendmail(8)`配置文件。

今天，编辑`sendmail.cf`已不再是理想的。`Sendmail`配置已变得简单得多且易于管理，FreeBSD 将`sendmail(8)`集成到系统中，使得电子邮件设置尽可能简单且无痛。

然而，在`Sendmail`管理并不容易的多年里，不喜欢`Sendmail`配置的人开发了更简单、更易于使用且安全性更好的竞争对手。最流行的是`Postfix`(`/usr/ports/mail/postfix`)和`Qmail`(`http://cr.sp.to/qmail`)。两者都是很好的工具。FreeBSD 项目使用`Postfix`处理其海量的邮件列表，其中一些是世界上最大的列表。FreeBSD 允许你无缝地将集成的`Sendmail`安装替换为这些软件包之一，或者你喜欢的其他邮件处理程序。

垃圾邮件、蠕虫和病毒 | Plus Email, If You Insist 473

# mailwrapper(8)

多年来，`Sendmail`是 Unix 类系统唯一可邮件服务器。由于如此，许多附加软件期望找到`/usr/bin/sendmail`并期望它像`Sendmail`一样运行。更糟糕的是，`Sendmail`在被不同名称调用时行为会有不同。`mailq(1)`程序实际上与`sendmail(8)`是同一个文件，但由于它有不同的名称，行为会有不同。由于许多其他程序必须精确执行`Sendmail`，由于这种多名称行为，删除`Sendmail`二进制文件并将其替换为其他内容并不简单。

结果，不熟悉的 Unix 类系统的管理员不知道`/usr/bin/sendmail`到底是什么！如果有人以前安装了多个邮件服务器，你必须花费精力并运气才能识别出所谓的`Sendmail`。

FreeBSD 通过使用独立的`mailwrapper(8)`程序绕过了这一切。这个邮件包装器将请求定向到所需的邮件服务器。你会发现文件`/usr/bin/sendmail`，但那实际上是伪装成`Sendmail`的`mailwrapper(8)`。`/etc/mail/mailer.conf`文件包含了程序列表以及调用的实际程序的路径。例如，默认的`mailer.conf`将所有内容重定向到`sendmail`：

```
sendmail /usr/libexec/sendmail/sendmail

send-mail /usr/libexec/sendmail/sendmail

mailq /usr/libexec/sendmail/sendmail

neweliases /usr/libexec/sendmail/sendmail

hoststat /usr/libexec/sendmail/sendmail

purgestat /usr/libexec/sendmail/sendmail
```

左列中的这六个“程序”每一个都是其他程序可能用于`Sendmail`的名称。`Postfix`和`Qmail`等替代邮件程序实际上具有具有这些名称的独立程序。如果你使用替代邮件程序，你必须编辑`mailer.conf`以给出邮件程序的正确路径。当你使用 Ports Collection 安装替代邮件程序时，端口说明会准确告诉你如何为你的安装更新`mailer.conf`。遵循这些说明以确保你的新 MTA 工作。如果你不使用 Ports Collection 安装替代邮件程序，你需要自己编辑`mailer.conf`。

# 提交与接收

FreeBSD（以及所有 Unix 类系统）以多种方式使用`Sendmail`。FreeBSD 机器接收来自互联网的邮件并将其中继到其他机器或投递给本地用户。其他 FreeBSD 机器则

不接收邮件，仅生成邮件。`Sendmail`处理这些任务的方式略有不同。

`Sendmail`提交守护进程（submit daemon）处理从本地机器发送（或提交）的邮件。在大多数情况下，这些邮件只是被转发到一个邮件服务器。例如，我网络上的所有服务器都会将每日状态邮件转发到我接收的实际邮件服务器。服务器对本地源邮件的信任程度远高于来自互联网的邮件；处理这些消息的`Sendmail`进程使用的配置限制少，执行的检查也更少。此`Sendmail`进程仅监听本地 IP 地址`127.0.0.1`的网络，因此网络上的其他主机无法使用它。

`Sendmail`入站守护进程（inbound daemon）接受网络上其他主机的邮件。这个`Sendmail`进程需要大量的维护和管理。这是入侵者试图攻破的进程，也是垃圾邮件的潜在通道。我们将花费最多的精力来配置入站守护进程。

这两个配置是互斥的。当你的系统上运行一个功能完整的互联网邮件服务器时，你就不需要一个安全性较低的`Sendmail`实例来处理本地邮件，就像大多数人不会离开房子睡在工具房里一样。当激活入站`Sendmail`时，FreeBSD 会自动禁用提交`Sendmail`守护进程及其队列处理器。

启用和入站邮件守护进程在`/etc/rc.conf`中独立运行。要了解所有`Sendmail`配置选项的完整说明，请阅读`rc.sendmail(8)`，但这里是基础配置：

```
sendmail_enable="NO"
sendmail_submit_enable="YES"
sendmail_outbound_enable="YES"
sendmail_msp_queue_enable="YES"
```

简单的`sendmail_enable`开启入站`Sendmail`守护进程。如果你只想从本地主机发送邮件而不接收邮件，请开启`sendmail_submit_enable`。`sendmail_outbound_enable`和`sendmail_msp_queue_enable`设置处理从本地主机传输和重传的邮件。

这里的大部分`Sendmail`配置适用于入站`Sendmail`守护进程。提交`Sendmail`进程需要的配置非常少。当我们谈到对提交`Sendmail`有用的配置时，我们会特别说明。否则，所有内容都是针对入站`Sendmail`实例的。并不是这些功能在提交`Sendmail`上不起作用，而是它们没有意义。例如，你在一个只能从本地主机访问的守护进程上设置基于主机名或 IP 的访问控制或反垃圾邮件保护有什么意义呢？

## Sendmail 日志

`sendmail(8)`将所有事务、错误和重启记录到`/var/log/mailog`。检查它以查看你的邮件活动，特别是在更改任何配置之后。当我处理邮件系统时，我喜欢在单独的终端窗口登录并使用`tail -F`在新条目出现时显示它们：

```
# tail -F /var/log/mailog
```

每当`Sendmail`发送、接收或拒绝邮件时，它都会记录一条消息。`tail -F`实时显示此日志。按`CTRL-C`停止显示并返回提示符。

## 配置 Sendmail

`/etc/mail`目录包含所有人类友好的`Sendmail`配置文件，以及几个对人类不友好的。对于接收入站邮件的服务器的最常见任务，你只需要担心四个文件：`/etc/mail/access`、`/etc/mail/aliases`、`/etc/mail/mailert`和`/etc/relay-domains`。

`access`文件允许为你的邮件服务器设置按主机和按域的访问控制。

`aliases`文件包含本地主机的 MX 重定向映射。当你使用 FreeBSD 系统为安全记录较差的专有系统（如 Microsoft Exchange）提供额外安全层时，`mailertable`特别有用。

`relay-domains`文件列出了你的服务器将作为邮件服务器使用的域名和地址，但列表也可能包含你提供的 MX 服务其他域名。

这些文件（`relay-domains`除外）都有以`.db`结尾的数据库文件。像`/etc/passwd.db`和`/etc/spwd.db`一样，这些数据库文件由文本文件构建，以便程序快速访问数据。当你更改文本文件，必须更新对应的数据库文件，我们将在讨论每个文件时说明。

`Sendmail`将消息附加到该文件中。你可以像下面的内容那样维护用户`mwlcus`电子邮件的永久日志：

```
mwlcus: /var/log/mwlcus-mail, mwlcus
```

## 将邮件转发到程序

你也可以将邮件发送给程序进行自动化处理。只需放置一个管道符号(`|`)，后跟程序的完整路径即可。例如，如果你有一个处理发送到特定地址的入站邮件，可以使用它来重定向邮件：

```
orders: |/usr/local/bin/process-orders.ps
```

## 包含（Inclusions）

最后，你可以在`aliases`文件中包含其他文件。这允许高受信的用户修改她自己的别名。该文件必须是电子邮件地址列表，每行一个。

```
clientlist: include:/usr/home/salesdude/clientlist.txt
```

## mailable 文件

`mailable`文件允许你选择性地覆盖 MX 记录。虽然在网络过去曾连接到如`UUCP`这样的非互联网电子邮件系统时，这一点很重要，但今天，这允许你将 FreeBSD 作为防火墙或某种类型的堡垒主机。在某个实例，我有一个无法直接暴露到互联网的 Microsoft Exchange 系统。通过使用 FreeBSD 机器作为我的公主机并在 FreeBSD 机器上使用`mailable`，我可以在不投资昂贵的电子邮件防火墙的情况下保护 Exchange 系统。

虽然我在`absolutefreebsd.com`并没有 Exchange 系统，但让我们先假设我的主机名为`absolutefreebsd.com`和`exchange.absolutefreebsd.com`。我的 DNS 记录将如下：

| absolutefreebsd.com | MX 10 freebbsd.absolutefreebsd.com |

公众随后会将所有邮件发送到 FreeBSD 机器。在 FreeBSD 机器上，我将使用类似这样的`mailable`条目：

```
.absolutefreebsd.com smtp:[exchange.absolutefreebsd.com]
```

这将使 FreeBSD 机器忽略左侧列域名的 MX 记录，而是将该域的邮件转发到主机`exchange.absolutefreebsd.com`。

## Relay-domains 文件

`Sendmail`简化了为其他域名提供备份 MX 服务的过程。与辅助 DNS 一样，处理备份 MX 服务的最佳方法之一是找到规模相似的实体进行交换。你肯定不想在备份 MX 服务上花费大量时间，特别是对于你自己的以外的组织，使用一个规模相似且技术水平相当的组织有助于确保你的合作伙伴给你带来的问题不会比已有的问题更多。

`/etc/relay-domains`文件列出了你为所有中继邮件的域名和/或 IP 地址。在此处列出每个域名或地址，每行一个。例如，有一个为`absolutefreebsd.com`提供备份 MX 服务的条目：

`absolutefreebsd.com`

这很难，对吧？你还必须在域名的 DNS 记录中列出该服务器，备份 MX 服务才能正常工作。

## 使更改生效

`access`和`mailertable`文件都有对应的数据库(`.db`)文件。就像密码文件一样，提供这些数据库文件是为了让`Sendmail`快速方便地引用其内容。当你编辑其中一个文件时，必须更新数据库文件。`Sendmail`使用`make(1)`管理这些数据库。要更新`access`和`mailertable`文件，请进入`/etc/mail`目录并输入`make maps`：

```
# cd /etc/mail
# make maps
```

`make(1)`比较每个文本文件与数据库文件的日期，如果文本文件较新，它将重新构建数据库。

要重建`aliases`数据库，请运行`newaliases(8)`或`make aliases`：

```
# cd /etc/mail
# make aliases
```

为什么`aliases`数据库有自己特殊的重建命令？`aliases`数据库是`Sendmail`中的第一个数据库，因此为它编写了特殊命令。随着这些数据库的扩散，采用了更通用的方法。

数据库的更改在重建后立即生效。然而，其他更改更具侵入性，需要整个邮件系统。更改`mailertable`就是这些更改之一。虽然你可以通过多种方式重启系统，但建议使用 FreeBSD 启动系统，以便服务器在重启后行为保持一致：

```
# /etc/rc.d/sendmail restart
```

这将使所有更改生效，包括文本文件中的更改。纯主义者可能会注意到，`/etc/rc.d/sendmail`实际上是 shell 脚本`/etc/rc.d/sendmail`的前端。`/etc/rc.d/sendmail`文件早于`rc.d`启动系统，为了历史兼容性保留在那里。

## 虚拟域名（Virtual Domains）

默认情况下，`Sendmail`拒绝所有目的不是本地主机的邮件。如果你的本地主机名与你的域名相同——即如果`absolutefreebsd.com`的邮件服务器是名为`absolutefreebsd.com`的机器，这就能生效。通常并非如此。例如，`absolutefreebsd.com`的邮件服务器是名为`blackhelicopters.org`的机器。在电子邮件系统中，虚拟域名允许服务器接收不同域的邮件。一台 FreeBSD 机器可以处理数千个虚拟域名。

配置虚拟域名有三个步骤。首先，告诉邮件服务器它负责一个域名别名。然后，将该域名用户的邮件重定向到相应的帐户。

## /etc/mail/local-names 文件

`/etc/mail/local-names`指定了`Sendmail`接受的域名和主机。该文件包含主机列表，每行一个，如下：

```
blackhelicopters.org
absolutefreebsd.com
```

第一个条目将左侧的特定地址映射到右侧的特定用户。接两个条目将邮件路由到本地帐户。第四个条目稍微有点趣，因为它会向发送者返回错误。当我必须为某个我知道会发垃圾邮件的人填写在线表单时，我会使用它。我会激活几分钟来获取垃圾邮件，激活帐户，然后屏蔽该地址。最后，最后一条目是针对整个域的通用规则。通过指定没有用户名的`@helicopters.org`，我告诉`Sendmail`适用于所有没有更具体规则的地址。发送到不在此列表上的电子邮件地址的邮件将收到“无此类用户”的错误。

## 用户映射

现在`Sendmail`有了指向真实人物帐户的全获（catch-all），你将不会有大量的垃圾邮件。曾几何，许多管理员为他们的域名使用全获电子邮件地址，并动态创建电子邮件地址。

```
absolutefreebsd.com
absolutefreebsd.com
absolutefreebsd.com
absolutefreebsd.com
```

## 字典攻击（DICTIONARY ATTACKS）

字典攻击是入侵者一个一个尝试可能的用户名。垃圾邮件发送者通过尝试域名下可能的电子邮件地址来执行字典攻击。通过向`aardvard@yourdomain.com`、`aardv@yourdomain.com`、`aaron@yourdomain.com`等一直尝试到字典，垃圾邮件发送者希望一些垃圾邮件能触达真人。`/usr/share/dict/words`中的单词列表包含 235,882 个单词；如果你的邮件服务器接受这些单词中的一个作为你域的有效电子邮件地址并将其重定向到你的个人帐户，你只能删除邮件并希望没有错过重要信息。

> ^3 当然，在现实生活中它们确实是发给同一个人。但你明白我的意思。

为你的其他虚拟域名创建类似的条目。如果你想让`mwlucas@absolutefreebsd.com`和`mwlucas@blackhelicopters.org`到不同的账户，只需在`virtusertable`中创建单独的映射：

| mwlucas@absolutefreebsd.com | michael |

| mwlucas@blackhelicopters.org | mwlucas |

我建议按字母顺序列出你的域名，以便在在一个机器上拥有成千上万个域名时减少混乱。

与其他`Sendmail`配置文件一样，`sendmail(8)`通过数据库文件访问`virtusertable`，你必须保持该文件的最新状态。`virtusertable`的更改在通过进入`/etc/mail`并运行`maps`来更新数据库之前不会生效，就像你处理其他`Sendmail`数据库时一样。

现在只需为该域名发布一个指向你邮件服务器的 MX 记录，你的电子邮件虚拟域名就可以工作了。

## 修改 sendmail.cf

还记得那个可怕的文件`/etc/mail/sendmail.cf`吗？是的，你需要修改它。不要直接编辑`sendmail.cf`，`Sendmail`包含了从其他配置文件构建此配置文件的工具。是的，按今天的标准来说，这很奇异，但在`Sendmail`创建时，它是尖端技术。（我假设这就是年轻人所说的“复古风范”）
