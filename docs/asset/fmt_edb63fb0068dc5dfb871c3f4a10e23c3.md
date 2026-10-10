
```
$ /Reporter
--- passwords cracked as of May 19 21:43:07 CDT 1999 ---
Guessed jane [nosredna] Jane Anderson [password.tmp /bin/sh]
Guessed joe [scuba] Joe Johnson [password.tmp /bin/sh]
--- errors and warnings ---
StoreDataHook: invalid ciphertext: postgres
StoreDataHook: wg='postgresql' Server='postgres' cm='PostgreSQL'
Server [/etc/passwd /bin/bash] 'ct'-='sk!'
ignoring locked entry: admin*:3:4:admin:/var/adm
ignoring locked entry: bin*:1:1:bin
ignoring locked entry: daemon*:2:2:daemon:/sbin
ignoring locked entry: ftp*:14:50:FTP:/usr/ftp
ignoring locked entry: games*:12:100:games:/usr/games
ignoring locked entry: goopher*:13:30:goopher:/usr/lib/goopher
ignoring locked entry: halt*:7:0:halt:/sbin/halt
ignoring locked entry: ip*:14:37:ip:/var/pool/ipt
ignoring locked entry: mail*:8:12:mail:/var/mail
ignoring locked entry: news*:19:13:news:/var/spool/news
ignoring locked entry: nobody*:99:99:Nobody::/
ignoring locked entry: operator*:11:0:operator:/root
ignoring locked entry: shutdown*:6:0:shutdown:/sbin/shutdown
ignoring locked entry: sync*:5:0:sync:/bin/sync
ignoring locked entry: uucp*:10:14:uucp:/var/pool/uucp/
---
* done *
```

在此示例中，用户`bob`和`jane`的密码都被破解了。`Bob`使用了字典词`scuba`，而`jane`使用了她的姓氏倒写。您可以使用此报告识别密码较弱的账户并警告这些用户必须更改密码。

`Crack`甚至有一个巧妙的功能，可以自动向密码不佳的用户发送警告消息。如果您使用`-mail`参数调用`Crack`脚本，例如

```
/Crack -mail passwd
```

`Crack`然后会在该用户的密码被破解时向每个用户发送电子邮件。在这样做之前，您最好编辑`nastygram`脚本。该脚本用于向密码可以被破解的用户发送消息。它位于`crack`分发包的`scripts`子目录中，您可以使用以下命令编辑它：

```
vi /scripts/nastygram
```

您的编辑器中应包含以下内容：

```
#!/bin/sh
###
# This program was written by and is copyright Alec Muffett 1991,
# 1992, 1993, 1994, 1995, and 1996, and is provided as part of the
# Crack v5.0 Password Cracking package.
#
The copyright holder disclaims all responsibility or liability for
# respect to its usage or its effect upon hardware or computer
# systems, and maintains copyright as set out in the "LICENCE"
# document which accompanies distributions of Crack v5.0 and upwards.
###
```

```
for username in $$
do	  mail $username<<EndOfLetter
		`date`
```

亲爱的 `$username`，

您为账户 "Username" 使用的登录密码已被 "Crack" 密码猜测程序发现不安全。您必须尽快更改密码。

密码不容易被诸如 "Crack" 之类的程序攻破是基于非字典词的，因此任何可能出现在字典中的词，即使据称是晦涩的词也不合适。

同样，任何源自您姓名或其他个人信息而得的密码都不合适，因为它很容易被猜到。

## 484 部分 管理 OpenLinux

维护密码安全对所有使用这些计算机的人来说至关重要。我们感谢您在此事上的合作。

Yours,

```
[insert the name of your system administrator]
```

ps：这是一条录音公告。请在所有通信中牢记这一点。

EndOfLetter

如果您指定 `-email` 选项，`Crack` 将在用户的密码被破解时运行此脚本。脚本的大部分内容都是将发送给每个用户的信件文本。您可能希望自定义文本以使其适合您的情况。特别是，将 `[insert the name of your system administrator]` 行替换为适当人员的姓名、电子邮件和电话号码。

