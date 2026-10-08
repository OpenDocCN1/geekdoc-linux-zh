

# 攻防 Web 应用程序

来自目标服务器的 ICMP 响应。如果收到 ICMP 不可用（Unreachable）响应，扫描器会将该服务解释为不可用。如果没有收到响应，扫描器则假设该端口是开放的。这种 UDP 扫描方法在连接互联网的网络上会导致假正报，因为 ICMP 不可用消息通常会被路由器丢弃。执行 UDP 扫描的更好方法是实际记录来自远程 UDP 服务的有效响应。然而，这需要扫描器理解每个 UDP 服务的工作原理、如何生成有效请求以及如何提供有效响应。对于我们在表 2-2 中指定的六个服务来说，这并不困难，但截至本文编写时，我们不知道除了 Foundation 的 FindScan 技术外，还有任何实现这种方法的 UDP 扫描工具。

好了，我们打赌你已经到了可以获取扫描工具的阶段了。我们的工具包括 Foundation 的 fscan 以及久誉的 nmap，它们都可以通过本章结尾“参考文献和延伸阅读”部分列出的 URL 免费获取。fscan 和 nmap 都支持我们在本节讨论的所有扫描技术（fscan 不支持 SYN 扫描）。我们将在接下来的服务发现章节中介绍这些工具的具体用法。

# 处理虚拟服务器

可能影响服务器发现结果的一个问题是负载均衡和虚拟服务器。

我们在第 1 章中讨论了负载均衡，这是大型 Web 网站采用的架构。如果多个服务器扫描规范名称（canonical name），结果将不会包含池中每个服务器的数据，而是仅包含扫描时排队响应的那一个。后续扫描可能会被定向到其他服务器。

这对于 Web 应用程序的安全审查并不一定是障碍，因为我们只对池中每个单独服务器的安全感兴趣。然而，全面的审查将考虑这一因素。一粒坏掉就坏了一整桶水。识别单个负载均衡服务器的一种简单方法是：首先识别规范名的 IP 地址，然后扫描该地址周围的一范围 IP。例如，你可以像这样 ping 规范名：

```
C:\ping victim.com [192.168.10.15] with 32 bytes of data:
```

```
Request timed out.
Request timed out.
[etc.]
```

# 第 2 章：特征分析

现在，使用 fscan 针对表 2-1 列出的端口之一，对解析出的规范服务器周围的 IP 范围进行扫描：

```
C:\>fscan -qp 80 192.168.10.15-100
Scan v1.12 - Command line port scanner.
Copyright 2000 (c) by Foundstone, Inc.
http://www.foundstone.com
```

Scan started at Thu Feb 14 20:32:33 2002

+   - 192.168.10.17 80/tcp
- 192.168.10.18 80/tcp

注意，我们使用了 fscan 的 `q` 静音模式开关，它不会尝试先 ping 目标地址。我们启动了该范围内的其他几台服务器，它们可能都是负载均衡且完全相同的服务器。然而，我们经常会在池中遇到一个或多个与其它服务器不同的服务器，它们运行着过时的软件版本，或者运行着如 SSH 这样的服务。通常可以很有把握地认为，这些服务器存在配置错误，可以通过它们的 IP 地址进行单独攻击。另一个需要考虑的因素是虚拟服务器。某些托管公司尝试在同一台机器上运行不同的 Web 服务器。请注意，扫描结果显示有大量活动服务器，实际上可能是一台具有多个 IP 地址的单机。

# 服务发现

一旦确定了服务器，就是弄清楚哪些端口运行着 HTTP（视情况而定 SSL）了。我们将这一过程称为服务发现，它是对 Web 服务发现中常用的端口列表进行端口扫描，并确定与之关联最密切的服务。注意，这些端口中的许多是基于 Web 的管理界面，我们将在第 1 章中详细讨论。

## 表 2-3. 用于发现的常用 HTTP 端口

| 端口 | 典型 Web 服务 |
| :--- | :--- |
| 80 | 世界标准 |
| 81 | Alternate WWW |
| 88 | Alternate WWW (Kerberos) |
| 443 | HTTP over SSL (https) |
| 900 | IBM Websphere |
| 2301 | Compaq Manager |
| 2381 | Compaq Manager over SSL |
| 4242 | Microsoft Application |
| 7001 | BEA Web |
| 7002 | BEA Web over SSL |
| 7070 | Sun Java Server over SSL |
| 8000 | Alternate server, or Web cache |
| 8001 | Alternate server or management |
| 8005 | Apache Tomcat |
| 8080 | Alternate server, or Squid (cachemgr.cgi), or Sun Java |
| 8100 | All Altaire |
| 8810, 8820, 8830, and so on belonging to Dynamo |
| 8888 | Alternate server |
| 9090 | Sun Java Server admin |
| 10000 | Netscape interface |

