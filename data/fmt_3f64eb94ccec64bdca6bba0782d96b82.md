
防止攻击者从你的系统中主动枚举信息，直接要求系统仅允许最少的访问权限，并为服务的正确运行提供最少必要的信息。这包括通过防火墙限制攻击者可见的服务，以及配置主机配置以防止信息泄露（例如通过 HTTP 响应头获取的信泄露）。

## 基于主机的防火墙/数据包过滤器

大多数组织在网络边界处至少设置了一个防火墙；然而，它们对系统的安全保护还不够充分，不足以抵御直接攻击，这导致源自内部网络的攻击可以利用未对 Internet 开放的漏洞服务，或者允许渗透边界防火墙的攻击者轻易地在内部网络中穿行。

一种流行的防火墙（或数据包过滤器）是 Linux 发行版自带的 `IPTables`。此防火墙允许管理员过滤掉所有非生产的协议和端口（无论是开启还是关闭的），阻止端口扫描器枚举运行在服务器上的所有服务。某些端口扫描器（如 `Nmap`）还可以进行系统推测，可能允许攻击者利用操作系统的漏洞。然而，通过限制服务器响应的协议和端口，这些对操作系统的猜测准确性会大大降低，从而显著减少攻击的精确性。

`IPTables` 还可以用于限制对更敏感服务的访问，例如 `SSH` 或 Web 管理界面，仅允许授权的 IP 地址连接到这些端口。这种方法并不是万无一失的，因为攻击者可能伪造 IP 地址；但它确实让目标变得不那么具有吸引力。

例如，为了配置 `IPTables` 仅允许来自 Internet 的 `80/TCP` 和 `443/TCP` 端口的连接，并限制仅管理 IP 地址访问 `22/TCP` 端口，你可以顺序运行以下所有命令。

首先，清除 Web 服务器上当前生效的所有 IPTable 规则：

```
iptables -F
iptables -X
```

然后设置 `IPTables` 使其具有默认拒绝（deny）过滤策略：

```
iptables -p INPUT DROP
iptables -p OUTPUT DROP
iptables -p FORWARD DROP
```

允许从任何地方到 Web 服务器（`WEB_IP_ADDR`）的 `80/TCP` 端口的 HTTP 请求：

```
iptables -A INPUT -p tcp -s 0/0 --sport 1024:65535 -d WEB_IP_ADDR \
--dport 80 -m state --state NEW, ESTABLISHED -j ACCEPT
```

允许从 Web 服务器 `80/TCP` 端口到任何地方的 HTTP 请求：

```
iptables -A OUTPUT -p tcp -s WEB_IP_ADDR --sport 80 -d 0/0 \
--dport 1024:65535 -m state --state ESTABLISHED -j ACCEPT
```

允许到 Web 服务器 `443/TCP` 端口的 HTTPS 请求：

```
iptables -A INPUT -p tcp -s 0/0 --sport 1024:65535 -d WEB_IP_ADDR \
--dport 443 -m state --state NEW, ESTABLISHED -j ACCEPT
```

允许从 Web 服务器 `443/TCP` 端口到任何地方的 HTTPS 请求：

```
iptables -A OUTPUT -p tcp -s WEB_IP_ADDR --sport 443 -d 0/0 \
--dport 1024:65535 -m state --state ESTABLISHED -j ACCEPT
```

仅允许从管理 IP 地址（`MGT_IP_ADDR`）到 Web 服务器 `22/TCP` 端口的 SSH 连接：

```
iptables -A INPUT -p tcp -s MGT_IP_ADDR -d WEB_IP_ADDR \
--dport 22 -m state --state NEW, ESTABLISHED -j ACCEPT
```

允许从管理 IP 地址到 Web 服务器 `22/TCP` 端口的 SSH 流量：

```
iptables -A OUTPUT -p tcp -s WEB_IP_ADDR --sport 22 -d 0/0 \
--dport 1024:65535 -m state --state ESTABLISHED -j ACCEPT
```

注：此处原文逻辑有一处小误（ESTABLISHED -j ACCEPT）

```
iptables -A OUTPUT -p tcp -s MGT_IP_ADDR --sport 22 -d 0/0 \
--dport 1024:65535 -m state --state ESTABLISHED -j ACCEPT
```

