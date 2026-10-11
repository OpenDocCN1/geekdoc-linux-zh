
| 关口请求 | TCP | `CHOKE_DMZ_IPADDR` | 1024:65535 | 入 | `WEB_PROXY_SERVER` | `WEB_PROXY_PORT` | 任意 |

| 服务器响应 | TCP | `CHOKE_DMZ_IPADDR` | 1024:65535 | 出 | `WEB_PROXY_SERVER` | `WEB_PROXY_PORT` | ACK |

以下规则允许来自关口机的入代理客户端连接，以及来自关口防火墙后私有局域网机器连接：

```
ipchains -A input -i $BASTION_DMZ_INTERFACE -p tcp \
-s $CHOKE_DMZ_IPADDR $UNPRIVPORTS \
-d $WEB_PROXY_SERVER $WEB_PROXY_PORT -j ACCEPT
```

```
ipchains -A output -i $BASTION_DMZ_INTERFACE -p tcp ! -y \
-s $WEB_PROXY_SERVER $WEB_PROXY_PORT \
-d $CHOKE_DMZ_IPADDR $UNPRIVPORTS -j ACCEPT
```

## 关口客户端到外部服务器的出连接

表 4.36 列出了 HTTP Web 服务的客户端连接协议。

### 表 4.36 关口 HTTP 客户端协议

| 描述 | 协议 | 远程地址 | 远程端口 | 入/出 | 本地地址 | 本地端口 | TCP 标志 |
|---|---|---|---|---|---|---|---|
| 关口客户端请求 | TCP | ANYWHERE | 80 | 出 | `CHOKE_DMZ_IPADDR` | 1024:65535 | 任意 |
| 远程服务器响应 | TCP | ANYWHERE | 80 | 入 | `CHOKE_DMZ_IPADDR` | 1024:65535 | ACK |

本节允许本地主机连接到堡垒和远程主机上的 Web 服务器：

```
ipchains -A output -i $CHOKE_DMZ_INTERFACE -p tcp \
-s CHOKE_DMZ_IPADDR $UNPRIVPORTS \
-d ANYWHERE 80 -j ACCEPT
```

```
ipchains -A input -i $CHOKE_DMZ_INTERFACE -p tcp ! -y \
-s ANYWHERE 80 \
-d CHOKE_DMZ_IPADDR $UNPRIVPORTS -j ACCEPT
```

表 4.37 列出了 SSL 服务的客户端协议。

### 表 4.37 关口 SSL 客户端协议

| 描述 | 协议 | 远程地址 | 远程端口 | 入/出 | 本地地址 | 本地端口 | TCP 标志 |
|---|---|---|---|---|---|---|---|
| 关口客户端请求 | TCP | ANYWHERE | 443 | 出 | `CHOKE_DMZ_IPADDR` | 1024:65535 | 任意 |
| 远程服务器响应 | TCP | ANYWHERE | 443 | 入 | `CHOKE_DMZ_IPADDR` | 1024:65535 | ACK |

# 第 4 章 局域网、多防火墙与边界网络

本节允许本地主机连接到堡垒和远程主机上的安全 Web 服务器：

```
ipchains -A output -i $CHOKE_DMZ_INTERFACE -p tcp \
-s CHOKE_DMZ_IPADDR $UNPRIVPORTS \
-d ANYWHERE 443 -j ACCEPT
```

```
ipchains -A input -i $CHOKE_DMZ_INTERFACE -p tcp ! -y \
-s ANYWHERE 443 \
-d CHOKE_DMZ_IPADDR $UNPRIVPORTS -j ACCEPT
```

表 4.38 列出了 Web 代理服务的客户端协议。

| 描述 | 协议 | 远程地址 | 远程端口 | 入/出 | 本地地址 | 本地端口 | 标志 |
| --- | --- | --- | --- | --- | --- | --- |
| 关口客户端请求 | TCP | `WEB_PROXY_SERVER` | `WEB_PROXY_PORT` | 出 | `CHOKE_DMZ_IPADDR` | 1024:65535 | 任意 |
| 远程服务器响应 | TCP | `WEB_PROXY_SERVER` | `WEB_PROXY_PORT` | 入 | `CHOKE_DMZ_IPADDR` | 1024:65535 | ACK |

