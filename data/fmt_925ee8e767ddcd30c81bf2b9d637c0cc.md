
进入`/path/to/xxx`目录，找到`xxx.json`。

然而，在这种情况下，我们还想表示我们指的不是专门分配了地址`192.168.1.0`的主机，而是指前三个数字（`192.168.1`）是有效的或固定的。最后一位是一种通配符。因此，我们指定：

```
192.168.1.0/24
```

这意味着`24`位（`192.168.1`）是有效的，而最后`8`位（在这种情况下为`0`）不是有效的，可以匹配任何数字。

## 基于状态的匹配

`iptables`新增了可以使用`state`模块根据数据包状态创建规则的功能。基于状态匹配创建规则的格式为：

```
iptables -m state --state [!] [state,state...]
```

四个可匹配的数据包状态如表`11.5`。

| 表 11.5 状态模块匹配 |
| 匹配 | 说明 |
| --- | --- |
| NEW | 匹配启动新连接的数据包。 |
| ESTABLISHED | 匹配属于已打开连接的数据包，这些包是对其他数据包的回应。 |
| RELATED | 匹配与另一个连接相关的包，例如过滤传输协议交换的数据段。 |
| INVALID | 匹配在现有连接上下文中没有意义的包，或者由于某些原因无法成功接收的包。 |

使用`iptables`和内核`2.4`根据状态信息匹配数据包的能力大大简化了数据包过滤过程。

## 一个实用的简单规则集

现在我们至少记录了`iptables`的命令语法和其运行的逻辑，可以开始添加在现实生活中管理数据包过滤的规则了。这是一个枯燥的过程，可能需要你花一些时间才能正确，特别是对于非常复杂的规则集。这里提供的示例对于大多数系统或内部用户有限的私有网络来说是相当安全的。尝试按照每条规则呈现的逻辑来操作，你就能顺利地创建出适用于你特定情况的自己的规则。

![](img/5b265b1d98ba2e1a657c3f9cdc5ce677_189_0.png)

这个简单规则集背后的想法是创建几种接受传入数据包的情况，并拒绝其他所有内容。我们不会尝试过滤传出的数据包，假设“内部”的每个人都是可信的且没有实施非法行为。我们可以使用连接状态匹配来开始我们的简单规则集，显式启用所有非绑定的 TCP：

```
iptables -t filter -A INPUT -m state \
--state ESTABLISHED,RELATED -j ACCEPT
```

因为状态匹配仅对 TCP 数据包有效，我们仍然需要为 UDP 数据包添加额外的规则。DNS 可能是当今互联网上最基础的服务，让我们允许名称服务器查询发生。假设我们名称服务器的 IP 地址存储在环境变量 `$DNS` 中，我们添加以下内容：

```
iptables -t filter -A INPUT udp -p $DNS \
--source-port domain -j ACCEPT
```

这四行代码为默认过滤表的 `INPUT` 链（传入流量）创建了规则，使得与现有连接相关的 TCP 包以及与域名服务（通过 `/etc/services`）相关的 UDP 包被接受。由于我们已经允许了已建立和相关的连接的 TCP 包，因此对于出的 Web 或 Ftp 流量不需要额外工作。

现在我们想要确保任何我们没有显式允许的数据包。在这个过程中，如果顺便做一些日志记录就好了。为此，我们添加：

```
iptables -N logden
iptables -t filter -A logden -j LOG \
--log-prefix "iptables: "
```

```
iptables -t filter -A logden -j DROP
iptables -t filter -A INPUT -i ! -m state \
  --state NEW,INVALID -j logden
```

首先，我们创建了一个名为 `logden` 的新用户自定义链。该链简单地记录数据包然后将其丢弃。我们在 `INPUT` 链中添加了一条规则，检查真实接口上的任何传入数据包，查看它们是否启动了新连接或无效的。如果是，数据包将被发送到 `logden` 链进行记录并丢弃。

## 伪装与 NAT

（注：原文此处存在大量重复的文本错误，翻译时已根据逻辑忽略重复部分。）

# 列表 11.1 iptables 脚本

```
#! /bin/bash

# 清空所有现有规则和用户自定义链

for TABLE in filter mangle; do

 iptables -t $TABLE -F

 iptables -t $TABLE -X

done

# 在此处添加你自己的 IP

MYIP=

## 如果适用，在此处添加你的内部网络掩码

INT=192.168.1.0/24

# 如果适用，在此处添加你的 Web 服务器地址

WEB=192.168.1.14

# 修改以反映你的网络环境

INTERNAL=eth1

EXTERNAL=eth0

# 允许我们发起的任何流量

iptables -t filter -A INPUT -m state \
--state ESTABLISHED,RELATED -j ACCEPT

## 查找 /etc/resolve.conf 中的域名；允许查询

for DNS in $(grep 'n' /etc/resolve.conf|awk '{print $2}'); do

 iptables -t filter -A INPUT -p udp -s DNS \
--source-port domain -j ACCEPT

# 如必要，允许入的 Web 流量

if [ "$WEB" = "" ]; then

 iptables -t filter -A INPUT -p tcp \
--source-port - -j ACCEPT

fi

# 拒绝记录登录以外的所有其他内容

iptables -t filter -A logdeny -j LOG \
--log-prefix "iptables":

 iptables -t filter -A logdeny -j DROP

iptables -t filter -A INPUT -i lo -m state \
--state NEW,INVALID -j logdeny

# 现在，如果必要，启用网络地址转换

if [ "$INT" = "" ]; then

 echo 1>/proc/sys/net/ipv4/ip_forward

 echo 1>/proc/sys/net/ipv4/conf/all/rp-filter

 if [ $EXTERNAL = pp0 ]; then

 iptables -t nat -A POSTROUTING -o $EXTERNAL
```

## 列表 11.1 继续

```
else

-j MASQUERADE

iptables -t nat -A POSTROUTING -o $EXTERNAL \
-j SNAT -nat to $MYIP

fi
```

```
# 设置并建立到我们 Web 服务器的端口转发

if [ "WEB" = "" ]; then

iptables -t nat -A PREROUTING -p tcp \
-d $MYIP --dport http -j DNAT --to $WEB:80

fi
```

```
## 脚本结束
