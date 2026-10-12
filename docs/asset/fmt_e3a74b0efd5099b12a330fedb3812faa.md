
```
# $ cat /var/log/syslog
Apr 26 11:00:02 named[9301]: starting 9.7.8 + bind
Apr 26 11:00:02 named[9301]: found 1 CPU, using 1 worker thread
Apr 26 11:00:02 named[9301]: loading configuration from '/etc/bind/named.conf'
Apr 26 11:00:02 named[9301]: listening on IPv6 interfaces: ::53
Apr 26 11:00:02 named[9301]: listening on IPv4 interfaces: 127.0.0.1:53
Apr 26 11:00:02 named[9301]: listening on IPv4 interfaces: 192.168.0.10:53
Apr 26 11:00:02 named[9301]: command channel listening on 127.0.0.1:53
Apr 26 11:00:02 named[9301]: command channel listening on :1953
Apr 26 11:00:02 named[9301]: zone 127.in-addr.arpa/IN: loaded serial 1
Apr 26 11:00:02 named[9301]: zone 255.in-addr.arpa/IN: loaded serial 1
Apr 26 11:00:02 named[9301]: zone localhost/IN: loaded serial 1
Apr 26 11:00:02 named[9301]: running
```

当你创建或更新 DNS 信息时，可以使用 `dig` 来测试服务器是否按计划工作。`dig` 输出中最用的部分通常是答案部分，它提供了名称服务器对查询的回复：

```
$ dig example.com
```

| ANSWER SECTION: | 172800 IN | A | 192.0.32.10 |

| example.com | | |

前面的输出显示 `example.com` 有一个指向 `192.0.32.10` 的单个 A 记录。该记录的 TTL（告诉记录可以在缓存中保留多久）是 172,800 秒（两天）。你也可以使用 `dig` 查询其他记录类型，使用 `-t` 选项后跟想要查询的记录类型（`-t` 也适用于 `host`）：

```
$ dig -t ubuntu.com
```

| ANSWER SECTION: | 3587 IN | MX | 10 mx.canonical.com |

| ubuntu.com | | |

如果你查询一个不存在的域名，`dig` 将返回查询中存在的顶级域的 SOA 记录：

```
$ dig domaindoesexist.info
```

| AUTHORITY SECTION: | 900 IN SOA a0.info.afilias-nst.info. noc.afilias-nst.info. ... |

| info. | |

因为它告诉你最后一个查询正确的域，这些信息对于追踪故障很有用。

TSIG 如果两台服务器使用 TSIG（第 845 页）无法通信，请确认两台服务器上的时间是否相同。TSIG 身份验证机制取决于当前时间。两台服务器的时钟未同步，TSIG 将失败。考虑在服务器上设置 NTP（第 1163 页）以解决此问题。

# 设置不同类型的 DNS 服务器 851

你可能希望使用与你的安装环境唯一的 IP 地址。你可能想要更改 `notify` 语句的设置。

`named.conf`：此示例中的 `named.conf` 文件列出了 `named` 响应查询的 IP 地址，并设置了日志记录（下一页）。

```
$ /etc/bind/named.conf
options {
  directory "/etc/bind";
  // recursion NO;
  allow-query {127.0.0.1; 192.168.0.0/24};
}
zone "." IN {
  type hint;
  file "db.root";
}
zone "0.168.192.in-addr.arpa" IN {
  type master;
  file "named.conf.local";
  notify NO;
}
zone "sam.net" IN {
  type master;
  file "sam.net";
  notify NO;
}
logging {
  channel "misc" {
    file "/var/log/bind/misc.log" versions 4 size 4m;
    print-time YES;
    print-severity YES;
    print-category YES;
  }
  channel "query" {
    file "/var/log/bind/query.log" versions 4 size 4m;
    print-time YES;
    print-severity NO;
    print-category NO;
  }
  category default {
    "misc";
  }
  category queries {
    "query";
  }
}
```

`Options` 子句中的 `allow-query` 语句指定了服务器响应查询的系统 IP 地址。如果本地系统将查询服务器，必须将 `127.0.0.1` 包含在内。该服务器是 `sam.net` 区域的权威服务器；`sam.net` 的区域文件为 `/etc/bind/sam.net`。

# 852 第 24 章 DNS/BIND：跟踪域名和地址

日志通过 `Logging` 子句开启。日志记录与 `named` 消息是分开的，后者会发送到 `syslog`。前一个示例中的 `Logging` 子句打开了两个日志通道，将信息记录到 `/var/log/bind/query.log`，并确保如果其中任何一个增长到 4MB（`file` 语句中的 `size 4m`），它将通过在文件名后添加 .1 来重命名并启动新文件。在末尾，同名的日志会递增。任何超过 `versions` 关键字（示例中）指定的数量的日志将被删除。参见 `logrotate`（第 622 页）维护日志文件的另一种方法。

`print` 语句决定了记录信息的时间、严重程度和类别，每个设置为 YES 或 NO。`category` 决定信息如何记录到通道中。在前一个示例中，默认信息发送到 `misc` 通道，查询发送到 `query` 通道。更多选项请参阅 `named.conf` 映射页。

`named.conf`：对于版本大小（`named.local`）的原始值是 `0.168.192-inet-addra`（在引用文件 `named.local` 的 Zone 子句中指定）。在 SOA 和 NS 资源记录之后，第一条 PTR 资源记录分别将区域 `0.168.192-inet-addra` 中的地址 1 (`192.168.0.1`) 与 `ns.sam.net.`、`www.sam.net.`、`ftp.sam.net.` 对应。接下来的三条 PTR 记录将 `192.168.0.3` 与 `mark.sam.net.` 对应，`192.168.0.4` 与 `mail.sam.net.` 对应。

```
$ cat /etc/bind/named.conf.local
$3D
0 IN SOA ns.sam.net. @ms01.com. (
2010110501 : serial
8h : refresh
2h : retry
4w : expire
10d) : minimum

1 IN NS ns.sam.net.
1 IN PTR www.sam.net.
1 IN PTR ftp.sam.net.
1 IN PTR mark.sam.net.
4 IN PTR mail.sam.net.
6 IN PTR ns.sam.net.
```

`sam.net`：区域记录本身利用了许多 BIND 功能，并包含了 TXT（第 830 页）、CNAME（第 828 页）和 MX（第 828 页）资源记录。当你查询资源记录时，`named` 会返回 TXT 记录以及你请求的记录。两个 NS 记录中的第一个指定了一个未限定名称 (`ns`)，BIND 在其后追加区域名 (`sam.net`)，从而产生 FDN `ns.sam.net`。第二个名称服务器使用 FDN 名称指定，BIND 不会更改该名称。MX 记录以类似的方式指定邮件服务器，并在数据字段开头包含一个优先级数字，数字越小表示越是首选服务器。

# 设置不同类型的 DNS 服务器

| $ cat sam.net |

| :--- |

| zone "sam.net" |
