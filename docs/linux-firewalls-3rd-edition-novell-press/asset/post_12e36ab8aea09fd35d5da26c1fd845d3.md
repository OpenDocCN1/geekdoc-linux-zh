
## 利用连接状态绕过规则检查

```sh
if [ "$CONNECTION_TRACKING" = "1" ]; then
    $IPT -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
    $IPT -A OUTPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
fi

# 单独使用状态模块时，INVALID 会破坏使用双向连接、
# 多连接或交换的协议，除非提供了该协议的 ALG。
# 目前，FTP 和 IRC 是仅有的支持 ALG 的协议。

$IPT -A INPUT -m state --state INVALID -j LOG \
    --log-prefix "INVALID input: "
$IPT -A INPUT -m state --state INVALID -j DROP

$IPT -A OUTPUT -m state --state INVALID -j LOG \
    --log-prefix "INVALID output: "
$IPT -A OUTPUT -m state --state INVALID -j DROP
fi
```

### 源地址欺骗和其他不良地址

```sh
# 拒绝伪装成来自外部接口 IP 地址的欺骗包
$IPT -A INPUT -i $INTERNET -s $IPADDR -j DROP

# 拒绝声称来自 A 类私有网络的包
$IPT -A INPUT -i $INTERNET -s $CLASS_A -j DROP

# 拒绝声称来自 B 类私有网络的包
$IPT -A INPUT -i $INTERNET -s $CLASS_B -j DROP

# 拒绝声称来自 C 类私有网络的包
$IPT -A INPUT -i $INTERNET -s $CLASS_C -j DROP

# 拒绝声称来自环回接口的包
$IPT -A INPUT -i $INTERNET -s $LOOPBACK -j DROP

# 拒绝格式错误的广播包
$IPT -A INPUT -i $INTERNET -s $BROADCAST_DEST -j LOG
$IPT -A INPUT -i $INTERNET -s $BROADCAST_DEST -j DROP

$IPT -A INPUT -i $INTERNET -d $BROADCAST_SRC -j LOG
$IPT -A INPUT -i $INTERNET -d $BROADCAST_SRC -j DROP
```

## 附录 B：防火墙示例和支持脚本

```sh
if [ "${DHCP_CLIENT}" = "0" ]; then
    # 拒绝定向广播
    # 用于映射网络和发起拒绝服务攻击
    $IPT -A INPUT -i $INTERNET -d $SUBNET_BASE -j DROP
    $IPT -A INPUT -i $INTERNET -d $SUBNET_BROADCAST -j DROP

    # 拒绝受限广播
    $IPT -A INPUT -i $INTERNET -d $BROADCAST_DEST -j DROP
fi

# 拒绝 D 类组播地址
# 作为源地址是非法的
$IPT -A INPUT -i $INTERNET -s $CLASS_D_MULTICAST -j DROP

$IPT -A INPUT -i $INTERNET -p ! udp -d $CLASS_D_MULTICAST -j DROP

$IPT -A INPUT -i $INTERNET -p udp -d $CLASS_D_MULTICAST -j ACCEPT

# 拒绝 E 类保留 IP 地址
$IPT -A INPUT -i $INTERNET -s $CLASS_E_RESERVED_NET -j DROP

if [ "${DHCP_CLIENT}" = "1" ]; then
    $IPT -A INPUT -i $INTERNET -p udp \
        -s $BROADCAST_SRC --sport 67 \
        -d $BROADCAST_DEST --dport 68 -j ACCEPT
fi

# 拒绝由 IANA 定义为保留的地址
# 0.*.*.*       - 无法在 DHCP 下单方面阻止
# 169.254.0.0/16 - 链路本地网络
# 192.0.2.0/24 - TEST-NET

$IPT -A INPUT -i $INTERNET -s 0.0.0.0/8 -j DROP
$IPT -A INPUT -i $INTERNET -s 169.254.0.0/16 -j DROP
$IPT -A INPUT -i $INTERNET -s 192.0.2.0/24 -j DROP

##############################################################################
# 禁止连接到常见的 TCP 非特权服务器端口

# X 窗口连接建立
$IPT -A OUTPUT -o $INTERNET -p tcp --syn \
    --destination-port $XWINDOW_PORTS -j REJECT

# X 窗口：传入连接尝试
$IPT -A INPUT -i $INTERNET -p tcp --syn \
    --destination-port $XWINDOW_PORTS -j DROP

# 建立到 NFS、OpenWindows、SOCKS 或 squid 的 TCP 连接

$IPT -A OUTPUT -o $INTERNET -p tcp \
-m multiport --destination-port \
$NFS_PORT,$OPENWINDOWS_PORT,$SOCKS_PORT,$SQUID_PORT \
-syn -j REJECT
$IPT -A INPUT -i $INTERNET -p tcp \
-m multiport --destination-port \
$NFS_PORT,$OPENWINDOWS_PORT,$SOCKS_PORT,$SQUID_PORT \
-syn -j DROP
```

