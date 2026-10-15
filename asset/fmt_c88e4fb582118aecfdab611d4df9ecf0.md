
- 7. 通用桌面箱 (UDB，有时称为 Multia)。这只是一个无名板，处理方式与本文其他部分相同。
- 8. AlphaStation 200, 250, 255, 400 (Avanti 机器)
- 9. EB164 (Aspen Avalanche, Timberline. Summit; Microway Screamer)
- 10. Kinetics 的 Platform 2000 机器
- 11. PC164 机器 (Durango)
- 12. Alcor 类型机器 (AlphaStation 500. 600: Maverick. Brett)
- 13. Alpha-XL
- 14. Alpha-XLT (XL 300, XL 366)
- 15. Mikasa 类型机器 (AlphaServer 1000)。1000A 不支持

除了 Jensen 之外的所有平台都包含一个 NCR 810 SCSI 控制器，尽管支持 BusLogic PCI SCSI 控制器（FlashPoint 除外）、Adaptec AHA2940 SCSI 控制器以及 Qlogic 1020 ISP 控制器。Jensen 设计使用 AHA1740 SCSI 控制器并支持。

支持 NE2000、DE422 和 DE4x5 (PCI) 以太网。这包括 UDB 的内部以太网硬件。内核也包含令牌环（Token ring）支持。

X Window 系统可以在除 Jensen 机器外的任何带有基于 S3 显卡的机器运行。`ftp://azartarn.com` 的 `/pub/linux/axp/jensen` 提供了适用于 S3 卡的服务器。TGA 服务器（例如 UDB）可以在你的 Red Hat Linux/Alpha CD 的 X11 目录中找到。来自 Orchid 和 Number 9 的大多数显卡都能工作。大多数 Diamond Stealth 卡也被支持。Digital TGA 显（基于 DC21030 芯片）在 8 位模式下受支持，并且还为 Mach64 卡提供了 X 服务器。

关于 Alpha 硬件的更多信息请见附录 C。

## 3.3. 安装 MINILOADER MILO

启动 Red Hat Linux/Alpha 最简单的方法是通过 Linux Miniloader（即 MILO）。你可以直接从系统固件加载 MILO，或者使用 ARC 控制台将 MILO 作为备用操作系统加载。这些过程的详细信息请参阅 MILO FAQ，该文件作为附录 D 提供。

完整的 MILO 树可以在 CD 的 `milo` 目录中找到。它包含了此 CD 制造时的最新文档和 MILO 镜像。然而，后续版本的 MILO 定期在 `gatekeeper.dev.com` 发布。`images/arc` 目录还包含软磁盘镜像，可用于 ARC 控制台直接启动到 MILO。这些镜像包含 MILO 和 `linload.exe`，以及一个可刷写的 MILO 版本以及用于支持刷写 MILO 平台的闪存管理工具（flash management utility）。如果你在使用 MILO 时遇到问题，首先应尝试使用新版本的 MILO。

如果你的机器不支持 MILO，你需要从 SRM 控制台直接启动软盘或 CD。有关如何操作的信息可以在 Red Hat 软件网站获取：`http://www.redhat.com/linux-info/alpha/faq`。

## 3.4 安装 Red Hat Linux/Alpha

### 3.4.1 制作启动盘

安装 Red Hat Linux/Alpha 的第一步是创建启动盘；使用哪种启动盘取决于你的拥硬件。Red Hat Linux/Alpha CD 的 `images` 目录下提供了多种启动盘镜像，以及一个包含有关可用镜像更多信息的 README 文件。

可用的启动镜像包括：
- 1. `cab.img` (AlphaPC64, Cabriolet)
- 2. `noname.img` (AxPPC33, Noname, Universal Desktop Box)
- 3. `eb64p.img` (EB64+, Aspen Timberlines)
- 4. `eb66.img` (EB66)
- 5. `eb66p.img` (EB66+)
- 6. `jensen.img` (Jensens)
- 7. `avanti.img` (AlphaStation 200, 250, 400)
- 8. `xl.img` (Alpha XL)
- 9. `xlt.img` (Alpha XTL)
- 10. `eb164.img` (EB164 基于机器)
- 11. `p2000.img` (Platform 2000)
- 12. `pc164.img` (Alcor 基于机器)
- 13. `alcor.img` (Alcor 基于机器)
- 14. `mikasa.img` (Mikasa 基于机器)

所有这些镜像都可以在带有 VGA 或 TGA 显卡的机器上工作。要从这些镜像制作软盘，请在 MS-DOS 或 MS-Windows 下使用 `write.exe`（位于 `dosutils` 目录）或在 Linux 或 Unix 下使用 `dd`。

### 3.4.2 开始安装

安装 Red Hat Linux/Alpha 需要使用内存磁盘（ramdisk）。Red Hat Linux/Alpha CD 的 `images` 目录下提供了几个内存磁盘镜像。要开始安装，将你的启动盘插入机器。

```
在 MS-DOS 下，你会输入：
```

```
sda2:root=/sda2
```

### 3.4.3 完成安装

Linux/Alpha 系统已完全配置。安装完成后，将重启计算机。

## 3.5 启动你的 RED HAT LINUX 系统

要从 MILO 启动 Red Hat Linux，必须使用以下参数：
- 标准 fdisk 样式：与 Intel 的方式一样。
- BSD 样式：除非绝对必要，否则我们不建议使用。

例如，如果根分区是第二个分区，你应该使用：

```
sda2:root=/sda2
```

如果你的根分区是第三个分区，你应该使用：

```
hdb3:root=/hdb3
```
