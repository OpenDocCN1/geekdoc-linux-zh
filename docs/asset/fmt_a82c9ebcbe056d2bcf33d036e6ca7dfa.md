
在构建和安装之后，几个命令和文件会被复制到你的文件系统中。然后你需要启用 IR 并确定端口大小。一些笔记本提供特殊的 `Fn` 键组合来开启 IR，而在其他笔记本上你必须更改 BIOS 设置。不同操作系统之间端口的 IRQ 设置也可能不同。例如，在 Sony Vaio 505TR 上，IR 端口在 Windows 下分配给 COM4，IRQ10。

然而，在启用端口并启动 Linux 后，`dmesg` 命令会报告三个串行端口：

```text
ttyS0 at 0x03f8 (irq 4)
ttyS1 at 0x02f8 (irq 3)
ttyS2 at 0x03e8 (irq 4)
```

如果你熟悉你笔记本的硬件，你应该能识别出新的串行端口（在此例中为 `/dev/ttyS2`）。为了在 Linux 下设置 `/dev/ttyS2`，使用 `setserial` 命令来修复明显的 IRQ 冲突（在 `ttyS0` 和 `ttyS2` 之间），将 IRQ10 分配给该端口：

```bash
# setserial /dev/ttyS2 irq 10
```

这一命令行，以及为系统加载 IrDA 支持所需的命令，可以放在一个简短的 Shell 脚本中：

```bash
setserial /dev/ttyS2 irq 10
insmod irda
insmod ir
irattach /dev/ttyS2
irmanager -d 1
```

保存脚本，使用诸如 `IR` 这样的名称，然后使用 `chmod` 命令使其可执行：

```bash
# chmod +x IR
```

下一步是编辑你的 Red Hat 或 Mandrake `/etc/conf.modules` 文件并插入以下内容：

```text
alias tty-ldisc-11 irtty
alias char-major-161 ircomm-tty
```

这些行提供内核模块的信息，以便从 Shell 脚本中加载。请注意，到你阅读此内容时，这些条目可能已更改。（参见包含在 `irda-utils` 软件中的各个 README 文件。）

### 打印机示例

然后你应该将 IrDA 设备（如打印机）放置在你的笔记本范围内。接下来，使用你的 Shell 脚本启动 IrDA：

```bash
# ./IR
```

打开打印机，并查看 `/proc/misc`：

```bash
$ cat /proc/misc
62 ir1pt0
63 irda
...
```

这显示了 `mkmod` 命令所需的信息，该命令用于创建 IrDA 打印机设备 `/dev/ir1pt0`：

```bash
$ mkmod /dev/ir1pt0 c 10 62
```

然后你可以查看文件 `/proc/net/irda/discovery` 的内容，以查看是否在该范围内找到了打印机：

```bash
$ cat /proc/net/irda/discovery

IrLMP: Discovery log:

Link saddr=0x0000c404

Link saddr=0x0000c3ed
    name: BJ C-50, hint: Printer IrCOMM, daddr: 0xcab8000
```

下一步是使用 Red Hat 的 `printtool` 创建一个打印机，配置打印机条目以匹配打印机（在此例中为 Canon BJC-50），保存配置，然后编辑系统打印机能力数据库 `/etc/printcap` 中生成的条目。将此：

```text
:IRprinter=/dev/ir1:
```

改为：

```text
:IRprinter=/dev/ir1pt0:
```

然后你可以用此命令打印文档：

```bash
$ lpr -PRprinter myfile.txt
```

#### Canon BJC-80 用户

Dave Davey 撰写的关于使用 Canon BJC-80 进行 IR 打印的一小页信息可在 <http://www.physiol.usyd.edu.au/daved/linux/bjc-80.html#startup> 获取。

许多 IrDA 设备在 Linux 下得到支持，如移动电话、打印机以及用于台式机的插件 Dongle。

### 通用串行总线

