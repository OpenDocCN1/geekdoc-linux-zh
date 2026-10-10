

## ppp-on-dialer 脚本

这是实际建立我们 PPP 链接的脚本中的第二个。

![](img/a3584dae761d2e3abed8bf40d7637389_359_0.png)

**注意**

Chat 脚本通常都是单行写的；反斜杠用于允许跨多个物理行进行续行（为了便于人类阅读），它们不属于脚本本身的一部分。但是，详细查看它非常有用，这样我们才能理解它实际上（应该）在做什么！

### 什么是 Chat 脚本

Chat 脚本是一系列 *期望字符串 发送字符串* 的配对。特别注意，我们在发送任何内容之前*总是期望某些东西*。

如果我们希望在*未*先接收任何内容的情况下发送某些内容，我们必须使用一个空的 *期望* 字符串（用 `""` 表示）；同样地，如果我们希望在不发送任何内容的情况下期望某些东西！此外，如果字符串包含多个单词（例如 NO CARRIER），你必须给字符串加上引号，以便 chat 将其视为一个单一实体。

我们模板中的 chat 行是：

```
exec /usr/sbin/chat -v
```

调用 chat，-v 告诉 chat 将*所有*输入/输出复制到系统日志中（通常是 `/var/log/messages`）。一旦你确信 chat 脚本能可靠工作，请编辑该行以移除 -v，从而避免在 syslog 中产生不必要的杂乱信息。

```
TIMEOUT 3
```

这将接收预期输入的超时时间设置为三秒。如果你使用的是速度极慢的调制解调器，可能需要将此值增加到五秒或十秒！

```
ABORT '\nBUSY\r'
```

如果接收到 *BUSY* 字符串，则中止操作。

```
ABORT '\nNO ANSWER\r'
```

如果接收到 *NO ANSWER* 字符串，则中止操作。

```
ABORT '\nRINGING\r\n\r\n\nRINGING\r'
```

如果接收到（重复的）*RINGING* 字符串，则中止操作。这是因为有人在拨打你的电话线！

```
""\rAT"
```

从调制解调器处不期望任何内容，并发送字符串 `AT`。

```
OK---+++\c--OK ATH0
```

这一行稍微复杂一些，因为它使用了一些 chat 的错误恢复功能。

它的含义是... 期望 OK；如果没有接收到（因为调制解调器不在命令模式下），则发送 `+++`（这是标准的兼容 Hayes 的调制解调器字符串，用于将调制解调器返回到命令模式），并期望 OK。然后发送 ATH0（调制解调器的挂断字符串）。这使得你的脚本能够应对调制解调器卡在在线状态的情况。

```
TIMEOUT        30
```

将脚本剩余部分的超时时间设置为 30 秒。如果你遇到 chat 脚本因超时而中止的问题，请将其增加到 45 秒或更多。

```
OK             ATDT$TELEPHONE
```

期望 OK（这是调制解调器对 ATH0 命令的响应）并拨打我们要呼叫的号码。

```
CONNECT
```

期望 CONNECT（我们的调制解调器在远程调制解调器应答时发送）并不回复任何内容。

```
login::--login:    $ACCOUNT
```

同样，这里也内置了一些错误恢复功能。期望登录提示符（`...login:`），但如果未在超时前接收到，则发送一个回车并再次查找登录提示符。当接收到提示符时，发送用户名（存储在 shell 变量 *ACCOUNT* 中）。

```
assord:        $PASSWORD
```

期望密码提示符并发送我们的密码（同样，存储在 shell 变量中）。

这个 chat 脚本具有合理的错误恢复能力。Chat 具有比这里展示的更多功能。更多信息请参阅 chat 手册页（`man 8 chat`）。

### 在服务器端启动 PPP

虽然 ppp-on-dialer 脚本对于在登录后自动在服务器端启动 pppd 的服务器来说没问题，但有些服务器要求你明确地在服务器上启动 PPP。

如果你需要发出一个命令来启动服务器上的 PPP，*确实*需要编辑 ppp-on-dialer 脚本。

在脚本的末尾（在密码行之后）添加额外的 *期望 发送* 配对——这一对将查找你的登录提示符（注意在 Bourne shell 中具有特殊含义的字符——例如 `[` 和 `]`（左方括号和右方括号））。

一旦找到 shell 提示符，chat 必须发出你的 ISP PPP 服务器所需的**PPP 启动**命令。

在我的情况下，我的 PPP 服务器使用标准的 Linux Bash 提示符 `[harrt@kepler harrt]$`，并且需要我输入

`ppp`

来启动服务器上的 PPP。

在这里允许一点错误恢复是个好主意，所以在我的情况下我使用 `harrt--harrt    ppp` 这表示，如果我们在超时前未接收到提示符，则发送一个回车并再次查找提示符。

一旦接收到提示符，则发送字符串 *ppp*。

![](img/a3584dae761d2e3abed8bf40d7637389_361_0.png)

> **注意**
> 别忘了在上一行末尾添加 `\`，以便 chat 仍然认为整个行脚本是在一行中。

不幸的是，一些服务器会产生非常多变的提示符。你可能需要使用 *minicom* 登录几次以了解发生了什么，并挑选稳定的 *期望* 字符串。

### 用于 PAP/CHAP 认证连接的 Chat 脚本

如果你的 ISP 使用 PAP/CHAP，那么你的 chat 脚本要简单得多。你的 chat 脚本所需要做的只是拨号，等待连接，然后让 *pppd* 处理登录。

```
#!/bin/sh

