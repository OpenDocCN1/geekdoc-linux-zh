
# 在此处添加接受授权流量的附加规则。
# 未显式接受的流量将被记录并丢弃。

例如，`$SSH` 变量可能以以下方式赋值：
`$SSH="192.168.1.1 192.168.1.2"`

这将导致 shell 循环执行以下 `iptables` 命令：

```
$IPT -A IN -p tcp -s $sip --dport 22 -m state NEW \
-j ACCEPT
```
其中 `$sip` 会替换为具体的 IP 地址。

要指定整个 C 类网段的主机都是被授权的，为 `$SSH` 变量赋值如下：
`$SSH="10.0.0.0/24"`

要指定任何主机都能访问本地服务器，为 `$SSH` 变量赋值如下：
`$SSH="0.0.0.0/0"`

要指定没有任何主机可以访问本地服务器，为 `$SSH` 变量赋值如下：
`$SSH=""`

你可以以相同的方式为 `$WWW` 变量赋值。列表 9-3 所示的完整防火墙代码展示了如何这样做。在执行 IN 链命令之前，shell 变量必须赋值。

使用以下模式创建 shell 循环：

```
for sip in $service; do

$IPT -A IN -p proto -s $sip --dport port -m state NEW \
-j ACCEPT

done
```
其中 `service` 是 shell 变量名，`proto` 是 tcp 或 udp，`port` 是服务器监听的端口。

# 第二部分：防火墙设计与实现

大多数常用服务可以通过编写指向服务器监听端口的单一规则来实现授权。然而，复杂的协议可能需要多条规则。某些协议（如 H.323）非代理防火墙支持。请参阅第 4 章“互联网服务”以了解更多你想授权的协议。

![](img/0f69b2a8749a24b957044e9f26f2d5b4_301_0.png)

图 9-4：OUTPUT 链

## 第9章：IPTables 防火墙实现

![](img/0f69b2a8749a24b957044e9f26f2d5b4_302_0.png)

图 9-4：OUT链

列表 9-4：OUT链

```
$IPT -N OUT

$IPT -A OUT -p tcp -j FLAGS

$IPT -A OUT -s ! $IP -j LDROP

$IPT -A OUT -m state --state ESTABLISHED,RELATED -j ACCEPT

#
# 此防火墙配置为默认阻止出站连接。
# 要允许任何未显式阻塞的输出，请取消
# 以下行的行的注释。在此处放置阻塞规则。
#IPT -A OUT -m state --state NEW -j ACCEPT
```

### 允许新的出站连接。

续

274 第II部分：防火墙的设计与实现

列表 9-4（续）
| `$IPT -A OUT -m state --state NEW -p tcp --dport 21 -j ACCEPT @ ftp` |
| `$IPT -A OUT -m state --state NEW -p tcp --dport 22 -j ACCEPT @ ssh` |
| `$IPT -A OUT -m state --state NEW -p tcp --dport 25 -j ACCEPT @ smtp` |
| `$IPT -A OUT -m state --state NEW -p tcp --dport 43 -j ACCEPT @ whois` |
| `$IPT -A OUT -m state --state NEW -p tcp --dport 53 -j ACCEPT @ domain` |
| `$IPT -A OUT -m state --state NEW -p tcp --dport 80 -j ACCEPT @ http` |
| `$IPT -A OUT -m state --state NEW -p tcp --dport 443 -j ACCEPT @ https` |
| `$IPT -A OUT -m state --state NEW -p tcp --dport 873 -j ACCEPT @ rsync` |
| `$IPT -A OUT -m state --state NEW -p udp --dport 53 -j ACCEPT @ domain` |

# 在此处添加接受授权流量的额外规则。
未被显式接受的流量将被记录并丢弃。

按照配置，该模型防火墙允许本地客户端连接到这些服务：

