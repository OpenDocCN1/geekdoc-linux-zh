
来自 Ubuntu 备用 CD 的安装程序看起来与桌面 CD 的程序非常不同，但提出的问题很大程度上是相同的。备用 CD 完全是基于文本的，起初可能有些令畏，但你会发现以这种方式安装 Ubuntu 更快，因为不需要加载整个桌面会话。

记住，CD 会为你设置好 LTSP。如果你计划运行 LTSP 服务器，最简单的安装方法是使用 Ubuntu 备用 CD。

CD 启动后，按 F4 并选择“安装到硬盘（Install to the Hard Disk）”选项。按 Enter 键确认开始安装。注意此时的工作站和命令行选项。

你遇到的第一个问题仅仅是设置安装过程中使用的语言，以及最终系统的语言。然后你会被要求选择位置。

现在你必须选择键盘布局。基于文本的安装程序有一个自动检测程序，要求你在键盘上按下一系列键。通过这些键，安装程序可以判断出最适合你的键盘布局。如果有任何键盘变体，现在会呈现给你选择。

安装程序现在将加载各种组件。如果你的计算机上有多个 NIC，将被要求选择作为安装期间的主要网卡（图 9-8）。通过此，安装程序想要知道哪块网卡连接到外部网络或互联网。

如果你的网络启用了 DHCP，此网卡将从网络设置 IP 地址。然后你将被提示为 LTSP 服务器选择主机名。如果你的网络没有启用 DHCP，你必须手动设置 IP 地址。

下一步是准备硬盘以进行安装。这里最简单的方法是选择“引导分区（Guided Partitioning）”。如果你想使用 LVM，请参考第 2 章和第 5 章中关于 LVM 的部分。如果你需要深入的分区或硬盘上已有不想丢失的数据，你必须规划如何进行。如果你安装在 Ubuntu 可以调整大小的分区上，它将为你提供该选项。这将允许你在一台电脑上安装两个操作系统并在启动时进行切换。

虽然 Ubuntu 的调整大小工具非常出色，但在执行此类操作之前，你应该始终备份数据。

之后，你必须选择你的时钟是否设置为协调世界时（UTC）。你的系统时钟应设置为 UTC。操作系统负责将系统时间转换为本地时间。

```
你的系统有多个网络接口。选择一个作为安装期间的主要网络接口。如果可能，已选择第一个连接的网接口。
主网络接口:
eth0: Advanced Micro Devices [AMD] 79c970 (PCInet32 LANCE)
heti: Advanced Micro Devices [AMD] 79c970 (PCInet32 LANCE)
Do Back>
```

![](img/aa15f1f82061fdaf4ff1da575e3e1c52_382_0.png)

除非你还有另一个要求系统时间为本地时间的操作系统，否则你应该在此处回答“yes”。

现在是时候在系统上设置第一个用户了。请记住，该用户将拥有完全的管理权限。首先，输入用户名，然后输入所需的用户名，最后输入两次密码。完成后，基础系统即完成安装。

在经过几个步骤后，你会看到一个关于屏幕分辨率的问题。对于你正在安装的系统类型，过高的屏幕分辨率可能会导致服务器与客户端之间的连接缓慢。默认选项就可以了。

完成后，安装程序将开始构建 LTSP 客户端根文件系统（图 9-9）。这就是本章前面提到的极简版 Ubuntu。它本质包含一个内核和一个 X 服务器。

这一步似乎需要很长时间，进度条更新并不频繁。耐心点，吃个零食——它最终会完成的。

完成后，提示将要求你移除 CD 并按回车重启系统进入你新的 Edubuntu 服务器。

## 初始化 LTSP 服务器设置

安装在 Ubuntu 机器上的 DHCP 服务器将自动启动，因此剩下的工作就是让你的瘦客户端从网络启动。如果你使用的是之前提到的单网卡设置，并且你的网络已经有了 DHCP 服务器，请不要启动 Ubuntu DHCP 服务器，因为这可能会导致 DHCP 服务不可用。

![](img/aa15f1f82061fdaf4ff1da575e3e1c52_383_0.png)

图 9-9 构建 LTSP 文件系统

### 提示

如果你仍在运行 Edubuntu Dapper 6.06 LTS 版本，还需要多做一些工作。最新版本的 Ubuntu 具有自动 DHCP 配置生成器。这意味着它们在通常的 LTSP 环境下不需要手动配置。6.06 LTS 版本需要手动配置 DHCP 服务器；请访问 `https://www.ubuntu.org/GettingStarted` 获取更多说明。

