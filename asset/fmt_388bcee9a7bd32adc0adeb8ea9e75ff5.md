
你希望允许外部访问 Apache 服务器。以下是该脚本：

# 在 DMZ 中访问 DNS 服务器

你希望允许外部访问 DNS 服务器。以下是该脚本：

```
# 允许来自外部的入站客户端/服务器 DNS 请求
$IPTABLES -A input -i $WORLD_INTERFACE \
  -p udp \
  -s 0/0 1024-65535 \
  -d $DMZ_DNS_SERVER_ADDR 53 \
  -J ACCEPT

# 允许出站的客户端/服务器 DNS 响应
$IPTABLES -A output -i $WORLD_INTERFACE \
  -p udp \
  -s $DMZ_DNS_SERVER_ADDR 53 \
  -d 0/0 1024-65535 \
  --J ACCEPT

# 允许来自外部的入站服务器/服务器 DNS 请求
$IPTABLES -A input -i $WORLD_INTERFACE \
  -p udp \
  -s 0/0 53 \
  -d $DMZ_DNS_SERVER_ADDR 53 \
  --J ACCEPT

# 允许出站的服务器/服务器 DNS 响应
$IPTABLES -A output -i $WORLD_INTERFACE \
  -p udp \
  -s $DMZ_DNS_SERVER_ADDR 53 \
  -d 0/0 53 \
  --J ACCEPT
```

# 第 20 章：防火墙、VPN 和 SSL 隧道

## 在 DMZ 中访问 identd (认证) 服务器

你希望允许外部访问 identd 服务器。identd 服务器通常运行在邮件服务器上，提供用户身份验证服务。假设你运行在 DMZ_MAIL_SERVER 上。以下是该脚本：

```
# 允许来自外部的入站认证请求
$IPTABLES -A input -i $WORLD_INTERFACE \
  -p tcp \
  -s 0/0 1024-65535 \
  -d $DMZ_MAIL_SERVER_ADDR 113 \
  -j ACCEPT

# 允许出站认证响应
$IPTABLES -A output -i $WORLD_INTERFACE \
  -p tcp -i y \
  -s $DMZ_MAIL_SERVER_ADDR 113 \
  -d 0/0 1024-65535 \
  -j ACCEPT
```

以下代码为你的邮件服务器启用认证客户端服务。

```
# 允许来自外部的入站认证响应
$IPTABLES -A input -i $WORLD_INTERFACE \
  -p tcp \
  -s 0/0 113 \
  -d $DMZ_MAIL_SERVER_ADDR 1024-65535 \
  -j ACCEPT

# 允许来自邮件服务器的出站认证请求
$IPTABLES -A output -i $WORLD_INTERFACE \
  -p tcp \
  -s $DMZ_MAIL_SERVER_ADDR 113 \
  -d 0/0 1024-65535 \
  -j ACCEPT
```

## 在 DMZ 中访问邮件服务器

你希望允许外部访问邮件服务器。

```
# 允许来自外部的入站 SMTP 请求
$IPTABLES -A input -i $WORLD_INTERFACE \
  -p tcp \
  -s 0/0 1024-65535 \
  -d $DMZ_MAIL_SERVER_ADDR 25 \
  -j ACCEPT

# 允许出站的 SMTP 请求/响应
$IPTABLES -A output -i $WORLD_INTERFACE \
  -p tcp -y \
  -s $DMZ_MAIL_SERVER_ADDR 25 \
  -d 0/0 1024-65535 \
  -j ACCEPT
```

### 重定向数据包

假设将将内部网络 (`192.168.2.0/24`) 发往 IP 地址为 `193.1.1.193` 端口 `80` 的特定网站的数据包重定向到 IP 地址为 `193.1.1.195` 的 Web 服务器。你可以在主防火墙规则中添加以下规则：

```
$IPTABLES -t nat -A POSTROUTING -s 192.168.2.0/24 \
-d 193.1.1.193 \
-p tcp --dport 80 \
-j SNAT --to 193.1.1.195
```

