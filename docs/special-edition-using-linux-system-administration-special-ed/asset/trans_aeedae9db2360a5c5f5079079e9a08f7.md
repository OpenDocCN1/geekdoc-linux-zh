
## Alpha、Beta 驱动程序

- AMD AM79C974（PCI）（Compaq、HP、Zeos 板载 SCSI）
  `ftp://metalab.unc.edu/pub/Linux/kernel/patches/scsi/AM79C974-0.3.tgz`
- Adaptec ACB-40xx SCSI-MFM/RLL 桥接板
  `ftp://metalab.unc.edu/pub/Linux/kernel/patches/scsi/adaptec-40xx.tar.gz`
- Always Technologies AL-500
  `ftp://metalab.unc.edu/pub/Linux/kernel/patches/scsi/al500-0.2.tar.gz`
- Iomega PC2/2B
  `ftp://metalab.unc.edu/pub/Linux/kernel/patches/scsi/iomega_pc2-1.1.x.tar.gz`
- Ricoh GSI-8
  `ftp://tsx-11.mit.edu/pub/Linux/ALPHA/scsi/gsi8.tar.gz`

## 不支持

- Adaptec AHA 2940UW Pro
- Adaptec AAA-13x RAID 适配器
- Adaptec AAA-113x RAID 端口卡
- Adaptec AIC-7810
- NCR 53C710 芯片（ISA）（过时的老芯片，但仍在某些 Compaq 型号中使用）
- 非 Adaptec 兼容的 DTC 板卡（327x、328x）

## 控制器（I/O）

任何标准的串行/并行/游戏杆/组合卡均可。Linux 支持 8250、16450、16550 和 16550A UART。支持非标准 IRQ（IRQ 9）的卡也可以使用。

参见 Neal Samuelson 的《Application Note AN-493》，作者 Martin S. Michael。第 5.0 节详细描述了 NS16550 与 NS16550A 之间的差异。简而言之，NS16550 的 FIFO 电路存在缺陷，而 NS16550A（及后续）芯片修复了这些问题。然而，National 很久以前生产的 NS16550 数量极少，因此现在应该非常罕见。而且，现代板卡上实际使用的许多“16550”器件来自众多生产多器件的制造商，可能并不使用 National 的“A”后缀。此外，一些多端口板卡会使用 16552 或 16554，或 National 及其他供应商的各种多端口或多功能芯片（通常为焊接在板上的密集封装，而非 40 引脚 DIP）。除非你遇到一颗非常古老的、散装或装在旧板上的 National“NS16550”（无 A）40 引脚 DIP 芯片，否则不必担心；若真遇到，应将其视为 16450（无 FIFO），而非 16550A——Zdhahai Stewart（zstewart@hisys.com）。

## 控制器（多端口）

### 非智能卡

**支持的型号**

- AST FourPort 及仿制卡（4 端口）
- Accent Async-4（4 端口）
- Arnet Multiport-8（8 端口）
- Bell Technologies HUB6（6 端口）
- Boca BB-1001、1008（4、8 端口）- 无 DTR、DSR 和 CD
- Boca BB-2016（16 端口）
- Boca IO/AT66（6 端口）
- Boca IO 2by4（4 串口/2 并口，使用 5 个 IRQ）
- Computone ValuePort（4、6、8 端口）（与 AST FourPort 兼容）
- DigiBoard PC/X、PC/Xem、PCI/Xem、EISA/Xem、PCI/Xr（4、8、16 端口）
- Control Hostess 550（4、8 端口）
- PC-COMM 4 端口（4 端口）
- SIIG I/O Expander 4S（4 端口，使用 4 个 IRQ）
- STB 4-COM（4 端口）
- Twincom ACI/550
- Usenet Serial Board II（4 端口）

非智能卡通常有两种类型：一种使用标准 COM 端口地址和 4 个 IRQ；另一种与 AST FourPort 兼容，使用可选的地址块和单个 IRQ。（地址和 IRQ 通过 setserial 设置。）如果你要购买这类卡，务必确认它符合哪种标准；价格并不能说明问题。

### 智能卡

**支持的型号**

- Computone IntelliPort II（4/8/16 端口）
  `ftp://ftp.computone.com/pub/bbs/beta/ip2linux-1.0.2.tar.gz`
- Cyclades Cyclom-Y（基于 RISC，8-32 端口）（ISA/PCI）
  `http://www.cyclades.com/`
- Cyclades-Z（高端，16-64 端口）（PCI）
  `http://www.cyclades.com/`
- DigiBoard PC/Xe（ISA）、PC/Xi（EISA）和 PC/Xeve
  `ftp://ftp.digibd.com/drivers/linux/`
- Equinox SST 智能串行 I/O 卡
  `http://www.equinox.com`
- Hayes ESP 1、2 和 8 端口版本
  自 2.1.15 起包含在内核中。适用于 2.0.x 内核版本的驱动程序可在以下位置找到：
  `http://www.nyx.net/~arobins...`
- Stallion EasyIO（ISA）/EasyConnection 8/32（ISA/MCA）/EasyConnection 8/64（PCI）
  有关 DIP 开关设置和配置文件，请查看 `http://www.stallion.com`。
- Stallion EasyConnection 8/64（ISA/EISA）/OnBoard（ISA/EISA）/Brumby（ISA）
  最新驱动程序可在 `ftp://ftp.stallion.com/drivers/ata5/Linux/v544.tar.gz` 找到。

