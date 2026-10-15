
```
$ dig www.example.net 10.1.1.4
; <<>> DiG 9.7.0-Pl <<>> www.example.net 10.1.1.4
; Global options: +cd
; Got answer:
; --HEADER-- opcode: QUERY, status: REFUSED, id: 23822
; flags: gr rd; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 0
; WARNING: recursion requested but not available

; QUESTION SECTION:
;www.example.net.		IN	A

; Query time: 1492 msec
; SERVER: 10.1.1.4#53(10.1.1.4)
; WHEN: Sat Mar 24 20:15:17 2012
; MSG SIZE rcvd: 33
```

在这两种情况下，你看到的是 DNS 服务器正在运行并响应，但是你的请求被拒绝了。在 `dig` 输出中，你可以看到解释：请求被拒绝是因为递归不可用。

这里发生的情况很可能是配置错误造成的，尤其是如果该域名服务器以前工作正常的话。许多组织出于安全原因限制允许在其上执行递归查询的主机，如果你尝试从类似 `yahoo.com` 的域名服务器解析像 `google.com` 这样的站点，你可以看到这种情况。很可能是一名管理员修改了配置文件并意外地完全禁用了递归，或者如果递归被限制为特定的 IP 地址，管理员可能意外地删除了这些 IP。

在 BIND 中，默认情况下递归是开启的，但可以通过其配置文件禁用或限制。该选项在根 `named.conf` 文件（通常位于 `/etc/bind/named.conf`）或 `named.conf` 包含的其他配置文件中配置，例如在某些服务器上的 `named.conf.local` 或 `named.conf.options`。你要查找的选项称为 `recursion` 或 `allow-recursion`，位于文件的 `options` 部分，可能如下所示：

```
options {
    allow-recursion { 10.1.1.2/4; };
...
};
```

在这个例子中，允许整个 10.1.1.0 子网进行递归。你可能还会看到如下内容：

```
acl "internal" { 127.0.0.1; 192.168.0.0/24; 10.1.0.0/16; };

options {
    allow-recursion { "internal"; };
...
};
```

这里，我们没有指定 IP 地址，而是指定了一个名为 `internal` 的 ACL（访问控制列表），我们在配置文件的早期将其定义为 IP 地址列表。BIND 允许你这样做，以便你可以在一个位置定义 ACL，然后在配置中多次引用它们。如果你在 BIND 配置文件中看到像前面那样的行，而递归不起作用，请确保你的客户端 IP 地址在允许的网络列表中。

另一方面，如果你看到类似以下内容，

```
options {
    recursion no;
...
};
```

则说明该域名服务器上的递归已被禁用。若要启用它，请删除此选项，以便 BIND 切换为默认递归开启的状态，或者更好的是，将其替换为 `allow-recursion` 语句，以便 BIND 可以将递归限制在特定网络中。无论哪种情况，完成后请重启 BIND 服务器，以确保更改生效。

### 当更新不生效时

作为一名 DNS 管理员，你可能需要排除故障的常见问题之一是你对区域文件所做的更改未生效。即使你并不负责 DNS 服务器，知道如何排除更新故障也是你工具箱中一项有用的技能。毕竟，如果你要求管理员进行更改，或者如果你通过某些 DNS 托管服务进行更改，但你不断收到旧记录，了解如何查明问题所在会很有帮助。

大多数 DNS 更新问题分为三类：由于 DNS 缓存而你（尚未）看到的更新、由于语法错误而被 DNS 服务器拒绝的更新，以及由于主 DNS 服务器上的更改未能传播到其从属主机而导致的问题。本节讨论如何使用我们迄今为止使用的相同 DNS 故障排除工具来识别每种类型的问题。

### DNS 缓存和 TTL

事实是，你平均的 DNS 记录可能会保持相同长达数周、数月甚至数年。由于许多 DNS 记录非常静态，每个 DNS 查询都必须遵循我们在本章追踪部分讨论的那种相同路径，这并不太有意义。相反，当 DNS 服务器执行查询时，它会对结果进行缓存，以便如果你之后发起相同的请求，它可以更快地返回答案。

当然，缓存的问题在于，你使用的 DNS 服务器如何知道应该缓存结果多长时间？答案是每个 DNS 记录都包含一个生存时间（Time To Live，即 TTL）值，以秒为单位。当你执行 DNS 请求时，你使用的服务器检查其缓存，任何比其相应 TTL 新的记录都会从缓存返回给你，即使它们可能在主机上已经更改。一旦记录的 TTL 过期，DNS 服务器将按照常规步骤解析 IP；然而，请注意，沿途查询的每个 DNS 服务器也有自己的 TTL，如果这些 TTL 尚未过期，它只会使用缓存中的 IP。这就是为什么你经常听到这样的说法：“看到你在 DNS 中的更改可能需要两天时间。”具体来说，根域名服务器和顶级域名服务器具有较长的 TTL，因此当你注册一个新域名时，可能需要一些时间这些更改才能传播出去。虽然你的平均 TTL 是几小时，但 TTL 可以从不到一分钟到多天不等，并且根据更改的类型，可能需要相当长的时间才能让所有相关缓存过期。

虽然 DNS 缓存非常实用，但 DNS 管理员面临的一个问题是，并非所有 DNS 服务器都会遵守你的 TTL（生存时间）。事实上，一些 ISP（互联网服务提供商）因完全忽视过低的 TTL 而闻名，目的是帮助减轻其 DNS 服务器的负载。因此，即使你将 TTL 设置为仅几分钟，你所做的 DNS 更改可能需要数小时才能在某个不遵守该 TTL 的 DNS 服务器上生效。

除了直接在 DNS 服务器上查看之外，查看区域 TTL 最简单的方法是使用 `dig` 命令：

```bash
$ dig web1.example.net
; <<> DiG 9.7.0-P1 <<> example.net
;; global options: +cmd
;; Got answer:
; ->HEADER<- opcode: QUERY, status: NOERROR, id: 30750
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 2

; QUESTION SECTION:
;web1.example.net.     IN A

; ANSWER SECTION:
web1.example.net.      300 IN A 10.1.2.5

; AUTHORITY SECTION:
example.net.           300 IN NS ns2.example.net.
example.net.           300 IN NS ns1.example.net.

; ADDITIONAL SECTION:
ns1.example.net.       300 IN A 10.1.1.3
ns2.example.net.       300 IN A 10.1.1.4

; Query time: 2 msec
; SERVER: 192.168.0.1#53(192.168.0.1)
; WHEN: Mon Mar 19 20:48:27 2012
; MSG SIZE rcvd: 118
```

除了 `dig` 报告每条记录的 TTL 外，它不仅包含你所请求的主记录的 TTL，还包含它返回的任何附加信息的 TTL。在这种情况下，所有记录的 TTL 碰巧都是 300 秒。这告诉我们，如果我们对 `web1.example.net` 记录进行更改，普通 DNS 服务器返回新记录可能需要长达 5 分钟。

当然，如果你进行了更新但没有看到效果，如何确定是缓存问题而不是其他问题？最好的方法是识别该域名的官方名称服务器之一（在早期的 `dig` 输出中，你可以看到是 `ns2.example.net` 和 `ns1.example.net`）。如果你不确定某个域名使用了哪些名称服务器，只需执行一个 `dig` 查询来获取 NS 记录：
