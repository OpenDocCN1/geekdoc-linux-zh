
```
HTTP/1.0 200 OK
Date: Sun, 12 Aug 2007 00:46:39 GMT
Server: Apache/1.3.31 (Unix)
Content-Location: index.html
Variant: accept-language,accept-charset
TCN: choice
Last-Modified: Fri, 04 May 2001 00:00:38 GMT

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.0 Transitional//EN">
<html xmlns="http://www.w3.org/TR/html1/html1-transitional.dtd">
<head>
<title>Test Page for Apache Installation</title>
</head>
<body
Background white, links blue (unvisited), navy (visited), red
</body>
</html>
```

查看这些内容最详尽的方法是使用 `Netcat` 连接到 Web 服务器并发布 HTTP 请求：

```
nc localhost 443

HEAD / HTTP/1.1

Host: localhost
```

```
HTTP/1.1 200 OK
Date: Sun, 12 Aug 2007 00:46:39 GMT
Server: Apache/1.3.31 (Unix)
Content-Location: index.html
Variant: accept-language,accept-charset
TCN: choice
Last-Modified: Fri, 04 May 2001 00:00:38 GMT

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.0 Transitional//EN">
<html xmlns="http://www.w3.org/TR/html1/html1-transitional.dtd">
<head>
<title>Test Page for Apache Installation</title>
</head>
<body
Background white, links blue (unvisited), navy (visited), red
</body>
</html>
```

查看这些内容最详尽的方法是使用 `Netcat` 连接到 Web 服务器并发布 HTTP 请求：

```
nc localhost 80

HEAD / HTTP/1.0

Host: localhost
```

```
HTTP/1.0 200 OK
Date: Sun, 12 Aug 2007 00:46:39 GMT
Server: Apache/1.3.31 (Unix)
Content-Location: index.html
Variant: accept-language,accept-charset
TCN: choice
Last-Modified: Fri, 04 May 2001 00:00:38 GMT

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.0 Transitional//EN">
<html xmlns="http://www.w3.org/TR/html1/html1-transitional.dtd">
<head>
<title>Test Page for Apache Installation</title>
</head>
<body
Background white, links blue (unvisited), navy (visited), red
</body>
</html>
```

在攻击者连接到你的网络之前，他们可能已经建立了关于你组织、人员和内部系统的画像，这使得他们能够制定出更详细、更精确的攻击。这种攻击可能采取社会工程的形式：
- 社会工程
- 利用配置不当的 Web 服务器
- 使用收集到的身份凭据登录外部服务

# 防止被动画像分析和情报侦察：安全策略与意识培训

应该设计并执行安全策略，以最大限度地减少信息泄露，包括通过互联网、电话、电子邮件和面对面的泄露。应该建立严格的流程，规定在向内部和外部人员提供信息之前需要什么授权，以及哪些信息是实际上被允许提供的（例如密码）。

应该对所有员工进行意识培训，以确保他们理解违反安全策略对组织和自身产生的影响，以及为了确保敏感信息不落入他人手中而必须执行的流程。

IT 安全团队还应该审计这些流程是否正在执行，通过检查已发布的内容、在互联网上搜索与组织相关的信息，以及进行社会工程测试，以确保流程得到遵守。

组织还应该制定《应急响应计划》，以确保所有员工在遭遇社会工程攻击或任何其他类型的攻击时确切知道该做什么。如果没有应急响应计划，大多数组织将被迫临时创建一个，导致有关攻击的关键信息丢失。

# 主动式 Web 应用枚举

| 流行度: | 9 |
| :--- | :--- |
| 简单性: | 5 |
| 影响范围: | 5 |
| 风险评分: | 6 |

为了扩展或验证在被动画像分析阶段收集到的信息，攻击者可能会转向执行主动 Web 应用枚举。这涉及到实际连接到组织的系统，以收集通常无法通过互联网搜索引擎获取的信息。这允许攻击者确切地看到针对组织员工和系统可以实施哪些攻击。

# 第13 章：Web 应用攻击

## 端口和服务扫描

如果攻击者的目标是在攻击前不被发现，那么他/她可能会推迟任何端口扫描，并开始从画像阶段收集的组织 Web 应用中枚举信息。如果端口扫描得不够谨慎，可能会触发入侵检测系统 `IDS` 或入侵防御系统 `IPS`，从而向管理员报警——假设 `IDS` 和 `IPS` 配置正确。

