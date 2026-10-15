
# 服务器安装软件说明

## 所有版本 (All Version)

- `GnuPG` 包是一个安全通信和数据存储工具。它是 `PGP` 软件的替代品。它还可以用于加密数据和创建数字签名。[稍将在书中编译]
- `redhat-logos` 包包含 `RedHat` “影子”标志和 `RPM` 模块。[服务器上不必要]
- `redhat-release` 包包含 `RedHat Linux` 发布文件。[不必要]
- `gd` 包允许你的代码快速绘制图像并将输出为 `"gif"` 文件。[不必要]
- `pcitls` 包包含用于检查和设置连接到 `PCI` 总线的设备的各种工具。[我们使用其他方法]
- `rmt` 工具提供远程网络访问以进行备份。[由于 `rmt` 依赖 `rsh`，存在安全风险]

## 服务器安装后必须安装的软件

为了能够在服务器上编译程序，你必须安装 `RPM` 包。安装的这部分非常重要，需要安装下面所有的相关包。这些包位于 `RedHat` 第一部分 `CD-ROM` 的 `RedHat/RPMS` 目录下，代表了 `Linux` 上编译和安装程序的基本必要软件。

### 步骤

首先，我们必须挂载 `CD-ROM` 驱动器并进入 `CD-ROM` 的 `RPM` 子目录。

要挂载 `CD-ROM` 驱动器并进入 `RPM` 目录，请使用以下命令：

```
[root@deep ~]# mount /dev/cdrom /cdrom
[root@deep ~]# cd /cdrom/RedHat/RPMS/
```

这是能够在 `Linux` 系统编译和安装程序的包。记住，这是允许你编译大部分 `tar` 包的最小包。`RedHat CD-ROM` 上还有其他编译器包，因此如果你在编译特定软件时遇到错误信息，请通过与 `tar` 包一起提供的 `README` 文件进行核实。

## Linux 安装 | 第 2 章

### 版本 6.1

- `autoconf-2.13-5.noarch.rpm`
- `m4-1.4-12.i386.rpm`
- `automake-1.4-5.noarch.rpm`
- `dev86-0.14-9.i386.rpm`
- `bison-1.2-28.i386.rpm`
- `byacc-1.9-11.i386.rpm`
- `cdcl-2.5-9.i386.rpm`
- `cpp-1.2-24.i386.rpm`
- `cproto-4.6-2.i386.rpm`
- `tags-3.2-1.i386.rpm`
- `egcs-1.1.2-24.noarch.rpm`
- `ElectricFence-2.1-11.i386.rpm`
- `flex-2.5-a4-3.i386.rpm`
- `gdb-4.18-4.i386.rpm`
- `kernel-headers-2.2.12-20.i386.rpm`
- `glibc-dev-2.1.2-11.i386.rpm`
- `make-3.77-6.i386.rpm`
- `patch-2.5-9.noarch.rpm`
- `autoconf-2.13-5.noarch.rpm`
- `m4-1.4-12.i386.rpm`
- `automake-1.4-6.noarch.rpm`
- `dev86-0.15-0.i386.rpm`
- `bison-1.2-28.i386.rpm`
- `byacc-1.9-11.i386.rpm`
- `cdcl-2.5-10.i386.rpm`
- `cpp-1.2-23.i386.rpm`
- `cproto-4.6-3.i386.rpm`
- `tags-3.4-1.i386.rpm`
- `egcs-1.1.2-30.i386.rpm`
- `ElectricFence-2.1-9.i386.rpm`
- `flex-2.5-a4-3.i386.rpm`
- `gdb-4.18-1.i386.rpm`
- `kernel-headers-2.2.14-5.0.i386.rpm`
- `glibc-dev-2.1.3-15.i386.rpm`
- `make-3.78-1.i386.rpm`
- `patch-2.5-10.i386.rpm`

注意：如果你不想在 `RPM` 安装期间遇到错误依赖管理问题，最好一起安装所有软件。

