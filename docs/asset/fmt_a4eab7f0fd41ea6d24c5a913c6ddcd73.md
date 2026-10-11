
```
ipchains -A input -i SERVER_LAN_INTERFACE -y -p tcp \
  -s POP_SERVER 110 \
  -d CLIENT_LAN UNPRIVPORTS -j ACCEPT
```

```
ipchains -A output -i CLIENT_LAN_INTERFACE -y -p tcp \
  -s POP_SERVER 110 \
  -d CLIENT_LAN UNPRIVPORTS -j ACCEPT
```

# 141 更大或更低信任度 LAN 的配置选项

```
ipchains -A forward -i $SERVER_LAN_INTERFACE -p tcp \
  -s $CLIENT_LAN_UNPRIVPORTS \
  -d POP_SERVER 110 -j ACCEPT
```

```
ipchains -A forward -i $CLIENT_LAN_INTERFACE -p tcp \
  -s $POP_SERVER_110 \
  -d $CLIENT_LAN_UNPRIVPORTS -j ACCEPT
```

最后，LAN 上的一个服务器机器上运行着本地代理服务器，绑定到端口 8080。内部机器指向 Web 服务器作为缓存代理，Web 服务器代表它们处理任何传出的请求：

```
# WWW PROXY
```

```
ipchains -A input -i $CLIENT_LAN_INTERFACE -p tcp \
  -s $CLIENT_LAN_UNPRIVPORTS \
  -d $WEB_SERVER 8080 -j ACCEPT
```

```
ipchains -A output -i $SERVER_LAN_INTERFACE -p tcp \
  -s $CLIENT_LAN_UNPRIVPORTS \
  -d $WEB_SERVER 8080 -j ACCEPT
```

```
ipchains -A input -i $SERVER_LAN_INTERFACE -y - p tcp \
  -s $WEB_SERVER 8080 \
  -d $CLIENT_LAN_UNPRIVPORTS -j ACCEPT
```

```
ipchains -A output -i $CLIENT_LAN_INTERFACE -y - p tcp \
  -s $WEB_SERVER 8080 \
  -d $CLIENT_LAN_UNPRIVPORTS -j ACCEPT
```

```
ipchains -A forward -i $SERVER_LAN_INTERFACE -p tcp \
  -s $CLIENT_LAN_UNPRIVPORTS \
  -d $WEB_SERVER 8080 -j ACCEPT
```

```
ipchains -A forward -i $SERVER_LAN_INTERFACE -p tcp \
  -s $CLIENT_LAN_UNPRIVPORTS \
  -d $WEB_SERVER 8080 -j ACCEPT
```

server LAN 上的 Web 服务器需要访问监听 TCP 端口 80 的远程服务器：

```
ipchains -A input -i $SERVER_LAN_INTERFACE -y - p tcp \
  -s $WEB_SERVER UNPRIVPORTS \
  -d ANYWHERE 80 -j ACCEPT
```

```
ipchains -A output -i $SERVER_LAN_INTERFACE -y - p tcp \
  -s $ANYWHERE 80 \
  -d UNPRIVPORTS -j ACCEPT
```

```
ipchains -A forward -i $EXTERNAL_INTERFACE -p tcp \
  -s $WEB_SERVER UNPRIVPORTS \
  -d ANYWHERE -j ACCEPT
```

# 将 LAN 流量到互联网的伪装

目前为止已多条转发和伪装规则。根据你如何制定规则，有许多选择。

## 接口伪装

对于个人家庭 LAN，只需对 LAN 和互联网之间的所有流量进行伪装是最简单的。以下规则通过防火墙的输入和输出规则对外部接口进行伪装：

```
ipchains -A forward -i EXTERNAL_INTERFACE \
  -s $CLIENT_LAN -j MASQUADE
```

通用伪装规则并未允许 LAN 流量通过外部接口。外部接口规则定义了哪些流量可以通过外部接口。此规则对 LAN 和互联网之间任何外部接口允许的流量进行伪装。

## 服务伪装

