
## 设置不同类型的 DNS 服务器

按照视图（View）类的顺序，所有用户——包括本地用户——都将获得为公众准备的视图，而没有用户能看到本地视图。

Options 子句中的许多语句可以应用于 View 子句内，在那里它们会覆盖（全局）Options 子句中的语句。**recursion** 语句可以出现在 Options 子句中，并且在每个 View 子句中都会出现。此 **named.conf** 文件设置了一个服务器，该服务器对源自本地的查询提供递归响应，而对来自公众的查询提供迭代响应。这种设置可以为本地用户快速、完整地提供答案，在继续为本地服务器提供权威名称服务的同时，限制分配给其他用户的网络和处理器带宽。

为了使 **named.conf** 更容易理解和维护，不同 View 子句中的区域可以拥有相同的名称但使用不同的区域文件。示例中本地和公开 View 子句都有名为 **zach.net** 的区域。公开的 **zach.net** 区域文件命名为 **public.net**，本地的则命名为 **local.net**。

Logging 子句在第 887 页中有描述。

定义 **zach.net** 的区域文件与前面示例中的类似；公开文件是本地文件的子集。在两个文件中 SOA 资源记录之后，分别是 TXT、两个 NS 和两个 MX 资源记录。接下来是三个 CNAME 资源记录，将指向 www.zach.net、ftp.zach.net 和 mail.zach.net 的查询引导至名为 **ns.zach.net** 的系统。接下来的四条资源记录指定了 ns.zach.net 域的两个名称服务器地址和两个邮件服务器。

最后四条资源记录出现在本地 **zach.net** 区域文件中，而不出现在公开区域文件中；它们是本地系统的地址（A）资源记录。不必在每个系统上通过 /etc/hosts 文件保存这些信息，你可以将其保存在 DNS 服务器上，在那里可以轻松地更新。当你使用 DNS 替代 /etc/hosts 时，必须相应地修改 /etc/nsswitch.conf 中的 **hosts** 行（第 495 页）。

```text
$ cat local.net
; zach.net local zone file
;
$TTL 3D
@ IN SOA ns.zach.net. mgs@sobell.com. (
    201311118 ; serial
    8H        ; refresh
    2H        ; retry
    4W        ; expire
    1D )      ; minimum

IN TXT "Sobell Associates Inc."
IN NS ns               ; Nameserver address (unqualified)
IN NS ns.speedy.net.   ; Nameserver address (qualified)
IN MX 10 mail          ; Mail exchange (primary/unqualified)
IN MX 20 mail.max.net. ; Mail exchange (2nd/qualified)
```

```text
ns IN A 192.168.0.1
mail IN A 192.168.0.2

www IN CNAME mail
ftp IN CNAME mail
gw IN CNAME ns

speedy IN A 192.168.0.5
grape IN A 192.168.0.3
potato IN A 192.168.0.4
peach IN A 192.168.0.6
```

zach.net 区域文件的公开版本如下：

```text
$ cat public.net
; zach.net public zone file
;
$TTL 3D
@ IN SOA ns.zach.net. mgs@sobell.com. (
    201311118 ; serial
    8H        ; refresh
    2H        ; retry
    4W        ; expire
    1D )      ; minimum

IN TXT "Sobell Associates Inc."
IN NS ns               ; Nameserver address (unqualified)
IN NS ns.speedy.net.   ; Nameserver address (qualified)

IN MX 10 mail          ; Mail exchange (primary/unqualified)
IN MX 20 mail.max.net. ; Mail exchange (2nd/qualified)

www IN CNAME mail
ftp IN CNAME mail
gw IN CNAME ns

ns IN A 192.168.0.1
mail IN A 192.168.0.2
```

这里有两个反向区域文件，每个文件都以 SOA 和 NS 资源记录开始，随后是每个服务器名称的 PTR 资源记录。该文件的本地版本还列出了本地系统的名称：

```text
$ cat named.local
; "0.168.192.in-addr.arpa" reverse zone file
;
$TTL 3D
@ IN SOA ns.zach.net. mgs@sobell.com. (
    2013110501 ; serial
    8H         ; refresh
    2H         ; retry
    4W         ; expire
    1D )       ; minimum

IN NS ns.zach.net.
IN NS ns.speedy.net.
1 IN PTR ns.zach.net.
2 IN PTR mail.zach.net.
3 IN PTR grape.zach.net.
4 IN PTR potato.zach.net.
5 IN PTR speedy.zach.net.
6 IN PTR peach.zach.net.
```

