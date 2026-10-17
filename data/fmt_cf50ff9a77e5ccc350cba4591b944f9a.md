
```
ipchains -A input -i $CHOKE_DMZ_INTERFACE -p tcp ! -y \
-s $IMAP_SERVER_DMZ_IPADDR 143 \
-d CHOKE_DMZ_IPADDR UNPRIVPORTS
```

## 访问 Usenet 服务 (TCP NNTP 端口 119)

Usenet 新通过运行在 TCP 服务端口 119 之上的 NNTP 协议访问。读取新闻和发布文章由本地新闻客户端处理。

非 ISP 站点为外界托管新闻服务器。对于小型站点，即使托管新闻服务器也是可能的。作为例外，服务器规则应配置为允许特定的外部客户端。公共服务器通常托管在外部堡垒上。

### 堡垒 NNTP 通道和服务器 DMZ 配置

表 4.19 列出了 NNTP 服务的完整客户端/服务器连接协议。

表 4.19 堡垒 NNTP 客户端/服务器通道

| 描述 | 协议 | 远程地址 | 远程端口 | 出 | 本地地址 | 本地端口 | 标志 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Choke 客户端查询 | TCP | CHOKE_DMZ_IPADDR | 1024:65535 | In | NEWS_SERVER | 119 | Any |
| DMZ 服务器响应 | TCP | CHOKE_DMZ_IPADDR | 1024:65535 | Out | NEWS_SERVER | 119 | ACK |
| 远程客户端查询 | TCP | NEWS_SERVER_DMZ_IPADDR | 119 | Out | NNTP clients | 1024:65535 | Any |
| DMZ 服务器响应 | TCP | NEWS_SERVER_DMZ_IPADDR | 119 | In | NNTP clients | 1024:65535 | ACK |
| 本地服务器查询 | TCP | NEWS_SERVER_DMZ_IPADDR | 1024:65535 | In | NEWS_FEED | 119 | Any |
| 远程服务器响应 | TCP | NEWS_SERVER_DMZ_IPADDR | 1024:65535 | Out | NEWS_FEED | 119 | ACK |

你从运行在 DMZ 服务器上的新闻服务器检索邮件：

```
ipchains -A output -i $CHOKE_DMZ_INTERFACE -p tcp \
  -s CHOKE_DMZ_IPADDR UNPRIVPORTS \
  -d NNTP_SERVER 119 - ACCEPT
```

```
ipchains -A input -i $CHOKE_DMZ_INTERFACE -p tcp ! -y \
  -s SNWS_SERVER 119 \
  -d CHOKE_DMZ_IPADDR UNPRIVPORTS - ACCEPT
```

如果本地新闻服务器运行在 DMZ 中的机器上，并为选择远程客户端提供公共服务，则定义一组服务器规则，允许远程客户端连接到机器的 NNTP 端口：

```
NEWS_SERVER_DMZ_IPADDR="192.168.1.6"
```

```
ipchains -A output -i $BASTION_DMZ_INTERFACE -p tcp \
-s $my.news.clients:$UNPRIVORTS \
-d $NEWS_SERVER_DMZ_IPADDR 119 -j ACCEPT
```

```
ipchains -A input -i $BASTION_DMZ_INTERFACE -p tcp -y \
-s $NEWS_SERVER_DMZ_IPADDR 119 \
-d $my.news.clients:$UNPRIVORTS -j ACCEPT
```

如果 DMZ 机器分配了私有 IP 地址，则需要端口转发模块：

```
ipmasqadm portfw -a -P tcp -L $my.news.clients:119 \
-R $NEWS_SERVER_DMZ_IPADDR 119
```

如果本地新闻服务器提供公共 Usenet 新闻组以及本地新闻组，则本地服务器需要来自远程服务器的新闻馈。以下规则允许访问作为新闻源的远程新闻服务器：

```
NEWS_FEED='my.news.feed'
```

