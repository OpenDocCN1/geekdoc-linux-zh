
# 主动模式（PORT）FTP 数据通道

接下来的两条规则允许标准的数据通道连接，即远程服务器通过回调从服务器 20 端口连接到客户端指定的非特权端口，以建立数据连接。

```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A INPUT -i $INTERNET -p tcp \
--sport 20 \
-d $IPADDR --dport $UNPRIVPORTS \
-m state --state NEW -j ACCEPT
fi
```

```bash
$IPT -A INPUT -i $INTERNET -p tcp \
--sport 20 \
-d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

```bash
$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
-s $IPADDR --sport $UNPRIVPORTS \
--dport 20 -j ACCEPT
```

这种不寻常的回调行为（即远程服务器与你的客户端建立次要连接）是 FTP 在数据包过滤层级难以保证安全的原因之一。

# 被动模式（PASSIVE）FTP 数据通道

接下来的两条规则允许大多数 Web 浏览器使用的较新的被动数据通道模式：

```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
--dport $UNPRIVPORTS -m state --state NEW -j ACCEPT
fi
```

```bash
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
--dport $UNPRIVPORTS -j ACCEPT
```

```bash
$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
--sport $UNPRIVPORTS \
-d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

被动模式被认为比主动模式更安全，因为 FTP 客户端会发起控制和数据连接，即使连接是在两个非特权端口之间建立的。此外，正如前文所述，被动模式没有主动模式在客户端方面所存在的 NAT 问题。

## 允许入站访问你的本地 FTP 服务器

是否向外界提供 FTP 服务是一个艰难的决定。虽然互联网上 FTP 站点众多，但 FTP 服务器的配置需要格外小心。存在许多可能的 FTP 安全漏洞利用。

如果你的目标是允许对机器上某些文件集进行通用的只读访问，你可能需要考虑通过 Web 服务器使这些文件可用。如果你的目标是允许从外部向你的机器上传文件，则应在防火墙层级、xinetd 配置层级、tcp_wrappers 层级和 FTP 配置层级上严格限制 FTP 服务器访问。

无论如何，如果你决定提供 FTP 服务并允许入站文件传输，则不应允许通过匿名 FTP 进行写入操作。对文件系统的远程写入访问应仅允许来自特定的已认证 FTP 用户账户、特定的远程站点，并且只能访问文件系统中经过严格控制和限制、专门保留的 FTP 区域。最好是从 chroot 环境中托管 FTP 区域。

### 入站 FTP 请求

接下来的两条规则允许入站控制连接到达你的 FTP 服务器：

```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A INPUT -i $INTERNET -p tcp \
       --sport $UNPRIVPORTS \
       -d $IPADDR --dport 21 \
       -m state --state NEW -j ACCEPT
fi
```

```bash
$IPT -A INPUT -i $INTERNET -p tcp \
     --sport $UNPRIVPORTS \
     -d $IPADDR --dport 21 -j ACCEPT
```

```bash
$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
     -s $IPADDR --sport 21 \
     --dport $UNPRIVPORTS -j ACCEPT
```

## 主动模式（PORT）FTP 数据通道响应

接下来的两条规则允许 FTP 服务器回调远程客户端并建立次要数据通道连接：

```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A OUTPUT -o $INTERNET -p tcp \
       --sport 20 \
       -d $IPADDR --dport $UNPRIVPORTS \
       -m state --state NEW -j ACCEPT
fi
```

```bash
$IPT -A OUTPUT -o $INTERNET -p tcp \
       --sport 20 \
       -d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

```bash
$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
       --sport $UNPRIVPORTS \
       -d $IPADDR --dport 20 -j ACCEPT