通过对 `TCP` 上的常用端口（如 `80`, `81`, `82`, `443`, `8000`, `8001`, `8080`, `8128` 和 `8443`）进行端口扫描，可能会发现其他方法。以下代码列出了如何使用 `Nmap` 对范围 IP 地址的一部分常用端口进行简单扫描。`-P` 选项扫描主机发现过程，即使主机看起来未处于活动状态也会执行。

```
nmap -P -80,443,8080 192.168.1.11-20
```

还可以使用更高级的技术来绕过防火墙或避免 `IDS` 检测，例如分段数据包或操作 `MTU`、创建欺骗性扫描、探测源 IP 地址、将源端口设置为 `53`、设置 `TTL` 值以及发送带有错误校验和的数据包。其他端口扫描器包括 `Unicorn Scan`、`Amap` 和 `Hping`。`Hping` 是一个生成专门定制的自定义数据包投向目标的极佳工具，允许对产生的数据包进行低级控制。

## 目标指纹识别

在发现 Web 应用后，攻击者现在需要对运行在系统上的 Web 服务器和 Web 服务器模块进行指纹识别。

指纹识别可以通过多种方式进行。大多数端口扫描都可以配置为提取 `banner` 或进行服务和操作系统预测，从而让攻击者了解开放端口是否运行着 Web 应用。

管理员还可能配置其应用程序运行在非标准端口上，试图向攻击者隐藏它们，或者让他们认为端口后面运行着另一个服务。这被称为“通过模糊性实现安全”。`Amap` 是“Application Mapper”的缩写，旨在执行快速且可靠的应用协议检测。这允许攻击者通过端口扫描来轻松确定每个端口上配置了哪些服务——无论它们是在标准端口还是非标准端口上。

`Nmap` 同样执行应用映射，使用 `-sV` 和 `-O` 选项探测开放端口，分别确定服务和操作系统信息。

# 攻防 Linux：安全秘密与解决方案

`--version-intensity` 选项也可用于设置探测强度，级别 `0` 为轻量探测，级别 `9` 发送所有类型的端口。

```
nmap -P0 -sV -O --version-intensity 5 -p80,443,8080 192.168.1.11-20
```

然而，这并不允许攻击者看到 Web 服务器返回的所有标头。查看这些内容最详尽的方法是使用 `Netcat` 连接到 Web 服务器并发布 HTTP 请求：

```
nc localhost 80

HEAD / HTTP/1.0

Host: localhost
```

```
HTTP/1.0 200 OK
Date: Sun, 12 Aug 2007 00:46:39 GMT
Server: Apache/1.3.31 (Unix)
Content-Location: index.html
Variant: accept-language,accept-charset
TCN: choice
Last-Modified: Fri, 04 May 2001 00:00:38 GMT

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.0 Transitional//EN">
<html xmlns="http://www.w3.org/TR/html1/html1-transitional.dtd">
<head>
<title>Test Page for Apache Installation</title>
</head>
<body
Background white, links blue (unvisited), navy (visited), red
</body>
</html>
```

查看这些内容最详尽的方法是使用 `Netcat` 连接到 Web 服务器并发布 HTTP 请求：

```
nc localhost 443

HEAD / HTTP/1.1

Host: localhost
```

```
HTTP/1.1 200 OK
Date: Sun, 12 Aug 2007 00:46:39 GMT
Server: Apache/1.3.31 (Unix)
Content-Location: index.html
Variant: accept-language,accept-charset
TCN: choice
Last-Modified: Fri, 04 May 2001 00:00:38 GMT

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.0 Transitional//EN">
<html xmlns="http://www.w3.org/TR/html1/html1-transitional.dtd">
<head>
<title>Test Page for Apache Installation</title>
</head>
<body
Background white, links blue (unvisited), navy (visited), red
</body>
</html>
```

查看这些内容最详尽的方法是使用 `Netcat` 连接到 Web 服务器并发布 HTTP 请求：

```
nc localhost 80

HEAD / HTTP/1.0

Host: localhost
```

```
HTTP/1.0 200 OK
Date: Sun, 12 Aug 2007 00:46:39 GMT
Server: Apache/1.3.31 (Unix)
Content-Location: index.html
Variant: accept-language,accept-charset
TCN: choice
Last-Modified: Fri, 04 May 2001 00:00:38 GMT

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.0 Transitional//EN">
<html xmlns="http://www.w3.org/TR/html1/html1-transitional.dtd">
<head>
<title>Test Page for Apache Installation</title>
</head>
<body
Background white, links blue (unvisited), navy (visited), red
</body>
</html>
```

