
| `knoppix lang=xx` | 将键盘语言设置为双字母代码 `xx`（其中 `xx` 是简体中文，`de` = 德语，`es` = 西班牙语，`fr` = 法语，`it` = 意大利语，`nl` = 荷兰语，`pl` = 波兰语，`ru` = 俄语，`sk` = 斯洛克语，`tr` = 土耳其语，`us` = 美国）。 | | |

| `knoppix mem=256M` | 指定 PC 的内存大小（兆字节）。 | | |

| `knoppix myconf=/dev/hd1` | 从存放 `knoppix.sh` 的 `/dev/hd1` 分区运行 `knoppix.sh` shell 脚本。 | | |

| `knoppix myconf=scan` | 让 Knoppix 搜索。 | | |

# 42 解决其他安装问题

| 启动命令 | 功能 | 表 3-2 (继续) |

| :--- | :--- | :--- |

| `knoppix noject` | 不弹出 CD。 | |

| `knoppix noprompt` | 不提示。 | |

| `knoppix nowheel` | 强制 PS/2。 | |

| `knoppix xxxxx` | 禁用。 | |

| `knoppix agga-off` | 禁用 VGA。 | |

| `knoppix pnp-off` | 禁用 ACPI。 | |

| `knoppix screen=resolution` | 设置分辨率。 | |

| `knoppix testcd` | 检查 CD 完整性。 | |

| `knoppix tohd=/dev/hd1` | 到硬盘。 | |

| `knoppix toram` | 使用 RAM。 | |

| `knoppix vga=ext` | 使用 VGA。 | |

| `knoppix vsync=60` | 设置垂直同步率。 | |

| `knoppix wheelmouse` | 使用 PS/2。 | |

| 启动命令 | 功能 | 书 I |

| :--- | :--- | :--- |

|  | 启动 | |

| | 启动 X 模块 | |

| | `xmodule=modname` | |

| | `xserver=progname` | |

## 解决 PC 重启问题

在某些 PC 上，当你在启动提示符处按回车时，初始 Linux 内核会加载并立即重启 PC。这可能是由于 PC 的 BIOS 中 ACPI 实现不当导致的。要绕过此问题，请在启动提示符处输入 `linux acpi=off` 来关闭 ACPI。如果不起作用，请考虑表 3-3 中你可能想要尝试的其它启动选项。

## 使用 Linux 内核启动选项

当你从 DVD 或第一张光盘启动 PC 进行 Linux 安装时，你会在启动提示符处看到一个文本界面。通常，你只需在该提示符处按回车或什么都不做，安装就会很快开始。然而，你可以在启动提示符处指定各种选项。这些选项控制 Linux 内核启动的各个方面，例如禁用对疑故障硬件的支持，或使用特定的驱动模块启动 X 服务器。其中某些启动选项可能帮助你绕过安装过程中可能遇到的问题。

要使用这些启动选项，通常你输入 `linux` 后跟启动选项。例如，要执行文本模式安装并告诉内核你的 PC 有 512MB 内存，你在启动提示符处输入以下内容：

```
linux text mem=512M
```

参考表 3-3 获取 Linux 启动选项的简要总结。你可以使用这些命令来开启或关闭功能。

| 启动选项 | 作用 |

|---|---|

| `allowcddma` | 为 CD/DVD 驱动器启用 DMA。 |

| `apic` | 解决 Intel 440GX BIOS 中常见的错误，且仅在内核安装内核时执行。 |

| `acpi=off` | 如果 ACPI 出现问题则禁用 ACPI。 |

| `dd` | 在安装 Red Linux 时提示输入驱动盘。 |

| `display=IP_address:0` | 使安装程序的 GUI 出现在由 IP 地址识别的远程系统上。（确保你在运行安装程序的远程系统主机上运行了 `xhost +hostname` 命令）。 |

| `driverdisk` | 在安装 Red Hat 时提示输入驱动盘。 |

| `enforcing=0` | 关闭安全增强型 Linux (SELinux) 强制访问控制。 |

## 解决其他安装问题

| 启动选项 | 作用 | 第一本书 |

|---|---|---||

| `expert` | 允许对可移动介质进行分区并提示驱动盘。 | | |

| `ide=nodma` | 禁用所有 IDE 设备上的 DMA，当你遇到 IDE 相关问题时非常有用。 | | |

