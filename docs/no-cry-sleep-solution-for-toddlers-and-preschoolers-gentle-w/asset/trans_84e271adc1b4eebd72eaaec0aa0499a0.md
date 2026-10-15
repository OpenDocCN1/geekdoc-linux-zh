

```
defaults
{
    instances      = 60
    log_type       = SYSLOG authpriv
    log_on_success = HOST PID
    log_on_failure = HOST
    cps            = 25 30
}
includedir /etc/xinetd.d
```

作为示例，这里展示了 xinetd.d 目录中的 swat 文件。请注意它默认是禁用的：

```
# default: off
# description: SWAT is the Samba Web Admin Tool.\
# Use swat to configure your Samba server. \
# To use SWAT, connect to port 901 with your \
# favorite web browser.
service swat
{
    port           = 901
    socket_type    = stream
    wait           = no
    only_from      = localhost
    user           = root
    server         = /usr/sbin/swat
    log_on_failure += USERID
    disable        = yes
}
```

## TCP Wrappers

TCP wrappers 为 xinetd 管理的服务器增加了另一层安全性。实际上，服务器被一个中间的安全层包裹，用于监控连接并控制访问。通过 xinetd 建立的服务器连接会被监控，验证远程用户身份并检查其是否发出有效请求。连接会由 syslogd 守护进程记录（参见第 27 章），可能出现在 /var/log/secure 等 syslogd 文件中。使用 TCP wrappers，你还可以按远程主机限制对系统的访问。主机列表保存在 hosts.allow 和 hosts.deny 文件中。这些文件中的条目格式为 service:hostname.domain。domain 是可选的。对于 service，你可以指定特定服务，如 FTP，或使用 ALL 表示所有服务。对于 hostname，你可以指定特定主机或使用通配符匹配多个主机。例如，ALL 将匹配所有主机。表 20-7 列出了可用的通配符。在下面的示例中，第一条条目允许所有主机访问 Web 服务 http。第二条条目允许 pangol.train.com 主机访问所有服务。第三条和第四条条目允许 rabbit.trek.com 和 sparrow.com 访问 FTP：

```
http:ALL
ALL:pangol.train.com
ftp:rabbit.trek.com
ftp:sparrow.com
```

## TABLE 20-7
TCP Wrapper Wildcards

| Wildcard | Description |
|---|---|
| ALL | Matches all hosts or services. |
| LOCAL | Matches any host specified with just a hostname without a domain name. Used to match on hosts in the local domain. |
| UNKNOWN | Matches any user or host whose name or address is unknown. |
| KNOWN | Matches any user or host whose name or address is known. |
| PARANOID | Matches any host whose hostname does not match its IP address. |
| EXCEPT | An operator that lets you provide exceptions to matches. It takes the form of list1 EXCEPT list2 where those hosts matched in list1 that are also matched in list2 are excluded. |

hosts.allow 文件保存允许访问的主机。如果你想允许除少数特定主机外的所有主机访问，可以在 hosts.allow 文件中为某服务指定 ALL，但将要拒绝访问的主机列在 hosts.deny 文件中。使用 IP 地址而不是主机名更安全，因为主机名可以通过 DNS 记录被破坏，攻击者可通过欺骗攻击冒充另一台主机。

当 xinetd 收到对 FTP 服务的请求时，TCP wrapper 会监控连接并启动 in.ftpd 服务器程序。默认情况下，所有请求都被允许。要明确允许 FTP 服务的所有请求，你可在 /etc/hosts.allow 文件中输入以下内容。条目 ALL:ALL 将系统对所有主机、所有服务开放：

```
ftp:ALL
```

> Tip 最初，TCP wrappers 由 tcpd 守护进程管理。然而，xinetd 已将其对 TCP wrappers 的支持集成到自己的程序中。如果你愿意，可以显式调用 tcpd 守护进程来处理服务。tcpd 手册页（man tcpd）提供了有关 tcpd 的更详细信息。

## CHAPTER
FTP 服务器

文件传输协议（FTP）旨在跨网络从一个系统向另一个系统传输大型文件。与大多数 Internet 操作一样，FTP 采用客户端/服务器模型。FTP 客户端程序可使用户向运行 FTP 服务器程序的远程系统传输文件。 第 14 章讨论了 FTP 客户端。任何 Linux 系统都可以作为 FTP 服务器运行。它只需要运行服务器软件——具有适当配置的 FTP 守护进程。传输在客户端和服务器系统上的用户账户之间进行。远程系统上的用户必须登录到服务器上的一个账户，然后只能传输该账户目录中的文件。一种特殊类型的用户账户，名为 ftp，允许任何用户使用用户名“anonymous”登录到它。该账户拥有自己的目录和文件集，被视为公开，网络上任何想要下载的人都可以使用。Internet 上的众多 FTP 站点都是支持匿名登录 FTP 用户账户的 FTP 服务器。任何 Linux 系统都可以配置为支持匿名 FTP 访问，从而成为网络 FTP 站点。此类站点可在局域网或 Internet 上运行。

> Note 在 Red Hat 上，匿名 FTP 的配置文件现在包含在 vsftpd 包中。安装此包会设置你的 FTP 目录并配置 FTP 账户。

## FTP 服务器

FTP 服务器软件由 FTP 守护进程和配置文件组成。守护进程是一个程序，持续检查来自远程用户的 FTP 请求。当收到请求时，它管理登录、设置到所请求用户账户的连接，并执行远程用户发送的任何 FTP 命令。对于匿名 FTP 访问，FTP 守护进程允许远程用户使用 anonymous 或 ftp 作为用户名登录到 FTP 账户。用户随后可以访问为 FTP 账户设置的目录和文件。然而，作为进一步的安全措施，守护进程会将该会话的根目录更改为 FTP 主目录。这会将系统的其余部分隐藏于远程用户之外。通常，系统上的任何用户都可以移动到对他/她开放的任何目录。使用匿名 FTP 登录的用户只能看到 FTP 主目录及其子目录。系统的其余部分对该用户是隐藏的。这种效果是通过 chroot 操作实现的（稍后讨论），它从字面上更改了系统根目录

