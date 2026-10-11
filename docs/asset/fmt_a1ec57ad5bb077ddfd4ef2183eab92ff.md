
| 1D IN A | 192.168.196.5 |

| 1D IN MX | 10 mail |

| 1D IN MX | 20 mail.friend.bogus. |

| 1D IN HINFO | "P6" "Linux 1.3.59" |

| 1D IN A | 192.168.196.2 |

| 1D IN MX | 10 mail |

| 1D IN MX | 20 mail.friend.bogus. |

| 1D IN HINFO | "Pentium" "Linux 1.2" |

这很好。如你所看到的，它看起来非常像区域文件本身。

## 4.4. 警告事项

这里我应该补充一些事情。上述示例中使用的 IP 地址取自私有网络，即它们不允许在互联网上使用。第二点是 `notify`；它告诉 `named` 的从属（slave）服务器它更新了区域。在 `bind` 中，当区域更新时它可以通知 NS 记录的服务器。我们不希望实验污染互联网对吧？当然，这个域名是虚假的，里面的所有地址也是如此。关于真实的示例，请参见下一节。

## 4.5. 为什么反向查询不起作用

这里有几个在设置反向区域时常见的“坑”。在继续之前，你需要确保你自己的服务器的反向查询工作正常。如果不是，请回去修复。

我将讨论从网络外部观察的两种反向查询失败：

### 4.5.1. 反向区域未委托

当你向服务提供商请求网络地址范围和域名时，域名通常是经过委托的。委托是 NS 记录，帮助你从一个名称服务器到另一个，如上文理论部分解释的那样。你读了吗？如果你的反向区域不起作用，回去读一遍。现在。

### 4.5.2. 你拥有无类子网

无类子网是如今互联网运行的基础。几年前，关于 IP 数字短缺的问题引起了很大动静。IETF 里的聪明人们集思广益并解决了这个问题。付出了代价的。代价是你得到的比一个“C”子网少，并且某些东西可能会损坏。请参阅 http://www.acmebw.com/askdns/00007.htm 以获取对此问题以及如何处理的很好的解释。

# 附录 G：名称服务器文档

某些 ISP 会提供其他处理此的方法，例如基于 Web 的表单供您输入反向映射，或其他自动化的系统。

## 5. 一个真实的域名示例

在这里我们列出了一些真实的区域文件（zone files）。

用户建议我在教程示例之外也包含一个运行中域的真实示例。

我在 LAND-5 的 David Bullock 许可下使用了此示例。这些文件是 1996 年 9 月 24 日当时的，随后经过了我的编辑以适应 `bind` 8 的限制并使用了扩展。因此，你看到的内容与你查询 LAND-5 域名服务器时找到的结果略有不同。

### 5.1. `/etc/named.conf` (或 `/var/named/named.conf`)

在这里我们找到了两个所需的反向区域的主区域部分：`127.0.0` 所在的网段，以及 LAND-5 的 `206.6.177` 子网。还有一条用于 `land-5` 正向区域 `land-5.com` 的主记录。另外请注意，他没有像我在 HOWTO 中那样将文件放在名为 `pz` 的目录中，而是将它们放在名为 `zone` 的目录中。

```
// Boot file for LAND-5 name server

options {

    directory "/var/named";

};

zone "." {

    type hint;

    file "root.hints";

};

zone "0.0.127.in-addr.arpa" {

    type master;

    file "zone/127.0.0";

};

zone "land-5.com" {

    type master;

    file "zone/land-5.com";

};

zone "177.6.206.in-addr.arpa" {

    type master;

    file "zone/206.6.177";

};
```

如果你想将此内容放入你的 `named.conf` 文件中进行测试，请务必在两个 `land-5` 区域的节中加入 `"notify no;"` 以防意外。

## 5.2. `/var/named/root.hints`

记住这个文件是动态的，这里列出的是旧的。最好像前面解释的那样，使用 `dig` 使用当前生成的。

```
<<>> DIG 8.1 << @A.ROOT-SERVERS.NET.

;(1 server found)

; res options: init recurs defnam dnsrch

; got answer:

; ->HEADER opcode: QUERY, status: NOERROR, id: 10

;; flags: qr aa rd; QUERY: 1, ANSWER: 13, AUTHORITY: 0, ADDITIONAL: 13

;; QUERY SECTION:

; , type = NS, class = IN

;; ANSWER SECTION:

6D IN NS G.ROOT-SERVERS.NET.

6D IN NS J.ROOT-SERVERS.NET.

6D IN NS K.ROOT-SERVERS.NET.

6D IN NS L.ROOT-SERVERS.NET.

6D IN NS M.ROOT-SERVERS.NET.

6D IN NS A.ROOT-SERVERS.NET.

6D IN NS H.ROOT-SERVERS.NET.

6D IN NS B.ROOT-SERVERS.NET.

6D IN NS C.ROOT-SERVERS.NET.

6D IN NS D.ROOT-SERVERS.NET.

6D IN NS E.ROOT-SERVERS.NET.

6D IN NS I.ROOT-SERVERS.NET.

6D IN NS F.ROOT-SERVERS.NET.

;; ADDITIONAL SECTION:

G.ROOT-SERVERS.NET. 5w6d6h IN A 192.112.36.4

J.ROOT-SERVERS.NET. 5w6d6h IN A 198.41.10.0

K.ROOT-SERVERS.NET. 5w6d6h IN A 193.0.14.129

L.ROOT-SERVERS.NET. 5w6d6h IN A 192.38.64.12

M.ROOT-SERVERS.NET. 5w6d6h IN A 202.122.73.23
```

```
A.ROOT-SERVERS.NET  5w6d6h IN A  198.41.0.4

H.ROOT-SERVERS.NET  5w6d6h IN A  128.63.2.53

B.ROOT-SERVERS.NET  5w6d6h IN A  128.9.10

C.ROOT-SERVERS.NET  5w6d6h IN A  192.33.4.12

D.ROOT-SERVERS.NET  5w6d6h IN A  128.8.10.90

E.ROOT-SERVERS.NET  5w6d6h IN A  192.203.23.10

I.ROOT-SERVERS.NET  5w6d6h IN A  192.36.148.17

F.ROOT-SERVERS.NET  5w6d6h IN A  192.5.241

;; Total query time: 215 msec

;; FROM: A.ROOT-SERVERS.NET. 198.41.0.4

;; WHEN: Sun Feb 15 01:22:51 1998

;; MSG sent: 177 rcvd: 43
```

### 5.3. `/var/named/zone/127.0.0`

基础内容、强制性的 SOA 记录以及将 `127.0.0` 映射到 `localhost` 的记录都是必须的。除非你的名称服务器地址发生变化，否则此文件可能不需要更新。

```
IN SOA land-5.com. root.land-5.com. (

    19960203      ; Serial

    28800         ; Refresh

    7200           ; Retry

    60480         ; Expire

    86400)        ; Minimum
```

### 5.4. `/var/named/zone/land-5.com`

在这里我们看到了强制性的 SOA 记录和 NS 记录。我们可以看到它在 `ns2.psi.net` 有一个辅助服务器。它应该有一个离地的备份服务器。我们还可以看到它有一个名为 `land-5` 的主主机处理许多不同的服务，并且它带有 CNAME 记录（使用 A 记录）。正如你看到的 SOA 记录，该区域文件源于 1996 年 9 月 20 日。记住，序列号必须单调递增；目前只有一位数字，所以他必须等到明天才能编辑该文件。考虑使用两位数字。

```
@ SOA land-5.com. root.land-5.com. (
```
