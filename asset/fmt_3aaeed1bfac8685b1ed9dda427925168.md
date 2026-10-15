
`-j ACCEPT`

```
$IPTABLES -A INPUT -i eth0 -p tcp --dport 5566 \
  -j ACCEPT
```

```
$IPTABLES -A INPUT -i eth0 -p tcp --dport 40000:40099\
  -j ACCEPT
```

## 在防火墙处拦截 Messenger 流量

标准的 MSN 客户端使用 TCP 端口 1863；然而，据报道某些客户端也会尝试回退其他标准端口，如 80 (`http`) 和 443 (`https`) 以重新建立连接。一种策略是阻止访问登录服务器本身。在本书写作时，服务器是 `messenger.hotmail1.com`，它映射到 `207.46.104.20`——尽管我怀疑 MSN 在该网络空间内会有其他登录服务器。你的方法可以分为三个方面：

### 记录并过滤 MSN 端口 1863：

```
$IPTABLES -A FORWARD -p tcp --dport 1863 -m limit \
  --limit 1/second -j LOG --log-level info \
  --log-prefix "Policy Violation: MSN "
$IPTABLES -A FORWARD -p tcp --dport 1863 -j DROP
```

### 记录并过滤登录服务器：

```
$IPTABLES -A FORWARD -d 207.46.104.20 -m limit \
  --limit 1/second -j LOG --log-level info \
  --log-prefix "Policy Violation: MSN "
$IPTABLES -A FORWARD -d 207.46.104.20 -j DROP
```

### 记录并过滤消息服务器：

```
$IPTABLES -A FORWARD -d 207.46.110.0/25 -m limit \
  --limit 1/second -j LOG --log-level info \
  --log-prefix "Policy Violation: MSN "
$IPTABLES -A FORWARD -d 207.46.110.0/25 -j DROP
```

## YAHOO MESSENGER

Yahoo Messenger 是 Yahoo 提供的即时通讯客户端。除了标准的文本即时消息外，它支持支持、视频和文件传输。它使用多个 TCP 和 UDP 端口，取决于所使用的服务。Yahoo 网站上的以下页面记录了 Yahoo Messenger 使用的端口和服务器：
`http://help.yahoo.com/help/us/msg/twin/twin-15.html`。

## 连接 YAHOO MESSENGER

在我们测试的所有即时通讯服务中，Yahoo 直到问题最少的。它对防火墙非常友好，即使对于语音和视频等复杂的服务也是如此。
对于登录和文本消息连接，Yahoo Messenger 使用以下 TCP 端口：

- 20（通常留给 FTP）
- 23（通常留给 telnet）
- 25（通常留给 SMTP）
- 80（通常留给 HTTP）
- 119（通常留给 NNTP）
- 5050
- 视频流量（摄像头）将使用 TCP 端口：5100
- 文件传输使用 TCP 端口：80
- 语音通信使用 TCP 或 UDP 端口 5000-5010

如果你在让这些服务穿过防火墙时遇到困难，常见的祸首可能是针对列出的端口的 DROP 规则。

## 拦截 YAHOO MESSENGER 流量

首先，Yahoo 在使其 客户端友好方面做得非常出色，因为他们到处使用“标准”服务和 IP 地址。这是目前最难过滤的。有效的方法是使用代理服务器来绕过这些规则。由于 Yahoo 经常更改，第一步是检查 `http://help.yahoo.com/help/us/msg/twin-15.html` 获取最新列表。在本书写作时，这些是：

- `sa.yahoo.com`
- `sb.msg.yahoo.com`
- `sc.msg.yahoo.com`
- `ss.msg.com`

使用 "`host`" 命令提取 IP 地址的示例：

```
[user@firewall /tmp]$ host sc.msg.com
sc.msg.com（是 scdcntest-b.msg.com 的别名）
scsdntest-b.msg.com 的地址为 216.155.993.148
scsdntest-b.msg.com 的地址为 216.155.993.149
scsdntest-b.msg.com 的地址为 216.155.993.150
scsdntest-b.msg.com 的地址为 216.155.993.151
scsdntest-b.msg.com 的地址为 216.155.993.152
scsdntest-b.msg.com 的地址为 216.155.993.153
scsdntest-b.msg.com 的地址为 216.155.993.154
scsdntest-b.msg.com 的地址为 216.155.993.155
```

```
[user@firewall /tmp]$ host sb.msg.yahoo.com
sb.msg.com（是 s-fooe.yahoo.com 的别名）
s-fooe.yahoo.com 的地址为 66.163.173.8
s-fooe.yahoo.com 的地址为 216.136.128.144
s-fooe.yahoo.com 的地址为 216.136.227.23
s-fooe.yahoo.com 的地址为 216.136.233.152
s-fooe.yahoo.com 的地址为 216.136.131.64
s-fooe.yahoo.com 的地址为 216.136.172.248
s-fooe.yahoo.com 的地址为 216.136.173.180
s-fooe.yahoo.com 的地址为 216.136.225.28
s-fooe.yahoo.com 的地址为 216.136.226.13
s-fooe.yahoo.com 的地址为 216.136.227.22
```

```
[user@firewall /tmp]$ host sc.msg.yahoo.com
sc.msg.com（是 scdcntest-b.msg.com 的别名）
scsdntest-b.msg.com 的地址为 216.155.993.147
scsdntest-b.msg.com 的地址为 216.155.993.148
scsdntest-b.msg.com 的地址为 216.155.993.149
scsdntest-b.msg.com 的地址为 216.155.993.150
```

为了拦截这些流量，你可以使用以下规则：

```
$IPTABLES -A FORWARD -p tcp --dport 1863 -m limit \
  --limit 1/second -j LOG --log-level info \
  --log-prefix "Policy Violation: MSN "
$IPTABLES -A FORWARD -p tcp --dport 1863 -j DROP
$IPTABLES -A FORWARD -d 207.46.104.20 -m limit \
  --limit 1/second -j LOG --log-level info \
  --log-prefix "Policy Violation: MSN "
$IPTABLES -A FORWARD -d 207.46.104.20 -j DROP
$IPTABLES -A FORWARD -d 207.46.110.0/25 -m limit \
  --limit 1/second -j LOG --log-level info \
  --log-prefix "Policy Violation: MSN "
$IPTABLES -A FORWARD -d 207.46.110.0/25 -j DROP
$IPTABLES -A FORWARD -d 216.155.993.127 -j DROP
$IPTABLES -A FORWARD -d 216.155.993.128 -j DROP
$IPTABLES -A FORWARD -d 216.155.993.129 -j DROP
$IPTABLES -A FORWARD -d 216.155.993.130 -j DROP
$IPTABLES -A FORWARD -d 216.155.993.131 -j DROP
$IPTABLES -A FORWARD -d 216.155.993.132 -j DROP
$IPTABLES -A FORWARD -d 216.155.993.133 -j DROP
$IPTABLES -A FORWARD -d 216.155.993.134 -j DROP
```
