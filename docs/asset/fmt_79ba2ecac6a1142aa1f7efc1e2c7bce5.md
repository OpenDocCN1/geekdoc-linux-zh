
这里，`token` 可以是 `error`、`scan`、`mlqueue`、`mlcomplete`、`llqueue`、`llcomplete`、`hlqueue` 或 `hlcomplete`。`level` 控制日志的详细程度，可以是包括 0 在内的任何正数。

SCSI 部分中的其余问题特定于 SCSI 主机适配器。您应仅为已安装的适配器选择支持。

## 网络设备支持

在本节中，您配置各种网络设备功能。

`CONFIG_NETDEVICES` [Y/n/?]

由于您正在为服务器配置内核，请对上一个问题回答 Y。

`CONFIG_ARCNET` [N/y/m/?]

除非您拥有 ARCnet 网络接口卡，否则默认值 N 就足够了。

### 伪网卡驱动支持

`CONFIG_DUMMY` [M/n/y/?]

该驱动程序创建一个伪网络接口设备，可用于欺骗网络客户端程序。将此作为模块保留可能会很有用；因此，推荐使用默认值 M。

### EQL（串行线路负载均衡）支持

`CONFIG_EQUALIZER` [N/y/m/?]

此功能对大多数服务器配置没有用。推荐使用默认答案。

### 以太网（10 或 100Mbit）

`CONFIG_NET_ETHERNET` [Y/n/?]

如果您要在以太网上使用系统，请选择默认答案 Y。

以下问题的答案取决于您拥有的网络卡类型；因此，请相应回答：

- `CONFIG_NET_VENDOR_3COM` [N/y/?]
- `CONFIG_LANCE` [N/y/m/?]
- `CONFIG_NET_VENDOR_SMC` [N/y/?]
- `CONFIG_NET_VENDOR_RACAL` [N/y/?]
- `CONFIG_NET_ISA` [N/y/?]
- `CONFIG_NET_EISA` [Y/n/?]
- `CONFIG_PCNET32` [N/y/m/?]
- `CONFIG_APRICOT` [N/y/m/?]
- `CONFIG_CS89x0` [N/y/m/?]
- `CONFIG_DE4X5` [N/y/m/?]
- `CONFIG_DEC_ELCP` [N/y/m/?]

`CONFIG_DGRS` [N/y/m/?]
`CONFIG_EXPRESS_PRO100` [Y/m/n/?]
`CONFIG_NE2K_PCI` [N/y/m/?]
`CONFIG_TLAN` [N/y/m/?]
`CONFIG_VIA_RHINE` [N/y/m/?]
`CONFIG_NET_POCKET` [N/y/?]
`CONFIG_FDDI` [N/y/?]
`CONFIG_DLCI` [N/y/m/?]
`CONFIG_PPP` [N/y/m/?]
`CONFIG_SLIP` [N/y/m/?]
`CONFIG_NET_RADIO` [N/y/?]
`CONFIG_TR` [N/y/?]
`CONFIG_HOSTESS_SV11` [N/m/?]
`CONFIG_COSA` [N/m/?]
`CONFIG_RCPCI` [N/y/m/?]
`CONFIG_WAN_DRIVERS` [N/y/?]
`CONFIG_LAPBETHER` [N/y/m/?]
`CONFIG_X25_ASY` [N/y/m/?]

## 业余无线电、ISDN 和旧 CD-ROM 支持

假设您不会使用业余无线电、ISDN 或旧 CD-ROM 支持，以下问题的默认答案就足够了：

- `CONFIG_HAMRADIO` [N/y/?]
- `CONFIG_ISDN` [N/y/m/?]
- `CONFIG_CD_NO_IDESCSI` [N/y/?]

![](img/c2419364ebb911c809b6a79991707c27_536_0.png)

### 提示

如果您计划使用 ISDN 卡为系统提供 Internet 连接，请获取 ISDN 路由器而不是内部卡。我与内部卡的个人经验使我得出这一结论。我尝试过一些知名品牌的 ISDN 卡，它们工作得并不好。除了处理另一张卡（PC 上的 IRQ 和 I/O 地址资源有限）的问题外，当考虑到在美国大部分地区专用 ISDN 本身就是一项相当昂贵的服务时，内部卡与外部 ISDN 路由器之间的价格差异并不显著。

## 字符设备

在本节中，您将被询问终端配置。

### 虚拟终端

`CONFIG_VT` [Y/n/?]

此功能允许您拥有虚拟终端。除非您在嵌入式 Linux 系统中安装内核，否则需要默认答案。

### 虚拟终端上控制台支持

`CONFIG_VT_CONSOLE` [Y/n/?]

此功能允许您将虚拟终端转变为系统控制台。这与上一个答案的原因相同。

### 串行端口上控制台支持

`CONFIG_SERIAL_CONSOLE` [N/y/?]

如果您想使用计算机的串行端口作为系统控制台，请选择 y。

### 扩展哑串行驱动程序选项

`CONFIG_SERIAL_EXTENDED` [N/y/?]

### Unix98 PTY 支持

`CONFIG_UNIX98_PTYS` [Y/n/?]

此功能提供对 UNIX 98 伪终端编号约定的支持，该约定优于传统的 Linux 伪终端编号约定。您应保留默认值。

如果您保留默认值，系统会询问您以下问题，以设置系统可使用的 UNIX 98 PTY 的最大数量：

### 使用中的 Unix98 PTY 的最大数量 (0-2048)

`CONFIG_UNIX98_PTY_COUNT` [256]

对于大多数情况，默认值应该足够。

### 鼠标支持（非串行鼠标）

`CONFIG_MOUSE` [Y/n/?]

此功能允许您在能够使用此类设备的终端上使用鼠标。推荐默认值。

### QIC-02 磁带支持

`CONFIG_QIC02_TAPE` [N/y/m/?]

如果您有 QIC-02 磁带，可以在此处选择添加对其的支持。

### 看门狗定时器支持

`CONFIG_WATCHDOG` [N/y/?]

如果您想创建一个看门狗定时器以便在故障时重启系统，请在此处回答 y。如果您启用此功能，则必须使用 `mknod` 程序创建一个名为 `/dev/watchdog` 的特殊设备（major,minor=130,0）。然后，您可以使用看门狗守护程序，每分钟向此特殊设备写入一次。如果内核检测到守护程序一分钟内未向设备写入，它将重启系统。

### /dev/nvram 支持

`CONFIG_NVRAM` [N/y/m/?]

此功能允许您创建一个特殊设备 `/dev/nvram`，从而可以读取/写入实时时钟中的非易失性内存。除非您知道自己在做什么，否则请保留默认值。

### 增强实时时钟支持

`CONFIG_RTC` [N/y/?]

此功能允许您创建一个特殊设备 `/dev/rtc`，可用于访问系统中的实时时钟。除非您知道自己在做什么，否则请保留默认值。

## 视频和操纵杆支持

您可能没有视频采集硬件或操纵杆，因此应接受以下问题的默认答案：

`CONFIG_VIDEO_DEV` [N/y/m/?]

`CONFIG_JOYSTICK` [N/y/m/?]

## Ftape，软盘磁带设备驱动程序

如果您拥有基于软盘控制器的磁带驱动器，则需要在此处选择添加对其的支持：

`CONFIG_FTAPE` [N/y/m/?]

## 文件系统

在本节中，您为各种文件系统特定功能配置内核。

`CONFIG_QUOTA` [N/y/?]

如果您希望内核内置磁盘配额支持，请在此处输入 y。

`CONFIG_AUTOFS_FS` [Y/m/n/?]