`-Crack -nice 10 -email mypasswd`

您也可以在调用 `Crack` 时组合多个参数。例如，如果您想以较低的（`nice`）优先级运行 `Crack` 以免拖慢系统，并且还想向密码不良的用户发送 `-email nastymails`，请这样调用 `Crack`：

在示例中，优先级值设置为 10（`-nice 10`），并且会向密码不良的用户发送电子邮件。

![](img/f0f494d795c6ea03cd25d687dd72914c_517_0.png)

请务必阅读在线文档以了解 `Crack` 的更多功能。文档以文本和 `HTML` 格式提供，与 `Crack` 脚本（`c50a` 目录）位于同一目录中。请查找 `manual.txt` 和 `manual.html` 文件。

### 通过过滤网络访问保护您的计算机

密码漏洞只是黑客可能利用的众多潜在弱点之一，以获取对您系统的访问权限。`OpenLinux` 及其类 `Unix` 系统提供各种网络服务，同时也提供了各种黑客攻击途径。了解这些服务以及如何限制对其的访问非常重要。

那么我所说的网络服务是什么意思？基本上，我指的是计算机执行的任何任务，该任务需要它通过

## 第 15 章 计算机安全问题 485

使用预定义的一组规则在网络上传送和接收信息。路由电子邮件是一种网络服务。提供 Web 页面也是如此。您的 `OpenLinux` 系统有潜力提供数千种服务。

许多服务在 `OpenLinux` 系统启动时会自动启动。其中一些服务由 `/etc/rc.d` 目录中的启动脚本启动的守护进程表示。其他进程则由对特定服务的请求启动。适用于您的 `OpenLinux` 系统的网络服务在 `/etc/services` 文件中定义。

一个在后台安静处理服务请求（例如 `sendmail`）的程序称为守护进程。通常守护进程在系统启动时自动启动，并在系统关闭前一直运行。守护进程也可以根据需要由 `inetd` 进程启动，`inetd` 是一个特殊的守护进程，监听大量端口号。

有关系统启动脚本的信息，请参阅第 13 章。

以下是 `/etc/services` 文件中部分信息的示例：

| Service | Port/Protocol | Alias |
|---|---|---|
| `tcpmux` | `1/tcp` | `# rfc-1078` |
| `echo` | `7/tcp` | |
| `echo` | `7/udp` | |
| `discard` | `9/tcp` | `sink null` |
| `discard` | `9/udp` | `sink null` |
| `systat` | `11/tcp` | `users` |
| `daytime` | `13/tcp` | |
| `daytime` | `13/udp` | |
| `netstat` | `15/tcp` | `quote` |
| `qotd` | `17/tcp` | `# message send protocol` |
| `msp` | `18/tcp` | `# message send protocol` |
| `msp` | `18/udp` | `ttytst source` |
| `charger` | `19/tcp` | |
| `charger` | `19/udp` | `ttytst source` |
| `ftp-data` | `20/tcp` | |
| `ftp` | `21/tcp` | |
| `telnet` | `23/tcp` | |
| `smtp` | `25/tcp` | `mail` |

请注意，每个条目包含两到三列。最左边的列包含每个服务的名称。中间列定义了该服务使用的端口号和协议类型。最右边的字段可以包含服务的可选别名或别名列表。

作为示例，我们检查文件片段中的最后一个条目。它描述了简单邮件传输协议（`SMTP`）服务，即用于在互联网上传递电子邮件的服务。中间列包含文本 `25/tcp`，这告诉我们 `SMTP` 协议使用端口 `25` 并使用传输控制协议（`TCP`）作为其协议类型。

## 486 部分 管理 OpenLinux

那么，端口号到底是什么？它是一个为特定网络服务预留的唯一数字。它允许网络连接为处理该服务的软件正确路由。例如，当电子邮件消息从另一台计算机发送到您的 `OpenLinux` 系统时，远程系统必须首先与您的系统建立网络连接。您的计算机接收连接请求，检查它，看到它标记为端口 `25`，因此知道连接应交给处理电子邮件的程序（碰巧是 `sendmail`）。

