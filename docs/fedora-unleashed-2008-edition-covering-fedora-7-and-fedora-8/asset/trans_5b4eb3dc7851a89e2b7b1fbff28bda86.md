

## 参考

- [http://www.gnu.org/software/bash/bash.html](http://www.gnu.org/software/bash/bash.html)— GNU 软件项目中的 Bash 主页。
- [http://www.tldp.org/LDP/abs/html/](http://www.tldp.org/LDP/abs/html/)— Mendel Cooper 的《高级 Bash 脚本指南》。
- [http://www.linuxnewbie.org/nht/intel/shells/basic.html](http://www.linuxnewbie.org/nht/intel/shells/basic.html)— 在该网站学习基本的 shell 命令。
- [http://www.cs.princeton.edu/~jlk/jlk/ksh93/](http://www.cs.princeton.edu/~jlk/jlk/ksh93/)—“The New Korn Shell—ksh93”，由 David G. Korn、Charles J. Northrup 和 Jeffery Korn 撰写的关于 Korn shell 的文章。
- [http://lug.umbc.edu/~mabzug1/bash-httpd.html](http://lug.umbc.edu/~mabzug1/bash-httpd.html)— Bash-httpd 常见问题解答，并附有指向最新版 bash 网络服务器 bash-httpd-0.02 的链接。
- [http://www.tsch.org/](http://www.tsch.org/)— 在此处了解有关 tesh 的更多信息。
- [http://www.zsh.org/](http://www.zsh.org/)— 在此处更详细地考察 zsh。

# 第 34 章

# 高级软件管理

Fedora 预先提供了大量已安装并随时可用的软件包。然而，Fedora 还附带了一个出色的软件包管理工具，名为 yum，它允许你快速轻松地下载和安装更多软件包。yum 工具（Yellowdog Updater, Modified）自 Fedora 1 版起就已包含在内，并已成为安装和更新应用的首选工具。本章将探讨 yum 的工作原理、基本用法以及更高级的软件包和存储库管理，包括使用 Fedora 提供的一些图形界面工具。但在开始之前，我们先看看 RPM，这是 yum 利用的底层技术。

## 使用 RPM 进行软件管理

rpm 命令使用 RPM 系统来安装、删除（erase）、升级、验证以及构建被称为 RPM 文件的软件存档。这些存档或软件包包含软件包标识（签名）、校验和（通过数学推导得出的验证值）以及软件存档本身，后者可以是源代码形式或二进制形式。RPM 软件包还包含大量额外信息，例如名称、版本和基本描述，并且可以包含用于软件安装、清除或升级的安装前和安装后脚本。

### 本章内容

- 使用 RPM 进行软件管理
- yum 入门
- 非交互式运行 yum
- 使用 yum 移除软件包
- 维护 yum
- 使用 yum 管理软件包清单
- 配置 yum
- 使用 pirut 进行软件管理
- 使用 Yum Extender
- 创建本地 yum 存储库
- 参考

## 什么是 RPM？

RPM 有着悠久的历史，并与 Fedora 的发起人 Red Hat 紧密相关。RPM 本身可以追溯到早期的 Linux 软件包管理软件——名为 RPM PMS 和 PM，它们是用 Perl 编写的。RPM 出现在 1995 年底发布的 Red Hat Linux 2.0 中，并在 1996 年发布的 Red Hat Linux 3.0.3 (Picaaso) 版本中用 C 语言重写。自那时起，rpm 命令就成为 Red Hat 独特软件管理系统的主要特性，该系统基于“纯净源代码”的概念，或者说是使用程序源代码的单个初始存档来构建针对不同系统的软件包并跟踪版本的能力。

除了改进早期软件管理脚本的软件包管理外，RPM 4.1 版本引入了旨在简化从单组源代码文件为不同平台构建软件功能的软件特性。更改可以跟踪并保存在开发者初始源代码之外，并且可以同时从零开始构建并安装多个软件包。同时，RPM 还会验证安装依赖关系。此外，诸如校验和和 GNU 隐私守护程序（GPG）签名等附加功能，使得二进制软件包能够安全分发，而不必担心病毒感染或木马代码的混入。Red Hat 承诺继续对 RPM 进行积极的开发。

安装在你电脑上的 RPM 数据库跟踪哪些软件包的哪些版本已安装。RPM 使用你系统的 /var/lib/rpm 目录来存储包含有关你系统上已安装软件信息 的文件（实际上是数据库）。你可以使用 ls 命令查看这些文件。（根据你安装的软件数量，你看到的文件大小可能与此处显示的不同。）

```
total 75476
-rw-r--r-- 1 root root 10432512 2007-10-29 21:36 Basenames
-rw-r--r-- 1 root root 12288 2007-10-29 21:17 Conflictfname
-rw-r--r-- 1 root root 0 2007-10-29 21:17 _db.000
-rw-r--r-- 1 root root 24576 2007-10-29 21:15 _db.001
-rw-r--r-- 1 root root 1318912 2007-10-29 21:15 _db.002
-rw-r--r-- 1 root root 450560 2007-10-29 21:15 _db.003
-rw-r--r-- 1 root root 3145728 2007-10-29 21:36 Dirnames
-rw-r--r-- 1 root root 10584064 2007-10-29 21:36 Filemd5s
-rw-r--r-- 1 root root 32768 2007-10-29 21:36 Group
-rw-r--r-- 1 root root 28480 2007-10-29 21:36 Installtid
-rw-r--r-- 1 root root 86016 2007-10-29 21:36 Name
-rw-r--r-- 1 root root 54706176 2007-10-29 21:36 Packages
-rw-r--r-- 1 root root 344064 2007-10-29 21:36 Providename
-rw-f--r-- 1 root root 131072 2007-10-29 21:36 Provideversion
-rw-r--r-- 1 root root 12288 2007-10-29 21:17 Pubkeys
-rw-r--r-- 1 root root 479232 2007-10-29 21:36 Requirename
-rw-r--r-- 1 root root 278528 2007-10-29 21:36 Requireversion
-rw-r--r-- 1 root root 163840 2007-10-29 21:36 Sha1header
-rw-f--r-- 1 root root 81920 2007-10-29 21:36 Sigmd5
-rw-r--r-- 1 root root 12288 2007-10-29 21:36 Triggername
```

已安装软件的主要数据库包含在名为 Packages 的文件中。如前例所示，如果你对 Fedora 执行完整安装（超过 4GB 的软件），该数据库可能会增长到 50MB（甚至更大）。安装 Fedora 后，rpm 及相关命令在软件管理操作期间会使用此目录。

## 命令行中的 rpm

作为 Fedora 系统管理员，你将使用 rpm 命令或 Fedora 图形客户端执行五项基本任务之一。这些操作必须由 root 操作员执行，包括以下内容：

- 安装新软件
- 擦除或移除过时或不需要的软件包
- 升级已安装的软件包
- 查询以获取有关软件包的信息
- 验证软件包安装或完整性

rpm 命令拥有超过 60 个命令行选项，但其管理功能可以根据前述五种操作类型进行分组。图形 RPM 客户端为这些操作提供了易于使用的界面。作为系统管理员，你可以在使用图形界面和使用 rpm 的各种命令行选项之间做出选择。

rpm 命令的一般格式如下：

```
# rpm option packagename
```

基本选项如下：

- -i — 安装选定的软件包或多个软件包
- -e — 擦除（移除）选定的软件包或多个软件包
- -u — 移除当前已安装的软件包，然后安装包含选定软件包或多个软件包内容的软件，保留现有配置文件
- -q — 查询系统或选定的软件包或多个软件包
- -v — 验证已安装或选定的软件包或多个软件包

## 两个实用的选项

通过在任何选项后附加 v 或 h，你可以获得以下效果：

- v — 一些状态反馈
- h — 在工作进行时显示哈希标记

