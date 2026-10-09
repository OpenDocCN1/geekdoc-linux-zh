
`Options` 部分的两行指示 `named` 在本地系统的端口 53（默认 `named` 端口）上监听传入的查询。`directory` 语句指定文件中所有相对路径所在的目录。具体来说，`rfc1912.zones` Zones 中命名的文件位于 `/var/named` 目录。如果你在 chroot jail 中运行 `named`，此目录位于 `/var/named:chroot` (750)。文件还指定了 `dump-file`（缓存 dump）、`statistics-file`（统计文件）和 `memstatistics-file`（内存统计文件）的位置。`query-source` 语句指定服务器发出查询的（地址）端口。`allow-query` 语句指定允许查询服务器的 IP 地址。此文件指定 `localhost` 可以查询服务器。

# 日志部分（Logging section）

`Logging` 部分导致调试消息被发送到 `data/named.run`。欲更多信息请参见第 753 页的 `Logging`。

# 视图部分（View section）

单独的 `View` 语句指定此服务器响应来自本地系统（`localhost`）的查询并执行递归查询。`include` 语句将 `/etc/named.rfc1912.zones` 文件（下一节讨论）如同它存在于 `View` 部分一样引入。欲更多信息请参见第 757 页的“View sections”。

# `named.rfc1912.zones`: 区域配置文件 (FEDORA)

如上一节所述，`named.caching-nameserver.conf` 文件通过在 `include` 语句中命名引入 `/etc/named.rfc1912.zones` 文件：

```
# cat /etc/named.rfc1912.zones
// named.rfc1912.zones
//
// 由 Red Hat bind-config 包提供
//
// 根据 RFC 1912 第 4.1 节推荐的
// localhost TLD 和地址区域的 ISC Bind named 配置
//
zone * IN {
  type hint;
  file "named.ca";
};
```

```
zone "localdomain" IN {
  type master;
  file "localdomain.zone";
  allow-update { none; };
}
```

```
zone "localhost" IN {
  type master;
  file "localhost.zone";
  allow-update { none; };
}
```

```
zone "0.0.127.in-addr.arpa" IN {
  type master;
  file "named.local";
  allow-update { none; };
}
```

```
zone "0.0.0.0.0.0.0.0.0.0.ip6.arpa" IN {
  type master;
  file "named.ip6.local";
  allow-update { none; };
}
```

```
zone "255.in-addr.arpa" IN {
  type master;
  file "named.broadcast";
  allow-update { none; };
}
```

```
zone "0.in-addr.arpa" IN {
  type master;
  file "named.zero";
  allow-update { none; };
}
```

## 区域部分 (Zone sections)

此文件包含七个区域部分，每个部分都有一个 `allow-update` 语句，指定不允许对区域进行动态更新。此文件中的所有文件名相对于 `named.caching-nameserver.conf` 中 `Options` 部分的目录语句。

- `*` (区域的名称为一个点。) 提示区域（hint zone）。指定当服务器启动或不知道应该查询哪个服务器时，它应该在 `/var/named.ca`（ca 代表缓存）中查找根域名的权威服务器的地址。

- `localhost` 指定 `localhost.localhost` 指向 `127.0.0.1`，防止本地服务器就此信息向上游查询查询。

- `localhost` 在本地系统上设置普通服务器。

- `0.0.127.in-addr.arpa` 设置 IPv4 反向域名解析。

- `0.0::0.ip6.arpa` 指定 IPv6 反向域名解析。

- `255.in-addr.arpa` 指定以 255 开头的 IP 地址的反向查询将由本地服务器处理，防止本地服务器就此信息向上游查询。

- `0.in-addr.arpa` 指定以 0 开头的 IP 地址的反向查询将由本地服务器处理，防止本地服务器就此信息向上游查询。

## 区域文件 (Zone Files)

`/var/named` 下有七个文件，每个文件对应于名为 `named.rfc1912.zones` 的区域部分。本节描述了其中三个区域文件。

### 根区域：`named.ca`

提示区域文件 `named.ca` 是 `ftp.internic.net/domain/named.cache` 的副本，该文件不会频繁变动。`named.ca` 文件指定了根域的权威服务器。DNS 服务器从此文件初始化缓存，并能根据这些信息确定任何域名的权威服务器。

根区域仅供回答递归查询的服务器需要。如果一个服务器响应递归查询，它需要执行从根域开始的一的一系列迭代查询。如果没有根提示文件，它将不知道根域服务器的位置。

### `/var/named/named.ca`