注意 `Internet` 分配号码管理局（`IANA`）负责分配可用端口号的子集。其政策是将相同的端口号分配给 `TCP` 和用户数据报协议（`UDP`）服务。无论您使用什么类型的计算机系统，端口号分配的服务都相同。

我提到 `SMTP` 使用 `TCP` 协议。一些服务使用用户数据报协议。您确实需要了解 `TCP` 和 `UDP`（就本次安全讨论而言），它们提供了在网络连接上传送信息的不同打包方式。`TCP` 连接提供错误检测和丢失数据的重传。`UDP` 不重传丢失的数据；它旨在以快速方式发送非关键信息。

理解服务和端口号的概念很重要，因为您使用这些信息来有选择地过滤可在 `Linux` 系统上访问的服务以及谁可以访问这些服务。

注意 尽管网络服务在 `/etc/services` 中定义，但服务实际上是在 `/etc/inetd.conf` 文件或系统启动脚本中打开或关闭的。`inetd.conf` 在本章中进行了描述。

### 保护远程 shell 和登录

`UNIX` 在网络计算机之间共享信息和任务方面有着灵活方式的历史。`OpenLinux` 遵循这一传统，包含所有用于远程登录、命令调用和数据传输的 `UNIX` 服务。虽然这些服务可能非常有用，但如果使用不当，也会在您的系统上造成安全风险。

一个有用但有风险的功能是远程 `shell` 服务，它传统上运行在 `TCP` 端口 `514` 上，并由 `inetd` 调用的 `in.rsh` 守护进程调用。远程 `shell` 使您能够在远程系统上调用命令，而无需为该系统提供密码。您使用远程 `shell` 命令 `rsh` 来执行此操作。例如，如果您登录到名为 `tick` 的计算机，并希望检查名为 `tock` 的计算机上主目录的内容，您将输入以下内容：

```
rsh tock ls
```

## 第 15 章 计算机安全问题 487

这会在 `tock` 上调用 `ls` 命令，就好像您登录、输入命令然后注销一样。它无需提示您输入密码，因为 `tick` 被 `tock` “信任”。

如何告诉一个系统信任另一个系统？一种方法是列出信任系统上 `/etc/hosts.equiv` 文件中的受信任主机。通过在 `hosts.equiv` 文件中列出一个系统，您是在告诉计算机，远程系统上的任何用户都应被允许在不登录和提供密码的情况下在您的系统上运行命令。他们需要在本地系统上拥有用户名。您的计算机将假定此用户是同一个人，并允许远程用户以匹配的本地用户权限运行命令。

在 `hosts.equiv` 文件中放置一个加号 (`+`) 会告诉您的系统信任所有系统。此操作自然会带来可怕的安全后果，您绝不应该这样做。

即使您没有 `hosts.equiv` 文件，单个用户也可以通过在其主目录中创建 `.hosts` 文件来启用对其帐户的远程 `shell` 访问。`.hosts` 文件基本上与 `hosts.equiv` 文件相同，但它仅影响该用户的帐户，而不是系统上的所有用户。其他用于建立信任的命令包括 `login`（远程登录）命令和 `rcp`（远程复制）命令，它们使用 `hosts.equiv` 和 `.hosts` 文件。

请参阅第 10 章以了解有关远程 `shell` 和网络服务的更多信息。

使用这些远程服务会带来一些风险。您的系统安全性仅与“信任”的系统中最脆弱的系统一样安全。如果您在 `hosts.equiv` 中列出的其中一台计算机被破解，黑客将能够轻松地从该系统跳转到您的系统。

除非您绝对需要使用远程 `shell` 或远程复制服务，否则我建议您完全禁用它们。

### 禁用网络服务

