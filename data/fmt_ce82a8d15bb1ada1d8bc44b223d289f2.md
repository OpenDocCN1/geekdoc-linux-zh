
如果需要，可以通过从主机系统（假设可用）拷贝内核配置文件 `.config` 到解压的 `linux-5.13.12` 目录来跳过内核配置。然而，我们不建议这种选项。最好探索所有内核菜单并从头创建内核配置。

编译内核映像和模块：

```
make
```

如果使用内核模块，可能需要模块配置。有关模块和内核配置的信息位于第 9.3 节“设备和模块概述”以及 `linux-5.13.12/Documentation` 目录下的内核文档。此外，`modprobe.d(5)` 可能让你感兴趣。

除非内核配置中内置模块支持，否则：

```
make modules_install
```

内核编译完成后，还需要额外的步骤来完成安装。某些文件需要拷贝到 `/boot` 目录。

> 如果系统有单独的 `/boot` 分区，拷贝的文件应该放在那里。最简单的方法是在继续之前，将主机（外部）的 `/boot` 挂载到 `/mnt/lfs/boot`。你系统中的 root 用户：

```
mount --bind /boot /mnt/lfs/boot
```

内核映像的路径可能根据使用的平台而异。下面的文件名可以根据情况更改，但文件名的主干为 `vmlinux`，以便与下一节描述的启动过程自动设置兼容。以下命令假设为 x86 架构：

```
cp -iv arch/x86/boot/bzImage /boot/vmlinuz-5.13.12-lfs-11.0
```

# Linux From Scratch - 版本 11.0

`System.map` 是内核的符号文件。它映射了内核 API 中每个函数的入口点，以及运行内核的内核数据结构的地址。它被用作调查内核问题时的一种资源。执行以下命令安装该文件：

```bash
cp -iv System.map /boot/System.map-5.13.12
```

由 `make menuconfig` 步骤产生的内核配置文件 `.config` 包含了所编译内核的所有配置选项。保留此文件以备后参考之用是一个好主意：

```bash
cp -iv .config /boot/config-5.13.12
```

安装 Linux 内核文档：

```bash
install -d /usr/share/doc/linux-5.13.12
cp -r Documentation/* /usr/share/doc/linux-5.13.12
```

需要注意的是，内核源码目录中的文件并不归 root 所有。当以 root 身份解压包时（我们在我们在 chroot 内部的操作的），文件将拥有打包者计算机上相应的用户 ID 和组 ID。这对于安装后删除任何包来说通常不是问题。然而，Linux 源码树通常会被保留很长时间。由于由于，包使用的任何用户 ID 可能会分配给机器上的某人。那个人将获得访问内核的权限。

> 注意

在许多情况下，对于以后在 BLFS 中安装的包，需要更新内核配置。与其他包不同，安装新构建的内核后没有必要删除内核源码树。

如果要保留内核源码树，请对 `linux-5.13.12` 目录运行 `chown -R 0:0` 以确保所有文件都归用户 root 所有。

> 警告

某些内核文档建议从 `/usr/src` 创建指向内核源码目录的符号链接。这适用于 2.6 系列之前的内核，并且在 LFS 文件系统中禁止创建，因为它可能会导致你希望在完整的 BLFS 系统上构建的软件包出现问题。

> 警告

系统包含目录 (`/usr/include`) 中的头文件始终应该是编译 libc 时所使用的那些头文件，即在第 5.4 节“Linux-5.13.12 API Headers”中安装的清理头文件。因此，它们绝不能被原始内核头文件或任何其他经过清理的内核头文件所替换。

## 10.3.2. 配置 Linux 模块加载顺序

大多数 Linux 模块会自动加载，但有时需要特定的指导。加载模块的程序 `modprobe` 或 `insmod` 使用 `/etc/modprobe.d/usb.conf` 来实现此目的。需要创建此文件，以便 USB 驱动程序（`ehci_hcd`、`ohci_hcd` 和 `uhci_hcd`）在构建为模块时能够按照正确的顺序加载；`ehci_hcd` 需要在 `ohci_hcd` 和 `uhci_hcd` 之前加载，以避免启动时出现警告。

