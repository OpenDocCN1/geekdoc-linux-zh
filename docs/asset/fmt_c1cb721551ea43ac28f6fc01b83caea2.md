
`$TTL` 指令将区域的默认最小生存时间设置为两天。这将在下一节中进行讨论。

# 区域文件的 SOA 记录

区域文件的第二行使用了你之前看到的特殊名称 `@`。在这里，它代表 `0.0.127.in-addr.arpa`，即 `SOA`（起始区域）记录所属的区域。括号内的字段包含了 SOA 特有的数据。

`SOA` 记录中的第一个 `data` 字段是主服务器的完全限定名称。第二个字段是区域的联系人邮箱地址。将 `@` 符号替换为“.”会将其写入 DNS 名称，例如 `foo@example.com` 将被写入 `foo.example.com`。

不要使用地址如 `a@example.com`，因为它会被误认为 `a.example.com`。确保 `SOA` 字段中指定的联系邮箱地址是重要的，因为它用于报告 DNS 设置问题和其他潜在有用信息。接几个数值字段指定此区域的各种特性。这些值必须正确配置，为了做到这一点，必须理解每个字段。如注释所示，这些字段是：序列号（serial number）、刷新间隔（refresh interval）、重试时间（retry time）、过期期（expire period）和最小 TTL。序列号是可以包含 0 之间值的 32 位数值。每当区域数据更改时，序列号必须递增。

# 使用 BIND 为真实域名提供 DNS

此更改作为那些需要传输区域内容的服务器的信号。通常使用 `YYYMMDDn` 格式分配序列号；即更改日期和两位数的修订版本（例如 20070610）。对于同一天的更改，只递增修订版本。对于次日的更改，日期更改且修订版本从 0 开始。

刷新间隔指定了客户端应该多久检查一次主数据是否更新。设置为 24 小时，但如果区域经常变化，该值应该更低。如果客户端和主都支持 NOTIFY 机制，重试时间在刷新时间过后客户端无法连接主服务器时才有效。它指定了再次尝试之前等待多久（设置为小时）。如果客户端在过期期内（通常由于严重故障）无法连接主服务器，它将丢弃已有的区域并停止查询。过期期应该足够长以便允许恢复。一千小时（约六周）是一个很好的默认值。如前所述，每个 RR 都有一个 `TTL` 字段，指定在数据源之前可以缓存多久。如果 RR 没有显式指定 `TTL`，则使用由 `TTL` 指令设置的默认 TTL。

`SOA TTL` 是 SOA 记录中的最后一个数值，用于确定负面响应（NXDOMAIN）应该缓存多久（也就是说，如果查询结果为 NXDOMAIN，该事实将缓存 SOA TTL 指定的时间）。旧版本的 BIND 使用 SOA TTL 来设置默认 TTL，但 BIND 9 不再这样做。为了缓存友好性，推荐默认 TTL 为 2（两天），SOA TTL 为 1（一小时）。之前使用的值适用于不经常变化的区域。对于具有不同要求的区域，你可能需要进行调整。对此，建议阅读 http://www.bind.net/docs/bind-9.html。

# 区域文件的其他记录

区域文件的最后两行创建了 NS 和 PTR 记录。NS 没有显式名称，因此它使用最后一个，即 SOA 记录的 `@`。因此，`0.0.127.in-addr.arpa` 的名称服务器定义为 `localhost`。

PTR 记录名称为 `1`，它变为 `1.0.0.1.in-addr.arpa`（地址 127.0.0.1 写入 DNS 名称的方式）。查询时，PTR 记录变为 `localhost`（在我们配置名称服务器为真实域名的权威后，你会看到许多 RR 类型中的）。

# TXT 记录和 SPF

DNS 中尚未提到一种记录，但最近的提议使用 TXT 记录来帮助文档工作，并对抗电子邮件伪造、垃圾邮件和钓鱼攻击。SMTP 的一个问题是，当邮件投递时，发送者可以声称邮件来自 `trusted.bank`，而实际上来自 `smalltime.crook`。邮件接收者收到邮件时，它看起来像是来自 `trusted.bank` 的有效指令，如果接收者信任该邮件并遵循其指令，他的银行账户可能会危险。这些情况可以通过使用 SPF（发送策略框架）来控制。

