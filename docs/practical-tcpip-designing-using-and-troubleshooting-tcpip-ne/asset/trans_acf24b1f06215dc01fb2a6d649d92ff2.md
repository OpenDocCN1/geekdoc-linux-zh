
"1/2/2"。在此模式下，**tcpdump** 不会费心显示问题数量，因为它始终为一个。它也不显示问题，因为你已经在查询中看到它了，而且为了紧凑，它不会显示权威或附加记录部分的任何细节。

## tcpdump 详细（冗长）显示

要查看数据包中的更多信息，请使用选项 `**-vv**`（非常冗长）和 `**-s200**` 运行 **tcpdump** 以捕获 200 字节（因为 DNS 数据包可能很大）。下面显示了相同数据包的详细 **tcpdump** 跟踪；输出仍然只有两行（非常长），但我们已将其拆分并排版以更清晰地显示结构。（第一行中的 **[[domain]]** 表示数据包太长未被全部捕获；在本例中并非如此——这是 **tcpdump** 中的一个错误。）

![](img/a2132b646d336d5f9a21102d6320e537_226_0.png)

输出显示问题（**gilligan.ncd.com**）前面有 **q:**，然后是答案（IP地址 192.43.160.247）。**authority** 部分以 **ns:** 为前缀，并显示域名 **ncd.com** 有两个名称服务器，**NS.ncd.com** 和 **NS.UU.NET**，每个前面都有 "NS" 表示名称服务器记录。最后，以 **ar:** 为前缀的 **additional** 部分给出了在 **ns:** 部分返回的两个名称服务器的IP地址，即 **A** 记录。

## 解析器如何将回复与原始查询关联——“identifier”字段

为简单起见，我们所有的示例都显示了解析器向服务器发送的单个查询和单个回复。然而，繁忙的客户端机器（例如邮件服务器）每秒可能发送数十个查询，而回复可能以任何顺序返回。解析器在查询中包含唯一的 *identifier*，服务器在回复中包含相同的标识符，这样客户端就可以将回复与相应的查询匹配。例如，在上面显示的单个 DNS 会话中，标识符是 **553**。

查询中标识符后面的加号 “\+” 表示此查询是 *recursive*——客户端希望服务器找到完整答案，即使它必须依次联系其他服务器。（普通客户端查询始终是递归的，因此你通常可以忽略这一点。然而，我们将在第 8.7 模块中看到，服务器之间发送的查询可以是递归的，也可以不是。）你经常会在回复中的标识符后面看到 “*”；我们在第 8.10 模块中介绍这一点。

在接下来的两个模块中，我们将查看 nslookup 和 **host** 程序中的选项，以提供更详细的输出。

## 7.9 实验 – 探测 DNS – nslookup 命令调试选项

**nslookup** 有一个选项，“-d”（debug），用于打印有关其如何解析地址的额外信息。我们使用它来找出查询为何意外失败或未按预期执行，或与 **tcpdump** 结合使用以深入了解 DNS 的详细工作原理。请记住，在本模块中我们没有介绍有关 DNS 本身的任何新内容——我们只是展示特定工具如何显示 DNS 信息。（正如我们在注释中解释的那样，**nslookup** 之外有更好的工具，但由于在某些机器上 **nslookup** 可能是唯一可用的工具，我们将详细介绍它。）

图 7.8 显示了 **nslookup** 的注释示例，已重新格式化以节省空间。输出清楚地显示：

- 我们在第 7.7 模块中解释的四个部分（问题、答案、权威/名称服务器记录、附加记录）。在每个部分中，每个资源记录都以 “->” 为前缀显示。（每个记录旁边的 **TTL** 信息显示其保持有效的时间——其“生存时间”。DNS 在缓存回复时使用它，正如我们在第 8.10 模块中解释的那样。）
- DNS 数据包的头，它包含指示此查询类型的操作码（这几乎总是正常问题，显示为 **QUERY**）、标识符、查询的状态（“响应代码，**rcode**”）以及数据包四个部分中各有多少记录。

输出不太清楚的是，此特定示例涉及四个单独的数据包。请记住，与 **tcpdump** 不同，**nslookup** 并不是跟踪由其他人发起的查询：它自己执行查询并在执行过程中显示所有细节。如果你同时运行 **tcpdump** 和 **nslookup**，实际的数据包流程会更容易看出（图 7.9）。与往常一样，使用选项 **-n** 运行 **tcpdump** 以以数字形式显示地址，以防止它自行生成 DNS 查询，这只会造成混淆。涉及的数据包有：

