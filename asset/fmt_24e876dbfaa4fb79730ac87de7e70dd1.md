
这些只是人们想要构建自己的 Linux 系统的众多原因中的几个。如果你是其中之一，那么这本书就是为你准备的。

## 谁不想读这本书

不想从零开始构建整个 Linux 系统的用户可能不想读这本书。然而，如果你确实想了解在幕后发生了什么，特别是从开启电脑到看到命令提示符之间发生了什么，那么你应该阅读《从通电到 Bash 提示符》`P2B` `HOWTO`。这个 `HOWTO` 以与本书类似的方式构建一个精简系统，但它更多地关注于安装一个可启动的系统，而不是一个完整的系统。

要决定你是想读这本书还是 `P2B` `HOWTO`，你可以问自己一个问题：我的主要目标是获取一个自己构建的运行良好的 Linux 系统，并在过程中学习并构建系统中每个组件的作用，还是仅仅学习部分是我的主要目标？如果你想边构建边学习，请读这本书。如果你只想学习，那么 `P2B` `HOWTO` 可能是更好的阅读材料。

《从通电到 Bash 提示符》`HOWTO` 可以从 `http://learning.taslug.org.au/power2bash` 下载。

# 组织结构

本书分为以下几个部分。尽管某些部分存在大量重复信息，但这是阅读它最简单的方法，也是我维护这本书最简单的方法。

## 第一部分 – 介绍

第一部分为你提供了关于本书的一般信息（版本、获取方式、更新日志、邮件列表以及如何与我联系）。它还解释了在你开始构建 `LFS` 系统之前真正需要阅读的几个方面。

## 第二部分 – 安装 LFS 系统

第二部分引导你安装 `LFS` 系统，这将成为你选择对你的全新系统进行所做的任何操作的基础。

## 第三部分 – 附录

第三部分包含了各种附录。

### I. 第一部分 – 介绍

目录

- 1. 介绍
- 2. 重要信息

## 第1章 介绍

### 介绍

在使用过许多 Linux 发行版后，从未对其中任何一个感到满意。我不喜欢它们的安排。我意识到，当我对一个 Linux 系统完全满意时，我必须从零开始构建，理想情况下只使用源码。这个想法一度看起来是非常疯狂，有时是不可能的。大多数问题源于我对某些程序和程序的缺乏了解。在解决了各种依赖问题、编译问题后，一个自定义的 Linux 系统被创建并正常运行。我将这个系统命名为 `LFS`，意为 Linux From Scratch（从零开始的 Linux）。

## 致谢

我要感谢以下个人和机构对 LinuxFromScratch 项目做出的贡献：

- Paul Jensen，提供了 `http://www.percdallas.com` 作为 `linuxfromscratch.org` 的主主机
- Bryan Dumm，提供了 `http://www.bcpub.com` 作为 `lfs.bcpub.com` 的镜像
- Jan Niemann，提供了 `http://helga.lk.tu-bs-de` 作为 `134.169.209` 的镜像
- Jason Andrade，提供了 `http://mirror.aarnet.edu.au` 作为 `Lfs.mirror.aarnet.edu.au` 的镜像
- Johan Lenglet，提供了 `http://www.linuxien.com/` 作为 `www.linuxien.com/lfs/` 的镜像
- Michael Peters，贡献了针对 Apple PowerPC 的修改方案
- VA Linux Systems，其代表 Linux.com 捐赠了一台 VA Linux 420（原为 StartX SP2）工作站用于本项目。
- Jesse Tie Ten Queue 捐赠了一台 Yamaha CDRW 8824E CD–RW。
- O'Reilly 捐赠了关于 SQL 和 PHP 的书籍。
- 来自各种 LFS 邮件列表的无数其他人，他们通过提出建议、测试和提交错误报告使这本书得以诞生。

## 更新日志

例如，如果第 5 章列出了某项更改，（通常）意味着其他架构的章节也进行了相同的更改。

### 2.4 – 2000年8月28日

