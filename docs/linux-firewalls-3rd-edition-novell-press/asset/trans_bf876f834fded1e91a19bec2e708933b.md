
## 受限主机（CHOKES）的 SSH 配置

第一条规则允许受限主机（choke machine）连接到运行在 DMZ 中的 sshd 服务器，包括网关防火墙主机：

```bash
$IPT -A OUTPUT -o $DMZ_INTERFACE -p tcp \
-s $DMZ_IPADDR --sport $UNPRIVPORTS \
-d $DMZ_ADDRESSES --port 22 \
-m state --state NEW -j ACCEPT
```

下一条规则将来自局域网客户端的连接转发到任何远程服务器：

```bash
$IPT -A FORWARD -i $LAN_INTERFACE -o $DMZ_INTERFACE -p tcp \
-s $LAN_ADDRESSES --sport $UNPRIVPORTS --port 22 \
-m state --state NEW -j ACCEPT
```

最后一条规则将来自选定远程客户端地址的连接转发到特定的本地主机，在本例中，该本地主机位于局域网中：

```bash
$IPT -A FORWARD -i $DMZ_INTERFACE -o $LAN_INTERFACE -p tcp \
-s <selected remote host> --sport $UNPRIVPORTS \
-d <selected LAN host> --port 22 \
-m state --state NEW -j ACCEPT
```

## FTP（TCP 端口 21 和 20）

FTP 在客户端和服务器之间交换数据有两种模式：正常数据通道端口模式（Port Mode）和被动数据通道模式（Passive Mode）。当使用 FTP 客户端程序连接到远程 FTP 站点时，默认机制为端口模式。当通过 Web 浏览器连接到 FTP 站点时，使用的机制为被动模式。偶尔，您可能会遇到只支持其中一种模式的 FTP 站点。

本节描述了客户端和服务器 FTP 组合的两种方法：

- 网关仅作为通往远程 FTP 服务器的通道；受限主机和局域网主机为客户端。
- FTP 服务器运行在 DMZ 中；受限主机、局域网主机和远程主机为客户端。

### 网关作为通往远程 FTP 服务器的通道

大多数站点需要 FTP 客户端访问远程文件仓库，这几乎是必然的。第一部分允许内部主机连接到远程 FTP 服务器。

以下规则允许从受限主机和局域网机器发起出站 FTP 客户端连接。常量是网关上使用的：

### 出站 FTP 客户端请求

```bash
$IPT -A FORWARD -i $DMZ_INTERFACE -o $EXTERNAL_INTERFACE -p tcp \
-s $LAN_ADDRESSES --sport $UNPRIVPORTS --dport 21 \
-m state --state NEW -j ACCEPT

$IPT -A FORWARD -i $DMZ_INTERFACE -o $EXTERNAL_INTERFACE -p tcp \
-s $CHOKE_IPADDR --sport $UNPRIVPORTS --dport 21 \
-m state --state NEW -j ACCEPT
```

**ip_conntrack_ftp** 模块负责处理 RELATED 规则的一部分，即端口或被动模式数据连接。不需要针对数据连接的特定规则。

这里包含两对数据通道连接请求规则，以求完整：

### 端口模式数据通道响应

```bash
$IPT -A FORWARD -i $EXTERNAL_INTERFACE -o $DMZ_INTERFACE -p tcp \
--sport 20 -d $LAN_ADDRESSES --dport $UNPRIVPORTS \
-m state --state NEW -j ACCEPT

$IPT -A FORWARD -i $EXTERNAL_INTERFACE -o $DMZ_INTERFACE -p tcp \
--sport 20 -d $CHOKE_IPADDR --dport $UNPRIVPORTS \
-m state --state NEW -j ACCEPT
```

### 被动模式数据通道响应

```bash
$IPT -A FORWARD -i $DMZ_INTERFACE -o $EXTERNAL_INTERFACE -p tcp \
-s $LAN_ADDRESSES --sport $UNPRIVPORTS --dport $UNPRIVPORTS \
-m state --state NEW -j ACCEPT

$IPT -A FORWARD -i $DMZ_INTERFACE -o $EXTERNAL_INTERFACE -p tcp \
-s $CHOKE_IPADDR --sport $UNPRIVPORTS --dport $UNPRIVPORTS \
-m state --state NEW -j ACCEPT
```

