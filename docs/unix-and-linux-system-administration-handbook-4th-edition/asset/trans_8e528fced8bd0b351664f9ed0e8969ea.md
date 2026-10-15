

Snippets of the files internal/atrust.com and world/atrust.com are shown below. First, the internal file:

```
; atrust.com - internal file
$TTL 86400
$ORIGIN atrust.com.
@               3600  SOA     ns1.atrust.com. trent.atrust.com. (
                                2010032900 10800 1200 3600000 3600 )
                3600  NS      NS1.atrust.com.
                3600  NS      NS2.atrust.com.
                3600  MX      10 mailserver.atrust.com.
                3600  A       66.77.122.161

ns1             A       192.168.2.11
ns2             A       66.77.122.161
www             A       66.77.122.161
mailserver      A       192.168.2.11
exchange        A       192.168.2.100
secure          A       66.77.122.161
...
```

使用 RFC1918 私有地址。另请注意，该站点没有使用 CNAME 为主机分配昵称，而是使用多个 A 记录。这种方案更快，因为遇到 CNAME 会导致额外查询。PTR 记录应仅指向映射到同一 IP 地址的多个名称中的一个。该站点还为其 DHCP 网络、我们的图书写作实验室以及其 Microsoft 基础设施委派了子域（未显示）。

以下是来自文件 world/atrust.com 的同一域的外部视图：

```
; atrust.com - external file
$TTL 57600
$ORIGIN atrust.com.
@               SOA     ns1.atrust.com. trent.atrust.com. (
                                2010030400 10800 1200 3600000 3600 )
                NS      NS1.atrust.com.
                NS      NS2.atrust.com.
                MX      10 mailserver.atrust.com.
                A       66.77.122.161

ns1.atrust.com. A       206.168.198.209
ns2.atrust.com. A       66.77.122.161
www             A       66.77.122.161
mailserver      A       206.168.198.209
secure          A       66.77.122.161
; reverse maps
exterior1       A       206.168.198.209
209.198.168.206 PTR     exterior1.atrust.com.
exterior2       A       206.168.198.213
213.198.168.206 PTR     exterior2.atrust.com.
...
```

与内部视图一样，昵称也是通过 A 记录实现的。实际上在外部世界视图中可见的主机很少，尽管从这些截断的摘录中并不明显。请注意，同时出现在两个视图中的机器（例如 ns1.atrust.com）在内部使用 RFC1918 私有地址，但在外部使用真实地址。

这些区域文件中的 TTL 设置为 16 小时（57,600 秒）。对于内部区域，TTL 为一天（86,400 秒）。区域文件中大多数单个记录未分配显式的 TTL 值。

外部文件末尾的奇怪 PTR 记录允许 atrust.com 的 ISP 委派一小块地址空间的反向映射。ISP 站点的 CNAME 记录使这种 CNAME hack 的变体能够工作；有关更多信息，请参阅第 585 页。

## The Internet Systems Consortium, isc.org

ISC 是 BIND 的作者和维护者，也是 F 根名称服务器的运营者。ISC 还运行一个 TLD 服务器，为许多顶级域名提供服务。这就是我们称他们为专家的原因！

下面是其配置文件中的片段。请注意，他们同时使用 IPv4 和 IPv6。他们还使用 TSIG 加密来在主从服务器之间对区域传输进行身份验证。transfer-source 选项确保传出区域传输请求的源 IP 地址符合主服务器上 allow-transfers 语句中的规范。

named.conf 文件：

```
// isc.org TLD name server
options {
    directory "/var/named";
    datasize 1000M;
    listen-on { 204.152.184.64; };
    listen-on-v6 { 2001:4f8:0:2:13; };
    recursion no;
    transfer-source 204.152.184.64;
    transfer-source-v6 2001:4f8:0:2:13;
};

// rndc key
key rndc_key {
    algorithm hmac-md5;
    secret "<secret>";
};

// TSIG key for name server ns-ext
key ns-ext {
    algorithm hmac-md5;
    secret "<secret>";
};
```

```
server 204.152.188.234 { keys { ns-ext; }; };

controls {
    inet 204.152.184.64 allow { any; } keys { rndc_key; };
};

include "inf/named.zones";      // Root, localhost, 127.0.0.1, ::1
include "master.zones";         // Zones we master
include "slave.zones";          // Lots of slaves
```

这些 include 语句使 named.conf 文件保持简短整洁。如果您提供大量区域，请考虑像这样将配置拆分为小块。更重要的是，设置您的文件系统层次结构，以便不要有一个包含一千个区域文件的文件夹。现代文件系统可以高效处理大型目录，但它们的管理可能很麻烦。

以下是 master.zones 文件的更多内容：

```
zone "isc.org" {
    type master;
    file "master/isc.org";
    allow-update { none; };
    allow-transfer { none; };
};

zone "sfo2.isc.org" {
    type master;
    file "master/sfo2.isc.org";
    allow-update { none; };
    allow-transfer { none; };
};

// Lots of zones truncated
```

以及 slaves.zones 中的内容：

```
zone "vix.com" {
    type slave;
    file "secondary/vix.com";
    masters { 204.152.188.234; };
};

zone "cix.net" {
    type slave;
    file "secondary/cix.net";
    masters { 204.152.188.234; };
};
```

master.zones 文件中 allow-transfer 子句设置为 none 意味着 ISC 使用多个主服务器——有人必须实现向从服务器的区域传输。

