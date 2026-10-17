
```
dnssec-lookaside trust-anchor "isc.org";
```

此配置告诉名称服务器在无法从 DNS 命名树根获取安全委托信息时建立信任链。根和顶级域已签名并提供 DNSSEC 服务，不需要验证。见第 661 页关于 DNSSEC 的优缺点及其影响。

`dnssec-must-be-secure` 选项允许你指定只接受特定域名的安全答案，或者你不在意不安全的。例如，你可以对 `important-stuff.mybank.com` 说 `yes`，对 `marketing.mybank.com` 说 `no`。涉及的域名必须被你的 `trusted-keys` 覆盖或在 DNS 服务器注册。

`zone-statistics yes; [no]` 此选项让 `named` 将区域统计维护为全局统计。见第 666 页关于 `named` 编译统计信息以及如何显示它们的信息。

| 性能调优 | | |
| :--- | :--- | :--- |
| `clients-per-query` int; [10] | 等待同一个查询的客户端 |
| `max-clients-per-query` int; [100] | 丢弃前的最大客户端数 |
| `sizes` int; [unlimited] | 服务器可最大内存 |
| `files` int; [unlimited] | 并发打开的文件数 |
| `lame-ttl` int; [10min] | 缓存失效服务器数据的秒数 |
| `max-cache-size` int; [] | 额外数据的缓存大小 |
| `max-cache-size` int; [] | 缓存答案的内存内存 |

| 统计信息 | | |
| :--- | :--- | :--- |
| `max-cache-ttl` int; [1week] | 缓存正向数据的最大 TTL |
| `max-cache-size` int; [] | 事务日志文件的最大大小 |
| `max-cache-ttl` int; [3hrs] | 缓存负向数据的最大 TTL |
| `tcp-clients` int; [100] | 最大同时 TCP 客户端数 |

这一长长的选项列表可调优 `named` 以使其在你的硬件上运行良好。我们没有详细描述它们，但如果你遇到了性能问题，这些选项可能为你的调优工作提供起点。

呼，我们终于完成了选项部分。让我们继续学习配置语言的其他部分！

# acl 语句

访问控制列表只是一个带名称的地址列表：

```
acl acl_name {

    address_match_list

};
```

你可以在任何调用地址列表的地方使用 `acl_name`。`acl` 必须是 `named.conf` 中的顶层语句，所以不要尝试将其溜入你的其他选项声明中。`named.conf` 是单次通过读取的，因此访问控制列表必须在使用之前定义。预定义了四个列表：

-   `any` - 所有主机
-   `localset` - 本地网络（网）上的所有主机
-   `localhost` - 机器本身
-   `none` - 没有任何

`localset` 列表包含了主机直接连接的所有网络。换句话说，它是机器网络地址对其网络掩码取模后的列表。

# (TSIG) key 语句

`key` 定义了一个“共享秘密”（即密码），用于验证两个服务器之间的通信；例如，在主服务器和用于区域传输的从服务器之间，或者在服务器和控制它的 `rndc` 协议之间。关于 BIND 支持加密认证的背景信息见从第 642 页开始的安全问题章节。在这里，我们简要介绍该过程的机制。

要构建一个键记录，你需要指定想要使用的加密算法以及以 base64 编码字符串表示的共享秘密（详见第 645 页）：

```
key key_id {

    algorithm string;

    secret string;

};
```

## 第 17 章

## DNS：域名系统

与访问控制列表一样，*key-id* 在使用之前必须先通过 *key* 语句进行定义。要将 *key* 与特定服务器关联，只需在相应 *server* 语句的 *clauses* 中包含 *key-id* 即可。该密钥用于验证来自该服务器的请求，并对这些请求的响应进行签名。

共享密钥是敏感信息，不应保存在全局可读的文件中。使用 `include` 语句将其引入 `namedd.conf` 文件中。

### trusted-keys 语句

理论上，DNSSEC 的父区域会验证其子区域的密钥，允许签名一直回溯到 DNS 根进行链式验证。在实践中，根区域和顶级域不支持 DNSSEC，因此需要其他方法来验证区域的密钥。

`trusted-keys` 语句是一种强制性方法，它直接告诉 `named`：“区域 XXX.com 的正确公钥是 YYY”，而 这种方法绕过了用于获取和验证区域密钥的常规 DNSSEC 机制。这种声明被称为“信任锚点（trust anchor）”。它旨在用于区域已签名但其父区域未签名的情况。

当然，XXX.com 必须对你的网站足够重要到值得这样对待，而且你必须通过某种带外方式来确定密钥的值。获取正确的密钥并没有什么魔法；远程区域的管理员必须通过电话告知你，或者通过其他可以验证身份的方式发送给你。HTTPS 安全网页通常用于此目的。每当密钥更改时，你都必须重新执行整个过程。

`trusted-keys` 语句的格式如下：

```
domain flags protocol algorithm key;

domain flags protocol algorithm key;

...
```

每一行代表一个特定域的信任锚点。`flags`、`protocol` 和 `algorithm` 是非负整数。`key` 是一个 base-64 编码字符串，与用于签名区域的 `DNSKEY` 资源记录匹配。

DNSSEC 的详细内容从第 648 页开始介绍。

### server 语句

**named** 潜在可能会与许多服务器通信，而其中并非所有服务器都运行着最新软件，也并非所有服务器都有名义名称，*server* 语句告诉 **named** 关于其远程对端的相关特征。*server* 语句可以覆盖特定服务器的默认设置；除非你想为区域传输（zone transfers）配置密钥，否则并不是必须的。

### masters 语句

```
server ip_addr {

  bogus yes | no; [no]

  provide-ifxr yes | no; [yes]

  request-ifxr yes | no; [yes]

  keys { key-id, key-id, ... }; [none]

  transfer-source ip-address [port]; [closest interface]

  transfer-source-v6 ipv6-address [port]; [closest interface]

};
```

你可以使用 `server` 语句为单个服务器覆盖全局配置选项的值。只需列出你希望使用非默认行为的选项即可。我们没有显示所有服务器特定的选项，仅显示了我们认为可能需要的。完整列表请参考 BIND 文档。

如果你将一个服务器标记为伪造（`bogus`），`named` 将不会向其发送任何查询。该指令应预留给确实是伪造的服务器；它与全局选项 `blackhole`（黑洞）的区别在于，`bogus` 仅扫描出站查询。相比之下，`blackhole` 选项会完全消除与列出的服务器的所有形式的通信。

作为动态更新区域主服务器的 BIND 服务器如果 `provide-ifxr` 设置为 `yes`，则会执行增量区域传输。同样，作为从服务器的服务器如果 `request-ifxr` 设置为 `yes`，则向主服务器请求增量区域传输。动态 DNS 在第 640 页有详细讨论。

`keys` 子句识别一个之前在 `key` 状态中定义的 ID，用于 TSIG 事务签名（见第 645 页）。对远程服务器的任何请求都将使用此密钥进行签名。来自远程服务器的请求不需要签名，但如果它们进行了签名，则将进行签名验证。

`transfer-source` 子句提供了应作为区域请求源地址（端口）的接口的 IPv4 或 IPv6 地址（以及（可选的）端口）。只有当系统有多个接口且远程服务器在其 `allow-transfer` 子句中有特定 IP 地址时，才需要此子句；这些地址必须匹配。

### masters 语句

`masters` 语句允许你通过识别 IP 地址和加密密钥来定义一组一个或多个主服务器。你可以在 `masters` 子句中使用定义的名称，而无需重复列出 IP 地址和密钥。

语法为：

```
masters name { ip_addr [port ip_port] [key key] ; };
```