```

## 被动模式（PASSIVE）FTP 数据通道响应

接下来的两条规则允许远程 FTP 客户端与本地服务器建立次要数据通道连接。

```bash
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
-dport $UNPRIVPORTS -j ACCEPT
```

> **注意**
>
> 不要在互联网上使用 tFTP！tFTP 提供的是简化版、未认证的 FTP 服务的 UDP 版本。它旨在让受信主机在局域网内将启动软件加载到路由器和无盘工作站中。有些人误将 tFTP 视为 FTP 的替代方案。绝对不要在互联网上使用它，句号。最好根本不要在系统中安装 tFTP。

# Web 服务

Web 服务基于超文本传输协议（HTTP）。客户端和服务器连接使用标准的 TCP 约定。除了标准的通用 HTTP 访问外，还有几种更高级的、专用通信协议可用，包括通过 SSL 或 TLS 的安全访问，以及通过 ISP 提供的 Web 服务器代理的访问。这些不同的访问协议使用不同的服务端口。

## 标准 HTTP 访问（TCP 端口 80）

在正常使用中，Web 服务通过 **http** 服务端口 **80** 提供。表 4.8 列出了 HTTP Web 服务的完整客户端/服务器连接协议。

**表 4.8**
**HTTP 协议**

| 描述 | 协议 | 远程地址 | 远程端口 | 本地进/出 | 本地地址 | 本地端口 | TCP 标志 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 本地客户端请求 | TCP | ANYWHERE | 80 | 出 | IPADDR | 1024:65535 | 任意 |
| 远程服务器响应 | TCP | ANYWHERE | 80 | 入 | IPADDR | 1024:65535 | ACK |
| 远程客户端请求 | TCP | ANYWHERE | 1024:65535 | 入 | IPADDR | 80 | 任意 |
| 本地服务器响应 | TCP | ANYWHERE | 1024:65535 | 出 | IPADDR | 80 | ACK |

## 作为客户端访问远程网站

在当今世界，家庭站点不希望通过 Web 浏览器访问万维网，这几乎是不可想象的。接下来的两条规则允许访问远程 Web 服务器：

```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then
 $IPT -A OUTPUT -o $INTERNET -p tcp \
 -s $IPADDR --sport $UNPRIVPORTS \
 --dport 80 -m state --state NEW -j ACCEPT
fi
```

```bash
$IPT -A OUTPUT -o $INTERNET -p tcp \
 -s $IPADDR --sport $UNPRIVPORTS \
 --dport 80 -j ACCEPT
```

```bash
$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
 --sport 80 \
 -d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

## 允许远程访问本地 Web 服务器

如果你决定运行自己的 Web 服务器并托管一个公共网站，以下通用服务器规则允许所有典型的入站访问到你的站点。这是大多数人托管网站所需的全部：

```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A INPUT   -i $INTERNET -p tcp \
  --sport $UNPRIVPORTS \
  -d $IPADDR --dport 80 \
  -m state --state NEW -j ACCEPT
fi

$IPT -A INPUT   -i $INTERNET -p tcp \
  --sport $UNPRIVPORTS \
  -d $IPADDR --dport 80 -j ACCEPT

$IPT -A OUTPUT   -o $INTERNET -p tcp ! --syn \
  -s $IPADDR --sport 80 \
  --dport $UNPRIVPORTS -j ACCEPT
```

## 安全 Web 访问（SSL 和 TLS）（TCP 端口 443）

安全套接字层（SSL）和传输层安全（TLS）用于安全、加密的 Web 访问。这些协议使用 **TCP 端口 443**。当你去商业网站购买东西、使用在线银行服务或进入需要输入个人信息的受保护 Web 区域时，你最常会遇到这种情况。随 Red Hat Linux 7.1 发布的 Apache Web 服务器包含 OpenSSL 支持。表 4.9 列出了该服务的完整客户端/服务器连接协议。

**表 4.9**
SSL 和 TLS 协议

| 描述 | 协议 | 远程地址 | 远程端口 | 进/出 | 本地地址 | 本地端口 | TCP 标志 |
|:------------|:---------|:---------------|:------------|:-------|:--------------|:-----------|:---------|
| 本地客户端请求 | TCP | ANYWHERE | 443 | 出 | IPADDR | 1024:65535 | 任意 |
| 远程服务器响应 | TCP | ANYWHERE | 443 | 入 | IPADDR | 1024:65535 | ACK |
| 远程客户端请求 | TCP | ANYWHERE | 1024:65535 | 入 | IPADDR | 443 | 任意 |
| 本地服务器响应 | TCP | ANYWHERE | 1024:65535 | 出 | IPADDR | 443 | ACK |

## 作为客户端通过 SSL 或 TLS 访问远程网站

大多数人最终都会希望有客户端访问安全网站的需求：

```bash
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT   -o $INTERNET -p tcp \
  -s $IPADDR --sport $UNPRIVPORTS \
  --dport 443 -m state --state NEW -j ACCEPT
fi
```

