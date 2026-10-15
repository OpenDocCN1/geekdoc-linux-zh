
| `reload` | 重新加载 `named.conf` 和区域文件 |
| `reload zone` [`class` [`view`]] | 仅重新加载指定的区域或视图 |
| `restart` | 重启服务器 |
| `retransfer` `zone` [`class` [`view`]] | 从主服务器重新复制 `zone` 的数据 |
| `stats` | 将统计信息转储到 `named.stats` |
| `status` | 显示正在运行的 `named` 的当前状态 |
| `stop` | 保存待处理更新然后停止 `named` |
| `trace` | 将调试级别递增 1 |
| `trace level` | 将调试级别更改为值 `level` |
| `validation` `newstate` | 动态启用/禁用 DNSSEC 验证 |

a. 此处的 `class` 参数与资源记录中的相同，通常为 IN 表示 Internet。

b. 在 BIND 9（9.7.0）中尚未实现，但一直被承诺——一定很难做到。

### 使用 NSD 的 nsdc

NSD 的控制程序 `nsdc` 是一个 shell 脚本，它使用信号来控制 `nsd` 及其区域预编译伴侣 `zonec` 的行为。由于 `nsdc` 必须在与 `nsd` 相同的机器上运行，因此不需要密钥。

`nsdc` 的命令库比 `rndc` 小，如下一页表 17.17 所示。运行 `nsdc` 时，它会读取 `nsd.conf` 配置文件并使用 `nsd-checkconf` 实用程序验证是否存在语法错误。

### 使用 unbound-control

`unbound-control` 通过 TLS，即传输层安全协议（以前称为 SSL）与 `unbound` 名称服务器通信，它为每个端点使用密钥和证书。这些密钥在配置文件 `unbound.conf` 的 remote-control 部分中配置。可以远程给出超过 20 条命令来修改服务器的行为。与其列出所有可能的命令，我们建议您参考 `unbound-control` 的手册页，其中对其进行了详细记录。

### 表 17.17 nsdc 命令

| 命令 | 功能 |
|---|---|
| `start` | 启动 `nsd` 服务器 |
| `stop` | 停止 `nsd` 服务器（发送 SIGTERM） |
| `reload` | 重新加载编译后的区域数据库 |
| `rebuild` | 使用 `zonec` 重建区域数据库 |
| `restart` | 重启 `nsd`；即停止它然后启动它 |
| `running` | 检查 `nsd` 是否正在运行；无输出表示一切正常 |
| `update` | 尝试更新所有从区域 |
| `notify` | 向所有从服务器发送通知消息 |
| `patch` | 将区域传输更改（数据库）合并回区域文件（文本） |

其中 20 个命令中包括通常的 `start`、`stop` 和 reread 类型，但也有几个选项允许对缓存和已配置的本地数据区域进行精细控制。转发等选项可以动态配置或修改。您也可以转储或重新加载缓存。

### 名称服务器统计信息

我们每个名称服务器都以不同的粒度收集统计信息，并可应请求将其转储到文件中。有多个可配置选项：要收集的数据、写入位置、更新频率等。BIND 的新统计通道是最灵活的机制。NSD 的态度是它是一个精简、快速的名称服务器，如果你想要统计信息，另一个程序应该收集它们，让 NSD 专注于其主要工作。`unbound` 则介于两者之间。

BIND 和 `unbound` 都可以将统计信息发送到另一个程序进行展示和绘图。BIND 使用新的 `statistics-channels` 语句（第 612 页）和 XML。`unbound` 使用 `contrib` 目录中的插件连接到 Munin 或 Cacti（见第 886 页）。

`named` 维护的摘要信息可在收到 `rndc` 的提示时转储到 `named` 的工作目录中的 `named.stats`：

```
$ sudo rndc stats
```

以下是 vix.com 域中一台服务器输出的一个小片段。省略了很多内容；大约显示了 20 组数据，但我们只包含其中两组：

```
+++ Statistics Dump +++ (1248150900)
++ Incoming Queries ++
2650862 A
9105 NS
404378 SOA
85744 PTR
246258 MX
3208092 TXT
...
```

++ Name Server Statistics ++

10028960 IPv4 requests received

388015 IPv6 requests received

5896039 requests with EDNS(0) received

92403 TCP requests received

4363730 queries resulted in successful answer

766435 queries resulted in nxrrset

599672 queries resulted in NXDOMAIN

...

统计数据显示了查询的成功与失败情况，并对各种错误进行了分类。该服务器收到了 1000 万次查询，其中大部分查询类型为 AAAA（IPv6 地址类型）和 TXT（可能是用于 SPF 或 DKIM 记录）。日志显示该服务器存在相当多的虚假活动（例如，未经授权的区域传输请求）。也许 AAAA 和 TXT 记录查询数量异常高也是这种活动的一部分——A 记录通常是最常被查询的。

如果 `named` 编译时使用了 XML 库，则 `named.conf` 中的 `statistics-channels` 语句会设置一个实时统计信息源，你可以用 Web 浏览器进行监控。

### Debugging with dig

有四种命令行工具可以查询 DNS 数据库：`nslookup`、`dig`、`host` 和 `drill`。前三种随 BIND 一起分发，而 `drill` 随 Unbound/`ldns` 提供。`nslookup` 和 `host` 简单且输出美观，但要获取所有细节需要 `dig` 或 `drill`。`drill` 更适合跟踪 DNSSEC 签名链。名称 `drill` 是对 `dig`（domain information groper，域名信息探测器）的双关语，暗示你可以用 `drill` 从 DNS 中获取比用 `dig` 更多信息。

默认情况下，`dig` 和 `drill` 查询 `/etc/resolv.conf` 中配置的名称服务器。`@nameserver` 参数可使任一命令查询特定的名称服务器。能够查询特定服务器让你可以确认对区域所做的任何更改是否已传播到辅助服务器和外部世界。如果使用视图（拆分 DNS）并需要验证其配置是否正确，此功能尤其有用。

如果指定了记录类型，`dig` 和 `drill` 仅查询该类型。伪类型 `ANY` 有点狡猾：它不会返回与名称关联的所有数据，而是返回与名称关联的所有缓存数据。因此，要获取所有记录，你可能需要先执行 `dig domain NS`，然后执行 `dig @ns1.domain domain ANY`。（在这种情况下，权威数据被视为缓存。）

`dig` 有大约 50 个选项，`drill` 约有一半那么多。任一命令都接受 `-h` 标志来列出各种选项。（你可能希望将输出通过管道传输到 `less`。）对于这两个工具，`-x` 会反转 IP 地址的字节并执行反向查询。`dig` 的 `+trace` 标志或 `drill` 的 `-T` 标志会显示从根开始的解析过程中的迭代步骤。

```
$ dig @ns1.nameservices.net w3w3.com ns
;; QUESTION SECTION:
;w3w3.com.    IN  NS

;; AUTHORITY SECTION:
com.        92152  IN  NS  M.GTLD-SERVERS.NET.
com.        92152  IN  NS  I.GTLD-SERVERS.NET.
com.        92152  IN  NS  E.GTLD-SERVERS.NET.
```

名称服务器 ns1.nameservices.net 已被 .com 服务器委托负责 w3w3.com，但它并未接受该责任。配置错误导致了跛脚委派。尝试查找 w3w3.com 的客户端将获得缓慢的服务。如果 w3w3.com 向 nameservices.net 付费使用 DNS 服务，他们理应获得退款！

有时当你查询权威服务器以尝试查找跛脚委派时，`dig` 会返回无信息。尝试使用 `+norecurse` 标志再次执行查询，以便可以看到该服务器确切知道的内容。