### 版本 6.1 安装命令

使用一个 `RPM` 命令安装上述所有需要的软件：

一次性安装所有软件的 `RPM` 命令是：`[root@deep RPM]$ -Uv autoconf-2.13-5.noarch.rpm m4-1.4-12.i386.rpm automake-1.4-5.noarch.rpm dev86-0.14-9.i386.rpm bison-1.2-28.i386.rpm byacc-1.9-11.i386.rpm cdcl-2.5-9.i386.rpm cpp-1.2-24.i386.rpm cproto-4.6-2.i386.rpm tags-3.2-1.i386.rpm egcs-1.1.2-24.noarch.rpm ElectricFence-2.1-11.i386.rpm flex-2.5-a4-3.i386.rpm gdb-4.18-4.i386.rpm kernel-headers-2.2.12-20.i386.rpm glibc-dev-2.1.2-11.i386.rpm make-3.77-6.i386.rpm patch-2.5-9.noarch.rpm`

```
autoconf
m4
automake
dev86
bison
byacc
cdcl
cpp
cproto
tags
egcs
ElectricFence
flex
gdb
kernel-headers
glibc-devel
make
patch
```

版权 1999-2000 Gerard Mourani, Open Network Architecture & OpenDocs Publishing

## Linux 安装

### 第 2 章

### 版本 6.2

使用 `RPM` 命令安装所有软件的 `RPM` 命令是：

`[root]# deep RPMs# -Uvh autoconf-2.13-5.noarch.rpm m4-1.4-12.i386.rpm rpm-automake-1.4-12.i386.rpm rpm-build-01.5.0-2.i386.rpm bison-1.28-2.i386.rpm byacc-1.9.2.i386.rpm cdcl-2.10.i386.rpm gcc-1.1.2-30.i386.rpm cproto-4.6-3.i386.rpm tags-3.4-1.i386.rpm egcs-1.1.2-30.i386.rpm ElectricFence-2.1-9.i386.rpm flex-2.5-a4-3.i386.rpm gdb-4.18-1.i386.rpm kernel-headers-2.2.14-5.0.i386.rpm glibc-dev-2.1.3-15.i386.rpm make-3.78-1.i386.rpm patch-2.5-10.i386.rpm`

```
autoconf
automake
dev86
bison
byacc
cdcl
cpp
cproto
tags
egcs
ElectricFence
flex
gdb
kernel-headers
glibc-devel
make
patch
```

## 第 3 章

你需要退出并重新登录使更改生效。

从控制台退出，使用命令：`root]# exit`

在安装并编译了服务器所需的软件包后，移除系统中不需要的所有对象以释放空间。

## 服务器上安装的程序

### 第 1 部分

由于我们自定义了 `Linux` 系统，以下是完成 `Linux` 安装后服务器上必须具备的程序列表。此列表必须与 `/tmp/` 中的 `install.log` 文件匹配。不要忘记安装所有软件包。

- `setup`
- `filesystem`
- `basesystem`
- `ldconfig`
- `glibc`
- `shadow-tools`
- `system`
- `libcap`
- `bash`
- `MAKEDEV`
- `SysV`
- `XFree6-Mach4`
- `chkconfig`
- `curses`
- `info`
- `fileutils`
- `grep`
- `ash`
- `authconfig`
- `bc`
- `bashutils`
- `binitils`
- `bzp2`
- `sed`
- `console-tools`
- `dsprogs`
- `rmt`
- `cpio`
- `cracklib-dicts`
- `crontabs`
- `textutils`
- `dev`
- `utils`
- `dump`
- `ed`
- `eject`
- `expect`
- `file`
- `findutils`
- `gawk`
- `gd`
- `gdb`
- `getty_ps`
- `glib`
- `gmp`
- `gnupg`
- `gpi`
- `groff`
- `gip`
- `hdpar`
- `inscripts`
- `ipchains`