在攻击者连接到你的网络之前，他们可能已经建立了关于你组织、人员和内部系统的画像，这使得他们能够制定出更详细、更精确的攻击。这种攻击可能采取社会工程的形式：
- 社会工程
- 利用配置不当的 Web 服务器
- 使用收集到的身份凭据登录外部服务

# Hacking Exposed Linux：Linux 安全秘籍与解决方案

系统预测，这可能允许攻击者利用操作系统中的漏洞。然而，通过限制服务器响应的协议和端口，对操作系统的猜测准确性会大大降低，从而显著减少攻击的精度。

`IPTables` 还可以用于限制对更敏感服务的访问（例如 `SSH` 或 Web 界面），允许授权的 IP 地址连接到这些端口。这并不是万无一失的，因为攻击者可能伪造 IP 地址；但它确实降低了被攻击的吸引力。

例如，为了配置 `IPTables` 以允许来自来自 `80/TCP` 和 `443/TCP` 端口的连接，并限制仅允许管理 IP 地址访问 `22/TCP` 端口，你可以顺序运行以下所有命令。

首先，清除所有当前用于连接到 Web 服务器的 `IPTable` 规则：

```
iptables -F

iptables -X
```

然后设置 `IPTables` 使其具有默认拒绝的策略：

```
iptables -P INPUT DROP

iptables -P OUTPUT DROP

iptables -P FORWARD DROP
```

允许从任何地方到 Web 服务器 (`WEB_IP_ADDR`) 的 `80/TCP` 端口的 HTTP 请求：

```
iptables -A INPUT -p tcp -s 0/0 --sport 1024:65533 -d WEB_IP_ADDR \
-dport 80 -m state --state NEW, ESTABLISHED -j ACCEPT
```

允许来自 Web 服务器的 `80/TCP` 端口的 HTTP 响应：

```
iptables -A OUTPUT -p tcp -s WEB_IP_ADDR --sport 80 -d 0/0 \
-dport 1024:65533 -m state --state NEW, ESTABLISHED -j ACCEPT
```

允许从任何地方到 Web 服务器的 `443/TCP` 端口的 HTTPS 请求：

```
iptables -A INPUT -p tcp -s 0/0 --sport 1024:65533 -d WEB_IP_ADDR \
-dport 443 -m state --state NEW, ESTABLISHED -j ACCEPT
```

允许来自 Web 服务器的 `443/TCP` 端口的 HTTPS 响应：

```
iptables -A OUTPUT -p tcp -s WEB_IP_ADDR --sport 443 -d 0/0 \
-dport 1024:65533 -m state --state NEW, ESTABLISHED -j ACCEPT
```

允许从管理 IP 地址 (`MGT_IP_ADDR`) 到 Web 服务器的 `22/TCP` 端口的 SSH 连接：

```
iptables -A INPUT -p tcp -s MGT_IP_ADDR --sport 1024:65533 -d WEB_IP_ADDR \
-dport 22 -m state --state NEW, ESTABLISHED -j ACCEPT
```

## 仅允许 Web 服务器通过 22/TCP 端口向管理 IP 地址发送的 SSH 流量：

```
iptables -A OUTPUT -p tcp -s WEB_IP_ADDR --port 22 -d MGT_IP_ADDR \
--dport 1024:65535 -m state --state ESTABLISHED -j ACCEPT
```

最后，明确规定所有不符合上述标准的流量都被丢弃。

```
iptables -A INPUT -j DROP

iptables -A OUTPUT -j DROP
```

## 服务器标头 (Server Header)

管理员可以设置以下 `Apache` 配置指令，以限制从 Web 服务器 HTTP 头部泄出的敏感信息：

```
ServerTokens ProductOnly
```

这将阻止 Web 服务器在 HTTP 服务器头部中泄露操作系统类型、安装的模块以及所有版本信息。遗憾的是，Web 服务器仍然会泄露它是一个 `Apache` 服务器。

## ModSecurity

`ModSecurity` 是一个 `Apache` 模块，作为嵌入在 Web 服务器中的 `IDS/IPS`。由于它是 Web 服务器的一部分，`ModSecurity` 能够在服务器解密或解压缩之后分析加密的 HTTPS 流量或压缩内容。

`ModSecurity` 指令 `SecServerSignature` 可用于更改 HTTP 服务器头部，以减少信息泄露或包含虚假信息以误导攻击者。包含 `mod_security` 模块的 `Apache` Web 服务器可以配置以下指令：

```
SecServerSignature "Microsoft-IIS/5.0."
```
