

配置名称服务器。在名称服务器字段中，输入 127.0.0.1。如果您想为解析器添加任何高级功能，请参考本章的第一部分，了解如何操作。

## 一个简单的域名配置

本节的目的是配置一个域名服务器。您可以先从创建一个仅缓存的名称服务器开始，就像您在上一节中学到的那样。然后，您将配置一个简单的域名配置。

首先，您应该为名称服务器选择一个名称。选择一个不会与您的 ISP 主机名称服务器或任何其他域名冲突的名称。在下面的示例中，您将使用 sampledomain.com 作为您的域名。

关于配置文件，您应该首先在 /etc/named.conf 文件中为区域添加一个条目。该条目应如下所示：

```
zone "sampledomain.com" IN {
    type master;
    file "sampledomain.com";
    notify no;    //When you make sure everything is fine, turn this to on..
};
```

下一步是编辑 /var/named/sampledomain.com 文件。此文件应包含有关该域上所有主机的信息。尽管这是一个简单的配置示例，但它看起来可能有点大。以下是 /var/named/sampledomain.com 文件的列表：

```
1 $ORIGIN sampledomain.com.
2 @    IN    SOA   ns.sampledomain.com. root.sampledomain.com. (
3                43      ; serial
4                8H      ; refresh
5                2H      ; retry
6                1W      ; expire
7                1D )    ; minimum
8 ;
9         TXT     "Sample Domain Configuration"
10        NS      ns    ; Inet Address of name server
11        NS      ns.otherdomain.com.
12        MX      10 mail ; Primary Mail Exchanger
13        MX      20 mail.otherdomain.com. ; Secondary Mail Exchanger
14 gw     A       192.168.0.1
15        HINFO   "Cisco" "IOS"
16        TXT     "The router"
17 ns     A       192.168.0.2
18        MX      10 mail
19        MX      20 mail.otherdomain.com.
20        HINFO   "K6-3" "SuSE Linux 6.3 - Kernel 2.4"
21 www    CNAME   ns
22 printer A      192.168.0.3
23      MX      10 mail
24      MX      20 mail.otherdomain.com.
25      HINFO   "P6" "SuSE Linux 6.2 - Kernel 2.2"
26      TXT     "The print server"
27 mail  A       192.168.0.4
28      MX      10 mail
29      MX      20 mail.otherdomain.com.
30      HINFO   "P5/133" "NT/4"
31 ftp   A       192.168.0.5
32      MX      10 mail
33      MX      20 mail.otherdomain.com.
34      HINFO   "P6" "Corel Linux 2.0 - Kernel 2.4"
```

此文件中有一些新的资源记录，将在下一节中逐一讨论：

- **A—** A 记录直接将指定的 IP 分配给主机名。在此上下文中，A 是 address 的缩写。
- **CNAME—** 规范命名是一种为每台机器提供多个名称的方法。在此示例中，www 是 ns 的别名。您不应让 MX、CNAME 或 SOA 记录引用 CNAME 记录。CNAME 记录始终应仅引用 A 记录。许多系统管理员建议根本不要使用 CNAME。
- **HINFO—** 此资源记录用于主机机器信息。其第一部分是 CPU 类型，第二部分是机器正在运行的操作系统。
- **MX—** 邮件交换器告诉邮件系统将发往 user@sampledomain.com 的邮件发送到何处。编号最低的 RR 具有第一优先级。在此示例中，第 10 行表示 mail.sampledomain.com 是主邮件服务器。如果失败，则使用次要邮件服务器。
- **TXT—** 这是您想要添加到对主机进行评论的注释。

正如您可能已经注意到的，该文件管理 sampledomain.com 上的所有其他主机。但是，如果您有主机名但没有 IP，就会遇到问题。在这种情况下，您需要一个反向文件来将主机映射到 IP 地址：

```
$ORIGIN 0.168.192.in-addr.arpa.
@       IN      SOA     sampledomain.com. root.sampledomain.com. (
                        43      ; serial
                        8H      ; refresh
                        2H      ; retry
                        1W      ; expire
                        1D )    ; minimum
                        NS      sampledomain.com.
1       PTR     gw.sampledomain.com.
2       PTR     sampledoman.com.
2       PTR     www.sampledomain.com.
3       PTR     printer.sampledomain.com.
4       PTR     mail.sampledomain.com.
5       PTR     ftp.sampledomain.com.
```

最后，您必须在 /etc/named.conf 文件中为此反向文件添加一个条目：

```
zone "0.168.192.in-addr.arpa" {
    type master;
    file "192.168.0";
};
```

编辑完文件后，重新启动 named 以使配置生效。

## 您的角色