```text
$ cat named.public
; "0.168.192.in-addr.arpa" reverse zone file
;
$TTL 3D
@ IN SOA ns.zach.net. mgs@sobell.com. (
    2013110501 ; serial
    8H         ; refresh
    2H         ; retry
    4W         ; expire
    1D )       ; minimum

IN NS ns.zach.net.
IN NS ns.speedy.net.
1 IN PTR ns.zach.net.
2 IN PTR mail.zach.net.
```

## 章节总结

DNS 将域名映射到 IP 地址，反之亦然。它在互联网上被实现为一个分层、分布式且复制的数据库。通过在 chroot 容器中运行并使用事务签名（TSIG）和 SELinux，你可以提高实施 DNS 的 BIND 的安全性。

当本地系统上的程序需要查找与域名对应的 IP 地址时，它会调用解析器（resolver）。解析器会查询本地 DNS 缓存（如果可用），然后查询局域网或互联网上的 DNS 服务器。有两种类型的查询：迭代查询和递归查询。当服务器响应迭代查询时，它返回手头现有的信息；它不会查询其他服务器。递归查询会促使服务器在必要时查询其他服务器以给出答案。

有三种类型的服务器。主服务器（Master servers）保存区域数据的主副本，并作为某区域的权威服务器。从服务器（Slave servers）也是权威的，它们从主服务器或其他从服务器复制数据。DNS 缓存不是权威的，它们要么从缓存中回答查询，要么将查询转发给另一台服务器。

DNS 数据库保存域的资源记录。存在许多类型的资源记录，包括 A（地址）、MX（邮件交换）、NS（名称服务器）、PTR（用于执行反向名称解析的指针）和 SOA（权威开始，描述区域）。

## 练习

- 1. 哪种服务器响应递归查询？该服务器是如何工作的？
- 2. 当 Web 浏览器尝试解析 URI 的域部分时，可能返回哪种类型的 DNS 记录？
- 3. MX 资源记录是做什么用的？
- 4. 如何从命令行查找 example.com 的 IP 地址？
- 5. 如果局域网名称服务器不可用，你如何指示 Linux 系统使用位于 192.168.1.254 的本地网络 DNS 缓存，或者使用位于 1.2.3.4 的 ISP 的 DNS 缓存？
- 6. 如何指示 DNS 服务器仅响应来自 137.44.* IP 范围的查询？
- 7. 解析器可能如何尝试查找 example 域的 IP 地址？

## 高级练习

- 8. 你如何设置一个不包含任何官方 InterNIC 分配域名名的私有域名层次结构？
- 9. DNS 的哪个部分最容易受到恶意用户的攻击，原因是什么？
- 10. 当你更改 DNS 条目时，不得不等待 DNS 记录在全球范围内更新通常令人烦躁。你可以通过将 TTL 设置为一个小数来防止这种延迟。为什么将 TTL 设置为一个小数是坏主意？
- 11. 概述一种使用 DNS 支持加密的方法。

## FIREWALLD 和 IPTABLES：设置防火墙

### 本章内容

- firewalld 服务 . . . . . . . . . . . 898
- JumpStart：使用 firewal-config 构建防火墙 . . . . . . . . . . . 900
- firewall-config：防火墙配置窗口 . . . . . . . . 902
- firewall-cmd：从命令行控制 firewalld . . . . . . . . 906
- iptables 简介 . . . . . . . . . . . 908
- iptables 命令的解剖结构 . . . . . . . . . . . 914
- 使用 iptables 构建一组规则 . . . . . . . . . . . 916
- 将规则复制到内核及从内核复制 . . . . . . . . . . . 922
- system-config-firewal：生成一组规则 . . . . . . . . . . . 923
- 使用 NAT 共享互联网连接 . . . . . . . . . . . 924

### 目标

阅读本章后，你应该能够：

- 解释 `firewalld` 和 `iptables` 服务有何不同
- 使用 `firewal-config` 配置基本防火墙
- 使用 `firewall-cmd` 配置基本防火墙
- 描述 `firewalld` 区域的目的
- 解释运行时配置和永久配置之间的区别
- 配置 NAT，使局域网上的多个客户端可以使用单个互联网连接

