
### 表 3-2（续）

| 启动命令 | 功能说明 |
| :--- | :--- |
| knoppix pci=bios | 对存在缺陷的 PCI 控制器直接使用 BIOS |
| knoppix pnpbios=off | 跳过即插即用 (PnP) BIOS 初始化 |
| knoppix screen=1280x1024 | 将屏幕分辨率设置为 1280 x 1024 像素（请输入您想要的任何分辨率，例如 1024x768、800x600、640x480 等） |
| knoppix testcd | 通过使用 MD5 校验和来检查 Live CD 的数据完整性 |
| knoppix tohd=/dev/hda1 | 将 Live CD 复制到指定的硬盘分区，并从中运行 |
| knoppix toram | 将 Live CD 复制到 RAM（内存）并从中运行（需要 1GB 内存） |
| knoppix vga=ext | 使用 50 行文本模式显示 |
| knoppix vsync=60 | X 窗口系统使用 60 Hz 的垂直刷新率（请输入您希望 X 使用的垂直刷新率） |
| knoppix wheelmouse | 为滚轮鼠标启用 IMPS/2 协议 |
| knoppix xmodule=modname | 使 X 服务器加载由 modname 指定的模块，以便 X 能在您的显卡上工作（modname 可以是 ati1、fbdev、i810、mga、nv、radeon、savage、svga 或 s3 之一。） |
| knoppix xserver=progname | 启动由 progname 指定的 X 服务器（可以是 XFree86 或 XF86_SVGA 之一） |

![](img/792720823146d68f19fd50c99ebfce4b_111_0.png)

当您有多个 Knoppix 启动命令时，只需将它们组合到一行中即可。例如，要指定跳过 SCSI 自动检测、关闭 ACPI、使用美国键盘布局、使用滚轮鼠标，并要求 X 服务器加载 nv 模块，您应在 boot: 提示符下输入以下内容：

`knoppix noSCSI acpi=off lang=us wheelmouse xmodule=nv`

## 致命的信号 11 错误

有些人在安装过程中会遇到致命的信号 11 错误消息——这会立即停止进程。此错误通常发生在初始启动屏幕之后，安装程序开始启动其图形用户界面 (GUI) 或文本界面时。安装过程中出现信号 11 错误最可能的原因是与内存或与 CPU（微处理器）相关的缓存有关的硬件错误。

## 解决其他安装问题

信号 11，也称为 SIGSEGV（Segment Violation Signal 的缩写，即段违例信号），可能会发生在 Linux 应用程序中。当进程试图访问它不应访问的内存位置时，会发生*段违例*。操作系统在问题发生前检测到该问题，并通过向违规进程发送信号 11 来停止该进程。如果这种情况发生在安装过程中，这意味着安装程序在访问内存时出现了错误，最可能的原因是硬件问题。针对信号 11 问题常用的建议修复方法是关闭 BIOS 中的 CPU 缓存。为此，您必须在 PC 启动时进入 Setup（通过按功能键，如 F2），并从 BIOS Setup 菜单中关闭 CPU 缓存。

![](img/792720823146d68f19fd50c99ebfce4b_112_0.png)

如果问题是由于内存中的硬件错误引起的（换句话说，是由于内存芯片故障导致的），您可以尝试将内存模块在插槽之间互换位置。如果您手头有备用模块，也可以考虑用另一个内存模块替换现有的内存模块。

您可以访问 www.bitwizard.nl/sig11 阅读更多关于信号 11 问题的信息。

## 绕过 PC 重启问题

在一些 PC 上，当您在启动提示符下按 Enter 键时，初始 Linux 内核加载后会立即重启 PC。这可能是由于 PC BIOS 中 ACPI 的实现存在缺陷所致。要绕过此问题，请在启动提示符下输入 **linux acpi=off** 以关闭 ACPI；如果不起作用，请查阅表 3-3 以查找您可能想要尝试的其他启动选项。

## 使用 Linux 内核启动选项

当您从 DVD 或第一张 CD-ROM 启动 PC 进行 Linux 安装时，会出现带有 boot: 提示符的文本屏幕。通常，您在该提示符下按 Enter 键或不做任何操作，安装程序稍后就会开始。但是，您可以相当多地指定 boot: 提示符下的各种选项。这些选项控制 Linux 内核启动的各个方面，例如禁用对故障硬件的支持，或使用特定的 X 驱动模块启动 X 服务器。其中一些启动选项有助于绕过您在安装过程中可能遇到的问题。

要使用这些启动选项，通常您需要输入 **linux** 后跟启动选项。例如，要执行测试模式安装并告诉内核您的 PC 有 512MB 内存，请在 boot: 提示符下输入以下内容：

```
linux text mem=512M
```

请查阅表 3-3 以获取部分 Linux 启动选项的简要摘要。您可以使用这些命令来开启或关闭特定功能。

虽然我在讨论安装问题故障排除的上下文中提到了这些 Linux 内核启动命令，但您可以随时使用其中许多命令，只要您使用任何 Linux 发行版启动 PC 并希望开启或关闭特定功能即可。

### 表 3-3 一些 Linux 启动选项

| 使用此启动选项 | 以执行此操作 |
| :--- | :--- |
| allowcdmdma | 为 CD/DVD 驱动器启用 DMA |
| apic | 解决在 Intel 440GX 芯片组 BIOS 中常见的错误，并且仅在安装程序内核上执行 |
| acpi=off | 如果存在 ACPI 问题，则禁用 ACPI |
| dd | 在 Red Hat Linux 安装过程中提示输入驱动器软盘 |
| display=IP_address:0 | 使安装程序 GUI 显示在由 IP 地址标识的远程系统上。（请确保您在运行安装程序的远程系统上执行命令 `xhost +hostname`，其中 hostname 是运行安装程序的主机。） |
| driverdisk | 在 Red Hat Linux 安装过程中提示输入驱动器软盘 |
| enforcing=0 | 关闭 Security Enhanced Linux (SELinux) 强制访问控制 |
| expert | 允许您分区可移动介质并提示输入驱动器软盘 |
| ide=nodma | 在所有 IDE 设备上禁用 DMA，在您遇到与 IDE 相关的问题时可能很有用 |
| ks | 使用 DHCP 配置网卡，并使用 NFS 服务器上的 kickstart 文件进行 kickstart 安装，该服务器由 DHCP 服务器提供的启动服务器参数标识 |
| ks=kickstartfile | 使用指定的 kickstartfile 中的 kickstart 文件进行 kickstart 安装。（kickstart 背后的理念是创建一个包含所有安装选项的文本文件，然后通过启动并提供该 kickstart 文件作为输入来触发安装。） |
| lowres | 强制安装程序 GUI 以较低分辨率 (640 x 480) 运行 |
| mediacheck | 提示您检查 CD 映像（也称为 ISO 映像）的完整性。检查映像是通过计算 MD5 校验和并将其与官方的 Fedora Core 值进行比较来完成的。检查 CD-ROM 可能需要几分钟时间。 |
| mem=xxxM | 覆盖内核在 PC 上检测到的内存数量。（一些旧机器可能只能检测 16MB 内存，而在一些新机器上，显卡可能会使用主内存的一部分。）请确保将 xxx 替换为代表您的 PC 上内存兆字节数的数字。 |
| nmi_watchdog=1 | 启用利用不可屏蔽中断 (NMI) 的内核内置死锁检测器 |