运行以下命令创建一个新文件 `/etc/modprobe.d/usb.conf`：

```bash
install -v -m755 -d /etc/modprobe.d
cat /etc/modprobe.d/usb.conf << "EOF"
# Begin /etc/modprobe.d/usb.conf
install ohci_hcd /sbin/modprobe ehci_hcd ; /sbin/modprobe -i ohci_hcd ; true
install uhci_hcd /sbin/modprobe ehci_hcd ; /sbin/modprobe -i uhci_hcd ; true
# End /etc/modprobe.d/usb.conf
EOF
```

## 10.3.3. Linux 的内容

安装的文件：`config-5.13.12`, `vmlinuz-5.13.12-lfs-11.0` 和 `System.map-5.13.12`

安装的目录：`/lib/modules`, `/usr/share/doc/linux-5.13.12`

## 要描述

- `config-5.13.12` 包含了内核的所有配置选项

- `vmlinuz-5.13.12-lfs-11.0` Linux 系统的引擎。当启动电脑时，内核是操作系统第一个加载的部分。它检测并初始化计算机硬件的所有组件，然后将这些组件作为文件树的形式提供给软件，并将单 CPU 转换为一台能够看似同时运行数十个程序的多任务机器。

- `System.map-5.13.12` 地址和符号的列表；它映射了内核中所有函数和数据结构的入口点和地址

## 10.4. 使用 GRUB 设置启动过程

> 注意：如果你的系统支持 UEFI 且你想通过 UEFI 启动 LFS，你应该跳过此页，并使用 BLFS 页面提供的说明配置支持 UEFI 的 GRUB。

### 10.4.1. 介绍

> 警告：错误地配置 GRUB 会导致你的系统无法运行，除非有 CD-ROM 或可启动 USB 驱动器等其他启动设备。启动你的 LFS 系统并不此部分。你可能只想修改你的引导程序，例如 Grub-Legacy、GRUB2 或 LILO。

确保启动磁盘已就绪。为了使其工作，你必须挂载 chroot。如果你不在 chroot 中，请执行：

```bash
cd /mnt/lfs
chroot /mnt
```

如果你已处于 chroot 中，请继续下一步。

生成 GRUB 镜像：

```bash
grub --output=/boot/grub.img /dev/sda
```

### 10.4.2. GRUB 命名规范

GRUB 使用 `(hdn,m)` 格式的命名，其中 n 是磁盘编号，m 是分区编号。磁盘编号从 0 开始，但分区编号从 1 开始。例如，`da1` 是 `(hd0,1)`。

### 10.4.3. 设置配置

GRUB 通过向分区写入数据来工作。建议为 `/boot` 使用较小的（200 MB）分区。

以下命令将覆盖当前的引导加载程序。如果不希望这样做（例如使用第三方引导管理器），请勿运行该命令。

```bash
grub-install /dev/sda
```

### 10.4.4. 创建 GRUB 配置文件

生成 `/boot/grub/grub.cfg`：

```bash
cat /boot/grub/grub.cfg << "EOF"
# Begin /boot/grub/grub.cfg
set default=0
set timeout=5

insmod ext2
set root=(hd0,2)
\menuentry "GNU/Linux, Linux 5.13.12-lfs-11.0" {
    linux /boot/vmlinuz-5.13.12-lfs-11.0 root=/dev/sda2 ro
}
EOF
```

## 第 11 章 结束

### 11.1. 结束

做得好！新的 LFS 系统已安装完成！祝愿你那闪亮的全新定制 Linux 系统上取得巨大成功。

创建一个 `/etc/lfs-release` 文件可能是一个好主意。通过这个文件，你（以及在我们某某时刻需要寻求帮助时）可以很容易地找到系统中安装了哪个版本的 LFS。运行以下命令创建此文件：

```
echo 11.0 > /etc/lfs-release
```

描述已安装系统的两个文件可以被安装在系统上的软件包使用，既可以是二进制形式，也可以通过构建的方式。

第一个文件显示了你的新系统相对于 Linux 标准基础（LSB）的状态。要创建此文件，运行：

