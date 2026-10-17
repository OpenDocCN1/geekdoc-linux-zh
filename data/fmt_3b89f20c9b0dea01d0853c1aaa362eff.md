
该工具分别创建两个带有 `.key` 和 `.private` 扩展的文件。`.private` 文件中的 `Key:` 行告诉了 `rndc` 和 `named` 需要共享的密钥（`mkDd2F1HMFe1Jqx1/z4cfw=`）。当我们有了它后，就可以设置一个非常简单的 `/etc/rndc.conf`：

```
/etc/rndc.conf
-------
# 与名称服务器 "localhost" 通信时使用名为 "rndc" 的键
server localhost { 
    key               rndc;
}

# 这里是关于名为 "rndc" 的键的细节
key rndc {
    algorithm           HMAC-MD5;
    secret              "mkDd2F1HMFe1Jqx1/z4cfw=";
}

# 默认
options {
    default-server     localhost;
    default-key        rndc;
}
```

该文件需要包含三个部分：

- `server` 部分定义了一个名称服务器（localhost），并指定了与其通信时使用的键（rndc）。
- `key` 部分包含了一些关于键的细节，由 `dnssec-keygen` 生成。当我们设置 `named` 时，我们需要告诉它关于键的相同信息，以便它能够验证 `rndc` 发出的请求。
- `options` 部分设置了合理的默认值（因为文件可能会列出多个服务器和键）。

如果需要，`rndc(8)` 和 `rndc.conf(5)` 帮助页包含更多信息。

## named.conf

接下来你必须配置 `named` 本身。它的单一配置文件（`/etc/named.conf`）语法与 `rndc.conf` 非常相似：此部分仅描述了对于配置功能性名称服务器至关重要的一小部分配置指令。如需更详细的参考，请参阅 BIND 9 ARM（管理员参考手册）；它随 BIND 一起发布，Red Hat 7.3 将安装在 `/usr/share/doc/bind-9.2.1/arm/` 下。

`named.conf` 文件中的 `options` 和 `named` 部分是绝对必要的。`options` 部分必须告诉 `named` 区域文件存放的位置，并且 `named` 必须知道在哪里找到根区域（`*`）。我们还设置了一个 `controls` 部分，允许接受来自 `rndc` 的经过验证命令。由于客户端（特别是 `nslookup`）依赖于解析名称服务器的 IP，我们还设置了 `0.0.127.in-addr.arpa` 反向区域。

我们从类似这样的配置文件开始：

```
/etc/named.conf
options {
    # 这里是存放区域文件的地方
    directory "/var/named";
}

# 允许运行在 localhost 上的 rndc 向我们发送命令
controls {
    inet 127.0.0.1 {
        allow { 127.0.0.1; }
        keys { rndc };
    }
}

# 与 rndc.conf 中指定的相同信息
key rndc {
    algorithm hmac-md5;
    secret "mKKd2FiHMFe1JQ1/z4cfw==";
}

# 关于根区域的信息
zone ".*" {
    type hint;
    file "root.hints";
}

# 许多软件依赖于能够解析 127.0.0.1
zone "0.0.127.in-addr.arpa" {
    type master;
    file "rev/127.0.0.0";
}
```

`options` 部分是我们指定 `named` 应该查找区域文件的目录的地方（如文件中其他部分命名的）。你将在本章随后的示例中学习如何使用其他选项。

接下来，我们指示 `named` 接受来自经过验证的 `rndc` 的命令。我们添加了一个 `key` 部分，与那个 `rndc.conf` 完全相同，以及一个 `controls` 部分，说明 `rndc` 将从 `localhost` 连接并使用指定的键。（你可以在 `allow` 列表中指定多个 IP 地址，或者像“安全”章节中描述的那样使用访问控制列表。）

`*` 区域告诉 `named` 关于 `root.hints` 文件中带有名称和地址的根服务器的信息。这些信息决定了最初查询哪一个根服务器（该决定通常会根据服务器的响应进行频繁修订）。虽然可以通过 FTP 获取提示文件，但推荐的、对网络友好的保持其同步的方法是使用 `dig`。我们向一个根名称服务器（哪一个都行）请求 `.` 的 NS 记录，并使用 `dig` 的输出：

