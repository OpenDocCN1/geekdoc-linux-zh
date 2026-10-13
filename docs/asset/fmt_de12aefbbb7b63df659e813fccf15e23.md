
`$IPT -A IN_NETWORK -p tcp -m state --state ESTABLISHED,RELATED -j ACCEPT`

`$IPT -A IN_NETWORK -p udp -m state --state ESTABLISHED,RELATED -j ACCEPT`

if [ "`$SMTMIP`" != "" ]
then
  `$IPT -A IN_NETWORK -p tcp --syn -d $SMTMIP --dport 25 -j ACCEPT`
fi

if [ "`$DNSIP`" != "" ]
then
  `$IPT -A IN_NETWORK -p udp -d $DNSIP --dport 53 -j ACCEPT`
fi

if [ "`$HTTPIP`" != "" ]
then
  `$IPT -A IN_NETWORK -p tcp --syn -d $HTTPIP --dport 80 -j ACCEPT`
fi

if [ "`$POPPIP`" != "" ]
then
    `$IPT -A IN_NETWORK -p tcp --syn -d $POPPIP --dport 110 -j ACCEPT`
fi

# AUTH 服务未运行——通常它不应该运行——
# TCP/IP 栈将向客户端响应 TCP RST 包，
# 有效地拒绝连接。因此，即使没有服务运行，
# 开放此端口也是合理的。
#

if [ "`$AUTH`" != "" ]
then
    `$IPT -A IN_NETWORK -p tcp --syn -d $AUTH --dport 113 -j ACCEPT`
fi

if [ "`$IMPIP`" != "" ]
then
    `$IPT -A IN_NETWORK -p tcp --syn -d $IMPIP --dport 143 -j ACCEPT`
fi

# 来自保护网络的出站流量
#

`$IPT -N OUT_NETWORK`
`$IPT -A OUT_NETWORK -p icmp -j OUT_ICMP`
`$IPT -A OUT_NETWORK -p tcp -j TCP_FLAGS`
`$IPT -A OUT_NETWORK -m state --state ESTABLISHED,RELATED -j ACCEPT`

# 以下六条规则允许运行在保护网络上的客户端
# 连接到远程服务器。通过添加和删除规则来自定义
# 授权的服务。

`$IPT -A OUT_NETWORK -m state --state NEW -p tcp --dport 21 -j ACCEPT`
`$IPT -A OUT_NETWORK -m state --state NEW -p tcp --dport 22 -j ACCEPT`
`$IPT -A OUT_NETWORK -m state --state NEW -p tcp --dport 25 -j ACCEPT`
`$IPT -A OUT_NETWORK -m state --state NEW -p tcp --dport 80 -j ACCEPT`
`$IPT -A OUT_NETWORK -m state --state NEW -p tcp --dport 443 -j ACCEPT`
`$IPT -A OUT_NETWORK -m state --state NEW -p udp --dport 53 -j ACCEPT`

--------------------------------------------------------------------------------
# 进入防火墙入站流量

```bash
$IPT -N IN_NETWORK
$IPT -A IN_NETWORK -p icmp -j IN_ICMP
$IPT -A IN_NETWORK -p tcp -j TCP_FLAGS
$IPT -A IN_NETWORK -p tcp --syn -j SYN_FLOOD
$IPT -A IN_NETWORK -p tcp -m state --state ESTABLISHED,RELATED -j ACCEPT
$IPT -A IN_NETWORK -p udp -m state --state ESTABLISHED,RELATED -j ACCEPT

if [ "$SMTMIP" != "" ]
then
  $IPT -A IN_NETWORK -p tcp --syn -d $SMTMIP --dport 25 -j ACCEPT
fi

if [ "$DNSIP" != "" ]
then
  $IPT -A IN_NETWORK -p udp -d $DNSIP --dport 53 -j ACCEPT
fi

if [ "$HTTPIP" != "" ]
then
  $IPT -A IN_NETWORK -p tcp --syn -d $HTTPIP --dport 80 -j ACCEPT
fi

if [ "$POPPIP" != "" ]
then
    $IPT -A IN_NETWORK -p tcp --syn -d $POPPIP --dport 110 -j ACCEPT
fi

# AUTH 服务未运行——通常它不应该运行——
# TCP/IP 栈将向客户端响应 TCP RST 包，
# 有效地拒绝连接。因此，即使没有服务运行，
# 开放此端口也是合理的。
#

if [ "$AUTH" != "" ]
then
    $IPT -A IN_NETWORK -p tcp --syn -d $AUTH --dport 113 -j ACCEPT
fi

if [ "$IMPIP" != "" ]
then
    $IPT -A IN_NETWORK -p tcp --syn -d $IMPIP --dport 143 -j ACCEPT
fi

# 来自保护网络的出站流量
#

$IPT -N OUT_NETWORK
$IPT -A OUT_NETWORK -p icmp -j OUT_ICMP
$IPT -A OUT_NETWORK -p tcp -j TCP_FLAGS
$IPT -A OUT_NETWORK -m state --state ESTABLISHED,RELATED -j ACCEPT

#
# 以下六条规则允许运行在保护网络上的客户端
# 连接到远程服务器。通过添加和删除规则来自定义
# 授权的服务。

$IPT -A OUT_NETWORK -m state --state NEW -p tcp --dport 21 -j ACCEPT
$IPT -A OUT_NETWORK -m state --state NEW -p tcp --dport 22 -j ACCEPT
$IPT -A OUT_NETWORK -m state --state NEW -p tcp --dport 25 -j ACCEPT
$IPT -A OUT_NETWORK -m state --state NEW -p tcp --dport 80 -j ACCEPT
$IPT -A OUT_NETWORK -m state --state NEW -p tcp --dport 443 -j ACCEPT
$IPT -A OUT_NETWORK -m state --state NEW -p udp --dport 53 -j ACCEPT
```

# 第11部分：防火墙的设计与实现
# 列表 10-3（续）

```bash
$IPT -A OUT_ICMP -p icmp --icmp-type echo-request -d $dip -j ACCEPT
$IPT -A OUT_ICMP -p icmp --icmp-type echo-reply -d $dip -j ACCEPT
done

# 对于一个不那么礼貌——但可能更安全的防火墙，
# 将后续规则中的 destination-unreachable 替换为 fragmentation-needed。

$IPT -A OUT_ICMP -p icmp --icmp-type destination-unreachable -j ACCEPT
$IPT -A OUT_ICMP -p icmp --icmp-type source-quench -j ACCEPT

# 对于一个不那么礼貌——但可能更安全的防火墙，
# 删除 parameter-problem 规则。

$IPT -A OUT_ICMP -p icmp --icmp-type parameter-problem -j ACCEPT
```
