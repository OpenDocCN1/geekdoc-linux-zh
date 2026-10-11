
你必须确保工作站设置允许机器从 USB 启动，这通常需要重新配置 BIOS。首先，重启工作站并按键进入 BIOS 配置（`F12` 或 `DEL`，有时是 `F1` 或 `F2`）。选择 `Boot` 菜单并启用“优先启动 USB 设备”（`Boot USB Devices First`）或类似的设置。在某些计算机中，U 盘被隐藏在启动 BIOS 的硬盘部分。在这种情况下，你需要选择 `Boot+Hard Drives`，将主驱动器更改为存储介质，然后确保在启动设备下选选择了 USB 驱动器。如果“从 USB 启动”是启用/禁用选项，请选择它，然后进入启动设备顺序并将 USB 选项移动到硬盘选项之上。保存更改并退出 BIOS 配置。此时，工作站将继续重启——*注意：* 如果你看到单行条 **Boot Error** 且没有其他反应，请根据制造商说明更新系统 BIOS。

## 日常使用新驱动器

当你的系统启动时，Fedora 环境的加载速度会比 Live CD 快得多。如图 3-3 所示，U 盘显示了新创建的文件夹，并且可以像常一样访问其他设备。“安装到硬盘”（`Install to Hard Drive`）图标保留在桌面上，如果你决定这样做，可以将其永久转换为 Fedora。

使用该操作系统不需要互联网连接，但强烈建议连接，因为大多数用户会想要下载额外的程序，以进一步测试操作系统的功能。

![](img/7605650e62fab537998f2b973dbf5a26_69_0.png)

图 3-3：在 USB 环境中工作。

## 第4 章：Linux 的故障排除与配置

本章内容

- 排除安装故障
- 配置 X Window 系统
- 解决安装问题
- 设置打印机
- 管理 DVD 和 CD-ROM
- 安装额外的软件包

在安装 Linux 的过程中，安装程序会尝试检测关键硬件组件，例如 SCSI 控制器和网卡。根据检测到的结果，安装程序将引导你完成一系列安装步骤。例如，如果安装程序检测不到网卡，它将跳过网络配置步骤。如果你实际上没有网卡，这是可以的；如果你有网卡而安装程序误认为你没有，那么你就遇到了安装问题。

另一种安装问题发生在重启 PC 后，显示的不是图形登录界面，而是文本终端。此错误意味着 X Window 系统配置出现问题。

此外，Linux 安装通常不包含你 PC 系统上每个硬件的配置程序。例如，大多数安装都会取消你的打印机的配置。在本章中，我将向你展示一些故障排除的方法。

## 46 使用文本模式

### 使用文本安装

大多数 Linux 安装程序都会尝试启动 GUI。如果安装程序失败，可以使用文本模式。

| 发行版 | 如何获取文本模式 |
| :--- | :--- |
| Debian | 运行文本模式。 |
| Fedora | 运行文本模式。 |
| Knoix | 运行文本模式。 |
| SUSE | 运行文本模式。 |
| Ubuntu | 运行文本模式。 |
| Xandros | 运行文本模式。 |

## 47 X 的故障排除

每当我安装 X 时，图形界面都不会出现。如果也遇到这种情况，这里是你可以进行配置的方法：

## 解决其他安装问题

7. 按下 `Ctrl+Alt+Delete` 或输入 `reboot` 重启电脑。

如果一切顺利，你应该会看到图形登录界面。

使用 X 服务的 `-configure` 选项创建的配置文件没有以最佳分辨率显示。要调整该配置文件，你需要在重启系统后运行一个实用程序来调整设置。你使用的实用程序取决于 Linux 发行版，但大多数发行版都包含一个让你通过图形化用户界面配置显卡、显示器和显示设置的实用程序。

## 解决其他安装问题

我确定我还没有列出所有潜伏在外的安装问题。没有人能做到。x86 PC 中存在如此多的组件，墨菲定律实际上要求必须存在某些安装程序无法处理的硬件组合。在本节中，我列出了几个已知问题。对于其他问题，我建议你去 Google Groups (`http://groups.google.com`) 并输入故障的一些症状。假设其他人也遇到了类似的问题，你可以获得有关如何排除故障解决你特定困境的指示。

## Knoppix 启动命令

Knoppix Live CD 可以作为一个很好的故障排除工具，因为 Knoppix 擅长检测硬件，并且可以直接从光盘运行。

