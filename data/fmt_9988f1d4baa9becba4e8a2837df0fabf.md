
本节检查了诸种流行的远程访问方法，如 `Telnet`。它还包含了广为人知的安全漏洞和缺陷，这些漏洞导致了安全远程访问系统（如 `SSH`）的创新。这些“安全”系统通过对用户会话和认证序列进行加密，为敏感数据提供了重要的保护。尽管远程访问非常有用，但确保 `Solaris` 系统的管理开销可能很大，这反映了远程访问服务所提供的功能不断增加。

![](img/11bcccd1804574cca0c3018732958dd5_238_0.png)

## 第三部分：安全

### Telnet

`Telnet` 是使用原始 `DARPA Telnet` 协议从客户端登录到 `Solaris` 机器的标准远程访问工具。此外，在支持 `TCP/IP` 的操作系统上可以使用 `Java Telnet` 客户端（[http://erp.stanford.edu/binaries.html]），它在任何具有原生运行 `Java` 或作为插件运行浏览器的操作系统上都支持。`Telnet` 是一个终端类程序，允许用户交互式访问其所选的登录 `shell`（例如 `C-shell`，或 `csh`）。大多数 `Telnet` 支持 `VT100` 或 `VT220` 终端仿真。登录 `shell` 可用于执行脚本、开发应用程序以及读取电子邮件和新闻——简而言之，一个 `Solaris` 环境应向用户提供的所有功能都可以提供，除了 `X11` 图形和 `Open Windows`，以及最近常见的桌面环境（`CDE`）。许多组织中的一种常见安排是，`Solaris` 服务器位于建筑的安全区域，且仅允许 `Telnet` 访问。

`Telnet` 会话期间发生的事件序列始于客户端向服务器发起的连接请求。服务器要么通过显式接受或拒绝连接做出响应（或超时）。拒绝的发生可能是因为服务器上通常接受 `Telnet` 客户端连接的端口被数据包过滤器或防火墙拦截。如果连接被接受，客户端将被要求输入用户名，然后是密码。如果用户名和密码组合有效，将产生一个 `shell` 并登录用户。这一系列事件如图 9-2 所示。

![](img/11bcccd1804574cca0c3018732958dd5_239_0.png)

图 9-1 客户端/服务器的典型远程访问拓扑

`Telnet` 连接的标准端口是 23。因此，像这样的命令，

```
$ telnet server
```

会被扩展为有效命令：

```
$ telnet server
```

这意味着 `Telnet` 可以用作访问几乎任何端口服务的工具。`Telnet` 由超级守护进程（`inetd`）控制。在 `/etc/services` 中有一条条目，它定义了 `Telnet` 服务的端口，如下所示：

```
telnet             23/tcp
```

配置文件 `/etc/inetd.conf` 还包含了 `inetd` 提供的服务的重要细节。`telnet` 守护进程的位置和属性在此处标识：

```
tcp /usr/sbin/telnetd
```

在这种情况下，你可以看到 `inetd` 通过使用封装器（`wrappers`）受到保护，这有助于通过 `syslog` 设施记录 `Telnet` 访问。由于 `inetd` 存在一些安全和性能问题（这些问题在近年来已得到修复），导致管理员避开使用它。例如，应用程序（http://www.apache.org）作为独立守护进程运行。

## 漏洞

`Telnet` 系统一个遗憾的缺点是用户名（尤其是未加密的密码）在网络上以明文传输。因此，如果你从巴黎的网吧使用 `Telnet` 客户端连接到纽约的服务器，你的流量可能会经过 20 到 30 个路由器和计算机，所有这些被程序用于“嗅探”网络数据包的内容。从 `AT&T` 到 `Sun` 网页的数据包传输路径的 `traceroute` 示例所示：

```
$ traceroute www.sun.com
Tracing route to weeast.usec.sun.com [192.49.30.1]
over a maximum of 30 hops:
1  184 ms 142 ms 202 ms 202.10.4.131
2  147 ms 144 ms 138 ms 202.10.4.129
3  150 ms 142 ms 144 ms 202.10.1.73
4  150 ms 144 ms 141 ms ia4.optus.net.au [202.139.32.17]
5  148 ms 143 ms 139 ms 202.139.1.97
6  490 ms 489 ms 474 ms sf1.optus.net.au [192.65.89.246]
7  526 ms 480 ms 485 ms gn.cwix.net [207.124.109.57]
8  494 ms 480 ms 482 ms core7.SanFrancisco.cw.net [204.70.10.99]
9  483 ms 489 ms 484 ms core2.SanFrancisco.cw.net [204.70.1.132]
10 557 ms 552 ms 561 ms xcore3.Boston.cw.net [204.70.150.81]
11 566 ms 572 ms 554 ms sun.Boston.cw.net [204.70.179.102]
12 577 ms 574 ms 558 ms weeast.usec.sun.com [192.49.9.30]
```

跟踪完成。
