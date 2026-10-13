
## Router 文件

路由器文件在工作站和邮件中继服务器之间略有不同。

由于 `smail` 默认假设使用 `uucp` 传输，这些路由器文件只是强制所有内容通过 IP 链路使用 SMTP。两个文件唯一的区别在于工作站配置使用 `smarthost` 路由，但中继服务器期望能够连接到消息的真实目的地。

### 工作站路由器文件

```
# inet_addrs - match domain literals containing literal IP
# addresses. The library routine gethostbyaddr(3N) will be
# called to see if a reverse mapping to the canonical hostname
# is available.
inet_addrs:
driver = gethostbyaddr,    # router to match IP domain
# literals
transport = smtp;          # deliver using SMTP over
# TCP/IP

fail_if_error,             # fail malformed domain
# literal addrs
check_for_local            # see if this is really the
# local host

# paths - force some routes using the YP network path database
paths:  driver = pathalias,    # general-use paths router
transport = smtp;             # for matches, deliver over
# SMTP
file = mail_paths,    # database containing path info
proto = yp,           # look in yp database

# inet_hosts - match hostnames with gethostbyname(3N) or bind
inet_hosts:
    driver = gethostbyname,   # match hosts with the
    # library function
    # driver=bind,            # Alternative for DNS
    transport = smtp;
    domain = mydomain.com

# smart_host - a partially specified smarthost director
#
# If the config file attribute smart_path is defined as a path
# from the local host to a remote host, then hostnames not
# matched otherwise will
# be sent off to the stated remote host. The config file
# attribute smart_transport can be used to specify a different
# transport.
#
# If the smart_path attribute is not defined, this router is
# ignored.
smart_host:
    driver = smarthost,       # special-case driver
    transport = smtp          # by default deliver over SMTP
```

### 邮件中继服务器的路由器文件

邮件中继服务器的路由器文件并没有本质上的不同。主要区别在于它可能没有定义 `smart_path`，因为它期望能够访问整个互联网，而不仅仅是一个上游邮件服务器。此文件已删除所有 `uucp` 路由。

```
# match_inet_addrs - match literal Internet-family addresses
#
# This director will match hostnames such as [192.2.12.200],
# which are literal addresses on a TCP/IP network. This form
# should only be used when the actual hostname cannot be found
# in the network databases, or to get around a "forces" file
# that reroutes mail to a host listed in the databases for the
# TCP/IP network.
Match_inet_addrs:
    driver=gethostbyaddr,    # match inet domain
    # literal addrs
        transport=smtp;      # delivery is over
```

```
# smtp/tcp
    fail_if_error,        # non-inet literals are
# errors
    check_for_local       # check for local host

# match-inet-hosts - match hosts in the TCP/IP network database
#
# On the mail hub we always want to use bind for host lookup
match-inet-hosts:
    driver=bind,          # match hosts on network
    transport=smtp;       # delivery is over smtp/tcp
    domain = mydomain.com # strip trailing domain
# before lookup
```

## 传输文件

`smail` 文档描述了传输配置文件。然而，在纯 SMTP 环境中，你几乎永远不需要它。

## 运行 smail

`smail` 实现了与 `sendmail` 相同的许多命令行选项。这是作者的刻意政策，以便其他程序，例如 `majordomo`，不必知道正在运行的是哪个 MTA。

## Qmail

`Qmail` 旨在作为 `sendmail+MH` 的更小、更简单的替代品。因为运行 `MH` 或 `fetchmail` 之类的额外复杂性通常是不必要的，所以 `qmail` 在某种程度上是在攻击一个已不存在的目标。

### Qmail 邮件投递选项

`Qmail` 有自己的方式将邮件投递给本地用户。实际上有三种不同的处理方式。`MAILDIR` 格式将邮件放在 `~/Mail/` 中，每个邮件单独一个文件。从避免文件锁定问题的角度来看，这是一件好事，但从 MUA 的角度来看，这是一件坏事，因为 MUA 必须打补丁才能识别这种格式。许多流行 MUA 的补丁都可用。第二种格式是 `MAILFILE`。这里的邮件全部放在用户主目录中的一个文件中，例如 `~/mbox`。许多 MUA 只需一个命令行选项来告诉它们去哪里查找即可读取此格式，但如果同时运行两个或多个 MUA，则会出现竞争问题。如果你的 MUA 使用 POP 或 IMAP 访问邮件，则竞争问题显然会消失。第三种格式是 `SPOOLDIR`，它将邮件放在 `/var/spool/mail/$USER` 中——就像传统的 `sendmail` 一样。`qmail` 的作者认为这种选项不安全，presumably 因为每个人的邮件都存放在同一个目录中。

### Qmail 消息处理

`Qmail` 处理消息的特有方式也有好处，即它可以与其他 MTA 协同运行，而它们不会互相干扰。这在处理多个域名、运行级联邮件处理程序以及其他更晦涩的情况下很有用。我只发现过一种情况，这样做实际上是有用的。

与 `sendmail` 一样，`qmail` 可以处理虚拟域名。然而，它不具备 `sendmail` 对虚拟用户和中继进行精细控制的能力。除非安装某些可选组件，否则 `qmail` 也不会使用中央别名文件 `/etc/aliases`。在这方面，它也与其他 MTA 相当不同。

`Qmail` 总是立即投递邮件。因此它不是拨号用户或所有邮件都通过集线器或中继路由的最佳选择。然而，据说它能很好地处理高邮件负载。因此它在与 `majordomo` 等列表服务器配合使用方面具有竞争力。`Qmail` 还提供了一个 `sendmail` 包装器，以便其他程序无需知道它们运行的不是真正的 `sendmail` 而只是一个纸板仿制品。
