
你可以使用 `allow-query` 语句（语法与之前描述的 `allow-recursion` 类似）选择更严格的限制，仅允许选定的主机查询你的名称服务器。当然，如果你的服务器是某个区域的权威服务器，此解决方案将不起作用。在这种情况下，你必须在每个希望提供权威数据的区域的配置部分中显式允许 `allow-query { all; }`。

## 控制区域传输 (Zone Transfers)

你还可以通过查询仅允许已的从服务器从你的服务器执行区域传输。区域传输不仅消耗大量资源（每次都需要 fork 出一个 `named-xfer` 进程）并提供了拒绝服务攻击的途径，还通过 `named-xfer` 中的缓冲区溢出存在远程利用漏洞，允许攻击者在受侵害的系统中获得 root 权限。为了防止这一点，请在所有的区域定义中添加如下部分：

```
zone "example.com" {

...

  allow-transfer {

    192.0.2.96; // 已知的从服务器。

    localhost; // 测试时通常需要。

  }

};
```

## 向潜在问题主机发出告警

尽管如此，可能有必要对少数几个麻烦的主机进行特殊处理。`named.conf` 中的 `server` 和 `black hole` 语句可用于告知 `named` 已知的投毒信息源或攻击尝试。例如，如果主机 203.154.1 重复尝试攻击服务器，在 `named.conf` 的 `options` 部分添加以下内容将导致你的服务器忽略来自该地址的流量。当然，你可以在 `black hole` 列表中指定多个地址和网络。

```
options {

...

  blackhole { 203.122.154.1; };

};
```

对于已知的错误数据源，你可以执行如下操作，让名称服务器直接停止查询它。标记为 `bogus` 的服务器将不会发送查询。

```
server bogus.info.com { bogus yes; };
```

AUS-CERT 告警 AL-1999.004 讨论了针对 DNS 服务器的拒绝服务攻击，还讨论了限制访问名称服务器各种方法，非常建议阅读。副本位于 ftp://ftp.auscert.org/pub/auscert/_advisory/AL-1999.004.dns_dos。除外，它建议采用最严格的配置，并对已知伪造请求的地址在服务器中添加以下 ACL：

```
/* 这些是已知的伪造地址。 */acl 'bogon' { 0.0.0.0/8; # 空地址

1.0.0.0/8; # IANA 注册的常用伪地址

2.0.0.0/8; # 测试地址

192.0.2.0/24; # 测试地址
```

```
/* RFC 1918 地址也可能是伪造的。如果你内部使用它们，请不要列出。 */10.0.0.0/8; 172.16.0.0/12; 192.168.0.0/16;
```

## 使用 DNS 安全扩展

DNSSEC 是 DNS 协议的一组安全扩展，使用加密数字签名提供数据完整性和身份验证。它提供了在 DNS 中存储公钥并使用它们验证事务的功能。DNSSEC 尚未广泛部署，但 BIND 9 支持用于服务器间的事务（区域传输、NOTIFY、递归查询、动态更新）。如果你的从服务器也运行 BIND 9，配置 TSIG（事务签名）是值得的。在这里我们简要讨论使用 TSIG 进行认证区域传输。

首先，使用 `dnssec-keygen`（就像我们使用 `rndc` 一样）生成共享密钥。该密钥存储在主服务器上。与之前一样，我们从 .private 文件中提取 `Key:` 数据。以下命令创建一个 512 位的主机传输传输密钥：

```bash
$ dnssec-keygen -hmac-md5 -b 512 -n host transfer
```

请记住不要通过不安全的通道将密钥从一台机器传输到另一台机器。使用 ssh、sftp (FTP) 或类似的工具。还要记住共享密钥不应存储在世界可读的文件中。两台机器上完全相同的语句看起来如下：

```
key transfer {

    algorithm 'hmac-md5';

    secret '...';                                     # 来自 .private 文件的密钥

}
```

最后，我们在主服务器上设置了一个服务器语句，指示它在与从服务器通信时使用刚刚创建的密钥，并使用适当的 allow-transfer 指令启用认证区域传输：

```
server 192.0.2.96 {

    key { transfer; }

}
```

BIND 9 ARM 包含了更多关于 TSIG 配置和 BIND 中 DNSSEC 支持的信息。

## 使用拆分 DNS (Split DNS)

BIND 经常运行在防火墙上——既作为网络内部解析器的代理，又用于为某些区域提供权威数据。在这些情况下，许多人倾向于避免通过 DNS 暴露过多的私有网络配置细节（尽管对于这是否真的有用存在一些争议）。从防火墙访问您系统的人只能看到显式允许访问的信息，而内部主机则允许访问其他数据。这种设置被称为拆分 DNS。

假设您有一组想要向外界开放的区域，以及另一组您希望让网络上的主机看到的区域。您可以使用如下配置来实现这一点：

```
acl private { localhost; 192.168.0.0/24; # 适当定义您的内部

network;};

view private_zones { match { private; }; recursion yes;

# 内部主机的递归解析。 zone internal.zone {

    # 区域语句; }; # 更多内部区域;}

view public_zones

{ match { any; } recursion no; zone external.zone {

}; # 区域语句;

} # 更多外部区域;}
```

