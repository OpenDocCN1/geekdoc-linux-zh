
```bash
root@kali-2019:~# dnsenum -f /usr/share/dnsenum/dns.txt kali.org
Smartmatch is experimental at /usr/bin/dnsenum line 698.
Smartmatch is experimental at /usr/bin/dnsenum line 698.
dnsenum VERSION:1.2.4

------ kali.org ------

Host's addresses:

kali.org.                  60    IN   A   192.124.249.10

Name Servers:

ns1.no-ip.com.             11842  IN   A   194.62.181.53
ns3.no-ip.com.              10611  IN   A   204.16.255.53
ns4.no-ip.com.              10973  IN   A   204.16.254.53
ns5.no-ip.com.              17082  IN   A   194.62.181.53
ns5.no-ip.com.              12491  IN   A   194.62.180.53

Mail (MX) Servers:

alt1.aspmx.l.google.com.     108  IN   A   209.85.144.27
alt3.aspmx.l.google.com.     107  IN   A   64.233.100.26
alt2.aspmx.l.google.com.     107  IN   A   74.125.141.26
aspmx.l.google.com.          205  IN   A   172.217.214.26
alt4.aspmx.l.google.com.     293  IN   A   74.125.193.26

archive.kali.org.       60      IN      CNAME   hera.kali.org.
hera.kali.org.         60      IN      A       192.99.45.148
backup.kali.org.       60      IN      CNAME   polyhymnia.kali.org.
polyhymnia.kali.org.   60      IN      A       54.39.103.103
bugs.kali.org.         60      IN      A       192.124.249.169
forums.kali.org.       60      IN      A       192.124.249.12
http.kali.org.         60      IN      CNAME   hebe.kali.org.
hebe.kali.org.         60      IN      A       192.99.200.113
mail.kali.org.         60      IN      CNAME   apollo.kali.org.
apollo.kali.org.       60      IN      A       23.239.31.92
old.kali.org.          60      IN      CNAME   tersiphore.kali.org.
tersiphore.kali.org.   60      IN      A       54.39.49.227
pan.kali.org.          60      IN      A       167.114.101.148
www.kali.org.          60      IN      A       192.124.249.10

kali.org class C netranges:

23.239.31.0/24
54.39.49.0/24
54.39.103.0/24
167.114.101.0/24
192.99.45.0/24
192.99.200.0/24
192.124.249.0/24
```

在这种情况下，让我们使用 `www.kali.org`。我们将这样编写命令：

`kali> dnsenum.pl -f /usr/share/dnsenum/dns.txt kali.org`

如下图所示，一旦按下回车，`dnsenum` 就开始枚举 `www.kali.org` 的域名服务器和邮件服务器。然后，它尝试使用我们提供的潜在子域名列表和 C 类网络地址范围（Class C netranges）来暴力破解子域名。最后，它尝试进行区域传输，但未成功。

```text
**Name Servers:**

ns1.hastydns.com. 11 IN A 66.135.47.136

**Mail (MX) Servers:**

**Trying Zone Transfers and getting Bind Versions:**

Trying Zone Transfer for hakin9.com on ns2.hastydns.com...
AXFR record query failed: connection failed

Trying Zone Transfer for hakin9.com on ns1.hastydns.com ...
AXFR record query failed: connection failed
```

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_179_0.png)

## 查询目标的 DNS 缓存以确定其杀毒软件

既然我们已经开始了解如何利用 DNS 服务来获取信息，让我们看看 DNS 在提供目标信息方面的另一个更高级用途。

我收录这项技术并非因为其实际可行性，而是为了其灵巧性和创造性——这两个大师级黑客必不可少的特质。

作为一名黑客，了解目标正在运行什么杀毒软件往往至关重要。除非你创建或购买了零日漏洞利用工具，否则它很可能会被杀毒软件检测并隔离。结果，你几天的、几周的甚至几个月的努力将付之东流。

并非所有的杀毒软件都一样！有些很好，有些很差。有些能检测某些恶意软件，有些则检测其他的。因此，一种攻击可能对某一种杀毒软件有效，而对另一种无效。如果我们能预先知道目标使用的是哪种杀毒软件，就可以量身定制一种能够规避该软件的攻击。

当公司拥有自己的 DNS 服务器时，该服务器会缓存每位员工发出的每个 DNS 查询。如果我们能检查 DNS 缓存，就能看到所有被查询过的域名。这意味着，如果我们能检查 DNS 缓存，就可以确定哪些杀毒软件域名（如 Symantec、McAfee、Kaspersky 等）被查询过，哪些没有。目标公司正在使用列表中的一个或所有杀毒软件域名。我们不知道具体是哪个，但我们知道，列表中未列出的杀毒软件公司未被使用。

仅凭这些信息，就可以帮助我们确定哪种攻击有效。

由于这属于中级到高级的侦察技术，我只留下一个链接供你深入学习：[https://www.hackers-arise.com/single-post/2016/05/23/How-to-Use-Recon-to-Determine-the-Target-s-AV-Software-1]

## 摘要

DNS 系统可以成为关于目标的重要信息库，包括域名服务器、邮件服务器以及许多子域名。其中许多子域名可能并不明显，目标公司可能认为这些子域名无法被查看，因为并没有任何链接指向它们。在很多时候，这些子域名可能包含对黑客而言机密且极具价值的信息。

### p0F 或被动操作系统检测

在对目标进行侦察的过程中，我们需要最关键的要素之一，就是目标的操作系统。大家应该已经明白，针对 MacOS 的漏洞无法用于 Windows 系统，反之亦然。可能不明显的是，针对 Windows Vista 的漏洞在 Windows 7 系统上可能无法利用。在许多情况下，针对 Windows 7 SP1 的漏洞在 Windows 7 SP2 上也可能无法利用。

我想说明的要点是，了解目标的操作系统对我们取得成功至关重要。如果没有这些信息，我们很可能只是在浪费时间精力。

在本课中，我们将介绍一种名为 `p0F` 的工具。这个名字是“被动操作系统指纹识别”（passive operating system fingerprinting）的首字母缩写。`p0F` 依赖于对各操作系统 TCP/IP 协议栈如何构建和实现数据包的深入理解，从而确定发送方的操作系统。因此，它是完全被动的，我们不需要用数据包或其他任何方式触碰目标系统。该工具使我们能够在不向目标发送任何数据包或探针的情况下确定目标操作系统。

## TCP/IP 基础