如果你倾向于显式规则，或者只想允许 LAN 访问外部接口可用的部分服务，可以按服务进行伪装。任何未由转发和伪装规则指定的都会路由到互联网。网络允许内部浏览器访问外部：

```
ipchains -A forward -i EXTERNAL_INTERFACE -p tcp \
  -s $CLIENT_LAN UNPRIVPORTS \
  -d ANYWHERE 80 -j MASQUADE
```

## 接口、服务和主机伪装

防火墙的精确性可以延伸到接口、端口和主机。在显示两个 LAN 的上一个示例中，两个 LAN 上的机器都使用 server LAN 上的特定机器作为本地 DNS 服务器 `DNS_SERVER`。只有 `DNS_SERVER` 允许访问外部 DNS 服务器。因为该机器运行转发服务器，它使用 UDP 端口 53 与外部进行点对点通信。虽然在伪装规则中显式定义了 `SERVER_LAN_INTERFACE`，但由于 `DNS_SERVER` 相对于 `SERVER_LAN_INTERFACE` 有特定地址，接口是隐含。也就是说， LAN 上的其他机器都不允许访问外部 DNS 服务器：

```
ipchains -A forward -i EXTERNAL_INTERFACE -p udp \
  -s $DNS_SERVER 53 \
  -d <isp.dns.server> 53 - MASQUADE
```

# 143 更大或更低信任度 LAN 的配置选项

如果服务器机器作为外部 DNS 服务器的客户端运行，则伪装规则将是：

```
ipchains -A forward -i $EXTERNAL_INTERFACE -p udp \
  -s $DNS_SERVER UNPRIVPORTS \
  -d <isp.dns.server> 53 - MASQUADE
```

```
ipchains -A forward -i $EXTERNAL_INTERFACE -p tcp \
  -s $DNS_SERVER UNPRIVPORTS \
  -d <isp.dns.server> 53 - MASQUADE
```

# 伪装与规则优先级层次

在第 3 章部署的单系统独立防火墙在外部接口上使用了特定的输入和输出规则。家庭 LAN 最简单的设置是允许内部接口的所有入站和出站流量，并转发和伪装所有指向远程外部地址的流量。输入、输出和转发规则用于 LAN，但应用于外部接口的规则提供了整个站点的过滤。

对于任何链（无论是 `input`、`output`、`forward` 还是站点定义的链），数据包都会按照规则定义的顺序对规则进行检查。第一个匹配的规则胜出。在 LAN 和转发或伪装的情况下，问题变成了何时应用哪条规则链？

如图 4.3 所示，每个数据包都到达该接口的 `input` 链。首先检查 `input` 链上的规则。如果数据包被输入过滤器接受，则下一个链取决于数据包的目的。如果目标是本地机器，数据包被放在环回接口的 `output` 链上。如果目标是另一个机器的接口，数据包首先传递到 `forward` 链。如果数据包被转发过滤器接受，则对数据包进行伪装，然后放在网关接口的 `output` 链上。最后，检查 `output` 链过滤器。如果数据包被该接口的过滤器规则接受，则发送到其最终目的地。

# 防火墙规则优先级

关于防火墙规则优先级的更完整的讨论，请参考 `IPCHAINS-HOWTO`。

# 144 第 4 章 LAN 问题、多重防火墙与边界网络

![](img/65af6c8c09dbe707d567ca01d4bca008_161_0.png)

图 4.3 伪装与规则优先级层级。

## 端口重定向——透明代理

`iptables` 的端口重定向功能是本地端口转发和伪装的一种局限的特殊情况。连接不会在网络接口之间进行转发或伪装。相反，任何匹配规则的流量，无论数据包的部地址或端口是什么，都会被重定向到本地端口。

此功能对于你可能运行的某些应用层代理非常有用。通常，应用层代理要求你重新配置或使用知晓本地代理服务的特殊应用程序来替换客户端软件。如果客户端程序没有使用特殊的代理协议，端口重定向可以使重定向变得不可见（例如，直接到 Web 服务器的 HTTP 协议与到 Web 代理服务器的代理 HTTP 协议不同）。

## 更大或更低信任 LAN 的配置选项 145
