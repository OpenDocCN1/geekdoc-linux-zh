
进入`/path/to/xxx`目录，找到`xxx.json`。

源端口在 DNS 世界中变得非常重要，这是因为 Dan Kaminsky 发现了 DNS 协议的一个漏洞，该漏洞允许在名称服务器使用可预测的源端口和查询 ID 时进行缓存投毒。UDP 端口的 `use-` 和 `avoid` 选项结合 `named` 软件的更改缓解了这种攻击。不要使用 `query-source` 为 DNS 查询指定固定的出口端口，否则你将抵消大随机端口范围提供的 Kaminsky 保护。

`use-*-udp-ports` 的默认值已经足够好，你通常不需要更改它们。如果你的防火墙阻止了该范围内的某些端口（例如用于 SunRPC 的 2049 端口），当你的名称服务器发送查询并使用被阻止的端口之一作为源时，防火墙会拦截答案，名称服务器最终会停止等待并重新发送查询。这虽然不是致命的，但对于处于“火力中”的用户来说非常困扰。

为了避免这个问题，请使用 `avoid-*-udp-ports` 选项让 BIND 避开被阻止的端口。任何被防火墙阻止的高位 UDP 端口都应该在列表中¹。如果你响应某些攻击更新了防火墙，请务必更新此处的端口列表。

`query-source` 选项允许你指定用于出站查询的 IP 地址。例如，你可能需要使用特定的 IP 地址来通过防火墙，或者区分内部和外部值。
`query` 从随机的高位端口发出，而答案返回到这些相同的端口。因此，你的防火墙必须准备好接受随机高位端口上的 UDP 报包。一些系统管理员以前设置一个特定的出口端口号，以便配置防火墙识别它并仅接受该端口的 UDP 报包。在 Kaminsky 时代，这种配置已不再安全。

如果你使用 `query-source` 选项，请仅指定你希望从哪个 IP 地址发送查询；不要指定端口号。

> ¹ 某些防火墙是有状态的，可能足够智能，可以识别出 DNS 答案与一秒前的相应查询是配对的。此类防火墙不需要此选项的帮助。

# 第 17 章 DNS：域名命名系统

## 转发的使用

```
forwards { in_addr; in_addr; ... }; [empty list]
forward only | first;
```

与其让每个名称服务器都执行其外部查询，你可以指定一个或多个服务器作为转发器。普通的服务器可以从其缓存以及它拥有权威性的记录中查找。如果它没有找到所需的答案，就可以将查询发送给转发器主机。这样，转发器构建的缓存有利于整个站点。这种设计是隐式的——转发器配置文件中没有任何地方说“嘿，你是一个转发器”。

`forwards` 选项列出了你想要作为转发器的服务器 IP 地址。它们会被轮流查询。使用转发器规避了从根服务器开始并遵循引用链的正常 DNS 流程。请注意不要创建转发循环。

`forward-only` 服务器缓存答案和对转发器的查询，但它永远不会查询其他。如果转发器没有响应，查询将失败。`forward-first` 服务器首选处理转发器，但如果它们没有响应，`forward-first` 服务器将自行完成查询。

由于 `forwards` 选项没有默认值，除非经过专门配置，否则不会发生转发。你可以在全局或在单个区域语句内开启转发。

## 权限

```
allow-query { address_match_list }; [all hosts]
allow-query-cache { address_match_list }; [all hosts]
allow-transfer { address_match_list }; [all hosts]
allow-update { address_match_list }; [none]
blackhole { address_match_list }; [empty]
```

这些选项指定了哪些主机（或网络）可以查询你的名称服务器或其缓存、阻止你的区域数据传输，或动态更新你的区域。这些列表是低成本的安全形式，且容易受到 IP 欺骗的影响，因此依赖它们存在某些风险。如果有人欺骗你的服务器回答 DNS 查询，可能不是大问题，但要避免 `allow-update` 和 `allow-transfer` 子句；请改用加密密钥。

