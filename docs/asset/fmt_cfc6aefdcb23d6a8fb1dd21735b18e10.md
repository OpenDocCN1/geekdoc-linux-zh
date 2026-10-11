
- `refer`：将文件内容复制到标准输出并处理引用

# Linux From Scratch - 版本 12.1

## roff2dvi

将 `roff` 文件转换为 DVI 格式

## roff2html

将 `roff` 文件转换为 HTML 格式

## roff2pdf

将 `roff` 文件转换为 PDF

## roff2ps

将 `roff` 文件转换为 `ps` 文件

## roff2text

将 `roff` 文件转换为文本文件

## roff2x

将 `roff` 文件转换为其他格式

## soelim

读取文件并将形如 `.so file` 的行替换为所提文件的内容

## tbl

将嵌入在 `tro` 输入文件中的表格描述编译编译为 `troff` 能够理解的命令

## tfmotdit

创建一个供 `groff -Tdvi` 使用的字体文件

## troff

与 Unix `troff` 具有高度兼容性；通常应使用 `groff` 命令来调用，该命令将按照相应的顺序并使用相应的选项运行预处理器和后处理器

## 8.63. GRUB-2.12

`GRUB` 软件包包含通用统一引导加载程序（GRand Unified Bootloader）。

约的编译时间：0.3 SBU

所需的磁盘空间：166 MB

### 8.63.1. 安装 GRUB

> 注意

如果你的系统支持 UEFI 且你想通过 UEFI 启动 LFS，你可以跳过 LFS 中的此软件包，并按照 BLFS 页面上的说明安装支持 UEFI 的 `GRUB`（及其依赖项）。

> 警告

取消任何可能影响构建的环境变量：

```
unset (C, CPP, CXX, LD) FLAGS
```

不要尝试使用自定义编译标志对此软件包进行“调优”。这是一个引导加载程序。源代码中的低级操作可能会被激进的优化破坏。

从发布 tar 包中添加一个文件：

```
echo depends blib_gpt > grub-core/extra_deps.lst
```

为编译 `GRUB` 准备：

```
./configure --prefix=/usr \
	--sysconfdir=/etc \
	--disable-efiemu \
	--disable-werror \
```

新配置选项的含义：

```
--disable-werror
```

这允许构建在较新版本的 Flex 引入警告的情况下完成完成。

```
--disable-efiemu
```

此选项通过禁用某些功能并消除 LFS 不需要的一些测试程序，来尽量减少构建的内容。

编译软件包：

```
make
```

不建议运行这些软件包的测试套件。大多数测试依赖于 LFS 环境中未提供的软件包。如果仍要运行测试，请运行 `make check`。

安装软件包：

```
make install
mv -v /etc/bash_completion.d/grub /usr/share/bash-completion/completions
```

使用 `GRUB` 使你的 LFS 系统可启动将在第 10.4 节“使用 GRUB 设置引导过程”中讨论。

### 8.63.2. GRUB 的内容

**已安装的程序：** `grub-bios-setup`, `grub-editenv`, `grub-file`, `grub-fstest`, `grub-glue-efi`, `grub-grub`, `grub-kbdcomp`, `grub-macless`, `grub-menulst2cfg`, `grub-mkconfig`, `grub-mkimage`, `grub-mklayout`, `grub-mknetcdir`, `grub-mkpasswd-pbkdf2`, `grub-mkrelpath`, `grub-mkresusc`, `grub-mkstandalone`, `grub-ofpathname`, `grub-probe`, `grub-reboot`, `grub-render-label`, `grub-script-check`, `grub-set-default`, `grub-sparc64-setup`, 和 `grub-syslinux2cfg`

**已安装的目录：** `/usr/lib/grub`, `/etc/grub`, `/usr/share/grub`, 以及 `/boot` (当首次运行 `grub install` 时)

## 简述

- **`grub-bios-setup`**: 是 `grub-install` 的辅助程序

- **`grub-editenv`**: 是用于编辑环境块的工具