## 初始化 Ubuntu 客户端设置

修改客户端计算机从网络启动通常是通过更改机器 BIOS 中的设置来实现的。查看计算机主板的说明书以了解如何更改这些设置是一个好主意。对于大多数机器，只需在启动时按 `Delete` 键进入 BIOS 并更改启动优先级即可。

一旦你设置好客户端机器从网卡启动，你就应该在每个客户端上看到与图 9-10 显示的类似的屏幕。这意味着客户端机器已经颁发了地址，并且 PXELUX 文件已从网络加载。

![](img/aa15f1f82061fdaf4ff1da575e3e1c52_384_0.png)

```
XELINUX 3.11 Debian-2008-03-16 Copyright (C) 1994-2005 H. Peter Anvin
UBDI data segment at 0089C7F0
UBDI data segment size: 248
UBDI code segment at 0088ECC0
UBDI code segment size: 000
px entry point found (hope) at 92ECC:0186
MY IP address seems to be CAA0AFA 192.168.0.258
IP192.168.0.100-192.168.0.254 192.168.0.1:255.255.255
TFTP prefix: /tftp/
Trying to load: pxlinux.cfg/01-8bc-29-a3-9c-ba
Trying to load: pxlinux.cfg/CAA0FA
Trying to load: pxlinux.cfg/CAR08F
Trying to load: pxlinux.cfg/CAR0A0
Trying to load: pxlinux.cfg/C0A0
Trying to load: pxlinux.cfg/CBA
Trying to load: pxlinux.cfg/C
Trying to load: pxlinux.cfg/default
Loading weinitux.
Loading initrd.img...
Ready...
```

图 9-10 DHCP 启动

如果你的客户端启动到了图形登录界面，且屏幕与图 9-11 所示类似，恭喜你——你已经成功设置了 LTSP 瘦客户端系统。如果不是，请参考本章末尾的 LTSP 故障排除章节。

## 如果已安装 Ubuntu，则切换到 Edubuntu

就像 Kubuntu 一样，Edubuntu 仅仅是来自 Ubuntu 仓库的一一组自定义包。寻找名为 `edubuntu-desktop` 的包。该包将同时安装 Edubuntu 桌面和其他所有所需的教育应用程序。这一步还将安装最新的 Edubuntu 艺术包，它将使用最新的教育壁纸和主题来定制你的桌面。如果你出于任何原因需要回到 Ubuntu 桌面，只需安装 `ubuntu-desktop` 包，你的系统将恢复到安装 Edubuntu 之前的状态。如果你需要 LTSP 设置，你将需要大量的手动配置。

## 在 Ubuntu 或桌面版安装中安装 LTSP 环境

你可能已经拥有一台 Ubuntu 机器，并希望在 LTSP 设置中使用它。实现这一点的程序非常简单，并且需要

![](img/aa15f1f82061fdaf4ff1da575e3e1c52_385_0.png)

大部分编辑工作发生在 `/var/lib/tftboot/ltsp/<path>` 目录下的 `pxelinux.cfg/default` 文件中。该文件的格式与旧的 LILO 配置语法非常相似（对于熟悉引导程序的你）。以下示例配置将向显示一个消息，稍后会解释。用户随后可以选择允许系统启动其默认配置（在本例中为本地硬盘），或者输入 `linux` 字并按回车，这将加载 LTSP 瘦客户端。

```
DEFAULT localboot
TIMEOUT 50
PROMPT 1
DISPLAY display.msg

LABEL linux
KERNEL vmlinuz
APPEND ro initrd=initrd.img quiet splash

LABEL localboot
LOCALBOOT 0
```

让我们来看这个配置文件并对其拆解，以便你可以创建适合自己环境的配置。（如果此示例文件已经符合你的需求，你可以直接跳到创建 `display.msg` 文件的部分。）

`DEFAULT` 关键字指定在超时后选择哪种启动选项。`TIMEOUT` 选项指定在启动默认选项之前等待多久。此超时时间以秒分之一为单位；因此，值 `50` 表示设置为 5 秒。`PROMPT` 选项指定 PXE 软件是否显示启动提示符，以允许用户选择操作系统。`DISPLAY` 选项在屏幕上显示一个文本文件
