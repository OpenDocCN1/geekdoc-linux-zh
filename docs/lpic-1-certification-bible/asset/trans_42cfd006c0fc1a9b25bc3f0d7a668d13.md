

## ftphut 参数

| 参数 | 功能 |
| :--- | :--- |
| `-V` | 显示版本信息。 |
| `-l <min>` | 在关闭之前不再接受连接的分钟数。此值的默认为 10。 |
| `-d <min>` | 在关闭之前断开用户连接的分钟数。此值的默认为 5。 |
| `time` | 服务器将被关闭的时间。可能的值如下：*now*，立即关闭服务器；`+<number>`，指定从现在起关闭服务器的分钟数；以及 *HHMM*，指定关闭服务器的确切时间。 |
| `warning-message` | 显示给用户的警告消息。您可以嵌入“魔法 cookie”变量，这些变量将由 FTP 服务器自动替换为动态信息。请参阅 man 页面了解变量列表。 |

### ftpwho 命令

`ftpwho` 命令显示当前连接到您的 FTP 服务器的用户。
以下是一个示例输出：

```
[root@redhat ~]# ftpwho
Service class all:
8349 ?       S     0:00 ftpd: 10.254.90.154: anonymous/jason@the-nashes.net:
 - 1 users (no maximum)
```

输出显示以下五个字段：

- 进程 ID
- tty 连接编号，由于未被使用，始终为 `?`。
- 连接状态
- 迄今使用的 CPU 时间
- 连接详情

状态字段可以是 *R*（运行中）、*S*（休眠）或 *Z*（崩溃）。详情显示谁连接了，来自哪里，以及用于匿名登录输入的电子邮件地址。

### ftpcount 命令

`ftpcount` 命令显示连接的用户数量，按 `ftpaccess` 文件中规定的用户类别进行细分。它还显示允许连接的最大用户数。例如：

```
[root@redhat ~]# ftpcount
Service class all            -       1 users (no maximum)
```

## 配置 Telnet

Telnet 服务器为系统提供远程终端访问权限，通常由 `inetd` 使用 `inetd.conf` 中的以下条目运行：

```
telnet stream tcp nowait root /usr/sbin/tcpd in.telnetd
```

表 16-8 显示了 `in.telnetd` 的可用参数。如果 `/etc/issue.net` 文件存在，它将在用户登录系统之前显示给用户。

### 表 16-8：in.telnetd 参数

| 参数 | 功能 |
| :--- | :--- |
| `-a <authmode>` | Telnet 守护程序提供的认证类型。默认情况下，`telnetd` 不处理认证，而是将其留给 `login`。 |
| `-D <debugmode>` | 设置调试模式。可能的值如下：`options`，显示关于 Telnet 选项协商的信息；`report`，显示 `options` 信息，但提供更多详细信息；`netdata`，显示数据流；以及 `ptydata`，显示写入 pty（伪终端）的数据。 |
| `-edebug` | 如果 Telnet 服务器编译了加密支持，这将启用加密调试信息。 |
| `-h` | 禁用用户在登录前显示的主机特定信息。 |
| `-L <Login Program>` | 指定非默认登录程序。默认为 `/bin/login`。 |
| `-n` | 禁用 TCP keep-alive。 |
| `-s` | 与 SecurID 认证卡一起使用。 |
| `-S <tos>` | 设置 IP 服务类型选项。 |
| `-X <authtype>` | 用于禁用认证（如果该选项被编译到服务器中）。 |

## 使用 sendmail

**目标 1.13 网络服务**

- 操作 sendmail 并进行基本配置。修改 sendmail 配置文件中的简单参数（如有必要，修改“智能主机”的 DS 值），创建邮件别名，管理邮件队列，启动和停止 sendmail，配置邮件转发（forward），执行 sendmail 的基本故障排除。不包括 sendmail 的高级自定义配置。包含命令 mailq、sendmail 和 newaliases。包含别名和 mail/ 配置文件。

Linux 服务器可以成为功能强大且高性能的邮件服务器。如今互联网上的大多数邮件服务器都运行 sendmail 服务器。大多数 Linux 发行版都包含最新版本的 sendmail，即使仅用于本地邮件使用。单靠 sendmail 并不能为您提供一个完整的邮件系统。表 16-9 显示了基本组件。

**在现实世界中**
有关 sendmail 的更多信息和文档可在 http://www.sendmail.org 上获取。

### 表 16-9：邮件系统组件

| 组件 | 用途 | 示例 |
| :--- | :--- | :--- |
| MTA（消息传输代理） | 在服务器之间传输消息。 | sendmail, Postfix, exim |
| MUA（邮件用户代理） | 将用户连接到电子邮件系统。 | pine, elm, Outlook Express |
| MDA（邮件传递代理） | 将消息从服务器传递到用户的帐户。 | Procmail |

