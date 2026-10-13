

打印机或扫描仪。

```
# mknod -m 660 /dev/lp3 c 6 3
# chown root /dev/lp3
# chgrp lp /dev/lp3
```

## 设备信息：/proc 和 /etc/sysconfig/hwconf

在 Red Hat 系统中，Kudzu 会在 /etc/sysconfig/hwconf 文件中维护已安装的所有硬件设备的完整配置文件（/etc/sysconfig 在第 30 章中有讨论）。如前所述，此文件由 Kudzu 更新；新硬件会被添加，旧设备则会被移除。条目定义了配置变量，例如设备类型（视频、CD-ROM、硬盘等）、使用的总线（PCI、IDE 等）、设备名称（如 hdd 或 st0）、使用的驱动程序以及设备的描述。此处显示了一个鼠标条目：

```
class: MOUSE
bus: PSAUX
detached: 0
device: psaux
driver: genericps/2
desc: "Generic 3 Button Mouse (PS/2)"
```

/proc 文件系统（参见第 30 章）为您的设备维护特殊的信息文件。/proc/devices 文件列出了所有已安装的控制字符设备和块设备及其主设备号。当前用于设备的 IRQ、DMA 和 I/O 端口分别列在 interrupts、dma 和 ioports 文件中。某些文件列出了涵盖多个设备的信息，例如 pci 文件列出所有 PCI 设备，sound 文件列出所有声音设备。sound 文件列出了关于声卡的详细信息。某些子目录，如 net、ide 和 scsi，包含不同设备的信息文件。某些文件保存可以动态更改的配置信息，例如 IP 数据包转发能力和最大文件数。您可以使用 redhat-config-proc 工具（系统工具菜单中的“内核调优”）或通过手动编辑某些文件来更改这些值。表 32-2 列出了几个与设备相关的 /proc 文件（其他条目请参见第 30 章）。

### 表 32-2：Proc 设备信息文件

| 文件 | 描述 |
|---|---|
| /proc/devices | 列出当前运行内核配置的设备驱动程序 |
| /proc/dma | 显示当前使用的 DMA 通道 |
| /proc/interrupts | 显示正在使用的 IRQ（中断） |
| /proc/ioports | 显示正在使用的 I/O 端口 |
| /proc/pci | 列出 PCI 设备 |
| /proc/sound | 列出声音设备 |
| /proc/scsi | SCSI 设备的目录 |
| /proc/ide | IDE 设备的目录 |
| /proc/net | 网络设备的目录 |

## 安装和管理终端及调制解调器

在 Linux 中，可能有多个用户同时登录。当然，每个用户都需要拥有自己的终端来访问 Linux 系统。您电脑上的显示器充当特殊的终端，称为控制台，但您可以通过 PC 上的串行端口或安装在 PC 上的专用多端口卡添加其他终端。其他终端可以是独立终端，也可以是使用终端仿真程序的 PC。关于终端安装的详细说明，请参阅 /usr/share/doc/HOWTO 目录下的 Term-HOWTO 文件（作为 Red Hat 文档 CD-ROM 的一部分安装）或在 Linux 文档项目网站（www.tldp.org）上查找。此处提供了一个简要说明。

### 串行端口

您电脑上的串行端口被称为 COM1、COM2、COM3 和 COM4。这些串行端口对应于终端设备 /dev/ttyS0 到 /dev/ttyS3。请注意，这些串行端口中的一些可能已被其他输入设备（如鼠标）和通信设备（如调制解调器）使用。如果您有串行打印机，那么其中一个串行设备已被其使用。如果您安装了多端口卡，则有更多端口可供选择。对于每个添加的终端，您必须在 Linux 系统上创建一个字符设备。与打印机一样，您使用 mknod 命令创建终端设备。终端设备的权限为 660。终端设备是主设备号为 4、次设备号通常从 64 开始的字符设备。

提示 /etc/fstab 文件中的 /dev/pts 条目在 /dev/pts 挂载了一个 devpts 文件系统，用于 Unix98 伪终端。这些伪终端通过编号命名的设备标识。

### mingetty, mgetty 和 agetty

终端设备通过 getty 程序及一组配置文件由您的系统管理。系统启动时，它读取 inittab 文件中已连接终端的列表，然后为每个终端执行相应的 getty 程序，即 mingetty、mgetty 或 agetty。这些 getty 程序负责建立 Linux 系统与指定终端之间的通信。mingetty 为虚拟控制台提供最基本的支持，而 agetty 提供增强的终端连接支持。agetty 还包括波特率和超时的参数。mgetty 专为传真/调制解调器连接设计，允许您配置拨号、登录和传真参数。mgetty 配置文件保存在 /etc/mgetty+sendfax 目录中。调制解调器连接信息保存在 /etc/mgetty+sendfax/mgetty.config 文件中。所有 getty 程序都可以读取放置在 /etc/issue 文件中的初始消息，该消息可以包含特殊代码以提供系统名称和当前日期及时间。

### termcap 和 inittab 文件

/etc/inittab 文件保存系统管理终端设备的指令。/etc/inittab 文件中的一行有四个基本组成部分：ID、运行级别、动作和进程。终端设备由 ID 号标识，从第一个设备的 1 开始。终端操作的运行级别通常是 1。动作通常是 respawn，意味着持续运行该进程。进程是对 mingetty、mgetty 或 agetty 的调用，并附带终端设备名称。/etc/termcap 文件保存不同终端类型的规格。这些是用户登录您的系统时可能使用的不同类型终端。您的 /etc/termcap 文件已经填入了大多数当前生产的终端的规格。/etc/termcap 文件中的条目由可用于终端的各种名称组成，名称之间用管道符 (|) 分隔，然后是一系列参数规格，每个规格以冒号结尾。您在此处可以找到特定终端类型使用的名称。您可以使用 more 命令显示您的 /etc/termcap 文件，然后使用搜索 (/) 来定位您的终端类型。您可以为终端设备设置许多选项。要更改这些选项，请使用 stty 命令，而不是直接更改配置文件。不带参数的 stty 命令列出终端的当前设置。

### tset

当用户登录时，使用 tset 命令初始化终端设备是很有帮助的。通常，**tset** 命令放置在用户的 **.bash_profile** 文件中，并在用户每次登录系统时自动执行。您使用 **tset** 命令设置终端类型以及终端设备所需的任何其他选项。以下是 **.bash_profile** 文件中 **tset** 的一个常见条目。**-m dialup:** 选项提示用户输入终端类型。此处指定的类型是默认类型，显示在括号中。用户按 ENTER 键选择默认值。提示看起来像这样：**TERM=(vt100)?**。

```
eval `tset -s -Q -m dialup:?vt00`
```

## 输入设备

鼠标和键盘等输入设备在多个层面上显示。初始配置在安装过程中进行，此时您需要选择鼠标和键盘类型。您可以使用管理配置工具（如 redhat-config-mouse 和 redhat-config-keyboard，位于“系统设置”菜单和窗口中的“鼠标和键盘”项）更改该配置。X Window 系统以及 KDE 和 GNOME 桌面环境也为鼠标和键盘提供了特殊配置。您可以选择键盘布局和语言，并配置鼠标的速度和显示效果。