域名可以在特殊格式的 TXT 记录中发布其电子邮件服务器的 IP 地址。TXT 记录可能如下所示：

```
trusted.bank.com IN TXT "v=spf ip4:37.21.50.80 -all"
```

此记录指定仅允许一个 IP 地址为 `trusted.bank` 发送邮件。接收邮件服务器随后对邮件来源的 IP 地址进行额外检查。它们也知道发送者声称来自 `trusted.bank`，例如。接收邮件服务器可以查找 `trusted.bank` 的 TXT 记录，提取允许的 IP 地址，并与真实的 IP 地址进行比较。如果它们匹配，则极该邮件确实来自 `trusted.bank`。如果不匹配，则该邮件是伪造的，应该删除或进一步调查。

SPF 系统依赖于发送者和接收者之间的协作。发送者必须在 DNS 中发布 TXT 记录，接收者在收到邮件时必须检查记录。如果你想了解更多关于 SPF 的细节，请访问首页 http://spf.pofobox.com/。

# 日志

示例现在具备了最小功能 DNS 服务器的所有元素，但在进一步实验之前，额外的日志将让你看到 `named` 正在做什么。日志操作在 `named.conf` 的 `logging` 部分进行配置，各种选项在 BIND 9 ARM 中有详细描述。

# 使用 BIND 为真实域名提供 DNS

```
logging {

    channel custom {

        file "/tmp/named.log"; # 消息发送到这里

        print-time yes; # 打印时间戳

        print-category yes; # 打印消息类别

    }

    category config { custom; }; # 配置文件

    category notify { custom; }; # NOTIFY 消息

    category dnssec { custom; }; # TSIG 消息

    category general { custom; }; # 杂项

    category security { custom; }; # 安全消息

    category xfer-out { custom; }; # 区域传输

    category lame-ervers { custom; };

}
```

保留并经常检查日志尤为重要，因为语法错误会导致 BIND 拒绝该区域且不对该区域进行查询，从而导致你的服务器变得*lame*（意味着它不是本应负责的区域的权威服务器）。

# 解析器配置

在运行 BIND 之前的最后一步是设置本地解析器软件。这涉及配置 `/etc/hosts`、`/etc/resol.conf` 和 `/etc/nswitch.conf` 文件。

为了避免冗余的网络流量，Unix 解析器仍然使用名为 `/etc/hosts` 的类似 hosts 的文本文件来存储常用主机的名称和地址。该文件中的每行包含一个 IP 地址和主机的名称列表。对于任何希望独立于 DNS 解析的主机，请向此文件添加项。如果条目在 `/etc/hosts` 中，解析器就不必联系 DNS 服务器解析名称，从而减少了网络流量。

`/etc/resol.conf` 指定了首选域名服务器的地址以及用于解析未限定名称的域名列表。你使用如 `nameserver 1.2.3.4` 格式的行指定服务器（其中 1.2.3.4 是服务器的地址）。你可以使用多个 `nameserver` 行（通常最多三个）。你可以使用 `search` 行来指定用于搜索未限定名称的域名列表。

# 第 23 章 管理 DNS

诸如 `search example.com example.example` 的搜索行会导致解析器尝试解析未限定的 `xyz`，首先作为 `xyz.example.com` 解析，如果失败，则作为 `xyz.example.net` 解析。不要在搜索列表中过多域名，因为这会降低解析速度。

`/etc/nsswitch.conf` 中的 `hosts: files dns` 行会导致解析器在名称查找过程中在使用 DNS 之前咨询 `/etc/hosts`。这允许你通过对 `/etc/hosts` 进行临时更改来覆盖 DNS，这在网络测试期间特别有用。（旧版本的解析器可能要求在 `/etc/conf` 文件中指定 `hosts, bind` 顺序。）

# 运行 namederver 守护进程

最后！你现在可以通过 `/etc/rc.d/named start` 启动 `named`。你应该能在 syslog（或根据你设置的日志配置的其他位置）中看到类似于失败的消息。实现此操作的一种方法是使用 `tail` 命令监控日志；它会向下滚动文件中的更改。

```
# tail -f /var/log/messages

July 9 23:48:33 named[2605]: starting BIND 9.2.3 -u named
```
