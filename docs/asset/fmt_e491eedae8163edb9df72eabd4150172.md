
`awk` 的 `print` 命令会将输出的顺序颠倒过来，并在两者之间插入一个制表符（`\t`）。通过 `>>` 可以将输出重定向并追加到 `/etc/hosts` 中。

> **注意**
>
> 上述示例只能用于你拥有控制权的主机，或者你确信不会发生变化的主机。如果你不是 Caldera 的域管理员，却把 Caldera 的主机加入你的 `/etc/hosts` 文件中，那可不是个好主意。

## WHOIS 命令

本章要介绍的最后一个程序是 `whois`。虽然它不是 BIND 工具之一，但这个程序提供与 DNS 相关的信息。具体来说，它从 `internic.net` 数据库提供与域名注册相关的信息。建议你将查询指向合适的 `whois` 服务器。在撰写本书时，`whois` 服务器包括以下这些：

- `whois.internic.net`—国际互联网络信息中心（InterNIC）
- `whois.nic.gov`—美国政府 NIC
- `whois.nic.mil`—美国军事 NIC
- `whois.ripe.net`—RIPE 欧洲网络协调中心
- `whois.apnic.net`—亚太 NIC
- `whois.arin.net`—美国互联网号码注册局（ARIN）
- `whois.funet.fi`—芬兰 NIC
- `whois.nic.af`—阿富汗 NIC
- `whois.nic.as`—美属萨摩亚 NIC
- `whois.nic.br`—巴西 NIC
- `whois.nic.bt`—不丹 NIC
- `whois.nic.ch`—瑞士 NIC
- `whois.nic.cx`—圣诞岛 NIC
- `whois.nic.fr`—法国 NIC
- `whois.nic.hm`—赫德岛和麦克唐纳群岛 NIC
- `whois.nic.it`—意大利 NIC
- `whois.nic.li`—列支敦士登 NIC
- `whois.nic.lk`—斯里兰卡 NIC
- `whois.nic.mx`—墨西哥 NIC
- `whois.nic.nu`—纽埃岛 NIC
- `whois.nic.pw`—帕劳 NIC
- `whois.nic.sh`—圣赫勒拿岛 NIC
- `whois.nic.tj`—塔吉克斯坦 NIC
- `whois.nic.tm`—土库曼斯坦 NIC
- `whois.nic.uk`—英国 NIC
- `www.nic.at`—奥地利 NIC
- `whois.dns.pt`—葡萄牙 NIC
- `whois.nic-se.se`—瑞典 NIC
- `whois.nic.ad.jp`—日本 NIC
- `whois.aunic.net`—澳大利亚 NIC
- `domain-registry.nl`—荷兰 NIC
- `whois.jpl.nasa.gov`—美国国家航空航天局喷气推进实验室 NIC
- `whois.berkeley.edu`—加州大学伯克利分校 NIC

对 `caldera.com` 域执行 `whois` 查询会返回以下结果：

```
# whois -h whois.internic.net calderasystems.com

  Domain Name: CALDERASYSTEMS.COM

  Registrar: NETWORK SOLUTIONS, INC.

  Whois Server: whois.networksolutions.com

  Referral URL: www.networksolutions.com

  Name Server: NS2.CALDERA.COM

  Name Server: NS.CALDERASYSTEMS.COM

  Updated Date: 12-apr-1999

>>> Last update of whois database: Wed, 22 Mar 00 03:32:04 EST <<<
```

注册局数据库仅包含 `.COM`、`.NET`、`.ORG`、`.EDU` 域名和注册商。

## 故障排查

*当我以交互方式使用 `nslookup` 时，收到以下错误：*

```
Can't find server name for address 127.0.0.1: Non-existent host/domain
```

你的 DNS 服务器正在运行，但你还没有正确配置本机的反向查找文件。请记住，在反向文件中，引用 `127.0.0.1` 的那一行应该如下所示：

```
1.0.0.127.in-addr.arpa.        IN      PTR     localhost.
```

注意，IP 地址是倒过来写的。

*如何判断我是否在使用缓存域名服务器？*

首先，确保你的 `/etc/hosts` 文件中第一行域名服务器配置如下：

```
nameserver 127.0.0.1
```

然后，不带任何参数启动 `nslookup`。你的默认服务器应该是地址为 `127.0.0.1` 的 `localhost`。如果不是，说明你没有使用本地域名服务器。

*当我将 `nslookup` 与 `localhost` 一起使用时，收到以下错误：*

```
localhost can't find pancall.com: Non-existent host/domain
```
