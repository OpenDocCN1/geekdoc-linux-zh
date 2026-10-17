
在第3章中，我们将讨论黑客用于扫描你的机器可用服务的各种方法和软件包。审计系统的一个关键部分是定期进行扫描，并检查你向整个世界开放了哪些服务。

首先，创建你机器上所有可用的网络接口列表。使用以下命令即可实现：

```
machine5 ifconfig -
eth0 Link encap:Ethernet Haddr 00:80:BC:A8:68:E6
inet addr: 192.168.1.20 Mask:255.255.128
BROADCAST MTU:1500 Metric:1
RX packets:0 errors:0 dropped:0 overflows:0 frame:0
TX packets:12 errors:0 dropped:0 overflows:0 carrier:0
Collisions:0 txqueuelen:100
Interrupt:9 Base address:0x300
```

```
eth0:0 Link encap:Ethernet Haddr 00:80:BC:A8:68:E6
inet addr: 10.15.100.10 Mask:255.255.255.0
BROADCAST MTU:1500 Metric:1
RX packets:0 errors:0 dropped:0 overflows:0 frame:0
TX packets:12 errors:0 dropped:0 overflows:0 carrier:0
collisions:0 txqueuelen:100
Interrupt:9 Base address:0x300
```

```
lo Link encap:Loopback
inet addr:127.0.0.1 Mask:255.0.0.0
```

```
UP LOOPBACK RUNNING MTU:3924 Metric:1
RX packets:678 errors dropped:0 overruns:0 frame:0
TX packets:678 errors dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:0

Link encap:Point-to-Point Protocol
inet addr: 172.16.28.55 Mask:255.255.255.252
POINTONOARP MULTICAST MTU:1500 Metric:1
RX packets:5184 errors dropped:0 overruns:0 frame:0
TX packets:6734 errors dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:10
```

上面我们有一台具有多个接口的机器：

*   `eth0`: 以太网卡上的 IP 地址
*   `eth0`: `eth0` own 上的虚拟 IP 地址
*   `ppp0`: PPP（现代）地址
*   `lo`: 回环地址

可能（且在安全配置中很可能）你的某些服务仅在特定接口上可用。例如，你可能让 `IMAP` 仅在其中一个接口上进行监听，或者你可能配置了 `ipchains`/`iptables` 仅允许某些数据包。因此，针对所有可用地址运行网络扫描器以明确指定每个接口上可用的内容是非常重要的。

你可以（也应该）从本地机器运行测试，但这可能无法给你提供最安全的可用性映射。你的机器面前的路由设备上可能有防火墙或访问控制列表，宿主机本身也有 `ipchains`/`iptables` 配置。因此，你还应该从外部接入点扫描你的主机。合适的接入点包括外部 `ISP` 账户、家庭拨号接入或朋友处。

> 如果通过网络或从不是你自己的机器进行扫描，获得机器所有者的许可是一个非常好的主意。解释你正在扫描的是自己的机器，而不是试图获取某些第三方的非法访问权限。尽可能提供详细信息，包括扫描的时间、持续时间、源和目的地。在扫描之前提出这一点总比在事后才解释要好。墨菲定律规定，入侵检测系统不会帮助人们判断你的机器是否正受到攻击，但当你只影响自己的机器时，它们肯定会抓到你。

# 第2章：主动措施与从入侵中恢复

你应该确保使用第3章中列出的几种网络安全扫描器进行你自己的扫描。不要只依赖于一个，因为每种工具都有不同的益处。

## 扫描检测器

黑客在尝试入侵你的系统之前，要做的第一件事是从网络上对其进行扫描。如果你部署了入侵检测系统（`IDS`）来在你被扫描时通知你，你就拥有优势，并可以做好阻止他们的准备。你可以在 `Linux` 上运行几种扫描检测器。每种工具都有不同的益处。

由 `John Riley` 等人创建的 `scanlogd` 是一个独立的守护进程。它可以使用原始套字、`libp` 或 `libcap` 来监听接入连接。如果在三秒间隔内检测到 7 个唯一的特权端口（`<1024`）、21 个唯一的非特权端口（`>1024`）或两者的加权组合，`scanlogd` 将评估为扫描。它将通过 `syslog` 记录扫描。此外，如果在 20 秒内检测到多次扫描，`scanlogd` 将临时报告该主机，以防止可能填充日志的拒绝服务攻击。

`syslog` 消息如下：

```
source_addr = dest_addr ports, ..., TCP_flags @time
```

例如，对本地主机进行 `nmap` 可能会生成以下 `syslog` 消息（为了清晰进行了折行）：

```
scanlogd: 127.0.0.1 to 127.0.0.1 ports 47161, 835, 6110, 889,
6005, 168, 403, ..., f??pxy, TOS 00 @17:19:58
scanlogd: 127.0.0.1 to 127.0.0.1 ports 44851, 134, 1002, 633,
2, 6006, 761, ..., f??pxy, TOS 00 @17:22:45
scanlogd: 127.0.0.1 to 127.0.0.1 ports 39792, 910, 73, 117,
2638, 169, 537, ..., f??pxy, TOS 00 @18:30:32
```

列出的 `TCP` 标志是设置在数据包本身中的 `TCP` 控制位。虽然在了解你正被扫描时并不需要理解这些位，但在深入观察扫描和攻击时，它们会非常有用。有关这些位的定义，请参考 `RFC-793`。

# PortSentry

`PortSentry` 是 `Psionic Abacus` 项目的一部分，`PortSentry`（`http://www.psionic.com/abacus/portsentry/`）不仅允许你检测扫描，还能对源采取行动。它可以检测正常和隐蔽扫描，并可以监控多 64 个端口，这对于捕捉扫描来说绰有余。

当检测到端口扫描时，`PortSentry` 可以以以下任何方式做出响应：

*   通过 `syslog` 记录扫描日志。
*   在 `/etc/hosts.deny` 中添加条目以拒绝来自该主机的连接。
*   在系统中添加一条本地路由，使你的机器无法与攻击者通信，从而有效拦截所有返回流量。
*   重新配置本地数据包过滤器，以拒绝来自攻击者的所有访问。

> 注意：自动拒绝主机可能会导致你的机器遭受拒绝服务攻击。攻击者可以伪造数据包，使其看起来来自不同的机器，而你的扫描检测器随后会拒绝该机器的访问。如果攻击者伪装成你与之通信的机器——例如日志主机、`DNS` 服务器或安全服务器——你将失去与这些机器的连接。

`PortSentry` 可以以多种方式运行：

*   `TCP` 模式：`PortSentry` 将绑定到指定的 `TCP` 端口，等待连接并响应。
