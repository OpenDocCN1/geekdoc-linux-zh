

## 第 14 章：计算机安全问题 585

- /etc/init.d/iptables — 这是 iptables 启动脚本，每次 Fedora 重启时都必须自动运行。当它启动时，它会清除所有的 iptables 规则和计数器，并从 /etc/sysconfig/iptables 文件安装新规则。你也可以从命令行使用不同的选项来检查 iptables 的状态 (status) 或运行 iptables-save 来保存当前规则 (save)。

为了让你开始使用 iptables，我为你提供了一组示例 iptables 规则，并说明了你如何根据不同情况更改这些规则。以下是你可以如何加载和保存后续示例中描述的任何一组规则：

1. 停止 iptables 并清除所有现有规则：
   `# /etc/init.d/iptables stop`

2. 使用任何文本编辑器将后续示例中的规则添加到文件中。根据你的情况修改规则并保存文件。

3. 以 root 用户身份，将该文件作为 shell 脚本进行运行。例如，如果你将文件命名为 firescript，可以这样运行它：
   `# sh firescript`

4. 查看规则是如何加载到内核的：
   `# iptables -L`

5. 如果一切看起来正常，将现在内核中的规则保存到 /etc/sysconfig/iptables 文件中：
   `# cp /etc/sysconfig/iptables /etc/sysconfig/iptables-old`
   `# service iptables save`

6. 启动 iptables：
   `# /etc/init.d/iptables start`

从现在起，规则将在每次重启或重启 iptables 时被读取。请保存一份你用于创建规则时使用的脚本副本，以防以后再次需要。

## 示例 1：用于共享 Internet 连接（以及服务器）的防火墙

由于防火墙配置可能根据你试图实现的目标而大不同，我根据几种不同的示例设置说明了如何配置防火墙。这些设置结合了不同级别的安全需求。

此示例包含一个家庭或小型办公室的局域网（LAN），其中一个 Fedora 系统作为局域网和互联网之间的 iptables 防火墙。该防火墙计算机同时也作为 Web 服务器、FTP 服务器和 DNS 服务器。图 14-2 显示了这种配置。

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_633_0.png)

**图 14-2**: 使用 iptables 作为互联网和局域网之间的防火墙

如果你想使用下面的示例防火墙脚本，你必须更改以下信息以匹配你的配置：

**防火墙计算机** — 防火墙设置如下：

- **本地主机 — 127.0.0.1**（IP 地址）和 lo（接口）。你可能不需要更改这些。
- **连接互联网 — 123.45.67.89**（IP 地址）和 eth0（接口）。请将它们分别替换为与你的连接相关的静态 IP 地址和接口名称。
- **连接局域网 — 10.0.0.1**（IP 地址）和 eth1（接口）。请将 10.0.0.1 和 eth1 分别替换为与你的局域网相关的静态 IP 地址和接口名称。
- **局域网上的计算机** — 局域网上的每台计算机都有一个从 10.0.0.2 到 10.0.0.25 的 IP 地址。将 10.0.0.25 更改为匹配你局域网地址范围的数字。

以下是一个加载防火墙规则的脚本示例，可用于图 14-2 所示的配置：

```bash
# (1) 策略（默认）
iptables -P INPUT DROP
iptables -P OUTPUT DROP
iptables -P FORWARD DROP

# (2) 用于接受的 TCP 数据包的自定义链
iptables -N okay
```

```bash
iptables -A okay -p TCP --syn -j ACCEPT
iptables -A okay -p TCP -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A okay -p TCP -j DROP
```

### (3) 来自局域网的 INPUT 链数据包

```bash
# 入站规则
iptables -A INPUT -p ALL -i eth0 -s 10.0.0.0/24 -j ACCEPT
iptables -A INPUT -p ALL -lo -s 127.0.0.1 -j ACCEPT
iptables -A INPUT -p ALL -lo -s 10.0.0.1 -j ACCEPT
iptables -A INPUT -p ALL -lo -s 123.45.67.89 -j ACCEPT
iptables -A INPUT -p ALL -i eth0 -d 10.0.0.255 -j ACCEPT
```

