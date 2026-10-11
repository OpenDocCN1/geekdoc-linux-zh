
# 332 附录 B 防火墙示例和支持脚本

```bash
#允许客户端连接到你的 IMAPS 服务器
#NFT rule filter input if $INTERNET ip saddr 0/0 tcp sport $UNPRIVORTS addaddr $IPADDR tcp dport 993 accept
#NFT rule filter output oif $INTERNET ip saddr $IPADDR tcp sport 993 daddr --0/0 tcp dport $UNPRIVORTS tcp flags != syn accept
```

```bash
#ssh
SSH_PORTS="1020-65535"
#NFT rule filter output if $INTERNET ip saddr $IPADDR tcp sport $SSH_PORTS --tcp dport 22 accept
#NFT rule filter input if $INTERNET tcp sport 22 ip daddr $IPADDR tcp dport --$SSH_PORTS tcp flags != syn accept
#NFT rule filter input if $INTERNET tcp sport $SSH_PORTS ip daddr $IPADDR --tcp dport 22 accept
#NFT rule filter output oif $INTERNET ip daddr $IPADDR tcp sport 22 tcp dport --$SSH_PORTS tcp flags != syn accept
```

```bash
#ftp
#NFT rule filter output oif $INTERNET ip saddr $IPADDR tcp sport $UNPRIVORTS --tcp dport 21 accept
#NFT rule filter input if $INTERNET ip daddr $IPADDR tcp sport 21 tcp dport --$UNPRIVORTS accept
#假设对 ftp 使用了 tc 模块
```

```bash
#dhcp (此机器在两个接口上运行 dhcp，因此需要规则)
#NFT rule filter output if $INTERNET ip saddr $BROADCAST_SRC udp sport 67-68 ip daddr $BROADCAST_DEST udp dport 67-68 accept
#NFT rule filter input if $INTERNET udp sport 67-68 udp dport 67-68 accept
#NFT rule filter output udp sport 67-68 udp dport 67-68 accept
#NFT rule filter input inp udp sport 67-68 udp dport 67-68 accept
```

```bash
# ntp
$NFT add rule filter output oif $INTERNET saddr $IPADDR udp port $UNPRIVORTS - ip ip daddr $TIME_SERVER udp port 123 accept
$NFT add rule filter input iif $INTERNET saddr $TIME_server udp port 123 - ip daddr $IPADDR udp port $UNPRIVORTS accept
```

```bash
# 记录到达此处的所有包
$NFT add rule filter input log
$NFT add rule filter output log
```

```bash
# 默认策略：
$NFT add rule filter input drop
$NFT add rule filter output accept
```

# 第 6 章优化的 iptables 防火墙

对于大多数使用 DSL、调制解调调器和低速租用线路的系统，Linux 网络代码处理数据包的速度通常比网络连接的速度快。特别是由于防火墙规则具有顺序依赖性且难以构建，因此组织规则以提高可读性比为了速度而组织更大的收益。

```
############################################################
# DNS 缓存域名服务器（查询远程，主服务器）

$IPT -A EXT-output -p udp --sport 53 --dport 53 \
  -j local-dns-server-query

$IPT -A EXT-input -p udp --sport 53 --dport 53 \
  -j remote-dns-server-response

# DNS 缓存域名服务器（通过 TCP 向远程服务器查询） \
$IPT -A EXT-output -p tcp \
  --sport $UNPRIVPORTS --dport 53 \
  -j local-dns-server-query

$IPT -A EXT-input -p tcp ! --syn \
  --sport 53 --dport $UNPRIVORTS \
  -j remote-dns-server-response

############################################################
# DNS 转发域名服务器或客户端请求
if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A local-dns-server-query \
  -d $NAMESERVER_1 \
  -m state NEW -j ACCEPT
  $IPT -A local-dns-server-query \
  -d $NAMESERVER_2 \
  -m state NEW -j ACCEPT
  $IPT -A local-dns-server-query \
  -d $NAMESERVER_3 \
  -m state NEW -j ACCEPT
fi

$IPT -A local-dns-server-query \
  -d $NAMESERVER_1 -j ACCEPT

$IPT -A local-dns-server-query \
  -d $NAMESERVER_2 -j ACCEPT

$IPT -A local-dns-server-query \
  -d $NAMESERVER_3 -j ACCEPT

# DNS 服务器对本地请求的响应
$IPT -A remote-dns-server-response \
  -s $NAMESERVER_1 -j ACCEPT

$IPT -A remote-dns-server-response \
  -s $NAMESERVER_2 -j ACCEPT

$IPT -A remote-dns-server-response \
  -s $NAMESERVER_3 -j ACCEPT
```

# 336 附录 B 防火墙示例和支持脚本

```
################################################
# 本地 TCP 客户端，远程服务器
```

```
IPT -A EXT-output -p tcp \
  --sport $UNPRIVORTPORTS \
  -j local-tcp-client-request

IPT -A EXT-input -p tcp ! --syn \
  --dport $UNPRIVORTPORTS \
  -j remote-tcp-server-response
```

```
################################################
# 本地 TCP 客户端输出和远程服务器输入链
```

```
# SSH 客户端

if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A local-tcp-client-request -p tcp \
  -d <selected_host> --dport 22 \
  -m state --state NEW \

fi
```

```
IPT -A local-tcp-client-request -p tcp \
  -d <selected_host> --dport 22 \
  -j ACCEPT
```

```
IPT -A remote-tcp-server-response -p tcp ! --syn \
  -s <selected_host> --sport 22 \
  -j ACCEPT
```
