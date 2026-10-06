

## 第3章

## 枚举

+ 本章内容：
- 枚举远程服务
- 自动化Banner抓取（Banner-Grabbing）
- 总结

## 36 第一部分：黑客技术与防御

在对目标主机进行端口扫描后，入侵者将确切知道哪些主机是活跃的以及它们开放了哪些端口。有了这些信息，逻辑上的下一步是从监听特定端口的服务中枚举出各种信息，例如用户名、文件共享和操作系统版本号。只有在获取了此类信息后，攻击者才能像下一章讨论的那样，转向利用特定的漏洞。

许多远程守护进程在连接到它们监听的端口时会显示横幅消息（banner message）。横幅消息可以提供有关服务的信息，例如其身份和版本信息。从远程服务获取横幅的过程被称为Banner抓取（banner grabbing）。由于大多数守护进程允许更改其横幅，你应该利用这种能力。

虽然更改服务器横幅以混淆潜在入侵者是一个好主意，但请记住，这并不能阻止更复杂的攻击者。

## 枚举远程服务

以下是已知易受枚举攻击的服务列表。它们按照通常监听的端口号进行排序（请查看你的Unix或Linux主机上的 /etc/services 文件以获取完整列表）。

> 此处列出的任何服务都可以配置为监听非标准端口。某些服务使用非ASCII字符进行通信，很难识别。可以使用可用位于 http://www.thehackerschoice.com/releases.php 的 Amap等工具来检测服务：

```bash
$ amap -sT intranet.somecompanyasanexample.com 9934
Total amount of tasks to perform: 15
Amap1.2.1b started at Sun Mar 9 09:30:22 2003, stand back and keep the children away.
Protocol on IP 192.168.1.3 port 9934 tcp matches ssl
Protocol on IP 192.168.1.3 port 9934 tcp matches http
Unidentified ports: None.
Amap1.2.1b ended at Sun Mar 9 09:30:59 2003
```

在这个示例中，Amap 成功发现主机 `intranet.somecompanyasanexample.com` 在端口 9934 上运行HTTPS。这是一个非常有用的信息，因为HTTPS的标准端口是443。

## 阻塞并停止不必要的服务

某些服务被配置为接受来自任何IP地址的连接。例如，电子商务组织的HTTP服务器必须接受来自任何IP地址的连接，以便允许所有位置的用户查看该组织的网站。在这种情况下，组织无法隐藏他们正在运行HTTP服务器的事实。

然而，根据组织的需求和网络架构，某些服务可能只期望来自授权IP地址的连接。在这些情况下，必须建立防火墙规则以确保来自未经授权IP地址的连接被阻塞。此外，必须通过防火墙规则关闭或阻塞不必要的服务。这将防止不应被授权主机访问的服务被利用和识别。

## FTP（文件传输协议）：21 (TCP)

FTP顾顾名，是一种从一个主机向另一个主机传输文件的协议。

## 获取FTP服务器Banner

FTP服务器在连接时通常会打印版本信息。可以使用FTP客户端连接到FTP服务器以获取其横幅。例如：

```bash
$ ftp 192.168.1.1
Connected to 192.168.1.1 (192.168.1.1).
220 192.168.1.1 FTP server (Version wu-2.6.2+Sun) ready.
Name (192.168.1.1:username):
```

telnet客户端也可以直接连接到FTP端口以获取横幅信息：

```bash
$ telnet 192.168.1.1 21
Connected to 192.168.1.1.
220 192.168.1.1 FTP server (Version wu-2.6.2+Sun) ready.
```

## 修改FTP服务器Banner

如果你正在运行WU-FTPD服务器，可以编辑 /etc/ftpaccess文件或使用greeting指令来更改服务器横幅。例如：

```text
greeting No banner available.
```

## SSH（安全外壳）：22 (TCP)

SSH是一种用于交换数据的安全协议。它可以登录远程机器、执行命令并传输文件。由于SSH通信是加密的，它是telnet、rlogin和FTP的可靠替代方案。

