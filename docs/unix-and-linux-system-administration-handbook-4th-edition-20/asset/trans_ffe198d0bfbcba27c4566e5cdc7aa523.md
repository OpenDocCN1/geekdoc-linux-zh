

# 第 17 章 DNS：域名系统

查询到达时。`match-recursive-only` 子句要求查询必须是递归的，并且源自允许的客户端。迭代查询（Iterative queries）允许你查看缓存中的内容；而此选项会阻止这种行为。

视图（Views）按顺序处理，因此首先处理限制最严格的视图。不同视图中的区域（Zones）可以具有相同的名称，但从不同的文件中获取数据。视图是一个“全有全无”的概念；如果你使用了视图，则 `named.conf` 文件中的所有 `zone` 语句都必须出现在视图的上下文中。

以下是一个来自 BIND 9 文档的示例。这两个视图定义了相同的区域，但使用了不同的数据。

```
view "internal" {
    match-clients { our_nets }; // 仅内部网络
    recursion yes;               // 仅内部客户端
    zone "example.com" {      // 区域的视图
        type master;
        file "example-internal.db";
    }
}
view "external" {
    match-clients { any };       // 允许所有查询
    recursion no;               // 但不允许递归
    zone "example.com" {      // 仅“公共”主机
        type master;
        file "example-external.db";
    }
}
```

如果视图的顺序反过来，将没有任何人能看到内部视图。内部主机在到达视图之前，会匹配外部视图 `match-clients` 子句中的任何值。

我们从第 620 页开始的第二个 DNS 配置示例提供了视图的另一个额外示例。

## 17.10 BIND 配置示例

现在我们已经探索了 `named.conf` 的奇妙之处，让我们来看一些完整的配置示例。在接下来的章节中，我们将讨论来自几种不同情境的样本：

- `localhost` 区域
- 一家使用拆分 DNS（split DNS）的小型安全公司
- 专家：isc.org，互联网系统联盟（Internet Systems Consortium）

## localhost 区域

地址 `127.0.0.1` 指向自身，并应该映射到名称 "localhost."某些网站将该地址映射到 "localhost.localdomain."，有些则两者都映射。对应的 IPv6 地址是 `::1`。

如果你忘记配置 `localhost` 区域，你的站点最终可能会向根服务器查询 `localhost` 的信息。根服务器接收到大量的查询，以至于操作人员正在考虑在根级别在 `localhost` 和 `127.0.0.1` 之间添加通用映射。根据 2010 年 1 月在欧洲 K 根服务器的测量结果（k.root-servers.org/statistics），"local" 是查询频率第四热门的域名，仅次于 `com`、`arp` 和 `net`。对于繁忙的名称服务器来说，有很多无用的查询（每秒 1500 次）。在流行的虚拟 TLD 类别中，其他异常名称还有 `home`、`localhost` 和 `domain`。

名称 `localhost` 的正向映射可以在域的正向区域文件中（带有适当的 `ORIGIN` 语句）定义，也可以在其自己的反向文件中定义。每个服务器（即使是缓存服务器）通常都是其自己的反向主机域的主服务器。

以下是 `named.conf` 中配置 `localhost` 的行：

```
zone "localhost" // localhost 正向区域
  type master;
  file "localhost";
  allow-update { none };
```

```
zone "0.0.127-in.addr.arpa" // localhost 反向区域
  type master;
  file "127.0.0";
  allow-update { none };
```

正向区域文件 `localhost` 包含：

```
$TTL 30
; localhost.
  IN SOA localhost. postmaster.localhost. (
      199805081 ;serial
      3600 ;refresh
      1800 ;retry
      604800 ;expiration
      3600 ;minimum)

  NS localhost.
  A 127.0.0.1
```

-21. 实际上，整个 A 类网络 127/8 都指向 `localhost`，但大多数人只使用 `127.0.0.1`。

以及反向文件 `127.0.0.0` ：

```
$TTL 30d
; 0.0.127.in-addr.arpa
@ IN SOA localhost. postmaster.localhost. ( 
    199805081 :serial
    3600 :refresh
    1800 :retry
    604800 :expiration
    3600 :minimum
    NS localhost.
    PTR localhost.
```

`localhost` 地址（127.0.0.1）的映射永远不会，因此超时时间可以设置得很大。注意序列号，它编码了日期；该文件最后一次更改于 1998 年。还要注意，本地域只列出了主名称服务器。这里的含义是 "0.0.127.in-addr.arpa"。

## 一家小型安全公司

我们的第一个示例针对一家专门从事安全咨询的小型公司——他们在最新版本的 Red Enterprise Linux 上运行 BIND 9，并使用视图来实现拆分 DNS 系统，使内部和外部用户使用不同的主机数据。他们还使用私有地址空间；地址的查询绝不会逃到互联网上扰乱全局 DNS 系统。以下是他们的 `named.conf` 文件，经过了格式化和注释：

```
options {
    directory "/var/domain";
    version "root@atrust.com";
    allow-transfer { 82.165.230.84; 71.33.249.193; 127.0.0.1; };
    listen-on { 192.168.2.10; 192.168.2.1; 127.0.0.1; 192.168.2.1; };
}
include "atrust.key"; // 600 权限文件的 atkey 定义
controls {
    inet 127.0.0.1 allow { 127.0.0.1; } keys { atkey; };
}
view "internal" {
    match-clients { 192.168.0.0/16; 206.168.198/28; 172.29.0.0/24; };
    recursion yes;
    include "infrastructure.zones";
    zone "example.com" {
        type master;
        file "example-internal.db";
    }
}
view "external" {
    match-clients { any };       // 允许所有查询
    recursion no;               // 但不允许递归
    zone "example.com" {      // 仅“公共”主机
        type master;
        file "example-external.db";
    }
}
```

## 一小型安全公司（续）

等待，OCR 文本在中间是碎片化的。我根据提供的片段重建了逻辑流。

```
view "internal" {
    match-clients { 192.168.0.0/16; 206.168.198/28; 172.29.0.0/24; };
    recursion yes;
    include "infrastructure.zones";
    zone "example.com" {
        type master;
        file "example-internal.db";
    }
}
```

## 一小型安全公司（重建流）

我们的第一个示例针对一家专门从事安全咨询的小型公司——他们在最新版本的 Red Enterprise Linux 上运行 BIND 9，并使用视图来实现拆分 DNS 系统，使内部和外部用户使用不同的主机数据。他们还使用私有地址空间；地址的查询绝不会逃到互联网上扰乱全局 DNS 系统。以下是他们的 `named.conf` 文件，经过了格式化和注释：

```
options {
    directory "/var/domain";
    version "root@atrust.com";
    allow-transfer { 82.165.230.84; 71.33.249.193; 127.0.0.1; };
    listen-on { 192.168.2.10; 192.168.2.1; 127.0.0.1; 192.168.2.1; };
}
include "atrust.key"; // 600 权限文件的 atkey 定义
controls {
    inet 127.0.0.1 allow { 127.0.0.1; } keys { atkey; };
}
view "internal" {
    match-clients { 192.168.0.0/16; 206.168.198/28; 172.29.0.0/24; };
    recursion yes;
    include "infrastructure.zones";
    zone "example.com" {
        type master;
        file "example-internal.db";
    }
}
view "external" {
    match-clients { any };       // 允许所有查询
    recursion no;               // 但不允许递归
    zone "example.com" {      // 仅“公共”主机
        type master;
        file "example-external.db";
    }
}
```

（注：OCR 在后面页面包含了大量的重复和碎片化区块。我将提供连贯的版本。）