受限主机的客户端规则包含在即将出现的“受限主机作为 FTP 服务器通道和客户端”部分中。

### DMZ 中的 FTP 服务器，受限主机、本地主机和远程主机作为客户端

本节定义了允许使用 FTP 的入站客户端请求的规则。

### 网关作为通往 FTP DMZ 服务器的通道

在网关上，下一条规则将来自任何远程机器的入站 FTP 客户端连接转发到 DMZ 中的服务器。使用此代码时，请注意需要定义常量 `DMZ_FTP_SERVER`：

```bash
$IPT -A FORWARD -i $EXTERNAL_INTERFACE -o $DMZ_INTERFACE -p tcp \
-s $UNPRIVPORTS -d $DMZ_FTP_SERVER --dport 21 \
-m state --state NEW -j ACCEPT
```

### 受限主机作为通往 FTP 服务器的通道和客户端

以下规则允许来自局域网和受限主机的出站 FTP 客户端连接到任何地方的 FTP 服务器。受限主机的规则并未专门提及 DMZ。

第一条规则将来自任何局域网机器的出站 FTP 客户端连接转发到任何服务器：

```bash
$IPT -A FORWARD -i $LAN_INTERFACE -o $DMZ_INTERFACE -p tcp \
-s $LAN_ADDRESSES --sport $UNPRIVPORTS --dport 21 \
-m state --state NEW -j ACCEPT
```

第二条规则允许从受限主机本身访问 FTP 客户端：

```bash
$IPT -A OUTPUT -o $DMZ_INTERFACE -p tcp \
-s $DMZ_IPADDR --sport $UNPRIVPORTS --dport 21 \
-m state --state NEW -j ACCEPT
```

### Web 服务

Web 服务通常基于 HTTP 协议。几种更高层的通信协议用于特殊目的，包括用于 Web 代理和缓存访问的特定协议（在 `/etc/services` 中 TCP 端口 **8080** 上的 **webcache**），以及用于安全访问的 SSL 和 TLS（在 /etc/services 中 TCP 端口 443 上的 https）。squid Web 代理默认使用 TCP 端口 3128（在 /etc/services 中 TCP 端口 3128 上的 squid）。

本节描述了客户端和服务器 Web 组合的四种方法：

- 网关仅作为本地 Web 客户端连接到远程 Web 服务器的通道；受限主机和局域网为客户端。
- 受限主机既充当转发器，也充当客户端。
- Web 服务器运行在 DMZ 中；受限主机、局域网和远程主机为客户端。
- Web 代理运行在 DMZ 中；受限主机和局域网为客户端。

### 网关作为本地 Web 客户端的通道

以下代码的第一部分允许本地主机连接到运行在远程主机上的 Web 服务器。

在网关上，以下规则将来自受限主机以及位于受限防火墙后面的私有局域网中机器的本地客户端连接转发出去：

```bash
$IPT -A FORWARD -i $DMZ_INTERFACE -o $EXTERNAL_INTERFACE -p tcp \
   -s $LAN_ADDRESSES --sport $UNPRIVPORTS --dport 80 \
   -m state --state NEW -j ACCEPT
```

```bash
$IPT -A FORWARD -i $DMZ_INTERFACE -o $EXTERNAL_INTERFACE -p tcp \
   -s $LAN_ADDRESSES --sport $UNPRIVPORTS --dport 443 \
   -m state --state NEW -j ACCEPT
```

```bash
$IPT -A FORWARD -i $DMZ_INTERFACE -o $EXTERNAL_INTERFACE -p tcp \
   -s $CHOKE_IPADDR --sport $UNPRIVPORTS --dport 80 \
   -m state --state NEW -j ACCEPT
```