- 将书籍分为 Intel 和 PPC 两个版本的独立书籍。
- 第 4 章：在“创建目录”部分添加了 `mail` 和 `dev/pts` 目录。
- 第 5 章：将 `chroot` 及其之后的所有内容都放在了一个新章节。
- 第 6 章：将优化部分移动到进入 `chroot` 环境之前的点。对于静态包使用编译器优化是浪费的，因为它们终究会被替换。
- 第 6 章：先 `chroot` 进入 `LFS/root` 目录。某些旧的 `chroot` 程序在当你的目录不在 `chroot` 环境内部时进入 `chroot` 会出现问题。此外，我们不再直接在 `chroot` 环境中执行 `bash`，而是启动 “envenv” 程序，以便进入一个只设置了 `CFLAG` 和 `CFLAGS` 的干净环境。
- 第 6 章：一些人在 `chroot` 环境下编译 `M4` 时遇到了问题。已为受影响的用户提供了如何静态安装此包的说明。
- 第 6 章：在 `fileutils` 包的动态安装期间，我们无法使用 `mv` 程序来移动 `mv` 程序。我们先将其复制到 `/bin`，然后删除 `/usr/bin/mv`。
- 第 5 章：在 Glibc 安装中添加了 `make localedata-locales`。如果你有一个支持 NLS 的系统（LFS 是支持的，但缺少 locale 的话它几乎毫无用），这会安装各种应用程序使用的 locale 文件（注意不是 GDK 应用程序）。
- 第 6 章：将 `vim` 的安装移动到 `Lilo` 之前，因为你可能想要编辑 Lilo 的 Makefile 文件以添加编译器优化。
- 第 6 章：将 `shadow password` 密码件的安装移动到 `sh-utils` 之后。否则 `sh-utils` 会用它的版本替换 `shadow password` 中的 “su” 版本，这本不该发生。
- 第 6 章：更改了我们进入 `chroot` 环境的方式。我们使用 `env` 创建一个空环境，这样来自普通 Linux 系统的环境变量就不会干扰 `chroot` 环境。进入 `chroot` 环境时设置的唯一变量是 `HOME`。
- 第 6 章：由于了进入 `chroot` 的新方式，创建了 `LFS/root/bash_profile` 文件，它设置了如 `TERM`、`CFLAGS`、`CXXFLAGS` 以及你认为必要的任何变量。

### 2.3.7 – 2000年8月3日

- 所有章节：删除了自己的 SGML 标签，因此文件内容不再缩进。这提高了将书籍复制并粘贴到你的文件中的便利性，而无需手动重新格式化以消除缩进。
- 第 4 章：在 `chmod 1777 tmp/` 命令中添加了 `var/tmp`。
- 第 4 章：通过将 `$LFS/usr` 和 `$LFS/usr/local` 的目录创建放在 for 循环中，使 `mkdir` 不再那么重复。
- 第 5 章：更改了 `sed` 操作后用于 `MAKEDEV` 的 `chmod 754` 命令。
- 第 5 章：更改了包安装顺序以符合字母排序。
- 第 5 章：在 `console-tools` 安装后，创建了 `/usr/share/defkeymap.map.gz` 文件，它将被 `loadkeys` 脚本使用。
- 第 5 章：从“Installing Procs”中删除了 “gcc -c watch”。如果在某些硬件上仍然需要，请告诉我们。
- 第 5 章：添加了 `/usr/bin/install` 符号链接，因为至少有一个包（syslogd）在它的 Makefile 中硬编码了安装路径。
- 第 5 章：在 `gettext` 安装后，我们有一个文件 `/po-mode.el`。该文件将被移动到它正确所属的 `/usr/share/gettext`。
- 第 5 章：当 `gzip` 安装且文件移动到 `/bin` 时，文件之间的符号链接会被删除。因此我们只需移动 `gzip` 并创建 `gzip` 和 `gunzip` 的符号链接。
- 第 5 章：当 `gzip` 安装且文件移动到 `/bin` 时，文件之间的符号链接会被删除。因此我们只需移动 `gzip` 并创建 `gzip` 和 `gunzip` 的符号链接。
- 第 5 章：当 `gzip` 安装且文件移动到 `/bin` 时，文件之间的符号链接会被删除。因此我们只需移动 `gzip` 并创建 `gzip` 和 `gunzip` 的符号链接。
- 第 5 章：当 `gzip` 安装且文件移动到 `/bin` 时，文件之间的符号链接会被删除。因此我们只需移动 `gzip` 并创建 `gzip` 和 `gunzip` 的符号链接。
- 第 5 章：当 `gzip` 安装且文件移动到 `/bin` 时，文件之间的符号链接会被删除。因此我们只需移动 `gzip` 并创建 `gzip` 和 `gunzip` 的符号链接。
- 第 5 章：当 `gzip` 安装且文件移动到 `/bin` 时，文件之间的符号链接会被删除。因此我们只需移动 `gzip` 并创建 `gzip` 和 `gunzip` 的符号链接。
