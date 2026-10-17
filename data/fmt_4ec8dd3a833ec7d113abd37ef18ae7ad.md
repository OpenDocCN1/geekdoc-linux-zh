
| DMZ 服务器响应 | TCP | DMZ_ADDRESSES | 23 | In | BASTION_DMZ_IPADDR | 1024:65535 | ACK |

# 格式化子网防火墙

注意，仅允许来自 choke 防火墙的入站 telnet 连接，而不允许从 DMZ 中的其他机器访问 telnet：

```
ipchains -A output -i $BASTION_DMZ_INTERFACE -p tcp -y \
  -s ANYWHERE 23 \
  -d $CHOKE_DMZ_IPADDR:$UNPRIVORTS
```

接下来两条规则允许从 bastion 访问 DMZ 中的任何机器：

```
ipchains -A output -i $BASTION_DMZ_INTERFACE -p tcp \
  -s $BASTION_DMZ_IPADDR:$UNPRIVORTS \
  -d $DMZ_ADDRESSES 23 -j ACCEPT
```

```
ipchains -A input -i $BASTION_DMZ_INTERFACE -p tcp -y \
  -s $DMZ_ADDRESSES 23 \
  -d $BASTION_DMZ_IPADDR:$UNPRIVORTS -j ACCEPT
```

# Choke Telnet DMZ 配置

表 4.22 列出了 Telnet 服务的完整客户端/服务器连接协议。

表 4.22 Choke Telnet 协议

| 描述 | 协议 | 远程地址 | 远程端口 | 出方向 | 本地地址 | 本地端口 | 标记 |
|---|---|---|---|---|---|---|---|
| Choke 请求 | TCP | ANYWHERE | 23 | Out | CHOKE_DMZ_IPADDR | 1024:65535 | Any |
| 远程服务器响应 | TCP | ANYWHERE | 23 | In | CHOKE_DMZ_IPADDR | 1024:65535 | ACK |
| Bastion 客户端请求 | TCP | BASTION_DMZ_IPADDR | 23 | In | BASTION_DMZ_IPADDR | 23 | Any |
| Choke 服务器响应 | TCP | BASTION_DMZ_IPADDR | 23 | Out | BASTION_DMZ_IPADDR | 23 | ACK |

注意，允许向任何地方建立出站 telnet 连接，以允许需要 telnet 到互联网上远程站点的 LAN 客户端。

```
ipchains -A output -i $CHOKE_DMZ_INTERFACE -p tcp -y \
  -s $CHOKE_DMZ_IPADDR:$UNPRIVORTS \
  -d ANYWHERE 23 -j ACCEPT
```

```
ipchains -A input -i $CHOKE_DMZ_INTERFACE -p tcp -y \
  -s ANYWHERE 23 \
  -d $CHOKE_DMZ_IPADDR:$UNPRIVORTS -j ACCEPT
```

这些规则允许从 bastion 访问 choke 防火墙。不允许从 DMZ 中的其他机器进行入站 telnet 访问：

```
ipchains -A input -i $CHOKE_DMZ_INTERFACE -p tcp \
  -s $BASTION_DMZ_IPADDR:$UNPRIVORTS \
  -d $CHOKE_DMZ_IPADDR 23 -j ACCEPT
```

```
ipchains -A output -i $CHOKE_DMZ_INTERFACE -p tcp ! -y \
  -s $CHOKE_DMZ_IPADDR 23 \
  -d $BASTION_DMZ_IPADDR:$UNPRIVORTS -j ACCEPT
```

# SSH (TCP 端口 22)

客户端和服务器规则允许从任何地方访问。在实践中，家庭基站点可能会将外部地址限制为特定的子集，因为连接的末端都必须配置为识别每个用户账户。虽然不建议使用 `inet` 来启动 `sshd`，但 ssh 可以编译为仅允许 `/etc/hosts` 中的主机访问列表。

# Bastion SSH 服务器配置

