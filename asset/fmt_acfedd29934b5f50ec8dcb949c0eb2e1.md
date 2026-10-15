
当作为普通用户运行时，此命令只显示该用户的进程。当作为 `root` 运行时，输出应该像这样，显示出各种进程和用户：

| COMMAND | PID | USER | FD | TYPE | DEVICE SIZE/OFF NODE NAME |
|---|---|---|---|---|---|---|---|---|
| rpcbind | 700 | root | 6 | IPv4 | 10492 | oto | UDP: *sunprpc |
| rpcbind | 700 | root | 8 | IPv4 | 10508 | oto | TCP: *sunprpc (LISTEN) |
| avahi-daemon | 872 | avahi | 13 | IPv4 | 2173675 | oto | UDP: *mdns |
| cuspd | 1010 | root | 9 | IPv6 | 4232114 | oto | TCP cp6-localhost:ipp (LISTEN) |
| ssh | 14366 | user | 3 | IPv4 | 38995911 | oto | TCP thishost.local:55457 -> |
| something.example.com:ssh | | | | | | | | |
| chromium-26534 | user | 8 | IPv4 | 42525253 | oto | TCP thishost.local:41551 -> |
| another.example.com:https | | | | | | | | |

此示例显示了顶部服务器的用户和进程 ID、多播 DNS 客户端程序、`avahi` 提供的旧式 RPC 服务以及一个支持 IPv6 的打印机服务 (`cuspd`)。最后两项显示了连接：来自 Chromium Web 浏览器的 SSL 连接和安全 Web 连接。由于输出可能非常多，通常最好应用过滤器（如节节讨论）。

`lsof` 程序就像 `netstat` 一样，它尝试将找到的每个 IP 地址反向解析为主机，这会减慢输出速度。使用 `-n` 选项禁用域名解析：

```bash
# lsof -n -i
```

你也可以指定 `-P` 来禁用 `/etc/services` 端口名查找。

### 按协议和端口过滤

如果你正在寻找某个特定的端口（例如，你知道某个进程正在使用特定端口并想知道该进程是什么），使用此命令：

```bash
# lsof -i:port
```

语法如下：

```bash
# lsof -protocol@host:port
```

协议、`@host` 和 `:port` 参数都是可选的，并将相应地过滤 `lsof` 的输出。与大多数网络工具一样，主机和端口可以是名称或数字。例如，如果你只想查看 TCP 端口 80（HTTP 端口）上的连接，请使用

```bash
# lsof -iTCP:80
```

### 按连接状态过滤

一个特别方便的 `lsof` 过滤器是连接状态。例如，要查看监听 TCP 端口的进程，输入

```bash
# lsof -iTCP -sTCP:LISTEN
```

此命令让你对当前运行的进程有一个良好的概览。然而，由于输出可能非常多，通常最好应用过滤器（如节节讨论）。

TCP/UDP 端口、指定本地端口、监听端口、扫描端口、将标准 I/O 重定向到和从网络连接，以及更多。要使用 `netcat` 向某个端口打开 TCP 连接，请运行

```bash
# $ netcat host port
```

`netcat` 只有在连接的另一端结束连接时才会终止，如果你将标准输入重定向到 `netcat`，这可能会让情况变得复杂。你可以随时通过按下 `CTRL-C` 来结束连接。（如果你想让程序和网络连接根据标准输入流终止，请尝试使用 `sock`。）

要监听某个特定端口，请运行

```bash
# $ netcat -1 -p port_number
```

## 10.5.4 端口扫描

有时你并不知道网络上的机器提供哪些服务，或者网络中包含哪些 IP 地址。网络映射器（`Nmap`）会扫描机器或机器网络上的所有端口以寻找开放端口，并列出它找到的端口。大多数发行版都包含 `Nmap` 软件包，或者你也可以从 `http://www.nmap.org/` 获取。（请查看 `Nmap` 手册页和在线资源以了解 `Nmap` 的所有功能。）

在列出你机器上的端口时，从至少两个端口运行 `Nmap` 扫描通常会有帮助：从你自己的机器和另一台机器（可能在你的本地网络之外）。这样做可以让你了解你的防火墙拦截了什么。

> 如果你要扫描你想用 `Nmap` 扫描的网络，请请求权限。网络管理员会监控端口扫描，并通常会禁用对运行扫描的机器的访问。

运行 `nmap host` 对主机进行常规扫描。例如：

```
$ nmap 10.1.2.2

Starting Nmap 5.21 ( http://nmap.org ) at 2015-09-21 16:51 PST

Nmap scan report for (0.00027 latency).

Host is up

Not shown: 993 closed ports

PORT STATE SERVICE

22/tcp open ssh

25/tcp open smtp

80/tcp open http

111/tcp open rpcbind

8800/tcp open unknown

9000/tcp open clistener

9090/tcp open zeus-admin
```

Nmap done: 1 IP address (1 host up) scanned in 0.12 seconds

如你所见，这里有许多开放的服务，其中许多在大多数发行版中默认是不开启的。事实上，这里通常默认开启的只有端口 111，即 `rpcbind` 端口。

## 10.6 远程过程调用 (RPC)

那么你在上一节扫描中看到的 `rpcbind` 服务呢？RPC 代表远程过程调用（remote procedure call），是一个驻留在应用层较低部分的系统。它的设计目的是为了让程序员更容易访问网络应用程序，这种方法利用了程序可以调用远程程序（通过程序编号识别）上的函数，而远程程序返回结果代码或消息。

RPC 实现使用 TCP 和 UDP 等传输协议，它们需要一个特殊的中间服务来将程序编号映射到 TCP 和 UDP 端口。服务器是 `rpcbind`，它必须运行在任何想要使用 RPC 服务的上。

要查看你的计算机运行的 `rpc` 服务，

```
$ rpcinfo -p localhost
```
