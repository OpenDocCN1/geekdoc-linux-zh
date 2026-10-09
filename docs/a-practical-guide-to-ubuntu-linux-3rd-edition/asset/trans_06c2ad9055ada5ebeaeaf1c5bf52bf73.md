
在 Options 子句或 Zone 子句中设置 **notify** 的值，它会覆盖给定区域的全局设置。其格式为

```
notify YES | NO | EXPLICIT
```

设置为 **YES** 时，主服务器将向该区域 NS 资源记录中列出的所有从服务器以及 **also-notify** 语句中列出的 IP 地址处的服务器发送通知。当你将 **notify** 设置为 **EXPLICIT** 时，服务器仅向 **also-notify** 语句中列出的服务器发送通知。**NO** 会关闭通知功能。

如果在主服务器上指定 **notify** 为 **YES**，则每次你更改区域中 SOA 资源记录的序列号字段时，从服务器上的区域文件都会更新。你必须手动将更改分发到 */etc/bind/named.conf* 以及包含的文件中。

## 分割视图 DNS 服务器

假设你想设置一个局域网（LAN），该网络向内部系统上的本地用户提供其所有系统和 服务，这些内部系统可能位于防火墙之后，但仅向互联网（公共）用户提供某些公共服务——例如 Web、FTP 和电子邮件。*分割视图*（也称为 *DMZ*）DNS 服务器通过区分来自内部系统的查询和来自公共系统（互联网上的系统）的查询来处理这种情况。

### 视图子句

BIND 9 在 *named.conf* 中引入了视图（View）子句。视图子句便于实施分割 DNS 服务器。每个视图向一组客户端提供 DNS 命名空间的不同视角。如果没有视图子句，*named.conf* 中指定的所有区域都是隐含的默认视图的一部分。

假设办公室在一个局域网上有几个系统，以及公共 Web、FTP、DNS 和邮件服务器。到互联网的单一连接经过了 NAT（第 1161 页），因此由本地系统和服务器共享。直接连接到互联网的系统是一个路由器、防火墙和服务器。此场景利用了 *named.conf* 中的视图子句，并支持为本地用户和公共用户提供独立的辅助名称服务器。虽然公共用户需要访问 DNS 服务器作为支持服务器的域的权威，但他们不需要 DNS 服务器支持递归查询。不为公共用户支持递归可以限制 DNS 服务器和互联网连接的负载。出于安全原因，除服务器外，公共用户不得访问有关本地系统的信息。本地用户应能够访问有关本地系统的信息，并且应能够递归地使用 DNS 服务器。

图 24-6（下一页）显示服务器对来自局域网和互联网的查询做出不同的响应。

![](img/2344fc4a798f29dca9e8b5ed7288171a_906_0.png)

*gufw*（第 876 页）或 *iptables* 实用程序（第 880 页）控制内部和外部系统上的用户可以访问哪些系统中的哪些端口。DNS 控制向哪些用户通告哪些系统。

named.conf 文件有四个子句：一个 Options 子句、两个 View 子句和一个 Logging 子句。Options 子句指定区域文件位于 /etc/bind 目录中。View 子句指定解析器被允许访问的特性和区域，这取决于解析器的地址。一个区域供局域网/本地用户使用；另一个区域供互联网/公共用户使用。Logging 子句为默认消息设置 misc2.log 文件。

指定哪些客户端看到某个视图有几种方法。下面的 named.conf 文件使用 match-clients 语句：

```
$ cat /etc/bind/named.conf
Options {
directory "/etc/bind";
}; //end options

view "local" IN {			// start local view
match-clients { 127.0.0.1; 192.168.0.0/24};
recursion YES;

zone "zach.net" IN {
type		master;
file	"local.net";
notify YES;
};

zone "0.168.192.in-addr.arpa" IN {
type		master;
file	"named.local";
notify YES;
};

zone "." IN {
type	hint;
file	"named.ca";
};

};			// end local view

view "public" IN { // start public view
  match-clients { "all";};
  recursion NO;

  zone "zach.net" IN {
    type master;
    file    "public.net";
    notify YES;
  };

  zone "0.168.192.in-addr.arpa" IN {
    type master;
    file    "named.public";
    notify YES;
  };

  zone "." IN {
    type hint;
    file    "named.ca";
  };
}; // end public view

logging{
  channel "misc" {
    file "/var/log/bind/misc2.log" versions 2 size 1m;
    print-time YES;
    print-severity YES;
    print-category YES;
  };
  category default {
    "misc";
  };
}; //end logging
```

named.conf 中 View 子句的顺序至关重要，因为呈现给客户端的视图是客户端匹配的第一个视图。前面的 named.conf 文件包含两个 View 子句：一个供本地用户使用，另一个供公共用户使用，按此顺序排列。本地用户定义为 192.168.0.0/24 子网或本地主机（127.0.0.1）上的用户；公共用户定义为任何用户。如果你颠倒了 View 子句的顺序，所有用户——包括本地用户——都会获得为公共用户设计的视图，而没有用户会看到本地视图。

