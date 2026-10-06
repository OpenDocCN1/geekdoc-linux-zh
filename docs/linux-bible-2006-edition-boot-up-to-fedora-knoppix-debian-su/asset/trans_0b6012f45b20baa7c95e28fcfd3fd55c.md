

# 启动 KNOOPPIX

如果你面前有一台符合要求的 PC，可以按照以下步骤开始：

- 1.  将你的 KNOOPPIX DVD 或 CD 插入相应的驱动器。
 2.  重启电脑。几片刻之后，你将看到启动界面。
    虽然《Linux 圣经》DVD 和普通 KNOOPPIX CD 的启动界面看起来有所不同，但你可以以相同的方式继续启动过程。
 3.  按下回车键（Enter）。如果一切顺利，你应该能看到 KNOOPPIX 桌面，然后可以进入“使用 KNOOPPIX”章节。如果 KNOOPPIX 没有正常启动，或者你想在启动之前对其进行进一步调整，请继续阅读下一节。

# 解决启动问题

通过理解整个启动过程，在大多数情况下，你将能够克服安装 KNOOPPIX 时可能遇到的任何问题。以下是你应该了解的一些：

- **启动顺序**—— 你的电脑 BIOS 有一个查找启动操作系统的特定顺序。典型的顺序是软盘、CD 或 DVD 以及硬盘。如果你的电脑跳过了 KNOOPPIX 启动盘并直接从硬盘启动，请确保 BIOS 中的启动顺序已设置为 CD 或 DVD。要更改 BIOS，请重启电脑并在硬件首次启动时按照指示（快速）进入 Setup 设置（通常是按下 F1、F2 或 DEL 键）。寻找选择启动顺序的选项，使你的 CD 或 DVD 在硬盘之前启动。
- **制作软盘**——如果你的电脑仍然无法从 CD 或 DVD 启动，你可以在运行的 KNOOPPIX 系统中创建两张软盘，运行 KNOOPPIX 磁盘上的 `mkbootfloppy` 命令（它会自动格式化软盘镜像并在需要插入软盘时通知你）。要为其他操作系统创建软盘，请参阅 KNOOPPIX 维（www.knoppix.net/wiki/MainPage）。
- **添加启动选项**——与其让启动过程自动检测并配置你硬件的一切，不如你可以在启动提示符中添加选项，这将覆盖你的 KNOOPPIX 自动配置日期。在启动提示符处按 F2 可查看额外的启动选项。

可以使用一些启动选项，可以帮助你克服启动时各种不同的问题。KNOOPPIX 将这些选项称为“作弊代码”（cheat codes）。要查看更完整的列表，请参阅文件 `knoppix-cheatcodes.txt`，当你在任何操作系统上挂载本书随附的 CD 或 DVD 时，可以在 KNOPPIX 目录中找到它。

许多选项可以用于不同的 Linux 系统。如果你在安装或启动不同的 Linux 发行版时遇到困难，可以尝试使用任何其他选项。你可能不会使用 "knoppix" 这个词，而是会使用不同的词来启动其他发行版的安装或启动过程（例如，对于红帽 Linux 系统使用“Linux”，或对于 Morphix Live-CD 使用“morphix”，取决于具体的发行版）。

当 KNOOPPIX 开始该过程时，你会看到屏幕，带有 `boot:` 提示符提供了可以帮助你按喜欢的方式运行 KNOOPPIX 的启动选项。表 11-1 显示了当你想要开启在启动时可能未开启的特定功能时应使用的选项。

### 表 11-1：选择选择的启动选项

| 选项 | 功能 |
| :--- | :--- |
| knoppix lang=?? | 选择特定的语言/键盘。将 ?? 替换为以下之一：cn, de, da, es, fr, it, nl, pl, ru, sk, tr, tw, uk, 或 us。 |
| knoppix desktop=?? | 代替 KDE 桌面 (kde)，将 ?? 替换为以下窗口管理器之一：fluxbox, cewm, larswm, wmaker, 或 xfce。 |
| knoppix blind | 启动 BrailleTerminal（不带 X ）。 |
| knoppix brittle=type,port,table | 添加用于盲文设备的参数。 |
| knoppix wheelmouse | 对于滚轮鼠标，启用 IMPS/2 协议。 |
| knoppix nowmouse | 对于普通的 PS/2 鼠标，使用 PS/2 协议。 |
| knoppix keyboard-us xkeyboard-us | 为文本（shell）和图形（X）分配不同的键盘驱动。 |
| knoppix dma | 为所有 IDE 驱动器开启 DMA 加速。 |
| knoppix alsa knoppix alsa-es1938 | 选择这两个符号中的任何来使用 ALSA 驱动（风险自担）。 |

如果有硬件被检测或配置不当，你可以让 KNOOPPIX 跳过该硬件。表 11-2 包含了跳过或关闭各种硬件功能的选项：

### 表 11-2：关闭硬件的启动选项

