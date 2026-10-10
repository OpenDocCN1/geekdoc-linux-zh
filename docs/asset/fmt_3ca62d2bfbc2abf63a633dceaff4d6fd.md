
# 配置 `named`

接下来你必须配置 `named` 本身。其单一的配置文件（`/etc/named.conf`）具有与 `rndc.conf` 非常相似的语法；本节仅描述配置一个功能性名称服务器所必需的少量配置指令子集。如需更全面的手册，请参考 `BIND 9 ARM`（管理员参考手册）；它随 `BIND` 分发，Fedora 将其安装在 `/usr/share/doc/bind-*/arm/` 目录下。

在 `named.conf` 文件中，仅有 `options` 和 `named` 部分是绝对必要的。`options` 部分必须告诉 `named` 区域文件存储在哪里，并且 `named` 必须知道在哪里找到根区域（`.`）。我们还设置了 `controls` 部分，以便接受经过适当身份验证的来自 `rndc` 的命令。由于客户端（特别是 `nslookup`）通常依赖于解析名称服务器的 IP，我们也设置了 `0.0.127.in-addr.arpa` 反向区域。

我们从类似以下内容的配置文件开始：

```
options {
    # This is where zone files are kept.
    directory "/var/named/";
};

# Allow rndc running on localhost to send us commands.
controls {
    inet 127.0.0.1 allow { localhost; } keys { rndc; };
};
include "/etc/rndc.key";

# Information about the root zone.
zone "." {
    type hint;
    file "root.hints";
};

# Lots of software depends on being able to resolve 127.0.0.1
zone "0.0.127.in-addr.arpa" {
    type master;
    file "rev/127.0.0";
};
```

`options` 部分用于指定 `named` 查找区域文件的目录（在文件的其他部分中指定的目录）。您将在本章后续的示例中了解如何使用的其他选项。

接下来，我们指示 `named` 接受来自经过身份验证的 `rndc` 的命令。我们包含密钥文件 `/etc/rndc.key` 以及 `controls` 部分，其中说明 `rndc` 从 `localhost` 连接并使用指定的密钥。（您可以在 `allow` 列表中指定多个 IP 地址，或使用如本章后面“管理 DNS 安全性”一节中所述的访问控制列表。）

`.` 区域告诉 `named` 有关根名称服务器的信息，其名称和地址位于 `root.hints` 文件中。该信息决定了最初查询哪个根名称服务器，尽管基于服务器的响应时间，这一决定通常会被修正。虽然可以通过 FTP 获取 `hints` 文件，但推荐的、对网络友好的保持同步方法是使用 `dig`。我们向一个根名称服务器（任何一个都行）请求 `.` 的 `NS` 记录，并直接使用 `dig` 的输出：

