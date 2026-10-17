
>>HEADER opcode: QUERY, status: NOERROR, id: 40803

>> flags: qr aa; QUERY: 1, ANSWER: 1, AUTHORITY: 4, ADDITIONAL: 4

:: www.redhat.com, type: ANY, class: IN

2h183s ns.redhat.com

2h183s ns2.redhat.com

2h183s ns3.redhat.com

2h183s speedy.redhat.com

1d2h8m A 207.175.42.153

1d2h8m A 207.165.229

1d2h8m A 206.132.41.213

2h183s A 199.183.42.251

其中 `<host>` 是要查询的主机名。

# host

`host` 程序使用命名服务器查询主机名：

- 使用 FQDN、域名、主机名或数字查询主机：

例如：

```
[root @ /] host-redhat.com
```

redhat.com 地址为 207.175.42.154。

其中 `<FQDN, 域名,主机名或数字>` 是 FQDN (`www.redhat.com`), 域名 (`redhat.com`), 主机名 (`www`) 或数字 (`207.175.42.154`)。

- 查找 DNS 维护的关于主机的所有信息：

例如：

```
[root @ /] host -a domain
```

code = 0 (Success), count=6

以下回答不是权威的:

以下回答未经服务器验证:

redhat.com 8112 NS ns.redhat.com

权威回答:

redhat.com 8112 NS ns.redhat.com

redhat.com 8112 NS ns3.redhat.com

redhat.com 8112 NS speedy.redhat.com

redhat.com 8112 A 207.175.42.154

redhat.com 1691 IN SOA ns.redhat.com/2001402 (version)

3600 refresh

1800 retry

60480 expiration

8600 minimum TTL

附加信息:

ns.redhat.com 94507 IN A 207.175.42.153

ns2.redhat.com 94507 IN A 208.165.229

ns3.redhat.com 94507 IN A 206.132.41.213

speedy.redhat.com 8112 IN A 199.183.42.251

这可以用于命名服务器查找关于 "redhat.com" 主机的所有信息。

- 列出完整域名，使用命令：

例如：

```
[root@deep /] host -l domain names
```

openma.com 命名服务器 openma.com

openma.com mail openma.com

localhost.openma.com 地址为 127.0.0.1

deep.openma.com 地址为 208.164.186.1

mail.openma.com 地址为 208.164.186.2

www.openma.com 地址为 208.164.186.3

此选项以官方主格式提供域名 "openma.com" 区域数据的完整下载。仅在绝对必要时才使用此命令。

# 安装文件

- `/etc/rc.d/init.named` > `/usr/lib/bind/include/hesiod.h`

- `/etc/rc.d/K45named` > `/usr/lib/bind/include/sys`

- `/etc/rc.d/rc1/K45named` > `/usr/lib/bind/include/net`

- `/etc/rc.d/rc2/K45named` > `/usr/lib/bind/lib`

- `/etc/rc.d/rc3/K45named` > `/usr/lib/bind/libbind.a`

- `/etc/rc.d/rc4/D45named` > `/usr/lib/bind/libbind.r_a`

- `/etc/rc.d/rc5/D45named` > `/usr/share/manroup/help`

- `/etc/rc.d/rc6/D45named` > `/usr/share/man1/dig.1`

- `/etc/named.conf` > `/usr/share/man1/host.1`

- `/usr/bin/addr` > `/usr/share/man1/dnsquery.1`

- `/usr/bin/named-book` > `/usr/share/man1/dnseck-keygen.1`

- `/usr/bin/dig` > `/usr/share/man3/bindhesiod.3`

- `/usr/bin/dnsquery` > `/usr/share/man3/gethostbyname.3`

- `/usr/bin/host` > `/usr/share/man3/inet_cidr.3`

# 服务器软件 (BIND/DNS 网络服务)

## 第 4 章

```
> /usr/lib/bind/include/arpa
> /usr/lib/bind/include/arpa
> /usr/lib/bind/include/inet.h
> /usr/lib/bind/include/arpa/nameser.h
> /usr/lib/bind/include/arpa/nameser_compat.h
> /usr/lib/bind/include/elastic.h
> /usr/lib/bind/include/sc/eventlib.h
> /usr/lib/bind/include/sc/misc.h
> /usr/lib/bind/include/sc/tree.h
> /usr/lib/bind/include/sc/logging.h
> /usr/lib/bind/include/sc/chmap.h
> /usr/lib/bind/include/memocluster.h
> /usr/lib/bind/include/sc/assertions.h
> /usr/lib/bind/include/sc/list.h
> /usr/lib/bind/include/secsec.h
> /usr/lib/bind/include/sc/marshall.h
> /usr/lib/bind/include/netdb.h
> /usr/lib/bind/include/resolv.h
> /usr/lib/bind/include/res_update.h
> /usr/lib/bind/include/irs.h
> /usr/lib/bind/include/irp.h
> /usr/share/man3/getaddrinfo.3
> /usr/share/man3/getgetodebyname.3
> /usr/share/man5/resolver.5
> /usr/share/man5/irs.conf.5
> /usr/share/man5/named.conf
> /usr/share/man7/hostname.7
> /usr/share/man7/mailaddr.7
> /usr/share/man8/ndc.8
> /usr/share/man8/named-xfer.8
> /usr/share/man8/named-bootconf.8
> /usr/share/man8/nslookup.8
> /usr/share/man8/nsupdate.8
> /usr/sbin/named
> /usr/sbin/named-xfer
> /usr/sbin/irpd
> /usr/sbin/dnskeygen
> /usr/sbin/named-bootconf
> /var/named
```

# 第 15 章 服务器软件 (邮件网络服务)

在本章中

- Linux Sendmail 服务器

    - 配置

    - 加固 Sendmail 安全

    - Sendmail 管理工具

    - Sendmail 用户工具

- Linux Imap & Pop 服务器

    - 配置

    - 加固 IMAP/POP 安全

## Linux Sendmail 服务器

### 概述

`Sendmail` 程序是世界上使用最广泛的互联网邮件传输代理 (`MTA`) 之一。`MTA` 的作用是将邮件从一台机器发送到另一台机器，仅此而已。`Sendmail` 并不是你用来读取电子邮件的客户端程序。相反，它将你的邮件通过互联网传输到你想让去的地方。过去，`Sendmail` 一直是系统黑客利用的容易，但随着 `Sendmail` 8 版本的出现，它已经变得困难得多。

在我们的配置和安装中，我们将为你提供两种不同的 `Sendmail` 配置方案：一种用于中央邮件中枢中继 (`Central Mail Hub Relay`)，另一种用于本地或邻近客户端和服务器。
