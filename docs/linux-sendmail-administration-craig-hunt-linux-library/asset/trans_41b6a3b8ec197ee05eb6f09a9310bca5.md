

# 第 6 章 使用 Sendmail 数据库

Sendmail 可用的数据库比你用过的还要多。有些数据库对 Linux 站点来说很小或毫无价值——bitdomain 数据库为一个没有任何 Linux 使用的网络进行地址转换，而 uuucdomain 数据库则转换 UUCP “bang”地址（旧的 host名-用户名 电子邮件地址），且几乎没人人使用它们。其他可用的数据库具有重叠的功能，这可能意味着你根本不需要同时使用它们。通过 RPM 交付的 redhat.mc 配置包含的上述定义和特征不足列表的一半，而它可能包含了更多你真正需要的数据库功能。为了帮助你评估需要哪些数据库，我们将更详细地检查所有这些数据库。

## Cr, Cw 和 Ct 文件

我们所涵盖的前三个数据库在严格意义上并不是数据库。它们是用于加载 `sendmail.cf` 变量的磁盘文件。“cr”文件和“cw”文件在配置 Sendmail 时起着重要作用，但由于网络安全环境的变化，“ct”文件已不再具有其实用作用。

加载 `t` 类的文件的文件通常被称为“ct”文件，因为该文件的传统名称是 /etc/sendmail.ct。在 Sendmail 8.11 中，该文件的默认名称是 /etc/mail/trusted-users，但该文件的功能保持不变。它用于将用户名添加到信任以其他用户名义发送邮件的用户列表中。默认情况下，ct 类包含用户名 daemon、root 和 uucp。

你永远不需要 /etc/mail/trusted-users 文件，这里有几个原因解释了你为什么不会使用它。首先，让人们以他名义发送邮件是一个坏主意。通常情况下，你不希望扩大信任用户列表。其次，如果你决定绝对必须将用户名添加到信任用户列表中，例如你可能想将用户名“mail”添加到信任用户列表中。你可以编辑宏配置文件来添加 `FEATURE(use_ct_file)` 命令，重建 `sendmail.cf` 文件，并创建一个包含单个单词 mail 的 `trusted-users` 文件。但你为什么要这么做呢？你可以轻松地编辑宏配置文件来添加 `define_CONTRUSTED_USERS, 'mail!'` 命令，重建 `sendmail.cf` 文件即可完成。这不仅比第二种方法稍微简单，而且更安全，因为少创建了一个文件，因此设置错误权限的文件也更少。

> 警告 尽管有此示例，但不建议使用 CONTRUSTED_USERS 或 use_ct_file，因为你不应该向信任用户列表添加任何用户。在垃圾邮件发送者和安全破解横行的时代，信任用户是一个坏主意。

与从未使用“ct”文件不同，“cr”文件是被使用的。“cr”文件实际上名为 relay-domains 文件。Sendmail 始终使用在 relay-domains 文件中找到的数据。该文件的目的和结构是下一个主题。

## relay-domains 文件

当邮件到达 Sendmail 服务器时，它会被接受、拒绝或中继。如果邮件是发送给服务器本身的（通过服务器接受的任何名称），则邮件将被接收用于本地投递，这意味着邮件被放在本地用户的信箱中，或者作为 Sendmail 数据库之一进行路由。如果邮件不是发送给服务器本身的，则会被拒绝或中继。邮件通过重新发送到投递地址来进行中继。在 Sendmail 8.9 之前，所有由 Sendmail 服务器接收的另一个主机邮件都会被中继。现在，除非你明确告诉 Sendmail 进行中继，否则任何邮件都不会中继。对于许多使用 Sendmail 服务器为他们的 PC 中继出站邮件的系统管理员来说，这是一个巨大的头疼问题。但这种变化是必要的。垃圾邮件发送者利用 Sendmail 的中继功能来隐藏垃圾邮件的来源。现在所有管理员都必须为垃圾邮件付出代价，即创建式中继配置所需的额外工作。

![](img/9639113aa446fb8976cb3d377f7aafdd_168_0.png)

