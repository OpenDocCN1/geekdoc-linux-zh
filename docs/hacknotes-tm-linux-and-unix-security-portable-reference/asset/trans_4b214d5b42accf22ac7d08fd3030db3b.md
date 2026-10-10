
## 使用 nmap 进行操作系统指纹识别

nmap 程序也可以被入侵者用来通过 `-O` 标志进行操作系统指纹识别：

```bash
# nmap -O 192.168.1.1

Starting nmap V. 3.00 ( www.insecure.org/nmap/ )
Interesting ports on (192.168.1.1):
(The 1597 ports scanned but not shown below are in state: closed)
Port          State     Service
22/tcp        open      ssh
80/tcp        open      http
113/tcp       open      auth
6000/tcp      open      Xl1

Remote operating system guess: Linux Kernel 2.4.0 - 2.5.20
Uptime 6.584 days (since Sun Oct 27 10:23:37 2002)

Nmap run completed -- 1 IP address (1 host up) scanned in 8 seconds
```

## 摘要

可以通过 Ping 主机来快速判断它们是否存活。此外，可以使用各种端口扫描技术来确定存活主机上哪些端口是开放的。然后，可以使用操作系统指纹识别工具来识别目标主机上的操作系统版本。一旦入侵者遵循了这种方法论，他或她就可以继续进行下一章中描述的**用户名和服务枚举**过程。

# 第 3 章

# 枚举

本章内容：

-   枚举远程服务
-   自动横幅获取
-   摘要

在对目标主机执行端口扫描后，入侵者将确切知道哪些主机是存活的，以及它们开放了哪些端口。有了这些信息，合乎逻辑的下一步是从监听特定端口的服务中枚举信息，例如用户名、文件共享以及操作系统和应用程序的版本号。只有在获取了这些信息后，攻击者才能继续利用下一章中讨论的特定漏洞。

许多远程服务守护进程在连接到其监听端口时会显示横幅消息。横幅消息可以提供有关服务的信息，例如它们的身份和版本信息。从远程服务获取横幅的过程被称为*横幅获取*。由于大多数守护进程允许修改其横幅，你应该利用这一功能。

> 虽然修改服务器横幅以混淆潜在入侵者是个好主意，但请记住，这不会阻止更高级的攻击者。

# 枚举远程服务

以下列出了已知存在枚举漏洞的服务。它们按照通常监听的端口号进行排序（请参阅 Unix 或 Linux 主机上的 `/etc/services` 文件以获取完整列表）。

### 使用 Amap 识别远程服务

此处列出的任何服务都可以配置为监听非标准端口。一些服务使用非 ASCII 字符进行通信，因此手动识别起来很困难。可以使用 Amap 等工具（可在 <http://www.thehackerschoice.com/releases.php> 获取）来确定此类服务：

```bash
[bash]$ amap -sT intranet.somecompanyasanexample.com 9934
Total amount of tasks to perform: 15
Amap v1.2.1b started at Sun Mar  9 09:30:22 2003, stand back and keep the children away.
Protocol on IP 192.168.1.3 port 9934 tcp matches ssl
Protocol on IP 192.168.1.3 port 9934 tcp matches http
Unidentified ports: None.
Amap v1.2.1b ended at Sun Mar  9 09:30:59 2003
```

在这个例子中，Amap 成功发现主机 *intranet.somecompanyasanexample.com* 在 9934 端口上运行 HTTPS。这是一个有用的信息，因为 HTTPS 的标准保留端口是 443。

### 阻止和停止不必要的服务

某些服务被配置为接受来自任何源 IP 地址的连接。例如，电子商务组织的 HTTP 服务器必须接受来自任何 IP 地址的连接，以便允许位于所有地区的远程用户查看该组织的网站。在这种情况下，组织无法隐藏其正在运行 HTTP 服务器的事实。

然而，根据组织的要求和网络架构，某些服务可能只期望来自授权 IP 地址的连接。在这种情况下，应该实施防火墙规则，以确保阻止来自未授权 IP 地址的连接。此外，必须关闭或通过防火墙规则阻止不必要的服务。这将防止不应被未授权远程主机访问的服务被利用和识别。

### FTP（文件传输协议）：21 (TCP)

顾名思义，FTP 是一种将文件从一台主机传输到另一台主机的协议。

#### 获取 FTP 服务器横幅

FTP 服务器在连接时通常会打印版本信息。可以使用 FTP 客户端连接到 FTP 服务器以获取其横幅。例如：

```
(bash)$ ftp 192.168.1.1
Connected to 192.168.1.1 (192.168.1.1).
220 192.168.1.1 FTP server (Version wu-2.6.2+Sun) ready.
Name (192.168.1.1:username):
```

也可以使用 telnet 客户端直接连接到 FTP 端口以获取横幅信息：

```
(bash)$ telnet 192.168.1.1 21
Trying 192.168.1.1...
Connected 192.168.1.1.
Escape character is '^'.
220 192.168.1.1 FTP server (Version wu-2.6.2+Sun) ready.
```

