
## SCSI 控制器

- 带有 AHA-777x (EISA), AHA-785x, AHA-787x (PCI), AHA-788x (PCI) 的 Adaptec 板控制器
- Always IN2000
- BusLogic (ISA/EISA/VLB/PCI) (所有型号)
- DPT PM2001, PM2012A (EATA-PIO)
- DPT Smartcache/SmartRAID Plus,III,IV 系列 (ISA/EISA/PCI)。请查看 `http://www.uni-mainz.de/-neuffer/scsi/dpt/` (EATA-DMA)
- 这些系列的卡包括 PM2011, PM2021, PM2041, PM3021, PM2012B, PM2022, PM2122, PM2322, PM3122, PM3222, PM3332, PM2024, PM2124, PM2044, PM2144, PM3324, PM3334
- DTC 329x (与 Eisa 154 兼容)
- Future Domain TMC-16x0, TMC-3260 (PCI)
- Future Domain TMC-8xx, TMC-950
- ICP-Vortex PCI-SCSI 磁盘阵列控制器（支持许多 RAID 级别）

Linux 1.2.13 和 2.0.29 的补丁可用：`http://icp-vortex.com/download/linux/linux/`。支持控制器 GDT6311RP, GDT6211RP, GDT6117RP, GDT6127RP, GDT6511RP, GDT6521RP, GDT6527RP, GDT6537RP 和 GDT6557RP。你也可以使用预补丁-2.0.31-4 到预补丁-2.0.31-9。

- ICP-Vortex EISA-SCSI 控制器（支持许多 RAID 级别）
- Linux 1.2.13 和 2.0.29 的补丁可用：`http://icp-vortex.com/download/linux/`。支持控制器 GDT3000B, GDT3000A, GDT3010A, GDT3020A 和 GDT3050A。你可以使用预补丁-2.0.31-4 到预补丁-2.0.31-9。
- Media Vision Audio Spectrum 16 (ISA)
- NCR 5380
- NCR 53C400 (Trant 130B) (使用通用 NCR 5380)
- NCR 53C56 (Assist / Media Vision 3D)
- NCR 53Cx
- NCR 53C810, 53C815, 53C820, 53C25, 53C860, 53C75, 53C95
- Qlogic Control/IDE (FAS408) (ISA/VLB)
- Quantum ISA-2005, ISA-250
- Seagate ST-01/ST-02 (ISA)
- SoundBlaster 16-2 (与 Adaptec 152 兼容) (ISA)
- Tekram DC-390, DC-390/U/F
- Trant T128/T128F/T28 (ISA)
- UltraStor 14F (ISA), 24F (EISA), 34F (VLB)
- Western Digital WD7000 SCSI
- AMD AM53C974, AM79C74 (PCI) (Compaq, HP, Zeos 板载 SCSI)
- Adapec AC-40XX
- Always Technologies AL-500
- BusLogic (ISA/EISA/VLB/PCI) (新驱动)
- Iomega PC2/2B
- Qlogic ISP1020 (PCI)
- Ricoh GSI-8
- 并口适配器
- 非 Adaptec DTC (327x, 328x)

# 控制器 (I/O)

任何标准的串口/并行/摇杆/组合卡支持 8250, 16450, 16550 和 16550A。支持非标准中断 (IRQ > 9) 的卡可以使用。参考 Martin S. Michael 写的 National Semiconductor“Application Note AN-493”。第5.0节描述了 NS1650 和 NS1650A 之间的差异。简而言之，NS1650 在 FIFO 电路中有 Bug（后来已修复）。National 生产的 NS16550 已经非常罕见。许多现代板卡上的“16550 部”来自许多兼容制造商，可能不使用 National“A”后缀。此外，某些多端口板卡将使用 16552 或 16554 或其他供应商的多端口芯片（通常是焊接在板卡上的 40 脚 DIP 封装）。除非遇到非常老的 National“NS16550”（无 A）独立芯片或在旧板上，否则将其视为 16450（无 FIFO）而非 16550A。

# 控制器 (多端口)

## 非智能卡 - 已支持

- Network Serial Board II (4端口)

非智能卡通常有两种：一种使用标准串口地址和四个中断，另一种是兼容 AST FourPort 并使用可选地址块和单个中断。（地址和中断使用 `setserial` 设置）。如果你获得了这些卡之一，请确保检查它符合哪种标准；价格没有参考。

## 智能卡 - 已支持

- Computune IntelliPort II (4/8/16端口)

  `ftp://ftp.computune.com/pub/bbs/beta/ip2linux-1.0.2.tar.gz`
- Cyclades Cyclom-8Y/16Y, (16端口) (ISA/PCI)
- DigiBoard PC/Xe (ISA), PC/Xi (EISA) 和 PC/Xeve
- Equinox SST
- Hayes-- (ISA)
- Moxa C102, C104, C168, C218 (8), C320 (ISA)
- Zynx 312 etherarray

# 网络适配器

以太适配器的性能差异很大。通常情况下，设计越新越好。某些旧卡如 3C501 唯一的用处是因为可以在垃圾堆中 5 美元买到。小心对待仿制品——并非所有的都是好的，劣质仿制品经常会导致死机。阅读 Ethernet HOWTO (`http://sunsite.unc.edu/LDP/HOWTO/`) 以详细描述各种卡。

## 已支持

### 以太

- 对于 DECchip DC2x4 系列以太卡，提供了“Tulip”驱动。
- 关于该驱动的更多信息可以在 `http://csdis.gfc.nasa.gov/drivers/tulip.html` 找到。
- Zynx 312

### ISDN

- ISDN 页 `http://www.ix.de/ix/linux-isdn.html`
- Teles 50 `ftp://ftp.franken.de/pub/isdn4linux/`
- 模拟标准调制解调器或常见以太适配器的 ISDN 卡不需要特殊驱动即可工作。

### 口袋和便携式适配器

- 关于 Linux 和并行口的使用信息，请访问 Linux Parallel 主页。
- `http://www.torque.net/linux-pp.html`
- D-Link DE600/DE620 并口适配器

### 无槽

- PLIP (并行口) - 使用“LapLink 线”或双向电缆

### ARCnet

- 与所有 ARCnet 卡兼容

### TokenRing

- 任何不使用 DMA 的 IBM tokenring 卡
- IBM Tropic 芯片卡
- Madge TokenRing OCI 16/4 Mk2

### FDDI

- DEC DEFEA (EISA) / DEFPA (PCI) (内核 2.0.24 及更高版本)

### 业余无线 (AX.25)

- 大多数通用的基于 8530 的 HDLC 板

# PCMIA 卡

- 完整列表请参见附录 B。

# 其他

## 以太网

- Racal-Interlan PCI 卡 (AMD PC 网芯片 97c9970)

## ISDN

- SpellCaster's Datacomute/BRI, Telecomute/BRI (ISA)

  `ftp://ftp.franken.de/pub/isdn4linux/`

## ATM

- Efficient Networks ENI155P-MF 155Mbps ATM 适配器 (PCI)

  `http://ircww.epfl.ch/linux-atm/`

## 帧中继

- Sangoma S502 56K 帧中继卡

  `ftp://ftp.sovereign.org/pub/wan/fr/`

## 无线

- Proxim RangeLan2 7100 (ISA) / 630x (OEM mini-ISA)

  `http://www.komacke.com/distribution.html`

## 不支持

- Sysconnect/ Schneider & Koch 令牌环卡（所有）

# 声卡

## 支持

- 6850 UART MIDI
