
这里，token 可以是 error、scan、mlqueue、mlcomplete、llqueue、llcomplete、hlqueue 或 hlcomplete。level 控制日志的详细程度，可以是任意正数，包括 0。

其余 SCSI 部分的问题特定于 SCSI 主机适配器。你应仅为已安装的适配器选择支持。

## Firewire 和 I2O 支持

如果您有 Firewire 或 I2O 设备，应为它们选择支持选项。

![](img/9eb7e89292d2f85707b4d49102c865b7_286_0.png)

> 这两种类型的设备均使用实验性驱动程序支持，因此目前还不是非常可靠。

## 网络设备支持

在本节中，您配置各种网络设备功能。

```
Network device support (CONFIG_NETDEVICES) [Y/n/?]
```

如果您想要网络设备，必须对前一个问题回答 yes。

```
ARCnet support (CONFIG_ARCNET) [N/y/m/?]
```

除非您有 ARCnet 网络接口卡，否则默认设置即可。

```
Dummy net driver support (CONFIG_DUMMY) [M/n/y/?] ?
```

接下来您将被询问有关网络卡的问题。根据网络卡厂商，您需要为该卡选择支持。如果找不到与卡相关的查询，很可能是您使用的是通用卡，默认设置即可正常工作。例如，如果您有一张无品牌名称的 PCI NE2000 兼容卡，可以在被问及以下问题时启用其支持：

```
PCI NE2000 support (CONFIG_NE2K_PCI) [N/y/m/?]
```

仅在您确定拥有 PCI 卡但不是品牌卡（可能具有专有且不受支持的模块）时才选择上述选项。

```
Wireless LAN (non-hamradio) (CONFIG_NET_RADIO) [N/y/?]
```

如果您有无线局域网，则在此选择 yes 以启用其支持。请注意，大多数无线接入点（WAP）具有可连接到系统的常规以太网接口，因此在这种情况下您不需要无线局域网支持。

```
Token Ring driver support (CONFIG_TR) [N/y/?]
```

如果您使用令牌环网络，则在此启用其支持；否则，选择默认答案。

```
Fibre Channel driver support (CONFIG_NET_FC) [N/y/?]
```

如果您有光纤通道设备，则需要启用此支持；否则，选择默认答案。

```
Red Creek Hardware VPN (EXPERIMENTAL) (CONFIG_RCPCI) [N/y/m/?]
```

如果您没有 Red Creek 硬件，选择默认答案。

```
Traffic Shaper (EXPERIMENTAL) (CONFIG_SHAPER) [N/y/m/?]
```

如果您希望控制传出网络流量，则通过选择 yes 启用此实验性支持。

```
Wan interfaces support (CONFIG_WAN) [N/y/?]
```

如果您有广域网卡，通过选择 yes 启用 WAN 支持；否则，选择默认答案。

```
PCMCIA network device support (CONFIG_NET_PCMCIA) [Y/n/?]
```

如果您有 PCMCIA 网络卡，通过选择 yes 启用 PCMCIA 网络设备支持；否则，选择默认答案。

## 业余无线电、IrDA、ISDN 和旧 CD-ROM 支持

我假设您不会使用业余无线电、IrDA（红外）、ISDN 或旧 CD-ROM 支持；因此，以下问题的默认答案已足够：

```
Amateur Radio support (CONFIG_HAMRADIO) [N/y/?]
IrDA subsystem support (CONFIG_IRDA) [N/y/m/?]
ISDN support (CONFIG_ISDN) [N/y/m/?]
Support non-SCSI/IDE/ATAPI CD-ROM drives (CONFIG_CD_NO_IDESCSI) [N/y/?]
```

![](img/9eb7e89292d2f85707b4d49102c865b7_288_0.png)

> 如果您计划使用 ISDN 卡为服务器提供互联网连接，我强烈建议您购买 ISDN 路由器而不是内部卡。我尝试过几款知名品牌的 ISDN 卡，它们工作得并不好。除了还要处理另一张卡的问题（PC 上的 IRQ 和 I/O 地址资源有限）之外，内部卡与外部 ISDN 路由器之间的价格差异并不显著。

## 输入核心支持

如果您有基于 USB 的人机接口设备（HID），则通过在下方回答 yes (y) 启用其支持：

```
Input core support (CONFIG_INPUT) [N/y/m/?]
```

![](img/9eb7e89292d2f85707b4d49102c865b7_288_1.png)

> 如果您想启用操纵杆支持，请在此启用输入核心支持。

## 字符设备

在本节中，您将被询问终端配置。

```
Virtual terminal (CONFIG_VT) [Y/n/?]
```

此功能允许您拥有虚拟终端。除非您在嵌入式 Linux 系统中安装内核，否则需要默认答案。

```
Support for console on virtual terminal (CONFIG_VT_CONSOLE) [Y/n/?]
```

此功能允许您将虚拟终端转变为系统控制台。出于与上一个答案相同的原因，这是必需的。

```
Support for console on serial port (CONFIG_SERIAL_CONSOLE) [N/y/?]
```

