

## 23.5 IP 伪装 (MASQUERADING)

3. 设置规则本身，记住规则是顺序处理的，并且在匹配到第一项后不再继续。

- `ipfwadm-[FOIA] -a <accept | deny | reject | masquerade> [-V interface IP | -W interface name] -S <source IP> -D <destination IP>`

-a 选项是规则列表的选项，后面应跟一个策略。有效的策略有 accept、deny、reject 和 masquerade。注意：这不适用于计费规则（Accounting rules）。

-V 和 -W 选项可选的。它们指定了该规则数据包将在哪个接口上传输或接收。如果没有指定，则假设数据包将在所有接口上被接受。可以使用 -V（IP 数字）或 -W（接口名称），但不能同时使用。-S 和 -D 分别指数据包的源（Source）和目的（Destination）。源 IP 和目的 IP 可以是点分四位数字或主机名。我建议使用 IP，因为这样不需要查找。

接下来的页面包含了简单伪装防火墙的描述，对入侵者提供了轻微的保护。如果需要更深入的信息，请阅读 ipfwadm 的 man 页面，或许还有许多专门针对防火墙的书籍。大多数书籍不会专门讨论 ipfwadm，但会提供可以应用于你的 Linux 机器的理论。

下面是一个 /etc/rc.d/rc.firewall 示例。像拨号（dial）一样，你应该在 rc.local 中调用它。

```bash
#!/bin/sh

PATH=/sbin/bin:/usr/sbin:/usr/bin

#
# /etc/rc.d/rc.firewall, 定义防火墙配置，
# 从 rc.local 调用。
#
PATH=/sbin/bin:/usr/sbin:/usr/bin
MY_ETH0=192.168.1.1
MY_NET=192.168.1.0
MY_STATIC=111.222.333.444

# 转发规则
# 首先清除内存中的任何旧规则
ipfwadm -F -f
# 然后设置默认策略为拒绝所有
ipfwadm -F -p deny
```

```bash
# 最后，我们想要对来自 MY_NET (eth0) 的 IP 进行伪装
# ppp0 接口（但我们可能需要在 s0
# 接口停止，如果拨号的话需要启动 ppp 连接！）
ipfwadm -F -a masquerade -W ppp0 -S $MY_NET/24 -D 0.0.0.0/0
ipfwadm -F -a masquerade -W s0 -S $MY_NET/24 -D 0.0.0.0/0
```

```bash
# 入站规则
# 首先，从内存中清除所有规则
ipfwadm -I -f
# 然后设置默认策略为拒绝所有
ipfwadm -I -p deny
```

```bash
# 允许从本地网络（只能是 eth0）进入
# 其他地方的数据包
ipfwadm -I - accept -W eth0 -S $MY_NET/24 -D 0.0.0.0/0
```

```bash
# 拒绝来自外部的、伪装成来自我本地网络的数据包
ipfwadm -I -a deny -W ppp0 -S $MY_NET/24 -D 0.0.0.0/0
```

```bash
# 对于从远程网络发往防火墙的数据包是有效的
#（即，如果我们使用该防火墙机器发送邮件，或者有人
# 合法地 telnet 进入防火墙）
ipfwadm -I -a accept -W ppp0 -S 0.0.0.0/0 -D $MY_STATIC/32
```

```bash
# 我们可能也使用 localhost 进行测试，使其有效
ipfwadm -I -a accept -V 127.0.0.1 -S 0.0.0.0/0 -D 0.0.0/0
```

```bash
# 出站规则（基本上是入站规则的反向）
# 通常，清除所有旧规则
ipfwadm -O -f
# 并设置拒绝默认策略
ipfwadm -O -p deny
```

```bash
ipfwadm -O -a accept -W eth0 -S 0.0.0.0/0 -D $MY_NET/24
```

```bash
# 拒绝尝试伪装的
ipfwadm -O -a deny -W ppp0 -S 0.0.0.0/0 -D $MY_NET/24
ipfwadm -O -a deny -W ppp0 -S $MY_NET/24 -D 0.0.0/0
ipfwadm -O -a deny -W ppp0 -S 0.0.0/0 -D $MY_NET/24
```

```bash
# 防火墙的所有出站数据都是有效的，
# 记得，我们需要让 sl0 有效，
# 还没有启用 ppp0。
ipfwadm -O -a accept -W ppp0 -S $MY_STATIC/32 -D 0.0.0/0
ipfwadm -O -a accept -W s0 -S $MY_STATIC/32 -D 0.0.0/0
```

```bash
# 还有... localhost 仍然有效
ipfwadm -O -a accept -V 127.0.0.1 -S 0.0.0.0/0 -D 0.0.0/0
```

echo "done"

下面是一个 /etc/rc.d/rc.firewallAccounting 示例。这个脚本应该保持独立，这样你就可以在重启它时不干扰防火墙的其他部分。另一种方法是将所有计费规则设置为 0 字节，但这允许你轻松地从计费列表中删除机器。该脚本期望一个名为 /FirewallAcctList 的文件，其中包含你想监控的机器列表。要监控流量，可以创建一个 cron任务通过邮件查看防火墙计费的输出。

```bash
#!/bin/sh

PATH=/sbin/bin:/usr/sbin:/usr/bin

#
# /etc/rc.d/rc.firewall, 定义防火墙配置，
# 从 rc.local 调用。
#
PATH=/sbin/bin:/usr/sbin:/usr/bin
MY_ETH0=192.168.1.1
MY_NET=192.168.1.0
MY_STATIC=111.222.333.444

echo -n "Starting accounting rules:"

# 杀死旧规则
ipfwadm -F -f
# 这些是系统规则！！记录所有流量作为参考
ipfwadm -A in -i -S $MY_NET/24 -D 0.0.0.0/0
ipfwadm -A out -i -S 0.0.0.0/0 -D $MY_NET/24

ipfwadm -A in -i -S $MY_NET/24 -D $MY_ETH0/32
ipfwadm -A out -i -S $MY_ETH0/32 -D $MY_NET/24

# 这些用于记录到名为
# FirewallAcctList 的单独机器...只是一个 IP 列表
for i in $(cat /FirewallAcctList); do
	echo -n "$i"
	ipfwadm -A in -i -S $i/32 -D 0.0.0/0
	ipfwadm -A out -i -S 0.0.0.0/0 -D $i/32
done
echo "done"
```

## 23.6 总结

当以安全的方式将局域网连接到互联网时，有几点需要考虑：首先，选择私有（可路由）网络。其次，通过按需拨号线路将你的防火墙机器连接到互联网。最后，允许局域网某些机器并拒绝访问。

## 附录

以下是书中引用的 URL 列表。这些 URL 包含了章节中使用程序的信息。

### 5. 网络
- Netalk: http://www.umich.edu/~rsug/netalk/ (通用)
- 打印: http://www.giubille.ch/~eugster/appleprint.html
- BIND: ftp://ftp.isc.org/bind

### 7. 电子邮件
- IMAP: http://www.imap.org
- Sendmail 首页: http://www.sendmail.org/
- Qmail: http://www.qmail.org

### 8. 互联网机构
- InterNIC: http://www.internic.net/
- 顶级域名: http://www.isi.edu/iana/domain-names.html
- CERT: http://www.cert.org/

### 9. Samba
- Samba: http://lake.canberra.edu.au/pub/samba.html
- Microsoft: http://www.microsoft.com/

### 10. 网络新闻
- 补丁: http://thereisnocabal.errols.com/