- FTP (TCP 端口 21)
- SSH (TCP 端口 22)
- SMTP (TCP 端口 25)
- WHOIS (TCP 端口 43)
- DNS (TCP 端口 53 和 UDP 端口 53)
- HTTP (TCP 端口 80)
- HTTPS (TCP 端口 443)
- RSYNC (TCP 端口 873)

![](img/0f69b2a8749a24b957044e9f26f2d5b4_303_0.png)

如果你喜欢具有宽松出站过滤的防火墙，请取消接受新出站连接行的注释。要禁止某项服务，可以在取消注释行的之前添加一个记录并拒绝相关数据报的规则。例如，要禁止出站 FTP 但授权所有其他 TCP 和 UDP 服务，你的防火墙应该包含这两个规则：

```
$IPT -A OUT -p tcp --dport 21 -j LDROP

$IPT -A OUT -m state --state NEW -j ACCEPT
```

在“日志链”章节中解释的 DROP 链会记录并丢弃发送给它的包。因此，这两条规则接受除发往 21 端口（FTP 命令端口）之外的所有新连接。

![](img/0f69b2a8749a24b957044e9f26f2d5b4_304_0.png)

回想，如第8 章所述，到达 IPTables 用户链（如 OUT 链）结尾的数据包将返回调用链。

### IN_ICMP 链：过滤
入站 ICMP 消息

图 9-5 显示了 IN_ICMP 链，它处理入站 ICMP 消息。
IN_ICMP 链：

1. 如果消息是来自授权主机的 echo 请求或回复，接受该消息。
2. 如果消息是目标不可达消息，接受该消息。
3. 如果消息是源猝发消息（source quench），接受该消息。
4. 如果消息是超时消息（time-exceeded），接受该消息。
5. 如果消息是参数问题消息，接受该消息。
6. 否则，将数据包返回到 INPUT 链，由其记录并丢弃。

列表 9-5 显示了组成 IN_ICMP 链的命令。注意，防火墙代码包含一个循环，根据 shell 变量 `$PING` 中包含的 IP 地址来执行接受 ping（echo 请求）消息的命令。该变量的值在执行命令之前必须设置。该变量的值与本章稍早描述的 `$SSH` shell 变量的形式相同。

![](img/0f69b2a8749a24b957044e9f26f2d5b4_305_0.png)

列表 9-5：IN_ICMP 链

```
$IPT -N IN_ICMP

for sip $PING; do

$IPT -A IN_ICMP -p icmp --icmp-type echo-request -s $sip
  -d $ip -j ACCEPT

$IPT -A IN_ICMP -p icmp --icmp-type echo-reply -s $sip
  -j ACCEPT

$IPT -A IN_ICMP -p icmp --icmp-type destination-unreachable -j ACCEPT

$IPT -A IN_ICMP -p icmp --icmp-type source-quench -j ACCEPT

$IPT -A IN_ICMP -p icmp --icmp-type time-exceeded -j ACCEPT

$IPT -A IN_ICMP -p icmp --icmp-type parameter-problem -j ACCEPT

done
```

## 第9章：IPTables 防火墙实现

```
$IPT -A IN_ICMP -p icmp --icmp-type time-exceeded -j ACCEPT

$IPT -A IN_ICMP -p icmp --icmp-type parameter-problem -j ACCEPT
```

如果你对处理 ICMP 消息有不同的策略，可以删除接受请求的规则，或者简单将 PING 变量设置为空：

```
PING=""
```

### OUT_ICMP 链：过滤
出站 ICMP 消息

图 9-6 描述了 OUT_ICMP 链，它处理出站 ICMP 消息。该链的结构与 IN_ICMP 链相似，但它接受分片消息而不接受超时消息。然而，对于 ICMP 消息：

> 提示：通过删除接受目标不可达和参数问题消息的规则，可以让防火墙更安全。

![](img/0f69b2a8749a24b957044e9f26f2d5b4_306_0.png)

图 9-6：OUT_ICMP 链

列表 9-6：OUT_ICMP 链

```