### 记录数据包信息

你可以使用 netfilter 内置的日志支持 (`/var/log/messages`) 来排查规则故障并监控流量。例如：

```
$sbin/iptables -A input -s 193.1.1.193 -j LOG
```

每当来自 `193.1.1.193` 机器的数据包进入防火墙时，它会被记录。你可以控制日志条目的数量，可以使用 `--limit --limit rate` 选项。例如：

```
$sbin/iptables -A input -s 193.1.1.193 -m limit --limit 10/second -j LOG
```

上述规则将记录来自 `193.1.1.193` 主机的最多 10 个数据包。你也可以使用前缀来标识 `193.1.1.193` 主机的数据包，例如：

```
$sbin/iptables -A input -s 193.1.1.193 -m limit --limit 10/second -j LOG
```

上述规则将记录来自 `193.1.1.193` 主机的最多 10 个数据包。你也可以使用前缀来标识 `193.1.1.193` 主机的数据包，例如：

```
$sbin/iptables -A input -s 193.1.1.193 -m limit --limit 10/second -j LOG
```

（注：此处原文内容似乎存在重复或中断，已按逻辑尽可能翻译）

### 设置数据包的服务类型 (TOS)

你可以通过设置 TOS 值来让某种类型的流量优先级高于另一种。TOS 值可以包括：

- 延迟 (Delay)
- 吞吐量 (Throughput)
- 可靠性 (Reliability)

例如，在以下情况下设置 TOS：

```
$IPTABLES -A PRERUTING -p tcp \
-dport -j TOS
```

### 状态检查

Netfilter 提供了将数据包关联到特定状态的能力：

- 新 (`NEW`)：尝试建立新连接的数据包。
- 相关 (`RELATED`)：与现有连接相关的数据包。
- 已建立 (`ESTABLISHED`)：属于现有连接的数据包。
- 无效 (`INVALID`)：不符合任何已知状态的数据包。

例如，通过以下规则允许已建立连接的数据包：

```
$iptables -A input -m state --state ESTABLISHED -j ACCEPT
```

### 网络地址转换 (NAT) 规则

Netfilter 中的 NAT 表允许你伪装、重定向甚至负载均衡。NAT 目标包括：

- `DNAT` (目标地址转换)：修改数据包的目标地址。
- `SNAT` (源地址转换)：修改数据包的源地址。
- `REDIRECT` (重定向)：将数据包重定向到本地。

使用 NAT 表中的 `POSTROUTING` 链，你可以创建一个简单的负载均衡环境。例如，将 `192.168.1.1` 负载均衡到 `192.168.1.20`、`192.168.1.21` 或 `192.168.1.22`：

```
$iptables -t nat -A POSTROUTING -s 192.168.1.1 -p tcp --dport 80 -j DNAT --to-destination 192.168.1.20
```

### 测试数据过滤规则

首先，你应该使用 `$sbin/iptables` 链名 `[-t 表名]` 命令列出所有规则。例如，要列出默认表中 `input` 链中的所有规则，请运行 `$sbin/iptables -L input`。

要测试现有规则，只需将 `-A`（追加规则）或 `-I`（插入规则）替换为 `-C`，并插入源和目的 IP 地址。例如，假设你有一如下规则：

```
$sbin/iptables -A input -i eth1 -p tcp \
  -s 0/0 \
  -d 192.168.1.100 \
  -dport 80 \
  -j REJECT
```

该规则表示，任何 IP 地址 (`-s 0/0`) 发往 IP 地址 `192.168.1.100` 端口 `80` 的数据包在以太网接口 `eth1` 上都会被拒绝。要测试这一点，你可以运行以下代码：

```
$sbin/iptables -C input -i eth1 -p tcp \
  -s 0/0 \
  -d 192.168.1.100 \
  -dport 80 \
  -j REJECT
```

如果输出为 "match"，则该规则存在。如果不存在，你应该添加它。
