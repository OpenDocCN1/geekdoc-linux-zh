
该方案的核心是将每个包安装到自己的根目录中。例如，你可以将 `gimp` 安装到 `/tools/graphics/gimp`，二进制文件位于 `/tools/graphics/gimp/gimp`。你可以通过将符号链接放入如 `/tools/bin` 等工具中，为你的工具集创建一个聚合二进制文件：

```
/tools/bin/gimp -> /tools/graphics/gimp/bin/gimp
```

用户可以将 `/tools/bin` 目录添加到他们的 `PATH` 变量中，以确保获取到所有的共享工具。

构建 `/tools/` 目录有多种选择。层次化方法（例如 `/tools/graphics`、`/tools/editors` 等）便于浏览并提高性能。你可能希望在命名规范中包含软件版本、硬件架构、操作系统或负责人的字母缩写，以便让较少的工具集合为许多类型的客户端服务。例如，Solaris 用户可能会在他们的 `PATH` 中包含 `/tools/sun4/bin`，而 Fedora 用户则包含 `/tools/fedora/bin`。

当你安装一个主要工具的新版本时，无限期保留旧版本是一个好主意，特别是当用户对他们使用的项目投入了大量的时间和精力时。理想情况下，工具的新版本应该与旧的数据文件和软件兼容，但在实践中，灾难是常有的。要求用户通过一些配置麻烦来访问旧版本的包是可以接受的；但破坏他们现有的工作并让他们承担后果将是不被允许的。

## 11.8 为 NFS 共享软件

### 依赖管理

某些包依赖于库或其他软件包。当你通过包管理系统在本地安装软件时，你会得到很多帮助来解决这些问题。然而，当你构建全站网络仓库时，必须显式地处理这些问题。

如果你以管理应用程序的方式管理库，你就可以编译工具使用来自共享 `/tools` 目录内部的库。这种惯例允许你同时运行多个版本的库。因为依赖的应用链接到了库的特定版本，即使在发布了库的新版本，设置仍然保持有效。缺点是这种设置随着时间的推移可能会变得难以使用和维护。

抵制链接到包含通用命名常用库的全局 `/tools/lib` 目录的诱惑。如果你更改了库，可能会遇到意想不到且难以诊断的问题。共享库系统旨在解决一些潜在的冲突，但在复杂的设置中这样做是有意义的。

要让链接器使用你系统中特定版本的共享库所需的精确步骤。在 Linux 下，你可以使用环境变量 `LD_LIBRARY_PATH` 或使用链接器的 `-R` 选项。

### 包装器脚本

遗憾的是，库级别的兼容性仅仅是故事的一半。工具相互调用的事实引发了另一个冲突机会。例如，假设名为 `bar` 的工具频繁使用名为 `foo` 的工具。如果你更新了 `bar` 的默认版本，你可能会发现 `foo` 突然停止工作。在这种情况下，你可以得出结论：`foo` 依赖于 `bar` 的某些不再支持（或至少不是默认）的行为。

如果你的软件仓库支持多个版本（例如 `/tools/util/bar-1.0` 和 `/tools/util/bar-2.0`），你可以通过将 `foo` 移动到 `foo.real` 并用一个小包装器脚本替换它来修复这个问题：

```
#!/bin/sh
# 确保程序找到与其同包的任何文件
# 如果它没有使用显式路径。
PATH=/tools/util/bar-1.0/bin:$PATH
export PATH
exec /tools/util/foo-1.0/bin/foo "$@"
```

现在，`foo` 将使用自定义的 `PATH` 环境变量启动，并优先调用旧版本的 `bar` 而不是新的。

包装器是一个强大的工具，不仅可以解决包依赖问题，还可以解决安全、架构或操作系统依赖性以及使用跟踪等问题。某些站点包装所有的共享二进制文件。

### 实现工具

共享软件仓库的维护是系统管理中的常见问题，管理员们开发了各种软件解决方案来帮助这一过程。与本地化一样，自解决方案往往占据主导地位，但一往一样，检查可用系统看看是否有符合你需求的值得的。

## 11.9 推荐软件

### 表 1.1 必需软件