## 获取SSH服务器Banner

尽管SSH通信是加密的，当使用telnet连接时，SSH守护进程会打印版本信息：

```bash
$ telnet 192.168.1.1 22
Trying 192.168.1.1...
Connected to 192.168.1.1.
Escape character is '^'.
SSH-1.99-OpenSSH_3.4p1
```

在上面的示例中，Banner显示的版本信息“OpenSSH_3.4p1”可以通过获取并编辑SSH源码来更改。使用grep命令在SSH源码中找到该字符串。一旦更改了该字符串，请重新编译并安装SSH。横幅还显示了协议版本“SSH-1.99”，更改此值可能会某些SSH客户端停止正常工作。

## Telnet：23 (TCP)

Telnet是用于登录远程机器的明文协议。

## 获取Telnet服务器Banner

只需telnet到服务器即可从telnet守护进程获取Banner信息：

```bash
$ telnet 192.168.1.1 23
Trying 192.168.1.1...
Connected to 192.168.1.1.
Escape character is '^]'
SunOS 5.8
login:
```

## 修改Telnet服务器Banner

为了更改telnet banner，你需要为它编写一个包装器（wrapper）。假设你正在inetd中运行telnetd，编辑你的 /etc/inetd.conf，并将

```text
telnet stream tcp nowait root /usr/sbin/in.telnetd in.telnetd
```

改为：

```text
telnet stream tcp nowait root /usr/sbin/in.telnetdwrapper in.telnetd
```

现在，你创建一个包含以下内容的 /usr/sbin/in.telnetdwrapper：

```sh
#!/bin/sh
/bin/echo "My banner\r"
exec /usr/sbin/in.telnetd
```

> 如果你使用inetd，请适当编辑xinetd.d目录下的telnet文件。必须重启inetd或xinetd才能生效。注意，某些版本的telnetd允许通过编辑 /etc/issue.net文件来更改banner信息。

## SMTP（简单邮件传输协议）：25 (TCP)

SMTP是互联网上用于传输电子邮件的协议。

## 获取SMTP服务器Banner

通过telnet到运行SMTP的主机的端口25可以获取SMTP进程banner：

```bash
$ telnet 192.168.1.1 25
Trying 192.168.1.1...
Connected to 192.168.1.1.
Escape character is '^'
220 192.168.1.1 ESMT Sendmail 8.10.2+Sun/8.10.2; Tue,
14 Jan 2003 09:28:02-0500 (EST)
```

## 修改SMTP服务器Banner

如果你使用Sendmail，可以通过编辑 /etc/sendmail.cf文件并更改SmtpGreeting字段来更改SMTP banner。

## 使用EXPN和VRFY枚举用户

EXPN和VRFY是SMTP支持的两个允许用户名枚举的命令。EXPN和VRFY可确认特定用户名的存在。EXPN可以用于枚举特定组邮件别名中所有用户的姓名和电子邮件地址。

这里是VRFY的示例：

```bash
$ telnet mail.somecompanyexample.com 25
Trying 10.0.0.11...
Connected to mail.somecompanyexample.com.
Escape character is '^'
220 mail.somecompanyexample.com ESMTP Sendmail 8.11.6/
8.11.6; Wed, 15 Jan 2003 22:04:06-0500 (EST)
VRFY smith
250 2.1.5 <smith@sales.somecompanyexample.com>
```

这里是使用EXPN的示例：

```bash
$ telnet mail.somecompanyexample.com 25
Trying 10.0.0.11...
Connected to mail.somecompanyexample.com.
Escape character is '^'
220 mail.somecompanyexample.com ESMTP Sendmail 8.11.6/
8.11.6; Wed, 15 Jan 2003 22:10:11-0500 (EST)
EXPN marketing-team
250-2.1.5 <bob@marketing.somecompanyexample.com>
```

