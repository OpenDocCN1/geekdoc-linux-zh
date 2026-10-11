

如果您想保护自己免受垃圾邮件的骚扰，我们强烈建议注释掉这一行。但是，笔记本电脑以及没有 24x7 DNS 的计算机上的用户确实需要此功能。

```
FEATURE(`accept_unresolvable_domains')
dnl FEATURE(`relay_based_on_MX')
```

这个 36 行的宏文件被转换为了 1,216 行的 `sendmail.cf` 文件。以下是将宏文件 `redhat.mc` 转换为最终 `sendmail.cf` 文件的流程。

```
m4 redhat.mc > /etc/sendmail.cf
```

请务必小心，不要覆盖现有的配置文件。以下描述将讲解该文件的主要配置选项，以展示其工作原理。

以下这一行会从生成的配置文件中移除多余的信息：

```
d divert(-1)
```

以下这一行包含了 `cf.m4` 文件：

```
include(`../m4/cf.m4')
```

下一行定义了默认的用户 ID：

```
define(`confDEF_USER_ID',`8:12')
```

下一行指定了要使用的操作系统类型。许多参数，如路径文件，都由此选项决定。

```
OSTYPE(`linux')
```

这一行表明该主机不是 UUCP 邮件中继：

```
undefine(`UUCP_RELAY')
```

这一行表明该主机不接受 BITNET 邮件：

```
undefine(`BITNET_RELAY')
```

这一行表明服务器应自动重建别名：

```
define(`confAUTO_REBUILD')
```

以下这一行将连接超时时间设置为 1 分钟：

```
define(`confTO_CONNECT', `1m')
```

以下这一行指出，如果此服务器是某主机的最佳 MX 记录且未做其他安排，则尝试直接连接到该主机；通常这会导致配置错误。

```
define(`confTRY_NULL_MX_LIST',true)
```

以下这一行声明 sendmail 不会将任何本地接口的名称和地址插入到 $=w 类（已知“等效”地址列表）中：

```
define(`confDONT_PROBE_INTERFACES',true)
```

下一行是 procmail 程序的路径：

```
define(`PROCMAIL_MAILER_PATH','/usr/bin/procmail')
```

这一行告诉 sendmail 使用发行版提供的 sendmail 受限 Shell (smrsh) 而不是 /bin/sh 来进行向程序的邮件发送：

```
FEATURE(`smrsh','/usr/sbin/smrsh')
```

以下这一行定义了一个可用于自定义邮件路由的表：

```
FEATURE(`mailertable','hash -o /etc/mail/mailertable')
```

下一行定义了特定域名的别名形式，允许在一台机器上托管多个虚拟域名：

```
FEATURE(`virtusertable','hash -o /etc/mail/virtusertable')
```

以下这一行会导致 sendmail 拒绝所有地址为 REDIRECT 的邮件，并返回 551 用户不在此本地；请尝试 <address> 的消息。如果设置了此项，您可以将已离开人员通过附加 .REDIRECT 别名的方式重定向到新地址。

```
FEATURE(redirect)
```

下一行导致 sendmail 始终将域名附加到地址中，即使对于本地邮件也是如此。

```
FEATURE(always_add_domain)
```

这一行启用了使用本地 sendmail.cw 文件的功能。

```
FEATURE(use_cw_file)
```

这一行导致 sendmail 使用 procmail 作为本地邮件处理程序。

```
FEATURE(local_procmail)
```

这一行是用于配合邮件器表使用的 procmail 接口。

```
MAILER(procmail)
```

下一行启用了 SMTP 邮件服务器功能。

```
MAILER(`smtp`)
```

以下这一行开启了访问数据库功能。访问数据库使您能够出于管理原因允许或拒绝接受来自特定域名的邮件。

```
FEATURE(`access_db`)
```

下一行启基于用户名、主机名或地址拦截邮件的功能。

```
FEATURE(`blacklist_recipients`)
```

这一行导致 sendmail 接受邮件，即使发送方的域名无法通过 DNS 解析。

```
FEATURE(`accept_unresolvable_domains`)
```

以下这一行中的 dnl 宏用于注释掉 FEATURE 命令。

```
dnl FEATURE(`relay_based_on_MX`)
```

## 邮件别名与转发

别名非常有用，因为它们允许邮箱拥有多个名称，因为它们在需要时可以邮件转发到其他地址，并且可以让重要的邮件（例如发给 root 的邮件）流向更频繁检查的账户。别名通过 `/etc/aliases` 文件进行配置，其语法如下：

```
name: name_1, name_2, name_3, . . .
```

别名可以是递归的，即一个别名指向另一个不同的别名。以下是 `/etc/aliases` 文件的一个示例。

```
# Basic system aliases -- these MUST be present.
MAILER-DAEMON: postmaster
postmaster:      root

# General redirections for pseudo accounts.
bin:             root
daemon:          root
games:          root
inger:           root
nobody:          root
system:          root
toor:            root
uucp:            root

# Well-known aliases.
manager:		root
dumper:		root
operator:		root

# trap decode to catch security attacks
decode:		root

# Person who should get root's mail
root:		jason, angie

# Custom Aliases
jason:		jason.nash
angie:		angie.nash
jason.nash	j
```

每当更新 /etc/aliases 文件时，您都需要运行 newaliases 命令，这与运行 sendmail -bi 相同。

```
[root@redhat ~]# newaliases
/etc/aliases: 14 aliases, longest 10 bytes, 152 bytes total
```

> **考试提示** 每当 /etc/aliases 中添加了新条目时，您必须运行 newaliases 命令。

别名必须由 root 处理。如果用户想要将自己的邮件转发到另一个位置，他们使用主目录中的 .forward 文件。.forward 文件的格式仅仅是用于转发邮件的电子邮件地址列表。例如：

```
jason@the-nashes.net
nash@site.org
"/home/jason/archive"
```

此文件会将收到的任何邮件转发到前两个地址，然后将其写入 /home/jason/archive 文件。

> **在现实世界中** sendmail 会检查以确保 .forward 文件，或其所处的目录，只能由所属用户写入。这是一种安全措施，以确保没有人会在您不知情的情况下转发您的邮件。

## 管理 sendmail

在大多数情况下，sendmail 不是通过 inetd 运行的，因为它一直驻留。它由取决于发行版的脚本在启动时开始运行。要在 Red Hat 系统上管理 sendmail，您会使用 /etc/rc.d/init.d/sendmail 脚本，如下所示：

```
/etc/rc.d/init.d/sendmail start|restart|stop|status
```

Debian 使用 `/etc/init.d/sendmail` 脚本，如下所示：

```
/etc/init.d/sendmail start|stop|restart|reload|force-reload|debug
```

force-reload 命令即使 sendmail 挂起也会重启它。debug 选项向 sendmail 发送 USR1 kill 信号，这告诉守护进程转储其进程信息。要查看队列中当前消息，您使用 `mailq` 命令，或 `sendmail -bp`。每条消息的第一行显示该主机上用于该消息的内部标识符 (TAA08962)、消息的字节大小 (11)、消息被接受进入队列的日期和时间 (Thu Dec 7 19:55)，以及消息的信封发送者 (root)。第二行显示导致该消息保留在队列中的错误消息；如果消息是首次处理，则此信息不存在。以下各行显示消息收件人，每行一个 (Jason@the-nashes.net)。可选的 `-v` 选项会增加某些错误的信息量。例如：

```
debian:/etc# mailq -v
        Mail Queue (2 requests)
-+Q-ID-+-Size-+-Priority---+Q-Time-++-------------------Sender/Recipient-----------------
SAA02253        5        30026 Mar 23 18:45 root
               (host map: lookup (@doom.org): deferred)
                json@doom.org
SAA02248        5        30025 Mar 23 18:45 root
               (host map: lookup (blah.com): deferred)
                json@blah.com
```

mailq 工具用于显示当前在队列中等待的消息。

## 使用 Apache

### 1.13 网络服务

- 操作并执行 apache 的基本配置。修改 apache 配置文件中的简单参数，启动、停止和重启 httpd，安排 httpd 在启动时自动重启。不包括 apache 的高级自定义配置。包括管理 httpd 配置文件。

Apache Web 服务器目前是互联网上最流行的服务器。每个 Linux 发行版都默认使用它，这是有充分理由的。它是免费的、快速的、可配置性极强、得到广泛支持且非常稳定。Apache 基于原始的 NCSA（国家高级计算中心）Web 服务器。由于原始源代码应用了如此之多的“补丁”，以至于它被称为“补丁”服务器。Apache 的名字可能有点俗气，但它是一个伟大的 Web 服务器！

Apache 提供标准 HTTP 以及支持 SSL 的安全连接。其他功能可以轻松通过模块添加。

