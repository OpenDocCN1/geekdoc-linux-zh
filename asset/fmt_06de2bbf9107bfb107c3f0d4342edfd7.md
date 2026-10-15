
```
-rw-r--r-- 10146 sys 4005 Apr 30 1996 Makefile
-rw-r--r-- 10146 sys 4829 Dec 20 1995 README
-rw-r--r-- 10146 sys 5362 Dec 20 1995 README.OLD
-rw-r--r-- 10146 sys 892 Jun 2 1995 TODO
-rw-r--r-- 10146 sys 2345 May 2 1996 VERSION
drwxr-xr-x 2 10146 sys 9 Jul 7 04:16 bin/
drwxr-xr-x 2 10146 sys 4096 Jul 7 04:16 ftp/
drwxr-xr-x 2 10146 sys 4096 Jul 7 04:16 fptpd/
drwxr-xr-x 3 10146 sys 41 Jul 7 04:16 lib/
```

接下来，打开 `(/SSLftp-0.8/)` 中的 `Makefile`，找到第 42 行并找到 `SSLTOP` 变量：

```
# the location where SSLeay is installed ...
# - expect a include and lib directory under here
SSLTOP=/usr/local/ssl
```

如果这不是你安装 SSLeay 的位置，你需要更改此值。`SSLeay` 默认安装到 `/usr/local/ssl`。

接下来，如果你没有使用 `SOCKS`，请注释掉下述部分的第 50 到 53 行：

```
# Decide if you want SOCKS support (which I haven't put into
# - the ftp client yet)
sockslib=
socksflags=
sockslib=/usr/local/lib/lib/socks.a
socksflags=-.DUSE_SOCKS
```

最后，取消 Linux 的两行

```
#CC = gcc -DLINUX $(socksflags)
#LDADD = $(sockslib)-lsbsd
```

从这里开始，你不应该遇到任何问题。首先，编译 `SSLftp`：

```
make ftp
```

然后编译 `SSLftppd`：

```
make ftpd
```

最后，安装包：

```
make install
```

现在，你准备好使用 `SSLftp` 了。

## 特定 FTP 应用安全

最后，以下章节将涉及值得提及的 FTP 相关的特定应用程序问题，包括影响：

- `ncftp`

- `filerunner`

- `ftftpd`

- `wu-ftpd 2.4.2-academ[BETA-18]`

### ncftpd

`ncftpd` 包带有 Linux FTP 服务器和客户端，它们提供了至少基本的会话支持。然而，`ncftpd` 流行主要是因为它减少了服务器负载并为更多用户服务。

`ncftp` 版本 2.0.0 和 2.4.2（可能还有其他版本）受到远程 FTP 服务器的攻击。远程 FTP 管理员可以在服务器上创建一个目录，导致远程执行取消执行。要确定你的系统是否存在漏洞，请访问 `http://www.open..com/security`。最后，`ncftp` 版本 3.4 (`libc5`) 也存在漏洞。除了存储和转发外，还存在其他结果。如果 `SMTP` 服务器发现邮件不可接受（目标账户超出配额或其用户不存在），`SMTP` 将向发送者返回错误消息以说明问题。

### filerunner

`Filerunner` 是一个图形化客户端。像 `telnet` 一样，`FTP`（或类似 `FTP`）是 Linux 必不可少的。每天使用 `SMTP` 传输消息。

### ftpwatch

通常，邮件在到达目的地之前会通过多个 `SMTP` 网关。例如，有一个来自 Macmillan Publishing 发送的邮件部分头部：

```
Received: from [198.70.148.65] HELO carmfw01.mcp.com)

by ag.ohio-state.com (CommuniGate SMTP 3.0)

with SMTP ID 1782539 for jray@postoffice.ag.io-state.edu;

--Fri, 09 Jul 1999 10:43:06 -0400

Received: from net1-167.mcp.com by carmfw01.mcp.com

via smtpd (for postoffice.ag.io-state.edu) [140.254.85.38])

--with SMTP; 9 Jul 1999 14:56:02 UT
```