```
ipchains -A input -i $BASTION_DMZ_INTERFACE -p tcp \
-s $NEWS_SERVER_DMZ_IPADDR:$UNPRIVORTS \
-d $NEWS_FEED 119 -j ACCEPT
```

```
ipchains -A output -i $BASTION_DMZ_INTERFACE -p tcp -y \
-s $NEWS_FEED 119 \
-d $NEWS_SERVER_DMZ_IPADDR:$UNPRIVORTS -j ACCEPT
```

# Choke NNTP 客户端 DMZ 配置

表 4.20 列出了 NNTP Usenet 服务的完整客户端/服务器连接协议。

表 4.20 Choke NNTP 客户端协议

| 描述 | 协议 | 远程地址 | 远程端口 | 出方向 | 本地地址 | 本地端口 | 标记 |
|---|---|---|---|---|---|---|---|
| Choke 客户端查询 | TCP | NEWS_SERVER | 119 | Out | CHOKE_DMZ_IPADDR | 1024:65535 | Any |
| 远程服务器响应 | TCP | NEWS_SERVER | 119 | in | CHOKE_DMZ_IPADDR | 1024:65535 | ACK |
| Choke 客户端查询 | TCP | NEWS_SERVER_DMZ_IPADDR | 119 | Out | CHOKE_DMZ_IPADDR | 1024:65535 | Any |
| DMZ 服务器响应 | TCP | NEWS_SERVER_DMZ_IPADDR | 119 | in | CHOKE_DMZ_IPADDR | 1024:65535 | ACK |

接下来两条规则允许本地客户端访问远程新闻服务器：

```
ipchains -A output -i $CHOKE_DMZ_INTERFACE -p tcp | \
  -s $CHOKE_DMZ_IPADDR:$UNPRIVORTS \
  -d $SNEWS_SERVER 119 -j ACCEPT
```

```
ipchains -A input -i $CHOKE_DMZ_INTERFACE -p tcp ! -y | \
  -s $SNEWS_SERVER 119 \
  -d $CHOKE_DMZ_IPADDR:$UNPRIVORTS -j ACCEPT
```

接下来两条规则允许本地客户端访问 DMZ 中的本地新闻服务器：

```
ipchains -A output -i $CHOKE_DMZ_INTERFACE -p tcp | \
  -s $CHOKE_DMZ_IPADDR:$UNPRIVORTS \
  -d $SNEWS_SERVER 119 -j ACCEPT
```

```
ipchains -A input -i $CHOKE_DMZ_INTERFACE -p tcp ! -y | \
  -s $SNEWS_SERVER 119 \
  -d $CHOKE_DMZ_IPADDR:$UNPRIVORTS -j ACCEPT
```

# Telnet (TCP 端口 23)

根据你的需求，可能会认为内部 telnet 服务是完全可以的。根据 LAN 中的 UNIX 机器类型，telnet 将是唯一的工具。客户端和服务器规则允许从任何地方访问。如果你使用 telnet，可能可以将外部地址限制为特定的子集。如果不可行，则应在 `/etc/hosts.allow` 中限制 telnet。

## Bastion DMZ 配置

表 4.21 列出了 Telnet 服务的客户端/服务器连接协议。

表 4.21 Bastion Telnet 协议

| 描述 | 协议 | 远程地址 | 远程端口 | 出方向 | 本地地址 | 本地端口 | 标记 |
|---|---|---|---|---|---|---|---|
| Choke 客户端请求 | TCP | CHOKE_DMZ_IPADDR | 1024:65535 | In | ANYWHERE | 23 | Any |
| 服务器响应 | TCP | CHOKE_DMZ_IPADDR | 1024:65535 | Out | ANYWHERE | 23 | ACK |
| Bastion 客户端请求 | TCP | DMZ_ADDRESSES | Out | BASTION_DMZ_IPADDR | 1024:65535 | Any |
