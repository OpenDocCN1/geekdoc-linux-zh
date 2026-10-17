
指定 IRQ 值为 0 告诉驱动程序不支持硬件接口（如某些 PAS 卡所示）。如果您的卡支持接口，应该使用它们，因为这可以降低驱动程序的 CPU 占用。
如果使用 Pro Audio Spectrum 卡，`is.pas_card` 应输入为 `'PAS'`，否则完全不需要指定。

## 6.3 Sony 的 CDU-535 接口 (`sonycd535=`)

此 CD-ROM 接口的语法为：

```
sonycd535=iobase,[irq]
```

如果希望指定 IRQ 0，可以使用零作为 I/O 基的“占位符”。

## 6.4 GoldStar 接口 (`gscd=`)

此 CD-ROM 接口的语法为：

```
gscd=iobase
```

## 6.5 ISP16 接口 (`isp16=`)

此 CD-ROM 接口的语法为：

```
isp16=[port[,irq,dma]][,,],drive_type]
```

对 `irq` 或 `dma` 使用 0 表示不使用它们。`drive.type` 的允许值为 `noisp16`、`Sanyo`、`Panasonic`、`Sony` 和 `Mitsumi`。使用 `noisp16` 会禁用整个驱动器。

## 6.6 Mitsumi 标准接口 (`mcd=`)

此 CD-ROM 接口的语法为：

```
mcd=iobase,[irq[,wait_value]]
```

`wait_value` 用于驱动器出现问题的用户作为内部超时，并可能取决于编译时的 DEFINE 而不实现。

## 6.7 Mitsumi XA/MultiSession 接口 (`mcdx-`)

目前，此“实验性”驱动有一个设置函数，但尚未实现任何参数（截至 1.3.15 版本）。这与上述硬件相同，但驱动程序具有扩展功能。

## 6.8 Optics Storage 接口 (`optcd-`)

此类卡的语法为：

```
optcd=iobase
```

## 6.9 Phillips 的 CM206 接口 (`cm206-`)

此类卡的语法为：

```
cm206=[iobase],[irq]
```

驱动程序假设 3 到 11 之间的数字为 IRQ 值，0x300 到 0x370 之间的数字为 I/O 端口，因此您可以按任何顺序指定一个或多个数字。它还接受 `scm206=auto` 来启用自动探测。

## 6.10 Sanyo 接口 (`sjcd-`)

此类卡的语法为：

```
sjcd=iobase,[irq,dma_channel]
```

## 6.11 SoundBlaster Pro 接口 (`sbpcd-`)

此类卡的语法为：

```
sbpcd=iobase,type
```

其中 `type` 为以下值之一（区分大小写）：`'SoundBlaster'`、`LaserMate'` 或 `'SPEA'`。I/O 基是 CD-ROM 接口的，而不是卡下部分的基地址。

## 7 其他硬件设备

任何不符合上述任何类别的设备都归类在此。

## 7.1 以太网设备 (`ether-`)

不同的驱动程序使用不同的参数，但它们至少共同具有 IRQ、I/O 端口基值和一个名称。在最通用的形式下，它如下：

```
ether=irq,iobase[param_1[,param_2,...,param_8]],name
```

第一个非数字参数被视为名称。`param.n` 值（如果适用）通常对每个卡/驱动程序具有不同的含义。典型的 `param.n` 值用于指定如共享内存地址、接口选择、DMA 通道和链路。

该参数最常用的用法是强制对第二个以太网进行探测，因为默认只探测一个。

```
ether=0,0,eth1
```

注意，上述示例中 IRQ 和 I/O 基的零值告诉驱动程序进行自动探测。注意，《Ethernet-How》关于使用多个卡以及特定卡/驱动程序对 `param.n` 值的实现有完整且详细的文档。感兴趣的读者应参考该文档中关于特定卡的章节以获取更多信息。

## 7.2 软磁盘驱动程序 (`floppy=`)

有很多软磁盘驱动程序选项，它们都列在 `linux/drivers/block` 的 `README.fd` 中。此信息直接取自该文件。

```
floppy=mask,allowed,drive_mask
```

将允许的驱动器位掩码设置为 `mask`。默认情况下，每个软磁盘控制器只允许 0 和 1 单元。这样做是因为非标准硬件（ASUS PCI 主板）在访问单元 2 或 3 时会映射键盘。该选项与 CMOS 选项相比已有些过时。

```
floppy=all,drives
```

将允许的驱动器位掩码设置为 `all`。如果一个软磁盘控制器连接了两个驱动器，请使用此项。

```
floppy=asus.pci
```

将位掩码设置为仅允许 0 和 1 单元（默认）。

```
floppy=daring
```

告诉软磁盘驱动程序你有一个良好的软磁盘控制器。这允许更高效、更流畅的运行，但在某些控制器上可能会失败。

## 8. 结语

一个正确的启动参数示例（同时包含标识符形式和整数形式）：

```
digi=E,PC/XI,D,16,200,D0000

digi=1,0,0,16,512,851968
```

请注意，在没有 `digi=` 启动参数的情况下，驱动程序启用 0x200 的 I/O 和 0xD0000 的共享内存基础。不会进行自动配置（autoprofig）。更多细节请参见 `linux/documentation/digiboot.txt` 文件。

## 7.11 RisCom/8 多端口串口驱动 (`riscom8=`)

通过为每个安装的板卡提供四个唯一的 I/O 端口值，最多支持四块板卡。更多细节请参见 `linux/Documentation/riscom8.txt` 文件。

## 7.12 Baycom 串口/并行无线解调器 (`baycom=`)

这些设备的启动参数格式为：

```
baycom-modem,io,irq,options[,modem,io,irq,options]
```