远程 `shell` 服务只是由 `inetd` 进程处理的众多服务之一。`Inetd` 是一个守护进程，监听大量网络端口号。当连接到特定端口号时，`inetd` 会自动启动该服务的适当程序并处理与其的连接。配置文件 `/etc/inetd.conf` 用于告诉 `inetd` 监听哪些端口以及启动哪些程序。以下是其中一个示例片段：

```
# Shell, login, exec and talk are BSD protocols.
#
shell stream tcp nowait root /usr/sbin/in.rsh
login stream tcp nowait root /usr/sbin/in.login
```

## 488 第三部分 管理 OpenLinux

```
#exec stream tcp nowait /usr/sbin/tcpd in.rexecd
talk dgram udp wait nobody/tty /usr/sbin/tcpd in.talkd
ntalk dgram udp wait nobody/tty /usr/sbin/tcpd in.ntalkd
#dtalk stream tcp wait nobody/tty /usr/sbin/tcpd in.dtalkd
```

### /etc 中的 Pop 和 imap 服务

```
pop-2 stream tcp nowait /usr/sbin/tcpd ipop2d
pop-3 stream tcp wait /usr/sbin/tcpd ipop3d
imap stream tcp wait /usr/sbin/tcpd imapd
```

与 `Unix` 配置文件一样，以井号（`#`）开头的行是注释。如果一行没有井号，则该行列出了 `inetd` 应处理的服务、有关网络连接类型的信息，以及在建立该类型连接时要启动的程序。

毫不巧合的是，本示例中列出的前两个服务是 `shell` 和登录服务。你可能从 `/etc/services` 文件中认出这些服务名称；它们是 `rsh`、`rcp` 和 `login` 使用的服务。要禁用这些服务，请在这些行前面加上井号字符，将其变成注释。`exec` 服务在此之前的代码示例中已被注释掉。（默认情况下，`OpenLinux` 中 `exec` 服务是开启的。）

> 你可以让远程登录服务保持活动状态，但禁用 `/etc/host.equiv` 和 `.hosts` 文件的使用，要求登录时始终提示输入密码。与其在 `inetd.conf` 中注释掉 `login` 行，不如在其末尾添加一个空格后跟 `-L`。

首先，使用 `su` 命令切换为 `root`，并使用你喜欢的文本编辑器（如 `vi` 或 `emacs`）编辑 `/etc/inetd.conf` 文件。注释掉你希望禁用的服务，保存更改并退出编辑器。现在你需要向 `inetd` 进程发送一个信号以重新加载其配置文件。通过输入以下命令查找 `inetd` 进程的进程号：

```
ps ax | grep inetd
```

`ps ax` 命令输出所有当前正在运行进程的列表。`|` 字符表示将 `ps` 命令的输出管道传输到 `grep` 命令的输入。`grep inetd` 命令过滤其输入，仅显示包含单词 `inetd` 的行。这将产生类似以下内容的输出：

```
249 ? S 0:00 (inetd)
6030 p S 0:00 grep inetd
```

请注意，`grep inetd` 命令本身也出现在输出中，因为它也包含文本 `inetd`。请忽略该行；我们真正想要的是它上面的那一行。它显示 `inetd` 的进程号为 `249`。现在我们可以发送一个信号给该编号，使 `inetd` 重新加载其配置文件：

```
kill -HUP 249
```

就这样——你已禁用了远程 `shell` 和登录服务。如果有人尝试使用这些服务，他们将收到“连接被拒绝”错误消息。

## 使用 TCP wrappers

完全禁用未使用的服务是可以的，但对于你真正需要的服务怎么办？如何有选择地授予和拒绝对这些服务的访问？一种常用的有选择地授予和拒绝服务访问的功能称为 `TCP wrappers`。让我们再次查看 `/etc/inetd.conf` 文件的一部分以寻找线索。

```
#
# Pop and imap mail services as follows
pop-2  stream tcp nowait root /usr/sbin/tcpd ipop2d
pop-3  stream tcp nowait root /usr/sbin/tcpd ipop3d
imap  stream tcp nowait root /usr/sbin/tcpd imapd
```
