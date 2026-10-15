
```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then
    # 如果使用了 ip_conntrack_ftp
    # 模块，则此规则不是必需的。
    $IPT -A INPUT -i $INTERNET -p tcp \
         --sport 20 \
         -d $IPADDR --dport $UNPRIVPORTS \
         -m state --state NEW -j ACCEPT
fi

$IPT -A INPUT -i $INTERNET -p tcp \
     --sport 20 \
     -d $IPADDR --dport $UNPRIVPORTS -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
     -s $IPADDR --sport $UNPRIVPORTS \
     --dport 20 -j ACCEPT
```

## 非特权端口之间的出站被动模式数据通道连接

```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then
    # 如果使用了 ip_conntrack_ftp
    # 模块，则此规则不是必需的。
    $IPT -A OUTPUT -o $INTERNET -p tcp \
         -s $IPADDR --sport $UNPRIVPORTS \
         --dport $UNPRIVPORTS -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
     -s $IPADDR --sport $UNPRIVPORTS \
     --dport $UNPRIVPORTS -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
     --sport $UNPRIVPORTS \
     -d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

## 入站远程客户端到本地服务器的请求

```bash
if [ "$FTP_SERVER" = "1" ]; then
    # 入站至端口 21 的控制连接
    if [ "$CONNECTION_TRACKING" = "1" ]; then
        $IPT -A INPUT -i $INTERNET -p tcp \
             --sport $UNPRIVPORTS \
             -d $IPADDR --dport 21 \
             -m state --state NEW -j ACCEPT
    fi

    $IPT -A INPUT -i $INTERNET -p tcp \
         --sport $UNPRIVPORTS \
         -d $IPADDR --dport 21 -j ACCEPT

    $IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
         -s $IPADDR --sport 21 \
         --dport $UNPRIVPORTS -j ACCEPT

    # 出站至端口 20 的端口模式数据通道连接
    if [ "$CONNECTION_TRACKING" = "1" ]; then
        $IPT -A OUTPUT -o $INTERNET -p tcp \
             -s $IPADDR --sport 20 \
             --dport $UNPRIVPORTS -m state --state NEW -j ACCEPT
    fi

    $IPT -A OUTPUT -o $INTERNET -p tcp \
         -s $IPADDR --sport 20 \
         --dport $UNPRIVPORTS -j ACCEPT

    $IPT -A INPUT -i $INTERNET -p tcp ! --syn \
         --sport $UNPRIVPORTS \
         -d $IPADDR --dport 20 -j ACCEPT

    # 非特权端口之间的入站被动模式数据通道连接
    if [ "$CONNECTION_TRACKING" = "1" ]; then
        $IPT -A INPUT -i $INTERNET -p tcp \
             --sport $UNPRIVPORTS \
             -d $IPADDR --dport $UNPRIVPORTS \
             -m state --state NEW -j ACCEPT
    fi

    $IPT -A INPUT -i $INTERNET -p tcp \
         --sport $UNPRIVPORTS \
         -d $IPADDR --dport $UNPRIVPORTS -j ACCEPT

    $IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
         -s $IPADDR --sport $UNPRIVPORTS \
         --dport $UNPRIVPORTS -j ACCEPT
fi
```

# 附录 B：防火墙示例和支持脚本

## HTTP 网络流量（TCP 端口 80）

### 出站本地客户端到远程服务器的请求

```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then
    $IPT -A OUTPUT -o $INTERNET -p tcp \
         -s $IPADDR --sport $UNPRIVPORTS \
         --dport 80 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
     -s $IPADDR --sport $UNPRIVPORTS \
     --dport 80 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
     --sport 80 \
     -d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

### 入站远程客户端到本地服务器的请求

```bash
if [ "$WEB_SERVER" = "1" ]; then
    if [ "$CONNECTION_TRACKING" = "1" ]; then
        $IPT -A INPUT -i $INTERNET -p tcp \
             --sport $UNPRIVPORTS \
             -d $IPADDR --dport 80 \
             -m state --state NEW -j ACCEPT
    fi

    $IPT -A INPUT -i $INTERNET -p tcp \
         --sport $UNPRIVPORTS \
         -d $IPADDR --dport 80 -j ACCEPT

    $IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
         -s $IPADDR --sport 80 \
         --dport $UNPRIVPORTS -j ACCEPT
fi
```

## SSL 网络流量（TCP 端口 443）

### 出站本地客户端到远程服务器的请求

```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then
    $IPT -A OUTPUT -o $INTERNET -p tcp \
         -s $IPADDR --sport $UNPRIVPORTS \
         --dport 443 -m state --state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
     -s $IPADDR --sport $UNPRIVPORTS \
     --dport 443 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
     --sport 443 \
     -d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

### 入站远程客户端到本地服务器的请求
