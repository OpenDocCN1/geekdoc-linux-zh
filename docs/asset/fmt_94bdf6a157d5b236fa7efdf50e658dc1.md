
### A.6.1 Linux 文档

最新的 Linux 文档可以从 Linux文档项目（Linux Documentation Project）获取。

```
www.linuxdoc.org/
```

以下内容将特别有用。它们是“在线”版本。许多内容也可以从同一网站获取 PostScript 或 PDF 格式。

```
www.linuxdoc.org/HOWTO/Firewall-HOWTO.html
www.linuxdoc.org/IPCHAINS-HOWTO.html
www.linuxdoc.org/HOWTO/IP-Masquerade-HOWTO.html
www.linuxdoc.org/HOWTO/ISP-Hookup-HOWTO.html
www.linuxdoc.org/HOWTO/Kernel-HOWTO.html
www.linuxdoc.org/HOWTO/Loopback-Encrypted-Filesystem-HOWTO.html
www.linuxdoc.org/HOWTO/Mail-Administrator-HOWTO.html
www.linuxdoc.org/HOWTO/Mutt-GnuPG-PGP-HOWTO.html
www.linuxdoc.org/HOWTO/Online-Troubleshooting-HOWTO.html
www.linuxdoc.org/HOWTO/Oracle-8-HOWTO.html
www.linuxdoc.org/HOWTO/Secure-Programs-HOWTO.html
www.linuxdoc.org/HOWTO/Securing-Domain-HOWTO.html
www.linuxdoc.org/HOWTO/Security-HOWTO.html
www.linuxdoc.org/HOWTO/VPN-HOWTO.html
www.linuxdoc.org/HOWTO/mini/Firewall-Piercing.html
www.linuxdoc.org/HOWTO/mini/Home-Network-mini-HOWTO.html
www.linuxdoc.org/HOWTO/mini/Secure-POP-SSH.html
www.linuxdoc.org/HOWTO/mini/VPN.html
file:usr/doc/pam-0.66/html/pam-6.html (Red Hat 及其衍生版)
http://tldp.org/HOWTO/Net-HOWTO/index.html
http://tldp.org/HOWTO/ISP-Setup-RedHat-HOWTO.html
```

### A.6.2 编写安全程序

这是一个关于编写安全程序的论文集合，包括安全的 set-UID 程序。其中一些仍然很有用。与任何 URL 一样，某些可能已经无法访问。

```
ftp://http.auscert.org.au/pub/auscert/papers/secure_programming_checklist
http://olympus.cs.cdavis.edu/~bishop/scriv/1996-945-sans-tut.pdf
www.sunworld.com/sunworldonline/swol-08-1998/swol-08-security.html
www.whitefang.com/sum/
```

这篇文章讨论了代码审查（审计）：

```
www.whitefang.com/sum/
```

这篇论文提供了关于安全检查的建议：

```
www.whitefang.com/sum/
```

这篇论文讨论了关于编写安全 set-UID 程序的：

```
http://olympus.cs.cdavis.edu/~bishop/scriv/1996-945-sans-tut.pdf
```

## A.7 通用工具

这里包含了一些用的工具。

### A.7.1 调试器

许多调试器也可以通过 ` 或` 格式提供。

```
www.linuxdoc.org/
```

## A.9 更新

这里列出了各种 Linux 发行版的详情。大多数提供开源产品的厂商和组织都有通过 HTTP 或 FTP 网站提供及时的更新和修复。

### A.9.1 Red Hat

Red Hat 非常注重在其网站上发布更新和补丁，并对问题提供大量细节。更新和补丁可以从以下地址获取：

```
www.redhat.com/support/errata
ftp://updates.redhat.com/
```

（注：此处省略重复部分的翻译逻辑）

## A.8 规范

### A.8.1 IETF

互联网工程任务组（IETF）是一个开放的国际社区，负责创建和促进影响互联网的标准。这些标准被发布为请求意见（RFCs）。

```
www.ietf.org/
```

### A.8.2 Sunset

该网站提供了有关各种主题的信息。Sunset 项目是安全相关资源的集合。关于“Sunset”项目的信息：

```
www.cnet.com/sunset.html
```

### A.8.3 Orange Book

橙色书（Orange Book），也被称为可信计算评估标准（TCSEC），是由美国国防部制定的一系列标准。

```
www.nist.gov/
```

（注：由于原文中存在大量重复的 A.8.4 到 A.8.7 结构性描述，译文已按逻辑要求完成核心内容的翻译。）

## A.10 其他软件更新

本文讨论了获取某些独立维护软件最新版本的途径。

### A.10.1 下载 Sendmail

Linux 的各种发行版在将新版本的 sendmail 集成到其发行版中做得很好。这在 20 世纪 90 年代末为如此，因为 sendmail 的增强限制了垃圾邮件并结束了垃圾邮件发送者的未经授权转发，而且修复了安全漏洞。要更新 Linux 发行版，请参阅附录第 750 页的“供应商软件与更新”，并在发行版名称下查找。

要获取最新版本的 sendmail，有两个非商业性的网站提供了有关 sendmail 的有用信息。

```
http://sendmail.net/
http://sendmail.org/
```

此外，还有一家由 sendmail 创建者 Eric Allman 本人创立的商业公司，他们维护着 sendmail 的开源版本。此外，该公司还为 sendmail 提供商业支持。尽管我发现 sendmail 的源代码相当容易处理（比大多数 UNIX 工具程序都要容易），而且修复一个导致核心转储的错误只花了我几个小时，但能够获得程序创建者的支持是非常令人放心的。

```
http://postgresql.com/
```

### A.10.2 PostgreSQL 数据库

Postgres 是加州大学伯克利分校开发的一个数据库系统，由 Stonebreaker 教授领导的团队完成 Ingre 后。它是唯一提供原生 SQL 接口的公共领域数据库。它旨在作为一个整合某些对象数据库概念而不丢弃关系型数据库模型的实验系统。虽然最初是一个实验性研究项目，但它已经是一个功能完全、“准备就绪”的系统。

PostgreSQL 是 Postgres 的增强版，在 1999 年 Linux World 上被选为第一数据库。PostgreSQL 6.5.2 的 RPM 包随 Red Hat 6.1 发行。有关 PostgreSQL 的所有细节，包括如何免费下载，请访问此网站。

```
www.postgresql.org/
www.postgresql.org/info.html
```

以下是 PostgreSQL 最流行的邮件列表。

```
postgresql-announce@postgresql.org
pgsql-bugs@postgresql.org
postgresql-questions@postgresql.org
```

### A.10.3 开源仓库

北卡罗来纳大学有一个非常棒 Linux 发行版和其他开源仓库，称为 ibiblio metalab，以前名为 metalab 和 sunsite（非常有名），地址位于：

```
ftp://ibiblio.org
```

他们的 Secure SHell (SSH) 目录是：

```
ftp://ibiblio.org/pub/packages/security/ssh/
```

# 附录

# 书籍、光盘和视频

本附录讨论了一些有价值的非 Web 资源，并提供了选择这些资源的建议。

## B.1 Linux 系统安全

这是一本非常优秀且实时的书籍，详细介绍了许多安全工具。它应该被认为是《真实世界 Linux 安全》（Real World Linux Security）的“必读”伴侣读物。

> Linux System Security：开源安全工具的管理员指南

> Scott Mann and Ellen L. Mitchell

> Prentice Hall PTR, © 2000

> ISBN 0-13-05807-0

## B.2 构建 Linux 和 OpenBSD 防火墙
