
# 禁用源路由数据包
```bash
for i in /proc/sys/net/ipv4/conf/*accept_source_route; do
echo 0 > $i
done
```

# 这些模块对于伪装它们各自的服务是必要的。
```bash
/sbin/modprobe_ip_masq_ftp.o
/sbin/modprobe_ip_masq_radio.o ports=554,7070,7071,69270,69271
/sbin/modprobe_ip_masq_irc.o
/sbin/modprobe_ip_masq_volive.o
/sbin/modprobe_ip_masq_cuseeme.o
/sbin/modprobe_ip_masq_quake.o
```

# 回环接口 (LOOPBACK)
```bash
```

# 回环接口上的允许无限流量。
```bash
ipchains -A input -i $LOOPBACK_INTERFACE -j ACCEPT
ipchains -A output -i $LOOPBACK_INTERFACE -j ACCEPT
```

# 网络幽灵
# 拒绝讨厌鬼的访问
```bash
```

# /etc/rc.drc/firewall.blocked 包含一个列表
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s address -j DENY
# 用于拦截来自任何地址的规则。
```

# 拒绝来自问题站的任何连接
```bash
if [ -f /etc/rc.drc/firewall.blocked ]; then
  ./etc/rc.drc/firewall.blocked
fi
```

# 伪骗与错误地址
# 拒绝伪造的数据包。
# 忽略明显非法的源地址。
# 保护免受伪造地址的攻击。
```bash
```

# 拒绝假称来自外部地址的伪造数据包。
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $IPADDR -j DENY
```

# 拒绝声称来自 Class A 私有网络的数据包
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_A -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -d $CLASS_A -j DENY
ipchains -A output -i $EXTERNAL_INTERFACE -s $CLASS_A - REJECT
ipchains -A output -i $EXTERNAL_INTERFACE -d $CLASS_A -j REJECT
```

# 拒绝声称来自 Class B 私有网络的数据包
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_B -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -d $CLASS_B -j DENY
© Copyright 1999 Open Network Architecture
132 关于本页面的意见可以邮件至 gmourani@videotron.ca
ipchains -A output -i $EXTERNAL_INTERFACE -s $CLASS_B -j REJECT
ipchains -A output -i $EXTERNAL_INTERFACE -d $CLASS_B -j REJECT
```

# 拒绝声称来自 Class C 私有网络的数据包
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_C -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -d $CLASS_C -j DENY
```

# 拒绝声称来自回环接口的数据包
```bash
ipchains -A input -i $LOOPBACK -j DENY
ipchains -A output -i $LOOPBACK -j REJECT
```

# 过滤广播地址数据包
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $BROADCAST_DEST -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -d $BROADCAST_SRC -j DENY
```

# Class D 多播地址
# 作为源地址时是非法的。
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_D_MULTIC -j DENY
```

# Class E 保留地址
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s $CLASS_E_RESERVED_NET -j DENY
```

# 拒绝由 IANA 定义的地址
# 0.*, 1.*, 5.*, 23.*, 27.*,
# 31.*, 39.*, 41.*, 42.*, 58.*, 60.*,
# 65.*, 95.*, 96.*, 192.*, 201.*, 217.*
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 0.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 1.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 5.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 23.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 27.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 31.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 39.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 41.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 42.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 58.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 60.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 65.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 95.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 96.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 192.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 201.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 217.0.0/8 -j DENY
```

# 65: 01000000 /3 包含了 65-79
```bash
ipchains -A input -i $EXTERNAL_INTERFACE -s 65.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 66.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 67.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 68.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 69.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 70.0.0/8 -j DENY
ipchains -A input -i $EXTERNAL_INTERFACE -s 71.0.0/8 -j DENY
```