此外，您可能希望配置内部主机 `named` 实际上将所有查询转发到防火墙，并且永远不尝试自己解析查询。named.conf 中的 `forward-only` 和 `forwarders` 选项可以做到这一点。（`forwarders` 指定了向其转发查询的名称服务器的 IP 地址列表。）

BIND 9 ARM 讨论了在安全的拆分 DNS 配置中运行 BIND 的几个细节。

## Fedora Core 和 Linux 命令

- 您将使用以下命令在 Fedora Core Linux 中管理 DNS：
- `dig`: 域名信息命令，用于查询远程 DNS 服务器
- `host`: 域名名称服务器查询工具
- `named`: Fedora Core Linux 附带的名称服务器程序
- `system-config-bind`: 用于配置 DNS 的 GUI 工具
- `update`: 动态 DNS 更新工具
- `rndc`: BIND 附带的名称服务器控制工具

## 引用

- [http://www.dns.net/dnsrd/]—DNS 资源数据库。
- [http://www.isc.org/products/BIND/]—ISC 的 BIND 网页。
- [http://archive.quadratic.net/docs/B9ARM.pdf]—《BIND 9 管理员参考手册》。
- 《The Concise Guide to DNS and BIND》，Nikolai Langfeldt 著（Que Publishing，2000）——对 DNS 管理理论和操作方面进行了深入讨论。
- [http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Chroot-BIND.HOWTO]—关于 chroot 如何与 BIND 9 工作的指南。
- [http://langfeldt.net/DNS-HOWTO/]—BIND 版本 4、8 和 9 版本的 DNS HOWTO 的主页。
- [http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/DNS-HOWTO.html#63]—设置解析缓存名称服务器。注意，引用的名为 `/var/named/root.hints` 的文件在 Fedora Core 中称为 `/var/named/named.ca`。
- [http://spf.pofobox.com/]—SPF（发送者策略框架）主页，一种防止电子邮件地址伪造的方法。

# 第 15 章

## 互联网连接

### 本章内容

- 常用配置信息
- 建立基础：localhost 接口
- 配置拨号上网访问
- 配置数字用户线路 (DSL) 接入
- 排除连接故障
- 配置拨入 PPP 服务器
- 引用

Fedora Core Linux 以多种方式支持互联网连接和互联网资源的使用。您将在此书中版本的 Fedora Core Linux 中找到丰富的互联网相关软件，并可以从各种来源下载数百个额外的免费工具。要使用它们，您需要一个可以工作的互联网连接。

在本章中，您将学习如何在 Fedora Core 中使用调制调器和点对点协议 (PPP) 以及其他方法（包括数字用户线路 DSL 和电缆调制器服务）建立互联网连接。几年前，让拨号连接工作是很困难的——因此这本书整整一章都用于它。现在，只要您有一个硬件调制调器，拨号配置就很简单。红帽工程师和 Linux 社区在实现连接方面已经取得了巨大进展。

### 常用配置信息

静态 IP 的费用比动态 IP 高。普通消费者并不需要静态 IP 的优势，因此他们乐意为动态分配的 IP 较少的费用。此外，DNS 信息可以通过动态主机配置协议（DHCP）由 ISP（互联网服务供应商）自动提供。这将在第13章“网络连接”中进行深入讨论。

如果你使用 DSL 接入或电缆调制解调器，你可能会通过 DHCP 获得动态 IP，也被分配一个静态 IP。如果你使用 DHCP，可能会自动获得 DNS 服务器的名称，或者你可能需要手动设置 DNS（在这种情况下，你需要知道 DNS 服务器的 IP 地址）。

在所有情况下，你都需要知道你的用户名、密码，以及配置其他服务时所需的邮件服务器和新闻服务器的名称。如果你专门要求，可以从你的 ISP 处获取这些信息。

> 注意
本书中的信息将帮助你理解并避免许多连接问题，但你仍可能遇到连接问题。请手留你 ISP 的技术帮助服务电话，以防你无法建立连接。请注意，很少有 ISP 提供 Linux 支持，如果你的特殊情况无法通过从书中获得的知识来解决，你可能需要向精通 Linux 的朋友或 Linux 用户组寻求帮助。

### 基础准备：localhost 接口

在连接互联网或网络之前，必须创建一个虚拟（dummy）或 localhost 接口。该接口被称为 lo（回环接口），被 TCP/IP 协议用于为你的机器分配 IP 地址，并且是建立 PPP 接口所必需。lo 接口也被许多网络感知应用程序使用，并且于设置。

#### 检查回环接口的可用性

Fedora Core 通常会在安装过程中处理此接口的设置。你可以以 root 身份使用 `ifconfig` 命令查看它是否可用。如果 lo 可用，命令及其响应将类似于下所示：

```
# /sbin/ifconfig

lo Link encap:Local Loopback

inet addr:127.0.0.1 Mask:255.0.0.0

UP LOOPBACK RUNNING MTU:16436 Metric:1

RX packets:12 errors:0 dropped:0 overflows:0 frame:0

TX packets:12 errors:0 dropped:0 overflows:0 carrier:0

collisions:0 txqueuel:0

RX bytes:760 (760.0 b) TX bytes:760 (760.0 b)
```