- 此文件包含了初始化互联网域名缓存所需的根名称服务器信息（例如，在 BIND 域名服务器的“cache <file>”配置文件中引用此文件）。

此文件可以通过 InterNIC 在匿名 FTP `FTP.INTERNIC.NET` 上的 `domain/named.cache` 获取 --

最后更新：2004年1月29日 根区域版本：2004012900

曾为 `NS.INTERNIC.NET`

```
360000 IN NS A.ROOT-SERVERS.NET.
A.ROOT-SERVERS.NET. 360000 A 198.41.0.4
```

曾为 `NS1.ISI.EDU`

```
360000 NS B.ROOT-SERVERS.NET.
B.ROOT-SERVERS.NET. 360000 A 192.228.79.201
```

曾为 `C.PSI.NET`

### `localhost.zone`

`localhost.zone` 区域定义了 `localhost` 区域，即本地系统上的普通服务器。它以 `$TTL` 指令开头，并包含三个资源记录：`SOA`、`NS` 和 `A`。后续文件中的 `$TTL` 指令指定此文件中指定的资源记录的默认生存时间为 86400 秒（24 小时）：

```
# cat /var/named/localhost.zone
$TTL 86400
@ @ SOA @ root ( serial (d. adams)
@ IN SOA 42 : refresh
3H : retry
15M : expiry
1W : minimum
1D )

IN NS @
IN A 127.0.0.1
IN AAAA ::1
```

如前所述，`SOA` 资源记录开头的 `@ @` 代表源（节点名称），即 `localhost`。前一个文件中的最后三行是 `NS` 记录，它指定了 `localhost` (@) 区域的名称服务器；`A` 资源记录指定了主机的 IPv4 地址为 `127.0.0.1`；`AAAA` 资源记录指定了主机的 IPv6 地址为 `::1`。由于这些记录有空白字段，每条记录都从前一个资源记录 `@` 继承该值。

### `named.local`

`named.local` 区域文件提供了关于 `0.0.127.in-addr.arpa` 反向查找区域的信息。它与 `localhost` 区域遵循相同的模式，但它有一个 `PTR` 记录，提供了与 IP 地址关联的名称。`PTR` 记录指定了将区域 (`0.0.127.in-addr.arpa`) 中地址为 1 的系统等同于名称 `localhost`，其 IP 地址为 `127.0.0.1`：

```
$ cat /var/named/named.local
$TTL 86400
@ @ SOA localhost, root
199702700 Serial
28800 Refresh
```

### `named.conf` 配置文件

其他区域文件执行与区域部分类似的功能。一旦启动了 `named`，您可以使用“故障排除”下描述的 `rndc` 测试来确保服务器正常工作。`named.conf` 文件包含与 `named-caching-nameserver.conf` 相同的区域。`named.conf` 中 `Options` 部分的注释带有日期。

使用 512 位的偏移量创建一个密钥。`dnssec-keygen` 工具 BIND 会生成此密钥。以下命令使用 MD5（一种单向哈希函数，第 1046 页）生成一个 512 位密钥：

```bash
$ /usr/sbin/dnssec-keygen -a hmac-md5 -b 512 -HOST keyname
keyname.+157+47586
```

在上述命令中，将 `keyname` 替换为唯一且有意义的内容。此命令会创建一个类似于 `keyname.+157+47586.private` 的文件名，其中 `keyname` 被替换为密钥名称，`.+157` 是所使用的算法，而 `+47586` 是文件名的一部分。如果你再次运行该命令，哈希值将会不同。密钥不会直接使用。使用它配合文件名参数，以显示密钥以及你在下一步中所需的信息：

```bash
$ cat Keyname.+157+47586.private
Private-key format: v1.2
Algorithm: 157 (HMAC-MD5)
Key: uNPDouqVwR7vo/zFyjkqKbQhcTd6Prm...
```

## 使用共享密钥

下一步是通过在两台服务器的 `/etc/named.conf` 文件中插入密钥代码来告知命名服务器。这是 `named.conf` 中的一个顶级部分，请插入以下 `Options` 部分：

```bind
key keyname {
    algorithm "hmac-md5";
    nsecret "uNPDouqVwR7vo/zFyjkqKbQhcTd6Prm...";
}
```

`keyname` 是你创建的密钥名称。`algorithm` 是出现在输出格式括号内的字符串。`secret` 是前述输出中 `Key:` 之后的字符串。你必须将每个字符串包含在双引号内。在复制密钥时要小心；它很长，不要将其分成多行。

