
存储在`/usr/sbin/`中的文件是`pppd`，即 PPP 守护进程；`pppdump`，一个数据包转储实用程序；以及`pppstats`，一个报告给定 PPP 接口统计信息的实用程序。

安装时存储在`/etc/ppp/`中的文件有`chap-secrets`和`pap-secrets`，其中包含用户和身份验证信息；`ip-up`和`ip-down`，它们是接口脚本；以及`options`，它定义了`pppd`的行为。`pppd`支持100多个选项，保证与几乎任何 PPP 实现的互操作性。值得庆幸的是，大多数当前一代的 PPP 都支持标准要求，即选项需要协商。因此许多选项并非必需。然而，一些更常见的选项在表7.4中给出。

## 表 7.4 pppd 选项

| Option | Description |
|---|---|
| `auth` | 要求对端进行身份验证。如果 Linux 节点已定义默认路由，则假定`auth`参数或“default”。如果 Linux 节点没有默认路由并且未指定`auth`或`noauth`，`pppd`将不要求身份验证；但对端必须具有 Linux 节点当前没有路由条目的网络中的 IP 地址。 |
| `call name` | 告诉`pppd`从`/etc/ppp/peers/name`读取其选项。这对于支持连接到多个站点非常有用。 |
| `connect script` | 指示`pppd`使用给定的脚本（或可执行文件）与串行端口和调制解调器通信。 |
| `crtscts` `no crtscts` | 打开和关闭硬件流控制。如果未指定，则不会更改流控制。 |
| `defaultroute` | 导致节点为远程对端创建默认路由条目。当连接至 Internet 或作为 LAN 连接到中央远程访问服务器的最后手段路由时，这通常是期望的行为。 |
| `file file` | 指示`pppd`从`file`读取配置参数。参数在文本文件中每行输入一个。 |
| `lock` | 指示`pppd`锁定串行端口以供其独占使用。 |
| `Local IP:Remote IP` | 本地和远程 PPP 接口可以通过在两个地址之间放置冒号 (`:`) 来指定。 |
| `debug` | 向`syslog`设施打开额外的调试信息。 |

### 表 7.4 继续

| Option | Description |
|---|---|
| `demand` | 指示`pppd`以按需拨号方式运行。如果发送了到远程站点的流量，`pppd`将自动在无需用户交互的情况下启动连接。这是网络网关的期望行为。 |
| `require-chap` `require pap` | 要求对端使用指定的选项进行身份验证。 |

## 运行 pppd

`pppd`可用于启动到远程站点的连接或等待来自远程站点的连接。当`pppd`用于连接到远程站点时，称为客户端操作，而当用于侦听连接时，则称为服务器。 （请记住，这种客户端/服务器模型源于客户端发起会话的想法；从协议角度来看，两个节点是对等节点，而不是客户端和服务器。）

要使用`pppd`启动 PPP 连接，必须知道并输入多个配置选项到`pppd`配置文件中。以下示例是连接到 ISP 时典型的示例。

所需配置信息是 PAP 用户名和密码或 CHAP 主机名和密码、接入电话号码、IP地址是动态分配还是静态分配，以及调制解调器连接的串行端口。

假设以下配置信息：

- PAP username: `customer1`
- PAP password: `customerpassword`
- Access telephone number: `800-555-5555`
- IP address: assigned dynamically
- Serial port: `/dev/ttyS0`

此信息现在必须输入到适当的文件中。由于此配置使用 PAP 身份验证，`/etc/ppp/pap-secrets`将具有以下条目：

```
#Secrets for authentication using PAP
# client    server    secret    IP addresses
customer1   isp   customerpassword
```

`pppd`不提供直接拨号支持，因此需要额外的程序来进行拨号。`chat`程序通常用于此目的。`chat`程序使用`chat`脚本，在过去，对于在启动 PPP 之前需要启动登录会话的远程访问服务器而言，它发挥了非常重要的作用。如今这已不再是大多数远程访问服务的情况——大多数服务现在可以在调制解调器摘机后立即启动 PPP。

