
## 第 12 章 · 加固你的系统

遵循这种方法，如果你的校园网络与互联网之间有一个防火墙和病毒过滤器，那么任何所有的远程系统（包括家庭和移动系统）在数据允许通过企业 `VPN` 访问主网络之前，都需要经过同等的保护。这种解决方案将让你受控于用户的意愿，除非该家庭 `VPN`/`防火墙`/`病毒过滤系统`是一个广为人知的、且人们对其拥有特权访问的系统。另一种解决方案是让进入每个办公室 `VPN` 的数据经过过滤，以阻止不可接受的端口和病毒。理想情况下，应该同时使用这两种解决方案（即对互联网和远程用户进行过滤，以及通过 `VPN` 对进入每个办公室的数据进行过滤），以应对更多的安全风险。

利用 `Linux` 的 `IP Tables` 或 `IP Chains`，以便你只允许必要的流量通过 `VPN`。如果你通过使用 `POP` 或 `IMAP` 限制路由来获取邮件，并使用 `SMTP` 将邮件发送到你基于 `Linux` 或 `UNIX` 的邮件服务器（通过书中的技术保持所有安全），你首要担心的问题就是携带邮件的病毒。如果你过滤掉来自这些远程系统的邮件附件，你将获得良好的保护。

为了让你对如何处理 `VPN` 安全有一个概念，这里有一个典型的场景。假设主办公室与 `Albany` 办公室之间有以下通信需求：

- `Albany` 用户可以访问 `192.168.0.3` 上的系统 `POP3` 和 `SMTP` 服务来检索和发送邮件。
- `Albany` 用户可以访问 `192.168.0.4` 上的内部 `Web` 服务器（`HTTP` 和 `HTTPS`）以用于企业内网。
- 主办公室的系统管理员（`SysAdmin`）需要从其 `IP` 为 `192.168.0.6` 的 `Linux` 工作站管理 `Albany` 办公室 `192.168.1.9` 上的 `Samba` 服务器。

主办公室的 `IP` 规则可能如下：

```bash
# 允许从 Albany 办公室发起的 POP 和 SNMP 流量
iptables -A FORWARD -i pp0 -p tcp --syn -m state \
  --state NEW -s 192.168.1.0/24 -d 192.168.0.3 110 -j ACCEPT
iptables -A FORWARD -i pp0 -p tcp --syn -m state \
  --state NEW -s 192.168.1.0/24 -d 192.168.0.3 25 -j ACCEPT
```

```bash
# 允许从 Albany 办公室发起的 HTTP 和 HTTPS 流量
iptables -A FORWARD -i pp0 -p tcp --syn -m state \
  --state NEW -s 192.168.1.0/24 -d 192.168.0.4 80 -j ACCEPT
iptables -A FORWARD -i pp0 -p tcp --syn -m state \
  --state NEW -s 192.168.1.0/24 -d 192.168.0.4 443 -j ACCEPT
```

```bash
# 允许从主办公室发起的到 Samba 服务器的 SSH 流量
iptables -A FORWARD -i pp0 -p tcp --syn -m state \
  --state NEW -s 192.168.0.6 -d 192.168.1.9 22 -j ACCEPT
```

## 虚拟专用网络 (`VPNs`)

```bash
# 允许已建立的后续包通过
# 初始 SYN 包 (RELATED IS NO-OP)
iptables -A FORWARD -p tcp -m state \
  --state ESTABLISHED,RELATED -j ACCEPT

# 阻塞所有来自 VPN 的流量
# (你可能不想记录所有流量)
iptables -A FORWARD -i ppp0 -s 192.168.1.0/24 \
  -j LOG --log-prefix "I want DROP -l1"
iptables -A FORWARD -i ppp0 -s 192.168.1.0/24 \
  -j DROP
```

并且如果使用了 `IP Chains`，它们可能如下：

```bash
# 观察 -s (源地址) 和 -d (目的地址) 参数
# 我在耍小花呢 --Bob
```

```bash
# 允许从 Albany 发起的 POP 和 SNMP 流量
ipchains -A input ppp0 -p tcp -s 192.168.0.0/24 \
  -d 192.168.0.3 110 -j ACCEPT
ipchains -A output - ppp0 -p tcp -d 192.168.1.0/24 \
  -s 192.168.0.3 110 -y -j ACCEPT
ipchains -A input - ppp0 -p tcp -s 192.168.1.0/24 \
  -d 192.168.0.3 25 -j ACCEPT
ipchains -A output - ppp0 -p tcp -d 192.168.1.0/24 \
  -s 192.168.0.3 25 -y -j ACCEPT
```

```bash
# 允许从 Albany 发起的 HTTP 和 HTTPS 流量
ipchains -A input ppp0 -p tcp -s 192.168.0.0/24 \
  -d 192.168.0.4 80 -j ACCEPT
ipchains -A output - ppp0 -p tcp -d 192.168.1.0/24 \
  -s 192.168.0.4 80 -y -j ACCEPT
ipchains -A input - ppp0 -p tcp -s 192.168.1.0/24 \
  -d 192.168.0.4 443 -j ACCEPT
ipchains -A output - ppp0 -p tcp -d 192.168.1.0/24 \
  -s 192.168.0.4 443 -y -j ACCEPT
```

```bash
# 允许从主办公室发起的
# Samba 服务器
ipchains -A output -i ppp0 -p tcp -s 192.168.0.6 \
  -d 192.168.1.9 22 -j ACCEPT
ipchains -A input - ppp0 -p tcp -s 192.168.0.6 \
  -d 192.168.1.9 22 -j ACCEPT
```

```bash
# 允许已建立的后续包通过
# 初始 SYN 包 (RELATED IS NO-OP)
iptables -A FORWARD -p tcp -m state \
  --state ESTABLISHED,RELATED -j ACCEPT

# 阻塞所有来自 VPN 的流量
# (你可能不想记录所有流量)
iptables -A FORWARD -i ppp0 -s 192.168.1.0/24 \
  -j LOG --log-prefix "I want DROP -l1"
iptables -A FORWARD -i ppp0 -s 192.168.1.0/24 \
  -j DROP
```

对于上一个示例，在主办公室，`IP Tables` 规则

```
iptables -A FORWARD -o eth0 -d 192.168.1.0/24 -j LOG
iptables -A FORWARD -o eth0 -d 192.168.1.0/24 -j DROP
iptables -A FORWARD -o eth0 -s 192.168.1.0/24 -j LOG
iptables -A FORWARD -o eth0 -s 192.168.1.0/24 -j DROP
```

或者 `IP Chains` 规则

```
ipchains -A output -i eth0 -d 192.168.1.0/24 -j DENY -1
ipchains -A input -i eth0 -s 192.168.1.0/24 -j DENY -1
```

将停止这一操作。

- 4. 加密需要大量的计算。请参见第 429 页的“`VPN` 性能测量”进行讨论。