```
/var/named/root.hints

# dig @j.root-servers.net > /var/named/root.hints
# cat /var/named/root.hints
| << dig 8.2 << @root-servers.net . ns
| (1 server found)
| ;; res options: init recurs defnam dnsrch
| ;; get answer:
| ;; >>HEADER<< opcode: QUERY, status: NOERROR, id: 6
| ;; flags: ra rr rd; QUERY: 1, ANSWER: 13, AUTHORITY: 0, ADDITIONAL: 13
| ;; QUERY SECTION: | ;; type = NS, class = IN

| ;; ANSWER SECTION:
| 60 IN NS H.ROOT-SERVERS.NET.
| 60 IN NS C.ROOT-SERVERS.NET.
| 60 IN NS G.ROOT-SERVERS.NET.
| 60 IN NS F.ROOT-SERVERS.NET.
| 60 IN NS B.ROOT-SERVERS.NET.
| 60 IN NS J.ROOT-SERVERS.NET.
| 60 IN NS K.ROOT-SERVERS.NET.
| 60 IN NS L.ROOT-SERVERS.NET.
| 60 IN NS M.ROOT-SERVERS.NET.
| 60 IN NS I.ROOT-SERVERS.NET.
| 60 IN NS E.ROOT-SERVERS.NET.
| 60 IN NS D.ROOT-SERVERS.NET.
| 60 IN NS A.ROOT-SERVERS.NET.
```

```
/var/named/root.hints

# dig @j.root-servers.net > /var/named/root.hints
# cat /var/named/root.hints
| << dig 8.2 << @root-servers.net . ns
| (1 server found)
| ;; res options: init recurs defnam dnsrch
| ;; get answer:
| ;; >>HEADER<< opcode: QUERY, status: NOERROR, id: 6
| ;; flags: ra rr rd; QUERY: 1, ANSWER: 13, AUTHORITY: 0, ADDITIONAL: 13
| ;; QUERY SECTION: | ;; type = NS, class = IN

| ;; ANSWER SECTION:
| 60 IN NS H.ROOT-SERVERS.NET.
| 60 IN NS C.ROOT-SERVERS.NET.
| 60 IN NS G.ROOT-SERVERS.NET.
| 60 IN NS F.ROOT-SERVERS.NET.
| 60 IN NS B.ROOT-SERVERS.NET.
| 60 IN NS J.ROOT-SERVERS.NET.
| 60 IN NS K.ROOT-SERVERS.NET.
| 60 IN NS L.ROOT-SERVERS.NET.
| 60 IN NS M.ROOT-SERVERS.NET.
| 60 IN NS I.ROOT-SERVERS.NET.
| 60 IN NS E.ROOT-SERVERS.NET.
| 60 IN NS D.ROOT-SERVERS.NET.
| 60 IN NS A.ROOT-SERVERS.NET.
```

`options` 部分是我们指定 `named` 应该查找区域文件的目录的地方（如文件中其他部分命名的）。你将在本章随后的示例中学习如何使用其他选项。

接下来，我们指示 `named` 接受来自经过验证的 `rndc` 的命令。我们添加了一个 `key` 部分，与那个 `rndc.conf` 完全相同，以及一个 `controls` 部分，说明 `rndc` 将从 `localhost` 连接并使用指定的键。（你可以在 `allow` 列表中指定多个 IP 地址，或者像“安全”章节中描述的那样使用访问控制列表。）

注释（注意：区域文件的注释语法与 `named.conf` 中的注释不同），字段包括序列号（serial）、刷新间隔（refresh）、重试时间（retry）、过期（expire）、周期（period）和最小 TTL。

序列号是 32 位整数，可以存储 0 到 4,294,967,295 之间的值。每当区域数据发生变化时，必须增加序列号。此更改作为向从服务器发送的信号，告知它们需要再次传输区域内容。惯例是使用 YYYYMMDD 格式分配序列号：即更改的日期加上两位数的修订号（例如 2020190101）。对于同一天内的更改，你只需增加修订号即可。（这合理地假设你一天内对一个区域的修改不超过 99 次。）到了第二天，数据发生变化后，修订号将从 01 开始计数。

刷新间隔指定了从服务器检查数据是否已更新的频率。该值被设置为 24 小时，但如果区域频繁变化，则该值应该更小。（如果主服务器支持 DNS NOTIFY 机制，从服务器可以更早地重新加载区域。大多数 DNS 软件都支持。）重试时间与从服务器在刷新时间过后仍无法连接主服务器的情况有关。它指定了在再次尝试之前应等待多久。（设置为两小时。）

如果从服务器在整个期间持续无法连接到主服务器（通常是因为灾难性故障），它将丢弃已有的区域数据并停止响应查询。因此，过期周期应该足够长，以便允许主服务器恢复。事实已反复证明，一或两周的值太短了。一千（约六周）被认为是一个良好的默认值。

正如你之前读到的，每个资源记录（RR）都有一个 TTL，它指定了在必须咨询数据源之前数据可以缓存多久。如果 RR 定义没有显式指定 TTL，则使用默认值（由 `$TTL` 指令设置）。这允许 RR 根据需要覆盖默认 TTL。

SOA TTL 是 SOA 记录中的最后一个数值字段，用于确定负向响应（NXDOMAIN）应该被缓存多久。（也就是说，如果查询导致 NXDOMAIN 响应，则该响应的缓存时间将与示的由 SOA TTL 指定的时间一样长。）旧版本的 BIND 会将 SOA 最小 TTL 设置为 B，但现在不再这样做。为了缓存友好，建议使用 2 天的默认 TTL 和 1 小时的 SOA TTL。

