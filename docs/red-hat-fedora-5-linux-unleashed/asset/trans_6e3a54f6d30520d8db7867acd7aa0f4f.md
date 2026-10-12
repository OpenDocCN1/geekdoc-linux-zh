

使用 `hwclock` 及其 `--set` 和 `--date` 选项可以手动设置硬件时钟，方法如下：

```
# hwclock --set --date '01/27/08 08:00:00'
# hwclock --show
Tue 27 Jan 2008 08:00:08 AM GMT -0.151718 seconds
```

在这些示例中，硬件时钟已通过 `hwclock` 进行了设置，随后再次使用它来验证新的硬件日期和时间。您也可以使用 `hwclock` 根据硬件时钟的值来设置 Linux 系统日期和时间。

例如，要从 PC 的硬件时钟设置系统时间，请使用 `--hctosys` 选项，方法如下：

```
# hwclock --hctosys
```

要根据系统时间设置硬件时钟，请使用 `--sysctohc` 选项，方法如下：

```
# hwclock --sysctohc
```

## 使用 system-config-date 客户端

Fedora 图形化 X 工具 `system-config-date` 可用于设置系统日期和时间。您可以通过点击桌面菜单中的“系统设置” -> “日期和时间”菜单项，或在 X11 终端窗口中通过命令行输入以下命令来启动该客户端：

```
$ system-config-date &
```

按下回车键后，系统会提示您输入 root 密码。输入 root 密码并点击“确定”按钮。随后您将会看到如图所示的窗口（图 4.9）。

通过日历和时间字段来设置日期和时间。您还可以通过在网络时间协议字段中输入远程时间服务器主机名，让工作站通过网络获取更新的日期和时间信息。这需要 `ntpd` 时间守护进程正确配置并正在运行。

> **注意**
> 
> 关于使用 `ntpd` 守护进程的 HTML 文档位于 `/usr/share/doc/http*`/ntpd.htm（如果系统中安装了 `ntpd`）。

点击“时区”选项卡可修改或验证系统时区。当前系统时区由 `/etc` 目录下一个名为 `localtime` 的文件指定，该文件是 `/usr/share/zoneinfo` 目录下相关时区数据库文件的副本。例如，

![](img/2045828cf45e5632bf056f9ca99d6755_144_0.png)

图 4.9 使用 Fedora 的 `system-config-date` 客户端设置系统日期和时间。

```
$ ls -l /etc/localtime
-rw-r--r-- 1 root root 1267 Apr 1 16:39 /etc/localtime
$ ls -l /usr/share/zoneinfo/America/New_York
-rw-r--r-- 5 root root 1267 Mar 13 18:00 /usr/share/zoneinfo/_America/New_York
```

如果您使用 `system-config-date` 更改时区，此文件将会改变。

## 管理 PCMCIA

移动 Linux 用户利用笔记本的 PCMCIA 插槽添加 70 针、信用卡大小的设备，以支持以太网局域网连接、无线操作、FireWire 设备、Compact Flash 硬盘、外部存储设备、串口和调制解调器。Linux 内核和 David Hinds 的 Card Services 软件支持许多不同类型的 PCMCIA 卡和位于 PCMCIA 托架中的 Compact Flash 外形卡。

PCMCIA 设备和适配器直接通过卡槽供电，尽管某些外部硬件可能需要额外的电源。PCMCIA 支持在启动时启用和配置。然而，在较新的 Linux 内核中，支持是通过内核模块或直接的 Linux 内核支持提供的。

### 使用 PCMCIA

PCMCIA Card Services 软件在插入卡片时通过一个或多个高或低蜂鸣声提供诊断信息。一声高和一声低蜂鸣表明卡片已被识别，但配置失败。单声蜂鸣表明卡片仅被识别。两声高蜂鸣表明卡片已被识别并配置成功。

例如，如果您使用 Compact Flash 存储设备并在运行 Fedora 时将其插入笔记本，您应该会听到两声高蜂鸣。然后，您可以使用 `dmesg` 命令检查哪个设备被分配给该卡片：

```
$ dmesg
...
hde: SunDisk SDCF8-8, ATA DISK drive
hde2 at 0x100-0x107,0x10e on irq 3
ide-floppy driver 0.99.newide
hde: 15680 sectors (8 MB) w/1KiB Cache, CHS=245/2/32
hde: hde1
```