| `ks` | 使用 DHCP 配置以太卡，并使用 DHCP 服务器提供的启动服务器参数识别的 NFS 服务器运行 kickstart 安装。 | | |

| `ks=kickstartfile` | 使用由 `kickstartfile` 指定的 kickstart 文件运行 kickstart 安装。（其背后的设计理念是创建一个包含所有安装选项的文本文件，然后通过启动并提供 kickstart 文件作为输入来启动安装。） | | | |

| `lowres` | 强制安装程序 GUI 以较低分辨率（640 x 480）运行。 | | |

| `mediacheck` | 提示检查 CD 镜像（也称为 ISO 镜像）的完整性。通过计算 MDS 校验和并对比来检查镜像。检查 CD-ROM 可能需要几分钟。 | | | |

| `mem=xxx` | 覆盖内核在 PC 上检测到的内存量。（某些旧设备设备只能检测到 16MB 内存，在某些新机器上，显卡可能会使用主内存的一部分。）确保将 `xxx` 替换为你 PC 内存的兆字节数。 | | | |

| `nmi_watchdog=1` | 启用利用不可掩断中断 (NMI) 的内置内核检测器。 | | | |

| `noaptic` | 防止内核使用高级可编程中断控制器 (APIC) 芯片。（你可以在已知有缺陷 APIC 的主板上使用此选项。） | | | |

| `nofirewire` | 不 FireWire。 | | | |

| `noht` | 禁用超线程，这是一项允许单个处理器在硬件层上充当多个虚拟处理器的功能。 | | | |

| `nomce` | 禁用由机器检查异常 (MCE) 对 CPU 执行的自诊断检查。在某些机器上，这些检查执行过于频繁，需要禁用。 | | | |

# 46 解决其他安装问题

| 表 3-3（续） |

| 启动选项 | 作用 |

| :--- | :--- |

| `nomount` | 在救援模式下不自动挂载已的 Linux 分区。 |

| `nopass` | 不将键盘和鼠标信息传递给安装程序的第二阶段。 |

| `nopcmcmia` | 忽略系统中的任何 PCMCIA 控制器。 |

| `nprobe` | 禁用自动硬件检测，并提示用户有关 PC 上安装的 SCSI 和网络硬件的信息。你可以通过这种方法向模块传递参数。 |

| `noshell` | 在安装期间禁用虚拟控制台 2（通过 Ctrl+Alt+F2 进入的）上的 shell 访问。 |

| `nousb` | 在安装期间禁用加载 USB 支持。（如果安装程序在过程早期挂起，则在没有 USB 支持的情况下启动可能会有帮助。） |

| `nousstorage` | 在安装程序的加载器中禁用加载 usstorage 模块。此选项可能有助于 SCSI 系统上的设备排序问题。 |

| `reboot=b` | 更改内核尝试重启 PC 的方式，即使内核在关机期间挂起也会重启。 |

| `pci=noacpi` | 使内核不使用 ACPI。 |

| `pci=bios` | 使内核使用 BIOS 路由中断。 |

| `rescue` | 以救援模式启动内核。 |

| `resolution=xxx` | 指定分辨率，例如 640x480、800x640 或 1024x768。 |

| `selinux=0` | 禁用 SELinux。 |

| `serial` | 启用串口输出。 |

| `skipddc` | 跳过显示数据通道 (DDC) 检测。 |

| `vnc` | 启动 VNC（虚拟网络计算）服务器，以便从另一个系统控制 GUI。 |

# 设置打印机 47

![71f80d7808bf5bad1239cc29be7bab2_60]

书中

虽然我在故障排除时提到了这些 Linux 内核启动命令，但你可以在任何启动 PC 时使用它们。

故障排除配置

## 设置打印机

在大多数 Linux 发行版中，只有在安装发行版后才能设置打印机。以下章节概述了 Ubuntu 的打印机配置步骤，适用于所有发行版。

要设置打印机，请按照以下步骤操作：

1. 从桌面选择设置：打印机。如果你不是以 root 登录，打印机配置工具会提示输入 root 密码。图 3-1 所示的打印机配置工具名为 `system-config-printer`。

点击添加。如果设备可以被识别，它将出现在列表中。如果无法识别，你仍然可以继续安装并手动添加所需的驱动程序和配置数据。图 3-2 显示了连接到串口的 Epson Stylus 打印机。

2. 点击“下一步”继续。
