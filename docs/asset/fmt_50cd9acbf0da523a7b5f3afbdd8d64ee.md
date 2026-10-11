
注意的是，内核源码目录中的文件并不属于 `root`。每当以 `root` 用户身份解包软件包时（我们在 `root` 内部执行了此操作），文件将具有其在打包计算机上的用户 ID 和组 ID。对于安装任何其他软件包来说，这不是问题，因为源码树在安装后会被删除。然而，Linux 源码树通常会保留很长时间。正因如此，软件包使用的任何用户 ID 可能会分配给机器上的某人。那个人将对内核源码具有写权限。

# 注意

在许多情况下，对于以后在 BLFS 中安装的软件包，需要更新内核配置。与其他软件包不同，在安装新构建的内核后，没有移除源码树。

如果需要保留源码树，请对 `linux-4.9.9` 目录运行 `chown -R 0:0` 以确保所有文件都属于用户 `root`。

# 警告

某些内核文档建议从 `/usr/src/linux` 创建指向内核源码目录的符号链接。这专门针对 2.6 系列之前的内核，并且在 LFS 系统上不能创建它，因为可能会导致在你基础 LFS 系统完成后你可能想要构建的软件包出现问题。

# 警告

系统 `include` 目录（`/usr/include`）中的头文件**始终**应该是针对编译的 Glibc 编译的那些，即第 6.7 节“Linux-4.9.9 API Headers”中的清理头文件。因此，它们**绝不能**被内核头文件或其他内核清理头文件替换。

# 8.3.2. 配置 Linux 模块加载顺序

大多数情况下 Linux 模块会自动加载，但有时它们需要特定的指导。加载模块的程序 `modprobe` 或 `insmod` 使用 `/etc/modprobe.d/usb.conf` 实现此目的。如果 USB 驱动程序（`ehci_hccd`、`ohci_hccd` 和 `uhci_hccd`）已编译为模块，则需要创建此文件，以便它们按正确的顺序加载；`ehci_hccd` 必须在 `ohci_hccd` 和 `uhci_hccd` 之前加载，以避免启动时出现警告。

运行以下命令创建一个新文件 `/etc/modprobe.d/usb.conf`：

```
install -v -m755 -d /etc/modprobe.d

cat /etc/modprobe.d/usb.conf << "EOF"

# Begin /etc/modprobe.d/usb.conf

install ohci_hccd /sbin/modprobe ehci_hccd; /sbin/modprobe ohci_hccd; true

install uhci_hccd /sbin/modprobe ehci_hccd; /sbin/modprobe -i uhci_hccd; true

# End /etc/modprobe.d/usb.conf

EOF
```

# 8.3.3. Linux 的内容

- 安装的文件：`config-4.9.9`、`vmlinux-4.9.9-lfs-8.0` 和 `System.map-uhci-4.9.9`
- 安装的目录：`/lib/modules` `/usr/share/doc/linux-4.9.9`

# 简述

- `config-4.9.9`
包含了内核的所有配置选择

- `vmlinux-4.9.9-lfs-8.0`
Linux 系统的引擎。当启动计算机时，内核是操作系统加载的第一部分。它检测并初始化计算机硬件的所有组件，然后将这些组件作为文件树的形式提供给软件，并将单个 CPU 转换为一台能够同时运行数十个程序的多任务机器。

- `System.map-4.9.9`
地址和符号的列表；它映射了内核中所有函数和数据结构的入口点和地址。

## 8.4. 使用 GRUB-v 设置启动过程

### 8.4.1. 简介

> **警告** 错误配置 GRUB 可能会导致系统在没有备用启动设备（如 CD-ROM）的情况下无法运行。本节对于启动你的 LFS 系统不是必需的。你可能只是想修改当前的引导程序，例如 Grub-Legacy、GRUB2 或 LILO。

确保准备好一个紧急启动盘，以便在计算机无法使用（无法启动）时“救援”计算机。如果你没有启动设备，可以创建一个。为了让下面的步骤生效，你需要跳转到 BLFS 并从 `libisoburn` 软件包安装 `xorriso`。

```
/tmp

grub-mkrescue --output=grub-img.iso

xorriso -as cdrecord -v dev=/dev/cdrom rw blank=as_needed grub-img.iso
```
