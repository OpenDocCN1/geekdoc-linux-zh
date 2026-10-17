
列表 130 - 使用 `tcpdump` 读取流向 `172.16.40.10` 端口 `81` 的流量，其看起来像 HTTP 数据。事实上，这些类似于 HTTP 请求的内容包含了 Basic HTTP 认证，用户名为 "Teh Forest Logger"。这是某些发生异常情况的明显信号。

为了揭开谜底的其余部分，我们需要依靠高级标头过滤。

## 4.5.3 高级标头过滤

在此处，为了检查转储文件中的请求和响应，我们希望过滤并仅显示数据包。为了做到这一点，我们寻找寻找开启了 PSH 和 ACK 标志位的数据包。在初始三次握手之后发送和接收的所有数据包都设置了 ACK 标志。PSH 标志¹⁰⁹ 用于强制立即交付数据包，通常用于交互式应用层协议以避免缓冲。

下图描述了 TCP 头部，并显示了 TCP 标志从第 14 个字节开始定义。

| 0 | 8 | 16 | 24 | 32 |
|---|---|---|---|---|
| | 源端口 | | 目的端口 |
| | 序列号 | | | |
| 确认号 | | | | |
| 数据 | C E U A P R S F | | 窗口大小 |
| 偏移 | 预留 W C R C S S Y I | | |
| | R E G K H T N N | | | |
| | 校验和 | | 紧急指针 |
| | | 选项 | | 填充 |

图 16：显示 14 字节标志的 TCP 数据包

查看图 16，我们可以看到 ACK 和 PSH 分别由第 14 字节的第四位和第五位表示：

```
CEUPRSF

WCRSSY

REGHTNN

00011000 = 十进制 24
```

列表 131 - 计算所需的位

¹⁰⁹ (BARPA Internet Program, 1981), https://tools.ietf.org/html/rfc793

PWK 2.0 版权 © Offensive Security Ltd. 保留所有权利。102

OFFENSIVE SECURITY
www.offensive-security.com

使用 Kali Linux 2.0 进行渗透测试

开启这些位将带给我们 00011000，即十进制的 24。

```
kali@kali:~$ echo "$(2#00011000)"
```

列表 132：在 bash 中将二进制位转换为十进制

我们可以将此数字通过 `'tcp[13] = 24*'` 作为显示过滤器传递给 `tcpdump`，表示我们只想看到带有 ACK 和 PSH标志位（数据包）的数据包，这些位由 tcp 头部第 14 字节的第四位和第五位（24）表示。请记住，`tcpdump` 数组索引是从零开始计算位数的，因此语法应该是 `(tcp[13])`。

这两个标志的组合有望让我们能够仅查看那些设置了 ACK 或 PSH 标志的 HTTP 请求和响应：

```
kali@kali:~$ sudo tcpdump -n 'tcp[13] = 24' -r password_cracking_filtered.pcap

06:51:20.802032 IP 208.68.234.99.60509 > 172.16.40.10.81: Flags [P], seq 1855084075-1

E..s.M@..E.C.

J..n.q......S1...

..A......GET HTTP/1.1

Host: admin.megacorpone.com

User-Agent: Teh Forest Lobster

E....@..E....

D.C.q.^...E..I?

..A......HTTP/1.1 401 Authorization Required

Date: 22 Apr 2013 12:51:20 GMT

Server: Apache/2.2.20 (Ubuntu)

WWW-Authentication: Basic realm="Password Protected Area"

Vary: Accept-Encoding

Content-Length: 48

Content-Type: text/html; charset=iso-859-1

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML/2.0//EN">

<html><head>

<title>401 Authorization Required</title>

<html><body>

<p>The server could not verify that you are authorized to access the document. Either you supplied the wrong credentials (e.g., bad password), or your browser doesn't understand how to supply the credentials.</p>

<address>Apache/2.2.20 (Ubuntu) Server at admin.megacorpone.com Port 81</address>

</body></html>
```

```
08:51:25.4432 IP 172.16.40.10.81 > 208.68.234.99.60509

E..s.M@..E.C.

J..n.q......S1...

..A......GET HTTP/1.1 

Date: 22 Apr 2013 12:51:25 GMT

Server: Apache/2.2.20 (Ubuntu)

Location: http://admin.megacorpone.com/admin/

Vary: Accept-Encoding

Content-Length: 48

Content-Type: text/html; charset=iso-859-1

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML/2.0//EN">

<html><head>

<title>301 Moved Permanently</title>

</head><h1>Moved Permanently</h1>

<p>The document has moved <a href="http://admin.megacorpone.com/admin/">here</a>.</p>

<hr>

<address>Apache/2.2.20 (Ubuntu) Server at admin.megacorpone.com Port 81</address>

</body></html>
```

列表 133 - 使用带有过滤的 tcpdump

从这里，我们的变得清晰了。我们看到了大量尝试认证 /admin 目录，这导致了 HTTP 401 回复，而最后一次尝试成功了，服务器回复了 301 响应。似乎有人访问了 megacorpone 的服务器！

### 4.5.3.1 练习

- 1. 使用 `tcpdump` 重现在端口 81 捕获流量的 Wireshark 练习。
- 2. 使用 `-X` 标志查看数据包内容。如果数据被截断，研究 `-s` 标志可能有所帮助。
- 3. 在 `password_cracking_filtered.pcap` 文件查找所有 'SYN'、'ACK' 和 'RST' 数据包。
- 4. 另一种语法可以使用更用户的过滤器来显示 ACK 和 PSH 数据包。在 `tcpdump` 手册中搜索 "flags" 以探索此语法。设计一个用于 ACK 和 PSH 数据的显示过滤器。

## 4.6 总结

在本模块中，我们演示了每个渗透者常用的实用工具，包括 Netcat、Socat、PowerShell、Wireshark 和 Tcpdump。这些工具在渗透测试过程中可以很多帮助，特别是当目标缺少专用工具或我们需要传输工具以扩展目标网络上的权限时。

# 脚本

GNU Bourne-Again Shell (Bash) 是一个强大的工作环境和脚本引擎。专业的安全人员利用 Bash 脚本来简化和自动化许多 Linux 任务和程序。在本模块中我们将介绍 Bash 脚本并探索几个实际场景。

## Bash 脚本简介

Bash 脚本是一个纯文本文件，包含了一系列命令，其执行方式就像在终端提示符处输入的一样。通常，Bash 脚本具有可选的扩展 `.sh`（为了方便识别），带有 `#!/bin/bash` 并在执行之前必须具有执行权限。让我们从一个简单的 "Hello World" 脚本开始：

```
kali@kali:~$ cat ./hello-world.sh

#!/bin/bash

# Hello World Script

echo "Hello World!"
```
