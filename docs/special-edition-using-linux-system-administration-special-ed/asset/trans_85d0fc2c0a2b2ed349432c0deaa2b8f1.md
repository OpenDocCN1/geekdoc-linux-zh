

## 安装适用于 Apache 的 FrontPage 扩展后 PHP 停止工作

当你安装 FrontPage 扩展时，它们会改变一些 Apache 结构。在此更改之后，PHP 将需要重新编译。在你的 PHP 源代码目录中，使用以下命令重新编译并安装 PHP：

```text
# make clean
# make
# make install
```

之后，重启 Apache。

## Apache 将 PHP 文件显示为源代码

如果你从 Apache 服务器请求一个 PHP 文件，而它返回的是该文件的源代码而不是处理后的结果，那么你在 Apache 配置文件 srm.conf 中缺少一条适当的 AddType 指令。在 srm.conf 中添加一条类似以下的条目，然后重启 Apache：

```text
AddType application/x-httpd-php3 .php3
```

## PHP 因缺少库而编译失败

如果你尝试使用外部功能构建 PHP，例如 GD 支持、FreeType 或 LDAP，则必须安装相应的开发库并使其可用，PHP 才能成功编译。部分库及其位置的列表可以在 http://www.php.net/FAQ.php3#1 的 PHP FAQ 中找到，包括以下内容：

- LDAP：ftp://ftp.openldap.org/pub/openldap/openldap-stable.tgz
- Berkeley DB2：http://www.sleepycat.com/
- GD：http://www.boutell.com/gd/#buildgd
- mSQL：http://www.hughes.com.au/
- MySQL：http://www.mysql.com/
- IMAP：ftp://ftp.cac.washington.edu/imap/old/
- FreeType：http://www.freetype.org/
- ZLib：http://www.cdrom.com/pub/infozip/zlib/
- expat XML 解析器：http://www.jclark.com/xml/expat.html
- PDFLib：http://www.pdflib.com
- mcrypt：ftp://argeas.cs-net.gr/pub/unix/mcrypt/
- mhash：http://sasweb.de/mhash/
- t1lib：http://www.neuroinformatik.ruhr-uni-bochum.de/ini/PEOPLE/rmz/t1lib/t1lib.html
- dmalloc：http://www.dmalloc.com/
- aspell：http://metalab.unc.edu/kevin/aspell/
- Readline：ftp://prep.ai.mit.edu/pub/gnu/readline/

## PHP 无法连接到我的数据库服务器

假设你为服务器使用了正确的用户名和密码，那么当 PHP 服务器和数据库服务器位于网络中的不同机器上时，此问题最有可能发生。如果你的数据库服务器根据连接来源主机进行限制，请务必将 PHP 服务器添加到数据库服务器上的有效客户端列表中。否则，连接将被拒绝。

此外，请确保 PHP 服务器上的主机表（/etc/hosts）中有数据库服务器的条目，并且数据库服务器上的主机表中有 PHP 服务器的条目。

使用 PHP 访问数据库时的另一个问题是，你的 PHP 安装可能没有针对你要访问的数据库服务器编译相应的库。在这种情况下，你应该按照前面“安装 PHP”一节中的说明重新编译 PHP。

## 第 26 章：新闻服务

本章包括

- Usenet 简史 570
- 新闻组层级 570
- 硬件要求 571
- 安装 INN 2.2.1 571
- INN 概述 572
- 配置 INN 574
- 理解 INN 日志文件 586
- 管理 INN 587
- 故障排除 588

### Usenet 简史

1979 年末，在带有 UUCP 的 V7 UNIX 发布后不久，北卡罗来纳大学的研究生 Steve Bellovin 发布了第一个版本的新闻软件。它被安装在两台计算机上，一台在北卡罗来纳大学，另一台在杜克大学。第一个版本是用 shell 脚本编写的，后来用 C 语言重写。这使得两所大学之间能够进行共享讨论。

自那时起，人们编写了许多版本的新闻软件；其中主要的有 A News、B News、C News、NNTP 和 INN。此外，还有一些商业化的新闻类软件实现，例如 DNews 和 Netscape Collabra。