如今，对于大多数 ISP 和企业连接，`chat`程序只需向调制解调器发送任何需要的初始化字符串和拨号命令即可。`chat`设置将通过`connect`参数指定。`connect`参数和一些其他关键参数包含在`/etc/ppp/options`文件中：

```
lock
debug
/dev/ttyS0
crtscts
defaultroute
connect '/usr/sbin/chat -v "" ATZ OK ATDT 8005555555'
```

这些选项已在表7.4中介绍过，但简而言之，选项文件已定义`pppd`需要锁定串行端口（`lock`选项）、记录额外的调试信息（`debug`）、使用串行端口`/dev/ttyS0`、打开硬件流控制（`crtscts`）、为对端创建默认路由，然后使用给定的`chat`命令进行连接。

然后可以通过简单地启动`pppd`来启动到 ISP 的连接：

```
[root@lefty /root]# pppd
```

`pppd`的问题通常与调制解调器或身份验证有关。检查问题的第一个地方是`/var/log/messages`文件。例如，以下条目：

```
Jun 3 09:08:45 lefty pppd[11857]: pppd 2.4.1 started by root, uid 0
Jun 3 09:08:45 lefty pppd[11857]: Removed stale lock on ttyS0 (pid 11850)
Jun 3 09:08:46 lefty chat[11858]: expect ( )
Jun 3 09:09:31 lefty chat[11858]: alarm
Jun 3 09:09:31 lefty chat[11858]: Failed
Jun 3 09:09:31 lefty pppd[11857]: Connect script failed
Jun 3 09:09:32 lefty pppd[11857]: Exit.
```

这意味着`chat`脚本失败，这可能是由拼写错误或在这种情况下调制解调器未响应引起的。

测试调制解调器最简单的方法是直接运行`chat`脚本并提高音量以从脚本接收音频反馈：

```
/usr/sbin/chat -v "" ATZ OK AT&L2M2 ATDT 8005555555
```

在身份验证问题方面，如果 Linux 路由器未通过远程站点身份验证，它将记录“Failed to authenticate ourselves to peer。”如果远程站点未通过 Linux 节点身份验证，则 Linux 将报告“Authentication failed。”

## 其他网络服务注意事项

对于作为网关的 Linux 路由器，网络设计师必须确定在网关上应运行哪些额外服务。额外服务的选择基于需求、成本和管理。

### 电子邮件

邮件服务通常在 Linux 网关上运行，以提供邮件投递，尤其面向互联网。

Linux 在处理邮件服务方面做得非常出色，这可能成为企业邮件系统的理想解决方案。

面向互联网的网关应谨慎考虑。将邮件服务器放置在`pppd`服务器上，如果网关被攻破，邮件服务器就会暴露。

### 域名服务 (DNS)

DNS 通常是与`pppd`在同一网关上运行的良好候选服务。与邮件服务器一样，DNS 服务器（通常是 BIND）也容易受到攻击；然而，DNS 被认为的风险不如电子邮件，原因有几个：它对黑客来说吸引力较小，传统上漏洞比邮件服务器少（尽管随着邮件服务器不断加固，这一趋势正在减弱），并且通常只会导致拒绝服务，而不是对资源的威胁。

以仅缓存模式运行的 DNS 服务器对企业和互联网网关都很有用。仅缓存服务器只是缓存所有请求条目以供以后使用。这为下一次请求特定主机名的用户节省了查询时间，并减少了网关 WAN 链路上的额外流量。

对于企业网关，值得考虑将内部域名也加载到名称服务器上。这允许名称服务器解析在本地进行，而不是将请求发送到 WAN 链路。名称服务器按定时方式拉取区域会产生少量额外负载，但负载通常很小，如果需要超过几个内部名称解析请求，这种权衡往往是值得的。

放置 DNS 服务器确实存在风险；与电子邮件一样，应谨慎考虑以确保获得的优势值得冒此风险。

### Web 缓存

Web 缓存与 DNS 类似，可能被考虑用于互联网和企业连接。在最佳情况下，在大型站点中访问过的页面可以预期达到 5%-10% 的命中率。许多当前 Web 缓存解决方案允许预定义站点被缓存以及常用页面被“镜像”，这对于存储企业内联网站的本地副本非常有效。

### rip2ad
