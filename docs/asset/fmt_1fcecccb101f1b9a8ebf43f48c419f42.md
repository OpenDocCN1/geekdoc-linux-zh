
尽管这种状态设置在大多数情况下对小型站点运行良好，但对于较大的站点或同时处理许多连接的防火墙，可能无法充分运行。原因在于状态表项超时，由于表大小和内存限制，静默连接的状态会被替换。本应被状态项接受的下一个数据包需要一条规则来允许该数据包，并且必须重建状态表项。

这的一个简单例子是作为缓存转发名称服务器的本地 DNS 服务器的规则。DNS 转发服务器使用服务器到服务器的通信。DNS 流量在两个主机的源目的端口 53 之间交换。UDP 客户端/服务器关系可以是显式的。以下规则显式允许（NEW）请求、传入的（ESTABLISHED）响应以及任何（RELATED）ICMP 错误消息：

```
iptables -A INPUT -m state \
--state ESTABLISHED, RELATED -j ACCEPT
```

```
iptables -A OUTPUT --out-interface <interface> -p udp \
-s IPADDR --source-port 53 -d $NAME_SERVER --destination-port 53 \
-m state --NEW, RELATED -j ACCEPT
```

DNS 使用简单的查询和响应协议。但对于可以长时间保持连接的应用程序（例如 FTP 控制会话或 SSH 会话）呢？如果状态项由于某种原因过早清除，未来的数据包将没有状态项可以匹配以识别为 ESTABLISHED 交换的一部分。

以下 SSH 连接规则允许这种可能性：

```
iptables -A INPUT -m state \
--state ESTABLISHED, RELATED -j ACCEPT
```

```
iptables -A OUTPUT -m state \
--state ESTABLISHED, RELATED -j ACCEPT
```

```
iptables -A OUTPUT --out-interface <interface> -p tcp \
-s IPADDR --source-port $UNPRIV_PORTS \
-d $REMOTE_SSH_SERVER --destination-port 22 \
-m state --state -j ACCEPT
```

```
iptables -A OUTPUT --out-interface <interface> -p tcp ! --syn \
-s IPADDR --source-port $UNPRIV_PORTS \
-d $REMOTE_SSH_SERVER --destination-port 22 \
-j ACCEPT
```

```bash
iptables -A INPUT --interface <interface> -p tcp ! --syn \
-s $REMOTE_SSH_SERVER --source-port 22 \
-d $IPADDR --destination-port $UNPRIVPORTS \
-j ACCEPT
```

## mac 过滤器表项匹配扩展

表 3.15 列出了 mac 匹配扩展可用的选项。

请记住，MAC 地址不会跨越边界（或网络段）。

同时请记住，只能指定源地址。mac 扩展只能用于入站接口的链，例如 INPUT、PREROUTING 和 FORWARD 链。

以下规则允许来自单个本地主机的 SSH 连接：

```bash
iptables -A INPUT -i <local interface> -p tcp \
-m mac --mac-source xx:xx:xx:xx:xx:xx \
--source-port 1024:65535 \
-d <IPADDR> --port 22 -j ACCEPT
```

## owner 所有者过滤器表项匹配扩展

表 3.16 列出了 owner 匹配扩展可用的选项。

该匹配指的是数据包的创建者。该扩展可以用于 OUTPUT 链。

这些选项在防火墙路由器上没有太大意义；但在终端主机上更有意义。

所以，假设你有一个带有显示器的防火墙网关，但可能没有键盘。

管理是从本地多用户主机完成的。允许一个单一用户账户从该主机登录防火墙。对于该多用户主机，对防火墙的管理员访问可以在本地显示如下：

```bash
iptables -A OUTPUT -o eth0 -p tcp \
-s <IPADDR> --port 1024:65535 \
-d fw <IPADDR> --dport 22 \
-m owner --uid-owner <admin userid> \
-gid-owner <admin groupid> -j ACCEPT
```

### 表 3.15 mac 匹配扩展

| -m | --match mac 选项 | 说明 |
|---|---|---|
| --mac-source [!] <address> | | 匹配进入以太网帧中的第二层以太网硬件源地址，格式为 xx:xx:xx:xx:xx:xx: |

### 表 3.16 owner 匹配扩展

| -m | --match owner 选项 | 说明 |
|---|---|---|
| --uid-owner <userid> | 匹配创建者的 UID |
| --gid-owner <groupid> | 匹配创建者的 GID |
| --pid-owner <processid> | 匹配创建者的 PID |
| --sid-owner <sessionid> | 匹配创建者的 SID 或 PPID |
| --cmd-owner <name> | 匹配由名为 <name> 的进程创建的数据包 |

# 第 3 章 iptables: 传统的 Linux 防火墙管理程序

## mark 标记过滤器匹配扩展

表 3.17 列出了匹配扩展可用的选项。

标记值（mark）和掩码（mask）是无符号长整数。如果指定了掩码，则会将值和掩码进行位与（AND）运算。

在示例中，特定源和目的之间的入站 telnet 数据包之前已经被标记过：

```bash
iptables -A FORWARD -i eth0 -o eth1 -p tcp \
-s <src address> --port 1024:65535 \
-d <destination address> --dport 23 \
-m mark --mark 0x00010070 \
-j ACCEPT
```

测试的标记值为数据包处理早期的某个点。标记值是一个标志，表示此数据包将以与其他数据包不同的方式处理。

## tos 过滤器匹配扩展

表 3.18 列出了匹配扩展可用的选项。

tos 值可以是字符串或数值值之一：

- minimize-delay（最小延迟）, 16, 0x10
- maximize-throughput（最大吞吐量）, 8, 0x08
- maximize-reliability（最大可靠性）, 4, 0x04
- minimize-cost（最小成本）, 2, 0x02
- normal-service（普通服务）, 0, 0x00

### 表 3.17 mark 标记匹配扩展

| m | --mark mark 选项 | 说明 |
|---|---|---|
| --mark <value>[/mask] | | 匹配具有 Netfilter 分配标记的数据包 |

### 表 3.18 tos 匹配扩展

| m | --match tos 选项 | 说明 |
|---|---|---|
| --tos <value> | | 匹配 IP 设置 |

## iptables 语法

TOS 字段已被重新定义为区分服务（DS）字段，用于区分服务代码点（DSCP）。

有关区分服务的更多详细信息，请参考以下源：

- RFC 2474, IPv4 和 IPv6 头部中区分服务（DS）字段的定义
- RFC 2475, 区分服务架构
- RFC 2990, 区分服务的后续
- RFC 3168, 在 IP 中添加显式拥塞通知 (ECN)
- RFC 3260, 区分服务的术语与澄清

## unclean 不洁过滤器匹配扩展

unclean 模块执行的特定数据包检查没有文档说明。该模块被认为是实验性的。

下行显示了 unclean 模块的语法。该模块不接受参数：

```bash
-m | --match unclean
```

在本书出版时，unclean 可能会被“认可”。在此期间，该模块可以作为选项的示例：

```bash
iptables -m unclean
```

在本书出版时，unclean 可能会被“认可”。在此期间，该模块可以作为选项的示例：

```bash
iptables -m --match unclean
```

在本书出版时，unclean 可能会被“认可”。在此期间，该模块可以作为选项的示例：

```bash
iptables -m --match unclean
```

在本书出版时，unclean 可能会被“认可”。在此期间，该模块可以作为选项的示例：