所使用的值对于不经常变化的区域是非常典型的默认值。对于具有不同要求的区域，你可能需要进行调整；在这种情况下，建议阅读网站 http://www.ripe.net/docs/ripe-203.html。

# 区域文件的其他记录

区域文件中的接下来两行创建 NS 和 PTR 记录。NS 记录没有指定显式名称，因此它使用上一个，即 SOA 记录的名称。因此，0.0.127.in-addr.arpa 的名称服务器被定义为 localhost。

PTR 记录的名称为 1，它变为 1.0.0.127.in-addr.arpa（这是你将地址 127.0.0.1 写为 DNS 名称的方式）。在经过限定后，PTR 记录名称 1 变为 localhost。（当我们稍后配置我们的名称服务器成为真实域名的权威服务器时，你会看到众多 RR 类型中的某些。）

# 日志

我们现在已经拥有了最小运行的 DNS 服务器的所有元素，但在进一步实验之前，一些额外的日志将让我们能够清楚地看到 named 正在做什么。日志选项配置在 named.conf 的一个 logging 部分中，各种选项在 BIND 9 ARM 中有详细描述。

所有日志消息都发送到一个或多个通道——每个通道都可以将消息写入 syslog、普通文件、stderr 或 null（写入 null 的日志消息会被丢弃）。存在不同的消息类别，例如解析配置文件时产生的消息、由 OS 错误引起消息等。你的日志语句必须定义某些通道，并将它们与你想要看到的消息类别关联。

BIND 日志非常灵活，但也很复杂，因此我们只检查一个简单的日志配置。

在 named.conf 中添加以下内容将设置一个名为 custom 的通道，它将带有时间戳的消息写入文件，并将列出的类别的消息发送到此处。

```
logging {
  channel custom {
    file "/tmp/named.log"; # 消息发送的位置。
    print-time yes;         # 时间戳
    print-category yes;     # 打印消息类别？
  }

  category config { custom; }; # 配置文件
  category notify { custom; }; # NOTIFY 消息
  category dnssec { custom; }; # TSIG 消息
  category general { custom; }; # 杂项
  category security { custom; }; # 安全消息
  category xfer-out { custom; }; # 区域传输
  category lame-servers { custom; };
}
```

# 使用 BIND 配置名称服务器

> 注意

保留并频繁检查你的日志尤为重要，因为语法错误经常会导致 BIND 拒绝一个区域且不对其响应查询，导致你的服务器变成“跛脚服务器”（lame）（即对于它本应权威的区域不再具有权威）。

# 解析器配置

在运行 BIND 之前的最后一步是设置本地解析器软件。这涉及配置 `/etc/hosts`、`/etc/resol.conf` 和 `/etc/nsswitch.conf` 文件。

为了避免产生流量，Unix 解析器使用类似 hosts 的文件来存储名称。`/etc/hosts` 中的每行都包含一个 IP 地址和名称列表。通过向 `/etc/hosts` 添加条目可以覆盖默认 DNS。像 example.com 这样的 search 字段会使解析器首先尝试解析 example.com，如果失败，则通过 `/etc/resol.conf` 指定的服务器进行解析。

# 运行守护进程

最后！你现在可以使用 `/etc/init.d/start` 启动 BIND。你应该会在 syslog（或你设置的日志）中看到类似的消息。一种方法是使用 `tail` 命令监控日志。

```
# tail -f /var/log/messages
May 9 23:48:33 named: starting -u
May 9 23:48:33 named: loading configuration from '/etc/named.conf
May 9 23:48:33 named: no IPv6 found
May 9 23:48:33 named: listening on IPv4 lo, 127.0.0.1
May 9 23:48:33 named: listening on IPv4 eth0, 192.168.2.1
May 9 23:48:33 named: zone 0.0.127.in-addr.arpa/IN: loaded 19970220
May 9 23:48:33 named: zone localhost/IN: loaded 42
May 9 23:48:33 named: running
```

你可以使用 `rndc` 与此 named 实例交互。不带参数运行 `rndc` 会显示可用命令列表，包括重新加载或刷新区域、将统计数据和数据库写入磁盘、切换查询日志以及停止服务器。（遗憾的是，`rndc` 没有实现早期版本 BIND 提供的 ndc 控制程序支持的所有命令。）

你应该能够本地解析 1.0.0.127.in-addr.arpa（尝试 `dig @localhost +nore`）以及通过递归解析其他名称。如果你不能，说明出了问题，你应该在继续之前阅读后面的“故障排除”章节来诊断并纠正你的问题。记住查看日志！

# 为真实域名提供 DNS 服务
