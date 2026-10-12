
# 第五部分

## 重新编译内核 第III

CCITT X.25 数据层（实验性）(`CONFIG_X25`) [N/y/?]

LAP 数据链路驱动（实验性）(`CONFIG_LAPB`) [N/y/?]

桥接（Bridging）（实验性）(`CONFIG_BRIDGE`) [N/y/?]

802.2 LLC（实验性）(`CONFIG_LLC`) [N/y/?]

Acorn Econet/AUN 协议（实验性）(`CONFIG_ECONET`) [N/y/?]

WAN 路由器 (`CONFIG_WAN_ROUTER`) [M/n/?]

快速切换（查看帮助！）(`CONFIG_NET_FASTROTETE`) [N/y/?]

高速接口之间的转发（`CONFIG_NET_FLOWCONTROL`） [N/m/?]

CPU 处理全带宽太慢（`CONFIG_CPU_IS_SLOW`） [N/y/?]

这些选项仅供精通用户使用。IPX 可配合程序为 Novell 提供服务。其他的最好关闭。脚本的后续部分允许你为内核配置通用 SCSI 支持：

- SCSI 支持
- SCSI 支持 (`CONFIG_SCSI`) [Y/m/n/?]
- SCSI 支持类型（磁盘、磁带、光驱）

SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y/m/n/?]

SCSI 磁带支持 (`CONFIG_CHR_DEV_ST`) [Y/m/n/?]

SCSI 光驱支持 (`CONFIG_BLK_DEV_SR`) [Y/m/n/?]

厂商特定扩展（用于 SCSI 光驱）(`CONFIG_BLK_DEV_SR`) [N/y/?]

SCSI 通用支持 (`CONFIG_CHR_DEV_SG`) [M/n/y/?]

某些 SCSI 设备（例如 CD jukebox）支持多个 LUN

在每个 SCSI 设备上探测所有 LUN (`CONFIG_SCSI_MULTI_LUN`) [Y/n/?]

详细 SCSI 错误报告（内核大小 +12K)(`CONFIG_SIZE_CONSTANTS`) [Y/n/?]

这些选项涵盖了 Linux 下 SCSI 驱动和设备的常用功能。选择取决于你的硬件，但出于性能和内核大小考虑，建议关闭详细 SCSI 报告。

# 第五部分

## 重新编译内核 第III

如果你对 SCSI 支持回答了 Y，现在提示指定你系统的实际 SCSI 卡或芯片：

- SCSI 底层驱动

7000FASST SCSI 支持 (`CONFIG_SCSI_7000FASST`) [M/n/y/?]

ACARD SCSI 支持 (`CONFIG_SCSI_ACARD`) [M/n/y/?]

Adptec AHA152X/2825 支持 (`CONFIG_SCSI_AHA52X`) [M/n/y/?]

Adptec AHA1542 支持 (`CONFIG_SCSI_AHA1542`) [M/n/y/?]

Adptec AHA1740 支持 (`CONFIG_SCSI_AHA1740`) [M/n/y/?]

Adptec AIC77xxx 支持 (`CONFIG_SCSI_AIC77XXX`) [M/n/y/?]

- 默认启用命令队列 (TQ) (`CONFIG_AIC77XXX_TCQ_ON_BY_DEFAULT`) [N/y/?]
- 每个设备的最大 TQ 命令数 (`CONFIG_AIC77XXX_CMDS_PER_DEVICE`) [8]
- 收集统计并在 `/proc` 中 (`CONFIG_AIC77XXX_PROC_STATS`) [Y/n/y/?]
- SCSI 总线重置后的延迟（秒）(`CONFIG_AIC77XXX_RETRIES_DELAY`) [5]

AdvanSys SCSI 支持 (`CONFIG_SCSI_ADVIANS`) [M/n/y/?]

始终支持 In2000 SCSI (`CONFIG_SCSI_IN2000`) [M/n/y/?]

AM53/79C74 支持 (`CONFIG_SCSI_AM53C974`) [M/n/y/?]

AMI MegaRaid (`CONFIG_SCSI_MEGARADA`) [M/n/y/?]

BusLogic 支持 (`CONFIG_SCSI_BUSLOGIC`) [M/n/y/?]

跳过 Flash 支持 (`CONFIG_SCSI_OMIT_FLASH`) [N/y/?]

HTC3180/3280 SCSI 支持 (`CONFIG_SCSI_DTC3280`) [M/n/y/?]

EATA/PCI（以及 EATA 数据）支持 (`CONFIG_SCSI_EATA`) [M/n/y/?]

