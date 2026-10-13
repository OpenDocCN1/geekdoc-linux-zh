
现在，如果你想在像之前讨论的那样列出规则并确定编号的情况下删除它，只需执行以下操作：

```
/sbin/iptables -D input -t filter -s 192.168.1.0/24 -j DROP
```

这将删除该规则。

# 在链中插入新规则

要在特定链的特定位置插入新规则，语法为：

```
/sbin/iptables -I chain_name rule_number rule_parameters -j target
```

例如：

```
/sbin/iptables -I input 1 -s 192.168.1.254 -j ACCEPT
```

这会将规则插入到默认过滤表中 `input` 链的第1位置。

# 在链中替换规则

要在特定链的特定位置替换现有规则，语法为：

```
/sbin/iptables -R chain_name rule_number rule_parameters -j target
```

例如：

```
/sbin/iptables -R input 1 -s 192.168.1.254 -j ACCEPT
```

这将用新规则替换默认过滤表中 `input` 链中第一位置的规则。

# 第 20 章：防火墙、VPN 和 SSL 隧道

## 501

你可以使用 `iptables` 程序在数据包过滤防火墙中创建/修改/删除规则和策略。

# 创建 SOHO 数据包过滤防火墙

在当今工作世界中，小型办公/家庭办公室（SOHO）是一个普遍现象，小企业主和远程办公者比以往任何时候都多。数字用户线路（DSL）和电缆互联网的出现使得即使是最小的家庭办公室也能实现全天候互联网连接。PC硬件价格下降为 SOHO 创建众多网络提供了真实机会。在本节中，我将讨论 SOHO 如何创建一个简单的防火墙系统，以对那些有太多时间进行黑客攻击的外世界采取保护措施。

假设网络上有三台机器，且这三台机器如所示具有真实的静态 IP 地址。每台机器都有可以在互联网上路由的 IP 地址。假设你——作为 SOHO 管理员——决定将 Linux 机器变成防火墙，如图 20-1 所示。

![](img/177ab5b774eeb101e12de61f8616d71a_523_0.png)

图 20-1：SOHO 网络

Linux PC 配置了两个以太网接口（`eth0` 和 `eth1`）。`eth0` 连接到 DSL 路由器，它是一个真实的 IP 地址。Linux PC 的私有 LAN 接口（`eth1`）具有私有 IP（`192.168.1.254`），该 LAN 中的其他两个系统也具有私有 IP 地址。

# 第五部分：防火墙

在这种配置下，所有来自私有网络的出站 `ipv4` 包通过 Linux 防火墙机器流向外部；同样，所有来自互联网的入数据包通过防火墙机器进入私有网络。这台 Linux PC 必须实现以下功能：

- IP 转发，以允许数据包在 `eth0` 和 `eth1` 之间移动
- IP 伪装，将 LAN 的 IP 地址动态更改为自身的外部接口（`eth0`）地址用于外部
- 数据包过滤规则，以保护私有 LAN

启用 IP 转发非常简单。你可以简单地在 `/etc/rc.local` 脚本中添加命令，以便在启动 Linux 系统时启用 IP 转发。

```
/sbin/sysctl -w net.ipv4.conf.forwarding=1
```

你也可以从 shell 执行它以随时开启 IP 转发。由于你已经如上一节讨论的那样在内核中启用了 `netfilter` 支持，你可以使用 `iptables` 启用伪装和数据包过滤，如名为 `so-firewall.sh` 的脚本所示（列表 20-1）。

## 列表 20-1：soho-firewall.sh

