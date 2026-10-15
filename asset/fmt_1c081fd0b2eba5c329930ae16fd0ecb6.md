
```bash
ipchains -A input -i EXTERNAL_INTERFACE -p tcp --state ! EST \
  -s $NAMESERVER_1.53 \
  -d $IPADDR $UNPRIVORTS -j ACCEPT
```

# TCP 仅在选定端口上接受

## SSH 服务器 (22)

```bash
ipchains -A input -i EXTERNAL_INTERFACE -p tcp \
  -s $ANYWHERE $UNPRIVORTS \
  -d $IPADDR 22 -j ACCEPT
```

```bash
ipchains -A output -i EXTERNAL_INTERFACE -p tcp --state ! EST \
  -s $IPADDR 22 \
  -d $ANYWHERE $UNPRIVORTS -j ACCEPT
```

```bash
ipchains -A input -i EXTERNAL_INTERFACE -p tcp \
  -s $ANYWHERE $SSH_PORTS \
  -d $IPADDR 22 -j ACCEPT
```

```bash
ipchains -A output -i EXTERNAL_INTERFACE -p tcp --state ! EST \
  -s $IPADDR 22 \
  -d $ANYWHERE $SSH_PORTS -j ACCEPT
```

## AUTH 服务器 (13)

### 拒绝（Reject）而不是丢弃（Deny）入站端口。

```bash
ipchains -A input -i EXTERNAL_INTERFACE -p tcp \
  -s $ANYWHERE \
  -d $13 -j REJECT
```

## syslog 服务器 (54)

### 此功能允许来自一个主机的日志记录。

```bash
ipchains -A input -i EXTERNAL_INTERFACE -p udp \
  -s $ANYWHERE \
  -d $54
```

## syslog 客户端 (54)

```bash
ipchains -A output -i EXTERNAL_INTERFACE -p udp \
  -s $ANYWHERE \
  -d $54 -j
```

## SMTP 服务器 (25)

```bash
ipchains -A input -i EXTERNAL_INTERFACE -p tcp \
  -s $ANYWHERE \
  -d $25 -j ACCEPT
```

## SMTP 客户端 (25)

```bash
ipchains -A output -i EXTERNAL_INTERFACE -p tcp --state ! EST
  -s $ANYWHERE \
  -d $ACCEPT
```

## IMAP 服务器 (143)

```bash
ipchains -A input -i EXTERNAL_INTERFACE -p tcp \
  -s $ANYWHERE \
  -d $143 -j ACCEPT
```

## IMAP 客户端 (143)

```bash
ipchains -A output -i EXTERNAL_INTERFACE -p tcp --state ! EST
  -s $ANYWHERE \
  -d $ACCEPT
```

## POP3 服务器 (110)

```bash
ipchains -A input -i EXTERNAL_INTERFACE -p tcp \
  -s $ANYWHERE \
  -d $110 -j ACCEPT
```

## POP3 客户端 (110)

```bash
ipchains -A output -i EXTERNAL_INTERFACE -p tcp --state ! EST
  -s $ANYWHERE \
  -d $ACCEPT
```

## UDP 入站 TRACEROUTE

### traceroute 使用 -S 32769 65535-0 33434:33523

```bash
iptables -A input -i $EXTERNAL_INTERFACE -p udp \
-s SMY_ISP TRACEROUTE_SRC_PORTS -j ACCEPT
iptables -A input -i $EXTERNAL_INTERFACE -p udp \
-s ANYWHERE TRACEROUTE_SRC_PORTS -j ACCEPT \
-d SIPADADDR TRACEROUTE_DEST_PORTS -j DENY
```

## 为丢弃的数据包启用日志

```bash
iptables -A input -i $EXTERNAL_INTERFACE -p tcp \
-s ANYWHERE \
-d $DENY -j LOG
```

```bash
iptables -A input -i $EXTERNAL_INTERFACE -p udp \
-s ANYWHERE \
-d $DENY -j LOG
```

```bash
iptables -A input -i $EXTERNAL_INTERFACE -p icmp \
-s ANYWHERE 5 -d $DENY -j LOG
```

```bash
iptables -A input -i $EXTERNAL_INTERFACE -p icmp \
-s ANYWHERE 13:255 -d $DENY -j LOG
```

```bash
case $1 in
  stop)
    echo -n "Shutting Firewall Services: "
    # 移除属于此过滤器的现有规则
    iptables -F

    # 删除此过滤器的自定义链
    iptables -X

    # 将过滤器的默认策略重置为接受。
    iptables -P input ACCEPT
    iptables -P output ACCEPT
    iptables -P forward
    ;;
  start)
    echo -n "Starting Firewall Services: "
    # (此处可添加启动逻辑)
    ;;
  status)
    iptables -L
    ;;
  restart|reload)
    $0 stop
    $0 start
    ;;
  *)
    echo "Usage: $0 {start|stop|status|restart}"
    exit 1
    ;;
esac
```

现在，使此脚本可执行并更改其默认权限：

```
[root@deep #] chmod 700 /etc/rc.d/init.d/firewall
```

```
[root@deep #] chmod 000 /etc/rc.d/init.d/firewall
```

通过以下命令为防火墙创建符号 rc 链接：

```
[root@deep #] chkconfig --add firewall
```

```
[root@deep #] chkconfig --level 34 firewall
```

现在，您的防火墙规则配置为使用 System V init（System vit 负责启动启动时运行的所有正常进程），并且在每次服务器重启时它会自动启动。

- 手动停止防火墙，请使用以下命令：

```
[root@deep #] /etc/rc.d/init.d/firewall stop
```

Shutting Firewall Services: [ OK ]

- 手动启动防火墙，请使用以下命令：

```
[root@deep #] /etc/rc.d/init.d/firewall start
```

Starting Firewall Services: [ OK ]

# Linux 伪装与转发

## 第 8 章

阅读内容：

`FORWARD_IPV4="yes"`

- 你必须重启网络才能使更改生效：

```
[root@]# ip /etc/rc.d/init.d/network restart
```

启动接口 lo [ OK ]

启动接口 eth0 [ OK ]

启动接口 eth1 [ OK ]

因此，你可以使用 `echo "1" > /proc/sys/net/ipv4/forward` 命令行将其写入你的 "`rc.local`" 脚本文件中，或者在 "`network`" 文件中将 "`FORWARD_IPV4=false`" 这一行的值改为 "`yes`" 来开启此功能。我个人更偏于使用后种代码。

## 在 RedHat Linux 6.2 下

- 若欲在你的 RH 6.2 系统上启用 IPv4 转发，请使用以下命令：

编辑 "`/etc/sysctl.conf`" 文件并添加以下行：

```bash
# Enable数据包转发
net.ipv4.ip_forward = 1
```

你必须重启网络才能使更改生效。重启网络的命令如下：
