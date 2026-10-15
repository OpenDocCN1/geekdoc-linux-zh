

与此相反，*forward-path* 和 *reverse-path* 中的参数可能是区分大小写的。这些参数的解释取决于 SMTP 收件人的操作系统以及用户数据库的结构，这就是为什么小写和大写字符可能会被不同对待。

## SMTP 回复代码

在 SMTP 发送方与 SMTP 收件人之间进行通信时，发送方向收件人传输各种命令并控制整个通信过程。收件人确认消息的接收并以相应的回复代码给出命令处理的状态。只有当发送方收到前一个命令的回执后，才能开始传输下一个命令。

最常见的 SMTP 回复代码列在下表：

### Table 12-2

| Reply Code | Description |
|---|---|
| 211 | System status or system help reply. |
| 214 | Displays the help message after entering HELP |
| 220 | SMTP server ready. |
| 221 | SMTP server has closed connection. |
| 250 | Specified command has been carried out. |
| 251 | User not local; will forward to *forward-path*. |
| 354 | Start of the DATA entry. |
| 421 | SMTP service not available. |
| 450 | Requested action not taken (mailbox is already in use). |
| 451 | Requested action aborted. |
| 452 | Requested action not taken; insufficient storage space in system. |
| 500 | Syntax error, command unrecognized. |
| 501 | Syntax error in parameters or arguments. |
| 502 | Command not implemented. |
| 503 | Bad sequence of commands. |
| 504 | Command not implemented for that parameter. |
| 550 | Requested action not taken; file unavailable (e.g., mailbox not found, no access). |
| 551 | User does not exist on mail server; try *forward-path*. |
| 552 | Requested mail action aborted: storage allocation exceeded. |
| 553 | Requested action not taken: mailbox name not allowed (e.g., mailbox syntax incorrect). |
| 554 | Transaction failed. |

## Minimal SMTP Command Implementation

并非所有到目前为止介绍的命令都由每个服务器实现。某些 SMTP 命令故意不包含在某些服务器实现中以提高服务器的安全性。其中一个安全关键命令是 HELP。Wietse Venema 的 Postfix SMTP 服务器并未完全实现此命令，并且简单地对 HELP 命令以回复代码 502 作出响应（“Command not implemented”）。

以下列表显示了 SMTP 服务器必须绝对实现以提供 SMTP 通信的 SMTP 命令：

- **HELO**
- **MAIL FROM:**
- **RCPT TO:**
- **DATA**
- **RSET**
- **NOOP**
- **QUIT**

## An Example for Sending Mail with Telnet

下面的文本显示了使用端口 25 上的 telnet 会话（标准邮件服务器端口）可以轻松重建的典型日志输出示例：

```
da53:~# telnet da51.digitalairlines.com 25
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
220 da51.digitalairlines.com ESMTP Postfix
HELO da53.digitalairlines.com
250 da51.digitalairlines.com
MAIL FROM: jgoldman@digitalairlines.com
250 Ok
RCPT TO: geeko@digitalairlines.com
250 Ok
DATA
354 End data with <CR><LF>.<CR><LF>
Subject: Lorem ipsum dolor sit amet

Lorem ipsum dolor sit amet, consectetuer adipiscing elit,
sed diam nonummy nibh euismod tincidunt ut laoreet dolore
magna aliquam erat volutpat. Ut wisi enim ad minim veniam,
quis nostrud exerci tution ullamcorper suscipit lobortis
isl ut aliquip ex ea commodo consequat.
.
250 Ok: queued as 45B5116A9D
QUIT
221 Bye
Connection closed by foreign host.
da53:~#
```

## Objective 2 Manage Spam

本目标解释了以下内容：

- Use SpamAssassin
- Test SpamAssassin

### Use SpamAssassin

spamassassin（和 spamc）期望其输入来自 STDIN。

使用 SpamAssassin 的最简单方法是将其邮箱通过管道传输到命令 spamassassin：

```
da51:~# cat /var/spool/mail/root | spamassassin
```

如果您想将 SpamAssassin 与 Postfix 配置一起使用，最简单的方法是使用 Procmail。您只需要编辑三个文件：

- Create the file /etc/procmailrc with this content:

```
#LOGFILE=/tmp/procmail.log
#VERBOSE=yes

# Until now, mail is untagged, you may add rules for
# mail that must not be tagged

:0 hbfw
| /usr/bin/spamc
```

邮件在第一个过滤器规则中被管道传输到 spamc。过滤器规则的标志在下面解释：

- h. Feed the header to the pipe, file, or mail destination (default).
- b. Feed the body to the pipe, file, or mail destination (default).

