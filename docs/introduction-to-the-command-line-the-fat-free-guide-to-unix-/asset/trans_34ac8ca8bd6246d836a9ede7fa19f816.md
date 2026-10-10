
# aptitude

**用途：** 基于 Debian Linux 系统的自动化包管理器。

**用法语法：** `aptitude [选项] [操作] [包]`

```bash
# aptitude install apache2
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following extra packages will be installed:
  apache2 apache2-mpm-worker apache2-utils apache2.2-common libapr1 libaprutil1
  libpq5
Suggested packages:
  apache2-doc apache2-suexec-apache2-suexec-custom
The following NEW packages will be installed:
  apache2 apache2-mpm-worker apache2-utils apache2.2-common libapr1
  libaprutil1 libpq5
0 upgraded, 7 newly installed, 0 to remove and 13 not upgraded.
After this operation, 6382kB of additional disk space will be used.
Do you want to continue [Y/n]? Y
...
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_233_0.png)

`aptitude` 是 Debian `dpkg` 包管理器的前端。它通过自动下载并安装包及其所需的依赖项来简化软件安装。在此示例中，`aptitude` 程序将自动下载并安装运行 Apache 网络服务器应用程序所需的包。

> **注意**
> */etc/apt/sources.list 中列出的软件仓库用于查询包数据库中可用的程序及其下载位置。*

常见用法示例：

| 命令 | 描述 |
| :--- | :--- |
| `aptitude update` | 更新包数据库 |
| `aptitude upgrade` | 安装所有包的最新版本 |
| `aptitude dist-upgrade` | 升级整个发行版 |
| `aptitude install [PACKAGE]` | 安装指定的包 |
| `aptitude remove [PACKAGE]` | 移除指定的包 |
| `aptitude search [NAME]` | 按名称搜索仓库中的包 |
| `aptitude show [PACKAGE]` | 显示关于某个包的信息 |
| `aptitude clean` | 清理包缓存 |
| `aptitude --purge-unused` | 移除未使用的包 |

# rpm

**用途：** 安装/移除 Red Hat Linux 包。

**用法语法：** `rpm [选项] [文件]`

```bash
# rpm -iv nmap-4.85BETA9-1.i386.rpm
Preparing packages for installation...
nmap-4.85BETA9-1
...
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_234_0.png)

**rpm** 是 Red Hat Linux 基础系统的传统包管理器。它可以在 Red Hat Enterprise Linux 和 Fedora 以及其他许多基于 Red Hat/Fedora 核心的 Linux 发行版中找到。

使用 **rpm**，您可以安装或移除专门为 Red Hat 和基于 Fedora 的系统创建的程序。这些包通常具有 `.rpm` 文件扩展名。上述示例展示了如何使用 **rpm** 命令安装 RPM 包。

> **注意**
> *大多数基于 Red Hat 的系统现在使用名为 **yum** 的程序来执行软件安装任务。鉴于 **yum** 会自动下载并安装请求的包以及所有所需的依赖项，直接安装使用 **rpm** 的情况很少见。更多信息请参见第 236 页。*

常见用法示例：

| 命令 | 描述 |
| :--- | :--- |
| `rpm -i [PACKAGE]` | 安装指定的包 |
| `rpm -U [PACKAGE]` | 升级指定的包 |
| `rpm -e [PACKAGE]` | 移除指定的包 |
| `rpm -qa` | 列出所有已安装的包 |

# yum

**用途：** 基于 Red Hat Linux 系统的自动化包管理器。

**用法语法：** `yum [选项] [包]`

```bash
# yum install npm
Loaded plugins: refresh-packagekit
Setting up Install Process
Resolving Dependencies
---> Running transaction check
---> Package npm.i586 2:4.76-4.fc11 set to be updated
---> Finished Dependency Resolution
...
```

使用 yum 包管理器安装软件包

**yum** 是 Red Hat Linux **rpm** 包管理器的前端。它通过自动下载并安装包及其所需的依赖项来简化软件安装。在此示例中，**yum** 命令将自动下载并安装运行 **npm** 工具所需的包。

> **注意**
> */etc/yum.conf 中列出的软件仓库用于查询包数据库中可用的包及其下载位置。*

**常见用法示例：**

| 命令 | 描述 |
| :--- | :--- |
| `yum install [PACKAGE]` | 安装指定的包 |
| `yum remove [PACKAGE]` | 移除指定的包 |
| `yum update` | 安装所有包的最新版本 |
| `yum upgrade` | 将发行版升级到最新版本 |
| `yum list` | 列出可用和已安装的包 |
| `yum search [NAME]` | 按名称搜索指定的包 |

# emerge

