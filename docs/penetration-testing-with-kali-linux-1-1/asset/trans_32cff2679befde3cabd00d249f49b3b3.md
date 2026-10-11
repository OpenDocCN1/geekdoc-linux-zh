
OSINT 框架并不旨在充当检查清单，但审阅这些类别和可用工具可以激发关于额外信息收集机会的灵感。

### 6.15.2 Maltego

Maltego^186^ 是一个功能非常强大的数据挖掘工具，提供了无尽的搜索工具和策略组合。其学习曲线可能非常陡峭，坦率地说，对于本模块而言它有点“杀鸡用牛刀”，但其令人印象深刻的能力值得进行介绍。

Maltego 搜索数千个在线数据源，并使用极其巧妙的“转换”（transforms）将一条信息转换为另一条。例如，如果我们正在执行用户信息收集行动，我们可以提交一个电子邮件地址，并通过各种自动化搜索，将其“转换”为关联的电话号码或街道地址。在组织信息收集练习中，我们可以提交一个域名，并将其“转换”为 Web 服务器，然后是一系列电子邮件地址，接着是一系列关联的社交媒体账户，最后是该电子邮件账户的潜在密码列表。

组合是无止境的，发现的信息以可扩展的图形形式呈现，允许轻松进行缩放和平移导航。

Maltego CE（Maltego 的受限“社区版”）包含在 Kali 中，并且需要免费注册才能使用。也有商用版本可用，可以处理更大的数据集。

^186^ (Paterna, 2019), https://www.paterna.com/buy/maltego-clients.php

多家供应商提供 Maltego 可以摄入并显示的信息。然而，一些提供商也对其数据访问收取费用。Maltego 不是完成实验室材料所必需的，但它可以是大规模信息收集操作中的不可或缺的工具。

## 6.16 总结

在本模块中，我们探讨了被动信息收集迭代过程的基础方面。我们涵盖了用于定位公司及其员工信息的各种技术和工具。这些信息在后续阶段往往证明是无价的。

# 7. 主动信息收集

在本模块中，我们将超越被动信息收集，探索涉及与目标服务直接交互的技术。我们将审视一些基础技术，但请记住，在实战中可以针对的服务数量不胜数。例如，包括我们在单独模块中更详细讨论的活动目录（Active Directory）。然而，在本模块中，我们将审视一些更常见的主动信息收集技术，包括端口扫描以及 DNS、SMB、NFS、SMTP 和 SNMP 枚举。

## 7.1 DNS 枚举

域名系统（DNS）^187^ 是互联网上最关键的系统之一，是一个负责将用户友好的域名翻译为 IP 地址的分布式数据库。

这是通过一种分层结构实现的，该结构划分为几个区域，从顶级根区域开始。让我们仔细看看解析 www.megacorpoone.com 这样的主机名所涉及的过程和服务器。

该过程从主机名被输入到浏览器或其他应用程序时开始。浏览器将主机名传递给操作系统的 DNS 客户端，然后操作系统将请求转发到其配置使用的外部 DNS 服务器。这个链条中的第一个服务器被称为 DNS 递归解析器（Recursor），负责与 DNS 基础设施交互并将结果返回给 DNS 客户端。DNS 递归解析器联系 DNS 根区域中的服务器之一。根服务器随后响应，提供负责包含顶级域名（TLD）^188^ 的区域的服务器地址，在本例中，是 .com TLD。

一旦 DNS 递归解析器接收到 TLD DNS 服务器的地址，它就会查询该服务器以获取 megacorpoone.com 域名的权威名称服务器（Authoritative Name Server）的地址。权威名称服务器是 DNS 查询过程的最后一步，包含在一个称为区域文件的本地数据库中的 DNS 记录。它通常为每个域托管两个区域：正向查找区域（用于查找特定主机名的 IP 地址）和反向查找区域（如果由管理员配置，用于查找特定 IP 地址的主机名）。一旦 DNS 递归解析器向 DNS 客户端提供 www.megacorpoone.com 的 IP 地址，浏览器就可以通过该 IP 地址联系正确的 Web 服务器并加载网页。

为了提高 DNS 的性能和可靠性，使用 DNS 缓存来在查询过程的不同阶段存储 DNS 记录的本地副本。这就是为什么一些现代应用程序，如 Web 浏览器，维护单独的 DNS 缓存的原因。此外，操作系统的本地 DNS 客户端以及查询过程中的每个 DNS 服务器也都维护自己的 DNS 缓存。域名所有者还可以通过 DNS 记录中的生存时间（TTL）字段来控制服务器或客户端缓存 DNS 记录的时间长度。

^187^ (Wikipedia, 2019), https://en.wikipedia.org/wiki/Domain_Name_System

