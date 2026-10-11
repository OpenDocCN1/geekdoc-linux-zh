
| 1 | 192.168.1.128 | 255.255.255.128 | 192.168.1.129 | 192.168.1.256* | 192.168.1.127 | 126 |

| 2 | 192.168.1.128 | 255.255.255.128 | 192.168.1.129 | 192.168.1.254 | 192.168.1.255 | 126 |

*\*注：原文示例中192.168.1.256可能为逻辑错误*

子网 `192.168.1.0` 和 `192.168.1.128` 可以分配给 2 个独立的内部网络网卡。从网络的角度来看，该站点由一个包含最多254个主机的单一网络组成。在内部，该站点由两个独立网络，每个包含最多126个主机。

子网划分允许创建多个内部网络，每个网络包含不同类别的客户端或服务器机器，且每个网络都有其相互独立的路由。可以对这两个网络应用不同的防火墙策略。虽然可以对局域网（LAN）地址进行地址伪装，但子网划分的流量通常在不经过伪装的情况下转发。

## 按主机、地址范围或端口选择性内部访问

通过防火墙机器内部接口的流量可以进行选择性限制，就像通过外部接口的流量一样。例如，与其让所有流量通过内部接口，不如将流量限制在 DNS、SMTP；AUTH、POP 和 HTTP。在这种情况下，假设防火墙机器为局域网提供这些服务。本地机器不允许访问任何外部服务。

## 关注点

在此示例中，本地主机被限制在特定的服务上：DNS、SMTP、AUTH、POP 和 HTTP。由于在这种情况下 POP 是本地邮件检索服务，而 DNS、SMTP 和 HTTP 本质上是代理服务，因此本地客户端没有直接访问互联网。在每情况下，本地客户端都是连接到本地服务器的。POP 是本地局域网服务。其他三个服务器代表客户端建立远程连接。

## 136 第 4 章 LAN 问题、多防火墙和边界网络

以下示例考虑了一个内部接口连接到局域网（LAN）的防火墙。内部接口的常量如下：

```
LAN_INTERFACE="eth0" # 连接到 LAN 的内部接口
FIREWALL="192.168.1.1" # 防火墙机器内部地址
LAN_ADDRESSES="*192.168.1.0/24" # 接口地址
# LAN 上使用的地址范围
```

LAN 机器将防火墙机器的内部接口指定为其名称 服务器：

```
ipchains -A input -i LAN_INTERFACE -p udp \
-s LAN_ADDRESSES SUNPRIVPORTS \
-d FIREWALL 53 -j ACCEPT
```

```
ipchains -A output -i LAN_INTERFACE -p udp \
-s FIREWALL 53 \
-d LAN_ADDRESSES SUNPRIVPORTS -j ACCEPT
```

```
ipchains -A input -i LAN_INTERFACE -p tcp \
-s LAN_ADDRESSES SUNPRIVPORTS \
-d FIREWALL 53 -j ACCEPT
```

```
ipchains -A output -i LAN_INTERFACE -y -p tcp \
-s FIREWALL 53 \
-d LAN_ADDRESSES SUNPRIVPORTS -j ACCEPT
```

LAN 机器将防火墙作为其 SMTP 和 POP 服务器：

- # 发送邮件 - SMTP

```
ipchains -A input -i LAN_INTERFACE -p tcp \
-s LAN_ADDRESSES SUNPRIVPORTS \
-d FIREWALL 25 -j ACCEPT
```

```
ipchains -A output -i LAN_INTERFACE -y -p tcp \
-s FIREWALL 25 \
-d LAN_ADDRESSES SUNPRIVPORTS -j ACCEPT
```

- # 接收邮件 - POP

```
ipchains -A input -i LAN_INTERFACE -p tcp \
-s LAN_ADDRESSES SUNPRIVPORTS \
-d FIREWALL 110 -j ACCEPT
```