黑名单地址列表标识了你永远不想通信的服务器；`named` 不接受来自这些服务器的查询，并且永远不会向它们询问答案。

## 报包大小

```
edns-udp-size <number>; [4096]
max-udp-size <number>; [4096]
```

互联网上的所有机器都必须能够重组 512 字节的 UDP 报包。

# option 语句

由于 DNS 使用 UDP 且 DNS 响应通常大于 512 字节，DNS 管理员必须担心大报包被丢。如果你的防火墙只允许分片的第一个 UDP 包通过，接收端将收到截断答案并用 TCP 重试查询。

`edns-udp-size` 选项设置名称服务器宣告的缓冲区大小。`max-udp-size` 设置服务器实际发送的最大报包大小。这两个大小都在 512-4096 字节范围内。

要了解你的站点允许的报包大小，运行 `dns.net txt` 命令并查看返回结果；关于 DNS reply-size 服务器的详情见第 652 页。如果该工具显示的很小，问题可能在你的边界，你需要修复防火墙。

作为临时解决方案，尝试将 `max-udp-size` 参数设置为 `reply-size` 服务器显示的值。此设置会让 `named` 将答案压缩到可能不分片的报包中。将 `edns-udp-size` 设置为相同的值，以便确保双向流量。在修复防火墙后，忘记将值改回 4096！

除非你确定存在报包大小问题，否则请避免这些选项，因为它们限制了可以处理完整 4096 字节路径的大小。

```
dnssec-enable yes | no; [yes]
dnssec-validation yes | no; [yes]
dnssec-lookaside domain trust-anchor domain; ".dlvis.org"
dnssec-must-be-secure domain yes | [none]
```

这些选项配置了对 DNSSEC 的支持。从第 648 页开始的章节提供了 DNSSEC 的通用讨论以及如何在站点设置 DNSSEC 的详细描述。

权威服务器需要开启 `dnssec-enable` 选项。递归服务器需要开启 `dnssec-enable` 和 `dnssec-validation`，并通过 `trusted-keys` 语句指定信任锚点。

如果目标域没有信任锚点，软件将尝试使用 `dnssec-lookaside` 选项查找一个，这规避了父域没有使用 DNSSEC 的问题。

# 第 17 章 DNS：域名系统

`dnssec-enable` 和 `dnssec-validation` 默认开启，这具有各种方面的影响：

- 一个已签名区域的权威服务器在开启 DNSSEC 感知位的情况下响应查询时，它将返回所请求的资源记录及其签名。
- 一个已签名区域的权威服务器在未设置 DNSSEC 感知位的情况下响应查询时，它仅返回所请求的资源记录，这与 de pre-DNSSEC 时代相同。
- 一个未签名区域的权威服务器响应查询时仅返回所请求的资源记录；没有需要包含的签名。
- 递归服务器代表用户发送带有 DNSSEC 感知位标记的查询。
- 递归服务器在将数据返回给用户之前，会验证已签名回复中包含的签名。

`dnssec-lookaside` 选项两个两个作为参数。例如，默认值等同于以下配置行：

```
dnssec-lookaside ".* trust-anchor \"div.isc.org\";";
```

此配置告诉名称服务器，如果无法从 DNS 命名树的根节点获取安全委托，则建立一个信任链来指向 `div.isc.org`。根域名和顶级域已签名并由 DNSSEC 服务，将不再需要旁路验证。请参第 661 页关于 DLV 的优缺点及其隐私影响的讨论。

`dnssec-must-be-secure` 选项允许你指定仅接受来自特定域的安全答案，或者相反，你不接受是不安全的答案。例如，你可以对 `important-mybank.com` 域名这样做，而对 `marketing.mybank.com` 域名这样做。涉及的域名必须被你的 `trusted-keys` 子句覆盖或在 DLV 服务器注册。

### 统计信息
`zone-statistics yes | no [no]`

此选项使 `named` 维护每个区域的统计以及全局统计。关于 `named` 编译的统计以及如何显示它们的更多信息，请参第 676 页。