通用串行总线 `USB` 最初由 IBM、Intel、Compaq、NEC 和 Northern Telecom 等多家大型计算机制造商于 1995 年开发为标准。其设计旨在推广低成本、低功耗且高速外围设备的使用，`USB` 支持 12Mbps 的传输速率，并声称允许最多 127 个设备通过 `USB` 集线器进行级联或支持。电缆长度通常限制在 5 米以内，且建议使用较短的电缆以避免电压降。

自 1997 年以来制造的大多数笔记本电脑（以及许多台式机）都支持 `USB`，通过提供一个小端口来连接集线器或其他 `USB` 外围设备，如键盘、鼠标、CD-ROM 驱动器、调制解调器、打印机、扫描仪或数字相机。使用 `USB` 的好处之一据称是减少昂贵的总线连接器和插卡；另一个好处是消除系统资源冲突（如 IRQ）。`USB` 设备还据称支持热插拔，类似于 PCMCIA 卡，并且许多设备提供直通连接器以允许多个设备级联（尽管大多数 `USB` 用户可能更倾向于使用自供电集线器来支持多个设备以获得最佳性能）。

Linux 对 `USB` 的支持首次出现在 Linux 内核的 2.3 开发系列中，尽管针对使用可加载模块和启动/停止脚本的后续 2.2 内核，源代码树中已有补丁可用。最初支持的设备包括各种键盘和鼠标。随着 Linux 内核 2.4 系列的出现，原生 `USB` 支持将成为现实。表 2.8 列出了当前在 Linux 上正常工作的若干设备。

要了解如何使用 `USB`、`USB` 的状态或如何在较旧的 Linux 内核上使 `USB` 工作，请访问 [http://www.linux-usb.org/](http://www.linux-usb.org/)。

有关 `USB` 的制造商和协议信息可在 [http://www.usb.org/](http://www.usb.org/) 找到。

### IEEE 1394 (FireWire)

最新的高速数据传输协议之一是 IEEE 1394，也称为 *FireWire*。由 Apple Computer 首先倡导，FireWire 比 `USB` 快得多，速度高达 400Mbps。作为小型计算机系统接口 `SCSI` 的替代方案，FireWire 也被吹捧为传输数字视频的理想方式，或者用于启用局域网 `LAN` 连接。

#### 表 2.9 Linux 下的 USB 设备

| 制造商 | 设备 |
|---|---|
| Apple | iMac 键盘 |
| Belkin | 键盘 |
| Cherry | MY3000 USB 4A CYA |
| Dallas Semiconductor | 扬声器 |
| Epson | Stylus Color 740 打印机 |
| Gravix | Gamepad Pro USB，型号 #4211 |
| HP | DeskJet 970Cse 打印机 |
| HP | Photosmart P1100 打印机 |
| HP | ScanJet 4100C 扫描仪 |
| HP | ScanJet 5200 扫描仪 |
| HP | ScanJet 6300C |
| Kensington | Orbit USB/PS2 鼠标 |
| Kodak | DC-240, 260, 265, 280, 290 相机 |
| Logitech | Wingman Gaming, N48, M-BA47, 鼠标 |
| Micro Innovations | LYNX 96 USB 鼠标 |
| Microsoft | Natural Keyboard Elite |
| Zoom | 2986L 调制解调器 |
| Zoom Telephonics | ZoomCam USB 网络摄像头 |

索尼等制造商的几种笔记本电脑型号在 1999 年上市时配备了 FireWire 端口。典型用途是传输高带宽数据，如数字视频。不幸的是，在编写本章时，Linux 尚无 FireWire 支持（除了几款数字视频相机、少数 PCI 适配器和几个外部硬盘外，市场上几乎没有 FireWire 设备）。

Linux 下（目前）尚不稳定的 FireWire 支持。您可以查看由 Emanuel Pirkler 主持的 GNU/Linux IEEE 1394 开发项目，位于 [http://ec1.ipt.uni-klu.ac.at/ieee1394/index.html](http://ec1.ipt.uni-klu.ac.at/ieee1394/index.html)。

虽然有一些初始驱动程序可用，但在编写本章时，文档很少，且只有一两个测试工具可用。您可以从 [http://www.firewire.org](http://www.firewire.org) 获取有关 FireWire 的更详细信息。

### 您的笔记本电池