三个主要配置文件如表 16-10 所示。

### 表 16-10：sendmail 配置文件

| 文件 | 功能 |
| :--- | :--- |
| `/etc/sendmail.cf` | 主配置文件。 |
| `/etc/sendmail.cw` | 列出接受邮件的主机列表。 |
| `/etc/aliases` | 列出别名地址。 |

### 自定义 sendmail.cf

sendmail 的主配置文件是 /etc/sendmail.cf。该文件非常大且复杂。它的设计初衷不是易于自定义，而是易于解析。以下是 Red Hat sendmail.cf 的一个示例：

```
RC < $+
RC > $+
RC > $+
RC < < $+ > $* > $*
RC < < $+ > + $*
RC < < $* >
Rl+
R#+ < > $*
R# < > $*
RC local : $* > $*
RC error : $* > $*
RC $- : $+ > $*
RC $+ > $+
        $: < $H > $1             try hub
        $: < $R > $1             try relay
        $: < < $1 > $aH >        nope, restore *detail
        < < $1 > + $2 > $3        find the user part
        $flocal $H $2 $: < $1    strip the extra +
        $* $1                    no *detail
        add *detail back in
        check whether *detail
        else discard
        $95 < local > $1 > $2    no host extension
        $95 < error > $1 > $2    no host extension
        $95 < $1 > $2 < < $2 >
        $95 < $1 > $2 < @ $1 >
```

这看起来很吓人，而且默认 Red Hat 系统中的该文件长度超过 1,200 行。大多数选项永远不需要更改，但即使是像这样的部分中不小心出现的一个拼写错误也可能是灾难性的。sendmail.cf 文件中考试所需的唯一条目是智能主机条目。在某些情况下，您的服务器可能不会自己处理邮件投递，而是将邮件转交给另一个服务器，通常是您的 ISP。DS 指令设置为用于投递邮件的服务器。例如，要将邮件交给 ISP 的服务器并由其处理投递，您可以将其设置为如下所示：

```
# "Smart" relay host (may be null)
DShip.name.net
```

![](img/96d9ccd181675a8ae8b6a1146c919d2b_651_0.png)

如果您的 ISP 实际上为您系统的邮件投递提供支持，则可能需要更改智能主机条目。

为帮助减轻这些配置问题，开发人员开发了一种新的配置方法。新方法使用 m4 预处理器。此预处理器允许管理员编写一个更容易理解的文件，然后将其转换为 sendmail.cf 格式。

![](img/96d9ccd181675a8ae8b6a1146c919d2b_651_1.png)

m4 预处理器用于简化 sendmail 的配置。宏文件被转换为最终的 sendmail.cf。

本节提供了该过程的快速概述，但并非旨在作为完整的指南，那将远超本书的范围。完整的 m4 宏列表见 README 文件。m4 宏具有以下语法：

```
Name(argument1, argument2, argument3 . . .)
```

有许多内置宏，您也可以创建自己的宏。表 16-11 展示了一些最常用的宏。

### 表 16-11：常见 m4 宏

| 宏 | 功能 |
| :--- | :--- |
| `define` | 定义带有参数的宏。 |
| `undefined` | 取消定义之前设置的宏。 |
| `include` | 包含参数中指定的文件。 |
| `dnl` | 忽略直到下一个换行符的所有字符。 |
| `divert` | 管理输出。 |
| `feature` | 用于启用其他功能。 |

以下是用于创建本节开头 sendmail.cf 的输入文件示例。

```
divert(-1)

dnl This is the macro config file used to generate the /etc/sendmail.cf
dnl file.  If you modify this file you will have to regenerate the
dnl /etc/sendmail.cf by running this macro config through the m4
dnl preprocessor:
dnl
dnl    m4 /etc/sendmail.mc > /etc/sendmail.cf
dnl

dnl You will need to have the sendmail-cf package installed for this to
dnl work.

include(`../m4/cf.m4')
define(`confDEF_USER_ID',"8:12")
OSTYPE(`linux')
undefine(`UUCP_RELAY')
undefine(`BITNET_RELAY')
define(`confAUTO_REBUILD')
define(`confTO_CONNECT', "1m")
define(`confTRY_NULL_MX_LIST',true)
define(`confFONT_PROBE_INTERFACES', true)
FEATURE(`PROCMAIL_MAILER_PATH','/usr/bin/procmail')
FEATURE(`smrsh','/usr/sbin/smrsh')
FEATURE(`mailertable','hash -o /etc/mail/mailertable')
FEATURE(`virtusertable','hash -o /etc/mail/virtusertable')
FEATURE(redirect)
FEATURE(always_add_domain)
FEATURE(use_cw_file)
FEATURE(local_procmail)
MAILER(procmail)
MAILER(smtp)
FEATURE(`access_db')
FEATURE(`blacklist_recipients')
```

