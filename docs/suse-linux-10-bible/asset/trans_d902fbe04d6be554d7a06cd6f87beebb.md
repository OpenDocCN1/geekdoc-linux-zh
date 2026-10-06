
当 BIND 服务器被配置为转发器（forwarder）时，它会自动缓存从 Internet DNS 服务器收到的任何响应。启用此缓存功能不需要任何额外配置。

当配置了转发声明（forwards declaration）时，请使用 *rcnamed* 启动命名服务器：

```
bind:: # rcnamed start
Starting nameserver BIND 9
```

若要在系统启动时自动启动 named，请使用 *chkconfig* -a named。

在开始测试 DNS 服务器之前，你需要配置 DNS 解析器。要执行此操作，你需要编辑 /etc/resolv.conf 文件。将 nameserver 条目更改为你新创建的 DNS 服务器。在这种情况下，即为 127.0.0.1。

```
search palmcoder.net
nameserver 127.0.0.1
```

当 DNS 服务器启动后，你可以查询 Internet 上的主机名，以检查转发器和 DNS 是否工作正常。*dig* 程序用于向 DNS 服务器查询信息（参见列表 21-1），我们在整个章节中都用它来实现此目的。

## 使用 dig

dig 程序正在逐渐引入，并作为 *nslookup 应用*的替代品。通过 dig，你可以查询 DNS 区域中的特定记录类型。要查询特定记录类型，请使用 -t 选项。例如：

- 查询 palmcoder.net 的 MX 记录，使用 *dig -t mx palmcoder.net.*。
- 查询命名服务器（NS），使用 *dig -t ns palmcoder.net.*。
- 查询地址记录（A），使用 *dig -a www.palmcoder.net.*。

列表 21-1：使用 dig 测试 DNS 服务器

```
bind:: # dig www.palmcoder.net
;; Warning: ID mismatch: expected 23997, got 50172
;; Warning: ID mismatch: expected 23997, got 50172
<<>> DIG 9.2.3 << www.palmcoder.net
;; global options: printcmd
;; answer:
;;>>HEADER<< opcode: QUERY, status: NOERROR, id: 23997
;; flags: gr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 1, OPTIONAL: 0
```

列表 21-1（续）

```
;; QUESTION SECTION:
www.palmcoder.net.             IN A

;; ANSWER SECTION:
www.palmcoder.net.             38396 IN CNAME
zen.palmcoder.net.             38400 IN A 212.13.208.115

;; AUTHORITY SECTION:
palmcoder.net.                 38400 IN NS zen.palmcoder.net.

;; Query time: 443 msec
;; SERVER: 127.0.0.1:853(127.0.0.1)
;; WHEN: Tue Jul 6 10:02:21 2004
;; MSG size: 83
```

在过去，名称解析器 nslookup 被用来替代 dig；nslookup 现在已被弃用，但仍包含在大多数 Linux 发行版中。如果你想进行快速名称解析，使用 nslookup hostname 会返回 IP 地址。

如果你从未用过 dig，它的输出可能会让你困惑，但当你理解了 DNS 的作用时，它对名称查询的响应是有逻辑的。输出包含三个基本部分：

- 响应的第一部分是 QUESTION（问题）部分。QUESTION 是最初发送到 DNS 服务器的内容。在这种情况下，你请求了 www.palmcoder.net 的 A 记录。（注意，我们在章节中会讨论记录类型）。
- 第二部分是 ANSWER（答案）部分。答案是对你查询的响应。在这种情况下，你发现 www.palmcoder.net 是 zen.palmcoder.net 的 CNAME，而后者的地址是 212.13.208.115。
- 最后，你还有 AUTHORITY（权威）部分。权威是 NS 记录中的服务器 IP 地址。

## 使用 host

host 是 nslookup 程序的易用替代品，它允许你查询关于域名的 DNS 信息。使用 host，你可以查询特定的域名记录，并默认查找主机名的地址。

```
bind:~ # host www.palmcoder.net
www.palmcoder.net is an alias for zen.palmcoder.net.
zen.palmcoder.net has address 212.13.208.115
```

在本示例中，host 查询了对 palmcoder.net 权威的命名服务器，并发现 www.palmcoder.net 实际上是 zen.palmcoder.net 的 CNAME。

如果你想找到域的特定 DNS 记录，使用 -t 选项指定记录类型：

```
bind:~ # host -t mx palmcoder.net
palmcoder.net mail is handled by 10 palmcoder.net.
palcoder.net mail is handled by 20 pirhana.bymark.co.uk.
```

在这里，host 查询了对 palmcoder.net 权威的命名服务器，请求该域的 MX 记录。它发现有两个 mail（pirhana.bymark.co.uk），其中 palmcoder.net 的优先级更高。