本节允许本地主机连接到堡垒和远程主机上的安全 Web 代理服务器：

```
ipchains -A output -i $CHOKE_DMZ_INTERFACE -p tcp \
-s CHOKE_DMZ_IPADDR $UNPRIVPORTS \
-d WEB_PROXY_SERVER WEB_PROXY_PORT -j ACCEPT
```

```
ipchains -A input -i $CHOKE_DMZ_INTERFACE -p tcp ! -y \
-s WEB_PROXY_SERVER WEB_PROXY_PORT \
-d CHOKE_DMZ_IPADDR $UNPRIVPORTS -j ACCEPT
```

堡垒是一个通过器（conduit），Web 服务器在 DMZ 中运行，而关口是一个客户端。表 4.39 列出了 HTTP Web 服务的客户端/服务器协议。

## 隔离子网防火墙 (Screened-Subnet Firewall)

### 表 4.39 堡垒 HTTP 客户端与服务器

| 描述 | 协议 | 远程地址 | 远程端口 | 入/出 | 本地地址 | 本地端口 | TCP 标志 |
|---|---|---|---|---|---|---|---|
| DMZ 客户端请求 | TCP | `DMZ_ADDRESSES` | 1024:65535 | 入 | ANYWHERE | 80 | 任意 |
| 远程服务器响应 | TCP | `DMZ_ADDRESSES` | 1024:65535 | 出 | ANYWHERE | 80 | ACK |
| 远程客户端请求 | TCP | ANYWHERE | 1024:65535 | 出 | `WEB_SERVER_DMZ_IPADDR` | 80 | ACK |
| DMZ 服务器响应 | TCP | ANYWHERE | 1024:65535 | 入 | `WEB_SERVER_DMZ_IPADDR` | 80 | ACK |

本节允许本地主机连接到堡垒和远程主机上的 Web 服务器，并允许远程客户端连接到 DMZ 中的 Web 服务器：

```
ipchains -A input -i $BASTION_DMZ_INTERFACE -p tcp \
-s DMZ_ADDRESSES UNPRIVPORTS \
-d ANYWHERE 80 -j ACCEPT
```

```
ipchains -A output -i $BASTION_DMZ_INTERFACE -p tcp ! -y \
-s ANYWHERE 80 \
-d DMZ_ADDRESSES UNPRIVPORTS -j ACCEPT
```

```
ipchains -A output -i $BASTION_DMZ_INTERFACE -p tcp ! -y \
-s ANYWHERE UNPRIVPORTS \
-d WEB_SERVER_DMZ_IPADDR 80 -j ACCEPT
```

```
ipchains -A input -i $BASTION_DMZ_INTERFACE -p tcp ! -y \
-s WEB_SERVER_DMZ_IPADDR 80 \
-d ANYWHERE UNPRIVPORTS -j ACCEPT
```

表 4.40 列出了 SSL 的完整客户端/服务器协议。

### 表 4.40 堡垒 SSL 客户端与服务器

| 描述 | 协议 | 远程地址 | 远程端口 | 入/出 | 本地地址 | 本地端口 | TCP 标志 |
|---|---|---|---|---|---|---|---|
| DMZ 客户端请求 | TCP | `DMZ_ADDRESSES` | 1024:65535 | 入 | ANYWHERE | 443 | 任意 |
| 远程服务器响应 | TCP | `DMZ_ADDRESSES` | 1024:65535 | 出 | ANYWHERE | 443 | ACK |
| 远程客户端请求 | TCP | ANYWHERE | 1024:65535 | 出 | `WEB_SERVER_DMZ_IPADDR` | 443 | 任意 |
| DMZ 服务器响应 | TCP | ANYWHERE | 1024:65535 | 入 | `WEB_SERVER_DMZ_IPADDR` | 443 | ACK |

本节允许本地主机连接到堡垒和远程主机上的 Web 服务器，并允许远程客户端连接到 DMZ 中的安全服务器：