最后，由于配置错误，确保所有流量都不被泄露：

```
iptables -A INPUT DROP
iptables -A OUTPUT DROP
```

## 服务器头部

管理员可以通过设置以下 Apache 配置来限制信息泄露：

```
ServerTokens Prod
```

`Server` 头部即使不能阻止攻击者探测 Web 服务器的类型和版本，但可以防止 Web 服务器泄露已安装模块。

## ModSecurity

`ModSecurity` 是一个充当 IDS/IPS 的模块，它可以分析加密的流量。由于它是 Web 服务器的一部分，`ModSecurity` 能够通过 HTTP 头部分析攻击内容。为了防止向攻击者泄露敏感信息，`ModSecurity` 可以配置：

```
ServerSignature "Microsoft-IIS/5.0"
```

值得注意的是，404 错误消息通常无法阻止攻击者发现 Web 服务器的类型和版本。如图 13-3 所示，默认错误消息会泄露 Web 服务器的配置。

## 访问控制利用

随着 Web 应用程序的复杂性和价值增加，确保系统机密性、完整性和可用性的安全要求也随之增加。由于缺乏时间、资源、技能或管理员和开发人员的安全意识，这些安全控制往往执行不当。

许多漏洞可以通过使用 Web 应用程序扫描器（如 `Paros` 和 `Nikto`，以及某种程度的 `Nessus`）被发现。

## 错误的错误处理

如果攻击者能够强制 Web 应用程序产生错误，错误消息通常包含有关底层操作系统、Web 服务器、数据库或应用程序的信息。这些信息随后可以用于直接攻击系统，或者允许其他攻击更精确地引导。

| | |
|---|---|
| 流行度 | 8 |
| 简单性 | 5 |
| 影响 | 4 |
| 风险评分 | 6 |

完整的文件路径通常通过应用程序服务（如 `Tomcat`）产生的错误消息进行枚举，如下：

```
-- java.FileNotFoundException: /var/www/hosts/site1/httpdocs/html/ config.xml (No such file or directory)
```

攻击者确切知道了 Web 服务器的文件系统结构，从而执行更精确的目录遍历攻击。文件系统本身还揭示了底层操作系统是一个 *NIX 系统。Web 服务器似乎还托管了虚拟网站，可能允许攻击者对不安全的第三方网站发起攻击，从而破坏系统并最终影响你的 Web 应用程序。

## 第 13 章：Web 应用攻击

### 377

![](img/09ab7f3aec00ce704a89a1cee1c6cf6a_412_0.png)

### 未找到 (Not Found)

服务器上未找到的 URL `/nonexistent.php`。

`Apache/2.0.55 (Debian) mod python/3.2.10 Python/2.4.4c PHP/4.4.2-1.1 mod_perl/2.0.2 Perl/5.8.8 Server at 192.168.0.167 Port 80`

完成

图 13-3 默认 Apache 错误信息显示了服务器类型和版本。

数据库（如 `MySQL`）作为 Web 应用的后端存储机制非常常见。如果 Web 应用和数据库的实现不安全，可能会暴露数据库错误信息。这些数据库错误可能包含与 Web 应用向后端数据库执行的 SQL 查询相关的信息，如果你足够幸运，你甚至可以获取整个 SQL 查询字符串。

当攻击者尝试开发 SQL 注入攻击时，这些数据库错误信息非常有帮助，因为攻击失败的原因通常会在错误中指定，这使得确定所需的精确语法变得容易得多。在章节后后的“数据验证不足”部分可以对 SQL 注入攻击进行更全面的查看。

Web 应用产生的错误通常更具离散性，但仍可能允许攻击者枚举数据库内的信息，这可能是通过暴力破解攻击实现的。。开发者犯的一个常见错误是为错误的用户名和错误的密码生成不同的错误信息：

```
Error: Username is invalid.
Error: Password is incorrect.
```

如果攻击者尝试使用无效的用户名和密码登录并收到显示用户名错误的错误，那么攻击者就知道数据库中不存在该用户名。如果返回的错误显示密码错误，那么攻击者就可以假设用户名是正确的，但密码错了。

Hacking Exposed Linux: Linux Security Secrets & Solutions