```bash
$IPT -A FORWARD -i $DMZ_INTERFACE -o $EXTERNAL_INTERFACE -p tcp \
   -s $CHOKE_IPADDR --sport $UNPRIVPORTS --dport 443 \
   -m state --state NEW -j ACCEPT
```

### 受限主机作为转发器和 Web 客户端

在此示例中，受限主机既充当转发器，也充当客户端。以下规则将来自局域网的本地客户端连接转发出去，并允许来自受限主机本身的客户端连接：

```bash
$IPT -A FORWARD -i $LAN_INTERFACE -o $DMZ_INTERFACE -p tcp \
   -s $LAN_ADDRESSES --sport $UNPRIVPORTS --dport 80 \
   -m state --state NEW -j ACCEPT
```

```bash
$IPT -A OUTPUT -o $DMZ_INTERFACE -p tcp \
   -s $DMZ_IPADDR --sport $UNPRIVPORTS --dport 80 \
   -m state --state NEW -j ACCEPT
```

```bash
$IPT -A FORWARD -i $LAN_INTERFACE -o $DMZ_INTERFACE -p tcp \
   -s $LAN_ADDRESSES --sport $UNPRIVPORTS --dport 443 \
   -m state --state NEW -j ACCEPT
```

```bash
$IPT -A OUTPUT -o $DMZ_INTERFACE -p tcp \
   -s $DMZ_IPADDR --sport $UNPRIVPORTS --dport 443 \
   -m state --state NEW -j ACCEPT
```

### DMZ 中的公共 Web 服务器；受限主机、局域网和远程主机作为客户端

在此示例中，该站点在 DMZ 中托管一个公共 Web 服务器。

网关是一个双向通道，允许公共访问本地服务器，同时继续使用前面部分中介绍的规则允许本地访问远程站点。这些规则适用于网关，并且需要预定义常量 DMZ_WEB_SERVER：

```bash
$IPT -A FORWARD -i $EXTERNAL_INTERFACE -o $DMZ_INTERFACE -p tcp \
    -s $UNPRIVPORTS -d $DMZ_WEB_SERVER --dport 80 \
-m state --state NEW -j ACCEPT
```

```bash
$IPT -A FORWARD -i $EXTERNAL_INTERFACE -o $DMZ_INTERFACE -p tcp \
    -s $UNPRIVPORTS -d $DMZ_WEB_SERVER --dport 443 \
-m state --state NEW -j ACCEPT
```

```bash
$IPT -A FORWARD -i $DMZ_INTERFACE -o $EXTERNAL_INTERFACE -p tcp \
-s $LAN_ADDRESSES --sport $UNPRIVPORTS --dport 80 \
-m state --state NEW -j ACCEPT
```

```bash
$IPT -A FORWARD -i $DMZ_INTERFACE -o $EXTERNAL_INTERFACE -p tcp \
-s $LAN_ADDRESSES --sport $UNPRIVPORTS --dport 443 \
-m state --state NEW -j ACCEPT
```

```bash
$IPT -A FORWARD -i $DMZ_INTERFACE -o $EXTERNAL_INTERFACE -p tcp \
-s $CHOKE_IPADDR --sport $UNPRIVPORTS --dport 80 \
-m state --state NEW -j ACCEPT
```

```bash
$IPT -A FORWARD -i $DMZ_INTERFACE -o $EXTERNAL_INTERFACE -p tcp \
-s $CHOKE_IPADDR --sport $UNPRIVPORTS --dport 443 \
-m state --state NEW -j ACCEPT
```

受限主机的规则与前一节中的保持不变。

### DMZ 中的 Web 代理；网关作为通道；受限主机和局域网作为客户端

虽然有可能从内部局域网服务器提供公共 Web 服务，但通常不会这样做，因为配置错误的服务器和 CGI 脚本具有更大的安全漏洞风险，且倾向于将私有信息与公共信息隔离。也就是说，同时托管私有内部网站和公共网站的站点，通常在位于不同局域网的不同机器上运行多个 Web 服务器。更常见的场景是从位于外围网络上的主机托管公共网站。