```
# dig @j.root-servers.net. ns > /var/named/root.hints
# cat /var/named/root.hints
;; <<> Dig 8.2 <<> @j.root-servers.net . ns
;; (1 server found)
;; res options: init recurs defnam dnsrch
;; got answer:
;; ->>HEADER<< opcode: QUERY, status: NOERROR, id: 6
;; flags: qr aa rd; QUERY: 1, ANSWER: 13, AUTHORITY: 0, ADDITIONAL: 13
;;
; QUERY SECTION:
;; , type = NS, class = IN
;
;
; ANSWER SECTION:
.			6d IN NS	H.ROOT-SERVERS.NET.
.			6d IN NS	C.ROOT-SERVERS.NET.
.			6d IN NS	G.ROOT-SERVERS.NET.
.			6d IN NS	F.ROOT-SERVERS.NET.
.			6d IN NS	B.ROOT-SERVERS.NET.
.			6d IN NS	J.ROOT-SERVERS.NET.
.			6d IN NS	K.ROOT-SERVERS.NET.
.			6d IN NS	L.ROOT-SERVERS.NET.
.			6d IN NS	M.ROOT-SERVERS.NET.
.			6d IN NS	I.ROOT-SERVERS.NET.
.			6d IN NS	E.ROOT-SERVERS.NET.
.			6d IN NS	D.ROOT-SERVERS.NET.
.			6d IN NS	A.ROOT-SERVERS.NET.
;
;; ADDITIONAL SECTION:
H.ROOT-SERVERS.NET.		5w6d16h IN A	128.63.2.53
C.ROOT-SERVERS.NET.		5w6d16h IN A	192.33.4.12
G.ROOT-SERVERS.NET.		5w6d16h IN A	192.112.36.4
F.ROOT-SERVERS.NET.      5w6d16h IN A    192.5.5.241
B.ROOT-SERVERS.NET.      5w6d16h IN A    128.9.0.107
J.ROOT-SERVERS.NET.      5w6d16h IN A    198.41.0.10
K.ROOT-SERVERS.NET.      193.0.14.129
L.ROOT-SERVERS.NET.      198.32.64.12
M.ROOT-SERVERS.NET.      202.12.27.33
I.ROOT-SERVERS.NET.      192.36.148.17
E.ROOT-SERVERS.NET.      192.203.230.10
D.ROOT-SERVERS.NET.      128.8.10.90
A.ROOT-SERVERS.NET.      198.41.0.4
;
;; Total query time: 4489 msec
;; FROM: lustre to SERVER: j.root-servers.net 198.41.0.10
;; WHEN: Mon Sep 10 04:18:26 2001
;; MSG SIZE  sent: 17  rcvd: 436
```

## 区域文件

`named.conf` 中的区域 `0.0.127.in-addr.arpa` 部分说明我们是该区域的主名称服务器，并且区域数据位于文件 `127.0.0` 中。在详细查看第一个真正的区域文件之前，先看一下 RR（资源记录）规格的一般格式：

```
name TTL class type data
```

这里，`name` 是与该记录关联的 DNS 名称。在区域文件中，以 `.` 结尾的名称是完全限定名称，而其他的名称是相对于区域名称的。在区域 `example.com` 中，`foo` 指的是完全限定名称 `foo.example.com`。特殊名称 `@` 是区域本身名称的缩写形式。如果省略名称，则再次使用最后指定的名称。

`TTL`（生存时间）字段是一个数字，指定记录可以被缓存的时间。这在下一节关于 `SOA` 记录的讨论中会详细解释。如果省略此字段，则假设使用区域的默认 `TTL`。`TTL` 值通常以秒为单位，但您可以添加 `m` 表示分钟，`h` 表示小时，或 `d` 表示天。

`BIND` 支持不同的记录类，但就实际目的而言，唯一重要的类是 `IN`，代表互联网。如果没有明确指定类，则假设默认值为 `IN`；为了少打几个字，我们在编写的任何区域文件中都不提及类。

`type` 字段是强制性的，它指定了正在使用的 RR，例如 `A`、`NS`、`MX` 或 `SOA`。（这里我们只使用了现有的少数几种 RR。请查阅 DNS 标准以获取完整列表。）

`data` 字段（或字段）包含特定于此类型记录的数据。适当的语法将在我们依次检查每个 RR 的使用时介绍。

以下是 `0.0.127.in-addr.arpa` 区域的区域文件：

```
$TTL	2D
@	SOA	localhost. hostmaster.example.com. (
		2001090101	; Serial
		24h		; Refresh
		2h		; Retry
		3600000	; Expire (1000h)
		1h)		; Minimum TTL
	NS	localhost.
1	PTR	localhost.
```

应该开始每个区域文件的 `$TTL` 指令将该区域的默认最小生存时间设置为两天。这在下一节中将进一步讨论。

### 区域文件的 SOA 记录

区域文件中的第二行使用了您之前看到的特殊 `@` 名称。在这里，它代表 `0.0.127.in-addr.arpa`，`SOA`（*Authority 的起点*）记录属于它。其余的字段（持续到右括号）包含 `SOA` 特定的数据。