- 别名（`CONFIG_SCSI_TAG`） [Y/n/?]
- 别名排序（`CONFIG_SCSI_SORT`） [N/y/?]
- EATA 上的命令数（`CONFIG_SCSI_MAX`） [16]
- EATA（DPT, STI, Olivell）支持（`CONFIG_SCSI_DATA`） [M/n/y/?]
- EATA-PIO（`CONFIG_SCSI_PIO`） [M/n/y/?]

Future Domain 196x（`CONFIG_SCSI_DOMAIN`） [N/y/?]

GDT 矩阵（`CONFIG_SCSI_GDT`） [N/y/?]

通用 NCR53c40（`CONFIG_SCSI_GENERIC`） [N/y/?]

- 启用 53c40 扩展 (`CONFIG_AIC77XXX`) [N/y/?]
- 53c40 的类似方法（`CONFIG_SCSI_PORT`） [M/n/y]
- 0 0 1000（`CONFIG_SCSI_1000`） [M/n/?]

# 第五部分 系统管理

## 第31 章 管理内核

IPX 协议 (`CONFIG_IPX`) [M/n/?]

IPX: 全内部 IPX 网络 (`CONFIG_IPX_INTERN`) [N/y/?]

IPX: SPX 网络（实验性）(`CONFIG_SPX`) [N/y/?]

Appletek DPP (`CONFIG_TALK`) [M/n/?]

CCITT X.25 数据层（实验性）(`CONFIG_X25`) [N/y/?]

LAP 数据链路驱动（实验性）(`CONFIG_LAPB`) [N/y/?]

桥接（Bridging）（实验性）(`CONFIG_BRIDGE`) [N/y/?]

802.2 LLC（实验性）(`CONFIG_LLC`) [N/y/?]

Acorn Econet/AUN 协议（实验性）(`CONFIG_ECONET`) [N/y/?]

WAN 路由器 (`CONFIG_WAN_ROUTER`) [M/n/?]

快速切换（查看帮助！）(`CONFIG_NET_FASTROTETE`) [N/y/?]

高速接口之间的转发（`CONFIG_NET_FLOWCONTROL`） [N/m/?]

CPU 处理全带宽太慢（`CONFIG_CPU_IS_SLOW`） [N/y/?]

这些选项仅供精通用户使用。IPX 可配合程序为 Novell 提供服务。其他的最好关闭。脚本的后续部分允许你启用其他网络协议和其他内核功能：

- SCSI 支持
- SCSI 支持 (`CONFIG_SCSI`) [Y/m/n/?]
- SCSI 支持类型（磁盘、磁带、光驱）

SCSI 磁盘支持 (`CONFIG_BLK_DEV_SD`) [Y/m/n/?]

SCSI 磁带支持 (`CONFIG_CHR_DEV_ST`) [Y/m/n/?]

SCSI 光驱支持 (`CONFIG_BLK_DEV_SR`) [Y/m/n/?]

厂商特定扩展（用于 SCSI 光驱）(`CONFIG_BLK_DEV_SR`) [N/y/?]

SCSI 通用支持 (`CONFIG_CHR_DEV_SG`) [M/n/y/?]

某些 SCSI 设备（例如 CD jukebox）支持多个 LUN

在每个 SCSI 设备上探测所有 LUN (`CONFIG_SCSI_MULTI_LUN`) [Y/n/?]

详细 SCSI 错误报告（内核大小 +12K)(`CONFIG_SIZE_CONSTANTS`) [Y/n/?]

# 第五部分

## 重新编译内核 第13章

带有你系统的 SCSI 驱动程序的内存磁盘（ramdisk）。使用此内存磁盘是因为它包含了支持 SCSI 所需模块。在 Linux 内核启动之前，引导程序会读取该内存磁盘。

然而，如果你不想对启动设备使用 SCSI 模块，请确保你已删除 `/boot` 目录下的 `initrd-kernel_version.img` 文件，或者你已经在内核中关闭了 initrd 支持。否则，内核内置的设备驱动程序将初始化该设备，随后初始内存磁盘包含的设备驱动程序将尝试执行相同的操作并失败。这本身并不是那么糟糕，但这种失败的驱动加载将触发内核恐慌（kernel panic）。如果你可以在 LILO 命令行中使用 `noinitrd` 选项从命令行启动内核镜像，则可以忽略删除 `initrd-kernel_version.img` 文件。

这里的在线帮助对于提供额外配置选项的驱动非常有帮助。通常情况下，标记命令队列（Tagged Command Queuing）是你应该启用以获得最佳的选项，但请检查其他选项，确保驱动中没有其他会影响此的因素。

内核配置现在带我们进入网络设备的选择：

- * 网络设备支持
- * 网络设备支持 (`CONFIG_DEVICES`) [Y/n/]