显式启用中继的一种方法是在 /etc/mail/relay-domains 文件中列出允许中继邮件的主机名。Sendmail 将该文件中编写的任何内容复制到类变量 R。类 R 中列出的任何主机都允许中继邮件。列表 6.2 显示了一个简单的 relay-domains 文件的内容。

### 列表 6.2 使用 relay-domains 文件

```
[root]# cat /etc/mail/relay-domains
ibis.foobirds.org
[root]# ps -ax | grep sendmail
542 ?  S  0:00 sendmail: accepting connections
[root]# kill -HUP 542
[root]# sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
ter <ruleset> <address>
=$R
ibis.foobirds.org
> ^D
```

SIGHUP 信号被传递给 Sendmail 进程，以确保它将 relay-domains 中的主机名到达类 R。列表 6.2 中的测试显示类 R 已被完全修改。

注意 relay-domains 和类 R 中列出的主机是中继邮件的来源；它们不是目的地。下一节将介绍的类 w包含目标命令主机名。类 R 包含命令主机名。

列表 6.2 仅向类 R 添加了一个域名。在 Sendmail 配置内部使用 `RELAY_DOMAIN` 宏可以向类 R 添加有限数量的域名。例如，在 Sendmail 配置中放置以下命令的效果与列表 6.2 中的 relay-domains 文件相同：

```
RELAY_DOMAIN('ibis.foobirds.org')
```

然而使用 relay-domains 文件比使用 RELAY_DOMAIN 宏更简单。RELAY_DOMAIN 需要修改 Sendmail 配置并运行 m4 来构建 `sendmail.cf` 文件。使用 relay-domains 时，Sendmail 默认检查 /etc/mail/relay-domains 并将其找到的主机添加到类 R。只有当你想要更改 relay-domains 的默认文件名时，才需要在配置中放置命令。有两种方法可以：

```
define(`CONF_FILE`, `/etc/mail/relay-domains`)
```
这意味着你没有显式设置任何值。
```
define(`CONF_FILE`, `/etc/for`)
```

有三个与设置 relay 值相关的命令：RELAY_DOMAIN、RELAY_DOMAIN_FILE 和 CONF_FILE。但你不需要使用它们任何一个。只需创建一个 /etc/mail/relay-domains 文件，并将服务器应该中继的主机放入其中。另一方面，下一节介绍的“cw”文件与“cr”文件同样重要。

## local-hostnames 文件

在第 5 章中，通用 Linux 和 Red Hat 配置都包含 `FEATURE(use_cw_file)` 命令。该功能读取 /etc/mail/local-hostnames 将主机名添加到类 w。默认情况下，类 w 包含 localhost、特殊地址 127.0.1 以及完整域名和未限定主机名。你放在 local-hostnames 中的任何内容都会添加到这些默认值。

系统检查 w 以决定是否接受本地投递的传入邮件。Sendmail 服务器只接受发送给服务器的本地投递邮件。然而许多系统使用 Sendmail 作为信箱来收集和处理。如果服务器收集和处理的邮件字面上指向另一个系统，则需要将该系统的名称添加到类 w，另一个系统的主机会被 Sendmail 视为别名。

假设 robin.foobirds.org 是一台使用服务器 wren.foobirds.org 作为信箱收集和处理的 PC。DNS 服务器中放置了 MX 记录，将 robin 的邮件指向 wlen。列表 6.3 显示了当 bear.mammals.foobirds.org 向 wlen 发送邮件时发生的情况。

### 列表 6.3 类 w 测试失败

```
$ craig@ibis sendmail -v t
To: jill@robin.foobirds.org
From: Logan
Subject: Class w test
^
connect... Connecting to wren.foobirds.org.
via esmtp...
220 wren.foobirds.org SMTP Sendmail 8.11.0/8.11.0;
Thu, 21 Sep 2000 16:27:59 -0400
>>> EHLO bear.mammals.org
250-wren.foobirds.org Hello root@bear.mammals.org [172.16.12.1],
pleased to meet you
>>> MAIL From:<logan@bear.mammals.org> SIZE=62
250 2.1.0 <jill@robin.mammals.org>... Sender ok
>>> RCPT To:<jill@robin.foobirds.org>
550 5.7.1 <jill@robin.foobirds.org>... Relaying denied
```