```
#!/bin/sh
# iptables 程序的路径
IPTABLES=/sbin/iptables
# 私有 LAN 地址
INTERNAL_LAN="192.168.1.0/24"
# 私有 LAN 接口
INTERNAL_LAN_INTERFACE="eth1"
# 私有 LAN 接口地址
INTERNAL_LAN_INTERFACE_ADDR="192.168.1.254"
# 外部 LAN 接口
EXTERNAL_LAN_INTERFACE="eth0"
# 外部 LAN 接口地址
EXTERNAL_LAN_INTERFACE_ADDR="207.183.1.18"
# 清空所有规则
$IPTABLES -F
# 设置默认策略
$IPTABLES -P INPUT DENY
$IPTABLES -P OUTPUT REJECT
$IPTABLES -P FORWARD REJECT
# 启用环回接口
$IPTABLES -A INPUT lo -j ACCEPT
$IPTABLES -A OUTPUT lo -j ACCEPT
# 启用内部接口
$IPTABLES -A INPUT eth1 -j ACCEPT
# 启用外部接口
$IPTABLES -A OUTPUT eth0 -j ACCEPT
# 伪装
$IPTABLES -t nat -A POSTROUTING -s $INTERNAL_LAN -o $EXTERNAL_LAN_INTERFACE -j MASQUERADE
# 转发流量
$IPTABLES -A FORWARD -s $INTERNAL_LAN -o $EXTERNAL_LAN_INTERFACE -j ACCEPT
$IPTABLES -A FORWARD -d $INTERNAL_LAN -i $EXTERNAL_LAN_INTERFACE -j ACCEPT
```

# 第 20 章：防火墙、VPN 和 SSL 隧道

当 shell 脚本变量替换为相应的值时，该规则如下：

```
/sbin/iptables -A output -i eth0 -p tcp \
-s 207.183.233.18 1024-65535 \
-d 0/0 80 -j ACCEPT
```

此规则允许防火墙通过外部接口输出目标为任何 IP 地址且端口为 80 的 HTTP 数据包。`1024-65535` 范围指定了 浏览器可以使用连接中的任何非特权端口（即大于 0-1023 的端口），因此防火墙不会拦截具有此类源端口号的数据包。

同样，在脚本中使用以下行来接受来自外部接口的 HTTP 响应流量：

```
$IPTABLES -A input $EXTERNAL_LAN_INTERFACE -p tcp ! -y \
-s 0/0 80 \
-d $EXTERNAL_LAN_INTERFACE_ADDR 1024-65535 \
-j ACCEPT
```

在这种情况下，只要源端口是 HTTP (`80`)，从外部 Web 服务器通过目的地的外部 IP 地址发送到防火墙外部接口的针对非特权端口的数据包就会被接受。

如你所见，开启双向连接需要你知道特定的服务运行在哪个端口。例如，假设你想允许外部访问你私有网络中的 Web 服务器。

## 允许外部 浏览器访问防火墙上的 Web 服务器

在防火墙上运行 Web 服务器不是一个好主意，但对于 SOHO 而言从资源角度可能是必要的。在这种情况下，你希望执行以下操作：

- 创建一条规则，允许任何 IP 连接到防火墙机器外部接口的 HTTP 端口。
- 创建一条规则，当源 IP 为任何 IP 且源端口为 HTTP (`80`) 时，允许防火墙/Web 服务器响应非特权端口（Web 客户端用于客户端连接的端口）。

以下行添加到 `soho-firewall.sh` 脚本中实现这些规则。

```bash
# 允许任何 IP 连接到防火墙外部接口
# 以向内部网络发送 HTTP 请求
$IPTABLES
 -A input -i $EXTERNAL_LAN_INTERFACE
 -p tcp ! -y \
 -s 0/0 1024-65535 \
 -d $EXTERNAL_LAN_INTERFACE_ADDR 80 \
 -j ACCEPT
```

# 允许内部 HTTP 响应通过防火墙的外部接口传到世界

```bash
$IPTABLES
 -A output -i $EXTERNAL_LAN_INTERFACE
 -p tcp \
 -s $EXTERNAL_LAN_INTERFACE_ADDR 80 \
 -d 0/0 1024-65535 \
 -j ACCEPT
```

如果你想启用 HTTPS（安全 HTTP）连接，请添加以下行：

- # 启用入站 HTTPS 连接

```bash
$IPTABLES
 -A input -i $EXTERNAL_LAN_INTERFACE
 -p tcp ! -y \
 -s 0/0 443 \
 -d $EXTERNAL_LAN_INTERFACE_ADDR 1024-65535 \
 -j ACCEPT
```

- # 启用出站 HTTPS 连接
