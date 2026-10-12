
WINS 是 RFC1001/1002 NetBIOS 名称服务（NBNS）的 Microsoft 实现。它允许 NetBIOS 客户端（如 Microsoft Windows 机器）将其选择的任意机器名称与机器被分配的 IP 地址一起注册。通过使用 WINS，网络客户端机器可以将机器名称解析为它们的 IP 地址。

对 NetBIOS 网络局限性的替代方案的需求最终促使 Microsoft 使用 DNS 和 Active Directory。Microsoft 的新实现试图以类似 WINS 用于 NetBIOS 网络的方式使用 DNS。WINS 和 Microsoft DNS 都依赖于动态名称注册。

Microsoft Windows 客户端可以在启动时向 DNS 服务器执行动态名称注册。或者，如果使用 DHCP 来分配工作站 IP 地址，则 DHCP 服务器可以在客户端确认 IP 地址租约时注册主机名及其 IP 地址。最后，Microsoft DNS 可以通过 Microsoft WINS 解析主机名。

以下配置演示了一个简单的、不安全的动态 DNS 服务器和一个与 DNS 配置相匹配的简单 DHCP 服务器。

## 46.2.1 动态 DNS

示例 DNS 配置是针对网络 `192.168.1.0/24` 的 IP 地址空间中的一个私有网络。私有类网络地址空间在 RFC1918 中规定。

假设该网络位于一个安全防火墙之后。以下文件适用于 ISC BIND 版本 9。BIND 是伯克利互联网名称守护程序。

主配置文件 `/etc/named.conf` 确定所有其他使用配置文件的位置和名称。该文件的位置和名称在操作系统的一部分中，通过启动脚本指定。

> <sup>1</sup>[Samba 邮件列表](https://lists.samba.org/smlang/)
> <sup>2</sup>[Samba IRC](http://www.samba.org/samba/irc.html)
> <sup>3</sup>[Samba 错误报告](https://bugzilla.samba.org/)
> <sup>4</sup>[Samba 支持页面](http://www.samba.org/samba/support.html)
> 
> 1. [ISC 网站](http://www.isc.org)
> 2. [O'Reilly DNS 出版物](http://www.oreilly.com/catalog/dns/index.htm)
> 3. [BIND9.NET 书籍信息](http://www.bind9.net/books-dhcp)

# Quenya.Org 配置文件

```
acl mynet {
    192.168.1.0/24;
    127.0.0.1;
};

options {
    directory "/var/named";
    listen-on-v6 { any; };
    notify no;
    forward first;
    forwarders {
        192.168.1.1;
    };
    auth-nxdomain yes;
    multiple-cnames yes;
    listen-on {
        mynet;
    };
};

# 以下三个区域定义无需任何修改。
# 第一个定义 localhost，第二个定义
# localhost 的反向查找。最后一个区域 "." 是
# 根名称服务器的定义。

zone "localhost" in {
    type master;
    file "localhost.zone";
};

zone "0.0.127.in-addr.arpa" in {
    type master;
    file "127.0.0.zone";
};

zone "." in {
    type hint;
    file "root.hint";
};

# 您可以在下方插入更多针对您自己域名的区域记录。
zone "quenya.org" {
    type master;
    file "/var/named/quenya.org.hosts";
    allow-query {
        mynet;
    };
    allow-transfer {
        mynet;
    };
    allow-update {
        mynet;
    };
};

zone "1.168.192.in-addr.arpa" {
    type master;
    file "/var/named/192.168.1.0.rev";
    allow-query {
        mynet;
    };
    allow-transfer {
        mynet;
    };
    allow-update {
        mynet;
    };
};
```

以下所有文件均位于目录 `/var/named` 中。这是 `/var/named/localhost.zone` 文件的内容：

```
$TTL 1w
@ IN SOA @ root (
    42      ; serial (d. adams)
    2D      ; refresh
    4H      ; retry
    6W      ; expiry
    1W      ; minimum
)
IN NS @
IN A 127.0.0.1
```

`/var/named/127.0.0.zone` 文件的内容：

```
$TTL 1w
@ IN SOA localhost. root.localhost. (
    42      ; serial (d. adams)
    2D      ; refresh
    4H      ; retry
    6W      ; expiry
    1W      ; minimum
)

IN NS           localhost.
IN PTR          localhost.
```

`/var/named/quenya.org.hosts` 文件的内容：

```
$ORIGIN .
$TTL 38400       ; 10 hours 40 minutes
quenya.org        IN SOA  marvel.quenya.org. root.quenya.org. (
                    2003021832  ; serial
                    10800       ; refresh (3 hours)
                    3600        ; retry (1 hour)
                    604800      ; expire (1 week)
                    38400       ; minimum (10 hours 40 minutes)
                )
        NS        marvel.quenya.org.
        MX    10  mail.quenya.org.

$ORIGIN quenya.org.
frodo             A     192.168.1.1
marvel            A     192.168.1.2
;
mail              CNAME marvel
www               CNAME marvel
```

`/var/named/192.168.1.0.rev` 文件的内容：

```
$ORIGIN .
$TTL 38400       ; 10 hours 40 minutes
1.168.192.in-addr.arpa IN SOA  marvel.quenya.org. root.quenya.org. (
                    2003021824  ; serial
                    10800       ; refresh (3 hours)
                    3600        ; retry (1 hour)
                    604800      ; expire (1 week)
                    38400       ; minimum (10 hours 40 minutes)
                )
        NS        marvel.quenya.org.

$ORIGIN 1.168.192.in-addr.arpa.
1       PTR     frodo.quenya.org.
2       PTR     marvel.quenya.org.
```