#
# This is part 2 of the ppp-on script. It will perform the
# connection protocol for the desired connection.
#
exec /usr/sbin/chat -v
TIMEOUT         3
ABORT	'\nBUSY\r'
ABORT	'\nNO ANSWER\r'
ABORT	'\nRINGING\r\n\n\nRINGING\r'
"\n\n\n\nPAT" 'OK\n++\n\c-OK'	ATHO
TIMEOUT	30
OK	ATDT$TELEPHONE
CONNECT	''
```

### pppd 的 debug 和 file 选项

正如我们已经看到的，你可以使用 pppd 的 -d 选项开启调试信息日志记录。debug 选项与此等效。

由于我们正使用新脚本建立新连接，暂时保留 debug 选项。

**警告**
如果你的磁盘空间紧张，记录 pppd 交换可能会迅速扩大你的 syslog 文件并给你造成麻烦（但要做到这一点，你必须连接失败并持续尝试好几分钟）。

一旦你确信一切正常工作，你就可以移除此选项。

如果你的 PPP 选项文件名不是 /etc/ppp/options 或 /etc/ppp/options.ttySx，请使用 pppd 的 file 选项指定文件名——例如：

```
exec /usr/sbin/pppd debug file options.myserver /dev/ttyS0 38400
```

### 测试你的连接脚本

打开一个新的 root Xterm（如果你在 X 环境下）或打开一个新的虚拟控制台并以 root 身份登录。

在这个新会话中，发出命令：

```
tail -f /var/log/messages
```

（或者你的系统日志文件）。

在第一个窗口（或虚拟控制台）中发出命令：

```
ppp-on
```

（或者你编辑后的 /usr/sbin/ppp-on 版本的名字）。如果你不在命令末尾指定 `&` 将脚本放入后台，你将无法取回终端提示符，直到 PPP 退出（当链接终止时）。

现在切回到跟踪系统日志的窗口。

你会看到类似以下内容（前提是你给 chat 指定了 `-v` 并且给 pppd 指定了 `-d`）这是 chat 脚本和响应被记录到系统日志文件中，接着是 pppd 的启动信息：

```
Oct 21 16:09:58 hwlin chat[98668]: abort on (NO CARRIER)
Oct 21 16:09:59 hwlin chat[98668]: abort on (BUSY)
Oct 21 16:09:59 hwlin chat[98668]: send (ATZ\*M)
Oct 21 16:09:59 hwlin chat[98668]: expect (OK)
Oct 21 16:10:00 hwlin chat[98668]: ATZ\*\*M
Oct 21 16:10:00 hwlin chat[98668]: OK -- got it
Oct 21 16:10:00 hwlin chat[98668]: send (ATDT722298\*M)
Oct 21 16:10:00 hwlin chat[98668]: expect (CONNECT)
Oct 21 16:10:22 hwlin chat[98668]: \*M
Oct 21 16:10:22 hwlin chat[98668]: ATDT722298\*\*M
Oct 21 16:10:22 hwlin chat[98668]: CONNECT -- got it
Oct 21 16:10:22 hwlin chat[98668]: send (\*M)
Oct 21 16:10:22 hwlin chat[98668]: expect (login)
Oct 21 16:10:23 hwlin chat[98668]: kepler login: -- got it
Oct 21 16:10:23 hwlin chat[98668]: send (harrt\*M)
Oct 21 16:10:23 hwlin chat[98668]: expect (ssword:)
Oct 21 16:10:23 hwlin chat[98668]: harrt\*M
Oct 21 16:10:23 hwlin chat[98668]: Password: -- got it
Oct 21 16:10:23 hwlin chat[98668]: send (?????\*M)
Oct 21 16:10:23 hwlin chat[98668]: expect (harrt)
Oct 21 16:10:24 hwlin chat[98668]: [harrt -- got it
Oct 21 16:10:24 hwlin chat[98668]: send (ppp\*M)
Oct 21 16:10:27 hwlin pppd[98723]: pppd 2.1.2 started by root, uid 0
Oct 21 16:10:27 hwlin pppd[98723]: Using interface ppp0
Oct 21 16:10:27 hwlin pppd[98723]: Connect: ppp0 <>->/dev/cua1
Oct 21 16:10:27 hwlin pppd[98723]: fsm_sdslat(LCP): Sent code 1, id 1.
Oct 21 16:10:27 hwlin pppd[98723]: LCP, sending Configure-Request, id 1
Oct 21 16:10:27 hwlin pppd[98723]: fsm_rconfigure(LCP): Rcvd id 1.
Oct 21 16:10:27 hwlin pppd[98723]: lcp_reqci: rcvd MRU (1500) (ACK)
Oct 21 16:10:27 hwlin pppd[98723]: lcp_reqci: rcvd ASYNCMAP (0) (ACK)
Oct 21 16:10:27 hwlin pppd[98723]: lcp_reqci: rcvd MAGICNUMBER (a098B898) (ACK)
```

