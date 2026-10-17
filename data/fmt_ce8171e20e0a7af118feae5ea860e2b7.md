
`nmap -T4 -Pn -v -sY -oA sctp -iL/targets.txt`

`nmap -T6 -Pn -v -sU -oA ipv6_udp -iL/targets.txt`

# SCTP

流控制传输协议 `SCTP` 是一种与 `TCP` 和 `UDP` 并列的协议。它提供了在 `IP` 上传输电话数据，复制了 `SS7` 的许多可靠性特性，并支撑称为 `SIGRAN` 的更大协议族。`SCTP` 支持 `IBM AIX`、`Oracle Solaris`、`HP-UX`、`Linux`、`Cisco IOS` 和 `VxWorks` 等操作系统。

## SCTP chunk 类型

| ID | 值 |  |
|---|---|---|
| 0 | DATA | 负载数据 |
| 1 | INIT | 初始化 |
| 2 | INIT ACK | 初始化确认 |
| 3 | SACK | 选择性确认 |
| 4 | HEARTBEAT | 心跳请求 |
| 5 | HEARTBEAT ACK | 心跳确认 |
| 6 | ABORT | 中止 |
| 7 | SHUTDOWN | 关闭 |
| 8 | SHUTDOWN ACK | 关闭确认 |
| 9 | ERROR | 操作错误 |
| 10 | COOKIE ECHO | Cookie |
| 11 | COOKIE ACK | Cookie确认 |
| 12 | ECN | 显式拥塞通知 |
| 13 | CWR | 拥塞窗口缩小 |
| 14 | SHUTDOWN COMPLETE | 关闭完成 |

`Nmap` 和 `SNMP` 等工具无法从私有地址 `NAT` 后面获取信息，因为需要对流入和流出的流量进行低级分析。在图 4-1 的 `ISS BlackICE` 事件日志中可以看到执行简单 `ICMP ping` 扫描的简单示例。

在测试期间运行 `Ethereal` 或 `tcpdump` 等网络嗅探器是有益的，捕捉未请求的 `ICMP` 响应，包括 `ICMP TTL` 超时 `类型 11` 消息、路由环和“`ICMP 管理禁止`” `类型 3 代码 13` 消息，表明路由器或防火墙上有 `ACL`。

## 使用 ICMP 进行操作系统指纹识别

值得值得 `Nmap` 工具是 `Nmap`，通过分析对 `ICMP` 探测的响应对 `Packet` 套件进行指纹识别。`Keuptools` 包含许多网络工具，地址可用：`http://www.dopra.com/read/php/packeto.html`。对于 `Windows`，`Foundation` 的 `SuperScan` 是一个优秀的端口扫描工具，功能良好，包括 `banner` 获取。可以从此处获取 `SuperScan`：`http://examples.oreilly.com/network/tools/superscan.zip`

`Scan` 设计有独特的 `SYN` 探测和后台监听组件，允许进行非常快速扫描。反向 `SYN cookie` `使用 SHA1` 误报变得不存在，因为监听组件只注册具有正确 `SYN` 代码的响应。`Scan` 比 `Nmap` 这样的扫描器快得多。`Unicscan` `http://www.unicscan.com` 是另一个执行半开放扫描的工具。它具有一些实用功能，建议高级用户使用 `UDP` 扫描。我的环境中，响应如下：

```bash
root@kali:~ # icmapscan -n 10.3.0.1
```

跨工具的 `UDP` 扫描可能不同。`Nmap` 提供了一个带有 `-sV` 的全面选项，但使用 `-F` 选项 `扫描 100 个端口` 测试单个主机需要几分钟。

使用 `TCP` 标志探测目标被称为反向技术。`RFC 793` 规定，如果主机上的端口关闭，应发送 `RST/ACK` 数据包以重置连接。

## 远程端口转发 - 通过另一个系统将端口转发到远程系统

将 `SSH` 服务器上的流量通过 `SSH` 客户端或其他主机转发到目标。这使得能够公网访问的用户可以访问私有网络上的资源。用例包括：

- 通过公网开放本地开发服务器
- 对私有网络上的资源授予 `IP` 限制的访问权限

`SSH -R OUTSIDE-IP:port:INSIDE-IP:port`

### `ssh -R 8080:localhost:80 ssh-server`
将流量转发到本地计算机 `localhost 8080` 端口上的所有接口。如果这些接口之一可以从互联网访问，则连接到 `8080` 端口的流量将被转发到其他服务。
`img/4541d1f2c9832b9303a6df6c92f86f6_237.png`

### `ssh -R 70.114.93.221:8080:localhost ssh-server`
将流量转发到本地系统上的 `ssh-server:localhost`，但仅允许来自 `IP` 地址 `70.114.93.221` 的 `SSH` 隧道入口。这需要在你的 `ssh_config` 配置中设置 `GatewayPorts clients`。
`img/4541d1f2c9832b9303a6df6c92f86f6_237_1.png`

### `ssh -R 8080:example.org:80 ssh-server`
将流量转发到本地系统上 `ssh-server:8080:localhost:80` 的所有接口。从你的本地系统，流量随后会被转发到 `example.org`。从 `example` 的角度来看，流量源自你的本地系统。
`img/4541d1f2c9832b9303a6df6c92f86f6_237_2.png`

## 在 `/etc/ssh/sshd_config` 中设置的 SSH 服务器配置

默认情况下，转发端口无法从公网访问。你需要在远程服务器上添加 `GatewayPorts yes` 以将公网流量转发到你的本地计算机。如果你想允许特定的客户端，可以使用此替代：
```ssh
GatewayPorts yes
```

## 动态端口转发：将端口范围的流量转发到远程服务器

在 `SSH` 客户端上开启 `SOCKS` 代理，允许你通过 `SSH` 服务器将流量转发到所有接口端口 `3000` 的任何目标。默认情况下，`SSH` 将使用 `SOCKS` 协议，转发 `TCP` 和 `UDP` 流量。

### `ssh -D 127.0.0.1:3000 ssh-server`
在本地系统上的 `127.0.0.1:3000` 开启 `SOCKS` 代理。如果你运行着 `SOCKS` 代理，可以配置网页浏览器作为源自 `ssh` 的连接来访问资源。例如，如果 `ssh` 有权访问私有网络内的其他服务器，你可以在本地访问这些服务器，就像你在网络上一样，而无需 `VPN`。这样测试代理：
```bash
curl -x socks://127.0.0.1:3000 https://example.com
```
`img/4541d1f2c9832b9303a6df6c92f86f6_237_4.png`

## SSH 客户端配置 - `/etc/ssh/ssh_config`

如果你在配置 `SSH` 客户端时希望 `SOCKS` 代理可用于比 `localhost` 更多的接口，可以使用命令进行配置，而不是手动编辑：
```ssh
ssh -o GatewayPorts=yes -D 3000 ssh-server
```
