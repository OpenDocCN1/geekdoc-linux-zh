
```
$IPT -A INPUT -i $INTERNET -p tcp \
  --sport $UNPRIVPORTS \
  -d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

```
$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
  -s $IPADDR --sport $UNPRIVPORTS \
  --dport $UNPRIVPORTS -j ACCEPT
```

## 注意

不要在互联网上使用 TFTP！TFTP 提供的是 FTP 服务的简化版、未认证的 UDP 版本。它旨在用于从可信主机通过本地网络向路由器和无盘工作站加载引导软件。有些人将 TFTP 误认为是 FTP 的替代品。绝对不要在互联网上使用它。最好根本不要在系统中安装 TFTP。

## 5.7.6 Web 服务

Web 服务基于超文本传输协议 `HTTP`。客户端和服务器连接使用标准的 TCP 约定。除了标准的通用 HTTP 访问外，还有几种更高级的专用通信协议，包括通过 SSL 或 TLS 的安全访问，以及通过 ISP 提供的 Web 代理进行的访问。这些不同的协议使用不同的端口。

### 标准 HTTP 访问 (TCP 端口 80)

在正常使用中，Web 服务通过 `http` 服务端口 `80` 提供。表 7.8 列出了 HTTP Web 服务的客户端/服务器连接协议。

#### 7.8 HTTP 协议

| 描述 | 协议 | 远程地址 | 远程端口 | 本地输入/输出 | 本地地址 | 本地端口 | TCP 标志 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 本地客户端请求 | TCP | ANYWHERE | 80 | 输出 | `$IPADDR` | 1024:65535 | 任意 | |
| 远程服务器响应 | TCP | ANYWHERE | 80 | 输入 | `$IPADDR` | 1024:65535 | ACK | |
| 远程客户端请求 | TCP | ANYWHERE | 1024:65535 | 输入 | `$IPADDR` | 80 | 任意 | |
| 本地服务器响应 | TCP | ANYWHERE | 1024:65535 | 输出 | `$IPADDR` | 80 | ACK | |

### 作为客户端访问远程站点

在当今世界，家庭站点不想通过 Web 浏览器访问万维网几乎是不可想象的。以下两条规则允许访问远程 Web 服务器：

```
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o $INTERNET -p tcp \
  -s $IPADDR --sport $UNPRIVPORTS \
  --dport 80 -m state --state NEW -j ACCEPT
fi
```

```
$IPT -A OUTPUT -o $INTERNET -p tcp \
  -s $IPADDR --sport $UNPRIVPORTS \
  --dport 80 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
  --sport 80 \
  -d $IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

### 允许远程访问本地 Web 服务器

如果您决定运行自己的 Web 服务器并托管一个公共网站，以下通用服务器规则允许所有典型的入站访问到您的站点。大多数人托管网站只需要这些设置：

```
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A INPUT -i $INTERNET -p tcp \
  --sport $UNPRIVPORTS \
  -d $IPADDR --dport 80 \
  -m state --state NEW -j ACCEPT
fi
```

```
$IPT -A INPUT -i $INTERNET -p tcp \
  --sport $UNPRIVPORTS \
  -d $IPADDR --dport 80 -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
  -s $IPADDR --sport 80 \
  --dport $UNPRIVPORTS -j ACCEPT
```

### 安全 Web 访问 (SSL 和 TLS) (TCP 端口 443)

安全套接字层 `SSL` 和传输层安全 `TLS` 用于安全、加密的 Web 访问。这些协议使用 TCP 端口 `443`。如果您去商业网站购买东西、使用在线银行服务或进入需要输入个人信息的受保护 Web 区域，您最常会遇到这些服务。随 Red Hat Linux 7.1 提供的 Apache Web 服务器实现了 OpenSSL 支持。表 7.9 列出了该服务的完整客户端/服务器连接协议。

#### 表 7.9 SSL 和 TLS 协议

| 描述 | 协议 | 远程地址 | 远程端口 | 入/出 | 本地地址 | 本地端口 | TCP 标志 |
|---|---|---|---|---|---|---|---|
| 本地客户端请求 | TCP | 任意位置 | 443 | 出 | IPADDR | 1024:65535 | 任意 |
| 远程服务器响应 | TCP | 任意位置 | 443 | 入 | IPADDR | 1024:65535 | ACK |
| 远程客户端请求 | TCP | 任意位置 | 1024:65535 | 入 | IPADDR | 443 | 任意 |
| 本地服务器响应 | TCP | 任意位置 | 1024:65535 | 出 | IPADDR | 443 | ACK |

### 作为客户端通过 SSL 或 TLS 访问远程网站

大多数人最终都会希望客户端能够访问安全网站：

```bash
if [ "CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o $INTERNET -p tcp \
  -s IPADDR --sport $UNPRIVPORTS \
  --dport 443 -m state NEW -j ACCEPT
fi

$IPT -A OUTPUT -o $INTERNET -p tcp \
  -s IPADDR --sport $UNPRIVPORTS \
  --dport 443 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
  --sport 443 \
  -d IPADDR --dport $UNPRIVPORTS -j ACCEPT
```

### 允许对本地 SSL 或 TLS Web 服务器的远程访问

如果你使用某种形式的电子商务或拥有经过用户验证的 Web 区域，你很可能希望允许入站连接到网站的加密保护区域。否则，你不需要本地服务器规则。

Linux 自带的 OpenSSL 和标准的 SSL 支持包均可用于 Apache Web 服务器。有关更多信息，请参阅 `http://www.apache.org/`。

以下规则允许使用 SSL 或 TLS 协议对您的 Web 服务器进行入站访问：

```bash
if [ "CONNECTION_TRACKING" = "1" ]; then
$IPT -A INPUT -i $INTERNET -p tcp \
  --sport $UNPRIVPORTS \
  -d $IPADDR --dport 443 \
  -m state --state NEW -j ACCEPT
fi

$IPT -A INPUT -i $INTERNET -p tcp \
  --sport $UNPRIVPORTS \
  -d $IPADDR --dport 443 -j ACCEPT

$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
  -s $IPADDR --dport 443 \
  --dport $UNPRIVPORTS -j ACCEPT
```

## 7.5 启用常见 TCP 服务

### Web 代理访问 (TCP 端口 8008, 8080)

公开可访问的 Web 服务器代理最常见于 ISP（互联网服务提供商）。作为客户，您配置浏览器使用远程代理服务。Web 代理通过 ISP 定义的用于此目的的两个特权端口之一进行访问，即端口 `8008` 或 `8080`。作为回报，当页面在您的 ISP 服务器上很容易缓存时，您将获得更快的页面访问速度，并且通过代理访问远程站点具有相对的匿名性。您的连接不是直接的，而是由您的 ISP 的代理代替您完成的。表 7.10 列出了 Web 代理服务的完整客户端/服务器连接协议。

#### 表 7.10 Web 代理协议

| 描述 | 协议 | 远程地址 | 远程端口 | 入/出 | 本地地址 | 本地端口 | TCP 标志 |