这里没有显示所有输出（您的可能看起来不同），但这个示例表明该卡片已被识别并配置为 `/dev/hde` 设备（包含一个分区 `/dev/hde1`）。然后您可以像使用任何其他存储介质一样使用该设备（有关使用硬盘的更多信息，请参阅第 58 章“管理文件系统”）。

其他设备也可以类似地被识别和配置。例如，如果您有一张以太网和调制解调器组合的 PCMCIA 卡并将其插入笔记本，您应该听到两组高蜂鸣（表示网络接口和调制解调器的识别和配置成功）。Linux 内核将报告接口和设备信息：

```
$ dmesg
...
eth0: NE2000 (DL10019 rev 05): 10BaseT, irq 3, hw_addr 00:E0:98:06:84:C5
ttyS04 at port 0x0af8 (irq = 3) is a 16450
```

在这里，网络接口被识别为 `eth0`（请参阅第 18 章“网络连接”，了解如何连接到网络）。调制解调器被配置为使用 `/dev/ttyS04`。

再次说明，PCMCIA 卡的问题排查可能很困难，特别是随着 802.11b/g 无线网卡在普及度和类型上的爆发式增长。此类故障排除可能需要下载、构建和安装新的驱动程序。

幸运的是，几乎所有串行、调制解调器和 Compact Flash 存储卡都能轻松识别和配置。许多以太网卡也得到支持。若要检查许多卡片的当前支持状态，请阅读 `SUPPORTED.CARDS` 文件。如果您安装了 `pcciacs` RPM 包，会在 `/usr/share/doc/kernel-pcciacs-3.X.XX/` 目录（其中 `X.XX` 是包的版本）下找到其副本。

## 注意

如果在配置和使用 PCMCIA 卡时遇到困难，请浏览 Linux PCMCIA 主页 http://kernel.org/pub/linux/utils/kernel/pcmcia/pcmcia.html/。点击“已知问题”链接，查看拥有相同卡片的其他用户是否遇到问题，或者该卡片是否未获得完全支持。如果有新版本的 PCMCIA 内核驱动程序可用，并且您卡片的驱动程序已更改（或已开发出新驱动程序），请下载并安装较新的软件。有关安装新 PCMCIA 模块的信息，请参阅第 39 章，或遵循随 PCMCIA 软件提供的说明。

## 控制 PCMCIA 服务

虽然在使用 Fedora 时可以插入或移除 PCMCIA 卡，但在使用这些卡片时请小心。例如，不要在连接到远程计算机时移除网络卡。不要在卡片的文件系统挂载和使用中拔出 Compact Flash 卡或其他存储介质卡（如 IBM microdrive）——这样做可能会损坏介质的文件系统并导致数据丢失。

您可以从命令行控制 PCMCIA 设备，并在不物理移除和插入卡片的情况下插入和移除卡片。使用 `cardctl` 命令来控制笔记本或带有 PCMCIA 适配器的台式 PC 上一个或多个卡槽的 PCMCIA 服务。`cardctl` 命令用于获取和打印有关已插入卡片的信息，挂起或恢复卡片的电源，重置卡片，执行软件插入或移除，或根据特定的预定义方案（如使用办公室或家庭网络）配置卡片。命令格式为 `cardctl <command> <slot_number>`（例如 0 或 1）。

例如，如果您已插入 Compact Flash 卡，请在卸载其文件系统后使用 `cardctl` 命令及其 `eject` 选项，加上卡槽号来弹出卡片，方法如下：

```
# cardctl eject 0
```

这可以在运行笔记本时节省电力。当再次需要该卡片时，您可以随后像这样“插入”卡片：

```
# cardctl insert 0
```

## 配置和使用 CD、DVD 及 CD-RW 驱动器

Linux 支持使用各种 CD 和 DVD 设备及介质。本节介绍如何确定分配给 CD 驱动器的设备以及获取额外的驱动器信息（如果驱动器支持在光介质上录制）。

AT Attachment Packet Interface，即 ATAPI，基于 IDE 的 CD 驱动器在安装期间被识别，并通过 `ide-cd` 内核模块工作。将创建一个名为 `/dev/cdrom` 的符号链接，指向您的 CD 设备（可能是 `/dev/hdb` 或