如果你在启动 Knoppix 时遇到困难，尝试在 `boot:` 提示符输入 Knoppix 启动命令。例如，如果 Knoppix 在尝试检测 SCSI 卡时卡死，你可以在 `boot:` 提示符输入 `knoppix nosci` 来禁用 SCSI。或者，如果你使用 X 服务加载 `nv` 模块（基于 NVIDIA 芯片的显卡），你可以在 `boot:` 提示符输入 `knoppix xmodule=nv`。

表 4-2：一些常用的 Knoppix 启动命令。

| 启动命令 | 功能 |
| :--- | :--- |
| `expert` | 以专家模式启动，允许用户交互式地设置和配置 Knoppix。 |
| `failsafe` | 在不尝试检测硬件的情况下启动（启动 Linux 所需的最基本硬件外）。 |
| `fb1280x1024` | 在指定的分辨率下使用固定帧图形（指定你想要的分率，例如 1024 x 768 或 800 x 600）。 |
| `knoppix 1` | 在运行级别 1（单用户模式）启动 knoppix，你可以用它来执行救援操作。 |
| `knoppix 2` | 在级别 2 启动，提供文本模式 shell 提示符。 |
| `knoppix acpi=off` | 完全禁用 ACPI（高级配置和电源接口）。 |
| `knoppix atapicd` | 对于 IDE-CD 驱动器使用 ATAPI-CD ROM 接口而不是模拟 SCSI 接口。 |
| `knoppix desktop=wmname` | 使用指定的窗口管理器 own默认的 KDE desktop=wmname（wname 为 fluxbox, icewm, larswm, twm, wmaker, 或 xfce）。 |
| `knoppix dma` | 为所有 IDE 驱动器启用直接访问 (DMA)。 |
| `knoppix floppyconfig` | 从软盘运行 shell 脚本 `knoppix.sh`。（该 shell 脚本包含运行运行的 Linux 命令）。 |
| `knoppix fromhome=/dev/hdval` | 从之前复制到指定硬盘分区的 Live CD 镜像启动。 |
| `hsync=80` | 为 X 使用 80 kHz 的水平刷新率（你想要使用的水平刷新率）。 |
| `knoppix lang=xx` | 设置由双字母代码 xx 指定的语言，其中 cn = 简体中文，de = 德语，da = 丹语，es = 西班牙语，fr = 法语，it = 意大利语，nl = 荷兰语，pl = 俄语，sk = 斯洛伐克语，tr = 土耳语，tw = 繁体中文，或 us = 美国英语。 |
| `knoppix mem=256M` | 指定 PC 的内存（兆字节）。 |
| `knoppix myconf=/dev/hdval` | 从 `/dev/hdval` 分区运行 shell 脚本 `knoppix.sh`。 |
| `knoppix myconf=scan` | 让 knoppix 搜索文件 `knoppix.sh`，并执行其中的命令。 |
| `knoppix noeject` | 停止 knoppix 后不弹出 Live CD。 |
| `knoppix noprom` | 停止 knoppix 后不提示 Live CD。 |
| `knoppix nowheel` | 为 PS/2 鼠标或触摸板强制使用 PS/2 协议（而不是自动检测鼠标）。 |
| `knoppix noxxx` | 让 knoppix 跳过硬件检测的特定部分（xxx 指定 apic = 高可编程中断控制器，agp = 加速图形电源管理，audio = 声卡，ddc = 动态主机配置，fstab = 文件系统总线，firewire = IEEE 1394 高速串行总线，pcmcia = 电脑接口，swap = 虚拟内存空间，usb = 通用串行总线）。 |
| `pc=bios` | 使用 BIOS 处理的 PCI 控制器。 |
| `pnpbios=off` | 跳过即插用 (PnP) BIOS 初始化。 |
| `knoppix screen=resolution` | 设置屏幕分辨率（resolution 为你需要的像素，例如 1024x768、800x600、640x480 等）。 |
| `knoppix testcd` | 使用 MD5 检查 Live CD 的数据完整性。 |
| `knoppix tohd=/dev/sda` | 将 Live CD 复制到指定的硬盘分区并从那里运行（需要 1GB RAM）。 |
| `knoppix toram` | 将 Live CD 复制到 RAM（内存）并从那里运行（需要 1GB RAM）。 |
| `knoppix vga=ext` | 使用 50 行文本模式显示。 |
| `knoppix vsync=60` | 为 X 使用 60 Hz 的垂直刷新率（你希望 X 使用的垂直刷新率）。 |