### 来自互联网的入站数据包规则

```bash
# 已建立连接的数据包
iptables -A INPUT -p ALL -d 123.45.67.89 -m state --state \
ESTABLISHED,RELATED -j ACCEPT
```

### TCP 规则

```bash
iptables -A INPUT -p TCP -i eth0 --destination-port 21 -j okay
iptables -A INPUT -p TCP -i eth0 --destination-port 22 -j okay
iptables -A INPUT -p TCP -i eth0 --destination-port 80 -j ACCEPT
```

### UDP 规则

```bash
iptables -A INPUT -p UDP -i eth0 --destination-port 53 -j ACCEPT
```

### ICMP 规则

```bash
iptables -A INPUT -p ICMP -i eth0 --icmp-type 8 -j ACCEPT
iptables -A INPUT -p ICMP -i eth0 --icmp-type 11 -j ACCEPT
```

### (4) FORWARD 链规则

```bash
# 已建立连接的数据包
iptables -A FORWARD -p ALL -m state --state
ESTABLISHED,RELATED -j ACCEPT
```

### (5) OUTPUT 规则

```bash
# 本地流量
iptables -A OUTPUT -p ALL -s 127.0.0.1 -j ACCEPT
```

### (6) POSTROUTING 规则

```bash
# NAT 伪装
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

## 管理 Fedora 和 RHEL

### 第三部分：

我将前面的脚本命令分为六部分。以下内容描述了这些部分：

**(1) 策略** — iptables -P 设置了 INPUT、OUTPUT 和 FORWARD 的默认策略。未匹配规则的数据包将被丢弃。

**(2) 自定义链** — 创建了一个名为 *okay* 的自定义链。下一行允许 SYN 数据包。紧接的一行允许状态为 ESTABLISHED 或 RELATED 的 TCP 数据包。最后一行则丢弃其他所有 TCP 数据包。

**(3) INPUT 链规则** — 大部分输入过滤在 INPUT 链中完成。第一条规则允许来自局域网 (10.0.0.0/24) 的所有协议。允许来自回环地址 (127.0.0.1)、防火墙 IP (10.0.0.1) 以及互联网 IP (123.45.67.89) 的流量。最后一条允许指向广播地址 (10.0.0.255) 的流量。

- **来自局域网的数据包** — iptables 允许来自局域网的流量。第一条规则允许源自局域网 IP 10.0.0.0/24 的所有协议。后续三条规则允许来自局域网 IP 地址的流量。最后一条允许指向有效目标地址的流量。
- **来自互联网的数据包** — iptables 接受与已建立连接的数据包。它接受直接请求防火墙 IP 地址 (123.45.67.89) 状态为 ESTABLISHED 或 RELATED 的包。
- **TCP 规则（新连接）** — 在这里你为想要向互联网提供的 TCP 服务开放端口。这些行中，你为 FTP 服务 (21)、安全 shell 服务 (22)、Web 服务 (80) 以及 IDENT 身份验证 (113) 开放了端口，后者对于某些协议可能是必要的。你没有立即接受这些请求，而是跳转到 *okay* 链，直到你进一步检查数据包格式是否正确。
- **UDP 规则** — iptables 接受来自 eth0 目标端口 53 的 UDP。
- **ICMP 规则** — iptables 接受来自 eth0 的类型为 8 的 ICMP 包。下一行允许来自 eth0 的类型为 11 的 ICMP 包。

**(4) FORWARD 链规则** — iptables 接受与已建立连接相关的数据包。

**(5) OUTPUT 规则** — iptables 允许源自 127.0.0.1 的本地流量。

**(6) POSTROUTING 规则** — NAT 伪装。

