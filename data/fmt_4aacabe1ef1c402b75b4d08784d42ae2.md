
DNS 配置可能复杂得多。为了正确配置 DNS，你应该理解一些概念。

## 关键术语

以下与 DNS 相关的重要术语：

- **主机 (Host)**：主机通常是指连接到网络上的计算机。
- **域名 (Domain name)**：域名对人类来说很难记忆，所以我们使用 IP 地址。
- **顶级域名 (Top-level domain)**：顶级域名有 `.com`, `.org`, `.net`, `.edu`, `.gov` 和 `.mil`。
- **FQDN**：完全限定域名是从顶层开始的域名。例如，`example.com`。
- **子域名 (Subdomain)**：子域名是较大域名的任何组成部分。例如，假设你想让你的组织拥有三个域名。你可能将这些命名为 `sales`、`eng` 和 `support`。如果你的公司是 `example.com`。
- **域名服务器 (Name server)**：域名服务器是响应 DNS 请求的服务器。域名服务器提供 IP 地址到域名的翻译（有时也相反）。服务器要么在本地存储此信息的副本（区域文件），要么存储从其他服务器获取的信息或将查询传递给其他。
- **权威域名服务器 (Authoritative name server)**：权威域名服务器是根据本地存储的信息（主记录）返回结果的服务器。
- **区域文件 (Zone file)**：用于存储 IP 地址到域名翻译信息的文件（也称为 DNS 记录）。此文件还包含用于定义域名本身的内容。
- **记录 (Record)**：在区域文件中，记录是定义区域单块信息的条目，例如翻译 IP 地址到域名的数据。
- **缓存服务器 (Caching server)**：缓存服务器是根据从另一个服务器（如权威域名服务器）获取的信息返回结果的结果。缓存服务器的主要优势是它可以加速 IP 地址到域名的解析，因为它可以缓存结果并使用缓存中的信息响应未来的请求。
- **TTL**：存储在缓存服务器中的数据通常不是永久的。提供数据的服务器还会为缓存服务器提供一个 TTL，即生存时间。缓存服务器会在内存中存储这些信息直到该 TTL 周期结束。通常这段时间为 24 小时，但取决于权威域名服务器中记录更新的频率。

# 第20章：基础 DNS 服务器配置

- **DNS 转发器（DNS forwarder）**——一种设计用于从互联网网络接收 DNS 查询并将查询发送到外部 DNS 服务器的 DNS 服务器。

- **正向查询（Forward lookup）**——将 IP 地址翻译为域名的过程。大多数 DNS 服务器提供此功能。

- **反向查询（Reverse lookup）**——将域名翻译为地址的过程。虽然许多 DNS 服务器提供此功能，但它没有正向查询常见。

- **BIND**——伯克利互联网域名系统（Berkeley Internet Name Domain）；互联网上广泛使用的 DNS 软件。该软件最初在加州大学伯尔克利分校开发。目前的 BIND 版本被称为 BIND 9。

- **dnsmasq**——一个可以作为 DNS 转发器的服务器。它也可以用作 DHCP（动态主机配置协议）服务器。它为较小的网络设计，以易于配置和管理系统资源开销低而闻名。

- **djbindns**——发布于2001年，该 DNS 服务器由 Daniel J. Bernstein 创建，是他他在应对 BIND 存在的多个安全漏洞时斗争的结果。它在某些发行版中更流行，特别是 Debian 和 Ubuntu，原始的 djbindns 项目在这些系统中分支出一个名为 dbndns 的项目。

- **PowerDNS**——PowerDNS 在1999年首次发布时是一个闭源项目。它最初的设计是为了提供一种名为*负载均衡*（load balancing）的功能，DNS 服务器提供不同的 IP 地址，将 URL 请求的负载分散到多个 Web 服务器之间。它于2003年作为开源发布。

> **注意：** LPIC-2 将测试你对 BIND 9 的细节。关于其他 DNS 服务器的考试目标是让你对这些服务器是什么有所认识。

# 名称解析的工作原理

以下示例特意简化处理，以让你对名称解析的工作原理有一个概念。许多因素可能会改变此过程的确切性质，包括示例中描述的每个 DNS 服务器的具体配置方式。

对于此示例，请考虑以下情况：你正在使用网络浏览器访问 `www.onecourses.com` 域名。为了确定该域名的 IP 地址，你的系统首先需要确定它可以查询哪些 DNS 服务器。需要查询 `/etc/network/resolv.conf` 文件来获取这些信息：

```
[root@localhost ~]# cat /etc/resolv.conf
nameserver 192.168.1.1
```

> 注意：在大多数情况下，最好至少有两个名称服务器设置。如果第一个名称服务器不可用，则由第二个进行回答。你会发现较小的公司只为自己的系统提供一个名称服务器。此外，如果你正在使用虚拟机，虚拟机管理器将作为虚拟机的唯一名称服务器。因此，如果你最终发现 `/etc/network/resolv.conf` 文件中只有一个名称服务器设置，请不要感到。

查询被发送到 IP 地址为 `192.168.1.1` 的名称服务器，这是你组织内部的 DNS 服务器。你可以此判断，因为该 IP 地址是私有 IP（在互联网上不可路由）。虽然此 DNS 服务器可能已经缓存了之前对 `www.onecourses.com` 的查询结果，但让我们假设本地 DNS 服务器没有这些信息。在这种情况下，DNS 服务器需要将请求传递给另一个 DNS 服务器。

虽然可以配置 DNS 服务器将请求传递给其他特定的 DNS 服务器，但在大多数情况下，查询会被传递给 DNS 域结构顶部的 DNS 服务器。这些服务器被称为根服务器（root servers）。共有 13 个根服务器；示例 20-1 显示了它们在 BIND 区域文件中描述的形式。

# 示例 20-1 根服务器

| ANSWER SECTION | IN | NS |
| :--- | :--- | :--- |
| | IN | NS | `a.root-servers.net` |
| | IN | NS | `b.root-servers.net` |
| | IN | NS | `c.root-servers.net` |
| | IN | NS | `d.root-servers.net` |
| | IN | NS | `e.root-servers.net` |
| | IN | NS | `f.root-servers.net` |
| | IN | NS | `g.root-servers.net` |
| | IN | NS | `h.root-servers.net` |
| | IN | NS | `i.root-servers.net` |
| | IN | NS | `j.root-servers.net` |
| | IN | NS | `k.root-servers.net` |
| | IN | NS | `l.root-servers.net` |
| | IN | NS | `m.root-servers.net` |

;; ADDITIONAL SECTION:

```
a.root-servers.net      3600000 IN      A       198.41.0.4
```
