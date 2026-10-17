
# 赋值

## 防火墙主机 IP 地址

`IP="xxx.xxx.xxx.xxx"`

## 入站服务的主机列表

`PING=""`
`SSH="0.0.0.0/0"`
`WWW="0.0.0.0/0"`

## 速率限制

`SYNOPT="--m limit --limit 5/second --limit-burst 10"`
`LOGOPT="--log-level -3 m limit --limit 1/second --limit-burst 10"`

## 以下赋值通常不需要更改

`BADIP="0.0.0.0/8 10.0.0.0/8 169.254.0.0/16 172.16.0.0/16 192.0.0.0/24 192.168.0.0/16 192.0.34.0/24 240.0.0.0/4 255.255.255.255"`
`SHUN=""`
`LO="127.0.0.1"`
`SSH="$SSH LO"`

`WWW="$WWW $LO"`
`IPT=/sbin/iptables`

# 清除现有的防火墙规则

```
if [ ! -x $IPTABLES ]
then
    echo "firewall: can't execute $IPTABLES"
    exit 1
fi

IPT -P INPUT DROP      # 设置默认策略为 DROP
IPT -P OUTPUT DROP     # 设置默认策略为 DROP
IPT -P FORWARD DROP    # 设置默认策略为 DROP
IPT -F                 # 清空所有链
IPT -X                 # 删除所有链
```

```bash
for table in filter mangle
do
    IPT -t table -F         # 删除表的规则
    IPT -t table -X         # 删除表的链
    IPT -t table -Z         # 重置表的计数器
done
```

# 日志链

```bash
IPT -N LDROP
IPT -A LDROP -j LOG --log-prefix "IPT: "
IPT -A LDROP -j DROP
IPT -N BADIP
IPT -A BADIP -j LOG --log-prefix "IPT: "
IPT -A BADIP -j DROP
IPT -N SHUN
IPT -A SHUN -j LOG --log-prefix "IPT Shun: "
IPT -A SHUN -j DROP
IPT -N FLOOD
IPT -A FLOOD -j LOG --log-prefix "IPT Flood: "
IPT -A FLOOD -j DROP
```

# 规则应用

```bash
IPT -A INPUT -i lo -j ACCEPT
IPT -A INPUT -p udp -s xxx.xxx.xxx.xxx --sport 53 -j ACCEPT
IPT -A INPUT -p tcp --syn -j REJECT
IPT -A INPUT -p udp -j REJECT
IPT -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
IPT -A INPUT -m state --state INVALID -j LDROP
IPT -A INPUT -s $BADIP -j BADIP
IPT -A INPUT -s $SHUN -j SHUN
IPT -A INPUT -s $LO -j ACCEPT
IPT -A INPUT -s $SSH -j SSH
IPT -A INPUT -s $WWW -j WWW
IPT -A INPUT -p tcp --dport 113 -j REJECT --reject-with tcp-reset
```

## 附录 E：示例防火墙脚本

```bash
IPT -N OUT_ICMP
for dip in $PING; do
IPT -A OUT_ICMP -p icmp --icmp-type echo-reply -d $dip -j ACCEPT
IPT -A OUT_ICMP -p icmp --icmp-type echo-request -d $dip -j ACCEPT
done
IPT -A OUT_ICMP -p icmp --icmp-type destination-unreachable -j ACCEPT
IPT -A OUT_ICMP -p icmp --icmp-type fragmentation-needed -j ACCEPT
IPT -A OUT_ICMP -p icmp --icmp-type source-quorum -j ACCEPT
IPT -A OUT_ICMP -p icmp --icmp-type parameter-problem -j ACCEPT
```

# 内置链规则

```bash
IPT -A INPUT -i lo -j ACCEPT
IPT -A INPUT -j BADIP
IPT -A INPUT -p ! icmp -j IN
IPT -A INPUT -p icmp -j IN_ICMP
IPT -A INPUT -j LDROOP
```

```bash
IPT -A OUTPUT -o lo -j ACCEPT
IPT -A OUTPUT -j BADIP
IPT -A OUTPUT -j SHUN
IPT -A OUTPUT -p ! icmp -j OUT
IPT -A OUTPUT -p icmp -j OUT_ICMP
IPT -A OUTPUT -j LDROOP
```

## IPTables 屏幕网络防火墙（第 10 章）

```bash
#!/bin/sh
#
# 环境要求：
# /etc/sysctl.conf 中的 sysctl
# /etc/rc.local 中的 modprobes
```

# 屏幕网络防火墙

# 版权所有 (C) 2002 Bill McCarthy

## 附录 E：示例防火墙脚本 481

# 本程序是自由软件；你可以根据自由软件基金会发布的 GNU 2 版或更高版本的通用公共许可证条款重新分发和/或修改它。

# 分发本程序的目的是希望它可能有用，但不提供任何保证，即使是关于商品性或特定用途的适用性的暗示保证。详情请参阅通用公共许可证。

# 你应该在获取此程序时收到一份通用公共许可证副本，或者能够从程序的下载网站获取。如果，你可以从自由软件会的网站 www.gnu.org 获取。

---
# 分配
---

# 修改这些分配以符合你的网络架构必要的变量

`EXTDEV=eth0`
`EXTIP="192.0.34.2"`
`EXTBASE="192.0.34.0"`
`EXTBCAST="192.0.34.255"`
`EXTGATE="192.0.34.254"`