### 禁止连接到常见的 UDP 非特权服务器端口

#### NFS 和 lockd

```sh
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o $INTERNET -p udp \
-m multiport --destination-port $NFS_PORT,$LOCKD_PORT \
-m state --state NEW -j REJECT
$IPT -A INPUT -i $INTERNET -p udp \
-m multiport --destination-port $NFS_PORT,$LOCKD_PORT \
-m state --state NEW -j DROP
else
$IPT -A OUTPUT -o $INTERNET -p udp \
-m multiport --destination-port $NFS_PORT,$LOCKD_PORT \
-j REJECT
$IPT -A INPUT -i $INTERNET -p udp \
-m multiport --destination-port $NFS_PORT,$LOCKD_PORT \
-j DROP
fi
```

#### DNS 名称服务器

#### DNS 转发名称服务器或客户端请求

```sh
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o $INTERNET -p udp \
-s $IPADDR --sport $UNPRIVPORTS \
-d $NAMESERVER --dport 53 \
-m state --state NEW -j ACCEPT
fi
$IPT -A OUTPUT -o $INTERNET -p udp \
-s $IPADDR --sport $UNPRIVPORTS \
-d $NAMESERVER --port 53 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p udp \
-s $NAMESERVER --sport 53 \
-d $IPADDR --port $UNPRIVPORTS -j ACCEPT

# ............................................................
# TCP 用于大响应

if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
-d $NAMESERVER --port 53 \
-m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
-d $NAMESERVER --port 53 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
-s $NAMESERVER --sport 53 \
-d $IPADDR --port $UNPRIVPORTS -j ACCEPT

# ............................................................
# DNS 缓存名称服务器（本地服务器到主服务器）

if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o $INTERNET -p udp \
-s $IPADDR --sport 53 \
-d $NAMESERVER --port 53 \
-m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p udp \
-s $IPADDR --port 53 \
-d $NAMESERVER --port 53 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p udp \
-s $NAMESERVER --sport 53 \
-d $IPADDR --port 53 -j ACCEPT
```

### 过滤 AUTH 用户识别服务 (TCP 端口 113)

```sh
# 从本地客户端到远程服务器的传出请求

$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
-dport 113 -m state --state NEW -j ACCEPT
fi
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
-dport 113 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
--sport 113 \
-d $IPADDR --dport $UNPRIVPORTS -j ACCEPT

# .........................
# 从远程客户端到本地服务器的传入请求

if [ "$ACCEPT_AUTH" = "1" ]; then
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A INPUT -i $INTERNET -p tcp \
--sport $UNPRIVPORTS \
-d $IPADDR -dport 113 \
-m state --state NEW -j ACCEPT

fi
$IPT -A INPUT -i $INTERNET -p tcp \
--sport $UNPRIVPORTS \
-d $IPADDR -dport 113 -j ACCEPT
$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
-s $IPADDR --sport 113 \
-dport $UNPRIVPORTS -j ACCEPT
else
$IPT -A INPUT -i $INTERNET -p tcp \
--sport $UNPRIVPORTS \
-d $IPADDR -dport 113 -j REJECT --reject-with tcp-reset
fi

##############################################################################
# 向任何外部邮件服务器发送邮件
# 如果使用 ISP 邮件网关代替，请使用 -d $MAIL_SERVER"
```

```sh
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
--dport 25 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
--dport 25 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
--sport 25 \
-d $IPADDR --dport $UNPRIVPORTS -j ACCEPT

########################################
# 作为 POP 客户端获取邮件 (TCP 端口 110)
########################################

if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
-d $POP_SERVER --dport 110 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
-d $POP_SERVER --dport 110 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
-s $POP_SERVER --sport 110 \
-d $IPADDR --dport $UNPRIVPORTS -j ACCEPT

########################################
# 访问 Usenet 新闻服务 (TCP/UDP 端口 119)
########################################

if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
-d $NEWS_SERVER --dport 119 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
-d $NEWS_SERVER --dport 119 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
-s $NEWS_SERVER --sport 119 \
-d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```
