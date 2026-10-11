
目录...................................................................................................................... 313

描述.................................................................................................................. 313

- 附录 B 资源.................................................................................. 314

- 引言............................................................................................................... 315

# 目录

- 书籍........................................................................................................................................... 316

- HOWTOs 与指南............................................................................................................... 317

- 其他............................................................................................................................................. 318

# 从零构建 Linux (Linux From Scratch)

Gerard Beekmans

Copyright © 1999, 2000 Gerard Beekmans 所有

本书描述了如何仅使用所需的软件源码，从已安装的 Linux 发行版开始从零创建你自己的 Linux 系统的过程。

本书的分发必须遵守 http://www.linuxudoc.org/COPYRIGHT.html 中 LDP 许可协议中规定的条款和条件。

当仅引用本书的一小部分用于信息目的或类似目的时，不需要显示 LDP 许可协议中描述的许可声明。然而，我要求你在引用时附带类似于下面这行的内容：“引用自 LFS 书籍 http://www.linuxfromscratch.org”。

# 献辞

本书献给我我亲爱且支持我的妻子 Beverly Beekmans。

- 目录
- 前言
- 谁想读这本书
- 谁不想读这本书
- 组织架构
- 第一部分 引言
- 第二部分 LFS 系统的安装
- 第三部分 附录

## 1. 第一部分 引言

### 1. 引言

引言

- 将如何进行
- 书籍版本
- 致谢
- 变更日志
- 邮件列表与存档
- 联系方式

### 2. 重要信息

- 关于 SLFS
- 如何下载软件

# 从零构建 Linux (Linux From Scratch)

如何安装软件

## II. 第二部分 LFS 系统的安装

## 3. 需要下载的软件包

## 4. 准备新分区

引言

- 创建新分区
- 在新分区上创建 ext2 文件系统
- 挂载新分区
- 创建目录

## 5. 准备 LFS 系统

如何以及为什么这样做

- 安装 Bash
- 安装 Binutils
- 安装 Bzip2
- 安装 Diffutils
- 安装 Fileutils
- 必要时在正常系统中安装 GCC
- 在 LFS 系统上安装 GCC
- 安装 Linux 内核
- 安装 Glibc
- 安装 Grep
- 安装 Gzip
- 安装 Make
- 安装 Sed
- 安装 Shellutils
- 安装 Tar
- 安装 Textutils
- 创建 passwd 和 group 文件
- 复制 `/proc/devices`

## 6. 安装基础系统软件

引言

- 调试符号与编译器优化
- 创建 `$LFS/root/bash_profile`
- 进入 chroot 环境
- 创建设备文件
- 安装 GCC
- 安装 Bison
- 安装 Mawk
- 安装 Patch
- 安装 Findutils
- 安装 Ncurses
- 安装 Less
- 安装 Groff
- 安装 Man
- 安装 Perl
- 安装 M4
- 安装 Texinfo
- 安装 Autoconf
- 安装 Automake

# Linux 从零开始 (Linux From Scratch)

- 安装 Bash
- 安装 Flex
- 安装 File
- 安装 Libtool
- 安装 Bin86
- 安装 Binutils
- 安装 Bzip2
- 安装 Gettext
- 安装 Consoletools
- 安装 Consoledata
- 安装 Diffutils
- 安装 E2fsprogs
- 安装 Ed
- 安装 Fileutils
- 安装 Grep
- 安装 Gzip
- 安装 Ldso
- 安装 Vim
- 安装 Lilo
- 安装 Make
- 安装 Modatils
- 安装 Procinfo
- 安装 Procps
- 安装 Psmisc
- 安装 Sed
- 安装 Shellutils
- 安装 Shadowpwd
- 安装 Syslogd
- 安装 Sysinit
- 安装 Tar
- 安装 Textutils
- 安装 Utilize
- 安装 Man-pages
- 删除旧 NSS 库文件
- 配置基本软件

## 7. 创建系统启动脚本

### 这里正在做什么

- 创建目录
- 创建 rc 脚本
- 创建 rcS 脚本
- 创建函数脚本
- 创建 checkfs 脚本
- 创建 halt 脚本
- 创建 loadkeys 脚本
- 创建 mountfs 脚本
- 创建 reboot 脚本
- 创建 sendsignal 脚本
- 创建 setclock 脚本
- 创建 syslog 脚本
- 创建 umountfs 脚本
- 设置符号链接和权限

### 创建 `/etc/fstab` 文件

## 8. 设置基础网络

# 介绍

安装网络软件

### 创建网络启动脚本

## 9. 使 LFS 系统可启动

# 介绍

安装内核

为 LILO 添加条目

测试系统

## III. 第三部分 – 附录

### A. 软件包描述

# 介绍

- Glibc
- Linux 内内核
- Ed
- Patch
- GCC
- Bison
- Mawk
- Findutils
- Ncurses
- Less
- Groff
- Man
- Perl
- M4
- Texinfo
- Autoconf
- Automake
- Bash
- Flex
- Binutils
- Bzip2
- Diffutils
- E2fsprogs
- File
- Fileutils
- Gettext
- Grep
- Gzip
- Ld.so
- Libtool
- Bin86
- Lilo
- Make
- Shellutils
- Shadow Password Suite
- Modutils
- Procinfo
- Procps
- Vim
- Psmisc
- Sed
- Sysklogd
- Sysvinit
- Tar
- Textutils
- Utilize Linux
- Console-tools
- Console-data
- Man-pages

### B. 资源

### 介绍

- 书籍
- HOWTO 和指南
- 其他

# 前言

## 谁会想读这本书

本书面向那些想要进一步了解 Linux 内部原理以及操作系统各个部分如何组合在一起的 Linux 用户。本书将引导你仅使用所需的软件源码，从零开始逐步创建一个属于你自己的自定义构建 Linux 系统。

这本书也面向那些希望摆脱现有的往往臃肿的商业版和免费发行版的 Linux 用户。使用现有的发行版还会迫使你使用它们所选择的文件系统结构、启动脚本结构等。通过这本书，你可以完全按照你喜欢的方式创建自己的结构和方法（这些可以基于本书提供的那些）。

此外，如果你有安全方面的考虑，你不希望依赖预编译的软件包。因此，你希望从零开始编译所有程序并自己安装它们。这可能是你想要构建自定义 Linux 系统的另一个原因。
