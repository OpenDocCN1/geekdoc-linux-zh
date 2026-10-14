
进入`/path/to/xxx`目录，找到`xxx.json`。

使用更新后的配置文件重启虚拟机后，你将能够通过任何连接到虚拟机 IP 地址的 VNC 客户端连接到其控制台。你需要提供在 `vncpasswd` 条目中指定的密码才能连接到控制台，此时你需要在那里登录。

# 获取有关 Xen 的更多信息

本节仅触及了使用 Xen 可以完成的许多事情、Xen 管理命令支持的许多命令等。我认为你会发现虚拟化程序模型优于其他类型的虚拟化，而 Xen 是目前唯一的商业级开源虚拟化程序。你会发现 Xen 本身提供了一个健壮且强大的虚拟化解决方案。

## 使用虚拟机和模拟器

我在互联网上获取 Xen 最新信息的最喜来源如下：

- **Ubuntu 上的 Xen:help**: 关于 Xen 的 Ubuntu 相关信息可以在 Ubuntu 论坛找到，地址为 https://help.ubuntu.com/community/Xen。
- **Xen Wiki**: 位于 http://wiki.xenource.com/xenwiki 的开放、可编辑的 Wiki。Xen Wiki 包含了大量的信息，并且是实时的。它是查找关于虚拟化所支持/建议的处理器、针对这些处理器和 Xen 的支持/建议的主主板信息，以及大量 HOWTO 和技术信息的最佳地方。
- **Open Xen 邮件列表**: 你可以订阅的社区列表 http://lists.xensource.com。该网站提供了多个列表的访问权限，你可以订阅这些列表，或者直接浏览搜索存档。这些列表包括多个领域，如标准 Xen 用户 (`xen-users`)、Xen 开发者社区 (`xen-dev`)、Xen 开源工具开发者 (`xen-tools`) 以及专注于 Xen 安全的开发者 (`xen-dev`)。在这些列表中，用户邮件列表可能对大多数人最有用。对于大多数列表，你可以订阅它们并在每条消息发送时接收，但实时接收可能会让你应接不暇。
- **Citrix 论坛**: 针对 Citrix 提供的商业 Xen 产品的邮件列表，但对公众开放。你可以在 http://forums.citrix.com 注册这些论坛，或者浏览其主题。如果你是 Citrix 用户并想要提问，这些论坛会很有用。再次，这些论坛专门针对 Citrix 的 Xen，但仍然经常包含对开源 Xen 用户的相关信息。
- **其他发行版上的 Xen**: 像 Fedora 和 Novell/SUSE 等 Linux 发行版是各种 Xen 相关资源的积极倡导者。Fedora 提供了关于开始使用 Xen、Xen 工具以及相关列表的通用信息，你可以在 https://www.redhat.com/mailman/listinfo/fedora-xen 找到它。Novell 在 http://forge.novell.com/modules/project/xenpreview 提供了“Xen 技术预览”，其中包含了最新 Xen 补丁的信息以及指向 Xen 文档和其他网站的通用链接。

## 安装和使用 QEMU

`QEMU` (http://bellard.org/qemu) 是由 Bellard 和其他人开发的一个极其强大的开源 CPU 模拟器。`QEMU` 可以模拟各种架构、处理器和相关的外设硬件。`QEMU` 可以运行为这些架构（包括 32 位和 64 位 x86、32 和 64 位 PowerPC、Motorola 68000、32 和 64 位 SPARC、SH、MIPS 和 ARM）编译的操作系统和软件。`QEMU` 为这些处理器/架构中的每一个虚拟化硬件环境，包括 CPU 以及外设设备如一个或多个串口、网络接口、PCI 总线、VGA 图形适配器、音频硬件、磁盘驱动器、USB 组件等。这让你能够运行适用于这些任何架构的未经修改的操作系统。例如，图 B-38 显示了一个 xterm 窗口，`QEMU` 启动了 MIPS 内核，并正在运行为 MIPS 平台编译的操作系统二进制文件。

### 第四部分

### 附章节

图 7-38

在 QEMU 下运行的 MIPS 内核和内核工具

![](img/e3248f698da647444405a34229bd9df5_1475_0.png)

Last Modified Nov 1, 2009 by Paul Gerbner

```
EB*00 ethercard probe at 02:00:01 92:54:00 12:34:56

linux version 2.6.31-generic #1

Uniform Multi-Platform v1.06 Kernel revision: 1.0.alpha2

idebus: QEMU-virtio PID models override with idebus===

hmdc: QEMU-virtio IDE/QEMU-KVM drive

ata0: device=/dev/hda

kernel v2.6.0: Packet Logger for kernel performance testing.

tcp: no-server is enabled

mmi1: Registered protocol m1

net: Registered protocol IPv6

QEMU:less memory image found at 0

UFS: Hard mount crashes filesystem randomly.

freeing unused kernel memory: 152K Free

Boxbox v1.2.1 (Debian 1.1.3)-built-in shell (ash)

type --help for a list of built-in commands

/bin/sh: can access tty: jdb control turned off

- uname -a

Linux 2.6.31-qemu #11
```

要在 Ubuntu 或 Ubuntu 系统上安装 QEMU，可以使用 apt 安装：

```
sudo apt update

sudo apt install qemu-system
```

安装完成后，你可以使用 `qemu-system` 命令来启动虚拟机。例如，启动一个 x86_64 虚拟机：

```bash
qemu-system-x86_64 -m 2G -hda your_image.qcow2
```