1986 年，一个使用 TCP/IP 上的 NNTP 协议而非 UUCP 进行新闻传输的新闻软件发布。它被称为 NNTP，由加州大学圣迭戈分校开发。不久之后，1987 年，多伦多大学开发了一个非常流行的新闻版本，称为 C News。C News 在互联网上被广泛使用。

目前互联网上几乎唯一使用的新闻软件是 INN。它最初由 UNET 的 Rich Salz 开发，并于 1992 年发布。它同时支持基于 NNTP 和 UUCP 的新闻投递。

自 INN 1.4 版本以来，互联网软件联盟（Internet Software Consortium）负责该软件的开发。现在 INN 已到 2.2.1 版本，可以从 ftp://ftp.isc.org/isc/inn 获取。我们将在本章中介绍 INN 2.2.1 版本。

### 新闻组层级

互联网上新闻组的当前结构被称为 Usenet。Usenet 是一个交换新闻文章的站点去中心化集合。成员站点上的用户阅读和撰写文章，并将新文章发布到本地服务器，然后本地服务器再一个接一个地将它们馈送给 Usenet 社区的其他站点。

新闻组按层级结构组织，详细程度各不相同。组的名称表示该组在层级中的位置。例如，一个名为 `comp.languages` 的组位于 comp 类别中，可能一般性地讨论计算机语言；而 `comp.languages.pascal` 组则更为精细，它是 comp 类别中 languages 子类别的一部分，讨论 Pascal 语言。

最著名且使用最广泛的顶级类别如下：

- **alt**：替代主题
- **comp**：计算机主题
- **rec**：娱乐主题
- **soc**：社会与社交主题

此外，还存在许多有针对性的顶级类别，包括国家顶级类别，如用于加拿大讨论的 can，以及与主题相关的类别，如用于幼儿园到 12 年级讨论的 k12。

除了这些公共 Usenet 类别之外，Usenet 站点还可以创建自己的本地类别，这些类别既可保密，也可提供给希望接收这些类别中新闻组馈送的站点共享。

### 硬件要求

运行一个可用的 INN 新闻服务器所需的硬件取决于两个因素：

- 你计划接收的新闻馈送的大小：你计划接收完整的 Usenet 新闻馈送，还是只接收选定组的部分馈送？
- 你预期将使用该服务器的并发新闻阅读器数量。

对于部分馈送站点，系统可以小到只有一台 Pentium II 300，配备 256MB 内存和 16GB 的 ultra-wide SCSI-2 硬盘空间，并通过 T1 连接与你的新闻提供商相连。通常，这种部分馈送不会接收 alt.* 层级和任何 *binaries 组。

在高端的全馈送站点，拥有大量用户时，很容易就需要 4 个 Pentium III 500 CPU、2GB 内存和超过 1TB 的硬盘容量。这些硬盘可以是 ultra-wide SCSI-2 硬盘，通过多个 ultra-wide SCSI 控制器（如 Adaptec 2940 UW 控制器）连接。对于全馈送站点，建议通过 T3 连接接入互联网，或者至少你必须有 4 或 5 条到新闻提供商的 T1 连接。

### 安装 INN 2.2.1

> **提示**
> 
> 要安装 INN，你首先必须安装 Perl 5.004 或更高版本。Perl 是所有主要 Linux 发行版的一部分；你可以从 http://www.perl.com/ 获取最新版本的 Perl。

预编译的 INN 软件随许多标准 Linux 发行版一起打包，例如 Red Hat 6.2。你可以使用 RPM 软件包添加命令将其安装到你的服务器上。但是，如果你想从源代码构建 INN 二进制文件，可以按照以下步骤操作：

1. 从 `ftp://ftp.isc.org/isc/inn/inn-2.2.1.tar.gz` 下载 INN 存档到你系统上的方便位置，例如 `/usr/local/src`。
2. 将当前目录更改为你下载 INN 的目录：

   ```text
   # cd /usr/local/src
   ```