^188^ (Wikipedia, 2019), https://en.wikipedia.org/wiki/Top-level_domain

### 7.1.1 与 DNS 服务器交互

每个域名可以使用不同类型的 DNS 记录。一些最常见的 DNS 记录类型包括：

- *NS* - 名称服务器记录包含托管该域 DNS 记录的权威服务器的名称。
- *A* - 也称为主机记录，"A 记录"包含主机名（如 www.megacorpone.com）的 IP 地址。
- *MX* - 邮件交换记录包含负责处理该域邮件的服务器名称。一个域可以包含多个 MX 记录。
- *PTR* - 指针记录用于反向查找区域，用于查找与 IP 地址关联的记录。
- *CNAME* - 规范名称记录用于为其他主机记录创建别名。
- *TXT* - 文本记录可以包含任意数据，可用于各种用途，例如域所有权验证。

由于 DNS 中包含的丰富信息，它通常是主动信息收集的有利目标。

为了演示这一点，我们将使用 **host** 命令来查找 www.megacorpone.com 的 IP 地址：

```
kali@kali:~$ host www.megacorpone.com
www.megacorpone.com has address 38.100.193.76
```
*列表 210 - 使用 host 查找 www.megacorpone.com 的 A 主机记录*

默认情况下，host 命令查找 A 记录，但我们也可以查询其他字段，如 MX 或 TXT 记录。为此，我们可以使用 -t 选项来指定我们要查找的记录类型：

```
kali@kali:~$ host -t mx megacorpone.com
megacorpone.com mail is handled by 10 fb.mail.gandi.net.
megacorpone.com mail is handled by 50 mail.megacorpone.com.
megacorpone.com mail is handled by 60 mail2.megacorpone.com.
megacorpone.com mail is handled by 20 spool.mail.gandi.net.

kali@kali:~$ host -t txt megacorpone.com
megacorpone.com descriptive text "Try Harder"
```
*列表 211 - 使用 host 查找 megacorpone.com 的 MX 和 TXT 记录*

### 7.1.2 自动化查询

现在我们有了来自 megacorpone.com 域名的初始数据，我们可以继续使用额外的 DNS 查询来发现属于同一域名的更多主机名和 IP 地址。例如，我们知道该域名有一个 Web 服务器，其主机名为 "www.megacorpone.com"。

让我们对该主机名运行 **host**：

![](img/ec25e59d75726b7041242a56d3376832_173_0.png)

```
kali@kali:~$ host www.megacorpone.com
www.megacorpone.com has address 38.100.193.76
```
*列表 212 - 使用 host 查找有效主机*

现在，让我们看看 megacorpone.com 是否有一个主机名为 "idontexist" 的服务器。注意查询输出的区别：

```
kali@kali:~$ host idontexist.megacorpone.com
Host idontexist.megacorpone.com not found: 3 (NXDOMAIN)
```
*列表 213 - 使用 host 查找无效主机*

在列表 212 中，我们查询了一个有效的主机名并收到了 IP 解析响应。相比之下，列表 213 返回了一个错误（NXDOMAIN^189^），表明该主机名不存在公共 DNS 记录。现在既然我们明白了如何搜索有效的主机名，我们就可以自动化我们的努力。

### 7.1.3 正向查找暴力破解

暴力破解是一种试错技术，旨在寻找有效信息，包括 Web 服务器上的目录、用户名和密码组合，或者在本例中，有效的 DNS 记录。通过使用包含常见主机名的词表，我们可以尝试猜测 DNS 记录并检查响应以获取有效的主机名。

在迄今为止的示例中，我们使用了*正向查找*，即请求主机名的 IP 地址，来查询一个有效和一个无效的主机名。如果 **host** 成功将一个名称解析为 IP，这可能是一个功能正常的服务器的迹象。

我们可以使用 **host** 命令在 Bash 单行程序中自动化常见主机名的正向 DNS 查询。

首先，让我们构建一个可能的主机名列表：

```
kali@kali:~$ cat list.txt
www
ftp
mail
owa
proxy
router
```
*列表 214 - 一个可能主机名的小列表*

接下来，我们可以使用一个 Bash 单行程序来尝试解析每个主机名：

```
kali@kali:~$ for ip in $(cat list.txt); do host $ip.megacorpone.com; done
www.megacorpone.com has address 38.100.193.76
Host ftp.megacorpone.com not found: 3 (NXDOMAIN)
mail.megacorpone.com has address 38.100.193.84
Host owa.megacorpone.com not found: 3 (NXDOMAIN)
Host proxy.megacorpone.com not found: 3 (NXDOMAIN)
router.megacorpone.com has address 38.100.193.71
```

^189^ (Internet Engineering Task Force, 2016), https://tools.ietf.org/html/rfc8020

