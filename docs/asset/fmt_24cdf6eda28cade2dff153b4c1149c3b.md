
```bash
$ traceroute -n www.google.com
traceroute to www.google.com (74.125.95.103), 30 hops max, 60 byte packets
1  192.168.1.254  3.634 ms  3.758 ms  4.511 ms
2  99.60.32.2  25.398 ms  27.472 ms  28.040 ms
3  76.196.172.4  28.261 ms  29.739 ms  28.926 ms
4  151.164.94.52  29.057 ms  29.583 ms  29.824 ms
5  69.220.8.57  39.645 ms *  40.455 ms
6  72.14.197.113  41.461 ms  39.534 ms  39.995 ms
7  72.14.233.67  39.437 ms  72.14.233.65  31.567 ms  36.633 ms
8  216.239.47.121  42.631 ms  43.298 ms  216.239.47.131 44.649 ms
...
```

使用 `traceroute` 显示 TCP/IP 数据包的路由

` traceroute` 命令用于追踪数据包在 TCP/IP 网络中经过的路径。上述示例演示了如何使用 `traceroute` 命令显示到 www.google.com 的网络路由。沿网络路径的路由器（又称跳数）会被识别，并附带响应时间（以毫秒为单位）。

> **提示** `traceroute6` 命令用于追踪 IP 版本 6 的主机。

**常见用法示例：**

| 命令 | 描述 |
|:---|:---|
| `traceroute [HOST]` | 追踪到指定主机的路由 |
| `traceroute -n [HOST]` | 追踪时不查找 DNS 名称 |

### tracepath

**用途：**在 Linux 系统上显示 TCP/IP 路由信息。

**语法：**`tracepath [OPTIONS] [HOST]`

![](img/fa2f95b64a707c963dfa0445bd9281a7_148_0.png)

`tracepath` 命令是 Linux 系统上 `traceroute` 命令的替代程序。你可以在 Linux 上使用这两个程序中的任意一个，但许多发行版默认只包含 `tracepath`。上述示例演示了如何使用 `tracepath` 显示到 www.google.com 的路由。

> **提示** `tracepath6` 命令用于跟踪 IP 版本 6 主机。

常见用法示例：

- `tracepath [HOST]`

  跟踪到指定主机的路径

- `tracepath -n [HOST]`

  在跟踪时不查找 DNS 名称

### nslookup

**用途：**在 Unix 系统上执行 DNS 查找。

**语法：**`nslookup [OPTIONS] [HOST]`

```bash
$ nslookup www.dontfeartheCommandLine.com
Server:        68.105.28.14
Address:       68.105.28.14#53

Non-authoritative answer:
Name:          dontfeartheCommandLine.com
Address:       64.202.189.170
Using the nslookup command to resolve a domain name
```

`nslookup` 命令执行 DNS 查找查询。它将 DNS 名称解析为 IP 地址，对于排查网络名称解析问题很有帮助。在上例中，解析并显示了指定主机的 IP 地址。

> **注意** `nslookup` 被视为一个遗留程序，在许多系统中已被更现代的命令（如 `dig`（见第 151 页）和 `host`（见第 152 页））所取代。

**常见用法示例：**

- `nslookup [HOST]`

  解析指定的主机名

### dig

**用途：**在 BSD 和 Linux 系统上执行 DNS 查找。

**语法：**`dig [OPTIONS] [HOST]`

```bash
$ dig dontfeartheCommandLine.com
; <<>> DiG 9.5.1-P2 <<>> dontfeartheCommandLine.com
; global options: printcmd
; Got answer:
; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 20739
; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

; QUESTION SECTION:
;dontfeartheCommandLine.com. IN A

; ANSWER SECTION:
dontfeartheCommandLine.com. 2681 IN A 64.202.189.170

; Query time: 4 msec
; SERVER: 10.10.1.4#53(10.10.1.44)
; WHEN: Mon Jun 1 05:38:40 2009
; MSG SIZE rcvd: 60
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_150_0.png)

`dig` 命令在 Linux 和 BSD 系统上执行 DNS 查询。它是 `nslookup` 命令的现代替代工具。上述示例演示了 `dig` 命令的典型用法。

常见用法示例：

- `dig [HOST]`

  显示指定主机的 DNS 信息

- `dig -t MX [HOST]`

  显示指定主机的邮件服务器

- `dig -t NS [HOST]`

  显示指定主机的名称服务器

### host

**用途：**简单的 DNS 查找工具。

**语法：**`host [OPTIONS] [HOST]`

```bash
$ host dontfeartheCommandLine.com

dontfeartheCommandLine.com has address 64.202.189.170

dontfeartheCommandLine.com mail is handled by 0 smtp.secureserver.net.

dontfeartheCommandLine.com mail is handled by 10
mailstore1.secureserver.net.

    Resolving a name using the host command
```

`host` 命令是 Unix 和 Linux 系统的简单 DNS 查找工具。它与 `nslookup` 和 `dig` 工具类似，但其输出更对用户友好，易于阅读和理解。上述示例展示了 `host` 命令产生的输出样本。

`host` 命令可以使用 `-t` 选项来查找有关域名的其他信息，如下例所示的邮件服务器（`-t MX`）和名称服务器（`-t NS`）。

```bash
$ host -t MX dontfeartheCommandLine.com

dontfeartheCommandLine.com mail is handled by 10
mailstore1.secureserver.net.

dontfeartheCommandLine.com mail is handled by 0 smtp.secureserver.net.

$ host -t NS dontfeartheCommandLine.com

dontfeartheCommandLine.com name server ns36.domaincontrol.com.

dontfeartheCommandLine.com name server ns35.domaincontrol.com.

    Resolving MX and NS records using the host command
```

常见用法示例：

| 命令 | 描述 |
| :--- | :--- |
| `host [HOST]` | 显示指定主机的 DNS 信息 |
| `host -t MX [HOST]` | 显示指定主机的邮件服务器 |
| `host -t NS [HOST]` | 显示指定主机的名称服务器 |
| `host -a [HOST]` | 显示指定主机的详细信息 |

### whois

**用途：**在 WHOIS 数据库中查找域名注册信息。

**语法：**`whois [OPTIONS] [DOMAIN]`