Options 子句中的许多语句可以在 View 子句中使用，在那里它们会覆盖（全局）Options 子句中的语句。**recursion** 语句可以在 Options 子句中出现，它出现在每个 View 子句中。此 named.conf 文件设置了一个服务器，该服务器为源自本地的查询提供递归答案，并为公共查询提供迭代答案。这种设置可以为本地用户提供快速、完整的答案，限制分配给其他用户的网络和处理器带宽，同时继续为本地服务器提供权威名称服务。

# 858 第 24 章 DNS/BIND：跟踪域名和地址

为了使 named.conf 更易于理解和维护，不同 View 子句中的区域可以具有相同的名称但不同的区域文件。示例中本地和公共 View 子句都具有区域名称 zach.net。公共的 zach.net 区域文件名为 public.net，本地的名为 local.net。

Logging 子句在第 852 页中进行了描述。

定义 zach.net 的区域文件与之前示例中的类似；公共文件是本地文件的一个子集。在两个文件中，SOA 资源记录后面是一个 TXT、两个 NS 和两个 MX 资源记录。接下来是三个 CNAME 资源记录，将指向 www.zach.net、ftp.zach.net 和 mail.zach.net 的查询引导到名为 ns.zach.net 的系统。接下来的四个资源记录指定 ns.zach.net 域的两个名称服务器地址和两个邮件服务器。

最后四个资源记录出现在本地的 zach.net 区域文件中，而未出现在公共区域文件中；它们是本地系统的地址（A）资源记录。与其将此类信息保存在每个系统的 /etc/hosts 文件中，你可以将其保存在 DNS 服务器上，在那里可以轻松更新。当你使用 DNS 而不是 /etc/hosts 时，必须相应地更改 /etc/nsswitch.conf（第 475 页）中的 hosts 行。

```
$ cat local.net
; zach.net local zone file

; TTL class record
@ IN SOA ns.zach.net. mgs@sobell.com. (
    20101118 ; serial
    8H ; refresh
    2H ; retry
    4W ; expire
    1D ) ; minimum

 IN TXT "Sobell Associates Inc."
 IN NS ; Nameserver address (unqualified)
 IN NS ns.speedy.net.; Nameserver address (qualified)
 IN MX 10 mail ; Mail exchange (primary/unqualified)
 IN MX 20 mail.max.net.; Mail exchange (2nd/qualified)

www IN CNAME ns
ftp IN CNAME ns
mail IN CNAME ns

ns IN A 192.168.0.1
 IN A 192.168.0.6
 IN MX 10 mail
 IN MX 20 mail.max.net.

speedy IN A 192.168.0.1
grape IN A 192.168.0.3
potato IN A 192.168.0.4
peach IN A 192.168.0.6
```

`zach.net` 区域文件的公共版本如下：

```
$ cat public.net
: zach.net public zone file

$TTL	3D
@	IN	SOA	ns.zach.net. mgs@sobell.com. (
			20101118	; serial
			8H		; refresh
			2H		; retry
			4W		; expire
			1D )	; minimum

IN	TXT	"Sobell Associates Inc."
IN	NS	ns		; Nameserver address (unqualified)
IN	NS	ns.speedy.net.; Nameserver address (qualified)

IN	MX	10 mail. ; Mail exchange (primary/unqualified)
IN	MX	20 mail.max.net. ; Mail exchange (2nd/qualified)

www	IN	CNAME	ns
ftp	IN	CNAME	ns
mail	IN	CNAME	ns

ns	IN	A	192.168.0.1
	IN	A	192.168.0.6
	IN	MX	10 mail
	IN	MX	20 mail.max.net.
```

这里有两个反向区域文件，每个文件都以 SOA 和 NS 资源记录开头，接着是每个服务器名称的 PTR 资源记录。此文件的本地版本还列出了本地系统的名称：

```
$ cat named.local
; "0.168.192.in-addr.arpa" reverse zone file

$TTL	3D
@	IN	SOA	ns.zach.net. mgs@sobell.com. (
			2010110501	; serial
			8H		; refresh
			2H		; retry
			4W		; expire
			1D )	; minimum

IN	NS	ns.zach.net.
IN	NS	ns.speedy.net.
1	IN	PTR	www.zach.net.
1	IN	PTR	www.zach.net.
1	IN	PTR	ftp.zach.net.
1	IN	PTR	mail.zach.net.
1	IN	PTR	speedy.zach.net.
3	IN	PTR	grape.zach.net.
4	IN	PTR	potato.zach.net.
6	IN	PTR	peach.zach.net.
```
