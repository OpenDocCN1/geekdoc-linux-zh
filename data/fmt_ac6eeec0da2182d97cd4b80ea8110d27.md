
可以使用命令行 `openssl` 工具连接到 HTTPS 服务器。与 HTTP（80 端口）发生的情况类似，可以使用诸如

```
HEAD / HTTP/1.0 [enter][enter]
```

或

```
GET / HTTP/1.0 [enter][enter]
```

这样的请求来获取横幅信息。

示例：

```
[bash]$ openssl s_client -connect:192.168.1.1:443
[已删除证书的各个项目]

HEAD / HTTP/1.0[enter]
[enter]
HTTP/1.1 200 OK
Date: Wed, 15 Jan 2003 17:59:12 GMT
Server: Apache/1.3.27 (Unix) PHP/4.2.1 mod_jk/1.2.0 mod_ssl/2.8.12 OpenSSL/0.9.6h
Content-Location: index.html.en
Vary: negotiate,accept-language,accept-charset
TCN: choice
Last-Modified: Thu, 09 May 2002 19:47:31 GMT
Accept-Ranges: bytes
Content-Length: 2673
Connection: close
Content-Type: text/html
Content-Language: en
Expires: Wed, 15 Jan 2003 17:59:12 GMT

Closed
```

### 更改 HTTPS 服务器横幅

请参阅“更改 HTTP 服务器横幅”。

## NNTPS（安全网络新闻传输协议）：563（TCP）

NNTPS 是基于 SSL（安全套接字层）的 NNTP。NNTPS 使用 SSL 来建立和维护安全通道，因此提供客户端与服务器之间的加密通信。

### 抓取 NNTPS 服务器横幅

可以使用命令行 `openssl` 工具连接到 NNTPS 服务器以获取横幅信息：

```
[bash]$ openssl s_client -connect:192.168.1.1:563
```

[已删除证书信息的各个项目]

```
200_192.168.1.1 InterNetNews NNRP server INN 1.4 22-Dec-93 ready
(posting_ok).
```

OpenSSL 可在 `http://www.openssl.org/` 获取。

### 更改 NNTPS 服务器横幅

请参阅“更改 NNTP 服务器横幅”。

## IMAPS（安全互联网消息访问协议）：993（TCP）

IMAPS 是基于 SSL（安全套接字层）的 IMAP。IMAPS 使用 SSL 来建立和维护安全通道，因此提供客户端与服务器之间的加密通信。

### 抓取 IMAPS 服务器横幅

可以使用命令行 `openssl` 工具连接到 IMAPS 服务器以获取横幅信息：

```
[bash]$ openssl s_client -connect:192.168.1.1:993
```

[已删除证书信息的各个项目]

* OK [CAPABILITY IMAP4 IMAP4rev1 LOGIN-REFERRALS AUTH=LOGIN]

localhost IMAP4rev1 2000.283 at Thu, 16 Jan 2003 03:51:56 -0500 (EST)

OpenSSL 可在 `http://www.openssl.org/` 获取。

### 更改 IMAPS 服务器横幅

请参阅“更改 IMAP 服务器横幅”。

## POP3S（安全邮局协议 3）：995（TCP）

POP3S 是基于 SSL（安全套接字层）的 POP3。POP3S 使用 SSL 来建立和维护安全通道，因此提供客户端与服务器之间的加密通信。

### 获取 POP3S 服务器横幅

可以使用命令行 `openssl` 工具连接到 POP3S 服务器以获取横幅信息：

```
(bash)$ openssl s_client -connect:192.168.1.1:995
```

[已删除证书信息的各个项目]

```
+OK QPOP (version 2.53) at 192.168.1.1 starting.
<3413.1213453134@192.168.1.1>
```

OpenSSL 可在 `http://www.openssl.org/` 获取。

### 更改 POP3S 服务器横幅

请参阅“更改 POP3 服务器横幅”。

## MySQL：3306（TCP）

MySQL 是一种流行的开源数据库软件包。它可在 `http://www.mysql.com/` 获取。

### 枚举 MySQL 版本信息

通过使用 `telnet` 客户端连接其端口，可以获取远程 MySQL 服务器的版本号：

```
(bash)$ telnet 10.0.0.1 3306
Trying 127.0.0.1...
Connected to 127.0.0.1. Escape character is `^]`.
(
3.23.45&r/3N0d*Connection closed by foreign host.
```

### 仅允许本地连接

不要允许内网外的主机连接到 MySQL 服务。确保存在防火墙规则以阻止此类连接尝试。应鼓励授权的外部用户使用 SSH 等安全隧道工具来建立远程连接。

> 虽然可以编辑 MySQL 源代码以更改连接时立即显示的版本信息，但这样做很可能会破坏许多 MySQL 客户端。

## 自动抓取横幅

Netcat 是一个使用 TCP 或 UDP 在网络连接上读写数据的工具。它可以像命令行 Telnet 客户端一样用于连接远程服务器，或者监听特定端口以接收传入连接。它还有很多其他有趣的功能，这些将在后续章节中探索。Netcat 可在 `http://www.atstake.com/research/tools/network_utilities/` 获取。

可以使用 Netcat 以如下方式抓取 SMTP 横幅：

```bash
$ nc 192.168.1.1 25
220 192.168.1.1 ESMTP Sendmail 8.10.2+Sun/8.10.2; Tue,
14 Jan 2003 09:28:02 -0500 (EST)
```

通过少量的 bash shell 编程，你可以使用 Netcat 执行自动横幅抓取。例如，考虑以下脚本（让我们称之为 *grab.bash*）：

```bash
#!/bin/bash
if [ $# -lt 1 ]
then
    echo Usage: $0 host
    exit 1
fi

while [ "$i" -lt 26 ]
do
    nc -v $1 $i < /dev/null
    i=`expr $i + 1`
    echo
done
```

该脚本由一个 `while` 循环组成，变量 `$i` 的值从 21 到 25。在 `while` 循环中，在值为 `$i`（21 到 25）的端口上建立与主机（传递给脚本的第一个参数，即 `$1`）的连接，并且 `/dev/null` 被作为输入提供给 Netcat 连接。由于 `/dev/null` 是一个不包含任何内容（空）的特殊文件，Netcat 将在抓取横幅的第一行（如果有）后立即终止。

在尝试执行上述脚本之前，必须授予执行权限：

```
[bash]$ chmod u+x ./grab.bash
```

现在运行脚本：

```
[bash]$ ./grab.bash 192.168.1.1
192.168.1.1 [192.168.1.1] 21 (ftp) open
220 192.168.1.1 FTP server (Version wu-2.6.2+Sun) ready.
221 You could at least say goodbye.

192.168.1.1 [192.168.1.1] 22 (ssh) open
SSH-1.99-OpenSSH_3.4p1

192.168.1.1 [192.168.1.1] 23 (telnet) : Connection refused

192.168.1.1 [192.168.1.1] 24 (?) : Connection refused

192.168.1.1 [192.168.1.1] 25 (smtp) open
220 192.168.1.1 ESMTP Sendmail 8.9.3/8.9.3; Fri, 17 Jan 2003
14:13:10 -0500 (EST)
```

如果需要在各种主机上执行上述脚本，你可以编写一个针对你的 `grab.bash` 脚本的封装器，如下所示：

```
#!/bin/bash

for i in `cat hosts.txt`
do
    ./grab.bash $i
    echo
done
```

![](img/77287f6ef97ef0bed6e23f6610950d06_109_0.png)