- 1. **nslookup** 本身发送查询以获取它将要使用的 DNS 服务器的详细信息（查询显示在以 ; **res_mkquery** 开头的行中）
- 2. 包含名称服务器详细信息的回复，以 **Got answer**: 开头：如果我们使用 **tcpdump** 跟踪由 **ping** 等其他程序发起的查询，数据包 1 和 2 根本不会出现
- 3. 我们真正感兴趣的查询——本例中为 **gilligan.ncc.com**
- 4. 包含答案和有关 **gilligan.ncc.com** 的其他三个信息部分的数据包。

我们发现人们在最初解释 **nslookup** 输出时经常遇到困难。一个原因是你正在处理“冰山隐藏部分”——DNS 包含大量细节，需要一段时间才能习惯。然而，另一个原因是输出没有清晰地呈现——它更像是为工具的开发人员利益而打印的调试跟踪，而不是为用户利益而提供的详细信息列表。不要因此而气馁——这不是你立即不理解的错，而是他们没有说清楚的错。正如我们上面所说，**nslookup** 之外有更好的工具，能更清晰地呈现信息。

```
alice% nslookup -d gilligan.ncc.com
:: res_mkquery(0, 52.6.72.194.in-addr.arpa, 1, 12)
----------------------------------
Got answer:
HEADER:
opcode = QUERY, id = 33005, rcode = NOERROR
header flags: response, auth. answer, want recursion. recursion avail.
questions = 1, answers = 1, authority records = 3, additional = 3
QUESTIONS:
52.6.72.194.in-addr.arpa, type = PTR, class = IN
ANSWERS:
-> 52.6.72.194.in-addr.arpa    name = ns1.bt.net      ttl = 86400 (1D)
AUTHORITY RECORDS:
-> 6.72.194.in-addr.arpa    nameserver = ns0.bt.net ttl = 86400 (1D)
-> 6.72.194.in-addr.arpa    nameserver = ns1.bt.net ttl = 86400 (1D)
-> 6.72.194.in-addr.arpa    nameserver = ns2.bt.net ttl = 86400 (1D)
ADDITIONAL RECORDS:
-> ns0.bt.net    internet address = 194.72.6.51 ttl = 86400 (1D)
-> ns1.bt.net    internet address = 194.72.6.52 ttl = 86400 (1D)
-> ns2.bt.net    internet address = 193.113.212.38 ttl = 86400 (1D)
Server: ns1.bt.net
Address: 194.72.6.52
:: res_mkquery(0, gilligan.ncc.com, 1, 1)
----------------------------------
Got answer:
HEADER:
opcode = QUERY, id = 33006, rcode = NOERROR
header flags: response, auth. answer, want recursion. recursion avail
questions = 1, answers = 1, authority records = 2, additional = 2
QUESTIONS:
gilligan.ncc.com, type = A, class = IN
ANSWERS:
-> gilligan.ncc.com    internet address = 192.43.160.247 ttl = 3600 (1H)
AUTHORITY RECORDS:
-> ncc.com    nameserver = ns.ncc.com    ttl = 3600 (1H)
-> ncc.com    nameserver = ns.UU.NET    ttl = 3600 (1H)
ADDITIONAL RECORDS:
-> ns.ncc.com    internet address = 192.43.160.250 ttl = 3600 (1H)
-> ns.UU.NET    internet address = 137.39.1.3 ttl = 162401 (1d)
Name:    gilligan.ncc.com
Address: 192.43.160.247
```

数据包 1 - 获取名称
我们使用的 DNS 服务器

数据包 2 - 回复给出名称
DNS 服务器

数据包 3 - 查询
gilligan.ncc.com

数据包 4 - 回复给出我们请求的
IP地址

### 图 7.8 nslookup 调试输出的注释示例

```
alice% tcpdump -n -t -s300
192.0.2.34.1025 > 194.72.6.52.53: 33005* PTR? 52.6.72.194.in-addr.arpa. (42)
194.72.6.52.53 > 192.0.2.34.1025: 33005* 1/3/3 PTR ns1.bt.net. (164) (DF)
192.0.2.34.1025 > 194.72.6.52.53: 33006* A? gilligan.ncc.com. (34)
194.72.6.52.53 > 192.0.2.34.1025: 33006* 1/2/2 A 192.43.160.247 (129) (DF)
```

### 图 7.9 图 7.8 中查询的实际数据包流程

