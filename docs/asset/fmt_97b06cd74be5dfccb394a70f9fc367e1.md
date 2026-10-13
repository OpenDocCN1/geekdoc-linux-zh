
```text
options {
    # 这是区域文件存储的位置。
    directory "/var/named";
};

# 允许在 localhost 上运行的 rndc 向我们发送命令。
controls {
    inet 127.0.0.1 allow { localhost; }
    keys { rndc; }
};

# 包含要使用的密钥
include "/etc/rndc.key";

# 关于根区域的信息。
zone "." {
    type hint;
    file "root.hints";
};

# 许多软件依赖于能够解析 127.0.0.1
zone "0.0.127.in-addr.arpa" {
    type master;
    file "rev/127.0.0";
};
```

`options` 部分是我们在其中指定 `named` 应查找区域文件的目录的地方（如在文件的其他部分中命名的那样）。您将在本章后面的示例中学习如何使用其他选项。

接下来，我们指示 `named` 接受来自经过身份验证的 `rndc` 的命令。我们包含密钥文件 `/etc/rndc.key` 和 `controls` 部分，说明 `rndc` 将从 `localhost` 连接并使用指定的密钥。（您可以在允许列表中指定多个 IP 地址，或者使用第“安全”部分中描述的访问控制列表。）

`.` 区域告知 `named` 有关根域名服务器的信息，其名称和地址位于 `root.hints` 文件中。此信息决定最初咨询哪个根域名服务器，

尽管这一决定通常会基于服务器的响应时间而频繁修订。虽然提示文件可以通过 FTP 获取，但推荐的、对网络更友好的同步方式是使用 `dig`。我们向一个根域名服务器（具体哪一个无所谓）查询 `.` 的 NS 记录，并直接使用 `dig` 的输出：

```bash
# dig @j.root-servers.net. ns > /var/named/root.hints
# cat /var/named/root.hints
; <<>> DiG 8.2 <<>> @j.root-servers.net . ns
; (1 server found)
; res options: init recurs defnam dnsrch
; got answer:
; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 6
; flags: qr aa rd; QUERY: 1, ANSWER: 13, AUTHORITY: 0, ADDITIONAL: 13
; QUERY SECTION:
;	; ., type = NS, class = IN
;
; ANSWER SECTION:
.	6D IN NS	H.ROOT-SERVERS.NET.
.	6D IN NS	C.ROOT-SERVERS.NET.
.	6D IN NS	G.ROOT-SERVERS.NET.
.	6D IN NS	F.ROOT-SERVERS.NET.
.	6D IN NS	B.ROOT-SERVERS.NET.
.	6D IN NS	J.ROOT-SERVERS.NET.
.	6D IN NS	K.ROOT-SERVERS.NET.
.	6D IN NS	L.ROOT-SERVERS.NET.
.	6D IN NS	M.ROOT-SERVERS.NET.
.	6D IN NS	I.ROOT-SERVERS.NET.
.	6D IN NS	E.ROOT-SERVERS.NET.
.	6D IN NS	D.ROOT-SERVERS.NET.
.	6D IN NS	A.ROOT-SERVERS.NET.
;
; ADDITIONAL SECTION:
H.ROOT-SERVERS.NET.	5w6d16h IN A	128.63.2.53
C.ROOT-SERVERS.NET.	5w6d16h IN A	192.33.4.12
G.ROOT-SERVERS.NET.	5w6d16h IN A	192.112.36.4
F.ROOT-SERVERS.NET.	5w6d16h IN A	192.5.5.241
B.ROOT-SERVERS.NET.	5w6d16h IN A	128.9.0.107
J.ROOT-SERVERS.NET.	5w6d16h IN A	198.41.0.10
K.ROOT-SERVERS.NET.	5w6d16h IN A	193.0.14.129
L.ROOT-SERVERS.NET.	5w6d16h IN A	198.32.64.12
M.ROOT-SERVERS.NET.	5w6d16h IN A	202.12.27.33
I.ROOT-SERVERS.NET.	5w6d16h IN A	192.36.148.17
E.ROOT-SERVERS.NET.	5w6d16h IN A	192.203.230.10
D.ROOT-SERVERS.NET.	5w6d16h IN A	128.8.10.90
A.ROOT-SERVERS.NET.	5w6d16h IN A	198.41.0.4

;; Total query time: 4489 msec
;; FROM: lustre to SERVER: j.root-servers.net 198.41.0.10
;; WHEN: Mon Sep 10 04:18:26 2001
;; MSG SIZE sent: 17 rcvd: 436
```

## 区域文件

`named.conf` 中关于区域 `0.0.127.in-addr.arpa` 的部分表明，我们是该区域的主域名服务器，且区域数据位于文件 `127.0.0` 中。在详细检查第一个实际区域文件之前，请先查看资源记录（Resource Record）规范的一般格式：

| 字段 | 描述 |

| :--- | :--- |

| name | TTL |

| class | type |

| data | |

在此，`name` 是与该记录关联的 DNS 名称。在区域文件中，以 `."` 结尾的名称是完全限定域名，而其他名称则是相对于区域名称的相对名称。在区域 `example.com` 中，`foo` 指的是完全限定名称 `foo.example.com`。特殊名称 `@` 是区域本身名称的简写形式。如果省略名称，则再次使用最后指定的名称。

TTL（Time To Live，生存时间）字段是一个数字，指定记录可以被缓存的时间。这在下一节关于 SOA 记录的讨论中会有更详细的解释。如果省略该字段，则假设使用区域的默认 TTL。TTL 值通常以秒为单位，但你可以附加 `m` 表示分钟，`h` 表示小时，或 `d` 表示天。

BIND 支持不同的记录类别，但就实际用途而言，唯一重要的类别是 IN，即互联网（Internet）类别。如果没有明确指定类别，则假定为默认值 IN；为了减少打字量，我们在这里编写的所有区域文件中都不提及类别。

类型（type）字段是必需的，它指明了所使用的 RR（资源记录），例如 A、NS、MX 或 SOA。（这里我们将只使用现有 RR 中的几种。请查阅 DNS 标准以获取完整列表。）数据字段（data field）包含特定于此记录类型的数据。随着我们依次考察每种 RR 的用法，将会介绍相应的语法。

以下是区域 `0.0.127.in-addr.arpa` 的区域文件：

```dns
$TTL 2D
@       SOA     localhost. hostmaster.example.com. (
                    2001090101 ; Serial
                    24h        ; Refresh
                    2h         ; Retry
                    3600000    ; Expire (1000h)
                    1h)        ; Minimum TTL
            NS      localhost.
1       PTR     localhost.
```

应当位于每个区域文件开头的 `$TTL` 指令将该区域的默认最小生存时间设置为两天。这在下一节中会进一步讨论。

### 区域文件的 SOA 记录

区域文件中的第二行使用了前面提到的特殊名称 `@`。在这里，它代表 `0.0.127.in-addr.arpa`，`SOA`（Start of Authority，权限起点）记录属于该区域。其余字段（直到右括号）包含 SOA 特有的数据。

SOA 记录中的第一个数据字段是域名主域名服务器的完全限定名称。第二个字段是该区域联系人的电子邮件地址。它通过用“.”替换 `@` 符号写成 DNS 名称形式；`foo@example.com` 应写为 `foo.example.com`。（注意末尾的点）。

不要使用像 `a.b@example.com` 这样的地址，因为它会被写为 `a.b.example.com`，随后可能被误读为 `a@b.example.com`。

> **提示**
