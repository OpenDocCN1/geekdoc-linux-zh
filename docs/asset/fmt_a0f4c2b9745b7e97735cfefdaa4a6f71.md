
```
view "external" {
    match-clients { any; };          // 允许所有查询
    recursion no;                    // 但不允许递归
    zone "example.com" {               // 仅限“公共”主机
        type master;
        file "example-external.db";
    }
}
```

如果反转视图，将没人能看到内部视图。内部主机将匹配外部视图 `match-clients` 子句中的 `any` 值。

我们的第二个 DNS 配置示例（从第 404 页开始）使用拆分 DNS 来强制通过 MX 记录执行入站网关；隐藏几个私有地址子网；并使从外部世界无法访问 HINFO 和 TXT 记录。

## 16.10 BIND 配置示例

现在我们已经探索了 `named.conf` 的奇妙之处，让我们来看一些完整的示例。接下来的章节显示了三个示例配置：

- 一个学生的 Linux 机器
- 一家使用拆分 DNS 的小公司
- 一个使用三日志的大学部门

### 家庭 Linux 机器

Rob Braun 是一个学生，家里有一台 Linux 机器，为他的域名 `example.net` 以及几个朋友提供 DNS 服务。他运行着 BIND 8.2.3。他的 `named.conf` 文件如下。Rob 的配置非常直观。大多数选项都是默认值：递归服务器、常规位置、查询和传输允许、在端口 53 上监听等。对区域配置进行了一些控制。例如，`example.net` 和 `example.org` 区域允许向一个主机传输，并且不允许动态更新。它是 `example.net` 和 `example.org` 两个域的主服务器。也是 `example.net` 和 `example.com` 的从服务器。正如学生配置预期的，日志部分不是默认的。它包含了 BIND 附带的示例。

```
/* named.conf */
options {
  directory "/var/named";
  pid-file "/var/named/named.pid";
}
zone "example.net" {
  type master;
  file "example.net";
  allow-transfer { 192.168.1.15 };
}
zone "example.org" {
  type master;
  file "example.org";
  allow-transfer { 192.168.1.15 };
}
zone "192.168.1.in-addr.arpa" { // 用于私有地址的反向区域
  type master;
  file "rev";
}
zone "." {
  type hint;
  file "cache.db";
}
zone "example.net" {
  type slave;
  file "example.net.sec";
  masters { 192.168.1.220 };
}
zone "example.com" {
  type slave;
  file "example.com.sec";
  masters { 192.168.1.220 };
}
```

![](img/4baffa9c0bc44e5d38f4bdc1a0243_0.png)

// 定义三个日志通道（重要的 syslog 信息、

// 中等调试和加载消息）然后

// 将类别映射到它们。

```
logging {
  channel syslog_errors {
    syslog local1;
    severity error;
  }
  channel moderate_debug {
    severity debug3; // 3级调试
    file "foo"; // 指向文件 foo
    print-time yes; // 时间戳日志条目
    print-category yes; // 打印类别
    print-severity yes; // 打印级别
  }
  channel no_info_messages {
    syslog local2;
    severity notice;
  }
category parser {
  syslog_errors;
  default_syslog;
}
category name-servers { null; }; // 不记录这些
category load { no_info_messages; };
category default {
  default_syslog;
  moderate_debug;
}
}
```

// logging 子句结束

此配置没有反向区域；`localhost` 必须在 `/etc/hosts` 文件中映射。

### 小型安全公司

我们的示例是一家专事安全咨询的小公司。他们在 Red Hat 7.2 上运行 BIND 9，并使用 `view` 实现拆分 DNS 系统，内部和外部用户可以看到不同的主机数据。他们对全局 DNS 系统使用私有空间。关于这些地址的查询永远不会逃逸到互联网……这是他们的 `named.conf` 文件，进行了格式化并增加了注释：

```
options {
  directory "/var/domain";
}
```

```
controls {
  inet 127.0.0.1 allow { 127.0.0.1; } keys { atkey; };
}
```

```
include "atrust.key"; // atkey 的模式 600 定义
view "internal" { // 内部视图
match-clients { 192.168.1.0/24; 192.168.2.0/24 };
 recursion yes;
zone "" { // 根提示区域
  type hint;
  file "named.ca";
}
zone "localhost" { // localhost 正向区域
  type master;
  file "localhost.zone";
  allow-update ( none );
}
zone "127.0.0.in-addr.arpa" { // localhost 反向区域
  type master;
  file "named.local";
  allow-update ( none );
}
zone "atrust.com" { // 内部正向区域
  type master;
  file "atrust.com-internal";
}
zone "192.168.2.in-addr.arpa" { // 内部反向区域
  type master;
  file "192.168.2.rev";
  allow-update ( none );
}
zone "1.168.1.in-addr.arpa" { // 内部反向区域
  type master;
  file "192.168.1.rev";
  allow-update ( none );
}
}
view "world" { // 外部视图
match-clients { any; };
 recursion no;
// 点和 localhost 区域如上，为简洁起见省略
zone "atrust.com" { // 外部正向区域
  type master;
  file "atrust.com-external";
}
}
```

# 402 Linux 管理手册

```
zone "kalos-strategy.com" IN { // 我们是从继的
type slave;
file "kalos-strategy.com";
masters { 66.1.239.14; };
zone "198.168.206.in-addr.arpa" { // 外部反向区域
type master;
file "206.168.198.rev";
allow-update ( none ); } // 外部视图结束
```

`atrust.key` 文件包含名为 `"atkey"` 的键值的定义：

```
key "atkey" {
algorithm hmac-md5
secret shared key goes here;
}
```

对于 `kalos-strategy.com`，需要两个条目，它是 `atrust.com` 的一家公司，且运行着一个从继服务器（`slave server`）。如果该区域（`zone`）仅在外部视图中提到，那么来自 `atrust.com` 域名之外的查询将没有问题，但来自内部的查询将发送到网络去询问一个由 `atrust.com` 自己的名称服务器具有权威性的问题。解决这种低效率的方案是在内部视图中提到 `kalos-strategy.com`，但将其列为正向区域（`forward zone`），以便名称服务器也能看到带有其外部主机（`ha`）的查询。
