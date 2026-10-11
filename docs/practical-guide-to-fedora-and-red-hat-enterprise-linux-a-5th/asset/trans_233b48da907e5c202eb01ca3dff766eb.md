

为了使 `named.conf` 更容易理解和维护，不同 View 部分中的区域可以具有相同的名称，但使用不同的区域文件。示例中的本地和公共 View 部分都包含名为 **zach.net** 的区域：公共的 **zach.net** 区域文件名为 **public.net**，而本地的则名为 **local.net**。

日志（Logging）部分在第 808 页有详细描述。

定义 **zach.net** 的区域文件与前面示例中的类似；公共文件是本地文件的一个子集。在两个文件中，SOA 资源记录之后分别是 TXT、两个 NS 以及两个 MX 资源记录。接下来是三个 CNAME 资源记录，它们将指向 www.zach.net、ftp.zach.net 和 mail.zach.net 的查询引导至名为 **ns.zach.net** 的系统。随后的四个资源记录为 ns.zach.net 域名指定了两个名称服务器地址和两个邮件服务器。

最后四个资源记录仅出现在本地的 **zach.net** 区域文件中，而不存在于公共区域文件中；它们是本地系统的地址（A）资源记录。与其在每个系统的 `/etc/hosts` 文件中保存这些信息，不如将其保存在 DNS 服务器上，这样更易于更新。当你使用 DNS 代替 `/etc/hosts` 时，必须修改 `/etc/nsswitch.conf` 中的 `hosts` 行（第 455 页）。

```
$ cat local.net
; zach.net local zone file

    TTL     3D
    @       IN      SOA     ns.zach.net. mgs@sobell.com. (
                        20051118  ; serial
                        8H        ; refresh
                        2h        ; retry
                        4W        ; expire
                        1D )      ; minimum

        IN      TXT     "Sobell Associates Inc."
        IN      NS      ns ; Nameserver address (unqualified)
        IN      NS      ns.speedy.net. ; Nameserver address (qualified)
        IN      MX      10 mail      ; Mail exchange (primary/unqualified)
        IN      MX      20 mail.max.net. ; Mail exchange (2nd/qualified)

www     IN      CNAME   ns
ftp     IN      CNAME   ns
mail    IN      CNAME   ns

ns      IN      A       192.168.0.1
        IN      A       192.168.0.6
        IN      MX      10 mail
        IN      MX      20 mail.max.net.

speedy  IN      A       192.168.0.1
grape   IN      A       192.168.0.3
potato  IN      A       192.168.0.4
peach   IN      A       192.168.0.6
```

**zach.net** 区域文件的公共版本如下：

```
$ cat public.net
; zach.net public zone file
;
$TTL    3D
@       IN      SOA     ns.zach.net. mgs@sobell.com. (
                        20051118  ; serial
                        8H        ; refresh
                        2H        ; retry
                        4W        ; expire
                        1D )      ; minimum

        IN      TXT     "Sobell Associates Inc."
        IN      NS      ns ; Nameserver address (unqualified)
        IN      NS      ns.speedy.net. ; Nameserver address (qualified)
        IN      MX      10 mail      ; Mail exchange (primary/unqualified)
        IN      MX      20 mail.max.net. ; Mail exchange (2nd/qualified)

www     IN      CNAME   ns
ftp     IN      CNAME   ns
mail    IN      CNAME   ns
ns      IN      A       192.168.0.1
        IN      A       192.168.0.6
        IN      MX      10 mail
        IN      MX      20 mail.max.net.
```

有两个反向区域文件，每个文件都以 SOA 和 NS 资源记录开头，随后是每个服务器名称对应的 PTR 资源记录。此文件的本地版本还列出了本地系统的名称：

```
$ cat named.local
; "0.168.192.in-addr.arpa" reverse zone file
;
$TTL    3D
@       IN      SOA     ns.zach.net. mgs@sobell.com. (
                        2005110501  ; serial
                        8H        ; refresh
                        2H        ; retry
                        4W        ; expire
                        1D )      ; minimum

        IN      NS      ns.zach.net.
        IN      NS      ns.speedy.net.
1       IN      PTR     gw.zach.net.
1       IN      PTR     www.zach.net.
1       IN      PTR     ftp.zach.net.
1       IN      PTR     mail.zach.net.
1       IN      PTR     speedy.zach.net.
3       IN      PTR     grape.zach.net.
4       IN      PTR     potato.zach.net.
6       IN      PTR     peach.zach.net.
```

