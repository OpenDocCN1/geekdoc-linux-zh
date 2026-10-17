
195.69.212.200.in-addr.arpa address = 195.69.213.15

## whois

`whois` 是来自 `whois` 软件包的命令行工具，用于查询互联网上的各种 `whois` 服务器。对于 IP 查询：

```
$ whois 165.93.0.83
```

OrgName: Cable & Wireless

OrgID: CWUS

Address: 3300 Regency Pkwy

City: Cary

State: NC

PostalCode: 27511

Country: US

NetRange: 165.93.0.0 - 165.93.255.255

CIDR: 165.93.0.0/16

NetName: CWDI-BLK

NetHandle: NET-165.93.0-1

Parent: NET-165.0-0

NetType: Direct Allocation

NameServer: NS.DIGISLE.NET

NameServer: NS1.DIGISLE.NET

Comment:

RegDate: 2002-08-23

TechHandle: ZC221-ARIN

TechName: Cable & Wireless

TechPhone: +1-919-465-4023

TechEmail: ip@gnoc.cw.net

OrgAbuseHandle: SPAM-ARIN

OrgAbuseName: SPAM COMPLAINTS

OrgAbusePhone: +1-800-977-4662

OrgAbuseEmail: abuse@cw.com

OrgNCHHandle: NOC99-ARIN

OrgNOCName: Network Operations Center

OrgNOCPhone: +1-800-977-4662

OrgNOCEmail: trouble@cw.net

OrgTechHandle: UIAA-ARIN

OrgTechName: US IP Address

OrgTechPhone: +1-800-977-4662

OrgTechEmail: ipadmin@clp.cw.net

OrgTechHandle: GIAA-ARIN

OrgTechName: Global IP Address Administration

OrgTechPhone: +1-919-465-4096

OrgTechEmail: ip@gnoc.cw.net

## 配置本地缓存名称服务器

缓存名称服务器构建已解析域名的本地缓存并提供给局域网内的其他用户。这加速了 DNS 查询并通过重用频繁访问域名的查询来节省带宽，在慢速拨号连接上特别有用。

如果你在计算机上安装了 `BIND` `Bind-utils`，可以通过安装 `caching-nameserver` 来配置缓存名称服务器。这会设置 `/etc/named.conf` 文件、`/var/named` 目录以及 `/var/named` 中的配置文件（`localhost.zone`, `named.local`）。要启动名称服务器，你可以手动启动它（见第 11 章“自动化任务”）或使用 `system-config-services` GUI。在 Settings 菜单中选择 Servers，选择 `named` 并点击 Start 按钮。

要让你的本地计算机使用缓存名称服务器，请重新配置 `/etc/resolv.conf` 文件，注释掉对 ISP 名称服务器的所有引用，并将唯一的名称服务器设置为本地主机（`127.0.0.1`）。名称服务器的 `/etc/resolv.conf` 为：

```
#etc/resolv.conf
nameserver 83.64.1.10
nameserver 83.64.0.10
nameserver 127.0.0.1
```

你网络上的其他机器应该在它们的 `/etc/resolv.conf` 文件中有本地名称服务器的 IP。假设运行名称服务器的计算机 IP 地址为 `192.168.1.5`，其他机器上的 `/etc/resolv.conf` 文件应该是：

```
#etc/resolv.conf
nameserver 83.64.1.10
nameserver 83.64.0.10
nameserver 192.168.1.5
```

## 配置本地缓存名称服务器

缓存名称服务器构建已解析域名的本地缓存并提供给局域网内的其他用户。这加速了 DNS 查询并通过重用频繁访问域名的查询来节省带宽，在慢速拨号连接上特别有用。

如果你在计算机上安装了 `BIND` `Bind-utils`，可以通过安装 `caching-nameserver` 来配置缓存名称服务器。这会设置 `/etc/named.conf` 文件、`/var/named` 目录以及 `/var/named` 中的配置文件（`localhost.zone`, `named.local`）。要启动名称服务器，你可以手动启动它（见第 11 章“自动化任务”）或使用 `system-config-services` GUI。在 Settings 菜单中选择 Servers，选择 `named` 并点击 Start 按钮。

要让你的本地计算机使用缓存名称服务器，请重新配置 `/etc/resolv.conf` 文件，注释掉对你 ISP 名称服务器的所有引用，并将唯一的名称服务器设置为本地主机（`127.0.0.1`）。名称服务器的 `/etc/resolv.conf` 为：

```
#etc/resolv.conf
nameserver 83.64.1.10
nameserver 83.64.0.10
nameserver 127.0.0.1
```

你网络上的其他机器应该在它们的 `/etc/resolv.conf` 文件中有本地名称服务器的 IP。假设运行名称服务器的计算机 IP 地址为 `192.168.1.5`，其他机器上的 `/etc/resolv.conf` 文件应该是：

```
#etc/resolv.conf
nameserver 83.64.1.10
nameserver 83.64.0.10
nameserver 192.168.1.5
```

## 使用缓存名称服务器拦截广告

设置缓存名称服务器的另一个优势是，你可以通过 DNS 区域拦截特定域名来拦截广告和不良网站。你通过覆盖你想拦截网站的 DNS 查询来实现。配置非常。首先，确定你想拦截的网站。例如，你可能想拦截所有广告 `doubleclick.net`。在 `/etc/named.conf` 中创建一个条目：`zone "doubleclick.net" { type master; file "fakes"; };`

然后创建一个新的 `/var/named/fakes` 文件。其内容应包含：

```
$TTL 1D
@ IN SOA dns.companyname.com. hostmaster.companyname.com. (200480817 1B 2H 4W 1D)

@ IN NS dns.companyname.example.com.
@ IN A 127.0.0.1
* IN A 127.0.0.1
```

## 第 23 章 管理 DNS

其中 `dns.companyname.com` 应该替换为缓存名称服务器的主机名。这将所有对 `doubleclick.net` 的 DNS 查询指向 `127.0.0.1`，在那里将无法找到记录。要使更改生效，你必须重启 `named` 以读取新的配置信息。第 11 章描述了重启 `named` 服务的几种方法；这里是其中一种：

```
# -HUP 'pidof named'
```

当 `named` 重启后，解析所有 `doubleclick.net` 地址的尝试将失败，广告将不会加载或显示，你的浏览体验将变得更快。

## 你自己的域名和第三方 DNS

你可以拥有自己的域名并为它提供第三方 DNS 服务，这意味着你不需要为自己配置和管理 DNS 名字服务器。你甚至可以在没有邮件服务器的情况下为你的域名设置一个电子邮箱地址。

以下是为你的域名提供第三方 DNS 服务涉及的主要任务总结：

- `注册并支付唯一域名`——公司现在提供这些域名的注册服务，因此请多加比较寻找最合理的价格，在使用前对该公司进行一些 Google 背景调查。
- `使用第三方 DNS 提供商提供 DNS 服务`——一个流行的提供商是 ZoneEdit，它提供了使用该服务的详细步骤。ZoneEdit 还提供邮件转发服务，因此发往 `you@your.domain` 的邮件将会被转发到你的 ISP 邮件账户。ZoneEdit 还允许你使用动态 DNS（Dynamic DNS），使你能够在动态分配的 IP（来自电缆或拨号上网提供商）上运行服务器，但仍然拥有你定位的 DNS 服务器。ZoneEdit 还可以为你提供一个启动网页，或将请求转发到已经建立的具有长地址的页面。
- `返回你的域名注册处并告诉它哪些名称服务器是你域名的权威服务器。`

在你完成上述任务后，信息大约需要三天时间传播到整个互联网。

## 使用 BIND 为真实域名提供 DNS
