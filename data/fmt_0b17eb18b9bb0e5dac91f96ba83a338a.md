
Ubuntu 自带 Apache 2.0，且该服务器（命名为 `httpd`）包含在本书的 CD-ROM 和 DVD 中。你可以从 Ubuntu FTP 服务器、通过 `Synaptic` 获取最新版本的 Apache 软件包，或者通过从 Apache 网站获取源代码并自行编译。要确定系统中所包含的 Apache 版本，请像这样使用 Web 服务器的 `-v` 命令：

```
$ /usr/sbin/httpd -v
Server version: Apache/2.0.50
Server built: Jun 29 2004 11:55
Server's Magic Number: 2003
Architecture: 32-bit
Server compiled with:
```

输出显示了版本号、编译日期时间、平台以及编译期间使用的各种选项。你可以使用 `-v` 查看版本信息。

# 安装 Apache 服务器

你可以通过 `APT` 安装 Apache，或者从源代码自行编译。Apache 可以构建在任何类 Unix 操作系统和 Windows 上。如果你正准备安装新版本的 Apache，应该关闭旧服务器。即使旧服务器不太可能干扰安装过程，关闭它也能确保没有问题。

## 使用 APT 安装

你可以通过 `APT` 安装 Apache，或者从源代码自行编译。

## 自行编译源码

你可以从 `http://apache.org/` 直接下载源码。编写时的最新版本 `2.2` 是一个 6MB 的压缩包。在获取 tar 包后，你必须将其放入临时目录，如 `/tmp`。解压 tar 包会创建一个名为 `apache_version` 的目录。

## 使用 configure 编译 Apache

要通过这种方式构建 Apache，在刚创建的目录中运行 `./configure` 脚本。你可以提供 `--prefix` 参数将其安装在默认目录 `/usr/local/apache/` 之外的目录中。使用此命令：

```
./configure --prefix=/usr/local/apache/
```

这会生成用于编译服务器代码的 `Makefile`。

# 第三部分

# 作为服务器的 Ubuntu

本部分包含

- 第 20 章 Apache Web 服务器管理 453
- 第 21 章 数据库服务管理 491
- 第 22 章 文件与打印 519
- 第 23 章 使用 FTP 进行远程文件服务 545
- 第 24 章 电子邮件处理 589
- 第 25 章 代理与反向代理 607
- 第 26 章 LDAP 617

# 第 20 章

# Apache Web 服务器管理

- 关于 Apache Web 服务器
- 安装 Apache 服务器
- 启动与停止 Apache
- 运行时服务器配置设置
- 文件系统认证与访问控制
- Apache 模块
- 虚拟主机
- 日志记录
- 动态内容
- 用于 Ubuntu 的其他 Web 服务器
- 参考文献

## Apache Web 服务器

本章涵盖了 Apache Web 服务器的配置和管理。本章包括了服务器一些主要组件的概述，并讨论了基于文本和图形界面的服务器配置。你将看到如何通过命令行启动、停止和重启 Apache。本章首先介绍了关于这个流行服务器的一些信息，然后向你展示如何安装、配置并开始使用 Apache。

根据 Netcraft 对 2005 年 1 月活跃网站的调查，Apache 是今天互联网上最广泛使用的 Web 服务器，如表 20.1 所示。

请注意，这些统计并没有反映 Apache 在内部网络（即内域网）中的使用情况。

Apache 这个名字出现在软件开发早期，因为它是一个“补丁式”的服务器，它由对免费提供的 NCSA HTTP Web 服务器源代码的各种补丁组合而成的。在 NCSA HTTP 项目停止后的一段时间里，许多人为该代码编写了各种补丁，以修复漏洞或添加他们想要的功能。许多代码在外面流传，人们在自由地分享它们，但它们完全没有经过管理。

一段时间后，Brian Behlendorf 和 Cliff Skolnik 为这些补丁建立了一个中心存储库，Apache 项目应运而生。该项目仍然由一个较小的核心程序员小组组成，但欢迎任何人向小组提交补丁，以便可能将其纳入代码中。

## 第 20 章 Apache 服务器管理

表 20.1 Netcraft 调查结果（2006 年4 月）

| Web 服务器 | 数量 | 百比 |
| --- | --- | --- |
| Apache | 50,588,443 | 62.72% |
| Microsoft* | 20,343,656 | 25.22% |
| SunONE | 1,907,503 | 2.36% |
| Zeus | 563,381 | 0.70% |

*所有 Web 服务器产品

在过去的几年里，人们对 Apache 项目的兴趣激增，部分原因是由于企业级信息服务对开源产生的新兴趣。这也是由于微软互联网信息服务 `IIS` 中发现的致命安全漏洞；恶意 Web 任务的存在；以及操作系统和网络面对现在著名的 Code Red、Blaster 和 Nimda 蠕虫时存在的漏洞。IBM 早期就承诺支持并使用 Apache 作为其 Web 服务的基础，并为该项目投入了大量资源，因为使用一个成熟、经过验证的 Web 服务器更有意义。

1999 年，Apache 软件基金作为一家非营利性公司成立。由 ASF 成员每年选举产生的董事会监督该公司。这家公司为几个开源软件开发项目（包括 Apache Web 服务器）提供基础支持。

了解 Apache 的最佳地方是 Apache 组网站 `http://www.apache.org/` 和 Apache Week 网站 `http://www.apacheweek.com/`，在这些网站上你可以通过电子邮件订阅 Apache 周报，以跟进项目的最新进展，关注安全公告并研究修复方案。

> 提示：你可以在其常见问题解答 `FAQs` 中找到 Apache 的概述，地址为 `http://httpd.apache.org/docs-2.0/faq/`。除了详细的文档外，你还可以在 Apache 服务器的 HTML 目录中找到 Apache 的完整文档。你可以通过新系统中自带的任一浏览器访问 `http://localhost/manual/index.html` 来查看这些文档。Ubuntu 自带 Apache 2.0，且该服务器（命名为 `httpd`）包含在本书的 CD-ROM 和 DVD 中。你可以从 Ubuntu FTP 服务器、通过 `Synaptic` 获取最新版本的 Apache 软件包，或者通过从 Apache 网站获取源代码并自行编译。要确定系统中所包含的 Apache 版本，请像这样使用 Web 服务器的 `-v` 命令：

```bash
$ /usr/sbin/httpd -v
Server version: Apache/2.0.50
Server built: Jun 29 2004 11:55
Server's Magic Number: 2003
Architecture: 32-bit
Server compiled with:
```

输出显示了版本号、编译日期时间、平台以及编译期间使用的各种选项。你可以使用 `-v` 查看版本信息。