- **`grub-file`**: 检查给定文件是否为指定的类型

- **`grub-fstest`**: 用于调试文件系统驱动程序的工具

- **`grub-glue-efi`**: 将 32 位和 64 位二进制文件合并成单个文件（用于 Apple 机器）

- **`grub-install`**: 在你的驱动器上安装 GRUB

- **`grub-kbdcomp`**: 将 xkb 布局转换为 GRUB 识别的布局的脚本

- **`grub-macless`**: 用于 HFS 或 HFS+ 文件系统的 Mac 风格 bless（bless 是

- **`grub-menulst2cfg`**: 生成 `menu.cfg`

- **`grub-mkconfig`**: 生成 `menu.cfg`

- **`grub-mkimage`**: 生成镜像

- **`grub-mklayout`**: 生成布局

- **`grub-mknetcdir`**: 生成 `netcdir`

- **`grub-mkpasswd-pbkdf2`**: 生成 PBKDF2 密码

- **`grub-mkrelpath`**: 生成相对路径

- **`grub-mkresusc`**: 生成 `resusc`

- **`grub-mkstandalone`**: 生成独立镜像

- **`grub-ofpathname`**: 生成路径

- **`grub-probe`**: 探测系统

- **`grub-reboot`**: 重启系统

- **`grub-render-label`**: 渲染标签

- **`grub-script-check`**: 检查脚本

- **`grub-set-default`**: 设置默认

- **`grub-sparc64-setup`**: 针对 `sparc64` 的设置

- **`grub-syslinux2cfg`**: 配置 `syslinux`

# Linux From Scratch - Version 12.1

**`ip mroute`** 允许用户设置、更改或删除多播路由

**`ip monitor`** 允许用户持续监控设备、地址和路由的状态

- **`Instat`** 提供 Linux 网络统计数据；它是旧 **`rtstat`** 程序的通用且功能更完备的替代品

- **`nstat`** 显示网络统计数据

- **`route`** **`ip route`** 的一个组件，用于列出路由表

- **`rtacct`** 显示 `/proc/net/rt_acct` 的内容

- **`rimon`** 路由监控工具

- **`rtpr`** 将 **`ip -o`** 的输出转换为可读格式

- **`rtstat`** 路由状态工具

- **`ss`** 类似于 **`netstat`** 命令；用于显示活跃连接

- **`tc`** 用于用于服务质量 (QoS) 和服务类别 (CoS) 实现的流量控制工具

- **`tc qdisc`** 允许用户设置队列规则

- **`tc class`** 允许用户根据队列规则调度设置类

- **`tc filter`** 允许用户设置 QoS/CoS 数据包过滤

- **`tc monitor`** 可用于查看内核中流量控制的更改。

## 8.66. Kbd-2.6.24

`Kbd` 软件包包含键表文件、控制台字体和键盘工具。

预计编译时间：0.1 SBU

所需磁盘空间：34 MB

### 8.66.1. 安装 Kbd

退格键（backspace）和删除键（delete）的行为在 `Kbd` 包中并不一致。以下补丁修复了 i386 键表的此问题：

```
patch -Np1 -i ../kbd-2.6.4-backspace-1.patch
```

补丁后，退格键生成代码为 127 的字符，删除键生成一个标准的转义序列。

删除冗余的 `resizecons` 程序（它防止了失效的 svgalib 提供视频文件 - 正常使用请适当设置语言）以及相应的帮助页。

```
sed -i '/RESIZECONS_PROGS/s/yes/no/' configure
sed -i 's/resizecons.8 //' docs/man/man8/Makefile
```

为编译准备 `Kbd`：

```bash
./configure --prefix=/usr --disable-vlock
```

配置选项的含义：

```
--disable-vlock
```

此选项防止构建 `vlock` 工具程序，因为它需要 PAM 库，而该库在 chroot 环境中不可用。

编译软件包：

```
make
```

测试结果，请执行：

```
make check
```

安装软件包：

```
make install
```