| 软件包 | 描述 |
| :--- | :--- |
| ssh/scp | 安全 shell - 使用加密 |
| sudo | su 的替代品 - 增加控制 |
| sendmail 或 postfix | 邮件传输选择 |
| traceroute | 网络追踪 - 用于调试 |
| tcpdump 或 Wireshark | 网络嗅探选择 - 用于分析流量 |
| gzip | GNU 数据压缩 - 用于解压 |
| mozilla 或 firefox | 浏览器选择 - 必选 |
| RCS/VCS/Subversion | 版本控制系统 - 对两者都有用 |
| Perl | 脚本语言 - 通用 |

### 表 1.2 有用软件

| 软件包 | 描述 |
| :--- | :--- |
| gcc | C/C++ 编译器 - 高质量编译器 |
| BIND | 名称服务工具 - 获取当前版本 |
| Samba | Windows SMB - 与 Windows 共享文件/打印 |
| Apache | Web 服务器 |
| Squid | Web 代理和缓存 |
| imapd/procmail | 邮件工具 - 用于访问和过滤邮件 |
| mrtg, RRDTool | 监控工具 - 用于网络流量和其他数据 |
| Acrobat Reader | PDF 文件查看，Adobe 提供的优秀免费工具 |
| gimp | 位图图像编辑器 |
| xfig | 简单的 X Windows 绘图程序 |
| GnuPG | 签名、验证和加密消息 |
| nvi/vim | 类 vi 文本编辑器 - 系统管理员推荐 |
| emacs | 文本编辑器/操作系统 - 适合高级用户 |
| pico, need | 文本编辑器 - 初学者的极佳选择 |
| enlist, mpage | 打印工具 - 漂亮打印和 N 排格式化器 |
| pine | 适合初者的邮件阅读器 |
| thunderbird | 偏好 GUI 的邮件阅读器 |
| meh/emxh | 处理大量邮件的阅读器（未维护良好） |

## 第 11 章 – 软件与配置管理

### 11.10 推荐阅读

- INTEL CORPORATION AND SYSTEMSOFT. 启动执行环境 (`PXE`) 规范，版本 2.1. 1999. www.pix.net/software/pxeboot/archive/pxespec.pdf
- MINTHA, JIM, AND PIETER KRUL. UltraLinux FAQ。 www.ultralinux/faq.html
- PXELux 配置。syslinux.zytor.com/pxpe.php
- RODIN, JOSIN. Debian 维护者指南。www.devian.org/doc/maint-guide 该文档包含关于 `.deb` 包的有用信息。
- SILVA, GUSTAVO NORONHA. APT 入门。www.devian.org/doc/manuals/apt-howto
- HODEL, DICK, AND FARIAN HERSCHEL. 使用 YaST 自动安装 Linux 系统。www.usenix.org/events/lisa99/full_packages/hohandel/hohandel
- STÜCKELBERG, MARC VUELLEMER, AND DAVID CLERC. Linux 远程启动 miniHOWTO：使用 Linux, DOS, Windows 95/98 和 Windows NT 配置远程启动工作站。1999。tldp.org/HOWTO/Remote-Boot.html
- 红帽企业 Linux 系统管理指南。www.redhat.com/docs
- WACHMANN, ALF. 如何通过 PXE 和 Kickstart 安装红帽 Linux。www.stanford.edu/~alfw/PXE-Kickstart/PXE-Kickstart.
- BURGESS, MARC. Cfigengine：站点配置引擎。UNIX 计算系统，第 8 卷第 3 期，1995。www.cfigengine.org
- ETKER, TOBIAS. SEPP: 软件安装与共享系统。波士：LISA 1998。people.ee.ethz.ch/oetiker/sepp

### 11.11 练习

- 111.1 概述 Kickstart 和 AutoYaST 之间的区别。什么情况下你会寻找发行特定安装程序的替代方案？
- 111.2 从 submersion.tigris.org 安装一个 Subversion 。设置 svn 并创建一个仓库。如何让该仓库在局域网任何地方都可用，同时保持合理的安全性？
- 111.3 审查你所在地的本地软件是如何组织的。该系统具有可扩展性吗？使用方便吗？进行讨论。
- 111.4 弄清楚创建 RPM 包所需的步骤。使用此过程为你选择的某个软件产品进行打包。
