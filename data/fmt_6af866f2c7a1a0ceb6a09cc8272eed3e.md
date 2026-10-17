
# 第 9 章：IPTables 防火墙 293

## 封禁主机

```
$IPT -N SHUN
for ip in $SHUNIP; do
  $IPT -A SHUN -s $ip -j LSHUN
  $IPT -A SHUN -d $ip -j LSHUN
done
```

## SYN 洪水攻击防护 (TCP SYN 报文)

```
$IPT -N FLOOD
```

接续规则允许以限制速率的报文通过。

```
$IPT -A FLOOD $SYNOP -j RETURN
$IPT -A FLOOD -j LFLOOD
```

## TCP 标志校验 (TCP 报文)

```
$IPT -N FLAGS
$IPT -A FLAGS -p tcp --tcp-flags ACK,FIN FIN -j LFLAGS
$IPT -A FLAGS -p tcp --tcp-flags ACK,PSH PSH -j LFLAGS
$IPT -A FLAGS -p tcp --tcp-flags ACK,URG URG -j LFLAGS
$IPT -A FLAGS -p tcp --tcp-flags FIN,RST,RST -j LFLAGS
$IPT -A FLAGS -p tcp --tcp-flags SYN,FIN,SYN -j LFLAGS
$IPT -A FLAGS -p tcp --tcp-flags SYN,RST,SYN -j LFLAGS
$IPT -A FLAGS -p tcp --tcp-flags ALL ALL -j LFLAGS
$IPT -A FLAGS -p tcp --tcp-flags ALL FIN,PSH,URG -j LFLAGS
$IPT -A FLAGS -p tcp --tcp-flags ALL SYN,FIN,PSH,URG -j LFLAGS
$IPT -A FLAGS -p tcp --tcp-flags ALL SYN,RST,ACK,FIN,URG -j LFLAGS
```

剩余的标志组合被视为有效的。

## 输入 TCP/UDP 报文。

继续

### 列表 9-13（继续）

```
$IPT -N IN
$IPT -A IN -m state --state INVALID -j LDORP
$IPT -A IN -p tcp --syn -j FLOOD
$IPT -A IN -p tcp -j FLAGS
$IPT -A IN -m state --state ESTABLISHED,RELATED -j ACCEPT
$IPT -A IN -s sip $sIP -j LDORP
```

接受新的入站连接。

```
for sip $SSH;
  $IPT -A IN -p tcp -s $sip -dport 22 -m state --state NEW -j ACCEPT
done
```

```
for sip $WWW;
  $IPT -A IN -p tcp -s $sip -dport 80 -m state --state NEW -j ACCEPT
done
```

拒绝 AUTH 请求

```
$IPT -A IN -p tcp --dport 113 -j REJECT --reject-with-tcp-reset
```

在此处添加允许授权流量的额外规则。

未被显式接受的流量将被记录并丢弃。

```
##################################################################
# 输出 TCP/UDP 报文
##################################################################
```

```
$IPT -N OUT
$IPT -A OUT -p tcp -j FLAGS
$IPT -A OUT -s ! $sIP -j LDORP
$IPT -A OUT -m state --state ESTABLISHED,RELATED -j ACCEPT
```

此防火墙配置为默认阻止出站连接。

要允许出站连接，请取消以下注释：

```
$IPT -A OUT -j ACCEPT
```

允许新的出站连接。

```
for sip $SSH;
  $IPT -A OUT -p tcp -s $sip -dport 22 -m state --state NEW -j ACCEPT
done
```

```
for sip $WWW;
  $IPT -A OUT -p tcp -s $sip -dport 80 -m state --state NEW -j ACCEPT
done
```

允许特定的出站流量。

在此处添加允许授权流量的额外规则。

未被显式接受的流量将被记录并丢弃。

##################################################################

# 输出 TCP/UDP 报文

##################################################################

```
$IPT -N OUT
$IPT -A OUT -p tcp -j FLAGS
$IPT -A OUT -s ! $sIP -j LDORP
$IPT -A OUT -m state --state ESTABLISHED,RELATED -j ACCEPT
```

此防火墙配置为默认阻止出站连接。

```
$IPT -A OUT -j ACCEPT
```

允许新的出站连接。

```
for sip $SSH;
  $IPT -A OUT -p tcp -s $sip -dport 22 -m state --state NEW -j ACCEPT
done
```

```
for sip $WWW;
  $IPT -A OUT -p tcp -s $sip -dport 80 -m state --state NEW -j ACCEPT
done
```

允许特定的出站流量。

在此处添加允许授权流量的额外规则。

未被显式接受的流量将被记录并丢弃。

##################################################################

# 输出 TCP/UDP 报文

##################################################################

```
$IPT -N OUT
$IPT -A OUT -p tcp -j FLAGS
$IPT -A OUT -s ! $sIP -j LDORP
$IPT -A OUT -m state --state ESTABLISHED,RELATED -j ACCEPT
```

此防火墙配置为默认阻止出站连接。

```
$IPT -A OUT -j ACCEPT
```

允许新的出站连接。

```
for sip $SSH;
  $IPT -A OUT -p tcp -s $sip -dport 22 -m state --state NEW -j ACCEPT
done
```

```
for sip $WWW;
```