如果您希望使用计算机的串行端口作为系统控制台，请在此选择 yes。

```
Extended dumb serial driver options (CONFIG_SERIAL_EXTENDED) [N/y/?]
```

除非您在上一个问题中将串行端口启用为系统控制台，否则在此选择默认答案。

```
Unix98 PTY support (CONFIG_UNIX98_PTYS) [Y/n/?]
```

此功能提供对 UNIX 98 伪终端编号约定的支持，该约定优于传统的 Linux 伪终端编号约定。您应选择默认答案。

如果您选择默认答案，系统将询问以下问题以设置系统可使用的 UNIX 98 PTY 的最大数量：

```
Maximum number of Unix98 PTYs in use (0-2048) (CONFIG_UNIX98_PTY_COUNT) [256]
```

对于大多数情况，默认值应足够。

## 鼠标支持

如果您的系统连接了鼠标，则在以下提示中选择默认答案是推荐的：

```
Mouse Support (not serial mice) (CONFIG_MOUSE) [Y/n/?]
```

## 操纵杆支持

如果您想启用操纵杆支持，则启用输入核心支持。

## 磁带驱动器支持

如果您有 QIC-02 磁带，可以在此选择添加其支持。

```
QIC-02 tape support (CONFIG_QIC02_TAPE) [N/y/m/?]
```

## 看门狗卡支持

如果您希望创建看门狗计时器以便在故障时重启系统，请在此回答 yes。

```
Watchdog Timer Support (CONFIG_WATCHDOG) [N/y/?]
```

如果您启用此功能，您必须使用 mknod 程序创建一个名为 /dev/watchdog 的特殊设备（major,minor=130,10）。然后，您可以使用看门狗守护程序每分钟向此特殊设备写入数据。如果内核检测到守护程序一分钟未向设备写入数据，则会重启系统。

```
/dev/nvram support (CONFIG_NVRAM) [N/y/m/?]
```

此功能允许您创建特殊设备 /dev/nvram 以对实时时钟中的非易失性存储器进行读写访问。除非您知道自己在做什么，否则选择默认答案。

```
Enhanced Real Time Clock Support (CONFIG_RTC) [N/y/?]
```

此功能允许您创建特殊设备 /dev/rtc，您可以使用它访问系统中的实时时钟。除非您知道自己在做什么，否则选择默认答案。

## Ftape、软盘磁带、视频和杂项设备支持

如果您有基于软盘控制器的磁带驱动器，需要在此选择添加其支持。

```
Ftape (QIC-80/Travan) support (CONFIG_FTAPE) [N/y/m/?]
```

```
/dev/agpgart (AGP Support) (CONFIG_AGP) [Y/m/n/?]
```

AGP（加速图形端口）支持将允许您启用高级 AGP 视频卡功能。如果您有 AGP 视频卡，请选择默认答案。

```
Direct Rendering Manager (XFree86 DRI support) (CONFIG_DRM) [Y/n/?]
```

如果您使用 X Windows 系统（使用 Xfree86），则选择默认答案以启用 Direct Rendering Infrastructure（DRI）支持，该支持通过为视频卡提供安全性、同步和直接内存访问（DMA）传输来增强您的 X 体验。如果您启用此功能，您将需要选择适合您视频卡的模块。

目前支持的卡包括 3dfx Banshee/Voodoo3+、3dlabs GMX 2000、ATI Rage 128、ATI Radeon、Intel I810 以及 Matrox G200/G400。

```
PCMCIA serial device support (CONFIG_PCMCIA_SERIAL_CS) [N/y/m/?]
```

如果您没有 PCMCIA 串行设备，请选择默认答案。

```
Video For Linux (CONFIG_VIDEO_DEV) [N/y/m/?]
```

如果您有视频采集设备，通过选择 yes 启用此选项；否则，选择默认答案。

## 文件系统

在本节中，您为内核配置各种文件系统特定功能。

```
Quota support (CONFIG_QUOTA) [N/y/?]
```

如果您希望内核内置磁盘配额支持，请在此选择 yes。

```
Kernel automounter support (CONFIG_AUTOFS_FS) [Y/m/n/?]
```

如果您希望远程文件系统（如 NFS 文件系统）自动挂载和卸载，请在此选择添加 automounter 的直接或基于模块的支持。此外，对以下问题回答 yes (y)：

```
Kernel automounter version 4 support (also supports v3) (CONFIG_AUTOFS4_FS) [Y/m/n/?]
```

```
Reiserfs support (CONFIG_REISERFS_FS) [N/y/m/?]
```

如果您希望启用日志文件系统支持，请在此选择 yes (y)。

```
ADFS file system support (CONFIG_ADFS_FS) [N/y/m/?]
```

如果您希望支持 Acorn 磁盘文件系统，请启用此选项。

```
Amiga FFS file system support (EXPERIMENTAL) (CONFIG_AFFS_FS) [N/y/m/?]
```

如果您希望支持 Amiga FFS 文件系统，请启用此选项。

```
Apple Macintosh file system support (EXPERIMENTAL) (CONFIG_HFS_FS) [N/y/m/?]
```