如果你正在运行 WU-FTPD 服务器，请编辑 `/etc/ftpaccess` 文件并使用 `greeting` 指令更改服务器横幅。例如：

```
greeting text No banner information available. Sorry.
```

SSH 是一种用于交换数据的安全协议。它可以用于登录远程机器、远程执行命令以及传输文件。由于 SSH 内部通信是加密的，它是 telnet、rlogin 和 FTP 等远程登录方案的有价值替代方案。

尽管 SSH 通信是加密的，但 SSH 守护进程在使用 telnet 客户端连接时会以明文打印版本信息：

```
[bash]$ telnet 192.168.1.1 22
Trying 192.168.1.1....
Connected to 192.168.1.1.
Escape character is '^]'.
SSH-1.99-OpenSSH_3.4p1
```

在前一个例子中，横幅显示的版本信息 “OpenSSH_3.4p1” 可以通过获取并编辑 OpenSSH 源代码进行更改。使用 `grep` 命令在获取的 OpenSSH 源代码中查找版本字符串。一旦更改了这个字符串，重新编译并重新安装 OpenSSH。

> 横幅还显示了前一个例子中的协议版本信息 “SSH-1.99”。不要更改或删除此信息，因为 SSH 客户端使用此字符串来识别协议和服务器信息。更改此值可能会导致某些 SSH 客户端无法正常工作。

Telnet 是一种用于登录远程机器的明文协议。

### 获取 Telnet 服务器横幅

可以通过简单地 telnet 到服务器来获取 telnet 守护程序的横幅信息：

```
[bash]$ telnet 192.168.1.1
Trying 192.168.1.1...
Connected to 192.168.1.1.
Escape character is '^}'.

SunOS 5.8
login:
```

### 更改 Telnet 服务器横幅

为了更改 telnet 横幅，你需要编写一个包装器。假设你正在使用 inetd 运行 telnetd，请编辑你的 `/etc/inetd.conf`，并更改

```
telnet stream tcp nowait root /usr/sbin/in.telnetd in.telnetd
to
telnet stream tcp nowait root /usr/sbin/in.telnetdwrapper in.telnetd
```

现在，你必须创建文件 `/usr/sbin/in.telnetdwrapper`，内容如下：

```
#!/bin/sh
/bin/echo "My banner\r"
exec /usr/sbin/in.telnetd
```

> 如果你使用的是 xinetd，请在 xinetd.d 目录中找到并相应地编辑 telnet 文件。

为了使更改生效，你必须重新启动 inetd 或 xinetd。

请注意，某些版本的 telnetd 允许通过编辑 `/etc/issue.net` 文件来更改横幅信息。

### SMTP（简单邮件传输协议）：25 (TCP)

SMTP 是一种在互联网上用于传输电子邮件消息的协议。

#### 获取 SMTP 服务器横幅

可以通过 telnet 到运行 SMTP 的主机的 25 端口来获取 SMTP 守护程序的横幅：

```bash
$ telnet 192.168.1.1 25
Trying 192.168.1.1 ...
Connected to 192.168.1.1.
Escape character is '^]'.
220 192.168.1.1 ESMTP Sendmail 8.10.2+Sun/8.10.2; Tue,
14 Jan 2003 09: 28:02-0500 (EST)
```

#### 更改 SMTP 服务器横幅

如果你使用的是 Sendmail，可以通过编辑 `/etc/sendmail.cf` 文件并更改 `SmtgreetingMessage` 字段的值来更改 SMTP 横幅。

#### 使用 EXPN 和 VRFY 枚举用户

EXPN 和 VRFY 是 SMTP 支持的两个命令，允许进行用户名枚举。EXPN 和 VRFY 可用于确认特定用户名的存在。EXPN 还可用于枚举特定组邮件别名中所有用户的名称和电子邮件地址。

这是一个使用 VRFY 的例子：

```bash
$ telnet mail.somecompanyasanexample.com 25
Trying 10.0.0.11 ...
Connected to mail.somecompanyasanexample.com.
Escape character is '^]'.
220 mail.somecompanyasanexample.com ESMTP Sendmail 8.11.6/
8.11.6; Wed, 15 Jan 2003 22:04:06 -0500 (EST)
VRFY smith
250 2.1.5 <smith@sales.somecompanyasanexample.com>
```

这是一个使用 EXPN 的例子：

```bash
$ telnet mail.somecompanyasanexample.com 25
Trying 10.0.0.11 ...
Connected to mail.somecompanyasanexample.com.
Escape character is '^]'.
220 mail.somecompanyasanexample.com ESMTP Sendmail 8.11.6/
8.11.6; Wed, 15 Jan 2003 22:10:11 -0500 (EST)
EXPN marketing-team
250-2.1.5 <bob@marketing.somecompanyasanexample.com>
```