```
cat > /etc/lfs-release << "EOF"
DISTRIB_ID="Linux From Scratch"
DISTRIB_RELEASE="11.0"
DISTRIB_CODENAME="<在此处输入名称>"
DISTRIB_DESCRIPTION="Linux From Scratch"
EOF
```

第二个包含大致相同的信息，被 systemd 和某些图形桌面环境使用。要创建此文件，运行：

```
cat > /etc/os-release << "EOF"
NAME="Linux From Scratch"
VERSION="11.0"
ID=lfs
PRETTY_NAME="Linux From Scratch 11.0"
VERSION_CODENAME="<在此处输入名称>"
EOF
```

请确保对 `DISTRIB_CODENAME` 和 `VERSION_CODENAME` 字段进行某种自定义，使你的系统独一无二。

### 11.2. 注册计数

既然你已经读完了这本书，你想要被记录为一名 LFS 用户吗？前往 https://www.linuxfromscratch.org/cgi-bin/lfscounter.php，通过输入你的名字和使用过的第一个 LFS 版本来注册成为 LFS 用户。

现在，让我们重启进入 LFS 吧。

### 11.3. 重启系统

现在所有软件都安装完毕，是时候重启你的电脑了。然而，你应该注意几点。你创建的系统是非常精简的，很可能不具备你继续后续所需的功能。通过在当前的 chroot 环境中从 BLFS 书中安装几个额外的软件包，你可以让自己在重启进入 LFS 安装系统后处于更好的后续位置。以下是一些建议：

- 像 Lynx 这样的文本浏览器将允许你在一个虚拟终端中轻松查看 BLFS 书，同时在另一个终端中构建软件包。

- `make-ca` 软件包将允许你设置本地信任的锚点证书，使系统能够验证远程服务器提供的 SSL 证书（例如，使用 HTTPS 的网站）。

- GPM 将允许你在虚拟终端中执行复制/粘贴操作。

- 如果你处于 `dhcpconfig` 不符合你网络需求的情况，安装如 `dhcpcd` 或 `dhcp` 的客户端部分软件包可能会有所帮助。

- 安装 `sudo` 对于以非 root 用户身份构建软件包并轻松将生成的包安装到你的系统中可能很有帮助。

- 如果你想在舒适的 GUI 环境中从远程系统访问你的新系统，请安装 `openssh`。

- 为了从互联网获取文件，请安装 `wget`。

- 为了连接无线接入点进行网络连接，请安装 `wpa_supplicant`。

- 最后，在此时阶段审查以下配置文件也是合适的：

  - `/etc/bashrc`

  - `/etc/dircors`

  - `/etc/fstab`

  - `/etc/hosts`

  - `/etc/inputrc`

  - `/etc/profile`

  - `/etc/resolv.conf`

  - `/etc/vimrc`

  - `/root/bash_profile`

  - `/root/bashrc`

  - `/etc/sysconfig/ifconfig.eth0`

既然我们已经说了这么多，让我们第一次启动我们那闪亮的全新 LFS 安装吧！从 chroot 环境退出：

```
logout
```

卸载 LFS 文件系统层次结构：

```
umount -Rv $LFS
```

现在，使用以下命令重启系统：

```
shutdown -r now
```

假设 GRUB 引导程序已如之前所述进行了设置，则菜单已设置为自动启动 LFS 11.0。

重启后，LFS 系统已准备就绪，并且可以根据需要添加更多软件。

### 11.4. 接下来怎么办？

感谢阅读这本 LFS 书。我们希望你发现这本书很有帮助，并学习了更多关于系统构建的知识。

现在 LFS 系统已经安装，你可能会想“接下来怎么办？”为了回答这个问题，我们为你整理了一份资源列表。

- 维护

  所有软件都会定期报告漏洞和安全公告。由于 LFS 系统是从源码编译的，因此跟进此类报告取决于你。有几个在线资源可以跟踪此类报告，下面列出了其中：

  - CERT（计算机应急响应小组）

    CERT 拥有一个邮件列表，用于发布有关各种操作系统和应用程序的安全警报。订阅信息可以在 http://www.us-cert.gov/cas/signup.html 获取。

  - Bugtraq

    Bugtrap 是一个完全公开的社区安全邮件列表。它发布新发现的安全问题，偶尔还会发布这些问题的潜在修复。订阅信息可以在 http://www.security.com/archive 获取。

  - Beyond Linux From Scratch

    《Beyond Linux Scratch》书籍涵盖了广泛软件的安装程序。