表 4.23 Bastion 服务器列出了 SSH 服务的连接协议。

| 描述 | 协议 | 远程地址 | 远程端口 | 出方向 | 本地地址 | 本地端口 | 标记 |
|---|---|---|---|---|---|---|---|
| Choke 客户端查询 | TCP | ANYWHERE | 23 | Out | CHOKE_DMZ_IPADDR | 1024:65535 | Any |
| 服务器响应 | TCP | ANYWHERE | 23 | In | CHOKE_DMZ_IPADDR | 1024:65535 | ACK |
| Bastion 客户端请求 | TCP | BASTION_DMZ_IPADDR | 23 | In | BASTION_DMZ_IPADDR | 23 | Any |
| Choke 服务器响应 | TCP | BASTION_DMZ_IPADDR | 23 | Out | BASTION_DMZ_IPADDR | 23 | ACK |

这些规则允许在 bastion 上运行 ssh 到外部站点：

```
ipchains -A output -i $BASTION_DMZ_INTERFACE -p tcp \
  -s $BASTION_DMZ_IPADDR:$UNPRIVORTS \
  -d ANYWHERE 22 -j ACCEPT
```

```
ipchains -A input -i $BASTION_DMZ_INTERFACE -p tcp ! -y \
  -s ANYWHERE 22 \
  -d $BASTION_DMZ_IPADDR:$UNPRIVORTS -j ACCEPT
```

# Bastion SSH 客户端 DMZ 配置

表 4.24 列出了 SSH 服务的协议。

表 4.24 Bastion SSH 协议

| 描述 | 协议 | 远程地址 | 远程端口 | 出方向 | 本地地址 | 本地端口 | 标记 |
|---|---|---|---|---|---|---|---|
| Bastion 客户端请求 | TCP | DMZ_ADDRESSES | 22 | Out | BASTION_DMZ_IPADDR | 1024:65535 | Any |
| DMZ 服务器响应 | TCP | DMZ_ADDRESSES | 22 | In | BASTION_DMZ_IPADDR | 1024:65535 | ACK |
| Bastion 客户端请求 | TCP | BASTION_DMZ_IPADDR | 23 | In | BASTION_DMZ_IPADDR | 23 | Any |
| DMZ 服务器响应 | TCP | BASTION_DMZ_IPADDR | 23 | Out | BASTION_DMZ_IPADDR | 23 | ACK |

这些规则允许 bastion 访问 DMZ 中的所有机器：

```
ipchains -A output -i $BASTION_DMZ_INTERFACE -p tcp | \
  -s $BASTION_DMZ_IPADDR:$UNPRIVORTS \
  -d $DMZ_ADDRESSES 22 -j ACCEPT
```

```
ipchains -A input -i $BASTION_DMZ_INTERFACE -p tcp | -y | \
  -s $DMZ_ADDRESSES 22 \
  -d $BASTION_DMZ_IPADDR:$UNPRIVORTS -j ACCEPT
```

# Choke SSH 客户端协议 DMZ 配置

表 4.25 列出了 SSH 服务的客户端连接协议。

## 表 4.25 Choke SSH 客户端协议

| 描述 | 协议 | 远程地址 | 远程端口 | 入/出 | 本地地址 | 本地端口 | TCP 标志 |
|---|---|---|---|---|---|---|---|
| Choke 客户端请求 | TCP | ANYWHERE | 22 | 出 | CHOKE_DMZ_IPADDR | 1024:65535 | Any |
| 远程服务器响应 | TCP | ANYWHERE | 22 | 入 | CHOKE_DMZ_IPADDR | 1024:65535 | ACK |
| Choke 客户端请求 | TCP | ANYWHERE | 22 | 出 | CHOKE_DMZ_IPADDR | 513:1023 | Any |
| 远程服务器响应 | TCP | ANYWHERE | 22 | 入 | CHOKE_DMZ_IPADDR | 513:1023 | ACK |

这些规则允许你使用 ssh 连接远程站点：
