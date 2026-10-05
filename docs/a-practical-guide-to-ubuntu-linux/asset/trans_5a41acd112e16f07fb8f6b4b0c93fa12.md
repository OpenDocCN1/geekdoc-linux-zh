
# telnet 对比 ssh

当你使用 telnet 连接到远程 UNIX 或 Linux 系统时，你会看到一个普通的文本登录提示。除非另有指定，否则 ssh 实用程序假设你在远程系统上的用户名与本地系统一致。由于 telnet 是为与非 UNIX 和 Linux 系统设计的，因此它不会做此类假设。

## telnet 不安全

每当你使用 telnet 输入敏感信息（如密码）时，这些信息都会以明文形式传输，任何监听会话的人都可以读取它们。

这两个工具的另一个区别在于，前者允许你配置许多特殊参数，例如如何处理回车或中断。在 UNIX 和 Linux 系统之间使用 telnet 时，你很少需要更改任何参数。

当你没有在命令行中指定远程主机名时，telnet 将以交互模式运行。以下示例与之前的 telnet 示例等效：

```
[bravo]$ telnet
telnet= open kudos
Trying 172.19.52.2...
Connected to kudos.example.com
Escape character is '^]'
...
```

在连接到远程系统之前，telnet 会告知你转义字符是；在大多数情况下，它是 `^]`（其中 `^` 代表 CONTROL 键）。当你按下 `CTRL-J` 时，你会进入 telnet 的交互模式。继续之前的示例：

```
[kudos]$ CONTROL-
telnet= ?
```

```
(显示帮助信息)
telnet= close
Connection closed.
[bravo]$
```

当你对 `telnet>` 提示输入问号时，telnet 会列出它的命令。该命令将结束当前的 telnet 会话并返回本地系统。若要退出 telnet 的交互模式并恢复与远程系统的通信，请在提示处按 RETURN 键。

你可以使用 telnet 访问选择提供此类服务的网站远程服务。然而，这些服务中的许多（例如美国会图书馆信息系统 LOCIS）已经迁移到了 Web。因此，你现在可以使用 Web浏览器获取相同的信息。

## 使用 telnet 连接到其他端口

默认情况下，telnet 连接到端口 23，该端口用于远程登录。然而，你可以通过指定端口号使用 telnet 连接到其他服务。除了标准服务外，互联网上许多特殊的远程服务也使用了未分配的端口号。例如，你可以使用 telnet 连接到指定端口（如 4000 或 8888）来访问名为 MUD（多用户地城或维度）的多人文本游戏。与标准协议的端口号不同，这些端口可以由游戏管理员任意选择。

telnet 不再被广泛用于登录远程系统，但它仍被广泛用作调试工具。该工具允许你直接与 TCP 服务器通信。某些标准协议非常简单，经验丰富的用户可以通过 telnet 连接到远程服务来调试问题。如果你在网络服务器上遇到问题，第一步就是尝试使用 telnet 连接到它。

在以下示例中，一个正在调试邮件投递问题的系统管理员使用 telnet 连接到 example.com 服务器上的 SMTP 端口（25 端口），以查看为什么它拒绝了来自垃圾邮件域域的邮件。输出的第一行显示了 telnet 正在尝试连接的 IP 地址。在 telnet 显示 `Connected to smpsrv.example.com` 消息后，用户遵循标准的 SMTP 协议使用 SMTP 对话。以 `hello` 开头的第一行开始会话并识别本地系统。在 SMTP 服务器回复解释了为什么邮件被拒绝后，用户使用 `quit` 结束。

```
$ telnet smpsrv.168.1.1
Trying 192.168.1.
Connected to smpsrv.example.com.
Escape character is '^A'.
hello example.com
220 smpsrv.example.com SMTP Sendmail 8.13.1/8.13.1; Wed, 4 May 2005 00:13:43 -0500 (CDT)
250 smpsrv.example.com Hello desktop [192.168.1.97], pleased to meet you
mail from:user@spam.com
+ 571 5.0.0 Domain banned for spamming
quit
221 2.0.0 smpsrv.example.com connection closing
```

telnet 实用程序允许你使用任何协议，只要你足够熟悉它并能手动输入命令。

## ftp: 在网络上传输文件

文件传输协议（FTP）是一种通过网络使用 TCP/IP 从另一个系统下载文件或上传文件的方法。FTP 不是一个安全协议；请仅将其用于从公共服务器下载公共信息。Web 浏览器可以从 FTP 服务器下载文件。第 19 章将介绍 FTP 客户端和服务器。

## ping: 测试网络连接

ping 实用程序（http://ftp.arl.ml/~mike/ping.html）向远程计算机发送一个 `ECHO_REQUEST` 数据包。该数据包会导致远程系统返回响应。这种交换是验证远程系统是否可用以及检查网络运行状况（例如速度或丢包情况）的快速方法。ping 实用程序使用 ICMP（互联网控制消息协议）协议。在不使用任何选项的情况下，ping 每执行一次通过 CONTROL-C 测试一次连接。

```
$ ping www.slashdot.org
PING www.slashdot.org (216.34.181.48) 56(84) bytes of data.
64 bytes from slashdot.org (216.34.181.48): icmp_seq=1 ttl=238 time=70.2ms
64 bytes from slashdot.org (216.34.181.48): icmp_seq=2 ttl=238 time=72.6ms
64 bytes from slashdot.org (216.34.181.48): icmp_seq=3 ttl=238 time=57.5ms
64 bytes from slashdot.org (216.34.181.48): icmp_seq=4 ttl=238 time=71.2ms
--- www.slashdot.org ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 302ms
rtt min/avg/max/mdev = 57.553/68.999/72.605/6.039ms
CONTROL-C
```

此示例显示到 www.slashdot.org 的连接已重定向到 slashdot.org，且系统是可用的。默认情况下，ping 发送包含 64 字节（55 字节数据和 8 字节协议头信息）的数据包。在前面的示例中，在用户通过 CONTROL-C 中断之前，向系统 slashdot.org 发送了四个数据包。每行括号中的四部分数字是远程系统的 IP 地址。包序列号（名为 `icmp_seq`）也会给出。如果数据包丢失，序列号中会出现间隙。往返时间已列出；它表示从发送数据包到经过的时间（毫秒）。