- LFS 提示

  LFS 提示是由志愿者提交的关于 Linux 之外问题的文档。位于 https://www.linuxscratch.org/blfs/view/11.0/

- 邮件列表

如果你需要帮助、想了解最新进展、想为项目做贡献等，可以订阅多个邮件列表。见第 11 章 - 邮件列表。

- Linux 文档项目

  Linux 文档项目 (TLDP) 的目标是协作解决所有 Linux 问题。TLDP 包含了大量的 HOWTO、指南和手册。位于 http://www.ldp.org/

## 第 V 部分 附录

# 附录 A 缩写与术语

- ABI 应用二进制接口

- ALFS 自动化 Linux From Scratch

- API 应用程序接口

- ASCII 信息交换标准

- BIOS 基础输入输出系统

- BLFS Beyond Linux Scratch

- BSD 软件发行版

- chroot 

- CMOS 互补金属氧化半导体

- COS 服务类别

- CPU 中央处理器

- CRC 冗余校验

- CVS 并版本系统

- DHCP 动态主机配置协议

- DNS 域名系统

- EGA 增强显卡

- IDE 集成驱动器

- IEEE 电气电子工程师学会

- IO 输入/输出

- IP 网络协议

- IPC 进程间通信

- IRC 即时聊天

- ELF 可执行可链接格式

- ext2 第二代扩展文件系统

- ext3 第三代扩展文件系统

- FAQ 常见问题解答

- FHS 文件层次结构标准

- FIFO 先入先出

- FQDN 完全限定域名名

- FTP 文件传输协议

- GB 千字节

- GCC GNU 编译器集

- GID 组标识

- GMT 格林尼标准时间

- HTML 超文本标记语言

- LED 发光二极管

- LFS Linux From Scratch

- LSB Linux 标准基础

- MB 字节

- MBR 主引导记录

- MD5 消息摘要 5

- NIC 网卡

- NLS 原生语言支持

- NNTP 网络新闻传输协议

- NPTL 原生 POSIX 线程库

- OSS 开放音频系统

- PCH 预编译头文件

- PCRE Perl正则表达式

- PID 进程标识

- PTY 伪终端

- QOS 服务质量

- RAM 随机访问内存

- RPC 远程过程调用

- RTC 实时钟

- SBU 标准构建单元

- SCO 圣十字公司

- SHA1 安全哈希算法 1

- TLDP Linux 文档项目

- TFTP 简单文件传输协议

- TLS 线程本地存储

- UID 用户标识

- umask 用户文件创建掩码

- USB 通用总线

- UTC 协调世界时

UUID 全局唯一标识符

VC 虚拟控制台

VGA 视频图形阵

VT 虚拟终端

# 附录 B 致谢

我们要感谢以下个人和组织对 Linux From Scratch (LFS) 所出的贡献。

- Gerard Beekmans <gerard@linuxfromscratch.org> – LFS 创建者

- Bruce Dubbs <dbubms@linuxfromscratch.org> – LFS 管理编辑

- Jim Gifford <jim@linuxfromscratch.org> – CLFS 项目共同领导人

- Pierre Labastie <pierre@linuxfromscratch.org> – BLFS 节点和 ALFS 负责人

- DJ Lucas <dj@linuxfromscratch.org> – LFS 和 BLFS 节点

- Ken Moffat <ken@linuxfromscratch.org> – BLFS 节点

- LFS 和 BLFS 邮件列表中的无数其他人员，他们通过提供建议、测试书籍以及提交错误报告（bug reports）、说明以及以及安装各种软件包的经验，帮助了这本书的成为可能。

## 翻译者

- Manuel Canales Esparca <macana@macenas-es.com> – 西班牙语 LFS 翻译项目

- Johan Lenglet <johan@linuxfromscratch.org> – 直至 2008 年法语 LFS 翻译项目