### 性能调优

| 选项 | 类型 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- |
| clients-per-query | int | [10] | 等待同一查询的客户端 |
| max-cache-per-query | int; [100] | 服务器丢弃前的最大客户端 |
| datasize | int; [unlimited] | 服务器可能使用的最大内存 |
| files | int; [unlimited] | 并发打开的文件数 |
| lame-ttl | int; [10min] | 缓存失效服务器数据的秒数 |
| max-cache-size | int; [] | 额外缓存的缓存大小 |
| max-cache-size | int; [] | 缓存答案的最大内存 |

# (TSIG) key 语句

| 选项 | 类型 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- |
| max-cache-ttl | int; | [1week] | 缓存正数据的最大 TTL |
| max-journal-size | int; | [] | 事务日志文件的最大大小 |
| max-ncache-ttl | int; | [3hrs] | 缓存负数据的最大 TTL |
| tcp-clients | int; | [100] | 最大并发 TCP 客户端 |

这个长选项列表可以用于在硬件上调优 `named` 运行。我们没有详细描述它们，但如果你遇到性能问题，这些选项可能为你的调优工作提供起点。

呼，我们终于完成了选项部分。让我们继续剩余的配置语言！

# acl 语句

访问控制列表仅仅是一个带有名称的地址匹配列表：

```
acl_name {
  address_match_list
};
```

你可以在任何调用地址匹配列表的地方使用 `acl` 名称。`acl` 必须是 `named.conf` 中的顶层语句，因此不要在其他选项声明中间偷偷溜入它。`named.conf` 是单次通过读取的，因此访问控制列表必须在使用它们之前定义。预定义了四个列表：

- `any` - 任意主机
- `localnets` - 本地网络上的所有主机
- `localhost` - 机器本身
- `none` - 无

`localnets` 列表包含了主机直接连接的所有网络。换句话说，它是机器网络地址对网络掩码取模的列表。

# TSIG key 语句

`key` 语句定义了一个“共享密钥”（密码），用于验证两个服务器之间的通信；例如，用于区域传输的主服务器和从服务器之间，或者服务器与控制它的 `rndc` 进程之间的通信。关于 BIND 对加密认证支持的背景信息请参见从第 642 页开始的安全问题。在这里，我们简要触及该过程的机制。

要构建密钥记录，你需要同时指定要使用的加密算法和共享密钥，共享密钥表示为 base64 编码的字符串（详见第 645 页）：

```
key-id {
  algorithm string;
  secret string;
};
```

# 第 17 章 DNS：域名系统

与访问控制列表一样，`key-id` 必须在使用之前通过 `key` 语句定义。要将密钥与特定服务器关联，只需在该服务器 `server` 语句的子句包含 `key-id`。密钥用于验证来自该服务器的请求，并对这些请求的响应进行签名。

共享密钥是敏感信息，不应保存在 world可读的文件中。使用 `include` 语句将其引入 `named.conf` 文件。

# trusted-keys 语句

理论上，DNSSEC 父区域授权其子区域的公钥，允许签名一直溯源到 DNS 根节点。实际上，根节点和顶级域不支持 DNSSEC，因此需要其他方法来验证区域的公钥。

`trusted-keys` 语句允许你指定仅接受来自特定域的安全答案，或者相反，你不接受是不安全的。例如，你可以对 `important-mybank.com` 域名这样做，而对 `marketing.mybank.com` 域名这样做。涉及的域名必须被你的 `trusted-keys` 子句覆盖或在 DLV 服务器注册。

## 日志语句

`named` 是当前“地球上最可配置日志系统”奖项的获得者。Syslog 将日志消息的优先级排序权交给程序员，而将这些消息的处理权交给系统管理员。对于给定的优先级，系统管理员无法说“我关心这条消息，但不关心这条消息：”。BIND 增加了类别（categories）来按类型对日志消息分类，并增加了通道（channels）来扩大消息处理的选择。类别由程序员决定，而通道由系统管理员决定。