作为 DNS 的管理员，您的角色是跟踪网络上发生的更改。您应该检查主机的完整性，并确保没有两个主机具有相同的名称。您可能希望自己命名主机并检查网络上发生的更新。

## 从 NIC 注册域名

如果您想要一个顶级域名，您必须从 NIC 注册。它很容易注册一个域名，只要它尚未被占用。您所要做的就是访问 http://www.internic.com 并按照网站上的步骤操作。您应该注意的一个重要事实是，这是一项付费服务。如果您忘记支付账单，就不会有人能够通过您的站点名称联系到您。

> 注意 发生过一个有趣的情况，微软忘记为 hotmail 域名支付账单。数百万人无法访问他们的电子邮件。来自田纳西州安提阿的程序员和 Linux 爱好者 Michael Chaney 为微软支付了账单，以便他可以检查自己的邮件！

## 域名黑市

当您尝试注册一个您认为独特的域名，却发现它已被占用时，可能会感到惊讶。您可能会尝试联系域名所有者，发现她愿意出售它——以非常高的价格。有些人通过出售他们的域名赚取了巨额利润，因为新进入互联网的大公司和机构愿意支付高价来注册他们的商业名称。如果您将来在业务中使用互联网，请考虑尽早注册您的域名。

## BIND 故障排除

*BIND 似乎长时间停滞。有时它会无缘无故地关闭。发生了什么？*

据报道，BIND 8.0 在与具有活动目录的 Windows 2000 操作系统通信时存在一些问题。您必须至少更新到 BIND 8.2。您可以从 SuSE FTP 或从 BIND 主页 http://www.isc.org/products/BIND/ 下载最新的 BIND。

*我想从 BIND 4.xx 升级到 BIND 8.xx，但我有很大的配置文件，不想重新配置所有这些。*

SuSE Linux 附带的一个名为 named-bootconf 的实用程序可以帮助您。此脚本将自动将您的设置更改为新设置。

*我想知道有关 BIND 的所有信息。我可以在哪里找到更多关于 BIND 的信息？*

http://www.isc.org/services/training/ 网站为希望了解更多关于 BIND 的系统管理员提供培训。您也可以查看随 SuSE Linux 提供的文档以获取更多信息。●

## 通过 Samba 与 Windows 的连接

### 本章内容

- 如何连接到 Windows 机器 302
- 安装 Samba 302
- 配置 Samba 303
- 高级 Samba 311
- 使用 Samba 打印到 Windows 机器 317
- 使用 Swat 配置 Samba 318
- 故障排除 320

## 如何连接到 Windows 机器

用户经常发现自己在包含 Microsoft Windows PC 的网络上安装 SuSE Linux。会出现用户希望与这些 PC 交换文件和打印服务的情况。用户始终可以使用 FTP 在 Linux 机器和 Windows 机器之间交换文件，但这并不方便。Windows 机器使用一种特殊的网络协议，使它们能够相互共享文件和打印机。这种协议以前称为 Server Message Block (SMB)，现在称为 Common Internet File System (CIFS)。如果您曾经在网络上使用过 Windows 机器，您就熟悉网络邻居。网络邻居使您能够看到网络上的所有基于 Windows 的 PC，连接到它们并交换文件和服务。

Microsoft Windows PC 使用 SMB 协议相互通信。Andrew Tridgell 于 1991 年启动了一个项目，目前称为 Samba。Samba 是 Andrew 等人通过逆向工程 SMB 协议的结果。Samba 在 UNIX 机器上运行，使其能够与网络上的 Microsoft Windows PC 共享文件和打印机。

Samba 被认为是开源社区生产的最杰出的项目之一。它实现了 Microsoft Windows PC 与 UNIX 世界其他部分以及反之的集成。Samba 提供了两个世界之间的缺失环节，并且做得很好。

即使 SMB 已更名为 CIFS，其余的 UNIX 世界仍然将其称为 SMB。因此，为了兼顾两个世界，我们将称其为 SMB/CIFS。

**提示** 如果您想知道 Samba 这个名字到底是怎么来的，您可能会被答案惊讶。Andrew Tridgell 最初称其为 SMB server，但已有产品使用该名称。因此，他运行了一个命令，搜索字典中包含字母 S.M.B. 的所有单词。列出了一个单词列表，他选择了 Samba。

## 安装 Samba

安装 Samba 应该不会太困难，因为它已经随 SuSE Linux 预打包。很有可能它已经安装在您的系统上。运行 Samba 的软件包要求如下：

- **软件包要求：**
- **系列 n：**
  - Samba
- **内核要求：**
  - 文件系统、网络文件系统、SMB 文件系统支持（仅当您计划访问 Windows 共享时）