## 章节总结

DNS 将域名映射为 IP 地址，反之亦然，它在 Internet 上被实现为一个分层、分布式和复制的数据库。尽管实现 DNS 的 BIND 存在安全问题，但你可以通过在 chroot 牢笼中运行它以及使用事务签名（TSIGs）和 SELinux 来提高其安全性。

当本地系统上的程序需要查找与域名对应的 IP 地址时，它会调用解析器（resolver）。解析器首先查询本地 DNS 缓存（如果可用），然后查询局域网或 Internet 上的 DNS 服务器。查询有两种类型：迭代（iterative）和递归（recursive）。当服务器响应迭代查询时，它返回手头拥有的任何信息；它不会查询其他服务器。递归查询则会导致服务器在必要时查询其他服务器以提供答案。

有三种类型的服务器。主服务器（Master servers）持有区域数据的主副本，对于某个区域是权威的。从服务器（Slave servers）也是权威的，它们从主服务器或其他从服务器复制数据。DNS 缓存不是权威的，它们要么从缓存中回答查询，要么将查询转发给另一台服务器。

DNS 数据库存储域的资源记录。存在许多类型的资源记录，包括 A（地址）、MX（邮件交换）、NS（名称服务器）、PTR（用于执行反向名称解析的指针）和 SOA（权威起始，描述该区域）。

## 练习

- 1. 哪种服务器响应递归查询？
- 2. 当 Web 浏览器尝试解析 URL 中的域名部分时，可能返回哪种类型的 DNS 记录？
- 3. MX 资源记录用于什么目的？
- 4. 如何从命令行查找 example.com 的 IP 地址？
- 5. 如果局域网名称服务器不可用，如何指示 Linux 系统使用位于 192.168.1.254 的本地网络 DNS 缓存，或位于 1.2.3.4 的 ISP DNS 缓存？
- 6. 如何指示 DNS 服务器仅响应来自 **137.44.*.*** IP 范围的查询？
- 7. 解析器可能会如何尝试查找 **example** 域名的 IP 地址？

### 高级练习

- 8. 如何设置一个不包含任何官方 InterNIC 分配域名的私有域名层次结构？
- 9. DNS 的哪部分最容易受到恶意用户的攻击，原因是什么？
- 10. 当你更改 DNS 条目时，不得不等待全球范围内的 DNS 记录更新往往令人沮丧。你可以通过将 TTL 设置为一个较小的数值来防止这种延迟。为什么将 TTL 设置为较小的数值是一个坏主意？
- 11. 概述一种使用 DNS 支持加密的方法。

## 25 iptables：设置防火墙

### 本章内容

- iptables 的工作原理
- 规则、匹配项、目标和链
- 网络数据包
- 跳转和目标
- JumpStart：使用 system-config-firewall 构建防火墙
- iptables 命令的解析
- 构建规则集
- system-config-firewall：生成规则集
- 使用 NAT 共享互联网连接

**iptables** 实用程序在 Linux 内核中构建和操作网络数据包过滤规则。你可以使用 **iptables** 创建一个保护系统免受恶意用户侵害的防火墙，并设置 NAT（网络地址转换，第 1095 页），这允许多个系统共享单一的互联网连接。**iptables** 实用程序灵活且可扩展，允许你设置简单和复杂的网络数据包过滤解决方案。它提供连接跟踪（状态化数据包过滤），允许你根据连接状态处理数据包。例如，你可以设置规则以拒绝试图打开新连接的入站数据包，并接受作为本地发起连接的响应而到达的入站数据包。**iptables** 基础软件包中未包含的功能可以通过 patch-o-matic 程序以补丁形式获得。

完全理解 **iptables** 所需的一些概念超出了本书的范围。虽然你可以在不同的几个层面使用 **iptables**，但本章仅介绍基础。不过，本章中有一些章节深入探讨了可能需要额外理解或解释的领域。如果某个概念不清楚，请参见第 822 页“更多信息”中的一个资源。