使用 fscan 对这些服务进行扫描非常简单。下面的示例扫描了 C 类网络中表 2-3 中的端口：

```
D:\>fscan -cp 80, 81, 88, 443 [rest of ports in Table 2-3] 8888, 9090, 10000 192.168.234.1-254
```

Fscan v1.12 Command line port scanner.
Copyright 2000 (c) by Foundstone, Inc.
http://www.foundstone.com

Scan started at Fri Feb 15 15:13:33 2002

```
192.168.234.1 80/tcp
192.168.234.34 80/tcp
192.168.234.34 443/tcp
192.168.234.34 8000/tcp
192.168.234.148 80/tcp
192.168.234.148 443/tcp
192.168.234.148 8000/tcp
```

Scan finished at Fri Feb 15 15:14:19 2002
Time taken: 4826 ports in 45.705 secs (105.59 ports/sec)

正如你从输出所示，我们发现了三个运行可能与 Web 相关的服务的服务器。显然，表 2-3 列出的列表并不完整。Web 服务可以配置为监听几乎任何可用端口。我们只推荐这种方法因为它涵盖了常见的 Web 服务，并节省了运行全 65,535 端口扫描的时间（请参见前文“服务器发现”下的相关讨论）。

# 服务器识别

服务器识别更常见地被称为指纹抓取（banner grabbing）。指纹抓取对 Web 黑客来说至关重要，因为它通常可以识别 Web 服务器软件的品牌和型号。HTTP 1.1 规范（RFC 2616）定义了服务器响应头字段，用于通信处理请求的服务器的信息。尽管 RFC 鼓励实现者出于安全考虑将此字段设置为可选选项，但目前大多数实现默认都会向该字段填充真实数据。
这是一个使用 netcat 工具进行指纹抓取的示例：

```
D:\nc -nnv 192.168.234.34 80 ([]) open
(UNKNOWN) [192.168.234.34] 80 (?)
HEAD / HTTP/1.0
[Two carriage returns]
HTTP/1.1 200 OK
Server: Microsoft-IIS/5.0
Date: Fri, 04 Jan 2002 23:55:58 GMT
[etc.]
```

> 注意使用 HEAD 方法来获取服务器指纹。这是抓取指纹最直接的方法。

文本文件输入可以使用重定向字符（<）输入到 netcat 连接中——例如 `nc -vv server 80 < file.txt`。

# 攻防 Web 应用程序

如果端口扫描器支持，可以在端口扫描的同时进行指纹抓取。我们通常使用 fscan 配合 `-b` 开关在端口扫描时抓取指纹。以下是带有 `-b` 开关之前运行的扫描（输出已精简）：

```
D:\>fscan -bgp 80,81,88,443 [rest of ports in Table 2-3], 8888,9090,10000 192.168.234.1-254
```

```
Fscan v1.12 Command line port scanner.
Copyright 2000 (c) by Foundstone, Inc.
http://www.foundstone.com

Scan started at Fri Feb 15 16:02:09 2002

```
192.168.234.1 80/tcp
192.168.234.34 80/tcp
HTTP/1.1 400 Bad Request [OD][0A]Server: Microsoft-IIS/5.0[0D][0A]
192.168.234.34 443/tcp
192.168.234.34 8000/tcp
192.168.234.148 80/tcp
HTTP/1.1 400 Bad Request [OD][0A]Server: Microsoft-IIS/5.0[0D][0A]
192.168.234.148 443/tcp
192.168.234.148 8000/tcp
```

Fscan 使用 HEAD 方法从开放端口抓取指纹，如所示，它并不总是返回 HTTP 200。注意，它无法从 SSL 服务抓取指纹，我们将在下一节讨论这个问题。

# 处理 SSL

正如我们提到的，netcat 和 fscan 等工具无法连接 SSL 服务以抓取指纹。如何从 SSL 服务抓取指纹？

最简单的方法之一是使用本地代理拦截通信并通过 SSL 隧道到目标服务器。现在有很多这样的工具，但我们青睐 sslproxy。以下命令说明了如何启动 sslproxy 在本地端口 5000 上监听，并连接到远程服务器端口 443。使用名为 `dummycert.pem` 的证书来协商 SSL 连接（它随 sslproxy 一起）。

```
C:\sslproxy -l 5000 -R www.victim.com -r 443
-c dummycert.pem -p ssl123
```

SSL: No verify locations, trying default
proxy ready, listening for connections

现在我们可以在另一个命令行中，使用 netcat 连接到本地 5000 端口，并尝试抓取指纹信息：