### wu-ftpd

如前所述，`wu-ftpd` 是 Linux 的默认选择。每天使用 `SMTP` 传输消息。

# 邮件安全

第 12 章

难以置信的是，尽管 `SMTP` 服务器在消息评估和传输过程中做出了许多决策，但电子邮件只需几秒钟就能环绕全球。此外，尽管 `SMTP` 的内部操作具有内在复杂性，但从外部来看非常用户友好，即使你是在原始层面与其交互。

事实上，你不需要使用任何特殊的邮件客户端与 `SMTP` 服务器通信。相反，你可以直接通过 `telnet` 会话连接 25 端口，使用近乎纯英语的语言进行交互。表 12.1 总结了常用的原始 `SMTP` 命令。

## 表 12.1 SMTP 命令

| 命令 | 用途 |
| --- | --- |
| DATA | 使用此命令指定接下来的文本行为邮件正文。通过发送一个只有一个句点的行来表示消息结束。 |
| EXPAND | 使用此命令将用户名扩展为完全限定的电子邮件地址。 |
| HELO (HELLO) | 使用此命令启动 `SMTP` 会话并交换标识数据。 |
| HELP | 使用此命令获取 `SMTP` 帮助。 |
| MAIL | 使用此命令启动邮件事务。 |
| QUIT | 使用此命令结束当前会话并关闭连接。 |
| RCPT (RECIPIENT) | 使用此命令指定收件人。 |
| RESET | 使用此命令中止当前操作。 |
| SEND | 使用此命令启动传输。 |
| VERIFY | 使用此命令验证用户名。 |

一个典型的会话：

```
[jray@pointy jray$ telnet postoffice.ag.ohio-state.edu 25
Trying 149.254.25.36...
Connected to postoffice.ag.ohio-state.edu...
Escape character is '^'
220 postoffice.ag.ohio-state.edu SMTP Sendmail 8.9.3/8.9.3;
Sat, 10 Jul 1999 10:32:13 -0400
HELO meine.ag.ohio-state.edu Hello IDENT:
>250 MAIL:<jray@NEW93119226.columbus.rr.com [24.93.119.226],
>pleased to meet you
```

- 要了解更多关于 `SMTP`、其命令及其通用规范，请参阅 `RFC 821`，地址为 `http://www.freesoft.org/CIE/RFC/821/12.htm`。

## Linux 网络安全

第四部分

```
MAIL FROM: jray@poisonontooth.com

250 jray@poisonontooth.com... Sender ok

RCPT TO: root@meine.ag.ohio-state.edu

250 root@meine.ag.ohio-state.edu... Recipient ok

DATA

354 Enter mail, with "." on a line by it

This is a test

250 KAA01845 Message accepted for delivery

quit

221 postoffice.ag.ohio-state.edu closing connection
```

这个会话揭示了一个令人不安的事实：`SMTP` 服务器默认情况下信任任何人。用户可以指定任何他们喜欢的回信地址，而 `SMTP` 服务器会尽职尽地使用这个伪造地址处理邮件。

注意

用户可以在 `Eudora`、`Outlook` 或其他邮件客户端通过更改用户信息在应用程序级别执行此操作。然而，直接与 `SMTP` 服务器会话可以为你提供自动化这一过程的机会。从典型客户端发送几封诚恳的邮件，远比在几分钟内从“`Nasty Nikki`”发送几十万封邮件要少烦人得多。此外，通过直接与 `SMTP` 服务器交互，如果攻击者选择一个已经被攻破的服务器，他们将获得几乎完全匿名的优势。

# 一个简单的 SMTP 客户端

下面的 `Perl` 代码是我几年前编写的一个 `TCP/IP` 客户端库。与其他邮件客户端不同，这段代码是一个与 `SMTP` 服务器交互的初级邮件客户端。我办公室附近的一个程序（被称为 "`supermail`”）允许你指定发件人的姓名、电子邮件地址以及收件人。
