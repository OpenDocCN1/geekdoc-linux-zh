
在 Options 子句中设置 `notify` 的值，或在 Zone 子句中设置它，这将覆盖给定区域的全局设置。其格式为：

```
notify YES | NO | EXPLICIT
```

YES 会调用主服务器通知该区域 NS 资源记录中列出的所有从服务器以及 also-notify 语句中列出的 IP 地址的服务器。当你将 `notify` 设置为 EXPLICIT 时，服务器将仅通知 also-notify 语句中列出的服务器。NO 则关闭通知功能。

如果你在主服务器上指定 `notify YES`，每当你更改区域中 SOA 记录的 serial 字段时，从服务器上的区域文件都会更新。你必须手动将更改分发到 /etc/bind/named.conf 及其包含的文件。

## 分拆视野服务器 (SPLIT HORIZON SERVER)

假设你想建立一个局域网（LAN），为内部系统的用户提供所有系统和服务（这些系统可能位于防火墙后），但仅向互联网（公共）用户提供某些公共服务——例如 Web、FTP 和邮件。分拆视域（也称为 DMZ）DNS 服务器通过区别对待来自内部系统的查询和来自公共系统（互联网上的系统）的查询来处理这种情况。

BIND 9 在 named.conf 中引入了 View（视图）子句。每个视图为一组客户端提供 DNS 命名空间的不同视角。当没有 View 子句时，named.conf 中指定的所有区域都是默认视图的一部分。

假设一个办公室的局域网内有几台系统，以及公共的 Web、FTP 和邮件服务器。连接到互联网的单一连接经过 NAT 处理（第 1161 页），因此由本地系统和服务器共享。直接连接到互联网的系统是路由器、防火墙和平。该场景利用了 named.conf 中的 View 子句，并为本地和公共用户支持了辅助 DNS 服务器。公共用户需要访问 DNS 服务器作为其所支持的域名的权威，但他们不需要 DNS 服务器支持递归查询。不为公共用户提供递归查询可以限制 DNS 服务器和互联网连接的负载。出于安全考虑，公共用户不得访问除服务器以外的本地系统信息。本地用户应该有权访问本地系统的信息，并能够递归地使用 DNS 映射器。

图 24-6 显示了服务器对来自局域网和互联网的查询会有不同的响应。

gufw（第 876 页）或 iptables 实用程序（第 880 页）控制内部和外部系统用户可以访问的端口。DNS 则控制哪些系统向哪些用户发布自己。

## 第 24 章 DNS/BIND：跟踪域名和地址

![](img/45ff4cd21497435daa35084a84b95d07_906_0.png)

图 24-6 分拆视域 DNS 服务器

named.conf 文件有四个子句：一个 Options 子句、两个 View 子句和一个 Logging 子句。Options 子句指定了位于 /etc/bind 目录下的区域文件。View 子句根据解析器的地址指定解析器所依赖的特性和区域。一个区域供局域网/本地用户使用；另一个供互联网/公共用户使用。Logging 子句设置了用于默认消息 misc2.log 文件。

有多种方法可以指定哪些客户端查看某个视图。以下 named.conf 文件使用了 match-clients 语句：

```
$ /etc/bind/named.conf
options
    directory "/etc/bind";
    //end options

```

```
view "local" IN {
    // start local view
match-clients { 127.0.0.1; 192.168.0.0/24};
    recursion YES;
```

```
zone "zach.net" IN {
    type master;
    file "local.net";
    notify YES;
```

```
zone "0.168.192.in-addr.arpa" IN {
    type master;
    file "named.local";
    notify YES;
```

```
zone "." IN {
    type hint;
    file "named.ca";
```

```
// end local view
```

```
view "public" IN {
match-clients { "all"; };
recursion NO;
```

```
zone "zach.net" IN {
type master;
file "public.net";
notify YES;
}
```

```
zone "0.168.192.in-addr.arpa" IN {
type master;
file "named.public";
notify YES;
}
```

```

 "." IN {
type hint;
file "named.ca";
}
```

```
logging{
channel "misc" {
file "/var/log/bind/misc2.log" versions 2 size 1m;
print-time YES;
print-severity YES;
print-category YES;
}
category default {
"misc";
}
}
```

named.conf 中 View 子句的顺序至关重要：呈现给客户端的视图是包含以下内容的第一个视图：按顺序，一个是给本地用户的，一个是公共用户的。named.conf 包含两个 View 子句：一个用于本地用户，一个用于公共用户。本地用户被定义为 192.168.0/24 子网或 localhost（127.0.0.1）上的用户；公共用户定义为任何用户。如果你反转了 View 子句的顺序，所有用户（包括本地用户）都将获得针对公共用户的视图。

（注：原文此处存在大量重复段落，已根据要求去重并翻译）

## 第 24 章 DNS/BIND：跟踪域名和地址

为了方便理解，View 子句与本地视图类似。recursion（递归）子句提供了源自本地用户的答案。named.conf 中 View 子句的顺序至关重要：呈现给客户端的视图是包含以下内容的第一个视图：按顺序，一个是给本地用户的，一个是公共用户的。named.conf 包含两个 View 子句：一个用于本地用户，一个用于公共用户。本地用户被定义为 192.168.0/24 子网或 localhost（127.0.0.1）上的用户；公共用户定义为任何用户。如果你反转了 View 子句的顺序，所有用户（包括本地用户）都将获得针对公共用户的视图。

## 设置不同类型的 DNS 服务器

zach.net 区域文件的公共版本如下：

```
$ cat public.net
; zach.net zone file
$TTL 3D
@ IN SOA ns.zach.net. mgs@sobell.com. (
      20101118 ; serial
      8H : refresh
      2H : retry
      4w : expire
      1D ) ; minimum
IN TXT "Sobell Associates."
IN NS ns ; 名称服务器地址（未限定域名）
IN NS ns.speedy.net.; 名称服务器地址（限定域名）
IN MX 10 mail; 邮件交换（主/未限定域名）
IN MX 20 mail.max.net.; 邮件交换（次/限定域名）
www CAME ns
ftp CAME ns
mail CAME ns
ns A 192.168.0.1
ns A 192.168.0.6
ns MX 10 mail
ns MX 20 mail.max.net.
```

这里有两个反向区域文件，每个文件从 SOA 和 NS 资源记录开始，随后是每个服务器名称的 PTR 记录。该文件的本地版本还列出了本地系统的名称：

```
$ cat named.local
";016.192.ind-addr.arpa" 反向区域文件
```

```
$TTL 3D
@ IN SOA ns.zach.net. mgs@sobell.com. (
      2010110501 ; serial
      8H : refresh
      2H : retry
      4w : expire
      1D ) ; minimum
IN NS ns.speedy.net.
IN NS ns.speedy.net.
1 IN PTR gw.zach.net.
1 IN PTR www.zach.net.
1 IN PTR ftp.zach.net.
1 IN PTR mail.zach.net.
1 IN PTR speedy.zach.net.
3 IN PTR grape.zach.net.
4 IN PTR potato.zach.net.
6 IN PTR peach.zach.net.
```