由于日志记录需要大量的解释且与主题有些偏移，请参阅从第 667 页开始的调试部分进行讨论。

## statistics-channels 语句

`statistics-channels` 语句允许你通过浏览器连接到运行中的 `named`，以查看正在积累的统计数据。由于你服务器的统计数据可能敏感，你应该将这些数据的访问限制在所在站点的可信主机上。其语法如下：

```
statistics-channels {
    inet (ip-addr | *) port# allow { address_match_list ;
}}
```

你可以包含 `inet-port-allow` 序列。默认是开放的，所以要小心！IP 地址默认为任意，端口默认为 80 端口（普通 HTTP），`allow` 子句默认允许任何人连接。使用统计通道时，你必须使用 `libxml2` 编译 `named`。

## zone 语句

`zone` 语句是 `named.conf` 文件的核心。它们告诉 `named` 哪些区域是其权威的，并设置适用于管理每个区域的选项。*zone* 语句也用于缓存服务器来预加载根服务器提示——根服务器的名称和地址，这些提示启动了 DNS 查找过程。

`zone` 语句的准确格式取决于 `named` 在该区域中扮演的角色。可能的区域类型有主（master）、从（slave）、提示（hint）、转发（forward）、存根（stub）和仅委托（delegation-only）。我们没有描述存根区域（仅 BIND 使用）或仅委托类型（用于停止在顶级区域中使用通配符来发布注册商的服务）。接下来的简短章节描述了其他区域类型。

早些时候介绍的许多全局选项可以成为 `zone` 语句的一部分并覆盖之前定义的值。我们在这里没有重复这些选项，但提到了某些经常使用的选项。

## 为区域配置主服务器

为区域配置主服务器
对于以此 `named` 为主服务器的区域，你需要如下格式：

```
zone "domain_name" {
  type master;
  file "path";
}
```

区域规格规范中的 `domain_name` 必须始终出现在双引号中。
区域数据存储在磁盘上人类可读（且人类可编辑）的文件中。由于文件名没有默认值，因此在声明主区域时必须提供 `file` 语句。区域文件只是第 574 页描述的格式的 DNS 资源记录集合。

其他特定服务器的属性也经常在 `zone` 语句中指定。例如：

```
allow-query { address_match_list }; [any]
allow-transfer { address_match_list }; [any]
allow-update { address_match_list }; [none]
zone-statistics yes | [no]
```

访问控制选项也是必须的，但使用它们是一个好主。每个选项接受 IP 地址或 TSIG 加密密钥。通常，加密密钥是安全的。如果该区域允许动态更新，则必须存在 `allow-update` 子句，并带有一个地址匹配列表以限制发生更新的主机。动态更新仅适用于主区域；`allow-update` 子句不能用于从区域。确保该子句仅包含你的机器（例如 DHCP 服务器），而不是整个互联网。

`zone-statistics` 选项让 `named` 跟踪查询/响应统计数据，例如重定向、导致错误和需要递归的响应数量和百分比。请参见第 676 页的示例。

有了所有这些区域特定的选项（以及我们未涵盖的约 40 多个），配置听起来开始变得复杂。然而，一个仅包含区域文件路径的主声明是完全合理的。这里有一个来自 BIND 文档的稍作修改的示例：

```
zone "example.com" {
  type master;
  file "forward/example.com";
  allow-query { any };
  allow-transfer { my-servers };
}
```

在这里，`my-servers` 将是你之前定义的访问控制列表。

20. 你还需要在防火墙处进行入站流量过滤；参见第 932 页。更好的是使用 TSIG 进行身份验证。

## 第 17 章 DNS：域名系统

## 为区域配置从服务器

从区域的 `zone` 语句与主区域类似：

```
zone "domain_name" {
    type slave;
    file "path";
    masters {ip_addr [port ip_port] [key keyname]; ... }; [no default];
    allow-query {address_match_list};
}
```