## Alpha、Beta 驱动程序

- Control RocketPort（8/16/32 端口）
  `ftp://metalab.unc.edu/pub/Linux/kernel/patches/serial/control-1.04.tar.gz`（适用于 1.2.x 内核）。适用于 2.x 内核的驱动程序可在以下位置找到：
  `http://ftp.leidenuniv.nl/linux/tsx-11/packages/control/.`
- DigiBoard COM/Xi
- Moxa C102、C104、C168、C218（8 端口）、C320（8/16/24/32 可扩展）和 C320T
  `ftp://ftp.moxa.com.tw/drivers/linux/`
- RISCcom/8
- Specialix SIO/XIO（模块化，4 到 32 端口）
  `ftp://metalab.unc.edu/pub/Linux/kernel/patches/serial/sidrv.taz`
- Specialix IO8+
  - 联系 `devices@BitWizard.nl`。

## 网络适配器

以太网适配器的性能差异很大。一般来说，设计越新越好。有些非常老的卡，如 3Com 3c501，之所以还有用，只因为能在废品堆里以每个 5 美元的价格找到。对兼容卡要小心——并非所有兼容卡都是好的，劣质兼容卡在 Linux 下常常导致莫名其妙的死机。请阅读 Ethernet HOWTO（`http://metalab.unc.edu/LDP/HOWTO`），了解各种网卡的详细说明。

### 支持的以太网

对于采用 DECchip DC21x4x 系列的以太网卡，可使用“Tulip”驱动程序。有关此驱动程序的更多信息，请访问 http://cesdis.gsfc.nasa.gov/linux/drivers/tulip.html。

- 3Com 3c501——尽量避而远之（3c501 驱动）
- 3Com 3c503（3c503 驱动）、3c505（3c505 驱动）、3c507（3c507 驱动）、3c509/3c509B（ISA）/3c579（EISA）
- 3Com Etherlink III Vortex 以太网卡（3c590、3c592、3c595、3c597）（PCI）、3Com Etherlink XL Boomerang（3c900、3c905）（PCI）和 Cyclone（3c905B、3c980）以太网卡（3c59x 驱动）以及 3Com Fast EtherLink 以太网卡（3c515）（ISA）（3c515 驱动）
  - 这些驱动程序的更新版本可在 http://cesdis.gsfc.nasa.gov/linux/drivers/vortex.html 获取。
  - 尽量避开 3c900 卡，因为驱动程序对该卡支持不佳。
- 3Com 3cFE575 Cyclone Cardbus（3c59x 驱动）
- 3Com 3c575 系列 Cardbus（3c59x 驱动）（全部 PCMCIA ??）
- AMD LANCE（79C960）/ PCnet-ISA/PCI（AT1500、HP J2405A、NE1500/NE2100）
- AT&T GIS WaveLAN
- Allied Telesis AT1700
- Allied Telesis LA100PCI-T
- Allied Telesyn AT2400T/BT（“ne”模块）
- Ansel Communications AC3200（EISA）
- Apricot Xen-II / 82596
- Cabletron E21xx
- Cogent EM110
- Crystal Lan CS8920、Cs8900
  - http://www.cirrus.com/private/drivers/ethernet/edrivers.html
- Danpex EN-9400
- DEC DE425（EISA）/DE434/DE435（PCI）/DE450/DE500（DE4x5 驱动）
- DEC DE450/DE500-XA（dc21x4x）（Tulip 驱动）
- DEC DEPCA 和 EtherWORKS
- DEC EtherWORKS 3（DE203、DE204、DE205）
- DEC QSilver（Tulip 驱动）
- Digi International RightSwitch
- DLink DE-220P、DE-528CT、DE-530+、DFE-500TX、DFE-530TX
  - 更多信息请参见 `http://www.dlink.ca/linux.html`。
- Fujitsu FMV-181/182/183/184
- HP PCLAN（27245 和 27xxx 系列）
- HP PCLAN PLUS（27247B 和 27252A）
- HP 10/100VG PCLAN（J2757、J2573、27248B、J2585）（**ISA/EISA/PCI**）
  - 更多信息请参见 `http://cesdis1.gsfc.nasa.gov:80/linux/drivers/100vg.html`。
- ICL EtherTeam 16i/32（**EISA**）
- Intel EtherExpress
- Intel EtherExpress Pro
- KTI ET16/P-D2、ET16/P-DC ISA（无需跳线，且支持硬件配置选项）
- Macromate MN-220P（PnP 或 NE2000 模式）
- NCR WaveLAN
- NE2000/NE1000（注意仿冒品）
- Netgear FA-310TX（Tulip 芯片）
- New Media Ethernet
- PureData PDUC8028、PDI8023
- SEEQ 8005
- SMC Ultra/EtherEZ（ISA）
- SMC 9000 系列
- SMC PCI EtherPower 10/100（Tulip 驱动）
- SMC EtherPower II（epic100.c 驱动）
- Sun LANCE 适配器（内核 2.2 及更高版本）
- Sun Intel 适配器（内核 2.2 及更高版本）
- Schneider & Koch G16
- Western Digital WD80x3
- Zenith Z-Note/IBM ThinkPad 300 内置适配器
- Znyx 312 etherarray（Tulip 驱动）

### ISDN

- Linux ISDN WWW 页面
    - 这个页面似乎已经不存在了。
- ISDN4Linux 工具可从 `ftp://ftp.franken.de/pub/isdn4linux/v2.0` 获取。

