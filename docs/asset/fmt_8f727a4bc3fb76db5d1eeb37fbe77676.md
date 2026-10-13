
`SSH`="192.168.34.2"

# 内部网络上每个公共服务器的 IP

`DNSIP`="10.0.0.2"

`HTTPPIP`="10.0.0.2"

`POPIP`="10.0.0.2"

`AUTHIP`="10.0.0.2"

`IMAPIP`="10.0.0.2"

# 未通信的主机和网络

# 以下赋值不需要更改

`BADIP`="$EXTBASE $EXTCAST 0.0.0/8 10.0.0/8 127.0.0/8 254.0.0/16 172.16.0/12 192.168.0.0/24 0.0.0/5"

`IPTABLES`=/sbin/iptables

`LOGOPT`="--log-level=3 -m limit 3/minute --burst 3"

`SYNOPT`="-m limit 5/second --burst 10"

--------------------------------------

# 清空现有的防火墙规则

--------------------------------------

```
if [ ! -x $IPTABLES ]; then
    die "firewall:t execute $IPTABLES"
```

```
iptables -P INPUT # 设置默认策略为 DROP
iptables -P OUTPUT # 设置默认策略为 DROP
iptables -P FORWARD # 设置默认策略为 DROP
iptables -F # 清空所有链
iptables -X # 删除所有链
```

```
for table in nat mangle; do
    iptables -t $table -F # 删除表的规则
    iptables -t $table -X # 删除表的链
    iptables -t $table -Z # 清零表的计数器
done
```

--------------------------------------

# 错误的 TCP 标志

--------------------------------------

```
iptables -N BADFLAGS
iptables -A BADFLAGS -j LOG --log-prefix "IPTFLAGS: " $LOGOPT
iptables -A BADFLAGS -j DROP
```

--------------------------------------

# TCP 标志验证

--------------------------------------

```
iptables -N TCP_FLAGS
iptables -A TCP_FLAGS -p tcp --tcp-flags ACK,FIN -j BADFLAGS
iptables -A TCP_FLAGS -p tcp --tcp-flags ACK,PSH -j BADFLAGS
iptables -A TCP_FLAGS -p tcp --tcp-flags ACK,URG -j BADFLAGS
iptables -A TCP_FLAGS -p tcp --tcp-flags FIN,RST -j BADFLAGS
iptables -A TCP_FLAGS -p tcp --tcp-flags SYN,FIN -j BADFLAGS
iptables -A TCP_FLAGS -p tcp --tcp-flags SYN,RST -j BADFLAGS
iptables -A TCP_FLAGS -p tcp --tcp-flags ALL ALL -j BADFLAGS
iptables -A TCP_FLAGS -p tcp --tcp-flags ALL NONE -j BADFLAGS
iptables -A TCP_FLAGS -p tcp --tcp-flags ALL FIN,PSH,URG -j BADFLAGS
iptables -A TCP_FLAGS -p tcp --tcp-flags ALL SYN,FIN,PSH,URG -j BADFLAGS
iptables -A TCP_FLAGS -p tcp --tcp-flags ALL RST,ACK,FIN,URG -j BADFLAGS
```

--------------------------------------

# SYN 洪水防护

--------------------------------------

```
iptables -N SYN_FLOOD
iptables -A SYN_FLOOD -p tcp --syn $SYNOPT -j RETURN
iptables -A SYN_FLOOD -p tcp ! -j RETURN
iptables -A SYN_FLOOD -p tcp --syn -j RETURN
iptables -A SYN_FLOOD -j LOG --log-prefix "IPT SYN_FLOOD: " $LOGOPT
iptables -A SYN_FLOOD -j DROP
```

--------------------------------------

# Bad IP 链

--------------------------------------

```
iptables -N BAD_IP
iptables -A BAD_IP -j LOG --log-prefix "IPT BAD_IP: " $LOGOPT
iptables -A BAD_IP -j DROP
```

--------------------------------------

# 屏蔽的主机

--------------------------------------

```
iptables -N SHUN
for ip in $SHUN; do
  iptables -A SHUN -s $ip -j BAD_IP
  iptables -A SHUN -d $ip -j BAD_IP
done
```

--------------------------------------

# 入站 IP 检查

--------------------------------------

```
iptables -N IN_IP_CHECK
for sip in $BADSIP
do
  iptables -A IN_IP_CHECK -s sip -j BAD_IP
done
iptables -A IN_IP_CHECK -i $EXTDEV -s $EXTIP -j BAD_IP
iptables -A IN_IP_CHECK -i $EXTDEV -s $INTNET -j BAD_IP
iptables -A IN_IP_CHECK -i $INTDEV -s $EXTIP -j BAD_IP
```

--------------------------------------

# 出站 IP 检查

--------------------------------------

```
iptables -N OUT_IP_CHECK
for dip in $BADSIP
do
  iptables -A OUT_IP_CHECK -d dip -j BAD_IP
done
iptables -A OUT_IP_CHECK -o $EXTDEV -s $EXTIP -j RETURN
iptables -A OUT_IP_CHECK -o $INTDEV -s $INTIP -j RETURN
iptables -A OUT_IP_CHECK -j BAD_IP
```

--------------------------------------

# 入站 ICMP

--------------------------------------

```
iptables -N IN_ICMP
for sip in $PING;
do
  iptables -A IN_ICMP -p icmp --icmp-type echo-request -s $sip -j ACCEPT
  iptables -A IN_ICMP -p icmp --icmp-type echo-reply -s $sip -j ACCEPT
done
iptables -A IN_ICMP -p icmp --icmp-type destination-unreachable -j ACCEPT
iptables -A IN_ICMP -p icmp --icmp-type source-quench -j ACCEPT
iptables -A IN_ICMP -p icmp --icmp-type time-exceeded -j ACCEPT
iptables -A IN_ICMP -p icmp --icmp-type parameter-problem -j ACCEPT
iptables -A IN_ICMP -j LOG --log-prefix "*IPT In ICMP: " $LOGOPTAG
iptables -A IN_ICMP -j DROP
```
