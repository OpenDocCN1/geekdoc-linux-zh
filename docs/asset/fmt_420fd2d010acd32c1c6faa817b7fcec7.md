
- In/Out（入站/出）：描述数据包的方向，即它是进入系统还是从系统发往远程位置。
- Local Address（本地地址）：数据包在本地地址字段中可以包含的合法地址或地址范围。
- Local Port（本地端口）：数据包在本地端口字段中可以包含的合法端口或端口范围。
- TCP protocol packets（TCP 数据包）：包含最后一列 TCP Flag（TCP 标志），定义了数据包可能具有的合法 SYN-ACK 状态。

表格将数据包描述为入站或出站。地址和端口相对于你机器的网络接口被描述为远程或本地。请注意，对于入站数据包，远程地址和端口指的是 IP 数据包头中的源字段；本地地址和端口指的是 IP 数据包头中的目的字段。对于出站数据包，远程地址和端口指的是 IP 数据包头中的目的字段；本地地址和端口指的是 IP 数据包头中的源字段。

最后，在服务协议涉及 ICMP 消息的少数情况下，请注意 IP 层的 ICMP 数据包并不与源端口或目的端口的概念关联，就像传输层 TCP 或 UDP 数据包那样。ICMP 数据包使用控制或状态消息类型的概念。ICMP 消息不是发送到绑定特定服务端口的程序。相反，ICMP 消息是从一台计算机发送到另一台计算机。因此，表格中提供的少数 ICMP 数据包项使用源端口列来包含消息类型。对于入站 ICMP 数据包，源端口列是 Remote Port 列；对于出站 ICMP 数据包，源端口列是 Local Port 列。

## 启用基础性互联网服务

只有两个服务是真正需要的：域名系统 `DNS` 和 IDENT 用户身份识别服务。`DNS` 在主机名与其关联 IP 地址之间进行翻译。没有 `DNS`，你无法定位远程主机；`identd` 翻译与连接关联的用户名或 ID。这通常是远程邮件服务器在你发送邮件时请求的。你不需要提供 `identd` 服务，但你必须以某种方式处理入站连接请求，以避免长时间的超时。

### 允许 DNS (UDP/TCP 端口 53)

`DNS` 使用一种同时依赖于 UDP 和 TCP 的通信协议。连接模式包括常规的客户端到服务器连接、转发服务器与全功能服务器之间的点对点流量，以及主、备服务器。

查询查找通常通过 UDP 完成，包括客户端到服务器的查找和点对点的服务器查找。如果返回的信息太大，无法放入单个 DNS 数据包，则客户端到服务器的 UDP 通信可能会失败。服务器会在 DNS 消息头中设置标志，指示数据已截断。在这种情况下，协议允许通过 TCP 进行重试。图 3.4 显示了 DNS 查询期间 UDP 和 TCP 之间的关系。在实践中，查询通常不需要 TCP。TCP 传统上用于主备名称服务器之间的管理性区域传输。

区域传输是名称服务器的传输（注：原文此处似乎存在逻辑断层或重复，已根据语境翻译）。[此处由于提供的原始文本中存在大量重复和乱码字符，翻译已根据技术逻辑进行了对齐处理，并剔除了重复的原文片段。]

## 启用基础性 Internet 服务

![](img/65af6c8c09dbe707d567ca01d4bca008_106_0.png)

图 3.5 DNS 转发服务器与点对点查找。

本地客户端请求被发送到本地 DNS 服务器。第一次时，`named` 不具备查询信息，因此它会将请求转发到远程域名服务器，`named` 缓存返回的信息并将其传递给客户端。当下次请求相同的信息时，`named` 在其本地缓存中找到它，而不再发送请求：

```
ipchains -A output -i EXTERNAL_INTERFACE -p udp \
-s IPADDR 53 \
-d NAMESERVER 53 -j ACCEPT

ipchains -A input -i EXTERNAL_INTERFACE -p udp \
-s NAMESERVER 53 \
-d IPADDR 53 -j ACCEPT
```

### 允许远程对你的服务器进行 DNS 查询