## 检查记录类型

在我们深入创建 DNS 区域（一个管理域）之前，我们需要讨论记录类型。我们简要提到了 DNS 不仅提供主机到 IP 地址的转换，还提供邮件服务器信息。记录类型告诉我们存储的是什么信息，以及你可以查询的内容。例如，你查询域的 MX 记录以确定发送邮件到该域时使用哪一个邮件服务器。依赖 DNS 的服务极大地减少了流量产生，因为你只看到你请求的数据，而不是整个记录。在 DNS 中，有六种记录类型需要记住：

- 地址记录（Address record）：DNS 中常见的记录是地址记录。地址记录用于将主机名转换为 IP 地址。
- 指针记录（Pointer record）：指针记录是地址记录的反向。它将 IP 地址转换为主机名。
- CNAME记录（CNAME record）：如果你想创建一个主机到另一个主机的别名，则使用 CNAME 记录。
- MX 记录：用于定义你创建的域（或区域）的邮件交换器（Mail Exchanger）。
- NS 记录：用于定义域的命名服务器。
- SOA 记录：起始区域（SOA）实际上是区域的头部。它包含了区域本身的信息并且是强制性的。

## 操作区域

区域（zone）是域（或子域）的描述或定义。区域构成了域的记录数据库/var/lib/named 是包含区域数据的文本文件。BIND 通过在 /etc/named.conf 中指定这些文件的位置来定义它的区域。在本节中，你将看到 DNS 区域是如何构建的，以及区域可以存储哪些信息。我们使用 palmcoder.net 作为区域的示例（参见列表 21-2），并将遍历 DNS 记录解释它们的用途。

列表 21-2：palmcoder.net 区域

```
palmcoder.net.  IN  SOA  palmcoder.net. admin.palmcoder.net. (
                   2005072401
                   10800
                3600
                60480
                86400)
NS  zen
MX  10 mail
MX  20 pirhana.bymark.co.uk.

zen  A  212.13.208.115
www  NAME  zen
mail A  212.13.208.115
scpan NAME  zen
shuttle A  195.137.245
```

## 起起始

在区域的开头，你拥有针对目标域 palmcoder.net 的权威 SOA。注意 palmcoder.net 以句号（点）结尾。这对于任何域的区域文件都至关重要。正如你在图 21-1 中所看到的，DNS 树的顶部是 DNS 树的根。句号是 DNS 树的限制符；一直沿着 palmcoder.net 域向上直到树顶，完整的域名是 palmcoder.net（带句号）。如果在示例末尾列出的区域记录未找到句号，SOA 的域名将附加到记录中的主机名。

## SOA 服务器

可以进一步分析 SOA 以分解记录的用途。在你管理的域定义之后，你需要定义该域的权威服务器。这看起来可能很奇怪，但在这种情况下你指的是一个名称而不是 IP 地址，因为 BIND 意识到它需要从自己的区域中查找服务器的 IP 地址（这听起来可能像恶性循环，但它确实有效）。例如在列表 21-2 中，palcoder.net 的 SOA 是 zen.palcoder.net。

## 主机管理员

在互联网上的许多事物，惯做法是为服务提供技术联系人。在这种情况下，它是邮件地址 justin.palcoder.net。你会注意到邮件地址中没有 @ 符号，而是一个句号。palcoder.net 区域的主机管理员是 justin.palcoder.net（justin@palmcoder.net）。

![](img/e4e45c9f32e76fb35fabbd1a96f1a1e_621_0.png)

如果邮件地址包含句号，你需要对其进行转义。例如，如果你的邮件地址是 justin.davies@palcoder.net，则主机条目为 justin\.davies.palcoder.net。

## SOA 记录

括号周围其余的数据都是 SOA 记录的一部分。所有时间设置均为秒。

## 序列号

第一个条目是区域的序列号。这是 SOA 最重要的部分之一，因为每次编辑区域文件时必须更改它。序列号告诉查询你 DNS 服务器的其他 DNS 服务器发生了变化。如果你不更改序列号，你的更改就不会在系统中传播。

序列号的一般形式是日期后跟一个任意数字。对于 7 月 24 日，你使用 2005072401（2005年7月24日）。注意日期是反序的，即年份（2005）、月份（07）和日期（24），额外的两位数字允许一天内重复多次更改。

## 刷新频率

如果你在系统中有一个从 DNS 服务器（作为你主服务器的备份），刷新频率告诉从服务器每多久检查一次区域的更新。如果你回看列表 21-2，你会看到刷新频率设置为 10800 秒（3 小时）。