由于密钥名称是唯一的，你可以在 `named.conf` 中插入任意数量的密钥部分。为了保护密钥，请确保 `root` 以外的用户无法读取它：确保 `root` 拥有访问权限，或者将密钥放在只有 `root` 才能读取的文件中，并使用 `include` 语句将其引入 `named.conf`。一旦两端都知道了密钥，请使用 `named.conf` 中的 `server` 语句告诉它们使用它：

```bind
server 1.2.3.4 {
    1.2.3.4 是另一台服务器的 IP 地址。
    keys { "keyname";
}
```

每台服务器都必须有一个 `server` 部分，包含另一台服务器的 IP 地址。现在，只有当它们使用密钥相互进行身份验证时，服务器才会相互通信。

## 在 chroot 中运行 BIND

为了提高安全性，你可以在 chroot 狱中运行 BIND。有关设置 chroot 狱的优势和方法的信息，请参阅第 428 页。关于 BIND 和 SELinux 的信息，请参阅第 732 页的注意事项。`bind-chroot` 包配置 BIND 在 chroot 狱中运行，它创建了一个目录 `/var/named`，用以取代所有 BIND 文件的根目录 (`/`)。安装此软件包后，所有的 BIND 文件都位于狱中，且其中使用的文件名是指向 chroot 中文件的符号链接。

```bash
# ls -l /var/named/etc
named.caching.conf -> /var/named/chroot/etc/named.c.conf
rfc1912.zones -> /var/named/chroot/etc/rfc1912.zones
/var/named:
total 5
data
localdomain.zone -> /var/named/chroot/var/named/localdomain.zone
localhost.zone -> /var/named/chroot/var/named/localhost.zone
named.broadcast -> /var/named/chroot/var/named/named.broadcast
named.ca -> /var/named/chroot/var/named/named.ca
named.ip6.local -> /var/named/chroot/var/named/named.ip6.local
named.local -> /var/named/chroot/var/named/named.local
named.zero -> /var/named/chroot/var/named/named.zero
```

安装 `bind-chroot` 包后，`ROOTDIR` 变量在 `/etc/sysconfig/named` 文件中被设置为 `/var/named/chroot`，该文件由 `named` 初始化脚本执行。

## 故障排除

当启动 DNS 缓存时，`var/log/messages` 文件包含类似下方的行。其他类型的 DNS 服务器也会显示类似的消息。

```text
# cat /var/log/messages
18:45:18 named[10003]: starting BIND 9.3.2 -u named -t /var/named/chroot
18:45:18 named[10003]: found 1 CPU, using 1 worker thread
18:45:18 named[10003]: loading configuration from '/etc/named.conf'
18:45:18 named[10003]: listening on IPv6 interface ::53
18:45:18 named[10003]: listening on IPv4 interface lo, 127.0.0.1:53
18:45:18 named[10003]: command channel listening on :953
18:45:18 named[10003]: command channel listening on :953
18:45:18 named[10003]: zone 0.in-addr.arpa/localhost_resolver: loaded serial 42
18:45:18 named[10003]: zone 255.in-addr.arpa/localhost_resolver: loaded serial 42
18:45:18 named[10003]: zone 0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.0.: loaded serial 1997022700
18:45:18 named[10003]: 0.0.ip6.arpa/localhost_resolver: loaded serial 1997022700
18:45:18 named[10003]: zone localdomain/localhost_resolver: loaded serial 42
18:45:18 named[10003]: zone localhost/localhost_resolver: loaded serial 42
18:45:18 named[10003]: running
```

带有 `status` 参数时，`named` 初始化脚本会显示有用信息：

```bash
$ /sbin/service named status
number of zones: 6
debug level: 0
xformers running: 0
xformers deferred: 0
soa queries: 0
query logging is OFF
recursive clients: 0/1000
tcp clients: 0/1000
server is up and running
```

当你创建或更新 DNS 时，可以使用 `dig` 来托管或测试服务器是否按照你的预期工作。`dig` 输出的大部分通常是答案，提供了命名服务器对你查询的回复：

```bash
$ dig example.com

:: ANSWER SECTION:
example.com.      172.16.0.1
```

```json
:
  category queries {
    "query";
  }
);
```

`Options` 部分中的 `allow-query` 语句指定了响应查询的系统 IP 地址。如果本地系统要查询服务器，则必须将其包含在 `127.0.0.1` 中。该权威权威区域是 `sam.net`；`sam.net` 的文件是 `/var/named/sam.net`。

# 日志