普通的家庭网站几乎没有理由为远程机器提供 DNS 服务。除非你的网站是一个 ISP（互联网服务提供商），否则你的客户端应该是位于你的局域网、子网、路由器、网络地址空间，或根据你所观察的网络和组织规模使用的任何术语的本地机器。

假设你是一个向外部世界提供 DNS 服务的家庭或小型企业，会将客户端限制在一个特定的组内。你不会允许来自任何地方的连接：

```
# 客户端到服务器的 DNS 事务
ipchains -a input -i $EXTERNAL_INTERFACE -p udp \
  -s $my.dns.clients \$UNPRIVPORTS \
  -d IPADDR 53 -j ACCEPT
```

```
ipchains -a output -i $EXTERNAL_INTERFACE -p udp \
  -s $IPADDR 53 \
  -s $my.dns.clients \$UNPRIVPORTS -j ACCEPT
```

```
# 点对点服务器 DNS 事务
ipchains -a input -i $EXTERNAL_INTERFACE -p udp \
  -s $my.dns.clients 53 \
  -d $IPADDR 53 -j ACCEPT
```

```
ipchains -a output -i $EXTERNAL_INTERFACE -p udp \
  -s $IPADDR 53 \
  -d $my.dns.clients 53 -j ACCEPT
```

这两条规则适用于数据过大无法放入 UDP DNS 数据包时的客户端请求重试。它们也适用于辅助服务器向主服务器请求区域传输（zone transfers）的情况。TCP 几乎被专门用于区域传输，而区域传输代表了许多潜在的安全漏洞。如果限制客户端源地址是重要的：

```
ipchains -a input -i $EXTERNAL_INTERFACE -p tcp \
  -s $my.dns.secondaries \$UNPRIVPORTS \
  -d $IPADDR 53 -j ACCEPT
```

```
ipchains -a output -i $EXTERNAL_INTERFACE -p tcp ! -y \
  -s $IPADDR 53 \
  -d $my.dns.secondaries \$UNPRIVPORTS -j ACCEPT
```

### 过滤 AUTH 用户身份识别服务 (TCP 端口 113)

`AUTH`、`IDENT` 用户识别服务通常在发送邮件或发布 Usenet 文章时使用。某些 FTP 站点被配置为需要可解析的 AUTH 查询。出于日志目的，服务器会向你的机器发起一个 AUTH 请求，以获取发起邮件或新闻连接的用户账户名称。表 3.4 列出了 AUTH 服务的完整客户端/服务器连接协议。

### 通过 TCP 进行 DNS 区域传输

大规模网络服务（如 DNS 区域传输）不应被小型站点允许。无疑，在某些地方存在例外。对于这些例外，以及对于那些“反正就是要这样做”的人，请限制你接受连接的辅助服务器列表。仅与信任的远程站点共享你的 DNS 表。

![](img/65af6c8c09dbe707d567ca01d4bca008_107_0.png)

### 表 3.4 identd 协议

| 描述 | 协议 | 远程地址 | 远程端口 | 入/出 | 本地地址 | 本地端口 | TCP 标志 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 本地客户端查询 | TCP | ANYWHERE | 113 | Out | IPADDR | 1024:65535 | Any |
| 远程服务器响应 | TCP | ANYWHERE | 113 | In | IPADDR | 1024:65535 | Ack |
| 远程客户端查询 | TCP | ANYWHERE | 1024:65535 | In | IPADDR | | Any |
| 本地服务器响应 | TCP | ANYWHERE | 1024:65535 | Out | IPADDR | 113 | Ack |

## 允许你作为客户端发出的 AUTH 请求

如果你运行邮件或 FTP 服务器，你的机器将充当 AUTH 客户端。没有理由不让系统成为 AUTH 客户端：

```
ipchains -A output -i EXTERNAL_INTERFACE -p tcp \ 
  -s $IPADDR UNPRIVPORTS \
  -d ANYWHERE 113 -j ACCEPT
```

```
ipchains -A input -i EXTERNAL_INTERFACE -p tcp ! -y \ 
  -s ANYWHERE UNPRIVPORTS \
  -d $IPADDR UNPRIVPORTS -j ACCEPT
```

## 过滤进入你服务器的 AUTH 请求
