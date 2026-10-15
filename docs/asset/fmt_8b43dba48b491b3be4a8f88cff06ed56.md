
```
zone "saclass.net" {
  type master;
  file "saclass/saclass.net";
  update-policy {
    grant feanor_mroe.subdomain saclass.net;
    grant mojo_mroe.subdomain saclass.net;
    grant dandle_mroe.subdomain saclass.net;
    grant pirate_mroe.subdomain saclass.net;
  }
}
```

# 表 16.5 BIND 中的安全功能

| 特性 | 上下文 | 页码 | 说明 |
| --- | --- | --- | --- |
| `acl` | 各种 | 534 | 访问控制列表 |
| `allow-query` | `options`, `zone` | 532 | 谁可以查询区域或服务器 |
| `allow-recursion` | `options` | 530 | 谁可以进行递归查询 |
| `allow-transfer` | `options`, `zone` | 532 | 谁可以请求区域传输 |
| `allow-update` | `zone` | 550 | 谁可以进行动态更新 |
| `blackhole` | `options` | 532 | 完全忽略的服务器 |
| `bogus` | `server` | 535 | 永远不查询的服务器 |
| `update-policy` | `zone` | 550 | 谁可以进行动态更新 |

# 重新回顾 BIND 中的访问控制列表

`ACL` 是命名的地址匹配列表，可以作为 `allow-query`、`allow-transfer` 和 `blackhole` 等语句的参数。其基本语法在第 534 页中描述。`ACL` 通过多种方式帮助增强 DNS 安全。

每个站点都应该至少有一个用于 `bogus` 地址的 `ACL` 和一个用于本地地址的 `ACL`。例如：

```
acl bogusnets {\      // 虚假网络的 ACL
    0.0.0.0/8;              // 默认通配符地址
    1.0.0.0/8;              // 预留地址
    2.0.0.0/8;              // 预留地址
    169.254.0.0/16;         // 链路本地地址
    192.0.2.0/24;           // 示例地址，如 example.com
    224.0.0.0/4;            // 多播地址空间
    10.0.0.0/8;             // 私有地址空间 (RFC1918)
    172.16.0.0/12;          // 私有地址空间 (RFC1918)
    192.168.0.0/16;         // 私有地址空间 (RFC1918)
};
```

```
acl cunets {\      // 科罗拉多大学网络的 ACL
    128.138.0.0/16;         // 主校区网络
    198.11.16/24;
    204.228.69/24;
};
```

在配置文件的全局选项部分，你可以包含：

```
allow-recursion { cunets; };
blackhole { bogusnets; };
```

如果你使用了私有地址并且正在配置你的内部 DNS 服务器，请不要将它们设为 `bogus`！

# DNS 安全问题

将区域传输限制在合法的从服务器也是一个好主意。`ACL` 让一切变得整洁有序：

```
acl ourslaves {
  128.138.242.1; // 节点
...
}
acl measurements {
  198.32.4.0/24; // Bill manning 的测量数据，v4 地址
  2001:478:6:0::48; // Bill manning 的测量数据，v6 地址
}
```

实际的限制通过类似下面的行实现：

`allow-transfer { ourslaves; measurements; };`

在这里，传输被限制在我们自己的从服务器以及一个互联网测量项目的机器，该项目通过遍历反向 DNS 树来确定互联网的规模以及配置错误的服务器百分比。通过这种方式限制传输，其他站点无法使用 `dig` 等工具（见第 509 页）导出你的整个数据库。

当然，你仍然应该通过路由器访问控制列表和每个主机的标准安全卫生措施在较低层次上保护你的网络。如果无法采取这些措施，你可以拒绝除网关机器以外的所有 DNS 数据包。

# 开放解析器 (Open resolvers)

开放解析器是一个在互联网上接受并回答查询的缓存服务器。开放解析器是有害的。外部人员可以在未经许可或不知的情况下消耗你的资源，如果他们有害，可能会污染你的解析器缓存。

糟糕的是，开放解析器有时被恶意用于放大拒绝服务攻击。攻击者向你的解析器发送伪造源地址的查询指向受害者。你的解析器会忠实地回答查询并向受害者发送数据包。统计数据显示，70% 到 75% 的缓存服务器目前是开放解析器！`site-factory.com/tools` 可以帮助测试你的站点。去那里，选择“open resolver”，并输入你服务器的 IP 地址。使用 `named.conf` 中的访问控制列表来限制你的缓存服务器回答来自你用户的查询。

# 第16 章 DNS：域名系统

## 运行 chroot

如果黑客攻破了你的名称服务器，他们可能会以该用户的身份访问系统。为了限制这种情况造成的损害，可以在 chroot 环境中以非用户身份运行服务器。对于 `named`，`-t` 标志指定 chroot 目录，`-u` 标志指定运行的 UID。例如：

```
$ named -u 53
```

许多站点没有使用 `-u` 和 `-t` 标志，但当发布新漏洞时，升级可能更好。chroot 牢笼不能是空的，因为它必须包含服务器通常需要的文件：`/dev/null`、`/dev/random`、配置文件、UNIX 套接字等。设置这些需要一些工作。chroot 调用在库加载后执行，因此不需要复制到牢笼。

## 使用 TSIG 进行服务器安全通信

在开发 DNSSEC（在下一节中介绍）期间，IETF 部署了一种名为 TSIG (`RFC2845`) 的简单机制，通过“事务签名”允许服务器之间的安全通信。仅通过 IP 地址可以保护主服务器与从服务器之间的区域传输，还可以保护动态更新。消息上的 TSIG 验证对方身份并确认数据未被篡改。签名在接收数据包时被检查并丢弃；它们不会被缓存成为 DNS 数据。

TSIG 使用对称加密。这意味着加密密钥与解密密钥相同。此密钥被称为“共享密钥”。TSIG 规范允许多种加密方法。为想要安全通信的每对服务器使用不同的密钥。TSIG 的计算开销比公钥加密得多，但由于需要手动配置，它适用于服务器对较少的本地网络。它无法扩展到全球互联网。

### 为 BIND 设置 TSIG

首先，使用 BIND 的 `dnssec-keygen` 为两个服务器（例如主、从）生成共享密钥主机密钥：

```
$ dnssec-keygen -a HMAC-SHA256 -b 128 -n HOST master-slave
master-slave1.+163+15496
```

`-b 128` 标志告诉 `dnssec-keygen` 创建 128 位密钥。我们在这里使用 128 位是为了让密钥足够短以适应打印在页面上。在现实生活中，你可能想使用更长的密钥；允许的最大是 512 位。此命令产生了两个：

```
master-slave1.+163+15496.private
master-slave1.+163+15496.key
```

`163` 代表 SHA-256 算法，`15496` 是当对一对服务器有多个密钥时使用的标识符。两个文件包含相同的密钥，但格式不同。

`.private` 密钥格式如下：

```
Private-key-format: v1.3
Algorithm: 163 (HMAC_SHA256)
Key: owt6W0l0ugaFVkw0qGxA==
Bits: AAA=
Created: 20160218012956
Publish: 20160218012956
Activate: 20160218012956
```

而 `.key` 文件看起来如下：

```
master-slave1. IN KEY 512 163 owt6W0l0ugaFVkw0qGxA==
```

注意 `dnssec-keygen` 在文件名和 `.key` 文件的内容末尾都添加了一个点。当 `dnssec-keygen` 用于添加到区域文件的 DNSSEC 密钥时，密钥名称必须是完全限定域名，因此以点结尾。可能应该有两个工具，一个用于生成共享密钥，另一个用于生成公钥密钥对。