```
ipchains -A output -i LAN_INTERFACE -y -p tcp \
-s FIREWALL 110 \
-d LAN_ADDRESSES SUNPRIVPORTS -j ACCEPT
```

`sendmail` 服务器将为邮件客户端发起 AUTH 查找：

```
ipchains -A output -i LAN_INTERFACE -p tcp \
-s FIREWALL SUNPRIVPORTS \
-d LAN_ADDRESSES 113 -j ACCEPT
```

```
ipchains -A input -i LAN_INTERFACE -y -p tcp \
-s LAN_ADDRESSES 113 \
-d FIREWALL SUNPRIVPORTS -j ACCEPT
```

## 更大或更不可信任的 LAN 的配置选项

最后，防火墙机器上的 8080 端口运行着一个本地代理 Web 服务器。内部机器将防火墙上的 Web 服务器作为其代理，Web 服务器代表它们转发任何传出的请求，并缓存从互联网检索的页面：

```
ipchains -A input -i LAN_INTERFACE -p tcp \
  -s LAN_ADDRESSES SUNPRIVPORTS \
  -d FIREWALL 8080 -j ACCEPT

ipchains -A output -i LAN_INTERFACE -y -p tcp \
  -s FIREWALL 8080 \
  -d LAN_ADDRESSES SUNPRIVPORTS -j ACCEPT
```

## 多 LAN 的配置选项

添加第二个内部 LAN 可以进一步扩展此示例。如图 4.2 所示，DNS、SMTP、AUTH、POP 和 HTTP 服务由第二个 LAN 提供，而不是防火墙提供。在这种情况下，流量被划分为两个子网。

# 140 第 4 章 LAN 问题、多重防火墙与边界网络

`SERVER_LAN` 上的 SMTP 服务器需要向远程目的地发送邮件。该服务器需要通过防火墙访问互联网：

```
ipchains -A input -i SERVER_LAN_INTERFACE -p tcp \
  -s SMAIL_SERVER UNPRIVPORTS \
  -d ANYWHERE 25 -j ACCEPT
```

```
ipchains -A output -i SERVER_LAN_INTERFACE -y -p tcp \
  -s SMAIL_SERVER UNPRIVPORTS \
  -d ANYWHERE 25 -j ACCEPT
```

```
ipchains -A forward -i EXTERNAL_INTERFACE -p tcp \
  -s SMAIL_SERVER UNPRIVPORTS \
  -d ANYWHERE 25 -j ACCEPT
```

`sendmail` 服务器将向邮件客户端发起 AUTH 查找请求：

```
ipchains -A output -i CLIENT_LAN_INTERFACE -p tcp \
  -s SMAIL_SERVER UNPRIVPORTS \
  -d CLIENT_LAN 113 -j ACCEPT
```

```
ipchains -A input -i CLIENT_LAN_INTERFACE -y -p tcp \
  -s CLIENT_LAN 113 \
  -d MAIL_SERVER UNPRIVPORTS -j ACCEPT
```

在实际上，`SERVER_LAN` 上的 SMTP 服务器需要接收来自远程源的邮件。如此处所示，直接通过内部 `sendmail` 守护进程接收入站邮件是不可能的，因为邮件服务器经过了伪装（masqueraded）。该解决方案将在在本章稍后讨论。为了方便讨论，基于本章目前为止提供信息的解决方案是在堡垒机（bastion）上运行邮件服务器。堡垒机将在 `MAIL_SERVER` 机器与远程机器之间中继邮件。

`CLIENT_LAN` 客户端指向 `POP_SERVER` 机器以获取邮件：

```
# 接收邮件 - POP
#
```

```
ipchains -A input -i CLIENT_LAN_INTERFACE -p tcp \
  -s CLIENT_LAN UNPRIVPORTS \
  -d POP_SERVER 110 -j ACCEPT
```

```
ipchains -A output -i SERVER_LAN_INTERFACE -p tcp \
  -s CLIENT_LAN UNPRIVPORTS \
  -d POP_SERVER 110 -j ACCEPT
```