| 选项 | 结果 |
| :--- | :--- |
| knoppix atapic | IDE CD-ROM 不进行 SCSI 仿真。 |
| knoppix noagp | 不检测 AGP 显卡。 |
| knoppix noaptic | 禁用高级可编程中断控制器（可以解决 SMP 计算机上的某些问题）。 |
| knoppix acpi-off | 禁用高级配置和电源接口 (ACPI)。 |
| knoppix noapm | 无高级电源管理支持。（如果 acpi 正常，apm 默认将关闭。同一时间只能激活一个。） |
| knoppix noaudio | 无声音支持。 |
| knoppix nodhcp | 不要尝试自动启动你的网络连接。 |
| knoppix fstab | 不要通过 fstab 查找。 |
| knoppix firewire | 不检测火线。 |
| knoppix popcmia | 不检测 PCIA 插。 |
| knoppix nosci | 不检测交换区。 |
| knoppix nosusb | 不检测 USB 设备。 |
| knoppix pnpoff | 禁用即插即用 (PnP)。 |
| knoppix failsafe | 故障安全。 |

表 11-3 列出了在遇到视频问题时可以帮助你的启动问题选项。

### 表 11-3：修复视频问题的启动选项

| 选项 | 结果 |
| :--- | :--- |
| knoppix ddc | 无数据通道 (DDC)。 |
| knoppix screen=?? | 将 ?? 替换为以下之一：640 ×480, 800 ×600, 1024 ×768, 1280 ×1024，或其他支持的分辨率。 |
| knoppix vsga=?? | 将 ?? 替换为以下之一以驱动你的显卡。 |
| knoppix vrefresh=60 | 设置垂直刷新率为 60 Hz。 |
| knoppix hrefresh=80 | 设置水平刷新率为 80 Hz。 |
| knoppix xserver=?? | 将 ?? 替换为以下之一以启动 X 服务器：ati, fbdev, nv, radeon, s3。 |
| knoppix level=normal | 正常模式。 |
| knoppix mode=2 | 文本模式。 |
| knoppix mode=3 | 帧模式。 |
| knoppix mode=4 | 帧模式。 |
| knoppix mode=5 | 帧模式。 |
| knoppix mode=6 | 帧模式。 |
| knoppix mode=7 | 帧模式。 |
| knoppix mode=8 | 帧模式。 |
| knoppix mode=9 | 帧模式。 |
| knoppix mode=10 | 帧模式。 |
| knoppix mode=11 | 帧模式。 |
| knoppix mode=12 | 帧模式。 |
| knoppix mode=13 | 帧模式。 |
| knoppix fb | 使用帧缓冲模式。 |
| knoppix module=?? | 将 ?? 替换为驱动程序。 |

## 自定义 KNOOPPIX

有很多从硬盘或软磁盘自定义 KNOOPPIX 的选项。请参阅“你的 KNOOPPIX 配置”章节了解如何保存这些配置。

## KNOOPPIX 的特殊功能和绕过方法

其他启动选项在之前提到的 `knoppix-cheatcodes.txt` 文件中描述。这些选项在 KNOOPPIX 启动时可以做的事情包括更改启动屏幕等。

# 第三部分 选择和安装 Linux 发行版

### 测试 CD

如果你怀疑 KNOOPPIX CD 是坏的，建议你在启动提示符处运行：

```
knoppix testcd
```
如果此时仍然无法启动 KNOOPPIX，可能是你的硬件不支持或某些损坏。要进一步解决该问题，请查看 knnoppix 论坛。

### 从 RAM 运行 KNOOPPIX

为了提高性能，KNOOPPIX 提供了一种从内存中运行 KNOOPPIX 的方法（前提你有内存），或者将其安装到硬盘上运行。如果你有超过1GB 的内存，可以通过输入以下命令完全从内存 运行 KNOOPPIX（这样你可以移除 KNOOPPIX DVD 和 CD）：

```
knoppix toram
```

### 将 KNOOPPIX 安装到硬盘

如果你的硬盘是 FAT 或 EXT2 文件系统类型且包含至少800MB的空间，你可以完全从硬盘运行 KNOOPPIX。要这样做，你必须知道要安装的硬盘分区名称。例如，对于第一个硬盘上的第一个分区，你应该使用 /dev/hda。在这种情况下，将 KNOOPPIX 复制到该分区，你需要在启动提示符处输入：

```
knoppix tohd=/dev/hda
```
你可以看到 KNOOPPIX 被复制到硬盘分区并自动从那里启动。下次你想启动 KNOOPPIX 时，可以通过插入 KNOOPPIX 介质并输入以下命令从硬盘启动：

```
knoppix fromhd=/dev/hda
```
从硬盘运行时，你可以安全地弹出 CD 或 DVD 并将驱动器用于其他事情（输入 `eject /dev/cdrom`）。

# 使用 KNOOPPIX

与其介绍许多 Linux 系统通用的 KNOOPPIX 功能（KDE工具、文字处理器等），我将带你快速浏览 KNOOPPIX 的特殊功能。如果你的电脑正常启动了 KNOOPPIX，你应该看到一个与图 11-1 所示类似的屏幕。

