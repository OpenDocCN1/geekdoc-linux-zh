
- `$IPADDR` `$UNPRIPVPORTS` -j ACCEPT

`ipchains` -A output -i `$EXTERNAL_INTERFACE` -p tcp \
-s `$IPADDR` `$UNPRIPVPORTS` \
-d `$ANYWHERE` 7070:7071 -j ACCEPT

```
# UDP 是首选方法：6970:6999
# 对于域网机器，UDP 需要 RealAudio 伪装模块和
# ipmasqm 第三方软件。
```

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
-s $ANYWHERE $UNPRIPVPORTS \
-d $IPADDR 6970:6999 -j ACCEPT
```

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p udp \
-s $IPADDR $UNPRIPVPORTS \
-d $ANYWHERE $UNPRIPVPORTS -j ACCEPT
```

```bash
# WHOIS 客户端 (43)

# ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
-s $ANYWHERE 43 \
-d $IPADDR $UNPRIPVPORTS -j ACCEPT
```

```bash
# ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! \
-s $IPADDR $UNPRIPVPORTS \
-d $ANYWHERE 43 -j ACCEPT
```

```bash
# 出站追踪路由

# ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
-s $IPADDR $TRACEROUT_SRC_PORTS \
-d $ANYWHERE $TRACEROUT_DEST_PORTS -j ACCEPT
```

# 本地网络内的无限制流量。
# 所有内部机器都可以访问防火墙机器。

```bash
ipchains -A input -i $LOCAL_INTERFACE_1 -s $LOCALNET_1 -j ACCEPT

ipchains -A output -i $LOCAL_INTERFACE_1 -d $LOCALNET_1 -j ACCEPT
```

# 伪装内部流量。
# 所有内部流量在外部进行伪装。

```bash
ipchains -A forward -i $EXTERNAL_INTERFACE -s $LOCALNET_1 -j MASQ
```

# 为选定的拒绝数据包启用日志

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
-d $IPADDR -j DENY -l
```

`ipchains` -A input -i `$EXTERNAL_INTERFACE` -p udp
-d `$IPADDR` `$PRIPVORTS` -j DENY -l

`ipchains` -A input -i `$EXTERNAL_INTERFACE` -p udp \
-d `$IPADDR` `$UNPRIVORTS` -j DENY -I

`ipchains` -A input -i `$EXTERNAL_INTERFACE` -p icmp \
-s `$ANYWHERE` 5 -d `$IPADDR` -j DENY -I

`ipchains` -A input -i `$EXTERNAL_INTERFACE` -p icmp \
-s `$ANYWHERE` 13:255 -d `$IPADDR` -j DENY -I
```

```bash
stop)
echo -n "正在关闭防火墙服务:"

# 移除所有属于此过滤器的现有规则
ipchains -F

# 重置过滤器的默认策略为接受。
ipchains -P input ACCEPT
ipchains -P output ACCEPT
ipchains -P forward ACCEPT

# 重置 TCP SYN Cookie 保护为关闭。
echo 0 > /proc/sys/net/ipv4/tcp_syncookies

# 重置 IP 欺骗保护为关闭。
# 使用源地址验证
for i in /proc/sys/net/ipv4/conf/*/rp_filter; do
echo 0 > $i
done

# 重置 ICMP 重定向接受为开启。
for i in /proc/sys/net/ipv4/conf/*/accept_redirects; do
echo 1 > $i
done

# 重置源路由包为开启。
for i in /proc/sys/net/ipv4/conf/*/accept_source_route; do
echo 1 > $i
done

status)
echo -n "现在显示防火墙统计数据吗?"

restart(reload)
$0 stop
$0 start

)
echo "用法: firewall {start|stop|restart|reload}"
exit 1
esac
```

现在，使此脚本具有可执行权限并更改其默认权限：

`[root@deep]# chmod 700 /etc/rc.init/d/firewall`

`[root@deep]# chmod 055 /etc/rc.init/d/firewall`

使用命令为您的防火墙创建符号链接 rc.d 链接：

```bash
[root@deep]# chconfig --add firewall
[root@deep]# chconfig --level 345 firewall on
```

现在，您的防火墙规则已配置为使用 System vit（System vit 负责启动启动时需要运行的所有进程），并且如果服务器重启，它每次都会自动启动。

若要手动停止系统上的防火墙，请使用命令：

`[root@deep]# /etc/rc.d/init.d/firewall stop`

若要手动启动系统上的防火墙，请使用命令：

`[root@deep]# /etc/rc.d/init.d/firewall start`

# 拒绝某些地址的访问

假设你有一个想要阻止访问你服务器的地址。你可以通过创建 rc.d 文件并取消你的防火墙规则脚本中以下行的注释来实现：

编辑你的防火墙脚本（`vi /etc/rc.d/init.d/firewall`）并取消以下行的注释：

```bash
if [ -f /etc/rc.d/init.d/firewall ]; then
```

创建一个 rc.d 文件，对于你想要阻止访问你服务器的地址：

`touch /etc/rc.d/init.d/firewall` 并取消防火墙规则脚本中以下行的注释：

```bash
假设你知道一个想要阻止访问你服务器的地址。
```

WHOIS 客户端 (43)

# ipchains -A input -i $EXTERNAL_INTERFACE -p tcp ! -y \
-s $ANYWHERE 43 \
-d $IPADDR $UNPRIPVPORTS -j ACCEPT
```

```bash
# ipchains -A output -i $EXTERNAL_INTERFACE -p tcp ! \
-s $IPADDR $UNPRIPVPORTS \
-d $ANYWHERE 43 -j ACCEPT
```

```bash
# 出站追踪路由

# ipchains -A output -i $EXTERNAL_INTERFACE -p udp \
-s $IPADDR $TRACEROUT_SRC_PORTS \
-d $ANYWHERE $TRACEROUT_DEST_PORTS -j ACCEPT
```

# 本地网络内的无限制流量。
# 所有内部机器都可以访问防火墙机器。

```bash
ipchains -A input -i $LOCAL_INTERFACE_1 -s $LOCALNET_1 -j ACCEPT

ipchains -A output -i $LOCAL_INTERFACE_1 -d $LOCALNET_1 -j ACCEPT
```

# 伪装内部流量。
# 所有内部流量在外部进行伪装。

```bash
ipchains -A forward -i $EXTERNAL_INTERFACE -s $LOCALNET_1 -j MASQ
```

# 为选定的拒绝数据包启用日志

```bash
ipchains -A input -i $EXTERNAL_INTERFACE -p tcp \
-d $IPADDR -j DENY -l
```
