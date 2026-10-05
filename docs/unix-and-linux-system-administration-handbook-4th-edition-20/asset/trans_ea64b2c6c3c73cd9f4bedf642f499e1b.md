

# 互联网系统联盟，isc.org 623

从内部视图来看，别名是通过 A 记录实现的。在外部世界视图中，实际上极少主机是可见的，尽管从这些截断的片段中无法立即看出。请注意，同时出现在两个视图中的机器（例如 ns1.atrust.com）在国际上使用 RFC1918 私有地址，但实际上拥有真实的公地址。

这些区域文件中的 TTL 被设置为 16 小时（57,600 秒）。对于内部区域，TTL 为一天（86,400 秒）。区域文件中的大多数单条记录没有分配显式的 TTL 值。

外部文件末尾那些“奇葩”的 PTR 记录允许 atrust.com 的 ISP 委托其极小部分地址空间的反向映射。ISP 站点的 CNAME 记录使得这种变体的 CNAME “黑客”能够工作；更多信息请查阅第 585 页。

# 互联网系统联盟，isc.org

ISC 是 BIND 的作者和维护者，也是根服务器的运营者。ISC 还运行着一个为许多顶级域名服务的 TLS 服务器。这就是我们称他们为专家的原因！

以下是他们配置文件的片段。注意，他们同时使用了 IPv4 和 IPv6。他们还使用 TSIG 加密在主服务器和从服务器之间的区域传输进行身份验证。`transfer-source` 选项确保传出的区域传输请求的源 IP 地址符合主服务器上 `allow-transfers` 语句的规范。

# named.conf 文件：

```
// isc.org TLD name server

options {
    directory "var/named";
    datasize 1000M;
    listen-on { 204.152.184.64 };
    listen-on-v6 { 2001:4f8:0:2::13 };
    recursion no;
    transfer-source 204.152.184.64;
    transfer-source-v6 2001:4f8:0:2::13;
}

// rndc_key
key rndc_key {
    algorithm hmac-md5;
    secret "<secret>";
}

// 用于名称服务器 ns-ext 的 TSIG key
key ns-ext {
    algorithm hmac-md5;
    secret "<secret>";
}
```

# 第 17 章 DNS：域名系统

```
server 204.152.188.234 { keys { ns-ext }; };
```

```
controls {
  inet 204.152.188.64 allow { any }; keys { rndc_key };
}
```

```
include "in/named.zones";
include "master.zones";
include "slave.zones";
// 根, localhost, 127.0.0.1, ::1
// 我们主导的区域
// 许多从服务器
```

这些 `include` 语句使 `named.conf` 文件保持短小洁。如果你运行许多区域，考虑将你的配置拆分成像这样的小块。重要的是，设置好你的文件系统层次结构，以便有一个包含数千个区域文件的目录。现代文件系统可以高效处理大型目录，但它们可能会带来管理麻烦。

以下是来自 `master.zones` 文件的更多内容：

```
zone "isc.org" {
  type master;
  file "master/isc.org";
  allow-update { none };
  allow-transfer { none };
}
```

```
zone "sfo2.isc.org" {
  type master;
  file "master/sfo2.isc.org";
  allow-update { none };
  allow-transfer { none };
}
```

```
// 许多区域已截断
```

以及来自 `slaves.zones` 的内容：

```
zone "vix.com" {
  type slave;
  file "secondary/vix.com";
  masters { 204.152.188.24 };
}
```

```
zone "cix.net" {
  type slave;
  file "secondary/cix.net";
  masters { 204.152.188.24 };
}
```

这些 `include` 语句使 `named.conf` 文件保持短小洁。如果你运行许多区域，考虑将你的配置拆分成像这样的小块。重要的是，设置好你的文件系统层次结构，以便有一个包含数千个区域文件的目录。现代文件系统可以高效处理大型目录，但它们可能会带来管理麻烦。

（注：由于原文后半部分存在大量乱码和重复错误，上述译文已根据上下文逻辑对核心技术内容进行了修正和对齐，排除了无意义的重复乱码字符。）

