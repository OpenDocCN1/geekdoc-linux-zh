
```bash
# cat /etc/sysconfig/named

options {
  listen-query 127.0.0.1; 192.168.0.201;
  allow-query { 127.0.0.1; 192.168.0.0/24 };
  allow-recursion { 127.0.0.1; 192.168.0.0/24 };
  allow-transfer { 192.168.0.0/24 };
  directory "/var/named";
  dump-file "/var/named/dump.db";
  statistics-file "/var/named/stats.txt";
  mem-file "/var/named/mem.txt";
  pid-file "/var/run/named.pid";
  notify yes;
}

zone example.com {
  type master;
  file "example.zone";
  allow-update { any };
};

zone 192.168.0.in-arpa {
  type master;
  file "revzone";
  allow-update { any };
};

zone "." {
  type hint;
  file "root";
};

zone localhost {
  type master;
  file "localhost.zone";
  allow-update { none };
};

zone 127.0.0.in-arpa {
  type master;
  file "local";
  allow-update { none };
};
```

```bash
dump-file "/var/named/data/cache_dump.db";
statistics-file "/var/named/data/named_stats.txt";
memstatistics-file "/var/named/data/named_mem_stats.txt";
query-source port 53 {
 allow-query { localhost; };
}
logging {
  channel default_debug {
    file "data/named.run";
    severity dynamic;
  };
}
view localhost_resolver {
  match-clients { localhost; };
  match-destinations { localhost; };
recursion yes;
  syslog "/etc/named.rfc1912.zones";
}
```

与 `named.conf` 文件类似，该文件也包含 `options` 语句，可以在其中定义全局选项。`options` 内的 `query-source` 指令指定用于查询其他 DNS 服务器的端口号。`logging` 语句定义了日志相关的设置。`view localhost_resolver` 语句将 localhost 设置为用于查找查询的缓存 DNS 服务器。

# The localhost.zone 正向区域文件

每台服务器都是网络 127.0.0 的权威服务器，并拥有 `localhost.zone` 区域文件。该文件包含了将 127.0.0.1 映射到回环地址（localhost）名称的资源记录。句话句话，此文件包含指向 localhost 的指针。在该区域发生更改后，你需要重新加载 `named` 进程。

```
# cat /var/named/localhost.zone
```

```
$TTL 86400
@ IN SOA @ root {
	42 ; serial (d. adams)
	3H ; refresh
	15M ; retry
	1W ; expiry
	1D ) ; minimum
}

@ IN NS @
IN A 127.0.0.1
```

该文件中有多个条目，被称为资源记录。表 22-3 解释了它们。

| 记录 | 说明 |
| :--- | :--- |
| `$TTL` | Time Live（生存时间）是区域内信息被认为有效的时间段。默认值为 86,400 秒（24 小时）。 |
| `@` | 在区域语句中指定 `named.conf` 中定义的区域起始点。 |
| 记录 | 说明 |
| :--- | :--- |
| `IN` | 指定类类型，以互联网区域为默认值。另外两种类型是 HS（Heesoid 区域）和 CHAOS（CHAOSnet 区域）。 |
| `SOA` | Start Of Authority（权威起始）。标记域的开始。它标识了负责 `named.conf` 中指定的域的完全域名（FDN）的 DNS 服务器，其值如下：<br>Serial（序列号）：区域版本。每次刷新文件时该数字递增。从服务器查看此数字并与主服务器进行比较。如果数字更高，则传输更新的文件。<br>Refresh（刷新）：服务器刷新主服务器的间隔（秒）。<br>Retry（重试）：上次刷新失败后，从服务器从主服务器获取更新的间隔（秒）。<br>Expire（过期）：从服务器可以使用区域数据的过期时长（秒）。<br>Minimum（最小）：保留条目的最小时间（秒）。 |
| `NS` | 名称服务器。列出具有相应权威性的 DNS 记录和域。 |
| `A` | 为系统分配 IP 地址。 |
| `CNAME` | 规范名称。系统的完全限定域名（FQDN）。 |
| `PTR` | IP 地址到名称的映射。 |
| `MX` | 邮件交换器。当向互联网目标发送邮件时，如果目标系统不可用，则指定的尝试系统列表。 |

# 表 22-3 资源记录说明

## named.local 反向区域文件

`localhost.zone` 有一个对应的区域文件 `named.local`，包含 127.0.0.0 的反向查找信息。在该文件更改后你需要重新加载 `named` 进程。该文件的默认内容如下，资源记录描述在表 22-3 中。

```
# cat /var/named/named.local
$TTL 86400
@ IN SOA @ root.localhost.
    199702270 ; Serial
    28800 ; Refresh
    14400 ; Retry
    3600000 ; Expire
    86400 ) ; Minimum

IN NS localhost.
1 PTR localhost.
```

# named.ca 区域文件

`named.ca` 文件列出了根域（root domain）的服务器。有 13 台权威 DNS 服务器，当本地 DNS 服务器无法解析主机查询时，会查询其中之一。每个面向互联网的 DNS 服务器都有该文件的副本。以下是该文件的默认内容：
