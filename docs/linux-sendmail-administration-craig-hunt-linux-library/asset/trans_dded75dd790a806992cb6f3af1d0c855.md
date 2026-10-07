

# 第 6 章 使用 Sendmail 数据库

```
>>>
250.0.0 Reset state
/home/logan/dead.letter... Saved message in /home/logan/dead.letter
Closing connection to wren.foobirds.org.
```

QUIT

```
221 2.0.0 wren.foobirds.org closing connection
```

除了为了节省篇幅删除了 EHLO 响应中的几行外，列表 6.3 中的测试结果看起来与之前完全一致。调用 Sendmail 时使用了 -v 和 -t 参数，以便我能从键盘输入测试内容并接收详细的响应。前四行（**粗体显示**）是我输入的。其余部分是远程邮件服务器的响应。如 `To` 行所示，邮件的收件人地址是 jill1.foobirds.org。Sendmail 显示的第一行说它正在通过 smtp 邮件收发程序连接到 wren.foobirds.org。发往 robin.foobirds.org 的邮件被发送到 wren.foobirds.org，这意味着 wren 必须是 robin 的首选邮件交换服务器。太棒了，除了这显然告诉了 wren 的管理员！***粗体斜体显示的*** 550 响应行是一条错误信息，表示 wren 将不会从 robin 转发邮件到 robin。嗯，我们并不想转发邮件，但确实想接收 robin 的邮件，而它显然不会这样做。问题出在，robin.foobirds.org 这个名称不是 wren.foobirds.org 的有效别名，因此 wren 不接受来自 robin 的邮件。

要修正这个问题，必须将 robin 添加到类 w 中。这可以通过两种方法实现。一种方法是使用 `LOCAL_DOMAIN` 宏命令直接在 Sendmail 配置中为类 w 添加该值，如本例所示：

```
LOCAL_DOMAIN(`robin.foobirds.org`)
```

如果只需要添加几个主机，这种方法非常有效。它简单直观，且所有内容都包含在 Sendmail 配置文件中。

添加别名的另一种方法是将它们放入 `local-host-names` 文件。当有多个名称需要添加或名称列表随时间变化时，将主机放在 `local-host-names` 文件中更好。在 `generic-linux.mc` 和 `redhat.mc` 配置的情况下，使用 `local-host-names` 文件更简单，因为配置中已经包含了 `FEATURE(use_cw_file)` 命令。无需添加 `LOCAL_DOMAIN` 命令或重新构建 `sendmail.cf` 文件。列表 6.4 显示了 `local-host-names` 文件中 robin 的两个条目，并显示了向 Sendmail 发送 SIGHUP 信号以确保 Sendmail 加载新值。

# 列表 6.4 local-host-names 文件中的条目

```
[root]# cat local-host-names
# local-host-names - include all aliases for your machine here.
#
robin.foobirds.org
robin
[root]# ps -ax | grep sendmail
542 ? S 0:00 sendmail: accepting connections
[root]# kill -HUP 542
[root]# sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
=$w
robin.foobirds.org
wren.foobirds.org
[172.16.12.3]
wren
localhost
robin
>D
```

wren 将接受来自 robin 的邮件，尽管它不一定知道如何处理。如果 Jill 将从 wren 上的信箱下载她的邮件，你必须为 Jill 创建一个有效的用户账户，以便允许 Sendmail 创建必要的池化目录来存放她的邮件，并允许她通过 POP 或 IMAP 下载邮件。如果 Jill 的邮件应该转发到另一个系统，则需要给 Sendmail 提供邮件路由指令。显然，将主机添加到类 w 是至关重要的，但这仅仅是第一步。可能的下一步是配置别名数据库。

# 别名数据库 (aliases Database)

一旦 Sendmail 服务器接收了用于本地投递的邮件，就必须决定如何投递邮件。它必须确定收件人地址中标识的用户是具有本地信箱的本地用户，还是邮件必须转发给真实收件人的用户别名。用于进行此判断的主要数据库是别名数据库。

![](img/9639113aa446fb8976cb3d377f7aafdd_172_0.png)

Sendmail 别名执行着重要功能，是创建邮件服务器必不可少的部分。邮件别名具有以下功能：

- 指定单个用户的昵名。昵名可用于将发往特殊名称（如 postmaster 或 root）的邮件重定向到执行工作的真实用户。别名可以简化域名标准电子邮件地址结构的创建，因为邮件别名的结构比登录名更灵活。

- 将邮件转发到其他主机。Sendmail 别名会自动将邮件转发到收件人地址中包含的主机地址。

- 定义邮件列表。具有多个收件人的别名就是一个邮件列表。

邮件别名定义在 `aliases` 文件中。`aliases` 文件的位置由 Sendmail 配置中的 `ALIAS_FILE` 定义。第 5 章中的 `redhat.mc` 配置文件使用 `ALIAS_FILE` 来设置别名文件的位置 `/etc/aliases`。默认情况下，Sendmail 8.11 将文件定位在 `/etc/mail` 目录 (`/etc/mail/aliases`)。无论位于何处，`aliases` 文件条目的的基本格式为：

```
alias: recipient
```

`alias` 是电子邮件地址中的用户名，`recipient` 是应该投递邮件的名称。`recipient` 字段可以包含用户名、另一个别名，或包含用户名和主机名的完整电子邮件地址。此外，一个别名可以有多个收件人以创建邮件列表。Red Hat 系统附带的 `aliases` 文件包含了少量添加内容，以说明别名的完整用途，如列表 6.5 所示。

# 列表 6.5 基础 Red Hat 别名数据库

```
#
# @(#aliases 8.2 (Berkeley) 3/5/94
# Aliases in this file will NOT be expanded in the header from
# Mail, but WILL be visible over networks or from /bin/mail.
#n# >>>>>>> The program "newaliases" must be run after
# >> NOTE >> this file is updated for any changes to
# >>>>>>> show through to sendmail.
```

```
# Basic system aliases -- these MUST be present.
MAILER-DAEMON: postmaster
postmaster: root
```

# General redirections for pseudo accounts.

```
bin: root
daemon: root
games: root
ing: root
nobody: root
system: root
to: root
ucp: root
```

# Well-known aliases.

```
manager: root
dumper: root
operator: root
webmaster: root
```

# trap catch

```
decode: root
```

# Person who should get mail

```
staff: root
```

# System administrator list

```
owner-staff: staff-request
: staff
staff-request: craig
```

# User aliases

```
jill.foobirds.org: norm
edwards: norm
edwardns: norm
: sara
rebecca.hunt: andy
sara.henson: kathy
leathe.McCafferty: kathy
```

Red Hat `aliases` 文件以 `#` 号开头的注释行开始，其中一条注释提醒你每次更新此文件都要运行 `newaliases`。Sendmail 不直接读取 `aliases` 文件，相反它读取由 `newaliases` 命令从该文件生成的数据库文件。

