
```bash
$ dig example.net NS
;; <<> DiG 9.7.0-P1 <>> example.net NS

;; global options: +cmd
;; Got answer:
;; ->>HEADER<< opcode: QUERY, status: NOERROR, id: 38194
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 2

;; QUESTION SECTION:
;example.net.            IN      NS

;; ANSWER SECTION:
example.net.        300   IN      NS      ns1.example.net.
example.net.        300   IN      NS      ns2.example.net.

;; ADDITIONAL SECTION:
ns1.example.net.    300   IN      A       10.1.1.3
ns2.example.net.    300   IN      A       10.1.1.4

;; Query time: 3 msec
;; SERVER: 192.168.0.1#53(192.168.0.1)
;; WHEN: Sat Mar 24 20:44:42 2012
;; MSG SIZE  rcvd: 98
```

一旦你获得了名称服务器列表，选择其中一个并直接查询它：

```bash
$ dig web1.example.net @10.1.1.4
```

当你直接查询名称服务器时，你就绕过了本地 DNS 服务器的任何缓存，从而获取当前最新的记录。因此，如果你从直接查询中获得的 IP 仍然是旧的 IP，你就知道该更改尚未传播到该名称服务器。此时，直接查询列表中的其余名称服务器，看看是否有任何一个拥有正确的记录。如果你发现没有 DNS 服务器拥有更新后的记录，那么你的区域文件中可能存在语法错误。如果某些 DNS 服务器有更新而其他服务器没有，你可能遇到了区域传输问题。

如果你发现名称服务器确实拥有正确的记录，但你的本地 DNS 服务器缓存了旧记录，你有几种补救措施。最简单的补救措施是等待本地缓存过期。理想情况下，如果你预知需要做出 DNS 更改且你的 TTL 较长，许多 DNS 管理员会在更改前几天降低 TTL，以便让所有 DNS 服务器有机会拉取新的较短 TTL。然后，一旦更改完成，再将 TTL 恢复为旧值。

如果你不能等待本地缓存过期，你也可以刷新相应的 DNS 缓存。第一个需要刷新的缓存位于你的操作系统上。是的，即使你的操作系统也会缓存 DNS 请求，这样每次需要解析记录时就不必查询名称服务器。在 Linux 上，`nscd` 守护进程（如果已安装）负责处理此缓存，因此要刷新其缓存，只需输入：

```bash
$ sudo /etc/init.d/nscd restart
```

如果你使用的是 Windows 系统，可以打开命令提示符并输入：

```bash
ipconfig /flushdns
```

在 Mac 上，你需要打开终端并输入：

```bash
lookupd -flushcache
```

或者，取决于你的 Mac OS X 版本：

```bash
dscacheutil -flushcache
```

如果是你的递归 DNS 服务器持有缓存，你需要拥有其管理权限才能刷新其缓存。要刷新 BIND 名称服务器的 DNS 缓存，你只需重启该服务。在基于 Red Hat 的系统上，这可能是：

```bash
$ sudo /etc/init.d/named restart
```

在基于 Debian 的系统上，该服务可能被称为 `bind` 或 `bind9`，而不是 `named`。如果你无法重启你的递归名称服务器，唯一的替代方案是临时将系统配置的名称服务器替换为一个没有缓存旧记录的名称服务器，或者，你可以将 IP 硬编码到你的 `/etc/hosts` 文件中，但这是我并不推荐的短视修复方法。

## 区域语法错误

如果你修改了 DNS 记录，并注意到更新没有到达该区域的任何名称服务器，可能的原因是区域文件中的语法错误。当你修改区域文件并重载 BIND 时，如果它注意到文件中有语法错误，它只会忽略对该特定区域文件的任何更改，并保留现有的记录。除非你关注日志文件，否则你甚至可能没有意识到发生了这种情况。如果你更新了一个区域，重载了 BIND 服务，而名称服务器仍然报告旧记录，请检查系统中的 `/var/log/syslog` 或 `/var/log/messages` 以查看来自 BIND 的错误消息。

以下是一个由语法错误导致的错误消息示例：

```text
Mar 27 21:07:26 ns1 named[25967]: /etc/bind/db.example.net:20: #ns2.example.net: bad owner name (check-names)
Mar 27 21:07:26 ns1 named[25967]: zone example.net/IN: loading from master file /etc/bind/db.example.net failed: bad owner name (check-names)
Mar 27 21:07:26 snowball named[25967]: zone example.net/IN: not loaded due to errors.
```

在这种情况下，错误消息的第一行好心肠地告诉我，错误位于 `/etc/bind/db.example.net` 的第 20 行。这里发生了一个经典的错误：除了使用分号的 BIND 外，几乎所有配置文件都支持使用 `#` 来注释掉一行。管理员在区域文件中错误地使用了 `#` 来注释掉一行，而不是使用分号，导致 BIND 拒绝了该区域。

## 区域传输问题

我们将讨论的最后一个可能导致 DNS 更改不生效的问题是区域传输问题。在典型的 DNS 基础设施中，一个 DNS 服务器被视为特定区域的主服务器，其余则配置为从服务器。所有更改都在主服务器上进行，然后推送到已配置的从服务器。区域传输问题可能很难立即检测到，因为你的主名称服务器会报告新记录；然而，对其中一个或多个从服务器的查询可能报告旧记录。结果是，不同的客户端在不同时间可能看到不同的 IP 地址。

识别区域传输问题的最快方法是对配置该区域的所有名称服务器使用 `dig` 等工具执行直接 DNS 查询。如果你看到某些名称服务器有更改而其他没有，等待一两分钟再试，看看更改是否只是需要一些时间来传播。如果几分钟后更改仍未传输，下一步是识别主 DNS 服务器并确认它拥有正确的记录。主 DNS 服务器配置在一个称为权限起始（Start of Authority，或 SOA）的特殊记录中。该列出了被视为该区域的权威 DNS 服务器，与其他针对特定记录类型的 `dig` 请求一样，只需查询域名并在查询末尾添加 SOA：

```bash
$ dig example.net SOA

; <<> DiG 9.7.0-P1 <<> example.net SOA
; ; global options: +cmd
; ; Got answer:
; ; ->>HEADER<< opcode: QUERY, status: NOERROR, id: 62609
; ; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 2

; ; QUESTION SECTION:
; example.net.			IN	SOA

; ; ANSWER SECTION:
example.net.			300	IN	SOA	ml.example.net. admin.example.net.
	2011062300 10800 2000 604800 7200
```

## DNS 服务器故障排除

在此输出中，我们特别关注以下这一行：

```
; ANSWER SECTION:
example.net. 300 IN SOA ns1.example.net. admin.example.net.
2011062300 10800 2000 604800 7200
```

这里可以看到，权威 DNS 服务器是 `ns1.example.net`。紧随其后的下一条记录 `admin.example.net` 并不是另一个名称服务器，而是该域名的管理联系人电子邮件地址。第一个句号实际上应替换为 @ 符号，因此在这种情况下，管理联系人是 `admin@example.net`。

一旦确定哪个名称服务器是某个区域的权威服务器，该服务器就应被配置为主服务器。如果我们怀疑存在区域传输问题，下一步是直接登录到主 DNS 服务器并检查其配置。