**用途：** 安装/移除 Gentoo Linux 包。

**用法语法：** `emerge [选项] [包]`

```bash
# emerge uptime
Calculating dependencies... done!
>>> Verifying ebuild Manifests...
>>> Emerging (1 of 1) app-vim/uptime-1.3 to /
>>> Downloading 'http://distfiles.gentoo.org/distfiles/uptime-1.3.tar.bz2'
...
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_236_0.png)

**emerge** 是 Gentoo 的 **Portage** 软件管理器的前端。它提供了与前面讨论的 **aptitude** 和 **yum** 命令类似的自动软件编译、安装和依赖项满足功能。

Portage 是一种独特的包管理器，它从源代码编译软件。这与大多数其他在软件安装时使用预编译二进制文件的 Linux 系统不同。从源代码编译软件可以创建针对平台优化的安装，研究表明其性能优于预编译包。然而，Portage 的缺点在于从源代码安装软件所需的时间要长得多。

> *要了解有关 Portage 软件管理器的更多信息，请参见 www.gentoo.org/doc/ 上的官方 Gentoo 文档。*

常见用法示例：

- `emerge [PACKAGE]` 安装指定的包
- `emerge -u world` 安装所有包的最新版本
- `emerge -C [PACKAGE]` 移除指定的包
- `emerge -s [PACKAGE]` 搜索指定的包
- `emerge --sync` 更新 portage 数据库

# pkg_add / pkg_delete

**用途：** 安装/移除 BSD 包。

**用法语法：** `pkg_add [选项] [包]`

```bash
# pkg_add -r perl 
Fetching ftp://ftp.freebsd.org/pub/FreeBSD/ports/i386/packages-7.2-release/Latest/perl.tbz...
Creating various symlinks in /usr/bin...
Symlinking /usr/local/bin/perl5.8.9 to /usr/bin/perl
...
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_237_0.png)

`pkg_add` 命令在 BSD 系统上安装软件包。在上述示例中，`pkg_add` 用于安装名为 Perl 的包。`-r` 选项指示 `pkg_add` 自动从 BSD 软件仓库获取指定的包。

> `pkg_add` 命令使用位于 ftp.freebsd.org 的默认 FTP 服务器。为了加快下载速度，您可以使用 `PACKAGEROOT` 环境变量指定一个 FTP 镜像。例如，输入 `export PACKAGEROOT=ftp.ca.freebsd.org` 将指示 `pkg_add` 命令使用位于加拿大的指定镜像。完整的 FTP 镜像站点列表可以在 http://mirrorlist.freebsd.org/FPBSDisites.php 在线找到。

`pkg_delete` 命令在 BSD 系统上卸载软件包。在下一个示例中，使用 `pkg_delete` 命令移除先前安装的 Perl 包。

**用法语法：** `pkg_delete [包]`

```bash
# pkg_delete perl-5.8.9_2 
Removing stale symlinks from /usr/bin...
Removing /usr/bin/perl5... Done.
...
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_237_1.png)

**常见用法示例：**

- `pkg_add -r [PACKAGE]` — 下载并安装指定的包
- `pkg_delete [PACKAGE]` — 卸载指定的包

# pkg_info

**用途：** 显示关于 BSD 包的信息。

**用法语法：** `pkg_info [选项]`

```bash
# pkg_info
bash-4.0.33          The GNU Project's Bourne Again SHell
en-freebsd-doc-20090913 Documentation from the FreeBSD Documentation
Project
gttext-0.17.1        GNU gettext package
libiconv-1.13.1      A character set conversion library
lua-5.1.1.4          Small, compilable scripting language providing easy
access
nano-2.0.9_1         Nano's ANOther editor, an enhanced free Pico clone
nmap-5.00            Port scanning utility for large networks
pcRE-7.9             Perl Compatible Regular Expressions library
perl-5.8.9.3_1       Practical Extraction and Report Language
pkg-config-0.23.1    A utility to retrieve information about installed
libraries
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_238_0.png)

`pkg_info` 命令显示 BSD 系统上已安装包的信息。在上述示例中，不带选项执行 `pkg_info` 会生成一个简单的已安装程序列表。

使用 `-a` 选项执行 `pkg_info` 命令将显示已安装包的详细信息，如下一个示例所示。

```bash
# pkg_info nmap-5.00 | less
Information for nmap-5.00:

Comment:
Port scanning utility for large networks

Description:
Nmap is a utility for network exploration and security auditing.
...
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_238_1.png)

**常见用法示例：**

- `pkg_info` | 显示已安装包的一个简单列表
- `pkg_info -a` | 显示已安装包的详细列表
- `pkg_info [PACKAGE]` | 显示关于*指定*包的信息

