
### 表 2-3. 用于发现的常用 HTTP 端口

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

使用 `fscan` 对这些服务进行扫描非常简单。下面的示例扫描了 C 类网络中表 2-3 中的端口：

```
D:\>fscan -cp 80, 81, 88, 443 [rest of ports in Table 2-3] 8888, 9090, 10000 192.168.234.1-254
```

`Fscan v1.12 Command line port scanner.`

`Copyright 2000 (c) by Foundstone, Inc.`

`http://www.foundstone.com`

`Scan started at Fri Feb 15 15:13:33 2002`

```
192.168.234.1 80/tcp
192.168.234.34 80/tcp
192.168.234.34 443/tcp
192.168.234.34 8000/tcp
192.168.234.148 80/tcp
192.168.234.148 443/tcp
192.168.234.148 8000/tcp
```

`Scan finished at Fri Feb 15 15:14:19 2002`

`Time taken: 4826 ports in 45.705 secs (105.59 ports/sec)`

正如你从输出所示，我们发现了三个运行可能与 Web 相关的服务的服务器。显然，表 2-3 列出的列表并不完整。Web 服务可以配置为监听几乎任何可用端口。我们只推荐这种方法因为它涵盖了常见的 Web 服务，并节省了运行全 65,535 端口扫描的时间（请参见前文“服务器发现”下的相关讨论）。

### 服务器识别

服务器识别更常见地被称为指纹抓取（banner grabbing）。指纹抓取对 Web 黑客来说至关重要，因为它通常可以识别 Web 服务器软件的品牌和型号。HTTP 1.1 规范（RFC 2616）定义了服务器响应头字段，用于通信处理请求的服务器的信息。尽管 RFC 鼓励实现者出于安全考虑将此字段设置为可选选项，但目前大多数实现默认都会向该字段填充真实数据。

这是一个使用 `netcat` 工具进行指纹抓取的示例：

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

> 注意使用 `HEAD` 方法来获取服务器指纹。这是抓取指纹最直接的方法。

文本文件输入可以使用重定向字符（`<`）输入到 `netcat` 连接中——例如 `nc -vv server 80 < file.txt`。

### 攻防 Web 应用程序

如果端口扫描器支持，可以在端口扫描的同时进行指纹抓取。我们通常使用 `fscan` 配合 `-b` 开关在端口扫描时抓取指纹。以下是带有 `-b` 开关之前运行的扫描（输出已精简）：

```
D:\>fscan -bgp 80,81,88,443 [rest of ports in Table 2-3], 8888,9090,10000 192.168.234.1-254
```

```
Fscan v1.12 Command line port scanner.
Copyright 2000 (c) by Foundstone, Inc.
http://www.foundstone.com

Scan started at Fri Feb 15 16:02:09 2002
```

`192.168.234.1 80/tcp`

`192.168.234.34 80/tcp`

`HTTP/1.1 400 Bad Request [OD][0A]Server: Microsoft-IIS/5.0[0D][0A]`

`192.168.234.34 443/tcp`

`192.168.234.34 8000/tcp`

`192.168.234.148 80/tcp`

`HTTP/1.1 400 Bad Request [OD][0A]Server: Microsoft-IIS/5.0[0D][0A]`

`192.168.234.148 443/tcp`

`192.168.234.148 8000/tcp`

`Fscan` 使用 `HEAD` 方法从开放端口抓取指纹，如所示，它并不总是返回 HTTP 200。注意，它无法从 SSL 服务抓取指纹，我们将在下一节讨论这个问题。

### 处理 SSL

正如我们提到的，`netcat` 和 `fscan` 等工具无法连接 SSL 服务以抓取指纹。如何从 SSL 服务抓取指纹？

最简单的方法之一是使用本地代理拦截通信并通过 SSL 隧道到目标服务器。现在有很多这样的工具，但我们青睐 `sslproxy`。以下命令说明了如何启动 `sslproxy` 在本地端口 5000 上监听，并连接到远程服务器端口 443。使用名为 `dummycert.pem` 的证书来协商 SSL 连接（它随 `sslproxy` 一起）。

```
C:\sslproxy -l 5000 -R www.victim.com -r 443
-c dummycert.pem -p ssl123
```

`SSL: No verify locations, trying default`
`proxy ready, listening for connections`

现在我们可以在另一个命令行中，使用 `netcat` 连接到本地 5000 端口，并尝试抓取指纹信息：

### 第 2 章：分析 (Profiling)

```
C:\nc> -vv localhost 5000
localhost [127.0.0.1] 5000 (?) open
HEAD / HTTP/1.0
```

```
HTTP/1.1 200 OK
Date: Fri, 15 Feb 2002 16:47:56 GMT
Server:WebSTAR/4.2 (Unix) mod_ssl/OpenSSL/0.9.6c
Connection: close
Content-Type: text/html
```
