
```text
[root@redhat ~]# dig @192.168.10.10 version.bind txt chaos
; <<>> DiG 8.2 <<>> @192.168.10.10 version.bind txt chaos
(1 server found)
; res options: init recurs defname dnsrch
; got answer:
; >>HEADER<< opcode: QUERY, status: SERRROR, id: 6
; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0,
ADDITIONAL: 0
; QUERY SECTION:
;  version.bind, type = TXT, class = CHAOS
;
; ANSWER SECTION:
VERSION.BIND.  0S CHAOS TXT   "8.2.2-P7"

; Total query time: 20 msec
; FROM: redhat.the-nashes.net to SERVER: 192.168.10.10
; WHEN: Sat Dec  9 15:40:19 2000
; MSG SIZE sent: 30 rcvd: 63
```

此示例显示一个运行 BIND v8.2.2-P7 的服务器。BIND 守护进程称为 `named`。较旧的 v4 使用了与较新版本不同的配置语法。在 BIND 套件中，除了 `named` 之外，还有示例配置文件和解析器库，允许客户端应用程序执行查询。

### 配置 BIND v8

BIND v8 使用 `named.conf` 配置文件，以及几个持有地址映射信息的区域文件。`named.conf` 的格式由一系列语句组成，每个语句以分号结束。有时使用花括号将行分组。虽然语法易于阅读和使用，但误放的分号可能导致严重问题，有时很难追踪。区域文件是资源记录列表，是 DNS 中的实际信息。区域是服务器负责的 DNS 命名空间部分。这与域不同，因为一个区域可能包含不止一个域或子域。可以设置多个 DNS 服务器作为主服务器的备份或次要服务器。次要服务器从主服务器拉取信息，这被称为区域传输。以下是一个 `named.conf` 文件的示例。

### BIND v8 配置

BIND v8 使用 `named.conf` 配置文件。

```
options {
    directory "/";
    named-xfer "/named-xfer";

    //directory "/var/named";
    //named-xfer "/var/named/named-xfer";

    // Don't reveal BIND version
    version "";
};

logging {
    category lame-servers { null; };
    category cname { null; };
};

// ndc control socket
controls {
    unix "/var/run/ndc" perm 0600 owner 0 group 0;
};

// Standard zones
//

zone "the-nashes.net" IN {
    type master;
    file "db.the-nashes";
};

zone "localhost" IN {
    type master;
    file "named.localhost";
    allow-transfer { localhost; };
};

zone "0.0.127.in-addr.arpa" IN {
    type master;
    file "named.loopback";
    allow-transfer { localhost; };
};

zone "." IN {
    type hint;
    file "named.root";
};
```

该配置文件设置了 `nashes.net` 的域名以及 `otherzone.net` 的从域名。从域名是指 DNS 服务器从另一台服务器获取区域文件的域名。从服务器保存信息的只读副本。

### named.conf 语句

接下来的章节将介绍可以在 `named.conf` 文件中使用的语句。

#### include 语句

`include` 语句引入另一个配置文件，将其添加到主 `named.conf` 中。这对于拥有部门级控制的大型站点非常有用。每个部门可以在服务器上的文件中维护自己的 DNS 信息，而该语句则将这些信息拉取到 DNS 配置中。语法如下：

```
include "path"
```

#### options 语句

`options` 语句指定全局配置设置。BIND v8 中有超过 50 种可能的 options 设置。语法如下：

```
options {
    option_statement;
    option_statement;
    ...
}
```

表 16-26 列出了一些常见的 `options` 语句。许多 `options` 语句使用地址列表进行安全控制。以下是一些此类列表的示例。

```
{ 192.168.10/24; 192.168.12/24; 10.10/16; 127.0.0.1}
{ ! 192.168.10.15; 192.168.10/24 }
```

第一个示例展示了几个网络地址和一个单主机（`localhost`）。第二个示例包含一个被拒绝的主机（用 `!` 指定）和一个被允许的网络。第二个示例中的顺序非常重要。BIND 在找到第一个匹配项后就会停止搜索。如果顺序颠倒，地址 `192.168.10.15` 将匹配 `192.168.10/24`，BIND 将永远不会到达限制该地址的条目。

**表 16-26 Options 语句**

| 语句 | 功能 |
| :--- | :--- |
| `version "string";` | 更改向客户端报告的版本号。有些人认为这样更安全。 |
| `directory "path";` | 服务器工作目录的完整路径。配置文件中的其他路径可以是相对于此目录的相对路径。 |
| `notify yes\|no;` | 如果此服务器是其他服务器的主服务器，则在区域数据库更改时通知从服务器。 |
| `also-notify <server address> ...;` | 还通知未列在配置文件中的其他服务器。对于拥有未对外宣传的独立内部服务器的站点很有用。 |
| `recursion yes\|no;` | 默认情况下，DNS 服务器会递归地通过命名空间查找以回答客户端的查询。此语句可以禁用此功能。 |
| `maintain-ixfr-base yes\|no;` | 在区域传输期间，仅向其他服务器发送更改，而不是整个数据库。 |
| `transfers-in <number>;` | 限制同时进行的入站区域传输数量。 |
| `transfers-out <number>;` | 限制同时进行的出站区域传输数量。 |
| `forwarders (ip addresses);` | 查询被转发到的服务器列表，而不是由本服务器解析。 |
| `forward only \| first;` | 如果设置为 `only`，此服务器将仅将请求转发给其他服务器，而不会自行解析。如果设置为 `first`，服务器会尝试转发查询，但如果失败，它将自行解析查询。 |
| `allow-query {address match list};` | 限制可以查询您的 DNS 服务器的客户端。 |
| `allow-transfer {address match list};` | 限制可以从您的服务器请求区域传输的系统。 |
| `blackhole {address match list};` | 列表中的系统无法与您的 DNS 服务器通信。 |

#### acl 语句

访问控制列表（ACL）语句必须位于配置文件的顶部，但创建的 `name_of_acl` 可以在任何使用地址匹配列表的地方使用。语法如下：

```
acl name_of_acl {
    Address_match_list
};
```

`acl` 语句应位于配置文件的顶部。块中定义的 ACL 名称不能在遇到 `acl` 块之前使用。表 16-27 列出了四个预定义的 ACL 列表。

**表 16-27 预定义 ACL 列表**

| 列表 | 成员 |
| :--- | :--- |
| Any | 允许所有主机。 |
| None | 拒绝所有主机。 |
| Localnets | 允许系统上任何接口的本地网络。 |
| Localhost | 允许系统上任何接口的 IP。 |

#### server 语句
