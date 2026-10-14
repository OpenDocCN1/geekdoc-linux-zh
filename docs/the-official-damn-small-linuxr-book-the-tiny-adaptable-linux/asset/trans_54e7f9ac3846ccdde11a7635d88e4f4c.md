

laptop 将运行 Damn Small Linux！接下来，我以 root 身份打开了一个终端窗口（右键单击 ATerminal 图标并选择 Aterm as Super User）。然后，我运行了 dmesg 命令以查看来自内核的启动消息。以下是一个示例：

```
# dmesg | less
<5>0MB HIGHMEM available.
<5>32MB LOWMEM available.
<4>Detected 167.049 MHz processor.
<6>Memory: 28652k/32768k available (1371k kernel code, 3728k reserved, 561k data, 140k init, 0k highmem)
<6>Floppy drive(s): fd0 is 1.44M
<4>hdc: TOSHIBA CD-ROM XM-1602B, ATAPI CD/DVD-ROM drive
<4>hda: attached ide-disk driver.
<6>hda: 4233600 sectors (2168 MB) w/96KiB Cache, CHS=525/128/63
<6>PCI: Found IRQ 11 for device 00:01.2
<6>usb-uhci.c: USB UHCI at I/O 0xfc0, IRQ 11
<4>usb-uhci.c: Detected 2 ports
<6>Yenta ISA IRQ mask 0x0498, PCI irq 5
<6>ttyS0 at 0x03f8 (irq = 4) is a 16550A
<6>parport0: PC-style at 0x378 [PCSPP,TRISTATE,EPP]
<6>parport0: irq 7 detected
```

上面显示的输出经过编辑后，告诉你一些你可以在笔记本上看到的东西和一些你看不到的东西。这台笔记本有 32MB 的 RAM 和一个 167.049MHz 的处理器（两者都较低，但对于我们的目的来说是可用的）。

该机器有一个软盘驱动器和 CD-ROM 驱动器（如果你正在查看机器，你已经可以看到），以及一个硬盘。硬盘大约有 2GB 的空间（2168MB）。笔记本上其他可用的端口包括两个 USB 端口、一个 CardBus 插槽（Yenta）、一个 COM1 端口（ttyS0）和一个并行端口（parport0）。接下来，我快速检查了处理器类型：

```
# cat /proc/cpuinfo
vendor_id  : GenuineIntel
cpu family : 5
model name : Pentium MMX
cpu MHz    : 167.049
```

到目前为止，看起来这台笔记本可以用于该项目。

## 使用 Tom’s Root Boot 评估笔记本

我需要尝试的第二台笔记本是 Texas Instruments TravelMate 4000E 486 WinDX2/50 MHz 笔记本。由于它没有 CD-ROM 驱动器，我启动了 Tom’s Root Boot 软盘并以 root 用户身份登录（xxxx 是密码）。由于只有一个 shell 界面，我可以立即输入 dmesg 来检查硬件：

```
# dmesg | less
Memory: 5836k/8192k available (1560k kernel code, 416k reserved, 288k data, 92k init)
CPU: 486
parport0: PC-style at 0x378, irq 7 [SPP]
ttyS0 at 0x03f8 (irq = 4) is a 16450
ttyS1 at 0x02f8 (irq = 3) is a 16550A
hda: ST9235AG, 200MB w/32kB Cache, CHS=985/13/32
Floppy drive(s): fd0 is 1.44M
Partition check
    hda: hda1
```

从输出中，你可以看到这台 486DX 机器上有 8MB 的 RAM。它有一个软盘驱动器（fd0）、并行端口（parport0）和两个串行端口（ttyS0 和 ttyS1）。它有一个 200MB 的硬盘，这在笔记本制造时可能相当大。IDE 硬盘上有一个分区（hda1）。

RAM 数量低立即使这台机器被淘汰（只有 8MB）。然而，如果它至少有 16MB 的 RAM，你可以尝试一下。你将面临的一些困难包括：从一堆软盘安装 DSL、为网络接口配置 PLIP，以及内容受限的磁盘空间。如果你愿意接受挑战的话，其他人已经在类似系统上运行过 DSL（请参阅 www.damnsmalllinux.org/486.html）。

本章的其余部分重新使用我刚刚描述的 Compaq Presario 1620 来创建一个数字媒体相框。

## 获取所需的零件

在评估完你的笔记本后，你需要考虑还需要为其添加什么。第一组零件是你需要让笔记本实现你想要的功能的零件。第二组零件是框架以及将笔记本安装到其中的零件。

### 为笔记本添加零件

你需要为笔记本添加哪些零件取决于你的笔记本缺少哪些零件以及你如何向笔记本添加内容。在我的例子中，以及其他拥有不到 100 美元笔记本的情况下，你可能缺少网络接口所需的硬件。

因为我使用的笔记本同时具有 USB 端口和 CardBus 插槽，所以我可以选择如何添加网络接口。再次翻找我的东西，我发现

